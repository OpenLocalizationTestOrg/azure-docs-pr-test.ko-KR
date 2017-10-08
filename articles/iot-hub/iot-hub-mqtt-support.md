---
title: "Azure IoT 허브 MQTT 지원 aaaUnderstand | Microsoft Docs"
description: "개발자 가이드-장치에서 사용 하 여 IoT Hub 장치 쪽 끝점 tooan 연결 hello MQTT 프로토콜에 대 한 지원. Azure IoT 장치 Sdk hello에 기본 제공 MQTT 지원에 대 한 정보를 포함 합니다."
services: iot-hub
documentationcenter: .net
author: kdotchkoff
manager: timlt
editor: 
ms.assetid: 1d71c27c-b466-4a40-b95b-d6550cf85144
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: kdotchko
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e461687963138987acdf1f4e0e34c453744ea191
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="communicate-with-your-iot-hub-using-hello-mqtt-protocol"></a><span data-ttu-id="3878a-104">Hello MQTT 프로토콜을 사용 하 여 IoT 허브와 통신</span><span class="sxs-lookup"><span data-stu-id="3878a-104">Communicate with your IoT hub using hello MQTT protocol</span></span>

<span data-ttu-id="3878a-105">IoT Hub hello를 사용 하 여 hello IoT Hub 장치 끝점을 장치 toocommunicate 있습니다 [MQTT v3.1.1] [ lnk-mqtt-org] 8883 포트 또는 포트 443에서 WebSocket 프로토콜을 통해 MQTT v3.1.1에서 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-105">IoT Hub enables devices toocommunicate with hello IoT Hub device endpoints using hello [MQTT v3.1.1][lnk-mqtt-org] protocol on port 8883 or MQTT v3.1.1 over WebSocket protocol on port 443.</span></span> <span data-ttu-id="3878a-106">IoT Hub는 TLS/SSL을 사용 하 여 보안 하는 모든 장치 통신 toobe 필요 (따라서 IoT Hub 지원 하지 않습니다 비보안 연결 1883 포트를 통해).</span><span class="sxs-lookup"><span data-stu-id="3878a-106">IoT Hub requires all device communication toobe secured using TLS/SSL (hence, IoT Hub doesn’t support non-secure connections over port 1883).</span></span>

## <a name="connecting-tooiot-hub"></a><span data-ttu-id="3878a-107">TooIoT 허브 연결</span><span class="sxs-lookup"><span data-stu-id="3878a-107">Connecting tooIoT Hub</span></span>

<span data-ttu-id="3878a-108">장치 צ ְ ײ hello MQTT 프로토콜 tooconnect tooan IoT hub hello에서 hello 라이브러리를 사용 하 여 [Azure IoT Sdk] [ lnk-device-sdks] 또는 직접 hello MQTT 프로토콜을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-108">A device can use hello MQTT protocol tooconnect tooan IoT hub either by using hello libraries in hello [Azure IoT SDKs][lnk-device-sdks] or by using hello MQTT protocol directly.</span></span>

## <a name="using-hello-device-sdks"></a><span data-ttu-id="3878a-109">Hello 장치 Sdk를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="3878a-109">Using hello device SDKs</span></span>

<span data-ttu-id="3878a-110">[장치 Sdk] [ lnk-device-sdks] 해당 지원 hello MQTT 프로토콜은 Java, Node.js, C, C#, 및 Python에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-110">[Device SDKs][lnk-device-sdks] that support hello MQTT protocol are available for Java, Node.js, C, C#, and Python.</span></span> <span data-ttu-id="3878a-111">hello 장치 Sdk hello 표준 IoT 허브 연결 문자열 tooestablish 연결 tooan IoT 허브를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-111">hello device SDKs use hello standard IoT Hub connection string tooestablish a connection tooan IoT hub.</span></span> <span data-ttu-id="3878a-112">toouse hello MQTT 프로토콜 hello 클라이언트 프로토콜 매개 변수 설정 해야 너무**MQTT**합니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-112">toouse hello MQTT protocol, hello client protocol parameter must be set too**MQTT**.</span></span> <span data-ttu-id="3878a-113">IoT Hub tooan hello로 hello 장치 Sdk 기본적으로 연결 **CleanSession** 플래그가 설정 너무**0** 사용 하 여 **QoS 1** hello IoT hub와 메시지 교환에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-113">By default, hello device SDKs connect tooan IoT Hub with hello **CleanSession** flag set too**0** and use **QoS 1** for message exchange with hello IoT hub.</span></span>

<span data-ttu-id="3878a-114">장치가 IoT 허브 연결된 tooan 면 hello 장치 Sdk tooand IoT 허브에서 메시지를 수신 하는 hello 장치 toosend 메시지를 사용할 수 있는 메서드를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-114">When a device is connected tooan IoT hub, hello device SDKs provide methods that enable hello device toosend messages tooand receive messages from an IoT hub.</span></span>

<span data-ttu-id="3878a-115">hello 다음 표에 포함 되어 링크 toocode 샘플 각 지원 되는 언어 및 hello 매개 변수 toouse tooestablish 연결 tooIoT 허브 지정에 대 한 hello MQTT 프로토콜을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-115">hello following table contains links toocode samples for each supported language and specifies hello parameter toouse tooestablish a connection tooIoT Hub using hello MQTT protocol.</span></span>

| <span data-ttu-id="3878a-116">언어</span><span class="sxs-lookup"><span data-stu-id="3878a-116">Language</span></span> | <span data-ttu-id="3878a-117">프로토콜 매개 변수</span><span class="sxs-lookup"><span data-stu-id="3878a-117">Protocol parameter</span></span> |
| --- | --- |
| <span data-ttu-id="3878a-118">[Node.js][lnk-sample-node]</span><span class="sxs-lookup"><span data-stu-id="3878a-118">[Node.js][lnk-sample-node]</span></span> |<span data-ttu-id="3878a-119">azure-iot-device-mqtt</span><span class="sxs-lookup"><span data-stu-id="3878a-119">azure-iot-device-mqtt</span></span> |
| <span data-ttu-id="3878a-120">[Java][lnk-sample-java]</span><span class="sxs-lookup"><span data-stu-id="3878a-120">[Java][lnk-sample-java]</span></span> |<span data-ttu-id="3878a-121">IotHubClientProtocol.MQTT</span><span class="sxs-lookup"><span data-stu-id="3878a-121">IotHubClientProtocol.MQTT</span></span> |
| <span data-ttu-id="3878a-122">[C][lnk-sample-c]</span><span class="sxs-lookup"><span data-stu-id="3878a-122">[C][lnk-sample-c]</span></span> |<span data-ttu-id="3878a-123">MQTT_Protocol</span><span class="sxs-lookup"><span data-stu-id="3878a-123">MQTT_Protocol</span></span> |
| <span data-ttu-id="3878a-124">[C#][lnk-sample-csharp]</span><span class="sxs-lookup"><span data-stu-id="3878a-124">[C#][lnk-sample-csharp]</span></span> |<span data-ttu-id="3878a-125">TransportType.Mqtt</span><span class="sxs-lookup"><span data-stu-id="3878a-125">TransportType.Mqtt</span></span> |
| <span data-ttu-id="3878a-126">[Python][lnk-sample-python]</span><span class="sxs-lookup"><span data-stu-id="3878a-126">[Python][lnk-sample-python]</span></span> |<span data-ttu-id="3878a-127">IoTHubTransportProvider.MQTT</span><span class="sxs-lookup"><span data-stu-id="3878a-127">IoTHubTransportProvider.MQTT</span></span> |

### <a name="migrating-a-device-app-from-amqp-toomqtt"></a><span data-ttu-id="3878a-128">AMQP tooMQTT에서 장치 응용 프로그램 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="3878a-128">Migrating a device app from AMQP tooMQTT</span></span>

<span data-ttu-id="3878a-129">Hello를 사용 하는 경우 [장치 Sdk][lnk-device-sdks], AMQP를 사용 하 여 전환 tooMQTT 필요 앞서 설명한 것 처럼 hello 클라이언트 초기화에 hello 프로토콜 매개 변수를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-129">If you are using hello [device SDKs][lnk-device-sdks], switching from using AMQP tooMQTT requires changing hello protocol parameter in hello client initialization as stated previously.</span></span>

<span data-ttu-id="3878a-130">이렇게 할 경우 다음 항목 toocheck hello를 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-130">When doing so, make sure toocheck hello following items:</span></span>

* <span data-ttu-id="3878a-131">AMQP은 MQTT hello 연결을 종료 하는 동안 많은 조건에 대 한 오류를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-131">AMQP returns errors for many conditions, while MQTT terminates hello connection.</span></span> <span data-ttu-id="3878a-132">결과적으로 예외 처리 논리를 일부 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-132">As a result your exception handling logic might require some changes.</span></span>
* <span data-ttu-id="3878a-133">MQTT hello를 지원 하지 않습니다 *거부* 를 받을 때 작업 [클라우드-장치 메시지][lnk-messaging]합니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-133">MQTT does not support hello *reject* operations when receiving [cloud-to-device messages][lnk-messaging].</span></span> <span data-ttu-id="3878a-134">백 엔드 앱 tooreceive hello 장치 앱의 응답을 필요한 경우 사용 하 여 고려 [메서드를 직접][lnk-methods]합니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-134">If your back-end app needs tooreceive a response from hello device app, consider using [direct methods][lnk-methods].</span></span>

## <a name="using-hello-mqtt-protocol-directly"></a><span data-ttu-id="3878a-135">직접 hello MQTT 프로토콜을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="3878a-135">Using hello MQTT protocol directly</span></span>
<span data-ttu-id="3878a-136">장치 hello 장치 Sdk를 사용할 수 없는 경우 toohello 공용 장치 끝점 hello MQTT 프로토콜을 사용 하 여 8883 포트에서 계속 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-136">If a device cannot use hello device SDKs, it can still connect toohello public device endpoints using hello MQTT protocol on port 8883.</span></span> <span data-ttu-id="3878a-137">Hello에 **연결** 패킷 hello 장치는 다음 값에는 hello를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-137">In hello **CONNECT** packet hello device should use hello following values:</span></span>

* <span data-ttu-id="3878a-138">Hello에 대 한 **ClientId** 필드의 경우 hello 사용 **deviceId**합니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-138">For hello **ClientId** field, use hello **deviceId**.</span></span>
* <span data-ttu-id="3878a-139">Hello에 대 한 **Username** 필드의 경우 사용 `{iothubhostname}/{device_id}/api-version=2016-11-14`, 여기서 {iothubhostname} hello IoT 허브의 전체 CName hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-139">For hello **Username** field, use `{iothubhostname}/{device_id}/api-version=2016-11-14`, where {iothubhostname} is hello full CName of hello IoT hub.</span></span>

    <span data-ttu-id="3878a-140">예를 들어 hello IoT 허브의 이름인 **contoso.azure devices.net** hello 장치 이름이 경우 **MyDevice01**, 전체 hello **Username** 필드에 포함 되어야 `contoso.azure-devices.net/MyDevice01/api-version=2016-11-14`.</span><span class="sxs-lookup"><span data-stu-id="3878a-140">For example, if hello name of your IoT hub is **contoso.azure-devices.net** and if hello name of your device is **MyDevice01**, hello full **Username** field should contain `contoso.azure-devices.net/MyDevice01/api-version=2016-11-14`.</span></span>
* <span data-ttu-id="3878a-141">Hello에 대 한 **암호** 필드의 경우 SAS 토큰을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-141">For hello **Password** field, use a SAS token.</span></span> <span data-ttu-id="3878a-142">SAS 토큰은 hello hello 형식의 hello HTTP 및 AMQP 프로토콜을 모두의 경우와 동일 hello:</span><span class="sxs-lookup"><span data-stu-id="3878a-142">hello format of hello SAS token is hello same as for both hello HTTP and AMQP protocols:</span></span><br/><span data-ttu-id="3878a-143">`SharedAccessSignature sig={signature-string}&se={expiry}&sr={URL-encoded-resourceURI}`</span><span class="sxs-lookup"><span data-stu-id="3878a-143">`SharedAccessSignature sig={signature-string}&se={expiry}&sr={URL-encoded-resourceURI}`.</span></span>

    <span data-ttu-id="3878a-144">방법에 대 한 자세한 내용은 toogenerate SAS 토큰의 hello 장치 섹션을 참조 [IoT 허브를 사용 하 여 보안 토큰][lnk-sas-tokens]합니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-144">For more information about how toogenerate SAS tokens, see hello device section of [Using IoT Hub security tokens][lnk-sas-tokens].</span></span>

    <span data-ttu-id="3878a-145">을 테스트할 때 사용할 수도 있습니다 hello [장치 탐색기] [ lnk-device-explorer] 도구 tooquickly 복사 하 고 사용자 고유의 코드에 붙여 넣을 수 있는 SAS 토큰을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-145">When testing, you can also use hello [device explorer][lnk-device-explorer] tool tooquickly generate a SAS token that you can copy and paste into your own code:</span></span>

  1. <span data-ttu-id="3878a-146">Toohello 이동 **관리** 탭에서 **장치 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-146">Go toohello **Management** tab in **Device Explorer**.</span></span>
  2. <span data-ttu-id="3878a-147">**SAS 토큰** (오른쪽 위)을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-147">Click **SAS Token** (top right).</span></span>
  3. <span data-ttu-id="3878a-148">**SASTokenForm**, hello에 장치를 선택 합니다. **DeviceID** 드롭 다운 합니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-148">On **SASTokenForm**, select your device in hello **DeviceID** drop down.</span></span> <span data-ttu-id="3878a-149">**TTL**을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-149">Set your **TTL**.</span></span>
  4. <span data-ttu-id="3878a-150">클릭 **생성** toocreate 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-150">Click **Generate** toocreate your token.</span></span>

     <span data-ttu-id="3878a-151">hello 생성 되는 SAS 토큰에이 구조: `HostName={your hub name}.azure-devices.net;DeviceId=javadevice;SharedAccessSignature=SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`합니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-151">hello SAS token that's generated has this structure: `HostName={your hub name}.azure-devices.net;DeviceId=javadevice;SharedAccessSignature=SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span></span>

     <span data-ttu-id="3878a-152">이 토큰 toouse hello로의 일부 hello **암호** MQTT를 사용 하 여 필드 tooconnect은: `SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`합니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-152">hello part of this token toouse as hello **Password** field tooconnect using MQTT is: `SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span></span>

<span data-ttu-id="3878a-153">MQTT에 대 한 연결 및 분리 패킷, IoT Hub 발급 hello에 대 한 이벤트 **Operations 모니터링** tootroubleshoot 연결 문제 도움이 되는 추가 정보를 사용 하 여 채널입니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-153">For MQTT connect and disconnect packets, IoT Hub issues an event on hello **Operations Monitoring** channel with additional information that can help you tootroubleshoot connectivity issues.</span></span>

### <a name="sending-device-to-cloud-messages"></a><span data-ttu-id="3878a-154">장치-클라우드 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="3878a-154">Sending device-to-cloud messages</span></span>

<span data-ttu-id="3878a-155">성공적으로 연결한 후 장치를 사용 하 여 메시지 tooIoT 허브 보낼 수 `devices/{device_id}/messages/events/` 또는 `devices/{device_id}/messages/events/{property_bag}` 로 **주제 이름**합니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-155">After making a successful connection, a device can send messages tooIoT Hub using `devices/{device_id}/messages/events/` or `devices/{device_id}/messages/events/{property_bag}` as a **Topic Name**.</span></span> <span data-ttu-id="3878a-156">hello `{property_bag}` 요소를 사용 하면 추가 속성을 url로 인코딩된 형식으로 hello 장치 toosend 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-156">hello `{property_bag}` element enables hello device toosend messages with additional properties in a url-encoded format.</span></span> <span data-ttu-id="3878a-157">예:</span><span class="sxs-lookup"><span data-stu-id="3878a-157">For example:</span></span>

```
RFC 2396-encoded(<PropertyName1>)=RFC 2396-encoded(<PropertyValue1>)&RFC 2396-encoded(<PropertyName2>)=RFC 2396-encoded(<PropertyValue2>)…
```

> [!NOTE]
> <span data-ttu-id="3878a-158">이 `{property_bag}` 요소 hello HTTP 프로토콜에 쿼리 문자열의 경우와 같은 인코딩을 사용 하 여 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-158">This `{property_bag}` element uses hello same encoding as for query strings in hello HTTP protocol.</span></span>
>
>

<span data-ttu-id="3878a-159">hello 장치 앱 ´ ï ´ `devices/{device_id}/messages/events/{property_bag}` hello로 **가 항목 이름을** toodefine *가 메시지를* toobe 원격 분석 메시지로 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-159">hello device app can also use `devices/{device_id}/messages/events/{property_bag}` as hello **Will topic name** toodefine *Will messages* toobe forwarded as a telemetry message.</span></span>

- <span data-ttu-id="3878a-160">IoT Hub에서는 QoS 2 메시지를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-160">IoT Hub does not support QoS 2 messages.</span></span> <span data-ttu-id="3878a-161">장치 응용 프로그램으로 메시지를 게시 하는 경우 **QoS 2**, IoT Hub hello 네트워크 연결을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-161">If a device app publishes a message with **QoS 2**, IoT Hub closes hello network connection.</span></span>
- <span data-ttu-id="3878a-162">IoT Hub에서는 보관 메시지가 지속되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-162">IoT Hub does not persist Retain messages.</span></span> <span data-ttu-id="3878a-163">장치 hello로 메시지를 보내는 경우 **RETAIN** 플래그가 설정 too1, IoT Hub 추가 hello **x-opt-유지** 응용 프로그램 속성 toohello 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-163">If a device sends a message with hello **RETAIN** flag set too1, IoT Hub adds hello **x-opt-retain** application property toohello message.</span></span> <span data-ttu-id="3878a-164">이 경우 대신 지속 hello 메시지를 보관, IoT Hub toohello 백 엔드 응용 프로그램 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-164">In this case, instead of persisting hello retain message, IoT Hub passes it toohello backend app.</span></span>
- <span data-ttu-id="3878a-165">IoT Hub는 장치 당 하나의 활성 MQTT 연결만을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-165">IoT Hub only supports one active MQTT connection per device.</span></span> <span data-ttu-id="3878a-166">모든 새 MQTT 연결 hello를 대신 하 여 동일한 장치 ID로 인해 IoT Hub toodrop hello에 대 한 기존 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-166">Any new MQTT connection on behalf of hello same device ID causes IoT Hub toodrop hello existing connection.</span></span>

<span data-ttu-id="3878a-167">자세한 내용은 [메시징 개발자 가이드][lnk-messaging]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3878a-167">For more information, see [Messaging developer's guide][lnk-messaging].</span></span>

### <a name="receiving-cloud-to-device-messages"></a><span data-ttu-id="3878a-168">클라우드-장치 메시지 수신</span><span class="sxs-lookup"><span data-stu-id="3878a-168">Receiving cloud-to-device messages</span></span>

<span data-ttu-id="3878a-169">IoT Hub에서 tooreceive 메시지, 장치가 가입 되어 있어야 사용 하 여 `devices/{device_id}/messages/devicebound/#` 로 **항목 필터**합니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-169">tooreceive messages from IoT Hub, a device should subscribe using `devices/{device_id}/messages/devicebound/#` as a **Topic Filter**.</span></span> <span data-ttu-id="3878a-170">여러 수준의 와일드 카드 hello  **#**  hello에 항목 필터 tooallow hello 장치 tooreceive 추가 속성 hello 항목 이름에만 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-170">hello multi-level wildcard **#** in hello Topic Filter is used only tooallow hello device tooreceive additional properties in hello topic name.</span></span> <span data-ttu-id="3878a-171">IoT Hub hello의 hello 사용 하지 못하도록  **#**  또는 **?**</span><span class="sxs-lookup"><span data-stu-id="3878a-171">IoT Hub does not allow hello usage of hello **#** or **?**</span></span> <span data-ttu-id="3878a-172">하위 토픽의 필터링을 위한 와일드카드</span><span class="sxs-lookup"><span data-stu-id="3878a-172">wildcards for filtering of sub-topics.</span></span> <span data-ttu-id="3878a-173">IoT Hub 범용 게시-구독 메시징 브로커 아니므로 문서화 hello 항목 이름 및 항목 필터를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-173">Since IoT Hub is not a general purpose pub-sub messaging broker, it only supports hello documented topic names and topic filters.</span></span>

<span data-ttu-id="3878a-174">hello 장치는 메시지를 받지 못하게 IoT 허브에서 hello 나타내는 tooits 장치별 끝점에서 성공적으로 구독 될 때까지 `devices/{device_id}/messages/devicebound/#` 항목 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-174">hello device does not receive any messages from IoT Hub, until it has successfully subscribed tooits device-specific endpoint, represented by hello `devices/{device_id}/messages/devicebound/#` topic filter.</span></span> <span data-ttu-id="3878a-175">성공한 구독 설정 된 후 hello 장치 tooit hello 구독의 hello 시간 이후에 보낸만으로 클라우드-장치 메시지를 받기 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-175">After successful subscription has been established, hello device starts receiving only cloud-to-device messages that have been sent tooit after hello time of hello subscription.</span></span> <span data-ttu-id="3878a-176">Hello 장치가 연결 된 **CleanSession** 플래그가 설정 너무**0**, hello 구독 다른 세션 간에 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-176">If hello device connects with **CleanSession** flag set too**0**, hello subscription is persisted across different sessions.</span></span> <span data-ttu-id="3878a-177">이 경우 다음으로 연결할 때 hello **CleanSession 0** hello 장치에서 보낸 tooit 끊어져 동안 해결 되지 않은 메시지를 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-177">In this case, hello next time it connects with **CleanSession 0** hello device receives outstanding messages that have been sent tooit while it was disconnected.</span></span> <span data-ttu-id="3878a-178">Hello 장치를 사용 하는 경우 **CleanSession** 플래그가 설정 너무**1** 하지만 수신 되지 않으면 모든 메시지가 IoT 허브에서 tooits 장치 끝점을 등록 될 때까지 합니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-178">If hello device uses **CleanSession** flag set too**1** though, it does not receive any messages from IoT Hub until it subscribes tooits device-endpoint.</span></span>

<span data-ttu-id="3878a-179">IoT Hub hello로 메시지를 배달 **주제 이름** `devices/{device_id}/messages/devicebound/`, 또는 `devices/{device_id}/messages/devicebound/{property_bag}` 모든 메시지 속성이 있는 경우.</span><span class="sxs-lookup"><span data-stu-id="3878a-179">IoT Hub delivers messages with hello **Topic Name** `devices/{device_id}/messages/devicebound/`, or `devices/{device_id}/messages/devicebound/{property_bag}` if there are any message properties.</span></span> <span data-ttu-id="3878a-180">`{property_bag}` 에는 메시지 속성의 URL 인코딩된 키/값 쌍이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-180">`{property_bag}` contains url-encoded key/value pairs of message properties.</span></span> <span data-ttu-id="3878a-181">응용 프로그램 속성 및 사용자 설정 시스템 속성 (같은 **messageId** 또는 **correlationId**) hello propertybag에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-181">Only application properties and user-settable system properties (such as **messageId** or **correlationId**) are included in hello property bag.</span></span> <span data-ttu-id="3878a-182">시스템 속성 이름은 hello 접두사가  **$** , 응용 프로그램 속성 접두사가 없는 원래 속성 이름 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-182">System property names have hello prefix **$**, application properties use hello original property name with no prefix.</span></span>

<span data-ttu-id="3878a-183">장치 앱 tooa 항목을 구독 하는 경우 **QoS 2**, IoT Hub 부여 hello에 최대 QoS 수준 1 **SUBACK** 패킷 합니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-183">When a device app subscribes tooa topic with **QoS 2**, IoT Hub grants maximum QoS level 1 in hello **SUBACK** packet.</span></span> <span data-ttu-id="3878a-184">그 후 IoT 허브는 QoS 1을 사용 하 여 메시지 toohello 장치를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-184">After that, IoT Hub delivers messages toohello device using QoS 1.</span></span>

### <a name="retrieving-a-device-twins-properties"></a><span data-ttu-id="3878a-185">장치 쌍 속성 검색</span><span class="sxs-lookup"><span data-stu-id="3878a-185">Retrieving a device twin's properties</span></span>

<span data-ttu-id="3878a-186">첫째, 장치가 구독 너무`$iothub/twin/res/#`, tooreceive hello 작업 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-186">First, a device subscribes too`$iothub/twin/res/#`, tooreceive hello operation's responses.</span></span> <span data-ttu-id="3878a-187">그런 다음 빈 메시지 tootopic 보내는 `$iothub/twin/GET/?$rid={request id}`에 지정된 된 값이 있는 **요청 id**. hello 서비스 hello 장치로 이중 데이터 항목에 포함 된 응답 메시지를 보냅니다 `$iothub/twin/res/{status}/?$rid={request id}`, 동일 hello를 사용 하 여  **요청 id** hello 요청으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-187">Then, it sends an empty message tootopic `$iothub/twin/GET/?$rid={request id}`, with a populated value for **request id**. hello service then sends a response message containing hello device twin data on topic `$iothub/twin/res/{status}/?$rid={request id}`, using hello same **request id** as hello request.</span></span>

<span data-ttu-id="3878a-188">request id는 [IoT Hub 메시징 개발자 가이드][lnk-messaging]에 따라 메시지 속성 값에 대한 유효한 값이며 status는 정수로 확인됩니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-188">Request id can be any valid value for a message property value, as per [IoT Hub messaging developer's guide][lnk-messaging], and status is validated as an integer.</span></span>
<span data-ttu-id="3878a-189">hello 응답 본문의 hello 장치로 이중 hello 속성 섹션에 포함:</span><span class="sxs-lookup"><span data-stu-id="3878a-189">hello response body contains hello properties section of hello device twin:</span></span>

<span data-ttu-id="3878a-190">hello 본문 hello identity 레지스트리 항목의 예를 들어 toohello "속성" 멤버를 제한:</span><span class="sxs-lookup"><span data-stu-id="3878a-190">hello body of hello identity registry entry limited toohello “properties” member, for example:</span></span>

        {
            "properties": {
                "desired": {
                    "telemetrySendFrequency": "5m",
                    "$version": 12
                },
                "reported": {
                    "telemetrySendFrequency": "5m",
                    "batteryLevel": 55,
                    "$version": 123
                }
            }
        }

<span data-ttu-id="3878a-191">hello 가능한 상태 코드는.</span><span class="sxs-lookup"><span data-stu-id="3878a-191">hello possible status codes are:</span></span>

|<span data-ttu-id="3878a-192">가동 상태</span><span class="sxs-lookup"><span data-stu-id="3878a-192">Status</span></span> | <span data-ttu-id="3878a-193">설명</span><span class="sxs-lookup"><span data-stu-id="3878a-193">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="3878a-194">200</span><span class="sxs-lookup"><span data-stu-id="3878a-194">200</span></span> | <span data-ttu-id="3878a-195">성공</span><span class="sxs-lookup"><span data-stu-id="3878a-195">Success</span></span> |
| <span data-ttu-id="3878a-196">429</span><span class="sxs-lookup"><span data-stu-id="3878a-196">429</span></span> | <span data-ttu-id="3878a-197">너무 많은 요청(제한됨), [IoT Hub 제한][lnk-quotas] 참조</span><span class="sxs-lookup"><span data-stu-id="3878a-197">Too many requests (throttled), as per [IoT Hub throttling][lnk-quotas]</span></span> |
| <span data-ttu-id="3878a-198">5**</span><span class="sxs-lookup"><span data-stu-id="3878a-198">5**</span></span> | <span data-ttu-id="3878a-199">서버 오류</span><span class="sxs-lookup"><span data-stu-id="3878a-199">Server errors</span></span> |

<span data-ttu-id="3878a-200">자세한 내용은 [장치 쌍 개발자 가이드][lnk-devguide-twin]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3878a-200">For more information, see [Device twins developer's guide][lnk-devguide-twin].</span></span>

### <a name="update-device-twins-reported-properties"></a><span data-ttu-id="3878a-201">장치 쌍의 reported 속성 업데이트</span><span class="sxs-lookup"><span data-stu-id="3878a-201">Update device twin's reported properties</span></span>

<span data-ttu-id="3878a-202">hello 다음 시퀀스에 설명 장치 hello를 업데이트 하는 방식은 hello 장치로 이중 IoT 허브에서의 속성을 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-202">hello following sequence describes how a device updates hello reported properties in hello device twin in IoT Hub:</span></span>

1. <span data-ttu-id="3878a-203">장치 toohello 먼저 구독 해야 `$iothub/twin/res/#` IoT 허브에서 항목 tooreceive hello 작업 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-203">A device must first subscribe toohello `$iothub/twin/res/#` topic tooreceive hello operation's responses from IoT Hub.</span></span>

1. <span data-ttu-id="3878a-204">Hello 장치로 이중 업데이트 toohello 포함 된 메시지를 전송 하는 장치는 `$iothub/twin/PATCH/properties/reported/?$rid={request id}` 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-204">A device sends a message that contains hello device twin update toohello `$iothub/twin/PATCH/properties/reported/?$rid={request id}` topic.</span></span> <span data-ttu-id="3878a-205">이 메시지는 **요청 ID** 값을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-205">This message includes a **request id** value.</span></span>

1. <span data-ttu-id="3878a-206">포함 된 응답 메시지에 대 한 ETag 값을 새 hello 보냅니다 hello 보고 properties 컬렉션 항목에 대 한 다음 서비스 hello `$iothub/twin/res/{status}/?$rid={request id}`합니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-206">hello service then sends a response message that contains hello new ETag value for hello reported properties collection on topic `$iothub/twin/res/{status}/?$rid={request id}`.</span></span> <span data-ttu-id="3878a-207">이 응답 메시지를 사용 하 여 hello 동일 **요청 id** hello 요청으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-207">This response message uses hello same **request id** as hello request.</span></span>

<span data-ttu-id="3878a-208">hello 요청 메시지 본문에는 보고 속성 (기타 속성이 나 메타 데이터를 수정할 수 있음)에 대 한 새 값을 제공 하는 JSON 문서를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-208">hello request message body contains a JSON document, which provides new values for reported properties (no other property or metadata can be modified).</span></span>
<span data-ttu-id="3878a-209">Hello JSON 문서에 있는 각 멤버를 업데이트 하거나 hello 장치로 이중의 문서에 hello 해당 멤버를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-209">Each member in hello JSON document updates or add hello corresponding member in hello device twin’s document.</span></span> <span data-ttu-id="3878a-210">구성원 설정 너무`null`, 삭제 hello 개체를 포함 하는 hello에서 멤버입니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-210">A member set too`null`, deletes hello member from hello containing object.</span></span> <span data-ttu-id="3878a-211">예:</span><span class="sxs-lookup"><span data-stu-id="3878a-211">For example:</span></span>

        {
            "telemetrySendFrequency": "35m",
            "batteryLevel": 60
        }

<span data-ttu-id="3878a-212">hello 가능한 상태 코드는.</span><span class="sxs-lookup"><span data-stu-id="3878a-212">hello possible status codes are:</span></span>

|<span data-ttu-id="3878a-213">가동 상태</span><span class="sxs-lookup"><span data-stu-id="3878a-213">Status</span></span> | <span data-ttu-id="3878a-214">설명</span><span class="sxs-lookup"><span data-stu-id="3878a-214">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="3878a-215">200</span><span class="sxs-lookup"><span data-stu-id="3878a-215">200</span></span> | <span data-ttu-id="3878a-216">성공</span><span class="sxs-lookup"><span data-stu-id="3878a-216">Success</span></span> |
| <span data-ttu-id="3878a-217">400</span><span class="sxs-lookup"><span data-stu-id="3878a-217">400</span></span> | <span data-ttu-id="3878a-218">잘못된 요청.</span><span class="sxs-lookup"><span data-stu-id="3878a-218">Bad Request.</span></span> <span data-ttu-id="3878a-219">형식이 잘못된 JSON</span><span class="sxs-lookup"><span data-stu-id="3878a-219">Malformed JSON</span></span> |
| <span data-ttu-id="3878a-220">429</span><span class="sxs-lookup"><span data-stu-id="3878a-220">429</span></span> | <span data-ttu-id="3878a-221">너무 많은 요청(제한됨), [IoT Hub 제한][lnk-quotas] 참조</span><span class="sxs-lookup"><span data-stu-id="3878a-221">Too many requests (throttled), as per [IoT Hub throttling][lnk-quotas]</span></span> |
| <span data-ttu-id="3878a-222">5**</span><span class="sxs-lookup"><span data-stu-id="3878a-222">5**</span></span> | <span data-ttu-id="3878a-223">서버 오류</span><span class="sxs-lookup"><span data-stu-id="3878a-223">Server errors</span></span> |

<span data-ttu-id="3878a-224">자세한 내용은 [장치 쌍 개발자 가이드][lnk-devguide-twin]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3878a-224">For more information, see [Device twins developer's guide][lnk-devguide-twin].</span></span>

### <a name="receiving-desired-properties-update-notifications"></a><span data-ttu-id="3878a-225">desired 속성 업데이트 알림 수신</span><span class="sxs-lookup"><span data-stu-id="3878a-225">Receiving desired properties update notifications</span></span>

<span data-ttu-id="3878a-226">IoT Hub 장치가 연결 된 알림 toohello 항목 보냅니다 `$iothub/twin/PATCH/properties/desired/?$version={new version}`, hello 솔루션 백 엔드 수행한 hello 업데이트의 hello 콘텐츠를 포함 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-226">When a device is connected, IoT Hub sends notifications toohello topic `$iothub/twin/PATCH/properties/desired/?$version={new version}`, which contain hello content of hello update performed by hello solution back end.</span></span> <span data-ttu-id="3878a-227">예:</span><span class="sxs-lookup"><span data-stu-id="3878a-227">For example:</span></span>

        {
            "telemetrySendFrequency": "5m",
            "route": null
        }

<span data-ttu-id="3878a-228">속성 업데이트와 `null` hello JSON 값은 개체 멤버를 삭제 하는 중입니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-228">As for property updates, `null` values means that hello JSON object member is being deleted.</span></span>


> [!IMPORTANT] 
> <span data-ttu-id="3878a-229">IoT Hub는 장치가 연결된 경우에만 변경 알림을 생성하여</span><span class="sxs-lookup"><span data-stu-id="3878a-229">IoT Hub generates change notifications only when devices are connected.</span></span> <span data-ttu-id="3878a-230">있는지 tooimplement hello 확인 [장치 다시 연결 흐름] [ lnk-devguide-twin-reconnection] tookeep hello 원하는 속성 IoT Hub와 hello 장치 응용 프로그램 간에 동기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-230">Make sure tooimplement hello [device reconnection flow][lnk-devguide-twin-reconnection] tookeep hello desired properties synchronized between IoT Hub and hello device app.</span></span>

<span data-ttu-id="3878a-231">자세한 내용은 [장치 쌍 개발자 가이드][lnk-devguide-twin]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3878a-231">For more information, see [Device twins developer's guide][lnk-devguide-twin].</span></span>

### <a name="respond-tooa-direct-method"></a><span data-ttu-id="3878a-232">응답 tooa 직접적인 방법</span><span class="sxs-lookup"><span data-stu-id="3878a-232">Respond tooa direct method</span></span>

<span data-ttu-id="3878a-233">첫째, 장치가 toosubscribe 너무`$iothub/methods/POST/#`합니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-233">First, a device has toosubscribe too`$iothub/methods/POST/#`.</span></span> <span data-ttu-id="3878a-234">IoT Hub 보냅니다 메서드 요청 toohello 항목 `$iothub/methods/POST/{method name}/?$rid={request id}`, 유효한 JSON 또는 본문이 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-234">IoT Hub sends method requests toohello topic `$iothub/methods/POST/{method name}/?$rid={request id}`, with either a valid JSON or an empty body.</span></span>

<span data-ttu-id="3878a-235">hello 장치 toorespond, 유효한 JSON 또는 빈 본문 toohello 항목으로 메시지를 보내는 `$iothub/methods/res/{status}/?$rid={request id}`여기서 **요청 id** toomatch hello 요청 메시지에서 hello에 및 **상태** toobe 정수에 .</span><span class="sxs-lookup"><span data-stu-id="3878a-235">toorespond, hello device sends a message with a valid JSON or empty body toohello topic `$iothub/methods/res/{status}/?$rid={request id}`, where **request id** has toomatch hello one in hello request message, and **status** has toobe an integer.</span></span>

<span data-ttu-id="3878a-236">자세한 내용은 [직접 메서드 개발자 가이드][lnk-methods]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3878a-236">For more information, see [Direct method developer's guide][lnk-methods].</span></span>

### <a name="additional-considerations"></a><span data-ttu-id="3878a-237">추가 고려 사항</span><span class="sxs-lookup"><span data-stu-id="3878a-237">Additional considerations</span></span>

<span data-ttu-id="3878a-238">최종 고려 사항으로 toocustomize hello MQTT 프로토콜 동작 hello 클라우드 쪽에서는 필요한 경우 검토 해야 hello [Azure IoT 프로토콜 게이트웨이] [ lnk-azure-protocol-gateway] 수 있게 해 주는 toodeploy 성능 우선 IoT Hub와 직접 상호 작용 하는 사용자 지정 프로토콜 게이트웨이.</span><span class="sxs-lookup"><span data-stu-id="3878a-238">As a final consideration, if you need toocustomize hello MQTT protocol behavior on hello cloud side, you should review hello [Azure IoT protocol gateway][lnk-azure-protocol-gateway] that enables you toodeploy a high-performance custom protocol gateway that interfaces directly with IoT Hub.</span></span> <span data-ttu-id="3878a-239">hello Azure IoT 프로토콜 게이트웨이 있습니다 toocustomize hello 장치 프로토콜 tooaccommodate brownfield MQTT 배포 또는 기타 사용자 지정 프로토콜을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-239">hello Azure IoT protocol gateway enables you toocustomize hello device protocol tooaccommodate brownfield MQTT deployments or other custom protocols.</span></span> <span data-ttu-id="3878a-240">그렇지만 이 방법을 사용하는 경우 사용자 지정 프로토콜 게이트웨이를 실행하고 작동해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-240">This approach does require, however, that you run and operate a custom protocol gateway.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3878a-241">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3878a-241">Next steps</span></span>

<span data-ttu-id="3878a-242">hello MQTT 프로토콜에 대해 자세히 toolearn 참조 hello [MQTT 설명서][lnk-mqtt-docs]합니다.</span><span class="sxs-lookup"><span data-stu-id="3878a-242">toolearn more about hello MQTT protocol, see hello [MQTT documentation][lnk-mqtt-docs].</span></span>

<span data-ttu-id="3878a-243">IoT Hub 배포 계획에 대해 자세히 toolearn 참조:</span><span class="sxs-lookup"><span data-stu-id="3878a-243">toolearn more about planning your IoT Hub deployment, see:</span></span>

* <span data-ttu-id="3878a-244">[IoT용 Azure Certified 장치 카탈로그][lnk-devices]</span><span class="sxs-lookup"><span data-stu-id="3878a-244">[Azure Certified for IoT device catalog][lnk-devices]</span></span>
* <span data-ttu-id="3878a-245">[추가 프로토콜 지원][lnk-protocols]</span><span class="sxs-lookup"><span data-stu-id="3878a-245">[Support additional protocols][lnk-protocols]</span></span>
* <span data-ttu-id="3878a-246">[Event Hubs와 비교][lnk-compare]</span><span class="sxs-lookup"><span data-stu-id="3878a-246">[Compare with Event Hubs][lnk-compare]</span></span>
* <span data-ttu-id="3878a-247">[크기 조정, HA 및 DR][lnk-scaling]</span><span class="sxs-lookup"><span data-stu-id="3878a-247">[Scaling, HA, and DR][lnk-scaling]</span></span>

<span data-ttu-id="3878a-248">toofurther는 IoT Hub의 hello 기능을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="3878a-248">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="3878a-249">[IoT Hub 개발자 가이드][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="3878a-249">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="3878a-250">[Azure IoT Edge에서 장치 시뮬레이션][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="3878a-250">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-device-sdks]: https://github.com/Azure/azure-iot-sdks
[lnk-mqtt-org]: http://mqtt.org/
[lnk-mqtt-docs]: http://mqtt.org/documentation
[lnk-sample-node]: https://github.com/Azure/azure-iot-sdk-node/blob/master/device/samples/simple_sample_device.js
[lnk-sample-java]: https://github.com/Azure/azure-iot-sdk-java/tree/master/device/samples/send-receive-sample/src/main/java/samples/com/microsoft/azure/iothub/SendReceive.java
[lnk-sample-c]: https://github.com/Azure/azure-iot-sdk-c/tree/master/iothub_client/samples/iothub_client_sample_mqtt
[lnk-sample-csharp]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/device/samples
[lnk-sample-python]: https://github.com/Azure/azure-iot-sdk-python/tree/master/device/samples
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer
[lnk-sas-tokens]: iot-hub-devguide-security.md#use-sas-tokens-in-a-device-app
[lnk-azure-protocol-gateway]: iot-hub-protocol-gateway.md

[lnk-devices]: https://catalog.azureiotsuite.com/
[lnk-protocols]: iot-hub-protocol-gateway.md
[lnk-compare]: iot-hub-compare-event-hubs.md
[lnk-scaling]: iot-hub-scaling.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md

[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-messaging]: iot-hub-devguide-messaging.md

[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-twin-reconnection]: iot-hub-devguide-device-twins.md#device-reconnection-flow
[lnk-devguide-twin]: iot-hub-devguide-device-twins.md

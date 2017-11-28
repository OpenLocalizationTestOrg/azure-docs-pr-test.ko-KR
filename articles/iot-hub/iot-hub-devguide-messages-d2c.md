---
title: "aaaUnderstand Azure IoT Hub 장치-클라우드 메시징 | Microsoft Docs"
description: "개발자 가이드-어떻게 toouse 장치-클라우드 IoT Hub와 메시징입니다. 원격 분석 및 비 telemtry 모두 데이터를 보내고 라우팅 toodeliver 메시지를 사용 하는 방법에 대 한 정보가 포함 됩니다."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: 07dc8a6be747365c7efbc528ab2762b0d9790758
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="send-device-to-cloud-messages-tooiot-hub"></a><span data-ttu-id="70ab0-104">장치-클라우드 메시지 tooIoT 허브 보내기</span><span class="sxs-lookup"><span data-stu-id="70ab0-104">Send device-to-cloud messages tooIoT Hub</span></span>

<span data-ttu-id="70ab0-105">toosend 시계열 원격 분석 및 경고 프로그램 장치 tooyour 솔루션 백 엔드를 장치 tooyour IoT 허브에서 장치-클라우드 메시지를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="70ab0-105">toosend time-series telemetry and alerts from your devices tooyour solution back end, send device-to-cloud messages from your device tooyour IoT hub.</span></span> <span data-ttu-id="70ab0-106">IoT Hub에서 지원하는 기타 장치-클라우드 옵션에 대한 설명은 [장치-클라우드 통신 지침][lnk-d2c-guidance]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="70ab0-106">For a discussion of other device-to-cloud options supported by IoT Hub, see [Device-to-cloud communications guidance][lnk-d2c-guidance].</span></span>

<span data-ttu-id="70ab0-107">장치 지향 끝점(**/devices/{deviceId}/messages/events**)을 통해 장치-클라우드 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="70ab0-107">You send device-to-cloud messages through a device-facing endpoint (**/devices/{deviceId}/messages/events**).</span></span> <span data-ttu-id="70ab0-108">라우팅 규칙 다음 hello 웹 서비스 끝점에 메시지 tooone IoT 허브에 라우트 합니다.</span><span class="sxs-lookup"><span data-stu-id="70ab0-108">Routing rules then route your messages tooone of hello service-facing endpoints on your IoT hub.</span></span> <span data-ttu-id="70ab0-109">Hello 헤더와 본문 허브 toodetermine를 통해 흐르는 hello 장치-클라우드 메시지의 라우팅 규칙에 사용 하 여 여기서 tooroute 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="70ab0-109">Routing rules use hello headers and body of hello device-to-cloud messages flowing through your hub toodetermine where tooroute them.</span></span> <span data-ttu-id="70ab0-110">기본적으로 메시지는 라우트된 toohello 기본 제공 서비스 연결 끝점 (**이벤트 메시지/**), 즉 호환 [이벤트 허브][lnk-event-hubs]합니다.</span><span class="sxs-lookup"><span data-stu-id="70ab0-110">By default, messages are routed toohello built-in service-facing endpoint (**messages/events**), that is compatible with [Event Hubs][lnk-event-hubs].</span></span> <span data-ttu-id="70ab0-111">따라서 표준을 사용할 수 있습니다 [이벤트 허브 통합 및 Sdk] [ lnk-compatible-endpoint] 솔루션에서 장치-클라우드 메시지 tooreceive 백 엔드 합니다.</span><span class="sxs-lookup"><span data-stu-id="70ab0-111">Therefore, you can use standard [Event Hubs integration and SDKs][lnk-compatible-endpoint] tooreceive device-to-cloud messages in your solution back end.</span></span>

<span data-ttu-id="70ab0-112">IoT Hub는 스트리밍 메시징 패턴을 사용하여 장치-클라우드 메시징을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="70ab0-112">IoT Hub implements device-to-cloud messaging using a streaming messaging pattern.</span></span> <span data-ttu-id="70ab0-113">IoT Hub 장치-클라우드 메시지와 더 비슷하게는 [이벤트 허브] [ lnk-event-hubs] *이벤트* 보다 [서비스 버스] [ lnk-servicebus] *메시지* 많은 양의 여러 판독기가 읽을 수 있는 hello 서비스를 통해 전달 되는 이벤트는 합니다.</span><span class="sxs-lookup"><span data-stu-id="70ab0-113">IoT Hub's device-to-cloud messages are more like [Event Hubs][lnk-event-hubs] *events* than [Service Bus][lnk-servicebus] *messages* in that there is a high volume of events passing through hello service that can be read by multiple readers.</span></span>

<span data-ttu-id="70ab0-114">장치-클라우드 IoT Hub와 메시징 hello 특성 뒤에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70ab0-114">Device-to-cloud messaging with IoT Hub has hello following characteristics:</span></span>

* <span data-ttu-id="70ab0-115">장치-클라우드 메시지는 영 속 IoT 허브의 기본 보존 **이벤트메시지/** tooseven 일 구성에 대 한 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="70ab0-115">Device-to-cloud messages are durable and retained in an IoT hub's default **messages/events** endpoint for up tooseven days.</span></span>
* <span data-ttu-id="70ab0-116">장치-클라우드 메시지 256KB 최대 있어야 하 고 toooptimize 전송 하는 일괄 처리로 그룹화 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70ab0-116">Device-to-cloud messages can be at most 256 KB, and can be grouped in batches toooptimize sends.</span></span> <span data-ttu-id="70ab0-117">배치는 최대 256KB가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70ab0-117">Batches can be at most 256 KB.</span></span>
* <span data-ttu-id="70ab0-118">Hello에 설명 된 대로 [컨트롤 액세스 tooIoT 허브] [ lnk-devguide-security] 섹션에서 IoT Hub-장치 인증 및 액세스 제어를 사용 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="70ab0-118">As explained in hello [Control access tooIoT Hub][lnk-devguide-security] section, IoT Hub enables per-device authentication and access control.</span></span>
* <span data-ttu-id="70ab0-119">IoT Hub too10 사용자 지정 끝점을 toocreate가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70ab0-119">IoT Hub allows you toocreate up too10 custom endpoints.</span></span> <span data-ttu-id="70ab0-120">메시지가는 IoT hub에 구성 된 경로에 따라 toohello 끝점 배달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="70ab0-120">Messages are delivered toohello endpoints based on routes configured on your IoT hub.</span></span> <span data-ttu-id="70ab0-121">자세한 내용은 [라우팅 규칙](#routing-rules)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="70ab0-121">For more information, see [Routing rules](#routing-rules).</span></span>
* <span data-ttu-id="70ab0-122">IoT Hub를 사용하면 수백만 대의 장치를 동시에 연결할 수 있습니다([할당량 및 제한][lnk-quotas] 참조).</span><span class="sxs-lookup"><span data-stu-id="70ab0-122">IoT Hub enables millions of simultaneously connected devices (see [Quotas and throttling][lnk-quotas]).</span></span>
* <span data-ttu-id="70ab0-123">IoT Hub는 임의 분할을 허용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="70ab0-123">IoT Hub does not allow arbitrary partitioning.</span></span> <span data-ttu-id="70ab0-124">장치-클라우드 메시지는 원래 **deviceId**와 관련하여 분할됩니다.</span><span class="sxs-lookup"><span data-stu-id="70ab0-124">Device-to-cloud messages are partitioned based on their originating **deviceId**.</span></span>

<span data-ttu-id="70ab0-125">Hello 차이 hello IoT Hub 및 이벤트 허브 서비스에 대 한 자세한 내용은 참조 [Azure IoT Hub 비교 및 Azure 이벤트 허브][lnk-comparison]합니다.</span><span class="sxs-lookup"><span data-stu-id="70ab0-125">For more information about hello differences between hello IoT Hub and Event Hubs services, see [Comparison of Azure IoT Hub and Azure Event Hubs][lnk-comparison].</span></span>

## <a name="send-non-telemetry-traffic"></a><span data-ttu-id="70ab0-126">비-원격 분석 트래픽 보내기</span><span class="sxs-lookup"><span data-stu-id="70ab0-126">Send non-telemetry traffic</span></span>

<span data-ttu-id="70ab0-127">메시지를 별도 실행 및 hello 솔루션 백 엔드의 처리를 필요로 하는 요청 장치 보내고 종종는 또한 tootelemetry 데이터 요소, 합니다.</span><span class="sxs-lookup"><span data-stu-id="70ab0-127">Often, in addition tootelemetry data points, devices send messages and requests that require separate execution and handling in hello solution back end.</span></span> <span data-ttu-id="70ab0-128">예를 들어 hello에서 특정 동작을 트리거해야 하는 중요 한 알림 백 엔드 합니다.</span><span class="sxs-lookup"><span data-stu-id="70ab0-128">For example, critical alerts that must trigger a specific action in hello back end.</span></span> <span data-ttu-id="70ab0-129">쉽게 작성할 수는 [라우팅 규칙] [ lnk-devguide-custom] toosend 이러한 유형의 메시지 tooan 끝점 전용 hello 메시지에 헤더 또는 hello 메시지 본문의 값에 따라 tootheir 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="70ab0-129">You can easily write a [routing rule][lnk-devguide-custom] toosend these types of messages tooan endpoint dedicated tootheir processing based on either a header on hello message or a value in hello message body.</span></span>

<span data-ttu-id="70ab0-130">Hello 가장 좋은 방법은 tooprocess이 메시지의 종류에 대 한 자세한 내용은 참조 hello [자습서: 어떻게 tooprocess IoT Hub 장치-클라우드 메시지] [ lnk-d2c-tutorial] 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="70ab0-130">For more information about hello best way tooprocess this kind of message, see hello [Tutorial: How tooprocess IoT Hub device-to-cloud messages][lnk-d2c-tutorial] tutorial.</span></span>

## <a name="route-device-to-cloud-messages"></a><span data-ttu-id="70ab0-131">장치-클라우드 메시지 라우팅</span><span class="sxs-lookup"><span data-stu-id="70ab0-131">Route device-to-cloud messages</span></span>

<span data-ttu-id="70ab0-132">라우팅 장치-클라우드 메시지 tooyour 백 엔드 응용 프로그램에 대 한 두 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70ab0-132">You have two options for routing device-to-cloud messages tooyour back-end apps:</span></span>

* <span data-ttu-id="70ab0-133">기본 제공 hello를 사용 하 여 [호환 이벤트 허브 끝점] [ lnk-compatible-endpoint] tooenable 백 엔드 앱 tooread hello 장치-클라우드 메시지 hello 허브에서 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="70ab0-133">Use hello built-in [Event Hub-compatible endpoint][lnk-compatible-endpoint] tooenable back-end apps tooread hello device-to-cloud messages received by hello hub.</span></span> <span data-ttu-id="70ab0-134">toolearn hello 기본 제공 하는 이벤트 허브 호환 끝점에 대 한 참조 [hello 기본 제공 끝점에서 장치-클라우드 메시지를 읽은][lnk-devguide-builtin]합니다.</span><span class="sxs-lookup"><span data-stu-id="70ab0-134">toolearn about hello built-in Event Hub-compatible endpoint, see [Read device-to-cloud messages from hello built-in endpoint][lnk-devguide-builtin].</span></span>
* <span data-ttu-id="70ab0-135">IoT hub에서 라우팅 규칙 toosend 메시지 toocustom 끝점을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="70ab0-135">Use routing rules toosend messages toocustom endpoints in your IoT hub.</span></span> <span data-ttu-id="70ab0-136">사용자 지정 끝점을 이벤트 허브, 서비스 버스 큐 또는 Service Bus 항목을 사용 하 여 백 엔드 앱 tooread 장치-클라우드 메시지를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="70ab0-136">Custom endpoints enable your back-end apps tooread device-to-cloud messages using Event Hubs, Service Bus queues, or Service Bus topics.</span></span> <span data-ttu-id="70ab0-137">라우팅 및 사용자 지정 끝점에 대 한 toolearn 참조 [장치-클라우드 메시지에 대 한 사용자 지정 끝점 및 라우팅 규칙을 사용 하 여][lnk-devguide-custom]합니다.</span><span class="sxs-lookup"><span data-stu-id="70ab0-137">toolearn about routing and custom endpoints, see [Use custom endpoints and routing rules for device-to-cloud messages][lnk-devguide-custom].</span></span>

## <a name="anti-spoofing-properties"></a><span data-ttu-id="70ab0-138">스푸핑 방지 속성</span><span class="sxs-lookup"><span data-stu-id="70ab0-138">Anti-spoofing properties</span></span>

<span data-ttu-id="70ab0-139">IoT Hub는 장치-클라우드 메시지에 스탬프 hello 다음 속성이 있는 모든 메시지를 스푸핑 tooavoid 장치:</span><span class="sxs-lookup"><span data-stu-id="70ab0-139">tooavoid device spoofing in device-to-cloud messages, IoT Hub stamps all messages with hello following properties:</span></span>

* <span data-ttu-id="70ab0-140">**ConnectionDeviceId**</span><span class="sxs-lookup"><span data-stu-id="70ab0-140">**ConnectionDeviceId**</span></span>
* <span data-ttu-id="70ab0-141">**ConnectionDeviceGenerationId**</span><span class="sxs-lookup"><span data-stu-id="70ab0-141">**ConnectionDeviceGenerationId**</span></span>
* <span data-ttu-id="70ab0-142">**ConnectionAuthMethod**</span><span class="sxs-lookup"><span data-stu-id="70ab0-142">**ConnectionAuthMethod**</span></span>

<span data-ttu-id="70ab0-143">hello 처음 두 개의 포함 hello **deviceId** 및 **generationId** 의 장치를 기준으로 발생 하는 hello [장치 id 속성][lnk-device-properties]합니다.</span><span class="sxs-lookup"><span data-stu-id="70ab0-143">hello first two contain hello **deviceId** and **generationId** of hello originating device, as per [Device identity properties][lnk-device-properties].</span></span>

<span data-ttu-id="70ab0-144">hello **ConnectionAuthMethod** 속성 다음과 같은 속성 hello로 JSON으로 직렬화 된 개체를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="70ab0-144">hello **ConnectionAuthMethod** property contains a JSON serialized object, with hello following properties:</span></span>

```json
{
  "scope": "{ hub | device}",
  "type": "{ symkey | sas}",
  "issuer": "iothub"
}
```

## <a name="next-steps"></a><span data-ttu-id="70ab0-145">다음 단계</span><span class="sxs-lookup"><span data-stu-id="70ab0-145">Next steps</span></span>

<span data-ttu-id="70ab0-146">Hello Sdk에 대 한 내용은 toosend 장치-클라우드 메시지를 사용 하 여, 참조 수 [Azure IoT Sdk][lnk-sdks]합니다.</span><span class="sxs-lookup"><span data-stu-id="70ab0-146">For information about hello SDKs you can use toosend device-to-cloud messages, see [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="70ab0-147">hello [시작] [ lnk-get-started] 보여 주는 자습서 시뮬레이션 및 실제 장치에서 toosend 장치-클라우드 메시지 방법을 합니다.</span><span class="sxs-lookup"><span data-stu-id="70ab0-147">hello [Get Started][lnk-get-started] tutorials show you how toosend device-to-cloud messages from both simulated and physical devices.</span></span> <span data-ttu-id="70ab0-148">자세한 정보를 얻기 위해 hello 참조 [경로 사용 하 여 프로세스 IoT Hub 장치-클라우드 메시지] [ lnk-d2c-tutorial] 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="70ab0-148">For more detail, see hello [Process IoT Hub device-to-cloud messages using routes][lnk-d2c-tutorial] tutorial.</span></span>

[lnk-devguide-builtin]: iot-hub-devguide-messages-read-builtin.md
[lnk-devguide-custom]: iot-hub-devguide-messages-read-custom.md
[lnk-comparison]: iot-hub-compare-event-hubs.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md
[lnk-get-started]: iot-hub-get-started.md

[lnk-event-hubs]: http://azure.microsoft.com/documentation/services/event-hubs/
[lnk-servicebus]: http://azure.microsoft.com/documentation/services/service-bus/
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-compatible-endpoint]: iot-hub-devguide-messages-read-builtin.md
[lnk-device-properties]: iot-hub-devguide-identity-registry.md#device-identity-properties
[lnk-devguide-security]: iot-hub-devguide-security.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

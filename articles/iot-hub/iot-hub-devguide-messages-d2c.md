---
title: "Azure IoT Hub 장치-클라우드 메시징 이해 | Microsoft Docs"
description: "개발자 가이드 - IoT Hub를 사용하여 장치-클라우드 메시징을 사용하는 방법입니다. 원격 분석 및 비원격 분석 데이터를 전송하고 라우팅을 사용하여 메시지를 전송하는 방법에 대한 정보가 포함됩니다."
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
ms.openlocfilehash: d856e26084ee79386a2e8e0e527804bda86b477b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="send-device-to-cloud-messages-to-iot-hub"></a><span data-ttu-id="72e81-104">IoT Hub에 장치-클라우드 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="72e81-104">Send device-to-cloud messages to IoT Hub</span></span>

<span data-ttu-id="72e81-105">시계열 원격 분석 및 경고를 장치에서 솔루션 백 엔드로 보내려면 장치-클라우드 메시지를 장치에서 IoT Hub로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="72e81-105">To send time-series telemetry and alerts from your devices to your solution back end, send device-to-cloud messages from your device to your IoT hub.</span></span> <span data-ttu-id="72e81-106">IoT Hub에서 지원하는 기타 장치-클라우드 옵션에 대한 설명은 [장치-클라우드 통신 지침][lnk-d2c-guidance]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="72e81-106">For a discussion of other device-to-cloud options supported by IoT Hub, see [Device-to-cloud communications guidance][lnk-d2c-guidance].</span></span>

<span data-ttu-id="72e81-107">장치 지향 끝점(**/devices/{deviceId}/messages/events**)을 통해 장치-클라우드 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="72e81-107">You send device-to-cloud messages through a device-facing endpoint (**/devices/{deviceId}/messages/events**).</span></span> <span data-ttu-id="72e81-108">그런 다음 라우팅 규칙은 메시지를 IoT Hub의 서비스 지향 끝점 중 하나로 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="72e81-108">Routing rules then route your messages to one of the service-facing endpoints on your IoT hub.</span></span> <span data-ttu-id="72e81-109">라우팅 규칙은 허브를 통과하는 장치-클라우드 메시지의 헤더 및 본문을 사용하여 허브를 라우팅할 위치를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="72e81-109">Routing rules use the headers and body of the device-to-cloud messages flowing through your hub to determine where to route them.</span></span> <span data-ttu-id="72e81-110">기본적으로 메시지는 [Event Hubs][lnk-event-hubs]와 호환되는 기본 제공 서비스 연결 끝점(**messages/events**)으로 라우팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="72e81-110">By default, messages are routed to the built-in service-facing endpoint (**messages/events**), that is compatible with [Event Hubs][lnk-event-hubs].</span></span> <span data-ttu-id="72e81-111">따라서 표준 [Event Hubs 통합 및 SDK][lnk-compatible-endpoint]를 사용하여 솔루션 백 엔드에서 장치-클라우드 메시지를 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72e81-111">Therefore, you can use standard [Event Hubs integration and SDKs][lnk-compatible-endpoint] to receive device-to-cloud messages in your solution back end.</span></span>

<span data-ttu-id="72e81-112">IoT Hub는 스트리밍 메시징 패턴을 사용하여 장치-클라우드 메시징을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="72e81-112">IoT Hub implements device-to-cloud messaging using a streaming messaging pattern.</span></span> <span data-ttu-id="72e81-113">IoT Hub의 장치 - 클라우드 메시지는 여러 독자가 읽을 수 있는 서비스를 통과하는 많은 양의 이벤트가 있다는 점에서 [Service Bus][lnk-servicebus] *메시지*보다는 [Event Hubs][lnk-event-hubs] *이벤트*에 가깝습니다.</span><span class="sxs-lookup"><span data-stu-id="72e81-113">IoT Hub's device-to-cloud messages are more like [Event Hubs][lnk-event-hubs] *events* than [Service Bus][lnk-servicebus] *messages* in that there is a high volume of events passing through the service that can be read by multiple readers.</span></span>

<span data-ttu-id="72e81-114">IoT Hub를 사용한 장치-클라우드 메시징의 특징은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="72e81-114">Device-to-cloud messaging with IoT Hub has the following characteristics:</span></span>

* <span data-ttu-id="72e81-115">장치-클라우드 메시지는 영구적이며 IoT Hub의 기본 **messages/events** 끝점에 최대 7일 동안 보관됩니다.</span><span class="sxs-lookup"><span data-stu-id="72e81-115">Device-to-cloud messages are durable and retained in an IoT hub's default **messages/events** endpoint for up to seven days.</span></span>
* <span data-ttu-id="72e81-116">장치-클라우드 메시지는 최대 256KB까지 가능하며 보내기를 최적화하기 위해 일괄 처리로 그룹화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72e81-116">Device-to-cloud messages can be at most 256 KB, and can be grouped in batches to optimize sends.</span></span> <span data-ttu-id="72e81-117">배치는 최대 256KB가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72e81-117">Batches can be at most 256 KB.</span></span>
* <span data-ttu-id="72e81-118">[IoT Hub에 대한 액세스 제어][lnk-devguide-security] 섹션에서 설명한 것처럼 IoT Hub는 장치 단위 인증 및 액세스 제어를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="72e81-118">As explained in the [Control access to IoT Hub][lnk-devguide-security] section, IoT Hub enables per-device authentication and access control.</span></span>
* <span data-ttu-id="72e81-119">IoT Hub를 사용하면 최대 10개의 사용자 지정 끝점을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72e81-119">IoT Hub allows you to create up to 10 custom endpoints.</span></span> <span data-ttu-id="72e81-120">메시지는 IoT Hub에 구성된 경로에 따라 끝점으로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="72e81-120">Messages are delivered to the endpoints based on routes configured on your IoT hub.</span></span> <span data-ttu-id="72e81-121">자세한 내용은 [라우팅 규칙](#routing-rules)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="72e81-121">For more information, see [Routing rules](#routing-rules).</span></span>
* <span data-ttu-id="72e81-122">IoT Hub를 사용하면 수백만 대의 장치를 동시에 연결할 수 있습니다([할당량 및 제한][lnk-quotas] 참조).</span><span class="sxs-lookup"><span data-stu-id="72e81-122">IoT Hub enables millions of simultaneously connected devices (see [Quotas and throttling][lnk-quotas]).</span></span>
* <span data-ttu-id="72e81-123">IoT Hub는 임의 분할을 허용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="72e81-123">IoT Hub does not allow arbitrary partitioning.</span></span> <span data-ttu-id="72e81-124">장치-클라우드 메시지는 원래 **deviceId**와 관련하여 분할됩니다.</span><span class="sxs-lookup"><span data-stu-id="72e81-124">Device-to-cloud messages are partitioned based on their originating **deviceId**.</span></span>

<span data-ttu-id="72e81-125">IoT Hub와 Event Hubs 서비스의 차이점에 대한 자세한 내용은 [Azure IoT Hub 및 Azure Event Hubs의 비교][lnk-comparison]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="72e81-125">For more information about the differences between the IoT Hub and Event Hubs services, see [Comparison of Azure IoT Hub and Azure Event Hubs][lnk-comparison].</span></span>

## <a name="send-non-telemetry-traffic"></a><span data-ttu-id="72e81-126">비-원격 분석 트래픽 보내기</span><span class="sxs-lookup"><span data-stu-id="72e81-126">Send non-telemetry traffic</span></span>

<span data-ttu-id="72e81-127">때때로 원격 분석 데이터 요소 외에도 장치는 솔루션 백 엔드에서 별도로 실행하고 처리해야 하는 메시지와 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="72e81-127">Often, in addition to telemetry data points, devices send messages and requests that require separate execution and handling in the solution back end.</span></span> <span data-ttu-id="72e81-128">예를 들어 백 엔드에서 특정 작업을 트리거해야 하는 중요한 경고가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72e81-128">For example, critical alerts that must trigger a specific action in the back end.</span></span> <span data-ttu-id="72e81-129">이러한 형식의 메시지를 메시지 헤더 또는 메시지 본문의 값을 기반으로 처리 전용 끝점에 보내는 [라우팅 규칙][lnk-devguide-custom]을 쉽게 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72e81-129">You can easily write a [routing rule][lnk-devguide-custom] to send these types of messages to an endpoint dedicated to their processing based on either a header on the message or a value in the message body.</span></span>

<span data-ttu-id="72e81-130">이런 종류의 메시지를 처리하는 최선의 방법에 대한 정보는 [자습서: IoT Hub 장치-클라우드 메시지를 처리하는 방법][lnk-d2c-tutorial] 자습서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="72e81-130">For more information about the best way to process this kind of message, see the [Tutorial: How to process IoT Hub device-to-cloud messages][lnk-d2c-tutorial] tutorial.</span></span>

## <a name="route-device-to-cloud-messages"></a><span data-ttu-id="72e81-131">장치-클라우드 메시지 라우팅</span><span class="sxs-lookup"><span data-stu-id="72e81-131">Route device-to-cloud messages</span></span>

<span data-ttu-id="72e81-132">백 엔드 앱에 장치-클라우드 메시지를 라우팅하는 두 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72e81-132">You have two options for routing device-to-cloud messages to your back-end apps:</span></span>

* <span data-ttu-id="72e81-133">허브에서 수신한 장치-클라우드 메시지를 백 엔드 앱에서 읽을 수 있도록 기본 제공 [Event Hub 호환 끝점][lnk-compatible-endpoint]을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="72e81-133">Use the built-in [Event Hub-compatible endpoint][lnk-compatible-endpoint] to enable back-end apps to read the device-to-cloud messages received by the hub.</span></span> <span data-ttu-id="72e81-134">기본 제공 Event Hub 호환 끝점에 대해 알아보려면 [기본 제공 끝점에서 장치-클라우드 메시지 읽기][lnk-devguide-builtin]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="72e81-134">To learn about the built-in Event Hub-compatible endpoint, see [Read device-to-cloud messages from the built-in endpoint][lnk-devguide-builtin].</span></span>
* <span data-ttu-id="72e81-135">라우팅 규칙을 사용하여 IoT Hub의 사용자 지정 끝점에 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="72e81-135">Use routing rules to send messages to custom endpoints in your IoT hub.</span></span> <span data-ttu-id="72e81-136">사용자 지정 끝점을 사용하면 백 엔드 앱에서 Event Hubs, Service Bus 큐 또는 Service Bus 토픽을 사용하여 장치-클라우드 메시지를 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72e81-136">Custom endpoints enable your back-end apps to read device-to-cloud messages using Event Hubs, Service Bus queues, or Service Bus topics.</span></span> <span data-ttu-id="72e81-137">라우팅 및 사용자 지정 끝점에 대해 알아보려면 [장치-클라우드 메시지에 대한 사용자 지정 끝점 및 라우팅 규칙 사용][lnk-devguide-custom]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="72e81-137">To learn about routing and custom endpoints, see [Use custom endpoints and routing rules for device-to-cloud messages][lnk-devguide-custom].</span></span>

## <a name="anti-spoofing-properties"></a><span data-ttu-id="72e81-138">스푸핑 방지 속성</span><span class="sxs-lookup"><span data-stu-id="72e81-138">Anti-spoofing properties</span></span>

<span data-ttu-id="72e81-139">장치-클라우드 메시지에서 스푸핑된 장치를 피하려면 IoT Hub는 다음 속성을 사용하여 모든 메시지를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="72e81-139">To avoid device spoofing in device-to-cloud messages, IoT Hub stamps all messages with the following properties:</span></span>

* <span data-ttu-id="72e81-140">**ConnectionDeviceId**</span><span class="sxs-lookup"><span data-stu-id="72e81-140">**ConnectionDeviceId**</span></span>
* <span data-ttu-id="72e81-141">**ConnectionDeviceGenerationId**</span><span class="sxs-lookup"><span data-stu-id="72e81-141">**ConnectionDeviceGenerationId**</span></span>
* <span data-ttu-id="72e81-142">**ConnectionAuthMethod**</span><span class="sxs-lookup"><span data-stu-id="72e81-142">**ConnectionAuthMethod**</span></span>

<span data-ttu-id="72e81-143">처음 두 가지는 [장치 ID 속성][lnk-device-properties]에 따라 원래 장치의 **deviceId** 및 **generationId**를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="72e81-143">The first two contain the **deviceId** and **generationId** of the originating device, as per [Device identity properties][lnk-device-properties].</span></span>

<span data-ttu-id="72e81-144">**ConnectionAuthMethod** 속성은 다음 속성을 가진 JSON으로 직렬화된 개체를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="72e81-144">The **ConnectionAuthMethod** property contains a JSON serialized object, with the following properties:</span></span>

```json
{
  "scope": "{ hub | device}",
  "type": "{ symkey | sas}",
  "issuer": "iothub"
}
```

## <a name="next-steps"></a><span data-ttu-id="72e81-145">다음 단계</span><span class="sxs-lookup"><span data-stu-id="72e81-145">Next steps</span></span>

<span data-ttu-id="72e81-146">장치-클라우드 메시지를 보내는 데 사용할 수 있는 SDK에 대한 자세한 내용은 [Azure IoT SDK][lnk-sdks]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="72e81-146">For information about the SDKs you can use to send device-to-cloud messages, see [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="72e81-147">[시작하기][lnk-get-started] 자습서에서는 시뮬레이트된 장치와 물리적 장치 둘 다에서 장치-클라우드 메시지를 보내는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="72e81-147">The [Get Started][lnk-get-started] tutorials show you how to send device-to-cloud messages from both simulated and physical devices.</span></span> <span data-ttu-id="72e81-148">자세한 내용은 [경로를 사용하여 IoT Hub 장치-클라우드 메시지 처리][lnk-d2c-tutorial] 자습서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="72e81-148">For more detail, see the [Process IoT Hub device-to-cloud messages using routes][lnk-d2c-tutorial] tutorial.</span></span>

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

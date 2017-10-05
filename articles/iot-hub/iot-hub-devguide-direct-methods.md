---
title: "Azure IoT Hub 직접 메서드 이해 | Microsoft Docs"
description: "개발자 가이드 - 직접 메서드를 사용하여 서비스 앱의 장치에서 코드 호출"
services: iot-hub
documentationcenter: .net
author: nberdy
manager: timlt
editor: 
ms.assetid: 9f0535f1-02e6-467a-9fc4-c0950702102d
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nberdy
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 77e788a32097edbcb1cd4faaa45f35812eabd94a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="understand-and-invoke-direct-methods-from-iot-hub"></a><span data-ttu-id="a3ef8-103">IoT Hub의 직접 메서드 호출 및 이해</span><span class="sxs-lookup"><span data-stu-id="a3ef8-103">Understand and invoke direct methods from IoT Hub</span></span>
## <a name="overview"></a><span data-ttu-id="a3ef8-104">개요</span><span class="sxs-lookup"><span data-stu-id="a3ef8-104">Overview</span></span>
<span data-ttu-id="a3ef8-105">IoT Hub를 사용하면 클라우드의 장치에서 직접 메서드를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3ef8-105">IoT Hub gives you ability to invoke direct methods on devices from the cloud.</span></span> <span data-ttu-id="a3ef8-106">직접 메서드는 사용자가 지정한 시간 제한을 초과하는 즉시 성공하거나 실패한다는 점에서 HTTP 호출과 비슷한 디바이스와의 요청-응답 상호 작용을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a3ef8-106">Direct methods represent a request-reply interaction with a device similar to an HTTP call in that they succeed or fail immediately (after a user-specified timeout).</span></span> <span data-ttu-id="a3ef8-107">즉각적인 작업 과정이 장치의 응답 가능성 여부에 따라 달라지는 시나리오에 유용합니다. 예를 들어 장치가 오프라인일 때 장치에 SMS 깨우기(wake-up)를 보내는 경우가 여기에 해당됩니다.(SMS가 메서드 호출보다 비용이 높아지고 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="a3ef8-107">This is useful for scenarios where the course of immediate action is different depending on whether the device was able to respond, such as sending an SMS wake-up to a device if a device is offline (SMS being more expensive than a method call).</span></span>

<span data-ttu-id="a3ef8-108">각 장치 메서드는 단일 장치를 대상으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ef8-108">Each device method targets a single device.</span></span> <span data-ttu-id="a3ef8-109">[jobs][lnk-devguide-jobs]는 여러 장치에서 직접 메서드를 호출하고 연결되지 않은 장치에 대한 메서드 호출을 예약하는 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ef8-109">[Jobs][lnk-devguide-jobs] provide a way to invoke direct methods on multiple devices, and schedule method invocation for disconnected devices.</span></span>

<span data-ttu-id="a3ef8-110">IoT Hub에 **서비스 연결** 권한만 있다면 누구든 장치에서 메서드를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3ef8-110">Anyone with **service connect** permissions on IoT Hub may invoke a method on a device.</span></span>

### <a name="when-to-use"></a><span data-ttu-id="a3ef8-111">사용하는 경우</span><span class="sxs-lookup"><span data-stu-id="a3ef8-111">When to use</span></span>
<span data-ttu-id="a3ef8-112">직접 메서드는 요청-응답 패턴을 따르며, 결과를 즉각적으로 확인해야 하는 통신, 대개는 팬을 작동하는 것과 같이 장치의 대화식 제어가 필요한 통신입니다.</span><span class="sxs-lookup"><span data-stu-id="a3ef8-112">Direct methods follow a request-response pattern and are meant for communications that require immediate confirmation of their result, usually interactive control of the device, for example to turn on a fan.</span></span>

<span data-ttu-id="a3ef8-113">desired 속성, 직접 메서드 또는 클라우드-장치 메시지 사용에 대해 궁금한 점이 있으면 [클라우드-장치 통신 지침][lnk-c2d-guidance]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a3ef8-113">Refer to [Cloud-to-device communication guidance][lnk-c2d-guidance] if in doubt between using desired properties, direct methods, or cloud-to-device messages.</span></span>

## <a name="method-lifecycle"></a><span data-ttu-id="a3ef8-114">메서드 수명 주기</span><span class="sxs-lookup"><span data-stu-id="a3ef8-114">Method lifecycle</span></span>
<span data-ttu-id="a3ef8-115">직접 메서드는 장치에서 구현되며, 제대로 인스턴스화하기 위해 메서드 페이로드에 0개 이상의 입력이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3ef8-115">Direct methods are implemented on the device and may require zero or more inputs in the method payload to correctly instantiate.</span></span> <span data-ttu-id="a3ef8-116">직접 메서드는 서비스 지향 URI를 통해 호출합니다(`{iot hub}/twins/{device id}/methods/`).</span><span class="sxs-lookup"><span data-stu-id="a3ef8-116">You invoke a direct method through a service-facing URI (`{iot hub}/twins/{device id}/methods/`).</span></span> <span data-ttu-id="a3ef8-117">장치는 장치별 MQTT 토픽을 통해 직접 메서드를 수신합니다(`$iothub/methods/POST/{method name}/`).</span><span class="sxs-lookup"><span data-stu-id="a3ef8-117">A device receives direct methods through a device-specific MQTT topic (`$iothub/methods/POST/{method name}/`).</span></span> <span data-ttu-id="a3ef8-118">향후 추가적인 장치 쪽 네트워킹 프로토콜에서 직접 메서드를 지원할 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="a3ef8-118">We may support direct methods on additional device-side networking protocols in the future.</span></span>

> [!NOTE]
> <span data-ttu-id="a3ef8-119">장치에서 직접 메서드를 호출할 때 속성 이름과 값은 US-ASCII로 출력 가능한 영숫자만 포함할 수 있으며 다음 집합은 제외됩니다. ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``</span><span class="sxs-lookup"><span data-stu-id="a3ef8-119">When you invoke a direct method on a device, property names and values can only contain US-ASCII printable alphanumeric, except any in the following set: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span></span>
> 
> 

<span data-ttu-id="a3ef8-120">직접 메서드는 동기식이며 제한 시간(기본값: 30초, 최대 3600초 설정 가능)이 지나면 성공하거나 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ef8-120">Direct methods are synchronous and either succeed or fail after the timeout period (default: 30 seconds, settable up to 3600 seconds).</span></span> <span data-ttu-id="a3ef8-121">직접 메서드는 장치가 온라인 상태에서 명령을 수신하는 경우에만 작동하기(예: 휴대폰에서 조명 켜기)를 바라는 대화형 시나리오에서 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ef8-121">Direct methods are useful in interactive scenarios where you want a device to act if and only if the device is online and receiving commands, such as turning on a light from a phone.</span></span> <span data-ttu-id="a3ef8-122">이러한 시나리오에서는 클라우드 서비스가 결과에 최대한 빨리 대응할 수 있도록 즉각적인 성공이나 실패를 보려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ef8-122">In these scenarios, you want to see an immediate success or failure so the cloud service can act on the result as soon as possible.</span></span> <span data-ttu-id="a3ef8-123">장치는 메서드의 결과로 메시지 본문을 반환할 수 있지만 메서드가 반드시 그렇게 해야 하는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="a3ef8-123">The device may return some message body as a result of the method, but it isn't required for the method to do so.</span></span> <span data-ttu-id="a3ef8-124">메서드 호출의 순서 지정 또는 동시성 의미 체계에 대한 보장은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a3ef8-124">There is no guarantee on ordering or any concurrency semantics on method calls.</span></span>

<span data-ttu-id="a3ef8-125">직접 메서드는 클라우드 쪽에서는 HTTP 전용, 장치 쪽에서는 MQTT 전용입니다.</span><span class="sxs-lookup"><span data-stu-id="a3ef8-125">Direct method are HTTP-only from the cloud side, and MQTT-only from the device side.</span></span>

<span data-ttu-id="a3ef8-126">메서드 요청 및 응답에 대한 페이로드는 최대 8KB의 JSON 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="a3ef8-126">The payload for method requests and responses is a JSON document up to 8KB.</span></span>

## <a name="reference-topics"></a><span data-ttu-id="a3ef8-127">참조 항목:</span><span class="sxs-lookup"><span data-stu-id="a3ef8-127">Reference topics:</span></span>
<span data-ttu-id="a3ef8-128">다음 참조 항목에서는 직접 메서드 사용에 대한 자세한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ef8-128">The following reference topics provide you with more information about using direct methods.</span></span>

## <a name="invoke-a-direct-method-from-a-back-end-app"></a><span data-ttu-id="a3ef8-129">백 엔드 앱에서 직접 메서드 호출</span><span class="sxs-lookup"><span data-stu-id="a3ef8-129">Invoke a direct method from a back-end app</span></span>
### <a name="method-invocation"></a><span data-ttu-id="a3ef8-130">메서드 호출</span><span class="sxs-lookup"><span data-stu-id="a3ef8-130">Method invocation</span></span>
<span data-ttu-id="a3ef8-131">장치의 직접 메서드 호출은 다음을 포함하는 HTTP 호출입니다.</span><span class="sxs-lookup"><span data-stu-id="a3ef8-131">Direct method invocations on a device are HTTP calls which comprise:</span></span>

* <span data-ttu-id="a3ef8-132">장치별 *URI*(`{iot hub}/twins/{device id}/methods/`)</span><span class="sxs-lookup"><span data-stu-id="a3ef8-132">The *URI* specific to the device (`{iot hub}/twins/{device id}/methods/`)</span></span>
* <span data-ttu-id="a3ef8-133">POST *메서드*</span><span class="sxs-lookup"><span data-stu-id="a3ef8-133">The POST *method*</span></span>
* <span data-ttu-id="a3ef8-134">*헤더* - 권한 부여, 요청 ID, 콘텐츠 형식, 콘텐츠 인코딩을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ef8-134">*Headers* which contain the authorization, request ID, content type, and content encoding</span></span>
* <span data-ttu-id="a3ef8-135">다음과 같은 형식의 투명한 JSON *본문*:</span><span class="sxs-lookup"><span data-stu-id="a3ef8-135">A transparent JSON *body* in the following format:</span></span>

```
{
    "methodName": "reboot",
    "responseTimeoutInSeconds": 200,
    "payload": {
        "input1": "someInput",
        "input2": "anotherInput"
    }
}
```

<span data-ttu-id="a3ef8-136">시간 제한은 초 단위입니다.</span><span class="sxs-lookup"><span data-stu-id="a3ef8-136">Timeout is in seconds.</span></span> <span data-ttu-id="a3ef8-137">시간 제한이 설정되지 않으면 기본값이 30초로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3ef8-137">If timeout is not set, it defaults to 30 seconds.</span></span>

### <a name="response"></a><span data-ttu-id="a3ef8-138">응답</span><span class="sxs-lookup"><span data-stu-id="a3ef8-138">Response</span></span>
<span data-ttu-id="a3ef8-139">백 엔드 앱은 다음을 포함하는 응답을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ef8-139">The back-end app receives a response which comprises:</span></span>

* <span data-ttu-id="a3ef8-140">*HTTP 상태 코드* - 현재 연결되지 않은 장치에 대한 404 오류를 비롯한 IoT Hub에서 오는 오류에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3ef8-140">*HTTP status code*, which is used for errors coming from the IoT Hub, including a 404 error for devices not currently connected</span></span>
* <span data-ttu-id="a3ef8-141">*헤더* - ETag, 요청 ID, 콘텐츠 형식, 콘텐츠 인코딩을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ef8-141">*Headers* which contain the ETag, request ID, content type, and content encoding</span></span>
* <span data-ttu-id="a3ef8-142">다음과 같은 형식의 JSON *본문*:</span><span class="sxs-lookup"><span data-stu-id="a3ef8-142">A JSON *body* in the following format:</span></span>

```
{
    "status" : 201,
    "payload" : {...}
}
```

   <span data-ttu-id="a3ef8-143">`status`와 `body`는 모두 장치에 의해 제공되며 장치 자체의 상태 코드 및/또는 설명으로 응답하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3ef8-143">Both `status` and `body` are provided by the device and used to respond with the device's own status code and/or description.</span></span>

## <a name="handle-a-direct-method-on-a-device"></a><span data-ttu-id="a3ef8-144">장치에서 직접 메서드 처리</span><span class="sxs-lookup"><span data-stu-id="a3ef8-144">Handle a direct method on a device</span></span>
### <a name="method-invocation"></a><span data-ttu-id="a3ef8-145">메서드 호출</span><span class="sxs-lookup"><span data-stu-id="a3ef8-145">Method invocation</span></span>
<span data-ttu-id="a3ef8-146">장치는 MQTT 토픽으로 직접 메서드 요청을 수신합니다. `$iothub/methods/POST/{method name}/?$rid={request id}`</span><span class="sxs-lookup"><span data-stu-id="a3ef8-146">Devices receive direct method requests on the MQTT topic: `$iothub/methods/POST/{method name}/?$rid={request id}`</span></span>

<span data-ttu-id="a3ef8-147">장치가 수신하는 본문은 다음과 같은 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="a3ef8-147">The body which the device receives is in the following format:</span></span>

```
{
    "input1": "someInput",
    "input2": "anotherInput"
}
```

<span data-ttu-id="a3ef8-148">메서드 요청은 QoS 0입니다.</span><span class="sxs-lookup"><span data-stu-id="a3ef8-148">Method requests are QoS 0.</span></span>

### <a name="response"></a><span data-ttu-id="a3ef8-149">응답</span><span class="sxs-lookup"><span data-stu-id="a3ef8-149">Response</span></span>
<span data-ttu-id="a3ef8-150">장치는 `$iothub/methods/res/{status}/?$rid={request id}`에 응답을 보내는데 여기서:</span><span class="sxs-lookup"><span data-stu-id="a3ef8-150">The device sends responses to `$iothub/methods/res/{status}/?$rid={request id}`, where:</span></span>

* <span data-ttu-id="a3ef8-151">`status` 속성은 장치가 제공하는 메서드 실행 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="a3ef8-151">The `status` property is the device-supplied status of method execution.</span></span>
* <span data-ttu-id="a3ef8-152">`$rid` 속성은 IoT Hub로부터 수신한 메서드 호출의 요청 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="a3ef8-152">The `$rid` property is the request ID from the method invocation received from IoT Hub.</span></span>

<span data-ttu-id="a3ef8-153">본문은 장치에 의해 설정되며 모든 상태가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3ef8-153">The body is set by the device and can be any status.</span></span>

## <a name="additional-reference-material"></a><span data-ttu-id="a3ef8-154">추가 참조 자료</span><span class="sxs-lookup"><span data-stu-id="a3ef8-154">Additional reference material</span></span>
<span data-ttu-id="a3ef8-155">이 IoT Hub 개발자 가이드의 다른 참조 자료:</span><span class="sxs-lookup"><span data-stu-id="a3ef8-155">Other reference topics in the IoT Hub developer guide include:</span></span>

* <span data-ttu-id="a3ef8-156">[IoT Hub 끝점][lnk-endpoints] - 각 IoT Hub에서 런타임 및 관리 작업에 대해 공개하는 다양한 끝점에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ef8-156">[IoT Hub endpoints][lnk-endpoints] describes the various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="a3ef8-157">[제한 및 할당량][lnk-quotas] - IoT Hub 서비스에 적용되는 할당량과 서비스를 사용할 때 예상되는 제한 동작에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ef8-157">[Throttling and quotas][lnk-quotas] describes the quotas that apply to the IoT Hub service and the throttling behavior to expect when you use the service.</span></span>
* <span data-ttu-id="a3ef8-158">[Azure IoT 장치 및 서비스 SDK][lnk-sdks] - IoT Hub와 상호 작용하는 장치 및 서비스 앱 모두를 개발할 때 사용할 수 있는 다양한 언어 SDK를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ef8-158">[Azure IoT device and service SDKs][lnk-sdks] lists the various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="a3ef8-159">[장치 쌍, 작업 및 메시지 라우팅을 위한 IoT Hub 쿼리 언어][lnk-query]에서는 IoT Hub에서 장치 쌍 및 작업에 대한 정보를 검색하는 데 사용할 수 있는 IoT Hub 쿼리 언어에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ef8-159">[IoT Hub query language for device twins, jobs, and message routing][lnk-query] describes the IoT Hub query language you can use to retrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="a3ef8-160">[IoT Hub MQTT 지원][lnk-devguide-mqtt] - MQTT 프로토콜에 대한 IoT Hub 지원에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ef8-160">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for the MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a3ef8-161">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a3ef8-161">Next steps</span></span>
<span data-ttu-id="a3ef8-162">직접 메서드를 사용하는 방법에 대해 알아봤으니 다음 IoT Hub 개발자 가이드 항목을 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="a3ef8-162">Now you have learned how to use direct methods, you may be interested in the following IoT Hub developer guide topic:</span></span>

* <span data-ttu-id="a3ef8-163">[여러 장치에서 jobs 예약][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="a3ef8-163">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="a3ef8-164">이 문서에서 설명한 일부 개념을 시도해 보려면 다음과 같은 IoT Hub 자습서를 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="a3ef8-164">If you would like to try out some of the concepts described in this article, you may be interested in the following IoT Hub tutorial:</span></span>

* <span data-ttu-id="a3ef8-165">[직접 메서드 사용][lnk-methods-tutorial]</span><span class="sxs-lookup"><span data-stu-id="a3ef8-165">[Use direct methods][lnk-methods-tutorial]</span></span>

<!-- links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-devguide-messages]: iot-hub-devguide-messaging.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md

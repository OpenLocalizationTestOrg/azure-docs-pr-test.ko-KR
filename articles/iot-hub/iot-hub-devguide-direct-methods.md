---
title: "Azure IoT Hub aaaUnderstand 메서드를 직접 | Microsoft Docs"
description: "개발자 가이드-서비스 응용 프로그램에서 사용자 장치에서 사용 가능한 메서드를 직접 tooinvoke 코드입니다."
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
ms.openlocfilehash: 0d15d44a0c3e1d1cda1669c1ed011c2f932e3d92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-invoke-direct-methods-from-iot-hub"></a><span data-ttu-id="3b28d-103">IoT Hub의 직접 메서드 호출 및 이해</span><span class="sxs-lookup"><span data-stu-id="3b28d-103">Understand and invoke direct methods from IoT Hub</span></span>
## <a name="overview"></a><span data-ttu-id="3b28d-104">개요</span><span class="sxs-lookup"><span data-stu-id="3b28d-104">Overview</span></span>
<span data-ttu-id="3b28d-105">IoT Hub hello 클라우드에서 장치에서 기능 tooinvoke 직접 메서드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3b28d-105">IoT Hub gives you ability tooinvoke direct methods on devices from hello cloud.</span></span> <span data-ttu-id="3b28d-106">직접 메서드 HTTP 호출 한다는 점에서 성공 하거나 실패 (직후 사용자가 지정한 시간 제한)은 장치 비슷한 tooan와 요청-회신 상호 작용을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="3b28d-106">Direct methods represent a request-reply interaction with a device similar tooan HTTP call in that they succeed or fail immediately (after a user-specified timeout).</span></span> <span data-ttu-id="3b28d-107">즉각적인 동작이 hello 과정은 hello 장치는 장치가 오프 라인 (SMS 되 고 메서드 호출에 비해) 이면 SMS 절전 tooa 장치를 보내는 것과 같은 수 toorespond 했는지 여부에 따라 서로 다른 시나리오에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b28d-107">This is useful for scenarios where hello course of immediate action is different depending on whether hello device was able toorespond, such as sending an SMS wake-up tooa device if a device is offline (SMS being more expensive than a method call).</span></span>

<span data-ttu-id="3b28d-108">각 장치 메서드는 단일 장치를 대상으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b28d-108">Each device method targets a single device.</span></span> <span data-ttu-id="3b28d-109">[작업] [ lnk-devguide-jobs] 여러 장치에서 방식으로 tooinvoke 직접 메서드를 제공 하 고 연결 되지 않은 장치에 대 한 메서드 호출을 예약 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b28d-109">[Jobs][lnk-devguide-jobs] provide a way tooinvoke direct methods on multiple devices, and schedule method invocation for disconnected devices.</span></span>

<span data-ttu-id="3b28d-110">IoT Hub에 **서비스 연결** 권한만 있다면 누구든 장치에서 메서드를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b28d-110">Anyone with **service connect** permissions on IoT Hub may invoke a method on a device.</span></span>

### <a name="when-toouse"></a><span data-ttu-id="3b28d-111">때 toouse</span><span class="sxs-lookup"><span data-stu-id="3b28d-111">When toouse</span></span>
<span data-ttu-id="3b28d-112">직접 메서드는 요청-응답 패턴을 따릅니다 하며 해당 결과 팬에 tooturn 예를 들어 hello 장치의 일반적으로 대화형 제어의 즉시 확인 해야 하는 통신을 위해 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b28d-112">Direct methods follow a request-response pattern and are meant for communications that require immediate confirmation of their result, usually interactive control of hello device, for example tooturn on a fan.</span></span>

<span data-ttu-id="3b28d-113">너무 참조[클라우드-장치 통신 지침] [ lnk-c2d-guidance] 원하는 속성을 사용 하 여 간의 의문이 있는 경우 메서드나 클라우드-장치 메시지를 직접 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b28d-113">Refer too[Cloud-to-device communication guidance][lnk-c2d-guidance] if in doubt between using desired properties, direct methods, or cloud-to-device messages.</span></span>

## <a name="method-lifecycle"></a><span data-ttu-id="3b28d-114">메서드 수명 주기</span><span class="sxs-lookup"><span data-stu-id="3b28d-114">Method lifecycle</span></span>
<span data-ttu-id="3b28d-115">직접 메서드 hello 장치에서 구현 되 고 0이 필요할 수 있습니다 또는 hello 메서드 페이로드 toocorrectly에 많은 입력 인스턴스화합니다.</span><span class="sxs-lookup"><span data-stu-id="3b28d-115">Direct methods are implemented on hello device and may require zero or more inputs in hello method payload toocorrectly instantiate.</span></span> <span data-ttu-id="3b28d-116">직접 메서드는 서비스 지향 URI를 통해 호출합니다(`{iot hub}/twins/{device id}/methods/`).</span><span class="sxs-lookup"><span data-stu-id="3b28d-116">You invoke a direct method through a service-facing URI (`{iot hub}/twins/{device id}/methods/`).</span></span> <span data-ttu-id="3b28d-117">장치는 장치별 MQTT 토픽을 통해 직접 메서드를 수신합니다(`$iothub/methods/POST/{method name}/`).</span><span class="sxs-lookup"><span data-stu-id="3b28d-117">A device receives direct methods through a device-specific MQTT topic (`$iothub/methods/POST/{method name}/`).</span></span> <span data-ttu-id="3b28d-118">Hello 앞에 추가 장치 측 네트워킹 프로토콜에 직접 메서드 지원 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b28d-118">We may support direct methods on additional device-side networking protocols in hello future.</span></span>

> [!NOTE]
> <span data-ttu-id="3b28d-119">장치에서 직접 메서드를 호출 하는 경우 속성 이름 및 값만 포함 될 수 있습니다 US-ASCII 인쇄 가능한 hello 관계 집합에서 제외 하 고 영숫자: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``합니다.</span><span class="sxs-lookup"><span data-stu-id="3b28d-119">When you invoke a direct method on a device, property names and values can only contain US-ASCII printable alphanumeric, except any in hello following set: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span></span>
> 
> 

<span data-ttu-id="3b28d-120">메서드는 동기적 이며 성공 하거나 직접 hello 제한 시간 후에 실패 하거나 (기본값: 30 초 이며 too3600 초를 설정할 수 있음).</span><span class="sxs-lookup"><span data-stu-id="3b28d-120">Direct methods are synchronous and either succeed or fail after hello timeout period (default: 30 seconds, settable up too3600 seconds).</span></span> <span data-ttu-id="3b28d-121">직접 메서드는 저장할 장치 tooact hello 장치는 휴대폰에서 빛 설정 등 온라인 상태이 고 받는 명령 하는 경우에 대화형 시나리오에서 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b28d-121">Direct methods are useful in interactive scenarios where you want a device tooact if and only if hello device is online and receiving commands, such as turning on a light from a phone.</span></span> <span data-ttu-id="3b28d-122">이러한 시나리오에서 원하는 toosee 즉시 성공 또는 실패 여부는 hello 클라우드 서비스 hello 결과 대해 가능한 한 빨리 작동할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b28d-122">In these scenarios, you want toosee an immediate success or failure so hello cloud service can act on hello result as soon as possible.</span></span> <span data-ttu-id="3b28d-123">hello 장치 일부 메시지 본문이 hello 메서드의 결과로 반환할 수 있지만 hello 메서드 toodo에 필요한 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b28d-123">hello device may return some message body as a result of hello method, but it isn't required for hello method toodo so.</span></span> <span data-ttu-id="3b28d-124">메서드 호출의 순서 지정 또는 동시성 의미 체계에 대한 보장은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3b28d-124">There is no guarantee on ordering or any concurrency semantics on method calls.</span></span>

<span data-ttu-id="3b28d-125">직접적인 방법 hello 클라우드 측면에서 HTTP 전용 hello 장치 쪽에서 MQTT 전용 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b28d-125">Direct method are HTTP-only from hello cloud side, and MQTT-only from hello device side.</span></span>

<span data-ttu-id="3b28d-126">메서드 요청 및 응답에 대 한 hello 페이로드는 too8KB JSON 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="3b28d-126">hello payload for method requests and responses is a JSON document up too8KB.</span></span>

## <a name="reference-topics"></a><span data-ttu-id="3b28d-127">참조 항목:</span><span class="sxs-lookup"><span data-stu-id="3b28d-127">Reference topics:</span></span>
<span data-ttu-id="3b28d-128">hello 다음 참조 항목 제공 직접 메서드를 사용 하는 방법에 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b28d-128">hello following reference topics provide you with more information about using direct methods.</span></span>

## <a name="invoke-a-direct-method-from-a-back-end-app"></a><span data-ttu-id="3b28d-129">백 엔드 앱에서 직접 메서드 호출</span><span class="sxs-lookup"><span data-stu-id="3b28d-129">Invoke a direct method from a back-end app</span></span>
### <a name="method-invocation"></a><span data-ttu-id="3b28d-130">메서드 호출</span><span class="sxs-lookup"><span data-stu-id="3b28d-130">Method invocation</span></span>
<span data-ttu-id="3b28d-131">장치의 직접 메서드 호출은 다음을 포함하는 HTTP 호출입니다.</span><span class="sxs-lookup"><span data-stu-id="3b28d-131">Direct method invocations on a device are HTTP calls which comprise:</span></span>

* <span data-ttu-id="3b28d-132">hello *URI* 특정 toohello 장치 (`{iot hub}/twins/{device id}/methods/`)</span><span class="sxs-lookup"><span data-stu-id="3b28d-132">hello *URI* specific toohello device (`{iot hub}/twins/{device id}/methods/`)</span></span>
* <span data-ttu-id="3b28d-133">hello POST *메서드*</span><span class="sxs-lookup"><span data-stu-id="3b28d-133">hello POST *method*</span></span>
* <span data-ttu-id="3b28d-134">*헤더* hello 권한 부여는, ID, 콘텐츠 형식 및 콘텐츠 인코딩을 요청</span><span class="sxs-lookup"><span data-stu-id="3b28d-134">*Headers* which contain hello authorization, request ID, content type, and content encoding</span></span>
* <span data-ttu-id="3b28d-135">투명 한 JSON *본문* 형식에 따라 hello에:</span><span class="sxs-lookup"><span data-stu-id="3b28d-135">A transparent JSON *body* in hello following format:</span></span>

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

<span data-ttu-id="3b28d-136">시간 제한은 초 단위입니다.</span><span class="sxs-lookup"><span data-stu-id="3b28d-136">Timeout is in seconds.</span></span> <span data-ttu-id="3b28d-137">제한 시간을 설정 하지 않으면 too30 기본값으로 설정 시간 (초)입니다.</span><span class="sxs-lookup"><span data-stu-id="3b28d-137">If timeout is not set, it defaults too30 seconds.</span></span>

### <a name="response"></a><span data-ttu-id="3b28d-138">응답</span><span class="sxs-lookup"><span data-stu-id="3b28d-138">Response</span></span>
<span data-ttu-id="3b28d-139">hello 백 엔드 응용 프로그램을 구성을 응답을 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b28d-139">hello back-end app receives a response which comprises:</span></span>

* <span data-ttu-id="3b28d-140">*HTTP 상태 코드*, hello IoT 허브에서에서 제공 하는 오류에 사용 되는, 장치에 대 한 404 오류를 포함 하 여 현재 연결 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b28d-140">*HTTP status code*, which is used for errors coming from hello IoT Hub, including a 404 error for devices not currently connected</span></span>
* <span data-ttu-id="3b28d-141">*헤더* hello ETag를 포함 합니다.는, ID, 콘텐츠 형식 및 콘텐츠 인코딩을 요청</span><span class="sxs-lookup"><span data-stu-id="3b28d-141">*Headers* which contain hello ETag, request ID, content type, and content encoding</span></span>
* <span data-ttu-id="3b28d-142">JSON *본문* 형식에 따라 hello에:</span><span class="sxs-lookup"><span data-stu-id="3b28d-142">A JSON *body* in hello following format:</span></span>

```
{
    "status" : 201,
    "payload" : {...}
}
```

   <span data-ttu-id="3b28d-143">둘 다 `status` 및 `body` hello 장치에서 제공 되 고 toorespond hello 장치의 상태 코드 및/또는 설명을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b28d-143">Both `status` and `body` are provided by hello device and used toorespond with hello device's own status code and/or description.</span></span>

## <a name="handle-a-direct-method-on-a-device"></a><span data-ttu-id="3b28d-144">장치에서 직접 메서드 처리</span><span class="sxs-lookup"><span data-stu-id="3b28d-144">Handle a direct method on a device</span></span>
### <a name="method-invocation"></a><span data-ttu-id="3b28d-145">메서드 호출</span><span class="sxs-lookup"><span data-stu-id="3b28d-145">Method invocation</span></span>
<span data-ttu-id="3b28d-146">Hello MQTT 항목에 대 한 직접 메서드 요청을 수신 하는 장치:`$iothub/methods/POST/{method name}/?$rid={request id}`</span><span class="sxs-lookup"><span data-stu-id="3b28d-146">Devices receive direct method requests on hello MQTT topic: `$iothub/methods/POST/{method name}/?$rid={request id}`</span></span>

<span data-ttu-id="3b28d-147">hello 받는 hello 장치가 고, 형식에 따라 hello:</span><span class="sxs-lookup"><span data-stu-id="3b28d-147">hello body which hello device receives is in hello following format:</span></span>

```
{
    "input1": "someInput",
    "input2": "anotherInput"
}
```

<span data-ttu-id="3b28d-148">메서드 요청은 QoS 0입니다.</span><span class="sxs-lookup"><span data-stu-id="3b28d-148">Method requests are QoS 0.</span></span>

### <a name="response"></a><span data-ttu-id="3b28d-149">응답</span><span class="sxs-lookup"><span data-stu-id="3b28d-149">Response</span></span>
<span data-ttu-id="3b28d-150">hello 장치 응답을 너무 전송`$iothub/methods/res/{status}/?$rid={request id}`, 여기서:</span><span class="sxs-lookup"><span data-stu-id="3b28d-150">hello device sends responses too`$iothub/methods/res/{status}/?$rid={request id}`, where:</span></span>

* <span data-ttu-id="3b28d-151">hello `status` 속성은 메서드 실행의 hello 장치가 제공한 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="3b28d-151">hello `status` property is hello device-supplied status of method execution.</span></span>
* <span data-ttu-id="3b28d-152">hello `$rid` 속성은 IoT 허브에서 받은 hello 메서드 호출에서 hello 요청 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="3b28d-152">hello `$rid` property is hello request ID from hello method invocation received from IoT Hub.</span></span>

<span data-ttu-id="3b28d-153">hello 본문 hello 장치에 의해 설정 되 고 모든 상태의 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b28d-153">hello body is set by hello device and can be any status.</span></span>

## <a name="additional-reference-material"></a><span data-ttu-id="3b28d-154">추가 참조 자료</span><span class="sxs-lookup"><span data-stu-id="3b28d-154">Additional reference material</span></span>
<span data-ttu-id="3b28d-155">Hello IoT 허브 개발자 가이드에서에서 다른 참조 항목은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3b28d-155">Other reference topics in hello IoT Hub developer guide include:</span></span>

* <span data-ttu-id="3b28d-156">[IoT Hub 끝점] [ lnk-endpoints] 설명 hello 런타임 및 관리 작업에 대 한 각 IoT 허브를 노출 하는 다양 한 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="3b28d-156">[IoT Hub endpoints][lnk-endpoints] describes hello various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="3b28d-157">[제한 및 할당량] [ lnk-quotas] hello 서비스를 사용 하는 경우 조정 동작 tooexpect hello와 toohello IoT 허브 서비스를 적용 하는 hello 할당량에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b28d-157">[Throttling and quotas][lnk-quotas] describes hello quotas that apply toohello IoT Hub service and hello throttling behavior tooexpect when you use hello service.</span></span>
* <span data-ttu-id="3b28d-158">[Azure IoT 장치 및 서비스 Sdk] [ lnk-sdks] 목록 hello 다양 한 언어 Sdk IoT Hub와 상호 작용 하는 장치 및 서비스 모두 앱을 개발할 때 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b28d-158">[Azure IoT device and service SDKs][lnk-sdks] lists hello various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="3b28d-159">[장치 트윈스, 작업 및 메시지 라우팅에 대 한 IoT Hub 쿼리 언어] [ lnk-query] hello 장치 트윈스 및 작업에 대 한 IoT 허브에서 tooretrieve 정보를 사용 하려면 IoT Hub 쿼리 언어에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b28d-159">[IoT Hub query language for device twins, jobs, and message routing][lnk-query] describes hello IoT Hub query language you can use tooretrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="3b28d-160">[IoT 허브 MQTT 지원] [ lnk-devguide-mqtt] hello MQTT 프로토콜에 대 한 IoT Hub 지원에 대 한 자세한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b28d-160">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for hello MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3b28d-161">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3b28d-161">Next steps</span></span>
<span data-ttu-id="3b28d-162">이제 어떻게 toouse 직접 메서드 관심이 있을 수 있습니다 hello IoT 허브 개발자 가이드 항목에 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="3b28d-162">Now you have learned how toouse direct methods, you may be interested in hello following IoT Hub developer guide topic:</span></span>

* <span data-ttu-id="3b28d-163">[여러 장치에서 jobs 예약][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="3b28d-163">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="3b28d-164">이 문서에서 설명 하는 hello 개념 중 일부는 tootry, 원하는 경우 IoT Hub 자습서 hello에 관심이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b28d-164">If you would like tootry out some of hello concepts described in this article, you may be interested in hello following IoT Hub tutorial:</span></span>

* <span data-ttu-id="3b28d-165">[직접 메서드 사용][lnk-methods-tutorial]</span><span class="sxs-lookup"><span data-stu-id="3b28d-165">[Use direct methods][lnk-methods-tutorial]</span></span>

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

---
title: "Azure IoT Hub 클라우드-장치 aaaUnderstand 메시징 | Microsoft Docs"
description: "개발자 가이드-어떻게 toouse 클라우드-장치 IoT Hub와 메시징입니다. Hello 메시지 수명 주기 및 구성 옵션에 대 한 정보가 포함 됩니다."
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
ms.openlocfilehash: 5c747b50163873d823556a8baa769c4b8f7f8c44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="send-cloud-to-device-messages-from-iot-hub"></a><span data-ttu-id="0ede5-104">IoT Hub에서 클라우드-장치 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="0ede5-104">Send cloud-to-device messages from IoT Hub</span></span>

<span data-ttu-id="0ede5-105">toosend 단방향 알림 toohello 장치 응용 프로그램 솔루션 백 엔드에서 IoT 허브 tooyour 장치에서 클라우드-장치 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-105">toosend one-way notifications toohello device app from your solution back end, send cloud-to-devices messages from your IoT hub tooyour device.</span></span> <span data-ttu-id="0ede5-106">IoT Hub가 지원하는 다른 클라우드-장치 옵션에 대한 설명은 [클라우드-장치 통신 지침][lnk-c2d-guidance]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0ede5-106">For a discussion of other cloud-to-devices options supported by IoT Hub, see [Cloud-to-device communications guidance][lnk-c2d-guidance].</span></span>

<span data-ttu-id="0ede5-107">서비스 지향 끝점(**/messages/devicebound**)을 통해 클라우드-장치 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-107">You send cloud-to-device messages through a service-facing endpoint (**/messages/devicebound**).</span></span> <span data-ttu-id="0ede5-108">장치를 장치 특정 끝점을 통해 hello 메시지 받습니다 (**/devices/ {deviceId} / 메시지/devicebound**).</span><span class="sxs-lookup"><span data-stu-id="0ede5-108">A device then receives hello messages through a device-specific endpoint (**/devices/{deviceId}/messages/devicebound**).</span></span>

<span data-ttu-id="0ede5-109">각 클라우드-장치 메시지 대상으로 하는 단일 장치 hello 설정 하 여 **를** 속성 너무**/devices/ {deviceId} / 메시지/devicebound**합니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-109">Each cloud-to-device message is targeted at a single device by setting hello **to** property too**/devices/{deviceId}/messages/devicebound**.</span></span>

<span data-ttu-id="0ede5-110">각 장치 큐는 클라우드-장치 메시지를 최대 50개까지 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-110">Each device queue holds at most 50 cloud-to-device messages.</span></span> <span data-ttu-id="0ede5-111">더 많은 메시지 toohello toosend 시도 같은 장치는 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-111">Trying toosend more messages toohello same device results in an error.</span></span>

## <a name="hello-cloud-to-device-message-lifecycle"></a><span data-ttu-id="0ede5-112">hello 클라우드-장치 메시지 수명 주기</span><span class="sxs-lookup"><span data-stu-id="0ede5-112">hello cloud-to-device message lifecycle</span></span>

<span data-ttu-id="0ede5-113">IoT Hub tooguarantee에서-최소 1 회 메시지 배달을 장치 단위 큐에 있는 클라우드-장치 메시지를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-113">tooguarantee at-least-once message delivery, IoT Hub persists cloud-to-device messages in per-device queues.</span></span> <span data-ttu-id="0ede5-114">장치를 명시적으로 승인 해야 *완료* 큐 hello에서 IoT Hub tooremove에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-114">Devices must explicitly acknowledge *completion* for IoT Hub tooremove them from hello queue.</span></span> <span data-ttu-id="0ede5-115">이 방법은 연결 및 장치 오류로부터 복원력을 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-115">This approach guarantees resiliency against connectivity and device failures.</span></span>

<span data-ttu-id="0ede5-116">hello 다음 다이어그램 그래프를 보여 줍니다 hello 수명 주기 상태 클라우드-장치 메시지에 대 한 IoT Hub에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-116">hello following diagram shows hello lifecycle state graph for a cloud-to-device message in IoT Hub.</span></span>

![클라우드-장치 메시지 수명 주기][img-lifecycle]

<span data-ttu-id="0ede5-118">IoT Hub 서비스 hello 메시지 tooa 장치, hello 서비스를 보낼 때 설정 하는 hello 메시지 상태 너무**큐에 대기 된**합니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-118">When hello IoT Hub service sends a message tooa device, hello service sets hello message state too**Enqueued**.</span></span> <span data-ttu-id="0ede5-119">장치가 너무 경우*수신* 메시지가 IoT Hub *잠금* hello 메시지 (너무 hello 상태를 설정 하 여**보이지 않는**), 다른 스레드에서 hello 장치 toostart에서 허용 하는 다른 메시지를 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-119">When a device wants too*receive* a message, IoT Hub *locks* hello message (by setting hello state too**Invisible**), which allows other threads on hello device toostart receiving other messages.</span></span> <span data-ttu-id="0ede5-120">장치 스레드 hello 메시지 처리를 완료 하 여 IoT Hub 알립니다 *완료* hello 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-120">When a device thread completes hello processing of a message, it notifies IoT Hub by *completing* hello message.</span></span> <span data-ttu-id="0ede5-121">IoT Hub 다음 상태를 설정 hello 너무**Completed**합니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-121">IoT Hub then sets hello state too**Completed**.</span></span>

<span data-ttu-id="0ede5-122">장치는 다음을 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-122">A device can also choose to:</span></span>

* <span data-ttu-id="0ede5-123">*거부* hello 메시지를 IoT Hub tooset 것 toohello **배달 못한 메시지로 분류** 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-123">*Reject* hello message, which causes IoT Hub tooset it toohello **Deadlettered** state.</span></span> <span data-ttu-id="0ede5-124">Hello MQTT 프로토콜을 통해 연결 하는 장치는 클라우드-장치 메시지를 거부할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-124">Devices that connect over hello MQTT protocol cannot reject cloud-to-device messages.</span></span>
* <span data-ttu-id="0ede5-125">*중단* hello 메시지를 IoT Hub tooput hello 메시지 hello 큐에 다시 hello 상태 너무 설정 하 여**큐에 대기 된**합니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-125">*Abandon* hello message, which causes IoT Hub tooput hello message back in hello queue, with hello state set too**Enqueued**.</span></span>

<span data-ttu-id="0ede5-126">스레드는 tooprocess 메시지가 IoT Hub에 게 알리지 않고 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-126">A thread could fail tooprocess a message without notifying IoT Hub.</span></span> <span data-ttu-id="0ede5-127">이 경우 메시지를 자동으로 hello에서 전환을 **보이지 않는** 상태 백 toohello **큐에 대기 된** 후 상태는 *표시 유형 (또는 잠금) 시간 초과*합니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-127">In this case, messages automatically transition from hello **Invisible** state back toohello **Enqueued** state after a *visibility (or lock) timeout*.</span></span> <span data-ttu-id="0ede5-128">이 시간 제한의 hello 기본 값은 1 분입니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-128">hello default value of this timeout is one minute.</span></span>

<span data-ttu-id="0ede5-129">메시지 hello 간에 전환할 수 **큐에 대기 된** 및 **보이지 않는** 에 대 한 상태에는 기껏해야 hello에 지정 된 횟수 만큼 hello **최대 배달 횟수** IoT 허브에서 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-129">A message can transition between hello **Enqueued** and **Invisible** states for, at most, hello number of times specified in hello **max delivery count** property on IoT Hub.</span></span> <span data-ttu-id="0ede5-130">IoT Hub 해당 전환 횟수 후 hello 메시지의 hello 상태 너무 설정**배달 못한 메시지로 분류**합니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-130">After that number of transitions, IoT Hub sets hello state of hello message too**Deadlettered**.</span></span> <span data-ttu-id="0ede5-131">마찬가지로, IoT 허브 상태를 설정 hello 메시지의 너무**배달 못한 메시지로 분류** 만료 시간 이후 (참조 [시간 toolive][lnk-ttl]).</span><span class="sxs-lookup"><span data-stu-id="0ede5-131">Similarly, IoT Hub sets hello state of a message too**Deadlettered** after its expiration time (see [Time toolive][lnk-ttl]).</span></span>

<span data-ttu-id="0ede5-132">hello [IoT Hub와 toosend 클라우드-장치 메시지 방법을] [ lnk-c2d-tutorial] hello에서 클라우드-장치 메시지 toosend 클라우드 하 고 장치에서 수신 하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-132">hello [How toosend cloud-to-device messages with IoT Hub][lnk-c2d-tutorial] shows you how toosend cloud-to-device messages from hello cloud and receive them on a device.</span></span>

<span data-ttu-id="0ede5-133">일반적으로 장치는 hello hello 메시지의 영향을 주지 않습니다 hello 응용 프로그램 논리 경우 클라우드-장치 메시지를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-133">Typically, a device completes a cloud-to-device message when hello loss of hello message does not affect hello application logic.</span></span> <span data-ttu-id="0ede5-134">예를 들어 때 hello hello 메시지 콘텐츠를 로컬로 지속에 장치나 작업 처리가 성공적으로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-134">For example, when hello device has persisted hello message content locally or has successfully executed an operation.</span></span> <span data-ttu-id="0ede5-135">hello 메시지 인 손실 hello hello 응용 프로그램의 기능에 영향을 주지는 일시적인 정보를 수행할 수도 수입니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-135">hello message could also carry transient information, whose loss would not impact hello functionality of hello application.</span></span> <span data-ttu-id="0ede5-136">경우에 따라 장기 실행 작업에 대 한 צ ְ ײ hello 클라우드-장치 메시지를 유지 한 후 hello 로컬 저장소에 대 한 작업 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-136">Sometimes, for long-running tasks, you can complete hello cloud-to-device message after persisting hello task description in local storage.</span></span> <span data-ttu-id="0ede5-137">그런 다음 hello 작업의 진행률의 여러 단계에서 하나 이상의 장치-클라우드 메시지와 함께 hello 솔루션 백 엔드에 알릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-137">Then you can notify hello solution back end with one or more device-to-cloud messages at various stages of progress of hello task.</span></span>

## <a name="message-expiration-time-toolive"></a><span data-ttu-id="0ede5-138">메시지 만료 (toolive 시간)</span><span class="sxs-lookup"><span data-stu-id="0ede5-138">Message expiration (time toolive)</span></span>

<span data-ttu-id="0ede5-139">모든 클라우드-장치 메시지에는 만료 시간이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-139">Every cloud-to-device message has an expiration time.</span></span> <span data-ttu-id="0ede5-140">이 이번 hello 서비스에 의해 설정 됩니다 (hello에 **ExpiryTimeUtc** 속성), 또는 기본 hello를 사용 하 여 IoT 허브 *시간 toolive* IoT Hub 속성으로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-140">This time is set either by hello service (in hello **ExpiryTimeUtc** property), or by IoT Hub using hello default *time toolive* specified as an IoT Hub property.</span></span> <span data-ttu-id="0ede5-141">[클라우드-장치 구성 옵션][lnk-c2d-configuration]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0ede5-141">See [Cloud-to-device configuration options][lnk-c2d-configuration].</span></span>

<span data-ttu-id="0ede5-142">일반적인 방식으로 tootake 장점은 만료 메시지 및 toodisconnected 장치 메시지를 전송 하지 않도록, tooset toolive 짧은 시간 값이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-142">A common way tootake advantage of message expiration and avoid sending messages toodisconnected devices, is tooset short time toolive values.</span></span> <span data-ttu-id="0ede5-143">이 방법은 hello 보다 효율적인 하면서 hello 장치 연결 상태를 유지 관리와 같은 결과 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-143">This approach achieves hello same result as maintaining hello device connection state, while being more efficient.</span></span> <span data-ttu-id="0ede5-144">메시지 승인이 요청 하는 경우 장치는 수 tooreceive 메시지 이며 어떤 장치가 온라인 상태 인지 실패 한 IoT Hub 알립니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-144">When you request message acknowledgements, IoT Hub notifies you which devices are able tooreceive messages, and which devices are not online or have failed.</span></span>

## <a name="message-feedback"></a><span data-ttu-id="0ede5-145">메시지 피드백</span><span class="sxs-lookup"><span data-stu-id="0ede5-145">Message feedback</span></span>

<span data-ttu-id="0ede5-146">클라우드-장치 메시지를 보내면 hello 서비스는 hello 메시지의 최종 상태에 대 한 메시지 피드백의 hello 배달을 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-146">When you send a cloud-to-device message, hello service can request hello delivery of per-message feedback regarding hello final state of that message.</span></span>

| <span data-ttu-id="0ede5-147">Ack 속성</span><span class="sxs-lookup"><span data-stu-id="0ede5-147">Ack property</span></span> | <span data-ttu-id="0ede5-148">동작</span><span class="sxs-lookup"><span data-stu-id="0ede5-148">Behavior</span></span> |
| ------------ | -------- |
| <span data-ttu-id="0ede5-149">**positive**</span><span class="sxs-lookup"><span data-stu-id="0ede5-149">**positive**</span></span> | <span data-ttu-id="0ede5-150">IoT Hub 피드백 메시지를 생성 하 고 hello 클라우드-장치 메시지 hello에 도달한 경우에 **Completed** 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-150">IoT Hub generates a feedback message if, and only if, hello cloud-to-device message reached hello **Completed** state.</span></span> |
| <span data-ttu-id="0ede5-151">**negative**</span><span class="sxs-lookup"><span data-stu-id="0ede5-151">**negative**</span></span> | <span data-ttu-id="0ede5-152">IoT Hub 및 경우에, hello 클라우드-장치 메시지 큐에 도달 hello 피드백 메시지를 생성 **배달 못한 메시지로 분류** 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-152">IoT Hub generates a feedback message, if and only if, hello cloud-to-device message reaches hello **Deadlettered** state.</span></span> |
| <span data-ttu-id="0ede5-153">**full**</span><span class="sxs-lookup"><span data-stu-id="0ede5-153">**full**</span></span>     | <span data-ttu-id="0ede5-154">IoT Hub는 어떤 경우든 피드백 메시지를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-154">IoT Hub generates a feedback message in either case.</span></span> |

<span data-ttu-id="0ede5-155">경우 **Ack** 은 **전체**, 및 피드백 메시지가, 해당 hello 피드백 메시지 만료 된 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-155">If **Ack** is **full**, and you don't receive a feedback message, it means that hello feedback message expired.</span></span> <span data-ttu-id="0ede5-156">hello 서비스 어떤 발생 했습니다 toohello 원본 메시지를 알 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-156">hello service can't know what happened toohello original message.</span></span> <span data-ttu-id="0ede5-157">실제로 서비스는 만료 되기 전에 hello 피드백을 처리할 수 있도록 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-157">In practice, a service should ensure that it can process hello feedback before it expires.</span></span> <span data-ttu-id="0ede5-158">hello 최대 만료 시간은 2 일 수 있는 충분 한 시간 tooget hello 서비스를 다시 실행 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-158">hello maximum expiry time is two days, which allows plenty of time tooget hello service running again if a failure occurs.</span></span>

<span data-ttu-id="0ede5-159">[끝점][lnk-endpoints]에 설명된 대로 IoT Hub는 서비스 지향 끝점(**/messages/servicebound/feedback**)을 통해 피드백을 메시지로 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-159">As explained in [Endpoints][lnk-endpoints], IoT Hub delivers feedback through a service-facing endpoint (**/messages/servicebound/feedback**) as messages.</span></span> <span data-ttu-id="0ede5-160">hello 의미 체계 의견을 받기 위한 클라우드-장치 메시지의 경우와 동일는 hello와 같은 hello가 [메시지 수명 주기][lnk-lifecycle]합니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-160">hello semantics for receiving feedback are hello same as for cloud-to-device messages, and have hello same [Message lifecycle][lnk-lifecycle].</span></span> <span data-ttu-id="0ede5-161">가능 하면 항상 피드백 메시지 일괄 처리 되는 단일 메시지에서 형식에 따라 hello로:</span><span class="sxs-lookup"><span data-stu-id="0ede5-161">Whenever possible, message feedback is batched in a single message, with hello following format:</span></span>

| <span data-ttu-id="0ede5-162">속성</span><span class="sxs-lookup"><span data-stu-id="0ede5-162">Property</span></span>     | <span data-ttu-id="0ede5-163">설명</span><span class="sxs-lookup"><span data-stu-id="0ede5-163">Description</span></span> |
| ------------ | ----------- |
| <span data-ttu-id="0ede5-164">EnqueuedTime</span><span class="sxs-lookup"><span data-stu-id="0ede5-164">EnqueuedTime</span></span> | <span data-ttu-id="0ede5-165">Hello 메시지를 만들 때를 나타내는 타임 스탬프입니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-165">Timestamp indicating when hello message was created.</span></span> |
| <span data-ttu-id="0ede5-166">UserId</span><span class="sxs-lookup"><span data-stu-id="0ede5-166">UserId</span></span>       | `{iot hub name}` |
| <span data-ttu-id="0ede5-167">ContentType</span><span class="sxs-lookup"><span data-stu-id="0ede5-167">ContentType</span></span>  | `application/vnd.microsoft.iothub.feedback.json` |

<span data-ttu-id="0ede5-168">hello 본문은 다음과 같은 속성 hello로 각 레코드의 JSON 직렬화 된 배열:</span><span class="sxs-lookup"><span data-stu-id="0ede5-168">hello body is a JSON-serialized array of records, each with hello following properties:</span></span>

| <span data-ttu-id="0ede5-169">속성</span><span class="sxs-lookup"><span data-stu-id="0ede5-169">Property</span></span>           | <span data-ttu-id="0ede5-170">설명</span><span class="sxs-lookup"><span data-stu-id="0ede5-170">Description</span></span> |
| ------------------ | ----------- |
| <span data-ttu-id="0ede5-171">EnqueuedTimeUtc</span><span class="sxs-lookup"><span data-stu-id="0ede5-171">EnqueuedTimeUtc</span></span>    | <span data-ttu-id="0ede5-172">Hello 메시지의 hello 결과 발생 한 시기를 나타내는 타임 스탬프입니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-172">Timestamp indicating when hello outcome of hello message happened.</span></span> <span data-ttu-id="0ede5-173">예를 들어 완료 하는 장치를 hello 또는 hello 메시지는 만료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-173">For example, hello device completed or hello message expired.</span></span> |
| <span data-ttu-id="0ede5-174">OriginalMessageId</span><span class="sxs-lookup"><span data-stu-id="0ede5-174">OriginalMessageId</span></span>  | <span data-ttu-id="0ede5-175">**MessageId** hello 클라우드-장치 메시지 toowhich의이 사용자 의견 정보를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-175">**MessageId** of hello cloud-to-device message toowhich this feedback information relates.</span></span> |
| <span data-ttu-id="0ede5-176">StatusCode</span><span class="sxs-lookup"><span data-stu-id="0ede5-176">StatusCode</span></span>         | <span data-ttu-id="0ede5-177">필수 문자열</span><span class="sxs-lookup"><span data-stu-id="0ede5-177">Required string.</span></span> <span data-ttu-id="0ede5-178">IoT Hub에 의해 생성된 피드백 메시지에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-178">Used in feedback messages generated by IoT Hub.</span></span> <br/> <span data-ttu-id="0ede5-179">'Success'</span><span class="sxs-lookup"><span data-stu-id="0ede5-179">'Success'</span></span> <br/> <span data-ttu-id="0ede5-180">'Expired'</span><span class="sxs-lookup"><span data-stu-id="0ede5-180">'Expired'</span></span> <br/> <span data-ttu-id="0ede5-181">'DeliveryCountExceeded'</span><span class="sxs-lookup"><span data-stu-id="0ede5-181">'DeliveryCountExceeded'</span></span> <br/> <span data-ttu-id="0ede5-182">'Rejected'</span><span class="sxs-lookup"><span data-stu-id="0ede5-182">'Rejected'</span></span> <br/> <span data-ttu-id="0ede5-183">'Purged'</span><span class="sxs-lookup"><span data-stu-id="0ede5-183">'Purged'</span></span> |
| <span data-ttu-id="0ede5-184">설명</span><span class="sxs-lookup"><span data-stu-id="0ede5-184">Description</span></span>        | <span data-ttu-id="0ede5-185">**StatusCode**에 대한 문자열 값입니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-185">String values for **StatusCode**.</span></span> |
| <span data-ttu-id="0ede5-186">deviceId</span><span class="sxs-lookup"><span data-stu-id="0ede5-186">DeviceId</span></span>           | <span data-ttu-id="0ede5-187">**DeviceId** hello 클라우드-장치 메시지 toowhich의 hello 대상 장치의 피드백의이 부분 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-187">**DeviceId** of hello target device of hello cloud-to-device message toowhich this piece of feedback relates.</span></span> |
| <span data-ttu-id="0ede5-188">DeviceGenerationId</span><span class="sxs-lookup"><span data-stu-id="0ede5-188">DeviceGenerationId</span></span> | <span data-ttu-id="0ede5-189">**DeviceGenerationId** hello 클라우드-장치 메시지 toowhich의 hello 대상 장치의 피드백의이 부분 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-189">**DeviceGenerationId** of hello target device of hello cloud-to-device message toowhich this piece of feedback relates.</span></span> |

<span data-ttu-id="0ede5-190">hello 서비스 지정 해야 합니다는 **MessageId** hello 클라우드-장치 메시지 toobe 수 toocorrelate 해당 피드백 hello 원본 메시지에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-190">hello service must specify a **MessageId** for hello cloud-to-device message toobe able toocorrelate its feedback with hello original message.</span></span>

<span data-ttu-id="0ede5-191">hello 다음 예제에서는 hello 피드백 메시지 본문</span><span class="sxs-lookup"><span data-stu-id="0ede5-191">hello following example shows hello body of a feedback message.</span></span>

```json
[
  {
    "OriginalMessageId": "0987654321",
    "EnqueuedTimeUtc": "2015-07-28T16:24:48.789Z",
    "StatusCode": 0,
    "Description": "Success",
    "DeviceId": "123",
    "DeviceGenerationId": "abcdefghijklmnopqrstuvwxyz"
  },
  {
    ...
  },
  ...
]
```

## <a name="cloud-to-device-configuration-options"></a><span data-ttu-id="0ede5-192">클라우드-장치 구성 옵션</span><span class="sxs-lookup"><span data-stu-id="0ede5-192">Cloud-to-device configuration options</span></span>

<span data-ttu-id="0ede5-193">각 IoT 허브는 hello 다음 클라우드-장치 메시징에 대 한 구성 옵션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-193">Each IoT hub exposes hello following configuration options for cloud-to-device messaging:</span></span>

| <span data-ttu-id="0ede5-194">속성</span><span class="sxs-lookup"><span data-stu-id="0ede5-194">Property</span></span>                  | <span data-ttu-id="0ede5-195">설명</span><span class="sxs-lookup"><span data-stu-id="0ede5-195">Description</span></span> | <span data-ttu-id="0ede5-196">범위 및 기본값</span><span class="sxs-lookup"><span data-stu-id="0ede5-196">Range and default</span></span> |
| ------------------------- | ----------- | ----------------- |
| <span data-ttu-id="0ede5-197">defaultTtlAsIso8601</span><span class="sxs-lookup"><span data-stu-id="0ede5-197">defaultTtlAsIso8601</span></span>       | <span data-ttu-id="0ede5-198">클라우드-장치 메시지에 대한 기본 TTL</span><span class="sxs-lookup"><span data-stu-id="0ede5-198">Default TTL for cloud-to-device messages.</span></span> | <span data-ttu-id="0ede5-199">Too2D ISO_8601 간격 (최소 1 분)입니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-199">ISO_8601 interval up too2D (minimum 1 minute).</span></span> <span data-ttu-id="0ede5-200">기본값은 1시간입니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-200">Default: 1 hour.</span></span> |
| <span data-ttu-id="0ede5-201">maxDeliveryCount</span><span class="sxs-lookup"><span data-stu-id="0ede5-201">maxDeliveryCount</span></span>          | <span data-ttu-id="0ede5-202">클라우드-장치 장치 단위 큐에 대한 최대 전달 수입니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-202">Maximum delivery count for cloud-to-device per-device queues.</span></span> | <span data-ttu-id="0ede5-203">1 too100 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-203">1 too100.</span></span> <span data-ttu-id="0ede5-204">기본값은 10입니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-204">Default: 10.</span></span> |
| <span data-ttu-id="0ede5-205">feedback.ttlAsIso8601</span><span class="sxs-lookup"><span data-stu-id="0ede5-205">feedback.ttlAsIso8601</span></span>     | <span data-ttu-id="0ede5-206">서비스 바인딩 피드백 메시지에 대한 보존 기간입니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-206">Retention for service-bound feedback messages.</span></span> | <span data-ttu-id="0ede5-207">Too2D ISO_8601 간격 (최소 1 분)입니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-207">ISO_8601 interval up too2D (minimum 1 minute).</span></span> <span data-ttu-id="0ede5-208">기본값은 1시간입니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-208">Default: 1 hour.</span></span> |
| <span data-ttu-id="0ede5-209">feedback.maxDeliveryCount</span><span class="sxs-lookup"><span data-stu-id="0ede5-209">feedback.maxDeliveryCount</span></span> |<span data-ttu-id="0ede5-210">피드백 큐에 대한 최대 전달 수입니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-210">Maximum delivery count for feedback queue.</span></span> | <span data-ttu-id="0ede5-211">1 too100 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-211">1 too100.</span></span> <span data-ttu-id="0ede5-212">기본값은 100입니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-212">Default: 100.</span></span> |

<span data-ttu-id="0ede5-213">Tooset 이러한 구성 옵션을 확인 하려면 어떻게 해야 하는 방법에 대 한 자세한 내용은 [만들 IoT hub][lnk-portal]합니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-213">For more information about how tooset these configuration options, see [Create IoT hubs][lnk-portal].</span></span>

## <a name="next-steps"></a><span data-ttu-id="0ede5-214">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0ede5-214">Next steps</span></span>

<span data-ttu-id="0ede5-215">Hello Sdk에 대 한 내용은 tooreceive 클라우드-장치 메시지를 사용 하 여, 참조 수 [Azure IoT Sdk][lnk-sdks]합니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-215">For information about hello SDKs you can use tooreceive cloud-to-device messages, see [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="0ede5-216">클라우드-장치 메시지를 받는 아웃 tootry 참조 hello [클라우드-장치 보내기] [ lnk-c2d-tutorial] 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="0ede5-216">tootry out receiving cloud-to-device messages, see hello [Send cloud-to-device][lnk-c2d-tutorial] tutorial.</span></span>

[img-lifecycle]: ./media/iot-hub-devguide-messages-c2d/lifecycle.png

[lnk-portal]: iot-hub-create-through-portal.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-ttl]: #message-expiration-time-to-live
[lnk-c2d-configuration]: #cloud-to-device-configuration-options
[lnk-lifecycle]: #message-lifecycle
[lnk-c2d-tutorial]: iot-hub-csharp-csharp-c2d.md

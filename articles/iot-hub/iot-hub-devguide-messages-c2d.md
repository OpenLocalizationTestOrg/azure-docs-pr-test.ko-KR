---
title: "Azure IoT Hub 클라우드-장치 메시징 이해 | Microsoft Docs"
description: "개발자 가이드 - IoT Hub를 사용하여 클라우드-장치 메시징을 사용하는 방법입니다. 메시지 수명 주기 및 구성 옵션에 대한 정보를 포함합니다."
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
ms.openlocfilehash: 04ac46498c912b0503036f70b7f3d0e28e5a82b8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="send-cloud-to-device-messages-from-iot-hub"></a><span data-ttu-id="c3077-104">IoT Hub에서 클라우드-장치 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="c3077-104">Send cloud-to-device messages from IoT Hub</span></span>

<span data-ttu-id="c3077-105">솔루션 백 엔드에서 장치 앱으로 단방향 알림을 보내려면 IoT Hub에서 장치로 클라우드-장치 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-105">To send one-way notifications to the device app from your solution back end, send cloud-to-devices messages from your IoT hub to your device.</span></span> <span data-ttu-id="c3077-106">IoT Hub가 지원하는 다른 클라우드-장치 옵션에 대한 설명은 [클라우드-장치 통신 지침][lnk-c2d-guidance]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3077-106">For a discussion of other cloud-to-devices options supported by IoT Hub, see [Cloud-to-device communications guidance][lnk-c2d-guidance].</span></span>

<span data-ttu-id="c3077-107">서비스 지향 끝점(**/messages/devicebound**)을 통해 클라우드-장치 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-107">You send cloud-to-device messages through a service-facing endpoint (**/messages/devicebound**).</span></span> <span data-ttu-id="c3077-108">그런 다음 장치는 장치별 끝점(**/devices/{deviceId}/messages/devicebound**)을 통해 메시지를 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-108">A device then receives the messages through a device-specific endpoint (**/devices/{deviceId}/messages/devicebound**).</span></span>

<span data-ttu-id="c3077-109">각 클라우드-장치 메시지는 **to** 속성을 **/devices/{deviceId}/messages/devicebound**로 설정하여 단일 장치를 대상화합니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-109">Each cloud-to-device message is targeted at a single device by setting the **to** property to **/devices/{deviceId}/messages/devicebound**.</span></span>

<span data-ttu-id="c3077-110">각 장치 큐는 클라우드-장치 메시지를 최대 50개까지 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-110">Each device queue holds at most 50 cloud-to-device messages.</span></span> <span data-ttu-id="c3077-111">동일한 장치에 더 많은 메시지를 보내려고 하면 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-111">Trying to send more messages to the same device results in an error.</span></span>

## <a name="the-cloud-to-device-message-lifecycle"></a><span data-ttu-id="c3077-112">클라우드-장치 메시지 수명 주기</span><span class="sxs-lookup"><span data-stu-id="c3077-112">The cloud-to-device message lifecycle</span></span>

<span data-ttu-id="c3077-113">메시지 전달을 한 번 이상 보장하기 위해 IoT Hub는 장치 별 큐에 클라우드-장치 메시지를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-113">To guarantee at-least-once message delivery, IoT Hub persists cloud-to-device messages in per-device queues.</span></span> <span data-ttu-id="c3077-114">IoT Hub가 큐에서 메시지를 제거하기 위해 장치가 *완료* 를 명시적으로 인정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-114">Devices must explicitly acknowledge *completion* for IoT Hub to remove them from the queue.</span></span> <span data-ttu-id="c3077-115">이 방법은 연결 및 장치 오류로부터 복원력을 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-115">This approach guarantees resiliency against connectivity and device failures.</span></span>

<span data-ttu-id="c3077-116">다음 다이어그램은 IoT Hub에서 클라우드-장치 메시지에 대한 수명 주기 상태 그래프를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-116">The following diagram shows the lifecycle state graph for a cloud-to-device message in IoT Hub.</span></span>

![클라우드-장치 메시지 수명 주기][img-lifecycle]

<span data-ttu-id="c3077-118">IoT Hub 서비스가 장치에 메시지를 보내면 서비스는 메시지 상태를 **큐에 넣음**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-118">When the IoT Hub service sends a message to a device, the service sets the message state to **Enqueued**.</span></span> <span data-ttu-id="c3077-119">장치가 메시지를 *수신*하려고 하면 IoT Hub는 상태를 **숨김**으로 설정하여 메시지를 *잠그고* 장치에 있는 다른 스레드가 다른 메시지 수신을 시작하도록 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-119">When a device wants to *receive* a message, IoT Hub *locks* the message (by setting the state to **Invisible**), which allows other threads on the device to start receiving other messages.</span></span> <span data-ttu-id="c3077-120">장치 스레드가 메시지의 처리를 완료하면 IoT Hub에 메시지를 *완료* 했다고 알립니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-120">When a device thread completes the processing of a message, it notifies IoT Hub by *completing* the message.</span></span> <span data-ttu-id="c3077-121">그런 다음 IoT Hub는 상태를 **완료**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-121">IoT Hub then sets the state to **Completed**.</span></span>

<span data-ttu-id="c3077-122">장치는 다음을 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-122">A device can also choose to:</span></span>

* <span data-ttu-id="c3077-123">메시지 *거부*. 이 경우 IoT Hub는 메시지를 **Deadlettered** 상태로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-123">*Reject* the message, which causes IoT Hub to set it to the **Deadlettered** state.</span></span> <span data-ttu-id="c3077-124">MQTT 프로토콜을 통해 연결하는 장치는 클라우드-장치 메시지를 거부할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-124">Devices that connect over the MQTT protocol cannot reject cloud-to-device messages.</span></span>
* <span data-ttu-id="c3077-125">메시지 *중단*. 이 경우 IoT Hub는 상태를 **큐에 넣음**으로 설정하여 메시지를 큐에 다시 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-125">*Abandon* the message, which causes IoT Hub to put the message back in the queue, with the state set to **Enqueued**.</span></span>

<span data-ttu-id="c3077-126">스레드는 IoT Hub에 알리지 않고 메시지를 처리하는 데 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-126">A thread could fail to process a message without notifying IoT Hub.</span></span> <span data-ttu-id="c3077-127">이 경우 *표시 또는 잠금 시간 초과* 후에 메시지는 **숨김** 상태에서 **큐에 넣음** 상태로 자동 전환됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-127">In this case, messages automatically transition from the **Invisible** state back to the **Enqueued** state after a *visibility (or lock) timeout*.</span></span> <span data-ttu-id="c3077-128">이 시간 제한의 기본값은 1분입니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-128">The default value of this timeout is one minute.</span></span>

<span data-ttu-id="c3077-129">메시지는 IoT Hub의 **최대 배달 횟수** 속성에 지정된 최대 지정된 횟수만큼 **큐에 넣음** 및 **숨김** 상태 간에 전환될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-129">A message can transition between the **Enqueued** and **Invisible** states for, at most, the number of times specified in the **max delivery count** property on IoT Hub.</span></span> <span data-ttu-id="c3077-130">해당 전환 횟수 후에 IoT Hub는 메시지의 상태를 **Deadlettered**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-130">After that number of transitions, IoT Hub sets the state of the message to **Deadlettered**.</span></span> <span data-ttu-id="c3077-131">마찬가지로 IoT Hub는 만료 시간 후에 메시지의 상태를 **Deadlettered**로 설정합니다. 관련 설명은 [TTL(Time to Live)][lnk-ttl]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3077-131">Similarly, IoT Hub sets the state of a message to **Deadlettered** after its expiration time (see [Time to live][lnk-ttl]).</span></span>

<span data-ttu-id="c3077-132">[IoT Hub를 사용하여 클라우드-장치 메시지를 보내는 방법][lnk-c2d-tutorial]에서는 클라우드에서 클라우드-장치 메시지를 보내고 장치에서 수신하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-132">The [How to send cloud-to-device messages with IoT Hub][lnk-c2d-tutorial] shows you how to send cloud-to-device messages from the cloud and receive them on a device.</span></span>

<span data-ttu-id="c3077-133">일반적으로 메시지 손실이 응용 프로그램 논리에 영향을 주지 않으면 장치가 클라우드-장치 메시지를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-133">Typically, a device completes a cloud-to-device message when the loss of the message does not affect the application logic.</span></span> <span data-ttu-id="c3077-134">예를 들어 장치가 메시지 콘텐츠를 로컬에 유지하거나 작업을 성공적으로 실행한 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-134">For example, when the device has persisted the message content locally or has successfully executed an operation.</span></span> <span data-ttu-id="c3077-135">또한 메시지가 임시 정보를 전달하고 있으므로 손실되더라도 응용 프로그램의 기능에 영향을 주지 않을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-135">The message could also carry transient information, whose loss would not impact the functionality of the application.</span></span> <span data-ttu-id="c3077-136">경우에 따라 장기간 실행되는 작업의 경우 로컬 저장소에 작업 설명을 보관한 후 클라우드-장치 메시지를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-136">Sometimes, for long-running tasks, you can complete the cloud-to-device message after persisting the task description in local storage.</span></span> <span data-ttu-id="c3077-137">그런 다음 작업이 진행되는 다양한 단계에서 하나 이상의 장치-클라우드 메시지를 사용하여 솔루션 백 엔드에 알림을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-137">Then you can notify the solution back end with one or more device-to-cloud messages at various stages of progress of the task.</span></span>

## <a name="message-expiration-time-to-live"></a><span data-ttu-id="c3077-138">메시지 만료(TTL(Time To Live))</span><span class="sxs-lookup"><span data-stu-id="c3077-138">Message expiration (time to live)</span></span>

<span data-ttu-id="c3077-139">모든 클라우드-장치 메시지에는 만료 시간이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-139">Every cloud-to-device message has an expiration time.</span></span> <span data-ttu-id="c3077-140">이 시간은 서비스에 의해 설정되거나(**ExpiryTimeUtc** 속성) IoT Hub 속성처럼 기본 *TTL(Time To Live)* 을 사용하여 IoT Hub에 의해 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-140">This time is set either by the service (in the **ExpiryTimeUtc** property), or by IoT Hub using the default *time to live* specified as an IoT Hub property.</span></span> <span data-ttu-id="c3077-141">[클라우드-장치 구성 옵션][lnk-c2d-configuration]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3077-141">See [Cloud-to-device configuration options][lnk-c2d-configuration].</span></span>

<span data-ttu-id="c3077-142">메시지 만료를 활용하여 연결되지 않은 장치에 메시지 보내기를 방지하는 일반적인 방법은 TTL(Time to Live) 값을 짧게 설정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-142">A common way to take advantage of message expiration and avoid sending messages to disconnected devices, is to set short time to live values.</span></span> <span data-ttu-id="c3077-143">이 방법은 장치 연결 상태를 유지 관리하는 것과 동일한 결과를 내면서 더 효율적입니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-143">This approach achieves the same result as maintaining the device connection state, while being more efficient.</span></span> <span data-ttu-id="c3077-144">메시지 승인을 요청하면 IoT Hub는 메시지를 수신할 수 있는 장치가 무엇인지 온라인 상태이거나 장애가 발생한 장치가 무엇인지를 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-144">When you request message acknowledgements, IoT Hub notifies you which devices are able to receive messages, and which devices are not online or have failed.</span></span>

## <a name="message-feedback"></a><span data-ttu-id="c3077-145">메시지 피드백</span><span class="sxs-lookup"><span data-stu-id="c3077-145">Message feedback</span></span>

<span data-ttu-id="c3077-146">클라우드-장치 메시지를 보낼 때 서비스는 해당 메시지의 최종 상태에 대한 메시지 단위 피드백을 전달하도록 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-146">When you send a cloud-to-device message, the service can request the delivery of per-message feedback regarding the final state of that message.</span></span>

| <span data-ttu-id="c3077-147">Ack 속성</span><span class="sxs-lookup"><span data-stu-id="c3077-147">Ack property</span></span> | <span data-ttu-id="c3077-148">동작</span><span class="sxs-lookup"><span data-stu-id="c3077-148">Behavior</span></span> |
| ------------ | -------- |
| <span data-ttu-id="c3077-149">**positive**</span><span class="sxs-lookup"><span data-stu-id="c3077-149">**positive**</span></span> | <span data-ttu-id="c3077-150">클라우드-장치 메시지가 **Completed** 상태가 되는 경우에만 IoT Hub가 피드백 메시지를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-150">IoT Hub generates a feedback message if, and only if, the cloud-to-device message reached the **Completed** state.</span></span> |
| <span data-ttu-id="c3077-151">**negative**</span><span class="sxs-lookup"><span data-stu-id="c3077-151">**negative**</span></span> | <span data-ttu-id="c3077-152">클라우드-장치 메시지가 **Deadlettered** 상태가 되는 경우에만 IoT Hub가 피드백 메시지를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-152">IoT Hub generates a feedback message, if and only if, the cloud-to-device message reaches the **Deadlettered** state.</span></span> |
| <span data-ttu-id="c3077-153">**full**</span><span class="sxs-lookup"><span data-stu-id="c3077-153">**full**</span></span>     | <span data-ttu-id="c3077-154">IoT Hub는 어떤 경우든 피드백 메시지를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-154">IoT Hub generates a feedback message in either case.</span></span> |

<span data-ttu-id="c3077-155">**Ack**가 **full**이고 피드백 메시지를 수신하지 못한 경우 피드백 메시지가 만료되었음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-155">If **Ack** is **full**, and you don't receive a feedback message, it means that the feedback message expired.</span></span> <span data-ttu-id="c3077-156">서비스는 원본 메시지에서 발생한 상황을 알지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-156">The service can't know what happened to the original message.</span></span> <span data-ttu-id="c3077-157">실제로 서비스는 만료되기 전에 피드백을 처리할 수 있는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-157">In practice, a service should ensure that it can process the feedback before it expires.</span></span> <span data-ttu-id="c3077-158">오류가 발생한 경우 서비스를 다시 가동하는 데 충분한 시간을 허용하기 위해 최대 만료 시간이 2일로 지정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-158">The maximum expiry time is two days, which allows plenty of time to get the service running again if a failure occurs.</span></span>

<span data-ttu-id="c3077-159">[끝점][lnk-endpoints]에 설명된 대로 IoT Hub는 서비스 지향 끝점(**/messages/servicebound/feedback**)을 통해 피드백을 메시지로 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-159">As explained in [Endpoints][lnk-endpoints], IoT Hub delivers feedback through a service-facing endpoint (**/messages/servicebound/feedback**) as messages.</span></span> <span data-ttu-id="c3077-160">피드백 수신을 위한 의미 체계는 클라우드-장치 메시지의 경우와 같으며 동일한 [메시지 수명 주기][lnk-lifecycle]를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-160">The semantics for receiving feedback are the same as for cloud-to-device messages, and have the same [Message lifecycle][lnk-lifecycle].</span></span> <span data-ttu-id="c3077-161">가능한 경우 메시지 피드백은 다음 형식으로 단일 메시지에서 일괄 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-161">Whenever possible, message feedback is batched in a single message, with the following format:</span></span>

| <span data-ttu-id="c3077-162">속성</span><span class="sxs-lookup"><span data-stu-id="c3077-162">Property</span></span>     | <span data-ttu-id="c3077-163">설명</span><span class="sxs-lookup"><span data-stu-id="c3077-163">Description</span></span> |
| ------------ | ----------- |
| <span data-ttu-id="c3077-164">EnqueuedTime</span><span class="sxs-lookup"><span data-stu-id="c3077-164">EnqueuedTime</span></span> | <span data-ttu-id="c3077-165">메시지를 만든 시간을 나타내는 타임스탬프입니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-165">Timestamp indicating when the message was created.</span></span> |
| <span data-ttu-id="c3077-166">UserId</span><span class="sxs-lookup"><span data-stu-id="c3077-166">UserId</span></span>       | `{iot hub name}` |
| <span data-ttu-id="c3077-167">ContentType</span><span class="sxs-lookup"><span data-stu-id="c3077-167">ContentType</span></span>  | `application/vnd.microsoft.iothub.feedback.json` |

<span data-ttu-id="c3077-168">본문은 각각 다음과 같은 속성이 있는 레코드의 JSON으로 직렬화된 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-168">The body is a JSON-serialized array of records, each with the following properties:</span></span>

| <span data-ttu-id="c3077-169">속성</span><span class="sxs-lookup"><span data-stu-id="c3077-169">Property</span></span>           | <span data-ttu-id="c3077-170">설명</span><span class="sxs-lookup"><span data-stu-id="c3077-170">Description</span></span> |
| ------------------ | ----------- |
| <span data-ttu-id="c3077-171">EnqueuedTimeUtc</span><span class="sxs-lookup"><span data-stu-id="c3077-171">EnqueuedTimeUtc</span></span>    | <span data-ttu-id="c3077-172">메시지의 결과가 발생하는 경우를 나타내는 타임스탬프입니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-172">Timestamp indicating when the outcome of the message happened.</span></span> <span data-ttu-id="c3077-173">예를 들어 완료된 장치 또는 만료된 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-173">For example, the device completed or the message expired.</span></span> |
| <span data-ttu-id="c3077-174">OriginalMessageId</span><span class="sxs-lookup"><span data-stu-id="c3077-174">OriginalMessageId</span></span>  | <span data-ttu-id="c3077-175">이 피드백 정보와 관련된 클라우드-장치 메시지의 **MessageId**입니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-175">**MessageId** of the cloud-to-device message to which this feedback information relates.</span></span> |
| <span data-ttu-id="c3077-176">StatusCode</span><span class="sxs-lookup"><span data-stu-id="c3077-176">StatusCode</span></span>         | <span data-ttu-id="c3077-177">필수 문자열</span><span class="sxs-lookup"><span data-stu-id="c3077-177">Required string.</span></span> <span data-ttu-id="c3077-178">IoT Hub에 의해 생성된 피드백 메시지에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-178">Used in feedback messages generated by IoT Hub.</span></span> <br/> <span data-ttu-id="c3077-179">'Success'</span><span class="sxs-lookup"><span data-stu-id="c3077-179">'Success'</span></span> <br/> <span data-ttu-id="c3077-180">'Expired'</span><span class="sxs-lookup"><span data-stu-id="c3077-180">'Expired'</span></span> <br/> <span data-ttu-id="c3077-181">'DeliveryCountExceeded'</span><span class="sxs-lookup"><span data-stu-id="c3077-181">'DeliveryCountExceeded'</span></span> <br/> <span data-ttu-id="c3077-182">'Rejected'</span><span class="sxs-lookup"><span data-stu-id="c3077-182">'Rejected'</span></span> <br/> <span data-ttu-id="c3077-183">'Purged'</span><span class="sxs-lookup"><span data-stu-id="c3077-183">'Purged'</span></span> |
| <span data-ttu-id="c3077-184">설명</span><span class="sxs-lookup"><span data-stu-id="c3077-184">Description</span></span>        | <span data-ttu-id="c3077-185">**StatusCode**에 대한 문자열 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-185">String values for **StatusCode**.</span></span> |
| <span data-ttu-id="c3077-186">deviceId</span><span class="sxs-lookup"><span data-stu-id="c3077-186">DeviceId</span></span>           | <span data-ttu-id="c3077-187">피드백의 해당 부분과 관련된 클라우드-장치 메시지에서 대상 장치의 **DeviceId**입니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-187">**DeviceId** of the target device of the cloud-to-device message to which this piece of feedback relates.</span></span> |
| <span data-ttu-id="c3077-188">DeviceGenerationId</span><span class="sxs-lookup"><span data-stu-id="c3077-188">DeviceGenerationId</span></span> | <span data-ttu-id="c3077-189">피드백의 해당 부분과 관련된 클라우드-장치 메시지에서 대상 장치의 **DeviceGenerationId**입니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-189">**DeviceGenerationId** of the target device of the cloud-to-device message to which this piece of feedback relates.</span></span> |

<span data-ttu-id="c3077-190">서비스는 원본 메시지와 해당 피드백을 상호 연결하기 위해 클라우드-장치 메시지에 대한 **MessageId** 를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-190">The service must specify a **MessageId** for the cloud-to-device message to be able to correlate its feedback with the original message.</span></span>

<span data-ttu-id="c3077-191">다음 예제에서는 피드백 메시지의 본문을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-191">The following example shows the body of a feedback message.</span></span>

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

## <a name="cloud-to-device-configuration-options"></a><span data-ttu-id="c3077-192">클라우드-장치 구성 옵션</span><span class="sxs-lookup"><span data-stu-id="c3077-192">Cloud-to-device configuration options</span></span>

<span data-ttu-id="c3077-193">각 IoT Hub는 클라우드-장치 메시징에 다음 구성 옵션을 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-193">Each IoT hub exposes the following configuration options for cloud-to-device messaging:</span></span>

| <span data-ttu-id="c3077-194">속성</span><span class="sxs-lookup"><span data-stu-id="c3077-194">Property</span></span>                  | <span data-ttu-id="c3077-195">설명</span><span class="sxs-lookup"><span data-stu-id="c3077-195">Description</span></span> | <span data-ttu-id="c3077-196">범위 및 기본값</span><span class="sxs-lookup"><span data-stu-id="c3077-196">Range and default</span></span> |
| ------------------------- | ----------- | ----------------- |
| <span data-ttu-id="c3077-197">defaultTtlAsIso8601</span><span class="sxs-lookup"><span data-stu-id="c3077-197">defaultTtlAsIso8601</span></span>       | <span data-ttu-id="c3077-198">클라우드-장치 메시지에 대한 기본 TTL</span><span class="sxs-lookup"><span data-stu-id="c3077-198">Default TTL for cloud-to-device messages.</span></span> | <span data-ttu-id="c3077-199">최대 2D(최소 1 분)까지 ISO_8601 간격입니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-199">ISO_8601 interval up to 2D (minimum 1 minute).</span></span> <span data-ttu-id="c3077-200">기본값은 1시간입니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-200">Default: 1 hour.</span></span> |
| <span data-ttu-id="c3077-201">maxDeliveryCount</span><span class="sxs-lookup"><span data-stu-id="c3077-201">maxDeliveryCount</span></span>          | <span data-ttu-id="c3077-202">클라우드-장치 장치 단위 큐에 대한 최대 전달 수입니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-202">Maximum delivery count for cloud-to-device per-device queues.</span></span> | <span data-ttu-id="c3077-203">1에서 100까지 입니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-203">1 to 100.</span></span> <span data-ttu-id="c3077-204">기본값은 10입니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-204">Default: 10.</span></span> |
| <span data-ttu-id="c3077-205">feedback.ttlAsIso8601</span><span class="sxs-lookup"><span data-stu-id="c3077-205">feedback.ttlAsIso8601</span></span>     | <span data-ttu-id="c3077-206">서비스 바인딩 피드백 메시지에 대한 보존 기간입니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-206">Retention for service-bound feedback messages.</span></span> | <span data-ttu-id="c3077-207">최대 2D(최소 1 분)까지 ISO_8601 간격입니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-207">ISO_8601 interval up to 2D (minimum 1 minute).</span></span> <span data-ttu-id="c3077-208">기본값은 1시간입니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-208">Default: 1 hour.</span></span> |
| <span data-ttu-id="c3077-209">feedback.maxDeliveryCount</span><span class="sxs-lookup"><span data-stu-id="c3077-209">feedback.maxDeliveryCount</span></span> |<span data-ttu-id="c3077-210">피드백 큐에 대한 최대 전달 수입니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-210">Maximum delivery count for feedback queue.</span></span> | <span data-ttu-id="c3077-211">1에서 100까지 입니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-211">1 to 100.</span></span> <span data-ttu-id="c3077-212">기본값은 100입니다.</span><span class="sxs-lookup"><span data-stu-id="c3077-212">Default: 100.</span></span> |

<span data-ttu-id="c3077-213">이러한 구성 옵션을 설정하는 방법에 대한 자세한 내용은 [IoT Hub 만들기][lnk-portal]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3077-213">For more information about how to set these configuration options, see [Create IoT hubs][lnk-portal].</span></span>

## <a name="next-steps"></a><span data-ttu-id="c3077-214">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c3077-214">Next steps</span></span>

<span data-ttu-id="c3077-215">클라우드-장치 메시지를 수신하는 데 사용할 수 있는 SDK에 대한 자세한 내용은 [Azure IoT SDK][lnk-sdks]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3077-215">For information about the SDKs you can use to receive cloud-to-device messages, see [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="c3077-216">클라우드-장치 메시지를 수신하려면 [클라우드-장치 보내기][lnk-c2d-tutorial] 자습서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3077-216">To try out receiving cloud-to-device messages, see the [Send cloud-to-device][lnk-c2d-tutorial] tutorial.</span></span>

[img-lifecycle]: ./media/iot-hub-devguide-messages-c2d/lifecycle.png

[lnk-portal]: iot-hub-create-through-portal.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-ttl]: #message-expiration-time-to-live
[lnk-c2d-configuration]: #cloud-to-device-configuration-options
[lnk-lifecycle]: #message-lifecycle
[lnk-c2d-tutorial]: iot-hub-csharp-csharp-c2d.md

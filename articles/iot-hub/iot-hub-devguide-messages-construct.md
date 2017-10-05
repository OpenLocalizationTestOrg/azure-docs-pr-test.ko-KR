---
title: "Azure IoT Hub 메시징 형식 이해 | Microsoft Docs"
description: "개발자 가이드 - IoT Hub 메시지의 형식 및 예상된 콘텐츠를 설명합니다."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 3fc5f1a3-3711-4611-9897-d4db079b4250
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: e6eafb1a0030b022da2b5d0b787e092f3067c99f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="create-and-read-iot-hub-messages"></a><span data-ttu-id="29d92-103">IoT Hub 메시지 만들기 및 읽기</span><span class="sxs-lookup"><span data-stu-id="29d92-103">Create and read IoT Hub messages</span></span>

<span data-ttu-id="29d92-104">프로토콜을 통해 원활한 상호 운용성을 지원하기 위해 IoT Hub는 모든 장치 지향 프로토콜에 대한 일반적인 메시지 형식을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="29d92-104">To support seamless interoperability across protocols, IoT Hub defines a common message format for all device-facing protocols.</span></span> <span data-ttu-id="29d92-105">이 메시지 형식은 [장치-클라우드][lnk-d2c] 및 [클라우드-장치][lnk-c2d] 메시지 둘 다에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="29d92-105">This message format is used for both [device-to-cloud][lnk-d2c] and [cloud-to-device][lnk-c2d] messages.</span></span> <span data-ttu-id="29d92-106">[IoT Hub 메시지][lnk-messaging]는 다음으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="29d92-106">An [IoT Hub message][lnk-messaging] consists of:</span></span>

* <span data-ttu-id="29d92-107">*시스템 속성*집합.</span><span class="sxs-lookup"><span data-stu-id="29d92-107">A set of *system properties*.</span></span> <span data-ttu-id="29d92-108">IoT Hub가 해석하거나 설정하는 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="29d92-108">Properties that IoT Hub interprets or sets.</span></span> <span data-ttu-id="29d92-109">이 집합은 미리 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="29d92-109">This set is predetermined.</span></span>
* <span data-ttu-id="29d92-110">*응용 프로그램 속성*집합.</span><span class="sxs-lookup"><span data-stu-id="29d92-110">A set of *application properties*.</span></span> <span data-ttu-id="29d92-111">메시지 본문을 역직렬화할 필요 없이 응용 프로그램이 정의하고 액세스할 수 있는 문자열 속성 사전입니다.</span><span class="sxs-lookup"><span data-stu-id="29d92-111">A dictionary of string properties that the application can define and access, without needing to deserialize the message body.</span></span> <span data-ttu-id="29d92-112">IoT Hub는 절대로 이러한 속성을 수정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="29d92-112">IoT Hub never modifies these properties.</span></span>
* <span data-ttu-id="29d92-113">불투명한 이진 본문.</span><span class="sxs-lookup"><span data-stu-id="29d92-113">An opaque binary body.</span></span>

<span data-ttu-id="29d92-114">속성 이름과 값은 다음과 같은 경우에 ASCII 영숫자 문자와 ``{'!', '#', '$', '%, '&', "'", '*', '*', '+', '-', '.', '^', '_', '`', '|', '~'}`\`를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29d92-114">Property names and values can only contain ASCII alphanumeric characters, plus ``{'!', '#', '$', '%, '&', "'", '*', '*', '+', '-', '.', '^', '_', '`', '|', '~'}`\` when you:</span></span>

* <span data-ttu-id="29d92-115">HTTP 프로토콜을 사용하여 장치-클라우드 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="29d92-115">Send device-to-cloud messages using the HTTP protocol.</span></span>
* <span data-ttu-id="29d92-116">클라우드-장치 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="29d92-116">Send cloud-to-device messages.</span></span>

<span data-ttu-id="29d92-117">다른 프로토콜을 사용하여 보낸 메시지를 인코딩하고 디코딩하는 방법에 대한 자세한 내용은 [Azure IoT SDK][lnk-sdks]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="29d92-117">For more information about how to encode and decode messages sent using different protocols, see [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="29d92-118">다음 테이블에는 IoT Hub 메시지의 시스템 속성 집합이 나열되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29d92-118">The following table lists the set of system properties in IoT Hub messages.</span></span>

| <span data-ttu-id="29d92-119">속성</span><span class="sxs-lookup"><span data-stu-id="29d92-119">Property</span></span> | <span data-ttu-id="29d92-120">설명</span><span class="sxs-lookup"><span data-stu-id="29d92-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="29d92-121">MessageId</span><span class="sxs-lookup"><span data-stu-id="29d92-121">MessageId</span></span> |<span data-ttu-id="29d92-122">사용자가 설정할 수 있는 메시지에 대한 식별자는 요청-회신 패턴에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="29d92-122">A user-settable identifier for the message used for request-reply patterns.</span></span> <span data-ttu-id="29d92-123">형식: ASCII 7 비트 영숫자 문자 + `{'-', ':',’.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '$', '''}`의 대/소문자 구분 문자열(최대 128자 길이)입니다.</span><span class="sxs-lookup"><span data-stu-id="29d92-123">Format: A case-sensitive string (up to 128 characters long) of ASCII 7-bit alphanumeric characters + `{'-', ':',’.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '$', '''}`.</span></span> |
| <span data-ttu-id="29d92-124">시퀀스 번호</span><span class="sxs-lookup"><span data-stu-id="29d92-124">Sequence number</span></span> |<span data-ttu-id="29d92-125">숫자(장치 큐 별로 고유함)는 IoT Hub에서 각 클라우드-장치 메시지에 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="29d92-125">A number (unique per device-queue) assigned by IoT Hub to each cloud-to-device message.</span></span> |
| <span data-ttu-id="29d92-126">받는 사람</span><span class="sxs-lookup"><span data-stu-id="29d92-126">To</span></span> |<span data-ttu-id="29d92-127">[클라우드-장치][lnk-c2d] 메시지에 지정된 대상입니다.</span><span class="sxs-lookup"><span data-stu-id="29d92-127">A destination specified in [Cloud-to-Device][lnk-c2d] messages.</span></span> |
| <span data-ttu-id="29d92-128">ExpiryTimeUtc</span><span class="sxs-lookup"><span data-stu-id="29d92-128">ExpiryTimeUtc</span></span> |<span data-ttu-id="29d92-129">메시지 만료 날짜 및 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="29d92-129">Date and time of message expiration.</span></span> |
| <span data-ttu-id="29d92-130">EnqueuedTime</span><span class="sxs-lookup"><span data-stu-id="29d92-130">EnqueuedTime</span></span> |<span data-ttu-id="29d92-131">IoT Hub에서 [클라우드-장치][lnk-c2d] 메시지를 수신한 날짜 및 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="29d92-131">Date and time the [Cloud-to-Device][lnk-c2d] message was received by IoT Hub.</span></span> |
| <span data-ttu-id="29d92-132">CorrelationId</span><span class="sxs-lookup"><span data-stu-id="29d92-132">CorrelationId</span></span> |<span data-ttu-id="29d92-133">일반적으로 요청-응답 패턴으로 요청의 MessageId가 포함된 응답 메시지의 String 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="29d92-133">A string property in a response message that typically contains the MessageId of the request, in request-reply patterns.</span></span> |
| <span data-ttu-id="29d92-134">UserId</span><span class="sxs-lookup"><span data-stu-id="29d92-134">UserId</span></span> |<span data-ttu-id="29d92-135">메시지의 원본을 지정하는 데 사용되는 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="29d92-135">An ID used to specify the origin of messages.</span></span> <span data-ttu-id="29d92-136">메시지가 IoT Hub에서 생성되면 `{iot hub name}`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="29d92-136">When messages are generated by IoT Hub, it is set to `{iot hub name}`.</span></span> |
| <span data-ttu-id="29d92-137">Ack</span><span class="sxs-lookup"><span data-stu-id="29d92-137">Ack</span></span> |<span data-ttu-id="29d92-138">피드백 메시지 생성기입니다.</span><span class="sxs-lookup"><span data-stu-id="29d92-138">A feedback message generator.</span></span> <span data-ttu-id="29d92-139">이 속성은 장치에서 소비하는 메시지의 결과로 피드백 메시지를 생성하는 IoT Hub를 요청하기 위해 클라우드-장치 메시지에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="29d92-139">This property is used in cloud-to-device messages to request IoT Hub to generate feedback messages as a result of the consumption of the message by the device.</span></span> <span data-ttu-id="29d92-140">가능한 값: **none**(기본값): 피드백 메시지가 생성되지 않습니다. **positive**: 메시지가 완료된 경우 피드백 메시지를 받습니다. **negative**: 장치에서 완료되지 않고 메시지가 만료(또는 최대 전달 횟수에 도달)되면 피드백 메시지를 받습니다. **full**: positive 및 negative 모두입니다.</span><span class="sxs-lookup"><span data-stu-id="29d92-140">Possible values: **none** (default): no feedback message is generated, **positive**: receive a feedback message if the message was completed, **negative**: receive a feedback message if the message expired (or maximum delivery count was reached) without being completed by the device, or **full**: both positive and negative.</span></span> <span data-ttu-id="29d92-141">자세한 내용은 [메시지 피드백][lnk-feedback]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="29d92-141">For more information, see [Message feedback][lnk-feedback].</span></span> |
| <span data-ttu-id="29d92-142">ConnectionDeviceId</span><span class="sxs-lookup"><span data-stu-id="29d92-142">ConnectionDeviceId</span></span> |<span data-ttu-id="29d92-143">IoT Hub에서 장치-클라우드 메시지에 설정하는 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="29d92-143">An ID set by IoT Hub on device-to-cloud messages.</span></span> <span data-ttu-id="29d92-144">메시지를 보낸 장치의 **deviceId** 를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="29d92-144">It contains the **deviceId** of the device that sent the message.</span></span> |
| <span data-ttu-id="29d92-145">ConnectionDeviceGenerationId</span><span class="sxs-lookup"><span data-stu-id="29d92-145">ConnectionDeviceGenerationId</span></span> |<span data-ttu-id="29d92-146">IoT Hub에서 장치-클라우드 메시지에 설정하는 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="29d92-146">An ID set by IoT Hub on device-to-cloud messages.</span></span> <span data-ttu-id="29d92-147">메시지를 보낸 장치의 **generationId**([장치 ID 속성][lnk-device-properties]당)를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="29d92-147">It contains the **generationId** (as per [Device identity properties][lnk-device-properties]) of the device that sent the message.</span></span> |
| <span data-ttu-id="29d92-148">ConnectionAuthMethod</span><span class="sxs-lookup"><span data-stu-id="29d92-148">ConnectionAuthMethod</span></span> |<span data-ttu-id="29d92-149">IoT Hub에서 장치-클라우드 메시지에 설정하는 인증 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="29d92-149">An authentication method set by IoT Hub on device-to-cloud messages.</span></span> <span data-ttu-id="29d92-150">이 속성에는 메시지를 보내는 장치를 인증하는 데 사용되는 인증 방법에 대한 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="29d92-150">This property contains information about the authentication method used to authenticate the device sending the message.</span></span> <span data-ttu-id="29d92-151">자세한 내용은 [장치-클라우드 스푸핑 방지][lnk-antispoofing]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="29d92-151">For more information, see [Device to cloud anti-spoofing][lnk-antispoofing].</span></span> |

## <a name="message-size"></a><span data-ttu-id="29d92-152">메시지 크기</span><span class="sxs-lookup"><span data-stu-id="29d92-152">Message size</span></span>

<span data-ttu-id="29d92-153">IoT Hub는 실제 페이로드만을 고려하여 프로토콜 진단 방식으로 메시지 크기를 측정합니다.</span><span class="sxs-lookup"><span data-stu-id="29d92-153">IoT Hub measures message size in a protocol-agnostic way, considering only the actual payload.</span></span> <span data-ttu-id="29d92-154">크기(바이트 단위)는 다음의 합계로 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="29d92-154">The size in bytes is calculated as the sum of the following:</span></span>

* <span data-ttu-id="29d92-155">본문 크기(바이트)입니다.</span><span class="sxs-lookup"><span data-stu-id="29d92-155">The body size in bytes.</span></span>
* <span data-ttu-id="29d92-156">모든 메시지 시스템 속성 값의 크기(바이트)입니다.</span><span class="sxs-lookup"><span data-stu-id="29d92-156">The size in bytes of all the values of the message system properties.</span></span>
* <span data-ttu-id="29d92-157">모든 사용자 속성 이름 및 값의 크기(바이트 단위)</span><span class="sxs-lookup"><span data-stu-id="29d92-157">The size in bytes of all user property names and values.</span></span>

<span data-ttu-id="29d92-158">속성 이름과 값은 ASCII 문자로 제한되므로 문자열의 길이는 바이트 단위의 크기와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="29d92-158">Property names and values are limited to ASCII characters, so the length of the strings equals the size in bytes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="29d92-159">다음 단계</span><span class="sxs-lookup"><span data-stu-id="29d92-159">Next steps</span></span>

<span data-ttu-id="29d92-160">IoT Hub의 메시지 크기 제한에 대한 자세한 내용은 [IoT Hub 할당량 및 제한][lnk-quotas]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="29d92-160">For information about message size limits in IoT Hub, see [IoT Hub quotas and throttling][lnk-quotas].</span></span>

<span data-ttu-id="29d92-161">다양한 프로그래밍 언어로 IoT Hub 메시지를 만들고 읽는 방법을 배우려면 [시작하기][lnk-get-started] 자습서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="29d92-161">To learn how to create and read IoT Hub messages in various programming languages, see the [Get started][lnk-get-started] tutorials.</span></span>

[lnk-messaging]: iot-hub-devguide-messaging.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-get-started]: iot-hub-get-started.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-feedback]: iot-hub-devguide-messages-c2d.md#message-feedback
[lnk-device-properties]: iot-hub-devguide-identity-registry.md#device-identity-properties
[lnk-antispoofing]: iot-hub-devguide-messages-d2c.md#anti-spoofing-properties

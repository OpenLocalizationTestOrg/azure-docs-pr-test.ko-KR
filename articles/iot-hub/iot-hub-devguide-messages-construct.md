---
title: "aaaUnderstand Azure IoT Hub 메시지 형식 | Microsoft Docs"
description: "개발자 가이드-구형 hello 예상의 형식과 내용을 IoT Hub 메시지입니다."
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
ms.openlocfilehash: 3b1567e47bc32f70c0c252996648c4035ae81243
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-read-iot-hub-messages"></a><span data-ttu-id="bef0b-103">IoT Hub 메시지 만들기 및 읽기</span><span class="sxs-lookup"><span data-stu-id="bef0b-103">Create and read IoT Hub messages</span></span>

<span data-ttu-id="bef0b-104">프로토콜을 통해 완전 한 상호 운용성 toosupport IoT Hub에 장치에 연결 하는 모든 프로토콜에 대 한 일반적인 메시지 형식을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="bef0b-104">toosupport seamless interoperability across protocols, IoT Hub defines a common message format for all device-facing protocols.</span></span> <span data-ttu-id="bef0b-105">이 메시지 형식은 [장치-클라우드][lnk-d2c] 및 [클라우드-장치][lnk-c2d] 메시지 둘 다에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="bef0b-105">This message format is used for both [device-to-cloud][lnk-d2c] and [cloud-to-device][lnk-c2d] messages.</span></span> <span data-ttu-id="bef0b-106">[IoT Hub 메시지][lnk-messaging]는 다음으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="bef0b-106">An [IoT Hub message][lnk-messaging] consists of:</span></span>

* <span data-ttu-id="bef0b-107">*시스템 속성*집합.</span><span class="sxs-lookup"><span data-stu-id="bef0b-107">A set of *system properties*.</span></span> <span data-ttu-id="bef0b-108">IoT Hub가 해석하거나 설정하는 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="bef0b-108">Properties that IoT Hub interprets or sets.</span></span> <span data-ttu-id="bef0b-109">이 집합은 미리 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="bef0b-109">This set is predetermined.</span></span>
* <span data-ttu-id="bef0b-110">*응용 프로그램 속성*집합.</span><span class="sxs-lookup"><span data-stu-id="bef0b-110">A set of *application properties*.</span></span> <span data-ttu-id="bef0b-111">Hello 응용 프로그램을 정의할 수 있는 문자열 속성 및 toodeserialize hello 메시지 본문 없이 액세스의 사전입니다.</span><span class="sxs-lookup"><span data-stu-id="bef0b-111">A dictionary of string properties that hello application can define and access, without needing toodeserialize hello message body.</span></span> <span data-ttu-id="bef0b-112">IoT Hub는 절대로 이러한 속성을 수정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bef0b-112">IoT Hub never modifies these properties.</span></span>
* <span data-ttu-id="bef0b-113">불투명한 이진 본문.</span><span class="sxs-lookup"><span data-stu-id="bef0b-113">An opaque binary body.</span></span>

<span data-ttu-id="bef0b-114">속성 이름과 값은 다음과 같은 경우에 ASCII 영숫자 문자와 ``{'!', '#', '$', '%, '&', "'", '*', '*', '+', '-', '.', '^', '_', '`', '|', '~'}`\`를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bef0b-114">Property names and values can only contain ASCII alphanumeric characters, plus ``{'!', '#', '$', '%, '&', "'", '*', '*', '+', '-', '.', '^', '_', '`', '|', '~'}`\` when you:</span></span>

* <span data-ttu-id="bef0b-115">Hello HTTP 프로토콜을 사용 하 여 장치-클라우드 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="bef0b-115">Send device-to-cloud messages using hello HTTP protocol.</span></span>
* <span data-ttu-id="bef0b-116">클라우드-장치 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="bef0b-116">Send cloud-to-device messages.</span></span>

<span data-ttu-id="bef0b-117">방법에 대 한 자세한 내용은 tooencode 서로 다른 프로토콜을 사용 하 여 보낸 메시지를 디코딩할 참조 및 [Azure IoT Sdk][lnk-sdks]합니다.</span><span class="sxs-lookup"><span data-stu-id="bef0b-117">For more information about how tooencode and decode messages sent using different protocols, see [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="bef0b-118">다음 표에 hello hello 메시지 IoT 허브에서에서 시스템 속성 집합을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="bef0b-118">hello following table lists hello set of system properties in IoT Hub messages.</span></span>

| <span data-ttu-id="bef0b-119">속성</span><span class="sxs-lookup"><span data-stu-id="bef0b-119">Property</span></span> | <span data-ttu-id="bef0b-120">설명</span><span class="sxs-lookup"><span data-stu-id="bef0b-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="bef0b-121">MessageId</span><span class="sxs-lookup"><span data-stu-id="bef0b-121">MessageId</span></span> |<span data-ttu-id="bef0b-122">요청-회신 패턴에 사용 되는 hello 메시지에 대 한 사용자 설정 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="bef0b-122">A user-settable identifier for hello message used for request-reply patterns.</span></span> <span data-ttu-id="bef0b-123">형식: 대/소문자 구분 문자열 (위쪽 too128 자)는 영숫자 ASCII 7 비트 + `{'-', ':',’.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '$', '''}`합니다.</span><span class="sxs-lookup"><span data-stu-id="bef0b-123">Format: A case-sensitive string (up too128 characters long) of ASCII 7-bit alphanumeric characters + `{'-', ':',’.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '$', '''}`.</span></span> |
| <span data-ttu-id="bef0b-124">시퀀스 번호</span><span class="sxs-lookup"><span data-stu-id="bef0b-124">Sequence number</span></span> |<span data-ttu-id="bef0b-125">고유한 장치 큐가 할당 한 번호 IoT Hub tooeach 클라우드-장치 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="bef0b-125">A number (unique per device-queue) assigned by IoT Hub tooeach cloud-to-device message.</span></span> |
| <span data-ttu-id="bef0b-126">너무</span><span class="sxs-lookup"><span data-stu-id="bef0b-126">too</span></span>|<span data-ttu-id="bef0b-127">[클라우드-장치][lnk-c2d] 메시지에 지정된 대상입니다.</span><span class="sxs-lookup"><span data-stu-id="bef0b-127">A destination specified in [Cloud-to-Device][lnk-c2d] messages.</span></span> |
| <span data-ttu-id="bef0b-128">ExpiryTimeUtc</span><span class="sxs-lookup"><span data-stu-id="bef0b-128">ExpiryTimeUtc</span></span> |<span data-ttu-id="bef0b-129">메시지 만료 날짜 및 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="bef0b-129">Date and time of message expiration.</span></span> |
| <span data-ttu-id="bef0b-130">EnqueuedTime</span><span class="sxs-lookup"><span data-stu-id="bef0b-130">EnqueuedTime</span></span> |<span data-ttu-id="bef0b-131">날짜 및 시간 hello [클라우드-장치] [ lnk-c2d] IoT 허브에서 메시지를 받았습니다.</span><span class="sxs-lookup"><span data-stu-id="bef0b-131">Date and time hello [Cloud-to-Device][lnk-c2d] message was received by IoT Hub.</span></span> |
| <span data-ttu-id="bef0b-132">CorrelationId</span><span class="sxs-lookup"><span data-stu-id="bef0b-132">CorrelationId</span></span> |<span data-ttu-id="bef0b-133">일반적으로 요청-회신 패턴의 hello 요청 MessageId hello를 포함 하는 응답 메시지에 사용 되는 문자열 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="bef0b-133">A string property in a response message that typically contains hello MessageId of hello request, in request-reply patterns.</span></span> |
| <span data-ttu-id="bef0b-134">UserId</span><span class="sxs-lookup"><span data-stu-id="bef0b-134">UserId</span></span> |<span data-ttu-id="bef0b-135">ID는 toospecify hello 원본 메시지를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bef0b-135">An ID used toospecify hello origin of messages.</span></span> <span data-ttu-id="bef0b-136">너무 설정 메시지가 IoT 허브에 의해 생성 되 면`{iot hub name}`합니다.</span><span class="sxs-lookup"><span data-stu-id="bef0b-136">When messages are generated by IoT Hub, it is set too`{iot hub name}`.</span></span> |
| <span data-ttu-id="bef0b-137">Ack</span><span class="sxs-lookup"><span data-stu-id="bef0b-137">Ack</span></span> |<span data-ttu-id="bef0b-138">피드백 메시지 생성기입니다.</span><span class="sxs-lookup"><span data-stu-id="bef0b-138">A feedback message generator.</span></span> <span data-ttu-id="bef0b-139">이 속성은 hello 장치별 hello 메시지의 hello 소비로 인해 클라우드-장치 메시지 toorequest IoT Hub toogenerate 피드백 메시지에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bef0b-139">This property is used in cloud-to-device messages toorequest IoT Hub toogenerate feedback messages as a result of hello consumption of hello message by hello device.</span></span> <span data-ttu-id="bef0b-140">가능한 값: **none** (기본값): 없음 피드백 메시지가 생성 되 **양의**: hello 메시지 완료 된 경우 피드백 메시지가 **음수**: 수신는 피드백 메시지 hello 메시지는 만료 되었습니다 (또는 최대 배달 횟수에 도달 했습니다) hello 장치에 의해 완료 되 고 없는 경우 또는 **전체**: 긍정 및 부정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bef0b-140">Possible values: **none** (default): no feedback message is generated, **positive**: receive a feedback message if hello message was completed, **negative**: receive a feedback message if hello message expired (or maximum delivery count was reached) without being completed by hello device, or **full**: both positive and negative.</span></span> <span data-ttu-id="bef0b-141">자세한 내용은 [메시지 피드백][lnk-feedback]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bef0b-141">For more information, see [Message feedback][lnk-feedback].</span></span> |
| <span data-ttu-id="bef0b-142">ConnectionDeviceId</span><span class="sxs-lookup"><span data-stu-id="bef0b-142">ConnectionDeviceId</span></span> |<span data-ttu-id="bef0b-143">IoT Hub에서 장치-클라우드 메시지에 설정하는 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="bef0b-143">An ID set by IoT Hub on device-to-cloud messages.</span></span> <span data-ttu-id="bef0b-144">Hello 포함 되어 **deviceId** hello 메시지를 보낸 hello 장치의 합니다.</span><span class="sxs-lookup"><span data-stu-id="bef0b-144">It contains hello **deviceId** of hello device that sent hello message.</span></span> |
| <span data-ttu-id="bef0b-145">ConnectionDeviceGenerationId</span><span class="sxs-lookup"><span data-stu-id="bef0b-145">ConnectionDeviceGenerationId</span></span> |<span data-ttu-id="bef0b-146">IoT Hub에서 장치-클라우드 메시지에 설정하는 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="bef0b-146">An ID set by IoT Hub on device-to-cloud messages.</span></span> <span data-ttu-id="bef0b-147">Hello 포함 되어 **generationId** (기준으로 [장치 id 속성][lnk-device-properties]) hello 메시지를 보낸 hello 장치의 합니다.</span><span class="sxs-lookup"><span data-stu-id="bef0b-147">It contains hello **generationId** (as per [Device identity properties][lnk-device-properties]) of hello device that sent hello message.</span></span> |
| <span data-ttu-id="bef0b-148">ConnectionAuthMethod</span><span class="sxs-lookup"><span data-stu-id="bef0b-148">ConnectionAuthMethod</span></span> |<span data-ttu-id="bef0b-149">IoT Hub에서 장치-클라우드 메시지에 설정하는 인증 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="bef0b-149">An authentication method set by IoT Hub on device-to-cloud messages.</span></span> <span data-ttu-id="bef0b-150">이 속성 hello 메시지를 보내는 hello 인증 사용 하는 방법 tooauthenticate hello 장치에 대 한 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="bef0b-150">This property contains information about hello authentication method used tooauthenticate hello device sending hello message.</span></span> <span data-ttu-id="bef0b-151">자세한 내용은 참조 [장치 toocloud 스푸핑 방지][lnk-antispoofing]합니다.</span><span class="sxs-lookup"><span data-stu-id="bef0b-151">For more information, see [Device toocloud anti-spoofing][lnk-antispoofing].</span></span> |

## <a name="message-size"></a><span data-ttu-id="bef0b-152">메시지 크기</span><span class="sxs-lookup"><span data-stu-id="bef0b-152">Message size</span></span>

<span data-ttu-id="bef0b-153">IoT Hub 측정만 hello 실제 페이로드를 고려 프로토콜을 알 수 없는 방식으로 메시지 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="bef0b-153">IoT Hub measures message size in a protocol-agnostic way, considering only hello actual payload.</span></span> <span data-ttu-id="bef0b-154">hello 크기 (바이트) hello 다음의 hello 합계로 계산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bef0b-154">hello size in bytes is calculated as hello sum of hello following:</span></span>

* <span data-ttu-id="bef0b-155">hello 본문 크기 (바이트)입니다.</span><span class="sxs-lookup"><span data-stu-id="bef0b-155">hello body size in bytes.</span></span>
* <span data-ttu-id="bef0b-156">hello hello 메시지 시스템 속성의 모든 hello 값의 바이트 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="bef0b-156">hello size in bytes of all hello values of hello message system properties.</span></span>
* <span data-ttu-id="bef0b-157">모든 사용자 속성 이름 및 값의 바이트 hello 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="bef0b-157">hello size in bytes of all user property names and values.</span></span>

<span data-ttu-id="bef0b-158">속성 이름 및 값은 제한 tooASCII 문자 hello hello 문자열 길이 크기를 바이트 단위로 hello와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="bef0b-158">Property names and values are limited tooASCII characters, so hello length of hello strings equals hello size in bytes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bef0b-159">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bef0b-159">Next steps</span></span>

<span data-ttu-id="bef0b-160">IoT Hub의 메시지 크기 제한에 대한 자세한 내용은 [IoT Hub 할당량 및 제한][lnk-quotas]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bef0b-160">For information about message size limits in IoT Hub, see [IoT Hub quotas and throttling][lnk-quotas].</span></span>

<span data-ttu-id="bef0b-161">toolearn toocreate 및 다양 한 프로그래밍 언어의 읽기 IoT Hub 메시지를 확인 하려면 어떻게 hello [시작] [ lnk-get-started] 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="bef0b-161">toolearn how toocreate and read IoT Hub messages in various programming languages, see hello [Get started][lnk-get-started] tutorials.</span></span>

[lnk-messaging]: iot-hub-devguide-messaging.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-get-started]: iot-hub-get-started.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-feedback]: iot-hub-devguide-messages-c2d.md#message-feedback
[lnk-device-properties]: iot-hub-devguide-identity-registry.md#device-identity-properties
[lnk-antispoofing]: iot-hub-devguide-messages-d2c.md#anti-spoofing-properties

---
title: "B2B 모니터링-에 대 한 추적 스키마 aaaAS2 Azure 논리 앱 | Microsoft Docs"
description: "A s 2를 사용 하 여 Azure 통합 계정에서 트랜잭션에서 스키마 toomonitor B2B 메시지를 추적 합니다."
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: f169c411-1bd7-4554-80c1-84351247bf94
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: fe3c5845e2e80160d6857d8c308d836e88af7331
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="start-or-enable-tracking-of-as2-messages-and-mdns-toomonitor-success-errors-and-message-properties"></a><span data-ttu-id="3ced1-103">시작 또는 AS2 메시지와 Mdn toomonitor 성공, 오류 및 메시지 속성 추적을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="3ced1-103">Start or enable tracking of AS2 messages and MDNs toomonitor success, errors, and message properties</span></span>
<span data-ttu-id="3ced1-104">이러한 AS2 추적 스키마를 사용할 수 있습니다 동시 비즈니스 (B2B) 트랜잭션을 Azure 통합 계정 toohelp에서 모니터링:</span><span class="sxs-lookup"><span data-stu-id="3ced1-104">You can use these AS2 tracking schemas in your Azure integration account toohelp you monitor business-to-business (B2B) transactions:</span></span>

* <span data-ttu-id="3ced1-105">AS2 메시지 추적 스키마</span><span class="sxs-lookup"><span data-stu-id="3ced1-105">AS2 message tracking schema</span></span>
* <span data-ttu-id="3ced1-106">AS2 MDN 추적 스키마</span><span class="sxs-lookup"><span data-stu-id="3ced1-106">AS2 MDN tracking schema</span></span>

## <a name="as2-message-tracking-schema"></a><span data-ttu-id="3ced1-107">AS2 메시지 추적 스키마</span><span class="sxs-lookup"><span data-stu-id="3ced1-107">AS2 message tracking schema</span></span>
````java

    {
       "agreementProperties": {  
            "senderPartnerName": "",  
            "receiverPartnerName": "",  
            "as2To": "",  
            "as2From": "",  
            "agreementName": ""  
        },  
        "messageProperties": {
            "direction": "",
            "messageId": "",
            "dispositionType": "",
            "fileName": "",
            "isMessageFailed": "",
            "isMessageSigned": "",
            "isMessageEncrypted": "",
            "isMessageCompressed": "",
            "correlationMessageId": "",
            "incomingHeaders": {
            },
            "outgoingHeaders": {
            },
        "isNrrEnabled": "",
        "isMdnExpected": "",
        "mdnType": ""
        }
    }
````

| <span data-ttu-id="3ced1-108">속성</span><span class="sxs-lookup"><span data-stu-id="3ced1-108">Property</span></span> | <span data-ttu-id="3ced1-109">형식</span><span class="sxs-lookup"><span data-stu-id="3ced1-109">Type</span></span> | <span data-ttu-id="3ced1-110">설명</span><span class="sxs-lookup"><span data-stu-id="3ced1-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3ced1-111">senderPartnerName</span><span class="sxs-lookup"><span data-stu-id="3ced1-111">senderPartnerName</span></span> | <span data-ttu-id="3ced1-112">string</span><span class="sxs-lookup"><span data-stu-id="3ced1-112">String</span></span> | <span data-ttu-id="3ced1-113">AS2 메시지 보낸 사람의 파트너 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3ced1-113">AS2 message sender's partner name.</span></span> <span data-ttu-id="3ced1-114">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="3ced1-114">(Optional)</span></span> |
| <span data-ttu-id="3ced1-115">receiverPartnerName</span><span class="sxs-lookup"><span data-stu-id="3ced1-115">receiverPartnerName</span></span> | <span data-ttu-id="3ced1-116">string</span><span class="sxs-lookup"><span data-stu-id="3ced1-116">String</span></span> | <span data-ttu-id="3ced1-117">AS2 메시지 받는 사람의 파트너 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3ced1-117">AS2 message receiver's partner name.</span></span> <span data-ttu-id="3ced1-118">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="3ced1-118">(Optional)</span></span> |
| <span data-ttu-id="3ced1-119">as2To</span><span class="sxs-lookup"><span data-stu-id="3ced1-119">as2To</span></span> | <span data-ttu-id="3ced1-120">문자열</span><span class="sxs-lookup"><span data-stu-id="3ced1-120">String</span></span> | <span data-ttu-id="3ced1-121">Hello AS2 메시지의 hello 헤더에서 AS2 메시지 받는 사람 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3ced1-121">AS2 message receiver’s name, from hello headers of hello AS2 message.</span></span> <span data-ttu-id="3ced1-122">(필수)</span><span class="sxs-lookup"><span data-stu-id="3ced1-122">(Mandatory)</span></span> |
| <span data-ttu-id="3ced1-123">as2From</span><span class="sxs-lookup"><span data-stu-id="3ced1-123">as2From</span></span> | <span data-ttu-id="3ced1-124">문자열</span><span class="sxs-lookup"><span data-stu-id="3ced1-124">String</span></span> | <span data-ttu-id="3ced1-125">Hello AS2 메시지의 hello 헤더에서 AS2 메시지 보낸 사람의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3ced1-125">AS2 message sender’s name, from hello headers of hello AS2 message.</span></span> <span data-ttu-id="3ced1-126">(필수)</span><span class="sxs-lookup"><span data-stu-id="3ced1-126">(Mandatory)</span></span> |
| <span data-ttu-id="3ced1-127">agreementName</span><span class="sxs-lookup"><span data-stu-id="3ced1-127">agreementName</span></span> | <span data-ttu-id="3ced1-128">문자열</span><span class="sxs-lookup"><span data-stu-id="3ced1-128">String</span></span> | <span data-ttu-id="3ced1-129">Hello AS2 계약 toowhich hello 메시지의 이름 확인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3ced1-129">Name of hello AS2 agreement toowhich hello messages are resolved.</span></span> <span data-ttu-id="3ced1-130">(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="3ced1-130">(Optional)</span></span> |
| <span data-ttu-id="3ced1-131">direction</span><span class="sxs-lookup"><span data-stu-id="3ced1-131">direction</span></span> | <span data-ttu-id="3ced1-132">문자열</span><span class="sxs-lookup"><span data-stu-id="3ced1-132">String</span></span> | <span data-ttu-id="3ced1-133">Hello 메시지 흐름의 방향을 수신 또는 송신 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ced1-133">Direction of hello message flow, receive or send.</span></span> <span data-ttu-id="3ced1-134">(필수)</span><span class="sxs-lookup"><span data-stu-id="3ced1-134">(Mandatory)</span></span> |
| <span data-ttu-id="3ced1-135">messageId</span><span class="sxs-lookup"><span data-stu-id="3ced1-135">messageId</span></span> | <span data-ttu-id="3ced1-136">문자열</span><span class="sxs-lookup"><span data-stu-id="3ced1-136">String</span></span> | <span data-ttu-id="3ced1-137">(선택 사항) hello AS2 메시지의 hello 헤더에서 AS2 메시지 ID</span><span class="sxs-lookup"><span data-stu-id="3ced1-137">AS2 message ID, from hello headers of hello AS2 message (Optional)</span></span> |
| <span data-ttu-id="3ced1-138">dispositionType</span><span class="sxs-lookup"><span data-stu-id="3ced1-138">dispositionType</span></span> |<span data-ttu-id="3ced1-139">문자열</span><span class="sxs-lookup"><span data-stu-id="3ced1-139">String</span></span> | <span data-ttu-id="3ced1-140">MDN(메시지 처리 알림) 처리 유형 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3ced1-140">Message Disposition Notification (MDN) disposition type value.</span></span> <span data-ttu-id="3ced1-141">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="3ced1-141">(Optional)</span></span> |
| <span data-ttu-id="3ced1-142">fileName</span><span class="sxs-lookup"><span data-stu-id="3ced1-142">fileName</span></span> | <span data-ttu-id="3ced1-143">문자열</span><span class="sxs-lookup"><span data-stu-id="3ced1-143">String</span></span> | <span data-ttu-id="3ced1-144">Hello AS2 메시지의 hello 헤더에서 파일 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3ced1-144">File name, from hello header of hello AS2 message.</span></span> <span data-ttu-id="3ced1-145">(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="3ced1-145">(Optional)</span></span> |
| <span data-ttu-id="3ced1-146">isMessageFailed</span><span class="sxs-lookup"><span data-stu-id="3ced1-146">isMessageFailed</span></span> |<span data-ttu-id="3ced1-147">Boolean</span><span class="sxs-lookup"><span data-stu-id="3ced1-147">Boolean</span></span> | <span data-ttu-id="3ced1-148">여부 hello AS2 메시지가 실패 했습니다.</span><span class="sxs-lookup"><span data-stu-id="3ced1-148">Whether hello AS2 message failed.</span></span> <span data-ttu-id="3ced1-149">(필수)</span><span class="sxs-lookup"><span data-stu-id="3ced1-149">(Mandatory)</span></span> |
| <span data-ttu-id="3ced1-150">isMessageSigned</span><span class="sxs-lookup"><span data-stu-id="3ced1-150">isMessageSigned</span></span> | <span data-ttu-id="3ced1-151">Boolean</span><span class="sxs-lookup"><span data-stu-id="3ced1-151">Boolean</span></span> | <span data-ttu-id="3ced1-152">Hello AS2 메시지가 서명 되었는지 여부를</span><span class="sxs-lookup"><span data-stu-id="3ced1-152">Whether hello AS2 message was signed.</span></span> <span data-ttu-id="3ced1-153">(필수)</span><span class="sxs-lookup"><span data-stu-id="3ced1-153">(Mandatory)</span></span> |
| <span data-ttu-id="3ced1-154">isMessageEncrypted</span><span class="sxs-lookup"><span data-stu-id="3ced1-154">isMessageEncrypted</span></span> | <span data-ttu-id="3ced1-155">Boolean</span><span class="sxs-lookup"><span data-stu-id="3ced1-155">Boolean</span></span> | <span data-ttu-id="3ced1-156">Hello AS2 메시지를 암호화 되었는지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="3ced1-156">Whether hello AS2 message was encrypted.</span></span> <span data-ttu-id="3ced1-157">(필수)</span><span class="sxs-lookup"><span data-stu-id="3ced1-157">(Mandatory)</span></span> |
| <span data-ttu-id="3ced1-158">isMessageCompressed</span><span class="sxs-lookup"><span data-stu-id="3ced1-158">isMessageCompressed</span></span> |<span data-ttu-id="3ced1-159">Boolean</span><span class="sxs-lookup"><span data-stu-id="3ced1-159">Boolean</span></span> | <span data-ttu-id="3ced1-160">Hello AS2 메시지를 압축 되었는지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="3ced1-160">Whether hello AS2 message was compressed.</span></span> <span data-ttu-id="3ced1-161">(필수)</span><span class="sxs-lookup"><span data-stu-id="3ced1-161">(Mandatory)</span></span> |
| <span data-ttu-id="3ced1-162">correlationMessageId</span><span class="sxs-lookup"><span data-stu-id="3ced1-162">correlationMessageId</span></span> | <span data-ttu-id="3ced1-163">문자열</span><span class="sxs-lookup"><span data-stu-id="3ced1-163">String</span></span> | <span data-ttu-id="3ced1-164">Mdn 사용 하 여 toocorrelate 메시지 AS2 메시지 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="3ced1-164">AS2 message ID, toocorrelate messages with MDNs.</span></span> <span data-ttu-id="3ced1-165">(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="3ced1-165">(Optional)</span></span> |
| <span data-ttu-id="3ced1-166">incomingHeaders</span><span class="sxs-lookup"><span data-stu-id="3ced1-166">incomingHeaders</span></span> |<span data-ttu-id="3ced1-167">JToken의 사전</span><span class="sxs-lookup"><span data-stu-id="3ced1-167">Dictionary of JToken</span></span> | <span data-ttu-id="3ced1-168">들어오는 AS2 메시지 헤더 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="3ced1-168">Incoming AS2 message header details.</span></span> <span data-ttu-id="3ced1-169">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="3ced1-169">(Optional)</span></span> |
| <span data-ttu-id="3ced1-170">outgoingHeaders</span><span class="sxs-lookup"><span data-stu-id="3ced1-170">outgoingHeaders</span></span> |<span data-ttu-id="3ced1-171">JToken의 사전</span><span class="sxs-lookup"><span data-stu-id="3ced1-171">Dictionary of JToken</span></span> | <span data-ttu-id="3ced1-172">보내는 AS2 메시지 헤더 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="3ced1-172">Outgoing AS2 message header details.</span></span> <span data-ttu-id="3ced1-173">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="3ced1-173">(Optional)</span></span> |
| <span data-ttu-id="3ced1-174">isNrrEnabled</span><span class="sxs-lookup"><span data-stu-id="3ced1-174">isNrrEnabled</span></span> | <span data-ttu-id="3ced1-175">Boolean</span><span class="sxs-lookup"><span data-stu-id="3ced1-175">Boolean</span></span> | <span data-ttu-id="3ced1-176">Hello 값은 알 수 없는 경우 기본값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ced1-176">Use default value if hello value is not known.</span></span> <span data-ttu-id="3ced1-177">(필수)</span><span class="sxs-lookup"><span data-stu-id="3ced1-177">(Mandatory)</span></span> |
| <span data-ttu-id="3ced1-178">isMdnExpected</span><span class="sxs-lookup"><span data-stu-id="3ced1-178">isMdnExpected</span></span> | <span data-ttu-id="3ced1-179">Boolean</span><span class="sxs-lookup"><span data-stu-id="3ced1-179">Boolean</span></span> | <span data-ttu-id="3ced1-180">Hello 값은 알 수 없는 경우 기본값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ced1-180">Use default value if hello value is not known.</span></span> <span data-ttu-id="3ced1-181">(필수)</span><span class="sxs-lookup"><span data-stu-id="3ced1-181">(Mandatory)</span></span> |
| <span data-ttu-id="3ced1-182">mdnType</span><span class="sxs-lookup"><span data-stu-id="3ced1-182">mdnType</span></span> | <span data-ttu-id="3ced1-183">열거형</span><span class="sxs-lookup"><span data-stu-id="3ced1-183">Enum</span></span> | <span data-ttu-id="3ced1-184">허용되는 값은 **NotConfigured**, **Sync** 또는 **Async**입니다.</span><span class="sxs-lookup"><span data-stu-id="3ced1-184">Allowed values are **NotConfigured**, **Sync**, and **Async**.</span></span> <span data-ttu-id="3ced1-185">필수 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="3ced1-185">(Mandatory)</span></span> |

## <a name="as2-mdn-tracking-schema"></a><span data-ttu-id="3ced1-186">AS2 MDN 추적 스키마</span><span class="sxs-lookup"><span data-stu-id="3ced1-186">AS2 MDN tracking schema</span></span>
````java

    {
        "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "as2To": "",
                "as2From": "",
                "agreementName": "g"
            },
            "messageProperties": {
                "direction": "",
                "messageId": "",
                "originalMessageId": "",
                "dispositionType": "",
                "isMessageFailed": "",
                "isMessageSigned": "",
                "isNrrEnabled": "",
                "statusCode": "",
                "micVerificationStatus": "",
                "correlationMessageId": "",
                "incomingHeaders": {
                },
                "outgoingHeaders": {
                }
            }
    }
````

| <span data-ttu-id="3ced1-187">속성</span><span class="sxs-lookup"><span data-stu-id="3ced1-187">Property</span></span> | <span data-ttu-id="3ced1-188">형식</span><span class="sxs-lookup"><span data-stu-id="3ced1-188">Type</span></span> | <span data-ttu-id="3ced1-189">설명</span><span class="sxs-lookup"><span data-stu-id="3ced1-189">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3ced1-190">senderPartnerName</span><span class="sxs-lookup"><span data-stu-id="3ced1-190">senderPartnerName</span></span> | <span data-ttu-id="3ced1-191">string</span><span class="sxs-lookup"><span data-stu-id="3ced1-191">String</span></span> | <span data-ttu-id="3ced1-192">AS2 메시지 보낸 사람의 파트너 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3ced1-192">AS2 message sender's partner name.</span></span> <span data-ttu-id="3ced1-193">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="3ced1-193">(Optional)</span></span> |
| <span data-ttu-id="3ced1-194">receiverPartnerName</span><span class="sxs-lookup"><span data-stu-id="3ced1-194">receiverPartnerName</span></span> | <span data-ttu-id="3ced1-195">string</span><span class="sxs-lookup"><span data-stu-id="3ced1-195">String</span></span> | <span data-ttu-id="3ced1-196">AS2 메시지 받는 사람의 파트너 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3ced1-196">AS2 message receiver's partner name.</span></span> <span data-ttu-id="3ced1-197">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="3ced1-197">(Optional)</span></span> |
| <span data-ttu-id="3ced1-198">as2To</span><span class="sxs-lookup"><span data-stu-id="3ced1-198">as2To</span></span> | <span data-ttu-id="3ced1-199">문자열</span><span class="sxs-lookup"><span data-stu-id="3ced1-199">String</span></span> | <span data-ttu-id="3ced1-200">Hello AS2 메시지 받는 사람 파트너 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3ced1-200">Partner name who receives hello AS2 message.</span></span> <span data-ttu-id="3ced1-201">(필수)</span><span class="sxs-lookup"><span data-stu-id="3ced1-201">(Mandatory)</span></span> |
| <span data-ttu-id="3ced1-202">as2From</span><span class="sxs-lookup"><span data-stu-id="3ced1-202">as2From</span></span> | <span data-ttu-id="3ced1-203">문자열</span><span class="sxs-lookup"><span data-stu-id="3ced1-203">String</span></span> | <span data-ttu-id="3ced1-204">Hello AS2 메시지를 보내는 파트너 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3ced1-204">Partner name who sends hello AS2 message.</span></span> <span data-ttu-id="3ced1-205">(필수)</span><span class="sxs-lookup"><span data-stu-id="3ced1-205">(Mandatory)</span></span> |
| <span data-ttu-id="3ced1-206">agreementName</span><span class="sxs-lookup"><span data-stu-id="3ced1-206">agreementName</span></span> | <span data-ttu-id="3ced1-207">문자열</span><span class="sxs-lookup"><span data-stu-id="3ced1-207">String</span></span> | <span data-ttu-id="3ced1-208">Hello AS2 계약 toowhich hello 메시지의 이름 확인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3ced1-208">Name of hello AS2 agreement toowhich hello messages are resolved.</span></span> <span data-ttu-id="3ced1-209">(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="3ced1-209">(Optional)</span></span> |
| <span data-ttu-id="3ced1-210">direction</span><span class="sxs-lookup"><span data-stu-id="3ced1-210">direction</span></span> |<span data-ttu-id="3ced1-211">문자열</span><span class="sxs-lookup"><span data-stu-id="3ced1-211">String</span></span> | <span data-ttu-id="3ced1-212">Hello 메시지 흐름의 방향을 수신 또는 송신 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ced1-212">Direction of hello message flow, receive or send.</span></span> <span data-ttu-id="3ced1-213">(필수)</span><span class="sxs-lookup"><span data-stu-id="3ced1-213">(Mandatory)</span></span> |
| <span data-ttu-id="3ced1-214">messageId</span><span class="sxs-lookup"><span data-stu-id="3ced1-214">messageId</span></span> | <span data-ttu-id="3ced1-215">string</span><span class="sxs-lookup"><span data-stu-id="3ced1-215">String</span></span> | <span data-ttu-id="3ced1-216">AS2 메시지 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="3ced1-216">AS2 message ID.</span></span> <span data-ttu-id="3ced1-217">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="3ced1-217">(Optional)</span></span> |
| <span data-ttu-id="3ced1-218">OriginalMessageId</span><span class="sxs-lookup"><span data-stu-id="3ced1-218">originalMessageId</span></span> |<span data-ttu-id="3ced1-219">문자열</span><span class="sxs-lookup"><span data-stu-id="3ced1-219">String</span></span> | <span data-ttu-id="3ced1-220">AS2 원래 메시지 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="3ced1-220">AS2 original message ID.</span></span> <span data-ttu-id="3ced1-221">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="3ced1-221">(Optional)</span></span> |
| <span data-ttu-id="3ced1-222">dispositionType</span><span class="sxs-lookup"><span data-stu-id="3ced1-222">dispositionType</span></span> | <span data-ttu-id="3ced1-223">문자열</span><span class="sxs-lookup"><span data-stu-id="3ced1-223">String</span></span> | <span data-ttu-id="3ced1-224">MDN 처리 유형 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3ced1-224">MDN disposition type value.</span></span> <span data-ttu-id="3ced1-225">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="3ced1-225">(Optional)</span></span> |
| <span data-ttu-id="3ced1-226">isMessageFailed</span><span class="sxs-lookup"><span data-stu-id="3ced1-226">isMessageFailed</span></span> |<span data-ttu-id="3ced1-227">Boolean</span><span class="sxs-lookup"><span data-stu-id="3ced1-227">Boolean</span></span> | <span data-ttu-id="3ced1-228">여부 hello AS2 메시지가 실패 했습니다.</span><span class="sxs-lookup"><span data-stu-id="3ced1-228">Whether hello AS2 message failed.</span></span> <span data-ttu-id="3ced1-229">(필수)</span><span class="sxs-lookup"><span data-stu-id="3ced1-229">(Mandatory)</span></span> |
| <span data-ttu-id="3ced1-230">isMessageSigned</span><span class="sxs-lookup"><span data-stu-id="3ced1-230">isMessageSigned</span></span> |<span data-ttu-id="3ced1-231">Boolean</span><span class="sxs-lookup"><span data-stu-id="3ced1-231">Boolean</span></span> | <span data-ttu-id="3ced1-232">Hello AS2 메시지가 서명 되었는지 여부를</span><span class="sxs-lookup"><span data-stu-id="3ced1-232">Whether hello AS2 message was signed.</span></span> <span data-ttu-id="3ced1-233">(필수)</span><span class="sxs-lookup"><span data-stu-id="3ced1-233">(Mandatory)</span></span> |
| <span data-ttu-id="3ced1-234">isNrrEnabled</span><span class="sxs-lookup"><span data-stu-id="3ced1-234">isNrrEnabled</span></span> | <span data-ttu-id="3ced1-235">Boolean</span><span class="sxs-lookup"><span data-stu-id="3ced1-235">Boolean</span></span> | <span data-ttu-id="3ced1-236">Hello 값은 알 수 없는 경우 기본값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ced1-236">Use default value if hello value is not known.</span></span> <span data-ttu-id="3ced1-237">(필수)</span><span class="sxs-lookup"><span data-stu-id="3ced1-237">(Mandatory)</span></span> |
| <span data-ttu-id="3ced1-238">statusCode</span><span class="sxs-lookup"><span data-stu-id="3ced1-238">statusCode</span></span> | <span data-ttu-id="3ced1-239">열거형</span><span class="sxs-lookup"><span data-stu-id="3ced1-239">Enum</span></span> | <span data-ttu-id="3ced1-240">허용되는 값은 **Accepted**, **Rejected** 또는 **AcceptedWithErrors**입니다.</span><span class="sxs-lookup"><span data-stu-id="3ced1-240">Allowed values are **Accepted**, **Rejected**, and **AcceptedWithErrors**.</span></span> <span data-ttu-id="3ced1-241">필수 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="3ced1-241">(Mandatory)</span></span> |
| <span data-ttu-id="3ced1-242">micVerificationStatus</span><span class="sxs-lookup"><span data-stu-id="3ced1-242">micVerificationStatus</span></span> | <span data-ttu-id="3ced1-243">열거형</span><span class="sxs-lookup"><span data-stu-id="3ced1-243">Enum</span></span> | <span data-ttu-id="3ced1-244">허용되는 값은 **NotApplicable**, **Succeeded** 또는 **Failed**입니다.</span><span class="sxs-lookup"><span data-stu-id="3ced1-244">Allowed values are **NotApplicable**, **Succeeded**, and **Failed**.</span></span> <span data-ttu-id="3ced1-245">필수 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="3ced1-245">(Mandatory)</span></span> |
| <span data-ttu-id="3ced1-246">correlationMessageId</span><span class="sxs-lookup"><span data-stu-id="3ced1-246">correlationMessageId</span></span> | <span data-ttu-id="3ced1-247">string</span><span class="sxs-lookup"><span data-stu-id="3ced1-247">String</span></span> | <span data-ttu-id="3ced1-248">상관 관계 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="3ced1-248">Correlation ID.</span></span> <span data-ttu-id="3ced1-249">원래 hello 메시지 ID (MDN이 구성 하는 hello 메시지의 메시지 ID hello).</span><span class="sxs-lookup"><span data-stu-id="3ced1-249">hello original messaged ID (hello message ID of hello message for which MDN is configured).</span></span> <span data-ttu-id="3ced1-250">(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="3ced1-250">(Optional)</span></span> |
| <span data-ttu-id="3ced1-251">incomingHeaders</span><span class="sxs-lookup"><span data-stu-id="3ced1-251">incomingHeaders</span></span> | <span data-ttu-id="3ced1-252">JToken의 사전</span><span class="sxs-lookup"><span data-stu-id="3ced1-252">Dictionary of JToken</span></span> | <span data-ttu-id="3ced1-253">들어오는 메시지 헤더 세부 정보를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="3ced1-253">Indicates incoming message header details.</span></span> <span data-ttu-id="3ced1-254">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="3ced1-254">(Optional)</span></span> |
| <span data-ttu-id="3ced1-255">outgoingHeaders</span><span class="sxs-lookup"><span data-stu-id="3ced1-255">outgoingHeaders</span></span> |<span data-ttu-id="3ced1-256">JToken의 사전</span><span class="sxs-lookup"><span data-stu-id="3ced1-256">Dictionary of JToken</span></span> | <span data-ttu-id="3ced1-257">보내는 메시지 헤더 세부 정보를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="3ced1-257">Indicates outgoing message header details.</span></span> <span data-ttu-id="3ced1-258">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="3ced1-258">(Optional)</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3ced1-259">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3ced1-259">Next steps</span></span>
* <span data-ttu-id="3ced1-260">Hello에 대 한 자세한 [엔터프라이즈 통합 팩](../logic-apps/logic-apps-enterprise-integration-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3ced1-260">Learn more about hello [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).</span></span>    
* <span data-ttu-id="3ced1-261">[B2B 메시지 모니터링](logic-apps-monitor-b2b-message.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="3ced1-261">Learn more about [monitoring B2B messages](logic-apps-monitor-b2b-message.md).</span></span>   
* <span data-ttu-id="3ced1-262">[B2B 사용자 지정 추적 스키마](logic-apps-track-integration-account-custom-tracking-schema.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="3ced1-262">Learn more about [B2B custom tracking schemas](logic-apps-track-integration-account-custom-tracking-schema.md).</span></span>   
* <span data-ttu-id="3ced1-263">[X12 추적 스키마](logic-apps-track-integration-account-x12-tracking-schema.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="3ced1-263">Learn more about [X12 tracking schemas](logic-apps-track-integration-account-x12-tracking-schema.md).</span></span>   
* <span data-ttu-id="3ced1-264">에 대 한 자세한 내용은 [hello Operations Management Suite 포털에서 B2B 메시지를 추적](../logic-apps/logic-apps-track-b2b-messages-omsportal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3ced1-264">Learn about [tracking B2B messages in hello Operations Management Suite portal](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>

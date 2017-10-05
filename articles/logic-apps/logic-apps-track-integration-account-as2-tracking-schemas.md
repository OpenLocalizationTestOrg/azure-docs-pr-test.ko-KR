---
title: "B2B 모니터링을 위한 AS2 추적 스키마 - Azure Logic Apps | Microsoft Docs"
description: "AS2 추적 스키마를 사용하여 Azure 통합 계정의 트랜잭션에서 B2B 메시지를 모니터링합니다."
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
ms.openlocfilehash: 31bd296dc5ed5ac6998a6c05ee80fd38b12d662c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="start-or-enable-tracking-of-as2-messages-and-mdns-to-monitor-success-errors-and-message-properties"></a><span data-ttu-id="1e593-103">AS2 메시지 및 MDN의 추적을 시작 또는 사용하여 성공, 오류 및 메시지 속성을 모니터링</span><span class="sxs-lookup"><span data-stu-id="1e593-103">Start or enable tracking of AS2 messages and MDNs to monitor success, errors, and message properties</span></span>
<span data-ttu-id="1e593-104">Azure 통합 계정에서 다음 AS2 추적 스키마를 사용하여 B2B(business-to-business) 트랜잭션을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-104">You can use these AS2 tracking schemas in your Azure integration account to help you monitor business-to-business (B2B) transactions:</span></span>

* <span data-ttu-id="1e593-105">AS2 메시지 추적 스키마</span><span class="sxs-lookup"><span data-stu-id="1e593-105">AS2 message tracking schema</span></span>
* <span data-ttu-id="1e593-106">AS2 MDN 추적 스키마</span><span class="sxs-lookup"><span data-stu-id="1e593-106">AS2 MDN tracking schema</span></span>

## <a name="as2-message-tracking-schema"></a><span data-ttu-id="1e593-107">AS2 메시지 추적 스키마</span><span class="sxs-lookup"><span data-stu-id="1e593-107">AS2 message tracking schema</span></span>
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

| <span data-ttu-id="1e593-108">속성</span><span class="sxs-lookup"><span data-stu-id="1e593-108">Property</span></span> | <span data-ttu-id="1e593-109">형식</span><span class="sxs-lookup"><span data-stu-id="1e593-109">Type</span></span> | <span data-ttu-id="1e593-110">설명</span><span class="sxs-lookup"><span data-stu-id="1e593-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1e593-111">senderPartnerName</span><span class="sxs-lookup"><span data-stu-id="1e593-111">senderPartnerName</span></span> | <span data-ttu-id="1e593-112">string</span><span class="sxs-lookup"><span data-stu-id="1e593-112">String</span></span> | <span data-ttu-id="1e593-113">AS2 메시지 보낸 사람의 파트너 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-113">AS2 message sender's partner name.</span></span> <span data-ttu-id="1e593-114">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-114">(Optional)</span></span> |
| <span data-ttu-id="1e593-115">receiverPartnerName</span><span class="sxs-lookup"><span data-stu-id="1e593-115">receiverPartnerName</span></span> | <span data-ttu-id="1e593-116">string</span><span class="sxs-lookup"><span data-stu-id="1e593-116">String</span></span> | <span data-ttu-id="1e593-117">AS2 메시지 받는 사람의 파트너 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-117">AS2 message receiver's partner name.</span></span> <span data-ttu-id="1e593-118">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-118">(Optional)</span></span> |
| <span data-ttu-id="1e593-119">as2To</span><span class="sxs-lookup"><span data-stu-id="1e593-119">as2To</span></span> | <span data-ttu-id="1e593-120">string</span><span class="sxs-lookup"><span data-stu-id="1e593-120">String</span></span> | <span data-ttu-id="1e593-121">AS2 메시지의 헤더에서 AS2 메시지 받는 사람의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-121">AS2 message receiver’s name, from the headers of the AS2 message.</span></span> <span data-ttu-id="1e593-122">필수 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-122">(Mandatory)</span></span> |
| <span data-ttu-id="1e593-123">as2From</span><span class="sxs-lookup"><span data-stu-id="1e593-123">as2From</span></span> | <span data-ttu-id="1e593-124">문자열</span><span class="sxs-lookup"><span data-stu-id="1e593-124">String</span></span> | <span data-ttu-id="1e593-125">AS2 메시지의 헤더에서 AS2 메시지 보낸 사람의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-125">AS2 message sender’s name, from the headers of the AS2 message.</span></span> <span data-ttu-id="1e593-126">필수 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-126">(Mandatory)</span></span> |
| <span data-ttu-id="1e593-127">agreementName</span><span class="sxs-lookup"><span data-stu-id="1e593-127">agreementName</span></span> | <span data-ttu-id="1e593-128">문자열</span><span class="sxs-lookup"><span data-stu-id="1e593-128">String</span></span> | <span data-ttu-id="1e593-129">메시지가 확인되는 AS2 규약의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-129">Name of the AS2 agreement to which the messages are resolved.</span></span> <span data-ttu-id="1e593-130">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-130">(Optional)</span></span> |
| <span data-ttu-id="1e593-131">direction</span><span class="sxs-lookup"><span data-stu-id="1e593-131">direction</span></span> | <span data-ttu-id="1e593-132">string</span><span class="sxs-lookup"><span data-stu-id="1e593-132">String</span></span> | <span data-ttu-id="1e593-133">메시지 흐름, 수신 또는 송신 방향입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-133">Direction of the message flow, receive or send.</span></span> <span data-ttu-id="1e593-134">필수 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-134">(Mandatory)</span></span> |
| <span data-ttu-id="1e593-135">messageId</span><span class="sxs-lookup"><span data-stu-id="1e593-135">messageId</span></span> | <span data-ttu-id="1e593-136">string</span><span class="sxs-lookup"><span data-stu-id="1e593-136">String</span></span> | <span data-ttu-id="1e593-137">AS2 메시지의 헤더에서 AS2 메시지 ID입니다. 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-137">AS2 message ID, from the headers of the AS2 message (Optional)</span></span> |
| <span data-ttu-id="1e593-138">dispositionType</span><span class="sxs-lookup"><span data-stu-id="1e593-138">dispositionType</span></span> |<span data-ttu-id="1e593-139">문자열</span><span class="sxs-lookup"><span data-stu-id="1e593-139">String</span></span> | <span data-ttu-id="1e593-140">MDN(메시지 처리 알림) 처리 유형 값입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-140">Message Disposition Notification (MDN) disposition type value.</span></span> <span data-ttu-id="1e593-141">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-141">(Optional)</span></span> |
| <span data-ttu-id="1e593-142">fileName</span><span class="sxs-lookup"><span data-stu-id="1e593-142">fileName</span></span> | <span data-ttu-id="1e593-143">문자열</span><span class="sxs-lookup"><span data-stu-id="1e593-143">String</span></span> | <span data-ttu-id="1e593-144">AS2 메시지의 헤더에서 파일 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-144">File name, from the header of the AS2 message.</span></span> <span data-ttu-id="1e593-145">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-145">(Optional)</span></span> |
| <span data-ttu-id="1e593-146">isMessageFailed</span><span class="sxs-lookup"><span data-stu-id="1e593-146">isMessageFailed</span></span> |<span data-ttu-id="1e593-147">Boolean</span><span class="sxs-lookup"><span data-stu-id="1e593-147">Boolean</span></span> | <span data-ttu-id="1e593-148">AS2 메시지의 실패 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-148">Whether the AS2 message failed.</span></span> <span data-ttu-id="1e593-149">필수 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-149">(Mandatory)</span></span> |
| <span data-ttu-id="1e593-150">isMessageSigned</span><span class="sxs-lookup"><span data-stu-id="1e593-150">isMessageSigned</span></span> | <span data-ttu-id="1e593-151">Boolean</span><span class="sxs-lookup"><span data-stu-id="1e593-151">Boolean</span></span> | <span data-ttu-id="1e593-152">AS2 메시지의 서명 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-152">Whether the AS2 message was signed.</span></span> <span data-ttu-id="1e593-153">필수 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-153">(Mandatory)</span></span> |
| <span data-ttu-id="1e593-154">isMessageEncrypted</span><span class="sxs-lookup"><span data-stu-id="1e593-154">isMessageEncrypted</span></span> | <span data-ttu-id="1e593-155">Boolean</span><span class="sxs-lookup"><span data-stu-id="1e593-155">Boolean</span></span> | <span data-ttu-id="1e593-156">AS2 메시지의 암호화 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-156">Whether the AS2 message was encrypted.</span></span> <span data-ttu-id="1e593-157">필수 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-157">(Mandatory)</span></span> |
| <span data-ttu-id="1e593-158">isMessageCompressed</span><span class="sxs-lookup"><span data-stu-id="1e593-158">isMessageCompressed</span></span> |<span data-ttu-id="1e593-159">Boolean</span><span class="sxs-lookup"><span data-stu-id="1e593-159">Boolean</span></span> | <span data-ttu-id="1e593-160">AS2 메시지의 압축 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-160">Whether the AS2 message was compressed.</span></span> <span data-ttu-id="1e593-161">필수 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-161">(Mandatory)</span></span> |
| <span data-ttu-id="1e593-162">correlationMessageId</span><span class="sxs-lookup"><span data-stu-id="1e593-162">correlationMessageId</span></span> | <span data-ttu-id="1e593-163">문자열</span><span class="sxs-lookup"><span data-stu-id="1e593-163">String</span></span> | <span data-ttu-id="1e593-164">MDN과 메시지를 상호 연관 짓기 위한 AS2 메시지 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-164">AS2 message ID, to correlate messages with MDNs.</span></span> <span data-ttu-id="1e593-165">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-165">(Optional)</span></span> |
| <span data-ttu-id="1e593-166">incomingHeaders</span><span class="sxs-lookup"><span data-stu-id="1e593-166">incomingHeaders</span></span> |<span data-ttu-id="1e593-167">JToken의 사전</span><span class="sxs-lookup"><span data-stu-id="1e593-167">Dictionary of JToken</span></span> | <span data-ttu-id="1e593-168">들어오는 AS2 메시지 헤더 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-168">Incoming AS2 message header details.</span></span> <span data-ttu-id="1e593-169">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-169">(Optional)</span></span> |
| <span data-ttu-id="1e593-170">outgoingHeaders</span><span class="sxs-lookup"><span data-stu-id="1e593-170">outgoingHeaders</span></span> |<span data-ttu-id="1e593-171">JToken의 사전</span><span class="sxs-lookup"><span data-stu-id="1e593-171">Dictionary of JToken</span></span> | <span data-ttu-id="1e593-172">보내는 AS2 메시지 헤더 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-172">Outgoing AS2 message header details.</span></span> <span data-ttu-id="1e593-173">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-173">(Optional)</span></span> |
| <span data-ttu-id="1e593-174">isNrrEnabled</span><span class="sxs-lookup"><span data-stu-id="1e593-174">isNrrEnabled</span></span> | <span data-ttu-id="1e593-175">Boolean</span><span class="sxs-lookup"><span data-stu-id="1e593-175">Boolean</span></span> | <span data-ttu-id="1e593-176">값을 알 수 없는 경우 기본값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-176">Use default value if the value is not known.</span></span> <span data-ttu-id="1e593-177">필수 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-177">(Mandatory)</span></span> |
| <span data-ttu-id="1e593-178">isMdnExpected</span><span class="sxs-lookup"><span data-stu-id="1e593-178">isMdnExpected</span></span> | <span data-ttu-id="1e593-179">Boolean</span><span class="sxs-lookup"><span data-stu-id="1e593-179">Boolean</span></span> | <span data-ttu-id="1e593-180">값을 알 수 없는 경우 기본값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-180">Use default value if the value is not known.</span></span> <span data-ttu-id="1e593-181">필수 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-181">(Mandatory)</span></span> |
| <span data-ttu-id="1e593-182">mdnType</span><span class="sxs-lookup"><span data-stu-id="1e593-182">mdnType</span></span> | <span data-ttu-id="1e593-183">열거형</span><span class="sxs-lookup"><span data-stu-id="1e593-183">Enum</span></span> | <span data-ttu-id="1e593-184">허용되는 값은 **NotConfigured**, **Sync** 또는 **Async**입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-184">Allowed values are **NotConfigured**, **Sync**, and **Async**.</span></span> <span data-ttu-id="1e593-185">필수 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-185">(Mandatory)</span></span> |

## <a name="as2-mdn-tracking-schema"></a><span data-ttu-id="1e593-186">AS2 MDN 추적 스키마</span><span class="sxs-lookup"><span data-stu-id="1e593-186">AS2 MDN tracking schema</span></span>
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

| <span data-ttu-id="1e593-187">속성</span><span class="sxs-lookup"><span data-stu-id="1e593-187">Property</span></span> | <span data-ttu-id="1e593-188">형식</span><span class="sxs-lookup"><span data-stu-id="1e593-188">Type</span></span> | <span data-ttu-id="1e593-189">설명</span><span class="sxs-lookup"><span data-stu-id="1e593-189">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1e593-190">senderPartnerName</span><span class="sxs-lookup"><span data-stu-id="1e593-190">senderPartnerName</span></span> | <span data-ttu-id="1e593-191">string</span><span class="sxs-lookup"><span data-stu-id="1e593-191">String</span></span> | <span data-ttu-id="1e593-192">AS2 메시지 보낸 사람의 파트너 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-192">AS2 message sender's partner name.</span></span> <span data-ttu-id="1e593-193">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-193">(Optional)</span></span> |
| <span data-ttu-id="1e593-194">receiverPartnerName</span><span class="sxs-lookup"><span data-stu-id="1e593-194">receiverPartnerName</span></span> | <span data-ttu-id="1e593-195">string</span><span class="sxs-lookup"><span data-stu-id="1e593-195">String</span></span> | <span data-ttu-id="1e593-196">AS2 메시지 받는 사람의 파트너 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-196">AS2 message receiver's partner name.</span></span> <span data-ttu-id="1e593-197">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-197">(Optional)</span></span> |
| <span data-ttu-id="1e593-198">as2To</span><span class="sxs-lookup"><span data-stu-id="1e593-198">as2To</span></span> | <span data-ttu-id="1e593-199">string</span><span class="sxs-lookup"><span data-stu-id="1e593-199">String</span></span> | <span data-ttu-id="1e593-200">AS2 메시지를 받는 파트너 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-200">Partner name who receives the AS2 message.</span></span> <span data-ttu-id="1e593-201">필수 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-201">(Mandatory)</span></span> |
| <span data-ttu-id="1e593-202">as2From</span><span class="sxs-lookup"><span data-stu-id="1e593-202">as2From</span></span> | <span data-ttu-id="1e593-203">문자열</span><span class="sxs-lookup"><span data-stu-id="1e593-203">String</span></span> | <span data-ttu-id="1e593-204">AS2 메시지를 보내는 파트너 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-204">Partner name who sends the AS2 message.</span></span> <span data-ttu-id="1e593-205">필수 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-205">(Mandatory)</span></span> |
| <span data-ttu-id="1e593-206">agreementName</span><span class="sxs-lookup"><span data-stu-id="1e593-206">agreementName</span></span> | <span data-ttu-id="1e593-207">문자열</span><span class="sxs-lookup"><span data-stu-id="1e593-207">String</span></span> | <span data-ttu-id="1e593-208">메시지가 확인되는 AS2 규약의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-208">Name of the AS2 agreement to which the messages are resolved.</span></span> <span data-ttu-id="1e593-209">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-209">(Optional)</span></span> |
| <span data-ttu-id="1e593-210">direction</span><span class="sxs-lookup"><span data-stu-id="1e593-210">direction</span></span> |<span data-ttu-id="1e593-211">string</span><span class="sxs-lookup"><span data-stu-id="1e593-211">String</span></span> | <span data-ttu-id="1e593-212">메시지 흐름, 수신 또는 송신 방향입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-212">Direction of the message flow, receive or send.</span></span> <span data-ttu-id="1e593-213">필수 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-213">(Mandatory)</span></span> |
| <span data-ttu-id="1e593-214">messageId</span><span class="sxs-lookup"><span data-stu-id="1e593-214">messageId</span></span> | <span data-ttu-id="1e593-215">string</span><span class="sxs-lookup"><span data-stu-id="1e593-215">String</span></span> | <span data-ttu-id="1e593-216">AS2 메시지 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-216">AS2 message ID.</span></span> <span data-ttu-id="1e593-217">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-217">(Optional)</span></span> |
| <span data-ttu-id="1e593-218">OriginalMessageId</span><span class="sxs-lookup"><span data-stu-id="1e593-218">originalMessageId</span></span> |<span data-ttu-id="1e593-219">문자열</span><span class="sxs-lookup"><span data-stu-id="1e593-219">String</span></span> | <span data-ttu-id="1e593-220">AS2 원래 메시지 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-220">AS2 original message ID.</span></span> <span data-ttu-id="1e593-221">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-221">(Optional)</span></span> |
| <span data-ttu-id="1e593-222">dispositionType</span><span class="sxs-lookup"><span data-stu-id="1e593-222">dispositionType</span></span> | <span data-ttu-id="1e593-223">문자열</span><span class="sxs-lookup"><span data-stu-id="1e593-223">String</span></span> | <span data-ttu-id="1e593-224">MDN 처리 유형 값입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-224">MDN disposition type value.</span></span> <span data-ttu-id="1e593-225">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-225">(Optional)</span></span> |
| <span data-ttu-id="1e593-226">isMessageFailed</span><span class="sxs-lookup"><span data-stu-id="1e593-226">isMessageFailed</span></span> |<span data-ttu-id="1e593-227">Boolean</span><span class="sxs-lookup"><span data-stu-id="1e593-227">Boolean</span></span> | <span data-ttu-id="1e593-228">AS2 메시지의 실패 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-228">Whether the AS2 message failed.</span></span> <span data-ttu-id="1e593-229">필수 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-229">(Mandatory)</span></span> |
| <span data-ttu-id="1e593-230">isMessageSigned</span><span class="sxs-lookup"><span data-stu-id="1e593-230">isMessageSigned</span></span> |<span data-ttu-id="1e593-231">Boolean</span><span class="sxs-lookup"><span data-stu-id="1e593-231">Boolean</span></span> | <span data-ttu-id="1e593-232">AS2 메시지의 서명 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-232">Whether the AS2 message was signed.</span></span> <span data-ttu-id="1e593-233">필수 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-233">(Mandatory)</span></span> |
| <span data-ttu-id="1e593-234">isNrrEnabled</span><span class="sxs-lookup"><span data-stu-id="1e593-234">isNrrEnabled</span></span> | <span data-ttu-id="1e593-235">Boolean</span><span class="sxs-lookup"><span data-stu-id="1e593-235">Boolean</span></span> | <span data-ttu-id="1e593-236">값을 알 수 없는 경우 기본값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-236">Use default value if the value is not known.</span></span> <span data-ttu-id="1e593-237">필수 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-237">(Mandatory)</span></span> |
| <span data-ttu-id="1e593-238">statusCode</span><span class="sxs-lookup"><span data-stu-id="1e593-238">statusCode</span></span> | <span data-ttu-id="1e593-239">열거형</span><span class="sxs-lookup"><span data-stu-id="1e593-239">Enum</span></span> | <span data-ttu-id="1e593-240">허용되는 값은 **Accepted**, **Rejected** 또는 **AcceptedWithErrors**입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-240">Allowed values are **Accepted**, **Rejected**, and **AcceptedWithErrors**.</span></span> <span data-ttu-id="1e593-241">필수 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-241">(Mandatory)</span></span> |
| <span data-ttu-id="1e593-242">micVerificationStatus</span><span class="sxs-lookup"><span data-stu-id="1e593-242">micVerificationStatus</span></span> | <span data-ttu-id="1e593-243">열거형</span><span class="sxs-lookup"><span data-stu-id="1e593-243">Enum</span></span> | <span data-ttu-id="1e593-244">허용되는 값은 **NotApplicable**, **Succeeded** 또는 **Failed**입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-244">Allowed values are **NotApplicable**, **Succeeded**, and **Failed**.</span></span> <span data-ttu-id="1e593-245">필수 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-245">(Mandatory)</span></span> |
| <span data-ttu-id="1e593-246">correlationMessageId</span><span class="sxs-lookup"><span data-stu-id="1e593-246">correlationMessageId</span></span> | <span data-ttu-id="1e593-247">string</span><span class="sxs-lookup"><span data-stu-id="1e593-247">String</span></span> | <span data-ttu-id="1e593-248">상관 관계 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-248">Correlation ID.</span></span> <span data-ttu-id="1e593-249">원래 메시지 ID(MDN이 구성된 메시지의 메시지 ID)입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-249">The original messaged ID (the message ID of the message for which MDN is configured).</span></span> <span data-ttu-id="1e593-250">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-250">(Optional)</span></span> |
| <span data-ttu-id="1e593-251">incomingHeaders</span><span class="sxs-lookup"><span data-stu-id="1e593-251">incomingHeaders</span></span> | <span data-ttu-id="1e593-252">JToken의 사전</span><span class="sxs-lookup"><span data-stu-id="1e593-252">Dictionary of JToken</span></span> | <span data-ttu-id="1e593-253">들어오는 메시지 헤더 세부 정보를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-253">Indicates incoming message header details.</span></span> <span data-ttu-id="1e593-254">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-254">(Optional)</span></span> |
| <span data-ttu-id="1e593-255">outgoingHeaders</span><span class="sxs-lookup"><span data-stu-id="1e593-255">outgoingHeaders</span></span> |<span data-ttu-id="1e593-256">JToken의 사전</span><span class="sxs-lookup"><span data-stu-id="1e593-256">Dictionary of JToken</span></span> | <span data-ttu-id="1e593-257">보내는 메시지 헤더 세부 정보를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-257">Indicates outgoing message header details.</span></span> <span data-ttu-id="1e593-258">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-258">(Optional)</span></span> |

## <a name="next-steps"></a><span data-ttu-id="1e593-259">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1e593-259">Next steps</span></span>
* <span data-ttu-id="1e593-260">[엔터프라이즈 통합 팩](../logic-apps/logic-apps-enterprise-integration-overview.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-260">Learn more about the [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).</span></span>    
* <span data-ttu-id="1e593-261">[B2B 메시지 모니터링](logic-apps-monitor-b2b-message.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-261">Learn more about [monitoring B2B messages](logic-apps-monitor-b2b-message.md).</span></span>   
* <span data-ttu-id="1e593-262">[B2B 사용자 지정 추적 스키마](logic-apps-track-integration-account-custom-tracking-schema.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-262">Learn more about [B2B custom tracking schemas](logic-apps-track-integration-account-custom-tracking-schema.md).</span></span>   
* <span data-ttu-id="1e593-263">[X12 추적 스키마](logic-apps-track-integration-account-x12-tracking-schema.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-263">Learn more about [X12 tracking schemas](logic-apps-track-integration-account-x12-tracking-schema.md).</span></span>   
* <span data-ttu-id="1e593-264">[Operations Management Suite 포털에서 B2B 메시지 추적](../logic-apps/logic-apps-track-b2b-messages-omsportal.md)에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1e593-264">Learn about [tracking B2B messages in the Operations Management Suite portal](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>

---
title: "Logic Apps B2B 오류 및 해결 방법 목록: Azure App Service | Microsoft Docs"
description: "Logic Apps B2B 오류 및 해결 방법 목록"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: cf44af18-1fe5-41d5-9e06-cc57a968207c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 1865d75f1b4c2aa18d5a3130f639572d19563b3e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="logic-apps-b2b-list-of-errors-and-solutions"></a><span data-ttu-id="698c1-103">Logic Apps B2B 오류 및 해결 방법 목록</span><span class="sxs-lookup"><span data-stu-id="698c1-103">Logic Apps B2B list of errors and solutions</span></span>  
<span data-ttu-id="698c1-104">이 문서에서는 Logic Apps B2B 시나리오에서 발생할 수 있는 오류를 해결하고 이러한 오류를 수정하기 위한 적절한 조치를 제안합니다.</span><span class="sxs-lookup"><span data-stu-id="698c1-104">This article helps you troubleshoot errors that might happen in Logic Apps B2B scenarios and suggests appropriate actions for correcting those errors.</span></span>


## <a name="agreement-resolution"></a><span data-ttu-id="698c1-105">규약 확인</span><span class="sxs-lookup"><span data-stu-id="698c1-105">Agreement Resolution</span></span>

### <a name="no-agreement-found"></a><span data-ttu-id="698c1-106">* 규약을 찾을 수 없음</span><span class="sxs-lookup"><span data-stu-id="698c1-106">*No agreement found</span></span> 

|   |   |  
|---|---|
| <span data-ttu-id="698c1-107">오류 설명</span><span class="sxs-lookup"><span data-stu-id="698c1-107">Error description</span></span> | <span data-ttu-id="698c1-108">규약 확인 매개 변수가 있는 규약을 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="698c1-108">No agreement found with Agreement Resolution Parameters</span></span>|    
| <span data-ttu-id="698c1-109">사용자 조치</span><span class="sxs-lookup"><span data-stu-id="698c1-109">User action</span></span> | <span data-ttu-id="698c1-110">동의한 비즈니스 ID로 통합 계정에 규약을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="698c1-110">The agreement should be added to the integration account with agreed business identities.</span></span></br> <span data-ttu-id="698c1-111">비즈니스 ID는 입력 메시지 ID와 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="698c1-111">The business identities should match to the input message ids</span></span>|  
|   |   |

### <a name="-no-agreement-found-with-identities"></a><span data-ttu-id="698c1-112">* ID가 있는 규약을 찾을 수 없음</span><span class="sxs-lookup"><span data-stu-id="698c1-112">* No agreement found with identities</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="698c1-113">오류 설명</span><span class="sxs-lookup"><span data-stu-id="698c1-113">Error description</span></span> | <span data-ttu-id="698c1-114">ID가 'AS2Identity'::'Partner1' 및 'AS2Identity'::'Partner3'인 규약을 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="698c1-114">No agreement found with identities: 'AS2Identity'::'Partner1' and'AS2Identity'::'Partner3'</span></span>| 
| <span data-ttu-id="698c1-115">사용자 조치</span><span class="sxs-lookup"><span data-stu-id="698c1-115">User action</span></span> | <span data-ttu-id="698c1-116">규약에 대해 구성된 AS2-From 또는 AS2-To가 잘못되었습니다.</span><span class="sxs-lookup"><span data-stu-id="698c1-116">Invalid AS2-From or AS2-To configured for agreement.</span></span> </br> <span data-ttu-id="698c1-117">AS2 메시지 헤더의 AS2 ID가 규약 구성과 일치하도록 AS2 메시지 AS2-From/AS2-To 헤더 또는 규약을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="698c1-117">Correct AS2 message AS2-From or AS2-To headers or agreement to match AS2 ids in AS2 message headers with agreement configurations</span></span> |
|   |   |     

## <a name="as2"></a><span data-ttu-id="698c1-118">AS2</span><span class="sxs-lookup"><span data-stu-id="698c1-118">AS2</span></span>

### <a name="-missing-as2-message-headers"></a><span data-ttu-id="698c1-119">* 누락된 AS2 메시지 헤더</span><span class="sxs-lookup"><span data-stu-id="698c1-119">* Missing AS2 message headers</span></span>  

|   |   |  
|---|---|
| <span data-ttu-id="698c1-120">오류 설명</span><span class="sxs-lookup"><span data-stu-id="698c1-120">Error description</span></span>| <span data-ttu-id="698c1-121">AS2 헤더가 잘못되었습니다.</span><span class="sxs-lookup"><span data-stu-id="698c1-121">Invalid AS2 headers.</span></span> <span data-ttu-id="698c1-122">'AS2-To' 또는 'AS2-From' 헤더 중 하나가 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="698c1-122">One of 'AS2-To' or 'AS2-From' headers are empty</span></span>| 
| <span data-ttu-id="698c1-123">사용자 조치</span><span class="sxs-lookup"><span data-stu-id="698c1-123">User action</span></span> | <span data-ttu-id="698c1-124">AS2-From, AS2-To 또는 두 헤더가 포함되지 않은 AS2 메시지를 받았습니다.</span><span class="sxs-lookup"><span data-stu-id="698c1-124">An AS2 message was received that did not contain the AS2-From or AS2-To or both headers.</span></span> </br> <span data-ttu-id="698c1-125">AS2 메시지 AS2-From 및 AS2-To 헤더를 확인하고 규약 구성에 따라 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="698c1-125">Check AS2 message AS2-From and AS2-To headers and correct them based on agreement configuration</span></span> |
|  |  | 


### <a name="-missing-as2-message-body-and-headers"></a><span data-ttu-id="698c1-126">* 누락된 AS2 메시지 본문 및 헤더</span><span class="sxs-lookup"><span data-stu-id="698c1-126">* Missing AS2 message body and headers</span></span>    

|   |   |  
|---|---|
| <span data-ttu-id="698c1-127">오류 설명</span><span class="sxs-lookup"><span data-stu-id="698c1-127">Error description</span></span>| <span data-ttu-id="698c1-128">요청 콘텐츠가 null이거나 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="698c1-128">The request content is null or empty</span></span> | 
| <span data-ttu-id="698c1-129">사용자 조치</span><span class="sxs-lookup"><span data-stu-id="698c1-129">User action</span></span> | <span data-ttu-id="698c1-130">메시지 본문이 포함되지 않은 AS2 메시지를 받았습니다.</span><span class="sxs-lookup"><span data-stu-id="698c1-130">An AS2 message was received that did not contain the message body</span></span> |
|  |  | 

### <a name="-as2-message-decryption-failure"></a><span data-ttu-id="698c1-131">* AS2 메시지 암호 해독 실패</span><span class="sxs-lookup"><span data-stu-id="698c1-131">* AS2 message decryption failure</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="698c1-132">오류 설명</span><span class="sxs-lookup"><span data-stu-id="698c1-132">Error description</span></span> |  <span data-ttu-id="698c1-133">[처리됨/오류: 암호 해독 실패]</span><span class="sxs-lookup"><span data-stu-id="698c1-133">[processed/Error: decryption-failed]</span></span> | 
| <span data-ttu-id="698c1-134">사용자 조치</span><span class="sxs-lookup"><span data-stu-id="698c1-134">User action</span></span> | <span data-ttu-id="698c1-135">파트너에게 보내기 전에 AS2Message에 @base64ToBinary를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="698c1-135">Add @base64ToBinary to AS2Message before sending to partner</span></span> 
```java
            "HTTP": {
                "inputs": {
                    "body": "@base64ToBinary(body('Encode_to_AS2_message')?['AS2Message']?['Content'])",
                    "headers": "@body('Encode_to_AS2_message')?['AS2Message']?['OutboundHeaders']",
                    "method": "POST",
                    "uri": "xxxxx.xxx"
                },
                
``` 

### <a name="-mdn-decryption-failure"></a><span data-ttu-id="698c1-136">* MDN 암호 해독 실패</span><span class="sxs-lookup"><span data-stu-id="698c1-136">* MDN decryption failure</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="698c1-137">오류 설명</span><span class="sxs-lookup"><span data-stu-id="698c1-137">Error description</span></span> |  <span data-ttu-id="698c1-138">[처리됨/오류: 암호 해독 실패]</span><span class="sxs-lookup"><span data-stu-id="698c1-138">[processed/Error: decryption-failed]</span></span> | 
| <span data-ttu-id="698c1-139">사용자 조치</span><span class="sxs-lookup"><span data-stu-id="698c1-139">User action</span></span> | <span data-ttu-id="698c1-140">파트너에게 보내기 전에 MDN에 @base64ToBinary를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="698c1-140">Add @base64ToBinary to MDN before sending to partner</span></span> 
```java
            "Response": {
                "inputs": {
                    "body": "@base64ToBinary(body('Decode_AS2_message')?['OutgoingMDN']?['Content'])",
                    "headers": "@body('Decode_AS2_message')?['OutgoingMDN']?['OutboundHeaders']",
                    "statusCode": 200
                },
                
``` 

### <a name="-missing-signing-certificate"></a><span data-ttu-id="698c1-141">* 누락된 서명 인증서</span><span class="sxs-lookup"><span data-stu-id="698c1-141">* Missing signing certificate</span></span>

|   |   |  
|---|---|
| <span data-ttu-id="698c1-142">오류 설명</span><span class="sxs-lookup"><span data-stu-id="698c1-142">Error description</span></span>| <span data-ttu-id="698c1-143">AS2 파티에 대해 서명 인증서가 구성되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="698c1-143">The Signing Certificate has not been configured for AS2 party.</span></span> </br> <span data-ttu-id="698c1-144">AS2-From: partner1 AS2-To: partner2</span><span class="sxs-lookup"><span data-stu-id="698c1-144">AS2-From: partner1 AS2-To: partner2</span></span> | 
| <span data-ttu-id="698c1-145">사용자 조치</span><span class="sxs-lookup"><span data-stu-id="698c1-145">User action</span></span> | <span data-ttu-id="698c1-146">서명을 위한 올바른 인증서로 AS2 규약 설정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="698c1-146">Configure AS2 agreement settings with correct certificate for signature</span></span> |
|  |  | 

## <a name="x12-and-edifact"></a><span data-ttu-id="698c1-147">X12 및 EDIFACT</span><span class="sxs-lookup"><span data-stu-id="698c1-147">X12 and EDIFACT</span></span>

### <a name="-leading-or-trailing-space-found"></a><span data-ttu-id="698c1-148">* 선행 공백 또는 후행 공백이 있음</span><span class="sxs-lookup"><span data-stu-id="698c1-148">* Leading or trailing space found</span></span>    
    
|   |   | 
|---|---|
| <span data-ttu-id="698c1-149">오류 설명</span><span class="sxs-lookup"><span data-stu-id="698c1-149">Error description</span></span> | <span data-ttu-id="698c1-150">구문 분석 중에 오류가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="698c1-150">Error encountered during parsing.</span></span> <span data-ttu-id="698c1-151">ID가 '987654'이고, 보낸 사람 ID가 'Partner1'이고, 받는 사람 ID가 'Partner2'인 교환(그룹 없음)에 포함된 ID가 '123456'인 Edifact 트랜잭션 집합이 다음 오류로 인해 일시 중단됩니다. "선행 분리 기호 또는 후행 분리 기호가 있습니다."</span><span class="sxs-lookup"><span data-stu-id="698c1-151">The Edifact transaction set with id '123456' contained in interchange (without group) with id '987654', with sender id 'Partner1', receiver id 'Partner2' is being suspended with following errors: Leading Trailing separator found</span></span> |
| <span data-ttu-id="698c1-152">사용자 조치</span><span class="sxs-lookup"><span data-stu-id="698c1-152">User action</span></span> | <span data-ttu-id="698c1-153">선행 공백 및 후행 공백을 허용하도록 구성할 규약 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="698c1-153">The agreement settings to be configured to allow leading and trailing space.</span></span> </br> <span data-ttu-id="698c1-154">선행 공백 및 후행 공백을 허용하도록 규약 설정을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="698c1-154">Edit agreement settings to allow leading and trailing space</span></span> |
|   |   |

![공백 허용](./media/logic-apps-enterprise-integration-b2b-list-errors-solutions/leadingandtrailing.png)

### <a name="-duplicate-check-has-enabled-in-the-agreement"></a><span data-ttu-id="698c1-156">* 규약에서 중복 검사가 활성화됨</span><span class="sxs-lookup"><span data-stu-id="698c1-156">* Duplicate check has enabled in the agreement</span></span>

|   |   | 
|---|---| 
| <span data-ttu-id="698c1-157">오류 설명</span><span class="sxs-lookup"><span data-stu-id="698c1-157">Error description</span></span> | <span data-ttu-id="698c1-158">중복 컨트롤 번호가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="698c1-158">Duplicate Control Number</span></span> |
| <span data-ttu-id="698c1-159">사용자 조치</span><span class="sxs-lookup"><span data-stu-id="698c1-159">User action</span></span> | <span data-ttu-id="698c1-160">이 오류는 받은 메시지에 중복 컨트롤 번호가 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="698c1-160">This error indicates the received message has duplicate control numbers.</span></span> </br> <span data-ttu-id="698c1-161">컨트롤 번호를 수정하고 메시지를 다시 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="698c1-161">Correct the control number and resend the message</span></span> |
|   |   |

### <a name="-missing-schema-in-the-agreement"></a><span data-ttu-id="698c1-162">* 규약에서 누락된 스키마</span><span class="sxs-lookup"><span data-stu-id="698c1-162">* Missing schema in the agreement</span></span>

|   |   | 
|---|---| 
| <span data-ttu-id="698c1-163">오류 설명</span><span class="sxs-lookup"><span data-stu-id="698c1-163">Error description</span></span> | <span data-ttu-id="698c1-164">구문 분석 중에 오류가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="698c1-164">Error encountered during parsing.</span></span> <span data-ttu-id="698c1-165">ID가 '000056422'이고, 보낸 사람 ID가 '12345678       '이고, 받는 사람 ID가 '87654321       '인 교환에서 ID가 '56422'인 기능 그룹에 포함된 ID가 '564220001'인 X12 트랜잭션 집합이 다음 오류로 인해 일시 중단됩니다. "이 메시지의 문서 유형을 알 수 없으며 규약에 구성된 기존 스키마로 확인되지 않았습니다."</span><span class="sxs-lookup"><span data-stu-id="698c1-165">The X12 transaction set with id '564220001' contained in functional group with id '56422', in interchange with id '000056422', with sender id '12345678       ', receiver id '87654321       ' is being suspended with following errors "The message has an unknown document type and did not resolve to any of the existing schemas configured in the agreement"</span></span> |
| <span data-ttu-id="698c1-166">사용자 조치</span><span class="sxs-lookup"><span data-stu-id="698c1-166">User action</span></span> | <span data-ttu-id="698c1-167">규약 설정에서 스키마를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="698c1-167">Configure schema in the agreement settings</span></span>  |
|   |   |

### <a name="-incorrect-schema-in-the-agreement"></a><span data-ttu-id="698c1-168">* 규약에 잘못된 스키마가 있음</span><span class="sxs-lookup"><span data-stu-id="698c1-168">* Incorrect schema in the agreement</span></span>

|   |   | 
|---|---| 
| <span data-ttu-id="698c1-169">오류 설명</span><span class="sxs-lookup"><span data-stu-id="698c1-169">Error description</span></span> | <span data-ttu-id="698c1-170">이 메시지의 문서 유형을 알 수 없으며 규약에 구성된 기존 스키마로 확인되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="698c1-170">The message has an unknown document type and did not resolve to any of the existing schemas configured in the agreement.</span></span> |
| <span data-ttu-id="698c1-171">사용자 조치</span><span class="sxs-lookup"><span data-stu-id="698c1-171">User action</span></span> | <span data-ttu-id="698c1-172">규약 설정에서 올바른 스키마를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="698c1-172">Configure correct schema in the agreement settings</span></span>  |
|   |   |

## <a name="flat-file"></a><span data-ttu-id="698c1-173">플랫 파일</span><span class="sxs-lookup"><span data-stu-id="698c1-173">Flat file</span></span>

### <a name="-input-message-with-no-body"></a><span data-ttu-id="698c1-174">* 본문이 없는 입력 메시지</span><span class="sxs-lookup"><span data-stu-id="698c1-174">* Input message with no body</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="698c1-175">오류 설명</span><span class="sxs-lookup"><span data-stu-id="698c1-175">Error description</span></span> | <span data-ttu-id="698c1-176">잘못된 템플릿(InvalidTemplate)입니다.</span><span class="sxs-lookup"><span data-stu-id="698c1-176">InvalidTemplate.</span></span> <span data-ttu-id="698c1-177">프로세스 템플릿 언어 식 '1' 줄 및 '1902' 열에서 작업 'Flat_File_Decoding' 입력에 있는 수 없음: ' 'content' 속성에 값 데 null 16 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="698c1-177">Unable to process template language expressions in action 'Flat_File_Decoding' inputs at line '1' and column '1902': 'Required property 'content' expects a value but got null.</span></span> <span data-ttu-id="698c1-178">경로 '.'.</span><span class="sxs-lookup"><span data-stu-id="698c1-178">Path ''.'.</span></span> |
| <span data-ttu-id="698c1-179">사용자 조치</span><span class="sxs-lookup"><span data-stu-id="698c1-179">User action</span></span> | <span data-ttu-id="698c1-180">이 오류는 입력 메시지에 본문이 포함되어 있지 않음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="698c1-180">This error indicates the input message does not contain a body</span></span> |
|   |   | 

## <a name="learn-more"></a><span data-ttu-id="698c1-181">자세한 정보</span><span class="sxs-lookup"><span data-stu-id="698c1-181">Learn more</span></span>
[<span data-ttu-id="698c1-182">엔터프라이즈 통합 팩에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="698c1-182">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md)
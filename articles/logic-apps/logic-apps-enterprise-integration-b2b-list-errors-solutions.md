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
ms.openlocfilehash: 0340e2979f1972ba631354e206c93969e55946e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="logic-apps-b2b-list-of-errors-and-solutions"></a><span data-ttu-id="007dc-103">Logic Apps B2B 오류 및 해결 방법 목록</span><span class="sxs-lookup"><span data-stu-id="007dc-103">Logic Apps B2B list of errors and solutions</span></span>  
<span data-ttu-id="007dc-104">이 문서에서는 Logic Apps B2B 시나리오에서 발생할 수 있는 오류를 해결하고 이러한 오류를 수정하기 위한 적절한 조치를 제안합니다.</span><span class="sxs-lookup"><span data-stu-id="007dc-104">This article helps you troubleshoot errors that might happen in Logic Apps B2B scenarios and suggests appropriate actions for correcting those errors.</span></span>


## <a name="agreement-resolution"></a><span data-ttu-id="007dc-105">규약 확인</span><span class="sxs-lookup"><span data-stu-id="007dc-105">Agreement Resolution</span></span>

### <a name="no-agreement-found"></a><span data-ttu-id="007dc-106">* 규약을 찾을 수 없음</span><span class="sxs-lookup"><span data-stu-id="007dc-106">*No agreement found</span></span> 

|   |   |  
|---|---|
| <span data-ttu-id="007dc-107">오류 설명</span><span class="sxs-lookup"><span data-stu-id="007dc-107">Error description</span></span> | <span data-ttu-id="007dc-108">규약 확인 매개 변수가 있는 규약을 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="007dc-108">No agreement found with Agreement Resolution Parameters</span></span>|    
| <span data-ttu-id="007dc-109">사용자 조치</span><span class="sxs-lookup"><span data-stu-id="007dc-109">User action</span></span> | <span data-ttu-id="007dc-110">hello 계약 동의한 비즈니스 id와 toohello 통합 계정을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="007dc-110">hello agreement should be added toohello integration account with agreed business identities.</span></span></br> <span data-ttu-id="007dc-111">hello 비즈니스 id toohello 입력된 메시지 id가 일치 해야</span><span class="sxs-lookup"><span data-stu-id="007dc-111">hello business identities should match toohello input message ids</span></span>|  
|   |   |

### <a name="-no-agreement-found-with-identities"></a><span data-ttu-id="007dc-112">* ID가 있는 규약을 찾을 수 없음</span><span class="sxs-lookup"><span data-stu-id="007dc-112">* No agreement found with identities</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="007dc-113">오류 설명</span><span class="sxs-lookup"><span data-stu-id="007dc-113">Error description</span></span> | <span data-ttu-id="007dc-114">ID가 'AS2Identity'::'Partner1' 및 'AS2Identity'::'Partner3'인 규약을 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="007dc-114">No agreement found with identities: 'AS2Identity'::'Partner1' and'AS2Identity'::'Partner3'</span></span>| 
| <span data-ttu-id="007dc-115">사용자 조치</span><span class="sxs-lookup"><span data-stu-id="007dc-115">User action</span></span> | <span data-ttu-id="007dc-116">잘못 된 AS2-에서 또는 규약에 대 한 AS2 tooconfigured 합니다.</span><span class="sxs-lookup"><span data-stu-id="007dc-116">Invalid AS2-From or AS2-tooconfigured for agreement.</span></span> </br> <span data-ttu-id="007dc-117">올바른 AS2 메시지가 AS2-에서 또는 AS2 tooheaders 또는 계약 toomatch AS2 id에서 AS2 메시지 헤더를 규약 구성</span><span class="sxs-lookup"><span data-stu-id="007dc-117">Correct AS2 message AS2-From or AS2-tooheaders or agreement toomatch AS2 ids in AS2 message headers with agreement configurations</span></span> |
|   |   |     

## <a name="as2"></a><span data-ttu-id="007dc-118">AS2</span><span class="sxs-lookup"><span data-stu-id="007dc-118">AS2</span></span>

### <a name="-missing-as2-message-headers"></a><span data-ttu-id="007dc-119">* 누락된 AS2 메시지 헤더</span><span class="sxs-lookup"><span data-stu-id="007dc-119">* Missing AS2 message headers</span></span>  

|   |   |  
|---|---|
| <span data-ttu-id="007dc-120">오류 설명</span><span class="sxs-lookup"><span data-stu-id="007dc-120">Error description</span></span>| <span data-ttu-id="007dc-121">AS2 헤더가 잘못되었습니다.</span><span class="sxs-lookup"><span data-stu-id="007dc-121">Invalid AS2 headers.</span></span> <span data-ttu-id="007dc-122">'AS2-To' 또는 'AS2-From' 헤더 중 하나가 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="007dc-122">One of 'AS2-To' or 'AS2-From' headers are empty</span></span>| 
| <span data-ttu-id="007dc-123">사용자 조치</span><span class="sxs-lookup"><span data-stu-id="007dc-123">User action</span></span> | <span data-ttu-id="007dc-124">AS2 hello를 포함 하지 않은 AS2 메시지가 수신 된-에서 또는 AS2 tooor 두 헤더가 모두 합니다.</span><span class="sxs-lookup"><span data-stu-id="007dc-124">An AS2 message was received that did not contain hello AS2-From or AS2-tooor both headers.</span></span> </br> <span data-ttu-id="007dc-125">AS2 메시지가 AS2 확인-에서 및 tooheaders AS2 규약 구성에 따라 수정</span><span class="sxs-lookup"><span data-stu-id="007dc-125">Check AS2 message AS2-From and AS2-tooheaders and correct them based on agreement configuration</span></span> |
|  |  | 


### <a name="-missing-as2-message-body-and-headers"></a><span data-ttu-id="007dc-126">* 누락된 AS2 메시지 본문 및 헤더</span><span class="sxs-lookup"><span data-stu-id="007dc-126">* Missing AS2 message body and headers</span></span>    

|   |   |  
|---|---|
| <span data-ttu-id="007dc-127">오류 설명</span><span class="sxs-lookup"><span data-stu-id="007dc-127">Error description</span></span>| <span data-ttu-id="007dc-128">콘텐츠를 요청 하는 hello가 null 이거나 비어</span><span class="sxs-lookup"><span data-stu-id="007dc-128">hello request content is null or empty</span></span> | 
| <span data-ttu-id="007dc-129">사용자 조치</span><span class="sxs-lookup"><span data-stu-id="007dc-129">User action</span></span> | <span data-ttu-id="007dc-130">Hello 메시지 본문을 포함 하지 않은 AS2 메시지가 수신 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="007dc-130">An AS2 message was received that did not contain hello message body</span></span> |
|  |  | 

### <a name="-as2-message-decryption-failure"></a><span data-ttu-id="007dc-131">* AS2 메시지 암호 해독 실패</span><span class="sxs-lookup"><span data-stu-id="007dc-131">* AS2 message decryption failure</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="007dc-132">오류 설명</span><span class="sxs-lookup"><span data-stu-id="007dc-132">Error description</span></span> |  <span data-ttu-id="007dc-133">[처리됨/오류: 암호 해독 실패]</span><span class="sxs-lookup"><span data-stu-id="007dc-133">[processed/Error: decryption-failed]</span></span> | 
| <span data-ttu-id="007dc-134">사용자 조치</span><span class="sxs-lookup"><span data-stu-id="007dc-134">User action</span></span> | <span data-ttu-id="007dc-135">추가 @base64ToBinary toopartner 보내기 전에 tooAS2Message</span><span class="sxs-lookup"><span data-stu-id="007dc-135">Add @base64ToBinary tooAS2Message before sending toopartner</span></span> 
```java
            "HTTP": {
                "inputs": {
                    "body": "@base64ToBinary(body('Encode_to_AS2_message')?['AS2Message']?['Content'])",
                    "headers": "@body('Encode_to_AS2_message')?['AS2Message']?['OutboundHeaders']",
                    "method": "POST",
                    "uri": "xxxxx.xxx"
                },
                
``` 

### <a name="-mdn-decryption-failure"></a><span data-ttu-id="007dc-136">* MDN 암호 해독 실패</span><span class="sxs-lookup"><span data-stu-id="007dc-136">* MDN decryption failure</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="007dc-137">오류 설명</span><span class="sxs-lookup"><span data-stu-id="007dc-137">Error description</span></span> |  <span data-ttu-id="007dc-138">[처리됨/오류: 암호 해독 실패]</span><span class="sxs-lookup"><span data-stu-id="007dc-138">[processed/Error: decryption-failed]</span></span> | 
| <span data-ttu-id="007dc-139">사용자 조치</span><span class="sxs-lookup"><span data-stu-id="007dc-139">User action</span></span> | <span data-ttu-id="007dc-140">추가 @base64ToBinary toopartner 보내기 전에 tooMDN</span><span class="sxs-lookup"><span data-stu-id="007dc-140">Add @base64ToBinary tooMDN before sending toopartner</span></span> 
```java
            "Response": {
                "inputs": {
                    "body": "@base64ToBinary(body('Decode_AS2_message')?['OutgoingMDN']?['Content'])",
                    "headers": "@body('Decode_AS2_message')?['OutgoingMDN']?['OutboundHeaders']",
                    "statusCode": 200
                },
                
``` 

### <a name="-missing-signing-certificate"></a><span data-ttu-id="007dc-141">* 누락된 서명 인증서</span><span class="sxs-lookup"><span data-stu-id="007dc-141">* Missing signing certificate</span></span>

|   |   |  
|---|---|
| <span data-ttu-id="007dc-142">오류 설명</span><span class="sxs-lookup"><span data-stu-id="007dc-142">Error description</span></span>| <span data-ttu-id="007dc-143">hello 서명 인증서 구성 되지 않았습니다 AS2 파티에 대해 합니다.</span><span class="sxs-lookup"><span data-stu-id="007dc-143">hello Signing Certificate has not been configured for AS2 party.</span></span> </br> <span data-ttu-id="007dc-144">AS2-From: partner1 AS2-To: partner2</span><span class="sxs-lookup"><span data-stu-id="007dc-144">AS2-From: partner1 AS2-To: partner2</span></span> | 
| <span data-ttu-id="007dc-145">사용자 조치</span><span class="sxs-lookup"><span data-stu-id="007dc-145">User action</span></span> | <span data-ttu-id="007dc-146">서명을 위한 올바른 인증서로 AS2 규약 설정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="007dc-146">Configure AS2 agreement settings with correct certificate for signature</span></span> |
|  |  | 

## <a name="x12-and-edifact"></a><span data-ttu-id="007dc-147">X12 및 EDIFACT</span><span class="sxs-lookup"><span data-stu-id="007dc-147">X12 and EDIFACT</span></span>

### <a name="-leading-or-trailing-space-found"></a><span data-ttu-id="007dc-148">* 선행 공백 또는 후행 공백이 있음</span><span class="sxs-lookup"><span data-stu-id="007dc-148">* Leading or trailing space found</span></span>    
    
|   |   | 
|---|---|
| <span data-ttu-id="007dc-149">오류 설명</span><span class="sxs-lookup"><span data-stu-id="007dc-149">Error description</span></span> | <span data-ttu-id="007dc-150">구문 분석 중에 오류가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="007dc-150">Error encountered during parsing.</span></span> <span data-ttu-id="007dc-151">Edifact 트랜잭션 집합 id ' 123456 'id ' 987654 된 교환 (그룹 제외)에 포함 된' hello, 보낸 사람 id 'Partner1', 받는 사람 id 'Partner2' 일시 중단 됩니다. 다음 오류로 인해: 발견 앞에 후행 구분 기호</span><span class="sxs-lookup"><span data-stu-id="007dc-151">hello Edifact transaction set with id '123456' contained in interchange (without group) with id '987654', with sender id 'Partner1', receiver id 'Partner2' is being suspended with following errors: Leading Trailing separator found</span></span> |
| <span data-ttu-id="007dc-152">사용자 조치</span><span class="sxs-lookup"><span data-stu-id="007dc-152">User action</span></span> | <span data-ttu-id="007dc-153">hello 규약 설정 toobe tooallow 선행 및 후행 공백이 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="007dc-153">hello agreement settings toobe configured tooallow leading and trailing space.</span></span> </br> <span data-ttu-id="007dc-154">선행 및 후행 공백이 규약 설정을 tooallow 편집</span><span class="sxs-lookup"><span data-stu-id="007dc-154">Edit agreement settings tooallow leading and trailing space</span></span> |
|   |   |

![공백 허용](./media/logic-apps-enterprise-integration-b2b-list-errors-solutions/leadingandtrailing.png)

### <a name="-duplicate-check-has-enabled-in-hello-agreement"></a><span data-ttu-id="007dc-156">* Hello 규약에서 중복 검사에 사용할 수</span><span class="sxs-lookup"><span data-stu-id="007dc-156">* Duplicate check has enabled in hello agreement</span></span>

|   |   | 
|---|---| 
| <span data-ttu-id="007dc-157">오류 설명</span><span class="sxs-lookup"><span data-stu-id="007dc-157">Error description</span></span> | <span data-ttu-id="007dc-158">중복 컨트롤 번호가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="007dc-158">Duplicate Control Number</span></span> |
| <span data-ttu-id="007dc-159">사용자 조치</span><span class="sxs-lookup"><span data-stu-id="007dc-159">User action</span></span> | <span data-ttu-id="007dc-160">이 오류는 수신 하는 hello 메시지는 중복 컨트롤 번호를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="007dc-160">This error indicates hello received message has duplicate control numbers.</span></span> </br> <span data-ttu-id="007dc-161">Hello 컨트롤 번호를 수정 하 고 hello 메시지를 다시 보내십시오.</span><span class="sxs-lookup"><span data-stu-id="007dc-161">Correct hello control number and resend hello message</span></span> |
|   |   |

### <a name="-missing-schema-in-hello-agreement"></a><span data-ttu-id="007dc-162">* Hello 계약의 누락 된 스키마</span><span class="sxs-lookup"><span data-stu-id="007dc-162">* Missing schema in hello agreement</span></span>

|   |   | 
|---|---| 
| <span data-ttu-id="007dc-163">오류 설명</span><span class="sxs-lookup"><span data-stu-id="007dc-163">Error description</span></span> | <span data-ttu-id="007dc-164">구문 분석 중에 오류가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="007dc-164">Error encountered during parsing.</span></span> <span data-ttu-id="007dc-165">hello X12 트랜잭션 집합 id를 가진 '564220001'에 포함 된 기능 그룹 id가 ' 56422', 보낸 사람 id 12345678 ' id '000056422' 인 교환의 ' 인 수신기 id ' 87654321' "hello 메시지에 알 수 없는 문서 ty 하는 다음 오류로 일시 중단 됩니다. pe 및 tooany hello 규약에서 구성 된 hello 기존 스키마의 해결 되지 않았습니다 "</span><span class="sxs-lookup"><span data-stu-id="007dc-165">hello X12 transaction set with id '564220001' contained in functional group with id '56422', in interchange with id '000056422', with sender id '12345678       ', receiver id '87654321       ' is being suspended with following errors "hello message has an unknown document type and did not resolve tooany of hello existing schemas configured in hello agreement"</span></span> |
| <span data-ttu-id="007dc-166">사용자 조치</span><span class="sxs-lookup"><span data-stu-id="007dc-166">User action</span></span> | <span data-ttu-id="007dc-167">Hello 규약 설정에서 스키마를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="007dc-167">Configure schema in hello agreement settings</span></span>  |
|   |   |

### <a name="-incorrect-schema-in-hello-agreement"></a><span data-ttu-id="007dc-168">* Hello 계약에 잘못 된 스키마</span><span class="sxs-lookup"><span data-stu-id="007dc-168">* Incorrect schema in hello agreement</span></span>

|   |   | 
|---|---| 
| <span data-ttu-id="007dc-169">오류 설명</span><span class="sxs-lookup"><span data-stu-id="007dc-169">Error description</span></span> | <span data-ttu-id="007dc-170">hello 메시지는 알 수 없는 문서 형식이 고 tooany hello 규약에서 구성 된 hello 기존 스키마의 해결 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="007dc-170">hello message has an unknown document type and did not resolve tooany of hello existing schemas configured in hello agreement.</span></span> |
| <span data-ttu-id="007dc-171">사용자 조치</span><span class="sxs-lookup"><span data-stu-id="007dc-171">User action</span></span> | <span data-ttu-id="007dc-172">Hello 규약 설정에서 올바른 스키마를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="007dc-172">Configure correct schema in hello agreement settings</span></span>  |
|   |   |

## <a name="flat-file"></a><span data-ttu-id="007dc-173">플랫 파일</span><span class="sxs-lookup"><span data-stu-id="007dc-173">Flat file</span></span>

### <a name="-input-message-with-no-body"></a><span data-ttu-id="007dc-174">* 본문이 없는 입력 메시지</span><span class="sxs-lookup"><span data-stu-id="007dc-174">* Input message with no body</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="007dc-175">오류 설명</span><span class="sxs-lookup"><span data-stu-id="007dc-175">Error description</span></span> | <span data-ttu-id="007dc-176">잘못된 템플릿(InvalidTemplate)입니다.</span><span class="sxs-lookup"><span data-stu-id="007dc-176">InvalidTemplate.</span></span> <span data-ttu-id="007dc-177">줄 '1' 및 '1902' 열에서 작업 'Flat_File_Decoding' 입력에 없습니다 tooprocess 템플릿 언어 식을: ' 'content' 속성에 값 데 null 16 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="007dc-177">Unable tooprocess template language expressions in action 'Flat_File_Decoding' inputs at line '1' and column '1902': 'Required property 'content' expects a value but got null.</span></span> <span data-ttu-id="007dc-178">경로 '.'.</span><span class="sxs-lookup"><span data-stu-id="007dc-178">Path ''.'.</span></span> |
| <span data-ttu-id="007dc-179">사용자 조치</span><span class="sxs-lookup"><span data-stu-id="007dc-179">User action</span></span> | <span data-ttu-id="007dc-180">이 오류 hello 입력된 메시지에 본문이 포함 되지 않습니다 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="007dc-180">This error indicates hello input message does not contain a body</span></span> |
|   |   | 

## <a name="learn-more"></a><span data-ttu-id="007dc-181">자세한 정보</span><span class="sxs-lookup"><span data-stu-id="007dc-181">Learn more</span></span>
[<span data-ttu-id="007dc-182">엔터프라이즈 통합 팩 hello에 대 한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="007dc-182">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md)

---
title: "마켓플레이스 요금 청구 엔터프라이즈 Api-aaaAzure | Microsoft Docs"
description: "Hello Enterprise Azure 고객 toopull 소비 데이터에 프로그래밍 방식으로 사용할 수 있는 보고 Api에 알아봅니다."
services: 
documentationcenter: 
author: aedwin
manager: aedwin
editor: 
tags: billing
ms.assetid: 3e817b43-0696-400c-a02e-47b7817f9b77
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: billing
ms.date: 04/25/2017
ms.author: aedwin
ms.openlocfilehash: cdf2836b52df06a4bf5ed71a476fe33662c5363c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---marketplace-store-charge"></a><span data-ttu-id="4526c-103">기업 고객을 위한 보고 API - Marketplace 스토어 요금(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="4526c-103">Reporting APIs for Enterprise customers - Marketplace Store Charge</span></span>

<span data-ttu-id="4526c-104">hello hello에 대 한 일별 마켓플레이스 저장 충전 API 반환 hello 마켓플레이스 사용량 기반 요금 분석 대금 청구 기간 또는 시작 및 종료 날짜 (한 번 요금 포함 되지 않습니다.)를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4526c-104">hello Marketplace Store Charge API returns hello usage-based marketplace charges breakdown by day for hello specified Billing Period or start and end dates (one time fees are not included).</span></span>

##<a name="request"></a><span data-ttu-id="4526c-105">요청</span><span class="sxs-lookup"><span data-stu-id="4526c-105">Request</span></span> 
<span data-ttu-id="4526c-106">Toobe 추가 해야 하는 공통 헤더 속성이 지정 되어 [여기](billing-enterprise-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4526c-106">Common header properties that need toobe added are specified [here](billing-enterprise-api.md).</span></span> <span data-ttu-id="4526c-107">청구 기간 지정 하지 않으면 다음 hello 현재 청구에 대 한 데이터 기간 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4526c-107">If a billing period is not specified, then data for hello current billing period is returned.</span></span> <span data-ttu-id="4526c-108">사용자가 지정한 시간 범위 hello 시작 되 면 지정할 수 있으며 hello 형식 yyyy-월-일 지원 hello 최대 시간 범위는 36 개월에에서 있는 날짜 매개 변수를 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="4526c-108">Custom time ranges can be specified with hello start and end date parameters that are in hello format yyyy-MM-dd, hello maximum supported time range is 36 months.</span></span>  

|<span data-ttu-id="4526c-109">메서드</span><span class="sxs-lookup"><span data-stu-id="4526c-109">Method</span></span> | <span data-ttu-id="4526c-110">요청 URI</span><span class="sxs-lookup"><span data-stu-id="4526c-110">Request URI</span></span>|
|-|-|
|<span data-ttu-id="4526c-111">GET</span><span class="sxs-lookup"><span data-stu-id="4526c-111">GET</span></span>|<span data-ttu-id="4526c-112">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacecharges</span><span class="sxs-lookup"><span data-stu-id="4526c-112">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacecharges</span></span>|
|<span data-ttu-id="4526c-113">GET</span><span class="sxs-lookup"><span data-stu-id="4526c-113">GET</span></span>|<span data-ttu-id="4526c-114">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/marketplacecharges</span><span class="sxs-lookup"><span data-stu-id="4526c-114">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/marketplacecharges</span></span>|
|<span data-ttu-id="4526c-115">GET</span><span class="sxs-lookup"><span data-stu-id="4526c-115">GET</span></span>|<span data-ttu-id="4526c-116">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacechargesbycustomdate?startTime=2017-01-01&endTime=2017-01-10</span><span class="sxs-lookup"><span data-stu-id="4526c-116">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacechargesbycustomdate?startTime=2017-01-01&endTime=2017-01-10</span></span>|

> [!Note]
> <span data-ttu-id="4526c-117">toouse hello 미리 보기 버전의 API, URL 위에 hello v1 v2를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="4526c-117">toouse hello preview version of API, replace v2 with v1 in hello above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="4526c-118">응답</span><span class="sxs-lookup"><span data-stu-id="4526c-118">Response</span></span>
 
    
        [
            {
                "id": "id",
                "subscriptionGuid": "00000000-0000-0000-0000-000000000000",
                "subscriptionName": "subName",
                "meterId": "2core",
                "usageStartDate": "2015-09-17T00:00:00Z",
                "usageEndDate": "2015-09-17T23:59:59Z",
                "offerName": "Virtual LoadMaster™ (VLM) for Azure",
                "resourceGroup": "Res group",
                "instanceId": "id",
                "additionalInfo": "{\"ImageType\":null,\"ServiceType\":\"Medium\"}",
                "tags": "",
                "orderNumber": "order",
                "unitOfMeasure": "",
                "costCenter": "100",
                "accountId": 100,
                "accountName": "Account Name",
                "accountOwnerId": "account@live.com",
                "departmentId": 101,
                "departmentName": "Department 1",
                "publisherName": "Publisher 1",
                "planName": "Plan name",
                "consumedQuantity": 1.15,
                "resourceRate": 0.1,
                "extendedCost": 1.11
            },
            ...
        ]
    

<span data-ttu-id="4526c-119">**응답 속성 정의**</span><span class="sxs-lookup"><span data-stu-id="4526c-119">**Response property definitions**</span></span>

|<span data-ttu-id="4526c-120">속성 이름</span><span class="sxs-lookup"><span data-stu-id="4526c-120">Property Name</span></span>| <span data-ttu-id="4526c-121">형식</span><span class="sxs-lookup"><span data-stu-id="4526c-121">Type</span></span>| <span data-ttu-id="4526c-122">설명</span><span class="sxs-lookup"><span data-stu-id="4526c-122">Description</span></span>
|-|-|-|
|<span data-ttu-id="4526c-123">id</span><span class="sxs-lookup"><span data-stu-id="4526c-123">id</span></span>|<span data-ttu-id="4526c-124">string</span><span class="sxs-lookup"><span data-stu-id="4526c-124">string</span></span>|<span data-ttu-id="4526c-125">Hello 마켓플레이스 요금 항목에 대 한 고유 Id</span><span class="sxs-lookup"><span data-stu-id="4526c-125">Unique Id for hello marketplace charge item</span></span>|
|<span data-ttu-id="4526c-126">subscriptionGuid</span><span class="sxs-lookup"><span data-stu-id="4526c-126">subscriptionGuid</span></span>|<span data-ttu-id="4526c-127">Guid</span><span class="sxs-lookup"><span data-stu-id="4526c-127">Guid</span></span>|<span data-ttu-id="4526c-128">hello 구독 Guid</span><span class="sxs-lookup"><span data-stu-id="4526c-128">hello Subscription Guid</span></span>|
|<span data-ttu-id="4526c-129">subscriptionName</span><span class="sxs-lookup"><span data-stu-id="4526c-129">subscriptionName</span></span>|<span data-ttu-id="4526c-130">string</span><span class="sxs-lookup"><span data-stu-id="4526c-130">string</span></span>|<span data-ttu-id="4526c-131">hello 구독 이름</span><span class="sxs-lookup"><span data-stu-id="4526c-131">hello Subscription Name</span></span>|
|<span data-ttu-id="4526c-132">meterId</span><span class="sxs-lookup"><span data-stu-id="4526c-132">meterId</span></span>|<span data-ttu-id="4526c-133">string</span><span class="sxs-lookup"><span data-stu-id="4526c-133">string</span></span>|<span data-ttu-id="4526c-134">측정기를 내보내는 hello에 대 한 id</span><span class="sxs-lookup"><span data-stu-id="4526c-134">Id for hello emitted Meter</span></span>|
|<span data-ttu-id="4526c-135">usageStartDate</span><span class="sxs-lookup"><span data-stu-id="4526c-135">usageStartDate</span></span>|<span data-ttu-id="4526c-136">DateTime</span><span class="sxs-lookup"><span data-stu-id="4526c-136">DateTime</span></span>|<span data-ttu-id="4526c-137">Hello 사용량 레코드에 대 한 시작 시간</span><span class="sxs-lookup"><span data-stu-id="4526c-137">Start time for hello usage record</span></span>|
|<span data-ttu-id="4526c-138">usageEndDate</span><span class="sxs-lookup"><span data-stu-id="4526c-138">usageEndDate</span></span>|<span data-ttu-id="4526c-139">DateTime</span><span class="sxs-lookup"><span data-stu-id="4526c-139">DateTime</span></span>|<span data-ttu-id="4526c-140">Hello 사용량 레코드에 대 한 종료 시간</span><span class="sxs-lookup"><span data-stu-id="4526c-140">End time for hello usage record</span></span>|
|<span data-ttu-id="4526c-141">offerName</span><span class="sxs-lookup"><span data-stu-id="4526c-141">offerName</span></span>|<span data-ttu-id="4526c-142">string</span><span class="sxs-lookup"><span data-stu-id="4526c-142">string</span></span>|<span data-ttu-id="4526c-143">hello 제안 이름</span><span class="sxs-lookup"><span data-stu-id="4526c-143">hello Offer name</span></span>|
|<span data-ttu-id="4526c-144">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="4526c-144">resourceGroup</span></span>|<span data-ttu-id="4526c-145">string</span><span class="sxs-lookup"><span data-stu-id="4526c-145">string</span></span>|<span data-ttu-id="4526c-146">hello 리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="4526c-146">hello resource Group</span></span>|
|<span data-ttu-id="4526c-147">instanceId</span><span class="sxs-lookup"><span data-stu-id="4526c-147">instanceId</span></span>|<span data-ttu-id="4526c-148">string</span><span class="sxs-lookup"><span data-stu-id="4526c-148">string</span></span>|<span data-ttu-id="4526c-149">인스턴스 ID</span><span class="sxs-lookup"><span data-stu-id="4526c-149">Instance Id</span></span>|
|<span data-ttu-id="4526c-150">additionalInfo</span><span class="sxs-lookup"><span data-stu-id="4526c-150">additionalInfo</span></span>|<span data-ttu-id="4526c-151">string</span><span class="sxs-lookup"><span data-stu-id="4526c-151">string</span></span>|<span data-ttu-id="4526c-152">추가 정보 JSON 문자열</span><span class="sxs-lookup"><span data-stu-id="4526c-152">Additional info JSON string</span></span>|
|<span data-ttu-id="4526c-153">tags</span><span class="sxs-lookup"><span data-stu-id="4526c-153">tags</span></span>|<span data-ttu-id="4526c-154">string</span><span class="sxs-lookup"><span data-stu-id="4526c-154">string</span></span>|<span data-ttu-id="4526c-155">태그 JSON 문자열</span><span class="sxs-lookup"><span data-stu-id="4526c-155">Tag JSON string</span></span>|
|<span data-ttu-id="4526c-156">orderNumber</span><span class="sxs-lookup"><span data-stu-id="4526c-156">orderNumber</span></span>|<span data-ttu-id="4526c-157">string</span><span class="sxs-lookup"><span data-stu-id="4526c-157">string</span></span>|<span data-ttu-id="4526c-158">hello 주문 번호</span><span class="sxs-lookup"><span data-stu-id="4526c-158">hello order number</span></span>|
|<span data-ttu-id="4526c-159">unitOfMeasure</span><span class="sxs-lookup"><span data-stu-id="4526c-159">unitOfMeasure</span></span>|<span data-ttu-id="4526c-160">string</span><span class="sxs-lookup"><span data-stu-id="4526c-160">string</span></span>|<span data-ttu-id="4526c-161">측정기 hello에 대 한 측정 단위</span><span class="sxs-lookup"><span data-stu-id="4526c-161">Unit of measure for hello meter</span></span>|
|<span data-ttu-id="4526c-162">costCenter</span><span class="sxs-lookup"><span data-stu-id="4526c-162">costCenter</span></span>|<span data-ttu-id="4526c-163">string</span><span class="sxs-lookup"><span data-stu-id="4526c-163">string</span></span>|<span data-ttu-id="4526c-164">hello 비용 센터</span><span class="sxs-lookup"><span data-stu-id="4526c-164">hello cost center</span></span>|
|<span data-ttu-id="4526c-165">accountId</span><span class="sxs-lookup"><span data-stu-id="4526c-165">accountId</span></span>|<span data-ttu-id="4526c-166">int</span><span class="sxs-lookup"><span data-stu-id="4526c-166">int</span></span>|<span data-ttu-id="4526c-167">hello 계정 Id</span><span class="sxs-lookup"><span data-stu-id="4526c-167">hello account Id</span></span>|
|<span data-ttu-id="4526c-168">accountName</span><span class="sxs-lookup"><span data-stu-id="4526c-168">accountName</span></span>|<span data-ttu-id="4526c-169">string</span><span class="sxs-lookup"><span data-stu-id="4526c-169">string</span></span> |<span data-ttu-id="4526c-170">hello 계정 이름</span><span class="sxs-lookup"><span data-stu-id="4526c-170">hello Account Name</span></span>|
|<span data-ttu-id="4526c-171">accountOwnerId</span><span class="sxs-lookup"><span data-stu-id="4526c-171">accountOwnerId</span></span>|<span data-ttu-id="4526c-172">string</span><span class="sxs-lookup"><span data-stu-id="4526c-172">string</span></span>|<span data-ttu-id="4526c-173">hello 계정 소유자 Id</span><span class="sxs-lookup"><span data-stu-id="4526c-173">hello Account Owner Id</span></span>|
|<span data-ttu-id="4526c-174">departmentId</span><span class="sxs-lookup"><span data-stu-id="4526c-174">departmentId</span></span>|<span data-ttu-id="4526c-175">int</span><span class="sxs-lookup"><span data-stu-id="4526c-175">int</span></span>|<span data-ttu-id="4526c-176">hello 부서 Id</span><span class="sxs-lookup"><span data-stu-id="4526c-176">hello department Id</span></span>|
|<span data-ttu-id="4526c-177">departmentName</span><span class="sxs-lookup"><span data-stu-id="4526c-177">departmentName</span></span>|<span data-ttu-id="4526c-178">string</span><span class="sxs-lookup"><span data-stu-id="4526c-178">string</span></span>|<span data-ttu-id="4526c-179">hello 부서 이름</span><span class="sxs-lookup"><span data-stu-id="4526c-179">hello department name</span></span>|
|<span data-ttu-id="4526c-180">publisherName</span><span class="sxs-lookup"><span data-stu-id="4526c-180">publisherName</span></span>|<span data-ttu-id="4526c-181">string</span><span class="sxs-lookup"><span data-stu-id="4526c-181">string</span></span>|<span data-ttu-id="4526c-182">hello 게시자 이름</span><span class="sxs-lookup"><span data-stu-id="4526c-182">hello publisher name</span></span>|
|<span data-ttu-id="4526c-183">planName</span><span class="sxs-lookup"><span data-stu-id="4526c-183">planName</span></span>|<span data-ttu-id="4526c-184">string</span><span class="sxs-lookup"><span data-stu-id="4526c-184">string</span></span>|<span data-ttu-id="4526c-185">hello 계획 이름</span><span class="sxs-lookup"><span data-stu-id="4526c-185">hello Plan name</span></span>|
|<span data-ttu-id="4526c-186">consumedQuantity</span><span class="sxs-lookup"><span data-stu-id="4526c-186">consumedQuantity</span></span>|<span data-ttu-id="4526c-187">decimal</span><span class="sxs-lookup"><span data-stu-id="4526c-187">decimal</span></span>|<span data-ttu-id="4526c-188">이 기간 동안의 사용량</span><span class="sxs-lookup"><span data-stu-id="4526c-188">Consumed Quantity during this time period</span></span>|
|<span data-ttu-id="4526c-189">resourceRate</span><span class="sxs-lookup"><span data-stu-id="4526c-189">resourceRate</span></span>|<span data-ttu-id="4526c-190">decimal</span><span class="sxs-lookup"><span data-stu-id="4526c-190">decimal</span></span>|<span data-ttu-id="4526c-191">측정기 hello에 대 한 단위 가격</span><span class="sxs-lookup"><span data-stu-id="4526c-191">Unit price for hello meter</span></span>|
|<span data-ttu-id="4526c-192">extendedCost</span><span class="sxs-lookup"><span data-stu-id="4526c-192">extendedCost</span></span>|<span data-ttu-id="4526c-193">decimal</span><span class="sxs-lookup"><span data-stu-id="4526c-193">decimal</span></span>|<span data-ttu-id="4526c-194">사용량 및 확장 비용에 따른 예상 요금</span><span class="sxs-lookup"><span data-stu-id="4526c-194">Estimated charge based on Consumed Quantity and Extended cost</span></span>|
<br/>
## <a name="see-also"></a><span data-ttu-id="4526c-195">참고 항목</span><span class="sxs-lookup"><span data-stu-id="4526c-195">See also</span></span>

* [<span data-ttu-id="4526c-196">청구 기간 API</span><span class="sxs-lookup"><span data-stu-id="4526c-196">Billing Periods API</span></span>](billing-enterprise-api-billing-periods.md)

* [<span data-ttu-id="4526c-197">사용량 세부 정보 API</span><span class="sxs-lookup"><span data-stu-id="4526c-197">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md) 

* [<span data-ttu-id="4526c-198">잔액 및 요약 API</span><span class="sxs-lookup"><span data-stu-id="4526c-198">Balance and Summary API</span></span>](billing-enterprise-api-balance-summary.md)

* [<span data-ttu-id="4526c-199">가격표 API</span><span class="sxs-lookup"><span data-stu-id="4526c-199">Price Sheet API</span></span>](billing-enterprise-api-pricesheet.md)
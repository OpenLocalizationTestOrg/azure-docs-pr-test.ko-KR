---
title: "Azure 청구 엔터프라이즈 API - Marketplace 요금 | Microsoft Docs"
description: "Azure 기업 고객이 사용량 데이터를 프로그래밍 방식으로 끌어올 수 있게 하는 보고 API에 대해 알아봅니다."
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
ms.openlocfilehash: 5539623f7ae35e14b6dafe6fdf9efe4bcaba4fd3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="reporting-apis-for-enterprise-customers---marketplace-store-charge"></a><span data-ttu-id="1e693-103">기업 고객을 위한 보고 API - Marketplace 스토어 요금(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="1e693-103">Reporting APIs for Enterprise customers - Marketplace Store Charge</span></span>

<span data-ttu-id="1e693-104">Marketplace 저장소 요금 API는 지정된 청구 기간 또는 시작 날짜 및 종료 날짜(1회 요금은 포함되지 않음)에 대한 일별 사용량 기반 Marketplace 요금 분석 결과를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="1e693-104">The Marketplace Store Charge API returns the usage-based marketplace charges breakdown by day for the specified Billing Period or start and end dates (one time fees are not included).</span></span>

##<a name="request"></a><span data-ttu-id="1e693-105">요청</span><span class="sxs-lookup"><span data-stu-id="1e693-105">Request</span></span> 
<span data-ttu-id="1e693-106">추가해야 할 공통 헤더 속성은 [여기](billing-enterprise-api.md)에 지정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e693-106">Common header properties that need to be added are specified [here](billing-enterprise-api.md).</span></span> <span data-ttu-id="1e693-107">청구 기간을 지정하지 않으면 현재 청구 기간에 대한 데이터가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e693-107">If a billing period is not specified, then data for the current billing period is returned.</span></span> <span data-ttu-id="1e693-108">사용자 지정 시간 범위는 yyyy-MM-dd 형식으로 시작 날짜 및 종료 날짜 매개 변수로 지정할 수 있으며, 지원되는 최대 시간 범위는 36개월입니다.</span><span class="sxs-lookup"><span data-stu-id="1e693-108">Custom time ranges can be specified with the start and end date parameters that are in the format yyyy-MM-dd, the maximum supported time range is 36 months.</span></span>  

|<span data-ttu-id="1e693-109">메서드</span><span class="sxs-lookup"><span data-stu-id="1e693-109">Method</span></span> | <span data-ttu-id="1e693-110">요청 URI</span><span class="sxs-lookup"><span data-stu-id="1e693-110">Request URI</span></span>|
|-|-|
|<span data-ttu-id="1e693-111">GET</span><span class="sxs-lookup"><span data-stu-id="1e693-111">GET</span></span>|<span data-ttu-id="1e693-112">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacecharges</span><span class="sxs-lookup"><span data-stu-id="1e693-112">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacecharges</span></span>|
|<span data-ttu-id="1e693-113">GET</span><span class="sxs-lookup"><span data-stu-id="1e693-113">GET</span></span>|<span data-ttu-id="1e693-114">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/marketplacecharges</span><span class="sxs-lookup"><span data-stu-id="1e693-114">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/marketplacecharges</span></span>|
|<span data-ttu-id="1e693-115">GET</span><span class="sxs-lookup"><span data-stu-id="1e693-115">GET</span></span>|<span data-ttu-id="1e693-116">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacechargesbycustomdate?startTime=2017-01-01&endTime=2017-01-10</span><span class="sxs-lookup"><span data-stu-id="1e693-116">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacechargesbycustomdate?startTime=2017-01-01&endTime=2017-01-10</span></span>|

> [!Note]
> <span data-ttu-id="1e693-117">API의 미리 보기 버전을 사용하려면 위 URL에서 v2를 v1로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="1e693-117">To use the preview version of API, replace v2 with v1 in the above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="1e693-118">응답</span><span class="sxs-lookup"><span data-stu-id="1e693-118">Response</span></span>
 
    
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
    

<span data-ttu-id="1e693-119">**응답 속성 정의**</span><span class="sxs-lookup"><span data-stu-id="1e693-119">**Response property definitions**</span></span>

|<span data-ttu-id="1e693-120">속성 이름</span><span class="sxs-lookup"><span data-stu-id="1e693-120">Property Name</span></span>| <span data-ttu-id="1e693-121">형식</span><span class="sxs-lookup"><span data-stu-id="1e693-121">Type</span></span>| <span data-ttu-id="1e693-122">설명</span><span class="sxs-lookup"><span data-stu-id="1e693-122">Description</span></span>
|-|-|-|
|<span data-ttu-id="1e693-123">id</span><span class="sxs-lookup"><span data-stu-id="1e693-123">id</span></span>|<span data-ttu-id="1e693-124">string</span><span class="sxs-lookup"><span data-stu-id="1e693-124">string</span></span>|<span data-ttu-id="1e693-125">Marketplace 요금 항목에 대한 고유 ID</span><span class="sxs-lookup"><span data-stu-id="1e693-125">Unique Id for the marketplace charge item</span></span>|
|<span data-ttu-id="1e693-126">subscriptionGuid</span><span class="sxs-lookup"><span data-stu-id="1e693-126">subscriptionGuid</span></span>|<span data-ttu-id="1e693-127">Guid</span><span class="sxs-lookup"><span data-stu-id="1e693-127">Guid</span></span>|<span data-ttu-id="1e693-128">구독 Guid</span><span class="sxs-lookup"><span data-stu-id="1e693-128">The Subscription Guid</span></span>|
|<span data-ttu-id="1e693-129">subscriptionName</span><span class="sxs-lookup"><span data-stu-id="1e693-129">subscriptionName</span></span>|<span data-ttu-id="1e693-130">string</span><span class="sxs-lookup"><span data-stu-id="1e693-130">string</span></span>|<span data-ttu-id="1e693-131">구독 이름</span><span class="sxs-lookup"><span data-stu-id="1e693-131">The Subscription Name</span></span>|
|<span data-ttu-id="1e693-132">meterId</span><span class="sxs-lookup"><span data-stu-id="1e693-132">meterId</span></span>|<span data-ttu-id="1e693-133">string</span><span class="sxs-lookup"><span data-stu-id="1e693-133">string</span></span>|<span data-ttu-id="1e693-134">내보내는 측정기의 ID</span><span class="sxs-lookup"><span data-stu-id="1e693-134">Id for the emitted Meter</span></span>|
|<span data-ttu-id="1e693-135">usageStartDate</span><span class="sxs-lookup"><span data-stu-id="1e693-135">usageStartDate</span></span>|<span data-ttu-id="1e693-136">DateTime</span><span class="sxs-lookup"><span data-stu-id="1e693-136">DateTime</span></span>|<span data-ttu-id="1e693-137">사용량 기록의 시작 시간</span><span class="sxs-lookup"><span data-stu-id="1e693-137">Start time for the usage record</span></span>|
|<span data-ttu-id="1e693-138">usageEndDate</span><span class="sxs-lookup"><span data-stu-id="1e693-138">usageEndDate</span></span>|<span data-ttu-id="1e693-139">DateTime</span><span class="sxs-lookup"><span data-stu-id="1e693-139">DateTime</span></span>|<span data-ttu-id="1e693-140">사용량 기록의 종료 시간</span><span class="sxs-lookup"><span data-stu-id="1e693-140">End time for the usage record</span></span>|
|<span data-ttu-id="1e693-141">offerName</span><span class="sxs-lookup"><span data-stu-id="1e693-141">offerName</span></span>|<span data-ttu-id="1e693-142">string</span><span class="sxs-lookup"><span data-stu-id="1e693-142">string</span></span>|<span data-ttu-id="1e693-143">제품 이름</span><span class="sxs-lookup"><span data-stu-id="1e693-143">The Offer name</span></span>|
|<span data-ttu-id="1e693-144">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="1e693-144">resourceGroup</span></span>|<span data-ttu-id="1e693-145">string</span><span class="sxs-lookup"><span data-stu-id="1e693-145">string</span></span>|<span data-ttu-id="1e693-146">리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="1e693-146">The resource Group</span></span>|
|<span data-ttu-id="1e693-147">instanceId</span><span class="sxs-lookup"><span data-stu-id="1e693-147">instanceId</span></span>|<span data-ttu-id="1e693-148">string</span><span class="sxs-lookup"><span data-stu-id="1e693-148">string</span></span>|<span data-ttu-id="1e693-149">인스턴스 ID</span><span class="sxs-lookup"><span data-stu-id="1e693-149">Instance Id</span></span>|
|<span data-ttu-id="1e693-150">additionalInfo</span><span class="sxs-lookup"><span data-stu-id="1e693-150">additionalInfo</span></span>|<span data-ttu-id="1e693-151">string</span><span class="sxs-lookup"><span data-stu-id="1e693-151">string</span></span>|<span data-ttu-id="1e693-152">추가 정보 JSON 문자열</span><span class="sxs-lookup"><span data-stu-id="1e693-152">Additional info JSON string</span></span>|
|<span data-ttu-id="1e693-153">tags</span><span class="sxs-lookup"><span data-stu-id="1e693-153">tags</span></span>|<span data-ttu-id="1e693-154">string</span><span class="sxs-lookup"><span data-stu-id="1e693-154">string</span></span>|<span data-ttu-id="1e693-155">태그 JSON 문자열</span><span class="sxs-lookup"><span data-stu-id="1e693-155">Tag JSON string</span></span>|
|<span data-ttu-id="1e693-156">orderNumber</span><span class="sxs-lookup"><span data-stu-id="1e693-156">orderNumber</span></span>|<span data-ttu-id="1e693-157">string</span><span class="sxs-lookup"><span data-stu-id="1e693-157">string</span></span>|<span data-ttu-id="1e693-158">주문 번호</span><span class="sxs-lookup"><span data-stu-id="1e693-158">The order number</span></span>|
|<span data-ttu-id="1e693-159">unitOfMeasure</span><span class="sxs-lookup"><span data-stu-id="1e693-159">unitOfMeasure</span></span>|<span data-ttu-id="1e693-160">string</span><span class="sxs-lookup"><span data-stu-id="1e693-160">string</span></span>|<span data-ttu-id="1e693-161">측정기의 측정 단위</span><span class="sxs-lookup"><span data-stu-id="1e693-161">Unit of measure for the meter</span></span>|
|<span data-ttu-id="1e693-162">costCenter</span><span class="sxs-lookup"><span data-stu-id="1e693-162">costCenter</span></span>|<span data-ttu-id="1e693-163">string</span><span class="sxs-lookup"><span data-stu-id="1e693-163">string</span></span>|<span data-ttu-id="1e693-164">비용 센터</span><span class="sxs-lookup"><span data-stu-id="1e693-164">The cost center</span></span>|
|<span data-ttu-id="1e693-165">accountId</span><span class="sxs-lookup"><span data-stu-id="1e693-165">accountId</span></span>|<span data-ttu-id="1e693-166">int</span><span class="sxs-lookup"><span data-stu-id="1e693-166">int</span></span>|<span data-ttu-id="1e693-167">계정 ID</span><span class="sxs-lookup"><span data-stu-id="1e693-167">The account Id</span></span>|
|<span data-ttu-id="1e693-168">accountName</span><span class="sxs-lookup"><span data-stu-id="1e693-168">accountName</span></span>|<span data-ttu-id="1e693-169">string</span><span class="sxs-lookup"><span data-stu-id="1e693-169">string</span></span> |<span data-ttu-id="1e693-170">계정 이름</span><span class="sxs-lookup"><span data-stu-id="1e693-170">The Account Name</span></span>|
|<span data-ttu-id="1e693-171">accountOwnerId</span><span class="sxs-lookup"><span data-stu-id="1e693-171">accountOwnerId</span></span>|<span data-ttu-id="1e693-172">string</span><span class="sxs-lookup"><span data-stu-id="1e693-172">string</span></span>|<span data-ttu-id="1e693-173">계정 소유자 ID</span><span class="sxs-lookup"><span data-stu-id="1e693-173">The Account Owner Id</span></span>|
|<span data-ttu-id="1e693-174">departmentId</span><span class="sxs-lookup"><span data-stu-id="1e693-174">departmentId</span></span>|<span data-ttu-id="1e693-175">int</span><span class="sxs-lookup"><span data-stu-id="1e693-175">int</span></span>|<span data-ttu-id="1e693-176">부서 ID</span><span class="sxs-lookup"><span data-stu-id="1e693-176">The department Id</span></span>|
|<span data-ttu-id="1e693-177">departmentName</span><span class="sxs-lookup"><span data-stu-id="1e693-177">departmentName</span></span>|<span data-ttu-id="1e693-178">string</span><span class="sxs-lookup"><span data-stu-id="1e693-178">string</span></span>|<span data-ttu-id="1e693-179">부서 이름</span><span class="sxs-lookup"><span data-stu-id="1e693-179">The department name</span></span>|
|<span data-ttu-id="1e693-180">publisherName</span><span class="sxs-lookup"><span data-stu-id="1e693-180">publisherName</span></span>|<span data-ttu-id="1e693-181">string</span><span class="sxs-lookup"><span data-stu-id="1e693-181">string</span></span>|<span data-ttu-id="1e693-182">게시자 이름</span><span class="sxs-lookup"><span data-stu-id="1e693-182">The publisher name</span></span>|
|<span data-ttu-id="1e693-183">planName</span><span class="sxs-lookup"><span data-stu-id="1e693-183">planName</span></span>|<span data-ttu-id="1e693-184">string</span><span class="sxs-lookup"><span data-stu-id="1e693-184">string</span></span>|<span data-ttu-id="1e693-185">계획 이름</span><span class="sxs-lookup"><span data-stu-id="1e693-185">The Plan name</span></span>|
|<span data-ttu-id="1e693-186">consumedQuantity</span><span class="sxs-lookup"><span data-stu-id="1e693-186">consumedQuantity</span></span>|<span data-ttu-id="1e693-187">decimal</span><span class="sxs-lookup"><span data-stu-id="1e693-187">decimal</span></span>|<span data-ttu-id="1e693-188">이 기간 동안의 사용량</span><span class="sxs-lookup"><span data-stu-id="1e693-188">Consumed Quantity during this time period</span></span>|
|<span data-ttu-id="1e693-189">resourceRate</span><span class="sxs-lookup"><span data-stu-id="1e693-189">resourceRate</span></span>|<span data-ttu-id="1e693-190">decimal</span><span class="sxs-lookup"><span data-stu-id="1e693-190">decimal</span></span>|<span data-ttu-id="1e693-191">측정기의 단가</span><span class="sxs-lookup"><span data-stu-id="1e693-191">Unit price for the meter</span></span>|
|<span data-ttu-id="1e693-192">extendedCost</span><span class="sxs-lookup"><span data-stu-id="1e693-192">extendedCost</span></span>|<span data-ttu-id="1e693-193">decimal</span><span class="sxs-lookup"><span data-stu-id="1e693-193">decimal</span></span>|<span data-ttu-id="1e693-194">사용량 및 확장 비용에 따른 예상 요금</span><span class="sxs-lookup"><span data-stu-id="1e693-194">Estimated charge based on Consumed Quantity and Extended cost</span></span>|
<br/>
## <a name="see-also"></a><span data-ttu-id="1e693-195">참고 항목</span><span class="sxs-lookup"><span data-stu-id="1e693-195">See also</span></span>

* [<span data-ttu-id="1e693-196">청구 기간 API</span><span class="sxs-lookup"><span data-stu-id="1e693-196">Billing Periods API</span></span>](billing-enterprise-api-billing-periods.md)

* [<span data-ttu-id="1e693-197">사용량 세부 정보 API</span><span class="sxs-lookup"><span data-stu-id="1e693-197">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md) 

* [<span data-ttu-id="1e693-198">잔액 및 요약 API</span><span class="sxs-lookup"><span data-stu-id="1e693-198">Balance and Summary API</span></span>](billing-enterprise-api-balance-summary.md)

* [<span data-ttu-id="1e693-199">가격표 API</span><span class="sxs-lookup"><span data-stu-id="1e693-199">Price Sheet API</span></span>](billing-enterprise-api-pricesheet.md)
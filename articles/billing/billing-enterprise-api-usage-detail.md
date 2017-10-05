---
title: "Azure 청구 엔터프라이즈 API - 사용량 세부 정보 | Microsoft Docs"
description: "Azure 리소스 소비 및 추세에 대한 통찰력을 제공하는 데 사용되는 Azure 청구 사용량 및 RateCard API에 대한 자세한 정보를 제공합니다."
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
ms.openlocfilehash: 5b49220e6eb27544dba54255ee88c56ad79c3141
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="reporting-apis-for-enterprise-customers---usage-details"></a><span data-ttu-id="5137b-103">기업 고객을 위한 보고 API - 사용량 세부 정보</span><span class="sxs-lookup"><span data-stu-id="5137b-103">Reporting APIs for Enterprise customers - Usage Details</span></span>

<span data-ttu-id="5137b-104">사용량 세부 정보 API는 등록에 따른 사용량과 예상 요금 의 일별 분석 결과를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5137b-104">The Usage Detail API offers a daily breakdown of consumed quantities and estimated charges by an Enrollment.</span></span> <span data-ttu-id="5137b-105">이 결과에는 인스턴스, 측정기 및 부서에 대한 정보도 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5137b-105">The result also includes information on instances, meters and departments.</span></span> <span data-ttu-id="5137b-106">API는 청구 기간 또는 지정된 시작 날짜와 종료 날짜를 기준으로 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5137b-106">The API can be queried by Billing period or by a specified start and end date.</span></span> 
## <a name="consumption-apis"></a><span data-ttu-id="5137b-107">사용량 API</span><span class="sxs-lookup"><span data-stu-id="5137b-107">Consumption APIs</span></span>


##<a name="request"></a><span data-ttu-id="5137b-108">요청</span><span class="sxs-lookup"><span data-stu-id="5137b-108">Request</span></span> 
<span data-ttu-id="5137b-109">추가해야 할 공통 헤더 속성은 [여기](billing-enterprise-api.md)에 지정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5137b-109">Common header properties that need to be added are specified [here](billing-enterprise-api.md).</span></span> <span data-ttu-id="5137b-110">청구 기간을 지정하지 않으면 현재 청구 기간에 대한 데이터가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="5137b-110">If a billing period is not specified, then data for the current billing period is returned.</span></span> <span data-ttu-id="5137b-111">사용자 지정 시간 범위는 yyyy-MM-dd 형식의 시작 날짜 및 종료 날짜 매개 변수로 지정할 수 있으며,</span><span class="sxs-lookup"><span data-stu-id="5137b-111">Custom time ranges can be specified with the start and end date parameters that are in the format yyyy-MM-dd.</span></span> <span data-ttu-id="5137b-112">지원되는 최대 시간 범위는 36개월입니다.</span><span class="sxs-lookup"><span data-stu-id="5137b-112">The maximum supported time range is 36 months.</span></span>  

|<span data-ttu-id="5137b-113">메서드</span><span class="sxs-lookup"><span data-stu-id="5137b-113">Method</span></span> | <span data-ttu-id="5137b-114">요청 URI</span><span class="sxs-lookup"><span data-stu-id="5137b-114">Request URI</span></span>|
|-|-|
|<span data-ttu-id="5137b-115">GET</span><span class="sxs-lookup"><span data-stu-id="5137b-115">GET</span></span>|<span data-ttu-id="5137b-116">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/usagedetails</span><span class="sxs-lookup"><span data-stu-id="5137b-116">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/usagedetails</span></span> 
|<span data-ttu-id="5137b-117">GET</span><span class="sxs-lookup"><span data-stu-id="5137b-117">GET</span></span>|<span data-ttu-id="5137b-118">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/usagedetails</span><span class="sxs-lookup"><span data-stu-id="5137b-118">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/usagedetails</span></span>|
|<span data-ttu-id="5137b-119">GET</span><span class="sxs-lookup"><span data-stu-id="5137b-119">GET</span></span>|<span data-ttu-id="5137b-120">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/usagedetailsbycustomdate?startTime=2017-01-01&endTime=2017-01-10</span><span class="sxs-lookup"><span data-stu-id="5137b-120">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/usagedetailsbycustomdate?startTime=2017-01-01&endTime=2017-01-10</span></span>|

> [!Note]
> <span data-ttu-id="5137b-121">API의 미리 보기 버전을 사용하려면 위 URL에서 v2를 v1로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="5137b-121">To use the preview version of API, replace v2 with v1 in the above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="5137b-122">응답</span><span class="sxs-lookup"><span data-stu-id="5137b-122">Response</span></span>

> <span data-ttu-id="5137b-123">잠재적으로 많은 양의 데이터로 인해 결과 집합이 페이징됩니다.</span><span class="sxs-lookup"><span data-stu-id="5137b-123">Due to the potentially large volume of data the result set is paged.</span></span> <span data-ttu-id="5137b-124">nextLink 속성(있는 경우)은 데이터의 다음 페이지에 대한 링크를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5137b-124">The nextLink property, if present, specifies the link for the next page of data.</span></span> <span data-ttu-id="5137b-125">링크가 비어 있으면 이 링크가 마지막 페이지임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="5137b-125">If the link is empty, it denotes that is the last page.</span></span> 
<br/>

    {
        "id": "string",
        "data": [
            {                       
            "accountId": 0,
            "productId": 0,
            "resourceLocationId": 0,
            "consumedServiceId": 0,
            "departmentId": 0,
            "accountOwnerEmail": "string",
            "accountName": "string",
            "serviceAdministratorId": "string",
            "subscriptionId": 0,
            "subscriptionGuid": "string",
            "subscriptionName": "string",
            "date": "2017-04-27T23:01:43.799Z",
            "product": "string",
            "meterId": "string",
            "meterCategory": "string",
            "meterSubCategory": "string",
            "meterRegion": "string",
            "meterName": "string",
            "consumedQuantity": 0,
            "resourceRate": 0,
            "Cost": 0,
            "resourceLocation": "string",
            "consumedService": "string",
            "instanceId": "string",
            "serviceInfo1": "string",
            "serviceInfo2": "string",
            "additionalInfo": "string",
            "tags": "string",
            "storeServiceIdentifier": "string",
            "departmentName": "string",
            "costCenter": "string",
            "unitOfMeasure": "string",
            "resourceGroup": "string"
            }
        ],
        "nextLink": "string"
    }

<br/><span data-ttu-id="5137b-126">
**응답 속성 정의**</span><span class="sxs-lookup"><span data-stu-id="5137b-126">
**Response property definitions**</span></span>

|<span data-ttu-id="5137b-127">속성 이름</span><span class="sxs-lookup"><span data-stu-id="5137b-127">Property Name</span></span>| <span data-ttu-id="5137b-128">형식</span><span class="sxs-lookup"><span data-stu-id="5137b-128">Type</span></span>| <span data-ttu-id="5137b-129">설명</span><span class="sxs-lookup"><span data-stu-id="5137b-129">Description</span></span>
|-|-|-|
|<span data-ttu-id="5137b-130">id</span><span class="sxs-lookup"><span data-stu-id="5137b-130">id</span></span>| <span data-ttu-id="5137b-131">string</span><span class="sxs-lookup"><span data-stu-id="5137b-131">string</span></span>| <span data-ttu-id="5137b-132">API 호출의 고유 ID</span><span class="sxs-lookup"><span data-stu-id="5137b-132">The unique Id for the API call.</span></span> |
|<span data-ttu-id="5137b-133">데이터</span><span class="sxs-lookup"><span data-stu-id="5137b-133">data</span></span>| <span data-ttu-id="5137b-134">JSON 배열</span><span class="sxs-lookup"><span data-stu-id="5137b-134">JSON array</span></span>| <span data-ttu-id="5137b-135">모든 인스턴스/측정기에 대한 일별 사용량 세부 정보의 배열</span><span class="sxs-lookup"><span data-stu-id="5137b-135">The Array of daily usage details for every instance\meter.</span></span>|
|<span data-ttu-id="5137b-136">nextLink</span><span class="sxs-lookup"><span data-stu-id="5137b-136">nextLink</span></span>| <span data-ttu-id="5137b-137">string</span><span class="sxs-lookup"><span data-stu-id="5137b-137">string</span></span>| <span data-ttu-id="5137b-138">더 많은 데이터 페이지가 있으면 nextLink에서 다음 데이터 페이지를 반환하는 URL을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="5137b-138">When there are more pages of data the nextLink points to the URL to return the next page of data.</span></span> |
|<span data-ttu-id="5137b-139">accountId</span><span class="sxs-lookup"><span data-stu-id="5137b-139">accountId</span></span>| <span data-ttu-id="5137b-140">int</span><span class="sxs-lookup"><span data-stu-id="5137b-140">int</span></span>| <span data-ttu-id="5137b-141">사용되지 않는 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="5137b-141">Obsolete field.</span></span> <span data-ttu-id="5137b-142">이전 버전과의 호환성을 위해 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="5137b-142">Present for backward compatibility.</span></span> |
|<span data-ttu-id="5137b-143">productId</span><span class="sxs-lookup"><span data-stu-id="5137b-143">productId</span></span>| <span data-ttu-id="5137b-144">int</span><span class="sxs-lookup"><span data-stu-id="5137b-144">int</span></span>| <span data-ttu-id="5137b-145">사용되지 않는 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="5137b-145">Obsolete field.</span></span> <span data-ttu-id="5137b-146">이전 버전과의 호환성을 위해 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="5137b-146">Present for backward compatibility.</span></span> |
|<span data-ttu-id="5137b-147">resourceLocationId</span><span class="sxs-lookup"><span data-stu-id="5137b-147">resourceLocationId</span></span>| <span data-ttu-id="5137b-148">int</span><span class="sxs-lookup"><span data-stu-id="5137b-148">int</span></span>| <span data-ttu-id="5137b-149">사용되지 않는 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="5137b-149">Obsolete field.</span></span> <span data-ttu-id="5137b-150">이전 버전과의 호환성을 위해 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="5137b-150">Present for backward compatibility.</span></span> |
|<span data-ttu-id="5137b-151">consumedServiceID</span><span class="sxs-lookup"><span data-stu-id="5137b-151">consumedServiceID</span></span>| <span data-ttu-id="5137b-152">int</span><span class="sxs-lookup"><span data-stu-id="5137b-152">int</span></span>| <span data-ttu-id="5137b-153">사용되지 않는 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="5137b-153">Obsolete field.</span></span> <span data-ttu-id="5137b-154">이전 버전과의 호환성을 위해 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="5137b-154">Present for backward compatibility.</span></span> |
|<span data-ttu-id="5137b-155">departmentId</span><span class="sxs-lookup"><span data-stu-id="5137b-155">departmentId</span></span>| <span data-ttu-id="5137b-156">int</span><span class="sxs-lookup"><span data-stu-id="5137b-156">int</span></span>| <span data-ttu-id="5137b-157">사용되지 않는 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="5137b-157">Obsolete field.</span></span> <span data-ttu-id="5137b-158">이전 버전과의 호환성을 위해 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="5137b-158">Present for backward compatibility.</span></span> |
|<span data-ttu-id="5137b-159">accountOwnerEmail</span><span class="sxs-lookup"><span data-stu-id="5137b-159">accountOwnerEmail</span></span>| <span data-ttu-id="5137b-160">string</span><span class="sxs-lookup"><span data-stu-id="5137b-160">string</span></span>| <span data-ttu-id="5137b-161">계정 소유자의 전자 메일 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="5137b-161">Email account of the account owner.</span></span> |
|<span data-ttu-id="5137b-162">accountName</span><span class="sxs-lookup"><span data-stu-id="5137b-162">accountName</span></span>| <span data-ttu-id="5137b-163">string</span><span class="sxs-lookup"><span data-stu-id="5137b-163">string</span></span>| <span data-ttu-id="5137b-164">계정의 이름을 입력한 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="5137b-164">Customer entered name of the account.</span></span> |
|<span data-ttu-id="5137b-165">serviceAdministratorId</span><span class="sxs-lookup"><span data-stu-id="5137b-165">serviceAdministratorId</span></span>| <span data-ttu-id="5137b-166">string</span><span class="sxs-lookup"><span data-stu-id="5137b-166">string</span></span>| <span data-ttu-id="5137b-167">서비스 관리자의 전자 메일 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="5137b-167">Email Address of Service Administrator.</span></span> |
|<span data-ttu-id="5137b-168">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="5137b-168">subscriptionId</span></span>| <span data-ttu-id="5137b-169">int</span><span class="sxs-lookup"><span data-stu-id="5137b-169">int</span></span>| <span data-ttu-id="5137b-170">사용되지 않는 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="5137b-170">Obsolete field.</span></span> <span data-ttu-id="5137b-171">이전 버전과의 호환성을 위해 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="5137b-171">Present for backward compatibility.</span></span> |
|<span data-ttu-id="5137b-172">subscriptionGuid</span><span class="sxs-lookup"><span data-stu-id="5137b-172">subscriptionGuid</span></span>| <span data-ttu-id="5137b-173">string</span><span class="sxs-lookup"><span data-stu-id="5137b-173">string</span></span>| <span data-ttu-id="5137b-174">구독의 전역 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="5137b-174">Global Unique Identifier for the subscription.</span></span> |
|<span data-ttu-id="5137b-175">subscriptionName</span><span class="sxs-lookup"><span data-stu-id="5137b-175">subscriptionName</span></span>| <span data-ttu-id="5137b-176">string</span><span class="sxs-lookup"><span data-stu-id="5137b-176">string</span></span>| <span data-ttu-id="5137b-177">구독의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5137b-177">Name of the subscription.</span></span> |
|<span data-ttu-id="5137b-178">date</span><span class="sxs-lookup"><span data-stu-id="5137b-178">date</span></span>| <span data-ttu-id="5137b-179">string</span><span class="sxs-lookup"><span data-stu-id="5137b-179">string</span></span>| <span data-ttu-id="5137b-180">소비가 발생한 날짜입니다.</span><span class="sxs-lookup"><span data-stu-id="5137b-180">The date on which consumption occurred.</span></span> |
|<span data-ttu-id="5137b-181">product</span><span class="sxs-lookup"><span data-stu-id="5137b-181">product</span></span>| <span data-ttu-id="5137b-182">string</span><span class="sxs-lookup"><span data-stu-id="5137b-182">string</span></span>| <span data-ttu-id="5137b-183">측정기에 대한 추가 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="5137b-183">Additional details on the meter.</span></span> <span data-ttu-id="5137b-184">예: A1(VM)Windows - 아시아 태평양 동부</span><span class="sxs-lookup"><span data-stu-id="5137b-184">Example: A1(VM)Windows - AP East</span></span>|
|<span data-ttu-id="5137b-185">meterId</span><span class="sxs-lookup"><span data-stu-id="5137b-185">meterId</span></span>| <span data-ttu-id="5137b-186">string</span><span class="sxs-lookup"><span data-stu-id="5137b-186">string</span></span>| <span data-ttu-id="5137b-187">사용량을 내보낸 측정기의 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="5137b-187">The identifier for the meter which emitted usage.</span></span> |
|<span data-ttu-id="5137b-188">meterCategory</span><span class="sxs-lookup"><span data-stu-id="5137b-188">meterCategory</span></span>| <span data-ttu-id="5137b-189">string</span><span class="sxs-lookup"><span data-stu-id="5137b-189">string</span></span>| <span data-ttu-id="5137b-190">사용된 Azure 플랫폼 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="5137b-190">The Azure platform service that was used.</span></span> |
|<span data-ttu-id="5137b-191">meterSubCategory</span><span class="sxs-lookup"><span data-stu-id="5137b-191">meterSubCategory</span></span>| <span data-ttu-id="5137b-192">string</span><span class="sxs-lookup"><span data-stu-id="5137b-192">string</span></span>| <span data-ttu-id="5137b-193">요율에 영향을 줄 수 있는 Azure 서비스 유형을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="5137b-193">Defines the Azure service type that can affect the rate.</span></span> <span data-ttu-id="5137b-194">예: A1 VM(Windows 외)</span><span class="sxs-lookup"><span data-stu-id="5137b-194">Example: A1 VM (Non-Windows</span></span>|
|<span data-ttu-id="5137b-195">meterRegion</span><span class="sxs-lookup"><span data-stu-id="5137b-195">meterRegion</span></span>| <span data-ttu-id="5137b-196">string</span><span class="sxs-lookup"><span data-stu-id="5137b-196">string</span></span>| <span data-ttu-id="5137b-197">데이터 센터 위치에 따라 가격이 책정되는 특정 서비스에 대한 데이터 센터의 위치를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="5137b-197">Identifies the location of the datacenter for certain services that are priced based on datacenter location.</span></span> |
|<span data-ttu-id="5137b-198">meterName</span><span class="sxs-lookup"><span data-stu-id="5137b-198">meterName</span></span>| <span data-ttu-id="5137b-199">string</span><span class="sxs-lookup"><span data-stu-id="5137b-199">string</span></span>| <span data-ttu-id="5137b-200">측정기의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5137b-200">Name of the meter.</span></span> |
|<span data-ttu-id="5137b-201">consumedQuantity</span><span class="sxs-lookup"><span data-stu-id="5137b-201">consumedQuantity</span></span>| <span data-ttu-id="5137b-202">double</span><span class="sxs-lookup"><span data-stu-id="5137b-202">double</span></span>| <span data-ttu-id="5137b-203">사용된 측정기의 양입니다.</span><span class="sxs-lookup"><span data-stu-id="5137b-203">The amount of the meter that has been consumed.</span></span> |
|<span data-ttu-id="5137b-204">resourceRate</span><span class="sxs-lookup"><span data-stu-id="5137b-204">resourceRate</span></span>| <span data-ttu-id="5137b-205">double</span><span class="sxs-lookup"><span data-stu-id="5137b-205">double</span></span>| <span data-ttu-id="5137b-206">청구 가능 단위당 해당되는 속도입니다.</span><span class="sxs-lookup"><span data-stu-id="5137b-206">The rate applicable per billable unit.</span></span> |
|<span data-ttu-id="5137b-207">cost</span><span class="sxs-lookup"><span data-stu-id="5137b-207">cost</span></span>| <span data-ttu-id="5137b-208">double</span><span class="sxs-lookup"><span data-stu-id="5137b-208">double</span></span>| <span data-ttu-id="5137b-209">측정기에 대해 발생한 요금입니다.</span><span class="sxs-lookup"><span data-stu-id="5137b-209">The charge that has been incurred for the meter.</span></span> |
|<span data-ttu-id="5137b-210">resourceLocation</span><span class="sxs-lookup"><span data-stu-id="5137b-210">resourceLocation</span></span>| <span data-ttu-id="5137b-211">string</span><span class="sxs-lookup"><span data-stu-id="5137b-211">string</span></span>| <span data-ttu-id="5137b-212">측정기가 실행되고 있는 데이터 센터를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="5137b-212">Identifies the datacenter where the meter is running.</span></span> |
|<span data-ttu-id="5137b-213">consumedService</span><span class="sxs-lookup"><span data-stu-id="5137b-213">consumedService</span></span>| <span data-ttu-id="5137b-214">string</span><span class="sxs-lookup"><span data-stu-id="5137b-214">string</span></span>| <span data-ttu-id="5137b-215">사용된 Azure 플랫폼 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="5137b-215">The Azure platform service that was used.</span></span> |
|<span data-ttu-id="5137b-216">instanceId</span><span class="sxs-lookup"><span data-stu-id="5137b-216">instanceId</span></span>| <span data-ttu-id="5137b-217">string</span><span class="sxs-lookup"><span data-stu-id="5137b-217">string</span></span>| <span data-ttu-id="5137b-218">이 식별자는 리소스의 이름 또는 정규화된 리소스 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="5137b-218">This identifier is the name of the resource or the fully qualified Resource ID.</span></span> <span data-ttu-id="5137b-219">자세한 내용은 [Azure Resource Manager API](https://docs.microsoft.com/rest/api/resources/resources)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5137b-219">For more information, see [Azure Resource Manager API](https://docs.microsoft.com/rest/api/resources/resources)</span></span> |
|<span data-ttu-id="5137b-220">serviceInfo1</span><span class="sxs-lookup"><span data-stu-id="5137b-220">serviceInfo1</span></span>| <span data-ttu-id="5137b-221">string</span><span class="sxs-lookup"><span data-stu-id="5137b-221">string</span></span>| <span data-ttu-id="5137b-222">내부 Azure 서비스 메타데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="5137b-222">Internal Azure Service Metadata.</span></span> |
|<span data-ttu-id="5137b-223">serviceInfo2</span><span class="sxs-lookup"><span data-stu-id="5137b-223">serviceInfo2</span></span>| <span data-ttu-id="5137b-224">string</span><span class="sxs-lookup"><span data-stu-id="5137b-224">string</span></span>| <span data-ttu-id="5137b-225">예를 들어, 가상 컴퓨터의 이미지 형식 및 ExpressRoute의 ISP 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5137b-225">For example, an image type for a virtual machine and ISP name for ExpressRoute.</span></span> |
|<span data-ttu-id="5137b-226">additionalInfo</span><span class="sxs-lookup"><span data-stu-id="5137b-226">additionalInfo</span></span>| <span data-ttu-id="5137b-227">string</span><span class="sxs-lookup"><span data-stu-id="5137b-227">string</span></span>| <span data-ttu-id="5137b-228">서비스 특정 메타데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="5137b-228">Service-specific metadata.</span></span> <span data-ttu-id="5137b-229">예를 들어 가상 컴퓨터용 이미지 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="5137b-229">For example, an image type for a virtual machine.</span></span> |
|<span data-ttu-id="5137b-230">tags</span><span class="sxs-lookup"><span data-stu-id="5137b-230">tags</span></span>| <span data-ttu-id="5137b-231">string</span><span class="sxs-lookup"><span data-stu-id="5137b-231">string</span></span>| <span data-ttu-id="5137b-232">태그를 추가한 고객입니다.</span><span class="sxs-lookup"><span data-stu-id="5137b-232">Customer added tags.</span></span> <span data-ttu-id="5137b-233">자세한 내용은 [태그를 사용하여 Azure 리소스 구성](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-using-tags)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5137b-233">For more information, see [Organize your Azure resources with tags](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-using-tags).</span></span> |
|<span data-ttu-id="5137b-234">storeServiceIdentifier</span><span class="sxs-lookup"><span data-stu-id="5137b-234">storeServiceIdentifier</span></span>| <span data-ttu-id="5137b-235">string</span><span class="sxs-lookup"><span data-stu-id="5137b-235">string</span></span>| <span data-ttu-id="5137b-236">이 열이 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5137b-236">This columns is not used.</span></span> <span data-ttu-id="5137b-237">이전 버전과의 호환성을 위해 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="5137b-237">Present for backward compatibility.</span></span> |
|<span data-ttu-id="5137b-238">departmentName</span><span class="sxs-lookup"><span data-stu-id="5137b-238">departmentName</span></span>| <span data-ttu-id="5137b-239">string</span><span class="sxs-lookup"><span data-stu-id="5137b-239">string</span></span>| <span data-ttu-id="5137b-240">부서 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5137b-240">Name of the department.</span></span> |
|<span data-ttu-id="5137b-241">costCenter</span><span class="sxs-lookup"><span data-stu-id="5137b-241">costCenter</span></span>| <span data-ttu-id="5137b-242">string</span><span class="sxs-lookup"><span data-stu-id="5137b-242">string</span></span>| <span data-ttu-id="5137b-243">사용량이 연결된 비용 센터입니다.</span><span class="sxs-lookup"><span data-stu-id="5137b-243">The cost center that the usage is associated with.</span></span> |
|<span data-ttu-id="5137b-244">unitOfMeasure</span><span class="sxs-lookup"><span data-stu-id="5137b-244">unitOfMeasure</span></span>| <span data-ttu-id="5137b-245">string</span><span class="sxs-lookup"><span data-stu-id="5137b-245">string</span></span>| <span data-ttu-id="5137b-246">서비스 요금이 청구되는 단위를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="5137b-246">Identifies the unit that the service is charged in.</span></span> <span data-ttu-id="5137b-247">예: GB, 시간, 10,000초</span><span class="sxs-lookup"><span data-stu-id="5137b-247">Example: GB, hours, 10,000 s.</span></span> |
|<span data-ttu-id="5137b-248">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="5137b-248">resourceGroup</span></span>| <span data-ttu-id="5137b-249">string</span><span class="sxs-lookup"><span data-stu-id="5137b-249">string</span></span>| <span data-ttu-id="5137b-250">배포된 측정기가 실행되는 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="5137b-250">The resource group in which the deployed meter is running in.</span></span> <span data-ttu-id="5137b-251">자세한 내용은 [Azure Resource Manager 개요](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5137b-251">For more information, see [Azure Resource Manager overview](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview).</span></span> |
<br/>
## <a name="see-also"></a><span data-ttu-id="5137b-252">참고 항목</span><span class="sxs-lookup"><span data-stu-id="5137b-252">See also</span></span>

* [<span data-ttu-id="5137b-253">청구 기간 API</span><span class="sxs-lookup"><span data-stu-id="5137b-253">Billing Periods API</span></span>](billing-enterprise-api-billing-periods.md)

* [<span data-ttu-id="5137b-254">잔액 및 요약 API</span><span class="sxs-lookup"><span data-stu-id="5137b-254">Balance and Summary API</span></span>](billing-enterprise-api-balance-summary.md)

* [<span data-ttu-id="5137b-255">Marketplace 저장소 요금 API</span><span class="sxs-lookup"><span data-stu-id="5137b-255">Marketplace Store Charge API</span></span>](billing-enterprise-api-marketplace-storecharge.md) 

* [<span data-ttu-id="5137b-256">가격표 API</span><span class="sxs-lookup"><span data-stu-id="5137b-256">Price Sheet API</span></span>](billing-enterprise-api-pricesheet.md)

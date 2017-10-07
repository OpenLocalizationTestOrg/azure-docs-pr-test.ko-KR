---
title: "aaaAzure 청구 엔터프라이즈 Api-사용량 세부 정보 | Microsoft Docs"
description: "Azure 리소스 소비 및 추세에 대 한 tooprovide 사용 되는 정보는 Azure 청구 사용량 및 RateCard Api에 알아봅니다."
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
ms.openlocfilehash: def0805008261df5872f015db3d2b26e47d25569
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---usage-details"></a><span data-ttu-id="00486-103">기업 고객을 위한 보고 API - 사용량 세부 정보</span><span class="sxs-lookup"><span data-stu-id="00486-103">Reporting APIs for Enterprise customers - Usage Details</span></span>

<span data-ttu-id="00486-104">사용 현황 세부 API hello 소비 된 수량 및 등록 하 여 예상된 요금 일별로 구분을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-104">hello Usage Detail API offers a daily breakdown of consumed quantities and estimated charges by an Enrollment.</span></span> <span data-ttu-id="00486-105">hello 결과는 인스턴스, 측정 단위 및 부서에 대 한 정보 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00486-105">hello result also includes information on instances, meters and departments.</span></span> <span data-ttu-id="00486-106">지정 된 시작 및 종료 날짜 또는 청구 기간에 의해 hello API를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00486-106">hello API can be queried by Billing period or by a specified start and end date.</span></span> 
## <a name="consumption-apis"></a><span data-ttu-id="00486-107">사용량 API</span><span class="sxs-lookup"><span data-stu-id="00486-107">Consumption APIs</span></span>


##<a name="request"></a><span data-ttu-id="00486-108">요청</span><span class="sxs-lookup"><span data-stu-id="00486-108">Request</span></span> 
<span data-ttu-id="00486-109">Toobe 추가 해야 하는 공통 헤더 속성이 지정 되어 [여기](billing-enterprise-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-109">Common header properties that need toobe added are specified [here](billing-enterprise-api.md).</span></span> <span data-ttu-id="00486-110">청구 기간 지정 하지 않으면 다음 hello 현재 청구에 대 한 데이터 기간 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00486-110">If a billing period is not specified, then data for hello current billing period is returned.</span></span> <span data-ttu-id="00486-111">사용자가 지정한 시간 범위 hello 시작 되 면 지정할 수 있습니다 및 종료 날짜의에서 매개 변수를 hello 형식 yyyy.</span><span class="sxs-lookup"><span data-stu-id="00486-111">Custom time ranges can be specified with hello start and end date parameters that are in hello format yyyy-MM-dd.</span></span> <span data-ttu-id="00486-112">hello 지원 되는 최대 시간 범위는 36 개월입니다.</span><span class="sxs-lookup"><span data-stu-id="00486-112">hello maximum supported time range is 36 months.</span></span>  

|<span data-ttu-id="00486-113">메서드</span><span class="sxs-lookup"><span data-stu-id="00486-113">Method</span></span> | <span data-ttu-id="00486-114">요청 URI</span><span class="sxs-lookup"><span data-stu-id="00486-114">Request URI</span></span>|
|-|-|
|<span data-ttu-id="00486-115">GET</span><span class="sxs-lookup"><span data-stu-id="00486-115">GET</span></span>|<span data-ttu-id="00486-116">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/usagedetails</span><span class="sxs-lookup"><span data-stu-id="00486-116">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/usagedetails</span></span> 
|<span data-ttu-id="00486-117">GET</span><span class="sxs-lookup"><span data-stu-id="00486-117">GET</span></span>|<span data-ttu-id="00486-118">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/usagedetails</span><span class="sxs-lookup"><span data-stu-id="00486-118">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/usagedetails</span></span>|
|<span data-ttu-id="00486-119">GET</span><span class="sxs-lookup"><span data-stu-id="00486-119">GET</span></span>|<span data-ttu-id="00486-120">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/usagedetailsbycustomdate?startTime=2017-01-01&endTime=2017-01-10</span><span class="sxs-lookup"><span data-stu-id="00486-120">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/usagedetailsbycustomdate?startTime=2017-01-01&endTime=2017-01-10</span></span>|

> [!Note]
> <span data-ttu-id="00486-121">toouse hello 미리 보기 버전의 API, URL 위에 hello v1 v2를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-121">toouse hello preview version of API, replace v2 with v1 in hello above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="00486-122">응답</span><span class="sxs-lookup"><span data-stu-id="00486-122">Response</span></span>

> <span data-ttu-id="00486-123">Toohello 잠재적으로 많은 양의 데이터 hello 결과 인해 집합이 페이징 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00486-123">Due toohello potentially large volume of data hello result set is paged.</span></span> <span data-ttu-id="00486-124">hello nextLink 속성이 있는 경우 데이터의 다음 페이지 hello에 대 한 hello 링크를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-124">hello nextLink property, if present, specifies hello link for hello next page of data.</span></span> <span data-ttu-id="00486-125">Hello 링크 비어 있으면 즉 hello 마지막 페이지를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="00486-125">If hello link is empty, it denotes that is hello last page.</span></span> 
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

<br/><span data-ttu-id="00486-126">
**응답 속성 정의**</span><span class="sxs-lookup"><span data-stu-id="00486-126">
**Response property definitions**</span></span>

|<span data-ttu-id="00486-127">속성 이름</span><span class="sxs-lookup"><span data-stu-id="00486-127">Property Name</span></span>| <span data-ttu-id="00486-128">형식</span><span class="sxs-lookup"><span data-stu-id="00486-128">Type</span></span>| <span data-ttu-id="00486-129">설명</span><span class="sxs-lookup"><span data-stu-id="00486-129">Description</span></span>
|-|-|-|
|<span data-ttu-id="00486-130">id</span><span class="sxs-lookup"><span data-stu-id="00486-130">id</span></span>| <span data-ttu-id="00486-131">string</span><span class="sxs-lookup"><span data-stu-id="00486-131">string</span></span>| <span data-ttu-id="00486-132">hello hello API 호출에 대 한 고유 Id입니다.</span><span class="sxs-lookup"><span data-stu-id="00486-132">hello unique Id for hello API call.</span></span> |
|<span data-ttu-id="00486-133">데이터</span><span class="sxs-lookup"><span data-stu-id="00486-133">data</span></span>| <span data-ttu-id="00486-134">JSON 배열</span><span class="sxs-lookup"><span data-stu-id="00486-134">JSON array</span></span>| <span data-ttu-id="00486-135">hello 모든 instance\meter에 대 한 사용 정보를 매일의 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="00486-135">hello Array of daily usage details for every instance\meter.</span></span>|
|<span data-ttu-id="00486-136">nextLink</span><span class="sxs-lookup"><span data-stu-id="00486-136">nextLink</span></span>| <span data-ttu-id="00486-137">string</span><span class="sxs-lookup"><span data-stu-id="00486-137">string</span></span>| <span data-ttu-id="00486-138">페이지 데이터 hello nextLink 포인트 toohello URL tooreturn hello 다음 데이터 페이지를 더 많이 있는 경우.</span><span class="sxs-lookup"><span data-stu-id="00486-138">When there are more pages of data hello nextLink points toohello URL tooreturn hello next page of data.</span></span> |
|<span data-ttu-id="00486-139">accountId</span><span class="sxs-lookup"><span data-stu-id="00486-139">accountId</span></span>| <span data-ttu-id="00486-140">int</span><span class="sxs-lookup"><span data-stu-id="00486-140">int</span></span>| <span data-ttu-id="00486-141">사용되지 않는 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="00486-141">Obsolete field.</span></span> <span data-ttu-id="00486-142">이전 버전과의 호환성을 위해 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-142">Present for backward compatibility.</span></span> |
|<span data-ttu-id="00486-143">productId</span><span class="sxs-lookup"><span data-stu-id="00486-143">productId</span></span>| <span data-ttu-id="00486-144">int</span><span class="sxs-lookup"><span data-stu-id="00486-144">int</span></span>| <span data-ttu-id="00486-145">사용되지 않는 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="00486-145">Obsolete field.</span></span> <span data-ttu-id="00486-146">이전 버전과의 호환성을 위해 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-146">Present for backward compatibility.</span></span> |
|<span data-ttu-id="00486-147">resourceLocationId</span><span class="sxs-lookup"><span data-stu-id="00486-147">resourceLocationId</span></span>| <span data-ttu-id="00486-148">int</span><span class="sxs-lookup"><span data-stu-id="00486-148">int</span></span>| <span data-ttu-id="00486-149">사용되지 않는 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="00486-149">Obsolete field.</span></span> <span data-ttu-id="00486-150">이전 버전과의 호환성을 위해 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-150">Present for backward compatibility.</span></span> |
|<span data-ttu-id="00486-151">consumedServiceID</span><span class="sxs-lookup"><span data-stu-id="00486-151">consumedServiceID</span></span>| <span data-ttu-id="00486-152">int</span><span class="sxs-lookup"><span data-stu-id="00486-152">int</span></span>| <span data-ttu-id="00486-153">사용되지 않는 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="00486-153">Obsolete field.</span></span> <span data-ttu-id="00486-154">이전 버전과의 호환성을 위해 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-154">Present for backward compatibility.</span></span> |
|<span data-ttu-id="00486-155">departmentId</span><span class="sxs-lookup"><span data-stu-id="00486-155">departmentId</span></span>| <span data-ttu-id="00486-156">int</span><span class="sxs-lookup"><span data-stu-id="00486-156">int</span></span>| <span data-ttu-id="00486-157">사용되지 않는 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="00486-157">Obsolete field.</span></span> <span data-ttu-id="00486-158">이전 버전과의 호환성을 위해 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-158">Present for backward compatibility.</span></span> |
|<span data-ttu-id="00486-159">accountOwnerEmail</span><span class="sxs-lookup"><span data-stu-id="00486-159">accountOwnerEmail</span></span>| <span data-ttu-id="00486-160">string</span><span class="sxs-lookup"><span data-stu-id="00486-160">string</span></span>| <span data-ttu-id="00486-161">Hello 계정 소유자의 전자 메일 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="00486-161">Email account of hello account owner.</span></span> |
|<span data-ttu-id="00486-162">accountName</span><span class="sxs-lookup"><span data-stu-id="00486-162">accountName</span></span>| <span data-ttu-id="00486-163">string</span><span class="sxs-lookup"><span data-stu-id="00486-163">string</span></span>| <span data-ttu-id="00486-164">입력 한 고객 이름 hello 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="00486-164">Customer entered name of hello account.</span></span> |
|<span data-ttu-id="00486-165">serviceAdministratorId</span><span class="sxs-lookup"><span data-stu-id="00486-165">serviceAdministratorId</span></span>| <span data-ttu-id="00486-166">string</span><span class="sxs-lookup"><span data-stu-id="00486-166">string</span></span>| <span data-ttu-id="00486-167">서비스 관리자의 전자 메일 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="00486-167">Email Address of Service Administrator.</span></span> |
|<span data-ttu-id="00486-168">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="00486-168">subscriptionId</span></span>| <span data-ttu-id="00486-169">int</span><span class="sxs-lookup"><span data-stu-id="00486-169">int</span></span>| <span data-ttu-id="00486-170">사용되지 않는 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="00486-170">Obsolete field.</span></span> <span data-ttu-id="00486-171">이전 버전과의 호환성을 위해 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-171">Present for backward compatibility.</span></span> |
|<span data-ttu-id="00486-172">subscriptionGuid</span><span class="sxs-lookup"><span data-stu-id="00486-172">subscriptionGuid</span></span>| <span data-ttu-id="00486-173">string</span><span class="sxs-lookup"><span data-stu-id="00486-173">string</span></span>| <span data-ttu-id="00486-174">Hello 구독에 대 한 전역 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="00486-174">Global Unique Identifier for hello subscription.</span></span> |
|<span data-ttu-id="00486-175">subscriptionName</span><span class="sxs-lookup"><span data-stu-id="00486-175">subscriptionName</span></span>| <span data-ttu-id="00486-176">string</span><span class="sxs-lookup"><span data-stu-id="00486-176">string</span></span>| <span data-ttu-id="00486-177">Hello 구독의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="00486-177">Name of hello subscription.</span></span> |
|<span data-ttu-id="00486-178">date</span><span class="sxs-lookup"><span data-stu-id="00486-178">date</span></span>| <span data-ttu-id="00486-179">string</span><span class="sxs-lookup"><span data-stu-id="00486-179">string</span></span>| <span data-ttu-id="00486-180">hello 날짜 소비 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="00486-180">hello date on which consumption occurred.</span></span> |
|<span data-ttu-id="00486-181">product</span><span class="sxs-lookup"><span data-stu-id="00486-181">product</span></span>| <span data-ttu-id="00486-182">string</span><span class="sxs-lookup"><span data-stu-id="00486-182">string</span></span>| <span data-ttu-id="00486-183">Hello 수준에 추가 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="00486-183">Additional details on hello meter.</span></span> <span data-ttu-id="00486-184">예: A1(VM)Windows - 아시아 태평양 동부</span><span class="sxs-lookup"><span data-stu-id="00486-184">Example: A1(VM)Windows - AP East</span></span>|
|<span data-ttu-id="00486-185">meterId</span><span class="sxs-lookup"><span data-stu-id="00486-185">meterId</span></span>| <span data-ttu-id="00486-186">string</span><span class="sxs-lookup"><span data-stu-id="00486-186">string</span></span>| <span data-ttu-id="00486-187">hello 식별자 사용 내보내집니다는 hello 미터입니다.</span><span class="sxs-lookup"><span data-stu-id="00486-187">hello identifier for hello meter which emitted usage.</span></span> |
|<span data-ttu-id="00486-188">meterCategory</span><span class="sxs-lookup"><span data-stu-id="00486-188">meterCategory</span></span>| <span data-ttu-id="00486-189">string</span><span class="sxs-lookup"><span data-stu-id="00486-189">string</span></span>| <span data-ttu-id="00486-190">번호 사용 된 Azure 플랫폼 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="00486-190">hello Azure platform service that was used.</span></span> |
|<span data-ttu-id="00486-191">meterSubCategory</span><span class="sxs-lookup"><span data-stu-id="00486-191">meterSubCategory</span></span>| <span data-ttu-id="00486-192">string</span><span class="sxs-lookup"><span data-stu-id="00486-192">string</span></span>| <span data-ttu-id="00486-193">Hello 속도 영향을 줄 수 있는 hello Azure 서비스 유형을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-193">Defines hello Azure service type that can affect hello rate.</span></span> <span data-ttu-id="00486-194">예: A1 VM(Windows 외)</span><span class="sxs-lookup"><span data-stu-id="00486-194">Example: A1 VM (Non-Windows</span></span>|
|<span data-ttu-id="00486-195">meterRegion</span><span class="sxs-lookup"><span data-stu-id="00486-195">meterRegion</span></span>| <span data-ttu-id="00486-196">string</span><span class="sxs-lookup"><span data-stu-id="00486-196">string</span></span>| <span data-ttu-id="00486-197">데이터 센터 위치에 따라 가격이 책정 됩니다 하는 특정 서비스에 대 한 hello 데이터 센터의 hello 위치를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-197">Identifies hello location of hello datacenter for certain services that are priced based on datacenter location.</span></span> |
|<span data-ttu-id="00486-198">meterName</span><span class="sxs-lookup"><span data-stu-id="00486-198">meterName</span></span>| <span data-ttu-id="00486-199">string</span><span class="sxs-lookup"><span data-stu-id="00486-199">string</span></span>| <span data-ttu-id="00486-200">Hello 표시기의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="00486-200">Name of hello meter.</span></span> |
|<span data-ttu-id="00486-201">consumedQuantity</span><span class="sxs-lookup"><span data-stu-id="00486-201">consumedQuantity</span></span>| <span data-ttu-id="00486-202">double</span><span class="sxs-lookup"><span data-stu-id="00486-202">double</span></span>| <span data-ttu-id="00486-203">소비 된 hello 미터의 hello 양입니다.</span><span class="sxs-lookup"><span data-stu-id="00486-203">hello amount of hello meter that has been consumed.</span></span> |
|<span data-ttu-id="00486-204">resourceRate</span><span class="sxs-lookup"><span data-stu-id="00486-204">resourceRate</span></span>| <span data-ttu-id="00486-205">double</span><span class="sxs-lookup"><span data-stu-id="00486-205">double</span></span>| <span data-ttu-id="00486-206">청구 가능 단위당 적용 가능한 hello 속도입니다.</span><span class="sxs-lookup"><span data-stu-id="00486-206">hello rate applicable per billable unit.</span></span> |
|<span data-ttu-id="00486-207">cost</span><span class="sxs-lookup"><span data-stu-id="00486-207">cost</span></span>| <span data-ttu-id="00486-208">double</span><span class="sxs-lookup"><span data-stu-id="00486-208">double</span></span>| <span data-ttu-id="00486-209">hello 충전량 hello 미터에 대 한 발생 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="00486-209">hello charge that has been incurred for hello meter.</span></span> |
|<span data-ttu-id="00486-210">resourceLocation</span><span class="sxs-lookup"><span data-stu-id="00486-210">resourceLocation</span></span>| <span data-ttu-id="00486-211">string</span><span class="sxs-lookup"><span data-stu-id="00486-211">string</span></span>| <span data-ttu-id="00486-212">Hello 측정기 실행 되 고 있는 hello 데이터 센터를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-212">Identifies hello datacenter where hello meter is running.</span></span> |
|<span data-ttu-id="00486-213">consumedService</span><span class="sxs-lookup"><span data-stu-id="00486-213">consumedService</span></span>| <span data-ttu-id="00486-214">string</span><span class="sxs-lookup"><span data-stu-id="00486-214">string</span></span>| <span data-ttu-id="00486-215">번호 사용 된 Azure 플랫폼 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="00486-215">hello Azure platform service that was used.</span></span> |
|<span data-ttu-id="00486-216">instanceId</span><span class="sxs-lookup"><span data-stu-id="00486-216">instanceId</span></span>| <span data-ttu-id="00486-217">string</span><span class="sxs-lookup"><span data-stu-id="00486-217">string</span></span>| <span data-ttu-id="00486-218">이 식별자는 hello 리소스의 hello 이름 또는 hello 정규화 된 리소스 id입니다.</span><span class="sxs-lookup"><span data-stu-id="00486-218">This identifier is hello name of hello resource or hello fully qualified Resource ID.</span></span> <span data-ttu-id="00486-219">자세한 내용은 [Azure Resource Manager API](https://docs.microsoft.com/rest/api/resources/resources)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="00486-219">For more information, see [Azure Resource Manager API](https://docs.microsoft.com/rest/api/resources/resources)</span></span> |
|<span data-ttu-id="00486-220">serviceInfo1</span><span class="sxs-lookup"><span data-stu-id="00486-220">serviceInfo1</span></span>| <span data-ttu-id="00486-221">string</span><span class="sxs-lookup"><span data-stu-id="00486-221">string</span></span>| <span data-ttu-id="00486-222">내부 Azure 서비스 메타데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="00486-222">Internal Azure Service Metadata.</span></span> |
|<span data-ttu-id="00486-223">serviceInfo2</span><span class="sxs-lookup"><span data-stu-id="00486-223">serviceInfo2</span></span>| <span data-ttu-id="00486-224">string</span><span class="sxs-lookup"><span data-stu-id="00486-224">string</span></span>| <span data-ttu-id="00486-225">예를 들어, 가상 컴퓨터의 이미지 형식 및 ExpressRoute의 ISP 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="00486-225">For example, an image type for a virtual machine and ISP name for ExpressRoute.</span></span> |
|<span data-ttu-id="00486-226">additionalInfo</span><span class="sxs-lookup"><span data-stu-id="00486-226">additionalInfo</span></span>| <span data-ttu-id="00486-227">string</span><span class="sxs-lookup"><span data-stu-id="00486-227">string</span></span>| <span data-ttu-id="00486-228">서비스 특정 메타데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="00486-228">Service-specific metadata.</span></span> <span data-ttu-id="00486-229">예를 들어 가상 컴퓨터용 이미지 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="00486-229">For example, an image type for a virtual machine.</span></span> |
|<span data-ttu-id="00486-230">tags</span><span class="sxs-lookup"><span data-stu-id="00486-230">tags</span></span>| <span data-ttu-id="00486-231">string</span><span class="sxs-lookup"><span data-stu-id="00486-231">string</span></span>| <span data-ttu-id="00486-232">태그를 추가한 고객입니다.</span><span class="sxs-lookup"><span data-stu-id="00486-232">Customer added tags.</span></span> <span data-ttu-id="00486-233">자세한 내용은 [태그를 사용하여 Azure 리소스 구성](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-using-tags)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="00486-233">For more information, see [Organize your Azure resources with tags](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-using-tags).</span></span> |
|<span data-ttu-id="00486-234">storeServiceIdentifier</span><span class="sxs-lookup"><span data-stu-id="00486-234">storeServiceIdentifier</span></span>| <span data-ttu-id="00486-235">string</span><span class="sxs-lookup"><span data-stu-id="00486-235">string</span></span>| <span data-ttu-id="00486-236">이 열이 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="00486-236">This columns is not used.</span></span> <span data-ttu-id="00486-237">이전 버전과의 호환성을 위해 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-237">Present for backward compatibility.</span></span> |
|<span data-ttu-id="00486-238">departmentName</span><span class="sxs-lookup"><span data-stu-id="00486-238">departmentName</span></span>| <span data-ttu-id="00486-239">string</span><span class="sxs-lookup"><span data-stu-id="00486-239">string</span></span>| <span data-ttu-id="00486-240">Hello 부서의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="00486-240">Name of hello department.</span></span> |
|<span data-ttu-id="00486-241">costCenter</span><span class="sxs-lookup"><span data-stu-id="00486-241">costCenter</span></span>| <span data-ttu-id="00486-242">string</span><span class="sxs-lookup"><span data-stu-id="00486-242">string</span></span>| <span data-ttu-id="00486-243">hello 사용과 연관 hello 비용 센터</span><span class="sxs-lookup"><span data-stu-id="00486-243">hello cost center that hello usage is associated with.</span></span> |
|<span data-ttu-id="00486-244">unitOfMeasure</span><span class="sxs-lookup"><span data-stu-id="00486-244">unitOfMeasure</span></span>| <span data-ttu-id="00486-245">string</span><span class="sxs-lookup"><span data-stu-id="00486-245">string</span></span>| <span data-ttu-id="00486-246">Hello 서비스에 청구 되는 hello 단위를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-246">Identifies hello unit that hello service is charged in.</span></span> <span data-ttu-id="00486-247">예: GB, 시간, 10,000초</span><span class="sxs-lookup"><span data-stu-id="00486-247">Example: GB, hours, 10,000 s.</span></span> |
|<span data-ttu-id="00486-248">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="00486-248">resourceGroup</span></span>| <span data-ttu-id="00486-249">string</span><span class="sxs-lookup"><span data-stu-id="00486-249">string</span></span>| <span data-ttu-id="00486-250">hello 리소스 그룹에서 실행 중인 배포 된 미터는 hello에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00486-250">hello resource group in which hello deployed meter is running in.</span></span> <span data-ttu-id="00486-251">자세한 내용은 [Azure Resource Manager 개요](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="00486-251">For more information, see [Azure Resource Manager overview](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview).</span></span> |
<br/>
## <a name="see-also"></a><span data-ttu-id="00486-252">참고 항목</span><span class="sxs-lookup"><span data-stu-id="00486-252">See also</span></span>

* [<span data-ttu-id="00486-253">청구 기간 API</span><span class="sxs-lookup"><span data-stu-id="00486-253">Billing Periods API</span></span>](billing-enterprise-api-billing-periods.md)

* [<span data-ttu-id="00486-254">잔액 및 요약 API</span><span class="sxs-lookup"><span data-stu-id="00486-254">Balance and Summary API</span></span>](billing-enterprise-api-balance-summary.md)

* [<span data-ttu-id="00486-255">Marketplace 저장소 요금 API</span><span class="sxs-lookup"><span data-stu-id="00486-255">Marketplace Store Charge API</span></span>](billing-enterprise-api-marketplace-storecharge.md) 

* [<span data-ttu-id="00486-256">가격표 API</span><span class="sxs-lookup"><span data-stu-id="00486-256">Price Sheet API</span></span>](billing-enterprise-api-pricesheet.md)

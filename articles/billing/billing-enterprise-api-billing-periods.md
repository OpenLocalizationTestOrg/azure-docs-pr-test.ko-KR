---
title: "Azure 청구 엔터프라이즈 API - 청구 기간 | Microsoft Docs"
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
ms.openlocfilehash: c6880b79189e0683387a7aafbd6fa4805b3b42ef
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="reporting-apis-for-enterprise-customers---billing-periods"></a><span data-ttu-id="beff9-103">기업 고객을 위한 보고 API - 청구 기간</span><span class="sxs-lookup"><span data-stu-id="beff9-103">Reporting APIs for Enterprise customers - Billing Periods</span></span>

<span data-ttu-id="beff9-104">청구 기간 API는 지정된 등록에 대한 사용량 데이터를 역방향 시간 순서로 표시한 청구 기간 목록을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="beff9-104">The Billing Periods API returns a list of billing periods that have consumption data for the specified Enrollment in reverse chronological order.</span></span> <span data-ttu-id="beff9-105">각 기간에는 4개의 데이터 집합(잔액 요약, 사용량 세부 정보, Marktplace 요금 및 가격표)에 대한 API 경로를 가리키는 속성이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="beff9-105">Each Period contains a property pointing to the API route for the four sets of data - BalanceSummary, UsageDetails, Marktplace Charges, and PriceSheet.</span></span> <span data-ttu-id="beff9-106">기간에 데이터가 없으면 해당 속성은 null입니다.</span><span class="sxs-lookup"><span data-stu-id="beff9-106">If the period does not have data, the corresponding property is null.</span></span> 


##<a name="request"></a><span data-ttu-id="beff9-107">요청</span><span class="sxs-lookup"><span data-stu-id="beff9-107">Request</span></span> 
<span data-ttu-id="beff9-108">추가해야 할 공통 헤더 속성은 [여기](billing-enterprise-api.md)에 지정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="beff9-108">Common header properties that need to be added are specified [here](billing-enterprise-api.md).</span></span> 

|<span data-ttu-id="beff9-109">메서드</span><span class="sxs-lookup"><span data-stu-id="beff9-109">Method</span></span> | <span data-ttu-id="beff9-110">요청 URI</span><span class="sxs-lookup"><span data-stu-id="beff9-110">Request URI</span></span>|
|-|-|
|<span data-ttu-id="beff9-111">GET</span><span class="sxs-lookup"><span data-stu-id="beff9-111">GET</span></span>| <span data-ttu-id="beff9-112">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingperiods</span><span class="sxs-lookup"><span data-stu-id="beff9-112">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingperiods</span></span>|

> [!Note]
> <span data-ttu-id="beff9-113">API의 미리 보기 버전을 사용하려면 위 URL에서 v2를 v1로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="beff9-113">To use the preview version of API, replace v2 with v1 in the above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="beff9-114">응답</span><span class="sxs-lookup"><span data-stu-id="beff9-114">Response</span></span>
 
    
    
      [
            {
                "billingPeriodId": "201704",
                "billingStart": "2017-04-01T00:00:00Z",
                "billingEnd": "2017-04-30T11:59:59Z",
                "balanceSummary": "/v1/enrollments/100/billingperiods/201704/balancesummary",
                "usageDetails": "/v1/enrollments/100/billingperiods/201704/usagedetails",
                "marketplaceCharges": "/v1/enrollments/100/billingperiods/201704/marketplacecharges",
                "priceSheet": "/v1/enrollments/100/billingperiods/201704/pricesheet"
            },          
            ....
      ]
    

<span data-ttu-id="beff9-115">**응답 속성 정의**</span><span class="sxs-lookup"><span data-stu-id="beff9-115">**Response property definitions**</span></span>

|<span data-ttu-id="beff9-116">속성 이름</span><span class="sxs-lookup"><span data-stu-id="beff9-116">Property Name</span></span>| <span data-ttu-id="beff9-117">형식</span><span class="sxs-lookup"><span data-stu-id="beff9-117">Type</span></span>| <span data-ttu-id="beff9-118">설명</span><span class="sxs-lookup"><span data-stu-id="beff9-118">Description</span></span>
|-|-|-|
|<span data-ttu-id="beff9-119">billingPeriodId</span><span class="sxs-lookup"><span data-stu-id="beff9-119">billingPeriodId</span></span>| <span data-ttu-id="beff9-120">string</span><span class="sxs-lookup"><span data-stu-id="beff9-120">string</span></span>| <span data-ttu-id="beff9-121">특정 청구 기간을 나타내는 고유 ID</span><span class="sxs-lookup"><span data-stu-id="beff9-121">The unique Id that represents a particular Billing period</span></span>|
|<span data-ttu-id="beff9-122">billingStart</span><span class="sxs-lookup"><span data-stu-id="beff9-122">billingStart</span></span>| <span data-ttu-id="beff9-123">datetime</span><span class="sxs-lookup"><span data-stu-id="beff9-123">datetime</span></span>| <span data-ttu-id="beff9-124">기간 시작 날짜는 나타내는 ISO 8601 문자열</span><span class="sxs-lookup"><span data-stu-id="beff9-124">ISO 8601 string representing the period start date</span></span>|
|<span data-ttu-id="beff9-125">billingEnd</span><span class="sxs-lookup"><span data-stu-id="beff9-125">billingEnd</span></span>| <span data-ttu-id="beff9-126">datetime</span><span class="sxs-lookup"><span data-stu-id="beff9-126">datetime</span></span>| <span data-ttu-id="beff9-127">기간 종료 날짜는 나타내는 ISO 8601 문자열</span><span class="sxs-lookup"><span data-stu-id="beff9-127">ISO 8601 string representing the period end date</span></span>|
|<span data-ttu-id="beff9-128">balanceSummary</span><span class="sxs-lookup"><span data-stu-id="beff9-128">balanceSummary</span></span>| <span data-ttu-id="beff9-129">string</span><span class="sxs-lookup"><span data-stu-id="beff9-129">string</span></span>| <span data-ttu-id="beff9-130">이 기간의 잔액 요약 데이터에 라우팅하는 URL 경로</span><span class="sxs-lookup"><span data-stu-id="beff9-130">The URL path that routes to the Balance Summary data for this period</span></span>|
|<span data-ttu-id="beff9-131">usageDetails</span><span class="sxs-lookup"><span data-stu-id="beff9-131">usageDetails</span></span>| <span data-ttu-id="beff9-132">string</span><span class="sxs-lookup"><span data-stu-id="beff9-132">string</span></span>| <span data-ttu-id="beff9-133">이 기간의 사용량 세부 정보 데이터에 라우팅하는 URL 경로</span><span class="sxs-lookup"><span data-stu-id="beff9-133">The URL path that routes to the Usage Details data for this period</span></span>|
|<span data-ttu-id="beff9-134">marketplaceCharges</span><span class="sxs-lookup"><span data-stu-id="beff9-134">marketplaceCharges</span></span>| <span data-ttu-id="beff9-135">string</span><span class="sxs-lookup"><span data-stu-id="beff9-135">string</span></span>| <span data-ttu-id="beff9-136">이 기간의 Marketplace 요금 데이터에 라우팅하는 URL 경로</span><span class="sxs-lookup"><span data-stu-id="beff9-136">The URL path that routes to the Marketplace Charges data for this period</span></span>|
|<span data-ttu-id="beff9-137">priceSheet</span><span class="sxs-lookup"><span data-stu-id="beff9-137">priceSheet</span></span>| <span data-ttu-id="beff9-138">string</span><span class="sxs-lookup"><span data-stu-id="beff9-138">string</span></span>| <span data-ttu-id="beff9-139">이 기간의 가격표 데이터에 라우팅하는 URL 경로</span><span class="sxs-lookup"><span data-stu-id="beff9-139">The URL path that routes to the PriceSheet data for this period</span></span>|

<br/>
## <a name="see-also"></a><span data-ttu-id="beff9-140">참고 항목</span><span class="sxs-lookup"><span data-stu-id="beff9-140">See also</span></span>

* [<span data-ttu-id="beff9-141">잔액 및 요약 API</span><span class="sxs-lookup"><span data-stu-id="beff9-141">Balance and Summary API</span></span>](billing-enterprise-api-balance-summary.md)

* [<span data-ttu-id="beff9-142">사용량 세부 정보 API</span><span class="sxs-lookup"><span data-stu-id="beff9-142">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md) 

* [<span data-ttu-id="beff9-143">Marketplace 저장소 요금 API</span><span class="sxs-lookup"><span data-stu-id="beff9-143">Marketplace Store Charge API</span></span>](billing-enterprise-api-marketplace-storecharge.md) 

* [<span data-ttu-id="beff9-144">가격표 API</span><span class="sxs-lookup"><span data-stu-id="beff9-144">Price Sheet API</span></span>](billing-enterprise-api-pricesheet.md)
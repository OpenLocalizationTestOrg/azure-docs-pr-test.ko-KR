---
title: "청구 기간 청구 엔터프라이즈 Api aaaAzure | Microsoft Docs"
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
ms.openlocfilehash: d4e17f25b22729a7f213306fb019ee0dbeca87ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---billing-periods"></a><span data-ttu-id="53473-103">기업 고객을 위한 보고 API - 청구 기간</span><span class="sxs-lookup"><span data-stu-id="53473-103">Reporting APIs for Enterprise customers - Billing Periods</span></span>

<span data-ttu-id="53473-104">대금 청구 기간 API hello 시간 순서에 등록에 대 한 hello에 대 한 데이터를 소비 하는 기간을 청구의 목록이 지정을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="53473-104">hello Billing Periods API returns a list of billing periods that have consumption data for hello specified Enrollment in reverse chronological order.</span></span> <span data-ttu-id="53473-105">각 기간에는 4 개의 집합이 데이터 요금-BalanceSummary, UsageDetails, Marktplace 요금 및 가격표를 hello에 대 한 toohello API 경로 가리키는 속성을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="53473-105">Each Period contains a property pointing toohello API route for hello four sets of data - BalanceSummary, UsageDetails, Marktplace Charges, and PriceSheet.</span></span> <span data-ttu-id="53473-106">Hello 기간에 데이터가 없는 hello 해당 하는 속성은 null입니다.</span><span class="sxs-lookup"><span data-stu-id="53473-106">If hello period does not have data, hello corresponding property is null.</span></span> 


##<a name="request"></a><span data-ttu-id="53473-107">요청</span><span class="sxs-lookup"><span data-stu-id="53473-107">Request</span></span> 
<span data-ttu-id="53473-108">Toobe 추가 해야 하는 공통 헤더 속성이 지정 되어 [여기](billing-enterprise-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="53473-108">Common header properties that need toobe added are specified [here](billing-enterprise-api.md).</span></span> 

|<span data-ttu-id="53473-109">메서드</span><span class="sxs-lookup"><span data-stu-id="53473-109">Method</span></span> | <span data-ttu-id="53473-110">요청 URI</span><span class="sxs-lookup"><span data-stu-id="53473-110">Request URI</span></span>|
|-|-|
|<span data-ttu-id="53473-111">GET</span><span class="sxs-lookup"><span data-stu-id="53473-111">GET</span></span>| <span data-ttu-id="53473-112">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingperiods</span><span class="sxs-lookup"><span data-stu-id="53473-112">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingperiods</span></span>|

> [!Note]
> <span data-ttu-id="53473-113">toouse hello 미리 보기 버전의 API, URL 위에 hello v1 v2를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="53473-113">toouse hello preview version of API, replace v2 with v1 in hello above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="53473-114">응답</span><span class="sxs-lookup"><span data-stu-id="53473-114">Response</span></span>
 
    
    
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
    

<span data-ttu-id="53473-115">**응답 속성 정의**</span><span class="sxs-lookup"><span data-stu-id="53473-115">**Response property definitions**</span></span>

|<span data-ttu-id="53473-116">속성 이름</span><span class="sxs-lookup"><span data-stu-id="53473-116">Property Name</span></span>| <span data-ttu-id="53473-117">형식</span><span class="sxs-lookup"><span data-stu-id="53473-117">Type</span></span>| <span data-ttu-id="53473-118">설명</span><span class="sxs-lookup"><span data-stu-id="53473-118">Description</span></span>
|-|-|-|
|<span data-ttu-id="53473-119">billingPeriodId</span><span class="sxs-lookup"><span data-stu-id="53473-119">billingPeriodId</span></span>| <span data-ttu-id="53473-120">string</span><span class="sxs-lookup"><span data-stu-id="53473-120">string</span></span>| <span data-ttu-id="53473-121">hello 특정 요금 청구 기간을 나타내는 고유 Id</span><span class="sxs-lookup"><span data-stu-id="53473-121">hello unique Id that represents a particular Billing period</span></span>|
|<span data-ttu-id="53473-122">billingStart</span><span class="sxs-lookup"><span data-stu-id="53473-122">billingStart</span></span>| <span data-ttu-id="53473-123">datetime</span><span class="sxs-lookup"><span data-stu-id="53473-123">datetime</span></span>| <span data-ttu-id="53473-124">Hello 기간 시작 날짜를 나타내는 ISO 8601 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="53473-124">ISO 8601 string representing hello period start date</span></span>|
|<span data-ttu-id="53473-125">billingEnd</span><span class="sxs-lookup"><span data-stu-id="53473-125">billingEnd</span></span>| <span data-ttu-id="53473-126">datetime</span><span class="sxs-lookup"><span data-stu-id="53473-126">datetime</span></span>| <span data-ttu-id="53473-127">Hello 기간 종료 날짜를 나타내는 ISO 8601 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="53473-127">ISO 8601 string representing hello period end date</span></span>|
|<span data-ttu-id="53473-128">balanceSummary</span><span class="sxs-lookup"><span data-stu-id="53473-128">balanceSummary</span></span>| <span data-ttu-id="53473-129">string</span><span class="sxs-lookup"><span data-stu-id="53473-129">string</span></span>| <span data-ttu-id="53473-130">hello URL 경로입니다.이 기간에 대 한 toohello 균형 요약 데이터의 경로</span><span class="sxs-lookup"><span data-stu-id="53473-130">hello URL path that routes toohello Balance Summary data for this period</span></span>|
|<span data-ttu-id="53473-131">usageDetails</span><span class="sxs-lookup"><span data-stu-id="53473-131">usageDetails</span></span>| <span data-ttu-id="53473-132">string</span><span class="sxs-lookup"><span data-stu-id="53473-132">string</span></span>| <span data-ttu-id="53473-133">hello URL 경로입니다.이 기간에 대 한 toohello 사용 정보 데이터의 경로</span><span class="sxs-lookup"><span data-stu-id="53473-133">hello URL path that routes toohello Usage Details data for this period</span></span>|
|<span data-ttu-id="53473-134">marketplaceCharges</span><span class="sxs-lookup"><span data-stu-id="53473-134">marketplaceCharges</span></span>| <span data-ttu-id="53473-135">string</span><span class="sxs-lookup"><span data-stu-id="53473-135">string</span></span>| <span data-ttu-id="53473-136">hello URL 경로입니다.이 기간에 대 한 toohello 마켓플레이스 요금 데이터의 경로</span><span class="sxs-lookup"><span data-stu-id="53473-136">hello URL path that routes toohello Marketplace Charges data for this period</span></span>|
|<span data-ttu-id="53473-137">priceSheet</span><span class="sxs-lookup"><span data-stu-id="53473-137">priceSheet</span></span>| <span data-ttu-id="53473-138">string</span><span class="sxs-lookup"><span data-stu-id="53473-138">string</span></span>| <span data-ttu-id="53473-139">hello URL 경로입니다.이 기간에 대 한 toohello 가격표 데이터의 경로</span><span class="sxs-lookup"><span data-stu-id="53473-139">hello URL path that routes toohello PriceSheet data for this period</span></span>|

<br/>
## <a name="see-also"></a><span data-ttu-id="53473-140">참고 항목</span><span class="sxs-lookup"><span data-stu-id="53473-140">See also</span></span>

* [<span data-ttu-id="53473-141">잔액 및 요약 API</span><span class="sxs-lookup"><span data-stu-id="53473-141">Balance and Summary API</span></span>](billing-enterprise-api-balance-summary.md)

* [<span data-ttu-id="53473-142">사용량 세부 정보 API</span><span class="sxs-lookup"><span data-stu-id="53473-142">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md) 

* [<span data-ttu-id="53473-143">Marketplace 저장소 요금 API</span><span class="sxs-lookup"><span data-stu-id="53473-143">Marketplace Store Charge API</span></span>](billing-enterprise-api-marketplace-storecharge.md) 

* [<span data-ttu-id="53473-144">가격표 API</span><span class="sxs-lookup"><span data-stu-id="53473-144">Price Sheet API</span></span>](billing-enterprise-api-pricesheet.md)
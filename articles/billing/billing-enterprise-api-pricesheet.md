---
title: "Azure 청구 엔터프라이즈 API - 가격표 | Microsoft Docs"
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
ms.openlocfilehash: 2e7d6e883abe4cee13bc5f684baf2a1ea9c6c397
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="reporting-apis-for-enterprise-customers---price-sheet"></a><span data-ttu-id="953cf-103">기업 고객을 위한 보고 API - 가격표</span><span class="sxs-lookup"><span data-stu-id="953cf-103">Reporting APIs for Enterprise customers - Price Sheet</span></span>

<span data-ttu-id="953cf-104">가격표 API는 지정된 등록 및 청구 기간에 대한 각 측정기에 적용할 수 있는 가격을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="953cf-104">The Price Sheet API provides the applicable rate for each Meter for the given Enrollment and Billing Period.</span></span>

##<a name="request"></a><span data-ttu-id="953cf-105">요청</span><span class="sxs-lookup"><span data-stu-id="953cf-105">Request</span></span>
<span data-ttu-id="953cf-106">추가해야 할 공통 헤더 속성은 [여기](billing-enterprise-api.md)에 지정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="953cf-106">Common header properties that need to be added are specified [here](billing-enterprise-api.md).</span></span> <span data-ttu-id="953cf-107">청구 기간을 지정하지 않으면 현재 청구 기간에 대한 데이터가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="953cf-107">If a billing period is not specified, then data for the current billing period is returned.</span></span>

|<span data-ttu-id="953cf-108">메서드</span><span class="sxs-lookup"><span data-stu-id="953cf-108">Method</span></span> | <span data-ttu-id="953cf-109">요청 URI</span><span class="sxs-lookup"><span data-stu-id="953cf-109">Request URI</span></span>|
|-|-|
|<span data-ttu-id="953cf-110">GET</span><span class="sxs-lookup"><span data-stu-id="953cf-110">GET</span></span>|<span data-ttu-id="953cf-111">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/pricesheet</span><span class="sxs-lookup"><span data-stu-id="953cf-111">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/pricesheet</span></span>|
|<span data-ttu-id="953cf-112">GET</span><span class="sxs-lookup"><span data-stu-id="953cf-112">GET</span></span>|<span data-ttu-id="953cf-113">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/pricesheet</span><span class="sxs-lookup"><span data-stu-id="953cf-113">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/pricesheet</span></span>|

> [!Note]
> <span data-ttu-id="953cf-114">API의 미리 보기 버전을 사용하려면 위 URL에서 v2를 v1로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="953cf-114">To use the preview version of API, replace v2 with v1 in the above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="953cf-115">응답</span><span class="sxs-lookup"><span data-stu-id="953cf-115">Response</span></span>

    
        [
            {
                "id": "enrollments/57354989/billingperiods/201601/products/343/pricesheets",
                "billingPeriodId": "201704",
                "meterId": "dc210ecb-97e8-4522-8134-2385494233c0",
                "meterName": "A1 VM",
                "unitOfMeasure": "100 Hours",
                "includedQuantity": 0,
                "partNumber": "N7H-00015",
                "unitPrice": 0.00,
                "currencyCode": "USD"
            },
            {
                "id": "enrollments/57354989/billingperiods/201601/products/2884/pricesheets",
                "billingPeriodId": "201404",
                "meterId": "dc210ecb-97e8-4522-8134-5385494233c0",
                "meterName": "Locally Redundant Storage Premium Storage - Snapshots - AU East",
                "unitOfMeasure": "100 GB",
                "includedQuantity": 0,
                "partNumber": "N9H-00402",
                "unitPrice": 0.00,
                "currencyCode": "USD"
            },
            ...
        ]
    

> [!Note]
><span data-ttu-id="953cf-116">미리 보기 API를 사용 중인 경우에는 meterId 필드가 제공되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="953cf-116">If you are using the Preview API, meterId field is not available.</span></span>
>

<span data-ttu-id="953cf-117">**응답 속성 정의**</span><span class="sxs-lookup"><span data-stu-id="953cf-117">**Response property definitions**</span></span>

|<span data-ttu-id="953cf-118">속성 이름</span><span class="sxs-lookup"><span data-stu-id="953cf-118">Property Name</span></span>| <span data-ttu-id="953cf-119">형식</span><span class="sxs-lookup"><span data-stu-id="953cf-119">Type</span></span>| <span data-ttu-id="953cf-120">설명</span><span class="sxs-lookup"><span data-stu-id="953cf-120">Description</span></span>
|-|-|-|
|<span data-ttu-id="953cf-121">id</span><span class="sxs-lookup"><span data-stu-id="953cf-121">id</span></span>| <span data-ttu-id="953cf-122">string</span><span class="sxs-lookup"><span data-stu-id="953cf-122">string</span></span>| <span data-ttu-id="953cf-123">특정 가격표 항목을 나타내는 고유 ID(청구 기간별 측정기)</span><span class="sxs-lookup"><span data-stu-id="953cf-123">The unique Id that represents a particular PriceSheet item (meter by billing period)</span></span>|
|<span data-ttu-id="953cf-124">billingPeriodId</span><span class="sxs-lookup"><span data-stu-id="953cf-124">billingPeriodId</span></span>| <span data-ttu-id="953cf-125">string</span><span class="sxs-lookup"><span data-stu-id="953cf-125">string</span></span>| <span data-ttu-id="953cf-126">특정 청구 기간을 나타내는 고유 ID</span><span class="sxs-lookup"><span data-stu-id="953cf-126">The unique Id that represents a particular Billing period</span></span>|
|<span data-ttu-id="953cf-127">meterId</span><span class="sxs-lookup"><span data-stu-id="953cf-127">meterId</span></span>| <span data-ttu-id="953cf-128">string</span><span class="sxs-lookup"><span data-stu-id="953cf-128">string</span></span>| <span data-ttu-id="953cf-129">측정기에 대한 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="953cf-129">The identifier for the meter.</span></span> <span data-ttu-id="953cf-130">사용 현황 meterId에 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="953cf-130">It can be mapped to the usage meterId.</span></span>|
|<span data-ttu-id="953cf-131">meterName</span><span class="sxs-lookup"><span data-stu-id="953cf-131">meterName</span></span>| <span data-ttu-id="953cf-132">string</span><span class="sxs-lookup"><span data-stu-id="953cf-132">string</span></span>| <span data-ttu-id="953cf-133">측정기 이름</span><span class="sxs-lookup"><span data-stu-id="953cf-133">The meter name</span></span>|
|<span data-ttu-id="953cf-134">unitOfMeasure</span><span class="sxs-lookup"><span data-stu-id="953cf-134">unitOfMeasure</span></span>| <span data-ttu-id="953cf-135">string</span><span class="sxs-lookup"><span data-stu-id="953cf-135">string</span></span>| <span data-ttu-id="953cf-136">서비스를 측정하기 위한 측정 단위</span><span class="sxs-lookup"><span data-stu-id="953cf-136">The Unit of Measure for measuring the service</span></span>|
|<span data-ttu-id="953cf-137">includedQuantity</span><span class="sxs-lookup"><span data-stu-id="953cf-137">includedQuantity</span></span>| <span data-ttu-id="953cf-138">decimal</span><span class="sxs-lookup"><span data-stu-id="953cf-138">decimal</span></span>| <span data-ttu-id="953cf-139">포함된 수량</span><span class="sxs-lookup"><span data-stu-id="953cf-139">Quantity that is included</span></span> |
|<span data-ttu-id="953cf-140">partNumber</span><span class="sxs-lookup"><span data-stu-id="953cf-140">partNumber</span></span>| <span data-ttu-id="953cf-141">string</span><span class="sxs-lookup"><span data-stu-id="953cf-141">string</span></span>| <span data-ttu-id="953cf-142">측정기와 연결된 부품 번호</span><span class="sxs-lookup"><span data-stu-id="953cf-142">The part number associated with the Meter</span></span>|
|<span data-ttu-id="953cf-143">unitPrice</span><span class="sxs-lookup"><span data-stu-id="953cf-143">unitPrice</span></span>| <span data-ttu-id="953cf-144">decimal</span><span class="sxs-lookup"><span data-stu-id="953cf-144">decimal</span></span>| <span data-ttu-id="953cf-145">측정기의 단가</span><span class="sxs-lookup"><span data-stu-id="953cf-145">The unit price for the meter</span></span>|
|<span data-ttu-id="953cf-146">currencyCode</span><span class="sxs-lookup"><span data-stu-id="953cf-146">currencyCode</span></span>| <span data-ttu-id="953cf-147">string</span><span class="sxs-lookup"><span data-stu-id="953cf-147">string</span></span>| <span data-ttu-id="953cf-148">unitPrice의 통화 코드</span><span class="sxs-lookup"><span data-stu-id="953cf-148">The currency code for the unitPrice</span></span>|
<br/>
## <a name="see-also"></a><span data-ttu-id="953cf-149">참고 항목</span><span class="sxs-lookup"><span data-stu-id="953cf-149">See also</span></span>

* [<span data-ttu-id="953cf-150">청구 기간 API</span><span class="sxs-lookup"><span data-stu-id="953cf-150">Billing Periods API</span></span>](billing-enterprise-api-billing-periods.md)

* [<span data-ttu-id="953cf-151">사용량 세부 정보 API</span><span class="sxs-lookup"><span data-stu-id="953cf-151">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md)

* [<span data-ttu-id="953cf-152">잔액 및 요약 API</span><span class="sxs-lookup"><span data-stu-id="953cf-152">Balance and Summary API</span></span>](billing-enterprise-api-balance-summary.md)

* [<span data-ttu-id="953cf-153">Marketplace 저장소 요금 API</span><span class="sxs-lookup"><span data-stu-id="953cf-153">Marketplace Store Charge API</span></span>](billing-enterprise-api-marketplace-storecharge.md)

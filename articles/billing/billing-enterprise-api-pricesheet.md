---
title: "aaaAzure 청구 엔터프라이즈 Api-가격표 | Microsoft Docs"
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
ms.openlocfilehash: 4cfe694c63fba266d117054b046d9caacb3b7197
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---price-sheet"></a><span data-ttu-id="9422b-103">기업 고객을 위한 보고 API - 가격표</span><span class="sxs-lookup"><span data-stu-id="9422b-103">Reporting APIs for Enterprise customers - Price Sheet</span></span>

<span data-ttu-id="9422b-104">hello 가격 시트 API hello 등록 및 대금 청구 기간에 대 한 각 수준에 대 한 hello 적용 가능한 속도 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9422b-104">hello Price Sheet API provides hello applicable rate for each Meter for hello given Enrollment and Billing Period.</span></span>

##<a name="request"></a><span data-ttu-id="9422b-105">요청</span><span class="sxs-lookup"><span data-stu-id="9422b-105">Request</span></span>
<span data-ttu-id="9422b-106">Toobe 추가 해야 하는 공통 헤더 속성이 지정 되어 [여기](billing-enterprise-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9422b-106">Common header properties that need toobe added are specified [here](billing-enterprise-api.md).</span></span> <span data-ttu-id="9422b-107">청구 기간 지정 하지 않으면 다음 hello 현재 청구에 대 한 데이터 기간 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9422b-107">If a billing period is not specified, then data for hello current billing period is returned.</span></span>

|<span data-ttu-id="9422b-108">메서드</span><span class="sxs-lookup"><span data-stu-id="9422b-108">Method</span></span> | <span data-ttu-id="9422b-109">요청 URI</span><span class="sxs-lookup"><span data-stu-id="9422b-109">Request URI</span></span>|
|-|-|
|<span data-ttu-id="9422b-110">GET</span><span class="sxs-lookup"><span data-stu-id="9422b-110">GET</span></span>|<span data-ttu-id="9422b-111">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/pricesheet</span><span class="sxs-lookup"><span data-stu-id="9422b-111">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/pricesheet</span></span>|
|<span data-ttu-id="9422b-112">GET</span><span class="sxs-lookup"><span data-stu-id="9422b-112">GET</span></span>|<span data-ttu-id="9422b-113">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/pricesheet</span><span class="sxs-lookup"><span data-stu-id="9422b-113">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/pricesheet</span></span>|

> [!Note]
> <span data-ttu-id="9422b-114">toouse hello 미리 보기 버전의 API, URL 위에 hello v1 v2를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="9422b-114">toouse hello preview version of API, replace v2 with v1 in hello above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="9422b-115">응답</span><span class="sxs-lookup"><span data-stu-id="9422b-115">Response</span></span>

    
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
><span data-ttu-id="9422b-116">Hello 미리 보기 API를 사용 하는 meterId 필드 ´ ù입니다.</span><span class="sxs-lookup"><span data-stu-id="9422b-116">If you are using hello Preview API, meterId field is not available.</span></span>
>

<span data-ttu-id="9422b-117">**응답 속성 정의**</span><span class="sxs-lookup"><span data-stu-id="9422b-117">**Response property definitions**</span></span>

|<span data-ttu-id="9422b-118">속성 이름</span><span class="sxs-lookup"><span data-stu-id="9422b-118">Property Name</span></span>| <span data-ttu-id="9422b-119">형식</span><span class="sxs-lookup"><span data-stu-id="9422b-119">Type</span></span>| <span data-ttu-id="9422b-120">설명</span><span class="sxs-lookup"><span data-stu-id="9422b-120">Description</span></span>
|-|-|-|
|<span data-ttu-id="9422b-121">id</span><span class="sxs-lookup"><span data-stu-id="9422b-121">id</span></span>| <span data-ttu-id="9422b-122">string</span><span class="sxs-lookup"><span data-stu-id="9422b-122">string</span></span>| <span data-ttu-id="9422b-123">hello (청구 기간으로 미터) 특정 가격표 항목을 나타내는 고유 Id</span><span class="sxs-lookup"><span data-stu-id="9422b-123">hello unique Id that represents a particular PriceSheet item (meter by billing period)</span></span>|
|<span data-ttu-id="9422b-124">billingPeriodId</span><span class="sxs-lookup"><span data-stu-id="9422b-124">billingPeriodId</span></span>| <span data-ttu-id="9422b-125">string</span><span class="sxs-lookup"><span data-stu-id="9422b-125">string</span></span>| <span data-ttu-id="9422b-126">hello 특정 요금 청구 기간을 나타내는 고유 Id</span><span class="sxs-lookup"><span data-stu-id="9422b-126">hello unique Id that represents a particular Billing period</span></span>|
|<span data-ttu-id="9422b-127">meterId</span><span class="sxs-lookup"><span data-stu-id="9422b-127">meterId</span></span>| <span data-ttu-id="9422b-128">string</span><span class="sxs-lookup"><span data-stu-id="9422b-128">string</span></span>| <span data-ttu-id="9422b-129">hello 식별자 hello 미터입니다.</span><span class="sxs-lookup"><span data-stu-id="9422b-129">hello identifier for hello meter.</span></span> <span data-ttu-id="9422b-130">매핑된 toohello 사용 meterId 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9422b-130">It can be mapped toohello usage meterId.</span></span>|
|<span data-ttu-id="9422b-131">meterName</span><span class="sxs-lookup"><span data-stu-id="9422b-131">meterName</span></span>| <span data-ttu-id="9422b-132">string</span><span class="sxs-lookup"><span data-stu-id="9422b-132">string</span></span>| <span data-ttu-id="9422b-133">hello 미터 이름</span><span class="sxs-lookup"><span data-stu-id="9422b-133">hello meter name</span></span>|
|<span data-ttu-id="9422b-134">unitOfMeasure</span><span class="sxs-lookup"><span data-stu-id="9422b-134">unitOfMeasure</span></span>| <span data-ttu-id="9422b-135">string</span><span class="sxs-lookup"><span data-stu-id="9422b-135">string</span></span>| <span data-ttu-id="9422b-136">hello 서비스를 측정 하기 위한 hello 측정 단위</span><span class="sxs-lookup"><span data-stu-id="9422b-136">hello Unit of Measure for measuring hello service</span></span>|
|<span data-ttu-id="9422b-137">includedQuantity</span><span class="sxs-lookup"><span data-stu-id="9422b-137">includedQuantity</span></span>| <span data-ttu-id="9422b-138">decimal</span><span class="sxs-lookup"><span data-stu-id="9422b-138">decimal</span></span>| <span data-ttu-id="9422b-139">포함된 수량</span><span class="sxs-lookup"><span data-stu-id="9422b-139">Quantity that is included</span></span> |
|<span data-ttu-id="9422b-140">partNumber</span><span class="sxs-lookup"><span data-stu-id="9422b-140">partNumber</span></span>| <span data-ttu-id="9422b-141">string</span><span class="sxs-lookup"><span data-stu-id="9422b-141">string</span></span>| <span data-ttu-id="9422b-142">측정기 hello와 관련 된 hello 부품 번호</span><span class="sxs-lookup"><span data-stu-id="9422b-142">hello part number associated with hello Meter</span></span>|
|<span data-ttu-id="9422b-143">unitPrice</span><span class="sxs-lookup"><span data-stu-id="9422b-143">unitPrice</span></span>| <span data-ttu-id="9422b-144">decimal</span><span class="sxs-lookup"><span data-stu-id="9422b-144">decimal</span></span>| <span data-ttu-id="9422b-145">측정기 hello에 대 한 hello 단가</span><span class="sxs-lookup"><span data-stu-id="9422b-145">hello unit price for hello meter</span></span>|
|<span data-ttu-id="9422b-146">currencyCode</span><span class="sxs-lookup"><span data-stu-id="9422b-146">currencyCode</span></span>| <span data-ttu-id="9422b-147">string</span><span class="sxs-lookup"><span data-stu-id="9422b-147">string</span></span>| <span data-ttu-id="9422b-148">hello unitPrice에 대 한 hello 통화 코드</span><span class="sxs-lookup"><span data-stu-id="9422b-148">hello currency code for hello unitPrice</span></span>|
<br/>
## <a name="see-also"></a><span data-ttu-id="9422b-149">참고 항목</span><span class="sxs-lookup"><span data-stu-id="9422b-149">See also</span></span>

* [<span data-ttu-id="9422b-150">청구 기간 API</span><span class="sxs-lookup"><span data-stu-id="9422b-150">Billing Periods API</span></span>](billing-enterprise-api-billing-periods.md)

* [<span data-ttu-id="9422b-151">사용량 세부 정보 API</span><span class="sxs-lookup"><span data-stu-id="9422b-151">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md)

* [<span data-ttu-id="9422b-152">잔액 및 요약 API</span><span class="sxs-lookup"><span data-stu-id="9422b-152">Balance and Summary API</span></span>](billing-enterprise-api-balance-summary.md)

* [<span data-ttu-id="9422b-153">Marketplace 저장소 요금 API</span><span class="sxs-lookup"><span data-stu-id="9422b-153">Marketplace Store Charge API</span></span>](billing-enterprise-api-marketplace-storecharge.md)

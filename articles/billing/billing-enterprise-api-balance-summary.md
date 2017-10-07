---
title: "aaaAzure 청구 엔터프라이즈 Api-균형 및 요약 | Microsoft Docs"
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
ms.openlocfilehash: b031de2c347e5abeacd11743cc96024434518918
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---balance-and-summary"></a><span data-ttu-id="20ef5-103">기업 고객을 위한 보고 API - 잔액 및 요약</span><span class="sxs-lookup"><span data-stu-id="20ef5-103">Reporting APIs for Enterprise customers - Balance and Summary</span></span>

<span data-ttu-id="20ef5-104">hello 균형 및 요약 API 월별 요약 잔액, 새 구매, Azure 마켓플레이스 서비스 요금이, 조정 및 초과 요금에 대 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="20ef5-104">hello Balance and Summary API offers a monthly summary of information on balances, new purchases, Azure Marketplace service charges, adjustments, and overage charges.</span></span>


##<a name="request"></a><span data-ttu-id="20ef5-105">요청</span><span class="sxs-lookup"><span data-stu-id="20ef5-105">Request</span></span> 
<span data-ttu-id="20ef5-106">Toobe 추가 해야 하는 공통 헤더 속성이 지정 되어 [여기](billing-enterprise-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="20ef5-106">Common header properties that need toobe added are specified [here](billing-enterprise-api.md).</span></span> <span data-ttu-id="20ef5-107">청구 기간 지정 하지 않으면 다음 hello 현재 청구에 대 한 데이터 기간 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="20ef5-107">If a billing period is not specified, then data for hello current billing period is returned.</span></span>

|<span data-ttu-id="20ef5-108">메서드</span><span class="sxs-lookup"><span data-stu-id="20ef5-108">Method</span></span> | <span data-ttu-id="20ef5-109">요청 URI</span><span class="sxs-lookup"><span data-stu-id="20ef5-109">Request URI</span></span>|
|-|-|
|<span data-ttu-id="20ef5-110">GET</span><span class="sxs-lookup"><span data-stu-id="20ef5-110">GET</span></span>| <span data-ttu-id="20ef5-111">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/balancesummary</span><span class="sxs-lookup"><span data-stu-id="20ef5-111">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/balancesummary</span></span>|
|<span data-ttu-id="20ef5-112">GET</span><span class="sxs-lookup"><span data-stu-id="20ef5-112">GET</span></span>| <span data-ttu-id="20ef5-113">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/balancesummary</span><span class="sxs-lookup"><span data-stu-id="20ef5-113">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/balancesummary</span></span>|

> [!Note]
> <span data-ttu-id="20ef5-114">toouse hello 미리 보기 버전의 API, URL 위에 hello v1 v2를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="20ef5-114">toouse hello preview version of API, replace v2 with v1 in hello above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="20ef5-115">응답</span><span class="sxs-lookup"><span data-stu-id="20ef5-115">Response</span></span>

        {
            "id": "enrollments/100/billingperiods/201507/balancesummaries",
            "billingPeriodId": 201507,
            "currencyCode": "USD",
            "beginningBalance": 0,
            "endingBalance": 1.1,
            "newPurchases": 1,
            "adjustments": 1.1,
            "utilized": 1.1,
            "serviceOverage": 1,
            "chargesBilledSeparately": 1,
            "totalOverage": 1,
            "totalUsage": 1.1,
            "azureMarketplaceServiceCharges": 1,
            "newPurchasesDetails": [
                {
                "name": "",
                "value": 1
                }
            ],
            "adjustmentDetails": [
                {
                "name": "Promo Credit",
                "value": 1.1
                },
                {
                "name": "SIE Credit",
                "value": 1.0
                }
            ]
        }


<span data-ttu-id="20ef5-116">**응답 속성 정의**</span><span class="sxs-lookup"><span data-stu-id="20ef5-116">**Response property definitions**</span></span>

|<span data-ttu-id="20ef5-117">속성 이름</span><span class="sxs-lookup"><span data-stu-id="20ef5-117">Property Name</span></span>| <span data-ttu-id="20ef5-118">형식</span><span class="sxs-lookup"><span data-stu-id="20ef5-118">Type</span></span>| <span data-ttu-id="20ef5-119">설명</span><span class="sxs-lookup"><span data-stu-id="20ef5-119">Description</span></span>
|-|-|-|
|<span data-ttu-id="20ef5-120">id</span><span class="sxs-lookup"><span data-stu-id="20ef5-120">id</span></span>|<span data-ttu-id="20ef5-121">string</span><span class="sxs-lookup"><span data-stu-id="20ef5-121">string</span></span>|<span data-ttu-id="20ef5-122">hello 특정 청구 기간 및 등록에 대 한 고유 Id</span><span class="sxs-lookup"><span data-stu-id="20ef5-122">hello unique Id for a specific billing period and enrollment</span></span>|
|<span data-ttu-id="20ef5-123">billingPeriodId</span><span class="sxs-lookup"><span data-stu-id="20ef5-123">billingPeriodId</span></span>|<span data-ttu-id="20ef5-124">string</span><span class="sxs-lookup"><span data-stu-id="20ef5-124">string</span></span> |<span data-ttu-id="20ef5-125">hello 청구 기간 Id</span><span class="sxs-lookup"><span data-stu-id="20ef5-125">hello billing period Id</span></span>|
|<span data-ttu-id="20ef5-126">currencyCode</span><span class="sxs-lookup"><span data-stu-id="20ef5-126">currencyCode</span></span>|<span data-ttu-id="20ef5-127">string</span><span class="sxs-lookup"><span data-stu-id="20ef5-127">string</span></span> |<span data-ttu-id="20ef5-128">hello 통화 코드</span><span class="sxs-lookup"><span data-stu-id="20ef5-128">hello currency code</span></span>|
|<span data-ttu-id="20ef5-129">beginningBalance</span><span class="sxs-lookup"><span data-stu-id="20ef5-129">beginningBalance</span></span>|<span data-ttu-id="20ef5-130">decimal</span><span class="sxs-lookup"><span data-stu-id="20ef5-130">decimal</span></span>| <span data-ttu-id="20ef5-131">hello 청구 기간에 대 한 hello 기초 잔액</span><span class="sxs-lookup"><span data-stu-id="20ef5-131">hello beginning balance for hello billing period</span></span>|
|<span data-ttu-id="20ef5-132">endingBalance</span><span class="sxs-lookup"><span data-stu-id="20ef5-132">endingBalance</span></span>|<span data-ttu-id="20ef5-133">decimal</span><span class="sxs-lookup"><span data-stu-id="20ef5-133">decimal</span></span>| <span data-ttu-id="20ef5-134">hello 균형 (매일 업데이트 됩니다이 진행 기간)에 대 한 hello 청구 기간의 끝</span><span class="sxs-lookup"><span data-stu-id="20ef5-134">hello ending balance for hello billing period (for open periods this will be updated daily)</span></span>|
|<span data-ttu-id="20ef5-135">newPurchases</span><span class="sxs-lookup"><span data-stu-id="20ef5-135">newPurchases</span></span>|<span data-ttu-id="20ef5-136">decimal</span><span class="sxs-lookup"><span data-stu-id="20ef5-136">decimal</span></span>| <span data-ttu-id="20ef5-137">총 신규 구매 금액</span><span class="sxs-lookup"><span data-stu-id="20ef5-137">Total new purchase amount</span></span>|
|<span data-ttu-id="20ef5-138">adjustments</span><span class="sxs-lookup"><span data-stu-id="20ef5-138">adjustments</span></span>|<span data-ttu-id="20ef5-139">decimal</span><span class="sxs-lookup"><span data-stu-id="20ef5-139">decimal</span></span>| <span data-ttu-id="20ef5-140">총 조정 금액</span><span class="sxs-lookup"><span data-stu-id="20ef5-140">Total adjustment amount</span></span>|
|<span data-ttu-id="20ef5-141">utilized</span><span class="sxs-lookup"><span data-stu-id="20ef5-141">utilized</span></span>|<span data-ttu-id="20ef5-142">decimal</span><span class="sxs-lookup"><span data-stu-id="20ef5-142">decimal</span></span>| <span data-ttu-id="20ef5-143">총 약정 사용량</span><span class="sxs-lookup"><span data-stu-id="20ef5-143">Total Commitment usage</span></span>|
|<span data-ttu-id="20ef5-144">serviceOverage</span><span class="sxs-lookup"><span data-stu-id="20ef5-144">serviceOverage</span></span>|<span data-ttu-id="20ef5-145">decimal</span><span class="sxs-lookup"><span data-stu-id="20ef5-145">decimal</span></span>| <span data-ttu-id="20ef5-146">Azure 서비스 초과 사용량</span><span class="sxs-lookup"><span data-stu-id="20ef5-146">Overage for Azure services</span></span>|
|<span data-ttu-id="20ef5-147">chargesBilledSeparately</span><span class="sxs-lookup"><span data-stu-id="20ef5-147">chargesBilledSeparately</span></span>|<span data-ttu-id="20ef5-148">decimal</span><span class="sxs-lookup"><span data-stu-id="20ef5-148">decimal</span></span>| <span data-ttu-id="20ef5-149">별도 청구 사용량</span><span class="sxs-lookup"><span data-stu-id="20ef5-149">Charges Billed separately</span></span>|
|<span data-ttu-id="20ef5-150">totalOverage</span><span class="sxs-lookup"><span data-stu-id="20ef5-150">totalOverage</span></span>|<span data-ttu-id="20ef5-151">decimal</span><span class="sxs-lookup"><span data-stu-id="20ef5-151">decimal</span></span>| <span data-ttu-id="20ef5-152">serviceOverage + chargesBilledSeparately</span><span class="sxs-lookup"><span data-stu-id="20ef5-152">serviceOverage + chargesBilledSeparately</span></span>|
|<span data-ttu-id="20ef5-153">totalUsage</span><span class="sxs-lookup"><span data-stu-id="20ef5-153">totalUsage</span></span>|<span data-ttu-id="20ef5-154">decimal</span><span class="sxs-lookup"><span data-stu-id="20ef5-154">decimal</span></span>| <span data-ttu-id="20ef5-155">Azure 서비스 약정 사용량 + 총 초과 사용량</span><span class="sxs-lookup"><span data-stu-id="20ef5-155">Azure service commitment + total Overage</span></span>|
|<span data-ttu-id="20ef5-156">azureMarketplaceServiceCharges</span><span class="sxs-lookup"><span data-stu-id="20ef5-156">azureMarketplaceServiceCharges</span></span>|<span data-ttu-id="20ef5-157">decimal</span><span class="sxs-lookup"><span data-stu-id="20ef5-157">decimal</span></span>| <span data-ttu-id="20ef5-158">Azure Marketplace에 대한 총 요금</span><span class="sxs-lookup"><span data-stu-id="20ef5-158">Total charges for Azure Marketplace</span></span>|
|<span data-ttu-id="20ef5-159">newPurchasesDetails</span><span class="sxs-lookup"><span data-stu-id="20ef5-159">newPurchasesDetails</span></span>|<span data-ttu-id="20ef5-160">이름 값 쌍의 JSON 문자열 배열</span><span class="sxs-lookup"><span data-stu-id="20ef5-160">JSON string array of Name Value pairs</span></span>|<span data-ttu-id="20ef5-161">신규 구매 목록</span><span class="sxs-lookup"><span data-stu-id="20ef5-161">List of new purchases</span></span>|
|<span data-ttu-id="20ef5-162">adjustmentDetails</span><span class="sxs-lookup"><span data-stu-id="20ef5-162">adjustmentDetails</span></span>|<span data-ttu-id="20ef5-163">이름 값 쌍의 JSON 문자열 배열</span><span class="sxs-lookup"><span data-stu-id="20ef5-163">JSON string array of Name Value pairs</span></span>|<span data-ttu-id="20ef5-164">조정 목록(프로모션 공제, SIE 공제 등)</span><span class="sxs-lookup"><span data-stu-id="20ef5-164">List of Adjustments (Promo credit, SIE credit etc.)</span></span> |


<br/>
## <a name="see-also"></a><span data-ttu-id="20ef5-165">참고 항목</span><span class="sxs-lookup"><span data-stu-id="20ef5-165">See also</span></span>

* [<span data-ttu-id="20ef5-166">청구 기간 API</span><span class="sxs-lookup"><span data-stu-id="20ef5-166">Billing Periods API</span></span>](billing-enterprise-api-billing-periods.md)

* [<span data-ttu-id="20ef5-167">사용량 세부 정보 API</span><span class="sxs-lookup"><span data-stu-id="20ef5-167">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md) 

* [<span data-ttu-id="20ef5-168">Marketplace 저장소 요금 API</span><span class="sxs-lookup"><span data-stu-id="20ef5-168">Marketplace Store Charge API</span></span>](billing-enterprise-api-marketplace-storecharge.md) 

* [<span data-ttu-id="20ef5-169">가격표 API</span><span class="sxs-lookup"><span data-stu-id="20ef5-169">Price Sheet API</span></span>](billing-enterprise-api-pricesheet.md)
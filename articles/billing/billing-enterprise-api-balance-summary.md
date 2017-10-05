---
title: "Azure 청구 엔터프라이즈 API - 잔액 및 요약 | Microsoft Docs"
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
ms.openlocfilehash: f6b149f0e656d2263705048aa5b644f5bb4a5712
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="reporting-apis-for-enterprise-customers---balance-and-summary"></a><span data-ttu-id="133b0-103">기업 고객을 위한 보고 API - 잔액 및 요약</span><span class="sxs-lookup"><span data-stu-id="133b0-103">Reporting APIs for Enterprise customers - Balance and Summary</span></span>

<span data-ttu-id="133b0-104">잔액 및 요약 API는 잔액, 신규 구매, Azure Marketplace 서비스 요금, 조정 및 초과 요금에 대한 월별 정보 요약을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="133b0-104">The Balance and Summary API offers a monthly summary of information on balances, new purchases, Azure Marketplace service charges, adjustments, and overage charges.</span></span>


##<a name="request"></a><span data-ttu-id="133b0-105">요청</span><span class="sxs-lookup"><span data-stu-id="133b0-105">Request</span></span> 
<span data-ttu-id="133b0-106">추가해야 할 공통 헤더 속성은 [여기](billing-enterprise-api.md)에 지정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="133b0-106">Common header properties that need to be added are specified [here](billing-enterprise-api.md).</span></span> <span data-ttu-id="133b0-107">청구 기간을 지정하지 않으면 현재 청구 기간에 대한 데이터가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="133b0-107">If a billing period is not specified, then data for the current billing period is returned.</span></span>

|<span data-ttu-id="133b0-108">메서드</span><span class="sxs-lookup"><span data-stu-id="133b0-108">Method</span></span> | <span data-ttu-id="133b0-109">요청 URI</span><span class="sxs-lookup"><span data-stu-id="133b0-109">Request URI</span></span>|
|-|-|
|<span data-ttu-id="133b0-110">GET</span><span class="sxs-lookup"><span data-stu-id="133b0-110">GET</span></span>| <span data-ttu-id="133b0-111">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/balancesummary</span><span class="sxs-lookup"><span data-stu-id="133b0-111">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/balancesummary</span></span>|
|<span data-ttu-id="133b0-112">GET</span><span class="sxs-lookup"><span data-stu-id="133b0-112">GET</span></span>| <span data-ttu-id="133b0-113">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/balancesummary</span><span class="sxs-lookup"><span data-stu-id="133b0-113">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/balancesummary</span></span>|

> [!Note]
> <span data-ttu-id="133b0-114">API의 미리 보기 버전을 사용하려면 위 URL에서 v2를 v1로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="133b0-114">To use the preview version of API, replace v2 with v1 in the above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="133b0-115">응답</span><span class="sxs-lookup"><span data-stu-id="133b0-115">Response</span></span>

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


<span data-ttu-id="133b0-116">**응답 속성 정의**</span><span class="sxs-lookup"><span data-stu-id="133b0-116">**Response property definitions**</span></span>

|<span data-ttu-id="133b0-117">속성 이름</span><span class="sxs-lookup"><span data-stu-id="133b0-117">Property Name</span></span>| <span data-ttu-id="133b0-118">형식</span><span class="sxs-lookup"><span data-stu-id="133b0-118">Type</span></span>| <span data-ttu-id="133b0-119">설명</span><span class="sxs-lookup"><span data-stu-id="133b0-119">Description</span></span>
|-|-|-|
|<span data-ttu-id="133b0-120">id</span><span class="sxs-lookup"><span data-stu-id="133b0-120">id</span></span>|<span data-ttu-id="133b0-121">string</span><span class="sxs-lookup"><span data-stu-id="133b0-121">string</span></span>|<span data-ttu-id="133b0-122">특정 청구 기간 및 등록에 대한 고유 ID</span><span class="sxs-lookup"><span data-stu-id="133b0-122">The unique Id for a specific billing period and enrollment</span></span>|
|<span data-ttu-id="133b0-123">billingPeriodId</span><span class="sxs-lookup"><span data-stu-id="133b0-123">billingPeriodId</span></span>|<span data-ttu-id="133b0-124">string</span><span class="sxs-lookup"><span data-stu-id="133b0-124">string</span></span> |<span data-ttu-id="133b0-125">청구 기간 ID</span><span class="sxs-lookup"><span data-stu-id="133b0-125">The billing period Id</span></span>|
|<span data-ttu-id="133b0-126">currencyCode</span><span class="sxs-lookup"><span data-stu-id="133b0-126">currencyCode</span></span>|<span data-ttu-id="133b0-127">string</span><span class="sxs-lookup"><span data-stu-id="133b0-127">string</span></span> |<span data-ttu-id="133b0-128">통화 코드</span><span class="sxs-lookup"><span data-stu-id="133b0-128">The currency code</span></span>|
|<span data-ttu-id="133b0-129">beginningBalance</span><span class="sxs-lookup"><span data-stu-id="133b0-129">beginningBalance</span></span>|<span data-ttu-id="133b0-130">decimal</span><span class="sxs-lookup"><span data-stu-id="133b0-130">decimal</span></span>| <span data-ttu-id="133b0-131">청구 기간의 기초 잔액</span><span class="sxs-lookup"><span data-stu-id="133b0-131">The beginning balance for the billing period</span></span>|
|<span data-ttu-id="133b0-132">endingBalance</span><span class="sxs-lookup"><span data-stu-id="133b0-132">endingBalance</span></span>|<span data-ttu-id="133b0-133">decimal</span><span class="sxs-lookup"><span data-stu-id="133b0-133">decimal</span></span>| <span data-ttu-id="133b0-134">청구 기간의 최종 잔액(영업일 기준으로 매일 업데이트됨)</span><span class="sxs-lookup"><span data-stu-id="133b0-134">The ending balance for the billing period (for open periods this will be updated daily)</span></span>|
|<span data-ttu-id="133b0-135">newPurchases</span><span class="sxs-lookup"><span data-stu-id="133b0-135">newPurchases</span></span>|<span data-ttu-id="133b0-136">decimal</span><span class="sxs-lookup"><span data-stu-id="133b0-136">decimal</span></span>| <span data-ttu-id="133b0-137">총 신규 구매 금액</span><span class="sxs-lookup"><span data-stu-id="133b0-137">Total new purchase amount</span></span>|
|<span data-ttu-id="133b0-138">adjustments</span><span class="sxs-lookup"><span data-stu-id="133b0-138">adjustments</span></span>|<span data-ttu-id="133b0-139">decimal</span><span class="sxs-lookup"><span data-stu-id="133b0-139">decimal</span></span>| <span data-ttu-id="133b0-140">총 조정 금액</span><span class="sxs-lookup"><span data-stu-id="133b0-140">Total adjustment amount</span></span>|
|<span data-ttu-id="133b0-141">utilized</span><span class="sxs-lookup"><span data-stu-id="133b0-141">utilized</span></span>|<span data-ttu-id="133b0-142">decimal</span><span class="sxs-lookup"><span data-stu-id="133b0-142">decimal</span></span>| <span data-ttu-id="133b0-143">총 약정 사용량</span><span class="sxs-lookup"><span data-stu-id="133b0-143">Total Commitment usage</span></span>|
|<span data-ttu-id="133b0-144">serviceOverage</span><span class="sxs-lookup"><span data-stu-id="133b0-144">serviceOverage</span></span>|<span data-ttu-id="133b0-145">decimal</span><span class="sxs-lookup"><span data-stu-id="133b0-145">decimal</span></span>| <span data-ttu-id="133b0-146">Azure 서비스 초과 사용량</span><span class="sxs-lookup"><span data-stu-id="133b0-146">Overage for Azure services</span></span>|
|<span data-ttu-id="133b0-147">chargesBilledSeparately</span><span class="sxs-lookup"><span data-stu-id="133b0-147">chargesBilledSeparately</span></span>|<span data-ttu-id="133b0-148">decimal</span><span class="sxs-lookup"><span data-stu-id="133b0-148">decimal</span></span>| <span data-ttu-id="133b0-149">별도 청구 사용량</span><span class="sxs-lookup"><span data-stu-id="133b0-149">Charges Billed separately</span></span>|
|<span data-ttu-id="133b0-150">totalOverage</span><span class="sxs-lookup"><span data-stu-id="133b0-150">totalOverage</span></span>|<span data-ttu-id="133b0-151">decimal</span><span class="sxs-lookup"><span data-stu-id="133b0-151">decimal</span></span>| <span data-ttu-id="133b0-152">serviceOverage + chargesBilledSeparately</span><span class="sxs-lookup"><span data-stu-id="133b0-152">serviceOverage + chargesBilledSeparately</span></span>|
|<span data-ttu-id="133b0-153">totalUsage</span><span class="sxs-lookup"><span data-stu-id="133b0-153">totalUsage</span></span>|<span data-ttu-id="133b0-154">decimal</span><span class="sxs-lookup"><span data-stu-id="133b0-154">decimal</span></span>| <span data-ttu-id="133b0-155">Azure 서비스 약정 사용량 + 총 초과 사용량</span><span class="sxs-lookup"><span data-stu-id="133b0-155">Azure service commitment + total Overage</span></span>|
|<span data-ttu-id="133b0-156">azureMarketplaceServiceCharges</span><span class="sxs-lookup"><span data-stu-id="133b0-156">azureMarketplaceServiceCharges</span></span>|<span data-ttu-id="133b0-157">decimal</span><span class="sxs-lookup"><span data-stu-id="133b0-157">decimal</span></span>| <span data-ttu-id="133b0-158">Azure Marketplace에 대한 총 요금</span><span class="sxs-lookup"><span data-stu-id="133b0-158">Total charges for Azure Marketplace</span></span>|
|<span data-ttu-id="133b0-159">newPurchasesDetails</span><span class="sxs-lookup"><span data-stu-id="133b0-159">newPurchasesDetails</span></span>|<span data-ttu-id="133b0-160">이름 값 쌍의 JSON 문자열 배열</span><span class="sxs-lookup"><span data-stu-id="133b0-160">JSON string array of Name Value pairs</span></span>|<span data-ttu-id="133b0-161">신규 구매 목록</span><span class="sxs-lookup"><span data-stu-id="133b0-161">List of new purchases</span></span>|
|<span data-ttu-id="133b0-162">adjustmentDetails</span><span class="sxs-lookup"><span data-stu-id="133b0-162">adjustmentDetails</span></span>|<span data-ttu-id="133b0-163">이름 값 쌍의 JSON 문자열 배열</span><span class="sxs-lookup"><span data-stu-id="133b0-163">JSON string array of Name Value pairs</span></span>|<span data-ttu-id="133b0-164">조정 목록(프로모션 공제, SIE 공제 등)</span><span class="sxs-lookup"><span data-stu-id="133b0-164">List of Adjustments (Promo credit, SIE credit etc.)</span></span> |


<br/>
## <a name="see-also"></a><span data-ttu-id="133b0-165">참고 항목</span><span class="sxs-lookup"><span data-stu-id="133b0-165">See also</span></span>

* [<span data-ttu-id="133b0-166">청구 기간 API</span><span class="sxs-lookup"><span data-stu-id="133b0-166">Billing Periods API</span></span>](billing-enterprise-api-billing-periods.md)

* [<span data-ttu-id="133b0-167">사용량 세부 정보 API</span><span class="sxs-lookup"><span data-stu-id="133b0-167">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md) 

* [<span data-ttu-id="133b0-168">Marketplace 저장소 요금 API</span><span class="sxs-lookup"><span data-stu-id="133b0-168">Marketplace Store Charge API</span></span>](billing-enterprise-api-marketplace-storecharge.md) 

* [<span data-ttu-id="133b0-169">가격표 API</span><span class="sxs-lookup"><span data-stu-id="133b0-169">Price Sheet API</span></span>](billing-enterprise-api-pricesheet.md)
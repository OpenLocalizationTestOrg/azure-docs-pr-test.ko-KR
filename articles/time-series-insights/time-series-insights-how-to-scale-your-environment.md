---
title: "Azure Time Series Insights 환경의 크기를 조정하는 방법 | Microsoft Docs"
description: "이 자습서에서는 Azure Time Series Insights 환경의 크기를 조정하는 방법을 다룹니다."
keywords: 
services: time-series-insights
documentationcenter: 
author: sandshadow
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/19/2017
ms.author: edett
ms.openlocfilehash: 8f6c66ea2173c98179ec899d6626c2ab6f7ec4b6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-scale-your-time-series-insights-environment"></a><span data-ttu-id="aaa6e-103">Time Series Insights 환경의 크기를 조정하는 방법</span><span class="sxs-lookup"><span data-stu-id="aaa6e-103">How to scale your Time Series Insights environment</span></span>

<span data-ttu-id="aaa6e-104">이 자습서에서는 Time Series Insights 환경의 크기를 조정하는 방법을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="aaa6e-104">This tutorial covers how to scale your Time Series Insights environment.</span></span>

> [!NOTE]
> <span data-ttu-id="aaa6e-105">SKU 형식 전반에서의 강화는 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="aaa6e-105">Scale up across sku types is not allowed.</span></span> <span data-ttu-id="aaa6e-106">S1 SKU를 사용한 환경은 S2 환경으로 변환할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="aaa6e-106">An environment with a S1 Sku cannot be converted into an S2 environment.</span></span>

## <a name="s1-sku-ingress-rates-and-capacities"></a><span data-ttu-id="aaa6e-107">S1 SKU 수신 속도 및 용량</span><span class="sxs-lookup"><span data-stu-id="aaa6e-107">S1 SKU ingress rates and capacities</span></span>

| <span data-ttu-id="aaa6e-108">S1 SKU 용량</span><span class="sxs-lookup"><span data-stu-id="aaa6e-108">S1 SKU Capacity</span></span> | <span data-ttu-id="aaa6e-109">수신 속도</span><span class="sxs-lookup"><span data-stu-id="aaa6e-109">Ingress Rate</span></span> | <span data-ttu-id="aaa6e-110">최대 저장소 용량</span><span class="sxs-lookup"><span data-stu-id="aaa6e-110">Maximum Storage Capacity</span></span>
| --- | --- | --- |
| <span data-ttu-id="aaa6e-111">1</span><span class="sxs-lookup"><span data-stu-id="aaa6e-111">1</span></span> | <span data-ttu-id="aaa6e-112">1GB(1백만 이벤트)</span><span class="sxs-lookup"><span data-stu-id="aaa6e-112">1 GB (1 million events)</span></span> | <span data-ttu-id="aaa6e-113">매달 30GB(3천만 이벤트)</span><span class="sxs-lookup"><span data-stu-id="aaa6e-113">30 GB (30 million events) per month</span></span> |
| <span data-ttu-id="aaa6e-114">10</span><span class="sxs-lookup"><span data-stu-id="aaa6e-114">10</span></span> | <span data-ttu-id="aaa6e-115">10GB(1천만 이벤트)</span><span class="sxs-lookup"><span data-stu-id="aaa6e-115">10 GB (10 million events)</span></span> | <span data-ttu-id="aaa6e-116">매달 300GB(3억 이벤트)</span><span class="sxs-lookup"><span data-stu-id="aaa6e-116">300 GB (300 million events) per month</span></span> |

## <a name="s2-sku-ingress-rates-and-capacities"></a><span data-ttu-id="aaa6e-117">S2 SKU 수신 속도 및 용량</span><span class="sxs-lookup"><span data-stu-id="aaa6e-117">S2 SKU ingress rates and capacities</span></span>

| <span data-ttu-id="aaa6e-118">S2 SKU 용량</span><span class="sxs-lookup"><span data-stu-id="aaa6e-118">S2 SKU Capacity</span></span> | <span data-ttu-id="aaa6e-119">수신 속도</span><span class="sxs-lookup"><span data-stu-id="aaa6e-119">Ingress Rate</span></span> | <span data-ttu-id="aaa6e-120">최대 저장소 용량</span><span class="sxs-lookup"><span data-stu-id="aaa6e-120">Maximum Storage Capacity</span></span>
| --- | --- | --- |
| <span data-ttu-id="aaa6e-121">1</span><span class="sxs-lookup"><span data-stu-id="aaa6e-121">1</span></span> | <span data-ttu-id="aaa6e-122">10GB(1천만 이벤트)</span><span class="sxs-lookup"><span data-stu-id="aaa6e-122">10 GB (10 million events)</span></span> | <span data-ttu-id="aaa6e-123">매달 300GB(3억 이벤트)</span><span class="sxs-lookup"><span data-stu-id="aaa6e-123">300 GB (300 million events) per month</span></span> |
| <span data-ttu-id="aaa6e-124">10</span><span class="sxs-lookup"><span data-stu-id="aaa6e-124">10</span></span> | <span data-ttu-id="aaa6e-125">100GB(1억 이벤트)</span><span class="sxs-lookup"><span data-stu-id="aaa6e-125">100 GB (100 million events)</span></span> | <span data-ttu-id="aaa6e-126">매달 3TB(30억 이벤트)</span><span class="sxs-lookup"><span data-stu-id="aaa6e-126">3 TB (3 billion events) per month</span></span> |

<span data-ttu-id="aaa6e-127">용량은 연속해서 크기가 조정되므로 용량 2의 S1 SKU는 일일 2GB(2백만) 이벤트 수신 속도 및 매달 60GB(6천만 이벤트)를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="aaa6e-127">Capacities scale linearly, so a S1 sku with capacity 2 supports 2 GB (2 million) events per day ingress rate and 60 GB (60 million events) per month.</span></span>

## <a name="changing-the-capacity-of-your-environment"></a><span data-ttu-id="aaa6e-128">사용자 환경의 용량 변경</span><span class="sxs-lookup"><span data-stu-id="aaa6e-128">Changing the capacity of your environment</span></span>

1. <span data-ttu-id="aaa6e-129">Azure Portal에서 용량을 변경할 환경을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="aaa6e-129">In the Azure portal, select the environment whose capacity you want to change.</span></span>
1. <span data-ttu-id="aaa6e-130">설정에서 구성을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aaa6e-130">Under Settings, click Configure.</span></span>
1. <span data-ttu-id="aaa6e-131">용량 슬라이더를 사용하여 수신 속도 및 저장소 용량에 대한 요구 사항을 충족하는 용량을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="aaa6e-131">Use the Capacity slider to select the capacity that meets the requirements for your ingress rates and storage capacity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aaa6e-132">다음 단계</span><span class="sxs-lookup"><span data-stu-id="aaa6e-132">Next steps</span></span>

* <span data-ttu-id="aaa6e-133">새 용량이 제한을 방지하기에 충분한지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="aaa6e-133">Verify that the new capacity is sufficient to prevent throttling.</span></span> <span data-ttu-id="aaa6e-134">자세한 내용은 [여기](time-series-insights-diagnose-and-solve-problems.md)에서 *사용자 환경이 제한될 수 있습니다* 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="aaa6e-134">For more details, see the *Your environment might be getting throttled* section [here](time-series-insights-diagnose-and-solve-problems.md).</span></span>
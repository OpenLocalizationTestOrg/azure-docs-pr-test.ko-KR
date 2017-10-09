---
title: "aaaHow tooscale Azure 시간 계열 Insights 환경 | Microsoft Docs"
description: "이 자습서에서는 어떻게 tooscale Azure 시간 계열 Insights 환경"
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
ms.openlocfilehash: 55eda388997589185bd34228762b95e182b228ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-your-time-series-insights-environment"></a><span data-ttu-id="59bfe-103">어떻게 tooscale 시간 시계열 Insights 환경</span><span class="sxs-lookup"><span data-stu-id="59bfe-103">How tooscale your Time Series Insights environment</span></span>

<span data-ttu-id="59bfe-104">이 자습서에서는 어떻게 tooscale 시간 시계열 Insights 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="59bfe-104">This tutorial covers how tooscale your Time Series Insights environment.</span></span>

> [!NOTE]
> <span data-ttu-id="59bfe-105">SKU 형식 전반에서의 강화는 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="59bfe-105">Scale up across sku types is not allowed.</span></span> <span data-ttu-id="59bfe-106">S1 SKU를 사용한 환경은 S2 환경으로 변환할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="59bfe-106">An environment with a S1 Sku cannot be converted into an S2 environment.</span></span>

## <a name="s1-sku-ingress-rates-and-capacities"></a><span data-ttu-id="59bfe-107">S1 SKU 수신 속도 및 용량</span><span class="sxs-lookup"><span data-stu-id="59bfe-107">S1 SKU ingress rates and capacities</span></span>

| <span data-ttu-id="59bfe-108">S1 SKU 용량</span><span class="sxs-lookup"><span data-stu-id="59bfe-108">S1 SKU Capacity</span></span> | <span data-ttu-id="59bfe-109">수신 속도</span><span class="sxs-lookup"><span data-stu-id="59bfe-109">Ingress Rate</span></span> | <span data-ttu-id="59bfe-110">최대 저장소 용량</span><span class="sxs-lookup"><span data-stu-id="59bfe-110">Maximum Storage Capacity</span></span>
| --- | --- | --- |
| <span data-ttu-id="59bfe-111">1</span><span class="sxs-lookup"><span data-stu-id="59bfe-111">1</span></span> | <span data-ttu-id="59bfe-112">1GB(1백만 이벤트)</span><span class="sxs-lookup"><span data-stu-id="59bfe-112">1 GB (1 million events)</span></span> | <span data-ttu-id="59bfe-113">매달 30GB(3천만 이벤트)</span><span class="sxs-lookup"><span data-stu-id="59bfe-113">30 GB (30 million events) per month</span></span> |
| <span data-ttu-id="59bfe-114">10</span><span class="sxs-lookup"><span data-stu-id="59bfe-114">10</span></span> | <span data-ttu-id="59bfe-115">10GB(1천만 이벤트)</span><span class="sxs-lookup"><span data-stu-id="59bfe-115">10 GB (10 million events)</span></span> | <span data-ttu-id="59bfe-116">매달 300GB(3억 이벤트)</span><span class="sxs-lookup"><span data-stu-id="59bfe-116">300 GB (300 million events) per month</span></span> |

## <a name="s2-sku-ingress-rates-and-capacities"></a><span data-ttu-id="59bfe-117">S2 SKU 수신 속도 및 용량</span><span class="sxs-lookup"><span data-stu-id="59bfe-117">S2 SKU ingress rates and capacities</span></span>

| <span data-ttu-id="59bfe-118">S2 SKU 용량</span><span class="sxs-lookup"><span data-stu-id="59bfe-118">S2 SKU Capacity</span></span> | <span data-ttu-id="59bfe-119">수신 속도</span><span class="sxs-lookup"><span data-stu-id="59bfe-119">Ingress Rate</span></span> | <span data-ttu-id="59bfe-120">최대 저장소 용량</span><span class="sxs-lookup"><span data-stu-id="59bfe-120">Maximum Storage Capacity</span></span>
| --- | --- | --- |
| <span data-ttu-id="59bfe-121">1</span><span class="sxs-lookup"><span data-stu-id="59bfe-121">1</span></span> | <span data-ttu-id="59bfe-122">10GB(1천만 이벤트)</span><span class="sxs-lookup"><span data-stu-id="59bfe-122">10 GB (10 million events)</span></span> | <span data-ttu-id="59bfe-123">매달 300GB(3억 이벤트)</span><span class="sxs-lookup"><span data-stu-id="59bfe-123">300 GB (300 million events) per month</span></span> |
| <span data-ttu-id="59bfe-124">10</span><span class="sxs-lookup"><span data-stu-id="59bfe-124">10</span></span> | <span data-ttu-id="59bfe-125">100GB(1억 이벤트)</span><span class="sxs-lookup"><span data-stu-id="59bfe-125">100 GB (100 million events)</span></span> | <span data-ttu-id="59bfe-126">매달 3TB(30억 이벤트)</span><span class="sxs-lookup"><span data-stu-id="59bfe-126">3 TB (3 billion events) per month</span></span> |

<span data-ttu-id="59bfe-127">용량은 연속해서 크기가 조정되므로 용량 2의 S1 SKU는 일일 2GB(2백만) 이벤트 수신 속도 및 매달 60GB(6천만 이벤트)를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="59bfe-127">Capacities scale linearly, so a S1 sku with capacity 2 supports 2 GB (2 million) events per day ingress rate and 60 GB (60 million events) per month.</span></span>

## <a name="changing-hello-capacity-of-your-environment"></a><span data-ttu-id="59bfe-128">사용자 환경의 hello 용량 변경</span><span class="sxs-lookup"><span data-stu-id="59bfe-128">Changing hello capacity of your environment</span></span>

1. <span data-ttu-id="59bfe-129">Hello Azure 포털에서에서 선택 hello 환경 용량 toochange 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="59bfe-129">In hello Azure portal, select hello environment whose capacity you want toochange.</span></span>
1. <span data-ttu-id="59bfe-130">설정에서 구성을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59bfe-130">Under Settings, click Configure.</span></span>
1. <span data-ttu-id="59bfe-131">Hello 용량 슬라이더 tooselect hello 수신 속도 대 한 hello 요구 사항을 충족 하는 용량과 저장소 용량을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="59bfe-131">Use hello Capacity slider tooselect hello capacity that meets hello requirements for your ingress rates and storage capacity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="59bfe-132">다음 단계</span><span class="sxs-lookup"><span data-stu-id="59bfe-132">Next steps</span></span>

* <span data-ttu-id="59bfe-133">Hello 새 용량이 충분 한지 확인 tooprevent 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="59bfe-133">Verify that hello new capacity is sufficient tooprevent throttling.</span></span> <span data-ttu-id="59bfe-134">자세한 내용은 참조 hello *환경 있습니다 수 제한에 이르기* 섹션 [여기](time-series-insights-diagnose-and-solve-problems.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="59bfe-134">For more details, see hello *Your environment might be getting throttled* section [here](time-series-insights-diagnose-and-solve-problems.md).</span></span>

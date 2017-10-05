---
title: "Stream Analytics 창 함수 소개 | Microsoft Docs"
description: "Stream Analytics의 세 가지 창 함수(연속, 도약, 슬라이딩)에 대해 알아봅니다."
keywords: "연속 창, 슬라이딩 윈도우, 도약 창"
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 0d8d8717-5d23-43f0-b475-af078ab4627d
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 09915ad747153210f655b152355c551046066a88
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="introduction-to-stream-analytics-window-functions"></a><span data-ttu-id="dbdc6-104">Stream Analytics 창 함수 소개</span><span class="sxs-lookup"><span data-stu-id="dbdc6-104">Introduction to Stream Analytics Window functions</span></span>
<span data-ttu-id="dbdc6-105">많은 실시간 스트리밍 시나리오에서 임시 창에 포함된 데이터에 작업을 수행하는 데 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="dbdc6-105">In many real time streaming scenarios, it is necessary to perform operations only on the data contained in temporal windows.</span></span> <span data-ttu-id="dbdc6-106">창 함수의 네이티브 지원은 개발자가 복잡한 스트림 처리 작업을 작성할 때 생산성을 향상시키는 Azure Stream Analytics의 주요 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="dbdc6-106">Native support for windowing functions is a key feature of Azure Stream Analytics that moves the needle on developer productivity in authoring complex stream processing jobs.</span></span> <span data-ttu-id="dbdc6-107">Stream Analytics을 사용하면 개발자가 [**연속**](https://msdn.microsoft.com/library/dn835055.aspx), [**도약**](https://msdn.microsoft.com/library/dn835041.aspx) 및 [**슬라이딩**](https://msdn.microsoft.com/library/dn835051.aspx) 창을 사용하여 스트리밍 데이터에 대한 임시 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbdc6-107">Stream Analytics enables developers to use [**Tumbling**](https://msdn.microsoft.com/library/dn835055.aspx), [**Hopping**](https://msdn.microsoft.com/library/dn835041.aspx) and [**Sliding**](https://msdn.microsoft.com/library/dn835051.aspx) windows to perform temporal operations on streaming data.</span></span> <span data-ttu-id="dbdc6-108">모든 [창](https://msdn.microsoft.com/library/dn835019.aspx) 작업 결과가 창의 **끝** 에 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="dbdc6-108">It is worth noting that all [Window](https://msdn.microsoft.com/library/dn835019.aspx) operations output results at the **end** of the window.</span></span> <span data-ttu-id="dbdc6-109">창의 출력은 사용된 집계 함수를 기반으로 하는 단일 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="dbdc6-109">The output of the window will be single event based on the aggregate function used.</span></span> <span data-ttu-id="dbdc6-110">이벤트에는 창 끝의 타임스탬프가 있고 모든 창 함수는 고정된 길이로 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="dbdc6-110">The event will have the time stamp of the end of the window and all Window functions are defined with a fixed length.</span></span> <span data-ttu-id="dbdc6-111">마지막으로 모든 창 함수는 반드시 [**GROUP BY**](https://msdn.microsoft.com/library/dn835023.aspx) 절에서 사용되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbdc6-111">Lastly it is important to note that all Window functions should be used in a [**GROUP BY**](https://msdn.microsoft.com/library/dn835023.aspx) clause.</span></span>

![Stream Analytics 창 함수 개념](media/stream-analytics-window-functions/stream-analytics-window-functions-conceptual.png)

## <a name="tumbling-window"></a><span data-ttu-id="dbdc6-113">연속 창</span><span class="sxs-lookup"><span data-stu-id="dbdc6-113">Tumbling Window</span></span>
<span data-ttu-id="dbdc6-114">연속 창 함수는 다른 시간 세그먼트에 데이터 스트림을 분할하는 데 사용되고 아래 예와 같이 그에 대한 기능을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="dbdc6-114">Tumbling window functions are used to segment a data stream into distinct time segments and perform a function against them, such as the example below.</span></span> <span data-ttu-id="dbdc6-115">연속 창의 핵심적인 차이는 반복되지만 겹치지 않고 이벤트가 둘 이상의 연속 창에 속할 수 없다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="dbdc6-115">The key differentiators of a Tumbling window are that they repeat, do not overlap and an event cannot belong to more than one tumbling window.</span></span>

![Stream Analytics 창 함수 연속 소개](media/stream-analytics-window-functions/stream-analytics-window-functions-tumbling-intro.png)

## <a name="hopping-window"></a><span data-ttu-id="dbdc6-117">도약 창</span><span class="sxs-lookup"><span data-stu-id="dbdc6-117">Hopping Window</span></span>
<span data-ttu-id="dbdc6-118">도약 창 함수는 고정된 기간만큼 시간을 앞으로 건너 뜁니다.</span><span class="sxs-lookup"><span data-stu-id="dbdc6-118">Hopping window functions hop forward in time by a fixed period.</span></span> <span data-ttu-id="dbdc6-119">겹칠 수 있는 연속 창으로 생각하기 쉬우므로 이벤트는 둘 이상의 도약 창 결과 집합에 속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbdc6-119">It may be easy to think of them as Tumbling windows that can overlap, so events can belong to more than one Hopping window result set.</span></span> <span data-ttu-id="dbdc6-120">연속 창과 동일한 도약 창을 만들려면 도약 크기를 창 크기와 동일하도록 지정하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dbdc6-120">To make a Hopping window the same as a Tumbling window one would simply specify the hop size to be the same as the window size.</span></span> 

![Stream Analytics 창 함수 도약 소개](media/stream-analytics-window-functions/stream-analytics-window-functions-hopping-intro.png)

## <a name="sliding-window"></a><span data-ttu-id="dbdc6-122">슬라이딩 윈도우</span><span class="sxs-lookup"><span data-stu-id="dbdc6-122">Sliding Window</span></span>
<span data-ttu-id="dbdc6-123">연속 또는 도약 창과 달리 슬라이딩 윈도우 함수는 이벤트가 발생할 때 출력 **만** 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="dbdc6-123">Sliding window functions, unlike Tumbling or Hopping windows, produce an output **only**  when an event occurs.</span></span> <span data-ttu-id="dbdc6-124">모든 창에는 하나 이상의 이벤트가 있고 창은 지속적으로 €(엡실론)만큼 앞으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="dbdc6-124">Every window will have at least one event and the window continuously moves forward by an € (epsilon).</span></span> <span data-ttu-id="dbdc6-125">도약 창과 마찬가지로 이벤트는 둘 이상의 슬라이딩 윈도우에 속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbdc6-125">Like Hopping Windows, events can belong to more than one Sliding Window.</span></span>

![Stream Analytics 창 함수 슬라이딩 소개](media/stream-analytics-window-functions/stream-analytics-window-functions-sliding-intro.png)

## <a name="getting-help-with-window-functions"></a><span data-ttu-id="dbdc6-127">창 함수 관련 도움말 보기</span><span class="sxs-lookup"><span data-stu-id="dbdc6-127">Getting help with Window functions</span></span>
<span data-ttu-id="dbdc6-128">추가 지원이 필요할 경우 [Azure Stream Analytics 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="dbdc6-128">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="dbdc6-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="dbdc6-129">Next steps</span></span>
* [<span data-ttu-id="dbdc6-130">Azure Stream Analytics 소개</span><span class="sxs-lookup"><span data-stu-id="dbdc6-130">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="dbdc6-131">Azure Stream Analytics 사용 시작</span><span class="sxs-lookup"><span data-stu-id="dbdc6-131">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="dbdc6-132">Azure  Stream Analytics 작업 규모 지정</span><span class="sxs-lookup"><span data-stu-id="dbdc6-132">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="dbdc6-133">Azure  Stream Analytics 쿼리 언어 참조</span><span class="sxs-lookup"><span data-stu-id="dbdc6-133">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="dbdc6-134">Azure Stream Analytics 관리 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="dbdc6-134">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)


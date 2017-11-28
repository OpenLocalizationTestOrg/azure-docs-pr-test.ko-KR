---
title: "Azure Stream Analytics로 이벤트 순서 및 지연 처리 | Microsoft Docs"
description: "Stream Analytics가 데이터 스트림의 잘못된 순서 또는 지연 이벤트에 어떻게 작동하는지 알아봅니다."
keywords: "순서 비지정, 지연, 이벤트"
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: a48e48c5fc65d0ffbb7c23f426a4b06dcd568821
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-stream-analytics-event-order-handling"></a><span data-ttu-id="c4f4a-104">Azure Stream Analytics 이벤트 순서 처리</span><span class="sxs-lookup"><span data-stu-id="c4f4a-104">Azure Stream Analytics event order handling</span></span>

<span data-ttu-id="c4f4a-105">이벤트의 임시 데이터 스트림에서 각 이벤트는 이벤트가 수신되는 시간이 함께 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-105">In a temporal data stream of events, each event is recorded with the time that the event is received.</span></span> <span data-ttu-id="c4f4a-106">일부 조건에서는 이벤트 스트림이 경우에 따라 일부 이벤트를 전송된 것과는 다른 순서로 수신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-106">Some conditions might cause event streams to occasionally receive some events in a different order than which they were sent.</span></span> <span data-ttu-id="c4f4a-107">간단한 TCP 재전송 또는 전송 장치와 수신 이벤트 허브 간 시계 기울이기에서 이 같은 현상이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-107">A simple TCP retransmit, or even a clock skew between the sending device and the receiving event hub might cause this to occur.</span></span> <span data-ttu-id="c4f4a-108">또한 “문장 부호” 이벤트도 수신된 이벤트 스트림에 추가되어 이벤트가 도착하지 않을 때 시간을 앞당깁니다.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-108">“Punctuation” events also are added to received event streams, to advance the time in the absence of event arrivals.</span></span> <span data-ttu-id="c4f4a-109">이러한 사항은 “3분 동안 로그인이 발생하지 않을 때 알림”과 같은 시나리오에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-109">These are needed in scenarios like “Notify me when no logins occur for 3 minutes."</span></span>

<span data-ttu-id="c4f4a-110">순서가 올바르지 않은 입력 스트림은 다음 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-110">Input streams that are not in order are either:</span></span>
* <span data-ttu-id="c4f4a-111">정렬되었습니다(따라서 **지연됨**).</span><span class="sxs-lookup"><span data-stu-id="c4f4a-111">Sorted (and therefore **delayed**).</span></span>
* <span data-ttu-id="c4f4a-112">사용자 지정 정책에 따라 시스템에서 조정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-112">Adjusted by the system, according to a user-specified policy.</span></span>


## <a name="lateness-tolerance"></a><span data-ttu-id="c4f4a-113">지연 허용 오차</span><span class="sxs-lookup"><span data-stu-id="c4f4a-113">Lateness tolerance</span></span>
<span data-ttu-id="c4f4a-114">Stream Analytics는 이러한 시나리오 형식을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-114">Stream Analytics tolerates these types of scenarios.</span></span> <span data-ttu-id="c4f4a-115">Stream Analytics는 “잘못된 순서” 및 “지연” 이벤트를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-115">Stream Analytics has handling for "out-of-order" and "late" events.</span></span> <span data-ttu-id="c4f4a-116">다음과 같은 방법으로 이러한 이벤트를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-116">It handles these events in the following ways:</span></span>

* <span data-ttu-id="c4f4a-117">순서가 올바르지 않으나 설정된 허용 오차 내로 도착하는 이벤트는 **타임스탬프 기준으로 다시 정렬**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-117">Events that arrive out of order but within the set tolerance are **reordered by timestamp**.</span></span>
* <span data-ttu-id="c4f4a-118">허용 오차보다 나중에 도착하는 이벤트는 **삭제 또는 조정**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-118">Events that arrive later than tolerance are **dropped or adjusted**.</span></span>
    * <span data-ttu-id="c4f4a-119">**조정**: 최신 허용 가능한 시간에 도착한 것처럼 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-119">**Adjusted**: Adjusted to appear to have arrived at the latest acceptable time.</span></span>
    * <span data-ttu-id="c4f4a-120">**삭제**: 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-120">**Dropped**: Discarded.</span></span>

![Stream Analytics 이벤트 처리](media/stream-analytics-event-handling/stream-analytics-event-handling.png)

## <a name="reduce-the-number-of-out-of-order-events"></a><span data-ttu-id="c4f4a-122">잘못된 순서 이벤트의 수 줄이기</span><span class="sxs-lookup"><span data-stu-id="c4f4a-122">Reduce the number of out-of-order events</span></span>

<span data-ttu-id="c4f4a-123">Stream Analytics는 들어오는 이벤트를 처리할 때 임시 변환을 적용하기 때문에(예: 기간 이동 집계 또는 임시 연결) Stream Analytics는 들어오는 이벤트를 타임스탬프 순서대로 정렬합니다.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-123">Because Stream Analytics applies a temporal transformation when it processes incoming events (for example, for windowed aggregates or temporal joins), Stream Analytics sorts incoming events by timestamp order.</span></span>

<span data-ttu-id="c4f4a-124">“타임스탬프 기준” 키워드가 사용되지 **않을** 경우 Azure Event Hubs 이벤트 큐에 넣기 시간이 기본적으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-124">When the “timestamp by” keyword is **not** used, the Azure Event Hubs event enqueue time is used by default.</span></span> <span data-ttu-id="c4f4a-125">이벤트 허브는 이벤트 허브의 각 파티션에 있는 타임스탬프의 단조성을 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-125">Event Hubs guarantees monotonicity of the timestamp on each partition of the event hub.</span></span> <span data-ttu-id="c4f4a-126">또한 모든 파티션의 이벤트가 타임스탬프 순서대로 병합되는 것을 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-126">It also guarantees that events from all partitions will be merged in timestamp order.</span></span> <span data-ttu-id="c4f4a-127">이러한 두 이벤트 허브 보증을 통해 잘못된 순서 이벤트를 없앨 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-127">These two Event Hubs guarantees ensure no out-of-order events.</span></span>

<span data-ttu-id="c4f4a-128">경우에 따라 보낸 사람의 타임스탬프를 사용하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-128">Sometimes, it’s important for you to use the sender’s timestamp.</span></span> <span data-ttu-id="c4f4a-129">이 경우 이벤트 페이로드의 타임스탬프가 “타임스탬프 기준”을 사용하여 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-129">In that case, a timestamp from the event payload is chosen by using “timestamp by.”</span></span> <span data-ttu-id="c4f4a-130">이러한 시나리오에서는 잘못 정렬된 이벤트의 원본이 하나 이상 도입될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-130">In these scenarios, one or more sources of event misorder might be introduced:</span></span>

* <span data-ttu-id="c4f4a-131">이벤트 생산자에 클록 오차가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-131">Event producers have clock skews.</span></span> <span data-ttu-id="c4f4a-132">이는 생산자가 다른 컴퓨터에 있어 다른 클록을 사용할 때 일반적입니다.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-132">This is common when producers are from different computers, so they have different clocks.</span></span>
* <span data-ttu-id="c4f4a-133">이벤트 원본에서 대상 이벤트 허브로 네트워크 지연이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-133">There's a network delay from the source of the events to the destination event hub.</span></span>
* <span data-ttu-id="c4f4a-134">클록 오차는 이벤트 허브 파티션 간에 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-134">Clock skews exist between event hub partitions.</span></span> <span data-ttu-id="c4f4a-135">Stream Analytics는 먼저 모든 이벤트 허브 파티션의 이벤트를 이벤트 큐에 넣기 시간으로 정렬합니다.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-135">Stream Analytics first sorts events from all event hub partitions by event enqueue time.</span></span> <span data-ttu-id="c4f4a-136">그런 다음 순서가 잘못된 이벤트에 대해 데이터 스트림을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-136">Then, it examines the data stream for misordered events.</span></span>

<span data-ttu-id="c4f4a-137">구성 탭에 다음과 같은 기본값이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-137">On the configuration tab, you see the following defaults:</span></span>

![Stream Analytics의 잘못된 순서 처리](media/stream-analytics-event-handling/stream-analytics-out-of-order-handling.png)

<span data-ttu-id="c4f4a-139">잘못된 순서 허용 시간으로 0초를 사용하는 경우 모든 이벤트를 항상 순서대로 되어 있도록 어설션합니다.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-139">If you use 0 seconds as the out-of-order tolerance window, you are asserting that all events are in order all the time.</span></span> <span data-ttu-id="c4f4a-140">순서가 잘못된 세 개의 이벤트 원본을 고려해 볼 때 그렇게 한 것 같지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-140">Given the three sources of misordered events, it’s unlikely that this is true.</span></span> 

<span data-ttu-id="c4f4a-141">Stream Analytics가 이벤트 순서 이상을 수정하도록 하려면 0이 아닌 잘못된 순서 허용 시간을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-141">To allow Stream Analytics to correct an event misorder, you can specify a non-zero out-of-order tolerance window.</span></span> <span data-ttu-id="c4f4a-142">Stream Analytics는 이벤트를 해당 창까지 버퍼링한 다음 사용자가 선택한 타임스탬프를 사용하여 순서를 다시 정렬합니다.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-142">Stream Analytics buffers events up to that window, and then reorders them by using the timestamp you chose.</span></span> <span data-ttu-id="c4f4a-143">그런 다음 임시 변환을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-143">It then applies the temporal transformation.</span></span> <span data-ttu-id="c4f4a-144">3초 창에서 시작할 수 있으며 값을 조정하여 시간이 조정된 이벤트의 수를 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-144">You can start with a 3-second window, and tune the value to reduce the number of events that are time-adjusted.</span></span> 

<span data-ttu-id="c4f4a-145">버퍼링의 부작용은 출력이 **동일한 시간만큼 지연**된다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-145">A side effect of the buffering is that the output is **delayed by the same amount of time**.</span></span> <span data-ttu-id="c4f4a-146">값을 조정하여 잘못된 순서 이벤트의 수를 줄이고 작업 대기 시간을 낮게 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-146">You can tune the value to reduce the number of out-of-order events, and keep the job latency low.</span></span>

## <a name="get-help"></a><span data-ttu-id="c4f4a-147">도움말 보기</span><span class="sxs-lookup"><span data-stu-id="c4f4a-147">Get help</span></span>
<span data-ttu-id="c4f4a-148">추가 지원이 필요한 경우 [Azure Stream Analytics 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-148">For additional assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c4f4a-149">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c4f4a-149">Next steps</span></span>
* [<span data-ttu-id="c4f4a-150">Stream Analytics 소개</span><span class="sxs-lookup"><span data-stu-id="c4f4a-150">Introduction to Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="c4f4a-151">Stream Analytics 시작</span><span class="sxs-lookup"><span data-stu-id="c4f4a-151">Get started with Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="c4f4a-152">Stream Analytics 작업 크기 조정</span><span class="sxs-lookup"><span data-stu-id="c4f4a-152">Scale Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="c4f4a-153">Stream Analytics 쿼리 언어 참조</span><span class="sxs-lookup"><span data-stu-id="c4f4a-153">Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="c4f4a-154">Stream Analytics 관리 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="c4f4a-154">Stream Analytics management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
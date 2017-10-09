---
title: "aaaHandling 이벤트 순서와 Azure 스트림 분석에 포함 | Microsoft Docs"
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
ms.openlocfilehash: 87c028662fbafbf4f72f57f215d017f65bb649f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stream-analytics-event-order-handling"></a><span data-ttu-id="116c3-104">Azure Stream Analytics 이벤트 순서 처리</span><span class="sxs-lookup"><span data-stu-id="116c3-104">Azure Stream Analytics event order handling</span></span>

<span data-ttu-id="116c3-105">이벤트의 임시 데이터 스트림의 각 이벤트를 기록 해당 hello 이벤트를 받을 hello 시간을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="116c3-105">In a temporal data stream of events, each event is recorded with hello time that hello event is received.</span></span> <span data-ttu-id="116c3-106">일부 조건 보다는 전송 된 대로 다른 순서로 toooccasionally 수신 하는 이벤트 스트림을 일부 이벤트를 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="116c3-106">Some conditions might cause event streams toooccasionally receive some events in a different order than which they were sent.</span></span> <span data-ttu-id="116c3-107">간단한 TCP 재전송 하거나 전송 장치와 이벤트 허브를 수신 하는 hello hello 간에 클럭 오차가이 toooccur 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="116c3-107">A simple TCP retransmit, or even a clock skew between hello sending device and hello receiving event hub might cause this toooccur.</span></span> <span data-ttu-id="116c3-108">"문장 부호"도 추가 된 이벤트 tooreceived 이벤트 스트림을 이벤트 도착 hello 없으면에서 tooadvance hello 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="116c3-108">“Punctuation” events also are added tooreceived event streams, tooadvance hello time in hello absence of event arrivals.</span></span> <span data-ttu-id="116c3-109">이러한 사항은 “3분 동안 로그인이 발생하지 않을 때 알림”과 같은 시나리오에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="116c3-109">These are needed in scenarios like “Notify me when no logins occur for 3 minutes."</span></span>

<span data-ttu-id="116c3-110">순서가 올바르지 않은 입력 스트림은 다음 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="116c3-110">Input streams that are not in order are either:</span></span>
* <span data-ttu-id="116c3-111">정렬되었습니다(따라서 **지연됨**).</span><span class="sxs-lookup"><span data-stu-id="116c3-111">Sorted (and therefore **delayed**).</span></span>
* <span data-ttu-id="116c3-112">시스템 hello tooa 사용자 지정 정책에 따라 조정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="116c3-112">Adjusted by hello system, according tooa user-specified policy.</span></span>


## <a name="lateness-tolerance"></a><span data-ttu-id="116c3-113">지연 허용 오차</span><span class="sxs-lookup"><span data-stu-id="116c3-113">Lateness tolerance</span></span>
<span data-ttu-id="116c3-114">Stream Analytics는 이러한 시나리오 형식을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="116c3-114">Stream Analytics tolerates these types of scenarios.</span></span> <span data-ttu-id="116c3-115">Stream Analytics는 “잘못된 순서” 및 “지연” 이벤트를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="116c3-115">Stream Analytics has handling for "out-of-order" and "late" events.</span></span> <span data-ttu-id="116c3-116">다음 방법으로 hello에서 이러한 이벤트를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="116c3-116">It handles these events in hello following ways:</span></span>

* <span data-ttu-id="116c3-117">잘못 된 순서로 도착 하지만 hello 내에서 허용 오차를 설정 하는 이벤트는 **타임 스탬프 순서를 조정할**합니다.</span><span class="sxs-lookup"><span data-stu-id="116c3-117">Events that arrive out of order but within hello set tolerance are **reordered by timestamp**.</span></span>
* <span data-ttu-id="116c3-118">허용 오차보다 나중에 도착하는 이벤트는 **삭제 또는 조정**합니다.</span><span class="sxs-lookup"><span data-stu-id="116c3-118">Events that arrive later than tolerance are **dropped or adjusted**.</span></span>
    * <span data-ttu-id="116c3-119">**조정**: 조정 된 tooappear toohave 최신 허용 가능한 시간 hello에 도착 합니다.</span><span class="sxs-lookup"><span data-stu-id="116c3-119">**Adjusted**: Adjusted tooappear toohave arrived at hello latest acceptable time.</span></span>
    * <span data-ttu-id="116c3-120">**삭제**: 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="116c3-120">**Dropped**: Discarded.</span></span>

![Stream Analytics 이벤트 처리](media/stream-analytics-event-handling/stream-analytics-event-handling.png)

## <a name="reduce-hello-number-of-out-of-order-events"></a><span data-ttu-id="116c3-122">이벤트의 순서가 hello 수 줄이기</span><span class="sxs-lookup"><span data-stu-id="116c3-122">Reduce hello number of out-of-order events</span></span>

<span data-ttu-id="116c3-123">Stream Analytics는 들어오는 이벤트를 처리할 때 임시 변환을 적용하기 때문에(예: 기간 이동 집계 또는 임시 연결) Stream Analytics는 들어오는 이벤트를 타임스탬프 순서대로 정렬합니다.</span><span class="sxs-lookup"><span data-stu-id="116c3-123">Because Stream Analytics applies a temporal transformation when it processes incoming events (for example, for windowed aggregates or temporal joins), Stream Analytics sorts incoming events by timestamp order.</span></span>

<span data-ttu-id="116c3-124">하 여 hello "timestamp" 키워드의 경우 **하지** 을 사용 하는 hello Azure 이벤트 허브 이벤트 큐에 넣지 시간이 기본적으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="116c3-124">When hello “timestamp by” keyword is **not** used, hello Azure Event Hubs event enqueue time is used by default.</span></span> <span data-ttu-id="116c3-125">이벤트 허브 단 조성에 hello 이벤트 허브의 각 파티션에 대해 hello 타임 스탬프를 보장 합니다.</span><span class="sxs-lookup"><span data-stu-id="116c3-125">Event Hubs guarantees monotonicity of hello timestamp on each partition of hello event hub.</span></span> <span data-ttu-id="116c3-126">또한 모든 파티션의 이벤트가 타임스탬프 순서대로 병합되는 것을 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="116c3-126">It also guarantees that events from all partitions will be merged in timestamp order.</span></span> <span data-ttu-id="116c3-127">이러한 두 이벤트 허브 보증을 통해 잘못된 순서 이벤트를 없앨 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="116c3-127">These two Event Hubs guarantees ensure no out-of-order events.</span></span>

<span data-ttu-id="116c3-128">경우에 따라이 하면 toouse hello 보낸 사람의 타임 스탬프 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="116c3-128">Sometimes, it’s important for you toouse hello sender’s timestamp.</span></span> <span data-ttu-id="116c3-129">"하 여 타임 스탬프입니다."를 사용 하 여 hello 이벤트 페이로드의 타임 스탬프를 선택 하는 경우</span><span class="sxs-lookup"><span data-stu-id="116c3-129">In that case, a timestamp from hello event payload is chosen by using “timestamp by.”</span></span> <span data-ttu-id="116c3-130">이러한 시나리오에서는 잘못 정렬된 이벤트의 원본이 하나 이상 도입될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="116c3-130">In these scenarios, one or more sources of event misorder might be introduced:</span></span>

* <span data-ttu-id="116c3-131">이벤트 생산자에 클록 오차가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="116c3-131">Event producers have clock skews.</span></span> <span data-ttu-id="116c3-132">이는 생산자가 다른 컴퓨터에 있어 다른 클록을 사용할 때 일반적입니다.</span><span class="sxs-lookup"><span data-stu-id="116c3-132">This is common when producers are from different computers, so they have different clocks.</span></span>
* <span data-ttu-id="116c3-133">Hello 이벤트 toohello 대상 이벤트 허브의 hello 소스에서 네트워크 지연이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="116c3-133">There's a network delay from hello source of hello events toohello destination event hub.</span></span>
* <span data-ttu-id="116c3-134">클록 오차는 이벤트 허브 파티션 간에 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="116c3-134">Clock skews exist between event hub partitions.</span></span> <span data-ttu-id="116c3-135">Stream Analytics는 먼저 모든 이벤트 허브 파티션의 이벤트를 이벤트 큐에 넣기 시간으로 정렬합니다.</span><span class="sxs-lookup"><span data-stu-id="116c3-135">Stream Analytics first sorts events from all event hub partitions by event enqueue time.</span></span> <span data-ttu-id="116c3-136">그런 다음 hello 데이터 스트림에 잘못 된 이벤트를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="116c3-136">Then, it examines hello data stream for misordered events.</span></span>

<span data-ttu-id="116c3-137">Hello 구성 탭에서 다음 기본값 hello를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="116c3-137">On hello configuration tab, you see hello following defaults:</span></span>

![Stream Analytics의 잘못된 순서 처리](media/stream-analytics-event-handling/stream-analytics-out-of-order-handling.png)

<span data-ttu-id="116c3-139">Hello 순서가의 허용 시간으로 0 초를 사용 하는 경우 모든 이벤트는 항상 hello에 순서 대로 어설션하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="116c3-139">If you use 0 seconds as hello out-of-order tolerance window, you are asserting that all events are in order all hello time.</span></span> <span data-ttu-id="116c3-140">잘못 된 이벤트 hello 3 소스가 들어 그럴 가능성은 true 임을 합니다.</span><span class="sxs-lookup"><span data-stu-id="116c3-140">Given hello three sources of misordered events, it’s unlikely that this is true.</span></span> 

<span data-ttu-id="116c3-141">tooallow 스트림 분석 toocorrect 이벤트 misorder, 0이 아닌 값의 순서가 허용 시간을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="116c3-141">tooallow Stream Analytics toocorrect an event misorder, you can specify a non-zero out-of-order tolerance window.</span></span> <span data-ttu-id="116c3-142">스트림 분석 버퍼 이벤트 toothat 창 및 다음 선택한 timestamp 안녕을 사용 하 여 순서를 재정렬 합니다.</span><span class="sxs-lookup"><span data-stu-id="116c3-142">Stream Analytics buffers events up toothat window, and then reorders them by using hello timestamp you chose.</span></span> <span data-ttu-id="116c3-143">다음 hello 임시 변환을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="116c3-143">It then applies hello temporal transformation.</span></span> <span data-ttu-id="116c3-144">3 초 창 시작 하며 hello 값 tooreduce hello 번호 시간 조정 된 이벤트를 튜닝할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="116c3-144">You can start with a 3-second window, and tune hello value tooreduce hello number of events that are time-adjusted.</span></span> 

<span data-ttu-id="116c3-145">Hello 버퍼링의 부작용은 hello 출력 **hello 동일 지연 시간**합니다.</span><span class="sxs-lookup"><span data-stu-id="116c3-145">A side effect of hello buffering is that hello output is **delayed by hello same amount of time**.</span></span> <span data-ttu-id="116c3-146">순서가 이벤트 hello 값 tooreduce hello 수를 조정 하 고 hello 작업 대기 시간을 낮게 유지 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="116c3-146">You can tune hello value tooreduce hello number of out-of-order events, and keep hello job latency low.</span></span>

## <a name="get-help"></a><span data-ttu-id="116c3-147">도움말 보기</span><span class="sxs-lookup"><span data-stu-id="116c3-147">Get help</span></span>
<span data-ttu-id="116c3-148">추가 지원이 필요한 경우 [Azure Stream Analytics 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="116c3-148">For additional assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="116c3-149">다음 단계</span><span class="sxs-lookup"><span data-stu-id="116c3-149">Next steps</span></span>
* [<span data-ttu-id="116c3-150">소개 tooStream 분석</span><span class="sxs-lookup"><span data-stu-id="116c3-150">Introduction tooStream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="116c3-151">Stream Analytics 시작</span><span class="sxs-lookup"><span data-stu-id="116c3-151">Get started with Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="116c3-152">Stream Analytics 작업 크기 조정</span><span class="sxs-lookup"><span data-stu-id="116c3-152">Scale Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="116c3-153">Stream Analytics 쿼리 언어 참조</span><span class="sxs-lookup"><span data-stu-id="116c3-153">Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="116c3-154">Stream Analytics 관리 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="116c3-154">Stream Analytics management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
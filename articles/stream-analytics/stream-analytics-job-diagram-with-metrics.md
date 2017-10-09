---
title: "aaa Azure 스트림 분석 작업 다이어그램 hello를 사용 하 여 디버깅 데이터 기반 | Microsoft Docs"
description: "Hello 작업 다이어그램 및 메트릭을 사용 하 여 스트림 분석 작업을 해결 합니다."
keywords: 
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
ms.date: 05/01/2017
ms.author: jeffstok
ms.openlocfilehash: 1af884d485bebb06b034da01a13f7f8240516571
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="data-driven-debugging-by-using-hello-job-diagram"></a><span data-ttu-id="376f1-103">데이터 기반 작업 다이어그램 hello를 사용 하 여 디버깅</span><span class="sxs-lookup"><span data-stu-id="376f1-103">Data-driven debugging by using hello job diagram</span></span>

<span data-ttu-id="376f1-104">hello에 hello 작업 다이어그램 **모니터링** 블레이드 hello Azure 포털에서에서 작업 파이프라인을 시각화 하는 데 도움이 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="376f1-104">hello job diagram on hello **Monitoring** blade in hello Azure portal can help you visualize your job pipeline.</span></span> <span data-ttu-id="376f1-105">입력, 출력 및 쿼리 단계를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="376f1-105">It shows inputs, outputs, and query steps.</span></span> <span data-ttu-id="376f1-106">각 단계에 대 한 hello 작업 다이어그램 tooexamine hello 메트릭을 사용할 수 있는데, 문제를 해결할 때 신속 하 게 toomore hello 문제의 소스에 격리 합니다.</span><span class="sxs-lookup"><span data-stu-id="376f1-106">You can use hello job diagram tooexamine hello metrics for each step, toomore quickly isolate hello source of a problem when you troubleshoot issues.</span></span>

## <a name="using-hello-job-diagram"></a><span data-ttu-id="376f1-107">Hello 작업 다이어그램을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="376f1-107">Using hello job diagram</span></span>

<span data-ttu-id="376f1-108">Hello Azure 포털에에서 아래에서 스트림 분석 작업에 있는 동안 **지원 + 문제 해결**선택, **작업 다이어그램**:</span><span class="sxs-lookup"><span data-stu-id="376f1-108">In hello Azure portal, while in a Stream Analytics job, under **SUPPORT + TROUBLESHOOTING**, select **Job diagram**:</span></span>

![메트릭이 있는 작업 다이어그램 - 위치](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-1.png)

<span data-ttu-id="376f1-110">쿼리 편집 창에서에서 각 쿼리 단계 toosee hello 해당 섹션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="376f1-110">Select each query step toosee hello corresponding section in a query editing pane.</span></span> <span data-ttu-id="376f1-111">Hello 단계에 대 한 메트릭 차트는 hello 페이지의 아래쪽 창에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="376f1-111">A metric chart for hello step is displayed in a lower pane on hello page.</span></span>

![메트릭이 있는 작업 다이어그램 - 기본 작업](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-2.png)

<span data-ttu-id="376f1-113">hello Azure 이벤트 허브 입력의 toosee hello 파티션을 선택 **중...**</span><span class="sxs-lookup"><span data-stu-id="376f1-113">toosee hello partitions of hello Azure Event Hubs input, select **. . .**</span></span> <span data-ttu-id="376f1-114">상황에 맞는 메뉴가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="376f1-114">A context menu appears.</span></span> <span data-ttu-id="376f1-115">또한 hello 입력된 병합기를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="376f1-115">You also can see hello input merger.</span></span>

![메트릭이 있는 작업 다이어그램 - 파티션 확장](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-3.png)

<span data-ttu-id="376f1-117">만 단일 파티션의 경우 파티션 노드 선택 hello toosee hello의 메트릭 차트입니다.</span><span class="sxs-lookup"><span data-stu-id="376f1-117">toosee hello metric chart for only a single partition, select hello partition node.</span></span> <span data-ttu-id="376f1-118">hello 메트릭 hello hello 페이지 맨 아래에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="376f1-118">hello metrics are shown at hello bottom of hello page.</span></span>

![메트릭이 있는 작업 다이어그램 - 더 많은 메트릭](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-4.png)

<span data-ttu-id="376f1-120">hello 메트릭 차트를 toosee 선택 hello 합병 노드 병합에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="376f1-120">toosee hello metrics chart for a merger, select hello merger node.</span></span> <span data-ttu-id="376f1-121">다음 차트 hello 이벤트가 제거 되거나 조정 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="376f1-121">hello following chart shows that no events were dropped or adjusted.</span></span>

![메트릭이 있는 작업 다이어그램 - 그리드](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-5.png)

<span data-ttu-id="376f1-123">toosee hello hello 메트릭 값 및 시간을 지점 toohello 차트의 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="376f1-123">toosee hello details of hello metric value and time, point toohello chart.</span></span>

![메트릭이 있는 작업 다이어그램 - 커서 올리기](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-6.png)

## <a name="troubleshoot-by-using-metrics"></a><span data-ttu-id="376f1-125">메트릭을 사용하여 문제 해결</span><span class="sxs-lookup"><span data-stu-id="376f1-125">Troubleshoot by using metrics</span></span>

<span data-ttu-id="376f1-126">hello **QueryLastProcessedTime** 메트릭을 특정 단계에서 데이터를 수신 하는 때를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="376f1-126">hello **QueryLastProcessedTime** metric indicates when a specific step received data.</span></span> <span data-ttu-id="376f1-127">Hello 토폴로지를 살펴보면에서 작업할 수 있습니다 뒤로 hello 출력 프로세서 toosee 단계 데이터를 받고 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="376f1-127">By looking at hello topology, you can work backward from hello output processor toosee which step is not receiving data.</span></span> <span data-ttu-id="376f1-128">단계 데이터를 수신 하지 않고 바로 앞 toohello 쿼리 단계를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="376f1-128">If a step is not getting data, go toohello query step just before it.</span></span> <span data-ttu-id="376f1-129">Hello 위의 쿼리 단계에는 시간 창 고에 대 한 충분 한 시간이 경과 하는 경우 toooutput 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="376f1-129">Check whether hello preceding query step has a time window, and if enough time has passed for it toooutput data.</span></span> <span data-ttu-id="376f1-130">(참고 당시 창이 있는 맞춰진된 toohello 시간입니다.)</span><span class="sxs-lookup"><span data-stu-id="376f1-130">(Note that time windows are snapped toohello hour.)</span></span>
 
<span data-ttu-id="376f1-131">이면 hello 이전 쿼리 단계에서 입력된 프로세서 사용 하 여 hello 입력된 된 메트릭 toohelp 응답 hello 다음 질문의 대상입니다.</span><span class="sxs-lookup"><span data-stu-id="376f1-131">If hello preceding query step is an input processor, use hello input metrics toohelp answer hello following targeted questions.</span></span> <span data-ttu-id="376f1-132">이는 입력 소스에서 데이터를 가져오는 작업인지 판단하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="376f1-132">They can help you determine whether a job is getting data from its input sources.</span></span> <span data-ttu-id="376f1-133">Hello 쿼리를 분할 하는 경우 각 파티션에 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="376f1-133">If hello query is partitioned, examine each partition.</span></span>
 
### <a name="how-much-data-is-being-read"></a><span data-ttu-id="376f1-134">얼마나 많은 데이터를 읽습니까?</span><span class="sxs-lookup"><span data-stu-id="376f1-134">How much data is being read?</span></span>

*   <span data-ttu-id="376f1-135">**InputEventsSourcesTotal** hello 읽을 데이터 단위 수입니다.</span><span class="sxs-lookup"><span data-stu-id="376f1-135">**InputEventsSourcesTotal** is hello number of data units read.</span></span> <span data-ttu-id="376f1-136">예를 들어 hello blob 수입니다.</span><span class="sxs-lookup"><span data-stu-id="376f1-136">For example, hello number of blobs.</span></span>
*   <span data-ttu-id="376f1-137">**InputEventsTotal** hello 읽은 이벤트 수입니다.</span><span class="sxs-lookup"><span data-stu-id="376f1-137">**InputEventsTotal** is hello number of events read.</span></span> <span data-ttu-id="376f1-138">이 메트릭은 각 파티션에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="376f1-138">This metric is available per partition.</span></span>
*   <span data-ttu-id="376f1-139">**InputEventsInBytesTotal** hello 읽은 바이트 수입니다.</span><span class="sxs-lookup"><span data-stu-id="376f1-139">**InputEventsInBytesTotal** is hello number of bytes read.</span></span>
*   <span data-ttu-id="376f1-140">**InputEventsLastArrivalTime**은 수신된 모든 이벤트의 큐에 넣은 시간과 함께 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="376f1-140">**InputEventsLastArrivalTime** is updated with every received event's enqueued time.</span></span>
 
### <a name="is-time-moving-forward-if-actual-events-are-read-punctuation-might-not-be-issued"></a><span data-ttu-id="376f1-141">시간은 앞으로 진행됩니까?</span><span class="sxs-lookup"><span data-stu-id="376f1-141">Is time moving forward?</span></span> <span data-ttu-id="376f1-142">실제 이벤트를 읽는 경우 문장 부호가 발생하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="376f1-142">If actual events are read, punctuation might not be issued.</span></span>

*   <span data-ttu-id="376f1-143">**InputEventsLastPunctuationTime** 경우 문장 부호 명령이 실행 되었음을 나타냅니다 tookeep 시간 이동 앞으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="376f1-143">**InputEventsLastPunctuationTime** indicates when a punctuation was issued tookeep time moving forward.</span></span> <span data-ttu-id="376f1-144">문장 부호가 발생하지 않는 경우 데이터 흐름을 차단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="376f1-144">If punctuation is not issued, data flow can get blocked.</span></span>
 
### <a name="are-there-any-errors-in-hello-input"></a><span data-ttu-id="376f1-145">Hello 입력에 오류 사항이 있습니까?</span><span class="sxs-lookup"><span data-stu-id="376f1-145">Are there any errors in hello input?</span></span>

*   <span data-ttu-id="376f1-146">**InputEventsEventDataNullTotal**은 null 데이터가 있는 이벤트의 개수입니다.</span><span class="sxs-lookup"><span data-stu-id="376f1-146">**InputEventsEventDataNullTotal** is a count of events that have null data.</span></span>
*   <span data-ttu-id="376f1-147">**InputEventsSerializerErrorsTotal**은 올바르게 deserialize할 수 없는 이벤트의 개수입니다.</span><span class="sxs-lookup"><span data-stu-id="376f1-147">**InputEventsSerializerErrorsTotal** is a count of events that could not be deserialized correctly.</span></span>
*   <span data-ttu-id="376f1-148">**InputEventsDegradedTotal**은 deserialization이 아닌 다른 문제가 있는 이벤트의 개수입니다.</span><span class="sxs-lookup"><span data-stu-id="376f1-148">**InputEventsDegradedTotal** is a count of events that had an issue other than with deserialization.</span></span>
 
### <a name="are-events-being-dropped-or-adjusted"></a><span data-ttu-id="376f1-149">이벤트 삭제되거나 조정됩니까?</span><span class="sxs-lookup"><span data-stu-id="376f1-149">Are events being dropped or adjusted?</span></span>

*   <span data-ttu-id="376f1-150">**InputEventsEarlyTotal** hello hello 상위 워터 마크 하기 전에 응용 프로그램 타임 스탬프에 있는 이벤트 수입니다.</span><span class="sxs-lookup"><span data-stu-id="376f1-150">**InputEventsEarlyTotal** is hello number of events that have an application timestamp before hello high watermark.</span></span>
*   <span data-ttu-id="376f1-151">**InputEventsLateTotal** hello는 hello 상위 워터 마크 이후는 응용 프로그램 타임 스탬프를 제공 하는 이벤트 수입니다.</span><span class="sxs-lookup"><span data-stu-id="376f1-151">**InputEventsLateTotal** is hello number of events that have an application timestamp after hello high watermark.</span></span>
*   <span data-ttu-id="376f1-152">**InputEventsDroppedBeforeApplicationStartTimeTotal** hello 숫자 이벤트 hello 작업 시작 시간을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="376f1-152">**InputEventsDroppedBeforeApplicationStartTimeTotal** is hello number events dropped before hello job start time.</span></span>
 
### <a name="are-we-falling-behind-in-reading-data"></a><span data-ttu-id="376f1-153">데이터를 읽을 때 뒤쳐지고 있습니까?</span><span class="sxs-lookup"><span data-stu-id="376f1-153">Are we falling behind in reading data?</span></span>

*   <span data-ttu-id="376f1-154">**InputEventsSourcesBackloggedTotal** 수가 더 많은 메시지 필요한 toobe 알려줍니다 Azure IoT Hub 및 이벤트 허브 입력에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="376f1-154">**InputEventsSourcesBackloggedTotal** tells you how many more messages need toobe read for Event Hubs and Azure IoT Hub inputs.</span></span>


## <a name="get-help"></a><span data-ttu-id="376f1-155">도움말 보기</span><span class="sxs-lookup"><span data-stu-id="376f1-155">Get help</span></span>
<span data-ttu-id="376f1-156">추가 지원이 필요한 경우 [Azure Stream Analytics 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="376f1-156">For additional assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="376f1-157">다음 단계</span><span class="sxs-lookup"><span data-stu-id="376f1-157">Next steps</span></span>
* [<span data-ttu-id="376f1-158">소개 tooStream 분석</span><span class="sxs-lookup"><span data-stu-id="376f1-158">Introduction tooStream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="376f1-159">Stream Analytics 시작</span><span class="sxs-lookup"><span data-stu-id="376f1-159">Get started with Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="376f1-160">Stream Analytics 작업 크기 조정</span><span class="sxs-lookup"><span data-stu-id="376f1-160">Scale Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="376f1-161">Stream Analytics 쿼리 언어 참조</span><span class="sxs-lookup"><span data-stu-id="376f1-161">Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="376f1-162">Stream Analytics 관리 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="376f1-162">Stream Analytics management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

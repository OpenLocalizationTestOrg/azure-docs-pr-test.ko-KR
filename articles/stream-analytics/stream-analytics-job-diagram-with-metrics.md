---
title: "작업 다이어그램을 사용하여 Azure Stream Analytics 데이터 기반 디버그 | Microsoft Docs"
description: "작업 다이어그램 및 메트릭을 사용하여 Stream Analytics 작업 문제를 해결합니다."
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
ms.openlocfilehash: 4e5949232e8377b7697eaebf96eacdc31c4f5422
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="data-driven-debugging-by-using-the-job-diagram"></a><span data-ttu-id="31e91-103">작업 다이어그램을 사용하여 데이터 기반 디버그</span><span class="sxs-lookup"><span data-stu-id="31e91-103">Data-driven debugging by using the job diagram</span></span>

<span data-ttu-id="31e91-104">Azure Portal의 **모니터링** 블레이드에 있는 작업 다이어그램은 작업 파이프라인을 시각화하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31e91-104">The job diagram on the **Monitoring** blade in the Azure portal can help you visualize your job pipeline.</span></span> <span data-ttu-id="31e91-105">입력, 출력 및 쿼리 단계를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="31e91-105">It shows inputs, outputs, and query steps.</span></span> <span data-ttu-id="31e91-106">작업 다이어그램을 사용하여 각 단계의 메트릭을 검사하면 문제를 해결할 때 문제의 원인을 더 빠르게 격리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31e91-106">You can use the job diagram to examine the metrics for each step, to more quickly isolate the source of a problem when you troubleshoot issues.</span></span>

## <a name="using-the-job-diagram"></a><span data-ttu-id="31e91-107">작업 다이어그램 사용</span><span class="sxs-lookup"><span data-stu-id="31e91-107">Using the job diagram</span></span>

<span data-ttu-id="31e91-108">Azure Portal에서 Stream Analytics 작업 동안에 **지원 + 문제 해결**에서 **작업 다이어그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="31e91-108">In the Azure portal, while in a Stream Analytics job, under **SUPPORT + TROUBLESHOOTING**, select **Job diagram**:</span></span>

![메트릭이 있는 작업 다이어그램 - 위치](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-1.png)

<span data-ttu-id="31e91-110">쿼리 편집 창에서 각 쿼리 단계를 선택하여 해당하는 섹션을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="31e91-110">Select each query step to see the corresponding section in a query editing pane.</span></span> <span data-ttu-id="31e91-111">단계에 해당하는 메트릭 차트가 페이지 아래쪽 창에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="31e91-111">A metric chart for the step is displayed in a lower pane on the page.</span></span>

![메트릭이 있는 작업 다이어그램 - 기본 작업](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-2.png)

<span data-ttu-id="31e91-113">Azure Event Hubs 입력의 파티션을 보려면 **. . .**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="31e91-113">To see the partitions of the Azure Event Hubs input, select **. . .**</span></span> <span data-ttu-id="31e91-114">상황에 맞는 메뉴가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="31e91-114">A context menu appears.</span></span> <span data-ttu-id="31e91-115">또한 입력된 합병을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31e91-115">You also can see the input merger.</span></span>

![메트릭이 있는 작업 다이어그램 - 파티션 확장](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-3.png)

<span data-ttu-id="31e91-117">단일 파티션에만 해당하는 메트릭 차트를 보려면 파티션 노드를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="31e91-117">To see the metric chart for only a single partition, select the partition node.</span></span> <span data-ttu-id="31e91-118">메트릭이 페이지의 맨 아래에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="31e91-118">The metrics are shown at the bottom of the page.</span></span>

![메트릭이 있는 작업 다이어그램 - 더 많은 메트릭](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-4.png)

<span data-ttu-id="31e91-120">병합에 대한 메트릭 차트를 보려면 병합 노드를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="31e91-120">To see the metrics chart for a merger, select the merger node.</span></span> <span data-ttu-id="31e91-121">다음 차트는 이벤트가 삭제되거나 조정되지 않았음을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="31e91-121">The following chart shows that no events were dropped or adjusted.</span></span>

![메트릭이 있는 작업 다이어그램 - 그리드](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-5.png)

<span data-ttu-id="31e91-123">메트릭 값과 시간에 대한 세부 정보를 보려면 차트를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="31e91-123">To see the details of the metric value and time, point to the chart.</span></span>

![메트릭이 있는 작업 다이어그램 - 커서 올리기](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-6.png)

## <a name="troubleshoot-by-using-metrics"></a><span data-ttu-id="31e91-125">메트릭을 사용하여 문제 해결</span><span class="sxs-lookup"><span data-stu-id="31e91-125">Troubleshoot by using metrics</span></span>

<span data-ttu-id="31e91-126">**QueryLastProcessedTime** 메트릭은 특정 단계가 데이터를 수신하는 시간을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="31e91-126">The **QueryLastProcessedTime** metric indicates when a specific step received data.</span></span> <span data-ttu-id="31e91-127">토폴로지를 찾아 출력 프로세서부터 거꾸로 작업하여 어떤 단계가 데이터를 수신하지 않는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31e91-127">By looking at the topology, you can work backward from the output processor to see which step is not receiving data.</span></span> <span data-ttu-id="31e91-128">단계가 데이터를 수신하지 않은 경우 바로 전 쿼리 단계로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="31e91-128">If a step is not getting data, go to the query step just before it.</span></span> <span data-ttu-id="31e91-129">이전 쿼리 단계에 시간 창이 있는지, 그리고 데이터가 출력되기에 충분한 시간이 경과하였는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="31e91-129">Check whether the preceding query step has a time window, and if enough time has passed for it to output data.</span></span> <span data-ttu-id="31e91-130">(시간 창은 시간으로 스냅됨)</span><span class="sxs-lookup"><span data-stu-id="31e91-130">(Note that time windows are snapped to the hour.)</span></span>
 
<span data-ttu-id="31e91-131">이전 쿼리 단계가 입력 프로세서인 경우 입력 메트릭을 사용하여 다음과 같은 대상 질문에 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="31e91-131">If the preceding query step is an input processor, use the input metrics to help answer the following targeted questions.</span></span> <span data-ttu-id="31e91-132">이는 입력 소스에서 데이터를 가져오는 작업인지 판단하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="31e91-132">They can help you determine whether a job is getting data from its input sources.</span></span> <span data-ttu-id="31e91-133">쿼리가 분할된 경우 각 파티션을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="31e91-133">If the query is partitioned, examine each partition.</span></span>
 
### <a name="how-much-data-is-being-read"></a><span data-ttu-id="31e91-134">얼마나 많은 데이터를 읽습니까?</span><span class="sxs-lookup"><span data-stu-id="31e91-134">How much data is being read?</span></span>

*   <span data-ttu-id="31e91-135">**InputEventsSourcesTotal**은 읽는 데이터 단위 수입니다.</span><span class="sxs-lookup"><span data-stu-id="31e91-135">**InputEventsSourcesTotal** is the number of data units read.</span></span> <span data-ttu-id="31e91-136">예를 들어 Blob의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="31e91-136">For example, the number of blobs.</span></span>
*   <span data-ttu-id="31e91-137">**InputEventsTotal**은 읽는 이벤트의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="31e91-137">**InputEventsTotal** is the number of events read.</span></span> <span data-ttu-id="31e91-138">이 메트릭은 각 파티션에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31e91-138">This metric is available per partition.</span></span>
*   <span data-ttu-id="31e91-139">**InputEventsInBytesTotal**은 읽는 바이트 수입니다.</span><span class="sxs-lookup"><span data-stu-id="31e91-139">**InputEventsInBytesTotal** is the number of bytes read.</span></span>
*   <span data-ttu-id="31e91-140">**InputEventsLastArrivalTime**은 수신된 모든 이벤트의 큐에 넣은 시간과 함께 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="31e91-140">**InputEventsLastArrivalTime** is updated with every received event's enqueued time.</span></span>
 
### <a name="is-time-moving-forward-if-actual-events-are-read-punctuation-might-not-be-issued"></a><span data-ttu-id="31e91-141">시간은 앞으로 진행됩니까?</span><span class="sxs-lookup"><span data-stu-id="31e91-141">Is time moving forward?</span></span> <span data-ttu-id="31e91-142">실제 이벤트를 읽는 경우 문장 부호가 발생하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31e91-142">If actual events are read, punctuation might not be issued.</span></span>

*   <span data-ttu-id="31e91-143">**InputEventsLastPunctuationTime**은 시간이 앞으로 진행하도록 문장 부호가 발생한 경우를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="31e91-143">**InputEventsLastPunctuationTime** indicates when a punctuation was issued to keep time moving forward.</span></span> <span data-ttu-id="31e91-144">문장 부호가 발생하지 않는 경우 데이터 흐름을 차단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31e91-144">If punctuation is not issued, data flow can get blocked.</span></span>
 
### <a name="are-there-any-errors-in-the-input"></a><span data-ttu-id="31e91-145">입력에 오류가 있습니까?</span><span class="sxs-lookup"><span data-stu-id="31e91-145">Are there any errors in the input?</span></span>

*   <span data-ttu-id="31e91-146">**InputEventsEventDataNullTotal**은 null 데이터가 있는 이벤트의 개수입니다.</span><span class="sxs-lookup"><span data-stu-id="31e91-146">**InputEventsEventDataNullTotal** is a count of events that have null data.</span></span>
*   <span data-ttu-id="31e91-147">**InputEventsSerializerErrorsTotal**은 올바르게 deserialize할 수 없는 이벤트의 개수입니다.</span><span class="sxs-lookup"><span data-stu-id="31e91-147">**InputEventsSerializerErrorsTotal** is a count of events that could not be deserialized correctly.</span></span>
*   <span data-ttu-id="31e91-148">**InputEventsDegradedTotal**은 deserialization이 아닌 다른 문제가 있는 이벤트의 개수입니다.</span><span class="sxs-lookup"><span data-stu-id="31e91-148">**InputEventsDegradedTotal** is a count of events that had an issue other than with deserialization.</span></span>
 
### <a name="are-events-being-dropped-or-adjusted"></a><span data-ttu-id="31e91-149">이벤트 삭제되거나 조정됩니까?</span><span class="sxs-lookup"><span data-stu-id="31e91-149">Are events being dropped or adjusted?</span></span>

*   <span data-ttu-id="31e91-150">**InputEventsEarlyTotal**은 상위 워터마크 전의 응용 프로그램 타임스탬프가 있는 이벤트 수입니다.</span><span class="sxs-lookup"><span data-stu-id="31e91-150">**InputEventsEarlyTotal** is the number of events that have an application timestamp before the high watermark.</span></span>
*   <span data-ttu-id="31e91-151">**InputEventsLateTotal**은 상위 워터마크 후의 응용 프로그램 타임스탬프가 있는 이벤트 수입니다.</span><span class="sxs-lookup"><span data-stu-id="31e91-151">**InputEventsLateTotal** is the number of events that have an application timestamp after the high watermark.</span></span>
*   <span data-ttu-id="31e91-152">**InputEventsDroppedBeforeApplicationStartTimeTotal**은 작업 시작 시간 전에 삭제된 숫자 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="31e91-152">**InputEventsDroppedBeforeApplicationStartTimeTotal** is the number events dropped before the job start time.</span></span>
 
### <a name="are-we-falling-behind-in-reading-data"></a><span data-ttu-id="31e91-153">데이터를 읽을 때 뒤쳐지고 있습니까?</span><span class="sxs-lookup"><span data-stu-id="31e91-153">Are we falling behind in reading data?</span></span>

*   <span data-ttu-id="31e91-154">**InputEventsSourcesBackloggedTotal**은 이벤트 허브 및 Azure IoT Hub 입력에 읽어야 하는 메시지가 얼마나 더 있는지를 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="31e91-154">**InputEventsSourcesBackloggedTotal** tells you how many more messages need to be read for Event Hubs and Azure IoT Hub inputs.</span></span>


## <a name="get-help"></a><span data-ttu-id="31e91-155">도움말 보기</span><span class="sxs-lookup"><span data-stu-id="31e91-155">Get help</span></span>
<span data-ttu-id="31e91-156">추가 지원이 필요한 경우 [Azure Stream Analytics 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31e91-156">For additional assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="31e91-157">다음 단계</span><span class="sxs-lookup"><span data-stu-id="31e91-157">Next steps</span></span>
* [<span data-ttu-id="31e91-158">Stream Analytics 소개</span><span class="sxs-lookup"><span data-stu-id="31e91-158">Introduction to Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="31e91-159">Stream Analytics 시작</span><span class="sxs-lookup"><span data-stu-id="31e91-159">Get started with Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="31e91-160">Stream Analytics 작업 크기 조정</span><span class="sxs-lookup"><span data-stu-id="31e91-160">Scale Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="31e91-161">Stream Analytics 쿼리 언어 참조</span><span class="sxs-lookup"><span data-stu-id="31e91-161">Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="31e91-162">Stream Analytics 관리 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="31e91-162">Stream Analytics management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

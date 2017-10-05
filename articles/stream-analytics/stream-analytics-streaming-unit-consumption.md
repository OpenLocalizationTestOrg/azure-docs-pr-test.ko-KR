---
title: "Azure Stream Analytics: 스트리밍 단위를 효율적으로 사용하도록 작업을 최적화 | Microsoft Docs"
description: "Azure Stream Analytics의 크기 조정 및 확장에 대한 모범 사례를 쿼리합니다."
keywords: "스트리밍 단위, 쿼리 성능"
services: stream-analytics
documentationcenter: 
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
ms.openlocfilehash: 1441a5df4fd92abf85763ca9a1512503b1a0da56
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="optimize-your-job-to-use-streaming-units-efficiently"></a><span data-ttu-id="ae8c6-104">스트리밍 단위를 효율적으로 사용하도록 작업을 최적화</span><span class="sxs-lookup"><span data-stu-id="ae8c6-104">Optimize your job to use Streaming Units efficiently</span></span>

<span data-ttu-id="ae8c6-105">Azure Stream Analytics는 실행하는 작업의 성능 "가중치"를 SU(스트림 단위)에 집계합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8c6-105">Azure Stream Analytics aggregates the performance "weight" of running a job into Streaming Units (SUs).</span></span> <span data-ttu-id="ae8c6-106">SU는 작업을 실행하는 데 사용하는 컴퓨팅 리소스를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ae8c6-106">SUs represent the computing resources that are consumed to execute a job.</span></span> <span data-ttu-id="ae8c6-107">SU는 CPU, 메모리의 혼합된 측정치 및 읽기/쓰기 속도를 기반으로 상대적 이벤트 처리 용량을 설명하는 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8c6-107">SUs provide a way to describe the relative event processing capacity based on a blended measure of CPU, memory, and read and write rates.</span></span> <span data-ttu-id="ae8c6-108">이 용량을 통해 사용자는 쿼리 논리에 집중할 수 있습니다. 또한 사용자가 저장소 계층 성능 고려 사항에 대해 알고, 작업에 대한 메모리를 수동으로 할당하고, 작업을 시기적절하게 실행하는 데 필요한 CPU 코어 수를 예상할 필요가 없어집니다.</span><span class="sxs-lookup"><span data-stu-id="ae8c6-108">This capacity lets you focus on the query logic and removes you from needing to know storage tier performance considerations, allocate memory for your job manually, and approximate the CPU core-count needed to run your job in a timely manner.</span></span>

## <a name="how-many-sus-are-required-for-a-job"></a><span data-ttu-id="ae8c6-109">작업에 필요한 SU 수는?</span><span class="sxs-lookup"><span data-stu-id="ae8c6-109">How many SUs are required for a job?</span></span>

<span data-ttu-id="ae8c6-110">특정 작업에 필요한 SU 수 선택은 입력에 대한 파티션 구성 및 작업에 정의된 쿼리에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="ae8c6-110">Choosing the number of required SUs for a particular job depends on the partition configuration for the inputs and the query that's defined within the job.</span></span> <span data-ttu-id="ae8c6-111">**규모** 블레이드를 사용하면 올바른 SU 수를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae8c6-111">The **Scale** blade allows you to set the right number of SUs.</span></span> <span data-ttu-id="ae8c6-112">필요한 것보다 많은 SU를 할당하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ae8c6-112">It is a best practice to allocate more SUs than needed.</span></span> <span data-ttu-id="ae8c6-113">Stream Analytics 처리 엔진은 메모리를 추가로 할당하는 비용으로 대기 시간과 처리량을 최적화합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8c6-113">The Stream Analytics processing engine optimizes for latency and throughput at the cost of allocating additional memory.</span></span>

<span data-ttu-id="ae8c6-114">일반적으로 *파티션 기준*을 사용하지 않는 쿼리에 대해 6 SU로 시작하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ae8c6-114">In general, the best practice is to start with 6 SUs for queries that don't use *PARTITION BY*.</span></span> <span data-ttu-id="ae8c6-115">그런 다음 대표적인 데이터 양을 전달하고 SU % 사용률 메트릭을 시험한 후 SU 수를 수정하는 평가판 및 오류 메서드를 사용하여 가장 적절한 부분을 판단합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8c6-115">Then determine the sweet spot by using a trial and error method in which you modify the number of SUs after you pass representative amounts of data and examine the SU %Utilization metric.</span></span>

<span data-ttu-id="ae8c6-116">Azure Stream Analytics는 처리를 시작하기 전에 “다시 정렬 버퍼”라는 창에 이벤트를 둡니다.</span><span class="sxs-lookup"><span data-stu-id="ae8c6-116">Azure Stream Analytics keeps events in a window called the “reorder buffer” before it starts any processing.</span></span> <span data-ttu-id="ae8c6-117">이벤트는 다시 정렬 창에 시간별로 정렬되며 후속 작업은 임시로 정렬된 이벤트에서 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae8c6-117">Events are sorted within the reorder window by time, and subsequent operations are performed on the temporally sorted events.</span></span> <span data-ttu-id="ae8c6-118">시간으로 다시 정렬된 이벤트를 통해 연산자는 규정된 시간 내에 모든 이벤트에 대한 가시성이 확보됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae8c6-118">Reordering events by time ensures that the operator has visibility into all the events in the stipulated timeframe.</span></span> <span data-ttu-id="ae8c6-119">또한 연산자는 필수 처리를 수행하고 출력을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae8c6-119">It also lets the operator perform the requisite processing and produce an output.</span></span> <span data-ttu-id="ae8c6-120">이 메커니즘의 부작용은 다시 정렬 창의 기간에 의해 처리가 지연되는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ae8c6-120">A side effect of this mechanism is that processing is delayed by the duration of the reorder window.</span></span> <span data-ttu-id="ae8c6-121">작업의 메모리 공간(SU 사용에 영향을 줌)은 이 다시 정렬 창의 크기와 창에 포함된 이벤트 수의 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="ae8c6-121">The memory footprint of the job (which affects SU consumption) is a function of the size of this reorder window and the number of events contained within it.</span></span>

> [!NOTE]
> <span data-ttu-id="ae8c6-122">작업을 업그레이드하는 동안 판독기 수가 변경되면 일시적인 경고가 감사 로그에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae8c6-122">When the number of readers changes during job upgrades, transient warnings are written to audit logs.</span></span> <span data-ttu-id="ae8c6-123">Stream Analytics 작업은 자동으로 이러한 일시적인 문제를 복구합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8c6-123">Stream Analytics jobs automatically recover from these transient issues.</span></span>

## <a name="common-high-memory-causes-for-high-su-usage-for-running-jobs"></a><span data-ttu-id="ae8c6-124">높은 공용 메모리로 인해 실행 중인 작업에 높은 SU 사용량 유발</span><span class="sxs-lookup"><span data-stu-id="ae8c6-124">Common high-memory causes for high SU usage for running jobs</span></span>

### <a name="high-cardinality-for-group-by"></a><span data-ttu-id="ae8c6-125">그룹화 기준에 대한 높은 카디널리티</span><span class="sxs-lookup"><span data-stu-id="ae8c6-125">High cardinality for GROUP BY</span></span>

<span data-ttu-id="ae8c6-126">들어오는 이벤트의 카디널리티는 작업에 대한 메모리 사용량을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8c6-126">The cardinality of incoming events dictates memory usage for the job.</span></span>

<span data-ttu-id="ae8c6-127">예를 들어 `SELECT count(*) from input group by clustered, tumblingwindow (minutes, 5)`에서 **클러스터**와 연관된 번호는 쿼리의 카디널리티입니다.</span><span class="sxs-lookup"><span data-stu-id="ae8c6-127">For example, in `SELECT count(*) from input group by clustered, tumblingwindow (minutes, 5)`, the number associated with **clustered** is the cardinality of the query.</span></span>

<span data-ttu-id="ae8c6-128">높은 카디널리티에 의해 발생한 문제를 완화하려면 **파티션 기준**을 사용하여 파티션을 늘림으로써 쿼리의 규모를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8c6-128">To mitigate issues that are caused by high cardinality, scale out the query by increasing partitions using **PARTITION BY**.</span></span>

```
Select count(*) from input
Partition By clusterid
GROUP BY clustered tumblingwindow (minutes, 5)
```

<span data-ttu-id="ae8c6-129">*클러스터*의 수는 이 그룹화 기준의 카디널리티입니다.</span><span class="sxs-lookup"><span data-stu-id="ae8c6-129">The number of *clustered* is the cardinality of GROUP BY here.</span></span>

<span data-ttu-id="ae8c6-130">쿼리가 분할되면 여러 노드에 걸쳐 분산됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae8c6-130">After the query is partitioned, it is spread out over multiple nodes.</span></span> <span data-ttu-id="ae8c6-131">결과적으로, 각 노드로 들어오는 이벤트 수가 감소하여 다시 정렬 버퍼의 크기가 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="ae8c6-131">As a result, the number of events coming into each node is reduced, which in turn reduces the size of the reorder buffer.</span></span> <span data-ttu-id="ae8c6-132">또한 partitionid에 따라 이벤트 허브 파티션을 분할해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8c6-132">You should also partition event hub partitions by partitionid.</span></span>

### <a name="high-unmatched-event-count-for-join"></a><span data-ttu-id="ae8c6-133">JOIN에 대해 일치하지 않는 이벤트 개수가 많음</span><span class="sxs-lookup"><span data-stu-id="ae8c6-133">High unmatched event count for JOIN</span></span>

<span data-ttu-id="ae8c6-134">JOIN에서 일치하지 않는 이벤트 수는 쿼리에 대한 메모리 사용률에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ae8c6-134">The number of unmatched events in a JOIN affects the memory utilization of the query.</span></span> <span data-ttu-id="ae8c6-135">예를 들어 클릭을 유도하는 광고 노출 수를 찾는 쿼리를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8c6-135">For example, take a query that is looking to find the number of ad impressions that generates clicks:</span></span>

```
SELECT id from clicks INNER JOIN,
impressions on impressions.id = clicks.id AND DATEDIFF(hour, impressions, clicks) between 0 AND 10
```

<span data-ttu-id="ae8c6-136">이 시나리오에서 많은 광고가 표시되고 몇 번의 클릭이 생성될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae8c6-136">In this scenario, it is possible that many ads are shown and few clicks are generated.</span></span> <span data-ttu-id="ae8c6-137">작업이 시간 창 내에서 모든 이벤트를 유지해야 그러한 결과가 도출됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae8c6-137">Such a result would require the job to keep all the events within the time window.</span></span> <span data-ttu-id="ae8c6-138">사용된 메모리의 양은 창 크기 및 이벤트 속도에 비례합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8c6-138">The amount of memory consumed is proportional to the window size and event rate.</span></span> 

<span data-ttu-id="ae8c6-139">이 상황을 완화하려면 파티션 기준을 사용하여 파티션을 늘려서 쿼리의 규모를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8c6-139">To mitigate this situation, scale out the query by increasing partitions by using PARTITION BY.</span></span> 

<span data-ttu-id="ae8c6-140">쿼리가 분할되면 여러 처리 노드에 걸쳐 분산됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae8c6-140">After the query is partitioned, it is spread out over multiple processing nodes.</span></span> <span data-ttu-id="ae8c6-141">결과적으로, 각 노드로 들어오는 이벤트 수가 감소하여 다시 정렬 버퍼의 크기가 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="ae8c6-141">As a result, the number of events coming into each node is reduced, which in turn reduces the size of the reorder buffer.</span></span>

### <a name="large-number-of-out-of-order-events"></a><span data-ttu-id="ae8c6-142">순서가 잘못된 이벤트 수가 많음</span><span class="sxs-lookup"><span data-stu-id="ae8c6-142">Large number of out of order events</span></span> 

<span data-ttu-id="ae8c6-143">큰 시간 창에 순서가 잘못된 이벤트가 많으면 “다시 정렬 버퍼”의 크기가 커집니다.</span><span class="sxs-lookup"><span data-stu-id="ae8c6-143">A large number of out of order events within a large time window causes the size of the "reorder buffer" to be larger.</span></span> <span data-ttu-id="ae8c6-144">이 상황을 완화하려면 파티션 기준을 사용하여 파티션을 늘려서 쿼리의 규모를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8c6-144">To mitigate this situation, scale the query by increasing partitions by using PARTITION BY.</span></span> <span data-ttu-id="ae8c6-145">쿼리가 분할되면 여러 노드에 걸쳐 분산됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae8c6-145">After the query is partitioned, it is spread out over multiple nodes.</span></span> <span data-ttu-id="ae8c6-146">결과적으로, 각 노드로 들어오는 이벤트 수가 감소하여 다시 정렬 버퍼의 크기가 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="ae8c6-146">As a result, the number of events coming into each node is reduced, which in turn reduces the size of the reorder buffer.</span></span> 


## <a name="get-help"></a><span data-ttu-id="ae8c6-147">도움말 보기</span><span class="sxs-lookup"><span data-stu-id="ae8c6-147">Get help</span></span>
<span data-ttu-id="ae8c6-148">추가 지원이 필요한 경우 [Azure Stream Analytics 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ae8c6-148">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ae8c6-149">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ae8c6-149">Next steps</span></span>
* [<span data-ttu-id="ae8c6-150">Azure Stream Analytics 소개</span><span class="sxs-lookup"><span data-stu-id="ae8c6-150">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="ae8c6-151">Azure Stream Analytics 사용 시작</span><span class="sxs-lookup"><span data-stu-id="ae8c6-151">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="ae8c6-152">Azure 스트림 분석 작업 규모 지정</span><span class="sxs-lookup"><span data-stu-id="ae8c6-152">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="ae8c6-153">Azure Stream Analytics 쿼리 언어 참조</span><span class="sxs-lookup"><span data-stu-id="ae8c6-153">Azure Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="ae8c6-154">Azure Stream Analytics 관리 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="ae8c6-154">Azure Stream Analytics Management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

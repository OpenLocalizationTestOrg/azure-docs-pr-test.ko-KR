---
title: "Azure 스트림 분석: 사용자 작업 toouse 스트리밍 단위를 효율적으로 최적화 | Microsoft Docs"
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
ms.openlocfilehash: 5ad98b34d625190a879260f54c9eff0294e230cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-job-toouse-streaming-units-efficiently"></a><span data-ttu-id="837e0-104">사용자 작업 toouse 스트리밍 단위를 효율적으로 최적화</span><span class="sxs-lookup"><span data-stu-id="837e0-104">Optimize your job toouse Streaming Units efficiently</span></span>

<span data-ttu-id="837e0-105">Azure 스트림 분석 집계 hello 성능 "weight"의 스트리밍 단위 (SUs)에 작업을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="837e0-105">Azure Stream Analytics aggregates hello performance "weight" of running a job into Streaming Units (SUs).</span></span> <span data-ttu-id="837e0-106">SUs는 hello 컴퓨팅 리소스를 소비 된 tooexecute 작업을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="837e0-106">SUs represent hello computing resources that are consumed tooexecute a job.</span></span> <span data-ttu-id="837e0-107">SUs는 이벤트를 제공할 방법 toodescribe hello 상대 처리 용량은 CPU, 메모리의 복합된 측정에 기반 하 고 읽기 및 쓰기 속도로 합니다.</span><span class="sxs-lookup"><span data-stu-id="837e0-107">SUs provide a way toodescribe hello relative event processing capacity based on a blended measure of CPU, memory, and read and write rates.</span></span> <span data-ttu-id="837e0-108">이 용량 확인할 수 있습니다 쿼리 논리 hello 설정 하 고 수동으로 작업에 대 한 메모리를 할당 하 고 적절 하 게에서 hello CPU 필요한 core-count toorun 작업 대략적인 필요 tooknow 저장소 계층 성능 고려 사항에서를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="837e0-108">This capacity lets you focus on hello query logic and removes you from needing tooknow storage tier performance considerations, allocate memory for your job manually, and approximate hello CPU core-count needed toorun your job in a timely manner.</span></span>

## <a name="how-many-sus-are-required-for-a-job"></a><span data-ttu-id="837e0-109">작업에 필요한 SU 수는?</span><span class="sxs-lookup"><span data-stu-id="837e0-109">How many SUs are required for a job?</span></span>

<span data-ttu-id="837e0-110">특정 작업에 대 한 필수 sus hello 번호를 선택 하는 작업은 hello 입력과 hello 작업 내에서 정의 된 hello 쿼리에 대 한 hello 파티션 구성에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="837e0-110">Choosing hello number of required SUs for a particular job depends on hello partition configuration for hello inputs and hello query that's defined within hello job.</span></span> <span data-ttu-id="837e0-111">hello **배율** 블레이드 있습니다 tooset hello SUs 오른쪽 횟수입니다.</span><span class="sxs-lookup"><span data-stu-id="837e0-111">hello **Scale** blade allows you tooset hello right number of SUs.</span></span> <span data-ttu-id="837e0-112">되기는 것 보다 더 많은 SUs tooallocate이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="837e0-112">It is a best practice tooallocate more SUs than needed.</span></span> <span data-ttu-id="837e0-113">대기 시간 및 추가 메모리 할당의 hello 비용에는 처리량에 대 한 hello 스트림 분석 처리 엔진을 최적화 합니다.</span><span class="sxs-lookup"><span data-stu-id="837e0-113">hello Stream Analytics processing engine optimizes for latency and throughput at hello cost of allocating additional memory.</span></span>

<span data-ttu-id="837e0-114">일반적으로 hello 모범 사례는 사용 하지 않는 쿼리에 대 한 6 SUs와 toostart *PARTITION BY*합니다.</span><span class="sxs-lookup"><span data-stu-id="837e0-114">In general, hello best practice is toostart with 6 SUs for queries that don't use *PARTITION BY*.</span></span> <span data-ttu-id="837e0-115">그런 다음 대표 양의 데이터를 전달 하 고 hello SU % 사용률 메트릭을 검사 후 SUs hello 수가 수정 하는 시행 착오 메서드를 사용 하 여 hello 부분은 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="837e0-115">Then determine hello sweet spot by using a trial and error method in which you modify hello number of SUs after you pass representative amounts of data and examine hello SU %Utilization metric.</span></span>

<span data-ttu-id="837e0-116">Azure 스트림 분석 처리를 시작 하기 전에 "재주문 버퍼" hello 라는 창에서 이벤트를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="837e0-116">Azure Stream Analytics keeps events in a window called hello “reorder buffer” before it starts any processing.</span></span> <span data-ttu-id="837e0-117">시간까지 hello 재주문 창 내 정렬 되어 있는 이벤트 및 후속 작업이 일시적으로 정렬 하는 hello 이벤트에서 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="837e0-117">Events are sorted within hello reorder window by time, and subsequent operations are performed on hello temporally sorted events.</span></span> <span data-ttu-id="837e0-118">이벤트 시간으로 다시 정렬. 그러면 해당 hello 연산자에 모든 열로 표시 유형 조건 hello의 hello 이벤트 기간으로 규정 합니다.</span><span class="sxs-lookup"><span data-stu-id="837e0-118">Reordering events by time ensures that hello operator has visibility into all hello events in hello stipulated timeframe.</span></span> <span data-ttu-id="837e0-119">또한 hello 연산자를 hello 필수 처리를 수행 하 고 출력을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="837e0-119">It also lets hello operator perform hello requisite processing and produce an output.</span></span> <span data-ttu-id="837e0-120">이 메커니즘의 부작용은 처리 hello 순서 바꾸기 창의 hello 기간으로 지연 됩니다.</span><span class="sxs-lookup"><span data-stu-id="837e0-120">A side effect of this mechanism is that processing is delayed by hello duration of hello reorder window.</span></span> <span data-ttu-id="837e0-121">hello 작업 (SU 소비 영향을 줌)의 hello 메모리 공간에는 그 안에 포함 된 이벤트의이 순서 바꾸기 창과 hello 번호의 hello 크기의 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="837e0-121">hello memory footprint of hello job (which affects SU consumption) is a function of hello size of this reorder window and hello number of events contained within it.</span></span>

> [!NOTE]
> <span data-ttu-id="837e0-122">업그레이드 작업 중 hello 판독기 수 변경 되 면 일시적인 경고 tooaudit 로그 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="837e0-122">When hello number of readers changes during job upgrades, transient warnings are written tooaudit logs.</span></span> <span data-ttu-id="837e0-123">Stream Analytics 작업은 자동으로 이러한 일시적인 문제를 복구합니다.</span><span class="sxs-lookup"><span data-stu-id="837e0-123">Stream Analytics jobs automatically recover from these transient issues.</span></span>

## <a name="common-high-memory-causes-for-high-su-usage-for-running-jobs"></a><span data-ttu-id="837e0-124">높은 공용 메모리로 인해 실행 중인 작업에 높은 SU 사용량 유발</span><span class="sxs-lookup"><span data-stu-id="837e0-124">Common high-memory causes for high SU usage for running jobs</span></span>

### <a name="high-cardinality-for-group-by"></a><span data-ttu-id="837e0-125">그룹화 기준에 대한 높은 카디널리티</span><span class="sxs-lookup"><span data-stu-id="837e0-125">High cardinality for GROUP BY</span></span>

<span data-ttu-id="837e0-126">들어오는 이벤트의 hello 카디널리티 hello 작업에 대 한 메모리 사용량을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="837e0-126">hello cardinality of incoming events dictates memory usage for hello job.</span></span>

<span data-ttu-id="837e0-127">예를 들어, `SELECT count(*) from input group by clustered, tumblingwindow (minutes, 5)`, 연결 된 번호 hello **클러스터형** hello 쿼리의 hello 카디널리티는 합니다.</span><span class="sxs-lookup"><span data-stu-id="837e0-127">For example, in `SELECT count(*) from input group by clustered, tumblingwindow (minutes, 5)`, hello number associated with **clustered** is hello cardinality of hello query.</span></span>

<span data-ttu-id="837e0-128">카디널리티가 높은으로 인해 toomitigate 문제 사용 하 여 파티션을 증가 하 여 hello 쿼리 확장 **PARTITION BY**합니다.</span><span class="sxs-lookup"><span data-stu-id="837e0-128">toomitigate issues that are caused by high cardinality, scale out hello query by increasing partitions using **PARTITION BY**.</span></span>

```
Select count(*) from input
Partition By clusterid
GROUP BY clustered tumblingwindow (minutes, 5)
```

<span data-ttu-id="837e0-129">수가 hello *클러스터 된* hello의 카디널리티는 GROUP BY 여기 됩니다.</span><span class="sxs-lookup"><span data-stu-id="837e0-129">hello number of *clustered* is hello cardinality of GROUP BY here.</span></span>

<span data-ttu-id="837e0-130">Hello 쿼리를 분한 후 여러 노드를 분산 시키는 됩니다.</span><span class="sxs-lookup"><span data-stu-id="837e0-130">After hello query is partitioned, it is spread out over multiple nodes.</span></span> <span data-ttu-id="837e0-131">결과적으로, 각 노드에으로 들어오는 이벤트 hello 수가 줄어듭니다 차례로 hello hello 다시 정렬 버퍼 크기를 줄여주는.</span><span class="sxs-lookup"><span data-stu-id="837e0-131">As a result, hello number of events coming into each node is reduced, which in turn reduces hello size of hello reorder buffer.</span></span> <span data-ttu-id="837e0-132">또한 partitionid에 따라 이벤트 허브 파티션을 분할해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="837e0-132">You should also partition event hub partitions by partitionid.</span></span>

### <a name="high-unmatched-event-count-for-join"></a><span data-ttu-id="837e0-133">JOIN에 대해 일치하지 않는 이벤트 개수가 많음</span><span class="sxs-lookup"><span data-stu-id="837e0-133">High unmatched event count for JOIN</span></span>

<span data-ttu-id="837e0-134">조인에 일치 하지 않는 이벤트의 hello 수가 hello 메모리 사용률이 hello 쿼리의 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="837e0-134">hello number of unmatched events in a JOIN affects hello memory utilization of hello query.</span></span> <span data-ttu-id="837e0-135">예를 들어 toofind hello 광고 노출 수 번의 클릭을 생성 하는 검색 하는 쿼리를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="837e0-135">For example, take a query that is looking toofind hello number of ad impressions that generates clicks:</span></span>

```
SELECT id from clicks INNER JOIN,
impressions on impressions.id = clicks.id AND DATEDIFF(hour, impressions, clicks) between 0 AND 10
```

<span data-ttu-id="837e0-136">이 시나리오에서 많은 광고가 표시되고 몇 번의 클릭이 생성될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="837e0-136">In this scenario, it is possible that many ads are shown and few clicks are generated.</span></span> <span data-ttu-id="837e0-137">이러한 결과 hello 시간 창 내의 모든 hello 이벤트 hello 작업 tookeep 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="837e0-137">Such a result would require hello job tookeep all hello events within hello time window.</span></span> <span data-ttu-id="837e0-138">사용 되는 메모리 양은 hello 비례 toohello 창 크기와 이벤트 속도입니다.</span><span class="sxs-lookup"><span data-stu-id="837e0-138">hello amount of memory consumed is proportional toohello window size and event rate.</span></span> 

<span data-ttu-id="837e0-139">toomitigate PARTITION BY를 사용 하 여 이러한 상황을 늘려 hello 쿼리 확장 분할 합니다.</span><span class="sxs-lookup"><span data-stu-id="837e0-139">toomitigate this situation, scale out hello query by increasing partitions by using PARTITION BY.</span></span> 

<span data-ttu-id="837e0-140">Hello 쿼리를 분한 후 여러 처리 노드를 분산 시키는 됩니다.</span><span class="sxs-lookup"><span data-stu-id="837e0-140">After hello query is partitioned, it is spread out over multiple processing nodes.</span></span> <span data-ttu-id="837e0-141">결과적으로, 각 노드에으로 들어오는 이벤트 hello 수가 줄어듭니다 차례로 hello hello 다시 정렬 버퍼 크기를 줄여주는.</span><span class="sxs-lookup"><span data-stu-id="837e0-141">As a result, hello number of events coming into each node is reduced, which in turn reduces hello size of hello reorder buffer.</span></span>

### <a name="large-number-of-out-of-order-events"></a><span data-ttu-id="837e0-142">순서가 잘못된 이벤트 수가 많음</span><span class="sxs-lookup"><span data-stu-id="837e0-142">Large number of out of order events</span></span> 

<span data-ttu-id="837e0-143">큰 시간 창 내의 순서가 틀린 이벤트 수가 많은 hello hello "버퍼 순서" toobe 더 큰 크기를 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="837e0-143">A large number of out of order events within a large time window causes hello size of hello "reorder buffer" toobe larger.</span></span> <span data-ttu-id="837e0-144">PARTITION BY를 사용 하 여 toomitigate 배율 hello 쿼리를 늘려 이러한 상황을 분할 합니다.</span><span class="sxs-lookup"><span data-stu-id="837e0-144">toomitigate this situation, scale hello query by increasing partitions by using PARTITION BY.</span></span> <span data-ttu-id="837e0-145">Hello 쿼리를 분한 후 여러 노드를 분산 시키는 됩니다.</span><span class="sxs-lookup"><span data-stu-id="837e0-145">After hello query is partitioned, it is spread out over multiple nodes.</span></span> <span data-ttu-id="837e0-146">결과적으로, 각 노드에으로 들어오는 이벤트 hello 수가 줄어듭니다 차례로 hello hello 다시 정렬 버퍼 크기를 줄여주는.</span><span class="sxs-lookup"><span data-stu-id="837e0-146">As a result, hello number of events coming into each node is reduced, which in turn reduces hello size of hello reorder buffer.</span></span> 


## <a name="get-help"></a><span data-ttu-id="837e0-147">도움말 보기</span><span class="sxs-lookup"><span data-stu-id="837e0-147">Get help</span></span>
<span data-ttu-id="837e0-148">추가 지원이 필요한 경우 [Azure Stream Analytics 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="837e0-148">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="837e0-149">다음 단계</span><span class="sxs-lookup"><span data-stu-id="837e0-149">Next steps</span></span>
* [<span data-ttu-id="837e0-150">스트림 분석 소개 tooAzure</span><span class="sxs-lookup"><span data-stu-id="837e0-150">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="837e0-151">Azure Stream Analytics 사용 시작</span><span class="sxs-lookup"><span data-stu-id="837e0-151">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="837e0-152">Azure 스트림 분석 작업 규모 지정</span><span class="sxs-lookup"><span data-stu-id="837e0-152">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="837e0-153">Azure Stream Analytics 쿼리 언어 참조</span><span class="sxs-lookup"><span data-stu-id="837e0-153">Azure Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="837e0-154">Azure Stream Analytics 관리 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="837e0-154">Azure Stream Analytics Management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

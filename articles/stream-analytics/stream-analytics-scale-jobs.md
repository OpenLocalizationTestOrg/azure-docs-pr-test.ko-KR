---
title: "스트림 분석 작업 tooincrease 처리량 aaaScale | Microsoft Docs"
description: "입력된 파티션 구성 hello 쿼리 정의 조정 하 고 설정 하 여 스트림 분석 작업 tooscale 스트리밍 단위를 작업 하는 방법에 대해 알아봅니다."
keywords: "데이터 스트리밍, 스트리밍 데이터 처리, 분석 조정"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 7e857ddb-71dd-4537-b7ab-4524335d7b35
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/22/2017
ms.author: jeffstok
ms.openlocfilehash: 4ba8f6b2f8bfebd52cfa07696b501b42cda21f75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-azure-stream-analytics-jobs-tooincrease-stream-data-processing-throughput"></a><span data-ttu-id="c7937-104">배율 Azure 스트림 분석 작업 tooincrease 스트림 데이터 처리 처리량</span><span class="sxs-lookup"><span data-stu-id="c7937-104">Scale Azure Stream Analytics jobs tooincrease stream data processing throughput</span></span>
<span data-ttu-id="c7937-105">이 문서 tootune 스트림 분석에서 스트리밍 분석 작업에 대 한 tooincrease 처리량을 쿼리 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-105">This article shows you how tootune a Stream Analytics query tooincrease throughput for Streaming Analytics jobs.</span></span> <span data-ttu-id="c7937-106">스트림 분석 tooscale 입력된 파티션을 구성 하 여 작업 하는 방법을 알아보려면, 튜닝 hello 분석 쿼리를 정의 및 계산 하 고 설정 작업 *스트리밍 단위* (SUs).</span><span class="sxs-lookup"><span data-stu-id="c7937-106">You learn how tooscale Stream Analytics jobs by configuring input partitions, tuning hello analytics query definition, and calculating and setting job *streaming units* (SUs).</span></span> 

## <a name="what-are-hello-parts-of-a-stream-analytics-job"></a><span data-ttu-id="c7937-107">스트림 분석 작업의 hello 부분 이란?</span><span class="sxs-lookup"><span data-stu-id="c7937-107">What are hello parts of a Stream Analytics job?</span></span>
<span data-ttu-id="c7937-108">Stream Analytics 작업 정의에는 입력, 쿼리 및 출력이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-108">A Stream Analytics job definition includes inputs, a query, and output.</span></span> <span data-ttu-id="c7937-109">입력은 위치 hello 작업에서 데이터 스트림을 hello를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-109">Inputs are where hello job reads hello data stream from.</span></span> <span data-ttu-id="c7937-110">hello 쿼리 사용 되는 tootransform hello 데이터 입력된 스트림의 이며 hello 출력 hello 작업이 hello 작업 결과 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-110">hello query is used tootransform hello data input stream, and hello output is where hello job sends hello job results to.</span></span>  

<span data-ttu-id="c7937-111">작업에는 데이터 스트림에 대해 하나 이상의 입력 소스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-111">A job requires at least one input source for data streaming.</span></span> <span data-ttu-id="c7937-112">hello 데이터 스트림 입력된 소스가 저장할 수 있습니다 또는 Azure blob 저장소에 Azure 이벤트 허브에서.</span><span class="sxs-lookup"><span data-stu-id="c7937-112">hello data stream input source can be stored in an Azure event hub or in Azure blob storage.</span></span> <span data-ttu-id="c7937-113">자세한 내용은 참조 [스트림 분석 소개 tooAzure](stream-analytics-introduction.md) 및 [Azure 스트림 분석을 사용 하 여 시작](stream-analytics-real-time-fraud-detection.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-113">For more information, see [Introduction tooAzure Stream Analytics](stream-analytics-introduction.md) and [Get started using Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md).</span></span>

## <a name="partitions-in-event-hubs-and-azure-storage"></a><span data-ttu-id="c7937-114">이벤트 허브와 Azure Storage의 파티션</span><span class="sxs-lookup"><span data-stu-id="c7937-114">Partitions in event hubs and Azure storage</span></span>
<span data-ttu-id="c7937-115">스트림 분석 작업 크기 조정에서는 hello 입력 또는 출력에 파티션 활용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-115">Scaling a Stream Analytics job takes advantage of partitions in hello input or output.</span></span> <span data-ttu-id="c7937-116">분할을 통해 데이터를 파티션 키에 따라 하위 집합으로 분할할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-116">Partitioning lets you divide data into subsets based on a partition key.</span></span> <span data-ttu-id="c7937-117">Hello 데이터 (예: 스트리밍 분석 작업의 경우)를 사용 하는 프로세스는 소비 하며 처리량을 향상 시키는 동시에 서로 다른 파티션을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-117">A process that consumes hello data (such as a Streaming Analytics job) can consume and write different partitions in parallel, which increases throughput.</span></span> <span data-ttu-id="c7937-118">Streaming Analytics로 작업할 때 이벤트 허브 및 Blob Storage에서 분할을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-118">When you work with Streaming Analytics, you can take advantage of partitioning in event hubs and in Blob storage.</span></span> 

<span data-ttu-id="c7937-119">파티션에 대 한 자세한 내용은 다음 문서는 hello 참조:</span><span class="sxs-lookup"><span data-stu-id="c7937-119">For more information about partitions, see hello following articles:</span></span>

* [<span data-ttu-id="c7937-120">Event Hubs 기능 개요</span><span class="sxs-lookup"><span data-stu-id="c7937-120">Event Hubs features overview</span></span>](../event-hubs/event-hubs-features.md#partitions)
* [<span data-ttu-id="c7937-121">데이터 분할</span><span class="sxs-lookup"><span data-stu-id="c7937-121">Data partitioning</span></span>](https://docs.microsoft.com/azure/architecture/best-practices/data-partitioning#partitioning-azure-blob-storage)


## <a name="streaming-units-sus"></a><span data-ttu-id="c7937-122">SU(스트리밍 단위)</span><span class="sxs-lookup"><span data-stu-id="c7937-122">Streaming units (SUs)</span></span>
<span data-ttu-id="c7937-123">스트리밍 단위 (SUs) 나타내는 hello 리소스 및에서 필요한 컴퓨팅 tooexecute Azure 스트림 분석 작업 순서.</span><span class="sxs-lookup"><span data-stu-id="c7937-123">Streaming units (SUs) represent hello resources and computing power that are required in order tooexecute an Azure Stream Analytics job.</span></span> <span data-ttu-id="c7937-124">SUs는 이벤트를 제공할 방법 toodescribe hello 상대 처리 용량은 CPU, 메모리의 복합된 측정에 기반 하 고 읽기 및 쓰기 속도로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-124">SUs provide a way toodescribe hello relative event processing capacity based on a blended measure of CPU, memory, and read and write rates.</span></span> <span data-ttu-id="c7937-125">SU를 각 해당 tooroughly 1 m B/초의 처리량입니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-125">Each SU corresponds tooroughly 1 MB/second of throughput.</span></span> 

<span data-ttu-id="c7937-126">개수 SUs 선택는 hello 작업에 대해 정의 된 hello 쿼리 및 hello 입력에 대 한 hello 파티션 구성에 따라 결정 하는 특정 작업에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-126">Choosing how many SUs are required for a particular job depends on hello partition configuration for hello inputs and on hello query defined for hello job.</span></span> <span data-ttu-id="c7937-127">작업에 대 한 SUs tooyour 할당량을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-127">You can select up tooyour quota in SUs for a job.</span></span> <span data-ttu-id="c7937-128">기본적으로 각 Azure 구독에는 특정 지역에서 모든 hello 분석 작업에 대 한 too50 SUs의 할당량이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-128">By default, each Azure subscription has a quota of up too50 SUs for all hello analytics jobs in a specific region.</span></span> <span data-ttu-id="c7937-129">연락처가이 할당량을 초과 하면 구독에 대 한 SUs tooincrease [Microsoft 지원](http://support.microsoft.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-129">tooincrease SUs for your subscriptions beyond this quota, contact [Microsoft Support](http://support.microsoft.com).</span></span> <span data-ttu-id="c7937-130">작업당 SU에 대한 유효한 값은 1, 3, 6이며 6 단위로 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-130">Valid values for SUs per job are 1, 3, 6, and up in increments of 6.</span></span>

## <a name="embarrassingly-parallel-jobs"></a><span data-ttu-id="c7937-131">병렬 처리가 적합한 작업</span><span class="sxs-lookup"><span data-stu-id="c7937-131">Embarrassingly parallel jobs</span></span>
<span data-ttu-id="c7937-132">*병렬* 작업은 Azure 스트림 분석에 있는 hello 가장 확장성이 높은 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-132">An *embarrassingly parallel* job is hello most scalable scenario we have in Azure Stream Analytics.</span></span> <span data-ttu-id="c7937-133">Hello 출력의 hello 쿼리 tooone 파티션의 hello 입력된 tooone 인스턴스 중 한 파티션에 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-133">It connects one partition of hello input tooone instance of hello query tooone partition of hello output.</span></span> <span data-ttu-id="c7937-134">이 병렬 처리 요구 사항을 준수 하는 hello에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-134">This parallelism has hello following requirements:</span></span>

1. <span data-ttu-id="c7937-135">같은 키 처리 되 고 hello에 종속 되는 쿼리 논리 인스턴스를 쿼리할 동일 hello에서, hello 이벤트 toohello 이동 하 고 있는지 확인 해야 입력의 같은 파티션을 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-135">If your query logic depends on hello same key being processed by hello same query instance, you must make sure that hello events go toohello same partition of your input.</span></span> <span data-ttu-id="c7937-136">이벤트 허브에 대 한이 hello 이벤트 데이터가지고 있어야 함을 의미 hello **PartitionKey** 값이 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-136">For event hubs, this means that hello event data must have hello **PartitionKey** value set.</span></span> <span data-ttu-id="c7937-137">또는 분할된 보낸 사람을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-137">Alternatively, you can use partitioned senders.</span></span> <span data-ttu-id="c7937-138">Blob 저장소에 대 한 즉 hello 이벤트는 전송 toohello 같은 파티션 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-138">For blob storage, this means that hello events are sent toohello same partition folder.</span></span> <span data-ttu-id="c7937-139">쿼리 논리 같은 키 처리 toobe hello 필요 하지 않은 경우 인스턴스를 쿼리할 동일 hello 하 여,이 요구 사항을 무시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-139">If your query logic does not require hello same key toobe processed by hello same query instance, you can ignore this requirement.</span></span> <span data-ttu-id="c7937-140">이 논리에 대한 예로 간단한 선택/프로젝트/필터 쿼리를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c7937-140">An example of this logic would be a simple select-project-filter query.</span></span>  

2. <span data-ttu-id="c7937-141">Hello 데이터 레이아웃을 hello 입력 쪽 되 면 쿼리 분할 되어 있는지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-141">Once hello data is laid out on hello input side, you must make sure that your query is partitioned.</span></span> <span data-ttu-id="c7937-142">이 옵션을 toouse **Partition By** 모든 hello 단계에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-142">This requires you toouse **Partition By** in all hello steps.</span></span> <span data-ttu-id="c7937-143">여러 단계 수 있지만 hello 분할 해야 모두 동일한 키입니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-143">Multiple steps are allowed, but they all must be partitioned by hello same key.</span></span> <span data-ttu-id="c7937-144">분할 키 hello를 너무 설정 되어 있어야 현재**PartitionId** hello 작업 toobe 병렬 완벽 하 게 하려면에서.</span><span class="sxs-lookup"><span data-stu-id="c7937-144">Currently, hello partitioning key must be set too**PartitionId** in order for hello job toobe fully parallel.</span></span>  

3. <span data-ttu-id="c7937-145">현재는 이벤트 허브 및 Blob Storage만 분할된 출력을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-145">Currently only event hubs and blob storage support partitioned output.</span></span> <span data-ttu-id="c7937-146">이벤트 허브 출력에 대 한 파티션 키 toobe hello 구성 해야 **PartitionId**합니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-146">For event hub output, you must configure hello partition key toobe **PartitionId**.</span></span> <span data-ttu-id="c7937-147">Blob 저장소 출력에 대 한 않아도 toodo 아무 것도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-147">For blob storage output, you don't have toodo anything.</span></span>  

4. <span data-ttu-id="c7937-148">hello 입력된 파티션 수와 hello 출력 파티션 수가 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-148">hello number of input partitions must equal hello number of output partitions.</span></span> <span data-ttu-id="c7937-149">Blob Storage 출력은 현재 파티션을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-149">Blob storage output doesn't currently support partitions.</span></span> <span data-ttu-id="c7937-150">하지만 괜찮습니다, 파티션 구성표 hello 업스트림 쿼리의 hello 상속 되므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-150">But that's okay, because it inherits hello partitioning scheme of hello upstream query.</span></span> <span data-ttu-id="c7937-151">다음은 완전한 병렬 작업을 허용하는 파티션 값의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-151">Here are examples of partition values that allow a fully parallel job:</span></span>  

   * <span data-ttu-id="c7937-152">8개의 이벤트 허브 입력 파티션 및 8개의 이벤트 허브 출력 파티션</span><span class="sxs-lookup"><span data-stu-id="c7937-152">8 event hub input partitions and 8 event hub output partitions</span></span>
   * <span data-ttu-id="c7937-153">8개의 이벤트 허브 입력 파티션 및 Blob Storage 출력</span><span class="sxs-lookup"><span data-stu-id="c7937-153">8 event hub input partitions and blob storage output</span></span>  
   * <span data-ttu-id="c7937-154">8개의 Blob Storage 입력 파티션 및 Blob Storage 출력</span><span class="sxs-lookup"><span data-stu-id="c7937-154">8 blob storage input partitions and blob storage output</span></span>  
   * <span data-ttu-id="c7937-155">8개의 Blob Storage 입력 파티션 및 8개의 이벤트 허브 출력 파티션</span><span class="sxs-lookup"><span data-stu-id="c7937-155">8 blob storage input partitions and 8 event hub output partitions</span></span>  

<span data-ttu-id="c7937-156">hello 다음 섹션에서는 설명 병렬는 몇 가지 예제 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-156">hello following sections discuss some example scenarios that are embarrassingly parallel.</span></span>

### <a name="simple-query"></a><span data-ttu-id="c7937-157">단순 쿼리</span><span class="sxs-lookup"><span data-stu-id="c7937-157">Simple query</span></span>

* <span data-ttu-id="c7937-158">입력: 8개의 파티션이 있는 이벤트 허브</span><span class="sxs-lookup"><span data-stu-id="c7937-158">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="c7937-159">출력: 8개의 파티션이 있는 이벤트 허브</span><span class="sxs-lookup"><span data-stu-id="c7937-159">Output: Event hub with 8 partitions</span></span>

<span data-ttu-id="c7937-160">쿼리:</span><span class="sxs-lookup"><span data-stu-id="c7937-160">Query:</span></span>

    SELECT TollBoothId
    FROM Input1 Partition By PartitionId
    WHERE TollBoothId > 100

<span data-ttu-id="c7937-161">이 쿼리는 간단한 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-161">This query is a simple filter.</span></span> <span data-ttu-id="c7937-162">따라서 tooworry toohello 이벤트 허브 전송 되는 hello 입력을 분할 하는 방법에 대 한 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-162">Therefore, we don't need tooworry about partitioning hello input that is being sent toohello event hub.</span></span> <span data-ttu-id="c7937-163">해당 hello 쿼리에 포함 되어 **파티션에 의해 PartitionId**앞에서 #2 요건을 충족 하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-163">Notice that hello query includes **Partition By PartitionId**, so it fulfills requirement #2 from earlier.</span></span> <span data-ttu-id="c7937-164">Hello 출력에 대 한 필요 tooconfigure hello 이벤트 허브 출력 hello 작업 toohave hello 파티션 키 집합에 너무**PartitionId**합니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-164">For hello output, we need tooconfigure hello event hub output in hello job toohave hello parition key set too**PartitionId**.</span></span> <span data-ttu-id="c7937-165">하나 이상의 마지막 검사 toomake hello 입력된 파티션 수가 출력 파티션의 수를 같은 toohello 인지입니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-165">One last check is toomake sure that hello number of input partitions is equal toohello number of output partitions.</span></span>

### <a name="query-with-a-grouping-key"></a><span data-ttu-id="c7937-166">그룹화 키가 있는 쿼리</span><span class="sxs-lookup"><span data-stu-id="c7937-166">Query with a grouping key</span></span>

* <span data-ttu-id="c7937-167">입력: 8개의 파티션이 있는 이벤트 허브</span><span class="sxs-lookup"><span data-stu-id="c7937-167">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="c7937-168">출력: Blob Storage</span><span class="sxs-lookup"><span data-stu-id="c7937-168">Output: Blob storage</span></span>

<span data-ttu-id="c7937-169">쿼리:</span><span class="sxs-lookup"><span data-stu-id="c7937-169">Query:</span></span>

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="c7937-170">이 쿼리에 그룹화 키가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-170">This query has a grouping key.</span></span> <span data-ttu-id="c7937-171">따라서 hello 같은 핵심 요구 toobe 같은 이벤트 보내야 한다고 toohello 이벤트 허브는 분할 방식에서 즉 인스턴스를 쿼리 하는 hello에서 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-171">Therefore, hello same key needs toobe processed by hello same query instance, which means that events must be sent toohello event hub in a partitioned manner.</span></span> <span data-ttu-id="c7937-172">하지만 어떤 키를 사용해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="c7937-172">But which key should be used?</span></span> <span data-ttu-id="c7937-173">**PartitionId**는 작업 논리 개념입니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-173">**PartitionId** is a job-logic concept.</span></span> <span data-ttu-id="c7937-174">실제로 신경을 hello 키가 **TollBoothId**, 따라서 hello **PartitionKey** hello 이벤트 데이터의 값은 **TollBoothId**합니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-174">hello key we actually care about is **TollBoothId**, so hello **PartitionKey** value of hello event data should be **TollBoothId**.</span></span> <span data-ttu-id="c7937-175">설정 하 여 hello 쿼리에서 수행할이 **Partition By** 너무**PartitionId**합니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-175">We do this in hello query by setting **Partition By** too**PartitionId**.</span></span> <span data-ttu-id="c7937-176">Hello 출력 blob 저장소 이므로 tooworry #4 요구 사항에 따라 파티션 키 값을 구성 하는 방법에 대 한 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-176">Since hello output is blob storage, we don't need tooworry about configuring a partition key value, as per requirement #4.</span></span>

### <a name="multi-step-query-with-a-grouping-key"></a><span data-ttu-id="c7937-177">그룹화 키가 있는 다중 단계 쿼리</span><span class="sxs-lookup"><span data-stu-id="c7937-177">Multi-step query with a grouping key</span></span>
* <span data-ttu-id="c7937-178">입력: 8개의 파티션이 있는 이벤트 허브</span><span class="sxs-lookup"><span data-stu-id="c7937-178">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="c7937-179">출력: 8개의 파티션이 있는 이벤트 허브 인스턴스</span><span class="sxs-lookup"><span data-stu-id="c7937-179">Output: Event hub instance with 8 partitions</span></span>

<span data-ttu-id="c7937-180">쿼리:</span><span class="sxs-lookup"><span data-stu-id="c7937-180">Query:</span></span>

    WITH Step1 AS (
    SELECT COUNT(*) AS Count, TollBoothId, PartitionId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="c7937-181">이 쿼리에 그룹화 키, 같은 핵심 요구 toobe hello에 의해 처리 되므로 hello 동일한 쿼리 인스턴스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-181">This query has a grouping key, so hello same key needs toobe processed by hello same query instance.</span></span> <span data-ttu-id="c7937-182">사용 하는 hello hello 이전 예제와 같이 동일한 전략입니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-182">We can use hello same strategy as in hello previous example.</span></span> <span data-ttu-id="c7937-183">이 경우 hello 쿼리는 여러 단계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-183">In this case, hello query has multiple steps.</span></span> <span data-ttu-id="c7937-184">각 단계에 **Partition By PartitionId**가 있나요?</span><span class="sxs-lookup"><span data-stu-id="c7937-184">Does each step have **Partition By PartitionId**?</span></span> <span data-ttu-id="c7937-185">예, hello 쿼리 #3 요건을 충족 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-185">Yes, so hello query fulfills requirement #3.</span></span> <span data-ttu-id="c7937-186">Hello 출력에 대 한 필요 tooset hello 파티션 키 너무**PartitionId**앞서 설명한 것 처럼, 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-186">For hello output, we need tooset hello partition key too**PartitionId**, as discussed earlier.</span></span> <span data-ttu-id="c7937-187">Hello 있다는 것도 확인할 수 있습니다 hello 입력으로 동일한 수의 파티션 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-187">We can also see that it has hello same number of partitions as hello input.</span></span>

## <a name="example-scenarios-that-are-not-embarrassingly-parallel"></a><span data-ttu-id="c7937-188">병렬 처리가 적합하지 *않은* 예제 시나리오</span><span class="sxs-lookup"><span data-stu-id="c7937-188">Example scenarios that are *not* embarrassingly parallel</span></span>

<span data-ttu-id="c7937-189">Hello 이전 섹션에서 몇 가지 병렬 시나리오 했죠.</span><span class="sxs-lookup"><span data-stu-id="c7937-189">In hello previous section, we showed some embarrassingly parallel scenarios.</span></span> <span data-ttu-id="c7937-190">이 섹션에서는 모든 hello 요구 사항 toobe 병렬 일치 하지 않는 시나리오에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-190">In this section, we discuss scenarios that don't meet all hello requirements toobe embarrassingly parallel.</span></span> 

### <a name="mismatched-partition-count"></a><span data-ttu-id="c7937-191">일치하지 않는 파티션 수</span><span class="sxs-lookup"><span data-stu-id="c7937-191">Mismatched partition count</span></span>
* <span data-ttu-id="c7937-192">입력: 8개의 파티션이 있는 이벤트 허브</span><span class="sxs-lookup"><span data-stu-id="c7937-192">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="c7937-193">출력: 32개의 파티션이 있는 이벤트 허브</span><span class="sxs-lookup"><span data-stu-id="c7937-193">Output: Event hub with 32 partitions</span></span>

<span data-ttu-id="c7937-194">중요 하지 않습니다는 경우 어떤 hello 쿼리가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-194">In this case, it doesn't matter what hello query is.</span></span> <span data-ttu-id="c7937-195">Hello 입력된 파티션 수에는 hello 출력 파티션 수와 일치 하지 않으면, hello 토폴로지 병렬 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-195">If hello input partition count doesn't match hello output partition count, hello topology isn't embarrassingly parallel.</span></span>

### <a name="not-using-event-hubs-or-blob-storage-as-output"></a><span data-ttu-id="c7937-196">이벤트 허브 또는 Blob Storage를 출력으로 사용하지 않음</span><span class="sxs-lookup"><span data-stu-id="c7937-196">Not using event hubs or blob storage as output</span></span>
* <span data-ttu-id="c7937-197">입력: 8개의 파티션이 있는 이벤트 허브</span><span class="sxs-lookup"><span data-stu-id="c7937-197">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="c7937-198">출력: PowerBI</span><span class="sxs-lookup"><span data-stu-id="c7937-198">Output: PowerBI</span></span>

<span data-ttu-id="c7937-199">PowerBI 출력은 현재 분할을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-199">PowerBI output doesn't currently support partitioning.</span></span> <span data-ttu-id="c7937-200">따라서 이 시나리오는 병렬 처리가 적합하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-200">Therefore, this scenario is not embarrassingly parallel.</span></span>

### <a name="multi-step-query-with-different-partition-by-values"></a><span data-ttu-id="c7937-201">서로 다른 Partition By 값이 있는 다중 단계 쿼리</span><span class="sxs-lookup"><span data-stu-id="c7937-201">Multi-step query with different Partition By values</span></span>
* <span data-ttu-id="c7937-202">입력: 8개의 파티션이 있는 이벤트 허브</span><span class="sxs-lookup"><span data-stu-id="c7937-202">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="c7937-203">출력: 8개의 파티션이 있는 이벤트 허브</span><span class="sxs-lookup"><span data-stu-id="c7937-203">Output: Event hub with 8 partitions</span></span>

<span data-ttu-id="c7937-204">쿼리:</span><span class="sxs-lookup"><span data-stu-id="c7937-204">Query:</span></span>

    WITH Step1 AS (
    SELECT COUNT(*) AS Count, TollBoothId, PartitionId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1 Partition By TollBoothId
    GROUP BY TumblingWindow(minute, 3), TollBoothId

<span data-ttu-id="c7937-205">Hello 두 번째 단계에 사용 하 여 볼 수 있듯이 **TollBoothId** hello 분할 키로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-205">As you can see, hello second step uses **TollBoothId** as hello partitioning key.</span></span> <span data-ttu-id="c7937-206">Hello 첫 번째 단계로, 동일를이 단계는 hello 하지 있으며 따라서 있어야 우리 toodo 한 순서 섞기 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-206">This step is not hello same as hello first step, and it therefore requires us toodo a shuffle.</span></span> 

<span data-ttu-id="c7937-207">hello 앞의 예제에서는 일부 스트림 분석 작업을 보여 줍니다 병렬 토폴로지 너무 준수 (또는 안 함).</span><span class="sxs-lookup"><span data-stu-id="c7937-207">hello preceding examples show some Stream Analytics jobs that conform too(or don't) an embarrassingly parallel topology.</span></span> <span data-ttu-id="c7937-208">준수 수행 하는 경우 hello 잠재력을 최대한 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-208">If they do conform, they have hello potential for maximum scale.</span></span> <span data-ttu-id="c7937-209">이러한 프로필 중 하나에 적합하지 않는 작업의 경우 향후 업데이트에서 크기 조정 지침이 제공될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-209">For jobs that don't fit one of these profiles, scaling guidance will be available in future updates.</span></span> <span data-ttu-id="c7937-210">지금은 hello 다음 섹션에에서 hello 일반적인 지침을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-210">For now, use hello general guidance in hello following sections.</span></span>

## <a name="calculate-hello-maximum-streaming-units-of-a-job"></a><span data-ttu-id="c7937-211">작업의 최대 스트리밍 단위를 hello를 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-211">Calculate hello maximum streaming units of a job</span></span>
<span data-ttu-id="c7937-212">hello 총 스트림 분석 작업에서 사용할 수 있는 스트리밍 단위 수가 hello 작업과 hello 각 단계에 대 한 파티션 수에 대 한 정의 된 hello 쿼리 단계 hello 수에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-212">hello total number of streaming units that can be used by a Stream Analytics job depends on hello number of steps in hello query defined for hello job and hello number of partitions for each step.</span></span>

### <a name="steps-in-a-query"></a><span data-ttu-id="c7937-213">쿼리의 단계</span><span class="sxs-lookup"><span data-stu-id="c7937-213">Steps in a query</span></span>
<span data-ttu-id="c7937-214">하나의 쿼리에는 하나 이상의 단계가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-214">A query can have one or many steps.</span></span> <span data-ttu-id="c7937-215">각 단계는 hello에 정의 된 하위 쿼리 **WITH** 키워드입니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-215">Each step is a subquery defined by hello **WITH** keyword.</span></span> <span data-ttu-id="c7937-216">hello 밖에 있는 hello 쿼리 **WITH** 키워드 (하나의 쿼리에만 해당) hello 같은 단계로 계산 **선택** 다음 쿼리에서 hello에 문의:</span><span class="sxs-lookup"><span data-stu-id="c7937-216">hello query that is outside hello **WITH** keyword (one query only) is also counted as a step, such as hello **SELECT** statement in hello following query:</span></span>

    WITH Step1 AS (
        SELECT COUNT(*) AS Count, TollBoothId
        FROM Input1 Partition By PartitionId
        GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1
    GROUP BY TumblingWindow(minute,3), TollBoothId

<span data-ttu-id="c7937-217">이 쿼리에는 2개의 단계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-217">This query has two steps.</span></span>

> [!NOTE]
> <span data-ttu-id="c7937-218">이 쿼리는 hello 문서 뒷부분에 보다 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-218">This query is discussed in more detail later in hello article.</span></span>
>  

### <a name="partition-a-step"></a><span data-ttu-id="c7937-219">단계 분할</span><span class="sxs-lookup"><span data-stu-id="c7937-219">Partition a step</span></span>
<span data-ttu-id="c7937-220">분할 된 단계가 hello를 조건 다음 사항이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-220">Partitioning a step requires hello following conditions:</span></span>

* <span data-ttu-id="c7937-221">hello 입력된 소스를 분할 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-221">hello input source must be partitioned.</span></span> 
* <span data-ttu-id="c7937-222">hello **선택** hello 쿼리 문은 분할 된 입력된 소스에서 읽어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-222">hello **SELECT** statement of hello query must read from a partitioned input source.</span></span>
* <span data-ttu-id="c7937-223">hello 단계 내에서 hello 쿼리 hello 있어야 **Partition By** 키워드입니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-223">hello query within hello step must have hello **Partition By** keyword.</span></span>

<span data-ttu-id="c7937-224">쿼리를 분할 hello 입력된 이벤트는 별도 파티션을 처리 하 고에서 집계 된 그룹 및 출력 이벤트는 각각 hello 그룹에 대해 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-224">When a query is partitioned, hello input events are processed and aggregated in separate partition groups, and outputs events are generated for each of hello groups.</span></span> <span data-ttu-id="c7937-225">집계를 결합된 하려는 경우 두 번째 단계 분할 되지 않은 tooaggregate를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-225">If you want a combined aggregate, you must create a second non-partitioned step tooaggregate.</span></span>

### <a name="calculate-hello-max-streaming-units-for-a-job"></a><span data-ttu-id="c7937-226">Hello 최대 스트리밍 단위는 작업에 대 한 계산</span><span class="sxs-lookup"><span data-stu-id="c7937-226">Calculate hello max streaming units for a job</span></span>
<span data-ttu-id="c7937-227">분할 되지 않은 모든 단계는 함께 toosix 스트리밍 단위 (SUs) 스트림 분석 작업에 대 한를 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-227">All non-partitioned steps together can scale up toosix streaming units (SUs) for a Stream Analytics job.</span></span> <span data-ttu-id="c7937-228">tooadd SUs는 한 단계를 분할 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-228">tooadd SUs, a step must be partitioned.</span></span> <span data-ttu-id="c7937-229">각 파티션에는 6개의 SU가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-229">Each partition can have six SUs.</span></span>

<table border="1">
<tr><th><span data-ttu-id="c7937-230">쿼리</span><span class="sxs-lookup"><span data-stu-id="c7937-230">Query</span></span></th><th><span data-ttu-id="c7937-231">Hello 작업에 대 한 최대 SUs</span><span class="sxs-lookup"><span data-stu-id="c7937-231">Max SUs for hello job</span></span></th></td>

<tr><td>
<ul>
<li><span data-ttu-id="c7937-232">hello 쿼리 한 단계를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-232">hello query contains one step.</span></span></li>
<li><span data-ttu-id="c7937-233">hello 단계 분할할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-233">hello step is not partitioned.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="c7937-234">6</span><span class="sxs-lookup"><span data-stu-id="c7937-234">6</span></span></td></tr>

<tr><td>
<ul>
<li><span data-ttu-id="c7937-235">hello 입력된 데이터 스트림은 3으로 분할 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-235">hello input data stream is partitioned by 3.</span></span></li>
<li><span data-ttu-id="c7937-236">hello 쿼리 한 단계를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-236">hello query contains one step.</span></span></li>
<li><span data-ttu-id="c7937-237">hello 단계 분할 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-237">hello step is partitioned.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="c7937-238">18</span><span class="sxs-lookup"><span data-stu-id="c7937-238">18</span></span></td></tr>

<tr><td>
<ul>
<li><span data-ttu-id="c7937-239">hello 쿼리에 두 단계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-239">hello query contains two steps.</span></span></li>
<li><span data-ttu-id="c7937-240">Hello 단계 모두 분할 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-240">Neither of hello steps is partitioned.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="c7937-241">6</span><span class="sxs-lookup"><span data-stu-id="c7937-241">6</span></span></td></tr>

<tr><td>
<ul>
<li><span data-ttu-id="c7937-242">hello 입력된 데이터 스트림은 3으로 분할 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-242">hello input data stream is partitioned by 3.</span></span></li>
<li><span data-ttu-id="c7937-243">hello 쿼리에 두 단계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-243">hello query contains two steps.</span></span> <span data-ttu-id="c7937-244">hello 입력된 단계를 분할 및 hello 두 번째 단계는 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-244">hello input step is partitioned and hello second step is not.</span></span></li>
<li><span data-ttu-id="c7937-245">hello <strong>선택</strong> 문은 분할 hello 입력에서 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-245">hello <strong>SELECT</strong> statement reads from hello partitioned input.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="c7937-246">24(분할된 단계에 대한 18+분할되지 않은 단계에 대한 6)</span><span class="sxs-lookup"><span data-stu-id="c7937-246">24 (18 for partitioned steps + 6 for non-partitioned steps)</span></span></td></tr>
</table>

### <a name="examples-of-scaling"></a><span data-ttu-id="c7937-247">크기 조정 예제</span><span class="sxs-lookup"><span data-stu-id="c7937-247">Examples of scaling</span></span>

<span data-ttu-id="c7937-248">hello 다음 쿼리 수를 계산 hello 자동차에 세 개의 tollbooths 유료 스테이션을 진행 하 고 3 분 창 내에서.</span><span class="sxs-lookup"><span data-stu-id="c7937-248">hello following query calculates hello number of cars within a three-minute window going through a toll station that has three tollbooths.</span></span> <span data-ttu-id="c7937-249">이 쿼리는 toosix SUs 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-249">This query can be scaled up toosix SUs.</span></span>

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="c7937-250">더 많은 toouse SUs에 대 한 쿼리 hello, 입력된 데이터 스트림을 hello 둘 다 및 hello 쿼리를 분할 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-250">toouse more SUs for hello query, both hello input data stream and hello query must be partitioned.</span></span> <span data-ttu-id="c7937-251">Hello 데이터 스트림 파티션 too3, 설정 되었으므로 hello 다음 수정 된 쿼리를 확장할 수 있습니다 too18 SUs:</span><span class="sxs-lookup"><span data-stu-id="c7937-251">Since hello data stream partition is set too3, hello following modified query can be scaled up too18 SUs:</span></span>

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="c7937-252">쿼리를 분할 hello 입력된 이벤트 처리 되 고 별도 파티션 그룹에 집계 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-252">When a query is partitioned, hello input events are processed and aggregated in separate partition groups.</span></span> <span data-ttu-id="c7937-253">출력 이벤트의 각 hello 그룹에 대해 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-253">Output events are also generated for each of hello groups.</span></span> <span data-ttu-id="c7937-254">분할 때 hello에 일부 예기치 않은 결과가 발생할 수 있습니다 **GROUP BY** hello 입력된 데이터 스트림에 hello 파티션 키 필드가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-254">Partitioning can cause some unexpected results when hello **GROUP BY** field is not hello partition key in hello input data stream.</span></span> <span data-ttu-id="c7937-255">예를 들어 hello **TollBoothId** hello 이전 쿼리에서 필드의 hello 파티션 키 않습니다 **Input1**합니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-255">For example, hello **TollBoothId** field in hello previous query is not hello partition key of **Input1**.</span></span> <span data-ttu-id="c7937-256">hello 결과 해당 hello 여러 파티션에 톨게이트 # 1에서 데이터를 분산 시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-256">hello result is that hello data from TollBooth #1 can be spread in multiple partitions.</span></span>

<span data-ttu-id="c7937-257">각 hello **Input1** 스트림 분석 하 여 파티션을 별도로 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-257">Each of hello **Input1** partitions will be processed separately by Stream Analytics.</span></span> <span data-ttu-id="c7937-258">결과적으로, 여러 레코드의 hello 자동차 수 hello 동일한 요금에 hello 같은 텀블 링 창 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-258">As a result, multiple records of hello car count for hello same tollbooth in hello same Tumbling window will be created.</span></span> <span data-ttu-id="c7937-259">Hello 입력된 파티션 키를 변경할 수 없는 경우에 다음 예제는 hello와 같이 아닌 파티션 단계를 추가 하 여이 문제를 해결할 수 있습니다.:</span><span class="sxs-lookup"><span data-stu-id="c7937-259">If hello input partition key can't be changed, this problem can be fixed by adding a non-partition step, as in hello following example:</span></span>

    WITH Step1 AS (
        SELECT COUNT(*) AS Count, TollBoothId
        FROM Input1 Partition By PartitionId
        GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1
    GROUP BY TumblingWindow(minute, 3), TollBoothId

<span data-ttu-id="c7937-260">이 쿼리는 크기 조정 된 too24 SUs 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-260">This query can be scaled too24 SUs.</span></span>

> [!NOTE]
> <span data-ttu-id="c7937-261">두 스트림을 조인 하는 경우는 hello 스트림을 분할 된 hello 열의 hello 파티션 키로 toocreate hello 조인을 사용 하 여 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-261">If you are joining two streams, make sure that hello streams are partitioned by hello partition key of hello column that you use toocreate hello joins.</span></span> <span data-ttu-id="c7937-262">또한 hello 했는지를 확인 동일한 수의 파티션 두 스트림이 모두에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-262">Also make sure that you have hello same number of partitions in both streams.</span></span>
> 
> 

## <a name="configure-stream-analytics-streaming-units"></a><span data-ttu-id="c7937-263">Stream Analytics 스트리밍 단위 구성</span><span class="sxs-lookup"><span data-stu-id="c7937-263">Configure Stream Analytics streaming units</span></span>

1. <span data-ttu-id="c7937-264">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-264">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c7937-265">리소스의 hello 목록에서 tooscale 원하고 엽니다 hello 스트림 분석 작업을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-265">In hello list of resources, find hello Stream Analytics job that you want tooscale and then open it.</span></span>
3. <span data-ttu-id="c7937-266">Hello 블레이드에서 아래에서 작업 **구성**, 클릭 **배율**합니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-266">In hello job blade, under **Configure**, click **Scale**.</span></span>

    ![Azure Portal Stream Analytics 작업 구성][img.stream.analytics.preview.portal.settings.scale]

4. <span data-ttu-id="c7937-268">Hello 작업에 대 한 hello 슬라이더 tooset hello SUs를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-268">Use hello slider tooset hello SUs for hello job.</span></span> <span data-ttu-id="c7937-269">제한 된 toospecific SU 설정이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-269">Notice that you are limited toospecific SU settings.</span></span>


## <a name="monitor-job-performance"></a><span data-ttu-id="c7937-270">작업 성능 모니터링</span><span class="sxs-lookup"><span data-stu-id="c7937-270">Monitor job performance</span></span>
<span data-ttu-id="c7937-271">Hello Azure 포털을 사용 하는 작업의 hello 처리량을 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-271">Using hello Azure portal, you can track hello throughput of a job:</span></span>

![Azure Stream Analytics 모니터링 작업][img.stream.analytics.monitor.job]

<span data-ttu-id="c7937-273">Hello 워크 로드의 hello 예상 처리량을 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-273">Calculate hello expected throughput of hello workload.</span></span> <span data-ttu-id="c7937-274">Hello 처리량 예상 보다 작은 경우 hello 입력된 파티션 튜닝 하 hello 쿼리를 조정 하 고 SUs tooyour 작업을 추가.</span><span class="sxs-lookup"><span data-stu-id="c7937-274">If hello throughput is less than expected, tune hello input partition, tune hello query, and add SUs tooyour job.</span></span>


## <a name="visualize-stream-analytics-throughput-at-scale-hello-raspberry-pi-scenario"></a><span data-ttu-id="c7937-275">최대 규모로 처리량 스트림 분석 시각화: hello 라스베리 Pi 시나리오</span><span class="sxs-lookup"><span data-stu-id="c7937-275">Visualize Stream Analytics throughput at scale: hello Raspberry Pi scenario</span></span>
<span data-ttu-id="c7937-276">스트림 분석 작업 확장 하는 방법을 이해 toohelp, 라스베리 Pi 장치에서 입력을 기반으로 하는 실험을 수행 했습니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-276">toohelp you understand how Stream Analytics jobs scale, we performed an experiment based on input from a Raspberry Pi device.</span></span> <span data-ttu-id="c7937-277">이 실험 사용 응 여러 스트리밍 단위와 파티션 처리량에 hello 결과 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-277">This experiment let us see hello effect on throughput of multiple streaming units and partitions.</span></span>

<span data-ttu-id="c7937-278">이 시나리오에서는 hello 장치 센서 데이터 (클라이언트) tooan 이벤트 허브를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-278">In this scenario, hello device sends sensor data (clients) tooan event hub.</span></span> <span data-ttu-id="c7937-279">스트리밍 분석 hello 데이터를 처리 하 고 출력 tooanother 이벤트 허브로 경고나 통계를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-279">Streaming Analytics processes hello data and sends an alert or statistics as an output tooanother event hub.</span></span> 

<span data-ttu-id="c7937-280">클라이언트 hello JSON 형식의 센서 데이터를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-280">hello client sends sensor data in JSON format.</span></span> <span data-ttu-id="c7937-281">hello 데이터 출력 JSON 형식 이기도합니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-281">hello data output is also in JSON format.</span></span> <span data-ttu-id="c7937-282">hello 데이터는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-282">hello data looks like this:</span></span>

    {"devicetime":"2014-12-11T02:24:56.8850110Z","hmdt":42.7,"temp":72.6,"prss":98187.75,"lght":0.38,"dspl":"R-PI Olivier's Office"}

<span data-ttu-id="c7937-283">다음 쿼리는 hello 광원이 해제 되어 사용 되는 toosend 경고입니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-283">hello following query is used toosend an alert when a light is switched off:</span></span>

    SELECT AVG(lght),
     "LightOff" as AlertText
    FROM input TIMESTAMP
    BY devicetime
     WHERE
        lght< 0.05 GROUP BY TumblingWindow(second, 1)

### <a name="measure-throughput"></a><span data-ttu-id="c7937-284">처리량 측정</span><span class="sxs-lookup"><span data-stu-id="c7937-284">Measure throughput</span></span>

<span data-ttu-id="c7937-285">이 컨텍스트에서 처리량이 hello 용량 고정된 된 양의 시간에서 스트림 분석에서 처리 하는 입력된 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-285">In this context, throughput is hello amount of input data processed by Stream Analytics in a fixed amount of time.</span></span> <span data-ttu-id="c7937-286">(측정 했습니다 10 분 동안.) hello에 대 한 tooachieve hello 최상의 처리 처리량 입력 데이터, 두 hello 데이터 스트림 입력 및 hello 쿼리 분할 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-286">(We measured for 10 minutes.) tooachieve hello best processing throughput for hello input data, both hello data stream input and hello query were  partitioned.</span></span> <span data-ttu-id="c7937-287">포함 **count ()** hello 쿼리 toomeasure 입력된 이벤트 수 처리 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-287">We included **COUNT()** in hello query toomeasure how many input events were processed.</span></span> <span data-ttu-id="c7937-288">입력된 이벤트 toocome toomake 있는지 hello 작업이 단순히 대기 하지, hello 입력된 이벤트 허브의 각 파티션에 약 300MB 입력된 데이터의 미리 채워진 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-288">toomake sure hello job was not simply waiting for input events toocome, each partition of hello input event hub was preloaded with about 300 MB of input data.</span></span>

<span data-ttu-id="c7937-289">hello 다음 표에 hello 결과가 나와 hello 스트리밍 단위 수가 증가 하 고 hello 해당 파티션 수를 이벤트 허브에 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-289">hello following table shows hello results we saw when we increased hello number of streaming units and hello corresponding partition counts in event hubs.</span></span>  

<table border="1">
<tr><th><span data-ttu-id="c7937-290">입력 파티션</span><span class="sxs-lookup"><span data-stu-id="c7937-290">Input Partitions</span></span></th><th><span data-ttu-id="c7937-291">출력 파티션</span><span class="sxs-lookup"><span data-stu-id="c7937-291">Output Partitions</span></span></th><th><span data-ttu-id="c7937-292">스트리밍 단위</span><span class="sxs-lookup"><span data-stu-id="c7937-292">Streaming Units</span></span></th><th><span data-ttu-id="c7937-293">지속적인 처리량</span><span class="sxs-lookup"><span data-stu-id="c7937-293">Sustained Throughput</span></span>
</th></td>

<tr><td><span data-ttu-id="c7937-294">12</span><span class="sxs-lookup"><span data-stu-id="c7937-294">12</span></span></td>
<td><span data-ttu-id="c7937-295">12</span><span class="sxs-lookup"><span data-stu-id="c7937-295">12</span></span></td>
<td><span data-ttu-id="c7937-296">6</span><span class="sxs-lookup"><span data-stu-id="c7937-296">6</span></span></td>
<td><span data-ttu-id="c7937-297">4.06MB/초</span><span class="sxs-lookup"><span data-stu-id="c7937-297">4.06 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="c7937-298">12</span><span class="sxs-lookup"><span data-stu-id="c7937-298">12</span></span></td>
<td><span data-ttu-id="c7937-299">12</span><span class="sxs-lookup"><span data-stu-id="c7937-299">12</span></span></td>
<td><span data-ttu-id="c7937-300">12</span><span class="sxs-lookup"><span data-stu-id="c7937-300">12</span></span></td>
<td><span data-ttu-id="c7937-301">8.06 MB/초</span><span class="sxs-lookup"><span data-stu-id="c7937-301">8.06 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="c7937-302">48</span><span class="sxs-lookup"><span data-stu-id="c7937-302">48</span></span></td>
<td><span data-ttu-id="c7937-303">48</span><span class="sxs-lookup"><span data-stu-id="c7937-303">48</span></span></td>
<td><span data-ttu-id="c7937-304">48</span><span class="sxs-lookup"><span data-stu-id="c7937-304">48</span></span></td>
<td><span data-ttu-id="c7937-305">38.32 MB/초</span><span class="sxs-lookup"><span data-stu-id="c7937-305">38.32 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="c7937-306">192</span><span class="sxs-lookup"><span data-stu-id="c7937-306">192</span></span></td>
<td><span data-ttu-id="c7937-307">192</span><span class="sxs-lookup"><span data-stu-id="c7937-307">192</span></span></td>
<td><span data-ttu-id="c7937-308">192</span><span class="sxs-lookup"><span data-stu-id="c7937-308">192</span></span></td>
<td><span data-ttu-id="c7937-309">172.67 MB/초</span><span class="sxs-lookup"><span data-stu-id="c7937-309">172.67 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="c7937-310">480</span><span class="sxs-lookup"><span data-stu-id="c7937-310">480</span></span></td>
<td><span data-ttu-id="c7937-311">480</span><span class="sxs-lookup"><span data-stu-id="c7937-311">480</span></span></td>
<td><span data-ttu-id="c7937-312">480</span><span class="sxs-lookup"><span data-stu-id="c7937-312">480</span></span></td>
<td><span data-ttu-id="c7937-313">454.27 MB/초</span><span class="sxs-lookup"><span data-stu-id="c7937-313">454.27 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="c7937-314">720</span><span class="sxs-lookup"><span data-stu-id="c7937-314">720</span></span></td>
<td><span data-ttu-id="c7937-315">720</span><span class="sxs-lookup"><span data-stu-id="c7937-315">720</span></span></td>
<td><span data-ttu-id="c7937-316">720</span><span class="sxs-lookup"><span data-stu-id="c7937-316">720</span></span></td>
<td><span data-ttu-id="c7937-317">609.69 MB/초</span><span class="sxs-lookup"><span data-stu-id="c7937-317">609.69 MB/s</span></span></td>
</tr>
</table>

<span data-ttu-id="c7937-318">되며 hello 다음 그래프에서는 SUs 및 처리량 사이의 hello 관계를 시각화 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7937-318">And hello following graph shows a visualization of hello relationship between SUs and throughput.</span></span>

![img.stream.analytics.perfgraph][img.stream.analytics.perfgraph]

## <a name="get-help"></a><span data-ttu-id="c7937-320">도움말 보기</span><span class="sxs-lookup"><span data-stu-id="c7937-320">Get help</span></span>
<span data-ttu-id="c7937-321">추가 지원이 필요한 경우 [Azure Stream Analytics 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c7937-321">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c7937-322">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c7937-322">Next steps</span></span>
* [<span data-ttu-id="c7937-323">스트림 분석 소개 tooAzure</span><span class="sxs-lookup"><span data-stu-id="c7937-323">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="c7937-324">Azure Stream Analytics 사용 시작</span><span class="sxs-lookup"><span data-stu-id="c7937-324">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="c7937-325">Azure Stream Analytics 쿼리 언어 참조</span><span class="sxs-lookup"><span data-stu-id="c7937-325">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="c7937-326">Azure Stream Analytics 관리 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="c7937-326">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Image references-->

[img.stream.analytics.monitor.job]: ./media/stream-analytics-scale-jobs/StreamAnalytics.job.monitor-NewPortal.png
[img.stream.analytics.configure.scale]: ./media/stream-analytics-scale-jobs/StreamAnalytics.configure.scale.png
[img.stream.analytics.perfgraph]: ./media/stream-analytics-scale-jobs/perf.png
[img.stream.analytics.streaming.units.scale]: ./media/stream-analytics-scale-jobs/StreamAnalyticsStreamingUnitsExample.jpg
[img.stream.analytics.preview.portal.settings.scale]: ./media/stream-analytics-scale-jobs/StreamAnalyticsPreviewPortalJobSettings-NewPortal.png   

<!--Link references-->

[microsoft.support]: http://support.microsoft.com
[azure.management.portal]: http://manage.windowsazure.com
[azure.event.hubs.developer.guide]: http://msdn.microsoft.com/library/azure/dn789972.aspx

[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301


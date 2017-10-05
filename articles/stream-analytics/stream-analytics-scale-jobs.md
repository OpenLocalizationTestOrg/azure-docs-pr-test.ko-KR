---
title: "처리량을 높이기 위한 Stream Analytics 작업 규모 지정 | Microsoft Docs"
description: "입력 파티션을 구성하고, 쿼리 정의를 조정하고, 작업 스트리밍 단위를 설정하여 Stream Analytics 작업의 크기를 조정하는 방법을 알아봅니다."
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
ms.openlocfilehash: ab894976c72ea3785d7f58e51b3dd64511e1e8e3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="scale-azure-stream-analytics-jobs-to-increase-stream-data-processing-throughput"></a><span data-ttu-id="1f372-104">Azure Stream Analytics 작업 크기를 조정하여 스트림 데이터 처리량 증가</span><span class="sxs-lookup"><span data-stu-id="1f372-104">Scale Azure Stream Analytics jobs to increase stream data processing throughput</span></span>
<span data-ttu-id="1f372-105">이 문서에서는 Streaming Analytics 작업에 대한 처리량을 증가시키기 위해 Stream Analytics 쿼리를 조정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-105">This article shows you how to tune a Stream Analytics query to increase throughput for Streaming Analytics jobs.</span></span> <span data-ttu-id="1f372-106">입력 파티션을 구성하고, 분석 쿼리 정의를 조정하고, 작업 *SU(스트리밍 단위)*를 계산 및 설정하여 Stream Analytics 작업의 크기를 조정하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-106">You learn how to scale Stream Analytics jobs by configuring input partitions, tuning the analytics query definition, and calculating and setting job *streaming units* (SUs).</span></span> 

## <a name="what-are-the-parts-of-a-stream-analytics-job"></a><span data-ttu-id="1f372-107">Stream Analytics 작업은 무엇으로 구성되나요?</span><span class="sxs-lookup"><span data-stu-id="1f372-107">What are the parts of a Stream Analytics job?</span></span>
<span data-ttu-id="1f372-108">Stream Analytics 작업 정의에는 입력, 쿼리 및 출력이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-108">A Stream Analytics job definition includes inputs, a query, and output.</span></span> <span data-ttu-id="1f372-109">입력은 작업이 데이터 스트림을 읽는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-109">Inputs are where the job reads the data stream from.</span></span> <span data-ttu-id="1f372-110">쿼리는 데이터 입력 스트림을 변환하는 데 사용되며, 출력은 작업이 작업 결과를 전송하는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-110">The query is used to transform the data input stream, and the output is where the job sends the job results to.</span></span>  

<span data-ttu-id="1f372-111">작업에는 데이터 스트림에 대해 하나 이상의 입력 소스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-111">A job requires at least one input source for data streaming.</span></span> <span data-ttu-id="1f372-112">데이터 스트림 입력 원본은 Azure 이벤트 허브 또는 Azure Blob Storage에 저장될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-112">The data stream input source can be stored in an Azure event hub or in Azure blob storage.</span></span> <span data-ttu-id="1f372-113">자세한 내용은 [Azure Stream Analytics 소개](stream-analytics-introduction.md) 및 [Azure Stream Analytics 사용 시작](stream-analytics-real-time-fraud-detection.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1f372-113">For more information, see [Introduction to Azure Stream Analytics](stream-analytics-introduction.md) and [Get started using Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md).</span></span>

## <a name="partitions-in-event-hubs-and-azure-storage"></a><span data-ttu-id="1f372-114">이벤트 허브와 Azure Storage의 파티션</span><span class="sxs-lookup"><span data-stu-id="1f372-114">Partitions in event hubs and Azure storage</span></span>
<span data-ttu-id="1f372-115">Stream Analytics 작업 크기 조정은 입력 또는 출력에 있는 파티션을 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-115">Scaling a Stream Analytics job takes advantage of partitions in the input or output.</span></span> <span data-ttu-id="1f372-116">분할을 통해 데이터를 파티션 키에 따라 하위 집합으로 분할할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-116">Partitioning lets you divide data into subsets based on a partition key.</span></span> <span data-ttu-id="1f372-117">데이터를 사용하는 프로세스(예: Streaming Analytics 작업)는 서로 다른 파티션을 병렬로 사용 및 기록하여 처리량을 증가시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-117">A process that consumes the data (such as a Streaming Analytics job) can consume and write different partitions in parallel, which increases throughput.</span></span> <span data-ttu-id="1f372-118">Streaming Analytics로 작업할 때 이벤트 허브 및 Blob Storage에서 분할을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-118">When you work with Streaming Analytics, you can take advantage of partitioning in event hubs and in Blob storage.</span></span> 

<span data-ttu-id="1f372-119">파티션에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1f372-119">For more information about partitions, see the following articles:</span></span>

* [<span data-ttu-id="1f372-120">Event Hubs 기능 개요</span><span class="sxs-lookup"><span data-stu-id="1f372-120">Event Hubs features overview</span></span>](../event-hubs/event-hubs-features.md#partitions)
* [<span data-ttu-id="1f372-121">데이터 분할</span><span class="sxs-lookup"><span data-stu-id="1f372-121">Data partitioning</span></span>](https://docs.microsoft.com/azure/architecture/best-practices/data-partitioning#partitioning-azure-blob-storage)


## <a name="streaming-units-sus"></a><span data-ttu-id="1f372-122">SU(스트리밍 단위)</span><span class="sxs-lookup"><span data-stu-id="1f372-122">Streaming units (SUs)</span></span>
<span data-ttu-id="1f372-123">SU(스트리밍 단위)는 Azure Stream Analytics 작업을 실행하는 데 필요한 리소스 및 계산 능력을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-123">Streaming units (SUs) represent the resources and computing power that are required in order to execute an Azure Stream Analytics job.</span></span> <span data-ttu-id="1f372-124">SU는 CPU, 메모리의 혼합된 측정치 및 읽기/쓰기 속도를 기반으로 상대적 이벤트 처리 용량을 설명하는 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-124">SUs provide a way to describe the relative event processing capacity based on a blended measure of CPU, memory, and read and write rates.</span></span> <span data-ttu-id="1f372-125">각 SU는 대략 1MB/초의 처리량에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-125">Each SU corresponds to roughly 1 MB/second of throughput.</span></span> 

<span data-ttu-id="1f372-126">특정 작업에 필요한 SU 수 선택은 입력에 대한 파티션 구성 및 작업에 정의된 쿼리에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-126">Choosing how many SUs are required for a particular job depends on the partition configuration for the inputs and on the query defined for the job.</span></span> <span data-ttu-id="1f372-127">작업에 대해 SU의 할당량까지 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-127">You can select up to your quota in SUs for a job.</span></span> <span data-ttu-id="1f372-128">기본적으로 각 Azure 구독에는 특정 지역의 모든 분석 작업에 대해 최대 50개의 SU 할당량이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-128">By default, each Azure subscription has a quota of up to 50 SUs for all the analytics jobs in a specific region.</span></span> <span data-ttu-id="1f372-129">구독의 SU를 이 할당량을 초과하여 늘리려면 [Microsoft 지원](http://support.microsoft.com)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="1f372-129">To increase SUs for your subscriptions beyond this quota, contact [Microsoft Support](http://support.microsoft.com).</span></span> <span data-ttu-id="1f372-130">작업당 SU에 대한 유효한 값은 1, 3, 6이며 6 단위로 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-130">Valid values for SUs per job are 1, 3, 6, and up in increments of 6.</span></span>

## <a name="embarrassingly-parallel-jobs"></a><span data-ttu-id="1f372-131">병렬 처리가 적합한 작업</span><span class="sxs-lookup"><span data-stu-id="1f372-131">Embarrassingly parallel jobs</span></span>
<span data-ttu-id="1f372-132">*병렬 처리가 적합한* 작업은 Azure Stream Analytics에서 가장 확장성이 뛰어난 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-132">An *embarrassingly parallel* job is the most scalable scenario we have in Azure Stream Analytics.</span></span> <span data-ttu-id="1f372-133">하나의 쿼리 인스턴스에 대한 하나의 입력 파티션을 하나의 출력 파티션에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-133">It connects one partition of the input to one instance of the query to one partition of the output.</span></span> <span data-ttu-id="1f372-134">이 병렬 처리에는 다음 요구 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-134">This parallelism has the following requirements:</span></span>

1. <span data-ttu-id="1f372-135">쿼리 논리가 동일한 쿼리 인스턴스에서 처리되는 동일한 키에 따라 다른 경우 이벤트가 동일한 입력 파티션으로 이동하는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-135">If your query logic depends on the same key being processed by the same query instance, you must make sure that the events go to the same partition of your input.</span></span> <span data-ttu-id="1f372-136">이벤트 허브의 경우 이것은 이벤트 데이터에 **PartitionKey** 값이 설정되어야 함을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-136">For event hubs, this means that the event data must have the **PartitionKey** value set.</span></span> <span data-ttu-id="1f372-137">또는 분할된 보낸 사람을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-137">Alternatively, you can use partitioned senders.</span></span> <span data-ttu-id="1f372-138">Blob Storage의 경우 이것은 이벤트가 같은 파티션 폴더에 전송된다는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-138">For blob storage, this means that the events are sent to the same partition folder.</span></span> <span data-ttu-id="1f372-139">쿼리 논리가 동일한 쿼리 인스턴스에서 동일한 키를 처리할 필요가 없는 경우 이 요구 사항을 무시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-139">If your query logic does not require the same key to be processed by the same query instance, you can ignore this requirement.</span></span> <span data-ttu-id="1f372-140">이 논리에 대한 예로 간단한 선택/프로젝트/필터 쿼리를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1f372-140">An example of this logic would be a simple select-project-filter query.</span></span>  

2. <span data-ttu-id="1f372-141">데이터가 입력 측에 배치되면 쿼리가 분할되었는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-141">Once the data is laid out on the input side, you must make sure that your query is partitioned.</span></span> <span data-ttu-id="1f372-142">그러려면 모든 단계에서 **Partition By**를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-142">This requires you to use **Partition By** in all the steps.</span></span> <span data-ttu-id="1f372-143">여러 단계가 허용되지만 모두 동일한 키로 분할되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-143">Multiple steps are allowed, but they all must be partitioned by the same key.</span></span> <span data-ttu-id="1f372-144">현재는 작업을 완전히 병렬로 처리하기 위해 분할 키를 **PartitionId**로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-144">Currently, the partitioning key must be set to **PartitionId** in order for the job to be fully parallel.</span></span>  

3. <span data-ttu-id="1f372-145">현재는 이벤트 허브 및 Blob Storage만 분할된 출력을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-145">Currently only event hubs and blob storage support partitioned output.</span></span> <span data-ttu-id="1f372-146">이벤트 허브 출력에 대해 파티션 키를 **PartitionId**로 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-146">For event hub output, you must configure the partition key to be **PartitionId**.</span></span> <span data-ttu-id="1f372-147">Blob Storage 출력의 경우 필요한 작업이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-147">For blob storage output, you don't have to do anything.</span></span>  

4. <span data-ttu-id="1f372-148">입력 파티션 수가 출력 파티션 수와 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-148">The number of input partitions must equal the number of output partitions.</span></span> <span data-ttu-id="1f372-149">Blob Storage 출력은 현재 파티션을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-149">Blob storage output doesn't currently support partitions.</span></span> <span data-ttu-id="1f372-150">하지만 업스트림 쿼리의 분할 스키마를 상속하므로 문제되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-150">But that's okay, because it inherits the partitioning scheme of the upstream query.</span></span> <span data-ttu-id="1f372-151">다음은 완전한 병렬 작업을 허용하는 파티션 값의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-151">Here are examples of partition values that allow a fully parallel job:</span></span>  

   * <span data-ttu-id="1f372-152">8개의 이벤트 허브 입력 파티션 및 8개의 이벤트 허브 출력 파티션</span><span class="sxs-lookup"><span data-stu-id="1f372-152">8 event hub input partitions and 8 event hub output partitions</span></span>
   * <span data-ttu-id="1f372-153">8개의 이벤트 허브 입력 파티션 및 Blob Storage 출력</span><span class="sxs-lookup"><span data-stu-id="1f372-153">8 event hub input partitions and blob storage output</span></span>  
   * <span data-ttu-id="1f372-154">8개의 Blob Storage 입력 파티션 및 Blob Storage 출력</span><span class="sxs-lookup"><span data-stu-id="1f372-154">8 blob storage input partitions and blob storage output</span></span>  
   * <span data-ttu-id="1f372-155">8개의 Blob Storage 입력 파티션 및 8개의 이벤트 허브 출력 파티션</span><span class="sxs-lookup"><span data-stu-id="1f372-155">8 blob storage input partitions and 8 event hub output partitions</span></span>  

<span data-ttu-id="1f372-156">다음 섹션에서는 병렬 처리가 적합한 작업의 몇 가지 예제 시나리오를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-156">The following sections discuss some example scenarios that are embarrassingly parallel.</span></span>

### <a name="simple-query"></a><span data-ttu-id="1f372-157">단순 쿼리</span><span class="sxs-lookup"><span data-stu-id="1f372-157">Simple query</span></span>

* <span data-ttu-id="1f372-158">입력: 8개의 파티션이 있는 이벤트 허브</span><span class="sxs-lookup"><span data-stu-id="1f372-158">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="1f372-159">출력: 8개의 파티션이 있는 이벤트 허브</span><span class="sxs-lookup"><span data-stu-id="1f372-159">Output: Event hub with 8 partitions</span></span>

<span data-ttu-id="1f372-160">쿼리:</span><span class="sxs-lookup"><span data-stu-id="1f372-160">Query:</span></span>

    SELECT TollBoothId
    FROM Input1 Partition By PartitionId
    WHERE TollBoothId > 100

<span data-ttu-id="1f372-161">이 쿼리는 간단한 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-161">This query is a simple filter.</span></span> <span data-ttu-id="1f372-162">따라서 이벤트 허브로 전송되는 입력을 분할하는 것에 대해 걱정하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-162">Therefore, we don't need to worry about partitioning the input that is being sent to the event hub.</span></span> <span data-ttu-id="1f372-163">쿼리가 **Partition By PartitionId**를 포함하므로 앞에서 언급된 요구 사항 2번을 충족합니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-163">Notice that the query includes **Partition By PartitionId**, so it fulfills requirement #2 from earlier.</span></span> <span data-ttu-id="1f372-164">출력의 경우 파티션 키가 **PartitionId**로 설정되도록 작업에서 이벤트 허브 출력을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-164">For the output, we need to configure the event hub output in the job to have the parition key set to **PartitionId**.</span></span> <span data-ttu-id="1f372-165">마지막 한 가지 검사는 입력 파티션 수가 출력 파티션 수와 같은지 확인하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-165">One last check is to make sure that the number of input partitions is equal to the number of output partitions.</span></span>

### <a name="query-with-a-grouping-key"></a><span data-ttu-id="1f372-166">그룹화 키가 있는 쿼리</span><span class="sxs-lookup"><span data-stu-id="1f372-166">Query with a grouping key</span></span>

* <span data-ttu-id="1f372-167">입력: 8개의 파티션이 있는 이벤트 허브</span><span class="sxs-lookup"><span data-stu-id="1f372-167">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="1f372-168">출력: Blob Storage</span><span class="sxs-lookup"><span data-stu-id="1f372-168">Output: Blob storage</span></span>

<span data-ttu-id="1f372-169">쿼리:</span><span class="sxs-lookup"><span data-stu-id="1f372-169">Query:</span></span>

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="1f372-170">이 쿼리에 그룹화 키가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-170">This query has a grouping key.</span></span> <span data-ttu-id="1f372-171">따라서 동일한 키는 동일한 쿼리 인스턴스에 의해 처리되어야 하며 이벤트를 분할된 방식으로 이벤트 허브로 보내야 함을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-171">Therefore, the same key needs to be processed by the same query instance, which means that events must be sent to the event hub in a partitioned manner.</span></span> <span data-ttu-id="1f372-172">하지만 어떤 키를 사용해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="1f372-172">But which key should be used?</span></span> <span data-ttu-id="1f372-173">**PartitionId**는 작업 논리 개념입니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-173">**PartitionId** is a job-logic concept.</span></span> <span data-ttu-id="1f372-174">실제로 고려할 키는 **TollBoothId**이므로 이벤트 데이터의 **PartitionKey** 값은 **TollBoothId**여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-174">The key we actually care about is **TollBoothId**, so the **PartitionKey** value of the event data should be **TollBoothId**.</span></span> <span data-ttu-id="1f372-175">**Partition By**를 **PartitionId**로 설정하여 쿼리에서 이 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-175">We do this in the query by setting **Partition By** to **PartitionId**.</span></span> <span data-ttu-id="1f372-176">출력이 Blob Storage이므로 요구 사항 4번에 따라 파티션 키 값 구성에 대해 걱정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-176">Since the output is blob storage, we don't need to worry about configuring a partition key value, as per requirement #4.</span></span>

### <a name="multi-step-query-with-a-grouping-key"></a><span data-ttu-id="1f372-177">그룹화 키가 있는 다중 단계 쿼리</span><span class="sxs-lookup"><span data-stu-id="1f372-177">Multi-step query with a grouping key</span></span>
* <span data-ttu-id="1f372-178">입력: 8개의 파티션이 있는 이벤트 허브</span><span class="sxs-lookup"><span data-stu-id="1f372-178">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="1f372-179">출력: 8개의 파티션이 있는 이벤트 허브 인스턴스</span><span class="sxs-lookup"><span data-stu-id="1f372-179">Output: Event hub instance with 8 partitions</span></span>

<span data-ttu-id="1f372-180">쿼리:</span><span class="sxs-lookup"><span data-stu-id="1f372-180">Query:</span></span>

    WITH Step1 AS (
    SELECT COUNT(*) AS Count, TollBoothId, PartitionId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="1f372-181">이 쿼리는 그룹화 키가 있으므로 동일한 키가 동일한 쿼리 인스턴스에서 처리되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-181">This query has a grouping key, so the same key needs to be processed by the same query instance.</span></span> <span data-ttu-id="1f372-182">이전 예제와 동일한 전략을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-182">We can use the same strategy as in the previous example.</span></span> <span data-ttu-id="1f372-183">이 경우 쿼리에는 여러 단계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-183">In this case, the query has multiple steps.</span></span> <span data-ttu-id="1f372-184">각 단계에 **Partition By PartitionId**가 있나요?</span><span class="sxs-lookup"><span data-stu-id="1f372-184">Does each step have **Partition By PartitionId**?</span></span> <span data-ttu-id="1f372-185">예, 따라서 쿼리는 요구 사항 3번을 충족합니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-185">Yes, so the query fulfills requirement #3.</span></span> <span data-ttu-id="1f372-186">출력의 경우 이전에 설명한 것처럼 파티션 키를 **PartitionId**로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-186">For the output, we need to set the partition key to **PartitionId**, as discussed earlier.</span></span> <span data-ttu-id="1f372-187">또한 입력으로 동일한 파티션 수를 포함하는 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-187">We can also see that it has the same number of partitions as the input.</span></span>

## <a name="example-scenarios-that-are-not-embarrassingly-parallel"></a><span data-ttu-id="1f372-188">병렬 처리가 적합하지 *않은* 예제 시나리오</span><span class="sxs-lookup"><span data-stu-id="1f372-188">Example scenarios that are *not* embarrassingly parallel</span></span>

<span data-ttu-id="1f372-189">이전 섹션에서는 병렬 처리가 적합한 시나리오를 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-189">In the previous section, we showed some embarrassingly parallel scenarios.</span></span> <span data-ttu-id="1f372-190">이 섹션에서는 병렬 처리에 적합하기 위한 모든 요구 사항을 충족하지 않는 시나리오에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-190">In this section, we discuss scenarios that don't meet all the requirements to be embarrassingly parallel.</span></span> 

### <a name="mismatched-partition-count"></a><span data-ttu-id="1f372-191">일치하지 않는 파티션 수</span><span class="sxs-lookup"><span data-stu-id="1f372-191">Mismatched partition count</span></span>
* <span data-ttu-id="1f372-192">입력: 8개의 파티션이 있는 이벤트 허브</span><span class="sxs-lookup"><span data-stu-id="1f372-192">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="1f372-193">출력: 32개의 파티션이 있는 이벤트 허브</span><span class="sxs-lookup"><span data-stu-id="1f372-193">Output: Event hub with 32 partitions</span></span>

<span data-ttu-id="1f372-194">이 경우 쿼리 내용은 중요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-194">In this case, it doesn't matter what the query is.</span></span> <span data-ttu-id="1f372-195">입력 파티션 수가 출력 파티션 수와 일치하지 않는 토폴로지는 병렬 처리가 적합하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-195">If the input partition count doesn't match the output partition count, the topology isn't embarrassingly parallel.</span></span>

### <a name="not-using-event-hubs-or-blob-storage-as-output"></a><span data-ttu-id="1f372-196">이벤트 허브 또는 Blob Storage를 출력으로 사용하지 않음</span><span class="sxs-lookup"><span data-stu-id="1f372-196">Not using event hubs or blob storage as output</span></span>
* <span data-ttu-id="1f372-197">입력: 8개의 파티션이 있는 이벤트 허브</span><span class="sxs-lookup"><span data-stu-id="1f372-197">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="1f372-198">출력: PowerBI</span><span class="sxs-lookup"><span data-stu-id="1f372-198">Output: PowerBI</span></span>

<span data-ttu-id="1f372-199">PowerBI 출력은 현재 분할을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-199">PowerBI output doesn't currently support partitioning.</span></span> <span data-ttu-id="1f372-200">따라서 이 시나리오는 병렬 처리가 적합하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-200">Therefore, this scenario is not embarrassingly parallel.</span></span>

### <a name="multi-step-query-with-different-partition-by-values"></a><span data-ttu-id="1f372-201">서로 다른 Partition By 값이 있는 다중 단계 쿼리</span><span class="sxs-lookup"><span data-stu-id="1f372-201">Multi-step query with different Partition By values</span></span>
* <span data-ttu-id="1f372-202">입력: 8개의 파티션이 있는 이벤트 허브</span><span class="sxs-lookup"><span data-stu-id="1f372-202">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="1f372-203">출력: 8개의 파티션이 있는 이벤트 허브</span><span class="sxs-lookup"><span data-stu-id="1f372-203">Output: Event hub with 8 partitions</span></span>

<span data-ttu-id="1f372-204">쿼리:</span><span class="sxs-lookup"><span data-stu-id="1f372-204">Query:</span></span>

    WITH Step1 AS (
    SELECT COUNT(*) AS Count, TollBoothId, PartitionId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1 Partition By TollBoothId
    GROUP BY TumblingWindow(minute, 3), TollBoothId

<span data-ttu-id="1f372-205">보이는 것처럼 두 번째 단계에서는 **TollBoothId** 를 분할 키로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-205">As you can see, the second step uses **TollBoothId** as the partitioning key.</span></span> <span data-ttu-id="1f372-206">이 단계는 첫 번째 단계와 동일하지 않으므로 순서를 섞어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-206">This step is not the same as the first step, and it therefore requires us to do a shuffle.</span></span> 

<span data-ttu-id="1f372-207">앞의 예제에서는 병렬 처리가 적합한 토폴로지를 준수(또는 준수하지 않는) 일부 Stream Analytics 작업을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-207">The preceding examples show some Stream Analytics jobs that conform to (or don't) an embarrassingly parallel topology.</span></span> <span data-ttu-id="1f372-208">준수하는 경우 최대 규모의 가능성을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-208">If they do conform, they have the potential for maximum scale.</span></span> <span data-ttu-id="1f372-209">이러한 프로필 중 하나에 적합하지 않는 작업의 경우 향후 업데이트에서 크기 조정 지침이 제공될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-209">For jobs that don't fit one of these profiles, scaling guidance will be available in future updates.</span></span> <span data-ttu-id="1f372-210">현재는 다음 섹션에 있는 일반적인 지침을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="1f372-210">For now, use the general guidance in the following sections.</span></span>

## <a name="calculate-the-maximum-streaming-units-of-a-job"></a><span data-ttu-id="1f372-211">작업의 최대 스트리밍 단위 계산</span><span class="sxs-lookup"><span data-stu-id="1f372-211">Calculate the maximum streaming units of a job</span></span>
<span data-ttu-id="1f372-212">Stream Analytics 작업에 사용될 수 있는 스트리밍 단위의 총 수는 작업에 대해 정의된 쿼리의 단계 수와 각 단계에 대한 파티션 수에 따라 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-212">The total number of streaming units that can be used by a Stream Analytics job depends on the number of steps in the query defined for the job and the number of partitions for each step.</span></span>

### <a name="steps-in-a-query"></a><span data-ttu-id="1f372-213">쿼리의 단계</span><span class="sxs-lookup"><span data-stu-id="1f372-213">Steps in a query</span></span>
<span data-ttu-id="1f372-214">하나의 쿼리에는 하나 이상의 단계가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-214">A query can have one or many steps.</span></span> <span data-ttu-id="1f372-215">각 단계는 **WITH** 키워드를 사용하여 정의된 하위 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-215">Each step is a subquery defined by the **WITH** keyword.</span></span> <span data-ttu-id="1f372-216">**WITH** 키워드(한 개 쿼리만) 밖에 있는 쿼리도 한 단계로 계산됩니다. 예를 들어 다음 쿼리에서 **SELECT** 문입니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-216">The query that is outside the **WITH** keyword (one query only) is also counted as a step, such as the **SELECT** statement in the following query:</span></span>

    WITH Step1 AS (
        SELECT COUNT(*) AS Count, TollBoothId
        FROM Input1 Partition By PartitionId
        GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1
    GROUP BY TumblingWindow(minute,3), TollBoothId

<span data-ttu-id="1f372-217">이 쿼리에는 2개의 단계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-217">This query has two steps.</span></span>

> [!NOTE]
> <span data-ttu-id="1f372-218">이 쿼리는 문서 뒷부분에서 좀 더 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-218">This query is discussed in more detail later in the article.</span></span>
>  

### <a name="partition-a-step"></a><span data-ttu-id="1f372-219">단계 분할</span><span class="sxs-lookup"><span data-stu-id="1f372-219">Partition a step</span></span>
<span data-ttu-id="1f372-220">단계를 분할하려면 다음 조건이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-220">Partitioning a step requires the following conditions:</span></span>

* <span data-ttu-id="1f372-221">입력 소스는 분할해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-221">The input source must be partitioned.</span></span> 
* <span data-ttu-id="1f372-222">쿼리의 **SELECT** 문은 분할된 입력 원본에서 읽어와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-222">The **SELECT** statement of the query must read from a partitioned input source.</span></span>
* <span data-ttu-id="1f372-223">단계 내의 쿼리에는 **Partition By** 키워드가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-223">The query within the step must have the **Partition By** keyword.</span></span>

<span data-ttu-id="1f372-224">쿼리가 분할되면 입력 이벤트가 처리되고 별도의 파티션 그룹에 집계되며 각 그룹에 대해 출력 이벤트가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-224">When a query is partitioned, the input events are processed and aggregated in separate partition groups, and outputs events are generated for each of the groups.</span></span> <span data-ttu-id="1f372-225">결합된 집계를 원하는 경우 집계할 또 다른 분할되지 않은 단계를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-225">If you want a combined aggregate, you must create a second non-partitioned step to aggregate.</span></span>

### <a name="calculate-the-max-streaming-units-for-a-job"></a><span data-ttu-id="1f372-226">작업의 최대 스트리밍 단위 계산</span><span class="sxs-lookup"><span data-stu-id="1f372-226">Calculate the max streaming units for a job</span></span>
<span data-ttu-id="1f372-227">하나의 Stream Analytics 작업에 대해 분할되지 않은 모든 단계를 최대 6개의 SU(스트리밍 단위)로 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-227">All non-partitioned steps together can scale up to six streaming units (SUs) for a Stream Analytics job.</span></span> <span data-ttu-id="1f372-228">SU를 추가하려면 단계를 분할해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-228">To add SUs, a step must be partitioned.</span></span> <span data-ttu-id="1f372-229">각 파티션에는 6개의 SU가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-229">Each partition can have six SUs.</span></span>

<table border="1">
<tr><th><span data-ttu-id="1f372-230">쿼리</span><span class="sxs-lookup"><span data-stu-id="1f372-230">Query</span></span></th><th><span data-ttu-id="1f372-231">작업에 대한 최대 SU</span><span class="sxs-lookup"><span data-stu-id="1f372-231">Max SUs for the job</span></span></th></td>

<tr><td>
<ul>
<li><span data-ttu-id="1f372-232">쿼리는 한 단계를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-232">The query contains one step.</span></span></li>
<li><span data-ttu-id="1f372-233">이 단계는 분할되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-233">The step is not partitioned.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="1f372-234">6</span><span class="sxs-lookup"><span data-stu-id="1f372-234">6</span></span></td></tr>

<tr><td>
<ul>
<li><span data-ttu-id="1f372-235">입력 데이터 스트림은 3으로 분할됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-235">The input data stream is partitioned by 3.</span></span></li>
<li><span data-ttu-id="1f372-236">쿼리는 한 단계를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-236">The query contains one step.</span></span></li>
<li><span data-ttu-id="1f372-237">이 단계는 분할됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-237">The step is partitioned.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="1f372-238">18</span><span class="sxs-lookup"><span data-stu-id="1f372-238">18</span></span></td></tr>

<tr><td>
<ul>
<li><span data-ttu-id="1f372-239">쿼리는 두 단계를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-239">The query contains two steps.</span></span></li>
<li><span data-ttu-id="1f372-240">두 단계모두 분할되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-240">Neither of the steps is partitioned.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="1f372-241">6</span><span class="sxs-lookup"><span data-stu-id="1f372-241">6</span></span></td></tr>

<tr><td>
<ul>
<li><span data-ttu-id="1f372-242">입력 데이터 스트림은 3으로 분할됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-242">The input data stream is partitioned by 3.</span></span></li>
<li><span data-ttu-id="1f372-243">쿼리는 두 단계를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-243">The query contains two steps.</span></span> <span data-ttu-id="1f372-244">입력 단계는 분할되며 두 번째 단계는 분할되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-244">The input step is partitioned and the second step is not.</span></span></li>
<li><span data-ttu-id="1f372-245"><strong>SELECT</strong> 문은 분할된 입력에서 읽어옵니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-245">The <strong>SELECT</strong> statement reads from the partitioned input.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="1f372-246">24(분할된 단계에 대한 18+분할되지 않은 단계에 대한 6)</span><span class="sxs-lookup"><span data-stu-id="1f372-246">24 (18 for partitioned steps + 6 for non-partitioned steps)</span></span></td></tr>
</table>

### <a name="examples-of-scaling"></a><span data-ttu-id="1f372-247">크기 조정 예제</span><span class="sxs-lookup"><span data-stu-id="1f372-247">Examples of scaling</span></span>

<span data-ttu-id="1f372-248">다음 쿼리는 3분의 기간 내에 세 곳의 요금 징수소가 있는 요금 스테이션을 통과하는 자동차 수를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-248">The following query calculates the number of cars within a three-minute window going through a toll station that has three tollbooths.</span></span> <span data-ttu-id="1f372-249">이 쿼리는 6개 SU까지 확장될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-249">This query can be scaled up to six SUs.</span></span>

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="1f372-250">쿼리에 더 많은 SU를 사용하려면 입력 데이터 스트림 및 쿼리를 모두 분할해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-250">To use more SUs for the query, both the input data stream and the query must be partitioned.</span></span> <span data-ttu-id="1f372-251">데이터 스트림 파티션이 3으로 설정되므로 다음의 수정된 쿼리를 최대 18개 SU로 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-251">Since the data stream partition is set to 3, the following modified query can be scaled up to 18 SUs:</span></span>

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="1f372-252">쿼리가 분할되면 입력 이벤트가 처리되고 별도의 파티션 그룹에 집계되며 각 그룹에 대해 출력 이벤트가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-252">When a query is partitioned, the input events are processed and aggregated in separate partition groups.</span></span> <span data-ttu-id="1f372-253">출력 이벤트도 각 그룹에 대해 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-253">Output events are also generated for each of the groups.</span></span> <span data-ttu-id="1f372-254">**GROUP BY** 필드가 입력 데이터 스트림의 파티션 키가 아닌 상태에서 분할을 수행하면 예기치 않은 결과가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-254">Partitioning can cause some unexpected results when the **GROUP BY** field is not the partition key in the input data stream.</span></span> <span data-ttu-id="1f372-255">예를 들어 이전 쿼리의 **TollBoothId** 필드는 **Input1**의 파티션 키가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-255">For example, the **TollBoothId** field in the previous query is not the partition key of **Input1**.</span></span> <span data-ttu-id="1f372-256">따라서 TollBooth #1의 데이터는 여러 파티션으로 분산될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-256">The result is that the data from TollBooth #1 can be spread in multiple partitions.</span></span>

<span data-ttu-id="1f372-257">각각의 **Input1** 파티션은 Stream Analytics에 의해 별도로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-257">Each of the **Input1** partitions will be processed separately by Stream Analytics.</span></span> <span data-ttu-id="1f372-258">결과적으로, 동일한 연속 창에 동일한 요금 징수소에 대한 자동차 수 레코드가 여러 개 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-258">As a result, multiple records of the car count for the same tollbooth in the same Tumbling window will be created.</span></span> <span data-ttu-id="1f372-259">입력 파티션 키를 변경할 수 없는 경우 다음 예제처럼 비분할 단계를 추가하여 이 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-259">If the input partition key can't be changed, this problem can be fixed by adding a non-partition step, as in the following example:</span></span>

    WITH Step1 AS (
        SELECT COUNT(*) AS Count, TollBoothId
        FROM Input1 Partition By PartitionId
        GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1
    GROUP BY TumblingWindow(minute, 3), TollBoothId

<span data-ttu-id="1f372-260">이 쿼리는 24개 SU까지 확장될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-260">This query can be scaled to 24 SUs.</span></span>

> [!NOTE]
> <span data-ttu-id="1f372-261">두 스트림을 조인하는 경우 스트림이 조인을 생성하는 데 사용하는 열의 파티션 키별로 분할되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-261">If you are joining two streams, make sure that the streams are partitioned by the partition key of the column that you use to create the joins.</span></span> <span data-ttu-id="1f372-262">또한 두 스트림에서 파티션 수가 동일한지도 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-262">Also make sure that you have the same number of partitions in both streams.</span></span>
> 
> 

## <a name="configure-stream-analytics-streaming-units"></a><span data-ttu-id="1f372-263">Stream Analytics 스트리밍 단위 구성</span><span class="sxs-lookup"><span data-stu-id="1f372-263">Configure Stream Analytics streaming units</span></span>

1. <span data-ttu-id="1f372-264">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-264">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="1f372-265">리소스 목록에서 확장할 Stream Analytics 작업을 찾은 후 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-265">In the list of resources, find the Stream Analytics job that you want to scale and then open it.</span></span>
3. <span data-ttu-id="1f372-266">작업 블레이드의 **구성** 아래에서 **크기 조정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-266">In the job blade, under **Configure**, click **Scale**.</span></span>

    ![Azure Portal Stream Analytics 작업 구성][img.stream.analytics.preview.portal.settings.scale]

4. <span data-ttu-id="1f372-268">슬라이더를 사용하여 작업에 대한 SU를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-268">Use the slider to set the SUs for the job.</span></span> <span data-ttu-id="1f372-269">특정 SU 설정으로 제한되는 것을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-269">Notice that you are limited to specific SU settings.</span></span>


## <a name="monitor-job-performance"></a><span data-ttu-id="1f372-270">작업 성능 모니터링</span><span class="sxs-lookup"><span data-stu-id="1f372-270">Monitor job performance</span></span>
<span data-ttu-id="1f372-271">Azure Portal을 사용하여 작업 처리량을 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-271">Using the Azure portal, you can track the throughput of a job:</span></span>

![Azure Stream Analytics 모니터링 작업][img.stream.analytics.monitor.job]

<span data-ttu-id="1f372-273">워크로드의 예상 처리량을 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-273">Calculate the expected throughput of the workload.</span></span> <span data-ttu-id="1f372-274">처리량이 예상보다 더 작은 경우 입력 파티션을 조정하고, 쿼리를 조정하고, 작업에 SU를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-274">If the throughput is less than expected, tune the input partition, tune the query, and add SUs to your job.</span></span>


## <a name="visualize-stream-analytics-throughput-at-scale-the-raspberry-pi-scenario"></a><span data-ttu-id="1f372-275">규모별 Stream Analytics 처리량 시각화: Raspberry Pi 시나리오</span><span class="sxs-lookup"><span data-stu-id="1f372-275">Visualize Stream Analytics throughput at scale: the Raspberry Pi scenario</span></span>
<span data-ttu-id="1f372-276">Stream Analytics 작업의 크기를 조정하는 방법을 이해하기 위해 Raspberry Pi 장치의 입력을 기반으로 실험을 수행했습니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-276">To help you understand how Stream Analytics jobs scale, we performed an experiment based on input from a Raspberry Pi device.</span></span> <span data-ttu-id="1f372-277">이 실험을 통해 여러 스트리밍 단위 및 파티션의 처리량에 미치는 영향을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-277">This experiment let us see the effect on throughput of multiple streaming units and partitions.</span></span>

<span data-ttu-id="1f372-278">이 시나리오에서는 장치가 이벤트 허브로 센서 데이터(클라이언트)를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-278">In this scenario, the device sends sensor data (clients) to an event hub.</span></span> <span data-ttu-id="1f372-279">Streaming Analytics에서 데이터를 처리하고 경고 또는 통계를 다른 이벤트 허브에 대한 출력으로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-279">Streaming Analytics processes the data and sends an alert or statistics as an output to another event hub.</span></span> 

<span data-ttu-id="1f372-280">클라이언트는 JSON 형식의 센서 데이터를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-280">The client sends sensor data in JSON format.</span></span> <span data-ttu-id="1f372-281">데이터 출력도 JSON 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-281">The data output is also in JSON format.</span></span> <span data-ttu-id="1f372-282">데이터는 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-282">The data looks like this:</span></span>

    {"devicetime":"2014-12-11T02:24:56.8850110Z","hmdt":42.7,"temp":72.6,"prss":98187.75,"lght":0.38,"dspl":"R-PI Olivier's Office"}

<span data-ttu-id="1f372-283">다음 쿼리는 광원 스위치가 꺼진 경우 경고를 보내는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-283">The following query is used to send an alert when a light is switched off:</span></span>

    SELECT AVG(lght),
     "LightOff" as AlertText
    FROM input TIMESTAMP
    BY devicetime
     WHERE
        lght< 0.05 GROUP BY TumblingWindow(second, 1)

### <a name="measure-throughput"></a><span data-ttu-id="1f372-284">처리량 측정</span><span class="sxs-lookup"><span data-stu-id="1f372-284">Measure throughput</span></span>

<span data-ttu-id="1f372-285">이 컨텍스트에서 처리량은 고정된 시간 동안 Stream Analytics이 처리한 입력 데이터의 양입니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-285">In this context, throughput is the amount of input data processed by Stream Analytics in a fixed amount of time.</span></span> <span data-ttu-id="1f372-286">(10분 동안 측정했음) 입력 데이터에 대해 최상의 처리량을 달성하려면 데이터 스트림 입력 및 쿼리 모두 분할됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-286">(We measured for 10 minutes.) To achieve the best processing throughput for the input data, both the data stream input and the query were  partitioned.</span></span> <span data-ttu-id="1f372-287">처리된 입력 이벤트 수를 측정하기 위해 **COUNT()**를 쿼리에 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-287">We included **COUNT()** in the query to measure how many input events were processed.</span></span> <span data-ttu-id="1f372-288">작업이 발생할 입력 이벤트를 단순히 기다리고 있지 않도록 입력 이벤트 허브의 각 파티션이 입력 데이터(약 300MB)로 미리 로드되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-288">To make sure the job was not simply waiting for input events to come, each partition of the input event hub was preloaded with about 300 MB of input data.</span></span>

<span data-ttu-id="1f372-289">다음 표에서 스트리밍 단위 수와 이벤트 허브에서 해당 파티션 수를 늘렸을 때 나타나는 결과를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-289">The following table shows the results we saw when we increased the number of streaming units and the corresponding partition counts in event hubs.</span></span>  

<table border="1">
<tr><th><span data-ttu-id="1f372-290">입력 파티션</span><span class="sxs-lookup"><span data-stu-id="1f372-290">Input Partitions</span></span></th><th><span data-ttu-id="1f372-291">출력 파티션</span><span class="sxs-lookup"><span data-stu-id="1f372-291">Output Partitions</span></span></th><th><span data-ttu-id="1f372-292">스트리밍 단위</span><span class="sxs-lookup"><span data-stu-id="1f372-292">Streaming Units</span></span></th><th><span data-ttu-id="1f372-293">지속적인 처리량</span><span class="sxs-lookup"><span data-stu-id="1f372-293">Sustained Throughput</span></span>
</th></td>

<tr><td><span data-ttu-id="1f372-294">12</span><span class="sxs-lookup"><span data-stu-id="1f372-294">12</span></span></td>
<td><span data-ttu-id="1f372-295">12</span><span class="sxs-lookup"><span data-stu-id="1f372-295">12</span></span></td>
<td><span data-ttu-id="1f372-296">6</span><span class="sxs-lookup"><span data-stu-id="1f372-296">6</span></span></td>
<td><span data-ttu-id="1f372-297">4.06MB/초</span><span class="sxs-lookup"><span data-stu-id="1f372-297">4.06 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="1f372-298">12</span><span class="sxs-lookup"><span data-stu-id="1f372-298">12</span></span></td>
<td><span data-ttu-id="1f372-299">12</span><span class="sxs-lookup"><span data-stu-id="1f372-299">12</span></span></td>
<td><span data-ttu-id="1f372-300">12</span><span class="sxs-lookup"><span data-stu-id="1f372-300">12</span></span></td>
<td><span data-ttu-id="1f372-301">8.06 MB/초</span><span class="sxs-lookup"><span data-stu-id="1f372-301">8.06 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="1f372-302">48</span><span class="sxs-lookup"><span data-stu-id="1f372-302">48</span></span></td>
<td><span data-ttu-id="1f372-303">48</span><span class="sxs-lookup"><span data-stu-id="1f372-303">48</span></span></td>
<td><span data-ttu-id="1f372-304">48</span><span class="sxs-lookup"><span data-stu-id="1f372-304">48</span></span></td>
<td><span data-ttu-id="1f372-305">38.32 MB/초</span><span class="sxs-lookup"><span data-stu-id="1f372-305">38.32 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="1f372-306">192</span><span class="sxs-lookup"><span data-stu-id="1f372-306">192</span></span></td>
<td><span data-ttu-id="1f372-307">192</span><span class="sxs-lookup"><span data-stu-id="1f372-307">192</span></span></td>
<td><span data-ttu-id="1f372-308">192</span><span class="sxs-lookup"><span data-stu-id="1f372-308">192</span></span></td>
<td><span data-ttu-id="1f372-309">172.67 MB/초</span><span class="sxs-lookup"><span data-stu-id="1f372-309">172.67 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="1f372-310">480</span><span class="sxs-lookup"><span data-stu-id="1f372-310">480</span></span></td>
<td><span data-ttu-id="1f372-311">480</span><span class="sxs-lookup"><span data-stu-id="1f372-311">480</span></span></td>
<td><span data-ttu-id="1f372-312">480</span><span class="sxs-lookup"><span data-stu-id="1f372-312">480</span></span></td>
<td><span data-ttu-id="1f372-313">454.27 MB/초</span><span class="sxs-lookup"><span data-stu-id="1f372-313">454.27 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="1f372-314">720</span><span class="sxs-lookup"><span data-stu-id="1f372-314">720</span></span></td>
<td><span data-ttu-id="1f372-315">720</span><span class="sxs-lookup"><span data-stu-id="1f372-315">720</span></span></td>
<td><span data-ttu-id="1f372-316">720</span><span class="sxs-lookup"><span data-stu-id="1f372-316">720</span></span></td>
<td><span data-ttu-id="1f372-317">609.69 MB/초</span><span class="sxs-lookup"><span data-stu-id="1f372-317">609.69 MB/s</span></span></td>
</tr>
</table>

<span data-ttu-id="1f372-318">다음 그래프는 SU와 처리량 간의 관계를 시각화한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1f372-318">And the following graph shows a visualization of the relationship between SUs and throughput.</span></span>

![img.stream.analytics.perfgraph][img.stream.analytics.perfgraph]

## <a name="get-help"></a><span data-ttu-id="1f372-320">도움말 보기</span><span class="sxs-lookup"><span data-stu-id="1f372-320">Get help</span></span>
<span data-ttu-id="1f372-321">추가 지원이 필요한 경우 [Azure Stream Analytics 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1f372-321">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1f372-322">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1f372-322">Next steps</span></span>
* [<span data-ttu-id="1f372-323">Azure Stream Analytics 소개</span><span class="sxs-lookup"><span data-stu-id="1f372-323">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="1f372-324">Azure Stream Analytics 사용 시작</span><span class="sxs-lookup"><span data-stu-id="1f372-324">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="1f372-325">Azure Stream Analytics 쿼리 언어 참조</span><span class="sxs-lookup"><span data-stu-id="1f372-325">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="1f372-326">Azure Stream Analytics 관리 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="1f372-326">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

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


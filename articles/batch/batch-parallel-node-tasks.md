---
title: "병렬 toouse의 aaaRun 작업 컴퓨터 리소스를 효율적으로-Azure 일괄 처리 | Microsoft Docs"
description: "Azure 배치 풀의 각 노드에서 동시 작업을 실행하고 더 적은 수의 계산 노드를 사용하여 효율성은 높이고 비용은 낮춥니다."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 538a067c-1f6e-44eb-a92b-8d51c33d3e1a
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 05df4b7d8e0bc595168a97faa231b7c90fe81980
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="run-tasks-concurrently-toomaximize-usage-of-batch-compute-nodes"></a><span data-ttu-id="5e7dc-103">일괄 처리 계산 노드 toomaximize 사용 작업을 동시에 실행</span><span class="sxs-lookup"><span data-stu-id="5e7dc-103">Run tasks concurrently toomaximize usage of Batch compute nodes</span></span> 

<span data-ttu-id="5e7dc-104">Azure 배치 풀의 각 계산 노드에서 동시에 둘 이상의 작업을 실행 하 여 hello 풀에 있는 노드의 더 적은 수의 리소스 사용을 최대화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e7dc-104">By running more than one task simultaneously on each compute node in your Azure Batch pool, you can maximize resource usage on a smaller number of nodes in hello pool.</span></span> <span data-ttu-id="5e7dc-105">일부 워크로드의 경우, 작업 시간이 짧아지고 비용이 낮아질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e7dc-105">For some workloads, this can result in shorter job times and lower cost.</span></span>

<span data-ttu-id="5e7dc-106">을 일부 시나리오에서 모든 노드의 리소스 tooa 단일 작업의 전용 제대로 활용 하는 동안 여러 가지 상황에서 여러 작업 tooshare 리소스만 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5e7dc-106">While some scenarios benefit from dedicating all of a node's resources tooa single task, several situations benefit from allowing multiple tasks tooshare those resources:</span></span>

* <span data-ttu-id="5e7dc-107">**데이터 전송 최소화** 경우 작업은 수 tooshare 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="5e7dc-107">**Minimizing data transfer** when tasks are able tooshare data.</span></span> <span data-ttu-id="5e7dc-108">이 시나리오에서는 크게 절약할 수 있습니다는 데이터 전송 비용이 공유 데이터 tooa 더 적은 수의 노드를 복사 하 여 각 노드에서 동시에 작업을 실행 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e7dc-108">In this scenario, you can dramatically reduce data transfer charges by copying shared data tooa smaller number of nodes and executing tasks in parallel on each node.</span></span> <span data-ttu-id="5e7dc-109">특히 hello 데이터 toobe 복사한 tooeach 노드 지리적 지역 간의 전송 해야 하는 경우이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e7dc-109">This especially applies if hello data toobe copied tooeach node must be transferred between geographic regions.</span></span>
* <span data-ttu-id="5e7dc-110">**메모리 사용 최대화** - 태스크에 많은 양의 메모리가 필요하지만 단기간에만 그리고 실행 중에는 가변 시간에 메모리 사용량을 최대화합니다.</span><span class="sxs-lookup"><span data-stu-id="5e7dc-110">**Maximizing memory usage** when tasks require a large amount of memory, but only during short periods of time, and at variable times during execution.</span></span> <span data-ttu-id="5e7dc-111">더 큰 하지만 적은 사용, 계산 노드를 더 많은 메모리 tooefficiently 이러한 급증을 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e7dc-111">You can employ fewer, but larger, compute nodes with more memory tooefficiently handle such spikes.</span></span> <span data-ttu-id="5e7dc-112">이러한 노드는 각 노드에 대해 병렬로 실행 하는 여러 작업이 있을 수 있지만 각 작업은 서로 다른 시간에 hello 노드 매우 많은 메모리를 활용 하기 위해.</span><span class="sxs-lookup"><span data-stu-id="5e7dc-112">These nodes would have multiple tasks running in parallel on each node, but each task would take advantage of hello nodes' plentiful memory at different times.</span></span>
* <span data-ttu-id="5e7dc-113">**노드 숫자 제한 완화** .</span><span class="sxs-lookup"><span data-stu-id="5e7dc-113">**Mitigating node number limits** when inter-node communication is required within a pool.</span></span> <span data-ttu-id="5e7dc-114">현재 노드 간 통신을 위해 구성 된 풀 제한 too50 계산 노드는.</span><span class="sxs-lookup"><span data-stu-id="5e7dc-114">Currently, pools configured for inter-node communication are limited too50 compute nodes.</span></span> <span data-ttu-id="5e7dc-115">이러한 풀의 각 노드는 병렬로 수 tooexecute 작업, 작업 수를 더 동시에 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e7dc-115">If each node in such a pool is able tooexecute tasks in parallel, a greater number of tasks can be executed simultaneously.</span></span>
* <span data-ttu-id="5e7dc-116">**온-프레미스 계산 클러스터를 복제**, 먼저 이동 하는 경우 계산 환경 tooAzure 등입니다.</span><span class="sxs-lookup"><span data-stu-id="5e7dc-116">**Replicating an on-premises compute cluster**, such as when you first move a compute environment tooAzure.</span></span> <span data-ttu-id="5e7dc-117">Hello 최대 수를 늘릴 수 계산 노드에 당 여러 작업을 실행 하는 현재 온-프레미스 솔루션의 노드 작업 toomore 밀접 하 게 해당 구성을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e7dc-117">If your current on-premises solution executes multiple tasks per compute node, you can increase hello maximum number of node tasks toomore closely mirror that configuration.</span></span>

## <a name="example-scenario"></a><span data-ttu-id="5e7dc-118">예제 시나리오 </span><span class="sxs-lookup"><span data-stu-id="5e7dc-118">Example scenario</span></span>
<span data-ttu-id="5e7dc-119">예제 tooillustrate로 hello 병렬 작업 실행의 이점, 가정해 작업 응용 프로그램에서 CPU 및 메모리 요구 사항이 되도록 [표준\_D1](../cloud-services/cloud-services-sizes-specs.md) 노드는 충분 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e7dc-119">As an example tooillustrate hello benefits of parallel task execution, let's say that your task application has CPU and memory requirements such that [Standard\_D1](../cloud-services/cloud-services-sizes-specs.md) nodes are sufficient.</span></span> <span data-ttu-id="5e7dc-120">되지만 이러한 노드 중 1, 000 필요한 hello 시간에서 toofinish hello 작업 순서에서에서 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e7dc-120">But, in order toofinish hello job in hello required time, 1,000 of these nodes are needed.</span></span>

<span data-ttu-id="5e7dc-121">1개 CPU 코어가 있는 Standard\_D1 노드를 사용하는 대신 각각 16개 코어가 있는 [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) 노드를 사용하여 병렬 태스크 실행을 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e7dc-121">Instead of using Standard\_D1 nodes that have 1 CPU core, you could use [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) nodes that have 16 cores each, and enable parallel task execution.</span></span> <span data-ttu-id="5e7dc-122">따라서 사용되는 *노드 수가 1/16로 줄기 때문에* 필요한 노드 수는 1000개가 아니라 63개입니다.</span><span class="sxs-lookup"><span data-stu-id="5e7dc-122">Therefore, *16 times fewer nodes* could be used--instead of 1,000 nodes, only 63 would be required.</span></span> <span data-ttu-id="5e7dc-123">또한 대형 응용 프로그램 파일이 나 참조 데이터 각 노드에 대해 필요한 경우 작업 기간 및 효율성은 다시 향상 hello 데이터는 16 개의 노드로 구성 복사한 tooonly 이므로.</span><span class="sxs-lookup"><span data-stu-id="5e7dc-123">Additionally, if large application files or reference data are required for each node, job duration and efficiency are again improved since hello data is copied tooonly 16 nodes.</span></span>

## <a name="enable-parallel-task-execution"></a><span data-ttu-id="5e7dc-124">병렬 작업 실행 사용</span><span class="sxs-lookup"><span data-stu-id="5e7dc-124">Enable parallel task execution</span></span>
<span data-ttu-id="5e7dc-125">Hello 풀 수준에서 병렬 작업 실행에 대 한 계산 노드를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5e7dc-125">You configure compute nodes for parallel task execution at hello pool level.</span></span> <span data-ttu-id="5e7dc-126">Hello 일괄 처리.NET 라이브러리를 사용 하 여 hello 설정할 [CloudPool.MaxTasksPerComputeNode] [ maxtasks_net] 풀을 만들 때 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="5e7dc-126">With hello Batch .NET library, set hello [CloudPool.MaxTasksPerComputeNode][maxtasks_net] property when you create a pool.</span></span> <span data-ttu-id="5e7dc-127">Hello 배치 REST API를 사용 하는 경우 설정 hello [maxTasksPerNode] [ rest_addpool] 풀을 만드는 동안 hello 요청 본문의 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="5e7dc-127">If you are using hello Batch REST API, set hello [maxTasksPerNode][rest_addpool] element in hello request body during pool creation.</span></span>

<span data-ttu-id="5e7dc-128">Azure 배치 tooset toofour 배 (4 x) hello 노드 코어 수가를 노드당 최대 작업 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e7dc-128">Azure Batch allows you tooset maximum tasks per node up toofour times (4x) hello number of node cores.</span></span> <span data-ttu-id="5e7dc-129">예를 들어 경우 hello으로 풀이 구성 되어 (4 코어), "Large" 크기의 노드 다음 `maxTasksPerNode` too16 설정 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e7dc-129">For example, if hello pool is configured with nodes of size "Large" (four cores), then `maxTasksPerNode` may be set too16.</span></span> <span data-ttu-id="5e7dc-130">Hello hello 노드 크기를 각 코어 수에 대 한 세부 정보를 참조 하십시오. [클라우드 서비스에 대 한 크기](../cloud-services/cloud-services-sizes-specs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5e7dc-130">For details on hello number of cores for each of hello node sizes, see [Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md).</span></span> <span data-ttu-id="5e7dc-131">서비스 제한에 대 한 자세한 내용은 참조 하십시오. [할당량과 hello Azure 배치 서비스에 대 한 제한을](batch-quota-limit.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5e7dc-131">For more information on service limits, see [Quotas and limits for hello Azure Batch service](batch-quota-limit.md).</span></span>

> [!TIP]
> <span data-ttu-id="5e7dc-132">계정 hello에 있는지 tootake 수 `maxTasksPerNode` 를 생성할 때 값는 [자동 크기 조정 수식을] [ enable_autoscaling] 풀에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e7dc-132">Be sure tootake into account hello `maxTasksPerNode` value when you construct an [autoscale formula][enable_autoscaling] for your pool.</span></span> <span data-ttu-id="5e7dc-133">예를 들어, `$RunningTasks` 를 평가하는 수식은 노드당 작업 수 증가에 크게 영향을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e7dc-133">For example, a formula that evaluates `$RunningTasks` could be dramatically affected by an increase in tasks per node.</span></span> <span data-ttu-id="5e7dc-134">자세한 내용은 [Azure Batch 풀에서 자동으로 계산 노드 크기 조정](batch-automatic-scaling.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5e7dc-134">See [Automatically scale compute nodes in an Azure Batch pool](batch-automatic-scaling.md) for more information.</span></span>
>
>

## <a name="distribution-of-tasks"></a><span data-ttu-id="5e7dc-135">작업 배분</span><span class="sxs-lookup"><span data-stu-id="5e7dc-135">Distribution of tasks</span></span>
<span data-ttu-id="5e7dc-136">Hello 계산 노드는 풀의 작업을 동시에 실행할 수 때 중요 한 toospecify 원하는 hello 작업 toobe hello 풀의 hello 노드에 분산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e7dc-136">When hello compute nodes in a pool can execute tasks concurrently, it's important toospecify how you want hello tasks toobe distributed across hello nodes in hello pool.</span></span>

<span data-ttu-id="5e7dc-137">Hello를 사용 하 여 [CloudPool.TaskSchedulingPolicy] [ task_schedule] 속성 ("확산") hello 풀의 모든 노드에서 태스크를 균등 하 게 할당할 수 있도록을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e7dc-137">By using hello [CloudPool.TaskSchedulingPolicy][task_schedule] property, you can specify that tasks should be assigned evenly across all nodes in hello pool ("spreading").</span></span> <span data-ttu-id="5e7dc-138">또는 가능한 한 많은 작업 할당 해야 tooeach 노드 작업 tooanother 노드 ("패키지") hello 풀에 할당 되기 전에 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e7dc-138">Or you can specify that as many tasks as possible should be assigned tooeach node before tasks are assigned tooanother node in hello pool ("packing").</span></span>

<span data-ttu-id="5e7dc-139">이 기능은 유용 방법의 예를 들어 hello 풀 고려 [표준\_D14](../cloud-services/cloud-services-sizes-specs.md) (위의 hello 예제)에 구성 된 노드는 [CloudPool.MaxTasksPerComputeNode] [ maxtasks_net] 16의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="5e7dc-139">As an example of how this feature is valuable, consider hello pool of [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) nodes (in hello example above) that is configured with a [CloudPool.MaxTasksPerComputeNode][maxtasks_net] value of 16.</span></span> <span data-ttu-id="5e7dc-140">경우 hello [CloudPool.TaskSchedulingPolicy] [ task_schedule] 구성 된 한 [ComputeNodeFillType] [ fill_type] 의 *팩*, 각 노드의 모든 16 개 코어의 사용을 최대화 하 고 허용 합니다는 [자동 크기 조정 풀](batch-automatic-scaling.md) tooprune hello 풀 (할당 된 작업 없이 노드)에서 사용 되지 않는 노드.</span><span class="sxs-lookup"><span data-stu-id="5e7dc-140">If hello [CloudPool.TaskSchedulingPolicy][task_schedule] is configured with a [ComputeNodeFillType][fill_type] of *Pack*, it would maximize usage of all 16 cores of each node and allow an [autoscaling pool](batch-automatic-scaling.md) tooprune unused nodes from hello pool (nodes without any tasks assigned).</span></span> <span data-ttu-id="5e7dc-141">리소스 사용량을 최소화하고 비용을 절감합니다.</span><span class="sxs-lookup"><span data-stu-id="5e7dc-141">This minimizes resource usage and saves money.</span></span>

## <a name="batch-net-example"></a><span data-ttu-id="5e7dc-142">Batch .NET 예</span><span class="sxs-lookup"><span data-stu-id="5e7dc-142">Batch .NET example</span></span>
<span data-ttu-id="5e7dc-143">이 [일괄 처리.NET] [ api_net] API 코드 조각을 요청 toocreate 노드당 4 개 작업의 최대 4 개의 큰 노드를 포함 하는 그룹을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e7dc-143">This [Batch .NET][api_net] API code snippet shows a request toocreate a pool that contains four large nodes with a maximum of four tasks per node.</span></span> <span data-ttu-id="5e7dc-144">예약 작업 이전 tooassigning 작업 tooanother 노드 hello 풀의 각 노드에 채울 정책 작업을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e7dc-144">It specifies a task scheduling policy that will fill each node with tasks prior tooassigning tasks tooanother node in hello pool.</span></span> <span data-ttu-id="5e7dc-145">풀 hello 일괄 처리.NET API를 사용 하 여 추가 하는 방법에 대 한 자세한 내용은 참조 하십시오. [BatchClient.PoolOperations.CreatePool][poolcreate_net]합니다.</span><span class="sxs-lookup"><span data-stu-id="5e7dc-145">For more information on adding pools by using hello Batch .NET API, see [BatchClient.PoolOperations.CreatePool][poolcreate_net].</span></span>

```csharp
CloudPool pool =
    batchClient.PoolOperations.CreatePool(
        poolId: "mypool",
        targetDedicatedComputeNodes: 4
        virtualMachineSize: "large",
        cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));

pool.MaxTasksPerComputeNode = 4;
pool.TaskSchedulingPolicy = new TaskSchedulingPolicy(ComputeNodeFillType.Pack);
pool.Commit();
```

## <a name="batch-rest-example"></a><span data-ttu-id="5e7dc-146">Batch REST 예</span><span class="sxs-lookup"><span data-stu-id="5e7dc-146">Batch REST example</span></span>
<span data-ttu-id="5e7dc-147">이 [배치 REST] [ api_rest] API 조각 요청 toocreate 노드당 4 개 작업의 최대 두 개의 큰 노드를 포함 하는 그룹을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e7dc-147">This [Batch REST][api_rest] API snippet shows a request toocreate a pool that contains two large nodes with a maximum of four tasks per node.</span></span> <span data-ttu-id="5e7dc-148">풀 hello REST API를 사용 하 여 추가 하는 방법에 대 한 자세한 내용은 참조 하십시오. [풀 tooan 계정 추가][rest_addpool]합니다.</span><span class="sxs-lookup"><span data-stu-id="5e7dc-148">For more information on adding pools by using hello REST API, see [Add a pool tooan account][rest_addpool].</span></span>

```json
{
  "odata.metadata":"https://myaccount.myregion.batch.azure.com/$metadata#pools/@Element",
  "id":"mypool",
  "vmSize":"large",
  "cloudServiceConfiguration": {
    "osFamily":"4",
    "targetOSVersion":"*",
  }
  "targetDedicatedComputeNodes":2,
  "maxTasksPerNode":4,
  "enableInterNodeCommunication":true,
}
```

> [!NOTE]
> <span data-ttu-id="5e7dc-149">Hello를 설정할 수 있습니다 `maxTasksPerNode` 요소 및 [MaxTasksPerComputeNode] [ maxtasks_net] 풀 만들 때에만 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="5e7dc-149">You can set hello `maxTasksPerNode` element and [MaxTasksPerComputeNode][maxtasks_net] property only at pool creation time.</span></span> <span data-ttu-id="5e7dc-150">풀이 이미 만들어진 후에는 수정될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5e7dc-150">They cannot be modified after a pool has already been created.</span></span>
>
>

## <a name="code-sample"></a><span data-ttu-id="5e7dc-151">코드 샘플</span><span class="sxs-lookup"><span data-stu-id="5e7dc-151">Code sample</span></span>
<span data-ttu-id="5e7dc-152">hello [ParallelNodeTasks] [ parallel_tasks_sample] GitHub에서 프로젝트 hello hello 사용을 보여 줍니다. [CloudPool.MaxTasksPerComputeNode] [ maxtasks_net] 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="5e7dc-152">hello [ParallelNodeTasks][parallel_tasks_sample] project on GitHub illustrates hello use of hello [CloudPool.MaxTasksPerComputeNode][maxtasks_net] property.</span></span>

<span data-ttu-id="5e7dc-153">이 C# 콘솔 응용 프로그램 사용 hello [일괄 처리.NET] [ api_net] 라이브러리 toocreate 하나 이상의 풀 계산 노드.</span><span class="sxs-lookup"><span data-stu-id="5e7dc-153">This C# console application uses hello [Batch .NET][api_net] library toocreate a pool with one or more compute nodes.</span></span> <span data-ttu-id="5e7dc-154">이러한 노드 toosimulate 가변 부하에서 구성 가능한 다양 한 태스크를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5e7dc-154">It executes a configurable number of tasks on those nodes toosimulate variable load.</span></span> <span data-ttu-id="5e7dc-155">출력 hello 응용 프로그램에서 각 작업을 실행 하는 노드를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e7dc-155">Output from hello application specifies which nodes executed each task.</span></span> <span data-ttu-id="5e7dc-156">또한 hello 응용 프로그램 hello 작업 매개 변수 및 기간에 대 한 요약을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5e7dc-156">hello application also provides a summary of hello job parameters and duration.</span></span> <span data-ttu-id="5e7dc-157">hello 샘플 응용 프로그램의 두 가지 다른 실행에서 hello 출력의 hello 요약 부분 아래에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="5e7dc-157">hello summary portion of hello output from two different runs of hello sample application appears below.</span></span>

```
Nodes: 1
Node size: large
Max tasks per node: 1
Tasks: 32
Duration: 00:30:01.4638023
```

<span data-ttu-id="5e7dc-158">hello 샘플 응용 프로그램의 첫 번째 실행 hello 표시 하는 hello 그룹 및 hello 기본 설정인 노드당 한 작업의 단일 노드와 상호 hello 작업 기간 (30 분) 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e7dc-158">hello first execution of hello sample application shows that with a single node in hello pool and hello default setting of one task per node, hello job duration is over 30 minutes.</span></span>

```
Nodes: 1
Node size: large
Max tasks per node: 4
Tasks: 32
Duration: 00:08:48.2423500
```

<span data-ttu-id="5e7dc-159">hello 실행 hello 샘플 프로그램의 중요 한 작업 기간을 감소 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e7dc-159">hello second run of hello sample shows a significant decrease in job duration.</span></span> <span data-ttu-id="5e7dc-160">즉, hello 풀 거의 hello 시간의 사분기에 병렬 작업 실행 toocomplete hello 작업에 대 한 허용 노드당 4 개 작업으로 구성 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="5e7dc-160">This is because hello pool was configured with four tasks per node, which allows for parallel task execution toocomplete hello job in nearly a quarter of hello time.</span></span>

> [!NOTE]
> <span data-ttu-id="5e7dc-161">위의 hello 요약에서 작업 기간 hello 풀 생성 시간을 포함 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="5e7dc-161">hello job durations in hello summaries above do not include pool creation time.</span></span> <span data-ttu-id="5e7dc-162">계산 노드를 모두 hello에 제출 된 toopreviously 만든 풀이 위의 hello 작업의 각 *Idle* 제출 시 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="5e7dc-162">Each of hello jobs above was submitted toopreviously created pools whose compute nodes were in hello *Idle* state at submission time.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="5e7dc-163">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5e7dc-163">Next steps</span></span>
### <a name="batch-explorer-heat-map"></a><span data-ttu-id="5e7dc-164">배치 탐색기 열 지도</span><span class="sxs-lookup"><span data-stu-id="5e7dc-164">Batch Explorer Heat Map</span></span>
<span data-ttu-id="5e7dc-165">hello [Azure 일괄 처리 탐색기][batch_explorer], hello Azure 일괄 처리 중 하나 [샘플 응용 프로그램][github_samples]를 포함 한 *열지도* 태스크 실행의 시각화를 제공 하는 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="5e7dc-165">hello [Azure Batch Explorer][batch_explorer], one of hello Azure Batch [sample applications][github_samples], contains a *Heat Map* feature that provides visualization of task execution.</span></span> <span data-ttu-id="5e7dc-166">Hello를 실행 하는 경우 [ParallelTasks] [ parallel_tasks_sample] 샘플 응용 프로그램에서는 hello 열 지도 기능 tooeasily hello 각 노드에서 병렬 작업 실행을 시각화 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e7dc-166">When you're executing hello [ParallelTasks][parallel_tasks_sample] sample application, you can use hello Heat Map feature tooeasily visualize hello execution of parallel tasks on each node.</span></span>

![배치 탐색기 열 지도][1]

<span data-ttu-id="5e7dc-168">*현재 4가지 작업을 실행하는 각 노드와 4개 노드의 풀을 보여 주는 배치 탐색기 열 지도*</span><span class="sxs-lookup"><span data-stu-id="5e7dc-168">*Batch Explorer Heat Map showing a pool of four nodes, with each node currently executing four tasks*</span></span>

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[batch_explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[cloudpool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[enable_autoscaling]: https://msdn.microsoft.com/library/azure/dn820173.aspx
[fill_type]: https://msdn.microsoft.com/library/microsoft.azure.batch.common.computenodefilltype.aspx
[github_samples]: https://github.com/Azure/azure-batch-samples
[maxtasks_net]: http://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.maxtaskspercomputenode.aspx
[rest_addpool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
[parallel_tasks_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/ParallelTasks
[poolcreate_net]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.createpool.aspx
[task_schedule]: https://msdn.microsoft.com/library/microsoft.azure.batch.cloudpool.taskschedulingpolicy.aspx

[1]: ./media/batch-parallel-node-tasks\heat_map.png

---
title: "병렬로 태스크를 실행하여 효율적으로 계산 리소스 사용 - Azure Batch | Microsoft Docs"
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
ms.openlocfilehash: 6903552d907a1ddb21d3b678e2d224b4b5e35b77
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="run-tasks-concurrently-to-maximize-usage-of-batch-compute-nodes"></a><span data-ttu-id="6b552-103">동시에 태스크를 실행하여 Batch 계산 노드의 사용량 극대화</span><span class="sxs-lookup"><span data-stu-id="6b552-103">Run tasks concurrently to maximize usage of Batch compute nodes</span></span> 

<span data-ttu-id="6b552-104">Azure 배치 풀의 각 계산 노드에서 동시에 둘 이상의 작업을 실행하여 풀의 더 작은 수의 노드에서 리소스 사용을 최대화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b552-104">By running more than one task simultaneously on each compute node in your Azure Batch pool, you can maximize resource usage on a smaller number of nodes in the pool.</span></span> <span data-ttu-id="6b552-105">일부 워크로드의 경우, 작업 시간이 짧아지고 비용이 낮아질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b552-105">For some workloads, this can result in shorter job times and lower cost.</span></span>

<span data-ttu-id="6b552-106">일부 시나리오에서는 노드의 모든 리소스를 단일 태스크에 전적으로 사용할 수 있지만 몇 가지 상황에서는 여러 태스크가 이러한 리소스를 공유할 수 있는 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b552-106">While some scenarios benefit from dedicating all of a node's resources to a single task, several situations benefit from allowing multiple tasks to share those resources:</span></span>

* <span data-ttu-id="6b552-107">**데이터 전송을 최소화** .</span><span class="sxs-lookup"><span data-stu-id="6b552-107">**Minimizing data transfer** when tasks are able to share data.</span></span> <span data-ttu-id="6b552-108">이 시나리오에서는 적은 수의 노드에 공유 데이터를 복사하고 각 노드에 병렬로 작업을 실행하여 데이터 전송 요금을 크게 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b552-108">In this scenario, you can dramatically reduce data transfer charges by copying shared data to a smaller number of nodes and executing tasks in parallel on each node.</span></span> <span data-ttu-id="6b552-109">특히 각 노드로 복사할 데이터를 지역 간에 전송해야 하는 경우 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b552-109">This especially applies if the data to be copied to each node must be transferred between geographic regions.</span></span>
* <span data-ttu-id="6b552-110">**메모리 사용 최대화** - 태스크에 많은 양의 메모리가 필요하지만 단기간에만 그리고 실행 중에는 가변 시간에 메모리 사용량을 최대화합니다.</span><span class="sxs-lookup"><span data-stu-id="6b552-110">**Maximizing memory usage** when tasks require a large amount of memory, but only during short periods of time, and at variable times during execution.</span></span> <span data-ttu-id="6b552-111">이러한 급증을 효율적으로 처리하기 위해 많은 메모리를 가진 적지만 크기가 큰 계산 노드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b552-111">You can employ fewer, but larger, compute nodes with more memory to efficiently handle such spikes.</span></span> <span data-ttu-id="6b552-112">이러한 노드에는 각 노드에서 병렬로 실행되는 여러 작업이 있지만 각 작업은 시간을 두고 노드의 풍부한 메모리를 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="6b552-112">These nodes would have multiple tasks running in parallel on each node, but each task would take advantage of the nodes' plentiful memory at different times.</span></span>
* <span data-ttu-id="6b552-113">**노드 숫자 제한 완화** .</span><span class="sxs-lookup"><span data-stu-id="6b552-113">**Mitigating node number limits** when inter-node communication is required within a pool.</span></span> <span data-ttu-id="6b552-114">현재 노드 간 통신에 대해 구성된 풀은 계산 노드가 50개로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b552-114">Currently, pools configured for inter-node communication are limited to 50 compute nodes.</span></span> <span data-ttu-id="6b552-115">이러한 풀의 각 노드가 병렬로 태스크를 실행할 수 있으면 더 많은 수의 태스크를 동시에 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b552-115">If each node in such a pool is able to execute tasks in parallel, a greater number of tasks can be executed simultaneously.</span></span>
* <span data-ttu-id="6b552-116">최초로 컴퓨팅 환경을 Azure로 이동하는 경우 등 **온-프레미스 계산 클러스터 복제**.</span><span class="sxs-lookup"><span data-stu-id="6b552-116">**Replicating an on-premises compute cluster**, such as when you first move a compute environment to Azure.</span></span> <span data-ttu-id="6b552-117">현재 온-프레미스 솔루션이 계산 노드 당 여러 태스크를 실행하는 경우 최대 노드 태스크 수를 늘려 해당 구성을 보다 자세히 미러링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b552-117">If your current on-premises solution executes multiple tasks per compute node, you can increase the maximum number of node tasks to more closely mirror that configuration.</span></span>

## <a name="example-scenario"></a><span data-ttu-id="6b552-118">예제 시나리오 </span><span class="sxs-lookup"><span data-stu-id="6b552-118">Example scenario</span></span>
<span data-ttu-id="6b552-119">병렬 태스크 실행의 이점을 보여 주는 한 예로서, 태스크 응용 프로그램에 [Standard\_D1](../cloud-services/cloud-services-sizes-specs.md) 노드로 충분한 CPU 및 메모리 요구 사항이 있다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6b552-119">As an example to illustrate the benefits of parallel task execution, let's say that your task application has CPU and memory requirements such that [Standard\_D1](../cloud-services/cloud-services-sizes-specs.md) nodes are sufficient.</span></span> <span data-ttu-id="6b552-120">하지만 주어진 시간에 작업을 완료하기 위해 이러한 노드가 1,000개 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6b552-120">But, in order to finish the job in the required time, 1,000 of these nodes are needed.</span></span>

<span data-ttu-id="6b552-121">1개 CPU 코어가 있는 Standard\_D1 노드를 사용하는 대신 각각 16개 코어가 있는 [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) 노드를 사용하여 병렬 태스크 실행을 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b552-121">Instead of using Standard\_D1 nodes that have 1 CPU core, you could use [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) nodes that have 16 cores each, and enable parallel task execution.</span></span> <span data-ttu-id="6b552-122">따라서 사용되는 *노드 수가 1/16로 줄기 때문에* 필요한 노드 수는 1000개가 아니라 63개입니다.</span><span class="sxs-lookup"><span data-stu-id="6b552-122">Therefore, *16 times fewer nodes* could be used--instead of 1,000 nodes, only 63 would be required.</span></span> <span data-ttu-id="6b552-123">또한 대규모 응용 프로그램 파일 또는 참조 데이터가 각 노드에 대해 필요한 경우 데이터는 16개의 노드로 복사되기 때문에 작업 기간 및 효율성은 다시 개선됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b552-123">Additionally, if large application files or reference data are required for each node, job duration and efficiency are again improved since the data is copied to only 16 nodes.</span></span>

## <a name="enable-parallel-task-execution"></a><span data-ttu-id="6b552-124">병렬 작업 실행 사용</span><span class="sxs-lookup"><span data-stu-id="6b552-124">Enable parallel task execution</span></span>
<span data-ttu-id="6b552-125">풀 수준에서 병렬 작업 실행을 위해 계산 노드를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="6b552-125">You configure compute nodes for parallel task execution at the pool level.</span></span> <span data-ttu-id="6b552-126">Batch .NET 라이브러리를 사용하여 풀을 만들 때 [CloudPool.MaxTasksPerComputeNode][maxtasks_net] 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6b552-126">With the Batch .NET library, set the [CloudPool.MaxTasksPerComputeNode][maxtasks_net] property when you create a pool.</span></span> <span data-ttu-id="6b552-127">Batch REST API를 사용하는 경우 풀을 만들 때 요청 본문에 [maxTasksPerNode][rest_addpool] 요소를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6b552-127">If you are using the Batch REST API, set the [maxTasksPerNode][rest_addpool] element in the request body during pool creation.</span></span>

<span data-ttu-id="6b552-128">Azure 배치를 사용하면 노드 코어의 최대 4배수의 노드 마다 최대 작업을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b552-128">Azure Batch allows you to set maximum tasks per node up to four times (4x) the number of node cores.</span></span> <span data-ttu-id="6b552-129">예를 들어, 풀이 노드 크기 “Large”로 구성되었다면(4코어) `maxTasksPerNode` 는 16으로 설정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b552-129">For example, if the pool is configured with nodes of size "Large" (four cores), then `maxTasksPerNode` may be set to 16.</span></span> <span data-ttu-id="6b552-130">각 노드 크기에 대한 코어 수에 대한 자세한 내용은 [클라우드 서비스에 적합한 크기](../cloud-services/cloud-services-sizes-specs.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6b552-130">For details on the number of cores for each of the node sizes, see [Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md).</span></span> <span data-ttu-id="6b552-131">서비스 제한에 대한 자세한 내용은 [Azure 배치 서비스에 대한 할당량 및 제한](batch-quota-limit.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6b552-131">For more information on service limits, see [Quotas and limits for the Azure Batch service](batch-quota-limit.md).</span></span>

> [!TIP]
> <span data-ttu-id="6b552-132">풀에 [자동 크기 조정 수식][enable_autoscaling]을 구성할 때는 `maxTasksPerNode` 값을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b552-132">Be sure to take into account the `maxTasksPerNode` value when you construct an [autoscale formula][enable_autoscaling] for your pool.</span></span> <span data-ttu-id="6b552-133">예를 들어, `$RunningTasks` 를 평가하는 수식은 노드당 작업 수 증가에 크게 영향을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b552-133">For example, a formula that evaluates `$RunningTasks` could be dramatically affected by an increase in tasks per node.</span></span> <span data-ttu-id="6b552-134">자세한 내용은 [Azure Batch 풀에서 자동으로 계산 노드 크기 조정](batch-automatic-scaling.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6b552-134">See [Automatically scale compute nodes in an Azure Batch pool](batch-automatic-scaling.md) for more information.</span></span>
>
>

## <a name="distribution-of-tasks"></a><span data-ttu-id="6b552-135">작업 배분</span><span class="sxs-lookup"><span data-stu-id="6b552-135">Distribution of tasks</span></span>
<span data-ttu-id="6b552-136">풀 내의 계산 노드가 작업을 동시에 실행할 수 있는 경우 풀 내 노드에서 작업을 배분하려는 방법을 지정하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="6b552-136">When the compute nodes in a pool can execute tasks concurrently, it's important to specify how you want the tasks to be distributed across the nodes in the pool.</span></span>

<span data-ttu-id="6b552-137">[CloudPool.TaskSchedulingPolicy][task_schedule] 속성을 사용하여 풀의 모든 노드에서 작업을 균등하게 할당하도록 지정할 수 있습니다("확산").</span><span class="sxs-lookup"><span data-stu-id="6b552-137">By using the [CloudPool.TaskSchedulingPolicy][task_schedule] property, you can specify that tasks should be assigned evenly across all nodes in the pool ("spreading").</span></span> <span data-ttu-id="6b552-138">또는 작업이 풀의 다른 노드로 할당되기 전에 최대한 많은 작업이 각 노드에 할당되도록 지정할 수 있습니다.("압축")</span><span class="sxs-lookup"><span data-stu-id="6b552-138">Or you can specify that as many tasks as possible should be assigned to each node before tasks are assigned to another node in the pool ("packing").</span></span>

<span data-ttu-id="6b552-139">이 기능이 얼마나 중요한지 확인하기 위해 위의 예에서 [CloudPool.MaxTasksPerComputeNode][maxtasks_net] 값이 16으로 구성된 [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) 노드 풀을 고려해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6b552-139">As an example of how this feature is valuable, consider the pool of [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) nodes (in the example above) that is configured with a [CloudPool.MaxTasksPerComputeNode][maxtasks_net] value of 16.</span></span> <span data-ttu-id="6b552-140">[CloudPool.TaskSchedulingPolicy][task_schedule]가 *Pack*인 [ComputeNodeFillType][fill_type]으로 구성된 경우, 각 노드의 모든 16개 코어의 사용량을 최대화하며 [풀 자동 크기 조정](batch-automatic-scaling.md)을 통해 풀에서 사용되지 않는 노드(작업이 할당되지 않은 노드)를 솎아냅니다.</span><span class="sxs-lookup"><span data-stu-id="6b552-140">If the [CloudPool.TaskSchedulingPolicy][task_schedule] is configured with a [ComputeNodeFillType][fill_type] of *Pack*, it would maximize usage of all 16 cores of each node and allow an [autoscaling pool](batch-automatic-scaling.md) to prune unused nodes from the pool (nodes without any tasks assigned).</span></span> <span data-ttu-id="6b552-141">리소스 사용량을 최소화하고 비용을 절감합니다.</span><span class="sxs-lookup"><span data-stu-id="6b552-141">This minimizes resource usage and saves money.</span></span>

## <a name="batch-net-example"></a><span data-ttu-id="6b552-142">Batch .NET 예</span><span class="sxs-lookup"><span data-stu-id="6b552-142">Batch .NET example</span></span>
<span data-ttu-id="6b552-143">이 [Batch .NET][api_net] API 코드 조각은 노드 당 최대 4개의 작업이 있는 네 개의 대규모 노드를 포함하는 풀을 만드는 요청을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="6b552-143">This [Batch .NET][api_net] API code snippet shows a request to create a pool that contains four large nodes with a maximum of four tasks per node.</span></span> <span data-ttu-id="6b552-144">풀의 다른 노드로 작업을 할당하기 전에 각 노드를 채울 정책을 예약하는 작업을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6b552-144">It specifies a task scheduling policy that will fill each node with tasks prior to assigning tasks to another node in the pool.</span></span> <span data-ttu-id="6b552-145">Batch .NET API를 사용하여 풀을 추가하는 방법에 대한 자세한 내용은 [BatchClient.PoolOperations.CreatePool][poolcreate_net]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6b552-145">For more information on adding pools by using the Batch .NET API, see [BatchClient.PoolOperations.CreatePool][poolcreate_net].</span></span>

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

## <a name="batch-rest-example"></a><span data-ttu-id="6b552-146">Batch REST 예</span><span class="sxs-lookup"><span data-stu-id="6b552-146">Batch REST example</span></span>
<span data-ttu-id="6b552-147">이 [Batch REST][api_rest] API 코드 조각은 노드당 최대 4개의 작업이 있는 두 대규모 노드를 포함하는 풀을 만드는 요청을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="6b552-147">This [Batch REST][api_rest] API snippet shows a request to create a pool that contains two large nodes with a maximum of four tasks per node.</span></span> <span data-ttu-id="6b552-148">REST API를 사용하여 풀을 추가하는 방법에 대한 자세한 내용은 [계정에 풀 추가][rest_addpool]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6b552-148">For more information on adding pools by using the REST API, see [Add a pool to an account][rest_addpool].</span></span>

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
> <span data-ttu-id="6b552-149">풀을 만들 때만 `maxTasksPerNode` 요소 및 [MaxTasksPerComputeNode][maxtasks_net] 속성을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b552-149">You can set the `maxTasksPerNode` element and [MaxTasksPerComputeNode][maxtasks_net] property only at pool creation time.</span></span> <span data-ttu-id="6b552-150">풀이 이미 만들어진 후에는 수정될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6b552-150">They cannot be modified after a pool has already been created.</span></span>
>
>

## <a name="code-sample"></a><span data-ttu-id="6b552-151">코드 샘플</span><span class="sxs-lookup"><span data-stu-id="6b552-151">Code sample</span></span>
<span data-ttu-id="6b552-152">GitHub의 [ParallelNodeTasks][parallel_tasks_sample] 프로젝트는 [CloudPool.MaxTasksPerComputeNode][maxtasks_net] 속성의 사용을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6b552-152">The [ParallelNodeTasks][parallel_tasks_sample] project on GitHub illustrates the use of the [CloudPool.MaxTasksPerComputeNode][maxtasks_net] property.</span></span>

<span data-ttu-id="6b552-153">이 C# 콘솔 응용 프로그램은 [Batch .NET][api_net] 라이브러리를 사용하여 하나 이상의 계산 노드가 있는 풀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6b552-153">This C# console application uses the [Batch .NET][api_net] library to create a pool with one or more compute nodes.</span></span> <span data-ttu-id="6b552-154">해당 노드에서 구성 가능한 다양한 작업을 실행하여 변수 부하를 시뮬레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="6b552-154">It executes a configurable number of tasks on those nodes to simulate variable load.</span></span> <span data-ttu-id="6b552-155">응용 프로그램에서 출력은 각 작업을 실행하는 노드를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6b552-155">Output from the application specifies which nodes executed each task.</span></span> <span data-ttu-id="6b552-156">또한 응용 프로그램은 작업 매개 변수 및 기간의 요약을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6b552-156">The application also provides a summary of the job parameters and duration.</span></span> <span data-ttu-id="6b552-157">아래는 예제 응용 프로그램의 두 가지 다른 실행에서의 출력을 요약하는 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="6b552-157">The summary portion of the output from two different runs of the sample application appears below.</span></span>

```
Nodes: 1
Node size: large
Max tasks per node: 1
Tasks: 32
Duration: 00:30:01.4638023
```

<span data-ttu-id="6b552-158">샘플 응용 프로그램의 최초 실행에서는 풀 내 단일 노드 및 노드 당 작업의 기본값 설정을 보여주며 작업 길이는 30분이 넘습니다.</span><span class="sxs-lookup"><span data-stu-id="6b552-158">The first execution of the sample application shows that with a single node in the pool and the default setting of one task per node, the job duration is over 30 minutes.</span></span>

```
Nodes: 1
Node size: large
Max tasks per node: 4
Tasks: 32
Duration: 00:08:48.2423500
```

<span data-ttu-id="6b552-159">샘플의 두 번째 실행은 작업 기간에서 크게 감소합니다.</span><span class="sxs-lookup"><span data-stu-id="6b552-159">The second run of the sample shows a significant decrease in job duration.</span></span> <span data-ttu-id="6b552-160">풀이 노드 당 4개의 작업으로 구성되었기 때문에 이를 사용하면 병렬 작업 실행이 거의 1/4 시간에서 작업을 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b552-160">This is because the pool was configured with four tasks per node, which allows for parallel task execution to complete the job in nearly a quarter of the time.</span></span>

> [!NOTE]
> <span data-ttu-id="6b552-161">위 요약의 작업 기간에는 풀 생성 시간이 포함되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="6b552-161">The job durations in the summaries above do not include pool creation time.</span></span> <span data-ttu-id="6b552-162">위의 각 작업은 이전에 만든 풀에 제출되며, 제출 시점에 계산 노드는 *Idle* 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="6b552-162">Each of the jobs above was submitted to previously created pools whose compute nodes were in the *Idle* state at submission time.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="6b552-163">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6b552-163">Next steps</span></span>
### <a name="batch-explorer-heat-map"></a><span data-ttu-id="6b552-164">배치 탐색기 열 지도</span><span class="sxs-lookup"><span data-stu-id="6b552-164">Batch Explorer Heat Map</span></span>
<span data-ttu-id="6b552-165">Azure Batch [샘플 응용 프로그램][github_samples] 중 하나인 [Azure Batch Explorer][batch_explorer]에는 작업 실행을 시각화하는 *열 지도* 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b552-165">The [Azure Batch Explorer][batch_explorer], one of the Azure Batch [sample applications][github_samples], contains a *Heat Map* feature that provides visualization of task execution.</span></span> <span data-ttu-id="6b552-166">[ParallelTasks][parallel_tasks_sample] 샘플 응용 프로그램을 실행할 때 열 지도 기능을 사용하면 각 노드에서 병렬 작업의 실행을 쉽게 시각화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b552-166">When you're executing the [ParallelTasks][parallel_tasks_sample] sample application, you can use the Heat Map feature to easily visualize the execution of parallel tasks on each node.</span></span>

![배치 탐색기 열 지도][1]

<span data-ttu-id="6b552-168">*현재 4가지 작업을 실행하는 각 노드와 4개 노드의 풀을 보여 주는 배치 탐색기 열 지도*</span><span class="sxs-lookup"><span data-stu-id="6b552-168">*Batch Explorer Heat Map showing a pool of four nodes, with each node currently executing four tasks*</span></span>

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

---
title: "상태별로 작업을 계산하여 작업 진행 상태 모니터링 - Azure Batch | Microsoft Docs"
description: "작업에 대한 태스크 수를 계산하도록 Get Task Counts 연산을 호출하여 작업의 진행 상황을 모니터링합니다. 활성, 실행 중, 완료된 태스크 수는 물론, 성공 또는 성공한 태스크 수를 계산할 수 있습니다."
services: batch
author: tamram
manager: timlt
ms.service: batch
ms.topic: article
ms.date: 08/02/2017
ms.author: tamram
ms.openlocfilehash: ceff59d7063b60a1344a47489d3d73e0e8ee07df
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="count-tasks-by-state-to-monitor-a-jobs-progress-preview"></a><span data-ttu-id="99078-104">상태별로 태스크 수를 계산하여 작업의 진행 상황 모니터링(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="99078-104">Count tasks by state to monitor a job's progress (Preview)</span></span>

<span data-ttu-id="99078-105">Azure Batch는 태스크 실행 시 작업의 진행 상황을 모니터링하는 효율적인 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="99078-105">Azure Batch provides an efficient way to monitor the progress of a job as it runs its tasks.</span></span> <span data-ttu-id="99078-106">[Get Task Counts][rest_get_task_counts] 연산을 호출하여 활성, 실행 중 또는 완료된 상태의 태스크 수와 성공 또는 실패한 태스크 수를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99078-106">You can call the [Get Task Counts][rest_get_task_counts] operation to find out how many tasks are in an active, running, or completed state, and how many have succeeded or failed.</span></span> <span data-ttu-id="99078-107">각 상태에 있는 태스크 수를 계산하면 사용자에게 해당 작업의 진행 상태를 쉽게 표시하거나, 작업에 영향을 미칠 수 있는 예상치 못한 지연 또는 오류를 감지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99078-107">By counting the number of tasks in each state, you can more easily display the job's progress to a user, or detect unexpected delays or failures that may affect the job.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="99078-108">Get Task Counts 연산은 현재 미리 보기 상태이며 Azure Government, Azure China 및 Azure Germany에서는 아직 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="99078-108">The Get Task Counts operation is currently in preview, and is not yet available in Azure Government, Azure China, and Azure Germany.</span></span> 
>
>

## <a name="how-tasks-are-counted"></a><span data-ttu-id="99078-109">태스크 계산 방법</span><span class="sxs-lookup"><span data-stu-id="99078-109">How tasks are counted</span></span>

<span data-ttu-id="99078-110">Get Task Counts 연산은 다음과 같이 상태별로 태스크 수를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="99078-110">The Get Task Counts operation counts tasks by state, as follows:</span></span>

- <span data-ttu-id="99078-111">대기열에 있으며 실행할 수 있는 태스크는 **활성**으로 계산되지만, 현재는 계산 노드에 할당되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="99078-111">A task is counted as **active** when it is queued and able to run, but is not currently assigned to a compute node.</span></span> <span data-ttu-id="99078-112">아직 완료되지 않은 상위 테스크에 종속된 태스크도 **활성**으로 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="99078-112">A task is also counted as **active** if it is dependent on a parent task that has not yet completed.</span></span> <span data-ttu-id="99078-113">태스크 종속성 동작에 대한 자세한 내용은 [태스크 종속성을 만들어 다른 태스크에 종속된 태스크 실행](batch-task-dependencies.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="99078-113">For more information on task dependencies, see [Create task dependencies to run tasks that depend on other tasks](batch-task-dependencies.md).</span></span> 
- <span data-ttu-id="99078-114">계산 모드에 할당되었지만, 아직 완료하지 않은 태스크는 **실행 중**으로 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="99078-114">A task is counted as **running** when it has been assigned to a compute node, but has not yet completed.</span></span> <span data-ttu-id="99078-115">[태스크에 대한 정보 가져오기][rest_get_task] 연산으로 표시된 대로 상태가 `preparing` 또는 `running`인 태스크는 **실행 중**으로 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="99078-115">A task is counted as **running** when its state is either `preparing` or `running`, as indicated by the [Get information about a task][rest_get_task] operation.</span></span>
- <span data-ttu-id="99078-116">더 이상 실행 자격이 없는 태스크는 **완료**로 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="99078-116">A task is counted as **completed** when it is no longer eligible to run.</span></span> <span data-ttu-id="99078-117">**완료**로 계산된 태스크는 일반적으로 성공적으로 완료되었거나, 비성공적으로 완료되었고 다시 시도 제한 횟수를 모두 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="99078-117">A task counted as **completed** has typically either finished successfully, or has finished unsuccessfully and has also exhausted its retry limit.</span></span> 

<span data-ttu-id="99078-118">또한 Get Task Counts 연산은 성공 또는 실패한 태스크 수도 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="99078-118">The Get Task Counts operation also reports how many tasks have succeeded or failed.</span></span> <span data-ttu-id="99078-119">Batch는 [executionInfo][https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task#executionInfo] 속성의 **결과**를 확인하여 태스크가 성공 또는 실패했는지 판별합니다.</span><span class="sxs-lookup"><span data-stu-id="99078-119">Batch determines whether a task has succeeded or failed by checking the **result** property of the [executionInfo][https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task#executionInfo] property:</span></span>

    - <span data-ttu-id="99078-120">태스크 실행 결과가 `success`인 태스크는 **성공**으로 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="99078-120">A task is counted as **succeeded** if the result of task execution is `success`.</span></span>
    - <span data-ttu-id="99078-121">태스크 실행 결과가 `failure`인 태스크는 **실패**로 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="99078-121">A task is counted as **failed** if the result of task execution is `failure`.</span></span>

<span data-ttu-id="99078-122">태스크 상태에 대한 자세한 내용은 [태스크에 대한 정보 가져오기][rest_get_task]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="99078-122">For more information about task states, see [Get information about a task][rest_get_task].</span></span>

<span data-ttu-id="99078-123">다음 .NET 코드 예제는 상태별로 태스크 수를 가져오는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="99078-123">The following .NET code sample shows how to retrieve task counts by state:</span></span> 

```csharp
var taskCounts = await batchClient.JobOperations.GetTaskCountsAsync("job-1");

Console.WriteLine("Task count in active state: {0}", taskCounts.Active);
Console.WriteLine("Task count in preparing or running state: {0}", taskCounts.Running);
Console.WriteLine("Task count in completed state: {0}", taskCounts.Completed);
Console.WriteLine("Succeeded task count: {0}", taskCounts.Succeeded);
Console.WriteLine("Failed task count: {0}", taskCounts.Failed);
Console.WriteLine("ValidationStatus: {0}", taskCounts.ValidationStatus);
```

> [!NOTE]
> <span data-ttu-id="99078-124">REST 및 기타 지원되는 언어에 유사한 패턴을 사용하여 작업에 대한 태스크 수를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99078-124">You can use a similar pattern for REST and other supported languages to get task counts for a job.</span></span> 
> 
> 

## <a name="consistency-checking-for-task-counts"></a><span data-ttu-id="99078-125">태스크 수에 대한 일관성 확인</span><span class="sxs-lookup"><span data-stu-id="99078-125">Consistency checking for task counts</span></span>

<span data-ttu-id="99078-126">Batch 서비스는 비동기식 분산 시스템의 여러 부분에서 데이터를 수집하여 태스크 수를 집계합니다.</span><span class="sxs-lookup"><span data-stu-id="99078-126">The Batch service aggregates task counts by gathering data from multiple parts of an asynchronous distributed system.</span></span> <span data-ttu-id="99078-127">태스크 수가 정확한지 확인하기 위해 Batch는 시스템의 여러 구성 요소에 대한 일관성 검사를 수행하여 상태 수에 대한 추가적인 검증을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="99078-127">To ensure that task counts are correct, Batch provides additional validation for state counts by performing consistency checks against multiple components of the system.</span></span> <span data-ttu-id="99078-128">Batch는 작업에 200,000개 미만의 태스크가 있는 경우 이러한 일관성 검사를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="99078-128">Batch performs these consistency checks as long as there are fewer than 200,000 tasks in the job.</span></span> <span data-ttu-id="99078-129">드물게 일관성 검사에서 오류가 발견되면 Batch는 일관성 검사의 결과를 기준으로 Get Tasks Counts 연산의 결과를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="99078-129">In the unlikely event that the consistency check finds errors, Batch corrects the result of the Get Tasks Counts operation based on the results of the consistency check.</span></span> <span data-ttu-id="99078-130">일관성 검사는 Get Task Counts 연산을 사용하는 고객이 솔루션에 필요한 올바른 정보를 얻을 수 있도록 해주는 추가적인 조치입니다.</span><span class="sxs-lookup"><span data-stu-id="99078-130">The consistency check is an extra measure to ensure that customers who rely on the Get Task Counts operation get the right information they need for their solution.</span></span>

<span data-ttu-id="99078-131">응답에서 **validationStatus** 속성은 Batch가 일관성 검사를 수행했는지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="99078-131">The **validationStatus** property in the response indicates whether Batch has performed the consistency check.</span></span> <span data-ttu-id="99078-132">Batch가 시스템에 포함된 실제 상태를 기준으로 상태 수를 검사하지 못했다면 **validationStatus** 속성은 `unvalidated`(으)로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="99078-132">If Batch has not been able to check state counts against the actual states held in the system, then the **validationStatus** property is set to `unvalidated`.</span></span> <span data-ttu-id="99078-133">성능상의 이유로, 작업에 200,000개 이상의 태스크가 포함되어 있는 경우 Batch가 일관성 검사를 수행하지 않으므로, 이 경우 **validationStatus** 속성을 `unvalidated`(으)로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99078-133">For performance reasons, Batch will not perform the consistency check if the job includes more than 200,000 tasks, so the **validationStatus** property may be set to `unvalidated` in this case.</span></span> <span data-ttu-id="99078-134">그러나 이 경우에는 모든 제한된 데이터 손실 가능성이 매우 높으므로, 태스크 수가 틀릴 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99078-134">However, the task count is not necessarily wrong in this case, as even a very limited data loss is highly unlikely.</span></span> 

<span data-ttu-id="99078-135">태스크 상태가 변경되면 집계 파이프라인은 몇 초 이내에 변경 사항을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="99078-135">When a task changes state, the aggregation pipeline processes the change within few seconds.</span></span> <span data-ttu-id="99078-136">Get Task Counts 연산은 해당 기간 이내에 업데이트된 태스크 수를 반영합니다.</span><span class="sxs-lookup"><span data-stu-id="99078-136">The Get Task Counts operation reflects the updated task counts within that period.</span></span> <span data-ttu-id="99078-137">그러나 집계 파이프라인이 태스크 상태의 변경을 놓칠 경우 해당 변경 사항은 다음 유효성 검사에 통과할 때까지 등록되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="99078-137">However, if the aggregation pipeline misses a change in a task state, then that change is not registered until the next validation pass.</span></span> <span data-ttu-id="99078-138">이 시간 동안 태스크 수는 누락된 이벤트로 인해 약간 정확하지 않을 수 있지만, 다음 유효성 검사 통과 시 수정됩니다.</span><span class="sxs-lookup"><span data-stu-id="99078-138">During this time, task counts may be slightly inaccurate due to the missed event, but they are corrected on the next validation pass.</span></span>

## <a name="best-practices-for-counting-a-jobs-tasks"></a><span data-ttu-id="99078-139">작업의 태스크 수를 계산하는 모범 관행</span><span class="sxs-lookup"><span data-stu-id="99078-139">Best practices for counting a job's tasks</span></span>

<span data-ttu-id="99078-140">Get Task Counts 연산 호출은 작업 상태별로 기본 수를 반환하는 가장 효율적인 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="99078-140">Calling the Get Task Counts operation is the most efficient way to return a basic count of a job's tasks by state.</span></span> <span data-ttu-id="99078-141">Batch 서비스 버전 2017-06-01.5.1을 사용하고 있는 경우 Get Task Counts를 사용하도록 코드를 작성 또는 업데이트하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="99078-141">If you are using Batch service version 2017-06-01.5.1, we recommend writing or updating your code to use Get Task Counts.</span></span>

<span data-ttu-id="99078-142">2017-06-01.5.1 이전의 Batch 서비스 버전에서는 Get Task Counts 연산을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="99078-142">The Get Task Counts operation is not available in Batch service versions earlier than 2017-06-01.5.1.</span></span> <span data-ttu-id="99078-143">이전 버전의 서비스를 사용하는 경우, 대신 목록 쿼리를 사용하여 작업의 태스크를 계산하세요.</span><span class="sxs-lookup"><span data-stu-id="99078-143">If you are using an older version of the service, then use a list query to count tasks in a job instead.</span></span> <span data-ttu-id="99078-144">자세한 내용은 [쿼리를 만들어서 효율적으로 Batch 리소스 나열](batch-efficient-list-queries.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="99078-144">For more information, see [Create queries to list Batch resources efficiently](batch-efficient-list-queries.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="99078-145">다음 단계</span><span class="sxs-lookup"><span data-stu-id="99078-145">Next steps</span></span>

* <span data-ttu-id="99078-146">Batch 서비스의 개념 및 기능에 대한 자세한 내용은 [Batch 기능 개요](batch-api-basics.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="99078-146">See the [Batch feature overview](batch-api-basics.md) to learn more about Batch service concepts and features.</span></span> <span data-ttu-id="99078-147">이 문서에서는 풀, 계산 노드, 작업 및 태스크 등의 기본 Batch 리소스에 대해 설명하며 서비스의 기능에 대한 개요를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="99078-147">The article discusses the primary Batch resources such as pools, compute nodes, jobs, and tasks, and provides an overview of the service's features.</span></span>
* <span data-ttu-id="99078-148">[Batch .NET 클라이언트 라이브러리](batch-dotnet-get-started.md) 또는 [Python](batch-python-tutorial.md)을 사용하여 배치 지원 응용 프로그램 개발에 대한 기본 사항을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="99078-148">Learn the basics of developing a Batch-enabled application using the [Batch .NET client library](batch-dotnet-get-started.md) or [Python](batch-python-tutorial.md).</span></span> <span data-ttu-id="99078-149">이러한 소개 자료에서는 Batch 서비스를 사용하여 여러 계산 노드에서 워크로드를 실행하는 작업 응용 프로그램을 단계별로 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="99078-149">These introductory articles guide you through a working application that uses the Batch service to execute a workload on multiple compute nodes.</span></span>


[rest_get_task_counts]: https://docs.microsoft.com/rest/api/batchservice/get-the-task-counts-for-a-job
[rest_get_task]: https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task
[rest_list_tasks]: https://docs.microsoft.com/rest/api/batchservice/list-the-tasks-associated-with-a-job

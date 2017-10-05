---
title: "작업 의존 관계를 사용하여 다른 작업의 완료에 따라 작업 실행 - Azure 배치 | Microsoft Docs"
description: "Azure 배치에서 MapReduce 스타일과 비슷한 빅 데이터 워크로드를 처리하기 위해 다른 작업의 완료에 종속된 작업을 만듭니다."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: b8d12db5-ca30-4c7d-993a-a05af9257210
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 465306d2de8d1dbe6ba1f0cd74be720b78a50de3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-task-dependencies-to-run-tasks-that-depend-on-other-tasks"></a><span data-ttu-id="36a2b-103">작업 의존 관계를 만들어 다른 작업에 종속된 작업 실행</span><span class="sxs-lookup"><span data-stu-id="36a2b-103">Create task dependencies to run tasks that depend on other tasks</span></span>

<span data-ttu-id="36a2b-104">상위 태스크가 완료된 후에 (일련의) 태스크를 실행하는 태스크 종속성을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36a2b-104">You can define task dependencies to run a task or set of tasks only after a parent task has completed.</span></span> <span data-ttu-id="36a2b-105">태스크 종속성이 유용한 몇 가지 시나리오는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="36a2b-105">Some scenarios where task dependencies are useful include:</span></span>

* <span data-ttu-id="36a2b-106">클라우드에서 MapReduce 스타일의 컴퓨팅 워크로드</span><span class="sxs-lookup"><span data-stu-id="36a2b-106">MapReduce-style workloads in the cloud.</span></span>
* <span data-ttu-id="36a2b-107">DAG(방향성 비순환 그래프)으로 표현할 수 있는 태스크의 데이터 처리 작업</span><span class="sxs-lookup"><span data-stu-id="36a2b-107">Jobs whose data processing tasks can be expressed as a directed acyclic graph (DAG).</span></span>
* <span data-ttu-id="36a2b-108">프로세스를 미리 렌더링하거나 사후 렌더링하는 경우 다음 태스크를 시작하기 전에 각 태스크를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="36a2b-108">Pre-rendering and post-rendering processes, where each task must complete before the next task can begin.</span></span>
* <span data-ttu-id="36a2b-109">다운스트림 태스크가 업스트림 태스크의 출력에 따라 달라지는 다른 작업</span><span class="sxs-lookup"><span data-stu-id="36a2b-109">Any other job in which downstream tasks depend on the output of upstream tasks.</span></span>

<span data-ttu-id="36a2b-110">Batch 태스크 종속성을 통해 하나 이상의 상위 태스크를 완료한 후에 계산 노드에서 실행하기 위해 예약된 태스크를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36a2b-110">With Batch task dependencies, you can create tasks that are scheduled for execution on compute nodes after the completion of one or more parent tasks.</span></span> <span data-ttu-id="36a2b-111">예를 들어, 별도의 병렬 태스크를 포함한 3D 동영상의 각 프레임을 렌더링하는 작업을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36a2b-111">For example, you can create a job that renders each frame of a 3D movie with separate, parallel tasks.</span></span> <span data-ttu-id="36a2b-112">해당 최종 작업인 "병합 태스크"는 전체 프레임이 성공적으로 렌더링된 경우에만 렌더링된 프레임을 완전한 영화로 함께 병합합니다.</span><span class="sxs-lookup"><span data-stu-id="36a2b-112">The final task--the "merge task"--merges the rendered frames into the complete movie only after all frames have been successfully rendered.</span></span>

<span data-ttu-id="36a2b-113">기본적으로 종속 태스크는 상위 태스크가 완료된 후에만 실행하기 위해 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="36a2b-113">By default, dependent tasks are scheduled for execution only after the parent task has completed successfully.</span></span> <span data-ttu-id="36a2b-114">상위 태스크가 실패한 경우 기본 동작을 재정의하고 태스크를 실행하는 종속성 동작을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36a2b-114">You can specify a dependency action to override the default behavior and run tasks when the parent task fails.</span></span> <span data-ttu-id="36a2b-115">자세한 내용은 [종속성 작업](#dependency-actions) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="36a2b-115">See the [Dependency actions](#dependency-actions) section for details.</span></span>  

<span data-ttu-id="36a2b-116">일대일 또는 일대다 관계에서 다른 태스크에 따라 달라지는 태스크를 만들 수 있으며,</span><span class="sxs-lookup"><span data-stu-id="36a2b-116">You can create tasks that depend on other tasks in a one-to-one or one-to-many relationship.</span></span> <span data-ttu-id="36a2b-117">지정된 범위의 태스크 ID 내에서 태스크 그룹이 완료되는 데 따라 태스크가 달라지는 범위 종속성을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36a2b-117">You can also create a range dependency where a task depends on the completion of a group of tasks within a specified range of task IDs.</span></span> <span data-ttu-id="36a2b-118">다대다 관계를 만들기 위해 다음 세 가지 기본 시나리오를 결합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36a2b-118">You can combine these three basic scenarios to create many-to-many relationships.</span></span>

## <a name="task-dependencies-with-batch-net"></a><span data-ttu-id="36a2b-119">배치 .NET을 사용한 태스크 종속성</span><span class="sxs-lookup"><span data-stu-id="36a2b-119">Task dependencies with Batch .NET</span></span>
<span data-ttu-id="36a2b-120">이 문서에서는 [배치 .NET][net_msdn] 라이브러리를 사용하여 태스크 종속성을 구성하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="36a2b-120">In this article, we discuss how to configure task dependencies by using the [Batch .NET][net_msdn] library.</span></span> <span data-ttu-id="36a2b-121">먼저는 작업에서 [태스크 종속성을 사용](#enable-task-dependencies)하는 방법을 보여 주고 [종속성을 사용하여 태스크를 구성](#create-dependent-tasks)하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="36a2b-121">We first show you how to [enable task dependency](#enable-task-dependencies) on your jobs, and then demonstrate how to [configure a task with dependencies](#create-dependent-tasks).</span></span> <span data-ttu-id="36a2b-122">또한 상위 태스크가 실패하는 경우 종속 태스크를 실행하는 종속성 작동을 지정하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="36a2b-122">We also describe how to specify a dependency action to run dependent tasks if the parent fails.</span></span> <span data-ttu-id="36a2b-123">마지막으로 배치에서 지원되는 [종속성 시나리오](#dependency-scenarios)를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="36a2b-123">Finally, we discuss the [dependency scenarios](#dependency-scenarios) that Batch supports.</span></span>

## <a name="enable-task-dependencies"></a><span data-ttu-id="36a2b-124">태스크 종속성 사용</span><span class="sxs-lookup"><span data-stu-id="36a2b-124">Enable task dependencies</span></span>
<span data-ttu-id="36a2b-125">Batch 응용 프로그램에서 태스크 종속성을 사용하려면 먼저 작업이 태스크 종속성을 사용하도록 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="36a2b-125">To use task dependencies in your Batch application, you must first configure the job to use task dependencies.</span></span> <span data-ttu-id="36a2b-126">Batch .NET에서 해당 [UsesTaskDependencies][net_usestaskdependencies] 속성을 `true`으로 설정하여 [CloudJob][net_cloudjob]에서 이를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="36a2b-126">In Batch .NET, enable it on your [CloudJob][net_cloudjob] by setting its [UsesTaskDependencies][net_usestaskdependencies] property to `true`:</span></span>

```csharp
CloudJob unboundJob = batchClient.JobOperations.CreateJob( "job001",
    new PoolInformation { PoolId = "pool001" });

// IMPORTANT: This is REQUIRED for using task dependencies.
unboundJob.UsesTaskDependencies = true;
```

<span data-ttu-id="36a2b-127">앞의 코드 조각에서 "batchClient"는 [BatchClient][net_batchclient] 클래스의 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="36a2b-127">In the preceding code snippet, "batchClient" is an instance of the [BatchClient][net_batchclient] class.</span></span>

## <a name="create-dependent-tasks"></a><span data-ttu-id="36a2b-128">종속성 태스크 만들기</span><span class="sxs-lookup"><span data-stu-id="36a2b-128">Create dependent tasks</span></span>
<span data-ttu-id="36a2b-129">하나 이상의 상위 태스크를 완료하는 데 따라 달라지는 태스크를 만들려면 태스크가 다른 태스크"에 종속"되도록 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36a2b-129">To create a task that depends on the completion of one or more parent tasks, you can specify that the task "depends on" the other tasks.</span></span> <span data-ttu-id="36a2b-130">Batch .NET에서 [TaskDependencies][net_taskdependencies] 클래스의 인스턴스를 사용하여 [CloudTask][net_cloudtask].[DependsOn][net_dependson] 속성을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="36a2b-130">In Batch .NET, configure the [CloudTask][net_cloudtask].[DependsOn][net_dependson] property with an instance of the [TaskDependencies][net_taskdependencies] class:</span></span>

```csharp
// Task 'Flowers' depends on completion of both 'Rain' and 'Sun'
// before it is run.
new CloudTask("Flowers", "cmd.exe /c echo Flowers")
{
    DependsOn = TaskDependencies.OnIds("Rain", "Sun")
},
```

<span data-ttu-id="36a2b-131">이 코드 조각은 태스크 ID가 "Flowers"인 종속 태스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="36a2b-131">This code snippet creates a dependent task with task ID "Flowers".</span></span> <span data-ttu-id="36a2b-132">"Flowers" 태스크는 "Rain" 및 "Sun" 태스크에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="36a2b-132">The "Flowers" task depends on tasks "Rain" and "Sun".</span></span> <span data-ttu-id="36a2b-133">"Rain" 및 "Sun" 태스크를 성공적으로 완료한 후에 "Flowers" 태스크를 계산 노드에서 실행되도록 예약합니다.</span><span class="sxs-lookup"><span data-stu-id="36a2b-133">Task "Flowers" will be scheduled to run on a compute node only after tasks "Rain" and "Sun" have completed successfully.</span></span>

> [!NOTE]
> <span data-ttu-id="36a2b-134">태스크가 **완료** 상태이고 해당 **종료 코드**가 `0`인 경우 성공적으로 완료되었다고 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="36a2b-134">A task is considered to be completed successfully when it is in the **completed** state and its **exit code** is `0`.</span></span> <span data-ttu-id="36a2b-135">즉, Batch .NET에서 `Completed`의 [CloudTask][net_cloudtask].[State][net_taskstate] 속성 값 및 CloudTask의 [TaskExecutionInformation][net_taskexecutioninformation].[ExitCode][net_exitcode] 속성 값은 `0`입니다.</span><span class="sxs-lookup"><span data-stu-id="36a2b-135">In Batch .NET, this means a [CloudTask][net_cloudtask].[State][net_taskstate] property value of `Completed` and the CloudTask's [TaskExecutionInformation][net_taskexecutioninformation].[ExitCode][net_exitcode] property value is `0`.</span></span>
> 
> 

## <a name="dependency-scenarios"></a><span data-ttu-id="36a2b-136">종속성 시나리오</span><span class="sxs-lookup"><span data-stu-id="36a2b-136">Dependency scenarios</span></span>
<span data-ttu-id="36a2b-137">Azure 배치에서 사용할 수 있는 세 가지 기본 태스크 종속성 시나리오는 일대일, 일대다 및 태스크 ID 범위 종속성입니다.</span><span class="sxs-lookup"><span data-stu-id="36a2b-137">There are three basic task dependency scenarios that you can use in Azure Batch: one-to-one, one-to-many, and task ID range dependency.</span></span> <span data-ttu-id="36a2b-138">네 번째 시나리오인 다대다를 제공하도록 결합될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36a2b-138">These can be combined to provide a fourth scenario, many-to-many.</span></span>

| <span data-ttu-id="36a2b-139">시나리오&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="sxs-lookup"><span data-stu-id="36a2b-139">Scenario&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span> | <span data-ttu-id="36a2b-140">예</span><span class="sxs-lookup"><span data-stu-id="36a2b-140">Example</span></span> |  |
|:---:| --- | --- |
|  [<span data-ttu-id="36a2b-141">일대일</span><span class="sxs-lookup"><span data-stu-id="36a2b-141">One-to-one</span></span>](#one-to-one) |<span data-ttu-id="36a2b-142">*taskB*가 *taskA*에 종속됨</span><span class="sxs-lookup"><span data-stu-id="36a2b-142">*taskB* depends on *taskA*</span></span> <p/> <span data-ttu-id="36a2b-143">*taskB*는 *taskA*가 성공적으로 완료될 때까지 실행하도록 예약되지 않음</span><span class="sxs-lookup"><span data-stu-id="36a2b-143">*taskB* will not be scheduled for execution until *taskA* has completed successfully</span></span> |<span data-ttu-id="36a2b-144">![다이어그램: 일대일 태스크 종속성][1]</span><span class="sxs-lookup"><span data-stu-id="36a2b-144">![Diagram: one-to-one task dependency][1]</span></span> |
|  [<span data-ttu-id="36a2b-145">일대다</span><span class="sxs-lookup"><span data-stu-id="36a2b-145">One-to-many</span></span>](#one-to-many) |<span data-ttu-id="36a2b-146">*taskC*는 *taskA* 및 *taskB*에 종속됨</span><span class="sxs-lookup"><span data-stu-id="36a2b-146">*taskC* depends on both *taskA* and *taskB*</span></span> <p/> <span data-ttu-id="36a2b-147">*taskC*는 *taskA* 및 *taskB*가 성공적으로 완료될 때까지 실행하도록 예약되지 않음</span><span class="sxs-lookup"><span data-stu-id="36a2b-147">*taskC* will not be scheduled for execution until both *taskA* and *taskB* have completed successfully</span></span> |<span data-ttu-id="36a2b-148">![다이어그램: 일대다 태스크 종속성][2]</span><span class="sxs-lookup"><span data-stu-id="36a2b-148">![Diagram: one-to-many task dependency][2]</span></span> |
|  [<span data-ttu-id="36a2b-149">태스크 ID 범위</span><span class="sxs-lookup"><span data-stu-id="36a2b-149">Task ID range</span></span>](#task-id-range) |<span data-ttu-id="36a2b-150">*taskD*가 태스크의 범위에 종속됨</span><span class="sxs-lookup"><span data-stu-id="36a2b-150">*taskD* depends on a range of tasks</span></span> <p/> <span data-ttu-id="36a2b-151">*taskD*는 ID *1*-*10*을 가진 태스크가 성공적으로 완료될 때까지 실행하도록 예약되지 않음</span><span class="sxs-lookup"><span data-stu-id="36a2b-151">*taskD* will not be scheduled for execution until the tasks with IDs *1* through *10* have completed successfully</span></span> |<span data-ttu-id="36a2b-152">![다이어그램: 태스크 ID 범위 종속성][3]</span><span class="sxs-lookup"><span data-stu-id="36a2b-152">![Diagram: Task id range dependency][3]</span></span> |

> [!TIP]
> <span data-ttu-id="36a2b-153">태스크 C, D, E 및 F는 각각 태스크 A 및 B에 종속되는 경우 **다대다** 관계를 만들 수 있습니다. 예를 들어, 다운스트림 태스크가 여러 업스트림 태스크의 출력에 따라 달라지는 병렬화된 전처리 시나리오에서 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="36a2b-153">You can create **many-to-many** relationships, such as where tasks C, D, E, and F each depend on tasks A and B. This is useful, for example, in parallelized preprocessing scenarios where your downstream tasks depend on the output of multiple upstream tasks.</span></span>
> 
> <span data-ttu-id="36a2b-154">이 섹션의 예제에서는 부모 태스크가 성공적으로 완료된 후에 종속 태스크가 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="36a2b-154">In the examples in this section, a dependent task runs only after the parent tasks complete successfully.</span></span> <span data-ttu-id="36a2b-155">이 동작은 종속 태스크에 대한 기본 동작입니다.</span><span class="sxs-lookup"><span data-stu-id="36a2b-155">This behavior is the default behavior for a dependent task.</span></span> <span data-ttu-id="36a2b-156">기본 동작을 재정의하는 종속성 작업을 지정하여 상위 태스크에 실패한 후에 종속 태스크를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36a2b-156">You can run a dependent task after a parent task fails by specifying a dependency action to override the default behavior.</span></span> <span data-ttu-id="36a2b-157">자세한 내용은 [종속성 작업](#dependency-actions) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="36a2b-157">See the [Dependency actions](#dependency-actions) section for details.</span></span>

### <a name="one-to-one"></a><span data-ttu-id="36a2b-158">일대일</span><span class="sxs-lookup"><span data-stu-id="36a2b-158">One-to-one</span></span>
<span data-ttu-id="36a2b-159">일대일 관계의 경우 태스크는 상위 태스크를 성공적으로 완료했는지에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="36a2b-159">In a one-to-one relationship, a task depends on the successful completion of one parent task.</span></span> <span data-ttu-id="36a2b-160">종속성을 만들려면 [CloudTask][net_cloudtask]의 [DependsOn][net_dependson] 속성을 채우는 경우 단일 태스크 ID를 [TaskDependencies][net_taskdependencies].[OnId][net_onid] 고정 메서드에 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="36a2b-160">To create the dependency, provide a single task ID to the [TaskDependencies][net_taskdependencies].[OnId][net_onid] static method when you populate the [DependsOn][net_dependson] property of [CloudTask][net_cloudtask].</span></span>

```csharp
// Task 'taskA' doesn't depend on any other tasks
new CloudTask("taskA", "cmd.exe /c echo taskA"),

// Task 'taskB' depends on completion of task 'taskA'
new CloudTask("taskB", "cmd.exe /c echo taskB")
{
    DependsOn = TaskDependencies.OnId("taskA")
},
```

### <a name="one-to-many"></a><span data-ttu-id="36a2b-161">일대다</span><span class="sxs-lookup"><span data-stu-id="36a2b-161">One-to-many</span></span>
<span data-ttu-id="36a2b-162">일대다 관계의 경우 태스크는 여러 상위 태스크를 완료했는지에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="36a2b-162">In a one-to-many relationship, a task depends on the completion of multiple parent tasks.</span></span> <span data-ttu-id="36a2b-163">종속성을 만들려면 [CloudTask][net_cloudtask]의 [DependsOn][net_dependson] 속성을 채우는 경우 태스크 ID 컬렉션을 [TaskDependencies][net_taskdependencies].[OnId][net_onids] 고정 메서드에 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="36a2b-163">To create the dependency, provide a collection of task IDs to the [TaskDependencies][net_taskdependencies].[OnIds][net_onids] static method when you populate the [DependsOn][net_dependson] property of [CloudTask][net_cloudtask].</span></span>

```csharp
// 'Rain' and 'Sun' don't depend on any other tasks
new CloudTask("Rain", "cmd.exe /c echo Rain"),
new CloudTask("Sun", "cmd.exe /c echo Sun"),

// Task 'Flowers' depends on completion of both 'Rain' and 'Sun'
// before it is run.
new CloudTask("Flowers", "cmd.exe /c echo Flowers")
{
    DependsOn = TaskDependencies.OnIds("Rain", "Sun")
},
``` 

### <a name="task-id-range"></a><span data-ttu-id="36a2b-164">태스크 ID 범위</span><span class="sxs-lookup"><span data-stu-id="36a2b-164">Task ID range</span></span>
<span data-ttu-id="36a2b-165">상위 태스크의 범위에 대한 종속성에서 태스크는 범위 내에 있는 ID를 가진 태스크를 완료했는지에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="36a2b-165">In a dependency on a range of parent tasks, a task depends on the the completion of tasks whose IDs lie within a range.</span></span>
<span data-ttu-id="36a2b-166">종속성을 만들려면 [CloudTask][net_cloudtask]의 [DependsOn][net_dependson] 속성을 채우는 경우 범위에서 처음 및 최신 태스크 ID를 [TaskDependencies][net_taskdependencies].[OnIdRange][net_onidrange] 고정 메서드에 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="36a2b-166">To create the dependency, provide the first and last task IDs in the range to the [TaskDependencies][net_taskdependencies].[OnIdRange][net_onidrange] static method when you populate the [DependsOn][net_dependson] property of [CloudTask][net_cloudtask].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="36a2b-167">종속성에 대한 태스크 ID 범위를 사용하는 경우 범위의 태스크 ID는 정수 값의 문자열 *표시여야* 합니다.</span><span class="sxs-lookup"><span data-stu-id="36a2b-167">When you use task ID ranges for your dependencies, the task IDs in the range *must* be string representations of integer values.</span></span>
> 
> <span data-ttu-id="36a2b-168">**충족**으로 설정된 종속성 작업에 매핑되는 오류를 성공적으로 완료하거나 해결하여 범위에 있는 모든 태스크가 종속성을 충족해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="36a2b-168">Every task in the range must satisfy the dependency, either by completing successfully or by completing with a failure that’s mapped to a dependency action set to **Satisfy**.</span></span> <span data-ttu-id="36a2b-169">자세한 내용은 [종속성 작업](#dependency-actions) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="36a2b-169">See the [Dependency actions](#dependency-actions) section for details.</span></span>
>
>

```csharp
// Tasks 1, 2, and 3 don't depend on any other tasks. Because
// we will be using them for a task range dependency, we must
// specify string representations of integers as their ids.
new CloudTask("1", "cmd.exe /c echo 1"),
new CloudTask("2", "cmd.exe /c echo 2"),
new CloudTask("3", "cmd.exe /c echo 3"),

// Task 4 depends on a range of tasks, 1 through 3
new CloudTask("4", "cmd.exe /c echo 4")
{
    // To use a range of tasks, their ids must be integer values.
    // Note that we pass integers as parameters to TaskIdRange,
    // but their ids (above) are string representations of the ids.
    DependsOn = TaskDependencies.OnIdRange(1, 3)
},
```

## <a name="dependency-actions"></a><span data-ttu-id="36a2b-170">종속성 작업</span><span class="sxs-lookup"><span data-stu-id="36a2b-170">Dependency actions</span></span>

<span data-ttu-id="36a2b-171">기본적으로 상위 태스크가 성공적으로 완료된 후에만 (일련의) 종속 태스크가 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="36a2b-171">By default, a dependent task or set of tasks runs only after a parent task has completed successfully.</span></span> <span data-ttu-id="36a2b-172">일부 시나리오에서는 상위 태스크가 실패하더라도 종속 태스크를 실행하려고 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36a2b-172">In some scenarios, you may want to run dependent tasks even if the parent task fails.</span></span> <span data-ttu-id="36a2b-173">종속성 작업을 지정하여 기본 동작을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36a2b-173">You can override the default behavior by specifying a dependency action.</span></span> <span data-ttu-id="36a2b-174">종속성 작업은 상위 태스크의 성공 또는 실패에 따라 종속 태스크를 실행할 수 있는지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="36a2b-174">A dependency action specifies whether a dependent task is eligible to run, based on the success or failure of the parent task.</span></span> 

<span data-ttu-id="36a2b-175">예를 들어, 종속 태스크는 데이터가 업스트림 태스크를 완료하도록 대기 중입니다.</span><span class="sxs-lookup"><span data-stu-id="36a2b-175">For example, suppose that a dependent task is awaiting data from the completion of the upstream task.</span></span> <span data-ttu-id="36a2b-176">업스트림 태스크가 실패할 경우 종속 태스크는 오래된 데이터를 사용하여 실행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36a2b-176">If the upstream task fails, the dependent task may still be able to run using older data.</span></span> <span data-ttu-id="36a2b-177">이 경우에 종속성 작업은 상위 태스크가 실패하더라도 종속 태스크를 실행할 수 있는지 여부를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36a2b-177">In this case, a dependency action can specify that the dependent task is eligible to run despite the failure of the parent task.</span></span>

<span data-ttu-id="36a2b-178">종속성 작업은 상위 태스크에 대한 종료 조건을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="36a2b-178">A dependency action is based on an exit condition for the parent task.</span></span> <span data-ttu-id="36a2b-179">다음과 같은 종료 조건에 대한 종속성 작업을 지정할 수 있습니다. .NET에 대한 세부 정보는 [ExitConditions][net_exitconditions]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="36a2b-179">You can specify a dependency action for any of the following exit conditions; for .NET, see the [ExitConditions][net_exitconditions] class for details:</span></span>

- <span data-ttu-id="36a2b-180">전처리 오류가 발생할 때</span><span class="sxs-lookup"><span data-stu-id="36a2b-180">When a pre-processing error occurs.</span></span>
- <span data-ttu-id="36a2b-181">파일을 업로드 오류가 발생할 때</span><span class="sxs-lookup"><span data-stu-id="36a2b-181">When a file upload error occurs.</span></span> <span data-ttu-id="36a2b-182">태스크가 **exitCodes** 또는 **exitCodeRanges**를 통해 지정된 종료 코드로 인해 종료된 다음 파일 업로드 오류가 발생하면 해당 종료 코드로 지정된 작업이 우선적으로 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="36a2b-182">If the task exits with an exit code that was specified via **exitCodes** or **exitCodeRanges**, and then encounters a file upload error, the action specified by the exit code takes precedence.</span></span>
- <span data-ttu-id="36a2b-183">태스크가 **ExitCodes** 속성으로 정의된 종료 코드로 인해 종료되는 경우</span><span class="sxs-lookup"><span data-stu-id="36a2b-183">When the task exits with an exit code defined by the **ExitCodes** property.</span></span>
- <span data-ttu-id="36a2b-184">태스크가 **ExitCodeRanges** 속성에서 지정한 범위 내에서 실패한 종료 코드로 인해 종료되는 경우</span><span class="sxs-lookup"><span data-stu-id="36a2b-184">When the task exits with an exit code that falls within a range specified by the **ExitCodeRanges** property.</span></span>
- <span data-ttu-id="36a2b-185">기본적인 경우(태스크가 **ExitCodes** 또는 **ExitCodeRanges**로 정의되지 않은 종료 코드로 인해 종료되거나 태스크가 전처리 오류와 함께 종료되고 **PreProcessingError** 속성이 설정되지 않았거나, 태스크가 파일 업로드 오류로 인해 실패하고 **FileUploadError** 속성이 설정되지 않은 경우)</span><span class="sxs-lookup"><span data-stu-id="36a2b-185">The default case, if the task exits with an exit code not defined by **ExitCodes** or **ExitCodeRanges**, or if the task exits with a pre-processing error and the **PreProcessingError** property is not set, or if the task fails with a file upload error and the **FileUploadError** property is not set.</span></span> 

<span data-ttu-id="36a2b-186">.NET의 종속성 작업을 지정하려면 종료 조건에 대한 [ExitOptions][net_exitoptions].[DependencyAction][net_dependencyaction] 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="36a2b-186">To specify a dependency action in .NET, set the [ExitOptions][net_exitoptions].[DependencyAction][net_dependencyaction] property for the exit condition.</span></span> <span data-ttu-id="36a2b-187">**DependencyAction** 속성은 다음 두 값 중 하나를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="36a2b-187">The **DependencyAction** property takes one of two values:</span></span>

- <span data-ttu-id="36a2b-188">**DependencyAction** 속성을 **충족**으로 설정하면 지정된 오류로 인해 상위 태스크를 종료하는 경우 종속 태스크를 실행할 수 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="36a2b-188">Setting the **DependencyAction** property to **Satisfy** indicates that dependent tasks are eligible to run if the parent task exits with a specified error.</span></span>
- <span data-ttu-id="36a2b-189">**DependencyAction** 속성을 **차단**으로 설정하면 종속 태스크를 실행할 수 없음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="36a2b-189">Setting the **DependencyAction** property to **Block** indicates that dependent tasks are not eligible to run.</span></span>

<span data-ttu-id="36a2b-190">**DependencyAction** 속성에 대한 기본 설정은 종료 코드 0의 경우 **충족**이고 다른 모든 종료 조건의 경우 **차단**입니다.</span><span class="sxs-lookup"><span data-stu-id="36a2b-190">The default setting for the **DependencyAction** property is **Satisfy** for exit code 0, and **Block** for all other exit conditions.</span></span>

<span data-ttu-id="36a2b-191">다음 코드 조각에서는 상위 태스크에 대한 **DependencyAction** 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="36a2b-191">The following code snippet sets the **DependencyAction** property for a parent task.</span></span> <span data-ttu-id="36a2b-192">전처리 오류 또는 지정된 오류 코드로 인해 상위 태스크가 종료되면 종속 태스크가 차단됩니다.</span><span class="sxs-lookup"><span data-stu-id="36a2b-192">If the parent task exits with a pre-processing error, or with the specified error codes, the dependent task is blocked.</span></span> <span data-ttu-id="36a2b-193">상위 태스크가 다른 0이 아닌 오류로 인해 종료되면 종속 태스크를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36a2b-193">If the parent task exits with any other non-zero error, the dependent task is eligible to run.</span></span>

```csharp
// Task A is the parent task.
new CloudTask("A", "cmd.exe /c echo A")
{
    // Specify exit conditions for task A and their dependency actions.
    ExitConditions = new ExitConditions
    {
        // If task A exits with a pre-processing error, block any downstream tasks (in this example, task B).
        PreProcessingError = new ExitOptions
        {
            DependencyAction = DependencyAction.Block
        },
        // If task A exits with the specified error codes, block any downstream tasks (in this example, task B).
        ExitCodes = new List<ExitCodeMapping>
        {
            new ExitCodeMapping(10, new ExitOptions() { DependencyAction = DependencyAction.Block }),
            new ExitCodeMapping(20, new ExitOptions() { DependencyAction = DependencyAction.Block })
        },
        // If task A succeeds or fails with any other error, any downstream tasks become eligible to run 
        // (in this example, task B).
        Default = new ExitOptions
        {
            DependencyAction = DependencyAction.Satisfy
        }
    }
},
// Task B depends on task A. Whether it becomes eligible to run depends on how task A exits.
new CloudTask("B", "cmd.exe /c echo B")
{
    DependsOn = TaskDependencies.OnId("A")
},
```

## <a name="code-sample"></a><span data-ttu-id="36a2b-194">코드 샘플</span><span class="sxs-lookup"><span data-stu-id="36a2b-194">Code sample</span></span>
<span data-ttu-id="36a2b-195">[TaskDependencies][github_taskdependencies] 샘플 프로젝트는 GitHub의 [Azure Batch 코드 샘플][github_samples] 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="36a2b-195">The [TaskDependencies][github_taskdependencies] sample project is one of the [Azure Batch code samples][github_samples] on GitHub.</span></span> <span data-ttu-id="36a2b-196">이 Visual Studio 솔루션은 다음 사항을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="36a2b-196">This Visual Studio solution demonstrates:</span></span>

- <span data-ttu-id="36a2b-197">작업에 대한 태스크 종속성을 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="36a2b-197">How to enable task dependency on a job</span></span>
- <span data-ttu-id="36a2b-198">다른 태스크에 종속된 태스크를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="36a2b-198">How to create tasks that depend on other tasks</span></span>
- <span data-ttu-id="36a2b-199">계산 노드의 풀에서 해당 태스크를 실행하는 방법</span><span class="sxs-lookup"><span data-stu-id="36a2b-199">How to execute those tasks on a pool of compute nodes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="36a2b-200">다음 단계</span><span class="sxs-lookup"><span data-stu-id="36a2b-200">Next steps</span></span>
### <a name="application-deployment"></a><span data-ttu-id="36a2b-201">응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="36a2b-201">Application deployment</span></span>
<span data-ttu-id="36a2b-202">배치의 [응용 프로그램 패키지](batch-application-packages.md) 기능은 계산 노드에서 태스크를 실행하는 응용 프로그램을 배포하고 버전을 관리하는 쉬운 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="36a2b-202">The [application packages](batch-application-packages.md) feature of Batch provides an easy way to both deploy and version the applications that your tasks execute on compute nodes.</span></span>

### <a name="installing-applications-and-staging-data"></a><span data-ttu-id="36a2b-203">응용 프로그램 설치 및 데이터 준비</span><span class="sxs-lookup"><span data-stu-id="36a2b-203">Installing applications and staging data</span></span>
<span data-ttu-id="36a2b-204">태스크를 실행하기 위해 노드를 준비하는 방법의 개요는 Azure 배치 포럼에서 [Batch 계산 노드에서 응용 프로그램 설치 및 데이터 스테이징][forum_post]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="36a2b-204">See [Installing applications and staging data on Batch compute nodes][forum_post] in the Azure Batch forum for an overview of methods for preparing your nodes to run tasks.</span></span> <span data-ttu-id="36a2b-205">Azure Batch 팀 구성원 중 한 사람이 작성한 이 게시물은 계산 노드에 응용 프로그램, 태스크 입력 데이터 및 다른 파일을 복사하는 다른 방법에 대한 좋은 기초입니다.</span><span class="sxs-lookup"><span data-stu-id="36a2b-205">Written by one of the Azure Batch team members, this post is a good primer on the different ways to copy applications, task input data, and other files to your compute nodes.</span></span>

[forum_post]: https://social.msdn.microsoft.com/Forums/en-US/87b19671-1bdf-427a-972c-2af7e5ba82d9/installing-applications-and-staging-data-on-batch-compute-nodes?forum=azurebatch
[github_taskdependencies]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/TaskDependencies
[github_samples]: https://github.com/Azure/azure-batch-samples
[net_batchclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_cloudtask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_dependson]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.dependson.aspx
[net_exitcode]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskexecutioninformation.exitcode.aspx
[net_exitconditions]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.exitconditions
[net_exitoptions]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.exitoptions
[net_dependencyaction]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.exitoptions#Microsoft_Azure_Batch_ExitOptions_DependencyAction
[net_msdn]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[net_onid]: https://msdn.microsoft.com/library/microsoft.azure.batch.taskdependencies.onid.aspx
[net_onids]: https://msdn.microsoft.com/library/microsoft.azure.batch.taskdependencies.onids.aspx
[net_onidrange]: https://msdn.microsoft.com/library/microsoft.azure.batch.taskdependencies.onidrange.aspx
[net_taskexecutioninformation]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskexecutioninformation.aspx
[net_taskstate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.common.taskstate.aspx
[net_usestaskdependencies]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.usestaskdependencies.aspx
[net_taskdependencies]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskdependencies.aspx

<span data-ttu-id="36a2b-206">[1]: ./media/batch-task-dependency/01_one_to_one.png "다이어그램: 일대일 종속성"</span><span class="sxs-lookup"><span data-stu-id="36a2b-206">[1]: ./media/batch-task-dependency/01_one_to_one.png "Diagram: one-to-one dependency"</span></span>
<span data-ttu-id="36a2b-207">[2]: ./media/batch-task-dependency/02_one_to_many.png "다이어그램: 일대다 종속성"</span><span class="sxs-lookup"><span data-stu-id="36a2b-207">[2]: ./media/batch-task-dependency/02_one_to_many.png "Diagram: one-to-many dependency"</span></span>
<span data-ttu-id="36a2b-208">[3]: ./media/batch-task-dependency/03_task_id_range.png "다이어그램: 태스크 ID 범위 종속성"</span><span class="sxs-lookup"><span data-stu-id="36a2b-208">[3]: ./media/batch-task-dependency/03_task_id_range.png "Diagram: task id range dependency"</span></span>

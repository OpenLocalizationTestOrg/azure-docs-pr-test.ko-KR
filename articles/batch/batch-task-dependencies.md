---
title: "다른 작업-Azure 일괄 처리의 hello 완료에 따라 aaaUse 작업 종속성 toorun 작업 | Microsoft Docs"
description: "MapReduce 스타일과 유사한 빅 데이터 처리에 대 한 다른 작업의 hello 완료에 종속 된 작업을 만들어 Azure 일괄 처리에서 워크 로드 합니다."
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
ms.openlocfilehash: faf08ec38cb30b1f66acd51e256c31aea6215c62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-task-dependencies-toorun-tasks-that-depend-on-other-tasks"></a><span data-ttu-id="d9d0f-103">다른 작업에 종속 되는 toorun 작업 작업 종속성을 만듭니다</span><span class="sxs-lookup"><span data-stu-id="d9d0f-103">Create task dependencies toorun tasks that depend on other tasks</span></span>

<span data-ttu-id="d9d0f-104">정의한 작업 종속성 toorun 작업 또는 작업 집합을 부모 작업이 완료 된 후에.</span><span class="sxs-lookup"><span data-stu-id="d9d0f-104">You can define task dependencies toorun a task or set of tasks only after a parent task has completed.</span></span> <span data-ttu-id="d9d0f-105">태스크 종속성이 유용한 몇 가지 시나리오는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d9d0f-105">Some scenarios where task dependencies are useful include:</span></span>

* <span data-ttu-id="d9d0f-106">Hello 클라우드에서 MapReduce 스타일 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9d0f-106">MapReduce-style workloads in hello cloud.</span></span>
* <span data-ttu-id="d9d0f-107">DAG(방향성 비순환 그래프)으로 표현할 수 있는 태스크의 데이터 처리 작업</span><span class="sxs-lookup"><span data-stu-id="d9d0f-107">Jobs whose data processing tasks can be expressed as a directed acyclic graph (DAG).</span></span>
* <span data-ttu-id="d9d0f-108">미리 렌더링 및 렌더링 후 프로세스 hello 다음 작업을 시작 하기 전에 각 태스크를 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9d0f-108">Pre-rendering and post-rendering processes, where each task must complete before hello next task can begin.</span></span>
* <span data-ttu-id="d9d0f-109">다른 작업 다운스트림 작업 hello 출력 업스트림 작업에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="d9d0f-109">Any other job in which downstream tasks depend on hello output of upstream tasks.</span></span>

<span data-ttu-id="d9d0f-110">일괄 처리 작업 종속성이 있는 하나 이상의 부모 작업으로 hello 완료 한 후 계산 노드에서 실행을 위해 예약 된 작업을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9d0f-110">With Batch task dependencies, you can create tasks that are scheduled for execution on compute nodes after hello completion of one or more parent tasks.</span></span> <span data-ttu-id="d9d0f-111">예를 들어, 별도의 병렬 태스크를 포함한 3D 동영상의 각 프레임을 렌더링하는 작업을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9d0f-111">For example, you can create a job that renders each frame of a 3D movie with separate, parallel tasks.</span></span> <span data-ttu-id="d9d0f-112">hello 최종 작업-hello "병합 작업"-렌더링 된 프레임을 hello 전체 동영상만 hello 결국 프레임이 병합이 성공적으로 렌더링 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d9d0f-112">hello final task--hello "merge task"--merges hello rendered frames into hello complete movie only after all frames have been successfully rendered.</span></span>

<span data-ttu-id="d9d0f-113">기본적으로 종속 작업 hello 부모 작업이 성공적으로 완료 한 후에 실행 예약 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9d0f-113">By default, dependent tasks are scheduled for execution only after hello parent task has completed successfully.</span></span> <span data-ttu-id="d9d0f-114">종속성 동작 toooverride hello 기본 동작을 지정 하 고 hello 부모 작업이 실패할 경우 작업을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9d0f-114">You can specify a dependency action toooverride hello default behavior and run tasks when hello parent task fails.</span></span> <span data-ttu-id="d9d0f-115">Hello 참조 [종속성 동작](#dependency-actions) 자세한 내용은 섹션.</span><span class="sxs-lookup"><span data-stu-id="d9d0f-115">See hello [Dependency actions](#dependency-actions) section for details.</span></span>  

<span data-ttu-id="d9d0f-116">일대일 또는 일대다 관계에서 다른 태스크에 따라 달라지는 태스크를 만들 수 있으며,</span><span class="sxs-lookup"><span data-stu-id="d9d0f-116">You can create tasks that depend on other tasks in a one-to-one or one-to-many relationship.</span></span> <span data-ttu-id="d9d0f-117">범위 종속 작업의 작업 Id의 지정된 된 범위 내에서 작업 그룹의 hello 완료에 종속 되는 위치를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9d0f-117">You can also create a range dependency where a task depends on hello completion of a group of tasks within a specified range of task IDs.</span></span> <span data-ttu-id="d9d0f-118">이러한 세 가지 기본 시나리오 toocreate 다 대 다 관계를 결합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9d0f-118">You can combine these three basic scenarios toocreate many-to-many relationships.</span></span>

## <a name="task-dependencies-with-batch-net"></a><span data-ttu-id="d9d0f-119">배치 .NET을 사용한 태스크 종속성</span><span class="sxs-lookup"><span data-stu-id="d9d0f-119">Task dependencies with Batch .NET</span></span>
<span data-ttu-id="d9d0f-120">이 문서에서는 방법을 사용 하 여 작업 종속성 tooconfigure hello [일괄 처리.NET] [ net_msdn] 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="d9d0f-120">In this article, we discuss how tooconfigure task dependencies by using hello [Batch .NET][net_msdn] library.</span></span> <span data-ttu-id="d9d0f-121">먼저 보여줍니다 너무 어떻게[작업 종속성을 사용 하도록 설정](#enable-task-dependencies) 사용자 작업에 너무 방법을 설명 하 고[종속성이 있는 작업을 구성할](#create-dependent-tasks)합니다.</span><span class="sxs-lookup"><span data-stu-id="d9d0f-121">We first show you how too[enable task dependency](#enable-task-dependencies) on your jobs, and then demonstrate how too[configure a task with dependencies](#create-dependent-tasks).</span></span> <span data-ttu-id="d9d0f-122">또한 방식과 toospecify 종속성 동작 toorun 종속 작업 hello 부모 실패할 경우 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9d0f-122">We also describe how toospecify a dependency action toorun dependent tasks if hello parent fails.</span></span> <span data-ttu-id="d9d0f-123">Hello에서는 마지막으로, [종속성 시나리오](#dependency-scenarios) 지 원하는 일괄 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9d0f-123">Finally, we discuss hello [dependency scenarios](#dependency-scenarios) that Batch supports.</span></span>

## <a name="enable-task-dependencies"></a><span data-ttu-id="d9d0f-124">태스크 종속성 사용</span><span class="sxs-lookup"><span data-stu-id="d9d0f-124">Enable task dependencies</span></span>
<span data-ttu-id="d9d0f-125">일괄 처리 응용 프로그램에서 작업 종속성 toouse 먼저 hello 작업 toouse 작업 종속성 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9d0f-125">toouse task dependencies in your Batch application, you must first configure hello job toouse task dependencies.</span></span> <span data-ttu-id="d9d0f-126">일괄 처리.net에서에서 사용 하면 [CloudJob] [ net_cloudjob] 설정 하 여 해당 [UsesTaskDependencies] [ net_usestaskdependencies] 속성 너무`true`:</span><span class="sxs-lookup"><span data-stu-id="d9d0f-126">In Batch .NET, enable it on your [CloudJob][net_cloudjob] by setting its [UsesTaskDependencies][net_usestaskdependencies] property too`true`:</span></span>

```csharp
CloudJob unboundJob = batchClient.JobOperations.CreateJob( "job001",
    new PoolInformation { PoolId = "pool001" });

// IMPORTANT: This is REQUIRED for using task dependencies.
unboundJob.UsesTaskDependencies = true;
```

<span data-ttu-id="d9d0f-127">코드 조각 앞 hello, "batchClient" hello의 인스턴스는 [BatchClient] [ net_batchclient] 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="d9d0f-127">In hello preceding code snippet, "batchClient" is an instance of hello [BatchClient][net_batchclient] class.</span></span>

## <a name="create-dependent-tasks"></a><span data-ttu-id="d9d0f-128">종속성 태스크 만들기</span><span class="sxs-lookup"><span data-stu-id="d9d0f-128">Create dependent tasks</span></span>
<span data-ttu-id="d9d0f-129">하나 이상의 부모 작업의 hello 완료에 종속 된 작업 toocreate 작업 "에 따라 달라 집니다" hello를 hello 하는 다른 작업을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9d0f-129">toocreate a task that depends on hello completion of one or more parent tasks, you can specify that hello task "depends on" hello other tasks.</span></span> <span data-ttu-id="d9d0f-130">일괄 처리.net에서 구성 hello [CloudTask][net_cloudtask].[ DependsOn] [ net_dependson] hello의 인스턴스로 속성 [TaskDependencies] [ net_taskdependencies] 클래스:</span><span class="sxs-lookup"><span data-stu-id="d9d0f-130">In Batch .NET, configure hello [CloudTask][net_cloudtask].[DependsOn][net_dependson] property with an instance of hello [TaskDependencies][net_taskdependencies] class:</span></span>

```csharp
// Task 'Flowers' depends on completion of both 'Rain' and 'Sun'
// before it is run.
new CloudTask("Flowers", "cmd.exe /c echo Flowers")
{
    DependsOn = TaskDependencies.OnIds("Rain", "Sun")
},
```

<span data-ttu-id="d9d0f-131">이 코드 조각은 태스크 ID가 "Flowers"인 종속 태스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d9d0f-131">This code snippet creates a dependent task with task ID "Flowers".</span></span> <span data-ttu-id="d9d0f-132">hello "꽃" 작업 작업에 따라 다름 "비"와 "일요일"입니다.</span><span class="sxs-lookup"><span data-stu-id="d9d0f-132">hello "Flowers" task depends on tasks "Rain" and "Sun".</span></span> <span data-ttu-id="d9d0f-133">작업 "꽃" 작업 "비"와 "Sun"가 성공적으로 완료 한 후에 계산 노드에서 예약 된 toorun 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9d0f-133">Task "Flowers" will be scheduled toorun on a compute node only after tasks "Rain" and "Sun" have completed successfully.</span></span>

> [!NOTE]
> <span data-ttu-id="d9d0f-134">작업은 toobe hello에 있으면 성공적으로 완료 된 것으로 간주 됩니다 **완료** 상태 및 해당 **종료 코드** 은 `0`합니다.</span><span class="sxs-lookup"><span data-stu-id="d9d0f-134">A task is considered toobe completed successfully when it is in hello **completed** state and its **exit code** is `0`.</span></span> <span data-ttu-id="d9d0f-135">즉 일괄 처리.NET에서는 [CloudTask][net_cloudtask].[ 상태] [ net_taskstate] 속성 값이 `Completed` CloudTask의 hello 및 [TaskExecutionInformation][net_taskexecutioninformation].[ ExitCode] [ net_exitcode] 속성 값은 `0`합니다.</span><span class="sxs-lookup"><span data-stu-id="d9d0f-135">In Batch .NET, this means a [CloudTask][net_cloudtask].[State][net_taskstate] property value of `Completed` and hello CloudTask's [TaskExecutionInformation][net_taskexecutioninformation].[ExitCode][net_exitcode] property value is `0`.</span></span>
> 
> 

## <a name="dependency-scenarios"></a><span data-ttu-id="d9d0f-136">종속성 시나리오</span><span class="sxs-lookup"><span data-stu-id="d9d0f-136">Dependency scenarios</span></span>
<span data-ttu-id="d9d0f-137">Azure 배치에서 사용할 수 있는 세 가지 기본 태스크 종속성 시나리오는 일대일, 일대다 및 태스크 ID 범위 종속성입니다.</span><span class="sxs-lookup"><span data-stu-id="d9d0f-137">There are three basic task dependency scenarios that you can use in Azure Batch: one-to-one, one-to-many, and task ID range dependency.</span></span> <span data-ttu-id="d9d0f-138">이들은 결합된 tooprovide 네 번째 시나리오에서는 다 대 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9d0f-138">These can be combined tooprovide a fourth scenario, many-to-many.</span></span>

| <span data-ttu-id="d9d0f-139">시나리오&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="sxs-lookup"><span data-stu-id="d9d0f-139">Scenario&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span> | <span data-ttu-id="d9d0f-140">예</span><span class="sxs-lookup"><span data-stu-id="d9d0f-140">Example</span></span> |  |
|:---:| --- | --- |
|  [<span data-ttu-id="d9d0f-141">일대일</span><span class="sxs-lookup"><span data-stu-id="d9d0f-141">One-to-one</span></span>](#one-to-one) |<span data-ttu-id="d9d0f-142">*taskB*가 *taskA*에 종속됨</span><span class="sxs-lookup"><span data-stu-id="d9d0f-142">*taskB* depends on *taskA*</span></span> <p/> <span data-ttu-id="d9d0f-143">*taskB*는 *taskA*가 성공적으로 완료될 때까지 실행하도록 예약되지 않음</span><span class="sxs-lookup"><span data-stu-id="d9d0f-143">*taskB* will not be scheduled for execution until *taskA* has completed successfully</span></span> |<span data-ttu-id="d9d0f-144">![다이어그램: 일대일 태스크 종속성][1]</span><span class="sxs-lookup"><span data-stu-id="d9d0f-144">![Diagram: one-to-one task dependency][1]</span></span> |
|  [<span data-ttu-id="d9d0f-145">일대다</span><span class="sxs-lookup"><span data-stu-id="d9d0f-145">One-to-many</span></span>](#one-to-many) |<span data-ttu-id="d9d0f-146">*taskC*는 *taskA* 및 *taskB*에 종속됨</span><span class="sxs-lookup"><span data-stu-id="d9d0f-146">*taskC* depends on both *taskA* and *taskB*</span></span> <p/> <span data-ttu-id="d9d0f-147">*taskC*는 *taskA* 및 *taskB*가 성공적으로 완료될 때까지 실행하도록 예약되지 않음</span><span class="sxs-lookup"><span data-stu-id="d9d0f-147">*taskC* will not be scheduled for execution until both *taskA* and *taskB* have completed successfully</span></span> |<span data-ttu-id="d9d0f-148">![다이어그램: 일대다 태스크 종속성][2]</span><span class="sxs-lookup"><span data-stu-id="d9d0f-148">![Diagram: one-to-many task dependency][2]</span></span> |
|  [<span data-ttu-id="d9d0f-149">태스크 ID 범위</span><span class="sxs-lookup"><span data-stu-id="d9d0f-149">Task ID range</span></span>](#task-id-range) |<span data-ttu-id="d9d0f-150">*taskD*가 태스크의 범위에 종속됨</span><span class="sxs-lookup"><span data-stu-id="d9d0f-150">*taskD* depends on a range of tasks</span></span> <p/> <span data-ttu-id="d9d0f-151">*taskD* hello 작업 Id 가진 될 때까지 실행을 위해 예약 되지 것입니다 *1* 통해 *10* 가 성공적으로 완료</span><span class="sxs-lookup"><span data-stu-id="d9d0f-151">*taskD* will not be scheduled for execution until hello tasks with IDs *1* through *10* have completed successfully</span></span> |<span data-ttu-id="d9d0f-152">![다이어그램: 태스크 ID 범위 종속성][3]</span><span class="sxs-lookup"><span data-stu-id="d9d0f-152">![Diagram: Task id range dependency][3]</span></span> |

> [!TIP]
> <span data-ttu-id="d9d0f-153">만들 수 있습니다 **다 대 다** C, D, E 및 F 각 작업 태스크 A와 B에 종속 되는 위치 등의 관계 이 값은 여기서 여러 업스트림 작업의 hello 출력에 따라 달라질 다운스트림 작업 병렬화 된 전처리 시나리오 등에서 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9d0f-153">You can create **many-to-many** relationships, such as where tasks C, D, E, and F each depend on tasks A and B. This is useful, for example, in parallelized preprocessing scenarios where your downstream tasks depend on hello output of multiple upstream tasks.</span></span>
> 
> <span data-ttu-id="d9d0f-154">이 섹션의 예제는 hello hello 부모 작업이 성공적으로 완료 된 후에 종속 태스크가 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9d0f-154">In hello examples in this section, a dependent task runs only after hello parent tasks complete successfully.</span></span> <span data-ttu-id="d9d0f-155">이 동작은 종속 작업에 대 한 hello 기본 동작에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9d0f-155">This behavior is hello default behavior for a dependent task.</span></span> <span data-ttu-id="d9d0f-156">종속 작업 종속성 동작 toooverride hello 기본 동작을 지정 하 여 부모 작업에 실패 한 후에 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9d0f-156">You can run a dependent task after a parent task fails by specifying a dependency action toooverride hello default behavior.</span></span> <span data-ttu-id="d9d0f-157">Hello 참조 [종속성 동작](#dependency-actions) 자세한 내용은 섹션.</span><span class="sxs-lookup"><span data-stu-id="d9d0f-157">See hello [Dependency actions](#dependency-actions) section for details.</span></span>

### <a name="one-to-one"></a><span data-ttu-id="d9d0f-158">일대일</span><span class="sxs-lookup"><span data-stu-id="d9d0f-158">One-to-one</span></span>
<span data-ttu-id="d9d0f-159">한 일 관계 작업 hello 하나의 부모 작업이 완료 되었는지에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="d9d0f-159">In a one-to-one relationship, a task depends on hello successful completion of one parent task.</span></span> <span data-ttu-id="d9d0f-160">toocreate hello 종속성, 작업 ID toohello 제공 [TaskDependencies][net_taskdependencies].[ OnId] [ net_onid] hello를 채울 때 정적 메서드 [DependsOn] [ net_dependson] 속성 [CloudTask] [ net_cloudtask].</span><span class="sxs-lookup"><span data-stu-id="d9d0f-160">toocreate hello dependency, provide a single task ID toohello [TaskDependencies][net_taskdependencies].[OnId][net_onid] static method when you populate hello [DependsOn][net_dependson] property of [CloudTask][net_cloudtask].</span></span>

```csharp
// Task 'taskA' doesn't depend on any other tasks
new CloudTask("taskA", "cmd.exe /c echo taskA"),

// Task 'taskB' depends on completion of task 'taskA'
new CloudTask("taskB", "cmd.exe /c echo taskB")
{
    DependsOn = TaskDependencies.OnId("taskA")
},
```

### <a name="one-to-many"></a><span data-ttu-id="d9d0f-161">일대다</span><span class="sxs-lookup"><span data-stu-id="d9d0f-161">One-to-many</span></span>
<span data-ttu-id="d9d0f-162">1 대 다 관계 작업 여러 부모 작업의 hello 완료에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="d9d0f-162">In a one-to-many relationship, a task depends on hello completion of multiple parent tasks.</span></span> <span data-ttu-id="d9d0f-163">toocreate hello 종속성, 작업 Id toohello의 컬렉션을 제공 [TaskDependencies][net_taskdependencies].[ OnIds] [ net_onids] hello를 채울 때 정적 메서드 [DependsOn] [ net_dependson] 속성 [CloudTask] [ net_cloudtask].</span><span class="sxs-lookup"><span data-stu-id="d9d0f-163">toocreate hello dependency, provide a collection of task IDs toohello [TaskDependencies][net_taskdependencies].[OnIds][net_onids] static method when you populate hello [DependsOn][net_dependson] property of [CloudTask][net_cloudtask].</span></span>

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

### <a name="task-id-range"></a><span data-ttu-id="d9d0f-164">태스크 ID 범위</span><span class="sxs-lookup"><span data-stu-id="d9d0f-164">Task ID range</span></span>
<span data-ttu-id="d9d0f-165">부모 작업의 범위에 대 한 종속성, 작업 Id 범위 내에 작업의 hello hello 완료에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="d9d0f-165">In a dependency on a range of parent tasks, a task depends on hello hello completion of tasks whose IDs lie within a range.</span></span>
<span data-ttu-id="d9d0f-166">toocreate hello 종속성 먼저 hello를 제공 하 고 마지막 범위 toohello hello에에서 ÷ Id [TaskDependencies][net_taskdependencies].[ OnIdRange] [ net_onidrange] hello를 채울 때 정적 메서드 [DependsOn] [ net_dependson] 속성 [CloudTask] [net_cloudtask].</span><span class="sxs-lookup"><span data-stu-id="d9d0f-166">toocreate hello dependency, provide hello first and last task IDs in hello range toohello [TaskDependencies][net_taskdependencies].[OnIdRange][net_onidrange] static method when you populate hello [DependsOn][net_dependson] property of [CloudTask][net_cloudtask].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d9d0f-167">종속성에 대 한 작업 ID 범위를 사용 하는 경우 hello hello 범위 내에 작업 Id *해야* 정수 값의 문자열 표현 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9d0f-167">When you use task ID ranges for your dependencies, hello task IDs in hello range *must* be string representations of integer values.</span></span>
> 
> <span data-ttu-id="d9d0f-168">Hello 범위에서 모든 작업이 성공적으로 완료 하거나도 매핑된 tooa 종속성 작업은 오류와 함께 완료 하 여 hello 종속성을 충족 해야**Satisfy**합니다.</span><span class="sxs-lookup"><span data-stu-id="d9d0f-168">Every task in hello range must satisfy hello dependency, either by completing successfully or by completing with a failure that’s mapped tooa dependency action set too**Satisfy**.</span></span> <span data-ttu-id="d9d0f-169">Hello 참조 [종속성 동작](#dependency-actions) 자세한 내용은 섹션.</span><span class="sxs-lookup"><span data-stu-id="d9d0f-169">See hello [Dependency actions](#dependency-actions) section for details.</span></span>
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
    // toouse a range of tasks, their ids must be integer values.
    // Note that we pass integers as parameters tooTaskIdRange,
    // but their ids (above) are string representations of hello ids.
    DependsOn = TaskDependencies.OnIdRange(1, 3)
},
```

## <a name="dependency-actions"></a><span data-ttu-id="d9d0f-170">종속성 작업</span><span class="sxs-lookup"><span data-stu-id="d9d0f-170">Dependency actions</span></span>

<span data-ttu-id="d9d0f-171">기본적으로 상위 태스크가 성공적으로 완료된 후에만 (일련의) 종속 태스크가 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9d0f-171">By default, a dependent task or set of tasks runs only after a parent task has completed successfully.</span></span> <span data-ttu-id="d9d0f-172">일부 시나리오에서는 hello 부모 작업에 실패 하는 경우에 toorun 종속 작업 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9d0f-172">In some scenarios, you may want toorun dependent tasks even if hello parent task fails.</span></span> <span data-ttu-id="d9d0f-173">종속성 동작을 지정 하 여 hello 기본 동작을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9d0f-173">You can override hello default behavior by specifying a dependency action.</span></span> <span data-ttu-id="d9d0f-174">종속 작업을 종속 작업 hello 부모 작업의 hello 성공 또는 실패에 따라, 적격 toorun 인지를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9d0f-174">A dependency action specifies whether a dependent task is eligible toorun, based on hello success or failure of hello parent task.</span></span> 

<span data-ttu-id="d9d0f-175">예를 들어 종속 작업 데이터 hello hello 업스트림 작업 완료를 대기 중입니다.</span><span class="sxs-lookup"><span data-stu-id="d9d0f-175">For example, suppose that a dependent task is awaiting data from hello completion of hello upstream task.</span></span> <span data-ttu-id="d9d0f-176">Hello 업스트림 작업에 실패 하면 hello 종속 작업은 오래 된 데이터를 사용 하 여 수 toorun를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9d0f-176">If hello upstream task fails, hello dependent task may still be able toorun using older data.</span></span> <span data-ttu-id="d9d0f-177">이 경우 종속성 동작이 해당 hello 종속 작업은 적격 toorun hello 부모 작업의 hello 실패 불구 하 고 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9d0f-177">In this case, a dependency action can specify that hello dependent task is eligible toorun despite hello failure of hello parent task.</span></span>

<span data-ttu-id="d9d0f-178">종속성 동작이 hello 부모 작업에 대 한 종료 조건을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9d0f-178">A dependency action is based on an exit condition for hello parent task.</span></span> <span data-ttu-id="d9d0f-179">Hello 종료 조건을; 다음 중 하나에 대 한 종속성 동작을 지정할 수 있습니다. .NET 참조 hello [ExitConditions] [ net_exitconditions] 세부 정보에 대 한 클래스:</span><span class="sxs-lookup"><span data-stu-id="d9d0f-179">You can specify a dependency action for any of hello following exit conditions; for .NET, see hello [ExitConditions][net_exitconditions] class for details:</span></span>

- <span data-ttu-id="d9d0f-180">전처리 오류가 발생할 때</span><span class="sxs-lookup"><span data-stu-id="d9d0f-180">When a pre-processing error occurs.</span></span>
- <span data-ttu-id="d9d0f-181">파일을 업로드 오류가 발생할 때</span><span class="sxs-lookup"><span data-stu-id="d9d0f-181">When a file upload error occurs.</span></span> <span data-ttu-id="d9d0f-182">Hello 작업을 통해 지정 된 종료 코드로 종료 **exitCodes** 또는 **exitCodeRanges**, 다음 파일 업로드 오류, 종료 코드 hello 우선적으로 지정 된 hello 작업에서 발생 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9d0f-182">If hello task exits with an exit code that was specified via **exitCodes** or **exitCodeRanges**, and then encounters a file upload error, hello action specified by hello exit code takes precedence.</span></span>
- <span data-ttu-id="d9d0f-183">Hello 작업 hello에 정의 된 종료 코드로 종료 될 때 **ExitCodes** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="d9d0f-183">When hello task exits with an exit code defined by hello **ExitCodes** property.</span></span>
- <span data-ttu-id="d9d0f-184">Hello 작업 hello로 지정 된 범위 내에 포함 되는 종료 코드로 종료 될 때 **ExitCodeRanges** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="d9d0f-184">When hello task exits with an exit code that falls within a range specified by hello **ExitCodeRanges** property.</span></span>
- <span data-ttu-id="d9d0f-185">기본적으로, hello 작업에 정의 되지 않은 종료 코드로 종료 되 면 hello **ExitCodes** 또는 **ExitCodeRanges**, 전처리 오류 및 hello 종료 될 hello 작업 또는 **PreProcessingError**  속성을 설정 하지 않으면 또는 작업 실패 하 고 파일 업로드 오류 및 hello 경우 hello **FileUploadError** 속성이 설정 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="d9d0f-185">hello default case, if hello task exits with an exit code not defined by **ExitCodes** or **ExitCodeRanges**, or if hello task exits with a pre-processing error and hello **PreProcessingError** property is not set, or if hello task fails with a file upload error and hello **FileUploadError** property is not set.</span></span> 

<span data-ttu-id="d9d0f-186">.net에서 집합 hello 종속성 동작이 toospecify [ExitOptions][net_exitoptions].[ 종속성] [ net_dependencyaction] hello 종료 조건에 대 한 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="d9d0f-186">toospecify a dependency action in .NET, set hello [ExitOptions][net_exitoptions].[DependencyAction][net_dependencyaction] property for hello exit condition.</span></span> <span data-ttu-id="d9d0f-187">hello **종속성** 속성은 두 값 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9d0f-187">hello **DependencyAction** property takes one of two values:</span></span>

- <span data-ttu-id="d9d0f-188">설정 hello **종속성** 속성 너무**Satisfy** hello 부모 작업은 지정 된 오류 종료 되 면 종속 작업은 적격 toorun 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d9d0f-188">Setting hello **DependencyAction** property too**Satisfy** indicates that dependent tasks are eligible toorun if hello parent task exits with a specified error.</span></span>
- <span data-ttu-id="d9d0f-189">설정 hello **종속성** 속성 너무**블록** 종속 작업 적격 toorun 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d9d0f-189">Setting hello **DependencyAction** property too**Block** indicates that dependent tasks are not eligible toorun.</span></span>

<span data-ttu-id="d9d0f-190">hello에 대 한 기본 설정은 hello **종속성** 속성은 **Satisfy** 종료 코드 0에 대 한 및 **블록** 다른 모든 종료 조건에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9d0f-190">hello default setting for hello **DependencyAction** property is **Satisfy** for exit code 0, and **Block** for all other exit conditions.</span></span>

<span data-ttu-id="d9d0f-191">hello 다음 코드 조각 설정 hello **종속성** 부모 작업에 대 한 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="d9d0f-191">hello following code snippet sets hello **DependencyAction** property for a parent task.</span></span> <span data-ttu-id="d9d0f-192">전처리 오류로 hello 부모 태스크가 종료 또는 hello로 지정 된 오류 코드를 환영 종속 작업이 차단 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9d0f-192">If hello parent task exits with a pre-processing error, or with hello specified error codes, hello dependent task is blocked.</span></span> <span data-ttu-id="d9d0f-193">종속 작업 hello hello 부모 작업 다른 0이 아닌 오류와 함께 종료 경우 적격 toorun입니다.</span><span class="sxs-lookup"><span data-stu-id="d9d0f-193">If hello parent task exits with any other non-zero error, hello dependent task is eligible toorun.</span></span>

```csharp
// Task A is hello parent task.
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
        // If task A exits with hello specified error codes, block any downstream tasks (in this example, task B).
        ExitCodes = new List<ExitCodeMapping>
        {
            new ExitCodeMapping(10, new ExitOptions() { DependencyAction = DependencyAction.Block }),
            new ExitCodeMapping(20, new ExitOptions() { DependencyAction = DependencyAction.Block })
        },
        // If task A succeeds or fails with any other error, any downstream tasks become eligible toorun 
        // (in this example, task B).
        Default = new ExitOptions
        {
            DependencyAction = DependencyAction.Satisfy
        }
    }
},
// Task B depends on task A. Whether it becomes eligible toorun depends on how task A exits.
new CloudTask("B", "cmd.exe /c echo B")
{
    DependsOn = TaskDependencies.OnId("A")
},
```

## <a name="code-sample"></a><span data-ttu-id="d9d0f-194">코드 샘플</span><span class="sxs-lookup"><span data-stu-id="d9d0f-194">Code sample</span></span>
<span data-ttu-id="d9d0f-195">hello [TaskDependencies] [ github_taskdependencies] 샘플 프로젝트를 사용 하면 hello 중 하나인 [Azure 배치 코드 샘플] [ github_samples] GitHub에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9d0f-195">hello [TaskDependencies][github_taskdependencies] sample project is one of hello [Azure Batch code samples][github_samples] on GitHub.</span></span> <span data-ttu-id="d9d0f-196">이 Visual Studio 솔루션은 다음 사항을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d9d0f-196">This Visual Studio solution demonstrates:</span></span>

- <span data-ttu-id="d9d0f-197">Tooenable 작업에 대 한 종속성을 작업 하는 방법</span><span class="sxs-lookup"><span data-stu-id="d9d0f-197">How tooenable task dependency on a job</span></span>
- <span data-ttu-id="d9d0f-198">방식과 toocreate 작업 하는 다른 작업에 종속</span><span class="sxs-lookup"><span data-stu-id="d9d0f-198">How toocreate tasks that depend on other tasks</span></span>
- <span data-ttu-id="d9d0f-199">어떻게 tooexecute 작업에서 계산 노드의 풀입니다.</span><span class="sxs-lookup"><span data-stu-id="d9d0f-199">How tooexecute those tasks on a pool of compute nodes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d9d0f-200">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d9d0f-200">Next steps</span></span>
### <a name="application-deployment"></a><span data-ttu-id="d9d0f-201">응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="d9d0f-201">Application deployment</span></span>
<span data-ttu-id="d9d0f-202">hello [응용 프로그램 패키지](batch-application-packages.md) 쉽게 tooboth 배포 및 버전 hello 응용 프로그램에서 작업을 실행 하는 계산 노드 일괄 처리의 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9d0f-202">hello [application packages](batch-application-packages.md) feature of Batch provides an easy way tooboth deploy and version hello applications that your tasks execute on compute nodes.</span></span>

### <a name="installing-applications-and-staging-data"></a><span data-ttu-id="d9d0f-203">응용 프로그램 설치 및 데이터 준비</span><span class="sxs-lookup"><span data-stu-id="d9d0f-203">Installing applications and staging data</span></span>
<span data-ttu-id="d9d0f-204">참조 [응용 프로그램을 설치 하 고 일괄 처리에 대 한 데이터를 준비 하는 계산 노드] [ forum_post] hello Azure 배치 포럼 toorun 작업 노드를 준비 하기 위한 방법에 대 한 개요입니다.</span><span class="sxs-lookup"><span data-stu-id="d9d0f-204">See [Installing applications and staging data on Batch compute nodes][forum_post] in hello Azure Batch forum for an overview of methods for preparing your nodes toorun tasks.</span></span> <span data-ttu-id="d9d0f-205">이 게시물은 hello 다양 한 방법 toocopy 응용 프로그램에 좋은 입문서 hello Azure 일괄 처리 팀 멤버 중 하나에 의해 작성 작업 입력된 데이터를 다른 파일 tooyour 계산 노드.</span><span class="sxs-lookup"><span data-stu-id="d9d0f-205">Written by one of hello Azure Batch team members, this post is a good primer on hello different ways toocopy applications, task input data, and other files tooyour compute nodes.</span></span>

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

[1]: ./media/batch-task-dependency/01_one_to_one.png "다이어그램: 일대일 종속성"
[2]: ./media/batch-task-dependency/02_one_to_many.png "다이어그램: 일대다 종속성"
[3]: ./media/batch-task-dependency/03_task_id_range.png "다이어그램: 태스크 ID 범위 종속성"

---
title: "계산 노드에서 작업을 준비하고 완료하는 태스크 만들기 - Azure Batch | Microsoft Docs"
description: "작업 수준 준비 태스크를 사용하여 Azure Batch 계산 노드로의 데이터 전송을 최소화하고 작업 완료 시 태스크를 해제하여 노드를 정리합니다."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 63d9d4f1-8521-4bbb-b95a-c4cad73692d3
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6a2525c02ce7bd3969469d2e28a5fccc948f89b1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="run-job-preparation-and-job-release-tasks-on-batch-compute-nodes"></a><span data-ttu-id="9c2de-103">Batch 계산 노드에서 작업 준비 및 작업 릴리스 태스크 실행</span><span class="sxs-lookup"><span data-stu-id="9c2de-103">Run job preparation and job release tasks on Batch compute nodes</span></span>

 <span data-ttu-id="9c2de-104">가끔씩 Azure Batch 작업에는 실행되기 전에 특정 형식으로 구성된 설정과 해당 작업이 완료된 이후의 사후 작업 유지 관리가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9c2de-104">An Azure Batch job often requires some form of setup before its tasks are executed, and post-job maintenance when its tasks are completed.</span></span> <span data-ttu-id="9c2de-105">즉 계산 노드에 공통 작업 입력 데이터를 다운로드하거나 해당 작업이 완료된 후 작업 출력 데이터를 Azure Storage에 업로드해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c2de-105">You might need to download common task input data to your compute nodes, or upload task output data to Azure Storage after the job completes.</span></span> <span data-ttu-id="9c2de-106">**작업 준비** 및 **작업 해제**를 사용하면 이러한 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c2de-106">You can use **job preparation** and **job release** tasks to perform these operations.</span></span>

## <a name="what-are-job-preparation-and-release-tasks"></a><span data-ttu-id="9c2de-107">작업 준비 및 해제 태스크에 대한 정의</span><span class="sxs-lookup"><span data-stu-id="9c2de-107">What are job preparation and release tasks?</span></span>
<span data-ttu-id="9c2de-108">작업 태스크가 실행되기 전에 하나 이상의 태스크를 실행하도록 예약된 모든 계산 노드에서 작업 준비 태스크가 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c2de-108">Before a job's tasks run, the job preparation task runs on all compute nodes scheduled to run at least one task.</span></span> <span data-ttu-id="9c2de-109">작업이 완료되면 하나 이상의 태스크를 실행한 풀의 각 노드에서 작업 릴리스 태스크가 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c2de-109">Once the job is completed, the job release task runs on each node in the pool that executed at least one task.</span></span> <span data-ttu-id="9c2de-110">일반 Batch 태스크처럼 작업 준비 또는 해제 태스크가 실행될 때 호출되는 명령줄을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c2de-110">As with normal Batch tasks, you can specify a command line to be invoked when a job preparation or release task is run.</span></span>

<span data-ttu-id="9c2de-111">작업 준비 및 해제 태스크는 파일([리소스 파일][net_job_prep_resourcefiles]) 다운로드, 관리자 권한 실행, 사용자 지정 환경 변수, 최대 실행 기간, 재시도 횟수 및 파일 보존 시간과 같은 익숙한 Batch 태스크 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9c2de-111">Job preparation and release tasks offer familiar Batch task features such as file download ([resource files][net_job_prep_resourcefiles]), elevated execution, custom environment variables, maximum execution duration, retry count, and file retention time.</span></span>

<span data-ttu-id="9c2de-112">다음 섹션에서는 [Batch .NET][api_net] 라이브러리에 있는 [JobPreparationTask][net_job_prep]와 [JobReleaseTask][net_job_release] 클래스를 사용하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="9c2de-112">In the following sections, you'll learn how to use the [JobPreparationTask][net_job_prep] and [JobReleaseTask][net_job_release] classes found in the [Batch .NET][api_net] library.</span></span>

> [!TIP]
> <span data-ttu-id="9c2de-113">계산 노드 풀이 작업 실행 간에 지속되고 여러 작업에서 사용되는 "공유 풀" 환경에서는 작업 준비 및 해제 태스크가 특히 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="9c2de-113">Job preparation and release tasks are especially helpful in "shared pool" environments, in which a pool of compute nodes persists between job runs and is used by many jobs.</span></span>
> 
> 

## <a name="when-to-use-job-preparation-and-release-tasks"></a><span data-ttu-id="9c2de-114">작업 준비 및 해제 태스크를 사용하는 시점</span><span class="sxs-lookup"><span data-stu-id="9c2de-114">When to use job preparation and release tasks</span></span>
<span data-ttu-id="9c2de-115">작업 준비 및 작업 해제 태스크가 적합한 경우는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9c2de-115">Job preparation and job release tasks are a good fit for the following situations:</span></span>

<span data-ttu-id="9c2de-116">**공통 태스크 데이터 다운로드**</span><span class="sxs-lookup"><span data-stu-id="9c2de-116">**Download common task data**</span></span>

<span data-ttu-id="9c2de-117">배치 작업은 종종 작업의 태스크에 대한 입력으로 데이터의 공통 집합이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9c2de-117">Batch jobs often require a common set of data as input for the job's tasks.</span></span> <span data-ttu-id="9c2de-118">예를 들어 일별 위험 분석 계산에서 시장 데이터는 작업 특정적이지만 작업의 모든 태스크에는 공통적입니다.</span><span class="sxs-lookup"><span data-stu-id="9c2de-118">For example, in daily risk analysis calculations, market data is job-specific, yet common to all tasks in the job.</span></span> <span data-ttu-id="9c2de-119">종종 수 기가바이트 크기인 시장 데이터는 각각의 계산 노드에 한 번만 다운로드되어 노드에서 실행하는 모든 태스크에서 사용할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c2de-119">This market data, often several gigabytes in size, should be downloaded to each compute node only once so that any task that runs on the node can use it.</span></span> <span data-ttu-id="9c2de-120">**작업 준비 태스크** 를 사용하여 작업의 다른 태스크를 실행하기 전에 각 노드에 이 데이터를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="9c2de-120">Use a **job preparation task** to download this data to each node before the execution of the job's other tasks.</span></span>

<span data-ttu-id="9c2de-121">**작업 및 태스크 출력 삭제**</span><span class="sxs-lookup"><span data-stu-id="9c2de-121">**Delete job and task output**</span></span>

<span data-ttu-id="9c2de-122">작업 간에 풀의 계산 노드 서비스를 해제하지 않는 "공유 풀" 환경에서 실행 간의 작업 데이터를 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c2de-122">In a "shared pool" environment, where a pool's compute nodes are not decommissioned between jobs, you may need to delete job data between runs.</span></span> <span data-ttu-id="9c2de-123">노드의 디스크 공간을 절약하거나 조직의 보안 정책을 충족시킬 필요도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c2de-123">You might need to conserve disk space on the nodes, or satisfy your organization's security policies.</span></span> <span data-ttu-id="9c2de-124">**작업 해제 태스크** 를 사용하여 작업 준비 태스크에서 다운로드했거나 태스크를 실행하는 동안 생성한 데이터를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="9c2de-124">Use a **job release task** to delete data that was downloaded by a job preparation task, or generated during task execution.</span></span>

<span data-ttu-id="9c2de-125">**로그 보존**</span><span class="sxs-lookup"><span data-stu-id="9c2de-125">**Log retention**</span></span>

<span data-ttu-id="9c2de-126">태스크가 생성한 로그 파일의 복사본을 유지하거나 실패한 응용 프로그램에서 생성될 수 있는 덤프 파일의 작동을 중단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c2de-126">You might want to keep a copy of log files that your tasks generate, or perhaps crash dump files that can be generated by failed applications.</span></span> <span data-ttu-id="9c2de-127">이런 경우 **작업 릴리스 태스크**를 사용하여 [Azure Storage][azure_storage] 계정에 이 데이터를 압축하고 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="9c2de-127">Use a **job release task** in such cases to compress and upload this data to an [Azure Storage][azure_storage] account.</span></span>

> [!TIP]
> <span data-ttu-id="9c2de-128">로그 및 기타 작업과 태스크 출력 데이터를 유지하는 다른 방법은 [Azure Batch File Conventions](batch-task-output.md) 라이브러리를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9c2de-128">Another way to persist logs and other job and task output data is to use the [Azure Batch File Conventions](batch-task-output.md) library.</span></span>
> 
> 

## <a name="job-preparation-task"></a><span data-ttu-id="9c2de-129">작업 준비 태스크</span><span class="sxs-lookup"><span data-stu-id="9c2de-129">Job preparation task</span></span>
<span data-ttu-id="9c2de-130">작업의 태스크를 실행하기 전에 Batch에서는 작업을 실행하도록 예약된 각 계산 노드에서 작업 준비 태스크가 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c2de-130">Before execution of a job's tasks, Batch executes the job preparation task on each compute node that is scheduled to run a task.</span></span> <span data-ttu-id="9c2de-131">기본적으로 Batch 서비스는 노드에서 실행하도록 예약된 태스크를 실행하기 전에 작업 준비 태스크가 완료되기를 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="9c2de-131">By default, the Batch service waits for the job preparation task to be completed before running the tasks scheduled to execute on the node.</span></span> <span data-ttu-id="9c2de-132">그러나 서비스를 대기하지 않도록 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c2de-132">However, you can configure the service not to wait.</span></span> <span data-ttu-id="9c2de-133">노드가 다시 시작되면 작업 준비 태스크도 다시 실행되지만, 이 동작을 사용하지 않도록 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c2de-133">If the node restarts, the job preparation task runs again, but you can also disable this behavior.</span></span>

<span data-ttu-id="9c2de-134">작업 준비 태스크는 태스크를 실행하도록 예약된 노드에서만 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c2de-134">The job preparation task is executed only on nodes that are scheduled to run a task.</span></span> <span data-ttu-id="9c2de-135">노드에 태스크를 할당하지 않은 경우 준비 태스크가 불필요하게 실행되지 않도록 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="9c2de-135">This prevents the unnecessary execution of a preparation task in case a node is not assigned a task.</span></span> <span data-ttu-id="9c2de-136">이는 작업에 대한 태스크 수가 풀의 노드 수보다 작은 경우에 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c2de-136">This can occur when the number of tasks for a job is less than the number of nodes in a pool.</span></span> <span data-ttu-id="9c2de-137">이 방식은 [동시 태스크 실행](batch-parallel-node-tasks.md) 을 활성화할 때도 적용되며, 이는 태스크 개수가 가능한 총 동시 태스크 개수보다 작으면 노드 일부를 유휴 상태로 남겨둡니다.</span><span class="sxs-lookup"><span data-stu-id="9c2de-137">It also applies when [concurrent task execution](batch-parallel-node-tasks.md) is enabled, which leaves some nodes idle if the task count is lower than the total possible concurrent tasks.</span></span> <span data-ttu-id="9c2de-138">유휴 노드에서 작업 준비 태스크를 실행하지 않으면 데이터 전송 요금에 적은 비용을 투자할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c2de-138">By not running the job preparation task on idle nodes, you can spend less money on data transfer charges.</span></span>

> [!NOTE]
> <span data-ttu-id="9c2de-139">JobPreparationTask는 각 작업을 시작할 때 실행되지만 StartTask는 먼저 계산 노드를 풀과 조인하거나 다시 시작할 때만 실행된다는 점에서 [JobPreparationTask][net_job_prep_cloudjob]은 [CloudPool.StartTask][pool_starttask]와 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="9c2de-139">[JobPreparationTask][net_job_prep_cloudjob] differs from [CloudPool.StartTask][pool_starttask] in that JobPreparationTask executes at the start of each job, whereas StartTask executes only when a compute node first joins a pool or restarts.</span></span>
> 
> 

## <a name="job-release-task"></a><span data-ttu-id="9c2de-140">작업 해제 태스크</span><span class="sxs-lookup"><span data-stu-id="9c2de-140">Job release task</span></span>
<span data-ttu-id="9c2de-141">작업이 완료로 표시되면 하나 이상의 태스크를 실행한 풀의 각 노드에서 작업 릴리스 태스크가 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c2de-141">Once a job is marked as completed, the job release task is executed on each node in the pool that executed at least one task.</span></span> <span data-ttu-id="9c2de-142">종료 요청을 발행하여 작업을 완료로 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="9c2de-142">You mark a job as completed by issuing a terminate request.</span></span> <span data-ttu-id="9c2de-143">그런 다음 Batch 서비스는 작업 상태를 *terminating*으로 설정하며, 작업과 연관된 모든 활성 또는 실행 중인 태스크를 종료하고, 작업 해제 태스크를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9c2de-143">The Batch service then sets the job state to *terminating*, terminates any active or running tasks associated with the job, and runs the job release task.</span></span> <span data-ttu-id="9c2de-144">작업은 *완료* 상태로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="9c2de-144">The job then moves to the *completed* state.</span></span>

> [!NOTE]
> <span data-ttu-id="9c2de-145">또한 작업 삭제는 작업 릴리스 태스크를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9c2de-145">Job deletion also executes the job release task.</span></span> <span data-ttu-id="9c2de-146">그러나 작업이 이미 종료되었고 나중에 삭제되는 경우에는 해제 태스크가 다시 실행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9c2de-146">However, if a job has already been terminated, the release task is not run a second time if the job is later deleted.</span></span>
> 
> 

## <a name="job-prep-and-release-tasks-with-batch-net"></a><span data-ttu-id="9c2de-147">배치 .NET을 사용한 작업 준비 및 릴리스 태스크</span><span class="sxs-lookup"><span data-stu-id="9c2de-147">Job prep and release tasks with Batch .NET</span></span>
<span data-ttu-id="9c2de-148">작업 준비 태스크를 사용하려면 [JobPreparationTask][net_job_prep] 개체를 작업의 [CloudJob.JobPreparationTask][net_job_prep_cloudjob] 속성에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="9c2de-148">To use a job preparation task, assign a [JobPreparationTask][net_job_prep] object to your job's [CloudJob.JobPreparationTask][net_job_prep_cloudjob] property.</span></span> <span data-ttu-id="9c2de-149">마찬가지로 [JobReleaseTask][net_job_release]를 초기화하고 작업의 [CloudJob.JobReleaseTask][net_job_prep_cloudjob] 속성을 할당하여 작업의 릴리스 태스크를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9c2de-149">Similarly, initialize a [JobReleaseTask][net_job_release] and assign it to your job's [CloudJob.JobReleaseTask][net_job_prep_cloudjob] property to set the job's release task.</span></span>

<span data-ttu-id="9c2de-150">이 코드 조각에서 `myBatchClient`는 완전히 [BatchClient][net_batch_client]의 인스턴스이고 `myPool`은 Batch 계정에 있는 기존 풀입니다.</span><span class="sxs-lookup"><span data-stu-id="9c2de-150">In this code snippet, `myBatchClient` is an instance of [BatchClient][net_batch_client], and `myPool` is an existing pool within the Batch account.</span></span>

```csharp
// Create the CloudJob for CloudPool "myPool"
CloudJob myJob =
    myBatchClient.JobOperations.CreateJob(
        "JobPrepReleaseSampleJob",
        new PoolInformation() { PoolId = "myPool" });

// Specify the command lines for the job preparation and release tasks
string jobPrepCmdLine =
    "cmd /c echo %AZ_BATCH_NODE_ID% > %AZ_BATCH_NODE_SHARED_DIR%\\shared_file.txt";
string jobReleaseCmdLine =
    "cmd /c del %AZ_BATCH_NODE_SHARED_DIR%\\shared_file.txt";

// Assign the job preparation task to the job
myJob.JobPreparationTask =
    new JobPreparationTask { CommandLine = jobPrepCmdLine };

// Assign the job release task to the job
myJob.JobReleaseTask =
    new JobPreparationTask { CommandLine = jobReleaseCmdLine };

await myJob.CommitAsync();
```

<span data-ttu-id="9c2de-151">위에서 설명했듯이 작업이 종료되거나 삭제될 때 해제 태스크가 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c2de-151">As mentioned earlier, the release task is executed when a job is terminated or deleted.</span></span> <span data-ttu-id="9c2de-152">[JobOperations.TerminateJobAsync][net_job_terminate]를 통해 작업을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="9c2de-152">Terminate a job with [JobOperations.TerminateJobAsync][net_job_terminate].</span></span> <span data-ttu-id="9c2de-153">[JobOperations.DeleteJobAsync][net_job_delete]를 통해 작업을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="9c2de-153">Delete a job with [JobOperations.DeleteJobAsync][net_job_delete].</span></span> <span data-ttu-id="9c2de-154">일반적으로 작업의 태스크들이 완료되거나 정의한 시간 제한에 도달했을 때 작업을 종료하거나 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="9c2de-154">You typically terminate or delete a job when its tasks are completed, or when a timeout that you've defined has been reached.</span></span>

```csharp
// Terminate the job to mark it as Completed; this will initiate the
// Job Release Task on any node that executed job tasks. Note that the
// Job Release Task is also executed when a job is deleted, thus you
// need not call Terminate if you typically delete jobs after task completion.
await myBatchClient.JobOperations.TerminateJobAsy("JobPrepReleaseSampleJob");
```

## <a name="code-sample-on-github"></a><span data-ttu-id="9c2de-155">GitHub의 코드 샘플</span><span class="sxs-lookup"><span data-stu-id="9c2de-155">Code sample on GitHub</span></span>
<span data-ttu-id="9c2de-156">작동 중인 작업 준비 및 해제 태스크를 보려면 GitHub의 [JobPrepRelease][job_prep_release_sample] 샘플 프로젝트를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9c2de-156">To see job preparation and release tasks in action, check out the [JobPrepRelease][job_prep_release_sample] sample project on GitHub.</span></span> <span data-ttu-id="9c2de-157">이 콘솔 응용 프로그램은 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9c2de-157">This console application does the following:</span></span>

1. <span data-ttu-id="9c2de-158">"small" 노드가 두 개인 풀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9c2de-158">Creates a pool with two "small" nodes.</span></span>
2. <span data-ttu-id="9c2de-159">작업 준비, 릴리스 및 표준 태스크를 사용하여 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9c2de-159">Creates a job with job preparation, release, and standard tasks.</span></span>
3. <span data-ttu-id="9c2de-160">먼저 노드 "공유" 디렉터리의 텍스트 파일에 노드 ID를 기록하는 작업 준비 태스크를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9c2de-160">Runs the job preparation task, which first writes the node ID to a text file in a node's "shared" directory.</span></span>
4. <span data-ttu-id="9c2de-161">동일한 텍스트 파일에 해당 태스크 ID를 기록하는 각 노드에서 태스크를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9c2de-161">Runs a task on each node that writes its task ID to the same text file.</span></span>
5. <span data-ttu-id="9c2de-162">모든 태스크가 완료되면(또는 시간 제한에 도달하면) 콘솔에 각 노드의 텍스트 파일에 있는 내용을 인쇄합니다.</span><span class="sxs-lookup"><span data-stu-id="9c2de-162">Once all tasks are completed (or the timeout is reached), prints the contents of each node's text file to the console.</span></span>
6. <span data-ttu-id="9c2de-163">작업이 완료되면 작업 릴리스 태스크를 실행하여 노드에서 파일을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="9c2de-163">When the job is completed, runs the job release task to delete the file from the node.</span></span>
7. <span data-ttu-id="9c2de-164">실행된 각 노드에 대한 작업 준비 및 릴리스 태스크의 종료 코드를 인쇄합니다.</span><span class="sxs-lookup"><span data-stu-id="9c2de-164">Prints the exit codes of the job preparation and release tasks for each node on which they executed.</span></span>
8. <span data-ttu-id="9c2de-165">실행을 일시 중지하여 작업 및/또는 풀 삭제를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9c2de-165">Pauses execution to allow confirmation of job and/or pool deletion.</span></span>

<span data-ttu-id="9c2de-166">샘플 응용 프로그램에서 출력은 다음과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="9c2de-166">Output from the sample application is similar to the following:</span></span>

```
Attempting to create pool: JobPrepReleaseSamplePool
Created pool JobPrepReleaseSamplePool with 2 small nodes
Checking for existing job JobPrepReleaseSampleJob...
Job JobPrepReleaseSampleJob not found, creating...
Submitting tasks and awaiting completion...
All tasks completed.

Contents of shared\job_prep_and_release.txt on tvm-2434664350_1-20160623t173951z:
-------------------------------------------
tvm-2434664350_1-20160623t173951z tasks:
  task001
  task004
  task005
  task006

Contents of shared\job_prep_and_release.txt on tvm-2434664350_2-20160623t173951z:
-------------------------------------------
tvm-2434664350_2-20160623t173951z tasks:
  task008
  task002
  task003
  task007

Waiting for job JobPrepReleaseSampleJob to reach state Completed
...

tvm-2434664350_1-20160623t173951z:
  Prep task exit code:    0
  Release task exit code: 0

tvm-2434664350_2-20160623t173951z:
  Prep task exit code:    0
  Release task exit code: 0

Delete job? [yes] no
yes
Delete pool? [yes] no
yes

Sample complete, hit ENTER to exit...
```

> [!NOTE]
> <span data-ttu-id="9c2de-167">새 풀에 있는 노드의 변수 생성 및 시작 시간으로 인해(일부 노드는 다른 노드 전에 태스크에 대해 준비됨) 다른 출력이 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c2de-167">Due to the variable creation and start time of nodes in a new pool (some nodes are ready for tasks before others), you may see different output.</span></span> <span data-ttu-id="9c2de-168">특히, 태스크가 신속하게 완료되기 때문에 풀의 노드 중 하나에서 작업의 태스크를 모두 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c2de-168">Specifically, because the tasks complete quickly, one of the pool's nodes may execute all of the job's tasks.</span></span> <span data-ttu-id="9c2de-169">이러한 경우 작업을 실행하지 않은 노드에는 작업 준비 및 릴리스 태스크가 존재하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9c2de-169">If this occurs, you will notice that the job prep and release tasks do not exist for the node that executed no tasks.</span></span>
> 
> 

### <a name="inspect-job-preparation-and-release-tasks-in-the-azure-portal"></a><span data-ttu-id="9c2de-170">Azure 포털에서 작업 준비 및 해제 태스크 검사</span><span class="sxs-lookup"><span data-stu-id="9c2de-170">Inspect job preparation and release tasks in the Azure portal</span></span>
<span data-ttu-id="9c2de-171">샘플 응용 프로그램을 실행할 때 [Azure 포털][portal]을 사용하면 작업 및 해당 태스크의 속성을 확인하거나 작업의 태스크에서 수정한 공유 텍스트 파일을 다운로드할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c2de-171">When you run the sample application, you can use the [Azure portal][portal] to view the properties of the job and its tasks, or even download the shared text file that is modified by the job's tasks.</span></span>

<span data-ttu-id="9c2de-172">다음은 샘플 응용 프로그램을 실행한 후에 Azure 포털에서 **준비 태스크 블레이드** 를 보여 주는 스크린샷입니다.</span><span class="sxs-lookup"><span data-stu-id="9c2de-172">The screenshot below shows the **Preparation tasks blade** in the Azure portal after a run of the sample application.</span></span> <span data-ttu-id="9c2de-173">작업이 완료되었지만 작업과 풀을 삭제하기 전에 *JobPrepReleaseSampleJob* 속성으로 이동하여 **준비 태스크** 또는 **해제 태스크**를 클릭하여 그 속성을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9c2de-173">Navigate to the *JobPrepReleaseSampleJob* properties after your tasks have completed (but before deleting your job and pool) and click **Preparation tasks** or **Release tasks** to view their properties.</span></span>

![Azure 포털에서 작업 준비 속성][1]

## <a name="next-steps"></a><span data-ttu-id="9c2de-175">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9c2de-175">Next steps</span></span>
### <a name="application-packages"></a><span data-ttu-id="9c2de-176">응용 프로그램 패키지</span><span class="sxs-lookup"><span data-stu-id="9c2de-176">Application packages</span></span>
<span data-ttu-id="9c2de-177">작업 준비 태스크 외에도 Batch의 [응용 프로그램 패키지](batch-application-packages.md) 기능을 사용하여 태스크 실행을 위한 계산 노드를 준비할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c2de-177">In addition to the job preparation task, you can also use the [application packages](batch-application-packages.md) feature of Batch to prepare compute nodes for task execution.</span></span> <span data-ttu-id="9c2de-178">이 기능은 설치 관리자를 실행하지 않아도 되는 응용 프로그램, 100개 이상의 파일을 포함하는 응용 프로그램 또는 엄격한 버전 제어를 필요로 하는 응용 프로그램을 배포하는 데 특히 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="9c2de-178">This feature is especially useful for deploying applications that do not require running an installer, applications that contain many (100+) files, or applications that require strict version control.</span></span>

### <a name="installing-applications-and-staging-data"></a><span data-ttu-id="9c2de-179">응용 프로그램 설치 및 데이터 준비</span><span class="sxs-lookup"><span data-stu-id="9c2de-179">Installing applications and staging data</span></span>
<span data-ttu-id="9c2de-180">아래의 MSDN 포럼 게시물에서는 작업을 실행하기 위해 노드를 준비하는 여러 가지 방법을 간략히 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9c2de-180">This MSDN forum post provides an overview of several methods of preparing your nodes for running tasks:</span></span>

<span data-ttu-id="9c2de-181">[Batch 계산 노드에서의 응용 프로그램 설치 및 데이터 스테이징][forum_post]</span><span class="sxs-lookup"><span data-stu-id="9c2de-181">[Installing applications and staging data on Batch compute nodes][forum_post]</span></span>

<span data-ttu-id="9c2de-182">Azure Batch 팀 멤버 중 하나에서 작성하고 응용 프로그램과 데이터를 계산 노드에 배포하는 데 사용할 수 있는 몇 가지 방법을 설명하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c2de-182">Written by one of the Azure Batch team members, it discusses several techniques that you can use to deploy applications and data to compute nodes.</span></span>

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_net_listjobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobs.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[azure_storage]: https://azure.microsoft.com/services/storage/
[portal]: https://portal.azure.com
[job_prep_release_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/JobPrepRelease
[forum_post]: https://social.msdn.microsoft.com/Forums/en-US/87b19671-1bdf-427a-972c-2af7e5ba82d9/installing-applications-and-staging-data-on-batch-compute-nodes?forum=azurebatch
[net_batch_client]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudjob]:https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_job_prep]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobpreparationtask.aspx
[net_job_prep_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobpreparationtask.aspx
[net_job_prep_resourcefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobpreparationtask.resourcefiles.aspx
[net_job_delete]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.deletejobasync.aspx
[net_job_terminate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.terminatejobasync.aspx
[net_job_release]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobreleasetask.aspx
[net_job_release_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobreleasetask.aspx
[pool_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.starttask.aspx

[net_list_certs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.certificateoperations.listcertificates.aspx
[net_list_compute_nodes]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listcomputenodes.aspx
[net_list_job_schedules]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobscheduleoperations.listjobschedules.aspx
[net_list_jobprep_status]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobpreparationandreleasetaskstatus.aspx
[net_list_jobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobs.aspx
[net_list_nodefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listnodefiles.aspx
[net_list_pools]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listpools.aspx
[net_list_schedule_jobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobscheduleoperations.listjobs.aspx
[net_list_task_files]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.listnodefiles.aspx
[net_list_tasks]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listtasks.aspx

[1]: ./media/batch-job-prep-release/portal-jobprep-01.png

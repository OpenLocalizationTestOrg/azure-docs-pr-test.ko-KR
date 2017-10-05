---
title: "다중 인스턴스 작업을 사용하여 MPI 응용 프로그램 실행 - Azure Batch | Microsoft Docs"
description: "Azure 배치에서 다중 인스턴스 작업 유형을 사용하여 MPI(메시지 전달 인터페이스) 응용 프로그램을 실행하는 방법에 대해 알아봅니다."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 83e34bd7-a027-4b1b-8314-759384719327
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: 5/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 77d12d6d48b22dfb3e7f09f273dffc11401bb15f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="use-multi-instance-tasks-to-run-message-passing-interface-mpi-applications-in-batch"></a><span data-ttu-id="d1bab-103">다중 인스턴스 작업을 사용하여 Batch에서 MPI(메시지 전달 인터페이스) 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="d1bab-103">Use multi-instance tasks to run Message Passing Interface (MPI) applications in Batch</span></span>

<span data-ttu-id="d1bab-104">다중 인스턴스 작업을 통해 여러 계산 노드에서 동시에 Azure 배치 작업을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-104">Multi-instance tasks allow you to run an Azure Batch task on multiple compute nodes simultaneously.</span></span> <span data-ttu-id="d1bab-105">이러한 작업을 통해 MPI(메시지 전달 인터페이스) 응용 프로그램과 같은 고성능 컴퓨팅 시나리오를 배치로 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-105">These tasks enable high performance computing scenarios like Message Passing Interface (MPI) applications in Batch.</span></span> <span data-ttu-id="d1bab-106">이 문서에서 [배치 .NET][api_net] 라이브러리를 사용하여 다중 인스턴스 작업을 실행하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-106">In this article, you learn how to execute multi-instance tasks using the [Batch .NET][api_net] library.</span></span>

> [!NOTE]
> <span data-ttu-id="d1bab-107">이 문서의 예제에서는 배치 .NET, MS-MPI 및 Windows 계산 노드에 집중하는 반면 여기에서 설명한 다중 인스턴스 작업 개념은 다른 플랫폼 및 기술(예를 들어 Linux 노드의 Python 및 Intel MPI)에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-107">While the examples in this article focus on Batch .NET, MS-MPI, and Windows compute nodes, the multi-instance task concepts discussed here are applicable to other platforms and technologies (Python and Intel MPI on Linux nodes, for example).</span></span>
>
>

## <a name="multi-instance-task-overview"></a><span data-ttu-id="d1bab-108">다중 인스턴스 작업 개요</span><span class="sxs-lookup"><span data-stu-id="d1bab-108">Multi-instance task overview</span></span>
<span data-ttu-id="d1bab-109">배치에서 각 태스크는 일반적으로 단일 계산 노드에서 실행됩니다. 작업에 여러 태스크를 제출하고 배치 서비스는 노드에서 실행을 위해 각 태스크를 예약합니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-109">In Batch, each task is normally executed on a single compute node--you submit multiple tasks to a job, and the Batch service schedules each task for execution on a node.</span></span> <span data-ttu-id="d1bab-110">그러나 태스크의 **다중 인스턴스 설정**을 구성하여 배치에 하나의 기본 태스크를 만들고 대신 여러 노드에서 여러 하위 태스크를 실행하도록 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-110">However, by configuring a task's **multi-instance settings**, you tell Batch to instead create one primary task and several subtasks that are then executed on multiple nodes.</span></span>

<span data-ttu-id="d1bab-111">![다중 인스턴스 작업 개요][1]</span><span class="sxs-lookup"><span data-stu-id="d1bab-111">![Multi-instance task overview][1]</span></span>

<span data-ttu-id="d1bab-112">작업에 다중 인스턴스 설정을 사용하여 태스크를 제출할 때 배치는 다중 인스턴스 태스크에 고유한 몇 가지 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-112">When you submit a task with multi-instance settings to a job, Batch performs several steps unique to multi-instance tasks:</span></span>

1. <span data-ttu-id="d1bab-113">배치 서비스는 다중 인스턴스 설정에 따라 하나의 **기본** 태스크 및 여러 개의 **하위 태스크**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-113">The Batch service creates one **primary** and several **subtasks** based on the multi-instance settings.</span></span> <span data-ttu-id="d1bab-114">작업의 총 수(주 및 모든 하위 작업)는 다중 인스턴스 설정에서 지정하는 **인스턴스**(계산 노드)의 총 수와 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-114">The total number of tasks (primary plus all subtasks) matches the number of **instances** (compute nodes) you specify in the multi-instance settings.</span></span>
2. <span data-ttu-id="d1bab-115">배치는 계산 노드 중 하나를 **마스터**로 지정하고 주 작업이 마스터에서 실행되도록 예약합니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-115">Batch designates one of the compute nodes as the **master**, and schedules the primary task to execute on the master.</span></span> <span data-ttu-id="d1bab-116">하위 작업이 다중 인스턴스 작업, 노드당 하나의 하위 작업에 할당된 계산 노드의 나머지 부분에서 실행되도록 예약합니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-116">It schedules the subtasks to execute on the remainder of the compute nodes allocated to the multi-instance task, one subtask per node.</span></span>
3. <span data-ttu-id="d1bab-117">주 및 하위 작업은 다중 인스턴스 설정에서 지정하는 모든 **공용 리소스 파일**을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-117">The primary and all subtasks download any **common resource files** you specify in the multi-instance settings.</span></span>
4. <span data-ttu-id="d1bab-118">공용 리소스 파일을 다운로드한 후 주 및 하위 작업에서 다중 인스턴스 설정에 지정하는 **조정 명령**을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-118">After the common resource files have been downloaded, the primary and subtasks execute the **coordination command** you specify in the multi-instance settings.</span></span> <span data-ttu-id="d1bab-119">조정 명령은 작업을 실행하기 위한 노드를 준비하는 데 일반적으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-119">The coordination command is typically used to prepare nodes for executing the task.</span></span> <span data-ttu-id="d1bab-120">이는 백그라운드 서비스 시작(예: [Microsoft MPI][msmpi_msdn]의 `smpd.exe`) 및 노드가 노드 간 메시지를 처리할 준비가 되었음을 확인하는 것을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-120">This can include starting background services (such as [Microsoft MPI][msmpi_msdn]'s `smpd.exe`) and verifying that the nodes are ready to process inter-node messages.</span></span>
5. <span data-ttu-id="d1bab-121">주 및 모든 하위 작업에서 조정 명령이 성공적으로 완료된 *후* 주 작업은 마스터 노드에서 **응용 프로그램 명령**을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-121">The primary task executes the **application command** on the master node *after* the coordination command has been completed successfully by the primary and all subtasks.</span></span> <span data-ttu-id="d1bab-122">응용 프로그램 명령은 다중 인스턴스 작업 자체의 명령줄이며 주 작업에서만 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-122">The application command is the command line of the multi-instance task itself, and is executed only by the primary task.</span></span> <span data-ttu-id="d1bab-123">[MS-MPI][msmpi_msdn] 기반 솔루션에서 `mpiexec.exe`를 사용하여 MPI 사용 응용 프로그램을 실행하는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-123">In an [MS-MPI][msmpi_msdn]-based solution, this is where you execute your MPI-enabled application using `mpiexec.exe`.</span></span>

> [!NOTE]
> <span data-ttu-id="d1bab-124">기능적으로 고유하지만 "다중 인스턴스 작업"은 [StartTask][net_starttask] 또는 [JobPreparationTask][net_jobprep]와 같은 고유 작업 유형이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-124">Though it is functionally distinct, the "multi-instance task" is not a unique task type like the [StartTask][net_starttask] or [JobPreparationTask][net_jobprep].</span></span> <span data-ttu-id="d1bab-125">다중 인스턴스 작업은 단순히 다중 인스턴스 설정이 구성된 표준 배치 작업(배치 .NET에서 [CloudTask][net_task])입니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-125">The multi-instance task is simply a standard Batch task ([CloudTask][net_task] in Batch .NET) whose multi-instance settings have been configured.</span></span> <span data-ttu-id="d1bab-126">이 문서에서는 이를 **다중 인스턴스 작업**이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-126">In this article, we refer to this as the **multi-instance task**.</span></span>
>
>

## <a name="requirements-for-multi-instance-tasks"></a><span data-ttu-id="d1bab-127">다중 인스턴스 작업에 대한 요구 사항</span><span class="sxs-lookup"><span data-stu-id="d1bab-127">Requirements for multi-instance tasks</span></span>
<span data-ttu-id="d1bab-128">다중 인스턴스 작업은 **노드 간 통신이 활성화**되고 **동시 작업 실행이 비활성화**된 풀이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-128">Multi-instance tasks require a pool with **inter-node communication enabled**, and with **concurrent task execution disabled**.</span></span> <span data-ttu-id="d1bab-129">동시 작업 실행을 사용하지 않도록 설정하려면 [CloudPool.MaxTasksPerComputeNode](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool#Microsoft_Azure_Batch_CloudPool_MaxTasksPerComputeNode) 속성을 1로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-129">To disable concurrent task execution, set the [CloudPool.MaxTasksPerComputeNode](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool#Microsoft_Azure_Batch_CloudPool_MaxTasksPerComputeNode) property to 1.</span></span>

<span data-ttu-id="d1bab-130">이 코드 조각에서는 일괄 처리 .NET 라이브러리를 사용하여 다중 인스턴스 작업용 풀을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-130">This code snippet shows how to create a pool for multi-instance tasks using the Batch .NET library.</span></span>

```csharp
CloudPool myCloudPool =
    myBatchClient.PoolOperations.CreatePool(
        poolId: "MultiInstanceSamplePool",
        targetDedicatedComputeNodes: 3
        virtualMachineSize: "small",
        cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));

// Multi-instance tasks require inter-node communication, and those nodes
// must run only one task at a time.
myCloudPool.InterComputeNodeCommunicationEnabled = true;
myCloudPool.MaxTasksPerComputeNode = 1;
```

> [!NOTE]
> <span data-ttu-id="d1bab-131">노드 간 통신이 비활성화되었거나 *maxTasksPerNode* 값이 1보다 큰 풀에서 다중 인스턴스 작업을 실행하려는 경우 작업은 예약되지 않습니다. 무기한으로 "활성" 상태로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-131">If you try to run a multi-instance task in a pool with internode communication disabled, or with a *maxTasksPerNode* value greater than 1, the task is never scheduled--it remains indefinitely in the "active" state.</span></span> 
>
> <span data-ttu-id="d1bab-132">다중 인스턴스 작업은 2015년 12월 14일 이후에 만든 풀의 노드에서만 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-132">Multi-instance tasks can execute only on nodes in pools created after 14 December 2015.</span></span>
>
>

### <a name="use-a-starttask-to-install-mpi"></a><span data-ttu-id="d1bab-133">StartTask를 사용하여 MPI 설치</span><span class="sxs-lookup"><span data-stu-id="d1bab-133">Use a StartTask to install MPI</span></span>
<span data-ttu-id="d1bab-134">다중 인스턴스 작업으로 MPI 응용 프로그램을 실행하려면 먼저 풀의 계산 노드에 MPI 구현(예: MS-MPI 또는 Intel MPI)을 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-134">To run MPI applications with a multi-instance task, you first need to install an MPI implementation (MS-MPI or Intel MPI, for example) on the compute nodes in the pool.</span></span> <span data-ttu-id="d1bab-135">노드가 풀에 연결되거나 다시 시작될 때마다 실행하는 [StartTask][net_starttask]를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-135">This is a good time to use a [StartTask][net_starttask], which executes whenever a node joins a pool, or is restarted.</span></span> <span data-ttu-id="d1bab-136">이 코드 조각은 MS-MPI 설치 패키지를 [리소스 파일][net_resourcefile]로 지정하는 StartTask를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-136">This code snippet creates a StartTask that specifies the MS-MPI setup package as a [resource file][net_resourcefile].</span></span> <span data-ttu-id="d1bab-137">리소스 파일이 노드로 다운로드된 후에 시작 태스크의 명령줄이 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-137">The start task's command line is executed after the resource file is downloaded to the node.</span></span> <span data-ttu-id="d1bab-138">이 경우 명령줄은 MS-MPI의 무인 설치를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-138">In this case, the command line performs an unattended install of MS-MPI.</span></span>

```csharp
// Create a StartTask for the pool which we use for installing MS-MPI on
// the nodes as they join the pool (or when they are restarted).
StartTask startTask = new StartTask
{
    CommandLine = "cmd /c MSMpiSetup.exe -unattend -force",
    ResourceFiles = new List<ResourceFile> { new ResourceFile("https://mystorageaccount.blob.core.windows.net/mycontainer/MSMpiSetup.exe", "MSMpiSetup.exe") },
    UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin)),
    WaitForSuccess = true
};
myCloudPool.StartTask = startTask;

// Commit the fully configured pool to the Batch service to actually create
// the pool and its compute nodes.
await myCloudPool.CommitAsync();
```

### <a name="remote-direct-memory-access-rdma"></a><span data-ttu-id="d1bab-139">RDMA(원격 직접 메모리 액세스)</span><span class="sxs-lookup"><span data-stu-id="d1bab-139">Remote direct memory access (RDMA)</span></span>
<span data-ttu-id="d1bab-140">배치 풀에서 계산 노드에 대해 A9 등, [RDMA 지원 크기](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 사용하는 경우 MPI 응용 프로그램은 Azure의 고성능, 지연율이 낮은 RDMA(원격 직접 메모리 액세스) 네트워크를 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-140">When you choose an [RDMA-capable size](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) such as A9 for the compute nodes in your Batch pool, your MPI application can take advantage of Azure's high-performance, low-latency remote direct memory access (RDMA) network.</span></span>

<span data-ttu-id="d1bab-141">다음 문서에서 "RDMA 지원"으로 지정된 크기를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-141">Look for the sizes specified as "RDMA capable" in the following articles:</span></span>

* <span data-ttu-id="d1bab-142">**CloudServiceConfiguration** 풀</span><span class="sxs-lookup"><span data-stu-id="d1bab-142">**CloudServiceConfiguration** pools</span></span>

  * <span data-ttu-id="d1bab-143">[Cloud Services 크기](../cloud-services/cloud-services-sizes-specs.md)(Windows만 해당)</span><span class="sxs-lookup"><span data-stu-id="d1bab-143">[Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md) (Windows only)</span></span>
* <span data-ttu-id="d1bab-144">**VirtualMachineConfiguration** 풀</span><span class="sxs-lookup"><span data-stu-id="d1bab-144">**VirtualMachineConfiguration** pools</span></span>

  * <span data-ttu-id="d1bab-145">[Azure에서 가상 컴퓨터 크기](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)(Linux)</span><span class="sxs-lookup"><span data-stu-id="d1bab-145">[Sizes for virtual machines in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux)</span></span>
  * <span data-ttu-id="d1bab-146">[Azure에서 가상 컴퓨터 크기](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)(Windows)</span><span class="sxs-lookup"><span data-stu-id="d1bab-146">[Sizes for virtual machines in Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows)</span></span>

> [!NOTE]
> <span data-ttu-id="d1bab-147">[Linux 계산 노드](batch-linux-nodes.md)에서 RDMA를 활용하려면 노드에서 **Intel MPI**를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-147">To take advantage of RDMA on [Linux compute nodes](batch-linux-nodes.md), you must use **Intel MPI** on the nodes.</span></span> <span data-ttu-id="d1bab-148">CloudServiceConfiguration 및 VirtualMachineConfiguration 풀에 대한 자세한 내용은 배치 기능 개요의 [풀](batch-api-basics.md) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d1bab-148">For more information on CloudServiceConfiguration and VirtualMachineConfiguration pools, see the Pool section of the [Batch feature overview](batch-api-basics.md).</span></span>
>
>

## <a name="create-a-multi-instance-task-with-batch-net"></a><span data-ttu-id="d1bab-149">배치 .NET을 사용하여 다중 인스턴스 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="d1bab-149">Create a multi-instance task with Batch .NET</span></span>
<span data-ttu-id="d1bab-150">이제 풀 요구 사항 및 MPI 패키지 설치를 다루었으며 다중 인스턴스 작업을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-150">Now that we've covered the pool requirements and MPI package installation, let's create the multi-instance task.</span></span> <span data-ttu-id="d1bab-151">이 코드 조각에서 표준 [CloudTask][net_task]를 만든 다음 해당 [MultiInstanceSettings][net_multiinstance_prop] 속성을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-151">In this snippet, we create a standard [CloudTask][net_task], then configure its [MultiInstanceSettings][net_multiinstance_prop] property.</span></span> <span data-ttu-id="d1bab-152">이전에 설명했듯이 다중 인스턴스 작업은 고유한 작업 유형이 아니지만 다중 인스턴스 설정으로 구성된 표준 배치 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-152">As mentioned earlier, the multi-instance task is not a distinct task type, but a standard Batch task configured with multi-instance settings.</span></span>

```csharp
// Create the multi-instance task. Its command line is the "application command"
// and will be executed *only* by the primary, and only after the primary and
// subtasks execute the CoordinationCommandLine.
CloudTask myMultiInstanceTask = new CloudTask(id: "mymultiinstancetask",
    commandline: "cmd /c mpiexec.exe -wdir %AZ_BATCH_TASK_SHARED_DIR% MyMPIApplication.exe");

// Configure the task's MultiInstanceSettings. The CoordinationCommandLine will be executed by
// the primary and all subtasks.
myMultiInstanceTask.MultiInstanceSettings =
    new MultiInstanceSettings(numberOfNodes) {
    CoordinationCommandLine = @"cmd /c start cmd /c ""%MSMPI_BIN%\smpd.exe"" -d",
    CommonResourceFiles = new List<ResourceFile> {
    new ResourceFile("https://mystorageaccount.blob.core.windows.net/mycontainer/MyMPIApplication.exe",
                     "MyMPIApplication.exe")
    }
};

// Submit the task to the job. Batch will take care of splitting it into subtasks and
// scheduling them for execution on the nodes.
await myBatchClient.JobOperations.AddTaskAsync("mybatchjob", myMultiInstanceTask);
```

## <a name="primary-task-and-subtasks"></a><span data-ttu-id="d1bab-153">주 작업 및 하위 작업</span><span class="sxs-lookup"><span data-stu-id="d1bab-153">Primary task and subtasks</span></span>
<span data-ttu-id="d1bab-154">작업에 대한 다중 인스턴스 설정을 만드는 경우 작업을 실행하는 계산 노드 수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-154">When you create the multi-instance settings for a task, you specify the number of compute nodes that are to execute the task.</span></span> <span data-ttu-id="d1bab-155">작업에 태스크를 제출하는 경우 배치 서비스는 지정한 노드 수와 일치하는 하나의 **주** 작업과 충분한 **하위 작업**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-155">When you submit the task to a job, the Batch service creates one **primary** task and enough **subtasks** that together match the number of nodes you specified.</span></span>

<span data-ttu-id="d1bab-156">이러한 작업은 0에서 *numberOfInstances* - 1의 범위로 정수 ID가 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-156">These tasks are assigned an integer id in the range of 0 to *numberOfInstances* - 1.</span></span> <span data-ttu-id="d1bab-157">ID가 0인 작업은 주 작업이며 모든 다른 ID는 하위 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-157">The task with id 0 is the primary task, and all other ids are subtasks.</span></span> <span data-ttu-id="d1bab-158">예를 들어 작업에 대한 다음과 같은 다중 인스턴스 설정을 만드는 경우 주 작업은 0의 ID를 가지며 하위 작업은 1~9의 ID를 가집니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-158">For example, if you create the following multi-instance settings for a task, the primary task would have an id of 0, and the subtasks would have ids 1 through 9.</span></span>

```csharp
int numberOfNodes = 10;
myMultiInstanceTask.MultiInstanceSettings = new MultiInstanceSettings(numberOfNodes);
```

### <a name="master-node"></a><span data-ttu-id="d1bab-159">마스터 노드</span><span class="sxs-lookup"><span data-stu-id="d1bab-159">Master node</span></span>
<span data-ttu-id="d1bab-160">다중 인스턴스 작업을 제출할 때 배치 서비스는 계산 노드 중 하나를 “마스터” 노드로 지정하고 주 작업이 마스터 노드에서 실행되도록 예약합니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-160">When you submit a multi-instance task, the Batch service designates one of the compute nodes as the "master" node, and schedules the primary task to execute on the master node.</span></span> <span data-ttu-id="d1bab-161">하위 작업은 다중 인스턴스 작업에 할당된 노드의 나머지 부분에서 실행되도록 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-161">The subtasks are scheduled to execute on the remainder of the nodes allocated to the multi-instance task.</span></span>

## <a name="coordination-command"></a><span data-ttu-id="d1bab-162">조정 명령</span><span class="sxs-lookup"><span data-stu-id="d1bab-162">Coordination command</span></span>
<span data-ttu-id="d1bab-163">**조정 명령**은 주 및 하위 작업에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-163">The **coordination command** is executed by both the primary and subtasks.</span></span>

<span data-ttu-id="d1bab-164">조정 명령의 호출을 차단합니다. 배치는 조정 명령이 모든 하위 작업에 대해 성공적으로 반환될 때까지 응용 프로그램 명령을 실행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-164">The invocation of the coordination command is blocking--Batch does not execute the application command until the coordination command has returned successfully for all subtasks.</span></span> <span data-ttu-id="d1bab-165">따라서 조정 명령은 모든 필요한 백그라운드 서비스를 시작하고 사용할 준비가 되었는지 확인한 다음 종료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-165">The coordination command should therefore start any required background services, verify that they are ready for use, and then exit.</span></span> <span data-ttu-id="d1bab-166">예를 들어 MS-MPI 버전 7을 사용하는 솔루션에 대한 이 조정 명령은 노드에서 SMPD 서비스를 시작한 다음 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-166">For example, this coordination command for a solution using MS-MPI version 7 starts the SMPD service on the node, then exits:</span></span>

```
cmd /c start cmd /c ""%MSMPI_BIN%\smpd.exe"" -d
```

<span data-ttu-id="d1bab-167">이 조정 명령에서 `start`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-167">Note the use of `start` in this coordination command.</span></span> <span data-ttu-id="d1bab-168">`smpd.exe` 응용 프로그램은 실행 후 즉시 반환하지 않으므로 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-168">This is required because the `smpd.exe` application does not return immediately after execution.</span></span> <span data-ttu-id="d1bab-169">[start][cmd_start] 명령을 사용하지 않고 이 조정 명령에서 반환하지 않으므로 응용 프로그램 명령의 실행이 차단됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-169">Without the use of the [start][cmd_start] command, this coordination command would not return, and would therefore block the application command from running.</span></span>

## <a name="application-command"></a><span data-ttu-id="d1bab-170">응용 프로그램 명령</span><span class="sxs-lookup"><span data-stu-id="d1bab-170">Application command</span></span>
<span data-ttu-id="d1bab-171">주 작업 및 모든 하위 작업이 조정 명령 실행을 마치면 다중 인스턴스 작업의 명령줄이 주 작업에서*만* 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-171">Once the primary task and all subtasks have finished executing the coordination command, the multi-instance task's command line is executed by the primary task *only*.</span></span> <span data-ttu-id="d1bab-172">조정 명령과 구분하도록 **응용 프로그램 명령**이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-172">We call this the **application command** to distinguish it from the coordination command.</span></span>

<span data-ttu-id="d1bab-173">MS-MPI 응용 프로그램의 경우 `mpiexec.exe`로 MPI 사용 응용 프로그램을 실행하는 데 응용 프로그램 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-173">For MS-MPI applications, use the application command to execute your MPI-enabled application with `mpiexec.exe`.</span></span> <span data-ttu-id="d1bab-174">예를 들어 MS-MPI 버전 7을 사용하는 솔루션에 대한 응용 프로그램 명령은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-174">For example, here is an application command for a solution using MS-MPI version 7:</span></span>

```
cmd /c ""%MSMPI_BIN%\mpiexec.exe"" -c 1 -wdir %AZ_BATCH_TASK_SHARED_DIR% MyMPIApplication.exe
```

> [!NOTE]
> <span data-ttu-id="d1bab-175">기본적으로 MS-MPI의 `mpiexec.exe`는 `CCP_NODES` 변수를 사용하므로([환경 변수](#environment-variables) 참조) 위의 응용 프로그램 명령줄 예에서는 이를 제외합니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-175">Because MS-MPI's `mpiexec.exe` uses the `CCP_NODES` variable by default (see [Environment variables](#environment-variables)) the example application command line above excludes it.</span></span>
>
>

## <a name="environment-variables"></a><span data-ttu-id="d1bab-176">환경 변수</span><span class="sxs-lookup"><span data-stu-id="d1bab-176">Environment variables</span></span>
<span data-ttu-id="d1bab-177">배치는 다중 인스턴스 작업에 할당된 계산 노드의 다중 인스턴스 작업에 관련된 여러 [환경 변수][msdn_env_var]를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-177">Batch creates several [environment variables][msdn_env_var] specific to multi-instance tasks on the compute nodes allocated to a multi-instance task.</span></span> <span data-ttu-id="d1bab-178">조정 및 응용 프로그램 명령줄은 실행하는 스크립트 및 프로그램을 참조할 수 있는 것처럼 이러한 환경 변수를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-178">Your coordination and application command lines can reference these environment variables, as can the scripts and programs they execute.</span></span>

<span data-ttu-id="d1bab-179">다음 환경 변수는 다중 인스턴스 작업에서 사용하기 위해 배치 서비스에 의해 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-179">The following environment variables are created by the Batch service for use by multi-instance tasks:</span></span>

* `CCP_NODES`
* `AZ_BATCH_NODE_LIST`
* `AZ_BATCH_HOST_LIST`
* `AZ_BATCH_MASTER_NODE`
* `AZ_BATCH_TASK_SHARED_DIR`
* `AZ_BATCH_IS_CURRENT_NODE_MASTER`

<span data-ttu-id="d1bab-180">해당 내용 및 가시성을 포함한 해당 환경 변수 및 다른 배치 계산 노드 환경 변수에 대한 자세한 내용은 [계산 노드 환경 변수][msdn_env_var]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d1bab-180">For full details on these and the other Batch compute node environment variables, including their contents and visibility, see [Compute node environment variables][msdn_env_var].</span></span>

> [!TIP]
> <span data-ttu-id="d1bab-181">배치 Linux MPI 코드 샘플은 이러한 다양한 환경 변수 사용 방법의 예를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-181">The Batch Linux MPI code sample contains an example of how several of these environment variables can be used.</span></span> <span data-ttu-id="d1bab-182">[coordination-cmd][coord_cmd_example] Bash 스크립트는 Azure Storage에서 일반적인 응용 프로그램 및 입력 파일을 다운로드하고 마스터 노드에서 NFS(네트워크 파일 시스템) 공유를 활성화하고 NFS 클라이언트로 다중 인스턴스 작업에 할당된 다른 노드를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-182">The [coordination-cmd][coord_cmd_example] Bash script downloads common application and input files from Azure Storage, enables a Network File System (NFS) share on the master node, and configures the other nodes allocated to the multi-instance task as NFS clients.</span></span>
>
>

## <a name="resource-files"></a><span data-ttu-id="d1bab-183">리소스 파일</span><span class="sxs-lookup"><span data-stu-id="d1bab-183">Resource files</span></span>
<span data-ttu-id="d1bab-184">다중 인스턴스 작업에 대해 고려해야 할 리소스 파일의 두 집합: *모든* 작업(주 및 하위 작업)이 다운로드하는 **공용 리소스 파일** 및 *주 작업에서만* 다운로드하는 다중 인스턴스 작업 자체에 지정된 **리소스 파일**입니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-184">There are two sets of resource files to consider for multi-instance tasks: **common resource files** that *all* tasks download (both primary and subtasks), and the **resource files** specified for the multi-instance task itself, which *only the primary* task downloads.</span></span>

<span data-ttu-id="d1bab-185">작업에 대해 다중 인스턴스 설정에서 하나 이상의 **공용 리소스 파일**을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-185">You can specify one or more **common resource files** in the multi-instance settings for a task.</span></span> <span data-ttu-id="d1bab-186">이러한 공용 리소스 파일은 주 및 모든 하위 작업에 의해 [Azure Storage](../storage/common/storage-introduction.md)에서 각 노드의 **작업 공유 디렉터리**로 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-186">These common resource files are downloaded from [Azure Storage](../storage/common/storage-introduction.md) into each node's **task shared directory** by the primary and all subtasks.</span></span> <span data-ttu-id="d1bab-187">`AZ_BATCH_TASK_SHARED_DIR` 환경 변수를 사용하여 응용 프로그램 및 조정 명령줄에서 작업 공유 디렉터리에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-187">You can access the task shared directory from application and coordination command lines by using the `AZ_BATCH_TASK_SHARED_DIR` environment variable.</span></span> <span data-ttu-id="d1bab-188">`AZ_BATCH_TASK_SHARED_DIR` 경로는 다중 인스턴스 작업에 할당된 모든 노드에서 동일하므로 주 데이터베이스와 모든 하위 작업 간의 단일 조정 명령을 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-188">The `AZ_BATCH_TASK_SHARED_DIR` path is identical on every node allocated to the multi-instance task, thus you can share a single coordination command between the primary and all subtasks.</span></span> <span data-ttu-id="d1bab-189">배치는 원격 액세스 측면에서 디렉터리를 "공유"하지 않지만 환경 변수에 대한 팁에서 이전에 설명한 것처럼 탑재 또는 공유 지점으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-189">Batch does not "share" the directory in a remote access sense, but you can use it as a mount or share point as mentioned earlier in the tip on environment variables.</span></span>

<span data-ttu-id="d1bab-190">다중 인스턴스 작업 자체에 대해 지정한 리소스 파일은 작업의 작업 디렉터리 `AZ_BATCH_TASK_WORKING_DIR`에 기본적으로 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-190">Resource files that you specify for the multi-instance task itself are downloaded to the task's working directory, `AZ_BATCH_TASK_WORKING_DIR`, by default.</span></span> <span data-ttu-id="d1bab-191">언급한 대로 공용 리소스 파일과 달리 주 작업만이 다중 인스턴스 작업 자체에 대해 지정된 리소스 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-191">As mentioned, in contrast to common resource files, only the primary task downloads resource files specified for the  multi-instance task itself.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d1bab-192">명령줄에서 이러한 디렉터리를 나타내는 환경 변수 `AZ_BATCH_TASK_SHARED_DIR` 및 `AZ_BATCH_TASK_WORKING_DIR`을 항상 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-192">Always use the environment variables `AZ_BATCH_TASK_SHARED_DIR` and `AZ_BATCH_TASK_WORKING_DIR` to refer to these directories in your command lines.</span></span> <span data-ttu-id="d1bab-193">경로를 수동으로 구성하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="d1bab-193">Do not attempt to construct the paths manually.</span></span>
>
>

## <a name="task-lifetime"></a><span data-ttu-id="d1bab-194">작업 수명</span><span class="sxs-lookup"><span data-stu-id="d1bab-194">Task lifetime</span></span>
<span data-ttu-id="d1bab-195">주 작업의 수명은 전체 다중 인스턴스 작업의 수명을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-195">The lifetime of the primary task controls the lifetime of the entire multi-instance task.</span></span> <span data-ttu-id="d1bab-196">주 작업이 종료될 때 모든 하위 작업이 종료됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-196">When the primary exits, all of the subtasks are terminated.</span></span> <span data-ttu-id="d1bab-197">주 작업의 종료 코드는 작업의 종료 코드이며 따라서 재시도 목적에 대한 작업의 성공 여부를 결정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-197">The exit code of the primary is the exit code of the task, and is therefore used to determine the success or failure of the task for retry purposes.</span></span>

<span data-ttu-id="d1bab-198">하위 작업 중 하나라도 실패하는 경우(예: 0이 아닌 반환 코드와 함께 종료) 전체 다중 인스턴스 작업이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-198">If any of the subtasks fail, exiting with a non-zero return code, for example, the entire multi-instance task fails.</span></span> <span data-ttu-id="d1bab-199">다중 인스턴스 작업은 종료되고 해당 재시도 한계까지 재시도됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-199">The multi-instance task is then terminated and retried, up to its retry limit.</span></span>

<span data-ttu-id="d1bab-200">다중 인스턴스 작업을 삭제하는 경우 주 및 모든 하위 작업도 배치 서비스에서 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-200">When you delete a multi-instance task, the primary and all subtasks are also deleted by the Batch service.</span></span> <span data-ttu-id="d1bab-201">모든 하위 작업 디렉터리 및 해당 파일은 표준 작업의 경우처럼 계산 노드에서 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-201">All subtask directories and their files are deleted from the compute nodes, just as for a standard task.</span></span>

<span data-ttu-id="d1bab-202">[MaxTaskRetryCount][net_taskconstraint_maxretry], [MaxWallClockTime][net_taskconstraint_maxwallclock] 및 [RetentionTime][net_taskconstraint_retention] 속성과 같은 다중 인스턴스 작업에 대한 [TaskConstraints][net_taskconstraints]는 표준 작업에 대한 것이므로 적용되고 주 및 모든 하위 작업에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-202">[TaskConstraints][net_taskconstraints] for a multi-instance task, such as the [MaxTaskRetryCount][net_taskconstraint_maxretry], [MaxWallClockTime][net_taskconstraint_maxwallclock], and [RetentionTime][net_taskconstraint_retention] properties, are honored as they are for a standard task, and apply to the primary and all subtasks.</span></span> <span data-ttu-id="d1bab-203">그러나 다중 인스턴스 태스크를 작업에 추가한 후 [RetentionTime][net_taskconstraint_retention] 속성을 변경하는 경우 이 변경은 주 작업에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-203">However, if you change the [RetentionTime][net_taskconstraint_retention] property after adding the multi-instance task to the job, this change is applied only to the primary task.</span></span> <span data-ttu-id="d1bab-204">모든 하위 작업은 원래 [RetentionTime][net_taskconstraint_retention]을 계속해서 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-204">All of the subtasks continue to use the original [RetentionTime][net_taskconstraint_retention].</span></span>

<span data-ttu-id="d1bab-205">계산 노드의 최근 작업 목록은 최근 작업이 다중 인스턴스 작업의 일부일 경우 하위 작업의 ID를 반영합니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-205">A compute node's recent task list reflects the id of a subtask if the recent task was part of a multi-instance task.</span></span>

## <a name="obtain-information-about-subtasks"></a><span data-ttu-id="d1bab-206">하위 작업에 대한 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="d1bab-206">Obtain information about subtasks</span></span>
<span data-ttu-id="d1bab-207">배치 .NET 라이브러리를 사용하여 하위 작업에 대한 정보를 가져오려면 [CloudTask.ListSubtasks][net_task_listsubtasks] 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-207">To obtain information on subtasks by using the Batch .NET library, call the [CloudTask.ListSubtasks][net_task_listsubtasks] method.</span></span> <span data-ttu-id="d1bab-208">이 메서드는 모든 하위 작업에 대한 정보 및 작업을 실행하는 계산 노드에 대한 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-208">This method returns information on all subtasks, and information about the compute node that executed the tasks.</span></span> <span data-ttu-id="d1bab-209">이 정보로부터 각 하위 작업의 루트 디렉터리, 풀 ID, 현재 상태, 종료 코드 등을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-209">From this information, you can determine each subtask's root directory, the pool id, its current state, exit code, and more.</span></span> <span data-ttu-id="d1bab-210">[PoolOperations.GetNodeFile][poolops_getnodefile] 메서드와 함께 이 정보를 사용하여 하위 작업의 파일을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-210">You can use this information in combination with the [PoolOperations.GetNodeFile][poolops_getnodefile] method to obtain the subtask's files.</span></span> <span data-ttu-id="d1bab-211">이 메서드는 주 작업(ID 0)에 대한 정보를 반환하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-211">Note that this method does not return information for the primary task (id 0).</span></span>

> [!NOTE]
> <span data-ttu-id="d1bab-212">별도로 언급하지 않는 한 다중 인스턴스 [CloudTask][net_task] 자체에서 작동하는 배치 .NET 메서드는 주 작업에*만* 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-212">Unless otherwise stated, Batch .NET methods that operate on the multi-instance [CloudTask][net_task] itself apply *only* to the primary task.</span></span> <span data-ttu-id="d1bab-213">예를 들어 다중 인스턴스 작업에서 [CloudTask.ListNodeFiles][net_task_listnodefiles] 메서드를 호출하는 경우 주 작업의 파일만 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-213">For example, when you call the [CloudTask.ListNodeFiles][net_task_listnodefiles] method on a multi-instance task, only the primary task's files are returned.</span></span>
>
>

<span data-ttu-id="d1bab-214">다음 코드 조각은 하위 작업 정보를 얻는 방법 뿐만 아니라 실행되는 노드에서 파일 콘텐츠를 요청하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-214">The following code snippet shows how to obtain subtask information, as well as request file contents from the nodes on which they executed.</span></span>

```csharp
// Obtain the job and the multi-instance task from the Batch service
CloudJob boundJob = batchClient.JobOperations.GetJob("mybatchjob");
CloudTask myMultiInstanceTask = boundJob.GetTask("mymultiinstancetask");

// Now obtain the list of subtasks for the task
IPagedEnumerable<SubtaskInformation> subtasks = myMultiInstanceTask.ListSubtasks();

// Asynchronously iterate over the subtasks and print their stdout and stderr
// output if the subtask has completed
await subtasks.ForEachAsync(async (subtask) =>
{
    Console.WriteLine("subtask: {0}", subtask.Id);
    Console.WriteLine("exit code: {0}", subtask.ExitCode);

    if (subtask.State == SubtaskState.Completed)
    {
        ComputeNode node =
            await batchClient.PoolOperations.GetComputeNodeAsync(subtask.ComputeNodeInformation.PoolId,
                                                                 subtask.ComputeNodeInformation.ComputeNodeId);

        NodeFile stdOutFile = await node.GetNodeFileAsync(subtask.ComputeNodeInformation.TaskRootDirectory + "\\" + Constants.StandardOutFileName);
        NodeFile stdErrFile = await node.GetNodeFileAsync(subtask.ComputeNodeInformation.TaskRootDirectory + "\\" + Constants.StandardErrorFileName);
        stdOut = await stdOutFile.ReadAsStringAsync();
        stdErr = await stdErrFile.ReadAsStringAsync();

        Console.WriteLine("node: {0}:", node.Id);
        Console.WriteLine("stdout.txt: {0}", stdOut);
        Console.WriteLine("stderr.txt: {0}", stdErr);
    }
    else
    {
        Console.WriteLine("\tSubtask {0} is in state {1}", subtask.Id, subtask.State);
    }
});
```

## <a name="code-sample"></a><span data-ttu-id="d1bab-215">코드 샘플</span><span class="sxs-lookup"><span data-stu-id="d1bab-215">Code sample</span></span>
<span data-ttu-id="d1bab-216">GitHub의 [MultiInstanceTasks][github_mpi] 코드 샘플에서는 다중 인스턴스 태스크를 사용하여 배치 계산 노드에서 [MS-MPI][msmpi_msdn] 응용 프로그램을 실행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-216">The [MultiInstanceTasks][github_mpi] code sample on GitHub demonstrates how to use a multi-instance task to run an [MS-MPI][msmpi_msdn] application on Batch compute nodes.</span></span> <span data-ttu-id="d1bab-217">[준비](#preparation) 및 [실행](#execution)의 단계에 따라 샘플을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-217">Follow the steps in [Preparation](#preparation) and [Execution](#execution) to run the sample.</span></span>

### <a name="preparation"></a><span data-ttu-id="d1bab-218">준비</span><span class="sxs-lookup"><span data-stu-id="d1bab-218">Preparation</span></span>
1. <span data-ttu-id="d1bab-219">[How to compile and run a simple MS-MPI program][msmpi_howto](간단한 MS-MPI 프로그램을 컴파일하고 실행하는 방법)의 처음 두 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-219">Follow the first two steps in [How to compile and run a simple MS-MPI program][msmpi_howto].</span></span> <span data-ttu-id="d1bab-220">이렇게 하면 다음 단계의 필수 조건을 충족시킵니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-220">This satisfies the prerequesites for the following step.</span></span>
2. <span data-ttu-id="d1bab-221">[MPIHelloWorld][helloworld_proj] 샘플 MPI 프로그램의 *릴리스* 버전을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-221">Build a *Release* version of the [MPIHelloWorld][helloworld_proj] sample MPI program.</span></span> <span data-ttu-id="d1bab-222">이는 다중 인스턴스 태스크를 통해 계산 노드에서 실행할 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-222">This is the program that will be run on compute nodes by the multi-instance task.</span></span>
3. <span data-ttu-id="d1bab-223">`MPIHelloWorld.exe`(2단계에서 빌드) 및 `MSMpiSetup.exe`(1단계에서 다운로드)를 포함하는 Zip 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-223">Create a zip file containing `MPIHelloWorld.exe` (which you built step 2) and `MSMpiSetup.exe` (which you downloaded step 1).</span></span> <span data-ttu-id="d1bab-224">다음 단계의 응용 프로그램 패키지로 이 Zip 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-224">You'll upload this zip file as an application package in the next step.</span></span>
4. <span data-ttu-id="d1bab-225">[Azure Portal][portal]을 사용하여 "MPIHelloWorld"라는 배치 [응용 프로그램](batch-application-packages.md)을 만들고, 이전 단계에서 만든 Zip 파일을 버전 "1.0"의 응용 프로그램 패키지로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-225">Use the [Azure portal][portal] to create a Batch [application](batch-application-packages.md) called "MPIHelloWorld", and specify the zip file you created in the previous step as version "1.0" of the application package.</span></span> <span data-ttu-id="d1bab-226">자세한 내용은 [응용 프로그램 업로드 및 관리](batch-application-packages.md#upload-and-manage-applications)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d1bab-226">See [Upload and manage applications](batch-application-packages.md#upload-and-manage-applications) for more information.</span></span>

> [!TIP]
> <span data-ttu-id="d1bab-227">응용 프로그램 패키지에 추가 종속성(예: `msvcp140d.dll` 또는 `vcruntime140d.dll`)을 포함할 필요가 없도록 *릴리스* 버전의 `MPIHelloWorld.exe`을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-227">Build a *Release* version of `MPIHelloWorld.exe` so that you don't have to include any additional dependencies (for example, `msvcp140d.dll` or `vcruntime140d.dll`) in your application package.</span></span>
>
>

### <a name="execution"></a><span data-ttu-id="d1bab-228">실행</span><span class="sxs-lookup"><span data-stu-id="d1bab-228">Execution</span></span>
1. <span data-ttu-id="d1bab-229">GitHub에서 [azure-batch-samples][github_samples_zip]를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-229">Download the [azure-batch-samples][github_samples_zip] from GitHub.</span></span>
2. <span data-ttu-id="d1bab-230">Visual Studio 2015 이상에서 MultiInstanceTasks **솔루션**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-230">Open the MultiInstanceTasks **solution** in Visual Studio 2015 or newer.</span></span> <span data-ttu-id="d1bab-231">`MultiInstanceTasks.sln` 솔루션 파일은 다음 위치에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-231">The `MultiInstanceTasks.sln` solution file is located in:</span></span>

    `azure-batch-samples\CSharp\ArticleProjects\MultiInstanceTasks\`
3. <span data-ttu-id="d1bab-232">**Microsoft.Azure.Batch.Samples.Common** 프로젝트의 `AccountSettings.settings`에 배치 계정 및 저장소 계정의 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-232">Enter your Batch and Storage account credentials in `AccountSettings.settings` in the **Microsoft.Azure.Batch.Samples.Common** project.</span></span>
4. <span data-ttu-id="d1bab-233">MultiInstanceTasks 솔루션을 **빌드 및 실행**하여 배치 풀의 계산 노드에서 MPI 샘플 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-233">**Build and run** the MultiInstanceTasks solution to execute the MPI sample application on compute nodes in a Batch pool.</span></span>
5. <span data-ttu-id="d1bab-234">*선택 사항*: [Azure Portal][portal] 또는 [배치 탐색기][batch_explorer]를 사용하여 리소스를 삭제하기 전에 샘플 풀, 작업 및 태스크("MultiInstanceSamplePool", "MultiInstanceSampleJob", "MultiInstanceSampleTask")를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-234">*Optional*: Use the [Azure portal][portal] or the [Batch Explorer][batch_explorer] to examine the sample pool, job, and task ("MultiInstanceSamplePool", "MultiInstanceSampleJob", "MultiInstanceSampleTask") before you delete the resources.</span></span>

> [!TIP]
> <span data-ttu-id="d1bab-235">Visual Studio가 없는 경우 [Visual Studio 커뮤니티][visual_studio]를 무료로 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-235">You can download [Visual Studio Community][visual_studio] for free if you do not have Visual Studio.</span></span>
>
>

<span data-ttu-id="d1bab-236">`MultiInstanceTasks.exe`는 다음과 유사하게 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-236">Output from `MultiInstanceTasks.exe` is similar to the following:</span></span>

```
Creating pool [MultiInstanceSamplePool]...
Creating job [MultiInstanceSampleJob]...
Adding task [MultiInstanceSampleTask] to job [MultiInstanceSampleJob]...
Awaiting task completion, timeout in 00:30:00...

Main task [MultiInstanceSampleTask] is in state [Completed] and ran on compute node [tvm-1219235766_1-20161017t162002z]:
---- stdout.txt ----
Rank 2 received string "Hello world" from Rank 0
Rank 1 received string "Hello world" from Rank 0

---- stderr.txt ----

Main task completed, waiting 00:00:10 for subtasks to complete...

---- Subtask information ----
subtask: 1
        exit code: 0
        node: tvm-1219235766_3-20161017t162002z
        stdout.txt:
        stderr.txt:
subtask: 2
        exit code: 0
        node: tvm-1219235766_2-20161017t162002z
        stdout.txt:
        stderr.txt:

Delete job? [yes] no: yes
Delete pool? [yes] no: yes

Sample complete, hit ENTER to exit...
```

## <a name="next-steps"></a><span data-ttu-id="d1bab-237">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d1bab-237">Next steps</span></span>
* <span data-ttu-id="d1bab-238">Microsoft HPC 및 Azure 배치 팀 블로그는 [Azure 배치의 Linux에 대한 MPI 지원][blog_mpi_linux]을 설명하고 배치와 함께 [OpenFOAM][openfoam] 사용에 대한 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-238">The Microsoft HPC & Azure Batch Team blog discusses [MPI support for Linux on Azure Batch][blog_mpi_linux], and includes information on using [OpenFOAM][openfoam] with Batch.</span></span> <span data-ttu-id="d1bab-239">[GitHub에서 OpenFOAM 예제][github_mpi]에 대한 Python 코드 샘플을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-239">You can find Python code samples for the [OpenFOAM example on GitHub][github_mpi].</span></span>
* <span data-ttu-id="d1bab-240">Azure 배치 MPI 솔루션에서 사용하기 위해 [Linux 계산 노드 풀을 만드는 방법](batch-linux-nodes.md)을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d1bab-240">Learn how to [create pools of Linux compute nodes](batch-linux-nodes.md) for use in your Azure Batch MPI solutions.</span></span>

[helloworld_proj]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/MultiInstanceTasks/MPIHelloWorld

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[batch_explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[blog_mpi_linux]: https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/
[cmd_start]: https://technet.microsoft.com/library/cc770297.aspx
[coord_cmd_example]: https://github.com/Azure/azure-batch-samples/blob/master/Python/Batch/article_samples/mpi/data/linux/openfoam/coordination-cmd
[github_mpi]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/MultiInstanceTasks
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_samples_zip]: https://github.com/Azure/azure-batch-samples/archive/master.zip
[msdn_env_var]: https://msdn.microsoft.com/library/azure/mt743623.aspx
[msmpi_msdn]: https://msdn.microsoft.com/library/bb524831.aspx
[msmpi_sdk]: http://go.microsoft.com/FWLink/p/?LinkID=389556
[msmpi_howto]: http://blogs.technet.com/b/windowshpc/archive/2015/02/02/how-to-compile-and-run-a-simple-ms-mpi-program.aspx
[openfoam]: http://www.openfoam.com/
[visual_studio]: https://www.visualstudio.com/vs/community/

[net_jobprep]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobpreparationtask.aspx
[net_multiinstance_class]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.aspx
[net_multiinstance_prop]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.multiinstancesettings.aspx
[net_multiinsance_commonresfiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.commonresourcefiles.aspx
[net_multiinstance_coordcmdline]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.coordinationcommandline.aspx
[net_multiinstance_numinstances]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.numberofinstances.aspx
[net_pool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_pool_create]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.createpool.aspx
[net_pool_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.starttask.aspx
[net_resourcefile]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.resourcefile.aspx
[net_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.aspx
[net_starttask_cmdline]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.commandline.aspx
[net_task]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_taskconstraints]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskconstraints.aspx
[net_taskconstraint_maxretry]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskconstraints.maxtaskretrycount.aspx
[net_taskconstraint_maxwallclock]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskconstraints.maxwallclocktime.aspx
[net_taskconstraint_retention]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskconstraints.retentiontime.aspx
[net_task_listsubtasks]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.listsubtasks.aspx
[net_task_listnodefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.listnodefiles.aspx
[poolops_getnodefile]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.getnodefile.aspx

[portal]: https://portal.azure.com
[rest_multiinstance]: https://msdn.microsoft.com/library/azure/mt637905.aspx

[1]: ./media/batch-mpi/batch_mpi_01.png "다중 인스턴스 개요"

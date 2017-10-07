---
title: "다중 인스턴스 aaaUse toorun MPI 응용 프로그램-Azure 일괄 처리 작업 | Microsoft Docs"
description: "Azure 일괄 처리에서 tooexecute 인터페이스 MPI (Message Passing) hello 다중 인스턴스 작업을 사용 하 여 응용 프로그램을 입력 하는 방법을 알아봅니다."
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
ms.openlocfilehash: b0e3295a6aeb76267c26d5504bcff59de3dc5e22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-multi-instance-tasks-toorun-message-passing-interface-mpi-applications-in-batch"></a>일괄 처리의 다중 인스턴스 작업 toorun 인터페이스 MPI (Message Passing) 응용 프로그램을 사용 하 여

다중 인스턴스 작업 사용 하면 Azure 일괄 처리 작업 toorun 여러 계산 노드에서 동시에 있습니다. 이러한 작업을 통해 MPI(메시지 전달 인터페이스) 응용 프로그램과 같은 고성능 컴퓨팅 시나리오를 배치로 수행할 수 있습니다. Hello를 사용 하 여 tooexecute 다중 인스턴스 작업 방법을 배웁니다이 문서에서는 [일괄 처리.NET] [ api_net] 라이브러리입니다.

> [!NOTE]
> Hello이이 문서의 예제에서는 일괄 처리.NET, MS-MPI를에 집중 하 고 Windows 계산 노드, 여기에 설명 된 hello 다중 인스턴스 작업 개념은 tooother 적용 가능한 플랫폼 및 (Python 및 예를 들어 Linux 노드에서 Intel MPI) 기술입니다.
>
>

## <a name="multi-instance-task-overview"></a>다중 인스턴스 작업 개요
일괄 처리에서 각 태스크는 정상적으로 실행 단일 계산 노드에서-여러 작업 tooa 작업을 제출 하 고 hello 일괄 처리 서비스 노드에서 실행에 대 한 각 작업을 예약 합니다. 그러나 작업의 구성으로 **다중 인스턴스 설정**, 일괄 처리를 지시 tooinstead 하나의 기본 작업과 여러 노드에 대해 다음 실행 되는 여러 개의 하위 작업을 만듭니다.

![다중 인스턴스 작업 개요][1]

다중 인스턴스 설정 tooa 작업 인 작업을 제출 하면 몇 가지 단계 고유한 toomulti 인스턴스 작업 일괄 처리를 수행 합니다.

1. hello 일괄 처리 서비스에서 만들어집니다 **기본** 과 몇 가지 **하위** hello 다중 인스턴스 설정을 기반으로 합니다. (모든 하위 작업 및 기본) 작업의 총 hello hello 수가 일치 **인스턴스** (계산 노드) hello 다중 인스턴스 설정에서 지정 합니다.
2. 일괄 처리 중 하나를 지정 hello 계산 노드 hello로 **마스터**, 일정 hello 마스터 주 작업 tooexecute hello 및 합니다. Hello 계산 노드에 할당 된 toohello 다중 인스턴스 작업 노드당 하나의 하위 작업의 나머지 부분에서는 hello에 hello 하위 tooexecute를 예약합니다.
3. 기본 hello 및 하위 작업을 모두 다운로드 **공용 리소스 파일** hello 다중 인스턴스 설정에서 지정 합니다.
4. 기본 hello 및 하위 작업 실행 hello hello 공용 리소스 파일을 다운로드 한 후 **조정 명령** hello 다중 인스턴스 설정에서 지정 합니다. hello 조정 명령 hello 작업을 실행 하는 데 일반적으로 사용 되는 tooprepare 노드입니다. 백그라운드 서비스 시작 포함할 수 있습니다 (같은 [Microsoft MPI][msmpi_msdn]의 `smpd.exe`) hello 노드 준비 tooprocess 노드 간 메시지 하는지 확인 하 고 있습니다.
5. hello 주 작업 실행 hello **응용 프로그램 명령** hello 마스터 노드에서 *후* hello 기본 및 모든 하위 작업으로 hello 조정 명령이 성공적으로 완료 되었습니다. hello 응용 프로그램 명령 자체 hello 다중 인스턴스 작업의 hello 명령줄이 고 hello 주 작업에 의해서만 실행 됩니다. [MS-MPI][msmpi_msdn] 기반 솔루션에서 `mpiexec.exe`를 사용하여 MPI 사용 응용 프로그램을 실행하는 위치입니다.

> [!NOTE]
> 기능적으로 고유한 이기는 하지만 hello "다중 인스턴스 작업" 형식이 아닌 고유 작업 hello와 같은 [StartTask] [ net_starttask] 또는 [JobPreparationTask] [ net_jobprep]. hello 다중 인스턴스 작업은 단순히 표준 일괄 처리 작업 ([CloudTask] [ net_task] 일괄 처리.net에서) 인 다중 인스턴스 설정이 구성 되었습니다. 이 문서에서는 hello로 toothis 참조 **다중 인스턴스 작업**합니다.
>
>

## <a name="requirements-for-multi-instance-tasks"></a>다중 인스턴스 작업에 대한 요구 사항
다중 인스턴스 작업은 **노드 간 통신이 활성화**되고 **동시 작업 실행이 비활성화**된 풀이 필요합니다. toodisable 동시 작업 실행을 집합 hello [CloudPool.MaxTasksPerComputeNode](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool#Microsoft_Azure_Batch_CloudPool_MaxTasksPerComputeNode) 속성 too1 합니다.

이 코드 조각은 hello 일괄 처리.NET 라이브러리를 사용 하 여 toocreate 다중 인스턴스에 대 한 풀을 작업 하는 방법을 보여 줍니다.

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
> Toorun 다중 인스턴스 작업 노드 간 통신을 사용 하 여 풀에 사용 하지 않도록 설정 하면 또는 *maxTasksPerNode* hello 작업은 예약 되지-, 1 보다 큰 값 hello "활성" 상태인 무기한으로 유지 됩니다. 
>
> 다중 인스턴스 작업은 2015년 12월 14일 이후에 만든 풀의 노드에서만 실행할 수 있습니다.
>
>

### <a name="use-a-starttask-tooinstall-mpi"></a>StartTask tooinstall MPI를 사용 하 여
다중 인스턴스 작업과 toorun MPI 응용 프로그램을 먼저 tooinstall hello 풀의 hello 계산 노드에서 MPI 구현 (예: Intel MPI 또는 MS-MPI). 이것이 좋은 시간 toouse는 [StartTask][net_starttask], 노드는 풀에 참가 하거나 다시 시작 될 때마다를 실행 하는 합니다. 이 코드 조각에서는으로 hello MS-MPI 설치 패키지를 지정 하는 StartTask는 [리소스 파일][net_resourcefile]합니다. hello 리소스 파일은 다운로드 한 toohello 노드 후 hello 시작 작업의 명령줄 실행 됩니다. 이 경우 hello 명령줄 MS-MPI의 무인된 설치를 수행합니다.

```csharp
// Create a StartTask for hello pool which we use for installing MS-MPI on
// hello nodes as they join hello pool (or when they are restarted).
StartTask startTask = new StartTask
{
    CommandLine = "cmd /c MSMpiSetup.exe -unattend -force",
    ResourceFiles = new List<ResourceFile> { new ResourceFile("https://mystorageaccount.blob.core.windows.net/mycontainer/MSMpiSetup.exe", "MSMpiSetup.exe") },
    UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin)),
    WaitForSuccess = true
};
myCloudPool.StartTask = startTask;

// Commit hello fully configured pool toohello Batch service tooactually create
// hello pool and its compute nodes.
await myCloudPool.CommitAsync();
```

### <a name="remote-direct-memory-access-rdma"></a>RDMA(원격 직접 메모리 액세스)
선택 하는 경우는 [RDMA 가능 크기](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) MPI 응용 프로그램의 Azure의 고성능의 대기 시간이 짧은 원격 직접 메모리 액세스 (RDMA) 네트워크 이용할 수 A9 hello에 대 한 계산 노드에 배치 풀을와 같은 합니다.

Hello 다음 문서에서에서 "RDMA 기능"로 지정 하는 hello 크기를 찾습니다.

* **CloudServiceConfiguration** 풀

  * [Cloud Services 크기](../cloud-services/cloud-services-sizes-specs.md)(Windows만 해당)
* **VirtualMachineConfiguration** 풀

  * [Azure에서 가상 컴퓨터 크기](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)(Linux)
  * [Azure에서 가상 컴퓨터 크기](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)(Windows)

> [!NOTE]
> RDMA tootake 활용 [Linux 계산 노드](batch-linux-nodes.md)를 사용 해야 **Intel MPI** hello 노드에서 합니다. CloudServiceConfiguration 및 VirtualMachineConfiguration 풀에 대 한 자세한 내용은 참조 하십시오. hello의 풀 섹션 hello [배치 기능 개요](batch-api-basics.md)합니다.
>
>

## <a name="create-a-multi-instance-task-with-batch-net"></a>배치 .NET을 사용하여 다중 인스턴스 작업 만들기
Hello 풀 요구 사항 및 MPI 패키지 설치 설명한 했으므로 hello 다중 인스턴스 작업을 만들어 보겠습니다. 이 코드 조각에서 표준 [CloudTask][net_task]를 만든 다음 해당 [MultiInstanceSettings][net_multiinstance_prop] 속성을 구성합니다. 앞서 언급 했 듯이 hello 다중 인스턴스 작업 고유한 작업 종류를 아니라 다중 인스턴스 설정으로 구성 하는 표준 일괄 처리 작업입니다.

```csharp
// Create hello multi-instance task. Its command line is hello "application command"
// and will be executed *only* by hello primary, and only after hello primary and
// subtasks execute hello CoordinationCommandLine.
CloudTask myMultiInstanceTask = new CloudTask(id: "mymultiinstancetask",
    commandline: "cmd /c mpiexec.exe -wdir %AZ_BATCH_TASK_SHARED_DIR% MyMPIApplication.exe");

// Configure hello task's MultiInstanceSettings. hello CoordinationCommandLine will be executed by
// hello primary and all subtasks.
myMultiInstanceTask.MultiInstanceSettings =
    new MultiInstanceSettings(numberOfNodes) {
    CoordinationCommandLine = @"cmd /c start cmd /c ""%MSMPI_BIN%\smpd.exe"" -d",
    CommonResourceFiles = new List<ResourceFile> {
    new ResourceFile("https://mystorageaccount.blob.core.windows.net/mycontainer/MyMPIApplication.exe",
                     "MyMPIApplication.exe")
    }
};

// Submit hello task toohello job. Batch will take care of splitting it into subtasks and
// scheduling them for execution on hello nodes.
await myBatchClient.JobOperations.AddTaskAsync("mybatchjob", myMultiInstanceTask);
```

## <a name="primary-task-and-subtasks"></a>주 작업 및 하위 작업
작업에 대 한 다중 인스턴스 설정을 hello을 만들면 hello tooexecute hello로 작업 하는 계산 노드 수를 지정 합니다. Hello 작업 tooa 작업을 제출 하는 경우 hello 일괄 처리 서비스에서 만들어집니다 **기본** 작업과 충분 **하위** 함께 지정한 노드의 hello 수를 일치 하는 합니다.

이러한 태스크는 너무 hello 범위는 0에는 정수 id를 할당 된*numberOfInstances* -1입니다. id가 0으로 hello 작업이 hello 기본 작업이 및 다른 모든 id는 하위 작업 합니다. 예를 들어 다음 작업에 대 한 다중 인스턴스 설정을 hello를 만들면 hello 주 작업 id가 0, 있고 hello 하위 작업 id 1-9 갖기.

```csharp
int numberOfNodes = 10;
myMultiInstanceTask.MultiInstanceSettings = new MultiInstanceSettings(numberOfNodes);
```

### <a name="master-node"></a>마스터 노드
다중 인스턴스 작업을 전송 하면 일괄 처리 서비스 hello은 hello 중 하나 계산 노드 hello "마스터" 노드로 지정 하 고 일정 hello hello 마스터 노드에서 tooexecute 주 작업 합니다. hello 하위 toohello 다중 인스턴스 작업을 할당 하는 hello 노드의 hello 나머지에 예약 된 tooexecute 됩니다.

## <a name="coordination-command"></a>조정 명령
hello **조정 명령** hello 기본과 하위 작업으로 실행 됩니다.

hello 조정 명령의 hello 호출을 차단 하 고-hello 조정 명령에 모든 하위 작업에 대 한 성공적으로 반환 될 때까지 일괄 처리 hello 응용 프로그램 명령을 실행 하지 않습니다. hello 조정 해야 따라서 모든 필요한 백그라운드 서비스를 시작, 사용 하기 위해 준비 되었는지 확인 명령과 다음 종료 합니다. 예를 들어이 조정 명령을 MS-MPI 버전 7 사용 하는 솔루션에 대 한 hello 노드에서 hello SMPD 서비스를 시작 하 여 다음 종료:

```
cmd /c start cmd /c ""%MSMPI_BIN%\smpd.exe"" -d
```

Hello 사용 `start` 이 조정 명령입니다. 때문에 이것이 필요 hello `smpd.exe` 실행 후 즉시 응용 프로그램을 반환 하지 않습니다. Hello hello 사용 하지 않고 [시작] [ cmd_start] 명령이 조정 명령은 반환 하지 않습니다는 따라서 hello 응용 프로그램 명령 실행을 차단 합니다.

## <a name="application-command"></a>응용 프로그램 명령
Hello 기본 작업에 의해 hello 다중 인스턴스 작업의 명령줄이 실행 hello 기본 작업 및 모든 하위 작업 실행이 완료 hello 조정 명령, 일단 *만*합니다. 이 hello 이라고 **응용 프로그램 명령** toodistinguish hello 조정 명령에서 합니다.

MS-MPI 응용 프로그램의 경우 사용 하 여 hello 응용 프로그램 명령 tooexecute MPI 사용이 가능한 응용 프로그램을 `mpiexec.exe`합니다. 예를 들어 MS-MPI 버전 7을 사용하는 솔루션에 대한 응용 프로그램 명령은 다음과 같습니다.

```
cmd /c ""%MSMPI_BIN%\mpiexec.exe"" -c 1 -wdir %AZ_BATCH_TASK_SHARED_DIR% MyMPIApplication.exe
```

> [!NOTE]
> 때문에 MS-MPI의 `mpiexec.exe` 사용 하 여 hello `CCP_NODES` 기본적으로 변수 (참조 [환경 변수](#environment-variables)) hello 예제 응용 프로그램 명령줄에서 제외 합니다.
>
>

## <a name="environment-variables"></a>환경 변수
일괄 처리를 여러 개 만들어 [환경 변수] [ msdn_env_var] hello에 있는 특정 toomulti 인스턴스 작업 계산 노드 tooa 다중 인스턴스 작업을 할당 합니다. 스크립트와 실행 프로그램 hello 수 조정 및 응용 프로그램 명령줄에 이러한 환경 변수를 참조할 수 있습니다.

hello 다음과 같은 환경 변수는 사용 하기 위해 hello 일괄 처리 서비스에서로 만들어집니다 다중 인스턴스 작업.

* `CCP_NODES`
* `AZ_BATCH_NODE_LIST`
* `AZ_BATCH_HOST_LIST`
* `AZ_BATCH_MASTER_NODE`
* `AZ_BATCH_TASK_SHARED_DIR`
* `AZ_BATCH_IS_CURRENT_NODE_MASTER`

이러한 이벤트에 대해 전체 내용과 hello에 대 한 다른 일괄 처리 계산 노드 환경 변수, 해당 내용 및 표시 여부를 포함 하 여 참조 [노드 환경 변수 계산][msdn_env_var]합니다.

> [!TIP]
> hello 일괄 처리 Linux MPI 코드 예제는 다양 한 이러한 환경 변수 사용 방법의 예가 포함 되어 있습니다. hello [조정 cmd] [ coord_cmd_example] Bash 스크립트 Azure 저장소에서 공통 응용 프로그램 및 입력된 파일을 다운로드 hello 마스터 노드에서 네트워크 파일 시스템 (NFS) 공유를 사용 하 고 구성에 다른 노드 hello NFS 클라이언트로 toohello 다중 인스턴스 작업을 할당 합니다.
>
>

## <a name="resource-files"></a>리소스 파일
두 가지 방법으로 다중 인스턴스 작업에 대 한 리소스 파일 tooconsider 종류가: **공용 리소스 파일** 하 *모든* 작업 다운로드 (기본 및 하위 작업), 및 hello **리소스파일** hello 다중 인스턴스 작업 자체는 지정 된 *hello 기본만* 다운로드 작업 합니다.

하나 이상 지정할 수 **공용 리소스 파일** 작업에 대 한 hello 다중 인스턴스 설정 합니다. 이러한 일반적인 리소스 파일에서 다운로드 한 [Azure 저장소](../storage/common/storage-introduction.md) 를 각 노드에 **작업 공유 디렉터리** hello 기본 및 모든 하위 작업으로 합니다. Hello를 사용 하 여 응용 프로그램 및 조정 명령줄에서 hello 작업 공유 디렉터리를 액세스할 수 있습니다 `AZ_BATCH_TASK_SHARED_DIR` 환경 변수입니다. hello `AZ_BATCH_TASK_SHARED_DIR` 경로 모든 노드에 할당 된 toohello 다중 인스턴스 작업에서 동일한, 따라서 hello 기본 및 모든 하위 작업 간의 단일 조정 명령을 공유할 수 있습니다. 일괄 처리 "를 공유 하지 않습니다" hello 디렉터리에 원격 액세스 의미 하지만 지점을 hello 팁 환경 변수에서 설명한 것 처럼 공유 하거나 마운트도 사용할 수 있습니다.

Hello 다중 인스턴스 작업 자체는 다운로드 한 toohello 작업의 작업 디렉터리를 지정 하는 리소스 파일 `AZ_BATCH_TASK_WORKING_DIR`, 기본적으로 합니다. 앞서 언급 했 듯이 반대로 toocommon 리소스 파일만 hello 주 작업 다운로드 hello 다중 인스턴스 작업 자체에 대해 지정 된 리소스 파일 합니다.

> [!IMPORTANT]
> 항상 hello 환경 변수를 사용 하 여 `AZ_BATCH_TASK_SHARED_DIR` 및 `AZ_BATCH_TASK_WORKING_DIR` 명령 줄에서 toorefer toothese 디렉터리입니다. 수동으로 tooconstruct hello 경로 시도 하지 마십시오.
>
>

## <a name="task-lifetime"></a>작업 수명
hello hello 전체 다중 인스턴스 작업의 기본 작업 컨트롤 hello 수명의 hello 수명입니다. 기본 hello 종료 될 때 모든 hello 하위 작업의 종료 됩니다. 기본 hello hello 종료 코드 hello 작업의 종료 코드 hello 이며 따라서 재시도 위해 hello 작업의 사용 되는 toodetermine hello 성공 또는 실패 합니다.

Hello 하위 작업 중 하나라도 실패, 0이 아닌 반환 코드와 함께 종료 예를 들어 hello 전체 다중 인스턴스 태스크가 실패 합니다. hello 다중 인스턴스 작업 종료 되어 tooits 다시 시도 한도를 다시 시도 합니다.

다중 인스턴스 작업을 삭제 하면 주 hello 및 모든 하위 hello 일괄 처리 서비스에서도 삭제 됩니다. 모든 하위 디렉터리 및 hello 계산 노드는 표준 작업의 경우 처럼에서 해당 파일을 삭제 합니다.

[TaskConstraints] [ net_taskconstraints] hello 등의 다중 인스턴스 작업에 대 한 [MaxTaskRetryCount][net_taskconstraint_maxretry], [MaxWallClockTime] [ net_taskconstraint_maxwallclock], 및 [RetentionTime] [ net_taskconstraint_retention] 속성을 적용 되는 표준 작업 되 고 toohello 적용 주 파일 그룹 및 하위 작업을 모두 합니다. 그러나 hello를 변경 하는 경우 [RetentionTime] [ net_taskconstraint_retention] 후 hello 다중 인스턴스 작업 toohello 작업,이 변경 내용을 추가 하는 속성은 적용 된 유일한 toohello 주 작업 합니다. Hello 하위 작업의 모든 계속 toouse hello 원래 [RetentionTime][net_taskconstraint_retention]합니다.

계산 노드의 최근 작업 목록 hello 최근 작업에는 다중 인스턴스 작업의 일부 였던 경우 하위 작업의 hello id를 반영 합니다.

## <a name="obtain-information-about-subtasks"></a>하위 작업에 대한 정보 가져오기
hello 일괄 처리.NET 라이브러리를 호출 hello를 사용 하 여 하위 작업에 tooobtain 정보 [CloudTask.ListSubtasks] [ net_task_listsubtasks] 메서드. 이 메서드는 모든 하위 작업에 정보를 반환 하 고 hello에 대 한 정보 hello 작업을 실행 하는 노드를 계산 합니다. 이 정보를 각 하위 작업의 루트 디렉터리, hello 풀 id, 현재 상태, 종료 코드를 등을 확인할 수 있습니다. 이 정보를 사용 하 여 hello와 함께에서 [PoolOperations.GetNodeFile] [ poolops_getnodefile] 메서드 tooobtain hello 하위 작업의 파일입니다. 참고가이 메서드 hello 기본 작업 (id 0)에 대 한 정보를 반환 하지 않습니다.

> [!NOTE]
> 작동 하는 일괄 처리.NET 메서드 다중 인스턴스 hello 따로 명시 하지 않는 [CloudTask] [ net_task] 적용 자체 *만* toohello 주 작업 합니다. 예를 들어 호출 하는 경우 hello [CloudTask.ListNodeFiles] [ net_task_listnodefiles] 는 다중 인스턴스 작업에서 메서드를 hello 주 작업 파일에만 반환 됩니다.
>
>

hello 만드는 코드는 어떻게 tooobtain 정보, 하위 작업으로 실행 된 hello 노드에서 파일 콘텐츠를 요청 합니다.

```csharp
// Obtain hello job and hello multi-instance task from hello Batch service
CloudJob boundJob = batchClient.JobOperations.GetJob("mybatchjob");
CloudTask myMultiInstanceTask = boundJob.GetTask("mymultiinstancetask");

// Now obtain hello list of subtasks for hello task
IPagedEnumerable<SubtaskInformation> subtasks = myMultiInstanceTask.ListSubtasks();

// Asynchronously iterate over hello subtasks and print their stdout and stderr
// output if hello subtask has completed
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

## <a name="code-sample"></a>코드 샘플
hello [MultiInstanceTasks] [ github_mpi] GitHub에서 코드 샘플 toouse 다중 인스턴스 toorun 작업 하는 방법을 보여 줍니다.는 [MS-MPI] [ msmpi_msdn] 일괄 처리 계산 노드에서 응용 프로그램입니다. Hello 단계에 따라 [준비](#preparation) 및 [실행](#execution) toorun hello 예제입니다.

### <a name="preparation"></a>준비
1. Hello 처음 두 단계에 따라 [어떻게 toocompile 간단한 MS-MPI 프로그램 실행 및][msmpi_howto]합니다. 이 단계를 수행 하는 hello에 대 한 hello prerequesites 충족 합니다.
2. 빌드는 *릴리스* 버전의 hello [MPIHelloWorld] [ helloworld_proj] MPI 프로그램 예제입니다. Hello 다중 인스턴스 작업에 의해 계산 노드에서 실행 되는 hello 프로그램입니다.
3. `MPIHelloWorld.exe`(2단계에서 빌드) 및 `MSMpiSetup.exe`(1단계에서 다운로드)를 포함하는 Zip 파일을 만듭니다. Hello 다음 단계에서 응용 프로그램 패키지로이 zip 파일을 업로드 합니다.
4. 사용 하 여 hello [Azure 포털] [ portal] toocreate 일괄 처리 [응용 프로그램](batch-application-packages.md) "MPIHelloWorld"를 호출 하 고 hello zip 파일의 버전 "1.0"으로 hello 이전 단계에서 만든를 지정 합니다. hello 응용 프로그램 패키지입니다. 자세한 내용은 [응용 프로그램 업로드 및 관리](batch-application-packages.md#upload-and-manage-applications)를 참조하세요.

> [!TIP]
> 빌드는 *릴리스* 버전의 `MPIHelloWorld.exe` tooinclude 모든 추가 종속성이 없는 있도록 (예를 들어 `msvcp140d.dll` 또는 `vcruntime140d.dll`) 응용 프로그램 패키지에 있습니다.
>
>

### <a name="execution"></a>실행
1. Hello 다운로드 [azure 일괄 처리-샘플] [ github_samples_zip] GitHub에서 합니다.
2. 열기 hello MultiInstanceTasks **솔루션** Visual Studio 2015에서 이상 버전입니다. hello `MultiInstanceTasks.sln` 솔루션 파일은:

    `azure-batch-samples\CSharp\ArticleProjects\MultiInstanceTasks\`
3. 자격 증명을 입력 일괄 처리 및 저장소 계정에서 `AccountSettings.settings` hello에 **Microsoft.Azure.Batch.Samples.Common** 프로젝트.
4. **빌드 및 실행** hello MultiInstanceTasks 솔루션 tooexecute hello MPI 샘플 응용 프로그램에서의 계산 노드 배치 풀 합니다.
5. *선택적*: 사용 하 여 hello [Azure 포털] [ portal] 또는 hello [일괄 처리 탐색기] [ batch_explorer] tooexamine hello 샘플 풀, 작업, 및 작업 ("MultiInstanceSamplePool", "MultiInstanceSampleJob", "MultiInstanceSampleTask") 하기 전에 hello 리소스를 삭제 합니다.

> [!TIP]
> Visual Studio가 없는 경우 [Visual Studio 커뮤니티][visual_studio]를 무료로 다운로드할 수 있습니다.
>
>

출력 `MultiInstanceTasks.exe` toohello 다음과 유사 합니다.

```
Creating pool [MultiInstanceSamplePool]...
Creating job [MultiInstanceSampleJob]...
Adding task [MultiInstanceSampleTask] toojob [MultiInstanceSampleJob]...
Awaiting task completion, timeout in 00:30:00...

Main task [MultiInstanceSampleTask] is in state [Completed] and ran on compute node [tvm-1219235766_1-20161017t162002z]:
---- stdout.txt ----
Rank 2 received string "Hello world" from Rank 0
Rank 1 received string "Hello world" from Rank 0

---- stderr.txt ----

Main task completed, waiting 00:00:10 for subtasks toocomplete...

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

Sample complete, hit ENTER tooexit...
```

## <a name="next-steps"></a>다음 단계
* hello Microsoft HPC 및 일괄 처리 Azure 팀 블로그 설명 [MPI Azure 일괄 처리에서 Linux에 대 한 지원][blog_mpi_linux], 사용 정보를 포함 하 고 [OpenFOAM] [ openfoam] 일괄 처리 합니다. Hello에 대 한 Python 코드 샘플을 확인할 수 [GitHub에서 OpenFOAM 예제][github_mpi]합니다.
* 너무 방법에 대해 알아봅니다[Linux 계산 노드는 풀을 만들](batch-linux-nodes.md) Azure 일괄 처리 MPI 솔루션에서 사용 하기 위해 합니다.

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

---
title: "aaaCreate tooprepare 작업과 계산 노드의-Azure 일괄 처리 완료 작업을 작업 | Microsoft Docs"
description: "사용 하 여 작업 수준 준비 작업 toominimize 데이터 전송 tooAzure 일괄 처리 계산 노드 및 노드 정리 작업 완료 시에 대 한 작업을 해제 합니다."
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
ms.openlocfilehash: fd5fb47ae6700281e63048c49a1241f4e935baba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="run-job-preparation-and-job-release-tasks-on-batch-compute-nodes"></a>Batch 계산 노드에서 작업 준비 및 작업 릴리스 태스크 실행

 가끔씩 Azure Batch 작업에는 실행되기 전에 특정 형식으로 구성된 설정과 해당 작업이 완료된 이후의 사후 작업 유지 관리가 필요합니다. Toodownload 공통 작업 입력된 데이터 tooyour 계산 노드를 필요 하거나 hello 작업이 완료 된 후에 작업 출력 데이터 tooAzure 저장소를 업로드할 수 있습니다. 사용할 수 있습니다 **준비 작업** 및 **릴리스 작업** tooperform 이러한 작업을 작업 합니다.

## <a name="what-are-job-preparation-and-release-tasks"></a>작업 준비 및 해제 태스크에 대한 정의
작업의 작업을 실행 하기 전에 hello 작업 준비 태스크 적어도 하나 이상의 태스크를 모든 계산 노드 예약된 toorun에서 실행 됩니다. Hello 작업이 완료 되 면 하나 이상의 작업을 실행 하는 hello 풀의 각 노드에서 hello 작업 릴리스 작업을 실행 합니다. 기본 일괄 처리 작업에서와 마찬가지로 작업 준비 될 때 호출 명령줄 toobe를 지정할 수 있습니다 또는 "릴리스" 작업을 실행 합니다.

작업 준비 및 해제 태스크는 파일([리소스 파일][net_job_prep_resourcefiles]) 다운로드, 관리자 권한 실행, 사용자 지정 환경 변수, 최대 실행 기간, 재시도 횟수 및 파일 보존 시간과 같은 익숙한 Batch 태스크 기능을 제공합니다.

다음 섹션 hello, 알아봅니다 어떻게 toouse hello [JobPreparationTask] [ net_job_prep] 및 [JobReleaseTask] [ net_job_release] hello에서 찾을 수 클래스 [일괄 처리.NET] [ api_net] 라이브러리입니다.

> [!TIP]
> 계산 노드 풀이 작업 실행 간에 지속되고 여러 작업에서 사용되는 "공유 풀" 환경에서는 작업 준비 및 해제 태스크가 특히 유용합니다.
> 
> 

## <a name="when-toouse-job-preparation-and-release-tasks"></a>Toouse 준비 작업 하 고 작업을 해제 하는 경우
준비 작업 및 작업 릴리스 작업은 hello 다음 상황에 가장 잘 맞는:

**공통 태스크 데이터 다운로드**

일괄 처리 작업은 일반적 hello 작업의 작업에 대 한 입력으로는 공통 데이터 집합이 필요합니다. 예를 들어 매일 위험 분석 계산에서 시장 데이터는 hello 작업에서 작업 관련 아직 일반적인 tooall 작업. Hello 노드에서 실행 되는 모든 작업에서 사용할 수 있도록이 시장 데이터를 자주 몇 기가바이트 크기의 계산 노드에 다운로드 한 tooeach은 한 번만 되어야 합니다. 사용 하 여 한 **태스크를 준비 하는 작업** toodownload hello 작업의 hello 실행의 다른 작업 전에이 데이터 tooeach 노드.

**작업 및 태스크 출력 삭제**

풀의 계산 노드 되지 않는 작업 간에 서비스 해제 됨, "풀을 공유 합니다." 환경에서 실행 간에 toodelete 작업 데이터를 할 수 있습니다. Tooconserve 해야 hello 노드에 디스크 공간이 또는 조직의 보안 정책을 충족 합니다. 사용 하 여 한 **작업 "릴리스" 작업** toodelete 데이터 작업 준비 태스크 다운로드할 되었거나 중에 생성 된 작업을 실행 합니다.

**로그 보존**

작업 생성 하는 로그 파일 또는 아마도 크래시 덤프 파일의 실패 한 응용 프로그램에 의해 생성 될 수 있는 복사본 tookeep을 할 수 있습니다. 사용 하 여는 **작업 그룹 작업** 이러한 경우 toocompress에이 데이터 tooan 업로드 [Azure 저장소] [ azure_storage] 계정.

> [!TIP]
> 또 다른 방법은 toopersist 로그 및 기타 작업 및 작업 출력 데이터는 toouse hello [Azure 일괄 처리 파일 규칙](batch-task-output.md) 라이브러리입니다.
> 
> 

## <a name="job-preparation-task"></a>작업 준비 태스크
작업의 작업을 실행 하기 전에 일괄 처리는 예약 된 작업 toorun 각 계산 노드에 hello 작업 준비 작업을 실행 합니다. 기본적으로 hello 일괄 처리 서비스는 hello 작업 준비 작업 toobe hello 작업 예약 된 tooexecute hello 노드를 실행 하기 전에 완료에 대 한 대기 합니다. 그러나 하지 toowait hello 서비스를 구성할 수 있습니다. Hello 노드 다시 시작 되 면 hello 작업 준비 작업을 다시 실행 하지만이 동작을 비활성화할 수 있습니다.

hello 작업 준비 작업은 예약 된 toorun 작업 중인 노드가에 대해서만 실행 됩니다. 이 노드는 작업을 할당 되지 않은 경우 hello 불필요 한 준비 작업을 실행할을 수 없습니다. 이 작업에 대 한 작업의 hello 수는 풀의 노드 수가 hello 보다 작은 경우 발생할 수 있습니다. 또한 적용 될 때 [동시 작업 실행](batch-parallel-node-tasks.md) 를 사용 하는 생략 된 일부 노드 유휴 hello 작업 수 hello 총 가능한 동시 작업이 보다 낮은 경우. 유휴 노드에서 hello 작업 준비 작업을 실행 하지 않으면, 적은 비용에는 데이터 전송 비용이 소요 단축할 수 있습니다.

> [!NOTE]
> [JobPreparationTask] [ net_job_prep_cloudjob] 에서 다른 [CloudPool.StartTask] [ pool_starttask] JobPreparationTask 반면 각 작업의 hello 시작 될 때 실행 된다는 점에서 StartTask 만 때 계산 노드에 처음 연결할 풀을 실행 하거나 다시 시작 합니다.
> 
> 

## <a name="job-release-task"></a>작업 해제 태스크
작업이 완료 된 것으로 표시 되 면 hello 작업 릴리스 작업은 하나 이상의 작업을 실행 하는 hello 풀의 각 노드에서 실행 됩니다. 종료 요청을 발행하여 작업을 완료로 표시합니다. 집합 작업 상태를 너무 hello 다음 일괄 처리 서비스 hello*종료*hello 작업과 연결 된 모든 활성 또는 실행 중인 작업을 종료 하 고 hello 작업 릴리스 작업을 실행 합니다. hello 작업에는 다음 toohello 이동 *완료* 상태입니다.

> [!NOTE]
> 또한 작업 삭제 hello 작업 릴리스 작업을 실행합니다. 그러나 작업이 이미 종료 된 경우 hello 릴리스 작업 실행 되지 않습니다를 두 번째로 hello 작업이 나중에 삭제 됩니다.
> 
> 

## <a name="job-prep-and-release-tasks-with-batch-net"></a>배치 .NET을 사용한 작업 준비 및 릴리스 태스크
toouse 작업 준비 작업을 할당 한 [JobPreparationTask] [ net_job_prep] 개체 tooyour 작업 [CloudJob.JobPreparationTask] [ net_job_prep_cloudjob] 속성 . 마찬가지로, 초기화는 [JobReleaseTask] [ net_job_release] tooyour 작업의 할당 및 [CloudJob.JobReleaseTask] [ net_job_prep_cloudjob] 속성 tooset hello 작업의 릴리스 작업입니다.

이 코드 조각에서는 `myBatchClient` 의 인스턴스가 [BatchClient][net_batch_client], 및 `myPool` hello 일괄 처리 계정 내에서 기존 풀 됩니다.

```csharp
// Create hello CloudJob for CloudPool "myPool"
CloudJob myJob =
    myBatchClient.JobOperations.CreateJob(
        "JobPrepReleaseSampleJob",
        new PoolInformation() { PoolId = "myPool" });

// Specify hello command lines for hello job preparation and release tasks
string jobPrepCmdLine =
    "cmd /c echo %AZ_BATCH_NODE_ID% > %AZ_BATCH_NODE_SHARED_DIR%\\shared_file.txt";
string jobReleaseCmdLine =
    "cmd /c del %AZ_BATCH_NODE_SHARED_DIR%\\shared_file.txt";

// Assign hello job preparation task toohello job
myJob.JobPreparationTask =
    new JobPreparationTask { CommandLine = jobPrepCmdLine };

// Assign hello job release task toohello job
myJob.JobReleaseTask =
    new JobPreparationTask { CommandLine = jobReleaseCmdLine };

await myJob.CommitAsync();
```

앞서 언급 했 듯이 hello 릴리스 작업은 작업은 종료 되거나 삭제 될 때 실행 됩니다. [JobOperations.TerminateJobAsync][net_job_terminate]를 통해 작업을 종료합니다. [JobOperations.DeleteJobAsync][net_job_delete]를 통해 작업을 삭제합니다. 일반적으로 작업의 태스크들이 완료되거나 정의한 시간 제한에 도달했을 때 작업을 종료하거나 삭제합니다.

```csharp
// Terminate hello job toomark it as Completed; this will initiate the
// Job Release Task on any node that executed job tasks. Note that the
// Job Release Task is also executed when a job is deleted, thus you
// need not call Terminate if you typically delete jobs after task completion.
await myBatchClient.JobOperations.TerminateJobAsy("JobPrepReleaseSampleJob");
```

## <a name="code-sample-on-github"></a>GitHub의 코드 샘플
hello를 확인해 보세요 toosee 작업 준비 및 릴리스 작업 동작에서 [JobPrepRelease] [ job_prep_release_sample] GitHub에서 샘플 프로젝트입니다. 이 콘솔 응용 프로그램은 다음 hello지 않습니다.

1. "small" 노드가 두 개인 풀을 만듭니다.
2. 작업 준비, 릴리스 및 표준 태스크를 사용하여 작업을 만듭니다.
3. 실행 hello 작업 준비 태스크는 먼저 노드 "공유" 디렉터리에 hello 노드 ID tooa 텍스트 파일을 기록 합니다.
4. 작업을 실행 하는 작업 ID toohello를 작성 하는 각 노드에서 같은 텍스트 파일입니다.
5. 모든 작업이 완료 됩니다 (또는 hello 시간 제한에 도달) 되 면 각 노드의 텍스트 파일 toohello 콘솔의 hello 내용을 인쇄 합니다.
6. Hello 작업이 완료 되 면 hello 노드에서 hello 작업 릴리스 작업 toodelete hello 파일을 실행 합니다.
7. 인쇄 hello 종료 코드의 hello 작업 준비 및 실행 된 각 노드에 대 한 작업을 해제 합니다.
8. 일시 중지 실행 tooallow 작업 및/또는 풀 삭제 확인 합니다.

Hello 샘플 응용 프로그램의 출력은 유사한 toohello 다음:

```
Attempting toocreate pool: JobPrepReleaseSamplePool
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

Waiting for job JobPrepReleaseSampleJob tooreach state Completed
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

Sample complete, hit ENTER tooexit...
```

> [!NOTE]
> Toohello 변수 만들기 및 시작 시간 (일부 노드는 다른 대체 이전 작업에 대 한 준비) 하는 새 풀에 있는 노드의 인해 서로 다른 출력을 볼 수 있습니다. 특히 hello 작업을 신속 하 게 완료 하기 때문에 hello 작업의 작업을 모두 실행할 수 있습니다 hello 풀의 노드 중 하나입니다. 이 문제가 발생 하는 경우에 필수 구성 요소를 작업 하 고 작업을 해제 하는 hello 알 수 없는 작업을 실행 하는 hello 노드에 대 한 존재 하지 않습니다.
> 
> 

### <a name="inspect-job-preparation-and-release-tasks-in-hello-azure-portal"></a>작업 준비 및 hello Azure 포털의에서 릴리스 작업 검사
Hello 샘플 응용 프로그램을 실행 하면 hello를 사용할 수 있습니다 [Azure 포털] [ portal] tooview hello hello 작업 및 해당 태스크의 속성 또는 심지어 hello 작업의 작업에 의해 수정 된 hello 공유 텍스트 파일을 다운로드 합니다.

hello 아래 스크린샷은 hello **준비 작업 블레이드** hello hello 샘플 응용 프로그램의 실행 후 Azure 포털의에서. Toohello 이동 *JobPrepReleaseSampleJob* 속성 작업 완료 된 후 (하지만 작업 및 풀을 삭제 하기 전에)를 클릭 하 고 **준비 작업** 또는 **작업릴리스** tooview 속성입니다.

![Azure 포털에서 작업 준비 속성][1]

## <a name="next-steps"></a>다음 단계
### <a name="application-packages"></a>응용 프로그램 패키지
또한 toohello 작업 준비 작업에 사용할 수도 있습니다 hello [응용 프로그램 패키지](batch-application-packages.md) tooprepare 일괄 처리의 기능 작업 실행에 대 한 노드를 계산 합니다. 이 기능은 설치 관리자를 실행하지 않아도 되는 응용 프로그램, 100개 이상의 파일을 포함하는 응용 프로그램 또는 엄격한 버전 제어를 필요로 하는 응용 프로그램을 배포하는 데 특히 유용합니다.

### <a name="installing-applications-and-staging-data"></a>응용 프로그램 설치 및 데이터 준비
아래의 MSDN 포럼 게시물에서는 작업을 실행하기 위해 노드를 준비하는 여러 가지 방법을 간략히 제공합니다.

[Batch 계산 노드에서의 응용 프로그램 설치 및 데이터 스테이징][forum_post]

Hello Azure 일괄 처리 팀 멤버 중 하나를 기록한 toodeploy 응용 프로그램 및 데이터 toocompute 노드를 사용할 수 있는 몇 가지 방법을 설명 합니다.

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

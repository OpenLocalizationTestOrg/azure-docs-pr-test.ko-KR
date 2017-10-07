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
# <a name="create-task-dependencies-toorun-tasks-that-depend-on-other-tasks"></a>다른 작업에 종속 되는 toorun 작업 작업 종속성을 만듭니다

정의한 작업 종속성 toorun 작업 또는 작업 집합을 부모 작업이 완료 된 후에. 태스크 종속성이 유용한 몇 가지 시나리오는 다음과 같습니다.

* Hello 클라우드에서 MapReduce 스타일 작업 합니다.
* DAG(방향성 비순환 그래프)으로 표현할 수 있는 태스크의 데이터 처리 작업
* 미리 렌더링 및 렌더링 후 프로세스 hello 다음 작업을 시작 하기 전에 각 태스크를 완료 해야 합니다.
* 다른 작업 다운스트림 작업 hello 출력 업스트림 작업에 따라 다릅니다.

일괄 처리 작업 종속성이 있는 하나 이상의 부모 작업으로 hello 완료 한 후 계산 노드에서 실행을 위해 예약 된 작업을 만들 수 있습니다. 예를 들어, 별도의 병렬 태스크를 포함한 3D 동영상의 각 프레임을 렌더링하는 작업을 만들 수 있습니다. hello 최종 작업-hello "병합 작업"-렌더링 된 프레임을 hello 전체 동영상만 hello 결국 프레임이 병합이 성공적으로 렌더링 되었습니다.

기본적으로 종속 작업 hello 부모 작업이 성공적으로 완료 한 후에 실행 예약 됩니다. 종속성 동작 toooverride hello 기본 동작을 지정 하 고 hello 부모 작업이 실패할 경우 작업을 실행할 수 있습니다. Hello 참조 [종속성 동작](#dependency-actions) 자세한 내용은 섹션.  

일대일 또는 일대다 관계에서 다른 태스크에 따라 달라지는 태스크를 만들 수 있으며, 범위 종속 작업의 작업 Id의 지정된 된 범위 내에서 작업 그룹의 hello 완료에 종속 되는 위치를 만들 수 있습니다. 이러한 세 가지 기본 시나리오 toocreate 다 대 다 관계를 결합할 수 있습니다.

## <a name="task-dependencies-with-batch-net"></a>배치 .NET을 사용한 태스크 종속성
이 문서에서는 방법을 사용 하 여 작업 종속성 tooconfigure hello [일괄 처리.NET] [ net_msdn] 라이브러리입니다. 먼저 보여줍니다 너무 어떻게[작업 종속성을 사용 하도록 설정](#enable-task-dependencies) 사용자 작업에 너무 방법을 설명 하 고[종속성이 있는 작업을 구성할](#create-dependent-tasks)합니다. 또한 방식과 toospecify 종속성 동작 toorun 종속 작업 hello 부모 실패할 경우 설명 합니다. Hello에서는 마지막으로, [종속성 시나리오](#dependency-scenarios) 지 원하는 일괄 처리 합니다.

## <a name="enable-task-dependencies"></a>태스크 종속성 사용
일괄 처리 응용 프로그램에서 작업 종속성 toouse 먼저 hello 작업 toouse 작업 종속성 구성 해야 합니다. 일괄 처리.net에서에서 사용 하면 [CloudJob] [ net_cloudjob] 설정 하 여 해당 [UsesTaskDependencies] [ net_usestaskdependencies] 속성 너무`true`:

```csharp
CloudJob unboundJob = batchClient.JobOperations.CreateJob( "job001",
    new PoolInformation { PoolId = "pool001" });

// IMPORTANT: This is REQUIRED for using task dependencies.
unboundJob.UsesTaskDependencies = true;
```

코드 조각 앞 hello, "batchClient" hello의 인스턴스는 [BatchClient] [ net_batchclient] 클래스입니다.

## <a name="create-dependent-tasks"></a>종속성 태스크 만들기
하나 이상의 부모 작업의 hello 완료에 종속 된 작업 toocreate 작업 "에 따라 달라 집니다" hello를 hello 하는 다른 작업을 지정할 수 있습니다. 일괄 처리.net에서 구성 hello [CloudTask][net_cloudtask].[ DependsOn] [ net_dependson] hello의 인스턴스로 속성 [TaskDependencies] [ net_taskdependencies] 클래스:

```csharp
// Task 'Flowers' depends on completion of both 'Rain' and 'Sun'
// before it is run.
new CloudTask("Flowers", "cmd.exe /c echo Flowers")
{
    DependsOn = TaskDependencies.OnIds("Rain", "Sun")
},
```

이 코드 조각은 태스크 ID가 "Flowers"인 종속 태스크를 만듭니다. hello "꽃" 작업 작업에 따라 다름 "비"와 "일요일"입니다. 작업 "꽃" 작업 "비"와 "Sun"가 성공적으로 완료 한 후에 계산 노드에서 예약 된 toorun 됩니다.

> [!NOTE]
> 작업은 toobe hello에 있으면 성공적으로 완료 된 것으로 간주 됩니다 **완료** 상태 및 해당 **종료 코드** 은 `0`합니다. 즉 일괄 처리.NET에서는 [CloudTask][net_cloudtask].[ 상태] [ net_taskstate] 속성 값이 `Completed` CloudTask의 hello 및 [TaskExecutionInformation][net_taskexecutioninformation].[ ExitCode] [ net_exitcode] 속성 값은 `0`합니다.
> 
> 

## <a name="dependency-scenarios"></a>종속성 시나리오
Azure 배치에서 사용할 수 있는 세 가지 기본 태스크 종속성 시나리오는 일대일, 일대다 및 태스크 ID 범위 종속성입니다. 이들은 결합된 tooprovide 네 번째 시나리오에서는 다 대 다를 수 있습니다.

| 시나리오&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | 예 |  |
|:---:| --- | --- |
|  [일대일](#one-to-one) |*taskB*가 *taskA*에 종속됨 <p/> *taskB*는 *taskA*가 성공적으로 완료될 때까지 실행하도록 예약되지 않음 |![다이어그램: 일대일 태스크 종속성][1] |
|  [일대다](#one-to-many) |*taskC*는 *taskA* 및 *taskB*에 종속됨 <p/> *taskC*는 *taskA* 및 *taskB*가 성공적으로 완료될 때까지 실행하도록 예약되지 않음 |![다이어그램: 일대다 태스크 종속성][2] |
|  [태스크 ID 범위](#task-id-range) |*taskD*가 태스크의 범위에 종속됨 <p/> *taskD* hello 작업 Id 가진 될 때까지 실행을 위해 예약 되지 것입니다 *1* 통해 *10* 가 성공적으로 완료 |![다이어그램: 태스크 ID 범위 종속성][3] |

> [!TIP]
> 만들 수 있습니다 **다 대 다** C, D, E 및 F 각 작업 태스크 A와 B에 종속 되는 위치 등의 관계 이 값은 여기서 여러 업스트림 작업의 hello 출력에 따라 달라질 다운스트림 작업 병렬화 된 전처리 시나리오 등에서 유용 합니다.
> 
> 이 섹션의 예제는 hello hello 부모 작업이 성공적으로 완료 된 후에 종속 태스크가 실행 됩니다. 이 동작은 종속 작업에 대 한 hello 기본 동작에 설명 합니다. 종속 작업 종속성 동작 toooverride hello 기본 동작을 지정 하 여 부모 작업에 실패 한 후에 실행할 수 있습니다. Hello 참조 [종속성 동작](#dependency-actions) 자세한 내용은 섹션.

### <a name="one-to-one"></a>일대일
한 일 관계 작업 hello 하나의 부모 작업이 완료 되었는지에 따라 다릅니다. toocreate hello 종속성, 작업 ID toohello 제공 [TaskDependencies][net_taskdependencies].[ OnId] [ net_onid] hello를 채울 때 정적 메서드 [DependsOn] [ net_dependson] 속성 [CloudTask] [ net_cloudtask].

```csharp
// Task 'taskA' doesn't depend on any other tasks
new CloudTask("taskA", "cmd.exe /c echo taskA"),

// Task 'taskB' depends on completion of task 'taskA'
new CloudTask("taskB", "cmd.exe /c echo taskB")
{
    DependsOn = TaskDependencies.OnId("taskA")
},
```

### <a name="one-to-many"></a>일대다
1 대 다 관계 작업 여러 부모 작업의 hello 완료에 따라 다릅니다. toocreate hello 종속성, 작업 Id toohello의 컬렉션을 제공 [TaskDependencies][net_taskdependencies].[ OnIds] [ net_onids] hello를 채울 때 정적 메서드 [DependsOn] [ net_dependson] 속성 [CloudTask] [ net_cloudtask].

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

### <a name="task-id-range"></a>태스크 ID 범위
부모 작업의 범위에 대 한 종속성, 작업 Id 범위 내에 작업의 hello hello 완료에 따라 다릅니다.
toocreate hello 종속성 먼저 hello를 제공 하 고 마지막 범위 toohello hello에에서 ÷ Id [TaskDependencies][net_taskdependencies].[ OnIdRange] [ net_onidrange] hello를 채울 때 정적 메서드 [DependsOn] [ net_dependson] 속성 [CloudTask] [net_cloudtask].

> [!IMPORTANT]
> 종속성에 대 한 작업 ID 범위를 사용 하는 경우 hello hello 범위 내에 작업 Id *해야* 정수 값의 문자열 표현 이어야 합니다.
> 
> Hello 범위에서 모든 작업이 성공적으로 완료 하거나도 매핑된 tooa 종속성 작업은 오류와 함께 완료 하 여 hello 종속성을 충족 해야**Satisfy**합니다. Hello 참조 [종속성 동작](#dependency-actions) 자세한 내용은 섹션.
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

## <a name="dependency-actions"></a>종속성 작업

기본적으로 상위 태스크가 성공적으로 완료된 후에만 (일련의) 종속 태스크가 실행됩니다. 일부 시나리오에서는 hello 부모 작업에 실패 하는 경우에 toorun 종속 작업 수 있습니다. 종속성 동작을 지정 하 여 hello 기본 동작을 재정의할 수 있습니다. 종속 작업을 종속 작업 hello 부모 작업의 hello 성공 또는 실패에 따라, 적격 toorun 인지를 지정 합니다. 

예를 들어 종속 작업 데이터 hello hello 업스트림 작업 완료를 대기 중입니다. Hello 업스트림 작업에 실패 하면 hello 종속 작업은 오래 된 데이터를 사용 하 여 수 toorun를 수 있습니다. 이 경우 종속성 동작이 해당 hello 종속 작업은 적격 toorun hello 부모 작업의 hello 실패 불구 하 고 지정할 수 있습니다.

종속성 동작이 hello 부모 작업에 대 한 종료 조건을 기반으로 합니다. Hello 종료 조건을; 다음 중 하나에 대 한 종속성 동작을 지정할 수 있습니다. .NET 참조 hello [ExitConditions] [ net_exitconditions] 세부 정보에 대 한 클래스:

- 전처리 오류가 발생할 때
- 파일을 업로드 오류가 발생할 때 Hello 작업을 통해 지정 된 종료 코드로 종료 **exitCodes** 또는 **exitCodeRanges**, 다음 파일 업로드 오류, 종료 코드 hello 우선적으로 지정 된 hello 작업에서 발생 하 고 있습니다.
- Hello 작업 hello에 정의 된 종료 코드로 종료 될 때 **ExitCodes** 속성입니다.
- Hello 작업 hello로 지정 된 범위 내에 포함 되는 종료 코드로 종료 될 때 **ExitCodeRanges** 속성입니다.
- 기본적으로, hello 작업에 정의 되지 않은 종료 코드로 종료 되 면 hello **ExitCodes** 또는 **ExitCodeRanges**, 전처리 오류 및 hello 종료 될 hello 작업 또는 **PreProcessingError**  속성을 설정 하지 않으면 또는 작업 실패 하 고 파일 업로드 오류 및 hello 경우 hello **FileUploadError** 속성이 설정 되지 않았습니다. 

.net에서 집합 hello 종속성 동작이 toospecify [ExitOptions][net_exitoptions].[ 종속성] [ net_dependencyaction] hello 종료 조건에 대 한 속성입니다. hello **종속성** 속성은 두 값 중 하나를 사용 합니다.

- 설정 hello **종속성** 속성 너무**Satisfy** hello 부모 작업은 지정 된 오류 종료 되 면 종속 작업은 적격 toorun 나타냅니다.
- 설정 hello **종속성** 속성 너무**블록** 종속 작업 적격 toorun 되지 않습니다.

hello에 대 한 기본 설정은 hello **종속성** 속성은 **Satisfy** 종료 코드 0에 대 한 및 **블록** 다른 모든 종료 조건에 대 한 합니다.

hello 다음 코드 조각 설정 hello **종속성** 부모 작업에 대 한 속성입니다. 전처리 오류로 hello 부모 태스크가 종료 또는 hello로 지정 된 오류 코드를 환영 종속 작업이 차단 됩니다. 종속 작업 hello hello 부모 작업 다른 0이 아닌 오류와 함께 종료 경우 적격 toorun입니다.

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

## <a name="code-sample"></a>코드 샘플
hello [TaskDependencies] [ github_taskdependencies] 샘플 프로젝트를 사용 하면 hello 중 하나인 [Azure 배치 코드 샘플] [ github_samples] GitHub에서 합니다. 이 Visual Studio 솔루션은 다음 사항을 보여 줍니다.

- Tooenable 작업에 대 한 종속성을 작업 하는 방법
- 방식과 toocreate 작업 하는 다른 작업에 종속
- 어떻게 tooexecute 작업에서 계산 노드의 풀입니다.

## <a name="next-steps"></a>다음 단계
### <a name="application-deployment"></a>응용 프로그램 배포
hello [응용 프로그램 패키지](batch-application-packages.md) 쉽게 tooboth 배포 및 버전 hello 응용 프로그램에서 작업을 실행 하는 계산 노드 일괄 처리의 기능을 제공 합니다.

### <a name="installing-applications-and-staging-data"></a>응용 프로그램 설치 및 데이터 준비
참조 [응용 프로그램을 설치 하 고 일괄 처리에 대 한 데이터를 준비 하는 계산 노드] [ forum_post] hello Azure 배치 포럼 toorun 작업 노드를 준비 하기 위한 방법에 대 한 개요입니다. 이 게시물은 hello 다양 한 방법 toocopy 응용 프로그램에 좋은 입문서 hello Azure 일괄 처리 팀 멤버 중 하나에 의해 작성 작업 입력된 데이터를 다른 파일 tooyour 계산 노드.

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

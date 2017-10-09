---
title: "작업의 진행 상태를 계산 하 여 작업 상태-Azure 배치 하 여 aaaMonitor | Microsoft Docs"
description: "작업에 대 한 toocount 작업 hello 작업 개수 가져오기 작업을 호출 하 여 작업의 hello 진행률을 모니터링 합니다. 활성, 실행 중, 완료된 태스크 수는 물론, 성공 또는 성공한 태스크 수를 계산할 수 있습니다."
services: batch
author: tamram
manager: timlt
ms.service: batch
ms.topic: article
ms.date: 08/02/2017
ms.author: tamram
ms.openlocfilehash: 03957d8a3d678bf44587f3bc7f988a76885c2af0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="count-tasks-by-state-toomonitor-a-jobs-progress-preview"></a>Count는 작업의 진행 상황 (미리 보기) 하 여 상태 toomonitor 작업

Azure 일괄 처리 작업이 실행 되는 작업의 효율적인 방법을 toomonitor hello 진행 상태를 제공 합니다. Hello를 호출할 수 있습니다 [작업 개수 가져오기] [ rest_get_task_counts] 태스크 수는 현재 실행 중 또는 완료 된 상태에 있으며 수 있는 아웃 작업 toofind 성공 했는지 아니면 실패 합니다. Hello 각 상태에 있는 작업 수를 계산 하 여 hello 작업의 진행률 tooa 사용자를 표시 하거나 예기치 않은 지연이 나 hello 작업에 영향을 줄 수 있는 오류를 감지 보다 쉽게 있습니다.

> [!IMPORTANT]
> hello 작업 개수 가져오기 작업은 현재 미리 보기로, 및은 아직 Azure Government, Azure 중국 및 Azure 독일에 제공 합니다. 
>
>

## <a name="how-tasks-are-counted"></a>태스크 계산 방법

hello 작업 개수 가져오기 작업 상태를 사용 하 여 작업을 다음과 같이 계산:

- 로 계산 되는 작업 **활성** toorun, 지연 및 수는 있지만 tooa 계산 노드를 현재 할당 되지 않은 것입니다. 아직 완료되지 않은 상위 테스크에 종속된 태스크도 **활성**으로 계산됩니다. 작업 종속성에 대 한 자세한 내용은 참조 하십시오. [다른 작업에 종속 된 toorun 작업 작업 종속성을 만들고](batch-task-dependencies.md)합니다. 
- 로 계산 되는 작업 **실행** tooa 계산 노드에 할당 된 것 이지만 아직 완료 되지 않았습니다. 로 계산 되는 작업 **실행** 때 상태를 하나 `preparing` 또는 `running`hello에 표시 된 대로, [작업에 대 한 정보를 가져올] [ rest_get_task] 작업 합니다.
- 로 계산 되는 작업 **완료** 때 더 이상 toorun 적합 합니다. **완료**로 계산된 태스크는 일반적으로 성공적으로 완료되었거나, 비성공적으로 완료되었고 다시 시도 제한 횟수를 모두 사용했습니다. 

또한 작업 개수 가져오기 작업 hello 태스크 수는 성공 또는 실패를 보고 합니다. 일괄 처리 작업에 성공 했는지 아니면 hello를 확인 하 여 실패 하는지 여부를 결정 **결과** hello [executionInfo] [https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task#executionInfo]의 속성 속성:

    - 로 계산 되는 작업 **성공** 태스크 실행의 hello 결과가 `success`합니다.
    - 로 계산 되는 작업 **실패** 태스크 실행의 hello 결과가 `failure`합니다.

태스크 상태에 대한 자세한 내용은 [태스크에 대한 정보 가져오기][rest_get_task]를 참조하세요.

hello 다음.NET 보여 주는 코드 예제 방법을 상태별 tooretrieve 태스크 수를 계산 합니다. 

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
> REST에 대 한 유사한 패턴 및 tooget 작업 계산 작업에 대 한 기타 지원 되는 언어를 사용할 수 있습니다. 
> 
> 

## <a name="consistency-checking-for-task-counts"></a>태스크 수에 대한 일관성 확인

hello 일괄 처리 서비스는 비동기 분산형된 시스템의 여러 부분에서 데이터를 수집 하 여 작업 개수를 집계 합니다. 해당 개수를 작업 tooensure 올바른지, 일괄 처리 상태를 hello 시스템의 여러 구성 요소에 대 한 일관성 검사를 수행 하 여 계산에 대 한 추가 유효성 검사를 제공 합니다. 일괄 처리는 hello 작업 중인 200, 000 보다 작은 작업으로 이러한 일관성 검사를 수행 합니다. Hello 예기치 않은 이벤트가 hello 일관성 검사 오류를 발견, 일괄 처리는 hello hello 일관성 확인 결과에 따른 hello 작업 개수 가져오기 작업의 hello 결과 수정 합니다. hello 일관성 확인은 hello 작업 개수 가져오기 작업에 의존 하는 고객 받을 hello 적절 한 정보를 해당 솔루션에 대 한 필요한 하는 추가적인 tooensure 합니다.

hello **validationStatus** hello에 대 한 응답 속성 일괄 처리에 hello 일관성 검사를 수행할지 여부를 나타냅니다. 일괄 처리는 hello 시스템에 보관 하는 hello 실제 상태에 대 한 상태 개수 수 toocheck 되어 있지 않으면, 다음 hello **validationStatus** 너무 속성이`unvalidated`합니다. 성능상의 이유로 일괄 처리는 수행 하지 않습니다 hello hello 작업에 포함 된 경우 일관성 확인 및 둘 이상의 200000 작업, 따라서 hello **validationStatus** 너무 속성을 설정할 수`unvalidated` 이 경우. 그러나 hello 작업 개수가 않습니다 반드시 잘못 된 경우에 매우 제한 된 데이터 손실 가능성이 매우 아니므로. 

작업 상태가 변경 되 면 hello 집계 파이프라인 처리 몇 초 내 hello 변경 합니다. hello 작업 개수 가져오기 작업 기간 내에 업데이트 하는 hello 작업 수를 반영합니다. 그러나 hello 집계 파이프라인 누락 작업 상태 변경, 다음 변경 아닌지 등록할 hello 다음 유효성 검사 통과 될 때까지 합니다. 이 시간 동안 작업 개수 toohello 누락된 이벤트 인해 약간 정확 하지 않을 수 있지만 hello 다음 유효성 검사 과정에서 수정 됩니다.

## <a name="best-practices-for-counting-a-jobs-tasks"></a>작업의 태스크 수를 계산하는 모범 관행

Hello 가장 효율적인 방식으로 tooreturn 상태별 작업의 작업의 기본 수는 hello 작업 개수 가져오기 작업을 호출 합니다. 일괄 처리 서비스 버전 2017-06-01.5.1를 사용 하는 경우에 쓰기 또는 업데이트 작업의 개수를 가져오기 하 여 코드 toouse 것이 좋습니다.

hello 작업 개수 가져오기 작업에서에서 사용할 수 없는 일괄 처리 서비스 버전 2017-06-01.5.1 보다 이전입니다. 이전 버전의 hello 서비스를 사용 하는 경우 다음 목록 쿼리 toocount 작업의 작업을 대신 사용 합니다. 자세한 내용은 참조 [쿼리 toolist 일괄 처리 리소스를 효율적으로 만들](batch-efficient-list-queries.md)합니다.

## <a name="next-steps"></a>다음 단계

* Hello 참조 [배치 기능 개요](batch-api-basics.md) toolearn 일괄 처리 서비스 개념 및 기능에 대 한 자세한 합니다. hello 문서 hello 기본 일괄 처리 리소스 풀, 계산 노드, 작업, 작업 등을 설명 하 고 hello 서비스의 기능 개요를 제공 합니다.
* Hello를 사용 하 여 일괄 처리 사용이 가능한 응용 프로그램 개발의 hello 기본 사항 알아보기 [일괄 처리.NET 클라이언트 라이브러리](batch-dotnet-get-started.md) 또는 [Python](batch-python-tutorial.md)합니다. 이러한 소개 문서 과정을 안내 일괄 처리 서비스 tooexecute hello를 사용 하는 응용 프로그램 작업에 여러 계산 노드.


[rest_get_task_counts]: https://docs.microsoft.com/rest/api/batchservice/get-the-task-counts-for-a-job
[rest_get_task]: https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task
[rest_list_tasks]: https://docs.microsoft.com/rest/api/batchservice/list-the-tasks-associated-with-a-job

---
title: "aaaDesign 효율적인 목록 쿼리-Azure 일괄 처리 | Microsoft Docs"
description: "풀, 작업, 태스크 및 계산 노드와 같은 Batch 리소스에 대한 정보를 요청할 때 쿼리를 필터링하여 성능을 향상시킵니다."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 031fefeb-248e-4d5a-9bc2-f07e46ddd30d
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 08/02/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b7e554119ec9d0e9e8007ccfb1ca80fe142a5e27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-queries-toolist-batch-resources-efficiently"></a>쿼리 toolist 일괄 처리 리소스를 효율적으로 만들기

여기에 대해 배워 봅니다 tooincrease 방식과 hello 작업을 쿼리할 때 hello 서비스에서 반환 되는 데이터 양을 줄여 Azure 일괄 처리 응용 프로그램의 성능을 작업, 계산 노드 hello로 [일괄 처리.NET] [ api_net] 라이브러리입니다.

거의 모든 일괄 처리 응용 프로그램 tooperform 일종의 hello 일괄 처리 서비스를 정기적으로 자주 쿼리 하는 모니터링 또는 다른 작업을 필요 합니다. 예를 들어 toodetermine hello 작업에서 모든 작업에 데이터를 가져올 해야 작업에 남아 있는 큐에 대기 중인된 작업이 모두 있는지 여부. 풀의 노드의 toodetermine hello 상태를 hello 풀의 모든 노드에서 데이터를 가져올 해야 합니다. 이 문서에서는 어떻게 tooexecute 등의 쿼리 hello 설명 가장 효율적인 방법입니다.

> [!NOTE]
> hello 일괄 처리 서비스는 작업의 작업 수를 세 hello 일반적인 시나리오에 대 한 특별 한 API 지원을 제공 합니다. 이러한 목록 쿼리를 사용 하는 대신 hello를 호출할 수 있습니다 [작업 개수 가져오기] [ rest_get_task_counts] 작업 합니다. Get Task Counts 연산은 보류 중, 실행 중 또는 완료 태스크 수, 성공 또는 실패한 태스크 수를 나타냅니다. Get Task Counts는 목록 쿼리보다 더 효율적입니다. 자세한 내용은 [상태별 작업 계수(미리 보기)](batch-get-task-counts.md)를 참조하세요. 
>
> hello 작업 개수 가져오기 작업에서에서 사용할 수 없는 일괄 처리 서비스 버전 2017-06-01.5.1 보다 이전입니다. 이전 버전의 hello 서비스를 사용 하는 경우 다음 목록 쿼리 toocount 작업의 작업을 대신 사용 합니다.
>
> 

## <a name="meet-hello-detaillevel"></a>DetailLevel hello 충족
일괄 처리 응용 프로그램을 프로덕션 환경에서 작업, 작업 및 계산 노드 같은 엔터티 hello 수천의에서 번호 수 있습니다. 이러한 리소스에 대 한 정보를 요청할 때 잠재적으로 많은 양의 데이터 "걸쳐 hello 와이어" hello 일괄 처리 서비스 tooyour 응용 프로그램에서 각 쿼리에 대. 쿼리에 의해 반환 되는 정보 유형과 hello 항목 수를 제한 하 여 쿼리의 hello 속도 높일 수 있으며 따라서 응용 프로그램의 성능을 hello 수 있습니다.

이 [일괄 처리.NET] [ api_net] API 코드 조각 목록 *모든* 와 함께 작업을 연관 된 작업 *모든* 각 hello 속성 작업:

```csharp
// Get a collection of all of hello tasks and all of their properties for job-001
IPagedEnumerable<CloudTask> allTasks =
    batchClient.JobOperations.ListTasks("job-001");
```

그러나에 "세부 정보 수준" tooyour 쿼리를 적용 하 여 훨씬 더 효율적인 목록 쿼리를 수행할 수 있습니다. 제공 하 여이 작업을 수행는 [ODATADetailLevel] [ odata] toohello 개체 [JobOperations.ListTasks] [ net_list_tasks] 메서드. 이 코드 조각 hello ID, 명령줄 및 완료 된 작업의 계산 노드 정보 속성을 반환합니다.

```csharp
// Configure an ODATADetailLevel specifying a subset of tasks and
// their properties tooreturn
ODATADetailLevel detailLevel = new ODATADetailLevel();
detailLevel.FilterClause = "state eq 'completed'";
detailLevel.SelectClause = "id,commandLine,nodeInfo";

// Supply hello ODATADetailLevel toohello ListTasks method
IPagedEnumerable<CloudTask> completedTasks =
    batchClient.JobOperations.ListTasks("job-001", detailLevel);
```

이 예제 시나리오에는 수천 개의 hello 작업에서 작업 하는 경우 hello hello 두 번째 쿼리에서 일반적으로 됩니다 먼저 반환 hello 보다 훨씬 빠릅니다. Hello 일괄 처리.NET API로 항목을 나열 하는 경우 ODATADetailLevel 사용에 대 한 자세한 정보가 포함 되어 [아래](#efficient-querying-in-batch-net)합니다.

> [!IMPORTANT]
> 항상 좋습니다 있습니다 *항상* ODATADetailLevel 개체 tooyour.NET API 목록 호출 tooensure 최대 효율성과 응용 프로그램의 성능을 제공 합니다. 세부 수준을 지정 하 여 서비스 응답 시간 일괄 처리, 네트워크 사용률을 향상 시키고 클라이언트 응용 프로그램에서 메모리 사용을 최소화 toolower를 도울 수 있습니다.
> 
> 

## <a name="filter-select-and-expand"></a>Filter, select 및 expand
hello [일괄 처리.NET] [ api_net] 및 [배치 REST] [ api_rest] Api 제공 hello 기능 tooreduce 목록으로 반환 되는 항목의 두 hello 수 hello 메모리 양과 각각에 대해 반환 되는 정보입니다. 이렇게 하려면 목록 쿼리를 수행할 때 **filter**, **select** 및 **expand 문자열**을 지정합니다.

### <a name="filter"></a>Filter
hello 필터 문자열은 hello 반환 되는 항목 수가 감소 하는 식입니다. 예를 들어 목록만 hello는 작업 또는 목록만 컴퓨터 노드를 준비 toorun 작업에 대 한 작업을 실행 합니다.

* 필터 문자열 hello 속성 이름, 연산자 및 값으로 구성 되는 식으로 하나 이상의 식으로 구성 됩니다. 지정할 수 있는 hello 속성은 각 속성에 지원 되는 hello 연산자 이므로 쿼리하면 특정 tooeach 엔터티 형식입니다.
* 여러 개의 식을 hello 논리 연산자를 사용 하 여 결합할 수 있습니다 `and` 및 `or`합니다.
* 이 예제에서는 필터 문자열 목록 hello 실행 "작업을 렌더링"만: `(state eq 'running') and startswith(id, 'renderTask')`합니다.

### <a name="select"></a>여기서
select 문자열 hello 각 항목에 대해 반환 되는 hello 속성 값을 제한 합니다. 속성 이름 목록을 지정 하 고 hello 항목 hello 쿼리 결과에 대 한 속성 값만 반환 됩니다.

* hello select 문자열 속성 이름의 쉼표로 구분 된 목록으로 이루어져 있습니다. 쿼리 중인 hello 엔터티 형식에 대 한 hello 속성을 지정할 수 있습니다.
* `id, state, stateTransitionTime` select 문자열 예제는 각 태스크에 대해 반환되어야 하는 세 가지 속성 값만 지정하고 있습니다.

### <a name="expand"></a>Expand
hello 확장 문자열 hello 수 필요한 tooobtain 된 API 호출의 특정 정보를 줄일 수 있습니다. expand 문자열을 사용하면 단일 API 호출로 각 항목에 대한 자세한 정보를 얻을 수 있습니다. 확장 문자열을 사용 하면 첫 번째 얻으려면 hello 목록 엔터티, 아니면 hello 목록의 각 항목에 대 한 정보를 요청 하는 대신 tooobtain hello 단일 API 호출에서 동일한 정보입니다. API 호출이 적어지면 성능이 향상되었음을 의미합니다.

* 비슷한 toohello 선택 문자열 hello 특정 데이터 목록 쿼리 결과에 포함 되어 있는지 여부를 문자열 컨트롤을 확장 합니다.
* hello 확장 문자열 작업, 작업 일정, 작업 및 풀 나열에 사용 되는 경우에 지원 합니다. 현재 통계 정보만 지원합니다.
* 모든 속성은 필수 및 선택 문자열을 지정 하지, hello 확장 문자열 *해야* 통계 정보를 사용 하는 tooget 수입니다. Select 문자열은 사용 되는 속성의 하위 집합 tooobtain `stats` hello 선택 문자열에 지정할 수 있으며 hello 확장 문자열 toobe 지정할 필요는 없습니다.
* 이 예에서는 확장 문자열 hello 목록의 각 항목에 대 한 통계 정보가 반환 되어야 함을 지정: `stats`합니다.

> [!NOTE]
> 3 개의 쿼리 문자열 유형에 hello 중 하나를 생성할 때 (필터를 선택 하 고 확장), hello 속성 이름과 대/소문자 일치의 REST API 요소 대응 하는지 확인 해야 합니다. 예를 들어 작업할 때는 hello.NET [CloudTask](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask) 지정 해야 클래스 **상태** 대신 **상태**hello.NET 속성은 경우에 [ CloudTask.State](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.state)합니다. 속성 매핑 간의 hello.NET 및 REST Api에 대 한 아래 hello 테이블을 참조 하십시오.
> 
> 

### <a name="rules-for-filter-select-and-expand-strings"></a>filter, select, expand 문자열 규칙
* 속성 이름 필터에서 선택한 문자열 확장 hello에서와 마찬가지로 나타나야 [배치 REST] [ api_rest] API-사용 하는 경우에 [일괄 처리.NET] [ api_net] 또는 다른 일괄 처리 Sdk hello 중 하나입니다.
* 모든 속성 이름은 대/소문자를 구분하지만, 속성 값은 대/소문자를 구분하지 않습니다.
* 날짜/시간 문자열은 두 형식 중 하나가 될 수 있으며 `DateTime`으로 시작해야 합니다.
  
  * W3C-DTF 형식 예제: `creationTime gt DateTime'2011-05-08T08:49:37Z'`
  * RFC 1123 형식 예제: `creationTime gt DateTime'Sun, 08 May 2011 08:49:37 GMT'`
* 부울 문자열은 `true` 또는 `false`입니다.
* 잘못된 속성이나 연산자를 지정한 경우 `400 (Bad Request)` 오류가 발생합니다.

## <a name="efficient-querying-in-batch-net"></a>Batch .NET에서 효율적인 쿼리
Hello 내 [일괄 처리.NET] [ api_net] API, hello [ODATADetailLevel] [ odata] 클래스 제공 하는 필터를 사용 하 고를 선택한 문자열 확장 toolist 작업입니다. hello ODataDetailLevel 클래스 hello 생성자에 지정 된 또는 hello 개체에 직접 설정할 수 있는 세 가지 공용 문자열 속성에 있습니다. 그런 다음 hello ODataDetailLevel 개체 변수로 전달 매개 변수 toohello 다양 한 작업 나열와 같은 [ListPools][net_list_pools], [ListJobs][net_list_jobs], 및 [ListTasks][net_list_tasks]합니다.

* [ODATADetailLevel][odata].[ FilterClause][odata_filter]: hello 반환 되는 항목 수를 제한 합니다.
* [ODATADetailLevel][odata].[SelectClause][odata_select]: 각 항목에 반환되는 속성 값을 지정합니다.
* [ODATADetailLevel][odata].[ExpandClause][odata_expand]: 각 항목에 대한 별도 호출 대신 단일 API 호출의 모든 항목에 대한 데이터를 검색합니다.

hello 다음 코드 조각에서는 hello 일괄 처리.NET API tooefficiently 쿼리 hello 일괄 처리 서비스 풀의 특정 집합의 hello 통계에 대 한 합니다. 이 시나리오에서는 hello 일괄 사용자 테스트 환경과 프로덕션 풀에 있습니다. "test" 라는 접두사가 hello 테스트 풀 Id 및 hello 프로덕션 풀 Id "prod" 접두사로 붙습니다. Hello 코드 조각에서 *myBatchClient* hello는 올바르게 초기화 된 인스턴스가 [BatchClient](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient) 클래스입니다.

```csharp
// First we need an ODATADetailLevel instance on which tooset hello filter, select,
// and expand clause strings
ODATADetailLevel detailLevel = new ODATADetailLevel();

// We want toopull only hello "test" pools, so we limit hello number of items returned
// by using a FilterClause and specifying that hello pool IDs must start with "test"
detailLevel.FilterClause = "startswith(id, 'test')";

// toofurther limit hello data that crosses hello wire, configure hello SelectClause to
// limit hello properties that are returned on each CloudPool object tooonly
// CloudPool.Id and CloudPool.Statistics
detailLevel.SelectClause = "id, stats";

// Specify hello ExpandClause so that hello .NET API pulls hello statistics for the
// CloudPools in a single underlying REST API call. Note that we use hello pool's
// REST API element name "stats" here as opposed too"Statistics" as it appears in
// hello .NET API (CloudPool.Statistics)
detailLevel.ExpandClause = "stats";

// Now get our collection of pools, minimizing hello amount of data that is returned
// by specifying hello detail level that we configured above
List<CloudPool> testPools =
    await myBatchClient.PoolOperations.ListPools(detailLevel).ToListAsync();
```

> [!TIP]
> 인스턴스 [ODATADetailLevel] [ odata] 선택으로 구성 된 및 Expand 절 전달할 수도 있습니다 tooappropriate Get 메서드와 같이 [PoolOperations.GetPool](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.getpool.aspx) toolimit hello 양을 반환 되는 데이터입니다.
> 
> 

## <a name="batch-rest-toonet-api-mappings"></a>배치 REST too.NET API 매핑
filter, select 및 expand 문자열의 속성 이름은 이름과 대소문자 모두 해당 REST API 항목을 반영 *해야 합니다* . hello 테이블 아래에 hello.NET 및 REST API 함수와 간의 매핑을 제공합니다.

### <a name="mappings-for-filter-strings"></a>filter 문자열 매핑
* **.NET 메서드 목록**: 수락이 열의 hello.NET API 메서드는 각각 한 [ODATADetailLevel] [ odata] 개체를 매개 변수로 합니다.
* **REST 목록 요청**: 각 REST API 페이지 hello 속성 및 작업을 지정 하는 테이블을 포함 하는이 열에는 사용할 수 있는 연결 된 tooin *필터* 문자열입니다. [ODATADetailLevel.FilterClause][odata_filter] 문자열을 구성할 때 이 속성 이름과 작업을 사용합니다.

| .NET 목록 메서드 | REST 목록 요청 |
| --- | --- |
| [CertificateOperations.ListCertificates][net_list_certs] |[계정에서 hello 인증서 나열][rest_list_certs] |
| [CloudTask.ListNodeFiles][net_list_task_files] |[작업과 관련 된 hello 파일 나열][rest_list_task_files] |
| [JobOperations.ListJobPreparationAndReleaseTaskStatus][net_list_jobprep_status] |[Hello 작업 준비 및 작업에 대 한 작업 릴리스 작업의 hello 상태 나열][rest_list_jobprep_status] |
| [JobOperations.ListJobs][net_list_jobs] |[계정에서 hello 작업 나열][rest_list_jobs] |
| [JobOperations.ListNodeFiles][net_list_nodefiles] |[노드에서 hello 파일 나열][rest_list_nodefiles] |
| [JobOperations.ListTasks][net_list_tasks] |[작업에 연결 된 hello 태스크 나열][rest_list_tasks] |
| [JobScheduleOperations.ListJobSchedules][net_list_job_schedules] |[계정에 작업 일정 hello 나열][rest_list_job_schedules] |
| [JobScheduleOperations.ListJobs][net_list_schedule_jobs] |[작업 일정와 관련 된 hello 작업 나열][rest_list_schedule_jobs] |
| [PoolOperations.ListComputeNodes][net_list_compute_nodes] |[목록 hello의에서 계산 노드는 풀][rest_list_compute_nodes] |
| [PoolOperations.ListPools][net_list_pools] |[계정에서 hello 풀 나열][rest_list_pools] |

### <a name="mappings-for-select-strings"></a>select 문자열 매핑
* **Batch .NET 형식**: Batch .NET API 형식.
* **REST API 엔터티**:이 열에서 각 페이지 hello 형식에 대 한 hello REST API 속성 이름을 나열 하는 하나 이상의 테이블을 포함 합니다. 이러한 속성 이름은 *select* 문자열을 구성할 때 사용됩니다. [ODATADetailLevel.SelectClause][odata_select] 문자열을 구성할 때 이와 동일한 속성을 사용합니다.

| Batch .NET 형식 | REST API 엔터티 |
| --- | --- |
| [Certificate][net_cert] |[인증서 정보 가져오기][rest_get_cert] |
| [CloudJob][net_job] |[작업 정보 가져오기][rest_get_job] |
| [CloudJobSchedule][net_schedule] |[작업 일정 정보 가져오기][rest_get_schedule] |
| [ComputeNode][net_node] |[노드 정보 가져오기][rest_get_node] |
| [CloudPool][net_pool] |[풀 정보 가져오기][rest_get_pool] |
| [CloudTask][net_task] |[태스크 정보 가져오기][rest_get_task] |

## <a name="example-construct-a-filter-string"></a>예: filter 문자열 구성
에 대 한 필터 문자열을 생성할 때 [ODATADetailLevel.FilterClause][odata_filter], 위의 "필터 문자열에 대 한 매핑" toofind hello REST API 설명서 페이지에서 해당 하는 hello 표를 참조 하십시오. toohello 목록 작업 tooperform 한다고 합니다. 해당 페이지에서 첫 번째 다중 행 테이블 hello의에서 hello 필터링 가능한 속성 및 해당 지원 되는 연산자를 찾을 수 있습니다. Tooretrieve 인 종료 코드는 0이 아닌 모든 작업을 원하는 경우 예를 들어이 행에 [작업과 연결 된 hello 작업을 나열] [ rest_list_tasks] hello 적용 가능한 속성이 문자열 및 허용 되는 연산자를 지정 합니다.

| 속성 | 허용되는 연산 | 형식 |
|:--- |:--- |:--- |
| `executionInfo/exitCode` |`eq, ge, gt, le , lt` |`Int` |

따라서 0이 아닌 종료 코드를 있는 모든 작업을 나열 하기 위한 필터 문자열 hello 다음과 같습니다.

`(executionInfo/exitCode lt 0) or (executionInfo/exitCode gt 0)`

## <a name="example-construct-a-select-string"></a>예: select 문자열 구성
tooconstruct [ODATADetailLevel.SelectClause][odata_select], "선택 문자열에 대 한 매핑" 아래에 위의 hello 표를 참조 하십시오. 및 toohello REST API 페이지 엔터티의 toohello 형식을 해당 하는 이동 했는지 나열 됩니다. 해당 페이지에서 첫 번째 다중 행 테이블 hello의에서 hello 선택할 수 있는 속성 및 해당 지원 되는 연산자를 찾을 수 있습니다. 목록에 tooretrieve만 hello ID 및 각 작업에 대 한 명령줄을 원할 경우 예를 들어 있습니다 이러한 행 hello 적용 가능한 표에 [작업에 대 한 정보를 가져올][rest_get_task]:

| 속성 | 형식 | 참고 사항 |
|:--- |:--- |:--- |
| `id` |`String` |`hello ID of hello task.` |
| `commandLine` |`String` |`hello command line of hello task.` |

hello select 문자열 hello ID 및 각 나열 된 작업을 사용 하 여 명령줄만을 포함 하는 데 다음 합니다.

`id, commandLine`

## <a name="code-samples"></a>코드 샘플
### <a name="efficient-list-queries-code-sample"></a>효율적인 목록 쿼리 코드 샘플
체크 아웃 hello [EfficientListQueries] [ efficient_query_sample] GitHub toosee 효율성에 대 한 샘플 프로젝트 목록을 쿼리 하는 응용 프로그램에서 성능에 영향을 줄 수 있습니다. 이 C# 콘솔 응용 프로그램 만들고 많은 수의 작업 tooa 작업을 추가 합니다. 그런 다음 여러 호출 toohello을 사용 하면 [JobOperations.ListTasks] [ net_list_tasks] 메서드와 전달 [ODATADetailLevel] [ odata] 개체 반환 된 데이터 toobe의 다른 속성 값 toovary hello 양을 구성 합니다. 유사한 toohello 다음을 출력을 생성합니다.

```
Adding 5000 tasks toojob jobEffQuery...
5000 tasks added in 00:00:47.3467587, hit ENTER tooquery tasks...

4943 tasks retrieved in 00:00:04.3408081 (ExpandClause:  | FilterClause: state eq 'active' | SelectClause: id,state)
0 tasks retrieved in 00:00:00.2662920 (ExpandClause:  | FilterClause: state eq 'running' | SelectClause: id,state)
59 tasks retrieved in 00:00:00.3337760 (ExpandClause:  | FilterClause: state eq 'completed' | SelectClause: id,state)
5000 tasks retrieved in 00:00:04.1429881 (ExpandClause:  | FilterClause:  | SelectClause: id,state)
5000 tasks retrieved in 00:00:15.1016127 (ExpandClause:  | FilterClause:  | SelectClause: id,state,environmentSettings)
5000 tasks retrieved in 00:00:17.0548145 (ExpandClause: stats | FilterClause:  | SelectClause: )

Sample complete, hit ENTER toocontinue...
```

Hello 경과 시간이 표시 된 것과 같이 hello 속성 및 반환 되는 항목의 hello 수를 제한 하 여 쿼리 응답 시간을 크게 낮출 수 있습니다. Hello에이 및 다른 샘플 프로젝트를 찾을 수 있습니다 [azure 일괄 처리-샘플] [ github_samples] GitHub의 리포지토리 합니다.

### <a name="batchmetrics-library-and-code-sample"></a>BatchMetrics 라이브러리 및 코드 샘플
또한 toohello EfficientListQueries 위의 코드 샘플을 찾을 수 있습니다 hello [BatchMetrics] [ batch_metrics] hello에서 프로젝트 [azure 일괄 처리-샘플] [ github_samples] GitHub 리포지토리 합니다. hello BatchMetrics 샘플 프로젝트 tooefficiently hello 일괄 처리 API를 사용 하 여 Azure 배치 작업 진행률을 모니터링 하는 방법을 보여 줍니다.

hello [BatchMetrics] [ batch_metrics] 샘플 사용자의 프로젝트 및 간단한 명령줄에 통합할 수 있는.NET 클래스 라이브러리 프로젝트에 포함 되어 tooexercise 프로그래밍 하 고 hello hello 사용을 보여 주기 라이브러리입니다.

hello 프로젝트 내에서 hello 샘플 응용 프로그램 작업을 수행 하는 hello를 보여 줍니다.

1. 필요한 순서 toodownload 유일한 hello 속성에서 특정 특성을 선택 합니다.
2. Hello 마지막 쿼리 이후에 변경 상태 전환 시간 순서 toodownload에 대 한 필터링

예를 들어 hello 메서드 뒤 hello BatchMetrics 라이브러리에에서 나타납니다. 해당 유일한 hello를 지정 하는 ODATADetailLevel 반환 `id` 및 `state` 쿼리는 hello 엔터티에 대 한 속성을 가져올 해야 합니다. 또한 지정 하는 상태가 지정 된 hello 이후 변경 된 엔터티만 `DateTime` 매개 변수를 반환 합니다.

```csharp
internal static ODATADetailLevel OnlyChangedAfter(DateTime time)
{
    return new ODATADetailLevel(
        selectClause: "id, state",
        filterClause: string.Format("stateTransitionTime gt DateTime'{0:o}'", time)
    );
}
```

## <a name="next-steps"></a>다음 단계
### <a name="parallel-node-tasks"></a>병렬 노드 작업
[동시 노드 작업과 Azure 배치 계산 리소스 사용량을 최대화](batch-parallel-node-tasks.md) 는 또 다른 관련 tooBatch 응용 프로그램 성능입니다. 일부 유형의 작업은 더 크지만 더 적은 계산 노드에서의 병렬 작업 실행에서 이점을 얻을 수 있습니다. 체크 아웃 hello [예제 시나리오](batch-parallel-node-tasks.md#example-scenario) 이러한 시나리오에 대 한 자세한 내용은 hello 문서.

### <a name="batch-forum"></a>배치 포럼
hello [Azure 배치 포럼] [ forum] 는 좋은 toodiscuss 일괄 처리를 놓고 hello 서비스에 대 한 질문은 msdn 합니다. 유용한 "고정" 게시물을 참조하고 Batch 솔루션을 빌드하는 동안 질문이 생기면 즉시 게시합니다.

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_net_listjobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobs.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[batch_metrics]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchMetrics
[efficient_query_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/EfficientListQueries
[forum]: https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=azurebatch
[github_samples]: https://github.com/Azure/azure-batch-samples
[odata]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.aspx
[odata_ctor]: https://msdn.microsoft.com/library/azure/dn866178.aspx
[odata_expand]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.expandclause.aspx
[odata_filter]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.filterclause.aspx
[odata_select]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.selectclause.aspx

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

[rest_list_certs]: https://msdn.microsoft.com/library/azure/dn820154.aspx
[rest_list_compute_nodes]: https://msdn.microsoft.com/library/azure/dn820159.aspx
[rest_list_job_schedules]: https://msdn.microsoft.com/library/azure/mt282174.aspx
[rest_list_jobprep_status]: https://msdn.microsoft.com/library/azure/mt282170.aspx
[rest_list_jobs]: https://msdn.microsoft.com/library/azure/dn820117.aspx
[rest_list_nodefiles]: https://msdn.microsoft.com/library/azure/dn820151.aspx
[rest_list_pools]: https://msdn.microsoft.com/library/azure/dn820101.aspx
[rest_list_schedule_jobs]: https://msdn.microsoft.com/library/azure/mt282169.aspx
[rest_list_task_files]: https://msdn.microsoft.com/library/azure/dn820142.aspx
[rest_list_tasks]: https://msdn.microsoft.com/library/azure/dn820187.aspx

[rest_get_cert]: https://msdn.microsoft.com/library/azure/dn820176.aspx
[rest_get_job]: https://msdn.microsoft.com/library/azure/dn820106.aspx
[rest_get_node]: https://msdn.microsoft.com/library/azure/dn820168.aspx
[rest_get_pool]: https://msdn.microsoft.com/library/azure/dn820165.aspx
[rest_get_schedule]: https://msdn.microsoft.com/library/azure/mt282171.aspx
[rest_get_task]: https://msdn.microsoft.com/library/azure/dn820133.aspx

[net_cert]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.certificate.aspx
[net_job]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_node]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.aspx
[net_pool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_schedule]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjobschedule.aspx
[net_task]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx

[rest_get_task_counts]: https://docs.microsoft.com/rest/api/batchservice/get-the-task-counts-for-a-job
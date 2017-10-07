---
title: "aaaCreate/일정 파이프라인, Data Factory에 체인 활동 | Microsoft Docs"
description: "데이터 파이프라인에서 Azure Data Factory toomove toocreate 알아보고 데이터를 변환 합니다. 데이터 기반 워크플로 tooproduce 준비 toouse 정보를 만듭니다."
keywords: "데이터 파이프라인, 데이터 기반 워크플로"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 13b137c7-1033-406f-aea7-b66f25b313c0
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/12/2017
ms.author: shlo
ms.openlocfilehash: 4a0fc20f98ce6453c16955e97fddb891926c173a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="pipelines-and-activities-in-azure-data-factory"></a>Azure 데이터 팩터리의 파이프라인 및 활동
이 문서에서는 파이프라인 및 Azure Data Factory에는 활동을 이해 하 고 데이터 이동 및 데이터 처리 시나리오에 대 한 tooconstruct 종단 간 데이터 기반 워크플로 사용할 수 있습니다.  

> [!NOTE]
> 이 문서에서는 통해 수행한 가정 [소개 tooAzure Data Factory](data-factory-introduction.md)합니다. 데이터 팩터리를 만드는 실습 경험이 없는 경우 [데이터 변환 자습서](data-factory-build-your-first-pipeline.md) 및/또는 [데이터 이동 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)를 진행하면 이 문서를 이해하는 데 도움이 됩니다.  

## <a name="overview"></a>개요
데이터 팩터리에는 하나 이상의 파이프라인이 포함될 수 있습니다. 파이프라인은 함께 작업을 수행하는 활동의 논리적 그룹화입니다. 파이프라인의 hello 활동 데이터에 대해 작업 tooperform를 정의합니다. 예를 들어 온-프레미스 SQL Server tooan Azure Blob 저장소에서에서 복사 작업 toocopy 데이터를 사용할 수 있습니다. 그런 다음 hello blob 저장소 tooproduce 출력 데이터에서 Azure HDInsight 클러스터 tooprocess/변환 데이터에서 하이브 스크립트를 실행 하는 하이브 활동을 사용 합니다. 마지막으로, 두 번째 복사본 활동 toocopy hello 출력 데이터 tooan Azure SQL 데이터 웨어하우스는 비즈니스 인텔리전스 (BI)를 기반으로 작성 된 보고 솔루션을 사용 합니다. 

활동은 0개 이상의 입력 [데이터 집합](data-factory-create-datasets.md)을 받고 하나 이상의 출력 [데이터 집합](data-factory-create-datasets.md)을 생성할 수 있습니다. hello 다음 보여 주는 다이어그램 파이프라인, 작업 및 데이터 집합 간의 hello 관계 Data Factory에: 

![파이프라인, 활동, 데이터 집합 간 관계](media/data-factory-create-pipelines/relationship-pipeline-activity-dataset.png)

파이프라인이 있습니다 toomanage 활동을 각 하는 대신 집합으로 개별적으로. 예를 들어, 배포 하 고 예약 하 고 일시 중단, 수 있으며 독립적으로 hello 파이프라인에서 작업 하지 처리 하는 대신 파이프라인 다시 시작 수 있습니다.

Data Factory는 데이터 이동 활동 및 데이터 변환 활동이라는 두 종류의 활동을 지원합니다. 각 활동은 0개 이상의 입력 [데이터 집합](data-factory-create-datasets.md)을 갖고 하나 이상의 출력 데이터 집합을 생성할 수 있습니다.

입력된 데이터 집합 hello 파이프라인의 활동에 대 한 hello 입력을 나타내고 출력 데이터 집합 hello 활동에 대 한 hello 출력을 나타냅니다. 데이터 집합은 테이블, 파일, 폴더, 문서를 비롯한 다양한 데이터 저장소 내의 데이터를 식별합니다. 데이터 집합을 만든 후 파이프라인의 작업에 사용할 수 있습니다. 예를 들어 데이터 집합은 복사 작업 또는 HDInsightHive 작업의 입력/출력 데이터 집합일 수 있습니다. 데이터 집합에 대한 자세한 내용은 [Azure Data Factory의 데이터 집합](data-factory-create-datasets.md) 문서를 참조하세요.

### <a name="data-movement-activities"></a>데이터 이동 활동
복사 활동 Data Factory에는 원본 데이터 저장소 tooa 싱크 데이터 저장소에서 데이터를 복사합니다. 데이터 팩터리 hello 다음 데이터 저장소를 지원 합니다. 데이터 소스에서 tooany 싱크를 작성할 수 있습니다. 데이터 저장소 toolearn 방법을 클릭 해당 저장소에서 데이터 tooand toocopy 합니다.

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> 데이터 저장소와 * 온-프레미스 될 수 있습니다 또는 Azure IaaS에서 고 tooinstall 있어야 하며 [데이터 관리 게이트웨이](data-factory-data-management-gateway.md) 에-프레미스/Azure IaaS 컴퓨터에 있습니다.

자세한 내용은 [데이터 이동 활동](data-factory-data-movement-activities.md) 문서를 참조하세요.

### <a name="data-transformation-activities"></a>데이터 변환 활동
[!INCLUDE [data-factory-transformation-activities](../../includes/data-factory-transformation-activities.md)]

자세한 내용은 [데이터 변환 활동](data-factory-data-transformation-activities.md) 문서를 참조하세요.

### <a name="custom-net-activities"></a>사용자 지정 .NET 활동 
데이터에서 복사 작업 hello 저장소 하지 않는 지원, 또는 변환 하는 고유한 논리를 사용 하 여 데이터 만들기/toomove 데이터를 유지 해야 하는 경우는 **사용자 지정.NET 작업**합니다. 사용자 지정 활동을 만들고 사용하는 방법에 대한 자세한 내용은 [Azure Data Factory 파이프라인에서 사용자 지정 활동 사용](data-factory-use-custom-activities.md)을 참조하세요.

## <a name="schedule-pipelines"></a>파이프라인 예약
파이프라인은 **시작** 시간과 **종료** 시간 사이에서만 활성화됩니다. Hello 시작 시간 이전 또는 hello 종료 시간 이후에 실행 되지 않습니다. Hello 파이프라인의 일시 중지 되 면이 실행 되지 않도록 해당 시작 및 종료 시간에 관계 없이 합니다. 파이프라인 toorun에 대 한 것 해야 일시 중지할 수 있습니다. 참조 [일정 예약 및 실행](data-factory-scheduling-and-execution.md) toounderstand Azure Data Factory에서 예약 및 실행의 작동 방식입니다.

## <a name="pipeline-json"></a>파이프라인 JSON
JSON 형식으로 파이프라인을 정의하는 방법에 대해 자세히 살펴보겠습니다. 파이프라인에 대 한 일반 구조 hello 모양은 다음과 같습니다.

```json
{
    "name": "PipelineName",
    "properties": 
    {
        "description" : "pipeline description",
        "activities":
        [

        ],
        "start": "<start date-time>",
        "end": "<end date-time>",
        "isPaused": true/false,
        "pipelineMode": "scheduled/onetime",
        "expirationTime": "15.00:00:00",
        "datasets": 
        [
        ]
    }
}
```

| 태그 | 설명 | 필수 |
| --- | --- | --- |
| name |Hello 파이프라인의 이름입니다. 수행 하는 파이프라인 hello hello 동작을 나타내는 이름을 지정 합니다. <br/><ul><li>최대 문자 수: 260</li><li>문자, 숫자 또는 밑줄(_)로 시작해야 합니다.</li><li>다음 문자는 사용할 수 없습니다. “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</li></ul> |예 |
| 설명 | 에 대 한 어떤 hello 파이프라인을 사용 하는 설명 하는 hello 텍스트를 지정 합니다. |예 |
| 작업 | hello **활동** 섹션 내에 정의 된 하나 이상의 활동을 가질 수 있습니다. Hello hello 활동 JSON 요소에 대 한 자세한 내용은 다음 섹션을 참조 하십시오. | 예 |  
| start | 시작 날짜 / 시간 hello 파이프라인에 대 한 합니다. [ISO 형식](http://en.wikipedia.org/wiki/ISO_8601)에 있어야 합니다. 예: `2016-10-14T16:32:41Z` <br/><br/>이제는 현지 시간을 가능한 toospecify 예는 EST입니다. 예제: `2016-02-27T06:00:00-05:00`”(오전 6시 동부 표준시)<br/><br/>hello 시작 및 끝 속성 함께 지정 hello 파이프라인에 대 한 활성 기간입니다. 출력 조각은 이 활성 기간에만 생성됩니다. |아니요<br/><br/>Hello end 속성에 대 한 값을 지정 하는 경우 hello 시작 속성에 대 한 값을 지정 해야 합니다.<br/><br/>hello 시작 및 종료 시간 둘 다 수 빈 toocreate 파이프라인. 값을 모두 지정 해야 합니다는 파이프라인 toorun hello에 대 한 활성 기간 tooset 합니다. 시작 및 종료 시간을 지정 하지 않을 경우 파이프라인을 만들 때 설정할 수 있습니다 hello 집합 AzureRmDataFactoryPipelineActivePeriod cmdlet를 사용 하 여 나중에 있습니다. |
| end | Hello 파이프라인에 대 한 날짜 및 시간을 종료 합니다. 지정된 경우 ISO 형식에 있어야 합니다. 예: `2016-10-14T17:32:41Z` <br/><br/>이제는 현지 시간을 가능한 toospecify 예는 EST입니다. 예: `2016-02-27T06:00:00-05:00`(오전 6시 동부 표준시)<br/><br/>toorun hello 파이프라인 hello hello 최종 속성 값으로 9999-09-09를 무제한으로 지정 합니다. <br/><br/> 파이프라인은 시작 시간과 종료 시간 사이에서만 활성화됩니다. Hello 시작 시간 이전 또는 hello 종료 시간 이후에 실행 되지 않습니다. Hello 파이프라인의 일시 중지 되 면이 실행 되지 않도록 해당 시작 및 종료 시간에 관계 없이 합니다. 파이프라인 toorun에 대 한 것 해야 일시 중지할 수 있습니다. 참조 [일정 예약 및 실행](data-factory-scheduling-and-execution.md) toounderstand Azure Data Factory에서 예약 및 실행의 작동 방식입니다. |아니요 <br/><br/>Hello 시작 속성에 대 한 값을 지정 하는 경우 hello end 속성에 대 한 값을 지정 해야 합니다.<br/><br/>Hello에 대 한 메모를 참조 하세요 **시작** 속성입니다. |
| isPaused | 집합 tootrue, hello 파이프라인 실행 되지 않으면 합니다. 에 hello에 일시 중지 된 상태입니다. 기본값 = false입니다. 이 속성 tooenable를 사용 하거나 파이프라인을 사용 하지 않도록 설정할 수 있습니다. |아니요 |
| pipelineMode | hello 메서드 hello 파이프라인에 대 한 실행을 예약 합니다. 허용되는 값은 scheduled(기본), onetime입니다.<br/><br/>'예약' hello 파이프라인 tooits 활성 기간 (시작 및 종료 시간)에 따라 지정 된 시간 간격으로 실행을 나타냅니다. 'Onetime' hello 파이프라인 실행 한 번만 지정 합니다. 현재는, Onetime 파이프라인이 생성된 후에 수정/업데이트가 불가능합니다. 일회성 설정에 대한 세부 정보는 [일회성 파이프라인](#onetime-pipeline)을 참조하세요. |아니요 |
| expirationTime | 어떤 hello에 대 한 시간을 만든 후 [일회성 파이프라인](#onetime-pipeline) 유효 하 고 프로 비전 된 상태로 유지 해야 합니다. 경우 없는 모든 활성 실패, 또는 실행을 보류 중인 hello 파이프라인은 자동으로 삭제 한 번에 도달 hello 만료 시간입니다. 기본값 hello:`"expirationTime": "3.00:00:00"`|아니요 |
| 데이터 집합 |Hello 파이프라인에 정의 된 활동에서 사용 하는 데이터 집합 toobe의 목록입니다. 이 속성을 특정 toothis 파이프라인 이며 hello 데이터 팩터리 내에 정의 된 있는 toodefine 사용 되는 데이터 집합 수입니다. 이 파이프라인 내에 정의된 데이터 집합은 이 파이프라인에서만 사용될 수 있고 공유될 수 없습니다. 자세한 내용은 [범위가 지정된 데이터 집합](data-factory-create-datasets.md#scoped-datasets)을 참조하세요. |아니요 |

## <a name="activity-json"></a>활동 JSON
hello **활동** 섹션 내에 정의 된 하나 이상의 활동을 가질 수 있습니다. 각 활동에는 다음 최상위 구조 hello에 있습니다.

```json
{
    "name": "ActivityName",
    "description": "description", 
    "type": "<ActivityType>",
    "inputs":  "[]",
    "outputs":  "[]",
    "linkedServiceName": "MyLinkedService",
    "typeProperties":
    {

    },
    "policy":
    {
    },
    "scheduler":
    {
    }
}
```

다음 표에서 hello 활동 JSON 정의에서 속성을 설명 합니다.

| 태그 | 설명 | 필수 |
| --- | --- | --- |
| name | Hello 활동의 이름입니다. Hello 활동을 수행 하는 hello 동작을 나타내는 이름을 지정 합니다. <br/><ul><li>최대 문자 수: 260</li><li>문자, 숫자 또는 밑줄(_)로 시작해야 합니다.</li><li>다음 문자는 사용할 수 없습니다. “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</li></ul> |예 |
| 설명 | 설명 하는 어떤 hello 활동에 사용 되는 텍스트 |예 |
| type | Hello 활동의 형식입니다. Hello 참조 [데이터 이동 작업](#data-movement-activities) 및 [데이터 변환 작업](#data-transformation-activities) 다양 한 유형의 활동에 대 한 섹션. |예 |
| inputs |Hello 활동에서 사용 하는 입력된 테이블<br/><br/>`// one input table`<br/>`"inputs":  [ { "name": "inputtable1"  } ],`<br/><br/>`// two input tables` <br/>`"inputs":  [ { "name": "inputtable1"  }, { "name": "inputtable2"  } ],` |예 |
| outputs |Hello 활동에 의해 사용 되는 출력된 테이블입니다.<br/><br/>`// one output table`<br/>`"outputs":  [ { "name": "outputtable1" } ],`<br/><br/>`//two output tables`<br/>`"outputs":  [ { "name": "outputtable1" }, { "name": "outputtable2" }  ],` |예 |
| linkedServiceName |Hello 활동에서 사용 하는 hello 연결 된 서비스의 이름입니다. <br/><br/>활동은 toohello 필요한 계산 환경에 연결 하는 hello 연결 된 서비스를 지정 해야 합니다. |HDInsight 작업 및 Azure 기계 학습 배치 평가 작업의 경우 예  <br/><br/>다른 모든 사용자의 경우 아니요 |
| typeProperties |Hello에 대 한 속성 **typeProperties** 섹션 hello 활동의 형식에 따라 달라 집니다. 활동에 대해 toosee 형식 속성 hello 이전 단원의 toohello 작업 링크를 클릭 합니다. | 아니요 |
| policy |Hello 활동의 hello 런타임 동작에 영향을 주는 정책입니다. 지정하지 않으면 기본 정책이 사용됩니다. |아니요 |
| scheduler | "스케줄러" 속성은 사용 되는 toodefine을 원하는 hello 활동에 대 한 일정입니다. 해당 속성의 하위 hello hello에서와 동일 hello는 [데이터 집합의 가용성 속성](data-factory-create-datasets.md#dataset-availability)합니다. |아니요 |


### <a name="policies"></a>정책
정책은은 hello 테이블 조각이 처리 시에 특히는 활동의 런타임 동작을 hello는 영향을 줍니다. 다음 표에서 hello hello 세부 정보를 제공 합니다.

| 속성 | 허용된 값 | 기본값 | 설명 |
| --- | --- | --- | --- |
| 동시성 |정수  <br/><br/>최대값: 10 |1 |Hello 활동의 동시 실행 수입니다.<br/><br/>Hello 여러 조각에서 발생할 수 있는 병렬 활동 실행 횟수를 결정 합니다. 예를 들어 활동을 통해 toogo 해야 하는 경우 다양 한 사용 가능한 데이터에 더 큰 동시성 가치가 속도가 향상 hello 데이터 처리 됩니다. |
| executionPriorityOrder |NewestFirst<br/><br/>OldestFirst |OldestFirst |Hello 데이터 조각이 처리 중인의 순서를 결정 합니다.<br/><br/>예를 들어 2개의 조각이 있으며(각각 오후 4시 및 오후 5시에 발생) 둘 다 실행 보류 상태입니다. Hello executionPriorityOrder toobe NewestFirst로 설정 하면 오후 5 시의 hello 조각이 먼저 처리 됩니다. 마찬가지로 executionPriorityORder toobe hello OldestFIrst로 설정 하면 오후 4 시의 hello 조각이 처리 됩니다. |
| retry |정수 <br/><br/>최대값이 10이 될 수 있음 |0 |Hello 조각에 대 한 hello 데이터 처리 전 까지의 재시도 횟수 Failure로 표시 됩니다. 지정 된 toohello를 데이터 조각에 대 한 활동 실행을 다시 시도 다시 시도 횟수입니다. hello 재시도 hello 실패 후 가능한 한 빨리 수행 됩니다. |
| 시간 제한 |TimeSpan |00:00:00 |Hello 활동에 대 한 제한 시간입니다. 예: 00:10:00(시간 제한 10분을 의미함)<br/><br/>값을 지정 하지 않거나 0으로 하는 경우에 hello 시간 초과 제한이 없습니다.<br/><br/>분할 영역에 데이터 처리 시간이 hello hello 제한 시간 값을 초과 하는 경우 취소 되 및 hello 시스템 tooretry hello 처리를 시도 합니다. 재시도 횟수 hello hello retry 속성에 따라 달라 집니다. 시간 제한이 발생 hello 상태 tooTimedOut 설정 됩니다. |
| delay |TimeSpan |00:00:00 |데이터 처리 hello 조각 시작 하기 전에 hello 지연 시간을 지정 합니다.<br/><br/>데이터 조각에 대 한 활동의 hello 실행 hello 지연 되는 hello 예상 실행 시간 후에 시작 됩니다.<br/><br/>예: 00:10:00(10분의 지연을 의미함) |
| longRetry |정수 <br/><br/>최대값: 10 |1 |hello 긴 다시 시도 횟수 후 hello 조각 실행이 실패 합니다.<br/><br/>longRetry 시도는 longRetryInterval에 따라 간격이 조정됩니다. 따라서 다시 시도 사이의 시간 toospecify 해야 할 경우 longRetry를 사용 합니다. Retry와 longRetry를 둘 다 지정 된 경우 다시 시도 횟수를 포함 하는 각 longRetry 시도 및 hello 최대 시도 횟수가 다시 시도 * longRetry 합니다.<br/><br/>예를 들어, hello 활동 정책의 설정에에서 따라 hello 사항이 있는 경우:<br/>Retry: 3<br/>longRetry: 2<br/>longRetryInterval: 01:00:00<br/><br/>하나의 분할 영역 tooexecute 가정 (상태 대기 중) hello 활동 실행 될 때마다가 실패 하 고 있습니다. 우선 3번 연속 실행 시도를 합니다. 각 시도 후 조각 상태 hello 재시도 것입니다. 통해 처음 3 시도 되 면 hello 조각 상태 LongRetry가 됩니다.<br/><br/>한 시간(즉, longRetryInteval의 값) 후에 3번 연속 실행이 다시 시도됩니다. 그 후 hello 조각 상태가 Failed가 고 더 이상 다시 시도 합니다. 즉, 전체적으로 6번의 시도가 일어납니다.<br/><br/>실행에 성공 hello 조각 상태는 준비와 더 이상 다시 시도 합니다.<br/><br/>longRetry 명확 하지 않은 시간에 도착 하면 종속 데이터 또는 hello 전체 환경 연결이 잘 끊어지는 어떤 데이터 처리가 수행 아래 있는 경우 사용할 수 있습니다. 이러한 경우에 한 번에 하나씩 재시도 수행 하 도움이 되지 않을 수 및 출력을 원하는 hello에 결과 시간 간격 후 이렇게 합니다.<br/><br/>주의: longRetry 또는 longRetryInterval에 높은 값을 설정하지 마세요. 일반적으로 더 높은 값을 지정하면 다른 시스템 문제가 발생합니다. |
| longRetryInterval |TimeSpan |00:00:00 |긴 시도 간의 지연을 hello |

## <a name="sample-copy-pipeline"></a>샘플 복사 파이프라인
다음 샘플 파이프라인 hello에 하나의 활동 형식의 **복사** hello에 **활동** 섹션. 이 샘플에서는 hello [복사 작업이](data-factory-data-movement-activities.md) Azure Blob 저장소 tooan Azure SQL 데이터베이스에서 데이터를 복사 합니다. 

```json
{
  "name": "CopyPipeline",
  "properties": {
    "description": "Copy data from a blob tooAzure SQL table",
    "activities": [
      {
        "name": "CopyFromBlobToSQL",
        "type": "Copy",
        "inputs": [
          {
            "name": "InputDataset"
          }
        ],
        "outputs": [
          {
            "name": "OutputDataset"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "SqlSink",
            "writeBatchSize": 10000,
            "writeBatchTimeout": "60:00:00"
          }
        },
        "Policy": {
          "concurrency": 1,
          "executionPriorityOrder": "NewestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
    ],
    "start": "2016-07-12T00:00:00Z",
    "end": "2016-07-13T00:00:00Z"
  }
} 
```

포인트 다음 참고 hello:

* Hello 활동 섹션에는 활동이 하나만 인 **형식** 너무 설정**복사**합니다.
* Hello 활동 너무 설정 되어 입력**InputDataset** 및 hello 활동 너무 설정 되어 출력**OutputDataset**합니다. JSON의 데이터 집합 정의에 대해서는 [데이터 집합](data-factory-create-datasets.md) 문서를 참조하세요. 
* Hello에 **typeProperties** 섹션 **BlobSource** hello 원본 유형으로 지정 된 및 **SqlSink** hello 싱크 유형으로 지정 합니다. Hello에 [데이터 이동 활동](#data-movement-activities) 섹션에서 데이터 원본 또는 싱크 toolearn를 해당 데이터 저장소에서 데이터를 이동 하는 방법에 대 한 자세한으로 toouse 되도록 저장소 hello를 클릭 합니다. 

이 파이프라인을 만드는 전체 연습을 참조 하십시오. [자습서: Blob 저장소 tooSQL 데이터베이스에서에서 데이터를 복사](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)합니다. 

## <a name="sample-transformation-pipeline"></a>샘플 변환 파이프라인
다음 샘플 파이프라인 hello에 하나의 활동 형식의 **HDInsightHive** hello에 **활동** 섹션. 이 샘플에서는 hello [HDInsight Hive 활동](data-factory-hive-activity.md) Azure HDInsight Hadoop 클러스터에서 하이브 스크립트 파일을 실행 하 여 Azure Blob 저장소에서 데이터를 변환 합니다. 

```json
{
    "name": "TransformPipeline",
    "properties": {
        "description": "My first Azure Data Factory pipeline",
        "activities": [
            {
                "type": "HDInsightHive",
                "typeProperties": {
                    "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                    "scriptLinkedService": "AzureStorageLinkedService",
                    "defines": {
                        "inputtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/inputdata",
                        "partitionedtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/partitioneddata"
                    }
                },
                "inputs": [
                    {
                        "name": "AzureBlobInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "policy": {
                    "concurrency": 1,
                    "retry": 3
                },
                "scheduler": {
                    "frequency": "Month",
                    "interval": 1
                },
                "name": "RunSampleHiveActivity",
                "linkedServiceName": "HDInsightOnDemandLinkedService"
            }
        ],
        "start": "2016-04-01T00:00:00Z",
        "end": "2016-04-02T00:00:00Z",
        "isPaused": false
    }
}
```

포인트 다음 참고 hello: 

* Hello 활동 섹션에는 활동이 하나만 인 **형식** 너무 설정**HDInsightHive**합니다.
* hello Hive 스크립트 파일 **partitionweblogs.hql**, hello Azure 저장소 계정에에서 저장 됩니다 (hello scriptLinkedService를 호출 하 여 지정 된 **AzureStorageLinkedService**), 및  **스크립트** hello 컨테이너에 폴더 **adfgetstarted**합니다.
* hello `defines` 섹션은 하이브 구성 값으로 toohello 하이브 스크립트에 전달 되는 사용 되는 toospecify hello 런타임 설정 (예: `${hiveconf:inputtable}`, `${hiveconf:partitionedtable}`).

hello **typeProperties** 섹션은 각 변환 활동 마다 다릅니다. 변환 작업을 위해 지원 되는 형식 속성에 대 한 toolearn 클릭 hello에 hello 변환 활동 [데이터 변환 작업](#data-transformation-activities) 테이블입니다. 

이 파이프라인을 만드는 전체 연습을 참조 하십시오. [자습서: 첫 번째 파이프라인 tooprocess 데이터 Hadoop 클러스터를 사용 하 여 빌드](data-factory-build-your-first-pipeline.md)합니다. 

## <a name="multiple-activities-in-a-pipeline"></a>파이프라인의 여러 활동
hello 이전 두 개의 샘플 파이프라인에 활동이 하나만 있어야 합니다. 그렇지만 하나의 파이프라인에 여러 개의 활동이 있을 수 있습니다.  

파이프라인의 여러 활동 있고 다른 활동의 입력이 아닌 출력을 작업의 경우 hello 활동에 대 한 입력된 데이터 조각이 준비가 되었는지 여부 hello 활동 병렬로 실행할 수 있습니다. 

연결할 수 있습니다. 두 활동의 hello hello 입력된 데이터 집합으로 한 활동의 hello 출력 데이터 집합을 포함 하면 다른 활동입니다. 두 번째 활동 hello hello 먼저 하나 성공적으로 완료 되는 경우에 실행 합니다.

![동일한 파이프라인 활동 hello에 연결](./media/data-factory-create-pipelines/chaining-one-pipeline.png)

이 샘플에서는 hello 파이프라인에는 두 개의 활동: t y 1과 Activity2 합니다. Dataset1 입력으로를 사용 하 고 출력을 생성 하는 hello Activity1 Dataset2 합니다. hello 활동은 입력으로 Dataset2 하 고 생성 출력 Dataset3 합니다. Y 1의 hello 출력 이후 Activity2 hello 입력이 됩니다 (Dataset2), Activity2 hello hello 활동이 성공적으로 완료 된 후에 실행 및 생성 hello Dataset2 조각입니다. Hello 활동 2 hello Activity1 어떤 이유로 실패 하 고 hello Dataset2 분할 영역을 생성 하지 않으므로, 해당 조각에 대 한 실행 되지 않습니다 (예: 9 AM too10 AM). 

다른 파이프라인에 있는 활동을 연결할 수도 있습니다.

![두 개의 파이프라인에서 활동 연결](./media/data-factory-create-pipelines/chaining-two-pipelines.png)

이 샘플에서 Pipeline1은 Dataset1을 입력으로 받고 Dataset2를 출력으로 생성하는 하나의 활동만 포함합니다. hello Pipeline2에를 입력 및 출력으로 Dataset3 Dataset2 받아들이는 활동이 하나만 있습니다. 

자세한 내용은 [예약 및 실행](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)을 참조하세요. 

## <a name="create-and-monitor-pipelines"></a>파이프라인 만들기 및 모니터링
다음 도구 또는 SDK 중 하나를 사용하여 파이프라인을 만들 수 있습니다. 

- 복사 마법사 
- Azure 포털
- Visual Studio
- Azure PowerShell
- Azure Resource Manager 템플릿
- REST API
- .NET API

이러한 도구 또는 Sdk 중 하나를 사용 하 여 파이프라인 만들기에 대 한 단계별 지침에 대 한 자습서를 따라 hello를 참조 하십시오.
 
- [데이터 변환 활동을 사용하여 파이프라인 빌드](data-factory-build-your-first-pipeline.md)
- [데이터 이동 활동을 사용하여 파이프라인 빌드](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)

파이프라인을 생성/배포를 관리 하 고 모니터링할 수를 사용 하 여 파이프라인 hello Azure 포털 블레이드 나 모니터와 응용 프로그램을 관리 합니다. Hello 다음 단계별 지침에 대 한 항목을 참조 하십시오. 

- [Azure Portal 블레이드를 사용하여 파이프라인 모니터링 및 관리](data-factory-monitor-manage-pipelines.md)
- [모니터 및 관리 앱을 사용하여 파이프라인 모니터링 및 관리](data-factory-monitor-manage-app.md)


## <a name="onetime-pipeline"></a>일회성 파이프라인
만들고 파이프라인 toorun를 주기적으로 예약할 수 있습니다 (예: 시간 또는 일별로) hello 내에서 시작 및 종료 hello 파이프라인 정의에서 지정 하는 시간입니다. 자세한 내용은 [활동 예약](#scheduling-and-execution) 을 참고하세요. 한 번만 실행되는 파이프라인을 만들 수도 있습니다. toodo hello 설정, **pipelineMode** hello에서 속성 정의 너무 파이프라인**onetime** hello JSON 샘플 다음에 표시 된 대로 합니다. 이 속성에 대 한 hello 기본값은 **예약**합니다.

```json
{
    "name": "CopyPipeline",
    "properties": {
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource",
                        "recursive": false
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "InputDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataset"
                    }
                ]
                "name": "CopyActivity-0"
            }
        ]
        "pipelineMode": "OneTime"
    }
}
```

참고 hello 다음.

* **시작** 및 **끝** hello 파이프라인에 대 한 시간 지정 되지 않았습니다.
* **가용성** 입력 및 출력의 데이터 집합 지정 (**주파수** 및 **간격**) Data Factory hello 값을 사용 하지 않는 경우에 합니다.  
* 다이어그램 뷰는 일회성 파이프라인을 표시하지 않습니다. 이 동작은 의도된 것입니다.
* 일회성 파이프라인은 업데이트할 수 없습니다. 일회성 파이프라인 복제, 이름을 바꾸거나, 속성을 업데이트 한 toocreate 배포할 수 있습니다 다른 합니다.


## <a name="next-steps"></a>다음 단계
- 데이터 집합에 대한 자세한 내용은 [데이터 집합 만들기](data-factory-create-datasets.md) 문서를 참조하세요. 
- 파이프라인을 예약하고 실행하는 방법에 대한 자세한 내용은 [Azure Data Factory에서 예약 및 실행](data-factory-scheduling-and-execution.md) 문서를 참조하세요. 
  


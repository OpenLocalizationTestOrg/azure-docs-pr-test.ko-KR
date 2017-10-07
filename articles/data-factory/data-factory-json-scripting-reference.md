---
title: "데이터 팩터리-aaaAzure JSON 스크립팅 참조 | Microsoft Docs"
description: "Data Factory 엔터티에 JSON 스키마를 제공합니다."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 813fd752bb0ecb1b513d022b9f302325105dac31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---json-scripting-reference"></a>Azure Data Factory - JSON 스크립팅 참조
이 문서에서는 Azure Data Factory 엔터티(파이프라인, 활동, 데이터 집합 및 연결된 서비스)를 정의하기 위한 JSON 스키마와 예제를 제공합니다.  

## <a name="pipeline"></a>파이프라인 
hello 파이프라인 정의 대 한 고급 구조는 다음과 같습니다. 

```json
{
  "name": "SamplePipeline",
  "properties": {
    "description": "Describe what pipeline does",
    "activities": [
    ],
    "start": "2016-07-12T00:00:00",
    "end": "2016-07-13T00:00:00"
  }
} 
```

다음 표에서 hello 파이프라인 JSON 정의 내에서 hello 속성을 설명 합니다.

| 속성 | 설명 | 필수
-------- | ----------- | --------
| name | Hello 파이프라인의 이름입니다. 활동 hello hello 동작을 나타내는 이름을 지정 하거나 파이프라인은 구성 된 toodo<br/><ul><li>최대 문자 수: 260</li><li>문자, 숫자 또는 밑줄(_)로 시작해야 합니다.</li><li>다음 문자는 사용할 수 없습니다. “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</li></ul> |예 |
| 설명 |어떤 hello 활동 또는 파이프라인을 설명 하는 텍스트에 사용 됩니다. | 아니요 |
| 작업 | 활동의 목록을 포함합니다. | 예 |
| start |시작 날짜 / 시간 hello 파이프라인에 대 한 합니다. [ISO 형식](http://en.wikipedia.org/wiki/ISO_8601)에 있어야 합니다. 예: 2014-10-14T16:32:41 <br/><br/>이제는 현지 시간을 가능한 toospecify 예는 EST입니다. 예: `2016-02-27T06:00:00**-05:00`(오전 6시 동부 표준시)<br/><br/>hello 시작 및 끝 속성 함께 지정 hello 파이프라인에 대 한 활성 기간입니다. 출력 조각은 이 활성 기간에만 생성됩니다. |아니요<br/><br/>Hello end 속성에 대 한 값을 지정 하는 경우 hello 시작 속성에 대 한 값을 지정 해야 합니다.<br/><br/>hello 시작 및 종료 시간 둘 다 수 빈 toocreate 파이프라인. 값을 모두 지정 해야 합니다는 파이프라인 toorun hello에 대 한 활성 기간 tooset 합니다. 시작 및 종료 시간을 지정 하지 않을 경우 파이프라인을 만들 때 설정할 수 있습니다 hello 집합 AzureRmDataFactoryPipelineActivePeriod cmdlet를 사용 하 여 나중에 있습니다. |
| end |Hello 파이프라인에 대 한 날짜 및 시간을 종료 합니다. 지정된 경우 ISO 형식에 있어야 합니다. 예: 2014-10-14T17:32:41 <br/><br/>이제는 현지 시간을 가능한 toospecify 예는 EST입니다. 예: `2016-02-27T06:00:00**-05:00`(오전 6시 동부 표준시)<br/><br/>toorun hello 파이프라인 hello hello 최종 속성 값으로 9999-09-09를 무제한으로 지정 합니다. |아니요 <br/><br/>Hello 시작 속성에 대 한 값을 지정 하는 경우 hello end 속성에 대 한 값을 지정 해야 합니다.<br/><br/>Hello에 대 한 메모를 참조 하세요 **시작** 속성입니다. |
| isPaused |집합 tootrue hello 파이프라인 실행 되지 않으면 합니다. 기본값 = false입니다. 속성 tooenable이를 사용 하거나 사용 하지 않도록 설정할 수 있습니다. |아니요 |
| pipelineMode |hello 메서드 hello 파이프라인에 대 한 실행을 예약 합니다. 허용되는 값은 scheduled(기본), onetime입니다.<br/><br/>'예약' hello 파이프라인 tooits 활성 기간 (시작 및 종료 시간)에 따라 지정 된 시간 간격으로 실행을 나타냅니다. 'Onetime' hello 파이프라인 실행 한 번만 지정 합니다. 현재는, Onetime 파이프라인이 생성된 후에 수정/업데이트가 불가능합니다. 일회성 설정에 대한 세부 정보는 [일회성 파이프라인](data-factory-create-pipelines.md#onetime-pipeline)을 참조하세요. |아니요 |
| expirationTime |hello에 대 한 파이프라인 올바른지와 프로 비전 된 유지할지를 만든 후 기간. 없는 모든 활성 실패 하거나 삭제 한 경우 실행 보류 중인 hello 파이프라인은 한 번 자동으로 hello 만료 시간에 도달 합니다. |아니요 |


## <a name="activity"></a>작업 
hello 파이프라인 정의 (활동 요소) 내에서 활동에 대 한 고급 구조는 다음과 같습니다.

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
    }
    "scheduler":
    {
    }
}
```

다음 테이블 hello 활동 JSON 정의 내에서 hello 속성을 설명 합니다.

| 태그 | 설명 | 필수 |
| --- | --- | --- |
| name |Hello 활동의 이름입니다. Hello 동작 hello 활동을 나타내는 이름을 toodo 구성 지정<br/><ul><li>최대 문자 수: 260</li><li>문자, 숫자 또는 밑줄(_)로 시작해야 합니다.</li><li>다음 문자는 사용할 수 없습니다. “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</li></ul> |예 |
| 설명 |어떤 hello 활동을 설명 하는 텍스트에 사용 됩니다. |예 |
| type |Hello hello 활동 유형을 지정합니다. Hello 참조 [데이터 저장소](#data-stores) 및 [데이터 변환 작업](#data-transformation-activities) 다양 한 유형의 활동에 대 한 섹션. |예 |
| inputs |Hello 활동에서 사용 하는 입력된 테이블<br/><br/>`// one input table`<br/>`"inputs":  [ { "name": "inputtable1"  } ],`<br/><br/>`// two input tables` <br/>`"inputs":  [ { "name": "inputtable1"  }, { "name": "inputtable2"  } ],` |예 |
| outputs |Hello 활동에 의해 사용 되는 출력된 테이블입니다.<br/><br/>`// one output table`<br/>`"outputs":  [ { "name": “outputtable1” } ],`<br/><br/>`//two output tables`<br/>`"outputs":  [ { "name": “outputtable1” }, { "name": “outputtable2” }  ],` |예 |
| linkedServiceName |Hello 활동에서 사용 하는 hello 연결 된 서비스의 이름입니다. <br/><br/>활동은 toohello 필요한 계산 환경에 연결 하는 hello 연결 된 서비스를 지정 해야 합니다. |HDInsight 활동, Azure Machine Learning 활동 및 저장 프로시저 활동의 경우 예 <br/><br/>다른 모든 사용자의 경우 아니요 |
| typeProperties |Hello typeProperties 섹션의 속성 hello 활동의 형식에 따라 달라 집니다. |아니요 |
| policy |Hello 활동의 hello 런타임 동작에 영향을 주는 정책입니다. 지정하지 않으면 기본 정책이 사용됩니다. |아니요 |
| scheduler |"스케줄러" 속성은 사용 되는 toodefine을 원하는 hello 활동에 대 한 일정입니다. 해당 속성의 하위 hello hello에서와 동일 hello는 [데이터 집합의 가용성 속성](data-factory-create-datasets.md#dataset-availability)합니다. |아니요 |

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

### <a name="typeproperties-section"></a>typeProperties 섹션
hello typeProperties 섹션은 각 활동 마다 다릅니다. 변환 작업에는 방금 hello 형식 속성이 있습니다. 파이프라인에서 변환 활동을 정의하는 JSON 샘플은 이 문서의 [데이터 변환 활동](#data-transformation-activities) 섹션을 참조하세요. 

**복사 작업이** hello typeProperties 섹션에는 하위 섹션 두 개가: **소스** 및 **싱크**합니다. 참조 [데이터 저장소](#data-stores) JSON toouse 데이터 소스 및/또는 싱크로 저장 하는 방법을 보여 주는 샘플에 대 한이 문서의 섹션. 

### <a name="sample-copy-pipeline"></a>샘플 복사 파이프라인
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
    "start": "2016-07-12T00:00:00",
    "end": "2016-07-13T00:00:00"
  }
} 
```

포인트 다음 참고 hello:

* Hello 활동 섹션에는 활동이 하나만 인 **형식** 너무 설정**복사**합니다.
* Hello 활동 너무 설정 되어 입력**InputDataset** 및 hello 활동 너무 설정 되어 출력**OutputDataset**합니다.
* Hello에 **typeProperties** 섹션 **BlobSource** hello 원본 유형으로 지정 된 및 **SqlSink** hello 싱크 유형으로 지정 합니다.

참조 [데이터 저장소](#data-stores) JSON toouse 데이터 소스 및/또는 싱크로 저장 하는 방법을 보여 주는 샘플에 대 한이 문서의 섹션.    

이 파이프라인을 만드는 전체 연습을 참조 하십시오. [자습서: Blob 저장소 tooSQL 데이터베이스에서에서 데이터를 복사](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)합니다. 

### <a name="sample-transformation-pipeline"></a>샘플 변환 파이프라인
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
        "start": "2016-04-01T00:00:00",
        "end": "2016-04-02T00:00:00",
        "isPaused": false
    }
}
```

포인트 다음 참고 hello: 

* Hello 활동 섹션에는 활동이 하나만 인 **형식** 너무 설정**HDInsightHive**합니다.
* hello Hive 스크립트 파일 **partitionweblogs.hql**, hello Azure 저장소 계정에에서 저장 됩니다 (hello scriptLinkedService를 호출 하 여 지정 된 **AzureStorageLinkedService**), 및  **스크립트** hello 컨테이너에 폴더 **adfgetstarted**합니다.
* hello **정의** 섹션은 하이브 구성 값으로 toohello 하이브 스크립트에 전달 되는 사용 되는 toospecify hello 런타임 설정 (예: `${hiveconf:inputtable}`, `${hiveconf:partitionedtable}`).

파이프라인에서 변환 활동을 정의하는 JSON 샘플은 이 문서의 [데이터 변환 활동](#data-transformation-activities) 섹션을 참조하세요.

이 파이프라인을 만드는 전체 연습을 참조 하십시오. [자습서: 첫 번째 파이프라인 tooprocess 데이터 Hadoop 클러스터를 사용 하 여 빌드](data-factory-build-your-first-pipeline.md)합니다. 

## <a name="linked-service"></a>연결된 서비스
연결 된 서비스 정의 대 한 hello 고급 구조는 다음과 같습니다.

```json
{
    "name": "<name of hello linked service>",
    "properties": {
        "type": "<type of hello linked service>",
        "typeProperties": {
        }
    }
}
```

다음 테이블 hello 활동 JSON 정의 내에서 hello 속성을 설명 합니다.

| 속성 | 설명 | 필수 |
| -------- | ----------- | -------- | 
| name | Hello 연결 된 서비스의 이름입니다. | 예 | 
| properties - type | Hello 연결 된 서비스 유형입니다. 예: Azure Storage, Azure SQL Database |
| typeProperties | hello typeProperties 섹션에는 각 데이터 저장소에 대 한 서로 하거나 환경을 계산 하는 요소에 있습니다. 참조 [데이터 저장소](#datastores) 모든 hello 데이터 저장소 연결 된 서비스에 대 한 섹션 및 [환경 계산](#compute-environments) 모든 hello에 대 한 계산 연결 된 서비스 |   

## <a name="dataset"></a>데이터 집합 
Azure Data Factory의 데이터 집합은 다음과 같이 정의됩니다.

```json
{
    "name": "<name of dataset>",
    "properties": {
        "type": "<type of dataset: AzureBlob, AzureSql etc...>",
        "external": <boolean flag tooindicate external data. only for input datasets>,
        "linkedServiceName": "<Name of hello linked service that refers tooa data store.>",
        "structure": [
            {
                "name": "<Name of hello column>",
                "type": "<Name of hello type>"
            }
        ],
        "typeProperties": {
            "<type specific property>": "<value>",
            "<type specific property 2>": "<value 2>",
        },
        "availability": {
            "frequency": "<Specifies hello time unit for data slice production. Supported frequency: Minute, Hour, Day, Week, Month>",
            "interval": "<Specifies hello interval within hello defined frequency. For example, frequency set too'Hour' and interval set too1 indicates that new data slices should be produced hourly>"
        },
       "policy":
        {      
        }
    }
}
```

다음 표에 hello JSON 위에 hello에 대 한 속성을 설명 합니다.   

| 속성 | 설명 | 필수 | 기본값 |
| --- | --- | --- | --- |
| name | Hello 데이터 집합의 이름입니다. 명명 규칙은 [Azure Data Factory - 명명 규칙](data-factory-naming-rules.md) 을 참조하세요. |예 |해당 없음 |
| type | hello 데이터 집합의 형식입니다. Azure Data Factory에서 지 원하는 hello 형식 중 하나를 지정 (예: AzureBlob, AzureSqlTable). 참조 [데이터 저장소](#data-stores) 데이터 저장소 및 데이터 집합 형식 Data Factory에서 지 원하는 모든 hello에 대 한 섹션. | 
| structure | Hello 데이터 집합의 스키마입니다. 열, 해당 형식 등을 포함합니다. | 아니요 |해당 없음 |
| typeProperties | Toohello에 해당 하는 속성 유형을 선택 합니다. 지원되는 형식 및 해당 속성은 [데이터 저장소](#data-stores) 섹션을 참조하세요. |예 |해당 없음 |
| external | 부울 여부 데이터 팩터리 파이프라인에서 명시적으로 데이터 집합은 생성 여부 toospecify를 플래그입니다. |아니요 |false |
| availability | 창 또는 데이터 집합 프로덕션 hello에 대 한 모델을 조각화 하는 hello를 처리 하는 hello를 정의 합니다. 모델을 조각화 하는 hello 데이터 집합에 대 한 세부 정보를 참조 하십시오. [일정 예약 및 실행](data-factory-scheduling-and-execution.md) 문서. |예 |해당 없음 |
| policy |Hello 조건 또는 hello 데이터 집합 분할 영역 충족 해야 하는 hello 조건을 정의 합니다. <br/><br/>세부 정보는 [데이터 집합 정책](#Policy) 을 참조하세요. |아니요 |해당 없음 |

각 열에 hello **구조** 섹션에서는 다음과 같은 속성 hello:

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| name |Hello 열의 이름입니다. |예 |
| type |Hello 열의 데이터 형식입니다.  |아니요 |
| culture |.NET 기반 유형을 지정 하 고.NET 형식이 사용 되는 문화권 toobe `Datetime` 또는 `Datetimeoffset`합니다. 기본값은 `en-us`입니다. |아니요 |
| format |포맷 유형을 지정 하 고.NET 형식이 사용 되는 문자열 toobe `Datetime` 또는 `Datetimeoffset`합니다. |아니요 |

다음 예제는 hello, hello 데이터 집합에 3 개의 열이 `slicetimestamp`, `projectname`, 및 `pageviews` 유형의 일부인 및: 문자열, 문자열 및 Decimal 각각.

```json
structure:  
[
    { "name": "slicetimestamp", "type": "String"},
    { "name": "projectname", "type": "String"},
    { "name": "pageviews", "type": "Decimal"}
]
```

hello 다음 표에서 설명 hello에 사용할 수 있는 속성 **가용성** 섹션:

| 속성 | 설명 | 필수 | 기본값 |
| --- | --- | --- | --- |
| frequency |데이터 집합 조각 프로덕션에 대 한 hello 시간 단위를 지정합니다.<br/><br/><b>지원되는 빈도</b>: 분, 시, 일, 주, 월 |예 |해당 없음 |
| interval |빈도 승수를 지정합니다.<br/><br/>"X 주파수 간격" 결정 얼마나 자주 hello 조각이 생성 됩니다.<br/><br/>설정 하는 경우는 시간 단위로 분할 되는 데이터 집합 toobe hello 필요, <b>주파수</b> 너무<b>시간</b>, 및 <b>간격</b> 너무<b>1</b>합니다.<br/><br/><b>참고</b>: 1 분으로 주파수를 지정 하면 15 보다 작은 간격 toono hello 설정 하는 것이 좋습니다 |예 |해당 없음 |
| style |Hello 간격의 시작/끝 hello에 hello 분할 영역을 생성 해야 하는지 여부를 지정 합니다.<ul><li>StartOfInterval</li><li>EndOfInterval</li></ul><br/><br/>Frequency를 tooMonth를 설정 하는 경우 스타일 tooEndOfInterval 설정 되어 있으면 hello 달의 마지막 날에 hello 조각이 생성 됩니다. Hello 스타일 tooStartOfInterval을 설정 하는 경우에 월의 첫째 날으로 hello에 hello 조각이 생성 됩니다.<br/><br/>Frequency를 tooDay를 설정 하는 경우 스타일 tooEndOfInterval 설정 되어 있으면 hello 조각이 hello 지난 1 시간 동안 hello 하루 중에 생성 됩니다.<br/><br/>Frequency를 tooHour를 설정 하는 경우 스타일 tooEndOfInterval 설정 되어 있으면 hello 조각이 hello 시간 hello 끝에 생성 됩니다. 예를 들어, 오후 1 ~ 2 시 기간에 조각의 hello 조각이 오후 2 시 생성 됩니다. |아니요 |EndOfInterval |
| anchorDateTime |스케줄러 toocompute 데이터 집합 분할 영역 경계에 의해 사용 된 시간에 hello 절대 위치를 정의 합니다. <br/><br/><b>참고</b>: hello AnchorDateTime에 hello 빈도 보다 더 세부적인 날짜 부분이 경우 hello 더 세분화 된 부분은 무시 됩니다. <br/><br/>예를 들어 경우 hello, <b>간격</b> 은 <b>매시간</b> (빈도: 시간 및 간격: 1) 및 hello <b>AnchorDateTime</b> 포함 <b>, 분, 초</b>다음 hello <b>, 분, 초</b> hello AnchorDateTime의 일부는 무시 됩니다. |아니요 |01/01/0001 |
| offset |어떤 hello에서 모든 데이터 집합 분할 영역의 시작과 끝을 향해 이동 하는 Timespan입니다. <br/><br/><b>참고</b>: hello 결과 결합 된 hello shift anchorDateTime 및 offset을 모두를 지정 합니다. |아니요 |해당 없음 |

가용성 섹션 뒤 hello 지정 hello 출력 데이터 집합의는 생성 된 시간별 (또는) 입력 데이터 집합은 1 시간 마다:

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 1    
}
```

hello **정책** 데이터 집합 정의 섹션 hello 조건 정의 또는 데이터 집합 분할 영역 hello hello 조건을 충족 해야 합니다.

| 정책 이름 | 설명 | 너무 적용| 필수 | 기본값 |
| --- | --- | --- | --- | --- |
| minimumSizeMB |Hello 데이터에 유효성을 검사 한 **Azure blob** 충족 hello 최소 크기 요구 사항 (메가바이트)입니다. |Azure Blob |아니요 |해당 없음 |
| minimumRows |Hello 데이터에 유효성을 검사 한 **Azure SQL 데이터베이스** 또는 **Azure 테이블** hello 최소 행 수를 포함 합니다. |<ul><li>Azure SQL Database</li><li>Azure 테이블</li></ul> |아니요 |해당 없음 |

**예제:**

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

데이터 집합이 Azure Data Factory에서 생성되지 않는 한 **external**로 표시되어야 합니다. 이 설정은 일반적으로 활동 또는 파이프라인 체인 사용 되지 않은 경우 파이프라인의 첫 번째 활동의 toohello 입력을 적용 합니다.

| 이름 | 설명 | 필수 | 기본값 |
| --- | --- | --- | --- |
| dataDelay |시간 toodelay hello 가능 여부 확인 hello hello slice를 지정 하는 hello에 대 한 외부 데이터입니다. 예를 들어 매시간 hello 데이터를 사용할 수, hello 검사 toosee hello 외부 데이터를 사용할 수 있으며 해당 조각이 hello dataDelay를 사용 하 여 준비 지연 될 수 있습니다.<br/><br/>만 toohello를 현재 시간 적용합니다.  예를 들어 지금 바로 오후 1시 이므로이 값은 10 분 hello 유효성 검사 오후 1 시 10 분에 시작 합니다.<br/><br/>이 설정은 지난 hello에서 분할 영역에는 영향을 주지 (분할 영역 조각 종료 시간 + dataDelay < 이제) 지연 없이 처리 됩니다.<br/><br/>23:59 시간 필요 toospecified hello를 사용 하 여 보다 큰 시간 `day.hours:minutes:seconds` 형식입니다. 예를 들어 toospecify 24 시간 동안 사용 하지 않는 24시: 00입니다. 나타내는 대신 사용 합니다. 24:00:00을 사용하면 24일(24.00:00:00)로 처리됩니다. 1일 4시간의 경우 1:04:00:00을 지정합니다. |아니요 |0 |
| retryInterval |hello 대기는 실패 및 hello 다음 다시 시도 사이의 시간입니다. Try 실패할 경우 retryInterval 후 hello 다음 시도가 됩니다. <br/><br/>지금 바로 오후 1시 이면 hello 첫 번째 시도 시작 하기. Hello 기간 toocomplete hello 첫 번째 유효성 검사 1 분 이며 hello 작업이 실패 했습니다 hello 다음 재시도에 않은 경우에 1시 + 1 분 (기간) + 1 분 (다시 시도 간격) = 오후 1시 02분 합니다. <br/><br/>지난 hello에 조각에 대 한 지연 되지 않습니다. hello 재시도 즉시 전파 합니다. |아니요 |00:01:00 (1분) |
| retryTimeout |각 다시 시도 대 한 hello 제한 시간입니다.<br/><br/>이 속성을 설정 하는 경우 too10 분 hello 유효성 검사 요구 toobe 10 분 이내에 완료 합니다. 10 분 tooperform hello 유효성 검사 보다 시간이 오래 걸리는 경우 제한 시간이 초과 hello에 다시 시도 합니다.<br/><br/>Hello 유효성 검사에 대 한 모든 시도 시간이 초과 되 면 hello 조각 TimedOut으로 표시 됩니다. |아니요 |00:10:00 (10분) |
| maximumRetry |횟수 toocheck hello 외부 데이터의 가용성을 hello에 대 한입니다. hello 허용 최대값은 10입니다. |아니요 |3 |


## <a name="data-stores"></a>데이터 저장소
hello [연결 된 서비스](#linked-service) 일반적인 tooall 유형의 연결 된 서비스 JSON 요소에 대 한 설명 섹션을 제공 합니다. 이 섹션에서는 JSON 요소를 특정 tooeach 데이터 저장소에 대 한 세부 정보를 제공 합니다.

hello [Dataset](#dataset) JSON 요소를 일반적인 tooall 유형의 데이터 집합에 대 한 설명 섹션을 제공 합니다. 이 섹션에서는 JSON 요소를 특정 tooeach 데이터 저장소에 대 한 세부 정보를 제공 합니다.

hello [활동](#activity) JSON 요소를 일반적인 tooall 유형의 활동에 대 한 설명 섹션을 제공 합니다. 이 섹션에서는 특정 tooeach 데이터 저장소는 복사 작업에는 원본/싱크로 사용 하는 경우 JSON 요소에 대 한 세부 정보를 제공 합니다.  

Hello 저장소 연결 된 서비스, 데이터 집합에 대 한 toosee hello JSON 스키마에 관심이 및 소스/hello 복사 작업에 대 한 싱크 hello에 대 한 hello 링크를 클릭 합니다.

| Category | 데이터 저장소 
|:--- |:--- |
| **Azure** |[Azure Blob 저장소](#azure-blob-storage) |
| &nbsp; |[Azure 데이터 레이크 저장소](#azure-datalake-store) |
| &nbsp; |[Azure Cosmos DB](#azure-cosmos-db) |
| &nbsp; |[Azure SQL Database](#azure-sql-database) |
| &nbsp; |[Azure SQL Data Warehouse](#azure-sql-data-warehouse) |
| &nbsp; |[Azure 검색](#azure-search) |
| &nbsp; |[Azure Table Storage](#azure-table-storage) |
| **데이터베이스** |[Amazon Redshift](#amazon-redshift) |
| &nbsp; |[IBM DB2](#ibm-db2) |
| &nbsp; |[MySQL](#mysql) |
| &nbsp; |[Oracle](#oracle) |
| &nbsp; |[PostgreSQL](#postgresql) |
| &nbsp; |[SAP Business Warehouse](#sap-business-warehouse) |
| &nbsp; |[SAP HANA](#sap-hana) |
| &nbsp; |[SQL Server](#sql-server) |
| &nbsp; |[Sybase](#sybase) |
| &nbsp; |[Teradata](#teradata) |
| **NoSQL** |[Cassandra](#cassandra) |
| &nbsp; |[MongoDB](#mongodb) |
| **파일** |[Amazon S3](#amazon-s3) |
| &nbsp; |[파일 시스템](#file-system) |
| &nbsp; |[FTP](#ftp) |
| &nbsp; |[HDFS](#hdfs) |
| &nbsp; |[SFTP](#sftp) |
| **기타** |[HTTP](#http) |
| &nbsp; |[OData](#odata) |
| &nbsp; |[ODBC](#odbc) |
| &nbsp; |[Salesforce](#salesforce) |
| &nbsp; |[웹 테이블](#web-table) |

## <a name="azure-blob-storage"></a>데이터 이동

### <a name="linked-service"></a>연결된 서비스
연결된 서비스에는 두 가지 유형, 즉 Azure Storage 연결된 서비스와 Azure Storage SAS 연결된 서비스가 있습니다.

#### <a name="azure-storage-linked-service"></a>Azure 저장소 연결된 서비스
toolink hello를 사용 하 여 Azure 저장소 계정 tooa 데이터 팩터리 **계정 키**, Azure 저장소 연결 서비스를 만듭니다. toodefine Azure 저장소 연결 된 서비스를 집합 hello **형식** hello 연결 서비스 너무**AzureStorage**합니다. 그런 다음, 다음 속성 hello에 지정할 수 **typeProperties** 섹션:  

| 속성 | 설명 | 필수 |
|:--- |:--- |:--- |
| connectionString |Hello connectionString 속성에 대 한 tooconnect tooAzure 저장소는 데 필요한 정보를 지정 합니다. |예 |

##### <a name="example"></a>예제  

```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
```

#### <a name="azure-storage-sas-linked-service"></a>Azure Storage SAS 연결된 서비스
hello Azure 저장소 SAS 연결 된 서비스는 공유 액세스 서명 (SAS)를 사용 하 여 Azure 저장소 계정 tooan Azure 데이터 팩터리에 toolink를 허용 합니다. Hello 저장소의 tooall/관련 리소스 (blob/컨테이너) hello 데이터 팩터리 시간 제한/범위 액세스를 제공합니다. toolink 공유 액세스 서명을 사용 하 여 Azure 저장소 계정 tooa 데이터 팩터리는 Azure 저장소 SAS 연결 된 서비스를 만듭니다. 연결 된 서비스를 집합 hello Azure 저장소 SAS toodefine **형식** hello 연결 서비스 너무**AzureStorageSas**합니다. 그런 다음, 다음 속성 hello에 지정할 수 **typeProperties** 섹션:   

| 속성 | 설명 | 필수 |
|:--- |:--- |:--- |
| sasUri |Blob, 컨테이너, 테이블 등 공유 액세스 서명 URI toohello Azure 저장소 리소스를 지정 합니다. |예 |

##### <a name="example"></a>예제

```json
{  
    "name": "StorageSasLinkedService",  
    "properties": {  
        "type": "AzureStorageSas",  
        "typeProperties": {  
            "sasUri": "<storageUri>?<sasToken>"   
        }  
    }  
}  
```

이러한 연결된 서비스에 대한 자세한 내용은 [Azure Blob Storage 커넥터](data-factory-azure-blob-connector.md#linked-service-properties) 문서를 참조하세요. 

### <a name="dataset"></a>데이터 집합
toodefine 된 Azure Blob 데이터 집합을 집합 hello **형식** hello 데이터 집합의 너무**AzureBlob**합니다. 그런 다음 hello 다음과 같은 Azure Blob hello에서 특정 속성을 지정 **typeProperties** 섹션: 

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| folderPath |경로 toohello 컨테이너 및 blob 저장소 hello에에서 폴더입니다. 예제: myblobcontainer\myblobfolder\ |예 |
| fileName |Hello blob 이름입니다. fileName은 선택 사항이며 대/소문자를 구분합니다.<br/><br/>에 파일 이름, hello 작업 (복사본 포함) 작동을 지정한 경우에 특정 Blob을 hello 합니다.<br/><br/>파일 이름을 지정 하지 않으면 복사 입력된 데이터 집합에 대 한 hello folderPath에 모든 Blob을 포함 합니다.<br/><br/>Hello 생성 된 파일의 이름을 hello 것이 형식에 따라 hello에 출력 데이터 집합에 대 한 파일 이름을 지정 하지 않으면,: 데이터입니다. <Guid>.txt (예:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt |아니요 |
| partitionedBy |partitionedBy는 선택적 속성입니다. 사용할 수 있습니다 toospecify 동적 folderPath 및 filename 시계열 데이터에 대 한 합니다. 예를 들어 folderPath는 매시간 데이터에 대한 매개 변수화됩니다. |아니요 |
| format | hello 형식 유형만 지원 됩니다: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**합니다. 집합 hello **형식** 이러한 값의 형식 tooone 아래의 속성입니다. 자세한 내용은 [텍스트 형식](data-factory-supported-file-and-compression-formats.md#text-format), [Json 형식](data-factory-supported-file-and-compression-formats.md#json-format), [Avro 형식](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc 형식](data-factory-supported-file-and-compression-formats.md#orc-format) 및 [Parquet 형식](data-factory-supported-file-and-compression-formats.md#parquet-format) 섹션을 참조하세요. <br><br> 너무 하려는 경우**파일을 다음으로 복사-은** 간의 파일 기반 저장소 (이진 복사), 두 입력 및 출력 데이터 집합 정의의 hello 형식 섹션을 건너뛰십시오. |아니요 |
| 압축 | Hello 유형 및 hello 데이터에 대 한 압축 수준을 지정 합니다. 지원되는 형식은 **GZip**, **Deflate**, **BZip2** 및 **ZipDeflate**입니다. 지원되는 수준은 **최적** 및 **가장 빠름**입니다. 자세한 내용은 [Azure Data Factory의 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md#compression-support)을 참조하세요. |아니요 |

#### <a name="example"></a>예제

```json
{
    "name": "AzureBlobInput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "fileName": "input.log",
            "folderPath": "adfgetstarted/inputdata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
 ```


자세한 내용은 [Azure Blob 커넥터](data-factory-azure-blob-connector.md#dataset-properties) 문서를 참조하세요.

### <a name="blobsource-in-copy-activity"></a>복사 활동의 BlobSource
Azure Blob 저장소에서 데이터를 복사 하는 경우 설정 hello **소스 형식** hello의 복사 작업이 너무**BlobSource**, 다음 hello에 대 한 속성을 지정 하 고 * * 소스 * * 섹션:

| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| recursive |Hello 데이터 읽는지 재귀적으로 hello 하위 폴더 또는 hello 지정한 폴더에서만 나타냅니다. |True(기본값), False |아니요 |

#### <a name="example-blobsource"></a>예제: BlobSource**
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQL",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureSqlOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "SqlSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
### <a name="blobsink-in-copy-activity"></a>복사 활동의 BlobSink
데이터 tooan Azure Blob 저장소를 복사 하는 경우 설정 hello **싱크 유형** hello의 복사 작업이 너무**BlobSink**, 다음 hello에 대 한 속성을 지정 하 고 **싱크** 섹션:

| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| copyBehavior |파일 시스템이 나 BlobSource hello 원본이 상태인 hello 복사 동작을 정의 합니다. |<b>PreserveHierarchy</b>: 전처리 hello hello 대상 폴더에서 파일 계층 구조입니다. hello 소스 파일 toosource 폴더의 상대 경로 동일한 toohello 대상 파일 tootarget 폴더의 상대 경로입니다.<br/><br/><b>FlattenHierarchy</b>: hello 원본 폴더에서 모든 파일에에서 있는 hello 먼저 대상 폴더의 수준입니다. hello 대상 파일에는 자동 생성 된 이름이 있습니다. <br/><br/><b>(기본값) MergeFiles:</b> hello 소스 폴더 tooone 파일에서 모든 파일을 병합 합니다. Hello 병합 된 파일 이름이 name을 지정된 하는 hello; 됩니다 hello 파일/Blob 이름이 지정 된 경우 그렇지 않은 경우 자동으로 생성 된 파일 이름 것입니다. |아니요 |

#### <a name="example-blobsink"></a>예제: BlobSink

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSQLInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

자세한 내용은 [Azure Blob 커넥터](data-factory-azure-blob-connector.md#copy-activity-properties) 문서를 참조하세요. 

## <a name="azure-data-lake-store"></a>Azure Data Lake Store

### <a name="linked-service"></a>연결된 서비스
Azure 데이터 레이크 저장소 연결 서비스 toodefine 집합 hello 유형의 hello 연결 된 서비스 너무**AzureDataLakeStore**, 다음 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션:  

| 속성 | 설명 | 필수 |
|:--- |:--- |:--- |
| type | hello type 속성 설정 해야 합니다: **AzureDataLakeStore** | 예 |
| dataLakeStoreUri | Hello Azure 데이터 레이크 저장소 계정에 대 한 정보를 지정 합니다. 형식에 따라 hello에: `https://[accountname].azuredatalakestore.net/webhdfs/v1` 또는 `adl://[accountname].azuredatalakestore.net/`합니다. | 예 |
| subscriptionId | Azure 구독 Id toowhich 데이터 레이크 저장소 속해 있습니다. | 싱크에 필요 |
| resourceGroupName | Azure 리소스 그룹 이름 toowhich 데이터 레이크 저장소 속해 있습니다. | 싱크에 필요 |
| servicePrincipalId | Hello 응용 프로그램의 클라이언트 ID를 지정 | 예(서비스 주체 인증의 경우) |
| servicePrincipalKey | Hello 응용 프로그램의 키를 지정 합니다. | 예(서비스 주체 인증의 경우) |
| tenant | 응용 프로그램에 속한 아래 hello 테 넌 트 정보 (도메인 이름 또는 테 넌 트 ID)를 지정 합니다. Hello Azure 포털의 hello 오른쪽 위 모서리에 hello 마우스 호버 하 여 검색할 수 있습니다. | 예(서비스 주체 인증의 경우) |
| 권한 부여 | 클릭 **Authorize** hello 단추 **데이터 팩터리 편집기** hello 자동 생성 된 권한 부여 URL toothis 속성에 할당 하 여 자격 증명을 입력 합니다. | 예(사용자 자격 증명 인증의 경우)|
| sessionId | Hello OAuth 권한 부여 세션에서 OAuth 세션 id입니다. 각 세션 ID는 고유하고 한 번만 사용될 수 있으며  이 설정은 Data Factory 편집기를 사용하는 경우 자동으로 생성됩니다. | 예(사용자 자격 증명 인증의 경우) |

#### <a name="example-using-service-principal-authentication"></a>예제: 서비스 주체 인증 사용
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info. Example: microsoft.onmicrosoft.com>"
        }
    }
}
```

#### <a name="example-using-user-credential-authentication"></a>예제: 사용자 자격 증명 인증 사용
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<session ID>",
            "authorization": "<authorization URL>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

자세한 내용은 [Azure Data Lake Store 커넥터](data-factory-azure-datalake-connector.md#linked-service-properties) 문서를 참조하세요. 

### <a name="dataset"></a>데이터 집합
Azure 데이터 레이크 저장소에서 데이터 집합 toodefine 집합 hello **형식** hello 데이터 집합의 너무**AzureDataLakeStore**, hello 다음과 같은 hello에 대 한 속성을 지정 하 고 **typeProperties**섹션: 

| 속성 | 설명 | 필수 |
|:--- |:--- |:--- |
| folderPath |Hello Azure 데이터 레이크의 경로 toohello 컨테이너 및 폴더를 저장 합니다. |예 |
| fileName |Hello Azure 데이터 레이크 저장소의 hello 파일의 이름입니다. fileName은 선택 사항이며 대/소문자를 구분합니다. <br/><br/>이름을 지정 하는 경우 (복사본 포함) hello 활동 hello 특정 파일에 작동 합니다.<br/><br/>FileName을 지정 하지 않으면 복사 입력된 데이터 집합에 대 한 hello folderPath의 모든 파일을 포함 합니다.<br/><br/>Hello 생성 된 파일의 이름을 hello 것이 형식에 따라 hello에 출력 데이터 집합에 대 한 파일 이름을 지정 하지 않으면,: 데이터입니다. <Guid>.txt (예:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt |아니요 |
| partitionedBy |partitionedBy는 선택적 속성입니다. 사용할 수 있습니다 toospecify 동적 folderPath 및 filename 시계열 데이터에 대 한 합니다. 예를 들어 folderPath는 매시간 데이터에 대한 매개 변수화됩니다. |아니요 |
| format | hello 형식 유형만 지원 됩니다: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**합니다. 집합 hello **형식** 이러한 값의 형식 tooone 아래의 속성입니다. 자세한 내용은 [텍스트 형식](data-factory-supported-file-and-compression-formats.md#text-format), [Json 형식](data-factory-supported-file-and-compression-formats.md#json-format), [Avro 형식](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc 형식](data-factory-supported-file-and-compression-formats.md#orc-format) 및 [Parquet 형식](data-factory-supported-file-and-compression-formats.md#parquet-format) 섹션을 참조하세요. <br><br> 너무 하려는 경우**파일을 다음으로 복사-은** 간의 파일 기반 저장소 (이진 복사), 두 입력 및 출력 데이터 집합 정의의 hello 형식 섹션을 건너뛰십시오. |아니요 |
| 압축 | Hello 유형 및 hello 데이터에 대 한 압축 수준을 지정 합니다. 지원되는 형식은 **GZip**, **Deflate**, **BZip2** 및 **ZipDeflate**입니다. 지원되는 수준은 **최적** 및 **가장 빠름**입니다. 자세한 내용은 [Azure Data Factory의 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md#compression-support)을 참조하세요. |아니요 |

#### <a name="example"></a>예제
```json
{
    "name": "AzureDataLakeStoreInput",
    "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/input/",
            "fileName": "SearchLog.tsv",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            }
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

자세한 내용은 [Azure Data Lake Store 커넥터](data-factory-azure-datalake-connector.md#dataset-properties) 문서를 참조하세요. 

### <a name="azure-data-lake-store-source-in-copy-activity"></a>복사 활동의 Azure Data Lake Store 소스
Azure 데이터 레이크 저장소에서 데이터를 복사 하는 경우 설정 hello **소스 형식** hello의 복사 작업이 너무**AzureDataLakeStoreSource**, 다음 hello에 대 한 속성을 지정 하 고 **소스**  섹션:

**AzureDataLakeStoreSource** hello 다음과 같은 속성을 지 원하는 **typeProperties** 섹션:

| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| recursive |Hello 데이터 읽는지 재귀적으로 hello 하위 폴더 또는 hello 지정한 폴더에서만 나타냅니다. |True(기본값), False |아니요 |

#### <a name="example-azuredatalakestoresource"></a>예제: AzureDataLakeStoreSource

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureDakeLaketoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureDataLakeStoreInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "AzureDataLakeStoreSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

자세한 내용은 [Azure Data Lake Store 커넥터](data-factory-azure-datalake-connector.md#copy-activity-properties) 문서를 참조하세요.

### <a name="azure-data-lake-store-sink-in-copy-activity"></a>복사 활동의 Azure Data Lake Store 싱크
데이터 tooan Azure 데이터 레이크 저장소를 복사 하는 경우 설정 hello **싱크 유형** hello의 복사 작업이 너무**AzureDataLakeStoreSink**, 다음 hello에 대 한 속성을 지정 하 고 **싱크**섹션:

| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| copyBehavior |Hello 복사 동작을 지정합니다. |<b>PreserveHierarchy</b>: 전처리 hello hello 대상 폴더에서 파일 계층 구조입니다. hello 소스 파일 toosource 폴더의 상대 경로 동일한 toohello 대상 파일 tootarget 폴더의 상대 경로입니다.<br/><br/><b>FlattenHierarchy</b>: hello 원본 폴더에서 모든 파일은 hello 첫 번째 수준의 대상 폴더에 만들어집니다. hello 대상 파일은 자동 생성 된 이름으로 만들어집니다.<br/><br/><b>MergeFiles</b>: hello 소스 폴더 tooone 파일에서 모든 파일을 병합 합니다. Hello 병합 된 파일 이름이 name을 지정된 하는 hello; 됩니다 hello 파일/Blob 이름이 지정 된 경우 그렇지 않은 경우 자동으로 생성 된 파일 이름 것입니다. |아니요 |

#### <a name="example-azuredatalakestoresink"></a>예제: AzureDataLakeStoreSink
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoDataLake",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureDataLakeStoreOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "AzureDataLakeStoreSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

자세한 내용은 [Azure Data Lake Store 커넥터](data-factory-azure-datalake-connector.md#copy-activity-properties) 문서를 참조하세요. 

## <a name="azure-cosmos-db"></a>Azure Cosmos DB  

### <a name="linked-service"></a>연결된 서비스
연결 된 서비스를 집합 hello Azure Cosmos DB toodefine **형식** hello 연결 서비스 너무**DocumentDb**, 다음 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션 내용  

| **속성** | **설명** | **필수** |
| --- | --- | --- |
| connectionString |Tooconnect tooAzure Cosmos DB 데이터베이스는 데 필요한 정보를 지정 합니다. |예 |

#### <a name="example"></a>예제

```json
{
    "name": "CosmosDBLinkedService",
    "properties": {
        "type": "DocumentDb",
        "typeProperties": {
            "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
        }
    }
}
```
자세한 내용은 [Azure Cosmos DB 커넥터](data-factory-azure-documentdb-connector.md#linked-service-properties) 문서를 참조하세요.

### <a name="dataset"></a>데이터 집합
toodefine Azure Cosmos DB dataset 집합 hello **형식** hello 데이터 집합의 너무**DocumentDbCollection**, hello 다음과 같은 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션 내용 

| **속성** | **설명** | **필수** |
| --- | --- | --- |
| collectionName |Hello Azure Cosmos DB 컬렉션의 이름입니다. |예 |

#### <a name="example"></a>예제

```json
{
    "name": "PersonCosmosDBTable",
    "properties": {
        "type": "DocumentDbCollection",
        "linkedServiceName": "CosmosDBLinkedService",
        "typeProperties": {
            "collectionName": "Person"
        },
        "external": true,
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```
자세한 내용은 [Azure Cosmos DB 커넥터](data-factory-azure-documentdb-connector.md#dataset-properties) 문서를 참조하세요.

### <a name="azure-cosmos-db-collection-source-in-copy-activity"></a>복사 작업에서 Azure Cosmos DB 컬렉션 원본
Azure Cosmos DB에서 데이터를 복사 하는 경우 설정 hello **소스 형식** hello의 복사 작업이 너무**DocumentDbCollectionSource**, 다음 hello에 대 한 속성을 지정 하 고 **소스** 섹션:


| **속성** | **설명** | **허용되는 값** | **필수** |
| --- | --- | --- | --- |
| 쿼리 |Hello tooread 데이터 쿼리를 지정 합니다. |Azure Cosmos DB에서 지원하는 쿼리 문자열입니다. <br/><br/>예: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"` |아니요 <br/><br/>지정 하지 않으면 실행 되는 SQL 문을 hello:`select <columns defined in structure> from mycollection` |
| nestingSeparator |문서 hello 특수 문자 tooindicate 중첩 |모든 character입니다. <br/><br/>Azure Cosmos DB는 중첩된 구조를 허용하는 JSON 문서용 NoSQL 저장소입니다. Azure 데이터 팩터리는 nestingSeparator 통해 사용자 toodenote 계층 구조를 사용 하면 "." 위의 예제 안녕하세요에. Hello 구분 기호 hello 복사 작업에서는 생성 3 명의 자식 요소가 있는 hello "Name" 개체 첫 번째, 중간 및 마지막를 따라 too"Name.First", "Name.Middle" 및 "Name.Last" hello에 테이블 정의 합니다. |아니요 |

#### <a name="example"></a>예제

```json
{
    "name": "DocDbToBlobPipeline",
    "properties": {
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "DocumentDbCollectionSource",
                    "query": "SELECT Person.Id, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person",
                    "nestingSeparator": "."
                },
                "sink": {
                    "type": "BlobSink",
                    "blobWriterAddHeader": true,
                    "writeBatchSize": 1000,
                    "writeBatchTimeout": "00:00:59"
                }
            },
            "inputs": [{
                "name": "PersonCosmosDBTable"
            }],
            "outputs": [{
                "name": "PersonBlobTableOut"
            }],
            "policy": {
                "concurrency": 1
            },
            "name": "CopyFromCosmosDbToBlob"
        }],
        "start": "2016-04-01T00:00:00",
        "end": "2016-04-02T00:00:00"
    }
}
```

### <a name="azure-cosmos-db-collection-sink-in-copy-activity"></a>복사 작업의 Azure Cosmos DB 컬렉션 싱크
데이터 tooAzure Cosmos DB 복사 하는 경우 설정 hello **싱크 유형** hello의 복사 작업이 너무**DocumentDbCollectionSink**, 다음 hello에 대 한 속성을 지정 하 고 **싱크**섹션:

| **속성** | **설명** | **허용되는 값** | **필수** |
| --- | --- | --- | --- |
| nestingSeparator |Hello 원본 열 이름 tooindicate 중첩 문서에에서 특수 문자 필요 합니다. <br/><br/>예를 들어 위의: `Name.First` hello 출력 테이블 생성 하는 hello Cosmos DB 문서의 JSON 구조를 다음 hello:<br/><br/>"Name": {<br/>    "First": "John"<br/>}, |문자는 사용 되는 tooseparate 중첩 수준입니다.<br/><br/>기본값은 `.`.(점)입니다. |문자는 사용 되는 tooseparate 중첩 수준입니다. <br/><br/>기본값은 `.`.(점)입니다. |
| writeBatchSize |TooAzure Cosmos DB 서비스 toocreate 문서를 요청 하는 병렬의 수입니다.<br/><br/>이 속성을 사용 하 여 Azure Cosmos DB에서 데이터를 복사할 때 hello 성능을 미세 조정할 수 있습니다. 더 많은 병렬 요청 tooAzure Cosmos DB 보내지므로 writeBatchSize를 늘리면 성능이 향상을 기대할 수 있습니다. 그러나 조정을 tooavoid 해야 hello 오류 메시지가 발생할 수 있습니다: "요청 빈도가 높습니다."입니다.<br/><br/>제한은 문서의 크기, 문서에서 용어의 수, 대상 컬렉션의 인덱싱 정책 등 여러 가지 요인으로 결정됩니다. 복사 작업을 사용할 수 있습니다 더 나은 컬렉션 (예를 들어 S3) toohave hello 사용 가능한 대부분 처리량 (2,500 단위 수/초를 요청 하는 데 사용). |Integer |아니요(기본값: 5) |
| writeBatchTimeout |대기 시간이 초과 되기 전에 작업 toocomplete hello에 대 한 시간입니다. |timespan<br/><br/> 예: “00:30:00”(30분). |아니요 |

#### <a name="example"></a>예제

```json
{
    "name": "BlobToDocDbPipeline",
    "properties": {
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "DocumentDbCollectionSink",
                    "nestingSeparator": ".",
                    "writeBatchSize": 2,
                    "writeBatchTimeout": "00:00:00"
                },
                "translator": {
                    "type": "TabularTranslator",
                    "ColumnMappings": "FirstName: Name.First, MiddleName: Name.Middle, LastName: Name.Last, BusinessEntityID: BusinessEntityID, PersonType: PersonType, NameStyle: NameStyle, title: aaaTitle, Suffix: Suffix"
                }
            },
            "inputs": [{
                "name": "PersonBlobTableIn"
            }],
            "outputs": [{
                "name": "PersonCosmosDbTableOut"
            }],
            "policy": {
                "concurrency": 1
            },
            "name": "CopyFromBlobToCosmosDb"
        }],
        "start": "2016-04-14T00:00:00",
        "end": "2016-04-15T00:00:00"
    }
}
```

자세한 내용은 [Azure Cosmos DB 커넥터](data-factory-azure-documentdb-connector.md#copy-activity-properties) 문서를 참조하세요.

## <a name="azure-sql-database"></a>Azure SQL 데이터베이스

### <a name="linked-service"></a>연결된 서비스
toodefine Azure SQL 데이터베이스에 연결 된 서비스를 집합 hello **형식** hello 연결 서비스 너무**AzureSqlDatabase**, 다음 hello에 대 한 속성을 지정 하 고 **typeProperties**섹션:  

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| connectionString |Hello connectionString 속성에 대 한 tooconnect toohello Azure SQL 데이터베이스 인스턴스는 데 필요한 정보를 지정 합니다. |예 |

#### <a name="example"></a>예제
```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

자세한 내용은 [Azure SQL 커넥터](data-factory-azure-sql-connector.md#linked-service-properties) 문서를 참조하세요. 

### <a name="dataset"></a>데이터 집합
Azure SQL 데이터베이스에서 데이터 집합 toodefine 집합 hello **형식** hello 데이터 집합의 너무**AzureSqlTable**, hello 다음과 같은 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션 내용 

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| tableName |Hello 테이블 또는 뷰의 연결 된 서비스는 hello Azure SQL 데이터베이스 인스턴스의 이름이 참조 합니다. |예 |

#### <a name="example"></a>예제

```json
{
    "name": "AzureSqlInput",
    "properties": {
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
자세한 내용은 [Azure SQL 커넥터](data-factory-azure-sql-connector.md#dataset-properties) 문서를 참조하세요. 

### <a name="sql-source-in-copy-activity"></a>복사 활동의 SQL 소스
Azure SQL 데이터베이스에서 데이터를 복사 하는 경우 설정 hello **소스 형식** hello의 복사 작업이 너무**SqlSource**, 다음 hello에 대 한 속성을 지정 하 고 **소스** 섹션 내용


| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| SqlReaderQuery |사용자 지정 쿼리 tooread 데이터 hello를 사용 합니다. |SQL 쿼리 문자열. 예: `select * from MyTable`. |아니요 |
| sqlReaderStoredProcedureName |Hello 원본 테이블에서 데이터를 읽을 수 있는 프로시저를 저장 하는 hello의 이름입니다. |저장 프로시저를 hello의 이름입니다. |아니요 |
| storedProcedureParameters |Hello에 대 한 매개 변수 저장 프로시저입니다. |이름/값 쌍입니다. Hello 이름과 대/소문자 hello 저장 프로시저 매개 변수의 이름 및 매개 변수는 대/소문자 구분 일치 해야 합니다. |아니요 |

#### <a name="example"></a>예제

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSQLInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
자세한 내용은 [Azure SQL 커넥터](data-factory-azure-sql-connector.md#copy-activity-properties) 문서를 참조하세요. 

### <a name="sql-sink-in-copy-activity"></a>복사 활동의 SQL 싱크
데이터 tooAzure SQL 데이터베이스를 복사 하는 경우 설정 hello **싱크 유형** hello의 복사 작업이 너무**SqlSink**, 다음 hello에 대 한 속성을 지정 하 고 **싱크** 섹션:

| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| writeBatchTimeout |대기 시간이 초과 되기 전에 일괄 처리 삽입 작업 toocomplete hello에 대 한 시간입니다. |timespan<br/><br/> 예: “00:30:00”(30분). |아니요 |
| writeBatchSize |WriteBatchSize hello 버퍼 크기에 이르면 hello SQL 테이블에 데이터를 삽입 합니다. |정수(행 수) |아니요(기본값: 10000) |
| sqlWriterCleanupScript |특정 조각의 데이터 정리 되도록 tooexecute 복사 작업에 대 한 쿼리를 지정 합니다. |쿼리 문입니다. |아니요 |
| sliceIdentifierColumnName |특정 조각 다시 실행 시점의 데이터를 사용 하는 tooclean 변수인 자동 생성 된 조각 식별자를 가진 toofill 복사 작업에 대 한 열 이름을 지정 합니다. |이진(32) 데이터 형식이 있는 열의 열 이름입니다. |아니요 |
| sqlWriterStoredProcedureName |Hello 저장 프로시저의 이름 (업데이트/삽입) upserts 데이터 hello 대상 테이블에 있습니다. |저장 프로시저를 hello의 이름입니다. |아니요 |
| storedProcedureParameters |Hello에 대 한 매개 변수 저장 프로시저입니다. |이름/값 쌍입니다. Hello 이름과 대/소문자 hello 저장 프로시저 매개 변수의 이름 및 매개 변수는 대/소문자 구분 일치 해야 합니다. |아니요 |
| sqlWriterTableType |Hello 저장 프로시저에 사용 하는 테이블 형식 이름 toobe를 지정 합니다. 복사 활동 임시 테이블과이 테이블 형식으로 사용할 수 있는 이동 된 hello 데이터를 만듭니다. 저장된 프로시저 코드 hello 데이터를 기존 데이터와 복사를 병합할 수 있습니다. |테이블 유형 이름 |아니요 |

#### <a name="example"></a>예제

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQL",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureSqlOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource",
                    "blobColumnSeparators": ","
                },
                "sink": {
                    "type": "SqlSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

자세한 내용은 [Azure SQL 커넥터](data-factory-azure-sql-connector.md#copy-activity-properties) 문서를 참조하세요. 

## <a name="azure-sql-data-warehouse"></a>Azure SQL 데이터 웨어하우스

### <a name="linked-service"></a>연결된 서비스
연결 된 서비스를 집합 hello Azure SQL 데이터 웨어하우스 toodefine **형식** hello 연결 서비스 너무**AzureSqlDW**, 다음 hello에 대 한 속성을 지정 하 고 **typeProperties**섹션:  

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| connectionString |Hello connectionString 속성에 대 한 tooconnect toohello Azure SQL 데이터 웨어하우스 인스턴스는 데 필요한 정보를 지정 합니다. |예 |



#### <a name="example"></a>예제

```json
{
    "name": "AzureSqlDWLinkedService",
    "properties": {
        "type": "AzureSqlDW",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

자세한 내용은 [Azure SQL Data Warehouse 커넥터](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) 문서를 참조하세요. 

### <a name="dataset"></a>데이터 집합
Azure SQL 데이터 웨어하우스 데이터 집합, toodefine 집합 hello **형식** hello 데이터 집합의 너무**AzureSqlDWTable**, hello 다음과 같은 hello에 대 한 속성을 지정 하 고 **typeProperties**섹션: 

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| tableName |Hello 테이블 또는 뷰의 연결 된 서비스 hello hello Azure SQL 데이터 웨어하우스 데이터베이스의 이름은 참조 합니다. |예 |

#### <a name="example"></a>예제

```json
{
    "name": "AzureSqlDWInput",
    "properties": {
    "type": "AzureSqlDWTable",
        "linkedServiceName": "AzureSqlDWLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

자세한 내용은 [Azure SQL Data Warehouse 커넥터](data-factory-azure-sql-data-warehouse-connector.md#dataset-properties) 문서를 참조하세요. 

### <a name="sql-dw-source-in-copy-activity"></a>복사 활동의 SQL DW 소스
Azure SQL 데이터 웨어하우스 로부터 데이터를 복사 하는 경우 설정 hello **소스 형식** hello의 복사 작업이 너무**SqlDWSource**, 다음 hello에 대 한 속성을 지정 하 고 **소스**섹션:


| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| SqlReaderQuery |사용자 지정 쿼리 tooread 데이터 hello를 사용 합니다. |SQL 쿼리 문자열. 예: `select * from MyTable` |아니요 |
| sqlReaderStoredProcedureName |Hello 원본 테이블에서 데이터를 읽을 수 있는 프로시저를 저장 하는 hello의 이름입니다. |저장 프로시저를 hello의 이름입니다. |아니요 |
| storedProcedureParameters |Hello에 대 한 매개 변수 저장 프로시저입니다. |이름/값 쌍입니다. Hello 이름과 대/소문자 hello 저장 프로시저 매개 변수의 이름 및 매개 변수는 대/소문자 구분 일치 해야 합니다. |아니요 |

#### <a name="example"></a>예제

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLDWtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSqlDWInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlDWSource",
                    "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

자세한 내용은 [Azure SQL Data Warehouse 커넥터](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) 문서를 참조하세요. 

### <a name="sql-dw-sink-in-copy-activity"></a>복사 활동의 SQL DW 싱크
SQL 데이터 웨어하우스 데이터 tooAzure 복사 하는 경우 설정 hello **싱크 유형** hello의 복사 작업이 너무**SqlDWSink**, 다음 hello에 대 한 속성을 지정 하 고 **싱크** 섹션 내용

| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| sqlWriterCleanupScript |특정 조각의 데이터 정리 되도록 tooexecute 복사 작업에 대 한 쿼리를 지정 합니다. |쿼리 문입니다. |아니요 |
| allowPolyBase |나타냅니다 여부 BULKINSERT 메커니즘 대신 toouse PolyBase (있는 경우). <br/><br/> **PolyBase를 사용 하는 권장 방법은 tooload 데이터를 SQL 데이터 웨어하우스에 하는 hello입니다.** |True <br/>False(기본값) |아니요 |
| polyBaseSettings |속성 때 hello 지정할 수 있는 그룹을 **allowPolybase** 너무 속성이**true**합니다. |&nbsp; |아니요 |
| rejectValue |Hello 쿼리가 실패 하기 전에 거부 될 수 있는 행의 hello 개수 또는 비율을 지정 합니다. <br/><br/>Hello에 대 한 옵션을 거부 hello PolyBase에 대해 자세히 알아보려면 **인수** 섹션 [CREATE EXTERNAL TABLE (TRANSACT-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) 항목입니다. |0(기본값), 1, 2, … |아니요 |
| rejectType |리터럴 값 또는 백분율 hello rejectValue 옵션이 지정 되었는지 여부를 지정 합니다. |값(기본값), 백분율 |아니요 |
| rejectSampleValue |PolyBase hello 다시 거부 된 행의 hello 비율을 계산 하기 전에 행 tooretrieve hello 수를 결정 합니다. |1, 2, … |예. **rejectType**이 **백분율**인 경우 |
| useTypeDefault |PolyBase hello 텍스트 파일에서 데이터를 검색 하는 경우 toohandle 누락 값의 텍스트 파일을 구분 하는 방법을 지정 합니다.<br/><br/>hello 인수 섹션에서이 속성에 대 한 자세한 [CREATE EXTERNAL FILE FORMAT (Transact SQL)](https://msdn.microsoft.com/library/dn935026.aspx)합니다. |True, False(기본값) |아니요 |
| writeBatchSize |WriteBatchSize hello 버퍼 크기에 이르면 hello SQL 테이블에 데이터 삽입 |정수(행 수) |아니요(기본값: 10000) |
| writeBatchTimeout |대기 시간이 초과 되기 전에 일괄 처리 삽입 작업 toocomplete hello에 대 한 시간입니다. |timespan<br/><br/> 예: “00:30:00”(30분). |아니요 |

#### <a name="example"></a>예제

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQLDW",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureSqlDWOutput"
            }],
            "typeProperties": {
                "source": {
                "type": "BlobSource",
                    "blobColumnSeparators": ","
                },
                "sink": {
                    "type": "SqlDWSink",
                    "allowPolyBase": true
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

자세한 내용은 [Azure SQL Data Warehouse 커넥터](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) 문서를 참조하세요. 

## <a name="azure-search"></a>Azure 검색

### <a name="linked-service"></a>연결된 서비스
연결 된 서비스를 집합 hello Azure 검색 toodefine **형식** hello 연결 서비스 너무**AzureSearch**, 다음 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션 내용  

| 속성 | 설명 | 필수 |
| -------- | ----------- | -------- |
| url | Hello Azure 검색 서비스에 대 한 URL입니다. | 예 |
| key | Hello Azure 검색 서비스에 대 한 관리자 키입니다. | 예 |

#### <a name="example"></a>예제

```json
{
    "name": "AzureSearchLinkedService",
    "properties": {
        "type": "AzureSearch",
        "typeProperties": {
            "url": "https://<service>.search.windows.net",
            "key": "<AdminKey>"
        }
    }
}
```

자세한 내용은 [Azure Search 커넥터](data-factory-azure-search-connector.md#linked-service-properties) 문서를 참조하세요.

### <a name="dataset"></a>데이터 집합
Azure 검색 된 데이터 집합 toodefine 집합 hello **형식** hello 데이터 집합의 너무**AzureSearchIndex**, hello 다음과 같은 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션 : 

| 속성 | 설명 | 필수 |
| -------- | ----------- | -------- |
| type | 너무 hello 유형 속성을 설정 해야**AzureSearchIndex**합니다.| 예 |
| indexName | Hello Azure 검색 인덱스의 이름입니다. 데이터 팩터리 hello 인덱스가 생성 되지 않습니다. hello 인덱스 Azure 검색에 있어야 합니다. | 예 |

#### <a name="example"></a>예제

```json
{
    "name": "AzureSearchIndexDataset",
    "properties": {
        "type": "AzureSearchIndex",
        "linkedServiceName": "AzureSearchLinkedService",
        "typeProperties": {
            "indexName": "products"
        },
        "availability": {
            "frequency": "Minute",
            "interval": 15
        }
    }
}
```

자세한 내용은 [Azure Search 커넥터](data-factory-azure-search-connector.md#dataset-properties) 문서를 참조하세요.

### <a name="azure-search-index-sink-in-copy-activity"></a>복사 활동의 Azure Search 인덱스 싱크
데이터 tooan Azure 검색 인덱스를 복사 하는 경우 설정 hello **싱크 유형** hello의 복사 작업이 너무**AzureSearchIndexSink**, 다음 hello에 대 한 속성을 지정 하 고 **싱크**섹션:

| 속성 | 설명 | 허용되는 값 | 필수 |
| -------- | ----------- | -------------- | -------- |
| WriteBehavior | Toomerge 또는 교체 때 문서에에서 이미 있는지 hello 인덱스를 지정 합니다. | 병합(기본값)<br/>업로드| 아니요 |
| writeBatchSize | WriteBatchSize hello 버퍼 크기에 이르면 hello Azure 검색 인덱스에 데이터를 업로드 합니다. | too1이 1, 000입니다. 기본값은 1,000입니다. | 아니요 |

#### <a name="example"></a>예제

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "SqlServertoAzureSearchIndex",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": " SqlServerInput"
            }],
            "outputs": [{
                "name": "AzureSearchIndexDataset"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "AzureSearchIndexSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

자세한 내용은 [Azure Search 커넥터](data-factory-azure-search-connector.md#copy-activity-properties) 문서를 참조하세요.

## <a name="azure-table-storage"></a>Azure Table Storage

### <a name="linked-service"></a>연결된 서비스
연결된 서비스에는 두 가지 유형, 즉 Azure Storage 연결된 서비스와 Azure Storage SAS 연결된 서비스가 있습니다.

#### <a name="azure-storage-linked-service"></a>Azure 저장소 연결된 서비스
toolink hello를 사용 하 여 Azure 저장소 계정 tooa 데이터 팩터리 **계정 키**, Azure 저장소 연결 서비스를 만듭니다. toodefine Azure 저장소 연결 된 서비스를 집합 hello **형식** hello 연결 서비스 너무**AzureStorage**합니다. 그런 다음, 다음 속성 hello에 지정할 수 **typeProperties** 섹션:  

| 속성 | 설명 | 필수 |
|:--- |:--- |:--- |
| type |hello type 속성 설정 해야 합니다: **AzureStorage** |예 |
| connectionString |Hello connectionString 속성에 대 한 tooconnect tooAzure 저장소는 데 필요한 정보를 지정 합니다. |예 |

**예제:**  

```json
{  
    "name": "StorageLinkedService",  
    "properties": {  
        "type": "AzureStorage",  
        "typeProperties": {  
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"  
        }  
    }  
}  
```

#### <a name="azure-storage-sas-linked-service"></a>Azure Storage SAS 연결된 서비스
hello Azure 저장소 SAS 연결 된 서비스는 공유 액세스 서명 (SAS)를 사용 하 여 Azure 저장소 계정 tooan Azure 데이터 팩터리에 toolink를 허용 합니다. Hello 저장소의 tooall/관련 리소스 (blob/컨테이너) hello 데이터 팩터리 시간 제한/범위 액세스를 제공합니다. toolink 공유 액세스 서명을 사용 하 여 Azure 저장소 계정 tooa 데이터 팩터리는 Azure 저장소 SAS 연결 된 서비스를 만듭니다. 연결 된 서비스를 집합 hello Azure 저장소 SAS toodefine **형식** hello 연결 서비스 너무**AzureStorageSas**합니다. 그런 다음, 다음 속성 hello에 지정할 수 **typeProperties** 섹션:   

| 속성 | 설명 | 필수 |
|:--- |:--- |:--- |
| type |hello type 속성 설정 해야 합니다: **AzureStorageSas** |예 |
| sasUri |Blob, 컨테이너, 테이블 등 공유 액세스 서명 URI toohello Azure 저장소 리소스를 지정 합니다. |예 |

**예제:**

```json
{  
    "name": "StorageSasLinkedService",  
    "properties": {  
        "type": "AzureStorageSas",  
        "typeProperties": {  
            "sasUri": "<storageUri>?<sasToken>"   
        }  
    }  
}  
```

이러한 연결된 서비스에 대한 자세한 내용은 [Azure Table Storage 커넥터](data-factory-azure-table-connector.md#linked-service-properties) 문서를 참조하세요. 

### <a name="dataset"></a>데이터 집합
Azure 테이블에서 데이터 집합 toodefine 집합 hello **형식** hello 데이터 집합의 너무**AzureTable**, hello 다음과 같은 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션: 

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| tableName |연결 된 서비스는 hello Azure 테이블 데이터베이스 인스턴스의 hello 테이블의 이름은 참조 합니다. |예. 를 azureTableSourceQuery 없이 tableName을 지정 하는 경우 hello 테이블의 모든 레코드가 복사한 toohello 대상 됩니다. Hello 쿼리를 충족 하는 hello 테이블에서 레코드는 azureTableSourceQuery도 지정 되어 경우 복사한 toohello 대상 합니다. |

#### <a name="example"></a>예제

```json
{
    "name": "AzureTableInput",
    "properties": {
        "type": "AzureTable",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

이러한 연결된 서비스에 대한 자세한 내용은 [Azure Table Storage 커넥터](data-factory-azure-table-connector.md#dataset-properties) 문서를 참조하세요. 

### <a name="azure-table-source-in-copy-activity"></a>복사 활동의 Azure Table 소스
Azure 테이블 저장소에서 데이터를 복사 하는 경우 설정 hello **소스 형식** hello의 복사 작업이 너무**AzureTableSource**, 다음 hello에 대 한 속성을 지정 하 고 **소스**섹션:

| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| AzureTableSourceQuery |사용자 지정 쿼리 tooread 데이터 hello를 사용 합니다. |Azure 테이블 쿼리 문자열. Hello 다음 섹션의 예제를 참조 하십시오. |아니요. 를 azureTableSourceQuery 없이 tableName을 지정 하는 경우 hello 테이블의 모든 레코드가 복사한 toohello 대상 됩니다. Hello 쿼리를 충족 하는 hello 테이블에서 레코드는 azureTableSourceQuery도 지정 되어 경우 복사한 toohello 대상 합니다. |
| azureTableSourceIgnoreTableNotFound |테이블의 hello 예외를 무시할지 존재 하지 여부를 나타냅니다. |TRUE<br/>FALSE |아니요 |

#### <a name="example"></a>예제

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureTabletoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureTableInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "AzureTableSource",
                    "AzureTableSourceQuery": "PartitionKey eq 'DefaultPartitionKey'"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

이러한 연결된 서비스에 대한 자세한 내용은 [Azure Table Storage 커넥터](data-factory-azure-table-connector.md#copy-activity-properties) 문서를 참조하세요. 

### <a name="azure-table-sink-in-copy-activity"></a>복사 활동의 Azure Table 싱크
데이터 tooAzure 테이블 저장소를 복사 하는 경우 설정 hello **싱크 유형** hello의 복사 작업이 너무**AzureTableSink**, 다음 hello에 대 한 속성을 지정 하 고 **싱크** 섹션 내용

| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| azureTableDefaultPartitionKeyValue |기본 파티션 키 값 hello 싱크에서 사용할 수 있는 합니다. |문자열 값 |아니요 |
| azureTablePartitionKeyName |해당 값은 파티션 키로 사용 하는 hello 열의 이름을 지정 합니다. 지정 하지 않으면 AzureTableDefaultPartitionKeyValue hello 파티션 키로 사용 됩니다. |열 이름 |아니요 |
| azureTableRowKeyName |해당 열 값은 행 키로 사용 되는 hello 열의 이름을 지정 합니다. 지정하지 않으면 각 행에 GUID를 사용합니다. |열 이름 |아니요 |
| azureTableInsertType |Azure 테이블에 hello 모드 tooinsert 데이터입니다.<br/><br/>이 속성은 파티션 및 행 키 일치 하는 hello 출력 테이블의 기존 행에는 값을 바꾸거나 병합 있는지 여부를 제어 합니다. <br/><br/>이러한 설정을 (병합 및 대체) 작동 방법에 대해 toolearn 참조 [삽입 또는 병합 엔터티](https://msdn.microsoft.com/library/azure/hh452241.aspx) 및 [삽입 또는 교체 엔터티](https://msdn.microsoft.com/library/azure/hh452242.aspx) 항목. <br/><br> 두 옵션 모두 hello 입력에 존재 하지 않는 hello 출력 테이블에 행을 삭제 및 hello 테이블 수준이 아닌 hello 행 수준에서이 설정을 적용 됩니다. |병합(기본값)<br/>바꾸기 |아니요 |
| writeBatchSize |Hello writeBatchSize 또는 writebatchtimeout에 도달 하는 경우에 hello Azure 테이블에 데이터를 삽입 합니다. |정수(행 수) |아니요(기본값: 10000) |
| writeBatchTimeout |Hello writeBatchSize 또는 writebatchtimeout에 도달 하는 경우 hello Azure 테이블에 데이터 삽입 |timespan<br/><br/>예: "00:20:00"(20분) |더 (기본 toostorage 클라이언트 기본 제한 시간 값인 90 초) |

#### <a name="example"></a>예제

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoTable",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureTableOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "AzureTableSink",
                    "writeBatchSize": 100,
                    "writeBatchTimeout": "01:00:00"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
이러한 연결된 서비스에 대한 자세한 내용은 [Azure Table Storage 커넥터](data-factory-azure-table-connector.md#copy-activity-properties) 문서를 참조하세요. 

## <a name="amazon-redshift"></a>Amazon RedShift

### <a name="linked-service"></a>연결된 서비스
연결 된 서비스를 집합 hello toodefine Amazon Redshift **형식** hello 연결 서비스 너무**AmazonRedshift**, 다음 hello에 대 한 속성을 지정 하 고 **typeProperties**섹션:  

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| server |Hello Amazon Redshift 서버의 IP 주소 또는 호스트 이름입니다. |예 |
| 포트 |Amazon Redshift 서버 hello hello TCP 포트 수가 hello toolisten를 사용 하 여 클라이언트 연결에 대 한 합니다. |기본값이 없음: 5439 |
| database |Hello Amazon Redshift 데이터베이스의 이름입니다. |예 |
| username |Access toohello 데이터베이스를 갖고 있는 사용자의 이름입니다. |예 |
| 암호 |Hello 사용자 계정의 암호입니다. |예 |

#### <a name="example"></a>예제

```json
{
    "name": "AmazonRedshiftLinkedService",
    "properties": {
        "type": "AmazonRedshift",
        "typeProperties": {
            "server": "<Amazon Redshift host name or IP address>",
            "port": 5439,
            "database": "<database name>",
            "username": "user",
            "password": "password"
        }
    }
}
```

자세한 내용은 [Amazon Redshift 커넥터](#data-factory-amazon-redshift-connector.md#linked-service-properties) 문서를 참조 하세요. 

### <a name="dataset"></a>데이터 집합
Amazon Redshift 데이터 집합, toodefine 집합 hello **형식** hello 데이터 집합의 너무**RelationalTable**, hello 다음과 같은 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션 내용 

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| tableName |연결 된 서비스는 hello Amazon Redshift 데이터베이스에 대 한 hello 테이블의 이름은 참조 합니다. |아니요(**RelationalSource**의 **쿼리**가 지정된 경우) |


#### <a name="example"></a>예제

```json
{
    "name": "AmazonRedshiftInputDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "AmazonRedshiftLinkedService",
        "typeProperties": {
            "tableName": "<Table name>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
자세한 내용은 [Amazon Redshift 커넥터](#data-factory-amazon-redshift-connector.md#dataset-properties) 문서를 참조 하세요.

### <a name="relational-source-in-copy-activity"></a>복사 활동의 Relational 소스 
Amazon Redshift에서 데이터를 복사 하는 경우 설정 hello **소스 형식** hello의 복사 작업이 너무**RelationalSource**, 다음 hello에 대 한 속성을 지정 하 고 **소스** 섹션 내용

| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| 쿼리 |사용자 지정 쿼리 tooread 데이터 hello를 사용 합니다. |SQL 쿼리 문자열. 예: `select * from MyTable` |아니요(**데이터 집합**의 **tableName**이 지정된 경우) |

#### <a name="example"></a>예제

```json
{
    "name": "CopyAmazonRedshiftToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "AmazonRedshiftInputDataset"
            }],
            "outputs": [{
                "name": "AzureBlobOutputDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "AmazonRedshiftToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```
자세한 내용은 [Amazon Redshift 커넥터](#data-factory-amazon-redshift-connector.md#copy-activity-properties) 문서를 참조 하세요.

## <a name="ibm-db2"></a>IBM DB2

### <a name="linked-service"></a>연결된 서비스
연결 된 서비스를 집합 hello toodefine IBM DB2 **형식** hello 연결 서비스 너무**OnPremisesDB2**, 다음 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션:  

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| server |Hello DB2 서버의 이름입니다. |예 |
| database |Hello DB2 데이터베이스의 이름입니다. |예 |
| schema |Hello hello 데이터베이스 스키마의 이름입니다. hello 스키마 이름이 대/소문자 구분 합니다. |아니요 |
| authenticationType |Tooconnect toohello DB2 데이터베이스를 사용 하는 인증 유형입니다. 가능한 값은 익명, 기본 및 Windows입니다. |예 |
| username |기본 또는 Windows 인증을 사용하는 경우 사용자 이름을 지정합니다. |아니요 |
| 암호 |Hello 사용자 이름에 대해 지정한 사용자 계정에 hello에 대 한 암호를 지정 합니다. |아니요 |
| gatewayName |데이터 팩터리 서비스 hello hello 게이트웨이의 이름 tooconnect toohello 온-프레미스 DB2 데이터베이스를 사용 해야 합니다. |예 |

#### <a name="example"></a>예제
```json
{
    "name": "OnPremDb2LinkedService",
    "properties": {
        "type": "OnPremisesDb2",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```
자세한 내용은 [IBM DB2 커넥터](#data-factory-onprem-db2-connector.md#linked-service-properties) 문서를 참조하세요.

### <a name="dataset"></a>데이터 집합
toodefine DB2 데이터 집합, 집합 hello **형식** hello 데이터 집합의 너무**RelationalTable**, hello 다음과 같은 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션:

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| tableName |연결 된 서비스는 hello DB2 데이터베이스 인스턴스의 hello 테이블의 이름은 참조 합니다. hello tableName은 대/소문자 구분 합니다. |아니요(**RelationalSource**의 **쿼리**가 지정된 경우) 

#### <a name="example"></a>예제
```json
{
    "name": "Db2DataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremDb2LinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

자세한 내용은 [IBM DB2 커넥터](#data-factory-onprem-db2-connector.md#dataset-properties) 문서를 참조하세요.

### <a name="relational-source-in-copy-activity"></a>복사 활동의 Relational 소스
IBM d b 2에서 데이터를 복사 하는 경우 설정 hello **소스 형식** hello의 복사 작업이 너무**RelationalSource**, 다음 hello에 대 한 속성을 지정 하 고 **소스** 섹션:


| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| 쿼리 |사용자 지정 쿼리 tooread 데이터 hello를 사용 합니다. |SQL 쿼리 문자열. 예: `"query": "select * from "MySchema"."MyTable""` |아니요(**데이터 집합**의 **tableName**이 지정된 경우) |

#### <a name="example"></a>예제
```json
{
    "name": "CopyDb2ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "select * from \"Orders\""
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "inputs": [{
                "name": "Db2DataSet"
            }],
            "outputs": [{
                "name": "AzureBlobDb2DataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "Db2ToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```
자세한 내용은 [IBM DB2 커넥터](#data-factory-onprem-db2-connector.md#copy-activity-properties) 문서를 참조하세요.

## <a name="mysql"></a>MySQL

### <a name="linked-service"></a>연결된 서비스
연결 된 서비스를 집합 hello toodefine MySQL **형식** hello 연결 서비스 너무**OnPremisesMySql**, 다음 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션:  

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| server |Hello MySQL 서버의 이름입니다. |예 |
| database |Hello MySQL 데이터베이스의 이름입니다. |예 |
| schema |Hello hello 데이터베이스 스키마의 이름입니다. |아니요 |
| authenticationType |Tooconnect toohello MySQL 데이터베이스를 사용 하는 인증 유형입니다. 가능한 값은 `Basic`입니다. |예 |
| username |사용자 이름 tooconnect toohello MySQL 데이터베이스를 지정 합니다. |예 |
| 암호 |지정한 hello 사용자 계정에 대 한 암호를 지정 합니다. |예 |
| gatewayName |데이터 팩터리 서비스 hello hello 게이트웨이의 이름 tooconnect toohello 온-프레미스 MySQL 데이터베이스를 사용 해야 합니다. |예 |

#### <a name="example"></a>예제

```json
{
    "name": "OnPremMySqlLinkedService",
    "properties": {
        "type": "OnPremisesMySql",
        "typeProperties": {
            "server": "<server name>",
            "database": "<database name>",
            "schema": "<schema name>",
            "authenticationType": "<authentication type>",
            "userName": "<user name>",
            "password": "<password>",
            "gatewayName": "<gateway>"
        }
    }
}
```

자세한 내용은 [MySQL 커넥터](data-factory-onprem-mysql-connector.md#linked-service-properties) 문서를 참조하세요. 

### <a name="dataset"></a>데이터 집합
toodefine MySQL dataset 집합 hello **형식** hello 데이터 집합의 너무**RelationalTable**, hello 다음과 같은 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션: 

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| tableName |MySQL 데이터베이스 인스턴스에 연결 된 서비스를 가리키는 hello에 hello 테이블의 이름입니다. |아니요(**RelationalSource**의 **쿼리**가 지정된 경우) |

#### <a name="example"></a>예제

```json
{
    "name": "MySqlDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremMySqlLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
자세한 내용은 [MySQL 커넥터](data-factory-onprem-mysql-connector.md#dataset-properties) 문서를 참조하세요. 

### <a name="relational-source-in-copy-activity"></a>복사 활동의 Relational 소스
MySQL 데이터베이스에서 데이터를 복사 하는 경우 설정 hello **소스 형식** hello의 복사 작업이 너무**RelationalSource**, 다음 hello에 대 한 속성을 지정 하 고 **소스** 섹션 내용


| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| 쿼리 |사용자 지정 쿼리 tooread 데이터 hello를 사용 합니다. |SQL 쿼리 문자열. 예: `select * from MyTable` |아니요(**데이터 집합**의 **tableName**이 지정된 경우) |


#### <a name="example"></a>예제
```json
{
    "name": "CopyMySqlToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "MySqlDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobMySqlDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "MySqlToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

자세한 내용은 [MySQL 커넥터](data-factory-onprem-mysql-connector.md#copy-activity-properties) 문서를 참조하세요. 

## <a name="oracle"></a>Oracle 

### <a name="linked-service"></a>연결된 서비스
연결 된 서비스를 집합 hello toodefine Oracle **형식** hello 연결 서비스 너무**OnPremisesOracle**, 다음 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션 내용  

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| driverType | 드라이버 toouse toocopy 데이터 지정 / tooOracle 데이터베이스입니다. 허용되는 값은 **Microsoft** 또는 **ODP**(기본값)입니다. 드라이버 세부 정보에 대해서는 [지원되는 버전 및 설치](#supported-versions-and-installation) 섹션을 참조하세요. | 아니요 |
| connectionString | Hello connectionString 속성에 대 한 tooconnect toohello Oracle 데이터베이스 인스턴스는 데 필요한 정보를 지정 합니다. | 예 |
| gatewayName | 사용 하는 tooconnect toohello 온-프레미스 Oracle 서버 hello 게이트웨이의 이름 |예 |

#### <a name="example"></a>예제
```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "driverType": "Microsoft",
            "connectionString": "Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

자세한 내용은 [Oracle 커넥터](data-factory-onprem-oracle-connector.md#linked-service-properties) 문서를 참조하세요.

### <a name="dataset"></a>데이터 집합
Oracle 데이터 집합, toodefine 집합 hello **형식** hello 데이터 집합의 너무**OracleTable**, hello 다음과 같은 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션: 

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| tableName |Oracle 데이터베이스를 연결 된 서비스 hello hello에 hello 테이블의 이름은 참조 합니다. |아니요(**OracleSource**의 **oracleReaderQuery**가 지정된 경우) |

#### <a name="example"></a>예제

```json
{
    "name": "OracleInput",
    "properties": {
        "type": "OracleTable",
        "linkedServiceName": "OnPremisesOracleLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "offset": "01:00:00",
            "interval": "1",
            "anchorDateTime": "2016-02-27T12:00:00",
            "frequency": "Hour"
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
자세한 내용은 [Oracle 커넥터](data-factory-onprem-oracle-connector.md#dataset-properties) 문서를 참조하세요.

### <a name="oracle-source-in-copy-activity"></a>복사 활동의 Oracle 소스
Oracle 데이터베이스에서 데이터를 복사 하는 경우 설정 hello **소스 형식** hello의 복사 작업이 너무**OracleSource**, 다음 hello에 대 한 속성을 지정 하 고 **소스** 섹션 내용

| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| oracleReaderQuery |사용자 지정 쿼리 tooread 데이터 hello를 사용 합니다. |SQL 쿼리 문자열. 예: `select * from MyTable` <br/><br/>지정 하지 않으면 실행 되는 SQL 문을 hello:`select * from MyTable` |아니요(**데이터 집합**의 **tableName**이 지정된 경우) |

#### <a name="example"></a>예제

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "OracletoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": " OracleInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "OracleSource",
                    "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
            "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

자세한 내용은 [Oracle 커넥터](data-factory-onprem-oracle-connector.md#copy-activity-properties) 문서를 참조하세요.

### <a name="oracle-sink-in-copy-activity"></a>복사 활동의 Oracle 싱크
데이터 tooam Oracle 데이터베이스를 복사 하는 경우 설정 hello **싱크 유형** hello의 복사 작업이 너무**OracleSink**, 다음 hello에 대 한 속성을 지정 하 고 **싱크** 섹션:

| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| writeBatchTimeout |대기 시간이 초과 되기 전에 일괄 처리 삽입 작업 toocomplete hello에 대 한 시간입니다. |timespan<br/><br/> 예: “00:30:00”(30분). |아니요 |
| writeBatchSize |WriteBatchSize hello 버퍼 크기에 이르면 hello SQL 테이블에 데이터를 삽입 합니다. |정수(행 수) |아니요(기본값: 100) |
| sqlWriterCleanupScript |특정 조각의 데이터 정리 되도록 tooexecute 복사 작업에 대 한 쿼리를 지정 합니다. |쿼리 문입니다. |아니요 |
| sliceIdentifierColumnName |특정 조각 다시 실행 시점의 데이터를 사용 하는 tooclean 변수인 자동 생성 된 조각 식별자를 가진 toofill 복사 작업에 대 한 열 이름을 지정 합니다. |이진(32) 데이터 형식이 있는 열의 열 이름입니다. |아니요 |

#### <a name="example"></a>예제
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-05T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoOracle",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "OracleOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "OracleSink"
                }
            },
            "scheduler": {
                "frequency": "Day",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
자세한 내용은 [Oracle 커넥터](data-factory-onprem-oracle-connector.md#copy-activity-properties) 문서를 참조하세요.

## <a name="postgresql"></a>PostgreSQL

### <a name="linked-service"></a>연결된 서비스
연결 된 서비스를 집합 hello toodefine는 PostgreSQL **형식** hello 연결 서비스 너무**OnPremisesPostgreSql**, 다음 hello에 대 한 속성을 지정 하 고 **typeProperties**섹션:  

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| server |Hello PostgreSQL 서버의 이름입니다. |예 |
| database |Hello PostgreSQL 데이터베이스의 이름입니다. |예 |
| schema |Hello hello 데이터베이스 스키마의 이름입니다. hello 스키마 이름이 대/소문자 구분 합니다. |아니요 |
| authenticationType |Tooconnect toohello PostgreSQL 데이터베이스를 사용 하는 인증 유형입니다. 가능한 값은 익명, 기본 및 Windows입니다. |예 |
| username |기본 또는 Windows 인증을 사용하는 경우 사용자 이름을 지정합니다. |아니요 |
| 암호 |Hello 사용자 이름에 대해 지정한 사용자 계정에 hello에 대 한 암호를 지정 합니다. |아니요 |
| gatewayName |데이터 팩터리 서비스 hello hello 게이트웨이의 이름 tooconnect toohello 온-프레미스 PostgreSQL 데이터베이스를 사용 해야 합니다. |예 |

#### <a name="example"></a>예제

```json
{
    "name": "OnPremPostgreSqlLinkedService",
    "properties": {
        "type": "OnPremisesPostgreSql",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```
자세한 내용은 [PostgreSQL 커넥터](data-factory-onprem-postgresql-connector.md#linked-service-properties) 문서를 참조하세요.

### <a name="dataset"></a>데이터 집합
toodefine PostgreSQL dataset 집합 hello **형식** hello 데이터 집합의 너무**RelationalTable**, hello 다음과 같은 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션: 

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| tableName |PostgreSQL 데이터베이스 인스턴스에 연결 된 서비스를 가리키는 hello에 hello 테이블의 이름입니다. hello tableName은 대/소문자 구분 합니다. |아니요(**RelationalSource**의 **쿼리**가 지정된 경우) |

#### <a name="example"></a>예제
```json
{
    "name": "PostgreSqlDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremPostgreSqlLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
자세한 내용은 [PostgreSQL 커넥터](data-factory-onprem-postgresql-connector.md#dataset-properties) 문서를 참조하세요.

### <a name="relational-source-in-copy-activity"></a>복사 활동의 Relational 소스
PostgreSQL 데이터베이스에서 데이터를 복사 하는 경우 설정 hello **소스 형식** hello의 복사 작업이 너무**RelationalSource**, 다음 hello에 대 한 속성을 지정 하 고 **소스**섹션:


| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| 쿼리 |사용자 지정 쿼리 tooread 데이터 hello를 사용 합니다. |SQL 쿼리 문자열. 예: "query": "select * from \"MySchema\".\"MyTable\"". |아니요(**데이터 집합**의 **tableName**이 지정된 경우) |

#### <a name="example"></a>예제

```json
{
    "name": "CopyPostgreSqlToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "select * from \"public\".\"usstates\""
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "inputs": [{
                "name": "PostgreSqlDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobPostgreSqlDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "PostgreSqlToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

자세한 내용은 [PostgreSQL 커넥터](data-factory-onprem-postgresql-connector.md#copy-activity-properties) 문서를 참조하세요.

## <a name="sap-business-warehouse"></a>SAP Business Warehouse


### <a name="linked-service"></a>연결된 서비스
연결 된 서비스를 집합 hello toodefine SAP 비즈니스 웨어하우스 (BW) **형식** hello 연결 서비스 너무**SapBw**, 다음 hello에 대 한 속성을 지정 하 고 **typeProperties**섹션:  

속성 | 설명 | 허용되는 값 | 필수
-------- | ----------- | -------------- | --------
server | SAP BW는 hello에 인스턴스가 있는 hello 서버의 이름입니다. | string | 예
systemNumber | Hello SAP BW 시스템의 시스템 번호입니다. | 문자열로 표현되는 두 자리 10진수. | 예
clientId | 클라이언트 hello W SAP 시스템에서에서 hello 클라이언트의 ID입니다. | 문자열로 표현되는 세 자리 10진수. | 예
username | Toohello SAP 서버 액세스를 갖고 있는 hello 사용자의 이름 | string | 예
암호 | Hello 사용자 암호입니다. | string | 예
gatewayName | 데이터 팩터리 서비스 hello hello 게이트웨이의 이름 tooconnect toohello 온-프레미스 SAP BW 인스턴스를 사용 해야 합니다. | string | 예
encryptedCredential | hello 암호화 된 자격 증명 문자열입니다. | string | 아니요

#### <a name="example"></a>예제

```json
{
    "name": "SapBwLinkedService",
    "properties": {
        "type": "SapBw",
        "typeProperties": {
            "server": "<server name>",
            "systemNumber": "<system number>",
            "clientId": "<client id>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

자세한 내용은 [SAP Business Warehouse 커넥터](data-factory-sap-business-warehouse-connector.md#linked-service-properties) 문서를 참조하세요. 

### <a name="dataset"></a>데이터 집합
SAP BW 데이터 집합, toodefine 집합 hello **형식** hello 데이터 집합의 너무**RelationalTable**합니다. 형식의 hello SAP BW 데이터 집합에 대 한 지원 유형별 속성이 없는 **RelationalTable**합니다.  

#### <a name="example"></a>예제

```json
{
    "name": "SapBwDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapBwLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
자세한 내용은 [SAP Business Warehouse 커넥터](data-factory-sap-business-warehouse-connector.md#dataset-properties) 문서를 참조하세요. 

### <a name="relational-source-in-copy-activity"></a>복사 활동의 Relational 소스
SAP Business Warehouse에서 데이터를 복사 하는 경우 설정 hello **소스 형식** hello의 복사 작업이 너무**RelationalSource**, 다음 hello에 대 한 속성을 지정 하 고 **소스**섹션:


| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| 쿼리 | Hello hello SAP BW 인스턴스에서 MDX 쿼리 tooread 데이터를 지정합니다. | MDX 쿼리. | 예 |

#### <a name="example"></a>예제

```json
{
    "name": "CopySapBwToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "<MDX query for SAP BW>"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "SapBwDataset"
            }],
            "outputs": [{
                "name": "AzureBlobDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "SapBwToBlob"
        }],
        "start": "2017-03-01T18:00:00",
        "end": "2017-03-01T19:00:00"
    }
}
```

자세한 내용은 [SAP Business Warehouse 커넥터](data-factory-sap-business-warehouse-connector.md#copy-activity-properties) 문서를 참조하세요. 

## <a name="sap-hana"></a>SAP HANA

### <a name="linked-service"></a>연결된 서비스
연결 된 서비스를 집합 hello toodefine SAP HANA **형식** hello 연결 서비스 너무**SapHana**, 다음 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션:  

속성 | 설명 | 허용되는 값 | 필수
-------- | ----------- | -------------- | --------
server | SAP HANA는 hello에 인스턴스가 있는 hello 서버의 이름입니다. 서버에서 사용자 지정된 포트를 사용하는 경우 `server:port`를 지정합니다. | string | 예
authenticationType | 인증 유형입니다. | string. "Basic" 또는 "Windows" | 예 
username | Toohello SAP 서버 액세스를 갖고 있는 hello 사용자의 이름 | string | 예
암호 | Hello 사용자 암호입니다. | string | 예
gatewayName | 데이터 팩터리 서비스 hello hello 게이트웨이의 이름 tooconnect toohello 온-프레미스 SAP HANA 인스턴스를 사용 해야 합니다. | string | 예
encryptedCredential | hello 암호화 된 자격 증명 문자열입니다. | string | 아니요

#### <a name="example"></a>예제

```json
{
    "name": "SapHanaLinkedService",
    "properties": {
        "type": "SapHana",
        "typeProperties": {
            "server": "<server name>",
            "authenticationType": "<Basic, or Windows>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}

```
자세한 내용은 [SAP HANA 커넥터](data-factory-sap-hana-connector.md#linked-service-properties) 문서를 참조하세요.
 
### <a name="dataset"></a>데이터 집합
SAP HANA 데이터 집합, toodefine 집합 hello **형식** hello 데이터 집합의 너무**RelationalTable**합니다. 형식의 hello SAP HANA 데이터 집합에 대 한 지원 유형별 속성이 없는 **RelationalTable**합니다. 

#### <a name="example"></a>예제

```json
{
    "name": "SapHanaDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapHanaLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
자세한 내용은 [SAP HANA 커넥터](data-factory-sap-hana-connector.md#dataset-properties) 문서를 참조하세요. 

### <a name="relational-source-in-copy-activity"></a>복사 활동의 Relational 소스
SAP HANA 데이터 저장소에서 데이터를 복사 하는 경우 설정 hello **소스 형식** hello의 복사 작업이 너무**RelationalSource**, 다음 hello에 대 한 속성을 지정 하 고 **소스**섹션:

| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| 쿼리 | Hello SAP HANA 인스턴스에서 hello SQL 쿼리 tooread 데이터를 지정합니다. | SQL 쿼리. | 예 |


#### <a name="example"></a>예제


```json
{
    "name": "CopySapHanaToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "<SQL Query for HANA>"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "SapHanaDataset"
            }],
            "outputs": [{
                "name": "AzureBlobDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "SapHanaToBlob"
        }],
        "start": "2017-03-01T18:00:00",
        "end": "2017-03-01T19:00:00"
    }
}
```

자세한 내용은 [SAP HANA 커넥터](data-factory-sap-hana-connector.md#copy-activity-properties) 문서를 참조하세요.


## <a name="sql-server"></a>SQL Server

### <a name="linked-service"></a>연결된 서비스
형식의 연결 된 서비스를 만들면 **OnPremisesSqlServer** toolink 온-프레미스 SQL Server 데이터베이스 tooa 데이터 팩터리입니다. 다음 표에서 hello JSON 요소 특정 tooon 온-프레미스 SQL Server 연결 된 서비스에 대 한 설명을 제공 합니다.

다음 표에서 hello JSON 요소 특정 tooSQL 연결 된 서버 서비스에 대 한 설명을 제공 합니다.

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| type |hello type 속성이로 설정 해야: **OnPremisesSqlServer**합니다. |예 |
| connectionString |SQL 인증 또는 Windows 인증을 사용 하 여 tooconnect toohello 온-프레미스 SQL Server 데이터베이스는 데 필요한 connectionString 정보를 지정 합니다. |예 |
| gatewayName |데이터 팩터리 서비스 hello hello 게이트웨이의 이름 tooconnect toohello 온-프레미스 SQL Server 데이터베이스를 사용 해야 합니다. |예 |
| username |Windows 인증을 사용하는 경우 사용자 이름을 지정합니다. 예: **domainname\\username**. |아니요 |
| 암호 |Hello 사용자 이름에 대해 지정한 사용자 계정에 hello에 대 한 암호를 지정 합니다. |아니요 |

Hello를 사용 하 여 자격 증명을 암호화할 수 **새로 AzureRmDataFactoryEncryptValue** cmdlet hello 다음 예제와 같이 hello 연결 문자열에서 사용 하 고 (**EncryptedCredential** 속성):  

```json
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```


#### <a name="example-json-for-using-sql-authentication"></a>예제: SQL 인증을 사용하는 JSON

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
#### <a name="example-json-for-using-windows-authentication"></a>예제: Windows 인증을 사용하는 JSON

사용자 이름 및 암호를 지정 하는 경우 게이트웨이에서 사용 하 여 해당 tooimpersonate hello 지정 된 사용자 계정 tooconnect toohello 온-프레미스 SQL Server 데이터베이스입니다. 그렇지 않은 경우 게이트웨이 게이트웨이 (시작 계정)의 보안 컨텍스트 hello와 직접 toohello SQL Server를 연결합니다.

```json
{
    "Name": " MyOnPremisesSQLDB",
    "Properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "ConnectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=True;",
            "username": "<domain\\username>",
            "password": "<password>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

자세한 내용은 [SQL Server 커넥터](data-factory-sqlserver-connector.md#linked-service-properties) 문서를 참조하세요. 

### <a name="dataset"></a>데이터 집합
SQL Server 데이터 집합, toodefine 집합 hello **형식** hello 데이터 집합의 너무**SqlServerTable**, hello 다음과 같은 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션: 

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| tableName |Hello 테이블 또는 뷰의 연결 된 서비스는 hello SQL Server 데이터베이스 인스턴스의 이름이 참조 합니다. |예 |

#### <a name="example"></a>예제
```json
{
    "name": "SqlServerInput",
    "properties": {
        "type": "SqlServerTable",
        "linkedServiceName": "SqlServerLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

자세한 내용은 [SQL Server 커넥터](data-factory-sqlserver-connector.md#dataset-properties) 문서를 참조하세요. 

### <a name="sql-source-in-copy-activity"></a>복사 활동의 SQL 소스
SQL Server 데이터베이스에서 데이터를 복사 하는 경우 설정 hello **소스 형식** hello의 복사 작업이 너무**SqlSource**, 다음 hello에 대 한 속성을 지정 하 고 **소스** 섹션 내용


| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| SqlReaderQuery |사용자 지정 쿼리 tooread 데이터 hello를 사용 합니다. |SQL 쿼리 문자열. 예: `select * from MyTable` Hello 입력된 데이터 집합에서 참조 하는 hello 데이터베이스에서 여러 테이블을 참조할 수 있습니다. 지정 하지 않으면 실행 되는 SQL 문을 hello: MyTable 중에서 선택 합니다. |아니요 |
| sqlReaderStoredProcedureName |Hello 원본 테이블에서 데이터를 읽을 수 있는 프로시저를 저장 하는 hello의 이름입니다. |저장 프로시저를 hello의 이름입니다. |아니요 |
| storedProcedureParameters |Hello에 대 한 매개 변수 저장 프로시저입니다. |이름/값 쌍입니다. Hello 이름과 대/소문자 hello 저장 프로시저 매개 변수의 이름 및 매개 변수는 대/소문자 구분 일치 해야 합니다. |아니요 |

경우 hello **sqlReaderQuery** 에 대해 지정 된 hello SqlSource, hello 복사 활동 hello SQL Server 데이터베이스 원본 tooget hello 데이터에 대해이 쿼리를 실행 합니다.

또는 hello를 지정 하 여 저장된 프로시저를 지정할 수 있습니다 **sqlReaderStoredProcedureName** 및 **storedProcedureParameters** (경우 hello 저장된 프로시저 매개 변수를 사용).

Hello 구조 섹션에 정의 된 hello 열 sqlReaderQuery 또는 sqlReaderStoredProcedureName 중 하나를 지정 하지 않으면 경우 사용 되는 toobuild hello SQL Server 데이터베이스에 대해 선택 쿼리 toorun 합니다. 데이터 집합 정의 hello hello 구조 없으면 hello 테이블에서 모든 열을 선택 합니다.

> [!NOTE]
> 사용 하는 경우 **sqlReaderStoredProcedureName**, hello에 대 한 값을 toospecify 보내야 **tableName** hello 데이터 집합 JSON의에서 속성입니다. 그러나 이 테이블에 대해 수행되는 유효성 검사는 없습니다.


#### <a name="example"></a>예제
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "SqlServertoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": " SqlServerInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

이 예제에서는 **sqlReaderQuery** SqlSource hello에 대 한 지정 합니다. 복사 활동 hello hello SQL Server 데이터베이스 원본 tooget hello 데이터에 대해이 쿼리를 실행합니다. 또는 hello를 지정 하 여 저장된 프로시저를 지정할 수 있습니다 **sqlReaderStoredProcedureName** 및 **storedProcedureParameters** (경우 hello 저장된 프로시저 매개 변수를 사용). hello sqlReaderQuery hello 입력된 데이터 집합에서 참조 하는 hello 데이터베이스 내에서 여러 테이블을 참조할 수 있습니다. 데이터 집합의 tableName typeProperty hello으로 설정 하는 제한 된 tooonly hello 테이블이 아닙니다.

Hello 구조 섹션에 정의 된 hello 열 sqlReaderQuery 또는 sqlReaderStoredProcedureName를 지정 하지 않으면 경우 사용 되는 toobuild hello SQL Server 데이터베이스에 대해 선택 쿼리 toorun 합니다. 데이터 집합 정의 hello hello 구조 없으면 hello 테이블에서 모든 열을 선택 합니다.

자세한 내용은 [SQL Server 커넥터](data-factory-sqlserver-connector.md#copy-activity-properties) 문서를 참조하세요. 

### <a name="sql-sink-in-copy-activity"></a>복사 활동의 SQL 싱크
데이터 tooa SQL Server 데이터베이스를 복사 하는 경우 설정 hello **싱크 유형** hello의 복사 작업이 너무**SqlSink**, 다음 hello에 대 한 속성을 지정 하 고 **싱크** 섹션:

| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| writeBatchTimeout |대기 시간이 초과 되기 전에 일괄 처리 삽입 작업 toocomplete hello에 대 한 시간입니다. |timespan<br/><br/> 예: “00:30:00”(30분). |아니요 |
| writeBatchSize |WriteBatchSize hello 버퍼 크기에 이르면 hello SQL 테이블에 데이터를 삽입 합니다. |정수(행 수) |아니요(기본값: 10000) |
| sqlWriterCleanupScript |특정 조각의 데이터 정리 되도록 tooexecute 복사 작업에 대 한 쿼리를 지정 합니다. 자세한 내용은 [반복성](#repeatability-during-copy) 섹션을 참조하세요. |쿼리 문입니다. |아니요 |
| sliceIdentifierColumnName |특정 조각 다시 실행 시점의 데이터를 사용 하는 tooclean 변수인 자동 생성 된 조각 식별자를 가진 toofill 복사 작업에 대 한 열 이름을 지정 합니다. 자세한 내용은 [반복성](#repeatability-during-copy) 섹션을 참조하세요. |이진(32) 데이터 형식이 있는 열의 열 이름입니다. |아니요 |
| sqlWriterStoredProcedureName |Hello 저장 프로시저의 이름 (업데이트/삽입) upserts 데이터 hello 대상 테이블에 있습니다. |저장 프로시저를 hello의 이름입니다. |아니요 |
| storedProcedureParameters |Hello에 대 한 매개 변수 저장 프로시저입니다. |이름/값 쌍입니다. Hello 이름과 대/소문자 hello 저장 프로시저 매개 변수의 이름 및 매개 변수는 대/소문자 구분 일치 해야 합니다. |아니요 |
| sqlWriterTableType |테이블 형식 이름 toobe hello 저장 프로시저에 사용을 지정 합니다. 복사 활동 임시 테이블과이 테이블 형식으로 사용할 수 있는 이동 된 hello 데이터를 만듭니다. 저장된 프로시저 코드 hello 데이터를 기존 데이터와 복사를 병합할 수 있습니다. |테이블 유형 이름 |아니요 |

#### <a name="example"></a>예제
복사 작업을 포함 하는 hello 파이프라인 구성된 toouse 이러한 입력 및 출력 데이터 집합은 하 고 예약 된 toorun 1 시간입니다. Hello 파이프라인 JSON 정의에서 hello **소스** 형식이 너무 설정**BlobSource** 및 **싱크** 형식이 너무 설정**SqlSink**합니다.

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQL",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": " SqlServerOutput "
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource",
                    "blobColumnSeparators": ","
                },
                "sink": {
                    "type": "SqlSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

자세한 내용은 [SQL Server 커넥터](data-factory-sqlserver-connector.md#copy-activity-properties) 문서를 참조하세요. 

## <a name="sybase"></a>Sybase

### <a name="linked-service"></a>연결된 서비스
연결 된 서비스를 집합 hello toodefine는 Sybase **형식** hello 연결 서비스 너무**OnPremisesSybase**, 다음 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션 내용  

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| server |Hello Sybase 서버의 이름입니다. |예 |
| database |Hello Sybase 데이터베이스의 이름입니다. |예 |
| schema |Hello hello 데이터베이스 스키마의 이름입니다. |아니요 |
| authenticationType |Tooconnect toohello Sybase 데이터베이스를 사용 하는 인증 유형입니다. 가능한 값은 익명, 기본 및 Windows입니다. |예 |
| username |기본 또는 Windows 인증을 사용하는 경우 사용자 이름을 지정합니다. |아니요 |
| 암호 |Hello 사용자 이름에 대해 지정한 사용자 계정에 hello에 대 한 암호를 지정 합니다. |아니요 |
| gatewayName |데이터 팩터리 서비스 hello hello 게이트웨이의 이름 tooconnect toohello 온-프레미스 Sybase 데이터베이스를 사용 해야 합니다. |예 |

#### <a name="example"></a>예제
```json
{
    "name": "OnPremSybaseLinkedService",
    "properties": {
        "type": "OnPremisesSybase",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

자세한 내용은 [Sybase 커넥터](data-factory-onprem-sybase-connector.md#linked-service-properties) 문서를 참조하세요. 

### <a name="dataset"></a>데이터 집합
toodefine Sybase dataset 집합 hello **형식** hello 데이터 집합의 너무**RelationalTable**, hello 다음과 같은 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션: 

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| tableName |Sybase 데이터베이스 인스턴스에 연결 된 서비스를 가리키는 hello에 hello 테이블의 이름입니다. |아니요(**RelationalSource**의 **쿼리**가 지정된 경우) |

#### <a name="example"></a>예제

```json
{
    "name": "SybaseDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremSybaseLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

자세한 내용은 [Sybase 커넥터](data-factory-onprem-sybase-connector.md#dataset-properties) 문서를 참조하세요. 

### <a name="relational-source-in-copy-activity"></a>복사 활동의 Relational 소스
Sybase 데이터베이스에서 데이터를 복사 하는 경우 설정 hello **소스 형식** hello의 복사 작업이 너무**RelationalSource**, 다음 hello에 대 한 속성을 지정 하 고 **소스** 섹션 내용


| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| 쿼리 |사용자 지정 쿼리 tooread 데이터 hello를 사용 합니다. |SQL 쿼리 문자열. 예: `select * from MyTable` |아니요(**데이터 집합**의 **tableName**이 지정된 경우) |

#### <a name="example"></a>예제

```json
{
    "name": "CopySybaseToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "select * from DBA.Orders"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "inputs": [{
                "name": "SybaseDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobSybaseDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "SybaseToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

자세한 내용은 [Sybase 커넥터](data-factory-onprem-sybase-connector.md#copy-activity-properties) 문서를 참조하세요.

## <a name="teradata"></a>Teradata

### <a name="linked-service"></a>연결된 서비스
연결 된 서비스를 집합 hello toodefine는 Teradata **형식** hello 연결 서비스 너무**OnPremisesTeradata**, 다음 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션 내용  

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| server |Hello Teradata 서버의 이름입니다. |예 |
| authenticationType |Tooconnect toohello Teradata 데이터베이스를 사용 하는 인증 유형입니다. 가능한 값은 익명, 기본 및 Windows입니다. |예 |
| username |기본 또는 Windows 인증을 사용하는 경우 사용자 이름을 지정합니다. |아니요 |
| 암호 |Hello 사용자 이름에 대해 지정한 사용자 계정에 hello에 대 한 암호를 지정 합니다. |아니요 |
| gatewayName |데이터 팩터리 서비스 hello hello 게이트웨이의 이름 tooconnect toohello 온-프레미스 Teradata 데이터베이스를 사용 해야 합니다. |예 |

#### <a name="example"></a>예제
```json
{
    "name": "OnPremTeradataLinkedService",
    "properties": {
        "type": "OnPremisesTeradata",
        "typeProperties": {
            "server": "<server>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

자세한 내용은 [Teradata 커넥터](data-factory-onprem-teradata-connector.md#linked-service-properties) 문서를 참조하세요.

### <a name="dataset"></a>데이터 집합
toodefine Teradata Blob 데이터 집합 집합 hello **형식** hello 데이터 집합의 너무**RelationalTable**합니다. 현재,는 hello Teradata 데이터 집합에 대 한 지원 형식 속성이 없습니다. 

#### <a name="example"></a>예제
```json
{
    "name": "TeradataDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremTeradataLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

자세한 내용은 [Teradata 커넥터](data-factory-onprem-teradata-connector.md#dataset-properties) 문서를 참조하세요.

### <a name="relational-source-in-copy-activity"></a>복사 활동의 Relational 소스
Teradata 데이터베이스에서 데이터를 복사 하는 경우 설정 hello **소스 형식** hello의 복사 작업이 너무**RelationalSource**, 다음 hello에 대 한 속성을 지정 하 고 **소스**섹션:

| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| 쿼리 |사용자 지정 쿼리 tooread 데이터 hello를 사용 합니다. |SQL 쿼리 문자열. 예: `select * from MyTable` |예 |

#### <a name="example"></a>예제

```json
{
    "name": "CopyTeradataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', SliceStart, SliceEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "TeradataDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobTeradataDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "TeradataToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "isPaused": false
    }
}
```

자세한 내용은 [Teradata 커넥터](data-factory-onprem-teradata-connector.md#copy-activity-properties) 문서를 참조하세요.

## <a name="cassandra"></a>Cassandra


### <a name="linked-service"></a>연결된 서비스
연결 된 서비스를 집합 hello toodefine는 Cassandra **형식** hello 연결 서비스 너무**OnPremisesCassandra**, 다음 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션 내용  

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| host |Cassandra 서버에 대한 하나 이상의 IP 주소 또는 호스트 이름.<br/><br/>동시에 IP 주소 또는 호스트 이름 tooconnect tooall 서버의 쉼표로 구분 된 목록을 지정 합니다. |예 |
| 포트 |hello Cassandra 서버 hello TCP 포트는 클라이언트 연결에 대 한 toolisten를 사용 합니다. |아니요. 기본값: 9042 |
| authenticationType |Basic 또는 Anonymous |예 |
| username |Hello 사용자 계정에 대 한 사용자 이름을 지정 합니다. |예, authenticationType tooBasic 설정 된 경우. |
| 암호 |Hello 사용자 계정의 암호를 지정 합니다. |예, authenticationType tooBasic 설정 된 경우. |
| gatewayName |데이터베이스가 사용 되는 tooconnect toohello 온-프레미스 Cassandra hello 게이트웨이의 hello 이름입니다. |예 |
| encryptedCredential |Hello 게이트웨이로 암호화 된 자격 증명입니다. |아니요 |

#### <a name="example"></a>예제

```json
{
    "name": "CassandraLinkedService",
    "properties": {
        "type": "OnPremisesCassandra",
        "typeProperties": {
            "authenticationType": "Basic",
            "host": "<cassandra server name or IP address>",
            "port": 9042,
            "username": "user",
            "password": "password",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

자세한 내용은 [Cassandra 커넥터](data-factory-onprem-cassandra-connector.md#linked-service-properties) 문서를 참조하세요. 

### <a name="dataset"></a>데이터 집합
toodefine Cassandra dataset 집합 hello **형식** hello 데이터 집합의 너무**CassandraTable**, hello 다음과 같은 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션: 

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| keyspace |키 스페이스 hello 또는 Cassandra 데이터베이스에서 스키마의 이름입니다. |예(**CassandraSource**의 **query**가 정의되지 않은 경우) |
| tableName |Hello Cassandra 데이터베이스 테이블의 이름입니다. |예(**CassandraSource**의 **query**가 정의되지 않은 경우) |

#### <a name="example"></a>예제

```json
{
    "name": "CassandraInput",
    "properties": {
        "linkedServiceName": "CassandraLinkedService",
        "type": "CassandraTable",
        "typeProperties": {
            "tableName": "mytable",
            "keySpace": "<key space>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

자세한 내용은 [Cassandra 커넥터](data-factory-onprem-cassandra-connector.md#dataset-properties) 문서를 참조하세요. 

### <a name="cassandra-source-in-copy-activity"></a>복사 활동의 Cassandra 소스
Cassandra에서 데이터를 복사 하는 경우 설정 hello **소스 형식** hello의 복사 작업이 너무**CassandraSource**, 다음 hello에 대 한 속성을 지정 하 고 **소스** 섹션 :

| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| 쿼리 |사용자 지정 쿼리 tooread 데이터 hello를 사용 합니다. |SQL-92 쿼리 또는 CQL 쿼리입니다. [CQL 참조](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html)를 참조하세요. <br/><br/>SQL 쿼리를 사용할 때 지정 **키 스페이스 name.table 이름** tooquery 원하는 toorepresent hello 테이블입니다. |아니요(데이터 집합의 tableName 및 keyspace가 정의된 경우) |
| consistencyLevel |hello 일관성 수준이 지정 복제 개수 데이터 toohello 클라이언트 응용 프로그램을 반환 하기 전에 tooa 읽기 요청 응답 해야 합니다. Cassandra 검사 읽기 요청을 데이터 toosatisfy hello에 대 한 복제본의 지정 된 수를 hello 합니다. |ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE. 자세한 내용은 [데이터 일관성 구성](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) 을 참조하세요. |아니요. 기본값은 ONE입니다. |

#### <a name="example"></a>예제
  
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "CassandraToAzureBlob",
            "description": "Copy from Cassandra tooan Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "CassandraInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "CassandraSource",
                    "query": "select id, firstname, lastname from mykeyspace.mytable"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

자세한 내용은 [Cassandra 커넥터](data-factory-onprem-cassandra-connector.md#copy-activity-properties) 문서를 참조하세요.

## <a name="mongodb"></a>MongoDB

### <a name="linked-service"></a>연결된 서비스
연결 된 서비스를 집합 hello toodefine는 MongoDB **형식** hello 연결 서비스 너무**OnPremisesMongoDB**, 다음 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션 내용  

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| server |Hello MongoDB 서버의 IP 주소 또는 호스트 이름입니다. |예 |
| 포트 |MongoDB 서버 hello TCP 포트는 클라이언트 연결에 대 한 toolisten를 사용 합니다. |선택 사항, 기본값: 27017 |
| authenticationType |Basic 또는 Anonymous입니다. |예 |
| username |사용자 계정 tooaccess MongoDB 합니다. |예(기본 인증을 사용하는 경우) |
| 암호 |Hello 사용자 암호입니다. |예(기본 인증을 사용하는 경우) |
| authSource |원하는 toouse toocheck 자격 증명 인증에 대 한 hello MongoDB 데이터베이스의 이름입니다. |선택 사항(기본 인증을 사용하는 경우). 기본값: hello 관리자 계정 및 databaseName 속성을 사용 하 여 지정 하는 hello 데이터베이스를 사용 합니다. |
| databaseName |원하는 tooaccess hello MongoDB 데이터베이스 이름입니다. |예 |
| gatewayName |Hello 데이터 저장소에 액세스 하는 hello 게이트웨이의 이름입니다. |예 |
| encryptedCredential |게이트웨이에 의해 암호화된 자격 증명입니다. |옵션 |

#### <a name="example"></a>예제

```json
{
    "name": "OnPremisesMongoDbLinkedService",
    "properties": {
        "type": "OnPremisesMongoDb",
        "typeProperties": {
            "authenticationType": "<Basic or Anonymous>",
            "server": "< hello IP address or host name of hello MongoDB server >",
            "port": "<hello number of hello TCP port that hello MongoDB server uses toolisten for client connections.>",
            "username": "<username>",
            "password": "<password>",
            "authSource": "< hello database that you want toouse toocheck your credentials for authentication. >",
            "databaseName": "<database name>",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

자세한 내용은 [MongoDB 커넥터](data-factory-on-premises-mongodb-connector.md#linked-service-properties) 문서를 참조하세요.

### <a name="dataset"></a>데이터 집합
toodefine MongoDB dataset 집합 hello **형식** hello 데이터 집합의 너무**MongoDbCollection**, hello 다음과 같은 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션: 

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| collectionName |MongoDB 데이터베이스의 hello 컬렉션의 이름입니다. |예 |

#### <a name="example"></a>예제

```json
{
    "name": "MongoDbInputDataset",
    "properties": {
        "type": "MongoDbCollection",
        "linkedServiceName": "OnPremisesMongoDbLinkedService",
        "typeProperties": {
            "collectionName": "<Collection name>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

자세한 내용은 [MongoDB 커넥터](data-factory-on-premises-mongodb-connector.md#dataset-properties) 문서를 참조하세요.

#### <a name="mongodb-source-in-copy-activity"></a>복사 활동의 MongoDB 소스
MongoDB에서 데이터를 복사 하는 경우 설정 hello **소스 형식** hello의 복사 작업이 너무**MongoDbSource**, 다음 hello에 대 한 속성을 지정 하 고 **소스** 섹션:

| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| 쿼리 |사용자 지정 쿼리 tooread 데이터 hello를 사용 합니다. |SQL-92 쿼리 문자열입니다. 예: `select * from MyTable` |아니요(**데이터 집합**의 **collectionName**이 지정된 경우) |

#### <a name="example"></a>예제

```json
{
    "name": "CopyMongoDBToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "MongoDbSource",
                    "query": "select * from MyTable"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "MongoDbInputDataset"
            }],
            "outputs": [{
                "name": "AzureBlobOutputDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "MongoDBToAzureBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

자세한 내용은 [MongoDB 커넥터](data-factory-on-premises-mongodb-connector.md#copy-activity-properties) 문서를 참조하세요.

## <a name="amazon-s3"></a>Amazon S3


### <a name="linked-service"></a>연결된 서비스
연결 된 서비스를 집합 hello toodefine Amazon S3 **형식** hello 연결 서비스 너무**AwsAccessKey**, 다음 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션 :  

| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| accessKeyID |Hello 비밀 선택 키의 ID입니다. |string |예 |
| secretAccessKey |자체 hello 비밀 선택 키입니다. |암호화된 비밀 문자열 |예 |

#### <a name="example"></a>예제
```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

자세한 내용은 [Amazon S3 커넥터](data-factory-amazon-simple-storage-service-connector.md#linked-service-properties) 문서를 참조 하세요.

### <a name="dataset"></a>데이터 집합
데이터 집합 toodefine Amazon S3 집합 hello **형식** hello 데이터 집합의 너무**AmazonS3**, hello 다음과 같은 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션: 

| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| bucketName |hello S3 버킷 이름입니다. |문자열 |예 |
| key |S3 hello 개체 키입니다. |문자열 |아니요 |
| 접두사 |Hello S3 개체 키에 대 한 접두사입니다. 이 접두사로 시작하는 키를 가진 개체가 선택됩니다. 키가 비어 있을 때에만 적용됩니다. |string |아니요 |
| 버전 |S3 개체 S3 버전 관리를 사용 하는 경우의 hello 버전입니다. |문자열 |아니요 |
| format | hello 형식 유형만 지원 됩니다: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**합니다. 집합 hello **형식** 이러한 값의 형식 tooone 아래의 속성입니다. 자세한 내용은 [텍스트 형식](data-factory-supported-file-and-compression-formats.md#text-format), [Json 형식](data-factory-supported-file-and-compression-formats.md#json-format), [Avro 형식](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc 형식](data-factory-supported-file-and-compression-formats.md#orc-format) 및 [Parquet 형식](data-factory-supported-file-and-compression-formats.md#parquet-format) 섹션을 참조하세요. <br><br> 너무 하려는 경우**파일을 다음으로 복사-은** 간의 파일 기반 저장소 (이진 복사), 두 입력 및 출력 데이터 집합 정의의 hello 형식 섹션을 건너뛰십시오. |아니요 | |
| 압축 | Hello 유형 및 hello 데이터에 대 한 압축 수준을 지정 합니다. 지원되는 형식은 **GZip**, **Deflate**, **BZip2** 및 **ZipDeflate**입니다. 지원 되는 hello 수준은: **최적** 및 **fastest 이면**합니다. 자세한 내용은 [Azure Data Factory의 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md#compression-support)을 참조하세요. |아니요 | |


> [!NOTE]
> bucketName + 키 hello S3 개체 여기서 버킷에 S3 개체에 대 한 hello 루트 컨테이너 하 고 키가 hello 전체 경로 tooS3 개체의 hello 위치를 지정 합니다.

#### <a name="example-sample-dataset-with-prefix"></a>예제: 샘플 데이터 집합(prefix 포함)

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "prefix": "testFolder/test",
            "bucketName": "<S3 bucket name>",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
#### <a name="example-sample-data-set-with-version"></a>예제: 샘플 데이터 집합(version 포함)

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "key": "testFolder/test.orc",
            "bucketName": "<S3 bucket name>",
            "version": "XXXXXXXXXczm0CJajYkHf0_k6LhBmkcL",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

#### <a name="example-dynamic-paths-for-s3"></a>예제: S3에 대한 동적 경로
Hello 샘플 hello Amazon S3 데이터 집합에서 키 및 bucketName 속성에 대 한 고정된 값을 사용 합니다.

```json
"key": "testFolder/test.orc",
"bucketName": "<S3 bucket name>",
```

SliceStart와 같은 시스템 변수를 사용 하 여 hello 키와 bucketName 런타임에 동적으로 계산 되는 데이터 팩터리를 가질 수 있습니다.

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

작업을 수행할 수는 Amazon S3 데이터 집합의 hello 접두사 속성에 대 한 hello 동일 합니다. 지원되는 함수 및 변수 목록은 [Data Factory 함수 및 시스템 변수](data-factory-functions-variables.md) 를 참조하세요.

자세한 내용은 [Amazon S3 커넥터](data-factory-amazon-simple-storage-service-connector.md#dataset-properties) 문서를 참조 하세요.

### <a name="file-system-source-in-copy-activity"></a>복사 활동의 파일 시스템 소스
Amazon s 3에서 데이터를 복사 하는 경우 설정 hello **소스 형식** hello의 복사 작업이 너무**FileSystemSource**, 다음 hello에 대 한 속성을 지정 하 고 **소스** 섹션 :


| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| recursive |Hello 디렉터리 개체 toorecursively 목록 S3 여부를 지정 합니다. |True/False |아니요 |


#### <a name="example"></a>예제


```json
{
    "name": "CopyAmazonS3ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource",
                    "recursive": true
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "AmazonS3InputDataset"
            }],
            "outputs": [{
                "name": "AzureBlobOutputDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "AmazonS3ToBlob"
        }],
        "start": "2016-08-08T18:00:00",
        "end": "2016-08-08T19:00:00"
    }
}
```

자세한 내용은 [Amazon S3 커넥터](data-factory-amazon-simple-storage-service-connector.md#copy-activity-properties) 문서를 참조 하세요.

## <a name="file-system"></a>파일 시스템


### <a name="linked-service"></a>연결된 서비스
온-프레미스 파일 시스템 tooan Azure 데이터 팩터리에 hello로 연결할 수 있습니다 **온-프레미스 파일 서버** 연결 된 서비스입니다. 다음 표에서 hello JSON 요소를 특정 toohello 온-프레미스 파일 서버를 연결 된 서비스에 대 한 설명을 제공 합니다.

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| type |Hello type 속성이 너무 설정 되어 있는지 확인**OnPremisesFileServer**합니다. |예 |
| host |Toocopy hello 폴더의 hello 루트 경로 지정 합니다. Hello 이스케이프 문자를 사용 하 여 ' \ ' hello 문자열의 특수 문자에 대 한 합니다. 예제를 살펴보려면 [연결된 서비스 및 데이터 집합 정의 샘플](#sample-linked-service-and-dataset-definitions) 을 참조하세요. |예 |
| userid |Hello 있는 사용자에 게 액세스 toohello 서버 hello ID를 지정 합니다. |아니요(encryptedCredential을 선택하는 경우) |
| 암호 |Hello 사용자 (userid)에 대 한 hello 암호를 지정 합니다. |아니요(encryptedcredential을 선택하는 경우) |
| encryptedCredential |새로 만들기-AzureRmDataFactoryEncryptValue hello cmdlet을 실행 하 여 얻을 수 있는 암호화 hello 자격 증명을 지정 합니다. |아니요 (일반 텍스트로 toospecify userid 및 password 선택) 하는 경우 |
| gatewayName |데이터 팩터리 tooconnect toohello 온-프레미스 파일 서버를 사용 해야 하는 hello 게이트웨이의 hello 이름을 지정 합니다. |예 |

#### <a name="sample-folder-path-definitions"></a>샘플 폴더 경로 정의 
| 시나리오 | 연결된 서비스 정의의 호스트 | 데이터 집합 정의의 folderPath |
| --- | --- | --- |
| 데이터 관리 게이트웨이 컴퓨터의 로컬 폴더:  <br/><br/>예: D:\\\* 또는 D:\folder\subfolder\\* |D:\\\\(데이터 관리 게이트웨이 버전 2.0 이상) <br/><br/> localhost(데이터 관리 게이트웨이 버전 2.0 미만) |.\\\\ 또는 folder\\\\subfolder(데이터 관리 게이트웨이 버전 2.0 이상) <br/><br/>D:\\\\ 또는 D:\\\\folder\\\\subfolder(게이트웨이 버전 2.0 미만) |
| 원격 공유 폴더:  <br/><br/>예: \\\\myserver\\share\\\* 또는 \\\\myserver\\share\\folder\\subfolder\\* |\\\\\\\\myserver\\\\share |.\\\\ 또는 folder\\\\subfolder |


#### <a name="example-using-username-and-password-in-plain-text"></a>예제: 일반 텍스트에 사용자 이름 및 암호 사용

```json
{
    "Name": "OnPremisesFileServerLinkedService",
    "properties": {
        "type": "OnPremisesFileServer",
        "typeProperties": {
            "host": "\\\\Contosogame-Asia",
            "userid": "Admin",
            "password": "123456",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-using-encryptedcredential"></a>예제: encryptedcredential 사용

```json
{
    "Name": " OnPremisesFileServerLinkedService ",
    "properties": {
        "type": "OnPremisesFileServer",
        "typeProperties": {
            "host": "D:\\",
            "encryptedCredential": "WFuIGlzIGRpc3Rpbmd1aXNoZWQsIG5vdCBvbmx5IGJ5xxxxxxxxxxxxxxxxx",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

자세한 내용은 [파일 시스템 커넥터](data-factory-onprem-file-system-connector.md#linked-service-properties) 문서를 참조하세요.

### <a name="dataset"></a>데이터 집합
파일 시스템 데이터 집합, toodefine 집합 hello **형식** hello 데이터 집합의 너무**FileShare**, hello 다음과 같은 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션: 

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| folderPath |Hello 하위 경로 toohello 폴더를 지정합니다. Hello 이스케이프 문자를 사용 하 여 ' \' hello 문자열의 특수 문자에 대 한 합니다. 예제를 살펴보려면 [연결된 서비스 및 데이터 집합 정의 샘플](#sample-linked-service-and-dataset-definitions) 을 참조하세요.<br/><br/>이 속성을 결합할 수 **partitionBy** toohave 폴더 경로 분할 영역에 따라 시작/종료 날짜와 시간입니다. |예 |
| fileName |Hello에 hello hello 파일 이름을 지정 **folderPath** hello 테이블 toorefer tooa 특정 파일 hello 폴더에 들어 있습니다. 이 속성에 대 한 모든 값을 지정 하지 않는 경우 hello 테이블 hello 폴더의 tooall 파일을 가리킵니다.<br/><br/>출력 데이터 집합에 대 한 파일 이름을 지정 하지 않으면, hello hello 생성 된 파일의 이름이 형식에 따라 hello에: <br/><br/>`Data.<Guid>.txt`(예: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt) |아니요 |
| fileFilter |필터 toobe tooselect 사용 되는 모든 파일이 아니라 hello folderPath에 있는 파일의 하위 집합을 지정 합니다. <br/><br/>허용 되는 값은 `*`(여러 문자) 및 `?`(하나의 문자)입니다.<br/><br/>예 1: "fileFilter": "*.log"<br/>예 2: "fileFilter": 2016-1-?.txt"<br/><br/>fileFilter는 FileShare 입력 데이터 집합에 적용할 수 있습니다. |아니요 |
| partitionedBy |시계열 데이터에 대 한 partitionedBy toospecify 동적 folderPath/파일 이름을 사용할 수 있습니다. 예를 들어 매시간 데이터에 대한 매개 변수를 포함하는 folderPath가 있습니다. |아니요 |
| format | hello 형식 유형만 지원 됩니다: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**합니다. 집합 hello **형식** 이러한 값의 형식 tooone 아래의 속성입니다. 자세한 내용은 [텍스트 형식](data-factory-supported-file-and-compression-formats.md#text-format), [Json 형식](data-factory-supported-file-and-compression-formats.md#json-format), [Avro 형식](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc 형식](data-factory-supported-file-and-compression-formats.md#orc-format) 및 [Parquet 형식](data-factory-supported-file-and-compression-formats.md#parquet-format) 섹션을 참조하세요. <br><br> 너무 하려는 경우**파일을 다음으로 복사-은** 간의 파일 기반 저장소 (이진 복사), 두 입력 및 출력 데이터 집합 정의의 hello 형식 섹션을 건너뛰십시오. |아니요 |
| 압축 | Hello 유형 및 hello 데이터에 대 한 압축 수준을 지정 합니다. 지원되는 형식은 **GZip**, **Deflate**, **BZip2** 및 **ZipDeflate**이고 지원되는 수준은 **최적** 및 **가장 빠름**입니다. [Azure Data Factory의 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md#compression-support)을 참조하세요. |아니요 |

> [!NOTE]
> fileName 및 fileFilter는 동시에 사용할 수 없습니다.

#### <a name="example"></a>예제

```json
{
    "name": "OnpremisesFileSystemInput",
    "properties": {
        "type": " FileShare",
        "linkedServiceName": " OnPremisesFileServerLinkedService ",
        "typeProperties": {
            "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
            "fileName": "{Hour}.csv",
            "partitionedBy": [{
                "name": "Year",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                        "format": "yyyy"
                }
            }, {
                "name": "Month",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                    "format": "MM"
                }
            }, {
                "name": "Day",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                    "format": "dd"
                }
            }, {
                "name": "Hour",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                    "format": "HH"
                }
            }]
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

자세한 내용은 [파일 시스템 커넥터](data-factory-onprem-file-system-connector.md#dataset-properties) 문서를 참조하세요.

### <a name="file-system-source-in-copy-activity"></a>복사 활동의 파일 시스템 소스
파일 시스템에서 데이터를 복사 하는 경우 설정 hello **소스 형식** hello의 복사 작업이 너무**FileSystemSource**, 다음 hello에 대 한 속성을 지정 하 고 **소스** 섹션 내용

| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| recursive |Hello 데이터 읽는지 재귀적으로 hello 지정 된 폴더 또는 hello 하위 폴더에서 나타냅니다. |True, False(기본값) |아니요 |

#### <a name="example"></a>예제

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2015-06-01T18:00:00",
        "end": "2015-06-01T19:00:00",
        "description": "Pipeline for copy activity",
        "activities": [{
            "name": "OnpremisesFileSystemtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "OnpremisesFileSystemInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
            "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
자세한 내용은 [파일 시스템 커넥터](data-factory-onprem-file-system-connector.md#copy-activity-properties) 문서를 참조하세요.

### <a name="file-system-sink-in-copy-activity"></a>복사 활동의 파일 시스템 싱크
시스템 데이터 tooFile 복사 하는 경우 설정 hello **싱크 유형** hello의 복사 작업이 너무**FileSystemSink**, 다음 hello에 대 한 속성을 지정 하 고 **싱크** 섹션:

| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| copyBehavior |파일 시스템이 나 BlobSource hello 원본이 상태인 hello 복사 동작을 정의 합니다. |**PreserveHierarchy:** hello 대상 폴더에서 hello 파일 계층 구조를 유지 합니다. 즉, hello 소스 파일 toohello 원본 폴더의 상대 경로 hello hello hello 대상 파일 toohello 대상 폴더의 상대 경로와 같은 hello 됩니다.<br/><br/>**FlattenHierarchy:** hello 원본 폴더에서 모든 파일은 hello 첫 번째 수준의 대상 폴더에 만들어집니다. hello 대상 파일은 자동으로 생성 된 이름으로 만들어집니다.<br/><br/>**MergeFiles:** hello 소스 폴더 tooone 파일에서 모든 파일을 병합 합니다. Hello 파일 이름/blob 이름이 지정 된 경우 hello 병합 된 파일 이름은 hello 지정 된 이름이입니다. 그렇지 않으면 자동 생성되는 파일 이름이 적용됩니다. |아니요 |
auto-

#### <a name="example"></a>예제

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2015-06-01T18:00:00",
        "end": "2015-06-01T20:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLtoOnPremisesFile",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSQLInput"
            }],
            "outputs": [{
                "name": "OnpremisesFileSystemOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "FileSystemSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 3,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

자세한 내용은 [파일 시스템 커넥터](data-factory-onprem-file-system-connector.md#copy-activity-properties) 문서를 참조하세요.

## <a name="ftp"></a>FTP

### <a name="linked-service"></a>연결된 서비스
연결 된 서비스를 집합 hello toodefine FTP **형식** hello 연결 서비스 너무**ftp 서버**, 다음 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션:  

| 속성 | 설명 | 필수 | 기본값 |
| --- | --- | --- | --- |
| host |FTP 서버 hello의 이름 또는 IP 주소 |예 |&nbsp; |
| authenticationType |인증 유형 지정 |예 |기본, 익명 |
| username |액세스 toohello FTP 서버에 있는 사용자 |아니요 |&nbsp; |
| 암호 |Hello 사용자 (사용자 이름)에 대 한 암호 |아니요 |&nbsp; |
| encryptedCredential |암호화 된 자격 증명 tooaccess hello FTP 서버 |아니요 |&nbsp; |
| gatewayName |Hello 데이터 관리 게이트웨이에 게이트웨이 tooconnect tooan의 이름 온-프레미스 FTP 서버 |아니요 |&nbsp; |
| 포트 |어떤 hello FTP 서버 수신 포트 |아니요 |21 |
| enableSsl |Toouse SSL/TLS 채널을 통해 FTP 여부를 지정 합니다. |아니요 |true |
| enableServerCertificateValidation |SSL/TLS 채널을 통해 FTP를 사용 하는 경우 tooenable 서버 SSL 인증서 유효성 검사 여부를 지정 합니다. |아니요 |true |

#### <a name="example-using-anonymous-authentication"></a>예제: 익명 인증 사용

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
            "typeProperties": {
            "authenticationType": "Anonymous",
            "host": "myftpserver.com"
        }
    }
}
```

#### <a name="example-using-username-and-password-in-plain-text-for-basic-authentication"></a>예제: 기본 인증에 일반 텍스트 형식의 사용자 이름 및 암호 사용

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "username": "Admin",
            "password": "123456"
        }
    }
}
```

#### <a name="example-using-port-enablessl-enableservercertificatevalidation"></a>예제: port, enableSsl, enableServerCertificateValidation 사용

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",    
            "username": "Admin",
            "password": "123456",
            "port": "21",
            "enableSsl": true,
            "enableServerCertificateValidation": true
        }
    }
}
```

#### <a name="example-using-encryptedcredential-for-authentication-and-gateway"></a>예제: 인증 및 게이트웨이에 encryptedCredential 사용

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "gatewayName": "<onpremgateway>"
        }
      }
}
```

자세한 내용은 [FTP 커넥터](data-factory-ftp-connector.md#linked-service-properties) 문서를 참조하세요.

### <a name="dataset"></a>데이터 집합
FTP toodefine 데이터 집합, 집합 hello **형식** hello 데이터 집합의 너무**FileShare**, hello 다음과 같은 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션: 

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| folderPath |하위 경로 toohello 폴더입니다. 이스케이프 문자를 사용 하 여 ' \ ' hello 문자열의 특수 문자에 대 한 합니다. 예제를 살펴보려면 [연결된 서비스 및 데이터 집합 정의 샘플](#sample-linked-service-and-dataset-definitions) 을 참조하세요.<br/><br/>이 속성을 결합할 수 **partitionBy** toohave 폴더 경로 분할 영역에 따라 시작/종료 날짜와 시간입니다. |예 
| fileName |Hello에 hello hello 파일 이름을 지정 **folderPath** hello 테이블 toorefer tooa 특정 파일 hello 폴더에 들어 있습니다. 이 속성에 대 한 모든 값을 지정 하지 않는 경우 hello 테이블 hello 폴더의 tooall 파일을 가리킵니다.<br/><br/>출력 데이터 집합에 대 한 파일 이름을 지정 하지 않으면,이 형식에 따라 hello에 hello 생성 된 파일의 hello 이름이 표시 됩니다. <br/><br/>Data.<Guid>.txt(예: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt) |아니요 |
| fileFilter |필터 toobe tooselect 사용 되는 모든 파일이 아니라 hello folderPath에 있는 파일의 하위 집합을 지정 합니다.<br/><br/>허용 되는 값은 `*`(여러 문자) 및 `?`(하나의 문자)입니다.<br/><br/>예 1: `"fileFilter": "*.log"`<br/>예 2: `"fileFilter": 2016-1-?.txt"`<br/><br/> fileFilter는 FileShare 입력 데이터 집합에 적용할 수 있습니다. 이 속성은 HDFS에는 지원되지 않습니다. |아니요 |
| partitionedBy |partitionedBy 사용된 toospecify 동적 folderPath 시계열 데이터에 대 한 파일 이름이 될 수 있습니다. 예를 들어 매시간 데이터에 대한 매개 변수가 있는 folderPath입니다. |아니요 |
| format | hello 형식 유형만 지원 됩니다: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**합니다. 집합 hello **형식** 이러한 값의 형식 tooone 아래의 속성입니다. 자세한 내용은 [텍스트 형식](data-factory-supported-file-and-compression-formats.md#text-format), [Json 형식](data-factory-supported-file-and-compression-formats.md#json-format), [Avro 형식](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc 형식](data-factory-supported-file-and-compression-formats.md#orc-format) 및 [Parquet 형식](data-factory-supported-file-and-compression-formats.md#parquet-format) 섹션을 참조하세요. <br><br> 너무 하려는 경우**파일을 다음으로 복사-은** 간의 파일 기반 저장소 (이진 복사), 두 입력 및 출력 데이터 집합 정의의 hello 형식 섹션을 건너뛰십시오. |아니요 |
| 압축 | Hello 유형 및 hello 데이터에 대 한 압축 수준을 지정 합니다. 지원되는 형식은 **GZip**, **Deflate**, **BZip2** 및 **ZipDeflate**이고 지원되는 수준은 **최적** 및 **가장 빠름**입니다. 자세한 내용은 [Azure Data Factory의 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md#compression-support)을 참조하세요. |아니요 |
| useBinaryTransfer |이전 전송 모드를 사용할지 여부를 지정합니다. 이진 모드인 경우 true이고 ASCII인 경우 false입니다. 기본값은 True입니다. 이 속성은 연결된 서비스 유형이 FtpServer인 경우에만 사용할 수 있습니다. |아니요 |

> [!NOTE]
> filename 및 fileFilter는 동시에 사용할 수 없습니다.

#### <a name="example"></a>예제

```json
{
    "name": "FTPFileInput",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "FTPLinkedService",
        "typeProperties": {
            "folderPath": "<path tooshared folder>",
            "fileName": "test.csv",
            "useBinaryTransfer": true
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

자세한 내용은 [FTP 커넥터](data-factory-ftp-connector.md#dataset-properties) 문서를 참조하세요.

### <a name="file-system-source-in-copy-activity"></a>복사 활동의 파일 시스템 소스
FTP 서버에서 데이터를 복사 하는 경우 설정 hello **소스 형식** hello의 복사 작업이 너무**FileSystemSource**, 다음 hello에 대 한 속성을 지정 하 고 **소스** 섹션 내용

| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| recursive |Hello 데이터 읽는지 재귀적으로 hello 하위 폴더 또는 hello 지정한 폴더에서만 나타냅니다. |True, False(기본값) |아니요 |

#### <a name="example"></a>예제

```json
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "FTPToBlobCopy",
            "inputs": [{
                "name": "FtpFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2016-08-24T18:00:00",
        "end": "2016-08-24T19:00:00"
    }
}
```

자세한 내용은 [FTP 커넥터](data-factory-ftp-connector.md#copy-activity-properties) 문서를 참조하세요.


## <a name="hdfs"></a>HDFS

### <a name="linked-service"></a>연결된 서비스
연결 된 서비스를 집합 hello toodefine는 HDFS **형식** hello 연결 서비스 너무**Hdfs**, 다음 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션:  

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| type |hello type 속성 설정 해야 합니다: **Hdfs** |예 |
| Url |URL toohello HDFS |예 |
| authenticationType |익명 또는 Windows입니다. <br><br> toouse **Kerberos 인증** HDFS 커넥터에 대 한 참조 너무[이 여기서](#use-kerberos-authentication-for-hdfs-connector) 온-프레미스 환경을 tooset 적절 하 게 합니다. |예 |
| userName |Windows 인증에 대한 사용자 이름. |예(Windows 인증에 대한) |
| password |Windows 인증에 대한 암호. |예(Windows 인증에 대한) |
| gatewayName |데이터 팩터리 서비스 hello hello 게이트웨이의 이름 tooconnect toohello HDFS 사용 해야 합니다. |예 |
| encryptedCredential |[새 AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) hello 액세스 자격 증명의 출력입니다. |아니요 |

#### <a name="example-using-anonymous-authentication"></a>예제: 익명 인증 사용

```json
{
    "name": "HDFSLinkedService",
    "properties": {
        "type": "Hdfs",
        "typeProperties": {
            "authenticationType": "Anonymous",
            "userName": "hadoop",
            "url": "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-using-windows-authentication"></a>예제: Windows 인증 사용

```json
{
    "name": "HDFSLinkedService",
    "properties": {
        "type": "Hdfs",
        "typeProperties": {
            "authenticationType": "Windows",
            "userName": "Administrator",
            "password": "password",
            "url": "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

자세한 내용은 [HDFS 커넥터](#data-factory-hdfs-connector.md#linked-service-properties) 문서를 참조하세요. 

### <a name="dataset"></a>데이터 집합
toodefine HDFS dataset 집합 hello **형식** hello 데이터 집합의 너무**FileShare**, hello 다음과 같은 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션: 

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| folderPath |경로 toohello 폴더입니다. 예: `myfolder`<br/><br/>이스케이프 문자를 사용 하 여 ' \ ' hello 문자열의 특수 문자에 대 한 합니다. 예: 폴더\하위 폴더의 경우 폴더\\\\하위 폴더를 지정하고 d:\samplefolder의 경우 d:\\\\samplefolder를 지정합니다.<br/><br/>이 속성을 결합할 수 **partitionBy** toohave 폴더 경로 분할 영역에 따라 시작/종료 날짜와 시간입니다. |예 |
| fileName |Hello에 hello hello 파일 이름을 지정 **folderPath** hello 테이블 toorefer tooa 특정 파일 hello 폴더에 들어 있습니다. 이 속성에 대 한 모든 값을 지정 하지 않는 경우 hello 테이블 hello 폴더의 tooall 파일을 가리킵니다.<br/><br/>출력 데이터 집합에 대 한 파일 이름을 지정 하지 않으면,이 형식에 따라 hello에 hello 생성 된 파일의 hello 이름이 표시 됩니다. <br/><br/>Data<Guid>.txt(예: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt) |아니요 |
| partitionedBy |partitionedBy 사용된 toospecify 동적 folderPath 시계열 데이터에 대 한 파일 이름이 될 수 있습니다. 예를 들어 folderPath는 매시간 데이터에 대해 매개 변수화됩니다. |아니요 |
| format | hello 형식 유형만 지원 됩니다: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**합니다. 집합 hello **형식** 이러한 값의 형식 tooone 아래의 속성입니다. 자세한 내용은 [텍스트 형식](data-factory-supported-file-and-compression-formats.md#text-format), [Json 형식](data-factory-supported-file-and-compression-formats.md#json-format), [Avro 형식](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc 형식](data-factory-supported-file-and-compression-formats.md#orc-format) 및 [Parquet 형식](data-factory-supported-file-and-compression-formats.md#parquet-format) 섹션을 참조하세요. <br><br> 너무 하려는 경우**파일을 다음으로 복사-은** 간의 파일 기반 저장소 (이진 복사), 두 입력 및 출력 데이터 집합 정의의 hello 형식 섹션을 건너뛰십시오. |아니요 |
| 압축 | Hello 유형 및 hello 데이터에 대 한 압축 수준을 지정 합니다. 지원되는 형식은 **GZip**, **Deflate**, **BZip2** 및 **ZipDeflate**입니다. 지원되는 수준은 **최적** 및 **가장 빠름**입니다. 자세한 내용은 [Azure Data Factory의 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md#compression-support)을 참조하세요. |아니요 |

> [!NOTE]
> filename 및 fileFilter는 동시에 사용할 수 없습니다.

#### <a name="example"></a>예제

```json
{
    "name": "InputDataset",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "HDFSLinkedService",
        "typeProperties": {
            "folderPath": "DataTransfer/UnitTest/"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

자세한 내용은 [HDFS 커넥터](#data-factory-hdfs-connector.md#dataset-properties) 문서를 참조하세요. 

### <a name="file-system-source-in-copy-activity"></a>복사 활동의 파일 시스템 소스
HDFS에서 데이터를 복사 하는 경우 설정 hello **소스 형식** hello의 복사 작업이 너무**FileSystemSource**, 다음 hello에 대 한 속성을 지정 하 고 **소스** 섹션:

**FileSystemSource** hello 다음과 같은 속성을 지원 합니다.

| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| recursive |Hello 데이터 읽는지 재귀적으로 hello 하위 폴더 또는 hello 지정한 폴더에서만 나타냅니다. |True, False(기본값) |아니요 |

#### <a name="example"></a>예제

```json
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "HdfsToBlobCopy",
            "inputs": [{
                "name": "InputDataset"
            }],
            "outputs": [{
                "name": "OutputDataset"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

자세한 내용은 [HDFS 커넥터](#data-factory-hdfs-connector.md#copy-activity-properties) 문서를 참조하세요.

## <a name="sftp"></a>SFTP


### <a name="linked-service"></a>연결된 서비스
연결 된 서비스를 집합 hello toodefine SFTP **형식** hello 연결 서비스 너무**Sftp**, 다음 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션:  

| 속성 | 설명 | 필수 |
| --- | --- | --- | --- |
| host | Hello SFTP 서버의 이름 또는 IP 주소입니다. |예 |
| 포트 |어떤 hello SFTP 서버 수신 대기 중인 포트입니다. hello 기본값은: 21 |아니요 |
| authenticationType |인증 유형을 지정합니다. 허용되는 값은 **기본** 및 **SshPublicKey**입니다. <br><br> 너무 참조[기본 인증을 사용 하 여](#using-basic-authentication) 및 [를 사용 하 여 SSH 공개 키 인증](#using-ssh-public-key-authentication) 더 많은 속성 및 JSON 샘플에서 각각 섹션. |예 |
| skipHostKeyValidation | Tooskip 호스트 키 유효성 검사 여부를 지정 합니다. | 아니요. hello 기본값: false |
| hostKeyFingerprint | Hello 호스트 키의 지문 안녕하세요를 지정 합니다. | 예 경우 hello `skipHostKeyValidation` toofalse 설정 됩니다.  |
| gatewayName |데이터 관리 게이트웨이 tooconnect tooan hello의 이름 온-프레미스 SFTP 서버. | 온-프레미스 SFTP 서버에서 데이터를 복사하는 경우에는 필수입니다. |
| encryptedCredential | 암호화 된 자격 증명 tooaccess hello SFTP 서버입니다. 자동 생성 된 복사 마법사 또는 hello ClickOnce 팝업 대화 상자에서 기본 인증 (사용자 이름 + 암호) 또는 SshPublicKey 인증 (사용자 이름 + 개인 키의 경로 또는 콘텐츠)를 지정 합니다. | 아니요. 온-프레미스 SFTP 서버에서 데이터를 복사하는 경우에만 적용됩니다. |

#### <a name="example-using-basic-authentication"></a>예제: 기본 인증 사용

toouse 기본 인증 설정 `authenticationType` 으로 `Basic`, hello SFTP 커넥터 hello 마지막 섹션에 도입 된 일반 자원을 hello 외에 다음과 같은 속성을 지정 합니다.

| 속성 | 설명 | 필수 |
| --- | --- | --- | --- |
| username | 사용자가 액세스 toohello SFTP 서버입니다. |예 |
| 암호 | Hello 사용자 (사용자 이름)에 대 한 암호입니다. | 예 |

```json
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<SFTP server name or IP address>",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "password": "xxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-basic-authentication-with-encrypted-credential"></a>예제: 암호화된 자격 증명으로 기본 인증**

```json
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<FTP server name or IP address>",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="using-ssh-public-key-authentication"></a>SSH 공개 키 인증 사용**

toouse 기본 인증 설정 `authenticationType` 으로 `SshPublicKey`, hello SFTP 커넥터 hello 마지막 섹션에 도입 된 일반 자원을 hello 외에 다음과 같은 속성을 지정 합니다.

| 속성 | 설명 | 필수 |
| --- | --- | --- | --- |
| username |액세스 toohello SFTP 서버에 있는 사용자 |예 |
| privateKeyPath | 절대 경로 toohello 지정 개인 키 파일 해당 게이트웨이에 액세스할 수 있습니다. | 어느 hello 지정 `privateKeyPath` 또는 `privateKeyContent`합니다. <br><br> 온-프레미스 SFTP 서버에서 데이터를 복사하는 경우에만 적용됩니다. |
| privateKeyContent | Hello 개인 키 콘텐츠는 serialize 된 문자열입니다. hello 복사 마법사 hello 개인 키 파일 읽고 hello 개인 키 콘텐츠를 자동으로 추출할 수 있습니다. 모든 다른 도구/SDK를 사용 하는 경우 hello privateKeyPath 속성을 대신 사용 합니다. | 어느 hello 지정 `privateKeyPath` 또는 `privateKeyContent`합니다. |
| passPhrase | 암호 구문을 통해 hello 키 파일을 보호 하는 경우에 hello 전달 구를/암호 toodecrypt hello 개인 키를 지정 합니다. | Yes 전달 구에 의해 hello 개인 키 파일 보호를 사용 합니다. |

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyPath",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<FTP server name or IP address>",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyPath": "D:\\privatekey_openssh",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true,
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-sshpublickey-authentication-using-private-key-content"></a>예제: 개인 키 콘텐츠를 사용하여 SshPublicKey 인증**

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyContent",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver.westus.cloudapp.azure.com",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyContent": "<base64 string of hello private key content>",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true
        }
    }
}
```

자세한 내용은 [SFTP 커넥터](data-factory-sftp-connector.md#linked-service-properties) 문서를 참조하세요. 

### <a name="dataset"></a>데이터 집합
toodefine SFTP 데이터 집합, 집합 hello **형식** hello 데이터 집합의 너무**FileShare**, hello 다음과 같은 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션: 

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| folderPath |하위 경로 toohello 폴더입니다. 이스케이프 문자를 사용 하 여 ' \ ' hello 문자열의 특수 문자에 대 한 합니다. 예제를 살펴보려면 [연결된 서비스 및 데이터 집합 정의 샘플](#sample-linked-service-and-dataset-definitions) 을 참조하세요.<br/><br/>이 속성을 결합할 수 **partitionBy** toohave 폴더 경로 분할 영역에 따라 시작/종료 날짜와 시간입니다. |예 |
| fileName |Hello에 hello hello 파일 이름을 지정 **folderPath** hello 테이블 toorefer tooa 특정 파일 hello 폴더에 들어 있습니다. 이 속성에 대 한 모든 값을 지정 하지 않는 경우 hello 테이블 hello 폴더의 tooall 파일을 가리킵니다.<br/><br/>출력 데이터 집합에 대 한 파일 이름을 지정 하지 않으면,이 형식에 따라 hello에 hello 생성 된 파일의 hello 이름이 표시 됩니다. <br/><br/>Data.<Guid>.txt(예: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt) |아니요 |
| fileFilter |필터 toobe tooselect 사용 되는 모든 파일이 아니라 hello folderPath에 있는 파일의 하위 집합을 지정 합니다.<br/><br/>허용 되는 값은 `*`(여러 문자) 및 `?`(하나의 문자)입니다.<br/><br/>예 1: `"fileFilter": "*.log"`<br/>예 2: `"fileFilter": 2016-1-?.txt"`<br/><br/> fileFilter는 FileShare 입력 데이터 집합에 적용할 수 있습니다. 이 속성은 HDFS에는 지원되지 않습니다. |아니요 |
| partitionedBy |partitionedBy 사용된 toospecify 동적 folderPath 시계열 데이터에 대 한 파일 이름이 될 수 있습니다. 예를 들어 매시간 데이터에 대한 매개 변수가 있는 folderPath입니다. |아니요 |
| format | hello 형식 유형만 지원 됩니다: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**합니다. 집합 hello **형식** 이러한 값의 형식 tooone 아래의 속성입니다. 자세한 내용은 [텍스트 형식](data-factory-supported-file-and-compression-formats.md#text-format), [Json 형식](data-factory-supported-file-and-compression-formats.md#json-format), [Avro 형식](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc 형식](data-factory-supported-file-and-compression-formats.md#orc-format) 및 [Parquet 형식](data-factory-supported-file-and-compression-formats.md#parquet-format) 섹션을 참조하세요. <br><br> 너무 하려는 경우**파일을 다음으로 복사-은** 간의 파일 기반 저장소 (이진 복사), 두 입력 및 출력 데이터 집합 정의의 hello 형식 섹션을 건너뛰십시오. |아니요 |
| 압축 | Hello 유형 및 hello 데이터에 대 한 압축 수준을 지정 합니다. 지원되는 형식은 **GZip**, **Deflate**, **BZip2** 및 **ZipDeflate**입니다. 지원되는 수준은 **최적** 및 **가장 빠름**입니다. 자세한 내용은 [Azure Data Factory의 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md#compression-support)을 참조하세요. |아니요 |
| useBinaryTransfer |이전 전송 모드를 사용할지 여부를 지정합니다. 이진 모드인 경우 true이고 ASCII인 경우 false입니다. 기본값은 True입니다. 이 속성은 연결된 서비스 유형이 FtpServer인 경우에만 사용할 수 있습니다. |아니요 |

> [!NOTE]
> filename 및 fileFilter는 동시에 사용할 수 없습니다.

#### <a name="example"></a>예제

```json
{
    "name": "SFTPFileInput",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "SftpLinkedService",
        "typeProperties": {
            "folderPath": "<path tooshared folder>",
            "fileName": "test.csv"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

자세한 내용은 [SFTP 커넥터](data-factory-sftp-connector.md#dataset-properties) 문서를 참조하세요. 

### <a name="file-system-source-in-copy-activity"></a>복사 활동의 파일 시스템 소스
SFTP 원본에서 데이터를 복사 하는 경우 설정 hello **소스 형식** hello의 복사 작업이 너무**FileSystemSource**, 다음 hello에 대 한 속성을 지정 하 고 **소스** 섹션 내용

| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| recursive |Hello 데이터 읽는지 재귀적으로 hello 하위 폴더 또는 hello 지정한 폴더에서만 나타냅니다. |True, False(기본값) |아니요 |



#### <a name="example"></a>예제

```json
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "SFTPToBlobCopy",
            "inputs": [{
                "name": "SFTPFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2017-02-20T18:00:00",
        "end": "2017-02-20T19:00:00"
    }
}
```

자세한 내용은 [SFTP 커넥터](data-factory-sftp-connector.md#copy-activity-properties) 문서를 참조하세요.


## <a name="http"></a>HTTP

### <a name="linked-service"></a>연결된 서비스
연결 된 서비스를 집합 hello toodefine HTTP **형식** hello 연결 서비스 너무**Http**, 다음 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션:  

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| url | 기본 URL toohello 웹 서버 | 예 |
| authenticationType | Hello 인증 유형을 지정합니다. 허용되는 값: **Anonymous**, **Basic**, **Digest**, **Windows**, **ClientCertificate**. <br><br> 이 표 아래에 더 많은 속성 및 JSON 샘플 toosections 해당 인증 형식에 각각 참조 합니다. | 예 |
| enableServerCertificateValidation | 소스 HTTPS 웹 서버인 경우 tooenable 서버 SSL 인증서 유효성 검사 여부를 지정 합니다. | 아니요. 기본값은 True입니다. |
| gatewayName | 데이터 관리 게이트웨이 tooconnect tooan hello의 이름 온-프레미스 HTTP 소스입니다. | 온-프레미스 HTTP 소스에서 데이터를 복사하는 경우에는 필수입니다. |
| encryptedCredential | 암호화 된 자격 증명 tooaccess hello HTTP 끝점입니다. 자동 생성 된 복사 마법사 또는 hello ClickOnce 팝업 대화 상자에 hello 인증 정보를 구성 합니다. | 아니요. 온-프레미스 HTTP 서버에서 데이터를 복사하는 경우에만 적용됩니다. |

#### <a name="example-using-basic-digest-or-windows-authentication"></a>예제: Basic, Digest 또는 Windows 인증 사용
설정 `authenticationType` 으로 `Basic`, `Digest`, 또는 `Windows`, hello hello HTTP 커넥터 제네릭 위에서 소개 하는 것 외에 다음과 같은 속성을 지정 합니다.

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| username | 사용자 이름 tooaccess hello HTTP 끝점입니다. | 예 |
| 암호 | Hello 사용자 (사용자 이름)에 대 한 암호입니다. | 예 |

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "Http",
        "typeProperties": {
            "authenticationType": "basic",
            "url": "https://en.wikipedia.org/wiki/",
            "userName": "user name",
            "password": "password"
        }
    }
}
```

#### <a name="example-using-clientcertificate-authentication"></a>예제: ClientCertificate 인증 사용

toouse 기본 인증 설정 `authenticationType` 으로 `ClientCertificate`, hello hello HTTP 커넥터 제네릭 위에서 소개 하는 것 외에 다음과 같은 속성을 지정 합니다.

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| embeddedCertData | hello 개인 정보 교환 (PFX) 파일의 이진 데이터의 Base64 인코딩 내용 hello입니다. | 어느 hello 지정 `embeddedCertData` 또는 `certThumbprint`합니다. |
| certThumbprint | 게이트웨이 컴퓨터의 인증서 저장소에 설치 된 hello 인증서의 지문을 hello 합니다. 온-프레미스 HTTP 소스에서 데이터를 복사하는 경우에만 적용됩니다. | 어느 hello 지정 `embeddedCertData` 또는 `certThumbprint`합니다. |
| 암호 | Hello 인증서와 연결 된 암호입니다. | 아니요 |

사용 하는 경우 `certThumbprint` toogrant hello 읽기 권한은 toohello 게이트웨이 서비스가 필요한 경우 인증 및 hello 인증서 hello hello 로컬 컴퓨터의 개인 저장소에 설치 하면:

1. MMC(Microsoft Management Console)를 시작합니다. Hello 추가 **인증서** 스냅인 해당 대상 hello **로컬 컴퓨터**합니다.
2. **인증서**, **개인**을 확장하고 **인증서**를 클릭합니다.
3. Hello 개인 저장소에서 hello 인증서를 마우스 오른쪽 단추로 클릭 하 고 선택 **모든 작업**->**개인 키 관리...**
3. Hello에 **보안** 탭에서 데이터 관리 게이트웨이 호스트 서비스가 실행 되 고 있는 hello 읽기 액세스 toohello 인증서로 hello 사용자 계정을 추가 합니다.  

**예: 클라이언트 인증서를 사용 하 여:** 이 연결 된 서비스 링크 데이터 팩터리 tooan 온-프레미스 HTTP 웹 서버. 데이터 관리 게이트웨이가 설치 된 hello 컴퓨터에 설치 된 클라이언트 인증서를 사용 합니다.

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "Http",
        "typeProperties": {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "certThumbprint": "thumbprint of certificate",
            "gatewayName": "gateway name"
        }
    }
}
```

#### <a name="example-using-client-certificate-in-a-file"></a>예제: 파일로 클라이언트 인증서 사용
서비스 링크 데이터 팩터리 tooan 온-프레미스 HTTP 웹 서버를 연결 설정 합니다. 데이터 관리 게이트웨이가 설치 된 hello 컴퓨터에 클라이언트 인증서 파일을 사용 합니다.

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "Http",
        "typeProperties": {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "embeddedCertData": "base64 encoded cert data",
            "password": "password of cert"
        }
    }
}
```

자세한 내용은 [HTTP 커넥터](data-factory-http-connector.md#linked-service-properties) 문서를 참조하세요.

### <a name="dataset"></a>데이터 집합
HTTP toodefine 데이터 집합, 집합 hello **형식** hello 데이터 집합의 너무**Http**, hello 다음과 같은 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션: 

| 속성 | 설명 | 필수 |
|:--- |:--- |:--- |
| relativeUrl | 상대 URL toohello 리소스 hello 데이터가 들어 있는입니다. 경로 지정 하지 않으면 hello 연결 된 서비스 정의에 지정 된 유일한 hello URL 사용 됩니다. <br><br> 사용할 수 있습니다 tooconstruct 동적 URL [데이터 팩터리 함수 및 시스템 변수](data-factory-functions-variables.md), 예: `"relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)"`합니다. | 아니요 |
| requestMethod | HTTP 메서드입니다. 허용되는 값은 **GET** 또는 **POST**입니다. | 아니요. 기본값은 `GET`입니다. |
| additionalHeaders | 추가 HTTP 요청 헤더입니다. | 아니요 |
| requestBody | HTTP 요청의 본문입니다. | 아니요 |
| format | Toosimply 하려는 경우 **으로 HTTP 끝점에서 hello 데이터를 검색-은** 것, 구문 분석 하지 않고 형식 설정에이 건너뜁니다. <br><br> 복사 중 tooparse hello HTTP 응답을 콘텐츠에 삭제 하는 경우에 hello 형식 유형만 지원 됩니다: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**합니다. 자세한 내용은 [텍스트 형식](data-factory-supported-file-and-compression-formats.md#text-format), [Json 형식](data-factory-supported-file-and-compression-formats.md#json-format), [Avro 형식](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc 형식](data-factory-supported-file-and-compression-formats.md#orc-format) 및 [Parquet 형식](data-factory-supported-file-and-compression-formats.md#parquet-format) 섹션을 참조하세요. |아니요 |
| 압축 | Hello 유형 및 hello 데이터에 대 한 압축 수준을 지정 합니다. 지원되는 형식은 **GZip**, **Deflate**, **BZip2** 및 **ZipDeflate**입니다. 지원되는 수준은 **최적** 및 **가장 빠름**입니다. 자세한 내용은 [Azure Data Factory의 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md#compression-support)을 참조하세요. |아니요 |

#### <a name="example-using-hello-get-default-method"></a>예: hello GET (기본값) 메서드 사용

```json
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "XXX/test.xml",
            "additionalHeaders": "Connection: keep-alive\nUser-Agent: Mozilla/5.0\n"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

#### <a name="example-using-hello-post-method"></a>예: hello POST 메서드를 사용 하 여

```json
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "/XXX/test.xml",
            "requestMethod": "Post",
            "requestBody": "body for POST HTTP request"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```
자세한 내용은 [HTTP 커넥터](data-factory-http-connector.md#dataset-properties) 문서를 참조하세요.

### <a name="http-source-in-copy-activity"></a>복사 활동의 HTTP 소스
HTTP 소스에서 데이터를 복사 하는 경우 설정 hello **소스 형식** hello의 복사 작업이 너무**HttpSource**, 다음 hello에 대 한 속성을 지정 하 고 **소스** 섹션:

| 속성 | 설명 | 필수 |
| -------- | ----------- | -------- |
| httpRequestTimeout | 안녕 hello HTTP 요청 tooget 응답 하기 위한 시간 제한 (TimeSpan). Hello timeout tooget 응답으로 hello timeout tooread 응답 데이터가 아닌 경우 | 아니요. 기본값: 00:01:40 |


#### <a name="example"></a>예제

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "HttpSourceToAzureBlob",
            "description": "Copy from an HTTP source tooan Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "HttpSourceDataInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "HttpSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

자세한 내용은 [HTTP 커넥터](data-factory-http-connector.md#copy-activity-properties) 문서를 참조하세요.

## <a name="odata"></a>OData

### <a name="linked-service"></a>연결된 서비스
연결 된 서비스를 집합 hello toodefine OData **형식** hello 연결 서비스 너무**OData**, 다음 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션:  

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| url |Hello OData 서비스의 Url입니다. |예 |
| authenticationType |Tooconnect toohello OData 원본을 사용 하는 인증 유형입니다. <br/><br/> 클라우드 OData의 경우 가능한 값은 익명, 기본 및 OAuth입니다(Azure Data Factory는 현재 Azure Active Directory 기반 OAuth만 지원). <br/><br/> 온-프레미스 OData의 경우 가능한 값은 익명, 기본 및 Windows입니다. |예 |
| username |기본 인증을 사용하는 경우 사용자 이름을 지정합니다. |예(기본 인증을 사용하는 경우에만) |
| 암호 |Hello 사용자 이름에 대해 지정한 사용자 계정에 hello에 대 한 암호를 지정 합니다. |예(기본 인증을 사용하는 경우에만) |
| authorizedCredential |OAuth를 사용 하는 경우 클릭 **Authorize** hello 데이터 팩터리 복사 마법사 또는 편집기에서 단추 및이 속성의 hello 값 자동 생성 됩니다. 사용자의 자격 증명을 입력 합니다. |예(OAuth 인증을 사용하는 경우에만) |
| gatewayName |데이터 팩터리 서비스 hello hello 게이트웨이의 이름 tooconnect toohello 온-프레미스 OData 서비스를 사용 해야 합니다. 온-프레미스 OData 소스의 데이터를 복사하는 경우에만 지정합니다. |아니요 |

#### <a name="example---using-basic-authentication"></a>예제: 기본 인증 사용
```json
{
    "name": "inputLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Basic",
            "username": "username",
            "password": "password"
        }
    }
}
```

#### <a name="example---using-anonymous-authentication"></a>예제: 익명 인증 사용

```json
{
    "name": "ODataLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Anonymous"
        }
    }
}
```

#### <a name="example---using-windows-authentication-accessing-on-premises-odata-source"></a>예제: 온-프레미스 OData 소스에 액세스하는 Windows 인증 사용

```json
{
    "name": "inputLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "<endpoint of on-premises OData source, for example, Dynamics CRM>",
            "authenticationType": "Windows",
            "username": "domain\\user",
            "password": "password",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example---using-oauth-authentication-accessing-cloud-odata-source"></a>예제: 클라우드 OData 소스에 액세스하는 OAuth 인증 사용
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "<endpoint of cloud OData source, for example, https://<tenant>.crm.dynamics.com/XRMServices/2011/OrganizationData.svc>",
            "authenticationType": "OAuth",
            "authorizedCredential": "<auto generated by clicking hello Authorize button on UI>"
        }
    }
}
```

자세한 내용은 [OData 커넥터](data-factory-odata-connector.md#linked-service-properties) 문서를 참조하세요.

### <a name="dataset"></a>데이터 집합
OData 데이터 집합, toodefine 집합 hello **형식** hello 데이터 집합의 너무**ODataResource**, hello 다음과 같은 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션: 

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| path |경로 toohello OData 리소스 |아니요 |

#### <a name="example"></a>예제

```json
{
    "name": "ODataDataset",
    "properties": {
        "type": "ODataResource",
        "typeProperties": {
            "path": "Products"
        },
        "linkedServiceName": "ODataLinkedService",
        "structure": [],
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "retryInterval": "00:01:00",
            "retryTimeout": "00:10:00",
            "maximumRetry": 3
        }
    }
}
```

자세한 내용은 [OData 커넥터](data-factory-odata-connector.md#dataset-properties) 문서를 참조하세요.

### <a name="relational-source-in-copy-activity"></a>복사 활동의 Relational 소스
OData 원본에서 데이터를 복사 하는 경우 설정 hello **소스 형식** hello의 복사 작업이 너무**RelationalSource**, 다음 hello에 대 한 속성을 지정 하 고 **소스** 섹션 내용

| 속성 | 설명 | 예 | 필수 |
| --- | --- | --- | --- |
| 쿼리 |사용자 지정 쿼리 tooread 데이터 hello를 사용 합니다. |"?$select=Name, Description&$top=5" |아니요 |

#### <a name="example"></a>예제

```json
{
    "name": "CopyODataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "?$select=Name, Description&$top=5"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "ODataDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobODataDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "ODataToBlob"
        }],
        "start": "2017-02-01T18:00:00",
        "end": "2017-02-03T19:00:00"
    }
}
```

자세한 내용은 [OData 커넥터](data-factory-odata-connector.md#copy-activity-properties) 문서를 참조하세요.


## <a name="odbc"></a>ODBC


### <a name="linked-service"></a>연결된 서비스
연결 된 서비스를 집합 hello toodefine ODBC **형식** hello 연결 서비스 너무**OnPremisesOdbc**, 다음 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션:  

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| connectionString |hello 연결 문자열 및 선택적의 hello이 아닌 액세스 자격 증명 일부분 자격 증명을 암호화 합니다. Hello 다음 섹션의에서 예를 참조 합니다. |예 |
| 자격 증명 |hello 액세스 자격 증명 드라이버 관련 속성 값 형식으로 지정 하는 hello 연결 문자열의 부분입니다. 예: “Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”. |아니요 |
| authenticationType |Tooconnect toohello ODBC 데이터 저장소를 사용 하는 인증 유형입니다. 가능한 값은 익명 및 기본입니다. |예 |
| username |기본 인증을 사용하는 경우 사용자 이름을 지정합니다. |아니요 |
| 암호 |Hello 사용자 이름에 대해 지정한 사용자 계정에 hello에 대 한 암호를 지정 합니다. |아니요 |
| gatewayName |데이터 팩터리 서비스 hello hello 게이트웨이의 이름 tooconnect toohello ODBC 데이터 저장소를 사용 해야 합니다. |예 |

#### <a name="example---using-basic-authentication"></a>예제: 기본 인증 사용

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "OnPremisesOdbc",
        "typeProperties": {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```
#### <a name="example---using-basic-authentication-with-encrypted-credentials"></a>예제: 암호화된 자격 증명으로 기본 인증 사용
Hello를 사용 하 여 hello 자격 증명을 암호화할 수 [새로 AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (1.0 버전의 Azure PowerShell) cmdlet 또는 [New-azuredatafactoryencryptvalue](https://msdn.microsoft.com/library/dn834940.aspx) (0.9 또는 이전 버전의 hello Azure PowerShell)입니다.  

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "OnPremisesOdbc",
        "typeProperties": {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=myserver.database.windows.net; Database=TestDatabase;;EncryptedCredential=eyJDb25uZWN0...........................",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-using-anonymous-authentication"></a>예제: 익명 인증 사용

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "OnPremisesOdbc",
        "typeProperties": {
            "authenticationType": "Anonymous",
            "connectionString": "Driver={SQL Server};Server={servername}.database.windows.net; Database=TestDatabase;",
            "credential": "UID={uid};PWD={pwd}",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

자세한 내용은 [ODBC 커넥터](data-factory-odbc-connector.md#linked-service-properties) 문서를 참조하세요. 

### <a name="dataset"></a>데이터 집합
ODBC 데이터 집합, toodefine 집합 hello **형식** hello 데이터 집합의 너무**RelationalTable**, hello 다음과 같은 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션: 

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| tableName |Hello ODBC 데이터 저장소의 hello 테이블의 이름입니다. |예 |


#### <a name="example"></a>예제

```json
{
    "name": "ODBCDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "ODBCLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

자세한 내용은 [ODBC 커넥터](data-factory-odbc-connector.md#dataset-properties) 문서를 참조하세요. 

### <a name="relational-source-in-copy-activity"></a>복사 활동의 Relational 소스
ODBC 데이터 저장소에서 데이터를 복사 하는 경우 설정 hello **소스 형식** hello의 복사 작업이 너무**RelationalSource**, 다음 hello에 대 한 속성을 지정 하 고 **소스** 섹션 내용

| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| 쿼리 |사용자 지정 쿼리 tooread 데이터 hello를 사용 합니다. |SQL 쿼리 문자열. 예: `select * from MyTable` |예 |

#### <a name="example"></a>예제

```json
{
    "name": "CopyODBCToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "OdbcDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobOdbcDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "OdbcToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
``` 

자세한 내용은 [ODBC 커넥터](data-factory-odbc-connector.md#copy-activity-properties) 문서를 참조하세요.

## <a name="salesforce"></a>Salesforce


### <a name="linked-service"></a>연결된 서비스
연결 된 서비스를 집합 hello toodefine Salesforce **형식** hello 연결 서비스 너무**Salesforce**, 다음 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션:  

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| environmentUrl | Hello URL의 Salesforce 인스턴스를 지정 합니다. <br><br> -기본값은 " https://login.salesforce.com " 입니다. <br> -toocopy 데이터로 샌드박스 "https://test.salesforce.com"를 지정 합니다. <br> -사용자 지정 도메인에서 toocopy 데이터 지정, 예를 들어 "https://[domain].my.salesforce.com"입니다. |아니요 |
| username |Hello 사용자 계정에 대 한 사용자 이름을 지정 합니다. |예 |
| 암호 |Hello 사용자 계정의 암호를 지정 합니다. |예 |
| securityToken |Hello 사용자 계정에 대 한 보안 토큰을 지정 합니다. 참조 [보안 토큰 가져오기](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) 방법에 대 한 보안 토큰 tooreset/get입니다. 보안 토큰에 대 한 toolearn 일반적으로 참조 [보안과 hello API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm)합니다. |예 |

#### <a name="example"></a>예제

```json
{
    "name": "SalesforceLinkedService",
    "properties": {
        "type": "Salesforce",
        "typeProperties": {
            "username": "<user name>",
            "password": "<password>",
            "securityToken": "<security token>"
        }
    }
}
```

자세한 내용은 [Salesforce 커넥터](data-factory-salesforce-connector.md#linked-service-properties) 문서를 참조하세요. 

### <a name="dataset"></a>데이터 집합
Salesforce 데이터 집합을 toodefine 집합 hello **형식** hello 데이터 집합의 너무**RelationalTable**, hello 다음과 같은 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션: 

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| tableName |Salesforce에 hello 테이블의 이름입니다. |아니요(**RelationalSource**의 **query**가 지정된 경우) |

#### <a name="example"></a>예제

```json
{
    "name": "SalesforceInput",
    "properties": {
        "linkedServiceName": "SalesforceLinkedService",
        "type": "RelationalTable",
        "typeProperties": {
            "tableName": "AllDataType__c"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

자세한 내용은 [Salesforce 커넥터](data-factory-salesforce-connector.md#dataset-properties) 문서를 참조하세요. 

### <a name="relational-source-in-copy-activity"></a>복사 활동의 Relational 소스
Salesforce 로부터 데이터를 복사 하는 경우 설정 hello **소스 형식** hello의 복사 작업이 너무**RelationalSource**, 다음 hello에 대 한 속성을 지정 하 고 **소스** 섹션 내용

| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| 쿼리 |사용자 지정 쿼리 tooread 데이터 hello를 사용 합니다. |SQL-92 쿼리 또는 [SOQL(Salesforce Object Query Language)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) 쿼리입니다. 예제: `select * from MyTable__c` |더 (경우 hello **tableName** 의 hello **dataset** 지정) |

#### <a name="example"></a>예제  



```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "SalesforceToAzureBlob",
            "description": "Copy from Salesforce tooan Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "SalesforceInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "SELECT Id, Col_AutoNumber__c, Col_Checkbox__c, Col_Currency__c, Col_Date__c, Col_DateTime__c, Col_Email__c, Col_Number__c, Col_Percent__c, Col_Phone__c, Col_Picklist__c, Col_Picklist_MultiSelect__c, Col_Text__c, Col_Text_Area__c, Col_Text_AreaLong__c, Col_Text_AreaRich__c, Col_URL__c, Col_Text_Encrypt__c, Col_Lookup__c FROM AllDataType__c"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

> [!IMPORTANT]
> 모든 사용자 지정 개체에 대 한 hello "__c" hello API 이름 부분이 필요 합니다.

자세한 내용은 [Salesforce 커넥터](data-factory-salesforce-connector.md#copy-activity-properties) 문서를 참조하세요. 

## <a name="web-data"></a>웹 데이터 

### <a name="linked-service"></a>연결된 서비스
연결 된 서비스를 집합 hello toodefine 웹 **형식** hello 연결 서비스 너무**웹**, 다음 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션:  

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| Url |URL toohello 웹 소스 |예 |
| authenticationType |익명 |예 |
 

#### <a name="example"></a>예제


```json
{
    "name": "web",
    "properties": {
        "type": "Web",
        "typeProperties": {
            "authenticationType": "Anonymous",
            "url": "https://en.wikipedia.org/wiki/"
        }
    }
}
```

자세한 내용은 [웹 테이블 커넥터](data-factory-web-table-connector.md#linked-service-properties) 문서를 참조하세요. 

### <a name="dataset"></a>데이터 집합
toodefine 웹 dataset 집합 hello **형식** hello 데이터 집합의 너무**WebTable**, hello 다음과 같은 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션: 

| 속성 | 설명 | 필수 |
|:--- |:--- |:--- |
| type |hello 데이터 집합의 형식입니다. 너무 설정 되어 있어야**WebTable** |예 |
| path |상대 URL toohello 리소스 hello 테이블을 포함 합니다. |아니요. 경로 지정 하지 않으면 hello 연결 된 서비스 정의에 지정 된 유일한 hello URL 사용 됩니다. |
| index |hello 리소스에 대 한 hello 테이블의 hello 인덱스입니다. 참조 [HTML 페이지에 테이블의 Get 인덱스](#get-index-of-a-table-in-an-html-page) 단계 toogetting 인덱스에 대 한 HTML 페이지에 테이블의 섹션입니다. |예 |

#### <a name="example"></a>예제

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": "WebLinkedService",
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

자세한 내용은 [웹 테이블 커넥터](data-factory-web-table-connector.md#dataset-properties) 문서를 참조하세요. 

### <a name="web-source-in-copy-activity"></a>복사 활동의 웹 소스
웹 테이블에서 데이터를 복사 하는 경우 설정 hello **소스 형식** hello의 복사 작업이 너무**WebSource**합니다. 현재 복사 작업에서 hello 소스 경우 형식의 **WebSource**, 추가 속성이 지원 됩니다.

#### <a name="example"></a>예제

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "WebTableToAzureBlob",
            "description": "Copy from a Web table tooan Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "WebTableInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "WebSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

자세한 내용은 [웹 테이블 커넥터](data-factory-web-table-connector.md#copy-activity-properties) 문서를 참조하세요. 

## <a name="compute-environments"></a>계산 환경
hello 다음 표에 나열 hello 계산 환경에서 실행할 수 있는 Data Factory와 hello 변환 활동에서 지원 합니다. hello 계산에 대 한 hello 링크를 클릭에 관심이 toosee toolink 연결 된 서비스에 대 한 JSON 스키마를 hello 것 tooa 데이터 팩터리입니다. 

| 컴퓨팅 환경 | 활동 |
| --- | --- |
| [주문형 HDInsight 클러스터](#on-demand-azure-hdinsight-cluster) 또는 [사용자 고유의 HDInsight 클러스터](#existing-azure-hdinsight-cluster) |[.NET 사용자 지정 활동](#net-custom-activity), [Hive 활동](#hdinsight-hive-activity), [Pig 활동](#hdinsight-pig-activity), [MapReduce 활동](#hdinsight-mapreduce-activity), [Hadoop 스트리밍 활동](#hdinsight-streaming-activityd), [Spark 활동](#hdinsight-spark-activity) |
| [Azure 배치](#azure-batch) |[.NET 사용자 지정 작업](#net-custom-activity) |
| [Azure 기계 학습](#azure-machine-learning) | [Machine Learning 배치 실행 활동](#machine-learning-batch-execution-activity), [Machine Learning 업데이트 리소스 활동](#machine-learning-update-resource-activity) |
| [Azure 데이터 레이크 분석](#azure-data-lake-analytics) |[데이터 레이크 분석 U-SQL](#data-lake-analytics-u-sql-activity) |
| [Azure SQL Database](#azure-sql-database-1), [Azure SQL Data Warehouse](#azure-sql-data-warehouse-1), [SQL Server](#sql-server-1) |[저장 프로시저](#stored-procedure-activity) |

## <a name="on-demand-azure-hdinsight-cluster"></a>주문형 Azure HDInsight 클러스터
hello Azure 데이터 팩터리 서비스는 Windows/Linux 기반에 주문형 HDInsight 클러스터 tooprocess 데이터를 자동으로 만들 수 있습니다. hello 클러스터 hello hello 클러스터와 연결 된 hello 저장소 계정 (hello JSON의에서 linkedServiceName 속성)와 동일한 지역에에서 생성 됩니다. Hello에 나오는 변환 작업에 따라이 연결 된 서비스를 실행할 수 있습니다: [.NET 사용자 지정 활동](#net-custom-activity), [활동 하이브](#hdinsight-hive-activity), [활동 Pig] (#hdinsight pig-작업, [MapReduce 작업 ](#hdinsight-mapreduce-activity), [Hadoop 스트리밍 작업](#hdinsight-streaming-activityd), [활동 멤버](#hdinsight-spark-activity)합니다. 

### <a name="linked-service"></a>연결된 서비스 
다음 표에서 hello 주문형 HDInsight 연결 된 서비스의 hello Azure JSON 정의에서 사용 되는 hello 속성에 대 한 설명을 제공 합니다.

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| type |너무 hello 유형 속성을 설정 해야**HDInsightOnDemand**합니다. |예 |
| clusterSize |Hello 클러스터의 작업자/데이터 노드 수입니다. hello HDInsight 클러스터는 헤드 노드 hello이이 속성에 대해 지정 하는 작업자 노드 수와 함께 2으로 생성 됩니다. hello 노드는 크기는 4 작업자 노드 클러스터는 24 코어 4 개 코어에 Standard_D3 (4\*작업자 노드 + 2에 대 한 4 = 16 코어가\*헤드 노드에 대 한 4 = 8 코어). 참조 [HDInsight 클러스터를 만드는 Linux 기반 Hadoop](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md) hello Standard_D3 계층에 대 한 세부 정보에 대 한 합니다. |예 |
| timetolive |hello는 hello 주문형 HDInsight 클러스터에 대 한 유휴 시간을 허용 합니다. 기간 hello 주문형 HDInsight 클러스터의 연결이 유지 hello 클러스터에 다른 활성 작업이 있는 경우 실행 작업을 완료 한 후 지정 합니다.<br/><br/>예를 들어 활동 실행 6 분 및 timetolive 않습니다 too5 분, 5 분 후 hello에 대 한 연결 유지 hello 클러스터 유지할 6 분의 처리를 실행 하는 hello 활동을 설정 합니다. Hello에서 처리 된를 실행 하는 다른 활동을 hello 6 분 창을 실행 하는 경우 동일한 클러스터입니다.<br/><br/>주문형 HDInsight 클러스터를 만드는 작업은 비용이 많이 드는 작업 (이 걸릴 수), 따라서 데이터 팩터리의 필요한 tooimprove 성능으로이 설정을 사용 하 여 주문형 HDInsight 클러스터를 다시 사용 하 여 합니다.<br/><br/>Timetolive 값 too0로 설정 하면 hello 클러스터 hello 활동 실행 처리 되는 즉시 삭제 됩니다. Hello에 다른 손을 높은 값을 설정 하는 경우 hello 클러스터 될 수 있습니다 유지 유휴 불필요 하 게 많은 비용이 발생 합니다. 따라서이 필요에 따라 hello 적절 한 값을 설정 하는 중요 합니다.<br/><br/>여러 파이프라인을 공유할 수 hello timetolive 속성 값이 적절 하 게 설정 하는 경우 hello 주문형 HDInsight 클러스터의 동일한 인스턴스에 hello |예 |
| 버전 |Hello HDInsight 클러스터의 버전입니다. 자세한 내용은 [Azure Data Factory에서 지원되는 HDInsight 버전](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory)을 참조하세요. |아니요 |
| linkedServiceName |Azure 저장소 연결 서비스 toobe를 저장 하 고 데이터 처리에 대 한 hello 주문형 클러스터에서 사용 합니다. <p>현재, hello 저장소로 Azure 데이터 레이크 저장소를 사용 하는 주문형 HDInsight 클러스터를 만들 수 없습니다. Azure 데이터 레이크 저장소에서 처리 하는 HDInsight에서 toostore hello 결과 데이터를 원하는 hello Azure Blob 저장소 toohello Azure 데이터 레이크 저장소에서에서 복사 작업 toocopy hello 데이터를 사용 합니다.</p>  | 예 |
| additionalLinkedServiceNames |HDInsight hello에 대 한 추가 저장소 계정을 연결 된 서비스 hello 데이터 팩터리 서비스에서 사용자 대신 등록할 수 있도록 지정 합니다. |아니요 |
| osType |운영 체제 유형입니다. 허용되는 값은 Windows(기본값) 및 Linux입니다. |아니요 |
| hcatalogLinkedServiceName |Azure SQL 연결의 hello 이름에 해당 지점 toohello HCatalog 데이터베이스를 서비스입니다. hello 주문형 HDInsight 클러스터는 hello metastore로 hello Azure SQL 데이터베이스를 사용 하 여 생성 됩니다. |아니요 |

### <a name="json-example"></a>JSON 예제
다음 JSON hello Linux 기반에 주문형 HDInsight 연결 된 서비스를 정의 합니다. hello 데이터 팩터리 서비스를 자동으로 만듭니다는 **Linux 기반** HDInsight 클러스터는 데이터 조각을 처리 하는 경우. 

```json
{
    "name": "HDInsightOnDemandLinkedService",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "linkedServiceName": "StorageLinkedService"
        }
    }
}
```

자세한 내용은 [계산 연결된 서비스](data-factory-compute-linked-services.md)을 참조하세요. 

## <a name="existing-azure-hdinsight-cluster"></a>기존 Azure HDInsight 클러스터
데이터 팩터리에 Azure HDInsight 연결 된 서비스 tooregister 고유한 HDInsight 클러스터를 만들 수 있습니다. Hello에 나오는 데이터 변환 작업에 따라이 연결 된 서비스를 실행할 수 있습니다: [.NET 사용자 지정 활동](#net-custom-activity), [활동 하이브](#hdinsight-hive-activity), [활동 Pig] (#hdinsight pig-작업, [MapReduce 활동](#hdinsight-mapreduce-activity), [Hadoop 스트리밍 작업](#hdinsight-streaming-activityd), [활동 멤버](#hdinsight-spark-activity)합니다. 

### <a name="linked-service"></a>연결된 서비스
다음 표에서 hello Azure HDInsight 연결 된 서비스의 hello Azure JSON 정의에서 사용 되는 hello 속성에 대 한 설명을 제공 합니다.

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| type |너무 hello 유형 속성을 설정 해야**HDInsight**합니다. |예 |
| clusterUri |hello hello HDInsight 클러스터의 URI입니다. |예 |
| username |Tooconnect tooan 기존 HDInsight 클러스터를 사용 하는 hello 사용자 toobe의 hello 이름을 지정 합니다. |예 |
| 암호 |Hello 사용자 계정의 암호를 지정 합니다. |예 |
| linkedServiceName | Hello HDInsight 클러스터의 hello toohello Azure blob 저장소를 참조 하는 Azure 저장소 연결 서비스의 이름을 사용 합니다. <p>현재 이 속성에 대한 Azure Data Lake Store 연결된 서비스를 지정할 수 없습니다. Hello HDInsight 클러스터에 데이터 레이크 저장소 액세스 toohello 경우 Hive/Pig 스크립트에서 hello Azure 데이터 레이크 저장소의에서 데이터를 액세스할 수 있습니다. </p>  |예 |

지원되는 HDInsight 클러스터 버전은 [지원되는 HDInsight 버전](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory)을 참조하세요. 

#### <a name="json-example"></a>JSON 예제

```json
{
    "name": "HDInsightLinkedService",
    "properties": {
        "type": "HDInsight",
        "typeProperties": {
            "clusterUri": " https://<hdinsightclustername>.azurehdinsight.net/",
            "userName": "admin",
            "password": "<password>",
            "linkedServiceName": "MyHDInsightStoragelinkedService"
        }
    }
}
```

## <a name="azure-batch"></a>Azure 배치
데이터 팩터리와 연결 된 Azure 배치 서비스 tooregister 가상 컴퓨터 (Vm)의 일괄 처리 풀을 만들 수 있습니다. Azure 일괄 처리 또는 Azure HDInsight를 사용하여 .NET 사용자 지정 활동을 실행할 수 있습니다. 이 연결된 서비스에서 [.NET 사용자 지정 활동](#net-custom-activity)을 실행할 수 있습니다. 

### <a name="linked-service"></a>연결된 서비스
다음 표에서 hello Azure 배치 연결 된 서비스의 hello Azure JSON 정의에서 사용 되는 hello 속성에 대 한 설명을 제공 합니다.

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| type |너무 hello 유형 속성을 설정 해야**AzureBatch**합니다. |예 |
| accountName |Azure 배치 계정 hello의 이름입니다. |예 |
| accessKey |Hello Azure 배치 계정에 대 한 액세스 키입니다. |예 |
| poolName |가상 컴퓨터의 hello 풀의 이름입니다. |예 |
| linkedServiceName |Hello이 Azure 배치 연결 된 서비스와 연결 된 Azure 저장소 연결 서비스의 이름입니다. 준비 파일에 대 한이 연결 된 서비스는 필요한 toorun hello 활동 및 hello 활동 실행 로그를 저장 합니다. |예 |


#### <a name="json-example"></a>JSON 예제

```json
{
    "name": "AzureBatchLinkedService",
    "properties": {
        "type": "AzureBatch",
        "typeProperties": {
            "accountName": "<Azure Batch account name>",
            "accessKey": "<Azure Batch account key>",
            "poolName": "<Azure Batch pool name>",
            "linkedServiceName": "<Specify associated storage linked service reference here>"
        }
    }
}
```

## <a name="azure-machine-learning"></a>Azure 기계 학습
기계 학습 일괄 점수 매기기 끝점용 데이터 팩터리에 Azure 기계 학습 연결 서비스 tooregister를 만듭니다. 이 연결된 서비스에서는 두 가지 데이터 변환 활동, 즉 [Machine Learning 배치 실행 활동](#machine-learning-batch-execution-activity)과, [Machine Learning 업데이트 리소스 활동](#machine-learning-update-resource-activity)을 실행할 수 있습니다. 

### <a name="linked-service"></a>연결된 서비스
다음 표에서 hello Azure 기계 학습 연결 서비스의 hello Azure JSON 정의에서 사용 되는 hello 속성에 대 한 설명을 제공 합니다.

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| 형식 |hello type 속성이로 설정 해야: **AzureML**합니다. |예 |
| mlEndpoint |hello 일괄 처리 첨 수 매기기 URL입니다. |예 |
| apiKey |hello 작업 영역 모델의 API를 게시 합니다. |예 |

#### <a name="json-example"></a>JSON 예제

```json
{
    "name": "AzureMLLinkedService",
    "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://[batch scoring endpoint]/jobs",
            "apiKey": "<apikey>"
        }
    }
}
```

## <a name="azure-data-lake-analytics"></a>Azure 데이터 레이크 분석
만들 프로그램 **Azure 데이터 레이크 분석** hello를 사용 하기 전에 서비스 toolink Azure Data Lake 분석 계산 서비스 tooan Azure 데이터 팩터리에 연결 [데이터 레이크 분석 U-SQL 작업](data-factory-usql-activity.md) 파이프라인에서 .

### <a name="linked-service"></a>연결된 서비스

다음 표에서 hello 연결 된 Azure Data Lake 분석 서비스의 hello JSON 정의에서 사용 되는 hello 속성에 대 한 설명을 제공 합니다. 

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| 형식 |hello type 속성이로 설정 해야: **AzureDataLakeAnalytics**합니다. |예 |
| accountName |Azure 데이터 레이크 분석 계정 이름입니다. |예 |
| dataLakeAnalyticsUri |Azure 데이터 레이크 분석 URI입니다. |아니요 |
| 권한 부여 |인증 코드를 클릭 한 후 자동으로 검색 됩니다 **Authorize** hello 데이터 팩터리 편집기 및 완료 hello OAuth 로그인 단추입니다. |예 |
| subscriptionId |Azure 구독 ID |아니요 (지정 하지 않으면 데이터 팩터리에 사용 되는 hello의 구독) 하는 경우. |
| resourceGroupName |Azure 리소스 그룹 이름 |아니요 (지정 하지 않으면 리소스 그룹의 데이터 팩터리에 사용 되는 hello) 하는 경우. |
| sessionId |hello OAuth 권한 부여 세션에서 세션 id입니다. 각 세션 ID는 고유하고 한 번만 사용될 수 있으며  이 ID는 hello 데이터 팩터리 편집기를 사용 하면 자동으로 생성 합니다. |예 |


#### <a name="json-example"></a>JSON 예제
다음 예에서는 hello 연결 된 Azure Data Lake 분석 서비스에 대 한 JSON 정의 제공 합니다.

```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "<account name>",
            "dataLakeAnalyticsUri": "datalakeanalyticscompute.net",
            "authorization": "<authcode>",
            "sessionId": "<session ID>",
            "subscriptionId": "<subscription id>",
            "resourceGroupName": "<resource group name>"
        }
    }
}
```

## <a name="azure-sql-database"></a>Azure SQL Database
Azure SQL 연결 서비스를 만들고 사용 하 여 hello로 [저장 프로시저 작업](#stored-procedure-activity) tooinvoke 데이터 팩토리 파이프라인에서 저장된 프로시저입니다. 

### <a name="linked-service"></a>연결된 서비스
toodefine Azure SQL 데이터베이스에 연결 된 서비스를 집합 hello **형식** hello 연결 서비스 너무**AzureSqlDatabase**, 다음 hello에 대 한 속성을 지정 하 고 **typeProperties**섹션:  

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| connectionString |Hello connectionString 속성에 대 한 tooconnect toohello Azure SQL 데이터베이스 인스턴스는 데 필요한 정보를 지정 합니다. |예 |

#### <a name="json-example"></a>JSON 예제

```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

이 연결된 서비스에 대한 자세한 내용은 [Azure SQL 커넥터](data-factory-azure-sql-connector.md#linked-service-properties) 문서를 참조하세요.

## <a name="azure-sql-data-warehouse"></a>Azure SQL 데이터 웨어하우스
Azure SQL 데이터 웨어하우스 연결 된 서비스를 만들고 사용 하 여 hello로 [저장 프로시저 작업](data-factory-stored-proc-activity.md) tooinvoke 데이터 팩토리 파이프라인에서 저장된 프로시저입니다. 

### <a name="linked-service"></a>연결된 서비스
연결 된 서비스를 집합 hello Azure SQL 데이터 웨어하우스 toodefine **형식** hello 연결 서비스 너무**AzureSqlDW**, 다음 hello에 대 한 속성을 지정 하 고 **typeProperties**섹션:  

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| connectionString |Hello connectionString 속성에 대 한 tooconnect toohello Azure SQL 데이터 웨어하우스 인스턴스는 데 필요한 정보를 지정 합니다. |예 |

#### <a name="json-example"></a>JSON 예제

```json
{
    "name": "AzureSqlDWLinkedService",
    "properties": {
        "type": "AzureSqlDW",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

자세한 내용은 [Azure SQL Data Warehouse 커넥터](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) 문서를 참조하세요. 

## <a name="sql-server"></a>SQL Server 
SQL Server 연결 된 서비스를 만들고 사용 하 여 hello로 [저장 프로시저 작업](data-factory-stored-proc-activity.md) tooinvoke 데이터 팩토리 파이프라인에서 저장된 프로시저입니다. 

### <a name="linked-service"></a>연결된 서비스
형식의 연결 된 서비스를 만들면 **OnPremisesSqlServer** toolink 온-프레미스 SQL Server 데이터베이스 tooa 데이터 팩터리입니다. 다음 표에서 hello JSON 요소 특정 tooon 온-프레미스 SQL Server 연결 된 서비스에 대 한 설명을 제공 합니다.

다음 표에서 hello JSON 요소 특정 tooSQL 연결 된 서버 서비스에 대 한 설명을 제공 합니다.

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| type |hello type 속성이로 설정 해야: **OnPremisesSqlServer**합니다. |예 |
| connectionString |SQL 인증 또는 Windows 인증을 사용 하 여 tooconnect toohello 온-프레미스 SQL Server 데이터베이스는 데 필요한 connectionString 정보를 지정 합니다. |예 |
| gatewayName |데이터 팩터리 서비스 hello hello 게이트웨이의 이름 tooconnect toohello 온-프레미스 SQL Server 데이터베이스를 사용 해야 합니다. |예 |
| username |Windows 인증을 사용하는 경우 사용자 이름을 지정합니다. 예: **domainname\\username**. |아니요 |
| 암호 |Hello 사용자 이름에 대해 지정한 사용자 계정에 hello에 대 한 암호를 지정 합니다. |아니요 |

Hello를 사용 하 여 자격 증명을 암호화할 수 **새로 AzureRmDataFactoryEncryptValue** cmdlet hello 다음 예제와 같이 hello 연결 문자열에서 사용 하 고 (**EncryptedCredential** 속성):  

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```


#### <a name="example-json-for-using-sql-authentication"></a>예제: SQL 인증을 사용하는 JSON

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
#### <a name="example-json-for-using-windows-authentication"></a>예제: Windows 인증을 사용하는 JSON

사용자 이름 및 암호를 지정 하는 경우 게이트웨이에서 사용 하 여 해당 tooimpersonate hello 지정 된 사용자 계정 tooconnect toohello 온-프레미스 SQL Server 데이터베이스입니다. 그렇지 않은 경우 게이트웨이 게이트웨이 (시작 계정)의 보안 컨텍스트 hello와 직접 toohello SQL Server를 연결합니다.

```json
{
    "Name": " MyOnPremisesSQLDB",
    "Properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "ConnectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=True;",
            "username": "<domain\\username>",
            "password": "<password>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

자세한 내용은 [SQL Server 커넥터](data-factory-sqlserver-connector.md#linked-service-properties) 문서를 참조하세요.

## <a name="data-transformation-activities"></a>데이터 변환 작업

작업 | 설명
-------- | -----------
[HDInsight Hive 활동](#hdinsight-hive-activity) | 데이터 팩터리 파이프라인에서 HDInsight Hive 활동 hello 하이브 쿼리를 직접 또는 요청 시 Windows/Linux 기반 HDInsight 클러스터를 실행합니다. 
[HDInsight Pig 활동](#hdinsight-pig-activity) | hello 데이터 팩터리 파이프라인에서 HDInsight Pig 작업을 직접 Pig 쿼리 또는 요청 시 Windows/Linux 기반 HDInsight 클러스터를 실행합니다.
[HDInsight MapReduce 작업](#hdinsight-mapreduce-activity) | 데이터 팩터리 파이프라인에서 HDInsight MapReduce 작업 hello MapReduce 프로그램을 직접 또는 요청 시 Windows/Linux 기반 HDInsight 클러스터를 실행합니다.
[HDInsight 스트리밍 작업](#hdinsight-streaming-activity) | 데이터 팩터리 파이프라인에서 HDInsight 스트리밍 활동 hello Hadoop 스트리밍 프로그램을 직접 또는 요청 시 Windows/Linux 기반 HDInsight 클러스터를 실행합니다.
[HDInsight Spark 작업](#hdinsight-spark-activity) | 데이터 팩터리 파이프라인에서 HDInsight Spark 활동 hello 고유한 HDInsight 클러스터에서 Spark 프로그램을 실행합니다. 
[Machine Learning Batch 실행 작업](#machine-learning-batch-execution-activity) | 웹 predictive analytics에 대해 서비스에 tooeasily 하면 게시 된 Azure 기계 학습을 사용 하는 파이프라인을 생성 하는 azure Data Factory 수 있습니다. Azure 데이터 팩터리 파이프라인에서 일괄 처리 실행 작업 hello를 사용 하 여 hello 데이터 일괄 처리에 대 한 기계 학습 웹 서비스 toomake 예측을 호출할 수 있습니다. 
[Machine Learning 업데이트 리소스 작업](#machine-learning-update-resource-activity) | 시간이 지남에 따라 hello 예측 모델 hello 점수 매기기 실험 toobe 다시 학습 되도록 new를 사용 하 여 필요한 기계 학습의에서 입력 데이터 집합입니다. 재교육를 완료 한 후 웹 서비스 hello와 점수 매기기 tooupdate hello 기계 학습 모델을 다시 학습 되도록 할 수 있습니다. Hello 새로 학습 모델로 hello 업데이트 리소스 작업 tooupdate hello 웹 서비스를 사용할 수 있습니다.
[저장 프로시저 작업](#stored-procedure-activity) | 데이터 팩터리 파이프라인 tooinvoke hello 데이터 저장소를 다음 중 하나에 있는 저장된 프로시저의에서 hello 저장 프로시저 작업을 사용할 수 있습니다: Azure SQL 데이터베이스, Azure SQL 데이터 웨어하우스, 기업 내에 SQL Server 데이터베이스 또는 Azure VM입니다. 
[Data Lake Analytics U-SQL 활동](#data-lake-analytics-u-sql-activity) | Data Lake Analytics U-SQL 작업은 Azure Data Lake Analytics 클러스터에 대해 U-SQL 스크립트를 실행합니다.  
[.NET 사용자 지정 작업](#net-custom-activity) | 데이터 팩터리에서 지원 되지 않는 방식으로 tootransform 데이터를 유지 해야 하는 경우 고유의 데이터 처리 논리와 사용자 지정 활동을 만들 있고 hello 파이프라인에서 hello 활동을 사용 합니다. Hello 사용자 지정.NET 작업 toorun Azure 배치 서비스 또는 Azure HDInsight 클러스터를 사용 하 여 구성할 수 있습니다. 

     
## <a name="hdinsight-hive-activity"></a>HDInsight Hive 작업
Hello 다음과 같은 Hive 활동 JSON 정의에서 속성을 지정할 수 있습니다. hello 활동에 대 한 hello type 속성 이어야 합니다: **HDInsightHive**합니다. HDInsight 연결 된 서비스를 먼저 만든 하 고 그의 hello 이름을 hello에 대 한 값으로 지정 해야 **linkedServiceName** 속성입니다. hello 다음 속성은 지원 hello **typeProperties** hello 유형의 활동 tooHDInsightHive 설정 섹션:

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| script |Hello Hive 스크립트를 인라인으로 지정 |아니요 |
| script path |저장소 hello 하이브 스크립트에는 Azure blob 저장소에 있으며 hello toohello 파일 경로 제공 합니다. 'script' 또는 'scriptPath' 속성을 사용합니다. 둘 모두를 사용할 수는 없습니다. hello 파일 이름은 대/소문자 구분입니다. |아니요 |
| defines |매개 변수를 'hiveconf'를 사용 하 여 hello 하이브 스크립트 내에서 참조 하는 것에 대 한 키/값 쌍으로 지정 |아니요 |

이러한 형식 속성은 특정 toohello Hive 활동입니다. Hello typeProperties 섹션) (외부 다른 속성은 모든 활동에 대해 지원 됩니다.   

### <a name="json-example"></a>JSON 예제
다음 JSON hello 파이프라인에서 HDInsight Hive 활동을 정의 합니다.  

```json
{
    "name": "Hive Activity",
    "description": "description",
    "type": "HDInsightHive",
    "inputs": [
      {
        "name": "input tables"
      }
    ],
    "outputs": [
      {
        "name": "output tables"
      }
    ],
    "linkedServiceName": "MyHDInsightLinkedService",
    "typeProperties": {
      "script": "Hive script",
      "scriptPath": "<pathtotheHivescriptfileinAzureblobstorage>",
      "defines": {
        "param1": "param1Value"
      }
    },
   "scheduler": {
      "frequency": "Day",
      "interval": 1
    }
}
```

자세한 내용은 [Hive 활동](data-factory-hive-activity.md)을 참조하세요. 

## <a name="hdinsight-pig-activity"></a>HDInsight Pig 작업
Hello 다음과 같은 Pig 작업 JSON 정의에서 속성을 지정할 수 있습니다. hello 활동에 대 한 hello type 속성 이어야 합니다: **HDInsightPig**합니다. HDInsight 연결 된 서비스를 먼저 만든 하 고 그의 hello 이름을 hello에 대 한 값으로 지정 해야 **linkedServiceName** 속성입니다. hello 다음 속성은 지원 hello **typeProperties** hello 유형의 활동 tooHDInsightPig 설정 섹션: 

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| script |Hello Pig 스크립트를 인라인으로 지정 |아니요 |
| script path |Azure blob 저장소에 hello Pig 스크립트를 저장 하 고 hello toohello 파일 경로 제공 합니다. 'script' 또는 'scriptPath' 속성을 사용합니다. 둘 모두를 사용할 수는 없습니다. hello 파일 이름은 대/소문자 구분입니다. |아니요 |
| defines |키/값 쌍으로 hello Pig 스크립트 내에서 참조 하는 것에 대 한 매개 변수를 지정 |아니요 |

이러한 형식 속성은 특정 toohello Pig 작업입니다. Hello typeProperties 섹션) (외부 다른 속성은 모든 활동에 대해 지원 됩니다.   

### <a name="json-example"></a>JSON 예제

```json
{
    "name": "HiveActivitySamplePipeline",
      "properties": {
    "activities": [
        {
            "name": "Pig Activity",
            "description": "description",
            "type": "HDInsightPig",
            "inputs": [
                  {
                    "name": "input tables"
                  }
            ],
            "outputs": [
                  {
                    "name": "output tables"
                  }
            ],
            "linkedServiceName": "MyHDInsightLinkedService",
            "typeProperties": {
                  "script": "Pig script",
                  "scriptPath": "<pathtothePigscriptfileinAzureblobstorage>",
                  "defines": {
                    "param1": "param1Value"
                  }
            },
               "scheduler": {
                  "frequency": "Day",
                  "interval": 1
            }
          }
    ]
  }
}
```

자세한 내용은 [Pig 활동](#data-factory-pig-activity.md)을 참조하세요. 

## <a name="hdinsight-mapreduce-activity"></a>HDInsight MapReduce 작업
Hello 다음과 같은 MapReduce 작업 JSON 정의에서 속성을 지정할 수 있습니다. hello 활동에 대 한 hello type 속성 이어야 합니다: **HDInsightMapReduce**합니다. HDInsight 연결 된 서비스를 먼저 만든 하 고 그의 hello 이름을 hello에 대 한 값으로 지정 해야 **linkedServiceName** 속성입니다. hello 다음 속성은 지원 hello **typeProperties** hello 유형의 활동 tooHDInsightMapReduce 설정 섹션: 

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| jarLinkedService | Hello hello JAR 파일을 포함 하는 Azure 저장소에 대 한 서비스 연결 된 하는 hello의 이름입니다. | 예 |
| jarFilePath  | Hello Azure 저장소에서에서 toohello JAR 파일 경로입니다. | 예 | 
| className | Hello hello JAR 파일의 기본 클래스의 이름입니다. | 예 | 
| arguments | Hello MapReduce 프로그램에 대 한 쉼표로 구분 된 인수 목록입니다. 런타임 시 몇 가지 추가 인수 표시 (예: mapreduce.job.tags) hello MapReduce 프레임 워크에서. toodifferentiate hello MapReduce 인수, 인수 hello 다음 예제와 같이 인수로 옵션과 값을 사용 하십시오 (-s-입력,-등에서 출력은 바로 뒤에 해당 값으로 옵션) | 아니요 | 

### <a name="json-example"></a>JSON 예제

```json
{
    "name": "MahoutMapReduceSamplePipeline",
    "properties": {
        "description": "Sample Pipeline tooRun a Mahout Custom Map Reduce Jar. This job calculates an Item Similarity Matrix toodetermine hello similarity between two items",
        "activities": [
            {
                "type": "HDInsightMapReduce",
                "typeProperties": {
                    "className": "org.apache.mahout.cf.taste.hadoop.similarity.item.ItemSimilarityJob",
                    "jarFilePath": "adfsamples/Mahout/jars/mahout-examples-0.9.0.2.2.7.1-34.jar",
                    "jarLinkedService": "StorageLinkedService",
                    "arguments": ["-s", "SIMILARITY_LOGLIKELIHOOD", "--input", "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/input", "--output", "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/output/", "--maxSimilaritiesPerItem", "500", "--tempDir", "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/temp/mahout"]
                },
                "inputs": [
                    {
                        "name": "MahoutInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "MahoutOutput"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "MahoutActivity",
                "description": "Custom Map Reduce toogenerate Mahout result",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-01-03T00:00:00",
        "end": "2017-01-04T00:00:00"
    }
}
```

자세한 내용은 [MapReduce 활동](data-factory-map-reduce.md)을 참조하세요. 

## <a name="hdinsight-streaming-activity"></a>HDInsight 스트리밍 작업
Hello 다음과 같은 Hadoop 스트리밍 작업 JSON 정의에서 속성을 지정할 수 있습니다. hello 활동에 대 한 hello type 속성 이어야 합니다: **HDInsightStreaming**합니다. HDInsight 연결 된 서비스를 먼저 만든 하 고 그의 hello 이름을 hello에 대 한 값으로 지정 해야 **linkedServiceName** 속성입니다. hello 다음 속성은 지원 hello **typeProperties** hello 유형의 활동 tooHDInsightStreaming 설정 섹션: 

| 속성 | 설명 | 
| --- | --- |
| mapper | Hello 매퍼 실행 파일의 이름입니다. Hello 예제 cat.exe는 hello 매퍼 실행 파일입니다.| 
| reducer | Hello 리 듀 서 실행 파일의 이름입니다. Hello 예제 wc.exe는 hello 리 듀 서 실행 합니다. | 
| input | 입력된 파일 (위치) hello 맵 편집기에 대 한 합니다. Hello 예에서: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample이 blob 컨테이너 hello, 예제/data/Gutenberg hello 폴더 이며 davinci.txt가 blob hello 합니다. |
| output | 출력 파일 위치 등 hello 리 듀 서에 대 한 합니다. hello Hadoop 스트리밍 작업의 hello 출력은이 속성에 지정 된 toohello 위치를 기록 합니다. |
| filePaths | Hello 매퍼 및 리 듀 서 실행 파일에 대 한 경로입니다. Hello 예에서: "adfsample/example/apps/wc.exe" adfsample이 blob 컨테이너 hello, example/apps가 hello 폴더 및 wc.exe는 hello를 실행 합니다. | 
| fileLinkedService | Hello hello filePaths 섹션에 지정 된 hello 파일이 포함 된 Azure 저장소를 나타내는 azure 저장소 연결 된 서비스입니다. | 
| arguments | Hello MapReduce 프로그램에 대 한 쉼표로 구분 된 인수 목록입니다. 런타임 시 몇 가지 추가 인수 표시 (예: mapreduce.job.tags) hello MapReduce 프레임 워크에서. toodifferentiate hello MapReduce 인수, 인수 hello 다음 예제와 같이 인수로 옵션과 값을 사용 하십시오 (-s-입력,-등에서 출력은 바로 뒤에 해당 값으로 옵션) | 
| getDebugInfo | 선택적 요소입니다. TooFailure, 설정 되 면 hello 로그 오류에 대해서만 다운로드 됩니다. TooAll, 설정 되어 있는 경우 로그 hello 실행 상태에 관계 없이 항상 다운로드 됩니다. | 

> [!NOTE]
> Hello에 대 한 hello Hadoop 스트리밍 작업에 대 한 출력 데이터 집합을 지정 해야 **출력** 속성입니다. 이 데이터 집합에만 dummy 하는 데이터 집합은 필요한 toodrive hello 파이프라인 일정 (시간별, 일별, 등) 수 있습니다. Hello 활동 입력을 사용 하지 않습니다, hello에 대 한 hello 활동에 대 한 입력된 데이터 집합 지정 건너뛸 수 있습니다 **입력** 속성입니다.  

## <a name="json-example"></a>JSON 예제

```json
{
    "name": "HadoopStreamingPipeline",
    "properties": {
        "description": "Hadoop Streaming Demo",
        "activities": [
            {
                "type": "HDInsightStreaming",
                "typeProperties": {
                    "mapper": "cat.exe",
                    "reducer": "wc.exe",
                    "input": "wasb://<nameofthecluster>@spestore.blob.core.windows.net/example/data/gutenberg/davinci.txt",
                    "output": "wasb://<nameofthecluster>@spestore.blob.core.windows.net/example/data/StreamingOutput/wc.txt",
                    "filePaths": ["<nameofthecluster>/example/apps/wc.exe","<nameofthecluster>/example/apps/cat.exe"],
                    "fileLinkedService": "StorageLinkedService",
                    "getDebugInfo": "Failure"
                },
                "outputs": [
                    {
                        "name": "StreamingOutputDataset"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "RunHadoopStreamingJob",
                "description": "Run a Hadoop streaming job",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2014-01-04T00:00:00",
        "end": "2014-01-05T00:00:00"
    }
}
```

자세한 내용은 [Hadoop 스트리밍 활동](data-factory-hadoop-streaming-activity.md) 문서를 참조하세요. 

## <a name="hdinsight-spark-activity"></a>HDInsight Spark 작업
Hello 다음과 같은 Spark 활동 JSON 정의에서 속성을 지정할 수 있습니다. hello 활동에 대 한 hello type 속성 이어야 합니다: **HDInsightSpark**합니다. HDInsight 연결 된 서비스를 먼저 만든 하 고 그의 hello 이름을 hello에 대 한 값으로 지정 해야 **linkedServiceName** 속성입니다. hello 다음 속성은 지원 hello **typeProperties** hello 유형의 활동 tooHDInsightSpark 설정 섹션: 

| 속성 | 설명 | 필수 |
| -------- | ----------- | -------- |
| rootPath | hello Azure Blob 컨테이너 및 hello Spark 파일이 있는 폴더입니다. hello 파일 이름은 대/소문자 구분입니다. | 예 |
| entryFilePath | Hello Spark 코드/패키지의 상대 경로 toohello 루트 폴더입니다. | 예 |
| className | 응용 프로그램의 Java/Spark main 클래스 | 아니요 | 
| arguments | 명령줄 인수 toohello Spark 프로그램의 목록입니다. | 아니요 | 
| proxyUser | hello 사용자 계정 tooimpersonate tooexecute hello Spark 프로그램 | 아니요 | 
| sparkConfig | Spark 구성 속성입니다. | 아니요 | 
| getDebugInfo | Hello Spark 로그 파일에서 복사한 toohello HDInsight 클러스터에서 사용 하는 Azure 저장소를가 하는 경우를 지정 합니다 (또는) sparkJobLinkedService 하 여 지정 합니다. 허용되는 값: None, Always 또는 Failure. 기본값: None. | 아니요 | 
| sparkJobLinkedService | hello hello Spark 작업 파일, 종속성 및 로그를 보유 하는 Azure 저장소 연결 된 서비스입니다.  이 속성에 대 한 값을 지정 하지 않으면 HDInsight 클러스터와 연결 된 hello 저장소 사용 됩니다. | 아니요 |

### <a name="json-example"></a>JSON 예제

```json
{
    "name": "SparkPipeline",
    "properties": {
        "activities": [
            {
                "type": "HDInsightSpark",
                "typeProperties": {
                    "rootPath": "adfspark\\pyFiles",
                    "entryFilePath": "test.py",
                    "getDebugInfo": "Always"
                },
                "outputs": [
                    {
                        "name": "OutputDataset"
                    }
                ],
                "name": "MySparkActivity",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-02-05T00:00:00",
        "end": "2017-02-06T00:00:00"
    }
}
```
포인트 다음 참고 hello: 

- hello **형식** 너무 속성이**HDInsightSpark**합니다.
- hello **rootPath** 너무 설정**adfspark\\pyFiles** adfspark 란 pyFiles 고 hello Azure Blob 컨테이너는 세밀 하 게 폴더 해당 컨테이너에 있습니다. 이 예제에서는 hello Azure Blob 저장소는 hello 즉 hello Spark 클러스터와 연결 합니다. Hello 파일 tooa 업로드할 수 있습니다 다른 Azure 저장소입니다. 이렇게 하면 Azure 저장소 연결 서비스 toolink 해당 저장소 계정 toohello 데이터 팩터리를 만듭니다. 그런 다음 hello 연결 된 서비스의 hello 이름을 hello에 대 한 값으로 지정 **sparkJobLinkedService** 속성입니다. 참조 [Spark 활동 속성](#spark-activity-properties) hello Spark 활동에서 지 원하는 다른 속성 및이 속성에 대 한 세부 정보에 대 한 합니다.
- hello **entryFilePath** toohello 설정 **test.py**, hello python 파일인 합니다. 
- hello **getDebugInfo** 너무 속성이**항상**, (성공 또는 실패) 생성 된 hello 로그 파일은 항상 의미 합니다.  

    > [!IMPORTANT]
    > 설정 하지 않으면이 속성 tooAlways 프로덕션 환경에서 문제를 해결 하는 경우가 아니면 하는 것이 좋습니다. 
- hello **출력** 섹션에는 하나의 출력 데이터 집합에 포함 합니다. Hello spark 프로그램 출력을 생성 하지 않는 경우에 출력 데이터 집합을 지정 해야 합니다. hello 출력 데이터 집합 드라이브 hello에 대 한 일정 hello 파이프라인 (시간별, 일별, 등).

Hello 활동에 대 한 자세한 내용은 참조 [Spark 활동](data-factory-spark.md) 문서.  

## <a name="machine-learning-batch-execution-activity"></a>Machine Learning Batch 실행 작업
Hello 다음과 같은 Azure ML 일괄 처리 실행 활동 JSON 정의에서 속성을 지정할 수 있습니다. hello 활동에 대 한 hello type 속성 이어야 합니다: **AzureMLBatchExecution**합니다. Azure 기계 학습 연결 된 서비스를 먼저 만들고 것의 hello 이름을 hello에 대 한 값으로 지정 해야 **linkedServiceName** 속성입니다. hello 다음 속성은 지원 hello **typeProperties** hello 유형의 활동 tooAzureMLBatchExecution 설정 섹션:

속성 | 설명 | 필수 
-------- | ----------- | --------
webServiceInput | 데이터 집합 toobe hello hello Azure ML 웹 서비스에 대 한 입력으로 전달 합니다. 이 데이터 집합 hello 활동에 대 한 hello 입력에 포함 되어야 합니다. |webServiceInput 또는 webServiceInputs를 사용합니다. | 
webServiceInputs | Hello Azure ML 웹 서비스에 대 한 입력으로 전달 되는 데이터 집합 toobe를 지정 합니다. Hello 웹 서비스는 여러 개의 입력을 hello webServiceInput 속성을 사용 하는 대신 hello webServiceInputs 속성을 사용 합니다. Hello에서 참조 되는 데이터 집합 **webServiceInputs** hello 활동에에서도 포함 해야 **입력**합니다. | webServiceInput 또는 webServiceInputs를 사용합니다. | 
webServiceOutputs | hello Azure ML 웹 서비스에 대 한 출력으로 할당 된 hello 데이터 집합입니다. hello 웹 서비스는이 데이터 집합에 출력 데이터를 반환합니다. | 예 | 
globalParameters | 이 섹션의 웹 서비스 매개 변수가 hello에 대 한 값을 지정 합니다. | 아니요 | 

### <a name="json-example"></a>JSON 예제
이 예제에서는 hello 활동에 데이터 집합이 두 hello **MLSqlInput** 입력으로 및 **MLSqlOutput** hello 출력으로 합니다. hello **MLSqlInput** hello를 사용 하 여 입력된 toohello 웹 서비스로 전달 되 **webServiceInput** JSON 속성입니다. hello **MLSqlOutput** hello를 사용 하 여 출력 toohello 웹 서비스로 전달 되 **webServiceOutputs** JSON 속성입니다. 

```json
{
   "name": "MLWithSqlReaderSqlWriter",
   "properties": {
      "description": "Azure ML model with sql azure reader/writer",
      "activities": [{
         "name": "MLSqlReaderSqlWriterActivity",
         "type": "AzureMLBatchExecution",
         "description": "test",
         "inputs": [ { "name": "MLSqlInput" }],
         "outputs": [ { "name": "MLSqlOutput" } ],
         "linkedServiceName": "MLSqlReaderSqlWriterDecisionTreeModel",
         "typeProperties":
         {
            "webServiceInput": "MLSqlInput",
            "webServiceOutputs": {
               "output1": "MLSqlOutput"
            },
            "globalParameters": {
               "Database server name": "<myserver>.database.windows.net",
               "Database name": "<database>",
               "Server user account name": "<user name>",
               "Server user account password": "<password>"
            }              
         },
         "policy": {
            "concurrency": 1,
            "executionPriorityOrder": "NewestFirst",
            "retry": 1,
            "timeout": "02:00:00"
         }
      }],
      "start": "2016-02-13T00:00:00",
       "end": "2016-02-14T00:00:00"
   }
}
```

Hello Azure 컴퓨터 학습 웹 서비스에는 판독기와 기록기 모듈 tooread/쓰기 데이터를 사용 하 여 배포 된 hello JSON 예에서 / tooan Azure SQL 데이터베이스입니다. 이 웹 서비스는 hello 다음 4 개의 매개 변수가 노출: 데이터베이스 서버 이름, 데이터베이스 이름, 서버 사용자 계정 이름 및 서버 사용자 계정 암호입니다.

> [!NOTE]
> 유일한 입 / 출력 hello AzureMLBatchExecution 활동의 매개 변수 toohello 웹 서비스 변수로 전달할 수 있습니다. 예를 들어 JSON 코드 조각은 위에 hello, MLSqlInput은 입력된 toohello webServiceInput 매개 변수를 통해 웹 서비스는 입력된 toohello 변수로 전달 되는 AzureMLBatchExecution 활동에는 사용 합니다.

## <a name="machine-learning-update-resource-activity"></a>Machine Learning 업데이트 리소스 활동
Hello 다음과 같은 Azure ML 업데이트 리소스 작업 JSON 정의에서 속성을 지정할 수 있습니다. hello 활동에 대 한 hello type 속성 이어야 합니다: **AzureMLUpdateResource**합니다. Azure 기계 학습 연결 된 서비스를 먼저 만들고 것의 hello 이름을 hello에 대 한 값으로 지정 해야 **linkedServiceName** 속성입니다. hello 다음 속성은 지원 hello **typeProperties** hello 유형의 활동 tooAzureMLUpdateResource 설정 섹션:

속성 | 설명 | 필수 
-------- | ----------- | --------
trainedModelName | 모델을 유지 하는 hello의 이름입니다. | 예 |  
trainedModelDatasetName | Hello 재교육 작업에서 반환 된 포인팅 toohello iLearner 파일을 데이터 집합입니다. | 예 | 

### <a name="json-example"></a>JSON 예제
hello 파이프라인에는 두 개의 활동: **AzureMLBatchExecution** 및 **AzureMLUpdateResource**합니다. hello Azure ML 일괄 처리 실행 작업 hello 학습 데이터를 입력으로 사용 하 고 출력으로 iLearner 파일을 생성 합니다. hello 활동 데이터를 학습 하는 hello 입력이 포함 된 hello 학습 웹 서비스 (학습 실험을 웹 서비스로 노출)을 호출 하 고 hello 웹 서비스에서 hello ilearner 파일을 받습니다. hello placeholderBlob hello Azure Data Factory 서비스 toorun hello 파이프라인에 필요한 더미 출력 데이터 집합 뿐입니다.


```json
{
    "name": "pipeline",
    "properties": {
        "activities": [
            {
                "name": "retraining",
                "type": "AzureMLBatchExecution",
                "inputs": [
                    {
                        "name": "trainingData"
                    }
                ],
                "outputs": [
                    {
                        "name": "trainedModelBlob"
                    }
                ],
                "typeProperties": {
                    "webServiceInput": "trainingData",
                    "webServiceOutputs": {
                        "output1": "trainedModelBlob"
                    }              
                 },
                "linkedServiceName": "trainingEndpoint",
                "policy": {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "02:00:00"
                }
            },
            {
                "type": "AzureMLUpdateResource",
                "typeProperties": {
                    "trainedModelName": "trained model",
                    "trainedModelDatasetName" :  "trainedModelBlob"
                },
                "inputs": [{ "name": "trainedModelBlob" }],
                "outputs": [{ "name": "placeholderBlob" }],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "AzureML Update Resource",
                "linkedServiceName": "updatableScoringEndpoint2"
            }
        ],
        "start": "2016-02-13T00:00:00",
        "end": "2016-02-14T00:00:00"
    }
}
```

## <a name="data-lake-analytics-u-sql-activity"></a>Data Lake Analytics U-SQL 작업
Hello 다음과 같은 U-SQL 작업 JSON 정의에서 속성을 지정할 수 있습니다. hello 활동에 대 한 hello type 속성 이어야 합니다: **DataLakeAnalyticsU SQL**합니다. 연결 된 Azure Data Lake 분석 서비스를 만들고 그의 hello 이름을 hello에 대 한 값으로 지정 해야 **linkedServiceName** 속성입니다. hello 다음 속성은 지원 hello **typeProperties** hello 유형의 활동 tooDataLakeAnalyticsU SQL 설정 섹션: 

| 속성 | 설명 | 필수 |
|:--- |:--- |:--- |
| scriptPath |Hello U-SQL 스크립트를 포함 하는 경로 toofolder 합니다. Hello 파일의 이름은 대/소문자 구분입니다. |아니요(스크립트를 사용하는 경우) |
| scriptLinkedService |Hello 스크립트 toohello 데이터 팩터리를 포함 하는 hello 저장소를 연결 하는 연결 된 서비스 |아니요(스크립트를 사용하는 경우) |
| script |scriptPath 및 scriptLinkedService를 지정하는 대신 인라인 스크립트를 지정합니다. 예: "script" : "CREATE DATABASE test" |아니요(scriptPath 및 scriptLinkedService를 사용하는 경우) |
| degreeOfParallelism |hello 최대 노드 수는 동시에 toorun hello 작업을 사용 합니다. |아니요 |
| 우선 순위 |먼저 어떤 작업에서 대기 중인 모든 선택한 toorun 해야를 결정 합니다. hello 낮은 hello 수치로 hello hello 우선 순위가 높습니다. |아니요 |
| 매개 변수 |Hello U-SQL 스크립트의 매개 변수 |아니요 |

### <a name="json-example"></a>JSON 예제

```json
{
    "name": "ComputeEventsByRegionPipeline",
    "properties": {
        "description": "This pipeline computes events for en-gb locale and date less than Feb 19, 2012.",
        "activities": 
        [
            {
                "type": "DataLakeAnalyticsU-SQL",
                "typeProperties": {
                    "scriptPath": "scripts\\kona\\SearchLogProcessing.txt",
                    "scriptLinkedService": "StorageLinkedService",
                    "degreeOfParallelism": 3,
                    "priority": 100,
                    "parameters": {
                        "in": "/datalake/input/SearchLog.tsv",
                        "out": "/datalake/output/Result.tsv"
                    }
                },
                "inputs": [
                    {
                        "name": "DataLakeTable"
                    }
                ],
                "outputs": 
                [
                    {
                        "name": "EventsByRegionTable"
                    }
                ],
                "policy": {
                    "timeout": "06:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "EventsByRegion",
                "linkedServiceName": "AzureDataLakeAnalyticsLinkedService"
            }
        ],
        "start": "2015-08-08T00:00:00",
        "end": "2015-08-08T01:00:00",
        "isPaused": false
    }
}
```

자세한 내용은 [Data Lake Analytics U-SQL 활동](data-factory-usql-activity.md)을 참조하세요. 

## <a name="stored-procedure-activity"></a>저장 프로시저 작업
Hello 다음과 같은 저장 프로시저 작업 JSON 정의에서 속성을 지정할 수 있습니다. hello 활동에 대 한 hello type 속성 이어야 합니다: **SqlServerStoredProcedure**합니다. Hello 연결 된 서비스를 다음 중 하나는 만들고 해야 hello 연결 된 서비스의 hello 이름을 hello에 대 한 값으로 지정 **linkedServiceName** 속성:

- SQL Server 
- Azure SQL 데이터베이스
- Azure SQL 데이터 웨어하우스

hello 다음 속성은 지원 hello **typeProperties** hello 유형의 활동 tooSqlServerStoredProcedure 설정 섹션:

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| storedProcedureName |Hello Azure SQL 데이터베이스 또는 출력 테이블 사용 hello hello 연결 된 서비스에 의해 표시 되는 Azure SQL 데이터 웨어하우스 hello 저장 프로시저의 hello 이름을 지정 합니다. |예 |
| storedProcedureParameters |저장 프로시저 매개 변수의 값을 지정합니다. 매개 변수에 대해 toopass을 null 필요 hello 구문 사용: "param1": null (모든 소문자). 이 속성을 사용 하는 방법에 대 한 샘플 toolearn 다음 hello를 참조 하십시오. |아니요 |

입력된 데이터 집합을 지정 않습니다 ('준비' 상태)에서 사용할 수 있어야 hello에 대 한 저장 프로시저 활동 toorun 합니다. hello 입력된 데이터 집합 매개 변수로 hello 저장 프로시저에서 사용할 수 없습니다. 시작 hello 저장 프로시저 작업 전에 것만 사용 되는 toocheck hello 종속성 합니다. 저장 프로시저 작업에 대한 출력 데이터 집합을 지정해야 합니다. 

출력 데이터 집합 지정 hello **일정** hello에 대 한 저장 프로시저 작업 (시간별, 매주, 매월, 등). hello 출력 데이터 집합 사용 해야 합니다는 **연결 된 서비스** tooan Azure SQL 데이터베이스 또는 Azure SQL 데이터 웨어하우스 또는 저장된 프로시저 toorun hello 하려는 SQL Server 데이터베이스를 참조 합니다. hello 출력 데이터 집합으로 사용할 수는 방식으로 toopass hello 결과 후속 처리에 대 한 hello 저장 프로시저의 다른 활동에 의해 ([활동 체인](data-factory-scheduling-and-execution.md##multiple-activities-in-a-pipeline)) hello 파이프라인에서. 그러나 데이터 팩터리는 저장된 프로시저 toothis 데이터 집합의 hello 출력을 자동으로 기록 하지 않습니다. Hello 저장 프로시저 출력 데이터 집합 가리키는 hello 해당 쓰기 tooa SQL 테이블 이며 경우에 따라 hello 출력 데이터 집합 수는 **더미 데이터 집합**, hello를 실행 하기 위한 toospecify hello 일정 저장 프로시저 작업에만 사용 되는 합니다.  

### <a name="json-example"></a>JSON 예제

```json
{
    "name": "SprocActivitySamplePipeline",
    "properties": {
        "activities": [
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "sp_sample",
                    "storedProcedureParameters": {
                        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)"
                    }
                },
                "outputs": [{ "name": "sprocsampleout" }],
                "name": "SprocActivitySample"
            }
        ],
         "start": "2016-08-02T00:00:00",
         "end": "2016-08-02T05:00:00",
        "isPaused": false
    }
}
```

자세한 내용은 [저장 프로시저 활동](data-factory-stored-proc-activity.md)을 참조하세요. 

## <a name="net-custom-activity"></a>.NET 사용자 지정 작업
Hello 다음과 같은.NET 사용자 지정 활동 JSON 정의에서 속성을 지정할 수 있습니다. hello 활동에 대 한 hello type 속성 이어야 합니다: **DotNetActivity**합니다. Azure HDInsight 연결 된 서비스를 만들어야 합니다 또는 Azure 배치 연결 된 서비스를 마우스 hello 연결 된 서비스의 hello 이름을 hello에 대 한 값으로 지정 **linkedServiceName** 속성입니다. hello 다음 속성은 지원 hello **typeProperties** hello 유형의 활동 tooDotNetActivity 설정 섹션:
 
| 속성 | 설명 | 필수 |
|:--- |:--- |:--- |
| AssemblyName | Hello 어셈블리의 이름입니다. Hello 예제: **MyDotnetActivity.dll**합니다. | 예 |
| EntryPoint |Hello IDotNetActivity 인터페이스를 구현 하는 hello 클래스의 이름입니다. Hello 예제: **MyDotNetActivityNS.MyDotNetActivity** 여기서 MyDotNetActivityNS hello 네임 스페이스 이므로 MyDotNetActivity hello 클래스입니다.  | 예 | 
| PackageLinkedService | Hello hello 사용자 지정 활동 zip 파일이 포함 된 toohello blob 저장소를 가리키는 Azure 저장소 연결 된 서비스의 이름입니다. Hello 예제: **AzureStorageLinkedService**합니다.| 예 |
| PackageFile | Hello zip 파일의 이름입니다. Hello 예제: **customactivitycontainer/MyDotNetActivity.zip**합니다. | 예 |
| extendedProperties | 정의 하 고 toohello.NET 코드에 전달할 수 있는 확장 된 속성입니다. 이 예제에서는 hello **SliceStart** 변수 tooa 값 hello SliceStart 시스템 변수를 기반으로 설정 되어 있습니다. | 아니요 | 

### <a name="json-example"></a>JSON 예제

```json
{
  "name": "ADFTutorialPipelineCustom",
  "properties": {
    "description": "Use custom activity",
    "activities": [
      {
        "Name": "MyDotNetActivity",
        "Type": "DotNetActivity",
        "Inputs": [
          {
            "Name": "InputDataset"
          }
        ],
        "Outputs": [
          {
            "Name": "OutputDataset"
          }
        ],
        "LinkedServiceName": "AzureBatchLinkedService",
        "typeProperties": {
          "AssemblyName": "MyDotNetActivity.dll",
          "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
          "PackageLinkedService": "AzureStorageLinkedService",
          "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
          "extendedProperties": {
            "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"
          }
        },
        "Policy": {
          "Concurrency": 2,
          "ExecutionPriorityOrder": "OldestFirst",
          "Retry": 3,
          "Timeout": "00:30:00",
          "Delay": "00:00:00"
        }
      }
    ],
    "start": "2016-11-16T00:00:00",
    "end": "2016-11-16T05:00:00",
    "isPaused": false
  }
}
```

자세한 내용은 [Data Factory에서 사용자 지정 활동 사용](data-factory-use-custom-activities.md) 문서를 참조하세요. 

## <a name="next-steps"></a>다음 단계
자습서를 따라 hello를 참조 하십시오. 

- [자습서: 복사 활동이 있는 파이프라인 만들기](data-factory-copy-activity-tutorial-using-azure-portal.md)
- [자습서: Hive 활동이 있는 파이프라인 만들기](data-factory-build-your-first-pipeline-using-editor.md)
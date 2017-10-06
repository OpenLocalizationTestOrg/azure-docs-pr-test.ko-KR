---
title: "aaaScheduling 및 데이터 팩터리를 사용 하 여 실행 | Microsoft Docs"
description: "Azure Data Factory 응용 프로그램 모델의 예약 및 실행에 대한 내용을 알아봅니다."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 088a83df-4d1b-4ac1-afb3-0787a9bd1ca5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 6114dd4896f5537c789c3b632fb90e501b694285
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="data-factory-scheduling-and-execution"></a>Data Factory 예약 및 실행
이 문서는 hello Azure Data Factory 응용 프로그램 모델의 hello 예약 및 실행 측면을 설명합니다. 이 문서는 사용자가 작업, 파이프라인, 연결된 서비스 및 데이터 집합과 같은 Data Factory 응용 프로그램 모델 개념을 이해하고 있다고 가정합니다. Azure Data Factory의 기본 개념에 대 한 참조 문서 다음 hello:

* [소개 tooData 팩터리](data-factory-introduction.md)
* [파이프라인](data-factory-create-pipelines.md)
* [데이터 집합](data-factory-create-datasets.md) 

## <a name="start-and-end-times-of-pipeline"></a>파이프라인의 시작 및 종료 시간
파이프라인은 **시작** 시간과 **종료** 시간 사이에서만 활성화됩니다. Hello 시작 시간 이전 또는 hello 종료 시간 이후에 실행 되지 않습니다. Hello 파이프라인이 일시 중지, 시작 및 종료 시간에 관계 없이 실행 되지 않습니다. 파이프라인 toorun에 대 한 것 해야 일시 중지할 수 있습니다. Hello 파이프라인 정의에서 이러한 설정을 (시작, 종료, 일시 중지)을 찾을: 

```json
"start": "2017-04-01T08:00:00Z",
"end": "2017-04-01T11:00:00Z"
"isPaused": false
```

이러한 속성에 대한 자세한 내용은 [파이프라인 만들기](data-factory-create-pipelines.md) 문서를 참조하세요. 


## <a name="specify-schedule-for-an-activity"></a>활동 일정 지정
Hello 파이프라인 실행 되는 없습니다. Hello에 실행 되는 hello 파이프라인의 hello 작업은 hello 파이프라인의 전체적인 맥락 합니다. Hello를 사용 하 여 활동에 대 한 되풀이 일정을 지정할 수 있습니다 **스케줄러** 활동 JSON의 섹션입니다. 예를 들어 예약할 수 있습니다 활동 toorun 매시간 다음과 같습니다.  

```json
"scheduler": {
    "frequency": "Hour",
    "interval": 1
},
```

Hello 다음 다이어그램에에서 나와 있는 것 처럼 활동에 대 한 일정 계열을 사용 하 여 연속 창의 hello 지정 파이프라인 시작 시간 및 종료. 연속 창은 일련의 고정된 크기의 겹치지 않는 연속적인 시간 간격입니다. 활동에 대한 이러한 논리적 연속 창을 **활동 기간**이라고 합니다.

![활동 스케줄러 예제](media/data-factory-scheduling-and-execution/scheduler-example.png)

hello **스케줄러** 활동에 대 한 속성은 선택 사항입니다. 이 속성을 지정 하면 경우 hello 활동에 대 한 출력 데이터 집합의 hello 정의에서 지정 하는 hello 흐름을 일치 해야 합니다. 현재 출력 데이터 집합은 어떤 드라이브 hello 일정입니다. 따라서 만들어야 출력 데이터 집합의 관계를 hello 활동 출력을 생성 하지 않는 경우에 합니다. 

## <a name="specify-schedule-for-a-dataset"></a>데이터 집합 일정 지정
Data Factory 파이프라인의 활동은 0개 이상의 입력 **데이터 집합**을 받고, 하나 이상의 출력 데이터 집합을 생성할 수 있습니다. 활동에 대 한 입력된 데이터를 사용할 수 있는 hello에 hello 흐름을 지정할 수 있습니다 또는 hello를 사용 하 여 hello 출력 데이터 생성 **가용성** hello 데이터 집합 정의에 섹션입니다. 

**빈도** hello에 **가용성** 섹션 hello 시간 단위를 지정 합니다. hello 빈도 대 한 값은 허용: 분, 시간, 일, 주 및 월. hello **간격** hello 가용성 섹션에서 속성 빈도의 승수를 지정 합니다. 예를 들어: hello 출력 데이터가 매일 생성 hello 주기 tooDay 설정 하는 경우 출력 데이터 집합에 대 한 too1 간격을 설정 합니다. 분으로 hello 빈도 지정 하는 경우에 15 보다 작은 간격 toono hello 설정 하는 것이 좋습니다. 

다음 예제는 hello에서 hello 입력된 데이터를 사용할 수 매시간 hello 출력 데이터가 매시간 생성 됩니다 (`"frequency": "Hour", "interval": 1`). 

**입력 데이터 집합:** 

```json
{
    "name": "AzureSqlInput",
    "properties": {
        "published": false,
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```


**출력 데이터 집합**

```json
{
    "name": "AzureBlobOutput",
    "properties": {
        "published": false,
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mypath/{Year}/{Month}/{Day}/{Hour}",
            "format": {
                "type": "TextFormat"
            },
            "partitionedBy": [
                { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
                { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
                { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
                { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "HH" }}
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

현재 **출력 데이터 집합 드라이브 hello 일정**합니다. 즉, hello 출력 데이터 집합에 대해 지정 된 hello 일정은 런타임에 작업에서 사용 되는 toorun 합니다. 따라서 만들어야 출력 데이터 집합의 관계를 hello 활동 출력을 생성 하지 않는 경우에 합니다. Hello 활동의 입력을 사용 하지 않습니다, hello 입력된 데이터 집합 만들기를 건너뛸 수 있습니다. 

다음 예제 hello 파이프라인 정의 hello **스케줄러** 속성은 hello 활동에 대 한 사용 되는 toospecify 일정입니다. 이 속성은 선택 사항입니다. 현재 hello 활동에 대 한 hello 일정 hello 일정 hello 출력 데이터 집합에 대해 지정 된 일치 해야 합니다.
 
```json
{
    "name": "SamplePipeline",
    "properties": {
        "description": "copy activity",
        "activities": [
            {
                "type": "Copy",
                "name": "AzureSQLtoBlob",
                "description": "copy activity",
                "typeProperties": {
                    "source": {
                        "type": "SqlSource",
                        "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 100000,
                        "writeBatchTimeout": "00:05:00"
                    }
                },
                "inputs": [
                    {
                        "name": "AzureSQLInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                }
            }
        ],
        "start": "2017-04-01T08:00:00Z",
        "end": "2017-04-01T11:00:00Z"
    }
}
```

이 예제에서는 hello 활동을 1 시간 마다 실행 hello 사이의 시작 시간 및 종료 hello 파이프라인. hello 출력 데이터는 3 개의 시간 창 (8-9 오전, 오전 9 시에서 오전 10, 및 10-11 오전)에 대 한 매시간 생성 됩니다. 

활동 실행에서 사용하거나 생성한 데이터의 각 단위를 **데이터 조각**이라고 합니다. 다이어그램을 다음 hello 하나의 입력 데이터 집합과 하나의 출력 데이터 집합 작업의 예를 보여 줍니다. 

![가용성 스케줄러](./media/data-factory-scheduling-and-execution/availability-scheduler.png)

hello 다이어그램 hello에 대 한 데이터 조각이 입력 및 출력 데이터 집합 1 시간 마다 hello를 보여줍니다. hello 다이어그램에는 처리를 위해 준비 하는 세 가지 입력된 조각을 보여 줍니다. hello 10-11 오전 활동 hello 10-11 오전 출력 조각을 생성 하는 진행 중입니다. 

변수를 사용 하 여 hello 데이터 집합 JSON의에서 현재 조각 hello와 관련 된 hello 시간 간격에 액세스할 수 있습니다: [SliceStart](data-factory-functions-variables.md#data-factory-system-variables) 및 [SliceEnd](data-factory-functions-variables.md#data-factory-system-variables)합니다. 마찬가지로, WindowStart hello 및 WindowEnd를 사용 하 여 연결 된 활동 hello 시간 간격을 액세스할 수 있습니다. 활동의 hello 일정 hello 활동에 대 한 hello 출력 데이터 집합의 일정을 hello 일치 해야 합니다. 따라서 SliceStart hello 및 SliceEnd 값은 hello 동일 WindowStart WindowEnd 값으로 각각. 이러한 변수에 대한 자세한 내용은 [Data Factory 함수 및 시스템 변수](data-factory-functions-variables.md#data-factory-system-variables) 문서를 참조하세요.  

이러한 변수를 작업 JSON에서 다양한 용도로 사용할 수 있습니다. 예를 들어 데이터 사용할 수 있습니다 이러한 tooselect 시계열 데이터를 나타내는 입력 및 출력 데이터 집합에서 (예: 8 AM too9 AM). 또한이 예제에서는 **WindowStart** 및 **WindowEnd** tooselect 관련 데이터를 활동에 대해 실행 하 고 적절 한 hello로 tooa blob 복사 **folderPath**합니다. hello **folderPath** 매시간에 대 한 매개 변수가 있는 toohave 별도 폴더입니다.  

앞 예제는 hello, 입력 및 출력 데이터 집합에 대해 지정 된 hello 일정이 동일 (매시간) hello 됩니다. Hello hello 활동에 대 한 입력된 데이터 집합을 사용할 수 경우 다른 빈도로 예: 15 분 마다 hello 출력 데이터 집합은 어떤 드라이브 hello 활동 일정으로이 출력 데이터 집합을 생성 하는 hello 활동이 계속 한 시간에 한 번 실행 됩니다. 자세한 내용은 [다양한 빈도로 데이터 집합 모델링](#model-datasets-with-different-frequencies)을 참조하세요.

## <a name="dataset-availability-and-policies"></a>데이터 집합 가용성 및 정책
데이터 집합 정의의 hello 가용성 섹션의 빈도 및 간격이 속성의 hello 사용에 알아보았습니다. hello 예약 및 실행 작업에 영향을 주는 다른 몇 가지 속성이 있습니다. 

### <a name="dataset-availability"></a>데이터 집합 가용성 
hello 다음 표에서 설명 hello에 사용할 수 있는 속성 **가용성** 섹션:

| 속성 | 설명 | 필수 | 기본값 |
| --- | --- | --- | --- |
| frequency |데이터 집합 조각 프로덕션에 대 한 hello 시간 단위를 지정합니다.<br/><br/><b>지원되는 빈도</b>: 분, 시, 일, 주, 월 |예 |해당 없음 |
| interval |빈도 승수를 지정합니다.<br/><br/>"X 주파수 간격" 결정 얼마나 자주 hello 조각이 생성 됩니다.<br/><br/>설정 하는 경우는 시간 단위로 분할 되는 데이터 집합 toobe hello 필요, <b>주파수</b> 너무<b>시간</b>, 및 <b>간격</b> 너무<b>1</b>합니다.<br/><br/><b>참고</b>: 1 분으로 주파수를 지정 하면 15 보다 작은 간격 toono hello 설정 하는 것이 좋습니다 |예 |해당 없음 |
| style |Hello 간격의 시작/끝 hello에 hello 분할 영역을 생성 해야 하는지 여부를 지정 합니다.<ul><li>StartOfInterval</li><li>EndOfInterval</li></ul><br/><br/>Frequency를 tooMonth를 설정 하는 경우 스타일 tooEndOfInterval 설정 되어 있으면 hello 달의 마지막 날에 hello 조각이 생성 됩니다. Hello 스타일 tooStartOfInterval을 설정 하는 경우에 월의 첫째 날으로 hello에 hello 조각이 생성 됩니다.<br/><br/>Frequency를 tooDay를 설정 하는 경우 스타일 tooEndOfInterval 설정 되어 있으면 hello 조각이 hello 지난 1 시간 동안 hello 하루 중에 생성 됩니다.<br/><br/>Frequency를 tooHour를 설정 하는 경우 스타일 tooEndOfInterval 설정 되어 있으면 hello 조각이 hello 시간 hello 끝에 생성 됩니다. 예를 들어, 오후 1 ~ 2 시 기간에 조각의 hello 조각이 오후 2 시 생성 됩니다. |아니요 |EndOfInterval |
| anchorDateTime |스케줄러 toocompute 데이터 집합 분할 영역 경계에 의해 사용 된 시간에 hello 절대 위치를 정의 합니다. <br/><br/><b>참고</b>: hello AnchorDateTime에 hello 빈도 보다 더 세부적인 날짜 부분이 경우 hello 더 세분화 된 부분은 무시 됩니다. <br/><br/>예를 들어 경우 hello, <b>간격</b> 은 <b>매시간</b> (빈도: 시간 및 간격: 1) 및 hello <b>AnchorDateTime</b> 포함 <b>, 분, 초</b>, 다음 hello <b>, 분, 초</b> hello AnchorDateTime의 일부는 무시 됩니다. |아니요 |01/01/0001 |
| offset |어떤 hello에서 모든 데이터 집합 분할 영역의 시작과 끝을 향해 이동 하는 Timespan입니다. <br/><br/><b>참고</b>: hello 결과 결합 된 hello shift anchorDateTime 및 offset을 모두를 지정 합니다. |아니요 |해당 없음 |

### <a name="offset-example"></a>offset example
기본적으로 매일(`"frequency": "Day", "interval": 1`) 조각은 UTC 시간으로 오전 12시(자정)에서 시작합니다. 대신 hello 시작 시간 toobe 오전 6 시 UTC 시간을 하려는 경우 hello hello 다음 코드 조각에에서 나와 있는 것 처럼 오프셋을 설정 합니다. 

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
### <a name="anchordatetime-example"></a>anchorDateTime 예제
다음 예제는 hello, hello dataset 23 시간 마다 한 번 생성 됩니다. hello 첫 번째 조각의 시작 시 hello anchorDateTime 너무 설정으로 지정 된 hello`2017-04-19T08:00:00` (UTC 시간).

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 23,    
    "anchorDateTime":"2017-04-19T08:00:00"    
}
```

### <a name="offsetstyle-example"></a>offset/style 예제
hello 다음 데이터 집합은 월별 데이터 집합 및 오전 8시 매월 세 번째 점입니다 (`3.08:00:00`):

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "offset": "3.08:00:00", 
    "style": "StartOfInterval"
}
```

### <a name="dataset-policy"></a>데이터 집합 정책
데이터 집합 방법을 조각 실행에서 생성 된 hello 데이터 유효성을 검사할 수 소비에 대 한 준비가 될 때까지 지정 하는 유효성 검사 정책 정의 가질 수 있습니다. 이러한 경우 hello 조각 실행을 마친 후 hello 출력 조각 상태가 변경 되 너무**대기** 의 하위 상태와 **유효성 검사**합니다. Hello 조각 상태 쪽 변경 hello 분할 영역 확인 되 면**준비**합니다. 데이터 조각 생성 되었으면 hello 유효성 검사를 통과 하지 못한 경우,이 조각의에 의존 하는 다운스트림 분할 영역에 대 한 활동 실행 처리 되지 않습니다. [모니터링 하 고 파이프라인 관리](data-factory-monitor-manage-pipelines.md) 표지 hello Data Factory에 데이터 조각이의 다양 한 상태입니다.

hello **정책** 데이터 집합 정의 섹션 hello 조건 정의 또는 데이터 집합 분할 영역 hello hello 조건을 충족 해야 합니다. hello 다음 표에서 설명 hello에 사용할 수 있는 속성 **정책** 섹션:

| 정책 이름 | 설명 | 너무 적용| 필수 | 기본값 |
| --- | --- | --- | --- | --- |
| minimumSizeMB | Hello 데이터에 유효성을 검사 한 **Azure blob** 충족 hello 최소 크기 요구 사항 (메가바이트)입니다. |Azure Blob |아니요 |해당 없음 |
| minimumRows | Hello 데이터에 유효성을 검사 한 **Azure SQL 데이터베이스** 또는 **Azure 테이블** hello 최소 행 수를 포함 합니다. |<ul><li>Azure SQL Database</li><li>Azure 테이블</li></ul> |아니요 |해당 없음 |

#### <a name="examples"></a>예
**minimumSizeMB:**

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

**minimumRows**

```json
"policy":
{
    "validation":
    {
        "minimumRows": 100
    }
}
```

이러한 속성과 예제에 대한 자세한 내용은 [데이터 집합 만들기](data-factory-create-datasets.md) 문서를 참조하세요. 

## <a name="activity-policies"></a>활동 정책
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

자세한 내용은 [파이프라인](data-factory-create-pipelines.md) 문서를 참조하세요. 

## <a name="parallel-processing-of-data-slices"></a>데이터 조각의 병렬 처리
지난 hello에 hello 파이프라인에 대 한 hello 시작 날짜를 설정할 수 있습니다. 이렇게 하면 데이터 팩터리 자동으로 이전 hello에서 모든 데이터 조각 (뒤로 채우기)을 계산 하 고 처리를 시작 합니다. 예를 들어: 경우 시작 날짜가 2017-04-01 파이프라인을 생성 하 고 hello 현재 날짜는 2017-04-10입니다. Hello의 hello 흐름 출력 데이터 집합은 매일, 다음 2017-04-01에서 모든 hello 분할 영역을 처리 하는 데이터 팩터리 하기 시작 하는 경우 too2017-04-09 즉시 시작 날짜를 hello 이므로 지난 hello에 합니다. hello 조각이 2017-04-10에서 처리 되지 않습니다 아직 hello 가용성 섹션의 스타일 속성의 hello 값은 EndOfInterval 때문에 기본적으로 합니다. hello 가장 오래 된 조각을 처리 하는 먼저 OldestFirst가 executionPriorityOrder 값 hello 기본값으로 합니다. Hello 스타일 속성에 대 한 참조 [dataset 가용성](#dataset-availability) 섹션. Hello executionPriorityOrder 섹션에 대 한 참조 hello [활동 정책](#activity-policies) 섹션. 

다시 채워진 데이터 조각을 toobe hello 설정 하 여 동시에 처리를 구성할 수 있습니다 **동시성** hello에 대 한 속성 **정책** hello 활동 JSON의 섹션입니다. 이 속성은 여러 조각에서 발생할 수 있는 병렬 활동 실행 hello 수를 결정 합니다. hello hello 동시성 속성 기본값은 1입니다. 따라서 기본적으로 조각이 한 번에 하나씩 처리됩니다. hello 최 댓 값은 10입니다. 파이프라인에서 큰 사용 가능한 데이터에 더 큰 동시성 값 집합을 통해 toogo를 필요로 하는 경우 데이터 처리 hello 빨라집니다. 

## <a name="rerun-a-failed-data-slice"></a>실패한 데이터 조각 다시 실행
데이터 조각을 처리 하는 동안 오류가 발생 하는 경우 Azure 포털 블레이드 또는 모니터 및 앱 관리를 사용 하 여 조각 hello 처리 실패 한 이유를 찾을 수 있습니다. 자세한 내용은 [Azure 포털 블레이드를 사용하여 파이프라인 모니터링 및 관리](data-factory-monitor-manage-pipelines.md) 또는 [앱 모니터링 및 관리](data-factory-monitor-manage-app.md)를 참조하세요.

다음 예에서는 두 개의 활동을 보여 주는 hello를 것이 좋습니다. 활동 1 및 활동 2가 있습니다. Activity1은 Dataset1의 조각을 사용 하 고 Dataset2 Activity2 tooproduce hello 최종 데이터 집합의 조각 한 입력으로 사용 되는 조각을 생성 합니다.

![실패한 조각](./media/data-factory-scheduling-and-execution/failed-slice.png)

hello 다이어그램을 보여 줍니다 세 최근 분할 영역 외부로 오류가 생성 hello 오전 9 10에 대 한 슬라이스 Dataset2 했습니다. 데이터 팩터리 hello 시간 시계열 데이터 집합에 대 한 종속성을 자동으로 추적합니다. 결과적으로, hello 활동 hello 오전 9 10 다운스트림 조각에 대 한 실행 시작 되지 않습니다.

데이터 팩터리 모니터링 및 관리 도구를 사용 하면 toodrill hello 진단 로그 hello 실패 한 조각 tooeasily 찾기 hello 루트 hello 문제에 대 한 발생 하 고 해결 합니다. Hello 문제를 해결 한 후에 tooproduce hello 실패 한 조각을 실행 하는 hello 활동을 쉽게 시작할 수 있습니다. 방법에 대 한 자세한 내용은 toorerun 참조, 데이터 조각에 대 한 상태 전환 이해 하 고 [모니터링 및 관리 Azure 포털 블레이드를 사용 하 여 파이프라인](data-factory-monitor-manage-pipelines.md) 또는 [모니터링 및 관리 앱](data-factory-monitor-manage-app.md)합니다.

오전 9 10에 대 한 조각화 hello를 다시 실행 한 후 **Dataset2**, Data Factory hello hello 최종 데이터 집합에서 hello 오전 9 10 종속 조각에 대 한 실행을 시작 합니다.

![실패한 조각 다시 실행](./media/data-factory-scheduling-and-execution/rerun-failed-slice.png)

## <a name="multiple-activities-in-a-pipeline"></a>파이프라인의 여러 활동
그렇지만 하나의 파이프라인에 여러 개의 활동이 있을 수 있습니다. 파이프라인의 여러 활동을 있고 hello 활동 출력은 다른 활동의 입력 하지 hello 활동에 대 한 입력된 데이터 조각이 준비가 되었는지 여부 hello 활동 병렬로 실행할 수 있습니다.

Hello 입력 데이터 집합의 hello 다른 활동으로 한 활동의 hello 출력 데이터 집합을 설정 하 여 두 개의 활동 (활동 다음에 다른 실행)을 연결할 수 있습니다. hello에 hello 활동 수 있는 동일한 파이프라인 또는 다른 파이프라인. 두 번째 활동 hello hello 먼저 하나 성공적으로 완료 하는 경우에 실행 합니다.

예를 들어 파이프라인의 두 활동에 있는 경우 다음 hello:

1. 외부 입력 데이터 집합 D1이 필요하고 출력 데이터 집합 D2를 생성하는 활동 A1
2. 데이터 집합 D2로부터의 입력이 필요하고 출력 데이터 집합 D3을 생성하는 활동 A2

이 시나리오, A1 및 A2 활동에는 hello에 동일한 파이프라인입니다. hello 활동 A1 hello 외부 데이터를 사용할 수를 예약 된 hello 가용성 주파수에 도달할 때 실행 됩니다. hello 활동 A2 실행 hello d 2에서 예약 된 조각을 사용할 수 있으며 hello 사용 가능한 일정된 빈도 도달 하면 됩니다. 데이터 집합 d 2의에서 hello 조각 중 하나에 오류가 발생 하는, 사용 가능 해질 때까지 A2 해당 조각에 대 한 실행 되지 않습니다.

동일한 파이프라인 hello 다음 다이어그램은 같습니다. 두 활동 hello에 다이어그램 보기 hello:

![동일한 파이프라인 활동 hello에 연결](./media/data-factory-scheduling-and-execution/chaining-one-pipeline.png)

앞서 언급 했 듯이 hello 활동 다른 파이프라인에 사용할 수 있습니다. 이 시나리오에서는 hello 다이어그램 보기 다이어그램을 다음 hello와 같습니다.

![두 개의 파이프라인에서 활동 연결](./media/data-factory-scheduling-and-execution/chaining-two-pipelines.png)

Hello 참조 [순차적으로 복사](#copy-sequentially) 예제를 보려면 hello 부록에서 섹션.

## <a name="model-datasets-with-different-frequencies"></a>다양한 빈도로 데이터 집합 모델링
Hello 샘플에서 창에 대 한 입력 및 출력 데이터 집합 및 hello 활동 일정 hello 주파수 같은 hello 되었습니다. 일부 시나리오에는 하나 이상의 입력의 hello 빈도 아닌 다른 빈도로 hello 기능 tooproduce 출력을 해야합니다. Data Factory가 이러한 시나리오의 모델링을 지원합니다.

### <a name="sample-1-produce-a-daily-output-report-for-input-data-that-is-available-every-hour"></a>샘플 1: 매시간 제공되는 입력 데이터에 대해 일별 출력 보고서 생성
Azure Blob 저장소에서 매시간 사용 가능한 센서로부터 입력 측정값 데이터가 있는 시나리오를 살펴보겠습니다. Hello 날에 대 한 tooproduce 평균, 최대값 및 최소값 등의 통계를 매일 집계 보고서를 원하는 [Data Factory hive 작업](data-factory-hive-activity.md)합니다.

다음은 Data Factory로 이 시나리오를 모델링하는 방법입니다.

**입력 데이터 집합**

매시간 hello는 일을 지정 하는 hello에 대 한 hello 폴더에 파일을 삭제할 입력입니다. 입력에 대한 Availability가 **Hour** 로 설정됩니다(frequency: Hour, interval: 1).

```json
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
**출력 데이터 집합**

하나의 출력 파일은 매일 hello 날의 폴더에 만들어집니다. 출력의 Availability는 **Day** 로 설정됩니다(frequency: Day 및 interval: 1).

```json
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

**작업: 파이프라인에서 hive 작업**

hello 하이브 스크립트에 적절 한 hello 받는 *DateTime* hello를 사용 하는 매개 변수로 정보 **WindowStart** hello 다음 코드 조각에에서 나와 있는 것 처럼 변수입니다. hello 하이브 스크립트 hello 날에 대 한 hello 올바른 폴더에서이 변수 tooload hello 데이터를 사용 하 고 hello 집계 toogenerate hello 출력을 실행 합니다.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-01-01T08:00:00",
    "end":"2015-01-01T11:00:00",
    "description":"hive activity",
    "activities": [
        {
            "name": "SampleHiveActivity",
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
            "linkedServiceName": "HDInsightLinkedService",
            "type": "HDInsightHive",
            "typeProperties": {
                "scriptPath": "adftutorial\\hivequery.hql",
                "scriptLinkedService": "StorageLinkedService",
                "defines": {
                    "Year": "$$Text.Format('{0:yyyy}',WindowStart)",
                    "Month": "$$Text.Format('{0:MM}',WindowStart)",
                    "Day": "$$Text.Format('{0:dd}',WindowStart)"
                }
            },
            "scheduler": {
                "frequency": "Day",
                "interval": 1
            },            
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 2,
                "timeout": "01:00:00"
            }
         }
     ]
   }
}
```

hello 다음 그림에 데이터 종속성 관점에서 hello 시나리오입니다.

![데이터 종속성](./media/data-factory-scheduling-and-execution/data-dependency.png)

hello 출력 분할 영역을 매일 24 시간 조각에서 입력된 데이터 집합에 따라 달라 집니다. 이러한 종속성을 파악 하 여 자동으로 hello hello에 속하는 입력된 데이터 조각을 데이터 팩터리 계산 동일한 시간으로 생성 된 출력 조각 toobe hello 기간입니다. Hello 24 입력된 분할 영역 중 하나를 사용할 수 없는 경우 데이터 팩터리의 hello 입력된 조각 toobe hello 일별 작업 실행을 시작 하기 전에 준비를 기다립니다.

### <a name="sample-2-specify-dependency-with-expressions-and-data-factory-functions"></a>샘플 2: 식 및 데이터 Data Factory 함수로 종속성 지정
다른 시나리오를 살펴보겠습니다. 두 개의 입력 데이터 집합을 처리하는 hive 작업이 있다고 가정합니다. 그 중 하나는 매일 새 데이터가 제공되지만 다른 하나는 매주 새 데이터를 가져옵니다. 매일은 출력을 생성 하 고 hello 두 개의 입력 간에 조인을 toodo 한다고 가정 합니다.

데이터 팩터리 자동으로 알아 hello 오른쪽 입력 hello 간단한 방법은 데이터 조각이 시간이 기간 작동 하지 않는다 toohello 출력을 정렬 하 여 tooprocess을 분리 합니다.

실행 하는 모든 활동에 대 한 데이터 팩터리 hello 사용 하도록 지난 주 데이터 조각을 hello 매주 입력된 데이터 집합에 대 한을 지정 해야 합니다. 이 동작은 hello 조각 tooimplement 뒤에 표시 된 대로 Azure 데이터 팩터리 함수를 사용 합니다.

**입력1: Azure Blob**

hello는 hello Azure blob 업데이트 되 고 매일 첫 번째 입력이 있습니다.

```json
{
  "name": "AzureBlobInputDaily",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

**입력2: Azure Blob**

Input2는 hello 매주 업데이트 되 고 Azure blob입니다.

```json
{
  "name": "AzureBlobInputWeekly",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 7
    }
  }
}
```

**출력: Azure Blob**

하나의 출력 파일은 hello 날에 대 한 hello 폴더에 매일을 만들어집니다. 출력의 가용성을 너무 설정**일** (빈도: 일, 간격: 1).

```json
{
  "name": "AzureBlobOutputDaily",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

**작업: 파이프라인에서 hive 작업**

hello은 두 개의 입력 하 고 출력 조각을 매일 생성 하는 hello hive 작업 합니다. 에 매일의 출력 조각 toodepend hello 주간 입력에 대 한 지난 주의 입력된 조각은 다음과 같이 지정할 수 있습니다.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-01-01T08:00:00",
    "end":"2015-01-01T11:00:00",
    "description":"hive activity",
    "activities": [
      {
        "name": "SampleHiveActivity",
        "inputs": [
          {
            "name": "AzureBlobInputDaily"
          },
          {
            "name": "AzureBlobInputWeekly",
            "startTime": "Date.AddDays(SliceStart, - Date.DayOfWeek(SliceStart))",
            "endTime": "Date.AddDays(SliceEnd,  -Date.DayOfWeek(SliceEnd))"  
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutputDaily"
          }
        ],
        "linkedServiceName": "HDInsightLinkedService",
        "type": "HDInsightHive",
        "typeProperties": {
          "scriptPath": "adftutorial\\hivequery.hql",
          "scriptLinkedService": "StorageLinkedService",
          "defines": {
            "Year": "$$Text.Format('{0:yyyy}',WindowStart)",
            "Month": "$$Text.Format('{0:MM}',WindowStart)",
            "Day": "$$Text.Format('{0:dd}',WindowStart)"
          }
        },
        "scheduler": {
          "frequency": "Day",
          "interval": 1
        },            
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 2,  
          "timeout": "01:00:00"
        }
       }
     ]
   }
}
```

Data Factory에서 지원하는 함수 및 시스템 변수 목록은 [Data Factory 함수 및 시스템 변수](data-factory-functions-variables.md) 를 참조하세요.

## <a name="appendix"></a>부록

### <a name="example-copy-sequentially"></a>예제: 순차적으로 복사
것은 가능한 toorun 여러 복사 작업 차례로 정렬/순차적 방식으로 합니다. 예를 들어 두 개의 복사본 입력 다음 hello로 (CopyActivity1 및 CopyActivity2) 파이프라인의 활동 데이터 출력 데이터 집합을 할 수 있습니다.   

CopyActivity1

입력: Dataset1. 출력: Dataset2.

CopyActivity2

입력: Dataset2.  출력: Dataset3.

CopyActivity2 hello CopyActivity1을 성공적으로 실행 하 고 Dataset2 ´ ï ´ 경우에 실행 됩니다.

Hello 샘플 파이프라인 JSON 다음과 같습니다.

```json
{
    "name": "ChainActivities",
    "properties": {
        "description": "Run activities in sequence",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "copyBehavior": "PreserveHierarchy",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset1"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset2"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlob1ToBlob2",
                "description": "Copy data from a blob tooanother"
            },
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset2"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset3"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlob2ToBlob3",
                "description": "Copy data from a blob tooanother"
            }
        ],
        "start": "2016-08-25T01:00:00Z",
        "end": "2016-08-25T01:00:00Z",
        "isPaused": false
    }
}
```

확인 hello 예 hello 출력 데이터 집합의 첫 번째 복사 작업 (Dataset2) hello hello 두 번째 활동에 대 한 입력으로 지정 됩니다. 따라서 두 번째 활동 hello hello 첫 번째 활동에서 hello 출력 데이터 집합은 준비 하는 경우에 실행 합니다.  

hello 예제 CopyActivity2 수 Dataset3, 등의 다른 입력 있지만 않아 hello 활동 CopyActivity1 완료 될 때까지 실행 되지 않습니다는 입력된 tooCopyActivity2로 Dataset2를 지정 합니다. 예:

CopyActivity1

입력: Dataset1. 출력: Dataset2.

CopyActivity2

입력: Dataset3, Dataset2. 출력: Dataset4.

```json
{
    "name": "ChainActivities",
    "properties": {
        "description": "Run activities in sequence",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "copyBehavior": "PreserveHierarchy",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset1"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset2"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlobToBlob",
                "description": "Copy data from a blob tooanother"
            },
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset3"
                    },
                    {
                        "name": "Dataset2"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset4"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlob3ToBlob4",
                "description": "Copy data from a blob tooanother"
            }
        ],
        "start": "2017-04-25T01:00:00Z",
        "end": "2017-04-25T01:00:00Z",
        "isPaused": false
    }
}
```

Hello 예에서는 두 입력된 데이터 집합 hello 두 번째 복사 작업에 지정 된 것을 확인 합니다. 여러 입력을 지정 하는 경우에만 hello 첫 번째 입력된 데이터 집합은 데이터를 복사 하는 데 사용 되는 있지만 다른 데이터 집합 종속성으로 사용 됩니다. CopyActivity2 hello 다음 조건이 충족 되 후에 시작 합니다.

* CopyActivity1이 성공적으로 완료되고 Dataset2가 사용 가능합니다. 데이터 tooDataset4를 복사 하는 경우에이 데이터 집합 사용 되지 않습니다. CopyActivity2에 대한 일정 종속성으로만 작동합니다.   
* Dataset3을 사용할 수 있습니다. 이 데이터 집합 대상인 복사한 toohello hello 데이터를 나타냅니다. 

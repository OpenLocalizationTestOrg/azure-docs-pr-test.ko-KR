---
title: "aaaData 팩터리 함수 및 시스템 변수 | Microsoft Docs"
description: "Azure 데이터 팩터리 함수 및 시스템 변수 목록을 제공합니다."
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
services: data-factory
ms.assetid: b6b3c2ae-b0e8-4e28-90d8-daf20421660d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: d2936c2821797947bb37d9775226a6c19c4b8ab9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---functions-and-system-variables"></a>Azure 데이터 팩터리 - 함수 및 시스템 변수
이 문서에서는 Azure 데이터 팩터리에서 지원하는 함수와 변수에 대한 정보를 제공합니다.

## <a name="data-factory-system-variables"></a>데이터 팩터리 시스템 변수
| 변수 이름 | 설명 | 개체 범위 | JSON 범위 및 사용 사례 |
| --- | --- | --- | --- |
| WindowStart |현재 작업 실행 창에 대한 시간 간격의 시작 |작업 |<ol><li>데이터 선택 쿼리를 지정합니다. Hello 커넥터 문서의 [데이터 이동 작업](data-factory-data-movement-activities.md) 문서.</li> |
| WindowEnd |현재 작업 실행 창에 대한 시간 간격의 끝 |작업 |WindowStart와 동일 |
| SliceStart |생성되는 데이터 조각에 대한 시간 간격 시작 |작업<br/>데이터 집합 |<ol><li>[Azure Blob](data-factory-azure-blob-connector.md) 및 [파일 시스템 데이터 집합](data-factory-onprem-file-system-connector.md)과 작업하는 동안 동적 폴더 경로 및 파일 이름을 지정합니다.</li><li>작업 입력 컬렉션에서 데이터 팩터리 함수에 입력 종속성을 지정합니다.</li></ol> |
| SliceEnd |현재 데이터 조각에 대한 시간 간격 끝 |작업<br/>dataset |SliceStart와 동일 |

> [!NOTE]
> 해당 hello 예약에 지정 된 hello 데이터 팩터리를 사용 하려면 현재 hello 출력 데이터 집합의 가용성에 지정 된 hello 일정이 정확히 일치 하는 활동입니다. 따라서 WindowStart, WindowEnd, 및 SliceStart와 SliceEnd 항상 매핑됩니다 toohello 동일한 기간과 단일 출력 조각 시간입니다.
> 

### <a name="example-for-using-a-system-variable"></a>시스템 변수 사용 예제
Hello 예제, 연도, 월, 일 및 시간을 다음에 **SliceStart** 에서 사용 되는 개별 변수로 추출 **folderPath** 및 **fileName** 속성입니다.

```json
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```

## <a name="data-factory-functions"></a>데이터 팩터리 함수
시스템 변수 함께 데이터 팩터리에서 목적으로 다음 hello에 대 한 함수를 사용할 수 있습니다.

1. 데이터 선택 쿼리 지정 (hello에서 참조 하는 커넥터 문서를 참조 [데이터 이동 작업](data-factory-data-movement-activities.md) 문서.
   
   데이터 팩터리 함수는 구문 tooinvoke hello:  **$$ <function>**  데이터 선택 쿼리와 hello 활동 및 데이터 집합에 다른 속성에 대 한 합니다.  
2. 작업 입력 컬렉션에서 데이터 팩터리 함수에 입력 종속성 지정
   
    $$는 입력 종속성 식을 지정할 때는 필요하지 않습니다.     

다음 샘플에서는 hello에 **sqlReaderQuery** JSON 파일에 속성 hello 반환한 tooa 값이 할당 `Text.Format` 함수입니다. 또한이 샘플에서는 시스템 변수 라는 **WindowStart**, 창을 실행 하는 hello 활동의 hello 시작 시간을 나타냅니다.

```json
{
    "Type": "SqlSource",
    "sqlReaderQuery": "$$Text.Format('SELECT * FROM MyTable WHERE StartTime = \\'{0:yyyyMMdd-HH}\\'', WindowStart)"
}
```

사용할 수 있는 다른 서식 옵션을 설명하는 [사용자 지정 날짜 및 시간 형식 문자열](https://msdn.microsoft.com/library/8kb3ddd4.aspx)(예: ay 및 yyyy) 토픽을 참조하세요. 

### <a name="functions"></a>함수
다음 표에서 hello Azure 데이터 팩터리의 모든 hello 함수를 나열 합니다.

| Category | 함수 | 매개 변수 | 설명 |
| --- | --- | --- | --- |
| Time |AddHours(X,Y) |X: DateTime  <br/><br/>Y: int |지정 된 시간 X Y 시간 toohello를 추가 합니다. <br/><br/>예: `9/5/2013 12:00:00 PM + 2 hours = 9/5/2013 2:00:00 PM` |
| Time |AddMinutes(X,Y) |X: DateTime  <br/><br/>Y: int |Y 분 tooX를 추가합니다.<br/><br/>예: `9/15/2013 12: 00:00 PM + 15 minutes = 9/15/2013 12: 15:00 PM` |
| Time |StartOfHour(X) |X: DateTime  |Hello 가져옵니다 X의 hello 시간 구성 요소는이 나타내는 hello 시간에 대 한 시간을 시작 합니다. <br/><br/>예: `StartOfHour of 9/15/2013 05: 10:23 PM is 9/15/2013 05: 00:00 PM` |
| Date |AddDays(X,Y) |X: DateTime <br/><br/>Y: int |Y 일 tooX를 추가합니다. <br/><br/>예제: 9/15/2013 12:00:00 PM + 2일 = 9/17/2013 12:00:00 PM<br/><br/>Y를 음수로 지정하여 일도 뺄 수 있습니다.<br/><br/>예: `9/15/2013 12:00:00 PM - 2 days = 9/13/2013 12:00:00 PM`. |
| Date |AddMonths(X,Y) |X: DateTime <br/><br/>Y: int |Y 개월 tooX를 추가합니다.<br/><br/>`Example: 9/15/2013 12:00:00 PM + 1 month = 10/15/2013 12:00:00 PM`<br/><br/>Y를 음수로 지정하여 월도 뺄 수 있습니다.<br/><br/>예: `9/15/2013 12:00:00 PM - 1 month = 8/15/2013 12:00:00 PM`.|
| Date |AddQuarters(X,Y) |X: DateTime  <br/><br/>Y: int |추가 Y * 3 개월 tooX 합니다.<br/><br/>예: `9/15/2013 12:00:00 PM + 1 quarter = 12/15/2013 12:00:00 PM` |
| Date |AddWeeks(X,Y) |X: DateTime <br/><br/>Y: int |추가 Y * 7 일 tooX<br/><br/>예: 9/15/2013 12:00:00 PM + 1주 = 9/22/2013 12:00:00 PM<br/><br/>Y를 음수로 지정하여 주도 뺄 수 있습니다.<br/><br/>예: `9/15/2013 12:00:00 PM - 1 week = 9/7/2013 12:00:00 PM`. |
| Date |AddYears(X,Y) |X: DateTime <br/><br/>Y: int |Y 년 tooX를 추가합니다.<br/><br/>`Example: 9/15/2013 12:00:00 PM + 1 year = 9/15/2014 12:00:00 PM`<br/><br/>Y를 음수로 지정하여 년도 뺄 수 있습니다.<br/><br/>예: `9/15/2013 12:00:00 PM - 1 year = 9/15/2012 12:00:00 PM`. |
| Date |Day(X) |X: DateTime  |X의 hello 일 구성 요소를 가져옵니다.<br/><br/>예: `Day of 9/15/2013 12:00:00 PM is 9`. |
| Date |DayOfWeek(X) |X: DateTime  |Hello 요일을 X의 요일 구성 요소를 가져옵니다.<br/><br/>예: `DayOfWeek of 9/15/2013 12:00:00 PM is Sunday`. |
| Date |DayOfYear(X) |X: DateTime  |X의 hello 연도 구성 요소로 표시 되는 hello 연도 hello 날을 가져옵니다.<br/><br/>예제:<br/>`12/1/2015: day 335 of 2015`<br/>`12/31/2015: day 365 of 2015`<br/>`12/31/2016: day 366 of 2016 (Leap Year)` |
| Date |DaysInMonth(X) |X: DateTime  |매개 변수 X의 hello 월 구성 요소로 표시 되는 hello 달의 hello 날짜를 가져옵니다.<br/><br/>예: `DaysInMonth of 9/15/2013 are 30 since there are 30 days in hello September month`. |
| Date |EndOfDay(X) |X: DateTime  |Hello 날짜-시간 hello 쪽 X의 hello 날짜 (day 구성 요소)을 나타내는 가져옵니다.<br/><br/>예: `EndOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 11:59:59 PM`. |
| Date |EndOfMonth(X) |X: DateTime  |매개 변수 X의 월 구성 요소로 표시 되는 hello 달의 hello 끝을 가져옵니다. <br/><br/>예: `EndOfMonth of 9/15/2013 05:10:23 PM is 9/30/2013 11:59:59 PM` (날짜 hello 9 월 말일을 나타내는 시간) |
| Date |StartOfDay(X) |X: DateTime  |매개 변수 X의 hello 일 구성 요소로 표시 되는 hello 하루의 hello 시작을 가져옵니다.<br/><br/>예: `StartOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 12:00:00 AM`. |
| DateTime |From(X) |X: String |날짜 시간 X tooa 문자열을 구문 분석 합니다. |
| DateTime |Ticks(X) |X: DateTime  |Hello 틱 hello 매개 변수 X의 속성을 가져옵니다. 1 개 틱에 100 나노초입니다. 이 속성의 hello 값 hello 0001 년 1 월 1 일 12시: 00 자정 이후 경과 된 틱 수를 나타냅니다. |
| 텍스트 |Format(X) |X: String 변수 |형식 hello 텍스트 (사용 하 여 `\\'` 조합 tooescape `'` 문자)입니다.|

> [!IMPORTANT]
> 다른 함수 내에서 함수를 사용 하는 경우 toouse 불필요  **$$**  hello 내부 함수에 대 한 접두사입니다. 예: $$Text.Format('PartitionKey eq \\'my_pkey_filter_value\\' 및 RowKey ge \\'{0: yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(SliceStart, -6)). 이 예제에서는 알 수 있듯이  **$$**  접두사가 hello에 대 한 사용 되지 않으면 **Time.AddHours** 함수입니다. 

#### <a name="example"></a>예제
Hello hello Hive 작업에 대 한 다음 예제에서는 입력 및 출력 매개 변수는 hello를 사용 하 여 결정 됩니다 `Text.Format` 함수 및 시스템 변수 SliceStart 합니다. 

```json  
{
    "name": "HiveActivitySamplePipeline",
        "properties": {
    "activities": [
            {
            "name": "HiveActivitySample",
            "type": "HDInsightHive",
            "inputs": [
                    {
                    "name": "HiveSampleIn"
                    }
            ],
            "outputs": [
                    {
                    "name": "HiveSampleOut"
                }
            ],
            "linkedServiceName": "HDInsightLinkedService",
            "typeproperties": {
                    "scriptPath": "adfwalkthrough\\scripts\\samplehive.hql",
                    "scriptLinkedService": "StorageLinkedService",
                    "defines": {
                        "Input": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/samplein/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)",
                        "Output": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/sampleout/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)"
                    },
                    "scheduler": {
                        "frequency": "Hour",
                        "interval": 1
                }
            }
            }
    ]
    }
}
```

### <a name="example-2"></a>예 2

다음 예제는 hello, hello DateTime 매개 변수를 사용 하 여 저장 프로시저 작업 결정은 hello에 대 한 텍스트를 hello 합니다. Format 함수 및 변수 SliceStart hello 합니다. 

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
                "outputs": [
                    {
                        "name": "sprocsampleout"
                    }
                ],
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "SprocActivitySample"
            }
        ],
            "start": "2016-08-02T00:00:00Z",
            "end": "2016-08-02T05:00:00Z",
        "isPaused": false
    }
}
```

### <a name="example-3"></a>예 3
다음 예제는 hello와 같이 hello AddDays 함수를 사용 하는 hello SliceStart,으로 표시 되는 대신 이전 날짜의 tooread 데이터: 

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-01-01T08:00:00",
        "end": "2017-01-01T11:00:00",
        "description": "hive activity",
        "activities": [
            {
                "name": "SampleHiveActivity",
                "inputs": [
                    {
                        "name": "MyAzureBlobInput",
                        "startTime": "Date.AddDays(SliceStart, -1)",
                        "endTime": "Date.AddDays(SliceEnd, -1)"
                    }
                ],
                "outputs": [
                    {
                        "name": "MyAzureBlobOutput"
                    }
                ],
                "linkedServiceName": "HDInsightLinkedService",
                "type": "HDInsightHive",
                "typeProperties": {
                    "scriptPath": "adftutorial\\hivequery.hql",
                    "scriptLinkedService": "StorageLinkedService",
                    "defines": {
                        "Year": "$$Text.Format('{0:yyyy}',WindowsStart)",
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

사용할 수 있는 다른 서식 옵션을 설명하는 [사용자 지정 날짜 및 시간 형식 문자열](https://msdn.microsoft.com/library/8kb3ddd4.aspx) (예: yy 대 yyyy) 토픽을 참조하세요. 


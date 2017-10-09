---
title: "Azure Data Factory에서 데이터 집합 aaaCreate | Microsoft Docs"
description: "AnchorDateTime 및 등의 속성을 사용 하는 예제 Azure Data Factory에서 toocreate 데이터 집합 오프셋 하는 방법을 알아봅니다."
keywords: "데이터 집합 만들기, 데이터 집합 예제, 오프셋 예제"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 0614cd24-2ff0-49d3-9301-06052fd4f92a
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: shlo
ms.openlocfilehash: 181859ed250595d756df73e9ebcac08d9e7184c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="datasets-in-azure-data-factory"></a>Azure 데이터 팩터리의 데이터 집합
이 문서에서는 데이터 집합의 정의, 데이터 집합을 JSON 형식으로 정의하는 방법, Azure Data Factory 파이프라인에서 데이터 집합을 사용하는 방법에 대해 설명합니다. Hello 데이터 집합 JSON 정의에서 각 섹션 (예를 들어 구조, 가용성 및 정책)에 대 한 세부 정보를 제공합니다. hello 문서도 예를 제공 hello를 사용 하 여 **오프셋**, **anchorDateTime**, 및 **스타일** 데이터 집합 JSON 정의에서 속성입니다.

> [!NOTE]
> 새 tooData 팩터리 인 경우 참조 [소개 tooAzure Data Factory](data-factory-introduction.md) 에 대 한 개요입니다. 데이터 팩터리를 만드는 것부터 직접 경험이 읽는 hello 하 여 더 잘 이해를 얻을 수 있습니다 [데이터 변환 자습서](data-factory-build-your-first-pipeline.md) 및 hello [데이터 이동 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)합니다. 

## <a name="overview"></a>개요
데이터 팩터리에는 하나 이상의 파이프라인이 포함될 수 있습니다. **파이프라인**은 함께 하나의 작업을 수행하는 **활동**의 논리적 그룹화입니다. 파이프라인의 hello 활동 데이터에 대해 작업 tooperform를 정의합니다. 예를 들어 온-프레미스 SQL Server tooAzure Blob 저장소에서에서 복사 작업 toocopy 데이터를 사용할 수 있습니다. 그런 다음 Azure HDInsight 클러스터 tooprocess 데이터에서 Blob 저장소 tooproduce 출력 데이터에서 하이브 스크립트를 실행 하는 하이브 활동을 사용할 수 있습니다. 마지막으로 두 번째 복사본 활동 toocopy hello 출력 데이터 tooAzure SQL 데이터 웨어하우스 위에 있는 BI (비즈니스 인텔리전스) 솔루션은 빌드됩니다 보고를 사용할 수 있습니다. 파이프라인 및 활동에 대한 자세한 내용은 [Azure Data Factory의 파이프라인 및 활동](data-factory-create-pipelines.md) 문서를 참조하세요.

활동은 0개 이상의 입력 **데이터 집합**을 받고, 하나 이상의 출력 데이터 집합을 생성할 수 있습니다. 입력된 데이터 집합 hello 파이프라인의 활동에 대 한 hello 입력을 나타내고 출력 데이터 집합 hello 활동에 대 한 hello 출력을 나타냅니다. 데이터 집합은 테이블, 파일, 폴더, 문서를 비롯한 다양한 데이터 저장소 내의 데이터를 식별합니다. 예를 들어 된 Azure Blob 데이터 집합에서 어떤 hello 파이프라인 hello 데이터 읽어야 하는 Blob 저장소에 hello blob 컨테이너 및 폴더를 지정 합니다. 

데이터 집합을 만들기 전에 만듭니다는 **연결 된 서비스** toolink 데이터 toohello 데이터 팩터리를 저장 합니다. 연결 된 서비스 데이터 팩터리의 tooconnect tooexternal 리소스에 대 한 필요한 hello 연결 정보를 정의 하는 연결 문자열 매우 비슷합니다. SQL 테이블, 파일, 폴더, 문서 등 hello 연결 된 데이터 저장소 내에서 데이터를 식별 하는 데이터 집합. 예를 들어 Azure 저장소는 저장소 계정 toohello 데이터 팩터리 서비스 링크를 연결 합니다. Azure Blob 데이터 집합을 hello blob 컨테이너 및 처리 하는 hello 입력된 blob toobe 있는 hello 폴더를 나타냅니다. 

샘플 시나리오는 다음과 같습니다. toocopy 데이터 Blob storage tooa SQL 데이터베이스의 경우, 두 개의 연결 된 서비스를 만들: Azure 저장소 및 Azure SQL 데이터베이스입니다. 그런 다음 두 개의 데이터 집합을 만듭니다: Azure Blob 데이터 집합 (가리키는, toohello Azure 저장소 연결 된 서비스) 및 Azure SQL 테이블 (toohello 연결 된 Azure SQL 데이터베이스 서비스 참조)입니다. hello Azure 저장소 및 Azure SQL 데이터베이스 연결 된 서비스 데이터 팩터리의 각각 런타임 tooconnect tooyour Azure 저장소 및 Azure SQL 데이터베이스에서 사용 하는 연결 문자열을 포함 합니다. hello Azure Blob 데이터 집합 hello blob 컨테이너 및 Blob 저장소에 hello 입력된 blob이 포함 된 blob 폴더를 지정 합니다. hello Azure SQL 테이블의 데이터 집합에 SQL 데이터베이스 toowhich hello 데이터 hello SQL 테이블 복사 toobe을 지정 합니다.

hello 다음 다이어그램 hello 사이의 관계를 표시 파이프라인, 활동, 데이터 집합 및 연결 된 서비스 Data Factory에: 

![파이프라인, 활동, 데이터 집합, 연결된 서비스 간 관계](media/data-factory-create-datasets/relationship-between-data-factory-entities.png)

## <a name="dataset-json"></a>데이터 집합 JSON
Data Factory의 데이터 집합은 다음과 같이 JSON 형식으로 정의됩니다.

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
| name |Hello 데이터 집합의 이름입니다. 명명 규칙은 [Azure Data Factory - 명명 규칙](data-factory-naming-rules.md) 을 참조하세요. |예 |해당 없음 |
| type |hello 데이터 집합의 형식입니다. Data Factory에서 지 원하는 hello 형식 중 하나를 지정 (예: AzureBlob, AzureSqlTable). <br/><br/>자세한 내용은 [데이터 집합 형식](#Type)을 참조하세요. |예 |해당 없음 |
| structure |Hello 데이터 집합의 스키마입니다.<br/><br/>자세한 내용은 [데이터 집합 구조](#Structure)를 참조하세요. |아니요 |해당 없음 |
| typeProperties | hello 유형 속성은 각 유형에 대해 서로 다릅니다 (예: Azure Blob, Azure SQL 테이블). Hello 지원 형식 및 해당 속성에 대 한 자세한 내용은 참조 하십시오. [Dataset 형식](#Type)합니다. |예 |해당 없음 |
| external | 부울 여부 데이터 팩터리 파이프라인에서 명시적으로 데이터 집합은 생성 여부 toospecify를 플래그입니다. 활동에 대 한 입력된 데이터 집합 hello hello 현재 파이프라인에 의해 생성 되지 않습니다, 하는 경우이 플래그 tootrue를 설정 합니다. 이 플래그 tootrue hello hello 첫 번째 활동의 입력된 데이터 집합에 대 한 hello 파이프라인에서 설정 합니다.  |아니요 |false |
| availability | Hello 처리 기간이 (매시간 또는 매일) 또는 데이터 집합 프로덕션 hello에 대 한 모델을 조각화 하는 hello를 정의 합니다. 각 데이터 단위는 데이터 조각이라는 작업 실행으로 사용되고 생성됩니다. 출력 데이터 집합의 hello 가용성 집합 toodaily (빈도-Day, 간격-1) 이면 조각은 매일 생성 합니다. <br/><br/>자세한 내용은 [데이터 집합 가용성](#Availability)을 참조하세요. <br/><br/>Hello 데이터 집합에 대 한 자세한 내용은 hello 참조 모델을 조각화 [일정 예약 및 실행](data-factory-scheduling-and-execution.md) 문서. |예 |해당 없음 |
| policy |Hello 조건 또는 hello 데이터 집합 분할 영역 충족 해야 하는 hello 조건을 정의 합니다. <br/><br/>자세한 내용은 참조 hello [Dataset 정책](#Policy) 섹션. |아니요 |해당 없음 |

## <a name="dataset-example"></a>데이터 집합 예제
다음 예제는 hello, hello 데이터 집합 이라는 테이블 나타냅니다 **MyTable** SQL 데이터베이스에 있습니다.

```json
{
    "name": "DatasetSample",
    "properties": {
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties":
        {
            "tableName": "MyTable"
        },
        "availability":
        {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

포인트 다음 참고 hello:

* **형식** tooAzureSqlTable 설정 됩니다.
* **tableName** type 속성 (특정 tooAzureSqlTable 유형) tooMyTable 설정 됩니다.
* **linkedServiceName** AzureSqlDatabase hello 다음 JSON 코드 조각은에 정의 된 유형의 tooa 연결 된 서비스를 참조 합니다. 
* **가용성 주파수** tooDay, 설정 및 **간격** too1 설정 됩니다. 즉, 해당 hello 데이터 집합 조각이 매일 생성 됩니다.  

**AzureSqlLinkedService**는 다음과 같이 정의됩니다.

```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "description": "",
        "typeProperties": {
            "connectionString": "Data Source=tcp:<servername>.database.windows.net,1433;Initial Catalog=<databasename>;User ID=<username>@<servername>;Password=<password>;Integrated Security=False;Encrypt=True;Connect Timeout=30"
        }
    }
}
```

JSON 코드 조각은 앞 hello:

* **형식** tooAzureSqlDatabase 설정 됩니다.
* **connectionString** type 속성 정보 tooconnect tooa SQL 데이터베이스를 지정 합니다.  

볼 수 있듯이 hello 연결 된 서비스 정의 방법을 tooconnect tooa SQL 데이터베이스입니다. hello 데이터 집합 테이블을 입력으로 사용 되 고 파이프라인의 hello 활동에 대 한 출력을 정의 합니다.   

> [!IMPORTANT]
> 로 표시 되어야 합니다 hello 파이프라인에서 데이터 집합을이 생성 하지 않는 한 **외부**합니다. 이 설정은 일반적으로 파이프라인의 첫 번째 활동의 tooinputs를 적용합니다.   


## <a name="Type"></a> 데이터 집합 형식
hello 데이터 저장소를 사용 하면에 hello 데이터 집합의 hello 유형에 따라 다릅니다. Hello 다음 Data Factory에서 지 원하는 데이터 저장소 목록에 대 한 표를 참조 하십시오. 데이터 저장소 toolearn 클릭 toocreate 연결 된 서비스와 해당 데이터에 대 한 데이터 집합 저장 하는 방법입니다.

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> *가 있는 데이터 저장소는 서비스(IaaS)로서 온-프레미스 또는 Azure 인프라에 있을 수 있습니다. 이러한 데이터 저장소 요구 tooinstall [데이터 관리 게이트웨이](data-factory-data-management-gateway.md)합니다.

Hello 데이터 집합의 hello 유형이 너무 설정 hello 이전 단원의 hello 예에서**AzureSqlTable**합니다. 마찬가지로, Azure Blob 데이터 집합의 경우 hello 유형이 hello 데이터 집합의 설정 되어 너무**AzureBlob**hello JSON 뒤에 나타난 것 처럼:

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

## <a name="Structure"></a>데이터 집합 구조
hello **구조** 섹션은 선택 사항입니다. 이름 및 데이터 형식 열의 컬렉션을 포함 하 여 hello 데이터 집합의 hello 스키마를 정의 합니다. Hello 구조 섹션 tooprovide 형식 정보를 사용 하는 tooconvert 형식과 hello 소스 toohello 대상에서 매핑되지 않은 열은 사용할 수 있습니다. 다음 예제는 hello, hello 데이터 집합에 3 개의 열이: `slicetimestamp`, `projectname`, 및 `pageviews`합니다. 형식은 각각 String, String 및 Decimal입니다.

```json
structure:  
[
    { "name": "slicetimestamp", "type": "String"},
    { "name": "projectname", "type": "String"},
    { "name": "pageviews", "type": "Decimal"}
]
```

Hello 구조에서 각 열에 다음 속성이 hello를 포함 되어 있습니다.

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| name |Hello 열의 이름입니다. |예 |
| type |Hello 열의 데이터 형식입니다.  |아니요 |
| culture |. Hello 형식이.NET 유형 때 사용 되는.NET 기반 culture toobe: `Datetime` 또는 `Datetimeoffset`합니다. hello 기본값은 `en-us`합니다. |아니요 |
| format |문자열 toobe hello 형식이.NET 형식이 때 사용 되는 형식: `Datetime` 또는 `Datetimeoffset`합니다. |아니요 |

hello 다음과 같은 지침이 도움이 tooinclude 정보를 구성 하는 경우 및 hello에 어떤 tooinclude 결정 **구조** 섹션.

* **구조화 된 데이터 원본에 대 한**, 원본 열 toosink 열 매핑와 이름이 동일 hello 하지는 경우에 hello 구조 섹션을 지정 합니다. 이러한 종류의 구조화 된 데이터 소스 자체 hello 데이터와 함께 데이터 스키마 및 형식 정보를 저장합니다. 구조화된 데이터 원본의 예로 SQL Server, Oracle 및 Azure 테이블이 있습니다. 
  
    형식 정보를 구조화 된 데이터 원본에 대해 사용할 수 있는 대로 hello 구조 섹션 포함 않는 경우 형식 정보가 포함 되지 않습니다.
* **읽은 데이터 원본 (특히 Blob storage)에 스키마에 대 한**, hello 데이터와 스키마 또는 형식 정보를 저장 하지 않고 toostore 데이터를 선택할 수 있습니다. 이러한 유형의 데이터 원본에 대 한 toomap 원본 열 toosink 열을 사용할 때 구조를 포함 합니다. 또한 구조 때 포함 hello 데이터 집합은 복사 작업에 대 한 입력 및 원본 데이터 집합의 데이터 형식이 hello 싱크에 대 한 변환된 toonative 형식 이어야 합니다. 
    
    데이터 팩터리의 지원 다음 구조에 대 한 형식 정보를 제공 하는 값에는 hello: **Int16, Int32, Int64, 단일, Double, Decimal, 바이트, 부울, 문자열, Guid, Datetime, Datetimeoffset 및 Timespan**합니다. 이러한 값은 CLS(공용 언어 사양) 규격 .NET 기반 type 값입니다.

데이터 팩터리 tooa 싱크 데이터 저장소를 저장 하는 원본 데이터에서 데이터를 이동할 때 자동으로 형식 변환을 수행 합니다. 
  

## <a name="dataset-availability"></a>데이터 집합 가용성
hello **가용성** 데이터 집합의 섹션 hello 처리 창 (예를 들어 매시간, 매일 또는 매주) hello 데이터 집합을 정의 합니다. 활동 기간에 대한 자세한 내용은 [예약 및 실행](data-factory-scheduling-and-execution.md)을 참조하세요.

hello 출력 데이터 집합 중 하나 생성 매시간 또는 hello 입력된 데이터 집합은 매 hello 가용성 섹션 뒤에 지정 합니다.

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 1    
}
```

Hello 파이프라인에는 시작 및 종료 시간을 다음 hello 하는 경우:  

```json
    "start": "2016-08-25T00:00:00Z",
    "end": "2016-08-25T05:00:00Z",
```

hello 출력 데이터 집합 생성 시간별 hello 파이프라인 내에서 시작 및 종료 시간입니다. 따라서 이 파이프라인에서는 각 활동 기간(오전 12-1시, 오전 1-2시, 오전 2-3시, 오전 3-4시, 오전 4-5시)마다 하나씩 5개의 데이터 집합 조각이 생성됩니다. 

hello 다음 표에서 속성 hello 가용성 섹션에서 사용할 수 있습니다.

| 속성 | 설명 | 필수 | 기본값 |
| --- | --- | --- | --- |
| frequency |데이터 집합 조각 프로덕션에 대 한 hello 시간 단위를 지정합니다.<br/><br/><b>지원되는 빈도</b>: 분, 시, 일, 주, 월 |예 |해당 없음 |
| interval |빈도에 대한 승수를 지정합니다.<br/><br/>"X 주파수 간격" 결정 얼마나 자주 hello 조각이 생성 됩니다. 예를 들어 조각화는 시간 단위로 데이터 집합 toobe hello 필요, 설정한 <b>주파수</b> 너무<b>시간</b>, 및 <b>간격</b> 너무<b>1</b>합니다.<br/><br/>지정 하는 경우 유의 **주파수** 으로 **분**, 15 보다 작은 간격 toono hello 설정 해야 합니다. |예 |해당 없음 |
| style |Hello 시작 또는 끝 hello 간격의 hello 분할 영역을 생성 해야 하는지 여부를 지정 합니다.<ul><li>StartOfInterval</li><li>EndOfInterval</li></ul>경우 **주파수** 너무 설정**월**, 및 **스타일** 너무 설정**EndOfInterval**, hello hello 달의 마지막 날에 생성 됩니다. 경우 **스타일** 너무 설정**StartOfInterval**, 달의 첫 번째 날 hello에 hello 조각이 생성 됩니다.<br/><br/>경우 **주파수** 너무 설정 되어**일**, 및 **스타일** 너무 설정 되어**EndOfInterval**, 지난 1 시간 동안 hello 하루의 hello에 hello 조각이 생성 됩니다.<br/><br/>경우 **주파수** 너무 설정 되어**시간**, 및 **스타일** 너무 설정**EndOfInterval**, hello 조각이 hello 시간 hello 끝에 생성 됩니다. 예를 들어, hello 오후 1-2 시의 기간에 조각의 hello 조각이 오후 2 시 생성 됩니다. |아니요 |EndOfInterval |
| anchorDateTime |Hello 스케줄러 toocompute 데이터 집합 분할 영역 경계에 의해 사용 된 시간에 hello 절대 위치를 정의 합니다. <br/><br/>이 propoerty hello 빈도 지정 된 것 보다 더 세부적인 날짜 부분이 있으면 hello 보다 세부적인 파트는 무시 됩니다. 예를 들어 경우 hello, **간격** 은 **매시간** (빈도: 시간 및 간격: 1), 및 hello **anchorDateTime** 포함 **, 분, 초**, 분 및 초 부분을 다음 hello **anchorDateTime** 무시 됩니다. |아니요 |01/01/0001 |
| offset |어떤 hello에서 모든 데이터 집합 분할 영역의 시작과 끝을 향해 이동 하는 Timespan입니다. <br/><br/>경우에 두 **anchorDateTime** 및 **오프셋** hello 결과 결합 된 hello shift 지정 됩니다. |아니요 |해당 없음 |

### <a name="offset-example"></a>offset example
기본적으로 조각은 매일(`"frequency": "Day", "interval": 1`) 오전 12시(자정) UTC(협정 세계시)에 시작합니다. 대신 hello 시작 시간 toobe 오전 6 시 UTC 시간을 하려는 경우 hello hello 다음 코드 조각에에서 나와 있는 것 처럼 오프셋을 설정 합니다. 

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
### <a name="anchordatetime-example"></a>anchorDateTime 예제
다음 예제는 hello, hello dataset 23 시간 마다 한 번 생성 됩니다. hello 첫 번째 조각의 시작 하 여 지정 된 hello 시 **anchorDateTime**, 너무 설정 된`2017-04-19T08:00:00` (UTC)입니다.

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 23,    
    "anchorDateTime":"2017-04-19T08:00:00"    
}
```

### <a name="offsetstyle-example"></a>offset/style 예제
hello 다음 데이터 집합은 월별, 오전 8시 매월 세 번째 서비스로 hello에 생성 되 고 (`3.08:00:00`):

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "offset": "3.08:00:00", 
    "style": "StartOfInterval"
}
```

## <a name="Policy"></a>데이터 집합 정책
hello **정책** hello 데이터 집합 정의 섹션 hello 조건 정의 또는 데이터 집합 분할 영역 hello hello 조건을 충족 해야 합니다.

### <a name="validation-policies"></a>정책 유효성 검사
| 정책 이름 | 설명 | 너무 적용| 필수 | 기본값 |
| --- | --- | --- | --- | --- |
| minimumSizeMB |Hello 데이터에 유효성을 검사 **Azure Blob 저장소** 충족 hello 최소 크기 요구 사항 (메가바이트)입니다. |Azure Blob 저장소 |아니요 |해당 없음 |
| minimumRows |Hello 데이터에 유효성을 검사 한 **Azure SQL 데이터베이스** 또는 **Azure 테이블** hello 최소 행 수를 포함 합니다. |<ul><li>Azure SQL 데이터베이스</li><li>Azure 테이블</li></ul> |아니요 |해당 없음 |

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

**minimumRows:**

```json
"policy":
{
    "validation":
    {
        "minimumRows": 100
    }
}
```

### <a name="external-datasets"></a>외부 데이터 집합
외부 데이터 집합은 hello hello 데이터 팩터리에서 실행 중인 파이프라인에서 생성 하지 않은 것입니다. Hello 데이터 집합으로 표시 되어 있으면 **외부**, hello **ExternalData** 정책 hello 데이터 집합 분할 영역 가용성의 정의 된 tooinfluence hello 동작을 수 있습니다.

Data Factory에서 데이터 집합을 생성하지 않는 한 **external**로 표시되어야 합니다. 이 설정은 활동 또는 파이프라인 체인 사용 되지 않은 경우 파이프라인의 첫 번째 활동의 toohello 입력 일반적으로 적용 됩니다.

| 이름 | 설명 | 필수 | 기본값 |
| --- | --- | --- | --- |
| dataDelay |hello toodelay hello hello hello에 대 한 외부 데이터의 hello 가용성 확인 시간은 조각입니다. 예를 들어 이 설정을 사용하여 시간별 검사를 지연할 수 있습니다.<br/><br/>hello 설정의 현재 시간 toohello를만 적용 됩니다.  예를 들어 지금 바로 오후 1시 이므로이 값은 10 분 hello 유효성 검사 오후 1 시 10 분에 시작 합니다.<br/><br/>참고가이 설정은 지난 hello에서 분할 영역에 영향을 주지 않습니다. **조각 종료 시간** + **dataDelay** < **현재 시간**인 경우 조각은 지연 없이 처리됩니다.<br/><br/>23시 59분 보다 큰 시간 hello를 사용 하 여 시간을 지정할 `day.hours:minutes:seconds` 형식입니다. 예를 들어, toospecify 24 시간, 24시: 00을 사용 하지 마십시오. 1.00:00:00을 사용합니다. 24:00:00을 사용하면 24일(24.00:00:00)로 처리됩니다. 1일 4시간의 경우 1:04:00:00을 지정합니다. |아니요 |0 |
| retryInterval |hello 실패 및 hello 다음 시도 사이의 대기 시간입니다. 이 설정은 toopresent 시간이 적용 됩니다. Hello 후 hello 다음 시도 hello 이전 시도 실패 한 경우 **retryInterval** 기간입니다. <br/><br/>지금 바로 오후 1시 이면 hello 첫 번째 시도 시작 하기. Hello 기간 toocomplete hello 첫 번째 유효성 검사 1 분 이며 hello 작업이 실패 했습니다 hello 다음 재시도에 않은 경우에 1시 + 1 분 (기간) + 1 분 (다시 시도 간격) = 오후 1시 02분 합니다. <br/><br/>지난 hello에 조각에 대 한 지연 되지 않습니다. hello 재시도 즉시 전파 합니다. |아니요 |00:01:00 (1분) |
| retryTimeout |각 다시 시도 대 한 hello 제한 시간입니다.<br/><br/>이 속성을 설정 하는 경우 too10 분, 10 분 이내에 hello 유효성 검사를 완료 해야 합니다. 10 분 tooperform hello 유효성 검사 보다 시간이 오래 걸리는 경우 제한 시간이 초과 hello에 다시 시도 합니다.<br/><br/>Hello 유효성 검사 시간 초과 대 한 모든 시도 hello 조각으로 표시 됩니다 **TimedOut**합니다. |아니요 |00:10:00 (10분) |
| maximumRetry |hello 횟수 toocheck hello 외부 데이터의 가용성을 hello에 대 한입니다. hello 최대 허용 값은 10입니다. |아니요 |3 |


## <a name="create-datasets"></a>데이터 집합 만들기
다음 도구 또는 SDK 중 하나를 사용하여 데이터 집합을 만들 수 있습니다. 

- 복사 마법사 
- Azure Portal
- Visual Studio
- PowerShell
- Azure Resource Manager 템플릿
- REST API
- .NET API

이러한 도구나 Sdk 중 하나를 사용 하 여 파이프라인 및 데이터 집합을 만들기 위한 단계별 지침에 대 한 자습서를 따라 hello를 참조 하십시오.
 
- [데이터 변환 활동을 사용하여 파이프라인 빌드](data-factory-build-your-first-pipeline.md)
- [데이터 이동 활동을 사용하여 파이프라인 빌드](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)

파이프라인을 만들고 배포한 후에 관리 및 모니터링할 수 있습니다를 사용 하 여 파이프라인 hello Azure 포털 블레이드 또는 hello 모니터링 및 관리 응용 프로그램입니다. Hello 다음 단계별 지침에 대 한 항목을 참조 하십시오. 

- [Azure Portal 블레이드를 사용하여 파이프라인 모니터링 및 관리](data-factory-monitor-manage-pipelines.md)
- [모니터링 하 고 hello 모니터링 및 관리 응용 프로그램을 사용 하 여 파이프라인 관리](data-factory-monitor-manage-app.md)


## <a name="scoped-datasets"></a>범위가 지정된 데이터 집합
Hello를 사용 하 여 범위 지정 된 tooa 파이프라인 된 데이터 집합을 만들 수 있습니다 **데이터 집합** 속성입니다. 이러한 데이터 집합은 다른 파이프라인의 활동이 아니라 이 파이프라인 내의 활동에서만 사용할 수 있습니다. 다음 예제는 hello와 두 개의 데이터 집합 (InputDataset rdc 및 OutputDataset rdc) toobe hello 파이프라인 내에서 사용 되는 파이프라인을 정의 합니다.  

> [!IMPORTANT]
> 범위가 지정 된 데이터 집합 일회성 파이프라인만 지원 됩니다 (여기서 **pipelineMode** 너무 설정**OneTime**). 자세한 내용은 [일회성 파이프라인](data-factory-create-pipelines.md#onetime-pipeline) 을 참조하세요.
>
>

```json
{
    "name": "CopyPipeline-rdc",
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
                        "name": "InputDataset-rdc"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataset-rdc"
                    }
                ],
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1,
                    "style": "StartOfInterval"
                },
                "name": "CopyActivity-0"
            }
        ],
        "start": "2016-02-28T00:00:00Z",
        "end": "2016-02-28T00:00:00Z",
        "isPaused": false,
        "pipelineMode": "OneTime",
        "expirationTime": "15.00:00:00",
        "datasets": [
            {
                "name": "InputDataset-rdc",
                "properties": {
                    "type": "AzureBlob",
                    "linkedServiceName": "InputLinkedService-rdc",
                    "typeProperties": {
                        "fileName": "emp.txt",
                        "folderPath": "adftutorial/input",
                        "format": {
                            "type": "TextFormat",
                            "rowDelimiter": "\n",
                            "columnDelimiter": ","
                        }
                    },
                    "availability": {
                        "frequency": "Day",
                        "interval": 1
                    },
                    "external": true,
                    "policy": {}
                }
            },
            {
                "name": "OutputDataset-rdc",
                "properties": {
                    "type": "AzureBlob",
                    "linkedServiceName": "OutputLinkedService-rdc",
                    "typeProperties": {
                        "fileName": "emp.txt",
                        "folderPath": "adftutorial/output",
                        "format": {
                            "type": "TextFormat",
                            "rowDelimiter": "\n",
                            "columnDelimiter": ","
                        }
                    },
                    "availability": {
                        "frequency": "Day",
                        "interval": 1
                    },
                    "external": false,
                    "policy": {}
                }
            }
        ]
    }
}
```

## <a name="next-steps"></a>다음 단계
- 파이프라인에 대한 자세한 내용은 [파이프라인 만들기](data-factory-create-pipelines.md)를 참조하세요. 
- 파이프라인을 예약하고 실행하는 방법에 대한 자세한 내용은 [Azure Data Factory 예약 및 실행](data-factory-scheduling-and-execution.md)을 참조하세요. 

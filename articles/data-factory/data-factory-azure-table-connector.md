---
title: "Azure 테이블에서 데이터를 aaaMove | Microsoft Docs"
description: "자세한 내용은 방법 toomove 한 데이터를 Azure 데이터 팩터리를 사용 하 여 Azure 테이블 저장소에서."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 07b046b1-7884-4e57-a613-337292416319
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jingwang
ms.openlocfilehash: 3dc3da6d88854674a9108b600534bc5d07575f15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-table-using-azure-data-factory"></a>Azure 데이터 팩터리를 사용 하 여 Azure 테이블에서 데이터 tooand 이동
이 문서에서는 toouse Azure 테이블 저장소에서 Azure Data Factory toomove 데이터에서 복사 작업을 hello 하는 방법을 설명 합니다. Hello에 기반 [데이터 이동 작업](data-factory-data-movement-activities.md) hello 복사 작업으로 데이터 이동에 대 한 일반적인 개요를 제공 하는 문서입니다. 

데이터 테이블 저장소 tooAzure 저장 하거나 Azure 테이블 저장소 지원 tooany 싱크 데이터에서 저장할 모든 지원 되는 원본에서 데이터를 복사할 수 있습니다. 목록이 hello 복사 작업에서 원본 또는 싱크도 지 원하는 데이터 저장소에 대 한 참조 hello [데이터 저장소를 지원](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 테이블입니다. 

## <a name="getting-started"></a>시작
다른 도구/API를 사용하여 Azure Table Storage 간에 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다.

hello 가장 쉬운 방법은 toocreate 파이프라인은 toouse hello **복사 마법사**합니다. 참조 [자습서: 복사 마법사를 사용 하 여 파이프라인을 만들고](data-factory-copy-data-wizard-tutorial.md) 간략 한 설명이 hello 복사 데이터 마법사를 사용 하 여 파이프라인을 만드는 방법에 대 한 합니다.

다음 도구 toocreate 파이프라인 hello을 사용할 수 있습니다: **Azure 포털**, **Visual Studio**, **Azure PowerShell**, **Azure 리소스 관리자 템플릿** , **.NET API**, 및 **REST API**합니다. 참조 [복사 활동 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 단계별 지침 toocreate 복사 작업으로 파이프라인에 대 한 합니다. 

Hello 도구 또는 Api를 사용 하는지 여부를 hello tooa 싱크 데이터 저장소를 저장 하는 원본 데이터에서 데이터를 이동 하는 파이프라인 단계 toocreate 다음을 수행 합니다. 

1. 만들 **연결 된 서비스** toolink 입력 및 출력 데이터 저장소 tooyour 데이터 팩터리입니다.
2. 만들 **데이터 집합** 입력 및 출력 toorepresent hello에 대 한 데이터 복사 작업을 합니다. 
3. 입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다. 

Hello 마법사를 사용 하 여 이러한 데이터 팩터리 엔터티 (연결 된 서비스, 데이터 집합 및 hello 파이프라인)에 대 한 JSON 정의를 자동으로 만들어집니다. 도구/Api (제외.NET API)를 사용 하면 hello JSON 형식을 사용 하 여이 Data Factory 엔터티를 정의 합니다.  샘플 은/Azure 테이블 저장소에서 사용 되는 toocopy 데이터를 Data Factory 엔터티에 대 한 JSON 정의 가진 [JSON 예제](#json-examples) 이 문서의 섹션. 

사용 되는 toodefine Data Factory 엔터티에 특정 tooAzure 테이블 저장소는 JSON 속성에 대 한 세부 정보를 제공 하는 다음 섹션 hello: 

## <a name="linked-service-properties"></a>연결된 서비스 속성
두 가지가 toolink Azure blob 저장소 tooan Azure 데이터 팩터리에 연결 된 서비스의 사용할 수 있습니다. **AzureStorage** 연결된 서비스 및 **AzureStorageSas** 연결된 서비스입니다. Azure 저장소 연결 서비스 hello 전역 액세스 toohello Azure 저장소와 hello data factory에 제공 합니다. 반면 hello Azure 저장소 SAS (공유 액세스 서명) 연결 된 서비스 시간 제한/범위 액세스 toohello Azure 저장소와 hello data factory에 제공 합니다. 이 두 연결된 서비스에는 다른 차이가 없습니다. 필요에 맞는 hello 연결 된 서비스를 선택 합니다. hello 다음 섹션에서는 더욱 자세히 설명에 두 개의 연결 된 서비스입니다.

[!INCLUDE [data-factory-azure-storage-linked-services](../../includes/data-factory-azure-storage-linked-services.md)]

## <a name="dataset-properties"></a>데이터 집합 속성
섹션 및 데이터 집합 정의에 사용 가능한 속성의 전체 목록을 보려면 hello [데이터 집합을 만드는](data-factory-create-datasets.md) 문서. 구조, 가용성 및 JSON 데이터 집합의 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다(Azure SQL, Azure blob, Azure 테이블 등).

hello typeProperties 섹션 hello 데이터 저장소에 hello 데이터의 hello 위치에 대 한 정보를 제공 및 데이터 집합의 각 유형에 대해과 다릅니다. hello **typeProperties** 형식의 hello 데이터 집합에 대 한 섹션 **AzureTable** hello 다음과 같은 속성에 있습니다.

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| tableName |연결 된 서비스는 hello Azure 테이블 데이터베이스 인스턴스의 hello 테이블의 이름은 참조 합니다. |예. 를 azureTableSourceQuery 없이 tableName을 지정 하는 경우 hello 테이블의 모든 레코드가 복사한 toohello 대상 됩니다. Hello 쿼리를 충족 하는 hello 테이블에서 레코드는 azureTableSourceQuery도 지정 되어 경우 복사한 toohello 대상 합니다. |

### <a name="schema-by-data-factory"></a>Data Factory에서의 스키마
Azure 테이블과 같은 스키마가 없는 데이터 저장소에 대 한 hello 데이터 팩터리 서비스 hello 같은 방법으로 다음 중 하나에 hello 스키마를 유추 합니다.

1. Hello를 사용 하 여 데이터의 hello 구조를 지정 하는 경우 **구조** hello 데이터 집합 정의 hello 데이터 팩터리 서비스에서 속성 hello 스키마와이 구조를 인식 합니다. 이 경우 행에 열의 값이 포함되어 있지 않으면 null 값이 제공됩니다.
2. Hello를 사용 하 여 hello 데이터 구조를 지정 하지 않으면 **구조** hello 데이터 집합 정의 데이터 팩터리의 속성 hello 데이터의 첫 번째 행 hello를 사용 하 여 hello 스키마를 유추 합니다. 이 경우 첫 번째 행 hello hello 전체 스키마를 포함 하지 않으면 일부 열 복사 작업의 hello 결과에서 누락 됩니다.

따라서 스키마 없는 데이터 원본에 대 한 hello 것이 가장 좋습니다 hello를 사용 하 여 데이터의 toospecify hello 구조 **구조** 속성입니다.

## <a name="copy-activity-properties"></a>복사 작업 속성
섹션 및 활동 정의에 사용 가능한 속성의 전체 목록을 참조 hello [파이프라인 만들기](data-factory-create-pipelines.md) 문서. 이름, 설명, 입력/출력 데이터 집합, 정책 등의 속성은 모든 유형의 활동에 사용할 수 있습니다.

속성 hello에 hello 활동의 hello typeProperties 섹션에서 사용할 수 있는 각 활동 유형에 다른 손 다릅니다. 복사 작업은 원본 및 싱크의 hello 형식에 따라 변경합니다.

**AzureTableSource** hello 다음과 같은 섹션 typeProperties의에서 속성을 지원 합니다.

| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| AzureTableSourceQuery |사용자 지정 쿼리 tooread 데이터 hello를 사용 합니다. |Azure 테이블 쿼리 문자열. Hello 다음 섹션의 예제를 참조 하십시오. |아니요. 를 azureTableSourceQuery 없이 tableName을 지정 하는 경우 hello 테이블의 모든 레코드가 복사한 toohello 대상 됩니다. Hello 쿼리를 충족 하는 hello 테이블에서 레코드는 azureTableSourceQuery도 지정 되어 경우 복사한 toohello 대상 합니다. |
| azureTableSourceIgnoreTableNotFound |테이블의 hello 예외를 무시할지 존재 하지 여부를 나타냅니다. |TRUE<br/>FALSE |아니요 |

### <a name="azuretablesourcequery-examples"></a>azureTableSourceQuery 예제
Azure 테이블 열이 문자열 형식인 경우:

```JSON
azureTableSourceQuery": "$$Text.Format('PartitionKey ge \\'{0:yyyyMMddHH00_0000}\\' and PartitionKey le \\'{0:yyyyMMddHH00_9999}\\'', SliceStart)"
```

Azure 테이블 열이 날짜/시간 형식인 경우:

```JSON
"azureTableSourceQuery": "$$Text.Format('DeploymentEndTime gt datetime\\'{0:yyyy-MM-ddTHH:mm:ssZ}\\' and DeploymentEndTime le datetime\\'{1:yyyy-MM-ddTHH:mm:ssZ}\\'', SliceStart, SliceEnd)"
```

**AzureTableSink** hello 다음과 같은 섹션 typeProperties의에서 속성을 지원 합니다.

| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| azureTableDefaultPartitionKeyValue |기본 파티션 키 값 hello 싱크에서 사용할 수 있는 합니다. |문자열 값 |아니요 |
| azureTablePartitionKeyName |해당 값은 파티션 키로 사용 하는 hello 열의 이름을 지정 합니다. 지정 하지 않으면 AzureTableDefaultPartitionKeyValue hello 파티션 키로 사용 됩니다. |열 이름 |아니요 |
| azureTableRowKeyName |해당 열 값은 행 키로 사용 되는 hello 열의 이름을 지정 합니다. 지정하지 않으면 각 행에 GUID를 사용합니다. |열 이름 |아니요 |
| azureTableInsertType |Azure 테이블에 hello 모드 tooinsert 데이터입니다.<br/><br/>이 속성은 파티션 및 행 키 일치 하는 hello 출력 테이블의 기존 행에는 값을 바꾸거나 병합 있는지 여부를 제어 합니다. <br/><br/>이러한 설정을 (병합 및 대체) 작동 방법에 대해 toolearn 참조 [삽입 또는 병합 엔터티](https://msdn.microsoft.com/library/azure/hh452241.aspx) 및 [삽입 또는 교체 엔터티](https://msdn.microsoft.com/library/azure/hh452242.aspx) 항목. <br/><br> 두 옵션 모두 hello 입력에 존재 하지 않는 hello 출력 테이블에 행을 삭제 및 hello 테이블 수준이 아닌 hello 행 수준에서이 설정을 적용 됩니다. |병합(기본값)<br/>바꾸기 |아니요 |
| writeBatchSize |Hello writeBatchSize 또는 writebatchtimeout에 도달 하는 경우에 hello Azure 테이블에 데이터를 삽입 합니다. |정수(행 수) |아니요(기본값: 10000) |
| writeBatchTimeout |Hello writeBatchSize 또는 writebatchtimeout에 도달 하는 경우 hello Azure 테이블에 데이터 삽입 |timespan<br/><br/>예: "00:20:00"(20분) |더 (기본 toostorage 클라이언트 기본 제한 시간 값인 90 초) |

### <a name="azuretablepartitionkeyname"></a>azureTablePartitionKeyName
AzureTablePartitionKeyName hello으로 hello 대상 열을 사용 하기 전에 hello 변환기 JSON 속성을 사용 하 여 원본 열 tooa 대상 열을 매핑하십시오.

다음 예제는 hello, 원본 열 DivisionID 매핑된 toohello 대상 열입니다.: DivisionID 합니다.  

```JSON
"translator": {
    "type": "TabularTranslator",
    "columnMappings": "DivisionID: DivisionID, FirstName: FirstName, LastName: LastName"
}
```
hello DivisionID hello 파티션 키로 지정 됩니다.

```JSON
"sink": {
    "type": "AzureTableSink",
    "azureTablePartitionKeyName": "DivisionID",
    "writeBatchSize": 100,
    "writeBatchTimeout": "01:00:00"
}
```
## <a name="json-examples"></a>JSON 예
hello 다음 예에서는 샘플 JSON 정의 사용 하 여 toocreate 파이프라인을 사용할 수 있는 [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md) 또는 [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 또는 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)합니다. 보여 줍니다 어떻게 toocopy 데이터 tooand Azure 테이블 저장소 및 Azure Blob 데이터베이스입니다. 그러나 데이터를 복사할 수 있습니다 **직접** 지원 hello 싱크 hello 소스 tooany 중 어디에서 든 합니다. 자세한 내용은의 "지원 되는 데이터 저장소와 형식" hello 섹션 참조 [복사 작업을 사용 하 여 데이터를 이동](data-factory-data-movement-activities.md)합니다.

## <a name="example-copy-data-from-azure-table-tooazure-blob"></a>예: Azure 테이블 tooAzure Blob에서에서 데이터를 복사 합니다.
다음 샘플에서는 hello:

1. [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) 형식의 연결된 서비스(테이블 및 blob에 모두 사용됨)
2. [AzureTable](#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)입니다.
3. [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)
4. hello [파이프라인](data-factory-create-pipelines.md) 사용 하 여 복사 작업으로 [AzureTableSource](#activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)합니다.

hello 예제 1 시간 마다 Azure 테이블 tooa blob에 toohello 기본 파티션에 속한 데이터를 복사 합니다. 이 예제에 사용 되는 hello JSON 속성 hello 샘플 다음 섹션에 설명 되어 있습니다.

**Azure 저장소 연결된 서비스:**

```JSON
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
Azure Data Factory는 두 가지 유형의 Azure Storage 연결된 서비스: **AzureStorage** 및 **AzureStorageSas**를 제공합니다. 에 대 한 hello 첫 번째 사용, hello 계정 키를 포함 하는 hello 연결 문자열을 지정 하 고 hello 공유 액세스 서명 (SAS) Uri를 지정 하면 이후 hello에 대 한 키를 누릅니다. 자세한 내용은 [연결된 서비스](#linked-service-properties) 섹션을 참조하세요.  

**Azure 테이블 입력 데이터 집합:**

hello 샘플 Azure 테이블에 포함 된 "MyTable" 테이블을 만들었다고 가정 합니다.

설정 "외부": "true" 알리고 hello 데이터 팩터리 서비스 hello 데이터 집합의 데이터 팩터리 외부 toohello hello data factory에는 활동에 의해 생성 되지 않습니다.

```JSON
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

**Azure Blob 출력 데이터 집합:**

데이터가 새 blob tooa 1 시간 마다 기록 됩니다 (빈도: 시, 간격: 1). hello blob에 대 한 hello 폴더 경로 처리 중인 hello 조각의 hello 시작 시간에 따라 동적으로 평가 됩니다. hello 폴더 경로 hello 시작 시간의 연도, 월, 일 및 시간 부분을 사용 합니다.

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": "\t",
        "rowDelimiter": "\n"
      }
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

**AzureTableSource 및 BlobSink를 사용하는 파이프라인의 복사 작업:**

hello 파이프라인에 포함 된 구성된 toouse 않은 복사 작업 입력 및 출력 데이터 집합을 hello 및 예약 된 toorun 1 시간입니다. Hello 파이프라인 JSON 정의에서 hello **소스** 형식이 너무 설정**AzureTableSource** 및 **싱크** 형식이 너무 설정**BlobSink**합니다. 지정 된 hello SQL 쿼리 **AzureTableSourceQuery** 속성 hello에서에서 데이터를 선택 hello 기본 파티션에 모든 시간 toocopy 합니다.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
            {
                "name": "AzureTabletoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                      {
                        "name": "AzureTableInput"
                    }
                ],
                "outputs": [
                      {
                            "name": "AzureBlobOutput"
                      }
                ],
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
            }
         ]    
    }
}
```

## <a name="example-copy-data-from-azure-blob-tooazure-table"></a>예: Azure Blob tooAzure 테이블에서에서 데이터를 복사 합니다.
다음 샘플에서는 hello:

1. [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) 형식의 연결된 서비스(테이블 및 blob에 모두 사용됨)
2. [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)입니다.
3. [AzureTable](#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)입니다.
4. hello [파이프라인](data-factory-create-pipelines.md) 사용 하 여 복사 작업으로 [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) 및 [AzureTableSink](#copy-activity-properties)합니다.

hello 샘플에 1 시간 마다 Azure blob tooan Azure 테이블에서에서 시계열 데이터 복사합니다. 이 예제에 사용 되는 hello JSON 속성 hello 샘플 다음 섹션에 설명 되어 있습니다.

**Azure 저장소 연결된 서비스(Azure 테이블 및 Blob용):**

```JSON
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

Azure Data Factory는 두 가지 유형의 Azure Storage 연결된 서비스: **AzureStorage** 및 **AzureStorageSas**를 제공합니다. 에 대 한 hello 첫 번째 사용, hello 계정 키를 포함 하는 hello 연결 문자열을 지정 하 고 hello 공유 액세스 서명 (SAS) Uri를 지정 하면 이후 hello에 대 한 키를 누릅니다. 자세한 내용은 [연결된 서비스](#linked-service-properties) 섹션을 참조하세요.

**Azure Blob 입력 데이터 집합:**

데이터는 매시간 새 blob에 선택됩니다(frequency: hour, interval: 1). hello 폴더 경로 파일 이름은 hello blob에 대 한 처리 중인 hello 조각의 hello 시작 시간에 따라 동적으로 평가 됩니다. 연도, 월 및 일 부분은 hello 시작 시간의 hello 폴더 경로 사용 하 고 파일 이름을 hello 시작 시간의 시간 부분을 hello를 사용 합니다. "external": "true" 설정을 알리고 hello 데이터 팩터리 서비스 hello 데이터 집합의 데이터 팩터리 외부 toohello hello data factory에는 활동에 의해 생성 되지 않습니다.

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": "\n"
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

**Azure 테이블 출력 데이터 집합:**

hello 샘플 Azure 테이블에 "MyTable" 라는 이름의 데이터 tooa 테이블에 복사 합니다. 와 Azure 테이블 만들기 hello Blob CSV 파일 toocontain 예상 대로 동일한 수의 열을 hello 합니다. 새 행 1 시간 마다 toohello 테이블을 추가 됩니다.

```JSON
{
  "name": "AzureTableOutput",
  "properties": {
    "type": "AzureTable",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "tableName": "MyOutputTable"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

**BlobSource 및 AzureTableSink를 사용하는 파이프라인의 복사 작업:**

hello 파이프라인에 포함 된 구성된 toouse 않은 복사 작업 입력 및 출력 데이터 집합을 hello 및 예약 된 toorun 1 시간입니다. Hello 파이프라인 JSON 정의에서 hello **소스** 형식이 너무 설정**BlobSource** 및 **싱크** 형식이 너무 설정**AzureTableSink**합니다.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoTable",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureTableOutput"
          }
        ],
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
      }
      ]
   }
}
```
## <a name="type-mapping-for-azure-table"></a>Azure 테이블에 대한 형식 매핑
Hello에 설명 된 대로 [데이터 이동 작업](data-factory-data-movement-activities.md) 문서, 복사 작업 소스 형식 toosink 형식에서 자동 형식 변환 2 단계 방식을 따릅니다 hello로 수행 합니다.

1. 네이티브 소스 형식 too.NET 형식에서 변환
2. .NET 형식 toonative 싱크 형식에서 변환

를 너무 & Azure 테이블에서 데이터를 이동할 때 다음 hello [Azure 테이블 서비스에 의해 정의 된 매핑을](https://msdn.microsoft.com/library/azure/dd179338.aspx) 그 반대의 Azure 테이블 OData 형식 too.NET 형식에서 사용 됩니다.

| OData 데이터 형식 | .NET 형식 | 세부 정보 |
| --- | --- | --- |
| Edm.Binary |byte[] |Too64 KB 바이트 배열입니다. |
| Edm.Boolean |bool |부울 값입니다. |
| Edm.DateTime |DateTime |UTC(협정 세계시)로 표현되는 64비트 값입니다. hello는 범위가 서 기 1601 년 1 월 1 일 자정 12 시에서에서 시작 하는 날짜/시간 지원 (서기), UTC입니다. hello 범위 9999 년 12 월 31 일에 끝납니다. |
| Edm.Double |double |64비트 부동 소수점 값입니다. |
| Edm.Guid |Guid |전역적으로 고유한 128 비트 식별자입니다. |
| Edm.Int32 |Int32 |32비트 정수입니다. |
| Edm.Int64 |Int64 |64비트 정수입니다. |
| Edm.String |문자열 |UTF-16으로 인코딩된 값입니다. 문자열 값 too64 KB up 될 수 있습니다. |

### <a name="type-conversion-sample"></a>형식 변환 샘플
다음 예제는 hello 형식 변환이 있는 Azure Blob tooAzure 테이블에서에서 데이터를 복사 하기 위해 사용 되며

Hello Blob 데이터 집합 CSV 형태로 표시 하 고 3 개의 열이 포함 되어 가정 합니다. 그 중 하나가 hello 요일에 대 한 약어 프랑스어 이름을 사용 하 여 사용자 지정 날짜/시간 형식의 datetime 열입니다.

Hello 열에 대 한 형식 정의 함께 다음과 같이 hello Blob 원본 데이터 집합을 정의 합니다.

```JSON
{
    "name": " AzureBlobInput",
    "properties":
    {
         "structure":
          [
                { "name": "userid", "type": "Int64"},
                { "name": "name", "type": "String"},
                { "name": "lastlogindate", "type": "Datetime", "culture": "fr-fr", "format": "ddd-MM-YYYY"}
          ],
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/myfolder",
            "fileName":"myfile.csv",
            "format":
            {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "external": true,
        "availability":
        {
            "frequency": "Hour",
            "interval": 1,
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
Azure 테이블 OData 형식 too.NET 형식에서 hello 형식 매핑이 들어 hello 테이블 Azure 테이블의 스키마를 따르는 hello로 정의할는 있습니다.

**Azure 테이블 스키마:**

| 열 이름 | 형식 |
| --- | --- |
| userid |Edm.Int64 |
| name |Edm.String |
| lastlogindate |Edm.DateTime |

다음으로 hello Azure 테이블의 데이터 집합을 다음과 같이 정의 합니다. Hello 형식 정보가 데이터 저장소를 기본 hello에 이미 지정 되어 있으므로 hello 유형 정보와 함께 toospecify "구조" 섹션을 않아도 됩니다.

```JSON
{
  "name": "AzureTableOutput",
  "properties": {
    "type": "AzureTable",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "tableName": "MyOutputTable"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

이 경우 데이터 팩터리의 자동으로 유형 수행 hello 날짜/시간 필드를 포함 하 여 Blob tooAzure 테이블에서에서 데이터를 이동 하는 경우 "fr-fr" hello culture를 사용 하 여 hello 사용자 지정 날짜/시간 형식으로 변환 합니다.

> [!NOTE]
> 원본 데이터 집합 toocolumns 싱크 데이터 집합에서의 열을 toomap 참조 [Azure Data Factory에서 데이터 집합 열에 매핑](data-factory-map-columns.md)합니다.

## <a name="performance-and-tuning"></a>성능 및 튜닝
키에 대 한 toolearn Azure 데이터 팩터리 및 다양 한 방법으로 toooptimize에서 데이터 이동 (복사 작업)의 성능에 영향을 해당 요소를 참조 [복사 활동 성능 및 조정 가이드](data-factory-copy-activity-performance.md)합니다.

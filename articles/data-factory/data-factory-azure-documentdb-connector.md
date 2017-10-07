---
title: "aaaMove 데이터/Azure Cosmos DB에서 | Microsoft Docs"
description: "Azure Data Factory를 사용하여 Azure Cosmos DB 컬렉션 간 데이터를 이동하는 방법에 대해 알아봅니다."
services: data-factory, cosmosdb
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: c9297b71-1bb4-4b29-ba3c-4cf1f5575fac
ms.service: multiple
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: bd23ce4e004a972ce6f3e4165cfdea4f0c18fecc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-cosmos-db-using-azure-data-factory"></a>Azure 데이터 팩터리를 사용 하 여 Azure Cosmos DB에서 tooand 데이터 이동
이 문서에서는 toouse Azure Cosmos DB (DocumentDB API)에서 Azure Data Factory toomove 데이터 복사 작업을 hello 하는 방법을 설명 합니다. Hello에 기반 [데이터 이동 작업](data-factory-data-movement-activities.md) hello 복사 작업으로 데이터 이동에 대 한 일반적인 개요를 제공 하는 문서입니다. 

데이터 tooAzure Cosmos DB 저장 하거나 Azure Cosmos DB 지원 tooany 싱크 데이터에서 저장할 모든 지원 되는 원본에서 데이터를 복사할 수 있습니다. 목록이 hello 복사 작업에서 원본 또는 싱크도 지 원하는 데이터 저장소에 대 한 참조 hello [데이터 저장소를 지원](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 테이블입니다. 

> [!IMPORTANT]
> Azure Cosmos DB 커넥터만 DocumentDB API를 지원합니다.

toocopy 데이터도-는 를/다른 Cosmos DB 컬렉션 또는 JSON 파일에서 참조 [가져오기/내보내기 JSON 문서](#importexport-json-documents)합니다.

## <a name="getting-started"></a>시작
다른 도구/API를 사용하여 Azure Cosmos DB 간에 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다.

hello 가장 쉬운 방법은 toocreate 파이프라인은 toouse hello **복사 마법사**합니다. 참조 [자습서: 복사 마법사를 사용 하 여 파이프라인을 만들고](data-factory-copy-data-wizard-tutorial.md) 간략 한 설명이 hello 복사 데이터 마법사를 사용 하 여 파이프라인을 만드는 방법에 대 한 합니다.

다음 도구 toocreate 파이프라인 hello을 사용할 수 있습니다: **Azure 포털**, **Visual Studio**, **Azure PowerShell**, **Azure 리소스 관리자 템플릿** , **.NET API**, 및 **REST API**합니다. 참조 [복사 활동 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 단계별 지침 toocreate 복사 작업으로 파이프라인에 대 한 합니다. 

Hello 도구 또는 Api를 사용 하는지 여부를 hello tooa 싱크 데이터 저장소를 저장 하는 원본 데이터에서 데이터를 이동 하는 파이프라인 단계 toocreate 다음을 수행 합니다. 

1. 만들 **연결 된 서비스** toolink 입력 및 출력 데이터 저장소 tooyour 데이터 팩터리입니다.
2. 만들 **데이터 집합** 입력 및 출력 toorepresent hello에 대 한 데이터 복사 작업을 합니다. 
3. 입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다. 

Hello 마법사를 사용 하 여 이러한 데이터 팩터리 엔터티 (연결 된 서비스, 데이터 집합 및 hello 파이프라인)에 대 한 JSON 정의를 자동으로 만들어집니다. 도구/Api (제외.NET API)를 사용 하면 hello JSON 형식을 사용 하 여이 Data Factory 엔터티를 정의 합니다.  샘플 은/Cosmos DB에서 사용 되는 toocopy 데이터를 Data Factory 엔터티에 대 한 JSON 정의 가진 [JSON 예제](#json-examples) 이 문서의 섹션. 

다음 섹션 hello JSON 속성을 사용 하는 toodefine Data Factory 엔터티에 특정 tooCosmos DB에 대 한 세부 정보를 제공 합니다. 

## <a name="linked-service-properties"></a>연결된 서비스 속성
다음 표에서 hello JSON 요소 특정 tooAzure Cosmos DB 연결 된 서비스에 대 한 설명을 제공 합니다.

| **속성** | **설명** | **필수** |
| --- | --- | --- |
| type |hello type 속성 설정 해야 합니다: **DocumentDb** |예 |
| connectionString |Tooconnect tooAzure Cosmos DB 데이터베이스는 데 필요한 정보를 지정 합니다. |예 |

예제:

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```

## <a name="dataset-properties"></a>데이터 집합 속성
섹션 및 데이터 집합 정의에 사용 가능한 속성의 전체 목록은 toohello를 참조 하십시오 [데이터 집합을 만드는](data-factory-create-datasets.md) 문서. 구조, 가용성 및 JSON 데이터 집합의 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다(Azure SQL, Azure blob, Azure 테이블 등).

hello typeProperties 섹션 hello 데이터 저장소에 hello 데이터의 hello 위치에 대 한 정보를 제공 및 데이터 집합의 각 유형에 대해과 다릅니다. hello typeProperties 형식의 hello 데이터 집합에 대 한 섹션 **DocumentDbCollection** hello 다음과 같은 속성에 있습니다.

| **속성** | **설명** | **필수** |
| --- | --- | --- |
| collectionName |Hello Cosmos DB 문서 컬렉션의 이름입니다. |예 |

예제:

```JSON
{
  "name": "PersonCosmosDbTable",
  "properties": {
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
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
### <a name="schema-by-data-factory"></a>Data Factory에서의 스키마
Azure Cosmos DB와 같은 스키마가 없는 데이터 저장소에 대 한 hello 데이터 팩터리 서비스 hello 같은 방법으로 다음 중 하나에 hello 스키마를 유추 합니다.  

1. Hello를 사용 하 여 데이터의 hello 구조를 지정 하는 경우 **구조** hello 데이터 집합 정의 hello 데이터 팩터리 서비스에서 속성 hello 스키마와이 구조를 인식 합니다. 이 경우 행에 열의 값이 포함되어 있지 않으면 null 값이 제공됩니다.
2. Hello를 사용 하 여 데이터의 hello 구조를 지정 하지 않으면 **구조** hello 데이터 집합 정의 hello 데이터 팩터리 서비스에서 속성 hello 데이터의 첫 번째 행 hello를 사용 하 여 hello 스키마를 유추 합니다. 이 경우 hello 첫 번째 행에 hello 전체 스키마가 포함 되어 있지 않으면, 일부 열은 복사 작업의 hello 결과에서 누락 됩니다.

따라서 스키마 없는 데이터 원본에 대 한 hello 것이 가장 좋습니다 hello를 사용 하 여 데이터의 toospecify hello 구조 **구조** 속성입니다.

## <a name="copy-activity-properties"></a>복사 작업 속성
섹션 및 활동 정의에 사용 가능한 속성의 전체 목록은 toohello를 참조 하십시오 [파이프라인 만들기](data-factory-create-pipelines.md) 문서. 이름, 설명, 입력/출력 테이블, 정책 등의 속성은 모든 형식의 활동에 사용할 수 있습니다.

> [!NOTE]
> 복사 활동 hello 하나의 입력을 하나의 출력을 생성 합니다.

속성 hello에 hello 활동의 hello typeProperties 섹션에서 사용할 수 있는 반면 다 각 활동 유형 및 복사 작업의 원본 및 싱크 hello 형식에 따라 발생 한 경우.

원본 유형인 경우 복사 작업의 경우 **DocumentDbCollectionSource** hello 다음과 같은 속성에서 사용할 수 있는 **typeProperties** 섹션:

| **속성** | **설명** | **허용되는 값** | **필수** |
| --- | --- | --- | --- |
| 쿼리 |Hello tooread 데이터 쿼리를 지정 합니다. |Azure Cosmos DB에서 지원하는 쿼리 문자열입니다. <br/><br/>예: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"` |아니요 <br/><br/>지정 하지 않으면 실행 되는 SQL 문을 hello:`select <columns defined in structure> from mycollection` |
| nestingSeparator |문서 hello 특수 문자 tooindicate 중첩 |모든 character입니다. <br/><br/>Azure Cosmos DB는 중첩된 구조를 허용하는 JSON 문서용 NoSQL 저장소입니다. Azure 데이터 팩터리는 nestingSeparator 통해 사용자 toodenote 계층 구조를 사용 하면 "." 위의 예제 안녕하세요에. Hello 구분 기호 hello 복사 작업에서는 생성 3 명의 자식 요소가 있는 hello "Name" 개체 첫 번째, 중간 및 마지막를 따라 too"Name.First", "Name.Middle" 및 "Name.Last" hello에 테이블 정의 합니다. |아니요 |

**DocumentDbCollectionSink** hello 다음과 같은 속성을 지원 합니다.

| **속성** | **설명** | **허용되는 값** | **필수** |
| --- | --- | --- | --- |
| nestingSeparator |Hello 원본 열 이름 tooindicate 중첩 문서에에서 특수 문자 필요 합니다. <br/><br/>예를 들어 위의: `Name.First` hello 출력 테이블 생성 하는 hello Cosmos DB 문서의 JSON 구조를 다음 hello:<br/><br/>"Name": {<br/>    "First": "John"<br/>}, |문자는 사용 되는 tooseparate 중첩 수준입니다.<br/><br/>기본값은 `.`.(점)입니다. |문자는 사용 되는 tooseparate 중첩 수준입니다. <br/><br/>기본값은 `.`.(점)입니다. |
| writeBatchSize |TooAzure Cosmos DB 서비스 toocreate 문서를 요청 하는 병렬의 수입니다.<br/><br/>이 속성을 사용 하 여 Cosmos DB에서 데이터를 복사할 때 hello 성능을 미세 조정할 수 있습니다. 더 많은 병렬 요청 tooCosmos DB 보내지므로 writeBatchSize를 늘리면 성능이 향상을 기대할 수 있습니다. 그러나 조정을 tooavoid 해야 hello 오류 메시지가 발생할 수 있습니다: "요청 빈도가 높습니다."입니다.<br/><br/>제한은 문서의 크기, 문서에서 용어의 수, 대상 컬렉션의 인덱싱 정책 등 여러 가지 요인으로 결정됩니다. 복사 작업을 사용할 수 있습니다 더 나은 컬렉션 (예: S3) toohave hello 사용 가능한 대부분 처리량 (2,500 단위 수/초를 요청 하는 데 사용). |Integer |아니요(기본값: 5) |
| writeBatchTimeout |대기 시간이 초과 되기 전에 작업 toocomplete hello에 대 한 시간입니다. |timespan<br/><br/> 예: “00:30:00”(30분). |아니요 |

## <a name="importexport-json-documents"></a>JSON 문서 가져오기/내보내기
이 Cosmos DB 커넥터를 사용하여 다음을 쉽게 수행할 수 있습니다.

* Azure Blob, Azure Data Lake, 온-프레미스 파일 시스템 또는 기타 Azure Data Factory에서 지원하는 파일 기반 저장소 등 다양한 원본에서 Cosmos DB로 JSON 문서를 가져오기
* Cosmos DB 컬렉션에서 다양한 파일 기반 저장소로 JSON 문서 내보내기
* 두 Cosmos DB 컬렉션 간에 데이터를 있는 그대로 마이그레이션

tooachieve 이러한 스키마를 알 수 없는 복사 
* 복사 마법사를 사용 하는 경우 확인 hello **"으로 내보내기-tooJSON 파일 또는 Cosmos DB 컬렉션"** 옵션입니다.
* 때 JSON 편집을 사용 하 여 지정 하지 않으면 hello "구조" 섹션 Cosmos DB 데이터 집합에도 복사 작업에서 소스/싱크 Cosmos DB "nestingSeparator" 속성. tooimport / 내보내기 tooJSON 파일, hello 파일 저장소 데이터 집합의 형식 유형을 "filePattern" config "JsonFormat"로 지정 하 고 hello rest 형식 설정 건너뛰기, 참조 [JSON 형식](data-factory-supported-file-and-compression-formats.md#json-format) 세부 정보 섹션.

## <a name="json-examples"></a>JSON 예
hello 다음 예에서는 샘플 JSON 정의 사용 하 여 toocreate 파이프라인을 사용할 수 있는 [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md) 또는 [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 또는 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)합니다. 표시 방법을 toocopy 데이터 tooand Azure Cosmos DB 및 Azure Blob 저장소에서 합니다. 그러나 데이터를 복사할 수 있습니다 **직접** 명시 된 hello 싱크 hello 소스 tooany 중 어디에서 든 [여기](data-factory-data-movement-activities.md#supported-data-stores-and-formats) Azure Data Factory에서 복사 작업 hello를 사용 하 여 합니다.

## <a name="example-copy-data-from-azure-cosmos-db-tooazure-blob"></a>예: Azure Cosmos DB tooAzure Blob에서에서 데이터를 복사 합니다.
아래 hello 샘플을 보여 줍니다.

1. [DocumentDb](#linked-service-properties)형식의 연결된 서비스입니다.
2. [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)형식의 연결된 서비스
3. [DocumentDbCollection](#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)입니다.
4. [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)
5. [DocumentDbCollectionSource](#copy-activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)입니다.

hello 샘플 Azure Cosmos DB tooAzure Blob 데이터를 복사합니다. 이 예제에 사용 되는 hello JSON 속성 hello 샘플 다음 섹션에 설명 되어 있습니다.

**Azure Cosmos DB 연결된 서비스:**

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```
**Azure Blob 저장소 연결된 서비스:**

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
**Azure 문서 DB 입력 데이터 집합:**

라는 컬렉션 있다고 가정 하 고 hello 샘플 **사람** Azure Cosmos DB 데이터베이스에 있습니다.

설정 "외부": "true" 및 externalData 지정 hello Azure 데이터 팩터리 서비스는 hello 테이블 정책 정보는 외부 toohello 데이터 팩터리 및 hello data factory에는 활동에 의해 생성 되지 않습니다.

```JSON
{
  "name": "PersonCosmosDbTable",
  "properties": {
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
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

**Azure Blob 출력 데이터 집합:**

데이터는 새 blob 복사 tooa 시간 단위가 hello 특정 날짜/시간을 반영 하는 hello blob에 대 한 hello 경로로 1 시간입니다.

```JSON
{
  "name": "PersonBlobTableOut",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "docdb",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "nullValue": "NULL"
      }
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
Hello Cosmos DB 데이터베이스의 사용자 컬렉션에에서 대 한 샘플 JSON 문서:

```JSON
{
  "PersonId": 2,
  "Name": {
    "First": "Jane",
    "Middle": "",
    "Last": "Doe"
  }
}
```
Cosmos DB는 계층적 JSON 문서에 대한 구문과 같이 SQL을 사용하여 쿼리 문서를 지원합니다.

예제: 

```sql
SELECT Person.PersonId, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person
```

hello 다음 파이프라인 hello hello Azure Cosmos DB 데이터베이스 tooan Azure blob의에서 사용자 컬렉션에서에서 데이터를 복사 합니다. Hello 복사 활동 hello의 일환으로 입력 및 출력 데이터 집합 지정 되었습니다.  

```JSON
{
  "name": "DocDbToBlobPipeline",
  "properties": {
    "activities": [
      {
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
        "inputs": [
          {
            "name": "PersonCosmosDbTable"
          }
        ],
        "outputs": [
          {
            "name": "PersonBlobTableOut"
          }
        ],
        "policy": {
          "concurrency": 1
        },
        "name": "CopyFromDocDbToBlob"
      }
    ],
    "start": "2015-04-01T00:00:00Z",
    "end": "2015-04-02T00:00:00Z"
  }
}
```
## <a name="example-copy-data-from-azure-blob-tooazure-cosmos-db"></a>예: Azure Blob tooAzure Cosmos DB에서에서 데이터를 복사 합니다. 
아래 hello 샘플을 보여 줍니다.

1. [DocumentDb](#azure-documentdb-linked-service-properties)형식의 연결된 서비스입니다.
2. [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)형식의 연결된 서비스
3. [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)입니다.
4. [DocumentDbCollection](#azure-documentdb-dataset-type-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)입니다.
5. [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) 및 [DocumentDbCollectionSink](#azure-documentdb-copy-activity-type-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)입니다.

hello 예제는 Azure blob tooAzure Cosmos DB에서에서 데이터를 복사합니다. 이 예제에 사용 되는 hello JSON 속성 hello 샘플 다음 섹션에 설명 되어 있습니다.

**Azure Blob 저장소 연결된 서비스:**

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
**Azure Cosmos DB 연결된 서비스:**

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```
**Azure Blob 입력 데이터 집합:**

```JSON
{
  "name": "PersonBlobTableIn",
  "properties": {
    "structure": [
      {
        "name": "Id",
        "type": "Int"
      },
      {
        "name": "FirstName",
        "type": "String"
      },
      {
        "name": "MiddleName",
        "type": "String"
      },
      {
        "name": "LastName",
        "type": "String"
      }
    ],
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "fileName": "input.csv",
      "folderPath": "docdb",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "nullValue": "NULL"
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
**Azure Cosmos DB 출력 데이터 집합:**

hello 샘플 "Person" 이라는 데이터 tooa 컬렉션을 복사 합니다.

```JSON
{
  "name": "PersonCosmosDbTableOut",
  "properties": {
    "structure": [
      {
        "name": "Id",
        "type": "Int"
      },
      {
        "name": "Name.First",
        "type": "String"
      },
      {
        "name": "Name.Middle",
        "type": "String"
      },
      {
        "name": "Name.Last",
        "type": "String"
      }
    ],
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
hello 다음 Azure Blob toohello hello Cosmos DB에서에서 사용자 컬렉션의에서 데이터 복사 파이프라인입니다. Hello 복사 활동 hello의 일환으로 입력 및 출력 데이터 집합 지정 되었습니다.

```JSON
{
  "name": "BlobToDocDbPipeline",
  "properties": {
    "activities": [
      {
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
          }
          "translator": {
              "type": "TabularTranslator",
              "ColumnMappings": "FirstName: Name.First, MiddleName: Name.Middle, LastName: Name.Last, BusinessEntityID: BusinessEntityID, PersonType: PersonType, NameStyle: NameStyle, title: aaaTitle, Suffix: Suffix, EmailPromotion: EmailPromotion, rowguid: rowguid, ModifiedDate: ModifiedDate"
          }
        },
        "inputs": [
          {
            "name": "PersonBlobTableIn"
          }
        ],
        "outputs": [
          {
            "name": "PersonCosmosDbTableOut"
          }
        ],
        "policy": {
          "concurrency": 1
        },
        "name": "CopyFromBlobToDocDb"
      }
    ],
    "start": "2015-04-14T00:00:00Z",
    "end": "2015-04-15T00:00:00Z"
  }
}
```
Hello 샘플 blob 입력 하는 경우

```
1,John,,Doe
```
다음으로 hello Cosmos DB의 JSON 출력이 됩니다.

```JSON
{
  "Id": 1,
  "Name": {
    "First": "John",
    "Middle": null,
    "Last": "Doe"
  },
  "id": "a5e8595c-62ec-4554-a118-3940f4ff70b6"
}
```
Azure Cosmos DB는 중첩된 구조를 허용하는 JSON 문서용 NoSQL 저장소입니다. Azure 데이터 팩터리를 통해 사용자 toodenote 계층 구조를 사용 하면 **nestingSeparator**, 즉 "." 표시할 수 있습니다. Hello 구분 기호 hello 복사 작업에서는 생성 3 명의 자식 요소가 있는 hello "Name" 개체 첫 번째, 중간 및 마지막를 따라 too"Name.First", "Name.Middle" 및 "Name.Last" hello에 테이블 정의 합니다.

## <a name="appendix"></a>부록
1. **질문:** 기존 레코드의 복사 작업 지원 업데이트 hello가?

    **대답:** 아니요.
2. **질문:** 레코드 복사와 복사 tooAzure Cosmos DB 거래의 다시 시도 하면 이미 어떻습니까?

    **답변:** 레코드는 "ID" 필드를 포함 하 고 hello 복사 작업 tooinsert hello로 레코드 동일한 ID를 hello 복사 작업에서 오류가 발생 합니다.  
3. **질문:** Data Factory는 [범위 또는 해시 기반 데이터 분할](../documentdb/documentdb-partition-data.md)을 지원합니까?

    **대답:** 아니요.
4. **질문:** 하나의 테이블에 대해 하나 이상의 Azure Cosmos DB 컬렉션을 지정할 수 있습니까?

    **대답:** 아니요. 이 경우 하나의 컬렉션만 지정할 수 있습니다.

## <a name="performance-and-tuning"></a>성능 및 튜닝
참조 [복사 활동 성능 및 조정 가이드](data-factory-copy-activity-performance.md) toolearn 키에 대 한 Azure 데이터 팩터리 및 다양 한 방법으로 toooptimize에서 데이터 이동 (복사 작업)의 성능에 영향을 해당 놓은 것입니다.

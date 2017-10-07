---
title: "데이터 팩터리를 사용 하 여 aaaPush 데이터 tooSearch 인덱스 | Microsoft Docs"
description: "방법에 대 한 자세한 내용은 Azure 데이터 팩터리를 사용 하 여 toopush 데이터 tooAzure 검색 인덱스입니다."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: f8d46e1e-5c37-4408-80fb-c54be532a4ab
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: f2d973d0a2c24d6448e2d59e37e24503aa433018
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="push-data-tooan-azure-search-index-by-using-azure-data-factory"></a>Azure 데이터 팩터리를 사용 하 여 데이터 tooan Azure 검색 인덱스를 푸시
이 문서에서는 toouse hello 복사 작업 toopush 데이터를 지원 되는 원본 데이터에서에서 tooAzure 검색 인덱스를 저장 하는 방법을 설명 합니다. 지원 되는 원본 데이터 저장소의 hello hello 소스 열에 나열 됩니다 [원본 및 싱크를 지원](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 테이블입니다. Hello를 기반으로 한이 문서 [데이터 이동 작업](data-factory-data-movement-activities.md) 복사 작업 및 지원 되는 데이터 저장소 조합이 데이터 이동에 대 한 일반적인 개요를 제공 하는 문서입니다.

## <a name="enabling-connectivity"></a>연결 사용
데이터 팩터리 서비스 tooallow tooan 온-프레미스 데이터 저장소를 연결, 온-프레미스 환경에 데이터 관리 게이트웨이 설치 합니다. Hello 원본 데이터를 호스팅하는 동일한 컴퓨터에 저장 하거나 경쟁 hello 데이터를 사용 하 여 리소스에 대 한 별도 컴퓨터 tooavoid 저장소 hello에 게이트웨이 설치할 수 있습니다.

데이터 관리 게이트웨이 온-프레미스 데이터 원본 toocloud 서비스 안전 하 고 관리 되는 방식으로 연결합니다. 데이터 관리 게이트웨이에 대한 자세한 내용은 [온-프레미스 및 클라우드 간 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 을 참조하세요.

## <a name="getting-started"></a>시작
다른 도구/Api를 사용 하 여 원본 데이터 저장소 tooAzure 검색 인덱스에서 데이터를 밀어 넣는 복사 활동으로 파이프라인을 만들 수 있습니다.

hello 가장 쉬운 방법은 toocreate 파이프라인은 toouse hello **복사 마법사**합니다. 참조 [자습서: 복사 마법사를 사용 하 여 파이프라인을 만들고](data-factory-copy-data-wizard-tutorial.md) 간략 한 설명이 hello 복사 데이터 마법사를 사용 하 여 파이프라인을 만드는 방법에 대 한 합니다.

다음 도구 toocreate 파이프라인 hello을 사용할 수 있습니다: **Azure 포털**, **Visual Studio**, **Azure PowerShell**, **Azure 리소스 관리자 템플릿** , **.NET API**, 및 **REST API**합니다. 참조 [복사 활동 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 단계별 지침 toocreate 복사 작업으로 파이프라인에 대 한 합니다. 

Hello 도구 또는 Api를 사용 하는지 여부를 hello tooa 싱크 데이터 저장소를 저장 하는 원본 데이터에서 데이터를 이동 하는 파이프라인 단계 toocreate 다음을 수행 합니다. 

1. 만들 **연결 된 서비스** toolink 입력 및 출력 데이터 저장소 tooyour 데이터 팩터리입니다.
2. 만들 **데이터 집합** 입력 및 출력 toorepresent hello에 대 한 데이터 복사 작업을 합니다. 
3. 입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다. 

Hello 마법사를 사용 하 여 이러한 데이터 팩터리 엔터티 (연결 된 서비스, 데이터 집합 및 hello 파이프라인)에 대 한 JSON 정의를 자동으로 만들어집니다. 도구/Api (제외.NET API)를 사용 하면 hello JSON 형식을 사용 하 여이 Data Factory 엔터티를 정의 합니다.  Data Factory 된 엔터티를 사용 하는 toocopy 데이터 tooAzure 검색 인덱스에 대 한 JSON 정의 된 샘플을 보려면 [JSON의 예: 온-프레미스 SQL Server tooAzure 검색 인덱스에서 데이터를 복사](#json-example-copy-data-from-on-premises-sql-server-to-azure-search-index) 이 문서의 섹션. 

다음 섹션 hello JSON 속성을 사용 하는 toodefine Data Factory 엔터티에 특정 tooAzure 검색 인덱스에 대 한 세부 정보를 제공 합니다.

## <a name="linked-service-properties"></a>연결된 서비스 속성

다음 표에서 hello JSON 요소를 특정 toohello 연결 된 Azure 검색 서비스에 대 한 설명을 제공 합니다.

| 속성 | 설명 | 필수 |
| -------- | ----------- | -------- |
| type | hello type 속성 설정 해야 합니다: **AzureSearch**합니다. | 예 |
| url | Hello Azure 검색 서비스에 대 한 URL입니다. | 예 |
| key | Hello Azure 검색 서비스에 대 한 관리자 키입니다. | 예 |

## <a name="dataset-properties"></a>데이터 집합 속성

섹션 및 데이터 집합 정의에 사용할 수 있는 속성의 전체 목록을 참조 hello [데이터 집합을 만드는](data-factory-create-datasets.md) 문서. 구조, 가용성 및 JSON 데이터 집합의 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다. hello **typeProperties** 섹션은 데이터 집합의 각 형식 마다 다릅니다. hello typeProperties hello 형식의 데이터 집합에 대 한 섹션 **AzureSearchIndex** hello 다음과 같은 속성에:

| 속성 | 설명 | 필수 |
| -------- | ----------- | -------- |
| type | 너무 hello 유형 속성을 설정 해야**AzureSearchIndex**합니다.| 예 |
| indexName | Hello Azure 검색 인덱스의 이름입니다. 데이터 팩터리 hello 인덱스가 생성 되지 않습니다. hello 인덱스 Azure 검색에 있어야 합니다. | 예 |


## <a name="copy-activity-properties"></a>복사 작업 속성
섹션 및 활동 정의에 사용할 수 있는 속성의 전체 목록을 참조 hello [파이프라인 만들기](data-factory-create-pipelines.md) 문서. 이름, 설명, 입력/출력 테이블, 다양한 정책 등의 속성은 모든 형식의 활동에 사용할 수 있습니다. 반면 hello typeProperties 섹션에서 사용할 수 있는 속성에 각 활동 유형에 따라 다릅니다. 복사 작업은 원본 및 싱크의 hello 형식에 따라 변경합니다.

Hello 싱크 hello 유형인 경우 복사 작업에 대 한 **AzureSearchIndexSink**, 다음과 같은 속성 hello는 typeProperties 섹션에 있습니다.

| 속성 | 설명 | 허용되는 값 | 필수 |
| -------- | ----------- | -------------- | -------- |
| WriteBehavior | Toomerge 또는 교체 때 문서에에서 이미 있는지 hello 인덱스를 지정 합니다. Hello 참조 [WriteBehavior 속성](#writebehavior-property)합니다.| 병합(기본값)<br/>업로드| 아니요 |
| writeBatchSize | WriteBatchSize hello 버퍼 크기에 이르면 hello Azure 검색 인덱스에 데이터를 업로드 합니다. Hello 참조 [WriteBatchSize 속성](#writebatchsize-property) 대 한 자세한 내용은 합니다. | too1이 1, 000입니다. 기본값은 1,000입니다. | 아니요 |

### <a name="writebehavior-property"></a>WriteBehavior 속성
데이터를 쓸 때 AzureSearchSink가 삽입됩니다. 즉, 문서 키 hello hello Azure 검색 인덱스에 이미 있는 경우 문서를 작성, Azure 검색 충돌 예외를 throw 하지 않고 hello 기존 문서를 업데이트 합니다.

hello를 AzureSearchSink hello를 두 가지 upsert 동작 (AzureSearch SDK 사용)에서 다음을 제공 합니다.

- **병합**: hello 새 문서에서 모든 hello 열 하나 기존 hello로 결합 합니다. Hello 새 문서에 null 값을 가진 열에 대 한 기존 자동 압축 hello hello 값 보존 됩니다.
- **업로드**: hello 새 문서 대체 hello 기존 합니다. 열의 hello 새 문서에 지정 되지 않은 경우 null이 아닌 값에에서 여부 hello 기존 문서 또는 not hello 값 toonull에 설정 됩니다.

hello 기본 동작은 **병합**합니다.

### <a name="writebatchsize-property"></a>writeBatchSize 속성
Azure Search 서비스는 일괄 처리로 문서 작성을 지원합니다. 일괄 처리 too1 1, 000 동작을 포함할 수 있습니다. 작업 한 문서 tooperform hello 업로드/병합 작업을 처리 합니다.

### <a name="data-type-support"></a>데이터 형식 지원
hello 다음 표에서 Azure 검색 데이터 형식을 지원 되는지 여부.

| Azure Search 데이터 형식 | Azure Search 싱크에서 지원됨 |
| ---------------------- | ------------------------------ |
| String | Y |
| Int32 | Y |
| Int64 | Y |
| Double | Y |
| Boolean | Y |
| DataTimeOffset | Y |
| 문자열 배열 | N |
| GeographyPoint | N |

## <a name="json-example-copy-data-from-on-premises-sql-server-tooazure-search-index"></a>JSON의 예: 온-프레미스 SQL Server tooAzure 검색 인덱스에서 데이터 복사

다음 샘플에서는 hello:

1.  [AzureSearch](#linked-service-properties) 형식의 연결된 서비스
2.  [OnPremisesSqlServer](data-factory-sqlserver-connector.md#linked-service-properties)형식의 연결된 서비스
3.  [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)
4.  [AzureSearchIndex](#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)
4.  [SqlSource](data-factory-sqlserver-connector.md#copy-activity-properties) 및 [AzureSearchIndexSink](#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)

hello 샘플 시계열 데이터에서에서 복사 온-프레미스 SQL Server 데이터베이스 tooan Azure 검색 인덱스 매시간 합니다. 이 샘플에 사용 되는 hello JSON 속성 hello 샘플 다음 섹션에 설명 되어 있습니다.

첫 번째 단계로, 온-프레미스 컴퓨터에 hello 데이터 관리 게이트웨이 설치 합니다. hello 지침은 hello [온-프레미스 위치와 클라우드 간의 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서.

**Azure Search 연결된 서비스:**

```JSON
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

**SQL Server 연결된 서비스**

```JSON
{
  "Name": "SqlServerLinkedService",
  "properties": {
    "type": "OnPremisesSqlServer",
    "typeProperties": {
      "connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=False;User ID=<username>;Password=<password>;",
      "gatewayName": "<gatewayname>"
    }
  }
}
```

**SQL Server 입력 데이터 집합**

hello 샘플 테이블 "MyTable" SQL Server에서 만들고 시계열 데이터에 대 한 "timestampcolumn" 라는 열이 포함 된 가정 합니다. TableName typeProperty hello 데이터 집합의 단일 데이터 집합 이지만 단일 테이블을 사용 하 여 동일한 데이터베이스를 사용 해야 하는 hello 내에서 여러 테이블에 대해 쿼리할 수 있습니다.

설정 "외부": "true" 알리고 데이터 팩터리 서비스 hello 데이터 집합의 데이터 팩터리 외부 toohello hello data factory에는 활동에 의해 생성 되지 않습니다.

```JSON
{
  "name": "SqlServerDataset",
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

**Azure Search 출력 데이터 집합:**

명명 된 hello 샘플 복사본 데이터 tooan Azure 검색 인덱스 **제품**합니다. 데이터 팩터리 hello 인덱스가 생성 되지 않습니다. tootest hello 샘플,이 이름을 가진 인덱스를 작성 합니다. Hello로 hello Azure 검색 인덱스를 만들 hello 입력된 데이터 집합에서와 같이 열 수가 같아야 합니다. 새 항목을 1 시간 마다 toohello Azure 검색 인덱스를 추가 됩니다.

```JSON
{
    "name": "AzureSearchIndexDataset",
    "properties": {
        "type": "AzureSearchIndex",
        "linkedServiceName": "AzureSearchLinkedService",
        "typeProperties" : {
            "indexName": "products",
        },
        "availability": {
            "frequency": "Minute",
            "interval": 15
        }
   }
}
```

**SQL 원본 및 Azure Search 인덱스 싱크를 사용하는 파이프라인의 복사 작업:**

hello 파이프라인에 포함 된 구성된 toouse 않은 복사 작업 입력 및 출력 데이터 집합을 hello 및 예약 된 toorun 1 시간입니다. Hello 파이프라인 JSON 정의에서 hello **소스** 형식이 너무 설정**SqlSource** 및 **싱크** 형식이 너무 설정**AzureSearchIndexSink**합니다. hello에 대 한 지정 된 hello SQL 쿼리 **SqlReaderQuery** 속성 시간 toocopy 지난 hello에 hello 데이터를 선택 합니다.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "SqlServertoAzureSearchIndex",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": " SqlServerInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSearchIndexDataset"
          }
        ],
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
      }
     ]
   }
}
```

클라우드 데이터 저장소에서 Azure Search로 데이터를 복사하는 경우 `executionLocation` 속성이 필수입니다. hello 다음 JSON 코드 조각은 hello 변경 사항이 표시 복사 작업에서 필요한 `typeProperties` 예를 들어 있습니다. 지원되는 값과 자세한 정보는[클라우드 데이터 저장소 간의 데이터 복사](data-factory-data-movement-activities.md#global)섹션을 확인합니다.

```JSON
"typeProperties": {
  "source": {
    "type": "BlobSource"
  },
  "sink": {
    "type": "AzureSearchIndexSink"
  },
  "executionLocation": "West US"
}
```


## <a name="copy-from-a-cloud-source"></a>클라우드 원본에서 복사
클라우드 데이터 저장소에서 Azure Search로 데이터를 복사하는 경우 `executionLocation` 속성이 필수입니다. hello 다음 JSON 코드 조각은 hello 변경 사항이 표시 복사 작업에서 필요한 `typeProperties` 예를 들어 있습니다. 지원되는 값과 자세한 정보는[클라우드 데이터 저장소 간의 데이터 복사](data-factory-data-movement-activities.md#global)섹션을 확인합니다.

```JSON
"typeProperties": {
  "source": {
    "type": "BlobSource"
  },
  "sink": {
    "type": "AzureSearchIndexSink"
  },
  "executionLocation": "West US"
}
```

원본 데이터 집합 toocolumns hello 복사 활동 정의에서 싱크 데이터 집합에서의 열을 매핑할 수도 있습니다. 자세한 내용은 [Azure Data Factory에서 데이터 집합 열 매핑](data-factory-map-columns.md)을 참조하세요.

## <a name="performance-and-tuning"></a>성능 및 튜닝  
Hello 참조 [복사 활동 성능 및 조정 가이드](data-factory-copy-activity-performance.md) toolearn 키에 대 한 데이터 이동 (복사 작업)의 성능에는 영향 및 다양 한 방법으로 toooptimize 놓은 것입니다.

## <a name="next-steps"></a>다음 단계
Hello 다음 문서를 참조 하십시오.

* [복사 작업 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) .

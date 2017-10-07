---
title: "데이터 팩터리를 사용 하 여 Amazon Redshift aaaMove 데이터로 | Microsoft Docs"
description: "방법에 대 한 자세한 내용은 Azure 데이터 팩터리를 사용 하 여 Amazon Redshift에서 toomove 데이터입니다."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 01d15078-58dc-455c-9d9d-98fbdf4ea51e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jingwang
ms.openlocfilehash: 2a097320734ebdd57282d250f7fdba35741777f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-amazon-redshift-using-azure-data-factory"></a>Azure 데이터 팩터리를 사용하여 Amazon Redshift에서 데이터 이동
이 문서에서는 toouse Amazon Redshift에서 Azure Data Factory toomove 데이터에서 복사 작업을 hello 하는 방법을 설명 합니다. hello을 기반으로 하는 hello 문서 [데이터 이동 작업](data-factory-data-movement-activities.md) hello 복사 작업으로 데이터 이동에 대 한 일반적인 개요를 제공 하는 문서입니다. 

Amazon Redshift 지원 tooany 싱크 데이터 저장소에서 데이터를 복사할 수 있습니다. 목록이 hello 복사 작업에서 싱크를 지 원하는 데이터 저장소에 대 한 참조 [데이터 저장소를 지원](data-factory-data-movement-activities.md#supported-data-stores-and-formats)합니다. 데이터 팩터리의 현재 이동 데이터를 다른 데이터 저장소 tooAmazon Redshift에서에서 데이터를 이동 하지 않습니다에서 Amazon Redshift tooother 데이터 저장소를 지원 합니다.

## <a name="prerequisites"></a>필수 조건
* 데이터 tooan 온-프레미스 데이터 저장소를 이동 하는 경우 설치 [데이터 관리 게이트웨이](data-factory-data-management-gateway.md) 온-프레미스 컴퓨터에 있습니다. 그런 다음 Grant 데이터 관리 게이트웨이 (hello 컴퓨터의 사용 하 여 IP 주소) hello 액세스 tooAmazon Redshift 클러스터입니다. 참조 [Authorize 액세스 toohello 클러스터](http://docs.aws.amazon.com/redshift/latest/gsg/rs-gsg-authorize-cluster-access.html) 지침에 대 한 합니다.
* 참조 데이터 tooan Azure 데이터 저장소를 이동 하는 경우 [Azure 데이터 센터 IP 범위](https://www.microsoft.com/download/details.aspx?id=41653) hello 계산 IP 주소와 hello Azure 데이터 센터에서 사용 하는 SQL 범위에 대 한 합니다.

## <a name="getting-started"></a>시작
다른 도구/API를 사용하여 Amazon Redshift 원본의 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다.

hello 가장 쉬운 방법은 toocreate 파이프라인은 toouse hello **복사 마법사**합니다. 참조 [자습서: 복사 마법사를 사용 하 여 파이프라인을 만들고](data-factory-copy-data-wizard-tutorial.md) 간략 한 설명이 hello 복사 데이터 마법사를 사용 하 여 파이프라인을 만드는 방법에 대 한 합니다.

다음 도구 toocreate 파이프라인 hello을 사용할 수 있습니다: **Azure 포털**, **Visual Studio**, **Azure PowerShell**, **Azure 리소스 관리자 템플릿** , **.NET API**, 및 **REST API**합니다. 참조 [복사 활동 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 단계별 지침 toocreate 복사 작업으로 파이프라인에 대 한 합니다. 

Hello 도구 또는 Api를 사용 하는지 여부를 hello tooa 싱크 데이터 저장소를 저장 하는 원본 데이터에서 데이터를 이동 하는 파이프라인 단계 toocreate 다음을 수행 합니다. 

1. 만들 **연결 된 서비스** toolink 입력 및 출력 데이터 저장소 tooyour 데이터 팩터리입니다.
2. 만들 **데이터 집합** 입력 및 출력 toorepresent hello에 대 한 데이터 복사 작업을 합니다. 
3. 입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다. 

Hello 마법사를 사용 하 여 이러한 데이터 팩터리 엔터티 (연결 된 서비스, 데이터 집합 및 hello 파이프라인)에 대 한 JSON 정의를 자동으로 만들어집니다. 도구/Api (제외.NET API)를 사용 하면 hello JSON 형식을 사용 하 여이 Data Factory 엔터티를 정의 합니다.  Data Factory 된 엔터티를 Amazon Redshift 데이터 저장소에서 사용 되는 toocopy 데이터에 대 한 JSON 정의 된 샘플을 보려면 [JSON의 예: Amazon Redshift tooAzure Blob에서에서 데이터를 복사](#json-example-copy-data-from-amazon-redshift-to-azure-blob) 이 문서의 섹션. 

사용 되는 toodefine Data Factory 엔터티에 특정 tooAmazon Redshift는 JSON 속성에 대 한 세부 정보를 제공 하는 다음 섹션 hello: 

## <a name="linked-service-properties"></a>연결된 서비스 속성
다음 표에서 hello JSON 요소 특정 tooAmazon Redshift 연결 된 서비스에 대 한 설명을 제공 합니다.

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| type |hello type 속성 설정 해야 합니다: **AmazonRedshift**합니다. |예 |
| server |Hello Amazon Redshift 서버의 IP 주소 또는 호스트 이름입니다. |예 |
| 포트 |Amazon Redshift 서버 hello hello TCP 포트 수가 hello toolisten를 사용 하 여 클라이언트 연결에 대 한 합니다. |기본값이 없음: 5439 |
| database |Hello Amazon Redshift 데이터베이스의 이름입니다. |예 |
| username |Access toohello 데이터베이스를 갖고 있는 사용자의 이름입니다. |예 |
| 암호 |Hello 사용자 계정의 암호입니다. |예 |

## <a name="dataset-properties"></a>데이터 집합 속성
섹션 및 데이터 집합 정의에 사용 가능한 속성의 전체 목록을 보려면 hello [데이터 집합을 만드는](data-factory-create-datasets.md) 문서. 구조, 가용성 및 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다(Azure SQL, Azure blob, Azure 테이블 등).

hello **typeProperties** 섹션은 데이터 집합의 각 형식 마다 다릅니다. Hello 데이터 저장소에 hello 데이터의 hello 위치에 대 한 정보를 제공합니다. 형식의 데이터 집합에 대 한 hello typeProperties 섹션 **RelationalTable** hello 다음과 같은 속성에 (Amazon Redshift 데이터 집합 포함)

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| tableName |연결 된 서비스는 hello Amazon Redshift 데이터베이스에 대 한 hello 테이블의 이름은 참조 합니다. |아니요(**RelationalSource**의 **쿼리**가 지정된 경우) |

## <a name="copy-activity-properties"></a>복사 작업 속성
섹션 및 활동 정의에 사용 가능한 속성의 전체 목록을 참조 hello [파이프라인 만들기](data-factory-create-pipelines.md) 문서. 이름, 설명, 입력/출력 테이블, 정책 등의 속성은 모든 형식의 활동에 사용할 수 있습니다.

반면 hello에 사용할 수 있는 속성 **typeProperties** hello 활동의 섹션에 각 활동 유형에 따라 다릅니다. 복사 작업은 원본 및 싱크의 hello 형식에 따라 변경합니다.

복사 작업의 원본 유형의 경우 **RelationalSource** (Amazon Redshift 포함), 다음과 같은 속성 hello typeProperties 섹션에서 사용할 수 있는:

| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| 쿼리 |사용자 지정 쿼리 tooread 데이터 hello를 사용 합니다. |SQL 쿼리 문자열. 예: select * from MyTable. |아니요(**데이터 집합**의 **tableName**이 지정된 경우) |

## <a name="json-example-copy-data-from-amazon-redshift-tooazure-blob"></a>JSON의 예: Amazon Redshift tooAzure Blob에서에서 데이터 복사
이 샘플에서는 toocopy 데이터로 Amazon Redshift 데이터베이스 tooan Azure Blob 저장소를 보여 줍니다. 그러나 데이터를 복사할 수 있습니다 **직접** 명시 된 hello 싱크 tooany [여기](data-factory-data-movement-activities.md#supported-data-stores-and-formats) Azure Data Factory에서 복사 작업 hello를 사용 하 여 합니다.  

hello 샘플 hello 데이터 팩터리 엔터티 뒤에 있습니다.

* [AmazonRedshift](#linked-service-properties)형식의 연결된 서비스입니다.
* [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)형식의 연결된 서비스
* [RelationalTable](#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)
* [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)
* [RelationalSource](#copy-activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md##copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)

hello 샘플 데이터 복사 Amazon Redshift tooa blob에 쿼리 결과에서 1 시간 마다 합니다. 이 예제에 사용 되는 hello JSON 속성 hello 샘플 다음 섹션에 설명 되어 있습니다.

**Amazon Redshift 연결된 서비스:**

```json
{
    "name": "AmazonRedshiftLinkedService",
    "properties":
    {
        "type": "AmazonRedshift",
        "typeProperties":
        {
            "server": "< hello IP address or host name of hello Amazon Redshift server >",
            "port": <hello number of hello TCP port that hello Amazon Redshift server uses toolisten for client connections.>,
            "database": "<hello database name of hello Amazon Redshift database>",
            "username": "<username>",
            "password": "<password>"
        }
    }
}
```

**Azure 저장소 연결된 서비스:**

```json
{
  "name": "AzureStorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
**Amazon Redshift 입력 데이터 집합:**

설정 `"external": true` 알리고 hello 데이터 팩터리 서비스 hello 데이터 집합의 데이터 팩터리 외부 toohello hello data factory에는 활동에 의해 생성 되지 않습니다. 이 속성 tootrue 하지 hello 파이프라인의 활동에 의해 생성 되는 입력된 데이터 집합에 설정 합니다.

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

**Azure Blob 출력 데이터 집합:**

데이터가 새 blob tooa 1 시간 마다 기록 됩니다 (빈도: 시, 간격: 1). hello blob에 대 한 hello 폴더 경로 처리 중인 hello 조각의 hello 시작 시간에 따라 동적으로 평가 됩니다. hello 폴더 경로 hello 시작 시간의 연도, 월, 일 및 시간 부분을 사용 합니다.

```json
{
    "name": "AzureBlobOutputDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/fromamazonredshift/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            },
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
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

**Azure Redshift 원본(RelationalSource) 및 Blob 싱크를 사용하는 파이프라인의 복사 작업:**

hello 파이프라인에 포함 된 구성된 toouse 않은 복사 작업 입력 및 출력 데이터 집합을 hello 및 예약 된 toorun 1 시간입니다. Hello 파이프라인 JSON 정의에서 hello **소스** 형식이 너무 설정**RelationalSource** 및 **싱크** 형식이 너무 설정**BlobSink**합니다. hello에 대 한 지정 된 hello SQL 쿼리 **쿼리** 속성 시간 toocopy 지난 hello에 hello 데이터를 선택 합니다.

```json
{
    "name": "CopyAmazonRedshiftToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
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
                "inputs": [
                    {
                        "name": "AmazonRedshiftInputDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutputDataSet"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "AmazonRedshiftToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```
### <a name="type-mapping-for-amazon-redshift"></a>Amazon Redshift에 대한 형식 매핑
Hello에 설명 된 대로 [데이터 이동 작업](data-factory-data-movement-activities.md) 문서, 복사 작업 소스 형식 toosink 형식에서 자동 형식 변환 2 단계 방식을 따릅니다 hello로 수행:

1. 네이티브 소스 형식 too.NET 형식에서 변환
2. .NET 형식 toonative 싱크 형식에서 변환

데이터 tooAmazon Redshift를 이동할 때 다음 매핑을 hello Amazon Redshift 형식 too.NET 형식에서 사용 됩니다.

| Amazon Redshift 형식 | .NET 기반 형식 |
| --- | --- |
| SmallInt |Int16 |
| INTEGER |Int32 |
| BIGINT |Int64 |
| DECIMAL |DECIMAL |
| Real |단일 |
| double precision |Double |
| BOOLEAN |문자열 |
| CHAR |문자열 |
| VARCHAR |문자열 |
| DATE |DateTime |
| TIMESTAMP |DateTime |
| TEXT |문자열 |

## <a name="map-source-toosink-columns"></a>원본 toosink 열 매핑
원본 데이터 집합 toocolumns 싱크 데이터 집합에서의 열을 매핑하는 방법에 대 한 toolearn 참조 [Azure Data Factory에서 데이터 집합 열에 매핑](data-factory-map-columns.md)합니다.

## <a name="repeatable-read-from-relational-sources"></a>관계형 원본에서 반복 가능한 읽기
관계형 데이터 저장소에서 데이터를 복사할 때 유의 tooavoid에서 반복성을 유지 의도 하지 않은 결과입니다. Azure Data Factory에서는 조각을 수동으로 다시 실행할 수 있습니다. 또한 오류가 발생하면 조각을 다시 실행하도록 데이터 집합에 대한 재시도 정책을 구성할 수 있습니다. Toomake 동일한 데이터를 hello 있는지 어떻게에 관계 없이 읽기 필요한 어느 쪽에 분할 영역을 다시 실행 하는 경우 조각에 여러 번 실행 됩니다. [관계형 원본에서 반복 가능한 읽기](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)를 참조하세요.

## <a name="performance-and-tuning"></a>성능 및 튜닝
참조 [복사 활동 성능 및 조정 가이드](data-factory-copy-activity-performance.md) toolearn 키에 대 한 Azure 데이터 팩터리 및 다양 한 방법으로 toooptimize에서 데이터 이동 (복사 작업)의 성능에 영향을 해당 놓은 것입니다.

## <a name="next-steps"></a>다음 단계
Hello 다음 문서를 참조 하십시오.

* [복사 작업 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) .

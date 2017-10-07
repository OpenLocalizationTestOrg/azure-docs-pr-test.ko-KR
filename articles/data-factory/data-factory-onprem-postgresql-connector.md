---
title: "aaaMove 데이터에서 PostgreSQL Azure 데이터 팩터리를 사용 하 여 | Microsoft Docs"
description: "방법에 대 한 자세한 내용은 Azure 데이터 팩터리를 사용 하 여 PostgreSQL 데이터베이스에서 toomove 데이터입니다."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 888d9ebc-2500-4071-b6d1-0f6bd1b5997c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: ea384f4e06f7d7bedae2949e4ea727c8f8806614
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-postgresql-using-azure-data-factory"></a>Azure 데이터 팩터리를 사용하여 PostgreSQL에서 데이터 이동
이 문서에서는 toouse 온-프레미스 PostgreSQL 데이터베이스에서 Azure Data Factory toomove 데이터에서 복사 작업을 hello 하는 방법을 설명 합니다. Hello에 기반 [데이터 이동 작업](data-factory-data-movement-activities.md) hello 복사 작업으로 데이터 이동에 대 한 일반적인 개요를 제공 하는 문서입니다.

온-프레미스 PostgreSQL 데이터 저장소 지원 tooany 싱크 데이터 저장소에서 데이터를 복사할 수 있습니다. 목록이 hello 복사 작업에서 싱크를 지 원하는 데이터 저장소에 대 한 참조 [데이터 저장소를 지원](data-factory-data-movement-activities.md#supported-data-stores-and-formats)합니다. 데이터 팩터리의 현재 tooother 데이터 저장소에서 데이터베이스를 한 PostgreSQL에서 데이터를 이동 하는 원하는 하지만 하지 tooan PostgreSQL 데이터베이스 저장 다른 데이터에서 데이터를 이동 합니다. 

## <a name="prerequisites"></a>필수 조건

데이터 팩터리 서비스는 hello 데이터 관리 게이트웨이 사용 하 여 연결 tooon 온-프레미스 PostgreSQL 원본을 지원 합니다. 참조 [온-프레미스 위치와 클라우드 간의 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 데이터 관리 게이트웨이 및 hello 게이트웨이 설정에 대 한 단계별 지침에 대 한 문서 toolearn 합니다.

게이트웨이 hello PostgreSQL 데이터베이스 Azure IaaS VM에서 호스팅되는 경우에 필요 합니다. Hello IaaS VM hello 데이터로 저장 같거나 hello 게이트웨이 다른 VM toohello 데이터베이스 연결 될 수 있습니다에 게이트웨이 설치할 수 있습니다.

> [!NOTE]
> 연결/게이트웨이 관련 문제 해결에 대한 팁은 [게이트웨이 문제 해결](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) 을 참조하세요.

## <a name="supported-versions-and-installation"></a>지원되는 버전 및 설치
데이터 관리 게이트웨이 tooconnect toohello PostgreSQL 데이터베이스를 설치 hello [PostgreSQL Ngpsql 데이터 공급자](http://go.microsoft.com/fwlink/?linkid=282716) 2.0.12 위에 hello 동일 또는 데이터 관리 게이트웨이 hello 시스템입니다. PostgreSQL 버전 7.4 이상이 지원됩니다.

## <a name="getting-started"></a>시작
여러 도구/API를 사용하여 온-프레미스 PostgreSQL 데이터 저장소의 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다. 

- hello 가장 쉬운 방법은 toocreate 파이프라인은 toouse hello **복사 마법사**합니다. 참조 [자습서: 복사 마법사를 사용 하 여 파이프라인을 만들고](data-factory-copy-data-wizard-tutorial.md) 간략 한 설명이 hello 복사 데이터 마법사를 사용 하 여 파이프라인을 만드는 방법에 대 한 합니다. 
- 다음 도구 toocreate 파이프라인 hello를 사용할 수 있습니다. 
    - Azure portal
    - Visual Studio
    - Azure PowerShell
    - Azure Resource Manager 템플릿
    - .NET API
    - REST API

     참조 [복사 활동 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 단계별 지침 toocreate 복사 작업으로 파이프라인에 대 한 합니다. 

Hello 도구 또는 Api를 사용 하는지 여부를 hello tooa 싱크 데이터 저장소를 저장 하는 원본 데이터에서 데이터를 이동 하는 파이프라인 단계 toocreate 다음을 수행 합니다.

1. 만들 **연결 된 서비스** toolink 입력 및 출력 데이터 저장소 tooyour 데이터 팩터리입니다.
2. 만들 **데이터 집합** 입력 및 출력 toorepresent hello에 대 한 데이터 복사 작업을 합니다. 
3. 입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다. 

Hello 마법사를 사용 하 여 이러한 데이터 팩터리 엔터티 (연결 된 서비스, 데이터 집합 및 hello 파이프라인)에 대 한 JSON 정의를 자동으로 만들어집니다. 도구/Api (제외.NET API)를 사용 하면 hello JSON 형식을 사용 하 여이 Data Factory 엔터티를 정의 합니다.  Data Factory 된 엔터티를 온-프레미스 PostgreSQL 데이터 저장소에서 사용 되는 toocopy 데이터에 대 한 JSON 정의 된 샘플을 보려면 [JSON의 예: PostgreSQL tooAzure Blob에서에서 데이터를 복사](#json-example-copy-data-from-postgresql-to-azure-blob) 이 문서의 섹션. 

다음 섹션 hello JSON 속성을 사용 하는 toodefine Data Factory 엔터티에 특정 tooa PostgreSQL 데이터 저장소에 대 한 세부 정보를 제공 합니다.

## <a name="linked-service-properties"></a>연결된 서비스 속성
다음 표에서 hello JSON 요소 특정 tooPostgreSQL 연결 된 서비스에 대 한 설명을 제공 합니다.

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| type |hello type 속성 설정 해야 합니다: **OnPremisesPostgreSql** |예 |
| server |Hello PostgreSQL 서버의 이름입니다. |예 |
| database |Hello PostgreSQL 데이터베이스의 이름입니다. |예 |
| schema |Hello hello 데이터베이스 스키마의 이름입니다. hello 스키마 이름이 대/소문자 구분 합니다. |아니요 |
| authenticationType |Tooconnect toohello PostgreSQL 데이터베이스를 사용 하는 인증 유형입니다. 가능한 값은 익명, 기본 및 Windows입니다. |예 |
| username |기본 또는 Windows 인증을 사용하는 경우 사용자 이름을 지정합니다. |아니요 |
| 암호 |Hello 사용자 이름에 대해 지정한 사용자 계정에 hello에 대 한 암호를 지정 합니다. |아니요 |
| gatewayName |데이터 팩터리 서비스 hello hello 게이트웨이의 이름 tooconnect toohello 온-프레미스 PostgreSQL 데이터베이스를 사용 해야 합니다. |예 |

## <a name="dataset-properties"></a>데이터 집합 속성
섹션 및 데이터 집합 정의에 사용 가능한 속성의 전체 목록을 보려면 hello [데이터 집합을 만드는](data-factory-create-datasets.md) 문서. 구조, 가용성 및 JSON 데이터 집합의 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다.

hello typeProperties 섹션 hello 데이터 저장소에 hello 데이터의 hello 위치에 대 한 정보를 제공 및 데이터 집합의 각 유형에 대해과 다릅니다. 형식의 데이터 집합에 대 한 hello typeProperties 섹션 **RelationalTable** hello 다음과 같은 속성에 (PostgreSQL 데이터 집합 포함):

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| tableName |PostgreSQL 데이터베이스 인스턴스에 연결 된 서비스를 가리키는 hello에 hello 테이블의 이름입니다. hello tableName은 대/소문자 구분 합니다. |아니요(**RelationalSource**의 **쿼리**가 지정된 경우) |

## <a name="copy-activity-properties"></a>복사 작업 속성
섹션 및 활동 정의에 사용 가능한 속성의 전체 목록을 참조 hello [파이프라인 만들기](data-factory-create-pipelines.md) 문서. 이름, 설명, 입력/출력 테이블, 정책 등의 속성은 모든 형식의 활동에 사용할 수 있습니다.

반면 hello 활동의 hello typeProperties 섹션에서 사용할 수 있는 속성에 각 활동 유형에 따라 다릅니다. 복사 작업은 원본 및 싱크의 hello 형식에 따라 변경합니다.

원본 유형의 경우 **RelationalSource** (PostgreSQL 포함), 다음과 같은 속성 hello는 typeProperties 섹션에 있습니다.

| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| 쿼리 |사용자 지정 쿼리 tooread 데이터 hello를 사용 합니다. |SQL 쿼리 문자열. 예: "query": "select * from \"MySchema\".\"MyTable\"". |아니요(**데이터 집합**의 **tableName**이 지정된 경우) |

> [!NOTE]
> 스키마 및 테이블 이름은 대/소문자를 구분합니다. 로 둘러쌀 `""` (큰따옴표) hello 쿼리에서 합니다.  

**예제:**

 `"query": "select * from \"MySchema\".\"MyTable\""`

## <a name="json-example-copy-data-from-postgresql-tooazure-blob"></a>JSON의 예: PostgreSQL tooAzure Blob에서에서 데이터 복사
이 예제에서는 샘플 JSON 정의 제공 합니다. 사용 하 여 toocreate 파이프라인을 사용할 수 있는 [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md) 또는 [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 또는 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)합니다. Toocopy 데이터로 PostgreSQL 데이터베이스 tooAzure Blob 저장소를 보여 줍니다. 그러나 데이터는 복사 tooany 명시 된 hello 싱크 가능 [여기](data-factory-data-movement-activities.md#supported-data-stores-and-formats) Azure Data Factory에서 복사 작업 hello를 사용 하 여 합니다.   

> [!IMPORTANT]
> 이 샘플은 JSON 코드 조각을 제공합니다. Hello 데이터 팩터리를 만들기 위한 단계별 지침을 다루지 않습니다. 단계별 지침은 [온-프레미스 위치와 클라우드 간에 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서를 참조하세요.

hello 샘플 hello 데이터 팩터리 엔터티 뒤에 있습니다.

1. [OnPremisesPostgreSql](data-factory-onprem-postgresql-connector.md#linked-service-properties)형식의 연결된 서비스
2. [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)형식의 연결된 서비스
3. [RelationalTable](data-factory-onprem-postgresql-connector.md#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)
4. [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)
5. hello [파이프라인](data-factory-create-pipelines.md) 사용 하 여 복사 작업으로 [RelationalSource](data-factory-onprem-postgresql-connector.md#copy-activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)합니다.

hello 샘플 데이터 복사 PostgreSQL 데이터베이스 tooa blob에 쿼리 결과에서 1 시간 마다 합니다. 이 예제에 사용 되는 hello JSON 속성 hello 샘플 다음 섹션에 설명 되어 있습니다.

첫 번째 단계로, hello 데이터 관리 게이트웨이 설치 합니다. hello 지침은 hello [온-프레미스 위치와 클라우드 간의 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서.

**PostgreSQL 연결된 서비스:**

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
**Azure Blob 저장소 연결된 서비스:**

```json
{
    "name": "AzureStorageLinkedService",
    "properties": {
    "type": "AzureStorage",
    "typeProperties": {
        "connectionString": "DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"
    }
    }
}
```
**PostgreSQL 입력 데이터 집합:**

hello 샘플 테이블 "MyTable"에서 만든 PostgreSQL 가정 시계열 데이터에 대 한 "timestamp" 라는 열을 포함 합니다.

설정 `"external": true` 알리고 hello 데이터 팩터리 서비스 hello 데이터 집합의 데이터 팩터리 외부 toohello hello data factory에는 활동에 의해 생성 되지 않습니다.

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

**Azure Blob 출력 데이터 집합:**

데이터가 새 blob tooa 1 시간 마다 기록 됩니다 (빈도: 시, 간격: 1). hello 폴더 경로 파일 이름은 hello blob에 대 한 처리 중인 hello 조각의 hello 시작 시간에 따라 동적으로 평가 됩니다. hello 폴더 경로 hello 시작 시간의 연도, 월, 일 및 시간 부분을 사용 합니다.

```json
{
    "name": "AzureBlobPostgreSqlDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/postgresql/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

**복사 작업을 포함하는 파이프라인:**

hello 파이프라인에 포함 된 구성된 toouse 않은 복사 작업은 예약 된 toorun 매 및 hello 입력 및 출력 데이터 집합. Hello 파이프라인 JSON 정의에서 hello **소스** 형식이 너무 설정**RelationalSource** 및 **싱크** 형식이 너무 설정**BlobSink**합니다. hello에 대 한 지정 된 hello SQL 쿼리 **쿼리** 속성 hello PostgreSQL 데이터베이스의 hello public.usstates 테이블에서 hello 데이터를 선택 합니다.

```json
{
    "name": "CopyPostgreSqlToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
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
                "inputs": [
                    {
                        "name": "PostgreSqlDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobPostgreSqlDataSet"
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
                "name": "PostgreSqlToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```
## <a name="type-mapping-for-postgresql"></a>PostgreSQL에 대한 형식 매핑
Hello에 설명 된 대로 [데이터 이동 작업](data-factory-data-movement-activities.md) 문서 복사 작업 단계 2 방식을 따릅니다 hello로 원본 형식 toosink 유형의 자동 형식 변환을 수행 합니다.

1. 네이티브 소스 형식 too.NET 형식에서 변환
2. .NET 형식 toonative 싱크 형식에서 변환

데이터 tooPostgreSQL를 이동할 때는 hello 다음 매핑은 사용 하는 PostgreSQL 형식 too.NET 형식에서 합니다.

| PostgreSQL 데이터베이스 형식 | PostgresSQL 별칭 | .NET Framework 형식 |
| --- | --- | --- |
| abstime | |Datetime | &nbsp;
| bigint |int8 |Int64 |
| bigserial |serial8 |Int64 |
| bit [ (n) ] | |Byte[], String | &nbsp;
| bit varying [ (n) ] |varbit |Byte[], String |
| 부울 |bool |부울 |
| box | |Byte[], String |&nbsp;
| bytea | |Byte[], String |&nbsp;
| character [ (n) ] |char [ (n) ] |문자열 |
| character varying [ (n) ] |varchar [ (n) ] |문자열 |
| cid | |문자열 |&nbsp;
| cidr | |문자열 |&nbsp;
| circle | |Byte[], String |&nbsp;
| date | |Datetime |&nbsp;
| daterange | |문자열 |&nbsp;
| double precision |float8 |Double |
| inet | |Byte[], String |&nbsp;
| intarry | |문자열 |&nbsp;
| int4range | |문자열 |&nbsp;
| int8range | |문자열 |&nbsp;
| 정수 |int, int4 |Int32 |
| interval [ fields ] [ (p) ] | |Timespan |&nbsp;
| json : | |문자열 |&nbsp;
| jsonb | |Byte[] |&nbsp;
| line | |Byte[], String |&nbsp;
| lseg | |Byte[], String |&nbsp;
| macaddr | |Byte[], String |&nbsp;
| money | |10진수 |&nbsp;
| numeric [ (p, s) ] |decimal [ (p, s) ] |10진수 |
| numrange | |문자열 |&nbsp;
| oid | |Int32 |&nbsp;
| path | |Byte[], String |&nbsp;
| pg_lsn | |Int64 |&nbsp;
| point | |Byte[], String |&nbsp;
| polygon | |Byte[], String |&nbsp;
| real |float4 |Single |
| smallint |int2 |Int16 |
| smallserial |serial2 |Int16 |
| serial |serial4 |Int32 |
| 텍스트 | |문자열 |&nbsp;

## <a name="map-source-toosink-columns"></a>원본 toosink 열 매핑
원본 데이터 집합 toocolumns 싱크 데이터 집합에서의 열을 매핑하는 방법에 대 한 toolearn 참조 [Azure Data Factory에서 데이터 집합 열에 매핑](data-factory-map-columns.md)합니다.

## <a name="repeatable-read-from-relational-sources"></a>관계형 원본에서 반복 가능한 읽기
관계형 데이터 저장소에서 데이터를 복사할 때 유의 tooavoid에서 반복성을 유지 의도 하지 않은 결과입니다. Azure Data Factory에서는 조각을 수동으로 다시 실행할 수 있습니다. 또한 오류가 발생하면 조각을 다시 실행하도록 데이터 집합에 대한 재시도 정책을 구성할 수 있습니다. Toomake 동일한 데이터를 hello 있는지 어떻게에 관계 없이 읽기 필요한 어느 쪽에 분할 영역을 다시 실행 하는 경우 조각에 여러 번 실행 됩니다. [관계형 원본에서 반복 가능한 읽기](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)를 참조하세요.

## <a name="performance-and-tuning"></a>성능 및 튜닝
참조 [복사 활동 성능 및 조정 가이드](data-factory-copy-activity-performance.md) toolearn 키에 대 한 Azure 데이터 팩터리 및 다양 한 방법으로 toooptimize에서 데이터 이동 (복사 작업)의 성능에 영향을 해당 놓은 것입니다.

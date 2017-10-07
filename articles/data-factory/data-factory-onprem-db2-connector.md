---
title: "Azure 데이터 팩터리를 사용 하 여 d b 2에서 aaaMove 데이터 | Microsoft Docs"
description: "Azure 데이터 팩터리 복사 작업을 사용 하 여 toomove 데이터를 온-프레미스 DB2 데이터베이스 하는 방법에 대해 알아봅니다"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: c1644e17-4560-46bb-bf3c-b923126671f1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jingwang
ms.openlocfilehash: 696ac059be644cb3901c37d2fc746e0682c65a1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-db2-by-using-azure-data-factory-copy-activity"></a>Azure Data Factory 복사 활동을 사용하여 DB2에서 데이터 이동
이 문서에서는 온-프레미스 DB2 데이터베이스 tooa 데이터 저장소에서 Azure Data Factory toocopy 데이터에서 복사 작업을 사용 하는 방법을 설명 합니다. Hello에 지원 되는 싱크로 나열 되어 있는 데이터 tooany 저장소를 복사할 수는 있지만 [Data Factory 데이터 이동 작업](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 문서. 이 항목 복사 작업을 사용 하 여 데이터 이동의 개요를 제공 하 고 hello 지원 데이터 저장소 조합을 나열 하는 hello Data Factory 문서 기반으로 합니다. 

Data Factory에는 현재 DB2 데이터베이스 tooa 동안의 데이터만 이동 지원 [싱크를 지원 되는 데이터 저장소](data-factory-data-movement-activities.md#supported-data-stores-and-formats)합니다. 다른 데이터에서 데이터를 이동 저장 tooa DB2 데이터베이스에 지원 되지 않습니다.

## <a name="prerequisites"></a>필수 조건
데이터 팩터리 hello를 사용 하 여 연결 tooan 온-프레미스 DB2 데이터베이스를 지원 [데이터 관리 게이트웨이](data-factory-data-management-gateway.md)합니다. 단계별 지침은 tooset hello 게이트웨이 데이터를 데이터 toomove 파이프라인을 참조 하십시오 hello [toocloud 온-프레미스에서에서 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서.

게이트웨이 hello d b 2에서 호스팅되는 Azure IaaS VM 하는 경우에 필요 합니다. Hello에 hello 게이트웨이 설치할 수 있습니다 hello 데이터 저장소로 동일한 IaaS VM입니다. Hello 게이트웨이 toohello 데이터베이스를 연결할 수 경우 다른 VM에 hello 게이트웨이 설치할 수 있습니다.

하지 않으면 하므로 필요 toomanually 설치 드라이버 toocopy 데이터 d b 2에서, hello 데이터 관리 게이트웨이 기본 제공 DB2 드라이버를 제공 합니다.

> [!NOTE]
> 연결 및 게이트웨이 문제를 해결 하는 정보에 대 한 참조 hello [게이트웨이 문제 해결](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) 문서.


## <a name="supported-versions"></a>지원되는 버전
데이터 팩터리 DB2 hello 커넥터 IBM DB2 플랫폼 및 버전 9, 10 및 11 DRDA 분산 관계형 데이터베이스 아키텍처 () SQL 액세스 관리자 버전에 따라 hello를 지원 합니다.

* z/OS용 IBM DB2 버전 11.1
* z/OS용 IBM DB2 버전 10.1
* i(AS400)용 IBM DB2 버전 7.2
* i(AS400)용 IBM DB2 버전 7.1
* LUW(Linux, UNIX, and Windows)용 IBM DB2 버전 11
* LUW용 IBM DB2 버전 10.5
* LUW용 IBM DB2 버전 10.1

> [!TIP]
> "Hello 패키지 해당 tooan SQL 문 실행 요청을 찾을 수 없습니다 hello 오류 메시지가 표시 되 면. SQLSTATE 805-51002 SQLCODE =, = "hello 이유는 hello 일반 사용자 hello 운영 체제에 대 한 필수 패키지 만들어지지 않습니다. tooresolve이 문제를 DB2 서버 유형에 대 한 다음이 지침을 따릅니다.
> - 용 DB2 (AS400) i: 전원 사용자 hello 일반 사용자에 대 한 복사 작업을 실행 하기 전에 hello 컬렉션을 만들 수 있도록 합니다. 명령 사용 하 여 hello toocreate hello 컬렉션:`create collection <username>`
> - Z/OS 또는 LUW 용 d b 2: 권한이 높은 계정-고급 사용자 또는 관리자가 패키지 기관과 BINDADD, 바인딩, 사용 권한을 EXECUTE tooPUBLIC-toorun hello를 한 번만 복사 합니다. 필수 패키지 hello hello 복사 중 자동으로 만들어집니다. 나중에 후속 복사 실행에 대 한 백 toohello 일반 사용자를 전환할 수 있습니다.

## <a name="getting-started"></a>시작
온-프레미스 DB2 데이터 저장소에서 복사 활동 toomove 데이터와 함께 다른 도구와 Api를 사용 하 여 파이프라인을 만들 수 있습니다. 

- hello 가장 쉬운 방법은 toocreate 파이프라인은 toouse hello Azure 데이터 팩터리 복사 마법사입니다. Hello 복사 마법사를 사용 하 여 파이프라인을 만드는 방법에 간략 한 설명이, 참조 hello [자습서: hello 복사 마법사를 사용 하 여 파이프라인을 만들고](data-factory-copy-data-wizard-tutorial.md)합니다. 
- 도구 toocreate hello Azure 포털, Visual Studio, Azure PowerShell는 Azure 리소스 관리자 템플릿, hello.NET API 및 hello를 포함 하 여 파이프라인을 사용할 수도 있습니다 REST API입니다. 단계별 지침은 toocreate 복사 작업으로 파이프라인에 대 한 참조 hello [복사 작업 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)합니다. 

Hello 도구 또는 Api를 사용 하는지 여부를 hello tooa 싱크 데이터 저장소를 저장 하는 원본 데이터에서 데이터를 이동 하는 파이프라인 단계 toocreate 다음을 수행 합니다.

1. 연결 된 서비스 toolink 입력 및 출력 데이터 저장소 tooyour 데이터 팩터리를 만듭니다.
2. Toorepresent 입력 데이터 집합을 만들고 hello 복사 작업에 대 한 데이터를 출력 합니다. 
3. 입력과 출력으로 각각의 데이터 집합을 사용하는 복사 활동이 포함된 파이프라인을 만듭니다. 

Hello hello Data Factory 연결 서비스에 대 한 JSON 정의 복사 마법사를 사용 하는 경우 데이터 집합 및 파이프라인 엔터티는 자동으로 생성 합니다. 도구 또는 Api를 사용 하 여 hello.NET API) (제외 hello JSON 형식을 사용 하 여 hello Data Factory 엔터티를 정의 합니다. hello [JSON의 예: DB2 tooAzure Blob 저장소에서에서 데이터를 복사](#json-example-copy-data-from-db2-to-azure-blob) 온-프레미스 DB2 데이터 저장소에서 사용 되는 toocopy 데이터 엔터티를 Data Factory hello에 대 한 hello JSON 정의 표시 합니다.

다음 섹션 hello JSON 속성을 사용 하는 toodefine hello Data Factory 된 엔터티를 특정 tooa DB2 데이터 저장소 hello에 대 한 세부 정보를 제공 합니다.

## <a name="db2-linked-service-properties"></a>DB2 연결된 서비스 속성
다음 표에서 hello 특정 tooa DB2 연결 서비스는 hello JSON 속성을 나열 합니다.

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| **type** |이 속성을 너무 설정 해야**OnPremisesDB2**합니다. |예 |
| **server** |hello DB2 서버 hello 이름입니다. |예 |
| **database** |hello DB2 데이터베이스의 hello 이름입니다. |예 |
| **schema** |hello DB2 데이터베이스에 대 한 hello 스키마의 hello 이름입니다. 대/소문자를 구분합니다. |아니요 |
| **authenticationType** |인증 시 사용 되는 tooconnect toohello DB2 데이터베이스의 hello 형식입니다. hello 가능한 값은: 익명, 기본 및 Windows. |예 |
| **사용자 이름** |기본 인증 또는 Windows 인증을 사용 하는 경우 hello 사용자 계정에 대 한 hello 이름입니다. |아니요 |
| **암호** |hello hello 사용자 계정의 암호입니다. |아니요 |
| **gatewayName** |데이터 팩터리 서비스 hello hello 게이트웨이의 hello 이름 tooconnect toohello 온-프레미스 DB2 데이터베이스를 사용 해야 합니다. |예 |

## <a name="dataset-properties"></a>데이터 집합 속성
Hello 섹션 및 데이터 집합 정의에 사용할 수 있는 속성 목록에 대 한 참조 hello [데이터 집합을 만드는](data-factory-create-datasets.md) 문서. 와 같은 섹션 **구조**, **가용성**, 및 hello **정책** JSON는 데이터 집합에 대 한 권장 사항과 비슷합니다 (Azure SQL, Azure Blob 저장소, Azure 테이블에 모든 데이터 집합 형식에 대 한 저장소 및 등)입니다.

hello **typeProperties** 데이터 집합의 각 형식에 대 한 다른 섹션과 hello 데이터 저장소에 hello 데이터의 hello 위치에 대 한 정보를 제공 합니다. hello **typeProperties** 형식의 데이터 집합에 대 한 섹션 **RelationalTable**, hello DB2 데이터 집합에 포함 되어 있는, hello 속성 뒤에:

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| **tableName** |hello 연결 된 서비스는 hello DB2 데이터베이스 인스턴스의 hello 테이블의 hello 이름을 가리킵니다. 대/소문자를 구분합니다. |더 (경우 hello **쿼리** 형식의 복사 작업의 속성 **RelationalSource** 지정) |

## <a name="copy-activity-properties"></a>복사 활동 속성
Hello 섹션 및 복사 활동 정의에 사용할 수 있는 속성 목록에 대 한 참조 hello [파이프라인 만들기](data-factory-create-pipelines.md) 문서. **name**, **description**, **inputs** 테이블, **outputs** 테이블 및 **policy**와 같은 복사 활동 속성은 모든 유형의 활동에 사용할 수 있습니다. hello에서 사용할 수 있는 속성 hello **typeProperties** 각 활동 유형에 대 한 hello 활동의 섹션입니다. 복사 작업에 대 한 hello 속성의 데이터 원본 및 싱크 hello 유형에 따라 달라 집니다.

Hello 원본 유형인 경우 복사 작업에 대 한 **RelationalSource** (DB2 포함), 다음과 같은 속성 hello hello에서 사용할 수 있는 **typeProperties** 섹션:

| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| **query** |Hello tooread hello 데이터 사용자 지정 쿼리를 사용 합니다. |SQL 쿼리 문자열. 예: `"query": "select * from "MySchema"."MyTable""` |더 (경우 hello **tableName** 속성이 데이터 집합의 지정 된) |

> [!NOTE]
> 스키마 및 테이블 이름은 대/소문자를 구분합니다. Hello 쿼리문을에서 속성 이름을 사용 하 여 묶습니다 "" (큰따옴표). 예:
>
> ```sql
> "query": "select * from "DB2ADMIN"."Customers""
> ```

## <a name="json-example-copy-data-from-db2-tooazure-blob-storage"></a>JSON의 예: DB2 tooAzure Blob 저장소에서에서 데이터 복사
이 예제에서는 샘플 JSON 정의 제공 hello를 사용 하 여 toocreate 파이프라인을 사용할 수 있는 [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), 또는 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)합니다. hello 예제 toocopy 데이터는 d b 2에서 데이터베이스 tooBlob 저장소 방법을 보여 줍니다. 하지만 데이터를 너무 복사할 수 있습니다[모든 지원 되는 데이터 저장 싱크 유형이](data-factory-data-movement-activities.md#supported-data-stores-and-formats) Azure 데이터 팩터리 복사 작업을 사용 하 여 합니다.

hello 샘플 Data Factory 엔터티에 따라 hello에 있습니다.

- [OnPremisesDb2](data-factory-onprem-db2-connector.md#linked-service-properties) 형식의 DB2 연결된 서비스
- [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) 형식의 Azure Blob 저장소 연결된 서비스
- [RelationalTable](data-factory-onprem-db2-connector.md#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)
- [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)
- A [파이프라인](data-factory-create-pipelines.md) hello를 사용 하 여 복사 활동으로 [RelationalSource](data-factory-onprem-db2-connector.md#copy-activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) 속성

hello 샘플에 1 시간 마다 DB2 데이터베이스 tooan Azure blob에서에서 쿼리 결과에서 데이터 복사합니다. hello 샘플에 사용 되는 hello JSON 속성 hello 엔터티 정의 다음에 나오는 hello 섹션에 설명 되어 있습니다.

첫 번째 단계로 데이터 관리 게이트웨이를 설치하고 구성합니다. 지침은 hello [온-프레미스 위치와 클라우드 간의 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서.

**DB2 연결된 서비스**

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

**Azure Blob 저장소 연결된 서비스**

```json
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorageLinkedService",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"
        }
    }
}
```

**DB2 입력 데이터 집합**

hello 샘플 hello 시계열 데이터에 대 한 "timestamp" 레이블이 지정 된 열이 있는 "MyTable" 이라는 DB2 테이블 만들었다고 가정 합니다.

hello **외부** 속성 너무 "true로 설정 되어 있습니다." 이 설정은이 데이터 집합 데이터 팩터리 외부 toohello 이며 hello data factory에는 활동에 의해 생성 되지 않을 hello 데이터 팩터리 서비스에 알립니다. 해당 hello 확인 **형식** 너무 속성이**RelationalTable**합니다.


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

**Azure Blob 출력 데이터 집합**

데이터에서 작성 되었습니다. 새 blob tooa 1 시간 마다 hello 설정 **주파수** 속성 너무 "시간" 및 hello **간격** 속성 too1 합니다. hello **folderPath** 처리 중인 hello 조각의 hello 시작 시간에 따라 hello blob 동적으로 평가 대 한 속성입니다. hello 폴더 경로 hello 시작 시간의 hello 연도, 월, 일 및 시간 부분을 사용 합니다.

```json
{
    "name": "AzureBlobDb2DataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/db2/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

**Hello 복사 작업에 대 한 파이프라인**

구성 된 복사 작업을 포함 하는 hello 파이프라인 toouse 입력 및 출력 데이터 집합을 지정 하 고 예약 된 toorun를 1 시간 마다가입니다. Hello hello 파이프라인에 대 한 JSON 정의에서 hello **소스** 형식이 너무 설정**RelationalSource** 및 hello **싱크** 형식이 너무 설정**BlobSink**. hello에 대 한 지정 된 hello SQL 쿼리 **쿼리** 속성 hello "Orders" 테이블에서 hello 데이터를 선택 합니다.

```json
{
    "name": "CopyDb2ToBlob",
    "properties": {
        "description": "pipeline for hello copy activity",
        "activities": [
            {
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
                "inputs": [
                    {
                        "name": "Db2DataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobDb2DataSet"
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
                "name": "Db2ToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```

## <a name="type-mapping-for-db2"></a>DB2에 대한 형식 매핑
Hello에 설명 된 대로 [데이터 이동 작업](data-factory-data-movement-activities.md) 문서, 복사 작업 2 단계 방식을 따릅니다 hello를 사용 하 여 소스 형식 toosink 형식을 자동 형식 변환을 수행 합니다.

1. 가 네이티브 소스 형식 tooa.NET 형식에서 변환
2. .NET 형식 tooa 네이티브 싱크 형식에서 변환

hello 다음 매핑은 사용 하는 복사 작업 DB2 형식 tooa.NET 유형에 서 hello 데이터를 변환 하는 경우:

| DB2 데이터베이스 형식 | .NET Framework 형식 |
| --- | --- |
| SmallInt |Int16 |
| Integer |Int32 |
| BigInt |Int64 |
| Real |단일 |
| Double |Double |
| Float |Double |
| 10진수 |10진수 |
| DecimalFloat |10진수 |
| 숫자 |10진수 |
| Date |DateTime |
| Time |TimeSpan |
| Timestamp |Datetime |
| xml |Byte[] |
| Char |문자열 |
| VarChar |문자열 |
| LongVarChar |문자열 |
| DB2DynArray |문자열 |
| 이진 |Byte[] |
| VarBinary |Byte[] |
| LongVarBinary |Byte[] |
| Graphic |문자열 |
| VarGraphic |문자열 |
| LongVarGraphic |문자열 |
| Clob |문자열 |
| Blob |Byte[] |
| DbClob |문자열 |
| SmallInt |Int16 |
| Integer |Int32 |
| BigInt |Int64 |
| Real |단일 |
| Double |Double |
| Float |Double |
| 10진수 |10진수 |
| DecimalFloat |10진수 |
| 숫자 |10진수 |
| Date |DateTime |
| Time |TimeSpan |
| Timestamp |Datetime |
| xml |Byte[] |
| Char |문자열 |

## <a name="map-source-toosink-columns"></a>원본 toosink 열 매핑
hello 싱크 데이터 집합의 원본 데이터 집합 toocolumns hello의에서 toomap 열 참조 toolearn [Azure Data Factory에서 데이터 집합 열에 매핑](data-factory-map-columns.md)합니다.

## <a name="repeatable-reads-from-relational-sources"></a>관계형 원본에서 반복 가능한 읽기
관계형 데이터 저장소에서 데이터를 복사할 때 유의 tooavoid에 반복성을 유지 의도 하지 않은 결과입니다. Azure Data Factory에서는 조각을 수동으로 다시 실행할 수 있습니다. Hello 재시도 구성할 수도 있습니다 **정책** dataset toorerun 오류 발생 시 분할 영역에 대 한 속성. 동일한 데이터 방법에 관계 없이 읽는 hello 하 고 있는지 확인을 다시 실행 하 고 hello 조각을 다시 실행 방법에 관계 없이 여러 번 hello 조각이 되었습니다. 자세한 내용은 [관계형 원본에서 반복 가능한 읽기](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)를 참조하세요.

## <a name="performance-and-tuning"></a>성능 및 튜닝
복사 활동와 같은 방법으로 toooptimize 성능을 hello에 hello 성능에 영향을 주는 주요 요인에 대 한 자세한 내용은 [복사 활동 성능 및 조정 가이드](data-factory-copy-activity-performance.md)합니다.

---
title: "aaaMove 데이터를 Azure 데이터 팩터리를 사용 하 여 SAP HANA | Microsoft Docs"
description: "방법에 대 한 자세한 내용은 Azure 데이터 팩터리를 사용 하 여 SAP HANA의 toomove 데이터입니다."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: 5cefe4c8ed01ea4e86e02496b2f8a9083d0b949c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-sap-hana-using-azure-data-factory"></a>Azure Data Factory를 사용하여 SAP HANA에서 데이터 이동
이 문서에서는 Azure Data Factory toomove 데이터는 온-프레미스 SAP HANA에 있는 toouse 복사 작업 hello 하는 방법을 설명 합니다. Hello에 기반 [데이터 이동 작업](data-factory-data-movement-activities.md) hello 복사 작업으로 데이터 이동에 대 한 일반적인 개요를 제공 하는 문서입니다.

온-프레미스 SAP HANA 데이터 저장소 지원 tooany 싱크 데이터 저장소에서 데이터를 복사할 수 있습니다. 데이터 목록에 대 한 지원 저장소 hello 복사 작업에서 싱크 참조 hello [데이터 저장소를 지원](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 테이블입니다. 데이터 팩터리의 현재만 지 원하는 데이터를 SAP HANA tooother 데이터에서에서 저장 하지 않은 이동 tooan SAP HANA 저장소 다른 데이터에서 데이터를 이동 합니다.

## <a name="supported-versions-and-installation"></a>지원되는 버전 및 설치
이 커넥터는 모든 버전의 SAP HANA 데이터베이스를 지원합니다. SQL 쿼리를 사용한 행/열 테이블 및 HANA 정보 모델(예: 분석 및 계산 보기)의 데이터 복사를 지원합니다.

tooenable hello 연결 toohello SAP HANA 인스턴스는 다음과 같은 구성 요소가 hello를 설치 합니다.
- **데이터 관리 게이트웨이**: Data Factory 서비스가 지 원하는 tooon 온-프레미스 데이터 연결 (포함 하 여 SAP HANA) 저장소 데이터 관리 게이트웨이 라는 구성 요소를 사용 합니다. 데이터 관리 게이트웨이 및 hello 게이트웨이 설정에 대 한 단계별 지침에 대 한 toolearn 참조 [toocloud 데이터 저장소를 저장 하는 온-프레미스 데이터 간의 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서. 게이트웨이 SAP HANA hello Azure IaaS 가상 컴퓨터 (VM)에서 호스팅되는 경우에 필요 합니다. 동일한 VM hello 데이터로 저장 하거나 hello 게이트웨이 다른 VM에 연결할 수 toohello 데이터베이스 hello에 hello 게이트웨이 설치할 수 있습니다.
- **SAP HANA ODBC 드라이버** hello 게이트웨이 컴퓨터에 있습니다. Hello에서 hello SAP HANA ODBC 드라이버를 다운로드할 수 있습니다 [SAP 소프트웨어 다운로드 센터](https://support.sap.com/swdc)합니다. Hello 키워드를 사용 하 여 검색 **SAP HANA CLIENT for Windows**합니다. 

## <a name="getting-started"></a>시작
여러 도구/API를 사용하여 온-프레미스 Cassandra 데이터 저장소의 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다. 

- hello 가장 쉬운 방법은 toocreate 파이프라인은 toouse hello **복사 마법사**합니다. 참조 [자습서: 복사 마법사를 사용 하 여 파이프라인을 만들고](data-factory-copy-data-wizard-tutorial.md) 간략 한 설명이 hello 복사 데이터 마법사를 사용 하 여 파이프라인을 만드는 방법에 대 한 합니다. 
- 다음 도구 toocreate 파이프라인 hello을 사용할 수 있습니다: **Azure 포털**, **Visual Studio**, **Azure PowerShell**, **Azure 리소스 관리자 템플릿** , **.NET API**, 및 **REST API**합니다. 참조 [복사 활동 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 단계별 지침 toocreate 복사 작업으로 파이프라인에 대 한 합니다. 

Hello 도구 또는 Api를 사용 하는지 여부를 hello tooa 싱크 데이터 저장소를 저장 하는 원본 데이터에서 데이터를 이동 하는 파이프라인 단계 toocreate 다음을 수행 합니다.

1. 만들 **연결 된 서비스** toolink 입력 및 출력 데이터 저장소 tooyour 데이터 팩터리입니다.
2. 만들 **데이터 집합** 입력 및 출력 toorepresent hello에 대 한 데이터 복사 작업을 합니다. 
3. 입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다. 

Hello 마법사를 사용 하 여 이러한 데이터 팩터리 엔터티 (연결 된 서비스, 데이터 집합 및 hello 파이프라인)에 대 한 JSON 정의를 자동으로 만들어집니다. 도구/Api (제외.NET API)를 사용 하면 hello JSON 형식을 사용 하 여이 Data Factory 엔터티를 정의 합니다.  Data Factory 된 엔터티를 사용 하는 toocopy 데이터를 온-프레미스 SAP HANA에 대 한 JSON 정의 된 샘플을 보려면 [JSON의 예: SAP HANA tooAzure Blob에서에서 데이터를 복사](#json-example-copy-data-from-sap-hana-to-azure-blob) 이 문서의 섹션. 

다음 섹션 hello JSON 속성을 사용 하는 toodefine Data Factory 엔터티에 특정 tooan SAP HANA 데이터 저장소에 대 한 세부 정보를 제공 합니다.

## <a name="linked-service-properties"></a>연결된 서비스 속성
다음 표에서 hello JSON 요소 특정 tooSAP HANA에 대 한 연결 된 서비스를 제공 합니다.

속성 | 설명 | 허용되는 값 | 필수
-------- | ----------- | -------------- | --------
server | SAP HANA는 hello에 인스턴스가 있는 hello 서버의 이름입니다. 서버에서 사용자 지정된 포트를 사용하는 경우 `server:port`를 지정합니다. | string | 예
authenticationType | 인증 유형입니다. | string. "Basic" 또는 "Windows" | 예 
username | Toohello SAP 서버 액세스를 갖고 있는 hello 사용자의 이름 | string | 예
암호 | Hello 사용자 암호입니다. | string | 예
gatewayName | 데이터 팩터리 서비스 hello hello 게이트웨이의 이름 tooconnect toohello 온-프레미스 SAP HANA 인스턴스를 사용 해야 합니다. | string | 예
encryptedCredential | hello 암호화 된 자격 증명 문자열입니다. | string | 아니요

## <a name="dataset-properties"></a>데이터 집합 속성
섹션 및 데이터 집합 정의에 사용 가능한 속성의 전체 목록을 보려면 hello [데이터 집합을 만드는](data-factory-create-datasets.md) 문서. 구조, 가용성 및 JSON 데이터 집합의 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다(Azure SQL, Azure blob, Azure 테이블 등).

hello **typeProperties** 데이터 집합의 각 형식에 대 한 다른 섹션과 hello 데이터 저장소에 hello 데이터의 hello 위치에 대 한 정보를 제공 합니다. 형식의 hello SAP HANA 데이터 집합에 대 한 지원 유형별 속성이 없는 **RelationalTable**합니다. 


## <a name="copy-activity-properties"></a>복사 작업 속성
섹션 및 활동 정의에 사용 가능한 속성의 전체 목록을 참조 hello [파이프라인 만들기](data-factory-create-pipelines.md) 문서. 이름, 설명, 입력/출력 테이블, 정책 등의 속성은 모든 형식의 활동에 사용할 수 있습니다.

반면 hello에 사용할 수 있는 속성 **typeProperties** hello 활동의 섹션에 각 활동 유형에 따라 다릅니다. 복사 작업은 원본 및 싱크의 hello 형식에 따라 변경합니다.

복사 작업의 원본 유형의 경우 **RelationalSource** (SAP HANA 포함), 다음과 같은 속성 hello typeProperties 섹션에서 사용할 수 있는:

| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| 쿼리 | Hello SAP HANA 인스턴스에서 hello SQL 쿼리 tooread 데이터를 지정합니다. | SQL 쿼리. | 예 |

## <a name="json-example-copy-data-from-sap-hana-tooazure-blob"></a>JSON의 예: SAP HANA tooAzure Blob에서에서 데이터 복사
hello 다음 예제에서는 제공 샘플 JSON 정의 사용 하 여 toocreate 파이프라인을 사용할 수 있는 [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md) 또는 [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 또는 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)합니다. 이 샘플은 어떻게 온-프레미스 SAP HANA tooan Azure Blob 저장소에서에서 toocopy 데이터입니다. 그러나 데이터를 복사할 수 있습니다 **직접** 나열 된 hello 싱크 tooany [여기](data-factory-data-movement-activities.md#supported-data-stores-and-formats) Azure Data Factory에서 복사 작업 hello를 사용 하 여 합니다.  

> [!IMPORTANT]
> 이 샘플은 JSON 코드 조각을 제공합니다. Hello 데이터 팩터리를 만들기 위한 단계별 지침을 다루지 않습니다. 단계별 지침은 [온-프레미스 위치와 클라우드 간에 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서를 참조하세요.

hello 샘플 hello 데이터 팩터리 엔터티 뒤에 있습니다.

1. [SapHana](#linked-service-properties) 형식의 연결된 서비스
2. [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) 형식의 연결된 서비스
3. [RelationalTable](#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)
4. [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)
5. [RelationalSource](#copy-activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)

hello 샘플에 1 시간 마다 SAP HANA 인스턴스 tooan Azure blob에서에서 데이터 복사합니다. 이 예제에 사용 되는 hello JSON 속성 hello 샘플 다음 섹션에 설명 되어 있습니다.

첫 번째 단계로, hello 데이터 관리 게이트웨이 설치 합니다. hello 지침은 hello [온-프레미스 위치와 클라우드 간의 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서.

### <a name="sap-hana-linked-service"></a>SAP HANA 연결된 서비스
SAP HANA 인스턴스 toohello 데이터 팩터리 서비스 링크 연결이 있습니다. hello type 속성이 너무 설정 되어**SapHana**합니다. hello typeProperties 섹션 hello SAP HANA 인스턴스에 대 한 연결 정보를 제공 합니다.

```json
{
    "name": "SapHanaLinkedService",
    "properties":
    {
        "type": "SapHana",
        "typeProperties":
        {
            "server": "<server name>",
            "authenticationType": "<Basic, or Windows>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}

```

### <a name="azure-storage-linked-service"></a>Azure 저장소 연결된 서비스
Azure 저장소 계정 toohello 데이터 팩터리 서비스 링크 연결이 있습니다. hello type 속성이 너무 설정 되어**AzureStorage**합니다. hello typeProperties 섹션 hello Azure 저장소 계정에 대 한 연결 정보를 제공 합니다.

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

### <a name="sap-hana-input-dataset"></a>SAP HANA 입력 데이터 집합

이 데이터 집합 hello SAP HANA 데이터 집합을 정의합니다. Hello Data Factory 데이터 집합의 hello 유형을 너무 설정**RelationalTable**합니다. 현재 SAP HANA 데이터 집합에 대한 type별 속성은 지정하지 않습니다. hello 쿼리 hello 복사 활동 정의에서 어떤 데이터 tooread hello SAP HANA 인스턴스에서 지정합니다. 

외부 속성 tootrue 설정 알리고 hello 데이터 팩터리 서비스 hello 테이블 데이터 팩터리 외부 toohello hello data factory에는 활동에 의해 생성 되지 않습니다.

빈도 간격 속성은 hello 일정을 정의 합니다. 이 경우 hello 데이터를 읽을 hello SAP HANA 인스턴스에서 1 시간 마다. 

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

### <a name="azure-blob-output-dataset"></a>Azure Blob 출력 데이터 집합
이 데이터 집합 hello 출력 Azure Blob 데이터 집합을 정의합니다. hello type 속성이 tooAzureBlob 설정 되어 있습니다. hello typeProperties 섹션 hello SAP HANA 인스턴스에서 복사한 hello 데이터 저장 위치를 제공 합니다. hello 데이터 tooa 새 blob 1 시간 마다 기록 됩니다 (빈도: 시, 간격: 1). hello blob에 대 한 hello 폴더 경로 처리 중인 hello 조각의 hello 시작 시간에 따라 동적으로 평가 됩니다. hello 폴더 경로 hello 시작 시간의 연도, 월, 일 및 시간 부분을 사용 합니다.

```json
{
    "name": "AzureBlobDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/saphana/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="pipeline-with-copy-activity"></a>복사 작업을 포함하는 파이프라인

hello 파이프라인에 포함 된 구성된 toouse 않은 복사 작업 입력 및 출력 데이터 집합을 hello 및 예약 된 toorun 1 시간입니다. Hello 파이프라인 JSON 정의에서 hello **소스** 형식이 너무 설정**RelationalSource** (SAP HANA 소스)에 대 한 및 **싱크** 형식이 너무 설정**BlobSink**. hello에 대 한 지정 된 hello SQL 쿼리 **쿼리** 속성 시간 toocopy 지난 hello에 hello 데이터를 선택 합니다.

```json
{
    "name": "CopySapHanaToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
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
                "inputs": [
                    {
                        "name": "SapHanaDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobDataSet"
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
                "name": "SapHanaToBlob"
            }
        ],
        "start": "2017-03-01T18:00:00Z",
        "end": "2017-03-01T19:00:00Z"
    }
}
```


### <a name="type-mapping-for-sap-hana"></a>SAP HANA에 대한 형식 매핑
Hello에 설명 된 대로 [데이터 이동 작업](data-factory-data-movement-activities.md) 문서, 복사 작업 소스 형식 toosink 형식에서 자동 형식 변환 2 단계 방식을 따릅니다 hello로 수행:

1. 네이티브 소스 형식 too.NET 형식에서 변환
2. .NET 형식 toonative 싱크 형식에서 변환

SAP HANA에서 데이터를 이동할 때는 다음 매핑을 hello SAP HANA 형식 too.NET 형식에서 사용 됩니다.

SAP HANA 형식 | .NET 기반 형식
------------- | ---------------
TINYINT | Byte
SmallInt | Int16
INT | Int32
BIGINT | Int64
Real | 단일
DOUBLE | 단일
DECIMAL | 10진수
BOOLEAN | Byte
VARCHAR | 문자열
NVARCHAR | string
CLOB | Byte[]
ALPHANUM | 문자열
BLOB | Byte[]
DATE | DateTime
TIME | timespan
TIMESTAMP | DateTime
SECONDDATE | DateTime

## <a name="known-limitations"></a>알려진 제한 사항
SAP HANA에서 데이터를 복사하는 경우 몇 가지 알려진 제한 사항이 있습니다.

- NVARCHAR 문자열은 잘림된 toomaximum 길이 4000 유니코드 문자
- SMALLDECIMAL은 지원되지 않습니다.
- VARBINARY는 지원되지 않습니다.
- 유효한 날짜는 1899/12/30 ~ 9999/12/31입니다.

## <a name="map-source-toosink-columns"></a>원본 toosink 열 매핑
원본 데이터 집합 toocolumns 싱크 데이터 집합에서의 열을 매핑하는 방법에 대 한 toolearn 참조 [Azure Data Factory에서 데이터 집합 열에 매핑](data-factory-map-columns.md)합니다.

## <a name="repeatable-read-from-relational-sources"></a>관계형 원본에서 반복 가능한 읽기
관계형 데이터 저장소에서 데이터를 복사할 때 유의 tooavoid에서 반복성을 유지 의도 하지 않은 결과입니다. Azure Data Factory에서는 조각을 수동으로 다시 실행할 수 있습니다. 또한 오류가 발생하면 조각을 다시 실행하도록 데이터 집합에 대한 재시도 정책을 구성할 수 있습니다. Toomake 동일한 데이터를 hello 있는지 어떻게에 관계 없이 읽기 필요한 어느 쪽에 분할 영역을 다시 실행 하는 경우 조각에 여러 번 실행 됩니다. [관계형 원본에서 반복 가능한 읽기](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)를 참조하세요.

## <a name="performance-and-tuning"></a>성능 및 튜닝
참조 [복사 활동 성능 및 조정 가이드](data-factory-copy-activity-performance.md) toolearn 키에 대 한 Azure 데이터 팩터리 및 다양 한 방법으로 toooptimize에서 데이터 이동 (복사 작업)의 성능에 영향을 해당 놓은 것입니다.

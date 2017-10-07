---
title: "ODBC 데이터 저장소에서 데이터 aaaMove | Microsoft Docs"
description: "Azure 데이터 팩터리를 사용 하 여 toomove 데이터를 ODBC 데이터에서에서을 저장 하는 방법을 알아봅니다."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: ad70a598-c031-4339-a883-c6125403cb76
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: jingwang
ms.openlocfilehash: bf96e71da449313b6144bb194205c572d2ca2030
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-odbc-data-stores-using-azure-data-factory"></a>Azure 데이터 팩터리를 사용하여 ODBC 데이터 저장소에서 데이터 이동
이 문서에서는 toouse hello 복사 작업에서는 온-프레미스 ODBC 데이터 Azure Data Factory toomove 데이터에 저장 하는 방법에 대해 설명 합니다. Hello에 기반 [데이터 이동 작업](data-factory-data-movement-activities.md) hello 복사 작업으로 데이터 이동에 대 한 일반적인 개요를 제공 하는 문서입니다.

ODBC 데이터 저장소 지원 tooany 싱크 데이터 저장소에서 데이터를 복사할 수 있습니다. 데이터 목록에 대 한 지원 저장소 hello 복사 작업에서 싱크 참조 hello [데이터 저장소를 지원](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 테이블입니다. 데이터 팩터리는 현재 tooother 데이터 저장소를 저장 하는 데이터를 ODBC 데이터에서에서 이동 뿐만 아니라 다른 데이터 저장소 tooan ODBC 데이터 저장소에서 데이터 이동에 대해 지원 합니다. 

## <a name="enabling-connectivity"></a>연결 사용
데이터 팩터리 서비스는 hello 데이터 관리 게이트웨이 사용 하 여 연결 tooon 온-프레미스 ODBC 원본을 지원 합니다. 참조 [온-프레미스 위치와 클라우드 간의 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 데이터 관리 게이트웨이 및 hello 게이트웨이 설정에 대 한 단계별 지침에 대 한 문서 toolearn 합니다. Azure IaaS VM에서 호스팅되는 경우에 hello 게이트웨이 tooconnect tooan ODBC 데이터 저장소를 사용 합니다.

Hello 동일한 온-프레미스 컴퓨터 또는 hello hello ODBC 데이터 저장소로 Azure VM에 hello 게이트웨이 설치할 수 있습니다. 하지만 별도 컴퓨터/Azure IaaS VM에 hello 게이트웨이 설치 하는 권장 tooavoid 리소스 경합 및 성능 향상을 위해 합니다. 별도 컴퓨터에 hello 게이트웨이 설치할 때 hello 컴퓨터 hello ODBC 데이터 저장소를 사용 하 여 수 tooaccess hello 컴퓨터 여야 합니다.

데이터 관리 게이트웨이 hello와는 별도로 hello 데이터 저장소 hello 게이트웨이 컴퓨터에 대 한 tooinstall hello ODBC 드라이버를 필요 합니다.

> [!NOTE]
> 연결/게이트웨이 관련 문제 해결에 대한 팁은 [게이트웨이 문제 해결](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) 을 참조하세요.

## <a name="getting-started"></a>시작
다른 도구/API를 사용하여 ODBC 데이터 저장소의 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다.

hello 가장 쉬운 방법은 toocreate 파이프라인은 toouse hello **복사 마법사**합니다. 참조 [자습서: 복사 마법사를 사용 하 여 파이프라인을 만들고](data-factory-copy-data-wizard-tutorial.md) 간략 한 설명이 hello 복사 데이터 마법사를 사용 하 여 파이프라인을 만드는 방법에 대 한 합니다.

다음 도구 toocreate 파이프라인 hello을 사용할 수 있습니다: **Azure 포털**, **Visual Studio**, **Azure PowerShell**, **Azure 리소스 관리자 템플릿** , **.NET API**, 및 **REST API**합니다. 참조 [복사 활동 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 단계별 지침 toocreate 복사 작업으로 파이프라인에 대 한 합니다. 

Hello 도구 또는 Api를 사용 하는지 여부를 hello tooa 싱크 데이터 저장소를 저장 하는 원본 데이터에서 데이터를 이동 하는 파이프라인 단계 toocreate 다음을 수행 합니다. 

1. 만들 **연결 된 서비스** toolink 입력 및 출력 데이터 저장소 tooyour 데이터 팩터리입니다.
2. 만들 **데이터 집합** 입력 및 출력 toorepresent hello에 대 한 데이터 복사 작업을 합니다. 
3. 입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다. 

Hello 마법사를 사용 하 여 이러한 데이터 팩터리 엔터티 (연결 된 서비스, 데이터 집합 및 hello 파이프라인)에 대 한 JSON 정의를 자동으로 만들어집니다. 도구/Api (제외.NET API)를 사용 하면 hello JSON 형식을 사용 하 여이 Data Factory 엔터티를 정의 합니다.  Data Factory 된 엔터티를 ODBC 데이터 저장소에서 사용 되는 toocopy 데이터에 대 한 JSON 정의 된 샘플을 보려면 [JSON의 예: tooAzure Blob을 저장 하는 ODBC 데이터에서 데이터 복사](#json-example-copy-data-from-odbc-data-store-to-azure-blob) 이 문서의 섹션. 

다음 섹션 hello JSON 속성을 사용 하는 toodefine Data Factory 엔터티에 특정 tooODBC 데이터 저장소에 대 한 세부 정보를 제공 합니다.

## <a name="linked-service-properties"></a>연결된 서비스 속성
다음 표에서 hello JSON 요소 특정 tooODBC 연결 된 서비스에 대 한 설명을 제공 합니다.

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| type |hello type 속성 설정 해야 합니다: **OnPremisesOdbc** |예 |
| connectionString |hello 연결 문자열 및 선택적의 hello이 아닌 액세스 자격 증명 일부분 자격 증명을 암호화 합니다. Hello 다음 섹션의에서 예를 참조 합니다. |예 |
| 자격 증명 |hello 액세스 자격 증명 드라이버 관련 속성 값 형식으로 지정 하는 hello 연결 문자열의 부분입니다. 예: “Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”. |아니요 |
| authenticationType |Tooconnect toohello ODBC 데이터 저장소를 사용 하는 인증 유형입니다. 가능한 값은 익명 및 기본입니다. |예 |
| username |기본 인증을 사용하는 경우 사용자 이름을 지정합니다. |아니요 |
| 암호 |Hello 사용자 이름에 대해 지정한 사용자 계정에 hello에 대 한 암호를 지정 합니다. |아니요 |
| gatewayName |데이터 팩터리 서비스 hello hello 게이트웨이의 이름 tooconnect toohello ODBC 데이터 저장소를 사용 해야 합니다. |예 |

### <a name="using-basic-authentication"></a>기본 인증 사용

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```
### <a name="using-basic-authentication-with-encrypted-credentials"></a>암호화된 자격 증명으로 기본 인증 사용
Hello를 사용 하 여 hello 자격 증명을 암호화할 수 [새로 AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (1.0 버전의 Azure PowerShell) cmdlet 또는 [New-azuredatafactoryencryptvalue](https://msdn.microsoft.com/library/dn834940.aspx) (0.9 또는 이전 버전의 hello Azure PowerShell)입니다.  

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=myserver.database.windows.net; Database=TestDatabase;;EncryptedCredential=eyJDb25uZWN0...........................",
            "gatewayName": "mygateway"
        }
    }
}
```

### <a name="using-anonymous-authentication"></a>익명 인증 사용

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "connectionString": "Driver={SQL Server};Server={servername}.database.windows.net; Database=TestDatabase;",
            "credential": "UID={uid};PWD={pwd}",
            "gatewayName": "mygateway"
        }
    }
}
```


## <a name="dataset-properties"></a>데이터 집합 속성
섹션 및 데이터 집합 정의에 사용 가능한 속성의 전체 목록을 보려면 hello [데이터 집합을 만드는](data-factory-create-datasets.md) 문서. 구조, 가용성 및 JSON 데이터 집합의 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다(Azure SQL, Azure blob, Azure 테이블 등).

hello **typeProperties** 데이터 집합의 각 형식에 대 한 다른 섹션과 hello 데이터 저장소에 hello 데이터의 hello 위치에 대 한 정보를 제공 합니다. 형식의 데이터 집합에 대 한 hello typeProperties 섹션 **RelationalTable** hello 다음과 같은 속성에 (ODBC 데이터 집합 포함)

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| tableName |Hello ODBC 데이터 저장소의 hello 테이블의 이름입니다. |예 |

## <a name="copy-activity-properties"></a>복사 작업 속성
섹션 및 활동 정의에 사용 가능한 속성의 전체 목록을 참조 hello [파이프라인 만들기](data-factory-create-pipelines.md) 문서. 이름, 설명, 입력/출력 테이블, 정책 등의 속성은 모든 형식의 활동에 사용할 수 있습니다.

Hello에 사용할 수 있는 속성 **typeProperties** 섹션 hello에 hello 활동의 다른 손 활동 형식에 따라 다릅니다. 복사 작업은 원본 및 싱크의 hello 형식에 따라 변경합니다.

복사 작업에서는 원본 유형인 경우 **RelationalSource** (ODBC 포함), 다음과 같은 속성 hello typeProperties 섹션에서 사용할 수 있는:

| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| 쿼리 |사용자 지정 쿼리 tooread 데이터 hello를 사용 합니다. |SQL 쿼리 문자열. 예: select * from MyTable. |예 |


## <a name="json-example-copy-data-from-odbc-data-store-tooazure-blob"></a>JSON의 예: tooAzure Blob을 저장 하는 ODBC 데이터에서 데이터 복사
이 예에서는 JSON 정의 제공 합니다. 사용 하 여 toocreate 파이프라인을 사용할 수 있는 [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md) 또는 [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 또는 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)합니다. ODBC에서 toocopy 데이터 tooan Azure Blob 저장소를 원본 하는 방법을 보여 줍니다. 그러나 데이터는 복사 tooany 명시 된 hello 싱크 가능 [여기](data-factory-data-movement-activities.md#supported-data-stores-and-formats) Azure Data Factory에서 복사 작업 hello를 사용 하 여 합니다.

hello 샘플 hello 데이터 팩터리 엔터티 뒤에 있습니다.

1. [OnPremisesOdbc](#linked-service-properties) 형식의 연결된 서비스입니다.
2. [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) 형식의 연결된 서비스
3. [RelationalTable](#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)
4. [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)
5. [RelationalSource](#copy-activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)

hello 샘플 데이터 복사는 ODBC 데이터 저장소 tooa blob에 쿼리 결과에서 1 시간 마다 합니다. 이 예제에 사용 되는 hello JSON 속성 hello 샘플 다음 섹션에 설명 되어 있습니다.

첫 번째 단계로 hello 데이터 관리 게이트웨이를 설정 합니다. hello 지침은 hello [온-프레미스 위치와 클라우드 간의 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서.

**ODBC 연결 된 서비스** 이 예제를 사용 하 여 hello 기본 인증. 사용할 수 있는 다른 유형의 인증은 [ODBC 연결된 서비스](#linked-service-properties) 섹션을 참조하세요.

```json
{
    "name": "OnPremOdbcLinkedService",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```

**Azure 저장소 연결된 서비스**

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

**ODBC 입력 데이터 집합**

hello 샘플 가정 ODBC 데이터베이스에 "MyTable" 테이블을 만든 시계열 데이터에 대 한 "timestampcolumn" 라는 열을 포함 합니다.

설정 "외부": "true" 알리고 hello 데이터 팩터리 서비스 hello 데이터 집합의 데이터 팩터리 외부 toohello hello data factory에는 활동에 의해 생성 되지 않습니다.

```json
{
    "name": "ODBCDataSet",
    "properties": {
        "published": false,
        "type": "RelationalTable",
        "linkedServiceName": "OnPremOdbcLinkedService",
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

데이터가 새 blob tooa 1 시간 마다 기록 됩니다 (빈도: 시, 간격: 1). hello blob에 대 한 hello 폴더 경로 처리 중인 hello 조각의 hello 시작 시간에 따라 동적으로 평가 됩니다. hello 폴더 경로 hello 시작 시간의 연도, 월, 일 및 시간 부분을 사용 합니다.

```json
{
    "name": "AzureBlobOdbcDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/odbc/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


**ODBC 원본(RelationalSource) 및 Blob 싱크 (BlobSink)를 사용하는 파이프라인의 복사 작업**

복사 작업을 포함 하는 hello 파이프라인 구성된 toouse 이러한 입력 및 출력 데이터 집합은 하 고 예약 된 toorun 1 시간입니다. Hello 파이프라인 JSON 정의에서 hello **소스** 형식이 너무 설정**RelationalSource** 및 **싱크** 형식이 너무 설정**BlobSink**합니다. hello에 대 한 지정 된 hello SQL 쿼리 **쿼리** 속성 시간 toocopy 지난 hello에 hello 데이터를 선택 합니다.

```json
{
    "name": "CopyODBCToBlob",
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
                        "name": "OdbcDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOdbcDataSet"
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
                "name": "OdbcToBlob"
            }
        ],
        "start": "2016-06-01T18:00:00Z",
        "end": "2016-06-01T19:00:00Z"
    }
}
```
### <a name="type-mapping-for-odbc"></a>ODBC에 대한 형식 매핑
Hello에 설명 된 대로 [데이터 이동 작업](data-factory-data-movement-activities.md) 문서, 복사 작업 소스 형식 toosink 형식에서 자동 형식 변환 2 단계 방식을 따릅니다 hello로 수행:

1. 네이티브 소스 형식 too.NET 형식에서 변환
2. .NET 형식 toonative 싱크 형식에서 변환

Hello에 설명 된 대로 ODBC 데이터 형식은 매핑된 too.NET 형식 ODBC 데이터 저장소에서 데이터를 이동할 때는 [ODBC 데이터 형식 매핑](https://msdn.microsoft.com/library/cc668763.aspx) 항목입니다.

## <a name="map-source-toosink-columns"></a>원본 toosink 열 매핑
원본 데이터 집합 toocolumns 싱크 데이터 집합에서의 열을 매핑하는 방법에 대 한 toolearn 참조 [Azure Data Factory에서 데이터 집합 열에 매핑](data-factory-map-columns.md)합니다.

## <a name="repeatable-read-from-relational-sources"></a>관계형 원본에서 반복 가능한 읽기
관계형 데이터 저장소에서 데이터를 복사할 때 유의 tooavoid에서 반복성을 유지 의도 하지 않은 결과입니다. Azure Data Factory에서는 조각을 수동으로 다시 실행할 수 있습니다. 또한 오류가 발생하면 조각을 다시 실행하도록 데이터 집합에 대한 재시도 정책을 구성할 수 있습니다. Toomake 동일한 데이터를 hello 있는지 어떻게에 관계 없이 읽기 필요한 어느 쪽에 분할 영역을 다시 실행 하는 경우 조각에 여러 번 실행 됩니다. [관계형 원본에서 반복 가능한 읽기](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)를 참조하세요.

## <a name="ge-historian-store"></a>GE Historian 저장소
ODBC 연결 된 서비스 toolink 만들면는 [GE Proficy 사 학자 (이제 GE 사 학자)](http://www.geautomation.com/products/proficy-historian) hello 다음 예제와 같이 저장소 tooan Azure 데이터 팩터리에 데이터:

```json
{
    "name": "HistorianLinkedService",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "connectionString": "DSN=<name of hello GE Historian store>",
            "gatewayName": "<gateway name>",
            "authenticationType": "Basic",
            "userName": "<user name>",
            "password": "<password>"
        }
    }
}
```

온-프레미스 컴퓨터에 데이터 관리 게이트웨이 설치 하 고 hello 포털과 hello 게이트웨이 등록 합니다. 온-프레미스 컴퓨터에 설치 하는 hello 게이트웨이 GE 사 학자 tooconnect toohello GE 사 학자 데이터 저장소에 대 한 hello ODBC 드라이버를 사용 합니다. 그러므로 hello 게이트웨이 컴퓨터에 아직 설치 되지 않은 경우에 hello 드라이버를 설치 합니다. 자세한 내용은 [연결 사용](#enabling-connectivity) 섹션을 참조하세요.

데이터 팩터리 솔루션에서 GE 사 학자를 저장 하는 hello를 사용 하기 전에 hello 게이트웨이 hello 다음 섹션의 지침을 사용 하 여 toohello 데이터 저장소에 연결할 수 있는지 여부를 확인 합니다.

ODBC 데이터를 사용 하 여 자세한 개요는 hello부터에서 hello 문서 읽기 복사 작업에서 원본 데이터 저장소로 저장 합니다.  

## <a name="troubleshoot-connectivity-issues"></a>연결 문제 해결
tootroubleshoot 연결 문제를 사용 하 여 hello **진단** 탭 **데이터 관리 게이트웨이 구성 관리자**합니다.

1. **데이터 관리 게이트웨이 구성 관리자**를 시작합니다. 에 대 한 "C:\Program Files\Microsoft 데이터 관리 Gateway\1.0\Shared\ConfigManager.exe" 직접 (또는) 검색을 실행 하거나 **게이트웨이** toofind 링크 너무**Microsoft 데이터 관리 게이트웨이** 다음 이미지는 hello와 같이 응용 프로그램입니다.

    ![게이트웨이 검색](./media/data-factory-odbc-connector/search-gateway.png)
2. Toohello 전환 **진단** 탭 합니다.

    ![게이트웨이 진단](./media/data-factory-odbc-connector/data-factory-gateway-diagnostics.png)
3. 선택 hello **형식** 데이터 (연결 된 서비스)를 저장 합니다.
4. 지정 **인증** 입력 **자격 증명** (또는) 입력 **연결 문자열** 사용 되는 tooconnect toohello 데이터 저장소입니다.
5. 클릭 **연결 테스트** tootest hello 연결 toohello 데이터 저장소입니다.

## <a name="performance-and-tuning"></a>성능 및 튜닝
참조 [복사 활동 성능 및 조정 가이드](data-factory-copy-activity-performance.md) toolearn 키에 대 한 Azure 데이터 팩터리 및 다양 한 방법으로 toooptimize에서 데이터 이동 (복사 작업)의 성능에 영향을 해당 놓은 것입니다.

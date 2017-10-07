---
title: "데이터 팩터리를 사용 하 여 Oracle에서 데이터를 aaaCopy | Microsoft Docs"
description: "어떻게 toocopy 있는 Oracle 데이터베이스에서 온-프레미스 데이터 Azure 데이터 팩터리를 사용 하 여에 대해 알아봅니다."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 3c20aa95-a8a1-4aae-9180-a6a16d64a109
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: adb6d5fbe38e18791616ac77e8179970bbea37fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tofrom-on-premises-oracle-using-azure-data-factory"></a>Azure Data Factory를 사용하여 온-프레미스 Oracle 간 데이터 복사
이 문서에서는 toouse 온-프레미스 Oracle 데이터베이스에서 Azure Data Factory toomove 데이터에서 복사 작업을 hello 하는 방법을 설명 합니다. Hello에 기반 [데이터 이동 작업](data-factory-data-movement-activities.md) hello 복사 작업으로 데이터 이동에 대 한 일반적인 개요를 제공 하는 문서입니다.

## <a name="supported-scenarios"></a>지원되는 시나리오
데이터를 복사할 수 **Oracle 데이터베이스에서** toohello 데이터 저장소를 다음:

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

Hello 다음 데이터 저장소에서에서 데이터를 복사할 수 **tooan Oracle 데이터베이스**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="prerequisites"></a>필수 조건
데이터 팩터리 hello 데이터 관리 게이트웨이 사용 하 여 연결 tooon 온-프레미스 Oracle 원본을 지원 합니다. 참조 [데이터 관리 게이트웨이](data-factory-data-management-gateway.md) 데이터 관리 게이트웨이에 대 한 문서 toolearn 및 [toocloud 온-프레미스에서에서 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서에 대 한 단계별 지침은 hello 게이트웨이 데이터 파이프라인 설정 toomove 데이터입니다.

게이트웨이 hello Oracle에서에서 호스팅되는 Azure IaaS VM 하는 경우에 필요 합니다. Hello IaaS VM hello 데이터로 저장 같거나 hello 게이트웨이 다른 VM toohello 데이터베이스 연결 될 수 있습니다에 hello 게이트웨이 설치할 수 있습니다.

> [!NOTE]
> 연결/게이트웨이 관련 문제 해결에 대한 팁은 [게이트웨이 문제 해결](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) 을 참조하세요.

## <a name="supported-versions-and-installation"></a>지원되는 버전 및 설치
이 Oracle 커넥터는 다음 두 가지 버전의 드라이버를 지원합니다.

- **Oracle (권장)에 대 한 Microsoft 드라이버**: 부터는 데이터 관리 게이트웨이 버전 2.7에서 Microsoft 드라이버 Oracle는 hello 게이트웨이 함께 자동으로 설치 됩니다. 따라서 필요 하지 않습니다 순서로 tooadditionally 핸들 hello 드라이버 tooestablish 연결 tooOracle 하 고이 드라이버를 사용 하 여 더 나은 복사 성능을 발생할 수도 있습니다. 아래 Oracle 데이터베이스 버전이 지원됩니다.
    - Oracle 12c R1(12.1)
    - Oracle 11g R1, R2(11.1, 11.2)
    - Oracle 10g R1, R2(10.1, 10.2)
    - Oracle 9i R1, R2(9.0.1, 9.2)
    - Oracle 8i R3(8.1.7)

> [!IMPORTANT]
> 현재 Microsoft driver for Oracle tooOracle를 작성 하지 않고 Oracle에서 데이터를 복사만 지원 합니다. 및 데이터 관리 게이트웨이 진단 탭에서 hello 테스트 연결 기능에서는이 드라이버를 지원 하지 않습니다. 또는 hello 복사 마법사 toovalidate hello 연결을 사용할 수 있습니다.
>

- **Oracle Data Provider for.NET:** toouse Oracle 데이터 공급자 toocopy 데이터를 선택할 수도 있습니다 / tooOracle 합니다. 이 구성 요소는 [Windows용 Oracle Data Access Components](http://www.oracle.com/technetwork/topics/dotnet/downloads/)에 포함됩니다. Hello 게이트웨이가 설치 된 hello 컴퓨터에 hello 적절 한 버전 (32/64 비트)를 설치 합니다. [Oracle 데이터 공급자.NET 12.1](http://docs.oracle.com/database/121/ODPNT/InstallSystemRequirements.htm#ODPNT149) tooOracle 데이터베이스 10g 릴리스 2 이상에 액세스할 수 있습니다.

    "XCopy 설치"를 선택한 경우 hello readme.htm의 단계를 수행 합니다. UI (비-XCopy 하나)가 포함 된 hello 설치 관리자를 선택 하는 것이 좋습니다.

    Hello 공급자를 설치한 후 **다시 시작** hello 서비스 애플릿을 (또는) 데이터 관리 게이트웨이 구성 관리자를 사용 하 여 컴퓨터에서 데이터 관리 게이트웨이 호스트 서비스입니다.  

복사 마법사 tooauthor hello 복사본 파이프라인을 사용 하는 경우 hello 드라이버 종류 자동 결정 됩니다. 게이트웨이 버전이 2.7보다 낮거나 싱크로 Oracle을 선택한 경우가 아니면 기본적으로 Microsoft 드라이버가 사용됩니다.

## <a name="getting-started"></a>시작
다른 도구/API를 사용하여 온-프레미스 Oracle 데이터베이스 간에 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다.

hello 가장 쉬운 방법은 toocreate 파이프라인은 toouse hello **복사 마법사**합니다. 참조 [자습서: 복사 마법사를 사용 하 여 파이프라인을 만들고](data-factory-copy-data-wizard-tutorial.md) 간략 한 설명이 hello 복사 데이터 마법사를 사용 하 여 파이프라인을 만드는 방법에 대 한 합니다.

다음 도구 toocreate 파이프라인 hello을 사용할 수 있습니다: **Azure 포털**, **Visual Studio**, **Azure PowerShell**, **Azure 리소스 관리자 템플릿** , **.NET API**, 및 **REST API**합니다. 참조 [복사 활동 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 단계별 지침 toocreate 복사 작업으로 파이프라인에 대 한 합니다.

Hello 도구 또는 Api를 사용 하는지 여부를 hello tooa 싱크 데이터 저장소를 저장 하는 원본 데이터에서 데이터를 이동 하는 파이프라인 단계 toocreate 다음을 수행 합니다.

1. **데이터 팩터리**를 만듭니다. 데이터 팩터리에는 하나 이상의 파이프라인이 포함될 수 있습니다. 
2. 만들 **연결 된 서비스** toolink 입력 및 출력 데이터 저장소 tooyour 데이터 팩터리입니다. 예를 들어 Oralce 데이터베이스 tooan Azure blob 저장소에서에서 데이터를 복사 하는 경우 만들면 두 개의 연결 된 서비스 toolink Oracle 데이터베이스와 Azure 저장소 계정 tooyour 데이터 팩터리입니다. 특정 tooOracle 있는 연결 된 서비스 속성을 참조 하십시오. [연결 된 서비스 속성](#linked-service-properties) 섹션.
3. 만들 **데이터 집합** 입력 및 출력 toorepresent hello에 대 한 데이터 복사 작업을 합니다. 예에서 hello hello 마지막 단계에서 언급 한 hello 입력된 데이터를 포함 하 여 Oracle 데이터베이스에서 데이터 집합 toospecify hello 테이블을 만듭니다. And, 다른 데이터 집합 toospecify hello blob 컨테이너 만들기 및 Oracle 데이터베이스 hello에서 복사 된 hello 데이터를 보유 하는 hello 폴더입니다. 참조 데이터 집합 속성을 특정 tooOracle [데이터 집합 속성](#dataset-properties) 섹션.
4. 입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다. 앞에서 언급 한 hello 예제를 사용 하 여 OracleSource 소스 및 BlobSink로는 싱크도 hello 복사 작업에 대 한. 마찬가지로, Azure Blob 저장소 tooOracle 데이터베이스에서에서 복사 하는 경우 BlobSource 및 사용 OracleSink hello 복사 활동에서. 복사 활동 속성을 특정 tooOracle 데이터베이스를 참조 하십시오. [활동 속성을 복사](#copy-activity-properties) 섹션. 에 대 한 내용은 toouse 데이터 저장 되는 방식과 원본 또는 싱크도, 데이터 저장소에 대 한 hello 이전 단원의 hello 링크를 클릭 합니다. 

Hello 마법사를 사용 하 여 이러한 데이터 팩터리 엔터티 (연결 된 서비스, 데이터 집합 및 hello 파이프라인)에 대 한 JSON 정의를 자동으로 만들어집니다. 도구/Api (제외.NET API)를 사용 하면 hello JSON 형식을 사용 하 여이 Data Factory 엔터티를 정의 합니다.  샘플 은/온-프레미스 Oracle 데이터베이스에서 사용 되는 toocopy 데이터를 Data Factory 엔터티에 대 한 JSON 정의 가진 [JSON 예제](#json-examples-for-copying-data-to-and-from-oracle-database) 이 문서의 섹션.

사용 되는 toodefine Data Factory 엔터티에 JSON 속성에 대 한 세부 정보를 제공 하는 다음 섹션 hello:

## <a name="linked-service-properties"></a>연결된 서비스 속성
다음 표에서 hello JSON 요소 특정 tooOracle 연결 된 서비스에 대 한 설명을 제공 합니다.

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| type |hello type 속성 설정 해야 합니다: **OnPremisesOracle** |예 |
| driverType | 드라이버 toouse toocopy 데이터 지정 / tooOracle 데이터베이스입니다. 허용되는 값은 **Microsoft** 또는 **ODP**(기본값)입니다. 드라이버 세부 정보에 대해서는 [지원되는 버전 및 설치](#supported-versions-and-installation) 섹션을 참조하세요. | 아니요 |
| connectionString | Hello connectionString 속성에 대 한 tooconnect toohello Oracle 데이터베이스 인스턴스는 데 필요한 정보를 지정 합니다. | 예 |
| gatewayName | 사용 하는 tooconnect toohello 온-프레미스 Oracle 서버 hello 게이트웨이의 이름 |예 |

**예제: Microsoft 드라이버 사용:**
```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "driverType": "Microsoft",
            "connectionString":"Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

**예제: ODP 드라이버 사용**

너무 참조[이 사이트](https://www.connectionstrings.com/oracle-data-provider-for-net-odp-net/) hello 허용 된 형식에 대 한 합니다.

```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "connectionString": "Data Source=(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=<hostname>)(PORT=<port number>))(CONNECT_DATA=(SERVICE_NAME=<SID>)));
User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

## <a name="dataset-properties"></a>데이터 집합 속성
섹션 및 데이터 집합 정의에 사용 가능한 속성의 전체 목록을 보려면 hello [데이터 집합을 만드는](data-factory-create-datasets.md) 문서. 구조, 가용성 및 JSON 데이터 집합의 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다(Oracle, Azure blob, Azure 테이블 등).

hello typeProperties 섹션 hello 데이터 저장소에 hello 데이터의 hello 위치에 대 한 정보를 제공 및 데이터 집합의 각 유형에 대해과 다릅니다. OracleTable 형식의 hello 데이터 집합에 대 한 hello typeProperties 섹션에는 다음과 같은 속성 hello에 있습니다.

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| tableName |Oracle 데이터베이스를 연결 된 서비스 hello hello에 hello 테이블의 이름은 참조 합니다. |아니요(**OracleSource**의 **oracleReaderQuery**가 지정된 경우) |

## <a name="copy-activity-properties"></a>복사 작업 속성
섹션 및 활동 정의에 사용 가능한 속성의 전체 목록을 참조 hello [파이프라인 만들기](data-factory-create-pipelines.md) 문서. 이름, 설명, 입력/출력 테이블, 정책 등의 속성은 모든 형식의 활동에 사용할 수 있습니다.

> [!NOTE]
> 복사 활동 hello 하나의 입력을 하나의 출력을 생성 합니다.

반면 hello 활동의 hello typeProperties 섹션에서 사용할 수 있는 속성에 각 활동 유형에 따라 다릅니다. 복사 작업은 원본 및 싱크의 hello 형식에 따라 변경합니다.

### <a name="oraclesource"></a>oracleReaderQuery
Hello 원본 유형인 경우 복사 활동에서 **OracleSource** hello 다음과 같은 속성에서 사용할 수 있는 **typeProperties** 섹션:

| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| oracleReaderQuery |사용자 지정 쿼리 tooread 데이터 hello를 사용 합니다. |SQL 쿼리 문자열. 예: select * from MyTable <br/><br/>지정 하지 않으면 실행 되는 SQL 문을 hello: 선택 * from MyTable |아니요(**데이터 집합**의 **tableName**이 지정된 경우) |

### <a name="oraclesink"></a>파이프라인
**OracleSink** hello 다음과 같은 속성을 지원 합니다.

| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| writeBatchTimeout |대기 시간이 초과 되기 전에 일괄 처리 삽입 작업 toocomplete hello에 대 한 시간입니다. |timespan<br/><br/> 예: “00:30:00”(30분). |아니요 |
| writeBatchSize |WriteBatchSize hello 버퍼 크기에 이르면 hello SQL 테이블에 데이터를 삽입 합니다. |정수(행 수) |아니요(기본값: 100) |
| sqlWriterCleanupScript |특정 조각의 데이터 정리 되도록 tooexecute 복사 작업에 대 한 쿼리를 지정 합니다. |쿼리 문입니다. |아니요 |
| sliceIdentifierColumnName |특정 조각 다시 실행 시점의 데이터를 사용 하는 tooclean 변수인 자동 생성 된 조각 식별자를 가진 toofill 복사 작업에 대 한 열 이름을 지정 합니다. |이진(32) 데이터 형식이 있는 열의 열 이름입니다. |아니요 |

## <a name="json-examples-for-copying-data-tooand-from-oracle-database"></a>Oracle 데이터베이스에서 데이터 tooand 복사 하기 위한 JSON 예제
hello 다음 예에서는 샘플 JSON 정의 사용 하 여 toocreate 파이프라인을 사용할 수 있는 [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md) 또는 [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 또는 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)합니다. 보여 줍니다 어떻게 toocopy 데이터로 / 하/Azure Blob 저장소에서 tooan Oracle 데이터베이스입니다. 그러나 데이터는 복사 tooany 명시 된 hello 싱크 가능 [여기](data-factory-data-movement-activities.md#supported-data-stores-and-formats) Azure Data Factory에서 복사 작업 hello를 사용 하 여 합니다.   

## <a name="example-copy-data-from-oracle-tooazure-blob"></a>예: Oracle tooAzure Blob에서에서 데이터를 복사 합니다.

hello 샘플 hello 데이터 팩터리 엔터티 뒤에 있습니다.

1. [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties)형식의 연결된 서비스
2. [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)형식의 연결된 서비스
3. [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)
4. [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)
5. [OracleSource](data-factory-onprem-oracle-connector.md#copy-activity-properties)를 소스로, [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)를 싱크로 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)

hello 샘플에 1 시간 마다는 온-프레미스 Oracle 데이터베이스 tooa blob의 테이블에서 데이터 복사합니다. Hello 샘플에 사용 되는 다양 한 속성에 대 한 자세한 내용은 hello 샘플 다음 섹션의 설명서를 참조 합니다.

**Oracle 연결된 서비스:**

```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "driverType": "Microsoft",
            "connectionString":"Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

**Azure Blob 저장소 연결된 서비스:**

```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<Account key>"
        }
    }
}
```

**Oracle 입력 데이터 집합:**

hello 샘플 테이블 "MyTable"에서 만든 Oracle 가정 시계열 데이터에 대 한 "timestampcolumn" 라는 열을 포함 합니다.

설정 "외부": "true" 알리고 hello 데이터 팩터리 서비스 hello 데이터 집합의 데이터 팩터리 외부 toohello hello data factory에는 활동에 의해 생성 되지 않습니다.

```json
{
    "name": "OracleInput",
    "properties": {
        "type": "OracleTable",
        "linkedServiceName": "OnPremisesOracleLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "offset": "01:00:00",
            "interval": "1",
            "anchorDateTime": "2014-02-27T12:00:00",
            "frequency": "Hour"
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

데이터가 새 blob tooa 1 시간 마다 기록 됩니다 (빈도: 시, 간격: 1). hello 폴더 경로 파일 이름은 hello blob에 대 한 처리 중인 hello 조각의 hello 시작 시간에 따라 동적으로 평가 됩니다. hello 폴더 경로 hello 시작 시간의 연도, 월, 일 및 시간 부분을 사용 합니다.

```json
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

**복사 작업을 포함하는 파이프라인:**

hello 파이프라인에 포함 된 구성된 toouse 않은 복사 작업은 예약 된 toorun 매 및 hello 입력 및 출력 데이터 집합. Hello 파이프라인 JSON 정의에서 hello **소스** 형식이 너무 설정**OracleSource** 및 **싱크** 형식이 너무 설정**BlobSink**합니다.  지정 된 hello SQL 쿼리 **oracleReaderQuery** 속성 시간 toocopy 지난 hello에 hello 데이터를 선택 합니다.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
            {
                "name": "OracletoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                    {
                        "name": " OracleInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "typeProperties": {
                    "source": {
                        "type": "OracleSource",
                        "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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

## <a name="example-copy-data-from-azure-blob-toooracle"></a>예: Azure Blob tooOracle에서 데이터를 복사 합니다.
이 샘플에서는 어떻게 toocopy 데이터를 Azure Blob 저장소 tooan 온-프레미스 Oracle 데이터베이스를 보여 줍니다. 그러나 데이터를 복사할 수 있습니다 **직접** 명시 된 hello 소스 중 하나에서 [여기](data-factory-data-movement-activities.md#supported-data-stores-and-formats) Azure Data Factory에서 복사 작업 hello를 사용 하 여 합니다.  

hello 샘플 hello 데이터 팩터리 엔터티 뒤에 있습니다.

1. [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties)형식의 연결된 서비스
2. [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)형식의 연결된 서비스
3. [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)입니다.
4. [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md).
5. [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties)를 소스로, [OracleSink](data-factory-onprem-oracle-connector.md#copy-activity-properties)를 싱크로 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)입니다.

hello 샘플 데이터 복사 온-프레미스 Oracle 데이터베이스에 있는 blob tooa 테이블에서 1 시간 마다 합니다. Hello 샘플에 사용 되는 다양 한 속성에 대 한 자세한 내용은 hello 샘플 다음 섹션의 설명서를 참조 합니다.

**Oracle 연결된 서비스:**
```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "connectionString": "Data Source=(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=<hostname>)(PORT=<port number>))(CONNECT_DATA=(SERVICE_NAME=<SID>)));
            User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

**Azure Blob 저장소 연결된 서비스:**
```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<Account key>"
        }
    }
}
```

**Azure Blob 입력 데이터 집합**

데이터는 매시간 새 blob에 선택됩니다(frequency: hour, interval: 1). hello 폴더 경로 파일 이름은 hello blob에 대 한 처리 중인 hello 조각의 hello 시작 시간에 따라 동적으로 평가 됩니다. 연도, 월 및 일 부분은 hello 시작 시간의 hello 폴더 경로 사용 하 고 파일 이름을 hello 시작 시간의 시간 부분을 hello를 사용 합니다. "external": "true" 설정을 hello 데이터 팩터리 서비스에 알리고이 테이블 데이터 팩터리 외부 toohello hello data factory에는 활동에 의해 생성 되지 않습니다.

```json
{
    "name": "AzureBlobInput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
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
            "frequency": "Day",
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

**Oracle 출력 데이터 집합:**

hello 샘플 Oracle에 "MyTable" 테이블을 만들었다고 가정 합니다. 사용 하 여 Oracle에 hello 테이블을 만들려면 hello Blob CSV 파일 toocontain 예상 대로 동일한 수의 열을 hello 합니다. 새 행 1 시간 마다 toohello 테이블을 추가 됩니다.

```json
{
    "name": "OracleOutput",
    "properties": {
        "type": "OracleTable",
        "linkedServiceName": "OnPremisesOracleLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "availability": {
            "frequency": "Day",
            "interval": "1"
        }
    }
}
```

**복사 작업을 포함하는 파이프라인:**

hello 파이프라인에 포함 된 구성된 toouse 않은 복사 작업 입력 및 출력 데이터 집합을 hello 및 예약 된 toorun 1 시간입니다. Hello 파이프라인 JSON 정의에서 hello **소스** 형식이 너무 설정**BlobSource** 및 hello **싱크** 형식이 너무 설정**OracleSink**합니다.  

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-05T19:00:00",
        "description":"pipeline with copy activity",
        "activities":[  
            {
                "name": "AzureBlobtoOracle",
                "description": "Copy Activity",
                "type": "Copy",
                "inputs": [
                    {
                        "name": "AzureBlobInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "OracleOutput"
                    }
                ],
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "OracleSink"
                    }
                },
                "scheduler": {
                    "frequency": "Day",
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


## <a name="troubleshooting-tips"></a>문제 해결 팁
### <a name="problem-1-net-framework-data-provider"></a>문제 1: .NET Framework Data Provider

Hello 다음을 참조 **오류 메시지가**:

    Copy activity met invalid parameters: 'UnknownParameterName', Detailed message: Unable toofind hello requested .Net Framework Data Provider. It may not be installed”.  

**가능한 원인:**

1. .NET Framework Data Provider for Oracle hello 설치 되지 않았습니다.
2. .NET Framework Data Provider for Oracle hello 설치 too.NET Framework 2.0 였으며 hello.NET Framework 4.0 폴더에서 찾을 수 없습니다.

**해결 방법**

1. Hello.NET Provider for Oracle 설치 하지 않은 경우 [설치](http://www.oracle.com/technetwork/topics/dotnet/downloads/) hello 시나리오를 다시 시도 하십시오.
2. Hello 공급자를 설치한 후에 hello 오류 메시지를 가져오는 경우 다음 단계 hello지 않습니다.
   1. Hello 폴더에서 컴퓨터 구성의.NET 2.0을 열어: <system disk>: \Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG\machine.config 합니다.
   2. 검색할 **Oracle Data Provider for.NET**, 샘플의 다음 hello에 표시 된 대로 수 toofind 항목 수 있어야 **system.data** -> **DbProviderFactories**: "<add name="Oracle Data Provider for .NET" invariant="Oracle.DataAccess.Client" description="Oracle Data Provider for.NET" type="Oracle.DataAccess.Client.OracleClientFactory, Oracle.DataAccess, Version=2.112.3.0, Culture=neutral, PublicKeyToken=89b483f429c47342" />”이라는 제목의 방법 가이드를 참조하세요.
3. Hello v4.0 폴더를 다음에이 항목 toohello machine.config 파일을 복사: <system disk>: \Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config, 및 hello 버전 too4.xxx.x.x 변경 합니다.
4. "< ODP.NET 설치 경로 > \11.2.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll"를 실행 하 여 hello 전역 어셈블리 캐시 (GAC)에 설치 `gacutil /i [provider path]`. # # 문제 해결 팁

### <a name="problem-2-datetime-formatting"></a>문제 2: 날짜/시간 서식

Hello 다음을 참조 **오류 메시지가**:

    Message=Operation failed in Oracle Database with hello following error: 'ORA-01861: literal does not match format string'.,Source=,''Type=Oracle.DataAccess.Client.OracleException,Message=ORA-01861: literal does not match format string,Source=Oracle Data Provider for .NET,'.

**해결 방법**

Hello 다음과 같이 날짜는 Oracle 데이터베이스에서 구성 하는 방법에 따라 복사 작업에서 tooadjust hello 쿼리 문자열을 할 수 있습니다 (사용 하 여 hello to_date 함수가) 샘플:

    "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= to_date(\\'{0:MM-dd-yyyy HH:mm}\\',\\'MM/DD/YYYY HH24:MI\\')  AND timestampcolumn < to_date(\\'{1:MM-dd-yyyy HH:mm}\\',\\'MM/DD/YYYY HH24:MI\\') ', WindowStart, WindowEnd)"


## <a name="type-mapping-for-oracle"></a>Oracle에 대한 형식 매핑
Hello에 설명 된 대로 [데이터 이동 작업](data-factory-data-movement-activities.md) 문서 복사 작업 단계 2 방식을 따릅니다 hello로 원본 형식 toosink 유형의 자동 형식 변환을 수행 합니다.

1. 네이티브 소스 형식 too.NET 형식에서 변환
2. .NET 형식 toonative 싱크 형식에서 변환

Oracle에서 데이터를 이동할 때는 hello 매핑은 다음 Oracle 데이터 형식 too.NET 형식에서 그 반대의 사용 됩니다.

| Oracle 데이터 형식 | .NET Framework 데이터 형식 |
| --- | --- |
| BFILE |Byte[] |
| BLOB |Byte[] |
| CHAR |문자열 |
| CLOB |문자열 |
| DATE |DateTime |
| FLOAT |Decimal, 문자열(전체 자릿수의 경우 > 28) |
| INTEGER |Decimal, 문자열(전체 자릿수의 경우 > 28) |
| 간격 연도 tooMONTH |Int32 |
| 간격 날짜 tooSECOND |TimeSpan |
| LONG |문자열 |
| LONG RAW |Byte[] |
| NCHAR |문자열 |
| NCLOB |문자열 |
| NUMBER |Decimal, 문자열(전체 자릿수의 경우 > 28) |
| NVARCHAR2 |문자열 |
| RAW |Byte[] |
| ROWID |문자열 |
| TIMESTAMP |DateTime |
| TIMESTAMP WITH LOCAL TIME ZONE |DateTime |
| TIMESTAMP WITH TIME ZONE |DateTime |
| UNSIGNED INTEGER |NUMBER |
| VARCHAR2 |문자열 |
| XML |문자열 |

> [!NOTE]
> 데이터 형식 **간격 연도 tooMONTH** 및 **간격 일 tooSECOND** Microsoft 드라이버를 사용 하는 경우 지원 되지 않습니다.

## <a name="map-source-toosink-columns"></a>원본 toosink 열 매핑
원본 데이터 집합 toocolumns 싱크 데이터 집합에서의 열을 매핑하는 방법에 대 한 toolearn 참조 [Azure Data Factory에서 데이터 집합 열에 매핑](data-factory-map-columns.md)합니다.

## <a name="repeatable-read-from-relational-sources"></a>관계형 원본에서 반복 가능한 읽기
관계형 데이터 저장소에서 데이터를 복사할 때 유의 tooavoid에서 반복성을 유지 의도 하지 않은 결과입니다. Azure Data Factory에서는 조각을 수동으로 다시 실행할 수 있습니다. 또한 오류가 발생하면 조각을 다시 실행하도록 데이터 집합에 대한 재시도 정책을 구성할 수 있습니다. Toomake 동일한 데이터를 hello 있는지 어떻게에 관계 없이 읽기 필요한 어느 쪽에 분할 영역을 다시 실행 하는 경우 조각에 여러 번 실행 됩니다. [관계형 원본에서 반복 가능한 읽기](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)를 참조하세요.

## <a name="performance-and-tuning"></a>성능 및 튜닝
참조 [복사 활동 성능 및 조정 가이드](data-factory-copy-activity-performance.md) toolearn 키에 대 한 Azure 데이터 팩터리 및 다양 한 방법으로 toooptimize에서 데이터 이동 (복사 작업)의 성능에 영향을 해당 놓은 것입니다.

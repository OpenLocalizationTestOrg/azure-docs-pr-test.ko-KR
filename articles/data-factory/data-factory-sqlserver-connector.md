---
title: "SQL Server에서 aaaMove 데이터 tooand | Microsoft Docs"
description: "Azure 데이터 팩터리를 사용 하 여 Azure VM에서 또는 toomove 데이터/SQL Server에서 데이터베이스 방법 즉 온-프레미스에 대 한 알아봅니다."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 864ece28-93b5-4309-9873-b095bbe6fedd
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jingwang
ms.openlocfilehash: f0cccf56a670e62ec893d75052a81eb26d562050
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-sql-server-on-premises-or-on-iaas-azure-vm-using-azure-data-factory"></a>Azure 데이터 팩터리를 사용 하 여 데이터 tooand IaaS (Azure VM)에서 또는 SQL Server 온-프레미스에서 이동
이 문서에서는 toouse 온-프레미스 SQL Server 데이터베이스에서 Azure Data Factory toomove 데이터에서 복사 작업을 hello 하는 방법을 설명 합니다. Hello에 기반 [데이터 이동 작업](data-factory-data-movement-activities.md) hello 복사 작업으로 데이터 이동에 대 한 일반적인 개요를 제공 하는 문서입니다. 

## <a name="supported-scenarios"></a>지원되는 시나리오
데이터를 복사할 수 **SQL Server 데이터베이스에서** toohello 데이터 저장소를 다음:

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

Hello 다음 데이터 저장소에서에서 데이터를 복사할 수 **tooa SQL Server 데이터베이스**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="supported-sql-server-versions"></a>지원되는 SQL Server 버전
이 SQL Server 커넥터 지원 데이터를 복사 toohello 다음 버전의 호스트 인스턴스 온-프레미스 또는 둘 다 SQL 인증 및 Windows 인증을 사용 하 여 Azure IaaS에서 /: SQL Server 2016, SQL Server 2014, SQL Server 2012, SQL Server 2008 R2, SQL Server 2008, SQL Server 2005

## <a name="enabling-connectivity"></a>연결 사용
SQL Server가 호스팅된 온-프레미스 또는 Azure IaaS에서 (인프라-as a Service) Vm을 연결 하는 데 필요한 단계 및 hello 개념 같은 hello 됩니다. 두 경우 모두 연결에 대 한 데이터 관리 게이트웨이 toouse가 필요 합니다.

참조 [온-프레미스 위치와 클라우드 간의 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 데이터 관리 게이트웨이 및 hello 게이트웨이 설정에 대 한 단계별 지침에 대 한 문서 toolearn 합니다. SQL Server에 연결하기 위해서는 게이트웨이 인스턴스를 설정해야 합니다.

게이트웨이 설치할 수 있지만 hello에 동일한 온-프레미스 컴퓨터 또는 클라우드 VM 인스턴스 성능 향상을 위해 SQL Server hello, 별도 컴퓨터에 설치 하는 것이 좋습니다. 리소스 경합을 줄이는 hello 게이트웨이 SQL Server가 별도 컴퓨터에 포함 합니다.

## <a name="getting-started"></a>시작
다른 도구/API를 사용하여 온-프레미스 SQL Server 데이터베이스 간에 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다.

hello 가장 쉬운 방법은 toocreate 파이프라인은 toouse hello **복사 마법사**합니다. 참조 [자습서: 복사 마법사를 사용 하 여 파이프라인을 만들고](data-factory-copy-data-wizard-tutorial.md) 간략 한 설명이 hello 복사 데이터 마법사를 사용 하 여 파이프라인을 만드는 방법에 대 한 합니다.

다음 도구 toocreate 파이프라인 hello을 사용할 수 있습니다: **Azure 포털**, **Visual Studio**, **Azure PowerShell**, **Azure 리소스 관리자 템플릿** , **.NET API**, 및 **REST API**합니다. 참조 [복사 활동 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 단계별 지침 toocreate 복사 작업으로 파이프라인에 대 한 합니다. 

Hello 도구 또는 Api를 사용 하는지 여부를 hello tooa 싱크 데이터 저장소를 저장 하는 원본 데이터에서 데이터를 이동 하는 파이프라인 단계 toocreate 다음을 수행 합니다. 

1. **데이터 팩터리**를 만듭니다. 데이터 팩터리에는 하나 이상의 파이프라인이 포함될 수 있습니다. 
2. 만들 **연결 된 서비스** toolink 입력 및 출력 데이터 저장소 tooyour 데이터 팩터리입니다. 예를 들어 SQL Server 데이터베이스 tooan Azure blob 저장소에서에서 데이터를 복사 하는 경우 만들면 두 개의 연결 된 서비스 toolink SQL Server 데이터베이스 및 Azure 저장소 계정 tooyour 데이터 팩터리입니다. 연결 된 서비스 속성 특정 tooSQL 서버 데이터베이스에 대해 참조 [연결 된 서비스 속성](#linked-service-properties) 섹션. 
3. 만들 **데이터 집합** 입력 및 출력 toorepresent hello에 대 한 데이터 복사 작업을 합니다. 예에서 hello hello 마지막 단계에서 언급 한 hello 입력된 데이터를 포함 하 여 SQL Server 데이터베이스에 데이터 집합 toospecify hello SQL 테이블을 만듭니다. And, 다른 데이터 집합 toospecify hello blob 컨테이너 만들기 및 SQL Server 데이터베이스 hello에서 복사 된 hello 데이터를 보유 하는 hello 폴더입니다. 데이터 집합 속성을 특정 tooSQL 서버 데이터베이스에 대 한 참조 [데이터 집합 속성](#dataset-properties) 섹션.
4. 입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다. 앞에서 언급 한 hello 예제를 사용 하 여 SqlSource 소스 및 BlobSink로는 싱크도 hello 복사 작업에 대 한. 마찬가지로, Azure Blob 저장소 tooSQL 서버 데이터베이스에서에서 복사 하는 경우 BlobSource 및 사용 SqlSink hello 복사 활동에서. 복사 활동 속성을 특정 tooSQL 서버 데이터베이스를 참조 하십시오. [활동 속성을 복사](#copy-activity-properties) 섹션. 에 대 한 내용은 toouse 데이터 저장 되는 방식과 원본 또는 싱크도, 데이터 저장소에 대 한 hello 이전 단원의 hello 링크를 클릭 합니다. 

Hello 마법사를 사용 하 여 이러한 데이터 팩터리 엔터티 (연결 된 서비스, 데이터 집합 및 hello 파이프라인)에 대 한 JSON 정의를 자동으로 만들어집니다. 도구/Api (제외.NET API)를 사용 하면 hello JSON 형식을 사용 하 여이 Data Factory 엔터티를 정의 합니다.  샘플 은/온-프레미스 SQL Server 데이터베이스에서 사용 되는 toocopy 데이터를 Data Factory 엔터티에 대 한 JSON 정의 가진 [JSON 예제](#json-examples-for-copying-data-from-and-to-sql-server) 이 문서의 섹션. 

다음 섹션 hello JSON 속성을 사용 하는 toodefine Data Factory 엔터티에 특정 tooSQL 서버에 대 한 세부 정보를 제공 합니다. 

## <a name="linked-service-properties"></a>연결된 서비스 속성
형식의 연결 된 서비스를 만들면 **OnPremisesSqlServer** toolink 온-프레미스 SQL Server 데이터베이스 tooa 데이터 팩터리입니다. 다음 표에서 hello JSON 요소 특정 tooon 온-프레미스 SQL Server 연결 된 서비스에 대 한 설명을 제공 합니다.

다음 표에서 hello JSON 요소 특정 tooSQL 연결 된 서버 서비스에 대 한 설명을 제공 합니다.

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| type |hello type 속성이로 설정 해야: **OnPremisesSqlServer**합니다. |예 |
| connectionString |SQL 인증 또는 Windows 인증을 사용 하 여 tooconnect toohello 온-프레미스 SQL Server 데이터베이스는 데 필요한 connectionString 정보를 지정 합니다. |예 |
| gatewayName |데이터 팩터리 서비스 hello hello 게이트웨이의 이름 tooconnect toohello 온-프레미스 SQL Server 데이터베이스를 사용 해야 합니다. |예 |
| username |Windows 인증을 사용하는 경우 사용자 이름을 지정합니다. 예: **domainname\\username**. |아니요 |
| 암호 |Hello 사용자 이름에 대해 지정한 사용자 계정에 hello에 대 한 암호를 지정 합니다. |아니요 |

Hello를 사용 하 여 자격 증명을 암호화할 수 **새로 AzureRmDataFactoryEncryptValue** cmdlet hello 다음 예제와 같이 hello 연결 문자열에서 사용 하 고 (**EncryptedCredential** 속성):  

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```

### <a name="samples"></a>샘플
**SQL 인증을 사용하는 JSON**

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties":
    {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
**Windows 인증을 사용하는 JSON**

데이터 관리 게이트웨이 지정 된 hello를 가장 하는 사용자 계정 tooconnect toohello 온-프레미스 SQL Server 데이터베이스입니다. 

```json
{
     "Name": " MyOnPremisesSQLDB",
     "Properties":
     {
         "type": "OnPremisesSqlServer",
         "typeProperties": {
             "ConnectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=True;",
             "username": "<domain\\username>",
             "password": "<password>",
             "gatewayName": "<gateway name>"
        }
     }
}
```

## <a name="dataset-properties"></a>데이터 집합 속성
형식의 데이터 집합 hello 샘플에서 사용한 **SqlServerTable** toorepresent SQL Server 데이터베이스의 테이블입니다.  

섹션 및 데이터 집합 정의에 사용 가능한 속성의 전체 목록을 보려면 hello [데이터 집합을 만드는](data-factory-create-datasets.md) 문서. 데이터 집합 JSON의 structure, availability, policy와 같은 섹션은 SQL Server, Azure Blob, Azure 테이블 등의 모든 데이터베이스 형식에 대해 비슷합니다.

hello typeProperties 섹션 hello 데이터 저장소에 hello 데이터의 hello 위치에 대 한 정보를 제공 및 데이터 집합의 각 유형에 대해과 다릅니다. hello **typeProperties** 형식의 hello 데이터 집합에 대 한 섹션 **SqlServerTable** hello 다음과 같은 속성에:

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| tableName |Hello 테이블 또는 뷰의 연결 된 서비스는 hello SQL Server 데이터베이스 인스턴스의 이름이 참조 합니다. |예 |

## <a name="copy-activity-properties"></a>복사 작업 속성
SQL Server 데이터베이스에서 데이터를 이동 하는 경우 hello 소스 형식에서에서 설정한 hello 복사 활동 너무**SqlSource**합니다. 마찬가지로, 데이터 tooa SQL Server 데이터베이스를 이동 하는 경우 설정한 hello 싱크 유형이 hello 복사 활동에서 너무**SqlSink**합니다. 이 섹션에서는 SqlSource 및 SqlSink에서 지원되는 속성의 목록을 제공합니다.

섹션 및 활동 정의에 사용 가능한 속성의 전체 목록을 참조 hello [파이프라인 만들기](data-factory-create-pipelines.md) 문서. 이름, 설명, 입력/출력 테이블, 정책 등의 속성은 모든 형식의 활동에 사용할 수 있습니다.

> [!NOTE]
> 복사 활동 hello 하나의 입력을 하나의 출력을 생성 합니다.

반면 hello 활동의 hello typeProperties 섹션에서 사용할 수 있는 속성에 각 활동 유형에 따라 다릅니다. 복사 작업은 원본 및 싱크의 hello 형식에 따라 변경합니다.

### <a name="sqlsource"></a>SqlSource
복사 작업의 원본 유형의 경우 **SqlSource**, hello 다음과 같은 속성에서 사용할 수 있는 **typeProperties** 섹션:

| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| SqlReaderQuery |사용자 지정 쿼리 tooread 데이터 hello를 사용 합니다. |SQL 쿼리 문자열. 예: select * from MyTable. Hello 입력된 데이터 집합에서 참조 하는 hello 데이터베이스에서 여러 테이블을 참조할 수 있습니다. 지정 하지 않으면 실행 되는 SQL 문을 hello: MyTable 중에서 선택 합니다. |아니요 |
| sqlReaderStoredProcedureName |Hello 원본 테이블에서 데이터를 읽을 수 있는 프로시저를 저장 하는 hello의 이름입니다. |저장 프로시저를 hello의 이름입니다. hello 마지막 SQL 문이 hello 저장 프로시저의 SELECT 문 이어야 합니다. |아니요 |
| storedProcedureParameters |Hello에 대 한 매개 변수 저장 프로시저입니다. |이름/값 쌍입니다. Hello 이름과 대/소문자 hello 저장 프로시저 매개 변수의 이름 및 매개 변수는 대/소문자 구분 일치 해야 합니다. |아니요 |

경우 hello **sqlReaderQuery** 에 대해 지정 된 hello SqlSource, hello 복사 활동 hello SQL Server 데이터베이스 원본 tooget hello 데이터에 대해이 쿼리를 실행 합니다.

또는 hello를 지정 하 여 저장된 프로시저를 지정할 수 있습니다 **sqlReaderStoredProcedureName** 및 **storedProcedureParameters** (경우 hello 저장된 프로시저 매개 변수를 사용).

Hello 구조 섹션에 정의 된 hello 열 sqlReaderQuery 또는 sqlReaderStoredProcedureName 중 하나를 지정 하지 않으면 경우 사용 되는 toobuild hello SQL Server 데이터베이스에 대해 선택 쿼리 toorun 합니다. 데이터 집합 정의 hello hello 구조 없으면 hello 테이블에서 모든 열을 선택 합니다.

> [!NOTE]
> 사용 하는 경우 **sqlReaderStoredProcedureName**, hello에 대 한 값을 toospecify 보내야 **tableName** hello 데이터 집합 JSON의에서 속성입니다. 그러나 이 테이블에 대해 수행되는 유효성 검사는 없습니다.

### <a name="sqlsink"></a>파이프라인
**SqlSink** hello 다음과 같은 속성을 지원 합니다.

| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| writeBatchTimeout |대기 시간이 초과 되기 전에 일괄 처리 삽입 작업 toocomplete hello에 대 한 시간입니다. |timespan<br/><br/> 예: “00:30:00”(30분). |아니요 |
| writeBatchSize |WriteBatchSize hello 버퍼 크기에 이르면 hello SQL 테이블에 데이터를 삽입 합니다. |정수(행 수) |아니요(기본값: 10000) |
| sqlWriterCleanupScript |특정 조각의 데이터 정리 되도록 tooexecute 복사 작업에 대 한 쿼리를 지정 합니다. 자세한 내용은 [반복 가능한 복사](#repeatable-copy) 섹션을 참조하세요. |쿼리 문입니다. |아니요 |
| sliceIdentifierColumnName |특정 조각 다시 실행 시점의 데이터를 사용 하는 tooclean 변수인 자동 생성 된 조각 식별자를 가진 toofill 복사 작업에 대 한 열 이름을 지정 합니다. 자세한 내용은 [반복 가능한 복사](#repeatable-copy) 섹션을 참조하세요. |이진(32) 데이터 형식이 있는 열의 열 이름입니다. |아니요 |
| sqlWriterStoredProcedureName |Hello 저장 프로시저의 이름 (업데이트/삽입) upserts 데이터 hello 대상 테이블에 있습니다. |저장 프로시저를 hello의 이름입니다. |아니요 |
| storedProcedureParameters |Hello에 대 한 매개 변수 저장 프로시저입니다. |이름/값 쌍입니다. Hello 이름과 대/소문자 hello 저장 프로시저 매개 변수의 이름 및 매개 변수는 대/소문자 구분 일치 해야 합니다. |아니요 |
| sqlWriterTableType |테이블 형식 이름 toobe hello 저장 프로시저에 사용을 지정 합니다. 복사 활동 임시 테이블과이 테이블 형식으로 사용할 수 있는 이동 된 hello 데이터를 만듭니다. 저장된 프로시저 코드 hello 데이터를 기존 데이터와 복사를 병합할 수 있습니다. |테이블 유형 이름 |아니요 |


## <a name="json-examples-for-copying-data-from-and-toosql-server"></a>TooSQL 서버와의 데이터를 복사 하기 위한 JSON 예제
hello 다음 예에서는 샘플 JSON 정의 사용 하 여 toocreate 파이프라인을 사용할 수 있는 [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md) 또는 [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 또는 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)합니다. 샘플 표시 방법을 따르는 hello toocopy 데이터 tooand SQL Server와 Azure Blob 저장소입니다. 그러나 데이터를 복사할 수 있습니다 **직접** 명시 된 hello 싱크 소스 tooany 중 어디에서 든 [여기](data-factory-data-movement-activities.md#supported-data-stores-and-formats) Azure Data Factory에서 복사 작업 hello를 사용 하 여 합니다.     

## <a name="example-copy-data-from-sql-server-tooazure-blob"></a>예: SQL Server tooAzure Blob에서에서 데이터를 복사 합니다.
다음 샘플에서는 hello:

1. [OnPremisesSqlServer](#linked-service-properties)형식의 연결된 서비스
2. [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)형식의 연결된 서비스
3. [SqlServerTable](#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)
4. [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)
5. hello [파이프라인](data-factory-create-pipelines.md) 사용 하 여 복사 작업으로 [SqlSource](#copy-activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)합니다.

hello 샘플 시계열 데이터 복사 SQL Server 테이블 tooan Azure blob에서에서 1 시간 마다 합니다. 이 예제에 사용 되는 hello JSON 속성 hello 샘플 다음 섹션에 설명 되어 있습니다.

첫 번째 단계로, hello 데이터 관리 게이트웨이 설치 합니다. hello 지침은 hello [온-프레미스 위치와 클라우드 간의 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서.

**SQL Server 연결된 서비스**
```json
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
**Azure Blob 저장소 연결된 서비스**

```json
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
**SQL Server 입력 데이터 집합**

hello 샘플 테이블 "MyTable" SQL Server에서 만들고 시계열 데이터에 대 한 "timestampcolumn" 라는 열이 포함 된 가정 합니다. TableName typeProperty hello 데이터 집합의 단일 데이터 집합 이지만 단일 테이블을 사용 하 여 동일한 데이터베이스를 사용 해야 하는 hello 내에서 여러 테이블에 대해 쿼리할 수 있습니다.

설정 "외부": "true" 알리고 데이터 팩터리 서비스 hello 데이터 집합의 데이터 팩터리 외부 toohello hello data factory에는 활동에 의해 생성 되지 않습니다.

```json
{
  "name": "SqlServerInput",
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
**Azure Blob 출력 데이터 집합**

데이터가 새 blob tooa 1 시간 마다 기록 됩니다 (빈도: 시, 간격: 1). hello blob에 대 한 hello 폴더 경로 처리 중인 hello 조각의 hello 시작 시간에 따라 동적으로 평가 됩니다. hello 폴더 경로 hello 시작 시간의 연도, 월, 일 및 시간 부분을 사용 합니다.

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
**복사 작업을 포함하는 파이프라인**

복사 작업을 포함 하는 hello 파이프라인 구성된 toouse 이러한 입력 및 출력 데이터 집합은 하 고 예약 된 toorun 1 시간입니다. Hello 파이프라인 JSON 정의에서 hello **소스** 형식이 너무 설정**SqlSource** 및 **싱크** 형식이 너무 설정**BlobSink**합니다. hello에 대 한 지정 된 hello SQL 쿼리 **SqlReaderQuery** 속성 시간 toocopy 지난 hello에 hello 데이터를 선택 합니다.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2016-06-01T18:00:00",
    "end":"2016-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "SqlServertoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": " SqlServerInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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
이 예제에서는 **sqlReaderQuery** SqlSource hello에 대 한 지정 합니다. 복사 활동 hello hello SQL Server 데이터베이스 원본 tooget hello 데이터에 대해이 쿼리를 실행합니다. 또는 hello를 지정 하 여 저장된 프로시저를 지정할 수 있습니다 **sqlReaderStoredProcedureName** 및 **storedProcedureParameters** (경우 hello 저장된 프로시저 매개 변수를 사용). hello sqlReaderQuery hello 입력된 데이터 집합에서 참조 하는 hello 데이터베이스 내에서 여러 테이블을 참조할 수 있습니다. 데이터 집합의 tableName typeProperty hello으로 설정 하는 제한 된 tooonly hello 테이블이 아닙니다.

Hello 구조 섹션에 정의 된 hello 열 sqlReaderQuery 또는 sqlReaderStoredProcedureName를 지정 하지 않으면 경우 사용 되는 toobuild hello SQL Server 데이터베이스에 대해 선택 쿼리 toorun 합니다. 데이터 집합 정의 hello hello 구조 없으면 hello 테이블에서 모든 열을 선택 합니다.

Hello 참조 [Sql 원본](#sqlsource) 섹션 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) hello SqlSource에서 BlobSink로 지원 되는 속성 목록에 대 한 합니다.

## <a name="example-copy-data-from-azure-blob-toosql-server"></a>예: Azure Blob tooSQL 서버에서에서 데이터를 복사 합니다.
다음 샘플에서는 hello:

1. hello는 연결 된 서비스 유형의 [OnPremisesSqlServer](#linked-service-properties)합니다.
2. hello는 연결 된 서비스 유형의 [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)합니다.
3. [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)입니다.
4. [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)
5. hello [파이프라인](data-factory-create-pipelines.md) 사용 하 여 복사 작업으로 [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) 및 [SqlSink](#sql-server-copy-activity-type-properties)합니다.

hello 샘플 시계열 데이터 복사, Azure blob tooa SQL Server 테이블에서 1 시간 마다 합니다. 이 예제에 사용 되는 hello JSON 속성 hello 샘플 다음 섹션에 설명 되어 있습니다.

**SQL Server 연결된 서비스**

```json
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
**Azure Blob 저장소 연결된 서비스**

```json
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
**Azure Blob 입력 데이터 집합**

데이터는 매시간 새 blob에 선택됩니다(frequency: hour, interval: 1). hello 폴더 경로 파일 이름은 hello blob에 대 한 처리 중인 hello 조각의 hello 시작 시간에 따라 동적으로 평가 됩니다. 연도, 월 및 일 부분은 hello 시작 시간의 hello 폴더 경로 사용 하 고 파일 이름을 hello 시작 시간의 시간 부분을 hello를 사용 합니다. "external": "true" 설정을 알리고 hello 데이터 팩터리 서비스 hello 데이터 집합의 데이터 팩터리 외부 toohello hello data factory에는 활동에 의해 생성 되지 않습니다.

```json
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
**SQL Server 출력 데이터 집합**

hello 샘플 SQL Server에서 "MyTable" 라는 이름의 데이터 tooa 테이블에 복사 합니다. SQL Server에 hello 테이블을 만들려면 hello Blob CSV 파일 toocontain 예상 대로 동일한 수의 열을 hello 합니다. 새 행 1 시간 마다 toohello 테이블을 추가 됩니다.

```json
{
  "name": "SqlServerOutput",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlServerLinkedService",
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
**복사 작업을 포함하는 파이프라인**

복사 작업을 포함 하는 hello 파이프라인 구성된 toouse 이러한 입력 및 출력 데이터 집합은 하 고 예약 된 toorun 1 시간입니다. Hello 파이프라인 JSON 정의에서 hello **소스** 형식이 너무 설정**BlobSource** 및 **싱크** 형식이 너무 설정**SqlSink**합니다.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQL",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": " SqlServerOutput "
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource",
            "blobColumnSeparators": ","
          },
          "sink": {
            "type": "SqlSink"
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

## <a name="troubleshooting-connection-issues"></a>연결 문제 해결
1. SQL Server tooaccept 원격 연결을 구성 합니다. **SQL Server Management Studio**를 시작하고 **서버**를 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다. 선택 **연결** hello 목록 및 검사에서 **허용 원격 연결 toohello 서버**합니다.

    ![원격 연결 사용](./media/data-factory-sqlserver-connector/AllowRemoteConnections.png)

    참조 [hello 원격 액세스 서버 구성 옵션 구성](https://msdn.microsoft.com/library/ms191464.aspx) 자세한 단계입니다.
2. **SQL Server 구성 관리자**를 시작합니다. 확장 **SQL Server 네트워크 구성** hello에 대 한 인스턴스 마우스 선택 **MSSQLSERVER에 대 한 프로토콜**합니다. 프로토콜 hello 오른쪽 창에 표시 됩니다. **TCP/IP**를 마우스 오른쪽 단추로 클릭하고 **사용**을 클릭하여 TCP/IP를 사용하도록 설정합니다.

    ![TCP/IP 사용](./media/data-factory-sqlserver-connector/EnableTCPProptocol.png)

    TCP/IP 프로토콜을 사용하는 다른 방법 및 자세한 내용은 [서버 네트워크 프로토콜 사용 또는 사용 안 함](https://msdn.microsoft.com/library/ms191294.aspx) 을 참조하세요.
3. 같은 창 hello에서 두 번 클릭 **TCP/IP** toolaunch **TCP/IP 속성** 창.
4. Toohello 전환 **IP 주소** 탭 합니다. Toosee 아래로 스크롤하여 **IPAll** 섹션. Hello 다운 참고 * * TCP 포트 * * (기본값은 **1433**).
5. 만들기는 **hello Windows 방화벽에 대 한 규칙** hello 컴퓨터 tooallow이이 포트를 통해 들어오는 트래픽을 합니다.  
6. **연결을 확인**: tooconnect toohello 정규화 된 이름을 사용 하 여 SQL Server는 다른 컴퓨터에서 SQL Server Management Studio를 사용 합니다. 예: "<machine><domain>.corp<company>.com,1433".

   > [!IMPORTANT]

   > 참조 [온-프레미스 원본 및 데이터 관리 게이트웨이 사용 하는 hello 클라우드 간 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 자세한 정보에 대 한 합니다.
   >
   > 연결/게이트웨이 관련 문제 해결에 대한 팁은 [게이트웨이 문제 해결](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) 을 참조하세요.
   >
   >


## <a name="identity-columns-in-hello-target-database"></a>Hello 대상 데이터베이스의 id 열
이 섹션에서는 id 열이 있는 없는 id 열 tooa 대상 테이블에 있는 원본 테이블에서 데이터를 복사 하는 예제를 제공 합니다.

**원본 테이블:**

```sql
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
**대상 테이블:**

```sql
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```

해당 hello 대상 테이블에 id 열을 확인 합니다.

**원본 데이터 집합 JSON 정의**

```json
{
    "name": "SampleSource",
    "properties": {
        "published": false,
        "type": " SqlServerTable",
        "linkedServiceName": "TestIdentitySQL",
        "typeProperties": {
            "tableName": "SourceTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```
**대상 데이터 집합 JSON 정의**

```json
{
    "name": "SampleTarget",
    "properties": {
        "structure": [
            { "name": "name" },
            { "name": "age" }
        ],
        "published": false,
        "type": "AzureSqlTable",
        "linkedServiceName": "TestIdentitySQLSource",
        "typeProperties": {
            "tableName": "TargetTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": false,
        "policy": {}
    }
}
```

원본 테이블과 대상 테이블의 스키마가 서로 다릅니다(대상에 ID가 포함된 추가 열이 있음). 이 시나리오에서는 toospecify 필요 **구조** hello id 열이 포함 되지 않으면 hello 대상 데이터 집합 정의 속성입니다.

## <a name="invoke-stored-procedure-from-sql-sink"></a>SQL 싱크에서 저장된 프로시저 호출
파이프라인의 복사 작업에서, SQL 싱크에서 저장된 프로시저를 호출하는 예를 보려면 [SQL 싱크에 대한 저장 프로시저 호출](data-factory-invoke-stored-procedure-from-copy-activity.md) 문서를 참조하세요.

## <a name="type-mapping-for-sql-server"></a>SQL 서버에 대한 형식 매핑
Hello에 설명 된 대로 [데이터 이동 작업](data-factory-data-movement-activities.md) 문서 hello 복사 활동 소스 형식 toosink 형식에서 자동 형식 변환 2 단계 방식을 따릅니다 hello로 수행:

1. 네이티브 소스 형식 too.NET 형식에서 변환
2. .NET 형식 toonative 싱크 형식에서 변환

데이터를 이동 너무 및 SQL server에서 hello SQL 형식 too.NET 형식에서 그 반대의 다음 매핑이 사용 됩니다.

hello 매핑 hello ADO.NET에 대 한 SQL Server 데이터 형식 매핑과 같습니다.

| SQL Server 데이터베이스 엔진 형식 | .NET Framework 형식 |
| --- | --- |
| bigint |Int64 |
| binary |Byte[] |
| bit |Boolean |
| char |String, Char[] |
| date |DateTime |
| DateTime |DateTime |
| datetime2 |DateTime |
| Datetimeoffset |Datetimeoffset |
| 10진수 |10진수 |
| FILESTREAM 특성(varbinary(max)) |Byte[] |
| Float |Double |
| 이미지 |Byte[] |
| int |Int32 |
| money |10진수 |
| nchar |String, Char[] |
| ntext |String, Char[] |
| numeric |10진수 |
| nvarchar |String, Char[] |
| real |단일 |
| rowversion |Byte[] |
| smalldatetime |DateTime |
| smallint |Int16 |
| smallmoney |10진수 |
| sql_variant |개체 * |
| 텍스트 |String, Char[] |
| 실시간 |timespan |
| timestamp |Byte[] |
| tinyint |Byte |
| uniqueidentifier |Guid |
| varbinary |Byte[] |
| varchar |String, Char[] |
| xml |xml |

## <a name="mapping-source-toosink-columns"></a>소스 toosink 열 매핑
원본 데이터 집합 toocolumns 싱크 데이터 집합에서의 열을 toomap 참조 [Azure Data Factory에서 데이터 집합 열에 매핑](data-factory-map-columns.md)합니다.

## <a name="repeatable-copy"></a>반복 가능한 복사
데이터 tooSQL 서버 데이터베이스를 복사할 때 hello 복사 활동 기본적으로 데이터 toohello 싱크 테이블을 추가 합니다. UPSERT tooperform 대신 참조 [반복 쓰기 tooSqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) 문서. 

관계형 데이터 저장소에서 데이터를 복사할 때 유의 tooavoid에서 반복성을 유지 의도 하지 않은 결과입니다. Azure Data Factory에서는 조각을 수동으로 다시 실행할 수 있습니다. 또한 오류가 발생하면 조각을 다시 실행하도록 데이터 집합에 대한 재시도 정책을 구성할 수 있습니다. Toomake 동일한 데이터를 hello 있는지 어떻게에 관계 없이 읽기 필요한 어느 쪽에 분할 영역을 다시 실행 하는 경우 조각에 여러 번 실행 됩니다. [관계형 원본에서 반복 가능한 읽기](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)를 참조하세요.

## <a name="performance-and-tuning"></a>성능 및 튜닝
참조 [복사 활동 성능 및 조정 가이드](data-factory-copy-activity-performance.md) toolearn 키에 대 한 Azure 데이터 팩터리 및 다양 한 방법으로 toooptimize에서 데이터 이동 (복사 작업)의 성능에 영향을 해당 놓은 것입니다.

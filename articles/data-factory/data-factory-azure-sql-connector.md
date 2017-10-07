---
title: "Azure SQL 데이터베이스에서 데이터를 aaaCopy | Microsoft Docs"
description: "자세한 방법을 toocopy 데이터를 Azure 데이터 팩터리를 사용 하 여 Azure SQL 데이터베이스입니다."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 484f735b-8464-40ba-a9fc-820e6553159e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: d2ff16191afb028da75699c5e4d0bb310538db0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-azure-sql-database-using-azure-data-factory"></a>Azure 데이터 팩터리를 사용 하 여 Azure SQL 데이터베이스에서 데이터 tooand 복사
이 문서에서는 toouse 복사 작업에서 Azure SQL 데이터베이스에서 Azure Data Factory toomove 데이터 tooand hello 하는 방법을 설명 합니다. Hello에 기반 [데이터 이동 작업](data-factory-data-movement-activities.md) hello 복사 작업으로 데이터 이동에 대 한 일반적인 개요를 제공 하는 문서입니다.  

## <a name="supported-scenarios"></a>지원되는 시나리오
데이터를 복사할 수 **Azure SQL 데이터베이스에서** toohello 데이터 저장소를 다음:

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

Hello 다음 데이터 저장소에서에서 데이터를 복사할 수 **tooAzure SQL 데이터베이스**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="supported-authentication-type"></a>지원되는 인증 유형
Azure SQL Database 커넥터는 기본 인증을 지원합니다.

## <a name="getting-started"></a>시작
다른 도구/API를 사용하여 Azure SQL Database 간에 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다.

hello 가장 쉬운 방법은 toocreate 파이프라인은 toouse hello **복사 마법사**합니다. 참조 [자습서: 복사 마법사를 사용 하 여 파이프라인을 만들고](data-factory-copy-data-wizard-tutorial.md) 간략 한 설명이 hello 복사 데이터 마법사를 사용 하 여 파이프라인을 만드는 방법에 대 한 합니다.

다음 도구 toocreate 파이프라인 hello을 사용할 수 있습니다: **Azure 포털**, **Visual Studio**, **Azure PowerShell**, **Azure 리소스 관리자 템플릿** , **.NET API**, 및 **REST API**합니다. 참조 [복사 활동 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 단계별 지침 toocreate 복사 작업으로 파이프라인에 대 한 합니다. 

Hello 도구 또는 Api를 사용 하는지 여부를 hello tooa 싱크 데이터 저장소를 저장 하는 원본 데이터에서 데이터를 이동 하는 파이프라인 단계 toocreate 다음을 수행 합니다. 

1. **데이터 팩터리**를 만듭니다. 데이터 팩터리에는 하나 이상의 파이프라인이 포함될 수 있습니다. 
2. 만들 **연결 된 서비스** toolink 입력 및 출력 데이터 저장소 tooyour 데이터 팩터리입니다. 예를 들어 Azure blob 저장소 tooan Azure SQL 데이터베이스에서 데이터를 복사 하는 경우 만들면 두 개의 연결 된 서비스 toolink Azure 저장소 계정 및 Azure SQL 데이터베이스 tooyour 데이터 팩터리입니다. 연결 된 서비스 속성 특정 tooAzure SQL 데이터베이스에 대해 참조 [연결 된 서비스 속성](#linked-service-properties) 섹션. 
3. 만들 **데이터 집합** 입력 및 출력 toorepresent hello에 대 한 데이터 복사 작업을 합니다. Hello 마지막 단계에서 언급 한 hello 예제에서는 데이터 집합 toospecify hello blob 컨테이너 및 hello 입력된 데이터를 포함 된 폴더를 만듭니다. 고 hello blob 저장소에서 복사 하는 hello 데이터를 보유 하는 hello Azure SQL 데이터베이스에서 다른 데이터 집합 toospecify hello SQL 테이블을 만듭니다. 특정 tooAzure 데이터 레이크 저장소는 데이터 집합 속성을 참조 하십시오. [데이터 집합 속성](#dataset-properties) 섹션.
4. 입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다. 앞에서 언급 한 hello 예제에서는 사용 BlobSource 원본과 SqlSink 싱크도 hello 복사 작업에 대 한 합니다. 마찬가지로, Azure SQL 데이터베이스 tooAzure Blob 저장소에서에서 복사 하는 경우 SqlSource 및 사용 BlobSink hello 복사 활동에서. 복사 활동 속성을 특정 tooAzure SQL 데이터베이스를 참조 하십시오. [활동 속성을 복사](#copy-activity-properties) 섹션. 에 대 한 내용은 toouse 데이터 저장 되는 방식과 원본 또는 싱크도, 데이터 저장소에 대 한 hello 이전 단원의 hello 링크를 클릭 합니다.

Hello 마법사를 사용 하 여 이러한 데이터 팩터리 엔터티 (연결 된 서비스, 데이터 집합 및 hello 파이프라인)에 대 한 JSON 정의를 자동으로 만들어집니다. 도구/Api (제외.NET API)를 사용 하면 hello JSON 형식을 사용 하 여이 Data Factory 엔터티를 정의 합니다.  샘플 은/Azure SQL 데이터베이스에서 사용 되는 toocopy 데이터를 Data Factory 엔터티에 대 한 JSON 정의 가진 [JSON 예제](#json-examples-for-copying-data-to-and-from-sql-database) 이 문서의 섹션. 

다음 섹션 hello JSON 속성을 사용 하는 toodefine Data Factory 엔터티에 특정 tooAzure SQL 데이터베이스에 대 한 세부 정보를 제공 합니다. 

## <a name="linked-service-properties"></a>연결된 서비스 속성
Azure SQL 한 Azure SQL 데이터베이스 tooyour 데이터 팩터리 서비스 링크를 연결합니다. 다음 표에서 hello JSON 요소 특정 tooAzure SQL에 대 한 연결 된 서비스를 제공 합니다.

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| type |hello type 속성 설정 해야 합니다: **AzureSqlDatabase** |예 |
| connectionString |Hello connectionString 속성에 대 한 tooconnect toohello Azure SQL 데이터베이스 인스턴스는 데 필요한 정보를 지정 합니다. 기본 인증만 지원됩니다. |예 |

> [!IMPORTANT]
> 구성 [Azure SQL 데이터베이스 방화벽](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) 데이터베이스 서버를 너무 hello[Azure 서비스 tooaccess hello 서버](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure)합니다. 또한 외부 Azure 비롯 하 여 데이터 팩터리 게이트웨이와 온-프레미스 데이터 원본에서 데이터 tooAzure SQL 데이터베이스를 복사 하는 경우 데이터 tooAzure SQL 데이터베이스를 전송 하는 hello 컴퓨터에 대 한 적절 한 IP 주소 범위를 구성 합니다.

## <a name="dataset-properties"></a>데이터 집합 속성
데이터 집합 toorepresent toospecify hello 데이터 집합의 hello 형식 속성을 설정 Azure SQL 데이터베이스에 입력 또는 출력 데이터: **AzureSqlTable**합니다. 집합 hello **linkedServiceName** hello SQL Azure의 hello dataset toohello 이름의 속성이 연결 된 서비스입니다.  

섹션 및 데이터 집합 정의에 사용 가능한 속성의 전체 목록을 보려면 hello [데이터 집합을 만드는](data-factory-create-datasets.md) 문서. 구조, 가용성 및 JSON 데이터 집합의 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다(Azure SQL, Azure blob, Azure 테이블 등).

hello typeProperties 섹션 hello 데이터 저장소에 hello 데이터의 hello 위치에 대 한 정보를 제공 및 데이터 집합의 각 유형에 대해과 다릅니다. hello **typeProperties** 형식의 hello 데이터 집합에 대 한 섹션 **AzureSqlTable** hello 다음과 같은 속성에:

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| tableName |Hello 테이블 또는 뷰의 연결 된 서비스는 hello Azure SQL 데이터베이스 인스턴스의 이름이 참조 합니다. |예 |

## <a name="copy-activity-properties"></a>복사 작업 속성
섹션 및 활동 정의에 사용 가능한 속성의 전체 목록을 참조 hello [파이프라인 만들기](data-factory-create-pipelines.md) 문서. 이름, 설명, 입력/출력 테이블, 정책 등의 속성은 모든 형식의 활동에 사용할 수 있습니다.

> [!NOTE]
> 복사 활동 hello 하나의 입력을 하나의 출력을 생성 합니다.

반면 hello에 사용할 수 있는 속성 **typeProperties** hello 활동의 섹션에 각 활동 유형에 따라 다릅니다. 복사 작업은 원본 및 싱크의 hello 형식에 따라 변경합니다.

Azure SQL 데이터베이스에서 데이터를 이동 하는 경우 hello 소스 형식에서에서 설정한 hello 복사 활동 너무**SqlSource**합니다. 마찬가지로, 데이터 tooan Azure SQL 데이터베이스를 이동 하는 경우 설정한 hello 싱크 유형이 hello 복사 활동에서 너무**SqlSink**합니다. 이 섹션에서는 SqlSource 및 SqlSink에서 지원되는 속성의 목록을 제공합니다.

### <a name="sqlsource"></a>SqlSource
Hello 원본 유형인 경우 복사 활동에서 **SqlSource**, hello 다음과 같은 속성에서 사용할 수 있는 **typeProperties** 섹션:

| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| SqlReaderQuery |사용자 지정 쿼리 tooread 데이터 hello를 사용 합니다. |SQL 쿼리 문자열. 예: `select * from MyTable`. |아니요 |
| sqlReaderStoredProcedureName |Hello 원본 테이블에서 데이터를 읽을 수 있는 프로시저를 저장 하는 hello의 이름입니다. |저장 프로시저를 hello의 이름입니다. hello 마지막 SQL 문이 hello 저장 프로시저의 SELECT 문 이어야 합니다. |아니요 |
| storedProcedureParameters |Hello에 대 한 매개 변수 저장 프로시저입니다. |이름/값 쌍입니다. Hello 이름과 대/소문자 hello 저장 프로시저 매개 변수의 이름 및 매개 변수는 대/소문자 구분 일치 해야 합니다. |아니요 |

경우 hello **sqlReaderQuery** 에 대해 지정 된 hello SqlSource, hello 복사 활동 hello Azure SQL 데이터베이스 원본 tooget hello 데이터에 대해이 쿼리를 실행 합니다. 또는 hello를 지정 하 여 저장된 프로시저를 지정할 수 있습니다 **sqlReaderStoredProcedureName** 및 **storedProcedureParameters** (경우 hello 저장된 프로시저 매개 변수를 사용).

Hello 데이터 집합 JSON의 hello 구조 섹션에 정의 된 hello 열은 사용 되는 toobuild 쿼리 sqlReaderQuery 또는 sqlReaderStoredProcedureName 중 하나를 지정 하지 않으면 (`select column1, column2 from mytable`) toorun hello Azure SQL 데이터베이스에 대 한 합니다. 데이터 집합 정의 hello hello 구조 없으면 hello 테이블에서 모든 열을 선택 합니다.

> [!NOTE]
> 사용 하는 경우 **sqlReaderStoredProcedureName**, hello에 대 한 값을 toospecify 보내야 **tableName** hello 데이터 집합 JSON의에서 속성입니다. 그러나 이 테이블에 대해 수행되는 유효성 검사는 없습니다.
>
>

### <a name="sqlsource-example"></a>SqlSource 예제

```JSON
"source": {
    "type": "SqlSource",
    "sqlReaderStoredProcedureName": "CopyTestSrcStoredProcedureWithParameters",
    "storedProcedureParameters": {
        "stringData": { "value": "str3" },
        "identifier": { "value": "$$Text.Format('{0:yyyy}', SliceStart)", "type": "Int"}
    }
}
```

**hello는 프로시저 정의 저장 합니다.**

```SQL
CREATE PROCEDURE CopyTestSrcStoredProcedureWithParameters
(
    @stringData varchar(20),
    @identifier int
)
AS
SET NOCOUNT ON;
BEGIN
     select *
     from dbo.UnitTestSrcTable
     where dbo.UnitTestSrcTable.stringData != stringData
    and dbo.UnitTestSrcTable.identifier != identifier
END
GO
```

### <a name="sqlsink"></a>파이프라인
**SqlSink** hello 다음과 같은 속성을 지원 합니다.

| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| writeBatchTimeout |대기 시간이 초과 되기 전에 일괄 처리 삽입 작업 toocomplete hello에 대 한 시간입니다. |timespan<br/><br/> 예: “00:30:00”(30분). |아니요 |
| writeBatchSize |WriteBatchSize hello 버퍼 크기에 이르면 hello SQL 테이블에 데이터를 삽입 합니다. |정수(행 수) |아니요(기본값: 10000) |
| sqlWriterCleanupScript |특정 조각의 데이터 정리 되도록 tooexecute 복사 작업에 대 한 쿼리를 지정 합니다. 자세한 내용은 [반복 가능한 복사](#repeatable-copy)를 참조하세요. |쿼리 문입니다. |아니요 |
| sliceIdentifierColumnName |특정 조각 다시 실행 시점의 데이터를 사용 하는 tooclean 변수인 자동 생성 된 조각 식별자를 가진 toofill 복사 작업에 대 한 열 이름을 지정 합니다. 자세한 내용은 [반복 가능한 복사](#repeatable-copy)를 참조하세요. |이진(32) 데이터 형식이 있는 열의 열 이름입니다. |아니요 |
| sqlWriterStoredProcedureName |Hello 저장 프로시저의 이름 (업데이트/삽입) upserts 데이터 hello 대상 테이블에 있습니다. |저장 프로시저를 hello의 이름입니다. |아니요 |
| storedProcedureParameters |Hello에 대 한 매개 변수 저장 프로시저입니다. |이름/값 쌍입니다. Hello 이름과 대/소문자 hello 저장 프로시저 매개 변수의 이름 및 매개 변수는 대/소문자 구분 일치 해야 합니다. |아니요 |
| sqlWriterTableType |Hello 저장 프로시저에 사용 하는 테이블 형식 이름 toobe를 지정 합니다. 복사 활동 임시 테이블과이 테이블 형식으로 사용할 수 있는 이동 된 hello 데이터를 만듭니다. 저장된 프로시저 코드 hello 데이터를 기존 데이터와 복사를 병합할 수 있습니다. |테이블 유형 이름 |아니요 |

#### <a name="sqlsink-example"></a>SqlSink 예제

```JSON
"sink": {
    "type": "SqlSink",
    "writeBatchSize": 1000000,
    "writeBatchTimeout": "00:05:00",
    "sqlWriterStoredProcedureName": "CopyTestStoredProcedureWithParameters",
    "sqlWriterTableType": "CopyTestTableType",
    "storedProcedureParameters": {
        "identifier": { "value": "1", "type": "Int" },
        "stringData": { "value": "str1" },
        "decimalData": { "value": "1", "type": "Decimal" }
    }
}
```

## <a name="json-examples-for-copying-data-tooand-from-sql-database"></a>SQL 데이터베이스에서 데이터 tooand 복사 하기 위한 JSON 예제
hello 다음 예에서는 샘플 JSON 정의 사용 하 여 toocreate 파이프라인을 사용할 수 있는 [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md) 또는 [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 또는 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)합니다. 표시 방법을 Azure SQL 데이터베이스 및 Azure Blob 저장소에서 데이터 tooand toocopy 합니다. 그러나 데이터를 복사할 수 있습니다 **직접** 명시 된 hello 싱크 소스 tooany 중 어디에서 든 [여기](data-factory-data-movement-activities.md#supported-data-stores-and-formats) Azure Data Factory에서 복사 작업 hello를 사용 하 여 합니다.

### <a name="example-copy-data-from-azure-sql-database-tooazure-blob"></a>예: Azure SQL 데이터베이스 tooAzure Blob에서에서 데이터를 복사 합니다.
hello 동일 정의 Data Factory 엔터티에 따라 hello:

1. [AzureSqlDatabase](#linked-service-properties) 형식의 연결된 서비스입니다.
2. [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) 형식의 연결된 서비스
3. [AzureSqlTable](#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)입니다.
4. [Azure Blob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)
5. [SqlSource](#copy-activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)입니다.

hello 샘플 시계열 데이터 복사 (시간별, 일별, 등) Azure SQL 데이터베이스 tooa blob의 테이블에서 1 시간 마다 합니다. 이 예제에 사용 되는 hello JSON 속성 hello 샘플 다음 섹션에 설명 되어 있습니다.  

**Azure SQL Database 연결된 서비스:**

```JSON
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
Hello 참조 [Azure SQL 연결 서비스](#linked-service) hello 목록에 대 한이 연결 된 서비스에서 지 원하는 속성의 섹션입니다.

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
Hello 참조 [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) 이 연결 된 서비스에서 지 원하는 속성의 hello 목록에 대 한 문서입니다.


**Azure SQL 입력 데이터 집합:**

hello 샘플 테이블 "MyTable"에서 만든 Azure SQL 가정 시계열 데이터에 대 한 "timestampcolumn" 라는 열을 포함 합니다.

설정 "외부": "true" 알리고 hello Azure 데이터 팩터리 서비스 hello 데이터 집합의 데이터 팩터리 외부 toohello hello data factory에는 활동에 의해 생성 되지 않습니다.

```JSON
{
  "name": "AzureSqlInput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
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

Hello 참조 [Azure SQL 데이터 집합 형식 속성](#dataset) 이 dataset 유형에에서 지 원하는 속성의 hello 목록에 대 한 섹션.  

**Azure Blob 출력 데이터 집합:**

데이터가 새 blob tooa 1 시간 마다 기록 됩니다 (빈도: 시, 간격: 1). hello blob에 대 한 hello 폴더 경로 처리 중인 hello 조각의 hello 시작 시간에 따라 동적으로 평가 됩니다. hello 폴더 경로 hello 시작 시간의 연도, 월, 일 및 시간 부분을 사용 합니다.

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}/",
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
Hello 참조 [Azure Blob 데이터 집합 형식 속성](data-factory-azure-blob-connector.md#dataset-properties) 이 dataset 유형에에서 지 원하는 속성의 hello 목록에 대 한 섹션.  

**SQL 원본 및 Blob 싱크를 사용하는 파이프라인의 복사 작업:**

hello 파이프라인에 포함 된 구성된 toouse 않은 복사 작업 입력 및 출력 데이터 집합을 hello 및 예약 된 toorun 1 시간입니다. Hello 파이프라인 JSON 정의에서 hello **소스** 형식이 너무 설정**SqlSource** 및 **싱크** 형식이 너무 설정**BlobSink**합니다. hello에 대 한 지정 된 hello SQL 쿼리 **SqlReaderQuery** 속성 시간 toocopy 지난 hello에 hello 데이터를 선택 합니다.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "AzureSQLtoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureSQLInput"
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
Hello 예에서 **sqlReaderQuery** SqlSource hello에 대 한 지정 합니다. 복사 활동 hello hello Azure SQL 데이터베이스 원본 tooget hello 데이터에 대해이 쿼리를 실행합니다. 또는 hello를 지정 하 여 저장된 프로시저를 지정할 수 있습니다 **sqlReaderStoredProcedureName** 및 **storedProcedureParameters** (경우 hello 저장된 프로시저 매개 변수를 사용).

Hello 데이터 집합 JSON의 hello 구조 섹션에 정의 된 hello 열 sqlReaderQuery 또는 sqlReaderStoredProcedureName 중 하나를 지정 하지 않으면 경우 사용 되는 toobuild hello Azure SQL 데이터베이스에 대 한 쿼리 toorun 합니다. 예: `select column1, column2 from mytable` 데이터 집합 정의 hello hello 구조 없으면 hello 테이블에서 모든 열을 선택 합니다.

Hello 참조 [Sql 원본](#sqlsource) 섹션 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) hello SqlSource에서 BlobSink로 지원 되는 속성 목록에 대 한 합니다.

### <a name="example-copy-data-from-azure-blob-tooazure-sql-database"></a>예: Azure Blob tooAzure SQL 데이터베이스에서에서 데이터를 복사 합니다.
hello 샘플 Data Factory 엔터티에 따라 hello를 정의 합니다.  

1. [AzureSqlDatabase](#linked-service-properties) 형식의 연결된 서비스입니다.
2. [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) 형식의 연결된 서비스
3. [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)입니다.
4. [AzureSqlTable](#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)입니다.
5. [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) 및 [SqlSink](#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)입니다.

hello 샘플 시계열 데이터 복사 (시간별, 일별, 등) Azure SQL 데이터베이스에서 Azure blob tooa 테이블에서 1 시간 마다 합니다. 이 예제에 사용 되는 hello JSON 속성 hello 샘플 다음 섹션에 설명 되어 있습니다.

**Azure SQL 연결된 서비스:**

```JSON
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
Hello 참조 [Azure SQL 연결 서비스](#linked-service) hello 목록에 대 한이 연결 된 서비스에서 지 원하는 속성의 섹션입니다.

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
Hello 참조 [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) 이 연결 된 서비스에서 지 원하는 속성의 hello 목록에 대 한 문서입니다.


**Azure Blob 입력 데이터 집합:**

데이터는 매시간 새 blob에 선택됩니다(frequency: hour, interval: 1). hello 폴더 경로 파일 이름은 hello blob에 대 한 처리 중인 hello 조각의 hello 시작 시간에 따라 동적으로 평가 됩니다. 연도, 월 및 일 부분은 hello 시작 시간의 hello 폴더 경로 사용 하 고 파일 이름을 hello 시작 시간의 시간 부분을 hello를 사용 합니다. "external": "true" 설정을 hello 데이터 팩터리 서비스에 알리고이 테이블 데이터 팩터리 외부 toohello hello data factory에는 활동에 의해 생성 되지 않습니다.

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/",
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
Hello 참조 [Azure Blob 데이터 집합 형식 속성](data-factory-azure-blob-connector.md#dataset-properties) 이 dataset 유형에에서 지 원하는 속성의 hello 목록에 대 한 섹션.

**Azure SQL Database 출력 데이터 집합:**

hello 샘플 라는 이름의 "MyTable" Azure sql에서 데이터 tooa 테이블에 복사 합니다. Azure SQL로에 hello 테이블을 만들려면 hello Blob CSV 파일 toocontain 예상 대로 동일한 수의 열을 hello 합니다. 새 행 1 시간 마다 toohello 테이블을 추가 됩니다.

```JSON
{
  "name": "AzureSqlOutput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
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
Hello 참조 [Azure SQL 데이터 집합 형식 속성](#dataset) 이 dataset 유형에에서 지 원하는 속성의 hello 목록에 대 한 섹션.

**Blob 원본 및 SQL 싱크를 사용하는 파이프라인의 복사 작업:**

hello 파이프라인에 포함 된 구성된 toouse 않은 복사 작업 입력 및 출력 데이터 집합을 hello 및 예약 된 toorun 1 시간입니다. Hello 파이프라인 JSON 정의에서 hello **소스** 형식이 너무 설정**BlobSource** 및 **싱크** 형식이 너무 설정**SqlSink**합니다.

```JSON
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
            "name": "AzureSqlOutput"
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
Hello 참조 [Sql 싱크](#sqlsink) 섹션 및 [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) hello 목록이 SqlSink 및 BlobSource에서 지 원하는 속성에 대 한 합니다.

## <a name="identity-columns-in-hello-target-database"></a>Hello 대상 데이터베이스의 id 열
이 섹션에서는 id 열이 있는 id 열 tooa 대상 테이블 없이 원본 테이블에서 데이터를 복사 하기 위한 예를 제공 합니다.

**원본 테이블:**

```SQL
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
**대상 테이블:**

```SQL
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```
해당 hello 대상 테이블에 id 열을 확인 합니다.

**원본 데이터 집합 JSON 정의**

```JSON
{
    "name": "SampleSource",
    "properties": {
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

```JSON
{
    "name": "SampleTarget",
    "properties": {
        "structure": [
            { "name": "name" },
            { "name": "age" }
        ],
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
파이프라인의 복사 작업에서, SQL 싱크에서 저장된 프로시저를 호출하는 예를 보려면 [복사 작업에서 SQL 싱크에 대한 저장 프로시저 호출](data-factory-invoke-stored-procedure-from-copy-activity.md) 문서를 참조하세요. 

## <a name="type-mapping-for-azure-sql-database"></a>Azure SQL Database에 대한 형식 매핑
Hello에 설명 된 대로 [데이터 이동 작업](data-factory-data-movement-activities.md) 문서 복사 작업 단계 2 방식을 따릅니다 hello로 원본 형식 toosink 유형의 자동 형식 변환을 수행 합니다.

1. 네이티브 소스 형식 too.NET 형식에서 변환
2. .NET 형식 toonative 싱크 형식에서 변환

Azure SQL 데이터베이스에서 데이터 tooand를 이동할 때는 hello 다음 매핑은 사용 하는 SQL 유형 too.NET 형식에서 그 반대의 합니다. hello 매핑 hello ADO.NET에 대 한 SQL Server 데이터 형식 매핑과 같습니다.

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

## <a name="map-source-toosink-columns"></a>원본 toosink 열 매핑
원본 데이터 집합 toocolumns 싱크 데이터 집합에서의 열을 매핑하는 방법에 대 한 toolearn 참조 [Azure Data Factory에서 데이터 집합 열에 매핑](data-factory-map-columns.md)합니다.

## <a name="repeatable-copy"></a>반복 가능한 복사
데이터 tooSQL 서버 데이터베이스를 복사할 때 hello 복사 활동 기본적으로 데이터 toohello 싱크 테이블을 추가 합니다. UPSERT tooperform 대신 참조 [반복 쓰기 tooSqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) 문서. 

관계형 데이터 저장소에서 데이터를 복사할 때 유의 tooavoid에서 반복성을 유지 의도 하지 않은 결과입니다. Azure Data Factory에서는 조각을 수동으로 다시 실행할 수 있습니다. 또한 오류가 발생하면 조각을 다시 실행하도록 데이터 집합에 대한 재시도 정책을 구성할 수 있습니다. Toomake 동일한 데이터를 hello 있는지 어떻게에 관계 없이 읽기 필요한 어느 쪽에 분할 영역을 다시 실행 하는 경우 조각에 여러 번 실행 됩니다. [관계형 원본에서 반복 가능한 읽기](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)를 참조하세요.

## <a name="performance-and-tuning"></a>성능 및 튜닝
참조 [복사 활동 성능 및 조정 가이드](data-factory-copy-activity-performance.md) toolearn 키에 대 한 Azure 데이터 팩터리 및 다양 한 방법으로 toooptimize에서 데이터 이동 (복사 작업)의 성능에 영향을 해당 놓은 것입니다.

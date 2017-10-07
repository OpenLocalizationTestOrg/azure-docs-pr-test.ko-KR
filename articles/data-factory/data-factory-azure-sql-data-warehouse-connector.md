---
title: "aaaCopy 데이터/Azure SQL 데이터 웨어하우스 로부터 | Microsoft Docs"
description: "자세한 내용은 방법 toocopy 데이터를 Azure 데이터 팩터리를 사용 하 여 Azure SQL 데이터 웨어하우스"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: d90fa9bd-4b79-458a-8d40-e896835cfd4a
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: 75bfcf3c99844fc1297ca500107da23cf875e41f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-azure-sql-data-warehouse-using-azure-data-factory"></a>Azure 데이터 팩터리를 사용 하 여 Azure SQL 데이터 웨어하우스 로부터 데이터 tooand 복사
이 문서에서는 toouse Azure SQL 데이터 웨어하우스 로부터 Azure Data Factory toomove 데이터에서 복사 작업을 hello 하는 방법을 설명 합니다. Hello에 기반 [데이터 이동 작업](data-factory-data-movement-activities.md) hello 복사 작업으로 데이터 이동에 대 한 일반적인 개요를 제공 하는 문서입니다.  

> [!TIP]
> tooachieve 최고의 성능을, Azure SQL 데이터 웨어하우스로 PolyBase tooload 데이터를 사용 합니다. hello [Azure SQL 데이터 웨어하우스를 사용 하 여 PolyBase tooload 데이터](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) 섹션 세부 정보를 포함 합니다. 사용 사례가 있는 연습을 보려면 [Azure Data Factory를 통해 Azure SQL Data Warehouse에 15분 이내 1TB 로드](data-factory-load-sql-data-warehouse.md)를 참조하세요.

## <a name="supported-scenarios"></a>지원되는 시나리오
데이터를 복사할 수 **Azure SQL 데이터 웨어하우스에서** toohello 데이터 저장소를 다음:

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

Hello 다음 데이터 저장소에서에서 데이터를 복사할 수 **tooAzure SQL 데이터 웨어하우스**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!TIP]
> SQL Server 또는 Azure SQL 데이터베이스 tooAzure에서 데이터를 복사 하는 경우 SQL 데이터 웨어하우스, hello 대상 저장소, Data Factory에에서 hello 테이블이 존재 하지 않는 경우 자동으로 hello 테이블을에서 만들 수 SQL 데이터 웨어하우스 hello 원본의 hello 테이블의 스키마 hello를 사용 하 여 데이터 저장소입니다. 자세한 내용은 [자동 테이블 만들기](#auto-table-creation)를 참조하세요.

## <a name="supported-authentication-type"></a>지원되는 인증 유형
Azure SQL Data Warehouse 커넥터는 기본 인증을 지원합니다.

## <a name="getting-started"></a>시작
다른 도구/API를 사용하여 Azure SQL Data Warehouse 간에 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다.

hello 가장 쉬운 방법은 toocreate Azure SQL 데이터 웨어하우스 로부터 데이터를 복사 하는 파이프라인 toouse hello 복사 데이터 마법사입니다. 참조 [자습서: 데이터를 Data Factory와 SQL 데이터 웨어하우스 로드](../sql-data-warehouse/sql-data-warehouse-load-with-data-factory.md) 간략 한 설명이 hello 복사 데이터 마법사를 사용 하 여 파이프라인을 만드는 방법에 대 한 합니다.

다음 도구 toocreate 파이프라인 hello을 사용할 수 있습니다: **Azure 포털**, **Visual Studio**, **Azure PowerShell**, **Azure 리소스 관리자 템플릿** , **.NET API**, 및 **REST API**합니다. 참조 [복사 활동 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 단계별 지침 toocreate 복사 작업으로 파이프라인에 대 한 합니다.

Hello 도구 또는 Api를 사용 하는지 여부를 hello tooa 싱크 데이터 저장소를 저장 하는 원본 데이터에서 데이터를 이동 하는 파이프라인 단계 toocreate 다음을 수행 합니다.

1. **데이터 팩터리**를 만듭니다. 데이터 팩터리에는 하나 이상의 파이프라인이 포함될 수 있습니다. 
2. 만들 **연결 된 서비스** toolink 입력 및 출력 데이터 저장소 tooyour 데이터 팩터리입니다. 예를 들어 Azure blob 저장소 tooan Azure SQL 데이터 웨어하우스 로부터 데이터를 복사 하는 경우 만들면 두 개의 연결 된 서비스 toolink Azure 저장소 계정 및 Azure SQL 데이터 웨어하우스 tooyour 데이터 팩터리입니다. 특정 tooAzure SQL 데이터 웨어하우스에 있는 연결 된 서비스 속성을 참조 하십시오. [연결 된 서비스 속성](#linked-service-properties) 섹션. 
3. 만들 **데이터 집합** 입력 및 출력 toorepresent hello에 대 한 데이터 복사 작업을 합니다. Hello 마지막 단계에서 언급 한 hello 예제에서는 데이터 집합 toospecify hello blob 컨테이너 및 hello 입력된 데이터를 포함 된 폴더를 만듭니다. 고 hello blob 저장소에서 복사 하는 hello 데이터를 보유 하는 hello Azure SQL 데이터 웨어하우스에 다른 데이터 집합 toospecify hello 테이블을 만듭니다. 특정 tooAzure SQL 데이터 웨어하우스는 데이터 집합 속성을 참조 하십시오. [데이터 집합 속성](#dataset-properties) 섹션.
4. 입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다. 앞에서 언급 한 hello 예제에서는 사용 BlobSource 원본과 SqlDWSink 싱크도 hello 복사 작업에 대 한 합니다. 마찬가지로, Azure SQL 데이터 웨어하우스 tooAzure Blob 저장소에서에서 복사 하는 경우 SqlDWSource 및 사용 BlobSink hello 복사 활동에서. 복사 활동 속성을 특정 tooAzure SQL 데이터 웨어하우스를 참조 하십시오. [활동 속성을 복사](#copy-activity-properties) 섹션. 에 대 한 내용은 toouse 데이터 저장 되는 방식과 원본 또는 싱크도, 데이터 저장소에 대 한 hello 이전 단원의 hello 링크를 클릭 합니다.

Hello 마법사를 사용 하 여 이러한 데이터 팩터리 엔터티 (연결 된 서비스, 데이터 집합 및 hello 파이프라인)에 대 한 JSON 정의를 자동으로 만들어집니다. 도구/Api (제외.NET API)를 사용 하면 hello JSON 형식을 사용 하 여이 Data Factory 엔터티를 정의 합니다.  샘플 은/Azure SQL 데이터 웨어하우스에서 사용 되는 toocopy 데이터를 Data Factory 엔터티에 대 한 JSON 정의 가진 [JSON 예제](#json-examples-for-copying-data-to-and-from-sql-data-warehouse) 이 문서의 섹션.

다음 섹션 hello 사용 되는 toodefine Data Factory 엔터티에 특정 tooAzure SQL 데이터 웨어하우스는 JSON 속성에 대 한 세부 정보를 제공 합니다.

## <a name="linked-service-properties"></a>연결된 서비스 속성
다음 표에서 hello JSON 요소 특정 tooAzure SQL 데이터 웨어하우스 연결 된 서비스에 대 한 설명을 제공 합니다.

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| type |hello type 속성 설정 해야 합니다: **AzureSqlDW** |예 |
| connectionString |Hello connectionString 속성에 대 한 tooconnect toohello Azure SQL 데이터 웨어하우스 인스턴스는 데 필요한 정보를 지정 합니다. 기본 인증만 지원됩니다. |예 |

> [!IMPORTANT]
> 구성 [Azure SQL 데이터베이스 방화벽](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) 데이터베이스 서버를 너무 hello 및[Azure 서비스 tooaccess hello 서버](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure)합니다. 또한 외부 Azure 비롯 하 여 데이터 팩터리 게이트웨이와 온-프레미스 데이터 원본에서 데이터 tooAzure SQL 데이터 웨어하우스를 복사 하는 경우 데이터 tooAzure SQL 데이터 웨어하우스를 전송 하는 hello 컴퓨터에 대 한 적절 한 IP 주소 범위를 구성 합니다.

## <a name="dataset-properties"></a>데이터 집합 속성
섹션 및 데이터 집합 정의에 사용 가능한 속성의 전체 목록을 보려면 hello [데이터 집합을 만드는](data-factory-create-datasets.md) 문서. 구조, 가용성 및 JSON 데이터 집합의 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다(Azure SQL, Azure blob, Azure 테이블 등).

hello typeProperties 섹션 hello 데이터 저장소에 hello 데이터의 hello 위치에 대 한 정보를 제공 및 데이터 집합의 각 유형에 대해과 다릅니다. hello **typeProperties** 형식의 hello 데이터 집합에 대 한 섹션 **AzureSqlDWTable** hello 다음과 같은 속성에:

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| tableName |Hello 테이블 또는 뷰의 연결 된 서비스 hello hello Azure SQL 데이터 웨어하우스 데이터베이스의 이름은 참조 합니다. |예 |

## <a name="copy-activity-properties"></a>복사 작업 속성
섹션 및 활동 정의에 사용 가능한 속성의 전체 목록을 참조 hello [파이프라인 만들기](data-factory-create-pipelines.md) 문서. 이름, 설명, 입력/출력 테이블, 정책 등의 속성은 모든 형식의 활동에 사용할 수 있습니다.

> [!NOTE]
> 복사 활동 hello 하나의 입력을 하나의 출력을 생성 합니다.

반면 hello 활동의 hello typeProperties 섹션에서 사용할 수 있는 속성에 각 활동 유형에 따라 다릅니다. 복사 작업은 원본 및 싱크의 hello 형식에 따라 변경합니다.

### <a name="sqldwsource"></a>SqlDWSource
원본 유형의 경우 **SqlDWSource**, hello 다음과 같은 속성에서 사용할 수 있는 **typeProperties** 섹션:

| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| SqlReaderQuery |사용자 지정 쿼리 tooread 데이터 hello를 사용 합니다. |SQL 쿼리 문자열. 예: select * from MyTable. |아니요 |
| sqlReaderStoredProcedureName |Hello 원본 테이블에서 데이터를 읽을 수 있는 프로시저를 저장 하는 hello의 이름입니다. |저장 프로시저를 hello의 이름입니다. hello 마지막 SQL 문이 hello 저장 프로시저의 SELECT 문 이어야 합니다. |아니요 |
| storedProcedureParameters |Hello에 대 한 매개 변수 저장 프로시저입니다. |이름/값 쌍입니다. Hello 이름과 대/소문자 hello 저장 프로시저 매개 변수의 이름 및 매개 변수는 대/소문자 구분 일치 해야 합니다. |아니요 |

경우 hello **sqlReaderQuery** 에 대해 지정 된 hello SqlDWSource, hello 복사 활동 hello Azure SQL 데이터 웨어하우스 원본 tooget hello 데이터에 대해이 쿼리를 실행 합니다.

또는 hello를 지정 하 여 저장된 프로시저를 지정할 수 있습니다 **sqlReaderStoredProcedureName** 및 **storedProcedureParameters** (경우 hello 저장된 프로시저 매개 변수를 사용).

Hello 데이터 집합 JSON의 hello 구조 섹션에 정의 된 hello 열 sqlReaderQuery 또는 sqlReaderStoredProcedureName 중 하나를 지정 하지 않으면 경우 사용 되는 toobuild hello Azure SQL 데이터 웨어하우스 로부터 쿼리 toorun 합니다. 예: `select column1, column2 from mytable`. 데이터 집합 정의 hello hello 구조 없으면 hello 테이블에서 모든 열을 선택 합니다.

#### <a name="sqldwsource-example"></a>SqlDWSource 예제

```JSON
"source": {
    "type": "SqlDWSource",
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

### <a name="sqldwsink"></a>파이프라인
**SqlDWSink** hello 다음과 같은 속성을 지원 합니다.

| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| sqlWriterCleanupScript |특정 조각의 데이터 정리 되도록 tooexecute 복사 작업에 대 한 쿼리를 지정 합니다. 자세한 내용은 [반복성 섹션](#repeatability-during-copy)을 참조하세요. |쿼리 문입니다. |아니요 |
| allowPolyBase |나타냅니다 여부 BULKINSERT 메커니즘 대신 toouse PolyBase (있는 경우). <br/><br/> **PolyBase를 사용 하는 권장 방법은 tooload 데이터를 SQL 데이터 웨어하우스에 하는 hello입니다.** 참조 [Azure SQL 데이터 웨어하우스를 사용 하 여 PolyBase tooload 데이터](#use-polybase-to-load-data-into-azure-sql-data-warehouse) 제약 조건 및 세부 정보에 대 한 섹션. |True <br/>False(기본값) |아니요 |
| polyBaseSettings |속성 때 hello 지정할 수 있는 그룹을 **allowPolybase** 너무 속성이**true**합니다. |&nbsp; |아니요 |
| rejectValue |Hello 쿼리가 실패 하기 전에 거부 될 수 있는 행의 hello 개수 또는 비율을 지정 합니다. <br/><br/>Hello에 대 한 옵션을 거부 hello PolyBase에 대해 자세히 알아보려면 **인수** 섹션 [CREATE EXTERNAL TABLE (TRANSACT-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) 항목입니다. |0(기본값), 1, 2, … |아니요 |
| rejectType |리터럴 값 또는 백분율 hello rejectValue 옵션이 지정 되었는지 여부를 지정 합니다. |값(기본값), 백분율 |아니요 |
| rejectSampleValue |PolyBase hello 다시 거부 된 행의 hello 비율을 계산 하기 전에 행 tooretrieve hello 수를 결정 합니다. |1, 2, … |예. **rejectType**이 **백분율**인 경우 |
| useTypeDefault |PolyBase hello 텍스트 파일에서 데이터를 검색 하는 경우 toohandle 누락 값의 텍스트 파일을 구분 하는 방법을 지정 합니다.<br/><br/>hello 인수 섹션에서이 속성에 대 한 자세한 [CREATE EXTERNAL FILE FORMAT (Transact SQL)](https://msdn.microsoft.com/library/dn935026.aspx)합니다. |True, False(기본값) |아니요 |
| writeBatchSize |WriteBatchSize hello 버퍼 크기에 이르면 hello SQL 테이블에 데이터 삽입 |정수(행 수) |아니요(기본값: 10000) |
| writeBatchTimeout |대기 시간이 초과 되기 전에 일괄 처리 삽입 작업 toocomplete hello에 대 한 시간입니다. |timespan<br/><br/> 예: “00:30:00”(30분). |아니요 |

#### <a name="sqldwsink-example"></a>SqlDWSink 예제

```JSON
"sink": {
    "type": "SqlDWSink",
    "allowPolyBase": true
}
```

## <a name="use-polybase-tooload-data-into-azure-sql-data-warehouse"></a>PolyBase tooload 데이터를 사용 하 여 Azure SQL 데이터 웨어하우스로
**[PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide)**를 사용하는 것은 처리량이 높은 많은 양의 데이터를 Azure SQL Data Warehouse에 로드하는 효율적인 방법입니다. Hello 처리량이 많은 향상 된 hello 기본 BULKINSERT 메커니즘 대신 PolyBase를 사용 하 여 볼 수 있습니다. 자세히 비교하려면 [복사 성능 참조 번호](data-factory-copy-activity-performance.md#performance-reference)를 참조하세요. 사용 사례가 있는 연습을 보려면 [Azure Data Factory를 통해 Azure SQL Data Warehouse에 15분 이내 1TB 로드](data-factory-load-sql-data-warehouse.md)를 참조하세요.

* 원본 데이터에 있으면 **Azure Blob 또는 Azure 데이터 레이크 저장소**, 및 hello 형식은 PolyBase와 호환, PolyBase를 사용 하 여 SQL 데이터 웨어하우스 tooAzure 직접 복사할 수 있습니다. 자세한 내용은 **[PolyBase를 사용하여 직접 복사](#direct-copy-using-polybase)**를 참조하세요.
* 원본 데이터 저장소와 형식이 지원 되지 않는 원래 PolyBase에서 사용 하 여 hello  **[PolyBase를 사용 하 여 준비 된 복사본](#staged-copy-using-polybase)**  대신 기능입니다. 또한 제공 하면 처리량이 더 자동으로 hello 데이터 PolyBase 호환 가능한 형식으로 변환 하 고 hello 데이터를 Azure Blob 저장소에 저장 합니다. 그런 다음 SQL Data Warehouse에 데이터를 로드합니다.

집합 hello `allowPolyBase` 속성 너무**true** hello Azure SQL 데이터 웨어하우스로 다음 Azure Data Factory toouse PolyBase toocopy 데이터에 대 한 예제와 같이 합니다. AllowPolyBase tootrue 설정 하는 경우에 hello를 사용 하 여 PolyBase 특정 속성을 지정할 수 있습니다 `polyBaseSettings` 속성 그룹입니다. hello 참조 [SqlDWSink](#SqlDWSink) polyBaseSettings 함께 사용할 수 있는 속성에 대 한 세부 정보에 대 한 섹션.

```JSON
"sink": {
    "type": "SqlDWSink",
    "allowPolyBase": true,
    "polyBaseSettings":
    {
        "rejectType": "percentage",
        "rejectValue": 10.0,
        "rejectSampleValue": 100,
        "useTypeDefault": true
    }
}
```

### <a name="direct-copy-using-polybase"></a>PolyBase를 사용하여 직접 복사
SQL Data Warehouse PolyBase는 Azure Blob 및 Azure Data Lake Store(서비스 주체 사용)를 원본으로 직접 지원하며 특정 파일 형식 요구 사항이 적용됩니다. 원본 데이터에이 섹션에 설명 된 hello 조건에 부합 하는 경우에 원본 데이터 저장소 tooAzure PolyBase를 사용 하 여 SQL 데이터 웨어하우스에서 직접 복사할 수 있습니다. 그렇지 않을 경우, [PolyBase를 사용하여 준비한 복사본](#staged-copy-using-polybase)을 사용할 수 있습니다.

> [!TIP]
> 데이터 레이크 저장소 tooSQL 데이터 웨어하우스에서에서 toocopy 데이터를 효율적으로 자세한 정보에서 [Azure 데이터 팩터리를 사용 하면 더 쉽고 편리 하 게 toouncover 데이터 로부터 이해를 포함 하 여 SQL 데이터 웨어하우스에 데이터 레이크 저장소를 사용 하는 경우](https://blogs.msdn.microsoft.com/azuredatalake/2017/04/08/azure-data-factory-makes-it-even-easier-and-convenient-to-uncover-insights-from-data-when-using-data-lake-store-with-sql-data-warehouse/)합니다.

Hello 요구 사항이 충족 되지 않는 Azure Data Factory hello 설정을 확인 하 고 hello 데이터 이동 위한 toohello BULKINSERT 메커니즘 자동으로 변경 합니다.

1. **원본에 연결된 서비스**의 형식은 **AzureStorage** 또는 **서비스 주체 인증이 적용된 AzureDataLakeStore**입니다.  
2. hello **입력된 데이터 집합** 유형의: **AzureBlob** 또는 **AzureDataLakeStore**에서 형식을 hello 및 `type` 속성은 **OrcFormat** , 또는 **TextFormat** 하는 구성을 따르고 hello로:

   1. `rowDelimiter`는 **\n**이어야 합니다.
   2. `nullValue`너무 설정**빈 문자열** (""), 또는 `treatEmptyAsNull` 너무 설정**true**합니다.
   3. `encodingName`너무 설정**u t f-8**, 즉 **기본** 값입니다.
   4. `escapeChar`, `quoteChar`, `firstRowAsHeader` 및 `skipLineCount`는 지정되지 않습니다.
   5. `compression`은 **no compression**, **GZip** 또는 **Deflate**일 수 있습니다.

    ```JSON
    "typeProperties": {
       "folderPath": "<blobpath>",
       "format": {
           "type": "TextFormat",     
           "columnDelimiter": "<any delimiter>",
           "rowDelimiter": "\n",       
           "nullValue": "",           
           "encodingName": "utf-8"    
       },
       "compression": {  
           "type": "GZip",  
           "level": "Optimal"  
       }  
    },
    ```

3. 없는 `skipHeaderLineCount` 설정을 **BlobSource** 또는 **AzureDataLakeStore** hello hello 파이프라인에서 복사 작업에 대 한 합니다.
4. 없는 `sliceIdentifierColumnName` 설정을 **SqlDWSink** hello hello 파이프라인에서 복사 작업에 대 한 합니다. (PolyBase는 한 번의 실행으로 모든 데이터를 업데이트하거나 아무 것도 업데이트하지 않도록 보장합니다. tooachieve **반복성**를 사용할 수 있습니다 `sqlWriterCleanupScript`).
5. 없는 `columnMapping` 복사 작업에 연결 된 hello에서 사용 되 고 있습니다.

### <a name="staged-copy-using-polybase"></a>PolyBase를 사용하여 준비한 복사본
원본 데이터 hello 이전 섹션에 도입 된 hello 조건 충족 하지 않는 경우 중간 준비 Azure Blob 저장소 (프리미엄 저장소 수 없음)를 통해 데이터 복사를 사용할 수 있습니다. 이 경우 Azure 데이터 팩터리 자동으로 hello 데이터 toomeet 데이터 형식 요구 사항을 PolyBase를 사용 하 여 PolyBase tooload 데이터의 SQL 데이터 웨어하우스로 변환을 수행 및 최초의 정리 hello Blob 저장소에서 임시 데이터입니다. 스테이징 Azure Blob을 통해 데이터를 복사하는 방법에 대한 자세한 내용은 [준비된 복사](data-factory-copy-activity-performance.md#staged-copy)를 참조하세요.

> [!NOTE]
> PolyBase를 사용 하 여 Azure SQL 데이터 웨어하우스에 저장 합니다. 온-프레미스 데이터에서 데이터를 복사 하 고 준비를 사용 중인 데이터 관리 게이트웨이 버전 2.4 미만인 경우 JRE (Java Runtime Environment) 게이트웨이에 필요한 컴퓨터를 사용 하는 tootransform 원본 데이터는 적절 한 형식입니다. 이와 같은 종속성 게이트웨이 toohello 최신 tooavoid를 업그레이드 하는 것이 좋습니다.
>

toouse이 기능을 만듭니다는 [Azure 저장소 연결 된 서비스](data-factory-azure-blob-connector.md#azure-storage-linked-service) toohello hello 중간 blob 저장소에 있는 Azure 저장소 계정을 참조 하는, 다음 hello 지정 `enableStaging` 및 `stagingSettings` hello 복사 작업에 대 한 속성 와 같이 코드 다음 hello:

```json
"activities":[  
{
    "name": "Sample copy activity from SQL Server tooSQL Data Warehouse via PolyBase",
    "type": "Copy",
    "inputs": [{ "name": "OnpremisesSQLServerInput" }],
    "outputs": [{ "name": "AzureSQLDWOutput" }],
    "typeProperties": {
        "source": {
            "type": "SqlSource",
        },
        "sink": {
            "type": "SqlDwSink",
            "allowPolyBase": true
        },
        "enableStaging": true,
        "stagingSettings": {
            "linkedServiceName": "MyStagingBlob"
        }
    }
}
]
```

## <a name="best-practices-when-using-polybase"></a>PolyBase를 사용하는 경우 모범 사례
hello 다음 섹션에서는 추가 모범 사례 toohello에서 설명 하는 스토리 [Azure SQL 데이터 웨어하우스에 대 한 모범 사례](../sql-data-warehouse/sql-data-warehouse-best-practices.md)합니다.

### <a name="required-database-permission"></a>필수 데이터베이스 권한
PolyBase toouse 필요 hello 사용자 되 고 사용 되는 tooload 데이터를 SQL 데이터 웨어하우스에 hello ["권한"](https://msdn.microsoft.com/library/ms191291.aspx) hello 대상 데이터베이스에 있습니다. Tooadd는 한 가지 방법은 tooachieve "db_owner" 역할의 멤버인 사용자에 게 해당 합니다. 자세한 내용은 방법 toodo 따르면 [이 섹션](../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md#authorization)합니다.

### <a name="row-size-and-data-type-limitation"></a>행 크기 및 데이터 형식 제한 사항
Polybase 부하는 제한 된 tooloading 행 모두 보다 작은 **1MB** tooVARCHR(MAX)를 로드할 수 없습니다 및 nvarchar (max) 또는 varbinary (max). 너무 참조[여기](../sql-data-warehouse/sql-data-warehouse-service-capacity-limits.md#loads)합니다.

크기가 1MB 보다 큰 행을 사용 하 여 원본 데이터를 설정한 경우 toosplit hello 원본 테이블 세로로를 각각의 최대 행 크기 hello hello 제한을 초과 하지 않는 여러 개의 작은 시나리오로 합니다. Azure SQL 데이터 웨어하우스에 함께 병합 하 고 PolyBase를 사용 하 여 hello 작은 테이블로 다음 로드할 수 있습니다.

### <a name="sql-data-warehouse-resource-class"></a>SQL Data Warehouse 리소스 클래스
최상의 가능한 처리량 tooachieve tooassign 큰 리소스 클래스 toohello 사용자 되 고 하는 것이 좋습니다. PolyBase 통해 SQL 데이터 웨어하우스로 tooload 데이터를 사용 합니다. 자세한 방법을 toodo를 따르면 [사용자 리소스 클래스 예제 변경](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example)합니다.

### <a name="tablename-in-azure-sql-data-warehouse"></a>Azure SQL 데이터 웨어하우스의 tableName
hello 다음 표에서 예제에 대해 방법 toospecify hello **tableName** JSON 스키마와 테이블 이름의 다양 한 조합에 대 한 데이터 집합의 속성입니다.

| DB 스키마 | 테이블 이름 | tableName JSON 속성 |
| --- | --- | --- |
| dbo |MyTable |MyTable 또는 dbo.MyTable 또는 [dbo].[MyTable] |
| dbo1 |MyTable |dbo1.MyTable 또는 [dbo1].[MyTable] |
| dbo |My.Table |[My.Table] 또는 [dbo].[My.Table] |
| dbo1 |My.Table |[dbo1].[My.Table] |

Hello 다음 오류가 표시 되 면 hello tableName 속성에 대 한 지정 된 값이 hello 문제일 수 있습니다. Hello hello tableName JSON 속성에 대 한 hello 올바른 방법은 toospecify 값 표를 참조 하십시오.  

```
Type=System.Data.SqlClient.SqlException,Message=Invalid object name 'stg.Account_test'.,Source=.Net SqlClient Data Provider
```

### <a name="columns-with-default-values"></a>기본값이 있는 열
현재, PolyBase 기능 Data Factory에만 허용 hello hello 대상 테이블에 나와 있듯이 열 수가 같아야 합니다. 가령 네 개의 열이 있고 그 중 한 열이 기본 값으로 정의된 테이블이 있다고 합시다. hello 입력된 데이터는 4 개의 열을 포함 계속 해야 합니다. 3 열 입력된 데이터 집합을 제공 하는 오류와 비슷한 toohello 메시지의 뒤에 생성:

```
All columns of hello table must be specified in hello INSERT BULK statement.
```
NULL 값은 특별한 형태의 기본값입니다. Hello 입력된 데이터 (blob) 해당 열에 대 한 hello 열에서 null을 허용 하는 경우 비어 있을 수 있습니다 (hello 입력된 데이터 집합에서 누락 될 수 없습니다). PolyBase hello Azure SQL 데이터 웨어하우스 NULL을 삽입합니다.  

## <a name="auto-table-creation"></a>자동 테이블 만들기
SQL Server에서 toocopy 데이터 복사 마법사를 사용 하는 경우, Azure SQL 데이터베이스 tooAzure SQL 데이터 웨어하우스 및 hello 테이블 toohello 원본 테이블의 해당 hello 대상 저장소에 없습니다. Data Factory 자동으로 hello 테이블을에서 만들 수 hello hello 원본 테이블 스키마를 사용 하 여 데이터 웨어하우스 합니다.

데이터 팩터리 hello 대상 저장소에 hello 표를 만들고 hello 동일한 hello 원본 데이터 저장소에는 이름 테이블로 합니다. hello 데이터 형식 열에 대 한 형식 매핑을 수행 하는 hello에 따라 선택 됩니다. 필요한 경우 형식 변환 toofix 소스 및 대상 저장소 간의 비 호환성 수행 합니다. 라운드 로빈 테이블 배포를 사용하기도 합니다.

| 원본 SQL Database 열 형식 | 대상 SQL DW 열 유형(크기 제한) |
| --- | --- |
| int | int |
| BigInt | BigInt |
| SmallInt | SmallInt |
| TinyInt | TinyInt |
| Bit | Bit |
| 10진수 | 10진수 |
| 숫자 | 10진수 |
| Float | Float |
| Money | Money |
| Real | Real |
| SmallMoney | SmallMoney |
| 이진 | 이진 |
| Varbinary | Varbinary (위쪽 too8000) |
| Date | Date |
| DateTime | DateTime |
| DateTime2 | DateTime2 |
| Time | Time |
| Datetimeoffset | Datetimeoffset |
| SmallDateTime | SmallDateTime |
| 텍스트 | Varchar (위쪽 too8000) |
| NText | NVarChar (위쪽 too4000) |
| 이미지 | VarBinary (위쪽 too8000) |
| UniqueIdentifier | UniqueIdentifier |
| Char | Char |
| NChar | NChar |
| VarChar | VarChar (위쪽 too8000) |
| NVarChar | NVarChar (위쪽 too4000) |
| xml | Varchar (위쪽 too8000) |

[!INCLUDE [data-factory-type-repeatability-for-sql-sources](../../includes/data-factory-type-repeatability-for-sql-sources.md)]

## <a name="type-mapping-for-azure-sql-data-warehouse"></a>Azure SQL 데이터 웨어하우스에 대한 형식 매핑
Hello에 설명 된 대로 [데이터 이동 작업](data-factory-data-movement-activities.md) 문서, 복사 작업 소스 형식 toosink 형식에서 자동 형식 변환 단계 2 방식을 따릅니다 hello로 수행:

1. 네이티브 소스 형식 too.NET 형식에서 변환
2. .NET 형식 toonative 싱크 형식에서 변환

를 너무 및 Azure SQL 데이터 웨어하우스 로부터 데이터를 이동할 때는 hello 다음 매핑은 사용 하는 SQL 유형 too.NET 형식에서 그 반대의 합니다.

hello 매핑 hello와 같습니다. [ADO.NET에 대 한 SQL Server 데이터 형식 매핑](https://msdn.microsoft.com/library/cc716729.aspx)합니다.

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

원본 데이터 집합 toocolumns hello 복사 활동 정의에서 싱크 데이터 집합에서의 열을 매핑할 수도 있습니다. 자세한 내용은 [Azure Data Factory에서 데이터 집합 열 매핑](data-factory-map-columns.md)을 참조하세요.

## <a name="json-examples-for-copying-data-tooand-from-sql-data-warehouse"></a>SQL 데이터 웨어하우스에서 데이터 tooand 복사 하기 위한 JSON 예제
hello 다음 예에서는 샘플 JSON 정의 사용 하 여 toocreate 파이프라인을 사용할 수 있는 [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md) 또는 [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 또는 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)합니다. 표시 방법을 Azure SQL 데이터 웨어하우스 및 Azure Blob 저장소에서 데이터 tooand toocopy 합니다. 그러나 데이터를 복사할 수 있습니다 **직접** 명시 된 hello 싱크 소스 tooany 중 어디에서 든 [여기](data-factory-data-movement-activities.md#supported-data-stores-and-formats) Azure Data Factory에서 복사 작업 hello를 사용 하 여 합니다.

### <a name="example-copy-data-from-azure-sql-data-warehouse-tooazure-blob"></a>예: Azure SQL 데이터 웨어하우스 tooAzure Blob에서에서 데이터를 복사 합니다.
hello 샘플 Data Factory 엔터티에 따라 hello를 정의 합니다.

1. [AzureSqlDW](#linked-service-properties) 형식의 연결된 서비스입니다.
2. [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) 형식의 연결된 서비스
3. [AzureSqlDWTable](#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)입니다.
4. [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)
5. [SqlDWSource](#copy-activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)입니다.

hello 샘플 시계열 (시간별, 일별, 등) 데이터 복사 Azure SQL 데이터 웨어하우스 데이터베이스 tooa blob의 테이블에서 1 시간 마다 합니다. 이 예제에 사용 되는 hello JSON 속성 hello 샘플 다음 섹션에 설명 되어 있습니다.

**Azure SQL 데이터 웨어하우스 연결된 서비스:**

```JSON
{
  "name": "AzureSqlDWLinkedService",
  "properties": {
    "type": "AzureSqlDW",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
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
**Azure SQL 데이터 웨어하우스 입력 데이터 집합:**

hello 샘플 테이블 "MyTable"에서 만든 Azure SQL 데이터 웨어하우스 및 포함 된 시계열 데이터에 대 한 "timestampcolumn" 라는 열을 가정 합니다.

설정 "외부": "true" 알리고 hello 데이터 팩터리 서비스 hello 데이터 집합의 데이터 팩터리 외부 toohello hello data factory에는 활동에 의해 생성 되지 않습니다.

```JSON
{
  "name": "AzureSqlDWInput",
  "properties": {
    "type": "AzureSqlDWTable",
    "linkedServiceName": "AzureSqlDWLinkedService",
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
**Azure Blob 출력 데이터 집합:**

데이터가 새 blob tooa 1 시간 마다 기록 됩니다 (빈도: 시, 간격: 1). hello blob에 대 한 hello 폴더 경로 처리 중인 hello 조각의 hello 시작 시간에 따라 동적으로 평가 됩니다. hello 폴더 경로 hello 시작 시간의 연도, 월, 일 및 시간 부분을 사용 합니다.

```JSON
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

**SqlDWSource 및 BlobSink를 사용하는 파이프라인의 복사 작업:**

hello 파이프라인에 포함 된 구성된 toouse 않은 복사 작업 입력 및 출력 데이터 집합을 hello 및 예약 된 toorun 1 시간입니다. Hello 파이프라인 JSON 정의에서 hello **소스** 형식이 너무 설정**SqlDWSource** 및 **싱크** 형식이 너무 설정**BlobSink**합니다. hello에 대 한 지정 된 hello SQL 쿼리 **SqlReaderQuery** 속성 시간 toocopy 지난 hello에 hello 데이터를 선택 합니다.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "AzureSQLDWtoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureSqlDWInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlDWSource",
            "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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
> [!NOTE]
> Hello 예에서 **sqlReaderQuery** SqlDWSource hello에 대 한 지정 합니다. 복사 활동 hello hello Azure SQL 데이터 웨어하우스 원본 tooget hello 데이터에 대해이 쿼리를 실행합니다.
>
> 또는 hello를 지정 하 여 저장된 프로시저를 지정할 수 있습니다 **sqlReaderStoredProcedureName** 및 **storedProcedureParameters** (경우 hello 저장된 프로시저 매개 변수를 사용).
>
> Hello 데이터 집합 JSON의 hello 구조 섹션에 정의 된 hello 열은 사용 되는 toobuild 쿼리 (select column1, column2 mytable에서) sqlReaderQuery 또는 sqlReaderStoredProcedureName 중 하나를 지정 하지 않으면 Azure SQL 데이터 웨어하우스 hello에 대 한 toorun 합니다. 데이터 집합 정의 hello hello 구조 없으면 hello 테이블에서 모든 열을 선택 합니다.
>
>

### <a name="example-copy-data-from-azure-blob-tooazure-sql-data-warehouse"></a>예: Azure Blob tooAzure SQL 데이터 웨어하우스에서에서 데이터를 복사 합니다.
hello 샘플 Data Factory 엔터티에 따라 hello를 정의 합니다.

1. [AzureSqlDW](#linked-service-properties) 형식의 연결된 서비스입니다.
2. [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) 형식의 연결된 서비스
3. [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)입니다.
4. [AzureSqlDWTable](#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)입니다.
5. [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) 및 [SqlDWSink](#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)입니다.

hello 샘플 시계열 데이터 복사 (시간별, 일별, 등) Azure SQL 데이터 웨어하우스 데이터베이스의 Azure blob tooa 테이블에서 1 시간 마다 합니다. 이 예제에 사용 되는 hello JSON 속성 hello 샘플 다음 섹션에 설명 되어 있습니다.

**Azure SQL 데이터 웨어하우스 연결된 서비스:**

```JSON
{
  "name": "AzureSqlDWLinkedService",
  "properties": {
    "type": "AzureSqlDW",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
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
**Azure Blob 입력 데이터 집합:**

데이터는 매시간 새 blob에 선택됩니다(frequency: hour, interval: 1). hello 폴더 경로 파일 이름은 hello blob에 대 한 처리 중인 hello 조각의 hello 시작 시간에 따라 동적으로 평가 됩니다. 연도, 월 및 일 부분은 hello 시작 시간의 hello 폴더 경로 사용 하 고 파일 이름을 hello 시작 시간의 시간 부분을 hello를 사용 합니다. "external": "true" 설정을 hello 데이터 팩터리 서비스에 알리고이 테이블 데이터 팩터리 외부 toohello hello data factory에는 활동에 의해 생성 되지 않습니다.

```JSON
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
**Azure SQL 데이터 웨어하우스 출력 데이터 집합:**

hello 샘플 Azure SQL 데이터 웨어하우스에 "MyTable" 라는 이름의 데이터 tooa 테이블에 복사 합니다. 와 Azure SQL 데이터 웨어하우스에 hello 테이블을 만들려면 hello Blob CSV 파일 toocontain 예상 대로 동일한 수의 열을 hello 합니다. 새 행 1 시간 마다 toohello 테이블을 추가 됩니다.

```JSON
{
  "name": "AzureSqlDWOutput",
  "properties": {
    "type": "AzureSqlDWTable",
    "linkedServiceName": "AzureSqlDWLinkedService",
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
**BlobSource 및 SqlDWSink를 사용하는 파이프라인의 복사 작업:**

hello 파이프라인에 포함 된 구성된 toouse 않은 복사 작업 입력 및 출력 데이터 집합을 hello 및 예약 된 toorun 1 시간입니다. Hello 파이프라인 JSON 정의에서 hello **소스** 형식이 너무 설정**BlobSource** 및 **싱크** 형식이 너무 설정**SqlDWSink**합니다.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQLDW",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlDWOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource",
            "blobColumnSeparators": ","
          },
          "sink": {
            "type": "SqlDWSink",
            "allowPolyBase": true
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
연습을 참조 하는 hello를 참조 하세요. [15 분 미만 Azure 데이터 팩터리에 Azure SQL 데이터 웨어하우스를 1TB를 로드](data-factory-load-sql-data-warehouse.md) 및 [Azure 데이터 팩터리를 사용 하 여 데이터 로드](../sql-data-warehouse/sql-data-warehouse-get-started-load-with-azure-data-factory.md) hello Azure SQL 데이터 웨어하우스의에서 문서 설명서입니다.

## <a name="performance-and-tuning"></a>성능 및 튜닝
참조 [복사 활동 성능 및 조정 가이드](data-factory-copy-activity-performance.md) toolearn 키에 대 한 Azure 데이터 팩터리 및 다양 한 방법으로 toooptimize에서 데이터 이동 (복사 작업)의 성능에 영향을 해당 놓은 것입니다.

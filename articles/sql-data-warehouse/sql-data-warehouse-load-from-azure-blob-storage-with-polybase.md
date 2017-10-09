---
title: "Azure blob tooAzure 데이터 웨어하우스에서 aaaLoad | Microsoft Docs"
description: "어떻게 toouse PolyBase tooload 데이터에서 Azure blob 저장소에 SQL 데이터 웨어하우스에 대해 알아봅니다. 공용 데이터에서 몇 가지 테이블을 hello Contoso 소매 데이터 웨어하우스 스키마를 로드 합니다."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: faca0fe7-62e7-4e1f-a86f-032b4ffcb06e
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 4b4978ccefa4d55ff5c89fba84c5e705422ddbb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-azure-blob-storage-into-sql-data-warehouse-polybase"></a>Azure blob 저장소에서 SQL 데이터 웨어하우스로 데이터를 로드합니다(PolyBase).
> [!div class="op_single_selector"]
> * [데이터 팩터리](sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md)
> * [PolyBase](sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md)
> 
> 

PolyBase T-SQL 명령을 tooload의에서 및 데이터를 Azure blob 저장소를 사용 하 여 Azure SQL 데이터 웨어하우스로. 

단순,이 자습서에서는 두 테이블에서에서 로드 공용 Azure 저장소 Blob hello Contoso 소매 데이터 웨어하우스 스키마로 tookeep 합니다. tooload hello 전체 데이터 집합을 hello 예제 실행 [부하 hello 전체 Contoso 소매 데이터 웨어하우스] [ Load hello full Contoso Retail Data Warehouse] hello Microsoft SQL Server Samples 리포지토리에서 합니다.

이 자습서에서는 다음 작업을 수행합니다.

1. Azure blob 저장소에서 PolyBase tooload 구성
2. 공용 데이터를 데이터베이스에 로드
3. Hello 로드가 완료 된 후에 최적화를 실행 합니다.

## <a name="before-you-begin"></a>시작하기 전에
toorun이이 자습서에서는 SQL 데이터 웨어하우스 데이터베이스에 이미 있는 Azure 계정이 필요 합니다. 계정이 아직 없다면 [SQL Data Warehouse 만들기][Create a SQL Data Warehouse]를 참조하세요.

## <a name="1-configure-hello-data-source"></a>1. Hello 데이터 소스 구성
PolyBase는 T-SQL 개체 외부 toodefine hello 위치 및 hello 외부 데이터의 특성을 사용합니다. hello 외부 개체 정의 SQL 데이터 웨어하우스에 저장 됩니다. hello 데이터 자체는 외부적으로 저장 됩니다.

### <a name="11-create-a-credential"></a>1.1. 자격 증명 만들기
**이 단계는** hello Contoso 공용 데이터를 로드 하는 경우. 액세스할 수 있는 tooanyone 이미 있기 때문에 보안 액세스 toohello 공용 데이터를 필요 하지 않습니다.

**이 단계를 건너뛰지 마십시오** . 자격 증명을 사용 하 여 hello 다음 통해 tooaccess 데이터 toocreate 데이터베이스 범위 자격 증명을 스크립트 하 고 hello 데이터 원본의 hello 위치를 정의할 때 사용 합니다.

```sql
-- A: Create a master key.
-- Only necessary if one does not already exist.
-- Required tooencrypt hello credential secret in hello next step.

CREATE MASTER KEY;


-- B: Create a database scoped credential
-- IDENTITY: Provide any string, it is not used for authentication tooAzure storage.
-- SECRET: Provide your Azure storage account key.


CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential
WITH
    IDENTITY = 'user',
    SECRET = '<azure_storage_account_key>'
;


-- C: Create an external data source
-- TYPE: HADOOP - PolyBase uses Hadoop APIs tooaccess data in Azure blob storage.
-- LOCATION: Provide Azure storage account name and blob container name.
-- CREDENTIAL: Provide hello credential created in hello previous step.

CREATE EXTERNAL DATA SOURCE AzureStorage
WITH (
    TYPE = HADOOP,
    LOCATION = 'wasbs://<blob_container_name>@<azure_storage_account_name>.blob.core.windows.net',
    CREDENTIAL = AzureStorageCredential
);
```

Toostep 2를 건너뜁니다.

### <a name="12-create-hello-external-data-source"></a>1.2. Hello 외부 데이터 원본 만들기
이 사용 하 여 [외부 데이터 원본 만들기] [ CREATE EXTERNAL DATA SOURCE] hello 데이터 및 데이터 형식을 hello toostore hello 위치 명령입니다. 

```sql
CREATE EXTERNAL DATA SOURCE AzureStorage_west_public
WITH 
(  
    TYPE = Hadoop 
,   LOCATION = 'wasbs://contosoretaildw-tables@contosoretaildw.blob.core.windows.net/'
); 
```

> [!IMPORTANT]
> Toomake 개인 azure blob 저장소 컨테이너 폴더를 선택 하면는 hello 데이터 소유자로 청구 됩니다 데이터에 대 한 전송 요금 데이터 hello 데이터 센터를 벗어날 때 기억해 야 합니다. 
> 
> 

## <a name="2-configure-data-format"></a>2. 데이터 형식 구성
hello 데이터는 Azure blob 저장소에 있는 텍스트 파일에 저장 하 고 각 필드 구분 기호로 구분 됩니다. 이 스크립트를 실행 [CREATE EXTERNAL FILE FORMAT] [ CREATE EXTERNAL FILE FORMAT] hello 텍스트 파일의 hello 데이터 형식의 toospecify hello 명령입니다. hello Contoso 데이터 압축 되지 않으며 파이프 구분 합니다.

```sql
CREATE EXTERNAL FILE FORMAT TextFileFormat 
WITH 
(   FORMAT_TYPE = DELIMITEDTEXT
,    FORMAT_OPTIONS    (   FIELD_TERMINATOR = '|'
                    ,    STRING_DELIMITER = ''
                    ,    DATE_FORMAT         = 'yyyy-MM-dd HH:mm:ss.fff'
                    ,    USE_TYPE_DEFAULT = FALSE 
                    )
);
``` 

## <a name="3-create-hello-external-tables"></a>3. Hello 외부 테이블 만들기
이제 사용자가 지정한 데이터 원본 및 파일 형식이 hello 준비 toocreate hello에 대 한 외부 테이블 있는지 합니다. 

### <a name="31-create-a-schema-for-hello-data"></a>3.1. Hello 데이터에 대 한 스키마를 만듭니다.
toocreate 장소 toostore hello Contoso 데이터베이스의 데이터를, 스키마를 만듭니다.

```sql
CREATE SCHEMA [asb]
GO
```

### <a name="32-create-hello-external-tables"></a>3.2. Hello 외부 테이블을 만듭니다.
이 스크립트 toocreate hello DimProduct 및 FactOnlineSales 외부 테이블을 실행 합니다. 여기서 수행 하는 모든 열 이름과 데이터 형식을 정의 이며 toohello 위치와 서식을 hello Azure blob 저장소 파일의 바인딩. hello 정의 SQL 데이터 웨어하우스에 저장 된 및 hello 데이터는 아직 hello Azure 저장소 Blob입니다.

hello **위치** 매개 변수는 hello Azure 저장소 Blob hello 루트 폴더 아래의 하위 hello 폴더입니다. 각 테이블은 서로 다른 폴더에 있습니다.

```sql

--DimProduct
CREATE EXTERNAL TABLE [asb].DimProduct (
    [ProductKey] [int] NOT NULL,
    [ProductLabel] [nvarchar](255) NULL,
    [ProductName] [nvarchar](500) NULL,
    [ProductDescription] [nvarchar](400) NULL,
    [ProductSubcategoryKey] [int] NULL,
    [Manufacturer] [nvarchar](50) NULL,
    [BrandName] [nvarchar](50) NULL,
    [ClassID] [nvarchar](10) NULL,
    [ClassName] [nvarchar](20) NULL,
    [StyleID] [nvarchar](10) NULL,
    [StyleName] [nvarchar](20) NULL,
    [ColorID] [nvarchar](10) NULL,
    [ColorName] [nvarchar](20) NOT NULL,
    [Size] [nvarchar](50) NULL,
    [SizeRange] [nvarchar](50) NULL,
    [SizeUnitMeasureID] [nvarchar](20) NULL,
    [Weight] [float] NULL,
    [WeightUnitMeasureID] [nvarchar](20) NULL,
    [UnitOfMeasureID] [nvarchar](10) NULL,
    [UnitOfMeasureName] [nvarchar](40) NULL,
    [StockTypeID] [nvarchar](10) NULL,
    [StockTypeName] [nvarchar](40) NULL,
    [UnitCost] [money] NULL,
    [UnitPrice] [money] NULL,
    [AvailableForSaleDate] [datetime] NULL,
    [StopSaleDate] [datetime] NULL,
    [Status] [nvarchar](7) NULL,
    [ImageURL] [nvarchar](150) NULL,
    [ProductURL] [nvarchar](150) NULL,
    [ETLLoadID] [int] NULL,
    [LoadDate] [datetime] NULL,
    [UpdateDate] [datetime] NULL
)
WITH
(
    LOCATION='/DimProduct/' 
,   DATA_SOURCE = AzureStorage_west_public
,   FILE_FORMAT = TextFileFormat
,   REJECT_TYPE = VALUE
,   REJECT_VALUE = 0
)
;

--FactOnlineSales
CREATE EXTERNAL TABLE [asb].FactOnlineSales 
(
    [OnlineSalesKey] [int]  NOT NULL,
    [DateKey] [datetime] NOT NULL,
    [StoreKey] [int] NOT NULL,
    [ProductKey] [int] NOT NULL,
    [PromotionKey] [int] NOT NULL,
    [CurrencyKey] [int] NOT NULL,
    [CustomerKey] [int] NOT NULL,
    [SalesOrderNumber] [nvarchar](20) NOT NULL,
    [SalesOrderLineNumber] [int] NULL,
    [SalesQuantity] [int] NOT NULL,
    [SalesAmount] [money] NOT NULL,
    [ReturnQuantity] [int] NOT NULL,
    [ReturnAmount] [money] NULL,
    [DiscountQuantity] [int] NULL,
    [DiscountAmount] [money] NULL,
    [TotalCost] [money] NOT NULL,
    [UnitCost] [money] NULL,
    [UnitPrice] [money] NULL,
    [ETLLoadID] [int] NULL,
    [LoadDate] [datetime] NULL,
    [UpdateDate] [datetime] NULL
)
WITH
(
    LOCATION='/FactOnlineSales/' 
,   DATA_SOURCE = AzureStorage_west_public
,   FILE_FORMAT = TextFileFormat
,   REJECT_TYPE = VALUE
,   REJECT_VALUE = 0
)
;
```

## <a name="4-load-hello-data"></a>4. Hello 데이터 로드
다양 한 방법 tooaccess 외부 데이터는.  Hello 외부 테이블에서 직접 데이터를 쿼리 하 hello 데이터 새 데이터베이스 테이블에 로드 하거나 외부 데이터 tooexisting 데이터베이스 테이블을 추가할 수 있습니다.  

### <a name="41-create-a-new-schema"></a>4.1. 새 스키마를 만듭니다.
CTAS는 데이터가 포함된 새 테이블을 만듭니다.  먼저 hello contoso 데이터에 대 한 스키마를 만듭니다.

```sql
CREATE SCHEMA [cso]
GO
```

### <a name="42-load-hello-data-into-new-tables"></a>4.2. Hello 데이터를 새 테이블로 로드
blob 저장소와 데이터베이스 내의 테이블에 저장 hello를 사용 하 여 Azure tooload 데이터 [CREATE TABLE AS SELECT (Transact SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] 문. CTAS에는 포함 된 로드 활용 하 여 hello 강력한 형식의 정당한 created.tooload hello 데이터를 새 테이블에 있는 외부 테이블 하나를 사용 하십시오 [CTAS] [ CTAS] 테이블당 문입니다. 
 
CTAS에는 새 테이블을 만들고을 select 문의 hello 결과 함께 채웁니다. CTAS에는 새 테이블 toohave hello 정의의 hello hello 결과 select 문 처럼 동일한 열과 데이터 형식을 hello 합니다. 외부 테이블에서 모든 hello 열을 선택 하면 hello 새 테이블에 hello 외부 테이블의 hello 열과 데이터 형식을의 복제본이 됩니다.

이 예제에서는 hello 차원과 hello 팩트 테이블 분산된 테이블 해시로 만듭니다. 

```sql
SELECT GETDATE();
GO

CREATE TABLE [cso].[DimProduct]            WITH (DISTRIBUTION = HASH([ProductKey]  ) ) AS SELECT * FROM [asb].[DimProduct]             OPTION (LABEL = 'CTAS : Load [cso].[DimProduct]             ');
CREATE TABLE [cso].[FactOnlineSales]       WITH (DISTRIBUTION = HASH([ProductKey]  ) ) AS SELECT * FROM [asb].[FactOnlineSales]        OPTION (LABEL = 'CTAS : Load [cso].[FactOnlineSales]        ');
```

### <a name="43-track-hello-load-progress"></a>4.3 hello 부하 진행률 추적
동적 관리 뷰 (Dmv)를 사용 하 여 부하의 hello 진행률을 추적할 수 있습니다. 

```sql
-- toosee all requests
SELECT * FROM sys.dm_pdw_exec_requests;

-- toosee a particular request identified by its label
SELECT * FROM sys.dm_pdw_exec_requests as r
WHERE r.[label] = 'CTAS : Load [cso].[DimProduct]             '
      OR r.[label] = 'CTAS : Load [cso].[FactOnlineSales]        '
;

-- tootrack bytes and files
SELECT
    r.command,
    s.request_id,
    r.status,
    count(distinct input_name) as nbr_files, 
    sum(s.bytes_processed)/1024/1024/1024 as gb_processed
FROM
    sys.dm_pdw_exec_requests r
    inner join sys.dm_pdw_dms_external_work s
        on r.request_id = s.request_id
WHERE 
    r.[label] = 'CTAS : Load [cso].[DimProduct]             '
    OR r.[label] = 'CTAS : Load [cso].[FactOnlineSales]        '
GROUP BY
    r.command,
    s.request_id,
    r.status
ORDER BY
    nbr_files desc,
    gb_processed desc;
```

## <a name="5-optimize-columnstore-compression"></a>5. Columnstore 압축을 최적화합니다.
기본적으로 SQL 데이터 웨어하우스는 hello 테이블을 클러스터형된 columnstore 인덱스로 저장합니다. 로드를 완료 한 후 일부 hello 데이터 행 수 압축 되지 hello columnstore에 합니다.  여기에는 다양한 이유가 있습니다. toolearn 더 참조 [columnstore 인덱스 관리][manage columnstore indexes]합니다.

toooptimize 쿼리 성능 및 columnstore 압축 하 여 로드 한 후 모든 hello 행 hello 테이블 tooforce hello columnstore 인덱스 toocompress를 다시 작성 합니다. 

```sql
SELECT GETDATE();
GO

ALTER INDEX ALL ON [cso].[DimProduct]               REBUILD;
ALTER INDEX ALL ON [cso].[FactOnlineSales]          REBUILD;
```

Columnstore 인덱스 유지 관리에 대 한 자세한 내용은 참조 hello [columnstore 인덱스 관리] [ manage columnstore indexes] 문서.

## <a name="6-optimize-statistics"></a>6. 통계를 최적화합니다.
부하 후 즉시 최상의 toocreate 단일 열 통계에는 다른 합니다. 통계에 대한 몇 가지 선택 사항이 있습니다. 예를 들어 모든 열에 단일 열 통계를 만드는 경우 걸릴 수 있습니다는 오랜 시간이 toorebuild 모든 hello 통계. 특정 열 쿼리 조건자의 toobe 것을 알고 있는 경우 해당 열에 만드는 통계를 건너뛸 수 있습니다.

모든 테이블의 모든 열에 단일 열 통계 toocreate 결정 한 경우에 hello 저장된 프로시저 코드 샘플을 사용할 수 있습니다 `prc_sqldw_create_stats` hello에 [통계] [ statistics] 문서.

다음 예제는 hello은 통계를 만들기 위한 좋은 시작 지점입니다. Hello 팩트 테이블에 각 조인 열 및 hello 차원 테이블의 각 열에 단일 열 통계를 만듭니다. 항상 단일 또는 여러 열 통계 tooother 팩트 테이블 열을 나중에 추가할 수 있습니다.

```sql
CREATE STATISTICS [stat_cso_DimProduct_AvailableForSaleDate] ON [cso].[DimProduct]([AvailableForSaleDate]);
CREATE STATISTICS [stat_cso_DimProduct_BrandName] ON [cso].[DimProduct]([BrandName]);
CREATE STATISTICS [stat_cso_DimProduct_ClassID] ON [cso].[DimProduct]([ClassID]);
CREATE STATISTICS [stat_cso_DimProduct_ClassName] ON [cso].[DimProduct]([ClassName]);
CREATE STATISTICS [stat_cso_DimProduct_ColorID] ON [cso].[DimProduct]([ColorID]);
CREATE STATISTICS [stat_cso_DimProduct_ColorName] ON [cso].[DimProduct]([ColorName]);
CREATE STATISTICS [stat_cso_DimProduct_ETLLoadID] ON [cso].[DimProduct]([ETLLoadID]);
CREATE STATISTICS [stat_cso_DimProduct_ImageURL] ON [cso].[DimProduct]([ImageURL]);
CREATE STATISTICS [stat_cso_DimProduct_LoadDate] ON [cso].[DimProduct]([LoadDate]);
CREATE STATISTICS [stat_cso_DimProduct_Manufacturer] ON [cso].[DimProduct]([Manufacturer]);
CREATE STATISTICS [stat_cso_DimProduct_ProductDescription] ON [cso].[DimProduct]([ProductDescription]);
CREATE STATISTICS [stat_cso_DimProduct_ProductKey] ON [cso].[DimProduct]([ProductKey]);
CREATE STATISTICS [stat_cso_DimProduct_ProductLabel] ON [cso].[DimProduct]([ProductLabel]);
CREATE STATISTICS [stat_cso_DimProduct_ProductName] ON [cso].[DimProduct]([ProductName]);
CREATE STATISTICS [stat_cso_DimProduct_ProductSubcategoryKey] ON [cso].[DimProduct]([ProductSubcategoryKey]);
CREATE STATISTICS [stat_cso_DimProduct_ProductURL] ON [cso].[DimProduct]([ProductURL]);
CREATE STATISTICS [stat_cso_DimProduct_Size] ON [cso].[DimProduct]([Size]);
CREATE STATISTICS [stat_cso_DimProduct_SizeRange] ON [cso].[DimProduct]([SizeRange]);
CREATE STATISTICS [stat_cso_DimProduct_SizeUnitMeasureID] ON [cso].[DimProduct]([SizeUnitMeasureID]);
CREATE STATISTICS [stat_cso_DimProduct_Status] ON [cso].[DimProduct]([Status]);
CREATE STATISTICS [stat_cso_DimProduct_StockTypeID] ON [cso].[DimProduct]([StockTypeID]);
CREATE STATISTICS [stat_cso_DimProduct_StockTypeName] ON [cso].[DimProduct]([StockTypeName]);
CREATE STATISTICS [stat_cso_DimProduct_StopSaleDate] ON [cso].[DimProduct]([StopSaleDate]);
CREATE STATISTICS [stat_cso_DimProduct_StyleID] ON [cso].[DimProduct]([StyleID]);
CREATE STATISTICS [stat_cso_DimProduct_StyleName] ON [cso].[DimProduct]([StyleName]);
CREATE STATISTICS [stat_cso_DimProduct_UnitCost] ON [cso].[DimProduct]([UnitCost]);
CREATE STATISTICS [stat_cso_DimProduct_UnitOfMeasureID] ON [cso].[DimProduct]([UnitOfMeasureID]);
CREATE STATISTICS [stat_cso_DimProduct_UnitOfMeasureName] ON [cso].[DimProduct]([UnitOfMeasureName]);
CREATE STATISTICS [stat_cso_DimProduct_UnitPrice] ON [cso].[DimProduct]([UnitPrice]);
CREATE STATISTICS [stat_cso_DimProduct_UpdateDate] ON [cso].[DimProduct]([UpdateDate]);
CREATE STATISTICS [stat_cso_DimProduct_Weight] ON [cso].[DimProduct]([Weight]);
CREATE STATISTICS [stat_cso_DimProduct_WeightUnitMeasureID] ON [cso].[DimProduct]([WeightUnitMeasureID]);
CREATE STATISTICS [stat_cso_FactOnlineSales_CurrencyKey] ON [cso].[FactOnlineSales]([CurrencyKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_CustomerKey] ON [cso].[FactOnlineSales]([CustomerKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_DateKey] ON [cso].[FactOnlineSales]([DateKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_OnlineSalesKey] ON [cso].[FactOnlineSales]([OnlineSalesKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_ProductKey] ON [cso].[FactOnlineSales]([ProductKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_PromotionKey] ON [cso].[FactOnlineSales]([PromotionKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_StoreKey] ON [cso].[FactOnlineSales]([StoreKey]);
```

## <a name="achievement-unlocked"></a>목표를 달성했습니다!
이제 Azure SQL 데이터 웨어하우스에 공용 데이터를 성공적으로 로드했습니다. 잘 하셨습니다!

이제 hello 다음과 같은 쿼리를 사용 하 여 hello 테이블 쿼리를 시작할 수 있습니다.

```sql
SELECT  SUM(f.[SalesAmount]) AS [sales_by_brand_amount]
,       p.[BrandName]
FROM    [cso].[FactOnlineSales] AS f
JOIN    [cso].[DimProduct]      AS p ON f.[ProductKey] = p.[ProductKey]
GROUP BY p.[BrandName]
```

## <a name="next-steps"></a>다음 단계
tooload hello 전체 Contoso 소매 데이터 웨어하우스의 데이터에서 hello 스크립트를 사용 하 여 더 많은 개발 팁에 대 한 참조 하십시오. [SQL 데이터 웨어하우스 개발 개요][SQL Data Warehouse development overview]합니다.

<!--Image references-->

<!--Article references-->
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Load data into SQL Data Warehouse]: sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: sql-data-warehouse-overview-develop.md
[manage columnstore indexes]: sql-data-warehouse-tables-index.md
[Statistics]: sql-data-warehouse-tables-statistics.md
[CTAS]: sql-data-warehouse-develop-ctas.md
[label]: sql-data-warehouse-develop-label.md

<!--MSDN references-->
[CREATE EXTERNAL DATA SOURCE]: https://msdn.microsoft.com/en-us/library/dn935022.aspx
[CREATE EXTERNAL FILE FORMAT]: https://msdn.microsoft.com/en-us/library/dn935026.aspx
[CREATE TABLE AS SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/mt204041.aspx
[sys.dm_pdw_exec_requests]: https://msdn.microsoft.com/library/mt203887.aspx
[REBUILD]: https://msdn.microsoft.com/library/ms188388.aspx

<!--Other Web references-->
[Microsoft Download Center]: http://www.microsoft.com/download/details.aspx?id=36433
[Load hello full Contoso Retail Data Warehouse]: https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/contoso-data-warehouse/readme.md

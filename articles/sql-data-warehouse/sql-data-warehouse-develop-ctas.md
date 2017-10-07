---
title: "SQL 데이터 웨어하우스에 (CTAS) 선택 aaaCreate 테이블 | Microsoft Docs"
description: "Hello를 사용 하 여 코딩 하기 위한 팁 솔루션 개발을 위한 Azure SQL 데이터 웨어하우스에 (CTAS) 문을 선택 하는 테이블을 만듭니다."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: 68ac9a94-09f9-424b-b536-06a125a653bd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: queries
ms.date: 01/30/2017
ms.author: shigu;barbkess
ms.openlocfilehash: e381601a0a4d94e189d8f9115bf2e7593025410b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-table-as-select-ctas-in-sql-data-warehouse"></a>SQL 데이터 웨어하우스의 CTAS(Create Table As Select)
Select는 테이블 만들기 또는 `CTAS` 사용할 수 있는 가장 중요 한 T-SQL 기능 hello 중 하나입니다. SELECT 문의 hello 출력에 따라 새 테이블을 만드는 완벽 하 게 병렬화 된 연산입니다. `CTAS`hello 간단 하 고 가장 빠른 방법은 toocreate 테이블의 복사본입니다. 이 문서는 `CTAS`에 대한 예제와 모범 사례를 모두 제공합니다.

## <a name="selectinto-vs-ctas"></a>SELECT..INTO 및 CTAS
`CTAS`는 `SELECT..INTO`의 매우 강력한 버전으로 간주할 수 있습니다.

다음은 간단한 `SELECT..INTO` 문의 예제입니다.

```sql
SELECT *
INTO    [dbo].[FactInternetSales_new]
FROM    [dbo].[FactInternetSales]
```

위의 hello 예제에서 `[dbo].[FactInternetSales_new]` 이러한 방화벽은 Azure SQL 데이터 웨어하우스에 hello 테이블 기본값에 클러스터형 COLUMNSTORE 인덱스와 ROUND_ROBIN 분산 테이블로 만들 수 있습니다.

`SELECT..INTO`그러나 없도록 하면 toochange hello 배포 메서드나 hello 인덱스 hello 작업의 일환으로 입력 합니다. 여기는 `CTAS`이 들어오는 곳입니다.

tooconvert 너무 위에 hello`CTAS` 은 매우 간단 합니다.

```sql
CREATE TABLE [dbo].[FactInternetSales_new]
WITH
(
    DISTRIBUTION = ROUND_ROBIN
,   CLUSTERED COLUMNSTORE INDEX
)
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
;
```

와 `CTAS` 수 toochange는 hello 테이블 형식 뿐 아니라 hello 테이블 데이터의 분포를 hello 둘 다 합니다. 

> [!NOTE]
> Toochange hello 인덱스에만 하려는 경우 프로그램 `CTAS` 작업과 hello 원본 테이블은 해시 distributed 않다면 `CTAS` 작업을 수행 합니다 유지 하는 경우 가장 hello 같은 배포 열과 데이터 유형입니다. 이렇게 하면 배포 데이터 이동 크로스 보다 효과적인 hello 작업 중 필요가 없습니다.
> 
> 

## <a name="using-ctas-toocopy-a-table"></a>CTAS toocopy 테이블을 사용 하 여
아마도 가장 일반적인 hello 중 하나 사용 하 여의 `CTAS` hello DDL을 변경할 수 있도록 테이블의 복사본을 만드는 것입니다. 예를 들어 처음에 만든으로 테이블 경우 `ROUND_ROBIN` tooa 테이블 열에 배포 하려는 변경 이제 `CTAS` 는 어떻게 hello 배포 열을 변경할 수 있습니다. `CTAS`사용 되는 toochange 분할 인덱싱 또는 열 형식이 될 수도 있습니다.

기본 배포 유형 hello를 사용 하 여이 테이블을 만든 경우를 가정해 `ROUND_ROBIN` 배포 열이 없는 hello에 지정 된 이후 distributed `CREATE TABLE`합니다.

```sql
CREATE TABLE FactInternetSales
(
    ProductKey int NOT NULL,
    OrderDateKey int NOT NULL,
    DueDateKey int NOT NULL,
    ShipDateKey int NOT NULL,
    CustomerKey int NOT NULL,
    PromotionKey int NOT NULL,
    CurrencyKey int NOT NULL,
    SalesTerritoryKey int NOT NULL,
    SalesOrderNumber nvarchar(20) NOT NULL,
    SalesOrderLineNumber tinyint NOT NULL,
    RevisionNumber tinyint NOT NULL,
    OrderQuantity smallint NOT NULL,
    UnitPrice money NOT NULL,
    ExtendedAmount money NOT NULL,
    UnitPriceDiscountPct float NOT NULL,
    DiscountAmount float NOT NULL,
    ProductStandardCost money NOT NULL,
    TotalProductCost money NOT NULL,
    SalesAmount money NOT NULL,
    TaxAmt money NOT NULL,
    Freight money NOT NULL,
    CarrierTrackingNumber nvarchar(25),
    CustomerPONumber nvarchar(25)
);
```

이제 원하는 toocreate 클러스터형 Columnstore 인덱스와이 테이블의 새 복사본의 Clustered Columnstore 테이블의 hello 성능 이용할 수 있도록 합니다. 또한 원하는 toodistribute ProductKey에서이 테이블과이 열에서 조인을 지정 해야 하 고 데이터 이동 tooavoid ProductKey에 조인 하는 동안 원하는 합니다. 마지막으로 원하는 기존 파티션을 삭제 하 여 오래 된 데이터를 신속 하 게 삭제할 수 있도록 tooadd OrderDateKey에서 분할 합니다. 다음은 이전 테이블에 새 테이블로 복사 하는 hello CTAS에는 문이입니다.

```sql
CREATE TABLE FactInternetSales_new
WITH
(
    CLUSTERED COLUMNSTORE INDEX,
    DISTRIBUTION = HASH(ProductKey),
    PARTITION
    (
        OrderDateKey RANGE RIGHT FOR VALUES
        (
        20000101,20010101,20020101,20030101,20040101,20050101,20060101,20070101,20080101,20090101,
        20100101,20110101,20120101,20130101,20140101,20150101,20160101,20170101,20180101,20190101,
        20200101,20210101,20220101,20230101,20240101,20250101,20260101,20270101,20280101,20290101
        )
    )
)
AS SELECT * FROM FactInternetSales;
```

마지막으로 테이블 tooswap 새 테이블의 이름을 바꿀 수 있으며 다음 이전 테이블을 삭제할 수 있습니다.

```sql
RENAME OBJECT FactInternetSales tooFactInternetSales_old;
RENAME OBJECT FactInternetSales_new tooFactInternetSales;

DROP TABLE FactInternetSales_old;
```

> [!NOTE]
> Azure SQL 데이터 웨어하우스는 자동 만들기 또는 통계 자동 업데이트를 아직 지원하지 않습니다.  순서 tooget hello 최상의 성능을 얻으려면 쿼리에서 것이 중요 통계 hello 첫 번째 로드 한 후 모든 테이블의 모든 열에 만들 수 또는 hello 데이터에서 발생 된 모든 주요 부분을 변경 합니다.  통계에 대 한 자세한 내용은 참조 hello [통계] [ Statistics] hello 개발 그룹 항목의 항목입니다.
> 
> 

## <a name="using-ctas-toowork-around-unsupported-features"></a>지원 되지 않는 기능 주위 CTAS toowork를 사용 하 여
`CTAS`다양 한 아래에 나열 된 지원 되지 않는 hello 기능 주위에 사용 되는 toowork 될 수도 있습니다. 이 종종 증명할 수 toobe 쌍방 상황 뿐만 아니라 코드 됩니다 규정을 준수 하지만 SQL 데이터 웨어하우스에 대 한 더 빠르게 실행 종종 됩니다. 이는 완전히 병렬화된 디자인의 결과입니다. CTAS로 해결할 수 있는 시나리오는 다음과 같습니다.

* UPDATE에 대한 ANSI JOINS
* DELETE에 대한 ANSI JOIN
* MERGE 문

> [!NOTE]
> 시도 toothink "CTAS에는 첫 번째"입니다. 사용 하 여 문제를 해결할 수 있다고 생각 되 면 `CTAS` hello 가장 좋은 방법은 tooapproach는 일반적으로 다음 그-결과적으로 더 많은 데이터를 작성 하는 경우에 마찬가지입니다.
> 
> 

## <a name="ansi-join-replacement-for-update-statements"></a>Update 문에 대한 ANSI 조인 대체
ANSI 조인 구문을 tooperform hello를 사용 하 여 함께 업데이트 또는 삭제 하는 두 개 이상의 테이블을 조인 하는 복잡 한 업데이트가 있는 알 수 있습니다.

이 테이블 tooupdate 했습니다 같이 가정해 봅니다.

```sql
CREATE TABLE [dbo].[AnnualCategorySales]
(    [EnglishProductCategoryName]    NVARCHAR(50)    NOT NULL
,    [CalendarYear]                    SMALLINT        NOT NULL
,    [TotalSalesAmount]                MONEY            NOT NULL
)
WITH
(
    DISTRIBUTION = ROUND_ROBIN
)
;
```

hello 원래 쿼리 다음과 같이 보지 못했을 수 있습니다.

```sql
UPDATE    acs
SET        [TotalSalesAmount] = [fis].[TotalSalesAmount]
FROM    [dbo].[AnnualCategorySales]     AS acs
JOIN    (
        SELECT    [EnglishProductCategoryName]
        ,        [CalendarYear]
        ,        SUM([SalesAmount])                AS [TotalSalesAmount]
        FROM    [dbo].[FactInternetSales]        AS s
        JOIN    [dbo].[DimDate]                    AS d    ON s.[OrderDateKey]                = d.[DateKey]
        JOIN    [dbo].[DimProduct]                AS p    ON s.[ProductKey]                = p.[ProductKey]
        JOIN    [dbo].[DimProductSubCategory]    AS u    ON p.[ProductSubcategoryKey]    = u.[ProductSubcategoryKey]
        JOIN    [dbo].[DimProductCategory]        AS c    ON u.[ProductCategoryKey]        = c.[ProductCategoryKey]
        WHERE     [CalendarYear] = 2004
        GROUP BY
                [EnglishProductCategoryName]
        ,        [CalendarYear]
        ) AS fis
ON    [acs].[EnglishProductCategoryName]    = [fis].[EnglishProductCategoryName]
AND    [acs].[CalendarYear]                = [fis].[CalendarYear]
;
```

ANSI 조인 hello에 SQL 데이터 웨어하우스를 지원 하지 않으므로 `FROM` 절은 `UPDATE` 문, 약간 변경 하지 않고 위에이 코드를 복사할 수 없습니다.

조합을 사용할 수 있습니다는 `CTAS` 및 암시적 tooreplace이이 코드를 조인 합니다.

```sql
-- Create an interim table
CREATE TABLE CTAS_acs
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT    ISNULL(CAST([EnglishProductCategoryName] AS NVARCHAR(50)),0)    AS [EnglishProductCategoryName]
,        ISNULL(CAST([CalendarYear] AS SMALLINT),0)                         AS [CalendarYear]
,        ISNULL(CAST(SUM([SalesAmount]) AS MONEY),0)                        AS [TotalSalesAmount]
FROM    [dbo].[FactInternetSales]        AS s
JOIN    [dbo].[DimDate]                    AS d    ON s.[OrderDateKey]                = d.[DateKey]
JOIN    [dbo].[DimProduct]                AS p    ON s.[ProductKey]                = p.[ProductKey]
JOIN    [dbo].[DimProductSubCategory]    AS u    ON p.[ProductSubcategoryKey]    = u.[ProductSubcategoryKey]
JOIN    [dbo].[DimProductCategory]        AS c    ON u.[ProductCategoryKey]        = c.[ProductCategoryKey]
WHERE     [CalendarYear] = 2004
GROUP BY
        [EnglishProductCategoryName]
,        [CalendarYear]
;

-- Use an implicit join tooperform hello update
UPDATE  AnnualCategorySales
SET     AnnualCategorySales.TotalSalesAmount = CTAS_ACS.TotalSalesAmount
FROM    CTAS_acs
WHERE   CTAS_acs.[EnglishProductCategoryName] = AnnualCategorySales.[EnglishProductCategoryName]
AND     CTAS_acs.[CalendarYear]               = AnnualCategorySales.[CalendarYear]
;

--Drop hello interim table
DROP TABLE CTAS_acs
;
```

## <a name="ansi-join-replacement-for-delete-statements"></a>Delete 문에 대한 ANSI 조인 대체
경우에 따라 데이터를 삭제 하기 위한 가장 좋은 방법이 hello는 toouse `CTAS`합니다. 단순히 hello 데이터를 삭제 하는 대신 tookeep 원하는 hello 데이터를 선택 합니다. 이 경우에 특히 유용 `DELETE` ansi SQL 데이터 웨어하우스 hello에 ANSI 조인을 지원 하지 않으므로 구문 조인를 사용 하는 문을 `FROM` 절은 `DELETE` 문.

변환된 DELETE 문의 예를 아래에서 볼 수 있습니다.

```sql
CREATE TABLE dbo.DimProduct_upsert
WITH
(   Distribution=HASH(ProductKey)
,   CLUSTERED INDEX (ProductKey)
)
AS -- Select Data you wish tookeep
SELECT     p.ProductKey
,          p.EnglishProductName
,          p.Color
FROM       dbo.DimProduct p
RIGHT JOIN dbo.stg_DimProduct s
ON         p.ProductKey = s.ProductKey
;

RENAME OBJECT dbo.DimProduct        tooDimProduct_old;
RENAME OBJECT dbo.DimProduct_upsert tooDimProduct;
```

## <a name="replace-merge-statements"></a>Merge 문 대체
`CTAS`를 사용하면 Merge 문을 최소한 부분적으로는 대체할 수 있습니다. Hello를 통합할 수 `INSERT` 및 hello `UPDATE` 단일 문으로 합니다. 삭제 된 데이터는 두 번째 문에 오프 닫힌 toobe를 해야 합니다.

`UPSERT` 의 예를 아래에서 볼 수 있습니다.

```sql
CREATE TABLE dbo.[DimProduct_upsert]
WITH
(   DISTRIBUTION = HASH([ProductKey])
,   CLUSTERED INDEX ([ProductKey])
)
AS
-- New rows and new versions of rows
SELECT      s.[ProductKey]
,           s.[EnglishProductName]
,           s.[Color]
FROM      dbo.[stg_DimProduct] AS s
UNION ALL  
-- Keep rows that are not being touched
SELECT      p.[ProductKey]
,           p.[EnglishProductName]
,           p.[Color]
FROM      dbo.[DimProduct] AS p
WHERE NOT EXISTS
(   SELECT  *
    FROM    [dbo].[stg_DimProduct] s
    WHERE   s.[ProductKey] = p.[ProductKey]
)
;

RENAME OBJECT dbo.[DimProduct]          too[DimProduct_old];
RENAME OBJECT dbo.[DimpProduct_upsert]  too[DimProduct];

```

## <a name="ctas-recommendation-explicitly-state-data-type-and-nullability-of-output"></a>CTAS 권장 사항: 데이터 형식 및 출력의 null 허용 여부를 명시적으로 지정
코드를 마이그레이션하는 경우 이 유형의 코딩 패턴을 볼 수 있습니다.

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455

CREATE TABLE result
(result DECIMAL(7,2) NOT NULL
)
WITH (DISTRIBUTION = ROUND_ROBIN)

INSERT INTO result
SELECT @d*@f
;
```

Instinctively이 코드 tooa CTAS에 마이그레이션해야 하 고 올바른는 생각할 수 있습니다. 그러나 여기에는 숨겨진 문제가 있습니다.

hello 다음 코드를 생성 하지 않습니다 동일한 결과 hello:

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455
;

CREATE TABLE ctas_r
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT @d*@f as result
;
```

Hello 열 "result" hello 데이터 형식 및 null 허용 여부 값 hello 식의 앞으로 수행을 확인 합니다. 주의 하지 않은 경우 toosubtle 차이 값에서 발생할 수 있습니다.

예를 들어 hello 다음을 시도해 보십시오.

```sql
SELECT result,result*@d
from result
;

SELECT result,result*@d
from ctas_r
;
```

결과 대해 저장 된 hello 값은 다릅니다. Hello hello 결과 열에 지 속성 값이 사용 되는 또 다른 식 hello 오류 훨씬 더 중요 한 됩니다.

![][1]

데이터 마이그레이션의 경우 이 값이 특히 중요합니다. Hello 두 번째 쿼리는 풀링할 때 보다 정확 하 게 하는 경우에 문제가 있습니다. hello 데이터는 다른 비교 toohello 소스 시스템와 hello 마이그레이션에서 tooquestions의 무결성을 유발 하는 합니다. 드문 경우 지만 hello "잘못 된" 응답 hello 오른쪽으로 실제로 한이 중 하나입니다!

hello hello 두 결과 간의이 차이 보면 원인은 tooimplicit 아래로 캐스팅을 입력 합니다. Hello hello 테이블의 첫 번째 예는 hello 열 정의 정의합니다. Hello 행이 삽입 될 때 암시적 형식 변환이 발생 합니다. 두 번째 예에서는 hello 즉 암시적 형식 변환 작업 없이 hello 식 hello 열의 데이터 형식을 정의 하는 대로 있습니다. 또한 hello 두 번째 예제에서 해당 hello 열으로 정의 된 null 허용 열 반면 하지 않았으면 hello 첫 번째 예제를 확인 합니다. Hello 테이블에서 만들어진 경우 hello 첫 번째 예에서는 열의 null 허용 여부가 명시적으로 정의 되었습니다. Hello 두 번째 예제에서 것 바로 두었습니다 toohello 식 및 기본적으로이 결과로 NULL 정의 합니다.  

이러한 문제는 tooresolve 명시적으로 설정 해야 hello 형식 변환 및 null 허용 여부 hello에 `SELECT` hello 부분의 `CTAS` 문. 설정할 수는 없습니다 hello에서 속성 표 파트를 만듭니다.

다음 예제에서는 hello toofix 코드 hello 하는 방법을 보여 줍니다.

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455

CREATE TABLE ctas_r
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT ISNULL(CAST(@d*@f AS DECIMAL(7,2)),0) as result
```

참고 hello 다음.

* CAST 또는 CONVERT가 사용되었을 수 있습니다.
* ISNULL은 사용 되는 tooforce 하지 COALESCE null 허용 여부
* ISNULL은 hello 가장 바깥쪽 함수
* hello ISNULL의 두 번째 부분 hello는 상수, 즉 0

> [!NOTE]
> Hello null 허용 여부 toobe 올바르게 설정에 대 한 중요 한 toouse 않습니다 `ISNULL` 아닌 `COALESCE`합니다. `COALESCE`결정적 함수 아니며 하므로 hello 식의 결과 hello은 항상 null을 허용 합니다. `ISNULL`은 다릅니다. 이는 결정적입니다. 따라서 두 번째 부분은 hello 때 hello `ISNULL` 상수 또는 리터럴 함수는 다음 hello 결과 값이 됩니다 NOT NULL입니다.
> 
> 

이 팁 방금 유용 계산의 hello 무결성을 보장 하지 않습니다. 테이블 파티션 전환을 위해서도 중요합니다. 이 테이블을 사용자의 실제 정보로 정의했다고 가정해 보겠습니다.

```sql
CREATE TABLE [dbo].[Sales]
(
    [date]      INT     NOT NULL
,   [product]   INT     NOT NULL
,   [store]     INT     NOT NULL
,   [quantity]  INT     NOT NULL
,   [price]     MONEY   NOT NULL
,   [amount]    MONEY   NOT NULL
)
WITH
(   DISTRIBUTION = HASH([product])
,   PARTITION   (   [date] RANGE RIGHT FOR VALUES
                    (20000101,20010101,20020101
                    ,20030101,20040101,20050101
                    )
                )
)
;
```

그러나 hello 값 필드는 계산된 식 hello 원본 데이터에 속하지 않습니다.

toocreate 분할 된 데이터 집합이 toodo를 할 수 있습니다.

```sql
CREATE TABLE [dbo].[Sales_in]
WITH    
(   DISTRIBUTION = HASH([product])
,   PARTITION   (   [date] RANGE RIGHT FOR VALUES
                    (20000101,20010101
                    )
                )
)
AS
SELECT
    [date]    
,   [product]
,   [store]
,   [quantity]
,   [price]   
,   [quantity]*[price]  AS [amount]
FROM [stg].[source]
OPTION (LABEL = 'CTAS : Partition IN table : Create')
;
```

hello 쿼리는 완벽 하 게 제대로 실행 됩니다. hello 문제가 tooperform hello 파티션 전환 려 할 때 발생 합니다. hello 테이블 정의와 일치 하지 않습니다. toomake hello 테이블 정의 CTAS toobe 수정 해야 하는 hello와 일치 합니다.

```sql
CREATE TABLE [dbo].[Sales_in]
WITH    
(   DISTRIBUTION = HASH([product])
,   PARTITION   (   [date] RANGE RIGHT FOR VALUES
                    (20000101,20010101
                    )
                )
)
AS
SELECT
    [date]    
,   [product]
,   [store]
,   [quantity]
,   [price]   
,   ISNULL(CAST([quantity]*[price] AS MONEY),0) AS [amount]
FROM [stg].[source]
OPTION (LABEL = 'CTAS : Partition IN table : Create');
```

따라서 CTAS에 대한 형식 일관성 및 null 허용 여부 속성 유지가 좋은 엔지니어링 모범 사례임을 알 수 있습니다. 계산에서 toomaintain 무결성 주며 갖는지도 확인 된 파티션 전환을 합니다.

사용 하 여 대 한 자세한 내용은 tooMSDN를 참조 하십시오 [CTAS][CTAS]합니다. Azure SQL 데이터 웨어하우스 hello 가장 중요 한 문 중 하나입니다. 완전하게 이해해야 합니다.

## <a name="next-steps"></a>다음 단계
더 많은 개발 팁은 [개발 개요][development overview]를 참조하세요.

<!--Image references-->
[1]: media/sql-data-warehouse-develop-ctas/ctas-results.png

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->
[CTAS]: https://msdn.microsoft.com/library/mt204041.aspx

<!--Other Web references-->

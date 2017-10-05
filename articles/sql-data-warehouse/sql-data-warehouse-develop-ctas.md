---
title: "SQL Data Warehouse의 CTAS(Create Table As Select) | Microsoft Docs"
description: "솔루션 개발을 위해 Azure SQL 데이터 웨어하우스의 CTAS(Create Table As Select) 문으로 코딩에 대한 팁."
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
ms.openlocfilehash: cb08313726e8135feaa9b413937c2197ea397f4b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-table-as-select-ctas-in-sql-data-warehouse"></a><span data-ttu-id="4a9b2-103">SQL 데이터 웨어하우스의 CTAS(Create Table As Select)</span><span class="sxs-lookup"><span data-stu-id="4a9b2-103">Create Table As Select (CTAS) in SQL Data Warehouse</span></span>
<span data-ttu-id="4a9b2-104">`CTAS`(Create Table As Select)는 현재 제공되고 있는 가장 중요한 T-SQL 기능 중 하나이며,</span><span class="sxs-lookup"><span data-stu-id="4a9b2-104">Create table as select or `CTAS` is one of the most important T-SQL features available.</span></span> <span data-ttu-id="4a9b2-105">이는 SELECT 문의 출력을 기반으로 새 테이블을 만드는 완전하게 병렬화된 연산입니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-105">It is a fully parallelized operation that creates a new table based on the output of a SELECT statement.</span></span> <span data-ttu-id="4a9b2-106">`CTAS`는 테이블 사본을 만드는 가장 간단하고 빠른 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-106">`CTAS` is the simplest and fastest way to create a copy of a table.</span></span> <span data-ttu-id="4a9b2-107">이 문서는 `CTAS`에 대한 예제와 모범 사례를 모두 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-107">This document provides both examples and best practices for `CTAS`.</span></span>

## <a name="selectinto-vs-ctas"></a><span data-ttu-id="4a9b2-108">SELECT..INTO 및 CTAS</span><span class="sxs-lookup"><span data-stu-id="4a9b2-108">SELECT..INTO vs. CTAS</span></span>
<span data-ttu-id="4a9b2-109">`CTAS`는 `SELECT..INTO`의 매우 강력한 버전으로 간주할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-109">You can consider `CTAS` as a super-charged version of `SELECT..INTO`.</span></span>

<span data-ttu-id="4a9b2-110">다음은 간단한 `SELECT..INTO` 문의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-110">Below is an example of a simple `SELECT..INTO` statement:</span></span>

```sql
SELECT *
INTO    [dbo].[FactInternetSales_new]
FROM    [dbo].[FactInternetSales]
```

<span data-ttu-id="4a9b2-111">위의 예제에서 `[dbo].[FactInternetSales_new]`는 Azure SQL Data Warehouse의 테이블 기본값이므로 CLUSTERED COLUMNSTORE INDEX를 포함한 ROUND_ROBIN 분산 테이블로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-111">In the example above `[dbo].[FactInternetSales_new]` would be created as ROUND_ROBIN distributed table with a CLUSTERED COLUMNSTORE INDEX on it as these are the table defaults in Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="4a9b2-112">그러나 `SELECT..INTO`에서는 작업의 일부로 배포 메서드 또는 인덱스 유형을 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-112">`SELECT..INTO` however does not allow you to change either the distribution method or the index type as part of the operation.</span></span> <span data-ttu-id="4a9b2-113">여기는 `CTAS`이 들어오는 곳입니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-113">This is where `CTAS` comes in.</span></span>

<span data-ttu-id="4a9b2-114">위의 문을 `CTAS` 로 변환하는 것은 매우 간단합니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-114">To convert the above to `CTAS` is quite straight-forward:</span></span>

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

<span data-ttu-id="4a9b2-115">`CTAS`를 사용하면 테이블 형식뿐만 아니라 테이블 데이터의 배포도 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-115">With `CTAS` you are able to change both the distribution of the table data as well as the table type.</span></span> 

> [!NOTE]
> <span data-ttu-id="4a9b2-116">`CTAS` 작업에서 색인만 변경하려고 하고 원본 테이블이 해시로 배포되는 경우 동일한 배포 열과 데이터 형식을 유지하면 `CTAS` 작업이 가장 잘 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-116">If you are only trying to change the index in your `CTAS` operation and the source table is hash distributed then your `CTAS` operation will perform best if you maintain the same distribution column and data type.</span></span> <span data-ttu-id="4a9b2-117">이렇게 하면 보다 효율적으로 작업하는 동안 배포 간 데이터 이동을 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-117">This will avoid cross distribution data movement during the operation which is more efficient.</span></span>
> 
> 

## <a name="using-ctas-to-copy-a-table"></a><span data-ttu-id="4a9b2-118">CTAS를 사용하여 테이블 복사</span><span class="sxs-lookup"><span data-stu-id="4a9b2-118">Using CTAS to copy a table</span></span>
<span data-ttu-id="4a9b2-119">`CTAS` 는 DDL을 변경할 수 있도록 테이블 복사본을 만드는 데 가장 흔히 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-119">Perhaps one of the most common uses of `CTAS` is creating a copy of a table so that you can change the DDL.</span></span> <span data-ttu-id="4a9b2-120">예를 들어 원래 `ROUND_ROBIN`으로 테이블을 만들었는데 열에 배포된 테이블로 변경하고 싶다면, `CTAS`를 통해 배포 열을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-120">If for example you originally created your table as `ROUND_ROBIN` and now want change it to a table distributed on a column, `CTAS` is how you would change the distribution column.</span></span> <span data-ttu-id="4a9b2-121">`CTAS` 를 사용해 분할, 인덱싱 또는 열 유형도 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-121">`CTAS` can also be used to change partitioning, indexing, or column types.</span></span>

<span data-ttu-id="4a9b2-122">`CREATE TABLE`에서는 배포 열을 지정하지 않았으므로 기본 배포 유형인 `ROUND_ROBIN` 배포 방식을 사용하여 이 테이블을 만들었다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-122">Let's say you created this table using the default distribution type of `ROUND_ROBIN` distributed since no distribution column was specified in the `CREATE TABLE`.</span></span>

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

<span data-ttu-id="4a9b2-123">이제 클러스터형 Columnstore 테이블의 성능을 활용하기 위해 클러스터형 Columnstore 인덱스로 이 테이블의 사본을 만들고자 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-123">Now you want to create a new copy of this table with a Clustered Columnstore Index so that you can take advantage of the performance of Clustered Columnstore tables.</span></span> <span data-ttu-id="4a9b2-124">또한 이 테이블에 조인을 예상하기 때문에 테이블을 ProductKey로 배포하고자 하며 ProductKey에 조인하는 동안 데이터 이동을 피하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-124">You also want to distribute this table on ProductKey since you are anticipating joins on this column and want to avoid data movement during joins on ProductKey.</span></span> <span data-ttu-id="4a9b2-125">마지막으로 이전 파티션을 제거하여 이전 데이터를 빠르게 삭제할 수 있도록 OrderDateKey에 분할을 추가하고자 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-125">Lastly you also want to add partitioning on OrderDateKey so that you can quickly delete old data by dropping old partitions.</span></span> <span data-ttu-id="4a9b2-126">이전 테이블을 새 테이블로 복사하는 CTAS 문은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-126">Here is the CTAS statement which would copy your old table into a new table.</span></span>

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

<span data-ttu-id="4a9b2-127">이제 새 테이블을 교환해 넣고 이전 테이블을 제거하도록 테이블 이름을 변경할 수 있게 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-127">Finally you can rename your tables to swap in your new table and then drop your old table.</span></span>

```sql
RENAME OBJECT FactInternetSales TO FactInternetSales_old;
RENAME OBJECT FactInternetSales_new TO FactInternetSales;

DROP TABLE FactInternetSales_old;
```

> [!NOTE]
> <span data-ttu-id="4a9b2-128">Azure SQL 데이터 웨어하우스는 자동 만들기 또는 통계 자동 업데이트를 아직 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-128">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span>  <span data-ttu-id="4a9b2-129">쿼리에서 최상의 성능을 얻으려면, 데이터를 처음 로드하거나 데이터에 상당한 변화가 발생한 후에 모든 테이블의 모든 열에서 통계가 만들어지는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-129">In order to get the best performance from your queries, it's important that statistics be created on all columns of all tables after the first load or any substantial changes occur in the data.</span></span>  <span data-ttu-id="4a9b2-130">통계에 대한 자세한 설명은 개발 항목 그룹의 [통계][Statistics] 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-130">For a detailed explanation of statistics, see the [Statistics][Statistics] topic in the Develop group of topics.</span></span>
> 
> 

## <a name="using-ctas-to-work-around-unsupported-features"></a><span data-ttu-id="4a9b2-131">CTAS를 사용하여 지원되지 않는 기능 해결</span><span class="sxs-lookup"><span data-stu-id="4a9b2-131">Using CTAS to work around unsupported features</span></span>
<span data-ttu-id="4a9b2-132">`CTAS` 를 사용하면 아래에 나와 있는 여러 지원되지 않는 기능과 관련된 문제도 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-132">`CTAS` can also be used to work around a number of the unsupported features listed below.</span></span> <span data-ttu-id="4a9b2-133">많은 경우 이는 코드가 규정을 준수하면서도 SQL 데이터 웨어하우스에서 더 빠르게 실행되는 윈/윈 상황으로 입증될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-133">This can often prove to be a win/win situation as not only will your code be compliant but it will often execute faster on SQL Data Warehouse.</span></span> <span data-ttu-id="4a9b2-134">이는 완전히 병렬화된 디자인의 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-134">This is as a result of its fully parallelized design.</span></span> <span data-ttu-id="4a9b2-135">CTAS로 해결할 수 있는 시나리오는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-135">Scenarios that can be worked around with CTAS include:</span></span>

* <span data-ttu-id="4a9b2-136">UPDATE에 대한 ANSI JOINS</span><span class="sxs-lookup"><span data-stu-id="4a9b2-136">ANSI JOINS on UPDATEs</span></span>
* <span data-ttu-id="4a9b2-137">DELETE에 대한 ANSI JOIN</span><span class="sxs-lookup"><span data-stu-id="4a9b2-137">ANSI JOINs on DELETEs</span></span>
* <span data-ttu-id="4a9b2-138">MERGE 문</span><span class="sxs-lookup"><span data-stu-id="4a9b2-138">MERGE statement</span></span>

> [!NOTE]
> <span data-ttu-id="4a9b2-139">"CTAS를 먼저" 생각해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-139">Try to think "CTAS first".</span></span> <span data-ttu-id="4a9b2-140">`CTAS` 를 사용하여 문제를 해결할 수 있다면 그 결과로 더 많은 데이터를 작성하더라도 대개 CTAS를 사용하는 것이 가장 효율적인 문제 해결 방식입니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-140">If you think you can solve a problem using `CTAS` then that is generally the best way to approach it - even if you are writing more data as a result.</span></span>
> 
> 

## <a name="ansi-join-replacement-for-update-statements"></a><span data-ttu-id="4a9b2-141">Update 문에 대한 ANSI 조인 대체</span><span class="sxs-lookup"><span data-stu-id="4a9b2-141">ANSI join replacement for update statements</span></span>
<span data-ttu-id="4a9b2-142">UPDATE 또는 DELETE를 수행하기 위해 ANSI 조인 구문을 사용하여 둘 이상의 테이블을 조인하는 복잡한 업데이트가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-142">You may find you have a complex update that joins more than two tables together using ANSI joining syntax to perform the UPDATE or DELETE.</span></span>

<span data-ttu-id="4a9b2-143">이 테이블을 업데이트해야 한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-143">Imagine you had to update this table:</span></span>

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

<span data-ttu-id="4a9b2-144">원래 쿼리는 다음과 같을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-144">The original query might have looked something like this:</span></span>

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

<span data-ttu-id="4a9b2-145">SQL 데이터 웨어하우스는 `UPDATE` 문의 `FROM` 절에서 ANSI 조인을 지원하지 않으므로 이 코드를 약간 변경해야 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-145">Since SQL Data Warehouse does not support ANSI joins in the `FROM` clause of an `UPDATE` statement, you cannot copy this code over without changing it slightly.</span></span>

<span data-ttu-id="4a9b2-146">`CTAS` 와 암시적 조인의 조합을 사용하여 이 코드를 대체할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-146">You can use a combination of a `CTAS` and an implicit join to replace this code:</span></span>

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

-- Use an implicit join to perform the update
UPDATE  AnnualCategorySales
SET     AnnualCategorySales.TotalSalesAmount = CTAS_ACS.TotalSalesAmount
FROM    CTAS_acs
WHERE   CTAS_acs.[EnglishProductCategoryName] = AnnualCategorySales.[EnglishProductCategoryName]
AND     CTAS_acs.[CalendarYear]               = AnnualCategorySales.[CalendarYear]
;

--Drop the interim table
DROP TABLE CTAS_acs
;
```

## <a name="ansi-join-replacement-for-delete-statements"></a><span data-ttu-id="4a9b2-147">Delete 문에 대한 ANSI 조인 대체</span><span class="sxs-lookup"><span data-stu-id="4a9b2-147">ANSI join replacement for delete statements</span></span>
<span data-ttu-id="4a9b2-148">`CTAS`를 사용하여 데이터를 삭제하는 것이 최선의 방법인 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-148">Sometimes the best approach for deleting data is to use `CTAS`.</span></span> <span data-ttu-id="4a9b2-149">단순히 데이터를 삭제하는 대신 유지 하려는 데이터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-149">Rather than deleting the data simply select the data you want to keep.</span></span> <span data-ttu-id="4a9b2-150">ANSI 조인 구문을 사용하는 `DELETE` 문에서 이러한 방법을 사용하면 특히 유용합니다. SQL Data Warehouse는 `DELETE` 문의 `FROM` 절에서 ANSI 조인을 지원하지 않기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-150">This especially true for `DELETE` statements that use ansi joining syntax since SQL Data Warehouse does not support ANSI joins in the `FROM` clause of a `DELETE` statement.</span></span>

<span data-ttu-id="4a9b2-151">변환된 DELETE 문의 예를 아래에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-151">An example of a converted DELETE statement is available below:</span></span>

```sql
CREATE TABLE dbo.DimProduct_upsert
WITH
(   Distribution=HASH(ProductKey)
,   CLUSTERED INDEX (ProductKey)
)
AS -- Select Data you wish to keep
SELECT     p.ProductKey
,          p.EnglishProductName
,          p.Color
FROM       dbo.DimProduct p
RIGHT JOIN dbo.stg_DimProduct s
ON         p.ProductKey = s.ProductKey
;

RENAME OBJECT dbo.DimProduct        TO DimProduct_old;
RENAME OBJECT dbo.DimProduct_upsert TO DimProduct;
```

## <a name="replace-merge-statements"></a><span data-ttu-id="4a9b2-152">Merge 문 대체</span><span class="sxs-lookup"><span data-stu-id="4a9b2-152">Replace merge statements</span></span>
<span data-ttu-id="4a9b2-153">`CTAS`를 사용하면 Merge 문을 최소한 부분적으로는 대체할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-153">Merge statements can be replaced, at least in part, by using `CTAS`.</span></span> <span data-ttu-id="4a9b2-154">`INSERT` 및 `UPDATE`를 단일 문으로 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-154">You can consolidate the `INSERT` and the `UPDATE` into a single statement.</span></span> <span data-ttu-id="4a9b2-155">삭제된 모든 레코드를 두 번째 문에서 종료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-155">Any deleted records would need to be closed off in a second statement.</span></span>

<span data-ttu-id="4a9b2-156">`UPSERT` 의 예를 아래에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-156">An example of an `UPSERT` is available below:</span></span>

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

RENAME OBJECT dbo.[DimProduct]          TO [DimProduct_old];
RENAME OBJECT dbo.[DimpProduct_upsert]  TO [DimProduct];

```

## <a name="ctas-recommendation-explicitly-state-data-type-and-nullability-of-output"></a><span data-ttu-id="4a9b2-157">CTAS 권장 사항: 데이터 형식 및 출력의 null 허용 여부를 명시적으로 지정</span><span class="sxs-lookup"><span data-stu-id="4a9b2-157">CTAS recommendation: Explicitly state data type and nullability of output</span></span>
<span data-ttu-id="4a9b2-158">코드를 마이그레이션하는 경우 이 유형의 코딩 패턴을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-158">When migrating code you might find you run across this type of coding pattern:</span></span>

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

<span data-ttu-id="4a9b2-159">원래 이 코드를 CTAS로 마이그레이션해야 한다고 생각하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-159">Instinctively you might think you should migrate this code to a CTAS and you would be correct.</span></span> <span data-ttu-id="4a9b2-160">그러나 여기에는 숨겨진 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-160">However, there is a hidden issue here.</span></span>

<span data-ttu-id="4a9b2-161">다음 코드는 동일한 결과를 산출하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-161">The following code does NOT yield the same result:</span></span>

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

<span data-ttu-id="4a9b2-162">참고로 열 "결과"는 데이터 형식 및 식의 null 허용 여부 값을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-162">Notice that the column "result" carries forward the data type and nullability values of the expression.</span></span> <span data-ttu-id="4a9b2-163">이 때문에 주의하지 않으면 값에 미묘한 차이가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-163">This can lead to subtle variances in values if you aren't careful.</span></span>

<span data-ttu-id="4a9b2-164">한 예로 다음을 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-164">Try the following as an example:</span></span>

```sql
SELECT result,result*@d
from result
;

SELECT result,result*@d
from ctas_r
;
```

<span data-ttu-id="4a9b2-165">결과에 대해 저장된 값이 서로 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-165">The value stored for result is different.</span></span> <span data-ttu-id="4a9b2-166">결과 열에 유지되는 값은 다른 식에 사용되므로 오류가 훨씬 더 중요해집니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-166">As the persisted value in the result column is used in other expressions the error becomes even more significant.</span></span>

![][1]

<span data-ttu-id="4a9b2-167">데이터 마이그레이션의 경우 이 값이 특히 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-167">This is particularly important for data migrations.</span></span> <span data-ttu-id="4a9b2-168">두 번째 쿼리가 더 정확한 것은 분명하지만 한 가지 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-168">Even though the second query is arguably more accurate there is a problem.</span></span> <span data-ttu-id="4a9b2-169">데이터는 원본 시스템과 비교할 때 다를 수 있으며 따라서 마이그레이션에서 무결성 문제가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-169">The data would be different compared to the source system and that leads to questions of integrity in the migration.</span></span> <span data-ttu-id="4a9b2-170">이는 "잘못된" 답이 실제로 정답인 드문 경우 중 하나입니다!</span><span class="sxs-lookup"><span data-stu-id="4a9b2-170">This is one of those rare cases where the "wrong" answer is actually the right one!</span></span>

<span data-ttu-id="4a9b2-171">두 결과 사이의 이러한 차이가 발생하는 이유는 암시적 형식 캐스팅에 바탕을 두고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-171">The reason we see this disparity between the two results is down to implicit type casting.</span></span> <span data-ttu-id="4a9b2-172">첫 번째 예제에서는 테이블에 열 정의를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-172">In the first example the table defines the column definition.</span></span> <span data-ttu-id="4a9b2-173">행이 삽입될 때 암시적 형식 변환이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-173">When the row is inserted an implicit type conversion occurs.</span></span> <span data-ttu-id="4a9b2-174">두 번째 예제에서는 식이 해당 열의 데이터 형식을 정의하므로 암시적 형 변환이 발생하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-174">In the second example there is no implicit type conversion as the expression defines data type of the column.</span></span> <span data-ttu-id="4a9b2-175">또한 참고로 두 번째 예제의 열은 null 허용으로 정의된 반면에 첫 번째 예제는 그렇지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-175">Notice also that the column in the second example has been defined as a NULLable column whereas in the first example it has not.</span></span> <span data-ttu-id="4a9b2-176">첫 번째 예제에서는 테이블이 생성될 때 열의 null 허용 여부가 명시적으로 정의되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-176">When the table was created in the first example column nullability was explicitly defined.</span></span> <span data-ttu-id="4a9b2-177">두 번째 예제에서는 식을 그대로 두기만 했는데, 기본적으로 이렇게 하면 null 정의가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-177">In the second example it was just left to the expression and by default this would result in a NULL definition.</span></span>  

<span data-ttu-id="4a9b2-178">이러한 문제를 해결하려면 `CTAS` 문의 `SELECT` 부분에서 형식 변환 및 Null 허용 여부를 명시적으로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-178">To resolve these issues you must explicitly set the type conversion and nullability in the `SELECT` portion of the `CTAS` statement.</span></span> <span data-ttu-id="4a9b2-179">테이블 생성 부분에서는 이러한 속성을 설정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-179">You cannot set these properties in the create table part.</span></span>

<span data-ttu-id="4a9b2-180">아래 예제에서는 코드를 수정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-180">The example below demonstrates how to fix the code:</span></span>

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455

CREATE TABLE ctas_r
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT ISNULL(CAST(@d*@f AS DECIMAL(7,2)),0) as result
```

<span data-ttu-id="4a9b2-181">다음 사항에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-181">Note the following:</span></span>

* <span data-ttu-id="4a9b2-182">CAST 또는 CONVERT가 사용되었을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-182">CAST or CONVERT could have been used</span></span>
* <span data-ttu-id="4a9b2-183">ISNULL은 COALESCE가 아닌 null 허용 여부를 강제 적용하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-183">ISNULL is used to force NULLability not COALESCE</span></span>
* <span data-ttu-id="4a9b2-184">ISNULL은 가장 바깥쪽 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-184">ISNULL is the outermost function</span></span>
* <span data-ttu-id="4a9b2-185">ISNULL의 두 번째 부분은 상수, 즉 0입니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-185">The second part of the ISNULL is a constant i.e. 0</span></span>

> [!NOTE]
> <span data-ttu-id="4a9b2-186">null 허용 여부를 올바르게 설정하려면 `COALESCE`가 아닌 `ISNULL`을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-186">For the nullability to be correctly set it is vital to use `ISNULL` and not `COALESCE`.</span></span> <span data-ttu-id="4a9b2-187">`COALESCE`는 결정적 함수가 아니므로 식의 결과는 언제나 null을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-187">`COALESCE` is not a deterministic function and so the result of the expression will always be NULLable.</span></span> <span data-ttu-id="4a9b2-188">`ISNULL`은 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-188">`ISNULL` is different.</span></span> <span data-ttu-id="4a9b2-189">이는 결정적입니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-189">It is deterministic.</span></span> <span data-ttu-id="4a9b2-190">그러므로 `ISNULL` 함수의 두 번째 부분이 상수이거나 리터럴이면 결과 값은 NOT NULL이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-190">Therefore when the second part of the `ISNULL` function is a constant or a literal then the resulting value will be NOT NULL.</span></span>
> 
> 

<span data-ttu-id="4a9b2-191">이 팁은 계산의 무결성을 보장하기 위해 중요할 뿐만 아니라,</span><span class="sxs-lookup"><span data-stu-id="4a9b2-191">This tip is not just useful for ensuring the integrity of your calculations.</span></span> <span data-ttu-id="4a9b2-192">테이블 파티션 전환을 위해서도 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-192">It is also important for table partition switching.</span></span> <span data-ttu-id="4a9b2-193">이 테이블을 사용자의 실제 정보로 정의했다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-193">Imagine you have this table defined as your fact:</span></span>

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

<span data-ttu-id="4a9b2-194">그러나 값 필드는 원본 데이터의 일부가 아닌 계산된 식입니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-194">However, the value field is a calculated expression it is not part of the source data.</span></span>

<span data-ttu-id="4a9b2-195">분할된 데이터 집합을 만들려면 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-195">To create your partitioned dataset you might want to do this:</span></span>

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

<span data-ttu-id="4a9b2-196">쿼리는 전혀 문제 없이 실행될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-196">The query would run perfectly fine.</span></span> <span data-ttu-id="4a9b2-197">문제는 파티션 전환을 수행하려고 할 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-197">The problem comes when you try to perform the partition switch.</span></span> <span data-ttu-id="4a9b2-198">즉, 테이블 정의가 일치하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-198">The table definitions do not match.</span></span> <span data-ttu-id="4a9b2-199">테이블 정의를 일치시키려면 CTAS를 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-199">To make the table definitions match the CTAS needs to be modified.</span></span>

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

<span data-ttu-id="4a9b2-200">따라서 CTAS에 대한 형식 일관성 및 null 허용 여부 속성 유지가 좋은 엔지니어링 모범 사례임을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-200">You can see therefore that type consistency and maintaining nullability properties on a CTAS is a good engineering best practice.</span></span> <span data-ttu-id="4a9b2-201">이 방법은 계산의 무결성을 유지하는 데 도움이 되며 파티션 전환을 확실히 가능하게 해 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-201">It helps to maintain integrity in your calculations and also ensures that partition switching is possible.</span></span>

<span data-ttu-id="4a9b2-202">[CTAS][CTAS] 사용에 대한 자세한 내용은 MSDN을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-202">Please refer to MSDN for more information on using [CTAS][CTAS].</span></span> <span data-ttu-id="4a9b2-203">이는 Azure SQL 데이터 웨어하우스의 매우 중요한 문 중 하나이므로,</span><span class="sxs-lookup"><span data-stu-id="4a9b2-203">It is one of the most important statements in Azure SQL Data Warehouse.</span></span> <span data-ttu-id="4a9b2-204">완전하게 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-204">Make sure you thoroughly understand it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4a9b2-205">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4a9b2-205">Next steps</span></span>
<span data-ttu-id="4a9b2-206">더 많은 개발 팁은 [개발 개요][development overview]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4a9b2-206">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->
[1]: media/sql-data-warehouse-develop-ctas/ctas-results.png

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->
[CTAS]: https://msdn.microsoft.com/library/mt204041.aspx

<!--Other Web references-->

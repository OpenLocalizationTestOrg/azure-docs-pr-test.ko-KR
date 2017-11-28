---
title: "SQL 데이터 웨어하우스에 옵션에 aaaGroup | Microsoft Docs"
description: "솔루션 개발을 위한 Azure SQL 데이터 웨어하우스의 GROUP BY 옵션 구현을 위한 팁."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: f95a1e43-768f-4b7b-8a10-8a0509d0c871
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: queries
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: cc443c2af4e3ef2babd74d78aa6fb57bb3c1c7ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="group-by-options-in-sql-data-warehouse"></a><span data-ttu-id="cb5dd-103">SQL 데이터 웨어하우스의 GROUP BY 옵션</span><span class="sxs-lookup"><span data-stu-id="cb5dd-103">Group by options in SQL Data Warehouse</span></span>
<span data-ttu-id="cb5dd-104">hello [GROUP BY] [ GROUP BY] 절을 사용 하는 tooaggregate 데이터 tooa 요약 행 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="cb5dd-104">hello [GROUP BY][GROUP BY] clause is used tooaggregate data tooa summary set of rows.</span></span> <span data-ttu-id="cb5dd-105">또한 Azure SQL 데이터 웨어하우스에서 직접 지원 하지 않는 대로 해결할 필요가 toobe 해당의 기능을 확장 하는 몇 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb5dd-105">It also has a few options that extend it's functionality that need toobe worked around as they are not directly supported by Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="cb5dd-106">이들 옵션은</span><span class="sxs-lookup"><span data-stu-id="cb5dd-106">These options are</span></span>

* <span data-ttu-id="cb5dd-107">GROUP BY with ROLLUP</span><span class="sxs-lookup"><span data-stu-id="cb5dd-107">GROUP BY with ROLLUP</span></span>
* <span data-ttu-id="cb5dd-108">그룹화 집합</span><span class="sxs-lookup"><span data-stu-id="cb5dd-108">GROUPING SETS</span></span>
* <span data-ttu-id="cb5dd-109">GROUP BY with CUBE</span><span class="sxs-lookup"><span data-stu-id="cb5dd-109">GROUP BY with CUBE</span></span>

## <a name="rollup-and-grouping-sets-options"></a><span data-ttu-id="cb5dd-110">롤업 및 그룹화 집합 옵션</span><span class="sxs-lookup"><span data-stu-id="cb5dd-110">Rollup and grouping sets options</span></span>
<span data-ttu-id="cb5dd-111">hello 여기 가장 간단한 옵션은 toouse `UNION ALL` 대신에 의존 하지 않고 tooperform hello 롤업 hello 명시적 구문입니다.</span><span class="sxs-lookup"><span data-stu-id="cb5dd-111">hello simplest option here is toouse `UNION ALL` instead tooperform hello rollup rather than relying on hello explicit syntax.</span></span> <span data-ttu-id="cb5dd-112">hello 결과 동일한 hello 정확 하 게</span><span class="sxs-lookup"><span data-stu-id="cb5dd-112">hello result is exactly hello same</span></span>

<span data-ttu-id="cb5dd-113">다음은 group by hello를 사용 하 여 문의 예 `ROLLUP` 옵션:</span><span class="sxs-lookup"><span data-stu-id="cb5dd-113">Below is an example of a group by statement using hello `ROLLUP` option:</span></span>

```sql
SELECT [SalesTerritoryCountry]
,      [SalesTerritoryRegion]
,      SUM(SalesAmount)             AS TotalSalesAmount
FROM  dbo.factInternetSales s
JOIN  dbo.DimSalesTerritory t       ON s.SalesTerritoryKey       = t.SalesTerritoryKey
GROUP BY ROLLUP (
                        [SalesTerritoryCountry]
                ,       [SalesTerritoryRegion]
                )
;
```

<span data-ttu-id="cb5dd-114">롤업을 사용 하 여 집계를 수행 하는 hello 요청한:</span><span class="sxs-lookup"><span data-stu-id="cb5dd-114">By using ROLLUP we have requested hello following aggregations:</span></span>

* <span data-ttu-id="cb5dd-115">국가 및 지역</span><span class="sxs-lookup"><span data-stu-id="cb5dd-115">Country and Region</span></span>
* <span data-ttu-id="cb5dd-116">국가</span><span class="sxs-lookup"><span data-stu-id="cb5dd-116">Country</span></span>
* <span data-ttu-id="cb5dd-117">총합계</span><span class="sxs-lookup"><span data-stu-id="cb5dd-117">Grand Total</span></span>

<span data-ttu-id="cb5dd-118">tooreplace toouse 해야이 `UNION ALL`; 명시적으로 필요한 hello 집계 지정 tooreturn hello 동일한 결과:</span><span class="sxs-lookup"><span data-stu-id="cb5dd-118">tooreplace this you will need toouse `UNION ALL`; specifying hello aggregations required explicitly tooreturn hello same results:</span></span>

```sql
SELECT [SalesTerritoryCountry]
,      [SalesTerritoryRegion]
,      SUM(SalesAmount) AS TotalSalesAmount
FROM  dbo.factInternetSales s
JOIN  dbo.DimSalesTerritory t     ON s.SalesTerritoryKey       = t.SalesTerritoryKey
GROUP BY
       [SalesTerritoryCountry]
,      [SalesTerritoryRegion]
UNION ALL
SELECT [SalesTerritoryCountry]
,      NULL
,      SUM(SalesAmount) AS TotalSalesAmount
FROM  dbo.factInternetSales s
JOIN  dbo.DimSalesTerritory t     ON s.SalesTerritoryKey       = t.SalesTerritoryKey
GROUP BY
       [SalesTerritoryCountry]
UNION ALL
SELECT NULL
,      NULL
,      SUM(SalesAmount) AS TotalSalesAmount
FROM  dbo.factInternetSales s
JOIN  dbo.DimSalesTerritory t     ON s.SalesTerritoryKey       = t.SalesTerritoryKey;
```

<span data-ttu-id="cb5dd-119">Toosee 원하는 toodo 필요한 것은 채택 GROUPING SETS 주 동일 hello 있지만 계정만 hello에 대 한 UNION ALL 섹션을 만들 집계 수준</span><span class="sxs-lookup"><span data-stu-id="cb5dd-119">For GROUPING SETS all we need toodo is adopt hello same principal but only create UNION ALL sections for hello aggregation levels we want toosee</span></span>

## <a name="cube-options"></a><span data-ttu-id="cb5dd-120">큐브 옵션</span><span class="sxs-lookup"><span data-stu-id="cb5dd-120">Cube options</span></span>
<span data-ttu-id="cb5dd-121">가능한 toocreate는 GROUP BY WITH CUBE는 hello UNION ALL 접근 방식을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb5dd-121">It is possible toocreate a GROUP BY WITH CUBE using hello UNION ALL approach.</span></span> <span data-ttu-id="cb5dd-122">hello 문제는 번거롭고 다루기 hello 코드 신속 하 게 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb5dd-122">hello problem is that hello code can quickly become cumbersome and unwieldy.</span></span> <span data-ttu-id="cb5dd-123">toomitigate이이 사용 하 여 고급 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="cb5dd-123">toomitigate this you can use this more advanced approach.</span></span>

<span data-ttu-id="cb5dd-124">위의 hello 예제를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb5dd-124">Let's use hello example above.</span></span>

<span data-ttu-id="cb5dd-125">hello 첫 번째 단계는 toodefine hello 모든 hello 수준의 toocreate 한다고 집계를 정의 하는 ' 큐브의'입니다.</span><span class="sxs-lookup"><span data-stu-id="cb5dd-125">hello first step is toodefine hello 'cube' that defines all hello levels of aggregation that we want toocreate.</span></span> <span data-ttu-id="cb5dd-126">적절 하지 중요 tootake hello hello 두 파생된 테이블의 CROSS JOIN의 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb5dd-126">It is important tootake note of hello CROSS JOIN of hello two derived tables.</span></span> <span data-ttu-id="cb5dd-127">이 모든 hello 수준을 위해 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb5dd-127">This generates all hello levels for us.</span></span> <span data-ttu-id="cb5dd-128">hello 코드의 나머지 부분 hello 거기 실제로 서식을 지정 하기 위한 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb5dd-128">hello rest of hello code is really there for formatting.</span></span>

```sql
CREATE TABLE #Cube
WITH
(   DISTRIBUTION = ROUND_ROBIN
,   LOCATION = USER_DB
)
AS
WITH GrpCube AS
(SELECT    CAST(ISNULL(Country,'NULL')+','+ISNULL(Region,'NULL') AS NVARCHAR(50)) as 'Cols'
,          CAST(ISNULL(Country+',','')+ISNULL(Region,'') AS NVARCHAR(50))  as 'GroupBy'
,          ROW_NUMBER() OVER (ORDER BY Country) as 'Seq'
FROM       ( SELECT 'SalesTerritoryCountry' as Country
             UNION ALL
             SELECT NULL
           ) c
CROSS JOIN ( SELECT 'SalesTerritoryRegion' as Region
             UNION ALL
             SELECT NULL
           ) r
)
SELECT Cols
,      CASE WHEN SUBSTRING(GroupBy,LEN(GroupBy),1) = ','
            THEN SUBSTRING(GroupBy,1,LEN(GroupBy)-1)
            ELSE GroupBy
       END AS GroupBy  --Remove Trailing Comma
,Seq
FROM GrpCube;
```

<span data-ttu-id="cb5dd-129">hello의 hello 결과 CTAS에는 아래 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb5dd-129">hello results of hello CTAS can be seen below:</span></span>

![][1]

<span data-ttu-id="cb5dd-130">hello 두 번째 단계는 대상 테이블 toostore 중간 결과 toospecify입니다.</span><span class="sxs-lookup"><span data-stu-id="cb5dd-130">hello second step is toospecify a target table toostore interim results:</span></span>

```sql
DECLARE
 @SQL NVARCHAR(4000)
,@Columns NVARCHAR(4000)
,@GroupBy NVARCHAR(4000)
,@i INT = 1
,@nbr INT = 0
;
CREATE TABLE #Results
(
 [SalesTerritoryCountry] NVARCHAR(50)
,[SalesTerritoryRegion]  NVARCHAR(50)
,[TotalSalesAmount]      MONEY
)
WITH
(   DISTRIBUTION = ROUND_ROBIN
,   LOCATION = USER_DB
)
;
```

<span data-ttu-id="cb5dd-131">hello 세 번째 단계는 hello 집계를 수행 하는 열이 큐브에 대해 tooloop을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cb5dd-131">hello third step is tooloop over our cube of columns performing hello aggregation.</span></span> <span data-ttu-id="cb5dd-132">hello 쿼리 hello #Cube 임시 테이블의 모든 행에 대해 한 번 실행 되 고 hello 결과 hello #Results 임시 테이블에 저장</span><span class="sxs-lookup"><span data-stu-id="cb5dd-132">hello query will run once for every row in hello #Cube temporary table and store hello results in hello #Results temp table</span></span>

```sql
SET @nbr =(SELECT MAX(Seq) FROM #Cube);

WHILE @i<=@nbr
BEGIN
    SET @Columns = (SELECT Cols    FROM #Cube where seq = @i);
    SET @GroupBy = (SELECT GroupBy FROM #Cube where seq = @i);

    SET @SQL ='INSERT INTO #Results
              SELECT '+@Columns+'
              ,      SUM(SalesAmount) AS TotalSalesAmount
              FROM  dbo.factInternetSales s
              JOIN  dbo.DimSalesTerritory t  
              ON s.SalesTerritoryKey = t.SalesTerritoryKey
              '+CASE WHEN @GroupBy <>''
                     THEN 'GROUP BY '+@GroupBy ELSE '' END

    EXEC sp_executesql @SQL;
    SET @i +=1;
END
```

<span data-ttu-id="cb5dd-133">마지막으로 간단히 hello #Results 임시 테이블에서 참조 하 여 hello 결과 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb5dd-133">Lastly we can return hello results by simply reading from hello #Results temporary table</span></span>

```sql
SELECT *
FROM #Results
ORDER BY 1,2,3
;
```

<span data-ttu-id="cb5dd-134">Hello 코드 섹션으로 분할 하 고 반복 구문을 hello를 생성 하 여 좀 더 관리 및 유지 관리 가능한 코드 향상 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb5dd-134">By breaking hello code up into sections and generating a looping construct hello code becomes more manageable and maintainable.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cb5dd-135">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cb5dd-135">Next steps</span></span>
<span data-ttu-id="cb5dd-136">더 많은 개발 팁은 [개발 개요][development overview]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cb5dd-136">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->
[1]: media/sql-data-warehouse-develop-group-by-options/sql-data-warehouse-develop-group-by-cube.png

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[GROUP BY]: https://msdn.microsoft.com/library/ms177673.aspx


<!--Other Web references-->

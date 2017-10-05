---
title: "SQL Data Warehouse의 GROUP BY 옵션 | Microsoft Docs"
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
ms.openlocfilehash: da71cb834c13da5d0f5690f471efc6c696163f30
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="group-by-options-in-sql-data-warehouse"></a><span data-ttu-id="aa947-103">SQL 데이터 웨어하우스의 GROUP BY 옵션</span><span class="sxs-lookup"><span data-stu-id="aa947-103">Group by options in SQL Data Warehouse</span></span>
<span data-ttu-id="aa947-104">[GROUP BY][GROUP BY] 절을 사용하여 데이터를 요약 행 집합으로 집계합니다.</span><span class="sxs-lookup"><span data-stu-id="aa947-104">The [GROUP BY][GROUP BY] clause is used to aggregate data to a summary set of rows.</span></span> <span data-ttu-id="aa947-105">또한 Azure SQL 데이터 웨어하우스에서 직접 지원하지 않기 때문에 해결해야 하는 기능을 확장하는 몇 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa947-105">It also has a few options that extend it's functionality that need to be worked around as they are not directly supported by Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="aa947-106">이들 옵션은</span><span class="sxs-lookup"><span data-stu-id="aa947-106">These options are</span></span>

* <span data-ttu-id="aa947-107">GROUP BY with ROLLUP</span><span class="sxs-lookup"><span data-stu-id="aa947-107">GROUP BY with ROLLUP</span></span>
* <span data-ttu-id="aa947-108">그룹화 집합</span><span class="sxs-lookup"><span data-stu-id="aa947-108">GROUPING SETS</span></span>
* <span data-ttu-id="aa947-109">GROUP BY with CUBE</span><span class="sxs-lookup"><span data-stu-id="aa947-109">GROUP BY with CUBE</span></span>

## <a name="rollup-and-grouping-sets-options"></a><span data-ttu-id="aa947-110">롤업 및 그룹화 집합 옵션</span><span class="sxs-lookup"><span data-stu-id="aa947-110">Rollup and grouping sets options</span></span>
<span data-ttu-id="aa947-111">여기서 가장 간단한 옵션은 명시적 구문에 의존하는 대신 `UNION ALL` 을 사용하여 롤업을 수행하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="aa947-111">The simplest option here is to use `UNION ALL` instead to perform the rollup rather than relying on the explicit syntax.</span></span> <span data-ttu-id="aa947-112">결과는 완전히 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="aa947-112">The result is exactly the same</span></span>

<span data-ttu-id="aa947-113">다음은 `ROLLUP` 옵션을 사용하는 GROUP BY 문의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="aa947-113">Below is an example of a group by statement using the `ROLLUP` option:</span></span>

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

<span data-ttu-id="aa947-114">ROLLUP을 사용하여 다음과 같은 집계를 요청했습니다.</span><span class="sxs-lookup"><span data-stu-id="aa947-114">By using ROLLUP we have requested the following aggregations:</span></span>

* <span data-ttu-id="aa947-115">국가 및 지역</span><span class="sxs-lookup"><span data-stu-id="aa947-115">Country and Region</span></span>
* <span data-ttu-id="aa947-116">국가</span><span class="sxs-lookup"><span data-stu-id="aa947-116">Country</span></span>
* <span data-ttu-id="aa947-117">총합계</span><span class="sxs-lookup"><span data-stu-id="aa947-117">Grand Total</span></span>

<span data-ttu-id="aa947-118">이 요청을 바꾸려면 `UNION ALL`을 사용해야 하며, 동일한 결과가 반환되도록 필요한 집계를 명시적으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="aa947-118">To replace this you will need to use `UNION ALL`; specifying the aggregations required explicitly to return the same results:</span></span>

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

<span data-ttu-id="aa947-119">GROUPING SETS의 경우 같은 원칙을 적용하되 보고자 하는 집계 수준에 맞는 UNION ALL 섹션만 만들면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa947-119">For GROUPING SETS all we need to do is adopt the same principal but only create UNION ALL sections for the aggregation levels we want to see</span></span>

## <a name="cube-options"></a><span data-ttu-id="aa947-120">큐브 옵션</span><span class="sxs-lookup"><span data-stu-id="aa947-120">Cube options</span></span>
<span data-ttu-id="aa947-121">UNION ALL 접근방식을 사용하여 GROUP BY WITH CUBE를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa947-121">It is possible to create a GROUP BY WITH CUBE using the UNION ALL approach.</span></span> <span data-ttu-id="aa947-122">문제는 코드가 금세 번거롭고 다루기 힘들게 될 수 있다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="aa947-122">The problem is that the code can quickly become cumbersome and unwieldy.</span></span> <span data-ttu-id="aa947-123">이 문제를 완화하기 위해 더 고급스러운 이 접근방식을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa947-123">To mitigate this you can use this more advanced approach.</span></span>

<span data-ttu-id="aa947-124">위의 예제를 사용해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="aa947-124">Let's use the example above.</span></span>

<span data-ttu-id="aa947-125">첫 번째 단계는 만들고자 하는 집계의 모든 수준을 정의하는 ‘큐브'를 정의하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="aa947-125">The first step is to define the 'cube' that defines all the levels of aggregation that we want to create.</span></span> <span data-ttu-id="aa947-126">파생된 테이블 두 개의 CROSS JOIN에 주목해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa947-126">It is important to take note of the CROSS JOIN of the two derived tables.</span></span> <span data-ttu-id="aa947-127">이렇게 하면 필요한 모든 수준이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa947-127">This generates all the levels for us.</span></span> <span data-ttu-id="aa947-128">코드의 나머지 부분은 사실상 서식 지정을 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="aa947-128">The rest of the code is really there for formatting.</span></span>

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

<span data-ttu-id="aa947-129">CTAS의 결과는 아래와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="aa947-129">The results of the CTAS can be seen below:</span></span>

![][1]

<span data-ttu-id="aa947-130">두 번째 단계는 중간 결과를 저장할 대상 테이블을 지정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="aa947-130">The second step is to specify a target table to store interim results:</span></span>

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

<span data-ttu-id="aa947-131">세 번째 단계는 집계를 수행하는 열의 큐브를 반복하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="aa947-131">The third step is to loop over our cube of columns performing the aggregation.</span></span> <span data-ttu-id="aa947-132">쿼리는 #Cube 임시 테이블의 모든 행에 대해 한 번 실행하며 결과를 #Results 임시 테이블에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="aa947-132">The query will run once for every row in the #Cube temporary table and store the results in the #Results temp table</span></span>

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

<span data-ttu-id="aa947-133">마지막으로 #Results 임시 테이블을 읽어서 결과를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa947-133">Lastly we can return the results by simply reading from the #Results temporary table</span></span>

```sql
SELECT *
FROM #Results
ORDER BY 1,2,3
;
```

<span data-ttu-id="aa947-134">코드를 섹션으로 분할하고 반복 구성을 생성하면 코드의 관리 및 유지 관리가 더 쉬워집니다.</span><span class="sxs-lookup"><span data-stu-id="aa947-134">By breaking the code up into sections and generating a looping construct the code becomes more manageable and maintainable.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aa947-135">다음 단계</span><span class="sxs-lookup"><span data-stu-id="aa947-135">Next steps</span></span>
<span data-ttu-id="aa947-136">더 많은 개발 팁은 [개발 개요][development overview]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="aa947-136">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->
[1]: media/sql-data-warehouse-develop-group-by-options/sql-data-warehouse-develop-group-by-cube.png

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[GROUP BY]: https://msdn.microsoft.com/library/ms177673.aspx


<!--Other Web references-->

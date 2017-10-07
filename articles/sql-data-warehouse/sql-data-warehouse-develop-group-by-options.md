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
# <a name="group-by-options-in-sql-data-warehouse"></a>SQL 데이터 웨어하우스의 GROUP BY 옵션
hello [GROUP BY] [ GROUP BY] 절을 사용 하는 tooaggregate 데이터 tooa 요약 행 집합입니다. 또한 Azure SQL 데이터 웨어하우스에서 직접 지원 하지 않는 대로 해결할 필요가 toobe 해당의 기능을 확장 하는 몇 가지 옵션이 있습니다.

이들 옵션은

* GROUP BY with ROLLUP
* 그룹화 집합
* GROUP BY with CUBE

## <a name="rollup-and-grouping-sets-options"></a>롤업 및 그룹화 집합 옵션
hello 여기 가장 간단한 옵션은 toouse `UNION ALL` 대신에 의존 하지 않고 tooperform hello 롤업 hello 명시적 구문입니다. hello 결과 동일한 hello 정확 하 게

다음은 group by hello를 사용 하 여 문의 예 `ROLLUP` 옵션:

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

롤업을 사용 하 여 집계를 수행 하는 hello 요청한:

* 국가 및 지역
* 국가
* 총합계

tooreplace toouse 해야이 `UNION ALL`; 명시적으로 필요한 hello 집계 지정 tooreturn hello 동일한 결과:

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

Toosee 원하는 toodo 필요한 것은 채택 GROUPING SETS 주 동일 hello 있지만 계정만 hello에 대 한 UNION ALL 섹션을 만들 집계 수준

## <a name="cube-options"></a>큐브 옵션
가능한 toocreate는 GROUP BY WITH CUBE는 hello UNION ALL 접근 방식을 사용 합니다. hello 문제는 번거롭고 다루기 hello 코드 신속 하 게 될 수 있습니다. toomitigate이이 사용 하 여 고급 방법입니다.

위의 hello 예제를 사용 합니다.

hello 첫 번째 단계는 toodefine hello 모든 hello 수준의 toocreate 한다고 집계를 정의 하는 ' 큐브의'입니다. 적절 하지 중요 tootake hello hello 두 파생된 테이블의 CROSS JOIN의 합니다. 이 모든 hello 수준을 위해 생성 됩니다. hello 코드의 나머지 부분 hello 거기 실제로 서식을 지정 하기 위한 합니다.

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

hello의 hello 결과 CTAS에는 아래 볼 수 있습니다.

![][1]

hello 두 번째 단계는 대상 테이블 toostore 중간 결과 toospecify입니다.

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

hello 세 번째 단계는 hello 집계를 수행 하는 열이 큐브에 대해 tooloop을 것입니다. hello 쿼리 hello #Cube 임시 테이블의 모든 행에 대해 한 번 실행 되 고 hello 결과 hello #Results 임시 테이블에 저장

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

마지막으로 간단히 hello #Results 임시 테이블에서 참조 하 여 hello 결과 반환할 수 있습니다.

```sql
SELECT *
FROM #Results
ORDER BY 1,2,3
;
```

Hello 코드 섹션으로 분할 하 고 반복 구문을 hello를 생성 하 여 좀 더 관리 및 유지 관리 가능한 코드 향상 됩니다.

## <a name="next-steps"></a>다음 단계
더 많은 개발 팁은 [개발 개요][development overview]를 참조하세요.

<!--Image references-->
[1]: media/sql-data-warehouse-develop-group-by-options/sql-data-warehouse-develop-group-by-cube.png

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[GROUP BY]: https://msdn.microsoft.com/library/ms177673.aspx


<!--Other Web references-->

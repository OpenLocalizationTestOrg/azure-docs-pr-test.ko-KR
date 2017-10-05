---
title: "U-SQL 카탈로그 시작 | Microsoft Docs"
description: "U-SQL 카탈로그를 사용하여 코드와 데이터를 공유하는 방법을 알아봅니다."
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 57143396-ab86-47dd-b6f8-613ba28c28d2
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/09/2017
ms.author: edmaca
ms.openlocfilehash: 08364c6c7bea53807844e3b1cc327dc3742e0487
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-u-sql-catalog"></a><span data-ttu-id="eca33-103">U-SQL 카탈로그 시작</span><span class="sxs-lookup"><span data-stu-id="eca33-103">Get started with the U-SQL Catalog</span></span>

## <a name="create-a-tvf"></a><span data-ttu-id="eca33-104">TVF 만들기</span><span class="sxs-lookup"><span data-stu-id="eca33-104">Create a TVF</span></span>

<span data-ttu-id="eca33-105">이전 U-SQL 스크립트에서는 동일한 원본 파일에서 읽어 오는 EXTRACT 사용을 반복했습니다.</span><span class="sxs-lookup"><span data-stu-id="eca33-105">In the previous U-SQL script, you repeated the use of EXTRACT to read from the same source file.</span></span> <span data-ttu-id="eca33-106">U-SQL TVF(테이블 반환 함수)를 사용하면 데이터를 나중에 다시 사용할 수 있게 캡슐화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eca33-106">With the U-SQL table-valued function (TVF), you can encapsulate the data for future reuse.</span></span>  

<span data-ttu-id="eca33-107">다음 스크립트는 기본 데이터베이스 및 스키마에 `Searchlog()`라는 TVF를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eca33-107">The following script creates a TVF called `Searchlog()` in the default database and schema:</span></span>

```
DROP FUNCTION IF EXISTS Searchlog;

CREATE FUNCTION Searchlog()
RETURNS @searchlog TABLE
(
            UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string
)
AS BEGIN
@searchlog =
    EXTRACT UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string
    FROM "/Samples/Data/SearchLog.tsv"
USING Extractors.Tsv();
RETURN;
END;
```

<span data-ttu-id="eca33-108">다음 스크립트는 이전 스크립트에서 정의된 TVF를 사용하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="eca33-108">The following script shows you how to use the TVF that was defined in the previous script:</span></span>

```
@res =
    SELECT
        Region,
        SUM(Duration) AS TotalDuration
    FROM Searchlog() AS S
GROUP BY Region
HAVING SUM(Duration) > 200;

OUTPUT @res
    TO "/output/SerachLog-use-tvf.csv"
    ORDER BY TotalDuration DESC
    USING Outputters.Csv();
```

## <a name="create-views"></a><span data-ttu-id="eca33-109">뷰 만들기</span><span class="sxs-lookup"><span data-stu-id="eca33-109">Create views</span></span>

<span data-ttu-id="eca33-110">단일 쿼리 식이 있는 경우 TVF 대신 U-SQL VIEW를 사용하여 해당 식을 캡슐화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eca33-110">If you have a single query expression, instead of a TVF you can use a U-SQL VIEW to encapsulate that expression.</span></span>

<span data-ttu-id="eca33-111">다음 스크립트는 기본 데이터베이스 및 스키마에 `SearchlogView`라는 뷰를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eca33-111">The following script creates a view called `SearchlogView` in the default database and schema:</span></span>

```
DROP VIEW IF EXISTS SearchlogView;

CREATE VIEW SearchlogView AS  
    EXTRACT UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string
    FROM "/Samples/Data/SearchLog.tsv"
USING Extractors.Tsv();
```

<span data-ttu-id="eca33-112">다음 스크립트는 정의된 뷰를 사용함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="eca33-112">The following script demonstrates the use of the defined view:</span></span>

```
@res =
    SELECT
        Region,
        SUM(Duration) AS TotalDuration
    FROM SearchlogView
GROUP BY Region
HAVING SUM(Duration) > 200;

OUTPUT @res
    TO "/output/Searchlog-use-view.csv"
    ORDER BY TotalDuration DESC
    USING Outputters.Csv();
```

## <a name="create-tables"></a><span data-ttu-id="eca33-113">테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="eca33-113">Create tables</span></span>
<span data-ttu-id="eca33-114">관계형 데이터베이스 테이블과 마찬가지로, U-SQL을 사용하여 미리 정의된 스키마가 포함된 테이블을 만들거나 테이블을 채운 쿼리(CREATE TABLE AS SELECT 또는 CTAS)에서 스키마를 유추하는 테이블을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eca33-114">As with relational database tables, with U-SQL you can create a table with a predefined schema or create a table that infers the schema from the query that populates the table (also known as CREATE TABLE AS SELECT or CTAS).</span></span>

<span data-ttu-id="eca33-115">다음 스크립트를 사용하여 데이터베이스 하나와 테이블 두 개를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eca33-115">Create a database and two tables by using the following script:</span></span>

```
DROP DATABASE IF EXISTS SearchLogDb;
CREATE DATABASE SearchLogDb;
USE DATABASE SearchLogDb;

DROP TABLE IF EXISTS SearchLog1;
DROP TABLE IF EXISTS SearchLog2;

CREATE TABLE SearchLog1 (
            UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string,

            INDEX sl_idx CLUSTERED (UserId ASC)
                DISTRIBUTED BY HASH (UserId)
);

INSERT INTO SearchLog1 SELECT * FROM master.dbo.Searchlog() AS s;

CREATE TABLE SearchLog2(
    INDEX sl_idx CLUSTERED (UserId ASC)
            DISTRIBUTED BY HASH (UserId)
) AS SELECT * FROM master.dbo.Searchlog() AS S; // You can use EXTRACT or SELECT here
```

## <a name="query-tables"></a><span data-ttu-id="eca33-116">쿼리 테이블</span><span class="sxs-lookup"><span data-stu-id="eca33-116">Query tables</span></span>
<span data-ttu-id="eca33-117">데이터 파일을 쿼리하는 것과 같은 방식으로 이전 스크립트에서 만든 테이블을 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eca33-117">You can query tables, such as those created in the previous script, in the same way that you query the data files.</span></span> <span data-ttu-id="eca33-118">EXTRACT를 사용하여 행 집합을 만드는 대신 테이블 이름을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eca33-118">Instead of creating a rowset by using EXTRACT, you now can refer to the table name.</span></span>

<span data-ttu-id="eca33-119">테이블에서 읽어 오려면 이전에 사용한 변환 스크립트를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="eca33-119">To read from the tables, modify the transform script that you used previously:</span></span>

```
@rs1 =
    SELECT
        Region,
        SUM(Duration) AS TotalDuration
    FROM SearchLogDb.dbo.SearchLog2
GROUP BY Region;

@res =
    SELECT *
    FROM @rs1
    ORDER BY TotalDuration DESC
    FETCH 5 ROWS;

OUTPUT @res
    TO "/output/Searchlog-query-table.csv"
    ORDER BY TotalDuration DESC
    USING Outputters.Csv();
```

 >[!NOTE]
 ><span data-ttu-id="eca33-120">현재는 테이블을 만든 스크립트와 같은 스크립트의 테이블에 SELECT를 실행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="eca33-120">Currently, you cannot run a SELECT on a table in the same script as the one where you created the table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eca33-121">다음 단계</span><span class="sxs-lookup"><span data-stu-id="eca33-121">Next Steps</span></span>
* [<span data-ttu-id="eca33-122">Microsoft Azure 데이터 레이크 분석 개요</span><span class="sxs-lookup"><span data-stu-id="eca33-122">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="eca33-123">Visual Studio용 데이터 레이크 도구를 사용하여 U-SQL 스크립트 개발</span><span class="sxs-lookup"><span data-stu-id="eca33-123">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="eca33-124">Azure 포털을 사용하여 Azure Data Lake Analytics 작업 모니터링 및 문제 해결</span><span class="sxs-lookup"><span data-stu-id="eca33-124">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)

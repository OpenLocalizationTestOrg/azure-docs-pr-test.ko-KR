---
title: "Hello U-SQL 카탈로그 시작 | Microsoft Docs"
description: "Toouse hello U-SQL tooshare 코드 및 데이터 카탈로그 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 559bb7a3879031eb290a3e82946d7bf42ac9f553
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-u-sql-catalog"></a><span data-ttu-id="ecc2a-103">U-SQL 카탈로그 hello로 시작.</span><span class="sxs-lookup"><span data-stu-id="ecc2a-103">Get started with hello U-SQL Catalog</span></span>

## <a name="create-a-tvf"></a><span data-ttu-id="ecc2a-104">TVF 만들기</span><span class="sxs-lookup"><span data-stu-id="ecc2a-104">Create a TVF</span></span>

<span data-ttu-id="ecc2a-105">Hello에서 추출 tooread hello 사용을 반복 hello 앞의 U-SQL 스크립트에서 동일한 소스 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="ecc2a-105">In hello previous U-SQL script, you repeated hello use of EXTRACT tooread from hello same source file.</span></span> <span data-ttu-id="ecc2a-106">Hello U-SQL 테이블 반환 함수 (TVF) 사용 하 여 나중에 다시 사용에 대 한 hello 데이터를 캡슐화 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecc2a-106">With hello U-SQL table-valued function (TVF), you can encapsulate hello data for future reuse.</span></span>  

<span data-ttu-id="ecc2a-107">hello 다음 스크립트를 만듭니다 라는 TVF `Searchlog()` hello 기본 데이터베이스와 스키마에서:</span><span class="sxs-lookup"><span data-stu-id="ecc2a-107">hello following script creates a TVF called `Searchlog()` in hello default database and schema:</span></span>

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

<span data-ttu-id="ecc2a-108">다음 스크립트는 hello toouse TVF hello 앞의 스크립트에 정의 된 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ecc2a-108">hello following script shows you how toouse hello TVF that was defined in hello previous script:</span></span>

```
@res =
    SELECT
        Region,
        SUM(Duration) AS TotalDuration
    FROM Searchlog() AS S
GROUP BY Region
HAVING SUM(Duration) > 200;

OUTPUT @res
    too"/output/SerachLog-use-tvf.csv"
    ORDER BY TotalDuration DESC
    USING Outputters.Csv();
```

## <a name="create-views"></a><span data-ttu-id="ecc2a-109">뷰 만들기</span><span class="sxs-lookup"><span data-stu-id="ecc2a-109">Create views</span></span>

<span data-ttu-id="ecc2a-110">쿼리 식 하나를 사용 하도록 설정한 경우 대신 TVF를 사용할 수 있습니다 보기 U-SQL tooencapsulate 해당 식입니다.</span><span class="sxs-lookup"><span data-stu-id="ecc2a-110">If you have a single query expression, instead of a TVF you can use a U-SQL VIEW tooencapsulate that expression.</span></span>

<span data-ttu-id="ecc2a-111">hello 다음 스크립트를 만듭니다 라는 보기가 `SearchlogView` hello 기본 데이터베이스와 스키마에서:</span><span class="sxs-lookup"><span data-stu-id="ecc2a-111">hello following script creates a view called `SearchlogView` in hello default database and schema:</span></span>

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

<span data-ttu-id="ecc2a-112">다음 스크립트는 hello hello 정의 된 보기의 hello 사용을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ecc2a-112">hello following script demonstrates hello use of hello defined view:</span></span>

```
@res =
    SELECT
        Region,
        SUM(Duration) AS TotalDuration
    FROM SearchlogView
GROUP BY Region
HAVING SUM(Duration) > 200;

OUTPUT @res
    too"/output/Searchlog-use-view.csv"
    ORDER BY TotalDuration DESC
    USING Outputters.Csv();
```

## <a name="create-tables"></a><span data-ttu-id="ecc2a-113">테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="ecc2a-113">Create tables</span></span>
<span data-ttu-id="ecc2a-114">관계형 데이터베이스 테이블 U-SQL와 수는 미리 정의 된 스키마가 있는 테이블을 만들 하거나 테이블을 만듭니다 (CREATE TABLE AS SELECT 또는 라고도 CTAS) hello 테이블을 채우는 hello 쿼리에서 hello 스키마를 유추 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecc2a-114">As with relational database tables, with U-SQL you can create a table with a predefined schema or create a table that infers hello schema from hello query that populates hello table (also known as CREATE TABLE AS SELECT or CTAS).</span></span>

<span data-ttu-id="ecc2a-115">다음 스크립트는 hello를 사용 하 여 데이터베이스와 두 개의 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ecc2a-115">Create a database and two tables by using hello following script:</span></span>

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

## <a name="query-tables"></a><span data-ttu-id="ecc2a-116">쿼리 테이블</span><span class="sxs-lookup"><span data-stu-id="ecc2a-116">Query tables</span></span>
<span data-ttu-id="ecc2a-117">Hello에 hello 이전 스크립트에서 만든 테이블을 쿼리할 수 같은 방식으로 데이터 파일 hello를 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecc2a-117">You can query tables, such as those created in hello previous script, in hello same way that you query hello data files.</span></span> <span data-ttu-id="ecc2a-118">압축 해제를 사용 하 여 행 집합을 만드는 대신 이제 toohello 테이블 이름을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecc2a-118">Instead of creating a rowset by using EXTRACT, you now can refer toohello table name.</span></span>

<span data-ttu-id="ecc2a-119">tooread hello 테이블에서 이전에 사용 hello 변환 스크립트를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecc2a-119">tooread from hello tables, modify hello transform script that you used previously:</span></span>

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
    too"/output/Searchlog-query-table.csv"
    ORDER BY TotalDuration DESC
    USING Outputters.Csv();
```

 >[!NOTE]
 ><span data-ttu-id="ecc2a-120">현재 실행할 수 없습니다 SELECT hello 하나 hello 처럼 동일한 스크립트에 있는 테이블에 hello 테이블을 만들 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="ecc2a-120">Currently, you cannot run a SELECT on a table in hello same script as hello one where you created hello table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ecc2a-121">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ecc2a-121">Next Steps</span></span>
* [<span data-ttu-id="ecc2a-122">Microsoft Azure 데이터 레이크 분석 개요</span><span class="sxs-lookup"><span data-stu-id="ecc2a-122">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="ecc2a-123">Visual Studio용 데이터 레이크 도구를 사용하여 U-SQL 스크립트 개발</span><span class="sxs-lookup"><span data-stu-id="ecc2a-123">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="ecc2a-124">Azure 포털을 사용하여 Azure Data Lake Analytics 작업 모니터링 및 문제 해결</span><span class="sxs-lookup"><span data-stu-id="ecc2a-124">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)

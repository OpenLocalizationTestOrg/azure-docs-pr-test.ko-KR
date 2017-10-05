---
title: "U-SQL 언어 시작 | Microsoft Docs"
description: "U-SQL 언어의 기본 사항에 대해 알아봅니다."
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
ms.date: 06/23/2017
ms.author: saveenr
ms.openlocfilehash: 38c4e1b9bd24ef0b8a81f6154620f3f98d3b5ac1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-u-sql"></a><span data-ttu-id="bf4c0-103">U-SQL 시작</span><span class="sxs-lookup"><span data-stu-id="bf4c0-103">Get started with U-SQL</span></span>
<span data-ttu-id="bf4c0-104">U-SQL은 선언적 SQL을 명령적 C#에 결합하여 규모에 관계 없이 데이터를 처리할 수 있도록 하는 언어입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4c0-104">U-SQL is a language that combines declarative SQL with imperative C# to let you process data at any scale.</span></span> <span data-ttu-id="bf4c0-105">U-SQL의 확장성 있는 분산 쿼리 기능을 통해 Azure SQL Database와 같은 관계형 저장소의 데이터를 효율적으로 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf4c0-105">Through the scalable, distributed-query capability of U-SQL, you can efficiently analyze data across relational stores such as Azure SQL Database.</span></span> <span data-ttu-id="bf4c0-106">U-SQL을 사용하면 읽기에 대한 스키마를 적용하고 사용자 지정 논리 및 UDF를 삽입하여 구조화되지 않은 데이터를 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf4c0-106">With U-SQL, you can process unstructured data by applying schema on read and inserting custom logic and UDFs.</span></span> <span data-ttu-id="bf4c0-107">또한 U-SQL에는 모든 규모에서 실행하는 방법을 세부적으로 제어할 수 있게 해주는 확장성이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf4c0-107">Additionally, U-SQL includes extensibility that gives you fine-grained control over how to execute at scale.</span></span> 

## <a name="learning-resources"></a><span data-ttu-id="bf4c0-108">학습 리소스</span><span class="sxs-lookup"><span data-stu-id="bf4c0-108">Learning resources</span></span>

* <span data-ttu-id="bf4c0-109">[U-SQL 자습서](http://aka.ms/usqltutorial)에서는 대부분의 U-SQL 언어에 대한 안내식 연습 과정을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4c0-109">The [U-SQL Tutorial](http://aka.ms/usqltutorial) provides a guided walkthrough of most of the U-SQL language.</span></span> <span data-ttu-id="bf4c0-110">U-SQL을 학습하려는 모든 개발자는 이 문서를 읽어보는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="bf4c0-110">This document is recommended reading for all developers wanting to learn U-SQL.</span></span>
* <span data-ttu-id="bf4c0-111">**U-SQL 언어 구문**에 대한 자세한 내용은 [U-SQL 언어 참조](http://go.microsoft.com/fwlink/p/?LinkId=691348)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bf4c0-111">For detailed information about the **U-SQL language syntax**, see the [U-SQL Language Reference](http://go.microsoft.com/fwlink/p/?LinkId=691348).</span></span>
* <span data-ttu-id="bf4c0-112">**U-SQL 디자인 철학**을 이해하려면 Visual Studio 블로그 게시물 [Introducing U-SQL – A Language that makes Big Data Processing Easy(U-SQL 소개 - 빅 데이터 처리를 수월하게 해주는 언어)](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bf4c0-112">To understand the **U-SQL design philosophy**, see the Visual Studio blog post [Introducing U-SQL – A Language that makes Big Data Processing Easy](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bf4c0-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="bf4c0-113">Prerequisites</span></span>

<span data-ttu-id="bf4c0-114">이 문서의 U-SQL 샘플을 살펴본 후에 [자습서: Visual Studio용 데이터 레이크 도구를 사용하여 U-SQL 스크립트 개발](data-lake-analytics-data-lake-tools-get-started.md)을 읽고 완료하세요.</span><span class="sxs-lookup"><span data-stu-id="bf4c0-114">Before you go through the U-SQL samples in this document, read and complete [Tutorial: Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span> <span data-ttu-id="bf4c0-115">이 자습서는 Azure Data Lake Tools for Visual Studio에서 U-SQL을 사용하는 기법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4c0-115">That tutorial explains the mechanics of using U-SQL with Azure Data Lake Tools for Visual Studio.</span></span>

## <a name="your-first-u-sql-script"></a><span data-ttu-id="bf4c0-116">첫 번째 U-SQL 스크립트</span><span class="sxs-lookup"><span data-stu-id="bf4c0-116">Your first U-SQL script</span></span>

<span data-ttu-id="bf4c0-117">다음 U-SQL 스크립트는 간단하며 U-SQL 언어의 많은 측면을 파악하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4c0-117">The following U-SQL script is simple and lets us explore many aspects the U-SQL language.</span></span>

```
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

OUTPUT @searchlog   
    TO "/output/SearchLog-first-u-sql.csv"
    USING Outputters.Csv();
```

<span data-ttu-id="bf4c0-118">이 스크립트에는 변환 단계가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bf4c0-118">This script doesn't have any transformation steps.</span></span> <span data-ttu-id="bf4c0-119">`SearchLog.tsv`라는 원본 파일을 읽어와서 스키마를 만들고, 행 집합을 SearchLog-first-u-sql.csv 파일에 다시 씁니다.</span><span class="sxs-lookup"><span data-stu-id="bf4c0-119">It reads from the source file called `SearchLog.tsv`, schematizes it, and writes the rowset back into a file called SearchLog-first-u-sql.csv.</span></span>

<span data-ttu-id="bf4c0-120">`Duration` 필드의 데이터 형식 옆에 있는 물음표를 보세요.</span><span class="sxs-lookup"><span data-stu-id="bf4c0-120">Notice the question mark next to the data type in the `Duration` field.</span></span> <span data-ttu-id="bf4c0-121">이는 `Duration` 필드가 null이어도 된다는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4c0-121">It means that the `Duration` field could be null.</span></span>

### <a name="key-concepts"></a><span data-ttu-id="bf4c0-122">주요 개념</span><span class="sxs-lookup"><span data-stu-id="bf4c0-122">Key concepts</span></span>
* <span data-ttu-id="bf4c0-123">**Rowset 변수**: 행 집합을 생성하는 각 쿼리 식은 변수에 할당될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf4c0-123">**Rowset variables**: Each query expression that produces a rowset can be assigned to a variable.</span></span> <span data-ttu-id="bf4c0-124">U-SQL은 스크립트의 T-SQL 변수 이름 지정 패턴(예: `@searchlog`)을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="bf4c0-124">U-SQL follows the T-SQL variable naming pattern (`@searchlog`, for example) in the script.</span></span>
* <span data-ttu-id="bf4c0-125">**EXTRACT** 키워드는 파일에서 데이터를 읽고 읽기에 대한 스키마를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4c0-125">The **EXTRACT** keyword reads data from a file and defines the schema on read.</span></span> <span data-ttu-id="bf4c0-126">`Extractors.Tsv`는 탭으로 구분된 값 파일에 대한 기본 제공 U-SQL 추출기입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4c0-126">`Extractors.Tsv` is a built-in U-SQL extractor for tab-separated-value files.</span></span> <span data-ttu-id="bf4c0-127">사용자 지정 추출기를 개발할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf4c0-127">You can develop custom extractors.</span></span>
* <span data-ttu-id="bf4c0-128">**OUTPUT**은 행 집합의 데이터를 파일에 씁니다.</span><span class="sxs-lookup"><span data-stu-id="bf4c0-128">The **OUTPUT** writes data from a rowset to a file.</span></span> <span data-ttu-id="bf4c0-129">`Outputters.Csv()`는 쉼표로 구분된 값 파일을 만들기 위한 기본 제공 U-SQL 출력기입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4c0-129">`Outputters.Csv()` is a built-in U-SQL outputter to create a comma-separated-value file.</span></span> <span data-ttu-id="bf4c0-130">사용자 지정 출력기를 개발할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf4c0-130">You can develop custom outputters.</span></span>

### <a name="file-paths"></a><span data-ttu-id="bf4c0-131">파일 경로</span><span class="sxs-lookup"><span data-stu-id="bf4c0-131">File paths</span></span>

<span data-ttu-id="bf4c0-132">EXTRACT 및 OUTPUT 문은 파일 경로를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4c0-132">The EXTRACT and OUTPUT statements use file paths.</span></span> <span data-ttu-id="bf4c0-133">파일 경로는 절대 경로 또는 상대 경로일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf4c0-133">File paths can be absolute or relative:</span></span>

<span data-ttu-id="bf4c0-134">다음에 나오는 이 절대 파일 경로는 `mystore`라는 Data Lake Store의 파일을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4c0-134">This following absolute file path refers to a file in a Data Lake Store named `mystore`:</span></span>

    adl://mystore.azuredatalakestore.net/Samples/Data/SearchLog.tsv

<span data-ttu-id="bf4c0-135">다음에 나오는 이 파일 경로는 `"/"`로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4c0-135">This following file path starts with `"/"`.</span></span> <span data-ttu-id="bf4c0-136">기본 Data Lake Store 계정의 파일을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4c0-136">It refers to a file in the default Data Lake Store account:</span></span>

    /output/SearchLog-first-u-sql.csv

## <a name="use-scalar-variables"></a><span data-ttu-id="bf4c0-137">스칼라 변수 사용</span><span class="sxs-lookup"><span data-stu-id="bf4c0-137">Use scalar variables</span></span>

<span data-ttu-id="bf4c0-138">스크립트 유지 관리를 간편하게 만들기 위해 스칼라 변수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf4c0-138">You can use scalar variables as well to make your script maintenance easier.</span></span> <span data-ttu-id="bf4c0-139">이전 U-SQL 스크립트를 다음과 같이 작성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf4c0-139">The previous U-SQL script can also be written as:</span></span>

    DECLARE @in  string = "/Samples/Data/SearchLog.tsv";
    DECLARE @out string = "/output/SearchLog-scalar-variables.csv";

    @searchlog =
        EXTRACT UserId          int,
                Start           DateTime,
                Region          string,
                Query           string,
                Duration        int?,
                Urls            string,
                ClickedUrls     string
        FROM @in
        USING Extractors.Tsv();

    OUTPUT @searchlog   
        TO @out
        USING Outputters.Csv();

## <a name="transform-rowsets"></a><span data-ttu-id="bf4c0-140">변환 행 집합</span><span class="sxs-lookup"><span data-stu-id="bf4c0-140">Transform rowsets</span></span>

<span data-ttu-id="bf4c0-141">**SELECT** 를 사용하여 행 집합을 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4c0-141">Use **SELECT** to transform rowsets:</span></span>

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

    @rs1 =
        SELECT Start, Region, Duration
        FROM @searchlog
    WHERE Region == "en-gb";

    OUTPUT @rs1   
        TO "/output/SearchLog-transform-rowsets.csv"
        USING Outputters.Csv();

<span data-ttu-id="bf4c0-142">WHERE 절에는 [C# 부울 식](https://msdn.microsoft.com/library/6a71f45d.aspx)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4c0-142">The WHERE clause uses a [C# Boolean expression](https://msdn.microsoft.com/library/6a71f45d.aspx).</span></span> <span data-ttu-id="bf4c0-143">자신의 식 및 함수에 C# 식 언어를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf4c0-143">You can use the C# expression language to do your own expressions and functions.</span></span> <span data-ttu-id="bf4c0-144">식 및 함수를 논리 결합(ANDs) 및 분리(ORs)와 결합하여 더 복잡한 필터링을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf4c0-144">You can even perform more complex filtering by combining them with logical conjunctions (ANDs) and disjunctions (ORs).</span></span>

<span data-ttu-id="bf4c0-145">다음 스크립트는 DateTime.Parse() 메서드와 논리 결합을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4c0-145">The following script uses the DateTime.Parse() method and a conjunction.</span></span>

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

    @rs1 =
        SELECT Start, Region, Duration
        FROM @searchlog
    WHERE Region == "en-gb";

    @rs1 =
        SELECT Start, Region, Duration
        FROM @rs1
        WHERE Start >= DateTime.Parse("2012/02/16") AND Start <= DateTime.Parse("2012/02/17");

    OUTPUT @rs1   
        TO "/output/SearchLog-transform-datetime.csv"
        USING Outputters.Csv();

 >[!NOTE]
 ><span data-ttu-id="bf4c0-146">두 번째 쿼리는 첫 번째 행 집합의 결과를 기반으로 작동하며, 두 필터의 결합이 결과가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf4c0-146">The second query is operating on the result of the first rowset, which creates a composite of the two filters.</span></span> <span data-ttu-id="bf4c0-147">또한 변수 이름은 재사용이 가능하며 이름에는 어휘 범위(정적 범위)가 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf4c0-147">You can also reuse a variable name, and the names are scoped lexically.</span></span>

## <a name="aggregate-rowsets"></a><span data-ttu-id="bf4c0-148">집계 행 집합</span><span class="sxs-lookup"><span data-stu-id="bf4c0-148">Aggregate rowsets</span></span>
<span data-ttu-id="bf4c0-149">U-SQL에는 개발자에게 친숙한 ORDER BY, GROUP BY 및 집계가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf4c0-149">U-SQL gives you the familiar ORDER BY, GROUP BY, and aggregations.</span></span>

<span data-ttu-id="bf4c0-150">다음 쿼리는 지역 당 총 기간을 알아내고 최장 기간 다섯 개를 순서대로 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4c0-150">The following query finds the total duration per region, and then displays the top five durations in order.</span></span>

<span data-ttu-id="bf4c0-151">U-SQL 행 집합은 다음 쿼리를 위해 이 순서를 유지하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bf4c0-151">U-SQL rowsets do not preserve their order for the next query.</span></span> <span data-ttu-id="bf4c0-152">따라서 출력 순서를 정하려면 OUTPUT 문에 ORDER BY를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4c0-152">Thus, to order an output, you need to add ORDER BY to the OUTPUT statement:</span></span>

    DECLARE @outpref string = "/output/Searchlog-aggregation";
    DECLARE @out1    string = @outpref+"_agg.csv";
    DECLARE @out2    string = @outpref+"_top5agg.csv";

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

    @rs1 =
        SELECT
            Region,
            SUM(Duration) AS TotalDuration
        FROM @searchlog
    GROUP BY Region;

    @res =
        SELECT *
        FROM @rs1
        ORDER BY TotalDuration DESC
        FETCH 5 ROWS;

    OUTPUT @rs1
        TO @out1
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

    OUTPUT @res
        TO @out2
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

<span data-ttu-id="bf4c0-153">U-SQL ORDER BY 절에서는 SELECT 식에 FETCH 절을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4c0-153">The U-SQL ORDER BY clause requires using the FETCH clause in a SELECT expression.</span></span>

<span data-ttu-id="bf4c0-154">U-SQL HAVING 절은 HAVING 조건을 만족하는 그룹으로 출력을 제한하는 데 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf4c0-154">The U-SQL HAVING clause can be used to restrict the output to groups that satisfy the HAVING condition:</span></span>

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

    @res =
        SELECT
            Region,
            SUM(Duration) AS TotalDuration
        FROM @searchlog
        GROUP BY Region
        HAVING SUM(Duration) > 200;

    OUTPUT @res
        TO "/output/Searchlog-having.csv"
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

<span data-ttu-id="bf4c0-155">고급 집계 시나리오의 경우 U-SQL 참조 설명서에서 [집계, 분석 및 참조 기능](https://msdn.microsoft.com/en-us/library/azure/mt621335.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bf4c0-155">For advanced aggregation scenarios, see the The U-SQL reference documentation for [aggregate, analytic, and reference functions](https://msdn.microsoft.com/en-us/library/azure/mt621335.aspx)</span></span>

## <a name="next-steps"></a><span data-ttu-id="bf4c0-156">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bf4c0-156">Next steps</span></span>
* [<span data-ttu-id="bf4c0-157">Microsoft Azure 데이터 레이크 분석 개요</span><span class="sxs-lookup"><span data-stu-id="bf4c0-157">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="bf4c0-158">Visual Studio용 데이터 레이크 도구를 사용하여 U-SQL 스크립트 개발</span><span class="sxs-lookup"><span data-stu-id="bf4c0-158">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)

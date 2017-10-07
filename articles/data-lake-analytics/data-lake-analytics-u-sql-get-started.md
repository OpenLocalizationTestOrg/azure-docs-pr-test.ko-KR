---
title: "U-SQL 언어 시작 | Microsoft Docs"
description: "Hello U SQL 언어의 hello 기본 사항에 알아봅니다."
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
ms.openlocfilehash: 5edee0e0d85211e84b3d47895c53d71f0a19f083
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-u-sql"></a><span data-ttu-id="3cacc-103">U-SQL 시작</span><span class="sxs-lookup"><span data-stu-id="3cacc-103">Get started with U-SQL</span></span>
<span data-ttu-id="3cacc-104">U-SQL는 선언적 SQL 결합 하는 언어에 있는 아무 눈금에는 데이터 toolet C# 명령적으로 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cacc-104">U-SQL is a language that combines declarative SQL with imperative C# toolet you process data at any scale.</span></span> <span data-ttu-id="3cacc-105">U-SQL의 hello 확장성, 분산 쿼리 기능을 통해 Azure SQL 데이터베이스 같은 관계형 저장소에서 데이터를 효율적으로 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cacc-105">Through hello scalable, distributed-query capability of U-SQL, you can efficiently analyze data across relational stores such as Azure SQL Database.</span></span> <span data-ttu-id="3cacc-106">U-SQL을 사용하면 읽기에 대한 스키마를 적용하고 사용자 지정 논리 및 UDF를 삽입하여 구조화되지 않은 데이터를 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cacc-106">With U-SQL, you can process unstructured data by applying schema on read and inserting custom logic and UDFs.</span></span> <span data-ttu-id="3cacc-107">또한 U-SQL 포함 방법 세부적으로 제어를 제공 하는 확장성이 배율로 tooexecute 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cacc-107">Additionally, U-SQL includes extensibility that gives you fine-grained control over how tooexecute at scale.</span></span> 

## <a name="learning-resources"></a><span data-ttu-id="3cacc-108">학습 리소스</span><span class="sxs-lookup"><span data-stu-id="3cacc-108">Learning resources</span></span>

* <span data-ttu-id="3cacc-109">hello [U-SQL 자습서](http://aka.ms/usqltutorial) hello U-SQL 언어의 대부분의는 안내 방식된 연습을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cacc-109">hello [U-SQL Tutorial](http://aka.ms/usqltutorial) provides a guided walkthrough of most of hello U-SQL language.</span></span> <span data-ttu-id="3cacc-110">이 문서 toolearn U-SQL 하려는 모든 개발자가 읽는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3cacc-110">This document is recommended reading for all developers wanting toolearn U-SQL.</span></span>
* <span data-ttu-id="3cacc-111">Hello에 대 한 자세한 내용은 **U-SQL 언어 구문을**, hello 참조 [U SQL 언어 참조](http://go.microsoft.com/fwlink/p/?LinkId=691348)합니다.</span><span class="sxs-lookup"><span data-stu-id="3cacc-111">For detailed information about hello **U-SQL language syntax**, see hello [U-SQL Language Reference](http://go.microsoft.com/fwlink/p/?LinkId=691348).</span></span>
* <span data-ttu-id="3cacc-112">toounderstand hello **U-SQL 디자인 원칙**, hello Visual Studio 블로그 게시물을 참조 [소개 U-SQL – 쉽게 빅 데이터 처리 하는 언어](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/)합니다.</span><span class="sxs-lookup"><span data-stu-id="3cacc-112">toounderstand hello **U-SQL design philosophy**, see hello Visual Studio blog post [Introducing U-SQL – A Language that makes Big Data Processing Easy](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3cacc-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="3cacc-113">Prerequisites</span></span>

<span data-ttu-id="3cacc-114">이 문서에 hello U-SQL 샘플을 통한 진행 하기 전에 읽고 완료 [자습서: 데이터 레이크 도구를 사용 하 여 Visual Studio에 대 한 개발 U-SQL 스크립트](data-lake-analytics-data-lake-tools-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3cacc-114">Before you go through hello U-SQL samples in this document, read and complete [Tutorial: Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span> <span data-ttu-id="3cacc-115">해당 자습서는 Azure 데이터 레이크 도구로 U-SQL를 사용 하 여 Visual studio의 hello 메커니즘을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cacc-115">That tutorial explains hello mechanics of using U-SQL with Azure Data Lake Tools for Visual Studio.</span></span>

## <a name="your-first-u-sql-script"></a><span data-ttu-id="3cacc-116">첫 번째 U-SQL 스크립트</span><span class="sxs-lookup"><span data-stu-id="3cacc-116">Your first U-SQL script</span></span>

<span data-ttu-id="3cacc-117">U-SQL 스크립트를 다음 hello은 단순 하며 많은 측면 hello U-SQL 언어를 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cacc-117">hello following U-SQL script is simple and lets us explore many aspects hello U-SQL language.</span></span>

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
    too"/output/SearchLog-first-u-sql.csv"
    USING Outputters.Csv();
```

<span data-ttu-id="3cacc-118">이 스크립트에는 변환 단계가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3cacc-118">This script doesn't have any transformation steps.</span></span> <span data-ttu-id="3cacc-119">호출 하는 hello 소스 파일에서 읽을 `SearchLog.tsv`schematizes, 및 hello 행 집합을 다시 첫 번째 u sql.csv SearchLog 라는 파일에 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cacc-119">It reads from hello source file called `SearchLog.tsv`, schematizes it, and writes hello rowset back into a file called SearchLog-first-u-sql.csv.</span></span>

<span data-ttu-id="3cacc-120">Hello 매개 변수 다음 toohello 데이터 형식에 hello 확인 `Duration` 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="3cacc-120">Notice hello question mark next toohello data type in hello `Duration` field.</span></span> <span data-ttu-id="3cacc-121">해당 hello 의미 `Duration` 필드는 null 일 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3cacc-121">It means that hello `Duration` field could be null.</span></span>

### <a name="key-concepts"></a><span data-ttu-id="3cacc-122">주요 개념</span><span class="sxs-lookup"><span data-stu-id="3cacc-122">Key concepts</span></span>
* <span data-ttu-id="3cacc-123">**행 집합 변수**: 행 집합을 생성 하는 각 쿼리 식 tooa 변수를 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cacc-123">**Rowset variables**: Each query expression that produces a rowset can be assigned tooa variable.</span></span> <span data-ttu-id="3cacc-124">U-SQL hello T-SQL 변수 명명 패턴을 따릅니다 (`@searchlog`예를 들면) hello 스크립트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cacc-124">U-SQL follows hello T-SQL variable naming pattern (`@searchlog`, for example) in hello script.</span></span>
* <span data-ttu-id="3cacc-125">hello **추출** 키워드 파일에서 데이터를 읽고 읽기의 hello 스키마를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cacc-125">hello **EXTRACT** keyword reads data from a file and defines hello schema on read.</span></span> <span data-ttu-id="3cacc-126">`Extractors.Tsv`는 탭으로 구분된 값 파일에 대한 기본 제공 U-SQL 추출기입니다.</span><span class="sxs-lookup"><span data-stu-id="3cacc-126">`Extractors.Tsv` is a built-in U-SQL extractor for tab-separated-value files.</span></span> <span data-ttu-id="3cacc-127">사용자 지정 추출기를 개발할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cacc-127">You can develop custom extractors.</span></span>
* <span data-ttu-id="3cacc-128">hello **출력** 행 집합 tooa 파일에서 데이터를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="3cacc-128">hello **OUTPUT** writes data from a rowset tooa file.</span></span> <span data-ttu-id="3cacc-129">`Outputters.Csv()`기본 제공 U-SQL outputter toocreate 쉼표로 구분 된 값 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="3cacc-129">`Outputters.Csv()` is a built-in U-SQL outputter toocreate a comma-separated-value file.</span></span> <span data-ttu-id="3cacc-130">사용자 지정 출력기를 개발할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cacc-130">You can develop custom outputters.</span></span>

### <a name="file-paths"></a><span data-ttu-id="3cacc-131">파일 경로</span><span class="sxs-lookup"><span data-stu-id="3cacc-131">File paths</span></span>

<span data-ttu-id="3cacc-132">hello 추출 및 문의 출력 파일 경로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cacc-132">hello EXTRACT and OUTPUT statements use file paths.</span></span> <span data-ttu-id="3cacc-133">파일 경로는 절대 경로 또는 상대 경로일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cacc-133">File paths can be absolute or relative:</span></span>

<span data-ttu-id="3cacc-134">이 다음 절대 파일 경로 참조 라는 데이터 레이크 저장소의 tooa 파일 `mystore`:</span><span class="sxs-lookup"><span data-stu-id="3cacc-134">This following absolute file path refers tooa file in a Data Lake Store named `mystore`:</span></span>

    adl://mystore.azuredatalakestore.net/Samples/Data/SearchLog.tsv

<span data-ttu-id="3cacc-135">다음에 나오는 이 파일 경로는 `"/"`로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="3cacc-135">This following file path starts with `"/"`.</span></span> <span data-ttu-id="3cacc-136">Hello 기본 데이터 레이크 저장소 계정에서 tooa 파일 참조:</span><span class="sxs-lookup"><span data-stu-id="3cacc-136">It refers tooa file in hello default Data Lake Store account:</span></span>

    /output/SearchLog-first-u-sql.csv

## <a name="use-scalar-variables"></a><span data-ttu-id="3cacc-137">스칼라 변수 사용</span><span class="sxs-lookup"><span data-stu-id="3cacc-137">Use scalar variables</span></span>

<span data-ttu-id="3cacc-138">으로 사용할 수 있습니다 스칼라 변수 잘 toomake 스크립트 유지 관리 보다 쉽게 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cacc-138">You can use scalar variables as well toomake your script maintenance easier.</span></span> <span data-ttu-id="3cacc-139">으로 hello 이전 U-SQL 스크립트를 작성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cacc-139">hello previous U-SQL script can also be written as:</span></span>

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
        too@out
        USING Outputters.Csv();

## <a name="transform-rowsets"></a><span data-ttu-id="3cacc-140">변환 행 집합</span><span class="sxs-lookup"><span data-stu-id="3cacc-140">Transform rowsets</span></span>

<span data-ttu-id="3cacc-141">사용 하 여 **선택** tootransform 행 집합:</span><span class="sxs-lookup"><span data-stu-id="3cacc-141">Use **SELECT** tootransform rowsets:</span></span>

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
        too"/output/SearchLog-transform-rowsets.csv"
        USING Outputters.Csv();

<span data-ttu-id="3cacc-142">WHERE 절 사용 하 여 hello는 [C# 부울 식](https://msdn.microsoft.com/library/6a71f45d.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="3cacc-142">hello WHERE clause uses a [C# Boolean expression](https://msdn.microsoft.com/library/6a71f45d.aspx).</span></span> <span data-ttu-id="3cacc-143">Hello C# 식 언어 toodo 고유한 식 및 함수에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cacc-143">You can use hello C# expression language toodo your own expressions and functions.</span></span> <span data-ttu-id="3cacc-144">식 및 함수를 논리 결합(ANDs) 및 분리(ORs)와 결합하여 더 복잡한 필터링을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cacc-144">You can even perform more complex filtering by combining them with logical conjunctions (ANDs) and disjunctions (ORs).</span></span>

<span data-ttu-id="3cacc-145">hello 다음 스크립트에서는 hello DateTime.Parse() 메서드 및 결합 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cacc-145">hello following script uses hello DateTime.Parse() method and a conjunction.</span></span>

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
        too"/output/SearchLog-transform-datetime.csv"
        USING Outputters.Csv();

 >[!NOTE]
 ><span data-ttu-id="3cacc-146">hello 두 번째 쿼리는 두 개의 필터 hello의 합성을 만드는 hello 첫 번째 행의 hello 결과에 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cacc-146">hello second query is operating on hello result of hello first rowset, which creates a composite of hello two filters.</span></span> <span data-ttu-id="3cacc-147">변수 이름으로도 다시 사용할 수 있습니다 및 hello 이름이 어휘 적으로 범위가 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3cacc-147">You can also reuse a variable name, and hello names are scoped lexically.</span></span>

## <a name="aggregate-rowsets"></a><span data-ttu-id="3cacc-148">집계 행 집합</span><span class="sxs-lookup"><span data-stu-id="3cacc-148">Aggregate rowsets</span></span>
<span data-ttu-id="3cacc-149">친숙 한 ORDER BY, GROUP BY 및 집계 hello U-SQL 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cacc-149">U-SQL gives you hello familiar ORDER BY, GROUP BY, and aggregations.</span></span>

<span data-ttu-id="3cacc-150">hello 다음 쿼리에서 hello 총 기간 / 지역당을 찾아 다음 순서로 hello 상위 5 개 기간이 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cacc-150">hello following query finds hello total duration per region, and then displays hello top five durations in order.</span></span>

<span data-ttu-id="3cacc-151">U-SQL 행 집합에서 다음 쿼리 hello에 대 한 순서를 유지 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3cacc-151">U-SQL rowsets do not preserve their order for hello next query.</span></span> <span data-ttu-id="3cacc-152">출력, 따라서 tooorder tooadd ORDER BY toohello 출력 문이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cacc-152">Thus, tooorder an output, you need tooadd ORDER BY toohello OUTPUT statement:</span></span>

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
        too@out1
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

    OUTPUT @res
        too@out2
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

<span data-ttu-id="3cacc-153">hello U-SQL ORDER BY 절 hello FETCH 절을 사용 하 여 SELECT 식에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cacc-153">hello U-SQL ORDER BY clause requires using hello FETCH clause in a SELECT expression.</span></span>

<span data-ttu-id="3cacc-154">hello U-SQL HAVING 절에 사용 되는 toorestrict hello 출력 toogroups hello HAVING 조건에 맞는 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cacc-154">hello U-SQL HAVING clause can be used toorestrict hello output toogroups that satisfy hello HAVING condition:</span></span>

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
        too"/output/Searchlog-having.csv"
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

<span data-ttu-id="3cacc-155">집계 고급 시나리오에 대 한 hello hello U-SQL 참조 설명서를 참조 하십시오. [분석, 집계 및 함수를 참조할](https://msdn.microsoft.com/en-us/library/azure/mt621335.aspx)</span><span class="sxs-lookup"><span data-stu-id="3cacc-155">For advanced aggregation scenarios, see hello hello U-SQL reference documentation for [aggregate, analytic, and reference functions](https://msdn.microsoft.com/en-us/library/azure/mt621335.aspx)</span></span>

## <a name="next-steps"></a><span data-ttu-id="3cacc-156">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3cacc-156">Next steps</span></span>
* [<span data-ttu-id="3cacc-157">Microsoft Azure 데이터 레이크 분석 개요</span><span class="sxs-lookup"><span data-stu-id="3cacc-157">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="3cacc-158">Visual Studio용 데이터 레이크 도구를 사용하여 U-SQL 스크립트 개발</span><span class="sxs-lookup"><span data-stu-id="3cacc-158">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)

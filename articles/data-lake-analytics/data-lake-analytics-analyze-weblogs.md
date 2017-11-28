---
title: "Azure 데이터 레이크 분석을 사용 하 여 웹 사이트 aaaAnalyze 로그 | Microsoft Docs"
description: "데이터 레이크 분석을 사용 하 여 웹 사이트 tooanalyze을 기록 하는 방법에 대해 알아봅니다. "
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 3a196735-d0d9-4deb-ba68-c4b3f3be8403
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: saveenr
ms.openlocfilehash: d27aaca95ed2b643cfed7a17b0066bf7fa4a1bf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-website-logs-using-azure-data-lake-analytics"></a><span data-ttu-id="e8c1f-103">Azure Data Lake Analytics를 사용하여 웹 사이트 로그 분석</span><span class="sxs-lookup"><span data-stu-id="e8c1f-103">Analyze Website logs using Azure Data Lake Analytics</span></span>
<span data-ttu-id="e8c1f-104">Toovisit hello 웹 사이트를 만들려고 tooanalyze 웹 사이트 로그는 참조 페이지 찾기에 특히 Data Lake 분석을 사용 하 여 오류가 발생 했습니다 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e8c1f-104">Learn how tooanalyze website logs using Data Lake Analytics, especially on finding out which referrers ran into errors when they tried toovisit hello website.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e8c1f-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="e8c1f-105">Prerequisites</span></span>
* <span data-ttu-id="e8c1f-106">**Visual Studio 2015 또는 Visual Studio 2013**.</span><span class="sxs-lookup"><span data-stu-id="e8c1f-106">**Visual Studio 2015 or Visual Studio 2013**.</span></span>
* <span data-ttu-id="e8c1f-107">**[Visual Studio용 Data Lake 도구](http://aka.ms/adltoolsvs)**.</span><span class="sxs-lookup"><span data-stu-id="e8c1f-107">**[Data Lake Tools for Visual Studio](http://aka.ms/adltoolsvs)**.</span></span>

    <span data-ttu-id="e8c1f-108">데이터 레이크 Tools for Visual Studio가 설치 되 면 표시 됩니다는 **데이터 레이크** hello에서 항목 **도구** Visual Studio에서 메뉴:</span><span class="sxs-lookup"><span data-stu-id="e8c1f-108">Once Data Lake Tools for Visual Studio is installed, you will see a **Data Lake** item in hello **Tools** menu in Visual Studio:</span></span>

    ![U-SQL Visual Studio 메뉴](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-menu.png)
* <span data-ttu-id="e8c1f-110">**데이터 레이크 분석 워크 로드와 hello 데이터 레이크 Tools for Visual Studio에 대 한 기본 지식이**합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c1f-110">**Basic knowledge of Data Lake Analytics and hello Data Lake Tools for Visual Studio**.</span></span> <span data-ttu-id="e8c1f-111">시작 tooget 참조:</span><span class="sxs-lookup"><span data-stu-id="e8c1f-111">tooget started, see:</span></span>

  * <span data-ttu-id="e8c1f-112">[Visual Studio용 데이터 레이크 도구를 사용하여 U-SQL 스크립트 개발](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e8c1f-112">[Develop U-SQL script using Data Lake tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="e8c1f-113">**데이터 레이크 분석 계정.**</span><span class="sxs-lookup"><span data-stu-id="e8c1f-113">**A Data Lake Analytics account.**</span></span>  <span data-ttu-id="e8c1f-114">[Azure Data Lake Analytics 계정 만들기](data-lake-analytics-get-started-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e8c1f-114">See [Create an Azure Data Lake Analytics account](data-lake-analytics-get-started-portal.md).</span></span>
* <span data-ttu-id="e8c1f-115">**Hello 샘플 데이터 toohello Data Lake 분석 계정에 업로드 합니다.**</span><span class="sxs-lookup"><span data-stu-id="e8c1f-115">**Upload hello sample data toohello Data Lake Analytics account.**</span></span> <span data-ttu-id="e8c1f-116">참조 [toocopy 예제 데이터 파일과](data-lake-analytics-get-started-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c1f-116">See [toocopy sample data files](data-lake-analytics-get-started-portal.md).</span></span>

    <span data-ttu-id="e8c1f-117">데이터 레이크 분석 작업 toorun 일부 데이터가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c1f-117">toorun a Data Lake Analytics job, you will need some data.</span></span> <span data-ttu-id="e8c1f-118">데이터 레이크 도구 hello 업로드 데이터를 지 원하는 경우에이 자습서 쉽게 toofollow hello 포털 tooupload hello 샘플 데이터 toomake 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c1f-118">Even though hello Data Lake Tools supports uploading data, you will use hello portal tooupload hello sample data toomake this tutorial easier toofollow.</span></span>

## <a name="connect-tooazure"></a><span data-ttu-id="e8c1f-119">TooAzure 연결</span><span class="sxs-lookup"><span data-stu-id="e8c1f-119">Connect tooAzure</span></span>
<span data-ttu-id="e8c1f-120">빌드 및 모든 U-SQL 스크립트를 테스트 수, 전에 tooAzure 먼저 연결 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c1f-120">Before you can build and test any U-SQL scripts, you must first connect tooAzure.</span></span>

<span data-ttu-id="e8c1f-121">**tooconnect tooData Lake 분석**</span><span class="sxs-lookup"><span data-stu-id="e8c1f-121">**tooconnect tooData Lake Analytics**</span></span>

1. <span data-ttu-id="e8c1f-122">Visual Studio를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e8c1f-122">Open Visual Studio.</span></span>
2. <span data-ttu-id="e8c1f-123">**Data Lake > 옵션 및 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c1f-123">Click **Data Lake > Options and Settings**.</span></span>
3. <span data-ttu-id="e8c1f-124">클릭 **로그인**, 또는 **사용자 변경** 경우 사용자가에 로그인을 hello 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="e8c1f-124">Click **Sign In**, or **Change User** if someone has signed in, and follow hello instructions.</span></span>
4. <span data-ttu-id="e8c1f-125">클릭 **확인** tooclose hello 옵션 및 설정 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="e8c1f-125">Click **OK** tooclose hello Options and Settings dialog.</span></span>

<span data-ttu-id="e8c1f-126">**toobrowse Data Lake 분석 계정**</span><span class="sxs-lookup"><span data-stu-id="e8c1f-126">**toobrowse your Data Lake Analytics accounts**</span></span>

1. <span data-ttu-id="e8c1f-127">Visual Studio에서 **CTRL+ALT+S**를 눌러 **서버 탐색기**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e8c1f-127">From Visual Studio, open **Server Explorer** by press **CTRL+ALT+S**.</span></span>
2. <span data-ttu-id="e8c1f-128">**서버 탐색기**에서 **Azure**를 확장한 후 **Data Lake Analytics**을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c1f-128">From **Server Explorer**, expand **Azure**, and then expand **Data Lake Analytics**.</span></span> <span data-ttu-id="e8c1f-129">계정이 있을 경우 해당 데이터 레이크 분석 계정 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8c1f-129">You shall see a list of your Data Lake Analytics accounts if there are any.</span></span> <span data-ttu-id="e8c1f-130">Data Lake 분석 계정 hello studio에서 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e8c1f-130">You cannot create Data Lake Analytics accounts from hello studio.</span></span> <span data-ttu-id="e8c1f-131">계정에는 toocreate 참조 [Azure 포털을 사용 하 여 Azure Data Lake 분석 시작](data-lake-analytics-get-started-portal.md) 또는 [Azure PowerShell을 사용 하 여 Azure Data Lake 분석 시작](data-lake-analytics-get-started-powershell.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c1f-131">toocreate an account, see [Get Started with Azure Data Lake Analytics using Azure Portal](data-lake-analytics-get-started-portal.md) or [Get Started with Azure Data Lake Analytics using Azure PowerShell](data-lake-analytics-get-started-powershell.md).</span></span>

## <a name="develop-u-sql-application"></a><span data-ttu-id="e8c1f-132">U-SQL 응용 프로그램 개발</span><span class="sxs-lookup"><span data-stu-id="e8c1f-132">Develop U-SQL application</span></span>
<span data-ttu-id="e8c1f-133">U-SQL 응용 프로그램은 대부분 U-SQL 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="e8c1f-133">A U-SQL application is mostly a U-SQL script.</span></span> <span data-ttu-id="e8c1f-134">U SQL에 대해 자세히 toolearn 참조 [U-SQL 시작](data-lake-analytics-u-sql-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c1f-134">toolearn more about U-SQL, see [Get started with U-SQL](data-lake-analytics-u-sql-get-started.md).</span></span>

<span data-ttu-id="e8c1f-135">추가 사용자 정의 연산자 toohello 응용 프로그램을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8c1f-135">You can add addition user-defined operators toohello application.</span></span>  <span data-ttu-id="e8c1f-136">자세한 내용은 [데이터 레이크 분석 작업을 위한 U-SQL 사용자 정의 연산자 개발](data-lake-analytics-u-sql-develop-user-defined-operators.md)을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="e8c1f-136">For more information, see [Develop U-SQL user defined operators for Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-user-defined-operators.md).</span></span>

<span data-ttu-id="e8c1f-137">**toocreate Data Lake 분석 작업을 제출 하 고**</span><span class="sxs-lookup"><span data-stu-id="e8c1f-137">**toocreate and submit a Data Lake Analytics job**</span></span>

1. <span data-ttu-id="e8c1f-138">Hello 클릭 **파일 > 새로 만들기 > 프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c1f-138">Click hello **File > New > Project**.</span></span>
2. <span data-ttu-id="e8c1f-139">Hello U-SQL 프로젝트 형식을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c1f-139">Select hello U-SQL Project type.</span></span>

    ![새 U-SQL Visual Studio 프로젝트](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-new-project.png)
3. <span data-ttu-id="e8c1f-141">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c1f-141">Click **OK**.</span></span> <span data-ttu-id="e8c1f-142">Visual studio는 Script.usql 파일로 솔루션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e8c1f-142">Visual studio creates a solution with a Script.usql file.</span></span>
4. <span data-ttu-id="e8c1f-143">Hello 스크립트 hello Script.usql 파일에 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c1f-143">Enter hello following script into hello Script.usql file:</span></span>

        // Create a database for easy reuse, so you don't need tooread from a file every time.
        CREATE DATABASE IF NOT EXISTS SampleDBTutorials;

        // Create a Table valued function. TVF ensures that your jobs fetch data from hello weblog file with hello correct schema.
        DROP FUNCTION IF EXISTS SampleDBTutorials.dbo.WeblogsView;
        CREATE FUNCTION SampleDBTutorials.dbo.WeblogsView()
        RETURNS @result TABLE
        (
            s_date DateTime,
            s_time string,
            s_sitename string,
            cs_method string,
            cs_uristem string,
            cs_uriquery string,
            s_port int,
            cs_username string,
            c_ip string,
            cs_useragent string,
            cs_cookie string,
            cs_referer string,
            cs_host string,
            sc_status int,
            sc_substatus int,
            sc_win32status int,
            sc_bytes int,
            cs_bytes int,
            s_timetaken int
        )
        AS
        BEGIN

            @result = EXTRACT
                s_date DateTime,
                s_time string,
                s_sitename string,
                cs_method string,
                cs_uristem string,
                cs_uriquery string,
                s_port int,
                cs_username string,
                c_ip string,
                cs_useragent string,
                cs_cookie string,
                cs_referer string,
                cs_host string,
                sc_status int,
                sc_substatus int,
                sc_win32status int,
                sc_bytes int,
                cs_bytes int,
                s_timetaken int
            FROM @"/Samples/Data/WebLog.log"
            USING Extractors.Text(delimiter:' ');
            RETURN;
        END;

        // Create a table for storing referrers and status
        DROP TABLE IF EXISTS SampleDBTutorials.dbo.ReferrersPerDay;
        @weblog = SampleDBTutorials.dbo.WeblogsView();
        CREATE TABLE SampleDBTutorials.dbo.ReferrersPerDay
        (
            INDEX idx1
            CLUSTERED(Year ASC)
            DISTRIBUTED BY HASH(Year)
        ) AS

        SELECT s_date.Year AS Year,
            s_date.Month AS Month,
            s_date.Day AS Day,
            cs_referer,
            sc_status,
            COUNT(DISTINCT c_ip) AS cnt
        FROM @weblog
        GROUP BY s_date,
                cs_referer,
                sc_status;

    <span data-ttu-id="e8c1f-144">toounderstand hello U SQL 참조 [데이터 레이크 분석 U-SQL 언어 시작](data-lake-analytics-u-sql-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c1f-144">toounderstand hello U-SQL, see [Get started with Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>    
5. <span data-ttu-id="e8c1f-145">새로운 U-SQL 스크립트 tooyour 프로젝트에 추가 하 고 hello 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c1f-145">Add a new U-SQL script tooyour project and enter hello following:</span></span>

        // Query hello referrers that ran into errors
        @content =
            SELECT *
            FROM SampleDBTutorials.dbo.ReferrersPerDay
            WHERE sc_status >=400 AND sc_status < 500;

        OUTPUT @content
        too@"/Samples/Outputs/UnsuccessfulResponses.log"
        USING Outputters.Tsv();
6. <span data-ttu-id="e8c1f-146">U-SQL 스크립트를 첫 번째 백 toohello 전환한 다음 toohello **전송** 단추, 분석 계정을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c1f-146">Switch back toohello first U-SQL script and next toohello **Submit** button, specify your Analytics account.</span></span>
7. <span data-ttu-id="e8c1f-147">**솔루션 탐색기**에서 **Script.usql**을 마우스 오른쪽 클릭하고 **빌드 스크립트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c1f-147">From **Solution Explorer**, right click **Script.usql**, and then click **Build Script**.</span></span> <span data-ttu-id="e8c1f-148">Hello 출력 창에 hello 결과 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c1f-148">Verify hello results in hello Output pane.</span></span>
8. <span data-ttu-id="e8c1f-149">**솔루션 탐색기**에서 **Script.usql**을 마우스 오른쪽 단추로 클릭하고 **스크립트 제출**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c1f-149">From **Solution Explorer**, right click **Script.usql**, and then click **Submit Script**.</span></span>
9. <span data-ttu-id="e8c1f-150">Hello 확인 **분석 계정** 는 hello toorun hello 작업 하 고 클릭 하나 **전송**합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c1f-150">Verify hello **Analytics Account** is hello one where you want toorun hello job, and then click **Submit**.</span></span> <span data-ttu-id="e8c1f-151">제출 결과 및 작업 링크는 hello 전송이 완료 되 면 Visual Studio 결과 창에 대 한 hello 데이터 레이크 도구에서에서 사용할 수 있는입니다.</span><span class="sxs-lookup"><span data-stu-id="e8c1f-151">Submission results and job link are available in hello Data Lake Tools for Visual Studio Results window when hello submission is completed.</span></span>
10. <span data-ttu-id="e8c1f-152">Hello 작업이 성공적으로 완료 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="e8c1f-152">Wait until hello job is completed successfully.</span></span>  <span data-ttu-id="e8c1f-153">Hello 작업에 실패 한 경우 hello 소스 파일을 가능성이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e8c1f-153">If hello job failed, it is most likely missing hello source file.</span></span>  <span data-ttu-id="e8c1f-154">이 자습서의 hello 필수 구성 요소 섹션을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="e8c1f-154">Please see hello Prerequisite section of this tutorial.</span></span> <span data-ttu-id="e8c1f-155">추가적인 문제 해결 정보는 [Azure 데이터 레이크 분석 작업 모니터링 및 문제 해결](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e8c1f-155">For additional troubleshooting information, see [Monitor and troubleshoot Azure Data Lake Analytics jobs](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span></span>

    <span data-ttu-id="e8c1f-156">Hello 작업이 완료 될 때 hello 화면에 따라 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c1f-156">When hello job is completed, you shall see hello following screen:</span></span>

    ![데이터 레이크 분석은 웹 로그와 웹 사이트 로그를 분석합니다.](./media/data-lake-analytics-analyze-weblogs/data-lake-analytics-analyze-weblogs-job-completed.png)
11. <span data-ttu-id="e8c1f-158">**Script1.usql**에 대해 7-10단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c1f-158">Now repeat steps 7- 10 for **Script1.usql**.</span></span>

<span data-ttu-id="e8c1f-159">**toosee hello 작업 출력**</span><span class="sxs-lookup"><span data-stu-id="e8c1f-159">**toosee hello job output**</span></span>

1. <span data-ttu-id="e8c1f-160">**서버 탐색기**를 확장 하 고 **Azure**를 확장 하 고 **Data Lake 분석**, Data Lake 분석 계정, **저장소계정**hello 기본 데이터 레이크 저장소 계정을 마우스 오른쪽 단추로 클릭 한 다음 클릭 **탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c1f-160">From **Server Explorer**, expand **Azure**, expand **Data Lake Analytics**, expand your Data Lake Analytics account, expand **Storage Accounts**, right-click hello default Data Lake Storage account, and then click **Explorer**.</span></span>
2. <span data-ttu-id="e8c1f-161">두 번 클릭 **샘플** tooopen hello 폴더를 차례로 두 번 클릭 한 다음 **출력**합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c1f-161">Double-click **Samples** tooopen hello folder, and then double-click **Outputs**.</span></span>
3. <span data-ttu-id="e8c1f-162">**UnsuccessfulResponsees.log**를 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c1f-162">Double-click **UnsuccessfulResponsees.log**.</span></span>
4. <span data-ttu-id="e8c1f-163">Toohello 출력 직접 순서 toonavigate에서 hello 작업의 hello 그래프 뷰 내 hello 출력 파일을 두 번 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8c1f-163">You can also double-click hello output file inside hello graph view of hello job in order toonavigate directly toohello output.</span></span>

## <a name="see-also"></a><span data-ttu-id="e8c1f-164">참고 항목</span><span class="sxs-lookup"><span data-stu-id="e8c1f-164">See also</span></span>
<span data-ttu-id="e8c1f-165">다양 한 도구를 사용 하 여 Data Lake 분석 시작 tooget 참조:</span><span class="sxs-lookup"><span data-stu-id="e8c1f-165">tooget started with Data Lake Analytics using different tools, see:</span></span>

* [<span data-ttu-id="e8c1f-166">Azure 포털을 사용하여 데이터 레이크 분석 시작</span><span class="sxs-lookup"><span data-stu-id="e8c1f-166">Get started with Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="e8c1f-167">Azure PowerShell을 사용하여 데이터 레이크 분석 시작</span><span class="sxs-lookup"><span data-stu-id="e8c1f-167">Get started with Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="e8c1f-168">.NET SDK를 사용하여 데이터 레이크 분석 시작</span><span class="sxs-lookup"><span data-stu-id="e8c1f-168">Get started with Data Lake Analytics using .NET SDK</span></span>](data-lake-analytics-get-started-net-sdk.md)

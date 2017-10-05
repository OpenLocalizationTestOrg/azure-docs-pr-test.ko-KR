---
title: "Azure Data Lake Analytics를 사용하여 웹 사이트 로그 분석 | Microsoft Docs"
description: "데이터 레이크 분석을 사용하여 웹 사이트 로그를 분석하는 방법에 대해 알아봅니다. "
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
ms.openlocfilehash: 25fbbe97d26491fc421f4821315761c18e523ec8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="analyze-website-logs-using-azure-data-lake-analytics"></a><span data-ttu-id="feb1c-103">Azure Data Lake Analytics를 사용하여 웹 사이트 로그 분석</span><span class="sxs-lookup"><span data-stu-id="feb1c-103">Analyze Website logs using Azure Data Lake Analytics</span></span>
<span data-ttu-id="feb1c-104">데이터 레이크 분석을 사용하여 웹 사이트 로그를 분석하는 방법, 특히 웹 사이트를 방문하려고 할 때 참조 페이지에 오류가 발생한 경우에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="feb1c-104">Learn how to analyze website logs using Data Lake Analytics, especially on finding out which referrers ran into errors when they tried to visit the website.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="feb1c-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="feb1c-105">Prerequisites</span></span>
* <span data-ttu-id="feb1c-106">**Visual Studio 2015 또는 Visual Studio 2013**.</span><span class="sxs-lookup"><span data-stu-id="feb1c-106">**Visual Studio 2015 or Visual Studio 2013**.</span></span>
* <span data-ttu-id="feb1c-107">**[Visual Studio용 Data Lake 도구](http://aka.ms/adltoolsvs)**.</span><span class="sxs-lookup"><span data-stu-id="feb1c-107">**[Data Lake Tools for Visual Studio](http://aka.ms/adltoolsvs)**.</span></span>

    <span data-ttu-id="feb1c-108">Visual Studio용 데이터 레이크 도구를 설치하면 Visual Studio의 **도구** 메뉴에서 **Data Lake** 항목을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="feb1c-108">Once Data Lake Tools for Visual Studio is installed, you will see a **Data Lake** item in the **Tools** menu in Visual Studio:</span></span>

    ![U-SQL Visual Studio 메뉴](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-menu.png)
* <span data-ttu-id="feb1c-110">**데이터 레이크 분석 및 Visual Studio용 데이터 레이크 도구에 대한 기본 지식**.</span><span class="sxs-lookup"><span data-stu-id="feb1c-110">**Basic knowledge of Data Lake Analytics and the Data Lake Tools for Visual Studio**.</span></span> <span data-ttu-id="feb1c-111">시작하려면 다음을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="feb1c-111">To get started, see:</span></span>

  * <span data-ttu-id="feb1c-112">[Visual Studio용 데이터 레이크 도구를 사용하여 U-SQL 스크립트 개발](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="feb1c-112">[Develop U-SQL script using Data Lake tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="feb1c-113">**데이터 레이크 분석 계정.**</span><span class="sxs-lookup"><span data-stu-id="feb1c-113">**A Data Lake Analytics account.**</span></span>  <span data-ttu-id="feb1c-114">[Azure Data Lake Analytics 계정 만들기](data-lake-analytics-get-started-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="feb1c-114">See [Create an Azure Data Lake Analytics account](data-lake-analytics-get-started-portal.md).</span></span>
* <span data-ttu-id="feb1c-115">**데이터 레이크 분석 계정에 샘플 데이터를 업로드합니다.**</span><span class="sxs-lookup"><span data-stu-id="feb1c-115">**Upload the sample data to the Data Lake Analytics account.**</span></span> <span data-ttu-id="feb1c-116">[샘플 데이터 파일 복사하기](data-lake-analytics-get-started-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="feb1c-116">See [To copy sample data files](data-lake-analytics-get-started-portal.md).</span></span>

    <span data-ttu-id="feb1c-117">데이터 레이크 분석 작업을 실행하려면 일부 데이터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="feb1c-117">To run a Data Lake Analytics job, you will need some data.</span></span> <span data-ttu-id="feb1c-118">데이터 레이크 도구가 데이터 업로드를 지원하지만 이 자습서를 더 쉽게 수행하기 위해 해당 포털을 사용하여 샘플 데이터를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="feb1c-118">Even though the Data Lake Tools supports uploading data, you will use the portal to upload the sample data to make this tutorial easier to follow.</span></span>

## <a name="connect-to-azure"></a><span data-ttu-id="feb1c-119">Azure에 연결</span><span class="sxs-lookup"><span data-stu-id="feb1c-119">Connect to Azure</span></span>
<span data-ttu-id="feb1c-120">모든 U-SQL 스크립트를 빌드하거나 테스트하기 전에 먼저 Azure에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="feb1c-120">Before you can build and test any U-SQL scripts, you must first connect to Azure.</span></span>

<span data-ttu-id="feb1c-121">**데이터 레이크 분석에 연결하려면**</span><span class="sxs-lookup"><span data-stu-id="feb1c-121">**To connect to Data Lake Analytics**</span></span>

1. <span data-ttu-id="feb1c-122">Visual Studio를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="feb1c-122">Open Visual Studio.</span></span>
2. <span data-ttu-id="feb1c-123">**Data Lake > 옵션 및 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="feb1c-123">Click **Data Lake > Options and Settings**.</span></span>
3. <span data-ttu-id="feb1c-124">**로그인** 또는 **사용자 변경**을 클릭하거나, 특정 사용자가 로그인한 경우 다음 지침을 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="feb1c-124">Click **Sign In**, or **Change User** if someone has signed in, and follow the instructions.</span></span>
4. <span data-ttu-id="feb1c-125">**확인** 을 클릭하여 해당 옵션 및 설정 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="feb1c-125">Click **OK** to close the Options and Settings dialog.</span></span>

<span data-ttu-id="feb1c-126">**데이터 레이크 분석 계정 찾아보기**</span><span class="sxs-lookup"><span data-stu-id="feb1c-126">**To browse your Data Lake Analytics accounts**</span></span>

1. <span data-ttu-id="feb1c-127">Visual Studio에서 **CTRL+ALT+S**를 눌러 **서버 탐색기**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="feb1c-127">From Visual Studio, open **Server Explorer** by press **CTRL+ALT+S**.</span></span>
2. <span data-ttu-id="feb1c-128">**서버 탐색기**에서 **Azure**를 확장한 후 **Data Lake Analytics**을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="feb1c-128">From **Server Explorer**, expand **Azure**, and then expand **Data Lake Analytics**.</span></span> <span data-ttu-id="feb1c-129">계정이 있을 경우 해당 데이터 레이크 분석 계정 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="feb1c-129">You shall see a list of your Data Lake Analytics accounts if there are any.</span></span> <span data-ttu-id="feb1c-130">Studio에서 데이터 레이크 분석 계정을 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="feb1c-130">You cannot create Data Lake Analytics accounts from the studio.</span></span> <span data-ttu-id="feb1c-131">계정을 만들려면 [Azure Portal을 사용하여 Azure Data Lake Analytics 시작](data-lake-analytics-get-started-portal.md) 또는 [Azure PowerShell을 사용하여 Azure Data Lake Analytics 시작](data-lake-analytics-get-started-powershell.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="feb1c-131">To create an account, see [Get Started with Azure Data Lake Analytics using Azure Portal](data-lake-analytics-get-started-portal.md) or [Get Started with Azure Data Lake Analytics using Azure PowerShell](data-lake-analytics-get-started-powershell.md).</span></span>

## <a name="develop-u-sql-application"></a><span data-ttu-id="feb1c-132">U-SQL 응용 프로그램 개발</span><span class="sxs-lookup"><span data-stu-id="feb1c-132">Develop U-SQL application</span></span>
<span data-ttu-id="feb1c-133">U-SQL 응용 프로그램은 대부분 U-SQL 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="feb1c-133">A U-SQL application is mostly a U-SQL script.</span></span> <span data-ttu-id="feb1c-134">U-SQL에 대한 자세한 내용은 [U-SQL 시작](data-lake-analytics-u-sql-get-started.md)을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="feb1c-134">To learn more about U-SQL, see [Get started with U-SQL](data-lake-analytics-u-sql-get-started.md).</span></span>

<span data-ttu-id="feb1c-135">해당 응용 프로그램에 더하기 사용자 정의 연산자를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="feb1c-135">You can add addition user-defined operators to the application.</span></span>  <span data-ttu-id="feb1c-136">자세한 내용은 [데이터 레이크 분석 작업을 위한 U-SQL 사용자 정의 연산자 개발](data-lake-analytics-u-sql-develop-user-defined-operators.md)을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="feb1c-136">For more information, see [Develop U-SQL user defined operators for Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-user-defined-operators.md).</span></span>

<span data-ttu-id="feb1c-137">**데이터 레이크 분석 작업 만들기 및 제출하기**</span><span class="sxs-lookup"><span data-stu-id="feb1c-137">**To create and submit a Data Lake Analytics job**</span></span>

1. <span data-ttu-id="feb1c-138">**파일 > 새로 만들기 > 프로젝트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="feb1c-138">Click the **File > New > Project**.</span></span>
2. <span data-ttu-id="feb1c-139">U-SQL 프로젝트 형식을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="feb1c-139">Select the U-SQL Project type.</span></span>

    ![새 U-SQL Visual Studio 프로젝트](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-new-project.png)
3. <span data-ttu-id="feb1c-141">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="feb1c-141">Click **OK**.</span></span> <span data-ttu-id="feb1c-142">Visual studio는 Script.usql 파일로 솔루션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="feb1c-142">Visual studio creates a solution with a Script.usql file.</span></span>
4. <span data-ttu-id="feb1c-143">Script.usql 파일에 다음 스크립트를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="feb1c-143">Enter the following script into the Script.usql file:</span></span>

        // Create a database for easy reuse, so you don't need to read from a file every time.
        CREATE DATABASE IF NOT EXISTS SampleDBTutorials;

        // Create a Table valued function. TVF ensures that your jobs fetch data from the weblog file with the correct schema.
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

    <span data-ttu-id="feb1c-144">U-SQL을 이해하려면 [데이터 레이크 분석 U-SQL 언어 시작](data-lake-analytics-u-sql-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="feb1c-144">To understand the U-SQL, see [Get started with Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>    
5. <span data-ttu-id="feb1c-145">새 U SQL 스크립트를 프로젝트에 추가하고 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="feb1c-145">Add a new U-SQL script to your project and enter the following:</span></span>

        // Query the referrers that ran into errors
        @content =
            SELECT *
            FROM SampleDBTutorials.dbo.ReferrersPerDay
            WHERE sc_status >=400 AND sc_status < 500;

        OUTPUT @content
        TO @"/Samples/Outputs/UnsuccessfulResponses.log"
        USING Outputters.Tsv();
6. <span data-ttu-id="feb1c-146">첫 번째 U-SQL 스크립트로 다시 전환하고 **제출** 단추 옆에 해당 분석 계정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="feb1c-146">Switch back to the first U-SQL script and next to the **Submit** button, specify your Analytics account.</span></span>
7. <span data-ttu-id="feb1c-147">**솔루션 탐색기**에서 **Script.usql**을 마우스 오른쪽 클릭하고 **빌드 스크립트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="feb1c-147">From **Solution Explorer**, right click **Script.usql**, and then click **Build Script**.</span></span> <span data-ttu-id="feb1c-148">출력 창에서 결과를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="feb1c-148">Verify the results in the Output pane.</span></span>
8. <span data-ttu-id="feb1c-149">**솔루션 탐색기**에서 **Script.usql**을 마우스 오른쪽 단추로 클릭하고 **스크립트 제출**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="feb1c-149">From **Solution Explorer**, right click **Script.usql**, and then click **Submit Script**.</span></span>
9. <span data-ttu-id="feb1c-150">**분석 계정**이 실행하려는 작업에 있는지 확인하고 **제출**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="feb1c-150">Verify the **Analytics Account** is the one where you want to run the job, and then click **Submit**.</span></span> <span data-ttu-id="feb1c-151">제출이 완료되면 Visual Studio용 데이터 레이크 도구 결과 창에서 제출 결과 및 작업 링크를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="feb1c-151">Submission results and job link are available in the Data Lake Tools for Visual Studio Results window when the submission is completed.</span></span>
10. <span data-ttu-id="feb1c-152">작업이 성공적으로 완료될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="feb1c-152">Wait until the job is completed successfully.</span></span>  <span data-ttu-id="feb1c-153">작업이 실패한 경우 대부분 원본 파일이 손실되었을 가능성이 큽니다.</span><span class="sxs-lookup"><span data-stu-id="feb1c-153">If the job failed, it is most likely missing the source file.</span></span>  <span data-ttu-id="feb1c-154">이 자습서의 필수 조건 섹션을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="feb1c-154">Please see the Prerequisite section of this tutorial.</span></span> <span data-ttu-id="feb1c-155">추가적인 문제 해결 정보는 [Azure 데이터 레이크 분석 작업 모니터링 및 문제 해결](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="feb1c-155">For additional troubleshooting information, see [Monitor and troubleshoot Azure Data Lake Analytics jobs](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span></span>

    <span data-ttu-id="feb1c-156">해당 작업이 완료되면 다음 화면이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="feb1c-156">When the job is completed, you shall see the following screen:</span></span>

    ![데이터 레이크 분석은 웹 로그와 웹 사이트 로그를 분석합니다.](./media/data-lake-analytics-analyze-weblogs/data-lake-analytics-analyze-weblogs-job-completed.png)
11. <span data-ttu-id="feb1c-158">**Script1.usql**에 대해 7-10단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="feb1c-158">Now repeat steps 7- 10 for **Script1.usql**.</span></span>

<span data-ttu-id="feb1c-159">**작업 출력 보기**</span><span class="sxs-lookup"><span data-stu-id="feb1c-159">**To see the job output**</span></span>

1. <span data-ttu-id="feb1c-160">**서버 탐색기**에서 **Azure**, **Data Lake Analytics**, Data Lake Analytics 계정, **저장소 계정**을 차례로 확장하고 기본 Data Lake 저장소 계정을 마우스 오른쪽 단추로 클릭한 다음 **탐색기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="feb1c-160">From **Server Explorer**, expand **Azure**, expand **Data Lake Analytics**, expand your Data Lake Analytics account, expand **Storage Accounts**, right-click the default Data Lake Storage account, and then click **Explorer**.</span></span>
2. <span data-ttu-id="feb1c-161">**샘플**을 두 번 클릭하여 해당 폴더를 연 다음 **출력**을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="feb1c-161">Double-click **Samples** to open the folder, and then double-click **Outputs**.</span></span>
3. <span data-ttu-id="feb1c-162">**UnsuccessfulResponsees.log**를 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="feb1c-162">Double-click **UnsuccessfulResponsees.log**.</span></span>
4. <span data-ttu-id="feb1c-163">출력 작업을 직접 탐색하기 위해 해당 작업의 그래프 뷰 내부에 있는 출력 파일을 두 번 클릭할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="feb1c-163">You can also double-click the output file inside the graph view of the job in order to navigate directly to the output.</span></span>

## <a name="see-also"></a><span data-ttu-id="feb1c-164">참고 항목</span><span class="sxs-lookup"><span data-stu-id="feb1c-164">See also</span></span>
<span data-ttu-id="feb1c-165">다른 도구를 사용하여 데이터 레이크 분석을 시작하려면 다음을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="feb1c-165">To get started with Data Lake Analytics using different tools, see:</span></span>

* [<span data-ttu-id="feb1c-166">Azure 포털을 사용하여 데이터 레이크 분석 시작</span><span class="sxs-lookup"><span data-stu-id="feb1c-166">Get started with Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="feb1c-167">Azure PowerShell을 사용하여 데이터 레이크 분석 시작</span><span class="sxs-lookup"><span data-stu-id="feb1c-167">Get started with Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="feb1c-168">.NET SDK를 사용하여 데이터 레이크 분석 시작</span><span class="sxs-lookup"><span data-stu-id="feb1c-168">Get started with Data Lake Analytics using .NET SDK</span></span>](data-lake-analytics-get-started-net-sdk.md)

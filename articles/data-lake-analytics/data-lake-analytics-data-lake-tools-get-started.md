---
title: "Visual Studio에 대 한 데이터 레이크 도구를 사용 하 여 aaaDevelop U-SQL 스크립트 | Microsoft Docs"
description: "Tooinstall 데이터 레이크 Tools for Visual Studio 방법 등에 대해 알아보기 toodevelop 및 테스트 U-SQL 스크립트입니다."
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: ad8a6992-02c7-47d4-a108-62fc5a0777a3
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/28/2017
ms.author: saveenr, yanacai
ms.openlocfilehash: 7a0c02c275b8cefecbe784ba63969cbf24a150d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-u-sql-scripts-by-using-data-lake-tools-for-visual-studio"></a><span data-ttu-id="0955c-103">Data Lake Tools for Visual Studio를 사용하여 U-SQL 스크립트 개발</span><span class="sxs-lookup"><span data-stu-id="0955c-103">Develop U-SQL scripts by using Data Lake Tools for Visual Studio</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]


<span data-ttu-id="0955c-104">자세한 내용은 toouse Visual Studio toocreate Azure Data Lake 분석 계정에 있는 작업을 정의 하는 방법을 [U-SQL](data-lake-analytics-u-sql-get-started.md), 및 toohello Data Lake 분석 서비스 작업을 제출 합니다.</span><span class="sxs-lookup"><span data-stu-id="0955c-104">Learn how toouse Visual Studio toocreate Azure Data Lake Analytics accounts, define jobs in [U-SQL](data-lake-analytics-u-sql-get-started.md), and submit jobs toohello Data Lake Analytics service.</span></span> <span data-ttu-id="0955c-105">데이터 레이크 분석에 대한 자세한 내용은 [Azure 데이터 레이크 분석 개요](data-lake-analytics-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0955c-105">For more information about Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="0955c-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="0955c-106">Prerequisites</span></span>

* <span data-ttu-id="0955c-107">**Visual Studio**: Express를 제외한 모든 버전이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="0955c-107">**Visual Studio**: All editions except Express are supported.</span></span>
    * <span data-ttu-id="0955c-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="0955c-108">Visual Studio 2017</span></span>
    * <span data-ttu-id="0955c-109">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="0955c-109">Visual Studio 2015</span></span>
    * <span data-ttu-id="0955c-110">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="0955c-110">Visual Studio 2013</span></span>
* <span data-ttu-id="0955c-111">**.NET용 Microsoft Azure SDK** 버전 2.7.1 이상.</span><span class="sxs-lookup"><span data-stu-id="0955c-111">**Microsoft Azure SDK for .NET** version 2.7.1 or later.</span></span>  <span data-ttu-id="0955c-112">Hello를 사용 하 여 설치 [웹 플랫폼 설치 관리자](http://www.microsoft.com/web/downloads/platform.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="0955c-112">Install it by using hello [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="0955c-113">**Data Lake Analytics** 계정.</span><span class="sxs-lookup"><span data-stu-id="0955c-113">A **Data Lake Analytics** account.</span></span> <span data-ttu-id="0955c-114">계정에는 toocreate 참조 [Azure 포털을 사용 하 여 Azure Data Lake 분석 시작](data-lake-analytics-get-started-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0955c-114">toocreate an account, see [Get Started with Azure Data Lake Analytics using Azure portal](data-lake-analytics-get-started-portal.md).</span></span>

## <a name="install-azure-data-lake-tools-for-visual-studio"></a><span data-ttu-id="0955c-115">Azure Data Lake Tools for Visual Studio 설치</span><span class="sxs-lookup"><span data-stu-id="0955c-115">Install Azure Data Lake Tools for Visual Studio</span></span> 

<span data-ttu-id="0955c-116">다운로드 하 여 Azure 데이터 레이크 Tools for Visual Studio 설치 [hello 다운로드 센터에서에서](http://aka.ms/adltoolsvs)합니다.</span><span class="sxs-lookup"><span data-stu-id="0955c-116">Download and install Azure Data Lake Tools for Visual Studio [from hello Download Center](http://aka.ms/adltoolsvs).</span></span> <span data-ttu-id="0955c-117">설치가 끝나면 다음을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0955c-117">After installation, note that:</span></span>
* <span data-ttu-id="0955c-118">hello **서버 탐색기** > **Azure** 노드를 포함 한 **Data Lake 분석** 노드.</span><span class="sxs-lookup"><span data-stu-id="0955c-118">hello **Server Explorer** > **Azure** node contains a **Data Lake Analytics** node.</span></span> 
* <span data-ttu-id="0955c-119">hello **도구** 메뉴에는 **데이터 레이크** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="0955c-119">hello **Tools** menu has a **Data Lake** item.</span></span>

## <a name="connect-tooan-azure-data-lake-analytics-account"></a><span data-ttu-id="0955c-120">Tooan Azure Data Lake 분석 계정을 연결 하세요.</span><span class="sxs-lookup"><span data-stu-id="0955c-120">Connect tooan Azure Data Lake Analytics account</span></span>

1. <span data-ttu-id="0955c-121">Visual Studio를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0955c-121">Open Visual Studio.</span></span>
2. <span data-ttu-id="0955c-122">**보기** > **서버 탐색기**를 선택하여 서버 탐색기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0955c-122">Open Server Explorer by selecting **View** > **Server Explorer**.</span></span>
3. <span data-ttu-id="0955c-123">**Azure**를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0955c-123">Right-click **Azure**.</span></span> <span data-ttu-id="0955c-124">그런 다음 선택 **tooMicrosoft Azure 구독 연결** hello 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="0955c-124">Then select **Connect tooMicrosoft Azure Subscription** and follow hello instructions.</span></span>
4. <span data-ttu-id="0955c-125">서버 탐색기에서 선택 **Azure** > **Data Lake Analytics**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0955c-125">In Server Explorer, select **Azure** > **Data Lake Analytics**.</span></span> <span data-ttu-id="0955c-126">Data Lake Analytics 계정 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0955c-126">You see a list of your Data Lake Analytics accounts.</span></span>


## <a name="write-your-first-u-sql-script"></a><span data-ttu-id="0955c-127">첫 번째 U-SQL 스크립트 작성</span><span class="sxs-lookup"><span data-stu-id="0955c-127">Write your first U-SQL script</span></span>

<span data-ttu-id="0955c-128">hello 텍스트 다음은 간단한 U-SQL 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="0955c-128">hello following text is a simple U-SQL script.</span></span> <span data-ttu-id="0955c-129">작은 데이터 집합 및 데이터 집합 toohello 기본 데이터 레이크 저장소 파일로 라는 쓰기 정의 `/data.csv`합니다.</span><span class="sxs-lookup"><span data-stu-id="0955c-129">It defines a small dataset and writes that dataset toohello default Data Lake Store as a file called `/data.csv`.</span></span>

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    too"/data.csv"
    USING Outputters.Csv();
```

### <a name="submit-a-data-lake-analytics-job"></a><span data-ttu-id="0955c-130">데이터 레이크 분석 작업 제출</span><span class="sxs-lookup"><span data-stu-id="0955c-130">Submit a Data Lake Analytics job</span></span>

1. <span data-ttu-id="0955c-131">**파일** > **새로 만들기** > **프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0955c-131">Select **File** > **New** > **Project**.</span></span>

2. <span data-ttu-id="0955c-132">선택 hello **U-SQL 프로젝트** 종류를 선택한 다음 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="0955c-132">Select hello **U-SQL Project** type, and then click **OK**.</span></span> <span data-ttu-id="0955c-133">Visual Studio는 **Script.usql** 파일로 솔루션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0955c-133">Visual Studio creates a solution with a **Script.usql** file.</span></span>

3. <span data-ttu-id="0955c-134">Hello에 hello 앞의 스크립트를 붙여 **Script.usql** 창.</span><span class="sxs-lookup"><span data-stu-id="0955c-134">Paste hello previous script into hello **Script.usql** window.</span></span>

4. <span data-ttu-id="0955c-135">Hello의 hello 왼쪽 위 모서리에 **Script.usql** 창의 hello Data Lake 분석 계정을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0955c-135">In hello upper-left corner of hello **Script.usql** window, specify hello Data Lake Analytics account.</span></span>

    ![U-SQL Visual Studio 프로젝트 제출](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-submit-job.png)

5. <span data-ttu-id="0955c-137">Hello의 hello 왼쪽 위 모서리에 **Script.usql** 창에서 **전송**합니다.</span><span class="sxs-lookup"><span data-stu-id="0955c-137">In hello upper-left corner of hello **Script.usql** window, select **Submit**.</span></span>
6. <span data-ttu-id="0955c-138">Hello 확인 **분석 계정**를 선택한 후 **전송**합니다.</span><span class="sxs-lookup"><span data-stu-id="0955c-138">Verify hello **Analytics Account**, and then select **Submit**.</span></span> <span data-ttu-id="0955c-139">Hello 전송이 완료 된 후 제출 결과 hello 데이터 레이크 Tools for Visual Studio 결과에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0955c-139">Submission results are available in hello Data Lake Tools for Visual Studio Results after hello submission is complete.</span></span>

    ![U-SQL Visual Studio 프로젝트 제출](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-submit-job-advanced.png)
7. <span data-ttu-id="0955c-141">toosee hello 최신 작업 상태 및 새로 고침 hello 화면을 클릭 하 여 **새로 고침**합니다.</span><span class="sxs-lookup"><span data-stu-id="0955c-141">toosee hello latest job status and refresh hello screen, click **Refresh**.</span></span> <span data-ttu-id="0955c-142">Hello 표시 hello 작업 성공 시 **작업 그래프**, **메타 데이터 작업**, **상태 기록**, 및 **진단**:</span><span class="sxs-lookup"><span data-stu-id="0955c-142">When hello job succeeds, it shows hello **Job Graph**, **MetaData Operations**, **State History**, and **Diagnostics**:</span></span>

    ![U-SQL Visual Studio 데이터 레이크 분석 작업 성능 그래프](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-performance-graph.png)

   * <span data-ttu-id="0955c-144">**작업 요약** 표시 hello hello 작업의 요약입니다.</span><span class="sxs-lookup"><span data-stu-id="0955c-144">**Job Summary** shows hello summary of hello job.</span></span>   
   * <span data-ttu-id="0955c-145">**작업 세부 정보** hello 스크립트, 리소스 및 꼭 짓 점을 포함 하 여 hello 작업에 대 한 보다 구체적인 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="0955c-145">**Job Details** shows more specific information about hello job, including hello script, resources, and vertices.</span></span>
   * <span data-ttu-id="0955c-146">**작업 그래프** hello 작업의 hello 진행률을 시각화 합니다.</span><span class="sxs-lookup"><span data-stu-id="0955c-146">**Job Graph** visualizes hello progress of hello job.</span></span>
   * <span data-ttu-id="0955c-147">**메타 데이터 작업** hello U-SQL 카탈로그에 대해 수행 된 모든 hello 작업을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0955c-147">**MetaData Operations** shows all hello actions that were taken on hello U-SQL catalog.</span></span>
   * <span data-ttu-id="0955c-148">**데이터** 모든 hello 입 / 출력을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0955c-148">**Data** shows all hello inputs and outputs.</span></span>
   * <span data-ttu-id="0955c-149">**진단**에서는 작업 실행 및 성능 최적화에 대한 고급 분석을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0955c-149">**Diagnostics** provides an advanced analysis for job execution and performance optimization.</span></span>

### <a name="toocheck-job-state"></a><span data-ttu-id="0955c-150">toocheck 작업 상태</span><span class="sxs-lookup"><span data-stu-id="0955c-150">toocheck job state</span></span>

1. <span data-ttu-id="0955c-151">서버 탐색기에서 선택 **Azure** > **Data Lake Analytics**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0955c-151">In Server Explorer, select **Azure** > **Data Lake Analytics**.</span></span> 
2. <span data-ttu-id="0955c-152">Hello Data Lake 분석 계정 이름을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="0955c-152">Expand hello Data Lake Analytics account name.</span></span>
3. <span data-ttu-id="0955c-153">**작업**을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0955c-153">Double-click **Jobs**.</span></span>
4. <span data-ttu-id="0955c-154">이전에 제출 hello 작업을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0955c-154">Select hello job that you previously submitted.</span></span>

### <a name="toosee-hello-output-of-a-job"></a><span data-ttu-id="0955c-155">작업의 toosee hello 출력</span><span class="sxs-lookup"><span data-stu-id="0955c-155">toosee hello output of a job</span></span>

1. <span data-ttu-id="0955c-156">서버 탐색기에서 제출한 toohello 작업을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="0955c-156">In Server Explorer, browse toohello job you submitted.</span></span>
2. <span data-ttu-id="0955c-157">Hello 클릭 **데이터** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0955c-157">Click hello **Data** tab.</span></span>
3. <span data-ttu-id="0955c-158">Hello에 **작업 출력** 탭, 선택 hello `"/data.csv"` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="0955c-158">In hello **Job Outputs** tab, select hello `"/data.csv"` file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0955c-159">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0955c-159">Next steps</span></span>

* [<span data-ttu-id="0955c-160">테스트 및 디버깅을 위해 고유한 워크스테이션에서 U-SQL 스크립트 실행</span><span class="sxs-lookup"><span data-stu-id="0955c-160">Run U-SQL scripts on your own workstation for testing and debugging</span></span>](data-lake-analytics-data-lake-tools-local-run.md)
* [<span data-ttu-id="0955c-161">U-SQL 작업에서 C# 코드 디버그</span><span class="sxs-lookup"><span data-stu-id="0955c-161">Debug C# code in U-SQL jobs</span></span>](data-lake-analytics-debug-u-sql-jobs.md)
* [<span data-ttu-id="0955c-162">Visual Studio 코드에 대 한 hello Azure 데이터 레이크 도구를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0955c-162">Use hello Azure Data Lake Tools for Visual Studio Code</span></span>](data-lake-analytics-data-lake-tools-for-vscode.md)

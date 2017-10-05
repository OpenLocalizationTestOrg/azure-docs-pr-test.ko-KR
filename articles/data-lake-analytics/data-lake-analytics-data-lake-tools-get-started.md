---
title: "Data Lake Tools for Visual Studio를 사용하여 U-SQL 스크립트 개발 | Microsoft Docs"
description: "Data Lake Tools for Visual Studio를 설치하고 U-SQL 스크립트를 개발 및 테스트하는 방법을 알아봅니다."
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
ms.openlocfilehash: 7bbbb08ff635477a88403a3ae6bd3486d31838ef
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="develop-u-sql-scripts-by-using-data-lake-tools-for-visual-studio"></a><span data-ttu-id="90b2e-103">Data Lake Tools for Visual Studio를 사용하여 U-SQL 스크립트 개발</span><span class="sxs-lookup"><span data-stu-id="90b2e-103">Develop U-SQL scripts by using Data Lake Tools for Visual Studio</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]


<span data-ttu-id="90b2e-104">Visual Studio를 사용하여 Azure Data Lake Analytics 계정을 만들고, [U-SQL](data-lake-analytics-u-sql-get-started.md)로 작업을 정의하고, 작업을 Data Lake Analytics 서비스에 제출하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="90b2e-104">Learn how to use Visual Studio to create Azure Data Lake Analytics accounts, define jobs in [U-SQL](data-lake-analytics-u-sql-get-started.md), and submit jobs to the Data Lake Analytics service.</span></span> <span data-ttu-id="90b2e-105">데이터 레이크 분석에 대한 자세한 내용은 [Azure 데이터 레이크 분석 개요](data-lake-analytics-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="90b2e-105">For more information about Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="90b2e-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="90b2e-106">Prerequisites</span></span>

* <span data-ttu-id="90b2e-107">**Visual Studio**: Express를 제외한 모든 버전이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="90b2e-107">**Visual Studio**: All editions except Express are supported.</span></span>
    * <span data-ttu-id="90b2e-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="90b2e-108">Visual Studio 2017</span></span>
    * <span data-ttu-id="90b2e-109">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="90b2e-109">Visual Studio 2015</span></span>
    * <span data-ttu-id="90b2e-110">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="90b2e-110">Visual Studio 2013</span></span>
* <span data-ttu-id="90b2e-111">**.NET용 Microsoft Azure SDK** 버전 2.7.1 이상.</span><span class="sxs-lookup"><span data-stu-id="90b2e-111">**Microsoft Azure SDK for .NET** version 2.7.1 or later.</span></span>  <span data-ttu-id="90b2e-112">[웹 플랫폼 설치 관리자](http://www.microsoft.com/web/downloads/platform.aspx)를 사용하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="90b2e-112">Install it by using the [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="90b2e-113">**Data Lake Analytics** 계정.</span><span class="sxs-lookup"><span data-stu-id="90b2e-113">A **Data Lake Analytics** account.</span></span> <span data-ttu-id="90b2e-114">계정을 만들려면 [Azure Portal을 사용하여 Azure Data Lake Analytics 시작](data-lake-analytics-get-started-portal.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="90b2e-114">To create an account, see [Get Started with Azure Data Lake Analytics using Azure portal](data-lake-analytics-get-started-portal.md).</span></span>

## <a name="install-azure-data-lake-tools-for-visual-studio"></a><span data-ttu-id="90b2e-115">Azure Data Lake Tools for Visual Studio 설치</span><span class="sxs-lookup"><span data-stu-id="90b2e-115">Install Azure Data Lake Tools for Visual Studio</span></span> 

<span data-ttu-id="90b2e-116">[다운로드 센터](http://aka.ms/adltoolsvs)에서 Azure Data Lake Tools for Visual Studio를 다운로드하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="90b2e-116">Download and install Azure Data Lake Tools for Visual Studio [from the Download Center](http://aka.ms/adltoolsvs).</span></span> <span data-ttu-id="90b2e-117">설치가 끝나면 다음을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90b2e-117">After installation, note that:</span></span>
* <span data-ttu-id="90b2e-118">**서버 탐색기** > **Azure** 노드에 **Data Lake Analytics** 노드가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="90b2e-118">The **Server Explorer** > **Azure** node contains a **Data Lake Analytics** node.</span></span> 
* <span data-ttu-id="90b2e-119">**도구** 메뉴에 **Data Lake** 항목이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90b2e-119">The **Tools** menu has a **Data Lake** item.</span></span>

## <a name="connect-to-an-azure-data-lake-analytics-account"></a><span data-ttu-id="90b2e-120">Azure Data Lake Analytics 계정에 연결</span><span class="sxs-lookup"><span data-stu-id="90b2e-120">Connect to an Azure Data Lake Analytics account</span></span>

1. <span data-ttu-id="90b2e-121">Visual Studio를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="90b2e-121">Open Visual Studio.</span></span>
2. <span data-ttu-id="90b2e-122">**보기** > **서버 탐색기**를 선택하여 서버 탐색기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="90b2e-122">Open Server Explorer by selecting **View** > **Server Explorer**.</span></span>
3. <span data-ttu-id="90b2e-123">**Azure**를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="90b2e-123">Right-click **Azure**.</span></span> <span data-ttu-id="90b2e-124">그런 다음 **Microsoft Azure 구독에 연결**을 클릭하고 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="90b2e-124">Then select **Connect to Microsoft Azure Subscription** and follow the instructions.</span></span>
4. <span data-ttu-id="90b2e-125">서버 탐색기에서 선택 **Azure** > **Data Lake Analytics**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="90b2e-125">In Server Explorer, select **Azure** > **Data Lake Analytics**.</span></span> <span data-ttu-id="90b2e-126">Data Lake Analytics 계정 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="90b2e-126">You see a list of your Data Lake Analytics accounts.</span></span>


## <a name="write-your-first-u-sql-script"></a><span data-ttu-id="90b2e-127">첫 번째 U-SQL 스크립트 작성</span><span class="sxs-lookup"><span data-stu-id="90b2e-127">Write your first U-SQL script</span></span>

<span data-ttu-id="90b2e-128">다음 텍스트는 간단한 U-SQL 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="90b2e-128">The following text is a simple U-SQL script.</span></span> <span data-ttu-id="90b2e-129">작은 데이터 집합을 정의하고 이 데이터 집합을 `/data.csv`라는 파일로 기본 Data Lake Store에 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="90b2e-129">It defines a small dataset and writes that dataset to the default Data Lake Store as a file called `/data.csv`.</span></span>

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    TO "/data.csv"
    USING Outputters.Csv();
```

### <a name="submit-a-data-lake-analytics-job"></a><span data-ttu-id="90b2e-130">데이터 레이크 분석 작업 제출</span><span class="sxs-lookup"><span data-stu-id="90b2e-130">Submit a Data Lake Analytics job</span></span>

1. <span data-ttu-id="90b2e-131">**파일** > **새로 만들기** > **프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="90b2e-131">Select **File** > **New** > **Project**.</span></span>

2. <span data-ttu-id="90b2e-132">**U-SQL 프로젝트** 형식을 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="90b2e-132">Select the **U-SQL Project** type, and then click **OK**.</span></span> <span data-ttu-id="90b2e-133">Visual Studio는 **Script.usql** 파일로 솔루션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="90b2e-133">Visual Studio creates a solution with a **Script.usql** file.</span></span>

3. <span data-ttu-id="90b2e-134">이전 스크립트를 **Script.usql** 창에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="90b2e-134">Paste the previous script into the **Script.usql** window.</span></span>

4. <span data-ttu-id="90b2e-135">**Script.usql** 창의 왼쪽 위 모서리에서 Data Lake Analytics 계정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="90b2e-135">In the upper-left corner of the **Script.usql** window, specify the Data Lake Analytics account.</span></span>

    ![U-SQL Visual Studio 프로젝트 제출](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-submit-job.png)

5. <span data-ttu-id="90b2e-137">**Script.usql** 창의 왼쪽 위 모서리에서 **제출**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="90b2e-137">In the upper-left corner of the **Script.usql** window, select **Submit**.</span></span>
6. <span data-ttu-id="90b2e-138">**분석 계정**을 확인한 후 **제출**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="90b2e-138">Verify the **Analytics Account**, and then select **Submit**.</span></span> <span data-ttu-id="90b2e-139">제출이 완료되면 Data Lake Tools for Visual Studio 결과에서 제출 결과를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90b2e-139">Submission results are available in the Data Lake Tools for Visual Studio Results after the submission is complete.</span></span>

    ![U-SQL Visual Studio 프로젝트 제출](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-submit-job-advanced.png)
7. <span data-ttu-id="90b2e-141">최근 작업 상태를 보고 화면을 새로 고치려면 **새로 고침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="90b2e-141">To see the latest job status and refresh the screen, click **Refresh**.</span></span> <span data-ttu-id="90b2e-142">작업이 성공하면 **작업 그래프**, **메타데이터 작업**, **상태 내역**, **진단**이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="90b2e-142">When the job succeeds, it shows the **Job Graph**, **MetaData Operations**, **State History**, and **Diagnostics**:</span></span>

    ![U-SQL Visual Studio 데이터 레이크 분석 작업 성능 그래프](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-performance-graph.png)

   * <span data-ttu-id="90b2e-144">**작업 요약**에 작업의 요약 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="90b2e-144">**Job Summary** shows the summary of the job.</span></span>   
   * <span data-ttu-id="90b2e-145">**작업 세부 정보**에는 스크립트, 리소스 및 꼭짓점을 비롯하여 작업에 대한 보다 자세한 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="90b2e-145">**Job Details** shows more specific information about the job, including the script, resources, and vertices.</span></span>
   * <span data-ttu-id="90b2e-146">**작업 그래프**는 작업의 진행률을 시각화합니다.</span><span class="sxs-lookup"><span data-stu-id="90b2e-146">**Job Graph** visualizes the progress of the job.</span></span>
   * <span data-ttu-id="90b2e-147">**메타데이터 작업**에는 U-SQL 카탈로그에서 수행된 모든 작업이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="90b2e-147">**MetaData Operations** shows all the actions that were taken on the U-SQL catalog.</span></span>
   * <span data-ttu-id="90b2e-148">**데이터**에는 모든 입력 및 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="90b2e-148">**Data** shows all the inputs and outputs.</span></span>
   * <span data-ttu-id="90b2e-149">**진단**에서는 작업 실행 및 성능 최적화에 대한 고급 분석을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="90b2e-149">**Diagnostics** provides an advanced analysis for job execution and performance optimization.</span></span>

### <a name="to-check-job-state"></a><span data-ttu-id="90b2e-150">작업 상태를 확인하려면</span><span class="sxs-lookup"><span data-stu-id="90b2e-150">To check job state</span></span>

1. <span data-ttu-id="90b2e-151">서버 탐색기에서 선택 **Azure** > **Data Lake Analytics**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="90b2e-151">In Server Explorer, select **Azure** > **Data Lake Analytics**.</span></span> 
2. <span data-ttu-id="90b2e-152">Data Lake Analytics 계정 이름을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="90b2e-152">Expand the Data Lake Analytics account name.</span></span>
3. <span data-ttu-id="90b2e-153">**작업**을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="90b2e-153">Double-click **Jobs**.</span></span>
4. <span data-ttu-id="90b2e-154">이전에 제출한 작업을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="90b2e-154">Select the job that you previously submitted.</span></span>

### <a name="to-see-the-output-of-a-job"></a><span data-ttu-id="90b2e-155">작업의 출력을 보려면</span><span class="sxs-lookup"><span data-stu-id="90b2e-155">To see the output of a job</span></span>

1. <span data-ttu-id="90b2e-156">서버 탐색기에서 제출한 작업을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="90b2e-156">In Server Explorer, browse to the job you submitted.</span></span>
2. <span data-ttu-id="90b2e-157">**데이터** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="90b2e-157">Click the **Data** tab.</span></span>
3. <span data-ttu-id="90b2e-158">**작업 출력** 탭에서 `"/data.csv"` 파일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="90b2e-158">In the **Job Outputs** tab, select the `"/data.csv"` file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="90b2e-159">다음 단계</span><span class="sxs-lookup"><span data-stu-id="90b2e-159">Next steps</span></span>

* [<span data-ttu-id="90b2e-160">테스트 및 디버깅을 위해 고유한 워크스테이션에서 U-SQL 스크립트 실행</span><span class="sxs-lookup"><span data-stu-id="90b2e-160">Run U-SQL scripts on your own workstation for testing and debugging</span></span>](data-lake-analytics-data-lake-tools-local-run.md)
* [<span data-ttu-id="90b2e-161">U-SQL 작업에서 C# 코드 디버그</span><span class="sxs-lookup"><span data-stu-id="90b2e-161">Debug C# code in U-SQL jobs</span></span>](data-lake-analytics-debug-u-sql-jobs.md)
* [<span data-ttu-id="90b2e-162">Azure Data Lake Tools for Visual Studio Code 사용</span><span class="sxs-lookup"><span data-stu-id="90b2e-162">Use the Azure Data Lake Tools for Visual Studio Code</span></span>](data-lake-analytics-data-lake-tools-for-vscode.md)

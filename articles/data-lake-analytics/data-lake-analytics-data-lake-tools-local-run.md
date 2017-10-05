---
title: "로컬 실행 및 Azure Data Lake U-SQL SDK를 사용하여 U-SQL 작업 테스트 및 디버그 | Microsoft Docs"
description: "Azure Data Lake Tools for Visual Studio 및 Azure Data Lake U-SQL SDK를 사용하여 로컬 워크스테이션에서 U-SQL 작업을 테스트하고 디버그하는 방법에 대해 알아봅니다."
services: data-lake-analytics
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 66dd58b1-0b28-46d1-aaae-43ee2739ae0a
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/15/2016
ms.author: yanacai
ms.openlocfilehash: 771a96df5cc66bac46e7144785be8cc072b57b31
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="test-and-debug-u-sql-jobs-by-using-local-run-and-the-azure-data-lake-u-sql-sdk"></a><span data-ttu-id="3f345-103">로컬 실행 및 Azure Data Lake U-SQL SDK를 사용하여 U-SQL 작업 테스트 및 디버그</span><span class="sxs-lookup"><span data-stu-id="3f345-103">Test and debug U-SQL jobs by using local run and the Azure Data Lake U-SQL SDK</span></span>

<span data-ttu-id="3f345-104">Azure Data Lake 서비스의 경우처럼 Visual Studio와 Azure Data Lake U-SQL SDK에 대해 Azure Data Lake 도구를 사용하여 워크스테이션에서 U-SQL 작업을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f345-104">You can use Azure Data Lake Tools for Visual Studio and the Azure Data Lake U-SQL SDK to run U-SQL jobs on your workstation, just as you can in the Azure Data Lake service.</span></span> <span data-ttu-id="3f345-105">이들 두 가지 로컬 실행 기능으로 U-SQL 작업을 테스트하고 디버그하는 시간을 절약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f345-105">These two local-run features save you time in testing and debugging your U-SQL jobs.</span></span>

## <a name="understand-the-data-root-folder-and-the-file-path"></a><span data-ttu-id="3f345-106">데이터 루트 폴더 및 파일 경로 이해</span><span class="sxs-lookup"><span data-stu-id="3f345-106">Understand the data-root folder and the file path</span></span>

<span data-ttu-id="3f345-107">로컬 실행 및 U-SQL SDK에는 모두 데이터 루트 폴더가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3f345-107">Both local run and the U-SQL SDK require a data-root folder.</span></span> <span data-ttu-id="3f345-108">데이터 루트 폴더는 로컬 계산 계정의 "로컬 저장소"입니다.</span><span class="sxs-lookup"><span data-stu-id="3f345-108">The data-root folder is a "local store" for the local compute account.</span></span> <span data-ttu-id="3f345-109">이는 Data Lake Analytics 계정의 Azure Data Lake Store 계정과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="3f345-109">It's equivalent to the Azure Data Lake Store account of a Data Lake Analytics account.</span></span> <span data-ttu-id="3f345-110">다른 데이터 루트 폴더로 전환하는 것은 다른 저장소 계정으로 전환하는 것과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3f345-110">Switching to a different data-root folder is just like switching to a different store account.</span></span> <span data-ttu-id="3f345-111">다른 데이터 루트 폴더와 공유된 데이터에 액세스하려는 경우 스크립트에서 절대 경로를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f345-111">If you want to access commonly shared data with different data-root folders, you must use absolute paths in your scripts.</span></span> <span data-ttu-id="3f345-112">또는 데이터 루트 폴더 아래에 파일 시스템 심볼 링크를 만들어 공유 데이터를 가리키도록 합니다(예, NTFS의 **mklink**).</span><span class="sxs-lookup"><span data-stu-id="3f345-112">Or, create file system symbolic links (for example, **mklink** on NTFS) under the data-root folder to point to the shared data.</span></span>

<span data-ttu-id="3f345-113">데이터 루트 폴더는 다음 용도로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f345-113">The data-root folder is used to:</span></span>

- <span data-ttu-id="3f345-114">데이터베이스, 테이블, TVF(테이블 반환 함수), 어셈블리 등의 메타데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3f345-114">Store metadata, including databases, tables, table-valued functions (TVFs), and assemblies.</span></span>
- <span data-ttu-id="3f345-115">U-SQL에서 상대 경로로 정의된 입력 및 출력 경로 조회 -</span><span class="sxs-lookup"><span data-stu-id="3f345-115">Look up the input and output paths that are defined as relative paths in U-SQL.</span></span> <span data-ttu-id="3f345-116">상대 경로를 사용하면 U-SQL 프로젝트를 Azure에 보다 쉽게 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f345-116">Using relative paths makes it easier to deploy your U-SQL projects to Azure.</span></span>

<span data-ttu-id="3f345-117">U-SQL 스크립트의 상대 경로 및 로컬 절대 경로를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f345-117">You can use both a relative path and a local absolute path in U-SQL scripts.</span></span> <span data-ttu-id="3f345-118">상대 경로는 지정된 데이터-루트 폴더 경로 기준으로 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3f345-118">The relative path is relative to the specified data-root folder path.</span></span> <span data-ttu-id="3f345-119">스크립트를 서버 쪽과 호환되게 하려면 경로 구분 기호로 "/"를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3f345-119">We recommend that you use "/" as the path separator to make your scripts compatible with the server side.</span></span> <span data-ttu-id="3f345-120">다음은 상대 경로 및 이와 대등한 절대 경로의 몇 가지 예입니다.</span><span class="sxs-lookup"><span data-stu-id="3f345-120">Here are some examples of relative paths and their equivalent absolute paths.</span></span> <span data-ttu-id="3f345-121">이 예에서 C:\LocalRunDataRoot는 데이터 루트 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="3f345-121">In these examples, C:\LocalRunDataRoot is the data-root folder.</span></span>

|<span data-ttu-id="3f345-122">상대 경로</span><span class="sxs-lookup"><span data-stu-id="3f345-122">Relative path</span></span>|<span data-ttu-id="3f345-123">절대 경로</span><span class="sxs-lookup"><span data-stu-id="3f345-123">Absolute path</span></span>|
|-------------|-------------|
|<span data-ttu-id="3f345-124">/abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="3f345-124">/abc/def/input.csv</span></span> |<span data-ttu-id="3f345-125">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="3f345-125">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="3f345-126">abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="3f345-126">abc/def/input.csv</span></span>  |<span data-ttu-id="3f345-127">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="3f345-127">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="3f345-128">D:/abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="3f345-128">D:/abc/def/input.csv</span></span> |<span data-ttu-id="3f345-129">D:\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="3f345-129">D:\abc\def\input.csv</span></span>|

## <a name="use-local-run-from-visual-studio"></a><span data-ttu-id="3f345-130">Visual Studio에서 로컬 실행 사용</span><span class="sxs-lookup"><span data-stu-id="3f345-130">Use local run from Visual Studio</span></span>

<span data-ttu-id="3f345-131">Data Lake Tools for Visual Studio는 Visual Studio에서 U-SQL 로컬 실행 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3f345-131">Data Lake Tools for Visual Studio provides a U-SQL local-run experience in Visual Studio.</span></span> <span data-ttu-id="3f345-132">이 기능을 사용하면 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f345-132">By using this feature, you can:</span></span>

- <span data-ttu-id="3f345-133">C# 어셈블리와 함께 U-SQL 스크립트를 로컬로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3f345-133">Run a U-SQL script locally, along with C# assemblies.</span></span>
- <span data-ttu-id="3f345-134">C# 어셈블리를 로컬로 디버그합니다.</span><span class="sxs-lookup"><span data-stu-id="3f345-134">Debug a C# assembly locally.</span></span>
- <span data-ttu-id="3f345-135">[서버 탐색기]에서 U-SQL 카탈로그(로컬 데이터베이스, 어셈블리, 스키마 및 테이블)를 만들고, 보고, 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="3f345-135">Create, view, and delete U-SQL catalogs (local databases, assemblies, schemas, and tables) from Server Explorer.</span></span> <span data-ttu-id="3f345-136">또 서버 탐색기에서 로컬 카탈로그도 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f345-136">You can also find the local catalog also from Server Explorer.</span></span>

    ![Data Lake Tools for Visual Studio의 로컬 카탈로그 로컬 실행](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-local-catalog.png)

<span data-ttu-id="3f345-138">Data Lake Tools 설치 관리자는 기본 데이터 루트 폴더로 사용할 C:\LocalRunRoot 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3f345-138">The Data Lake Tools installer creates a C:\LocalRunRoot folder to be used as the default data-root folder.</span></span> <span data-ttu-id="3f345-139">기본 병렬 처리 로컬 실행은 1입니다.</span><span class="sxs-lookup"><span data-stu-id="3f345-139">The default local-run parallelism is 1.</span></span>

### <a name="to-configure-local-run-in-visual-studio"></a><span data-ttu-id="3f345-140">Visual Studio에서 로컬 실행을 구성하려면</span><span class="sxs-lookup"><span data-stu-id="3f345-140">To configure local run in Visual Studio</span></span>

1. <span data-ttu-id="3f345-141">Visual Studio를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3f345-141">Open Visual Studio.</span></span>
2. <span data-ttu-id="3f345-142">**서버 탐색기**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3f345-142">Open **Server Explorer**.</span></span>
3. <span data-ttu-id="3f345-143">**Azure** > **Data Lake Analytics**를 차례로 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="3f345-143">Expand **Azure** > **Data Lake Analytics**.</span></span>
4. <span data-ttu-id="3f345-144">**Data Lake** 메뉴, **옵션 및 설정**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3f345-144">Click the **Data Lake** menu, and then click **Options and Settings**.</span></span>
5. <span data-ttu-id="3f345-145">왼쪽 트리에서 **Azure Data Lake**, **일반**을 차례로 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="3f345-145">In the left tree, expand **Azure Data Lake**, and then expand **General**.</span></span>

    ![Data Lake Tools for Visual Studio의 로컬 실행 구성 설정](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-configure.png)

<span data-ttu-id="3f345-147">로컬 실행을 수행하려면 Visual Studio U-SQL 프로젝트가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3f345-147">A Visual Studio U-SQL project is required for performing local run.</span></span> <span data-ttu-id="3f345-148">이 점이 Azure에서 실행하는 U-SQL 스크립트와 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="3f345-148">This part is different from running U-SQL scripts from Azure.</span></span>

### <a name="to-run-a-u-sql-script-locally"></a><span data-ttu-id="3f345-149">로컬로 U-SQL 스크립트를 실행하려면</span><span class="sxs-lookup"><span data-stu-id="3f345-149">To run a U-SQL script locally</span></span>
1. <span data-ttu-id="3f345-150">Visual Studio에서 U-SQL 프로젝트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3f345-150">From Visual Studio, open your U-SQL project.</span></span>   
2. <span data-ttu-id="3f345-151">[솔루션 탐색기]에서 U-SQL 스크립트를 마우스 오른쪽 단추로 클릭한 다음 **스크립트 제출**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3f345-151">Right-click a U-SQL script in Solution Explorer, and then click **Submit Script**.</span></span>
3. <span data-ttu-id="3f345-152">로컬로 스크립트를 실행하려면 분석 계정을 **(로컬)**로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3f345-152">Select **(Local)** as the Analytics account to run your script locally.</span></span>
<span data-ttu-id="3f345-153">또는 스크립트 창 위쪽에서 **(로컬)** 계정을 클릭한 다음 **제출**을 클릭하거나 Ctrl+F5 바로 가기를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f345-153">You can also click the **(Local)** account on the top of script window, and then click **Submit** (or use the Ctrl + F5 keyboard shortcut).</span></span>

    ![Data Lake Tools for Visual Studio의 로컬 실행 작업 제출](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-submit-job.png)

### <a name="debug-scripts-and-c-assemblies-locally"></a><span data-ttu-id="3f345-155">로컬에서 스크립트 및 C# 어셈블리 디버그</span><span class="sxs-lookup"><span data-stu-id="3f345-155">Debug scripts and C# assemblies locally</span></span>

<span data-ttu-id="3f345-156">Azure Data Lake Analytics 서비스에 C# 어셈블리를 제출하고 등록하지 않아도 C# 어셈블리를 디버그할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f345-156">You can debug C# assemblies without submitting and registering it to Azure Data Lake Analytics Service.</span></span> <span data-ttu-id="3f345-157">코드 숨김 파일 및 참조된 C# 프로젝트 양쪽 모두에 중단점을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f345-157">You can set breakpoints in both the code behind file and in a referenced C# project.</span></span>

#### <a name="to-debug-local-code-in-code-behind-file"></a><span data-ttu-id="3f345-158">코드 숨김 파일의 로컬 코드를 디버그하려면</span><span class="sxs-lookup"><span data-stu-id="3f345-158">To debug local code in code behind file</span></span>

1. <span data-ttu-id="3f345-159">코드 숨김 파일에 중단점을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3f345-159">Set breakpoints in the code behind file.</span></span>
2. <span data-ttu-id="3f345-160">F5 키를 눌러서 스크립트를 로컬에서 디버그합니다.</span><span class="sxs-lookup"><span data-stu-id="3f345-160">Press F5 to debug the script locally.</span></span>

> [!NOTE]
   > <span data-ttu-id="3f345-161">다음 프로시저는 Visual Studio 2015에만 해당됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f345-161">The following procedure only works in Visual Studio 2015.</span></span> <span data-ttu-id="3f345-162">이전 버전의 Visual Studio에서는 pdb 파일을 수동으로 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f345-162">In older Visual Studio you may need to manually add the pdb files.</span></span>  
   >
   >

#### <a name="to-debug-local-code-in-a-referenced-c-project"></a><span data-ttu-id="3f345-163">참조된 C# 프로젝트의 로컬 코드를 디버그하려면</span><span class="sxs-lookup"><span data-stu-id="3f345-163">To debug local code in a referenced C# project</span></span>

1. <span data-ttu-id="3f345-164">C# 어셈블리 프로젝트를 만들고 빌드하여 출력 dll을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="3f345-164">Create a C# Assembly project, and build it to generate the output dll.</span></span>
2. <span data-ttu-id="3f345-165">U-SQL 문을 사용하여 dll을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="3f345-165">Register the dll using a U-SQL statement:</span></span>

        CREATE ASSEMBLY assemblyname FROM @"..\..\path\to\output\.dll";
        
3. <span data-ttu-id="3f345-166">C# 코드에 중단점을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3f345-166">Set breakpoints in the C# code.</span></span>
4. <span data-ttu-id="3f345-167">F5 키를 눌러서 C# dll을 로컬에서 참조하는 스크립트를 디버그합니다.</span><span class="sxs-lookup"><span data-stu-id="3f345-167">Press F5 to debug the script with referencing the C# dll locally.</span></span>

## <a name="use-local-run-from-the-data-lake-u-sql-sdk"></a><span data-ttu-id="3f345-168">Data Lake U-SQL SDK에서 로컬 실행 사용</span><span class="sxs-lookup"><span data-stu-id="3f345-168">Use local run from the Data Lake U-SQL SDK</span></span>

<span data-ttu-id="3f345-169">Visual Studio를 사용하여 U-SQL 스크립트를 로컬로 실행하는 것 외에도 Azure Data Lake U-SQL SDK를 사용하여 명령줄 및 프로그래밍 인터페이스로 U-SQL 스크립트를 로컬로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f345-169">In addition to running U-SQL scripts locally by using Visual Studio, you can use the Azure Data Lake U-SQL SDK to run U-SQL scripts locally with command-line and programming interfaces.</span></span> <span data-ttu-id="3f345-170">이를 통해 U-SQL 로컬 테스트를 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f345-170">Through these, you can scale your U-SQL local test.</span></span>

<span data-ttu-id="3f345-171">[Azure Data Lake U-SQL SDK](data-lake-analytics-u-sql-sdk.md)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="3f345-171">Learn more about [Azure Data Lake U-SQL SDK](data-lake-analytics-u-sql-sdk.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="3f345-172">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3f345-172">Next steps</span></span>

* <span data-ttu-id="3f345-173">더 복잡한 쿼리를 보려면 [Azure Data Lake Analytics을 사용하여 웹 사이트 로그 분석](data-lake-analytics-analyze-weblogs.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3f345-173">To see a more complex query, see [Analyze website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="3f345-174">작업 세부 정보를 보려면, [Azure Data lake Analytics 작업에 대한 작업 브라우저 및 작업 보기 사용하기](data-lake-analytics-data-lake-tools-view-jobs.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3f345-174">To view job details, see [Use Job Browser and Job View for Azure Data Lake Analytics jobs](data-lake-analytics-data-lake-tools-view-jobs.md).</span></span>
* <span data-ttu-id="3f345-175">꼭짓점 실행 보기를 사용하려면 [Data Lake Tools for Visual Studio에서 Vertex Execution View 사용](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3f345-175">To use the vertex execution view, see [Use the Vertex Execution View in Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span></span>

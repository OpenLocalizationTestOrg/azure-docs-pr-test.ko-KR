---
title: "aaaTest 및 디버그 U-SQL 작업을 사용 하 여 로컬 실행 및 Azure 데이터 레이크 U-SQL SDK hello | Microsoft Docs"
description: "로컬 워크스테이션 toouse Azure 데이터 레이크 Tools for Visual Studio 및 Azure 데이터 레이크 U-SQL SDK tootest hello 및 디버그 U-SQL 작업 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: be04558a504acf6a088e207608ee2d4a011d3ffc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="test-and-debug-u-sql-jobs-by-using-local-run-and-hello-azure-data-lake-u-sql-sdk"></a><span data-ttu-id="f7357-103">테스트 및 U-SQL 작업을 사용 하 여 로컬 실행 hello Azure 데이터 레이크 U-SQL SDK 디버그</span><span class="sxs-lookup"><span data-stu-id="f7357-103">Test and debug U-SQL jobs by using local run and hello Azure Data Lake U-SQL SDK</span></span>

<span data-ttu-id="f7357-104">Hello Azure 데이터 레이크 서비스의 경우와 마찬가지로 워크스테이션에서 Visual Studio 및 hello Azure 데이터 레이크 U-SQL SDK toorun U-SQL 작업에 대해 Azure 데이터 레이크 도구를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7357-104">You can use Azure Data Lake Tools for Visual Studio and hello Azure Data Lake U-SQL SDK toorun U-SQL jobs on your workstation, just as you can in hello Azure Data Lake service.</span></span> <span data-ttu-id="f7357-105">이들 두 가지 로컬 실행 기능으로 U-SQL 작업을 테스트하고 디버그하는 시간을 절약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7357-105">These two local-run features save you time in testing and debugging your U-SQL jobs.</span></span>

## <a name="understand-hello-data-root-folder-and-hello-file-path"></a><span data-ttu-id="f7357-106">Hello 데이터 루트 폴더 및 파일 경로 hello 이해</span><span class="sxs-lookup"><span data-stu-id="f7357-106">Understand hello data-root folder and hello file path</span></span>

<span data-ttu-id="f7357-107">로컬 실행와 hello U-SQL SDK 모두 데이터 루트 폴더를이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7357-107">Both local run and hello U-SQL SDK require a data-root folder.</span></span> <span data-ttu-id="f7357-108">hello 데이터 루트 폴더는 hello 로컬 계산 계정에 대 한 "로컬 저장소".</span><span class="sxs-lookup"><span data-stu-id="f7357-108">hello data-root folder is a "local store" for hello local compute account.</span></span> <span data-ttu-id="f7357-109">이 Data Lake 분석 계정 해당 toohello Azure 데이터 레이크 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="f7357-109">It's equivalent toohello Azure Data Lake Store account of a Data Lake Analytics account.</span></span> <span data-ttu-id="f7357-110">다른 저장소 계정 tooa 전환와 동일 하 게 서로 다른 데이터 루트 폴더는 tooa 전환입니다.</span><span class="sxs-lookup"><span data-stu-id="f7357-110">Switching tooa different data-root folder is just like switching tooa different store account.</span></span> <span data-ttu-id="f7357-111">Tooaccess 서로 다른 데이터 루트 폴더와 일반적으로 데이터를 공유 하려면 스크립트에서 절대 경로 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7357-111">If you want tooaccess commonly shared data with different data-root folders, you must use absolute paths in your scripts.</span></span> <span data-ttu-id="f7357-112">또는 파일 시스템에 대 한 기호화 된 링크를 만듭니다 (예를 들어 **mklink** ntfs) hello 데이터 루트 폴더 toopoint toohello에서 데이터를 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7357-112">Or, create file system symbolic links (for example, **mklink** on NTFS) under hello data-root folder toopoint toohello shared data.</span></span>

<span data-ttu-id="f7357-113">hello 데이터 루트 폴더에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7357-113">hello data-root folder is used to:</span></span>

- <span data-ttu-id="f7357-114">데이터베이스, 테이블, TVF(테이블 반환 함수), 어셈블리 등의 메타데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f7357-114">Store metadata, including databases, tables, table-valued functions (TVFs), and assemblies.</span></span>
- <span data-ttu-id="f7357-115">입력 hello 및 U-SQL에 상대 경로로 정의 된 출력 경로를 조회 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7357-115">Look up hello input and output paths that are defined as relative paths in U-SQL.</span></span> <span data-ttu-id="f7357-116">상대 경로 사용 하 여 사용 하면 보다 쉽게 toodeploy U-SQL 프로젝트 tooAzure 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7357-116">Using relative paths makes it easier toodeploy your U-SQL projects tooAzure.</span></span>

<span data-ttu-id="f7357-117">U-SQL 스크립트의 상대 경로 및 로컬 절대 경로를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7357-117">You can use both a relative path and a local absolute path in U-SQL scripts.</span></span> <span data-ttu-id="f7357-118">hello 상대 경로 상대 toohello 지정한 데이터 루트 폴더 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="f7357-118">hello relative path is relative toohello specified data-root folder path.</span></span> <span data-ttu-id="f7357-119">하면 사용 하 여 "/"로 hello 경로 구분 기호 toomake 스크립트 hello 서버 쪽와 호환 되는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f7357-119">We recommend that you use "/" as hello path separator toomake your scripts compatible with hello server side.</span></span> <span data-ttu-id="f7357-120">다음은 상대 경로 및 이와 대등한 절대 경로의 몇 가지 예입니다.</span><span class="sxs-lookup"><span data-stu-id="f7357-120">Here are some examples of relative paths and their equivalent absolute paths.</span></span> <span data-ttu-id="f7357-121">다음 예에서 C:\LocalRunDataRoot는 hello 데이터 루트 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="f7357-121">In these examples, C:\LocalRunDataRoot is hello data-root folder.</span></span>

|<span data-ttu-id="f7357-122">상대 경로</span><span class="sxs-lookup"><span data-stu-id="f7357-122">Relative path</span></span>|<span data-ttu-id="f7357-123">절대 경로</span><span class="sxs-lookup"><span data-stu-id="f7357-123">Absolute path</span></span>|
|-------------|-------------|
|<span data-ttu-id="f7357-124">/abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="f7357-124">/abc/def/input.csv</span></span> |<span data-ttu-id="f7357-125">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="f7357-125">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="f7357-126">abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="f7357-126">abc/def/input.csv</span></span>  |<span data-ttu-id="f7357-127">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="f7357-127">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="f7357-128">D:/abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="f7357-128">D:/abc/def/input.csv</span></span> |<span data-ttu-id="f7357-129">D:\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="f7357-129">D:\abc\def\input.csv</span></span>|

## <a name="use-local-run-from-visual-studio"></a><span data-ttu-id="f7357-130">Visual Studio에서 로컬 실행 사용</span><span class="sxs-lookup"><span data-stu-id="f7357-130">Use local run from Visual Studio</span></span>

<span data-ttu-id="f7357-131">Data Lake Tools for Visual Studio는 Visual Studio에서 U-SQL 로컬 실행 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f7357-131">Data Lake Tools for Visual Studio provides a U-SQL local-run experience in Visual Studio.</span></span> <span data-ttu-id="f7357-132">이 기능을 사용하면 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7357-132">By using this feature, you can:</span></span>

- <span data-ttu-id="f7357-133">C# 어셈블리와 함께 U-SQL 스크립트를 로컬로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f7357-133">Run a U-SQL script locally, along with C# assemblies.</span></span>
- <span data-ttu-id="f7357-134">C# 어셈블리를 로컬로 디버그합니다.</span><span class="sxs-lookup"><span data-stu-id="f7357-134">Debug a C# assembly locally.</span></span>
- <span data-ttu-id="f7357-135">[서버 탐색기]에서 U-SQL 카탈로그(로컬 데이터베이스, 어셈블리, 스키마 및 테이블)를 만들고, 보고, 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="f7357-135">Create, view, and delete U-SQL catalogs (local databases, assemblies, schemas, and tables) from Server Explorer.</span></span> <span data-ttu-id="f7357-136">서버 탐색기에서도 hello 로컬 카탈로그를 찾을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7357-136">You can also find hello local catalog also from Server Explorer.</span></span>

    ![Data Lake Tools for Visual Studio의 로컬 카탈로그 로컬 실행](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-local-catalog.png)

<span data-ttu-id="f7357-138">hello 기본 데이터 루트 폴더로 사용할 C:\LocalRunRoot 폴더 toobe hello 데이터 레이크 도구 설치 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f7357-138">hello Data Lake Tools installer creates a C:\LocalRunRoot folder toobe used as hello default data-root folder.</span></span> <span data-ttu-id="f7357-139">hello 기본 로컬 실행 병렬 처리는 1입니다.</span><span class="sxs-lookup"><span data-stu-id="f7357-139">hello default local-run parallelism is 1.</span></span>

### <a name="tooconfigure-local-run-in-visual-studio"></a><span data-ttu-id="f7357-140">tooconfigure 로컬 Visual Studio에서 실행</span><span class="sxs-lookup"><span data-stu-id="f7357-140">tooconfigure local run in Visual Studio</span></span>

1. <span data-ttu-id="f7357-141">Visual Studio를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f7357-141">Open Visual Studio.</span></span>
2. <span data-ttu-id="f7357-142">**서버 탐색기**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f7357-142">Open **Server Explorer**.</span></span>
3. <span data-ttu-id="f7357-143">**Azure** > **Data Lake Analytics**를 차례로 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="f7357-143">Expand **Azure** > **Data Lake Analytics**.</span></span>
4. <span data-ttu-id="f7357-144">Hello 클릭 **데이터 레이크** 메뉴를 차례로 클릭 **옵션 및 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="f7357-144">Click hello **Data Lake** menu, and then click **Options and Settings**.</span></span>
5. <span data-ttu-id="f7357-145">Hello 왼쪽 트리에서 **Azure 데이터 레이크**을 펼친 다음 **일반**합니다.</span><span class="sxs-lookup"><span data-stu-id="f7357-145">In hello left tree, expand **Azure Data Lake**, and then expand **General**.</span></span>

    ![Data Lake Tools for Visual Studio의 로컬 실행 구성 설정](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-configure.png)

<span data-ttu-id="f7357-147">로컬 실행을 수행하려면 Visual Studio U-SQL 프로젝트가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f7357-147">A Visual Studio U-SQL project is required for performing local run.</span></span> <span data-ttu-id="f7357-148">이 점이 Azure에서 실행하는 U-SQL 스크립트와 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="f7357-148">This part is different from running U-SQL scripts from Azure.</span></span>

### <a name="toorun-a-u-sql-script-locally"></a><span data-ttu-id="f7357-149">로컬로 toorun는 U-SQL 스크립트</span><span class="sxs-lookup"><span data-stu-id="f7357-149">toorun a U-SQL script locally</span></span>
1. <span data-ttu-id="f7357-150">Visual Studio에서 U-SQL 프로젝트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f7357-150">From Visual Studio, open your U-SQL project.</span></span>   
2. <span data-ttu-id="f7357-151">[솔루션 탐색기]에서 U-SQL 스크립트를 마우스 오른쪽 단추로 클릭한 다음 **스크립트 제출**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7357-151">Right-click a U-SQL script in Solution Explorer, and then click **Submit Script**.</span></span>
3. <span data-ttu-id="f7357-152">선택 **(Local)** hello 분석 계정 toorun 로컬로 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="f7357-152">Select **(Local)** as hello Analytics account toorun your script locally.</span></span>
<span data-ttu-id="f7357-153">Hello를 클릭할 수도 있습니다 **(Local)** hello 스크립트 창 위쪽의 계정 및 클릭 **전송** (또는 안녕하세요 Ctrl + F5 바로 가기 키 사용).</span><span class="sxs-lookup"><span data-stu-id="f7357-153">You can also click hello **(Local)** account on hello top of script window, and then click **Submit** (or use hello Ctrl + F5 keyboard shortcut).</span></span>

    ![Data Lake Tools for Visual Studio의 로컬 실행 작업 제출](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-submit-job.png)

### <a name="debug-scripts-and-c-assemblies-locally"></a><span data-ttu-id="f7357-155">로컬에서 스크립트 및 C# 어셈블리 디버그</span><span class="sxs-lookup"><span data-stu-id="f7357-155">Debug scripts and C# assemblies locally</span></span>

<span data-ttu-id="f7357-156">제출 하 고 tooAzure 데이터 레이크 분석 서비스를 등록 하지 않고 C# 어셈블리를 디버깅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7357-156">You can debug C# assemblies without submitting and registering it tooAzure Data Lake Analytics Service.</span></span> <span data-ttu-id="f7357-157">참조 된 C# 프로젝트 및 두 hello 코드 숨김 파일에서에서 중단점을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7357-157">You can set breakpoints in both hello code behind file and in a referenced C# project.</span></span>

#### <a name="toodebug-local-code-in-code-behind-file"></a><span data-ttu-id="f7357-158">toodebug 로컬 코드 코드 숨김 파일에</span><span class="sxs-lookup"><span data-stu-id="f7357-158">toodebug local code in code behind file</span></span>

1. <span data-ttu-id="f7357-159">Hello 코드 숨김 파일에에서 중단점을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7357-159">Set breakpoints in hello code behind file.</span></span>
2. <span data-ttu-id="f7357-160">F5 toodebug hello 스크립트 로컬 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="f7357-160">Press F5 toodebug hello script locally.</span></span>

> [!NOTE]
   > <span data-ttu-id="f7357-161">다음 절차에서 Visual Studio 2015 에서만 작동 하는 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="f7357-161">hello following procedure only works in Visual Studio 2015.</span></span> <span data-ttu-id="f7357-162">이전 Visual Studio에서 할 수 있습니다 toomanually hello pdb 파일을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7357-162">In older Visual Studio you may need toomanually add hello pdb files.</span></span>  
   >
   >

#### <a name="toodebug-local-code-in-a-referenced-c-project"></a><span data-ttu-id="f7357-163">참조 된 C# 프로젝트의 toodebug 로컬 코드</span><span class="sxs-lookup"><span data-stu-id="f7357-163">toodebug local code in a referenced C# project</span></span>

1. <span data-ttu-id="f7357-164">C# 어셈블리 프로젝트를 만들고 toogenerate hello 출력 dll을 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="f7357-164">Create a C# Assembly project, and build it toogenerate hello output dll.</span></span>
2. <span data-ttu-id="f7357-165">U SQL 문을 사용 하 여 hello dll을 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7357-165">Register hello dll using a U-SQL statement:</span></span>

        CREATE ASSEMBLY assemblyname FROM @"..\..\path\to\output\.dll";
        
3. <span data-ttu-id="f7357-166">Hello C# 코드에에서 중단점을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7357-166">Set breakpoints in hello C# code.</span></span>
4. <span data-ttu-id="f7357-167">로컬로 hello C# dll 참조를 사용한 toodebug hello 스크립트 F5 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="f7357-167">Press F5 toodebug hello script with referencing hello C# dll locally.</span></span>

## <a name="use-local-run-from-hello-data-lake-u-sql-sdk"></a><span data-ttu-id="f7357-168">데이터 레이크 U-SQL SDK hello에서 사용 하 여 로컬 실행</span><span class="sxs-lookup"><span data-stu-id="f7357-168">Use local run from hello Data Lake U-SQL SDK</span></span>

<span data-ttu-id="f7357-169">Visual Studio를 사용 하 여 로컬로 toorunning U-SQL 스크립트 뿐만 아니라, 명령줄 및 프로그래밍 인터페이스 로컬로 hello Azure 데이터 레이크 U-SQL SDK toorun U-SQL 스크립트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7357-169">In addition toorunning U-SQL scripts locally by using Visual Studio, you can use hello Azure Data Lake U-SQL SDK toorun U-SQL scripts locally with command-line and programming interfaces.</span></span> <span data-ttu-id="f7357-170">이를 통해 U-SQL 로컬 테스트를 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7357-170">Through these, you can scale your U-SQL local test.</span></span>

<span data-ttu-id="f7357-171">[Azure Data Lake U-SQL SDK](data-lake-analytics-u-sql-sdk.md)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="f7357-171">Learn more about [Azure Data Lake U-SQL SDK](data-lake-analytics-u-sql-sdk.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="f7357-172">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f7357-172">Next steps</span></span>

* <span data-ttu-id="f7357-173">toosee 복잡 한 쿼리를 참조 [Azure 데이터 레이크 분석을 사용 하 여 웹 사이트 로그 분석](data-lake-analytics-analyze-weblogs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f7357-173">toosee a more complex query, see [Analyze website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="f7357-174">tooview 작업 세부 정보 참조 [사용 하 여 작업 브라우저와 Azure 데이터 레이크 분석 작업에 대 한 작업 보기](data-lake-analytics-data-lake-tools-view-jobs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f7357-174">tooview job details, see [Use Job Browser and Job View for Azure Data Lake Analytics jobs](data-lake-analytics-data-lake-tools-view-jobs.md).</span></span>
* <span data-ttu-id="f7357-175">toouse hello 꼭 짓 점 실행 보기 참조 [꼭 짓 점 실행 보기 데이터 레이크 Tools for Visual Studio에서에서 사용 하 여 hello](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f7357-175">toouse hello vertex execution view, see [Use hello Vertex Execution View in Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span></span>

---
title: "U-SQL 작업 디버그 | Microsoft Docs"
description: "Visual Studio를 사용하여 U-SQL의 실패한 꼭짓점을 디버그하는 방법을 알아봅니다."
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: bcd0b01e-1755-4112-8e8a-a5cabdca4df2
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 09/02/2016
ms.author: saveenr
ms.openlocfilehash: 2a77c72d3062272305208934d6406d040266c753
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="debug-user-defined-c-code-for-failed-u-sql-jobs"></a><span data-ttu-id="f5684-103">실패한 U-SQL 작업에 대한 사용자 정의 C# 코드 디버그</span><span class="sxs-lookup"><span data-stu-id="f5684-103">Debug user-defined C# code for failed U-SQL jobs</span></span>

<span data-ttu-id="f5684-104">U-SQL은 C#을 사용하는 확장성 모델을 제공하기 때문에 사용자 지정 추출기 또는 리듀서와 같은 기능을 추가하는 코드를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5684-104">U-SQL provides an extensibility model using C#, so you can write your code to add functionality such as a custom extractor or reducer.</span></span> <span data-ttu-id="f5684-105">자세한 내용은 [U-SQL 프로그래밍 기능 가이드](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-u-sql-programmability-guide#use-user-defined-functions-udf)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f5684-105">To learn more, see [U-SQL programmability guide](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-u-sql-programmability-guide#use-user-defined-functions-udf).</span></span> <span data-ttu-id="f5684-106">실제로 어떤 코드라도 디버깅이 필요하며 빅 데이터 시스템에는 로그 파일과 같이 제한된 런타임 디버깅 정보만 제공될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5684-106">In practice any code may need debugging, and big data systems may only provide limited runtime debugging information such as log files.</span></span>

<span data-ttu-id="f5684-107">Azure Data Lake Tools for Visual Studio에는 디버깅을 위해 실패한 작업을 클라우드에서 로컬 컴퓨터로 복제할 수 있는 **실패한 꼭짓점 디버그**라는 기능이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5684-107">Azure Data Lake Tools for Visual Studio provides a feature called **Failed Vertex Debug**, which lets you clone a failed job from the cloud to your local machine for debugging.</span></span> <span data-ttu-id="f5684-108">로컬 클론은 모든 입력 데이터와 사용자 코드를 비롯한 전체 클라우드 환경을 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="f5684-108">The local clone captures the entire cloud environment, including any input data and user code.</span></span>

<span data-ttu-id="f5684-109">다음 비디오에서는 Azure Data Lake Tools for Visual Studio의 실패한 꼭짓점 디버그를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f5684-109">The following video demonstrates Failed Vertex Debug in Azure Data Lake Tools for Visual Studio.</span></span>

> [!VIDEO https://e0d1.wpc.azureedge.net/80E0D1/OfficeMixProdMediaBlobStorage/asset-d3aeab42-6149-4ecc-b044-aa624901ab32/b0fc0373c8f94f1bb8cd39da1310adb8.mp4?sv=2012-02-12&sr=c&si=a91fad76-cfdd-4513-9668-483de39e739c&sig=K%2FR%2FdnIi9S6P%2FBlB3iLAEV5pYu6OJFBDlQy%2FQtZ7E7M%3D&se=2116-07-19T09:27:30Z&rscd=attachment%3B%20filename%3DDebugyourcustomcodeinUSQLADLA.mp4]
>

> [!NOTE]
> <span data-ttu-id="f5684-110">Visual Studio에 [Microsoft Visual C++ 2015 재배포 가능 업데이트 3](https://www.microsoft.com/en-us/download/details.aspx?id=53840) 및 [Windows용 유니버설 C 런타임](https://www.microsoft.com/download/details.aspx?id=50410)이 설치되어 있지 않다면 해당 업데이트가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f5684-110">Visual Studio requires the following two updates, if they are not already installed: [Microsoft Visual C++ 2015 Redistributable Update 3](https://www.microsoft.com/en-us/download/details.aspx?id=53840) and the [Universal C Runtime for Windows](https://www.microsoft.com/download/details.aspx?id=50410).</span></span>

## <a name="download-failed-vertex-to-local-machine"></a><span data-ttu-id="f5684-111">로컬 컴퓨터에 실패한 꼭짓점 다운로드</span><span class="sxs-lookup"><span data-stu-id="f5684-111">Download failed vertex to local machine</span></span>

<span data-ttu-id="f5684-112">Azure Data Lake Tools for Visual Studio에서 실패한 작업을 열면 오류 탭에 자세한 오류 메시지가 있는 노란 경고 막대를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5684-112">When you open a failed job in Azure Data Lake Tools for Visual Studio, you see a yellow alert bar with detailed error messages in the error tab.</span></span>

1. <span data-ttu-id="f5684-113">**다운로드** 를 클릭하여 모든 필수 리소스 및 입력 스트림을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="f5684-113">Click **Download** to download all the required resources and input streams.</span></span> <span data-ttu-id="f5684-114">다운로드가 완료되지 않으면 **다시 시도**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f5684-114">If the download doesn't complete, click **Retry**.</span></span>

2. <span data-ttu-id="f5684-115">다운로드가 완료되면 **열기**를 클릭하여 로컬 디버깅 환경을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="f5684-115">Click **Open** after the download completes to generate a local debugging environment.</span></span> <span data-ttu-id="f5684-116">디버깅 솔루션이 있는 새로운 Visual Studio 인스턴스가 자동으로 생성되고 열립니다.</span><span class="sxs-lookup"><span data-stu-id="f5684-116">A new Visual Studio instance with a debugging solution is automatically created and opened.</span></span>

![Azure Data Lake Analytics U-SQL 디버그 Visual Studio 정점 다운로드](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-download-vertex.png)

<span data-ttu-id="f5684-118">작업에는 코드 숨김 소스 파일이나 등록된 어셈블리가 포함될 수 있으며 이러한 두 가지 유형에는 서로 다른 디버깅 시나리오가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5684-118">Jobs may include code-behind source files or registered assemblies, and these two types have different debugging scenarios.</span></span>

- [<span data-ttu-id="f5684-119">코드 숨김을 사용하여 실패한 작업 디버그</span><span class="sxs-lookup"><span data-stu-id="f5684-119">Debug a failed job with code-behind</span></span>](#debug-job-failed-with-code-behind)
- [<span data-ttu-id="f5684-120">어셈블리를 사용하여 실패한 작업 디버그</span><span class="sxs-lookup"><span data-stu-id="f5684-120">Debug a failed job with assemblies</span></span>](#debug-job-failed-with-assemblies)


## <a name="debug-job-failed-with-code-behind"></a><span data-ttu-id="f5684-121">코드 숨김으로 인해 실패한 작업 디버그</span><span class="sxs-lookup"><span data-stu-id="f5684-121">Debug job failed with code-behind</span></span>

<span data-ttu-id="f5684-122">U-SQL 작업이 실패하고 작업에 사용자 코드(U-SQL 프로젝트에서 대개 `Script.usql.cs`라고 명명된)가 포함되는 경우 해당 소스 코드를 디버깅 솔루션으로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f5684-122">If a U-SQL job fails, and the job includes user code (typically named `Script.usql.cs` in a U-SQL project), that source code is imported into the debugging solution.</span></span>  <span data-ttu-id="f5684-123">여기에서 Visual Studio 디버깅 도구(조사식, 변수 등)를 사용하여 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5684-123">From there you can use the Visual Studio debugging tools (watch, variables, etc.) to troubleshoot the problem.</span></span>

> [!NOTE]
> <span data-ttu-id="f5684-124">디버깅 전에 예외 설정 창(**Ctrl + Alt + E**)에서 **공용 언어 런타임 예외**를 선택했는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5684-124">Before debugging, be sure to check **Common Language Runtime Exceptions** in the Exception Settings window (**Ctrl + Alt + E**).</span></span>

![Azure Data Lake Analytics U-SQL 디버그 Visual Studio 설정](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-clr-exception-setting.png)

1. <span data-ttu-id="f5684-126">**F5**를 눌러서 코드 숨김 코드를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f5684-126">Press **F5** to run the code-behind code.</span></span> <span data-ttu-id="f5684-127">예외로 인해 중지될 때까지 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5684-127">It will run until it is stopped by an exception.</span></span>

2. <span data-ttu-id="f5684-128">`ADLTool_Codebehind.usql.cs` 파일을 열고 중단점을 설정한 후 **F5** 키를 눌러 단계별로 코드를 디버그합니다.</span><span class="sxs-lookup"><span data-stu-id="f5684-128">Open the `ADLTool_Codebehind.usql.cs` file and set breakpoints, then press **F5** to debug the code step by step.</span></span>

    ![Azure Data Lake Analytics U-SQL 디버그 예외](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-debug-exception.png)

## <a name="debug-job-failed-with-assemblies"></a><span data-ttu-id="f5684-130">어셈블리로 인해 실패한 작업 디버그</span><span class="sxs-lookup"><span data-stu-id="f5684-130">Debug job failed with assemblies</span></span>

<span data-ttu-id="f5684-131">U-SQL 스크립트에 등록된 어셈블리를 사용하는 경우 시스템은 소스 코드를 자동으로 가져올 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f5684-131">If you use registered assemblies in your U-SQL script, the system can't get the source code automatically.</span></span> <span data-ttu-id="f5684-132">이런 경우 어셈블리 소스 코드 파일을 솔루션에 수동으로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f5684-132">In this case, manually add the assemblies' source code files to the solution.</span></span>

### <a name="configure-the-solution"></a><span data-ttu-id="f5684-133">솔루션 구성</span><span class="sxs-lookup"><span data-stu-id="f5684-133">Configure the solution</span></span>

1. <span data-ttu-id="f5684-134">**솔루션 'VertexDebug' > 추가 > 기존 프로젝트...**를 마우스 오른쪽 단추로 클릭하여 어셈블리의 소스 코드를 찾고 프로젝트를 디버깅 솔루션에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f5684-134">Right-click **Solution 'VertexDebug' > Add > Existing Project...** to find the assemblies' source code and add the project to the debugging solution.</span></span>

    ![Azure Data Lake Analytics U-SQL 디버그 - 프로젝트 추가](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-add-project-to-debug-solution.png)

2. <span data-ttu-id="f5684-136">솔루션에서 **LocalVertexHost > 속성**을 마우스 오른쪽 단추로 클릭하고 **작업 디렉터리** 경로를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="f5684-136">Right-click **LocalVertexHost > Properties** in the solution and copy the **Working Directory** path.</span></span>

3. <span data-ttu-id="f5684-137">**어셈블리 소스 코드 프로젝트 > 속성**을 마우스 오른쪽 단추로 클릭하고 왼쪽의 **빌드** 탭을 선택하고 복사한 경로를 **출력 > 출력 경로**에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="f5684-137">Right-Click **assembly source code project > Properties**, select the **Build** tab at left, and paste the copied path as **Output > Output path**.</span></span>

    ![Azure Data Lake Analytics U-SQL 디버그 - pdb 경로 설정](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-set-pdb-path.png)

4. <span data-ttu-id="f5684-139">**Ctrl + Alt + E**를 누르고 예외 설정 창에서 **공용 언어 런타임 예외**를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f5684-139">Press **Ctrl + Alt + E**, check **Common Language Runtime Exceptions** in Exception Settings window.</span></span>

### <a name="start-debug"></a><span data-ttu-id="f5684-140">디버그 시작</span><span class="sxs-lookup"><span data-stu-id="f5684-140">Start debug</span></span>

1. <span data-ttu-id="f5684-141">**어셈블리 소스 코드 프로젝트 > 다시 빌드**를 마우스 오른쪽 단추로 클릭하여 `LocalVertexHost` 작업 디렉터리로 .pdb 파일을 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="f5684-141">Right-click **assembly source code project > Rebuild** to output .pdb files to the `LocalVertexHost` working directory.</span></span>

2. <span data-ttu-id="f5684-142">**F5** 키를 누르면 예외에 의해 중지될 때까지 프로젝트가 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5684-142">Press **F5** and the project will run until it is stopped by an exception.</span></span> <span data-ttu-id="f5684-143">다음과 같은 경고 메시지가 표시될 수 있으며 이 메시지는 무시해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5684-143">You may see the following warning message, which you can safely ignore.</span></span> <span data-ttu-id="f5684-144">디버그 화면으로 이동하는 데 최대 1분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5684-144">It can take up to a minute to get to the debug screen.</span></span>

    ![Azure Data Lake Analytics U-SQL 디버그 Visual Studio 경고](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-visual-studio-u-sql-debug-warning.png)

3. <span data-ttu-id="f5684-146">소스 코드를 열고 중단점을 설정한 후 **F5** 키를 눌러 단계별로 코드를 디버그합니다.</span><span class="sxs-lookup"><span data-stu-id="f5684-146">Open your source code and set breakpoints, then press **F5** to debug the code step by step.</span></span>

<span data-ttu-id="f5684-147">Visual Studio 디버깅 도구(조사식, 변수 등)를 사용하여 문제를 해결할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5684-147">You can also use the Visual Studio debugging tools (watch, variables, etc.) to troubleshoot the problem.</span></span>

> [!NOTE]
> <span data-ttu-id="f5684-148">업데이트된 .pdb 파일을 생성하기 위해 코드를 수정한 후 매번 어셈블리 소스 코드 프로젝트를 다시 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="f5684-148">Rebuild the assembly source code project each time after you modify the code to generate updated .pdb files.</span></span>

<span data-ttu-id="f5684-149">디버깅 후 프로젝트가 성공적으로 완료되면 출력 창에 다음 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5684-149">After debugging, if the project completes successfully the output window shows the following message:</span></span>

```
The Program 'LocalVertexHost.exe' has exited with code 0 (0x0).
```

![Azure Data Lake Analytics U-SQL 디버그 성공](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-debug-succeed.png)

## <a name="resubmit-the-job"></a><span data-ttu-id="f5684-151">작업 다시 제출</span><span class="sxs-lookup"><span data-stu-id="f5684-151">Resubmit the job</span></span>

<span data-ttu-id="f5684-152">디버깅을 완료한 후에는 실패한 작업을 다시 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5684-152">Once you have completed debugging, resubmit the failed job.</span></span>

1. <span data-ttu-id="f5684-153">코드 숨김 솔루션이 있는 작업의 경우 C# 코드를 코드 숨김 소스 파일(대개 `Script.usql.cs`)로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="f5684-153">For jobs with code-behind solutions, copy your C# code into the code-behind source file (typically `Script.usql.cs`).</span></span>
2. <span data-ttu-id="f5684-154">어셈블리가 있는 작업의 경우 업데이트된 .dll 어셈블리를 ADLA 데이터베이스에 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="f5684-154">For jobs with assemblies, register the updated .dll assemblies into your ADLA database:</span></span>
    1. <span data-ttu-id="f5684-155">서버 탐색기 또는 클라우드 탐색기에서 **ADLA 계정 > 데이터베이스** 노드를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="f5684-155">From Server Explorer or Cloud Explorer, expand the **ADLA account > Databases** node.</span></span>
    2. <span data-ttu-id="f5684-156">**어셈블리**를 마우스 오른쪽 단추로 클릭하고 새 .dll을 ADLA 데이터베이스에 등록합니다. ![Azure Data Lake Analytics U-SQL 디버그 어셈블리 등록](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-register-assembly.png)</span><span class="sxs-lookup"><span data-stu-id="f5684-156">Right-click **Assemblies** and register your new .dll assemblies with the ADLA database: ![Azure Data Lake Analytics U-SQL debug register assembly](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-register-assembly.png)</span></span>
3. <span data-ttu-id="f5684-157">작업을 다시 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="f5684-157">Resubmit your job.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f5684-158">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f5684-158">Next steps</span></span>

- [<span data-ttu-id="f5684-159">U-SQL 프로그래밍 기능 가이드</span><span class="sxs-lookup"><span data-stu-id="f5684-159">U-SQL programmability guide</span></span>](data-lake-analytics-u-sql-programmability-guide.md)
- [<span data-ttu-id="f5684-160">Azure Data Lake Analytics 작업에 대한 U-SQL 사용자 정의 연산자를 개발합니다.</span><span class="sxs-lookup"><span data-stu-id="f5684-160">Develop U-SQL User-defined operators for Azure Data Lake Analytics jobs</span></span>](data-lake-analytics-u-sql-develop-user-defined-operators.md)
- [<span data-ttu-id="f5684-161">자습서: Visual Studio용 데이터 레이크 도구를 사용하여 U-SQL 스크립트 개발</span><span class="sxs-lookup"><span data-stu-id="f5684-161">Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)

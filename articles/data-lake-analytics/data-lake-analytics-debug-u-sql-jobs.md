---
title: "aaaDebug U-SQL 작업 | Microsoft Docs"
description: "U SQL toodebug Visual Studio를 사용 하 여 꼭 짓 점 실패 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 092bffa1a59ed91c5837402d0276447480b923fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-user-defined-c-code-for-failed-u-sql-jobs"></a><span data-ttu-id="07249-103">실패한 U-SQL 작업에 대한 사용자 정의 C# 코드 디버그</span><span class="sxs-lookup"><span data-stu-id="07249-103">Debug user-defined C# code for failed U-SQL jobs</span></span>

<span data-ttu-id="07249-104">U-SQL C#을 사용 하 여 코드 tooadd 기능 추출기 사용자 지정 또는 리 듀 서 같은 작성할 수 있습니다 확장성 모델을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="07249-104">U-SQL provides an extensibility model using C#, so you can write your code tooadd functionality such as a custom extractor or reducer.</span></span> <span data-ttu-id="07249-105">toolearn 더 참조 [U SQL 프로그래밍 기능 가이드](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-u-sql-programmability-guide#use-user-defined-functions-udf)합니다.</span><span class="sxs-lookup"><span data-stu-id="07249-105">toolearn more, see [U-SQL programmability guide](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-u-sql-programmability-guide#use-user-defined-functions-udf).</span></span> <span data-ttu-id="07249-106">실제로 어떤 코드라도 디버깅이 필요하며 빅 데이터 시스템에는 로그 파일과 같이 제한된 런타임 디버깅 정보만 제공될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07249-106">In practice any code may need debugging, and big data systems may only provide limited runtime debugging information such as log files.</span></span>

<span data-ttu-id="07249-107">라는 기능을 제공 하는 azure 데이터 레이크 Tools for Visual Studio **꼭 짓 점 디버그 실패**, hello 클라우드 tooyour 디버깅을 위해 로컬 컴퓨터에서 실패 한 작업을 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07249-107">Azure Data Lake Tools for Visual Studio provides a feature called **Failed Vertex Debug**, which lets you clone a failed job from hello cloud tooyour local machine for debugging.</span></span> <span data-ttu-id="07249-108">로컬 복제본 hello hello 전체 클라우드 환경을에서는 모든 입력된 데이터와 사용자 코드를 포함 하 여 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="07249-108">hello local clone captures hello entire cloud environment, including any input data and user code.</span></span>

<span data-ttu-id="07249-109">hello 다음 비디오에서는 Azure 데이터 레이크 도구에서 꼭 짓 점 디버깅 하지 못했습니다 Visual Studio에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="07249-109">hello following video demonstrates Failed Vertex Debug in Azure Data Lake Tools for Visual Studio.</span></span>

> [!VIDEO https://e0d1.wpc.azureedge.net/80E0D1/OfficeMixProdMediaBlobStorage/asset-d3aeab42-6149-4ecc-b044-aa624901ab32/b0fc0373c8f94f1bb8cd39da1310adb8.mp4?sv=2012-02-12&sr=c&si=a91fad76-cfdd-4513-9668-483de39e739c&sig=K%2FR%2FdnIi9S6P%2FBlB3iLAEV5pYu6OJFBDlQy%2FQtZ7E7M%3D&se=2116-07-19T09:27:30Z&rscd=attachment%3B%20filename%3DDebugyourcustomcodeinUSQLADLA.mp4]
>

> [!NOTE]
> <span data-ttu-id="07249-110">아직 설치 되지 않은 경우 visual Studio 필요한 두 업데이트를 수행 하는 hello: [Microsoft Visual c + + 2015 재배포 가능 패키지 업데이트 3](https://www.microsoft.com/en-us/download/details.aspx?id=53840) 및 [유니버설 C 런타임에 대 한 Windows](https://www.microsoft.com/download/details.aspx?id=50410)합니다.</span><span class="sxs-lookup"><span data-stu-id="07249-110">Visual Studio requires hello following two updates, if they are not already installed: [Microsoft Visual C++ 2015 Redistributable Update 3](https://www.microsoft.com/en-us/download/details.aspx?id=53840) and the [Universal C Runtime for Windows](https://www.microsoft.com/download/details.aspx?id=50410).</span></span>

## <a name="download-failed-vertex-toolocal-machine"></a><span data-ttu-id="07249-111">꼭 짓 점 toolocal 컴퓨터 다운로드 실패</span><span class="sxs-lookup"><span data-stu-id="07249-111">Download failed vertex toolocal machine</span></span>

<span data-ttu-id="07249-112">Visual Studio 용 Azure 데이터 레이크 도구에서 실패 한 작업을 열면 hello 오류 탭에서 자세한 오류 메시지가 포함 된 노란색 경고 표시줄을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="07249-112">When you open a failed job in Azure Data Lake Tools for Visual Studio, you see a yellow alert bar with detailed error messages in hello error tab.</span></span>

1. <span data-ttu-id="07249-113">클릭 **다운로드** toodownload hello 모든 필요한 리소스 및 입력된 스트림을 합니다.</span><span class="sxs-lookup"><span data-stu-id="07249-113">Click **Download** toodownload all hello required resources and input streams.</span></span> <span data-ttu-id="07249-114">클릭 하 여 hello 다운로드 완료 하지 **을 다시 시도**합니다.</span><span class="sxs-lookup"><span data-stu-id="07249-114">If hello download doesn't complete, click **Retry**.</span></span>

2. <span data-ttu-id="07249-115">클릭 **열려** hello 다운로드에는 로컬 디버깅 환경을 toogenerate 완료 된 후입니다.</span><span class="sxs-lookup"><span data-stu-id="07249-115">Click **Open** after hello download completes toogenerate a local debugging environment.</span></span> <span data-ttu-id="07249-116">디버깅 솔루션이 있는 새로운 Visual Studio 인스턴스가 자동으로 생성되고 열립니다.</span><span class="sxs-lookup"><span data-stu-id="07249-116">A new Visual Studio instance with a debugging solution is automatically created and opened.</span></span>

![Azure Data Lake Analytics U-SQL 디버그 Visual Studio 정점 다운로드](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-download-vertex.png)

<span data-ttu-id="07249-118">작업에는 코드 숨김 소스 파일이나 등록된 어셈블리가 포함될 수 있으며 이러한 두 가지 유형에는 서로 다른 디버깅 시나리오가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07249-118">Jobs may include code-behind source files or registered assemblies, and these two types have different debugging scenarios.</span></span>

- [<span data-ttu-id="07249-119">코드 숨김을 사용하여 실패한 작업 디버그</span><span class="sxs-lookup"><span data-stu-id="07249-119">Debug a failed job with code-behind</span></span>](#debug-job-failed-with-code-behind)
- [<span data-ttu-id="07249-120">어셈블리를 사용하여 실패한 작업 디버그</span><span class="sxs-lookup"><span data-stu-id="07249-120">Debug a failed job with assemblies</span></span>](#debug-job-failed-with-assemblies)


## <a name="debug-job-failed-with-code-behind"></a><span data-ttu-id="07249-121">코드 숨김으로 인해 실패한 작업 디버그</span><span class="sxs-lookup"><span data-stu-id="07249-121">Debug job failed with code-behind</span></span>

<span data-ttu-id="07249-122">U-SQL 작업에 실패 하 고 사용자 코드를 포함 하는 hello 작업 하는 경우 (일반적으로 이름이 `Script.usql.cs` U-SQL 프로젝트에서), 해당 소스 코드는 솔루션을 디버깅 하는 hello로 가져온 합니다.</span><span class="sxs-lookup"><span data-stu-id="07249-122">If a U-SQL job fails, and hello job includes user code (typically named `Script.usql.cs` in a U-SQL project), that source code is imported into hello debugging solution.</span></span>  <span data-ttu-id="07249-123">여기에서 hello Visual Studio 디버깅 도구 (조사식, 변수 등) tootroubleshoot hello 문제를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07249-123">From there you can use hello Visual Studio debugging tools (watch, variables, etc.) tootroubleshoot hello problem.</span></span>

> [!NOTE]
> <span data-ttu-id="07249-124">를 디버깅 하려면 먼저 수 있는지 toocheck **공용 언어 런타임 예외** hello 예외 설정 창에서 (**Ctrl + Alt + E**).</span><span class="sxs-lookup"><span data-stu-id="07249-124">Before debugging, be sure toocheck **Common Language Runtime Exceptions** in hello Exception Settings window (**Ctrl + Alt + E**).</span></span>

![Azure Data Lake Analytics U-SQL 디버그 Visual Studio 설정](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-clr-exception-setting.png)

1. <span data-ttu-id="07249-126">키를 눌러 **F5** toorun hello 코드 숨김 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="07249-126">Press **F5** toorun hello code-behind code.</span></span> <span data-ttu-id="07249-127">예외로 인해 중지될 때까지 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="07249-127">It will run until it is stopped by an exception.</span></span>

2. <span data-ttu-id="07249-128">열기 hello `ADLTool_Codebehind.usql.cs` 중단점을 설정 하 고 파일 키를 누릅니다 **F5** toodebug hello 코드 단계별 합니다.</span><span class="sxs-lookup"><span data-stu-id="07249-128">Open hello `ADLTool_Codebehind.usql.cs` file and set breakpoints, then press **F5** toodebug hello code step by step.</span></span>

    ![Azure Data Lake Analytics U-SQL 디버그 예외](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-debug-exception.png)

## <a name="debug-job-failed-with-assemblies"></a><span data-ttu-id="07249-130">어셈블리로 인해 실패한 작업 디버그</span><span class="sxs-lookup"><span data-stu-id="07249-130">Debug job failed with assemblies</span></span>

<span data-ttu-id="07249-131">U-SQL 스크립트에서 등록 된 어셈블리를 사용 하는 경우 hello 시스템 hello 소스 코드를 자동으로 가져올 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="07249-131">If you use registered assemblies in your U-SQL script, hello system can't get hello source code automatically.</span></span> <span data-ttu-id="07249-132">이 경우 hello 어셈블리의 소스 코드 파일 toohello 솔루션을 수동으로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="07249-132">In this case, manually add hello assemblies' source code files toohello solution.</span></span>

### <a name="configure-hello-solution"></a><span data-ttu-id="07249-133">Hello 솔루션 구성</span><span class="sxs-lookup"><span data-stu-id="07249-133">Configure hello solution</span></span>

1. <span data-ttu-id="07249-134">마우스 오른쪽 단추로 클릭 **솔루션 'VertexDebug' > 추가 > 기존 프로젝트...**  toofind 어셈블리의 소스 코드를 hello 및 솔루션을 디버깅 하는 hello 프로젝트 toohello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="07249-134">Right-click **Solution 'VertexDebug' > Add > Existing Project...** toofind hello assemblies' source code and add hello project toohello debugging solution.</span></span>

    ![Azure Data Lake Analytics U-SQL 디버그 - 프로젝트 추가](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-add-project-to-debug-solution.png)

2. <span data-ttu-id="07249-136">마우스 오른쪽 단추로 클릭 **LocalVertexHost > 속성** hello 솔루션 및 복사 hello에 **작업 디렉터리** 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="07249-136">Right-click **LocalVertexHost > Properties** in hello solution and copy hello **Working Directory** path.</span></span>

3. <span data-ttu-id="07249-137">마우스 오른쪽 단추로 클릭 **어셈블리 소스 코드 프로젝트 > 속성**선택, hello **빌드** 왼쪽을 탭 하 고으로 복사 하는 hello 경로 붙여 넣습니다 **출력 > 출력 경로**합니다.</span><span class="sxs-lookup"><span data-stu-id="07249-137">Right-Click **assembly source code project > Properties**, select hello **Build** tab at left, and paste hello copied path as **Output > Output path**.</span></span>

    ![Azure Data Lake Analytics U-SQL 디버그 - pdb 경로 설정](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-set-pdb-path.png)

4. <span data-ttu-id="07249-139">**Ctrl + Alt + E**를 누르고 예외 설정 창에서 **공용 언어 런타임 예외**를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="07249-139">Press **Ctrl + Alt + E**, check **Common Language Runtime Exceptions** in Exception Settings window.</span></span>

### <a name="start-debug"></a><span data-ttu-id="07249-140">디버그 시작</span><span class="sxs-lookup"><span data-stu-id="07249-140">Start debug</span></span>

1. <span data-ttu-id="07249-141">마우스 오른쪽 단추로 클릭 **어셈블리 소스 코드 프로젝트 > 다시 작성** toooutput.pdb 파일 toohello `LocalVertexHost` 작업 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="07249-141">Right-click **assembly source code project > Rebuild** toooutput .pdb files toohello `LocalVertexHost` working directory.</span></span>

2. <span data-ttu-id="07249-142">키를 눌러 **F5** hello 프로젝트 예외로 인해 중지 될 때까지 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="07249-142">Press **F5** and hello project will run until it is stopped by an exception.</span></span> <span data-ttu-id="07249-143">Hello 안전 하 게 무시할 수 있는 경고 메시지의 뒤에 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07249-143">You may see hello following warning message, which you can safely ignore.</span></span> <span data-ttu-id="07249-144">Tooa 분 tooget toohello 디버그 화면을 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07249-144">It can take up tooa minute tooget toohello debug screen.</span></span>

    ![Azure Data Lake Analytics U-SQL 디버그 Visual Studio 경고](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-visual-studio-u-sql-debug-warning.png)

3. <span data-ttu-id="07249-146">소스 코드를 열고 중단점을 설정 키를 누릅니다 **F5** toodebug hello 코드 단계별 지침.</span><span class="sxs-lookup"><span data-stu-id="07249-146">Open your source code and set breakpoints, then press **F5** toodebug hello code step by step.</span></span>

<span data-ttu-id="07249-147">Hello Visual Studio 디버깅 도구 (조사식, 변수 등) tootroubleshoot hello 문제를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07249-147">You can also use hello Visual Studio debugging tools (watch, variables, etc.) tootroubleshoot hello problem.</span></span>

> [!NOTE]
> <span data-ttu-id="07249-148">Hello 코드 업데이트 toogenerate.pdb 파일을 수정한 후 때마다 hello 어셈블리 소스 코드 프로젝트를 다시 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="07249-148">Rebuild hello assembly source code project each time after you modify hello code toogenerate updated .pdb files.</span></span>

<span data-ttu-id="07249-149">디버깅 후 hello 프로젝트 완료 되 면 hello 출력 창에는 hello 메시지의 뒤에 표시:</span><span class="sxs-lookup"><span data-stu-id="07249-149">After debugging, if hello project completes successfully hello output window shows hello following message:</span></span>

```
hello Program 'LocalVertexHost.exe' has exited with code 0 (0x0).
```

![Azure Data Lake Analytics U-SQL 디버그 성공](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-debug-succeed.png)

## <a name="resubmit-hello-job"></a><span data-ttu-id="07249-151">Hello 작업을 다시 제출 하십시오.</span><span class="sxs-lookup"><span data-stu-id="07249-151">Resubmit hello job</span></span>

<span data-ttu-id="07249-152">디버깅을 완료 한 후에 hello 실패 한 작업을 다시 전송 하십시오.</span><span class="sxs-lookup"><span data-stu-id="07249-152">Once you have completed debugging, resubmit hello failed job.</span></span>

1. <span data-ttu-id="07249-153">코드 숨김 솔루션으로 작업에 대 한 C# 코드 hello 코드 숨김 소스 파일에 복사 (일반적으로 `Script.usql.cs`).</span><span class="sxs-lookup"><span data-stu-id="07249-153">For jobs with code-behind solutions, copy your C# code into hello code-behind source file (typically `Script.usql.cs`).</span></span>
2. <span data-ttu-id="07249-154">어셈블리를 사용한 작업에 대 한 ADLA 데이터베이스로 업데이트 hello.dll 어셈블리를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="07249-154">For jobs with assemblies, register hello updated .dll assemblies into your ADLA database:</span></span>
    1. <span data-ttu-id="07249-155">서버 탐색기 또는 클라우드 탐색기에서 확장 hello **ADLA 계정 > 데이터베이스** 노드.</span><span class="sxs-lookup"><span data-stu-id="07249-155">From Server Explorer or Cloud Explorer, expand hello **ADLA account > Databases** node.</span></span>
    2. <span data-ttu-id="07249-156">마우스 오른쪽 단추로 클릭 **어셈블리** hello ADLA 데이터베이스와 새.dll 어셈블리를 등록 하 고: ![어셈블리를 등록 하는 Azure 데이터 레이크 분석 U-SQL 디버그](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-register-assembly.png)</span><span class="sxs-lookup"><span data-stu-id="07249-156">Right-click **Assemblies** and register your new .dll assemblies with hello ADLA database: ![Azure Data Lake Analytics U-SQL debug register assembly](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-register-assembly.png)</span></span>
3. <span data-ttu-id="07249-157">작업을 다시 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="07249-157">Resubmit your job.</span></span>

## <a name="next-steps"></a><span data-ttu-id="07249-158">다음 단계</span><span class="sxs-lookup"><span data-stu-id="07249-158">Next steps</span></span>

- [<span data-ttu-id="07249-159">U-SQL 프로그래밍 기능 가이드</span><span class="sxs-lookup"><span data-stu-id="07249-159">U-SQL programmability guide</span></span>](data-lake-analytics-u-sql-programmability-guide.md)
- [<span data-ttu-id="07249-160">Azure Data Lake Analytics 작업에 대한 U-SQL 사용자 정의 연산자를 개발합니다.</span><span class="sxs-lookup"><span data-stu-id="07249-160">Develop U-SQL User-defined operators for Azure Data Lake Analytics jobs</span></span>](data-lake-analytics-u-sql-develop-user-defined-operators.md)
- [<span data-ttu-id="07249-161">자습서: Visual Studio용 데이터 레이크 도구를 사용하여 U-SQL 스크립트 개발</span><span class="sxs-lookup"><span data-stu-id="07249-161">Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)

---
title: "Azure Data Lake Tools: Visual Studio Code를 사용한 U-SQL 로컬 실행 및 로컬 디버그 | Microsoft Docs"
description: "Visual Studio Code toolocal 및 로컬 실행에 대 한 Azure 데이터 레이크 도구 toouse 디버깅 하는 방법에 대해 알아봅니다."
Keywords: "VScode, Azure 데이터 레이크 도구, 로컬 실행 로컬 디버그, 디버깅, 로컬 미리 보기 저장소 파일 업로드 toostorage 경로"
services: data-lake-analytics
documentationcenter: 
author: jejiang
manager: DJ
editor: jejiang
tags: azure-portal
ms.assetid: dc9b21d8-c5f4-4f77-bcbc-eff458f48de2
ms.service: data-lake-analytics
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: big-data
ms.date: 07/14/2017
ms.author: jejiang
ms.openlocfilehash: fb152f07fe8c4b03dde8fb8e62c7475eccda0578
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="u-sql-local-run-and-local-debug-with-visual-studio-code"></a><span data-ttu-id="1220b-104">Visual Studio Code로 U-SQL 로컬 실행 및 로컬 디버그</span><span class="sxs-lookup"><span data-stu-id="1220b-104">U-SQL local run and local debug with Visual Studio Code</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1220b-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="1220b-105">Prerequisites</span></span>
<span data-ttu-id="1220b-106">이러한 절차를 시작 하기 전에 필수 구성 요소가 충족 다음 hello 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1220b-106">Make sure you have hello following prerequisites in place before you start these procedures:</span></span>
- <span data-ttu-id="1220b-107">Azure Data Lake Tool for Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="1220b-107">Azure Data Lake Tool for Visual Studio Code.</span></span> <span data-ttu-id="1220b-108">자세한 내용은 [Azure Data Lake Tools for Visual Studio Code 사용](data-lake-analytics-data-lake-tools-for-vscode.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1220b-108">For instructions, see [Use Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span></span>
- <span data-ttu-id="1220b-109">C# Visual Studio Code (tooperform U SQL 로컬 디버그 경우)에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="1220b-109">C# for Visual Studio Code (if you want tooperform a U-SQL local debug).</span></span>

   ![Data Lake Tools for Visual Studio Code에 C# 설치](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-install-ms-vscodecsharp.png)
   
   > [!NOTE]
   > <span data-ttu-id="1220b-111">hello U-SQL 로컬 실행 및 디버그 기능 현재만 지원 Windows 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="1220b-111">hello U-SQL local run and debug features currently only support Windows users.</span></span> 


## <a name="set-up-hello-u-sql-local-run-environment"></a><span data-ttu-id="1220b-112">Hello U-SQL 로컬 실행된 환경 설정</span><span class="sxs-lookup"><span data-stu-id="1220b-112">Set up hello U-SQL local run environment</span></span>

1. <span data-ttu-id="1220b-113">Ctrl + Shift + P tooopen hello 명령 팔레트를 선택한 다음 입력 **ADL: LocalRun 종속성 다운로드** toodownload hello 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="1220b-113">Select Ctrl+Shift+P tooopen hello command palette, and then enter **ADL: Download LocalRun Dependency** toodownload hello packages.</span></span>  

   ![Hello ADL LocalRun 종속성 패키지를 다운로드 합니다.](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/DownloadLocalRun.png)

2. <span data-ttu-id="1220b-115">Hello 종속성 패키지가 hello에 표시 된 hello 경로에서 찾은 **출력** 창에서 한 다음 BuildTools 및 Win10SDK 10240 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="1220b-115">Locate hello dependency packages from hello path shown in hello **Output** pane, and then install BuildTools and Win10SDK 10240.</span></span> <span data-ttu-id="1220b-116">다음은 예제 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="1220b-116">Here is an example path:</span></span>  
`C:\Users\xxx\.vscode\extensions\usqlextpublisher.usql-vscode-ext-x.x.x\LocalRunDependency
`  
  <span data-ttu-id="1220b-117">![Hello 종속성 패키지 찾기](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/LocateDependencyPath.png)</span><span class="sxs-lookup"><span data-stu-id="1220b-117">![Locate hello dependency packages](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/LocateDependencyPath.png)</span></span>

   <span data-ttu-id="1220b-118">a.</span><span class="sxs-lookup"><span data-stu-id="1220b-118">a.</span></span> <span data-ttu-id="1220b-119">tooinstall BuildTools, hello 마법사의 지시를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="1220b-119">tooinstall BuildTools, follow hello wizard instructions.</span></span>   

  ![BuildTools 설치](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/InstallBuildTools.png)

   <span data-ttu-id="1220b-121">b.</span><span class="sxs-lookup"><span data-stu-id="1220b-121">b.</span></span> <span data-ttu-id="1220b-122">tooinstall Win10SDK 10240 hello 마법사의 지시를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="1220b-122">tooinstall Win10SDK 10240, follow hello wizard instructions.</span></span>  

  ![Win10SDK 10240 설치](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/InstallWin10SDK.png)

3. <span data-ttu-id="1220b-124">Hello 환경 변수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1220b-124">Set up hello environment variable.</span></span> <span data-ttu-id="1220b-125">집합 hello **SCOPE_CPP_SDK** 환경 변수를:</span><span class="sxs-lookup"><span data-stu-id="1220b-125">Set hello **SCOPE_CPP_SDK** environment variable to:</span></span>  
`C:\Users\xxx\.vscode\extensions\usqlextpublisher.usql-vscode-ext-x.x.x\LocalRunDependency\CppSDK_3rdparty
`  
4. <span data-ttu-id="1220b-126">Hello OS toomake hello 환경 변수 설정이 적용 되었는지 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="1220b-126">Restart hello OS toomake sure that hello environment variable settings take effect.</span></span>  

   ![Hello SCOPE_CPP_SDK 환경 변수에서 설치 되어 있는지 확인](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/ConfigScopeCppSDk.png)

## <a name="start-hello-local-run-service-and-submit-hello-u-sql-job-tooa-local-account"></a><span data-ttu-id="1220b-128">Hello 로컬 실행된 서비스를 시작 하 고 hello tooa 로컬 계정 U-SQL 작업 제출</span><span class="sxs-lookup"><span data-stu-id="1220b-128">Start hello local run service and submit hello U-SQL job tooa local account</span></span> 
<span data-ttu-id="1220b-129">Hello 처음 사용자에 대 한 증명된 toodownload hello ADL 중인: LocalRun 종속성 다운로드를 아직 설치 되지 않은 경우 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="1220b-129">For hello first-time user, you are prompted toodownload hello ADL: Download LocalRun Dependency packages if they are not already installed.</span></span>
1. <span data-ttu-id="1220b-130">Ctrl + Shift + P tooopen hello 명령 팔레트를 선택한 다음 입력 **ADL: 로컬 실행 서비스 시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="1220b-130">Select Ctrl+Shift+P tooopen hello command palette, and then enter **ADL: Start Local Run Service**.</span></span>
2. <span data-ttu-id="1220b-131">선택 **Accept** tooaccept hello 처음으로 hello에 대 한 Microsoft 소프트웨어 사용 조건.</span><span class="sxs-lookup"><span data-stu-id="1220b-131">Select **Accept** tooaccept hello Microsoft Software License Terms for hello first time.</span></span> 

   ![Hello Microsoft 소프트웨어 사용 조건에 동의](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/AcceptEULA.png)   
3. <span data-ttu-id="1220b-133">hello cmd 콘솔이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="1220b-133">hello cmd console opens.</span></span> <span data-ttu-id="1220b-134">신규 사용자 tooenter 필요 **3**, 입력 및 출력 데이터에 대 한 hello 로컬 폴더 경로 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="1220b-134">For first-time users, you need tooenter **3**, and then locate hello local folder path for your data input and output.</span></span> <span data-ttu-id="1220b-135">다른 옵션에 대 한 hello 기본값을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1220b-135">For other options, you can use hello default values.</span></span> 

   ![Data Lake Tools for Visual Studio Code가 cmd 로컬 실행](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-cmd.png)
4. <span data-ttu-id="1220b-137">Ctrl + Shift + P tooopen hello 명령 색상표를 선택, 입력 **ADL: 작업 제출**를 선택한 후 **로컬** toosubmit hello 작업 tooyour 로컬 계정.</span><span class="sxs-lookup"><span data-stu-id="1220b-137">Select Ctrl+Shift+P tooopen hello command palette, enter **ADL: Submit Job**, and then select **Local** toosubmit hello job tooyour local account.</span></span>

   ![Data Lake Tools for Visual Studio Code 로컬 선택](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-select-local.png)
5. <span data-ttu-id="1220b-139">Hello 작업을 제출 하면 hello 제출 세부 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1220b-139">After you submit hello job, you can view hello submission details.</span></span> <span data-ttu-id="1220b-140">선택 tooview hello 전송에 자세히 설명 **jobUrl** hello에 **출력** 창.</span><span class="sxs-lookup"><span data-stu-id="1220b-140">tooview hello submission details select **jobUrl** in hello **Output** window.</span></span> <span data-ttu-id="1220b-141">Hello cmd 콘솔에서 hello 작업 전송 상태를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1220b-141">You can also view hello job submission status from hello cmd console.</span></span> <span data-ttu-id="1220b-142">입력 **7** hello cmd 콘솔에서 tooknow 하려는 경우 자세한 작업 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="1220b-142">Enter **7** in hello cmd console if you want tooknow more job details.</span></span>

   <span data-ttu-id="1220b-143">![Data Lake Tools for Visual Studio Code 로컬 실행 출력](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-result.png)
   ![Data Lake Tools for Visual Studio Code 로컬 실행 cmd 상태](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-localrun-cmd-status.png)</span><span class="sxs-lookup"><span data-stu-id="1220b-143">![Data Lake Tools for Visual Studio Code local run output](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-result.png)
![Data Lake Tools for Visual Studio Code local run cmd status](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-localrun-cmd-status.png)</span></span> 


## <a name="start-a-local-debug-for-hello-u-sql-job"></a><span data-ttu-id="1220b-144">Hello U-SQL 작업에 대 한 로컬 디버그를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="1220b-144">Start a local debug for hello U-SQL job</span></span>  
<span data-ttu-id="1220b-145">Hello 처음 사용자에 대 한 증명된 toodownload hello ADL 중인: LocalRun 종속성 다운로드를 아직 설치 되지 않은 경우 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="1220b-145">For hello first-time user, you are prompted toodownload hello ADL: Download LocalRun Dependency packages if they are not already installed.</span></span>
  
1. <span data-ttu-id="1220b-146">Ctrl + Shift + P tooopen hello 명령 팔레트를 선택한 다음 입력 **ADL: 로컬 실행 서비스 시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="1220b-146">Select Ctrl+Shift+P tooopen hello command palette, and then enter **ADL: Start Local Run Service**.</span></span> <span data-ttu-id="1220b-147">hello cmd 콘솔이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="1220b-147">hello cmd console opens.</span></span> <span data-ttu-id="1220b-148">해당 hello 있는지 확인 **DataRoot** 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1220b-148">Make sure that hello **DataRoot** is set.</span></span>
3. <span data-ttu-id="1220b-149">C# 코드 숨김에서 중단점을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1220b-149">Set a breakpoint in your C# code-behind.</span></span>
4. <span data-ttu-id="1220b-150">Hello 스크립트 편집기에서 다시 Ctrl + Shift + P tooopen hello 명령 콘솔을 선택 하 고 다음을 입력 **로컬 디버그** toostart 로컬 디버그 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="1220b-150">Back in hello script editor, select Ctrl+Shift+P tooopen hello command console, and then enter **Local Debug** toostart your local debug service.</span></span>

![Data Lake Tools for Visual Studio Code 로컬 디버그 결과](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-debug-result.png)


## <a name="next-steps"></a><span data-ttu-id="1220b-152">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1220b-152">Next steps</span></span>
- <span data-ttu-id="1220b-153">Azure Data Lake Tools for Visual Studio Code 사용에 대해서는 [Azure Data Lake Tools for Visual Studio Code 사용](data-lake-analytics-data-lake-tools-for-vscode.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1220b-153">For using Azure Data Lake Tools for Visual Studio Code, see [Use Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span></span>
- <span data-ttu-id="1220b-154">Data Lake Analytics 시작 정보는 [자습서: Azure Data Lake Analytics 시작](data-lake-analytics-get-started-portal.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1220b-154">For getting started information on Data Lake Analytics, see [Tutorial: Get started with Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span></span>
- <span data-ttu-id="1220b-155">Data Lake Tools for Visual Studio에 대한 자세한 내용은 [자습서: Data Lake Tools for Visual Studio를 사용하여 U-SQL 스크립트 개발](data-lake-analytics-data-lake-tools-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1220b-155">For information about Data Lake Tools for Visual Studio, see [Tutorial: Develop U-SQL scripts by using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
- <span data-ttu-id="1220b-156">Hello에 대 한 내용은 어셈블리를 개발, [Azure 데이터 레이크 분석 작업에 대 한 개발 U-SQL 어셈블리](data-lake-analytics-u-sql-develop-assemblies.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1220b-156">For hello information on developing assemblies, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md).</span></span>

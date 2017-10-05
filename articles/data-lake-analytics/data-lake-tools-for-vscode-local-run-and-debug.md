---
title: "Azure Data Lake Tools: Visual Studio Code를 사용한 U-SQL 로컬 실행 및 로컬 디버그 | Microsoft Docs"
description: "Azure Data Lake Tools for Visual Studio Code를 사용하여 로컬 실행 및 로컬 디버그하는 방법을 알아봅니다."
Keywords: "VScode,Azure Data Lake Tools,로컬 실행,로컬 디버그,로컬 디버그,저장소 파일 미리 보기,저장소 경로로 업로드"
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
ms.openlocfilehash: 367e4ba792f83d6ee246208306e4c09b69cb49ef
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="u-sql-local-run-and-local-debug-with-visual-studio-code"></a><span data-ttu-id="e11ef-104">Visual Studio Code로 U-SQL 로컬 실행 및 로컬 디버그</span><span class="sxs-lookup"><span data-stu-id="e11ef-104">U-SQL local run and local debug with Visual Studio Code</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e11ef-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="e11ef-105">Prerequisites</span></span>
<span data-ttu-id="e11ef-106">이러한 절차를 시작하기 전에 다음 필수 조건을 갖추고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e11ef-106">Make sure you have the following prerequisites in place before you start these procedures:</span></span>
- <span data-ttu-id="e11ef-107">Azure Data Lake Tool for Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="e11ef-107">Azure Data Lake Tool for Visual Studio Code.</span></span> <span data-ttu-id="e11ef-108">자세한 내용은 [Azure Data Lake Tools for Visual Studio Code 사용](data-lake-analytics-data-lake-tools-for-vscode.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e11ef-108">For instructions, see [Use Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span></span>
- <span data-ttu-id="e11ef-109">C# for Visual Studio Code(U-SQL 로컬 디버그를 수행하려는 경우)</span><span class="sxs-lookup"><span data-stu-id="e11ef-109">C# for Visual Studio Code (if you want to perform a U-SQL local debug).</span></span>

   ![Data Lake Tools for Visual Studio Code에 C# 설치](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-install-ms-vscodecsharp.png)
   
   > [!NOTE]
   > <span data-ttu-id="e11ef-111">U-SQL 로컬 실행 및 디버그 기능은 현재 Windows 사용자만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="e11ef-111">The U-SQL local run and debug features currently only support Windows users.</span></span> 


## <a name="set-up-the-u-sql-local-run-environment"></a><span data-ttu-id="e11ef-112">U-SQL 로컬 실행 환경 설정</span><span class="sxs-lookup"><span data-stu-id="e11ef-112">Set up the U-SQL local run environment</span></span>

1. <span data-ttu-id="e11ef-113">Ctrl+Shift+P를 선택하여 명령 팔레트를 연 다음 **ADL: Download LocalRun Dependency**를 입력하여 패키지를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="e11ef-113">Select Ctrl+Shift+P to open the command palette, and then enter **ADL: Download LocalRun Dependency** to download the packages.</span></span>  

   ![ADL LocalRun Dependency 패키지 다운로드](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/DownloadLocalRun.png)

2. <span data-ttu-id="e11ef-115">**출력** 패널에 표시된 경로에서 종속성 패키지를 찾은 다음 BuildTools 및 Win10SDK 10240을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e11ef-115">Locate the dependency packages from the path shown in the **Output** pane, and then install BuildTools and Win10SDK 10240.</span></span> <span data-ttu-id="e11ef-116">다음은 예제 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="e11ef-116">Here is an example path:</span></span>  
`C:\Users\xxx\.vscode\extensions\usqlextpublisher.usql-vscode-ext-x.x.x\LocalRunDependency
`  
  <span data-ttu-id="e11ef-117">![종속성 패키지 찾기](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/LocateDependencyPath.png)</span><span class="sxs-lookup"><span data-stu-id="e11ef-117">![Locate the dependency packages](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/LocateDependencyPath.png)</span></span>

   <span data-ttu-id="e11ef-118">a.</span><span class="sxs-lookup"><span data-stu-id="e11ef-118">a.</span></span> <span data-ttu-id="e11ef-119">BuildTools를 설치하려면 마법사의 지시를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="e11ef-119">To install BuildTools, follow the wizard instructions.</span></span>   

  ![BuildTools 설치](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/InstallBuildTools.png)

   <span data-ttu-id="e11ef-121">b.</span><span class="sxs-lookup"><span data-stu-id="e11ef-121">b.</span></span> <span data-ttu-id="e11ef-122">Win10SDK 10240을 설치하려면 마법사의 지시를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="e11ef-122">To install Win10SDK 10240, follow the wizard instructions.</span></span>  

  ![Win10SDK 10240 설치](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/InstallWin10SDK.png)

3. <span data-ttu-id="e11ef-124">환경 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e11ef-124">Set up the environment variable.</span></span> <span data-ttu-id="e11ef-125">**SCOPE_CPP_SDK** 환경 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e11ef-125">Set the **SCOPE_CPP_SDK** environment variable to:</span></span>  
`C:\Users\xxx\.vscode\extensions\usqlextpublisher.usql-vscode-ext-x.x.x\LocalRunDependency\CppSDK_3rdparty
`  
4. <span data-ttu-id="e11ef-126">환경 변수 설정을 적용하려면 운영 체제를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e11ef-126">Restart the OS to make sure that the environment variable settings take effect.</span></span>  

   ![SCOPE_CPP_SDK 환경 변수가 설치되어 있는지 확인](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/ConfigScopeCppSDk.png)

## <a name="start-the-local-run-service-and-submit-the-u-sql-job-to-a-local-account"></a><span data-ttu-id="e11ef-128">로컬 실행 서비스 시작 및 로컬 계정에 U-SQL 작업 제출</span><span class="sxs-lookup"><span data-stu-id="e11ef-128">Start the local run service and submit the U-SQL job to a local account</span></span> 
<span data-ttu-id="e11ef-129">첫 번째 사용자의 경우 아직 설치되지 않은 경우 ADL: Download LocalRun Dependency 패키지를 다운로드하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e11ef-129">For the first-time user, you are prompted to download the ADL: Download LocalRun Dependency packages if they are not already installed.</span></span>
1. <span data-ttu-id="e11ef-130">Ctrl+Shift+P를 선택하여 명령 팔레트를 연 다음 **ADL: Start Local Run Service**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e11ef-130">Select Ctrl+Shift+P to open the command palette, and then enter **ADL: Start Local Run Service**.</span></span>
2. <span data-ttu-id="e11ef-131">**Accept**를 선택하여 처음으로 Microsoft 소프트웨어 사용 조건에 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="e11ef-131">Select **Accept** to accept the Microsoft Software License Terms for the first time.</span></span> 

   ![Microsoft 소프트웨어 사용 조건에 동의](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/AcceptEULA.png)   
3. <span data-ttu-id="e11ef-133">cmd 콘솔이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="e11ef-133">The cmd console opens.</span></span> <span data-ttu-id="e11ef-134">처음 사용하는 경우 **3**을 입력한 다음 데이터 입력 및 출력을 위한 로컬 폴더 경로를 찾아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e11ef-134">For first-time users, you need to enter **3**, and then locate the local folder path for your data input and output.</span></span> <span data-ttu-id="e11ef-135">다른 옵션은 기본값을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e11ef-135">For other options, you can use the default values.</span></span> 

   ![Data Lake Tools for Visual Studio Code가 cmd 로컬 실행](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-cmd.png)
4. <span data-ttu-id="e11ef-137">Ctrl+Shift+P를 선택하여 명령 팔레트를 열고 **ADL: Submit Job**을 입력한 다음 **Local**을 선택하여 작업을 로컬 계정에 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="e11ef-137">Select Ctrl+Shift+P to open the command palette, enter **ADL: Submit Job**, and then select **Local** to submit the job to your local account.</span></span>

   ![Data Lake Tools for Visual Studio Code 로컬 선택](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-select-local.png)
5. <span data-ttu-id="e11ef-139">작업을 제출하면 제출 세부 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e11ef-139">After you submit the job, you can view the submission details.</span></span> <span data-ttu-id="e11ef-140">제출 세부 정보를 보려면 **Output** 창에서 **jobUrl**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e11ef-140">To view the submission details select **jobUrl** in the **Output** window.</span></span> <span data-ttu-id="e11ef-141">cmd 콘솔에서 작업 제출 상태를 볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e11ef-141">You can also view the job submission status from the cmd console.</span></span> <span data-ttu-id="e11ef-142">작업 세부 정보에 대해 더 알고 싶은 경우 cmd 콘솔에 **7**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e11ef-142">Enter **7** in the cmd console if you want to know more job details.</span></span>

   <span data-ttu-id="e11ef-143">![Data Lake Tools for Visual Studio Code 로컬 실행 출력](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-result.png)
   ![Data Lake Tools for Visual Studio Code 로컬 실행 cmd 상태](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-localrun-cmd-status.png)</span><span class="sxs-lookup"><span data-stu-id="e11ef-143">![Data Lake Tools for Visual Studio Code local run output](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-result.png)
![Data Lake Tools for Visual Studio Code local run cmd status](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-localrun-cmd-status.png)</span></span> 


## <a name="start-a-local-debug-for-the-u-sql-job"></a><span data-ttu-id="e11ef-144">U-SQL 작업에 대한 로컬 디버그 시작</span><span class="sxs-lookup"><span data-stu-id="e11ef-144">Start a local debug for the U-SQL job</span></span>  
<span data-ttu-id="e11ef-145">첫 번째 사용자의 경우 아직 설치되지 않은 경우 ADL: Download LocalRun Dependency 패키지를 다운로드하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e11ef-145">For the first-time user, you are prompted to download the ADL: Download LocalRun Dependency packages if they are not already installed.</span></span>
  
1. <span data-ttu-id="e11ef-146">Ctrl+Shift+P를 선택하여 명령 팔레트를 연 다음 **ADL: Start Local Run Service**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e11ef-146">Select Ctrl+Shift+P to open the command palette, and then enter **ADL: Start Local Run Service**.</span></span> <span data-ttu-id="e11ef-147">cmd 콘솔이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="e11ef-147">The cmd console opens.</span></span> <span data-ttu-id="e11ef-148">**DataRoot**가 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e11ef-148">Make sure that the **DataRoot** is set.</span></span>
3. <span data-ttu-id="e11ef-149">C# 코드 숨김에서 중단점을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e11ef-149">Set a breakpoint in your C# code-behind.</span></span>
4. <span data-ttu-id="e11ef-150">스크립트 편집기로 돌아가 Ctrl+Shift+P를 선택하여 명령 콘솔을 연 다음 **Local Debug**를 입력하여 로컬 디버그 서비스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e11ef-150">Back in the script editor, select Ctrl+Shift+P to open the command console, and then enter **Local Debug** to start your local debug service.</span></span>

![Data Lake Tools for Visual Studio Code 로컬 디버그 결과](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-debug-result.png)


## <a name="next-steps"></a><span data-ttu-id="e11ef-152">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e11ef-152">Next steps</span></span>
- <span data-ttu-id="e11ef-153">Azure Data Lake Tools for Visual Studio Code 사용에 대해서는 [Azure Data Lake Tools for Visual Studio Code 사용](data-lake-analytics-data-lake-tools-for-vscode.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e11ef-153">For using Azure Data Lake Tools for Visual Studio Code, see [Use Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span></span>
- <span data-ttu-id="e11ef-154">Data Lake Analytics 시작 정보는 [자습서: Azure Data Lake Analytics 시작](data-lake-analytics-get-started-portal.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e11ef-154">For getting started information on Data Lake Analytics, see [Tutorial: Get started with Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span></span>
- <span data-ttu-id="e11ef-155">Data Lake Tools for Visual Studio에 대한 자세한 내용은 [자습서: Data Lake Tools for Visual Studio를 사용하여 U-SQL 스크립트 개발](data-lake-analytics-data-lake-tools-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e11ef-155">For information about Data Lake Tools for Visual Studio, see [Tutorial: Develop U-SQL scripts by using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
- <span data-ttu-id="e11ef-156">어셈블리를 개발에 대한 정보는 [Azure Data Lake Analytics 작업에 U-SQL 어셈블리 개발](data-lake-analytics-u-sql-develop-assemblies.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e11ef-156">For the information on developing assemblies, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md).</span></span>

---
title: "Azure Automation을 사용하여 작업 트리거 | Microsoft Docs"
description: "Azure Automation을 사용하여 StorSimple 데이터 관리자 작업을 트리거하는 방법에 대해 알아보기(비공개 미리 보기)"
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 03/16/2017
ms.author: vidarmsft
ms.openlocfilehash: 9691408bcd80afb6eba534f26749b76dd3bfe315
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-automation-to-trigger-a-job-private-preview"></a><span data-ttu-id="e44e8-103">Azure Automation을 사용하여 작업 트리거(비공개 미리 보기)</span><span class="sxs-lookup"><span data-stu-id="e44e8-103">Use Azure Automation to trigger a job (Private Preview)</span></span>

<span data-ttu-id="e44e8-104">이 문서에서는 Azure Automation을 사용하여 StorSimple 데이터 관리자 작업을 트리거하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e44e8-104">This articles describes how to use Azure Automation to trigger a StorSimple Data Manager job.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e44e8-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="e44e8-105">Prerequisites</span></span>

<span data-ttu-id="e44e8-106">시작하기 전에 다음 항목이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44e8-106">Before you begin, ensure that you have:</span></span>

*   <span data-ttu-id="e44e8-107">Azure Powershell을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e44e8-107">Azure Powershell installed.</span></span> <span data-ttu-id="e44e8-108">[Azure Powershell을 다운로드합니다](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="e44e8-108">[Download Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
*   <span data-ttu-id="e44e8-109">데이터 변환 작업을 초기화하는 구성 설정 및 이러한 설정을 가져오는 지침도 여기에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="e44e8-109">Configuration settings to initialize the Data Transformation job (instructions to obtain these settings are included here).</span></span>
*   <span data-ttu-id="e44e8-110">리소스 그룹 내의 하이브리드 데이터 리소스에서 올바르게 구성된 작업 정의입니다.</span><span class="sxs-lookup"><span data-stu-id="e44e8-110">A job definition that has been correctly configured in a Hybrid Data Resource within a resource group.</span></span>
*   <span data-ttu-id="e44e8-111">`DataTransformationApp.zip` [zip](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/raw/master/Azure%20Automation%20For%20Data%20Manager/DataTransformationApp.zip) 파일을 github 리포지토리에서 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="e44e8-111">Download `DataTransformationApp.zip` [zip](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/raw/master/Azure%20Automation%20For%20Data%20Manager/DataTransformationApp.zip) file from the github repository.</span></span>
*   <span data-ttu-id="e44e8-112">`Get-ConfigurationParams.ps1` [스크립트](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Get-ConfigurationParams.ps1)를 github 리포지토리에서 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="e44e8-112">Download `Get-ConfigurationParams.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Get-ConfigurationParams.ps1) from the github repository.</span></span>
*   <span data-ttu-id="e44e8-113">`Trigger-DataTransformation-Job.ps1` [스크립트](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Trigger-DataTransformation-Job.ps1)를 github 리포지토리에서 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="e44e8-113">Download `Trigger-DataTransformation-Job.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Trigger-DataTransformation-Job.ps1) from the github repository.</span></span>

## <a name="step-by-step"></a><span data-ttu-id="e44e8-114">단계별 과정</span><span class="sxs-lookup"><span data-stu-id="e44e8-114">Step-by-step</span></span>

### <a name="get-azure-active-directory-permissions-for-the-automation-job-to-run-the-job-definition"></a><span data-ttu-id="e44e8-115">작업 정의 실행을 위해 자동화 작업에 대한 Azure Active Directory 사용 권한 가져오기</span><span class="sxs-lookup"><span data-stu-id="e44e8-115">Get Azure Active Directory permissions for the automation job to run the job definition</span></span>

1. <span data-ttu-id="e44e8-116">Active Directory에 대한 구성 매개 변수를 검색하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e44e8-116">To retrieve the configuration parameters for Active Directory, do the following steps:</span></span>

    1. <span data-ttu-id="e44e8-117">로컬 컴퓨터에서 Windows PowerShell을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e44e8-117">Open Windows PowerShell in your local machine.</span></span> <span data-ttu-id="e44e8-118">[Azure PowerShell](https://azure.microsoft.com/downloads/)이 설치되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e44e8-118">Ensure that [Azure PowerShell](https://azure.microsoft.com/downloads/) is installed.</span></span>
    1. <span data-ttu-id="e44e8-119">`Get-ConfigurationParams.ps1` 스크립트(위에서 다운로드한 폴더에 있음)를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e44e8-119">Run the `Get-ConfigurationParams.ps1` script (in the folder you downloaded above).</span></span> <span data-ttu-id="e44e8-120">PowerShell 창에 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e44e8-120">Type the following command in the PowerShell window:</span></span>

        ```
        .\Get-ConfigurationParams.ps1 -SubscriptionName "AzureSubscriptionName" -ActiveDirectoryKey "AnyRandomPassword" -AppName "ApplicationName"
         ```

        <span data-ttu-id="e44e8-121">ActiveDirectoryKey는 나중에 사용하는 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="e44e8-121">The ActiveDirectoryKey is a password that you use later.</span></span> <span data-ttu-id="e44e8-122">사용자가 선택한 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e44e8-122">Enter a password of your choice.</span></span> <span data-ttu-id="e44e8-123">AppName에는 아무 문자열이나 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44e8-123">AppName can be any string.</span></span>

2. <span data-ttu-id="e44e8-124">이 스크립트는 Automation Runbook을 트리거하는 동안 사용해야 하는 다음 값을 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="e44e8-124">This script outputs the following values that should be used while triggering the automation runbook.</span></span> <span data-ttu-id="e44e8-125">이러한 값을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="e44e8-125">Make a note of these values.</span></span>

    - <span data-ttu-id="e44e8-126">클라이언트 ID</span><span class="sxs-lookup"><span data-stu-id="e44e8-126">Client ID</span></span>
    - <span data-ttu-id="e44e8-127">테넌트 ID</span><span class="sxs-lookup"><span data-stu-id="e44e8-127">Tenant ID</span></span>
    - <span data-ttu-id="e44e8-128">Active Directory 키(위에서 입력한 것과 동일)</span><span class="sxs-lookup"><span data-stu-id="e44e8-128">Active Directory key (same as the one entered above)</span></span>
    - <span data-ttu-id="e44e8-129">구독 ID</span><span class="sxs-lookup"><span data-stu-id="e44e8-129">Subscription ID</span></span>

### <a name="set-up-the-automation-account"></a><span data-ttu-id="e44e8-130">Automation 계정 설정</span><span class="sxs-lookup"><span data-stu-id="e44e8-130">Set up the Automation Account</span></span>

1. <span data-ttu-id="e44e8-131">Azure에서 로그인하고 사용자의 Automation 계정을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e44e8-131">Log on to Azure and open your Automation account.</span></span>
2. <span data-ttu-id="e44e8-132">**자산** 타일을 클릭하여 자산 목록을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e44e8-132">Click **Assets** tile to open the list of assets.</span></span>
3. <span data-ttu-id="e44e8-133">**모듈** 타일을 클릭하여 모듈 목록을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e44e8-133">Click **Modules** tile to open the list of modules.</span></span>
4. <span data-ttu-id="e44e8-134">**+ 모듈 추가** 단추를 클릭하면 모듈 추가 블레이드가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="e44e8-134">Click **+ Add a module** button and the Add module blade is launched.</span></span>

    ![Automation 계정 설정](./media/storsimple-data-manager-job-using-automation/add-module1m.png)

5. <span data-ttu-id="e44e8-136">로컬 컴퓨터에서 `DataTransformationApp.zip` 파일을 클릭한 후, **확인**을 클릭하여 모듈을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e44e8-136">After you have selected the `DataTransformationApp.zip` file from your local computer, click **OK** to import the module.</span></span>

   <span data-ttu-id="e44e8-137">Azure Automation이 사용자 계정에 모듈을 가져오면 모듈에 대한 메타데이터를 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="e44e8-137">When Azure Automation imports a module to your account, it extracts metadata about the module.</span></span> <span data-ttu-id="e44e8-138">이 작업에는 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44e8-138">This operation may take a couple of minutes.</span></span>

   ![Automation 계정 설정](./media/storsimple-data-manager-job-using-automation/add-module2m.png)

   

6. <span data-ttu-id="e44e8-140">모듈이 배포되는 도중 및 완료 시점에 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e44e8-140">You receive a notification that the module is being deployed and another notification when the process is complete.</span></span>  <span data-ttu-id="e44e8-141">**모듈** 타일에서 상태를 확인할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44e8-141">You can also check the status in **Modules** tile.</span></span>

### <a name="to-import-the-runbook-that-triggers-the-job-definition"></a><span data-ttu-id="e44e8-142">작업 정의를 트리거하는 Runbook을 가져오려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e44e8-142">To import the runbook that triggers the job definition</span></span>

1. <span data-ttu-id="e44e8-143">Azure 포털에서 자동화 계정을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e44e8-143">In the Azure portal, open your Automation account.</span></span>
2. <span data-ttu-id="e44e8-144">**Runbook** 타일을 클릭하여 Runbook 목록을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e44e8-144">Click **Runbooks** tile to open the list of runbooks.</span></span>
3. <span data-ttu-id="e44e8-145">**+ Runbook 추가**를 클릭한 다음, **기존 Runbook 가져오기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e44e8-145">Click **+ Add a runbook** and then **Import an existing runbook**.</span></span>

   ![기존 Runbook 가져오기](./media/storsimple-data-manager-job-using-automation/import-a-runbook.png)

4. <span data-ttu-id="e44e8-147">**Runbook 파일**을 클릭하고 `Trigger-DataTransformation-Job.ps1`을 가져올 파일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e44e8-147">Click **Runbook file** and select the file to import `Trigger-DataTransformation-Job.ps1`.</span></span>
5. <span data-ttu-id="e44e8-148">**만들기**를 클릭하여 Runbook을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e44e8-148">Click **Create** to import the runbook.</span></span> <span data-ttu-id="e44e8-149">새 Runbook이 Automation 계정의 Runbook 목록에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e44e8-149">The new runbook appears in the list of runbooks for the Automation account.</span></span>
7. <span data-ttu-id="e44e8-150">**Trigger-DataTransformation-Job** Runbook을 클릭한 다음 **편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e44e8-150">Click **Trigger-DataTransformation-Job** runbook and then click **Edit**.</span></span>
8. <span data-ttu-id="e44e8-151">확인 메시지가 표시되면 **게시**, **예**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e44e8-151">Click **Publish** and then **Yes** when prompted for confirmation.</span></span>


### <a name="to-run-the-runbook"></a><span data-ttu-id="e44e8-152">Runbook을 실행하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e44e8-152">To run the runbook:</span></span>
1. <span data-ttu-id="e44e8-153">Azure 포털에서 자동화 계정을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e44e8-153">In the Azure portal, open your Automation account.</span></span>
2. <span data-ttu-id="e44e8-154">**Runbook** 타일을 클릭하여 Runbook 목록을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e44e8-154">Click the **Runbooks** tile to open the list of runbooks.</span></span>
3. <span data-ttu-id="e44e8-155">**Trigger-DataTransformation-Job**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e44e8-155">Click **Trigger-DataTransformation-Job**.</span></span>
4. <span data-ttu-id="e44e8-156">**시작**을 클릭하여 runbook을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e44e8-156">Click **Start** to start the runbook.</span></span>

   ![Runbook 시작](./media/storsimple-data-manager-job-using-automation/run-runbook1m.png)

5. <span data-ttu-id="e44e8-158">**Runbook 시작** 블레이드에서 모든 매개 변수를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e44e8-158">In the **Start runbook** blade, enter all the parameters.</span></span> <span data-ttu-id="e44e8-159">**확인**을 클릭하여 데이터 변환 작업을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="e44e8-159">Click **OK** to submit the Data Transformation job.</span></span>

   ![Runbook 시작](./media/storsimple-data-manager-job-using-automation/run-runbook2m.png)


## <a name="next-steps"></a><span data-ttu-id="e44e8-161">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e44e8-161">Next steps</span></span>

<span data-ttu-id="e44e8-162">[StorSimple 데이터 관리자 UI를 사용하여 데이터를 변환합니다](storsimple-data-manager-ui.md).</span><span class="sxs-lookup"><span data-stu-id="e44e8-162">[Use StorSimple Data Manager UI to transform your data](storsimple-data-manager-ui.md).</span></span>
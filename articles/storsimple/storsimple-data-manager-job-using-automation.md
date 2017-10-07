---
title: "Azure 자동화 tootrigger aaaUse 작업 | Microsoft Docs"
description: "자세한 내용은 방법 StorSimple 데이터 관리자 작업 (비공개 미리 보기)를 트리거할 기준이 toouse Azure 자동화"
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
ms.openlocfilehash: 0d9d6e5e6d52ed27ca759ed7e949b5f5dfd319c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-automation-tootrigger-a-job-private-preview"></a><span data-ttu-id="16b6a-103">Azure 자동화 tootrigger 작업 (비공개 미리 보기)를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="16b6a-103">Use Azure Automation tootrigger a job (Private Preview)</span></span>

<span data-ttu-id="16b6a-104">이 문서에 설명 방법을 toouse Azure 자동화 tootrigger StorSimple Data Manager 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="16b6a-104">This articles describes how toouse Azure Automation tootrigger a StorSimple Data Manager job.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="16b6a-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="16b6a-105">Prerequisites</span></span>

<span data-ttu-id="16b6a-106">시작하기 전에 다음 항목이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="16b6a-106">Before you begin, ensure that you have:</span></span>

*   <span data-ttu-id="16b6a-107">Azure Powershell을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="16b6a-107">Azure Powershell installed.</span></span> <span data-ttu-id="16b6a-108">[Azure Powershell을 다운로드합니다](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="16b6a-108">[Download Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
*   <span data-ttu-id="16b6a-109">구성 설정 tooinitialize hello 데이터 변환 작업 (지침 tooobtain 이러한 설정을 여기에 포함 됩니다).</span><span class="sxs-lookup"><span data-stu-id="16b6a-109">Configuration settings tooinitialize hello Data Transformation job (instructions tooobtain these settings are included here).</span></span>
*   <span data-ttu-id="16b6a-110">리소스 그룹 내의 하이브리드 데이터 리소스에서 올바르게 구성된 작업 정의입니다.</span><span class="sxs-lookup"><span data-stu-id="16b6a-110">A job definition that has been correctly configured in a Hybrid Data Resource within a resource group.</span></span>
*   <span data-ttu-id="16b6a-111">다운로드 `DataTransformationApp.zip` [zip](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/raw/master/Azure%20Automation%20For%20Data%20Manager/DataTransformationApp.zip) hello github 리포지토리에서 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="16b6a-111">Download `DataTransformationApp.zip` [zip](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/raw/master/Azure%20Automation%20For%20Data%20Manager/DataTransformationApp.zip) file from hello github repository.</span></span>
*   <span data-ttu-id="16b6a-112">다운로드 `Get-ConfigurationParams.ps1` [스크립트](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Get-ConfigurationParams.ps1) hello github 리포지토리에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="16b6a-112">Download `Get-ConfigurationParams.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Get-ConfigurationParams.ps1) from hello github repository.</span></span>
*   <span data-ttu-id="16b6a-113">다운로드 `Trigger-DataTransformation-Job.ps1` [스크립트](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Trigger-DataTransformation-Job.ps1) hello github 리포지토리에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="16b6a-113">Download `Trigger-DataTransformation-Job.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Trigger-DataTransformation-Job.ps1) from hello github repository.</span></span>

## <a name="step-by-step"></a><span data-ttu-id="16b6a-114">단계별 과정</span><span class="sxs-lookup"><span data-stu-id="16b6a-114">Step-by-step</span></span>

### <a name="get-azure-active-directory-permissions-for-hello-automation-job-toorun-hello-job-definition"></a><span data-ttu-id="16b6a-115">Hello 자동화 작업 toorun hello 작업 정의 대 한 Azure Active Directory 사용 권한 가져오기</span><span class="sxs-lookup"><span data-stu-id="16b6a-115">Get Azure Active Directory permissions for hello automation job toorun hello job definition</span></span>

1. <span data-ttu-id="16b6a-116">Active Directory에 대 한 tooretrieve hello 구성 매개 변수는 다음 단계 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="16b6a-116">tooretrieve hello configuration parameters for Active Directory, do hello following steps:</span></span>

    1. <span data-ttu-id="16b6a-117">로컬 컴퓨터에서 Windows PowerShell을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="16b6a-117">Open Windows PowerShell in your local machine.</span></span> <span data-ttu-id="16b6a-118">[Azure PowerShell](https://azure.microsoft.com/downloads/)이 설치되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="16b6a-118">Ensure that [Azure PowerShell](https://azure.microsoft.com/downloads/) is installed.</span></span>
    1. <span data-ttu-id="16b6a-119">Hello 실행 `Get-ConfigurationParams.ps1` hello 폴더에서 위의 다운로드 한 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="16b6a-119">Run hello `Get-ConfigurationParams.ps1` script (in hello folder you downloaded above).</span></span> <span data-ttu-id="16b6a-120">Hello 다음 hello PowerShell 창에서 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="16b6a-120">Type hello following command in hello PowerShell window:</span></span>

        ```
        .\Get-ConfigurationParams.ps1 -SubscriptionName "AzureSubscriptionName" -ActiveDirectoryKey "AnyRandomPassword" -AppName "ApplicationName"
         ```

        <span data-ttu-id="16b6a-121">hello ActiveDirectoryKey 나중에 사용할 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="16b6a-121">hello ActiveDirectoryKey is a password that you use later.</span></span> <span data-ttu-id="16b6a-122">사용자가 선택한 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="16b6a-122">Enter a password of your choice.</span></span> <span data-ttu-id="16b6a-123">AppName에는 아무 문자열이나 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b6a-123">AppName can be any string.</span></span>

2. <span data-ttu-id="16b6a-124">이 스크립트는 다음 hello 자동화 runbook을 트리거하는 동안 사용 해야 하는 값에는 hello를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="16b6a-124">This script outputs hello following values that should be used while triggering hello automation runbook.</span></span> <span data-ttu-id="16b6a-125">이러한 값을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="16b6a-125">Make a note of these values.</span></span>

    - <span data-ttu-id="16b6a-126">클라이언트 ID</span><span class="sxs-lookup"><span data-stu-id="16b6a-126">Client ID</span></span>
    - <span data-ttu-id="16b6a-127">테넌트 ID</span><span class="sxs-lookup"><span data-stu-id="16b6a-127">Tenant ID</span></span>
    - <span data-ttu-id="16b6a-128">Active Directory 키 (동일: hello 위에 입력 한 하나)</span><span class="sxs-lookup"><span data-stu-id="16b6a-128">Active Directory key (same as hello one entered above)</span></span>
    - <span data-ttu-id="16b6a-129">구독 ID</span><span class="sxs-lookup"><span data-stu-id="16b6a-129">Subscription ID</span></span>

### <a name="set-up-hello-automation-account"></a><span data-ttu-id="16b6a-130">자동화 계정 hello 설정</span><span class="sxs-lookup"><span data-stu-id="16b6a-130">Set up hello Automation Account</span></span>

1. <span data-ttu-id="16b6a-131">TooAzure 로그온 하 고 자동화 계정 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="16b6a-131">Log on tooAzure and open your Automation account.</span></span>
2. <span data-ttu-id="16b6a-132">클릭 **자산** 자산의 타일 tooopen hello 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="16b6a-132">Click **Assets** tile tooopen hello list of assets.</span></span>
3. <span data-ttu-id="16b6a-133">클릭 **모듈** 타일 tooopen hello 모듈 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="16b6a-133">Click **Modules** tile tooopen hello list of modules.</span></span>
4. <span data-ttu-id="16b6a-134">클릭 **모듈 추가 +** 단추와 hello 추가 모듈 블레이드 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="16b6a-134">Click **+ Add a module** button and hello Add module blade is launched.</span></span>

    ![Automation 계정 설정](./media/storsimple-data-manager-job-using-automation/add-module1m.png)

5. <span data-ttu-id="16b6a-136">Hello를 선택한 후 `DataTransformationApp.zip` 로컬 컴퓨터에서 파일을 클릭 하 여 **확인** tooimport hello 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="16b6a-136">After you have selected hello `DataTransformationApp.zip` file from your local computer, click **OK** tooimport hello module.</span></span>

   <span data-ttu-id="16b6a-137">Azure 자동화 모듈 tooyour 계정을 가져오면 hello 모듈에 대 한 메타 데이터를 추출 합니다.</span><span class="sxs-lookup"><span data-stu-id="16b6a-137">When Azure Automation imports a module tooyour account, it extracts metadata about hello module.</span></span> <span data-ttu-id="16b6a-138">이 작업에는 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b6a-138">This operation may take a couple of minutes.</span></span>

   ![Automation 계정 설정](./media/storsimple-data-manager-job-using-automation/add-module2m.png)

   

6. <span data-ttu-id="16b6a-140">알림이 해당 hello 모듈 배포 되 고 및 hello 프로세스가 완료 되 면 다른 알림입니다.</span><span class="sxs-lookup"><span data-stu-id="16b6a-140">You receive a notification that hello module is being deployed and another notification when hello process is complete.</span></span>  <span data-ttu-id="16b6a-141">Hello 상태를 확인할 수도 있습니다 **모듈** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="16b6a-141">You can also check hello status in **Modules** tile.</span></span>

### <a name="tooimport-hello-runbook-that-triggers-hello-job-definition"></a><span data-ttu-id="16b6a-142">hello 작업 정의 트리거하는 tooimport hello runbook</span><span class="sxs-lookup"><span data-stu-id="16b6a-142">tooimport hello runbook that triggers hello job definition</span></span>

1. <span data-ttu-id="16b6a-143">Hello Azure 포털에서에서 자동화 계정을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="16b6a-143">In hello Azure portal, open your Automation account.</span></span>
2. <span data-ttu-id="16b6a-144">클릭 **Runbook** runbook의 타일 tooopen hello 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="16b6a-144">Click **Runbooks** tile tooopen hello list of runbooks.</span></span>
3. <span data-ttu-id="16b6a-145">**+ Runbook 추가**를 클릭한 다음, **기존 Runbook 가져오기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="16b6a-145">Click **+ Add a runbook** and then **Import an existing runbook**.</span></span>

   ![기존 Runbook 가져오기](./media/storsimple-data-manager-job-using-automation/import-a-runbook.png)

4. <span data-ttu-id="16b6a-147">클릭 **Runbook 파일** 및 선택 hello 파일 tooimport `Trigger-DataTransformation-Job.ps1`합니다.</span><span class="sxs-lookup"><span data-stu-id="16b6a-147">Click **Runbook file** and select hello file tooimport `Trigger-DataTransformation-Job.ps1`.</span></span>
5. <span data-ttu-id="16b6a-148">클릭 **만들기** tooimport hello runbook입니다.</span><span class="sxs-lookup"><span data-stu-id="16b6a-148">Click **Create** tooimport hello runbook.</span></span> <span data-ttu-id="16b6a-149">새 runbook hello hello 자동화 계정에 대 한 runbook의 hello 목록에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="16b6a-149">hello new runbook appears in hello list of runbooks for hello Automation account.</span></span>
7. <span data-ttu-id="16b6a-150">**Trigger-DataTransformation-Job** Runbook을 클릭한 다음 **편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="16b6a-150">Click **Trigger-DataTransformation-Job** runbook and then click **Edit**.</span></span>
8. <span data-ttu-id="16b6a-151">확인 메시지가 표시되면 **게시**, **예**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="16b6a-151">Click **Publish** and then **Yes** when prompted for confirmation.</span></span>


### <a name="toorun-hello-runbook"></a><span data-ttu-id="16b6a-152">toorun hello runbook의 경우:</span><span class="sxs-lookup"><span data-stu-id="16b6a-152">toorun hello runbook:</span></span>
1. <span data-ttu-id="16b6a-153">Hello Azure 포털에서에서 자동화 계정을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="16b6a-153">In hello Azure portal, open your Automation account.</span></span>
2. <span data-ttu-id="16b6a-154">Hello 클릭 **Runbook** runbook의 타일 tooopen hello 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="16b6a-154">Click hello **Runbooks** tile tooopen hello list of runbooks.</span></span>
3. <span data-ttu-id="16b6a-155">**Trigger-DataTransformation-Job**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="16b6a-155">Click **Trigger-DataTransformation-Job**.</span></span>
4. <span data-ttu-id="16b6a-156">클릭 **시작** toostart hello runbook입니다.</span><span class="sxs-lookup"><span data-stu-id="16b6a-156">Click **Start** toostart hello runbook.</span></span>

   ![Runbook 시작](./media/storsimple-data-manager-job-using-automation/run-runbook1m.png)

5. <span data-ttu-id="16b6a-158">Hello에 **runbook을 시작** 블레이드에서 모든 hello 매개 변수를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="16b6a-158">In hello **Start runbook** blade, enter all hello parameters.</span></span> <span data-ttu-id="16b6a-159">클릭 **확인** toosubmit hello 데이터 변환 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="16b6a-159">Click **OK** toosubmit hello Data Transformation job.</span></span>

   ![Runbook 시작](./media/storsimple-data-manager-job-using-automation/run-runbook2m.png)


## <a name="next-steps"></a><span data-ttu-id="16b6a-161">다음 단계</span><span class="sxs-lookup"><span data-stu-id="16b6a-161">Next steps</span></span>

<span data-ttu-id="16b6a-162">[데이터 tootransform StorSimple 데이터 관리자 UI를 사용 하 여](storsimple-data-manager-ui.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="16b6a-162">[Use StorSimple Data Manager UI tootransform your data](storsimple-data-manager-ui.md).</span></span>

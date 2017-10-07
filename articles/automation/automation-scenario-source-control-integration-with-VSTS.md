---
title: "소스 제어 Visual Stuido Team Services와 Azure 자동화 aaaIntegrate | Microsoft Docs"
description: "Azure Automation 계정 및 Visual Stuido Team Services 소스 제어와의 통합 설정을 안내하는 시나리오입니다."
services: automation
documentationcenter: 
author: eamono
manager: 
editor: 
keywords: "azure powershell, VSTS, 소스 제어, Automation"
ms.assetid: a43b395a-e740-41a3-ae62-40eac9d0ec00
ms.service: automation
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/24/2017
ms.openlocfilehash: 8f6faa596a5ad1f8b72e820ca320b3e103d83579
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---automation-source-control-integration-with-visual-studio-team-services"></a><span data-ttu-id="b3f2e-104">Azure Automation 시나리오 - Visual Studio Team Services와 Automation 소스 제어 통합</span><span class="sxs-lookup"><span data-stu-id="b3f2e-104">Azure Automation scenario - Automation source control integration with Visual Studio Team Services</span></span>

<span data-ttu-id="b3f2e-105">이 시나리오에서 toomanage Azure 자동화 runbook 또는 소스 제어에서 DSC 구성을 사용 하는 Visual Studio Team Services 프로젝트를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3f2e-105">In this scenario, you have a Visual Studio Team Services project that you are using toomanage Azure Automation runbooks or DSC configurations under source control.</span></span>
<span data-ttu-id="b3f2e-106">이 문서에서는 설명 방법을 toointegrate VSTS 각 체크 인에 대 한 연속 통합을 지에서 발생 하므로 Azure 자동화 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="b3f2e-106">This article describes how toointegrate VSTS with your Azure Automation environment so that continuous integration happens for each check-in.</span></span>

## <a name="getting-hello-scenario"></a><span data-ttu-id="b3f2e-107">Hello 시나리오를 가져오기</span><span class="sxs-lookup"><span data-stu-id="b3f2e-107">Getting hello scenario</span></span>

<span data-ttu-id="b3f2e-108">이 시나리오 hello에서 직접 가져올 수 있는 두 개의 PowerShell runbook 이루어져 [Runbook 갤러리](automation-runbook-gallery.md) hello Azure 포털 또는 hello에서 다운로드 [PowerShell 갤러리](https://www.powershellgallery.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f2e-108">This scenario consists of two PowerShell runbooks that you can import directly from hello [Runbook Gallery](automation-runbook-gallery.md) in hello Azure portal or download from hello [PowerShell Gallery](https://www.powershellgallery.com).</span></span>

### <a name="runbooks"></a><span data-ttu-id="b3f2e-109">Runbook</span><span class="sxs-lookup"><span data-stu-id="b3f2e-109">Runbooks</span></span>

<span data-ttu-id="b3f2e-110">Runbook</span><span class="sxs-lookup"><span data-stu-id="b3f2e-110">Runbook</span></span> | <span data-ttu-id="b3f2e-111">설명</span><span class="sxs-lookup"><span data-stu-id="b3f2e-111">Description</span></span>| 
--------|------------|
<span data-ttu-id="b3f2e-112">Sync-VSTS</span><span class="sxs-lookup"><span data-stu-id="b3f2e-112">Sync-VSTS</span></span> | <span data-ttu-id="b3f2e-113">체크 인 작업이 완료되면 VSTS 소스 제어에서 runbook 또는 구성을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b3f2e-113">Import runbooks or configurations from VSTS source control when a check-in is done.</span></span> <span data-ttu-id="b3f2e-114">수동으로 실행 가져오기 되며 모든 runbook 또는 hello 자동화 계정에 구성을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f2e-114">If run manually, it will import and publish all runbooks or configurations into hello Automation account.</span></span>| 
<span data-ttu-id="b3f2e-115">Sync-VSTSGit</span><span class="sxs-lookup"><span data-stu-id="b3f2e-115">Sync-VSTSGit</span></span> | <span data-ttu-id="b3f2e-116">체크 인 작업이 완료되면 Git 소스 제어의 VSTS에서 runbook 또는 구성을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b3f2e-116">Import runbooks or configurations from VSTS under Git source control when a check-in is done.</span></span> <span data-ttu-id="b3f2e-117">수동으로 실행 가져오기 되며 모든 runbook 또는 hello 자동화 계정에 구성을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f2e-117">If run manually, it will import and publish all runbooks or configurations into hello Automation account.</span></span>|

### <a name="variables"></a><span data-ttu-id="b3f2e-118">variables</span><span class="sxs-lookup"><span data-stu-id="b3f2e-118">Variables</span></span>

<span data-ttu-id="b3f2e-119">변수</span><span class="sxs-lookup"><span data-stu-id="b3f2e-119">Variable</span></span> | <span data-ttu-id="b3f2e-120">설명</span><span class="sxs-lookup"><span data-stu-id="b3f2e-120">Description</span></span>|
-----------|------------|
<span data-ttu-id="b3f2e-121">VSToken</span><span class="sxs-lookup"><span data-stu-id="b3f2e-121">VSToken</span></span> | <span data-ttu-id="b3f2e-122">만들려는 hello VSTS 개인용 액세스 토큰을 포함 하는 변수 자산을 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f2e-122">Secure variable asset you will create that contains hello VSTS personal access token.</span></span> <span data-ttu-id="b3f2e-123">VSTS 개인용 액세스 하는 toocreate 방법을 학습할 수 있는 hello에 토큰 [VSTS 인증 페이지](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f2e-123">You can learn how toocreate a VSTS personal access token on hello [VSTS authentication page](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/overview).</span></span> 
## <a name="installing-and-configuring-this-scenario"></a><span data-ttu-id="b3f2e-124">이 시나리오 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="b3f2e-124">Installing and configuring this scenario</span></span>

<span data-ttu-id="b3f2e-125">만들기는 [개인용 액세스 토큰](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/overview) 저마다 자동화 계정으로 toosync hello runbook 또는 구성을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f2e-125">Create a [personal access token](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/overview) in VSTS that you will use toosync hello runbooks or configurations into your automation account.</span></span>

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPersonalToken.png) 

<span data-ttu-id="b3f2e-126">만들기는 [secure 변수의](automation-variables.md) 프로그램 자동화 계정 toohold hello 개인용 액세스 토큰 hello runbook tooVSTS 및 동기화 hello runbook 또는 구성이 hello 자동화 계정에 인증할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f2e-126">Create a [secure variable](automation-variables.md) in your automation account toohold hello personal access token so that hello runbook can authenticate tooVSTS and sync hello runbooks or configurations into hello Automation account.</span></span> <span data-ttu-id="b3f2e-127">이름을 VSToken으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3f2e-127">You can name this VSToken.</span></span> 

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSTokenVariable.png)

<span data-ttu-id="b3f2e-128">Runbook 또는 hello 자동화 계정으로 구성 동기화 hello runbook을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b3f2e-128">Import hello runbook that will sync your runbooks or configurations into hello automation account.</span></span> <span data-ttu-id="b3f2e-129">Hello를 사용할 수 있습니다 [VSTS 샘플 runbook](https://www.powershellgallery.com/packages/Sync-VSTS/1.0/DisplayScript) 또는 hello [Git 샘플 runbook과 VSTS] (https://www.powershellgallery.com/packages/Sync-VSTSGit/1.0/DisplayScript) VSTS 사용 여부에 따라 PowerShellGallery.com hello에서 원본 제어 또는 git VSTS tooyour 자동화 계정을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f2e-129">You can use hello [VSTS sample runbook](https://www.powershellgallery.com/packages/Sync-VSTS/1.0/DisplayScript) or hello [VSTS with Git sample runbook] (https://www.powershellgallery.com/packages/Sync-VSTSGit/1.0/DisplayScript) from hello PowerShellGallery.com depending on if you use VSTS source control or VSTS with Git and deploy tooyour automation account.</span></span>

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPowerShellGallery.png)

<span data-ttu-id="b3f2e-130">이제 webhook을 만들 수 있도록 이 runbook을 [게시](automation-creating-importing-runbook.md#publishing-a-runbook)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3f2e-130">You can now [publish](automation-creating-importing-runbook.md#publishing-a-runbook) this runbook so you can create a webhook.</span></span> 
![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPublishRunbook.png)

<span data-ttu-id="b3f2e-131">만들기는 [webhook](automation-webhooks.md) 이 동기화 VSTS runbook 및 아래와 같이 hello 매개 변수를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f2e-131">Create a [webhook](automation-webhooks.md) for this Sync-VSTS runbook and fill in hello parameters as shown below.</span></span> <span data-ttu-id="b3f2e-132">VSTS에서 서비스 후크에 대 한 필요 하므로 hello webhook url을 복사 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f2e-132">Make sure you copy hello webhook url as you will need it for a service hook in VSTS.</span></span> <span data-ttu-id="b3f2e-133">hello VSAccessTokenVariableName hello 이름 (VSToken)을 이전 toohold hello 개인용 액세스 토큰을 만든 hello 보안 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="b3f2e-133">hello VSAccessTokenVariableName is hello name (VSToken) of hello secure variable that you created earlier toohold hello personal access token.</span></span> 

<span data-ttu-id="b3f2e-134">VSTS (동기화 VSTS.ps1)와 통합 하면 매개 변수 뒤 hello를 소요 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3f2e-134">Integrating with VSTS (Sync-VSTS.ps1) will take hello following parameters.</span></span>
### <a name="sync-vsts-parameters"></a><span data-ttu-id="b3f2e-135">Sync-VSTS 매개 변수</span><span class="sxs-lookup"><span data-stu-id="b3f2e-135">Sync-VSTS Parameters</span></span>

<span data-ttu-id="b3f2e-136">매개 변수</span><span class="sxs-lookup"><span data-stu-id="b3f2e-136">Parameter</span></span> | <span data-ttu-id="b3f2e-137">설명</span><span class="sxs-lookup"><span data-stu-id="b3f2e-137">Description</span></span>| 
--------|------------|
<span data-ttu-id="b3f2e-138">WebhookData</span><span class="sxs-lookup"><span data-stu-id="b3f2e-138">WebhookData</span></span> | <span data-ttu-id="b3f2e-139">Hello VSTS 서비스 후크에서 보내는 hello 체크 인 정보를 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3f2e-139">This will contain hello checkin information sent from hello VSTS service hook.</span></span> <span data-ttu-id="b3f2e-140">이 매개 변수는 비워 두어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f2e-140">You should leave this parameter blank.</span></span>| 
<span data-ttu-id="b3f2e-141">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="b3f2e-141">ResourceGroup</span></span> | <span data-ttu-id="b3f2e-142">Hello 자동화 계정에 있는 hello 리소스 그룹의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b3f2e-142">This is hello name of hello resource group that hello automation account is in.</span></span>|
<span data-ttu-id="b3f2e-143">AutomationAccountName</span><span class="sxs-lookup"><span data-stu-id="b3f2e-143">AutomationAccountName</span></span> | <span data-ttu-id="b3f2e-144">hello hello 자동화 계정의 이름입니다 VSTS와 동기화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3f2e-144">hello name of hello automation account that will sync with VSTS.</span></span>|
<span data-ttu-id="b3f2e-145">VSFolder</span><span class="sxs-lookup"><span data-stu-id="b3f2e-145">VSFolder</span></span> | <span data-ttu-id="b3f2e-146">Hello runbook 및 구성이 있는 VSTS에서 hello 폴더의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b3f2e-146">The name of hello folder in VSTS where hello runbooks and configurations exist.</span></span>|
<span data-ttu-id="b3f2e-147">VSAccount</span><span class="sxs-lookup"><span data-stu-id="b3f2e-147">VSAccount</span></span> | <span data-ttu-id="b3f2e-148">Visual Studio Team Services 계정 hello의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b3f2e-148">hello name of hello Visual Studio Team Services account.</span></span>| 
<span data-ttu-id="b3f2e-149">VSAccessTokenVariableName</span><span class="sxs-lookup"><span data-stu-id="b3f2e-149">VSAccessTokenVariableName</span></span> | <span data-ttu-id="b3f2e-150">hello VSTS 개인용 액세스 토큰을 보유 하는 hello secure 변수의 (VSToken)의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b3f2e-150">hello name of hello secure variable (VSToken) that holds hello VSTS personal access token.</span></span>| 


![](media/automation-scenario-source-control-integration-with-VSTS/VSTSWebhook.png)

<span data-ttu-id="b3f2e-151">VSTS (동기화 VSTSGit.ps1) GIT와 함께 사용 하는 경우 매개 변수 뒤 hello를 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="b3f2e-151">If you are using VSTS with GIT (Sync-VSTSGit.ps1) it will take hello following parameters.</span></span>

<span data-ttu-id="b3f2e-152">매개 변수</span><span class="sxs-lookup"><span data-stu-id="b3f2e-152">Parameter</span></span> | <span data-ttu-id="b3f2e-153">설명</span><span class="sxs-lookup"><span data-stu-id="b3f2e-153">Description</span></span>|
--------|------------|
<span data-ttu-id="b3f2e-154">WebhookData</span><span class="sxs-lookup"><span data-stu-id="b3f2e-154">WebhookData</span></span> | <span data-ttu-id="b3f2e-155">Hello VSTS 서비스 후크에서 보내는 hello 체크 인 정보를 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3f2e-155">This will contain hello checkin information sent from hello VSTS service hook.</span></span> <span data-ttu-id="b3f2e-156">이 매개 변수는 비워 두어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f2e-156">You should leave this parameter blank.</span></span>| <span data-ttu-id="b3f2e-157">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="b3f2e-157">ResourceGroup</span></span> | <span data-ttu-id="b3f2e-158">이 hello는 hello 자동화 계정에 있는 hello 리소스 그룹의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b3f2e-158">This hello name of hello resource group that hello automation account is in.</span></span>|
<span data-ttu-id="b3f2e-159">AutomationAccountName</span><span class="sxs-lookup"><span data-stu-id="b3f2e-159">AutomationAccountName</span></span> | <span data-ttu-id="b3f2e-160">hello hello 자동화 계정의 이름입니다 VSTS와 동기화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3f2e-160">hello name of hello automation account that will sync with VSTS.</span></span>|
<span data-ttu-id="b3f2e-161">VSAccount</span><span class="sxs-lookup"><span data-stu-id="b3f2e-161">VSAccount</span></span> | <span data-ttu-id="b3f2e-162">Visual Studio Team Services 계정 hello의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b3f2e-162">hello name of hello Visual Studio Team Services account.</span></span>|
<span data-ttu-id="b3f2e-163">VSProject</span><span class="sxs-lookup"><span data-stu-id="b3f2e-163">VSProject</span></span> | <span data-ttu-id="b3f2e-164">hello runbook 및 구성이 있는 VSTS에서 hello 프로젝트의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b3f2e-164">hello name of hello project in VSTS where hello runbooks and configurations exist.</span></span>|
<span data-ttu-id="b3f2e-165">GitRepo</span><span class="sxs-lookup"><span data-stu-id="b3f2e-165">GitRepo</span></span> | <span data-ttu-id="b3f2e-166">hello Git 리포지토리의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b3f2e-166">hello name of hello Git repository.</span></span>|
<span data-ttu-id="b3f2e-167">GitBranch</span><span class="sxs-lookup"><span data-stu-id="b3f2e-167">GitBranch</span></span> | <span data-ttu-id="b3f2e-168">hello 이름 hello VSTS Git 리포지토리의 분기입니다.</span><span class="sxs-lookup"><span data-stu-id="b3f2e-168">hello name of hello branch in VSTS Git repository.</span></span>|
<span data-ttu-id="b3f2e-169">폴더</span><span class="sxs-lookup"><span data-stu-id="b3f2e-169">Folder</span></span> | <span data-ttu-id="b3f2e-170">VSTS Git 분기에서 hello 폴더의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b3f2e-170">hello name of hello folder in VSTS Git branch.</span></span>|
<span data-ttu-id="b3f2e-171">VSAccessTokenVariableName</span><span class="sxs-lookup"><span data-stu-id="b3f2e-171">VSAccessTokenVariableName</span></span> | <span data-ttu-id="b3f2e-172">hello VSTS 개인용 액세스 토큰을 보유 하는 hello secure 변수의 (VSToken)의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b3f2e-172">hello name of hello secure variable (VSToken) that holds hello VSTS personal access token.</span></span>|

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSGitWebhook.png)

<span data-ttu-id="b3f2e-173">VSTS에서 코드 체크 인에이 webhook을 트리거하는 체크 인 toohello 폴더에 대 한 서비스 후크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b3f2e-173">Create a service hook in VSTS for check-ins toohello folder that triggers this webhook on code check-in.</span></span> <span data-ttu-id="b3f2e-174">새 구독을 만들 때와 hello 서비스 toointegrate로 Web Hook를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f2e-174">Select Web Hooks as hello service toointegrate with when you create a new subscription.</span></span> <span data-ttu-id="b3f2e-175">[VSTS 서비스 후크 설명서](https://www.visualstudio.com/en-us/docs/marketplace/integrate/service-hooks/get-started)에서 서비스 후크에 대해 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3f2e-175">You can learn more about service hooks on [VSTS Service Hooks documentation](https://www.visualstudio.com/en-us/docs/marketplace/integrate/service-hooks/get-started).</span></span>
![](media/automation-scenario-source-control-integration-with-VSTS/VSTSServiceHook.png)

<span data-ttu-id="b3f2e-176">이제 수 toodo runbook 및 VSTS 구성을의 체크 인 될 하 고 자동으로 이러한 사항이 동기화 해야 자동화 계정으로 했습니다.</span><span class="sxs-lookup"><span data-stu-id="b3f2e-176">You should now be able toodo all check-ins of your runbooks and configurations into VSTS and have these automatically sync’d into your automation account.</span></span>

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSSyncRunbookOutput.png)

<span data-ttu-id="b3f2e-177">이 runbook을 VSTS에서 트리거된 하지 않고 수동으로 실행 하는 경우 hello webhookdata 매개 변수를 비워 둘 수 있습니다 및 지정 된 hello VSTS 폴더에서 전체 동기화를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f2e-177">If you run this runbook manually without being triggered by VSTS, you can leave hello webhookdata parameter empty and it will do a full sync from hello VSTS folder specified.</span></span>

<span data-ttu-id="b3f2e-178">VSTS에서 hello 서비스 후크 제거 toouninstall hello 시나리오를 원한다 면 hello runbook 및 hello VSToken 변수를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f2e-178">If you wish toouninstall hello scenario, remove hello service hook from VSTS, delete hello runbook, and hello VSToken variable.</span></span>

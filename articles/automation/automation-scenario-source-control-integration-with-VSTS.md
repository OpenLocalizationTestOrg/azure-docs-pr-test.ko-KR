---
title: "Visual Studio Team Services 소스 제어에 Azure Automation 통합 | Microsoft Docs"
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
ms.openlocfilehash: 01f9c01c9e04e02dbb548b68cf99684ba6ddd57e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-scenario---automation-source-control-integration-with-visual-studio-team-services"></a><span data-ttu-id="a6e47-104">Azure Automation 시나리오 - Visual Studio Team Services와 Automation 소스 제어 통합</span><span class="sxs-lookup"><span data-stu-id="a6e47-104">Azure Automation scenario - Automation source control integration with Visual Studio Team Services</span></span>

<span data-ttu-id="a6e47-105">이 시나리오에서는 소스 제어에서 Azure Automation 또는 DSC 구성을 관리하는 데 Visual Studio Team Services 프로젝트를 사용하고 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e47-105">In this scenario, you have a Visual Studio Team Services project that you are using to manage Azure Automation runbooks or DSC configurations under source control.</span></span>
<span data-ttu-id="a6e47-106">이 문서에서는 각 체크 인에 대해 연속 통합이 발생할 수 있도록 Azure Automation 환경에 VSTS를 통합하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e47-106">This article describes how to integrate VSTS with your Azure Automation environment so that continuous integration happens for each check-in.</span></span>

## <a name="getting-the-scenario"></a><span data-ttu-id="a6e47-107">시나리오 가져오기</span><span class="sxs-lookup"><span data-stu-id="a6e47-107">Getting the scenario</span></span>

<span data-ttu-id="a6e47-108">이 시나리오는 Azure 포털의 [Runbook 갤러리](automation-runbook-gallery.md)에서 직접 가져오거나 [PowerShell 갤러리](https://www.powershellgallery.com)에서 다운로드할 수 있는 2개의 PowerShell runbook으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6e47-108">This scenario consists of two PowerShell runbooks that you can import directly from the [Runbook Gallery](automation-runbook-gallery.md) in the Azure portal or download from the [PowerShell Gallery](https://www.powershellgallery.com).</span></span>

### <a name="runbooks"></a><span data-ttu-id="a6e47-109">Runbook</span><span class="sxs-lookup"><span data-stu-id="a6e47-109">Runbooks</span></span>

<span data-ttu-id="a6e47-110">Runbook</span><span class="sxs-lookup"><span data-stu-id="a6e47-110">Runbook</span></span> | <span data-ttu-id="a6e47-111">설명</span><span class="sxs-lookup"><span data-stu-id="a6e47-111">Description</span></span>| 
--------|------------|
<span data-ttu-id="a6e47-112">Sync-VSTS</span><span class="sxs-lookup"><span data-stu-id="a6e47-112">Sync-VSTS</span></span> | <span data-ttu-id="a6e47-113">체크 인 작업이 완료되면 VSTS 소스 제어에서 runbook 또는 구성을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a6e47-113">Import runbooks or configurations from VSTS source control when a check-in is done.</span></span> <span data-ttu-id="a6e47-114">수동으로 실행하는 경우 모든 runbook 또는 구성을 Automation 계정으로 가져와 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e47-114">If run manually, it will import and publish all runbooks or configurations into the Automation account.</span></span>| 
<span data-ttu-id="a6e47-115">Sync-VSTSGit</span><span class="sxs-lookup"><span data-stu-id="a6e47-115">Sync-VSTSGit</span></span> | <span data-ttu-id="a6e47-116">체크 인 작업이 완료되면 Git 소스 제어의 VSTS에서 runbook 또는 구성을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a6e47-116">Import runbooks or configurations from VSTS under Git source control when a check-in is done.</span></span> <span data-ttu-id="a6e47-117">수동으로 실행하는 경우 모든 runbook 또는 구성을 Automation 계정으로 가져와 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e47-117">If run manually, it will import and publish all runbooks or configurations into the Automation account.</span></span>|

### <a name="variables"></a><span data-ttu-id="a6e47-118">변수</span><span class="sxs-lookup"><span data-stu-id="a6e47-118">Variables</span></span>

<span data-ttu-id="a6e47-119">변수</span><span class="sxs-lookup"><span data-stu-id="a6e47-119">Variable</span></span> | <span data-ttu-id="a6e47-120">설명</span><span class="sxs-lookup"><span data-stu-id="a6e47-120">Description</span></span>|
-----------|------------|
<span data-ttu-id="a6e47-121">VSToken</span><span class="sxs-lookup"><span data-stu-id="a6e47-121">VSToken</span></span> | <span data-ttu-id="a6e47-122">VSTS 개인 액세스 토큰이 포함된 변수 자산을 만들어 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e47-122">Secure variable asset you will create that contains the VSTS personal access token.</span></span> <span data-ttu-id="a6e47-123">[VSTS 인증 페이지](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/overview)에서 VSTS 개인 액세스 토큰을 만드는 방법을 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6e47-123">You can learn how to create a VSTS personal access token on the [VSTS authentication page](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/overview).</span></span> 
## <a name="installing-and-configuring-this-scenario"></a><span data-ttu-id="a6e47-124">이 시나리오 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="a6e47-124">Installing and configuring this scenario</span></span>

<span data-ttu-id="a6e47-125">runbook 또는 구성을 Automation 계정에 동기화하는 데 사용할 [개인 액세스 토큰](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/overview)을 VSTS에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a6e47-125">Create a [personal access token](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/overview) in VSTS that you will use to sync the runbooks or configurations into your automation account.</span></span>

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPersonalToken.png) 

<span data-ttu-id="a6e47-126">VSTS에서 runbook을 인증하고 runbook 및 구성을 Automation 계정에 동기화할 수 있도록 Automation 계정에 개인 액세스 토큰을 저장할 [보안 변수](automation-variables.md)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a6e47-126">Create a [secure variable](automation-variables.md) in your automation account to hold the personal access token so that the runbook can authenticate to VSTS and sync the runbooks or configurations into the Automation account.</span></span> <span data-ttu-id="a6e47-127">이름을 VSToken으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6e47-127">You can name this VSToken.</span></span> 

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSTokenVariable.png)

<span data-ttu-id="a6e47-128">runbook 또는 구성을 Automation 계정에 동기화하는 runbook을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a6e47-128">Import the runbook that will sync your runbooks or configurations into the automation account.</span></span> <span data-ttu-id="a6e47-129">VSTS 소스 제어를 사용하는지 또는 Git이 있는 VSTS를 사용하여 Automation 계정에 배포하는지에 따라 [VSTS 샘플 runbook](https://www.powershellgallery.com/packages/Sync-VSTS/1.0/DisplayScript) 또는 PowerShellGallery.com(https://www.powershellgallery.com/packages/Sync-VSTSGit/1.0/DisplayScript)의 [Git이 있는 VSTS 샘플 runbook]을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6e47-129">You can use the [VSTS sample runbook](https://www.powershellgallery.com/packages/Sync-VSTS/1.0/DisplayScript) or the [VSTS with Git sample runbook] (https://www.powershellgallery.com/packages/Sync-VSTSGit/1.0/DisplayScript) from the PowerShellGallery.com depending on if you use VSTS source control or VSTS with Git and deploy to your automation account.</span></span>

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPowerShellGallery.png)

<span data-ttu-id="a6e47-130">이제 webhook을 만들 수 있도록 이 runbook을 [게시](automation-creating-importing-runbook.md#publishing-a-runbook)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6e47-130">You can now [publish](automation-creating-importing-runbook.md#publishing-a-runbook) this runbook so you can create a webhook.</span></span> 
![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPublishRunbook.png)

<span data-ttu-id="a6e47-131">이 Sync-VSTS runbook에 대해 [webhook](automation-webhooks.md)을 만들고 아래와 같이 매개 변수를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e47-131">Create a [webhook](automation-webhooks.md) for this Sync-VSTS runbook and fill in the parameters as shown below.</span></span> <span data-ttu-id="a6e47-132">VSTS의 서비스 후크에 필요하므로 webhook URL을 복사해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e47-132">Make sure you copy the webhook url as you will need it for a service hook in VSTS.</span></span> <span data-ttu-id="a6e47-133">VSAccessTokenVariableName은 개인 액세스 토큰을 저장하기 위해 앞에서 만든 보안 변수의 이름(VSToken)입니다.</span><span class="sxs-lookup"><span data-stu-id="a6e47-133">The VSAccessTokenVariableName is the name (VSToken) of the secure variable that you created earlier to hold the personal access token.</span></span> 

<span data-ttu-id="a6e47-134">VSTS(Sync-VSTS.ps1)와 통합하면 다음과 같은 매개 변수가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6e47-134">Integrating with VSTS (Sync-VSTS.ps1) will take the following parameters.</span></span>
### <a name="sync-vsts-parameters"></a><span data-ttu-id="a6e47-135">Sync-VSTS 매개 변수</span><span class="sxs-lookup"><span data-stu-id="a6e47-135">Sync-VSTS Parameters</span></span>

<span data-ttu-id="a6e47-136">매개 변수</span><span class="sxs-lookup"><span data-stu-id="a6e47-136">Parameter</span></span> | <span data-ttu-id="a6e47-137">설명</span><span class="sxs-lookup"><span data-stu-id="a6e47-137">Description</span></span>| 
--------|------------|
<span data-ttu-id="a6e47-138">WebhookData</span><span class="sxs-lookup"><span data-stu-id="a6e47-138">WebhookData</span></span> | <span data-ttu-id="a6e47-139">VSTS 서비스 후크에서 전송되는 체크 인 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6e47-139">This will contain the checkin information sent from the VSTS service hook.</span></span> <span data-ttu-id="a6e47-140">이 매개 변수는 비워 두어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e47-140">You should leave this parameter blank.</span></span>| 
<span data-ttu-id="a6e47-141">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="a6e47-141">ResourceGroup</span></span> | <span data-ttu-id="a6e47-142">Automation 계정이 있는 리소스 그룹의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a6e47-142">This is the name of the resource group that the automation account is in.</span></span>|
<span data-ttu-id="a6e47-143">AutomationAccountName</span><span class="sxs-lookup"><span data-stu-id="a6e47-143">AutomationAccountName</span></span> | <span data-ttu-id="a6e47-144">VSTS와 동기화될 Automation 계정의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a6e47-144">The name of the automation account that will sync with VSTS.</span></span>|
<span data-ttu-id="a6e47-145">VSFolder</span><span class="sxs-lookup"><span data-stu-id="a6e47-145">VSFolder</span></span> | <span data-ttu-id="a6e47-146">runbook 및 구성이 있는 VSTS의 폴더 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a6e47-146">The name of the folder in VSTS where the runbooks and configurations exist.</span></span>|
<span data-ttu-id="a6e47-147">VSAccount</span><span class="sxs-lookup"><span data-stu-id="a6e47-147">VSAccount</span></span> | <span data-ttu-id="a6e47-148">Visual Studio Team Services 계정의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a6e47-148">The name of the Visual Studio Team Services account.</span></span>| 
<span data-ttu-id="a6e47-149">VSAccessTokenVariableName</span><span class="sxs-lookup"><span data-stu-id="a6e47-149">VSAccessTokenVariableName</span></span> | <span data-ttu-id="a6e47-150">VSTS 개인 액세스 토큰을 보유하는 보안 변수(VSToken)의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a6e47-150">The name of the secure variable (VSToken) that holds the VSTS personal access token.</span></span>| 


![](media/automation-scenario-source-control-integration-with-VSTS/VSTSWebhook.png)

<span data-ttu-id="a6e47-151">GIT이 있는 VSTS(Sync-VSTSGit.ps1)를 사용하는 경우 다음 매개 변수가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6e47-151">If you are using VSTS with GIT (Sync-VSTSGit.ps1) it will take the following parameters.</span></span>

<span data-ttu-id="a6e47-152">매개 변수</span><span class="sxs-lookup"><span data-stu-id="a6e47-152">Parameter</span></span> | <span data-ttu-id="a6e47-153">설명</span><span class="sxs-lookup"><span data-stu-id="a6e47-153">Description</span></span>|
--------|------------|
<span data-ttu-id="a6e47-154">WebhookData</span><span class="sxs-lookup"><span data-stu-id="a6e47-154">WebhookData</span></span> | <span data-ttu-id="a6e47-155">VSTS 서비스 후크에서 전송되는 체크 인 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6e47-155">This will contain the checkin information sent from the VSTS service hook.</span></span> <span data-ttu-id="a6e47-156">이 매개 변수는 비워 두어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e47-156">You should leave this parameter blank.</span></span>| <span data-ttu-id="a6e47-157">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="a6e47-157">ResourceGroup</span></span> | <span data-ttu-id="a6e47-158">Automation 계정이 있는 리소스 그룹의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a6e47-158">This the name of the resource group that the automation account is in.</span></span>|
<span data-ttu-id="a6e47-159">AutomationAccountName</span><span class="sxs-lookup"><span data-stu-id="a6e47-159">AutomationAccountName</span></span> | <span data-ttu-id="a6e47-160">VSTS와 동기화될 Automation 계정의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a6e47-160">The name of the automation account that will sync with VSTS.</span></span>|
<span data-ttu-id="a6e47-161">VSAccount</span><span class="sxs-lookup"><span data-stu-id="a6e47-161">VSAccount</span></span> | <span data-ttu-id="a6e47-162">Visual Studio Team Services 계정의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a6e47-162">The name of the Visual Studio Team Services account.</span></span>|
<span data-ttu-id="a6e47-163">VSProject</span><span class="sxs-lookup"><span data-stu-id="a6e47-163">VSProject</span></span> | <span data-ttu-id="a6e47-164">runbook 및 구성이 있는 VSTS의 프로젝트 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a6e47-164">The name of the project in VSTS where the runbooks and configurations exist.</span></span>|
<span data-ttu-id="a6e47-165">GitRepo</span><span class="sxs-lookup"><span data-stu-id="a6e47-165">GitRepo</span></span> | <span data-ttu-id="a6e47-166">Git 리포지토리의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a6e47-166">The name of the Git repository.</span></span>|
<span data-ttu-id="a6e47-167">GitBranch</span><span class="sxs-lookup"><span data-stu-id="a6e47-167">GitBranch</span></span> | <span data-ttu-id="a6e47-168">VSTS Git 리포지토리의 분기 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a6e47-168">The name of the branch in VSTS Git repository.</span></span>|
<span data-ttu-id="a6e47-169">폴더</span><span class="sxs-lookup"><span data-stu-id="a6e47-169">Folder</span></span> | <span data-ttu-id="a6e47-170">VSTS Git 분기에 있는 폴더의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a6e47-170">The name of the folder in VSTS Git branch.</span></span>|
<span data-ttu-id="a6e47-171">VSAccessTokenVariableName</span><span class="sxs-lookup"><span data-stu-id="a6e47-171">VSAccessTokenVariableName</span></span> | <span data-ttu-id="a6e47-172">VSTS 개인 액세스 토큰을 보유하는 보안 변수(VSToken)의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a6e47-172">The name of the secure variable (VSToken) that holds the VSTS personal access token.</span></span>|

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSGitWebhook.png)

<span data-ttu-id="a6e47-173">코드 체크 인 시, 이 webhook을 트리거하는 폴더로의 체크 인을 위해 VSTS에 서비스 후크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a6e47-173">Create a service hook in VSTS for check-ins to the folder that triggers this webhook on code check-in.</span></span> <span data-ttu-id="a6e47-174">새 구독을 만들 때 통합할 서비스로 webhook를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e47-174">Select Web Hooks as the service to integrate with when you create a new subscription.</span></span> <span data-ttu-id="a6e47-175">[VSTS 서비스 후크 설명서](https://www.visualstudio.com/en-us/docs/marketplace/integrate/service-hooks/get-started)에서 서비스 후크에 대해 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6e47-175">You can learn more about service hooks on [VSTS Service Hooks documentation](https://www.visualstudio.com/en-us/docs/marketplace/integrate/service-hooks/get-started).</span></span>
![](media/automation-scenario-source-control-integration-with-VSTS/VSTSServiceHook.png)

<span data-ttu-id="a6e47-176">이제 VSTS에 대한 runbook 및 구성의 모든 체크 인을 수행하고 이러한 항목을 Automation 계정에 자동으로 동기화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6e47-176">You should now be able to do all check-ins of your runbooks and configurations into VSTS and have these automatically sync’d into your automation account.</span></span>

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSSyncRunbookOutput.png)

<span data-ttu-id="a6e47-177">VSTS에 의해 트리거되지 않고 수동으로 이 runbook을 실행하는 경우 webhookdata 매개 변수를 비워 둘 수 있습니다. 그러면 지정된 VSTS 폴더에서 전체 동기화가 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6e47-177">If you run this runbook manually without being triggered by VSTS, you can leave the webhookdata parameter empty and it will do a full sync from the VSTS folder specified.</span></span>

<span data-ttu-id="a6e47-178">이 시나리오를 제거하려면 VSTS에서 서비스 후크를 제거하고 runbook 및 VSToken 변수를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e47-178">If you wish to uninstall the scenario, remove the service hook from VSTS, delete the runbook, and the VSToken variable.</span></span>

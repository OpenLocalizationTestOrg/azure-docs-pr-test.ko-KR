---
title: "Azure 자동화 Hybrid Runbook Worker에 runbook aaaRun | Microsoft Docs"
description: "이 문서에서는 로컬 데이터 센터 또는 클라우드 공급자를 hello 하이브리드 Runbook 작업자 역할의 컴퓨터에서 runbook을 실행 하는 방법에 대 한 정보를 제공 합니다."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 06227cda-f3d1-47fe-b3f8-436d2b9d81ee
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/22/2017
ms.author: magoedte
ms.openlocfilehash: 51961e02603e5690edd11e577594ad2ddea489a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="running-runbooks-on-a-hybrid-runbook-worker"></a><span data-ttu-id="c084e-103">Hybrid Runbook Worker에서 Runbook 실행</span><span class="sxs-lookup"><span data-stu-id="c084e-103">Running runbooks on a Hybrid Runbook Worker</span></span> 
<span data-ttu-id="c084e-104">Azure 자동화 Hybrid Runbook Worker를 실행 하는를 실행 하는 runbook의 hello 구조에서 차이가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c084e-104">There is no difference in hello structure of runbooks that run in Azure Automation and those that run on a Hybrid Runbook Worker.</span></span> <span data-ttu-id="c084e-105">각 사용 하는 Runbook 가능성이 크게 다른 경우에 일반적으로 하이브리드 Runbook 작업자를 대상으로 하는 runbook 자체 hello 로컬 컴퓨터 또는 배포 된, runbook 동안 hello 로컬 환경에서 리소스에 대 한 리소스를 관리 하므로 Azure 자동화에서 일반적으로 Azure 클라우드 hello에 리소스를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="c084e-105">Runbooks that you use with each most likely differ significantly though since runbooks targeting a Hybrid Runbook Worker typically manage resources on hello local computer itself or against resources in hello local environment where it is deployed, while runbooks in Azure Automation typically manage resources in hello Azure cloud.</span></span>

<span data-ttu-id="c084e-106">Azure 자동화에서 Hybrid Runbook Worker에 대 한 runbook을 편집할 수는 있지만 hello 편집기에서 tootest hello runbook을 시도 하는 경우 문제가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c084e-106">You can edit a runbook for Hybrid Runbook Worker in Azure Automation, but you may have difficulties if you try tootest hello runbook in hello editor.</span></span>  <span data-ttu-id="c084e-107">hello 로컬 리소스 설치 되지 않은 Azure 자동화 환경에는 쿼리에서 액세스 하는 hello PowerShell 모듈과 hello 테스트 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="c084e-107">hello PowerShell modules that access hello local resources may not be installed in your Azure Automation environment in which case, hello test would fail.</span></span>  <span data-ttu-id="c084e-108">설치 하면 hello 필수 모듈, 다음 hello runbook은 실행 되지만 전체 테스트에 대 한 로컬 리소스 수 tooaccess 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c084e-108">If you do install hello required modules, then hello runbook will run, but it will not be able tooaccess local resources for a complete test.</span></span>

## <a name="starting-a-runbook-on-hybrid-runbook-worker"></a><span data-ttu-id="c084e-109">Hybrid Runbook Worker에서 Runbook 시작</span><span class="sxs-lookup"><span data-stu-id="c084e-109">Starting a runbook on Hybrid Runbook Worker</span></span>
<span data-ttu-id="c084e-110">[Azure 자동화에서 Runbook 시작](automation-starting-a-runbook.md) 에 Runbook을 시작하는 여러 가지 방법이 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c084e-110">[Starting a Runbook in Azure Automation](automation-starting-a-runbook.md) describes different methods for starting a runbook.</span></span>  <span data-ttu-id="c084e-111">Hybrid Runbook Worker 추가 **RunOn** Hybrid Runbook Worker Group의 hello 이름을 지정할 수 있는 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="c084e-111">Hybrid Runbook Worker adds a **RunOn** option where you can specify hello name of a Hybrid Runbook Worker Group.</span></span>  <span data-ttu-id="c084e-112">그룹이 지정 된 다음 hello runbook 검색 하 고 hello 직원 들이 해당 그룹의 하 여 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c084e-112">If a group is specified, then hello runbook is retrieved and run by of hello workers in that group.</span></span>  <span data-ttu-id="c084e-113">이 옵션을 지정하지 않으면 평소처럼 Azure 자동화에서 Runbook이 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="c084e-113">If this option is not specified, then it is run in Azure Automation as normal.</span></span>

<span data-ttu-id="c084e-114">제공 됩니다 hello Azure 포털에서에서 runbook을 시작할 때 한 **에서 실행** 옵션을 선택할 수 있는 **Azure** 또는 **Hybrid Worker**합니다.</span><span class="sxs-lookup"><span data-stu-id="c084e-114">When you start a runbook in hello Azure portal, you are presented with a **Run on** option where you can select **Azure** or **Hybrid Worker**.</span></span>  <span data-ttu-id="c084e-115">선택 하는 경우 **Hybrid Worker**, 드롭다운에서 hello 그룹을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c084e-115">If you select **Hybrid Worker**, then you can select hello group from a dropdown.</span></span>

<span data-ttu-id="c084e-116">사용 하 여 hello **RunOn** 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="c084e-116">Use hello **RunOn** parameter.</span></span>  <span data-ttu-id="c084e-117">다음 명령 toostart 라는 MyHybridGroup Windows PowerShell을 사용 하 여 하이브리드 Runbook 작업자 그룹에 Runbook을 라는 runbook hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c084e-117">You can use hello following command toostart a runbook named Test-Runbook on a Hybrid Runbook Worker Group named MyHybridGroup using Windows PowerShell.</span></span>

    Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook" -RunOn "MyHybridGroup"

> [!NOTE]
> <span data-ttu-id="c084e-118">hello **RunOn** toohello 추가 된 매개 변수 **Start-azureautomationrunbook** 0.9.1 버전의 Microsoft Azure PowerShell cmdlet에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c084e-118">hello **RunOn** parameter was added toohello **Start-AzureAutomationRunbook** cmdlet in version 0.9.1 of Microsoft Azure PowerShell.</span></span>  <span data-ttu-id="c084e-119">수행 해야 [hello 최신 버전 다운로드](https://azure.microsoft.com/downloads/) 설치는 이전 하나 있는 경우.</span><span class="sxs-lookup"><span data-stu-id="c084e-119">You should [download hello latest version](https://azure.microsoft.com/downloads/) if you have an earlier one installed.</span></span>  <span data-ttu-id="c084e-120">필요할 때만 tooinstall 워크스테이션 Windows PowerShell에서 hello runbook을 시작 하는 위치에이 버전.</span><span class="sxs-lookup"><span data-stu-id="c084e-120">You only need tooinstall this version on a workstation where you are starting hello runbook from Windows PowerShell.</span></span>  <span data-ttu-id="c084e-121">Tooinstall 불필요 hello 작업자 컴퓨터에 해당 컴퓨터에서 runbook toostart 경우가 아니면 합니다.</span><span class="sxs-lookup"><span data-stu-id="c084e-121">You do not need tooinstall it on hello worker computer unless you intend toostart runbooks from that computer.</span></span>  <span data-ttu-id="c084e-122">현재이 위해서는 hello 최신 버전의 Azure Powershell toobe 자동화 계정에 설치 된 후 다른 runbook에서 Hybrid Runbook Worker에 runbook를 시작할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c084e-122">You cannot currently start a runbook on a Hybrid Runbook Worker from another runbook since this would require hello latest version of Azure Powershell toobe installed in your Automation account.</span></span>  <span data-ttu-id="c084e-123">hello에 대 한 최신 정보는 Azure 자동화에서 자동으로 업데이트 되 고 자동으로 푸시 다운할 toohello 작업자 곧 합니다.</span><span class="sxs-lookup"><span data-stu-id="c084e-123">hello latest version is automatically updated in Azure Automation and automatically pushed down toohello workers soon.</span></span>
>
>

## <a name="runbook-permissions"></a><span data-ttu-id="c084e-124">Runbook 사용 권한</span><span class="sxs-lookup"><span data-stu-id="c084e-124">Runbook permissions</span></span>
<span data-ttu-id="c084e-125">하이브리드 Runbook 작업자에서 실행 되는 Runbook 수 없는 사용 하 여 hello 동일한 Azure 외부의 리소스에 액세스 하는 이후 tooAzure 리소스를 인증 하는 runbook에 대 한 일반적으로 사용 되는 메서드.</span><span class="sxs-lookup"><span data-stu-id="c084e-125">Runbooks running on a Hybrid Runbook Worker cannot use hello same method that is typically used for runbooks authenticating tooAzure resources, since they are accessing resources outside of Azure.</span></span>  <span data-ttu-id="c084e-126">hello runbook 자체 인증 toolocal 리소스를 제공 하거나 수 또는 RunAs 계정 tooprovide 모든 runbook에 대 한 사용자 컨텍스트를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c084e-126">hello runbook can either provide its own authentication toolocal resources, or you can specify a RunAs account tooprovide a user context for all runbooks.</span></span>

### <a name="runbook-authentication"></a><span data-ttu-id="c084e-127">Runbook 인증</span><span class="sxs-lookup"><span data-stu-id="c084e-127">Runbook authentication</span></span>
<span data-ttu-id="c084e-128">기본적으로 runbook은 액세스 하는 자체 인증 tooresources도 제공 해야 하므로 hello 온-프레미스 컴퓨터에 로컬 시스템 계정 hello hello 컨텍스트에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c084e-128">By default, runbooks will run in hello context of hello local System account on hello on-premises computer, so they must provide their own authentication tooresources that they will access.</span></span>  

<span data-ttu-id="c084e-129">사용할 수 있습니다 [자격 증명](http://msdn.microsoft.com/library/dn940015.aspx) 및 [인증서](http://msdn.microsoft.com/library/dn940013.aspx) toospecify 자격 증명 허용 toodifferent 리소스를 인증할 수 있도록 하는 cmdlet이 포함 된 runbook의 자산입니다.</span><span class="sxs-lookup"><span data-stu-id="c084e-129">You can use [Credential](http://msdn.microsoft.com/library/dn940015.aspx) and [Certificate](http://msdn.microsoft.com/library/dn940013.aspx) assets in your runbook with cmdlets that allow you toospecify credentials so you can authenticate toodifferent resources.</span></span>  <span data-ttu-id="c084e-130">hello 다음 예제에서는 컴퓨터를 다시 시작 하는 runbook의 일부</span><span class="sxs-lookup"><span data-stu-id="c084e-130">hello following example shows a portion of a runbook that restarts a computer.</span></span>  <span data-ttu-id="c084e-131">변수 자산에서 hello 컴퓨터의 자격 증명 자산 및 hello 이름에서 자격 증명을 검색 하 고 이러한 값을 사용 하 여 hello Restart-computer cmdlet과 함께 합니다.</span><span class="sxs-lookup"><span data-stu-id="c084e-131">It retrieves credentials from a credential asset and hello name of hello computer from a variable asset and then uses these values with hello Restart-Computer cmdlet.</span></span>

    $Cred = Get-AzureRmAutomationCredential -ResourceGroupName "ResourceGroup01" -Name "MyCredential"
    $Computer = Get-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" -Name  "ComputerName"

    Restart-Computer -ComputerName $Computer -Credential $Cred

<span data-ttu-id="c084e-132">활용할 수 있습니다 [InlineScript](automation-powershell-workflow.md#inlinescript), 있습니다 toorun 코드 블록을 다른 컴퓨터에서 hello로 지정 된 자격 증명으로 [PSCredential 일반 매개 변수](http://technet.microsoft.com/library/jj129719.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="c084e-132">You can also leverage [InlineScript](automation-powershell-workflow.md#inlinescript), which  allows you toorun blocks of code on another computer with credentials specified by hello [PSCredential common parameter](http://technet.microsoft.com/library/jj129719.aspx).</span></span>

### <a name="runas-account"></a><span data-ttu-id="c084e-133">실행 계정</span><span class="sxs-lookup"><span data-stu-id="c084e-133">RunAs account</span></span>
<span data-ttu-id="c084e-134">자신의 인증 toolocal 리소스를 제공 하는 runbook을 대신 지정할 수 있습니다는 **RunAs** Hybrid worker 그룹에 대 한 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="c084e-134">Instead of having runbooks provide their own authentication toolocal resources, you can specify a **RunAs** account for a Hybrid worker group.</span></span>  <span data-ttu-id="c084e-135">지정한는 [자격 증명 자산](automation-credentials.md) hello 그룹에서 하이브리드 Runbook 작업자에서 실행할 때 이러한 자격 증명으로 실행 되는 모든 runbook 및 있는 toolocal 리소스에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="c084e-135">You specify a [credential asset](automation-credentials.md) that has access toolocal resources, and all runbooks run under these credentials when running on a Hybrid Runbook Worker in hello group.</span></span>  

<span data-ttu-id="c084e-136">hello 자격 증명에 대 한 hello 사용자 이름은 hello 다음 형식 중 하나에 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c084e-136">hello user name for hello credential must be in one of hello following formats:</span></span>

* <span data-ttu-id="c084e-137">domain\username</span><span class="sxs-lookup"><span data-stu-id="c084e-137">domain\username</span></span>
* username@domain
* <span data-ttu-id="c084e-138">(로컬 toohello 온-프레미스 컴퓨터 계정)에 대 한 사용자 이름</span><span class="sxs-lookup"><span data-stu-id="c084e-138">username (for accounts local toohello on-premises computer)</span></span>

<span data-ttu-id="c084e-139">다음 프로시저 toospecify Hybrid worker 그룹에 대 한 실행 계정 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c084e-139">Use hello following procedure toospecify a RunAs account for a Hybrid worker group:</span></span>

1. <span data-ttu-id="c084e-140">만들기는 [자격 증명 자산](automation-credentials.md) 와 toolocal 리소스에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="c084e-140">Create a [credential asset](automation-credentials.md) with access toolocal resources.</span></span>
2. <span data-ttu-id="c084e-141">Hello Azure 포털에서에서 자동화 계정을 hello를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c084e-141">Open hello Automation account in hello Azure portal.</span></span>
3. <span data-ttu-id="c084e-142">선택 hello **Hybrid Worker 그룹** 타일을 마우스 다음 hello 그룹을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c084e-142">Select hello **Hybrid Worker Groups** tile, and then select hello group.</span></span>
4. <span data-ttu-id="c084e-143">**모든 설정** 및 **Hybrid Worker 그룹 설정**을 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c084e-143">Select **All settings** and then **Hybrid worker group settings**.</span></span>
5. <span data-ttu-id="c084e-144">변경 **실행** 에서 **기본** 너무**사용자 지정**합니다.</span><span class="sxs-lookup"><span data-stu-id="c084e-144">Change **Run As** from **Default** too**Custom**.</span></span>
6. <span data-ttu-id="c084e-145">Hello 자격 증명 및 클릭 선택 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="c084e-145">Select hello credential and click **Save**.</span></span>

### <a name="automation-run-as-account"></a><span data-ttu-id="c084e-146">Automation 실행 계정</span><span class="sxs-lookup"><span data-stu-id="c084e-146">Automation Run As account</span></span>
<span data-ttu-id="c084e-147">Azure의에서 리소스를 배포 하기 위한 자동화 된 빌드 프로세스의 일부로 필요할 수 있습니다 액세스 tooon 온-프레미스 시스템 toosupport 작업 또는 단계 집합이 배포 시퀀스에서.</span><span class="sxs-lookup"><span data-stu-id="c084e-147">As part of your automated build process for deploying resources in Azure, you may require access tooon-premise systems toosupport a task or set of steps in your deployment sequence.</span></span>  <span data-ttu-id="c084e-148">hello 실행 계정을 사용 하 여 Azure에 대 한 toosupport 인증, 계정 인증서 계정으로 실행 tooinstall hello 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c084e-148">toosupport authentication against Azure using hello Run As account, you need tooinstall hello Run As account certificate.</span></span>  

<span data-ttu-id="c084e-149">다음 PowerShell runbook hello *내보내기 RunAsCertificateToHybridWorker*를 Azure 자동화 계정에서 hello 계정으로 실행 인증서를 내보내는 및 다운로드 하 고에 hello 로컬 컴퓨터 인증서 저장소로 가져옵니다는 하이브리드 작업자 toohello 연결 된 동일한 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="c084e-149">hello following PowerShell runbook, *Export-RunAsCertificateToHybridWorker*, exports hello Run As certificate from your Azure Automation account and downloads and imports it into hello local machine certificate store on a Hybrid worker connected toohello same account.</span></span>  <span data-ttu-id="c084e-150">단계가 완료 되 면 hello 작업자 tooAzure hello 계정으로 실행 계정을 사용 하 여 성공적으로 인증할 수를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c084e-150">Once that step is completed, it verifies hello worker can successfully authenticate tooAzure using hello Run As account.</span></span>

    <#PSScriptInfo
    .VERSION 1.0
    .GUID 3a796b9a-623d-499d-86c8-c249f10a6986
    .AUTHOR Azure Automation Team
    .COMPANYNAME Microsoft
    .COPYRIGHT 
    .TAGS Azure Automation 
    .LICENSEURI 
    .PROJECTURI 
    .ICONURI 
    .EXTERNALMODULEDEPENDENCIES 
    .REQUIREDSCRIPTS 
    .EXTERNALSCRIPTDEPENDENCIES 
    .RELEASENOTES
    #>

    <#  
    .SYNOPSIS  
    Exports hello Run As certificate from an Azure Automation account tooa hybrid worker in that account. 
  
    .DESCRIPTION  
    This runbook exports hello Run As certificate from an Azure Automation account tooa hybrid worker in that account.
    Run this runbook in hello hybrid worker where you want hello certificate installed.
    This allows hello use of hello AzureRunAsConnection tooauthenticate tooAzure and manage Azure resources from runbooks running in hello hybrid worker.

    .EXAMPLE
    .\Export-RunAsCertificateToHybridWorker

    .NOTES
    AUTHOR: Azure Automation Team 
    LASTEDIT: 2016.10.13
    #>

    [OutputType([string])] 

    # Set hello password used for this certificate
    $Password = "YourStrongPasswordForTheCert"

    # Stop on errors
    $ErrorActionPreference = 'stop'

    # Get hello management certificate that will be used toomake calls into Azure Service Management resources
    $RunAsCert = Get-AutomationCertificate -Name "AzureRunAsCertificate"
       
    # location toostore temporary certificate in hello Automation service host
    $CertPath = Join-Path $env:temp  "AzureRunAsCertificate.pfx"
   
    # Save hello certificate
    $Cert = $RunAsCert.Export("pfx",$Password)
    Set-Content -Value $Cert -Path $CertPath -Force -Encoding Byte | Write-Verbose 

    Write-Output ("Importing certificate into $env:computername local machine root store from " + $CertPath)
    $SecurePassword = ConvertTo-SecureString $Password -AsPlainText -Force
    Import-PfxCertificate -FilePath $CertPath -CertStoreLocation Cert:\LocalMachine\My -Password $SecurePassword -Exportable | Write-Verbose

    # Test that authentication tooAzure Resource Manager is working
    $RunAsConnection = Get-AutomationConnection -Name "AzureRunAsConnection" 
    
    Add-AzureRmAccount `
      -ServicePrincipal `
      -TenantId $RunAsConnection.TenantId `
      -ApplicationId $RunAsConnection.ApplicationId `
      -CertificateThumbprint $RunAsConnection.CertificateThumbprint | Write-Verbose

    Set-AzureRmContext -SubscriptionId $RunAsConnection.SubscriptionID | Write-Verbose

    # List automation accounts tooconfirm Azure Resource Manager calls are working
    Get-AzureRmAutomationAccount | Select AutomationAccountName

<span data-ttu-id="c084e-151">Hello 저장 *내보내기 RunAsCertificateToHybridWorker* 으로 runbook tooyour 컴퓨터는 `.ps1` 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c084e-151">Save hello *Export-RunAsCertificateToHybridWorker* runbook tooyour computer with a `.ps1` extension.</span></span>  <span data-ttu-id="c084e-152">자동화 계정으로 가져오고 hello hello 변수 값을 변경 하는 hello runbook 편집 `$Password` 자신의 암호를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c084e-152">Import it into your Automation account and edit hello runbook, changing hello value of hello variable `$Password` with your own password.</span></span>  <span data-ttu-id="c084e-153">게시 한 후 실행 하 고 hello 계정으로 실행 계정을 사용 하 여 runbook을 인증 하는 hello Hybrid Worker 그룹을 대상으로 하는 hello runbook을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c084e-153">Publish and then run hello runbook targeting hello Hybrid Worker group that run and authenticate runbooks using hello Run As account.</span></span>  <span data-ttu-id="c084e-154">hello 작업 스트림 보고서 hello 시도 tooimport hello 인증서 hello 로컬 컴퓨터 저장소 및 개수 자동화 계정이 구독에 정의 되어 있고 인증이 성공 하는 경우에 따라 여러 줄이 포함 된 다음과입니다.</span><span class="sxs-lookup"><span data-stu-id="c084e-154">hello job stream reports hello attempt tooimport hello certificate into hello local machine store, and follows with multiple lines depending on how many Automation accounts are defined in your subscription and if authentication is successful.</span></span>  

## <a name="troubleshooting-runbooks-on-hybrid-runbook-worker"></a><span data-ttu-id="c084e-155">Hybrid Runbook Worker에서 Runbook 문제 해결</span><span class="sxs-lookup"><span data-stu-id="c084e-155">Troubleshooting runbooks on Hybrid Runbook Worker</span></span>
<span data-ttu-id="c084e-156">로그는 각 Hybrid Worker의 로컬에 저장되며 위치는 C:\ProgramData\Microsoft\System Center\Orchestrator\7.2\SMA\Sandboxes입니다.</span><span class="sxs-lookup"><span data-stu-id="c084e-156">Logs are stored locally on each hybrid worker at C:\ProgramData\Microsoft\System Center\Orchestrator\7.2\SMA\Sandboxes.</span></span>  <span data-ttu-id="c084e-157">하이브리드 작업자 오류 및 이벤트에에서 기록 hello Windows 이벤트 로그의 **응용 프로그램 및 서비스 Logs\Microsoft SMA\Operational**합니다.</span><span class="sxs-lookup"><span data-stu-id="c084e-157">Hybrid worker also records errors and events in hello Windows event log under **Application and Services Logs\Microsoft-SMA\Operational**.</span></span>  <span data-ttu-id="c084e-158">이벤트 관련 toorunbooks hello 작업자에서 실행 되는 너무 기록**응용 프로그램 및 서비스 Logs\Microsoft Automation\Operational**합니다.</span><span class="sxs-lookup"><span data-stu-id="c084e-158">Events related toorunbooks executed on hello worker are written too**Application and Services Logs\Microsoft-Automation\Operational**.</span></span>  <span data-ttu-id="c084e-159">hello **Microsoft SMA** 로그에 많은 더 많은 이벤트 관련된 toohello runbook 작업 푸시된 toohello 작업자 및 hello 처리가 hello runbook의 합니다.</span><span class="sxs-lookup"><span data-stu-id="c084e-159">hello **Microsoft-SMA** log includes many more events related toohello runbook job pushed toohello worker and hello processing of hello runbook.</span></span>  <span data-ttu-id="c084e-160">Hello 동안 **Microsoft 자동화** 이벤트 로그에 없는 많은 이벤트가 hello runbook 실행의 문제 해결을 지원 세부 정보와 함께, 적어도 hello runbook 작업의 hello 결과 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c084e-160">While hello **Microsoft-Automation** event log does not have many events with details assisting with hello troubleshooting of runbook execution, you will at least find hello results of hello runbook job.</span></span>  

<span data-ttu-id="c084e-161">[Runbook 출력 및 메시지](automation-runbook-output-and-messages.md) tooAzure 정당한 hybrid worker에서 자동화 같은 hello 클라우드에서 실행 되는 runbook 작업에 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c084e-161">[Runbook output and messages](automation-runbook-output-and-messages.md) are sent tooAzure Automation from hybrid workers just like runbook jobs run in hello cloud.</span></span>  <span data-ttu-id="c084e-162">또한 Verbose hello를 사용할 수 있습니다 및 진행률 스트림을 hello 동일한 다른 runbook에 대 한 동일한 방식으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c084e-162">You can also enable hello Verbose and Progress streams hello same way you would for other runbooks.</span></span>  

<span data-ttu-id="c084e-163">Runbook을 성공적으로 완료 하지 않은 경우 hello 작업 요약 상태가 표시 **Suspended**, hello 문제 해결 문서를 검토 하십시오 [Hybrid Runbook Worker: runbook 작업의 상태와 함께 종료 일시 중단](automation-troubleshooting-hybrid-runbook-worker.md#a-runbook-job-terminates-with-a-status-of-suspended)합니다.</span><span class="sxs-lookup"><span data-stu-id="c084e-163">If your runbooks are not completing successfully and hello job summary shows a status of **Suspended**, please review hello troubleshooting article [Hybrid Runbook Worker: A runbook job terminates with a status of Suspended](automation-troubleshooting-hybrid-runbook-worker.md#a-runbook-job-terminates-with-a-status-of-suspended).</span></span>   

## <a name="next-steps"></a><span data-ttu-id="c084e-164">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c084e-164">Next steps</span></span>
* <span data-ttu-id="c084e-165">runbook을 사용 하는 toostart 수 있는 hello 다른 메서드에 대 한 자세한 정보는 toolearn 참조 [Azure 자동화에서 Runbook 시작](automation-starting-a-runbook.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c084e-165">toolearn more about hello different methods that can be used toostart a runbook, see [Starting a Runbook in Azure Automation](automation-starting-a-runbook.md).</span></span>  
* <span data-ttu-id="c084e-166">hello toounderstand hello 텍스트 편집기를 사용 하 여 Azure 자동화는 PowerShell 및 PowerShell 워크플로 runbook으로 작업 하기 위한 다른 절차 참조 [Azure 자동화에서 Runbook 편집](automation-edit-textual-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="c084e-166">toounderstand hello different procedures for working with PowerShell and PowerShell Workflow runbooks in Azure Automation using hello textual editor, see [Editing a Runbook in Azure Automation](automation-edit-textual-runbook.md)</span></span>

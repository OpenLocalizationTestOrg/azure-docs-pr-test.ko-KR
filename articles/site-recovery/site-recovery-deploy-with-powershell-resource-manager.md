---
title: "PowerShell 및 Azure Resource Manager를 사용하여 Hyper-V VM 복제 | Microsoft Docs"
description: "PowerShell 및 Azure Resource Manager를 사용하여 Azure Site Recovery를 통해 자동으로 Hyper-V VM을 Azure로 복제합니다."
services: site-recovery
documentationcenter: 
author: bsiva
manager: abhiag
editor: 
ms.assetid: 05e0d76e-c3f5-4845-8052-094019b6d102
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/31/2017
ms.author: bsiva
ms.openlocfilehash: dbd562b73b0caecd0feb993bd6fb796dddb0438c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-between-on-premises-hyper-v-virtual-machines-and-azure-by-using-powershell-and-azure-resource-manager"></a><span data-ttu-id="f78f7-103">PowerShell 및 Azure Resource Manager를 사용하여 온-프레미스 Hyper-V 가상 컴퓨터와 Azure 간 복제</span><span class="sxs-lookup"><span data-stu-id="f78f7-103">Replicate between on-premises Hyper-V virtual machines and Azure by using PowerShell and Azure Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f78f7-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="f78f7-104">Azure Portal</span></span>](site-recovery-hyper-v-site-to-azure.md)
> * [<span data-ttu-id="f78f7-105">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f78f7-105">PowerShell - Resource Manager</span></span>](site-recovery-deploy-with-powershell-resource-manager.md)
> * [<span data-ttu-id="f78f7-106">클래식 포털</span><span class="sxs-lookup"><span data-stu-id="f78f7-106">Classic Portal</span></span>](site-recovery-hyper-v-site-to-azure-classic.md)
>
>

## <a name="overview"></a><span data-ttu-id="f78f7-107">개요</span><span class="sxs-lookup"><span data-stu-id="f78f7-107">Overview</span></span>
<span data-ttu-id="f78f7-108">Azure Site Recovery는 여러 배포 시나리오에서 가상 컴퓨터의 복제, 장애 조치(Failover) 및 복구를 오케스트레이션하여 비즈니스 연속성 및 재해 복구 전략에 기여합니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-108">Azure Site Recovery contributes to your business continuity and disaster recovery strategy by orchestrating replication, failover, and recovery of virtual machines in a number of deployment scenarios.</span></span> <span data-ttu-id="f78f7-109">배포 시나리오의 전체 목록은 [Azure Site Recovery 개요](site-recovery-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f78f7-109">For a full list of deployment scenarios, see the [Azure Site Recovery overview](site-recovery-overview.md).</span></span>

<span data-ttu-id="f78f7-110">Azure PowerShell은 Windows PowerShell을 통해 Azure를 관리하기 위한 cmdlet을 제공하는 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-110">Azure PowerShell is a module that provides cmdlets to manage Azure through Windows PowerShell.</span></span> <span data-ttu-id="f78f7-111">Azure 프로필 모듈 또는 Azure Resource Manager 모듈 등 두 유형의 모듈로 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-111">It can work with two types of modules: the Azure Profile module, or the Azure Resource Manager module.</span></span>

<span data-ttu-id="f78f7-112">Azure Resource Manager에 대한 Azure PowerShell과 함께 사용할 수 있는 사이트 복구 PowerShell cmdlet을 사용하여 Azure에서 서버를 보호하고 복구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-112">Site Recovery PowerShell cmdlets, available with Azure PowerShell for Azure Resource Manager, help you protect and recover your servers in Azure.</span></span>

<span data-ttu-id="f78f7-113">이 문서에서는 Azure에 서버 보호를 구성하고 오케스트레이션하기 위해 Azure Resource Manager와 함께 Windows PowerShell을 사용하여 사이트 복구를 배포하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-113">This article describes how to use Windows PowerShell, together with Azure Resource Manager, to deploy Site Recovery to configure and orchestrate server protection to Azure.</span></span> <span data-ttu-id="f78f7-114">이 문서에 사용된 예제는 Azure Resource Manager로 Azure PowerShell을 사용하여 Azure에 대한 Hyper-V 호스트의 가상 컴퓨터를 보호, 장애 조치하고 복구하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-114">The example used in this article shows you how to protect, fail over, and recover virtual machines on a Hyper-V host to Azure, by using Azure PowerShell with Azure Resource Manager.</span></span>

> [!NOTE]
> <span data-ttu-id="f78f7-115">사이트 복구 PowerShell cmdlet을 사용하여 한 가상 컴퓨터 관리자 사이트에서 다른 가상 컴퓨터 관리자 사이트로, 가상 컴퓨터 관리자 사이트에서 Azure로, Hyper-V 사이트에서 Azure로 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-115">The Site Recovery PowerShell cmdlets currently allow you to configure the following: one Virtual Machine Manager site to another, a Virtual Machine Manager site to Azure, and a Hyper-V site to Azure.</span></span>
>
>

<span data-ttu-id="f78f7-116">이 문서를 사용하기 위해 PowerShell 전문가가 될 필요는 없지만 모듈, cmdlet 및 세션과 같은 기본 개념을 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-116">You don't need to be a PowerShell expert to use this article, but you do need to understand the basic concepts, such as modules, cmdlets, and sessions.</span></span> <span data-ttu-id="f78f7-117">Windows PowerShell에 대한 자세한 내용은 [Windows PowerShell 시작](http://technet.microsoft.com/library/hh857337.aspx)(영문)을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="f78f7-117">For more information about Windows PowerShell, see [Getting Started with Windows PowerShell](http://technet.microsoft.com/library/hh857337.aspx).</span></span>

<span data-ttu-id="f78f7-118">자세한 내용은 [Azure Resource Manager에서 Azure PowerShell 사용](../powershell-azure-resource-manager.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f78f7-118">You can also read more about [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

> [!NOTE]
> <span data-ttu-id="f78f7-119">CSP(클라우드 솔루션 공급자) 프로그램의 일부인 Microsoft 파트너를 통해 고객의 각 CSP 구독(테넌트 구독)에 대한 고객의 서버 보호를 구성하고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-119">Microsoft partners that are part of the Cloud Solution Provider (CSP) program can configure and manage protection of their customers' servers to their customers' respective CSP subscriptions (tenant subscriptions).</span></span>
>
>

## <a name="before-you-start"></a><span data-ttu-id="f78f7-120">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="f78f7-120">Before you start</span></span>
<span data-ttu-id="f78f7-121">다음 필수 조건이 충족되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-121">Make sure you have these prerequisites in place:</span></span>

* <span data-ttu-id="f78f7-122">[Microsoft Azure](https://azure.microsoft.com/) 계정.</span><span class="sxs-lookup"><span data-stu-id="f78f7-122">A [Microsoft Azure](https://azure.microsoft.com/) account.</span></span> <span data-ttu-id="f78f7-123">[무료 평가판](https://azure.microsoft.com/pricing/free-trial/)으로 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-123">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="f78f7-124">[Azure Site Recovery Manager 가격](https://azure.microsoft.com/pricing/details/site-recovery/)에 대해 알아볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-124">In addition, you can read about [Azure Site Recovery Manager pricing](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
* <span data-ttu-id="f78f7-125">Azure PowerShell 1.0</span><span class="sxs-lookup"><span data-stu-id="f78f7-125">Azure PowerShell 1.0.</span></span> <span data-ttu-id="f78f7-126">이 릴리스에 대한 정보 및 설치하는 방법은 [Azure PowerShell 1.0.](https://azure.microsoft.com/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f78f7-126">For information about this release and how to install it, see [Azure PowerShell 1.0.](https://azure.microsoft.com/)</span></span>
* <span data-ttu-id="f78f7-127">[AzureRM.SiteRecovery](https://www.powershellgallery.com/packages/AzureRM.SiteRecovery/) 및 [AzureRM.RecoveryServices](https://www.powershellgallery.com/packages/AzureRM.RecoveryServices/) 모듈.</span><span class="sxs-lookup"><span data-stu-id="f78f7-127">The [AzureRM.SiteRecovery](https://www.powershellgallery.com/packages/AzureRM.SiteRecovery/) and [AzureRM.RecoveryServices](https://www.powershellgallery.com/packages/AzureRM.RecoveryServices/) modules.</span></span> <span data-ttu-id="f78f7-128">[PowerShell 갤러리](https://www.powershellgallery.com/)</span><span class="sxs-lookup"><span data-stu-id="f78f7-128">You can get the latest versions of these modules from the [PowerShell gallery](https://www.powershellgallery.com/)</span></span>

<span data-ttu-id="f78f7-129">이 문서에서는 Azure Resource Manager로 Azure Powershell을 사용하여 서버 보호를 구성하고 관리하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-129">This article illustrates how to use Azure Powershell with Azure Resource Manager to configure and manage protection of your servers.</span></span> <span data-ttu-id="f78f7-130">이 문서에 사용된 예제에서는 Azure에 대한 Hyper-V 호스트에서 실행 중인 가상 컴퓨터를 보호하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-130">The example used in this article shows you how to protect a virtual machine, running on a Hyper-V host, to Azure.</span></span> <span data-ttu-id="f78f7-131">다음에 나오는 필수 구성 요소는 이 예제에 해당됩니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-131">The following prerequisites are specific to this example.</span></span> <span data-ttu-id="f78f7-132">다양한 사이트 복구 시나리오에 대한 포괄적인 요구 사항 집합은 해당 시나리오와 관련된 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f78f7-132">For a more comprehensive set of requirements for the various Site Recovery scenarios, refer to the documentation pertaining to that scenario.</span></span>

* <span data-ttu-id="f78f7-133">하나 이상의 가상 컴퓨터가 포함된 Windows Server 2012 R2 또는 Microsoft Hyper-V Server 2012 R2를 실행하는 Hyper-V 호스트.</span><span class="sxs-lookup"><span data-stu-id="f78f7-133">A Hyper-V host running Windows Server 2012 R2 or Microsoft Hyper-V Server 2012 R2 containing one or more virtual machines.</span></span>
* <span data-ttu-id="f78f7-134">직접 또는 프록시를 통해 인터넷에 연결된 Hyper-V 서버.</span><span class="sxs-lookup"><span data-stu-id="f78f7-134">Hyper-V servers connected to the Internet, either directly or through a proxy.</span></span>
* <span data-ttu-id="f78f7-135">보호할 가상 컴퓨터는 [가상 컴퓨터 필수 조건](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)에 맞아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-135">The virtual machines you want to protect should conform with [Virtual Machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

## <a name="step-1-sign-in-to-your-azure-account"></a><span data-ttu-id="f78f7-136">1단계: Azure 계정에 로그인</span><span class="sxs-lookup"><span data-stu-id="f78f7-136">Step 1: Sign in to your Azure account</span></span>
1. <span data-ttu-id="f78f7-137">PowerShell 콘솔을 열고 이 명령을 실행하여 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-137">Open a PowerShell console and run this command to sign in to your Azure account.</span></span> <span data-ttu-id="f78f7-138">cmdlet은 계정 자격 증명에 대한 프롬프트를 표시하는 웹 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-138">The cmdlet brings up a web page that will prompt you for your account credentials.</span></span>

        Login-AzureRmAccount

    <span data-ttu-id="f78f7-139">또는 `-Credential` 매개 변수를 사용하여 `Login-AzureRmAccount` cmdlet에 대한 매개 변수로 계정 자격 증명을 포함할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-139">Alternately, you could also include your account credentials as a parameter to the `Login-AzureRmAccount` cmdlet, by using the `-Credential` parameter.</span></span>

    <span data-ttu-id="f78f7-140">사용자가 테넌트를 대신하여 작업 중인 CSP 파트너인 경우 tenantID 또는 테넌트 기본 도메인 이름을 사용하여 고객을 테넌트로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-140">If you are CSP partner working on behalf of a tenant, specify the customer as a tenant, by using their tenantID or tenant primary domain name.</span></span>

        Login-AzureRmAccount -Tenant "fabrikam.com"
2. <span data-ttu-id="f78f7-141">계정에 여러 구독이 있을 수 있으므로 사용하려는 구독을 계정과 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-141">An account can have several subscriptions, so you should associate the subscription you want to use with the account.</span></span>

        Select-AzureRmSubscription -SubscriptionName $SubscriptionName
3. <span data-ttu-id="f78f7-142">다음 명령을 사용하여 Recovery Services와 Site Recovery에 대해 Azure 공급자를 사용하도록 구독이 등록되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-142">Verify that your subscription is registered to use the Azure providers for Recovery Services and Site Recovery, by using the following commands:</span></span>

   * `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices`
   * `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`

   <span data-ttu-id="f78f7-143">이러한 명령의 출력에서 **RegistrationState**가 **등록됨**으로 설정된 경우에 2단계를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-143">In the output of these commands, if the **RegistrationState** is set to **Registered**, you can proceed to Step 2.</span></span> <span data-ttu-id="f78f7-144">그렇지 않은 경우 구독에서 누락된 공급자를 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-144">If not, you should register the missing provider in your subscription.</span></span>

   <span data-ttu-id="f78f7-145">사이트 복구 및 복구 서비스에 대해 Azure 공급자를 등록하려면 다음 명령을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-145">To register the Azure provider for Site Recovery and Recovery Services, run the following commands:</span></span>

       Register-AzureRmResourceProvider -ProviderNamespace Microsoft.SiteRecovery
       Register-AzureRmResourceProvider -ProviderNamespace Microsoft.RecoveryServices

   <span data-ttu-id="f78f7-146">`Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices` 및 `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery` 명령을 사용하여 공급자가 성공적으로 등록되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-146">Verify that the providers registered successfully by using the following commands: `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices` and `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`.</span></span>

## <a name="step-2-set-up-the-recovery-services-vault"></a><span data-ttu-id="f78f7-147">2단계: 복구 서비스 자격 증명 모음 설정</span><span class="sxs-lookup"><span data-stu-id="f78f7-147">Step 2: Set up the Recovery Services vault</span></span>
1. <span data-ttu-id="f78f7-148">자격 증명 모음을 만들거나 기존 리소스 그룹을 사용하는 Azure Resource Manager 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-148">Create an Azure Resource Manager resource group in which you'll create the vault, or use an existing resource group.</span></span> <span data-ttu-id="f78f7-149">다음 명령을 사용하여 새로운 리소스 그룹을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-149">You can create a new resource group by using the following command:</span></span>

        New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Geo  

    <span data-ttu-id="f78f7-150">여기서 $ResourceGroupName 변수는 만들려는 리소스 그룹의 이름을 포함하고 $Geo 변수는 리소스 그룹을 만들 Azure 지역(예: "브라질 남부")을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-150">where the $ResourceGroupName variable contains the name of the resource group you want to create, and the $Geo variable contains the Azure region in which to create the resource group (for example, "Brazil South").</span></span>

    <span data-ttu-id="f78f7-151">`Get-AzureRmResourceGroup` cmdlet을 사용하여 구독에 리소스 그룹의 목록을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-151">You can obtain a list of resource groups in your subscription by using the `Get-AzureRmResourceGroup` cmdlet.</span></span>
2. <span data-ttu-id="f78f7-152">다음과 같이 새 Azure 복구 서비스 자격 증명 모음을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-152">Create a new Azure Recovery Services vault as follows:</span></span>

        $vault = New-AzureRmRecoveryServicesVault -Name <string> -ResourceGroupName <string> -Location <string>

    <span data-ttu-id="f78f7-153">`Get-AzureRmRecoveryServicesVault` cmdlet을 사용하여 기존 자격 증명 모음의 목록을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-153">You can retrieve a list of existing vaults by using the `Get-AzureRmRecoveryServicesVault` cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="f78f7-154">클래식 포털 또는 Azure 서비스 관리 PowerShell 모듈을 사용하여 만든 사이트 복구 자격 증명 모음에서 작업을 수행하려는 경우 `Get-AzureRmSiteRecoveryVault` cmdlet을 사용하여 이러한 자격 증명 모음 목록을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-154">If you wish to perform operations on Site Recovery vaults created using the classic portal or the Azure Service Management PowerShell module, you can retrieve a list of such vaults by using the `Get-AzureRmSiteRecoveryVault` cmdlet.</span></span> <span data-ttu-id="f78f7-155">모든 새 작업에 대해 새 복구 서비스 자격 증명 모음을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-155">You should create a new Recovery Services vault for all new operations.</span></span> <span data-ttu-id="f78f7-156">앞서 만든 사이트 복구 자격 증명 모음은 지원되지만 최신 기능이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-156">The Site Recovery vaults you've created earlier are supported, but don't have the latest features.</span></span>
>
>

## <a name="step-3-set-the-recovery-services-vault-context"></a><span data-ttu-id="f78f7-157">3단계: 복구 서비스 자격 증명 모음 설정</span><span class="sxs-lookup"><span data-stu-id="f78f7-157">Step 3: Set the Recovery Services vault context</span></span>
1. <span data-ttu-id="f78f7-158">다음 명령을 실행하여 자격 증명 모음 컨텍스트를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-158">Set the vault context by running the following command:</span></span>

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-create-a-hyper-v-site-and-generate-a-new-vault-registration-key-for-the-site"></a><span data-ttu-id="f78f7-159">4단계: Hyper-V 사이트를 만들고 사이트에 대한 새 자격 증명 모음 등록 키를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-159">Step 4: Create a Hyper-V site and generate a new vault registration key for the site.</span></span>
1. <span data-ttu-id="f78f7-160">다음과 같이 새 Hyper-V 사이트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-160">Create a new Hyper-V site as follows:</span></span>

        $sitename = "MySite"                #Specify site friendly name
        New-AzureRmSiteRecoverySite -Name $sitename

    <span data-ttu-id="f78f7-161">이 cmdlet은 사이트 복구 작업을 시작하여 사이트를 만들고 사이트 복구 작업 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-161">This cmdlet starts a Site Recovery job to create the site, and returns a Site Recovery job object.</span></span> <span data-ttu-id="f78f7-162">작업이 완료될 때까지 기다리고 작업이 성공적으로 완료되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-162">Wait for the job to complete and verify that the job completed successfully.</span></span>

    <span data-ttu-id="f78f7-163">작업 개체를 검색할 수 있으므로 Get-AzureRmSiteRecoveryJob cmdlet을 사용하여 작업의 현재 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-163">You can retrieve the job object, and thereby check the current status of the job, by using the Get-AzureRmSiteRecoveryJob cmdlet.</span></span>
2. <span data-ttu-id="f78f7-164">다음과 같이 사이트에 대한 등록 키를 생성하고 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-164">Generate and download a registration key for the site, as follows:</span></span>

        $SiteIdentifier = Get-AzureRmSiteRecoverySite -Name $sitename | Select -ExpandProperty SiteIdentifier
        Get-AzureRmRecoveryServicesVaultSettingsFile -Vault $vault -SiteIdentifier $SiteIdentifier -SiteFriendlyName $sitename -Path $Path

    <span data-ttu-id="f78f7-165">Hyper-V 호스트에 다운로드한 키를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-165">Copy the downloaded key to the Hyper-V host.</span></span> <span data-ttu-id="f78f7-166">사이트에 Hyper-V 호스트를 등록하는 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-166">You need the key to register the Hyper-V host to the site.</span></span>

## <a name="step-5-install-the-azure-site-recovery-provider-and-azure-recovery-services-agent-on-your-hyper-v-host"></a><span data-ttu-id="f78f7-167">5단계: Hyper-V 호스트에 Azure Site Recovery 공급자와 Azure 복구 서비스 에이전트 설치</span><span class="sxs-lookup"><span data-stu-id="f78f7-167">Step 5: Install the Azure Site Recovery provider and Azure Recovery Services Agent on your Hyper-V host</span></span>
1. <span data-ttu-id="f78f7-168">[Microsoft](https://aka.ms/downloaddra)에서 공급자의 최신 버전을 위한 설치 관리자를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-168">Download the installer for the latest version of the provider from [Microsoft](https://aka.ms/downloaddra).</span></span>
2. <span data-ttu-id="f78f7-169">Hyper-V 호스트에서 설치 관리자를 실행하고 설치 끝부분에서 등록 단계를 계속 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-169">Run the installer on your Hyper-V host, and at the end of the installation continue to the registration step.</span></span>
3. <span data-ttu-id="f78f7-170">메시지가 표시되면 다운로드한 사이트 등록 키를 제공하고 사이트에 Hyper-V 호스트의 등록을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-170">When prompted, provide the downloaded site registration key, and complete registration of the Hyper-V host to the site.</span></span>
4. <span data-ttu-id="f78f7-171">다음 명령을 사용하여 Hyper-V 호스트가 사이트에 등록되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-171">Verify that the Hyper-V host is registered to the site by using the following command:</span></span>

        $server =  Get-AzureRmSiteRecoveryServer -FriendlyName $server-friendlyname

## <a name="step-6-create-a-replication-policy-and-associate-it-with-the-protection-container"></a><span data-ttu-id="f78f7-172">6단계: 복제 정책을 만들고 보호 컨테이너와 연결</span><span class="sxs-lookup"><span data-stu-id="f78f7-172">Step 6: Create a replication policy and associate it with the protection container</span></span>
1. <span data-ttu-id="f78f7-173">다음과 같이 복제 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-173">Create a replication policy as follows:</span></span>

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $Recoverypoints = 6                    #specify the number of recovery points
        $storageaccountID = Get-AzureRmStorageAccount -Name "mystorea" -ResourceGroupName "MyRG" | Select -ExpandProperty Id

        $PolicyResult = New-AzureRmSiteRecoveryPolicy -Name $PolicyName -ReplicationProvider “HyperVReplicaAzure” -ReplicationFrequencyInSeconds $ReplicationFrequencyInSeconds  -RecoveryPoints $Recoverypoints -ApplicationConsistentSnapshotFrequencyInHours 1 -RecoveryAzureStorageAccountId $storageaccountID

    <span data-ttu-id="f78f7-174">반환된 작업을 확인하여 복제 정책 만들기 성공했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-174">Check the returned job to ensure that the replication policy creation succeeds.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="f78f7-175">지정된 저장소 계정은 복구 서비스 자격 증명 모음과 같은 Azure 지역에 있어야 하고 지역에서 복제를 활성화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-175">The storage account specified should be in the same Azure region as your Recovery Services vault, and should have geo-replication enabled.</span></span>
   >
   > * <span data-ttu-id="f78f7-176">지정된 복구 저장소 계정이 Azure 저장소 형식(클래식)인 경우 보호된 컴퓨터의 장애 조치는 Azure IaaS(클래식)에 대한 컴퓨터를 복구합니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-176">If the specified Recovery storage account is of type Azure Storage (Classic), failover of the protected machines recover the machine to Azure IaaS (Classic).</span></span>
   > * <span data-ttu-id="f78f7-177">지정된 복구 저장소 계정이 Azure 저장소 형식(Azure Resource Manager)인 경우 보호된 컴퓨터의 장애 조치는 Azure IaaS(Azure Resource Manager)에 대한 컴퓨터를 복구합니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-177">If the specified Recovery storage account is of type Azure Storage (Azure Resource Manager), failover of the protected machines recover the machine to Azure IaaS (Azure Resource Manager).</span></span>
   >
   >
2. <span data-ttu-id="f78f7-178">다음과 같이 사이트에 해당하는 보호 컨테이너를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-178">Get the protection container corresponding to the site, as follows:</span></span>

        $protectionContainer = Get-AzureRmSiteRecoveryProtectionContainer
3. <span data-ttu-id="f78f7-179">다음과 같이 복제 정책을 사용하여 보호 컨테이너 연결을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-179">Start the association of the protection container with the replication policy, as follows:</span></span>

     <span data-ttu-id="f78f7-180">$Policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $PolicyName   $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy $Policy -PrimaryProtectionContainer $protectionContainer</span><span class="sxs-lookup"><span data-stu-id="f78f7-180">$Policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $PolicyName   $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy $Policy -PrimaryProtectionContainer $protectionContainer</span></span>

   <span data-ttu-id="f78f7-181">연결 작업이 완료될 때까지 기다리고 성공적으로 완료되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-181">Wait for the association job to complete, and ensure that it completed successfully.</span></span>

## <a name="step-7-enable-protection-for-virtual-machines"></a><span data-ttu-id="f78f7-182">7단계: 가상 컴퓨터의 보호 활성화</span><span class="sxs-lookup"><span data-stu-id="f78f7-182">Step 7: Enable protection for virtual machines</span></span>
1. <span data-ttu-id="f78f7-183">다음과 같이 보호하려는 VM에 해당하는 보호 엔터티를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-183">Get the protection entity corresponding to the VM you want to protect, as follows:</span></span>

        $VMFriendlyName = "Fabrikam-app"                    #Name of the VM
        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -ProtectionContainer $protectionContainer -FriendlyName $VMFriendlyName
2. <span data-ttu-id="f78f7-184">다음과 같이 가상 컴퓨터의 보호를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-184">Start protecting the virtual machine, as follows:</span></span>

        $Ostype = "Windows"                                 # "Windows" or "Linux"
        $DRjob = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionEntity -Policy $Policy -Protection Enable -RecoveryAzureStorageAccountId $storageaccountID  -OS $OStype -OSDiskName $protectionEntity.Disks[0].Name

   > [!IMPORTANT]
   > <span data-ttu-id="f78f7-185">지정된 저장소 계정은 복구 서비스 자격 증명 모음과 같은 Azure 지역에 있어야 하고 지역에서 복제를 활성화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-185">The storage account specified should be in the same Azure region as your Recovery Services vault, and should have geo-replication enabled.</span></span>
   >
   > * <span data-ttu-id="f78f7-186">지정된 복구 저장소 계정이 Azure 저장소 형식(클래식)인 경우 보호된 컴퓨터의 장애 조치는 Azure IaaS(클래식)에 대한 컴퓨터를 복구합니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-186">If the specified Recovery storage account is of type Azure Storage (Classic), failover of the protected machines recover the machine to Azure IaaS (Classic).</span></span>
   > * <span data-ttu-id="f78f7-187">지정된 복구 저장소 계정이 Azure 저장소 형식(Azure Resource Manager)인 경우 보호된 컴퓨터의 장애 조치는 Azure IaaS(Azure Resource Manager)에 대한 컴퓨터를 복구합니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-187">If the specified Recovery storage account is of type Azure Storage (Azure Resource Manager), failover of the protected machines recover the machine to Azure IaaS (Azure Resource Manager).</span></span>
   >
   > <span data-ttu-id="f78f7-188">보호하는 VM에 둘 이상의 디스크가 연결된 경우 *OSDiskName* 매개 변수를 사용하여 운영 체제 디스크를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-188">If the VM you are protecting has more than one disk attached to it, specify the operating system disk by using the *OSDiskName* parameter.</span></span>
   >
   >
3. <span data-ttu-id="f78f7-189">가상 컴퓨터가 초기 복제 이후의 보호되는 상태에 도달할 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-189">Wait for the virtual machines to reach a protected state after the initial replication.</span></span> <span data-ttu-id="f78f7-190">복제될 데이터의 양과 Azure에 사용 가능한 업스트림 대역폭 등의 요인에 따라 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-190">This can take a while, depending on factors such as the amount of data to be replicated and the available upstream bandwidth to Azure.</span></span> <span data-ttu-id="f78f7-191">작업 상태와 작업 설명은 VM이 보호되는 상태에 도달할 때 다음과 같이 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-191">The job State and StateDescription are updated as follows, upon the VM reaching a protected state.</span></span>

        PS C:\> $DRjob = Get-AzureRmSiteRecoveryJob -Job $DRjob

        PS C:\> $DRjob | Select-Object -ExpandProperty State
        Succeeded

        PS C:\> $DRjob | Select-Object -ExpandProperty StateDescription
        Completed
4. <span data-ttu-id="f78f7-192">장애 조치 시에 가상 컴퓨터의 네트워크 인터페이스 카드를 연결할 VM 역할 크기 및 Azure 네트워크와 같은 복구 속성을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-192">Update recovery properties, such as the VM role size, and the Azure network to attach the virtual machine's network interface cards to upon failover.</span></span>

        PS C:\> $nw1 = Get-AzureRmVirtualNetwork -Name "FailoverNw" -ResourceGroupName "MyRG"

        PS C:\> $VMFriendlyName = "Fabrikam-App"

        PS C:\> $VM = Get-AzureRmSiteRecoveryVM -ProtectionContainer $protectionContainer -FriendlyName $VMFriendlyName

        PS C:\> $UpdateJob = Set-AzureRmSiteRecoveryVM -VirtualMachine $VM -PrimaryNic $VM.NicDetailsList[0].NicId -RecoveryNetworkId $nw1.Id -RecoveryNicSubnetName $nw1.Subnets[0].Name

        PS C:\> $UpdateJob = Get-AzureRmSiteRecoveryJob -Job $UpdateJob

        PS C:\> $UpdateJob

        Name             : b8a647e0-2cb9-40d1-84c4-d0169919e2c5
        ID               : /Subscriptions/a731825f-4bf2-4f81-a611-c331b272206e/resourceGroups/MyRG/providers/Microsoft.RecoveryServices/vault
                           s/MyVault/replicationJobs/b8a647e0-2cb9-40d1-84c4-d0169919e2c5
        Type             : Microsoft.RecoveryServices/vaults/replicationJobs
        JobType          : UpdateVmProperties
        DisplayName      : Update the virtual machine
        ClientRequestId  : 805a22a3-be86-441c-9da8-f32685673112-2015-12-10 17:55:51Z-P
        State            : Succeeded
        StateDescription : Completed
        StartTime        : 10-12-2015 17:55:53 +00:00
        EndTime          : 10-12-2015 17:55:54 +00:00
        TargetObjectId   : 289682c6-c5e6-42dc-a1d2-5f9621f78ae6
        TargetObjectType : ProtectionEntity
        TargetObjectName : Fabrikam-App
        AllowedActions   : {Restart}
        Tasks            : {UpdateVmPropertiesTask}
        Errors           : {}



## <a name="step-8-run-a-test-failover"></a><span data-ttu-id="f78f7-193">8단계: 테스트 장애 조치 실행</span><span class="sxs-lookup"><span data-stu-id="f78f7-193">Step 8: Run a test failover</span></span>
1. <span data-ttu-id="f78f7-194">다음과 같이 테스트 장애 조치 작업을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-194">Run a test failover job, as follows:</span></span>

        $nw = Get-AzureRmVirtualNetwork -Name "TestFailoverNw" -ResourceGroupName "MyRG" #Specify Azure vnet name and resource group

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -FriendlyName $VMFriendlyName -ProtectionContainer $protectionContainer

        $TFjob = Start-AzureRmSiteRecoveryTestFailoverJob -ProtectionEntity $protectionEntity -Direction PrimaryToRecovery -AzureVMNetworkId $nw.Id
2. <span data-ttu-id="f78f7-195">테스트 VM이 Azure에서 만들어졌는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-195">Verify that the test VM is created in Azure.</span></span> <span data-ttu-id="f78f7-196">(Azure에서 테스트 VM을 만든 후 테스트 장애 조치 작업이 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-196">(The test failover job is suspended, after creating the test VM in Azure.</span></span> <span data-ttu-id="f78f7-197">다음 단계에 설명된 대로 작업 다시 시작 시 생성된 아티팩트를 정리하여 작업이 완료됩니다.)</span><span class="sxs-lookup"><span data-stu-id="f78f7-197">The job completes by cleaning up the created artefacts upon resuming the job, as illustrated in the next step.)</span></span>
3. <span data-ttu-id="f78f7-198">다음과 같이 테스트 장애 조치(Failover)를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="f78f7-198">Complete the test failover, as follows:</span></span>

        $TFjob = Resume-AzureRmSiteRecoveryJob -Job $TFjob

## <a name="next-steps"></a><span data-ttu-id="f78f7-199">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f78f7-199">Next Steps</span></span>
<span data-ttu-id="f78f7-200">[자세히 알아보세요](https://msdn.microsoft.com/library/azure/mt637930.aspx) .</span><span class="sxs-lookup"><span data-stu-id="f78f7-200">[Read more](https://msdn.microsoft.com/library/azure/mt637930.aspx) about Azure Site Recovery with Azure Resource Manager PowerShell cmdlets.</span></span>

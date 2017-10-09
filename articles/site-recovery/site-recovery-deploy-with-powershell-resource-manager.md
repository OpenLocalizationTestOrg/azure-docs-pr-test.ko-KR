---
title: "PowerShell 및 Azure 리소스 관리자 사용 하 여 Hyper-v Vm aaaReplicate | Microsoft Docs"
description: "PowerShell 및 Azure 리소스 관리자를 사용 하 여 Azure 사이트 복구와 Hyper-v Vm tooAzure의 hello 복제를 자동화 합니다."
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
ms.openlocfilehash: 4fb15ce2e9ad54f1dd6f54ff769eb912aa4b0272
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-between-on-premises-hyper-v-virtual-machines-and-azure-by-using-powershell-and-azure-resource-manager"></a><span data-ttu-id="be5d3-103">PowerShell 및 Azure Resource Manager를 사용하여 온-프레미스 Hyper-V 가상 컴퓨터와 Azure 간 복제</span><span class="sxs-lookup"><span data-stu-id="be5d3-103">Replicate between on-premises Hyper-V virtual machines and Azure by using PowerShell and Azure Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="be5d3-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="be5d3-104">Azure Portal</span></span>](site-recovery-hyper-v-site-to-azure.md)
> * [<span data-ttu-id="be5d3-105">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="be5d3-105">PowerShell - Resource Manager</span></span>](site-recovery-deploy-with-powershell-resource-manager.md)
> * [<span data-ttu-id="be5d3-106">클래식 포털</span><span class="sxs-lookup"><span data-stu-id="be5d3-106">Classic Portal</span></span>](site-recovery-hyper-v-site-to-azure-classic.md)
>
>

## <a name="overview"></a><span data-ttu-id="be5d3-107">개요</span><span class="sxs-lookup"><span data-stu-id="be5d3-107">Overview</span></span>
<span data-ttu-id="be5d3-108">Azure Site Recovery는 복제, 장애 조치 및 다양 한 배포 시나리오에서에서 가상 컴퓨터의 복구를 오케스트레이션 하 여 tooyour 비즈니스 연속성 및 재해 복구 전략을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="be5d3-108">Azure Site Recovery contributes tooyour business continuity and disaster recovery strategy by orchestrating replication, failover, and recovery of virtual machines in a number of deployment scenarios.</span></span> <span data-ttu-id="be5d3-109">배포 시나리오의 전체 목록을 보려면 hello [Azure Site Recovery 개요](site-recovery-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="be5d3-109">For a full list of deployment scenarios, see hello [Azure Site Recovery overview](site-recovery-overview.md).</span></span>

<span data-ttu-id="be5d3-110">Azure PowerShell은 cmdlet toomanage Windows PowerShell을 통해 Azure를 제공 하는 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="be5d3-110">Azure PowerShell is a module that provides cmdlets toomanage Azure through Windows PowerShell.</span></span> <span data-ttu-id="be5d3-111">두 가지 유형의 모듈에서 작동할 수: hello Azure 프로필 모듈 또는 hello Azure 리소스 관리자 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="be5d3-111">It can work with two types of modules: hello Azure Profile module, or hello Azure Resource Manager module.</span></span>

<span data-ttu-id="be5d3-112">Azure Resource Manager에 대한 Azure PowerShell과 함께 사용할 수 있는 사이트 복구 PowerShell cmdlet을 사용하여 Azure에서 서버를 보호하고 복구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be5d3-112">Site Recovery PowerShell cmdlets, available with Azure PowerShell for Azure Resource Manager, help you protect and recover your servers in Azure.</span></span>

<span data-ttu-id="be5d3-113">이 문서에서는 설명 방법을 toouse Windows PowerShell과 함께 Azure 리소스 관리자, toodeploy 사이트 복구 tooconfigure 고 서버 보호 tooAzure를 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="be5d3-113">This article describes how toouse Windows PowerShell, together with Azure Resource Manager, toodeploy Site Recovery tooconfigure and orchestrate server protection tooAzure.</span></span> <span data-ttu-id="be5d3-114">이 문서에서 사용 하는 hello 예제 tooprotect, 장애 조치 하 고 Azure 리소스 관리자와 Azure PowerShell을 사용 하 여 Hyper-v 호스트 tooAzure에 가상 컴퓨터를 복구 하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="be5d3-114">hello example used in this article shows you how tooprotect, fail over, and recover virtual machines on a Hyper-V host tooAzure, by using Azure PowerShell with Azure Resource Manager.</span></span>

> [!NOTE]
> <span data-ttu-id="be5d3-115">hello 사이트 복구 PowerShell cmdlet 현재를 사용 하면 다음 tooconfigure hello: 하나의 가상 컴퓨터 관리자 사이트 tooanother, 가상 컴퓨터 관리자 사이트 tooAzure 및 Hyper-v 사이트 tooAzure 합니다.</span><span class="sxs-lookup"><span data-stu-id="be5d3-115">hello Site Recovery PowerShell cmdlets currently allow you tooconfigure hello following: one Virtual Machine Manager site tooanother, a Virtual Machine Manager site tooAzure, and a Hyper-V site tooAzure.</span></span>
>
>

<span data-ttu-id="be5d3-116">Toounderstand hello 등의 기본 개념, 모듈, cmdlet 및 세션 필요는 없지만이 문서에서는 PowerShell 전문가 toouse toobe 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="be5d3-116">You don't need toobe a PowerShell expert toouse this article, but you do need toounderstand hello basic concepts, such as modules, cmdlets, and sessions.</span></span> <span data-ttu-id="be5d3-117">Windows PowerShell에 대한 자세한 내용은 [Windows PowerShell 시작](http://technet.microsoft.com/library/hh857337.aspx)(영문)을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="be5d3-117">For more information about Windows PowerShell, see [Getting Started with Windows PowerShell](http://technet.microsoft.com/library/hh857337.aspx).</span></span>

<span data-ttu-id="be5d3-118">자세한 내용은 [Azure Resource Manager에서 Azure PowerShell 사용](../powershell-azure-resource-manager.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="be5d3-118">You can also read more about [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

> [!NOTE]
> <span data-ttu-id="be5d3-119">Hello 클라우드 솔루션 공급자 (CSP) 프로그램의 일부인 Microsoft 파트너를 구성 하 고 해당 고객의 서버에 대 한 보호를 관리할 수 tootheir 고객의 각 CSP 구독 (테 넌 트 구독의 경우).</span><span class="sxs-lookup"><span data-stu-id="be5d3-119">Microsoft partners that are part of hello Cloud Solution Provider (CSP) program can configure and manage protection of their customers' servers tootheir customers' respective CSP subscriptions (tenant subscriptions).</span></span>
>
>

## <a name="before-you-start"></a><span data-ttu-id="be5d3-120">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="be5d3-120">Before you start</span></span>
<span data-ttu-id="be5d3-121">다음 필수 조건이 충족되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="be5d3-121">Make sure you have these prerequisites in place:</span></span>

* <span data-ttu-id="be5d3-122">[Microsoft Azure](https://azure.microsoft.com/) 계정.</span><span class="sxs-lookup"><span data-stu-id="be5d3-122">A [Microsoft Azure](https://azure.microsoft.com/) account.</span></span> <span data-ttu-id="be5d3-123">[무료 평가판](https://azure.microsoft.com/pricing/free-trial/)으로 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be5d3-123">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="be5d3-124">[Azure Site Recovery Manager 가격](https://azure.microsoft.com/pricing/details/site-recovery/)에 대해 알아볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be5d3-124">In addition, you can read about [Azure Site Recovery Manager pricing](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
* <span data-ttu-id="be5d3-125">Azure PowerShell 1.0</span><span class="sxs-lookup"><span data-stu-id="be5d3-125">Azure PowerShell 1.0.</span></span> <span data-ttu-id="be5d3-126">이 릴리스에 대 한 내용은 방법과 tooinstall, 참조 [Azure PowerShell 1.0.](https://azure.microsoft.com/)</span><span class="sxs-lookup"><span data-stu-id="be5d3-126">For information about this release and how tooinstall it, see [Azure PowerShell 1.0.](https://azure.microsoft.com/)</span></span>
* <span data-ttu-id="be5d3-127">hello [AzureRM.SiteRecovery](https://www.powershellgallery.com/packages/AzureRM.SiteRecovery/) 및 [AzureRM.RecoveryServices](https://www.powershellgallery.com/packages/AzureRM.RecoveryServices/) 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="be5d3-127">hello [AzureRM.SiteRecovery](https://www.powershellgallery.com/packages/AzureRM.SiteRecovery/) and [AzureRM.RecoveryServices](https://www.powershellgallery.com/packages/AzureRM.RecoveryServices/) modules.</span></span> <span data-ttu-id="be5d3-128">Hello에서 hello 이러한 모듈의 최신 버전을 얻을 수 있습니다 [PowerShell 갤러리](https://www.powershellgallery.com/)</span><span class="sxs-lookup"><span data-stu-id="be5d3-128">You can get hello latest versions of these modules from hello [PowerShell gallery](https://www.powershellgallery.com/)</span></span>

<span data-ttu-id="be5d3-129">이 문서에서는 설명 방법을 tooconfigure Azure 리소스 관리자와 Azure Powershell toouse 및 서버 보호를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="be5d3-129">This article illustrates how toouse Azure Powershell with Azure Resource Manager tooconfigure and manage protection of your servers.</span></span> <span data-ttu-id="be5d3-130">이 문서에서 사용 하는 hello 예제 방법을 보여주는 tooprotect tooAzure Hyper-v 호스트에서 실행 되는 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="be5d3-130">hello example used in this article shows you how tooprotect a virtual machine, running on a Hyper-V host, tooAzure.</span></span> <span data-ttu-id="be5d3-131">hello 다음 필수 구성 요소는 특정 toothis 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="be5d3-131">hello following prerequisites are specific toothis example.</span></span> <span data-ttu-id="be5d3-132">Hello에 대 한 요구 사항 보다 포괄적인 집합에 대 한 다양 한 사이트 복구 시나리오 toothat 시나리오와 관련 된 toohello 설명서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="be5d3-132">For a more comprehensive set of requirements for hello various Site Recovery scenarios, refer toohello documentation pertaining toothat scenario.</span></span>

* <span data-ttu-id="be5d3-133">하나 이상의 가상 컴퓨터가 포함된 Windows Server 2012 R2 또는 Microsoft Hyper-V Server 2012 R2를 실행하는 Hyper-V 호스트.</span><span class="sxs-lookup"><span data-stu-id="be5d3-133">A Hyper-V host running Windows Server 2012 R2 or Microsoft Hyper-V Server 2012 R2 containing one or more virtual machines.</span></span>
* <span data-ttu-id="be5d3-134">직접 또는 프록시를 통해 toohello 인터넷에 연결 하는 Hyper-v 서버.</span><span class="sxs-lookup"><span data-stu-id="be5d3-134">Hyper-V servers connected toohello Internet, either directly or through a proxy.</span></span>
* <span data-ttu-id="be5d3-135">hello tooprotect 원하는 가상 컴퓨터에 맞아야 합니다 [가상 컴퓨터 필수 구성 요소](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)합니다.</span><span class="sxs-lookup"><span data-stu-id="be5d3-135">hello virtual machines you want tooprotect should conform with [Virtual Machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

## <a name="step-1-sign-in-tooyour-azure-account"></a><span data-ttu-id="be5d3-136">1 단계: tooyour Azure 계정에 로그인</span><span class="sxs-lookup"><span data-stu-id="be5d3-136">Step 1: Sign in tooyour Azure account</span></span>
1. <span data-ttu-id="be5d3-137">PowerShell 콘솔을 열고이 명령 toosign tooyour Azure 계정에서에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="be5d3-137">Open a PowerShell console and run this command toosign in tooyour Azure account.</span></span> <span data-ttu-id="be5d3-138">hello cmdlet 계정 자격 증명을 요청 하는 웹 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="be5d3-138">hello cmdlet brings up a web page that will prompt you for your account credentials.</span></span>

        Login-AzureRmAccount

    <span data-ttu-id="be5d3-139">매개 변수 toohello로 계정 자격 증명도 포함 될 수 또는 `Login-AzureRmAccount` hello를 사용 하 여 cmdlet `-Credential` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="be5d3-139">Alternately, you could also include your account credentials as a parameter toohello `Login-AzureRmAccount` cmdlet, by using hello `-Credential` parameter.</span></span>

    <span data-ttu-id="be5d3-140">CSP 파트너 테 넌 트를 대신 하 여 작업 인 경우에 tenantID 또는 테 넌 트 주 도메인 이름을 사용 하 여 hello 고객 테 넌 트로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="be5d3-140">If you are CSP partner working on behalf of a tenant, specify hello customer as a tenant, by using their tenantID or tenant primary domain name.</span></span>

        Login-AzureRmAccount -Tenant "fabrikam.com"
2. <span data-ttu-id="be5d3-141">한 계정 hello 계정과 toouse hello 구독을 연결 해야 하므로 여러 구독 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be5d3-141">An account can have several subscriptions, so you should associate hello subscription you want toouse with hello account.</span></span>

        Select-AzureRmSubscription -SubscriptionName $SubscriptionName
3. <span data-ttu-id="be5d3-142">구독 등록된 toouse 인지 확인 hello 다음 명령을 사용 하 여 복구 서비스 및 사이트 복구를 위한 Azure 공급자 hello:</span><span class="sxs-lookup"><span data-stu-id="be5d3-142">Verify that your subscription is registered toouse hello Azure providers for Recovery Services and Site Recovery, by using hello following commands:</span></span>

   * `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices`
   * `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`

   <span data-ttu-id="be5d3-143">경우 hello 이러한 명령의 출력 hello에에서 **RegistrationState** 너무 설정**등록 된**, tooStep 2를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be5d3-143">In hello output of these commands, if hello **RegistrationState** is set too**Registered**, you can proceed tooStep 2.</span></span> <span data-ttu-id="be5d3-144">그렇지 않으면 구독에서 hello 누락 된 공급자를 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="be5d3-144">If not, you should register hello missing provider in your subscription.</span></span>

   <span data-ttu-id="be5d3-145">tooregister hello Azure 사이트 복구 및 hello 다음 명령을 실행 하는 복구 서비스 공급자:</span><span class="sxs-lookup"><span data-stu-id="be5d3-145">tooregister hello Azure provider for Site Recovery and Recovery Services, run hello following commands:</span></span>

       Register-AzureRmResourceProvider -ProviderNamespace Microsoft.SiteRecovery
       Register-AzureRmResourceProvider -ProviderNamespace Microsoft.RecoveryServices

   <span data-ttu-id="be5d3-146">Hello 공급자 hello 다음 명령을 사용 하 여 성공적으로 등록 되었는지 확인: `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices` 및 `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`합니다.</span><span class="sxs-lookup"><span data-stu-id="be5d3-146">Verify that hello providers registered successfully by using hello following commands: `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices` and `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`.</span></span>

## <a name="step-2-set-up-hello-recovery-services-vault"></a><span data-ttu-id="be5d3-147">2 단계: hello 복구 서비스 자격 증명 모음 설정</span><span class="sxs-lookup"><span data-stu-id="be5d3-147">Step 2: Set up hello Recovery Services vault</span></span>
1. <span data-ttu-id="be5d3-148">합니다 hello 자격 증명 모음을 만들거나 기존 리소스 그룹을 사용 하 여 Azure 리소스 관리자 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="be5d3-148">Create an Azure Resource Manager resource group in which you'll create hello vault, or use an existing resource group.</span></span> <span data-ttu-id="be5d3-149">다음 명령을 hello를 사용 하 여 새 리소스 그룹을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be5d3-149">You can create a new resource group by using hello following command:</span></span>

        New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Geo  

    <span data-ttu-id="be5d3-150">hello $ResourceGroupName 변수에 포함 hello 리소스 그룹의 이름을 hello toocreate, 원하는 hello $Geo 변수에 포함 hello Azure toocreate hello 리소스 그룹 (예: "브라질 남쪽")의 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="be5d3-150">where hello $ResourceGroupName variable contains hello name of hello resource group you want toocreate, and hello $Geo variable contains hello Azure region in which toocreate hello resource group (for example, "Brazil South").</span></span>

    <span data-ttu-id="be5d3-151">Hello를 사용 하 여 구독에서 리소스 그룹의 목록을 가져올 수 있습니다 `Get-AzureRmResourceGroup` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="be5d3-151">You can obtain a list of resource groups in your subscription by using hello `Get-AzureRmResourceGroup` cmdlet.</span></span>
2. <span data-ttu-id="be5d3-152">다음과 같이 새 Azure 복구 서비스 자격 증명 모음을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="be5d3-152">Create a new Azure Recovery Services vault as follows:</span></span>

        $vault = New-AzureRmRecoveryServicesVault -Name <string> -ResourceGroupName <string> -Location <string>

    <span data-ttu-id="be5d3-153">Hello를 사용 하 여 기존 자격 증명 모음 목록을 검색할 수 있습니다 `Get-AzureRmRecoveryServicesVault` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="be5d3-153">You can retrieve a list of existing vaults by using hello `Get-AzureRmRecoveryServicesVault` cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="be5d3-154">Hello를 사용 하 여 이러한 자격 증명 모음 목록을 검색 하 고 hello 클래식 포털 또는 hello Azure 서비스 관리 PowerShell 모듈을 사용 하 여 만든 사이트 복구 자격 증명에서 tooperform 작업 하려는 경우 `Get-AzureRmSiteRecoveryVault` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="be5d3-154">If you wish tooperform operations on Site Recovery vaults created using hello classic portal or hello Azure Service Management PowerShell module, you can retrieve a list of such vaults by using hello `Get-AzureRmSiteRecoveryVault` cmdlet.</span></span> <span data-ttu-id="be5d3-155">모든 새 작업에 대해 새 복구 서비스 자격 증명 모음을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="be5d3-155">You should create a new Recovery Services vault for all new operations.</span></span> <span data-ttu-id="be5d3-156">앞서 만든 hello 사이트 복구 자격 증명 지원 되기는 하지만 hello 최신 기능에 없는 합니다.</span><span class="sxs-lookup"><span data-stu-id="be5d3-156">hello Site Recovery vaults you've created earlier are supported, but don't have hello latest features.</span></span>
>
>

## <a name="step-3-set-hello-recovery-services-vault-context"></a><span data-ttu-id="be5d3-157">3 단계: hello 복구 서비스 자격 증명 모음 컨텍스트 설정</span><span class="sxs-lookup"><span data-stu-id="be5d3-157">Step 3: Set hello Recovery Services vault context</span></span>
1. <span data-ttu-id="be5d3-158">Hello 다음 명령을 실행 하 여 hello 자격 증명 모음 컨텍스트를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="be5d3-158">Set hello vault context by running hello following command:</span></span>

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-create-a-hyper-v-site-and-generate-a-new-vault-registration-key-for-hello-site"></a><span data-ttu-id="be5d3-159">4 단계: Hyper-v 사이트를 만들고 hello 사이트에 대 한 새 자격 증명 모음 등록 키를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="be5d3-159">Step 4: Create a Hyper-V site and generate a new vault registration key for hello site.</span></span>
1. <span data-ttu-id="be5d3-160">다음과 같이 새 Hyper-V 사이트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="be5d3-160">Create a new Hyper-V site as follows:</span></span>

        $sitename = "MySite"                #Specify site friendly name
        New-AzureRmSiteRecoverySite -Name $sitename

    <span data-ttu-id="be5d3-161">이 cmdlet은 사이트 복구 작업 toocreate hello 사이트를 시작 하 고 사이트 복구 작업 개체를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="be5d3-161">This cmdlet starts a Site Recovery job toocreate hello site, and returns a Site Recovery job object.</span></span> <span data-ttu-id="be5d3-162">Hello 작업 toocomplete 기다렸다가 hello 작업이 완료 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="be5d3-162">Wait for hello job toocomplete and verify that hello job completed successfully.</span></span>

    <span data-ttu-id="be5d3-163">Hello 작업 개체를 검색할 수 있으며 hello AzureRmSiteRecoveryJob Get cmdlet을 사용 하 여 hello hello 작업의 현재 상태를 확인 함으로써 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be5d3-163">You can retrieve hello job object, and thereby check hello current status of hello job, by using hello Get-AzureRmSiteRecoveryJob cmdlet.</span></span>
2. <span data-ttu-id="be5d3-164">생성 하 고 다음과 같이 hello 사이트에 대 한 등록 키를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="be5d3-164">Generate and download a registration key for hello site, as follows:</span></span>

        $SiteIdentifier = Get-AzureRmSiteRecoverySite -Name $sitename | Select -ExpandProperty SiteIdentifier
        Get-AzureRmRecoveryServicesVaultSettingsFile -Vault $vault -SiteIdentifier $SiteIdentifier -SiteFriendlyName $sitename -Path $Path

    <span data-ttu-id="be5d3-165">복사 hello 키 toohello Hyper-v 호스트를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="be5d3-165">Copy hello downloaded key toohello Hyper-V host.</span></span> <span data-ttu-id="be5d3-166">Hello 키 tooregister hello Hyper-v 호스트 toohello 사이트가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="be5d3-166">You need hello key tooregister hello Hyper-V host toohello site.</span></span>

## <a name="step-5-install-hello-azure-site-recovery-provider-and-azure-recovery-services-agent-on-your-hyper-v-host"></a><span data-ttu-id="be5d3-167">5 단계: Hyper-v 호스트에 hello Azure Site Recovery provider 및 Azure 복구 서비스 에이전트 설치</span><span class="sxs-lookup"><span data-stu-id="be5d3-167">Step 5: Install hello Azure Site Recovery provider and Azure Recovery Services Agent on your Hyper-V host</span></span>
1. <span data-ttu-id="be5d3-168">Hello hello 공급자의 최신 버전에 대 한 hello 설치 관리자 다운로드 [Microsoft](https://aka.ms/downloaddra)합니다.</span><span class="sxs-lookup"><span data-stu-id="be5d3-168">Download hello installer for hello latest version of hello provider from [Microsoft](https://aka.ms/downloaddra).</span></span>
2. <span data-ttu-id="be5d3-169">Hello 설치 hello 종료 및 Hyper-v 호스트에서 실행된 hello installer toohello 등록 단계를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="be5d3-169">Run hello installer on your Hyper-V host, and at hello end of hello installation continue toohello registration step.</span></span>
3. <span data-ttu-id="be5d3-170">메시지가 표시 되 면 hello hello Hyper-v 호스트 toohello 사이트의 등록을 완료 하 고 사이트 등록 키 다운로드를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="be5d3-170">When prompted, provide hello downloaded site registration key, and complete registration of hello Hyper-V host toohello site.</span></span>
4. <span data-ttu-id="be5d3-171">해당 hello Hyper-v 호스트 hello 다음 명령을 사용 하 여 등록 된 toohello 사이트는 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="be5d3-171">Verify that hello Hyper-V host is registered toohello site by using hello following command:</span></span>

        $server =  Get-AzureRmSiteRecoveryServer -FriendlyName $server-friendlyname

## <a name="step-6-create-a-replication-policy-and-associate-it-with-hello-protection-container"></a><span data-ttu-id="be5d3-172">6 단계: 복제 정책을 만들고 hello 보호 컨테이너와 연결</span><span class="sxs-lookup"><span data-stu-id="be5d3-172">Step 6: Create a replication policy and associate it with hello protection container</span></span>
1. <span data-ttu-id="be5d3-173">다음과 같이 복제 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="be5d3-173">Create a replication policy as follows:</span></span>

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $Recoverypoints = 6                    #specify hello number of recovery points
        $storageaccountID = Get-AzureRmStorageAccount -Name "mystorea" -ResourceGroupName "MyRG" | Select -ExpandProperty Id

        $PolicyResult = New-AzureRmSiteRecoveryPolicy -Name $PolicyName -ReplicationProvider “HyperVReplicaAzure” -ReplicationFrequencyInSeconds $ReplicationFrequencyInSeconds  -RecoveryPoints $Recoverypoints -ApplicationConsistentSnapshotFrequencyInHours 1 -RecoveryAzureStorageAccountId $storageaccountID

    <span data-ttu-id="be5d3-174">검사 hello hello 복제 정책 만들기가 성공 하면 작업이 tooensure를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="be5d3-174">Check hello returned job tooensure that hello replication policy creation succeeds.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="be5d3-175">hello 저장소 계정을 지정 해야에 복구 서비스 자격 증명 모음과 동일한 Azure 지역 hello 및 지역에서 복제를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="be5d3-175">hello storage account specified should be in hello same Azure region as your Recovery Services vault, and should have geo-replication enabled.</span></span>
   >
   > * <span data-ttu-id="be5d3-176">저장소 계정 유형이 Azure 저장소 (기본)이 복구를 지정 하는 hello hello의 장애 조치 컴퓨터 복구 hello 컴퓨터 tooAzure IaaS (클래식)를 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="be5d3-176">If hello specified Recovery storage account is of type Azure Storage (Classic), failover of hello protected machines recover hello machine tooAzure IaaS (Classic).</span></span>
   > * <span data-ttu-id="be5d3-177">복구 저장소 계정 유형이 Azure 저장소 (Azure 리소스 관리자)이 지정 하는 hello, hello의 장애 조치 컴퓨터 복구 hello 컴퓨터 tooAzure IaaS (Azure 리소스 관리자)를 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="be5d3-177">If hello specified Recovery storage account is of type Azure Storage (Azure Resource Manager), failover of hello protected machines recover hello machine tooAzure IaaS (Azure Resource Manager).</span></span>
   >
   >
2. <span data-ttu-id="be5d3-178">다음과 같이 hello 보호 컨테이너 해당 toohello 사이트, 가져오기:</span><span class="sxs-lookup"><span data-stu-id="be5d3-178">Get hello protection container corresponding toohello site, as follows:</span></span>

        $protectionContainer = Get-AzureRmSiteRecoveryProtectionContainer
3. <span data-ttu-id="be5d3-179">다음과 같이 hello 복제 정책을 사용 하 여 hello 보호 컨테이너의 hello 연결을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="be5d3-179">Start hello association of hello protection container with hello replication policy, as follows:</span></span>

     <span data-ttu-id="be5d3-180">$Policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $PolicyName   $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy $Policy -PrimaryProtectionContainer $protectionContainer</span><span class="sxs-lookup"><span data-stu-id="be5d3-180">$Policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $PolicyName   $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy $Policy -PrimaryProtectionContainer $protectionContainer</span></span>

   <span data-ttu-id="be5d3-181">Hello 연관 작업 toocomplete 기다렸다가 성공적으로 완료 되었는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="be5d3-181">Wait for hello association job toocomplete, and ensure that it completed successfully.</span></span>

## <a name="step-7-enable-protection-for-virtual-machines"></a><span data-ttu-id="be5d3-182">7단계: 가상 컴퓨터의 보호 활성화</span><span class="sxs-lookup"><span data-stu-id="be5d3-182">Step 7: Enable protection for virtual machines</span></span>
1. <span data-ttu-id="be5d3-183">Hello 보호 엔터티 해당 toohello tooprotect를 다음과 같이 원하는 VM 가져오기:</span><span class="sxs-lookup"><span data-stu-id="be5d3-183">Get hello protection entity corresponding toohello VM you want tooprotect, as follows:</span></span>

        $VMFriendlyName = "Fabrikam-app"                    #Name of hello VM
        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -ProtectionContainer $protectionContainer -FriendlyName $VMFriendlyName
2. <span data-ttu-id="be5d3-184">다음과 같이 hello 가상 컴퓨터 보호를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="be5d3-184">Start protecting hello virtual machine, as follows:</span></span>

        $Ostype = "Windows"                                 # "Windows" or "Linux"
        $DRjob = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionEntity -Policy $Policy -Protection Enable -RecoveryAzureStorageAccountId $storageaccountID  -OS $OStype -OSDiskName $protectionEntity.Disks[0].Name

   > [!IMPORTANT]
   > <span data-ttu-id="be5d3-185">hello 저장소 계정을 지정 해야에 복구 서비스 자격 증명 모음과 동일한 Azure 지역 hello 및 지역에서 복제를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="be5d3-185">hello storage account specified should be in hello same Azure region as your Recovery Services vault, and should have geo-replication enabled.</span></span>
   >
   > * <span data-ttu-id="be5d3-186">저장소 계정 유형이 Azure 저장소 (기본)이 복구를 지정 하는 hello hello의 장애 조치 컴퓨터 복구 hello 컴퓨터 tooAzure IaaS (클래식)를 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="be5d3-186">If hello specified Recovery storage account is of type Azure Storage (Classic), failover of hello protected machines recover hello machine tooAzure IaaS (Classic).</span></span>
   > * <span data-ttu-id="be5d3-187">복구 저장소 계정 유형이 Azure 저장소 (Azure 리소스 관리자)이 지정 하는 hello, hello의 장애 조치 컴퓨터 복구 hello 컴퓨터 tooAzure IaaS (Azure 리소스 관리자)를 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="be5d3-187">If hello specified Recovery storage account is of type Azure Storage (Azure Resource Manager), failover of hello protected machines recover hello machine tooAzure IaaS (Azure Resource Manager).</span></span>
   >
   > <span data-ttu-id="be5d3-188">VM을 보호 하는 hello에 둘 이상의 연결 된 tooit 디스크로 hello를 사용 하 여 hello 운영 체제 디스크를 지정 하는 경우 *OSDiskName* 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="be5d3-188">If hello VM you are protecting has more than one disk attached tooit, specify hello operating system disk by using hello *OSDiskName* parameter.</span></span>
   >
   >
3. <span data-ttu-id="be5d3-189">Hello 초기 복제 후 보호 되는 상태로 가상 컴퓨터 tooreach hello에 대 한 대기 합니다.</span><span class="sxs-lookup"><span data-stu-id="be5d3-189">Wait for hello virtual machines tooreach a protected state after hello initial replication.</span></span> <span data-ttu-id="be5d3-190">이렇게 복제 데이터 toobe hello 양 등의 요인에 따라 시간이 오래 걸릴 하 고 사용 가능한 업스트림 대역폭 tooAzure hello.</span><span class="sxs-lookup"><span data-stu-id="be5d3-190">This can take a while, depending on factors such as hello amount of data toobe replicated and hello available upstream bandwidth tooAzure.</span></span> <span data-ttu-id="be5d3-191">hello 작업 상태 및 StateDescription hello 보호 된 상태에 도달 하는 VM에 다음과 같이 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="be5d3-191">hello job State and StateDescription are updated as follows, upon hello VM reaching a protected state.</span></span>

        PS C:\> $DRjob = Get-AzureRmSiteRecoveryJob -Job $DRjob

        PS C:\> $DRjob | Select-Object -ExpandProperty State
        Succeeded

        PS C:\> $DRjob | Select-Object -ExpandProperty StateDescription
        Completed
4. <span data-ttu-id="be5d3-192">VM 역할 크기 hello 및 hello Azure 네트워크 tooattach hello 가상 컴퓨터의 네트워크 인터페이스 카드 tooupon 장애 조치 같은 복구 속성을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="be5d3-192">Update recovery properties, such as hello VM role size, and hello Azure network tooattach hello virtual machine's network interface cards tooupon failover.</span></span>

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
        DisplayName      : Update hello virtual machine
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



## <a name="step-8-run-a-test-failover"></a><span data-ttu-id="be5d3-193">8단계: 테스트 장애 조치 실행</span><span class="sxs-lookup"><span data-stu-id="be5d3-193">Step 8: Run a test failover</span></span>
1. <span data-ttu-id="be5d3-194">다음과 같이 테스트 장애 조치 작업을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="be5d3-194">Run a test failover job, as follows:</span></span>

        $nw = Get-AzureRmVirtualNetwork -Name "TestFailoverNw" -ResourceGroupName "MyRG" #Specify Azure vnet name and resource group

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -FriendlyName $VMFriendlyName -ProtectionContainer $protectionContainer

        $TFjob = Start-AzureRmSiteRecoveryTestFailoverJob -ProtectionEntity $protectionEntity -Direction PrimaryToRecovery -AzureVMNetworkId $nw.Id
2. <span data-ttu-id="be5d3-195">Azure에서 VM을 만든 hello 테스트를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="be5d3-195">Verify that hello test VM is created in Azure.</span></span> <span data-ttu-id="be5d3-196">(hello 테스트 장애 조치 작업이 중지 됨, Azure의 hello 테스트 VM을 만든 후 합니다.</span><span class="sxs-lookup"><span data-stu-id="be5d3-196">(hello test failover job is suspended, after creating hello test VM in Azure.</span></span> <span data-ttu-id="be5d3-197">hello 작업이 hello 다음 단계에 설명 된 대로 hello 작업을 다시 시작 시 hello 만든 artefacts을 정리 하 여 완료 됩니다.)</span><span class="sxs-lookup"><span data-stu-id="be5d3-197">hello job completes by cleaning up hello created artefacts upon resuming hello job, as illustrated in hello next step.)</span></span>
3. <span data-ttu-id="be5d3-198">테스트 장애 조치을 다음과 같이 전체 hello:</span><span class="sxs-lookup"><span data-stu-id="be5d3-198">Complete hello test failover, as follows:</span></span>

        $TFjob = Resume-AzureRmSiteRecoveryJob -Job $TFjob

## <a name="next-steps"></a><span data-ttu-id="be5d3-199">다음 단계</span><span class="sxs-lookup"><span data-stu-id="be5d3-199">Next Steps</span></span>
<span data-ttu-id="be5d3-200">[자세히 알아보세요](https://msdn.microsoft.com/library/azure/mt637930.aspx) .</span><span class="sxs-lookup"><span data-stu-id="be5d3-200">[Read more](https://msdn.microsoft.com/library/azure/mt637930.aspx) about Azure Site Recovery with Azure Resource Manager PowerShell cmdlets.</span></span>

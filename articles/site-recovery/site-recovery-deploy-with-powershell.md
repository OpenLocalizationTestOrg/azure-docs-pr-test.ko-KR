---
title: "클래식 포털에서 PowerShell을 사용하여 Azure에 Hyper-V VM 복제 | Microsoft Docs"
description: "클래식 포털에서 Site Recovery 및 PowerShell을 사용하여 VMM 클라우드의 Hyper-V 가상 컴퓨터 복제를 자동화합니다."
services: site-recovery
documentationcenter: 
author: bsiva
manager: abhiag
editor: tysonn
ms.assetid: 9011f567-e0b4-4306-951a-b30da19f5db6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: bsiva
ms.openlocfilehash: 581daaaa5cc0cf8be782f834c6bdb3f27ee413fb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="replicate-hyper-v-vms-to-azure-with-powershell-in-the-classic-portal"></a><span data-ttu-id="887e0-103">클래식 포털에서 PowerShell을 사용하여 Azure에 Hyper-V VM 복제</span><span class="sxs-lookup"><span data-stu-id="887e0-103">Replicate Hyper-V VMs to Azure with PowerShell in the classic portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="887e0-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="887e0-104">Azure Portal</span></span>](site-recovery-vmm-to-azure.md)
> * [<span data-ttu-id="887e0-105">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="887e0-105">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [<span data-ttu-id="887e0-106">클래식 포털</span><span class="sxs-lookup"><span data-stu-id="887e0-106">Classic Portal</span></span>](site-recovery-vmm-to-azure-classic.md)
> * [<span data-ttu-id="887e0-107">PowerShell - 클래식</span><span class="sxs-lookup"><span data-stu-id="887e0-107">PowerShell - Classic</span></span>](site-recovery-deploy-with-powershell.md)
>
>

## <a name="overview"></a><span data-ttu-id="887e0-108">개요</span><span class="sxs-lookup"><span data-stu-id="887e0-108">Overview</span></span>
<span data-ttu-id="887e0-109">Azure Site Recovery는 여러 배포 시나리오에서 가상 컴퓨터의 복제, 장애 조치(Failover) 및 복구를 오케스트레이션하여 BCDR(비즈니스 연속성 및 재해 복구) 전략에 기여합니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-109">Azure Site Recovery contributes to your business continuity and disaster recovery (BCDR) strategy by orchestrating replication, failover and recovery of virtual machines in a number of deployment scenarios.</span></span> <span data-ttu-id="887e0-110">배포 시나리오의 전체 목록은 [Azure Site Recovery 개요](site-recovery-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="887e0-110">For a full list of deployment scenarios see the [Azure Site Recovery overview](site-recovery-overview.md).</span></span>

<span data-ttu-id="887e0-111">이 문서에서는 System Center VMM 클라우드의 Hyper-V 가상 컴퓨터를 Azure 저장소로 복제하도록 Azure Site Recovery를 설정할 때 수행해야 하는 일반적인 작업을 PowerShell을 사용하여 자동화하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-111">This article shows you how to use PowerShell to automate common tasks you need to perform when you set up Azure Site Recovery to replicate Hyper-V virtual machines in System Center VMM clouds to Azure storage.</span></span>

<span data-ttu-id="887e0-112">본 문서에는 시나리오에 대한 필수 조건이 포함되어 있으며, 사이트 복구 자격 증명 모음을 설정하고, 원본 VMM 서버에 Azure Site Recovery 공급자를 설치하며, 서버를 자격 증명 모음에 등록하고, Azure 저장소 계정을 추가하며, Hyper-V 호스트 서버에 Azure 복구 서비스 에이전트를 설치하고, 보호된 모든 가상 컴퓨터에 적용되는 VMM 클라우드에 대한 보호 설정을 구성하고, 해당 가상 컴퓨터에 대해 보호를 사용하도록 설정하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-112">The article includes prerequisites for the scenario, and shows you how to set up a Site Recovery vault, install the Azure Site Recovery Provider on the source VMM server, register the server in the vault, add an Azure storage account, install the Azure Recovery Services agent on Hyper-V host servers, configure protection settings for VMM clouds that will be applied to all protected virtual machines, and then enable protection for those virtual machines.</span></span> <span data-ttu-id="887e0-113">끝으로, 장애 조치(Failover)를 테스트하여 모두 예상대로 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-113">Finish up by testing the failover to make sure everything's working as expected.</span></span>

<span data-ttu-id="887e0-114">이 시나리오를 설정하는 동안 문제가 발생할 경우 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)에 문의 사항을 게시하세요.</span><span class="sxs-lookup"><span data-stu-id="887e0-114">If you run into problems setting up this scenario, post your questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

> [!NOTE]
> <span data-ttu-id="887e0-115">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../azure-resource-manager/resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-115">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="887e0-116">이 문서에서는 클래식 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-116">This article covers using the Classic deployment model.</span></span>
>
>

## <a name="before-you-start"></a><span data-ttu-id="887e0-117">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="887e0-117">Before you start</span></span>
<span data-ttu-id="887e0-118">다음 필수 조건이 충족되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-118">Make sure you have these prerequisites in place:</span></span>

### <a name="azure-prerequisites"></a><span data-ttu-id="887e0-119">Azure 필수 조건</span><span class="sxs-lookup"><span data-stu-id="887e0-119">Azure prerequisites</span></span>
* <span data-ttu-id="887e0-120">[Microsoft Azure](https://azure.microsoft.com/) 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-120">You'll need a [Microsoft Azure](https://azure.microsoft.com/) account.</span></span> <span data-ttu-id="887e0-121">[무료 평가판](https://azure.microsoft.com/pricing/free-trial/)으로 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-121">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="887e0-122">복제된 데이터를 저장하려면 Azure 저장소 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-122">You'll need an Azure storage account to store replicated data.</span></span> <span data-ttu-id="887e0-123">계정의 지역에서 복제 기능을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-123">The account needs geo-replication enabled.</span></span> <span data-ttu-id="887e0-124">계정은 Azure Site Recovery 자격 증명 모음과 동일한 지역에 있고 동일한 구독과 연결되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-124">It should be in the same region as the Azure Site Recovery vault and be associated with the same subscription.</span></span> <span data-ttu-id="887e0-125">[Azure 저장소에 대해 자세히 알아보세요](../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="887e0-125">[Learn more about Azure storage](../storage/common/storage-introduction.md).</span></span>
* <span data-ttu-id="887e0-126">보호할 가상 컴퓨터가 [Azure 가상 컴퓨터 필수 조건](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)을 준수하는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-126">You'll need to make sure that virtual machines you want to protect comply with [Azure virtual machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

### <a name="vmm-prerequisites"></a><span data-ttu-id="887e0-127">VMM 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="887e0-127">VMM prerequisites</span></span>
* <span data-ttu-id="887e0-128">System Center 2012 R2에서 실행되는 VMM 서버가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-128">You'll need  VMM server running on System Center 2012 R2.</span></span>
* <span data-ttu-id="887e0-129">보호할 VMM 서버에 클라우드가 하나 이상 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-129">You'll need at least one cloud on the VMM server you want to protect.</span></span> <span data-ttu-id="887e0-130">클라우드에는 다음이 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-130">The cloud should contain:</span></span>
  * <span data-ttu-id="887e0-131">하나 이상의 VMM 호스트 그룹.</span><span class="sxs-lookup"><span data-stu-id="887e0-131">One or more VMM host groups.</span></span>
  * <span data-ttu-id="887e0-132">각 호스트 그룹에 있는 하나 이상의 Hyper-V 호스트 서버 또는 클러스터.</span><span class="sxs-lookup"><span data-stu-id="887e0-132">One or more Hyper-V host servers or clusters in each host group .</span></span>
  * <span data-ttu-id="887e0-133">원본 Hyper-V 서버에 있는 하나 이상의 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="887e0-133">One or more virtual machines on the source Hyper-V server.</span></span>

### <a name="hyper-v-prerequisites"></a><span data-ttu-id="887e0-134">Hyper-V 필수 조건</span><span class="sxs-lookup"><span data-stu-id="887e0-134">Hyper-V prerequisites</span></span>
* <span data-ttu-id="887e0-135">호스트 Hyper-V 서버는 **Windows Server 2012** 이상(Hyper-V 역할 수행) 또는 **Microsoft Hyper-V Server 2012**를 실행하고 최신 업데이트가 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-135">The host Hyper-V servers must be running at least **Windows Server 2012** with Hyper-V role or **Microsoft Hyper-V Server 2012** and have the latest updates installed.</span></span>
* <span data-ttu-id="887e0-136">클러스터에서 Hyper-V를 실행하는 경우 고정 IP 주소 기반 클러스터가 있으면 클러스터 브로커가 자동으로 만들어지지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-136">If you're running Hyper-V in a cluster note that cluster broker isn't created automatically if you have a static IP address-based cluster.</span></span> <span data-ttu-id="887e0-137">클러스터 브로커를 수동으로 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-137">You'll need to configure the cluster broker manually.</span></span> <span data-ttu-id="887e0-138">이렇게 하려면 [서버 관리자] > [장애 조치(Failover) 클러스터 관리자]에서 클러스터에 연결하여 **역할 구성**을 클릭하고 고가용성 마법사의 **역할 선택** 화면에서 **Hyper-V 복제본 Broker**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-138">To do this, in Server Manager > Failover Cluster Manager, connect to the cluster, click **Configure Role** and select **Hyper-V Replica Broker** in the **Select Role** screen of the High Availability wizard.</span></span>
* <span data-ttu-id="887e0-139">보호를 관리할 Hyper-V 호스트 서버 또는 클러스터가 모두 VMM 클라우드에 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-139">Any Hyper-V host server or cluster for which you want to manage protection must be included in a VMM cloud.</span></span>

### <a name="network-mapping-prerequisites"></a><span data-ttu-id="887e0-140">네트워크 매핑 필수 조건</span><span class="sxs-lookup"><span data-stu-id="887e0-140">Network mapping prerequisites</span></span>
<span data-ttu-id="887e0-141">Azure 네트워크에서 가상 컴퓨터를 보호하는 경우 매핑은 원본 VMM 서버의 VM 네트워크와 대상 Azure 네트워크 간을 매핑하여 다음을 가능하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-141">When you protect virtual machines in Azure network mapping maps between VM networks on the source VMM server and target Azure networks to enable the following:</span></span>

* <span data-ttu-id="887e0-142">속해 있는 복구 계획에 관계없이 동일한 네트워크에서 장애 조치(Failover)되는 모든 컴퓨터가 서로 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-142">All machines which fail over on the same network can connect to each other, irrespective of which recovery plan they are in.</span></span>
* <span data-ttu-id="887e0-143">네트워크 게이트웨이가 대상 Azure 네트워크에서 설정된 경우 가상 컴퓨터가 다른 온-프레미스 가상 컴퓨터에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-143">If a network gateway is setup on the target Azure network, virtual machines can connect to other on-premises virtual machines.</span></span>
* <span data-ttu-id="887e0-144">네트워크 매핑을 구성하지 않으면 동일한 복구 계획에서 장애 조치(Failover)되는 가상 컴퓨터만 Azure로의 장애 조치(Failover) 후에 서로 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-144">If you don’t configure network mapping only virtual machines that fail over in the same recovery plan will be able to connect to each other after failover to Azure.</span></span>

<span data-ttu-id="887e0-145">네트워크 매핑을 배포하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-145">If you want to deploy network mapping you'll need the following:</span></span>

* <span data-ttu-id="887e0-146">원본 VMM 서버에서 보호할 가상 컴퓨터가 VM 네트워크에 연결되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-146">The virtual machines you want to protect on the source VMM server should be connected to a VM network.</span></span> <span data-ttu-id="887e0-147">해당 네트워크가 클라우드와 연결된 논리 네트워크에 연결되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-147">That network should be linked to a logical network that is associated with the cloud.</span></span>
* <span data-ttu-id="887e0-148">복제된 가상 컴퓨터가 장애 조치(Failover) 후 연결할 수 있는 Azure 네트워크.</span><span class="sxs-lookup"><span data-stu-id="887e0-148">An Azure network to which replicated virtual machines can connect after failover.</span></span> <span data-ttu-id="887e0-149">이 네트워크는 장애 조치(Failover) 시 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-149">You'll select this network at the time of failover.</span></span> <span data-ttu-id="887e0-150">네트워크는 Azure Site Recovery 구독과 동일한 지역에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-150">The network should be in the same region as your Azure Site Recovery subscription.</span></span>

### <a name="powershell-prerequisites"></a><span data-ttu-id="887e0-151">PowerShell 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="887e0-151">PowerShell prerequisites</span></span>
<span data-ttu-id="887e0-152">Azure PowerShell을 사용할 준비가 되었는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="887e0-152">Make sure you have Azure PowerShell ready to go.</span></span> <span data-ttu-id="887e0-153">이미 PowerShell을 사용하고 있는 경우 버전 0.8.10 이상으로 업그레이드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-153">If you are already using PowerShell, you'll need to upgrade to version 0.8.10 or later.</span></span> <span data-ttu-id="887e0-154">PowerShell 설치에 대한 자세한 내용은 [Azure PowerShell을 설치 및 구성하는 방법](/powershell/azureps-cmdlets-docs)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="887e0-154">For information about setting up PowerShell, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="887e0-155">PowerShell을 설정 및 구성하면 [여기](/powershell/azure/overview)에서 서비스에 사용 가능한 모든 cmdlet을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-155">Once you have set up and configured PowerShell, you can view all of the available cmdlets for the service [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="887e0-156">Azure PowerShell에서 매개 변수 값, 입력, 출력이 일반적으로 처리되는 방법 등 cmdlet을 사용하는 데 도움이 되는 팁을 보려면 [Azure Cmdlet 시작하기](/powershell/azure/get-started-azureps)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="887e0-156">To learn about tips that can help you use the cmdlets, such as how parameter values, inputs, and outputs are typically handled in Azure PowerShell, see [Get Started with Azure Cmdlets](/powershell/azure/get-started-azureps).</span></span>

## <a name="step-1-set-the-subscription"></a><span data-ttu-id="887e0-157">1단계: 구독 설정</span><span class="sxs-lookup"><span data-stu-id="887e0-157">Step 1: Set the subscription</span></span>
<span data-ttu-id="887e0-158">PowerShell에서 다음 cmdlet을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-158">In PowerShell, run these cmdlets:</span></span>

```
$UserName = "<user@live.com>"
$Password = "<password>"
$AzureSubscriptionName = "prod_sub1"

$SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
$Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $securePassword
Add-AzureAccount -Credential $Cred;
$AzureSubscription = Select-AzureSubscription -SubscriptionName $AzureSubscriptionName

```

<span data-ttu-id="887e0-159">“< >” 안의 요소를 자신의 특정 정보로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-159">Replace the elements within the "< >" with your specific information.</span></span>

## <a name="step-2-create-a-site-recovery-vault"></a><span data-ttu-id="887e0-160">2단계: 사이트 복구 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="887e0-160">Step 2: Create a Site Recovery vault</span></span>
<span data-ttu-id="887e0-161">PowerShell에서 “< >” 안의 요소를 자신의 특정 정보로 대체하고 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-161">In PowerShell, replace the elements within the "< >" with your specific information, and run these commands:</span></span>

```

$VaultName = "<testvault123>"
$VaultGeo  = "<Southeast Asia>"
$OutputPathForSettingsFile = "<c:\>"

```


```
New-AzureSiteRecoveryVault -Location $VaultGeo -Name $VaultName;
$vault = Get-AzureSiteRecoveryVault -Name $VaultName;

```

## <a name="step-3-generate-a-vault-registration-key"></a><span data-ttu-id="887e0-162">3단계: 자격 증명 모음 등록 키 생성</span><span class="sxs-lookup"><span data-stu-id="887e0-162">Step 3: Generate a vault registration key</span></span>
<span data-ttu-id="887e0-163">자격 증명 모음에 등록 키를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-163">Generate a registration key in the vault.</span></span> <span data-ttu-id="887e0-164">Azure Site Recovery 공급자를 다운로드하고 VMM 서버에 설치한 후 이 키를 사용하여 VMM 서버를 자격 증명 모음에 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-164">After you download the Azure Site Recovery Provider and install it on the VMM server, you'll use this key to register the VMM server in the vault.</span></span>

1. <span data-ttu-id="887e0-165">자격 증명 모음 설정 파일을 가져오고 컨텍스트를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-165">Get the vault setting file and set the context:</span></span>

   ```

   $VaultName = "<testvault123>"
   $VaultGeo  = "<Southeast Asia>"
   $OutputPathForSettingsFile = "<c:\>"

   $VaultSetingsFile = Get-AzureSiteRecoveryVaultSettingsFile -Location $VaultGeo -Name $VaultName -Path $OutputPathForSettingsFile;

   ```
2. <span data-ttu-id="887e0-166">다음 명령을 실행하여 자격 증명 모음 컨텍스트를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-166">Set the vault context by running the following commands:</span></span>

   ```

   $VaultSettingFilePath = $vaultSetingsFile.FilePath
   $VaultContext = Import-AzureSiteRecoveryVaultSettingsFile -Path $VaultSettingFilePath -ErrorAction Stop

   ```

## <a name="step-4-install-the-azure-site-recovery-provider"></a><span data-ttu-id="887e0-167">4단계: Azure Site Recovery 공급자 설치</span><span class="sxs-lookup"><span data-stu-id="887e0-167">Step 4: Install the Azure Site Recovery Provider</span></span>
1. <span data-ttu-id="887e0-168">VMM 컴퓨터에서 다음 명령을 실행하여 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-168">On the VMM machine, create a directory by running the following command:</span></span>

   ```

   pushd C:\ASR\

   ```
2. <span data-ttu-id="887e0-169">다음 명령을 실행하고 다운로드한 공급자를 사용하여 파일을 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-169">Extract the files using the downloaded provider by running the following command</span></span>

   ```

   AzureSiteRecoveryProvider.exe /x:. /q

   ```
3. <span data-ttu-id="887e0-170">다음 명령을 사용하여 공급자를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-170">Install the provider using the following commands:</span></span>

   ```

   .\SetupDr.exe /i

   ```

   ```

   $installationRegPath = "hklm:\software\Microsoft\Microsoft System Center Virtual Machine Manager Server\DRAdapter"
   do
   {
     $isNotInstalled = $true;
     if(Test-Path $installationRegPath)
     {
         $isNotInstalled = $false;
     }
   }While($isNotInstalled)

   ```

   <span data-ttu-id="887e0-171">설치가 완료될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-171">Wait for the installation to finish.</span></span>
4. <span data-ttu-id="887e0-172">다음 명령을 사용하여 자격 증명 모음에 서버를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-172">Register the server in the vault using the following command:</span></span>

   ```

   $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
   pushd $BinPath
   $encryptionFilePath = "C:\temp\"
   .\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

   ```

## <a name="step-5-create-an-azure-storage-account"></a><span data-ttu-id="887e0-173">5단계: Azure 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="887e0-173">Step 5: Create an Azure storage account</span></span>
<span data-ttu-id="887e0-174">Azure 저장소 계정이 없는 경우 다음 명령을 실행하여 지리적 복제가 활성화된 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-174">If you don't have an Azure storage account, create a geo-replication enabled account by running the following command:</span></span>

```

$StorageAccountName = "teststorageacc1"
$StorageAccountGeo  = "Southeast Asia"

New-AzureStorageAccount -StorageAccountName $StorageAccountName -Label $StorageAccountName -Location $StorageAccountGeo;

```

<span data-ttu-id="887e0-175">저장소 계정은 Azure Site Recovery 서비스와 같은 지역에 있고 같은 구독과 연결되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-175">Note that the storage account must be in the same region as the Azure Site Recovery service, and be associated with the same subscription.</span></span>

## <a name="step-6-install-the-azure-recovery-services-agent"></a><span data-ttu-id="887e0-176">6단계: Azure 복구 서비스 에이전트 설치</span><span class="sxs-lookup"><span data-stu-id="887e0-176">Step 6: Install the Azure Recovery Services Agent</span></span>
<span data-ttu-id="887e0-177">Azure 포털에서 보호할 VMM 클라우드에 있는 각 Hyper-V 호스트 서버에 Azure 복구 서비스 에이전트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-177">From the Azure portal, install the Azure Recovery Services agent on each Hyper-V host server located in the VMM clouds you want to protect.</span></span>

<span data-ttu-id="887e0-178">모든 VMM 호스트에 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-178">Run the following command on all VMM hosts:</span></span>

```

marsagentinstaller.exe /q /nu

```


## <a name="step-7-configure-cloud-protection-settings"></a><span data-ttu-id="887e0-179">7단계: 클라우드 보호 설정 구성</span><span class="sxs-lookup"><span data-stu-id="887e0-179">Step 7: Configure cloud protection settings</span></span>
1. <span data-ttu-id="887e0-180">다음 명령을 실행하여 Azure에 대한 클라우드 보호 프로필을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-180">Create a cloud protection profile to Azure by running the following command:</span></span>

   ```

   $ReplicationFrequencyInSeconds = "300";
   $ProfileResult = New-AzureSiteRecoveryProtectionProfileObject -ReplicationProvider HyperVReplica -RecoveryAzureSubscription $AzureSubscriptionName -RecoveryAzureStorageAccount $StorageAccountName -ReplicationFrequencyInSeconds     $ReplicationFrequencyInSeconds;

   ```
2. <span data-ttu-id="887e0-181">다음 명령을 실행하여 보호 컨테이너를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-181">Get a protection container by running the following commands:</span></span>

   ```

   $PrimaryCloud = "testcloud"
   $protectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $PrimaryCloud;

   ```
3. <span data-ttu-id="887e0-182">클라우드와 보호 컨테이너 연결을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-182">Start the association of the protection container with the cloud:</span></span>

   ```

   $associationJob = Start-AzureSiteRecoveryProtectionProfileAssociationJob -ProtectionProfile $profileResult -PrimaryProtectionContainer $protectionContainer;        

   ```
4. <span data-ttu-id="887e0-183">작업이 완료되면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-183">After the job has finished, run the following command:</span></span>

        $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
        if($job -eq $null -or $job.StateDescription -ne "Completed")
        {
        $isJobLeftForProcessing = $true;
        }


1. <span data-ttu-id="887e0-184">작업에서 처리를 완료하면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-184">After the job has finished processing, run the following command:</span></span>

        Do
        {
        $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
        Write-Host "Job State:{0}, StateDescription:{1}" -f Job.State, $job.StateDescription;
        if($job -eq $null -or $job.StateDescription -ne "Completed")
        {
            $isJobLeftForProcessing = $true;
        }

        if($isJobLeftForProcessing)
        {
            Start-Sleep -Seconds 60
        }
        }While($isJobLeftForProcessing)



<span data-ttu-id="887e0-185">작동 완료 여부를 확인하려면 [작업 모니터](#monitor)의 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-185">To check the completion of the operation, follow the steps in [Monitor Activity](#monitor).</span></span>

## <a name="step-8-configure-network-mapping"></a><span data-ttu-id="887e0-186">8단계: 네트워크 매핑 구성</span><span class="sxs-lookup"><span data-stu-id="887e0-186">Step 8: Configure network mapping</span></span>
<span data-ttu-id="887e0-187">네트워크 매핑을 시작하기 전에 원본 VMM 서버의 가상 컴퓨터가 VM 네트워크에 연결되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-187">Before you begin network mapping verify that virtual machines on the source VMM server are connected to a VM network.</span></span> <span data-ttu-id="887e0-188">또한 Azure 가상 네트워크를 하나 이상 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-188">In addition, create one or more Azure virtual networks.</span></span> <span data-ttu-id="887e0-189">단일 Azure 네트워크에 여러 개의 VM 네트워크를 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-189">Note that multiple VM networks can be mapped to a single Azure network.</span></span>

<span data-ttu-id="887e0-190">대상 네트워크에 여러 서브넷이 있고 이 서브넷 중 하나의 이름이 원본 가상 컴퓨터가 있는 서브넷과 같으면 복제본 가상 컴퓨터가 장애 조치(Failover) 후에 대상 서브넷에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-190">Note that if the target network has multiple subnets and one of those subnets has the same name as subnet on which the source virtual machine is located, then the replica virtual machine will be connected to that target subnet after failover.</span></span> <span data-ttu-id="887e0-191">일치하는 이름을 가진 대상 서브넷이 없으면 가상 컴퓨터가 네트워크의 첫 번째 서브넷에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-191">If there is not a target subnet with a matching name, the virtual machine will be connected to the first subnet in the network.</span></span>

<span data-ttu-id="887e0-192">첫 번째 명령은 현재 Azure Site Recovery 자격 증명 모음의 서버를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-192">The first command gets servers for the current Azure Site Recovery vault.</span></span> <span data-ttu-id="887e0-193">이 명령은 $Servers 어레이 변수에 Microsoft Azure Site Recovery 서버를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-193">The command stores the Microsoft Azure Site Recovery servers in the $Servers array variable.</span></span>

    $Servers = Get-AzureSiteRecoveryServer


<span data-ttu-id="887e0-194">두 번째 명령은 $Servers 어레이의 첫 번째 서버에 대한 사이트 복구 네트워크를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-194">The second command gets the site recovery network for the first server in the $Servers array.</span></span> <span data-ttu-id="887e0-195">이 명령은 $Networks 변수에 네트워크를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-195">The command stores the networks in the $Networks variable.</span></span>

    $Networks = Get-AzureSiteRecoveryNetwork -Server $Servers[0]

<span data-ttu-id="887e0-196">세 번째 명령은 Get-AzureSubscription cmdlet을 사용하여 Azure 구독을 가져온 다음 해당 값을 $Subscriptions 변수에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-196">The third command gets your Azure subscriptions by using the Get-AzureSubscription cmdlet, and then stores that value in the $Subscriptions variable.</span></span>

    $Subscriptions = Get-AzureSubscription



<span data-ttu-id="887e0-197">네 번째 명령은 Get-AzureVNetSite cmdlet을 사용하여 Azure 가상 네트워크를 가져온 다음 해당 값을 $AzureVmNetworks 변수에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-197">The fourth command gets Azure virtual networks by using the Get-AzureVNetSite cmdlet, and then that value in the $AzureVmNetworks variable.</span></span>

    $AzureVmNetworks = Get-AzureVNetSite



<span data-ttu-id="887e0-198">최종 cmdlet은 기본 네트워크와 Azure 가상 컴퓨터 네트워크 사이에 매핑을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-198">The final cmdlet creates a mapping between the primary network and the Azure virtual machine network.</span></span> <span data-ttu-id="887e0-199">cmdlet은 $Networks의 첫 번째 요소로 기본 네트워크를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-199">The cmdlet specifies the primary network as the first element of $Networks.</span></span> <span data-ttu-id="887e0-200">cmdlet은 ID를 사용하여 $AzureVmNetworks의 첫 번째 요소로 가상 컴퓨터 네트워크를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-200">The cmdlet specifies a virtual machine network as the first element of $AzureVmNetworks by using its ID.</span></span> <span data-ttu-id="887e0-201">이 명령에는 Azure 구독 ID가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-201">The command includes your Azure subscription ID.</span></span>

    New-AzureSiteRecoveryNetworkMapping -PrimaryNetwork $Networks[0] -AzureSubscriptionId $Subscriptions[0].SubscriptionId -AzureVMNetworkId $AzureVmNetworks[0].Id


## <a name="step-9-enable-protection-for-virtual-machines"></a><span data-ttu-id="887e0-202">9단계: 가상 컴퓨터의 보호 활성화</span><span class="sxs-lookup"><span data-stu-id="887e0-202">Step 9: Enable protection for virtual machines</span></span>
<span data-ttu-id="887e0-203">서버, 클라우드 및 네트워크가 제대로 구성되었으면 클라우드에서 가상 컴퓨터에 대한 보호를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-203">After servers, clouds, and networks are configured correctly, you can enable protection for virtual machines in the cloud.</span></span> <span data-ttu-id="887e0-204">다음 사항에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="887e0-204">Note the following:</span></span>

<span data-ttu-id="887e0-205">가상 컴퓨터에서 [Azure 가상 컴퓨터 필수 조건](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)을 충족해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-205">Virtual machines must meet [Azure virtual machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

<span data-ttu-id="887e0-206">보호를 사용하도록 설정하려면 가상 컴퓨터에 대해 운영 체제 및 운영 체제 디스크 속성을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-206">To enable protection the operating system and operating system disk properties must be set for the virtual machine.</span></span> <span data-ttu-id="887e0-207">VMM에서 가상 컴퓨터 템플릿을 사용하여 가상 컴퓨터를 만들 때 속성을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-207">When you create a virtual machine in VMM using a virtual machine template you can set the property.</span></span> <span data-ttu-id="887e0-208">가상 컴퓨터 속성의 **일반** 및 **하드웨어 구성** 탭에서 기존 가상 컴퓨터에 대해 이러한 속성을 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-208">You can also set these properties for existing virtual machines on the **General** and **Hardware Configuration** tabs of the virtual machine properties.</span></span> <span data-ttu-id="887e0-209">이러한 속성을 VMM에서 설정하지 않는 경우 Azure Site Recovery 포털에서 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-209">If you don't set these properties in VMM you'll be able to configure them in the Azure Site Recovery portal.</span></span>

1. <span data-ttu-id="887e0-210">보호를 활성화하려면 다음 명령을 실행하여 보호 컨테이너를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-210">To enable protection, run the following command to get the protection container:</span></span>

     <span data-ttu-id="887e0-211">$ProtectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $CloudName</span><span class="sxs-lookup"><span data-stu-id="887e0-211">$ProtectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $CloudName</span></span>
2. <span data-ttu-id="887e0-212">다음 명령을 실행하여 VM(보호 엔터티)을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-212">Get the protection entity (VM) by running the following command:</span></span>

        $protectionEntity = Get-AzureSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer



1. <span data-ttu-id="887e0-213">다음 명령을 실행하여 VM에 DR을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-213">Enable the DR for the VM by running the following command:</span></span>

        $jobResult = Set-AzureSiteRecoveryProtectionEntity -ProtectionEntity $protectionEntity     -Protection Enable -Force



## <a name="test-your-deployment"></a><span data-ttu-id="887e0-214">배포 테스트</span><span class="sxs-lookup"><span data-stu-id="887e0-214">Test your deployment</span></span>
<span data-ttu-id="887e0-215">배포를 테스트하려면 단일 가상 컴퓨터에 대한 테스트 장애 조치(Failover)를 실행하거나, 여러 개의 가상 컴퓨터로 구성된 복구 계획을 만들고 이 계획에 대한 테스트 장애 조치(Failover)를 실행하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-215">To test your deployment you can run a test failover for a single virtual machine, or create a recovery plan consisting of multiple virtual machines and run a test failover for the plan.</span></span> <span data-ttu-id="887e0-216">테스트 장애 조치(Failover)에서는 격리된 네트워크에서 장애 조치(Failover) 및 복구 메커니즘을 시뮬레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-216">Test failover simulates your failover and recovery mechanism in an isolated network.</span></span> <span data-ttu-id="887e0-217">다음 사항에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="887e0-217">Note that:</span></span>

* <span data-ttu-id="887e0-218">장애 조치(Failover) 후에 원격 데스크탑을 사용하여 Azure의 가상 컴퓨터에 연결하려면 가상 컴퓨터에서 원격 데스크탑 연결을 사용하도록 설정하고 나서 테스트 장애 조치(Failover)를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-218">If you want to connect to the virtual machine in Azure using Remote Desktop after the failover, enable Remote Desktop Connection on the virtual machine before you run the test failover.</span></span>
* <span data-ttu-id="887e0-219">장애 조치(Failover) 후에 공개 IP 주소를 사용하여 원격 데스크탑을 통해 Azure의 가상 컴퓨터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-219">After failover, you'll use a public IP address to connect to the virtual machine in Azure using Remote Desktop.</span></span> <span data-ttu-id="887e0-220">이 작업을 하려면 공개 주소를 사용하여 가상 컴퓨터에 연결하지 못하도록 차단하는 도메인 정책이 없어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-220">If you want to do this, ensure you don't have any domain policies that prevent you from connecting to a virtual machine using a public address.</span></span>

<span data-ttu-id="887e0-221">작동 완료 여부를 확인하려면 [작업 모니터](#monitor)의 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-221">To check the completion of the operation, follow the steps in [Monitor Activity](#monitor).</span></span>

### <a name="create-a-recovery-plan"></a><span data-ttu-id="887e0-222">복구 계획 만들기</span><span class="sxs-lookup"><span data-stu-id="887e0-222">Create a recovery plan</span></span>
1. <span data-ttu-id="887e0-223">아래 데이터를 사용하여 복구 계획의 템플릿으로 .xml 파일을 만든 다음 "C:\RPTemplatePath.xml"로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-223">Create an .xml file as a template for your recovery plan using the data below, and then save it as "C:\RPTemplatePath.xml".</span></span>
2. <span data-ttu-id="887e0-224">RecoveryPlan node Id, Name, PrimaryServerId, SecondaryServerId를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-224">Change the RecoveryPlan node Id, Name, PrimaryServerId, and SecondaryServerId.</span></span>
3. <span data-ttu-id="887e0-225">ProtectionEntity 노드 PrimaryProtectionEntityId(VMM의 vmid)를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-225">Change the ProtectionEntity node PrimaryProtectionEntityId (vmid from VMM).</span></span>
4. <span data-ttu-id="887e0-226">ProtectionEntity 노드를 추가하여 VM을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-226">You can add more VMs by adding more ProtectionEntity nodes.</span></span>

        <#
        <?xml version="1.0" encoding="utf-16"?>
        <RecoveryPlan Id="d0323b26-5be2-471b-addc-0a8742796610" Name="rp-test"     PrimaryServerId="9350a530-d5af-435b-9f2b-b941b5d9fcd5"     SecondaryServerId="21a9403c-6ec1-44f2-b744-b4e50b792387" Description=""     Version="V2014_07">
          <Actions />
          <ActionGroups>
            <ShutdownAllActionGroup Id="ShutdownAllActionGroup">
              <PreActionSequence />
              <PostActionSequence />
            </ShutdownAllActionGroup>
            <FailoverAllActionGroup Id="FailoverAllActionGroup">
              <PreActionSequence />
              <PostActionSequence />
            </FailoverAllActionGroup>
            <BootActionGroup Id="DefaultActionGroup">
              <PreActionSequence />
              <PostActionSequence />
              <ProtectionEntity PrimaryProtectionEntityId="d4c8ce92-a613-4c63-9b03-    cf163cc36ef8" />
            </BootActionGroup>
          </ActionGroups>
          <ActionGroupSequence>
            <ActionGroup Id="ShutdownAllActionGroup" ActionId="ShutdownAllActionGroup"     Before="FailoverAllActionGroup" />
            <ActionGroup Id="FailoverAllActionGroup" ActionId="FailoverAllActionGroup"     After="ShutdownAllActionGroup" Before="DefaultActionGroup" />
            <ActionGroup Id="DefaultActionGroup" ActionId="DefaultActionGroup" After="FailoverAllActionGroup"/>
          </ActionGroupSequence>
        </RecoveryPlan>
        #>



1. <span data-ttu-id="887e0-227">템플릿에 데이터를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-227">Fill in the data in the template:</span></span>

        $TemplatePath = "C:\RPTemplatePath.xml";



1. <span data-ttu-id="887e0-228">RecoveryPlan 만들기:</span><span class="sxs-lookup"><span data-stu-id="887e0-228">Create the RecoveryPlan:</span></span>

        $RPCreationJob = New-AzureSiteRecoveryRecoveryPlan -File $TemplatePath -WaitForCompletion;

### <a name="run-a-test-failover"></a><span data-ttu-id="887e0-229">테스트 장애 조치(Failover) 실행</span><span class="sxs-lookup"><span data-stu-id="887e0-229">Run a test failover</span></span>
1. <span data-ttu-id="887e0-230">다음 명령을 실행하여 RecoveryPlan 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-230">Get the RecoveryPlan object by running the following command:</span></span>

     <span data-ttu-id="887e0-231">$RPObject = Get-AzureSiteRecoveryRecoveryPlan -Name $RPName;</span><span class="sxs-lookup"><span data-stu-id="887e0-231">$RPObject = Get-AzureSiteRecoveryRecoveryPlan -Name $RPName;</span></span>
2. <span data-ttu-id="887e0-232">다음 명령을 실행하여 테스트 장애 조치(Failover)를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-232">Start the test failover by running the following command:</span></span>

        $jobIDResult = Start-AzureSiteRecoveryTestFailoverJob -RecoveryPlan $RPObject -Direction PrimaryToRecovery;


## <span data-ttu-id="887e0-233"><a name=monitor></a> 작업 모니터</span><span class="sxs-lookup"><span data-stu-id="887e0-233"><a name=monitor></a> Monitor Activity</span></span>
<span data-ttu-id="887e0-234">다음 명령을 사용하여 작업을 모니터합니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-234">Use the following commands to monitor the activity.</span></span> <span data-ttu-id="887e0-235">처리가 완료될 때까지 기다린 후 다음 작업을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="887e0-235">Note that you have to wait in between jobs for the processing to finish.</span></span>

    Do
    {
            $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
            Write-Host "Job State:{0}, StateDescription:{1}" -f Job.State, $job.StateDescription;
            if($job -eq $null -or $job.StateDescription -ne "Completed")
            {
                $isJobLeftForProcessing = $true;
            }

        if($isJobLeftForProcessing)
            {
                Start-Sleep -Seconds 60
            }
    }While($isJobLeftForProcessing)



## <a name="next-steps"></a><span data-ttu-id="887e0-236">다음 단계</span><span class="sxs-lookup"><span data-stu-id="887e0-236">Next steps</span></span>
<span data-ttu-id="887e0-237">[자세히 알아보세요](/powershell/azure/overview) .</span><span class="sxs-lookup"><span data-stu-id="887e0-237">[Read more](/powershell/azure/overview) about Azure Site Recovery PowerShell cmdlets.</span></span> <span data-ttu-id="887e0-238"></a></span><span class="sxs-lookup"><span data-stu-id="887e0-238"></a>.</span></span>

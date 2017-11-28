---
title: "Hyper-V VM을 Azure에 복제 | Microsoft Docs"
description: "온-프레미스 Hyper-V VM을 Azure에 복제, 장애 조치(failover) 및 복구하는 작업을 조정하는 방법 설명"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 1777e0eb-accb-42b5-a747-11272e131a52
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 04/05/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: hyper-v-site-walkthrough-overview
ms.openlocfilehash: 8a2ea92759a777b1178fbfe8084a97eec931f709
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-hyper-v-virtual-machines-without-vmm-to-azure-using-azure-site-recovery-with-the-azure-portal"></a><span data-ttu-id="b2e02-103">Azure Portal에서 Azure Site Recovery를 사용하여 Hyper-V 가상 컴퓨터(VMM 제외)를 Azure에 복제</span><span class="sxs-lookup"><span data-stu-id="b2e02-103">Replicate Hyper-V virtual machines (without VMM) to Azure using Azure Site Recovery with the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="b2e02-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="b2e02-104">Azure portal</span></span>](site-recovery-hyper-v-site-to-azure.md)
> * [<span data-ttu-id="b2e02-105">Azure 클래식</span><span class="sxs-lookup"><span data-stu-id="b2e02-105">Azure classic</span></span>](site-recovery-hyper-v-site-to-azure-classic.md)
> * [<span data-ttu-id="b2e02-106">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b2e02-106">PowerShell - Resource Manager</span></span>](site-recovery-deploy-with-powershell-resource-manager.md)
>
>

<span data-ttu-id="b2e02-107">이 문서에서는 Azure Portal에서 [Azure Site Recovery](site-recovery-overview.md)를 사용하여 온-프레미스 Hyper-V 가상 컴퓨터를 Azure에 복제하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-107">This article describes how to replicate on-premises Hyper-V virtual machines to Azure, using [Azure Site Recovery](site-recovery-overview.md) in the Azure portal.</span></span> <span data-ttu-id="b2e02-108">이 배포에서는 Hyper-V VM이 System Center VMM(Virtual Machine Manager)을 통해 관리되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-108">In this deployment Hyper-V VMs aren't managed by System Center Virtual Machine Manager (VMM).</span></span>

<span data-ttu-id="b2e02-109">이 문서를 읽은 후에는 하단에서 의견을 게시하거나 [Azure Recovery Services 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)에서 기술적인 질문을 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-109">After reading this article, post any comments at the bottom, or ask technical questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

<span data-ttu-id="b2e02-110">컴퓨터를 Azure로 마이그레이션하려면(장애 복구(failback) 없이) [이 문서](site-recovery-migrate-to-azure.md)에서 자세한 방법을 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="b2e02-110">If you want to migrate machines to Azure (without failback), learn more in [this article](site-recovery-migrate-to-azure.md).</span></span>



## <a name="deployment-steps"></a><span data-ttu-id="b2e02-111">배포 단계</span><span class="sxs-lookup"><span data-stu-id="b2e02-111">Deployment steps</span></span>

<span data-ttu-id="b2e02-112">문서에 따라 다음 배포 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-112">Follow the article to complete these deployment steps:</span></span>

1. <span data-ttu-id="b2e02-113">이 배포에 대한 아키텍처를 [알아봅니다](site-recovery-components.md#hyper-v-to-azure).</span><span class="sxs-lookup"><span data-stu-id="b2e02-113">[Learn more](site-recovery-components.md#hyper-v-to-azure) about the architecture for this deployment.</span></span> <span data-ttu-id="b2e02-114">또한 Site Recovery에서 Hyper-V 복제가 작동하는 방식을 [알아봅니다](site-recovery-hyper-v-azure-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="b2e02-114">In addition, [learn about](site-recovery-hyper-v-azure-architecture.md) how Hyper-V replication works in Site Recovery.</span></span>
2. <span data-ttu-id="b2e02-115">필수 조건 및 제한 사항을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-115">Verify prerequisites and limitations.</span></span>
3. <span data-ttu-id="b2e02-116">Azure 네트워크 및 저장소 계정을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-116">Set up Azure network and storage accounts.</span></span>
4. <span data-ttu-id="b2e02-117">Hyper-V 호스트를 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-117">Prepare Hyper-V hosts.</span></span>
5. <span data-ttu-id="b2e02-118">Recovery Services 자격 증명 모음을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-118">Create a Recovery Services vault.</span></span> <span data-ttu-id="b2e02-119">자격 증명 모음은 구성 설정을 포함하며 복제를 오케스트레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-119">The vault contains configuration settings, and orchestrates replication.</span></span>
6. <span data-ttu-id="b2e02-120">원본 설정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-120">Specify source settings.</span></span> <span data-ttu-id="b2e02-121">Hyper-V 호스트를 포함하는 Hyper-V 사이트를 만들고, 해당 사이트를 자격 증명 모음에 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-121">Create a Hyper-V site that contains the Hyper-V hosts, and register the site in the vault.</span></span> <span data-ttu-id="b2e02-122">Hyper-V 호스트에 Azure Site Recovery 공급자와 Recovery Services 에이전트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-122">Install the Azure Site Recovery Provider, and the Microsoft Recovery Services agent, on the Hyper-V hosts.</span></span>
7. <span data-ttu-id="b2e02-123">대상 및 복제 설정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-123">Set up target and replication settings.</span></span>
8. <span data-ttu-id="b2e02-124">VM에 대해 복제를 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-124">Enable replication for the VMs.</span></span>
9. <span data-ttu-id="b2e02-125">모든 것이 예상대로 작동하는지 확인할 수 있도록 테스트 장애 조치를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-125">Run a test failover to make sure everything's working as expected.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="b2e02-126">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b2e02-126">Prerequisites</span></span>


<span data-ttu-id="b2e02-127">**요구 사항**</span><span class="sxs-lookup"><span data-stu-id="b2e02-127">**Requirement**</span></span> | <span data-ttu-id="b2e02-128">**세부 정보**</span><span class="sxs-lookup"><span data-stu-id="b2e02-128">**Details**</span></span> |
--- | --- |
<span data-ttu-id="b2e02-129">**Azure**</span><span class="sxs-lookup"><span data-stu-id="b2e02-129">**Azure**</span></span> | <span data-ttu-id="b2e02-130">[Azure 요구 사항](site-recovery-prereq.md#azure-requirements)에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-130">Learn about [Azure requirements](site-recovery-prereq.md#azure-requirements).</span></span>
<span data-ttu-id="b2e02-131">**온-프레미스 서버**</span><span class="sxs-lookup"><span data-stu-id="b2e02-131">**On-premises servers**</span></span> | <span data-ttu-id="b2e02-132">온-프레미스 Hyper-V 호스트에 대한 요구 사항을 [자세히 알아봅니다](site-recovery-prereq.md#disaster-recovery-of-hyper-v-virtual-machines-to-azure-no-virtual-machine-manager).</span><span class="sxs-lookup"><span data-stu-id="b2e02-132">[Learn more](site-recovery-prereq.md#disaster-recovery-of-hyper-v-virtual-machines-to-azure-no-virtual-machine-manager) about requirements for the on-premises Hyper-V hosts.</span></span>
<span data-ttu-id="b2e02-133">**온-프레미스 Hyper-V VM**</span><span class="sxs-lookup"><span data-stu-id="b2e02-133">**On-premises Hyper-V VMs**</span></span> | <span data-ttu-id="b2e02-134">복제하려는 VM은 [지원되는 운영 체제](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)를 실행하고 [Azure 필수 조건](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-134">VMs you want to replicate should be running a [supported operating system](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions), and conform with [Azure prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>
<span data-ttu-id="b2e02-135">**Azure URL**</span><span class="sxs-lookup"><span data-stu-id="b2e02-135">**Azure URLs**</span></span> | <span data-ttu-id="b2e02-136">Hyper-V가 다음 URL에 액세스할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-136">Hyper-V hosts need access to these URLs:</span></span><br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> <span data-ttu-id="b2e02-137">IP 주소 기반 방화벽 규칙이 있는 경우 해당 규칙이 Azure와의 통신을 허용하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-137">If you have IP address-based firewall rules, ensure they allow communication to Azure.</span></span><br/></br> <span data-ttu-id="b2e02-138">[Azure 데이터 센터 IP 범위](https://www.microsoft.com/download/confirmation.aspx?id=41653) 및 HTTPS(443) 포트를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-138">Allow the [Azure Datacenter IP Ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653), and the HTTPS (443) port.</span></span><br/></br> <span data-ttu-id="b2e02-139">구독하는 Azure 지역과 미국 서부에 해당하는 IP 주소 범위를 허용하세요(Access Control 및 ID 관리에 사용됨).</span><span class="sxs-lookup"><span data-stu-id="b2e02-139">Allow IP address ranges for the Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>



## <a name="prepare-for-deployment"></a><span data-ttu-id="b2e02-140">배포 준비</span><span class="sxs-lookup"><span data-stu-id="b2e02-140">Prepare for deployment</span></span>

<span data-ttu-id="b2e02-141">배포를 준비하기 위해 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-141">To prepare for deployment you need to:</span></span>

1. <span data-ttu-id="b2e02-142">[Azure 네트워크를 설정](#set-up-an-azure-network) 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-142">[Set up an Azure network](#set-up-an-azure-network) in which Azure VMs will be located when they're created after failover.</span></span>
2. <span data-ttu-id="b2e02-143">[Azure 저장소 계정을 설정](#set-up-an-azure-storage-account) 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-143">[Set up an Azure storage account](#set-up-an-azure-storage-account) for replicated data.</span></span>
3. <span data-ttu-id="b2e02-144">[Hyper-v 호스트를 준비](#prepare-the-hyper-v-hosts) 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-144">[Prepare the Hyper-V hosts](#prepare-the-hyper-v-hosts) to ensure they can access the required URLs.</span></span>

### <a name="set-up-an-azure-network"></a><span data-ttu-id="b2e02-145">Azure 네트워크를 설정합니다</span><span class="sxs-lookup"><span data-stu-id="b2e02-145">Set up an Azure network</span></span>

<span data-ttu-id="b2e02-146">Azure 네트워크 설정</span><span class="sxs-lookup"><span data-stu-id="b2e02-146">Set up an Azure network.</span></span> <span data-ttu-id="b2e02-147">이는 장애 조치(failover) 후 생성된 Azure VM이 네트워크에 연결될 수 있게 하기 위해 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-147">You’ll need this so that the Azure VMs created after failover are connected to a network.</span></span>

* <span data-ttu-id="b2e02-148">네트워크가 Recovery Services 자격 증명 모음과 같은 지역에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-148">The network should be in the same region as the Recovery Services vault.</span></span>
* <span data-ttu-id="b2e02-149">장애 조치(failover)된 Azure VM에 사용하려는 리소스 모델에 따라 [Resource Manager 모드](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) 또는 [클래식 모드](../virtual-network/virtual-networks-create-vnet-classic-pportal.md)에서 Azure 네트워크를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-149">Depending on the resource model you want to use for failed over Azure VMs, you set up the Azure network in [Resource Manager mode](../virtual-network/virtual-networks-create-vnet-arm-pportal.md), or [classic mode](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).</span></span>
* <span data-ttu-id="b2e02-150">시작하기 전에 네트워크를 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-150">We recommend you set up a network before you begin.</span></span> <span data-ttu-id="b2e02-151">그렇지 않으면 Site Recovery를 배포하는 동안 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-151">If you don't, you need to do it during Site Recovery deployment.</span></span>
- <span data-ttu-id="b2e02-152">Site Recovery에 사용되는 저장소 계정은 같은 구독 내에서 또는 서로 다른 구독 간에 [이동](../azure-resource-manager/resource-group-move-resources.md)할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-152">Storage accounts used by Site Recovery can't be [moved](../azure-resource-manager/resource-group-move-resources.md) within the same, or across different, subscriptions.</span></span>


### <a name="set-up-an-azure-storage-account"></a><span data-ttu-id="b2e02-153">Azure 저장소 계정을 설정</span><span class="sxs-lookup"><span data-stu-id="b2e02-153">Set up an Azure storage account</span></span>

- <span data-ttu-id="b2e02-154">Azure로 복제된 데이터를 계속 유지하려면 표준/프리미엄 Azure 저장소 계정이 필요합니다.[Premium Storage](../storage/storage-premium-storage.md)는 IO를 많이 사용하는 워크로드를 호스트하기 위해 일관된 IO 고성능과 짧은 대기 시간이 요구되는 가상 컴퓨터에 일반적으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-154">You need a standard/premium Azure storage account to hold data replicated to Azure.[Premium storage](../storage/storage-premium-storage.md) is typically used for virtual machines that need a consistently high IO performance, and low latency to host IO intensive workloads.</span></span>
- <span data-ttu-id="b2e02-155">프리미엄 계정을 사용하여 복제된 데이터를 저장하려는 경우 온-프레미스 데이터에 대한 지속적인 변화를 캡처하는 복제 로그를 저장하는 표준 저장소 계정이 필요할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-155">If you want to use a premium account to store replicated data, you also need a standard storage account to store replication logs that capture ongoing changes to on-premises data.</span></span>
- <span data-ttu-id="b2e02-156">장애 조치(failover)된 Azure VM에 사용하려는 리소스 모델에 따라 [Resource Manager 모드](../storage/storage-create-storage-account.md) 또는 [클래식 모드](../storage/storage-create-storage-account-classic-portal.md)에서 계정을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-156">Depending on the resource model you want to use for failed over Azure VMs, you set up an account in [Resource Manager mode](../storage/storage-create-storage-account.md), or [classic mode](../storage/storage-create-storage-account-classic-portal.md).</span></span>
- <span data-ttu-id="b2e02-157">시작하기 전에 저장소 계정을 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-157">We recommend that you set up a storage account before you begin.</span></span> <span data-ttu-id="b2e02-158">그렇지 않으면 Site Recovery를 배포하는 동안 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-158">If you don't you need to do it during Site Recovery deployment.</span></span> <span data-ttu-id="b2e02-159">계정은 Recovery Services 자격 증명 모음과 동일한 지역에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-159">The accounts must be in the same region as the Recovery Services vault.</span></span>
- <span data-ttu-id="b2e02-160">Site Recovery에 사용되는 저장소 계정은 동일한 구독 내의 리소스 그룹 간이나 서로 다른 구독 간에 이동할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-160">You can't move storage accounts used by Site Recovery across resource groups within the same subscription, or across different subscriptions.</span></span>


### <a name="prepare-the-hyper-v-hosts"></a><span data-ttu-id="b2e02-161">Hyper-v 호스트를 준비</span><span class="sxs-lookup"><span data-stu-id="b2e02-161">Prepare the Hyper-V hosts</span></span>

* <span data-ttu-id="b2e02-162">Hyper-V 호스트가 [필수 구성 요소](site-recovery-prereq.md#disaster-recovery-of-hyper-v-virtual-machines-to-azure-no-virtual-machine-manager)를 충족하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-162">Make sure that the Hyper-V hosts meet the [prerequisites](site-recovery-prereq.md#disaster-recovery-of-hyper-v-virtual-machines-to-azure-no-virtual-machine-manager).</span></span>
- <span data-ttu-id="b2e02-163">호스트가 필요한 URL에 액세스할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-163">Make sure that the hosts can access the required URLs.</span></span>


## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="b2e02-164">복구 서비스 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="b2e02-164">Create a Recovery Services vault</span></span>
1. <span data-ttu-id="b2e02-165">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-165">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b2e02-166">**새로 만들기** > **모니터링 + 관리** > **Backup 및 Site Recovery(OMS)**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-166">Click **New** > **Monitoring + Management** > **Backup and Site Recovery (OMS)**.</span></span>  

    ![새 자격 증명 모음](./media/site-recovery-hyper-v-site-to-azure/new-vault.png)

3. <span data-ttu-id="b2e02-168">**이름**에 자격 증명 모음을 식별하기 위한 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-168">In **Name**, specify a friendly name to identify the vault.</span></span> <span data-ttu-id="b2e02-169">구독이 두 개 이상인 경우 그중에서 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-169">If you have more than one subscription, select one of them.</span></span>

4. <span data-ttu-id="b2e02-170">[새 리소스 그룹을 만들거나](../azure-resource-manager/resource-group-template-deploy-portal.md) 기존 리소스 그룹을 선택하고 Azure 지역을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-170">[Create a new resource group](../azure-resource-manager/resource-group-template-deploy-portal.md) or select an existing one, and specify an Azure region.</span></span> <span data-ttu-id="b2e02-171">이 지역에 컴퓨터가 복제됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-171">Machines will be replicated to this region.</span></span> <span data-ttu-id="b2e02-172">지원되는 하위 지역을 확인하려면 [Azure Site Recovery 가격 정보](https://azure.microsoft.com/pricing/details/site-recovery/)에서 지리적 가용성을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b2e02-172">To check supported regions, see Geographic Availability in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>

5. <span data-ttu-id="b2e02-173">대시보드에서 자격 증명 모음에 빠르게 액세스하려면 **대시보드에 고정**을 클릭하고 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-173">If you want to quickly access the vault from the Dashboard, click **Pin to dashboard**, and then click **Create**.</span></span>

    ![새 자격 증명 모음](./media/site-recovery-hyper-v-site-to-azure/new-vault-settings.png)

<span data-ttu-id="b2e02-175">새 자격 증명 모음은 **대시보드** > **모든 리소스** 목록과 주 **Recovery Services 자격 증명 모음** 블레이드에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-175">The new vault appears in the **Dashboard** > **All resources** list, and on the main **Recovery Services vaults** blade.</span></span>



## <a name="select-the-protection-goal"></a><span data-ttu-id="b2e02-176">보호 목표 선택</span><span class="sxs-lookup"><span data-stu-id="b2e02-176">Select the protection goal</span></span>

<span data-ttu-id="b2e02-177">복제할 대상과 복제할 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-177">Select what you want to replicate, and where you want to replicate to.</span></span>

1. <span data-ttu-id="b2e02-178">**Recovery Services 자격 증명 모음**에서 자격 증명 모음을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-178">In the **Recovery Services vaults**, select the vault.</span></span>
2. <span data-ttu-id="b2e02-179">**시작**에서 **Site Recovery** > **인프라 준비** > **보호 목표**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-179">In **Getting Started**, click **Site Recovery** > **Prepare Infrastructure** > **Protection goal**.</span></span>

    ![목표 선택](./media/site-recovery-hyper-v-site-to-azure/choose-goals.png)
3. <span data-ttu-id="b2e02-181">**보호 목표**에서 **Azure에**를 선택하고 **예, Hyper-V 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-181">In **Protection goal**, select **To Azure**, and select **Yes, with Hyper-V**.</span></span> <span data-ttu-id="b2e02-182">**아니요** 를 선택하여 VMM을 사용 중이지 않음을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-182">Select **No** to confirm you're not using VMM.</span></span> <span data-ttu-id="b2e02-183">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-183">Then click **OK**.</span></span>

    ![목표 선택](./media/site-recovery-hyper-v-site-to-azure/choose-goals2.png)

## <a name="set-up-the-source-environment"></a><span data-ttu-id="b2e02-185">원본 환경 설정</span><span class="sxs-lookup"><span data-stu-id="b2e02-185">Set up the source environment</span></span>

<span data-ttu-id="b2e02-186">Hyper-V 사이트를 설정하고, Hyper-V 호스트에 Azure Site Recovery 공급자와 Azure Recovery Services 에이전트를 설치하고, 자격 증명 모음에 사이트를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-186">Set up the Hyper-V site, install the Azure Site Recovery Provider and the Azure Recovery Services agent on Hyper-V hosts, and register the site in the vault.</span></span>

1. <span data-ttu-id="b2e02-187">**인프라 준비**에서 **원본**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-187">In **Prepare Infrastructure**, click **Source**.</span></span> <span data-ttu-id="b2e02-188">Hyper-V 호스트 또는 클러스터의 컨테이너로 새 Hyper-V 사이트를 추가하려면 **+Hyper-V 사이트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-188">To add a new Hyper-V site as a container for your Hyper-V hosts or clusters, click **+Hyper-V Site**.</span></span>

    ![원본 설정](./media/site-recovery-hyper-v-site-to-azure/set-source1.png)
2. <span data-ttu-id="b2e02-190">**Hyper-V 사이트 만들기**에서 사이트의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-190">In **Create Hyper-V site**, specify a name for the site.</span></span> <span data-ttu-id="b2e02-191">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-191">Then click **OK**.</span></span> <span data-ttu-id="b2e02-192">앞에서 만든 사이트를 선택하고 **+Hyper-V 서버**를 클릭하여 사이트에 서버를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-192">Now, select the site you created, and click **+Hyper-V Server** to add a server to the site.</span></span>

    ![원본 설정](./media/site-recovery-hyper-v-site-to-azure/set-source2.png)

3. <span data-ttu-id="b2e02-194">**서버 추가** > **서버 형식**에 **Hyper-V 서버**가 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-194">In **Add Server** > **Server type**, check that **Hyper-V server** is displayed.</span></span>

    - <span data-ttu-id="b2e02-195">추가하려는 Hyper-V 서버가 [필수 구성 요소](#on-premises-prerequisites)를 충족하며 지정된 URL에 액세스할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-195">Make sure that the Hyper-V server you want to add complies with the [prerequisites](#on-premises-prerequisites), and is able to access the specified URLs.</span></span>
    - <span data-ttu-id="b2e02-196">Azure Site Recovery 공급자 설치 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-196">Download the Azure Site Recovery Provider installation file.</span></span> <span data-ttu-id="b2e02-197">이 파일을 실행하여 공급자와 Recovery Services 에이전트를 각 Hyper-V 호스트에 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-197">You run this file to install the Provider and the Recovery Services agent on each Hyper-V host.</span></span>

    ![원본 설정](./media/site-recovery-hyper-v-site-to-azure/set-source3.png)


## <a name="install-the-provider-and-agent"></a><span data-ttu-id="b2e02-199">공급자 및 에이전트를 설치</span><span class="sxs-lookup"><span data-stu-id="b2e02-199">Install the Provider and agent</span></span>

1. <span data-ttu-id="b2e02-200">Hyper-V 사이트를 추가할 각 호스트에서 공급자 설치 파일을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-200">Run the Provider setup file on each host you added to the Hyper-V site.</span></span> <span data-ttu-id="b2e02-201">Hyper-V 클러스터에 설치하는 경우 각 클러스터 노드에서 설치 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-201">If you're installing on a Hyper-V cluster, run setup on each cluster node.</span></span> <span data-ttu-id="b2e02-202">각 Hyper-V 클러스터 노드를 설치하고 등록하면 노드 간 마이그레이션에서도 VM이 안전하게 보호됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-202">Installing and registering each Hyper-V cluster node ensures that VMs are protected, even if they migrate across nodes.</span></span>
2. <span data-ttu-id="b2e02-203">Microsoft Update 정책에 따라 공급자 업데이트가 설치되도록 **Microsoft Update**에서 업데이트를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-203">In **Microsoft Update**, you can opt in for updates so that Provider updates are installed in accordance with your Microsoft Update policy.</span></span>
3. <span data-ttu-id="b2e02-204">**설치**에서 기본 공급자 설치 위치를 수락하거나 수정하고 **설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-204">In **Installation**, accept or modify the default Provider installation location and click **Install**.</span></span>
4. <span data-ttu-id="b2e02-205">**자격 증명 모음 설정**에서 **찾아보기**를 클릭하고 다운로드한 자격 증명 모음 키 파일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-205">In **Vault Settings**, click **Browse** to select the vault key file that you downloaded.</span></span> <span data-ttu-id="b2e02-206">Azure Site Recovery 구독, 자격 증명 모음 이름 및 Hyper-V 서버가 속한 Hyper-V 사이트를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-206">Specify the Azure Site Recovery subscription, the vault name, and the Hyper-V site to which the Hyper-V server belongs.</span></span>

    ![서버 등록](./media/site-recovery-hyper-v-site-to-azure/provider3.png)

5. <span data-ttu-id="b2e02-208">**프록시 설정**에서, Hyper-V 호스트에서 실행 중인 공급자가 인터넷을 통해 Azure Site Recovery에 연결하는 방법을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-208">In **Proxy Settings**, specify how the Provider running on Hyper-V hosts connects to Azure Site Recovery over the internet.</span></span>

    * <span data-ttu-id="b2e02-209">공급자를 직접 연결하려면 **프록시 없이 Azure Site Recovery에 직접 연결**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-209">If you want the Provider to connect directly select **Connect directly to Azure Site Recovery without a proxy**.</span></span>
    * <span data-ttu-id="b2e02-210">기존 프록시에 인증이 필요하거나 공급자 연결에 사용자 지정 프록시를 사용하려면 **프록시 서버를 사용하여 Azure Site Recovery에 연결**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-210">If your existing proxy requires authentication, or you want to use a custom proxy for the Provider connection, select **Connect to Azure Site Recovery using a proxy server**.</span></span>
    * <span data-ttu-id="b2e02-211">프록시를 사용하는 경우:</span><span class="sxs-lookup"><span data-stu-id="b2e02-211">If you use a proxy:</span></span>
        - <span data-ttu-id="b2e02-212">주소, 포트 및 자격 증명을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-212">Specify the address, port, and credentials</span></span>
        - <span data-ttu-id="b2e02-213">[필수 구성 요소](#prerequisites)에 설명된 URL이 프록시를 통과할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-213">Make sure the URLs described in the [prerequisites](#prerequisites) are allowed through the proxy.</span></span>

    ![인터넷](./media/site-recovery-hyper-v-site-to-azure/provider7.PNG)

6. <span data-ttu-id="b2e02-215">설치가 완료되면 **등록**을 클릭하여 자격 증명 모음에 서버를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-215">After installation finishes, click **Register** to register the server in the vault.</span></span>

    ![설치 위치](./media/site-recovery-hyper-v-site-to-azure/provider2.png)

7. <span data-ttu-id="b2e02-217">등록이 완료되면 Azure Site Recovery에서 Hyper-V 서버의 메타데이터가 검색되며 서버가 **Site Recovery 인프라** > **Hyper-V 호스트**에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-217">After registration finishes, metadata from the Hyper-V server is retrieved by Azure Site Recovery, and the server is displayed in **Site Recovery Infrastructure** > **Hyper-V Hosts**.</span></span>


## <a name="set-up-the-target-environment"></a><span data-ttu-id="b2e02-218">대상 환경 설정</span><span class="sxs-lookup"><span data-stu-id="b2e02-218">Set up the target environment</span></span>

<span data-ttu-id="b2e02-219">복제에 사용할 Azure 저장소 계정과 장애 조치(failover) 후 Azure VM이 연결될 Azure 네트워크를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-219">Specify the Azure storage account for replication, and the Azure network to which Azure VMs will connect after failover.</span></span>

1. <span data-ttu-id="b2e02-220">**인프라 준비** > **대상**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-220">Click **Prepare infrastructure** > **Target**.</span></span>
2. <span data-ttu-id="b2e02-221">장애 조치(failover) 후 Azure VM을 만들 구독 및 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-221">Select the subscription and the resource group in which you want to create the Azure VMs after failover.</span></span> <span data-ttu-id="b2e02-222">Azure(클래식 또는 리소스 관리)에서 VM에 사용할 배포 모델을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-222">Choose the deployment model that you want to use in Azure (classic or resource management) for the VMs.</span></span>

3. <span data-ttu-id="b2e02-223">Site Recovery가 호환되는 Azure 저장소 계정 및 네트워크가 하나 이상 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-223">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

    - <span data-ttu-id="b2e02-224">저장소 계정이 없으면 **+저장소**를 클릭하여 Resource Manager 기반 계정 인라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-224">If you don't have a storage account, click **+Storage** to create a Resource Manager-based account inline.</span></span> <span data-ttu-id="b2e02-225">[저장소 요구 사항](site-recovery-prereq.md#azure-requirements)을 읽어 보세요.</span><span class="sxs-lookup"><span data-stu-id="b2e02-225">Read about [storage requirements](site-recovery-prereq.md#azure-requirements).</span></span>
    - <span data-ttu-id="b2e02-226">Azure 네트워크가 없으면 **+네트워크**를 클릭하여 Resource Manager 기반 네트워크 인라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-226">If you don't have a Azure network, click **+Network** to create a Resource Manager-based network inline.</span></span>

    ![저장소](./media/site-recovery-vmware-to-azure/enable-rep3.png)




## <a name="configure-replication-settings"></a><span data-ttu-id="b2e02-228">복제 설정 구성</span><span class="sxs-lookup"><span data-stu-id="b2e02-228">Configure replication settings</span></span>

1. <span data-ttu-id="b2e02-229">새 복제 정책을 만들려면 **인프라 준비** > **복제 설정** > **+만들기 및 연결**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-229">To create a new replication policy, click **Prepare infrastructure** > **Replication Settings** > **+Create and associate**.</span></span>

    ![네트워크](./media/site-recovery-hyper-v-site-to-azure/gs-replication.png)
2. <span data-ttu-id="b2e02-231">**만들기 및 연결 정책**에서 정책 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-231">In **Create and associate policy**, specify a policy name.</span></span>
3. <span data-ttu-id="b2e02-232">**복사 빈도**에서 초기 복제 후 델타 데이터를 복제할 빈도(30초 마다, 5분마다 또는 15분마다)를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-232">In **Copy frequency**, specify how often you want to replicate delta data after the initial replication (every 30 seconds, 5 or 15 minutes).</span></span>

    > [!NOTE]
    > <span data-ttu-id="b2e02-233">Premium Storage로 복제하는 경우 30초 빈도가 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-233">A 30 second frequency isn't supported when replicating to premium storage.</span></span> <span data-ttu-id="b2e02-234">Premium Storage에서 지원하는 blob당 스냅숏 수(100)에 따라 제한이 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-234">The limitation is determined by the number of snapshots per blob (100) supported by premium storage.</span></span> <span data-ttu-id="b2e02-235">[자세히 알아보세요](../storage/storage-premium-storage.md#snapshots-and-copy-blob)을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="b2e02-235">[Learn more](../storage/storage-premium-storage.md#snapshots-and-copy-blob).</span></span>

4. <span data-ttu-id="b2e02-236">**복구 지점 보존**에서 각 복구 지점에 대해 지속될 보존 시간을 시간 단위로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-236">In **Recovery point retention**, specify in hours how long the retention window is for each recovery point.</span></span> <span data-ttu-id="b2e02-237">VM을 이 기간 내의 모든 지점으로 복구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-237">VMs can be recovered to any point within a window.</span></span>
5. <span data-ttu-id="b2e02-238">**앱 일치 스냅숏 빈도**에서 응용 프로그램 일치 스냅숏이 포함된 복구 지점을 만드는 빈도(1~12시간)를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-238">In **App-consistent snapshot frequency**, specify how frequently (1-12 hours) recovery points containing application-consistent snapshots are created.</span></span>

    - <span data-ttu-id="b2e02-239">Hyper-V는 두 가지 유형의 스냅숏, 즉 전체 가상 컴퓨터의 증분 스냅숏을 제공하는 표준 스냅숏과 가상 컴퓨터 내 응용 프로그램 데이터의 지정 시간 스냅숏을 만드는 응용 프로그램 일치 스냅숏을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-239">Hyper-V uses two types of snapshots — a standard snapshot that provides an incremental snapshot of the entire virtual machine, and an application-consistent snapshot that takes a point-in-time snapshot of the application data inside the virtual machine.</span></span>
    - <span data-ttu-id="b2e02-240">응용 프로그램 일치 스냅숏은 VSS(볼륨 섀도 복사본 서비스)를 사용하여 스냅숏을 만들 때 응용 프로그램이 일관된 상태가 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-240">Application-consistent snapshots use Volume Shadow Copy Service (VSS) to ensure that applications are in a consistent state when the snapshot is taken.</span></span>
    - <span data-ttu-id="b2e02-241">응용 프로그램 일치 스냅숏을 사용하도록 설정하면 원본 가상 컴퓨터에서 실행되는 응용 프로그램의 성능에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-241">If you enable application-consistent snapshots, it will affect the performance of applications running on source virtual machines.</span></span> <span data-ttu-id="b2e02-242">구성하는 추가 복구 지점 수보다 작은 값을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-242">Ensure that the value you set is less than the number of additional recovery points you configure.</span></span>

6. <span data-ttu-id="b2e02-243">**초기 복제 시작 시간**에서 초기 복제를 시작할 시간을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-243">In **Initial replication start time**, specify when to start the initial replication.</span></span> <span data-ttu-id="b2e02-244">복제는 인터넷 대역폭을 통해 발생하므로 바쁜 시간을 피해서 복제 일정을 예약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-244">The replication occurs over your internet bandwidth so you might want to schedule it outside your busy hours.</span></span> <span data-ttu-id="b2e02-245">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-245">Then click **OK**.</span></span>

    ![복제 정책](./media/site-recovery-hyper-v-site-to-azure/gs-replication2.png)

<span data-ttu-id="b2e02-247">새 정책을 만들면 새 정책이 자동으로 Hyper-V 사이트에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-247">When you create a new policy, it's automatically associated with the Hyper-V site.</span></span> <span data-ttu-id="b2e02-248">**복제** > 정책 이름 > **Hyper-V 사이트 연결**에서 Hyper-V 사이트 및 해당 사이트 내의 VM을 여러 복제 정책과 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-248">You can associate a Hyper-V site (and the VMs in it) with multiple replication policies in **Replication** > policy-name > **Associate Hyper-V Site**.</span></span>

## <a name="capacity-planning"></a><span data-ttu-id="b2e02-249">용량 계획</span><span class="sxs-lookup"><span data-stu-id="b2e02-249">Capacity planning</span></span>

<span data-ttu-id="b2e02-250">기본 인프라를 설치했으니 용량 계획에 대해 생각해 보고 추가 리소스가 필요한지 파악할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-250">Now that you have your basic infrastructure set up, you can think about capacity planning, and figure out whether you need additional resources.</span></span>

<span data-ttu-id="b2e02-251">Site Recovery는 컴퓨팅, 네트워킹 및 저장소에 적절한 리소스를 할당할 수 있도록 도와주는 Capacity Planner를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-251">Site Recovery provides a capacity planner to help you allocate the right resources for compute, networking, and storage.</span></span> <span data-ttu-id="b2e02-252">평균 VM, 디스크 및 저장소 수를 기반으로 예측하는 빠른 모드 또는 워크로드 수준에서 사용자 지정된 숫자를 사용하는 세부 모드에서 플래너를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-252">You can run the planner in quick mode for estimations based on an average number of VMs, disks, and storage, or in detailed mode with customized numbers at the workload level.</span></span> <span data-ttu-id="b2e02-253">시작하기 전에 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-253">Before you start you need to:</span></span>

* <span data-ttu-id="b2e02-254">VM, VM당 디스크, 디스크당 저장소를 포함하여 복제 환경에 대한 정보를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-254">Gather information about your replication environment, including VMs, disks per VMs, and storage per disk.</span></span>
* <span data-ttu-id="b2e02-255">복제된 데이터의 일일 변경(이탈)률을 예측합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-255">Estimate the daily change (churn) rate for your replicated data.</span></span> <span data-ttu-id="b2e02-256">[Hyper-V 복제본용 Capacity Planner](https://www.microsoft.com/download/details.aspx?id=39057) 를 사용하면 이 작업을 간편하게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-256">You can use the [Capacity Planner for Hyper-V Replica](https://www.microsoft.com/download/details.aspx?id=39057) to help you do this.</span></span>

1. <span data-ttu-id="b2e02-257">**다운로드**를 클릭하여 도구를 다운로드한 후 실행하세요.</span><span class="sxs-lookup"><span data-stu-id="b2e02-257">Click **Download** to download the tool, and then run it.</span></span> <span data-ttu-id="b2e02-258">[문서를 읽어보세요](site-recovery-capacity-planner.md) .</span><span class="sxs-lookup"><span data-stu-id="b2e02-258">[Read the article](site-recovery-capacity-planner.md) that accompanies the tool.</span></span>
2. <span data-ttu-id="b2e02-259">작업을 마쳤으면 **Capacity Planner를 실행하셨습니까?**에서 **예**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-259">When you’re done, select **Yes** in **Have you run the Capacity Planner**?</span></span>

   ![용량 계획](./media/site-recovery-hyper-v-site-to-azure/gs-capacity-planning.png)

<span data-ttu-id="b2e02-261">[네트워크 대역폭 제어](#network-bandwidth-considerations)에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="b2e02-261">Learn more about [controlling network bandwidth](#network-bandwidth-considerations)</span></span>



## <a name="enable-replication"></a><span data-ttu-id="b2e02-262">복제 활성화</span><span class="sxs-lookup"><span data-stu-id="b2e02-262">Enable replication</span></span>

<span data-ttu-id="b2e02-263">시작하기 전에 Azure 사용자 계정에 Azure로 새 가상 컴퓨터를 복제할 수 있는 필수 [사용 권한](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-263">Before you start, ensure that your Azure user account has the required  [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) to enable replication of a new virtual machine to Azure.</span></span>

<span data-ttu-id="b2e02-264">다음과 같이 VM에 대해 복제를 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-264">Enable replication for VMs as follows:</span></span>          

1. <span data-ttu-id="b2e02-265">**응용 프로그램 복제** > **원본**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-265">Click **Replicate application** > **Source**.</span></span> <span data-ttu-id="b2e02-266">처음으로 복제를 설정한 후에는 **+복제**를 클릭하여 추가 컴퓨터에 대해 복제를 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-266">After you've set up replication for the first time, you can click **+Replicate** to enable replication for additional machines.</span></span>

    ![복제 활성화](./media/site-recovery-hyper-v-site-to-azure/enable-replication.png)
2. <span data-ttu-id="b2e02-268">**원본**에서 Hyper-V 사이트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-268">In **Source**, select the Hyper-V site.</span></span> <span data-ttu-id="b2e02-269">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-269">Then click **OK**.</span></span>
3. <span data-ttu-id="b2e02-270">**대상**에서 자격 증명 모음 구독을 선택하고, 장애 조치(failover) 후 Azure에서 사용할 장애 조치(failover) 모델(클래식 또는 리소스 관리)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-270">In **Target**, select the vault subscription, and the failover model you want to use in Azure (classic or resource management) after failover.</span></span>
4. <span data-ttu-id="b2e02-271">사용하려는 저장소 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-271">Select the storage account you want to use.</span></span> <span data-ttu-id="b2e02-272">사용하려는 계정이 없는 경우 [새로 만들 수 있습니다](#set-up-an-azure-storage-account).</span><span class="sxs-lookup"><span data-stu-id="b2e02-272">If you don't have an account you want to use, you can [create one](#set-up-an-azure-storage-account).</span></span> <span data-ttu-id="b2e02-273">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-273">Then click **OK**.</span></span>
5. <span data-ttu-id="b2e02-274">장애 조치(failover) 후 Azure VM이 생성될 때 연결할 Azure 네트워크 및 서브넷을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-274">Select the Azure network and subnet to which Azure VMs will connect when they're created failover.</span></span>

    - <span data-ttu-id="b2e02-275">복제를 활성화한 모든 컴퓨터에 네트워크 설정을 적용하려면 **선택한 컴퓨터에 대해 지금 구성합니다.**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-275">To apply the network settings to all machines you enable for replication, select **Configure now for selected machines**.</span></span>
    - <span data-ttu-id="b2e02-276">네트워크가 없는 경우 **만들어야** 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-276">Select **Configure later** to select the Azure network per machine.</span></span>
    - <span data-ttu-id="b2e02-277">사용하려는 네트워크가 없는 경우 [새로 만들 수 있습니다](#set-up-an-azure-network).</span><span class="sxs-lookup"><span data-stu-id="b2e02-277">If you don't have a network you want to use, you can [create one](#set-up-an-azure-network).</span></span> <span data-ttu-id="b2e02-278">해당하는 경우 서브넷을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-278">Select a subnet if applicable.</span></span> <span data-ttu-id="b2e02-279">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-279">Then click **OK**.</span></span>

   ![복제 활성화](./media/site-recovery-hyper-v-site-to-azure/enable-replication11.png)

6. <span data-ttu-id="b2e02-281">**Virtual Machines** > **가상 컴퓨터 선택**에서 복제하려는 각 컴퓨터를 클릭하여 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-281">In **Virtual Machines** > **Select virtual machines**, click and select each machine you want to replicate.</span></span> <span data-ttu-id="b2e02-282">복제를 활성화할 수 있는 컴퓨터만 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-282">You can only select machines for which replication can be enabled.</span></span> <span data-ttu-id="b2e02-283">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-283">Then click **OK**.</span></span>

    ![복제 활성화](./media/site-recovery-hyper-v-site-to-azure/enable-replication5-for-exclude-disk.png)

7. <span data-ttu-id="b2e02-285">**속성** > **속성 구성**에서 선택한 VM의 운영 체제 및 OS 디스크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-285">In **Properties** > **Configure properties**, select the operating system for the selected VMs, and the OS disk.</span></span>
8. <span data-ttu-id="b2e02-286">Azure VM 이름(대상 이름)이 [Azure Virtual Machine 요구 사항](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)을 충족하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-286">Verify that the Azure VM name (target name) complies with [Azure virtual machine requirements](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>
9. <span data-ttu-id="b2e02-287">기본적으로 VM의 모든 디스크가 복제에 선택되지만 디스크를 지워서 제외할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-287">By default all the disks of the VM are selected for replication, but you can clear disks to exclude them.</span></span>
    - <span data-ttu-id="b2e02-288">복제 대역폭을 줄이기 위해 디스크를 제외할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-288">You might want to exclude disks to reduce replication bandwidth.</span></span> <span data-ttu-id="b2e02-289">예를 들어 임시 데이터 또는 컴퓨터나 앱이 다시 시작할 때마다 새로 고쳐지는 데이터(예: pagefile.sys 또는 SQL Server tempdb)가 포함된 디스크를 복제에서 제외하려는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-289">For example, you might not want to replicate disks with temporary data, or data that's refreshed each time a machine or apps restarts (such as pagefile.sys or Microsoft SQL Server tempdb).</span></span> <span data-ttu-id="b2e02-290">디스크를 선택 취소하여 복제에서 해당 디스크를 제외할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-290">You can exclude the disk from replication by unselecting the disk.</span></span>
    - <span data-ttu-id="b2e02-291">기본 디스크만 제외할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-291">Only basic disks can be exclude.</span></span> <span data-ttu-id="b2e02-292">OS 디스크는 제외할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-292">You can't exclude OS disks.</span></span>
    - <span data-ttu-id="b2e02-293">동적 디스크는 제외하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-293">We recommend that you don't exclude dynamic disks.</span></span> <span data-ttu-id="b2e02-294">Site Recovery는 게스트 VM 내의 가상 하드 디스크가 기본 디스크인지 아니면 동적 디스크인지 식별할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-294">Site Recovery can't identify whether a virtual hard disk inside a guest VM is basic or dynamic.</span></span> <span data-ttu-id="b2e02-295">모든 종속적인 동적 볼륨 디스크가 제외되지 않으면, 보호된 동적 디스크는 VM이 장애 조치되면 실패한 디스크로 나타나며 해당 디스크에 있는 데이터는 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-295">If all dependent dynamic volume disks aren't excluded, the protected dynamic disk will show as a failed disk when the VM fails over, and the data on that disk won't be accessible.</span></span>
        - <span data-ttu-id="b2e02-296">복제를 사용하도록 설정한 후 복제에 대해 디스크를 추가 또는 제거할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-296">After replication is enabled, you can't add or remove disks for replication.</span></span> <span data-ttu-id="b2e02-297">디스크를 추가하거나 제외하려는 경우 VM에 대한 보호를 사용하지 않도록 설정한 다음 다시 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-297">If you want to add or exclude a disk, you need to disable protection for the VM, and then re-enable it.</span></span>
        - <span data-ttu-id="b2e02-298">Azure에서 수동으로 만드는 디스크는 장애 복구되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-298">Disks you create manually in Azure aren't failed back.</span></span> <span data-ttu-id="b2e02-299">예를 들어 디스크 3장을 장애 조치하고 2장을 직접 Azure VM에서 만든다면 장애 조치된 3장의 디스크만이 Azure에서 다시 Hyper-V로 장애 복구됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-299">For example, if you fail over three disks, and create two directly in Azure VM, only the three disks which were failed over will be failed back from Azure to Hyper-V.</span></span> <span data-ttu-id="b2e02-300">장애 복구 또는 Hyper-V에서 Azure로 역방향 복제에서 수동으로 만든 디스크를 포함할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-300">You can't include disks created manually in failback, or in reverse replication from Hyper-V to Azure.</span></span>
        - <span data-ttu-id="b2e02-301">응용 프로그램 작동에 필요한 디스크를 제외하면 Azure로 장애 조치(failover) 후 복제된 응용 프로그램이 실행될 수 있도록 디스크를 Azure에 수동으로 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-301">If you exclude a disk that's needed for an application to operate, after failover to Azure you need to create it manually in Azure, so that the replicated application can run.</span></span> <span data-ttu-id="b2e02-302">또는 Azure Automation을 복구 계획에 통합하여 컴퓨터의 장애 조치(failover) 동안 디스크를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-302">Alternatively, you could integrate Azure automation into a recovery plan, to create the disk during failover of the machine.</span></span>

10. <span data-ttu-id="b2e02-303">**확인**을 클릭하여 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-303">Click **OK** to save changes.</span></span> <span data-ttu-id="b2e02-304">나중에 추가 속성을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-304">You can set additional properties later.</span></span>

    ![복제 활성화](./media/site-recovery-hyper-v-site-to-azure/enable-replication6-with-exclude-disk.png)

11. <span data-ttu-id="b2e02-306">**복제 설정** > **복제 설정 구성**에서 보호되는 VM에 적용할 복제 정책을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-306">In **Replication settings** > **Configure replication settings**, select the replication policy you want to apply for the protected VMs.</span></span> <span data-ttu-id="b2e02-307">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-307">Then click **OK**.</span></span> <span data-ttu-id="b2e02-308">**복제 정책** > 정책 이름 > **설정 편집**에서 복제 정책을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-308">You can modify the replication policy in **Replication policies** > policy-name > **Edit Settings**.</span></span> <span data-ttu-id="b2e02-309">적용하는 변경 사항은 이미 복제 중인 컴퓨터와 새 컴퓨터에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-309">Changes you apply will be used for machines that are already replicating, and new machines.</span></span>


   ![복제 활성화](./media/site-recovery-hyper-v-site-to-azure/enable-replication7.png)

<span data-ttu-id="b2e02-311">**작업** > **Site Recovery 작업**에서 **보호 사용** 작업의 진행률을 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-311">You can track progress of the **Enable Protection** job in **Jobs** > **Site Recovery jobs**.</span></span> <span data-ttu-id="b2e02-312">**보호 완료** 작업이 실행된 후에는 컴퓨터가 장애 조치(failover)를 수행할 준비가 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-312">After the **Finalize Protection** job runs the machine is ready for failover.</span></span>

### <a name="view-and-manage-vm-properties"></a><span data-ttu-id="b2e02-313">VM 속성 보기 및 관리</span><span class="sxs-lookup"><span data-stu-id="b2e02-313">View and manage VM properties</span></span>

<span data-ttu-id="b2e02-314">원본 컴퓨터의 속성을 확인하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-314">We recommend that you verify the properties of the source machine.</span></span>

1. <span data-ttu-id="b2e02-315">**보호된 항목**에서 **복제된 항목**을 클릭하고 컴퓨터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-315">In **Protected Items**, click **Replicated Items**, and select the machine.</span></span>

    ![복제 활성화](./media/site-recovery-hyper-v-site-to-azure/test-failover1.png)
2. <span data-ttu-id="b2e02-317">**속성**에서 해당 VM에 대한 복제 및 장애 조치(failover) 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-317">In **Properties**, you can view replication and failover information for the VM.</span></span>

    ![복제 활성화](./media/site-recovery-hyper-v-site-to-azure/test-failover2.png)
3. <span data-ttu-id="b2e02-319">**계산 및 네트워크** > **계산 속성**에서 Azure VM 이름 및 대상 크기를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-319">In **Compute and Network** > **Compute properties**, you can specify the Azure VM name and target size.</span></span> <span data-ttu-id="b2e02-320">필요한 경우 Azure 요구 사항을 준수하도록 이름을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-320">Modify the name to comply with Azure requirements if you need to.</span></span> <span data-ttu-id="b2e02-321">또한 대상 네트워크, 서브넷 및 Azure VM에 할당될 IP 주소에 대한 정보를 보고 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-321">You can also view and modify information about the target network, subnet, and IP address that will be assigned to the Azure VM.</span></span> <span data-ttu-id="b2e02-322">다음 사항에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="b2e02-322">Note the following:</span></span>

   * <span data-ttu-id="b2e02-323">대상 IP 주소를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-323">You can set the target IP address.</span></span> <span data-ttu-id="b2e02-324">주소를 입력하지 않으면 장애 조치(Failover)된 컴퓨터가 DHCP를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-324">If you don't provide an address, the failed over machine will use DHCP.</span></span> <span data-ttu-id="b2e02-325">장애 조치(failover) 시 사용할 수 없는 주소를 설정하면 장애 조치(failover)가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-325">If you set an address that isn't available at failover, the failover will fail.</span></span> <span data-ttu-id="b2e02-326">주소를 테스트 장애 조치(failover) 네트워크에서 사용할 수 있는 경우 테스트 장애 조치(failover)에 동일한 대상 IP 주소를 사용해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-326">The same target IP address can be used for test failover if the address is available in the test failover network.</span></span>
   * <span data-ttu-id="b2e02-327">네트워크 어댑터 수는 다음과 같이 대상 가상 컴퓨터에 대해 지정하는 크기에 따라 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-327">The number of network adapters is dictated by the size you specify for the target virtual machine, as follows:</span></span>

     * <span data-ttu-id="b2e02-328">원본 컴퓨터의 네트워크 어댑터 수가 대상 컴퓨터 크기에 허용되는 어댑터 수보다 작거나 같은 경우, 대상의 어댑터 수는 소스와 동일해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-328">If the number of network adapters on the source machine is less than or equal to the number of adapters allowed for the target machine size, then the target will have the same number of adapters as the source.</span></span>
     * <span data-ttu-id="b2e02-329">원본 가상 컴퓨터의 어댑터의 수가 대상 크기에 허용된 수를 초과하면 대상 크기 최대치가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-329">If the number of adapters for the source virtual machine exceeds the number allowed for the target size then the target size maximum will be used.</span></span>
     * <span data-ttu-id="b2e02-330">예를 들어 원본 컴퓨터에 두 네트워크 어댑터가 있고 대상 컴퓨터 크기가 4를 지원하는 경우, 대상 컴퓨터에는 2개의 어댑터가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-330">For example if a source machine has two network adapters and the target machine size supports four, the target machine will have two adapters.</span></span> <span data-ttu-id="b2e02-331">원본 컴퓨터에 두 어댑터가 있지만 지원되는 대상 크기가 하나만 지원하는 경우 대상 컴퓨터에는 1개의 어댑터만 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-331">If the source machine has two adapters but the supported target size only supports one then the target machine will have only one adapter.</span></span>     
     * <span data-ttu-id="b2e02-332">VM에 네트워크 어댑터가 여러 개 있으면 모두 동일한 네트워크에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-332">If the VM has multiple network adapters they will all connect to the same network.</span></span>
     * <span data-ttu-id="b2e02-333">가상 컴퓨터에 네트워크 어댑터가 여러 개 있으면 목록에서 첫 번째 어댑터가 Azure 가상 컴퓨터에서 *기본* 네트워크 어댑터가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-333">If the virtual machine has multiple network adapters then the first one shown in the list becomes the *Default* network adapter in the Azure virtual machine.</span></span>

     ![복제 활성화](./media/site-recovery-hyper-v-site-to-azure/test-failover4.png)

4. <span data-ttu-id="b2e02-335">**디스크**에서 복제될 VM의 운영 체제 및 데이터 디스크를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-335">In **Disks**, you can see the operating system and data disks on the VM that will be replicated.</span></span>

#### <a name="managed-disks"></a><span data-ttu-id="b2e02-336">관리 디스크</span><span class="sxs-lookup"><span data-stu-id="b2e02-336">Managed disks</span></span>

<span data-ttu-id="b2e02-337">**계산 및 네트워크** > **계산 속성**에서 Azure에 마이그레이션할 때 컴퓨터에 Managed Disks를 연결하려면 VM에서 "Managed Disks 사용" 설정을 "예"로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-337">In **Compute and Network** > **Compute properties**, you can set "Use managed disks" setting to "Yes" for the VM if you want to attach managed disks to your machine on migration to Azure.</span></span> <span data-ttu-id="b2e02-338">Managed Disks는 VM 디스크와 연결된 저장소 계정을 관리하여 Azure IaaS VM의 디스크 관리를 간소화합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-338">Managed disks simplifies disk management for Azure IaaS VMs by managing the storage accounts associated with the VM disks.</span></span> <span data-ttu-id="b2e02-339">[Managed Disks에 대한 자세히 알아봅니다](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview).</span><span class="sxs-lookup"><span data-stu-id="b2e02-339">[Learn More about managed disks](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview).</span></span>

   - <span data-ttu-id="b2e02-340">Managed Disks를 만들고 Azure에 장애 조치 시에만 가상 컴퓨터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-340">Managed disks are created and attached to the virtual machine only on a failover to Azure.</span></span> <span data-ttu-id="b2e02-341">보호를 사용하도록 설정하여 온-프레미스 컴퓨터의 데이터를 저장소 계정에 계속 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-341">On enabling protection, data from on-premises machines will continue to replicate to storage accounts.</span></span>
   <span data-ttu-id="b2e02-342">Resource Manager 배포 모델을 사용하여 배포된 가상 컴퓨터에 대해서만 Managed Disks를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-342">Managed disks can be created only for virtual machines deployed using the Resource manager deployment model.</span></span>

  > [!NOTE]
  > <span data-ttu-id="b2e02-343">현재 Azure로부터 온-프레미스 Hyper-V 환경으로의 장애 복구는 Managed Disks를 포함한 컴퓨터에 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-343">Failback from Azure to on-premises Hyper-V environment is not currently supported for machines with managed disks.</span></span> <span data-ttu-id="b2e02-344">Azure에 이 컴퓨터를 마이그레이션할 경우 "Managed Disks 사용"을 "예"로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-344">Set "Use managed disks" to "Yes" only if you intend to migrate this machine to Azure.</span></span>

   - <span data-ttu-id="b2e02-345">"Managed Disks 사용"을 "예"로 설정하면 리소스 그룹에서 "Managed Disks 사용"을 "예"로 설정한 가용성 집합만을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-345">When you set "Use managed disks" to "Yes", only availability sets in the resource group with "Use managed disks" set to "Yes" would be available for selection.</span></span> <span data-ttu-id="b2e02-346">Managed Disks를 포함한 가상 컴퓨터가 "Managed Disks 사용" 속성을 "예"로 설정한 가용성 집합의 일부이기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-346">This is because virtual machines with managed disks can only be part of availability sets with "Use managed disks" property set to "Yes".</span></span> <span data-ttu-id="b2e02-347">장애 조치 시 Managed Disks를 사용하려는 의도에 따라 "Managed Disks 사용" 속성이 설정된 가용성 집합을 만들었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-347">Make sure that you create availability sets with "Use managed disks" property set based on your intent to use managed disks on failover.</span></span> <span data-ttu-id="b2e02-348">마찬가지로 "Managed Disks 사용"을 "아니요"로 설정하면 리소스 그룹에서 "Managed Disks 사용" 속성을 "아니요"로 설정한 가용성 집합만을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-348">Likewise, when you set "Use managed disks" to "No", only availability sets in the resource group with "Use managed disks" property set to "No" would be available for selection.</span></span> <span data-ttu-id="b2e02-349">[Managed Disks와 가용성 집합에 대해 자세히 알아봅니다](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set).</span><span class="sxs-lookup"><span data-stu-id="b2e02-349">[Learn more about managed disks and availability sets](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set).</span></span>

  > [!NOTE]
  > <span data-ttu-id="b2e02-350">복제에 사용되는 저장소 계정이 특정 시점에 저장소 서비스 암호화로 암호화된 경우 장애 조치 중에 Managed Disks를 만드는 작업에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-350">If the storage account used for replication was encrypted with Storage Service Encryption at any point in time, creation of managed disks during failover will fail.</span></span> <span data-ttu-id="b2e02-351">"Managed Disks 사용"을 "아니요"로 설정하고 장애 조치를 다시 시도하거나 가상 컴퓨터에 대한 보호를 사용하지 않도록 하고 특정 시점에서 저장소 서비스 암호화를 사용하지 않은 저장소 계정에 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-351">You can either set "Use managed disks" to "No" and retry failover or disable protection for the virtual machine and protect it to a storage account which did not have Storage service encryption enabled at any point in time.</span></span>
  > <span data-ttu-id="b2e02-352">[저장소 서비스를 암호화 및 Managed Disks에 대해 자세히 알아봅니다](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption).</span><span class="sxs-lookup"><span data-stu-id="b2e02-352">[Learn more about Storage service encryption and managed disks](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption).</span></span>


## <a name="test-the-deployment"></a><span data-ttu-id="b2e02-353">배포 테스트</span><span class="sxs-lookup"><span data-stu-id="b2e02-353">Test the deployment</span></span>

<span data-ttu-id="b2e02-354">배포를 테스트하기 위해 단일 가상 컴퓨터에 대한 테스트 장애 조치(Failover)를 실행하거나 하나 이상의 가상 컴퓨터를 포함한 복구 계획을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-354">To test the deployment you can run a test failover for a single virtual machine or a recovery plan that contains one or more virtual machines.</span></span>

### <a name="before-you-start"></a><span data-ttu-id="b2e02-355">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="b2e02-355">Before you start</span></span>

 - <span data-ttu-id="b2e02-356">장애 조치(Failover) 후 RDP를 사용하여 Azure VM에 연결하려면 [연결 준비](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover)에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="b2e02-356">If you want to connect to Azure VMs using RDP after failover, learn about [preparing to connect](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover).</span></span>
 - <span data-ttu-id="b2e02-357">완벽하게 테스트하려면 테스트 환경에 Active Directory 및 DNS 복사본이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-357">To fully test you need to copy of Active Directory and DNS in your test environment.</span></span> <span data-ttu-id="b2e02-358">[자세히 알아보세요](site-recovery-active-directory.md#test-failover-considerations)을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="b2e02-358">[Learn more](site-recovery-active-directory.md#test-failover-considerations).</span></span>

### <a name="run-a-test-failover"></a><span data-ttu-id="b2e02-359">테스트 장애 조치(Failover) 실행</span><span class="sxs-lookup"><span data-stu-id="b2e02-359">Run a test failover</span></span>

1. <span data-ttu-id="b2e02-360">단일 컴퓨터를 장애 조치(failover)하려면 **복제된 항목**에서 VM > **+테스트 장애 조치(failover)** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-360">To fail over a single machine, in **Replicated Items**, click the VM > **+Test Failover** icon.</span></span>
2. <span data-ttu-id="b2e02-361">복구 계획을 장애 조치(failover)하려면 **복구 계획**에서 계획 > **테스트 장애 조치(failover)**를 마우스 오른쪽 버튼으로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-361">To fail over a recovery plan, in **Recovery Plans**, right-click the plan > **Test Failover**.</span></span> <span data-ttu-id="b2e02-362">복구 계획을 만들려면 [다음 지침을 따릅니다](site-recovery-create-recovery-plans.md).</span><span class="sxs-lookup"><span data-stu-id="b2e02-362">To create a recovery plan, [follow these instructions](site-recovery-create-recovery-plans.md).</span></span>
3. <span data-ttu-id="b2e02-363">**테스트 장애 조치(failover)**에서 장애 조치(failover)가 발생한 후에 Azure VM이 연결될 Azure 네트워크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-363">In **Test Failover**, select the Azure network to which Azure VMs will be connected after failover occurs.</span></span>
4. <span data-ttu-id="b2e02-364">**확인**을 클릭하여 장애 조치(failover)를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-364">Click **OK** to begin the failover.</span></span> <span data-ttu-id="b2e02-365">VM을 클릭하여 속성을 열거나 자격 증명 모음 이름 > **작업** > **Site Recovery 작업**에서 **테스트 장애 조치(failover)**에서 진행률을 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-365">You can track progress by clicking on the VM to open its properties, or on the **Test Failover** job in vault name > **Jobs** > **Site Recovery jobs**.</span></span>
5. <span data-ttu-id="b2e02-366">또한 장애 조치(failover)가 완료된 후 Azure 포털 > **Virtual Machines**에 Azure 컴퓨터 복제본이 나타나는 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-366">After the failover completes, you should also be able to see the replica Azure machine appear in the Azure portal > **Virtual Machines**.</span></span> <span data-ttu-id="b2e02-367">VM의 크기가 적당하고, 올바른 네트워크에 연결되었고, 실행 중인지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-367">You should make sure that the VM is the appropriate size, that it's connected to the appropriate network, and that it's running.</span></span>
6. <span data-ttu-id="b2e02-368">장애 조치(failover) 후 연결을 준비하는 경우 Azure VM에 연결할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-368">If you prepared for connections after failover, you should be able to connect to the Azure VM.</span></span>
7. <span data-ttu-id="b2e02-369">작업을 완료하면 복구 계획에서 **테스트 장애 조치 정리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-369">Once you're done, click on **Cleanup test failover** on the recovery plan.</span></span> <span data-ttu-id="b2e02-370">**참고** 에서 테스트 장애 조치와 연관된 모든 관측 내용을 기록하고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-370">In **Notes** record and save any observations associated with the test failover.</span></span> <span data-ttu-id="b2e02-371">그러면 테스트 장애 조치 중에 생성된 가상 컴퓨터가 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-371">This will delete the virtual machines that were created during test failover.</span></span>

<span data-ttu-id="b2e02-372">자세한 내용은 [Azure로 테스트 장애 조치](site-recovery-test-failover-to-azure.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b2e02-372">For more details, read the [Test failover to Azure](site-recovery-test-failover-to-azure.md) article.</span></span>



## <a name="monitor-the-deployment"></a><span data-ttu-id="b2e02-373">배포 모니터링</span><span class="sxs-lookup"><span data-stu-id="b2e02-373">Monitor the deployment</span></span>

<span data-ttu-id="b2e02-374">Site Recovery 배포의 구성 설정 및 상태를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-374">Monitor the configuration settings, status, and health for your Site Recovery deployment:</span></span>

1. <span data-ttu-id="b2e02-375">자격 증명 모음 이름을 클릭하여 **Essentials** 대시보드에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-375">Click on the vault name to access the **Essentials** dashboard.</span></span> <span data-ttu-id="b2e02-376">이 대시보드에서 Site Recovery 작업, 복제 상태, 복구 계획, 서버 상태 및 이벤트를 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-376">In this dashboard you can track Site Recovery jobs, replication status, recovery plans, server health, and events.</span></span>  

    ![Essentials](./media/site-recovery-hyper-v-site-to-azure/essentials.png)
2. <span data-ttu-id="b2e02-378">**상태** 타일에서 문제가 있는 사이트 서버와 지난 24시간 동안 Site Recovery에 의해 발생한 이벤트를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-378">In the **Health** tile you can monitor site servers that are experiencing issue, and the events raised by Site Recovery in the last 24 hours.</span></span> <span data-ttu-id="b2e02-379">다른 Site Recovery 및 백업 자격 증명 모음의 상태를 포함하여 가장 유용한 타일과 레이아웃을 표시하도록 Essentials를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-379">You can customize Essentials to show the tiles and layouts that are most useful to you, including the status of other Site Recovery and Backup vaults.</span></span>
3. <span data-ttu-id="b2e02-380">**복제된 항목**, **복구 계획** 및 **Site Recovery 작업** 타일에서 복제를 관리 및 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-380">You can manage and monitor replication in the **Replicated Items**, **Recovery Plans**, and **Site Recovery Jobs** tiles.</span></span> <span data-ttu-id="b2e02-381">**작업** > **Site Recovery 작업**에서 작업을 자세히 살펴볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-381">You can drill into jobs for more details in **Jobs** > **Site Recovery Jobs**.</span></span>

## <a name="command-line-provider-and-agent-installation"></a><span data-ttu-id="b2e02-382">명령줄 공급자 및 에이전트 설치</span><span class="sxs-lookup"><span data-stu-id="b2e02-382">Command-line Provider and agent installation</span></span>

<span data-ttu-id="b2e02-383">다음 명령줄을 사용하여 Azure Site Recovery 공급자와 에이전트를 설치할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-383">The Azure Site Recovery Provider and agent can also be installed using the following command line.</span></span> <span data-ttu-id="b2e02-384">이 방법은 Windows Server 2012 R2용 Server Core에 대한 공급자를 설치하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-384">This method can be used to install the provider on a Server Core for Windows Server 2012 R2.</span></span>

1. <span data-ttu-id="b2e02-385">공급자 설치 파일 및 등록 키를 폴더로 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-385">Download the Provider installation file and registration key to a folder.</span></span> <span data-ttu-id="b2e02-386">예: C:\ASR.</span><span class="sxs-lookup"><span data-stu-id="b2e02-386">For example C:\ASR.</span></span>
2. <span data-ttu-id="b2e02-387">상승된 명령 프롬프트에서 다음 명령을 실행하여 공급자 설치 관리자를 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-387">From an elevated command prompt, run these commands to extract the Provider installer:</span></span>

            C:\Windows\System32> CD C:\ASR
            C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
3. <span data-ttu-id="b2e02-388">다음 명령을 실행하여 구성 요소를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-388">Run this command to install the components:</span></span>

            C:\ASR> setupdr.exe /i
4. <span data-ttu-id="b2e02-389">그런 후 다음 이 명령을 실행하여 서버를 자격 증명 모음에 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-389">Then run these commands to register the server in the vault:</span></span>

            CD C:\Program Files\Microsoft Azure Site Recovery Provider\
            C:\Program Files\Microsoft Azure Site Recovery Provider\> DRConfigurator.exe /r  /Friendlyname <friendly name of the server> /Credentials <path of the credentials file>

<br/>
<span data-ttu-id="b2e02-390">여기서,</span><span class="sxs-lookup"><span data-stu-id="b2e02-390">Where:</span></span>

* <span data-ttu-id="b2e02-391">**/Credentials**: 등록 키 파일이 있는 위치를 지정하는 필수 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-391">**/Credentials**: Mandatory parameter that specifies the location in which the registration key file is located</span></span>  
* <span data-ttu-id="b2e02-392">**/FriendlyName**: Azure Site Recovery 포털에 나타나는 Hyper-V 호스트 서버의 이름에 대한 필수 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-392">**/FriendlyName**: Mandatory parameter for the name of the Hyper-V host server that appears in the Azure Site Recovery portal.</span></span>
* <span data-ttu-id="b2e02-393">**/proxyAddress**: 프록시 서버의 주소를 지정하는 선택적 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-393">**/proxyAddress**: Optional parameter that specifies the address of the proxy server.</span></span>
* <span data-ttu-id="b2e02-394">**/proxyport** : 프록시 서버의 포트를 지정하는 선택적 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-394">**/proxyport** : Optional parameter that specifies the port of the proxy server.</span></span>
* <span data-ttu-id="b2e02-395">**/proxyUsername**: (프록시가 인증을 필요로 하는 경우) 프록시 사용자 이름을 지정하는 선택적 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-395">**/proxyUsername**: Optional parameter that specifies the Proxy user name (if proxy requires authentication).</span></span>
* <span data-ttu-id="b2e02-396">**/proxyPassword**: (프록시가 인증을 필요로 하는 경우) 프록시 서버를 인증하기 위한 암호를 지정하는 선택적 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-396">**/proxyPassword**: Optional parameter that specifies the Password for authenticating with the proxy server (if proxy requires authentication).</span></span>


## <a name="network-bandwidth-considerations"></a><span data-ttu-id="b2e02-397">네트워크 대역폭 고려 사항</span><span class="sxs-lookup"><span data-stu-id="b2e02-397">Network bandwidth considerations</span></span>
<span data-ttu-id="b2e02-398">[Hyper-V Capacity Planner 도구](site-recovery-capacity-planner.md)를 사용하여 복제(초기 복제 후 델타)에 필요한 대역폭을 계산할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-398">You can use the [Hyper-V capacity planner tool](site-recovery-capacity-planner.md) to calculate the bandwidth you need for replication (initial replication and then delta).</span></span> <span data-ttu-id="b2e02-399">복제에 사용되는 대역폭 사용량을 제어하는 몇 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-399">To control the amount of bandwidth use for replication you have a few options:</span></span>

* <span data-ttu-id="b2e02-400">**대역폭 제한**: Azure에 복제되는 Hyper-V 트래픽이 특정 Hyper-V 호스트를 통과합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-400">**Throttle bandwidth**: Hyper-V traffic that replicates to Azure goes through a specific Hyper-V host.</span></span> <span data-ttu-id="b2e02-401">호스트 서버의 대역폭을 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-401">You can throttle bandwidth on the host server.</span></span>
* <span data-ttu-id="b2e02-402">**대역폭 조정**: 몇 가지 레지스트리 키를 사용하면 복제에 사용되는 대역폭에 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-402">**Tweak bandwidth**: You can influence the bandwidth used for replication using a couple of registry keys.</span></span>

### <a name="throttle-bandwidth"></a><span data-ttu-id="b2e02-403">대역폭 제한</span><span class="sxs-lookup"><span data-stu-id="b2e02-403">Throttle bandwidth</span></span>
1. <span data-ttu-id="b2e02-404">Hyper-V 호스트 서버에서 Microsoft Azure 백업 MMC 스냅인을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-404">Open the Microsoft Azure Backup MMC snap-in on the Hyper-V host server.</span></span> <span data-ttu-id="b2e02-405">기본적으로 Microsoft Azure 백업에 대한 바로 가기가 바탕 화면 또는 C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-405">By default a shortcut for Microsoft Azure Backup is available on the desktop or in C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.</span></span>
2. <span data-ttu-id="b2e02-406">스냅인에서 **속성 변경**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-406">In the snap-in click **Change Properties**.</span></span>
3. <span data-ttu-id="b2e02-407">**제한** 탭에서 **백업 작업에 인터넷 대역폭 사용 제한 사용**을 선택하고 근무 시간 및 근무 외 시간에 대한 한도를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-407">On the **Throttling** tab select **Enable internet bandwidth usage throttling for backup operations**, and set the limits for work and non-work hours.</span></span> <span data-ttu-id="b2e02-408">유효 범위는 초당 512Kbps~102Mbp입니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-408">Valid ranges are from 512 Kbps to 102 Mbps per second.</span></span>

    ![대역폭 제한](./media/site-recovery-hyper-v-site-to-azure/throttle2.png)

<span data-ttu-id="b2e02-410">[Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet를 사용하여 제한을 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-410">You can also use the [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet to set throttling.</span></span> <span data-ttu-id="b2e02-411">다음은 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-411">Here's a sample:</span></span>

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

<span data-ttu-id="b2e02-412">**Set-OBMachineSetting -NoThrottle** 은 제한이 필요 없다는 뜻입니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-412">**Set-OBMachineSetting -NoThrottle** indicates that no throttling is required.</span></span>

### <a name="influence-network-bandwidth"></a><span data-ttu-id="b2e02-413">네트워크 대역폭에 영향</span><span class="sxs-lookup"><span data-stu-id="b2e02-413">Influence network bandwidth</span></span>
1. <span data-ttu-id="b2e02-414">레지스트리에서 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-414">In the registry navigate to **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.</span></span>
   * <span data-ttu-id="b2e02-415">복제 디스크의 대역폭 트래픽에 영향을 주려면 **UploadThreadsPerVM**값을 수정하거나 없는 경우 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-415">To influence the bandwidth traffic on a replicating disk, modify the value the **UploadThreadsPerVM**, or create the key if it doesn't exist.</span></span>
   * <span data-ttu-id="b2e02-416">Azure에서 장애 복구(failback) 트래픽에 대한 대역폭에 영향을 주려면 **DownloadThreadsPerVM**값을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-416">To influence the bandwidth for failback traffic from Azure, modify the value **DownloadThreadsPerVM**.</span></span>
2. <span data-ttu-id="b2e02-417">기본값은 4입니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-417">The default value is 4.</span></span> <span data-ttu-id="b2e02-418">"과도하게 프로비전된" 네트워크에서는 이러한 레지스트리 키를 기본값에서 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-418">In an “overprovisioned” network, these registry keys should be changed from the default values.</span></span> <span data-ttu-id="b2e02-419">최대값은 32입니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-419">The maximum is 32.</span></span> <span data-ttu-id="b2e02-420">트래픽을 모니터링하여 값을 최적화합니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-420">Monitor traffic to optimize the value.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b2e02-421">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b2e02-421">Next steps</span></span>

<span data-ttu-id="b2e02-422">초기 복제가 완료되고 배포를 테스트한 후에는 필요할 때 장애 조치(failover)를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2e02-422">After initial replication is complete, and you've tested the deployment, you can invoke failovers as the need arises.</span></span> <span data-ttu-id="b2e02-423">여러 장애 조치(failover) 유형 및 장애 조치(failover) 실행 방법에 대해 [자세히 알아보세요](site-recovery-failover.md).</span><span class="sxs-lookup"><span data-stu-id="b2e02-423">[Learn more](site-recovery-failover.md) about different types of failovers and how to run them.</span></span>

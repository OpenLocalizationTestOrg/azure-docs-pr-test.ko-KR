---
title: Hyper-v Vm tooAzure aaaReplicate | Microsoft Docs
description: "설명 방법을 tooorchestrate 복제, 장애 조치 및 복구의 온-프레미스 하이퍼-V Vm tooAzure"
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
ms.openlocfilehash: 6fba41e43823fc57511d51ea2e09691159693982
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-without-vmm-tooazure-using-azure-site-recovery-with-hello-azure-portal"></a><span data-ttu-id="98e85-103">Hyper-v 가상 컴퓨터 (VMM 없음) tooAzure Azure Site Recovery를 사용 하 여 Azure 포털 hello로 복제</span><span class="sxs-lookup"><span data-stu-id="98e85-103">Replicate Hyper-V virtual machines (without VMM) tooAzure using Azure Site Recovery with hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="98e85-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="98e85-104">Azure portal</span></span>](site-recovery-hyper-v-site-to-azure.md)
> * [<span data-ttu-id="98e85-105">Azure 클래식</span><span class="sxs-lookup"><span data-stu-id="98e85-105">Azure classic</span></span>](site-recovery-hyper-v-site-to-azure-classic.md)
> * [<span data-ttu-id="98e85-106">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="98e85-106">PowerShell - Resource Manager</span></span>](site-recovery-deploy-with-powershell-resource-manager.md)
>
>

<span data-ttu-id="98e85-107">이 문서에서는 어떻게 tooreplicate 온-프레미스 Hyper-v 가상 컴퓨터 tooAzure 설명를 사용 하 여 [Azure Site Recovery](site-recovery-overview.md) hello Azure 포털의에서.</span><span class="sxs-lookup"><span data-stu-id="98e85-107">This article describes how tooreplicate on-premises Hyper-V virtual machines tooAzure, using [Azure Site Recovery](site-recovery-overview.md) in hello Azure portal.</span></span> <span data-ttu-id="98e85-108">이 배포에서는 Hyper-V VM이 System Center VMM(Virtual Machine Manager)을 통해 관리되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-108">In this deployment Hyper-V VMs aren't managed by System Center Virtual Machine Manager (VMM).</span></span>

<span data-ttu-id="98e85-109">이 문서를 읽은 후 hello 맨 아래에 모든 메모를 게시 하거나 hello에 대 한 기술적 질문 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-109">After reading this article, post any comments at hello bottom, or ask technical questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

<span data-ttu-id="98e85-110">자세한 내용을 보려면 toomigrate 컴퓨터 tooAzure 장애 복구) (제외 하려는 경우 [이 여기서](site-recovery-migrate-to-azure.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-110">If you want toomigrate machines tooAzure (without failback), learn more in [this article](site-recovery-migrate-to-azure.md).</span></span>



## <a name="deployment-steps"></a><span data-ttu-id="98e85-111">배포 단계</span><span class="sxs-lookup"><span data-stu-id="98e85-111">Deployment steps</span></span>

<span data-ttu-id="98e85-112">Hello 문서 toocomplete 다음 배포 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-112">Follow hello article toocomplete these deployment steps:</span></span>

1. <span data-ttu-id="98e85-113">[자세한 내용은](site-recovery-components.md#hyper-v-to-azure) 이 배포에 대 한 hello 아키텍처에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-113">[Learn more](site-recovery-components.md#hyper-v-to-azure) about hello architecture for this deployment.</span></span> <span data-ttu-id="98e85-114">또한 Site Recovery에서 Hyper-V 복제가 작동하는 방식을 [알아봅니다](site-recovery-hyper-v-azure-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="98e85-114">In addition, [learn about](site-recovery-hyper-v-azure-architecture.md) how Hyper-V replication works in Site Recovery.</span></span>
2. <span data-ttu-id="98e85-115">필수 조건 및 제한 사항을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-115">Verify prerequisites and limitations.</span></span>
3. <span data-ttu-id="98e85-116">Azure 네트워크 및 저장소 계정을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-116">Set up Azure network and storage accounts.</span></span>
4. <span data-ttu-id="98e85-117">Hyper-V 호스트를 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-117">Prepare Hyper-V hosts.</span></span>
5. <span data-ttu-id="98e85-118">Recovery Services 자격 증명 모음을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-118">Create a Recovery Services vault.</span></span> <span data-ttu-id="98e85-119">hello 자격 증명 모음 구성 설정을 포함 하 고 복제를 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-119">hello vault contains configuration settings, and orchestrates replication.</span></span>
6. <span data-ttu-id="98e85-120">원본 설정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-120">Specify source settings.</span></span> <span data-ttu-id="98e85-121">Hello Hyper-v 호스트를 포함 하는 Hyper-v 사이트를 만들고 hello 사이트 hello 자격 증명 모음에 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-121">Create a Hyper-V site that contains hello Hyper-V hosts, and register hello site in hello vault.</span></span> <span data-ttu-id="98e85-122">Hello Hyper-v 호스트에 hello Azure Site Recovery Provider 및 hello Microsoft 복구 서비스 에이전트를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-122">Install hello Azure Site Recovery Provider, and hello Microsoft Recovery Services agent, on hello Hyper-V hosts.</span></span>
7. <span data-ttu-id="98e85-123">대상 및 복제 설정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-123">Set up target and replication settings.</span></span>
8. <span data-ttu-id="98e85-124">Hello Vm에 대 한 복제를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-124">Enable replication for hello VMs.</span></span>
9. <span data-ttu-id="98e85-125">모든 것이 예상 대로 작동 하는지 테스트 장애 조치 toomake를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-125">Run a test failover toomake sure everything's working as expected.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="98e85-126">필수 조건</span><span class="sxs-lookup"><span data-stu-id="98e85-126">Prerequisites</span></span>


<span data-ttu-id="98e85-127">**요구 사항**</span><span class="sxs-lookup"><span data-stu-id="98e85-127">**Requirement**</span></span> | <span data-ttu-id="98e85-128">**세부 정보**</span><span class="sxs-lookup"><span data-stu-id="98e85-128">**Details**</span></span> |
--- | --- |
<span data-ttu-id="98e85-129">**Azure**</span><span class="sxs-lookup"><span data-stu-id="98e85-129">**Azure**</span></span> | <span data-ttu-id="98e85-130">[Azure 요구 사항](site-recovery-prereq.md#azure-requirements)에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-130">Learn about [Azure requirements](site-recovery-prereq.md#azure-requirements).</span></span>
<span data-ttu-id="98e85-131">**온-프레미스 서버**</span><span class="sxs-lookup"><span data-stu-id="98e85-131">**On-premises servers**</span></span> | <span data-ttu-id="98e85-132">[자세한 내용은](site-recovery-prereq.md#disaster-recovery-of-hyper-v-virtual-machines-to-azure-no-virtual-machine-manager) hello 온-프레미스 Hyper-v 호스트에 대 한 요구 사항에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-132">[Learn more](site-recovery-prereq.md#disaster-recovery-of-hyper-v-virtual-machines-to-azure-no-virtual-machine-manager) about requirements for hello on-premises Hyper-V hosts.</span></span>
<span data-ttu-id="98e85-133">**온-프레미스 Hyper-V VM**</span><span class="sxs-lookup"><span data-stu-id="98e85-133">**On-premises Hyper-V VMs**</span></span> | <span data-ttu-id="98e85-134">Vm tooreplicate를 실행 해야 하는 것이 원하는 [지원 되는 운영 체제](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions), 준수 및 [Azure 필수 구성 요소](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-134">VMs you want tooreplicate should be running a [supported operating system](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions), and conform with [Azure prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>
<span data-ttu-id="98e85-135">**Azure URL**</span><span class="sxs-lookup"><span data-stu-id="98e85-135">**Azure URLs**</span></span> | <span data-ttu-id="98e85-136">Hyper-v 호스트 toothese Url에 액세스할 필요:</span><span class="sxs-lookup"><span data-stu-id="98e85-136">Hyper-V hosts need access toothese URLs:</span></span><br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> <span data-ttu-id="98e85-137">IP 주소를 기준으로 방화벽 규칙을 사용 하는 경우 통신 tooAzure를 허용 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-137">If you have IP address-based firewall rules, ensure they allow communication tooAzure.</span></span><br/></br> <span data-ttu-id="98e85-138">Hello 허용 [Azure 데이터 센터 IP 범위](https://www.microsoft.com/download/confirmation.aspx?id=41653), 및 hello HTTPS (443) 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-138">Allow hello [Azure Datacenter IP Ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653), and hello HTTPS (443) port.</span></span><br/></br> <span data-ttu-id="98e85-139">West US (액세스 제어 및 Id 관리에 사용) 및 hello 구독의 Azure 지역에 대 한 IP 주소 범위를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-139">Allow IP address ranges for hello Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>



## <a name="prepare-for-deployment"></a><span data-ttu-id="98e85-140">배포 준비</span><span class="sxs-lookup"><span data-stu-id="98e85-140">Prepare for deployment</span></span>

<span data-ttu-id="98e85-141">tooprepare 배포 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-141">tooprepare for deployment you need to:</span></span>

1. <span data-ttu-id="98e85-142">[Azure 네트워크를 설정](#set-up-an-azure-network) 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-142">[Set up an Azure network](#set-up-an-azure-network) in which Azure VMs will be located when they're created after failover.</span></span>
2. <span data-ttu-id="98e85-143">[Azure 저장소 계정을 설정](#set-up-an-azure-storage-account) 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-143">[Set up an Azure storage account](#set-up-an-azure-storage-account) for replicated data.</span></span>
3. <span data-ttu-id="98e85-144">[Hello Hyper-v 호스트를 준비](#prepare-the-hyper-v-hosts) tooensure hello 액세스할 수 있는 Url 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-144">[Prepare hello Hyper-V hosts](#prepare-the-hyper-v-hosts) tooensure they can access hello required URLs.</span></span>

### <a name="set-up-an-azure-network"></a><span data-ttu-id="98e85-145">Azure 네트워크를 설정</span><span class="sxs-lookup"><span data-stu-id="98e85-145">Set up an Azure network</span></span>

<span data-ttu-id="98e85-146">Azure 네트워크 설정</span><span class="sxs-lookup"><span data-stu-id="98e85-146">Set up an Azure network.</span></span> <span data-ttu-id="98e85-147">Hello Azure Vm은 연결 된 tooa 네트워크 장애 조치 후 만들어지도록이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-147">You’ll need this so that hello Azure VMs created after failover are connected tooa network.</span></span>

* <span data-ttu-id="98e85-148">hello 네트워크 hello에 있어야 hello와 동일한 지역 복구 서비스 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-148">hello network should be in hello same region as hello Recovery Services vault.</span></span>
* <span data-ttu-id="98e85-149">Hello 리소스 모델에 따라 원하는 toouse 장애 조치 Azure Vm에 대 한, hello Azure 네트워크에서 설정한 [Resource Manager 모드](../virtual-network/virtual-networks-create-vnet-arm-pportal.md), 또는 [클래식 모드](../virtual-network/virtual-networks-create-vnet-classic-pportal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-149">Depending on hello resource model you want toouse for failed over Azure VMs, you set up hello Azure network in [Resource Manager mode](../virtual-network/virtual-networks-create-vnet-arm-pportal.md), or [classic mode](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).</span></span>
* <span data-ttu-id="98e85-150">시작하기 전에 네트워크를 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-150">We recommend you set up a network before you begin.</span></span> <span data-ttu-id="98e85-151">Toodo 필요 하지 않으면 사이트 복구 배포 시이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-151">If you don't, you need toodo it during Site Recovery deployment.</span></span>
- <span data-ttu-id="98e85-152">Site Recovery에 의해 사용 되는 저장소 계정 수 없습니다 [이동](../azure-resource-manager/resource-group-move-resources.md) hello 동일 하지만, 또는 간에, 서로 다른 구독 내에서.</span><span class="sxs-lookup"><span data-stu-id="98e85-152">Storage accounts used by Site Recovery can't be [moved](../azure-resource-manager/resource-group-move-resources.md) within hello same, or across different, subscriptions.</span></span>


### <a name="set-up-an-azure-storage-account"></a><span data-ttu-id="98e85-153">Azure 저장소 계정을 설정</span><span class="sxs-lookup"><span data-stu-id="98e85-153">Set up an Azure storage account</span></span>

- <span data-ttu-id="98e85-154">표준/프리미엄 Azure 저장소 계정 toohold 데이터 tooAzure 복제 해야 합니다. [프리미엄 저장소](../storage/storage-premium-storage.md) 계속 높게 IO 성능과 짧은 대기 시간 toohost IO가 많은 작업을 필요로 하는 가상 컴퓨터에 대해 일반적으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-154">You need a standard/premium Azure storage account toohold data replicated tooAzure.[Premium storage](../storage/storage-premium-storage.md) is typically used for virtual machines that need a consistently high IO performance, and low latency toohost IO intensive workloads.</span></span>
- <span data-ttu-id="98e85-155">Toouse 프리미엄 계정 toostore 복제 된 데이터를 캡처 지속적인 tooon 온-프레미스 데이터를 변경 표준 저장소 계정을 toostore 복제 로그를 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-155">If you want toouse a premium account toostore replicated data, you also need a standard storage account toostore replication logs that capture ongoing changes tooon-premises data.</span></span>
- <span data-ttu-id="98e85-156">Hello 리소스 모델에 따라 원하는 toouse 장애 조치 Azure Vm에 대 한에서 계정을 설정한 [Resource Manager 모드](../storage/storage-create-storage-account.md), 또는 [클래식 모드](../storage/storage-create-storage-account-classic-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-156">Depending on hello resource model you want toouse for failed over Azure VMs, you set up an account in [Resource Manager mode](../storage/storage-create-storage-account.md), or [classic mode](../storage/storage-create-storage-account-classic-portal.md).</span></span>
- <span data-ttu-id="98e85-157">시작하기 전에 저장소 계정을 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-157">We recommend that you set up a storage account before you begin.</span></span> <span data-ttu-id="98e85-158">그렇지 않으면 toodo 해야 사이트 복구 배포 시이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-158">If you don't you need toodo it during Site Recovery deployment.</span></span> <span data-ttu-id="98e85-159">hello 계정은 hello에 있어야 hello와 동일한 지역 복구 서비스 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-159">hello accounts must be in hello same region as hello Recovery Services vault.</span></span>
- <span data-ttu-id="98e85-160">저장소 계정에서 사용 되는 사이트 복구 hello 내의 리소스 그룹 동일 이동할 수 없습니다, 구독 또는 다른 구독에서.</span><span class="sxs-lookup"><span data-stu-id="98e85-160">You can't move storage accounts used by Site Recovery across resource groups within hello same subscription, or across different subscriptions.</span></span>


### <a name="prepare-hello-hyper-v-hosts"></a><span data-ttu-id="98e85-161">Hello Hyper-v 호스트를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-161">Prepare hello Hyper-V hosts</span></span>

* <span data-ttu-id="98e85-162">Hello Hyper-v 호스트 hello를 충족 하는지 확인 [필수 구성 요소](site-recovery-prereq.md#disaster-recovery-of-hyper-v-virtual-machines-to-azure-no-virtual-machine-manager)합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-162">Make sure that hello Hyper-V hosts meet hello [prerequisites](site-recovery-prereq.md#disaster-recovery-of-hyper-v-virtual-machines-to-azure-no-virtual-machine-manager).</span></span>
- <span data-ttu-id="98e85-163">Hello 호스트 필요한 hello Url에 액세스할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-163">Make sure that hello hosts can access hello required URLs.</span></span>


## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="98e85-164">복구 서비스 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="98e85-164">Create a Recovery Services vault</span></span>
1. <span data-ttu-id="98e85-165">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-165">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="98e85-166">**새로 만들기** > **모니터링 + 관리** > **Backup 및 Site Recovery(OMS)**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-166">Click **New** > **Monitoring + Management** > **Backup and Site Recovery (OMS)**.</span></span>  

    ![새 자격 증명 모음](./media/site-recovery-hyper-v-site-to-azure/new-vault.png)

3. <span data-ttu-id="98e85-168">**이름**, 이름 tooidentify hello 자격 증명 모음을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-168">In **Name**, specify a friendly name tooidentify hello vault.</span></span> <span data-ttu-id="98e85-169">구독이 두 개 이상인 경우 그 중에서 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-169">If you have more than one subscription, select one of them.</span></span>

4. <span data-ttu-id="98e85-170">[새 리소스 그룹을 만들거나](../azure-resource-manager/resource-group-template-deploy-portal.md) 기존 리소스 그룹을 선택하고 Azure 지역을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-170">[Create a new resource group](../azure-resource-manager/resource-group-template-deploy-portal.md) or select an existing one, and specify an Azure region.</span></span> <span data-ttu-id="98e85-171">컴퓨터는 복제 된 toothis 영역 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-171">Machines will be replicated toothis region.</span></span> <span data-ttu-id="98e85-172">지원 toocheck 지역에서 지역 가용성 참조 [Azure 사이트 복구 가격 정보](https://azure.microsoft.com/pricing/details/site-recovery/)합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-172">toocheck supported regions, see Geographic Availability in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>

5. <span data-ttu-id="98e85-173">Tooquickly 액세스 hello 자격 증명 모음 대시보드 hello에서 클릭 **Pin toodashboard**, 클릭 하 고 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-173">If you want tooquickly access hello vault from hello Dashboard, click **Pin toodashboard**, and then click **Create**.</span></span>

    ![새 자격 증명 모음](./media/site-recovery-hyper-v-site-to-azure/new-vault-settings.png)

<span data-ttu-id="98e85-175">hello에 hello 새 자격 증명 모음 표시 **대시보드** > **모든 리소스** 목록으로 이동한에 주 hello **복구 서비스 자격 증명 모음** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-175">hello new vault appears in hello **Dashboard** > **All resources** list, and on hello main **Recovery Services vaults** blade.</span></span>



## <a name="select-hello-protection-goal"></a><span data-ttu-id="98e85-176">Hello 보호 목표를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-176">Select hello protection goal</span></span>

<span data-ttu-id="98e85-177">대상을 선택 tooreplicate, tooreplicate를 원본 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-177">Select what you want tooreplicate, and where you want tooreplicate to.</span></span>

1. <span data-ttu-id="98e85-178">Hello에 **복구 서비스 자격 증명 모음**선택, hello 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-178">In hello **Recovery Services vaults**, select hello vault.</span></span>
2. <span data-ttu-id="98e85-179">**시작**에서 **Site Recovery** > **인프라 준비** > **보호 목표**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-179">In **Getting Started**, click **Site Recovery** > **Prepare Infrastructure** > **Protection goal**.</span></span>

    ![목표 선택](./media/site-recovery-hyper-v-site-to-azure/choose-goals.png)
3. <span data-ttu-id="98e85-181">**보호 목표**선택, **tooAzure**, 선택 하 고 **Hyper-v와 함께 예,**합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-181">In **Protection goal**, select **tooAzure**, and select **Yes, with Hyper-V**.</span></span> <span data-ttu-id="98e85-182">선택 **아니요** tooconfirm VMM을 사용 하지 않는다고 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-182">Select **No** tooconfirm you're not using VMM.</span></span> <span data-ttu-id="98e85-183">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-183">Then click **OK**.</span></span>

    ![목표 선택](./media/site-recovery-hyper-v-site-to-azure/choose-goals2.png)

## <a name="set-up-hello-source-environment"></a><span data-ttu-id="98e85-185">Hello 소스 환경 설정</span><span class="sxs-lookup"><span data-stu-id="98e85-185">Set up hello source environment</span></span>

<span data-ttu-id="98e85-186">Hello 하이퍼-V 사이트를 설정 하 고, Hyper-v 호스트에 hello Azure Site Recovery Provider 및 hello Azure 복구 서비스 에이전트를 설치 하 고 및 hello 사이트 hello 자격 증명 모음에 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-186">Set up hello Hyper-V site, install hello Azure Site Recovery Provider and hello Azure Recovery Services agent on Hyper-V hosts, and register hello site in hello vault.</span></span>

1. <span data-ttu-id="98e85-187">**인프라 준비**에서 **원본**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-187">In **Prepare Infrastructure**, click **Source**.</span></span> <span data-ttu-id="98e85-188">새 Hyper-v 사이트에 Hyper-v 호스트 또는 클러스터에 대 한 컨테이너로 tooadd 클릭 **+ Hyper-v 사이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-188">tooadd a new Hyper-V site as a container for your Hyper-V hosts or clusters, click **+Hyper-V Site**.</span></span>

    ![원본 설정](./media/site-recovery-hyper-v-site-to-azure/set-source1.png)
2. <span data-ttu-id="98e85-190">**만들 Hyper-v 사이트**, hello 사이트에 대 한 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-190">In **Create Hyper-V site**, specify a name for hello site.</span></span> <span data-ttu-id="98e85-191">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-191">Then click **OK**.</span></span> <span data-ttu-id="98e85-192">이제 작성 하 고 클릭 하 여 hello 사이트를 선택 **+ Hyper-v 서버** tooadd 서버 toohello 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-192">Now, select hello site you created, and click **+Hyper-V Server** tooadd a server toohello site.</span></span>

    ![원본 설정](./media/site-recovery-hyper-v-site-to-azure/set-source2.png)

3. <span data-ttu-id="98e85-194">**서버 추가** > **서버 형식**에 **Hyper-V 서버**가 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-194">In **Add Server** > **Server type**, check that **Hyper-V server** is displayed.</span></span>

    - <span data-ttu-id="98e85-195">Tooadd hello를 준수 하는 것이 원하는 hello Hyper-v server에 해당 하는지 확인 한 [필수 구성 요소](#on-premises-prerequisites), 및가 수 tooaccess hello 지정 된 Url입니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-195">Make sure that hello Hyper-V server you want tooadd complies with hello [prerequisites](#on-premises-prerequisites), and is able tooaccess hello specified URLs.</span></span>
    - <span data-ttu-id="98e85-196">Hello Azure Site Recovery Provider 설치 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-196">Download hello Azure Site Recovery Provider installation file.</span></span> <span data-ttu-id="98e85-197">이 파일 tooinstall hello 공급자를 실행 하 고 각 Hyper-v 호스트에서 복구 서비스 에이전트 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-197">You run this file tooinstall hello Provider and hello Recovery Services agent on each Hyper-V host.</span></span>

    ![원본 설정](./media/site-recovery-hyper-v-site-to-azure/set-source3.png)


## <a name="install-hello-provider-and-agent"></a><span data-ttu-id="98e85-199">Hello 공급자 및 에이전트 설치</span><span class="sxs-lookup"><span data-stu-id="98e85-199">Install hello Provider and agent</span></span>

1. <span data-ttu-id="98e85-200">Toohello 하이퍼-V 사이트를 추가 각 호스트에서 hello 공급자 설치 파일을 실행 했습니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-200">Run hello Provider setup file on each host you added toohello Hyper-V site.</span></span> <span data-ttu-id="98e85-201">Hyper-V 클러스터에 설치하는 경우 각 클러스터 노드에서 설치 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-201">If you're installing on a Hyper-V cluster, run setup on each cluster node.</span></span> <span data-ttu-id="98e85-202">각 Hyper-V 클러스터 노드를 설치하고 등록하면 노드 간 마이그레이션에서도 VM이 안전하게 보호됩니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-202">Installing and registering each Hyper-V cluster node ensures that VMs are protected, even if they migrate across nodes.</span></span>
2. <span data-ttu-id="98e85-203">Microsoft Update 정책에 따라 공급자 업데이트가 설치되도록 **Microsoft Update**에서 업데이트를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-203">In **Microsoft Update**, you can opt in for updates so that Provider updates are installed in accordance with your Microsoft Update policy.</span></span>
3. <span data-ttu-id="98e85-204">**설치**, 수락 하거나 hello 기본 공급자 설치 위치를 수정 하 고 클릭 **설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-204">In **Installation**, accept or modify hello default Provider installation location and click **Install**.</span></span>
4. <span data-ttu-id="98e85-205">**자격 증명 모음 설정을**, 클릭 **찾아보기** tooselect hello 자격 증명 모음 키 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-205">In **Vault Settings**, click **Browse** tooselect hello vault key file that you downloaded.</span></span> <span data-ttu-id="98e85-206">Hello Azure Site Recovery 구독 hello 자격 증명 모음 이름을 지정 하 고 hello 하이퍼-V 사이트 toowhich hello Hyper-v 서버가 속하는 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-206">Specify hello Azure Site Recovery subscription, hello vault name, and hello Hyper-V site toowhich hello Hyper-V server belongs.</span></span>

    ![서버 등록](./media/site-recovery-hyper-v-site-to-azure/provider3.png)

5. <span data-ttu-id="98e85-208">**프록시 설정을**, Hyper-v 호스트에서 실행 중인 공급자를 통해 tooAzure 사이트 복구를 연결 하는 hello 인터넷 hello 하는 방법을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-208">In **Proxy Settings**, specify how hello Provider running on Hyper-V hosts connects tooAzure Site Recovery over hello internet.</span></span>

    * <span data-ttu-id="98e85-209">Hello 공급자 tooconnect 직접 선택 하려면 **tooAzure Site Recovery 프록시 없이 직접 연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-209">If you want hello Provider tooconnect directly select **Connect directly tooAzure Site Recovery without a proxy**.</span></span>
    * <span data-ttu-id="98e85-210">기존 프록시 인증 필요 hello 공급자 연결에 대 한 사용자 지정 프록시 toouse를 원하는 경우 선택 **연결에서 프록시 서버를 사용 하 여 사이트 복구 tooAzure**합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-210">If your existing proxy requires authentication, or you want toouse a custom proxy for hello Provider connection, select **Connect tooAzure Site Recovery using a proxy server**.</span></span>
    * <span data-ttu-id="98e85-211">프록시를 사용하는 경우:</span><span class="sxs-lookup"><span data-stu-id="98e85-211">If you use a proxy:</span></span>
        - <span data-ttu-id="98e85-212">Hello 주소, 포트 및 자격 증명을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-212">Specify hello address, port, and credentials</span></span>
        - <span data-ttu-id="98e85-213">Hello에 설명 된 있는지 hello Url 확인 [필수 구성 요소](#prerequisites) hello 프록시를 통해 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-213">Make sure hello URLs described in hello [prerequisites](#prerequisites) are allowed through hello proxy.</span></span>

    ![인터넷](./media/site-recovery-hyper-v-site-to-azure/provider7.PNG)

6. <span data-ttu-id="98e85-215">설치를 마친 후 클릭 **등록** tooregister hello 서버 hello 자격 증명 모음에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-215">After installation finishes, click **Register** tooregister hello server in hello vault.</span></span>

    ![설치 위치](./media/site-recovery-hyper-v-site-to-azure/provider2.png)

7. <span data-ttu-id="98e85-217">등록 완료 되 면 hello Hyper-v 서버에서 메타 데이터를 Azure Site Recovery에서 검색 되 고 hello 서버에 표시 되 **사이트 복구 인프라** > **Hyper-v 호스트**합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-217">After registration finishes, metadata from hello Hyper-V server is retrieved by Azure Site Recovery, and hello server is displayed in **Site Recovery Infrastructure** > **Hyper-V Hosts**.</span></span>


## <a name="set-up-hello-target-environment"></a><span data-ttu-id="98e85-218">Hello 대상 환경 설정</span><span class="sxs-lookup"><span data-stu-id="98e85-218">Set up hello target environment</span></span>

<span data-ttu-id="98e85-219">복제에 대 한 hello Azure 저장소 계정을 지정 하 고 hello Azure 네트워크 toowhich Azure Vm 장애 조치 후 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-219">Specify hello Azure storage account for replication, and hello Azure network toowhich Azure VMs will connect after failover.</span></span>

1. <span data-ttu-id="98e85-220">**인프라 준비** > **대상**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-220">Click **Prepare infrastructure** > **Target**.</span></span>
2. <span data-ttu-id="98e85-221">Hello 구독 및 장애 조치 후 toocreate hello Azure Vm 만들려는 hello 리소스 그룹을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-221">Select hello subscription and hello resource group in which you want toocreate hello Azure VMs after failover.</span></span> <span data-ttu-id="98e85-222">Hello 배포 선택 hello Vm에 대 한 Azure (기본 또는 리소스 관리)에서 toouse 되도록 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-222">Choose hello deployment model that you want toouse in Azure (classic or resource management) for hello VMs.</span></span>

3. <span data-ttu-id="98e85-223">Site Recovery가 호환되는 Azure 저장소 계정 및 네트워크가 하나 이상 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-223">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

    - <span data-ttu-id="98e85-224">저장소 계정에 없으면 클릭 **+ 저장소** toocreate 리소스 관리자 기반 계정 인라인 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-224">If you don't have a storage account, click **+Storage** toocreate a Resource Manager-based account inline.</span></span> <span data-ttu-id="98e85-225">[저장소 요구 사항](site-recovery-prereq.md#azure-requirements)을 읽어 보세요.</span><span class="sxs-lookup"><span data-stu-id="98e85-225">Read about [storage requirements](site-recovery-prereq.md#azure-requirements).</span></span>
    - <span data-ttu-id="98e85-226">Azure 네트워크를 설정 하지 않은 경우 클릭 **+ 네트워크** toocreate 리소스 관리자 기반 네트워크 인라인 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-226">If you don't have a Azure network, click **+Network** toocreate a Resource Manager-based network inline.</span></span>

    ![저장소](./media/site-recovery-vmware-to-azure/enable-rep3.png)




## <a name="configure-replication-settings"></a><span data-ttu-id="98e85-228">복제 설정 구성</span><span class="sxs-lookup"><span data-stu-id="98e85-228">Configure replication settings</span></span>

1. <span data-ttu-id="98e85-229">새 복제 정책을 toocreate 클릭 **준비 인프라** > **복제 설정을** > **+ 만들기 및 연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-229">toocreate a new replication policy, click **Prepare infrastructure** > **Replication Settings** > **+Create and associate**.</span></span>

    ![네트워크](./media/site-recovery-hyper-v-site-to-azure/gs-replication.png)
2. <span data-ttu-id="98e85-231">**만들기 및 연결 정책**에서 정책 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-231">In **Create and associate policy**, specify a policy name.</span></span>
3. <span data-ttu-id="98e85-232">**복사 빈도**를 얼마나 자주 hello 초기 복제 (30 초 마다, 5 분 또는 15 분) 후 tooreplicate 델타 데이터를 원하는 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-232">In **Copy frequency**, specify how often you want tooreplicate delta data after hello initial replication (every 30 seconds, 5 or 15 minutes).</span></span>

    > [!NOTE]
    > <span data-ttu-id="98e85-233">두 번째 30 주파수 toopremium 저장소를 복제할 때 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-233">A 30 second frequency isn't supported when replicating toopremium storage.</span></span> <span data-ttu-id="98e85-234">hello 제한 프리미엄 저장소에서 지 원하는 (100) blob 당 스냅숏 hello 수로 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-234">hello limitation is determined by hello number of snapshots per blob (100) supported by premium storage.</span></span> <span data-ttu-id="98e85-235">[자세히 알아봅니다](../storage/storage-premium-storage.md#snapshots-and-copy-blob).</span><span class="sxs-lookup"><span data-stu-id="98e85-235">[Learn more](../storage/storage-premium-storage.md#snapshots-and-copy-blob).</span></span>

4. <span data-ttu-id="98e85-236">**복구 지점 보존**, 시간 길이 지정 hello 보존 기간은 각 복구 지점에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-236">In **Recovery point retention**, specify in hours how long hello retention window is for each recovery point.</span></span> <span data-ttu-id="98e85-237">Vm 수 tooany 지점 창 내에서 복구 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-237">VMs can be recovered tooany point within a window.</span></span>
5. <span data-ttu-id="98e85-238">**앱 일치 스냅숏 빈도**에서 응용 프로그램 일치 스냅숏이 포함된 복구 지점을 만드는 빈도(1~12시간)를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-238">In **App-consistent snapshot frequency**, specify how frequently (1-12 hours) recovery points containing application-consistent snapshots are created.</span></span>

    - <span data-ttu-id="98e85-239">Hyper-v에서는 두 가지 유형의 스냅숏 사용-hello 전체 가상 컴퓨터의 증분 스냅숏을 제공 하는 표준 스냅숏 및 hello hello 가상 컴퓨터 응용 프로그램 데이터의 지정 시간 스냅숏을 생성 하는 응용 프로그램에 일관 된 스냅숏입니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-239">Hyper-V uses two types of snapshots — a standard snapshot that provides an incremental snapshot of hello entire virtual machine, and an application-consistent snapshot that takes a point-in-time snapshot of hello application data inside hello virtual machine.</span></span>
    - <span data-ttu-id="98e85-240">응용 프로그램에 일관 된 스냅숏의 hello 스냅숏이 만들어질 때 응용 프로그램은 일관 된 상태에서 볼륨 섀도 복사본 서비스 (VSS) tooensure를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-240">Application-consistent snapshots use Volume Shadow Copy Service (VSS) tooensure that applications are in a consistent state when hello snapshot is taken.</span></span>
    - <span data-ttu-id="98e85-241">응용 프로그램 일치 스냅숏을 사용할 경우 원본 가상 컴퓨터에서 실행 중인 응용 프로그램의 hello 성능이 저하 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-241">If you enable application-consistent snapshots, it will affect hello performance of applications running on source virtual machines.</span></span> <span data-ttu-id="98e85-242">설정한 hello 값 hello 구성 하는 추가 복구 지점 개수 보다 작은지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="98e85-242">Ensure that hello value you set is less than hello number of additional recovery points you configure.</span></span>

6. <span data-ttu-id="98e85-243">**초기 복제 시작 시간**때 toostart hello 초기 복제를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-243">In **Initial replication start time**, specify when toostart hello initial replication.</span></span> <span data-ttu-id="98e85-244">hello 복제 하므로 tooschedule 해도 인터넷 대역폭을 통해 발생 사용 중인 시간 외 것입니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-244">hello replication occurs over your internet bandwidth so you might want tooschedule it outside your busy hours.</span></span> <span data-ttu-id="98e85-245">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-245">Then click **OK**.</span></span>

    ![복제 정책](./media/site-recovery-hyper-v-site-to-azure/gs-replication2.png)

<span data-ttu-id="98e85-247">새 정책을 만들 때 자동으로 hello Hyper-v 사이트와 연결 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-247">When you create a new policy, it's automatically associated with hello Hyper-V site.</span></span> <span data-ttu-id="98e85-248">Hyper-v 사이트 (및 그 안에 hello Vm)에서 여러 복제 정책을 연결할 수 있습니다 **복제** > 정책 이름 > **Hyper-v 사이트 연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-248">You can associate a Hyper-V site (and hello VMs in it) with multiple replication policies in **Replication** > policy-name > **Associate Hyper-V Site**.</span></span>

## <a name="capacity-planning"></a><span data-ttu-id="98e85-249">용량 계획</span><span class="sxs-lookup"><span data-stu-id="98e85-249">Capacity planning</span></span>

<span data-ttu-id="98e85-250">기본 인프라를 설치했으니 용량 계획에 대해 생각해 보고 추가 리소스가 필요한지 파악할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-250">Now that you have your basic infrastructure set up, you can think about capacity planning, and figure out whether you need additional resources.</span></span>

<span data-ttu-id="98e85-251">사이트 복구를 사용 하는 용량 플래너 toohelp 계산, 네트워킹 및 저장소에 대 한 hello 오른쪽 리소스를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-251">Site Recovery provides a capacity planner toohelp you allocate hello right resources for compute, networking, and storage.</span></span> <span data-ttu-id="98e85-252">사용자 지정 된 숫자 값을 hello 작업 수준에서 hello 플래너를 Vm, 디스크 및 저장소는 평균 수에 따라 예상에 대 한 빠른 모드에서 detailed 모드에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-252">You can run hello planner in quick mode for estimations based on an average number of VMs, disks, and storage, or in detailed mode with customized numbers at hello workload level.</span></span> <span data-ttu-id="98e85-253">시작하기 전에 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-253">Before you start you need to:</span></span>

* <span data-ttu-id="98e85-254">VM, VM당 디스크, 디스크당 저장소를 포함하여 복제 환경에 대한 정보를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-254">Gather information about your replication environment, including VMs, disks per VMs, and storage per disk.</span></span>
* <span data-ttu-id="98e85-255">복제 된 데이터에 대 한 hello 매일 변경 (변동) 속도 예측 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-255">Estimate hello daily change (churn) rate for your replicated data.</span></span> <span data-ttu-id="98e85-256">Hello를 사용할 수 있습니다 [Hyper-v 복제본 용량 플래너](https://www.microsoft.com/download/details.aspx?id=39057) toohelp이 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-256">You can use hello [Capacity Planner for Hyper-V Replica](https://www.microsoft.com/download/details.aspx?id=39057) toohelp you do this.</span></span>

1. <span data-ttu-id="98e85-257">클릭 **다운로드** toodownload hello 도구를 한 다음를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-257">Click **Download** toodownload hello tool, and then run it.</span></span> <span data-ttu-id="98e85-258">[Hello 문서 읽기](site-recovery-capacity-planner.md) hello 도구와 함께 제공 되는 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-258">[Read hello article](site-recovery-capacity-planner.md) that accompanies hello tool.</span></span>
2. <span data-ttu-id="98e85-259">완료 되 면 선택 **예** 에 **hello Capacity Planner를 실행 한**?</span><span class="sxs-lookup"><span data-stu-id="98e85-259">When you’re done, select **Yes** in **Have you run hello Capacity Planner**?</span></span>

   ![용량 계획](./media/site-recovery-hyper-v-site-to-azure/gs-capacity-planning.png)

<span data-ttu-id="98e85-261">[네트워크 대역폭 제어](#network-bandwidth-considerations)에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="98e85-261">Learn more about [controlling network bandwidth](#network-bandwidth-considerations)</span></span>



## <a name="enable-replication"></a><span data-ttu-id="98e85-262">복제 활성화</span><span class="sxs-lookup"><span data-stu-id="98e85-262">Enable replication</span></span>

<span data-ttu-id="98e85-263">시작 하기 전에 Azure 사용자 계정에 필요한 hello에 있는지 확인 [권한을](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) 새 가상 컴퓨터 tooAzure의 tooenable 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-263">Before you start, ensure that your Azure user account has hello required  [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replication of a new virtual machine tooAzure.</span></span>

<span data-ttu-id="98e85-264">다음과 같이 VM에 대해 복제를 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-264">Enable replication for VMs as follows:</span></span>          

1. <span data-ttu-id="98e85-265">**응용 프로그램 복제** > **원본**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-265">Click **Replicate application** > **Source**.</span></span> <span data-ttu-id="98e85-266">처음으로 hello에 대 한 복제를 설정한 후 클릭 **복제 +** 추가 컴퓨터에 대 한 tooenable 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-266">After you've set up replication for hello first time, you can click **+Replicate** tooenable replication for additional machines.</span></span>

    ![복제 활성화](./media/site-recovery-hyper-v-site-to-azure/enable-replication.png)
2. <span data-ttu-id="98e85-268">**소스**선택, hello 하이퍼-V 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-268">In **Source**, select hello Hyper-V site.</span></span> <span data-ttu-id="98e85-269">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-269">Then click **OK**.</span></span>
3. <span data-ttu-id="98e85-270">**대상**hello toouse Azure (기본 또는 리소스 관리)에서 장애 조치 후 원하는 장애 조치 모델을 hello 자격 증명 모음 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-270">In **Target**, select hello vault subscription, and hello failover model you want toouse in Azure (classic or resource management) after failover.</span></span>
4. <span data-ttu-id="98e85-271">원하는 toouse hello 저장소 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-271">Select hello storage account you want toouse.</span></span> <span data-ttu-id="98e85-272">Toouse 원하는 계정을 없는 경우 다음을 할 수 있습니다 [만드세요](#set-up-an-azure-storage-account)합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-272">If you don't have an account you want toouse, you can [create one](#set-up-an-azure-storage-account).</span></span> <span data-ttu-id="98e85-273">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-273">Then click **OK**.</span></span>
5. <span data-ttu-id="98e85-274">선택 hello Azure 네트워크와 서브넷 toowhich Azure Vm 장애 조치 만들 때 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-274">Select hello Azure network and subnet toowhich Azure VMs will connect when they're created failover.</span></span>

    - <span data-ttu-id="98e85-275">tooapply hello 네트워크 설정을 tooall 컴퓨터 사용 하도록 설정 하면 복제를 위해 선택 **선택한 컴퓨터에 지금 구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-275">tooapply hello network settings tooall machines you enable for replication, select **Configure now for selected machines**.</span></span>
    - <span data-ttu-id="98e85-276">선택 **나중에 구성** tooselect hello 컴퓨터당 Azure 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-276">Select **Configure later** tooselect hello Azure network per machine.</span></span>
    - <span data-ttu-id="98e85-277">Toouse 원하는 네트워크를 설정 하지 않은 경우 다음을 할 수 있습니다 [만드세요](#set-up-an-azure-network)합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-277">If you don't have a network you want toouse, you can [create one](#set-up-an-azure-network).</span></span> <span data-ttu-id="98e85-278">해당하는 경우 서브넷을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-278">Select a subnet if applicable.</span></span> <span data-ttu-id="98e85-279">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-279">Then click **OK**.</span></span>

   ![복제 활성화](./media/site-recovery-hyper-v-site-to-azure/enable-replication11.png)

6. <span data-ttu-id="98e85-281">**가상 컴퓨터** > **가상 컴퓨터 선택**, 클릭 하 고 tooreplicate 사용할 각 컴퓨터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-281">In **Virtual Machines** > **Select virtual machines**, click and select each machine you want tooreplicate.</span></span> <span data-ttu-id="98e85-282">복제를 활성화할 수 있는 컴퓨터만 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-282">You can only select machines for which replication can be enabled.</span></span> <span data-ttu-id="98e85-283">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-283">Then click **OK**.</span></span>

    ![복제 활성화](./media/site-recovery-hyper-v-site-to-azure/enable-replication5-for-exclude-disk.png)

7. <span data-ttu-id="98e85-285">**속성** > **속성 구성**OS 디스크 hello을 hello 선택한 Vm에 대 한 hello 운영 체제를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-285">In **Properties** > **Configure properties**, select hello operating system for hello selected VMs, and hello OS disk.</span></span>
8. <span data-ttu-id="98e85-286">해당 hello Azure VM 이름 (대상 이름)을 준수 확인 [Azure 가상 컴퓨터 요구 사항을](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-286">Verify that hello Azure VM name (target name) complies with [Azure virtual machine requirements](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>
9. <span data-ttu-id="98e85-287">기본적으로 모든 hello 디스크 hello VM의 복제를 위해 선택 하지만 디스크 tooexclude 지울 수 있습니다 이러한.</span><span class="sxs-lookup"><span data-stu-id="98e85-287">By default all hello disks of hello VM are selected for replication, but you can clear disks tooexclude them.</span></span>
    - <span data-ttu-id="98e85-288">Tooexclude 디스크 tooreduce 복제 대역폭을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-288">You might want tooexclude disks tooreduce replication bandwidth.</span></span> <span data-ttu-id="98e85-289">예를 들어 임시 데이터로 tooreplicate 디스크 원하지 않을 수 있습니다 또는 (예: pagefile.sys 또는 Microsoft SQL Server tempdb)가 새로 고쳐질 때마다 컴퓨터나 응용 프로그램 데이터를 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-289">For example, you might not want tooreplicate disks with temporary data, or data that's refreshed each time a machine or apps restarts (such as pagefile.sys or Microsoft SQL Server tempdb).</span></span> <span data-ttu-id="98e85-290">Hello 디스크 선택을 취소 하 여 hello 디스크 복제에서 제외할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-290">You can exclude hello disk from replication by unselecting hello disk.</span></span>
    - <span data-ttu-id="98e85-291">기본 디스크만 제외할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-291">Only basic disks can be exclude.</span></span> <span data-ttu-id="98e85-292">OS 디스크는 제외할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-292">You can't exclude OS disks.</span></span>
    - <span data-ttu-id="98e85-293">동적 디스크는 제외하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-293">We recommend that you don't exclude dynamic disks.</span></span> <span data-ttu-id="98e85-294">Site Recovery는 게스트 VM 내의 가상 하드 디스크가 기본 디스크인지 아니면 동적 디스크인지 식별할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-294">Site Recovery can't identify whether a virtual hard disk inside a guest VM is basic or dynamic.</span></span> <span data-ttu-id="98e85-295">모든 종속 동적 볼륨 디스크 제외 되지 않으면 hello VM 장애 조치, 되 고 hello 해당 디스크에 액세스할 수 없게 하는 경우 실패 한 디스크 hello 보호 된 동적 디스크가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-295">If all dependent dynamic volume disks aren't excluded, hello protected dynamic disk will show as a failed disk when hello VM fails over, and hello data on that disk won't be accessible.</span></span>
        - <span data-ttu-id="98e85-296">복제를 사용하도록 설정한 후 복제에 대해 디스크를 추가 또는 제거할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-296">After replication is enabled, you can't add or remove disks for replication.</span></span> <span data-ttu-id="98e85-297">Tooadd 원하는 디스크를 제외 하거나, hello VM toodisable 보호 해야 하 고 다시 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-297">If you want tooadd or exclude a disk, you need toodisable protection for hello VM, and then re-enable it.</span></span>
        - <span data-ttu-id="98e85-298">Azure에서 수동으로 만드는 디스크는 장애 복구되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-298">Disks you create manually in Azure aren't failed back.</span></span> <span data-ttu-id="98e85-299">예를 들어 세 디스크 실패 하 고 Azure VM에 직접 두 개 만든 경우 Azure tooHyper-V에서 다시 hello 세 디스크만 장애 조치 된 장애 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-299">For example, if you fail over three disks, and create two directly in Azure VM, only hello three disks which were failed over will be failed back from Azure tooHyper-V.</span></span> <span data-ttu-id="98e85-300">장애 복구 또는 Hyper-v tooAzure에서 역방향 복제를 수동으로 만든 디스크를 포함할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-300">You can't include disks created manually in failback, or in reverse replication from Hyper-V tooAzure.</span></span>
        - <span data-ttu-id="98e85-301">응용 프로그램 toooperate에 필요한 디스크를 제외 하면 후 장애 조치 tooAzure 해야 toocreate Azure 때문에 해당 hello 복제 응용 프로그램에서 수동으로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-301">If you exclude a disk that's needed for an application toooperate, after failover tooAzure you need toocreate it manually in Azure, so that hello replicated application can run.</span></span> <span data-ttu-id="98e85-302">또는 Azure 자동화 hello 컴퓨터의 장애 조치 중 toocreate hello 디스크 복구 계획을 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-302">Alternatively, you could integrate Azure automation into a recovery plan, toocreate hello disk during failover of hello machine.</span></span>

10. <span data-ttu-id="98e85-303">클릭 **확인** toosave 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-303">Click **OK** toosave changes.</span></span> <span data-ttu-id="98e85-304">나중에 추가 속성을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-304">You can set additional properties later.</span></span>

    ![복제 활성화](./media/site-recovery-hyper-v-site-to-azure/enable-replication6-with-exclude-disk.png)

11. <span data-ttu-id="98e85-306">**복제 설정을** > **복제 설정을 구성**, hello Vm 보호 된 원하는 tooapply hello 복제 정책을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-306">In **Replication settings** > **Configure replication settings**, select hello replication policy you want tooapply for hello protected VMs.</span></span> <span data-ttu-id="98e85-307">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-307">Then click **OK**.</span></span> <span data-ttu-id="98e85-308">hello 복제 정책을 수정할 수 있습니다 **복제 정책** > 정책 이름 > **설정 편집**합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-308">You can modify hello replication policy in **Replication policies** > policy-name > **Edit Settings**.</span></span> <span data-ttu-id="98e85-309">적용하는 변경 사항은 이미 복제 중인 컴퓨터와 새 컴퓨터에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-309">Changes you apply will be used for machines that are already replicating, and new machines.</span></span>


   ![복제 활성화](./media/site-recovery-hyper-v-site-to-azure/enable-replication7.png)

<span data-ttu-id="98e85-311">Hello의 진행률을 추적할 수 있습니다 **보호 사용** 작업 **작업** > **사이트 복구 작업이**합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-311">You can track progress of hello **Enable Protection** job in **Jobs** > **Site Recovery jobs**.</span></span> <span data-ttu-id="98e85-312">Hello 후 **보호 완료** 실행 작업 hello 컴퓨터는 장애 조치에 대해 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-312">After hello **Finalize Protection** job runs hello machine is ready for failover.</span></span>

### <a name="view-and-manage-vm-properties"></a><span data-ttu-id="98e85-313">VM 속성 보기 및 관리</span><span class="sxs-lookup"><span data-stu-id="98e85-313">View and manage VM properties</span></span>

<span data-ttu-id="98e85-314">Hello 원본 컴퓨터의 hello 속성을 확인 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-314">We recommend that you verify hello properties of hello source machine.</span></span>

1. <span data-ttu-id="98e85-315">**보호 된 항목**, 클릭 **복제 항목**, 및 select hello 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-315">In **Protected Items**, click **Replicated Items**, and select hello machine.</span></span>

    ![복제 활성화](./media/site-recovery-hyper-v-site-to-azure/test-failover1.png)
2. <span data-ttu-id="98e85-317">**속성**및 복제를 볼 수 있습니다에 대 한 장애 조치 정보 hello VM입니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-317">In **Properties**, you can view replication and failover information for hello VM.</span></span>

    ![복제 활성화](./media/site-recovery-hyper-v-site-to-azure/test-failover2.png)
3. <span data-ttu-id="98e85-319">**계산 및 네트워크** > **속성 계산**, hello Azure VM 이름 및 대상 크기를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-319">In **Compute and Network** > **Compute properties**, you can specify hello Azure VM name and target size.</span></span> <span data-ttu-id="98e85-320">Azure 요구 사항에 hello 이름 toocomply 해야 할 경우 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-320">Modify hello name toocomply with Azure requirements if you need to.</span></span> <span data-ttu-id="98e85-321">또한 보고 및 hello 대상 네트워크, 서브넷 및 IP 주소를 할당할 toohello Azure VM에 대 한 정보를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-321">You can also view and modify information about hello target network, subnet, and IP address that will be assigned toohello Azure VM.</span></span> <span data-ttu-id="98e85-322">참고 hello 다음.</span><span class="sxs-lookup"><span data-stu-id="98e85-322">Note hello following:</span></span>

   * <span data-ttu-id="98e85-323">Hello 대상 IP 주소를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-323">You can set hello target IP address.</span></span> <span data-ttu-id="98e85-324">주소를 제공 하지 않으면 장애 조치 컴퓨터 hello DHCP를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-324">If you don't provide an address, hello failed over machine will use DHCP.</span></span> <span data-ttu-id="98e85-325">장애 조치에 사용할 수 없는 주소를 설정 하는 경우 hello 장애 조치가 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-325">If you set an address that isn't available at failover, hello failover will fail.</span></span> <span data-ttu-id="98e85-326">hello hello 주소는 hello 테스트 장애 조치 네트워크에서 사용할 수 있는 하는 경우 테스트 장애 조치에 대해 동일한 대상 IP 주소를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-326">hello same target IP address can be used for test failover if hello address is available in hello test failover network.</span></span>
   * <span data-ttu-id="98e85-327">네트워크 어댑터의 hello 수는 다음과 같이 hello 대상 가상 컴퓨터에 대해 지정 하는 hello 크기에 따라 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-327">hello number of network adapters is dictated by hello size you specify for hello target virtual machine, as follows:</span></span>

     * <span data-ttu-id="98e85-328">Hello hello 원본 컴퓨터의 네트워크 어댑터 수가 보다 작거나 같은 경우 hello 대상 컴퓨터 크기에 허용 되는 어댑터 수가 toohello 다음 hello 대상 갖습니다 hello hello 소스와 같은 수의 어댑터.</span><span class="sxs-lookup"><span data-stu-id="98e85-328">If hello number of network adapters on hello source machine is less than or equal toohello number of adapters allowed for hello target machine size, then hello target will have hello same number of adapters as hello source.</span></span>
     * <span data-ttu-id="98e85-329">Hello 원본 가상 컴퓨터에 대 한 어댑터의 hello 수를 초과 하면 hello 수 수 hello 대상 크기 다음 hello 대상 크기는 최대 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-329">If hello number of adapters for hello source virtual machine exceeds hello number allowed for hello target size then hello target size maximum will be used.</span></span>
     * <span data-ttu-id="98e85-330">예를 들어 원본 컴퓨터에 네트워크 어댑터가 두 개 및 4 hello 대상 컴퓨터 크기 지원로 hello 대상 컴퓨터는 두 개의 어댑터를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-330">For example if a source machine has two network adapters and hello target machine size supports four, hello target machine will have two adapters.</span></span> <span data-ttu-id="98e85-331">Hello 원본 컴퓨터에 두 개의 어댑터가 있지만 hello 지원 되는 대상 크기 하나만 지원 하는 경우 hello 대상 컴퓨터에서 하나의 어댑터를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-331">If hello source machine has two adapters but hello supported target size only supports one then hello target machine will have only one adapter.</span></span>     
     * <span data-ttu-id="98e85-332">Hello VM에 여러 네트워크 어댑터는 모든 연결 toohello 동일한 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-332">If hello VM has multiple network adapters they will all connect toohello same network.</span></span>
     * <span data-ttu-id="98e85-333">Hello 가상 컴퓨터에 여러 네트워크 어댑터가 다음 hello 경우 먼저 하나 hello 목록에 표시 될 hello *기본* hello Azure 가상 컴퓨터의에서 네트워크 어댑터입니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-333">If hello virtual machine has multiple network adapters then hello first one shown in hello list becomes hello *Default* network adapter in hello Azure virtual machine.</span></span>

     ![복제 활성화](./media/site-recovery-hyper-v-site-to-azure/test-failover4.png)

4. <span data-ttu-id="98e85-335">**디스크**, hello 운영 체제를 확인할 수 있습니다 및 데이터 디스크에 hello VM에 복제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-335">In **Disks**, you can see hello operating system and data disks on hello VM that will be replicated.</span></span>

#### <a name="managed-disks"></a><span data-ttu-id="98e85-336">관리 디스크</span><span class="sxs-lookup"><span data-stu-id="98e85-336">Managed disks</span></span>

<span data-ttu-id="98e85-337">**계산 및 네트워크** > **속성 계산**, 마이그레이션 tooAzure에서 관리 하는 디스크 tooyour 컴퓨터 tooattach hello VM에 대 한 너무 "Yes" 설정 "디스크 관리 되는 사용"을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-337">In **Compute and Network** > **Compute properties**, you can set "Use managed disks" setting too"Yes" for hello VM if you want tooattach managed disks tooyour machine on migration tooAzure.</span></span> <span data-ttu-id="98e85-338">관리 되는 디스크 hello VM 디스크와 연결 된 hello 저장소 계정을 관리 하 여 Azure IaaS Vm에 대 한 디스크 관리를 간소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-338">Managed disks simplifies disk management for Azure IaaS VMs by managing hello storage accounts associated with hello VM disks.</span></span> <span data-ttu-id="98e85-339">[Managed Disks에 대한 자세히 알아봅니다](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview).</span><span class="sxs-lookup"><span data-stu-id="98e85-339">[Learn More about managed disks](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview).</span></span>

   - <span data-ttu-id="98e85-340">관리 되는 디스크는 장애 조치 tooAzure에 대해서만 생성 되 고 연결 된 toohello 가상 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-340">Managed disks are created and attached toohello virtual machine only on a failover tooAzure.</span></span> <span data-ttu-id="98e85-341">보호를 사용 하도록 설정 하면, 온-프레미스 컴퓨터의에서 데이터를 tooreplicate toostorage 계정을 계속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-341">On enabling protection, data from on-premises machines will continue tooreplicate toostorage accounts.</span></span>
   <span data-ttu-id="98e85-342">Hello 리소스 관리자 배포 모델을 사용 하 여 배포 된 가상 컴퓨터에 대해서만 관리 하는 디스크를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-342">Managed disks can be created only for virtual machines deployed using hello Resource manager deployment model.</span></span>

  > [!NOTE]
  > <span data-ttu-id="98e85-343">관리 되는 디스크를 사용 하 여 컴퓨터에 대 한 장애 복구 Azure tooon 온-프레미스 Hyper-v 환경에서 현재 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-343">Failback from Azure tooon-premises Hyper-V environment is not currently supported for machines with managed disks.</span></span> <span data-ttu-id="98e85-344">"디스크 관리 되는 사용" 너무 "예"로 설정 toomigrate이 컴퓨터 tooAzure를 가져오려는 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-344">Set "Use managed disks" too"Yes" only if you intend toomigrate this machine tooAzure.</span></span>

   - <span data-ttu-id="98e85-345">너무 "Yes" "디스크 관리 되는 사용"을 설정 하는 경우 가용성 집합에만 hello 리소스 그룹의 "디스크 관리 되는 사용" 집합과 너무 "Yes" 것을 선택할 수입니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-345">When you set "Use managed disks" too"Yes", only availability sets in hello resource group with "Use managed disks" set too"Yes" would be available for selection.</span></span> <span data-ttu-id="98e85-346">즉, 관리 되는 디스크와 가상 컴퓨터 "디스크 관리를 사용 하 여" 속성이 설정 된 가용성 집합의 일부가 너무 "Yes" 수만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-346">This is because virtual machines with managed disks can only be part of availability sets with "Use managed disks" property set too"Yes".</span></span> <span data-ttu-id="98e85-347">"디스크 관리를 사용 하 여" 속성이 설정 된 장애 조치 시 의도 toouse 관리 되는 디스크에 따라 가용성 집합을 만드는 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-347">Make sure that you create availability sets with "Use managed disks" property set based on your intent toouse managed disks on failover.</span></span> <span data-ttu-id="98e85-348">마찬가지로, 설정 하는 경우 "디스크 관리 되는 사용" 너무 "No", "디스크 관리 되는 사용" 속성이 너무 "아니요"를 설정 하는 hello 리소스 그룹에만 가용성 집합은 선택할 수 있는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-348">Likewise, when you set "Use managed disks" too"No", only availability sets in hello resource group with "Use managed disks" property set too"No" would be available for selection.</span></span> <span data-ttu-id="98e85-349">[Managed Disks와 가용성 집합에 대해 자세히 알아봅니다](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set).</span><span class="sxs-lookup"><span data-stu-id="98e85-349">[Learn more about managed disks and availability sets](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set).</span></span>

  > [!NOTE]
  > <span data-ttu-id="98e85-350">Hello 저장소 계정 복제에 사용 되는 시간에 언제 든 지 저장소 서비스 암호화로 암호화 된, 장애 조치 중에 관리 되는 디스크를 만들 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-350">If hello storage account used for replication was encrypted with Storage Service Encryption at any point in time, creation of managed disks during failover will fail.</span></span> <span data-ttu-id="98e85-351">유지할 수 있습니다 설정 "디스크 관리 되는 사용" 너무 "No" 장애 조치를 다시 시도 또는 hello 가상 컴퓨터에 대 한 보호를 사용 하지 않도록 설정 하 고 저장소 서비스 암호화 시간에서 언제 든 지 사용할 수 없는 tooa 저장소 계정을 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-351">You can either set "Use managed disks" too"No" and retry failover or disable protection for hello virtual machine and protect it tooa storage account which did not have Storage service encryption enabled at any point in time.</span></span>
  > <span data-ttu-id="98e85-352">[저장소 서비스를 암호화 및 Managed Disks에 대해 자세히 알아봅니다](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption).</span><span class="sxs-lookup"><span data-stu-id="98e85-352">[Learn more about Storage service encryption and managed disks](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption).</span></span>


## <a name="test-hello-deployment"></a><span data-ttu-id="98e85-353">Hello 배포 테스트</span><span class="sxs-lookup"><span data-stu-id="98e85-353">Test hello deployment</span></span>

<span data-ttu-id="98e85-354">tootest hello 배포는 단일 가상 컴퓨터 또는 하나 이상의 가상 컴퓨터를 포함 하는 복구 계획에 대 한 테스트 장애 조치를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-354">tootest hello deployment you can run a test failover for a single virtual machine or a recovery plan that contains one or more virtual machines.</span></span>

### <a name="before-you-start"></a><span data-ttu-id="98e85-355">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="98e85-355">Before you start</span></span>

 - <span data-ttu-id="98e85-356">Tooconnect tooAzure Vm을 원하는 경우에 대 한 자세한 내용은 RDP를 사용 하 여 장애 조치 후 [tooconnect 준비](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover)합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-356">If you want tooconnect tooAzure VMs using RDP after failover, learn about [preparing tooconnect](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover).</span></span>
 - <span data-ttu-id="98e85-357">테스트 환경에서 Active Directory 및 DNS toocopy 필요한 toofully 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-357">toofully test you need toocopy of Active Directory and DNS in your test environment.</span></span> <span data-ttu-id="98e85-358">[자세히 알아봅니다](site-recovery-active-directory.md#test-failover-considerations).</span><span class="sxs-lookup"><span data-stu-id="98e85-358">[Learn more](site-recovery-active-directory.md#test-failover-considerations).</span></span>

### <a name="run-a-test-failover"></a><span data-ttu-id="98e85-359">테스트 장애 조치(Failover) 실행</span><span class="sxs-lookup"><span data-stu-id="98e85-359">Run a test failover</span></span>

1. <span data-ttu-id="98e85-360">단일 컴퓨터를 통해 toofail에서 **복제 항목**, hello VM을 클릭 > **+ 테스트 장애 조치** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-360">toofail over a single machine, in **Replicated Items**, click hello VM > **+Test Failover** icon.</span></span>
2. <span data-ttu-id="98e85-361">복구를 통해 toofail 계획 **복구 계획**를 마우스 오른쪽 단추로 클릭 hello 계획 > **테스트 장애 조치**합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-361">toofail over a recovery plan, in **Recovery Plans**, right-click hello plan > **Test Failover**.</span></span> <span data-ttu-id="98e85-362">복구 계획 toocreate [다음이 지침에 따라](site-recovery-create-recovery-plans.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-362">toocreate a recovery plan, [follow these instructions](site-recovery-create-recovery-plans.md).</span></span>
3. <span data-ttu-id="98e85-363">**테스트 장애 조치**선택, 장애 조치 발생 후 hello Azure 네트워크 toowhich Azure Vm 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-363">In **Test Failover**, select hello Azure network toowhich Azure VMs will be connected after failover occurs.</span></span>
4. <span data-ttu-id="98e85-364">클릭 **확인** toobegin hello 장애 조치 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-364">Click **OK** toobegin hello failover.</span></span> <span data-ttu-id="98e85-365">Hello 또는 hello VM tooopen에 해당 속성을 클릭 하 여 진행률을 추적할 수 **테스트 장애 조치** 자격 증명 모음 이름에는 작업 > **작업** > **사이트 복구 작업이**합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-365">You can track progress by clicking on hello VM tooopen its properties, or on hello **Test Failover** job in vault name > **Jobs** > **Site Recovery jobs**.</span></span>
5. <span data-ttu-id="98e85-366">Hello 장애 조치가 끝나면도 있어야 toosee hello 복제본 Azure 컴퓨터 hello Azure 포털에에서 표시 > **가상 컴퓨터**합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-366">After hello failover completes, you should also be able toosee hello replica Azure machine appear in hello Azure portal > **Virtual Machines**.</span></span> <span data-ttu-id="98e85-367">해당 hello VM 실행 되 고 toohello 적절 한 네트워크 연결 된 hello 적절 한 크기 인지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-367">You should make sure that hello VM is hello appropriate size, that it's connected toohello appropriate network, and that it's running.</span></span>
6. <span data-ttu-id="98e85-368">연결에 대 한 장애 조치 후 준비 수 tooconnect toohello Azure VM이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-368">If you prepared for connections after failover, you should be able tooconnect toohello Azure VM.</span></span>
7. <span data-ttu-id="98e85-369">완료 되 면 클릭 **테스트 장애 조치 정리** hello 복구 계획에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-369">Once you're done, click on **Cleanup test failover** on hello recovery plan.</span></span> <span data-ttu-id="98e85-370">**노트** 기록 하 고 테스트 장애 조치 hello와 관련 된 모든 관찰을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-370">In **Notes** record and save any observations associated with hello test failover.</span></span> <span data-ttu-id="98e85-371">테스트 장애 조치 중에 생성 된 hello 가상 컴퓨터를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-371">This will delete hello virtual machines that were created during test failover.</span></span>

<span data-ttu-id="98e85-372">자세한 내용은 hello를 읽을 [테스트 장애 조치 tooAzure](site-recovery-test-failover-to-azure.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="98e85-372">For more details, read hello [Test failover tooAzure](site-recovery-test-failover-to-azure.md) article.</span></span>



## <a name="monitor-hello-deployment"></a><span data-ttu-id="98e85-373">모니터 hello 배포</span><span class="sxs-lookup"><span data-stu-id="98e85-373">Monitor hello deployment</span></span>

<span data-ttu-id="98e85-374">Hello 구성 설정, 상태 및 사이트 복구 배포에 대 한 상태를 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-374">Monitor hello configuration settings, status, and health for your Site Recovery deployment:</span></span>

1. <span data-ttu-id="98e85-375">Hello 자격 증명 모음 이름 tooaccess hello 클릭 **Essentials** 대시보드 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-375">Click on hello vault name tooaccess hello **Essentials** dashboard.</span></span> <span data-ttu-id="98e85-376">이 대시보드에서 Site Recovery 작업, 복제 상태, 복구 계획, 서버 상태 및 이벤트를 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-376">In this dashboard you can track Site Recovery jobs, replication status, recovery plans, server health, and events.</span></span>  

    ![Essentials](./media/site-recovery-hyper-v-site-to-azure/essentials.png)
2. <span data-ttu-id="98e85-378">Hello에 **상태** 타일 hello 지난 24 시간 동안 hello에서 Site Recovery에 의해 발생 한 이벤트 및 문제를 발생 하는 사이트 서버를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-378">In hello **Health** tile you can monitor site servers that are experiencing issue, and hello events raised by Site Recovery in hello last 24 hours.</span></span> <span data-ttu-id="98e85-379">Essentials tooshow hello 타일 및 다른 사이트 복구 및 백업 자격 증명 모음은 hello 상태를 포함 하는 가장 유용한 tooyou 된 레이아웃을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-379">You can customize Essentials tooshow hello tiles and layouts that are most useful tooyou, including hello status of other Site Recovery and Backup vaults.</span></span>
3. <span data-ttu-id="98e85-380">관리 하 고 hello에 대 한 복제를 모니터링할 수 **복제 항목**, **복구 계획**, 및 **사이트 복구 작업이** 타일입니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-380">You can manage and monitor replication in hello **Replicated Items**, **Recovery Plans**, and **Site Recovery Jobs** tiles.</span></span> <span data-ttu-id="98e85-381">**작업** > **Site Recovery 작업**에서 작업을 자세히 살펴볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-381">You can drill into jobs for more details in **Jobs** > **Site Recovery Jobs**.</span></span>

## <a name="command-line-provider-and-agent-installation"></a><span data-ttu-id="98e85-382">명령줄 공급자 및 에이전트 설치</span><span class="sxs-lookup"><span data-stu-id="98e85-382">Command-line Provider and agent installation</span></span>

<span data-ttu-id="98e85-383">hello Azure 사이트 복구 공급자 및 에이전트 설치할 수도 있습니다 hello 다음 명령줄을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-383">hello Azure Site Recovery Provider and agent can also be installed using hello following command line.</span></span> <span data-ttu-id="98e85-384">이 메서드는 Server Core에 대 한 Windows Server 2012 r 2에서 사용 되는 tooinstall hello 공급자 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-384">This method can be used tooinstall hello provider on a Server Core for Windows Server 2012 R2.</span></span>

1. <span data-ttu-id="98e85-385">Hello 공급자 설치 파일과 등록 키 tooa 폴더를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-385">Download hello Provider installation file and registration key tooa folder.</span></span> <span data-ttu-id="98e85-386">예: C:\ASR.</span><span class="sxs-lookup"><span data-stu-id="98e85-386">For example C:\ASR.</span></span>
2. <span data-ttu-id="98e85-387">상승된 된 명령 프롬프트에서 이러한 명령을 tooextract hello 공급자 설치 관리자를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-387">From an elevated command prompt, run these commands tooextract hello Provider installer:</span></span>

            C:\Windows\System32> CD C:\ASR
            C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
3. <span data-ttu-id="98e85-388">이 명령은 tooinstall hello 구성 요소를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-388">Run this command tooinstall hello components:</span></span>

            C:\ASR> setupdr.exe /i
4. <span data-ttu-id="98e85-389">그런 다음 hello 자격 증명 모음에 이러한 명령을 tooregister hello 서버를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-389">Then run these commands tooregister hello server in hello vault:</span></span>

            CD C:\Program Files\Microsoft Azure Site Recovery Provider\
            C:\Program Files\Microsoft Azure Site Recovery Provider\> DRConfigurator.exe /r  /Friendlyname <friendly name of hello server> /Credentials <path of hello credentials file>

<br/>
<span data-ttu-id="98e85-390">여기서,</span><span class="sxs-lookup"><span data-stu-id="98e85-390">Where:</span></span>

* <span data-ttu-id="98e85-391">**/ 자격 증명**:는 hello 등록 키 파일의 위치를 가리키는 hello 위치를 지정 하는 필수 매개 변수</span><span class="sxs-lookup"><span data-stu-id="98e85-391">**/Credentials**: Mandatory parameter that specifies hello location in which hello registration key file is located</span></span>  
* <span data-ttu-id="98e85-392">**/ FriendlyName**: hello Azure Site Recovery 포털에 표시 되는 hello Hyper-v 호스트 서버 hello 이름에 대 한 필수 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-392">**/FriendlyName**: Mandatory parameter for hello name of hello Hyper-V host server that appears in hello Azure Site Recovery portal.</span></span>
* <span data-ttu-id="98e85-393">**/proxyAddress**: hello hello 프록시 서버의 주소를 지정 하는 선택적 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-393">**/proxyAddress**: Optional parameter that specifies hello address of hello proxy server.</span></span>
* <span data-ttu-id="98e85-394">**/proxyport** : hello hello 프록시 서버의 포트를 지정 하는 선택적 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-394">**/proxyport** : Optional parameter that specifies hello port of hello proxy server.</span></span>
* <span data-ttu-id="98e85-395">**/proxyUsername**: (프록시에 인증이 필요) 하는 경우 hello 프록시 사용자 이름을 지정 하는 선택적 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-395">**/proxyUsername**: Optional parameter that specifies hello Proxy user name (if proxy requires authentication).</span></span>
* <span data-ttu-id="98e85-396">**/proxyPassword**:를 지정 하는 선택적 매개 변수 (프록시에 인증이 필요) 하는 경우 프록시 서버 hello에 인증 하기 위해 암호를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-396">**/proxyPassword**: Optional parameter that specifies hello Password for authenticating with hello proxy server (if proxy requires authentication).</span></span>


## <a name="network-bandwidth-considerations"></a><span data-ttu-id="98e85-397">네트워크 대역폭 고려 사항</span><span class="sxs-lookup"><span data-stu-id="98e85-397">Network bandwidth considerations</span></span>
<span data-ttu-id="98e85-398">Hello를 사용할 수 있습니다 [Hyper-v 용량 계획 도구](site-recovery-capacity-planner.md) toocalculate hello 대역폭 (초기 복제와 델타) 복제에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-398">You can use hello [Hyper-V capacity planner tool](site-recovery-capacity-planner.md) toocalculate hello bandwidth you need for replication (initial replication and then delta).</span></span> <span data-ttu-id="98e85-399">toocontrol hello 양 복제용 대역폭 사용의 몇 가지 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-399">toocontrol hello amount of bandwidth use for replication you have a few options:</span></span>

* <span data-ttu-id="98e85-400">**대역폭 제한**: tooAzure를 복제 하는 Hyper-v 트래픽이 특정 Hyper-v 호스트를 통과 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-400">**Throttle bandwidth**: Hyper-V traffic that replicates tooAzure goes through a specific Hyper-V host.</span></span> <span data-ttu-id="98e85-401">Hello 호스트 서버에서 대역폭을 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-401">You can throttle bandwidth on hello host server.</span></span>
* <span data-ttu-id="98e85-402">**대역폭을 조정**: 몇 가지 레지스트리 키를 사용 하 여 복제에 사용 되는 hello 대역폭에 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-402">**Tweak bandwidth**: You can influence hello bandwidth used for replication using a couple of registry keys.</span></span>

### <a name="throttle-bandwidth"></a><span data-ttu-id="98e85-403">대역폭 제한</span><span class="sxs-lookup"><span data-stu-id="98e85-403">Throttle bandwidth</span></span>
1. <span data-ttu-id="98e85-404">Hello Microsoft Azure 백업 MMC 스냅인 hello Hyper-v 호스트 서버에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-404">Open hello Microsoft Azure Backup MMC snap-in on hello Hyper-V host server.</span></span> <span data-ttu-id="98e85-405">기본적으로 Microsoft Azure 백업에 대 한 바로 가기는 C:\Program Files\Microsoft Azure 복구 서비스 Agent\bin\wabadmin 또는 hello 바탕 화면에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-405">By default a shortcut for Microsoft Azure Backup is available on hello desktop or in C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.</span></span>
2. <span data-ttu-id="98e85-406">Hello 스냅인에서 클릭 **속성 변경**합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-406">In hello snap-in click **Change Properties**.</span></span>
3. <span data-ttu-id="98e85-407">Hello에 **제한** 탭 선택 **백업 작업에 대 한 인터넷 대역폭 제한을 사용 하도록 설정**, 작업에 대 한 hello 제한을 설정 하 고 비 작업 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-407">On hello **Throttling** tab select **Enable internet bandwidth usage throttling for backup operations**, and set hello limits for work and non-work hours.</span></span> <span data-ttu-id="98e85-408">유효 범위는 512 Kbps too102 Mbps 초당에서.</span><span class="sxs-lookup"><span data-stu-id="98e85-408">Valid ranges are from 512 Kbps too102 Mbps per second.</span></span>

    ![대역폭 제한](./media/site-recovery-hyper-v-site-to-azure/throttle2.png)

<span data-ttu-id="98e85-410">Hello를 사용할 수도 있습니다 [Set-obmachinesetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet tooset 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-410">You can also use hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet tooset throttling.</span></span> <span data-ttu-id="98e85-411">다음은 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-411">Here's a sample:</span></span>

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

<span data-ttu-id="98e85-412">**Set-OBMachineSetting -NoThrottle** 은 제한이 필요 없다는 뜻입니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-412">**Set-OBMachineSetting -NoThrottle** indicates that no throttling is required.</span></span>

### <a name="influence-network-bandwidth"></a><span data-ttu-id="98e85-413">네트워크 대역폭에 영향</span><span class="sxs-lookup"><span data-stu-id="98e85-413">Influence network bandwidth</span></span>
1. <span data-ttu-id="98e85-414">너무 hello 레지스트리 이동**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-414">In hello registry navigate too**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.</span></span>
   * <span data-ttu-id="98e85-415">복제 디스크에서 tooinfluence hello 대역폭 트래픽을 수정 hello 값 hello **UploadThreadsPerVM**, 하거나 존재 하지 않는 경우 hello 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-415">tooinfluence hello bandwidth traffic on a replicating disk, modify hello value hello **UploadThreadsPerVM**, or create hello key if it doesn't exist.</span></span>
   * <span data-ttu-id="98e85-416">hello 값을 수정 하는 Azure에서 장애 복구 트래픽을 tooinfluence hello 대역폭 **DownloadThreadsPerVM**합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-416">tooinfluence hello bandwidth for failback traffic from Azure, modify hello value **DownloadThreadsPerVM**.</span></span>
2. <span data-ttu-id="98e85-417">hello 기본값은 4입니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-417">hello default value is 4.</span></span> <span data-ttu-id="98e85-418">"Overprovisioned" 네트워크에서 이러한 레지스트리 키 hello 기본값에서 변경 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-418">In an “overprovisioned” network, these registry keys should be changed from hello default values.</span></span> <span data-ttu-id="98e85-419">최대 hello은 32입니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-419">hello maximum is 32.</span></span> <span data-ttu-id="98e85-420">트래픽 toooptimize hello 값을 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-420">Monitor traffic toooptimize hello value.</span></span>

## <a name="next-steps"></a><span data-ttu-id="98e85-421">다음 단계</span><span class="sxs-lookup"><span data-stu-id="98e85-421">Next steps</span></span>

<span data-ttu-id="98e85-422">초기 복제가 완료 되 면 hello 배포를 테스트 한 후에 hello 필요할 때 장애 조치를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-422">After initial replication is complete, and you've tested hello deployment, you can invoke failovers as hello need arises.</span></span> <span data-ttu-id="98e85-423">[자세한 내용은](site-recovery-failover.md) 다양 한 유형의 장애 조치를 수행 하는 방법에 대 한 방법과 toorun 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e85-423">[Learn more](site-recovery-failover.md) about different types of failovers and how toorun them.</span></span>

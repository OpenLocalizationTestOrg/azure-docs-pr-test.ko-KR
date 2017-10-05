---
title: "Azure Site Recovery 및 PowerShell을 사용하여 VMM 클라우드의 Hyper-V 가상 컴퓨터 복제(Resource Manager) | Microsoft Docs"
description: "Azure Site Recovery 및 PowerShell을 사용하여 VMM 클라우드의 Hyper-V 가상 컴퓨터 복제"
services: site-recovery
documentationcenter: 
author: Rajani-Janaki-Ram
manager: rochakm
editor: raynew
ms.assetid: 6ac509ad-5024-43d8-b621-d8fec019b9a9
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: rajanaki
ms.openlocfilehash: 34086044db752f09f1282517b59856091e85c2fc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-to-azure-using-powershell-and-azure-resource-manager"></a><span data-ttu-id="27d78-103">PowerShell 및 Azure Resource Manager를 사용하여 Azure에 VMM 클라우드의 Hyper-V 가상 컴퓨터 복제</span><span class="sxs-lookup"><span data-stu-id="27d78-103">Replicate Hyper-V virtual machines in VMM clouds to Azure using PowerShell and Azure Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="27d78-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="27d78-104">Azure Portal</span></span>](site-recovery-vmm-to-azure.md)
> * [<span data-ttu-id="27d78-105">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="27d78-105">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [<span data-ttu-id="27d78-106">클래식 포털</span><span class="sxs-lookup"><span data-stu-id="27d78-106">Classic Portal</span></span>](site-recovery-vmm-to-azure-classic.md)
> * [<span data-ttu-id="27d78-107">PowerShell - 클래식</span><span class="sxs-lookup"><span data-stu-id="27d78-107">PowerShell - Classic</span></span>](site-recovery-deploy-with-powershell.md)
>
>

## <a name="overview"></a><span data-ttu-id="27d78-108">개요</span><span class="sxs-lookup"><span data-stu-id="27d78-108">Overview</span></span>
<span data-ttu-id="27d78-109">Azure Site Recovery는 여러 배포 시나리오에서 가상 컴퓨터의 복제, 장애 조치(Failover) 및 복구를 오케스트레이션하여 BCDR(비즈니스 연속성 및 재해 복구) 전략에 기여합니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-109">Azure Site Recovery contributes to your business continuity and disaster recovery (BCDR) strategy by orchestrating replication, failover and recovery of virtual machines in a number of deployment scenarios.</span></span> <span data-ttu-id="27d78-110">배포 시나리오의 전체 목록은 [Azure Site Recovery 개요](site-recovery-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="27d78-110">For a full list of deployment scenarios see the [Azure Site Recovery overview](site-recovery-overview.md).</span></span>

<span data-ttu-id="27d78-111">이 문서에서는 System Center VMM 클라우드의 Hyper-V 가상 컴퓨터를 Azure 저장소로 복제하도록 Azure Site Recovery를 설정할 때 수행해야 하는 일반적인 작업을 PowerShell을 사용하여 자동화하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-111">This article shows you how to use PowerShell to automate common tasks you need to perform when you set up Azure Site Recovery to replicate Hyper-V virtual machines in System Center VMM clouds to Azure storage.</span></span>

<span data-ttu-id="27d78-112">이 문서는 시나리오의 필수 조건을 포함하고 있으며, 다음 내용을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-112">The article includes prerequisites for the scenario, and shows you</span></span>

* <span data-ttu-id="27d78-113">복구 서비스 자격 증명 모음을 설정하는 방법</span><span class="sxs-lookup"><span data-stu-id="27d78-113">How to set up a Recovery Services Vault</span></span>
* <span data-ttu-id="27d78-114">원본 VMM 서버에 Azure Site Recovery 공급자 설치</span><span class="sxs-lookup"><span data-stu-id="27d78-114">Install the Azure Site Recovery Provider on the source VMM server</span></span>
* <span data-ttu-id="27d78-115">자격 증명 모음에 서버를 등록하고, Azure 저장소 계정 추가</span><span class="sxs-lookup"><span data-stu-id="27d78-115">Register the server in the vault, add an Azure storage account</span></span>
* <span data-ttu-id="27d78-116">Hyper-V 호스트 서버에 Azure 복구 서비스 에이전트 설치</span><span class="sxs-lookup"><span data-stu-id="27d78-116">Install the Azure Recovery Services agent on Hyper-V host servers</span></span>
* <span data-ttu-id="27d78-117">VMM 클라우드에 대한 보호 설정 구성, 이 구성은 모든 보호되는 가상 컴퓨터에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-117">Configure protection settings for VMM clouds, that will be applied to all protected virtual machines</span></span>
* <span data-ttu-id="27d78-118">이러한 가상 컴퓨터의 보호 활성화</span><span class="sxs-lookup"><span data-stu-id="27d78-118">Enable protection for those virtual machines.</span></span>
* <span data-ttu-id="27d78-119">모든 기능이 예상대로 작동하는지 확인하기 위해 장애 조치(Failover) 테스트</span><span class="sxs-lookup"><span data-stu-id="27d78-119">Test the fail-over to make sure everything's working as expected.</span></span>

<span data-ttu-id="27d78-120">이 시나리오를 설정하는 동안 문제가 발생할 경우 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)에 문의 사항을 게시하세요.</span><span class="sxs-lookup"><span data-stu-id="27d78-120">If you run into problems setting up this scenario, post your questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

> [!NOTE]
> <span data-ttu-id="27d78-121">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../azure-resource-manager/resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-121">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="27d78-122">이 문서에서는 리소스 관리자 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-122">This article covers using the Resource Manager deployment model.</span></span>
>
>

## <a name="before-you-start"></a><span data-ttu-id="27d78-123">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="27d78-123">Before you start</span></span>
<span data-ttu-id="27d78-124">다음 필수 조건이 충족되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-124">Make sure you have these prerequisites in place:</span></span>

### <a name="azure-prerequisites"></a><span data-ttu-id="27d78-125">Azure 필수 조건</span><span class="sxs-lookup"><span data-stu-id="27d78-125">Azure prerequisites</span></span>
* <span data-ttu-id="27d78-126">[Microsoft Azure](https://azure.microsoft.com/) 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-126">You'll need a [Microsoft Azure](https://azure.microsoft.com/) account.</span></span> <span data-ttu-id="27d78-127">계정이 없는 분은 [무료 계정](https://azure.microsoft.com/free)으로 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-127">If you don't have one, start with a [free account](https://azure.microsoft.com/free).</span></span> <span data-ttu-id="27d78-128">[Azure Site 복구 관리자 가격 책정](https://azure.microsoft.com/pricing/details/site-recovery/)에 대해서도 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="27d78-128">In addition, you can read about the [Azure Site Recovery Manager pricing](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
* <span data-ttu-id="27d78-129">CSP 구독 시나리오에 복제하려면 CSP 구독이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-129">You'll need a CSP subscription if you are trying out the replication to a CSP subscription scenario.</span></span> <span data-ttu-id="27d78-130">[CSP 프로그램에 등록하는 방법](https://msdn.microsoft.com/library/partnercenter/mt156995.aspx)에서 CSP 프로그램에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="27d78-130">Learn more about the CSP program in [how to enroll in the CSP program](https://msdn.microsoft.com/library/partnercenter/mt156995.aspx).</span></span>
* <span data-ttu-id="27d78-131">Azure로 복제된 데이터를 저장하려면 Azure v2 저장소(Resource Manager) 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-131">You'll need an Azure v2 storage (Resource Manager) account to store data replicated to Azure.</span></span> <span data-ttu-id="27d78-132">계정의 지역에서 복제 기능을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-132">The account needs geo-replication enabled.</span></span> <span data-ttu-id="27d78-133">계정은 Azure Site Recovery 서비스와 같은 지역에 있어야 하며, 같은 구독 또는 CSP 구독에 연결되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-133">It should be in the same region as the Azure Site Recovery service, and be associated with the same subscription or the CSP subscription.</span></span> <span data-ttu-id="27d78-134">Azure 저장소 설정에 대한 자세한 내용은 [Microsoft Azure 저장소 소개](../storage/common/storage-introduction.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="27d78-134">To learn more about setting up Azure storage, see the [Introduction to Microsoft Azure Storage](../storage/common/storage-introduction.md) for reference.</span></span>
* <span data-ttu-id="27d78-135">보호할 가상 컴퓨터가 [Azure 가상 컴퓨터 필수 조건](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)을 준수하는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-135">You'll need to make sure that virtual machines you want to protect comply with the [Azure virtual machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

> [!NOTE]
> <span data-ttu-id="27d78-136">현재, VM 수준 작업만 Powershell을 통해 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-136">Currently, only VM level operations are possible through Powershell.</span></span> <span data-ttu-id="27d78-137">복구 계획 수준 작업에 대한 지원이 곧 제공될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-137">Support for recovery plan level operations will be made soon.</span></span>  <span data-ttu-id="27d78-138">지금은 '보호되는 VM' 수준에서만 장애 조치(Failover)를 수행할 수 있고 복구 수준에서는 수행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-138">For now, you are limited to performing fail-overs only at a ‘protected VM’ granularity and not at a Recovery Plan level.</span></span>
>
>

### <a name="vmm-prerequisites"></a><span data-ttu-id="27d78-139">VMM 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="27d78-139">VMM prerequisites</span></span>
* <span data-ttu-id="27d78-140">System Center 2012 R2에서 실행되는 VMM 서버가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-140">You'll need VMM server running on System Center 2012 R2.</span></span>
* <span data-ttu-id="27d78-141">보호할 가상 컴퓨터를 포함하는 모든 VMM 서버가 Azure Site Recovery 공급자를 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-141">Any VMM server containing virtual machines you want to protect must be running the Azure Site Recovery Provider.</span></span> <span data-ttu-id="27d78-142">이 공급자는 Azure Site Recovery 배포 중에 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-142">This is installed during the Azure Site Recovery deployment.</span></span>
* <span data-ttu-id="27d78-143">보호할 VMM 서버에 클라우드가 하나 이상 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-143">You'll need at least one cloud on the VMM server you want to protect.</span></span> <span data-ttu-id="27d78-144">클라우드에는 다음이 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-144">The cloud should contain:</span></span>
  * <span data-ttu-id="27d78-145">하나 이상의 VMM 호스트 그룹.</span><span class="sxs-lookup"><span data-stu-id="27d78-145">One or more VMM host groups.</span></span>
  * <span data-ttu-id="27d78-146">각 호스트 그룹에 있는 하나 이상의 Hyper-V 호스트 서버 또는 클러스터</span><span class="sxs-lookup"><span data-stu-id="27d78-146">One or more Hyper-V host servers or clusters in each host group.</span></span>
  * <span data-ttu-id="27d78-147">원본 Hyper-V 서버에 있는 하나 이상의 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="27d78-147">One or more virtual machines on the source Hyper-V server.</span></span>
* <span data-ttu-id="27d78-148">VMM 클라우드 설정에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-148">Learn more about setting up VMM clouds:</span></span>
  * <span data-ttu-id="27d78-149">[System Center 2012 R2 VMM에서 사설 클라우드의 새로운 기능](http://go.microsoft.com/fwlink/?LinkId=324952)과 [VMM 2012 및 클라우드](http://go.microsoft.com/fwlink/?LinkId=324956)에서 사설 VMM 클라우드에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-149">Read more about private VMM clouds in [What’s New in Private Cloud with System Center 2012 R2 VMM](http://go.microsoft.com/fwlink/?LinkId=324952) and in [VMM 2012 and the clouds](http://go.microsoft.com/fwlink/?LinkId=324956).</span></span>
  * <span data-ttu-id="27d78-150">[VMM 클라우드 패브릭 구성](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric)</span><span class="sxs-lookup"><span data-stu-id="27d78-150">Learn about [Configuring the VMM cloud fabric](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric)</span></span>
  * <span data-ttu-id="27d78-151">클라우드 패브릭 요소가 구현되면 [VMM에서 사설 클라우드 만들기](http://go.microsoft.com/fwlink/p/?LinkId=324953) 및 [연습: System Center 2012 SP1 VMM으로 사설 클라우드 만들기](http://go.microsoft.com/fwlink/p/?LinkId=324954)에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="27d78-151">After your cloud fabric elements are in place learn about creating private clouds in [Creating a private cloud in VMM](http://go.microsoft.com/fwlink/p/?LinkId=324953) and in [Walkthrough: Creating private clouds with System Center 2012 SP1 VMM](http://go.microsoft.com/fwlink/p/?LinkId=324954).</span></span>

### <a name="hyper-v-prerequisites"></a><span data-ttu-id="27d78-152">Hyper-V 필수 조건</span><span class="sxs-lookup"><span data-stu-id="27d78-152">Hyper-V prerequisites</span></span>
* <span data-ttu-id="27d78-153">호스트 Hyper-V 서버는 **Windows Server 2012** 이상(Hyper-V 역할 수행) 또는 **Microsoft Hyper-V Server 2012**를 실행하고 최신 업데이트가 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-153">The host Hyper-V servers must be running at least **Windows Server 2012** with Hyper-V role or **Microsoft Hyper-V Server 2012** and have the latest updates installed.</span></span>
* <span data-ttu-id="27d78-154">클러스터에서 Hyper-V를 실행하는 경우 고정 IP 주소 기반 클러스터가 있으면 클러스터 브로커가 자동으로 만들어지지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-154">If you're running Hyper-V in a cluster note that cluster broker isn't created automatically if you have a static IP address-based cluster.</span></span> <span data-ttu-id="27d78-155">클러스터 브로커를 수동으로 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-155">You'll need to configure the cluster broker manually.</span></span> <span data-ttu-id="27d78-156">자세한</span><span class="sxs-lookup"><span data-stu-id="27d78-156">For</span></span>
* <span data-ttu-id="27d78-157">자세한 내용은 [Hyper-V 복제본 Broker 구성 방법](http://blogs.technet.com/b/haroldwong/archive/2013/03/27/server-virtualization-series-hyper-v-replica-broker-explained-part-15-of-20-by-yung-chou.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="27d78-157">For instructions see [How to Configure Hyper-V Replica Broker](http://blogs.technet.com/b/haroldwong/archive/2013/03/27/server-virtualization-series-hyper-v-replica-broker-explained-part-15-of-20-by-yung-chou.aspx).</span></span>
* <span data-ttu-id="27d78-158">보호를 관리할 Hyper-V 호스트 서버 또는 클러스터가 모두 VMM 클라우드에 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-158">Any Hyper-V host server or cluster for which you want to manage protection must be included in a VMM cloud.</span></span>

### <a name="network-mapping-prerequisites"></a><span data-ttu-id="27d78-159">네트워크 매핑 필수 조건</span><span class="sxs-lookup"><span data-stu-id="27d78-159">Network mapping prerequisites</span></span>
<span data-ttu-id="27d78-160">Azure에서 가상 컴퓨터를 보호하는 경우 네트워크 매핑은 원본 VMM 서버의 VM 네트워크와 대상 Azure 네트워크를 매핑하여 다음을 가능하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-160">When you protect virtual machines in Azure, the network mapping  maps the virtual machine networks on the source VMM server and target Azure networks to enable the following:</span></span>

* <span data-ttu-id="27d78-161">속해 있는 복구 계획에 관계없이 동일한 네트워크에서 장애 조치(Failover)되는 모든 컴퓨터가 서로 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-161">All machines which fail over on the same network can connect to each other, irrespective of which recovery plan they are in.</span></span>
* <span data-ttu-id="27d78-162">네트워크 게이트웨이가 대상 Azure 네트워크에서 설정된 경우 가상 컴퓨터가 다른 온-프레미스 가상 컴퓨터에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-162">If a network gateway is setup on the target Azure network, virtual machines can connect to other on-premises virtual machines.</span></span>
* <span data-ttu-id="27d78-163">네트워크 매핑을 구성하지 않으면 동일한 복구 계획에서 장애 조치(Failover)되는 가상 컴퓨터만 Azure로의 장애 조치(Failover) 후에 서로 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-163">If you don’t configure network mapping, only the virtual machines that fail over in the same recovery plan will be able to connect to each other after fail-over to Azure.</span></span>

<span data-ttu-id="27d78-164">네트워크 매핑을 배포하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-164">If you want to deploy network mapping you'll need the following:</span></span>

* <span data-ttu-id="27d78-165">원본 VMM 서버에서 보호할 가상 컴퓨터가 VM 네트워크에 연결되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-165">The virtual machines you want to protect on the source VMM server should be connected to a VM network.</span></span> <span data-ttu-id="27d78-166">해당 네트워크가 클라우드와 연결된 논리 네트워크에 연결되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-166">That network should be linked to a logical network that is associated with the cloud.</span></span>
* <span data-ttu-id="27d78-167">복제된 가상 컴퓨터가 장애 조치(Failover) 후 연결할 수 있는 Azure 네트워크.</span><span class="sxs-lookup"><span data-stu-id="27d78-167">An Azure network to which replicated virtual machines can connect after fail-over.</span></span> <span data-ttu-id="27d78-168">이 네트워크는 장애 조치(Failover) 시 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-168">You'll select this network at the time of fail-over.</span></span> <span data-ttu-id="27d78-169">네트워크는 Azure Site Recovery 구독과 동일한 지역에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-169">The network should be in the same region as your Azure Site Recovery subscription.</span></span>

<span data-ttu-id="27d78-170">네트워크 매핑에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="27d78-170">Learn more about network mapping in</span></span>

* [<span data-ttu-id="27d78-171">VMM에서 논리 네트워크를 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="27d78-171">How to configure logical networks in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386307)
* [<span data-ttu-id="27d78-172">VMM에서 VM 네트워크 및 게이트웨이를 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="27d78-172">How to configure VM networks and gateways in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386308)
* [<span data-ttu-id="27d78-173">Azure에서 가상 네트워크를 구성 및 모니터링하는 방법</span><span class="sxs-lookup"><span data-stu-id="27d78-173">How to configure and monitor virtual networks in Azure</span></span>](https://azure.microsoft.com/documentation/services/virtual-network/)

### <a name="powershell-prerequisites"></a><span data-ttu-id="27d78-174">PowerShell 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="27d78-174">PowerShell prerequisites</span></span>
<span data-ttu-id="27d78-175">Azure PowerShell을 사용할 준비가 되었는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="27d78-175">Make sure you have Azure PowerShell ready to go.</span></span> <span data-ttu-id="27d78-176">이미 PowerShell을 사용하고 있는 경우 버전 0.8.10 이상으로 업그레이드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-176">If you are already using PowerShell, you'll need to upgrade to version 0.8.10 or later.</span></span> <span data-ttu-id="27d78-177">PowerShell 설치에 대한 자세한 내용은 [Azure PowerShell을 설치 및 구성하는 방법](/powershell/azureps-cmdlets-docs)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="27d78-177">For information about setting up PowerShell, see the [Guide to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="27d78-178">PowerShell을 설정 및 구성하면 [여기](/powershell/azure/overview)에서 서비스에 사용 가능한 모든 cmdlet을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-178">Once you have set up and configured PowerShell, you can view all of the available cmdlets for the service [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="27d78-179">Azure PowerShell에서 매개 변수 값, 입력, 출력이 일반적으로 처리되는 방법 등 cmdlet를 사용하는 데 도움이 되는 팁을 보려면 [Azure Cmdlet 시작하기](/powershell/azure/get-started-azureps)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="27d78-179">To learn about tips that can help you use the cmdlets, such as how parameter values, inputs, and outputs are typically handled in Azure PowerShell, see the [Guide to get Started with Azure Cmdlets](/powershell/azure/get-started-azureps).</span></span>

## <a name="step-1-set-the-subscription"></a><span data-ttu-id="27d78-180">1단계: 구독 설정</span><span class="sxs-lookup"><span data-stu-id="27d78-180">Step 1: Set the subscription</span></span>
1. <span data-ttu-id="27d78-181">Azure powershell에서 다음 cmdlet을 사용하여 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-181">From Azure powershell, login to your Azure account: using the following cmdlets</span></span>

        $UserName = "<user@live.com>"
        $Password = "<password>"
        $SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
        $Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $SecurePassword
        Login-AzureRmAccount #-Credential $Cred
2. <span data-ttu-id="27d78-182">구독 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-182">Get a list of your subscriptions.</span></span> <span data-ttu-id="27d78-183">각 구독의 subscriptionID 목록도 함께 표시될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-183">This will also list the subscriptionIDs for each of the subscriptions.</span></span> <span data-ttu-id="27d78-184">복구 서비스 자격 증명 모음을 만들려는 구독의 subscriptionID를 메모합니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-184">Note down the subscriptionID of the subscription in which you wish to create the recovery services vault</span></span>

        Get-AzureRmSubscription
3. <span data-ttu-id="27d78-185">구독 ID를 알려주어 복구 서비스 자격 증명 모음을 만들 구독을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-185">Set the subscription in which the recovery services vault is to be created by mentioning the subscription ID</span></span>

        Set-AzureRmContext –SubscriptionID <subscriptionId>

## <a name="step-2-create-a-recovery-services-vault"></a><span data-ttu-id="27d78-186">2단계: 복구 서비스 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="27d78-186">Step 2: Create a Recovery Services vault</span></span>
1. <span data-ttu-id="27d78-187">또한 Azure Resource Manager에 리소스 그룹이 없는 경우 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-187">Create a resource group  in Azure Resource Manager if you don't have one already</span></span>

        New-AzureRmResourceGroup -Name #ResourceGroupName -Location #location
2. <span data-ttu-id="27d78-188">새 복구 서비스 자격 증명 모음을 만들고, 만든 ASR 자격 증명 모음 개체를 변수에 저장합니다(나중에 사용됨).</span><span class="sxs-lookup"><span data-stu-id="27d78-188">Create a new Recovery Services vault and save the created ASR vault object in a variable (will be used later).</span></span> <span data-ttu-id="27d78-189">Get-AzureRMRecoveryServicesVault cmdlet을 사용하여 ASR 자격 증명 모음 개체 게시 만들기를 검색할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-189">You can also retrieve the ASR vault object post creation using the Get-AzureRMRecoveryServicesVault cmdlet:-</span></span>

        $vault = New-AzureRmRecoveryServicesVault -Name #vaultname -ResouceGroupName #ResourceGroupName -Location #location

## <a name="step-3-set-the-recovery-services-vault-context"></a><span data-ttu-id="27d78-190">3단계: 복구 서비스 자격 증명 모음 설정</span><span class="sxs-lookup"><span data-stu-id="27d78-190">Step 3: Set the Recovery Services Vault context</span></span>

<span data-ttu-id="27d78-191">다음 명령을 실행하여 자격 증명 모음 컨텍스트를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-191">Set the vault context by running the below command.</span></span>

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-install-the-azure-site-recovery-provider"></a><span data-ttu-id="27d78-192">4단계: Azure Site Recovery 공급자 설치</span><span class="sxs-lookup"><span data-stu-id="27d78-192">Step 4: Install the Azure Site Recovery Provider</span></span>
1. <span data-ttu-id="27d78-193">VMM 컴퓨터에서 다음 명령을 실행하여 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-193">On the VMM machine, create a directory by running the following command:</span></span>

       New-Item c:\ASR -type directory
2. <span data-ttu-id="27d78-194">다음 명령을 실행하고 다운로드한 공급자를 사용하여 파일을 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-194">Extract the files using the downloaded provider by running the following command</span></span>

       pushd C:\ASR\
       .\AzureSiteRecoveryProvider.exe /x:. /q
3. <span data-ttu-id="27d78-195">다음 명령을 사용하여 공급자를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-195">Install the provider using the following commands:</span></span>

       .\SetupDr.exe /i
       $installationRegPath = "hklm:\software\Microsoft\Microsoft System Center Virtual Machine Manager Server\DRAdapter"
       do
       {
         $isNotInstalled = $true;
         if(Test-Path $installationRegPath)
         {
           $isNotInstalled = $false;
         }
       }While($isNotInstalled)

   <span data-ttu-id="27d78-196">설치가 완료될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-196">Wait for the installation to finish.</span></span>
4. <span data-ttu-id="27d78-197">다음 명령을 사용하여 자격 증명 모음에 서버를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-197">Register the server in the vault using the following command:</span></span>

       $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
       pushd $BinPath
       $encryptionFilePath = "C:\temp\".\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

## <a name="step-5-create-an-azure-storage-account"></a><span data-ttu-id="27d78-198">5단계: Azure 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="27d78-198">Step 5: Create an Azure storage account</span></span>

<span data-ttu-id="27d78-199">Azure 저장소 계정이 없는 경우 다음 명령을 실행하여 자격 증명 모음과 동일한 지역에 지역에서 복제가 활성화된 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-199">If you don't have an Azure storage account, create a geo-replication enabled account in the same geo as the vault by running the following command:</span></span>

        $StorageAccountName = "teststorageacc1"    #StorageAccountname
        $StorageAccountGeo  = "Southeast Asia"     
        $ResourceGroupName =  “myRG”             #ResourceGroupName
        $RecoveryStorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageAccountName -Type “StandardGRS” -Location $StorageAccountGeo

<span data-ttu-id="27d78-200">저장소 계정은 Azure Site Recovery 서비스와 같은 지역에 있고 같은 구독과 연결되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-200">Note that the storage account must be in the same region as the Azure Site Recovery service, and be associated with the same subscription.</span></span>

## <a name="step-6-install-the-azure-recovery-services-agent"></a><span data-ttu-id="27d78-201">6단계: Azure 복구 서비스 에이전트 설치</span><span class="sxs-lookup"><span data-stu-id="27d78-201">Step 6: Install the Azure Recovery Services Agent</span></span>
1. <span data-ttu-id="27d78-202">[http://aka.ms/latestmarsagent](http://aka.ms/latestmarsagent) 에서 Azure 복구 서비스 에이전트를 다운로드하여 보호할 VMM 클라우드에 있는 각 Hyper-V 호스트 서버에 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-202">Download the Azure Recovery Services agent at [http://aka.ms/latestmarsagent](http://aka.ms/latestmarsagent) and install it on each Hyper-V host server located in the VMM clouds you want to protect.</span></span>
2. <span data-ttu-id="27d78-203">모든 VMM 호스트에 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-203">Run the following command on all VMM hosts:</span></span>

       marsagentinstaller.exe /q /nu

## <a name="step-7-configure-cloud-protection-settings"></a><span data-ttu-id="27d78-204">7단계: 클라우드 보호 설정 구성</span><span class="sxs-lookup"><span data-stu-id="27d78-204">Step 7: Configure cloud protection settings</span></span>
1. <span data-ttu-id="27d78-205">다음 명령을 실행하여 Azure에 대한 복제 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-205">Create a replication policy to Azure by running the following command:</span></span>

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $Recoverypoints = 6                    #specify the number of recovery points

        $policryresult = New-AzureRmSiteRecoveryPolicy -Name $policyname -ReplicationProvider HyperVReplicaAzure -ReplicationFrequencyInSeconds $replicationfrequencyinseconds -RecoveryPoints $recoverypoints -ApplicationConsistentSnapshotFrequencyInHours 1 -RecoveryAzureStorageAccountId "/subscriptions/q1345667/resourceGroups/test/providers/Microsoft.Storage/storageAccounts/teststorageacc1"

1. <span data-ttu-id="27d78-206">다음 명령을 실행하여 보호 컨테이너를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-206">Get a protection container by running the following commands:</span></span>

       $PrimaryCloud = "testcloud"
       $protectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloud;  
2. <span data-ttu-id="27d78-207">생성된 작업을 사용하고 친숙한 정책 이름을 알려주어 변수에 정책 세부 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-207">Get the policy details to a variable using the job that was created and mentioning the friendly policy name:</span></span>

       $policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $policyname
3. <span data-ttu-id="27d78-208">복제 정책을 사용하여 보호 컨테이너 연결을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-208">Start the association of the protection container with the replication policy:</span></span>

       $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy     $Policy -PrimaryProtectionContainer $protectionContainer  
4. <span data-ttu-id="27d78-209">작업이 완료되면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-209">After the job has finished, run the following command:</span></span>

       $job = Get-AzureRmSiteRecoveryJob -Job $associationJob

       if($job -eq $null -or $job.StateDescription -ne "Completed")
       {
         $isJobLeftForProcessing = $true;
       }
5. <span data-ttu-id="27d78-210">작업에서 처리를 완료하면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-210">After the job has finished processing, run the following command:</span></span>

       if($isJobLeftForProcessing)
       {
         Start-Sleep -Seconds 60
       }
       }While($isJobLeftForProcessing)

<span data-ttu-id="27d78-211">작동 완료 여부를 확인하려면 [작업 모니터](#monitor)의 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-211">To check the completion of the operation, follow the steps in [Monitor Activity](#monitor).</span></span>

## <a name="step-8-configure-network-mapping"></a><span data-ttu-id="27d78-212">8단계: 네트워크 매핑 구성</span><span class="sxs-lookup"><span data-stu-id="27d78-212">Step 8: Configure network mapping</span></span>
<span data-ttu-id="27d78-213">네트워크 매핑을 시작하기 전에 원본 VMM 서버의 가상 컴퓨터가 VM 네트워크에 연결되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-213">Before you begin network mapping verify that virtual machines on the source VMM server are connected to a VM network.</span></span> <span data-ttu-id="27d78-214">또한 Azure 가상 네트워크를 하나 이상 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-214">In addition, create one or more Azure virtual networks.</span></span>

<span data-ttu-id="27d78-215">[Azure Resource Manager 및 PowerShell을 사용하여 사이트 간 VPN 연결로 가상 네트워크 만들기](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="27d78-215">Learn more about how to create a virtual network using Azure Resource Manager and PowerShell, in [Create a virtual network with a site-to-site VPN connection using Azure Resource Manager and PowerShell](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)</span></span>

<span data-ttu-id="27d78-216">단일 Azure 네트워크에 여러 가상 컴퓨터 네트워크를 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-216">Note that multiple Virtual Machine networks can be mapped to a single Azure network.</span></span> <span data-ttu-id="27d78-217">대상 네트워크에 여러 서브넷이 있고 이 서브넷 중 하나의 이름이 원본 가상 컴퓨터가 있는 서브넷과 같으면 복제본 가상 컴퓨터가 장애 조치(Failover) 후에 대상 서브넷에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-217">If the target network has multiple subnets and one of those subnets has the same name as subnet on which the source virtual machine is located, then the replica virtual machine will be connected to that target subnet after fail-over.</span></span> <span data-ttu-id="27d78-218">일치하는 이름을 가진 대상 서브넷이 없으면 가상 컴퓨터가 네트워크의 첫 번째 서브넷에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-218">If there is no target subnet with a matching name, the virtual machine will be connected to the first subnet in the network.</span></span>

1. <span data-ttu-id="27d78-219">첫 번째 명령은 현재 Azure Site Recovery 자격 증명 모음의 서버를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-219">The first command gets servers for the current Azure Site Recovery vault.</span></span> <span data-ttu-id="27d78-220">이 명령은 $Servers 어레이 변수에 Microsoft Azure Site Recovery 서버를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-220">The command stores the Microsoft Azure Site Recovery servers in the $Servers array variable.</span></span>

        $Servers = Get-AzureRmSiteRecoveryServer
2. <span data-ttu-id="27d78-221">두 번째 명령은 $Servers 어레이의 첫 번째 서버에 대한 사이트 복구 네트워크를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-221">The second command gets the site recovery network for the first server in the $Servers array.</span></span> <span data-ttu-id="27d78-222">이 명령은 $Networks 변수에 네트워크를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-222">The command stores the networks in the $Networks variable.</span></span>

        $Networks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[0]

1. <span data-ttu-id="27d78-223">세 번째 명령은 Azure 가상 네트워크를 가져온 다음 해당 값을 $AzureVmNetworks 변수에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-223">The third command gets Azure virtual networks, and then that value in the $AzureVmNetworks variable.</span></span>

        $AzureVmNetworks =  Get-AzureRmVirtualNetwork
2. <span data-ttu-id="27d78-224">최종 cmdlet은 기본 네트워크와 Azure 가상 컴퓨터 네트워크 사이에 매핑을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-224">The final cmdlet creates a mapping between the primary network and the Azure virtual machine network.</span></span> <span data-ttu-id="27d78-225">cmdlet은 $Networks의 첫 번째 요소로 기본 네트워크를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-225">The cmdlet specifies the primary network as the first element of $Networks.</span></span> <span data-ttu-id="27d78-226">cmdlet은 $AzureVmNetworks의 첫 번째 요소로 가상 컴퓨터 네트워크를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-226">The cmdlet specifies a virtual machine network as the first element of $AzureVmNetworks.</span></span>

        New-AzureRmSiteRecoveryNetworkMapping -PrimaryNetwork $Networks[0] -AzureVMNetworkId $AzureVmNetworks[0]

## <a name="step-9-enable-protection-for-virtual-machines"></a><span data-ttu-id="27d78-227">9단계: 가상 컴퓨터의 보호 활성화</span><span class="sxs-lookup"><span data-stu-id="27d78-227">Step 9: Enable protection for virtual machines</span></span>
<span data-ttu-id="27d78-228">서버, 클라우드 및 네트워크가 제대로 구성되었으면 클라우드에서 가상 컴퓨터에 대한 보호를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-228">After the servers, clouds and networks are configured correctly, you can enable protection for virtual machines in the cloud.</span></span>

 <span data-ttu-id="27d78-229">다음 사항에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="27d78-229">Note the following:</span></span>

* <span data-ttu-id="27d78-230">가상 컴퓨터는 Azure 요구 사항을 충족해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-230">Virtual machines must meet Azure requirements.</span></span> <span data-ttu-id="27d78-231">계획 가이드의 [필수 조건 및 지원](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) 에서 해당 요구 사항을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="27d78-231">Check these in [Prerequisites and Support](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) in the planning guide.</span></span>
* <span data-ttu-id="27d78-232">보호를 사용하도록 설정하려면 가상 컴퓨터에 대해 운영 체제 및 운영 체제 디스크 속성을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-232">To enable protection, the operating system and operating system disk properties must be set for the virtual machine.</span></span> <span data-ttu-id="27d78-233">VMM에서 가상 컴퓨터 템플릿을 사용하여 가상 컴퓨터를 만들 때 속성을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-233">When you create a virtual machine in VMM using a virtual machine template you can set the property.</span></span> <span data-ttu-id="27d78-234">가상 컴퓨터 속성의 **일반** 및 **하드웨어 구성** 탭에서 기존 가상 컴퓨터에 대해 이러한 속성을 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-234">You can also set these properties for existing virtual machines on the **General** and **Hardware Configuration** tabs of the virtual machine properties.</span></span> <span data-ttu-id="27d78-235">이러한 속성을 VMM에서 설정하지 않는 경우 Azure Site Recovery 포털에서 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-235">If you don't set these properties in VMM you'll be able to configure them in the Azure Site Recovery portal.</span></span>

1. <span data-ttu-id="27d78-236">보호를 활성화하려면 다음 명령을 실행하여 보호 컨테이너를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-236">To enable protection, run the following command to get the protection container:</span></span>

          $ProtectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $CloudName
2. <span data-ttu-id="27d78-237">다음 명령을 실행하여 VM(보호 엔터티)을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-237">Get the protection entity (VM) by running the following command:</span></span>

           $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -friendlyName $VMName -ProtectionContainer $protectionContainer
3. <span data-ttu-id="27d78-238">다음 명령을 실행하여 VM에 DR을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-238">Enable the DR for the VM by running the following command:</span></span>

          $jobResult = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionentity -Protection Enable –Force -Policy $policy -RecoveryAzureStorageAccountId  $storageID "/subscriptions/217653172865hcvkchgvd/resourceGroups/rajanirgps/providers/Microsoft.Storage/storageAccounts/teststorageacc1

## <a name="test-your-deployment"></a><span data-ttu-id="27d78-239">배포 테스트</span><span class="sxs-lookup"><span data-stu-id="27d78-239">Test your deployment</span></span>
<span data-ttu-id="27d78-240">배포를 테스트하려면 단일 가상 컴퓨터에 대한 테스트 장애 조치(Failover)를 실행하거나, 여러 개의 가상 컴퓨터로 구성된 복구 계획을 만들고 이 계획에 대한 테스트 장애 조치(Failover)를 실행하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-240">To test your deployment you can run a test fail-over for a single virtual machine, or create a recovery plan consisting of multiple virtual machines and run a test fail-over for the plan.</span></span> <span data-ttu-id="27d78-241">테스트 장애 조치(Failover)에서는 격리된 네트워크에서 장애 조치(Failover) 및 복구 메커니즘을 시뮬레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-241">Test fail-over simulates your fail-over and recovery mechanism in an isolated network.</span></span> <span data-ttu-id="27d78-242">다음 사항에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="27d78-242">Note that:</span></span>

* <span data-ttu-id="27d78-243">장애 조치(Failover) 후에 원격 데스크탑을 사용하여 Azure의 가상 컴퓨터에 연결하려면 가상 컴퓨터에서 원격 데스크탑 연결을 사용하도록 설정하고 나서 테스트 장애 조치(Failover)를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-243">If you want to connect to the virtual machine in Azure using Remote Desktop after the fail-over, enable Remote Desktop Connection on the virtual machine before you run the test failover.</span></span>
* <span data-ttu-id="27d78-244">장애 조치(Failover) 후에 공개 IP 주소를 사용하여 원격 데스크탑을 통해 Azure의 가상 컴퓨터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-244">After fail-over, you'll use a public IP address to connect to the virtual machine in Azure using Remote Desktop.</span></span> <span data-ttu-id="27d78-245">이 작업을 하려면 공개 주소를 사용하여 가상 컴퓨터에 연결하지 못하도록 차단하는 도메인 정책이 없어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-245">If you want to do this, ensure you don't have any domain policies that prevent you from connecting to a virtual machine using a public address.</span></span>

<span data-ttu-id="27d78-246">작동 완료 여부를 확인하려면 [작업 모니터](#monitor)의 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-246">To check the completion of the operation, follow the steps in [Monitor Activity](#monitor).</span></span>

### <a name="run-a-test-failover"></a><span data-ttu-id="27d78-247">테스트 장애 조치(Failover) 실행</span><span class="sxs-lookup"><span data-stu-id="27d78-247">Run a test failover</span></span>
- <span data-ttu-id="27d78-248">다음 명령을 실행하여 테스트 장애 조치(Failover)를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-248">Start the test failover by running the following command:</span></span>

       $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

### <a name="run-a-planned-failover"></a><span data-ttu-id="27d78-249">계획된 장애 조치(Failover) 실행</span><span class="sxs-lookup"><span data-stu-id="27d78-249">Run a planned failover</span></span>
- <span data-ttu-id="27d78-250">다음 명령을 실행하여 계획된 장애 조치(Failover)를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-250">Start the planned failover by running the following command:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

### <a name="run-an-unplanned-failover"></a><span data-ttu-id="27d78-251">계획되지 않은 장애 조치 실행</span><span class="sxs-lookup"><span data-stu-id="27d78-251">Run an unplanned failover</span></span>
- <span data-ttu-id="27d78-252">다음 명령을 실행하여 계획되지 않은 장애 조치(Failover)를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-252">Start the unplanned failover by running the following command:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

## <span data-ttu-id="27d78-253"><a name=monitor></a> 작업 모니터</span><span class="sxs-lookup"><span data-stu-id="27d78-253"><a name=monitor></a> Monitor Activity</span></span>
<span data-ttu-id="27d78-254">다음 명령을 사용하여 작업을 모니터합니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-254">Use the following commands to monitor the activity.</span></span> <span data-ttu-id="27d78-255">처리가 완료될 때까지 기다린 후 다음 작업을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27d78-255">Note that you have to wait in between jobs for the processing to finish.</span></span>

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



## <a name="next-steps"></a><span data-ttu-id="27d78-256">다음 단계</span><span class="sxs-lookup"><span data-stu-id="27d78-256">Next steps</span></span>
<span data-ttu-id="27d78-257">[자세히 알아보세요](/powershell/module/azurerm.recoveryservices.backup/#recovery) .</span><span class="sxs-lookup"><span data-stu-id="27d78-257">[Read more](/powershell/module/azurerm.recoveryservices.backup/#recovery) about Azure Site Recovery with Azure Resource Manager PowerShell cmdlets.</span></span>

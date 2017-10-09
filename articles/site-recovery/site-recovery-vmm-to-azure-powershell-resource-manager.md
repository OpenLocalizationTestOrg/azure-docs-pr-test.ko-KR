---
title: "Azure Site Recovery 및 PowerShell (리소스 관리자)를 사용 하 여 VMM 클라우드에서 aaaReplicate Hyper-v 가상 컴퓨터 | Microsoft Docs"
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
ms.openlocfilehash: b0f641de4e10a600ead415ceb9bd488fb4d1659d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooazure-using-powershell-and-azure-resource-manager"></a><span data-ttu-id="c9f86-103">PowerShell 및 Azure 리소스 관리자를 사용 하 여 VMM 클라우드에 tooAzure에서 Hyper-v 가상 컴퓨터 복제</span><span class="sxs-lookup"><span data-stu-id="c9f86-103">Replicate Hyper-V virtual machines in VMM clouds tooAzure using PowerShell and Azure Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c9f86-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="c9f86-104">Azure Portal</span></span>](site-recovery-vmm-to-azure.md)
> * [<span data-ttu-id="c9f86-105">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c9f86-105">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [<span data-ttu-id="c9f86-106">클래식 포털</span><span class="sxs-lookup"><span data-stu-id="c9f86-106">Classic Portal</span></span>](site-recovery-vmm-to-azure-classic.md)
> * [<span data-ttu-id="c9f86-107">PowerShell - 클래식</span><span class="sxs-lookup"><span data-stu-id="c9f86-107">PowerShell - Classic</span></span>](site-recovery-deploy-with-powershell.md)
>
>

## <a name="overview"></a><span data-ttu-id="c9f86-108">개요</span><span class="sxs-lookup"><span data-stu-id="c9f86-108">Overview</span></span>
<span data-ttu-id="c9f86-109">Azure Site Recovery는 복제, 장애 조치 및 다양 한 배포 시나리오에서에서 가상 컴퓨터의 복구를 오케스트레이션 하 여 tooyour 비즈니스 연속성 및 재해 복구 (BCDR) 전략을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-109">Azure Site Recovery contributes tooyour business continuity and disaster recovery (BCDR) strategy by orchestrating replication, failover and recovery of virtual machines in a number of deployment scenarios.</span></span> <span data-ttu-id="c9f86-110">배포의 전체 목록은 시나리오 참조 hello [Azure Site Recovery 개요](site-recovery-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-110">For a full list of deployment scenarios see hello [Azure Site Recovery overview](site-recovery-overview.md).</span></span>

<span data-ttu-id="c9f86-111">이 문서에서는 어떻게 toouse PowerShell tooautomate 일반적인 작업 tooperform 때 필요한 System Center VMM 클라우드에 tooAzure 저장소에서 Azure Site Recovery tooreplicate Hyper-v 가상 컴퓨터를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-111">This article shows you how toouse PowerShell tooautomate common tasks you need tooperform when you set up Azure Site Recovery tooreplicate Hyper-V virtual machines in System Center VMM clouds tooAzure storage.</span></span>

<span data-ttu-id="c9f86-112">hello 문서에서는 hello 시나리오에 대 한 필수 구성 요소를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-112">hello article includes prerequisites for hello scenario, and shows you</span></span>

* <span data-ttu-id="c9f86-113">어떻게 tooset 복구 서비스 자격 증명 모음을</span><span class="sxs-lookup"><span data-stu-id="c9f86-113">How tooset up a Recovery Services Vault</span></span>
* <span data-ttu-id="c9f86-114">소스 VMM 서버 hello에 hello Azure Site Recovery Provider 설치</span><span class="sxs-lookup"><span data-stu-id="c9f86-114">Install hello Azure Site Recovery Provider on hello source VMM server</span></span>
* <span data-ttu-id="c9f86-115">Hello 서버 hello 자격 증명 모음에 등록, Azure 저장소 계정 추가</span><span class="sxs-lookup"><span data-stu-id="c9f86-115">Register hello server in hello vault, add an Azure storage account</span></span>
* <span data-ttu-id="c9f86-116">Hyper-v 호스트 서버에 hello Azure 복구 서비스 에이전트 설치</span><span class="sxs-lookup"><span data-stu-id="c9f86-116">Install hello Azure Recovery Services agent on Hyper-V host servers</span></span>
* <span data-ttu-id="c9f86-117">적용 된 tooall 보호 하는 가상 컴퓨터를 VMM 클라우드에 대 한 보호 설정 구성</span><span class="sxs-lookup"><span data-stu-id="c9f86-117">Configure protection settings for VMM clouds, that will be applied tooall protected virtual machines</span></span>
* <span data-ttu-id="c9f86-118">이러한 가상 컴퓨터의 보호 활성화</span><span class="sxs-lookup"><span data-stu-id="c9f86-118">Enable protection for those virtual machines.</span></span>
* <span data-ttu-id="c9f86-119">Hello 장애 조치 toomake 모든 것이 예상 대로 작동 하는지 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-119">Test hello fail-over toomake sure everything's working as expected.</span></span>

<span data-ttu-id="c9f86-120">이 시나리오를 설정 하는 문제를 실행 하는 경우 hello에 질문을 게시할 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-120">If you run into problems setting up this scenario, post your questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

> [!NOTE]
> <span data-ttu-id="c9f86-121">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../azure-resource-manager/resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-121">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="c9f86-122">이 문서에서는 hello 리소스 관리자 배포 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-122">This article covers using hello Resource Manager deployment model.</span></span>
>
>

## <a name="before-you-start"></a><span data-ttu-id="c9f86-123">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="c9f86-123">Before you start</span></span>
<span data-ttu-id="c9f86-124">다음 필수 조건이 충족되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-124">Make sure you have these prerequisites in place:</span></span>

### <a name="azure-prerequisites"></a><span data-ttu-id="c9f86-125">Azure 필수 조건</span><span class="sxs-lookup"><span data-stu-id="c9f86-125">Azure prerequisites</span></span>
* <span data-ttu-id="c9f86-126">[Microsoft Azure](https://azure.microsoft.com/) 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-126">You'll need a [Microsoft Azure](https://azure.microsoft.com/) account.</span></span> <span data-ttu-id="c9f86-127">계정이 없는 분은 [무료 계정](https://azure.microsoft.com/free)으로 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-127">If you don't have one, start with a [free account](https://azure.microsoft.com/free).</span></span> <span data-ttu-id="c9f86-128">Hello에 대 한 읽을 수는 또한 [Azure Site Recovery 관리자 가격](https://azure.microsoft.com/pricing/details/site-recovery/)합니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-128">In addition, you can read about hello [Azure Site Recovery Manager pricing](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
* <span data-ttu-id="c9f86-129">Hello 복제 tooa CSP 구독 시나리오를 시도 하는 경우에 CSP 구독을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-129">You'll need a CSP subscription if you are trying out hello replication tooa CSP subscription scenario.</span></span> <span data-ttu-id="c9f86-130">Hello CSP 프로그램에 대 한 자세한 [어떻게 hello CSP 프로그램에서 tooenroll](https://msdn.microsoft.com/library/partnercenter/mt156995.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-130">Learn more about hello CSP program in [how tooenroll in hello CSP program](https://msdn.microsoft.com/library/partnercenter/mt156995.aspx).</span></span>
* <span data-ttu-id="c9f86-131">Azure v2 저장소 (리소스 관리자) 계정 toostore 복제 된 데이터 tooAzure 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-131">You'll need an Azure v2 storage (Resource Manager) account toostore data replicated tooAzure.</span></span> <span data-ttu-id="c9f86-132">hello 계정에는 지역에서 복제를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-132">hello account needs geo-replication enabled.</span></span> <span data-ttu-id="c9f86-133">Hello Azure Site Recovery 서비스와 동일한 지역 hello와 hello 연관 될 것 같은 구독 또는 hello CSP 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-133">It should be in hello same region as hello Azure Site Recovery service, and be associated with hello same subscription or hello CSP subscription.</span></span> <span data-ttu-id="c9f86-134">Azure 저장소 설정에 대 한 더 toolearn 참조 hello [Azure 저장소 소개 tooMicrosoft](../storage/common/storage-introduction.md) 참조에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-134">toolearn more about setting up Azure storage, see hello [Introduction tooMicrosoft Azure Storage](../storage/common/storage-introduction.md) for reference.</span></span>
* <span data-ttu-id="c9f86-135">가상 컴퓨터 tooprotect 원하는 hello 준수 하는지 toomake 필요 합니다 [Azure 가상 컴퓨터 필수 구성 요소](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)합니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-135">You'll need toomake sure that virtual machines you want tooprotect comply with hello [Azure virtual machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

> [!NOTE]
> <span data-ttu-id="c9f86-136">현재, VM 수준 작업만 Powershell을 통해 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-136">Currently, only VM level operations are possible through Powershell.</span></span> <span data-ttu-id="c9f86-137">복구 계획 수준 작업에 대한 지원이 곧 제공될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-137">Support for recovery plan level operations will be made soon.</span></span>  <span data-ttu-id="c9f86-138">지금은 제한 tooperforming 실패-있음만 단위는 'protected VM' 및 복구 계획 수준에서 되지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-138">For now, you are limited tooperforming fail-overs only at a ‘protected VM’ granularity and not at a Recovery Plan level.</span></span>
>
>

### <a name="vmm-prerequisites"></a><span data-ttu-id="c9f86-139">VMM 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="c9f86-139">VMM prerequisites</span></span>
* <span data-ttu-id="c9f86-140">System Center 2012 R2에서 실행되는 VMM 서버가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-140">You'll need VMM server running on System Center 2012 R2.</span></span>
* <span data-ttu-id="c9f86-141">가상 컴퓨터가 포함 된 모든 VMM 서버 원하는 tooprotect hello Azure Site Recovery Provider를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-141">Any VMM server containing virtual machines you want tooprotect must be running hello Azure Site Recovery Provider.</span></span> <span data-ttu-id="c9f86-142">이 hello Azure 사이트 복구 배포 하는 동안 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-142">This is installed during hello Azure Site Recovery deployment.</span></span>
* <span data-ttu-id="c9f86-143">Hello tooprotect VMM 서버에 클라우드가 하나 이상 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-143">You'll need at least one cloud on hello VMM server you want tooprotect.</span></span> <span data-ttu-id="c9f86-144">hello 클라우드 포함 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-144">hello cloud should contain:</span></span>
  * <span data-ttu-id="c9f86-145">하나 이상의 VMM 호스트 그룹.</span><span class="sxs-lookup"><span data-stu-id="c9f86-145">One or more VMM host groups.</span></span>
  * <span data-ttu-id="c9f86-146">각 호스트 그룹에 있는 하나 이상의 Hyper-V 호스트 서버 또는 클러스터</span><span class="sxs-lookup"><span data-stu-id="c9f86-146">One or more Hyper-V host servers or clusters in each host group.</span></span>
  * <span data-ttu-id="c9f86-147">Hello 원본 Hyper-v 서버에서 하나 이상의 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="c9f86-147">One or more virtual machines on hello source Hyper-V server.</span></span>
* <span data-ttu-id="c9f86-148">VMM 클라우드 설정에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-148">Learn more about setting up VMM clouds:</span></span>
  * <span data-ttu-id="c9f86-149">사설 클라우드를 VMM에 대해 자세히 읽어보세요 [What's New in System Center 2012 R2 VMM 사설 클라우드의](http://go.microsoft.com/fwlink/?LinkId=324952) 및 [VMM 2012 및 hello 클라우드](http://go.microsoft.com/fwlink/?LinkId=324956)합니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-149">Read more about private VMM clouds in [What’s New in Private Cloud with System Center 2012 R2 VMM](http://go.microsoft.com/fwlink/?LinkId=324952) and in [VMM 2012 and hello clouds](http://go.microsoft.com/fwlink/?LinkId=324956).</span></span>
  * <span data-ttu-id="c9f86-150">에 대 한 자세한 내용은 [구성 hello VMM 클라우드 패브릭](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric)</span><span class="sxs-lookup"><span data-stu-id="c9f86-150">Learn about [Configuring hello VMM cloud fabric](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric)</span></span>
  * <span data-ttu-id="c9f86-151">클라우드 패브릭 요소가 구현되면 [VMM에서 사설 클라우드 만들기](http://go.microsoft.com/fwlink/p/?LinkId=324953) 및 [연습: System Center 2012 SP1 VMM으로 사설 클라우드 만들기](http://go.microsoft.com/fwlink/p/?LinkId=324954)에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="c9f86-151">After your cloud fabric elements are in place learn about creating private clouds in [Creating a private cloud in VMM](http://go.microsoft.com/fwlink/p/?LinkId=324953) and in [Walkthrough: Creating private clouds with System Center 2012 SP1 VMM](http://go.microsoft.com/fwlink/p/?LinkId=324954).</span></span>

### <a name="hyper-v-prerequisites"></a><span data-ttu-id="c9f86-152">Hyper-V 필수 조건</span><span class="sxs-lookup"><span data-stu-id="c9f86-152">Hyper-V prerequisites</span></span>
* <span data-ttu-id="c9f86-153">hello Hyper-v 호스트 서버 해야 이상을 실행 하 고 **Windows Server 2012** Hyper-v 역할과 또는 **Microsoft Hyper-v Server 2012** 최신 업데이트가 설치 되어 hello 있어야 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-153">hello host Hyper-V servers must be running at least **Windows Server 2012** with Hyper-V role or **Microsoft Hyper-V Server 2012** and have hello latest updates installed.</span></span>
* <span data-ttu-id="c9f86-154">클러스터에서 Hyper-V를 실행하는 경우 고정 IP 주소 기반 클러스터가 있으면 클러스터 브로커가 자동으로 만들어지지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-154">If you're running Hyper-V in a cluster note that cluster broker isn't created automatically if you have a static IP address-based cluster.</span></span> <span data-ttu-id="c9f86-155">Tooconfigure hello 클러스터 브로커를 수동으로 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-155">You'll need tooconfigure hello cluster broker manually.</span></span> <span data-ttu-id="c9f86-156">자세한</span><span class="sxs-lookup"><span data-stu-id="c9f86-156">For</span></span>
* <span data-ttu-id="c9f86-157">에 대 한 참조 [어떻게 tooConfigure Hyper-v 복제본 브로커](http://blogs.technet.com/b/haroldwong/archive/2013/03/27/server-virtualization-series-hyper-v-replica-broker-explained-part-15-of-20-by-yung-chou.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-157">For instructions see [How tooConfigure Hyper-V Replica Broker](http://blogs.technet.com/b/haroldwong/archive/2013/03/27/server-virtualization-series-hyper-v-replica-broker-explained-part-15-of-20-by-yung-chou.aspx).</span></span>
* <span data-ttu-id="c9f86-158">모든 Hyper-v 호스트 서버 또는 클러스터 toomanage 보호 하려는 VMM 클라우드에 포함 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-158">Any Hyper-V host server or cluster for which you want toomanage protection must be included in a VMM cloud.</span></span>

### <a name="network-mapping-prerequisites"></a><span data-ttu-id="c9f86-159">네트워크 매핑 필수 조건</span><span class="sxs-lookup"><span data-stu-id="c9f86-159">Network mapping prerequisites</span></span>
<span data-ttu-id="c9f86-160">Azure의 가상 컴퓨터를 보호 하는 경우 네트워크 매핑 hello hello hello 원본 VMM 서버와 대상 Azure 네트워크 tooenable hello 다음 가상 컴퓨터 네트워크를 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-160">When you protect virtual machines in Azure, hello network mapping  maps hello virtual machine networks on hello source VMM server and target Azure networks tooenable hello following:</span></span>

* <span data-ttu-id="c9f86-161">모든 컴퓨터를 장애 조치 hello에 동일한 네트워크 tooeach 기타에 복구 계획과 관계 없이 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-161">All machines which fail over on hello same network can connect tooeach other, irrespective of which recovery plan they are in.</span></span>
* <span data-ttu-id="c9f86-162">설치 프로그램 hello 대상 Azure 네트워크에 네트워크 게이트웨이가 사용 하는 경우 가상 컴퓨터 tooother 온-프레미스 가상 컴퓨터를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-162">If a network gateway is setup on hello target Azure network, virtual machines can connect tooother on-premises virtual machines.</span></span>
* <span data-ttu-id="c9f86-163">Hello에 장애 조치 hello 동일한 가상 컴퓨터만 네트워크 매핑을 구성 하지 않으면, 복구 계획 장애 조치 tooAzure 후에 다른 수 tooconnect tooeach 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-163">If you don’t configure network mapping, only hello virtual machines that fail over in hello same recovery plan will be able tooconnect tooeach other after fail-over tooAzure.</span></span>

<span data-ttu-id="c9f86-164">네트워크 매핑을 toodeploy 하려는 경우에 hello 다음이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-164">If you want toodeploy network mapping you'll need hello following:</span></span>

* <span data-ttu-id="c9f86-165">hello 원본 VMM 서버의 tooprotect 원하는 hello 가상 컴퓨터에 연결 된 tooa VM 네트워크 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-165">hello virtual machines you want tooprotect on hello source VMM server should be connected tooa VM network.</span></span> <span data-ttu-id="c9f86-166">해당 네트워크 hello는 클라우드와 연결 된 논리 네트워크를 연결 된 tooa 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-166">That network should be linked tooa logical network that is associated with hello cloud.</span></span>
* <span data-ttu-id="c9f86-167">Azure 네트워크 toowhich 복제 가상 컴퓨터 장애 조치 후 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-167">An Azure network toowhich replicated virtual machines can connect after fail-over.</span></span> <span data-ttu-id="c9f86-168">장애 조치 hello 시간에이 네트워크를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-168">You'll select this network at hello time of fail-over.</span></span> <span data-ttu-id="c9f86-169">hello 네트워크 hello에 있어야 합니다. Azure Site Recovery 구독와 동일한 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-169">hello network should be in hello same region as your Azure Site Recovery subscription.</span></span>

<span data-ttu-id="c9f86-170">네트워크 매핑에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="c9f86-170">Learn more about network mapping in</span></span>

* [<span data-ttu-id="c9f86-171">어떻게 tooconfigure VMM에서에서 논리 네트워크</span><span class="sxs-lookup"><span data-stu-id="c9f86-171">How tooconfigure logical networks in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386307)
* [<span data-ttu-id="c9f86-172">어떻게 tooconfigure VM 네트워크 및 VMM에서 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="c9f86-172">How tooconfigure VM networks and gateways in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386308)
* [<span data-ttu-id="c9f86-173">어떻게 Azure에서 가상 네트워크 tooconfigure 및 모니터링</span><span class="sxs-lookup"><span data-stu-id="c9f86-173">How tooconfigure and monitor virtual networks in Azure</span></span>](https://azure.microsoft.com/documentation/services/virtual-network/)

### <a name="powershell-prerequisites"></a><span data-ttu-id="c9f86-174">PowerShell 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="c9f86-174">PowerShell prerequisites</span></span>
<span data-ttu-id="c9f86-175">Azure PowerShell 준비 toogo 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-175">Make sure you have Azure PowerShell ready toogo.</span></span> <span data-ttu-id="c9f86-176">PowerShell을 이미 사용 중인 tooupgrade tooversion 0.8.10 맞춰야 이상.</span><span class="sxs-lookup"><span data-stu-id="c9f86-176">If you are already using PowerShell, you'll need tooupgrade tooversion 0.8.10 or later.</span></span> <span data-ttu-id="c9f86-177">PowerShell 설정에 대 한 정보를 참조 hello [tooinstall 안내 하 고 Azure powershell](/powershell/azureps-cmdlets-docs)합니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-177">For information about setting up PowerShell, see hello [Guide tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="c9f86-178">Hello hello 서비스에 대 한 사용 가능한 cmdlet의 모든 볼 수를 설정 하 고 PowerShell을 구성한 후 [여기](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-178">Once you have set up and configured PowerShell, you can view all of hello available cmdlets for hello service [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="c9f86-179">매개 변수 값, 입력 및 출력이 처리 되는 방법과 일반적으로 Azure PowerShell 같은 hello cmdlet을 사용 하는 데 도움이 되는 팁에 대 한 toolearn 참조 hello [tooget Azure cmdlet 시작 안내](/powershell/azure/get-started-azureps)합니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-179">toolearn about tips that can help you use hello cmdlets, such as how parameter values, inputs, and outputs are typically handled in Azure PowerShell, see hello [Guide tooget Started with Azure Cmdlets](/powershell/azure/get-started-azureps).</span></span>

## <a name="step-1-set-hello-subscription"></a><span data-ttu-id="c9f86-180">1 단계: hello 구독 설정</span><span class="sxs-lookup"><span data-stu-id="c9f86-180">Step 1: Set hello subscription</span></span>
1. <span data-ttu-id="c9f86-181">Azure powershell, 로그인 tooyour Azure 계정에서에서: hello 다음 cmdlet을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="c9f86-181">From Azure powershell, login tooyour Azure account: using hello following cmdlets</span></span>

        $UserName = "<user@live.com>"
        $Password = "<password>"
        $SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
        $Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $SecurePassword
        Login-AzureRmAccount #-Credential $Cred
2. <span data-ttu-id="c9f86-182">구독 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-182">Get a list of your subscriptions.</span></span> <span data-ttu-id="c9f86-183">이 또한은 나열 hello subscriptionIDs 각 hello 구독에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-183">This will also list hello subscriptionIDs for each of hello subscriptions.</span></span> <span data-ttu-id="c9f86-184">Hello 구독의 toocreate hello 복구 서비스 자격 증명 모음 원하는 hello subscriptionID 다운 note</span><span class="sxs-lookup"><span data-stu-id="c9f86-184">Note down hello subscriptionID of hello subscription in which you wish toocreate hello recovery services vault</span></span>

        Get-AzureRmSubscription
3. <span data-ttu-id="c9f86-185">hello에 복구 서비스 자격 증명 모음이 toobe hello 구독 ID를 언급 하 여 만든 hello 구독 설정</span><span class="sxs-lookup"><span data-stu-id="c9f86-185">Set hello subscription in which hello recovery services vault is toobe created by mentioning hello subscription ID</span></span>

        Set-AzureRmContext –SubscriptionID <subscriptionId>

## <a name="step-2-create-a-recovery-services-vault"></a><span data-ttu-id="c9f86-186">2단계: 복구 서비스 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="c9f86-186">Step 2: Create a Recovery Services vault</span></span>
1. <span data-ttu-id="c9f86-187">또한 Azure Resource Manager에 리소스 그룹이 없는 경우 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-187">Create a resource group  in Azure Resource Manager if you don't have one already</span></span>

        New-AzureRmResourceGroup -Name #ResourceGroupName -Location #location
2. <span data-ttu-id="c9f86-188">새 복구 서비스 자격 증명 모음을 만들고 (됩니다 나중에 사용) 변수에 ASR 자격 증명 모음 개체를 만든 hello를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-188">Create a new Recovery Services vault and save hello created ASR vault object in a variable (will be used later).</span></span> <span data-ttu-id="c9f86-189">Hello AzureRMRecoveryServicesVault Get cmdlet을 사용 하 여 hello ASR 자격 증명 모음 개체 post 만들기를 검색할 수도 있습니다.-</span><span class="sxs-lookup"><span data-stu-id="c9f86-189">You can also retrieve hello ASR vault object post creation using hello Get-AzureRMRecoveryServicesVault cmdlet:-</span></span>

        $vault = New-AzureRmRecoveryServicesVault -Name #vaultname -ResouceGroupName #ResourceGroupName -Location #location

## <a name="step-3-set-hello-recovery-services-vault-context"></a><span data-ttu-id="c9f86-190">3 단계: hello 복구 서비스 자격 증명 모음 컨텍스트를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-190">Step 3: Set hello Recovery Services Vault context</span></span>

<span data-ttu-id="c9f86-191">아래의 명령 hello를 실행 하 여 hello 자격 증명 모음 컨텍스트를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-191">Set hello vault context by running hello below command.</span></span>

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-install-hello-azure-site-recovery-provider"></a><span data-ttu-id="c9f86-192">4 단계: hello Azure Site Recovery Provider 설치</span><span class="sxs-lookup"><span data-stu-id="c9f86-192">Step 4: Install hello Azure Site Recovery Provider</span></span>
1. <span data-ttu-id="c9f86-193">Hello VMM 컴퓨터에서 hello 다음 명령을 실행 하 여 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-193">On hello VMM machine, create a directory by running hello following command:</span></span>

       New-Item c:\ASR -type directory
2. <span data-ttu-id="c9f86-194">다운로드 한 hello 공급자를 사용 하 여 hello 다음 명령을 실행 하 여 hello 파일 추출</span><span class="sxs-lookup"><span data-stu-id="c9f86-194">Extract hello files using hello downloaded provider by running hello following command</span></span>

       pushd C:\ASR\
       .\AzureSiteRecoveryProvider.exe /x:. /q
3. <span data-ttu-id="c9f86-195">다음 명령을 hello를 사용 하 여 hello 공급자를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-195">Install hello provider using hello following commands:</span></span>

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

   <span data-ttu-id="c9f86-196">Hello 설치 toofinish 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-196">Wait for hello installation toofinish.</span></span>
4. <span data-ttu-id="c9f86-197">Hello 서버 hello 다음 명령을 사용 하 여 hello 자격 증명 모음에 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-197">Register hello server in hello vault using hello following command:</span></span>

       $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
       pushd $BinPath
       $encryptionFilePath = "C:\temp\".\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

## <a name="step-5-create-an-azure-storage-account"></a><span data-ttu-id="c9f86-198">5단계: Azure 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="c9f86-198">Step 5: Create an Azure storage account</span></span>

<span data-ttu-id="c9f86-199">Azure 저장소 계정이 없는 경우 지역에서 복제를 사용 계정을 만들 hello에 hello 지역 자격 증명 모음에 hello 다음 명령을 실행 하 여:</span><span class="sxs-lookup"><span data-stu-id="c9f86-199">If you don't have an Azure storage account, create a geo-replication enabled account in hello same geo as hello vault by running hello following command:</span></span>

        $StorageAccountName = "teststorageacc1"    #StorageAccountname
        $StorageAccountGeo  = "Southeast Asia"     
        $ResourceGroupName =  “myRG”             #ResourceGroupName
        $RecoveryStorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageAccountName -Type “StandardGRS” -Location $StorageAccountGeo

<span data-ttu-id="c9f86-200">Hello 저장소 계정이 있어야 hello Azure Site Recovery 서비스와 동일한 지역 hello와 연결 된 동일한 구독 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-200">Note that hello storage account must be in hello same region as hello Azure Site Recovery service, and be associated with hello same subscription.</span></span>

## <a name="step-6-install-hello-azure-recovery-services-agent"></a><span data-ttu-id="c9f86-201">6 단계: hello Azure 복구 서비스 에이전트 설치</span><span class="sxs-lookup"><span data-stu-id="c9f86-201">Step 6: Install hello Azure Recovery Services Agent</span></span>
1. <span data-ttu-id="c9f86-202">hello Azure 복구 서비스 에이전트 다운로드 [http://aka.ms/latestmarsagent](http://aka.ms/latestmarsagent) tooprotect 있습니다 클라우드 hello VMM에에서 있는 각 Hyper-v 호스트 서버에 설치 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-202">Download hello Azure Recovery Services agent at [http://aka.ms/latestmarsagent](http://aka.ms/latestmarsagent) and install it on each Hyper-V host server located in hello VMM clouds you want tooprotect.</span></span>
2. <span data-ttu-id="c9f86-203">Hello 모든 VMM 호스트에서 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-203">Run hello following command on all VMM hosts:</span></span>

       marsagentinstaller.exe /q /nu

## <a name="step-7-configure-cloud-protection-settings"></a><span data-ttu-id="c9f86-204">7단계: 클라우드 보호 설정 구성</span><span class="sxs-lookup"><span data-stu-id="c9f86-204">Step 7: Configure cloud protection settings</span></span>
1. <span data-ttu-id="c9f86-205">복제 정책 tooAzure hello 다음 명령을 실행 하 여 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-205">Create a replication policy tooAzure by running hello following command:</span></span>

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $Recoverypoints = 6                    #specify hello number of recovery points

        $policryresult = New-AzureRmSiteRecoveryPolicy -Name $policyname -ReplicationProvider HyperVReplicaAzure -ReplicationFrequencyInSeconds $replicationfrequencyinseconds -RecoveryPoints $recoverypoints -ApplicationConsistentSnapshotFrequencyInHours 1 -RecoveryAzureStorageAccountId "/subscriptions/q1345667/resourceGroups/test/providers/Microsoft.Storage/storageAccounts/teststorageacc1"

1. <span data-ttu-id="c9f86-206">Hello 다음 명령을 실행 하 여 보호 컨테이너를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-206">Get a protection container by running hello following commands:</span></span>

       $PrimaryCloud = "testcloud"
       $protectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloud;  
2. <span data-ttu-id="c9f86-207">생성 된 hello 작업을 사용 하 고 hello 친숙 한 정책 이름에 언급 hello 정책 세부 정보 tooa 변수 가져오기:</span><span class="sxs-lookup"><span data-stu-id="c9f86-207">Get hello policy details tooa variable using hello job that was created and mentioning hello friendly policy name:</span></span>

       $policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $policyname
3. <span data-ttu-id="c9f86-208">Hello 복제 정책을 사용 하 여 hello 보호 컨테이너의 hello 연결을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-208">Start hello association of hello protection container with hello replication policy:</span></span>

       $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy     $Policy -PrimaryProtectionContainer $protectionContainer  
4. <span data-ttu-id="c9f86-209">Hello 작업이 완료 되 면 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-209">After hello job has finished, run hello following command:</span></span>

       $job = Get-AzureRmSiteRecoveryJob -Job $associationJob

       if($job -eq $null -or $job.StateDescription -ne "Completed")
       {
         $isJobLeftForProcessing = $true;
       }
5. <span data-ttu-id="c9f86-210">Hello 작업 처리를 완료 한 후에 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-210">After hello job has finished processing, run hello following command:</span></span>

       if($isJobLeftForProcessing)
       {
         Start-Sleep -Seconds 60
       }
       }While($isJobLeftForProcessing)

<span data-ttu-id="c9f86-211">hello 작업의 toocheck hello 완료 hello 단계에 따라 [모니터 활동](#monitor)합니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-211">toocheck hello completion of hello operation, follow hello steps in [Monitor Activity](#monitor).</span></span>

## <a name="step-8-configure-network-mapping"></a><span data-ttu-id="c9f86-212">8단계: 네트워크 매핑 구성</span><span class="sxs-lookup"><span data-stu-id="c9f86-212">Step 8: Configure network mapping</span></span>
<span data-ttu-id="c9f86-213">시작 하기 전에 네트워크 매핑을 hello 원본 VMM 서버의 가상 컴퓨터가 연결 된 tooa VM 네트워크에 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-213">Before you begin network mapping verify that virtual machines on hello source VMM server are connected tooa VM network.</span></span> <span data-ttu-id="c9f86-214">또한 Azure 가상 네트워크를 하나 이상 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-214">In addition, create one or more Azure virtual networks.</span></span>

<span data-ttu-id="c9f86-215">Toocreate a 가상 네트워크에서 Azure 리소스 관리자 및 PowerShell을 사용 하는 방법에 대 한 자세한 [Azure 리소스 관리자 및 PowerShell을 사용 하는 사이트 간 VPN 연결으로 가상 네트워크 만들기](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="c9f86-215">Learn more about how toocreate a virtual network using Azure Resource Manager and PowerShell, in [Create a virtual network with a site-to-site VPN connection using Azure Resource Manager and PowerShell](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)</span></span>

<span data-ttu-id="c9f86-216">Note 여러 가상 컴퓨터 네트워크는 매핑된 tooa 단일 Azure 네트워크 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-216">Note that multiple Virtual Machine networks can be mapped tooa single Azure network.</span></span> <span data-ttu-id="c9f86-217">Hello 대상 네트워크에 서브넷이 여러 hello에 이러한 서브넷 중 하나는 hello 원본 가상 컴퓨터는 서브넷 이름이 같은 있는 경우 hello 복제 가상 컴퓨터 장애 조치 후에 대상 서브넷 연결된 toothat 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-217">If hello target network has multiple subnets and one of those subnets has hello same name as subnet on which hello source virtual machine is located, then hello replica virtual machine will be connected toothat target subnet after fail-over.</span></span> <span data-ttu-id="c9f86-218">이름이 일치 하는 대상 서브넷 이면 hello 가상 컴퓨터 연결된 toohello hello 네트워크의 첫 번째 서브넷 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-218">If there is no target subnet with a matching name, hello virtual machine will be connected toohello first subnet in hello network.</span></span>

1. <span data-ttu-id="c9f86-219">첫 번째 명령은 hello hello 현재 Azure Site Recovery 자격 증명 모음에 대 한 서버를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-219">hello first command gets servers for hello current Azure Site Recovery vault.</span></span> <span data-ttu-id="c9f86-220">hello 명령은 hello Microsoft Azure Site Recovery 서버 hello $Servers 배열 변수에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-220">hello command stores hello Microsoft Azure Site Recovery servers in hello $Servers array variable.</span></span>

        $Servers = Get-AzureRmSiteRecoveryServer
2. <span data-ttu-id="c9f86-221">hello 두 번째 명령은 hello $Servers 배열의 첫 번째 서버 hello에 대 한 hello 사이트 복구 네트워크를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-221">hello second command gets hello site recovery network for hello first server in hello $Servers array.</span></span> <span data-ttu-id="c9f86-222">hello 명령 hello $Networks 변수에 hello 네트워크를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-222">hello command stores hello networks in hello $Networks variable.</span></span>

        $Networks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[0]

1. <span data-ttu-id="c9f86-223">세 번째 명령은 hello hello $AzureVmNetworks 변수에 Azure 가상 네트워크 및 해당 값을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-223">hello third command gets Azure virtual networks, and then that value in hello $AzureVmNetworks variable.</span></span>

        $AzureVmNetworks =  Get-AzureRmVirtualNetwork
2. <span data-ttu-id="c9f86-224">hello 최종 cmdlet은 기본 네트워크 hello 및 hello Azure 가상 컴퓨터 네트워크 간의 매핑을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-224">hello final cmdlet creates a mapping between hello primary network and hello Azure virtual machine network.</span></span> <span data-ttu-id="c9f86-225">hello cmdlet $Networks의 hello 첫 번째 요소로 hello 주 네트워크를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-225">hello cmdlet specifies hello primary network as hello first element of $Networks.</span></span> <span data-ttu-id="c9f86-226">hello cmdlet hello $AzureVmNetworks의 첫 번째 요소와 가상 컴퓨터 네트워크를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-226">hello cmdlet specifies a virtual machine network as hello first element of $AzureVmNetworks.</span></span>

        New-AzureRmSiteRecoveryNetworkMapping -PrimaryNetwork $Networks[0] -AzureVMNetworkId $AzureVmNetworks[0]

## <a name="step-9-enable-protection-for-virtual-machines"></a><span data-ttu-id="c9f86-227">9단계: 가상 컴퓨터의 보호 활성화</span><span class="sxs-lookup"><span data-stu-id="c9f86-227">Step 9: Enable protection for virtual machines</span></span>
<span data-ttu-id="c9f86-228">Hello 서버, 클라우드 및 네트워크가 올바르게 구성 된 hello 클라우드의 가상 컴퓨터에 대 한 보호를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-228">After hello servers, clouds and networks are configured correctly, you can enable protection for virtual machines in hello cloud.</span></span>

 <span data-ttu-id="c9f86-229">참고 hello 다음.</span><span class="sxs-lookup"><span data-stu-id="c9f86-229">Note hello following:</span></span>

* <span data-ttu-id="c9f86-230">가상 컴퓨터는 Azure 요구 사항을 충족해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-230">Virtual machines must meet Azure requirements.</span></span> <span data-ttu-id="c9f86-231">이러한 체크 인 [필수 구성 요소 및 지원](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) hello 계획 가이드에서입니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-231">Check these in [Prerequisites and Support](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) in hello planning guide.</span></span>
* <span data-ttu-id="c9f86-232">tooenable 보호, hello 운영 체제 및 운영 체제 디스크 속성 hello 가상 컴퓨터에 대해 설정 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-232">tooenable protection, hello operating system and operating system disk properties must be set for hello virtual machine.</span></span> <span data-ttu-id="c9f86-233">가상 컴퓨터 템플릿을 사용 하 여 VMM에서 가상 컴퓨터를 만들 때 hello 속성을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-233">When you create a virtual machine in VMM using a virtual machine template you can set hello property.</span></span> <span data-ttu-id="c9f86-234">Hello에 기존 가상 컴퓨터에 대 한 이러한 속성을 설정할 수도 있습니다 **일반** 및 **하드웨어 구성** hello 가상 컴퓨터 속성의 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-234">You can also set these properties for existing virtual machines on hello **General** and **Hardware Configuration** tabs of hello virtual machine properties.</span></span> <span data-ttu-id="c9f86-235">VMM에서 이러한 속성을 설정 하지 않으면 수 수 tooconfigure hello Azure Site Recovery 포털에서 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-235">If you don't set these properties in VMM you'll be able tooconfigure them in hello Azure Site Recovery portal.</span></span>

1. <span data-ttu-id="c9f86-236">hello 명령 tooget hello 보호 컨테이너를 다음 실행 tooenable 보호:</span><span class="sxs-lookup"><span data-stu-id="c9f86-236">tooenable protection, run hello following command tooget hello protection container:</span></span>

          $ProtectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $CloudName
2. <span data-ttu-id="c9f86-237">Hello 다음 명령을 실행 하 여 hello 보호 엔터티를 (VM)를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-237">Get hello protection entity (VM) by running hello following command:</span></span>

           $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -friendlyName $VMName -ProtectionContainer $protectionContainer
3. <span data-ttu-id="c9f86-238">Hello 다음 명령을 실행 하 여 hello VM에 대 한 DR hello 사용:</span><span class="sxs-lookup"><span data-stu-id="c9f86-238">Enable hello DR for hello VM by running hello following command:</span></span>

          $jobResult = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionentity -Protection Enable –Force -Policy $policy -RecoveryAzureStorageAccountId  $storageID "/subscriptions/217653172865hcvkchgvd/resourceGroups/rajanirgps/providers/Microsoft.Storage/storageAccounts/teststorageacc1

## <a name="test-your-deployment"></a><span data-ttu-id="c9f86-239">배포 테스트</span><span class="sxs-lookup"><span data-stu-id="c9f86-239">Test your deployment</span></span>
<span data-ttu-id="c9f86-240">tootest 배포 테스트를 실행할 수는 단일 가상 컴퓨터에 대 한 장애 조치 또는 여러 가상 컴퓨터의 구성 된 복구 계획을 만들고 실행 hello 계획에 대 한 테스트 장애 조치 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-240">tootest your deployment you can run a test fail-over for a single virtual machine, or create a recovery plan consisting of multiple virtual machines and run a test fail-over for hello plan.</span></span> <span data-ttu-id="c9f86-241">테스트 장애 조치(Failover)에서는 격리된 네트워크에서 장애 조치(Failover) 및 복구 메커니즘을 시뮬레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-241">Test fail-over simulates your fail-over and recovery mechanism in an isolated network.</span></span> <span data-ttu-id="c9f86-242">다음 사항에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="c9f86-242">Note that:</span></span>

* <span data-ttu-id="c9f86-243">Hello 장애 조치 후 원격 데스크톱을 사용 하 여 Azure에서 tooconnect toohello 가상 컴퓨터를 원하는 경우는 hello 테스트 장애 조치를 실행 하기 전에 hello 가상 컴퓨터에서 원격 데스크톱 연결을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-243">If you want tooconnect toohello virtual machine in Azure using Remote Desktop after hello fail-over, enable Remote Desktop Connection on hello virtual machine before you run hello test failover.</span></span>
* <span data-ttu-id="c9f86-244">장애 조치 후 원격 데스크톱을 사용 하 여 Azure에서 공용 IP 주소 tooconnect toohello 가상 컴퓨터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-244">After fail-over, you'll use a public IP address tooconnect toohello virtual machine in Azure using Remote Desktop.</span></span> <span data-ttu-id="c9f86-245">Toodo이를 확인 하는 공용 주소를 사용 하 여 연결 tooa 가상 컴퓨터를 방해 하는 모든 도메인 정책 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-245">If you want toodo this, ensure you don't have any domain policies that prevent you from connecting tooa virtual machine using a public address.</span></span>

<span data-ttu-id="c9f86-246">hello 작업의 toocheck hello 완료 hello 단계에 따라 [모니터 활동](#monitor)합니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-246">toocheck hello completion of hello operation, follow hello steps in [Monitor Activity](#monitor).</span></span>

### <a name="run-a-test-failover"></a><span data-ttu-id="c9f86-247">테스트 장애 조치(Failover) 실행</span><span class="sxs-lookup"><span data-stu-id="c9f86-247">Run a test failover</span></span>
- <span data-ttu-id="c9f86-248">Hello 다음 명령을 실행 하 여 hello 테스트 장애 조치를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-248">Start hello test failover by running hello following command:</span></span>

       $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

### <a name="run-a-planned-failover"></a><span data-ttu-id="c9f86-249">계획된 장애 조치(Failover) 실행</span><span class="sxs-lookup"><span data-stu-id="c9f86-249">Run a planned failover</span></span>
- <span data-ttu-id="c9f86-250">Hello 다음 명령을 실행 하 여 hello 계획 된 장애 조치를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-250">Start hello planned failover by running hello following command:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

### <a name="run-an-unplanned-failover"></a><span data-ttu-id="c9f86-251">계획되지 않은 장애 조치 실행</span><span class="sxs-lookup"><span data-stu-id="c9f86-251">Run an unplanned failover</span></span>
- <span data-ttu-id="c9f86-252">시작 계획 되지 않은 장애 조치 hello 다음 명령을 실행 하 여 hello:</span><span class="sxs-lookup"><span data-stu-id="c9f86-252">Start hello unplanned failover by running hello following command:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

## <span data-ttu-id="c9f86-253"><a name=monitor></a> 작업 모니터</span><span class="sxs-lookup"><span data-stu-id="c9f86-253"><a name=monitor></a> Monitor Activity</span></span>
<span data-ttu-id="c9f86-254">다음 명령을 toomonitor hello 활동 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-254">Use hello following commands toomonitor hello activity.</span></span> <span data-ttu-id="c9f86-255">Note toowait 사이 처리 toofinish hello에 대 한 작업을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9f86-255">Note that you have toowait in between jobs for hello processing toofinish.</span></span>

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



## <a name="next-steps"></a><span data-ttu-id="c9f86-256">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c9f86-256">Next steps</span></span>
<span data-ttu-id="c9f86-257">[자세히 알아보세요](/powershell/module/azurerm.recoveryservices.backup/#recovery) .</span><span class="sxs-lookup"><span data-stu-id="c9f86-257">[Read more](/powershell/module/azurerm.recoveryservices.backup/#recovery) about Azure Site Recovery with Azure Resource Manager PowerShell cmdlets.</span></span>

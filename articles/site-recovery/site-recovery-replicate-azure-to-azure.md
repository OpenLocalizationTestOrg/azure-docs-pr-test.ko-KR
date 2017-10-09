---
title: "aaaReplicate 응용 프로그램 (Azure tooAzure) | Microsoft Docs"
description: "이 문서에서는 가상의 복제를 tooset 실행 컴퓨터 하는 방법을 설명 Azure 지역에서 Azure의 다른 너무 영역입니다."
services: site-recovery
documentationcenter: 
author: asgang
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 5/22/2017
ms.author: asgang
ms.openlocfilehash: fb190dac14419f892a1c6b45a3d991d8005e4bd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-virtual-machines-tooanother-azure-region"></a><span data-ttu-id="8e8e4-103">Azure 가상 컴퓨터 tooanother Azure 지역 복제</span><span class="sxs-lookup"><span data-stu-id="8e8e4-103">Replicate Azure virtual machines tooanother Azure region</span></span>



>[!NOTE]
>
> <span data-ttu-id="8e8e4-104">Azure Virtual Machines에 대한 Site Recovery 복제는 현재 미리 보기로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e8e4-104">Site Recovery replication for Azure virtual machines is currently in preview.</span></span>

<span data-ttu-id="8e8e4-105">이 문서에서는 가상의 복제를 tooset 실행 컴퓨터 하는 방법을 설명 한 Azure 지역 tooanother Azure 지역에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e8e4-105">This article describes how tooset up replication of virtual machines running in one Azure region tooanother Azure region.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8e8e4-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="8e8e4-106">Prerequisites</span></span>

* <span data-ttu-id="8e8e4-107">hello 문서 복구 서비스 자격 증명 모음 및 사이트 복구에 대 한 이미 알고 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e8e4-107">hello article assumes that you already know about Site Recovery and Recovery Services Vault.</span></span> <span data-ttu-id="8e8e4-108">Toohave 만든 '복구 서비스 자격 증명 모음' 이전 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e8e4-108">You need toohave a 'Recovery services vault' pre created.</span></span>

    >[!NOTE]
    >
    > <span data-ttu-id="8e8e4-109">Hello '복구 서비스 자격 증명 모음'에서 만드는 Vm tooreplicate 저장할 hello 위치 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8e8e4-109">It is recommended that you create hello 'Recovery services vault' in hello location where you want your VMs tooreplicate.</span></span> <span data-ttu-id="8e8e4-110">예를 들어 대상 위치가 '미국 중부'이면 '미국 중부'에 자격 증명 모음을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8e8e4-110">For example, if your target location is 'Central US', create vault in 'Central US'.</span></span>

* <span data-ttu-id="8e8e4-111">Hello Azure Vm에서 NSG 네트워크 보안 그룹 () 규칙 또는 방화벽 프록시 toocontrol 액세스 toooutbound 인터넷 연결을 사용 하는, 경우에 해당 하면 허용 목록 hello 필요한 Url 또는 Ip를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e8e4-111">If you are using Network Security Groups (NSG) rules or firewall proxy toocontrol access toooutbound internet connectivity on hello Azure VMs, ensure that you whitelist hello required URLs or IPs.</span></span> <span data-ttu-id="8e8e4-112">너무 참조[네트워킹 지침 문서](./site-recovery-azure-to-azure-networking-guidance.md) 내용을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e8e4-112">Refer too[Networking guidance document](./site-recovery-azure-to-azure-networking-guidance.md) for more details.</span></span>

* <span data-ttu-id="8e8e4-113">Express 경로 또는 온-프레미스 및 hello 간의 VPN 연결이 있는 경우에 따라, Azure의 위치를 소스 [Azure tooon 프레미스 ExpressRoute에 대 한 사이트 복구 고려 사항 / VPN 구성](site-recovery-azure-to-azure-networking-guidance.md#guidelines-for-existing-azure-to-on-premises-expressroutevpn-configuration) 문서.</span><span class="sxs-lookup"><span data-stu-id="8e8e4-113">If you have an ExpressRoute or a VPN connection between on-premises and hello source location in Azure, follow [Site Recovery Considerations for Azure tooon-premises ExpressRoute / VPN configuration](site-recovery-azure-to-azure-networking-guidance.md#guidelines-for-existing-azure-to-on-premises-expressroutevpn-configuration) document.</span></span>

* <span data-ttu-id="8e8e4-114">Azure 사용자 계정에 필요한 toohave 특정 [권한을](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable Azure 가상 컴퓨터를 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e8e4-114">Your Azure user account needs toohave certain [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replication of an Azure virtual machine.</span></span>

* <span data-ttu-id="8e8e4-115">Azure 구독에 활성화 된 toocreate Vm 있어야 합니다. 원하는 DR 영역으로 toouse hello 대상 위치에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e8e4-115">Your Azure subscription should be enabled toocreate VMs in hello target location you want toouse as DR region.</span></span> <span data-ttu-id="8e8e4-116">지원 tooenable hello 필요한 할당량을 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e8e4-116">You can contact support tooenable hello required quota.</span></span>

## <a name="enable-replication-from-azure-site-recovery-vault"></a><span data-ttu-id="8e8e4-117">Azure Site Recovery 자격 증명 모음에서 복제 사용</span><span class="sxs-lookup"><span data-stu-id="8e8e4-117">Enable replication from Azure Site Recovery vault</span></span>
<span data-ttu-id="8e8e4-118">이 그림에서는 hello ' 동아시아 '는 Azure 위치 toohello ' 동남 아시아 ' 위치에서에서 실행 중인 Vm 복제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e8e4-118">For this illustration, we will replicate VMs running  in hello ‘East Asia’ Azure location toohello ‘South East Asia’ location.</span></span> <span data-ttu-id="8e8e4-119">hello 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8e8e4-119">hello steps are as follows:</span></span>

 <span data-ttu-id="8e8e4-120">클릭 **복제 +** hello 가상 컴퓨터에 대 한 자격 증명 모음 tooenable 복제 hello에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e8e4-120">Click **+Replicate** in hello vault tooenable replication for hello virtual machines.</span></span>

1. <span data-ttu-id="8e8e4-121">**원본:** toohello의 시작 위치 hello 컴퓨터의이 경우에 참조 **Azure**합니다.</span><span class="sxs-lookup"><span data-stu-id="8e8e4-121">**Source:** It refers toohello point of origin of hello machines which in this case is **Azure**.</span></span>

2. <span data-ttu-id="8e8e4-122">**원본 위치:** 저장할 tooprotect 가상 컴퓨터에서 Azure 지역 hello는 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e8e4-122">**Source location:** It is hello Azure region from where you want tooprotect your virtual machines.</span></span> <span data-ttu-id="8e8e4-123">이 그림에 대 한 hello 원본 위치 ' 동아시아 ' 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e8e4-123">For this illustration, hello source location will be 'East Asia'</span></span>

3. <span data-ttu-id="8e8e4-124">**배포 모델:** hello 원본 컴퓨터의 toohello Azure 배포 모델을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e8e4-124">**Deployment model:** It refers toohello Azure deployment model of hello source machines.</span></span> <span data-ttu-id="8e8e4-125">클래식 중 하나를 선택할 수 있습니다 또는 protection hello 다음 단계에 대 한 리소스 관리자 및 toohello 특정 모델에 속한 컴퓨터 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e8e4-125">You can select either classic or resource manager and machines belonging toohello specific model will be listed for protection in hello next step.</span></span>

      >[!NOTE]
      >
      > <span data-ttu-id="8e8e4-126">클래식 가상 컴퓨터는 복제한 후 클래식 가상 컴퓨터로 복구할 수만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e8e4-126">You can only replicate a classic virtual machine and recover it as a classic virtual machine.</span></span> <span data-ttu-id="8e8e4-127">Resource Manager 가상 컴퓨터로는 복구할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8e8e4-127">You cannot recover it as a Resource Manager virtual machine.</span></span>

4. <span data-ttu-id="8e8e4-128">**리소스 그룹:** hello 리소스 그룹 toowhich 속한 원본 가상 컴퓨터의 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e8e4-128">**Resource Group:** It’s hello resource group toowhich your source virtual machines belong.</span></span> <span data-ttu-id="8e8e4-129">Hello 다음 단계에서 보호를 위해 hello 선택한 리소스 그룹 아래의 모든 hello Vm으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e8e4-129">All hello VMs under hello selected resource group will be listed for protection in hello next step.</span></span>

    ![복제 활성화](./media/site-recovery-replicate-azure-to-azure/enabledrwizard1.png)

<span data-ttu-id="8e8e4-131">**가상 컴퓨터 > 가상 컴퓨터 선택**, 클릭 하 고 tooreplicate 사용할 각 컴퓨터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e8e4-131">In **Virtual Machines > Select virtual machines**, click and select each machine you want tooreplicate.</span></span> <span data-ttu-id="8e8e4-132">복제를 활성화할 수 있는 컴퓨터만 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e8e4-132">You can only select machines for which replication can be enabled.</span></span> <span data-ttu-id="8e8e4-133">그런 후 확인을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8e8e4-133">Then click OK.</span></span>
    <span data-ttu-id="8e8e4-134">![복제 활성화](./media/site-recovery-replicate-azure-to-azure/virtualmachine_selection.png)</span><span class="sxs-lookup"><span data-stu-id="8e8e4-134">![Enable replication](./media/site-recovery-replicate-azure-to-azure/virtualmachine_selection.png)</span></span>


<span data-ttu-id="8e8e4-135">설정 섹션에서 대상 사이트 속성을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e8e4-135">Under Settings section you can configure target site properties</span></span>

1. <span data-ttu-id="8e8e4-136">**대상 위치:** 원본 가상 컴퓨터 데이터를 복제할 hello 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="8e8e4-136">**Target Location:**  This is hello location where your source virtual machine data will be replicated.</span></span> <span data-ttu-id="8e8e4-137">선택한 컴퓨터 위치에 따라, 사이트 복구 적절 한 대상 지역 목록 hello 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e8e4-137">Depending upon your selected machines location, Site Recovery will provide you hello list of suitable target regions.</span></span>

    > [!TIP]
    > <span data-ttu-id="8e8e4-138">대상 위치 tookeep 것이 좋습니다 서비스 자격 증명 모음 복구 주기와 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e8e4-138">It is recommended tookeep target location same as of your recovery services vault.</span></span>

2. <span data-ttu-id="8e8e4-139">**대상 리소스 그룹:** 는 hello 리소스 그룹 toowhich 모든 복제 된 가상 컴퓨터에 속하게 됩니다. 기본적으로 ASR 새 리소스 그룹에에서 만들어집니다 hello 대상 지역 이름은 "asr" 접미사.</span><span class="sxs-lookup"><span data-stu-id="8e8e4-139">**Target resource group :** It is hello resource group toowhich all your replicated virtual machines will belong.By default ASR will create a new resource group in hello target region with name having "asr" suffix.</span></span> <span data-ttu-id="8e8e4-140">ASR에서 이미 만든 리소스 그룹에 존재 하는 경우 재사용 됩니다. Toocustomize 선택할 수도 있습니다 hello 섹션 아래에서 설명 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8e8e4-140">In case resource group created by ASR already exist, it will be reused.You can also choose toocustomize it as shown in hello section below.</span></span>    
3. <span data-ttu-id="8e8e4-141">**대상 가상 네트워크:** 기본적으로 ASR 새 가상 네트워크에에서 만들어집니다 hello 대상 지역 이름은 "asr" 접미사입니다.</span><span class="sxs-lookup"><span data-stu-id="8e8e4-141">**Target Virtual Network:** By default, ASR will create a new virtual network in hello target region with name having "asr" suffix.</span></span> <span data-ttu-id="8e8e4-142">이렇게 매핑된 tooyour 원본 네트워크 되 고 이후의 모든 보호에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e8e4-142">This will be mapped tooyour source network and will be used for any future protection.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8e8e4-143">[네트워킹 정보를 확인](site-recovery-network-mapping-azure-to-azure.md) tooknow 네트워크 매핑에 대 한 자세한 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e8e4-143">[Check networking details](site-recovery-network-mapping-azure-to-azure.md) tooknow more about network mapping.</span></span>

4. <span data-ttu-id="8e8e4-144">**대상 저장소 계정:** 기본적으로 ASR hello 새 대상 저장소 계정을 만듭니다 소스 VM 저장소 구성이 모방 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e8e4-144">**Target Storage accounts:** By default, ASR will create hello new target storage account mimicking your source VM storage configuration.</span></span> <span data-ttu-id="8e8e4-145">ASR에서 만든 저장소 계정이 이미 있는 경우 해당 계정이 재사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e8e4-145">In case storage account created by ASR already exist, it will be reused.</span></span>

5. <span data-ttu-id="8e8e4-146">**저장소 계정은 캐시:** ASR hello 소스 영역에 캐시 저장소를 호출 하는 추가 저장소 계정이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e8e4-146">**Cache Storage accounts:** ASR needs extra storage account called cache storage in hello source region.</span></span> <span data-ttu-id="8e8e4-147">모든 hello 소스 Vm 추적 되 고 해당 toohello 대상 위치를 복제 하기 전에 toocache 저장소 계정 전송 hello의 상황을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e8e4-147">All hello changes happening on hello source VMs are tracked and sent toocache storage account before replicating those toohello target location.</span></span>

6. <span data-ttu-id="8e8e4-148">**가용성 집합:** 기본적으로 ASR "asr" 접미사가 이름과 설정 hello 대상 지역에 새 가용성 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="8e8e4-148">**Availability set :** By default, ASR will create a new availability set in hello target region with name having "asr" suffix.</span></span> <span data-ttu-id="8e8e4-149">ASR에서 만든 가용성 집합이 이미 있는 경우 해당 집합이 재사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e8e4-149">In case availability set created by ASR already exist, it will be reused.</span></span>

7.  <span data-ttu-id="8e8e4-150">**복제 정책:** 복구 지점 보존 기록 및 응용 프로그램 일치 스냅숏 빈도 대 한 hello 설정을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e8e4-150">**Replication Policy:** It defines hello settings for recovery point retention history and app consistent snapshot frequency.</span></span> <span data-ttu-id="8e8e4-151">기본적으로 ASR은 복구 지점 보존의 경우 기본'24시간' 설정으로, 앱 일치 스냅숏 빈도의 경우 '60분' 설정으로 새 복제 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8e8e4-151">By default, ASR will create a new replication policy with default settings of ‘24 hours’ for recovery point retention and ’60 minutes’ for app consistent snapshot frequency.</span></span>

    ![복제 활성화](./media/site-recovery-replicate-azure-to-azure/enabledrwizard3.PNG)

## <a name="customize-target-resources"></a><span data-ttu-id="8e8e4-153">대상 리소스 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="8e8e4-153">Customize target resources</span></span>

<span data-ttu-id="8e8e4-154">ASR에서 사용 하는 toochange hello 기본값을 원하는 경우에 필요에 따라 hello 설정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e8e4-154">In case you want toochange hello defaults used by ASR, you can change hello settings based on your needs.</span></span>

1. <span data-ttu-id="8e8e4-155">**사용자 지정:** toochange 클릭 hello ASR에서 사용 하는 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="8e8e4-155">**Customize:** Click it toochange hello defaults used by ASR.</span></span>

2. <span data-ttu-id="8e8e4-156">**대상 리소스 그룹:** hello 구독 내에서 hello 대상 위치에 있는 모든 hello 리소스 그룹의 hello 목록에서 hello 리소스 그룹을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e8e4-156">**Target resource group :**  You can select hello resource group from hello list of all hello resource groups existing in hello target location within hello subscription.</span></span>

3. <span data-ttu-id="8e8e4-157">**대상 가상 네트워크:** hello 대상 위치에 hello 목록이 모든 hello 가상 네트워크를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e8e4-157">**Target Virtual Network:** You can find hello list of all hello virtual network in hello target location.</span></span>

4. <span data-ttu-id="8e8e4-158">**가용성 집합:** 가용성 집합 설정 toohello 가상 컴퓨터 가용성 소스 지역에서의 일부인만 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e8e4-158">**Availability set :** You can only add availability sets settings toohello virtual machines which are a part of availability in source region.</span></span>

5. <span data-ttu-id="8e8e4-159">**대상 저장소 계정:**</span><span class="sxs-lookup"><span data-stu-id="8e8e4-159">**Target Storage accounts:**</span></span>

<span data-ttu-id="8e8e4-160">![복제를 사용하도록 설정](./media/site-recovery-replicate-azure-to-azure/customize.PNG) **대상 리소스 만들기**를 클릭하고 복제를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8e8e4-160">![Enable replication](./media/site-recovery-replicate-azure-to-azure/customize.PNG) Click on **Create target resource** and Enable Replication</span></span>


<span data-ttu-id="8e8e4-161">가상 컴퓨터가 보호 되 면 아래에서 Vm 상태의 hello 상태를 확인할 수 있습니다 **복제 항목**</span><span class="sxs-lookup"><span data-stu-id="8e8e4-161">Once virtual machines are protected you can check hello status of VMs health under **Replicated items**</span></span>

>[!NOTE]
><span data-ttu-id="8e8e4-162">Hello 하는 동안 초기 복제 발생 가능성이 상태는 시간 toorefresh 및 일정 시간 동안 진행률을 표시 되지 않으면 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e8e4-162">During hello time of initial replication there could a possibility that status takes time toorefresh and you don't see progress for some time.</span></span> <span data-ttu-id="8e8e4-163">Hello 블레이드 tooget hello 최신 상태 hello 위에 hello 새로 고침 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e8e4-163">You can click hello Refresh button on hello top of hello blade tooget hello latest status.</span></span>
>

![복제 활성화](./media/site-recovery-replicate-azure-to-azure/replicateditems.PNG)


## <a name="next-steps"></a><span data-ttu-id="8e8e4-165">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8e8e4-165">Next steps</span></span>
- <span data-ttu-id="8e8e4-166">테스트 장애 조치(failover) 실행에 대해 [자세히 알아보세요](site-recovery-test-failover-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="8e8e4-166">[Learn more](site-recovery-test-failover-to-azure.md) about running a test failover.</span></span>
- <span data-ttu-id="8e8e4-167">[자세한 내용은](site-recovery-failover.md) 다양 한 유형의 장애 조치에 대 한 방법과 toorun 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e8e4-167">[Learn more](site-recovery-failover.md) about different types of failovers, and how toorun them.</span></span>
- <span data-ttu-id="8e8e4-168">에 대 한 자세한 내용은 [복구 계획을 사용 하 여](site-recovery-create-recovery-plans.md) tooreduce RTO 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e8e4-168">Learn more about [using recovery plans](site-recovery-create-recovery-plans.md) tooreduce RTO.</span></span>
- <span data-ttu-id="8e8e4-169">장애 조치(failover) 후에 [Azure VM을 다시 보호](site-recovery-how-to-reprotect.md)하는 방법에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="8e8e4-169">Learn more about [reprotecting Azure  VMs](site-recovery-how-to-reprotect.md) after failover.</span></span>

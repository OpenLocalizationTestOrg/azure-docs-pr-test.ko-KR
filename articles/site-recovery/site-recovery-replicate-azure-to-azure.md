---
title: "응용 프로그램 복제(Azure에서 Azure로) | Microsoft Docs"
description: "이 문서에서는 하나의 Azure 지역에서 실행 중인 가상 컴퓨터의 복제를 Azure의 다른 지역으로 설정하는 방법을 설명합니다."
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
ms.openlocfilehash: f9f97cf840b722c8cfee169dd1640e0682f287ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-azure-virtual-machines-to-another-azure-region"></a><span data-ttu-id="d7798-103">다른 Azure 지역으로 Azure 가상 컴퓨터 복제</span><span class="sxs-lookup"><span data-stu-id="d7798-103">Replicate Azure virtual machines to another Azure region</span></span>



>[!NOTE]
>
> <span data-ttu-id="d7798-104">Azure 가상 컴퓨터에 대한 Site Recovery 복제는 현재 미리 보기로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7798-104">Site Recovery replication for Azure virtual machines is currently in preview.</span></span>

<span data-ttu-id="d7798-105">이 문서에서는 하나의 Azure 지역에서 실행 중인 가상 컴퓨터의 복제를 다른 Azure 지역으로 설정하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d7798-105">This article describes how to set up replication of virtual machines running in one Azure region to another Azure region.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d7798-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d7798-106">Prerequisites</span></span>

* <span data-ttu-id="d7798-107">이 문서에서는 Site Recovery 및 Recovery Services 자격 증명 모음에 대해 이미 알고 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="d7798-107">The article assumes that you already know about Site Recovery and Recovery Services Vault.</span></span> <span data-ttu-id="d7798-108">사전에 만들어진 'Recovery Services 자격 증명 모음'이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7798-108">You need to have a 'Recovery services vault' pre created.</span></span>

    >[!NOTE]
    >
    > <span data-ttu-id="d7798-109">'Recovery Services 자격 증명 모음'은 VM을 복제할 위치에 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d7798-109">It is recommended that you create the 'Recovery services vault' in the location where you want your VMs to replicate.</span></span> <span data-ttu-id="d7798-110">예를 들어 대상 위치가 '미국 중부'이면 '미국 중부'에 자격 증명 모음을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d7798-110">For example, if your target location is 'Central US', create vault in 'Central US'.</span></span>

* <span data-ttu-id="d7798-111">NSG(네트워크 보안 그룹) 규칙 또는 방화벽 프록시를 사용하여 Azure VM의 아웃바운드 인터넷 연결에 대한 액세스를 제어하는 경우 필요한 URL 또는 IP가 허용 목록에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d7798-111">If you are using Network Security Groups (NSG) rules or firewall proxy to control access to outbound internet connectivity on the Azure VMs, ensure that you whitelist the required URLs or IPs.</span></span> <span data-ttu-id="d7798-112">자세한 내용은 [네트워킹 지침 문서](./site-recovery-azure-to-azure-networking-guidance.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d7798-112">Refer to [Networking guidance document](./site-recovery-azure-to-azure-networking-guidance.md) for more details.</span></span>

* <span data-ttu-id="d7798-113">Azure의 원본 위치와 온-프레미스 간에 ExpressRoute 또는 VPN 연결이 있는 경우 [온-프레미스 ExpressRoute/VPN 구성에 대한 Azure Site Recovery 고려 사항](site-recovery-azure-to-azure-networking-guidance.md#guidelines-for-existing-azure-to-on-premises-expressroutevpn-configuration) 문서에 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="d7798-113">If you have an ExpressRoute or a VPN connection between on-premises and the source location in Azure, follow [Site Recovery Considerations for Azure to on-premises ExpressRoute / VPN configuration](site-recovery-azure-to-azure-networking-guidance.md#guidelines-for-existing-azure-to-on-premises-expressroutevpn-configuration) document.</span></span>

* <span data-ttu-id="d7798-114">Azure 가상 컴퓨터 복제를 사용하려면 Azure 사용자 계정에 특정 [사용 권한](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7798-114">Your Azure user account needs to have certain [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) to enable replication of an Azure virtual machine.</span></span>

* <span data-ttu-id="d7798-115">DR 지역으로 사용할 대상 위치에서 VM을 만들려면 Azure 구독을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7798-115">Your Azure subscription should be enabled to create VMs in the target location you want to use as DR region.</span></span> <span data-ttu-id="d7798-116">지원 팀에 문의하여 필요한 할당량을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7798-116">You can contact support to enable the required quota.</span></span>

## <a name="enable-replication-from-azure-site-recovery-vault"></a><span data-ttu-id="d7798-117">Azure Site Recovery 자격 증명 모음에서 복제 사용</span><span class="sxs-lookup"><span data-stu-id="d7798-117">Enable replication from Azure Site Recovery vault</span></span>
<span data-ttu-id="d7798-118">이 설명에서는 '동아시아' Azure 위치에서 실행 중인 VM을 '동남 아시아' 위치로 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="d7798-118">For this illustration, we will replicate VMs running  in the ‘East Asia’ Azure location to the ‘South East Asia’ location.</span></span> <span data-ttu-id="d7798-119">단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d7798-119">The steps are as follows:</span></span>

 <span data-ttu-id="d7798-120">자격 증명 모음에서 **+복제**를 클릭하여 가상 컴퓨터에 대해 복제를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d7798-120">Click **+Replicate** in the vault to enable replication for the virtual machines.</span></span>

1. <span data-ttu-id="d7798-121">**원본:** 이 경우 **Azure**인 컴퓨터의 원점을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="d7798-121">**Source:** It refers to the point of origin of the machines which in this case is **Azure**.</span></span>

2. <span data-ttu-id="d7798-122">**원본 위치:** 가상 컴퓨터를 보호할 Azure 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="d7798-122">**Source location:** It is the Azure region from where you want to protect your virtual machines.</span></span> <span data-ttu-id="d7798-123">이 설명에서는 원본 위치가 '동아시아'입니다.</span><span class="sxs-lookup"><span data-stu-id="d7798-123">For this illustration, the source location will be 'East Asia'</span></span>

3. <span data-ttu-id="d7798-124">**배포 모델:** 원본 컴퓨터의 Azure 배포 모델을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="d7798-124">**Deployment model:** It refers to the Azure deployment model of the source machines.</span></span> <span data-ttu-id="d7798-125">클래식 또는 리소스 관리자를 선택할 수 있으며 특정 모델에 속한 컴퓨터는 다음 단계에서 보호를 위해 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7798-125">You can select either classic or resource manager and machines belonging to the specific model will be listed for protection in the next step.</span></span>

      >[!NOTE]
      >
      > <span data-ttu-id="d7798-126">클래식 가상 컴퓨터를 복제하면 클래식 가상 컴퓨터로만 복구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7798-126">You can only replicate a classic virtual machine and recover it as a classic virtual machine.</span></span> <span data-ttu-id="d7798-127">Resource Manager 가상 컴퓨터로 복구할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d7798-127">You cannot recover it as a Resource Manager virtual machine.</span></span>

4. <span data-ttu-id="d7798-128">**리소스 그룹:** 원본 가상 컴퓨터가 속해 있는 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="d7798-128">**Resource Group:** It’s the resource group to which your source virtual machines belong.</span></span> <span data-ttu-id="d7798-129">선택한 리소스 그룹 아래의 모든 VM은 다음 단계에서 보호를 위해 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7798-129">All the VMs under the selected resource group will be listed for protection in the next step.</span></span>

    ![복제 활성화](./media/site-recovery-replicate-azure-to-azure/enabledrwizard1.png)

<span data-ttu-id="d7798-131">**Virtual Machines > 가상 컴퓨터 선택**에서 복제하려는 각 컴퓨터를 클릭하여 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d7798-131">In **Virtual Machines > Select virtual machines**, click and select each machine you want to replicate.</span></span> <span data-ttu-id="d7798-132">복제를 활성화할 수 있는 컴퓨터만 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7798-132">You can only select machines for which replication can be enabled.</span></span> <span data-ttu-id="d7798-133">그런 후 확인을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d7798-133">Then click OK.</span></span>
    <span data-ttu-id="d7798-134">![복제 활성화](./media/site-recovery-replicate-azure-to-azure/virtualmachine_selection.png)</span><span class="sxs-lookup"><span data-stu-id="d7798-134">![Enable replication](./media/site-recovery-replicate-azure-to-azure/virtualmachine_selection.png)</span></span>


<span data-ttu-id="d7798-135">설정 섹션에서 대상 사이트 속성을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7798-135">Under Settings section you can configure target site properties</span></span>

1. <span data-ttu-id="d7798-136">**대상 위치:** 원본 가상 컴퓨터 데이터가 복제될 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="d7798-136">**Target Location:**  This is the location where your source virtual machine data will be replicated.</span></span> <span data-ttu-id="d7798-137">선택한 컴퓨터 위치에 따라 Site Recovery에서 적합한 대상 지역 목록을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d7798-137">Depending upon your selected machines location, Site Recovery will provide you the list of suitable target regions.</span></span>

    > [!TIP]
    > <span data-ttu-id="d7798-138">대상 위치를 복구 서비스 자격 증명 모음과 동일하게 유지하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d7798-138">It is recommended to keep target location same as of your recovery services vault.</span></span>

2. <span data-ttu-id="d7798-139">**대상 리소스 그룹:** 모든 복제된 가상 컴퓨터가 속하게 될 리소스 그룹입니다. 기본적으로 ASR은 이름에 "asr" 접미사가 있는 대상 지역에 새 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d7798-139">**Target resource group :** It is the resource group to which all your replicated virtual machines will belong.By default ASR will create a new resource group in the target region with name having "asr" suffix.</span></span> <span data-ttu-id="d7798-140">ASR에서 만든 리소스 그룹이 이미 있는 경우 해당 그룹이 재사용됩니다. 아래 섹션에 표시된 대로 사용자 지정하도록 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7798-140">In case resource group created by ASR already exist, it will be reused.You can also choose to customize it as shown in the section below.</span></span>    
3. <span data-ttu-id="d7798-141">**대상 가상 네트워크:** 기본적으로 ASR은 이름에 "asr" 접미사가 있는 대상 지역에 새 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d7798-141">**Target Virtual Network:** By default, ASR will create a new virtual network in the target region with name having "asr" suffix.</span></span> <span data-ttu-id="d7798-142">이 가상 네트워크는 원본 네트워크에 매핑되고 이후의 모든 보호를 위해 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7798-142">This will be mapped to your source network and will be used for any future protection.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d7798-143">네트워크 매핑에 대해 더 자세히 알아보려면 [네트워킹 세부 정보를 확인](site-recovery-network-mapping-azure-to-azure.md)하세요.</span><span class="sxs-lookup"><span data-stu-id="d7798-143">[Check networking details](site-recovery-network-mapping-azure-to-azure.md) to know more about network mapping.</span></span>

4. <span data-ttu-id="d7798-144">**대상 저장소 계정:** 기본적으로 ASR은 소스 VM 저장소 구성을 모방하는 새 대상 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d7798-144">**Target Storage accounts:** By default, ASR will create the new target storage account mimicking your source VM storage configuration.</span></span> <span data-ttu-id="d7798-145">ASR에서 만든 저장소 계정이 이미 있는 경우 해당 계정이 재사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7798-145">In case storage account created by ASR already exist, it will be reused.</span></span>

5. <span data-ttu-id="d7798-146">**캐시 저장소 계정:** ASR은 소스 지역에 캐시 저장소로 불리는 추가 저장소 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7798-146">**Cache Storage accounts:** ASR needs extra storage account called cache storage in the source region.</span></span> <span data-ttu-id="d7798-147">원본 VM에서 발생하는 모든 변경 내용이 대상 위치로 복제되기 전에 추적되고 캐시 저장소 계정으로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7798-147">All the changes happening on the source VMs are tracked and sent to cache storage account before replicating those to the target location.</span></span>

6. <span data-ttu-id="d7798-148">**가용성 집합:** 기본적으로 ASR은 이름에 "asr" 접미사가 있는 대상 지역에 새 가용성 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d7798-148">**Availability set :** By default, ASR will create a new availability set in the target region with name having "asr" suffix.</span></span> <span data-ttu-id="d7798-149">ASR에서 만든 가용성 집합이 이미 있는 경우 해당 집합이 재사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7798-149">In case availability set created by ASR already exist, it will be reused.</span></span>

7.  <span data-ttu-id="d7798-150">**복제 정책:** 복구 지점 보존 기록 및 앱 일치 스냅숏 빈도 대한 설정을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="d7798-150">**Replication Policy:** It defines the settings for recovery point retention history and app consistent snapshot frequency.</span></span> <span data-ttu-id="d7798-151">기본적으로 ASR은 복구 지점 보존의 경우 기본'24시간' 설정으로, 앱 일치 스냅숏 빈도의 경우 '60분' 설정으로 새 복제 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d7798-151">By default, ASR will create a new replication policy with default settings of ‘24 hours’ for recovery point retention and ’60 minutes’ for app consistent snapshot frequency.</span></span>

    ![복제 활성화](./media/site-recovery-replicate-azure-to-azure/enabledrwizard3.PNG)

## <a name="customize-target-resources"></a><span data-ttu-id="d7798-153">대상 리소스 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="d7798-153">Customize target resources</span></span>

<span data-ttu-id="d7798-154">ASR에서 사용하는 기본값을 변경하려면 필요에 따라 설정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7798-154">In case you want to change the defaults used by ASR, you can change the settings based on your needs.</span></span>

1. <span data-ttu-id="d7798-155">**사용자 지정:** ASR에서 사용하는 기본값을 변경하려면 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d7798-155">**Customize:** Click it to change the defaults used by ASR.</span></span>

2. <span data-ttu-id="d7798-156">**대상 리소스 그룹:** 구독 내 대상 위치에 있는 모든 리소스 그룹의 목록에서 리소스 그룹을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7798-156">**Target resource group :**  You can select the resource group from the list of all the resource groups existing in the target location within the subscription.</span></span>

3. <span data-ttu-id="d7798-157">**대상 가상 네트워크:** 대상 위치에서 모든 가상 네트워크 목록을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7798-157">**Target Virtual Network:** You can find the list of all the virtual network in the target location.</span></span>

4. <span data-ttu-id="d7798-158">**가용성 집합:** 가용성 집합 설정은 소스 영역에서 가용성의 일부인 가상 컴퓨터에만 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7798-158">**Availability set :** You can only add availability sets settings to the virtual machines which are a part of availability in source region.</span></span>

5. <span data-ttu-id="d7798-159">**대상 저장소 계정:**</span><span class="sxs-lookup"><span data-stu-id="d7798-159">**Target Storage accounts:**</span></span>

<span data-ttu-id="d7798-160">![복제를 사용하도록 설정](./media/site-recovery-replicate-azure-to-azure/customize.PNG) **대상 리소스 만들기**를 클릭하고 복제를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d7798-160">![Enable replication](./media/site-recovery-replicate-azure-to-azure/customize.PNG) Click on **Create target resource** and Enable Replication</span></span>


<span data-ttu-id="d7798-161">가상 컴퓨터가 보호되면 **복제 항목** 아래 VM 상태의 상태를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7798-161">Once virtual machines are protected you can check the status of VMs health under **Replicated items**</span></span>

>[!NOTE]
><span data-ttu-id="d7798-162">초기 복제 기간 중 상태를 새로 고치는 데 시간이 걸릴 수도 있고 일정 시간 동안 진행률이 표시되지 않을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7798-162">During the time of initial replication there could a possibility that status takes time to refresh and you don't see progress for some time.</span></span> <span data-ttu-id="d7798-163">최신 상태를 가져오려면 블레이드 맨 위에 있는 [새로 고침] 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d7798-163">You can click the Refresh button on the top of the blade to get the latest status.</span></span>
>

![복제 활성화](./media/site-recovery-replicate-azure-to-azure/replicateditems.PNG)


## <a name="next-steps"></a><span data-ttu-id="d7798-165">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d7798-165">Next steps</span></span>
- <span data-ttu-id="d7798-166">테스트 장애 조치(failover) 실행에 대해 [자세히 알아보세요](site-recovery-test-failover-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="d7798-166">[Learn more](site-recovery-test-failover-to-azure.md) about running a test failover.</span></span>
- <span data-ttu-id="d7798-167">여러 장애 조치 유형 및 장애 조치 실행 방법에 대해 [자세히 알아보세요](site-recovery-failover.md).</span><span class="sxs-lookup"><span data-stu-id="d7798-167">[Learn more](site-recovery-failover.md) about different types of failovers, and how to run them.</span></span>
- <span data-ttu-id="d7798-168">[복구 계획을 사용](site-recovery-create-recovery-plans.md)하여 RTO를 줄이는 방법에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="d7798-168">Learn more about [using recovery plans](site-recovery-create-recovery-plans.md) to reduce RTO.</span></span>
- <span data-ttu-id="d7798-169">장애 조치(failover) 후에 [Azure VM을 다시 보호](site-recovery-how-to-reprotect.md)하는 방법에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="d7798-169">Learn more about [reprotecting Azure  VMs](site-recovery-how-to-reprotect.md) after failover.</span></span>

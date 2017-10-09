---
title: "복제 tooAzure VMware에 대 한 테스트 장애 조치 aaaRun | Microsoft Docs"
description: "VMware Vm tooAzure hello Azure Site Recovery 서비스를 사용 하 여 복제에 대 한 테스트 장애 조치를 실행 하는 데 필요한 hello 단계를 요약 합니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a640e139-3a09-4ad8-8283-8fa92544f4c6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: bed934446f0c6940089bfae24a13de4fb1556a62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-12-run-a-test-failover-tooazure-for-vmware-vms"></a><span data-ttu-id="0b838-103">12 단계: VMware Vm에 대 한 테스트 장애 조치 tooAzure 실행</span><span class="sxs-lookup"><span data-stu-id="0b838-103">Step 12: Run a test failover tooAzure for VMware VMs</span></span>

<span data-ttu-id="0b838-104">이 문서에서 설명 하는 방법을 toorun 테스트 장애 조치에서 온-프레미스 VMware 가상 컴퓨터 hello를 사용 하 여 tooAzure [Azure Site Recovery](site-recovery-overview.md) hello Azure 포털의에서 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="0b838-104">This article describes how toorun a test failover from  on-premises VMware virtual machines tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="0b838-105">Hello 아래쪽 hello 또는이 문서에 의견과 질문을 게시 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.</span><span class="sxs-lookup"><span data-stu-id="0b838-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="before-you-start"></a><span data-ttu-id="0b838-106">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="0b838-106">Before you start</span></span>

<span data-ttu-id="0b838-107">Hello VM 속성을 확인 하 고 변경 하는 것을 권장 하는 테스트 장애 조치를 실행 하기 전에 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b838-107">Before you run a test failover we recommend that you verify hello VM properties, and make any changes you need to.</span></span> <span data-ttu-id="0b838-108">hello VM 속성에 액세스할 수 있습니다 **복제 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="0b838-108">you can access hello VM properties in **Replicated items**.</span></span> <span data-ttu-id="0b838-109">hello **Essentials** 블레이드 컴퓨터 설정 및 상태에 대 한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b838-109">hello **Essentials** blade shows information about machines settings and status.</span></span>

## <a name="managed-disk-considerations"></a><span data-ttu-id="0b838-110">Managed Disk 고려 사항</span><span class="sxs-lookup"><span data-stu-id="0b838-110">Managed disk considerations</span></span>

<span data-ttu-id="0b838-111">[관리 디스크](../virtual-machines/windows/managed-disks-overview.md) hello VM 디스크와 연결 된 hello 저장소 계정을 관리 하 여 Azure Vm에 대 한 디스크 관리를 단순화 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b838-111">[Managed disks](../virtual-machines/windows/managed-disks-overview.md) simplify disk management for Azure VMs, by managing hello storage accounts associated with hello VM disks.</span></span> 

- <span data-ttu-id="0b838-112">VM에 대 한 보호를 사용 하도록 설정 하면 VM 데이터 tooa 저장소 계정을 복제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b838-112">When you enable protection for a VM, VM data replicates tooa storage account.</span></span> <span data-ttu-id="0b838-113">관리 되는 디스크에 생성 되 고 장애 조치 발생 toohello VM 연결.</span><span class="sxs-lookup"><span data-stu-id="0b838-113">Managed disks are created and attached toohello VM only when failover occurs.</span></span>
- <span data-ttu-id="0b838-114">Hello 리소스 관리자 모델을 사용 하 여 배포할 Vm에 대해서만 관리 하는 디스크를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b838-114">Managed disks can be created only for VMs deployed using hello Resource Manager model.</span></span>  
- <span data-ttu-id="0b838-115">이 설정을 사용하면, **관리 디스크 사용**을 활성화한 리소스 그룹의 가용성 집합만 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b838-115">With this setting enabled, only availability sets in Resource Groups that have **Use managed disks** enabled can be selected.</span></span> <span data-ttu-id="0b838-116">가용성 집합에 관리 되는 디스크와 Vm 있어야 **관리 되는 디스크 사용** 도**예**합니다.</span><span class="sxs-lookup"><span data-stu-id="0b838-116">VMs with managed disks must be in availability sets with **Use managed disks** set too**Yes**.</span></span> <span data-ttu-id="0b838-117">Vm에 대 한 hello 설정을 활성화 하지 않으면 가용성 집합에만 리소스 그룹에 사용 하도록 설정 하는 관리 되는 디스크 없이 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b838-117">If hello setting isn't enabled for VMs, then only availability sets in Resource Groups without managed disks enabled can be selected.</span></span>
- <span data-ttu-id="0b838-118">관리 디스크와 가용성 집합에 대해 [자세히 알아봅니다](https://docs.microsoft.com/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set).</span><span class="sxs-lookup"><span data-stu-id="0b838-118">[Learn more](https://docs.microsoft.com/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set) about managed disks and availability sets.</span></span>
- <span data-ttu-id="0b838-119">복제를 위해 사용할 hello 저장소 계정의 저장소 서비스 암호화로 암호화 된, 하는 경우 장애 조치 중 관리 되는 디스크를 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0b838-119">If hello storage account you use for replication has been encrypted with Storage Service Encryption, managed disks can't be created during failover.</span></span> <span data-ttu-id="0b838-120">이 경우 관리 되는 디스크의 사용을 활성화 하 고 또는 VM hello에 대 한 보호를 사용 하지 않도록 설정 하 고, toouse 없는 경우 암호화를 사용 하는 저장소 계정을 다시 설정 하지 않는 하나.</span><span class="sxs-lookup"><span data-stu-id="0b838-120">In this case either don't enable use of managed disks, or disable protection for hello VM, and reenable it toouse a storage account that doesn't have encryption enabled.</span></span> <span data-ttu-id="0b838-121">[자세히 알아봅니다](https://docs.microsoft.com/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption).</span><span class="sxs-lookup"><span data-stu-id="0b838-121">[Learn more](https://docs.microsoft.com/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption).</span></span>


## <a name="network-considerations"></a><span data-ttu-id="0b838-122">네트워크 고려 사항</span><span class="sxs-lookup"><span data-stu-id="0b838-122">Network considerations</span></span>

<span data-ttu-id="0b838-123">장애 조치 후에 만든 Azure VM에 대 한 hello 대상 IP 주소를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b838-123">You can set hello target IP address for an Azure VM created after failover.</span></span>

- <span data-ttu-id="0b838-124">주소를 제공 하지 않으면 장애 조치 컴퓨터 hello DHCP를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b838-124">If you don't provide an address, hello failed over machine will use DHCP.</span></span>
- <span data-ttu-id="0b838-125">장애 조치(failover) 시 사용할 수 없는 주소를 설정하면 장애 조치(failover)가 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0b838-125">If you set an address that isn't available at failover, failover won't work.</span></span>
- <span data-ttu-id="0b838-126">hello hello 주소는 hello 테스트 장애 조치 네트워크에서 사용할 수 있는 하는 경우 테스트 장애 조치에 대해 동일한 대상 IP 주소를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b838-126">hello same target IP address can be used for test failover, if hello address is available in hello test failover network.</span></span>
- <span data-ttu-id="0b838-127">네트워크 어댑터의 hello 수 hello 대상 가상 컴퓨터에 대해 지정 하는 hello 크기에 따라 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b838-127">hello number of network adapters is dictated by hello size you specify for hello target virtual machine:</span></span>

     - <span data-ttu-id="0b838-128">Hello hello 원본 컴퓨터의 네트워크 어댑터 수가 hello 대상 컴퓨터 크기에 허용 된 어댑터의 hello 개수 보다 작거나 같은 다른 이름으로 hello 경우 hello 대상 갖습니다 hello hello 소스와 같은 수의 어댑터.</span><span class="sxs-lookup"><span data-stu-id="0b838-128">If hello number of network adapters on hello source machine is hello same as, or less than, hello number of adapters allowed for hello target machine size, then hello target will have hello same number of adapters as hello source.</span></span>
     - <span data-ttu-id="0b838-129">Hello hello에 대 한 어댑터 수가 원본 가상 컴퓨터는 hello 대상 크기는 최대 사용 됩니다 hello 대상 크기에 허용 된 hello 수를 초과 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b838-129">If hello number of adapters for hello source virtual machine exceeds hello number allowed for hello target size, then hello target size maximum will be used.</span></span>
     - <span data-ttu-id="0b838-130">예를 들어, 원본 컴퓨터에 네트워크 어댑터가 두 개 있고을 hello 대상 컴퓨터 크기를 지 원하는 4 개 경우 hello 대상 컴퓨터에 두 개의 어댑터 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="0b838-130">For example, if a source machine has two network adapters and hello target machine size supports four, hello target machine will have two adapters.</span></span> <span data-ttu-id="0b838-131">Hello 원본 컴퓨터에 두 개의 어댑터가 있지만 hello 지원 되는 대상 크기 하나만 지원 하는 경우 hello 대상 컴퓨터에서 하나의 어댑터를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b838-131">If hello source machine has two adapters but hello supported target size only supports one then hello target machine will have only one adapter.</span></span>     
   - <span data-ttu-id="0b838-132">Hello 가상 컴퓨터에 여러 네트워크 어댑터는 모든 연결 toohello 동일한 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="0b838-132">If hello virtual machine has multiple network adapters they will all connect toohello same network.</span></span>
   - <span data-ttu-id="0b838-133">Hello 가상 컴퓨터에 여러 네트워크 어댑터가 다음 hello 경우 먼저 하나 hello 목록에 표시 될 hello *기본* hello Azure 가상 컴퓨터의에서 네트워크 어댑터입니다.</span><span class="sxs-lookup"><span data-stu-id="0b838-133">If hello virtual machine has multiple network adapters then hello first one shown in hello list becomes hello *Default* network adapter in hello Azure virtual machine.</span></span>
 - <span data-ttu-id="0b838-134">IP 주소를 지정하는 방법에 대해 [자세히 알아봅니다](vmware-walkthrough-network.md).</span><span class="sxs-lookup"><span data-stu-id="0b838-134">[Learn more](vmware-walkthrough-network.md) about IP addressing.</span></span>



## <a name="view-and-modify-vm-settings"></a><span data-ttu-id="0b838-135">VM 설정 보기 및 수정</span><span class="sxs-lookup"><span data-stu-id="0b838-135">View and modify VM settings</span></span>

<span data-ttu-id="0b838-136">장애 조치를 실행 하기 전에 hello 원본 컴퓨터의 hello 속성을 확인 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0b838-136">We recommend that you verify hello properties of hello source machine before you run a failover.</span></span>

1. <span data-ttu-id="0b838-137">**보호 된 항목**, 클릭 **복제 항목**, hello VM을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b838-137">In **Protected Items**, click **Replicated Items**, and click hello VM.</span></span>
2. <span data-ttu-id="0b838-138">Hello에 **복제 된 항목** 창 VM 정보, 상태 상태 및 hello 최신 사용 가능한 복구 지점은 요약을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b838-138">In hello **Replicated item** pane, you can see a summary of VM information, health status, and hello latest available recovery points.</span></span> <span data-ttu-id="0b838-139">클릭 **속성** tooview 더 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b838-139">Click **Properties** tooview more details.</span></span>
3. <span data-ttu-id="0b838-140">**계산 및 네트워크**에서 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b838-140">In **Compute and Network**, you can:</span></span>
    - <span data-ttu-id="0b838-141">Hello Azure VM 이름을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b838-141">Modify hello Azure VM name.</span></span> <span data-ttu-id="0b838-142">hello 이름은 만족 해야 합니다 [Azure 요구 사항](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)합니다.</span><span class="sxs-lookup"><span data-stu-id="0b838-142">hello name must meet [Azure requirements](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>
    - <span data-ttu-id="0b838-143">장애 조치(failover) 후 [리소스 그룹]을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0b838-143">Specify a post-failover [resource group].</span></span>
    - <span data-ttu-id="0b838-144">Hello Azure VM에 대 한 대상 크기를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b838-144">Specify a target size for hello Azure VM</span></span>
    - <span data-ttu-id="0b838-145">[가용성 집합](../virtual-machines/windows/tutorial-availability-sets.md)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0b838-145">Select an [availability set](../virtual-machines/windows/tutorial-availability-sets.md).</span></span>
    - <span data-ttu-id="0b838-146">지정 여부 toouse [관리 디스크](#managed-disk-considerations)합니다.</span><span class="sxs-lookup"><span data-stu-id="0b838-146">Specify whether toouse [managed disks](#managed-disk-considerations).</span></span> <span data-ttu-id="0b838-147">선택 **예**tooattach 마이그레이션 tooAzure에 tooyour 컴퓨터를 관리 하는 디스크를 하려는 경우.</span><span class="sxs-lookup"><span data-stu-id="0b838-147">Select **Yes**, if you want tooattach managed disks tooyour machine on migration tooAzure.</span></span>
    - <span data-ttu-id="0b838-148">보거나 hello 네트워크/서브넷이 있는 hello에 Azure VM 배치 될 장애 조치 후 및 할당할 tooit hello IP 주소 등의 네트워크 설정을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b838-148">View or modify network settings, including hello network/subnet in which hello Azure VM will be located after failover, and hello IP address that will be assigned tooit.</span></span>
4. <span data-ttu-id="0b838-149">**디스크**및 hello 운영 체제에 대 한 정보를 확인할 수 있습니다에 데이터 디스크 VM hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b838-149">In **Disks**, you can see information about hello operating system and data disks on hello VM.</span></span>

## <a name="run-a-test-failover"></a><span data-ttu-id="0b838-150">테스트 장애 조치(Failover) 실행</span><span class="sxs-lookup"><span data-stu-id="0b838-150">Run a test failover</span></span>

<span data-ttu-id="0b838-151">한 모든 항목을 설정한 후에 모든 것이 예상 대로 작동 하는지 테스트 장애 조치 toomake를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b838-151">After you've set everything up, run a test failover toomake sure everything's working as expected.</span></span>

- <span data-ttu-id="0b838-152">Tooconnect tooAzure Vm을 원하는 경우 RDP를 사용 하 여 장애 조치 후 [tooconnect 준비](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover)합니다.</span><span class="sxs-lookup"><span data-stu-id="0b838-152">If you want tooconnect tooAzure VMs using RDP after failover, [prepare tooconnect](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover).</span></span>
 - <span data-ttu-id="0b838-153">테스트 환경에서 Active Directory 및 DNS toocopy 필요한 toofully 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b838-153">toofully test you need toocopy of Active Directory and DNS in your test environment.</span></span> <span data-ttu-id="0b838-154">[자세히 알아봅니다](site-recovery-active-directory.md#test-failover-considerations).</span><span class="sxs-lookup"><span data-stu-id="0b838-154">[Learn more](site-recovery-active-directory.md#test-failover-considerations).</span></span>
 - <span data-ttu-id="0b838-155">테스트 장애 조치(failover)에 대한 전체 정보는 [이 문서](site-recovery-test-failover-to-azure.md)를 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="0b838-155">For full information about test failover, read [this article](site-recovery-test-failover-to-azure.md) article.</span></span>
- <span data-ttu-id="0b838-156">시작하기 전에 간단한 동영상 개요를 보세요.</span><span class="sxs-lookup"><span data-stu-id="0b838-156">Get a quick video overview before you start:</span></span>


     >[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video4-Recovery-Plan-DR-Drill-and-Failover/player]


<span data-ttu-id="0b838-157">이제 장애 조치(Failover)를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0b838-157">Now, run a failover:</span></span>

1. <span data-ttu-id="0b838-158">단일 컴퓨터를 통해 toofail에서 **설정** > **복제 항목**, hello VM을 클릭 > **+ 테스트 장애 조치** 아이콘.</span><span class="sxs-lookup"><span data-stu-id="0b838-158">toofail over a single machine, in **Settings** > **Replicated Items**, click hello VM > **+Test Failover** icon.</span></span>

    ![테스트 장애 조치(Failover)](./media/vmware-walkthrough-test-failover/test-failover.png)

2. <span data-ttu-id="0b838-160">복구를 통해 toofail 계획 **설정** > **복구 계획**를 마우스 오른쪽 단추로 클릭 hello 계획 > **테스트 장애 조치**합니다.</span><span class="sxs-lookup"><span data-stu-id="0b838-160">toofail over a recovery plan, in **Settings** > **Recovery Plans**, right-click hello plan > **Test Failover**.</span></span> <span data-ttu-id="0b838-161">복구 계획 toocreate [다음이 지침에 따라](site-recovery-create-recovery-plans.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0b838-161">toocreate a recovery plan, [follow these instructions](site-recovery-create-recovery-plans.md).</span></span>  

3. <span data-ttu-id="0b838-162">**테스트 장애 조치**선택, 장애 조치 발생 후 hello Azure 네트워크 toowhich Azure Vm 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b838-162">In **Test Failover**, select hello Azure network toowhich Azure VMs will be connected after failover occurs.</span></span>

4. <span data-ttu-id="0b838-163">클릭 **확인** toobegin hello 장애 조치 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b838-163">Click **OK** toobegin hello failover.</span></span> <span data-ttu-id="0b838-164">Hello 또는 hello VM tooopen에 해당 속성을 클릭 하 여 진행률을 추적할 수 **테스트 장애 조치** 자격 증명 모음 이름에는 작업 > **설정** > **작업**  >  **사이트 복구 작업이**합니다.</span><span class="sxs-lookup"><span data-stu-id="0b838-164">You can track progress by clicking on hello VM tooopen its properties, or on hello **Test Failover** job in vault name > **Settings** > **Jobs** > **Site Recovery jobs**.</span></span>

5. <span data-ttu-id="0b838-165">Hello 장애 조치가 끝나면도 있어야 toosee hello 복제본 Azure 컴퓨터 hello Azure 포털에에서 표시 > **가상 컴퓨터**합니다.</span><span class="sxs-lookup"><span data-stu-id="0b838-165">After hello failover completes, you should also be able toosee hello replica Azure machine appear in hello Azure portal > **Virtual Machines**.</span></span> <span data-ttu-id="0b838-166">해당 hello VM 실행 되 고 toohello 적절 한 네트워크 연결 된 hello 적절 한 크기 인지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b838-166">You should make sure that hello VM is hello appropriate size, that it's connected toohello appropriate network, and that it's running.</span></span>

6. <span data-ttu-id="0b838-167">연결에 대 한 장애 조치 후 준비 수 tooconnect toohello Azure VM이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b838-167">If you prepared for connections after failover, you should be able tooconnect toohello Azure VM.</span></span>

7. <span data-ttu-id="0b838-168">를 완료 한 후 클릭 **테스트 장애 조치 정리** hello 복구 계획에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b838-168">After you finish, click on **Cleanup test failover** on hello recovery plan.</span></span> <span data-ttu-id="0b838-169">**노트**을 기록 하 고 테스트 장애 조치 hello와 관련 된 모든 관찰을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b838-169">In **Notes**, record and save any observations associated with hello test failover.</span></span> <span data-ttu-id="0b838-170">테스트 장애 조치 중에 생성 된 hello Vm을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b838-170">This will delete hello VMs that were created during test failover.</span></span>



## <a name="next-steps"></a><span data-ttu-id="0b838-171">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0b838-171">Next steps</span></span>

- <span data-ttu-id="0b838-172">[자세한 내용은](site-recovery-failover.md) 다양 한 유형의 장애 조치에 대 한 방법과 toorun 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b838-172">[Learn more](site-recovery-failover.md) about different types of failovers, and how toorun them.</span></span>
- <span data-ttu-id="0b838-173">컴퓨터를 복제하고 장애 복구하는 대신 마이그레이션하는 경우 [여기를 참조하세요](site-recovery-migrate-to-azure.md#migrate-on-premises-vms-and-physical-servers).</span><span class="sxs-lookup"><span data-stu-id="0b838-173">If you're migrating machines rather than replicating and failing back, [read more](site-recovery-migrate-to-azure.md#migrate-on-premises-vms-and-physical-servers).</span></span>
- <span data-ttu-id="0b838-174">[장애 복구에 대해 알아보세요](site-recovery-failback-azure-to-vmware.md), 복제 Azure Vm 및 toofail 다시 toohello 기본 온-프레미스 사이트를 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b838-174">[Read about failback](site-recovery-failback-azure-to-vmware.md), toofail back and replicate Azure VMs back toohello primary on-premises site.</span></span>

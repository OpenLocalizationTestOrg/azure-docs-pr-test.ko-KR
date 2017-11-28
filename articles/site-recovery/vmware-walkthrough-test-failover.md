---
title: "Azure에 대한 VMware 복제를 위한 테스트 장애 조치 실행 | Microsoft Docs"
description: "Azure Site Recovery 서비스를 사용하여 Azure로 VMware VM을 복제하기 위해 테스트 장애 조치(failover)를 실행하는 데 필요한 단계를 요약합니다."
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
ms.openlocfilehash: f1a6df56a2bb0094d972d2e659057cc124156b88
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="step-12-run-a-test-failover-to-azure-for-vmware-vms"></a><span data-ttu-id="963b8-103">12단계: Azure에 VMware VM에 대한 테스트 장애 조치 실행</span><span class="sxs-lookup"><span data-stu-id="963b8-103">Step 12: Run a test failover to Azure for VMware VMs</span></span>

<span data-ttu-id="963b8-104">이 문서에서는 Azure Portal에서 [Azure Site Recovery](site-recovery-overview.md) 서비스를 사용하여 온-프레미스 VMware 가상 컴퓨터에서 Azure에 테스트 장애 조치를 실행하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="963b8-104">This article describes how to run a test failover from  on-premises VMware virtual machines to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="963b8-105">이 문서의 하단 또는 [Azure Recovery Services 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)에서 의견이나 질문을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="963b8-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="before-you-start"></a><span data-ttu-id="963b8-106">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="963b8-106">Before you start</span></span>

<span data-ttu-id="963b8-107">테스트 장애 조치(failover)를 실행하기 전에 VM 속성을 확인하고 필요한 사항을 변경하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="963b8-107">Before you run a test failover we recommend that you verify the VM properties, and make any changes you need to.</span></span> <span data-ttu-id="963b8-108">**복제 항목**에서 VM 속성에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="963b8-108">you can access the VM properties in **Replicated items**.</span></span> <span data-ttu-id="963b8-109">**Essentials** 블레이드는 컴퓨터 설정 및 상태에 대한 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="963b8-109">The **Essentials** blade shows information about machines settings and status.</span></span>

## <a name="managed-disk-considerations"></a><span data-ttu-id="963b8-110">Managed Disk 고려 사항</span><span class="sxs-lookup"><span data-stu-id="963b8-110">Managed disk considerations</span></span>

<span data-ttu-id="963b8-111">[Managed Disks](../virtual-machines/windows/managed-disks-overview.md)는 VM 디스크와 연결된 저장소 계정을 관리하여 Azure VM의 디스크 관리를 간소화합니다.</span><span class="sxs-lookup"><span data-stu-id="963b8-111">[Managed disks](../virtual-machines/windows/managed-disks-overview.md) simplify disk management for Azure VMs, by managing the storage accounts associated with the VM disks.</span></span> 

- <span data-ttu-id="963b8-112">VM에 보호를 활성화하면 VM 데이터는 저장소 계정에 복제됩니다.</span><span class="sxs-lookup"><span data-stu-id="963b8-112">When you enable protection for a VM, VM data replicates to a storage account.</span></span> <span data-ttu-id="963b8-113">Managed Disks는 장애 조치(failover) 시에만 생성되고 VM에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="963b8-113">Managed disks are created and attached to the VM only when failover occurs.</span></span>
- <span data-ttu-id="963b8-114">Resource Manager 배포 모델을 사용하여 배포된 VM에 대해서만 Managed Disks를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="963b8-114">Managed disks can be created only for VMs deployed using the Resource Manager model.</span></span>  
- <span data-ttu-id="963b8-115">이 설정을 사용하면, **Managed Disks 사용**을 활성화한 리소스 그룹의 가용성 집합만 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="963b8-115">With this setting enabled, only availability sets in Resource Groups that have **Use managed disks** enabled can be selected.</span></span> <span data-ttu-id="963b8-116">관리 디스크가 있는 VM은 가용성 집합에 있어야 하며 **관리 디스크 사용** 설정이 **예**로 되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="963b8-116">VMs with managed disks must be in availability sets with **Use managed disks** set to **Yes**.</span></span> <span data-ttu-id="963b8-117">VM에서 이 설정을 사용하지 않는 경우 활성화한 관리 디스크가 없는 리소스 그룹의 가용성 집합만 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="963b8-117">If the setting isn't enabled for VMs, then only availability sets in Resource Groups without managed disks enabled can be selected.</span></span>
- <span data-ttu-id="963b8-118">관리 디스크와 가용성 집합에 대해 [자세히 알아봅니다](https://docs.microsoft.com/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set).</span><span class="sxs-lookup"><span data-stu-id="963b8-118">[Learn more](https://docs.microsoft.com/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set) about managed disks and availability sets.</span></span>
- <span data-ttu-id="963b8-119">복제에 사용하는 저장소 계정이 저장소 서비스 암호화로 암호화된 경우에는 장애 조치(failover)를 수행하는 도중에 관리 디스크를 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="963b8-119">If the storage account you use for replication has been encrypted with Storage Service Encryption, managed disks can't be created during failover.</span></span> <span data-ttu-id="963b8-120">이 경우 관리 디스크의 사용을 활성화하거나 VM에 대한 보호를 비활성화하고, 활성화된 암호화가 없는 저장소 계정을 사용하도록 다시 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="963b8-120">In this case either don't enable use of managed disks, or disable protection for the VM, and reenable it to use a storage account that doesn't have encryption enabled.</span></span> <span data-ttu-id="963b8-121">[자세히 알아보기](https://docs.microsoft.com/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption).</span><span class="sxs-lookup"><span data-stu-id="963b8-121">[Learn more](https://docs.microsoft.com/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption).</span></span>


## <a name="network-considerations"></a><span data-ttu-id="963b8-122">네트워크 고려 사항</span><span class="sxs-lookup"><span data-stu-id="963b8-122">Network considerations</span></span>

<span data-ttu-id="963b8-123">장애 조치 후에 만든 Azure VM에 대상 IP 주소를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="963b8-123">You can set the target IP address for an Azure VM created after failover.</span></span>

- <span data-ttu-id="963b8-124">주소를 입력하지 않으면 장애 조치(Failover)된 컴퓨터가 DHCP를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="963b8-124">If you don't provide an address, the failed over machine will use DHCP.</span></span>
- <span data-ttu-id="963b8-125">장애 조치(failover) 시 사용할 수 없는 주소를 설정하면 장애 조치(failover)가 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="963b8-125">If you set an address that isn't available at failover, failover won't work.</span></span>
- <span data-ttu-id="963b8-126">주소를 테스트 장애 조치(Failover) 네트워크에서 사용할 수 있는 경우 테스트 장애 조치(Failover)에 동일한 대상 IP 주소를 사용해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="963b8-126">The same target IP address can be used for test failover, if the address is available in the test failover network.</span></span>
- <span data-ttu-id="963b8-127">네트워크 어댑터 수는 대상 가상 컴퓨터에 대해 지정하는 크기에 따라 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="963b8-127">The number of network adapters is dictated by the size you specify for the target virtual machine:</span></span>

     - <span data-ttu-id="963b8-128">원본 컴퓨터의 네트워크 어댑터 수가 대상 컴퓨터 크기에 허용되는 어댑터 수보다 작거나 같은 경우, 대상의 어댑터 수는 소스와 동일하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="963b8-128">If the number of network adapters on the source machine is the same as, or less than, the number of adapters allowed for the target machine size, then the target will have the same number of adapters as the source.</span></span>
     - <span data-ttu-id="963b8-129">원본 가상 컴퓨터의 어댑터의 수가 대상 크기에 허용된 수를 초과하면 대상 크기 최대치가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="963b8-129">If the number of adapters for the source virtual machine exceeds the number allowed for the target size, then the target size maximum will be used.</span></span>
     - <span data-ttu-id="963b8-130">예를 들어 원본 컴퓨터에 두 네트워크 어댑터가 있고 대상 컴퓨터 크기가 4를 지원하는 경우, 대상 컴퓨터에는 2개의 어댑터가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="963b8-130">For example, if a source machine has two network adapters and the target machine size supports four, the target machine will have two adapters.</span></span> <span data-ttu-id="963b8-131">원본 컴퓨터에 두 어댑터가 있지만 지원되는 대상 크기가 하나만 지원하는 경우 대상 컴퓨터에는 1개의 어댑터만 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="963b8-131">If the source machine has two adapters but the supported target size only supports one then the target machine will have only one adapter.</span></span>     
   - <span data-ttu-id="963b8-132">가상 컴퓨터에 네트워크 어댑터가 여러 개 있으면 모두 동일한 네트워크에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="963b8-132">If the virtual machine has multiple network adapters they will all connect to the same network.</span></span>
   - <span data-ttu-id="963b8-133">가상 컴퓨터에 네트워크 어댑터가 여러 개 있으면 목록에서 첫 번째 어댑터가 Azure 가상 컴퓨터에서 *기본* 네트워크 어댑터가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="963b8-133">If the virtual machine has multiple network adapters then the first one shown in the list becomes the *Default* network adapter in the Azure virtual machine.</span></span>
 - <span data-ttu-id="963b8-134">IP 주소를 지정하는 방법에 대해 [자세히 알아봅니다](vmware-walkthrough-network.md).</span><span class="sxs-lookup"><span data-stu-id="963b8-134">[Learn more](vmware-walkthrough-network.md) about IP addressing.</span></span>



## <a name="view-and-modify-vm-settings"></a><span data-ttu-id="963b8-135">VM 설정 보기 및 수정</span><span class="sxs-lookup"><span data-stu-id="963b8-135">View and modify VM settings</span></span>

<span data-ttu-id="963b8-136">장애 조치(failover)를 실행하기 전에 원본 컴퓨터의 속성을 확인하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="963b8-136">We recommend that you verify the properties of the source machine before you run a failover.</span></span>

1. <span data-ttu-id="963b8-137">**보호된 항목**에서 **복제된 항목**을 클릭하고 VM을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="963b8-137">In **Protected Items**, click **Replicated Items**, and click the VM.</span></span>
2. <span data-ttu-id="963b8-138">**복제된 항목** 창에서 VM 정보, 상태 및 최신 사용 가능한 복구 지점의 요약을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="963b8-138">In the **Replicated item** pane, you can see a summary of VM information, health status, and the latest available recovery points.</span></span> <span data-ttu-id="963b8-139">자세한 내용을 보려면 **속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="963b8-139">Click **Properties** to view more details.</span></span>
3. <span data-ttu-id="963b8-140">**계산 및 네트워크**에서 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="963b8-140">In **Compute and Network**, you can:</span></span>
    - <span data-ttu-id="963b8-141">Azure VM 이름을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="963b8-141">Modify the Azure VM name.</span></span> <span data-ttu-id="963b8-142">이름은 [Azure 요구 사항](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)을 충족해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="963b8-142">The name must meet [Azure requirements](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>
    - <span data-ttu-id="963b8-143">장애 조치(failover) 후 [리소스 그룹]을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="963b8-143">Specify a post-failover [resource group].</span></span>
    - <span data-ttu-id="963b8-144">Azure VM에 대한 대상 크기를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="963b8-144">Specify a target size for the Azure VM</span></span>
    - <span data-ttu-id="963b8-145">[가용성 집합](../virtual-machines/windows/tutorial-availability-sets.md)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="963b8-145">Select an [availability set](../virtual-machines/windows/tutorial-availability-sets.md).</span></span>
    - <span data-ttu-id="963b8-146">[관리 디스크](#managed-disk-considerations)의 사용 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="963b8-146">Specify whether to use [managed disks](#managed-disk-considerations).</span></span> <span data-ttu-id="963b8-147">관리 디스크를 Azure로의 마이그레이션에서 컴퓨터에 연결하려는 경우 **예**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="963b8-147">Select **Yes**, if you want to attach managed disks to your machine on migration to Azure.</span></span>
    - <span data-ttu-id="963b8-148">장애 조치(failover) 후 Azure VM이 배치될 네트워크/서브넷 및 할당되는 IP 주소를 포함한 네트워크 설정을 보거나 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="963b8-148">View or modify network settings, including the network/subnet in which the Azure VM will be located after failover, and the IP address that will be assigned to it.</span></span>
4. <span data-ttu-id="963b8-149">**디스크**에서 VM의 운영 체제 및 데이터 디스크에 대한 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="963b8-149">In **Disks**, you can see information about the operating system and data disks on the VM.</span></span>

## <a name="run-a-test-failover"></a><span data-ttu-id="963b8-150">테스트 장애 조치(Failover) 실행</span><span class="sxs-lookup"><span data-stu-id="963b8-150">Run a test failover</span></span>

<span data-ttu-id="963b8-151">모든 항목을 설정한 후 모든 것이 예상대로 작동하는지 확인할 수 있도록 테스트 장애 조치를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="963b8-151">After you've set everything up, run a test failover to make sure everything's working as expected.</span></span>

- <span data-ttu-id="963b8-152">장애 조치(failover) 후 RDP를 사용하여 Azure VM에 연결하려면 [연결을 준비](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover)합니다.</span><span class="sxs-lookup"><span data-stu-id="963b8-152">If you want to connect to Azure VMs using RDP after failover, [prepare to connect](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover).</span></span>
 - <span data-ttu-id="963b8-153">완벽하게 테스트하려면 테스트 환경에 Active Directory 및 DNS 복사본이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="963b8-153">To fully test you need to copy of Active Directory and DNS in your test environment.</span></span> <span data-ttu-id="963b8-154">[자세히 알아보기](site-recovery-active-directory.md#test-failover-considerations).</span><span class="sxs-lookup"><span data-stu-id="963b8-154">[Learn more](site-recovery-active-directory.md#test-failover-considerations).</span></span>
 - <span data-ttu-id="963b8-155">테스트 장애 조치(failover)에 대한 전체 정보는 [이 문서](site-recovery-test-failover-to-azure.md)를 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="963b8-155">For full information about test failover, read [this article](site-recovery-test-failover-to-azure.md) article.</span></span>
- <span data-ttu-id="963b8-156">시작하기 전에 간단한 동영상 개요를 보세요.</span><span class="sxs-lookup"><span data-stu-id="963b8-156">Get a quick video overview before you start:</span></span>


     >[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video4-Recovery-Plan-DR-Drill-and-Failover/player]


<span data-ttu-id="963b8-157">이제 장애 조치(Failover)를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="963b8-157">Now, run a failover:</span></span>

1. <span data-ttu-id="963b8-158">단일 컴퓨터를 장애 조치(failover)하려면 **설정** > **복제된 항목**에서 VM > **+테스트 장애 조치(failover)** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="963b8-158">To fail over a single machine, in **Settings** > **Replicated Items**, click the VM > **+Test Failover** icon.</span></span>

    ![테스트 장애 조치(Failover)](./media/vmware-walkthrough-test-failover/test-failover.png)

2. <span data-ttu-id="963b8-160">복구 계획을 장애 조치(Failover)하려면 **설정** > **복구 계획**에서 계획을 마우스 오른쪽 버튼으로 클릭하고 **테스트 장애 조치(Failover)**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="963b8-160">To fail over a recovery plan, in **Settings** > **Recovery Plans**, right-click the plan > **Test Failover**.</span></span> <span data-ttu-id="963b8-161">복구 계획을 만들려면 [다음 지침을 따릅니다](site-recovery-create-recovery-plans.md).</span><span class="sxs-lookup"><span data-stu-id="963b8-161">To create a recovery plan, [follow these instructions](site-recovery-create-recovery-plans.md).</span></span>  

3. <span data-ttu-id="963b8-162">**테스트 장애 조치(failover)**에서 장애 조치(failover)가 발생한 후에 Azure VM이 연결될 Azure 네트워크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="963b8-162">In **Test Failover**, select the Azure network to which Azure VMs will be connected after failover occurs.</span></span>

4. <span data-ttu-id="963b8-163">**확인** 을 클릭하여 장애 조치(Failover)를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="963b8-163">Click **OK** to begin the failover.</span></span> <span data-ttu-id="963b8-164">VM을 클릭하여 속성을 열거나 자격 증명 모음 이름 > **설정** > **작업** > **Site Recovery 작업**의 **테스트 장애 조치(failover)**에서 진행률을 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="963b8-164">You can track progress by clicking on the VM to open its properties, or on the **Test Failover** job in vault name > **Settings** > **Jobs** > **Site Recovery jobs**.</span></span>

5. <span data-ttu-id="963b8-165">또한 장애 조치(failover)가 완료된 후 Azure 포털 > **Virtual Machines**에 Azure 컴퓨터 복제본이 나타나는 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="963b8-165">After the failover completes, you should also be able to see the replica Azure machine appear in the Azure portal > **Virtual Machines**.</span></span> <span data-ttu-id="963b8-166">VM의 크기가 적당하고, 올바른 네트워크에 연결되었고, 실행 중인지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="963b8-166">You should make sure that the VM is the appropriate size, that it's connected to the appropriate network, and that it's running.</span></span>

6. <span data-ttu-id="963b8-167">장애 조치(failover) 후 연결을 준비하는 경우 Azure VM에 연결할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="963b8-167">If you prepared for connections after failover, you should be able to connect to the Azure VM.</span></span>

7. <span data-ttu-id="963b8-168">완료하면 복구 계획에서 **테스트 장애 조치 정리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="963b8-168">After you finish, click on **Cleanup test failover** on the recovery plan.</span></span> <span data-ttu-id="963b8-169">**참고**에서 테스트 장애 조치와 관련된 모든 관측 내용을 기록하고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="963b8-169">In **Notes**, record and save any observations associated with the test failover.</span></span> <span data-ttu-id="963b8-170">그러면 테스트 장애 조치 중에 생성된 VM이 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="963b8-170">This will delete the VMs that were created during test failover.</span></span>



## <a name="next-steps"></a><span data-ttu-id="963b8-171">다음 단계</span><span class="sxs-lookup"><span data-stu-id="963b8-171">Next steps</span></span>

- <span data-ttu-id="963b8-172">여러 장애 조치 유형 및 장애 조치 실행 방법에 대해 [자세히 알아보세요](site-recovery-failover.md).</span><span class="sxs-lookup"><span data-stu-id="963b8-172">[Learn more](site-recovery-failover.md) about different types of failovers, and how to run them.</span></span>
- <span data-ttu-id="963b8-173">컴퓨터를 복제하고 장애 복구하는 대신 마이그레이션하는 경우 [여기를 참조하세요](site-recovery-migrate-to-azure.md#migrate-on-premises-vms-and-physical-servers).</span><span class="sxs-lookup"><span data-stu-id="963b8-173">If you're migrating machines rather than replicating and failing back, [read more](site-recovery-migrate-to-azure.md#migrate-on-premises-vms-and-physical-servers).</span></span>
- <span data-ttu-id="963b8-174">Azure VM을 장애 복구하고 기본 온-프레미스 사이트로 다시 복제하는 [장애 복구(failback)에 대해 자세히 알아보세요](site-recovery-failback-azure-to-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="963b8-174">[Read about failback](site-recovery-failback-azure-to-vmware.md), to fail back and replicate Azure VMs back to the primary on-premises site.</span></span>

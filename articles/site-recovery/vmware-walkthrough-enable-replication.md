---
title: "Azure Site Recovery를 사용하여 Azure에 복제되는 VMware VM에 복제 설정 | Microsoft Docs"
description: "Azure Site Recovery 서비스를 사용하여 VMware VM에 Azure로 복제를 설정하는 데 필요한 단계를 요약합니다."
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 519c5559-7032-4954-b8b5-f24f5242a954
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 470b9ddd8df4a4e74ec7174f79020c252323e502
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="step-11-enable-replication-for-vmware-virtual-machines-to-azure"></a><span data-ttu-id="66118-103">11단계: Azure에 VMware 가상 컴퓨터의 복제 설정</span><span class="sxs-lookup"><span data-stu-id="66118-103">Step 11: Enable replication for VMware virtual machines to Azure</span></span>


<span data-ttu-id="66118-104">이 문서에서는 Azure Portal에서 [Azure Site Recovery](site-recovery-overview.md) 서비스를 사용하여 온-프레미스 VMware 가상 컴퓨터를 Azure에 복제하도록 설정하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="66118-104">This article describes how to enable replication for on-premises VMware virtual machines to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="66118-105">이 문서의 하단 또는 [Azure Recovery Services 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)에서 의견이나 질문을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="66118-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="before-you-start"></a><span data-ttu-id="66118-106">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="66118-106">Before you start</span></span>

- <span data-ttu-id="66118-107">VMware VM에는 [모바일 서비스 구성 요소가 설치](vmware-walkthrough-install-mobility.md)되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66118-107">VMware VMs must have the [Mobility service component installed](vmware-walkthrough-install-mobility.md).</span></span> <span data-ttu-id="66118-108">복제를 사용하도록 설정하는 경우 푸시 설치용으로 VM이 준비되면 프로세스 서버가 자동으로 모바일 서비스를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="66118-108">- If a VM is prepared for push installation, the process server automatically installs the Mobility service when you enable replication.</span></span>
- <span data-ttu-id="66118-109">Azure 사용자 계정에는 Azure에 VM을 복제할 수 있는 특정 [사용 권한](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66118-109">Your Azure user account needs specific [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) to enable replication of a VM to Azure</span></span>
- <span data-ttu-id="66118-110">VM을 추가하거나 수정하는 경우 변경 사항이 적용되어 포털에 표시되는 데 15분 이상 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66118-110">When you add or modify VMs, it can take up to 15 minutes or longer for changes to take effect, and for them to appear in the portal.</span></span>
- <span data-ttu-id="66118-111">**구성 서버** > **마지막 연락**에서 VM을 마지막으로 검색한 시간을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66118-111">You can check the last discovered time for VMs in **Configuration Servers** > **Last Contact At**.</span></span>
- <span data-ttu-id="66118-112">예약된 검색을 기다리지 않고 VM을 추가하려면 구성 서버를 강조 표시하고(클릭하지 않음) **새로 고침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="66118-112">To add VMs without waiting for the scheduled discovery, highlight the configuration server (don’t click it), and click **Refresh**.</span></span>



## <a name="exclude-disks-from-replication"></a><span data-ttu-id="66118-113">복제에서 디스크 제외</span><span class="sxs-lookup"><span data-stu-id="66118-113">Exclude disks from replication</span></span>

<span data-ttu-id="66118-114">기본적으로 컴퓨터의 모든 디스크가 복제됩니다.</span><span class="sxs-lookup"><span data-stu-id="66118-114">By default all disks on a machine are replicated.</span></span> <span data-ttu-id="66118-115">디스크를 복제에서 제외할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66118-115">You can exclude disks from replication.</span></span> <span data-ttu-id="66118-116">예를 들어 임시 데이터 또는 컴퓨터나 응용 프로그램이 다시 시작할 때마다 새로 고쳐지는 데이터(예: pagefile.sys 또는 SQL Server tempdb)가 포함된 디스크를 복제하고 싶지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66118-116">For example you might not want to replicate disks with temporary data, or data that's refreshed each time a machine or application restarts (for example pagefile.sys or SQL Server tempdb).</span></span> [<span data-ttu-id="66118-117">자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="66118-117">Learn more</span></span>](site-recovery-exclude-disk.md)

## <a name="replicate-vms"></a><span data-ttu-id="66118-118">VM 복제</span><span class="sxs-lookup"><span data-stu-id="66118-118">Replicate VMs</span></span>

<span data-ttu-id="66118-119">시작하기 전에 간단한 동영상 개요를 보세요.</span><span class="sxs-lookup"><span data-stu-id="66118-119">Before you start, watch a quick video overview</span></span>

>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video3-Protect-VMware-Virtual-Machines/player]

1. <span data-ttu-id="66118-120">**2단계: 응용 프로그램 복제** > **원본**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="66118-120">Click **Step 2: Replicate application** > **Source**.</span></span>
2. <span data-ttu-id="66118-121">**원본**에서 구성 서버를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="66118-121">In **Source**, select the configuration server.</span></span>
3. <span data-ttu-id="66118-122">**컴퓨터 형식**에서 **가상 컴퓨터**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="66118-122">In **Machine type**, select **Virtual Machines**.</span></span>
4. <span data-ttu-id="66118-123">**vCenter/vSphere 하이퍼바이저**에서 vSphere 호스트를 관리하는 vCenter Server를 선택하거나 해당 호스트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="66118-123">In **vCenter/vSphere Hypervisor**, select the vCenter server that manages the vSphere host, or select the host.</span></span>
5. <span data-ttu-id="66118-124">프로세스 서버를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="66118-124">Select the process server.</span></span> <span data-ttu-id="66118-125">추가 프로세스 서버를 만들지 않은 경우 이 프로세스 서버가 구성 서버가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="66118-125">If you haven't created any additional process servers this will be the configuration server.</span></span> <span data-ttu-id="66118-126">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="66118-126">Then click **OK**.</span></span>

    ![복제 활성화](./media/vmware-walkthrough-enable-replication/enable-replication2.png)

6. <span data-ttu-id="66118-128">**대상**에서 장애 조치 VM을 만들려는 구독 및 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="66118-128">In **Target**, select the subscription and the resource group in which you want to create the failed over VMs.</span></span> <span data-ttu-id="66118-129">장애 조치 VM에 대해 Azure(클래식 또는 리소스 관리)에서 사용할 배포 모델을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="66118-129">Choose the deployment model that you want to use in Azure (classic or resource management), for the failed over VMs.</span></span>


7. <span data-ttu-id="66118-130">데이터 복제에 사용할 Azure Storage 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="66118-130">Select the Azure storage account you want to use for replicating data.</span></span> <span data-ttu-id="66118-131">이미 설정한 계정을 사용하지 않으려면 새로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66118-131">If you don't want to use an account you've already set up, you can create a new one.</span></span>

8. <span data-ttu-id="66118-132">장애 조치(Failover) 후 Azure VM이 생성될 때 연결될 Azure 네트워크 및 서브넷을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="66118-132">Select the Azure network and subnet to which Azure VMs will connect, when they're created after failover.</span></span> <span data-ttu-id="66118-133">컴퓨터마다 Azure 네트워크를 선택하려면 **나중에 구성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="66118-133">Select **Configure now for selected machines**, to apply the network setting to all machines you select for protection.</span></span> <span data-ttu-id="66118-134">네트워크가 없는 경우 **만들어야** 합니다.</span><span class="sxs-lookup"><span data-stu-id="66118-134">Select **Configure later** to select the Azure network per machine.</span></span> <span data-ttu-id="66118-135">기존 네트워크를 사용하지 않으려면 하나를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66118-135">If you don't want to use an existing network, you can create one.</span></span>

    ![복제 활성화](./media/vmware-walkthrough-enable-replication/enable-rep3.png)
9. <span data-ttu-id="66118-137">**Virtual Machines** > **가상 컴퓨터 선택**에서 복제하려는 각 컴퓨터를 클릭하여 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="66118-137">In **Virtual Machines** > **Select virtual machines**, click and select each machine you want to replicate.</span></span> <span data-ttu-id="66118-138">복제를 활성화할 수 있는 컴퓨터만 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66118-138">You can only select machines for which replication can be enabled.</span></span> <span data-ttu-id="66118-139">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="66118-139">Then click **OK**.</span></span>

    ![복제 활성화](./media/vmware-walkthrough-enable-replication/enable-replication5.png)
10. <span data-ttu-id="66118-141">**속성** > **속성 구성**에서 프로세스 서버가 자동으로 컴퓨터에 모바일 서비스를 설치하는 데 사용할 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="66118-141">In **Properties** > **Configure properties**, select the account that will be used by the process server to automatically install the Mobility service on the machine.</span></span>
11. <span data-ttu-id="66118-142">기본적으로 모든 디스크가 복제됩니다.</span><span class="sxs-lookup"><span data-stu-id="66118-142">By default all disks are replicated.</span></span> <span data-ttu-id="66118-143">**모든 디스크** 를 클릭하고 복제하지 않으려는 디스크를 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="66118-143">Click **All Disks** and clear any disks you don't want to replicate.</span></span> <span data-ttu-id="66118-144">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="66118-144">Then click **OK**.</span></span> <span data-ttu-id="66118-145">나중에 추가 VM 속성을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66118-145">You can set additional VM properties later.</span></span>

    ![복제 활성화](./media/vmware-walkthrough-enable-replication/enable-replication6.png)
11. <span data-ttu-id="66118-147">**복제 설정** > **복제 설정 구성**에서 올바른 복제 정책이 선택되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="66118-147">In **Replication settings** > **Configure replication settings**, verify that the correct replication policy is selected.</span></span> <span data-ttu-id="66118-148">정책을 수정하면 복제 중인 컴퓨터와 새 컴퓨터에 변경 내용이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="66118-148">If you modify a policy, changes will be applied to replicating machine, and to new machines.</span></span>
12. <span data-ttu-id="66118-149">컴퓨터를 복제 그룹으로 수집하려는 경우 **다중 VM 일관성** 을 사용하도록 설정하고 그룹에 대한 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="66118-149">Enable **Multi-VM consistency** if you want to gather machines into a replication group, and specify a name for the group.</span></span> <span data-ttu-id="66118-150">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="66118-150">Then click **OK**.</span></span> <span data-ttu-id="66118-151">다음 사항에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="66118-151">Note that:</span></span>

    * <span data-ttu-id="66118-152">복제 그룹의 컴퓨터는 함께 복제되고 장애 조치(failover) 시 공유 크래시 일관성 및 앱 일치 복구 지점을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="66118-152">Machines in replication groups replicate together, and have shared crash-consistent and app-consistent recovery points when they fail over.</span></span>
    * <span data-ttu-id="66118-153">워크로드를 미러링하도록 VM 및 물리적 서버를 함께 수집하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="66118-153">We recommend that you gather VMs and physical servers together so that they mirror your workloads.</span></span> <span data-ttu-id="66118-154">다중 VM 일관성을 사용하도록 설정하면 워크로드 성능에 영향을 줄 수 있습니다. 컴퓨터가 동일한 워크로드를 실행하고 일관성이 필요한 경우에만 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66118-154">Enabling multi-VM consistency can impact workload performance, and should only be used if machines are running the same workload and you need consistency.</span></span>

    ![복제 활성화](./media/vmware-walkthrough-enable-replication/enable-replication7.png)
13. <span data-ttu-id="66118-156">**복제 사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="66118-156">Click **Enable Replication**.</span></span> <span data-ttu-id="66118-157">**설정** > **작업** > **Site Recovery 작업**에서 **보호 사용** 작업의 진행률을 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66118-157">You can track progress of the **Enable Protection** job in **Settings** > **Jobs** > **Site Recovery Jobs**.</span></span> <span data-ttu-id="66118-158">**보호 완료** 작업이 실행된 후에는 컴퓨터가 장애 조치(failover)를 수행할 준비가 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66118-158">After the **Finalize Protection** job runs the machine is ready for failover.</span></span>

## <a name="next-steps"></a><span data-ttu-id="66118-159">다음 단계</span><span class="sxs-lookup"><span data-stu-id="66118-159">Next steps</span></span>

<span data-ttu-id="66118-160">[12단계: 테스트 장애 조치(failover) 실행](vmware-walkthrough-test-failover.md)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="66118-160">Go to [Step 12: Run a test failover](vmware-walkthrough-test-failover.md)</span></span>

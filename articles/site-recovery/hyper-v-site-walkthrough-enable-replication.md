---
title: "Azure Site Recovery를 사용하여 Azure로 Hyper-V VM 복제(System Center VMM 없음)를 위한 복제 설정 | Microsoft Docs"
description: "Azure Site Recovery 서비스를 사용하여 Hyper-V VM을 Azure로 복제를 활성화하는 데 필요한 단계를 요약합니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: bd31ef01-69f1-4591-a519-e42510a6e2f4
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: aabe99dbd375b80e4a87ca7a067927008672b4ed
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="step-10-enable-replication-for-hyper-v-vms-replicating-to-azure"></a><span data-ttu-id="79a50-103">10단계: Azure로 Hyper-V VM 복제를 위한 복제를 활성화</span><span class="sxs-lookup"><span data-stu-id="79a50-103">Step 10: Enable replication for Hyper-V VMs replicating to Azure</span></span>


<span data-ttu-id="79a50-104">이 문서에서는 Azure Portal에서 [Azure Site Recovery](site-recovery-overview.md) 서비스를 사용하여 Azure로 온-프레미스 Hyper-V 가상 컴퓨터(System Center VMM에서 관리되지 않음) 복제를 활성화하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="79a50-104">This article describes how to enable replication for on-premises Hyper-V virtual machines (not managed by System Center VMM) to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="79a50-105">이 문서의 하단 또는 [Azure Recovery Services 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)에서 의견이나 질문을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="79a50-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>




## <a name="before-you-start"></a><span data-ttu-id="79a50-106">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="79a50-106">Before you start</span></span>

<span data-ttu-id="79a50-107">시작하기 전에 Azure 사용자 계정에 Azure로 새 가상 컴퓨터 복제를 활성화하는 데 필요한 [사용 권한](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="79a50-107">Before you start, ensure that your Azure user account has the required [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) to enable replication of a new virtual machine to Azure.</span></span>

## <a name="exclude-disks-from-replication"></a><span data-ttu-id="79a50-108">복제에서 디스크 제외</span><span class="sxs-lookup"><span data-stu-id="79a50-108">Exclude disks from replication</span></span>

<span data-ttu-id="79a50-109">기본적으로 컴퓨터의 모든 디스크가 복제됩니다.</span><span class="sxs-lookup"><span data-stu-id="79a50-109">By default all disks on a machine are replicated.</span></span> <span data-ttu-id="79a50-110">디스크를 복제에서 제외할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79a50-110">You can exclude disks from replication.</span></span> <span data-ttu-id="79a50-111">예를 들어 임시 데이터 또는 컴퓨터나 응용 프로그램이 다시 시작할 때마다 새로 고쳐지는 데이터(예: pagefile.sys 또는 SQL Server tempdb)가 포함된 디스크를 복제하고 싶지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79a50-111">For example you might not want to replicate disks with temporary data, or data that's refreshed each time a machine or application restarts (for example pagefile.sys or SQL Server tempdb).</span></span> [<span data-ttu-id="79a50-112">자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="79a50-112">Learn more</span></span>](site-recovery-exclude-disk.md)


## <a name="replicate-vms"></a><span data-ttu-id="79a50-113">VM 복제</span><span class="sxs-lookup"><span data-stu-id="79a50-113">Replicate VMs</span></span>

<span data-ttu-id="79a50-114">다음과 같이 VM에 대해 복제를 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="79a50-114">Enable replication for VMs as follows:</span></span>          

1. <span data-ttu-id="79a50-115">**응용 프로그램 복제** > **원본**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79a50-115">Click **Replicate application** > **Source**.</span></span> <span data-ttu-id="79a50-116">처음으로 복제를 설정한 후에는 **+복제**를 클릭하여 추가 컴퓨터에 대해 복제를 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79a50-116">After you've set up replication for the first time, you can click **+Replicate** to enable replication for additional machines.</span></span>

    ![복제 활성화](./media/hyper-v-site-walkthrough-enable-replication/enable-replication.png)
2. <span data-ttu-id="79a50-118">**원본**에서 Hyper-V 사이트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="79a50-118">In **Source**, select the Hyper-V site.</span></span> <span data-ttu-id="79a50-119">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79a50-119">Then click **OK**.</span></span>
3. <span data-ttu-id="79a50-120">**대상**에서 자격 증명 모음 구독을 선택하고, 장애 조치(failover) 후 Azure에서 사용할 장애 조치(failover) 모델(클래식 또는 리소스 관리)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="79a50-120">In **Target**, select the vault subscription, and the failover model you want to use in Azure (classic or resource management) after failover.</span></span>
4. <span data-ttu-id="79a50-121">사용하려는 저장소 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="79a50-121">Select the storage account you want to use.</span></span> <span data-ttu-id="79a50-122">사용하려는 계정이 없는 경우 [새로 만들 수 있습니다](#set-up-an-azure-storage-account).</span><span class="sxs-lookup"><span data-stu-id="79a50-122">If you don't have an account you want to use, you can [create one](#set-up-an-azure-storage-account).</span></span> <span data-ttu-id="79a50-123">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79a50-123">Then click **OK**.</span></span>
5. <span data-ttu-id="79a50-124">장애 조치(failover) 후 Azure VM이 생성될 때 연결할 Azure 네트워크 및 서브넷을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="79a50-124">Select the Azure network and subnet to which Azure VMs will connect when they're created failover.</span></span>

    - <span data-ttu-id="79a50-125">복제를 활성화한 모든 컴퓨터에 네트워크 설정을 적용하려면 **선택한 컴퓨터에 대해 지금 구성합니다.**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="79a50-125">To apply the network settings to all machines you enable for replication, select **Configure now for selected machines**.</span></span>
    - <span data-ttu-id="79a50-126">네트워크가 없는 경우 **만들어야** 합니다.</span><span class="sxs-lookup"><span data-stu-id="79a50-126">Select **Configure later** to select the Azure network per machine.</span></span>
    - <span data-ttu-id="79a50-127">사용하려는 네트워크가 없는 경우 [새로 만들 수 있습니다](#set-up-an-azure-network).</span><span class="sxs-lookup"><span data-stu-id="79a50-127">If you don't have a network you want to use, you can [create one](#set-up-an-azure-network).</span></span> <span data-ttu-id="79a50-128">해당하는 경우 서브넷을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="79a50-128">Select a subnet if applicable.</span></span> <span data-ttu-id="79a50-129">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79a50-129">Then click **OK**.</span></span>

   ![복제 활성화](./media/hyper-v-site-walkthrough-enable-replication/enable-replication11.png)

6. <span data-ttu-id="79a50-131">**Virtual Machines** > **가상 컴퓨터 선택**에서 복제하려는 각 컴퓨터를 클릭하여 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="79a50-131">In **Virtual Machines** > **Select virtual machines**, click and select each machine you want to replicate.</span></span> <span data-ttu-id="79a50-132">복제를 활성화할 수 있는 컴퓨터만 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79a50-132">You can only select machines for which replication can be enabled.</span></span> <span data-ttu-id="79a50-133">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79a50-133">Then click **OK**.</span></span>

    ![복제 활성화](./media/hyper-v-site-walkthrough-enable-replication/enable-replication5-for-exclude-disk.png)

7. <span data-ttu-id="79a50-135">**속성** > **속성 구성**에서 선택한 VM의 운영 체제 및 OS 디스크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="79a50-135">In **Properties** > **Configure properties**, select the operating system for the selected VMs, and the OS disk.</span></span>
8. <span data-ttu-id="79a50-136">Azure VM 이름(대상 이름)이 [Azure Virtual Machine 요구 사항](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)을 충족하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="79a50-136">Verify that the Azure VM name (target name) complies with [Azure virtual machine requirements](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>
9. <span data-ttu-id="79a50-137">기본적으로 VM의 모든 디스크는 복제를 위해 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="79a50-137">By default all the disks of the VM are selected for replication.</span></span> <span data-ttu-id="79a50-138">디스크를 지워서 제외시킵니다.</span><span class="sxs-lookup"><span data-stu-id="79a50-138">Clear disks to exclude them.</span></span>
10. <span data-ttu-id="79a50-139">**확인**을 클릭하여 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="79a50-139">Click **OK** to save changes.</span></span> <span data-ttu-id="79a50-140">나중에 추가 속성을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79a50-140">You can set additional properties later.</span></span>

    ![복제 활성화](./media/hyper-v-site-walkthrough-enable-replication/enable-replication6-with-exclude-disk.png)

11. <span data-ttu-id="79a50-142">**복제 설정** > **복제 설정 구성**에서 보호되는 VM에 적용할 복제 정책을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="79a50-142">In **Replication settings** > **Configure replication settings**, select the replication policy you want to apply for the protected VMs.</span></span> <span data-ttu-id="79a50-143">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79a50-143">Then click **OK**.</span></span> <span data-ttu-id="79a50-144">**복제 정책** > 정책 이름 > **설정 편집**에서 복제 정책을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79a50-144">You can modify the replication policy in **Replication policies** > policy-name > **Edit Settings**.</span></span> <span data-ttu-id="79a50-145">적용하는 변경 사항은 이미 복제 중인 컴퓨터와 새 컴퓨터에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="79a50-145">Changes you apply will be used for machines that are already replicating, and new machines.</span></span>


   ![복제 활성화](./media/hyper-v-site-walkthrough-enable-replication/enable-replication7.png)

<span data-ttu-id="79a50-147">**작업** > **Site Recovery 작업**에서 **보호 사용** 작업의 진행률을 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79a50-147">You can track progress of the **Enable Protection** job in **Jobs** > **Site Recovery jobs**.</span></span> <span data-ttu-id="79a50-148">**보호 완료** 작업이 실행된 후에는 컴퓨터가 장애 조치(failover)를 수행할 준비가 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79a50-148">After the **Finalize Protection** job runs the machine is ready for failover.</span></span>


## <a name="next-steps"></a><span data-ttu-id="79a50-149">다음 단계</span><span class="sxs-lookup"><span data-stu-id="79a50-149">Next steps</span></span>


<span data-ttu-id="79a50-150">[11단계: 테스트 장애 조치(failover) 실행](hyper-v-site-walkthrough-test-failover.md)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="79a50-150">Go to [Step 11: Run a test failover](hyper-v-site-walkthrough-test-failover.md)</span></span>

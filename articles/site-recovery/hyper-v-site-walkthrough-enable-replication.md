---
title: "Hyper-v Vm (System Center VMM) 없이 Azure Site Recovery와 tooAzure 복제에 대 한 복제 aaaEnable | Microsoft Docs"
description: "Tooenable 복제 tooAzure hello Azure Site Recovery 서비스를 사용 하 여 Hyper-v Vm에 필요한 hello 단계가 요약 되어 있습니다."
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
ms.openlocfilehash: 1589cb7aa1fe954e075cb7bf1f4a4ec199ed3ec7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-enable-replication-for-hyper-v-vms-replicating-tooazure"></a><span data-ttu-id="02e72-103">10 단계: Hyper-v Vm tooAzure 복제에 대 한 복제를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="02e72-103">Step 10: Enable replication for Hyper-V VMs replicating tooAzure</span></span>


<span data-ttu-id="02e72-104">이 문서에서는 방법에 대 한 복제 tooenable 온-프레미스 Hyper-v 가상 컴퓨터 (System Center VMM에서 관리 하지)를 설명 hello를 사용 하 여 tooAzure [Azure Site Recovery](site-recovery-overview.md) hello Azure 포털에서에서 서비스.</span><span class="sxs-lookup"><span data-stu-id="02e72-104">This article describes how tooenable replication for on-premises Hyper-V virtual machines (not managed by System Center VMM) tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="02e72-105">Hello 아래쪽 hello 또는이 문서에 의견과 질문을 게시 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.</span><span class="sxs-lookup"><span data-stu-id="02e72-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>




## <a name="before-you-start"></a><span data-ttu-id="02e72-106">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="02e72-106">Before you start</span></span>

<span data-ttu-id="02e72-107">시작 하기 전에 Azure 사용자 계정에 필요한 hello에 있는지 확인 [권한을](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) 새 가상 컴퓨터 tooAzure의 tooenable 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="02e72-107">Before you start, ensure that your Azure user account has hello required [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replication of a new virtual machine tooAzure.</span></span>

## <a name="exclude-disks-from-replication"></a><span data-ttu-id="02e72-108">복제에서 디스크 제외</span><span class="sxs-lookup"><span data-stu-id="02e72-108">Exclude disks from replication</span></span>

<span data-ttu-id="02e72-109">기본적으로 컴퓨터의 모든 디스크가 복제됩니다.</span><span class="sxs-lookup"><span data-stu-id="02e72-109">By default all disks on a machine are replicated.</span></span> <span data-ttu-id="02e72-110">디스크를 복제에서 제외할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02e72-110">You can exclude disks from replication.</span></span> <span data-ttu-id="02e72-111">예를 들어 임시 데이터, 또는 새로 고쳐지는 데이터 때마다 컴퓨터 tooreplicate 디스크 원하지 않을 수 있습니다 또는 응용 프로그램 (예: pagefile.sys 또는 SQL Server tempdb)를 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="02e72-111">For example you might not want tooreplicate disks with temporary data, or data that's refreshed each time a machine or application restarts (for example pagefile.sys or SQL Server tempdb).</span></span> [<span data-ttu-id="02e72-112">자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="02e72-112">Learn more</span></span>](site-recovery-exclude-disk.md)


## <a name="replicate-vms"></a><span data-ttu-id="02e72-113">VM 복제</span><span class="sxs-lookup"><span data-stu-id="02e72-113">Replicate VMs</span></span>

<span data-ttu-id="02e72-114">다음과 같이 VM에 대해 복제를 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="02e72-114">Enable replication for VMs as follows:</span></span>          

1. <span data-ttu-id="02e72-115">**응용 프로그램 복제** > **원본**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="02e72-115">Click **Replicate application** > **Source**.</span></span> <span data-ttu-id="02e72-116">처음으로 hello에 대 한 복제를 설정한 후 클릭 **복제 +** 추가 컴퓨터에 대 한 tooenable 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="02e72-116">After you've set up replication for hello first time, you can click **+Replicate** tooenable replication for additional machines.</span></span>

    ![복제 활성화](./media/hyper-v-site-walkthrough-enable-replication/enable-replication.png)
2. <span data-ttu-id="02e72-118">**소스**선택, hello 하이퍼-V 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="02e72-118">In **Source**, select hello Hyper-V site.</span></span> <span data-ttu-id="02e72-119">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="02e72-119">Then click **OK**.</span></span>
3. <span data-ttu-id="02e72-120">**대상**hello toouse Azure (기본 또는 리소스 관리)에서 장애 조치 후 원하는 장애 조치 모델을 hello 자격 증명 모음 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="02e72-120">In **Target**, select hello vault subscription, and hello failover model you want toouse in Azure (classic or resource management) after failover.</span></span>
4. <span data-ttu-id="02e72-121">원하는 toouse hello 저장소 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="02e72-121">Select hello storage account you want toouse.</span></span> <span data-ttu-id="02e72-122">Toouse 원하는 계정을 없는 경우 다음을 할 수 있습니다 [만드세요](#set-up-an-azure-storage-account)합니다.</span><span class="sxs-lookup"><span data-stu-id="02e72-122">If you don't have an account you want toouse, you can [create one](#set-up-an-azure-storage-account).</span></span> <span data-ttu-id="02e72-123">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="02e72-123">Then click **OK**.</span></span>
5. <span data-ttu-id="02e72-124">선택 hello Azure 네트워크와 서브넷 toowhich Azure Vm 장애 조치 만들 때 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="02e72-124">Select hello Azure network and subnet toowhich Azure VMs will connect when they're created failover.</span></span>

    - <span data-ttu-id="02e72-125">tooapply hello 네트워크 설정을 tooall 컴퓨터 사용 하도록 설정 하면 복제를 위해 선택 **선택한 컴퓨터에 지금 구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="02e72-125">tooapply hello network settings tooall machines you enable for replication, select **Configure now for selected machines**.</span></span>
    - <span data-ttu-id="02e72-126">선택 **나중에 구성** tooselect hello 컴퓨터당 Azure 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="02e72-126">Select **Configure later** tooselect hello Azure network per machine.</span></span>
    - <span data-ttu-id="02e72-127">Toouse 원하는 네트워크를 설정 하지 않은 경우 다음을 할 수 있습니다 [만드세요](#set-up-an-azure-network)합니다.</span><span class="sxs-lookup"><span data-stu-id="02e72-127">If you don't have a network you want toouse, you can [create one](#set-up-an-azure-network).</span></span> <span data-ttu-id="02e72-128">해당하는 경우 서브넷을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="02e72-128">Select a subnet if applicable.</span></span> <span data-ttu-id="02e72-129">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="02e72-129">Then click **OK**.</span></span>

   ![복제 활성화](./media/hyper-v-site-walkthrough-enable-replication/enable-replication11.png)

6. <span data-ttu-id="02e72-131">**가상 컴퓨터** > **가상 컴퓨터 선택**, 클릭 하 고 tooreplicate 사용할 각 컴퓨터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="02e72-131">In **Virtual Machines** > **Select virtual machines**, click and select each machine you want tooreplicate.</span></span> <span data-ttu-id="02e72-132">복제를 활성화할 수 있는 컴퓨터만 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02e72-132">You can only select machines for which replication can be enabled.</span></span> <span data-ttu-id="02e72-133">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="02e72-133">Then click **OK**.</span></span>

    ![복제 활성화](./media/hyper-v-site-walkthrough-enable-replication/enable-replication5-for-exclude-disk.png)

7. <span data-ttu-id="02e72-135">**속성** > **속성 구성**OS 디스크 hello을 hello 선택한 Vm에 대 한 hello 운영 체제를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="02e72-135">In **Properties** > **Configure properties**, select hello operating system for hello selected VMs, and hello OS disk.</span></span>
8. <span data-ttu-id="02e72-136">해당 hello Azure VM 이름 (대상 이름)을 준수 확인 [Azure 가상 컴퓨터 요구 사항을](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)합니다.</span><span class="sxs-lookup"><span data-stu-id="02e72-136">Verify that hello Azure VM name (target name) complies with [Azure virtual machine requirements](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>
9. <span data-ttu-id="02e72-137">기본적으로 모든 hello 디스크 hello VM의 복제를 위해 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="02e72-137">By default all hello disks of hello VM are selected for replication.</span></span> <span data-ttu-id="02e72-138">일반 디스크 tooexclude 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="02e72-138">Clear disks tooexclude them.</span></span>
10. <span data-ttu-id="02e72-139">클릭 **확인** toosave 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="02e72-139">Click **OK** toosave changes.</span></span> <span data-ttu-id="02e72-140">나중에 추가 속성을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02e72-140">You can set additional properties later.</span></span>

    ![복제 활성화](./media/hyper-v-site-walkthrough-enable-replication/enable-replication6-with-exclude-disk.png)

11. <span data-ttu-id="02e72-142">**복제 설정을** > **복제 설정을 구성**, hello Vm 보호 된 원하는 tooapply hello 복제 정책을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="02e72-142">In **Replication settings** > **Configure replication settings**, select hello replication policy you want tooapply for hello protected VMs.</span></span> <span data-ttu-id="02e72-143">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="02e72-143">Then click **OK**.</span></span> <span data-ttu-id="02e72-144">hello 복제 정책을 수정할 수 있습니다 **복제 정책** > 정책 이름 > **설정 편집**합니다.</span><span class="sxs-lookup"><span data-stu-id="02e72-144">You can modify hello replication policy in **Replication policies** > policy-name > **Edit Settings**.</span></span> <span data-ttu-id="02e72-145">적용하는 변경 사항은 이미 복제 중인 컴퓨터와 새 컴퓨터에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="02e72-145">Changes you apply will be used for machines that are already replicating, and new machines.</span></span>


   ![복제 활성화](./media/hyper-v-site-walkthrough-enable-replication/enable-replication7.png)

<span data-ttu-id="02e72-147">Hello의 진행률을 추적할 수 있습니다 **보호 사용** 작업 **작업** > **사이트 복구 작업이**합니다.</span><span class="sxs-lookup"><span data-stu-id="02e72-147">You can track progress of hello **Enable Protection** job in **Jobs** > **Site Recovery jobs**.</span></span> <span data-ttu-id="02e72-148">Hello 후 **보호 완료** 실행 작업 hello 컴퓨터는 장애 조치에 대해 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="02e72-148">After hello **Finalize Protection** job runs hello machine is ready for failover.</span></span>


## <a name="next-steps"></a><span data-ttu-id="02e72-149">다음 단계</span><span class="sxs-lookup"><span data-stu-id="02e72-149">Next steps</span></span>


<span data-ttu-id="02e72-150">너무 이동[11 단계: 테스트 장애 조치 실행](hyper-v-site-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="02e72-150">Go too[Step 11: Run a test failover](hyper-v-site-walkthrough-test-failover.md)</span></span>

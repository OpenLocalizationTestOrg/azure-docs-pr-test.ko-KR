---
title: "Azure Site Recovery를 사용하여 Azure VM 복제를 위한 테스트 장애 조치 실행 | Microsoft Docs"
description: "Azure Site Recovery 서비스를 사용하여 다른 Azure 지역에 Azure VM을 복제하기 위한 테스트 장애 조치를 실행하는 데 필요한 단계를 요약하고 있습니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: e15c1b0c-5d75-4fdf-acb0-e61def9e9339
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: raynew
ms.openlocfilehash: 8babb0d016729f318442af93596d206c38d91206
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="step-6-run-a-test-failover-for-azure-vm-replication"></a><span data-ttu-id="e137b-103">6단계: Azure VM 복제를 위한 테스트 장애 조치 실행</span><span class="sxs-lookup"><span data-stu-id="e137b-103">Step 6: Run a test failover for Azure VM replication</span></span>

<span data-ttu-id="e137b-104">Azure VM(가상 컴퓨터)에 대한 복제를 활성화한 후에 Azure Portal에서 [Azure Site Recovery](site-recovery-overview.md) 서비스를 사용하여 이 문서의 단계에 따라 한 Azure 지역에서 다른 Azure 지역으로 테스트 장애 조치를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e137b-104">After you've enabled replication for Azure virtual machine (VMs), follow the steps in this article, to run test failover from one Azure region to another, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

- <span data-ttu-id="e137b-105">이 문서를 완료하면 테스트 장애 조치를 통해 하나 이상의 Azure VM에서 보조 Azure 지역으로 장애 조치할 수 있는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e137b-105">When you finish the article, you should have verified with a test failover, that at least one Azure VM can fail over to your secondary Azure region.</span></span> 
- <span data-ttu-id="e137b-106">이 문서의 하단에서 의견을 게시하거나 [Azure Recovery Services 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)에서 질문하세요.</span><span class="sxs-lookup"><span data-stu-id="e137b-106">Post any comments at the bottom of this article, or ask questions in the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span></span>

>[!NOTE]
>
> <span data-ttu-id="e137b-107">Azure VM 복제는 현재 미리 보기로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="e137b-107">Azure VM replication is currently in preview.</span></span>


## <a name="before-you-start"></a><span data-ttu-id="e137b-108">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="e137b-108">Before you start</span></span>

- <span data-ttu-id="e137b-109">테스트 장애 조치를 실행하기 전에 VM 속성을 확인하고 필요한 사항을 변경하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e137b-109">Before you run a test failover, we recommend that you verify the VM properties, and make any changes you need to.</span></span> <span data-ttu-id="e137b-110">**복제 항목**에서 VM 속성에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e137b-110">You can access the VM properties in **Replicated items**.</span></span> <span data-ttu-id="e137b-111">**Essentials** 블레이드는 컴퓨터 설정 및 상태에 대한 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="e137b-111">The **Essentials** blade shows information about machines settings and status.</span></span>
- <span data-ttu-id="e137b-112">프로덕션 장애 조치에 대해 설정된 네트워크(기본 또는 사용자 지정)가 아니라 테스트 장애 조치에 대한 별도의 Azure VM 네트워크를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e137b-112">We recommend you use a separate Azure VM network for the test failover, and not the network (default or customized) that was set up for production failover.</span></span>
- <span data-ttu-id="e137b-113">테스트 장애 조치는 Azure VM(및 해당 저장소)에서 보조 Azure 지역으로 장애 조치하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e137b-113">The test failover fails over Azure VMs (and their storage) to the secondary Azure region.</span></span> <span data-ttu-id="e137b-114">종속된 앱이나 리소스는 복제하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e137b-114">It doesn't replicate any dependent apps or resources.</span></span> <span data-ttu-id="e137b-115">장애 조치된 VM에서 실행되는 앱이 Active Directory 또는 DNS와 같은 다른 리소스에 종속되어 있는 경우 보조 지역에서 아직 사용할 수 없는 앱도 복제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e137b-115">If apps running on failed over VMs are dependent on other resources, such as Active Directory or DNS, you need to replicate these too, if they're not already available in your secondary region.</span></span> [<span data-ttu-id="e137b-116">자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="e137b-116">Learn more</span></span>](site-recovery-test-failover-to-azure.md#prepare-active-directory-and-dns)
- <span data-ttu-id="e137b-117">온-프레미스 사이트에서 장애 조치한 후 복제된 VM에 액세스하려면 이러한 VM에 [연결하도록 준비](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e137b-117">If you want to access replicated VMs after failover from an on-premises site, you need to [prepare to connect](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover) to these VMs.</span></span>

## <a name="run-a-test-failover"></a><span data-ttu-id="e137b-118">테스트 장애 조치(Failover) 실행</span><span class="sxs-lookup"><span data-stu-id="e137b-118">Run a test failover</span></span>

1. <span data-ttu-id="e137b-119">**설정** > **복제된 항목**에서 VM **+테스트 장애 조치** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e137b-119">In **Settings** > **Replicated Items**, click the VM **+Test Failover** icon.</span></span> 

2. <span data-ttu-id="e137b-120">**테스트 장애 조치**에서 장애 조치에 사용할 복구 지점을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e137b-120">In **Test Failover**, Select a recovery point to use for the failover:</span></span>

    - <span data-ttu-id="e137b-121">**가장 최근에 처리됨**: VM을 Site Recovery 서비스에서 처리된 최신 복구 지점으로 장애 조치합니다.</span><span class="sxs-lookup"><span data-stu-id="e137b-121">**Latest processed**: Fails the VM over to the latest recovery point that was processed by the Site Recovery service.</span></span> <span data-ttu-id="e137b-122">타임스탬프가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e137b-122">The time stamp is shown.</span></span> <span data-ttu-id="e137b-123">이 옵션을 사용하면 데이터를 처리하는 데 시간을 소비하지 않으므로 낮은 RTO(복구 시간 목표)가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="e137b-123">With this option, no time is spent processing data, so it provides a low RTO (Recovery Time Objective).</span></span>
    - <span data-ttu-id="e137b-124">**최신 앱 일치**: 모든 VM을 최신 앱 일치 복구 지점으로 장애 조치합니다.</span><span class="sxs-lookup"><span data-stu-id="e137b-124">**Latest app-consistent**: This option fails over all VMs to the latest app-consistent recovery point.</span></span> <span data-ttu-id="e137b-125">타임스탬프가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e137b-125">The time stamp is shown.</span></span> 
    - <span data-ttu-id="e137b-126">**사용자 지정**: 복구 지점을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e137b-126">**Custom**: Select any recovery point.</span></span>
 
3. <span data-ttu-id="e137b-127">장애 조치가 발생한 후에 보조 지역의 Azure VM을 연결할 대상 Azure 가상 네트워크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e137b-127">Select the target Azure virtual network to which Azure VMs in the secondary region will be connected, after the failover occurs.</span></span>
4. <span data-ttu-id="e137b-128">장애 조치를 시작하려면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e137b-128">To start the failover, click **OK**.</span></span> <span data-ttu-id="e137b-129">진행률을 추적하려면 VM을 클릭하여 해당 속성을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e137b-129">To track progress, click the VM to open its properties.</span></span> <span data-ttu-id="e137b-130">또는 자격 증명 모음 이름 > **설정** > **작업** > **Site Recovery 작업**에서 **테스트 장애 조치** 작업을 클릭하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e137b-130">Or, you can click the **Test Failover** job in the vault name > **Settings** > **Jobs** > **Site Recovery jobs**.</span></span>
5. <span data-ttu-id="e137b-131">장애 조치가 완료되면 Azure Portal > **Virtual Machines**에서 Azure VM 복제본이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e137b-131">After the failover finishes, the replica Azure VM appears in the Azure portal > **Virtual Machines**.</span></span> <span data-ttu-id="e137b-132">VM의 크기가 적당하고, 올바른 네트워크에 연결되었고, 실행 중인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e137b-132">Make sure that the VM is the appropriate size, that it's connected to the appropriate network, and that it's running.</span></span>
6. <span data-ttu-id="e137b-133">테스트 장애 조치 중에 만든 VM을 삭제하려면 복제된 항목 또는 복구 계획에서 **테스트 장애 조치 정리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e137b-133">To delete the VMs that were created during the test failover, click **Cleanup test failover** on the replicated item or the recovery plan.</span></span> <span data-ttu-id="e137b-134">**참고**에서 테스트 장애 조치와 관련된 모든 관측 내용을 기록하고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e137b-134">In **Notes**, record and save any observations associated with the test failover.</span></span> 

<span data-ttu-id="e137b-135">테스트 장애 조치(failover)에 대해 [자세히 알아보세요](site-recovery-test-failover-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="e137b-135">[Learn more](site-recovery-test-failover-to-azure.md) about test failovers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e137b-136">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e137b-136">Next steps</span></span>

<span data-ttu-id="e137b-137">장애 조치를 테스트한 후에 이 연습이 완료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e137b-137">After you've tested failover, this walkthrough is complete.</span></span> <span data-ttu-id="e137b-138">이제 프로덕션에서 장애 조치를 실행하는 방법을 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e137b-138">Now, learn about running failovers in production:</span></span>

- <span data-ttu-id="e137b-139">여러 장애 조치 유형 및 장애 조치 실행 방법에 대해 [자세히 알아보세요](site-recovery-failover.md).</span><span class="sxs-lookup"><span data-stu-id="e137b-139">[Learn more](site-recovery-failover.md) about different types of failovers, and how to run them.</span></span>
- <span data-ttu-id="e137b-140">[복구 계획을 사용](site-recovery-create-recovery-plans.md)하여 여러 VM을 장애 조치하는 방법을 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e137b-140">Learn more about failing over multiple VMs [using a recovery plan](site-recovery-create-recovery-plans.md).</span></span>
- <span data-ttu-id="e137b-141">[복구 계획 사용](site-recovery-create-recovery-plans.md)을 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e137b-141">Learn more about [using recovery plans](site-recovery-create-recovery-plans.md).</span></span>
- <span data-ttu-id="e137b-142">장애 조치(failover) 후에 [Azure VM을 다시 보호](site-recovery-how-to-reprotect.md)하는 방법에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="e137b-142">Learn more about [reprotecting Azure  VMs](site-recovery-how-to-reprotect.md) after failover.</span></span>


---
title: "Azure Site Recovery와 Azure VM 복제에 대 한 테스트 장애 조치 aaaRun | Microsoft Docs"
description: "필요한 Azure Vm 복제 tooanother Azure 지역을 사용 하 여 Azure Site Recovery를 hello에 대 한 테스트 장애 조치를 실행 하기 위한 서비스는 hello 단계를 요약 합니다."
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
ms.openlocfilehash: c1f765aa94c59dd70b33317ebbcd04beb7977969
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-run-a-test-failover-for-azure-vm-replication"></a><span data-ttu-id="67d47-103">6단계: Azure VM 복제를 위한 테스트 장애 조치 실행</span><span class="sxs-lookup"><span data-stu-id="67d47-103">Step 6: Run a test failover for Azure VM replication</span></span>

<span data-ttu-id="67d47-104">Azure 가상 컴퓨터 (Vm)에 대 한 복제를 사용 하도록 설정한 후이 문서에서는 Azure 지역 tooanother, hello를 사용 하 여에서 toorun 테스트 장애 조치 hello 단계에 따라 [Azure Site Recovery](site-recovery-overview.md) hello Azure 포털의에서 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="67d47-104">After you've enabled replication for Azure virtual machine (VMs), follow hello steps in this article, toorun test failover from one Azure region tooanother, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

- <span data-ttu-id="67d47-105">Hello 문서를 완료 하면 해야 확인 했습니다 테스트 장애 조치 있는 Azure VM을 하나 이상 tooyour 보조 Azure 지역 조치 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67d47-105">When you finish hello article, you should have verified with a test failover, that at least one Azure VM can fail over tooyour secondary Azure region.</span></span> 
- <span data-ttu-id="67d47-106">이 문서에서는 hello 맨 아래에 대 한 설명을 게시 하거나 hello에서 질문 하기 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span><span class="sxs-lookup"><span data-stu-id="67d47-106">Post any comments at hello bottom of this article, or ask questions in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span></span>

>[!NOTE]
>
> <span data-ttu-id="67d47-107">Azure VM 복제는 현재 미리 보기로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="67d47-107">Azure VM replication is currently in preview.</span></span>


## <a name="before-you-start"></a><span data-ttu-id="67d47-108">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="67d47-108">Before you start</span></span>

- <span data-ttu-id="67d47-109">테스트 장애 조치를 실행 하기 전에 hello VM 속성을 확인 해야 할 변경 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="67d47-109">Before you run a test failover, we recommend that you verify hello VM properties, and make any changes you need to.</span></span> <span data-ttu-id="67d47-110">hello VM 속성에 액세스할 수 있습니다 **복제 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="67d47-110">You can access hello VM properties in **Replicated items**.</span></span> <span data-ttu-id="67d47-111">hello **Essentials** 블레이드 컴퓨터 설정 및 상태에 대 한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="67d47-111">hello **Essentials** blade shows information about machines settings and status.</span></span>
- <span data-ttu-id="67d47-112">Hello 테스트 장애 조치 및 hello 네트워크가 아니라 별도 Azure VM 네트워크를 사용 하는 것이 좋습니다 (기본 또는 사용자 지정) 프로덕션 장애 조치에 대해 설정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="67d47-112">We recommend you use a separate Azure VM network for hello test failover, and not hello network (default or customized) that was set up for production failover.</span></span>
- <span data-ttu-id="67d47-113">hello 테스트 장애 조치 Azure Vm (및 해당 저장소)를 통해 실패 toohello 보조 Azure 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="67d47-113">hello test failover fails over Azure VMs (and their storage) toohello secondary Azure region.</span></span> <span data-ttu-id="67d47-114">종속된 앱이나 리소스는 복제하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="67d47-114">It doesn't replicate any dependent apps or resources.</span></span> <span data-ttu-id="67d47-115">실행 되는 앱 실패 한 Vm을 통해 DNS, Active Directory 등의 다른 리소스에 종속 된 경우 필요한 tooreplicate 이러한도 있지 않는 경우 이미 사용할 수 있는 보조 지역의 합니다.</span><span class="sxs-lookup"><span data-stu-id="67d47-115">If apps running on failed over VMs are dependent on other resources, such as Active Directory or DNS, you need tooreplicate these too, if they're not already available in your secondary region.</span></span> [<span data-ttu-id="67d47-116">자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="67d47-116">Learn more</span></span>](site-recovery-test-failover-to-azure.md#prepare-active-directory-and-dns)
- <span data-ttu-id="67d47-117">너무 필요한 tooaccess 온-프레미스 사이트에서 장애 조치 후 Vm을 복제 하려면[tooconnect 준비](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover) toothese Vm입니다.</span><span class="sxs-lookup"><span data-stu-id="67d47-117">If you want tooaccess replicated VMs after failover from an on-premises site, you need too[prepare tooconnect](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover) toothese VMs.</span></span>

## <a name="run-a-test-failover"></a><span data-ttu-id="67d47-118">테스트 장애 조치(Failover) 실행</span><span class="sxs-lookup"><span data-stu-id="67d47-118">Run a test failover</span></span>

1. <span data-ttu-id="67d47-119">**설정** > **복제 항목**, VM hello 클릭 **+ 테스트 장애 조치** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="67d47-119">In **Settings** > **Replicated Items**, click hello VM **+Test Failover** icon.</span></span> 

2. <span data-ttu-id="67d47-120">**테스트 장애 조치**를 hello 장애 조치에 대 한 복구 지점 toouse 선택:</span><span class="sxs-lookup"><span data-stu-id="67d47-120">In **Test Failover**, Select a recovery point toouse for hello failover:</span></span>

    - <span data-ttu-id="67d47-121">**최신 처리**: 실패 hello Site Recovery 서비스에서 처리 된 toohello 최신 복구 지점을 통해 VM hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="67d47-121">**Latest processed**: Fails hello VM over toohello latest recovery point that was processed by hello Site Recovery service.</span></span> <span data-ttu-id="67d47-122">hello 타임 스탬프가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67d47-122">hello time stamp is shown.</span></span> <span data-ttu-id="67d47-123">이 옵션을 사용하면 데이터를 처리하는 데 시간을 소비하지 않으므로 낮은 RTO(복구 시간 목표)가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="67d47-123">With this option, no time is spent processing data, so it provides a low RTO (Recovery Time Objective).</span></span>
    - <span data-ttu-id="67d47-124">**최신 응용 프로그램에 일관 된**:이 옵션 모든 Vm toohello 최신 응용 프로그램 일치 복구 지점으로 장애 조치 합니다.</span><span class="sxs-lookup"><span data-stu-id="67d47-124">**Latest app-consistent**: This option fails over all VMs toohello latest app-consistent recovery point.</span></span> <span data-ttu-id="67d47-125">hello 타임 스탬프가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67d47-125">hello time stamp is shown.</span></span> 
    - <span data-ttu-id="67d47-126">**사용자 지정**: 복구 지점을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="67d47-126">**Custom**: Select any recovery point.</span></span>
 
3. <span data-ttu-id="67d47-127">Hello 장애 조치가 발생 한 후 선택 hello 대상 Azure 가상 네트워크 toowhich hello 보조 지역에서 Azure Vm 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67d47-127">Select hello target Azure virtual network toowhich Azure VMs in hello secondary region will be connected, after hello failover occurs.</span></span>
4. <span data-ttu-id="67d47-128">toostart hello 장애 조치를 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="67d47-128">toostart hello failover, click **OK**.</span></span> <span data-ttu-id="67d47-129">tootrack 진행 되는 hello VM tooopen 해당 속성을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="67d47-129">tootrack progress, click hello VM tooopen its properties.</span></span> <span data-ttu-id="67d47-130">또는 hello를 클릭할 수 **테스트 장애 조치** hello 자격 증명 모음 이름에는 작업 > **설정** > **작업** > **사이트복구작업**.</span><span class="sxs-lookup"><span data-stu-id="67d47-130">Or, you can click hello **Test Failover** job in hello vault name > **Settings** > **Jobs** > **Site Recovery jobs**.</span></span>
5. <span data-ttu-id="67d47-131">Hello 후 장애 조치 완료 되 면 hello 복제 Azure VM hello Azure 포털에에서 표시 > **가상 컴퓨터**합니다.</span><span class="sxs-lookup"><span data-stu-id="67d47-131">After hello failover finishes, hello replica Azure VM appears in hello Azure portal > **Virtual Machines**.</span></span> <span data-ttu-id="67d47-132">해당 hello VM 실행 되 고 toohello 적절 한 네트워크 연결 된 hello 적절 한 크기 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="67d47-132">Make sure that hello VM is hello appropriate size, that it's connected toohello appropriate network, and that it's running.</span></span>
6. <span data-ttu-id="67d47-133">toodelete hello hello 테스트 장애 조치 중에 만든 Vm 클릭 **테스트 장애 조치 정리** hello에서 항목 또는 hello 복구 계획을 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="67d47-133">toodelete hello VMs that were created during hello test failover, click **Cleanup test failover** on hello replicated item or hello recovery plan.</span></span> <span data-ttu-id="67d47-134">**노트**을 기록 하 고 테스트 장애 조치 hello와 관련 된 모든 관찰을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="67d47-134">In **Notes**, record and save any observations associated with hello test failover.</span></span> 

<span data-ttu-id="67d47-135">테스트 장애 조치(failover)에 대해 [자세히 알아보세요](site-recovery-test-failover-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="67d47-135">[Learn more](site-recovery-test-failover-to-azure.md) about test failovers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="67d47-136">다음 단계</span><span class="sxs-lookup"><span data-stu-id="67d47-136">Next steps</span></span>

<span data-ttu-id="67d47-137">장애 조치를 테스트한 후에 이 연습이 완료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="67d47-137">After you've tested failover, this walkthrough is complete.</span></span> <span data-ttu-id="67d47-138">이제 프로덕션에서 장애 조치를 실행하는 방법을 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="67d47-138">Now, learn about running failovers in production:</span></span>

- <span data-ttu-id="67d47-139">[자세한 내용은](site-recovery-failover.md) 다양 한 유형의 장애 조치에 대 한 방법과 toorun 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="67d47-139">[Learn more](site-recovery-failover.md) about different types of failovers, and how toorun them.</span></span>
- <span data-ttu-id="67d47-140">[복구 계획을 사용](site-recovery-create-recovery-plans.md)하여 여러 VM을 장애 조치하는 방법을 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="67d47-140">Learn more about failing over multiple VMs [using a recovery plan](site-recovery-create-recovery-plans.md).</span></span>
- <span data-ttu-id="67d47-141">[복구 계획 사용](site-recovery-create-recovery-plans.md)을 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="67d47-141">Learn more about [using recovery plans](site-recovery-create-recovery-plans.md).</span></span>
- <span data-ttu-id="67d47-142">장애 조치(failover) 후에 [Azure VM을 다시 보호](site-recovery-how-to-reprotect.md)하는 방법에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="67d47-142">Learn more about [reprotecting Azure  VMs](site-recovery-how-to-reprotect.md) after failover.</span></span>


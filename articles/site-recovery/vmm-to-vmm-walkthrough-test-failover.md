---
title: "Azure 사이트 복구와 Hyper-v VM 복제 tooa 보조 사이트에 대 한 테스트 장애 조치 aaaRun | Microsoft Docs"
description: "어떻게 복제 tooa Hyper-v VM에 대 한 테스트 장애 조치 toorun 보조 System Center VMM 인 사이트를 Azure Site Recovery에 설명 합니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a3fd11ce-65a1-4308-8435-45cf954353ef
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: a60411541c2db001c573735bcb0d651f6618f295
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-run-a-test-failover-for-hyper-v-replication-tooa-secondary-site"></a><span data-ttu-id="1f3a6-103">10 단계: Hyper-v 복제 tooa 보조 사이트에 대 한 테스트 장애 조치 실행</span><span class="sxs-lookup"><span data-stu-id="1f3a6-103">Step 10: Run a test failover for Hyper-V replication tooa secondary site</span></span>


<span data-ttu-id="1f3a6-104">Hyper-v 가상 컴퓨터 (Vm)에 대 한 복제를 사용 하도록 설정한 후 [Azure Site Recovery](site-recovery-overview.md),이 문서 toorun 테스트 장애 조치를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f3a6-104">After you enable replication for Hyper-V virtual machines (VMs) with [Azure Site Recovery](site-recovery-overview.md), use this article toorun a test failover.</span></span> <span data-ttu-id="1f3a6-105">테스트 장애 조치(failover)에서는 복제가 프로덕션 환경에 영향을 주지 않는 상태로 작동하는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1f3a6-105">A test failover verifies that replication is working, without impacting your production environment.</span></span> 


<span data-ttu-id="1f3a6-106">이 문서를 읽은 후 게시 설명을 hello 맨 아래에 하거나 hello에 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.</span><span class="sxs-lookup"><span data-stu-id="1f3a6-106">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="before-you-start"></a><span data-ttu-id="1f3a6-107">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="1f3a6-107">Before you start</span></span>

- <span data-ttu-id="1f3a6-108">테스트 장애 조치를 트리거하는, hello 네트워크 toowhich hello 테스트 복제본 Vm에 연결 됩니다 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f3a6-108">When you're triggering a test failover, you can specify hello network toowhich hello test replica VMs will connect.</span></span> <span data-ttu-id="1f3a6-109">[자세한 내용은](site-recovery-test-failover-vmm-to-vmm.md#network-options-in-site-recovery) hello 네트워크 옵션에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f3a6-109">[Learn more](site-recovery-test-failover-vmm-to-vmm.md#network-options-in-site-recovery) about hello network options.</span></span>
- <span data-ttu-id="1f3a6-110">네트워크 매핑 중 선택한 네트워크는 선택하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1f3a6-110">We recommend that you don't choose a network that you selected during network mapping.</span></span>
- <span data-ttu-id="1f3a6-111">hello이이 문서의 지침에 설명 방법을 통해 단일 VM toofail 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f3a6-111">hello instructions in this article describe how toofail over a single VM.</span></span> <span data-ttu-id="1f3a6-112">에 대 한 읽기 [복구 계획 만들기](site-recovery-create-recovery-plans.md) 하려는 경우 toofail 여러 Vm에 함께 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f3a6-112">Read about [creating recovery plans](site-recovery-create-recovery-plans.md) if you want toofail over multiple VMs together.</span></span>
- <span data-ttu-id="1f3a6-113">또한 [테스트 장애 조치(failover)의 제한 사항](site-recovery-test-failover-vmm-to-vmm.md#things-to-note)도 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="1f3a6-113">Read about [limitations for test failovers](site-recovery-test-failover-vmm-to-vmm.md#things-to-note).</span></span>
- <span data-ttu-id="1f3a6-114">hello 테스트 장애 조치 중 VM tooa 제공 되는 IP 주소는 hello VM hello 동일한 IP 주소 (hello IP 주소는 hello 테스트 장애 조치 네트워크에서 사용할 수 있다고 가정)는 계획 되거나 계획 되지 않은 장애 조치에 대 한 수신 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f3a6-114">hello IP address given tooa VM during test failover is hello same IP address that hello VM would receive for a planned or unplanned failover (presuming that hello IP address is available in hello test failover network).</span></span> <span data-ttu-id="1f3a6-115">Hello IP 주소를 hello 테스트 장애 조치 네트워크에서 사용할 수 없는 경우 VM hello hello 테스트 장애 조치 네트워크에서 사용할 수 있는 다른 IP 주소를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="1f3a6-115">If hello IP address isn't available in hello test failover network, hello VM receives another IP address that is available in hello test failover network.</span></span>
- <span data-ttu-id="1f3a6-116">않도록 하려는 경우 테스트 장애 조치 toodo 프로덕션 네트워크에서는 종단 간 네트워크 연결 컴퓨터의 전체 유효성 검사에 대 한, note입니다.</span><span class="sxs-lookup"><span data-stu-id="1f3a6-116">If you do want toodo a test failover in your production network, for full validatation of end-to-end network connectivity machine, note that:</span></span>
    - <span data-ttu-id="1f3a6-117">hello 주 VM hello 테스트 장애 조치를 수행할 때 종료 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f3a6-117">hello primary VM should be shut down when you're doing hello test failover.</span></span> <span data-ttu-id="1f3a6-118">그렇지 않은 경우 두 Vm이 동일한 id hello에서 실행 될 것 hello로 동일한 네트워크 hello에서 같은 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="1f3a6-118">Otherwise, two VMs with hello same identity will be running in hello same network at hello same time.</span></span> 
    - <span data-ttu-id="1f3a6-119">Tootest Vm 변경 하면 hello 정리 하면 테스트 장애 조치 하는 경우 해당 변경 내용이 손실 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f3a6-119">If you make changes tootest VMs, those changes are lost when you clean up hello test failover.</span></span> <span data-ttu-id="1f3a6-120">이러한 변경 내용은 뒤로 toohello 복제 되지 않습니다 주 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="1f3a6-120">These changes aren't replicated back toohello primary VM.</span></span>
    - <span data-ttu-id="1f3a6-121">테스트는 프로덕션 네트워크 toodowntime 프로덕션 작업에 대 한 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f3a6-121">Testing a a production network leads toodowntime for your production workloads.</span></span> <span data-ttu-id="1f3a6-122">사용자가 toouse 하지 hello 앱 hello 재해 복구 훈련과 진행 중인 경우.</span><span class="sxs-lookup"><span data-stu-id="1f3a6-122">Ask users not toouse hello app when hello disaster recovery drill is in progress.</span></span>  


## <a name="run-a-test-failover-for-a-vm"></a><span data-ttu-id="1f3a6-123">VM에 대해 테스트 장애 조치(failover) 실행</span><span class="sxs-lookup"><span data-stu-id="1f3a6-123">Run a test failover for a VM</span></span>

1. <span data-ttu-id="1f3a6-124">단일 VM 통해 toofail에서 **복제 항목**, hello VM 클릭 > **테스트 장애 조치**합니다.</span><span class="sxs-lookup"><span data-stu-id="1f3a6-124">toofail over a single VM, in **Replicated Items**, click hello VM > **Test Failover**.</span></span>
2. <span data-ttu-id="1f3a6-125">**테스트 장애 조치**, 테스트 Vm 되는 방식이 연결된 toonetworks hello 테스트 장애 조치 후를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f3a6-125">In **Test Failover**, specify how test VMs will be connected toonetworks after hello test failover.</span></span> 
3. <span data-ttu-id="1f3a6-126">클릭 **확인** toobegin hello 장애 조치 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f3a6-126">Click **OK** toobegin hello failover.</span></span> <span data-ttu-id="1f3a6-127">Hello에서 진행률 추적 **작업** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f3a6-127">Track progress on hello **Jobs** tab.</span></span>
5. <span data-ttu-id="1f3a6-128">장애 조치 완료 되 면 해당 hello 테스트 Vm 시작을 성공적으로 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f3a6-128">After failover is complete, verify that hello test VMs start successfully.</span></span>
6. <span data-ttu-id="1f3a6-129">완료 되 면 클릭 **테스트 장애 조치 정리** hello 복구 계획에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f3a6-129">When you're done, click **Cleanup test failover** on hello recovery plan.</span></span>
7. <span data-ttu-id="1f3a6-130">**노트**을 기록 하 고 테스트 장애 조치 hello와 관련 된 모든 관찰을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f3a6-130">In **Notes**, record and save any observations associated with hello test failover.</span></span> <span data-ttu-id="1f3a6-131">이 단계는 hello 가상 컴퓨터와 테스트 장애 조치 중에 생성 된 네트워크를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f3a6-131">This step deletes hello virtual machines and networks that were created during test failover.</span></span>


## <a name="next-steps"></a><span data-ttu-id="1f3a6-132">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1f3a6-132">Next steps</span></span>

<span data-ttu-id="1f3a6-133">Hello 배포를 테스트 한 후에 대 한 자세한 다른 유형의 [장애 조치](site-recovery-failover.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1f3a6-133">After you've tested hello deployment, learn more about other types of [failover](site-recovery-failover.md).</span></span>

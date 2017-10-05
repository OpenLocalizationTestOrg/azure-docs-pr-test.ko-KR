---
title: "Azure Site Recovery를 사용하여 Hyper-V VM을 보조 사이트로 복제하기 위한 테스트 장애 조치(failover) 실행 | Microsoft 문서"
description: "Azure Site Recovery를 사용하여 보조 System Center VMM 사이트로 Hyper-V VM을 복제하기 위해 테스트 장애 조치(failover)를 실행하는 방법을 설명합니다."
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
ms.openlocfilehash: 23d235d326273e7ec59feee6588a39f685401e52
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="step-10-run-a-test-failover-for-hyper-v-replication-to-a-secondary-site"></a><span data-ttu-id="618b5-103">10단계: 보조 사이트로의 Hyper-V 복제를 위한 테스트 장애 조치(failover) 실행</span><span class="sxs-lookup"><span data-stu-id="618b5-103">Step 10: Run a test failover for Hyper-V replication to a secondary site</span></span>


<span data-ttu-id="618b5-104">[Azure Site Recovery](site-recovery-overview.md)를 사용하여 Hyper-V VM(가상 컴퓨터)을 복제하도록 설정한 후 이 문서를 참조하여 테스트 장애 조치(failover)를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="618b5-104">After you enable replication for Hyper-V virtual machines (VMs) with [Azure Site Recovery](site-recovery-overview.md), use this article to run a test failover.</span></span> <span data-ttu-id="618b5-105">테스트 장애 조치(failover)에서는 복제가 프로덕션 환경에 영향을 주지 않는 상태로 작동하는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="618b5-105">A test failover verifies that replication is working, without impacting your production environment.</span></span> 


<span data-ttu-id="618b5-106">이 문서를 읽은 후에 하단 또는 [Azure Recovery Services 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)에서 의견을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="618b5-106">After reading this article, post any comments at the bottom, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="before-you-start"></a><span data-ttu-id="618b5-107">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="618b5-107">Before you start</span></span>

- <span data-ttu-id="618b5-108">테스트 장애 조치(failover)를 트리거할 때는 테스트 복제본 VM이 연결되도록 할 네트워크를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="618b5-108">When you're triggering a test failover, you can specify the network to which the test replica VMs will connect.</span></span> <span data-ttu-id="618b5-109">네트워크 옵션에 대해 자세히 알아보려면 [여기](site-recovery-test-failover-vmm-to-vmm.md#network-options-in-site-recovery)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="618b5-109">[Learn more](site-recovery-test-failover-vmm-to-vmm.md#network-options-in-site-recovery) about the network options.</span></span>
- <span data-ttu-id="618b5-110">네트워크 매핑 중 선택한 네트워크는 선택하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="618b5-110">We recommend that you don't choose a network that you selected during network mapping.</span></span>
- <span data-ttu-id="618b5-111">이 문서의 지침에서는 단일 VM을 장애 조치(failover)하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="618b5-111">The instructions in this article describe how to fail over a single VM.</span></span> <span data-ttu-id="618b5-112">여러 VM을 함께 장애 조치(failover)하려는 경우에는 [복구 계획 만들기](site-recovery-create-recovery-plans.md)를 확인해 보세요.</span><span class="sxs-lookup"><span data-stu-id="618b5-112">Read about [creating recovery plans](site-recovery-create-recovery-plans.md) if you want to fail over multiple VMs together.</span></span>
- <span data-ttu-id="618b5-113">또한 [테스트 장애 조치(failover)의 제한 사항](site-recovery-test-failover-vmm-to-vmm.md#things-to-note)도 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="618b5-113">Read about [limitations for test failovers](site-recovery-test-failover-vmm-to-vmm.md#things-to-note).</span></span>
- <span data-ttu-id="618b5-114">테스트 장애 조치(failover) 중에 VM에 제공된 IP 주소는 이 IP 주소가 테스트 장애 조치(failover) 네트워크에서 사용할 수 있는 경우, VM이 계획되거나 계획되지 않은 장애 조치(failover)에 대해 수신하는 것과 같은 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="618b5-114">The IP address given to a VM during test failover is the same IP address that the VM would receive for a planned or unplanned failover (presuming that the IP address is available in the test failover network).</span></span> <span data-ttu-id="618b5-115">해당 IP 주소를 테스트 장애 조치(failover) 네트워크에서 사용할 수 없는 경우 VM은 테스트 장애 조치(failover) 네트워크에서 사용 가능한 다른 IP 주소를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="618b5-115">If the IP address isn't available in the test failover network, the VM receives another IP address that is available in the test failover network.</span></span>
- <span data-ttu-id="618b5-116">프로덕션 네트워크에서 테스트 장애 조치(failover)를 수행하려는 경우 종단 간 네트워크 연결 컴퓨터의 유효성을 완전하게 검사하려면 다음 사항에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="618b5-116">If you do want to do a test failover in your production network, for full validatation of end-to-end network connectivity machine, note that:</span></span>
    - <span data-ttu-id="618b5-117">테스트 장애 조치(failover)를 수행할 때는 주 VM을 종료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="618b5-117">The primary VM should be shut down when you're doing the test failover.</span></span> <span data-ttu-id="618b5-118">이렇게 하지 않으면 ID가 같은 두 VM이 동시에 동일한 네트워크에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="618b5-118">Otherwise, two VMs with the same identity will be running in the same network at the same time.</span></span> 
    - <span data-ttu-id="618b5-119">테스트 VM을 변경하는 경우 테스트 장애 조치(failover)를 지우면 해당 변경 내용이 손실됩니다.</span><span class="sxs-lookup"><span data-stu-id="618b5-119">If you make changes to test VMs, those changes are lost when you clean up the test failover.</span></span> <span data-ttu-id="618b5-120">즉, 이러한 변경 내용이 기본 VM에 다시 복제되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="618b5-120">These changes aren't replicated back to the primary VM.</span></span>
    - <span data-ttu-id="618b5-121">프로덕션 네트워크를 테스트하면 프로덕션 작업에서 가동 중지 시간이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="618b5-121">Testing a a production network leads to downtime for your production workloads.</span></span> <span data-ttu-id="618b5-122">따라서 재해 복구 연습을 진행 중일 때는 사용자들이 앱을 사용하지 않도록 요청하세요.</span><span class="sxs-lookup"><span data-stu-id="618b5-122">Ask users not to use the app when the disaster recovery drill is in progress.</span></span>  


## <a name="run-a-test-failover-for-a-vm"></a><span data-ttu-id="618b5-123">VM에 대해 테스트 장애 조치(failover) 실행</span><span class="sxs-lookup"><span data-stu-id="618b5-123">Run a test failover for a VM</span></span>

1. <span data-ttu-id="618b5-124">단일 VM을 장애 조치(failover)하려면 **복제된 항목**에서 VM > **테스트 장애 조치(failover)**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="618b5-124">To fail over a single VM, in **Replicated Items**, click the VM > **Test Failover**.</span></span>
2. <span data-ttu-id="618b5-125">**테스트 장애 조치(failover)**에서 테스트 장애 조치(failover) 후에 테스트 VM을 네트워크에 연결할 방법을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="618b5-125">In **Test Failover**, specify how test VMs will be connected to networks after the test failover.</span></span> 
3. <span data-ttu-id="618b5-126">**확인**을 클릭하여 장애 조치(failover)를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="618b5-126">Click **OK** to begin the failover.</span></span> <span data-ttu-id="618b5-127">**작업** 탭에서 진행 상황을 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="618b5-127">Track progress on the **Jobs** tab.</span></span>
5. <span data-ttu-id="618b5-128">장애 조치(failover)가 완료되면 테스트 VM이 정상적으로 시작되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="618b5-128">After failover is complete, verify that the test VMs start successfully.</span></span>
6. <span data-ttu-id="618b5-129">작업이 완료되면 복구 계획에서 **테스트 장애 조치 정리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="618b5-129">When you're done, click **Cleanup test failover** on the recovery plan.</span></span>
7. <span data-ttu-id="618b5-130">**참고**에서 테스트 장애 조치와 관련된 모든 관측 내용을 기록하고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="618b5-130">In **Notes**, record and save any observations associated with the test failover.</span></span> <span data-ttu-id="618b5-131">이 단계는 테스트 장애 조치(failover) 중에 생성된 가상 컴퓨터 및 네트워크를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="618b5-131">This step deletes the virtual machines and networks that were created during test failover.</span></span>


## <a name="next-steps"></a><span data-ttu-id="618b5-132">다음 단계</span><span class="sxs-lookup"><span data-stu-id="618b5-132">Next steps</span></span>

<span data-ttu-id="618b5-133">배포를 테스트한 후 다른 유형의 [장애 조치(failover)](site-recovery-failover.md)에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="618b5-133">After you've tested the deployment, learn more about other types of [failover](site-recovery-failover.md).</span></span>

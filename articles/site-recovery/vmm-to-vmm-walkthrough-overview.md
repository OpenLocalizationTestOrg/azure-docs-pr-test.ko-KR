---
title: "Azure Site Recovery와 aaaReplicate Hyper-v Vm tooa 보조 VMM 사이트 | Microsoft Docs"
description: "Hyper-v Vm tooa 보조 VMM 사이트 hello Azure 포털을 사용 하 여 복제에 대 한 개요를 제공 합니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 476ca82a-8f5c-4498-9dcf-e1011d60ed59
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: raynew
ms.openlocfilehash: 90e44bfc2237dfa7646fb2b7b1e533a7f6d83c50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooa-secondary-vmm-site"></a><span data-ttu-id="1ca02-103">VMM 클라우드 tooa 보조 VMM 사이트에서 Hyper-v 가상 컴퓨터 복제</span><span class="sxs-lookup"><span data-stu-id="1ca02-103">Replicate Hyper-V virtual machines in VMM clouds tooa secondary VMM site</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="1ca02-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="1ca02-104">Azure portal</span></span>](site-recovery-vmm-to-vmm.md)
> * [<span data-ttu-id="1ca02-105">클래식 포털</span><span class="sxs-lookup"><span data-stu-id="1ca02-105">Classic portal</span></span>](site-recovery-vmm-to-vmm-classic.md)
> * [<span data-ttu-id="1ca02-106">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1ca02-106">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

<span data-ttu-id="1ca02-107">이 문서에서는 hello tooreplicate 온-프레미스 보조 VMM 위치 tooa System Center Virtual Machine Manager (VMM) 클라우드에서 관리 되는 Hyper-v 가상 컴퓨터 (Vm)는 데 필요한 단계에 대 한 개요를 사용 하 여 [Azure Site Recovery](site-recovery-overview.md)hello Azure 포털의에서.</span><span class="sxs-lookup"><span data-stu-id="1ca02-107">This article provides an overview of hello steps required tooreplicate on-premises Hyper-V virtual machines (VMs) managed in System Center Virtual Machine Manager (VMM) clouds, tooa secondary VMM location, using [Azure Site Recovery](site-recovery-overview.md) in hello Azure portal.</span></span>

<span data-ttu-id="1ca02-108">이 문서를 읽은 후 게시 설명을 hello 맨 아래에 하거나 hello에 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.</span><span class="sxs-lookup"><span data-stu-id="1ca02-108">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="step-1-review-hello-scenario-architecture"></a><span data-ttu-id="1ca02-109">1 단계: hello 시나리오 아키텍처를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ca02-109">Step 1: Review hello scenario architecture</span></span>

<span data-ttu-id="1ca02-110">배포를 시작 하 고 hello 시나리오 아키텍처를 검토 hello에 대 한 구성 요소를 모두 이해 하기 전에 toodeploy를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ca02-110">Before you start deployment, review hello scenario architecture, and make sure that you understand all hello components you need toodeploy.</span></span>

<span data-ttu-id="1ca02-111">너무 이동[1 단계: hello 아키텍처를 검토](vmm-to-vmm-walkthrough-architecture.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1ca02-111">Go too[Step 1: Review hello architecture](vmm-to-vmm-walkthrough-architecture.md).</span></span>

## <a name="step-2-review-prerequisites-and-limitations"></a><span data-ttu-id="1ca02-112">2단계: 필수 구성 요소 및 제한 사항 검토</span><span class="sxs-lookup"><span data-stu-id="1ca02-112">Step 2: Review prerequisites and limitations</span></span>

<span data-ttu-id="1ca02-113">Hello 배포 필수 구성 요소 및 제한 사항 이해 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ca02-113">Make sure that you understand hello deployment prerequisites and limitations.</span></span>

<span data-ttu-id="1ca02-114">**Azure의 필수 구성 요소**: Azure 복구 서비스 자격 증명 모음 tooorchestrate 하 고 복제를 관리 및 Microsoft Azure 구독이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ca02-114">**Azure prerequisites**: You need a Microsoft Azure subscription, and Azure Recovery Services vault, tooorchestrate and manage replication.</span></span>
<span data-ttu-id="1ca02-115">**온-프레미스 VMM 서버 및 Hyper-V 호스트**: VMM 서버 및 Hyper-V 호스트가 Site Recovery 배포용으로 준비되었으며 배포 규격에 맞는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1ca02-115">**On-premises VMM servers and Hyper-V hosts**: Make sure that VMM servers and Hyper-V hosts are compliant and prepared for Site Recovery deployment.</span></span>

<span data-ttu-id="1ca02-116">너무 이동[2 단계: 사전 요구 사항 및 제한 사항 확인](vmm-to-vmm-walkthrough-prerequisites.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1ca02-116">Go too[Step 2: Verify prerequisites and limitations](vmm-to-vmm-walkthrough-prerequisites.md).</span></span>

## <a name="step-3-plan-networking"></a><span data-ttu-id="1ca02-117">3단계: 네트워킹 계획</span><span class="sxs-lookup"><span data-stu-id="1ca02-117">Step 3: Plan networking</span></span>

<span data-ttu-id="1ca02-118">Toodo 일부 네트워크 tooensure hello 시나리오를 배포할 때 VMM VM 네트워크 간에 네트워크 매핑을 구성할 수 있는지를 계획 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ca02-118">You need toodo some network planning tooensure that you can configure network mapping between VMM VM networks when you deploy hello scenario.</span></span>

<span data-ttu-id="1ca02-119">너무 이동[3 단계: 네트워킹 계획](vmm-to-vmm-walkthrough-network.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1ca02-119">Go too[Step 3: Plan networking](vmm-to-vmm-walkthrough-network.md).</span></span>


## <a name="step-4-prepare-vmm-and-hyper-v"></a><span data-ttu-id="1ca02-120">4단계: VMM 및 Hyper-V 준비</span><span class="sxs-lookup"><span data-stu-id="1ca02-120">Step 4: Prepare VMM and Hyper-V</span></span>

<span data-ttu-id="1ca02-121">사이트 복구 배포에 대 한 hello VMM 서버와 Hyper-v 호스트를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ca02-121">Prepare hello VMM servers and Hyper-V hosts for Site Recovery deployment.</span></span>

<span data-ttu-id="1ca02-122">너무 이동[4 단계: 온-프레미스 서버를 준비](vmm-to-vmm-walkthrough-vmm-hyper-v.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1ca02-122">Go too[Step 4: Prepare on-premises servers](vmm-to-vmm-walkthrough-vmm-hyper-v.md).</span></span>

## <a name="step-5-set-up-a-vault"></a><span data-ttu-id="1ca02-123">5단계: 자격 증명 모음 설정</span><span class="sxs-lookup"><span data-stu-id="1ca02-123">Step 5: Set up a vault</span></span>

<span data-ttu-id="1ca02-124">Recovery Services 자격 증명 모음을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1ca02-124">Set up a Recovery Services vault.</span></span> <span data-ttu-id="1ca02-125">hello 자격 증명 모음 구성 설정을 포함 하 고 복제를 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ca02-125">hello vault contains configuration settings, and orchestrates replication.</span></span>

<span data-ttu-id="1ca02-126">[5단계: 자격 증명 모음 설정](vmm-to-vmm-walkthrough-create-vault.md).</span><span class="sxs-lookup"><span data-stu-id="1ca02-126">[Step 5: Set up a vault](vmm-to-vmm-walkthrough-create-vault.md).</span></span>

## <a name="step-6-set-up-source-and-target-settings"></a><span data-ttu-id="1ca02-127">6단계: 원본 및 대상 설정 지정</span><span class="sxs-lookup"><span data-stu-id="1ca02-127">Step 6: Set up source and target settings</span></span>

<span data-ttu-id="1ca02-128">Hello 원본 및 대상 복제 VMM 위치를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ca02-128">Set up hello source and target replication VMM locations.</span></span> <span data-ttu-id="1ca02-129">Hello VMM 서버 toohello 자격 증명 모음을 추가 하 고 Site Recovery 구성 요소에 대 한 hello 설치 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ca02-129">Add hello VMM servers toohello vault, and download hello installation files for Site Recovery components.</span></span> <span data-ttu-id="1ca02-130">Hello VMM 서버에 Azure Site Recovery Provider 설치 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ca02-130">Run Azure Site Recovery Provider setup on hello VMM server.</span></span> <span data-ttu-id="1ca02-131">설치 프로그램 hello VMM 서버의 hello 공급자를 설치 하 고 hello 서버 hello 자격 증명 모음에 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ca02-131">Setup installs hello Provider on hello VMM server, and registers hello server in hello vault.</span></span> <span data-ttu-id="1ca02-132">각 Hyper-v 호스트에 hello Microsoft 복구 서비스 에이전트를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ca02-132">You install hello Microsoft Recovery Services agent on each Hyper-V host.</span></span>

<span data-ttu-id="1ca02-133">너무 이동[6 단계: 원본 및 대상 설정을 지정 hello](vmm-to-vmm-walkthrough-source-target.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1ca02-133">Go too[Step 6: Set up hello source and target settings](vmm-to-vmm-walkthrough-source-target.md).</span></span>

## <a name="step-7-configure-network-mapping"></a><span data-ttu-id="1ca02-134">7단계: 네트워크 매핑 구성</span><span class="sxs-lookup"><span data-stu-id="1ca02-134">Step 7: Configure network mapping</span></span>

<span data-ttu-id="1ca02-135">Hello 소스 및 대상 위치의 VMM VM 네트워크를 매핑하십시오.</span><span class="sxs-lookup"><span data-stu-id="1ca02-135">Map VMM VM networks in hello source and target locations.</span></span> <span data-ttu-id="1ca02-136">장애 조치 후 Vm은 어떤 hello 원본 Hyper-v VM이 있는 해당 맵을 toohello 원본 VM 네트워크 hello 대상 네트워크에 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ca02-136">After failover, VMs are created in hello target network that maps toohello source VM network in which hello source Hyper-V VM is located.</span></span>

<span data-ttu-id="1ca02-137">너무 이동[7 단계: 네트워크 매핑을 구성](vmm-to-vmm-walkthrough-network-mapping.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1ca02-137">Go too[Step 7: Configure network mapping](vmm-to-vmm-walkthrough-network-mapping.md).</span></span>


## <a name="step-8-set-up-a-replication-policy"></a><span data-ttu-id="1ca02-138">8단계: 복제 정책 설정</span><span class="sxs-lookup"><span data-stu-id="1ca02-138">Step 8: Set up a replication policy</span></span>

<span data-ttu-id="1ca02-139">VMM 위치 간에 VM을 복제할 방법을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1ca02-139">Specify how  VMs will be replicated between VMM locations.</span></span>

<span data-ttu-id="1ca02-140">너무 이동[8 단계: 복제 정책 설정](vmm-to-vmm-walkthrough-replication.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1ca02-140">Go too[Step 8: Set up a replication policy](vmm-to-vmm-walkthrough-replication.md).</span></span>


## <a name="step-9-enable-replication-for-vms"></a><span data-ttu-id="1ca02-141">9단계: VM을 복제하도록 설정</span><span class="sxs-lookup"><span data-stu-id="1ca02-141">Step 9: Enable replication for VMs</span></span>

<span data-ttu-id="1ca02-142">원하는 tooreplicate hello Vm을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ca02-142">Select hello VMs you want tooreplicate.</span></span> <span data-ttu-id="1ca02-143">진행 중인 델타 복제 뒤 복제 트리거 hello 초기 복제 toohello 보조 사이트에 대 한 VM을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ca02-143">Enabling a VM for replication triggers hello initial replication toohello secondary site, followed by ongoing delta replication.</span></span>

<span data-ttu-id="1ca02-144">너무 이동[9 단계: 복제 사용](vmm-to-vmm-walkthrough-enable-replication.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1ca02-144">Go too[Step 9: Enable replication](vmm-to-vmm-walkthrough-enable-replication.md).</span></span>


## <a name="step-10-run-a-test-failover"></a><span data-ttu-id="1ca02-145">10단계: 테스트 장애 조치(failover) 실행</span><span class="sxs-lookup"><span data-stu-id="1ca02-145">Step 10: Run a test failover</span></span>

<span data-ttu-id="1ca02-146">모든 것이 예상 대로 작동 하는지 테스트 장애 조치 toomake를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ca02-146">Run a test failover toomake sure everything's working as expected.</span></span>

<span data-ttu-id="1ca02-147">너무 이동[10 단계: 테스트 장애 조치 실행](vmm-to-vmm-walkthrough-test-failover.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1ca02-147">Go too[Step 10: Run a test failover](vmm-to-vmm-walkthrough-test-failover.md).</span></span>

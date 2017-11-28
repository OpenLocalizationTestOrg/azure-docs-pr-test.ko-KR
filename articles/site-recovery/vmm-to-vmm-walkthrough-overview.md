---
title: "Azure Site Recovery를 사용하여 보조 VMM 사이트에 Hyper-V VM 복제 | Microsoft 문서"
description: "Azure Portal을 사용하여 보조 VMM 사이트에 Hyper-V VM을 복제하는 과정을 대략적으로 설명합니다."
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
ms.openlocfilehash: b422dd2cf23426de2f154a553b38509082536309
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-to-a-secondary-vmm-site"></a><span data-ttu-id="d234d-103">보조 VMM 사이트에 VMM 클라우드의 Hyper-V 가상 컴퓨터 복제</span><span class="sxs-lookup"><span data-stu-id="d234d-103">Replicate Hyper-V virtual machines in VMM clouds to a secondary VMM site</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d234d-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="d234d-104">Azure portal</span></span>](site-recovery-vmm-to-vmm.md)
> * [<span data-ttu-id="d234d-105">클래식 포털</span><span class="sxs-lookup"><span data-stu-id="d234d-105">Classic portal</span></span>](site-recovery-vmm-to-vmm-classic.md)
> * [<span data-ttu-id="d234d-106">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d234d-106">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

<span data-ttu-id="d234d-107">이 문서에서는 Azure Portal에서 [Azure Site Recovery](site-recovery-overview.md)를 사용해 System Center Virtual Machine Manager(VMM) 클라우드에서 관리되는 온-프레미스 Hyper-V VM(가상 컴퓨터)을 보조 VMM 위치로 복제하기 위해 수행해야 하는 단계를 간략하게 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d234d-107">This article provides an overview of the steps required to replicate on-premises Hyper-V virtual machines (VMs) managed in System Center Virtual Machine Manager (VMM) clouds, to a secondary VMM location, using [Azure Site Recovery](site-recovery-overview.md) in the Azure portal.</span></span>

<span data-ttu-id="d234d-108">이 문서를 읽은 후에 하단 또는 [Azure Recovery Services 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)에서 의견을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="d234d-108">After reading this article, post any comments at the bottom, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="step-1-review-the-scenario-architecture"></a><span data-ttu-id="d234d-109">1단계: 시나리오 아키텍처 검토</span><span class="sxs-lookup"><span data-stu-id="d234d-109">Step 1: Review the scenario architecture</span></span>

<span data-ttu-id="d234d-110">배포를 시작하기 전에 시나리오 아키텍처를 검토하고 배포에 필요한 모든 구성 요소를 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d234d-110">Before you start deployment, review the scenario architecture, and make sure that you understand all the components you need to deploy.</span></span>

<span data-ttu-id="d234d-111">[1단계: 아키텍처 검토](vmm-to-vmm-walkthrough-architecture.md)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d234d-111">Go to [Step 1: Review the architecture](vmm-to-vmm-walkthrough-architecture.md).</span></span>

## <a name="step-2-review-prerequisites-and-limitations"></a><span data-ttu-id="d234d-112">2단계: 필수 구성 요소 및 제한 사항 검토</span><span class="sxs-lookup"><span data-stu-id="d234d-112">Step 2: Review prerequisites and limitations</span></span>

<span data-ttu-id="d234d-113">배포 필수 구성 요소 및 제한 사항을 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d234d-113">Make sure that you understand the deployment prerequisites and limitations.</span></span>

<span data-ttu-id="d234d-114">**Azure 필수 구성 요소**: 복제를 오케이스트레이션하고 관리하기 위한 Azure Recovery Services 자격 증명 모음과 Microsoft Azure 구독이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d234d-114">**Azure prerequisites**: You need a Microsoft Azure subscription, and Azure Recovery Services vault, to orchestrate and manage replication.</span></span>
<span data-ttu-id="d234d-115">**온-프레미스 VMM 서버 및 Hyper-V 호스트**: VMM 서버 및 Hyper-V 호스트가 Site Recovery 배포용으로 준비되었으며 배포 규격에 맞는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d234d-115">**On-premises VMM servers and Hyper-V hosts**: Make sure that VMM servers and Hyper-V hosts are compliant and prepared for Site Recovery deployment.</span></span>

<span data-ttu-id="d234d-116">[2단계: 필수 구성 요소 및 제한 사항 확인](vmm-to-vmm-walkthrough-prerequisites.md)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d234d-116">Go to [Step 2: Verify prerequisites and limitations](vmm-to-vmm-walkthrough-prerequisites.md).</span></span>

## <a name="step-3-plan-networking"></a><span data-ttu-id="d234d-117">3단계: 네트워킹 계획</span><span class="sxs-lookup"><span data-stu-id="d234d-117">Step 3: Plan networking</span></span>

<span data-ttu-id="d234d-118">몇 가지 네트워크 계획을 수행하여 시나리오를 배포할 때 VMM VM 네트워크 간에 네트워크 매핑을 구성할 수 있는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d234d-118">You need to do some network planning to ensure that you can configure network mapping between VMM VM networks when you deploy the scenario.</span></span>

<span data-ttu-id="d234d-119">[3단계: 네트워킹 계획](vmm-to-vmm-walkthrough-network.md)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d234d-119">Go to [Step 3: Plan networking](vmm-to-vmm-walkthrough-network.md).</span></span>


## <a name="step-4-prepare-vmm-and-hyper-v"></a><span data-ttu-id="d234d-120">4단계: VMM 및 Hyper-V 준비</span><span class="sxs-lookup"><span data-stu-id="d234d-120">Step 4: Prepare VMM and Hyper-V</span></span>

<span data-ttu-id="d234d-121">Site Recovery 배포용 VMM 서버 및 Hyper-V 호스트를 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="d234d-121">Prepare the VMM servers and Hyper-V hosts for Site Recovery deployment.</span></span>

<span data-ttu-id="d234d-122">[4단계: 온-프레미스 서버 준비](vmm-to-vmm-walkthrough-vmm-hyper-v.md)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d234d-122">Go to [Step 4: Prepare on-premises servers](vmm-to-vmm-walkthrough-vmm-hyper-v.md).</span></span>

## <a name="step-5-set-up-a-vault"></a><span data-ttu-id="d234d-123">5단계: 자격 증명 모음 설정</span><span class="sxs-lookup"><span data-stu-id="d234d-123">Step 5: Set up a vault</span></span>

<span data-ttu-id="d234d-124">Recovery Services 자격 증명 모음을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d234d-124">Set up a Recovery Services vault.</span></span> <span data-ttu-id="d234d-125">자격 증명 모음은 구성 설정을 포함하며 복제를 오케스트레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="d234d-125">The vault contains configuration settings, and orchestrates replication.</span></span>

<span data-ttu-id="d234d-126">[5단계: 자격 증명 모음 설정](vmm-to-vmm-walkthrough-create-vault.md).</span><span class="sxs-lookup"><span data-stu-id="d234d-126">[Step 5: Set up a vault](vmm-to-vmm-walkthrough-create-vault.md).</span></span>

## <a name="step-6-set-up-source-and-target-settings"></a><span data-ttu-id="d234d-127">6단계: 원본 및 대상 설정 지정</span><span class="sxs-lookup"><span data-stu-id="d234d-127">Step 6: Set up source and target settings</span></span>

<span data-ttu-id="d234d-128">원본 및 대상 복제 VMM 위치를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d234d-128">Set up the source and target replication VMM locations.</span></span> <span data-ttu-id="d234d-129">VMM 서버를 자격 증명 모음에 추가하고 Site Recovery 구성 요소의 설치 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="d234d-129">Add the VMM servers to the vault, and download the installation files for Site Recovery components.</span></span> <span data-ttu-id="d234d-130">VMM 서버에서 Azure Site Recovery Provider 설치를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d234d-130">Run Azure Site Recovery Provider setup on the VMM server.</span></span> <span data-ttu-id="d234d-131">설치를 실행하면 VMM 서버에 Azure Site Recovery Provider가 설치되고 자격 증명 모음에 서버가 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="d234d-131">Setup installs the Provider on the VMM server, and registers the server in the vault.</span></span> <span data-ttu-id="d234d-132">각 Hyper-V 호스트에 Microsoft Recovery Services 에이전트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d234d-132">You install the Microsoft Recovery Services agent on each Hyper-V host.</span></span>

<span data-ttu-id="d234d-133">[6단계: 원본 및 대상 설정 지정](vmm-to-vmm-walkthrough-source-target.md)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d234d-133">Go to [Step 6: Set up the source and target settings](vmm-to-vmm-walkthrough-source-target.md).</span></span>

## <a name="step-7-configure-network-mapping"></a><span data-ttu-id="d234d-134">7단계: 네트워크 매핑 구성</span><span class="sxs-lookup"><span data-stu-id="d234d-134">Step 7: Configure network mapping</span></span>

<span data-ttu-id="d234d-135">원본 및 대상 위치에서 VMM VM 네트워크를 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="d234d-135">Map VMM VM networks in the source and target locations.</span></span> <span data-ttu-id="d234d-136">장애 조치(failover) 후에는 원본 Hyper-V VM이 있는 원본 VM 네트워크에 매핑되는 대상 네트워크에 VM이 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="d234d-136">After failover, VMs are created in the target network that maps to the source VM network in which the source Hyper-V VM is located.</span></span>

<span data-ttu-id="d234d-137">[7단계: 네트워크 매핑 구성](vmm-to-vmm-walkthrough-network-mapping.md)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d234d-137">Go to [Step 7: Configure network mapping](vmm-to-vmm-walkthrough-network-mapping.md).</span></span>


## <a name="step-8-set-up-a-replication-policy"></a><span data-ttu-id="d234d-138">8단계: 복제 정책 설정</span><span class="sxs-lookup"><span data-stu-id="d234d-138">Step 8: Set up a replication policy</span></span>

<span data-ttu-id="d234d-139">VMM 위치 간에 VM을 복제할 방법을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d234d-139">Specify how  VMs will be replicated between VMM locations.</span></span>

<span data-ttu-id="d234d-140">[8단계: 복제 정책 설정](vmm-to-vmm-walkthrough-replication.md)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d234d-140">Go to [Step 8: Set up a replication policy](vmm-to-vmm-walkthrough-replication.md).</span></span>


## <a name="step-9-enable-replication-for-vms"></a><span data-ttu-id="d234d-141">9단계: VM을 복제하도록 설정</span><span class="sxs-lookup"><span data-stu-id="d234d-141">Step 9: Enable replication for VMs</span></span>

<span data-ttu-id="d234d-142">복제할 VM을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d234d-142">Select the VMs you want to replicate.</span></span> <span data-ttu-id="d234d-143">VM을 복제할 수 있도록 설정하면 보조 사이트로의 초기 복제가 트리거된 다음 델타 복제가 계속 진행됩니다.</span><span class="sxs-lookup"><span data-stu-id="d234d-143">Enabling a VM for replication triggers the initial replication to the secondary site, followed by ongoing delta replication.</span></span>

<span data-ttu-id="d234d-144">[9단계: 복제 활성화](vmm-to-vmm-walkthrough-enable-replication.md)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d234d-144">Go to [Step 9: Enable replication](vmm-to-vmm-walkthrough-enable-replication.md).</span></span>


## <a name="step-10-run-a-test-failover"></a><span data-ttu-id="d234d-145">10단계: 테스트 장애 조치(failover) 실행</span><span class="sxs-lookup"><span data-stu-id="d234d-145">Step 10: Run a test failover</span></span>

<span data-ttu-id="d234d-146">모든 것이 예상대로 작동하는지 확인할 수 있도록 테스트 장애 조치를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d234d-146">Run a test failover to make sure everything's working as expected.</span></span>

<span data-ttu-id="d234d-147">[10단계: 테스트 장애 조치(failover) 실행](vmm-to-vmm-walkthrough-test-failover.md)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d234d-147">Go to [Step 10: Run a test failover](vmm-to-vmm-walkthrough-test-failover.md).</span></span>

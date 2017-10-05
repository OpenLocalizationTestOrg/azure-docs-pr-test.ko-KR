---
title: "Azure Site Recovery를 사용하여 Azure로 Hyper-V VM 복제 | Microsoft Docs"
description: "온-프레미스 Hyper-V VM을 Azure에 복제, 장애 조치(failover) 및 복구하는 작업을 조정하는 방법 설명"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: efddd986-bc13-4a1d-932d-5484cdc7ad8d
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: da10b213bc2543942b5ac77cf5c5d8547c00220c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-hyper-v-virtual-machines-without-vmm-to-azure"></a><span data-ttu-id="ce1a1-103">Azure로 Hyper-V 가상 컴퓨터(VMM 없음) 복제</span><span class="sxs-lookup"><span data-stu-id="ce1a1-103">Replicate Hyper-V virtual machines (without VMM) to Azure</span></span> 

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ce1a1-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="ce1a1-104">Azure portal</span></span>](site-recovery-hyper-v-site-to-azure.md)
> * [<span data-ttu-id="ce1a1-105">Azure 클래식</span><span class="sxs-lookup"><span data-stu-id="ce1a1-105">Azure classic</span></span>](site-recovery-hyper-v-site-to-azure-classic.md)
> * [<span data-ttu-id="ce1a1-106">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ce1a1-106">PowerShell - Resource Manager</span></span>](site-recovery-deploy-with-powershell-resource-manager.md)
>
>

<span data-ttu-id="ce1a1-107">이 문서에서는 Azure Portal에서 [Azure Site Recovery](site-recovery-overview.md)를 사용하여 Azure로 온-프레미스 Hyper-V 가상 컴퓨터를 복제하는 데 필요한 단계의 개요를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ce1a1-107">This article provides an overview of the steps required to replicate on-premises Hyper-V virtual machines to Azure, using the [Azure Site Recovery](site-recovery-overview.md) in the Azure portal.</span></span> <span data-ttu-id="ce1a1-108">이 배포에서는 Hyper-V VM이 System Center VMM(Virtual Machine Manager)을 통해 관리되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ce1a1-108">In this deployment Hyper-V VMs aren't managed by System Center Virtual Machine Manager (VMM).</span></span>


<span data-ttu-id="ce1a1-109">이 문서를 읽은 후에는 하단에서 의견을 게시하거나 [Azure Recovery Services 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)에서 기술적인 질문을 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce1a1-109">After reading this article, post any comments at the bottom, or ask technical questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="step-1-review-architecture-and-prerequisites"></a><span data-ttu-id="ce1a1-110">1단계: 아키텍처 및 필수 구성 요소 검토</span><span class="sxs-lookup"><span data-stu-id="ce1a1-110">Step 1: Review architecture and prerequisites</span></span>

<span data-ttu-id="ce1a1-111">배포를 시작하기 전에 시나리오 아키텍처를 검토하고 배포에 필요한 모든 구성 요소를 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce1a1-111">Before you start deployment, review the scenario architecture, and make sure you understand all the components you need to deploy</span></span>

<span data-ttu-id="ce1a1-112">[1단계: 아키텍처 검토](hyper-v-site-walkthrough-architecture.md)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ce1a1-112">Go to [Step 1: Review the architecture](hyper-v-site-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="ce1a1-113">2단계: 필수 구성 요소 검토</span><span class="sxs-lookup"><span data-stu-id="ce1a1-113">Step 2: Review prerequisites</span></span>

<span data-ttu-id="ce1a1-114">각 배포 구성 요소에 대한 필수 조건이 준비되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ce1a1-114">Make sure you have the prerequisites in place for each deployment component:</span></span>

- <span data-ttu-id="ce1a1-115">**Azure 필수 구성 요소**: Microsoft Azure 계정, Azure 네트워크 및 저장소 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ce1a1-115">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
- <span data-ttu-id="ce1a1-116">**온-프레미스 Hyper-V 필수 구성 요소**: Hyper-V 호스트가 Site Recovery 배포에 준비되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ce1a1-116">**On-premises Hyper-V prerequisites**: Make sure Hyper-V hosts are prepared for Site Recovery deployment.</span></span>
- <span data-ttu-id="ce1a1-117">**복제된 VM**: 복제할 VM이 Azure 요구 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce1a1-117">**Replicated VMs**: VMs you want to replicate need to comply with Azure requirements.</span></span>

<span data-ttu-id="ce1a1-118">[2단계: 필수 구성 요소 및 제한 사항 확인](hyper-v-site-walkthrough-prerequisites.md)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ce1a1-118">Go to [Step 2: Verify prerequisites and limitations](hyper-v-site-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="ce1a1-119">3단계: 용량 계획</span><span class="sxs-lookup"><span data-stu-id="ce1a1-119">Step 3: Plan capacity</span></span>

<span data-ttu-id="ce1a1-120">전체 배포를 진행하려면 필요한 복제 리소스를 파악해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce1a1-120">If you're doing a full deployment you need to figure out what replication resources you need.</span></span> <span data-ttu-id="ce1a1-121">이 작업을 수행하는 데 도움이 되는 몇 가지 도구를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce1a1-121">There are a couple of tools available to help you do this.</span></span> <span data-ttu-id="ce1a1-122">2단계로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ce1a1-122">Go to Step 2.</span></span> <span data-ttu-id="ce1a1-123">환경을 테스트하는 빠른 설정을 수행하는 경우 이 단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce1a1-123">If you're doing a quick set up to test the environment you can skip this step.</span></span>

<span data-ttu-id="ce1a1-124">[3단계: 용량 계획](hyper-v-site-walkthrough-capacity.md)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ce1a1-124">Go to [Step 3: Plan capacity](hyper-v-site-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="ce1a1-125">4단계: 네트워킹 계획</span><span class="sxs-lookup"><span data-stu-id="ce1a1-125">Step 4: Plan networking</span></span>

<span data-ttu-id="ce1a1-126">장애 조치(failover)가 발생한 후에 Azure VM이 네트워크에 연결되어 있는지 및 IP 주소가 올바른지를 확인하기 위해 일부 네트워크 계획을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce1a1-126">You need to do some network planning to ensure that Azure VMs are connected to networks after failover occurs, and  that that they have the right IP addresses.</span></span>

<span data-ttu-id="ce1a1-127">[4단계: 네트워킹 계획](hyper-v-site-walkthrough-network.md)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ce1a1-127">Go to [Step 4: Plan networking](hyper-v-site-walkthrough-network.md)</span></span>

##  <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="ce1a1-128">5단계: Azure 리소스 준비</span><span class="sxs-lookup"><span data-stu-id="ce1a1-128">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="ce1a1-129">시작하기 전에 Azure 네트워크 및 저장소를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ce1a1-129">Set up Azure networks and storage before you start.</span></span> <span data-ttu-id="ce1a1-130">이 작업은 배포하는 동안에도 수행할 수 있지만 시작하기 전에 수행하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ce1a1-130">You can do this during deployment, but we recommend you do this before you start.</span></span>

<span data-ttu-id="ce1a1-131">[5단계: Azure 준비](hyper-v-site-walkthrough-prepare-azure.md)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ce1a1-131">Go to [Step 5: Prepare Azure](hyper-v-site-walkthrough-prepare-azure.md)</span></span>


## <a name="step-6-prepare-hyper-v"></a><span data-ttu-id="ce1a1-132">6단계: Hyper-V 준비</span><span class="sxs-lookup"><span data-stu-id="ce1a1-132">Step 6: Prepare Hyper-V</span></span>

<span data-ttu-id="ce1a1-133">Hyper-V 서버가 Site Recovery 배포 요구 사항을 충족하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ce1a1-133">Make sure that Hyper-V servers meet Site Recovery deployment requirements.</span></span>

<span data-ttu-id="ce1a1-134">[6단계: Hyper-V 준비](hyper-v-site-walkthrough-prepare-hyper-v.md)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ce1a1-134">Go to [Step 6: Prepare Hyper-V](hyper-v-site-walkthrough-prepare-hyper-v.md)</span></span>

## <a name="step-7-set-up-a-vault"></a><span data-ttu-id="ce1a1-135">7단계: 자격 증명 모음 설정</span><span class="sxs-lookup"><span data-stu-id="ce1a1-135">Step 7: Set up a vault</span></span>

<span data-ttu-id="ce1a1-136">복제를 오케스트레이션하고 관리하도록 Recovery Services 자격 증명 모음을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce1a1-136">You need to set up a Recovery Services vault to orchestrate and manage replication.</span></span> <span data-ttu-id="ce1a1-137">자격 증명 모음을 설정할 때 복제하려는 항목 및 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ce1a1-137">When you set up the vault, you specify what you want to replicate, and where you want to replicate it to.</span></span>

<span data-ttu-id="ce1a1-138">[7단계: 자격 증명 모음 만들기](hyper-v-site-walkthrough-create-vault.md)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ce1a1-138">Go to [Step 7: Create a vault](hyper-v-site-walkthrough-create-vault.md)</span></span>

## <a name="step-8-configure-source-and-target-settings"></a><span data-ttu-id="ce1a1-139">8단계: 원본 및 대상 설정 구성</span><span class="sxs-lookup"><span data-stu-id="ce1a1-139">Step 8: Configure source and target settings</span></span>

<span data-ttu-id="ce1a1-140">복제에 사용되는 원본 및 대상을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ce1a1-140">Set up the source and target that's used for replication.</span></span> <span data-ttu-id="ce1a1-141">원본 설정을 구성하는 것에는 Hyper-V 사이트에 대한 Hyper-V 호스트, 각 Hyper-V 호스트에 Site Recovery 공급자 및 Recovery Services 에이전트 설치 및 Recovery Services 자격 증명 모음에서 사이트 등록이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce1a1-141">Setting up source settings includes adding Hyper-V hosts to a Hyper-V site, installing the Site Recovery Provider and Recovery Services agent on each Hyper-V host, and registering the site in the Recovery Services vault.</span></span>

<span data-ttu-id="ce1a1-142">[8단계: 원본 및 대상 설정](hyper-v-site-walkthrough-source-target.md)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ce1a1-142">Go to [Step 8: Set up the source and target](hyper-v-site-walkthrough-source-target.md)</span></span>

## <a name="step-9-set-up-a-replication-policy"></a><span data-ttu-id="ce1a1-143">9단계: 복제 정책 설정</span><span class="sxs-lookup"><span data-stu-id="ce1a1-143">Step 9: Set up a replication policy</span></span>

<span data-ttu-id="ce1a1-144">자격 증명 모음에서 Hyper-V VM을 위한 복제 설정을 지정하는 정책을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ce1a1-144">You set up a policy to specify replication settings for Hyper-V VMs in the vault.</span></span>

<span data-ttu-id="ce1a1-145">[9단계: 복제 정책 설정](hyper-v-site-walkthrough-replication.md)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ce1a1-145">Go to [Step 9: Set up a replication policy](hyper-v-site-walkthrough-replication.md)</span></span>


## <a name="step-10-enable-replication"></a><span data-ttu-id="ce1a1-146">10단계: 복제 활성화</span><span class="sxs-lookup"><span data-stu-id="ce1a1-146">Step 10: Enable replication</span></span>

<span data-ttu-id="ce1a1-147">복제 정책을 준비한 후, 활성화하면 VM의 초기 복제가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="ce1a1-147">After you have a replication policy in place,  After enabling, initial replication of the VM occurs.</span></span>

<span data-ttu-id="ce1a1-148">[10단계: 복제 활성화](hyper-v-site-walkthrough-enable-replication.md)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ce1a1-148">Go to [Step 10: Enable replication](hyper-v-site-walkthrough-enable-replication.md)</span></span>

## <a name="step-11-run-a-test-failover"></a><span data-ttu-id="ce1a1-149">11단계: 테스트 장애 조치(failover) 실행</span><span class="sxs-lookup"><span data-stu-id="ce1a1-149">Step 11: Run a test failover</span></span>

<span data-ttu-id="ce1a1-150">초기 복제가 완료되고 델타 복제가 실행된 후에 테스트 장애 조치(failover)를 실행하여 예상대로 작동되는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce1a1-150">After initial replication finishes, and delta replication is running, you can run a test failover to make sure everything works as expected.</span></span>

<span data-ttu-id="ce1a1-151">[11단계: 테스트 장애 조치(failover) 실행](hyper-v-site-walkthrough-test-failover.md)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ce1a1-151">Go to [Step 11: Run a test failover](hyper-v-site-walkthrough-test-failover.md)</span></span>

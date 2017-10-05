---
title: "Azure Site Recovery를 사용하여 Azure에 VMware VM 복제 | Microsoft Docs"
description: "VMware VM에서 실행되는 워크로드를 Azure에 복제하는 데 필요한 단계의 개요 제공"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: dab98aa5-9c41-4475-b7dc-2e07ab1cfd18
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: db6f5f95929503e82a529dba26b56af1edb0767f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-vmware-vms-to-azure-with-site-recovery"></a><span data-ttu-id="aff22-103">Site Recovery를 사용하여 Azure에 VMware VM 복제</span><span class="sxs-lookup"><span data-stu-id="aff22-103">Replicate VMware VMs to Azure with Site Recovery</span></span>

<span data-ttu-id="aff22-104">이 문서에서는 Azure Portal에서 [Azure Site Recovery](site-recovery-overview.md) 서비스를 사용하여 온-프레미스 VMware 가상 컴퓨터를 Azure에 복제하는 데 필요한 단계의 개요를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="aff22-104">This article provides an overview of the steps required to replicate on-premises VMware virtual machines to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>


![배포 프로세스](./media/vmware-walkthrough-overview/vmware-to-azure-process.png)

<span data-ttu-id="aff22-106">**그림 1: 배포 프로세스 요약**</span><span class="sxs-lookup"><span data-stu-id="aff22-106">**Figure 1: Deployment process summary**</span></span>

## <a name="step-1-review-architecture-and-prerequisites"></a><span data-ttu-id="aff22-107">1단계: 아키텍처 및 필수 조건 검토</span><span class="sxs-lookup"><span data-stu-id="aff22-107">Step 1: Review architecture and prerequisites</span></span>

<span data-ttu-id="aff22-108">배포를 시작하기 전에 시나리오 아키텍처를 검토하고 배포에 필요한 모든 구성 요소를 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aff22-108">Before you start deployment, review the scenario architecture, and make sure you understand all the components you need to deploy</span></span>

<span data-ttu-id="aff22-109">[1단계: 아키텍처 검토](vmware-walkthrough-architecture.md)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="aff22-109">Go to [Step 1: Review the architecture](vmware-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="aff22-110">2단계: 필수 구성 요소 검토</span><span class="sxs-lookup"><span data-stu-id="aff22-110">Step 2: Review prerequisites</span></span>

<span data-ttu-id="aff22-111">각 배포 구성 요소에 대한 필수 조건이 준비되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="aff22-111">Make sure you have the prerequisites in place for each deployment component:</span></span>

- <span data-ttu-id="aff22-112">**Azure 필수 조건**: Microsoft Azure 계정, Azure 네트워크 및 저장소 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="aff22-112">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
- <span data-ttu-id="aff22-113">**온-프레미스 Site Recovery 구성 요소**: 컴퓨터가 온-프레미스 Site Recovery 구성 요소를 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aff22-113">**On-premises Site Recovery components**: You need a machine running on-premises Site Recovery components.</span></span>
- <span data-ttu-id="aff22-114">**온-프레미스 VMware 필수 조건**: Site Recovery가 VMware 서버 및 VM에 액세스할 수 있도록 계정을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aff22-114">**On-premises VMware prerequisites**: You need to set up accounts so that Site Recovery can access VMware servers and VMs.</span></span>
- <span data-ttu-id="aff22-115">**VM 복제**: 복제하려는 VM이 Azure 요구 사항을 준수하고 모바일 서비스 구성 요소가 설치되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aff22-115">**Replicated VMs**: VMs you want to replicate need to comply with Azure requirements, and have the Mobility service component installed.</span></span>

<span data-ttu-id="aff22-116">[2단계: 필수 조건 및 제한 사항 검토](vmware-walkthrough-prerequisites.md)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="aff22-116">Go to [Step 2: Review prerequisites and limitations](vmware-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="aff22-117">3단계: 용량 계획</span><span class="sxs-lookup"><span data-stu-id="aff22-117">Step 3: Plan capacity</span></span>

<span data-ttu-id="aff22-118">전체 배포를 진행하려면 필요한 복제 리소스를 파악해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aff22-118">If you're doing a full deployment you need to figure out what replication resources you need.</span></span> <span data-ttu-id="aff22-119">이 작업을 수행하는 데 도움이 되는 몇 가지 도구를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aff22-119">There are a couple of tools available to help you do this.</span></span> <span data-ttu-id="aff22-120">2단계로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="aff22-120">Go to Step 2.</span></span> <span data-ttu-id="aff22-121">환경을 테스트하는 빠른 설정을 수행하는 경우 이 단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aff22-121">If you're doing a quick set up to test the environment you can skip this step.</span></span>

<span data-ttu-id="aff22-122">[3단계: 용량 계획](vmware-walkthrough-capacity.md)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="aff22-122">Go to [Step 3: Plan capacity](vmware-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="aff22-123">4단계: 네트워킹 계획</span><span class="sxs-lookup"><span data-stu-id="aff22-123">Step 4: Plan networking</span></span>

<span data-ttu-id="aff22-124">장애 조치(failover)가 발생한 후에 Azure VM이 네트워크에 연결되어 있는지 및 IP 주소가 올바른지를 확인하기 위해 일부 네트워크 계획을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aff22-124">You need to do some network planning to ensure that Azure VMs are connected to networks after failover occurs, and  that that they have the right IP addresses.</span></span>

<span data-ttu-id="aff22-125">[4단계: 네트워킹 계획](vmware-walkthrough-network.md)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="aff22-125">Go to [Step 4: Plan networking](vmware-walkthrough-network.md)</span></span>

##  <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="aff22-126">5단계: Azure 리소스 준비</span><span class="sxs-lookup"><span data-stu-id="aff22-126">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="aff22-127">시작하기 전에 Azure 네트워크 및 저장소를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="aff22-127">Set up Azure networks and storage before you start.</span></span> <span data-ttu-id="aff22-128">이 작업은 배포하는 동안에도 수행할 수 있지만 시작하기 전에 수행하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="aff22-128">You can do this during deployment, but we recommend you do this before you start.</span></span>

<span data-ttu-id="aff22-129">[5단계: Azure 준비](vmware-walkthrough-prepare-azure.md)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="aff22-129">Go to [Step 5: Prepare Azure](vmware-walkthrough-prepare-azure.md)</span></span>


## <a name="step-6-prepare-vmware"></a><span data-ttu-id="aff22-130">6단계: VMware 준비</span><span class="sxs-lookup"><span data-stu-id="aff22-130">Step 6: Prepare VMware</span></span>

<span data-ttu-id="aff22-131">Site Recovery에서 사용할 계정을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aff22-131">You need to set up accounts that Site Recovery will use to:</span></span>

- <span data-ttu-id="aff22-132">VMware 가상화 서버에 액세스하여 자동으로 VM을 감지합니다.</span><span class="sxs-lookup"><span data-stu-id="aff22-132">Access VMware virtualization servers to automatically detect VMs.</span></span>
- <span data-ttu-id="aff22-133">VM에 액세스하여 모바일 서비스를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="aff22-133">Access VMs to install the Mobility service.</span></span> <span data-ttu-id="aff22-134">복제를 활성화하기 전에 복제하려는 VM 각각에 모바일 서비스 에이전트를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aff22-134">Each VM you want to replicate must have the Mobility service agent installed before you can enable replication for it.</span></span>

<span data-ttu-id="aff22-135">[6단계: VMware 준비](vmware-walkthrough-prepare-vmware.md)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="aff22-135">Go to [Step 6: Prepare VMware](vmware-walkthrough-prepare-vmware.md)</span></span>

## <a name="step-7-set-up-a-vault"></a><span data-ttu-id="aff22-136">7단계: 자격 증명 모음 설정</span><span class="sxs-lookup"><span data-stu-id="aff22-136">Step 7: Set up a vault</span></span>

<span data-ttu-id="aff22-137">복제를 오케스트레이션하고 관리하도록 Recovery Services 자격 증명 모음을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aff22-137">You need to set up a Recovery Services vault to orchestrate and manage replication.</span></span> <span data-ttu-id="aff22-138">자격 증명 모음을 설정할 때 복제하려는 항목 및 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="aff22-138">When you set up the vault, you specify what you want to replicate, and where you want to replicate it to.</span></span>

<span data-ttu-id="aff22-139">[7단계: 자격 증명 모음 설정](vmware-walkthrough-create-vault.md)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="aff22-139">Go to [Step 7: Set up a vault](vmware-walkthrough-create-vault.md)</span></span>

## <a name="step-8-configure-source-and-target-settings"></a><span data-ttu-id="aff22-140">8단계: 원본 및 대상 설정 구성</span><span class="sxs-lookup"><span data-stu-id="aff22-140">Step 8: Configure source and target settings</span></span>

<span data-ttu-id="aff22-141">복제에 사용되는 원본 및 대상을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="aff22-141">Set up the source and target that's used for replication.</span></span> <span data-ttu-id="aff22-142">소스 설정을 설정하는 작업에는 온-프레미스 Site Recovery 구성 요소를 설치하는 통합 설정 실행 작업이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="aff22-142">Setting up source settings includes running Unified Setup to install the on-premises Site Recovery components.</span></span>

<span data-ttu-id="aff22-143">[8단계: 원본 및 대상 설정](vmware-walkthrough-source-target.md)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="aff22-143">Go to [Step 8: Set up the source and target](vmware-walkthrough-source-target.md)</span></span>

## <a name="step-9-set-up-a-replication-policy"></a><span data-ttu-id="aff22-144">9단계: 복제 정책 설정</span><span class="sxs-lookup"><span data-stu-id="aff22-144">Step 9: Set up a replication policy</span></span>

<span data-ttu-id="aff22-145">자격 증명 모음에서 VMware VM에 복제 설정을 지정하는 정책을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="aff22-145">You set up a policy to specify replication settings for VMware VMs in the vault.</span></span>

<span data-ttu-id="aff22-146">[9단계: 복제 정책 설정](vmware-walkthrough-replication.md)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="aff22-146">Go to [Step 9: Set up a replication policy](vmware-walkthrough-replication.md)</span></span>

## <a name="step-10-install-the-mobility-service"></a><span data-ttu-id="aff22-147">10단계: 모바일 서비스 설치</span><span class="sxs-lookup"><span data-stu-id="aff22-147">Step 10: Install the Mobility service</span></span>

<span data-ttu-id="aff22-148">복제하려는 각 VM에 모바일 서비스가 설치되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aff22-148">The Mobility service must be installed on each VM you want to replicate.</span></span> <span data-ttu-id="aff22-149">푸시 또는 끌어오기 설치를 사용하여 서비스를 설정하는 방법에는 몇 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aff22-149">There are a few ways to set up the service with push or pull installation.</span></span>

<span data-ttu-id="aff22-150">[10단계: 모바일 서비스 설치](vmware-walkthrough-install-mobility.md)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="aff22-150">Go to [Step 10: Install the Mobility service](vmware-walkthrough-install-mobility.md)</span></span>

## <a name="step-11-enable-replication"></a><span data-ttu-id="aff22-151">11단계: 복제 활성화</span><span class="sxs-lookup"><span data-stu-id="aff22-151">Step 11: Enable replication</span></span>

<span data-ttu-id="aff22-152">VM에서 모바일 서비스를 실행한 후에 복제를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aff22-152">After the Mobility service is running on a VM you can enable replication for it.</span></span> <span data-ttu-id="aff22-153">활성화한 후 VM의 초기 복제가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="aff22-153">After enabling, initial replication of the VM occurs.</span></span>

<span data-ttu-id="aff22-154">[11단계: 복제 활성화](vmware-walkthrough-enable-replication.md)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="aff22-154">Go to [Step 11: Enable replication](vmware-walkthrough-enable-replication.md)</span></span>

## <a name="step-12-run-a-test-failover"></a><span data-ttu-id="aff22-155">12단계: 테스트 장애 조치(Failover) 실행</span><span class="sxs-lookup"><span data-stu-id="aff22-155">Step 12: Run a test failover</span></span>

<span data-ttu-id="aff22-156">초기 복제가 완료되고 델타 복제가 실행된 후에 테스트 장애 조치를 실행하여 예상대로 작동되는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aff22-156">After initial replication finishes, and delta replication is running, you can run a test failover to make sure everything works as expected.</span></span>

<span data-ttu-id="aff22-157">[12단계: 테스트 장애 조치(Failover) 실행](vmware-walkthrough-test-failover.md)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="aff22-157">Go to [Step 12: Run a test failover](vmware-walkthrough-test-failover.md)</span></span>

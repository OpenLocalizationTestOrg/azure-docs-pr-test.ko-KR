---
title: "Azure Site Recovery를 사용하여 VMM 클라우드의 Hyper-V VM을 Azure로 복제 | Microsoft 문서"
description: "이 문서에서는 Azure Site Recovery 서비스를 사용하여 VMM 클라우드의 Hyper-V VM을 Azure로 복제하는 과정을 간략하게 설명합니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: af68d21184c137b2b0f1bb4c1afb9bf507e8332d
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/29/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-to-azure-using-site-recovery-in-the-azure-portal"></a><span data-ttu-id="5fec4-103">Azure Portal에서 Site Recovery를 사용하여 VMM 클라우드의 Hyper-V 가상 컴퓨터를 Azure에 복제</span><span class="sxs-lookup"><span data-stu-id="5fec4-103">Replicate Hyper-V virtual machines in VMM clouds to Azure using Site Recovery in the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5fec4-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="5fec4-104">Azure portal</span></span>](site-recovery-vmm-to-azure.md)
> * [<span data-ttu-id="5fec4-105">Azure 클래식</span><span class="sxs-lookup"><span data-stu-id="5fec4-105">Azure classic</span></span>](site-recovery-vmm-to-azure-classic.md)
> * [<span data-ttu-id="5fec4-106">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5fec4-106">PowerShell Resource Manager</span></span>](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [<span data-ttu-id="5fec4-107">PowerShell 클래식</span><span class="sxs-lookup"><span data-stu-id="5fec4-107">PowerShell classic</span></span>](site-recovery-deploy-with-powershell.md)


<span data-ttu-id="5fec4-108">이 문서에서는 Azure Portal에서 [Azure Site Recovery](site-recovery-overview.md) 서비스를 사용해 System Center Virtual Machine Manager(VMM) 클라우드에서 관리되는 온-프레미스 Hyper-V VM(가상 컴퓨터)을 Azure로 복제하기 위해 수행해야 하는 단계를 간략하게 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="5fec4-108">This article provides an overview of the steps required to replicate on-premises Hyper-V virtual machines (VMs) managed in System Center Virtual Machine Manager (VMM) clouds to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="5fec4-109">이 문서를 읽은 후에 하단 또는 [Azure Recovery Services 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)에서 의견을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="5fec4-109">After reading this article, post any comments at the bottom, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="step-1-review-the-scenario-architecture"></a><span data-ttu-id="5fec4-110">1단계: 시나리오 아키텍처 검토</span><span class="sxs-lookup"><span data-stu-id="5fec4-110">Step 1: Review the scenario architecture</span></span>

<span data-ttu-id="5fec4-111">배포를 시작하기 전에 시나리오 아키텍처를 검토하고 배포에 필요한 모든 구성 요소를 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fec4-111">Before you start deployment, review the scenario architecture, and make sure that you understand all the components you need to deploy.</span></span>

<span data-ttu-id="5fec4-112">[1단계: 아키텍처 검토](vmm-to-azure-walkthrough-architecture.md)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="5fec4-112">Go to [Step 1: Review the architecture](vmm-to-azure-walkthrough-architecture.md)</span></span>

## <a name="step-2-review-prerequisites-and-limitations"></a><span data-ttu-id="5fec4-113">2단계: 필수 구성 요소 및 제한 사항 검토</span><span class="sxs-lookup"><span data-stu-id="5fec4-113">Step 2: Review prerequisites and limitations</span></span>

<span data-ttu-id="5fec4-114">배포 필수 구성 요소 및 제한 사항을 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fec4-114">Make sure that you understand the deployment prerequisites and limitations.</span></span>

<span data-ttu-id="5fec4-115">**Azure 필수 구성 요소**: Microsoft Azure 계정, Azure 네트워크 및 저장소 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5fec4-115">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
<span data-ttu-id="5fec4-116">**온-프레미스 VMM 서버 및 Hyper-V 호스트**: VMM 서버 및 Hyper-V 호스트가 Site Recovery 배포용으로 준비되었으며 배포 규격에 맞는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5fec4-116">**On-premises VMM servers and Hyper-V hosts**: Make sure that VMM servers and Hyper-V hosts are compliant and prepared for Site Recovery deployment.</span></span>
<span data-ttu-id="5fec4-117">**복제된 VM**: 복제할 VM이 Azure 요구 사항을 준수하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5fec4-117">**Replicated VMs**: Check that VMs you want to replicate comply with Azure requirements.</span></span>

<span data-ttu-id="5fec4-118">[2단계: 필수 구성 요소 및 제한 사항 확인](vmm-to-azure-walkthrough-prerequisites.md)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="5fec4-118">Go to [Step 2: Verify prerequisites and limitations](vmm-to-azure-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="5fec4-119">3단계: 용량 계획</span><span class="sxs-lookup"><span data-stu-id="5fec4-119">Step 3: Plan capacity</span></span>

<span data-ttu-id="5fec4-120">전체 배포를 진행하려면 필요한 복제 리소스를 파악해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fec4-120">If you're doing a full deployment, you need to figure out what replication resources you need.</span></span> <span data-ttu-id="5fec4-121">이 작업을 수행하는 데 도움이 되는 몇 가지 도구를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fec4-121">There are a couple of tools available to help you do this.</span></span> <span data-ttu-id="5fec4-122">환경을 테스트하는 빠른 설정을 수행하려면 이 단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fec4-122">If you're doing a quick set up to test the environment, you can skip this step.</span></span>

<span data-ttu-id="5fec4-123">[3단계: 용량 계획](vmm-to-azure-walkthrough-capacity.md)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="5fec4-123">Go to [Step 3: Plan capacity](vmm-to-azure-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="5fec4-124">4단계: 네트워킹 계획</span><span class="sxs-lookup"><span data-stu-id="5fec4-124">Step 4: Plan networking</span></span>

<span data-ttu-id="5fec4-125">시나리오를 배포할 때 네트워크 매핑을 구성할 수 있는지, 장애 조치(failover) 후에 Azure VM이 Azure Virtual Network에 연결되는지, 그리고 Azure VM에 적절한 IP 주소가 할당되는지를 확인하려면 몇 가지 네트워크 계획을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fec4-125">You need to do some network planning to ensure that you can configure network mapping when you deploy the scenario, that Azure VMs will be connected to Azure virtual networks after failover occurs, and that that they're assigned appropriate IP addresses.</span></span>

<span data-ttu-id="5fec4-126">[4단계: 네트워킹 계획](vmm-to-azure-walkthrough-network.md)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="5fec4-126">Go to [Step 4: Plan networking](vmm-to-azure-walkthrough-network.md)</span></span>


## <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="5fec4-127">5단계: Azure 리소스 준비</span><span class="sxs-lookup"><span data-stu-id="5fec4-127">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="5fec4-128">Azure 계정, 네트워크 및 저장소를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5fec4-128">Set up an Azure account, networks, and storage.</span></span> <span data-ttu-id="5fec4-129">이 작업은 배포하는 동안에도 수행할 수 있지만 시작하기 전에 수행하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5fec4-129">You can do this during deployment, but we recommend you do this before you start.</span></span>

<span data-ttu-id="5fec4-130">[5단계: Azure 준비](vmm-to-azure-walkthrough-prepare-azure.md)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="5fec4-130">Go to [Step 5: Prepare Azure](vmm-to-azure-walkthrough-prepare-azure.md)</span></span>

## <a name="step-6-prepare-vmm-and-hyper-v"></a><span data-ttu-id="5fec4-131">6단계: VMM 및 Hyper-V 준비</span><span class="sxs-lookup"><span data-stu-id="5fec4-131">Step 6: Prepare VMM and Hyper-V</span></span>

<span data-ttu-id="5fec4-132">Site Recovery 배포용 온-프레미스 VMM 서버 및 Hyper-V 호스트를 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="5fec4-132">Prepare the on-premises VMM servers and Hyper-V hosts for Site Recovery deployment.</span></span>

<span data-ttu-id="5fec4-133">[6단계: 온-프레미스 서버 준비](vmm-to-azure-walkthrough-vmm-hyper-v.md)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="5fec4-133">Go to [Step 6: Prepare on-premises servers](vmm-to-azure-walkthrough-vmm-hyper-v.md)</span></span>

## <a name="step-7-set-up-a-vault"></a><span data-ttu-id="5fec4-134">7단계: 자격 증명 모음 설정</span><span class="sxs-lookup"><span data-stu-id="5fec4-134">Step 7: Set up a vault</span></span>

<span data-ttu-id="5fec4-135">Recovery Services 자격 증명 모음을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5fec4-135">Set up a Recovery Services vault.</span></span> <span data-ttu-id="5fec4-136">자격 증명 모음은 구성 설정을 포함하며 복제를 오케스트레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="5fec4-136">The vault contains configuration settings, and orchestrates replication.</span></span>

[<span data-ttu-id="5fec4-137">7단계: 자격 증명 모음 설정</span><span class="sxs-lookup"><span data-stu-id="5fec4-137">Step 7: Set up a vault</span></span>](vmm-to-azure-walkthrough-create-vault.md)

## <a name="step-8-configure-source-and-target-settings"></a><span data-ttu-id="5fec4-138">8단계: 원본 및 대상 설정 구성</span><span class="sxs-lookup"><span data-stu-id="5fec4-138">Step 8: Configure source and target settings</span></span>

<span data-ttu-id="5fec4-139">원본 및 대상을 복제 위치를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5fec4-139">Set up the source and target replication locations.</span></span> <span data-ttu-id="5fec4-140">VMM 서버를 자격 증명 모음에 추가하고 Site Recovery 구성 요소의 설치 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="5fec4-140">Add the VMM server to the vault, and download the installation files for Site Recovery components.</span></span> <span data-ttu-id="5fec4-141">VMM 서버에서 Azure Site Recovery Provider 설치를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5fec4-141">Run Azure Site Recovery Provider setup on the VMM server.</span></span> <span data-ttu-id="5fec4-142">설치를 실행하면 VMM 서버에 Azure Site Recovery Provider가 설치되고 자격 증명 모음에 서버가 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="5fec4-142">Setup installs the Provider on the VMM server, and registers the server in the vault.</span></span> <span data-ttu-id="5fec4-143">각 Hyper-V 호스트에 Microsoft Recovery Services 에이전트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="5fec4-143">You install the Microsoft Recovery Services agent on each Hyper-V host.</span></span>

<span data-ttu-id="5fec4-144">[8단계: 원본 및 대상 설정 구성](vmm-to-azure-walkthrough-source-target.md)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="5fec4-144">Go to [Step 8: Configure source and target settings](vmm-to-azure-walkthrough-source-target.md)</span></span>

## <a name="step-9-configure-network-mapping"></a><span data-ttu-id="5fec4-145">9단계: 네트워크 매핑 구성</span><span class="sxs-lookup"><span data-stu-id="5fec4-145">Step 9: Configure network mapping</span></span>

<span data-ttu-id="5fec4-146">온-프레미스 VMM VM 네트워크를 Azure Virtual Network에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="5fec4-146">Map on-premises VMM VM networks to Azure virtual networks.</span></span> <span data-ttu-id="5fec4-147">장애 조치(failover) 후에는 원본 Hyper-V가 있는 온-프레미스 VM 네트워크에 매핑되는 Azure 네트워크에 Azure VM이 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="5fec4-147">After failover, Azure VMs are created in the Azure network that maps to the on-premises VM network in which the source Hyper-V is located.</span></span>

<span data-ttu-id="5fec4-148">[9단계: 네트워크 매핑 구성](vmm-to-azure-walkthrough-network-mapping.md)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="5fec4-148">Go to [Step 9: Configure network mapping](vmm-to-azure-walkthrough-network-mapping.md)</span></span>


## <a name="step-10-set-up-a-replication-policy"></a><span data-ttu-id="5fec4-149">10단계: 복제 정책 설정</span><span class="sxs-lookup"><span data-stu-id="5fec4-149">Step 10: Set up a replication policy</span></span>

<span data-ttu-id="5fec4-150">온-프레미스 VM을 Azure로 복제할 방법을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5fec4-150">Specify how on-premises VMs will be replicated to Azure.</span></span>

<span data-ttu-id="5fec4-151">[10단계: 복제 정책 설정](vmm-to-azure-walkthrough-replication.md)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="5fec4-151">Go to [Step 10: Set up a replication policy](vmm-to-azure-walkthrough-replication.md)</span></span>


## <a name="step-11-enable-replication-for-vms"></a><span data-ttu-id="5fec4-152">11단계: VM을 복제하도록 설정</span><span class="sxs-lookup"><span data-stu-id="5fec4-152">Step 11: Enable replication for VMs</span></span>

<span data-ttu-id="5fec4-153">복제할 VM을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5fec4-153">Select the VMs you want to replicate.</span></span> <span data-ttu-id="5fec4-154">VM을 복제할 수 있도록 설정하면 Azure로의 초기 복제가 트리거된 다음 델타 복제가 계속 진행됩니다.</span><span class="sxs-lookup"><span data-stu-id="5fec4-154">ENabling a VM for replication triggers the initial replication to Azure, followed by ongoing delta replication.</span></span>

<span data-ttu-id="5fec4-155">[11단계: 복제 활성화](vmm-to-azure-walkthrough-enable-replication.md)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="5fec4-155">Go to [Step 11: Enable replication](vmm-to-azure-walkthrough-enable-replication.md)</span></span>


## <a name="step-12-run-a-test-failover"></a><span data-ttu-id="5fec4-156">12단계: 테스트 장애 조치(failover) 실행</span><span class="sxs-lookup"><span data-stu-id="5fec4-156">Step 12: Run a test failover</span></span>

<span data-ttu-id="5fec4-157">모든 것이 예상대로 작동하는지 확인할 수 있도록 테스트 장애 조치를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5fec4-157">Run a test failover to make sure everything's working as expected.</span></span>

<span data-ttu-id="5fec4-158">[12단계: 테스트 장애 조치(failover) 실행](vmm-to-azure-walkthrough-test-failover.md)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="5fec4-158">Go to [Step 12: Run a test failover](vmm-to-azure-walkthrough-test-failover.md)</span></span>



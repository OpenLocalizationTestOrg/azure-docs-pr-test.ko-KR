---
title: "Azure Site Recovery와 aaaReplicate VMware Vm tooAzure | Microsoft Docs"
description: "VMware Vm tooAzure에서 실행 되는 작업을 복제 하기 위한 hello 단계의 개요를 제공 합니다."
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
ms.openlocfilehash: 7104f67a3635b916048dcb61bca770c89f0c77fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-vmware-vms-tooazure-with-site-recovery"></a><span data-ttu-id="f4b80-103">사이트 복구와 VMware Vm tooAzure 복제</span><span class="sxs-lookup"><span data-stu-id="f4b80-103">Replicate VMware VMs tooAzure with Site Recovery</span></span>

<span data-ttu-id="f4b80-104">이 문서에서는 hello 단계 필요한 tooreplicate 온-프레미스 VMware 가상 컴퓨터 tooAzure, hello를 사용 하 여 간략하게 [Azure Site Recovery](site-recovery-overview.md) hello Azure 포털의에서 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="f4b80-104">This article provides an overview of hello steps required tooreplicate on-premises VMware virtual machines tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


![배포 프로세스](./media/vmware-walkthrough-overview/vmware-to-azure-process.png)

<span data-ttu-id="f4b80-106">**그림 1: 배포 프로세스 요약**</span><span class="sxs-lookup"><span data-stu-id="f4b80-106">**Figure 1: Deployment process summary**</span></span>

## <a name="step-1-review-architecture-and-prerequisites"></a><span data-ttu-id="f4b80-107">1단계: 아키텍처 및 필수 구성 요소 검토</span><span class="sxs-lookup"><span data-stu-id="f4b80-107">Step 1: Review architecture and prerequisites</span></span>

<span data-ttu-id="f4b80-108">배포를 시작 하기 전에 hello 시나리오 아키텍처를 검토 하 고 toodeploy 필요한 모든 hello 구성 요소 이해</span><span class="sxs-lookup"><span data-stu-id="f4b80-108">Before you start deployment, review hello scenario architecture, and make sure you understand all hello components you need toodeploy</span></span>

<span data-ttu-id="f4b80-109">너무 이동[1 단계: hello 아키텍처 검토](vmware-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="f4b80-109">Go too[Step 1: Review hello architecture](vmware-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="f4b80-110">2단계: 필수 구성 요소 검토</span><span class="sxs-lookup"><span data-stu-id="f4b80-110">Step 2: Review prerequisites</span></span>

<span data-ttu-id="f4b80-111">Hello 필수 구성 요소에서 각 배포 구성 요소에 대 한 있습니까 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4b80-111">Make sure you have hello prerequisites in place for each deployment component:</span></span>

- <span data-ttu-id="f4b80-112">**Azure 필수 구성 요소**: Microsoft Azure 계정, Azure 네트워크 및 저장소 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f4b80-112">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
- <span data-ttu-id="f4b80-113">**온-프레미스 Site Recovery 구성 요소**: 컴퓨터가 온-프레미스 Site Recovery 구성 요소를 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4b80-113">**On-premises Site Recovery components**: You need a machine running on-premises Site Recovery components.</span></span>
- <span data-ttu-id="f4b80-114">**온-프레미스 VMware 필수 구성 요소**: 계정을 tooset 사이트 복구는 VMware 서버 및 Vm에 액세스할 수 있도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4b80-114">**On-premises VMware prerequisites**: You need tooset up accounts so that Site Recovery can access VMware servers and VMs.</span></span>
- <span data-ttu-id="f4b80-115">**Vm 복제**: Vm Azure 요구 사항에 tooreplicate 필요 toocomply을 hello 모바일 서비스 구성 요소가 설치 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4b80-115">**Replicated VMs**: VMs you want tooreplicate need toocomply with Azure requirements, and have hello Mobility service component installed.</span></span>

<span data-ttu-id="f4b80-116">너무 이동[2 단계: 필수 구성 요소 및 제한 사항 검토](vmware-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="f4b80-116">Go too[Step 2: Review prerequisites and limitations](vmware-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="f4b80-117">3단계: 용량 계획</span><span class="sxs-lookup"><span data-stu-id="f4b80-117">Step 3: Plan capacity</span></span>

<span data-ttu-id="f4b80-118">전체 배포를 수행 하는 경우 필요한 복제 리소스 아웃 toofigure를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4b80-118">If you're doing a full deployment you need toofigure out what replication resources you need.</span></span> <span data-ttu-id="f4b80-119">두 도구 사용 가능한 toohelp의이 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4b80-119">There are a couple of tools available toohelp you do this.</span></span> <span data-ttu-id="f4b80-120">TooStep 2를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4b80-120">Go tooStep 2.</span></span> <span data-ttu-id="f4b80-121">빠른 tootest hello 환경을 설정 하 고이 단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4b80-121">If you're doing a quick set up tootest hello environment you can skip this step.</span></span>

<span data-ttu-id="f4b80-122">너무 이동[3 단계: 용량 계획](vmware-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="f4b80-122">Go too[Step 3: Plan capacity](vmware-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="f4b80-123">4단계: 네트워킹 계획</span><span class="sxs-lookup"><span data-stu-id="f4b80-123">Step 4: Plan networking</span></span>

<span data-ttu-id="f4b80-124">Toodo 일부 네트워크 tooensure 있는지 Azure Vm 연결된 toonetworks 장애 조치가 발생 한 후와 hello 수 있는 올바른 IP 주소를 계획 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4b80-124">You need toodo some network planning tooensure that Azure VMs are connected toonetworks after failover occurs, and  that that they have hello right IP addresses.</span></span>

<span data-ttu-id="f4b80-125">너무 이동[4 단계: 네트워킹 계획](vmware-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="f4b80-125">Go too[Step 4: Plan networking](vmware-walkthrough-network.md)</span></span>

##  <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="f4b80-126">5단계: Azure 리소스 준비</span><span class="sxs-lookup"><span data-stu-id="f4b80-126">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="f4b80-127">시작하기 전에 Azure 네트워크 및 저장소를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f4b80-127">Set up Azure networks and storage before you start.</span></span> <span data-ttu-id="f4b80-128">이 작업은 배포하는 동안에도 수행할 수 있지만 시작하기 전에 수행하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f4b80-128">You can do this during deployment, but we recommend you do this before you start.</span></span>

<span data-ttu-id="f4b80-129">너무 이동[5 단계: Azure 준비](vmware-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="f4b80-129">Go too[Step 5: Prepare Azure](vmware-walkthrough-prepare-azure.md)</span></span>


## <a name="step-6-prepare-vmware"></a><span data-ttu-id="f4b80-130">6단계: VMware 준비</span><span class="sxs-lookup"><span data-stu-id="f4b80-130">Step 6: Prepare VMware</span></span>

<span data-ttu-id="f4b80-131">사이트 복구를 사용 하 여 계정을 tooset이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4b80-131">You need tooset up accounts that Site Recovery will use to:</span></span>

- <span data-ttu-id="f4b80-132">액세스 VMware 가상화 서버 tooautomatically Vm을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4b80-132">Access VMware virtualization servers tooautomatically detect VMs.</span></span>
- <span data-ttu-id="f4b80-133">Vm tooinstall hello 모바일 서비스에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4b80-133">Access VMs tooinstall hello Mobility service.</span></span> <span data-ttu-id="f4b80-134">Tooreplicate hello 모바일 서비스 에이전트가 하기 전에 설치 되어 있어야 합니다. 원하는 각 VM에 대 한 복제를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4b80-134">Each VM you want tooreplicate must have hello Mobility service agent installed before you can enable replication for it.</span></span>

<span data-ttu-id="f4b80-135">너무 이동[6 단계: VMware 준비](vmware-walkthrough-prepare-vmware.md)</span><span class="sxs-lookup"><span data-stu-id="f4b80-135">Go too[Step 6: Prepare VMware](vmware-walkthrough-prepare-vmware.md)</span></span>

## <a name="step-7-set-up-a-vault"></a><span data-ttu-id="f4b80-136">7단계: 자격 증명 모음 설정</span><span class="sxs-lookup"><span data-stu-id="f4b80-136">Step 7: Set up a vault</span></span>

<span data-ttu-id="f4b80-137">복구 서비스 자격 증명 모음 tooorchestrate tooset 필요 하 고 복제를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4b80-137">You need tooset up a Recovery Services vault tooorchestrate and manage replication.</span></span> <span data-ttu-id="f4b80-138">수행할 hello 자격 증명 모음을 설정할 때 지정 tooreplicate, tooreplicate 원본 위치에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4b80-138">When you set up hello vault, you specify what you want tooreplicate, and where you want tooreplicate it to.</span></span>

<span data-ttu-id="f4b80-139">너무 이동[7 단계: 자격 증명 모음 설정](vmware-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="f4b80-139">Go too[Step 7: Set up a vault](vmware-walkthrough-create-vault.md)</span></span>

## <a name="step-8-configure-source-and-target-settings"></a><span data-ttu-id="f4b80-140">8단계: 원본 및 대상 설정 구성</span><span class="sxs-lookup"><span data-stu-id="f4b80-140">Step 8: Configure source and target settings</span></span>

<span data-ttu-id="f4b80-141">Hello 원본 및 복제에 사용 되는 대상을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4b80-141">Set up hello source and target that's used for replication.</span></span> <span data-ttu-id="f4b80-142">소스 설정 될 때까지 설정 통합 설치 tooinstall hello 온-프레미스 복구 사이트 구성 요소를 실행 작업이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4b80-142">Setting up source settings includes running Unified Setup tooinstall hello on-premises Site Recovery components.</span></span>

<span data-ttu-id="f4b80-143">너무 이동[8 단계: hello 소스 및 대상 설정](vmware-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="f4b80-143">Go too[Step 8: Set up hello source and target](vmware-walkthrough-source-target.md)</span></span>

## <a name="step-9-set-up-a-replication-policy"></a><span data-ttu-id="f4b80-144">9단계: 복제 정책 설정</span><span class="sxs-lookup"><span data-stu-id="f4b80-144">Step 9: Set up a replication policy</span></span>

<span data-ttu-id="f4b80-145">설정한 정책 toospecify 복제 설정을 VMware Vm에 대 한 hello 자격 증명 모음에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4b80-145">You set up a policy toospecify replication settings for VMware VMs in hello vault.</span></span>

<span data-ttu-id="f4b80-146">너무 이동[9 단계: 복제 정책 설정](vmware-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="f4b80-146">Go too[Step 9: Set up a replication policy](vmware-walkthrough-replication.md)</span></span>

## <a name="step-10-install-hello-mobility-service"></a><span data-ttu-id="f4b80-147">10 단계: hello 모바일 서비스를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4b80-147">Step 10: Install hello Mobility service</span></span>

<span data-ttu-id="f4b80-148">hello 모바일 서비스를 설치 해야 원하는 tooreplicate 각 VM에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4b80-148">hello Mobility service must be installed on each VM you want tooreplicate.</span></span> <span data-ttu-id="f4b80-149">밀어넣기 또는 끌어오기 설치로 hello 서비스를 몇 가지 방법으로 tooset 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4b80-149">There are a few ways tooset up hello service with push or pull installation.</span></span>

<span data-ttu-id="f4b80-150">너무 이동[10 단계: hello Mobility service 설치](vmware-walkthrough-install-mobility.md)</span><span class="sxs-lookup"><span data-stu-id="f4b80-150">Go too[Step 10: Install hello Mobility service](vmware-walkthrough-install-mobility.md)</span></span>

## <a name="step-11-enable-replication"></a><span data-ttu-id="f4b80-151">11단계: 복제 활성화</span><span class="sxs-lookup"><span data-stu-id="f4b80-151">Step 11: Enable replication</span></span>

<span data-ttu-id="f4b80-152">Hello 모바일 서비스의 VM에서 실행 되 고 복제를 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4b80-152">After hello Mobility service is running on a VM you can enable replication for it.</span></span> <span data-ttu-id="f4b80-153">를 사용 하도록 설정한 후 hello VM의 초기 복제가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="f4b80-153">After enabling, initial replication of hello VM occurs.</span></span>

<span data-ttu-id="f4b80-154">너무 이동[11 단계: 복제 사용](vmware-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="f4b80-154">Go too[Step 11: Enable replication](vmware-walkthrough-enable-replication.md)</span></span>

## <a name="step-12-run-a-test-failover"></a><span data-ttu-id="f4b80-155">12단계: 테스트 장애 조치(failover) 실행</span><span class="sxs-lookup"><span data-stu-id="f4b80-155">Step 12: Run a test failover</span></span>

<span data-ttu-id="f4b80-156">초기 복제가 완료 된 후 델타 복제 실행 되 고 정상적으로 작동 하는지 테스트 장애 조치 toomake를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4b80-156">After initial replication finishes, and delta replication is running, you can run a test failover toomake sure everything works as expected.</span></span>

<span data-ttu-id="f4b80-157">너무 이동[12 단계: 테스트 장애 조치 실행](vmware-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="f4b80-157">Go too[Step 12: Run a test failover](vmware-walkthrough-test-failover.md)</span></span>

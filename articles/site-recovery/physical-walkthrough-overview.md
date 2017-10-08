---
title: "실제 aaaReplicate 온-프레미스 Azure Site Recovery와 서버 tooAzure | Microsoft Docs"
description: "Hello Azure Site Recovery 서비스와 Windows/Linux 물리적 서버의 tooAzure 온-프레미스에서 실행 되는 작업을 복제 하기 위한 hello 단계의 개요를 제공 합니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 20122f01-929a-4675-b85b-a9b99d2618bc
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: f801b9544072d4029ec06cc1abfd4ff370e852e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-physical-servers-tooazure-with-site-recovery"></a><span data-ttu-id="deed4-103">사이트 복구와 실제 서버 tooAzure 복제</span><span class="sxs-lookup"><span data-stu-id="deed4-103">Replicate physical servers tooAzure with Site Recovery</span></span>

<span data-ttu-id="deed4-104">이 문서에서는 hello 단계 필요한 tooreplicate 온-프레미스 Windows/Linux 물리적 서버의 tooAzure, hello를 사용 하 여 간략하게 [Azure Site Recovery](site-recovery-overview.md) hello Azure 포털의에서 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="deed4-104">This article provides an overview of hello steps required tooreplicate on-premises Windows/Linux physical servers tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


## <a name="step-1-review-architecture-and-prerequisites"></a><span data-ttu-id="deed4-105">1단계: 아키텍처 및 필수 구성 요소 검토</span><span class="sxs-lookup"><span data-stu-id="deed4-105">Step 1: Review architecture and prerequisites</span></span>

<span data-ttu-id="deed4-106">배포를 시작 하기 전에 hello 시나리오 아키텍처를 검토 하 고 tooset hello 배포를 필요한 모든 hello 구성 요소를 이해 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="deed4-106">Before you start deployment, review hello scenario architecture, and make sure you understand all hello components you need tooset up hello deployment.</span></span>

<span data-ttu-id="deed4-107">너무 이동[1 단계: hello 아키텍처 검토](physical-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="deed4-107">Go too[Step 1: Review hello architecture](physical-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="deed4-108">2단계: 필수 구성 요소 검토</span><span class="sxs-lookup"><span data-stu-id="deed4-108">Step 2: Review prerequisites</span></span>

<span data-ttu-id="deed4-109">Hello 필수 구성 요소에서 각 배포 구성 요소에 대 한 있습니까 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="deed4-109">Make sure you have hello prerequisites in place for each deployment component:</span></span>

- <span data-ttu-id="deed4-110">**Azure 필수 구성 요소**: Microsoft Azure 계정, Azure 네트워크 및 저장소 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="deed4-110">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
- <span data-ttu-id="deed4-111">**온-프레미스 Site Recovery 구성 요소**: 컴퓨터가 온-프레미스 Site Recovery 구성 요소를 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="deed4-111">**On-premises Site Recovery components**: You need a machine running on-premises Site Recovery components.</span></span>
- <span data-ttu-id="deed4-112">**복제 된 컴퓨터**: tooreplicate 원하는 서버 toocomply 온-프레미스 및 Azure 요구 사항을 적용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="deed4-112">**Replicated machines**: Servers you want tooreplicate need toocomply with on-premises and Azure requirements.</span></span>

<span data-ttu-id="deed4-113">너무 이동[2 단계: 필수 구성 요소 및 제한 사항 검토](physical-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="deed4-113">Go too[Step 2: Review prerequisites and limitations](physical-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="deed4-114">3단계: 용량 계획</span><span class="sxs-lookup"><span data-stu-id="deed4-114">Step 3: Plan capacity</span></span>

<span data-ttu-id="deed4-115">전체 배포를 수행 하는 경우 필요한 복제 리소스 아웃 toofigure를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="deed4-115">If you're doing a full deployment you need toofigure out what replication resources you need.</span></span> <span data-ttu-id="deed4-116">빠른 tootest hello 환경을 설정 하 고,이 단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="deed4-116">If you're doing a quick set up tootest hello environment, you can skip this step.</span></span>

<span data-ttu-id="deed4-117">너무 이동[3 단계: 용량 계획](physical-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="deed4-117">Go too[Step 3: Plan capacity](physical-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="deed4-118">4단계: 네트워킹 계획</span><span class="sxs-lookup"><span data-stu-id="deed4-118">Step 4: Plan networking</span></span>

<span data-ttu-id="deed4-119">Toodo 일부 네트워크 tooensure 있는지 Azure Vm 연결된 toonetworks 장애 조치가 발생 한 후와 hello 수 있는 올바른 IP 주소를 계획 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="deed4-119">You need toodo some network planning tooensure that Azure VMs are connected toonetworks after failover occurs, and  that that they have hello right IP addresses.</span></span>

<span data-ttu-id="deed4-120">너무 이동[4 단계: 네트워킹 계획](physical-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="deed4-120">Go too[Step 4: Plan networking](physical-walkthrough-network.md)</span></span>

##  <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="deed4-121">5단계: Azure 리소스 준비</span><span class="sxs-lookup"><span data-stu-id="deed4-121">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="deed4-122">시작하기 전에 Azure 네트워크 및 저장소를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="deed4-122">Set up Azure networks and storage before you start.</span></span> 

<span data-ttu-id="deed4-123">너무 이동[5 단계: Azure 준비](physical-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="deed4-123">Go too[Step 5: Prepare Azure](physical-walkthrough-prepare-azure.md)</span></span>


## <a name="step-6-set-up-a-vault"></a><span data-ttu-id="deed4-124">6단계: 자격 증명 모음 설정</span><span class="sxs-lookup"><span data-stu-id="deed4-124">Step 6: Set up a vault</span></span>

<span data-ttu-id="deed4-125">복구 서비스 자격 증명 모음 tooorchestrate를 설정 하 고 복제를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="deed4-125">You set up a Recovery Services vault tooorchestrate and manage replication.</span></span> <span data-ttu-id="deed4-126">수행할 hello 자격 증명 모음을 설정할 때 지정 tooreplicate, tooreplicate 원본 위치에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="deed4-126">When you set up hello vault, you specify what you want tooreplicate, and where you want tooreplicate it to.</span></span>

<span data-ttu-id="deed4-127">너무 이동[6 단계: 자격 증명 모음 설정](physical-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="deed4-127">Go too[Step 6: Set up a vault](physical-walkthrough-create-vault.md)</span></span>

## <a name="step-7-configure-source-and-target-settings"></a><span data-ttu-id="deed4-128">7단계: 원본 및 대상 설정 구성</span><span class="sxs-lookup"><span data-stu-id="deed4-128">Step 7: Configure source and target settings</span></span>

<span data-ttu-id="deed4-129">Hello 소스에 대 한 설정을 구성 하 고 대상 (Azure) 사이트로 합니다.</span><span class="sxs-lookup"><span data-stu-id="deed4-129">Configure settings for hello source and target (Azure) site.</span></span> <span data-ttu-id="deed4-130">소스 설정 포함 통합 설치 tooinstall hello 온-프레미스 복구 사이트 구성 요소를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="deed4-130">Source settings includes running Unified Setup tooinstall hello on-premises Site Recovery components.</span></span>

<span data-ttu-id="deed4-131">너무 이동[7 단계: hello 소스 및 대상 설정](physical-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="deed4-131">Go too[Step 7: Set up hello source and target](physical-walkthrough-source-target.md)</span></span>

## <a name="step-8-set-up-a-replication-policy"></a><span data-ttu-id="deed4-132">8단계: 복제 정책 설정</span><span class="sxs-lookup"><span data-stu-id="deed4-132">Step 8: Set up a replication policy</span></span>

<span data-ttu-id="deed4-133">설정한 정책 toospecify 물리적 서버에 복제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="deed4-133">You set up a policy toospecify how physical servers should replicate.</span></span>

<span data-ttu-id="deed4-134">너무 이동[8 단계: 복제 정책 설정](physical-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="deed4-134">Go too[Step 8: Set up a replication policy](physical-walkthrough-replication.md)</span></span>

## <a name="step-9-install-hello-mobility-service"></a><span data-ttu-id="deed4-135">9 단계: hello 모바일 서비스를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="deed4-135">Step 9: Install hello Mobility service</span></span>

<span data-ttu-id="deed4-136">hello 모바일 서비스를 설치 해야 tooreplicate 구성할 각 서버.</span><span class="sxs-lookup"><span data-stu-id="deed4-136">hello Mobility service must be installed on each server you want tooreplicate.</span></span> <span data-ttu-id="deed4-137">밀어넣기 또는 끌어오기 설치로 hello 서비스를 몇 가지 방법으로 tooset 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="deed4-137">There are a few ways tooset up hello service, with push or pull installation.</span></span>

<span data-ttu-id="deed4-138">너무 이동[9 단계: hello Mobility service 설치](physical-walkthrough-install-mobility.md)</span><span class="sxs-lookup"><span data-stu-id="deed4-138">Go too[Step 9: Install hello Mobility service](physical-walkthrough-install-mobility.md)</span></span>

## <a name="step-10-enable-replication"></a><span data-ttu-id="deed4-139">10단계: 복제 활성화</span><span class="sxs-lookup"><span data-stu-id="deed4-139">Step 10: Enable replication</span></span>

<span data-ttu-id="deed4-140">Hello 모바일 서비스를 서버에서 실행 한 후 복제를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="deed4-140">After hello Mobility service is running on a server, you can enable replication for it.</span></span> <span data-ttu-id="deed4-141">를 사용 하도록 설정한 후 hello VM의 초기 복제가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="deed4-141">After enabling, initial replication of hello VM occurs.</span></span>

<span data-ttu-id="deed4-142">너무 이동[10 단계: 복제 사용](physical-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="deed4-142">Go too[Step 10: Enable replication](physical-walkthrough-enable-replication.md)</span></span>

## <a name="step-11-run-a-test-failover"></a><span data-ttu-id="deed4-143">11단계: 테스트 장애 조치(failover) 실행</span><span class="sxs-lookup"><span data-stu-id="deed4-143">Step 11: Run a test failover</span></span>

<span data-ttu-id="deed4-144">초기 복제가 완료 된 후 델타 복제 실행 되 고 정상적으로 작동 하는지 테스트 장애 조치 toomake를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="deed4-144">After initial replication finishes and delta replication is running, you can run a test failover toomake sure everything works as expected.</span></span>

<span data-ttu-id="deed4-145">너무 이동[11 단계: 테스트 장애 조치 실행](physical-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="deed4-145">Go too[Step 11: Run a test failover](physical-walkthrough-test-failover.md)</span></span>


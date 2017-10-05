---
title: "Azure Site Recovery를 사용하여 Azure에 물리적 온-프레미스 서버 복제 | Microsoft Docs"
description: "Azure Site Recovery 서비스를 사용하여 온-프레미스 Windows/Linux 물리적 서버에서 실행되는 워크로드를 Azure에 복제하는 단계에 대한 개요를 제공합니다."
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
ms.openlocfilehash: 0a09b35e98dc0b2f5283c2a707a3a2b8ac9a39f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-physical-servers-to-azure-with-site-recovery"></a><span data-ttu-id="ac7db-103">Site Recovery를 사용하여 Azure에 물리적 서버 복제</span><span class="sxs-lookup"><span data-stu-id="ac7db-103">Replicate physical servers to Azure with Site Recovery</span></span>

<span data-ttu-id="ac7db-104">이 문서에서는 Azure Portal에서 [Azure Site Recovery](site-recovery-overview.md) 서비스를 사용하여 온-프레미스 Windows/Linux 물리적 서버를 Azure에 복제하는 데 필요한 단계의 개요를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7db-104">This article provides an overview of the steps required to replicate on-premises Windows/Linux physical servers to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>


## <a name="step-1-review-architecture-and-prerequisites"></a><span data-ttu-id="ac7db-105">1단계: 아키텍처 및 필수 조건 검토</span><span class="sxs-lookup"><span data-stu-id="ac7db-105">Step 1: Review architecture and prerequisites</span></span>

<span data-ttu-id="ac7db-106">배포를 시작하기 전에 시나리오 아키텍처를 검토하고 배포를 설정하는 데 필요한 모든 구성 요소를 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7db-106">Before you start deployment, review the scenario architecture, and make sure you understand all the components you need to set up the deployment.</span></span>

<span data-ttu-id="ac7db-107">[1단계: 아키텍처 검토](physical-walkthrough-architecture.md)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7db-107">Go to [Step 1: Review the architecture](physical-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="ac7db-108">2단계: 필수 구성 요소 검토</span><span class="sxs-lookup"><span data-stu-id="ac7db-108">Step 2: Review prerequisites</span></span>

<span data-ttu-id="ac7db-109">각 배포 구성 요소에 대한 필수 조건이 준비되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7db-109">Make sure you have the prerequisites in place for each deployment component:</span></span>

- <span data-ttu-id="ac7db-110">**Azure 필수 조건**: Microsoft Azure 계정, Azure 네트워크 및 저장소 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7db-110">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
- <span data-ttu-id="ac7db-111">**온-프레미스 Site Recovery 구성 요소**: 컴퓨터가 온-프레미스 Site Recovery 구성 요소를 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7db-111">**On-premises Site Recovery components**: You need a machine running on-premises Site Recovery components.</span></span>
- <span data-ttu-id="ac7db-112">**복제된 컴퓨터**: 복제하려는 서버는 온-프레미스 및 Azure 요구 사항을 준수 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7db-112">**Replicated machines**: Servers you want to replicate need to comply with on-premises and Azure requirements.</span></span>

<span data-ttu-id="ac7db-113">[2단계: 필수 조건 및 제한 사항 검토](physical-walkthrough-prerequisites.md)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7db-113">Go to [Step 2: Review prerequisites and limitations](physical-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="ac7db-114">3단계: 용량 계획</span><span class="sxs-lookup"><span data-stu-id="ac7db-114">Step 3: Plan capacity</span></span>

<span data-ttu-id="ac7db-115">전체 배포를 진행하려면 필요한 복제 리소스를 파악해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7db-115">If you're doing a full deployment you need to figure out what replication resources you need.</span></span> <span data-ttu-id="ac7db-116">환경을 테스트하는 빠른 설정을 수행하려면 이 단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac7db-116">If you're doing a quick set up to test the environment, you can skip this step.</span></span>

<span data-ttu-id="ac7db-117">[3단계: 용량 계획](physical-walkthrough-capacity.md)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7db-117">Go to [Step 3: Plan capacity](physical-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="ac7db-118">4단계: 네트워킹 계획</span><span class="sxs-lookup"><span data-stu-id="ac7db-118">Step 4: Plan networking</span></span>

<span data-ttu-id="ac7db-119">장애 조치(failover)가 발생한 후에 Azure VM이 네트워크에 연결되어 있는지 및 IP 주소가 올바른지를 확인하기 위해 일부 네트워크 계획을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7db-119">You need to do some network planning to ensure that Azure VMs are connected to networks after failover occurs, and  that that they have the right IP addresses.</span></span>

<span data-ttu-id="ac7db-120">[4단계: 네트워킹 계획](physical-walkthrough-network.md)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7db-120">Go to [Step 4: Plan networking](physical-walkthrough-network.md)</span></span>

##  <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="ac7db-121">5단계: Azure 리소스 준비</span><span class="sxs-lookup"><span data-stu-id="ac7db-121">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="ac7db-122">시작하기 전에 Azure 네트워크 및 저장소를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7db-122">Set up Azure networks and storage before you start.</span></span> 

<span data-ttu-id="ac7db-123">[5단계: Azure 준비](physical-walkthrough-prepare-azure.md)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7db-123">Go to [Step 5: Prepare Azure](physical-walkthrough-prepare-azure.md)</span></span>


## <a name="step-6-set-up-a-vault"></a><span data-ttu-id="ac7db-124">6단계: 자격 증명 모음 설정</span><span class="sxs-lookup"><span data-stu-id="ac7db-124">Step 6: Set up a vault</span></span>

<span data-ttu-id="ac7db-125">복제를 오케스트레이션하고 관리하도록 Recovery Services 자격 증명 모음을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7db-125">You set up a Recovery Services vault to orchestrate and manage replication.</span></span> <span data-ttu-id="ac7db-126">자격 증명 모음을 설정할 때 복제하려는 항목 및 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7db-126">When you set up the vault, you specify what you want to replicate, and where you want to replicate it to.</span></span>

<span data-ttu-id="ac7db-127">[6단계: 자격 증명 모음 설정](physical-walkthrough-create-vault.md)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7db-127">Go to [Step 6: Set up a vault](physical-walkthrough-create-vault.md)</span></span>

## <a name="step-7-configure-source-and-target-settings"></a><span data-ttu-id="ac7db-128">7단계: 원본 및 대상 설정 구성</span><span class="sxs-lookup"><span data-stu-id="ac7db-128">Step 7: Configure source and target settings</span></span>

<span data-ttu-id="ac7db-129">원본 및 대상(Azure) 사이트에 대한 설정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7db-129">Configure settings for the source and target (Azure) site.</span></span> <span data-ttu-id="ac7db-130">원본 설정에는 온-프레미스 Site Recovery 구성 요소를 설치하는 통합 설정 실행 작업이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac7db-130">Source settings includes running Unified Setup to install the on-premises Site Recovery components.</span></span>

<span data-ttu-id="ac7db-131">[7단계: 원본 및 대상 설정](physical-walkthrough-source-target.md)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7db-131">Go to [Step 7: Set up the source and target](physical-walkthrough-source-target.md)</span></span>

## <a name="step-8-set-up-a-replication-policy"></a><span data-ttu-id="ac7db-132">8단계: 복제 정책 설정</span><span class="sxs-lookup"><span data-stu-id="ac7db-132">Step 8: Set up a replication policy</span></span>

<span data-ttu-id="ac7db-133">물리적 서버가 복제되는 방식을 지정하는 정책을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7db-133">You set up a policy to specify how physical servers should replicate.</span></span>

<span data-ttu-id="ac7db-134">[8단계: 복제 정책 설정](physical-walkthrough-replication.md)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7db-134">Go to [Step 8: Set up a replication policy](physical-walkthrough-replication.md)</span></span>

## <a name="step-9-install-the-mobility-service"></a><span data-ttu-id="ac7db-135">9단계: 모바일 서비스 설치</span><span class="sxs-lookup"><span data-stu-id="ac7db-135">Step 9: Install the Mobility service</span></span>

<span data-ttu-id="ac7db-136">복제하려는 각 서버에 모바일 서비스가 설치되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7db-136">The Mobility service must be installed on each server you want to replicate.</span></span> <span data-ttu-id="ac7db-137">푸시 또는 풀 설치를 사용하여 서비스를 설정하는 방법에는 몇 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac7db-137">There are a few ways to set up the service, with push or pull installation.</span></span>

<span data-ttu-id="ac7db-138">[9단계: 모바일 서비스 설치](physical-walkthrough-install-mobility.md)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7db-138">Go to [Step 9: Install the Mobility service](physical-walkthrough-install-mobility.md)</span></span>

## <a name="step-10-enable-replication"></a><span data-ttu-id="ac7db-139">10단계: 복제 활성화</span><span class="sxs-lookup"><span data-stu-id="ac7db-139">Step 10: Enable replication</span></span>

<span data-ttu-id="ac7db-140">서버에서 모바일 서비스를 실행한 후에 복제를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac7db-140">After the Mobility service is running on a server, you can enable replication for it.</span></span> <span data-ttu-id="ac7db-141">활성화한 후 VM의 초기 복제가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac7db-141">After enabling, initial replication of the VM occurs.</span></span>

<span data-ttu-id="ac7db-142">[10단계: 복제 활성화](physical-walkthrough-enable-replication.md)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7db-142">Go to [Step 10: Enable replication](physical-walkthrough-enable-replication.md)</span></span>

## <a name="step-11-run-a-test-failover"></a><span data-ttu-id="ac7db-143">11단계: 테스트 장애 조치(Failover) 실행</span><span class="sxs-lookup"><span data-stu-id="ac7db-143">Step 11: Run a test failover</span></span>

<span data-ttu-id="ac7db-144">초기 복제가 완료되고 델타 복제가 실행된 후에 테스트 장애 조치를 실행하여 모든 항목이 예상대로 작동되는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac7db-144">After initial replication finishes and delta replication is running, you can run a test failover to make sure everything works as expected.</span></span>

<span data-ttu-id="ac7db-145">[11단계: 테스트 장애 조치(Failover) 실행](physical-walkthrough-test-failover.md)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ac7db-145">Go to [Step 11: Run a test failover](physical-walkthrough-test-failover.md)</span></span>


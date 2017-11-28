---
title: "Azure Vm의 Azure 지역 간 복제를 위한 aaaReview hello 아키텍처 | Microsoft Docs"
description: "이 문서에서는 구성 요소와 hello Azure Site Recovery 서비스를 사용 하 여 Azure 지역 간에 Azure Vm을 복제할 때 사용 되는 아키텍처의 개요를 제공 합니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/12/2017
ms.author: raynew
ms.openlocfilehash: 4caab4e7a764040f317201d1345c40c73f836d81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-1-review-hello-architecture-for-azure-vm-replication-between-azure-regions"></a><span data-ttu-id="4d978-103">1 단계: Azure 지역 간 복제 Azure VM에 대 한 hello 아키텍처를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d978-103">Step 1: Review hello architecture for Azure VM replication between Azure regions</span></span>


<span data-ttu-id="4d978-104">Hello를 검토 한 후 [개요 단계](azure-to-azure-walkthrough-overview.md) 이 배포에 대 한 읽기이 문서 toounderstand hello 구성 요소 및 복제 하는 하나의 Azure 지역 tooanother에서 Azure 가상 컴퓨터 (Vm)를 복구 하는 경우 사용 되는 프로세스를 사용 하 여 [Azure 사이트 복구](site-recovery-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4d978-104">After reviewing hello [overview steps](azure-to-azure-walkthrough-overview.md) for this deployment, read this article toounderstand hello components and processes used when replicating and recovering Azure virtual machines (VMs) from one Azure region tooanother, using [Azure Site Recovery](site-recovery-overview.md).</span></span>

- <span data-ttu-id="4d978-105">Hello 문서를 완료 하면 Azure VM 복제 tooanother 지역의 작동 방식을 명확히 이해가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d978-105">When you finish hello article, you should have a clear understanding of how Azure VM replication tooanother region works.</span></span>
- <span data-ttu-id="4d978-106">이 문서에서는 hello 맨 아래에 대 한 설명을 게시 하거나 hello에서 질문 하기 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.</span><span class="sxs-lookup"><span data-stu-id="4d978-106">Post any comments at hello bottom of this article, or ask questions in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

>[!NOTE]
><span data-ttu-id="4d978-107">Azure VM 복제 hello Site Recovery 서비스를 현재 미리 보기 중입니다.</span><span class="sxs-lookup"><span data-stu-id="4d978-107">Azure VM replication with hello Site Recovery service is currently in preview.</span></span>



## <a name="architectural-components"></a><span data-ttu-id="4d978-108">아키텍처 구성 요소</span><span class="sxs-lookup"><span data-stu-id="4d978-108">Architectural components</span></span>

<span data-ttu-id="4d978-109">hello 다음 다이어그램은 높은 수준의 (이 예에서는 hello 미국 동부 위치)에 특정 지역에서 Azure VM 환경 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d978-109">hello following diagram provides a high-level view of an Azure VM environment in a specific region (in this example, hello East US location).</span></span> <span data-ttu-id="4d978-110">Azure VM 환경은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4d978-110">In an Azure VM environment:</span></span>
- <span data-ttu-id="4d978-111">앱은 여러 저장소 계정에 디스크가 분산되어 있는 VM에서 실행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d978-111">Apps can be running on VMs with disks spread across storage accounts.</span></span>
- <span data-ttu-id="4d978-112">hello Vm 가상 네트워크 내에서 하나 이상의 서브넷에 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d978-112">hello VMs can be included in one or more subnets within a virtual network.</span></span>

![고객 환경](./media/azure-to-azure-walkthrough-architecture/source-environment.png)

## <a name="replication-process"></a><span data-ttu-id="4d978-114">복제 프로세스</span><span class="sxs-lookup"><span data-stu-id="4d978-114">Replication process</span></span>

### <a name="step-1"></a><span data-ttu-id="4d978-115">1단계</span><span class="sxs-lookup"><span data-stu-id="4d978-115">Step 1</span></span>

<span data-ttu-id="4d978-116">Hello Azure 포털에서에서 Azure VM 복제를 사용 하도록 설정 하면 hello 리소스 hello 뒤에 표시 된 다이어그램과 테이블에 자동으로 hello 대상 지역에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="4d978-116">When you enable Azure VM replication in hello Azure portal, hello resources shown in hello following diagram and table are automatically created in hello target region.</span></span> <span data-ttu-id="4d978-117">기본적으로 리소스는 원본 지역 설정을 기반으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="4d978-117">By default, resources are created based on source region settings.</span></span> <span data-ttu-id="4d978-118">필요에 따라 hello 대상 설정을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d978-118">You can customize hello target settings as required.</span></span> <span data-ttu-id="4d978-119">[자세히 알아봅니다](site-recovery-replicate-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="4d978-119">[Learn more](site-recovery-replicate-azure-to-azure.md).</span></span>

![복제를 사용하도록 설정하는 프로세스, 1단계](./media/azure-to-azure-walkthrough-architecture/enable-replication-step-1.png)

<span data-ttu-id="4d978-121">**리소스**</span><span class="sxs-lookup"><span data-stu-id="4d978-121">**Resource**</span></span> | <span data-ttu-id="4d978-122">**세부 정보**</span><span class="sxs-lookup"><span data-stu-id="4d978-122">**Details**</span></span>
--- | ---
<span data-ttu-id="4d978-123">**대상 리소스 그룹**</span><span class="sxs-lookup"><span data-stu-id="4d978-123">**Target resource group**</span></span> | <span data-ttu-id="4d978-124">복제 된 Vm 장애 조치 후 속한 리소스 그룹 toowhich를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d978-124">hello resource group toowhich replicated VMs belong after failover.</span></span>
<span data-ttu-id="4d978-125">**대상 가상 네트워크**</span><span class="sxs-lookup"><span data-stu-id="4d978-125">**Target virtual network**</span></span> | <span data-ttu-id="4d978-126">복제 된 Vm이 있는 장애 조치 후 가상 네트워크를 hello입니다.</span><span class="sxs-lookup"><span data-stu-id="4d978-126">hello virtual network in which replicated VMs are located after failover.</span></span> <span data-ttu-id="4d978-127">네트워크 매핑은 원본 및 대상 가상 네트워크 간에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="4d978-127">A network mapping is created between source and target virtual networks, and vice versa.</span></span>
<span data-ttu-id="4d978-128">**캐시 저장소 계정**</span><span class="sxs-lookup"><span data-stu-id="4d978-128">**Cache storage accounts**</span></span> | <span data-ttu-id="4d978-129">Vm이 원본에 대 한 변경 내용을 복제 toohello 대상 저장소 계정, 하기 전에 추적 되며 toohello 캐시 저장소 계정 hello 대상 위치에 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d978-129">Before changes on source VMs are replicated toohello target storage account, they are tracked and sent toohello cache storage account in hello target location.</span></span> <span data-ttu-id="4d978-130">이렇게 하면 hello VM에서 실행 되는 프로덕션 응용 프로그램에 미치는 영향을 최소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d978-130">This ensures minimal impact on production apps running on hello VM.</span></span>
<span data-ttu-id="4d978-131">**대상 저장소 계정**</span><span class="sxs-lookup"><span data-stu-id="4d978-131">**Target storage accounts**</span></span>  | <span data-ttu-id="4d978-132">Hello 대상 위치 toowhich hello 데이터의 저장소 계정 복제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d978-132">Storage accounts in hello target location toowhich hello data is replicated.</span></span>
<span data-ttu-id="4d978-133">**대상 가용성 집합**</span><span class="sxs-lookup"><span data-stu-id="4d978-133">**Target availability sets**</span></span>  | <span data-ttu-id="4d978-134">가용성을 복제 하는 hello Vm 있는 장애 조치 후에 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d978-134">Availability sets in which hello replicated VMs are located after failover.</span></span>

### <a name="step-2"></a><span data-ttu-id="4d978-135">2단계</span><span class="sxs-lookup"><span data-stu-id="4d978-135">Step 2</span></span>

<span data-ttu-id="4d978-136">복제를 사용 하는 hello 사이트 복구 확장 모바일 서비스는 hello VM에 자동으로 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d978-136">As replication is enabled, hello Site Recovery extension Mobility service is automatically installed on hello VM.</span></span> <span data-ttu-id="4d978-137">hello 다음 작업이 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d978-137">hello following occurs:</span></span>

1. <span data-ttu-id="4d978-138">hello VM Site Recovery에 등록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d978-138">hello VM is registered with Site Recovery.</span></span>

2. <span data-ttu-id="4d978-139">연속 복제 hello VM에 대해 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d978-139">Continuous replication is configured for hello VM.</span></span> <span data-ttu-id="4d978-140">데이터 디스크는 지속적으로 hello VM에서 쓰는 toohello 캐시 저장소 계정 hello 원본 위치에 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d978-140">Data writes on hello VM disks are continuously transferred toohello cache storage account in hello source location.</span></span>

   ![복제를 사용하도록 설정하는 프로세스, 2단계](./media/azure-to-azure-walkthrough-architecture/enable-replication-step-2.png)

  
  <span data-ttu-id="4d978-142">사이트 복구 되지 필요 함을 인바운드 연결 toohello VM note 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d978-142">Note that Site Recovery never needs inbound connectivity toohello VM.</span></span> <span data-ttu-id="4d978-143">연결 tooSite 복구 서비스 Url/IP 주소, Office 365 인증 Url/IP 주소 및 캐시 저장소 계정 IP 주소가 필요한 아웃 바운드만 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d978-143">Only outbound connectivity tooSite Recovery service URLs/IP addresses, Office 365 authentication URLs/IP addresses, and cache storage account IP addresses is needed.</span></span> 

## <a name="continuous-replication-process"></a><span data-ttu-id="4d978-144">연속 복제 프로세스</span><span class="sxs-lookup"><span data-stu-id="4d978-144">Continuous replication process</span></span>

<span data-ttu-id="4d978-145">연속 복제를 작동 한 후 즉시. 쓰기는 디스크 전송 toohello 캐시 저장소 계정.</span><span class="sxs-lookup"><span data-stu-id="4d978-145">After continuous replication is working, disk writes are immediately transferred toohello cache storage account.</span></span> <span data-ttu-id="4d978-146">사이트 복구 hello 데이터를 처리 하 고 대상 저장소 계정과 toohello 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="4d978-146">Site Recovery processes hello data and sends it toohello target storage account.</span></span> <span data-ttu-id="4d978-147">Hello 데이터를 처리 한 후에 몇 분 마다으로 hello 대상 저장소 계정에서 복구 지점이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d978-147">After hello data is processed, recovery points are generated in hello target storage account every few minutes.</span></span>

## <a name="failover-process"></a><span data-ttu-id="4d978-148">장애 조치(failover) 프로세스</span><span class="sxs-lookup"><span data-stu-id="4d978-148">Failover process</span></span>

<span data-ttu-id="4d978-149">장애 조치를 시작할 때 hello 대상 리소스 그룹, 대상 가상 네트워크, 대상 서브넷에 Vm 만들어집니다 hello 및 hello 대상 가용성 집합.</span><span class="sxs-lookup"><span data-stu-id="4d978-149">When you initiate a failover, hello VMs are created in hello target resource group, target virtual network, target subnet, and hello target availability set.</span></span> <span data-ttu-id="4d978-150">장애 조치(failover) 중에는 모든 복구 지점을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d978-150">During a failover, you can use any recovery point.</span></span>

![장애 조치(failover) 프로세스](./media/azure-to-azure-walkthrough-architecture/failover.png)

## <a name="next-steps"></a><span data-ttu-id="4d978-152">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4d978-152">Next steps</span></span>

<span data-ttu-id="4d978-153">너무 이동[2 단계: 사전 요구 사항 및 제한 사항 확인](azure-to-azure-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="4d978-153">Go too[Step 2: Verify prerequisites and limitations](azure-to-azure-walkthrough-prerequisites.md)</span></span>

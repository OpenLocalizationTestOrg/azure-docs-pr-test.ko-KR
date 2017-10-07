---
title: "aaaHow는 Azure 사이트 복구에서 수행 되는 Azure 지역 작업 간 Azure 가상 컴퓨터 복제 합니까?  | Microsoft Docs"
description: "이 문서에서는 구성 요소와 hello Azure Site Recovery 서비스를 사용 하 여 Azure 지역 간에 Azure Vm을 복제할 때 사용 되는 아키텍처의 개요를 제공 합니다."
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/29/2017
ms.author: sujayt
ms.openlocfilehash: 01eda83e490821f8afc8a2973c18a19453a2e84a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-azure-vm-replication-work-in-site-recovery"></a><span data-ttu-id="1666d-104">Site Recovery에서 Azure VM 복제가 작동하는 방식</span><span class="sxs-lookup"><span data-stu-id="1666d-104">How does Azure VM replication work in Site Recovery?</span></span>


<span data-ttu-id="1666d-105">이 문서에서는 hello 구성 요소 및 프로세스를 설명 hello를 사용 하 여 tooanother 한 지역에서에서 복제 하 고 Azure 가상 컴퓨터 (Vm) 복구에 관련 [Azure Site Recovery](site-recovery-overview.md) 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="1666d-105">This article describes hello components and processes involved in replicating and recovering Azure virtual machines (VMs) from one region tooanother by using hello [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

>[!NOTE]
><span data-ttu-id="1666d-106">Azure VM 복제 hello Site Recovery 서비스를 현재 미리 보기 중입니다.</span><span class="sxs-lookup"><span data-stu-id="1666d-106">Azure VM replication with hello Site Recovery service is currently in preview.</span></span>

<span data-ttu-id="1666d-107">이 문서에서는 hello 맨 아래에 대 한 설명을 게시 하거나 hello에서 질문 하기 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.</span><span class="sxs-lookup"><span data-stu-id="1666d-107">Post any comments at hello bottom of this article, or ask questions in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="architectural-components"></a><span data-ttu-id="1666d-108">아키텍처 구성 요소</span><span class="sxs-lookup"><span data-stu-id="1666d-108">Architectural components</span></span>

<span data-ttu-id="1666d-109">hello 다음 다이어그램은 높은 수준의 (이 예에서는 hello 미국 동부 위치)에 특정 지역에서 Azure VM 환경 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1666d-109">hello following diagram provides a high-level view of an Azure VM environment in a specific region (in this example, hello East US location).</span></span> <span data-ttu-id="1666d-110">Azure VM 환경은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1666d-110">In an Azure VM environment:</span></span>
- <span data-ttu-id="1666d-111">앱은 여러 저장소 계정에 디스크가 분산되어 있는 VM에서 실행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1666d-111">Apps can be running on VMs with disks spread across storage accounts.</span></span>
- <span data-ttu-id="1666d-112">hello Vm 가상 네트워크 내에서 하나 이상의 서브넷에 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1666d-112">hello VMs can be included in one or more subnets within a virtual network.</span></span>

![고객 환경](./media/site-recovery-azure-to-azure-architecture/source-environment.png)

<span data-ttu-id="1666d-114">Hello 배포 필수 구성 요소 및 hello에 대 한 요구 사항을 알아봅니다 [지원 매트릭스](site-recovery-support-matrix-azure-to-azure.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1666d-114">Learn about hello deployment prerequisites and requirements in hello [support matrix](site-recovery-support-matrix-azure-to-azure.md).</span></span>

## <a name="replication-process"></a><span data-ttu-id="1666d-115">복제 프로세스</span><span class="sxs-lookup"><span data-stu-id="1666d-115">Replication process</span></span>

### <a name="step-1"></a><span data-ttu-id="1666d-116">1단계</span><span class="sxs-lookup"><span data-stu-id="1666d-116">Step 1</span></span>

<span data-ttu-id="1666d-117">Hello Azure 포털에서에서 Azure VM 복제를 사용 하도록 설정 하면 hello 리소스 hello 뒤에 표시 된 다이어그램과 테이블에 자동으로 hello 대상 지역에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="1666d-117">When you enable Azure VM replication in hello Azure portal, hello resources shown in hello following diagram and table are automatically created in hello target region.</span></span> <span data-ttu-id="1666d-118">기본적으로 리소스는 원본 지역 설정을 기반으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="1666d-118">By default, resources are created based on source region settings.</span></span> <span data-ttu-id="1666d-119">필요에 따라 hello 대상 설정을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1666d-119">You can customize hello target settings as required.</span></span> <span data-ttu-id="1666d-120">[자세히 알아봅니다](site-recovery-replicate-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="1666d-120">[Learn more](site-recovery-replicate-azure-to-azure.md).</span></span>

![복제를 사용하도록 설정하는 프로세스, 1단계](./media/site-recovery-azure-to-azure-architecture/enable-replication-step-1.png)

<span data-ttu-id="1666d-122">**리소스**</span><span class="sxs-lookup"><span data-stu-id="1666d-122">**Resource**</span></span> | <span data-ttu-id="1666d-123">**세부 정보**</span><span class="sxs-lookup"><span data-stu-id="1666d-123">**Details**</span></span>
--- | ---
<span data-ttu-id="1666d-124">**대상 리소스 그룹**</span><span class="sxs-lookup"><span data-stu-id="1666d-124">**Target resource group**</span></span> | <span data-ttu-id="1666d-125">복제 된 Vm 장애 조치 후 속한 리소스 그룹 toowhich를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="1666d-125">hello resource group toowhich replicated VMs belong after failover.</span></span>
<span data-ttu-id="1666d-126">**대상 가상 네트워크**</span><span class="sxs-lookup"><span data-stu-id="1666d-126">**Target virtual network**</span></span> | <span data-ttu-id="1666d-127">복제 된 Vm이 있는 장애 조치 후 가상 네트워크를 hello입니다.</span><span class="sxs-lookup"><span data-stu-id="1666d-127">hello virtual network in which replicated VMs are located after failover.</span></span> <span data-ttu-id="1666d-128">네트워크 매핑은 원본 및 대상 가상 네트워크 간에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="1666d-128">A network mapping is created between source and target virtual networks, and vice versa.</span></span>
<span data-ttu-id="1666d-129">**캐시 저장소 계정**</span><span class="sxs-lookup"><span data-stu-id="1666d-129">**Cache storage accounts**</span></span> | <span data-ttu-id="1666d-130">Vm이 원본에 대 한 변경 내용을 복제 toohello 대상 저장소 계정, 하기 전에 추적 되며 toohello 캐시 저장소 계정 hello 대상 위치에 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1666d-130">Before changes on source VMs are replicated toohello target storage account, they are tracked and sent toohello cache storage account in hello target location.</span></span> <span data-ttu-id="1666d-131">이렇게 하면 hello VM에서 실행 되는 프로덕션 응용 프로그램에 미치는 영향을 최소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="1666d-131">This ensures minimal impact on production apps running on hello VM.</span></span>
<span data-ttu-id="1666d-132">**대상 저장소 계정**</span><span class="sxs-lookup"><span data-stu-id="1666d-132">**Target storage accounts**</span></span>  | <span data-ttu-id="1666d-133">Hello 대상 위치 toowhich hello 데이터의 저장소 계정 복제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1666d-133">Storage accounts in hello target location toowhich hello data is replicated.</span></span>
<span data-ttu-id="1666d-134">**대상 가용성 집합**</span><span class="sxs-lookup"><span data-stu-id="1666d-134">**Target availability sets**</span></span>  | <span data-ttu-id="1666d-135">가용성을 복제 하는 hello Vm 있는 장애 조치 후에 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1666d-135">Availability sets in which hello replicated VMs are located after failover.</span></span>

### <a name="step-2"></a><span data-ttu-id="1666d-136">2단계</span><span class="sxs-lookup"><span data-stu-id="1666d-136">Step 2</span></span>

<span data-ttu-id="1666d-137">복제를 사용 하는 hello 사이트 복구 확장 모바일 서비스는 hello VM에 자동으로 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1666d-137">As replication is enabled, hello Site Recovery extension Mobility service is automatically installed on hello VM.</span></span> <span data-ttu-id="1666d-138">hello 다음 작업이 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1666d-138">hello following occurs:</span></span>

1. <span data-ttu-id="1666d-139">hello VM Site Recovery에 등록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1666d-139">hello VM is registered with Site Recovery.</span></span>

2. <span data-ttu-id="1666d-140">연속 복제 hello VM에 대해 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1666d-140">Continuous replication is configured for hello VM.</span></span> <span data-ttu-id="1666d-141">데이터 디스크는 지속적으로 hello VM에서 쓰는 toohello 캐시 저장소 계정 hello 원본 위치에 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="1666d-141">Data writes on hello VM disks are continuously transferred toohello cache storage account in hello source location.</span></span>

   ![복제를 사용하도록 설정하는 프로세스, 2단계](./media/site-recovery-azure-to-azure-architecture/enable-replication-step-2.png)

   >[!IMPORTANT]
   > <span data-ttu-id="1666d-143">사이트 복구는 인바운드 연결 toohello VM 하지 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1666d-143">Site Recovery never needs inbound connectivity toohello VM.</span></span> <span data-ttu-id="1666d-144">hello VM 아웃 바운드 연결 tooSite 복구 서비스 Url/IP 주소, Office 365 인증 Url/IP 주소 및 캐시 저장소 계정 IP 주소가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1666d-144">hello VM needs only outbound connectivity tooSite Recovery service URLs/IP addresses, Office 365 authentication URLs/IP addresses, and cache storage account IP addresses.</span></span> <span data-ttu-id="1666d-145">자세한 내용은 참조 hello [Azure 가상 컴퓨터 복제를 위한 네트워킹 지침](site-recovery-azure-to-azure-networking-guidance.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="1666d-145">For more information, see hello [Networking guidance for replicating Azure virtual machines](site-recovery-azure-to-azure-networking-guidance.md) article.</span></span>

## <a name="continuous-replication-process"></a><span data-ttu-id="1666d-146">연속 복제 프로세스</span><span class="sxs-lookup"><span data-stu-id="1666d-146">Continuous replication process</span></span>

<span data-ttu-id="1666d-147">연속 복제를 작동 한 후 즉시. 쓰기는 디스크 전송 toohello 캐시 저장소 계정.</span><span class="sxs-lookup"><span data-stu-id="1666d-147">After continuous replication is working, disk writes are immediately transferred toohello cache storage account.</span></span> <span data-ttu-id="1666d-148">사이트 복구 hello 데이터를 처리 하 고 대상 저장소 계정과 toohello 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="1666d-148">Site Recovery processes hello data and sends it toohello target storage account.</span></span> <span data-ttu-id="1666d-149">Hello 데이터를 처리 한 후에 몇 분 마다으로 hello 대상 저장소 계정에서 복구 지점이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1666d-149">After hello data is processed, recovery points are generated in hello target storage account every few minutes.</span></span>

## <a name="failover-process"></a><span data-ttu-id="1666d-150">장애 조치(failover) 프로세스</span><span class="sxs-lookup"><span data-stu-id="1666d-150">Failover process</span></span>

<span data-ttu-id="1666d-151">장애 조치를 시작할 때 hello 대상 리소스 그룹, 대상 가상 네트워크, 대상 서브넷에 Vm 만들어집니다 hello 및 hello 대상 가용성 집합.</span><span class="sxs-lookup"><span data-stu-id="1666d-151">When you initiate a failover, hello VMs are created in hello target resource group, target virtual network, target subnet, and hello target availability set.</span></span> <span data-ttu-id="1666d-152">장애 조치(failover) 중에는 모든 복구 지점을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1666d-152">During a failover, you can use any recovery point.</span></span>

![장애 조치(failover) 프로세스](./media/site-recovery-azure-to-azure-architecture/failover.png)

## <a name="next-steps"></a><span data-ttu-id="1666d-154">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1666d-154">Next steps</span></span>

- <span data-ttu-id="1666d-155">Azure VM 복제를 위한 [네트워킹](site-recovery-azure-to-azure-networking-guidance.md)에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="1666d-155">Learn about [networking](site-recovery-azure-to-azure-networking-guidance.md) for Azure VM replication.</span></span>
- <span data-ttu-id="1666d-156">너무 연습에 따라[Azure Vm을 복제 합니다.](site-recovery-azure-to-azure.md)</span><span class="sxs-lookup"><span data-stu-id="1666d-156">Follow a walkthrough too[replicate Azure VMs.](site-recovery-azure-to-azure.md)</span></span>

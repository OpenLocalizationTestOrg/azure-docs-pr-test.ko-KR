---
title: "Azure Site Recovery에서 Azure 지역 간에 Azure 가상 컴퓨터 복제가 작동하는 방식  | Microsoft Docs"
description: "이 문서에서는 Azure Site Recovery 서비스를 사용하여 Azure 지역 간에 Azure VM을 복제하는 경우 사용되는 구성 요소와 아키텍처에 대한 개요를 제공합니다."
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
ms.openlocfilehash: ec397eaeda963f257d1bd996f1f57189bcde17ca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-does-azure-vm-replication-work-in-site-recovery"></a><span data-ttu-id="519e5-104">Site Recovery에서 Azure VM 복제가 작동하는 방식</span><span class="sxs-lookup"><span data-stu-id="519e5-104">How does Azure VM replication work in Site Recovery?</span></span>


<span data-ttu-id="519e5-105">이 문서에서는 [Azure Site Recovery](site-recovery-overview.md) 서비스를 사용하여 하나의 지역에서 다른 지역으로 Azure VM(가상 컴퓨터)을 복제하고 복구하는 데 관련되는 구성 요소와 프로세스에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="519e5-105">This article describes the components and processes involved in replicating and recovering Azure virtual machines (VMs) from one region to another by using the [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

>[!NOTE]
><span data-ttu-id="519e5-106">Site Recovery 서비스를 사용하는 Azure VM 복제는 현재 미리 보기로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="519e5-106">Azure VM replication with the Site Recovery service is currently in preview.</span></span>

<span data-ttu-id="519e5-107">이 문서의 하단에서 의견을 게시하거나 [Azure Recovery Services 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)에서 질문하세요.</span><span class="sxs-lookup"><span data-stu-id="519e5-107">Post any comments at the bottom of this article, or ask questions in the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="architectural-components"></a><span data-ttu-id="519e5-108">아키텍처 구성 요소</span><span class="sxs-lookup"><span data-stu-id="519e5-108">Architectural components</span></span>

<span data-ttu-id="519e5-109">다음 다이어그램은 특정 지역(이 예제에서는 미국 동부 지역)의 Azure VM 환경을 개략적으로 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="519e5-109">The following diagram provides a high-level view of an Azure VM environment in a specific region (in this example, the East US location).</span></span> <span data-ttu-id="519e5-110">Azure VM 환경은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="519e5-110">In an Azure VM environment:</span></span>
- <span data-ttu-id="519e5-111">앱은 여러 저장소 계정에 디스크가 분산되어 있는 VM에서 실행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="519e5-111">Apps can be running on VMs with disks spread across storage accounts.</span></span>
- <span data-ttu-id="519e5-112">VM은 가상 네트워크 내에서 하나 이상의 서브넷에 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="519e5-112">The VMs can be included in one or more subnets within a virtual network.</span></span>

![고객 환경](./media/site-recovery-azure-to-azure-architecture/source-environment.png)

<span data-ttu-id="519e5-114">[지원 매트릭스](site-recovery-support-matrix-azure-to-azure.md)에서 배포 필수 구성 요소 및 요구 사항을 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="519e5-114">Learn about the deployment prerequisites and requirements in the [support matrix](site-recovery-support-matrix-azure-to-azure.md).</span></span>

## <a name="replication-process"></a><span data-ttu-id="519e5-115">복제 프로세스</span><span class="sxs-lookup"><span data-stu-id="519e5-115">Replication process</span></span>

### <a name="step-1"></a><span data-ttu-id="519e5-116">1단계</span><span class="sxs-lookup"><span data-stu-id="519e5-116">Step 1</span></span>

<span data-ttu-id="519e5-117">Azure Portal에서 Azure VM 복제를 사용하는 경우 다음 다이어그램과 표에 표시된 리소스가 대상 지역에 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="519e5-117">When you enable Azure VM replication in the Azure portal, the resources shown in the following diagram and table are automatically created in the target region.</span></span> <span data-ttu-id="519e5-118">기본적으로 리소스는 원본 지역 설정을 기반으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="519e5-118">By default, resources are created based on source region settings.</span></span> <span data-ttu-id="519e5-119">필요에 따라 대상 설정을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="519e5-119">You can customize the target settings as required.</span></span> <span data-ttu-id="519e5-120">[자세히 알아보세요](site-recovery-replicate-azure-to-azure.md)을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="519e5-120">[Learn more](site-recovery-replicate-azure-to-azure.md).</span></span>

![복제를 사용하도록 설정하는 프로세스, 1단계](./media/site-recovery-azure-to-azure-architecture/enable-replication-step-1.png)

<span data-ttu-id="519e5-122">**리소스**</span><span class="sxs-lookup"><span data-stu-id="519e5-122">**Resource**</span></span> | <span data-ttu-id="519e5-123">**세부 정보**</span><span class="sxs-lookup"><span data-stu-id="519e5-123">**Details**</span></span>
--- | ---
<span data-ttu-id="519e5-124">**대상 리소스 그룹**</span><span class="sxs-lookup"><span data-stu-id="519e5-124">**Target resource group**</span></span> | <span data-ttu-id="519e5-125">장애 조치(failover) 후 복제된 VM이 속하게 되는 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="519e5-125">The resource group to which replicated VMs belong after failover.</span></span>
<span data-ttu-id="519e5-126">**대상 가상 네트워크**</span><span class="sxs-lookup"><span data-stu-id="519e5-126">**Target virtual network**</span></span> | <span data-ttu-id="519e5-127">장애 조치(failover) 후 복제된 VM이 있는 가상 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="519e5-127">The virtual network in which replicated VMs are located after failover.</span></span> <span data-ttu-id="519e5-128">네트워크 매핑은 원본 및 대상 가상 네트워크 간에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="519e5-128">A network mapping is created between source and target virtual networks, and vice versa.</span></span>
<span data-ttu-id="519e5-129">**캐시 저장소 계정**</span><span class="sxs-lookup"><span data-stu-id="519e5-129">**Cache storage accounts**</span></span> | <span data-ttu-id="519e5-130">원본 VM에 대한 변경 내용은 대상 저장소 계정에 복제되기 전에 추적되어 대상 위치의 캐시 저장소 계정으로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="519e5-130">Before changes on source VMs are replicated to the target storage account, they are tracked and sent to the cache storage account in the target location.</span></span> <span data-ttu-id="519e5-131">이렇게 하면 VM에서 실행 중인 프로덕션 앱에 미치는 영향을 최소화합니다.</span><span class="sxs-lookup"><span data-stu-id="519e5-131">This ensures minimal impact on production apps running on the VM.</span></span>
<span data-ttu-id="519e5-132">**대상 저장소 계정**</span><span class="sxs-lookup"><span data-stu-id="519e5-132">**Target storage accounts**</span></span>  | <span data-ttu-id="519e5-133">데이터가 복제되는 대상 위치의 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="519e5-133">Storage accounts in the target location to which the data is replicated.</span></span>
<span data-ttu-id="519e5-134">**대상 가용성 집합**</span><span class="sxs-lookup"><span data-stu-id="519e5-134">**Target availability sets**</span></span>  | <span data-ttu-id="519e5-135">장애 조치(failover) 후 복제된 VM이 있는 가용성 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="519e5-135">Availability sets in which the replicated VMs are located after failover.</span></span>

### <a name="step-2"></a><span data-ttu-id="519e5-136">2단계</span><span class="sxs-lookup"><span data-stu-id="519e5-136">Step 2</span></span>

<span data-ttu-id="519e5-137">복제를 사용하도록 설정하면 Site Recovery 확장 이동성 서비스가 VM에 자동으로 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="519e5-137">As replication is enabled, the Site Recovery extension Mobility service is automatically installed on the VM.</span></span> <span data-ttu-id="519e5-138">다음 동작이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="519e5-138">The following occurs:</span></span>

1. <span data-ttu-id="519e5-139">VM이 Site Recovery에 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="519e5-139">The VM is registered with Site Recovery.</span></span>

2. <span data-ttu-id="519e5-140">VM에 대해 연속 복제가 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="519e5-140">Continuous replication is configured for the VM.</span></span> <span data-ttu-id="519e5-141">VM 디스크에서의 데이터 쓰기가 원본 위치의 캐시 저장소 계정에 지속적으로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="519e5-141">Data writes on the VM disks are continuously transferred to the cache storage account in the source location.</span></span>

   ![복제를 사용하도록 설정하는 프로세스, 2단계](./media/site-recovery-azure-to-azure-architecture/enable-replication-step-2.png)

   >[!IMPORTANT]
   > <span data-ttu-id="519e5-143">Site Recovery에는 VM에 대한 인바운드 연결이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="519e5-143">Site Recovery never needs inbound connectivity to the VM.</span></span> <span data-ttu-id="519e5-144">VM은 Site Recovery 서비스 URL/IP 주소, Office 365 인증 URL/IP 주소 및 캐시 저장소 계정 IP 주소에 대한 아웃바운드 연결만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="519e5-144">The VM needs only outbound connectivity to Site Recovery service URLs/IP addresses, Office 365 authentication URLs/IP addresses, and cache storage account IP addresses.</span></span> <span data-ttu-id="519e5-145">자세한 내용은 [Networking guidance for replicating Azure virtual machines](site-recovery-azure-to-azure-networking-guidance.md)(Azure 가상 컴퓨터 복제를 위한 네트워킹 지침) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="519e5-145">For more information, see the [Networking guidance for replicating Azure virtual machines](site-recovery-azure-to-azure-networking-guidance.md) article.</span></span>

## <a name="continuous-replication-process"></a><span data-ttu-id="519e5-146">연속 복제 프로세스</span><span class="sxs-lookup"><span data-stu-id="519e5-146">Continuous replication process</span></span>

<span data-ttu-id="519e5-147">연속 복제가 작동한 후에는 디스크 쓰기가 캐시 저장소 계정으로 즉시 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="519e5-147">After continuous replication is working, disk writes are immediately transferred to the cache storage account.</span></span> <span data-ttu-id="519e5-148">Site Recovery는 데이터를 처리하여 대상 저장소 계정으로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="519e5-148">Site Recovery processes the data and sends it to the target storage account.</span></span> <span data-ttu-id="519e5-149">데이터가 처리된 후에는 몇 분마다 대상 저장소 계정에 복구 지점이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="519e5-149">After the data is processed, recovery points are generated in the target storage account every few minutes.</span></span>

## <a name="failover-process"></a><span data-ttu-id="519e5-150">장애 조치(failover) 프로세스</span><span class="sxs-lookup"><span data-stu-id="519e5-150">Failover process</span></span>

<span data-ttu-id="519e5-151">장애 조치(failover)를 시작하면 대상 리소스 그룹, 대상 가상 네트워크, 대상 서브넷 및 대상 가용성 집합에 VM이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="519e5-151">When you initiate a failover, the VMs are created in the target resource group, target virtual network, target subnet, and the target availability set.</span></span> <span data-ttu-id="519e5-152">장애 조치(failover) 중에는 모든 복구 지점을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="519e5-152">During a failover, you can use any recovery point.</span></span>

![장애 조치(failover) 프로세스](./media/site-recovery-azure-to-azure-architecture/failover.png)

## <a name="next-steps"></a><span data-ttu-id="519e5-154">다음 단계</span><span class="sxs-lookup"><span data-stu-id="519e5-154">Next steps</span></span>

- <span data-ttu-id="519e5-155">Azure VM 복제를 위한 [네트워킹](site-recovery-azure-to-azure-networking-guidance.md)에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="519e5-155">Learn about [networking](site-recovery-azure-to-azure-networking-guidance.md) for Azure VM replication.</span></span>
- <span data-ttu-id="519e5-156">[Azure VM 복제](site-recovery-azure-to-azure.md)를 연습해 보세요.</span><span class="sxs-lookup"><span data-stu-id="519e5-156">Follow a walkthrough to [replicate Azure VMs.](site-recovery-azure-to-azure.md)</span></span>

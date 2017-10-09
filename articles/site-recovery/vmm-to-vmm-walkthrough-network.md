---
title: "Azure 사이트 복구와 Hyper-v 복제 tooa 보조 VMM 사이트에 대 한 네트워킹 aaaPlan | Microsoft Docs"
description: "이 문서에서는 Azure 사이트 복구와 Hyper-v Vm tooa 보조 System Center VMM 사이트를 복제할 때 네트워크 계획을 설명 합니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 095f2d73-994e-4fc0-96f2-e03a7d72e492
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: raynew
ms.openlocfilehash: 5934db4a661a2c697a1a799c3848852250ddb451
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-3-plan-networking-for-hyper-v-vm-replication-tooa-secondary-vmm-site"></a><span data-ttu-id="67616-103">3 단계: Hyper-v VM 복제 tooa 보조 VMM 사이트에 대 한 네트워킹 계획</span><span class="sxs-lookup"><span data-stu-id="67616-103">Step 3: Plan networking for Hyper-V VM replication tooa secondary VMM site</span></span>

<span data-ttu-id="67616-104">System Center Virtual Machine Manager (VMM) 클라우드에서 관리 되는 Hyper-v 가상 컴퓨터 (Vm)를 복제 하는 경우 네트워킹이 문서 tooplan 읽을 배포 필수 조건 검토 한 후 tooa 보조 사이트를 사용 하 여 [Azure사이트복구](site-recovery-overview.md) hello Azure 포털의에서.</span><span class="sxs-lookup"><span data-stu-id="67616-104">After reviewing deployment prerequisites, read this article tooplan networking when replicating Hyper-V virtual machines (VMs) managed in System Center Virtual Machine Manager (VMM) clouds, tooa secondary site using [Azure Site Recovery](site-recovery-overview.md) in hello Azure portal.</span></span> 

<span data-ttu-id="67616-105">이 문서를 읽은 후 게시 설명을 hello 맨 아래에 하거나 hello에 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.</span><span class="sxs-lookup"><span data-stu-id="67616-105">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="network-mapping-overview"></a><span data-ttu-id="67616-106">네트워크 매핑 개요</span><span class="sxs-lookup"><span data-stu-id="67616-106">Network mapping overview</span></span>

<span data-ttu-id="67616-107">네트워크 매핑은 (VMM에서 관리 됨) Hyper-v Vm tooa 보조 데이터 센터를 복제할 때 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67616-107">Network mapping is used when replicating Hyper-V VMs (managed in VMM) tooa secondary datacenter.</span></span> <span data-ttu-id="67616-108">네트워크 매핑은 원본 VMM 서버의 VM 네트워크와 대상 VMM 서버의 VM 네트워크 사이를 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="67616-108">Network mapping maps between VM networks on a source VMM server, and VM networks on a target VMM server.</span></span> <span data-ttu-id="67616-109">매핑 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="67616-109">Mapping does hello following:</span></span>

- <span data-ttu-id="67616-110">**네트워크 연결**-장애 조치 후 Vm 연결 tooappropriate 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="67616-110">**Network connection**—Connects VMs tooappropriate networks after failover.</span></span> <span data-ttu-id="67616-111">hello 복제본 VM에 연결 된 toohello 대상 네트워크 매핑된 toohello 원본 네트워크를 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67616-111">hello replica VM will be connected toohello target network that's mapped toohello source network.</span></span>
- <span data-ttu-id="67616-112">**최적의 배치**-최적으로 위치 hello Hyper-v 호스트 서버에 복제본 Vm입니다.</span><span class="sxs-lookup"><span data-stu-id="67616-112">**Optimal placement**—Optimally places hello replica VMs on Hyper-V host servers.</span></span> <span data-ttu-id="67616-113">복제본 Vm 수 액세스 hello 매핑되는지 VM 네트워크 호스트에 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67616-113">Replica VMs are placed on hosts that can access hello mapped VM networks.</span></span>
- <span data-ttu-id="67616-114">**네트워크 매핑이 없는**-네트워크 매핑을 구성 하지 않는 경우 복제본 Vm 장애 조치 후 tooany 연결 된 VM 네트워크에 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="67616-114">**No network mapping**—If you don’t configure network mapping, replica VMs won’t be connected tooany VM networks after failover.</span></span>


### <a name="example"></a><span data-ttu-id="67616-115">예제</span><span class="sxs-lookup"><span data-stu-id="67616-115">Example</span></span>

<span data-ttu-id="67616-116">다음 예에서는 tooillustrate은이 메커니즘입니다.</span><span class="sxs-lookup"><span data-stu-id="67616-116">Here’s an example tooillustrate this mechanism.</span></span> <span data-ttu-id="67616-117">뉴욕과 시카고 두 위치에 있는 조직을 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="67616-117">Let’s take an organization with two locations in New York and Chicago.</span></span>

<span data-ttu-id="67616-118">**위치**</span><span class="sxs-lookup"><span data-stu-id="67616-118">**Location**</span></span> | <span data-ttu-id="67616-119">**VMM 서버**</span><span class="sxs-lookup"><span data-stu-id="67616-119">**VMM server**</span></span> | <span data-ttu-id="67616-120">**VM 네트워크**</span><span class="sxs-lookup"><span data-stu-id="67616-120">**VM networks**</span></span> | <span data-ttu-id="67616-121">**다음으로 매핑**</span><span class="sxs-lookup"><span data-stu-id="67616-121">**Mapped to**</span></span>
---|---|---|---
<span data-ttu-id="67616-122">뉴욕</span><span class="sxs-lookup"><span data-stu-id="67616-122">New York</span></span> | <span data-ttu-id="67616-123">VMM-뉴욕</span><span class="sxs-lookup"><span data-stu-id="67616-123">VMM-NewYork</span></span>| <span data-ttu-id="67616-124">VMNetwork1-뉴욕</span><span class="sxs-lookup"><span data-stu-id="67616-124">VMNetwork1-NewYork</span></span> | <span data-ttu-id="67616-125">TooVMNetwork1-시카고와 매핑된</span><span class="sxs-lookup"><span data-stu-id="67616-125">Mapped tooVMNetwork1-Chicago</span></span>
 |  | <span data-ttu-id="67616-126">VMNetwork2-뉴욕</span><span class="sxs-lookup"><span data-stu-id="67616-126">VMNetwork2-NewYork</span></span> | <span data-ttu-id="67616-127">매핑되지 않음</span><span class="sxs-lookup"><span data-stu-id="67616-127">Not mapped</span></span>
<span data-ttu-id="67616-128">시카코</span><span class="sxs-lookup"><span data-stu-id="67616-128">Chicago</span></span> | <span data-ttu-id="67616-129">VMM-시카고</span><span class="sxs-lookup"><span data-stu-id="67616-129">VMM-Chicago</span></span>| <span data-ttu-id="67616-130">VMNetwork1-시카고</span><span class="sxs-lookup"><span data-stu-id="67616-130">VMNetwork1-Chicago</span></span> | <span data-ttu-id="67616-131">매핑된 tooVMNetwork1-뉴욕</span><span class="sxs-lookup"><span data-stu-id="67616-131">Mapped tooVMNetwork1-NewYork</span></span>
 | | <span data-ttu-id="67616-132">VMNetwork1-시카고</span><span class="sxs-lookup"><span data-stu-id="67616-132">VMNetwork1-Chicago</span></span> | <span data-ttu-id="67616-133">매핑되지 않음</span><span class="sxs-lookup"><span data-stu-id="67616-133">Not mapped</span></span>

<span data-ttu-id="67616-134">이 예제에서:</span><span class="sxs-lookup"><span data-stu-id="67616-134">In this example:</span></span>

- <span data-ttu-id="67616-135">연결 된 tooVMNetwork1-뉴욕에 있는 모든 가상 컴퓨터에 대 한 복제 가상 컴퓨터를 만들면 tooVMNetwork1-시카고와 연결된 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67616-135">When a replica virtual machine is created for any virtual machine that is connected tooVMNetwork1-NewYork, it will be connected tooVMNetwork1-Chicago.</span></span>
- <span data-ttu-id="67616-136">VMNetwork2-뉴욕 또는 VMNetwork2-시카고에 대 한 복제 가상 컴퓨터를 만들면 연결된 tooany 네트워크 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="67616-136">When a replica virtual machine is created for VMNetwork2-NewYork or VMNetwork2-Chicago, it will not be connected tooany network.</span></span>

<span data-ttu-id="67616-137">예제 조직에 hello 논리 네트워크 hello 클라우드와 연결 된 VMM 클라우드가 설정 되어 방법을 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="67616-137">Here's how VMM clouds are set up in our example organization, and hello logical networks associated with hello clouds.</span></span>

#### <a name="cloud-protection-settings"></a><span data-ttu-id="67616-138">클라우드 보호 설정</span><span class="sxs-lookup"><span data-stu-id="67616-138">Cloud protection settings</span></span>

<span data-ttu-id="67616-139">**보호된 클라우드**</span><span class="sxs-lookup"><span data-stu-id="67616-139">**Protected cloud**</span></span> | <span data-ttu-id="67616-140">**클라우드 보호**</span><span class="sxs-lookup"><span data-stu-id="67616-140">**Protecting cloud**</span></span> | <span data-ttu-id="67616-141">**논리 네트워크(뉴욕)**</span><span class="sxs-lookup"><span data-stu-id="67616-141">**Logical network (New York)**</span></span>  
---|---|---
<span data-ttu-id="67616-142">GoldCloud1</span><span class="sxs-lookup"><span data-stu-id="67616-142">GoldCloud1</span></span> | <span data-ttu-id="67616-143">GoldCloud2</span><span class="sxs-lookup"><span data-stu-id="67616-143">GoldCloud2</span></span> |
<span data-ttu-id="67616-144">SilverCloud1</span><span class="sxs-lookup"><span data-stu-id="67616-144">SilverCloud1</span></span>| <span data-ttu-id="67616-145">SilverCloud2</span><span class="sxs-lookup"><span data-stu-id="67616-145">SilverCloud2</span></span> |
<span data-ttu-id="67616-146">GoldCloud2</span><span class="sxs-lookup"><span data-stu-id="67616-146">GoldCloud2</span></span> | <p><span data-ttu-id="67616-147">해당 없음</span><span class="sxs-lookup"><span data-stu-id="67616-147">NA</span></span></p><p></p> | <p><span data-ttu-id="67616-148">LogicalNetwork1-뉴욕</span><span class="sxs-lookup"><span data-stu-id="67616-148">LogicalNetwork1-NewYork</span></span></p><p><span data-ttu-id="67616-149">LogicalNetwork1-시카고</span><span class="sxs-lookup"><span data-stu-id="67616-149">LogicalNetwork1-Chicago</span></span></p>
<span data-ttu-id="67616-150">SilverCloud2</span><span class="sxs-lookup"><span data-stu-id="67616-150">SilverCloud2</span></span> | <p><span data-ttu-id="67616-151">해당 없음</span><span class="sxs-lookup"><span data-stu-id="67616-151">NA</span></span></p><p></p> | <p><span data-ttu-id="67616-152">LogicalNetwork1-뉴욕</span><span class="sxs-lookup"><span data-stu-id="67616-152">LogicalNetwork1-NewYork</span></span></p><p><span data-ttu-id="67616-153">LogicalNetwork1-시카고</span><span class="sxs-lookup"><span data-stu-id="67616-153">LogicalNetwork1-Chicago</span></span></p>

#### <a name="logical-and-vm-network-settings"></a><span data-ttu-id="67616-154">논리 및 VM 네트워크 설정</span><span class="sxs-lookup"><span data-stu-id="67616-154">Logical and VM network settings</span></span>

<span data-ttu-id="67616-155">**위치**</span><span class="sxs-lookup"><span data-stu-id="67616-155">**Location**</span></span> | <span data-ttu-id="67616-156">**논리 네트워크**</span><span class="sxs-lookup"><span data-stu-id="67616-156">**Logical network**</span></span> | <span data-ttu-id="67616-157">**연결된 VM 네트워크**</span><span class="sxs-lookup"><span data-stu-id="67616-157">**Associated VM network**</span></span>
---|---|---
<span data-ttu-id="67616-158">뉴욕</span><span class="sxs-lookup"><span data-stu-id="67616-158">New York</span></span> | <span data-ttu-id="67616-159">LogicalNetwork1-뉴욕</span><span class="sxs-lookup"><span data-stu-id="67616-159">LogicalNetwork1-NewYork</span></span> | <span data-ttu-id="67616-160">VMNetwork1-뉴욕</span><span class="sxs-lookup"><span data-stu-id="67616-160">VMNetwork1-NewYork</span></span>
<span data-ttu-id="67616-161">시카코</span><span class="sxs-lookup"><span data-stu-id="67616-161">Chicago</span></span> | <span data-ttu-id="67616-162">LogicalNetwork1-시카고</span><span class="sxs-lookup"><span data-stu-id="67616-162">LogicalNetwork1-Chicago</span></span> | <span data-ttu-id="67616-163">VMNetwork1-시카고</span><span class="sxs-lookup"><span data-stu-id="67616-163">VMNetwork1-Chicago</span></span>
 | <span data-ttu-id="67616-164">LogicalNetwork2Chicago</span><span class="sxs-lookup"><span data-stu-id="67616-164">LogicalNetwork2Chicago</span></span> | <span data-ttu-id="67616-165">VMNetwork2-시카고</span><span class="sxs-lookup"><span data-stu-id="67616-165">VMNetwork2-Chicago</span></span>

#### <a name="target-network-settings"></a><span data-ttu-id="67616-166">대상 네트워크 설정</span><span class="sxs-lookup"><span data-stu-id="67616-166">Target network settings</span></span>

<span data-ttu-id="67616-167">Hello 대상 VM 네트워크를 선택 하면 이러한 설정에 따라 hello 다음 표에서 사용할 수 있는 hello 선택 항목을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="67616-167">Based on these settings, when you select hello target VM network, hello following table shows hello choices that will be available.</span></span>

<span data-ttu-id="67616-168">**선택**</span><span class="sxs-lookup"><span data-stu-id="67616-168">**Select**</span></span> | <span data-ttu-id="67616-169">**보호된 클라우드**</span><span class="sxs-lookup"><span data-stu-id="67616-169">**Protected cloud**</span></span> | <span data-ttu-id="67616-170">**클라우드 보호**</span><span class="sxs-lookup"><span data-stu-id="67616-170">**Protecting cloud**</span></span> | <span data-ttu-id="67616-171">**사용 가능한 대상 네트워크**</span><span class="sxs-lookup"><span data-stu-id="67616-171">**Target network available**</span></span>
---|---|---|---
<span data-ttu-id="67616-172">VMNetwork1-시카고</span><span class="sxs-lookup"><span data-stu-id="67616-172">VMNetwork1-Chicago</span></span> | <span data-ttu-id="67616-173">SilverCloud1</span><span class="sxs-lookup"><span data-stu-id="67616-173">SilverCloud1</span></span> | <span data-ttu-id="67616-174">SilverCloud2</span><span class="sxs-lookup"><span data-stu-id="67616-174">SilverCloud2</span></span> | <span data-ttu-id="67616-175">사용 가능</span><span class="sxs-lookup"><span data-stu-id="67616-175">Available</span></span>
 | <span data-ttu-id="67616-176">GoldCloud1</span><span class="sxs-lookup"><span data-stu-id="67616-176">GoldCloud1</span></span> | <span data-ttu-id="67616-177">GoldCloud2</span><span class="sxs-lookup"><span data-stu-id="67616-177">GoldCloud2</span></span> | <span data-ttu-id="67616-178">사용 가능</span><span class="sxs-lookup"><span data-stu-id="67616-178">Available</span></span>
<span data-ttu-id="67616-179">VMNetwork2-시카고</span><span class="sxs-lookup"><span data-stu-id="67616-179">VMNetwork2-Chicago</span></span> | <span data-ttu-id="67616-180">SilverCloud1</span><span class="sxs-lookup"><span data-stu-id="67616-180">SilverCloud1</span></span> | <span data-ttu-id="67616-181">SilverCloud2</span><span class="sxs-lookup"><span data-stu-id="67616-181">SilverCloud2</span></span> | <span data-ttu-id="67616-182">사용할 수 없음</span><span class="sxs-lookup"><span data-stu-id="67616-182">Not available</span></span>
 | <span data-ttu-id="67616-183">GoldCloud1</span><span class="sxs-lookup"><span data-stu-id="67616-183">GoldCloud1</span></span> | <span data-ttu-id="67616-184">GoldCloud2</span><span class="sxs-lookup"><span data-stu-id="67616-184">GoldCloud2</span></span> | <span data-ttu-id="67616-185">사용 가능</span><span class="sxs-lookup"><span data-stu-id="67616-185">Available</span></span>


<span data-ttu-id="67616-186">Hello 대상 네트워크에 여러 서브넷과 이러한 서브넷 중 하나가 이름이 같은 hello는 hello에서 원본 가상 컴퓨터가 위치한 서브넷,으로 다음 hello hello 복제 가상 컴퓨터에 장애 조치 후 연결 된 toothat 대상 서브넷이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67616-186">If hello target network has multiple subnets and one of those subnets has hello same name as hello subnet on which hello source virtual machine is located, then hello replica virtual machine will be connected toothat target subnet after failover.</span></span> <span data-ttu-id="67616-187">이름이 일치 하는 대상 서브넷 이면 hello 가상 컴퓨터 연결된 toohello hello 네트워크의 첫 번째 서브넷 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67616-187">If there’s no target subnet with a matching name, hello virtual machine will be connected toohello first subnet in hello network.</span></span>


#### <a name="failback-behavior"></a><span data-ttu-id="67616-188">장애 복구 동작</span><span class="sxs-lookup"><span data-stu-id="67616-188">Failback behavior</span></span>

<span data-ttu-id="67616-189">장애 복구 (역방향 복제)의 hello 경우 어떤 일이 생기 toosee VMNetwork1-뉴욕 매핑된 tooVMNetwork1-시카고와 설정을 다음 hello로 인지를 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="67616-189">toosee what happens in hello case of failback (reverse replication), let’s assume that VMNetwork1-NewYork is mapped tooVMNetwork1-Chicago, with hello following settings.</span></span>


<span data-ttu-id="67616-190">**가상 컴퓨터**</span><span class="sxs-lookup"><span data-stu-id="67616-190">**Virtual machine**</span></span> | <span data-ttu-id="67616-191">**연결 된 tooVM 네트워크**</span><span class="sxs-lookup"><span data-stu-id="67616-191">**Connected tooVM network**</span></span>
---|---
<span data-ttu-id="67616-192">VM1</span><span class="sxs-lookup"><span data-stu-id="67616-192">VM1</span></span> | <span data-ttu-id="67616-193">VMNetwork1-네트워크</span><span class="sxs-lookup"><span data-stu-id="67616-193">VMNetwork1-Network</span></span>
<span data-ttu-id="67616-194">VM2(VM1의 복제)</span><span class="sxs-lookup"><span data-stu-id="67616-194">VM2 (replica of VM1)</span></span> | <span data-ttu-id="67616-195">VMNetwork1-시카고</span><span class="sxs-lookup"><span data-stu-id="67616-195">VMNetwork1-Chicago</span></span>

<span data-ttu-id="67616-196">이러한 설정을 사용하여 몇 가지 가능한 시나리오에서 발생하는 결과를 검토해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="67616-196">With these settings, let's review what happens in a couple of possible scenarios.</span></span>

<span data-ttu-id="67616-197">**시나리오**</span><span class="sxs-lookup"><span data-stu-id="67616-197">**Scenario**</span></span> | <span data-ttu-id="67616-198">**결과**</span><span class="sxs-lookup"><span data-stu-id="67616-198">**Outcome**</span></span>
---|---
<span data-ttu-id="67616-199">장애 조치 후 v M-2의 hello 네트워크 속성 변경 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="67616-199">No change in hello network properties of VM-2 after failover.</span></span> | <span data-ttu-id="67616-200">V M-1에 연결 된 toohello 원본 네트워크 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67616-200">VM-1 remains connected toohello source network.</span></span>
<span data-ttu-id="67616-201">장애 조치(failover) 후 VM-2의 네트워크 속성이 변경되고 연결이 끊김</span><span class="sxs-lookup"><span data-stu-id="67616-201">Network properties of VM-2 are changed after failover and is disconnected.</span></span> | <span data-ttu-id="67616-202">VM-1의 연결이 끊김</span><span class="sxs-lookup"><span data-stu-id="67616-202">VM-1 is disconnected.</span></span>
<span data-ttu-id="67616-203">V M-2의 네트워크 속성은 장애 조치 후 변경 되 고 tooVMNetwork2-시카고와 연결된 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67616-203">Network properties of VM-2 are changed after failover and is connected tooVMNetwork2-Chicago.</span></span> | <span data-ttu-id="67616-204">VMNetwork2-시카고가 매핑되지 않는 경우 VM-1의 연결이 끊김</span><span class="sxs-lookup"><span data-stu-id="67616-204">If VMNetwork2-Chicago isn’t mapped, VM-1 will be disconnected.</span></span>
<span data-ttu-id="67616-205">VMNetwork1-시카고의 네트워크 매핑이 변경됨</span><span class="sxs-lookup"><span data-stu-id="67616-205">Network mapping of VMNetwork1-Chicago is changed.</span></span> | <span data-ttu-id="67616-206">V M-1에 연결 된 toohello 매핑된 네트워크와 지금 tooVMNetwork1-시카고 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67616-206">VM-1 will be connected toohello network now mapped tooVMNetwork1-Chicago.</span></span>



## <a name="prepare-for-network-mapping"></a><span data-ttu-id="67616-207">네트워크 매핑을 준비</span><span class="sxs-lookup"><span data-stu-id="67616-207">Prepare for network mapping</span></span>

1. <span data-ttu-id="67616-208">Hello 원본 및 대상 VMM 서버에서 hello 원본 클라우드와 대상 클라우드에 연결한 논리 네트워크에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67616-208">On hello source and target VMM servers, you should have a logical network associated with hello source and target clouds.</span></span> 
2. <span data-ttu-id="67616-209">Hello 원본 및 대상 서버의 VM 네트워크 논리 네트워크 연결 된 toohello 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67616-209">In hello source and target servers, you should have a VM network linked toohello logical network.</span></span>
3. <span data-ttu-id="67616-210">Hello 원본 위치에 있는 Hyper-v 호스트에서 Vm에 연결 된 toohello 원본 VM 네트워크 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67616-210">VMs on Hyper-V hosts in hello source location should be linked toohello source VM network.</span></span> <span data-ttu-id="67616-211">동일한 hello에 VM 네트워크 간 매핑을 구성할 수만 단일 VMM 서버를 사용 하는 경우 서버.</span><span class="sxs-lookup"><span data-stu-id="67616-211">If you're only using a single VMM server, you can configure mapping between VM networks on hello same server.</span></span>

<span data-ttu-id="67616-212">Site Recovery를 배포하는 동안 네트워크 매핑을 설정하면 다음 작업이 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="67616-212">Here's what happens when you set up network mapping during Site Recovery deployment:</span></span>

- <span data-ttu-id="67616-213">네트워크 매핑을 설정 하 고 대상 VM 네트워크를 선택 하는 경우 hello 원본 VM 네트워크를 사용 하는 hello VMM 원본 클라우드가 표시 됩니다, hello hello 대상 클라우드가 사용 가능한 대상 VM 네트워크와 함께 합니다.</span><span class="sxs-lookup"><span data-stu-id="67616-213">When you set up network mapping and select a target VM network, hello VMM source clouds that use hello source VM network will be displayed, along with hello available target VM networks on hello target clouds.</span></span>
- - <span data-ttu-id="67616-214">매핑이 올바르게 구성 된 하 고 복제가 활성화 되어 원본이 VM 연결된 tooits 원본 VM 네트워크 수와 hello 대상 위치의 복제본 연결 될 tooits VM 네트워크를 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="67616-214">When mapping is configured correctly and replication is enabled, a source VM will be connected tooits source VM network, and its replica at hello target location will be connected tooits mapped VM network.</span></span>
- <span data-ttu-id="67616-215">Hello 대상 네트워크에 여러 서브넷과 이러한 서브넷 중 하나가 이름이 같은 hello는 hello에서 원본 가상 컴퓨터가 위치한 서브넷,으로 다음 hello hello 복제 가상 컴퓨터에 장애 조치 후 연결 된 toothat 대상 서브넷이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67616-215">If hello target network has multiple subnets, and one of those subnets has hello same name as hello subnet on which hello source virtual machine is located, then hello replica virtual machine will be connected toothat target subnet after failover.</span></span> <span data-ttu-id="67616-216">이름이 일치 하는 대상 서브넷 이면 hello VM hello 네트워크에 연결 된 toohello 첫 번째 서브넷 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67616-216">If there’s no target subnet with a matching name, hello VM will be connected toohello first subnet in hello network.</span></span>

## <a name="connect-toovms-after-failover"></a><span data-ttu-id="67616-217">장애 조치 후 tooVMs 연결</span><span class="sxs-lookup"><span data-stu-id="67616-217">Connect tooVMs after failover</span></span>

<span data-ttu-id="67616-218">복제 및 장애 조치 전략을 계획할 때는 hello 주요 질문 중 하나는 어떻게 장애 조치 후 tooconnect toohello 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="67616-218">When planning your replication and failover strategy, one of hello key questions is how tooconnect toohello replica after failover.</span></span> <span data-ttu-id="67616-219">다음의 두 가지 방법 중에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67616-219">There are a couple of choices:</span></span> 

- <span data-ttu-id="67616-220">**다른 IP 주소를 사용 하 여**:에 대해 선택할 수 toouse 다른 IP 주소를 hello VM을 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="67616-220">**Use a different IP address**: You can select toouse a different IP address for hello replicated VM.</span></span> <span data-ttu-id="67616-221">이 시나리오 hello에 VM 장애 조치 후 새 IP 주소를 갖게 되며 DNS 업데이트가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="67616-221">In this scenario hello VM gets a new IP address after failover, and a DNS update is required.</span></span>
- <span data-ttu-id="67616-222">**유지 동일한 IP 주소를 hello**: 할 수 있습니다 toouse hello hello 복제본 VM에 대 한 동일한 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="67616-222">**Retain hello same IP address**: You might want toouse hello same IP address for hello replica VM.</span></span> <span data-ttu-id="67616-223">동일한 IP 주소를 간소화 하면서 hello 장애 조치 후 네트워크 관련된 문제를 줄여 hello 복구 합니다.</span><span class="sxs-lookup"><span data-stu-id="67616-223">Keeping hello same IP addresses simplifies hello recovery by reducing network related issues after failover.</span></span> 

## <a name="retain-ip-addresses"></a><span data-ttu-id="67616-224">IP 주소 유지</span><span class="sxs-lookup"><span data-stu-id="67616-224">Retain IP addresses</span></span>

<span data-ttu-id="67616-225">Hello toohello 보조 사이트 장애 조치 한 후 기본 사이트, 전체 서브넷 장애 조치를 수행 하 고 업데이트할 수 경로 tooindicate hello hello IP 주소의 새 위치 또는 대체 배포 hello 간의 늘어난된 서브넷 tooretain hello IP 주소를 원하는 경우 기본 및 복구 사이트 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="67616-225">If you want tooretain hello IP addresses from hello primary site after failover toohello secondary site, you can do a full subnet failover, and update routes tooindicate hello new location of hello IP addresses, or alternative deploy a stretched subnet between hello primary and hello recovery sites.</span></span>

### <a name="stretched-subnet"></a><span data-ttu-id="67616-226">늘어난 서브넷</span><span class="sxs-lookup"><span data-stu-id="67616-226">Stretched subnet</span></span>

<span data-ttu-id="67616-227">스트레치 된 서브넷에 hello 서브넷은 동시에 hello 기본 및 보조 사이트 모두 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67616-227">In a stretched subnet, hello subnet is available simultaneously in both hello primary and secondary site.</span></span> <span data-ttu-id="67616-228">서버와 해당 (계층 3) IP 구성 toohello 보조 사이트를 이동 하는 경우 hello 네트워크 hello 트래픽 toohello 새 위치로 자동으로 라우팅할 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67616-228">If you move a server and its IP (Layer 3) configuration toohello secondary site, hello network will route hello traffic toohello new location automatically.</span></span> 

<span data-ttu-id="67616-229">계층 2(데이터 링크 계층) 측면을 고려하면 확대 VLAN을 관리할 수 있는 네트워킹 장비가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="67616-229">From a Layer 2 (data link layer) perspective, you need networking equipment that can manage a stretched VLAN.</span></span> <span data-ttu-id="67616-230">또한 늘이기 hello VLAN, 여 hello 잠재적인 장애 도메인은 tooboth 사이트의 경우 기본적으로 단일 실패 지점이 되 고 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="67616-230">In addition, by stretching hello VLAN, hello potential fault domain extends tooboth sites, essentially becoming a single point of failure.</span></span> <span data-ttu-id="67616-231">이러한 현상이 발생할 가능성은 거의 없기는 하지만, 브로드캐스트 스톰이 시작해서 격리되지 못하게 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67616-231">While this is an unlikely, it could happen that a broadcast storm started and cannot be isolated.</span></span> 


### <a name="subnet-failover"></a><span data-ttu-id="67616-232">서브넷 장애 조치(failover)</span><span class="sxs-lookup"><span data-stu-id="67616-232">Subnet failover</span></span>

<span data-ttu-id="67616-233">서브넷 장애 조치 tooobtain hello 확대 되므로 hello 서브넷의 이점 실제로 늘이거나 하지 않고 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67616-233">You can run a subnet failover tooobtain hello benefits of hello stretched subnet, without actually stretching it.</span></span> <span data-ttu-id="67616-234">이 솔루션에서는 서브넷을 사용할 수 hello 원본 또는 대상 사이트에서 하지만 둘 다에 없는 동시에 합니다.</span><span class="sxs-lookup"><span data-stu-id="67616-234">In this solution, a subnet will be available in hello source or target site, but not at both simultaneously.</span></span> <span data-ttu-id="67616-235">toomaintain hello IP 주소 공간 hello 이벤트에는 장애 조치를 정렬할 수 있습니다 프로그래밍 방식으로 한 사이트 tooanother에서 hello 라우터 인프라 toomove hello 서브넷에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="67616-235">toomaintain hello IP address space in hello event of a failover, you can programmatically arrange for hello router infrastructure toomove hello subnets from one site tooanother.</span></span> <span data-ttu-id="67616-236">서브넷으로 이동 하므로 장애 조치 발생 후 hello Vm에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="67616-236">After when failover occurs, subnets would move with hello associated VMs.</span></span> <span data-ttu-id="67616-237">hello 주요 단점은 실패 하는 hello 이벤트에서 toomove hello 전체 서브넷 있는입니다.</span><span class="sxs-lookup"><span data-stu-id="67616-237">hello main drawback is that in hello event of a failure, you have toomove hello whole subnet.</span></span>

### <a name="example"></a><span data-ttu-id="67616-238">예제</span><span class="sxs-lookup"><span data-stu-id="67616-238">Example</span></span>

<span data-ttu-id="67616-239">전체 서브넷 장애 조치(failover)의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="67616-239">Here's an example of complete subnet failover.</span></span> <span data-ttu-id="67616-240">hello 기본 사이트의 서브넷 192.168.1.0/24에서 실행 중인 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="67616-240">hello primary site has applications running in subnet 192.168.1.0/24.</span></span> <span data-ttu-id="67616-241">장애 조치가이 서브넷의 모든 hello Vm toohello 보조 사이트를 통해 실패 하는 IP 주소를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="67616-241">At failover, all hello VMs in this subnet are failed over toohello secondary site, and retain their IP addresses.</span></span> <span data-ttu-id="67616-242">경로 필요 toobe 수정 tooreflect hello 팩트 toosubnet 192.168.1.0/24 속한 모든 hello VM 가상 컴퓨터 toohello 보조 사이트를 이동 이제 했습니다.</span><span class="sxs-lookup"><span data-stu-id="67616-242">Routes need toobe modified tooreflect hello fact that all hello VM virtual machines belonging toosubnet 192.168.1.0/24 have now moved toohello secondary site.</span></span>

<span data-ttu-id="67616-243">다음 그래픽 표시 hello 서브넷 장애 조치 전후 hello:</span><span class="sxs-lookup"><span data-stu-id="67616-243">hello following graphics show hello subnets before and after failover:</span></span>

- <span data-ttu-id="67616-244">장애 조치 하기 전에 서브넷 192.168.0.1/24 활성화 되어 hello 원본 사이트에서 장애 조치 후 hello 보조 사이트에 활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67616-244">Before failover, subnet 192.168.0.1/24 is active on hello source site, become active on hello secondary site after failover.</span></span>
- <span data-ttu-id="67616-245">주 사이트 및 사이트 복구, 세 번째 사이트 및 기본 사이트 간의 hello 라우팅합니다 및 세 번째 사이트와 복구 사이트 toobe 적절히 수정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67616-245">hello routes between primary site and recovery site, third site and primary site, and third site and recovery site will have toobe appropriately modified.</span></span>

<span data-ttu-id="67616-246">**장애 조치(failover) 전**</span><span class="sxs-lookup"><span data-stu-id="67616-246">**Before failover**</span></span>

![장애 조치(failover) 전](./media/vmm-to-vmm-walkthrough-network/network-design2.png)

<span data-ttu-id="67616-248">**장애 조치(failover) 후**</span><span class="sxs-lookup"><span data-stu-id="67616-248">**After failover**</span></span>

![장애 조치(failover) 후](./media/vmm-to-vmm-walkthrough-network/network-design3.png)

<span data-ttu-id="67616-250">장애 조치(failover) 후에는 다음 작업이 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="67616-250">After failover, here's what happens:</span></span>

- <span data-ttu-id="67616-251">사이트 복구 hello 고정 IP 주소 풀에서 각 VMM 인스턴스에 대 한 hello 관련 네트워크에서 VM hello에서 각 네트워크 인터페이스에 대 한 IP 주소를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="67616-251">Site Recovery allocates an IP address for each network interface on hello VM, from hello static IP address pool in hello relevant network, for each VMM instance.</span></span>
- <span data-ttu-id="67616-252">Hello 보조 사이트에 hello IP 주소 풀은 하는 경우와 같지 않다는 hello 원본 사이트, 사이트 복구에 할당 하는 hello 동일한 IP 주소 (hello 원본 VM)의 toohello 복제본 VM hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="67616-252">If hello IP address pool in hello secondary site is hello same as that on hello source site, Site Recovery allocates hello same IP address (of hello source VM) toohello replica VM.</span></span> <span data-ttu-id="67616-253">VMM에서 hello IP 주소가 예약 되었는지 하지만 hello Hyper-v 호스트에 hello 장애 조치 IP 주소로 설정 되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="67616-253">hello IP address is reserved in VMM, but it isn't set as hello failover IP address on hello Hyper-V host.</span></span> <span data-ttu-id="67616-254">hello hyper-v 호스트의 IP 주소를 장애 조치 hello 장애 조치 하기 바로 전에 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67616-254">hello failover IP address on a Hyper-v host is set just before hello failover.</span></span>
- <span data-ttu-id="67616-255">Hello 동일한 IP 주소를 사용할 수 없는 경우 사이트 복구 hello 풀에서 사용 가능한 다른 IP 주소를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="67616-255">If hello same IP address isn't available, Site Recovery allocates another available IP address from hello pool.</span></span>
- <span data-ttu-id="67616-256">Vm에서 DHCP를 사용 하는 경우 사이트 복구 hello IP 주소를 관리 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="67616-256">If VMs use DHCP, Site Recovery doesn't manage hello IP addresses.</span></span> <span data-ttu-id="67616-257">DHCP hello toocheck 필요한 hello 보조 사이트 서버 hello hello 원본 사이트와 동일한 범위에서 주소를 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67616-257">You need toocheck that hello DHCP server on hello secondary site can allocate address from hello same range as hello source site.</span></span>

### <a name="validate-hello-ip-address"></a><span data-ttu-id="67616-258">Hello IP 주소의 유효성을 검사합니다</span><span class="sxs-lookup"><span data-stu-id="67616-258">Validate hello IP address</span></span>

<span data-ttu-id="67616-259">VM에 대 한 보호를 활성화 한 후에 다음 샘플 스크립트 tooverify hello 할당 된 주소 toohello VM 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67616-259">After you enable protection for a VM, you can use following sample script tooverify hello address assigned toohello VM.</span></span> <span data-ttu-id="67616-260">hello 동일한 IP 주소 hello 장애 조치 IP 주소로 설정 되며 장애 조치 시 hello toohello VM을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="67616-260">hello same IP address will be set as hello failover IP address, and assigned toohello VM at hello time of failover:</span></span>

    ```
    $vm = Get-SCVirtualMachine -Name <VM_NAME>
    $na = $vm[0].VirtualNetworkAdapters>
    $ip = Get-SCIPAddress -GrantToObjectID $na[0].id
    $ip.address 
    ```

## <a name="changing-ip-addresses"></a><span data-ttu-id="67616-261">IP 주소 변경</span><span class="sxs-lookup"><span data-stu-id="67616-261">Changing IP addresses</span></span>

<span data-ttu-id="67616-262">이 시나리오에서는 장애 조치 하는 Vm의 hello IP 주소가 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67616-262">In this scenario, hello IP addresses of VMs that fail over are changed.</span></span> <span data-ttu-id="67616-263">hello이이 솔루션의 단점은 hello 유지 관리가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="67616-263">hello drawback of this solution is hello maintenance required.</span></span> <span data-ttu-id="67616-264">일반적으로는 복제본 VM이 시작된 후에 DNS가 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="67616-264">Typically, DNS will be updated after replica VMs start.</span></span> <span data-ttu-id="67616-265">DNS 항목 toobe 변경 하거나 되는 네트워크와 업데이트 된 캐시 된 항목에 fluster 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67616-265">DNS entries might need toobe changed or fluster in thenetwork, and cached entries updated.</span></span> <span data-ttu-id="67616-266">이로 인해 가동 중지 시간이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67616-266">This can result in downtime.</span></span> <span data-ttu-id="67616-267">다음 방법을 통해 가동 중지 시간을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67616-267">Downtime can be mitigated as follows:</span></span>

- <span data-ttu-id="67616-268">인트라넷 응용 프로그램의 경우 낮은 TTL 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="67616-268">Use low TTL values for intranet applications.</span></span>
- <span data-ttu-id="67616-269">Tooupdate hello DNS 서버 tooensure 시기 적절 한 업데이트를 사이트 복구 복구 계획 스크립트 다음에 오는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="67616-269">Use hello following script in a Site Recovery recovery plan, tooupdate hello DNS server tooensure a timely update.</span></span> <span data-ttu-id="67616-270">동적 DNS 등록을 사용 하는 경우에 hello 스크립트를 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="67616-270">You don't need hello script if you use dynamic DNS registration.</span></span>

    ```
    param(
    string]$Zone,
    [string]$name,
    [string]$IP
    )
    $Record = Get-DnsServerResourceRecord -ZoneName $zone -Name $name
    $newrecord = $record.clone()
    $newrecord.RecordData[0].IPv4Address  =  $IP
    Set-DnsServerResourceRecord -zonename $zone -OldInputObject $record -NewInputObject $Newrecord
    ```
    
### <a name="example"></a><span data-ttu-id="67616-271">예제</span><span class="sxs-lookup"><span data-stu-id="67616-271">Example</span></span> 

<span data-ttu-id="67616-272">기본 hello 간에 toouse 서로 다른 IP 주소 및 hello 복구 사이트를 계획 중인 시나리오를 살펴보겠습니다. 이 예제에서는 서로 다른 IP 주소 기본 및 보조 사이트에 걸쳐 있고 hello 주 가상 컴퓨터 또는 복구 사이트에서 호스팅되는 응용 프로그램에서 세 번째의 사이트에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67616-272">Let's look at a scenario in which you're planning toouse different IP addresses across hello primary and hello recovery sites.In this example we have different IP addresses across primary and secondary sites, and there;s a third site from which applications hosted on hello primary or recovery site can be accessed.</span></span>

- <span data-ttu-id="67616-273">장애 조치 하기 전에 앱 hello 기본 사이트에 호스팅된 서브넷 192.168.1.0/24 이므로 서브넷 172.16.1.0/24 hello 보조 사이트에 구성 된 toobe 장애 조치 후 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67616-273">Before failover, apps are hosted subnet 192.168.1.0/24 on hello primary site, and are configured toobe in subnet 172.16.1.0/24 on hello secondary site after a failover.</span></span>
- <span data-ttu-id="67616-274">세 사이트 모두 서로 액세스할 수 있도록 VPN 연결/네트워크 라우팅이 적절하게 구성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="67616-274">VPN connections/network routes have been configured appropriately so that all three sites can access each other.</span></span>
- <span data-ttu-id="67616-275">장애 조치 후 응용 프로그램 hello 복구 서브넷에 복원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67616-275">After failover, apps will be restored in hello recovery subnet.</span></span> <span data-ttu-id="67616-276">이 시나리오에서는 없습니다 필요 toofail hello 전체 서브넷을 통해 않으며 변경이 필요한 tooreconfigure VPN 또는 네트워크 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="67616-276">In this scenario there's no need toofail over hello entire subnet, and no changes are needed tooreconfigure VPN or network routes.</span></span> <span data-ttu-id="67616-277">hello 장애 조치 및 일부 DNS 업데이트를 응용 프로그램에 계속 액세스할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="67616-277">hello failover, and some DNS updates, ensure that applications remain accessible.</span></span>
- <span data-ttu-id="67616-278">DNS 구성된 tooallow 동적 업데이트를 하는 경우 다음 hello Vm 등록 됩니다 장애 조치 후 시작할 때 hello 새 IP 주소를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="67616-278">If DNS is configured tooallow dynamic updates, then hello VMs will register themselves using hello new IP address, when they start after failover.</span></span>

<span data-ttu-id="67616-279">**장애 조치(failover) 전**</span><span class="sxs-lookup"><span data-stu-id="67616-279">**Before failover**</span></span>

![다른 IP - 장애 조치 전](./media/vmm-to-vmm-walkthrough-network/network-design10.png)

<span data-ttu-id="67616-281">**장애 조치(failover) 후**</span><span class="sxs-lookup"><span data-stu-id="67616-281">**After failover**</span></span>

![다른 IP - 장애 조치 후](./media/vmm-to-vmm-walkthrough-network/network-design11.png)



## <a name="next-steps"></a><span data-ttu-id="67616-283">다음 단계</span><span class="sxs-lookup"><span data-stu-id="67616-283">Next steps</span></span>

<span data-ttu-id="67616-284">너무 이동[4 단계: 준비 VMM 및 Hyper-v](vmm-to-vmm-walkthrough-vmm-hyper-v.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="67616-284">Go too[Step 4: Prepare VMM and Hyper-V](vmm-to-vmm-walkthrough-vmm-hyper-v.md).</span></span>



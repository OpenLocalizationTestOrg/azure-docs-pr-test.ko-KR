---
title: "사이트 복구와 Hyper-v VM 복제에 대 한 네트워크 매핑 aaaPlan | Microsoft Docs"
description: "온-프레미스 데이터 센터 tooAzure 또는 tooa 보조 사이트에서 Hyper-v 가상 컴퓨터 복제에 대 한 네트워크 매핑을 설정 합니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: tysonn
ms.assetid: fcaa2f52-489d-4c1c-865f-9e78e000b351
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/23/2017
ms.author: raynew
ms.openlocfilehash: 86199b5840ea10fd33630bcc75d14340a49e01bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="plan-network-mapping-for-hyper-v-vm-replication-with-site-recovery"></a><span data-ttu-id="b4718-103">Site Recovery를 사용하여 Hyper-V VM 복제를 위한 네트워크 매핑 계획</span><span class="sxs-lookup"><span data-stu-id="b4718-103">Plan network mapping for Hyper-V VM replication with Site Recovery</span></span>



<span data-ttu-id="b4718-104">이 문서에서는 Hyper-v Vm tooAzure 또는 tooa 보조 사이트의 복제 하는 동안 매핑, hello를 사용 하 여 네트워크에 대 한 계획과 toounderstand [Azure Site Recovery 서비스](site-recovery-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b4718-104">This article helps you toounderstand and plan for network mapping during replication of Hyper-V VMs tooAzure, or tooa secondary site, using hello [Azure Site Recovery service](site-recovery-overview.md).</span></span>

<span data-ttu-id="b4718-105">읽은 후이 문서 hello 아래쪽이 문서에 대 한 설명을 게시 하거나 hello에 대 한 기술적 질문 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.</span><span class="sxs-lookup"><span data-stu-id="b4718-105">After reading this article post any comments at hello bottom of this article, or ask technical questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="network-mapping-for-replication-tooazure"></a><span data-ttu-id="b4718-106">복제 tooAzure에 대 한 네트워크 매핑</span><span class="sxs-lookup"><span data-stu-id="b4718-106">Network mapping for replication tooAzure</span></span>

<span data-ttu-id="b4718-107">네트워크 매핑은 (VMM에서 관리 됨) Hyper-v Vm tooAzure 복제할 때 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4718-107">Network mapping is used when replicating Hyper-V VMs (managed in VMM) tooAzure.</span></span> <span data-ttu-id="b4718-108">네트워크 매핑은 원본 VMM 서버의 VM 네트워크와 대상 Azure 네트워크 사이를 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="b4718-108">Network mapping maps between VM networks on a source VMM server, and target Azure networks.</span></span> <span data-ttu-id="b4718-109">매핑 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b4718-109">Mapping does hello following:</span></span>

- <span data-ttu-id="b4718-110">**네트워크 연결**-복제 된 Azure Vm으로 연결 된 toohello 매핑된 네트워크 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4718-110">**Network connection**—Ensures that replicated Azure VMs are connected toohello mapped network.</span></span> <span data-ttu-id="b4718-111">장애 조치 hello에 동일 하는 모든 컴퓨터에서 서로 다른 복구 계획 장애 조치 될 경우에 네트워크 tooeach 기타, 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4718-111">All machines which fail over on hello same network can connect tooeach other, even if they failed over in different recovery plans.</span></span>
- <span data-ttu-id="b4718-112">**네트워크 게이트웨이**-hello 대상 Azure 네트워크에 네트워크 게이트웨이가 설치 되 면 하는 경우 Vm tooother 온-프레미스 가상 컴퓨터에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4718-112">**Network gateway**—If a network gateway is set up on hello target Azure network, VMs can connect tooother on-premises virtual machines.</span></span>

<span data-ttu-id="b4718-113">다음 사항에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="b4718-113">Note that:</span></span>

- <span data-ttu-id="b4718-114">소스를 VMM VM 네트워크 tooan Azure 가상 네트워크를 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="b4718-114">You map a source VMM VM network tooan Azure virtual network.</span></span>
- <span data-ttu-id="b4718-115">Hello에 Azure Vm 장애 조치 후 원본 네트워크에 연결 된 toohello 매핑된 대상 가상 네트워크가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4718-115">After failover Azure VMs in hello source network will be connected toohello mapped target virtual network.</span></span>
- <span data-ttu-id="b4718-116">새 Vm toohello 원본 VM 네트워크에 연결 된 추가 복제가 실행 되 면 toohello 매핑된 Azure 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="b4718-116">New VMs added toohello source VM network are connected toohello mapped Azure network when replication occurs.</span></span>
- <span data-ttu-id="b4718-117">Hello 대상 네트워크에 여러 서브넷이 hello에 이러한 서브넷 중 하나는 hello 원본 가상 컴퓨터는 서브넷 이름이 같은 있는 경우 hello 복제본 가상 컴퓨터가 장애 조치 후 toothat 대상 서브넷 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4718-117">If hello target network has multiple subnets, and one of those subnets has hello same name as subnet on which hello source virtual machine is located, then hello replica virtual machine connects toothat target subnet after failover.</span></span>
- <span data-ttu-id="b4718-118">이름이 일치 하는 대상 서브넷 이면 hello 네트워크의 첫 번째 서브넷 toohello hello 가상 컴퓨터에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4718-118">If there’s no target subnet with a matching name, hello virtual machine connects toohello first subnet in hello network.</span></span>


## <a name="network-mapping-for-replication-tooa-secondary-datacenter"></a><span data-ttu-id="b4718-119">복제 tooa 보조 데이터 센터에 대 한 네트워크 매핑</span><span class="sxs-lookup"><span data-stu-id="b4718-119">Network mapping for replication tooa secondary datacenter</span></span>

<span data-ttu-id="b4718-120">네트워크 매핑은 (System Center Virtual Machine Manager (VMM)에서 관리 됨) Hyper-v Vm tooa 보조 데이터 센터를 복제할 때 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4718-120">Network mapping is used when replicating Hyper-V VMs (managed in System Center Virtual Machine Manager (VMM)) tooa secondary datacenter.</span></span> <span data-ttu-id="b4718-121">네트워크 매핑은 원본 VMM 서버의 VM 네트워크와 대상 VMM 서버의 VM 네트워크 사이를 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="b4718-121">Network mapping maps between VM networks on a source VMM server, and VM networks on a target VMM server.</span></span> <span data-ttu-id="b4718-122">매핑 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b4718-122">Mapping does hello following:</span></span>

- <span data-ttu-id="b4718-123">**네트워크 연결**-장애 조치 후 Vm 연결 tooappropriate 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="b4718-123">**Network connection**—Connects VMs tooappropriate networks after failover.</span></span> <span data-ttu-id="b4718-124">hello 복제본 VM에 연결 된 toohello 대상 네트워크 매핑된 toohello 원본 네트워크를 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4718-124">hello replica VM will be connected toohello target network that's mapped toohello source network.</span></span>
- <span data-ttu-id="b4718-125">**최적의 배치**-최적으로 위치 hello Hyper-v 호스트 서버에 복제본 Vm입니다.</span><span class="sxs-lookup"><span data-stu-id="b4718-125">**Optimal placement**—Optimally places hello replica VMs on Hyper-V host servers.</span></span> <span data-ttu-id="b4718-126">복제본 Vm 수 액세스 hello 매핑되는지 VM 네트워크 호스트에 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4718-126">Replica VMs are placed on hosts that can access hello mapped VM networks.</span></span>
- <span data-ttu-id="b4718-127">**네트워크 매핑이 없는**-네트워크 매핑을 구성 하지 않는 경우 복제본 Vm 장애 조치 후 tooany 연결 된 VM 네트워크에 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b4718-127">**No network mapping**—If you don’t configure network mapping, replica VMs won’t be connected tooany VM networks after failover.</span></span>

<span data-ttu-id="b4718-128">다음 사항에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="b4718-128">Note that:</span></span>

- <span data-ttu-id="b4718-129">네트워크 매핑은 두 명의 VMM 서버의 VM 네트워크 간 구성할 수 있습니다 또는 단일 VMM 서버에서 두 사이트에서 관리 하는 경우 환영 동일 서버.</span><span class="sxs-lookup"><span data-stu-id="b4718-129">Network mapping can be configured between VM networks on two VMM servers, or on a single VMM server if two sites are managed by hello same server.</span></span>
- <span data-ttu-id="b4718-130">매핑이 올바르게 구성 되 고 복제가 설정 되어 hello 기본 위치의 VM에 연결 된 tooa 네트워크 됩니다와 hello 대상 위치의 복제본 연결 될 네트워크 tooits에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4718-130">When mapping is configured correctly and replication is enabled, a VM at hello primary location will be connected tooa network, and its replica at hello target location will be connected tooits mapped network.</span></span>
-
- <span data-ttu-id="b4718-131">네트워크가 올바르게 설정 되었는지, VMM에서 네트워크 매핑 중 대상 VM 네트워크를 선택 하면, hello 원본 VM 네트워크를 사용 하는 hello VMM 원본 클라우드가 표시 됩니다, hello에 사용 되는 hello 대상 클라우드가 사용 가능한 대상 VM 네트워크와 함께 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4718-131">If networks have been set up correctly in VMM, when you select a target VM network during network mapping, hello VMM source clouds that use hello source VM network will be displayed, along with hello available target VM networks on hello target clouds that are used for protection.</span></span>
- <span data-ttu-id="b4718-132">Hello 대상 네트워크에 여러 서브넷과 이러한 서브넷 중 하나가 이름이 같은 hello는 hello에서 원본 가상 컴퓨터가 위치한 서브넷,으로 다음 hello hello 복제 가상 컴퓨터에 장애 조치 후 연결 된 toothat 대상 서브넷이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4718-132">If hello target network has multiple subnets and one of those subnets has hello same name as hello subnet on which hello source virtual machine is located, then hello replica virtual machine will be connected toothat target subnet after failover.</span></span> <span data-ttu-id="b4718-133">이름이 일치 하는 대상 서브넷 이면 hello 가상 컴퓨터 연결된 toohello hello 네트워크의 첫 번째 서브넷 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4718-133">If there’s no target subnet with a matching name, hello virtual machine will be connected toohello first subnet in hello network.</span></span>



### <a name="example"></a><span data-ttu-id="b4718-134">예제</span><span class="sxs-lookup"><span data-stu-id="b4718-134">Example</span></span>

<span data-ttu-id="b4718-135">다음 예에서는 tooillustrate은이 메커니즘입니다.</span><span class="sxs-lookup"><span data-stu-id="b4718-135">Here’s an example tooillustrate this mechanism.</span></span> <span data-ttu-id="b4718-136">뉴욕과 시카고 두 위치에 있는 조직을 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b4718-136">Let’s take an organization with two locations in New York and Chicago.</span></span>

<span data-ttu-id="b4718-137">**위치**</span><span class="sxs-lookup"><span data-stu-id="b4718-137">**Location**</span></span> | <span data-ttu-id="b4718-138">**VMM 서버**</span><span class="sxs-lookup"><span data-stu-id="b4718-138">**VMM server**</span></span> | <span data-ttu-id="b4718-139">**VM 네트워크**</span><span class="sxs-lookup"><span data-stu-id="b4718-139">**VM networks**</span></span> | <span data-ttu-id="b4718-140">**다음으로 매핑**</span><span class="sxs-lookup"><span data-stu-id="b4718-140">**Mapped to**</span></span>
---|---|---|---
<span data-ttu-id="b4718-141">뉴욕</span><span class="sxs-lookup"><span data-stu-id="b4718-141">New York</span></span> | <span data-ttu-id="b4718-142">VMM-뉴욕</span><span class="sxs-lookup"><span data-stu-id="b4718-142">VMM-NewYork</span></span>| <span data-ttu-id="b4718-143">VMNetwork1-뉴욕</span><span class="sxs-lookup"><span data-stu-id="b4718-143">VMNetwork1-NewYork</span></span> | <span data-ttu-id="b4718-144">TooVMNetwork1-시카고와 매핑된</span><span class="sxs-lookup"><span data-stu-id="b4718-144">Mapped tooVMNetwork1-Chicago</span></span>
 |  | <span data-ttu-id="b4718-145">VMNetwork2-뉴욕</span><span class="sxs-lookup"><span data-stu-id="b4718-145">VMNetwork2-NewYork</span></span> | <span data-ttu-id="b4718-146">매핑되지 않음</span><span class="sxs-lookup"><span data-stu-id="b4718-146">Not mapped</span></span>
<span data-ttu-id="b4718-147">시카코</span><span class="sxs-lookup"><span data-stu-id="b4718-147">Chicago</span></span> | <span data-ttu-id="b4718-148">VMM-시카고</span><span class="sxs-lookup"><span data-stu-id="b4718-148">VMM-Chicago</span></span>| <span data-ttu-id="b4718-149">VMNetwork1-시카고</span><span class="sxs-lookup"><span data-stu-id="b4718-149">VMNetwork1-Chicago</span></span> | <span data-ttu-id="b4718-150">매핑된 tooVMNetwork1-뉴욕</span><span class="sxs-lookup"><span data-stu-id="b4718-150">Mapped tooVMNetwork1-NewYork</span></span>
 | | <span data-ttu-id="b4718-151">VMNetwork1-시카고</span><span class="sxs-lookup"><span data-stu-id="b4718-151">VMNetwork1-Chicago</span></span> | <span data-ttu-id="b4718-152">매핑되지 않음</span><span class="sxs-lookup"><span data-stu-id="b4718-152">Not mapped</span></span>

<span data-ttu-id="b4718-153">이 예제에서:</span><span class="sxs-lookup"><span data-stu-id="b4718-153">In this example:</span></span>

- <span data-ttu-id="b4718-154">연결 된 tooVMNetwork1-뉴욕에 있는 모든 가상 컴퓨터에 대 한 복제 가상 컴퓨터를 만들면 tooVMNetwork1-시카고와 연결된 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4718-154">When a replica virtual machine is created for any virtual machine that is connected tooVMNetwork1-NewYork, it will be connected tooVMNetwork1-Chicago.</span></span>
- <span data-ttu-id="b4718-155">VMNetwork2-뉴욕 또는 VMNetwork2-시카고에 대 한 복제 가상 컴퓨터를 만들면 연결된 tooany 네트워크 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b4718-155">When a replica virtual machine is created for VMNetwork2-NewYork or VMNetwork2-Chicago, it will not be connected tooany network.</span></span>

<span data-ttu-id="b4718-156">예제 조직에 hello 논리 네트워크 hello 클라우드와 연결 된 VMM 클라우드가 설정 되어 방법을 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b4718-156">Here's how VMM clouds are set up in our example organization, and hello logical networks associated with hello clouds.</span></span>

#### <a name="cloud-protection-settings"></a><span data-ttu-id="b4718-157">클라우드 보호 설정</span><span class="sxs-lookup"><span data-stu-id="b4718-157">Cloud protection settings</span></span>

<span data-ttu-id="b4718-158">**보호된 클라우드**</span><span class="sxs-lookup"><span data-stu-id="b4718-158">**Protected cloud**</span></span> | <span data-ttu-id="b4718-159">**클라우드 보호**</span><span class="sxs-lookup"><span data-stu-id="b4718-159">**Protecting cloud**</span></span> | <span data-ttu-id="b4718-160">**논리 네트워크(뉴욕)**</span><span class="sxs-lookup"><span data-stu-id="b4718-160">**Logical network (New York)**</span></span>  
---|---|---
<span data-ttu-id="b4718-161">GoldCloud1</span><span class="sxs-lookup"><span data-stu-id="b4718-161">GoldCloud1</span></span> | <span data-ttu-id="b4718-162">GoldCloud2</span><span class="sxs-lookup"><span data-stu-id="b4718-162">GoldCloud2</span></span> |
<span data-ttu-id="b4718-163">SilverCloud1</span><span class="sxs-lookup"><span data-stu-id="b4718-163">SilverCloud1</span></span>| <span data-ttu-id="b4718-164">SilverCloud2</span><span class="sxs-lookup"><span data-stu-id="b4718-164">SilverCloud2</span></span> |
<span data-ttu-id="b4718-165">GoldCloud2</span><span class="sxs-lookup"><span data-stu-id="b4718-165">GoldCloud2</span></span> | <p><span data-ttu-id="b4718-166">해당 없음</span><span class="sxs-lookup"><span data-stu-id="b4718-166">NA</span></span></p><p></p> | <p><span data-ttu-id="b4718-167">LogicalNetwork1-뉴욕</span><span class="sxs-lookup"><span data-stu-id="b4718-167">LogicalNetwork1-NewYork</span></span></p><p><span data-ttu-id="b4718-168">LogicalNetwork1-시카고</span><span class="sxs-lookup"><span data-stu-id="b4718-168">LogicalNetwork1-Chicago</span></span></p>
<span data-ttu-id="b4718-169">SilverCloud2</span><span class="sxs-lookup"><span data-stu-id="b4718-169">SilverCloud2</span></span> | <p><span data-ttu-id="b4718-170">해당 없음</span><span class="sxs-lookup"><span data-stu-id="b4718-170">NA</span></span></p><p></p> | <p><span data-ttu-id="b4718-171">LogicalNetwork1-뉴욕</span><span class="sxs-lookup"><span data-stu-id="b4718-171">LogicalNetwork1-NewYork</span></span></p><p><span data-ttu-id="b4718-172">LogicalNetwork1-시카고</span><span class="sxs-lookup"><span data-stu-id="b4718-172">LogicalNetwork1-Chicago</span></span></p>

#### <a name="logical-and-vm-network-settings"></a><span data-ttu-id="b4718-173">논리 및 VM 네트워크 설정</span><span class="sxs-lookup"><span data-stu-id="b4718-173">Logical and VM network settings</span></span>

<span data-ttu-id="b4718-174">**위치**</span><span class="sxs-lookup"><span data-stu-id="b4718-174">**Location**</span></span> | <span data-ttu-id="b4718-175">**논리 네트워크**</span><span class="sxs-lookup"><span data-stu-id="b4718-175">**Logical network**</span></span> | <span data-ttu-id="b4718-176">**연결된 VM 네트워크**</span><span class="sxs-lookup"><span data-stu-id="b4718-176">**Associated VM network**</span></span>
---|---|---
<span data-ttu-id="b4718-177">뉴욕</span><span class="sxs-lookup"><span data-stu-id="b4718-177">New York</span></span> | <span data-ttu-id="b4718-178">LogicalNetwork1-뉴욕</span><span class="sxs-lookup"><span data-stu-id="b4718-178">LogicalNetwork1-NewYork</span></span> | <span data-ttu-id="b4718-179">VMNetwork1-뉴욕</span><span class="sxs-lookup"><span data-stu-id="b4718-179">VMNetwork1-NewYork</span></span>
<span data-ttu-id="b4718-180">시카코</span><span class="sxs-lookup"><span data-stu-id="b4718-180">Chicago</span></span> | <span data-ttu-id="b4718-181">LogicalNetwork1-시카고</span><span class="sxs-lookup"><span data-stu-id="b4718-181">LogicalNetwork1-Chicago</span></span> | <span data-ttu-id="b4718-182">VMNetwork1-시카고</span><span class="sxs-lookup"><span data-stu-id="b4718-182">VMNetwork1-Chicago</span></span>
 | <span data-ttu-id="b4718-183">LogicalNetwork2Chicago</span><span class="sxs-lookup"><span data-stu-id="b4718-183">LogicalNetwork2Chicago</span></span> | <span data-ttu-id="b4718-184">VMNetwork2-시카고</span><span class="sxs-lookup"><span data-stu-id="b4718-184">VMNetwork2-Chicago</span></span>

#### <a name="target-network-settings"></a><span data-ttu-id="b4718-185">대상 네트워크 설정</span><span class="sxs-lookup"><span data-stu-id="b4718-185">Target network settings</span></span>

<span data-ttu-id="b4718-186">Hello 대상 VM 네트워크를 선택 하면 이러한 설정에 따라 hello 다음 표에서 사용할 수 있는 hello 선택 항목을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4718-186">Based on these settings, when you select hello target VM network, hello following table shows hello choices that will be available.</span></span>

<span data-ttu-id="b4718-187">**선택**</span><span class="sxs-lookup"><span data-stu-id="b4718-187">**Select**</span></span> | <span data-ttu-id="b4718-188">**보호된 클라우드**</span><span class="sxs-lookup"><span data-stu-id="b4718-188">**Protected cloud**</span></span> | <span data-ttu-id="b4718-189">**클라우드 보호**</span><span class="sxs-lookup"><span data-stu-id="b4718-189">**Protecting cloud**</span></span> | <span data-ttu-id="b4718-190">**사용 가능한 대상 네트워크**</span><span class="sxs-lookup"><span data-stu-id="b4718-190">**Target network available**</span></span>
---|---|---|---
<span data-ttu-id="b4718-191">VMNetwork1-시카고</span><span class="sxs-lookup"><span data-stu-id="b4718-191">VMNetwork1-Chicago</span></span> | <span data-ttu-id="b4718-192">SilverCloud1</span><span class="sxs-lookup"><span data-stu-id="b4718-192">SilverCloud1</span></span> | <span data-ttu-id="b4718-193">SilverCloud2</span><span class="sxs-lookup"><span data-stu-id="b4718-193">SilverCloud2</span></span> | <span data-ttu-id="b4718-194">사용 가능</span><span class="sxs-lookup"><span data-stu-id="b4718-194">Available</span></span>
 | <span data-ttu-id="b4718-195">GoldCloud1</span><span class="sxs-lookup"><span data-stu-id="b4718-195">GoldCloud1</span></span> | <span data-ttu-id="b4718-196">GoldCloud2</span><span class="sxs-lookup"><span data-stu-id="b4718-196">GoldCloud2</span></span> | <span data-ttu-id="b4718-197">사용 가능</span><span class="sxs-lookup"><span data-stu-id="b4718-197">Available</span></span>
<span data-ttu-id="b4718-198">VMNetwork2-시카고</span><span class="sxs-lookup"><span data-stu-id="b4718-198">VMNetwork2-Chicago</span></span> | <span data-ttu-id="b4718-199">SilverCloud1</span><span class="sxs-lookup"><span data-stu-id="b4718-199">SilverCloud1</span></span> | <span data-ttu-id="b4718-200">SilverCloud2</span><span class="sxs-lookup"><span data-stu-id="b4718-200">SilverCloud2</span></span> | <span data-ttu-id="b4718-201">사용할 수 없음</span><span class="sxs-lookup"><span data-stu-id="b4718-201">Not available</span></span>
 | <span data-ttu-id="b4718-202">GoldCloud1</span><span class="sxs-lookup"><span data-stu-id="b4718-202">GoldCloud1</span></span> | <span data-ttu-id="b4718-203">GoldCloud2</span><span class="sxs-lookup"><span data-stu-id="b4718-203">GoldCloud2</span></span> | <span data-ttu-id="b4718-204">사용 가능</span><span class="sxs-lookup"><span data-stu-id="b4718-204">Available</span></span>


<span data-ttu-id="b4718-205">Hello 대상 네트워크에 여러 서브넷과 이러한 서브넷 중 하나가 이름이 같은 hello는 hello에서 원본 가상 컴퓨터가 위치한 서브넷,으로 다음 hello hello 복제 가상 컴퓨터에 장애 조치 후 연결 된 toothat 대상 서브넷이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4718-205">If hello target network has multiple subnets and one of those subnets has hello same name as hello subnet on which hello source virtual machine is located, then hello replica virtual machine will be connected toothat target subnet after failover.</span></span> <span data-ttu-id="b4718-206">이름이 일치 하는 대상 서브넷 이면 hello 가상 컴퓨터 연결된 toohello hello 네트워크의 첫 번째 서브넷 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4718-206">If there’s no target subnet with a matching name, hello virtual machine will be connected toohello first subnet in hello network.</span></span>


#### <a name="failback-behavior"></a><span data-ttu-id="b4718-207">장애 복구 동작</span><span class="sxs-lookup"><span data-stu-id="b4718-207">Failback behavior</span></span>

<span data-ttu-id="b4718-208">장애 복구 (역방향 복제)의 hello 경우 어떤 일이 생기 toosee VMNetwork1-뉴욕 매핑된 tooVMNetwork1-시카고와 설정을 다음 hello로 인지를 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b4718-208">toosee what happens in hello case of failback (reverse replication), let’s assume that VMNetwork1-NewYork is mapped tooVMNetwork1-Chicago, with hello following settings.</span></span>


<span data-ttu-id="b4718-209">**가상 컴퓨터**</span><span class="sxs-lookup"><span data-stu-id="b4718-209">**Virtual machine**</span></span> | <span data-ttu-id="b4718-210">**연결 된 tooVM 네트워크**</span><span class="sxs-lookup"><span data-stu-id="b4718-210">**Connected tooVM network**</span></span>
---|---
<span data-ttu-id="b4718-211">VM1</span><span class="sxs-lookup"><span data-stu-id="b4718-211">VM1</span></span> | <span data-ttu-id="b4718-212">VMNetwork1-네트워크</span><span class="sxs-lookup"><span data-stu-id="b4718-212">VMNetwork1-Network</span></span>
<span data-ttu-id="b4718-213">VM2(VM1의 복제)</span><span class="sxs-lookup"><span data-stu-id="b4718-213">VM2 (replica of VM1)</span></span> | <span data-ttu-id="b4718-214">VMNetwork1-시카고</span><span class="sxs-lookup"><span data-stu-id="b4718-214">VMNetwork1-Chicago</span></span>

<span data-ttu-id="b4718-215">이러한 설정을 사용하여 몇 가지 가능한 시나리오에서 발생하는 결과를 검토해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b4718-215">With these settings, let's review what happens in a couple of possible scenarios.</span></span>

<span data-ttu-id="b4718-216">**시나리오**</span><span class="sxs-lookup"><span data-stu-id="b4718-216">**Scenario**</span></span> | <span data-ttu-id="b4718-217">**결과**</span><span class="sxs-lookup"><span data-stu-id="b4718-217">**Outcome**</span></span>
---|---
<span data-ttu-id="b4718-218">장애 조치 후 v M-2의 hello 네트워크 속성 변경 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b4718-218">No change in hello network properties of VM-2 after failover.</span></span> | <span data-ttu-id="b4718-219">V M-1에 연결 된 toohello 원본 네트워크 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4718-219">VM-1 remains connected toohello source network.</span></span>
<span data-ttu-id="b4718-220">장애 조치(failover) 후 VM-2의 네트워크 속성이 변경되고 연결이 끊김</span><span class="sxs-lookup"><span data-stu-id="b4718-220">Network properties of VM-2 are changed after failover and is disconnected.</span></span> | <span data-ttu-id="b4718-221">VM-1의 연결이 끊김</span><span class="sxs-lookup"><span data-stu-id="b4718-221">VM-1 is disconnected.</span></span>
<span data-ttu-id="b4718-222">V M-2의 네트워크 속성은 장애 조치 후 변경 되 고 tooVMNetwork2-시카고와 연결된 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4718-222">Network properties of VM-2 are changed after failover and is connected tooVMNetwork2-Chicago.</span></span> | <span data-ttu-id="b4718-223">VMNetwork2-시카고가 매핑되지 않는 경우 VM-1의 연결이 끊김</span><span class="sxs-lookup"><span data-stu-id="b4718-223">If VMNetwork2-Chicago isn’t mapped, VM-1 will be disconnected.</span></span>
<span data-ttu-id="b4718-224">VMNetwork1-시카고의 네트워크 매핑이 변경됨</span><span class="sxs-lookup"><span data-stu-id="b4718-224">Network mapping of VMNetwork1-Chicago is changed.</span></span> | <span data-ttu-id="b4718-225">V M-1에 연결 된 toohello 매핑된 네트워크와 지금 tooVMNetwork1-시카고 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4718-225">VM-1 will be connected toohello network now mapped tooVMNetwork1-Chicago.</span></span>



## <a name="next-steps"></a><span data-ttu-id="b4718-226">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b4718-226">Next steps</span></span>

<span data-ttu-id="b4718-227">에 대 한 자세한 내용은 [hello 네트워크 인프라 계획](site-recovery-network-design.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b4718-227">Learn about [planning hello network infrastructure](site-recovery-network-design.md).</span></span>

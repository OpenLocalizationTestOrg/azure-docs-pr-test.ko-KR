---
title: "Azure Site Recovery를 사용하여 보조 VMM 사이트로의 Hyper-V 복제를 위한 네트워킹 계획 | Microsoft 문서"
description: "이 문서에서는 Azure Site Recovery를 사용하여 보조 System Center VMM 사이트로 Hyper-V VM을 복제할 때의 네트워크 계획에 대해 설명합니다."
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
ms.openlocfilehash: a1f3f6e6cba074647195e2b0cbcdc7b4f3dec475
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="step-3-plan-networking-for-hyper-v-vm-replication-to-a-secondary-vmm-site"></a><span data-ttu-id="2e1fc-103">3단계: 보조 VMM 사이트로의 Hyper-V VM 복제를 위한 네트워킹 계획</span><span class="sxs-lookup"><span data-stu-id="2e1fc-103">Step 3: Plan networking for Hyper-V VM replication to a secondary VMM site</span></span>

<span data-ttu-id="2e1fc-104">배포 필수 구성 요소를 검토한 후 이 문서의 내용에 따라 Azure Portal에서 [Azure Site Recovery](site-recovery-overview.md)를 사용하여 System Center VMM(Virtual Machine Manager) 클라우드에서 관리되는 Hyper-V VM(가상 컴퓨터)을 보조 사이트로 복제할 때의 네트워킹을 계획할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-104">After reviewing deployment prerequisites, read this article to plan networking when replicating Hyper-V virtual machines (VMs) managed in System Center Virtual Machine Manager (VMM) clouds, to a secondary site using [Azure Site Recovery](site-recovery-overview.md) in the Azure portal.</span></span> 

<span data-ttu-id="2e1fc-105">이 문서를 읽은 후에 하단 또는 [Azure Recovery Services 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)에서 의견을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-105">After reading this article, post any comments at the bottom, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="network-mapping-overview"></a><span data-ttu-id="2e1fc-106">네트워크 매핑 개요</span><span class="sxs-lookup"><span data-stu-id="2e1fc-106">Network mapping overview</span></span>

<span data-ttu-id="2e1fc-107">네트워크 매핑은 VMM에서 관리되는 Hyper-V VM을 보조 데이터 센터로 복제할 때 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-107">Network mapping is used when replicating Hyper-V VMs (managed in VMM) to a secondary datacenter.</span></span> <span data-ttu-id="2e1fc-108">네트워크 매핑은 원본 VMM 서버의 VM 네트워크와 대상 VMM 서버의 VM 네트워크 사이를 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-108">Network mapping maps between VM networks on a source VMM server, and VM networks on a target VMM server.</span></span> <span data-ttu-id="2e1fc-109">매핑은 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-109">Mapping does the following:</span></span>

- <span data-ttu-id="2e1fc-110">**네트워크 연결** - 장애 조치 후 VM을 적절한 네트워크에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-110">**Network connection**—Connects VMs to appropriate networks after failover.</span></span> <span data-ttu-id="2e1fc-111">복제본 VM은 원본 네트워크에 매핑되는 대상 네트워크에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-111">The replica VM will be connected to the target network that's mapped to the source network.</span></span>
- <span data-ttu-id="2e1fc-112">**최적 배치** - Hyper-V 호스트 서버에 복제본 VM을 가장 적합하게 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-112">**Optimal placement**—Optimally places the replica VMs on Hyper-V host servers.</span></span> <span data-ttu-id="2e1fc-113">복제본 VM은 매핑된 VM 네트워크에 액세스할 수 있는 호스트에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-113">Replica VMs are placed on hosts that can access the mapped VM networks.</span></span>
- <span data-ttu-id="2e1fc-114">**네트워크 매핑 안 함**- 네트워크 매핑을 구성하지 않으면 장애 조치 후 복제본 VM이 VM 네트워크에 연결되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-114">**No network mapping**—If you don’t configure network mapping, replica VMs won’t be connected to any VM networks after failover.</span></span>


### <a name="example"></a><span data-ttu-id="2e1fc-115">예제</span><span class="sxs-lookup"><span data-stu-id="2e1fc-115">Example</span></span>

<span data-ttu-id="2e1fc-116">이 메커니즘을 설명하는 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-116">Here’s an example to illustrate this mechanism.</span></span> <span data-ttu-id="2e1fc-117">뉴욕과 시카고 두 위치에 있는 조직을 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-117">Let’s take an organization with two locations in New York and Chicago.</span></span>

<span data-ttu-id="2e1fc-118">**위치**</span><span class="sxs-lookup"><span data-stu-id="2e1fc-118">**Location**</span></span> | <span data-ttu-id="2e1fc-119">**VMM 서버**</span><span class="sxs-lookup"><span data-stu-id="2e1fc-119">**VMM server**</span></span> | <span data-ttu-id="2e1fc-120">**VM 네트워크**</span><span class="sxs-lookup"><span data-stu-id="2e1fc-120">**VM networks**</span></span> | <span data-ttu-id="2e1fc-121">**다음으로 매핑**</span><span class="sxs-lookup"><span data-stu-id="2e1fc-121">**Mapped to**</span></span>
---|---|---|---
<span data-ttu-id="2e1fc-122">뉴욕</span><span class="sxs-lookup"><span data-stu-id="2e1fc-122">New York</span></span> | <span data-ttu-id="2e1fc-123">VMM-뉴욕</span><span class="sxs-lookup"><span data-stu-id="2e1fc-123">VMM-NewYork</span></span>| <span data-ttu-id="2e1fc-124">VMNetwork1-뉴욕</span><span class="sxs-lookup"><span data-stu-id="2e1fc-124">VMNetwork1-NewYork</span></span> | <span data-ttu-id="2e1fc-125">VMNetwork1-시카고로 매핑</span><span class="sxs-lookup"><span data-stu-id="2e1fc-125">Mapped to VMNetwork1-Chicago</span></span>
 |  | <span data-ttu-id="2e1fc-126">VMNetwork2-뉴욕</span><span class="sxs-lookup"><span data-stu-id="2e1fc-126">VMNetwork2-NewYork</span></span> | <span data-ttu-id="2e1fc-127">매핑되지 않음</span><span class="sxs-lookup"><span data-stu-id="2e1fc-127">Not mapped</span></span>
<span data-ttu-id="2e1fc-128">시카코</span><span class="sxs-lookup"><span data-stu-id="2e1fc-128">Chicago</span></span> | <span data-ttu-id="2e1fc-129">VMM-시카고</span><span class="sxs-lookup"><span data-stu-id="2e1fc-129">VMM-Chicago</span></span>| <span data-ttu-id="2e1fc-130">VMNetwork1-시카고</span><span class="sxs-lookup"><span data-stu-id="2e1fc-130">VMNetwork1-Chicago</span></span> | <span data-ttu-id="2e1fc-131">VMNetwork1-뉴욕으로 매핑</span><span class="sxs-lookup"><span data-stu-id="2e1fc-131">Mapped to VMNetwork1-NewYork</span></span>
 | | <span data-ttu-id="2e1fc-132">VMNetwork1-시카고</span><span class="sxs-lookup"><span data-stu-id="2e1fc-132">VMNetwork1-Chicago</span></span> | <span data-ttu-id="2e1fc-133">매핑되지 않음</span><span class="sxs-lookup"><span data-stu-id="2e1fc-133">Not mapped</span></span>

<span data-ttu-id="2e1fc-134">이 예제에서:</span><span class="sxs-lookup"><span data-stu-id="2e1fc-134">In this example:</span></span>

- <span data-ttu-id="2e1fc-135">VMNetwork1-뉴욕에 연결된 모든 가상 컴퓨터에 대한 복제 가상 컴퓨터를 만들면 VMNetwork1-시카고에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-135">When a replica virtual machine is created for any virtual machine that is connected to VMNetwork1-NewYork, it will be connected to VMNetwork1-Chicago.</span></span>
- <span data-ttu-id="2e1fc-136">VMNetwork2-뉴욕 또는 VMNetwork2-시카고에 대한 복제 가상 컴퓨터를 만들면 어떤 네트워크에도 연결되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-136">When a replica virtual machine is created for VMNetwork2-NewYork or VMNetwork2-Chicago, it will not be connected to any network.</span></span>

<span data-ttu-id="2e1fc-137">VMM 클라우드가 예제 조직 및 클라우드와 연결된 논리 네트워크에서 설정된 방식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-137">Here's how VMM clouds are set up in our example organization, and the logical networks associated with the clouds.</span></span>

#### <a name="cloud-protection-settings"></a><span data-ttu-id="2e1fc-138">클라우드 보호 설정</span><span class="sxs-lookup"><span data-stu-id="2e1fc-138">Cloud protection settings</span></span>

<span data-ttu-id="2e1fc-139">**보호된 클라우드**</span><span class="sxs-lookup"><span data-stu-id="2e1fc-139">**Protected cloud**</span></span> | <span data-ttu-id="2e1fc-140">**클라우드 보호**</span><span class="sxs-lookup"><span data-stu-id="2e1fc-140">**Protecting cloud**</span></span> | <span data-ttu-id="2e1fc-141">**논리 네트워크(뉴욕)**</span><span class="sxs-lookup"><span data-stu-id="2e1fc-141">**Logical network (New York)**</span></span>  
---|---|---
<span data-ttu-id="2e1fc-142">GoldCloud1</span><span class="sxs-lookup"><span data-stu-id="2e1fc-142">GoldCloud1</span></span> | <span data-ttu-id="2e1fc-143">GoldCloud2</span><span class="sxs-lookup"><span data-stu-id="2e1fc-143">GoldCloud2</span></span> |
<span data-ttu-id="2e1fc-144">SilverCloud1</span><span class="sxs-lookup"><span data-stu-id="2e1fc-144">SilverCloud1</span></span>| <span data-ttu-id="2e1fc-145">SilverCloud2</span><span class="sxs-lookup"><span data-stu-id="2e1fc-145">SilverCloud2</span></span> |
<span data-ttu-id="2e1fc-146">GoldCloud2</span><span class="sxs-lookup"><span data-stu-id="2e1fc-146">GoldCloud2</span></span> | <p><span data-ttu-id="2e1fc-147">해당 없음</span><span class="sxs-lookup"><span data-stu-id="2e1fc-147">NA</span></span></p><p></p> | <p><span data-ttu-id="2e1fc-148">LogicalNetwork1-뉴욕</span><span class="sxs-lookup"><span data-stu-id="2e1fc-148">LogicalNetwork1-NewYork</span></span></p><p><span data-ttu-id="2e1fc-149">LogicalNetwork1-시카고</span><span class="sxs-lookup"><span data-stu-id="2e1fc-149">LogicalNetwork1-Chicago</span></span></p>
<span data-ttu-id="2e1fc-150">SilverCloud2</span><span class="sxs-lookup"><span data-stu-id="2e1fc-150">SilverCloud2</span></span> | <p><span data-ttu-id="2e1fc-151">해당 없음</span><span class="sxs-lookup"><span data-stu-id="2e1fc-151">NA</span></span></p><p></p> | <p><span data-ttu-id="2e1fc-152">LogicalNetwork1-뉴욕</span><span class="sxs-lookup"><span data-stu-id="2e1fc-152">LogicalNetwork1-NewYork</span></span></p><p><span data-ttu-id="2e1fc-153">LogicalNetwork1-시카고</span><span class="sxs-lookup"><span data-stu-id="2e1fc-153">LogicalNetwork1-Chicago</span></span></p>

#### <a name="logical-and-vm-network-settings"></a><span data-ttu-id="2e1fc-154">논리 및 VM 네트워크 설정</span><span class="sxs-lookup"><span data-stu-id="2e1fc-154">Logical and VM network settings</span></span>

<span data-ttu-id="2e1fc-155">**위치**</span><span class="sxs-lookup"><span data-stu-id="2e1fc-155">**Location**</span></span> | <span data-ttu-id="2e1fc-156">**논리 네트워크**</span><span class="sxs-lookup"><span data-stu-id="2e1fc-156">**Logical network**</span></span> | <span data-ttu-id="2e1fc-157">**연결된 VM 네트워크**</span><span class="sxs-lookup"><span data-stu-id="2e1fc-157">**Associated VM network**</span></span>
---|---|---
<span data-ttu-id="2e1fc-158">뉴욕</span><span class="sxs-lookup"><span data-stu-id="2e1fc-158">New York</span></span> | <span data-ttu-id="2e1fc-159">LogicalNetwork1-뉴욕</span><span class="sxs-lookup"><span data-stu-id="2e1fc-159">LogicalNetwork1-NewYork</span></span> | <span data-ttu-id="2e1fc-160">VMNetwork1-뉴욕</span><span class="sxs-lookup"><span data-stu-id="2e1fc-160">VMNetwork1-NewYork</span></span>
<span data-ttu-id="2e1fc-161">시카코</span><span class="sxs-lookup"><span data-stu-id="2e1fc-161">Chicago</span></span> | <span data-ttu-id="2e1fc-162">LogicalNetwork1-시카고</span><span class="sxs-lookup"><span data-stu-id="2e1fc-162">LogicalNetwork1-Chicago</span></span> | <span data-ttu-id="2e1fc-163">VMNetwork1-시카고</span><span class="sxs-lookup"><span data-stu-id="2e1fc-163">VMNetwork1-Chicago</span></span>
 | <span data-ttu-id="2e1fc-164">LogicalNetwork2Chicago</span><span class="sxs-lookup"><span data-stu-id="2e1fc-164">LogicalNetwork2Chicago</span></span> | <span data-ttu-id="2e1fc-165">VMNetwork2-시카고</span><span class="sxs-lookup"><span data-stu-id="2e1fc-165">VMNetwork2-Chicago</span></span>

#### <a name="target-network-settings"></a><span data-ttu-id="2e1fc-166">대상 네트워크 설정</span><span class="sxs-lookup"><span data-stu-id="2e1fc-166">Target network settings</span></span>

<span data-ttu-id="2e1fc-167">이러한 설정에 따라 대상 VM 네트워크를 선택하면 다음 표에 사용 가능한 선택 항목이 보입니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-167">Based on these settings, when you select the target VM network, the following table shows the choices that will be available.</span></span>

<span data-ttu-id="2e1fc-168">**선택**</span><span class="sxs-lookup"><span data-stu-id="2e1fc-168">**Select**</span></span> | <span data-ttu-id="2e1fc-169">**보호된 클라우드**</span><span class="sxs-lookup"><span data-stu-id="2e1fc-169">**Protected cloud**</span></span> | <span data-ttu-id="2e1fc-170">**클라우드 보호**</span><span class="sxs-lookup"><span data-stu-id="2e1fc-170">**Protecting cloud**</span></span> | <span data-ttu-id="2e1fc-171">**사용 가능한 대상 네트워크**</span><span class="sxs-lookup"><span data-stu-id="2e1fc-171">**Target network available**</span></span>
---|---|---|---
<span data-ttu-id="2e1fc-172">VMNetwork1-시카고</span><span class="sxs-lookup"><span data-stu-id="2e1fc-172">VMNetwork1-Chicago</span></span> | <span data-ttu-id="2e1fc-173">SilverCloud1</span><span class="sxs-lookup"><span data-stu-id="2e1fc-173">SilverCloud1</span></span> | <span data-ttu-id="2e1fc-174">SilverCloud2</span><span class="sxs-lookup"><span data-stu-id="2e1fc-174">SilverCloud2</span></span> | <span data-ttu-id="2e1fc-175">사용 가능</span><span class="sxs-lookup"><span data-stu-id="2e1fc-175">Available</span></span>
 | <span data-ttu-id="2e1fc-176">GoldCloud1</span><span class="sxs-lookup"><span data-stu-id="2e1fc-176">GoldCloud1</span></span> | <span data-ttu-id="2e1fc-177">GoldCloud2</span><span class="sxs-lookup"><span data-stu-id="2e1fc-177">GoldCloud2</span></span> | <span data-ttu-id="2e1fc-178">사용 가능</span><span class="sxs-lookup"><span data-stu-id="2e1fc-178">Available</span></span>
<span data-ttu-id="2e1fc-179">VMNetwork2-시카고</span><span class="sxs-lookup"><span data-stu-id="2e1fc-179">VMNetwork2-Chicago</span></span> | <span data-ttu-id="2e1fc-180">SilverCloud1</span><span class="sxs-lookup"><span data-stu-id="2e1fc-180">SilverCloud1</span></span> | <span data-ttu-id="2e1fc-181">SilverCloud2</span><span class="sxs-lookup"><span data-stu-id="2e1fc-181">SilverCloud2</span></span> | <span data-ttu-id="2e1fc-182">사용할 수 없음</span><span class="sxs-lookup"><span data-stu-id="2e1fc-182">Not available</span></span>
 | <span data-ttu-id="2e1fc-183">GoldCloud1</span><span class="sxs-lookup"><span data-stu-id="2e1fc-183">GoldCloud1</span></span> | <span data-ttu-id="2e1fc-184">GoldCloud2</span><span class="sxs-lookup"><span data-stu-id="2e1fc-184">GoldCloud2</span></span> | <span data-ttu-id="2e1fc-185">사용 가능</span><span class="sxs-lookup"><span data-stu-id="2e1fc-185">Available</span></span>


<span data-ttu-id="2e1fc-186">대상 네트워크에 여러 서브넷이 있고 이 서브넷 중 하나의 이름이 원본 가상 컴퓨터가 있는 서브넷과 같으면 복제 가상 컴퓨터가 장애 조치(failover) 후에 대상 서브넷에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-186">If the target network has multiple subnets and one of those subnets has the same name as the subnet on which the source virtual machine is located, then the replica virtual machine will be connected to that target subnet after failover.</span></span> <span data-ttu-id="2e1fc-187">일치하는 이름을 가진 대상 서브넷이 없으면 가상 컴퓨터가 네트워크의 첫 번째 서브넷에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-187">If there’s no target subnet with a matching name, the virtual machine will be connected to the first subnet in the network.</span></span>


#### <a name="failback-behavior"></a><span data-ttu-id="2e1fc-188">장애 복구 동작</span><span class="sxs-lookup"><span data-stu-id="2e1fc-188">Failback behavior</span></span>

<span data-ttu-id="2e1fc-189">장애 복구(역방향 복제)의 경우 수행되는 작업을 보려면 다음 설정을 사용하여 VMNetwork1-뉴욕이 VMNetwork1-시카고에 매핑되어 있다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-189">To see what happens in the case of failback (reverse replication), let’s assume that VMNetwork1-NewYork is mapped to VMNetwork1-Chicago, with the following settings.</span></span>


<span data-ttu-id="2e1fc-190">**가상 컴퓨터**</span><span class="sxs-lookup"><span data-stu-id="2e1fc-190">**Virtual machine**</span></span> | <span data-ttu-id="2e1fc-191">**VM 네트워크에 연결**</span><span class="sxs-lookup"><span data-stu-id="2e1fc-191">**Connected to VM network**</span></span>
---|---
<span data-ttu-id="2e1fc-192">VM1</span><span class="sxs-lookup"><span data-stu-id="2e1fc-192">VM1</span></span> | <span data-ttu-id="2e1fc-193">VMNetwork1-네트워크</span><span class="sxs-lookup"><span data-stu-id="2e1fc-193">VMNetwork1-Network</span></span>
<span data-ttu-id="2e1fc-194">VM2(VM1의 복제)</span><span class="sxs-lookup"><span data-stu-id="2e1fc-194">VM2 (replica of VM1)</span></span> | <span data-ttu-id="2e1fc-195">VMNetwork1-시카고</span><span class="sxs-lookup"><span data-stu-id="2e1fc-195">VMNetwork1-Chicago</span></span>

<span data-ttu-id="2e1fc-196">이러한 설정을 사용하여 몇 가지 가능한 시나리오에서 발생하는 결과를 검토해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-196">With these settings, let's review what happens in a couple of possible scenarios.</span></span>

<span data-ttu-id="2e1fc-197">**시나리오**</span><span class="sxs-lookup"><span data-stu-id="2e1fc-197">**Scenario**</span></span> | <span data-ttu-id="2e1fc-198">**결과**</span><span class="sxs-lookup"><span data-stu-id="2e1fc-198">**Outcome**</span></span>
---|---
<span data-ttu-id="2e1fc-199">장애 조치(failover) 후 VM-2의 네트워크 속성이 변경되지 않음</span><span class="sxs-lookup"><span data-stu-id="2e1fc-199">No change in the network properties of VM-2 after failover.</span></span> | <span data-ttu-id="2e1fc-200">VM-1에 원본 네트워크에 연결된 상태로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-200">VM-1 remains connected to the source network.</span></span>
<span data-ttu-id="2e1fc-201">장애 조치(failover) 후 VM-2의 네트워크 속성이 변경되고 연결이 끊김</span><span class="sxs-lookup"><span data-stu-id="2e1fc-201">Network properties of VM-2 are changed after failover and is disconnected.</span></span> | <span data-ttu-id="2e1fc-202">VM-1의 연결이 끊김</span><span class="sxs-lookup"><span data-stu-id="2e1fc-202">VM-1 is disconnected.</span></span>
<span data-ttu-id="2e1fc-203">장애 조치(failover) 후 VM-2의 네트워크 속성이 변경되고 VMNetwork2-시카고에 연결됨</span><span class="sxs-lookup"><span data-stu-id="2e1fc-203">Network properties of VM-2 are changed after failover and is connected to VMNetwork2-Chicago.</span></span> | <span data-ttu-id="2e1fc-204">VMNetwork2-시카고가 매핑되지 않는 경우 VM-1의 연결이 끊김</span><span class="sxs-lookup"><span data-stu-id="2e1fc-204">If VMNetwork2-Chicago isn’t mapped, VM-1 will be disconnected.</span></span>
<span data-ttu-id="2e1fc-205">VMNetwork1-시카고의 네트워크 매핑이 변경됨</span><span class="sxs-lookup"><span data-stu-id="2e1fc-205">Network mapping of VMNetwork1-Chicago is changed.</span></span> | <span data-ttu-id="2e1fc-206">VM-1이 현재 VMNetwork1-시카고에 매핑된 네트워크에 연결됨</span><span class="sxs-lookup"><span data-stu-id="2e1fc-206">VM-1 will be connected to the network now mapped to VMNetwork1-Chicago.</span></span>



## <a name="prepare-for-network-mapping"></a><span data-ttu-id="2e1fc-207">네트워크 매핑을 준비</span><span class="sxs-lookup"><span data-stu-id="2e1fc-207">Prepare for network mapping</span></span>

1. <span data-ttu-id="2e1fc-208">원본 및 대상 VMM 서버에는 원본 및 대상 클라우드와 연결된 논리 네트워크가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-208">On the source and target VMM servers, you should have a logical network associated with the source and target clouds.</span></span> 
2. <span data-ttu-id="2e1fc-209">원본 및 대상 서버는 논리 네트워크에 연결된 VM 네트워크가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-209">In the source and target servers, you should have a VM network linked to the logical network.</span></span>
3. <span data-ttu-id="2e1fc-210">원본 위치에 있는 Hyper-V 호스트의 VM은 원본 VM 네트워크에 연결되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-210">VMs on Hyper-V hosts in the source location should be linked to the source VM network.</span></span> <span data-ttu-id="2e1fc-211">단일 VMM 서버만 사용하는 경우에는 같은 서버의 VM 네트워크 간에 매핑을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-211">If you're only using a single VMM server, you can configure mapping between VM networks on the same server.</span></span>

<span data-ttu-id="2e1fc-212">Site Recovery를 배포하는 동안 네트워크 매핑을 설정하면 다음 작업이 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-212">Here's what happens when you set up network mapping during Site Recovery deployment:</span></span>

- <span data-ttu-id="2e1fc-213">네트워크 매핑을 설정하고 대상 VM 네트워크를 선택하면 대상 클라우드에서 사용 가능한 대상 VM 네트워크와 함께 원본 VM 네트워크를 사용하는 VMM 원본 클라우드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-213">When you set up network mapping and select a target VM network, the VMM source clouds that use the source VM network will be displayed, along with the available target VM networks on the target clouds.</span></span>
- - <span data-ttu-id="2e1fc-214">매핑이 올바르게 구성되었고 복제를 설정한 경우 원본 VM이 원본 VM 네트워크에 연결되며 대상 위치의 복제본은 매핑된 해당 VM 네트워크에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-214">When mapping is configured correctly and replication is enabled, a source VM will be connected to its source VM network, and its replica at the target location will be connected to its mapped VM network.</span></span>
- <span data-ttu-id="2e1fc-215">대상 네트워크에 여러 서브넷이 있고 이 서브넷 중 하나의 이름이 원본 가상 컴퓨터가 있는 서브넷과 같으면 복제 가상 컴퓨터가 장애 조치(failover) 후에 대상 서브넷에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-215">If the target network has multiple subnets, and one of those subnets has the same name as the subnet on which the source virtual machine is located, then the replica virtual machine will be connected to that target subnet after failover.</span></span> <span data-ttu-id="2e1fc-216">이름이 일치하는 대상 서브넷이 없으면 VM은 네트워크의 첫 번째 서브넷에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-216">If there’s no target subnet with a matching name, the VM will be connected to the first subnet in the network.</span></span>

## <a name="connect-to-vms-after-failover"></a><span data-ttu-id="2e1fc-217">장애 조치(failover) 후 VM에 연결</span><span class="sxs-lookup"><span data-stu-id="2e1fc-217">Connect to VMs after failover</span></span>

<span data-ttu-id="2e1fc-218">복제 및 장애 조치(failover) 전략을 계획할 때 고려해야 하는 중요한 요소 중 하나는 장애 조치(failover) 이후 복제본에 연결할 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-218">When planning your replication and failover strategy, one of the key questions is how to connect to the replica after failover.</span></span> <span data-ttu-id="2e1fc-219">다음의 두 가지 방법 중에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-219">There are a couple of choices:</span></span> 

- <span data-ttu-id="2e1fc-220">**다른 IP 주소 사용**: 복제된 Azure VM에 대해 다른 IP 주소를 사용하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-220">**Use a different IP address**: You can select to use a different IP address for the replicated VM.</span></span> <span data-ttu-id="2e1fc-221">이 시나리오에서 VM은 장애 조치(failover) 후에 새 IP 주소를 갖게 되며 DNS 업데이트가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-221">In this scenario the VM gets a new IP address after failover, and a DNS update is required.</span></span>
- <span data-ttu-id="2e1fc-222">**동일한 IP 주소 유지**: 복제본 VM에 대해 동일한 IP 주소를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-222">**Retain the same IP address**: You might want to use the same IP address for the replica VM.</span></span> <span data-ttu-id="2e1fc-223">동일한 IP 주소를 유지하면 장애 조치(failover) 후 네트워크 관련 문제가 줄어들어 복구가 간소화됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-223">Keeping the same IP addresses simplifies the recovery by reducing network related issues after failover.</span></span> 

## <a name="retain-ip-addresses"></a><span data-ttu-id="2e1fc-224">IP 주소 유지</span><span class="sxs-lookup"><span data-stu-id="2e1fc-224">Retain IP addresses</span></span>

<span data-ttu-id="2e1fc-225">보조 사이트로의 장애 조치(failover) 이후 기본 사이트의 IP 주소를 유지하려는 경우 전체 서브넷 장애 조치(failover)를 수행하고 IP 주소의 새 위치를 나타내도록 경로를 업데이트하거나, 기본 사이트와 복구 사이트 간에 확대 서브넷을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-225">If you want to retain the IP addresses from the primary site after failover to the secondary site, you can do a full subnet failover, and update routes to indicate the new location of the IP addresses, or alternative deploy a stretched subnet between the primary and the recovery sites.</span></span>

### <a name="stretched-subnet"></a><span data-ttu-id="2e1fc-226">늘어난 서브넷</span><span class="sxs-lookup"><span data-stu-id="2e1fc-226">Stretched subnet</span></span>

<span data-ttu-id="2e1fc-227">확대 서브넷에서는 기본 사이트와 보조 사이트 둘 다에서 서브넷을 동시에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-227">In a stretched subnet, the subnet is available simultaneously in both the primary and secondary site.</span></span> <span data-ttu-id="2e1fc-228">서버와 해당 IP(계층 3) 구성을 보조 사이트로 이동하는 경우 네트워크는 새 위치로 트래픽을 자동 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-228">If you move a server and its IP (Layer 3) configuration to the secondary site, the network will route the traffic to the new location automatically.</span></span> 

<span data-ttu-id="2e1fc-229">계층 2(데이터 링크 계층) 측면을 고려하면 확대 VLAN을 관리할 수 있는 네트워킹 장비가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-229">From a Layer 2 (data link layer) perspective, you need networking equipment that can manage a stretched VLAN.</span></span> <span data-ttu-id="2e1fc-230">또한 VLAN을 확대하면 잠재적 장애 도메인이 두 사이트로 모두 확장되므로 단일 실패 지점이 발생하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-230">In addition, by stretching the VLAN, the potential fault domain extends to both sites, essentially becoming a single point of failure.</span></span> <span data-ttu-id="2e1fc-231">이러한 현상이 발생할 가능성은 거의 없기는 하지만, 브로드캐스트 스톰이 시작해서 격리되지 못하게 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-231">While this is an unlikely, it could happen that a broadcast storm started and cannot be isolated.</span></span> 


### <a name="subnet-failover"></a><span data-ttu-id="2e1fc-232">서브넷 장애 조치(failover)</span><span class="sxs-lookup"><span data-stu-id="2e1fc-232">Subnet failover</span></span>

<span data-ttu-id="2e1fc-233">서브넷 장애 조치(failover)를 실행하면 서브넷을 실제로 확대하지 않고도 확대 서브넷의 이점을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-233">You can run a subnet failover to obtain the benefits of the stretched subnet, without actually stretching it.</span></span> <span data-ttu-id="2e1fc-234">이 솔루션에서는 원본 또는 대상 사이트 중 하나에서 서브넷을 사용할 수 있으며 두 사이트에서 동시에 사용할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-234">In this solution, a subnet will be available in the source or target site, but not at both simultaneously.</span></span> <span data-ttu-id="2e1fc-235">장애 조치(failover) 시 IP 주소 공간을 유지 관리하기 위해 라우터 인프라에 대해 프로그래밍 방식으로 정렬하여 한 사이트에서 다른 사이트로 서브넷을 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-235">To maintain the IP address space in the event of a failover, you can programmatically arrange for the router infrastructure to move the subnets from one site to another.</span></span> <span data-ttu-id="2e1fc-236">장애 조치(failover) 후에는 서브넷이 연결된 VM과 함께 이동됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-236">After when failover occurs, subnets would move with the associated VMs.</span></span> <span data-ttu-id="2e1fc-237">주요 단점은 오류 발생 시 전체 서브넷을 이동해야 한다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-237">The main drawback is that in the event of a failure, you have to move the whole subnet.</span></span>

### <a name="example"></a><span data-ttu-id="2e1fc-238">예제</span><span class="sxs-lookup"><span data-stu-id="2e1fc-238">Example</span></span>

<span data-ttu-id="2e1fc-239">전체 서브넷 장애 조치(failover)의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-239">Here's an example of complete subnet failover.</span></span> <span data-ttu-id="2e1fc-240">주 사이트에 서브넷 192.168.1.0/24에서 실행되는 응용 프로그램이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-240">The primary site has applications running in subnet 192.168.1.0/24.</span></span> <span data-ttu-id="2e1fc-241">장애 조치(failover) 시 이 서브넷의 모든 VM은 보조 사이트로 장애 조치(failover)되며 IP 주소는 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-241">At failover, all the VMs in this subnet are failed over to the secondary site, and retain their IP addresses.</span></span> <span data-ttu-id="2e1fc-242">서브넷 192.168.1.0/24에 속하는 모든 VM(가상 컴퓨터)이 보조 사이트로 이동했음을 반영하여 경로를 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-242">Routes need to be modified to reflect the fact that all the VM virtual machines belonging to subnet 192.168.1.0/24 have now moved to the secondary site.</span></span>

<span data-ttu-id="2e1fc-243">다음 그림에는 장애 조치(failover) 전과 후의 서브넷이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-243">The following graphics show the subnets before and after failover:</span></span>

- <span data-ttu-id="2e1fc-244">서브넷 192.168.0.1/24는 장애 조치(failover) 전에는 원본 사이트에서 활성화되며 장애 조치(failover) 후에는 보조 사이트에서 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-244">Before failover, subnet 192.168.0.1/24 is active on the source site, become active on the secondary site after failover.</span></span>
- <span data-ttu-id="2e1fc-245">기본 사이트와 복구 사이트, 세 번째 사이트와 기본 사이트, 그리고 세 번째 사이트와 복구 사이트 간의 경로를 적절하게 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-245">The routes between primary site and recovery site, third site and primary site, and third site and recovery site will have to be appropriately modified.</span></span>

<span data-ttu-id="2e1fc-246">**장애 조치(failover) 전**</span><span class="sxs-lookup"><span data-stu-id="2e1fc-246">**Before failover**</span></span>

![장애 조치(failover) 전](./media/vmm-to-vmm-walkthrough-network/network-design2.png)

<span data-ttu-id="2e1fc-248">**장애 조치(failover) 후**</span><span class="sxs-lookup"><span data-stu-id="2e1fc-248">**After failover**</span></span>

![장애 조치(failover) 후](./media/vmm-to-vmm-walkthrough-network/network-design3.png)

<span data-ttu-id="2e1fc-250">장애 조치(failover) 후에는 다음 작업이 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-250">After failover, here's what happens:</span></span>

- <span data-ttu-id="2e1fc-251">Site Recovery가 각 VMM 인스턴스에 대해 관련 네트워크의 고정 IP 주소 풀에서 VM의 각 네트워크 인터페이스에 대한 IP 주소를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-251">Site Recovery allocates an IP address for each network interface on the VM, from the static IP address pool in the relevant network, for each VMM instance.</span></span>
- <span data-ttu-id="2e1fc-252">보조 사이트의 IP 주소 풀이 원본 사이트의 풀과 같은 경우 Site Recovery는 복제본 VM에 원본 VM의 동일 IP 주소를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-252">If the IP address pool in the secondary site is the same as that on the source site, Site Recovery allocates the same IP address (of the source VM) to the replica VM.</span></span> <span data-ttu-id="2e1fc-253">IP 주소는 VMM에서 예약되지만 Hyper-V 호스트에서 장애 조치(failover) IP 주소로 설정되지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-253">The IP address is reserved in VMM, but it isn't set as the failover IP address on the Hyper-V host.</span></span> <span data-ttu-id="2e1fc-254">Hyper-V 호스트의 장애 조치(failover) IP 주소는 장애 조치(failover) 직전에 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-254">The failover IP address on a Hyper-v host is set just before the failover.</span></span>
- <span data-ttu-id="2e1fc-255">동일한 IP 주소를 사용할 수 없는 경우 Site Recovery가 풀에서 사용 가능한 다른 IP 주소를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-255">If the same IP address isn't available, Site Recovery allocates another available IP address from the pool.</span></span>
- <span data-ttu-id="2e1fc-256">VM이 DHCP를 사용하는 경우 Site Recovery는 IP 주소를 관리하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-256">If VMs use DHCP, Site Recovery doesn't manage the IP addresses.</span></span> <span data-ttu-id="2e1fc-257">보조 사이트의 DHCP 서버가 원본 사이트와 동일한 범위에서 주소를 할당할 수 있는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-257">You need to check that the DHCP server on the secondary site can allocate address from the same range as the source site.</span></span>

### <a name="validate-the-ip-address"></a><span data-ttu-id="2e1fc-258">IP 주소 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="2e1fc-258">Validate the IP address</span></span>

<span data-ttu-id="2e1fc-259">VM을 보호하도록 설정한 후에는 다음 샘플 스크립트를 사용하여 VM에 할당된 주소를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-259">After you enable protection for a VM, you can use following sample script to verify the address assigned to the VM.</span></span> <span data-ttu-id="2e1fc-260">동일한 IP 주소가 장애 조치(failover) IP 주소로 설정되고 장애 조치(failover) 시 VM에 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-260">The same IP address will be set as the failover IP address, and assigned to the VM at the time of failover:</span></span>

    ```
    $vm = Get-SCVirtualMachine -Name <VM_NAME>
    $na = $vm[0].VirtualNetworkAdapters>
    $ip = Get-SCIPAddress -GrantToObjectID $na[0].id
    $ip.address 
    ```

## <a name="changing-ip-addresses"></a><span data-ttu-id="2e1fc-261">IP 주소 변경</span><span class="sxs-lookup"><span data-stu-id="2e1fc-261">Changing IP addresses</span></span>

<span data-ttu-id="2e1fc-262">이 시나리오에서는 장애 조치(failover)되는 VM의 IP 주소가 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-262">In this scenario, the IP addresses of VMs that fail over are changed.</span></span> <span data-ttu-id="2e1fc-263">이 솔루션의 단점은 유지 관리가 필요하다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-263">The drawback of this solution is the maintenance required.</span></span> <span data-ttu-id="2e1fc-264">일반적으로는 복제본 VM이 시작된 후에 DNS가 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-264">Typically, DNS will be updated after replica VMs start.</span></span> <span data-ttu-id="2e1fc-265">그러므로 네트워크에서 DNS 항목을 변경하거나 클러스터로 만들어야 할 수 있으며 캐시된 항목을 업데이트해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-265">DNS entries might need to be changed or fluster in thenetwork, and cached entries updated.</span></span> <span data-ttu-id="2e1fc-266">이로 인해 가동 중지 시간이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-266">This can result in downtime.</span></span> <span data-ttu-id="2e1fc-267">다음 방법을 통해 가동 중지 시간을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-267">Downtime can be mitigated as follows:</span></span>

- <span data-ttu-id="2e1fc-268">인트라넷 응용 프로그램의 경우 낮은 TTL 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-268">Use low TTL values for intranet applications.</span></span>
- <span data-ttu-id="2e1fc-269">업데이트가 제때 수행되도록 Site Recovery 복구 계획에서 다음 스크립트를 사용하여 DNS 서버를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-269">Use the following script in a Site Recovery recovery plan, to update the DNS server to ensure a timely update.</span></span> <span data-ttu-id="2e1fc-270">동적 DNS 등록을 사용하는 경우에는 이 스크립트를 사용할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-270">You don't need the script if you use dynamic DNS registration.</span></span>

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
    
### <a name="example"></a><span data-ttu-id="2e1fc-271">예제</span><span class="sxs-lookup"><span data-stu-id="2e1fc-271">Example</span></span> 

<span data-ttu-id="2e1fc-272">기본 사이트와 복구 사이트에서 서로 다른 IP 주소를 사용하려는 시나리오를 예로 들어 보겠습니다. 이 예에서는 기본 사이트와 보조 사이트의 IP 주소가 다릅니다. 그리고 기본 사이트 또는 복구 사이트에서 호스트되는 응용 프로그램이 액세스할 수 있는 세 번째 사이트도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-272">Let's look at a scenario in which you're planning to use different IP addresses across the primary and the recovery sites.In this example we have different IP addresses across primary and secondary sites, and there;s a third site from which applications hosted on the primary or recovery site can be accessed.</span></span>

- <span data-ttu-id="2e1fc-273">앱은 장애 조치(failover) 전에는 기본 사이트의 서브넷 192.168.1.0/24에서 호스트되며, 장애 조치(failover) 후에는 서브넷 172.16.1.0/24에 포함되도록 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-273">Before failover, apps are hosted subnet 192.168.1.0/24 on the primary site, and are configured to be in subnet 172.16.1.0/24 on the secondary site after a failover.</span></span>
- <span data-ttu-id="2e1fc-274">세 사이트 모두 서로 액세스할 수 있도록 VPN 연결/네트워크 라우팅이 적절하게 구성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-274">VPN connections/network routes have been configured appropriately so that all three sites can access each other.</span></span>
- <span data-ttu-id="2e1fc-275">장애 조치(failover) 후에는 앱이 복구 서브넷에서 복구됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-275">After failover, apps will be restored in the recovery subnet.</span></span> <span data-ttu-id="2e1fc-276">이 시나리오에서는 전체 서브넷을 장애 조치(failover)할 필요가 없으며 VPN 또는 네트워크 경로를 다시 구성하기 위해 변경해야 하는 사항이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-276">In this scenario there's no need to fail over the entire subnet, and no changes are needed to reconfigure VPN or network routes.</span></span> <span data-ttu-id="2e1fc-277">장애 조치(failover) 및 일부 DNS 업데이트를 수행하면 응용 프로그램이 액세스 가능한 상태로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-277">The failover, and some DNS updates, ensure that applications remain accessible.</span></span>
- <span data-ttu-id="2e1fc-278">DNS가 동적 업데이트를 허용하도록 구성된 경우 장애 조치(failover) 후 시작되는 VM은 새 IP 주소를 사용하여 자체 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-278">If DNS is configured to allow dynamic updates, then the VMs will register themselves using the new IP address, when they start after failover.</span></span>

<span data-ttu-id="2e1fc-279">**장애 조치(failover) 전**</span><span class="sxs-lookup"><span data-stu-id="2e1fc-279">**Before failover**</span></span>

![다른 IP - 장애 조치 전](./media/vmm-to-vmm-walkthrough-network/network-design10.png)

<span data-ttu-id="2e1fc-281">**장애 조치(failover) 후**</span><span class="sxs-lookup"><span data-stu-id="2e1fc-281">**After failover**</span></span>

![다른 IP - 장애 조치 후](./media/vmm-to-vmm-walkthrough-network/network-design11.png)



## <a name="next-steps"></a><span data-ttu-id="2e1fc-283">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2e1fc-283">Next steps</span></span>

<span data-ttu-id="2e1fc-284">[4단계: VMM 및 Hyper-V 준비](vmm-to-vmm-walkthrough-vmm-hyper-v.md)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="2e1fc-284">Go to [Step 4: Prepare VMM and Hyper-V](vmm-to-vmm-walkthrough-vmm-hyper-v.md).</span></span>



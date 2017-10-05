---
title: "Azure Site Recovery를 사용하여 Azure로의 Hyper-V(System Center VMM 포함) 복제를 위한 네트워킹 계획 | Microsoft 문서"
description: "이 문서에서는 Azure로 Hyper-V VM(VMM 포함)을 복제하는 데 필요한 네트워킹 계획을 설명합니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 41c3c83e-6b1a-496a-8179-498c552ef0c7
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: ef87cd82b021e40f0da05142878daff245cd9c62
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/29/2017
---
# <a name="step-4-plan-networking-for-hyper-v-with-vmm-to-azure-replication"></a><span data-ttu-id="f97cb-103">4단계: Azure로의 Hyper-V(VMM 포함) 복제를 위한 네트워킹 계획</span><span class="sxs-lookup"><span data-stu-id="f97cb-103">Step 4: Plan networking for Hyper-V (with VMM) to Azure replication</span></span>

<span data-ttu-id="f97cb-104">전체 배포를 진행하려는 경우 [용량 계획](vmm-to-azure-walkthrough-capacity.md)을 수행한 후 이 문서의 내용을 참조하여 [Azure Site Recovery](site-recovery-overview.md) 서비스를 사용해 System Center Virtual Machine Manager(VMM) 클라우드의 온-프레미스 Hyper-V VM을 Azure로 복제할 때의 네트워크 계획 고려 사항에 대해 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f97cb-104">After performing [capacity planning](vmm-to-azure-walkthrough-capacity.md) (if you're doing a full deployment), read this article to learn about network planning considerations when replicating on-premises Hyper-V VMs in System Center Virtual Machine Manager (VMM) clouds to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="f97cb-105">이 문서의 하단에서 의견을 게시하거나 [Azure Recovery Services 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)에서 질문하세요.</span><span class="sxs-lookup"><span data-stu-id="f97cb-105">Post any comments at the bottom of this article, or ask questions in the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="network-mapping-for-replication-to-azure"></a><span data-ttu-id="f97cb-106">Azure로의 복제를 위한 네트워크 매핑</span><span class="sxs-lookup"><span data-stu-id="f97cb-106">Network mapping for replication to Azure</span></span>

<span data-ttu-id="f97cb-107">네트워크 매핑은 Hyper-V VM(VMM에서 관리됨)을 Azure로 복제할 때 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f97cb-107">Network mapping is used when replicating Hyper-V VMs (managed in VMM) to Azure.</span></span> <span data-ttu-id="f97cb-108">네트워크 매핑은 원본 VMM 서버의 VM 네트워크와 대상 Azure 네트워크 사이를 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="f97cb-108">Network mapping maps between VM networks on a source VMM server, and target Azure networks.</span></span> <span data-ttu-id="f97cb-109">매핑은 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f97cb-109">Mapping does the following:</span></span>

- <span data-ttu-id="f97cb-110">**네트워크 연결** - 장애 조치(failover) 후에 복제된 모든 Azure VM이 매핑된 Azure 네트워크에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="f97cb-110">**Network connection**—After failover, all replicated Azure VMs are connected to the mapped Azure network.</span></span> <span data-ttu-id="f97cb-111">동일한 네트워크에서 장애 조치되는 모든 컴퓨터가 서로 연결될 수 있으며, 이는 서로 다른 복구 계획에서 장애 조치된 경우에도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="f97cb-111">All machines which fail over on the same network can connect to each other, even if they failed over in different recovery plans.</span></span>
- <span data-ttu-id="f97cb-112">**네트워크 게이트웨이** - 대상 Azure 네트워크에 네트워크 게이트웨이가 설정되어 있으면 VM은 매핑된 온-프레미스 네트워크의 다른 온-프레미스 가상 컴퓨터에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f97cb-112">**Network gateway**—If a network gateway is set up on the target Azure network, VMs can connect to other on-premises virtual machines in the mapped on-premised network.</span></span>

### <a name="prepare-vmm-for-network-mapping"></a><span data-ttu-id="f97cb-113">네트워크 매핑용 VMM 준비</span><span class="sxs-lookup"><span data-stu-id="f97cb-113">Prepare VMM for network mapping</span></span>

<span data-ttu-id="f97cb-114">다음과 같이 네트워크 매핑용 VMM을 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="f97cb-114">Prepare VMM for network mapping as follows:</span></span>

1. <span data-ttu-id="f97cb-115">VMM이 없으면 Hyper-V 호스트가 있는 클라우드와 연결된 [VMM 논리 네트워크](https://docs.microsoft.com/system-center/vmm/network-logical)를 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="f97cb-115">If you don't have one, prepare a [VMM logical network](https://docs.microsoft.com/system-center/vmm/network-logical) that's associated with the cloud in which the Hyper-V hosts are located.</span></span>
2. <span data-ttu-id="f97cb-116">VMM이 없으면 위에서 준비한 논리 네트워크에 연결된 [VM 네트워크](https://docs.microsoft.com/system-center/vmm/network-virtual)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f97cb-116">If you don't have one, created a [VM network](https://docs.microsoft.com/system-center/vmm/network-virtual) linked to the logical network you prepared above.</span></span>
3. <span data-ttu-id="f97cb-117">VMM 클라우드의 Hyper-V 호스트 서버/클러스터에 있는 VM을 VM 네트워크에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="f97cb-117">Connect VMs on the Hyper-V host server/cluster in the VMM cloud, to the VM network.</span></span>

 
<span data-ttu-id="f97cb-118">다음 사항에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="f97cb-118">Note that:</span></span> 
- <span data-ttu-id="f97cb-119">원본 VM 네트워크에 추가된 새 VM은 복제된 후에 매핑된 Azure 네트워크에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="f97cb-119">New VMs are added to the source VM network are connected to the mapped Azure network when replication occurs.</span></span>
- <span data-ttu-id="f97cb-120">대상 네트워크에 여러 서브넷이 있고 이 서브넷 중 하나의 이름이 원본 가상 컴퓨터가 있는 서브넷과 같으면 복제 가상 컴퓨터가 장애 조치(failover) 후에 대상 서브넷에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="f97cb-120">If the target network has multiple subnets, and one of those subnets has the same name as subnet on which the source virtual machine is located, then the replica virtual machine connects to that target subnet after failover.</span></span>
- <span data-ttu-id="f97cb-121">일치하는 이름을 가진 대상 서브넷이 없으면 가상 컴퓨터가 네트워크의 첫 번째 서브넷에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="f97cb-121">If there’s no target subnet with a matching name, the virtual machine connects to the first subnet in the network.</span></span>
- <span data-ttu-id="f97cb-122">시나리오를 배포하면서 Azure 네트워크를 준비하고 네트워크 매핑을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f97cb-122">You prepare an Azure network, and set up network mappings, as you deploy the scenario.</span></span>

## <a name="connecting-to-azure-vms-after-failover"></a><span data-ttu-id="f97cb-123">장애 조치(failover) 후 Azure VM에 연결</span><span class="sxs-lookup"><span data-stu-id="f97cb-123">Connecting to Azure VMs after failover</span></span>

<span data-ttu-id="f97cb-124">복제 및 장애 조치(failover) 전략을 계획할 경우 주요 질문 중 하나는 장애 조치(failover) 후에 Azure VM에 어떻게 연결하는가에 대한 질문입니다.</span><span class="sxs-lookup"><span data-stu-id="f97cb-124">When planning your replication and failover strategy, one of the key questions is how to connect to the Azure VM after failover.</span></span> <span data-ttu-id="f97cb-125">복제본 Azure VM에 대한 네트워크 전략을 설계할 때 몇 가지 선택 항목이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f97cb-125">There are a couple of choices when designing your network strategy for replica Azure VMs:</span></span>

- <span data-ttu-id="f97cb-126">**다른 IP 주소 사용**: 복제된 Azure VM 네트워크에 다른 IP 주소 범위를 사용하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f97cb-126">**Use a different IP address**: You can select to use a different IP address range for the replicated Azure VM network.</span></span> <span data-ttu-id="f97cb-127">이 시나리오에서 VM은 장애 조치(failover) 후에 새 IP 주소를 갖게 되며 DNS 업데이트가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f97cb-127">In this scenario the VM gets a new IP address after failover, and a DNS update is required.</span></span>
- <span data-ttu-id="f97cb-128">**동일한 IP 주소 유지**: 기본 온-프레미스 네트워크에 있는 것과 동일한 IP 주소 범위를 장애 조치(failover) 후 Azure 네트워크에 대해 사용하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="f97cb-128">**Retain the same IP address**: You might want to use the same IP address range as that in your primary on-premises network, for the Azure network after failover.</span></span>  <span data-ttu-id="f97cb-129">동일한 IP 주소를 유지하면 장애 조치(failover) 후 네트워크 관련 문제가 줄어들어 복구가 간소화됩니다.</span><span class="sxs-lookup"><span data-stu-id="f97cb-129">Keeping the same IP addresses simplifies the recovery by reducing network related issues after failover.</span></span> <span data-ttu-id="f97cb-130">그러나 Azure에 복제하는 경우 장애 조치 후에 경로를 IP 주소의 새 위치로 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f97cb-130">However, when you're replicating to Azure, you will need to update routes with the new location of the IP addresses after failover.</span></span>


## <a name="retain-ip-addresses"></a><span data-ttu-id="f97cb-131">IP 주소 유지</span><span class="sxs-lookup"><span data-stu-id="f97cb-131">Retain IP addresses</span></span>

<span data-ttu-id="f97cb-132">Site Recovery는 Azure에 장애 조치할 경우 서브넷 장애 조치를 사용하여 고정 IP 주소를 유지하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f97cb-132">Site Recovery provides the capability to retain fixed IP addresses when failing over to Azure, with a subnet failover.</span></span>

<span data-ttu-id="f97cb-133">서브넷 장애 조치를 사용하는 경우 특정 서브넷은 사이트 1 또는 사이트 2에 있으며 두 사이트에 동시에 존재하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f97cb-133">With subnet failover, a specific subnet is present at Site 1 or Site 2, but never at both sites simultaneously.</span></span> <span data-ttu-id="f97cb-134">장애 조치(failover) 시 IP 주소 공간을 유지 관리하기 위해 라우터 인프라에 대해 프로그래밍 방식으로 정렬하여 한 사이트에서 다른 사이트로 서브넷을 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f97cb-134">In order to maintain the IP address space in the event of a failover, you programmatically arrange for the router infrastructure to move the subnets from one site to another.</span></span> <span data-ttu-id="f97cb-135">장애 조치(failover) 중에 서브넷은 연결되어 있는 보호된 VM과 함께 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f97cb-135">During failover, the subnets move with the associated protected VMs.</span></span> <span data-ttu-id="f97cb-136">주요 단점은 오류 발생 시 전체 서브넷을 이동해야 한다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="f97cb-136">The main drawback is that in the event of a failure, you have to move the whole subnet.</span></span>



### <a name="failover-example"></a><span data-ttu-id="f97cb-137">장애 조치 예제</span><span class="sxs-lookup"><span data-stu-id="f97cb-137">Failover example</span></span>

<span data-ttu-id="f97cb-138">Azure로 장애 조치(failover)에 관한 예제를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f97cb-138">Let's look at an example for failover to Azure.</span></span>

- <span data-ttu-id="f97cb-139">Woodgrove Bank라는 가상의 회사에는 비즈니스 앱을 호스팅하는 온-프레미스 인프라가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f97cb-139">A ficticious company, Woodgrove Bank, has an on-premises infrastructure hosting their business apps.</span></span> <span data-ttu-id="f97cb-140">모바일 응용 프로그램은 Azure에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="f97cb-140">Their mobile applications are hosted on Azure.</span></span>
- <span data-ttu-id="f97cb-141">Azure 및 온-프레미스 서버에서 Woodgrove Bank VM 간의 연결은 온-프레미스 에지 네트워크와 Azure 가상 네트워크 간에 있는 사이트 간(VPN) 연결에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="f97cb-141">Connectivity between Woodgrove Bank VMs in Azure and on-premises servers is provided by a site-to-site (VPN) connection between the on-premises edge network and the Azure virtual network.</span></span>
- <span data-ttu-id="f97cb-142">이 VPN은 Azure에서 회사의 가상 네트워크가 온-프레미스 네트워크의 확장으로 나타난다는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="f97cb-142">This VPN means that the company's virtual network in Azure appears as an extension of their on-premises network.</span></span>
- <span data-ttu-id="f97cb-143">Woodgrove는 Site Recovery를 사용하여 온-프레미스 워크로드를 Azure로 복제하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="f97cb-143">Woodgrove wants to use Site Recovery to replicate on-premises workloads to Azure.</span></span>
 - <span data-ttu-id="f97cb-144">Woodgrove는 하드 코딩된 IP 주소에 종속된 응용 프로그램 및 구성을 처리해야 하므로 Azure로 장애 조치(failover)한 이후 해당 응용 프로그램의 IP 주소를 유지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f97cb-144">Woodgrove has to deal with applications and configurations which depend on hard-coded IP addresses, and thus need to retain IP addresses for their applications after failover to Azure.</span></span>
 - <span data-ttu-id="f97cb-145">Woodgrove는 172.16.1.0/24, 172.16.2.0/24의 IP 주소를 Azure에서 실행 중인 해당 리소스에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="f97cb-145">Woodgrove has assigned IP addresses from range 172.16.1.0/24, 172.16.2.0/24 to its resources running in Azure.</span></span>


<span data-ttu-id="f97cb-146">Woodgrove가 IP 주소를 유지하는 동시에 해당 VM을 Azure로 복제할 수 있으려면 회사는 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f97cb-146">For Woodgrove to be able to replicate its VMs to Azure while retaining the IP addresses, here's what the company needs to do:</span></span>

1. <span data-ttu-id="f97cb-147">Azure 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f97cb-147">Create an Azure virtual network.</span></span> <span data-ttu-id="f97cb-148">응용 프로그램이 원활하게 장애 조치(failover)할 수 있도록 온-프레미스 네트워크를 확장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f97cb-148">It should be an extension of the on-premises network, so that applications can fail over seamlessly.</span></span>
2. <span data-ttu-id="f97cb-149">Azure를 사용하면 Azure에서 만든 가상 네트워크에 대한 지점 및 사이트 간 연결뿐만 아니라 사이트 간 VPN 연결을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f97cb-149">Azure allows you to add site-to-site VPN connectivity, in addition to point-to-site connectivity to the virtual networks created in Azure.</span></span>
3. <span data-ttu-id="f97cb-150">사이트 간 연결을 설정하는 경우 Azure 네트워크에서 IP 주소 범위가 온-프레미스 IP 주소 범위와 다른 경우에만 온-프레미스 위치(로컬 네트워크)에 트래픽을 라우팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f97cb-150">When setting up the site-to-site connection, in the Azure network, you can route traffic to the on-premises location (local-network) only if the IP address range is different from the on-premises IP address range.</span></span>
    - <span data-ttu-id="f97cb-151">이는 Azure는 확대 서브넷을 지원하지 않기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="f97cb-151">This is because Azure doesn’t support stretched subnets.</span></span> <span data-ttu-id="f97cb-152">따라서 온-프레미스에 서브넷 192.168.1.0/24가 있는 경우 Azure 네트워크에 로컬 네트워크 192.168.1.0/24를 추가할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f97cb-152">So if you have subnet 192.168.1.0/24 on-premises, you can’t add a local-network 192.168.1.0/24 in the Azure network.</span></span>
    - <span data-ttu-id="f97cb-153">이렇게 예측하는 이유는 Azure가 서브넷에 활성 VM이 없고 해당 서브넷이 재해 복구용으로만 만들어진다는 것을 모르기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="f97cb-153">This is expected because Azure doesn’t know that there are no active VMs in the subnet, and that the subnet is being created for disaster recovery only.</span></span>
    - <span data-ttu-id="f97cb-154">Azure 네트워크 외부에서 네트워크 트래픽을 제대로 라우팅할 수 있으려면 네트워크 및 로컬 네트워크의 서브넷이 충돌하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f97cb-154">To be able to correctly route network traffic out of an Azure network the subnets in the network and the local-network mustn't conflict.</span></span>

![서브넷 장애 조치(failover) 전](./media/vmm-to-azure-walkthrough-network/network-design7.png)

### <a name="before-failover"></a><span data-ttu-id="f97cb-156">장애 조치(failover) 전</span><span class="sxs-lookup"><span data-stu-id="f97cb-156">Before failover</span></span>

1. <span data-ttu-id="f97cb-157">추가 네트워크(예: 복구 네트워크)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f97cb-157">Create an additional network (for example Recovery Network).</span></span> <span data-ttu-id="f97cb-158">이것은 장애 조치 VM이 생성되는 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="f97cb-158">This is the network in which failed over VMs are created.</span></span>
2. <span data-ttu-id="f97cb-159">VM에 사용할 IP 주소가 장애 조치(failover) 후에 유지되는지 확인하려면 VM 속성 > **구성**에서 온-프레미스 VM과 동일한 IP 주소를 지정하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f97cb-159">To ensure that the IP address for a VM is retained after a failover, in the VM properties > **Configure**, specify the same IP address that the VM has on-premises, and click **Save**.</span></span>
3. <span data-ttu-id="f97cb-160">VM이 장애 조치되는 경우 Azure Site Recovery는 가상 컴퓨터에 제공된 IP 주소를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="f97cb-160">When the VM is failed over, Azure Site Recovery will assign the provided IP address to it.</span></span>

    ![네트워크 속성](./media/vmm-to-azure-walkthrough-network/network-design8.png)

4. <span data-ttu-id="f97cb-162">장애 조치가 트리거되고 Azure에서 필수 IP 주소로 VM이 생성된 후 [Vnet 대 Vnet 연결](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md)을 사용하여 네트워크에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f97cb-162">After failover is trigger is triggered, and the VMs are created in Azure with the required IP address, you can connect to the network using a [Vnet to Vnet vonnection](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).</span></span> <span data-ttu-id="f97cb-163">이 작업은 스크립팅될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f97cb-163">This action can be scripted.</span></span>
5. <span data-ttu-id="f97cb-164">이제 192.168.1.0/24가 Azure로 이동되었음을 반영하도록 경로를 적절하게 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f97cb-164">Routes need to be appropriately modified, to reflect that 192.168.1.0/24 has now moved to Azure.</span></span>

    ![서브넷 장애 조치(failover) 후](./media/vmm-to-azure-walkthrough-network/network-design9.png)

### <a name="after-failover"></a><span data-ttu-id="f97cb-166">장애 조치(failover) 후</span><span class="sxs-lookup"><span data-stu-id="f97cb-166">After failover</span></span>

<span data-ttu-id="f97cb-167">위에서 설명한 대로 Azure 네트워크가 없는 경우 장애 조치(failover) 후 기본 사이트와 Azure 간의 사이트 간 VPN 연결을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f97cb-167">If you don't have an Azure network as illustrated above, you can create a site-to-site VPN connection between your primary site and Azure, after failvoer.</span></span>

## <a name="change-ip-addresses"></a><span data-ttu-id="f97cb-168">IP 주소 변경</span><span class="sxs-lookup"><span data-stu-id="f97cb-168">Change IP addresses</span></span>

<span data-ttu-id="f97cb-169">이 [블로그 게시물](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/)은 장애 조치(failover) 후 IP 주소를 유지할 필요가 없을 때 Azure 네트워킹 인프라를 설정하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f97cb-169">This [blog post](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/) explains how to set up the Azure networking infrastructure when you don't need to retain IP addresses after failover.</span></span> <span data-ttu-id="f97cb-170">응용 프로그램 설명으로 시작하여 온-프레미스 및 Azure의 네트워킹을 설정하는 방법을 찾고, 장애 조치(failover)를 실행하는 방법에 대한 정보로 마무리합니다.</span><span class="sxs-lookup"><span data-stu-id="f97cb-170">It starts with an application description, looks at how to set up networking on-premises and in Azure, and concludes with information about running failovers.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="f97cb-171">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f97cb-171">Next steps</span></span>

<span data-ttu-id="f97cb-172">[5단계: Azure 준비](vmm-to-azure-walkthrough-prepare-azure.md)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f97cb-172">Go to [Step 5: Prepare Azure](vmm-to-azure-walkthrough-prepare-azure.md)</span></span>

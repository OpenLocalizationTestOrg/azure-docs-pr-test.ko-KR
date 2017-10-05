---
title: "Azure Site Recovery를 사용하여 Azure로 Hyper-V(System Center VMM 없음) 복제를 위한 네트워킹 계획 | Microsoft Docs"
description: "이 문서에서는 Azure로 Hyper-V VM(VMM 없음)을 복제하는 데 필요한 네트워킹 계획을 설명합니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 5ca12254-975d-48e8-a84d-422825dac9b2
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: 100b9d8a55c2c163e7a04680f0f7d7963315ee73
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="step-4-plan-networking-for-hyper-v-to-azure-replication"></a><span data-ttu-id="a42b2-103">4단계: Azure로 Hyper-V 복제를 위한 네트워킹 계획</span><span class="sxs-lookup"><span data-stu-id="a42b2-103">Step 4: Plan networking for Hyper-V to Azure replication</span></span>

<span data-ttu-id="a42b2-104">이 문서에서는 [Azure Site Recovery](site-recovery-overview.md) 서비스를 사용하여 온-프레미스 Hyper-V VM(System Center VMM 없음)을 Azure로 복제할 때 네트워킹 계획 고려 사항을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a42b2-104">This article summarizes network planning considerations when replicating on-premises Hyper-V VMs (without System Center VMM) to Azure using the [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="a42b2-105">이 문서의 하단에서 의견을 게시하거나 [Azure Recovery Services 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)에서 질문하세요.</span><span class="sxs-lookup"><span data-stu-id="a42b2-105">Post any comments at the bottom of this article, or ask questions in the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="connecting-to-replica-vms-after-failover"></a><span data-ttu-id="a42b2-106">장애 조치(failover) 후 복제본 VM에 연결</span><span class="sxs-lookup"><span data-stu-id="a42b2-106">Connecting to replica VMs after failover</span></span>

<span data-ttu-id="a42b2-107">복제 및 장애 조치(failover) 전략을 계획할 경우 주요 질문 중 하나는 장애 조치(failover) 후에 Azure VM에 어떻게 연결하는가입니다.</span><span class="sxs-lookup"><span data-stu-id="a42b2-107">When planning your replication and failover strategy, one of the key questions is how to connect to the Azure VM after failover.</span></span> <span data-ttu-id="a42b2-108">복제본 Azure VM에 대한 네트워크 전략을 설계할 때 몇 가지 선택 항목이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a42b2-108">There are a couple of choices when designing your network strategy for replica Azure VMs:</span></span>

- <span data-ttu-id="a42b2-109">**다른 IP 주소**: 복제된 Azure VM 네트워크에 다른 IP 주소 범위를 사용하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a42b2-109">**Different IP address**: You can select to use a different IP address range for the replicated Azure VM network.</span></span> <span data-ttu-id="a42b2-110">이 시나리오에서 VM은 장애 조치(failover) 후에 새 IP 주소를 갖게 되며 DNS 업데이트가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a42b2-110">In this scenario the VM gets a new IP address after failover, and a DNS update is required.</span></span> [<span data-ttu-id="a42b2-111">자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="a42b2-111">Learn more</span></span>](site-recovery-test-failover-vmm-to-vmm.md#prepare-the-infrastructure-for-test-failover)
- <span data-ttu-id="a42b2-112">**동일한 IP 주소**: 기본 온-프레미스 네트워크에 있는 것과 동일한 IP 주소 범위를 장애 조치(failover) 후 Azure 네트워크에 대해 사용하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a42b2-112">**Same IP address**: You might want to use the same IP address range as that in your primary on-premises network, for the Azure network after failover.</span></span>  <span data-ttu-id="a42b2-113">동일한 IP 주소를 유지하면 장애 조치(failover) 후 네트워크 관련 문제가 줄어들어 복구가 간소화됩니다.</span><span class="sxs-lookup"><span data-stu-id="a42b2-113">Keeping the same IP addresses simplifies the recovery by reducing network related issues after failover.</span></span> <span data-ttu-id="a42b2-114">그러나 Azure에 복제하는 경우 장애 조치 후에 경로를 IP 주소의 새 위치로 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a42b2-114">However, when you're replicating to Azure, you will need to update routes with the new location of the IP addresses after failover.</span></span>


## <a name="retain-ip-addresses"></a><span data-ttu-id="a42b2-115">IP 주소 유지</span><span class="sxs-lookup"><span data-stu-id="a42b2-115">Retain IP addresses</span></span>

<span data-ttu-id="a42b2-116">Site Recovery는 Azure에 장애 조치할 경우 서브넷 장애 조치를 사용하여 고정 IP 주소를 유지하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a42b2-116">Site Recovery provides the capability to retain fixed IP addresses when failing over to Azure, with a subnet failover.</span></span>

<span data-ttu-id="a42b2-117">서브넷 장애 조치를 사용하는 경우 특정 서브넷은 사이트 1 또는 사이트 2에 있으며 두 사이트에 동시에 존재하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a42b2-117">With subnet failover, a specific subnet is present at Site 1 or Site 2, but never at both sites simultaneously.</span></span> <span data-ttu-id="a42b2-118">장애 조치(failover) 시 IP 주소 공간을 유지 관리하기 위해 라우터 인프라에 대해 프로그래밍 방식으로 정렬하여 한 사이트에서 다른 사이트로 서브넷을 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a42b2-118">In order to maintain the IP address space in the event of a failover, you programmatically arrange for the router infrastructure to move the subnets from one site to another.</span></span> <span data-ttu-id="a42b2-119">장애 조치(failover) 중에 서브넷은 연결되어 있는 보호된 VM과 함께 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a42b2-119">During failover, the subnets move with the associated protected VMs.</span></span> <span data-ttu-id="a42b2-120">주요 단점은 오류 발생 시 전체 서브넷을 이동해야 한다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="a42b2-120">The main drawback is that in the event of a failure, you have to move the whole subnet.</span></span>


### <a name="failover-example"></a><span data-ttu-id="a42b2-121">장애 조치 예제</span><span class="sxs-lookup"><span data-stu-id="a42b2-121">Failover example</span></span>

<span data-ttu-id="a42b2-122">Azure로 장애 조치(failover)에 관한 예제를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a42b2-122">Let's look at an example for failover to Azure.</span></span>

- <span data-ttu-id="a42b2-123">Woodgrove Bank라는 가상의 회사에는 비즈니스 앱을 호스팅하는 온-프레미스 인프라가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a42b2-123">A ficticious company, Woodgrove Bank, has an on-premises infrastructure hosting their business apps.</span></span> <span data-ttu-id="a42b2-124">모바일 응용 프로그램은 Azure에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="a42b2-124">Their mobile applications are hosted on Azure.</span></span>
- <span data-ttu-id="a42b2-125">Azure 및 온-프레미스 서버에서 Woodgrove Bank VM 간의 연결은 온-프레미스 에지 네트워크와 Azure 가상 네트워크 간에 있는 사이트 간(VPN) 연결에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="a42b2-125">Connectivity between Woodgrove Bank VMs in Azure and on-premises servers is provided by a site-to-site (VPN) connection between the on-premises edge network and the Azure virtual network.</span></span>
- <span data-ttu-id="a42b2-126">이 VPN은 Azure에서 회사의 가상 네트워크가 온-프레미스 네트워크의 확장으로 나타난다는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="a42b2-126">This VPN means that the company's virtual network in Azure appears as an extension of their on-premises network.</span></span>
- <span data-ttu-id="a42b2-127">Woodgrove는 Site Recovery를 사용하여 온-프레미스 워크로드를 Azure로 복제하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a42b2-127">Woodgrove wants to use Site Recovery to replicate on-premises workloads to Azure.</span></span>
 - <span data-ttu-id="a42b2-128">Woodgrove는 하드 코딩된 IP 주소에 종속된 응용 프로그램 및 구성을 처리해야 하므로 Azure로 장애 조치(failover)한 이후 해당 응용 프로그램의 IP 주소를 유지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a42b2-128">Woodgrove has to deal with applications and configurations which depend on hard-coded IP addresses, and thus need to retain IP addresses for their applications after failover to Azure.</span></span>
 - <span data-ttu-id="a42b2-129">Woodgrove는 172.16.1.0/24, 172.16.2.0/24의 IP 주소를 Azure에서 실행 중인 해당 리소스에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="a42b2-129">Woodgrove has assigned IP addresses from range 172.16.1.0/24, 172.16.2.0/24 to its resources running in Azure.</span></span>


<span data-ttu-id="a42b2-130">Woodgrove가 IP 주소를 유지하는 동시에 해당 VM을 Azure로 복제할 수 있으려면 회사는 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a42b2-130">For Woodgrove to be able to replicate its VMs to Azure while retaining the IP addresses, here's what the company needs to do:</span></span>

1. <span data-ttu-id="a42b2-131">Azure 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a42b2-131">Create an Azure virtual network.</span></span> <span data-ttu-id="a42b2-132">응용 프로그램이 원활하게 장애 조치(failover)할 수 있도록 온-프레미스 네트워크를 확장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a42b2-132">It should be an extension of the on-premises network, so that applications can fail over seamlessly.</span></span>
2. <span data-ttu-id="a42b2-133">Azure를 사용하면 Azure에서 만든 가상 네트워크에 대한 지점 및 사이트 간 연결뿐만 아니라 사이트 간 VPN 연결을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a42b2-133">Azure allows you to add site-to-site VPN connectivity, in addition to point-to-site connectivity to the virtual networks created in Azure.</span></span>
3. <span data-ttu-id="a42b2-134">사이트 간 연결을 설정하는 경우 Azure 네트워크에서 IP 주소 범위가 온-프레미스 IP 주소 범위와 다른 경우에만 온-프레미스 위치(로컬 네트워크)에 트래픽을 라우팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a42b2-134">When setting up the site-to-site connection, in the Azure network, you can route traffic to the on-premises location (local-network) only if the IP address range is different from the on-premises IP address range.</span></span>
    - <span data-ttu-id="a42b2-135">이는 Azure는 확대 서브넷을 지원하지 않기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="a42b2-135">This is because Azure doesn’t support stretched subnets.</span></span> <span data-ttu-id="a42b2-136">따라서 온-프레미스에 서브넷 192.168.1.0/24가 있는 경우 Azure 네트워크에 로컬 네트워크 192.168.1.0/24를 추가할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a42b2-136">So if you have subnet 192.168.1.0/24 on-premises, you can’t add a local-network 192.168.1.0/24 in the Azure network.</span></span>
    - <span data-ttu-id="a42b2-137">이렇게 예측하는 이유는 Azure가 서브넷에 활성 VM이 없고 해당 서브넷이 재해 복구용으로만 만들어진다는 것을 모르기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="a42b2-137">This is expected because Azure doesn’t know that there are no active VMs in the subnet, and that the subnet is being created for disaster recovery only.</span></span>
    - <span data-ttu-id="a42b2-138">Azure 네트워크 외부에서 네트워크 트래픽을 제대로 라우팅할 수 있으려면 네트워크 및 로컬 네트워크의 서브넷이 충돌하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a42b2-138">To be able to correctly route network traffic out of an Azure network the subnets in the network and the local-network mustn't conflict.</span></span>

![서브넷 장애 조치(failover) 전](./media/hyper-v-site-walkthrough-network/network-design7.png)

### <a name="before-failover"></a><span data-ttu-id="a42b2-140">장애 조치(failover) 전</span><span class="sxs-lookup"><span data-stu-id="a42b2-140">Before failover</span></span>

1. <span data-ttu-id="a42b2-141">추가 네트워크(예: 복구 네트워크)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a42b2-141">Create an additional network (for example Recovery Network).</span></span> <span data-ttu-id="a42b2-142">이것은 장애 조치 VM이 생성되는 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="a42b2-142">This is the network in which failed over VMs are created.</span></span>
2. <span data-ttu-id="a42b2-143">VM에 사용할 IP 주소가 장애 조치(failover) 후에 유지되는지 확인하려면 VM 속성 > **구성**에서 온-프레미스 VM과 동일한 IP 주소를 지정하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a42b2-143">To ensure that the IP address for a VM is retained after a failover, in the VM properties > **Configure**, specify the same IP address that the VM has on-premises, and click **Save**.</span></span>
3. <span data-ttu-id="a42b2-144">VM이 장애 조치되는 경우 Azure Site Recovery는 가상 컴퓨터에 제공된 IP 주소를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="a42b2-144">When the VM is failed over, Azure Site Recovery will assign the provided IP address to it.</span></span>

    ![네트워크 속성](./media/hyper-v-site-walkthrough-network/network-design8.png)

4. <span data-ttu-id="a42b2-146">장애 조치가 트리거되고 Azure에서 필수 IP 주소로 VM이 생성된 후 [Vnet 대 Vnet 연결](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md)을 사용하여 네트워크에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a42b2-146">After failover is trigger is triggered, and the VMs are created in Azure with the required IP address, you can connect to the network using a [Vnet to Vnet vonnection](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).</span></span> <span data-ttu-id="a42b2-147">이 작업은 스크립팅될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a42b2-147">This action can be scripted.</span></span>
5. <span data-ttu-id="a42b2-148">이제 192.168.1.0/24가 Azure로 이동되었음을 반영하도록 경로를 적절하게 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a42b2-148">Routes need to be appropriately modified, to reflect that 192.168.1.0/24 has now moved to Azure.</span></span>

    ![서브넷 장애 조치(failover) 후](./media/hyper-v-site-walkthrough-network/network-design9.png)

### <a name="after-failover"></a><span data-ttu-id="a42b2-150">장애 조치(failover) 후</span><span class="sxs-lookup"><span data-stu-id="a42b2-150">After failover</span></span>

<span data-ttu-id="a42b2-151">위에서 설명한 대로 Azure 네트워크가 없는 경우 장애 조치(failover) 후 기본 사이트와 Azure 간의 사이트 간 VPN 연결을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a42b2-151">If you don't have an Azure network as illustrated above, you can create a site-to-site VPN connection between your primary site and Azure, after failvoer.</span></span>

## <a name="change-ip-addresses"></a><span data-ttu-id="a42b2-152">IP 주소 변경</span><span class="sxs-lookup"><span data-stu-id="a42b2-152">Change IP addresses</span></span>

<span data-ttu-id="a42b2-153">이 [블로그 게시물](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/)은 장애 조치(failover) 후 IP 주소를 유지할 필요가 없을 때 Azure 네트워킹 인프라를 설정하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a42b2-153">This [blog post](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/) explains how to set up the Azure networking infrastructure when you don't need to retain IP addresses after failover.</span></span> <span data-ttu-id="a42b2-154">응용 프로그램 설명으로 시작하여 온-프레미스 및 Azure의 네트워킹을 설정하는 방법을 찾고, 장애 조치(failover)를 실행하는 방법에 대한 정보로 마무리합니다.</span><span class="sxs-lookup"><span data-stu-id="a42b2-154">It starts with an application description, looks at how to set up networking on-premises and in Azure, and concludes with information about running failovers.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="a42b2-155">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a42b2-155">Next steps</span></span>

<span data-ttu-id="a42b2-156">[5단계: Azure 준비](hyper-v-site-walkthrough-prepare-azure.md)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a42b2-156">Go to [Step 5: Prepare Azure](hyper-v-site-walkthrough-prepare-azure.md)</span></span>

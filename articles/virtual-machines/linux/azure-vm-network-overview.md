---
title: "Azure 및 Linux VM 네트워크 개요 | Microsoft Docs"
description: "Azure 및 Linux VM 네트워킹 개요입니다."
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: vlivech
manager: timlt
editor: 
ms.assetid: b5420e35-0463-4456-9803-6142db150f2e
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 10/25/2016
ms.author: v-livech
ms.openlocfilehash: 1ff4a0482d6dc6ec0eceaa89ca4b87ba1e2f89a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-and-linux-vm-network-overview"></a><span data-ttu-id="e91a3-103">Azure 및 Linux VM 네트워크 개요</span><span class="sxs-lookup"><span data-stu-id="e91a3-103">Azure and Linux VM Network Overview</span></span>
## <a name="virtual-networks"></a><span data-ttu-id="e91a3-104">가상 네트워크</span><span class="sxs-lookup"><span data-stu-id="e91a3-104">Virtual Networks</span></span>
<span data-ttu-id="e91a3-105">Azure 가상 네트워크(VNet)는 클라우드의 사용자 네트워크를 나타내는 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="e91a3-105">An Azure virtual network (VNet) is a representation of your own network in the cloud.</span></span> <span data-ttu-id="e91a3-106">구독 전용 Azure 클라우드를 논리적으로 격리한 것이 가상 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="e91a3-106">It is a logical isolation of the Azure cloud dedicated to your subscription.</span></span> <span data-ttu-id="e91a3-107">사용자는 이 네트워크 내부의 IP 주소 블록, DNS 설정, 보안 정책 및 경로 테이블을 완벽하게 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e91a3-107">You can fully control the IP address blocks, DNS settings, security policies, and route tables within this network.</span></span> <span data-ttu-id="e91a3-108">또한 VNet을 여러 서브넷으로 분할하고 Azure IaaS VM(가상 컴퓨터) 및/또는 Cloud Services(PaaS 역할 인스턴스)를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e91a3-108">You can also further segment your VNet into subnets and launch Azure IaaS virtual machines (VMs) and/or Cloud services (PaaS role instances).</span></span> <span data-ttu-id="e91a3-109">뿐만 아니라 Azure에서 제공하는 연결 옵션 중 하나를 사용하여 가상 네트워크를 온-프레미스 네트워크에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e91a3-109">Additionally, you can connect the virtual network to your on-premises network using one of the connectivity options available in Azure.</span></span> <span data-ttu-id="e91a3-110">기본적으로 네트워크를 Azure로 확장하여 IP 주소 블록을 완벽하게 제어하고, Azure가 제공하는 엔터프라이즈급 솔루션의 혜택을 누릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e91a3-110">In essence, you can expand your network to Azure, with complete control on IP address blocks with the benefit of enterprise scale Azure provides.</span></span>

* [<span data-ttu-id="e91a3-111">가상 네트워크 개요</span><span class="sxs-lookup"><span data-stu-id="e91a3-111">Virtual Network Overview</span></span>](../../virtual-network/virtual-networks-overview.md)

<span data-ttu-id="e91a3-112">Azure CLI를 사용하여 VNet을 만들려면 다음 연습을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e91a3-112">To create a VNet by using the Azure CLI, go here to follow the walk through.</span></span>

* [<span data-ttu-id="e91a3-113">Azure CLI를 사용하여 VNet을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="e91a3-113">How to create a VNet using the Azure CLI</span></span>](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)

## <a name="network-security-groups"></a><span data-ttu-id="e91a3-114">네트워크 보안 그룹</span><span class="sxs-lookup"><span data-stu-id="e91a3-114">Network Security Groups</span></span>
<span data-ttu-id="e91a3-115">NSG(네트워크 보안 그룹)은 ACL(액세스 제어 목록)의 가상 네트워크에 VM 인스턴스에 대한 허용 또는 거부 네트워크 트래픽 규칙의 목록을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="e91a3-115">Network security group (NSG) contains a list of Access Control List (ACL) rules that allow or deny network traffic to your VM instances in a Virtual Network.</span></span> <span data-ttu-id="e91a3-116">NSG는 서브넷 또는 서브넷 내의 개별 VM 인스턴스 중 하나와 연결될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e91a3-116">NSGs can be associated with either subnets or individual VM instances within that subnet.</span></span> <span data-ttu-id="e91a3-117">NSG를 서브넷과 연결한 경우 ACL 규칙은 해당 서브넷에 있는 모든 VM 인스턴스에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e91a3-117">When a NSG is associated with a subnet, the ACL rules apply to all the VM instances in that subnet.</span></span> <span data-ttu-id="e91a3-118">또한 개별 VM에 대한 트래픽은 해당 VM에 직접 NSG를 연결하여 추가로 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e91a3-118">In addition, traffic to an individual VM can be restricted further by associating a NSG directly to that VM.</span></span>

* [<span data-ttu-id="e91a3-119">NSG(네트워크 보안 그룹)란?</span><span class="sxs-lookup"><span data-stu-id="e91a3-119">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="e91a3-120">Azure CLI에서 NSG를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="e91a3-120">How to create NSGs in the Azure CLI</span></span>](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)

## <a name="user-defined-routes"></a><span data-ttu-id="e91a3-121">사용자 정의 경로</span><span class="sxs-lookup"><span data-stu-id="e91a3-121">User Defined Routes</span></span>
<span data-ttu-id="e91a3-122">Azure에서 VNet(가상 네트워크)에 VM(가상 컴퓨터)을 추가하면 네트워크를 통해 다른 VM과 통신할 수 있는지 자동으로 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e91a3-122">When you add virtual machines (VMs) to a virtual network (VNet) in Azure, you will notice that the VMs are able to communicate with each other over the network, automatically.</span></span> <span data-ttu-id="e91a3-123">서로 다른 서브넷에 있는 VM 간에도 게이트웨이를 지정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e91a3-123">You do not need to specify a gateway, even though the VMs are in different subnets.</span></span> <span data-ttu-id="e91a3-124">VM에서 공용 인터넷에 통신하는 경우는 물론, Azure와 사용자 고유의 데이터 센터 간 하이브리드 연결이 있는 경우 사용자의 온-프레미스 네트워크에 통신하는 경우에도 마찬가지입니다 .</span><span class="sxs-lookup"><span data-stu-id="e91a3-124">The same is true for communication from the VMs to the public Internet, and even to your on-premises network when a hybrid connection from Azure to your own datacenter is present.</span></span>

* [<span data-ttu-id="e91a3-125">사용자 정의 경로 및 IP 전달이란?</span><span class="sxs-lookup"><span data-stu-id="e91a3-125">What are User Defined Routes and IP Forwarding?</span></span>](../../virtual-network/virtual-networks-udr-overview.md)
* [<span data-ttu-id="e91a3-126">Azure CLI에서 UDR 만들기</span><span class="sxs-lookup"><span data-stu-id="e91a3-126">Create a UDR in the Azure CLI</span></span>](../../virtual-network/virtual-network-create-udr-arm-cli.md)

## <a name="associating-a-fqdn-to-your-linux-vm"></a><span data-ttu-id="e91a3-127">Linux VM에 FQDN 연결</span><span class="sxs-lookup"><span data-stu-id="e91a3-127">Associating a FQDN to your Linux VM</span></span>
<span data-ttu-id="e91a3-128">Resource Manager 배포 모델을 사용하여 Azure Portal에서 VM(가상 컴퓨터)을 만들 때, 가상 컴퓨터의 공용 IP 리소스가 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="e91a3-128">When you create a virtual machine (VM) in the Azure portal using the Resource Manager deployment model, a public IP resource for the virtual machine is automatically created.</span></span> <span data-ttu-id="e91a3-129">이 IP 주소를 사용하여 VM에 원격으로 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="e91a3-129">You use this IP address to remotely access the VM.</span></span> <span data-ttu-id="e91a3-130">기본적으로 포털에서 정규화된 도메인 이름 또는 FQDN을 만들지는 않지만 VM을 만들면 이름을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e91a3-130">Although the portal does not create a fully qualified domain name, or FQDN, by default, you can add one once the VM is created.</span></span>

* [<span data-ttu-id="e91a3-131">Azure Portal에서 정규화된 도메인 이름 만들기</span><span class="sxs-lookup"><span data-stu-id="e91a3-131">Create a Fully Qualified Domain Name in the Azure portal</span></span>](portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="network-interfaces"></a><span data-ttu-id="e91a3-132">네트워크 인터페이스</span><span class="sxs-lookup"><span data-stu-id="e91a3-132">Network interfaces</span></span>
<span data-ttu-id="e91a3-133">네트워크 인터페이스(NIC)는 VM(가상 컴퓨터)과 기본 소프트웨어 네트워크 간 상호 연결입니다.</span><span class="sxs-lookup"><span data-stu-id="e91a3-133">A network interface (NIC) is the interconnection between a Virtual Machine (VM) and the underlying software network.</span></span> <span data-ttu-id="e91a3-134">이 문서에서는 네트워크 인터페이스란 무엇이며 Azure Resource Manager 배포 모델에서 어떻게 사용되는지에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e91a3-134">This article explains what a network interface is and how it's used in the Azure Resource Manager deployment model.</span></span>

* [<span data-ttu-id="e91a3-135">가상 네트워크 인터페이스</span><span class="sxs-lookup"><span data-stu-id="e91a3-135">Virtual Network Interfaces</span></span>](../../virtual-network/virtual-network-network-interface.md)

## <a name="virtual-nics-and-dns-labeling"></a><span data-ttu-id="e91a3-136">가상 NIC 및 DNS 레이블 지정</span><span class="sxs-lookup"><span data-stu-id="e91a3-136">Virtual NICs and DNS labeling</span></span>
<span data-ttu-id="e91a3-137">영구적으로 유지해야 하는 서버가 있지만 서버가 가축으로 처리되고 해체되며 자주 배포되는 경우 NIC에 DNS 레이블 지정을 사용하여 VNET의 이름을 유지하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="e91a3-137">If you have a server that you need to be persistent, but that server is treated as cattle and is torn down and deployed frequently, you will want to use DNS labeling on your NIC to persist the name on the VNET.</span></span>  <span data-ttu-id="e91a3-138">다음 연습을 통해 고정 IP를 가진 NIC를 영구적으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e91a3-138">With the following walk-through you will setup a persistently named NIC with a static IP.</span></span>

* [<span data-ttu-id="e91a3-139">Azure CLI를 사용하여 전체 Linux 환경 만들기</span><span class="sxs-lookup"><span data-stu-id="e91a3-139">Create a complete Linux environment by using the Azure CLI</span></span>](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="virtual-network-gateways"></a><span data-ttu-id="e91a3-140">가상 네트워크 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="e91a3-140">Virtual Network Gateways</span></span>
<span data-ttu-id="e91a3-141">가상 네트워크 게이트웨이는 Azure 가상 네트워크와 온-프레미스 위치 및 Azure 내의 가상 네트워크 간(VNet 간)에 네트워크 트래픽을 보내는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e91a3-141">A virtual network gateway is used to send network traffic between Azure virtual networks and on-premises locations and also between virtual networks within Azure (VNet-to-VNet).</span></span> <span data-ttu-id="e91a3-142">VPN Gateway를 구성할 때 가상 네트워크 게이트웨이 및 가상 네트워크 게이트웨이 연결을 만들고 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e91a3-142">When you configure a VPN gateway, you must create and configure a virtual network gateway and a virtual network gateway connection.</span></span>

* [<span data-ttu-id="e91a3-143">VPN Gateway 정보</span><span class="sxs-lookup"><span data-stu-id="e91a3-143">About VPN Gateway</span></span>](../../vpn-gateway/vpn-gateway-about-vpngateways.md)

## <a name="internal-load-balancing"></a><span data-ttu-id="e91a3-144">내부 부하 분산</span><span class="sxs-lookup"><span data-stu-id="e91a3-144">Internal Load Balancing</span></span>
<span data-ttu-id="e91a3-145">Azure 부하 분산 장치는 계층 4(TCP, UDP) 부하 분산 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="e91a3-145">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer.</span></span> <span data-ttu-id="e91a3-146">부하 분산 장치는 부하 분산 장치 집합에 있는 클라우드 서비스 또는 가상 컴퓨터의 정상 서비스 인스턴스 간에 들어오는 트래픽을 배포하여 고가용성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e91a3-146">The load balancer provides high availability by distributing incoming traffic among healthy service instances in cloud services or virtual machines in a load balancer set.</span></span> <span data-ttu-id="e91a3-147">Azure Load Balancer는 여러 포트, 여러 IP 주소 또는 둘 다에서 이러한 서비스를 제공할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e91a3-147">Azure Load Balancer can also present those services on multiple ports, multiple IP addresses, or both.</span></span>

* [<span data-ttu-id="e91a3-148">Azure CLI를 사용하여 내부 부하 분산 장치 만들기</span><span class="sxs-lookup"><span data-stu-id="e91a3-148">Creating an internal load balancer using the Azure CLI</span></span>](../../load-balancer/load-balancer-get-started-internet-arm-cli.md)


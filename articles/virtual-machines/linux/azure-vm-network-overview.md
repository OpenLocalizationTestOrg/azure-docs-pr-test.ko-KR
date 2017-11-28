---
title: "aaaAzure 및 Linux VM 네트워크 개요 | Microsoft Docs"
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
ms.openlocfilehash: c3de2dc583c62160e10c0e97e96fef49b9eaffbf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-and-linux-vm-network-overview"></a><span data-ttu-id="44461-103">Azure 및 Linux VM 네트워크 개요</span><span class="sxs-lookup"><span data-stu-id="44461-103">Azure and Linux VM Network Overview</span></span>
## <a name="virtual-networks"></a><span data-ttu-id="44461-104">가상 네트워크</span><span class="sxs-lookup"><span data-stu-id="44461-104">Virtual Networks</span></span>
<span data-ttu-id="44461-105">Azure 가상 네트워크 (VNet)는 hello 클라우드에서 사용자의 네트워크의 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="44461-105">An Azure virtual network (VNet) is a representation of your own network in hello cloud.</span></span> <span data-ttu-id="44461-106">Azure 클라우드 전용 tooyour 구독 hello의 논리적 격리는</span><span class="sxs-lookup"><span data-stu-id="44461-106">It is a logical isolation of hello Azure cloud dedicated tooyour subscription.</span></span> <span data-ttu-id="44461-107">Hello IP 주소 블록, DNS 설정, 보안 정책 및이 네트워크 내에서 경로 테이블을 완벽 하 게 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44461-107">You can fully control hello IP address blocks, DNS settings, security policies, and route tables within this network.</span></span> <span data-ttu-id="44461-108">또한 VNet을 여러 서브넷으로 분할하고 Azure IaaS VM(가상 컴퓨터) 및/또는 Cloud Services(PaaS 역할 인스턴스)를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44461-108">You can also further segment your VNet into subnets and launch Azure IaaS virtual machines (VMs) and/or Cloud services (PaaS role instances).</span></span> <span data-ttu-id="44461-109">또한 Azure에서 사용할 수 있는 hello 연결 옵션 중 하나를 사용 하 여 hello 가상 네트워크 tooyour 온-프레미스 네트워크를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44461-109">Additionally, you can connect hello virtual network tooyour on-premises network using one of hello connectivity options available in Azure.</span></span> <span data-ttu-id="44461-110">기본적으로 Azure에서 제공 하는 엔터프라이즈 규모의 hello 혜택을 사용 하 여 IP 주소 블록에 완벽 한 제어 하 여 네트워크 tooAzure 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44461-110">In essence, you can expand your network tooAzure, with complete control on IP address blocks with hello benefit of enterprise scale Azure provides.</span></span>

* [<span data-ttu-id="44461-111">Virtual Network 개요</span><span class="sxs-lookup"><span data-stu-id="44461-111">Virtual Network Overview</span></span>](../../virtual-network/virtual-networks-overview.md)

<span data-ttu-id="44461-112">사용 하 여 VNet toocreate hello Azure CLI, 이동 여기 toofollow hello 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="44461-112">toocreate a VNet by using hello Azure CLI, go here toofollow hello walk through.</span></span>

* [<span data-ttu-id="44461-113">사용 하 여 VNet toocreate Azure CLI hello 하는 방법</span><span class="sxs-lookup"><span data-stu-id="44461-113">How toocreate a VNet using hello Azure CLI</span></span>](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)

## <a name="network-security-groups"></a><span data-ttu-id="44461-114">네트워크 보안 그룹</span><span class="sxs-lookup"><span data-stu-id="44461-114">Network Security Groups</span></span>
<span data-ttu-id="44461-115">네트워크 보안 그룹 NSG ()를 허용 하거나 거부 네트워크 트래픽을 가상 네트워크에서 VM 인스턴스 tooyour 액세스 제어 목록 (ACL) 규칙 목록이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44461-115">Network security group (NSG) contains a list of Access Control List (ACL) rules that allow or deny network traffic tooyour VM instances in a Virtual Network.</span></span> <span data-ttu-id="44461-116">NSG는 서브넷 또는 서브넷 내의 개별 VM 인스턴스 중 하나와 연결될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44461-116">NSGs can be associated with either subnets or individual VM instances within that subnet.</span></span> <span data-ttu-id="44461-117">NSG를 서브넷과 연결 하는 경우 해당 서브넷에 tooall hello VM 인스턴스 hello ACL 규칙에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="44461-117">When a NSG is associated with a subnet, hello ACL rules apply tooall hello VM instances in that subnet.</span></span> <span data-ttu-id="44461-118">또한 트래픽 tooan 개별 VM을 제한할 수 NSG를 연결 하 여 추가 VM toothat 직접 합니다.</span><span class="sxs-lookup"><span data-stu-id="44461-118">In addition, traffic tooan individual VM can be restricted further by associating a NSG directly toothat VM.</span></span>

* [<span data-ttu-id="44461-119">NSG(네트워크 보안 그룹)란?</span><span class="sxs-lookup"><span data-stu-id="44461-119">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="44461-120">Toocreate Nsg에 Azure CLI hello 하는 방법</span><span class="sxs-lookup"><span data-stu-id="44461-120">How toocreate NSGs in hello Azure CLI</span></span>](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)

## <a name="user-defined-routes"></a><span data-ttu-id="44461-121">사용자 정의 경로</span><span class="sxs-lookup"><span data-stu-id="44461-121">User Defined Routes</span></span>
<span data-ttu-id="44461-122">Azure에서 가상 컴퓨터 (Vm) tooa 가상 네트워크 (VNet)를 추가할 때 hello Vm은 서로 수 toocommunicate hello 네트워크를 통해 자동으로 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44461-122">When you add virtual machines (VMs) tooa virtual network (VNet) in Azure, you will notice that hello VMs are able toocommunicate with each other over hello network, automatically.</span></span> <span data-ttu-id="44461-123">Hello Vm 서브넷이 서로 다른 경우에 게이트웨이 toospecify를 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="44461-123">You do not need toospecify a gateway, even though hello VMs are in different subnets.</span></span> <span data-ttu-id="44461-124">hello 같은 기준이 hello Vm toohello에서 통신에 대 한 공용 인터넷 및 tooyour Azure에서 하이브리드 연결 데이터 센터를 사용할 수 있는지를 소유 하는 경우에 tooyour 온-프레미스 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="44461-124">hello same is true for communication from hello VMs toohello public Internet, and even tooyour on-premises network when a hybrid connection from Azure tooyour own datacenter is present.</span></span>

* [<span data-ttu-id="44461-125">사용자 정의 경로 및 IP 전달이란?</span><span class="sxs-lookup"><span data-stu-id="44461-125">What are User Defined Routes and IP Forwarding?</span></span>](../../virtual-network/virtual-networks-udr-overview.md)
* [<span data-ttu-id="44461-126">Hello Azure CLI에에서는 UDR 만들기</span><span class="sxs-lookup"><span data-stu-id="44461-126">Create a UDR in hello Azure CLI</span></span>](../../virtual-network/virtual-network-create-udr-arm-cli.md)

## <a name="associating-a-fqdn-tooyour-linux-vm"></a><span data-ttu-id="44461-127">FQDN tooyour Linux VM 연결</span><span class="sxs-lookup"><span data-stu-id="44461-127">Associating a FQDN tooyour Linux VM</span></span>
<span data-ttu-id="44461-128">Hello Azure 포털에서에서 가상 컴퓨터 (VM)를 만들 때 hello 리소스 관리자 배포 모델을 공용 IP를 사용 하 여 리소스가 hello 가상 컴퓨터에 대 한 자동으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="44461-128">When you create a virtual machine (VM) in hello Azure portal using hello Resource Manager deployment model, a public IP resource for hello virtual machine is automatically created.</span></span> <span data-ttu-id="44461-129">VM이 IP 주소 tooremotely 액세스 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="44461-129">You use this IP address tooremotely access hello VM.</span></span> <span data-ttu-id="44461-130">Hello 포털에서는 생성 하지는 정규화 된 도메인 이름 또는 FQDN으로 기본적으로 있지만 hello VM가 만들어지면 하나 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44461-130">Although hello portal does not create a fully qualified domain name, or FQDN, by default, you can add one once hello VM is created.</span></span>

* [<span data-ttu-id="44461-131">Hello Azure 포털에서에서 정규화 된 도메인 이름 만들기</span><span class="sxs-lookup"><span data-stu-id="44461-131">Create a Fully Qualified Domain Name in hello Azure portal</span></span>](portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="network-interfaces"></a><span data-ttu-id="44461-132">네트워크 인터페이스</span><span class="sxs-lookup"><span data-stu-id="44461-132">Network interfaces</span></span>
<span data-ttu-id="44461-133">네트워크 인터페이스 (NIC) hello 연결로 가상 컴퓨터 (VM) 및 기본 소프트웨어 네트워크 hello 사이입니다.</span><span class="sxs-lookup"><span data-stu-id="44461-133">A network interface (NIC) is hello interconnection between a Virtual Machine (VM) and hello underlying software network.</span></span> <span data-ttu-id="44461-134">이 문서에서는 설명 네트워크 인터페이스 이며 hello Azure 리소스 관리자 배포 모델에서 사용 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="44461-134">This article explains what a network interface is and how it's used in hello Azure Resource Manager deployment model.</span></span>

* [<span data-ttu-id="44461-135">가상 네트워크 인터페이스</span><span class="sxs-lookup"><span data-stu-id="44461-135">Virtual Network Interfaces</span></span>](../../virtual-network/virtual-network-network-interface.md)

## <a name="virtual-nics-and-dns-labeling"></a><span data-ttu-id="44461-136">가상 NIC 및 DNS 레이블 지정</span><span class="sxs-lookup"><span data-stu-id="44461-136">Virtual NICs and DNS labeling</span></span>
<span data-ttu-id="44461-137">Toobe 영구적으로 해야 하지만 해당 서버 캐 틀으로 처리 되 고 삭제 됩니다 서버 있고 자주 배포 toouse hello VNET에 있는 NIC toopersist hello 이름에 DNS 레이블을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="44461-137">If you have a server that you need toobe persistent, but that server is treated as cattle and is torn down and deployed frequently, you will want toouse DNS labeling on your NIC toopersist hello name on hello VNET.</span></span>  <span data-ttu-id="44461-138">연습을 수행 하는 hello로 고정 ip 영구적으로 명명 된 NIC는 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="44461-138">With hello following walk-through you will setup a persistently named NIC with a static IP.</span></span>

* [<span data-ttu-id="44461-139">Hello Azure CLI를 사용 하 여 전체 Linux 환경 만들기</span><span class="sxs-lookup"><span data-stu-id="44461-139">Create a complete Linux environment by using hello Azure CLI</span></span>](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="virtual-network-gateways"></a><span data-ttu-id="44461-140">가상 네트워크 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="44461-140">Virtual Network Gateways</span></span>
<span data-ttu-id="44461-141">가상 네트워크 게이트웨이에 사용 되는 Azure 가상 네트워크와 온-프레미스 위치 간 및 Azure (VNet 대 VNet) 내에서 가상 네트워크 간의 toosend 네트워크 트래픽을 합니다.</span><span class="sxs-lookup"><span data-stu-id="44461-141">A virtual network gateway is used toosend network traffic between Azure virtual networks and on-premises locations and also between virtual networks within Azure (VNet-to-VNet).</span></span> <span data-ttu-id="44461-142">VPN Gateway를 구성할 때 가상 네트워크 게이트웨이 및 가상 네트워크 게이트웨이 연결을 만들고 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="44461-142">When you configure a VPN gateway, you must create and configure a virtual network gateway and a virtual network gateway connection.</span></span>

* [<span data-ttu-id="44461-143">VPN Gateway 정보</span><span class="sxs-lookup"><span data-stu-id="44461-143">About VPN Gateway</span></span>](../../vpn-gateway/vpn-gateway-about-vpngateways.md)

## <a name="internal-load-balancing"></a><span data-ttu-id="44461-144">내부 부하 분산</span><span class="sxs-lookup"><span data-stu-id="44461-144">Internal Load Balancing</span></span>
<span data-ttu-id="44461-145">Azure 부하 분산 장치는 계층 4(TCP, UDP) 부하 분산 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="44461-145">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer.</span></span> <span data-ttu-id="44461-146">hello 부하 분산 장치 부하 분산 장치 집합의 가상 컴퓨터 또는 클라우드 서비스의 비정상 상태 서비스 인스턴스 간에 들어오는 트래픽을 분산 하 여 고가용성을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="44461-146">hello load balancer provides high availability by distributing incoming traffic among healthy service instances in cloud services or virtual machines in a load balancer set.</span></span> <span data-ttu-id="44461-147">Azure Load Balancer는 여러 포트, 여러 IP 주소 또는 둘 다에서 이러한 서비스를 제공할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44461-147">Azure Load Balancer can also present those services on multiple ports, multiple IP addresses, or both.</span></span>

* [<span data-ttu-id="44461-148">Hello Azure CLI를 사용 하는 내부 부하 분산 장치 만들기</span><span class="sxs-lookup"><span data-stu-id="44461-148">Creating an internal load balancer using hello Azure CLI</span></span>](../../load-balancer/load-balancer-get-started-internet-arm-cli.md)


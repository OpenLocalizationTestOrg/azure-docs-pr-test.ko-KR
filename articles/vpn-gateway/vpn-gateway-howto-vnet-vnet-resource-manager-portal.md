---
title: "다른 VNet에 Azure Virtual Network 연결: 포털 | Microsoft Docs"
description: "리소스 관리자 및 Azure Portal을 사용하여 Vnet 간의 VPN Gateway 연결을 만듭니다."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a7015cfc-764b-46a1-bfac-043d30a275df
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: 0293495a9cbdab1fc797d9948e4cbb7759b1ba54
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-the-azure-portal"></a><span data-ttu-id="81187-103">Azure Portal을 사용하여 VNet-VNet 간 VPN Gateway 연결 구성</span><span class="sxs-lookup"><span data-stu-id="81187-103">Configure a VNet-to-VNet VPN gateway connection using the Azure portal</span></span>

<span data-ttu-id="81187-104">이 문서에서는 가상 네트워크 간에 VPN Gateway 연결을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="81187-104">This article shows you how to create a VPN gateway connection between virtual networks.</span></span> <span data-ttu-id="81187-105">가상 네트워크는 같은 또는 다른 구독의 같은 지역에 있을 수도 있고 다른 지역에 있을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81187-105">The virtual networks can be in the same or different regions, and from the same or different subscriptions.</span></span> <span data-ttu-id="81187-106">다른 구독의 VNet을 연결할 때 구독은 동일한 Active Directory 테넌트와 연결될 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="81187-106">When connecting VNets from different subscriptions, the subscriptions do not need to be associated with the same Active Directory tenant.</span></span> 

<span data-ttu-id="81187-107">이 문서의 단계는 Resource Manager 배포 모델에 적용되며 Azure Portal을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="81187-107">The steps in this article apply to the Resource Manager deployment model and use the Azure portal.</span></span> <span data-ttu-id="81187-108">다른 배포 도구 또는 배포 모델을 사용하는 경우 다음 목록에서 별도의 옵션을 선택하여 이 구성을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81187-108">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="81187-109">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="81187-109">Azure portal</span></span>](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [<span data-ttu-id="81187-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="81187-110">PowerShell</span></span>](vpn-gateway-vnet-vnet-rm-ps.md)
> * [<span data-ttu-id="81187-111">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="81187-111">Azure CLI</span></span>](vpn-gateway-howto-vnet-vnet-cli.md)
> * [<span data-ttu-id="81187-112">Azure Portal(클래식)</span><span class="sxs-lookup"><span data-stu-id="81187-112">Azure portal (classic)</span></span>](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [<span data-ttu-id="81187-113">다양한 배포 모델 간 연결 - Azure Portal</span><span class="sxs-lookup"><span data-stu-id="81187-113">Connect different deployment models - Azure portal</span></span>](vpn-gateway-connect-different-deployment-models-portal.md)
> * [<span data-ttu-id="81187-114">다양한 배포 모델 간 연결 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="81187-114">Connect different deployment models - PowerShell</span></span>](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

![v2v 다이어그램](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/v2vrmps.png)

<span data-ttu-id="81187-116">가상 네트워크를 다른 가상 네트워크에 연결(VNet-VNet)하는 것은 VNet을 온-프레미스 사이트 위치에 연결하는 것과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="81187-116">Connecting a virtual network to another virtual network (VNet-to-VNet) is similar to connecting a VNet to an on-premises site location.</span></span> <span data-ttu-id="81187-117">두 연결 유형 모두 VPN 게이트웨이를 사용하여 IPsec/IKE를 통한 보안 터널을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="81187-117">Both connectivity types use a VPN gateway to provide a secure tunnel using IPsec/IKE.</span></span> <span data-ttu-id="81187-118">VNet이 동일한 지역에 있는 경우 VNet 피어링을 사용하여 연결하려고 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81187-118">If your VNets are in the same region, you may want to consider connecting them using VNet Peering.</span></span> <span data-ttu-id="81187-119">VNet 피어링은 VPN Gateway를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="81187-119">VNet peering does not use a VPN gateway.</span></span> <span data-ttu-id="81187-120">자세한 내용은 [VNet 피어링](../virtual-network/virtual-network-peering-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="81187-120">For more information, see [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span>

<span data-ttu-id="81187-121">VNet-VNet 통신을 다중 사이트 구성과 결합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81187-121">VNet-to-VNet communication can be combined with multi-site configurations.</span></span> <span data-ttu-id="81187-122">이렇게 하면 다음 다이어그램에 표시된 것처럼 프레미스 간 연결을 가상 네트워크 간 연결과 결합하는 네트워크 토폴로지를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81187-122">This lets you establish network topologies that combine cross-premises connectivity with inter-virtual network connectivity, as shown in the following diagram:</span></span>

<span data-ttu-id="81187-123">![연결 정보](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/aboutconnections.png "About connections")</span><span class="sxs-lookup"><span data-stu-id="81187-123">![About connections](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/aboutconnections.png "About connections")</span></span>

### <a name="why-connect-virtual-networks"></a><span data-ttu-id="81187-124">가상 네트워크에 연결하는 이유</span><span class="sxs-lookup"><span data-stu-id="81187-124">Why connect virtual networks?</span></span>

<span data-ttu-id="81187-125">다음과 같은 이유로 가상 네트워크에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81187-125">You may want to connect virtual networks for the following reasons:</span></span>

* <span data-ttu-id="81187-126">**지역 간 지리적 중복 및 지리적 상태**</span><span class="sxs-lookup"><span data-stu-id="81187-126">**Cross region geo-redundancy and geo-presence**</span></span>
  
  * <span data-ttu-id="81187-127">인터넷 연결 끝점으로 이동하지 않고도 보안 연결을 통해 지역에서 복제 또는 동기화를 직접 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81187-127">You can set up your own geo-replication or synchronization with secure connectivity without going over Internet-facing endpoints.</span></span>
  * <span data-ttu-id="81187-128">Azure Traffic Manager 및 부하 분산 장치를 사용하여 여러 Azure 지역 간의 지리적 중복을 통해 워크로드의 가용성을 높게 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81187-128">With Azure Traffic Manager and Load Balancer, you can set up highly available workload with geo-redundancy across multiple Azure regions.</span></span> <span data-ttu-id="81187-129">이러한 작업의 한 가지 주요 예는 여러 Azure 지역에 분산된 가용성 그룹을 사용하여 SQL AlwaysOn을 설정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="81187-129">One important example is to set up SQL Always On with Availability Groups spreading across multiple Azure regions.</span></span>
* <span data-ttu-id="81187-130">**분리 또는 관리 경계를 가진 지역별 다중 계층 응용 프로그램**</span><span class="sxs-lookup"><span data-stu-id="81187-130">**Regional multi-tier applications with isolation or administrative boundary**</span></span>
  
  * <span data-ttu-id="81187-131">같은 지역 내에서 분리 또는 관리 요구 사항 때문에 여러 가상 네트워크가 함께 연결된 다중 계층 응용 프로그램을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81187-131">Within the same region, you can set up multi-tier applications with multiple virtual networks connected together due to isolation or administrative requirements.</span></span>

<span data-ttu-id="81187-132">VNet 간 연결에 대한 자세한 내용은 이 문서의 끝에 있는 [VNet 간 FAQ](#faq)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="81187-132">For more information about VNet-to-VNet connections, see the [VNet-to-VNet FAQ](#faq) at the end of this article.</span></span> <span data-ttu-id="81187-133">VNet이 다른 구독에 있으면 포털에서 연결을 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="81187-133">Note that if your VNets are in different subscriptions, you can't create the connection in the portal.</span></span> <span data-ttu-id="81187-134">[PowerShell](vpn-gateway-vnet-vnet-rm-ps.md) 또는 [CLI](vpn-gateway-howto-vnet-vnet-cli.md)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81187-134">You can use [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md) or [CLI](vpn-gateway-howto-vnet-vnet-cli.md).</span></span>

### <span data-ttu-id="81187-135"><a name="values"></a>예제 설정</span><span class="sxs-lookup"><span data-stu-id="81187-135"><a name="values"></a>Example settings</span></span>

<span data-ttu-id="81187-136">연습으로 이러한 단계를 사용하는 경우 예제 설정 값을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81187-136">When using these steps as an exercise, you can use the example settings values.</span></span> <span data-ttu-id="81187-137">예제에서는 각 VNet에 대한 여러 주소 공간을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="81187-137">For example purposes, we use multiple address spaces for each VNet.</span></span> <span data-ttu-id="81187-138">그러나 VNet 간 구성에는 여러 개의 주소 공간이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="81187-138">However, VNet-to-VNet configurations don't require multiple address spaces.</span></span>

<span data-ttu-id="81187-139">**TestVNet1에 대한 값:**</span><span class="sxs-lookup"><span data-stu-id="81187-139">**Values for TestVNet1:**</span></span>

* <span data-ttu-id="81187-140">VNet 이름: TestVNet1</span><span class="sxs-lookup"><span data-stu-id="81187-140">VNet Name: TestVNet1</span></span>
* <span data-ttu-id="81187-141">주소 공간: 10.11.0.0/16</span><span class="sxs-lookup"><span data-stu-id="81187-141">Address space: 10.11.0.0/16</span></span>
  * <span data-ttu-id="81187-142">서브넷 이름: FrontEnd</span><span class="sxs-lookup"><span data-stu-id="81187-142">Subnet name: FrontEnd</span></span>
  * <span data-ttu-id="81187-143">서브넷 주소 범위: 10.11.0.0/24</span><span class="sxs-lookup"><span data-stu-id="81187-143">Subnet address range: 10.11.0.0/24</span></span>
* <span data-ttu-id="81187-144">리소스 그룹: TestRG1</span><span class="sxs-lookup"><span data-stu-id="81187-144">Resource Group: TestRG1</span></span>
* <span data-ttu-id="81187-145">위치: 미국 동부</span><span class="sxs-lookup"><span data-stu-id="81187-145">Location: East US</span></span>
* <span data-ttu-id="81187-146">주소 공간: 10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="81187-146">Address Space: 10.12.0.0/16</span></span>
  * <span data-ttu-id="81187-147">서브넷 이름: BackEnd</span><span class="sxs-lookup"><span data-stu-id="81187-147">Subnet name: BackEnd</span></span>
  * <span data-ttu-id="81187-148">서브넷 주소 범위: 10.12.0.0/24</span><span class="sxs-lookup"><span data-stu-id="81187-148">Subnet address range: 10.12.0.0/24</span></span>
* <span data-ttu-id="81187-149">게이트웨이 서브넷 이름: GatewaySubnet (포털에서 자동으로 채워짐)</span><span class="sxs-lookup"><span data-stu-id="81187-149">Gateway Subnet name: GatewaySubnet (this will auto-fill in the portal)</span></span>
  * <span data-ttu-id="81187-150">게이트웨이 서브넷 주소 범위: 10.11.255.0/27</span><span class="sxs-lookup"><span data-stu-id="81187-150">Gateway Subnet address range: 10.11.255.0/27</span></span>
* <span data-ttu-id="81187-151">DNS 서버: DNS 서버의 IP 주소를 사용</span><span class="sxs-lookup"><span data-stu-id="81187-151">DNS Server: Use the IP address of your DNS Server</span></span>
* <span data-ttu-id="81187-152">Virtual Network 게이트웨이 이름: TestVNet1GW</span><span class="sxs-lookup"><span data-stu-id="81187-152">Virtual Network Gateway Name: TestVNet1GW</span></span>
* <span data-ttu-id="81187-153">게이트웨이 유형: VPN</span><span class="sxs-lookup"><span data-stu-id="81187-153">Gateway Type: VPN</span></span>
* <span data-ttu-id="81187-154">VPN 유형: 경로 기반</span><span class="sxs-lookup"><span data-stu-id="81187-154">VPN type: Route-based</span></span>
* <span data-ttu-id="81187-155">SKU: 사용할 게이트웨이 SKU 선택</span><span class="sxs-lookup"><span data-stu-id="81187-155">SKU: Select the Gateway SKU you want to use</span></span>
* <span data-ttu-id="81187-156">공용 IP 주소 이름: TestVNet1GWIP</span><span class="sxs-lookup"><span data-stu-id="81187-156">Public IP address name: TestVNet1GWIP</span></span>
* <span data-ttu-id="81187-157">연결 값:</span><span class="sxs-lookup"><span data-stu-id="81187-157">Connection values:</span></span>
  * <span data-ttu-id="81187-158">이름: TestVNet1toTestVNet4</span><span class="sxs-lookup"><span data-stu-id="81187-158">Name: TestVNet1toTestVNet4</span></span>
  * <span data-ttu-id="81187-159">공유 키: 공유 키를 직접 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81187-159">Shared key: You can create the shared key yourself.</span></span> <span data-ttu-id="81187-160">이 예제에서는 abc123을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="81187-160">For this example, we'll use abc123.</span></span> <span data-ttu-id="81187-161">중요한 사실은 Vnet 간의 연결을 만들 때 값이 일치해야 한다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="81187-161">The important thing is that when you create the connection between the VNets, the value must match.</span></span>

<span data-ttu-id="81187-162">**TestVNet4에 대한 값:**</span><span class="sxs-lookup"><span data-stu-id="81187-162">**Values for TestVNet4:**</span></span>

* <span data-ttu-id="81187-163">VNet 이름: TestVNet4</span><span class="sxs-lookup"><span data-stu-id="81187-163">VNet Name: TestVNet4</span></span>
* <span data-ttu-id="81187-164">주소 공간: 10.41.0.0/16</span><span class="sxs-lookup"><span data-stu-id="81187-164">Address space: 10.41.0.0/16</span></span>
  * <span data-ttu-id="81187-165">서브넷 이름: FrontEnd</span><span class="sxs-lookup"><span data-stu-id="81187-165">Subnet name: FrontEnd</span></span>
  * <span data-ttu-id="81187-166">서브넷 주소 범위: 10.41.0.0/24</span><span class="sxs-lookup"><span data-stu-id="81187-166">Subnet address range: 10.41.0.0/24</span></span>
* <span data-ttu-id="81187-167">리소스 그룹: TestRG1</span><span class="sxs-lookup"><span data-stu-id="81187-167">Resource Group: TestRG1</span></span>
* <span data-ttu-id="81187-168">위치: 미국 서부</span><span class="sxs-lookup"><span data-stu-id="81187-168">Location: West US</span></span>
* <span data-ttu-id="81187-169">주소 공간: 10.42.0.0/16</span><span class="sxs-lookup"><span data-stu-id="81187-169">Address Space: 10.42.0.0/16</span></span>
  * <span data-ttu-id="81187-170">서브넷 이름: BackEnd</span><span class="sxs-lookup"><span data-stu-id="81187-170">Subnet name: BackEnd</span></span>
  * <span data-ttu-id="81187-171">서브넷 주소 범위: 10.42.0.0/24</span><span class="sxs-lookup"><span data-stu-id="81187-171">Subnet address range: 10.42.0.0/24</span></span>
* <span data-ttu-id="81187-172">게이트웨이 서브넷 이름: GatewaySubnet (포털에서 자동으로 채워짐)</span><span class="sxs-lookup"><span data-stu-id="81187-172">GatewaySubnet name: GatewaySubnet (this will auto-fill in the portal)</span></span>
  * <span data-ttu-id="81187-173">게이트웨이 서브넷 주소 범위: 10.41.255.0/27</span><span class="sxs-lookup"><span data-stu-id="81187-173">GatewaySubnet address range: 10.41.255.0/27</span></span>
* <span data-ttu-id="81187-174">DNS 서버: DNS 서버의 IP 주소를 사용</span><span class="sxs-lookup"><span data-stu-id="81187-174">DNS Server: Use the IP address of your DNS Server</span></span>
* <span data-ttu-id="81187-175">Virtual Network 게이트웨이 이름: TestVNet4GW</span><span class="sxs-lookup"><span data-stu-id="81187-175">Virtual Network Gateway Name: TestVNet4GW</span></span>
* <span data-ttu-id="81187-176">게이트웨이 유형: VPN</span><span class="sxs-lookup"><span data-stu-id="81187-176">Gateway Type: VPN</span></span>
* <span data-ttu-id="81187-177">VPN 유형: 경로 기반</span><span class="sxs-lookup"><span data-stu-id="81187-177">VPN type: Route-based</span></span>
* <span data-ttu-id="81187-178">SKU: 사용할 게이트웨이 SKU 선택</span><span class="sxs-lookup"><span data-stu-id="81187-178">SKU: Select the Gateway SKU you want to use</span></span>
* <span data-ttu-id="81187-179">공용 IP 주소 이름: TestVNet4GWIP</span><span class="sxs-lookup"><span data-stu-id="81187-179">Public IP address name: TestVNet4GWIP</span></span>
* <span data-ttu-id="81187-180">연결 값:</span><span class="sxs-lookup"><span data-stu-id="81187-180">Connection values:</span></span>
  * <span data-ttu-id="81187-181">이름: TestVNet4toTestVNet1</span><span class="sxs-lookup"><span data-stu-id="81187-181">Name: TestVNet4toTestVNet1</span></span>
  * <span data-ttu-id="81187-182">공유 키: 공유 키를 직접 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81187-182">Shared key: You can create the shared key yourself.</span></span> <span data-ttu-id="81187-183">이 예제에서는 abc123을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="81187-183">For this example, we'll use abc123.</span></span> <span data-ttu-id="81187-184">중요한 사실은 Vnet 간의 연결을 만들 때 값이 일치해야 한다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="81187-184">The important thing is that when you create the connection between the VNets, the value must match.</span></span>

## <span data-ttu-id="81187-185"><a name="CreatVNet"></a>1. TestVNet1 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="81187-185"><a name="CreatVNet"></a>1. Create and configure TestVNet1</span></span>
<span data-ttu-id="81187-186">VNet이 이미 있는 경우 설정이 VPN 게이트웨이 설계와 호환되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="81187-186">If you already have a VNet, verify that the settings are compatible with your VPN gateway design.</span></span> <span data-ttu-id="81187-187">다른 네트워크와 겹칠 수 있는 서브넷에 특히 주의합니다.</span><span class="sxs-lookup"><span data-stu-id="81187-187">Pay particular attention to any subnets that may overlap with other networks.</span></span> <span data-ttu-id="81187-188">겹치는 서브넷에 있으면 연결이 제대로 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="81187-188">If you have overlapping subnets, your connection won't work properly.</span></span> <span data-ttu-id="81187-189">VNet이 올바른 설정으로 구성되었다면 [DNS 서버 지정](#dns) 섹션의 단계를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81187-189">If your VNet is configured with the correct settings, you can begin the steps in the [Specify a DNS server](#dns) section.</span></span>

### <a name="to-create-a-virtual-network"></a><span data-ttu-id="81187-190">가상 네트워크를 만들려면</span><span class="sxs-lookup"><span data-stu-id="81187-190">To create a virtual network</span></span>
[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-basic-vnet-rm-portal-include.md)]

## <span data-ttu-id="81187-191"><a name="subnets"></a>2. 다른 주소 공간 추가 및 서브넷 만들기</span><span class="sxs-lookup"><span data-stu-id="81187-191"><a name="subnets"></a>2. Add additional address space and create subnets</span></span>
<span data-ttu-id="81187-192">VNet이 만들어지면 여기에 다른 주소 공간을 추가하고 서브넷을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81187-192">You can add additional address space and create subnets once your VNet has been created.</span></span>

[!INCLUDE [vpn-gateway-additional-address-space](../../includes/vpn-gateway-additional-address-space-include.md)]

## <span data-ttu-id="81187-193"><a name="gatewaysubnet"></a>3. 게이트웨이 서브넷 만들기</span><span class="sxs-lookup"><span data-stu-id="81187-193"><a name="gatewaysubnet"></a>3. Create a gateway subnet</span></span>
<span data-ttu-id="81187-194">가상 네트워크를 게이트웨이에 연결하기 전에 먼저 연결하려는 가상 네트워크에 대한 게이트웨이 서브넷을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="81187-194">Before connecting your virtual network to a gateway, you first need to create the gateway subnet for the virtual network to which you want to connect.</span></span> <span data-ttu-id="81187-195">향후 추가적인 구성 요구 사항을 수용하기에 충분한 IP 주소를 제공하기 위하여 가능하면 /28 또는 /27 CIDR 블록을 사용하여 게이트웨이 서브넷을 만드는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="81187-195">If possible, it's best to create a gateway subnet using a CIDR block of /28 or /27 in order to provide enough IP addresses to accommodate additional future configuration requirements.</span></span>

<span data-ttu-id="81187-196">연습으로 이 구성을 만드는 경우 게이트웨이 서브넷을 만들 때 이러한 [예제 설정](#values)을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="81187-196">If you are creating this configuration as an exercise, refer to these [Example settings](#values) when creating your gateway subnet.</span></span>

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

### <a name="to-create-a-gateway-subnet"></a><span data-ttu-id="81187-197">게이트웨이 서브넷을 만들려면</span><span class="sxs-lookup"><span data-stu-id="81187-197">To create a gateway subnet</span></span>
[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-rm-portal-include.md)]

## <span data-ttu-id="81187-198"><a name="dns"></a>4. DNS 서버 지정(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="81187-198"><a name="dns"></a>4. Specify a DNS server (optional)</span></span>
<span data-ttu-id="81187-199">DNS는 VNet 간 연결에 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="81187-199">DNS is not required for VNet-to-VNet connections.</span></span> <span data-ttu-id="81187-200">하지만 가상 네트워크에 배포된 리소스에 대한 이름을 확인하려는 경우 DNS 서버를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="81187-200">However, if you want to have name resolution for resources that are deployed to your virtual network, you should specify a DNS server.</span></span> <span data-ttu-id="81187-201">이 설정을 통해 이 가상 네트워크에 대한 이름을 확인하는 데 사용하려는 DNS 서버를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81187-201">This setting lets you specify the DNS server that you want to use for name resolution for this virtual network.</span></span> <span data-ttu-id="81187-202">DNS 서버를 만들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="81187-202">It does not create a DNS server.</span></span>

[!INCLUDE [vpn-gateway-add-dns-rm-portal](../../includes/vpn-gateway-add-dns-rm-portal-include.md)]

## <span data-ttu-id="81187-203"><a name="VNetGateway"></a>5. 가상 네트워크 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="81187-203"><a name="VNetGateway"></a>5. Create a virtual network gateway</span></span>
<span data-ttu-id="81187-204">이 단계에서는 VNet용 가상 네트워크 게이트웨이를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="81187-204">In this step, you create the virtual network gateway for your VNet.</span></span> <span data-ttu-id="81187-205">종종 선택한 게이트웨이 SKU에 따라 게이트웨이를 만드는 데 45분 이상 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81187-205">Creating a gateway can often take 45 minutes or more, depending on the selected gateway SKU.</span></span> <span data-ttu-id="81187-206">연습으로 이 구성을 만드는 경우 [예제 설정](#values)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="81187-206">If you are creating this configuration as an exercise, you can refer to the [Example settings](#values).</span></span>

### <a name="to-create-a-virtual-network-gateway"></a><span data-ttu-id="81187-207">가상 네트워크 게이트웨이를 만들려면</span><span class="sxs-lookup"><span data-stu-id="81187-207">To create a virtual network gateway</span></span>
[!INCLUDE [vpn-gateway-add-gw-rm-portal](../../includes/vpn-gateway-add-gw-rm-portal-include.md)]

## <span data-ttu-id="81187-208"><a name="CreateTestVNet4"></a>6. TestVNet4 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="81187-208"><a name="CreateTestVNet4"></a>6. Create and configure TestVNet4</span></span>
<span data-ttu-id="81187-209">TestVNet1를 구성한 후 TestVNet4 TestVNet4의 값을 대체하고 이전 단계를 반복하여 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="81187-209">Once you've configured TestVNet1, create TestVNet4 by repeating the previous steps, replacing the values with those of TestVNet4.</span></span> <span data-ttu-id="81187-210">TestVNet1에 대한 가상 네트워크 게이트웨이 만들기 TestVNet4 구성하기 전에 끝날 때까지 기다릴 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="81187-210">You don't need to wait until the virtual network gateway for TestVNet1 has finished creating before configuring TestVNet4.</span></span> <span data-ttu-id="81187-211">고유한 값을 사용하는 경우에 주소 공간에 연결하려는 Vnet를 사용하여 겹치지 않는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="81187-211">If you are using your own values, make sure that the address spaces don't overlap with any of the VNets that you want to connect to.</span></span>

## <span data-ttu-id="81187-212"><a name="TestVNet1Connection"></a>7. TestVNet1 연결 구성</span><span class="sxs-lookup"><span data-stu-id="81187-212"><a name="TestVNet1Connection"></a>7. Configure the TestVNet1 connection</span></span>
<span data-ttu-id="81187-213">가상 네트워크 게이트웨이 TestVNet1 및 TestVNet4를 모두 완료했을 때 게이트웨이 연결 가상 네트워크를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81187-213">When the virtual network gateways for both TestVNet1 and TestVNet4 have completed, you can create your virtual network gateway connections.</span></span> <span data-ttu-id="81187-214">이 섹션에서는 VNet1에서 VNet4에 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="81187-214">In this section, you will create a connection from VNet1 to VNet4.</span></span> <span data-ttu-id="81187-215">이러한 단계는 동일한 구독에 있는 Vnet에 대해서만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="81187-215">These steps work only for VNets in the same subscription.</span></span> <span data-ttu-id="81187-216">Vnet이 다른 구독에 있으면 PowerShell을 사용하여 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="81187-216">If your VNets are in different subscriptions, you must use PowerShell to make the connection.</span></span> <span data-ttu-id="81187-217">[PowerShell](vpn-gateway-vnet-vnet-rm-ps.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="81187-217">See the [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md) article.</span></span>

1. <span data-ttu-id="81187-218">**모든 리소스**에서, VNet에 대한 가상 네트워크 게이트웨이로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="81187-218">In **All resources**, navigate to the virtual network gateway for your VNet.</span></span> <span data-ttu-id="81187-219">예를 들어 **TestVNet1GW**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="81187-219">For example, **TestVNet1GW**.</span></span> <span data-ttu-id="81187-220">**TestVNet1GW**를 클릭하여 가상 네트워크 게이트웨이 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="81187-220">Click **TestVNet1GW** to open the virtual network gateway blade.</span></span>
   
    <span data-ttu-id="81187-221">![연결 블레이드](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/settings_connection.png "Connections blade")</span><span class="sxs-lookup"><span data-stu-id="81187-221">![Connections blade](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/settings_connection.png "Connections blade")</span></span>
2. <span data-ttu-id="81187-222">**+ 추가**를 클릭하여 **연결 추가** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="81187-222">Click **+Add** to open the **Add connection** blade.</span></span>
3. <span data-ttu-id="81187-223">**연결 추가** 블레이드에서 이름 필드에 연결에 대한 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="81187-223">On the **Add connection** blade, in the name field, type a name for your connection.</span></span> <span data-ttu-id="81187-224">예를 들어, **TestVNet1toTestVNet4**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="81187-224">For example, **TestVNet1toTestVNet4**.</span></span>
   
    <span data-ttu-id="81187-225">![연결 이름](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/v1tov4.png "Connection name")</span><span class="sxs-lookup"><span data-stu-id="81187-225">![Connection name](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/v1tov4.png "Connection name")</span></span>
4. <span data-ttu-id="81187-226">**연결 형식**은</span><span class="sxs-lookup"><span data-stu-id="81187-226">For **Connection type**.</span></span> <span data-ttu-id="81187-227">드롭다운에서 **VNet-VNet**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="81187-227">select **VNet-to-VNet** from the dropdown.</span></span>
5. <span data-ttu-id="81187-228">**첫 번째 가상 네트워크 게이트웨이** 필드 값은 지정된 가상 네트워크 게이트웨이에서 이 연결을 만들고 있으므로 자동으로 입력됩니다.</span><span class="sxs-lookup"><span data-stu-id="81187-228">The **First virtual network gateway** field value is automatically filled in because you are creating this connection from the specified virtual network gateway.</span></span>
6. <span data-ttu-id="81187-229">**두 번째 가상 네트워크 게이트웨이** 필드는 연결을 만들고자 하는 VNet의 가상 네트워크 게이트웨이입니다.</span><span class="sxs-lookup"><span data-stu-id="81187-229">The **Second virtual network gateway** field is the virtual network gateway of the VNet that you want to create a connection to.</span></span> <span data-ttu-id="81187-230">**다른 가상 네트워크 게이트웨이 선택**을 클릭하여 **선택 가상 네트워크 게이트웨이** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="81187-230">Click **Choose another virtual network gateway** to open the **Choose virtual network gateway** blade.</span></span>
   
    <span data-ttu-id="81187-231">![연결 추가](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/add_connection.png "Add a connection")</span><span class="sxs-lookup"><span data-stu-id="81187-231">![Add connection](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/add_connection.png "Add a connection")</span></span>
7. <span data-ttu-id="81187-232">이 블레이드에 나열된 가상 네트워크 게이트웨이를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="81187-232">View the virtual network gateways that are listed on this blade.</span></span> <span data-ttu-id="81187-233">구독에 있는 가상 네트워크 게이트웨이만 나열되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="81187-233">Notice that only virtual network gateways that are in your subscription are listed.</span></span> <span data-ttu-id="81187-234">구독에 있지 않은 가상 네트워크 게이트웨이에 연결하려는 경우에 [PowerShell 문서](vpn-gateway-vnet-vnet-rm-ps.md)를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="81187-234">If you want to connect to a virtual network gateway that is not in your subscription, please use the [PowerShell article](vpn-gateway-vnet-vnet-rm-ps.md).</span></span> 
8. <span data-ttu-id="81187-235">연결하려는 가상 네트워크 게이트웨이를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="81187-235">Click the virtual network gateway that you want to connect to.</span></span>
9. <span data-ttu-id="81187-236">**공유 키** 필드에서 연결에 대한 공유 키를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="81187-236">In the **Shared key** field, type a shared key for your connection.</span></span> <span data-ttu-id="81187-237">이 키를 생성하거나 직접 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81187-237">You can generate or create this key yourself.</span></span> <span data-ttu-id="81187-238">사이트 간 연결에서 사용되는 키는 온-프레미스 장치 및 가상 네트워크 게이트웨이 연결에서 사용하는 키와 정확히 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="81187-238">In a site-to-site connection, the key you use would be exactly the same for your on-premises device and your virtual network gateway connection.</span></span> <span data-ttu-id="81187-239">개념은 비슷하지만 여기에서는 VPN 장치에 연결하지 않고, 다른 가상 네트워크 게이트웨이를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="81187-239">The concept is similar here, except that rather than connecting to a VPN device, you are connecting to another virtual network gateway.</span></span>
   
    <span data-ttu-id="81187-240">![공유 키](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/sharedkey.png "Shared key")</span><span class="sxs-lookup"><span data-stu-id="81187-240">![Shared key](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/sharedkey.png "Shared key")</span></span>
10. <span data-ttu-id="81187-241">블레이드의 맨 아래에서 **확인**을 클릭하여 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="81187-241">Click **OK** at the bottom of the blade to save your changes.</span></span>

## <span data-ttu-id="81187-242"><a name="TestVNet4Connection"></a>8. TestVNet4 연결 구성</span><span class="sxs-lookup"><span data-stu-id="81187-242"><a name="TestVNet4Connection"></a>8. Configure the TestVNet4 connection</span></span>
<span data-ttu-id="81187-243">다음으로 TestVNet4에서 TestVNet1에 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="81187-243">Next, create a connection from TestVNet4 to TestVNet1.</span></span> <span data-ttu-id="81187-244">TestVNet1에서 TestVNet4에 연결을 만드는 데 사용한 것과 동일한 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="81187-244">Use the same method that you used to create the connection from TestVNet1 to TestVNet4.</span></span> <span data-ttu-id="81187-245">동일한 공유 키를 사용하고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="81187-245">Make sure that you use the same shared key.</span></span>

## <span data-ttu-id="81187-246"><a name="VerifyConnection"></a>9. 연결 확인</span><span class="sxs-lookup"><span data-stu-id="81187-246"><a name="VerifyConnection"></a>9. Verify your connection</span></span>
<span data-ttu-id="81187-247">연결을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="81187-247">Verify the connection.</span></span> <span data-ttu-id="81187-248">각 가상 네트워크 게이트웨이에 대해 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="81187-248">For each virtual network gateway, do the following:</span></span>

1. <span data-ttu-id="81187-249">가상 네트워크 게이트웨이에 대한 블레이드를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="81187-249">Locate the blade for the virtual network gateway.</span></span> <span data-ttu-id="81187-250">예를 들어 **TestVNet4GW**를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="81187-250">For example, **TestVNet4GW**.</span></span> 
2. <span data-ttu-id="81187-251">가상 네트워크 게이트웨이 블레이드에서 **연결**을 클릭하여 가상 네트워크 게이트웨이에 대한 연결 블레이드를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="81187-251">On the virtual network gateway blade, click **Connections** to view the connections blade for the virtual network gateway.</span></span>

<span data-ttu-id="81187-252">연결을 보고 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="81187-252">View the connections and verify the status.</span></span> <span data-ttu-id="81187-253">연결이 설정되면 상태 값으로 **Succeeded** 및 **Connected**가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="81187-253">Once the connection is created, you will see **Succeeded** and **Connected** as the Status values.</span></span>

<span data-ttu-id="81187-254">![성공](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/connected.png "Succeeded")</span><span class="sxs-lookup"><span data-stu-id="81187-254">![Succeeded](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/connected.png "Succeeded")</span></span>

<span data-ttu-id="81187-255">연결에 대한 자세한 내용을 보려면 개별적으로 각 연결을 두 번 클릭하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="81187-255">You can double-click each connection separately to view more information about the connection.</span></span>

<span data-ttu-id="81187-256">![Essentials](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/essentials.png "Essentials")</span><span class="sxs-lookup"><span data-stu-id="81187-256">![Essentials](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/essentials.png "Essentials")</span></span>

## <span data-ttu-id="81187-257"><a name="faq"></a>VNet 간 FAQ</span><span class="sxs-lookup"><span data-stu-id="81187-257"><a name="faq"></a>VNet-to-VNet FAQ</span></span>
<span data-ttu-id="81187-258">VNet 간 연결에 대한 자세한 내용은 FAQ 세부 정보를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="81187-258">View the FAQ details for additional information about VNet-to-VNet connections.</span></span>

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="81187-259">다음 단계</span><span class="sxs-lookup"><span data-stu-id="81187-259">Next steps</span></span>
<span data-ttu-id="81187-260">연결이 완료되면 가상 네트워크에 가상 컴퓨터를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81187-260">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="81187-261">자세한 내용은 [Virtual Machines 설명서](https://docs.microsoft.com/azure/#pivot=services&panel=Compute)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="81187-261">See the [Virtual Machines documentation](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) for more information.</span></span>

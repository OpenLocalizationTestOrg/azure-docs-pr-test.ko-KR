---
title: "공존할 수 있는 ExpressRoute 및 사이트 간 VPN 연결 구성: Resource Manager: Azure | Microsoft Docs"
description: "이 문서에서는 Resource Manager 모델에 대해 공존할 수 있는 ExpressRoute와 사이트 간 VPN 연결을 구성하는 과정을 안내합니다."
documentationcenter: na
services: expressroute
author: charwen
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c7717b14-3da3-4a6d-b78e-a5020766bc2c
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/19/2017
ms.author: charwen,cherylmc
ms.openlocfilehash: b29147a37f9a90fc80e16b350ac9b91daac1d7f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-expressroute-and-site-to-site-coexisting-connections"></a><span data-ttu-id="2938f-103">ExpressRoute 및 사이트 간 공존 연결 구성</span><span class="sxs-lookup"><span data-stu-id="2938f-103">Configure ExpressRoute and Site-to-Site coexisting connections</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2938f-104">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2938f-104">PowerShell - Resource Manager</span></span>](expressroute-howto-coexist-resource-manager.md)
> * [<span data-ttu-id="2938f-105">PowerShell - 클래식</span><span class="sxs-lookup"><span data-stu-id="2938f-105">PowerShell - Classic</span></span>](expressroute-howto-coexist-classic.md)
> 
> 

<span data-ttu-id="2938f-106">사이트 간 VPN과 ExpressRoute가 공존하는 연결을 구성하면 여러 장점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-106">Configuring Site-to-Site VPN and ExpressRoute coexisting connections has several advantages.</span></span> <span data-ttu-id="2938f-107">사이트 간 VPN을 ExpressRoute 보안 장애 조치(failover) 경로로 구성하거나 사이트 간 VPN을 사용하여 ExpressRoute를 통해 연결되지 않은 사이트에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-107">You can configure a Site-to-Site VPN as a secure failover path for ExressRoute, or use Site-to-Site VPNs to connect to sites that are not connected through ExpressRoute.</span></span> <span data-ttu-id="2938f-108">이 문서에서는 두 시나리오를 모두 구성하는 단계를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-108">We cover the steps to configure both scenarios in this article.</span></span> <span data-ttu-id="2938f-109">이 문서는 Resource Manager 배포 모델에 적용되며 PowerShell을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-109">This article applies to the Resource Manager deployment model and uses PowerShell.</span></span> <span data-ttu-id="2938f-110">이 구성은 Azure 포털에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-110">This configuration is not available in the Azure portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2938f-111">ExpressRoute 회로는 아래 지침을 수행하기 전에 미리 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-111">ExpressRoute circuits must be pre-configured before you follow the instructions below.</span></span> <span data-ttu-id="2938f-112">계속 진행하기 전에 [ExpressRoute 회로 만들기](expressroute-howto-circuit-arm.md) 및 [라우팅 구성](expressroute-howto-routing-arm.md) 지침을 수행했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-112">Make sure that you have followed the guides to [create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and [configure routing](expressroute-howto-routing-arm.md) before you proceed.</span></span>
> 
> 

## <a name="limits-and-limitations"></a><span data-ttu-id="2938f-113">제한 및 제한 사항</span><span class="sxs-lookup"><span data-stu-id="2938f-113">Limits and limitations</span></span>
* <span data-ttu-id="2938f-114">**통과 라우팅이 지원되지 않습니다.**</span><span class="sxs-lookup"><span data-stu-id="2938f-114">**Transit routing is not supported.**</span></span> <span data-ttu-id="2938f-115">사이트 간 VPN을 통해 연결된 로컬 네트워크와 ExpressRoute를 통해 연결된 로컬 네트워크 사이는 Azure를 통해 라우팅할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-115">You cannot route (via Azure) between your local network connected via Site-to-Site VPN and your local network connected via ExpressRoute.</span></span>
* <span data-ttu-id="2938f-116">**기본 SKU 게이트웨이는 지원되지 않습니다.**</span><span class="sxs-lookup"><span data-stu-id="2938f-116">**Basic SKU gateway is not supported.**</span></span> <span data-ttu-id="2938f-117">[ExpressRoute 게이트웨이](expressroute-about-virtual-network-gateways.md) 및 [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md) 모두에 기본이 아닌 SKU 게이트웨이를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-117">You must use a non-Basic SKU gateway for both the [ExpressRoute gateway](expressroute-about-virtual-network-gateways.md) and the [VPN gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="2938f-118">**경로 기반 VPN Gateway만 지원됩니다.**</span><span class="sxs-lookup"><span data-stu-id="2938f-118">**Only route-based VPN gateway is supported.**</span></span> <span data-ttu-id="2938f-119">경로 기반 [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md)를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-119">You must use a route-based [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="2938f-120">**VPN Gateway에 고정 경로를 구성해야 합니다.**</span><span class="sxs-lookup"><span data-stu-id="2938f-120">**Static route should be configured for your VPN gateway.**</span></span> <span data-ttu-id="2938f-121">로컬 네트워크가 ExpressRoute 및 사이트 간 VPN 모두에 연결된 경우 로컬 네트워크에서 정적 경로를 구성하여 사이트 간 VPN 연결을 공용 인터넷에 라우팅해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-121">If your local network is connected to both ExpressRoute and a Site-to-Site VPN, you must have a static route configured in your local network to route the Site-to-Site VPN connection to the public Internet.</span></span>
* <span data-ttu-id="2938f-122">**ExpressRoute 게이트웨이를 먼저 구성하여 회로에 연결해야 합니다.**</span><span class="sxs-lookup"><span data-stu-id="2938f-122">**ExpressRoute gateway must be configured first and linked to a circuit.**</span></span> <span data-ttu-id="2938f-123">사이트 간 VPN Gateway를 추가하기 전에 ExpressRoute 게이트웨이를 먼저 만들고 회로에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-123">You must create the ExpressRoute gateway first and link it to a circuit before you add the Site-to-Site VPN gateway.</span></span>

## <a name="configuration-designs"></a><span data-ttu-id="2938f-124">구성 디자인</span><span class="sxs-lookup"><span data-stu-id="2938f-124">Configuration designs</span></span>
### <a name="configure-a-site-to-site-vpn-as-a-failover-path-for-expressroute"></a><span data-ttu-id="2938f-125">사이트 간 VPN을 ExpressRoute에 대한 장애 조치(failover) 경로로 구성</span><span class="sxs-lookup"><span data-stu-id="2938f-125">Configure a Site-to-Site VPN as a failover path for ExpressRoute</span></span>
<span data-ttu-id="2938f-126">ExpressRoute에 대한 백업으로 사이트 간 VPN 연결을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-126">You can configure a Site-to-Site VPN connection as a backup for ExpressRoute.</span></span> <span data-ttu-id="2938f-127">Azure 개인 피어링 경로에 연결된 가상 네트워크에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-127">This applies only to virtual networks linked to the Azure private peering path.</span></span> <span data-ttu-id="2938f-128">공용 Azure 및 Microsoft 피어링을 통해 액세스할 수 있는 서비스에 대한 VPN 기반 장애 조치 솔루션은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-128">There is no VPN-based failover solution for services accessible through Azure public and Microsoft peerings.</span></span> <span data-ttu-id="2938f-129">ExpressRoute 회로는 항상 기본 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-129">The ExpressRoute circuit is always the primary link.</span></span> <span data-ttu-id="2938f-130">ExpressRoute 회로가 실패하면 데이터는 사이트 간 VPN 경로를 통해 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-130">Data flows through the Site-to-Site VPN path only if the ExpressRoute circuit fails.</span></span>

> [!NOTE]
> <span data-ttu-id="2938f-131">두 경로가 동일한 경우 사이트 간 VPN보다 ExpressRoute 회로가 사용되며, Azure는 가장 긴 접두사 일치 항목을 사용하여 패킷의 대상에 대한 경로를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-131">While ExpressRoute circuit is preferred over Site-to-Site VPN when both routes are the same, Azure will use the longest prefix match to choose the route towards the packet's destination.</span></span>
> 
> 

![공존](media/expressroute-howto-coexist-resource-manager/scenario1.jpg)

### <a name="configure-a-site-to-site-vpn-to-connect-to-sites-not-connected-through-expressroute"></a><span data-ttu-id="2938f-133">사이트 간 VPN을 구성하여 ExpressRoute를 통해 연결되지 않은 사이트에 연결</span><span class="sxs-lookup"><span data-stu-id="2938f-133">Configure a Site-to-Site VPN to connect to sites not connected through ExpressRoute</span></span>
<span data-ttu-id="2938f-134">일부 사이트는 사이트 간 VPN을 통해 Azure에 직접 연결하고 일부 사이트는 ExpressRoute를 통해 연결된 네트워크를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-134">You can configure your network where some sites connect directly to Azure over Site-to-Site VPN, and some sites connect through ExpressRoute.</span></span> 

![공존](media/expressroute-howto-coexist-resource-manager/scenario2.jpg)

> [!NOTE]
> <span data-ttu-id="2938f-136">가상 네트워크를 중계 라우터로 구성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-136">You cannot configure a virtual network as a transit router.</span></span>
> 
> 

## <a name="selecting-the-steps-to-use"></a><span data-ttu-id="2938f-137">사용할 단계 선택</span><span class="sxs-lookup"><span data-stu-id="2938f-137">Selecting the steps to use</span></span>
<span data-ttu-id="2938f-138">두 가지 절차 중에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-138">There are two different sets of procedures to choose from.</span></span> <span data-ttu-id="2938f-139">연결할 기존 가상 네트워크가 있는지 아니면 새 가상 네트워크를 만들 것인지에 따라 구성 절차를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-139">The configuration procedure that you select depends on whether you have an existing virtual network that you want to connect to, or you want to create a new virtual network.</span></span>

* <span data-ttu-id="2938f-140">VNet이 없어서 만들어야 하는 경우</span><span class="sxs-lookup"><span data-stu-id="2938f-140">I don't have a VNet and need to create one.</span></span>
  
    <span data-ttu-id="2938f-141">가상 네트워크가 아직 없는 경우 이 절차에서는 Resource Manager 배포 모델을 사용하여 새 가상 네트워크를 만들고 새 ExpressRoute 및 사이트 간 VPN 연결을 만드는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-141">If you don’t already have a virtual network, this procedure walks you through creating a new virtual network using Resource Manager deployment model and creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="2938f-142">가상 네트워크를 구성하려면 [새 가상 네트워크 및 공존 연결을 만들려면](#new) 섹션의 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-142">To configure a virtual network, follow the steps in [To create a new virtual network and coexisting connections](#new).</span></span>
* <span data-ttu-id="2938f-143">이미 Resource Manager 배포 모델 VNet이 있는 경우</span><span class="sxs-lookup"><span data-stu-id="2938f-143">I already have a Resource Manager deployment model VNet.</span></span>
  
    <span data-ttu-id="2938f-144">기존 사이트 간 VPN 또는 ExpressRoute에 연결된 가상 네트워크가 이미 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-144">You may already have a virtual network in place with an existing Site-to-Site VPN connection or ExpressRoute connection.</span></span> <span data-ttu-id="2938f-145">[기존 VNet에 대해 공존 연결을 구성하려면](#add) 섹션에서는 게이트웨이를 삭제한 다음 새 ExpressRoute 및 사이트 간 VPN 연결을 만드는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-145">The [To configure coexisting connections for an already existing VNet](#add) section walks you through deleting the gateway, and then creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="2938f-146">새 연결을 만들 때 특정 순서대로 단계를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-146">When creating the new connections, the steps must be completed in a specific order.</span></span> <span data-ttu-id="2938f-147">게이트웨이 및 연결을 만들 때 다른 문서의 지침을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="2938f-147">Don't use the instructions in other articles to create your gateways and connections.</span></span>
  
    <span data-ttu-id="2938f-148">이 절차에서, 공존할 수 있는 연결을 만들려면 게이트웨이를 삭제한 다음 새 게이트웨이를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-148">In this procedure, creating connections that can coexist requires you to delete your gateway, and then configure new gateways.</span></span> <span data-ttu-id="2938f-149">게이트웨이 및 연결을 삭제하고 다시 만드는 동안 크로스-프레미스 연결의 가동 중지 시간이 발생하지만 VM 또는 서비스를 새 가상 네트워크로 마이그레이션할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-149">You will have downtime for your cross-premises connections while you delete and recreate your gateway and connections, but you will not need to migrate any of your VMs or services to a new virtual network.</span></span> <span data-ttu-id="2938f-150">VM 및 서비스는 그렇게 구성된 경우 게이트웨이를 구성하는 동안 부하 분산 장치를 통해 계속 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-150">Your VMs and services will still be able to communicate out through the load balancer while you configure your gateway if they are configured to do so.</span></span>

## <span data-ttu-id="2938f-151"><a name="new"></a>새 가상 네트워크 및 공존 연결을 만들려면</span><span class="sxs-lookup"><span data-stu-id="2938f-151"><a name="new"></a>To create a new virtual network and coexisting connections</span></span>
<span data-ttu-id="2938f-152">이 절차에서는 공존하는 VNet 연결과 사이트 간 및 ExpressRoute 연결을 만드는 방법을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-152">This procedure walks you through creating a VNet and Site-to-Site and ExpressRoute connections that will coexist.</span></span>

1. <span data-ttu-id="2938f-153">최신 버전의 Azure PowerShell cmdlet을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-153">Install the latest version of the Azure PowerShell cmdlets.</span></span> <span data-ttu-id="2938f-154">cmdlet 설치에 대한 자세한 내용은 [Azure PowerShell 설치 및 구성 방법](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2938f-154">For information about installing the cmdlets, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="2938f-155">이 구성에 사용할 cmdlet은 지금까지 사용하던 것과 약간 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-155">The cmdlets that you use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="2938f-156">다음 지침에 지정된 cmdlet을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-156">Be sure to use the cmdlets specified in these instructions.</span></span>
2. <span data-ttu-id="2938f-157">계정에 로그인하여 환경을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-157">Log in to your account and set up the environment.</span></span>

  ```powershell
  login-AzureRmAccount
  Select-AzureRmSubscription -SubscriptionName 'yoursubscription'
  $location = "Central US"
  $resgrp = New-AzureRmResourceGroup -Name "ErVpnCoex" -Location $location
  $VNetASN = 65010
  ```
3. <span data-ttu-id="2938f-158">게이트웨이 서브넷을 포함하여 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-158">Create a virtual network including Gateway Subnet.</span></span> <span data-ttu-id="2938f-159">가상 네트워크 구성에 대한 자세한 내용은 [Azure Virtual Network 구성](../virtual-network/virtual-networks-create-vnet-arm-ps.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2938f-159">For more information about the virtual network configuration, see [Azure Virtual Network configuration](../virtual-network/virtual-networks-create-vnet-arm-ps.md).</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="2938f-160">게이트웨이 서브넷은 /27 또는 더 짧은 접두사(예: /26 또는 /25)여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-160">The Gateway Subnet must be /27 or a shorter prefix (such as /26 or /25).</span></span>
   > 
   > 
   
    <span data-ttu-id="2938f-161">새 VNet을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-161">Create a new VNet.</span></span>

  ```powershell
  $vnet = New-AzureRmVirtualNetwork -Name "CoexVnet" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AddressPrefix "10.200.0.0/16"
  ```
   
    <span data-ttu-id="2938f-162">서브넷을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-162">Add subnets.</span></span>

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name "App" -VirtualNetwork $vnet -AddressPrefix "10.200.1.0/24"
  Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet -AddressPrefix "10.200.255.0/24"
  ```
   
    <span data-ttu-id="2938f-163">VNet 구성을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-163">Save the VNet configuration.</span></span>

  ```powershell
  $vnet = Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
4. <span data-ttu-id="2938f-164"><a name="gw"></a>ExpressRoute 게이트웨이를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-164"><a name="gw"></a>Create an ExpressRoute gateway.</span></span> <span data-ttu-id="2938f-165">ExpressRoute 게이트웨이 구성에 대한 자세한 내용은 [ExpressRoute 게이트웨이 구성](expressroute-howto-add-gateway-resource-manager.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2938f-165">For more information about the ExpressRoute gateway configuration, see [ExpressRoute gateway configuration](expressroute-howto-add-gateway-resource-manager.md).</span></span> <span data-ttu-id="2938f-166">GatewaySKU는 *Standard*, *HighPerformance* 또는 *UltraPerformance*이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-166">The GatewaySKU must be *Standard*, *HighPerformance*, or *UltraPerformance*.</span></span>

  ```powershell
  $gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $gwIP = New-AzureRmPublicIpAddress -Name "ERGatewayIP" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AllocationMethod Dynamic
  $gwConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "ERGatewayIpConfig" -SubnetId $gwSubnet.Id -PublicIpAddressId $gwIP.Id
  $gw = New-AzureRmVirtualNetworkGateway -Name "ERGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "ExpressRoute" -GatewaySku Standard
  ```
5. <span data-ttu-id="2938f-167">ExpressRoute 게이트웨이를 ExpressRoute 회로에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-167">Link the ExpressRoute gateway to the ExpressRoute circuit.</span></span> <span data-ttu-id="2938f-168">이 단계를 완료하면 ExpressRoute를 통해 온-프레미스 네트워크와 Azure 간의 연결이 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-168">After this step has been completed, the connection between your on-premises network and Azure, through ExpressRoute, is established.</span></span> <span data-ttu-id="2938f-169">링크 작업에 대한 자세한 내용은 [Vnet을 ExpressRoute에 연결](expressroute-howto-linkvnet-arm.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2938f-169">For more information about the link operation, see [Link VNets to ExpressRoute](expressroute-howto-linkvnet-arm.md).</span></span>

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "YourCircuit" -ResourceGroupName "YourCircuitResourceGroup"
  New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -VirtualNetworkGateway1 $gw -PeerId $ckt.Id -ConnectionType ExpressRoute
  ```
6. <span data-ttu-id="2938f-170"><a name="vpngw"></a>그런 다음 사이트 간 VPN Gateway를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-170"><a name="vpngw"></a>Next, create your Site-to-Site VPN gateway.</span></span> <span data-ttu-id="2938f-171">VPN Gateway 구성에 대한 자세한 내용은 [사이트 간 연결로 VNet 구성](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2938f-171">For more information about the VPN gateway configuration, see [Configure a VNet with a Site-to-Site connection](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md).</span></span> <span data-ttu-id="2938f-172">GatewaySKU는 *Standard*, *HighPerformance* 또는 *UltraPerformance*이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-172">The GatewaySKU must be *Standard*, *HighPerformance*, or *UltraPerformance*.</span></span> <span data-ttu-id="2938f-173">VpnType은 *RouteBased*여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-173">The VpnType must *RouteBased*.</span></span>

  ```powershell
  $gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $gwIP = New-AzureRmPublicIpAddress -Name "VPNGatewayIP" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AllocationMethod Dynamic
  $gwConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "VPNGatewayIpConfig" -SubnetId $gwSubnet.Id -PublicIpAddressId $gwIP.Id
  New-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "Vpn" -VpnType "RouteBased" -GatewaySku "Standard"
  ```
   
    <span data-ttu-id="2938f-174">Azure VPN Gateway는 BGP 라우팅 프로토콜을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-174">Azure VPN gateway supports BGP routing protocol.</span></span> <span data-ttu-id="2938f-175">다음 명령에서 -Asn 스위치를 추가하여 해당 Virtual Network에 대해 ASN(AS 번호)을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-175">You can specify ASN (AS Number) for that Virtual Network by adding the -Asn switch in the following command.</span></span> <span data-ttu-id="2938f-176">매개 변수를 지정하지 않으면 AS 번호는 기본적으로 65515가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-176">Not specifying that parameter will default to AS number 65515.</span></span>

  ```powershell
  $azureVpn = New-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "Vpn" -VpnType "RouteBased" -GatewaySku "Standard" -Asn $VNetASN
  ```
   
    <span data-ttu-id="2938f-177">Azure가 $azureVpn.BgpSettings.BgpPeeringAddress 및 $azureVpn.BgpSettings.Asn에서 VPN Gateway에 사용하는 BGP 피어링 IP 및 AS 번호를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-177">You can find the BGP peering IP and the AS number that Azure uses for the VPN gateway in $azureVpn.BgpSettings.BgpPeeringAddress and $azureVpn.BgpSettings.Asn.</span></span> <span data-ttu-id="2938f-178">자세한 내용은 Azure VPN Gateway에 대한 [BGP 구성](../vpn-gateway/vpn-gateway-bgp-resource-manager-ps.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2938f-178">For more information, see [Configure BGP](../vpn-gateway/vpn-gateway-bgp-resource-manager-ps.md) for Azure VPN gateway.</span></span>
7. <span data-ttu-id="2938f-179">로컬 사이트 VPN Gateway 엔터티를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-179">Create a local site VPN gateway entity.</span></span> <span data-ttu-id="2938f-180">이 명령은 온-프레미스 VPN Gateway를 구성하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-180">This command doesn’t configure your on-premises VPN gateway.</span></span> <span data-ttu-id="2938f-181">대신, Azure VPN Gateway를 연결할 수 있도록 공용 IP 주소 및 온-프레미스 주소 공간과 같은 로컬 게이트웨이 설정을 제공할 수 있게 해줍니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-181">Rather, it allows you to provide the local gateway settings, such as the public IP and the on-premises address space, so that the Azure VPN gateway can connect to it.</span></span>
   
    <span data-ttu-id="2938f-182">로컬 VPN 장치가 고정 라우팅만을 지원하는 경우 다음과 같은 방식으로 고정 경로를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-182">If your local VPN device only supports static routing, you can configure the static routes in the following way:</span></span>

  ```powershell
  $MyLocalNetworkAddress = @("10.100.0.0/16","10.101.0.0/16","10.102.0.0/16")
  $localVpn = New-AzureRmLocalNetworkGateway -Name "LocalVPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -GatewayIpAddress *<Public IP>* -AddressPrefix $MyLocalNetworkAddress
  ```
   
    <span data-ttu-id="2938f-183">로컬 VPN 장치가 BGP를 지원하고 동적 라우팅을 사용하도록 설정하려는 경우 로컬 VPN 장치가 사용하는 BGP 피어링 IP 및 AS 번호를 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-183">If your local VPN device supports the BGP and you want to enable dynamic routing, you need to know the BGP peering IP and the AS number that your local VPN device uses.</span></span>

  ```powershell
  $localVPNPublicIP = "<Public IP>"
  $localBGPPeeringIP = "<Private IP for the BGP session>"
  $localBGPASN = "<ASN>"
  $localAddressPrefix = $localBGPPeeringIP + "/32"
  $localVpn = New-AzureRmLocalNetworkGateway -Name "LocalVPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -GatewayIpAddress $localVPNPublicIP -AddressPrefix $localAddressPrefix -BgpPeeringAddress $localBGPPeeringIP -Asn $localBGPASN
  ```
8. <span data-ttu-id="2938f-184">새 Azure VPN Gateway에 연결할 로컬 VPN 장치를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-184">Configure your local VPN device to connect to the new Azure VPN gateway.</span></span> <span data-ttu-id="2938f-185">VPN 장치 구성에 대한 자세한 내용은 [VPN 장치 구성](../vpn-gateway/vpn-gateway-about-vpn-devices.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2938f-185">For more information about VPN device configuration, see [VPN Device Configuration](../vpn-gateway/vpn-gateway-about-vpn-devices.md).</span></span>
9. <span data-ttu-id="2938f-186">Azure의 사이트 간 VPN Gateway를 로컬 게이트웨이에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-186">Link the Site-to-Site VPN gateway on Azure to the local gateway.</span></span>

  ```powershell
  $azureVpn = Get-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName
  New-AzureRmVirtualNetworkGatewayConnection -Name "VPNConnection" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -VirtualNetworkGateway1 $azureVpn -LocalNetworkGateway2 $localVpn -ConnectionType IPsec -SharedKey <yourkey>
  ```

## <span data-ttu-id="2938f-187"><a name="add"></a>기존 VNet에 대한 공존 연결을 구성하려면</span><span class="sxs-lookup"><span data-stu-id="2938f-187"><a name="add"></a>To configure coexisting connections for an already existing VNet</span></span>
<span data-ttu-id="2938f-188">기존 가상 네트워크가 있는 경우 게이트웨이 서브넷 크기를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-188">If you have an existing virtual network, check the gateway subnet size.</span></span> <span data-ttu-id="2938f-189">게이트웨이 서브넷이 /28 또는 /29인 경우 우선 가상 네트워크 게이트웨이를 삭제하고 게이트웨이 서브넷 크기를 늘려야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-189">If the gateway subnet is /28 or /29, you must first delete the virtual network gateway and increase the gateway subnet size.</span></span> <span data-ttu-id="2938f-190">이 섹션에서 단계별 수행 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-190">The steps in this section show you how to do that.</span></span>

<span data-ttu-id="2938f-191">게이트웨어 서브넷이 /27 이상이고 가상 네트워크가 ExpressRoute를 통해 연결된 경우 아래 단계를 건너뛰고 이전 섹션의 ["6단계 - 사이트 간 VPN Gateway 만들기"](#vpngw) 를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-191">If the gateway subnet is /27 or larger and the virtual network is connected via ExpressRoute, you can skip the steps below and proceed to ["Step 6 - Create a Site-to-Site VPN gateway"](#vpngw) in the previous section.</span></span> 

> [!NOTE]
> <span data-ttu-id="2938f-192">기존 게이트웨이를 삭제하면 이 구성에서 작업하는 동안 로컬 프레미스와 가상 네트워크의 연결이 끊어집니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-192">When you delete the existing gateway, your local premises will lose the connection to your virtual network while you are working on this configuration.</span></span> 
> 
> 

1. <span data-ttu-id="2938f-193">최신 버전의 Azure PowerShell cmdlet을 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-193">You'll need to install the latest version of the Azure PowerShell cmdlets.</span></span> <span data-ttu-id="2938f-194">cmdlet 설치에 대한 자세한 내용은 [Azure PowerShell 설치 및 구성 방법](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2938f-194">For more information about installing cmdlets, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="2938f-195">이 구성에 사용할 cmdlet은 지금까지 사용하던 것과 약간 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-195">The cmdlets that you use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="2938f-196">다음 지침에 지정된 cmdlet을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-196">Be sure to use the cmdlets specified in these instructions.</span></span> 
2. <span data-ttu-id="2938f-197">기존 ExpressRoute 또는 사이트 간 VPN Gateway를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-197">Delete the existing ExpressRoute or Site-to-Site VPN gateway.</span></span>

  ```powershell 
  Remove-AzureRmVirtualNetworkGateway -Name <yourgatewayname> -ResourceGroupName <yourresourcegroup>
  ```
3. <span data-ttu-id="2938f-198">게이트웨이 서브넷을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-198">Delete Gateway Subnet.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name <yourvnetname> -ResourceGroupName <yourresourcegroup> Remove-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet -VirtualNetwork $vnet
  ```
4. <span data-ttu-id="2938f-199">/27 이상인 게이트웨이 서브넷을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-199">Add a Gateway Subnet that is /27 or larger.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="2938f-200">가상 네트워크에 게이트웨이 서브넷 크기를 늘릴 수 있는 IP 주소가 충분히 남아 있지 않을 경우 추가 IP 주소 공간을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-200">If you don't have enough IP addresses left in your virtual network to increase the gateway subnet size, you need to add more IP address space.</span></span>
   > 
   > 

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name <yourvnetname> -ResourceGroupName <yourresourcegroup>
  Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet -AddressPrefix "10.200.255.0/24"
  ```
   
    <span data-ttu-id="2938f-201">VNet 구성을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-201">Save the VNet configuration.</span></span>

  ```powershell
  $vnet = Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
5. <span data-ttu-id="2938f-202">이제 게이트웨이 없는 VNet이 생겼습니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-202">At this point, you have a VNet with no gateways.</span></span> <span data-ttu-id="2938f-203">새 게이트웨이를 만들고 연결을 완료하려면 이전 단계의 [4단계 - ExpressRoute 게이트웨이 만들기](#gw)를 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-203">To create new gateways and complete your connections, you can proceed with [Step 4 - Create an ExpressRoute gateway](#gw), found in the preceding set of steps.</span></span>

## <a name="to-add-point-to-site-configuration-to-the-vpn-gateway"></a><span data-ttu-id="2938f-204">VPN Gateway에 지점 및 사이트 간 구성을 추가하려면</span><span class="sxs-lookup"><span data-stu-id="2938f-204">To add point-to-site configuration to the VPN gateway</span></span>
<span data-ttu-id="2938f-205">아래 단계에 따라 공존 설정에서 VPN Gateway에 지점 및 사이트 간 구성을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-205">You can follow the steps below to add Point-to-Site configuration to your VPN gateway in a co-existence setup.</span></span>

1. <span data-ttu-id="2938f-206">VPN 클라이언트 주소 풀을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-206">Add VPN Client address pool.</span></span>

  ```powershell
  $azureVpn = Get-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName
  Set-AzureRmVirtualNetworkGatewayVpnClientConfig -VirtualNetworkGateway $azureVpn -VpnClientAddressPool "10.251.251.0/24"
  ```
2. <span data-ttu-id="2938f-207">VPN Gateway에 대한 Azure에 VPN 루트 인증서를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-207">Upload the VPN root certificate to Azure for your VPN gateway.</span></span> <span data-ttu-id="2938f-208">이 예에서는 다음 PowerShell cmdlet이 실행되는 로컬 컴퓨터에 루트 인증서가 저장되는 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="2938f-208">In this example, it's assumed that the root certificate is stored in the local machine where the following PowerShell cmdlets are run.</span></span>

  ```powershell
  $p2sCertFullName = "RootErVpnCoexP2S.cer" 
  $p2sCertMatchName = "RootErVpnCoexP2S" 
  $p2sCertToUpload=get-childitem Cert:\CurrentUser\My | Where-Object {$_.Subject -match $p2sCertMatchName} 
  if ($p2sCertToUpload.count -eq 1){write-host "cert found"} else {write-host "cert not found" exit} 
  $p2sCertData = [System.Convert]::ToBase64String($p2sCertToUpload.RawData) Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $p2sCertFullName -VirtualNetworkGatewayname $azureVpn.Name -ResourceGroupName $resgrp.ResourceGroupName -PublicCertData $p2sCertData
  ```

<span data-ttu-id="2938f-209">지점 및 사이트 간 VPN에 대한 자세한 내용은 [지점 및 사이트 간 연결 구성](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2938f-209">For more information on Point-to-Site VPN, see [Configure a Point-to-Site connection](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2938f-210">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2938f-210">Next steps</span></span>
<span data-ttu-id="2938f-211">ExpressRoute에 대한 자세한 내용은 [ExpressRoute FAQ](expressroute-faqs.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2938f-211">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

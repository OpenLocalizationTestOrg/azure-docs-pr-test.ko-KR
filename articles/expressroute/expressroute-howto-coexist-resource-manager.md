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
ms.openlocfilehash: efda9f89d95617c8c4e75af91b20631dc468d4db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-expressroute-and-site-to-site-coexisting-connections"></a><span data-ttu-id="8db24-103">ExpressRoute 및 사이트 간 공존 연결 구성</span><span class="sxs-lookup"><span data-stu-id="8db24-103">Configure ExpressRoute and Site-to-Site coexisting connections</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8db24-104">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8db24-104">PowerShell - Resource Manager</span></span>](expressroute-howto-coexist-resource-manager.md)
> * [<span data-ttu-id="8db24-105">PowerShell - 클래식</span><span class="sxs-lookup"><span data-stu-id="8db24-105">PowerShell - Classic</span></span>](expressroute-howto-coexist-classic.md)
> 
> 

<span data-ttu-id="8db24-106">사이트 간 VPN과 ExpressRoute가 공존하는 연결을 구성하면 여러 장점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-106">Configuring Site-to-Site VPN and ExpressRoute coexisting connections has several advantages.</span></span> <span data-ttu-id="8db24-107">ExressRoute에 대 한 보안 장애 조치 경로와 사이트 간 VPN을 구성할 수도 있고 ExpressRoute를 통해 연결 되어 있지 않은 사이트 간 Vpn tooconnect toosites를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-107">You can configure a Site-to-Site VPN as a secure failover path for ExressRoute, or use Site-to-Site VPNs tooconnect toosites that are not connected through ExpressRoute.</span></span> <span data-ttu-id="8db24-108">두 시나리오 모두이 문서의 단계 tooconfigure hello을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-108">We cover hello steps tooconfigure both scenarios in this article.</span></span> <span data-ttu-id="8db24-109">이 문서 toohello 리소스 관리자 배포 모델을 적용 하 고는 PowerShell을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-109">This article applies toohello Resource Manager deployment model and uses PowerShell.</span></span> <span data-ttu-id="8db24-110">이 구성은 hello Azure 포털에서에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-110">This configuration is not available in hello Azure portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8db24-111">ExpressRoute 회로 아래 hello 지침을 따르기 전에 미리 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-111">ExpressRoute circuits must be pre-configured before you follow hello instructions below.</span></span> <span data-ttu-id="8db24-112">Hello 가이드 너무 수행 되었는지 확인[ExpressRoute 회로 만들기](expressroute-howto-circuit-arm.md) 및 [라우팅 구성](expressroute-howto-routing-arm.md) 계속 진행 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="8db24-112">Make sure that you have followed hello guides too[create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and [configure routing](expressroute-howto-routing-arm.md) before you proceed.</span></span>
> 
> 

## <a name="limits-and-limitations"></a><span data-ttu-id="8db24-113">제한 및 제한 사항</span><span class="sxs-lookup"><span data-stu-id="8db24-113">Limits and limitations</span></span>
* <span data-ttu-id="8db24-114">**통과 라우팅이 지원되지 않습니다.**</span><span class="sxs-lookup"><span data-stu-id="8db24-114">**Transit routing is not supported.**</span></span> <span data-ttu-id="8db24-115">사이트 간 VPN을 통해 연결된 로컬 네트워크와 ExpressRoute를 통해 연결된 로컬 네트워크 사이는 Azure를 통해 라우팅할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-115">You cannot route (via Azure) between your local network connected via Site-to-Site VPN and your local network connected via ExpressRoute.</span></span>
* <span data-ttu-id="8db24-116">**기본 SKU 게이트웨이는 지원되지 않습니다.**</span><span class="sxs-lookup"><span data-stu-id="8db24-116">**Basic SKU gateway is not supported.**</span></span> <span data-ttu-id="8db24-117">두 hello에 대 한 기본 SKU가 아닌 게이트웨이 사용 해야 [express 경로 게이트웨이](expressroute-about-virtual-network-gateways.md) 및 hello [VPN 게이트웨이](../vpn-gateway/vpn-gateway-about-vpngateways.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-117">You must use a non-Basic SKU gateway for both hello [ExpressRoute gateway](expressroute-about-virtual-network-gateways.md) and hello [VPN gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="8db24-118">**경로 기반 VPN Gateway만 지원됩니다.**</span><span class="sxs-lookup"><span data-stu-id="8db24-118">**Only route-based VPN gateway is supported.**</span></span> <span data-ttu-id="8db24-119">경로 기반 [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md)를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-119">You must use a route-based [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="8db24-120">**VPN Gateway에 고정 경로를 구성해야 합니다.**</span><span class="sxs-lookup"><span data-stu-id="8db24-120">**Static route should be configured for your VPN gateway.**</span></span> <span data-ttu-id="8db24-121">로컬 네트워크 연결된 tooboth ExpressRoute 이며는-사이트 VPN, 있어야 로컬 네트워크 tooroute hello 사이트 간 VPN 연결 toohello에 구성 된 고정 경로 경우 공용 인터넷 합니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-121">If your local network is connected tooboth ExpressRoute and a Site-to-Site VPN, you must have a static route configured in your local network tooroute hello Site-to-Site VPN connection toohello public Internet.</span></span>
* <span data-ttu-id="8db24-122">**Express 경로 게이트웨이 먼저 구성 해야 하며 tooa 회로 연결 합니다.**</span><span class="sxs-lookup"><span data-stu-id="8db24-122">**ExpressRoute gateway must be configured first and linked tooa circuit.**</span></span> <span data-ttu-id="8db24-123">Hello express 경로 게이트웨이 먼저 만든 및 hello 사이트 간 VPN 게이트웨이 추가 하기 전에 tooa 회로 연결 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-123">You must create hello ExpressRoute gateway first and link it tooa circuit before you add hello Site-to-Site VPN gateway.</span></span>

## <a name="configuration-designs"></a><span data-ttu-id="8db24-124">구성 디자인</span><span class="sxs-lookup"><span data-stu-id="8db24-124">Configuration designs</span></span>
### <a name="configure-a-site-to-site-vpn-as-a-failover-path-for-expressroute"></a><span data-ttu-id="8db24-125">사이트 간 VPN을 ExpressRoute에 대한 장애 조치(failover) 경로로 구성</span><span class="sxs-lookup"><span data-stu-id="8db24-125">Configure a Site-to-Site VPN as a failover path for ExpressRoute</span></span>
<span data-ttu-id="8db24-126">ExpressRoute에 대한 백업으로 사이트 간 VPN 연결을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-126">You can configure a Site-to-Site VPN connection as a backup for ExpressRoute.</span></span> <span data-ttu-id="8db24-127">이 toovirtual 네트워크 연결 된 toohello Azure 개인 피어 링 경로 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-127">This applies only toovirtual networks linked toohello Azure private peering path.</span></span> <span data-ttu-id="8db24-128">공용 Azure 및 Microsoft 피어링을 통해 액세스할 수 있는 서비스에 대한 VPN 기반 장애 조치 솔루션은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-128">There is no VPN-based failover solution for services accessible through Azure public and Microsoft peerings.</span></span> <span data-ttu-id="8db24-129">hello ExpressRoute 회로 항상 hello 기본 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-129">hello ExpressRoute circuit is always hello primary link.</span></span> <span data-ttu-id="8db24-130">ExpressRoute 회로 hello 실패할 경우에 데이터 hello 사이트 간 VPN 경로 통해 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-130">Data flows through hello Site-to-Site VPN path only if hello ExpressRoute circuit fails.</span></span>

> [!NOTE]
> <span data-ttu-id="8db24-131">ExpressRoute 회로 상태인 동안 기본 사이트 간 VPN을 통해 두 경로가 동일한 hello 되는 경우 Azure hello 패킷 대상 쪽으로 hello 가장 긴 접두사 일치 toochoose hello 경로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-131">While ExpressRoute circuit is preferred over Site-to-Site VPN when both routes are hello same, Azure will use hello longest prefix match toochoose hello route towards hello packet's destination.</span></span>
> 
> 

![공존](media/expressroute-howto-coexist-resource-manager/scenario1.jpg)

### <a name="configure-a-site-to-site-vpn-tooconnect-toosites-not-connected-through-expressroute"></a><span data-ttu-id="8db24-133">ExpressRoute를 통해 연결 되어 있지는 사이트 간 VPN tooconnect toosites 구성</span><span class="sxs-lookup"><span data-stu-id="8db24-133">Configure a Site-to-Site VPN tooconnect toosites not connected through ExpressRoute</span></span>
<span data-ttu-id="8db24-134">여기서 일부 사이트 직접 tooAzure 사이트 간 VPN을 통해 연결 하 고 연결 일부 사이트 ExpressRoute를 통해 네트워크를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-134">You can configure your network where some sites connect directly tooAzure over Site-to-Site VPN, and some sites connect through ExpressRoute.</span></span> 

![공존](media/expressroute-howto-coexist-resource-manager/scenario2.jpg)

> [!NOTE]
> <span data-ttu-id="8db24-136">가상 네트워크를 중계 라우터로 구성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-136">You cannot configure a virtual network as a transit router.</span></span>
> 
> 

## <a name="selecting-hello-steps-toouse"></a><span data-ttu-id="8db24-137">Hello 단계 toouse 선택</span><span class="sxs-lookup"><span data-stu-id="8db24-137">Selecting hello steps toouse</span></span>
<span data-ttu-id="8db24-138">프로시저 toochoose의 서로 다른 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-138">There are two different sets of procedures toochoose from.</span></span> <span data-ttu-id="8db24-139">선택 하는 hello 구성 프로시저는 기존 가상 네트워크, tooconnect 하거나 toocreate 새 가상 네트워크를 원하는 있는지 여부에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-139">hello configuration procedure that you select depends on whether you have an existing virtual network that you want tooconnect to, or you want toocreate a new virtual network.</span></span>

* <span data-ttu-id="8db24-140">VNet 했으며 toocreate 하나 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-140">I don't have a VNet and need toocreate one.</span></span>
  
    <span data-ttu-id="8db24-141">가상 네트워크가 아직 없는 경우 이 절차에서는 Resource Manager 배포 모델을 사용하여 새 가상 네트워크를 만들고 새 ExpressRoute 및 사이트 간 VPN 연결을 만드는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-141">If you don’t already have a virtual network, this procedure walks you through creating a new virtual network using Resource Manager deployment model and creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="8db24-142">가상 네트워크 tooconfigure hello 단계에 따라 [toocreate 새 가상 네트워크 및 공존할 연결](#new)합니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-142">tooconfigure a virtual network, follow hello steps in [toocreate a new virtual network and coexisting connections](#new).</span></span>
* <span data-ttu-id="8db24-143">이미 Resource Manager 배포 모델 VNet이 있는 경우</span><span class="sxs-lookup"><span data-stu-id="8db24-143">I already have a Resource Manager deployment model VNet.</span></span>
  
    <span data-ttu-id="8db24-144">기존 사이트 간 VPN 또는 ExpressRoute에 연결된 가상 네트워크가 이미 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-144">You may already have a virtual network in place with an existing Site-to-Site VPN connection or ExpressRoute connection.</span></span> <span data-ttu-id="8db24-145">hello [이미 기존 VNet에 대 한 tooconfigure 공존할 연결](#add) 섹션을 단계별로 hello 게이트웨이 삭제 한 후 새 ExpressRoute 및 사이트 간 VPN 연결을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-145">hello [tooconfigure coexisting connections for an already existing VNet](#add) section walks you through deleting hello gateway, and then creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="8db24-146">Hello 새 연결을 만들 때에 특정 순서로 hello 단계를 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-146">When creating hello new connections, hello steps must be completed in a specific order.</span></span> <span data-ttu-id="8db24-147">게이트웨이 및 연결에는 기타 기사 toocreate의 hello 지침을 사용 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="8db24-147">Don't use hello instructions in other articles toocreate your gateways and connections.</span></span>
  
    <span data-ttu-id="8db24-148">이 절차에서는 공존할 수 있는 연결을 만드는 있습니다 toodelete 게이트웨이 차지 하며 다음 새 게이트웨이 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-148">In this procedure, creating connections that can coexist requires you toodelete your gateway, and then configure new gateways.</span></span> <span data-ttu-id="8db24-149">생깁니다 크로스-프레미스 연결에 대 한 가동 중지 시간 toomigrate 필요는 없지만 하지만 삭제 하 고 게이트웨이 및 연결을 다시 Vm 또는 서비스 tooa 새로운 가상 네트워크 중 하나.</span><span class="sxs-lookup"><span data-stu-id="8db24-149">You will have downtime for your cross-premises connections while you delete and recreate your gateway and connections, but you will not need toomigrate any of your VMs or services tooa new virtual network.</span></span> <span data-ttu-id="8db24-150">Vm 및 서비스가 hello 부하 분산 장치를 통해 아웃 수 toocommunicate 있더라도 구성된 toodo 있으므로 게이트웨이 구성 하는 동안 합니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-150">Your VMs and services will still be able toocommunicate out through hello load balancer while you configure your gateway if they are configured toodo so.</span></span>

## <span data-ttu-id="8db24-151"><a name="new"></a>새 가상 네트워크를 toocreate 및 공존할 연결</span><span class="sxs-lookup"><span data-stu-id="8db24-151"><a name="new"></a>toocreate a new virtual network and coexisting connections</span></span>
<span data-ttu-id="8db24-152">이 절차에서는 공존하는 VNet 연결과 사이트 간 및 ExpressRoute 연결을 만드는 방법을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-152">This procedure walks you through creating a VNet and Site-to-Site and ExpressRoute connections that will coexist.</span></span>

1. <span data-ttu-id="8db24-153">Hello hello Azure PowerShell cmdlet의 최신 버전을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-153">Install hello latest version of hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="8db24-154">Hello cmdlet을 설치 하는 방법에 대 한 정보를 참조 하십시오. [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-154">For information about installing hello cmdlets, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="8db24-155">이 구성에 사용 하는 hello cmdlet 무엇 친숙할 수 있지만와 약간 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-155">hello cmdlets that you use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="8db24-156">있는지 toouse hello cmdlet이이 지침에 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-156">Be sure toouse hello cmdlets specified in these instructions.</span></span>
2. <span data-ttu-id="8db24-157">Tooyour 계정을 로그인 하 고 hello 환경을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-157">Log in tooyour account and set up hello environment.</span></span>

  ```powershell
  login-AzureRmAccount
  Select-AzureRmSubscription -SubscriptionName 'yoursubscription'
  $location = "Central US"
  $resgrp = New-AzureRmResourceGroup -Name "ErVpnCoex" -Location $location
  $VNetASN = 65010
  ```
3. <span data-ttu-id="8db24-158">게이트웨이 서브넷을 포함하여 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-158">Create a virtual network including Gateway Subnet.</span></span> <span data-ttu-id="8db24-159">Hello 가상 네트워크 구성에 대 한 자세한 내용은 참조 [Azure 가상 네트워크 구성](../virtual-network/virtual-networks-create-vnet-arm-ps.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-159">For more information about hello virtual network configuration, see [Azure Virtual Network configuration](../virtual-network/virtual-networks-create-vnet-arm-ps.md).</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="8db24-160">hello 게이트웨이 서브넷은 / 27 또는 짧은 접두사 (예: /26 또는 /25) 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-160">hello Gateway Subnet must be /27 or a shorter prefix (such as /26 or /25).</span></span>
   > 
   > 
   
    <span data-ttu-id="8db24-161">새 VNet을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-161">Create a new VNet.</span></span>

  ```powershell
  $vnet = New-AzureRmVirtualNetwork -Name "CoexVnet" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AddressPrefix "10.200.0.0/16"
  ```
   
    <span data-ttu-id="8db24-162">서브넷을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-162">Add subnets.</span></span>

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name "App" -VirtualNetwork $vnet -AddressPrefix "10.200.1.0/24"
  Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet -AddressPrefix "10.200.255.0/24"
  ```
   
    <span data-ttu-id="8db24-163">Hello VNet 구성을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-163">Save hello VNet configuration.</span></span>

  ```powershell
  $vnet = Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
4. <span data-ttu-id="8db24-164"><a name="gw"></a>ExpressRoute 게이트웨이를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-164"><a name="gw"></a>Create an ExpressRoute gateway.</span></span> <span data-ttu-id="8db24-165">Hello express 경로 게이트웨이 구성에 대 한 자세한 내용은 참조 [express 경로 게이트웨이 구성](expressroute-howto-add-gateway-resource-manager.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-165">For more information about hello ExpressRoute gateway configuration, see [ExpressRoute gateway configuration](expressroute-howto-add-gateway-resource-manager.md).</span></span> <span data-ttu-id="8db24-166">hello GatewaySKU 해야 *표준*, *HighPerformance*, 또는 *UltraPerformance*합니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-166">hello GatewaySKU must be *Standard*, *HighPerformance*, or *UltraPerformance*.</span></span>

  ```powershell
  $gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $gwIP = New-AzureRmPublicIpAddress -Name "ERGatewayIP" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AllocationMethod Dynamic
  $gwConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "ERGatewayIpConfig" -SubnetId $gwSubnet.Id -PublicIpAddressId $gwIP.Id
  $gw = New-AzureRmVirtualNetworkGateway -Name "ERGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "ExpressRoute" -GatewaySku Standard
  ```
5. <span data-ttu-id="8db24-167">Hello express 경로 게이트웨이 toohello ExpressRoute 회로 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-167">Link hello ExpressRoute gateway toohello ExpressRoute circuit.</span></span> <span data-ttu-id="8db24-168">이 단계를 완료 한 후 온-프레미스 네트워크와 Azure ExpressRoute 통해 hello 연결이 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-168">After this step has been completed, hello connection between your on-premises network and Azure, through ExpressRoute, is established.</span></span> <span data-ttu-id="8db24-169">Hello 링크 작업에 대 한 자세한 내용은 참조 [링크 Vnet tooExpressRoute](expressroute-howto-linkvnet-arm.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-169">For more information about hello link operation, see [Link VNets tooExpressRoute](expressroute-howto-linkvnet-arm.md).</span></span>

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "YourCircuit" -ResourceGroupName "YourCircuitResourceGroup"
  New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -VirtualNetworkGateway1 $gw -PeerId $ckt.Id -ConnectionType ExpressRoute
  ```
6. <span data-ttu-id="8db24-170"><a name="vpngw"></a>그런 다음 사이트 간 VPN Gateway를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-170"><a name="vpngw"></a>Next, create your Site-to-Site VPN gateway.</span></span> <span data-ttu-id="8db24-171">Hello VPN 게이트웨이 구성에 대 한 자세한 내용은 참조 [사이트 간 연결을 사용 하 여 VNet 구성](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-171">For more information about hello VPN gateway configuration, see [Configure a VNet with a Site-to-Site connection](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md).</span></span> <span data-ttu-id="8db24-172">hello GatewaySKU 해야 *표준*, *HighPerformance*, 또는 *UltraPerformance*합니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-172">hello GatewaySKU must be *Standard*, *HighPerformance*, or *UltraPerformance*.</span></span> <span data-ttu-id="8db24-173">hello VpnType 해야 *RouteBased*합니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-173">hello VpnType must *RouteBased*.</span></span>

  ```powershell
  $gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $gwIP = New-AzureRmPublicIpAddress -Name "VPNGatewayIP" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AllocationMethod Dynamic
  $gwConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "VPNGatewayIpConfig" -SubnetId $gwSubnet.Id -PublicIpAddressId $gwIP.Id
  New-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "Vpn" -VpnType "RouteBased" -GatewaySku "Standard"
  ```
   
    <span data-ttu-id="8db24-174">Azure VPN Gateway는 BGP 라우팅 프로토콜을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-174">Azure VPN gateway supports BGP routing protocol.</span></span> <span data-ttu-id="8db24-175">다음 명령을 hello에 hello-Asn 스위치를 추가 하 여 해당 가상 네트워크에 대 한 ASN (AS 번호)을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-175">You can specify ASN (AS Number) for that Virtual Network by adding hello -Asn switch in hello following command.</span></span> <span data-ttu-id="8db24-176">해당 매개 변수를 지정 하지 않으면 됩니다 기본 tooAS 번호 65515입니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-176">Not specifying that parameter will default tooAS number 65515.</span></span>

  ```powershell
  $azureVpn = New-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "Vpn" -VpnType "RouteBased" -GatewaySku "Standard" -Asn $VNetASN
  ```
   
    <span data-ttu-id="8db24-177">BGP 피어 링이 IP hello 및 $azureVpn.BgpSettings.BgpPeeringAddress 및 $azureVpn.BgpSettings.Asn hello VPN 게이트웨이에 대 한 Azure를 사용 하는 숫자로 hello 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-177">You can find hello BGP peering IP and hello AS number that Azure uses for hello VPN gateway in $azureVpn.BgpSettings.BgpPeeringAddress and $azureVpn.BgpSettings.Asn.</span></span> <span data-ttu-id="8db24-178">자세한 내용은 Azure VPN Gateway에 대한 [BGP 구성](../vpn-gateway/vpn-gateway-bgp-resource-manager-ps.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8db24-178">For more information, see [Configure BGP](../vpn-gateway/vpn-gateway-bgp-resource-manager-ps.md) for Azure VPN gateway.</span></span>
7. <span data-ttu-id="8db24-179">로컬 사이트 VPN Gateway 엔터티를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-179">Create a local site VPN gateway entity.</span></span> <span data-ttu-id="8db24-180">이 명령은 온-프레미스 VPN Gateway를 구성하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-180">This command doesn’t configure your on-premises VPN gateway.</span></span> <span data-ttu-id="8db24-181">대신, tooprovide hello 로컬 게이트웨이 설정 hello 공용 IP와 같은 허용 및 hello 온-프레미스 주소 공간을 hello Azure VPN 게이트웨이에 연결할 수 있도록 tooit 합니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-181">Rather, it allows you tooprovide hello local gateway settings, such as hello public IP and hello on-premises address space, so that hello Azure VPN gateway can connect tooit.</span></span>
   
    <span data-ttu-id="8db24-182">로컬 VPN 장치만을 지 원하는 경우 고정 라우팅은 hello 방식으로 다음의 hello 고정 경로 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-182">If your local VPN device only supports static routing, you can configure hello static routes in hello following way:</span></span>

  ```powershell
  $MyLocalNetworkAddress = @("10.100.0.0/16","10.101.0.0/16","10.102.0.0/16")
  $localVpn = New-AzureRmLocalNetworkGateway -Name "LocalVPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -GatewayIpAddress *<Public IP>* -AddressPrefix $MyLocalNetworkAddress
  ```
   
    <span data-ttu-id="8db24-183">Tooknow hello BGP 로컬 VPN 장치 지원 hello BGP tooenable 동적 라우팅 원하는 경우 해야 IP 및 로컬 VPN 번호 처럼 hello 피어 링 장치에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-183">If your local VPN device supports hello BGP and you want tooenable dynamic routing, you need tooknow hello BGP peering IP and hello AS number that your local VPN device uses.</span></span>

  ```powershell
  $localVPNPublicIP = "<Public IP>"
  $localBGPPeeringIP = "<Private IP for hello BGP session>"
  $localBGPASN = "<ASN>"
  $localAddressPrefix = $localBGPPeeringIP + "/32"
  $localVpn = New-AzureRmLocalNetworkGateway -Name "LocalVPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -GatewayIpAddress $localVPNPublicIP -AddressPrefix $localAddressPrefix -BgpPeeringAddress $localBGPPeeringIP -Asn $localBGPASN
  ```
8. <span data-ttu-id="8db24-184">로컬 VPN 장치 tooconnect toohello 새 Azure VPN 게이트웨이 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-184">Configure your local VPN device tooconnect toohello new Azure VPN gateway.</span></span> <span data-ttu-id="8db24-185">VPN 장치 구성에 대한 자세한 내용은 [VPN 장치 구성](../vpn-gateway/vpn-gateway-about-vpn-devices.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8db24-185">For more information about VPN device configuration, see [VPN Device Configuration](../vpn-gateway/vpn-gateway-about-vpn-devices.md).</span></span>
9. <span data-ttu-id="8db24-186">Azure toohello 로컬 게이트웨이에 사이트 간 VPN 게이트웨이 hello 하는 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-186">Link hello Site-to-Site VPN gateway on Azure toohello local gateway.</span></span>

  ```powershell
  $azureVpn = Get-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName
  New-AzureRmVirtualNetworkGatewayConnection -Name "VPNConnection" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -VirtualNetworkGateway1 $azureVpn -LocalNetworkGateway2 $localVpn -ConnectionType IPsec -SharedKey <yourkey>
  ```

## <span data-ttu-id="8db24-187"><a name="add"></a>기존 VNet에 대 한 tooconfigure 공존할 연결</span><span class="sxs-lookup"><span data-stu-id="8db24-187"><a name="add"></a>tooconfigure coexisting connections for an already existing VNet</span></span>
<span data-ttu-id="8db24-188">기존 가상 네트워크를 사용 하도록 설정한 경우 hello 게이트웨이 서브넷 크기를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-188">If you have an existing virtual network, check hello gateway subnet size.</span></span> <span data-ttu-id="8db24-189">Hello 게이트웨이 서브넷이 / 28 또는/29 일 경우 먼저 hello 가상 네트워크 게이트웨이 삭제 하며 hello 게이트웨이 서브넷 크기를 늘리세요.</span><span class="sxs-lookup"><span data-stu-id="8db24-189">If hello gateway subnet is /28 or /29, you must first delete hello virtual network gateway and increase hello gateway subnet size.</span></span> <span data-ttu-id="8db24-190">hello이 섹션의 단계 방법을 보여 줍니다 toodo입니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-190">hello steps in this section show you how toodo that.</span></span>

<span data-ttu-id="8db24-191">Hello 게이트웨이 서브넷이 / 27 이상의 및 hello 가상 네트워크는 ExpressRoute를 통해 연결 되어, 다음 hello 단계를 건너뛰고 너무 진행할 수 있습니다["6 단계-사이트 간 VPN 게이트웨이 만들기"](#vpngw) hello 이전 섹션에서.</span><span class="sxs-lookup"><span data-stu-id="8db24-191">If hello gateway subnet is /27 or larger and hello virtual network is connected via ExpressRoute, you can skip hello steps below and proceed too["Step 6 - Create a Site-to-Site VPN gateway"](#vpngw) in hello previous section.</span></span> 

> [!NOTE]
> <span data-ttu-id="8db24-192">Hello 기존 게이트웨이 삭제 하면이 구성에서 작업 하는 동안 로컬 프레미스 hello 연결 tooyour 가상 네트워크는 손실 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-192">When you delete hello existing gateway, your local premises will lose hello connection tooyour virtual network while you are working on this configuration.</span></span> 
> 
> 

1. <span data-ttu-id="8db24-193">Tooinstall hello 최신 버전의 hello Azure PowerShell cmdlet 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-193">You'll need tooinstall hello latest version of hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="8db24-194">Cmdlet을 설치 하는 방법에 대 한 자세한 내용은 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-194">For more information about installing cmdlets, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="8db24-195">이 구성에 사용 하는 hello cmdlet 무엇 친숙할 수 있지만와 약간 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-195">hello cmdlets that you use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="8db24-196">있는지 toouse hello cmdlet이이 지침에 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-196">Be sure toouse hello cmdlets specified in these instructions.</span></span> 
2. <span data-ttu-id="8db24-197">Hello 기존 express 경로 또는 사이트 간 VPN 게이트웨이 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-197">Delete hello existing ExpressRoute or Site-to-Site VPN gateway.</span></span>

  ```powershell 
  Remove-AzureRmVirtualNetworkGateway -Name <yourgatewayname> -ResourceGroupName <yourresourcegroup>
  ```
3. <span data-ttu-id="8db24-198">게이트웨이 서브넷을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-198">Delete Gateway Subnet.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name <yourvnetname> -ResourceGroupName <yourresourcegroup> Remove-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet -VirtualNetwork $vnet
  ```
4. <span data-ttu-id="8db24-199">/27 이상인 게이트웨이 서브넷을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-199">Add a Gateway Subnet that is /27 or larger.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="8db24-200">가상 네트워크 tooincrease hello 게이트웨이 서브넷 크기에 남아 있는 충분 한 IP 주소를 설정 하지 않은 경우 tooadd IP 주소 공간이 더 필요한 합니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-200">If you don't have enough IP addresses left in your virtual network tooincrease hello gateway subnet size, you need tooadd more IP address space.</span></span>
   > 
   > 

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name <yourvnetname> -ResourceGroupName <yourresourcegroup>
  Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet -AddressPrefix "10.200.255.0/24"
  ```
   
    <span data-ttu-id="8db24-201">Hello VNet 구성을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-201">Save hello VNet configuration.</span></span>

  ```powershell
  $vnet = Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
5. <span data-ttu-id="8db24-202">이제 게이트웨이 없는 VNet이 생겼습니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-202">At this point, you have a VNet with no gateways.</span></span> <span data-ttu-id="8db24-203">toocreate 새 게이트웨이 연결을 완료 하 고, 계속 진행할 수 [4 단계-express 경로 게이트웨이 만들기](#gw)hello 앞 단계에서에서 발견 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-203">toocreate new gateways and complete your connections, you can proceed with [Step 4 - Create an ExpressRoute gateway](#gw), found in hello preceding set of steps.</span></span>

## <a name="tooadd-point-to-site-configuration-toohello-vpn-gateway"></a><span data-ttu-id="8db24-204">tooadd 지점-사이트 구성 toohello VPN 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="8db24-204">tooadd point-to-site configuration toohello VPN gateway</span></span>
<span data-ttu-id="8db24-205">동시 설치 프로그램에서 tooadd 지점-사이트 tooyour VPN 게이트웨이 구성 하는 다음 hello 단계를 따를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-205">You can follow hello steps below tooadd Point-to-Site configuration tooyour VPN gateway in a co-existence setup.</span></span>

1. <span data-ttu-id="8db24-206">VPN 클라이언트 주소 풀을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-206">Add VPN Client address pool.</span></span>

  ```powershell
  $azureVpn = Get-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName
  Set-AzureRmVirtualNetworkGatewayVpnClientConfig -VirtualNetworkGateway $azureVpn -VpnClientAddressPool "10.251.251.0/24"
  ```
2. <span data-ttu-id="8db24-207">VPN 게이트웨이에 대 한 VPN 루트 인증서 tooAzure hello를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-207">Upload hello VPN root certificate tooAzure for your VPN gateway.</span></span> <span data-ttu-id="8db24-208">이 예제에서는 해당 hello 루트 인증서는 PowerShell cmdlet을 다음 hello는 실행 되는 hello 로컬 컴퓨터에 저장 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-208">In this example, it's assumed that hello root certificate is stored in hello local machine where hello following PowerShell cmdlets are run.</span></span>

  ```powershell
  $p2sCertFullName = "RootErVpnCoexP2S.cer" 
  $p2sCertMatchName = "RootErVpnCoexP2S" 
  $p2sCertToUpload=get-childitem Cert:\CurrentUser\My | Where-Object {$_.Subject -match $p2sCertMatchName} 
  if ($p2sCertToUpload.count -eq 1){write-host "cert found"} else {write-host "cert not found" exit} 
  $p2sCertData = [System.Convert]::ToBase64String($p2sCertToUpload.RawData) Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $p2sCertFullName -VirtualNetworkGatewayname $azureVpn.Name -ResourceGroupName $resgrp.ResourceGroupName -PublicCertData $p2sCertData
  ```

<span data-ttu-id="8db24-209">지점 및 사이트 간 VPN에 대한 자세한 내용은 [지점 및 사이트 간 연결 구성](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8db24-209">For more information on Point-to-Site VPN, see [Configure a Point-to-Site connection](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8db24-210">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8db24-210">Next steps</span></span>
<span data-ttu-id="8db24-211">ExpressRoute에 대 한 자세한 내용은 참조 hello [express 경로 FAQ](expressroute-faqs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8db24-211">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

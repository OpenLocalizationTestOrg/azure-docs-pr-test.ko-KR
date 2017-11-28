---
title: "Azure 사이트 간 연결의 강제 터널링 구성: Resource Manager | Microsoft Docs"
description: "모든 인터넷 바인딩된 트래픽을 온-프레미스 위치에 다시 리디렉션하거나 '강제 적용'하는 방법입니다."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: cbe58db8-b598-4c9f-ac88-62c865eb8721
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: cherylmc
ms.openlocfilehash: 207c53924863eb51ee369fe46d5ad12fb1905c53
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="configure-forced-tunneling-using-the-azure-resource-manager-deployment-model"></a><span data-ttu-id="e7d27-103">Azure Resource Manager 배포 모델을 사용하여 강제 터널링 구성</span><span class="sxs-lookup"><span data-stu-id="e7d27-103">Configure forced tunneling using the Azure Resource Manager deployment model</span></span>

<span data-ttu-id="e7d27-104">강제 터널링을 사용하면 검사 및 감사에 대한 사이트 간 VPN 터널을 통해 모든 인터넷 바인딩된 트래픽을 온-프레미스 위치에 다시 리디렉션하거나 "force"할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d27-104">Forced tunneling lets you redirect or "force" all Internet-bound traffic back to your on-premises location via a Site-to-Site VPN tunnel for inspection and auditing.</span></span> <span data-ttu-id="e7d27-105">대부분의 엔터프라이즈 IT 정책에 있어서 중요한 보안 요구 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="e7d27-105">This is a critical security requirement for most enterprise IT policies.</span></span> <span data-ttu-id="e7d27-106">강제 터널링 없이 Azure의 VM에서 인터넷 바인딩된 트래픽은 항상 트래픽을 검사 또는 감사하도록 허용하는 옵션 없이 Azure 네트워크 인프라에서 직접 인터넷으로 트래버스합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d27-106">Without forced tunneling, Internet-bound traffic from your VMs in Azure always traverses from Azure network infrastructure directly out to the Internet, without the option to allow you to inspect or audit the traffic.</span></span> <span data-ttu-id="e7d27-107">인증되지 않은 인터넷 액세스는 잠재적으로 정보 공개 또는 다른 유형의 보안 위반을 발생시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d27-107">Unauthorized Internet access can potentially lead to information disclosure or other types of security breaches.</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)] 

<span data-ttu-id="e7d27-108">이 문서에서는 Resource Manager 배포 모델을 사용하여 만든 가상 네트워크에 대한 강제 터널링을 구성하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d27-108">This article walks you through configuring forced tunneling for virtual networks created using the Resource Manager deployment model.</span></span> <span data-ttu-id="e7d27-109">강제 터널링은 포털을 통해서가 아닌 PowerShell을 사용하여 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d27-109">Forced tunneling can be configured by using PowerShell, not through the portal.</span></span> <span data-ttu-id="e7d27-110">클래식 배포 모델에 대한 강제 터널링을 구성하려면 다음 드롭다운 목록에서 클래식 문서를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d27-110">If you want to configure forced tunneling for the classic deployment model, select classic article from the following dropdown list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e7d27-111">PowerShell - 클래식</span><span class="sxs-lookup"><span data-stu-id="e7d27-111">PowerShell - Classic</span></span>](vpn-gateway-about-forced-tunneling.md)
> * [<span data-ttu-id="e7d27-112">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e7d27-112">PowerShell - Resource Manager</span></span>](vpn-gateway-forced-tunneling-rm.md)
> 
> 

## <a name="about-forced-tunneling"></a><span data-ttu-id="e7d27-113">강제 터널링 정보</span><span class="sxs-lookup"><span data-stu-id="e7d27-113">About forced tunneling</span></span>

<span data-ttu-id="e7d27-114">다음 다이어그램에서는 강제 터널링 작동 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e7d27-114">The following diagram illustrates how forced tunneling works.</span></span> 

![강제 터널링](./media/vpn-gateway-forced-tunneling-rm/forced-tunnel.png)

<span data-ttu-id="e7d27-116">위의 예에서 프런트 엔드 서브넷은 강제 터널링되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d27-116">In the example above, the Frontend subnet is not forced tunneled.</span></span> <span data-ttu-id="e7d27-117">프런트 엔드 서브넷에서 작업은 계속해서 인터넷에서 직접 고객의 요청을 수락하고 응답할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d27-117">The workloads in the Frontend subnet can continue to accept and respond to customer requests from the Internet directly.</span></span> <span data-ttu-id="e7d27-118">중간 계층 및 백 엔드 서브넷은 강제 터널링됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7d27-118">The Mid-tier and Backend subnets are forced tunneled.</span></span> <span data-ttu-id="e7d27-119">이러한 두 서브넷에서 인터넷으로의 모든 아웃바운드 연결은 S2S VPN 터널 중 하나를 통해 온-프레미스 사이트로 다시 force되거나 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7d27-119">Any outbound connections from these two subnets to the Internet will be forced or redirected back to an on-premises site via one of the S2S VPN tunnels.</span></span>

<span data-ttu-id="e7d27-120">이를 통해 필요한 다중 계층 서비스 아키텍처를 계속 사용하면서 Azure의 가상 컴퓨터 또는 클라우드 서비스에서 인터넷 액세스를 제한하고 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d27-120">This allows you to restrict and inspect Internet access from your virtual machines or cloud services in Azure, while continuing to enable your multi-tier service architecture required.</span></span> <span data-ttu-id="e7d27-121">가상 네트워크에 인터넷 연결 작업이 없는 경우 강제 터널링을 전체 가상 네트워크에 적용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d27-121">If there are no Internet-facing workloads in your virtual networks, you also can apply forced tunneling to the entire virtual networks.</span></span>

## <a name="requirements-and-considerations"></a><span data-ttu-id="e7d27-122">요구 사항 및 고려 사항</span><span class="sxs-lookup"><span data-stu-id="e7d27-122">Requirements and considerations</span></span>

<span data-ttu-id="e7d27-123">Azure에서 강제 터널링은 가상 네트워크 사용자 정의 경로를 통해 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7d27-123">Forced tunneling in Azure is configured via virtual network user-defined routes.</span></span> <span data-ttu-id="e7d27-124">온-프레미스 사이트에 트래픽을 리디렉션하는 것은 Azure VPN Gateway에 기본 경로로 표현됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7d27-124">Redirecting traffic to an on-premises site is expressed as a Default Route to the Azure VPN gateway.</span></span> <span data-ttu-id="e7d27-125">사용자 정의 경로 및 가상 네트워크에 대한 자세한 내용은 [사용자 정의 경로 및 IP 전달](../virtual-network/virtual-networks-udr-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e7d27-125">For more information about user-defined routing and virtual networks, see [User-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md).</span></span>

* <span data-ttu-id="e7d27-126">각 가상 네트워크 서브넷에는 기본 제공 시스템 라우팅 테이블이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d27-126">Each virtual network subnet has a built-in, system routing table.</span></span> <span data-ttu-id="e7d27-127">시스템 라우팅 테이블에는 다음 3개의 경로 그룹이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d27-127">The system routing table has the following three groups of routes:</span></span>
  
  * <span data-ttu-id="e7d27-128">**로컬 VNet 경로:** 동일한 가상 네트워크에서 대상 VM으로 직접</span><span class="sxs-lookup"><span data-stu-id="e7d27-128">**Local VNet routes:** Directly to the destination VMs in the same virtual network.</span></span>
  * <span data-ttu-id="e7d27-129">**온-프레미스 경로:** Azure VPN Gateway로</span><span class="sxs-lookup"><span data-stu-id="e7d27-129">**On-premises routes:** To the Azure VPN gateway.</span></span>
  * <span data-ttu-id="e7d27-130">**기본 경로:** 인터넷으로 직접.</span><span class="sxs-lookup"><span data-stu-id="e7d27-130">**Default route:** Directly to the Internet.</span></span> <span data-ttu-id="e7d27-131">이전의 두 경로를 벗어나는 개인 IP 주소로 향하는 패킷은 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7d27-131">Packets destined to the private IP addresses not covered by the previous two routes are dropped.</span></span>
* <span data-ttu-id="e7d27-132">이 절차는 UDR(사용자 정의 경로)을 사용하여 라우팅 테이블을 만들어 기본 경로에 추가한 다음 라우팅 테이블을 VNet 서브넷에 연결하여 해당 서브넷에 강제 터널링을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d27-132">This procedure uses user-defined routes (UDR) to create a routing table to add a default route, and then associate the routing table to your VNet subnet(s) to enable forced tunneling on those subnets.</span></span>
* <span data-ttu-id="e7d27-133">강제 터널링은 경로 기반 VPN 게이트웨이가 있는 VNet에 연결되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d27-133">Forced tunneling must be associated with a VNet that has a route-based VPN gateway.</span></span> <span data-ttu-id="e7d27-134">가상 네트워크에 연결된 크로스-프레미스 로컬 사이트 사이에서 "기본 사이트"를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d27-134">You need to set a "default site" among the cross-premises local sites connected to the virtual network.</span></span> <span data-ttu-id="e7d27-135">또한 트래픽 선택기로 0.0.0.0/0을 사용하여 온-프레미스 VPN 장치를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d27-135">Also, the on-premises VPN device must be configured using 0.0.0.0/0 as traffic selectors.</span></span> 
* <span data-ttu-id="e7d27-136">Express 경로 강제 터널링은 이 메커니즘을 통해 구성되지 않지만 대신 Express 경로 BGP 피어링 세션을 통해 기본 경로를 보급하여 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7d27-136">ExpressRoute forced tunneling is not configured via this mechanism, but instead, is enabled by advertising a default route via the ExpressRoute BGP peering sessions.</span></span> <span data-ttu-id="e7d27-137">자세한 내용은 [ExpressRoute 설명서](https://azure.microsoft.com/documentation/services/expressroute/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e7d27-137">For more information, see the [ExpressRoute Documentation](https://azure.microsoft.com/documentation/services/expressroute/).</span></span>

## <a name="configuration-overview"></a><span data-ttu-id="e7d27-138">구성 개요</span><span class="sxs-lookup"><span data-stu-id="e7d27-138">Configuration overview</span></span>

<span data-ttu-id="e7d27-139">다음 절차를 사용하면 리소스 그룹과 VNet을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d27-139">The following procedure helps you create a resource group and a VNet.</span></span> <span data-ttu-id="e7d27-140">그런 다음 VPN Gateway를 만들고 강제 터널링을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d27-140">You'll then create a VPN gateway and configure forced tunneling.</span></span> <span data-ttu-id="e7d27-141">이 절차에서 가상 네트워크 'MultiTier-VNet'에는 3개의 서브넷( 'Frontend', 'Midtier' 및 'Backend' 서브넷)과 함께 4개의 크로스 프레미스 연결('DefaultSiteHQ' 및 3개의 분기)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d27-141">In this procedure, the virtual network 'MultiTier-VNet' has three subnets: 'Frontend', 'Midtier', and 'Backend', with four cross-premises connections: 'DefaultSiteHQ', and three Branches.</span></span>

<span data-ttu-id="e7d27-142">절차 단계에서는 강제 터널링에 대한 기본 사이트 연결로 DefaultSiteHQ를 설정하고 강제 터널링을 사용하도록 'Midtier' 및 'Backend' 서브넷을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d27-142">The procedure steps set the 'DefaultSiteHQ' as the default site connection for forced tunneling, and configure the 'Midtier' and 'Backend' subnets to use forced tunneling.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="e7d27-143">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="e7d27-143">Before you begin</span></span>

<span data-ttu-id="e7d27-144">최신 버전의 Azure Resource Manager PowerShell cmdlet을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d27-144">Install the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="e7d27-145">PowerShell cmdlet 설치에 대한 자세한 내용은 [Azure PowerShell 설치 및 구성 방법](/powershell/azure/overview) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e7d27-145">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for more information about installing the PowerShell cmdlets.</span></span>

### <a name="to-log-in"></a><span data-ttu-id="e7d27-146">로그인하려면</span><span class="sxs-lookup"><span data-stu-id="e7d27-146">To log in</span></span>

[!INCLUDE [To log in](../../includes/vpn-gateway-ps-login-include.md)]

## <a name="configure-forced-tunneling"></a><span data-ttu-id="e7d27-147">강제 터널링 구성</span><span class="sxs-lookup"><span data-stu-id="e7d27-147">Configure forced tunneling</span></span>

1. <span data-ttu-id="e7d27-148">리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e7d27-148">Create a resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name 'ForcedTunneling' -Location 'North Europe'
  ```
2. <span data-ttu-id="e7d27-149">가상 네트워크를 만들고 서브넷을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d27-149">Create a virtual network and specify subnets.</span></span>

  ```powershell 
  $s1 = New-AzureRmVirtualNetworkSubnetConfig -Name "Frontend" -AddressPrefix "10.1.0.0/24"
  $s2 = New-AzureRmVirtualNetworkSubnetConfig -Name "Midtier" -AddressPrefix "10.1.1.0/24"
  $s3 = New-AzureRmVirtualNetworkSubnetConfig -Name "Backend" -AddressPrefix "10.1.2.0/24"
  $s4 = New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix "10.1.200.0/28"
  $vnet = New-AzureRmVirtualNetwork -Name "MultiTier-VNet" -Location "North Europe" -ResourceGroupName "ForcedTunneling" -AddressPrefix "10.1.0.0/16" -Subnet $s1,$s2,$s3,$s4
  ```
3. <span data-ttu-id="e7d27-150">로컬 네트워크 게이트웨이를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e7d27-150">Create the local network gateways.</span></span>

  ```powershell
  $lng1 = New-AzureRmLocalNetworkGateway -Name "DefaultSiteHQ" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.111" -AddressPrefix "192.168.1.0/24"
  $lng2 = New-AzureRmLocalNetworkGateway -Name "Branch1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.112" -AddressPrefix "192.168.2.0/24"
  $lng3 = New-AzureRmLocalNetworkGateway -Name "Branch2" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.113" -AddressPrefix "192.168.3.0/24"
  $lng4 = New-AzureRmLocalNetworkGateway -Name "Branch3" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.114" -AddressPrefix "192.168.4.0/24"
  ```
4. <span data-ttu-id="e7d27-151">경로 테이블 및 경로 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e7d27-151">Create the route table and route rule.</span></span>

  ```powershell
  New-AzureRmRouteTable –Name "MyRouteTable" -ResourceGroupName "ForcedTunneling" –Location "North Europe"
  $rt = Get-AzureRmRouteTable –Name "MyRouteTable" -ResourceGroupName "ForcedTunneling" 
  Add-AzureRmRouteConfig -Name "DefaultRoute" -AddressPrefix "0.0.0.0/0" -NextHopType VirtualNetworkGateway -RouteTable $rt
  Set-AzureRmRouteTable -RouteTable $rt
  ```
5. <span data-ttu-id="e7d27-152">중간 계층 및 백 엔드 서브넷에 경로 테이블을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d27-152">Associate the route table to the Midtier and Backend subnets.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name "MultiTier-Vnet" -ResourceGroupName "ForcedTunneling"
  Set-AzureRmVirtualNetworkSubnetConfig -Name "MidTier" -VirtualNetwork $vnet -AddressPrefix "10.1.1.0/24" -RouteTable $rt
  Set-AzureRmVirtualNetworkSubnetConfig -Name "Backend" -VirtualNetwork $vnet -AddressPrefix "10.1.2.0/24" -RouteTable $rt
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
6. <span data-ttu-id="e7d27-153">기본 사이트로 게이트웨이를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e7d27-153">Create the Gateway with a default site.</span></span> <span data-ttu-id="e7d27-154">이 단계에서 게이트웨이를 만들고 구성하기 때문에 완료되기까지 약간의 시간이 걸리며, 45분 이상 걸리는 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d27-154">This step takes some time to complete, sometimes 45 minutes or more, because you are creating and configuring the gateway.</span></span><br> <span data-ttu-id="e7d27-155">**-GatewayDefaultSite**는 이 설정을 올바르게 구성할 수 있도록 강제 라우팅 구성을 수행할 수 있도록 하는 cmdlet 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="e7d27-155">The **-GatewayDefaultSite** is the cmdlet parameter that allows the forced routing configuration to work, so take care to configure this setting properly.</span></span> <span data-ttu-id="e7d27-156">이 매개 변수는 PowerShell 1.0 이상에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d27-156">This parameter is available in PowerShell 1.0 or later.</span></span>

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name "GatewayIP" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -AllocationMethod Dynamic
  $gwsubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $ipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "gwIpConfig" -SubnetId $gwsubnet.Id -PublicIpAddressId $pip.Id
  New-AzureRmVirtualNetworkGateway -Name "Gateway1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -IpConfigurations $ipconfig -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -GatewayDefaultSite $lng1 -EnableBgp $false
  ```
7. <span data-ttu-id="e7d27-157">사이트 간 VPN 연결을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d27-157">Establish the Site-to-Site VPN connections.</span></span>

  ```powershell
  $gateway = Get-AzureRmVirtualNetworkGateway -Name "Gateway1" -ResourceGroupName "ForcedTunneling"
  $lng1 = Get-AzureRmLocalNetworkGateway -Name "DefaultSiteHQ" -ResourceGroupName "ForcedTunneling" 
  $lng2 = Get-AzureRmLocalNetworkGateway -Name "Branch1" -ResourceGroupName "ForcedTunneling" 
  $lng3 = Get-AzureRmLocalNetworkGateway -Name "Branch2" -ResourceGroupName "ForcedTunneling" 
  $lng4 = Get-AzureRmLocalNetworkGateway -Name "Branch3" -ResourceGroupName "ForcedTunneling" 
    
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng1 -ConnectionType IPsec -SharedKey "preSharedKey"
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection2" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng2 -ConnectionType IPsec -SharedKey "preSharedKey"
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection3" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng3 -ConnectionType IPsec -SharedKey "preSharedKey"
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection4" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng4 -ConnectionType IPsec -SharedKey "preSharedKey"
    
  Get-AzureRmVirtualNetworkGatewayConnection -Name "Connection1" -ResourceGroupName "ForcedTunneling"
  ```
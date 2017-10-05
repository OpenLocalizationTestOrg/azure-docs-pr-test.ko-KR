---
title: "공존할 수 있는 ExpressRoute 및 사이트 간 VPN 연결 구성: 클래식: Azure | Microsoft Docs"
description: "이 문서에서는 클래식 배포 모델에 대해 공존할 수 있는 Express 경로와 사이트 간 VPN 연결을 구성하는 과정을 안내합니다."
documentationcenter: na
services: expressroute
author: charwen
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: dcf1a5af-a289-466a-b812-0bfedbd2bda0
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: charwen
ms.openlocfilehash: 09d1649f0ca0cf4ca464d95b29461cad3fe51788
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="configure-expressroute-and-site-to-site-coexisting-connections-classic"></a><span data-ttu-id="9bfd6-103">ExpressRoute 및 사이트 간 공존 연결 구성(클래식)</span><span class="sxs-lookup"><span data-stu-id="9bfd6-103">Configure ExpressRoute and Site-to-Site coexisting connections (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9bfd6-104">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9bfd6-104">PowerShell - Resource Manager</span></span>](expressroute-howto-coexist-resource-manager.md)
> * [<span data-ttu-id="9bfd6-105">PowerShell - 클래식</span><span class="sxs-lookup"><span data-stu-id="9bfd6-105">PowerShell - Classic</span></span>](expressroute-howto-coexist-classic.md)
> 
> 

<span data-ttu-id="9bfd6-106">사이트 간 VPN 및 Express 경로를 구성하는 기능이 있으면 여러 장점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-106">Having the ability to configure Site-to-Site VPN and ExpressRoute has several advantages.</span></span> <span data-ttu-id="9bfd6-107">사이트 간 VPN을 Exress 경로에 대한 안전한 장애 조치(failover) 경로로 구성하거나 사이트 간 VPN을 사용하여 Express 경로를 통해 연결되지 않은 사이트에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-107">You can configure Site-to-Site VPN as a secure failover path for ExressRoute, or use Site-to-Site VPNs to connect to sites that are not connected through ExpressRoute.</span></span> <span data-ttu-id="9bfd6-108">이 문서에서는 두 시나리오 모두를 구성하는 단계를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-108">We will cover the steps to configure both scenarios in this article.</span></span> <span data-ttu-id="9bfd6-109">이 문서는 클래식 배포 모델에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-109">This article applies to the classic deployment model.</span></span> <span data-ttu-id="9bfd6-110">이 구성은 포털에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-110">This configuration is not available in the portal.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="9bfd6-111">**Azure 배포 모델 정보**</span><span class="sxs-lookup"><span data-stu-id="9bfd6-111">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="9bfd6-112">Express 경로 회로는 아래 지침을 수행하기 전에 미리 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-112">ExpressRoute circuits must be pre-configured before you follow the instructions below.</span></span> <span data-ttu-id="9bfd6-113">다음 단계를 수행하기 전에 [ExpressRoute 회로 만들기](expressroute-howto-circuit-classic.md) 및 [라우팅 구성](expressroute-howto-routing-classic.md)을 위해 지침을 수행했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-113">Make sure that you have followed the guides to [create an ExpressRoute circuit](expressroute-howto-circuit-classic.md) and [configure routing](expressroute-howto-routing-classic.md) before you follow the steps below.</span></span>
> 
> 

## <a name="limits-and-limitations"></a><span data-ttu-id="9bfd6-114">제한 및 제한 사항</span><span class="sxs-lookup"><span data-stu-id="9bfd6-114">Limits and limitations</span></span>
* <span data-ttu-id="9bfd6-115">**통과 라우팅이 지원되지 않습니다.**</span><span class="sxs-lookup"><span data-stu-id="9bfd6-115">**Transit routing is not supported.**</span></span> <span data-ttu-id="9bfd6-116">사이트 간 VPN을 통해 연결된 로컬 네트워크와 ExpressRoute를 통해 연결된 로컬 네트워크 사이는 Azure를 통해 라우팅할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-116">You cannot route (via Azure) between your local network connected via Site-to-Site VPN and your local network connected via ExpressRoute.</span></span>
* <span data-ttu-id="9bfd6-117">**지점 및 사이트 간 라우팅이 지원되지 않습니다.**</span><span class="sxs-lookup"><span data-stu-id="9bfd6-117">**Point-to-site is not supported.**</span></span> <span data-ttu-id="9bfd6-118">지점 및 사이트 간 VPN을 ExpressRoute에 연결된 동일한 VNet에 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-118">You can't enable point-to-site VPN connections to the same VNet that is connected to ExpressRoute.</span></span> <span data-ttu-id="9bfd6-119">동일한 VNet에 대해 지점 및 사이트 간 VPN과 Express 경로를 함께 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-119">Point-to-site VPN and ExpressRoute cannot coexist for the same VNet.</span></span>
* <span data-ttu-id="9bfd6-120">**사이트 간 VPN Gateway에서 강제 터널링을 사용할 수 없습니다.**</span><span class="sxs-lookup"><span data-stu-id="9bfd6-120">**Forced tunneling cannot be enabled on the Site-to-Site VPN gateway.**</span></span> <span data-ttu-id="9bfd6-121">모든 인터넷 바인딩된 트래픽을 ExpressRoute를 통해 온-프레미스 네트워크에 다시 '강제 적용'할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-121">You can only "force" all Internet-bound traffic back to your on-premises network via ExpressRoute.</span></span>
* <span data-ttu-id="9bfd6-122">**기본 SKU 게이트웨이는 지원되지 않습니다.**</span><span class="sxs-lookup"><span data-stu-id="9bfd6-122">**Basic SKU gateway is not supported.**</span></span> <span data-ttu-id="9bfd6-123">[ExpressRoute 게이트웨이](expressroute-about-virtual-network-gateways.md) 및 [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md) 모두에 기본이 아닌 SKU 게이트웨이를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-123">You must use a non-Basic SKU gateway for both the [ExpressRoute gateway](expressroute-about-virtual-network-gateways.md) and the [VPN gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="9bfd6-124">**경로 기반 VPN Gateway만 지원됩니다.**</span><span class="sxs-lookup"><span data-stu-id="9bfd6-124">**Only route-based VPN gateway is supported.**</span></span> <span data-ttu-id="9bfd6-125">경로 기반 [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md)를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-125">You must use a route-based [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="9bfd6-126">**VPN Gateway에 고정 경로를 구성해야 합니다.**</span><span class="sxs-lookup"><span data-stu-id="9bfd6-126">**Static route should be configured for your VPN gateway.**</span></span> <span data-ttu-id="9bfd6-127">로컬 네트워크가 ExpressRoute 및 사이트 간 VPN 모두에 연결된 경우 로컬 네트워크에서 정적 경로를 구성하여 사이트 간 VPN 연결을 공용 인터넷에 라우팅해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-127">If your local network is connected to both ExpressRoute and a Site-to-Site VPN, you must have a static route configured in your local network to route the Site-to-Site VPN connection to the public Internet.</span></span>
* <span data-ttu-id="9bfd6-128">**ExpressRoute 게이트웨이를 먼저 구성해야 합니다.**</span><span class="sxs-lookup"><span data-stu-id="9bfd6-128">**ExpressRoute gateway must be configured first.**</span></span> <span data-ttu-id="9bfd6-129">사이트 간 VPN Gateway를 추가하기 전에 ExpressRoute 게이트웨이를 먼저 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-129">You must create the ExpressRoute gateway first before you add the Site-to-Site VPN gateway.</span></span>

## <a name="configuration-designs"></a><span data-ttu-id="9bfd6-130">구성 디자인</span><span class="sxs-lookup"><span data-stu-id="9bfd6-130">Configuration designs</span></span>
### <a name="configure-a-site-to-site-vpn-as-a-failover-path-for-expressroute"></a><span data-ttu-id="9bfd6-131">사이트 간 VPN을 ExpressRoute에 대한 장애 조치(failover) 경로로 구성</span><span class="sxs-lookup"><span data-stu-id="9bfd6-131">Configure a Site-to-Site VPN as a failover path for ExpressRoute</span></span>
<span data-ttu-id="9bfd6-132">ExpressRoute에 대한 백업으로 사이트 간 VPN 연결을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-132">You can configure a Site-to-Site VPN connection as a backup for ExpressRoute.</span></span> <span data-ttu-id="9bfd6-133">Azure 개인 피어링 경로에 연결된 가상 네트워크에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-133">This applies only to virtual networks linked to the Azure private peering path.</span></span> <span data-ttu-id="9bfd6-134">공용 Azure 및 Microsoft 피어링을 통해 액세스할 수 있는 서비스에 대한 VPN 기반 장애 조치 솔루션은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-134">There is no VPN-based failover solution for services accessible through Azure public and Microsoft peerings.</span></span> <span data-ttu-id="9bfd6-135">Express 경로 회로는 항상 기본 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-135">The ExpressRoute circuit is always the primary link.</span></span> <span data-ttu-id="9bfd6-136">Express 경로 회로가 실패하면 데이터는 사이트 간 VPN 경로를 통해 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-136">Data will flow through the Site-to-Site VPN path only if the ExpressRoute circuit fails.</span></span> 

> [!NOTE]
> <span data-ttu-id="9bfd6-137">두 경로가 동일한 경우 사이트 간 VPN보다 ExpressRoute 회로가 사용되며, Azure는 가장 긴 접두사 일치 항목을 사용하여 패킷의 대상에 대한 경로를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-137">While ExpressRoute circuit is preferred over Site-to-Site VPN when both routes are the same, Azure will use the longest prefix match to choose the route towards the packet's destination.</span></span>
> 
> 

![공존](media/expressroute-howto-coexist-classic/scenario1.jpg)

### <a name="configure-a-site-to-site-vpn-to-connect-to-sites-not-connected-through-expressroute"></a><span data-ttu-id="9bfd6-139">사이트 간 VPN을 구성하여 ExpressRoute를 통해 연결되지 않은 사이트에 연결</span><span class="sxs-lookup"><span data-stu-id="9bfd6-139">Configure a Site-to-Site VPN to connect to sites not connected through ExpressRoute</span></span>
<span data-ttu-id="9bfd6-140">일부 사이트는 사이트 간 VPN을 통해 Azure에 직접 연결하고 일부 사이트는 ExpressRoute를 통해 연결된 네트워크를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-140">You can configure your network where some sites connect directly to Azure over Site-to-Site VPN, and some sites connect through ExpressRoute.</span></span> 

![공존](media/expressroute-howto-coexist-classic/scenario2.jpg)

> [!NOTE]
> <span data-ttu-id="9bfd6-142">가상 네트워크를 통과 라우터로 구성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-142">You cannot a configure a virtual network as a transit router.</span></span>
> 
> 

## <a name="selecting-the-steps-to-use"></a><span data-ttu-id="9bfd6-143">사용할 단계 선택</span><span class="sxs-lookup"><span data-stu-id="9bfd6-143">Selecting the steps to use</span></span>
<span data-ttu-id="9bfd6-144">연결이 공존할 수 있도록 구성하기 위해 선택하는 서로 다른 두 절차가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-144">There are two different sets of procedures to choose from in order to configure connections that can coexist.</span></span> <span data-ttu-id="9bfd6-145">연결할 기존 가상 네트워크가 있는지, 아니면 새 가상 네트워크를 만들 것인지에 따라 구성 절차를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-145">The configuration procedure that you select will depend on whether you have an existing virtual network that you want to connect to, or you want to create a new virtual network.</span></span>

* <span data-ttu-id="9bfd6-146">VNet이 없어서 만들어야 하는 경우</span><span class="sxs-lookup"><span data-stu-id="9bfd6-146">I don't have a VNet and need to create one.</span></span>
  
    <span data-ttu-id="9bfd6-147">가상 네트워크가 아직 없는 경우 이 절차에서는 클래식 배포 모델을 사용하여 새 가상 네트워크를 만들고 새 Express 경로 및 사이트 간 VPN 연결을 만드는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-147">If you don’t already have a virtual network, this procedure will walk you through creating a new virtual network using the classic deployment model and creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="9bfd6-148">구성하려면 이 문서의 [새 가상 네트워크 및 공존 연결을 만들려면](#new)섹션에 있는 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-148">To configure, follow the steps in the article section [To create a new virtual network and coexisting connections](#new).</span></span>
* <span data-ttu-id="9bfd6-149">이미 클래식 배포 모델 VNet이 있는 경우</span><span class="sxs-lookup"><span data-stu-id="9bfd6-149">I already have a classic deployment model VNet.</span></span>
  
    <span data-ttu-id="9bfd6-150">기존 사이트 간 VPN 또는 Express 경로에 연결된 가상 네트워크가 이미 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-150">You may already have a virtual network in place with an existing Site-to-Site VPN connection or ExpressRoute connection.</span></span> <span data-ttu-id="9bfd6-151">[기존 VNet에 대해 공존 연결을 구성하려면](#add) 문서 섹션에서는 게이트웨이를 삭제한 다음 새 Express 경로 및 사이트 간 VPN 연결을 만드는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-151">The article section [To configure coexsiting connections for an already existing VNet](#add) will walk you through deleting the gateway, and then creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="9bfd6-152">새 연결을 만들 때 지정된 순서대로 단계를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-152">Note that when creating the new connections, the steps must be completed in a very specific order.</span></span> <span data-ttu-id="9bfd6-153">게이트웨이 및 연결을 만들 때 다른 문서의 지침을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-153">Don't use the instructions in other articles to create your gateways and connections.</span></span>
  
    <span data-ttu-id="9bfd6-154">이 절차에서 함께 사용할 수 있는 연결을 만들려면 게이트웨이를 삭제한 다음 공존할 수 있는 새 게이트웨이를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-154">In this procedure, creating connections that can coexist will require you to delete your gateway, and then configure new gateways.</span></span> <span data-ttu-id="9bfd6-155">이 경우 게이트웨이 및 연결을 삭제하고 다시 만드는 동안 크로스-프레미스 연결을 위한 가동 중지 시간이 발생하지만 VM 또는 서비스를 새 가상 네트워크로 마이그레이션할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-155">This means you will have downtime for your cross-premises connections while you delete and recreate your gateway and connections, but you will not need to migrate any of your VMs or services to a new virtual network.</span></span> <span data-ttu-id="9bfd6-156">VM 및 서비스는 그렇게 구성된 경우 게이트웨이를 구성하는 동안 부하 분산 장치를 통해 계속 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-156">Your VMs and services will still be able to communicate out through the load balancer while you configure your gateway if they are configured to do so.</span></span>

## <span data-ttu-id="9bfd6-157"><a name="new"></a>새 가상 네트워크 및 공존 연결을 만들려면</span><span class="sxs-lookup"><span data-stu-id="9bfd6-157"><a name="new"></a>To create a new virtual network and coexisting connections</span></span>
<span data-ttu-id="9bfd6-158">이 절차는 VNet 만들기를 안내하고 함께 사용하는 사이트 간 및 Express 경로 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-158">This procedure will walk you through creating a VNet and create Site-to-Site and ExpressRoute connections that will coexist.</span></span>

1. <span data-ttu-id="9bfd6-159">최신 버전의 Azure PowerShell cmdlet을 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-159">You'll need to install the latest version of the Azure PowerShell cmdlets.</span></span> <span data-ttu-id="9bfd6-160">PowerShell cmdlet 설치에 대한 자세한 내용은 [Azure PowerShell 설치 및 구성 방법](/powershell/azure/overview) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-160">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for more information about installing the PowerShell cmdlets.</span></span> <span data-ttu-id="9bfd6-161">이 구성에 사용할 cmdlet은 지금까지 익숙하던 cmdlet과는 약간 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-161">Note that the cmdlets that you'll use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="9bfd6-162">다음 지침에 지정된 cmdlet을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-162">Be sure to use the cmdlets specified in these instructions.</span></span> 
2. <span data-ttu-id="9bfd6-163">가상 네트워크의 스키마를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-163">Create a schema for your virtual network.</span></span> <span data-ttu-id="9bfd6-164">구성 스키마에 대한 자세한 내용은 [Azure 가상 네트워크 구성 스키마](https://msdn.microsoft.com/library/azure/jj157100.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-164">For more information about the configuration schema, see [Azure Virtual Network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>
   
    <span data-ttu-id="9bfd6-165">스키마를 만들 때 다음 값을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-165">When you create your schema, make sure you use the following values:</span></span>
   
   * <span data-ttu-id="9bfd6-166">가상 네트워크의 게이트웨이 서브넷은 /27 또는 더 짧은 접두사여야 합니다.(/26 또는 /25와 같이)</span><span class="sxs-lookup"><span data-stu-id="9bfd6-166">The gateway subnet for the virtual network must be /27 or a shorter prefix (such as /26 or /25).</span></span>
   * <span data-ttu-id="9bfd6-167">게이트웨이 연결 유형은 "전용"입니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-167">The gateway connection type is "Dedicated".</span></span>
     
             <VirtualNetworkSite name="MyAzureVNET" Location="Central US">
               <AddressSpace>
                 <AddressPrefix>10.17.159.192/26</AddressPrefix>
               </AddressSpace>
               <Subnets>
                 <Subnet name="Subnet-1">
                   <AddressPrefix>10.17.159.192/27</AddressPrefix>
                 </Subnet>
                 <Subnet name="GatewaySubnet">
                   <AddressPrefix>10.17.159.224/27</AddressPrefix>
                 </Subnet>
               </Subnets>
               <Gateway>
                 <ConnectionsToLocalNetwork>
                   <LocalNetworkSiteRef name="MyLocalNetwork">
                     <Connection type="Dedicated" />
                   </LocalNetworkSiteRef>
                 </ConnectionsToLocalNetwork>
               </Gateway>
             </VirtualNetworkSite>
3. <span data-ttu-id="9bfd6-168">xml 스키마 파일을 만들고 구성한 후 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-168">After creating and configuring your xml schema file, upload the file.</span></span> <span data-ttu-id="9bfd6-169">그러면 가상 네트워크가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-169">This will create your virtual network.</span></span>
   
    <span data-ttu-id="9bfd6-170">다음 cmdlet(사용자 고유의 값으로 대체)을 사용하여 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-170">Use the following cmdlet to upload your file, replacing the value with your own.</span></span>
   
        Set-AzureVNetConfig -ConfigurationPath 'C:\NetworkConfig.xml'
4. <span data-ttu-id="9bfd6-171"><a name="gw"></a>Express 경로 게이트웨이를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-171"><a name="gw"></a>Create an ExpressRoute gateway.</span></span> <span data-ttu-id="9bfd6-172">GatewaySKU를 *Standard*, *HighPerformance* 또는 *UltraPerformance*로 지정하고 GatewayType을 *DynamicRouting*으로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-172">Be sure to specify the GatewaySKU as *Standard*, *HighPerformance*, or *UltraPerformance* and the GatewayType as *DynamicRouting*.</span></span>
   
    <span data-ttu-id="9bfd6-173">다음 샘플(사용자 고유의 값으로 대체)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-173">Use the following sample, substituting the values for your own.</span></span>
   
        New-AzureVNetGateway -VNetName MyAzureVNET -GatewayType DynamicRouting -GatewaySKU HighPerformance
5. <span data-ttu-id="9bfd6-174">Express 경로 게이트웨이를 Express 경로 회로에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-174">Link the ExpressRoute gateway to the ExpressRoute circuit.</span></span> <span data-ttu-id="9bfd6-175">이 단계를 완료하면 Express 경로를 통해 온-프레미스 네트워크와 Azure 간의 연결이 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-175">After this step has been completed, the connection between your on-premises network and Azure, through ExpressRoute, is established.</span></span>
   
        New-AzureDedicatedCircuitLink -ServiceKey <service-key> -VNetName MyAzureVNET
6. <span data-ttu-id="9bfd6-176"><a name="vpngw"></a>그런 다음 사이트 간 VPN 게이트웨이를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-176"><a name="vpngw"></a>Next, create your Site-to-Site VPN gateway.</span></span> <span data-ttu-id="9bfd6-177">GatewaySKU는 *Standard*, *HighPerformance* 또는 *UltraPerformance*이어야 하고 GatewayType은 *DynamicRouting*이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-177">The GatewaySKU must be *Standard*, *HighPerformance*, or *UltraPerformance* and the GatewayType must be *DynamicRouting*.</span></span>
   
        New-AzureVirtualNetworkGateway -VNetName MyAzureVNET -GatewayName S2SVPN -GatewayType DynamicRouting -GatewaySKU  HighPerformance
   
    <span data-ttu-id="9bfd6-178">게이트웨이 ID와 공용 IP를 비롯한 가상 네트워크 게이트웨이 설정을 검색하려면 `Get-AzureVirtualNetworkGateway` cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-178">To retrieve the virtual network gateway settings, including the gateway ID and the public IP, use the `Get-AzureVirtualNetworkGateway` cmdlet.</span></span>
   
        Get-AzureVirtualNetworkGateway
   
        GatewayId            : 348ae011-ffa9-4add-b530-7cb30010565e
        GatewayName          : S2SVPN
        LastEventData        :
        GatewayType          : DynamicRouting
        LastEventTimeStamp   : 5/29/2015 4:41:41 PM
        LastEventMessage     : Successfully created a gateway for the following virtual network: GNSDesMoines
        LastEventID          : 23002
        State                : Provisioned
        VIPAddress           : 104.43.x.y
        DefaultSite          :
        GatewaySKU           : HighPerformance
        Location             :
        VnetId               : 979aabcf-e47f-4136-ab9b-b4780c1e1bd5
        SubnetId             :
        EnableBgp            : False
        OperationDescription : Get-AzureVirtualNetworkGateway
        OperationId          : 42773656-85e1-a6b6-8705-35473f1e6f6a
        OperationStatus      : Succeeded
7. <span data-ttu-id="9bfd6-179">로컬 사이트 VPN 게이트웨이 엔터티를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-179">Create a local site VPN gateway entity.</span></span> <span data-ttu-id="9bfd6-180">이 명령은 온-프레미스 VPN Gateway를 구성하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-180">This command doesn’t configure your on-premises VPN gateway.</span></span> <span data-ttu-id="9bfd6-181">대신, Azure VPN 게이트웨이를 연결할 수 있도록 공용 IP 주소 및 온-프레미스 주소 공간과 같은 로컬 게이트웨이 설정을 제공할 수 있게 해줍니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-181">Rather, it allows you to provide the local gateway settings, such as the public IP and the on-premises address space, so that the Azure VPN gateway can connect to it.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="9bfd6-182">사이트 간 VPN의 로컬 사이트는 netcfg에 정의되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-182">The local site for the Site-to-Site VPN is not defined in the netcfg.</span></span> <span data-ttu-id="9bfd6-183">대신, 다음 cmdlet을 사용하여 로컬 사이트 매개 변수를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-183">Instead, you must use this cmdlet to specify the local site parameters.</span></span> <span data-ttu-id="9bfd6-184">포털 또는 netcfg 파일을 사용하여 정의할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-184">You cannot define it using either portal, or the netcfg file.</span></span>
   > 
   > 
   
    <span data-ttu-id="9bfd6-185">다음 샘플(사용자 고유의 값으로 대체)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-185">Use the following sample, replacing the values with your own.</span></span>
   
        New-AzureLocalNetworkGateway -GatewayName MyLocalNetwork -IpAddress <MyLocalGatewayIp> -AddressSpace <MyLocalNetworkAddress>
   
   > [!NOTE]
   > <span data-ttu-id="9bfd6-186">로컬 네트워크에 여러 경로가 있는 경우 모두 배열로 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-186">If your local network has multiple routes, you can pass them all in as an array.</span></span>  <span data-ttu-id="9bfd6-187">$MyLocalNetworkAddress = @("10.1.2.0/24","10.1.3.0/24","10.2.1.0/24")</span><span class="sxs-lookup"><span data-stu-id="9bfd6-187">$MyLocalNetworkAddress = @("10.1.2.0/24","10.1.3.0/24","10.2.1.0/24")</span></span>  
   > 
   > 

    <span data-ttu-id="9bfd6-188">게이트웨이 ID와 공용 IP를 비롯한 가상 네트워크 게이트웨이 설정을 검색하려면 `Get-AzureVirtualNetworkGateway` cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-188">To retrieve the virtual network gateway settings, including the gateway ID and the public IP, use the `Get-AzureVirtualNetworkGateway` cmdlet.</span></span> <span data-ttu-id="9bfd6-189">다음 예제를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-189">See the following example.</span></span>

        Get-AzureLocalNetworkGateway

        GatewayId            : 532cb428-8c8c-4596-9a4f-7ae3a9fcd01b
        GatewayName          : MyLocalNetwork
        IpAddress            : 23.39.x.y
        AddressSpace         : {10.1.2.0/24}
        OperationDescription : Get-AzureLocalNetworkGateway
        OperationId          : ddc4bfae-502c-adc7-bd7d-1efbc00b3fe5
        OperationStatus      : Succeeded


1. <span data-ttu-id="9bfd6-190">새 게이트웨이에 연결할 로컬 VPN 장치를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-190">Configure your local VPN device to connect to the new gateway.</span></span> <span data-ttu-id="9bfd6-191">VPN 장치를 구성할 때 6단계에서 검색한 정보를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-191">Use the information that you retrieved in step 6 when configuring your VPN device.</span></span> <span data-ttu-id="9bfd6-192">VPN 장치 구성에 대한 자세한 내용은 [VPN 장치 구성](../vpn-gateway/vpn-gateway-about-vpn-devices.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-192">For more information about VPN device configuration, see [VPN Device Configuration](../vpn-gateway/vpn-gateway-about-vpn-devices.md).</span></span>
2. <span data-ttu-id="9bfd6-193">Azure의 사이트 간 VPN 게이트웨이를 로컬 게이트웨이에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-193">Link the Site-to-Site VPN gateway on Azure to the local gateway.</span></span>
   
    <span data-ttu-id="9bfd6-194">이 예제에서 connectedEntityId는 `Get-AzureLocalNetworkGateway`를 실행하여 찾을 수 있는 로컬 게이트웨이 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-194">In this example, connectedEntityId is the local gateway ID, which you can find by running `Get-AzureLocalNetworkGateway`.</span></span> <span data-ttu-id="9bfd6-195">virtualNetworkGatewayId는 `Get-AzureVirtualNetworkGateway` cmdlet을 사용하여 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-195">You can find virtualNetworkGatewayId by using the `Get-AzureVirtualNetworkGateway` cmdlet.</span></span> <span data-ttu-id="9bfd6-196">이 단계를 수행하면 사이트 간 VPN 연결을 통해 로컬 네트워크와 Azure 간의 연결이 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-196">After this step, the connection between your local network and Azure via the Site-to-Site VPN connection is established.</span></span>

        New-AzureVirtualNetworkGatewayConnection -connectedEntityId <local-network-gateway-id> -gatewayConnectionName Azure2Local -gatewayConnectionType IPsec -sharedKey abc123 -virtualNetworkGatewayId <azure-s2s-vpn-gateway-id>

## <span data-ttu-id="9bfd6-197"><a name="add"></a>기존 VNet에 대한 공존 연결을 구성하려면</span><span class="sxs-lookup"><span data-stu-id="9bfd6-197"><a name="add"></a>To configure coexsiting connections for an already existing VNet</span></span>
<span data-ttu-id="9bfd6-198">기존 가상 네트워크가 있는 경우 게이트웨이 서브넷 크기를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-198">If you have an existing virtual network, check the gateway subnet size.</span></span> <span data-ttu-id="9bfd6-199">게이트웨이 서브넷이 /28 또는 /29인 경우 우선 가상 네트워크 게이트웨이를 삭제하고 게이트웨이 서브넷 크기를 늘려야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-199">If the gateway subnet is /28 or /29, you must first delete the virtual network gateway and increase the gateway subnet size.</span></span> <span data-ttu-id="9bfd6-200">이 섹션에서 단계별 수행 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-200">The steps in this section will show you how to do that.</span></span>

<span data-ttu-id="9bfd6-201">게이트웨어 서브넷이 /27 이상이고 가상 네트워크가 Express 경로를 통해 연결된 경우 아래 단계를 건너뛰고 이전 섹션의 ["6단계 - 사이트 간 VPN 게이트웨이 만들기"](#vpngw) 를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-201">If the gateway subnet is /27 or larger and the virtual network is connected via ExpressRoute, you can skip the steps below and proceed to ["Step 6 - Create a Site-to-Site VPN gateway"](#vpngw) in the previous section.</span></span>

> [!NOTE]
> <span data-ttu-id="9bfd6-202">기존 게이트웨이를 삭제하면 이 구성에서 작업하는 동안 로컬 프레미스와 가상 네트워크의 연결이 끊어집니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-202">When you delete the existing gateway, your local premises will lose the connection to your virtual network while you are working on this configuration.</span></span>
> 
> 

1. <span data-ttu-id="9bfd6-203">최신 버전의 Azure 리소스 관리자 PowerShell cmdlet을 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-203">You'll need to install the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="9bfd6-204">PowerShell cmdlet 설치에 대한 자세한 내용은 [Azure PowerShell 설치 및 구성 방법](/powershell/azure/overview) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-204">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for more information about installing the PowerShell cmdlets.</span></span> <span data-ttu-id="9bfd6-205">이 구성에 사용할 cmdlet은 지금까지 익숙하던 cmdlet과는 약간 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-205">Note that the cmdlets that you'll use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="9bfd6-206">다음 지침에 지정된 cmdlet을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-206">Be sure to use the cmdlets specified in these instructions.</span></span> 
2. <span data-ttu-id="9bfd6-207">기존 Express 경로 또는 사이트 간 VPN 게이트웨이를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-207">Delete the existing ExpressRoute or Site-to-Site VPN gateway.</span></span> <span data-ttu-id="9bfd6-208">다음 cmdlet(사용자 고유의 값으로 대체)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-208">Use the following cmdlet, replacing the values with your own.</span></span>
   
        Remove-AzureVNetGateway –VnetName MyAzureVNET
3. <span data-ttu-id="9bfd6-209">가상 네트워크 스키마를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-209">Export the virtual network schema.</span></span> <span data-ttu-id="9bfd6-210">다음 PowerShell cmdlet(사용자 고유의 값으로 대체)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-210">Use the following PowerShell cmdlet, replacing the values with your own.</span></span>
   
        Get-AzureVNetConfig –ExportToFile “C:\NetworkConfig.xml”
4. <span data-ttu-id="9bfd6-211">게이트웨이 서브넷이 /27 또는 더 짧은 접두사가 되도록 네트워크 구성 파일 스키마를 편집합니다.(/26 또는 /25와 같이)</span><span class="sxs-lookup"><span data-stu-id="9bfd6-211">Edit the network configuration file schema so that the gateway subnet is /27 or a shorter prefix (such as /26 or /25).</span></span> <span data-ttu-id="9bfd6-212">다음 예제를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-212">See the following example.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="9bfd6-213">가상 네트워크에 게이트웨이 서브넷 크기를 늘릴 수 있는 IP 주소가 충분히 남아 있지 않을 경우 추가 IP 주소 공간을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-213">If you don't have enough IP addresses left in your virtual network to increase the gateway subnet size, you need to add more IP address space.</span></span> <span data-ttu-id="9bfd6-214">구성 스키마에 대한 자세한 내용은 [Azure 가상 네트워크 구성 스키마](https://msdn.microsoft.com/library/azure/jj157100.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-214">For more information about the configuration schema, see [Azure Virtual Network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>
   > 
   > 
   
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.17.159.224/27</AddressPrefix>
          </Subnet>
5. <span data-ttu-id="9bfd6-215">이전 게이트웨이가 사이트 간 VPN인 경우 연결 형식을 **전용**으로 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-215">If your previous gateway was a Site-to-Site VPN, you must also change the connection type to **Dedicated**.</span></span>
   
                 <Gateway>
                  <ConnectionsToLocalNetwork>
                    <LocalNetworkSiteRef name="MyLocalNetwork">
                      <Connection type="Dedicated" />
                    </LocalNetworkSiteRef>
                  </ConnectionsToLocalNetwork>
                </Gateway>
6. <span data-ttu-id="9bfd6-216">이제 게이트웨이가 없는 VNet이 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-216">At this point, you'll have a VNet with no gateways.</span></span> <span data-ttu-id="9bfd6-217">새 게이트웨이를 만들고 연결을 완료하려면 이전 단계의 [4단계 - Express 경로 게이트웨이 만들기](#gw)를 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="9bfd6-217">To create new gateways and complete your connections, you can proceed with [Step 4 - Create an ExpressRoute gateway](#gw), found in the preceding set of steps.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9bfd6-218">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9bfd6-218">Next steps</span></span>
<span data-ttu-id="9bfd6-219">Express 경로에 대한 자세한 내용은 [Express 경로 FAQ](expressroute-faqs.md)</span><span class="sxs-lookup"><span data-stu-id="9bfd6-219">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md)</span></span>


---
title: "공존할 수 있는 ExpressRoute 및 사이트 간 VPN 연결 구성: 클래식: Azure | Microsoft Docs"
description: "이 문서에서는 express 경로 hello 클래식 배포 모델에 대 한 공존할 수 있는 사이트 간 VPN 연결을 구성 하는 과정을 안내 합니다."
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
ms.openlocfilehash: abb30fff55e8ec243f2920c5b2f70c43717755fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-expressroute-and-site-to-site-coexisting-connections-classic"></a><span data-ttu-id="658b2-103">ExpressRoute 및 사이트 간 공존 연결 구성(클래식)</span><span class="sxs-lookup"><span data-stu-id="658b2-103">Configure ExpressRoute and Site-to-Site coexisting connections (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="658b2-104">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="658b2-104">PowerShell - Resource Manager</span></span>](expressroute-howto-coexist-resource-manager.md)
> * [<span data-ttu-id="658b2-105">PowerShell - 클래식</span><span class="sxs-lookup"><span data-stu-id="658b2-105">PowerShell - Classic</span></span>](expressroute-howto-coexist-classic.md)
> 
> 

<span data-ttu-id="658b2-106">Hello 기능 tooconfigure 사이트 간 VPN 및 express 경로 여러 가지 장점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-106">Having hello ability tooconfigure Site-to-Site VPN and ExpressRoute has several advantages.</span></span> <span data-ttu-id="658b2-107">ExressRoute에 대 한 보안 장애 조치 경로와 사이트 간 VPN을 구성 하거나 ExpressRoute를 통해 연결 되어 있지 않은 사이트 간 Vpn tooconnect toosites를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-107">You can configure Site-to-Site VPN as a secure failover path for ExressRoute, or use Site-to-Site VPNs tooconnect toosites that are not connected through ExpressRoute.</span></span> <span data-ttu-id="658b2-108">Hello 단계 tooconfigure 두 시나리오 모두이 문서에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-108">We will cover hello steps tooconfigure both scenarios in this article.</span></span> <span data-ttu-id="658b2-109">이 문서는 toohello 클래식 배포 모델을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-109">This article applies toohello classic deployment model.</span></span> <span data-ttu-id="658b2-110">이 구성은 hello 포털에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-110">This configuration is not available in hello portal.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="658b2-111">**Azure 배포 모델 정보**</span><span class="sxs-lookup"><span data-stu-id="658b2-111">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="658b2-112">ExpressRoute 회로 아래 hello 지침을 따르기 전에 미리 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-112">ExpressRoute circuits must be pre-configured before you follow hello instructions below.</span></span> <span data-ttu-id="658b2-113">Hello 가이드 너무 수행 되었는지 확인[ExpressRoute 회로 만들기](expressroute-howto-circuit-classic.md) 및 [라우팅 구성](expressroute-howto-routing-classic.md) 아래 hello 단계를 수행 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="658b2-113">Make sure that you have followed hello guides too[create an ExpressRoute circuit](expressroute-howto-circuit-classic.md) and [configure routing](expressroute-howto-routing-classic.md) before you follow hello steps below.</span></span>
> 
> 

## <a name="limits-and-limitations"></a><span data-ttu-id="658b2-114">제한 및 제한 사항</span><span class="sxs-lookup"><span data-stu-id="658b2-114">Limits and limitations</span></span>
* <span data-ttu-id="658b2-115">**통과 라우팅이 지원되지 않습니다.**</span><span class="sxs-lookup"><span data-stu-id="658b2-115">**Transit routing is not supported.**</span></span> <span data-ttu-id="658b2-116">사이트 간 VPN을 통해 연결된 로컬 네트워크와 ExpressRoute를 통해 연결된 로컬 네트워크 사이는 Azure를 통해 라우팅할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-116">You cannot route (via Azure) between your local network connected via Site-to-Site VPN and your local network connected via ExpressRoute.</span></span>
* <span data-ttu-id="658b2-117">**지점 및 사이트 간 라우팅이 지원되지 않습니다.**</span><span class="sxs-lookup"><span data-stu-id="658b2-117">**Point-to-site is not supported.**</span></span> <span data-ttu-id="658b2-118">지점-사이트 VPN 연결 toohello를 설정할 수 없는 연결 된 tooExpressRoute 동일한 VNet입니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-118">You can't enable point-to-site VPN connections toohello same VNet that is connected tooExpressRoute.</span></span> <span data-ttu-id="658b2-119">지점-사이트 VPN 및 express 경로 공존할 수 없으며 hello에 대 한 동일한 VNet입니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-119">Point-to-site VPN and ExpressRoute cannot coexist for hello same VNet.</span></span>
* <span data-ttu-id="658b2-120">**사이트 간 VPN 게이트웨이 hello에 강제 터널링을 사용할 수 없습니다.**</span><span class="sxs-lookup"><span data-stu-id="658b2-120">**Forced tunneling cannot be enabled on hello Site-to-Site VPN gateway.**</span></span> <span data-ttu-id="658b2-121">만 ExpressRoute 통해 모든 인터넷 바인딩된 트래픽이 백 tooyour 온-프레미스 네트워크를 "강제 적용" 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-121">You can only "force" all Internet-bound traffic back tooyour on-premises network via ExpressRoute.</span></span>
* <span data-ttu-id="658b2-122">**기본 SKU 게이트웨이는 지원되지 않습니다.**</span><span class="sxs-lookup"><span data-stu-id="658b2-122">**Basic SKU gateway is not supported.**</span></span> <span data-ttu-id="658b2-123">두 hello에 대 한 기본 SKU가 아닌 게이트웨이 사용 해야 [express 경로 게이트웨이](expressroute-about-virtual-network-gateways.md) 및 hello [VPN 게이트웨이](../vpn-gateway/vpn-gateway-about-vpngateways.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-123">You must use a non-Basic SKU gateway for both hello [ExpressRoute gateway](expressroute-about-virtual-network-gateways.md) and hello [VPN gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="658b2-124">**경로 기반 VPN Gateway만 지원됩니다.**</span><span class="sxs-lookup"><span data-stu-id="658b2-124">**Only route-based VPN gateway is supported.**</span></span> <span data-ttu-id="658b2-125">경로 기반 [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md)를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-125">You must use a route-based [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="658b2-126">**VPN Gateway에 고정 경로를 구성해야 합니다.**</span><span class="sxs-lookup"><span data-stu-id="658b2-126">**Static route should be configured for your VPN gateway.**</span></span> <span data-ttu-id="658b2-127">로컬 네트워크 연결된 tooboth ExpressRoute 이며는-사이트 VPN, 있어야 로컬 네트워크 tooroute hello 사이트 간 VPN 연결 toohello에 구성 된 고정 경로 경우 공용 인터넷 합니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-127">If your local network is connected tooboth ExpressRoute and a Site-to-Site VPN, you must have a static route configured in your local network tooroute hello Site-to-Site VPN connection toohello public Internet.</span></span>
* <span data-ttu-id="658b2-128">**ExpressRoute 게이트웨이를 먼저 구성해야 합니다.**</span><span class="sxs-lookup"><span data-stu-id="658b2-128">**ExpressRoute gateway must be configured first.**</span></span> <span data-ttu-id="658b2-129">Hello 사이트 간 VPN 게이트웨이 추가 하기 전에 hello express 경로 게이트웨이 먼저 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-129">You must create hello ExpressRoute gateway first before you add hello Site-to-Site VPN gateway.</span></span>

## <a name="configuration-designs"></a><span data-ttu-id="658b2-130">구성 디자인</span><span class="sxs-lookup"><span data-stu-id="658b2-130">Configuration designs</span></span>
### <a name="configure-a-site-to-site-vpn-as-a-failover-path-for-expressroute"></a><span data-ttu-id="658b2-131">사이트 간 VPN을 ExpressRoute에 대한 장애 조치(failover) 경로로 구성</span><span class="sxs-lookup"><span data-stu-id="658b2-131">Configure a Site-to-Site VPN as a failover path for ExpressRoute</span></span>
<span data-ttu-id="658b2-132">ExpressRoute에 대한 백업으로 사이트 간 VPN 연결을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-132">You can configure a Site-to-Site VPN connection as a backup for ExpressRoute.</span></span> <span data-ttu-id="658b2-133">이 toovirtual 네트워크 연결 된 toohello Azure 개인 피어 링 경로 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-133">This applies only toovirtual networks linked toohello Azure private peering path.</span></span> <span data-ttu-id="658b2-134">공용 Azure 및 Microsoft 피어링을 통해 액세스할 수 있는 서비스에 대한 VPN 기반 장애 조치 솔루션은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-134">There is no VPN-based failover solution for services accessible through Azure public and Microsoft peerings.</span></span> <span data-ttu-id="658b2-135">hello ExpressRoute 회로 항상 hello 기본 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-135">hello ExpressRoute circuit is always hello primary link.</span></span> <span data-ttu-id="658b2-136">ExpressRoute 회로 hello 실패할 경우에 데이터 hello 사이트 간 VPN 경로 통해 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-136">Data will flow through hello Site-to-Site VPN path only if hello ExpressRoute circuit fails.</span></span> 

> [!NOTE]
> <span data-ttu-id="658b2-137">ExpressRoute 회로 상태인 동안 기본 사이트 간 VPN을 통해 두 경로가 동일한 hello 되는 경우 Azure hello 패킷 대상 쪽으로 hello 가장 긴 접두사 일치 toochoose hello 경로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-137">While ExpressRoute circuit is preferred over Site-to-Site VPN when both routes are hello same, Azure will use hello longest prefix match toochoose hello route towards hello packet's destination.</span></span>
> 
> 

![공존](media/expressroute-howto-coexist-classic/scenario1.jpg)

### <a name="configure-a-site-to-site-vpn-tooconnect-toosites-not-connected-through-expressroute"></a><span data-ttu-id="658b2-139">ExpressRoute를 통해 연결 되어 있지는 사이트 간 VPN tooconnect toosites 구성</span><span class="sxs-lookup"><span data-stu-id="658b2-139">Configure a Site-to-Site VPN tooconnect toosites not connected through ExpressRoute</span></span>
<span data-ttu-id="658b2-140">여기서 일부 사이트 직접 tooAzure 사이트 간 VPN을 통해 연결 하 고 연결 일부 사이트 ExpressRoute를 통해 네트워크를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-140">You can configure your network where some sites connect directly tooAzure over Site-to-Site VPN, and some sites connect through ExpressRoute.</span></span> 

![공존](media/expressroute-howto-coexist-classic/scenario2.jpg)

> [!NOTE]
> <span data-ttu-id="658b2-142">가상 네트워크를 통과 라우터로 구성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-142">You cannot a configure a virtual network as a transit router.</span></span>
> 
> 

## <a name="selecting-hello-steps-toouse"></a><span data-ttu-id="658b2-143">Hello 단계 toouse 선택</span><span class="sxs-lookup"><span data-stu-id="658b2-143">Selecting hello steps toouse</span></span>
<span data-ttu-id="658b2-144">공존할 수 있는 순서 tooconfigure 연결에서 프로시저 toochoose의 서로 다른 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-144">There are two different sets of procedures toochoose from in order tooconfigure connections that can coexist.</span></span> <span data-ttu-id="658b2-145">선택 하는 hello 구성 프로시저는 기존 가상 네트워크, tooconnect 하거나 toocreate 새 가상 네트워크를 원하는 있는지 여부에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-145">hello configuration procedure that you select will depend on whether you have an existing virtual network that you want tooconnect to, or you want toocreate a new virtual network.</span></span>

* <span data-ttu-id="658b2-146">VNet 했으며 toocreate 하나 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-146">I don't have a VNet and need toocreate one.</span></span>
  
    <span data-ttu-id="658b2-147">가상 네트워크를 아직 없는 경우이 절차는 과정을 단계별로 hello 클래식 배포 모델을 사용 하 고 새 ExpressRoute 및 사이트 간 VPN 연결을 만드는 새 가상 네트워크를 만드는 합니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-147">If you don’t already have a virtual network, this procedure will walk you through creating a new virtual network using hello classic deployment model and creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="658b2-148">tooconfigure, hello 문서 섹션의 hello 단계 수행 [toocreate 새 가상 네트워크 및 공존할 연결](#new)합니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-148">tooconfigure, follow hello steps in hello article section [toocreate a new virtual network and coexisting connections](#new).</span></span>
* <span data-ttu-id="658b2-149">이미 클래식 배포 모델 VNet이 있는 경우</span><span class="sxs-lookup"><span data-stu-id="658b2-149">I already have a classic deployment model VNet.</span></span>
  
    <span data-ttu-id="658b2-150">기존 사이트 간 VPN 또는 ExpressRoute에 연결된 가상 네트워크가 이미 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-150">You may already have a virtual network in place with an existing Site-to-Site VPN connection or ExpressRoute connection.</span></span> <span data-ttu-id="658b2-151">문서 섹션 hello [이미 기존 VNet에 대 한 tooconfigure coexsiting 연결](#add) hello 게이트웨이 삭제 하 고 다음 ExpressRoute 및 사이트 간 VPN에 대 한 새 연결을 만드는 과정을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-151">hello article section [tooconfigure coexsiting connections for an already existing VNet](#add) will walk you through deleting hello gateway, and then creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="658b2-152">Note hello 새 연결을 만들 때 hello 단계에 따라 매우 구체적인 순서를 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-152">Note that when creating hello new connections, hello steps must be completed in a very specific order.</span></span> <span data-ttu-id="658b2-153">게이트웨이 및 연결에는 기타 기사 toocreate의 hello 지침을 사용 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="658b2-153">Don't use hello instructions in other articles toocreate your gateways and connections.</span></span>
  
    <span data-ttu-id="658b2-154">이 절차에서는 공존할 수 있는 연결을 만드는 및 필요 합니다. 있습니다 toodelete 게이트웨이 새 게이트웨이 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-154">In this procedure, creating connections that can coexist will require you toodelete your gateway, and then configure new gateways.</span></span> <span data-ttu-id="658b2-155">이 해야 의미 크로스-프레미스 연결에 대 한 가동 중지 시간 toomigrate 필요는 없지만 하지만 삭제 하 고 게이트웨이 및 연결을 다시 만들 Vm 또는 서비스 tooa 새로운 가상 네트워크 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-155">This means you will have downtime for your cross-premises connections while you delete and recreate your gateway and connections, but you will not need toomigrate any of your VMs or services tooa new virtual network.</span></span> <span data-ttu-id="658b2-156">Vm 및 서비스가 hello 부하 분산 장치를 통해 아웃 수 toocommunicate 있더라도 구성된 toodo 있으므로 게이트웨이 구성 하는 동안 합니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-156">Your VMs and services will still be able toocommunicate out through hello load balancer while you configure your gateway if they are configured toodo so.</span></span>

## <span data-ttu-id="658b2-157"><a name="new"></a>새 가상 네트워크를 toocreate 및 공존할 연결</span><span class="sxs-lookup"><span data-stu-id="658b2-157"><a name="new"></a>toocreate a new virtual network and coexisting connections</span></span>
<span data-ttu-id="658b2-158">이 절차는 VNet 만들기를 안내하고 함께 사용하는 사이트 간 및 Express 경로 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-158">This procedure will walk you through creating a VNet and create Site-to-Site and ExpressRoute connections that will coexist.</span></span>

1. <span data-ttu-id="658b2-159">Tooinstall hello 최신 버전의 hello Azure PowerShell cmdlet 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-159">You'll need tooinstall hello latest version of hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="658b2-160">참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview) hello PowerShell cmdlet을 설치 하는 방법에 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-160">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information about installing hello PowerShell cmdlets.</span></span> <span data-ttu-id="658b2-161">Note hello cmdlet는이 구성에 사용할 내용을 저장할 수와 약간 다 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-161">Note that hello cmdlets that you'll use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="658b2-162">있는지 toouse hello cmdlet이이 지침에 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-162">Be sure toouse hello cmdlets specified in these instructions.</span></span> 
2. <span data-ttu-id="658b2-163">가상 네트워크의 스키마를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-163">Create a schema for your virtual network.</span></span> <span data-ttu-id="658b2-164">Hello 구성 스키마에 대 한 자세한 내용은 참조 [Azure 가상 네트워크 구성 스키마](https://msdn.microsoft.com/library/azure/jj157100.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-164">For more information about hello configuration schema, see [Azure Virtual Network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>
   
    <span data-ttu-id="658b2-165">스키마를 만들 때 다음 값에는 hello를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-165">When you create your schema, make sure you use hello following values:</span></span>
   
   * <span data-ttu-id="658b2-166">hello 가상 네트워크에 대 한 hello 게이트웨이 서브넷은 / 27 또는 짧은 접두사 (예: /26 또는 /25) 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-166">hello gateway subnet for hello virtual network must be /27 or a shorter prefix (such as /26 or /25).</span></span>
   * <span data-ttu-id="658b2-167">hello 게이트웨이 연결 유형은 "전용".</span><span class="sxs-lookup"><span data-stu-id="658b2-167">hello gateway connection type is "Dedicated".</span></span>
     
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
3. <span data-ttu-id="658b2-168">를 만들고 xml 스키마 파일을 구성 후 hello 파일을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-168">After creating and configuring your xml schema file, upload hello file.</span></span> <span data-ttu-id="658b2-169">그러면 가상 네트워크가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-169">This will create your virtual network.</span></span>
   
    <span data-ttu-id="658b2-170">다음 cmdlet tooupload hello 자신의 hello 값을 대체 하 여 파일을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-170">Use hello following cmdlet tooupload your file, replacing hello value with your own.</span></span>
   
        Set-AzureVNetConfig -ConfigurationPath 'C:\NetworkConfig.xml'
4. <span data-ttu-id="658b2-171"><a name="gw"></a>ExpressRoute 게이트웨이를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-171"><a name="gw"></a>Create an ExpressRoute gateway.</span></span> <span data-ttu-id="658b2-172">있는지 toospecify 수로 GatewaySKU hello *표준*, *HighPerformance*, 또는 *UltraPerformance* 으로 GatewayType hello 및 *DynamicRouting*.</span><span class="sxs-lookup"><span data-stu-id="658b2-172">Be sure toospecify hello GatewaySKU as *Standard*, *HighPerformance*, or *UltraPerformance* and hello GatewayType as *DynamicRouting*.</span></span>
   
    <span data-ttu-id="658b2-173">다음 샘플, 사용자 고유의 대 한 hello 값으로 대체 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-173">Use hello following sample, substituting hello values for your own.</span></span>
   
        New-AzureVNetGateway -VNetName MyAzureVNET -GatewayType DynamicRouting -GatewaySKU HighPerformance
5. <span data-ttu-id="658b2-174">Hello express 경로 게이트웨이 toohello ExpressRoute 회로 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-174">Link hello ExpressRoute gateway toohello ExpressRoute circuit.</span></span> <span data-ttu-id="658b2-175">이 단계를 완료 한 후 온-프레미스 네트워크와 Azure ExpressRoute 통해 hello 연결이 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-175">After this step has been completed, hello connection between your on-premises network and Azure, through ExpressRoute, is established.</span></span>
   
        New-AzureDedicatedCircuitLink -ServiceKey <service-key> -VNetName MyAzureVNET
6. <span data-ttu-id="658b2-176"><a name="vpngw"></a>그런 다음 사이트 간 VPN Gateway를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-176"><a name="vpngw"></a>Next, create your Site-to-Site VPN gateway.</span></span> <span data-ttu-id="658b2-177">hello GatewaySKU 해야 *표준*, *HighPerformance*, 또는 *UltraPerformance* hello GatewayType 해야 *DynamicRouting*합니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-177">hello GatewaySKU must be *Standard*, *HighPerformance*, or *UltraPerformance* and hello GatewayType must be *DynamicRouting*.</span></span>
   
        New-AzureVirtualNetworkGateway -VNetName MyAzureVNET -GatewayName S2SVPN -GatewayType DynamicRouting -GatewaySKU  HighPerformance
   
    <span data-ttu-id="658b2-178">tooretrieve hello 가상 네트워크 게이트웨이 등의 설정을 hello 게이트웨이 ID와 hello 공용 IP를 사용 하 여 hello `Get-AzureVirtualNetworkGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="658b2-178">tooretrieve hello virtual network gateway settings, including hello gateway ID and hello public IP, use hello `Get-AzureVirtualNetworkGateway` cmdlet.</span></span>
   
        Get-AzureVirtualNetworkGateway
   
        GatewayId            : 348ae011-ffa9-4add-b530-7cb30010565e
        GatewayName          : S2SVPN
        LastEventData        :
        GatewayType          : DynamicRouting
        LastEventTimeStamp   : 5/29/2015 4:41:41 PM
        LastEventMessage     : Successfully created a gateway for hello following virtual network: GNSDesMoines
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
7. <span data-ttu-id="658b2-179">로컬 사이트 VPN Gateway 엔터티를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-179">Create a local site VPN gateway entity.</span></span> <span data-ttu-id="658b2-180">이 명령은 온-프레미스 VPN Gateway를 구성하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-180">This command doesn’t configure your on-premises VPN gateway.</span></span> <span data-ttu-id="658b2-181">대신, tooprovide hello 로컬 게이트웨이 설정 hello 공용 IP와 같은 허용 및 hello 온-프레미스 주소 공간을 hello Azure VPN 게이트웨이에 연결할 수 있도록 tooit 합니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-181">Rather, it allows you tooprovide hello local gateway settings, such as hello public IP and hello on-premises address space, so that hello Azure VPN gateway can connect tooit.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="658b2-182">사이트 간 VPN hello에 대 한 로컬 사이트 hello hello netcfg에서 정의 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-182">hello local site for hello Site-to-Site VPN is not defined in hello netcfg.</span></span> <span data-ttu-id="658b2-183">대신,이 cmdlet toospecify hello 로컬 사이트 매개 변수를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-183">Instead, you must use this cmdlet toospecify hello local site parameters.</span></span> <span data-ttu-id="658b2-184">포털 또는 hello netcfg 파일 중 하나를 사용 하 여 정의할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-184">You cannot define it using either portal, or hello netcfg file.</span></span>
   > 
   > 
   
    <span data-ttu-id="658b2-185">다음 샘플, 자신의 hello 값 대체 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-185">Use hello following sample, replacing hello values with your own.</span></span>
   
        New-AzureLocalNetworkGateway -GatewayName MyLocalNetwork -IpAddress <MyLocalGatewayIp> -AddressSpace <MyLocalNetworkAddress>
   
   > [!NOTE]
   > <span data-ttu-id="658b2-186">로컬 네트워크에 여러 경로가 있는 경우 모두 배열로 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-186">If your local network has multiple routes, you can pass them all in as an array.</span></span>  <span data-ttu-id="658b2-187">$MyLocalNetworkAddress = @("10.1.2.0/24","10.1.3.0/24","10.2.1.0/24")</span><span class="sxs-lookup"><span data-stu-id="658b2-187">$MyLocalNetworkAddress = @("10.1.2.0/24","10.1.3.0/24","10.2.1.0/24")</span></span>  
   > 
   > 

    <span data-ttu-id="658b2-188">tooretrieve hello 가상 네트워크 게이트웨이 등의 설정을 hello 게이트웨이 ID와 hello 공용 IP를 사용 하 여 hello `Get-AzureVirtualNetworkGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="658b2-188">tooretrieve hello virtual network gateway settings, including hello gateway ID and hello public IP, use hello `Get-AzureVirtualNetworkGateway` cmdlet.</span></span> <span data-ttu-id="658b2-189">다음 예제는 hello를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="658b2-189">See hello following example.</span></span>

        Get-AzureLocalNetworkGateway

        GatewayId            : 532cb428-8c8c-4596-9a4f-7ae3a9fcd01b
        GatewayName          : MyLocalNetwork
        IpAddress            : 23.39.x.y
        AddressSpace         : {10.1.2.0/24}
        OperationDescription : Get-AzureLocalNetworkGateway
        OperationId          : ddc4bfae-502c-adc7-bd7d-1efbc00b3fe5
        OperationStatus      : Succeeded


1. <span data-ttu-id="658b2-190">로컬 VPN 장치 tooconnect toohello 새 게이트웨이 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-190">Configure your local VPN device tooconnect toohello new gateway.</span></span> <span data-ttu-id="658b2-191">VPN 장치를 구성 하는 경우 6 단계에서 검색 된 hello 정보를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-191">Use hello information that you retrieved in step 6 when configuring your VPN device.</span></span> <span data-ttu-id="658b2-192">VPN 장치 구성에 대한 자세한 내용은 [VPN 장치 구성](../vpn-gateway/vpn-gateway-about-vpn-devices.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="658b2-192">For more information about VPN device configuration, see [VPN Device Configuration](../vpn-gateway/vpn-gateway-about-vpn-devices.md).</span></span>
2. <span data-ttu-id="658b2-193">Azure toohello 로컬 게이트웨이에 사이트 간 VPN 게이트웨이 hello 하는 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-193">Link hello Site-to-Site VPN gateway on Azure toohello local gateway.</span></span>
   
    <span data-ttu-id="658b2-194">이 예제에서는 connectedEntityId는를 실행 하 여 찾을 수 있는 hello 로컬 게이트웨이 ID `Get-AzureLocalNetworkGateway`합니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-194">In this example, connectedEntityId is hello local gateway ID, which you can find by running `Get-AzureLocalNetworkGateway`.</span></span> <span data-ttu-id="658b2-195">Hello를 사용 하 여 virtualNetworkGatewayId를 찾을 수 있습니다 `Get-AzureVirtualNetworkGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="658b2-195">You can find virtualNetworkGatewayId by using hello `Get-AzureVirtualNetworkGateway` cmdlet.</span></span> <span data-ttu-id="658b2-196">이 단계를 hello 사이트 간 VPN 연결을 통해 로컬 네트워크와 Azure 간의 hello 연결이 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-196">After this step, hello connection between your local network and Azure via hello Site-to-Site VPN connection is established.</span></span>

        New-AzureVirtualNetworkGatewayConnection -connectedEntityId <local-network-gateway-id> -gatewayConnectionName Azure2Local -gatewayConnectionType IPsec -sharedKey abc123 -virtualNetworkGatewayId <azure-s2s-vpn-gateway-id>

## <span data-ttu-id="658b2-197"><a name="add"></a>기존 VNet에 대 한 tooconfigure coexsiting 연결</span><span class="sxs-lookup"><span data-stu-id="658b2-197"><a name="add"></a>tooconfigure coexsiting connections for an already existing VNet</span></span>
<span data-ttu-id="658b2-198">기존 가상 네트워크를 사용 하도록 설정한 경우 hello 게이트웨이 서브넷 크기를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-198">If you have an existing virtual network, check hello gateway subnet size.</span></span> <span data-ttu-id="658b2-199">Hello 게이트웨이 서브넷이 / 28 또는/29 일 경우 먼저 hello 가상 네트워크 게이트웨이 삭제 하며 hello 게이트웨이 서브넷 크기를 늘리세요.</span><span class="sxs-lookup"><span data-stu-id="658b2-199">If hello gateway subnet is /28 or /29, you must first delete hello virtual network gateway and increase hello gateway subnet size.</span></span> <span data-ttu-id="658b2-200">hello이 섹션의 단계 방법을 살펴보겠습니다 toodo입니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-200">hello steps in this section will show you how toodo that.</span></span>

<span data-ttu-id="658b2-201">Hello 게이트웨이 서브넷이 / 27 이상의 및 hello 가상 네트워크는 ExpressRoute를 통해 연결 되어, 다음 hello 단계를 건너뛰고 너무 진행할 수 있습니다["6 단계-사이트 간 VPN 게이트웨이 만들기"](#vpngw) hello 이전 섹션에서.</span><span class="sxs-lookup"><span data-stu-id="658b2-201">If hello gateway subnet is /27 or larger and hello virtual network is connected via ExpressRoute, you can skip hello steps below and proceed too["Step 6 - Create a Site-to-Site VPN gateway"](#vpngw) in hello previous section.</span></span>

> [!NOTE]
> <span data-ttu-id="658b2-202">Hello 기존 게이트웨이 삭제 하면이 구성에서 작업 하는 동안 로컬 프레미스 hello 연결 tooyour 가상 네트워크는 손실 됩니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-202">When you delete hello existing gateway, your local premises will lose hello connection tooyour virtual network while you are working on this configuration.</span></span>
> 
> 

1. <span data-ttu-id="658b2-203">Tooinstall hello 최신 버전의 hello Azure 리소스 관리자 PowerShell cmdlet 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-203">You'll need tooinstall hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="658b2-204">참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview) hello PowerShell cmdlet을 설치 하는 방법에 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-204">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information about installing hello PowerShell cmdlets.</span></span> <span data-ttu-id="658b2-205">Note hello cmdlet는이 구성에 사용할 내용을 저장할 수와 약간 다 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-205">Note that hello cmdlets that you'll use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="658b2-206">있는지 toouse hello cmdlet이이 지침에 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-206">Be sure toouse hello cmdlets specified in these instructions.</span></span> 
2. <span data-ttu-id="658b2-207">Hello 기존 express 경로 또는 사이트 간 VPN 게이트웨이 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-207">Delete hello existing ExpressRoute or Site-to-Site VPN gateway.</span></span> <span data-ttu-id="658b2-208">다음 cmdlet, 사용자의 정보로 hello 값 대체 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-208">Use hello following cmdlet, replacing hello values with your own.</span></span>
   
        Remove-AzureVNetGateway –VnetName MyAzureVNET
3. <span data-ttu-id="658b2-209">Hello 가상 네트워크 스키마를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-209">Export hello virtual network schema.</span></span> <span data-ttu-id="658b2-210">다음 PowerShell cmdlet, 사용자의 정보로 hello 값 대체 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-210">Use hello following PowerShell cmdlet, replacing hello values with your own.</span></span>
   
        Get-AzureVNetConfig –ExportToFile “C:\NetworkConfig.xml”
4. <span data-ttu-id="658b2-211">Hello 게이트웨이 서브넷이 / 27 또는 짧은 접두사 (예: /26 또는 /25) 있도록 hello 네트워크 구성 파일 스키마를 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-211">Edit hello network configuration file schema so that hello gateway subnet is /27 or a shorter prefix (such as /26 or /25).</span></span> <span data-ttu-id="658b2-212">다음 예제는 hello를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="658b2-212">See hello following example.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="658b2-213">가상 네트워크 tooincrease hello 게이트웨이 서브넷 크기에 남아 있는 충분 한 IP 주소를 설정 하지 않은 경우 tooadd IP 주소 공간이 더 필요한 합니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-213">If you don't have enough IP addresses left in your virtual network tooincrease hello gateway subnet size, you need tooadd more IP address space.</span></span> <span data-ttu-id="658b2-214">Hello 구성 스키마에 대 한 자세한 내용은 참조 [Azure 가상 네트워크 구성 스키마](https://msdn.microsoft.com/library/azure/jj157100.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-214">For more information about hello configuration schema, see [Azure Virtual Network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>
   > 
   > 
   
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.17.159.224/27</AddressPrefix>
          </Subnet>
5. <span data-ttu-id="658b2-215">이전 게이트웨이 사이트 간 VPN 경우도 변경 해야 hello 연결 유형 너무**전용**합니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-215">If your previous gateway was a Site-to-Site VPN, you must also change hello connection type too**Dedicated**.</span></span>
   
                 <Gateway>
                  <ConnectionsToLocalNetwork>
                    <LocalNetworkSiteRef name="MyLocalNetwork">
                      <Connection type="Dedicated" />
                    </LocalNetworkSiteRef>
                  </ConnectionsToLocalNetwork>
                </Gateway>
6. <span data-ttu-id="658b2-216">이제 게이트웨이가 없는 VNet이 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-216">At this point, you'll have a VNet with no gateways.</span></span> <span data-ttu-id="658b2-217">toocreate 새 게이트웨이 연결을 완료 하 고, 계속 진행할 수 [4 단계-express 경로 게이트웨이 만들기](#gw)hello 앞 단계에서에서 발견 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="658b2-217">toocreate new gateways and complete your connections, you can proceed with [Step 4 - Create an ExpressRoute gateway](#gw), found in hello preceding set of steps.</span></span>

## <a name="next-steps"></a><span data-ttu-id="658b2-218">다음 단계</span><span class="sxs-lookup"><span data-stu-id="658b2-218">Next steps</span></span>
<span data-ttu-id="658b2-219">ExpressRoute에 대 한 자세한 내용은 참조 hello [express 경로 FAQ](expressroute-faqs.md)</span><span class="sxs-lookup"><span data-stu-id="658b2-219">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md)</span></span>


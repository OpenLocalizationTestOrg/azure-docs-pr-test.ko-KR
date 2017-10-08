---
title: "어떻게 tooconfigure (피어 링)에 대 한 라우팅 ExpressRoute 회로: Azure: 클래식 | Microsoft Docs"
description: "이 문서를 만들고 hello private, public 및 Microsoft 피어 링 express 경로 회로 프로 비전에 대 한 hello 단계를 안내 합니다. 또한이 문서를 보면 toocheck hello 상태 업데이트 또는 회로 대 한 피어 링 삭제 방법을 알 수 있습니다."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: a4bd39d2-373a-467a-8b06-36cfcc1027d2
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: dc5bcc4b86c3bc965a88281b6c2a660f3bc58eb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit-classic"></a><span data-ttu-id="80ca5-104">ExpressRoute 회로의 피어링 만들기 및 수정(클래식)</span><span class="sxs-lookup"><span data-stu-id="80ca5-104">Create and modify peering for an ExpressRoute circuit (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="80ca5-105">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="80ca5-105">Azure portal</span></span>](expressroute-howto-routing-portal-resource-manager.md)
> * [<span data-ttu-id="80ca5-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="80ca5-106">PowerShell</span></span>](expressroute-howto-routing-arm.md)
> * [<span data-ttu-id="80ca5-107">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="80ca5-107">Azure CLI</span></span>](howto-routing-cli.md)
> * [<span data-ttu-id="80ca5-108">비디오 - 개인 피어링</span><span class="sxs-lookup"><span data-stu-id="80ca5-108">Video - Private peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="80ca5-109">비디오 - 공용 피어링</span><span class="sxs-lookup"><span data-stu-id="80ca5-109">Video - Public peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="80ca5-110">비디오 - Microsoft 피어링</span><span class="sxs-lookup"><span data-stu-id="80ca5-110">Video - Microsoft peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="80ca5-111">PowerShell(클래식)</span><span class="sxs-lookup"><span data-stu-id="80ca5-111">PowerShell (classic)</span></span>](expressroute-howto-routing-classic.md)
> 

<span data-ttu-id="80ca5-112">이 문서는 hello 단계 toocreate 안내 하 고 PowerShell 및 hello 클래식 배포 모델을 사용 하 여 ExpressRoute 회로 대 한 라우팅 구성을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-112">This article walks you through hello steps toocreate and manage routing configuration for an ExpressRoute circuit using PowerShell and hello classic deployment model.</span></span> <span data-ttu-id="80ca5-113">다음 hello 단계도 안내해 어떻게 toocheck hello 상태 업데이트 또는 삭제 하 고, 피어 링 express 경로 회로 대 한 프로 비전 해제.</span><span class="sxs-lookup"><span data-stu-id="80ca5-113">hello steps below will also show you how toocheck hello status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="80ca5-114">**Azure 배포 모델 정보**</span><span class="sxs-lookup"><span data-stu-id="80ca5-114">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]


## <a name="configuration-prerequisites"></a><span data-ttu-id="80ca5-115">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="80ca5-115">Configuration prerequisites</span></span>
* <span data-ttu-id="80ca5-116">Hello 최신 버전의 hello Azure 서비스 관리 (SM) PowerShell cmdlet 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-116">You will need hello latest version of hello Azure Service Management (SM) PowerShell cmdlets.</span></span> <span data-ttu-id="80ca5-117">자세한 내용은 [Azure PowerShell cmdlet 시작](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="80ca5-117">For more information, see [Getting started with Azure PowerShell cmdlets](/powershell/azure/overview).</span></span>  
* <span data-ttu-id="80ca5-118">Hello 검토 했는지 확인 [필수 구성 요소](expressroute-prerequisites.md) 페이지 hello [라우팅 요구 사항](expressroute-routing.md) 페이지 및 hello [워크플로](expressroute-workflows.md) 구성을 시작 하기 전에 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-118">Make sure that you have reviewed hello [prerequisites](expressroute-prerequisites.md) page, hello [routing requirements](expressroute-routing.md) page, and hello [workflows](expressroute-workflows.md) page before you begin configuration.</span></span>
* <span data-ttu-id="80ca5-119">활성화된 Express 경로 회로가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-119">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="80ca5-120">너무 hello 지침에 따라[ExpressRoute 회로 만들기](expressroute-howto-circuit-classic.md) 있고 계속 hello 회로 하기 전에 연결 공급자가 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-120">Follow hello instructions too[create an ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="80ca5-121">ExpressRoute 회로 hello 하면 아래에 설명 된 toobe 수 toorun hello cmdlet에 대 한 가능 하 고 프로 비전 된 상태에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-121">hello ExpressRoute circuit must be in a provisioned and enabled state for you toobe able toorun hello cmdlets described below.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="80ca5-122">이러한 지침은 계층 2 연결 서비스를 제공 하는 서비스 공급자를 사용 하 여 만든 toocircuits만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-122">These instructions only apply toocircuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="80ca5-123">관리된 3계층 서비스(일반적으로 MPLS와 같은 IPVPN)를 제공하는 서비스 공급자를 사용하는 경우 연결 공급자는 사용자를 위해 라우팅을 구성하고 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-123">If you are using a service provider offering managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

<span data-ttu-id="80ca5-124">Express 경로 회로에 한 가지, 두 가지 또는 세 가지 피어링을 구성할 수 있습니다.(개인, Azure 공용 Azure 및 Microsoft)</span><span class="sxs-lookup"><span data-stu-id="80ca5-124">You can configure one, two, or all three peerings (Azure private, Azure public and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="80ca5-125">선택한 순서로 피어링을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-125">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="80ca5-126">그러나 한 번에 하나씩 피어 링의 hello 구성을 완료 되었는지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-126">However, you must make sure that you complete hello configuration of each peering one at a time.</span></span>


### <a name="log-in-tooyour-azure-account-and-select-a-subscription"></a><span data-ttu-id="80ca5-127">Tooyour Azure 계정에에서 로그인을 구독 선택</span><span class="sxs-lookup"><span data-stu-id="80ca5-127">Log in tooyour Azure account and select a subscription</span></span>
1. <span data-ttu-id="80ca5-128">관리자 권한으로 PowerShell 콘솔을 열고 및 tooyour 계정을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-128">Open your PowerShell console with elevated rights and connect tooyour account.</span></span> <span data-ttu-id="80ca5-129">다음 예제에서는 toohelp 연결한 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-129">Use hello following example toohelp you connect:</span></span>

        Login-AzureRmAccount

2. <span data-ttu-id="80ca5-130">Hello 계정에 대 한 hello 구독을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-130">Check hello subscriptions for hello account.</span></span>

        Get-AzureRmSubscription

3. <span data-ttu-id="80ca5-131">둘 이상의 구독을 보유 하는 경우 toouse hello 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-131">If you have more than one subscription, select hello subscription that you want toouse.</span></span>

        Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"

4. <span data-ttu-id="80ca5-132">를 사용 하 여 다음 cmdlet tooadd hello Azure 구독 tooPowerShell hello 클래식 배포 모델에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-132">Next, use hello following cmdlet tooadd your Azure subscription tooPowerShell for hello classic deployment model.</span></span>

        Add-AzureAccount


## <a name="azure-private-peering"></a><span data-ttu-id="80ca5-133">Azure 개인 피어링</span><span class="sxs-lookup"><span data-stu-id="80ca5-133">Azure private peering</span></span>
<span data-ttu-id="80ca5-134">이 섹션 toocreate를 가져오고, 업데이트, 고 hello ExpressRoute 회로 대 한 개인 피어 링 구성을 Azure 삭제 방법에 지침을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-134">This section provides instructions on how toocreate, get, update, and delete hello Azure private peering configuration for an ExpressRoute circuit.</span></span> 

### <a name="toocreate-azure-private-peering"></a><span data-ttu-id="80ca5-135">Azure 개인 피어 링 toocreate</span><span class="sxs-lookup"><span data-stu-id="80ca5-135">toocreate Azure private peering</span></span>
1. <span data-ttu-id="80ca5-136">**ExpressRoute에 대 한 hello PowerShell 모듈을 가져옵니다.**</span><span class="sxs-lookup"><span data-stu-id="80ca5-136">**Import hello PowerShell module for ExpressRoute.**</span></span>
   
    <span data-ttu-id="80ca5-137">Hello ExpressRoute cmdlet을 사용 하 여 순서 toostart에 hello PowerShell 세션으로 hello Azure 및 ExpressRoute 모듈을 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-137">You must import hello Azure and ExpressRoute modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="80ca5-138">실행된 hello 다음 hello PowerShell 세션으로 tooimport hello Azure 및 ExpressRoute 모듈은 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-138">Run hello following commands tooimport hello Azure and ExpressRoute modules into hello PowerShell session.</span></span>  
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. <span data-ttu-id="80ca5-139">**Express 경로 회로를 만듭니다.**</span><span class="sxs-lookup"><span data-stu-id="80ca5-139">**Create an ExpressRoute circuit.**</span></span>
   
    <span data-ttu-id="80ca5-140">Hello 지침 toocreate 따라는 [ExpressRoute 회로](expressroute-howto-circuit-classic.md) hello 연결 공급자가 사용자를 프로 비전 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-140">Follow hello instructions toocreate an [ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have it provisioned by hello connectivity provider.</span></span> <span data-ttu-id="80ca5-141">관리 되는 계층 3 서비스를 제공 하는 연결 공급자, 경우에 연결 공급자 tooenable 있습니다에 대 한 피어 링 개인 Azure를 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-141">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="80ca5-142">이 경우 hello 다음 섹션에 나열 된 toofollow 지침 필요 하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-142">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="80ca5-143">그러나 연결 공급자 회로 만든 후,에 대 한 라우팅 관리 하지 않는 경우 아래 hello 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-143">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow hello instructions below.</span></span> 
3. <span data-ttu-id="80ca5-144">**Hello ExpressRoute 회로 tooensure은 프로 비전을 확인 합니다.**</span><span class="sxs-lookup"><span data-stu-id="80ca5-144">**Check hello ExpressRoute circuit tooensure it is provisioned.**</span></span>
   
    <span data-ttu-id="80ca5-145">Hello ExpressRoute 회로 프로 비전 하 고도 사용 하도록 설정 하는 경우에 먼저 toosee를 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-145">You must first check toosee if hello ExpressRoute circuit is Provisioned and also Enabled.</span></span> <span data-ttu-id="80ca5-146">아래 hello 예제를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="80ca5-146">See hello example below.</span></span>
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    <span data-ttu-id="80ca5-147">Hello 회로가 프로 비전 됨과 Enabled로 표시 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-147">Make sure that hello circuit shows as Provisioned and Enabled.</span></span> <span data-ttu-id="80ca5-148">그렇지 않으면 작업할 연결 공급자 tooget 회로 toohello 필요한 상황 및 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-148">If it doesn't, work with your connectivity provider tooget your circuit toohello required state and status.</span></span>
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. <span data-ttu-id="80ca5-149">**Azure 개인 피어 링 hello 회로 대 한 구성 합니다.**</span><span class="sxs-lookup"><span data-stu-id="80ca5-149">**Configure Azure private peering for hello circuit.**</span></span>
   
    <span data-ttu-id="80ca5-150">Hello 다음 단계를 진행 하기 전에 다음 항목 hello 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-150">Make sure that you have hello following items before you proceed with hello next steps:</span></span>
   
   * <span data-ttu-id="80ca5-151">/ 30 서브넷 hello 기본 링크에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-151">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="80ca5-152">가상 네트워크에 예약된 주소 공간의 일부가 아니어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-152">This must not be part of any address space reserved for virtual networks.</span></span>
   * <span data-ttu-id="80ca5-153">/ 30 서브넷 hello 보조 링크에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-153">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="80ca5-154">가상 네트워크에 예약된 주소 공간의 일부가 아니어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-154">This must not be part of any address space reserved for virtual networks.</span></span>
   * <span data-ttu-id="80ca5-155">유효한 VLAN ID tooestablish이 피어 링을 합니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-155">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="80ca5-156">없는 다른 피어 링 되도록 hello 회로에 사용 하 여 hello 동일한 VLAN ID</span><span class="sxs-lookup"><span data-stu-id="80ca5-156">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
   * <span data-ttu-id="80ca5-157">피어링에 대한 AS 숫자입니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-157">AS number for peering.</span></span> <span data-ttu-id="80ca5-158">2바이트 및 4바이트 AS 번호를 모두 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-158">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="80ca5-159">이 피어링에 개인 AS 숫자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-159">You can use a private AS number for this peering.</span></span> <span data-ttu-id="80ca5-160">65515를 사용하지 않는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-160">Ensure that you are not using 65515.</span></span>
   * <span data-ttu-id="80ca5-161">MD5 해시 toouse 하나를 선택 하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-161">An MD5 hash if you choose toouse one.</span></span> <span data-ttu-id="80ca5-162">**선택 사항입니다**.</span><span class="sxs-lookup"><span data-stu-id="80ca5-162">**This is optional**.</span></span>
     
    <span data-ttu-id="80ca5-163">Azure 개인 피어 링 회로 대 한 cmdlet tooconfigure 다음 hello를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-163">You can run hello following cmdlet tooconfigure Azure private peering for your circuit.</span></span>
     
        <span data-ttu-id="80ca5-164">New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100</span><span class="sxs-lookup"><span data-stu-id="80ca5-164">New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100</span></span>
     
    <span data-ttu-id="80ca5-165">Toouse MD5 해시를 선택 하는 경우 아래의 hello cmdlet을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-165">You can use hello cmdlet below if you choose toouse an MD5 hash.</span></span>
     
        <span data-ttu-id="80ca5-166">New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100 -SharedKey "A1B2C3D4"</span><span class="sxs-lookup"><span data-stu-id="80ca5-166">New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100 -SharedKey "A1B2C3D4"</span></span>
     
     > [!IMPORTANT]
     > <span data-ttu-id="80ca5-167">고객 ASN이 아닌 피어링 ASN로 AS 번호를 지정했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-167">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
     > 
     > 

### <a name="tooview-azure-private-peering-details"></a><span data-ttu-id="80ca5-168">세부 정보를 피어 링 개인 Azure tooview</span><span class="sxs-lookup"><span data-stu-id="80ca5-168">tooview Azure private peering details</span></span>
<span data-ttu-id="80ca5-169">Cmdlet을 다음 hello를 사용 하 여 구성 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-169">You can get configuration details using hello following cmdlet</span></span>

    Get-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 100


### <a name="tooupdate-azure-private-peering-configuration"></a><span data-ttu-id="80ca5-170">tooupdate Azure 개인 피어 링 구성</span><span class="sxs-lookup"><span data-stu-id="80ca5-170">tooupdate Azure private peering configuration</span></span>
<span data-ttu-id="80ca5-171">Hello 다음 cmdlet을 사용 하 여 hello 구성의 어떠한 부분을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-171">You can update any part of hello configuration using hello following cmdlet.</span></span> <span data-ttu-id="80ca5-172">Hello 아래 예제에서는 100 too500에서 hello hello 회로의 VLAN ID를 업데이트 중입니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-172">In hello example below, hello VLAN ID of hello circuit is being updated from 100 too500.</span></span>

    Set-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 500 -SharedKey "A1B2C3D4"

### <a name="toodelete-azure-private-peering"></a><span data-ttu-id="80ca5-173">Azure 개인 피어 링 toodelete</span><span class="sxs-lookup"><span data-stu-id="80ca5-173">toodelete Azure private peering</span></span>
<span data-ttu-id="80ca5-174">Hello 다음 cmdlet을 실행 하 여 피어 링 구성을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-174">You can remove your peering configuration by running hello following cmdlet.</span></span>

> [!WARNING]
> <span data-ttu-id="80ca5-175">모든 가상 네트워크 없는지 hello ExpressRoute 회로에서 연결 된이 cmdlet을 실행 하기 전에 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-175">You must ensure that all virtual networks are unlinked from hello ExpressRoute circuit before running this cmdlet.</span></span> 
> 
> 

    Remove-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"


## <a name="azure-public-peering"></a><span data-ttu-id="80ca5-176">Azure 공용 피어링</span><span class="sxs-lookup"><span data-stu-id="80ca5-176">Azure public peering</span></span>
<span data-ttu-id="80ca5-177">이 섹션 toocreate를 get, 업데이트 및 삭제 hello ExpressRoute 회로 대 한 Azure 공용 피어 링 구성 방법에 지침을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-177">This section provides instructions on how toocreate, get, update and delete hello Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-public-peering"></a><span data-ttu-id="80ca5-178">Azure 공용 피어 링 toocreate</span><span class="sxs-lookup"><span data-stu-id="80ca5-178">toocreate Azure public peering</span></span>
1. <span data-ttu-id="80ca5-179">**ExpressRoute에 대 한 hello PowerShell 모듈을 가져옵니다.**</span><span class="sxs-lookup"><span data-stu-id="80ca5-179">**Import hello PowerShell module for ExpressRoute.**</span></span>
   
    <span data-ttu-id="80ca5-180">Hello ExpressRoute cmdlet을 사용 하 여 순서 toostart에 hello PowerShell 세션으로 hello Azure 및 ExpressRoute 모듈을 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-180">You must import hello Azure and ExpressRoute modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="80ca5-181">실행된 hello 다음 hello PowerShell 세션으로 tooimport hello Azure 및 ExpressRoute 모듈은 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-181">Run hello following commands tooimport hello Azure and ExpressRoute modules into hello PowerShell session.</span></span> 
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. <span data-ttu-id="80ca5-182">**ExpressRoute 회로 만들기**</span><span class="sxs-lookup"><span data-stu-id="80ca5-182">**Create an ExpressRoute circuit**</span></span>
   
    <span data-ttu-id="80ca5-183">Hello 지침 toocreate 따라는 [ExpressRoute 회로](expressroute-howto-circuit-classic.md) hello 연결 공급자가 사용자를 프로 비전 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-183">Follow hello instructions toocreate an [ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have it provisioned by hello connectivity provider.</span></span> <span data-ttu-id="80ca5-184">관리 되는 계층 3 서비스를 제공 하는 연결 공급자, 경우에 연결 공급자 tooenable Azure 사용자에 대 한 피어 링 공용를 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-184">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure public peering for you.</span></span> <span data-ttu-id="80ca5-185">이 경우 hello 다음 섹션에 나열 된 toofollow 지침 필요 하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-185">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="80ca5-186">그러나 연결 공급자 회로 만든 후,에 대 한 라우팅 관리 하지 않는 경우 아래 hello 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-186">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow hello instructions below.</span></span>
3. <span data-ttu-id="80ca5-187">**Express 경로 회로 tooensure은 프로 비전 확인**</span><span class="sxs-lookup"><span data-stu-id="80ca5-187">**Check ExpressRoute circuit tooensure it is provisioned**</span></span>
   
    <span data-ttu-id="80ca5-188">Hello ExpressRoute 회로 프로 비전 하 고도 사용 하도록 설정 하는 경우에 먼저 toosee를 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-188">You must first check toosee if hello ExpressRoute circuit is Provisioned and also Enabled.</span></span> <span data-ttu-id="80ca5-189">아래 hello 예제를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="80ca5-189">See hello example below.</span></span>
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    <span data-ttu-id="80ca5-190">Hello 회로가 프로 비전 됨과 Enabled로 표시 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-190">Make sure that hello circuit shows as Provisioned and Enabled.</span></span> <span data-ttu-id="80ca5-191">그렇지 않으면 작업할 연결 공급자 tooget 회로 toohello 필요한 상황 및 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-191">If it doesn't, work with your connectivity provider tooget your circuit toohello required state and status.</span></span>
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. <span data-ttu-id="80ca5-192">**Azure 공용 피어 링 hello 회로 대 한 구성**</span><span class="sxs-lookup"><span data-stu-id="80ca5-192">**Configure Azure public peering for hello circuit**</span></span>
   
    <span data-ttu-id="80ca5-193">다음 정보를 계속 진행 하기 전에 hello 가졌는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-193">Ensure that you have hello following information before you proceed further.</span></span>
   
   * <span data-ttu-id="80ca5-194">/ 30 서브넷 hello 기본 링크에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-194">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="80ca5-195">유효한 공용 IPv4 접두사여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-195">This must be a valid public IPv4 prefix.</span></span>
   * <span data-ttu-id="80ca5-196">/ 30 서브넷 hello 보조 링크에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-196">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="80ca5-197">유효한 공용 IPv4 접두사여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-197">This must be a valid public IPv4 prefix.</span></span>
   * <span data-ttu-id="80ca5-198">유효한 VLAN ID tooestablish이 피어 링을 합니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-198">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="80ca5-199">없는 다른 피어 링 되도록 hello 회로에 사용 하 여 hello 동일한 VLAN ID</span><span class="sxs-lookup"><span data-stu-id="80ca5-199">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
   * <span data-ttu-id="80ca5-200">피어링에 대한 AS 숫자입니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-200">AS number for peering.</span></span> <span data-ttu-id="80ca5-201">2바이트 및 4바이트 AS 번호를 모두 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-201">You can use both 2-byte and 4-byte AS numbers.</span></span>
   * <span data-ttu-id="80ca5-202">MD5 해시 toouse 하나를 선택 하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-202">An MD5 hash if you choose toouse one.</span></span> <span data-ttu-id="80ca5-203">**선택 사항입니다**.</span><span class="sxs-lookup"><span data-stu-id="80ca5-203">**This is optional**.</span></span>
     
    <span data-ttu-id="80ca5-204">다음 cmdlet tooconfigure Azure 공용 피어 링 회로 대 한 hello를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-204">You can run hello following cmdlet tooconfigure Azure public peering for your circuit</span></span>
     
        <span data-ttu-id="80ca5-205">New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200</span><span class="sxs-lookup"><span data-stu-id="80ca5-205">New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200</span></span>
     
    <span data-ttu-id="80ca5-206">Toouse MD5 해시를 선택 하는 경우 아래의 hello cmdlet을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-206">You can use hello cmdlet below if you choose toouse an MD5 hash</span></span>
     
        <span data-ttu-id="80ca5-207">New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200 -SharedKey "A1B2C3D4"</span><span class="sxs-lookup"><span data-stu-id="80ca5-207">New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200 -SharedKey "A1B2C3D4"</span></span>
     
     > [!IMPORTANT]
     > <span data-ttu-id="80ca5-208">고객 ASN이 아닌 피어링 ASN로 AS 번호를 지정했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-208">Ensure that you specify your AS number as peering ASN and not customer ASN.</span></span>
     > 
     > 

### <a name="tooview-azure-public-peering-details"></a><span data-ttu-id="80ca5-209">세부 정보를 피어 링 공용 Azure tooview</span><span class="sxs-lookup"><span data-stu-id="80ca5-209">tooview Azure public peering details</span></span>
<span data-ttu-id="80ca5-210">Cmdlet을 다음 hello를 사용 하 여 구성 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-210">You can get configuration details using hello following cmdlet</span></span>

    Get-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 131.107.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 131.107.0.4/30
    State                          : Enabled
    VlanId                         : 200


### <a name="tooupdate-azure-public-peering-configuration"></a><span data-ttu-id="80ca5-211">tooupdate Azure 공용 피어 링 구성</span><span class="sxs-lookup"><span data-stu-id="80ca5-211">tooupdate Azure public peering configuration</span></span>
<span data-ttu-id="80ca5-212">Hello 다음 cmdlet을 사용 하 여 hello 구성의 어떠한 부분을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-212">You can update any part of hello configuration using hello following cmdlet</span></span>

    Set-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 600 -SharedKey "A1B2C3D4"

<span data-ttu-id="80ca5-213">위 예제는 hello에 200 too600에서 hello hello 회로의 VLAN ID를 업데이트 중입니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-213">hello VLAN ID of hello circuit is being updated from 200 too600 in hello above example.</span></span>

### <a name="toodelete-azure-public-peering"></a><span data-ttu-id="80ca5-214">Azure 공용 피어 링 toodelete</span><span class="sxs-lookup"><span data-stu-id="80ca5-214">toodelete Azure public peering</span></span>
<span data-ttu-id="80ca5-215">Hello 다음 cmdlet을 실행 하 여 피어 링 구성을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-215">You can remove your peering configuration by running hello following cmdlet</span></span>

    Remove-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

## <a name="microsoft-peering"></a><span data-ttu-id="80ca5-216">Microsoft 피어링</span><span class="sxs-lookup"><span data-stu-id="80ca5-216">Microsoft peering</span></span>
<span data-ttu-id="80ca5-217">이 섹션, toocreate를 가져오기, 업데이트 및 삭제 hello ExpressRoute 회로 대 한 Microsoft 피어 링 구성 방법에 지침을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-217">This section provides instructions on how toocreate, get, update and delete hello Microsoft peering configuration for an ExpressRoute circuit.</span></span> 

### <a name="toocreate-microsoft-peering"></a><span data-ttu-id="80ca5-218">toocreate Microsoft 피어 링</span><span class="sxs-lookup"><span data-stu-id="80ca5-218">toocreate Microsoft peering</span></span>
1. <span data-ttu-id="80ca5-219">**ExpressRoute에 대 한 hello PowerShell 모듈을 가져옵니다.**</span><span class="sxs-lookup"><span data-stu-id="80ca5-219">**Import hello PowerShell module for ExpressRoute.**</span></span>
   
    <span data-ttu-id="80ca5-220">Hello ExpressRoute cmdlet을 사용 하 여 순서 toostart에 hello PowerShell 세션으로 hello Azure 및 ExpressRoute 모듈을 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-220">You must import hello Azure and ExpressRoute modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="80ca5-221">실행된 hello 다음 hello PowerShell 세션으로 tooimport hello Azure 및 ExpressRoute 모듈은 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-221">Run hello following commands tooimport hello Azure and ExpressRoute modules into hello PowerShell session.</span></span>  
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. <span data-ttu-id="80ca5-222">**ExpressRoute 회로 만들기**</span><span class="sxs-lookup"><span data-stu-id="80ca5-222">**Create an ExpressRoute circuit**</span></span>
   
    <span data-ttu-id="80ca5-223">Hello 지침 toocreate 따라는 [ExpressRoute 회로](expressroute-howto-circuit-classic.md) hello 연결 공급자가 사용자를 프로 비전 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-223">Follow hello instructions toocreate an [ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have it provisioned by hello connectivity provider.</span></span> <span data-ttu-id="80ca5-224">관리 되는 계층 3 서비스를 제공 하는 연결 공급자, 경우에 연결 공급자 tooenable 있습니다에 대 한 피어 링 개인 Azure를 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-224">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="80ca5-225">이 경우 hello 다음 섹션에 나열 된 toofollow 지침 필요 하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-225">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="80ca5-226">그러나 연결 공급자 회로 만든 후,에 대 한 라우팅 관리 하지 않는 경우 아래 hello 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-226">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow hello instructions below.</span></span>
3. <span data-ttu-id="80ca5-227">**Express 경로 회로 tooensure은 프로 비전 확인**</span><span class="sxs-lookup"><span data-stu-id="80ca5-227">**Check ExpressRoute circuit tooensure it is provisioned**</span></span>
   
    <span data-ttu-id="80ca5-228">먼저 hello ExpressRoute 회로 사용 및 프로 비전 됨 상태 이면 toosee를 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-228">You must first check toosee if hello ExpressRoute circuit is in Provisioned and Enabled state.</span></span>
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    <span data-ttu-id="80ca5-229">Hello 회로가 프로 비전 됨과 Enabled로 표시 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-229">Make sure that hello circuit shows as Provisioned and Enabled.</span></span> <span data-ttu-id="80ca5-230">그렇지 않으면 작업할 연결 공급자 tooget 회로 toohello 필요한 상황 및 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-230">If it doesn't, work with your connectivity provider tooget your circuit toohello required state and status.</span></span>
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. <span data-ttu-id="80ca5-231">**Microsoft hello 회로 대 한 피어 링 구성**</span><span class="sxs-lookup"><span data-stu-id="80ca5-231">**Configure Microsoft peering for hello circuit**</span></span>
   
    <span data-ttu-id="80ca5-232">계속 하기 전에 정보 다음 hello 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-232">Make sure that you have hello following information before you proceed.</span></span>
   
   * <span data-ttu-id="80ca5-233">/ 30 서브넷 hello 기본 링크에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-233">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="80ca5-234">사용자가 소유하고 RIR/IRR에 등록된 유효한 공용 IPv4 접두사여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-234">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
   * <span data-ttu-id="80ca5-235">/ 30 서브넷 hello 보조 링크에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-235">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="80ca5-236">사용자가 소유하고 RIR/IRR에 등록된 유효한 공용 IPv4 접두사여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-236">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
   * <span data-ttu-id="80ca5-237">유효한 VLAN ID tooestablish이 피어 링을 합니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-237">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="80ca5-238">없는 다른 피어 링 되도록 hello 회로에 사용 하 여 hello 동일한 VLAN ID</span><span class="sxs-lookup"><span data-stu-id="80ca5-238">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
   * <span data-ttu-id="80ca5-239">피어링에 대한 AS 숫자입니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-239">AS number for peering.</span></span> <span data-ttu-id="80ca5-240">2바이트 및 4바이트 AS 번호를 모두 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-240">You can use both 2-byte and 4-byte AS numbers.</span></span>
   * <span data-ttu-id="80ca5-241">접두사를 보급: 목록을 제공 해야 모든 접두사의 hello BGP 세션을 통해 tooadvertise 계획 합니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-241">Advertised prefixes: You must provide a list of all prefixes you plan tooadvertise over hello BGP session.</span></span> <span data-ttu-id="80ca5-242">공용 IP 주소 접두사만 수락됩니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-242">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="80ca5-243">Toosend 접두사를 계획 하는 경우 쉼표로 구분 된 목록을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-243">You can send a comma separated list if you plan toosend a set of prefixes.</span></span> <span data-ttu-id="80ca5-244">이 접두사는 RIR에 등록 된 tooyou 여야 / IRR입니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-244">These prefixes must be registered tooyou in an RIR / IRR.</span></span>
   * <span data-ttu-id="80ca5-245">고객 ASN: 등록 된 toohello 숫자로 피어 링 되지 않은 접두사를 배포 하는 경우 등록 된 숫자 toowhich로 hello를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-245">Customer ASN: If you are advertising prefixes that are not registered toohello peering AS number, you can specify hello AS number toowhich they are registered.</span></span> <span data-ttu-id="80ca5-246">**선택 사항입니다**.</span><span class="sxs-lookup"><span data-stu-id="80ca5-246">**This is optional**.</span></span>
   * <span data-ttu-id="80ca5-247">라우팅 레지스트리 이름을: hello RIR 지정할 수 있습니다는 hello에 대 한 번호 매기기로이 앞에 추가 IRR를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-247">Routing Registry Name: You can specify hello RIR / IRR against which hello AS number and prefixes are registered.</span></span>
   * <span data-ttu-id="80ca5-248">MD5 해시를 toouse 하나를 선택 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="80ca5-248">An MD5 hash, if you choose toouse one.</span></span> <span data-ttu-id="80ca5-249">**선택 사항입니다.**</span><span class="sxs-lookup"><span data-stu-id="80ca5-249">**This is optional.**</span></span>
     
    <span data-ttu-id="80ca5-250">회로 대 한 cmdlet tooconfigure Microsoft pering 다음 hello를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-250">You can run hello following cmdlet tooconfigure Microsoft pering for your circuit</span></span>
     
        <span data-ttu-id="80ca5-251">New-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"</span><span class="sxs-lookup"><span data-stu-id="80ca5-251">New-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"</span></span>

### <a name="tooview-microsoft-peering-details"></a><span data-ttu-id="80ca5-252">tooview Microsoft 피어 링 세부 정보</span><span class="sxs-lookup"><span data-stu-id="80ca5-252">tooview Microsoft peering details</span></span>
<span data-ttu-id="80ca5-253">Cmdlet을 다음 hello를 사용 하 여 구성 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-253">You can get configuration details using hello following cmdlet.</span></span>

    Get-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 123.0.0.0/30
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 2245
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : ARIN
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 300


### <a name="tooupdate-microsoft-peering-configuration"></a><span data-ttu-id="80ca5-254">tooupdate Microsoft 피어 링 구성</span><span class="sxs-lookup"><span data-stu-id="80ca5-254">tooupdate Microsoft peering configuration</span></span>
<span data-ttu-id="80ca5-255">Hello 다음 cmdlet을 사용 하 여 hello 구성의 어떠한 부분을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-255">You can update any part of hello configuration using hello following cmdlet.</span></span>

    Set-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"

### <a name="toodelete-microsoft-peering"></a><span data-ttu-id="80ca5-256">toodelete Microsoft 피어 링</span><span class="sxs-lookup"><span data-stu-id="80ca5-256">toodelete Microsoft peering</span></span>
<span data-ttu-id="80ca5-257">Hello 다음 cmdlet을 실행 하 여 피어 링 구성을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-257">You can remove your peering configuration by running hello following cmdlet.</span></span>

    Remove-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

## <a name="next-steps"></a><span data-ttu-id="80ca5-258">다음 단계</span><span class="sxs-lookup"><span data-stu-id="80ca5-258">Next steps</span></span>
<span data-ttu-id="80ca5-259">그런 다음, [연결할 ExpressRoute 회로 VNet tooan](expressroute-howto-linkvnet-classic.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="80ca5-259">Next, [Link a VNet tooan ExpressRoute circuit](expressroute-howto-linkvnet-classic.md).</span></span>

* <span data-ttu-id="80ca5-260">워크플로에 대한 자세한 내용은 [Express 경로 워크플로](expressroute-workflows.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="80ca5-260">For more information about workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="80ca5-261">회로 피어링에 대한 자세한 내용은 [Express 경로 회로 및 라우팅 도메인](expressroute-circuit-peerings.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="80ca5-261">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>


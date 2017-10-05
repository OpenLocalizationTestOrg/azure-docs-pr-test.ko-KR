---
title: "ExpressRoute 회로에 라우팅을 구성하는 방법(피어링): Azure: 클래식| Microsoft Docs"
description: "이 문서에서는 Express 경로 회로의 개인, 공용 및 Microsoft 피어링을 만들고 프로비전하는 단계를 안내합니다. 또한 회로의 상태를 확인하고 업데이트 또는 삭제하는 방법을 보여줍니다."
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
ms.openlocfilehash: 37713db70f3ae837edafc997b78b16b121d0a885
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit-classic"></a><span data-ttu-id="5e680-104">ExpressRoute 회로의 피어링 만들기 및 수정(클래식)</span><span class="sxs-lookup"><span data-stu-id="5e680-104">Create and modify peering for an ExpressRoute circuit (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5e680-105">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="5e680-105">Azure portal</span></span>](expressroute-howto-routing-portal-resource-manager.md)
> * [<span data-ttu-id="5e680-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5e680-106">PowerShell</span></span>](expressroute-howto-routing-arm.md)
> * [<span data-ttu-id="5e680-107">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="5e680-107">Azure CLI</span></span>](howto-routing-cli.md)
> * [<span data-ttu-id="5e680-108">비디오 - 개인 피어링</span><span class="sxs-lookup"><span data-stu-id="5e680-108">Video - Private peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="5e680-109">비디오 - 공용 피어링</span><span class="sxs-lookup"><span data-stu-id="5e680-109">Video - Public peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="5e680-110">비디오 - Microsoft 피어링</span><span class="sxs-lookup"><span data-stu-id="5e680-110">Video - Microsoft peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="5e680-111">PowerShell(클래식)</span><span class="sxs-lookup"><span data-stu-id="5e680-111">PowerShell (classic)</span></span>](expressroute-howto-routing-classic.md)
> 

<span data-ttu-id="5e680-112">이 문서에서는 PowerShell 및 클래식 배포 모델을 사용하여 Express 경로 회로에 대한 라우팅 구성을 만들고 관리하는 단계를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-112">This article walks you through the steps to create and manage routing configuration for an ExpressRoute circuit using PowerShell and the classic deployment model.</span></span> <span data-ttu-id="5e680-113">아래 단계에서는 Express 경로 회로에 대한 피어링의 상태 확인, 업데이트 또는 삭제 및 프로비전 해제를 수행하는 방법도 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-113">The steps below will also show you how to check the status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="5e680-114">**Azure 배포 모델 정보**</span><span class="sxs-lookup"><span data-stu-id="5e680-114">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]


## <a name="configuration-prerequisites"></a><span data-ttu-id="5e680-115">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="5e680-115">Configuration prerequisites</span></span>
* <span data-ttu-id="5e680-116">최신 버전의 Azure SM(서비스 관리) PowerShell cmdlet이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-116">You will need the latest version of the Azure Service Management (SM) PowerShell cmdlets.</span></span> <span data-ttu-id="5e680-117">자세한 내용은 [Azure PowerShell cmdlet 시작](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5e680-117">For more information, see [Getting started with Azure PowerShell cmdlets](/powershell/azure/overview).</span></span>  
* <span data-ttu-id="5e680-118">구성을 시작하기 전에 [필수 구성 요소](expressroute-prerequisites.md) 페이지, [라우팅 요구 사항](expressroute-routing.md) 페이지 및 [워크플로](expressroute-workflows.md) 페이지를 검토했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-118">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md) page, the [routing requirements](expressroute-routing.md) page, and the [workflows](expressroute-workflows.md) page before you begin configuration.</span></span>
* <span data-ttu-id="5e680-119">활성화된 Express 경로 회로가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-119">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="5e680-120">지침을 수행하여 [Express 경로 회로를 만들고](expressroute-howto-circuit-classic.md) 진행하기 전에 연결 공급자를 통해 회로를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-120">Follow the instructions to [create an ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have the circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="5e680-121">Express 경로 회로는 아래에 설명한 cmdlet을 실행할 수 있도록 프로비전되고 활성화된 상태여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-121">The ExpressRoute circuit must be in a provisioned and enabled state for you to be able to run the cmdlets described below.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5e680-122">이 지침은 2계층 연결 서비스를 제공하는 서비스 공급자를 사용하여 만든 회로에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-122">These instructions only apply to circuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="5e680-123">관리된 3계층 서비스(일반적으로 MPLS와 같은 IPVPN)를 제공하는 서비스 공급자를 사용하는 경우 연결 공급자는 사용자를 위해 라우팅을 구성하고 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-123">If you are using a service provider offering managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

<span data-ttu-id="5e680-124">Express 경로 회로에 한 가지, 두 가지 또는 세 가지 피어링을 구성할 수 있습니다.(개인, Azure 공용 Azure 및 Microsoft)</span><span class="sxs-lookup"><span data-stu-id="5e680-124">You can configure one, two, or all three peerings (Azure private, Azure public and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="5e680-125">선택한 순서로 피어링을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-125">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="5e680-126">그러나 각 피어링의 구성을 한 번에 하나씩 완료하도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-126">However, you must make sure that you complete the configuration of each peering one at a time.</span></span>


### <a name="log-in-to-your-azure-account-and-select-a-subscription"></a><span data-ttu-id="5e680-127">Azure 계정에 로그인 및 구독 선택</span><span class="sxs-lookup"><span data-stu-id="5e680-127">Log in to your Azure account and select a subscription</span></span>
1. <span data-ttu-id="5e680-128">상승된 권한으로 PowerShell 콘솔을 열고 계정에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-128">Open your PowerShell console with elevated rights and connect to your account.</span></span> <span data-ttu-id="5e680-129">연결에 도움이 되도록 다음 예제를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-129">Use the following example to help you connect:</span></span>

        Login-AzureRmAccount

2. <span data-ttu-id="5e680-130">계정에 대한 구독을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-130">Check the subscriptions for the account.</span></span>

        Get-AzureRmSubscription

3. <span data-ttu-id="5e680-131">둘 이상의 구독이 있는 경우 사용할 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-131">If you have more than one subscription, select the subscription that you want to use.</span></span>

        Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"

4. <span data-ttu-id="5e680-132">다음 cmdlet을 사용하여 클래식 배포 모델용 PowerShell에 Azure 구독을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-132">Next, use the following cmdlet to add your Azure subscription to PowerShell for the classic deployment model.</span></span>

        Add-AzureAccount


## <a name="azure-private-peering"></a><span data-ttu-id="5e680-133">Azure 개인 피어링</span><span class="sxs-lookup"><span data-stu-id="5e680-133">Azure private peering</span></span>
<span data-ttu-id="5e680-134">이 섹션에서는 Express 경로 회로에 Azure 개인 피어링 구성을 만들고 가져오며 업데이트 및 삭제하는 방법에 대한 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-134">This section provides instructions on how to create, get, update, and delete the Azure private peering configuration for an ExpressRoute circuit.</span></span> 

### <a name="to-create-azure-private-peering"></a><span data-ttu-id="5e680-135">Azure 개인 피어링을 만들려면</span><span class="sxs-lookup"><span data-stu-id="5e680-135">To create Azure private peering</span></span>
1. <span data-ttu-id="5e680-136">**Express 경로에 대한 PowerShell 모듈을 가져옵니다.**</span><span class="sxs-lookup"><span data-stu-id="5e680-136">**Import the PowerShell module for ExpressRoute.**</span></span>
   
    <span data-ttu-id="5e680-137">Express 경로 cmdlet을 사용하려면 Azure와 Express 경로 모듈을 PowerShell 세션으로 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-137">You must import the Azure and ExpressRoute modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span></span> <span data-ttu-id="5e680-138">다음 명령을 실행하여 PowerShell 세션으로 Azure 및 Express 경로 모듈을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-138">Run the following commands to import the Azure and ExpressRoute modules into the PowerShell session.</span></span>  
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. <span data-ttu-id="5e680-139">**Express 경로 회로를 만듭니다.**</span><span class="sxs-lookup"><span data-stu-id="5e680-139">**Create an ExpressRoute circuit.**</span></span>
   
    <span data-ttu-id="5e680-140">지침에 따라 [Express 경로 회로](expressroute-howto-circuit-classic.md)를 만들고 연결 공급자를 통해 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-140">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have it provisioned by the connectivity provider.</span></span> <span data-ttu-id="5e680-141">연결 공급자가 관리된 3계층 서비스를 제공하는 경우 연결 공급자를 요청하여 Azure 개인 피어링을 사용하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-141">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure private peering for you.</span></span> <span data-ttu-id="5e680-142">이 경우에 다음 섹션에 나열된 지침에 따를 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-142">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="5e680-143">그러나 회로를 만든 후에 연결 공급자가 라우팅을 관리하지 않는 경우 아래 지침을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-143">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow the instructions below.</span></span> 
3. <span data-ttu-id="5e680-144">**Express 경로 회로를 확인하여 프로비전되도록 합니다.**</span><span class="sxs-lookup"><span data-stu-id="5e680-144">**Check the ExpressRoute circuit to ensure it is provisioned.**</span></span>
   
    <span data-ttu-id="5e680-145">먼저 Express 경로 회로가 프로비전되고 사용 가능한지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-145">You must first check to see if the ExpressRoute circuit is Provisioned and also Enabled.</span></span> <span data-ttu-id="5e680-146">아래 예제를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5e680-146">See the example below.</span></span>
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    <span data-ttu-id="5e680-147">회로가 프로비전 및 사용 가능으로 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-147">Make sure that the circuit shows as Provisioned and Enabled.</span></span> <span data-ttu-id="5e680-148">그렇지 않은 경우 연결 공급자로 작업하여 회로를 필요한 상태 및 상태로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-148">If it doesn't, work with your connectivity provider to get your circuit to the required state and status.</span></span>
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. <span data-ttu-id="5e680-149">**회로에 Azure 개인 피어링을 구성합니다.**</span><span class="sxs-lookup"><span data-stu-id="5e680-149">**Configure Azure private peering for the circuit.**</span></span>
   
    <span data-ttu-id="5e680-150">다음 단계를 계속 진행하기 전에 다음 항목이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-150">Make sure that you have the following items before you proceed with the next steps:</span></span>
   
   * <span data-ttu-id="5e680-151">기본 링크에 대한 /30 서브넷입니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-151">A /30 subnet for the primary link.</span></span> <span data-ttu-id="5e680-152">가상 네트워크에 예약된 주소 공간의 일부가 아니어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-152">This must not be part of any address space reserved for virtual networks.</span></span>
   * <span data-ttu-id="5e680-153">보조 링크에 대한 /30 서브넷입니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-153">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="5e680-154">가상 네트워크에 예약된 주소 공간의 일부가 아니어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-154">This must not be part of any address space reserved for virtual networks.</span></span>
   * <span data-ttu-id="5e680-155">피어링을 설정할 유효한 VLAN ID입니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-155">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="5e680-156">회로에 다른 피어링이 동일한 VLAN ID를 사용하지 않는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-156">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
   * <span data-ttu-id="5e680-157">피어링에 대한 AS 숫자입니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-157">AS number for peering.</span></span> <span data-ttu-id="5e680-158">2바이트 및 4바이트 AS 번호를 모두 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-158">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="5e680-159">이 피어링에 개인 AS 숫자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-159">You can use a private AS number for this peering.</span></span> <span data-ttu-id="5e680-160">65515를 사용하지 않는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-160">Ensure that you are not using 65515.</span></span>
   * <span data-ttu-id="5e680-161">하나를 사용하기로 선택한 경우 MD5 해시를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-161">An MD5 hash if you choose to use one.</span></span> <span data-ttu-id="5e680-162">**선택 사항입니다**.</span><span class="sxs-lookup"><span data-stu-id="5e680-162">**This is optional**.</span></span>
     
    <span data-ttu-id="5e680-163">다음 cmdlet을 실행하여 회로에 Azure 개인 피어링을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-163">You can run the following cmdlet to configure Azure private peering for your circuit.</span></span>
     
        <span data-ttu-id="5e680-164">New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100</span><span class="sxs-lookup"><span data-stu-id="5e680-164">New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100</span></span>
     
    <span data-ttu-id="5e680-165">MD5 해시를 사용하기로 선택한 경우 아래 cmdlet를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-165">You can use the cmdlet below if you choose to use an MD5 hash.</span></span>
     
        <span data-ttu-id="5e680-166">New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100 -SharedKey "A1B2C3D4"</span><span class="sxs-lookup"><span data-stu-id="5e680-166">New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100 -SharedKey "A1B2C3D4"</span></span>
     
     > [!IMPORTANT]
     > <span data-ttu-id="5e680-167">고객 ASN이 아닌 피어링 ASN로 AS 번호를 지정했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-167">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
     > 
     > 

### <a name="to-view-azure-private-peering-details"></a><span data-ttu-id="5e680-168">Azure 개인 피어링 세부 정보를 보려면</span><span class="sxs-lookup"><span data-stu-id="5e680-168">To view Azure private peering details</span></span>
<span data-ttu-id="5e680-169">다음 cmdlet을 사용하여 구성 세부 정보를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-169">You can get configuration details using the following cmdlet</span></span>

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


### <a name="to-update-azure-private-peering-configuration"></a><span data-ttu-id="5e680-170">Azure 개인 피어링 구성을 업데이트하려면</span><span class="sxs-lookup"><span data-stu-id="5e680-170">To update Azure private peering configuration</span></span>
<span data-ttu-id="5e680-171">다음 cmdlet을 사용하여 구성의 일부를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-171">You can update any part of the configuration using the following cmdlet.</span></span> <span data-ttu-id="5e680-172">아래 예제에서는 회로의 VLAN ID를 100개에서 500개로 업데이트 중입니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-172">In the example below, the VLAN ID of the circuit is being updated from 100 to 500.</span></span>

    Set-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 500 -SharedKey "A1B2C3D4"

### <a name="to-delete-azure-private-peering"></a><span data-ttu-id="5e680-173">Azure 개인 피어링을 삭제하려면</span><span class="sxs-lookup"><span data-stu-id="5e680-173">To delete Azure private peering</span></span>
<span data-ttu-id="5e680-174">다음 cmdlet을 실행하여 피어링 구성을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-174">You can remove your peering configuration by running the following cmdlet.</span></span>

> [!WARNING]
> <span data-ttu-id="5e680-175">이 cmdlet을 실행하기 전에 모든 가상 네트워크가 Express 경로 회로에서 연결되지 않았는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-175">You must ensure that all virtual networks are unlinked from the ExpressRoute circuit before running this cmdlet.</span></span> 
> 
> 

    Remove-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"


## <a name="azure-public-peering"></a><span data-ttu-id="5e680-176">Azure 공용 피어링</span><span class="sxs-lookup"><span data-stu-id="5e680-176">Azure public peering</span></span>
<span data-ttu-id="5e680-177">이 섹션에서는 Express 경로 회로에 Azure 공용 피어링 구성을 만들고 가져오며 업데이트 및 삭제하는 방법에 대한 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-177">This section provides instructions on how to create, get, update and delete the Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="to-create-azure-public-peering"></a><span data-ttu-id="5e680-178">Azure 공용 피어링을 만들려면</span><span class="sxs-lookup"><span data-stu-id="5e680-178">To create Azure public peering</span></span>
1. <span data-ttu-id="5e680-179">**Express 경로에 대한 PowerShell 모듈을 가져옵니다.**</span><span class="sxs-lookup"><span data-stu-id="5e680-179">**Import the PowerShell module for ExpressRoute.**</span></span>
   
    <span data-ttu-id="5e680-180">Express 경로 cmdlet을 사용하려면 Azure와 Express 경로 모듈을 PowerShell 세션으로 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-180">You must import the Azure and ExpressRoute modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span></span> <span data-ttu-id="5e680-181">다음 명령을 실행하여 PowerShell 세션으로 Azure 및 Express 경로 모듈을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-181">Run the following commands to import the Azure and ExpressRoute modules into the PowerShell session.</span></span> 
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. <span data-ttu-id="5e680-182">**Express 경로 회로 만들기**</span><span class="sxs-lookup"><span data-stu-id="5e680-182">**Create an ExpressRoute circuit**</span></span>
   
    <span data-ttu-id="5e680-183">지침에 따라 [Express 경로 회로](expressroute-howto-circuit-classic.md) 를 만들고 연결 공급자를 통해 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-183">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have it provisioned by the connectivity provider.</span></span> <span data-ttu-id="5e680-184">연결 공급자가 관리된 3계층 서비스를 제공하는 경우 연결 공급자를 요청하여 Azure 공용 피어링을 사용하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-184">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure public peering for you.</span></span> <span data-ttu-id="5e680-185">이 경우에 다음 섹션에 나열된 지침에 따를 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-185">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="5e680-186">그러나 회로를 만든 후에 연결 공급자가 라우팅을 관리하지 않는 경우 아래 지침을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-186">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow the instructions below.</span></span>
3. <span data-ttu-id="5e680-187">**Express 경로 회로를 확인하여 프로비전되도록 합니다.**</span><span class="sxs-lookup"><span data-stu-id="5e680-187">**Check ExpressRoute circuit to ensure it is provisioned**</span></span>
   
    <span data-ttu-id="5e680-188">먼저 Express 경로 회로가 프로비전되고 사용 가능한지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-188">You must first check to see if the ExpressRoute circuit is Provisioned and also Enabled.</span></span> <span data-ttu-id="5e680-189">아래 예제를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5e680-189">See the example below.</span></span>
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    <span data-ttu-id="5e680-190">회로가 프로비전 및 사용 가능으로 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-190">Make sure that the circuit shows as Provisioned and Enabled.</span></span> <span data-ttu-id="5e680-191">그렇지 않은 경우 연결 공급자로 작업하여 회로를 필요한 상태 및 상태로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-191">If it doesn't, work with your connectivity provider to get your circuit to the required state and status.</span></span>
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. <span data-ttu-id="5e680-192">**회로에 Azure 공용 피어링 구성**</span><span class="sxs-lookup"><span data-stu-id="5e680-192">**Configure Azure public peering for the circuit**</span></span>
   
    <span data-ttu-id="5e680-193">더 진행하기 전에 다음 정보가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-193">Ensure that you have the following information before you proceed further.</span></span>
   
   * <span data-ttu-id="5e680-194">기본 링크에 대한 /30 서브넷입니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-194">A /30 subnet for the primary link.</span></span> <span data-ttu-id="5e680-195">유효한 공용 IPv4 접두사여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-195">This must be a valid public IPv4 prefix.</span></span>
   * <span data-ttu-id="5e680-196">보조 링크에 대한 /30 서브넷입니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-196">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="5e680-197">유효한 공용 IPv4 접두사여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-197">This must be a valid public IPv4 prefix.</span></span>
   * <span data-ttu-id="5e680-198">피어링을 설정할 유효한 VLAN ID입니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-198">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="5e680-199">회로에 다른 피어링이 동일한 VLAN ID를 사용하지 않는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-199">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
   * <span data-ttu-id="5e680-200">피어링에 대한 AS 숫자입니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-200">AS number for peering.</span></span> <span data-ttu-id="5e680-201">2바이트 및 4바이트 AS 번호를 모두 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-201">You can use both 2-byte and 4-byte AS numbers.</span></span>
   * <span data-ttu-id="5e680-202">하나를 사용하기로 선택한 경우 MD5 해시를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-202">An MD5 hash if you choose to use one.</span></span> <span data-ttu-id="5e680-203">**선택 사항입니다**.</span><span class="sxs-lookup"><span data-stu-id="5e680-203">**This is optional**.</span></span>
     
    <span data-ttu-id="5e680-204">다음 cmdlet을 실행하여 회로에 Azure 공용 피어링을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-204">You can run the following cmdlet to configure Azure public peering for your circuit</span></span>
     
        <span data-ttu-id="5e680-205">New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200</span><span class="sxs-lookup"><span data-stu-id="5e680-205">New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200</span></span>
     
    <span data-ttu-id="5e680-206">MD5 해시를 사용하기로 선택한 경우 아래 cmdlet를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-206">You can use the cmdlet below if you choose to use an MD5 hash</span></span>
     
        <span data-ttu-id="5e680-207">New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200 -SharedKey "A1B2C3D4"</span><span class="sxs-lookup"><span data-stu-id="5e680-207">New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200 -SharedKey "A1B2C3D4"</span></span>
     
     > [!IMPORTANT]
     > <span data-ttu-id="5e680-208">고객 ASN이 아닌 피어링 ASN로 AS 번호를 지정했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-208">Ensure that you specify your AS number as peering ASN and not customer ASN.</span></span>
     > 
     > 

### <a name="to-view-azure-public-peering-details"></a><span data-ttu-id="5e680-209">Azure 공용 피어링 세부 정보를 보려면</span><span class="sxs-lookup"><span data-stu-id="5e680-209">To view Azure public peering details</span></span>
<span data-ttu-id="5e680-210">다음 cmdlet을 사용하여 구성 세부 정보를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-210">You can get configuration details using the following cmdlet</span></span>

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


### <a name="to-update-azure-public-peering-configuration"></a><span data-ttu-id="5e680-211">Azure 공용 피어링 구성을 업데이트하려면</span><span class="sxs-lookup"><span data-stu-id="5e680-211">To update Azure public peering configuration</span></span>
<span data-ttu-id="5e680-212">다음 cmdlet을 사용하여 구성의 일부를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-212">You can update any part of the configuration using the following cmdlet</span></span>

    Set-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 600 -SharedKey "A1B2C3D4"

<span data-ttu-id="5e680-213">아래 예제에서 회로의 VLAN ID를 200개에서 600개로 업데이트 중입니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-213">The VLAN ID of the circuit is being updated from 200 to 600 in the above example.</span></span>

### <a name="to-delete-azure-public-peering"></a><span data-ttu-id="5e680-214">Azure 공용 피어링을 삭제하려면</span><span class="sxs-lookup"><span data-stu-id="5e680-214">To delete Azure public peering</span></span>
<span data-ttu-id="5e680-215">다음 cmdlet을 실행하여 피어링 구성을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-215">You can remove your peering configuration by running the following cmdlet</span></span>

    Remove-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

## <a name="microsoft-peering"></a><span data-ttu-id="5e680-216">Microsoft 피어링</span><span class="sxs-lookup"><span data-stu-id="5e680-216">Microsoft peering</span></span>
<span data-ttu-id="5e680-217">이 섹션에서는 Express 경로 회로에 Microsoft 피어링 구성을 만들고 가져오며 업데이트 및 삭제하는 방법에 대한 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-217">This section provides instructions on how to create, get, update and delete the Microsoft peering configuration for an ExpressRoute circuit.</span></span> 

### <a name="to-create-microsoft-peering"></a><span data-ttu-id="5e680-218">Microsoft 피어링을 만들려면</span><span class="sxs-lookup"><span data-stu-id="5e680-218">To create Microsoft peering</span></span>
1. <span data-ttu-id="5e680-219">**Express 경로에 대한 PowerShell 모듈을 가져옵니다.**</span><span class="sxs-lookup"><span data-stu-id="5e680-219">**Import the PowerShell module for ExpressRoute.**</span></span>
   
    <span data-ttu-id="5e680-220">Express 경로 cmdlet을 사용하려면 Azure와 Express 경로 모듈을 PowerShell 세션으로 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-220">You must import the Azure and ExpressRoute modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span></span> <span data-ttu-id="5e680-221">다음 명령을 실행하여 PowerShell 세션으로 Azure 및 Express 경로 모듈을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-221">Run the following commands to import the Azure and ExpressRoute modules into the PowerShell session.</span></span>  
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. <span data-ttu-id="5e680-222">**Express 경로 회로 만들기**</span><span class="sxs-lookup"><span data-stu-id="5e680-222">**Create an ExpressRoute circuit**</span></span>
   
    <span data-ttu-id="5e680-223">지침에 따라 [Express 경로 회로](expressroute-howto-circuit-classic.md) 를 만들고 연결 공급자를 통해 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-223">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have it provisioned by the connectivity provider.</span></span> <span data-ttu-id="5e680-224">연결 공급자가 관리된 3계층 서비스를 제공하는 경우 연결 공급자를 요청하여 Azure 개인 피어링을 사용하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-224">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure private peering for you.</span></span> <span data-ttu-id="5e680-225">이 경우에 다음 섹션에 나열된 지침에 따를 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-225">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="5e680-226">그러나 회로를 만든 후에 연결 공급자가 라우팅을 관리하지 않는 경우 아래 지침을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-226">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow the instructions below.</span></span>
3. <span data-ttu-id="5e680-227">**Express 경로 회로를 확인하여 프로비전되도록 합니다.**</span><span class="sxs-lookup"><span data-stu-id="5e680-227">**Check ExpressRoute circuit to ensure it is provisioned**</span></span>
   
    <span data-ttu-id="5e680-228">먼저 Express 경로 회로가 프로비전되고 사용 가능한 상태인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-228">You must first check to see if the ExpressRoute circuit is in Provisioned and Enabled state.</span></span>
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    <span data-ttu-id="5e680-229">회로가 프로비전 및 사용 가능으로 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-229">Make sure that the circuit shows as Provisioned and Enabled.</span></span> <span data-ttu-id="5e680-230">그렇지 않은 경우 연결 공급자로 작업하여 회로를 필요한 상태 및 상태로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-230">If it doesn't, work with your connectivity provider to get your circuit to the required state and status.</span></span>
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. <span data-ttu-id="5e680-231">**회로에 Microsoft 피어링 구성**</span><span class="sxs-lookup"><span data-stu-id="5e680-231">**Configure Microsoft peering for the circuit**</span></span>
   
    <span data-ttu-id="5e680-232">진행하기 전에 다음 정보가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-232">Make sure that you have the following information before you proceed.</span></span>
   
   * <span data-ttu-id="5e680-233">기본 링크에 대한 /30 서브넷입니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-233">A /30 subnet for the primary link.</span></span> <span data-ttu-id="5e680-234">사용자가 소유하고 RIR/IRR에 등록된 유효한 공용 IPv4 접두사여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-234">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
   * <span data-ttu-id="5e680-235">보조 링크에 대한 /30 서브넷입니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-235">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="5e680-236">사용자가 소유하고 RIR/IRR에 등록된 유효한 공용 IPv4 접두사여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-236">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
   * <span data-ttu-id="5e680-237">피어링을 설정할 유효한 VLAN ID입니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-237">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="5e680-238">회로에 다른 피어링이 동일한 VLAN ID를 사용하지 않는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-238">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
   * <span data-ttu-id="5e680-239">피어링에 대한 AS 숫자입니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-239">AS number for peering.</span></span> <span data-ttu-id="5e680-240">2바이트 및 4바이트 AS 번호를 모두 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-240">You can use both 2-byte and 4-byte AS numbers.</span></span>
   * <span data-ttu-id="5e680-241">보급된 접두사: BGP 세션을 통해 보급하려는 모든 접두사 목록을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-241">Advertised prefixes: You must provide a list of all prefixes you plan to advertise over the BGP session.</span></span> <span data-ttu-id="5e680-242">공용 IP 주소 접두사만 수락됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-242">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="5e680-243">접두사 집합을 보내려는 경우에 쉼표로 구분 된 목록을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-243">You can send a comma separated list if you plan to send a set of prefixes.</span></span> <span data-ttu-id="5e680-244">이 접두사는 RIR/IRR에 등록되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-244">These prefixes must be registered to you in an RIR / IRR.</span></span>
   * <span data-ttu-id="5e680-245">고객 ASN: 피어링 AS 숫자에 등록되지 않은 광고 접두사인 경우 등록된 AS 번호를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-245">Customer ASN: If you are advertising prefixes that are not registered to the peering AS number, you can specify the AS number to which they are registered.</span></span> <span data-ttu-id="5e680-246">**선택 사항입니다**.</span><span class="sxs-lookup"><span data-stu-id="5e680-246">**This is optional**.</span></span>
   * <span data-ttu-id="5e680-247">라우팅 레지스트리 이름: AS 번호 및 접두사가 등록된 RIR/ IRR를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-247">Routing Registry Name: You can specify the RIR / IRR against which the AS number and prefixes are registered.</span></span>
   * <span data-ttu-id="5e680-248">하나를 사용하기로 선택한 경우 MD5 해시를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-248">An MD5 hash, if you choose to use one.</span></span> <span data-ttu-id="5e680-249">**선택 사항입니다.**</span><span class="sxs-lookup"><span data-stu-id="5e680-249">**This is optional.**</span></span>
     
    <span data-ttu-id="5e680-250">다음 cmdlet을 실행하여 회로에 Microsoft 피어링을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-250">You can run the following cmdlet to configure Microsoft pering for your circuit</span></span>
     
        <span data-ttu-id="5e680-251">New-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"</span><span class="sxs-lookup"><span data-stu-id="5e680-251">New-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"</span></span>

### <a name="to-view-microsoft-peering-details"></a><span data-ttu-id="5e680-252">Microsoft 피어링 세부 정보를 보려면</span><span class="sxs-lookup"><span data-stu-id="5e680-252">To view Microsoft peering details</span></span>
<span data-ttu-id="5e680-253">다음 cmdlet을 사용하여 구성 세부 정보를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-253">You can get configuration details using the following cmdlet.</span></span>

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


### <a name="to-update-microsoft-peering-configuration"></a><span data-ttu-id="5e680-254">Microsoft 피어링 구성을 업데이트하려면</span><span class="sxs-lookup"><span data-stu-id="5e680-254">To update Microsoft peering configuration</span></span>
<span data-ttu-id="5e680-255">다음 cmdlet을 사용하여 구성의 일부를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-255">You can update any part of the configuration using the following cmdlet.</span></span>

    Set-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"

### <a name="to-delete-microsoft-peering"></a><span data-ttu-id="5e680-256">Microsoft 피어링을 삭제하려면</span><span class="sxs-lookup"><span data-stu-id="5e680-256">To delete Microsoft peering</span></span>
<span data-ttu-id="5e680-257">다음 cmdlet을 실행하여 피어링 구성을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-257">You can remove your peering configuration by running the following cmdlet.</span></span>

    Remove-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

## <a name="next-steps"></a><span data-ttu-id="5e680-258">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5e680-258">Next steps</span></span>
<span data-ttu-id="5e680-259">이제 [VNet을 Express 경로 회로에 연결](expressroute-howto-linkvnet-classic.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5e680-259">Next, [Link a VNet to an ExpressRoute circuit](expressroute-howto-linkvnet-classic.md).</span></span>

* <span data-ttu-id="5e680-260">워크플로에 대한 자세한 내용은 [Express 경로 워크플로](expressroute-workflows.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5e680-260">For more information about workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="5e680-261">회로 피어링에 대한 자세한 내용은 [Express 경로 회로 및 라우팅 도메인](expressroute-circuit-peerings.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5e680-261">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>


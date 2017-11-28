---
title: "ExpressRoute 회로에 가상 네트워크 연결: PowerShell: Azure | Microsoft Docs"
description: "이 문서는 리소스 관리자 배포 모델 및 PowerShell을 사용하여 VNet(가상 네트워크)을 Express 경로 회로에 연결하는 방법에 대한 개요를 제공합니다."
services: expressroute
documentationcenter: na
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: daacb6e5-705a-456f-9a03-c4fc3f8c1f7e
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: ganesr
ms.openlocfilehash: 8c2f3036f754a98090ab860f95900416690ebf83
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="connect-a-virtual-network-to-an-expressroute-circuit"></a><span data-ttu-id="60022-103">Virtual Network를 ExpressRoute 회로에 연결</span><span class="sxs-lookup"><span data-stu-id="60022-103">Connect a virtual network to an ExpressRoute circuit</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="60022-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="60022-104">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="60022-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="60022-105">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="60022-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="60022-106">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="60022-107">비디오 - Azure Portal</span><span class="sxs-lookup"><span data-stu-id="60022-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="60022-108">PowerShell(클래식)</span><span class="sxs-lookup"><span data-stu-id="60022-108">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
>

<span data-ttu-id="60022-109">이 문서를 참조하면 Resource Manager 배포 모델 및 PowerShell을 사용하여 VNet(가상 네트워크)을 Azure ExpressRoute 회로에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60022-109">This article helps you link virtual networks (VNets) to Azure ExpressRoute circuits by using the Resource Manager deployment model and PowerShell.</span></span> <span data-ttu-id="60022-110">가상 네트워크는 같은 구독에 있을 수도 있고 다른 구독의 일부일 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60022-110">Virtual networks can either be in the same subscription or part of another subscription.</span></span> <span data-ttu-id="60022-111">또한 이 문서는 가상 네트워크 링크를 업데이트하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="60022-111">This article also shows you how to update a virtual network link.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="60022-112">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="60022-112">Before you begin</span></span>
* <span data-ttu-id="60022-113">최신 버전의 Azure PowerShell 모듈을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="60022-113">Install the latest version of the Azure PowerShell modules.</span></span> <span data-ttu-id="60022-114">자세한 내용은 [Azure PowerShell 설치 및 구성하는 방법](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60022-114">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="60022-115">구성을 시작하기 전에 [필수 조건](expressroute-prerequisites.md), [라우팅 요구 사항](expressroute-routing.md) 및 [워크플로](expressroute-workflows.md)를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="60022-115">Review the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="60022-116">활성화된 Express 경로 회로가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60022-116">You must have an active ExpressRoute circuit.</span></span> 
  * <span data-ttu-id="60022-117">지침을 수행하여 [Express 경로 회로를 만들고](expressroute-howto-circuit-arm.md) 연결 공급자를 통해 회로를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="60022-117">Follow the instructions to [create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have the circuit enabled by your connectivity provider.</span></span> 
  * <span data-ttu-id="60022-118">회로에 구성된 Azure 개인 피어링이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="60022-118">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="60022-119">라우팅 지침에 대한 문서는 [라우팅 구성](expressroute-howto-routing-arm.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60022-119">See the [configure routing](expressroute-howto-routing-arm.md) article for routing instructions.</span></span> 
  * <span data-ttu-id="60022-120">Azure 개인 피어링이 구성되어 있고 네트워크와 Microsoft 간의 BGP 피어링이 종단 간 연결을 사용하도록 작동 중이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60022-120">Ensure that Azure private peering is configured and the BGP peering between your network and Microsoft is up so that you can enable end-to-end connectivity.</span></span>
  * <span data-ttu-id="60022-121">가상 네트워크 및 가상 네트워크 게이트웨이를 만들어서 완전히 프로비전해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60022-121">Ensure that you have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="60022-122">지침에 따라 [ExpressRoute에 대한 가상 네트워크 게이트웨이를 만듭니다](expressroute-howto-add-gateway-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="60022-122">Follow the instructions to [create a virtual network gateway for ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span></span> <span data-ttu-id="60022-123">ExpressRoute의 가상 네트워크 게이트웨이는 GatewayType으로 VPN이 아닌 'ExpressRoute'를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="60022-123">A virtual network gateway for ExpressRoute uses the GatewayType 'ExpressRoute', not VPN.</span></span>

* <span data-ttu-id="60022-124">최대 10개의 가상 네트워크를 표준 Express 경로 회로에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60022-124">You can link up to 10 virtual networks to a standard ExpressRoute circuit.</span></span> <span data-ttu-id="60022-125">표준 Express 경로 회로를 사용하는 경우 모든 가상 네트워크는 동일한 지역에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60022-125">All virtual networks must be in the same geopolitical region when using a standard ExpressRoute circuit.</span></span> 

* <span data-ttu-id="60022-126">Express 경로 프리미엄 추가 기능을 사용하도록 설정하면 Express 경로 회로의 지역 외부에서 가상 네트워크를 연결하거나 Express 경로 회로에 많은 수의 가상 네트워크를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60022-126">You can link a virtual networks outside of the geopolitical region of the ExpressRoute circuit, or connect a larger number of virtual networks to your ExpressRoute circuit if you enabled the ExpressRoute premium add-on.</span></span> <span data-ttu-id="60022-127">프리미엄 추가 기능에 대한 자세한 내용은 [FAQ](expressroute-faqs.md) 에서 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="60022-127">Check the [FAQ](expressroute-faqs.md) for more details on the premium add-on.</span></span>


## <a name="connect-a-virtual-network-in-the-same-subscription-to-a-circuit"></a><span data-ttu-id="60022-128">동일한 구독에 있는 가상 네트워크를 회로에 연결</span><span class="sxs-lookup"><span data-stu-id="60022-128">Connect a virtual network in the same subscription to a circuit</span></span>
<span data-ttu-id="60022-129">다음 cmdlet를 사용하여 Express 경로 회로에 가상 네트워크 게이트웨이를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60022-129">You can connect a virtual network gateway to an ExpressRoute circuit by using the following cmdlet.</span></span> <span data-ttu-id="60022-130">cmdlet을 실행하기 전에 가상 네트워크 게이트웨이가 연결을 위해 생성되고 준비되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="60022-130">Make sure that the virtual network gateway is created and is ready for linking before you run the cmdlet:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$gw = Get-AzureRmVirtualNetworkGateway -Name "ExpressRouteGw" -ResourceGroupName "MyRG"
$connection = New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName "MyRG" -Location "East US" -VirtualNetworkGateway1 $gw -PeerId $circuit.Id -ConnectionType ExpressRoute
```

## <a name="connect-a-virtual-network-in-a-different-subscription-to-a-circuit"></a><span data-ttu-id="60022-131">다른 구독에 있는 가상 네트워크를 회로에 연결</span><span class="sxs-lookup"><span data-stu-id="60022-131">Connect a virtual network in a different subscription to a circuit</span></span>
<span data-ttu-id="60022-132">여러 구독에서 Express 경로 회로를 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60022-132">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="60022-133">아래 그림에는 여러 구독에서 Express 경로 회로에 대한 작업을 공유하는 방법의 간단한 계통도가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60022-133">The following figure shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

<span data-ttu-id="60022-134">큰 구름 안에 있는 각각의 작은 구름은 한 조직 내의 여러 부서에 속하는 구독을 나타내는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="60022-134">Each of the smaller clouds within the large cloud is used to represent subscriptions that belong to different departments within an organization.</span></span> <span data-ttu-id="60022-135">조직 내의 각 부서는 자체 구독을 사용하여 서비스를 배포하되, 단일 Express 경로 회로를 공유하여 온-프레미스 네트워크로 다시 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60022-135">Each of the departments within the organization can use their own subscription for deploying their services--but they can share a single ExpressRoute circuit to connect back to your on-premises network.</span></span> <span data-ttu-id="60022-136">단일 부서(이 예제에서는 IT)가 Express 경로 회로를 소유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60022-136">A single department (in this example: IT) can own the ExpressRoute circuit.</span></span> <span data-ttu-id="60022-137">조직 내의 기타 구독도 Express 경로 회로를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60022-137">Other subscriptions within the organization can use the ExpressRoute circuit.</span></span>

> [!NOTE]
> <span data-ttu-id="60022-138">ExpressRoute 회로에 대한 연결 및 대역폭 요금은 구독 소유자에게 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="60022-138">Connectivity and bandwidth charges for the ExpressRoute circuit will be applied to the subscription owner.</span></span> <span data-ttu-id="60022-139">모든 가상 네트워크는 동일한 대역폭을 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="60022-139">All virtual networks share the same bandwidth.</span></span>
> 
> 

![구독 간 연결](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)


### <a name="administration---circuit-owners-and-circuit-users"></a><span data-ttu-id="60022-141">관리 - 회로 소유자 및 회로 사용자</span><span class="sxs-lookup"><span data-stu-id="60022-141">Administration - circuit owners and circuit users</span></span>

<span data-ttu-id="60022-142">’회로 소유자’는 ExpressRoute 회로 리소스의 인증된 고급 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="60022-142">The 'circuit owner' is an authorized Power User of the ExpressRoute circuit resource.</span></span> <span data-ttu-id="60022-143">회로 소유자는 '회로 사용자'가 사용할 수 있는 권한 부여를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60022-143">The circuit owner can create authorizations that can be redeemed by 'circuit users'.</span></span> <span data-ttu-id="60022-144">회로 사용자는 ExpressRoute 회로와 동일한 구독 내에 있지 않은 가상 네트워크 게이트웨이의 소유자입니다.</span><span class="sxs-lookup"><span data-stu-id="60022-144">Circuit users are owners of virtual network gateways that are not within the same subscription as the ExpressRoute circuit.</span></span> <span data-ttu-id="60022-145">회로 사용자는 가상 네트워크당 하나의 권한 부여를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60022-145">Circuit users can redeem authorizations (one authorization per virtual network).</span></span>

<span data-ttu-id="60022-146">회로 소유자는 언제든지 부여된 권한을 수정하고 해지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60022-146">The circuit owner has the power to modify and revoke authorizations at any time.</span></span> <span data-ttu-id="60022-147">권한 부여를 해지하면 액세스가 해지된 구독에서 모든 링크 연결이 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="60022-147">Revoking an authorization results in all link connections being deleted from the subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="60022-148">회로 소유자 작업</span><span class="sxs-lookup"><span data-stu-id="60022-148">Circuit owner operations</span></span>

<span data-ttu-id="60022-149">**권한 부여를 만들려면**</span><span class="sxs-lookup"><span data-stu-id="60022-149">**To create an authorization**</span></span>

<span data-ttu-id="60022-150">회로 소유자가 권한 부여를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="60022-150">The circuit owner creates an authorization.</span></span> <span data-ttu-id="60022-151">그러면 회로 사용자가 Express 경로 회로에 가상 네트워크 게이트웨이를 연결하는 데 사용할 수 있는 권한 부여 키가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="60022-151">This results in the creation of an authorization key that can be used by a circuit user to connect their virtual network gateways to the ExpressRoute circuit.</span></span> <span data-ttu-id="60022-152">권한 부여는 하나의 연결에만 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="60022-152">An authorization is valid for only one connection.</span></span>

<span data-ttu-id="60022-153">다음 cmdlet 조각은 권한 부여를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="60022-153">The following cmdlet snippet shows how to create an authorization:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
Add-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization1"
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit

$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$auth1 = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization1"
```


<span data-ttu-id="60022-154">이에 대한 응답에는 권한 부여 키와 상태가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="60022-154">The response to this will contain the authorization key and status:</span></span>

    Name                   : MyAuthorization1
    Id                     : /subscriptions/&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&/resourceGroups/ERCrossSubTestRG/providers/Microsoft.Network/expressRouteCircuits/CrossSubTest/authorizations/MyAuthorization1
    Etag                   : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&& 
    AuthorizationKey       : ####################################
    AuthorizationUseStatus : Available
    ProvisioningState      : Succeeded



<span data-ttu-id="60022-155">**권한 부여를 검토하려면**</span><span class="sxs-lookup"><span data-stu-id="60022-155">**To review authorizations**</span></span>

<span data-ttu-id="60022-156">회로 소유자는 다음 cmdlet을 실행하여 특정 회로에 발급한 모든 권한 부여를 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60022-156">The circuit owner can review all authorizations that are issued on a particular circuit by running the following cmdlet:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$authorizations = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit
```

<span data-ttu-id="60022-157">**권한 부여를 추가하려면**</span><span class="sxs-lookup"><span data-stu-id="60022-157">**To add authorizations**</span></span>

<span data-ttu-id="60022-158">회로 소유자는 다음 cmdlet를 사용하여 권한 부여를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60022-158">The circuit owner can add authorizations by using the following cmdlet:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
Add-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization2"
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit

$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$authorizations = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit
```

<span data-ttu-id="60022-159">**권한 부여를 삭제하려면**</span><span class="sxs-lookup"><span data-stu-id="60022-159">**To delete authorizations**</span></span>

<span data-ttu-id="60022-160">회로 소유자는 다음 cmdlet을 실행하여 권한 부여를 취소/삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60022-160">The circuit owner can revoke/delete authorizations to the user by running the following cmdlet:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuitAuthorization -Name "MyAuthorization2" -ExpressRouteCircuit $circuit
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit
```    

### <a name="circuit-user-operations"></a><span data-ttu-id="60022-161">회로 사용자 작업</span><span class="sxs-lookup"><span data-stu-id="60022-161">Circuit user operations</span></span>

<span data-ttu-id="60022-162">회로 사용자는 회로 소유자로부터 권한 부여 키를 받아야 하며 피어 ID가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="60022-162">The circuit user needs the peer ID and an authorization key from the circuit owner.</span></span> <span data-ttu-id="60022-163">권한 부여 키는 GUID입니다.</span><span class="sxs-lookup"><span data-stu-id="60022-163">The authorization key is a GUID.</span></span>

<span data-ttu-id="60022-164">다음 명령에서 피어 ID를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60022-164">Peer ID can be checked from the following command:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
```

<span data-ttu-id="60022-165">**연결 권한 부여를 사용하려면**</span><span class="sxs-lookup"><span data-stu-id="60022-165">**To redeem a connection authorization**</span></span>

<span data-ttu-id="60022-166">회로 사용자는 다음 cmdlet을 실행하여 링크 권한 부여를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60022-166">The circuit user can run the following cmdlet to redeem a link authorization:</span></span>

```powershell
$id = "/subscriptions/********************************/resourceGroups/ERCrossSubTestRG/providers/Microsoft.Network/expressRouteCircuits/MyCircuit"    
$gw = Get-AzureRmVirtualNetworkGateway -Name "ExpressRouteGw" -ResourceGroupName "MyRG"
$connection = New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName "RemoteResourceGroup" -Location "East US" -VirtualNetworkGateway1 $gw -PeerId $id -ConnectionType ExpressRoute -AuthorizationKey "^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^"
```

<span data-ttu-id="60022-167">**연결 권한 부여를 해제하려면**</span><span class="sxs-lookup"><span data-stu-id="60022-167">**To release a connection authorization**</span></span>

<span data-ttu-id="60022-168">Express 경로 회로와 가상 네트워크의 연결을 삭제하여 권한 부여를 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60022-168">You can release an authorization by deleting the connection that links the ExpressRoute circuit to the virtual network.</span></span>

## <a name="modify-a-virtual-network-connection"></a><span data-ttu-id="60022-169">가상 네트워크 연결 수정</span><span class="sxs-lookup"><span data-stu-id="60022-169">Modify a virtual network connection</span></span>
<span data-ttu-id="60022-170">가상 네트워크 연결의 특정 속성을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60022-170">You can update certain properties of a virtual network connection.</span></span> 

<span data-ttu-id="60022-171">**연결 무게를 업데이트하려면**</span><span class="sxs-lookup"><span data-stu-id="60022-171">**To update the connection weight**</span></span>

<span data-ttu-id="60022-172">가상 네트워크를 여러 ExpressRoute 회로에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60022-172">Your virtual network can be connected to multiple ExpressRoute circuits.</span></span> <span data-ttu-id="60022-173">둘 이상의 ExpressRoute 회로에서 동일한 접두사를 수신할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60022-173">You may receive the same prefix from more than one ExpressRoute circuit.</span></span> <span data-ttu-id="60022-174">이 접두사를 대상으로 하는 트래픽을 전송할 연결을 선택하기 위해 연결의 *RoutingWeight*를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60022-174">To choose which connection to send traffic destined for this prefix, you can change *RoutingWeight* of a connection.</span></span> <span data-ttu-id="60022-175">트래픽은 제일 높은 *RoutingWeight*를 사용한 연결로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="60022-175">Traffic will be sent on the connection with the highest *RoutingWeight*.</span></span>

```powershell
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name "MyVirtualNetworkConnection" -ResourceGroupName "MyRG"
$connection.RoutingWeight = 100
Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection
```

<span data-ttu-id="60022-176">*RoutingWeight*의 범위는 0에서 32000입니다.</span><span class="sxs-lookup"><span data-stu-id="60022-176">The range of *RoutingWeight* is 0 to 32000.</span></span> <span data-ttu-id="60022-177">기본값은 0입니다.</span><span class="sxs-lookup"><span data-stu-id="60022-177">The default value is 0.</span></span>

## <a name="next-steps"></a><span data-ttu-id="60022-178">다음 단계</span><span class="sxs-lookup"><span data-stu-id="60022-178">Next steps</span></span>
<span data-ttu-id="60022-179">ExpressRoute에 대한 자세한 내용은 [ExpressRoute FAQ](expressroute-faqs.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60022-179">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

---
title: "가상 네트워크 tooan ExpressRoute 회로 연결: PowerShell: Azure | Microsoft Docs"
description: "이 문서는 가상 toolink (Vnet) tooExpressRoute 회로 hello 리소스 관리자 배포 모델 및 PowerShell을 사용 하 여 네트워크 하는 방법의 개요를 제공 합니다."
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
ms.openlocfilehash: e75a9f6b42fa8e1a579e4f19882ec99b277b545f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit"></a><span data-ttu-id="0ccd5-103">가상 네트워크 tooan ExpressRoute 회로 연결</span><span class="sxs-lookup"><span data-stu-id="0ccd5-103">Connect a virtual network tooan ExpressRoute circuit</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0ccd5-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="0ccd5-104">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="0ccd5-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0ccd5-105">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="0ccd5-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="0ccd5-106">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="0ccd5-107">비디오 - Azure Portal</span><span class="sxs-lookup"><span data-stu-id="0ccd5-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="0ccd5-108">PowerShell(클래식)</span><span class="sxs-lookup"><span data-stu-id="0ccd5-108">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
>

<span data-ttu-id="0ccd5-109">이 문서를 사용 하면 hello 리소스 관리자 배포 모델 및 PowerShell을 사용 하 여 가상 네트워크 (Vnet) tooAzure ExpressRoute 회로 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ccd5-109">This article helps you link virtual networks (VNets) tooAzure ExpressRoute circuits by using hello Resource Manager deployment model and PowerShell.</span></span> <span data-ttu-id="0ccd5-110">Hello에 수 가상 네트워크가 동일한 구독 또는 다른 구독에 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ccd5-110">Virtual networks can either be in hello same subscription or part of another subscription.</span></span> <span data-ttu-id="0ccd5-111">또한 이렇게 하면 어떻게 tooupdate 가상 네트워크를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ccd5-111">This article also shows you how tooupdate a virtual network link.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="0ccd5-112">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="0ccd5-112">Before you begin</span></span>
* <span data-ttu-id="0ccd5-113">Hello hello Azure PowerShell 모듈의 최신 버전을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ccd5-113">Install hello latest version of hello Azure PowerShell modules.</span></span> <span data-ttu-id="0ccd5-114">자세한 내용은 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="0ccd5-114">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="0ccd5-115">검토 hello [필수 구성 요소](expressroute-prerequisites.md), [라우팅 요구 사항](expressroute-routing.md), 및 [워크플로](expressroute-workflows.md) 구성을 시작 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="0ccd5-115">Review hello [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="0ccd5-116">활성화된 Express 경로 회로가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ccd5-116">You must have an active ExpressRoute circuit.</span></span> 
  * <span data-ttu-id="0ccd5-117">너무 hello 지침에 따라[ExpressRoute 회로 만들기](expressroute-howto-circuit-arm.md) 있고 hello 회로 연결 공급자가 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ccd5-117">Follow hello instructions too[create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have hello circuit enabled by your connectivity provider.</span></span> 
  * <span data-ttu-id="0ccd5-118">회로에 구성된 Azure 개인 피어링이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0ccd5-118">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="0ccd5-119">Hello 참조 [라우팅 구성](expressroute-howto-routing-arm.md) 라우팅 지침에 대 한 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="0ccd5-119">See hello [configure routing](expressroute-howto-routing-arm.md) article for routing instructions.</span></span> 
  * <span data-ttu-id="0ccd5-120">구성 된 Azure 개인 피어 링 및 종단 간 연결을 사용 하도록 설정할 수 있도록 중일 hello 네트워크와 Microsoft 간에 BGP 피어 링을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ccd5-120">Ensure that Azure private peering is configured and hello BGP peering between your network and Microsoft is up so that you can enable end-to-end connectivity.</span></span>
  * <span data-ttu-id="0ccd5-121">가상 네트워크 및 가상 네트워크 게이트웨이를 만들어서 완전히 프로비전해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ccd5-121">Ensure that you have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="0ccd5-122">너무 hello 지침에 따라[ExpressRoute에 대 한 가상 네트워크 게이트웨이 만들](expressroute-howto-add-gateway-resource-manager.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0ccd5-122">Follow hello instructions too[create a virtual network gateway for ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span></span> <span data-ttu-id="0ccd5-123">ExpressRoute에 대 한 가상 네트워크 게이트웨이 hello GatewayType 'ExpressRoute' 하지 VPN을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0ccd5-123">A virtual network gateway for ExpressRoute uses hello GatewayType 'ExpressRoute', not VPN.</span></span>

* <span data-ttu-id="0ccd5-124">Too10 가상 네트워크 tooa 표준 ExpressRoute 회로를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ccd5-124">You can link up too10 virtual networks tooa standard ExpressRoute circuit.</span></span> <span data-ttu-id="0ccd5-125">모든 가상 네트워크 hello에 있어야 합니다. 동일한 지리적 지역 표준 ExpressRoute 회로 사용 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="0ccd5-125">All virtual networks must be in hello same geopolitical region when using a standard ExpressRoute circuit.</span></span> 

* <span data-ttu-id="0ccd5-126">Hello ExpressRoute 회로의 hello 지리적 영역 외부의 가상 네트워크를 연결 하거나 hello ExpressRoute premium 추가 기능을 사용 하는 경우 많은 수의 가상 네트워크 tooyour ExpressRoute 회로 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ccd5-126">You can link a virtual networks outside of hello geopolitical region of hello ExpressRoute circuit, or connect a larger number of virtual networks tooyour ExpressRoute circuit if you enabled hello ExpressRoute premium add-on.</span></span> <span data-ttu-id="0ccd5-127">Hello 확인 [FAQ](expressroute-faqs.md) hello premium 추가 기능에 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ccd5-127">Check hello [FAQ](expressroute-faqs.md) for more details on hello premium add-on.</span></span>


## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a><span data-ttu-id="0ccd5-128">Hello의 가상 네트워크 연결 동일한 구독 tooa 회로</span><span class="sxs-lookup"><span data-stu-id="0ccd5-128">Connect a virtual network in hello same subscription tooa circuit</span></span>
<span data-ttu-id="0ccd5-129">Hello 다음 cmdlet을 사용 하 여 가상 네트워크 게이트웨이 tooan ExpressRoute 회로 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ccd5-129">You can connect a virtual network gateway tooan ExpressRoute circuit by using hello following cmdlet.</span></span> <span data-ttu-id="0ccd5-130">해당 hello 가상 네트워크 게이트웨이 만들어지고 hello cmdlet을 실행 하기 전에 연결을 위한 준비 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ccd5-130">Make sure that hello virtual network gateway is created and is ready for linking before you run hello cmdlet:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$gw = Get-AzureRmVirtualNetworkGateway -Name "ExpressRouteGw" -ResourceGroupName "MyRG"
$connection = New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName "MyRG" -Location "East US" -VirtualNetworkGateway1 $gw -PeerId $circuit.Id -ConnectionType ExpressRoute
```

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a><span data-ttu-id="0ccd5-131">다른 구독 tooa 회로에 가상 네트워크에 연결</span><span class="sxs-lookup"><span data-stu-id="0ccd5-131">Connect a virtual network in a different subscription tooa circuit</span></span>
<span data-ttu-id="0ccd5-132">여러 구독에서 Express 경로 회로를 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ccd5-132">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="0ccd5-133">다음 그림 hello 간단한 계통도 나와의 ExpressRoute 회로 대 한 일정 공유 works 여러 구독에서.</span><span class="sxs-lookup"><span data-stu-id="0ccd5-133">hello following figure shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

<span data-ttu-id="0ccd5-134">사용 되는 toorepresent 속하는 구독에 조직 내의 toodifferent 부서는 각각 hello 작은 구름 hello 큰 구름 안에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ccd5-134">Each of hello smaller clouds within hello large cloud is used toorepresent subscriptions that belong toodifferent departments within an organization.</span></span> <span data-ttu-id="0ccd5-135">가 자신의 구독을 사용할 수 각각 hello 부서 hello 조직 내에서 배포를 위한 서비스-있지만 공유할 수 단일 express 경로 회로 tooconnect 백 tooyour 온-프레미스 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="0ccd5-135">Each of hello departments within hello organization can use their own subscription for deploying their services--but they can share a single ExpressRoute circuit tooconnect back tooyour on-premises network.</span></span> <span data-ttu-id="0ccd5-136">단일 부서 (이 예제의: IT) hello ExpressRoute 회로 소유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ccd5-136">A single department (in this example: IT) can own hello ExpressRoute circuit.</span></span> <span data-ttu-id="0ccd5-137">Hello 조직 내에서 다른 구독 hello ExpressRoute 회로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ccd5-137">Other subscriptions within hello organization can use hello ExpressRoute circuit.</span></span>

> [!NOTE]
> <span data-ttu-id="0ccd5-138">Hello ExpressRoute 회로 대 한 연결 및 대역폭 요금은 구독 소유자 toohello 적용된 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ccd5-138">Connectivity and bandwidth charges for hello ExpressRoute circuit will be applied toohello subscription owner.</span></span> <span data-ttu-id="0ccd5-139">Hello를 공유 하는 모든 가상 네트워크 대역폭이 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ccd5-139">All virtual networks share hello same bandwidth.</span></span>
> 
> 

![구독 간 연결](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)


### <a name="administration---circuit-owners-and-circuit-users"></a><span data-ttu-id="0ccd5-141">관리 - 회로 소유자 및 회로 사용자</span><span class="sxs-lookup"><span data-stu-id="0ccd5-141">Administration - circuit owners and circuit users</span></span>

<span data-ttu-id="0ccd5-142">'회로 소유자' hello는 hello ExpressRoute 회로 리소스의 인증된 된 전원 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="0ccd5-142">hello 'circuit owner' is an authorized Power User of hello ExpressRoute circuit resource.</span></span> <span data-ttu-id="0ccd5-143">hello 회로 소유자는 '회로 사용자'가 교환할 수 있는 권한 부여를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ccd5-143">hello circuit owner can create authorizations that can be redeemed by 'circuit users'.</span></span> <span data-ttu-id="0ccd5-144">회로 사용자 가상 네트워크의 소유자가 없는 내 게이트웨이 ExpressRoute 회로 hello으로 동일한 구독 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ccd5-144">Circuit users are owners of virtual network gateways that are not within hello same subscription as hello ExpressRoute circuit.</span></span> <span data-ttu-id="0ccd5-145">회로 사용자는 가상 네트워크당 하나의 권한 부여를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ccd5-145">Circuit users can redeem authorizations (one authorization per virtual network).</span></span>

<span data-ttu-id="0ccd5-146">hello 회로 소유자는 언제 든 지 hello 전원 toomodify 및 revoke 권한을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="0ccd5-146">hello circuit owner has hello power toomodify and revoke authorizations at any time.</span></span> <span data-ttu-id="0ccd5-147">액세스가 해지 된 hello 구독에서 삭제 되 고 모든 링크 연결에는 권한 부여 결과 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ccd5-147">Revoking an authorization results in all link connections being deleted from hello subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="0ccd5-148">회로 소유자 작업</span><span class="sxs-lookup"><span data-stu-id="0ccd5-148">Circuit owner operations</span></span>

<span data-ttu-id="0ccd5-149">**toocreate 권한 부여**</span><span class="sxs-lookup"><span data-stu-id="0ccd5-149">**toocreate an authorization**</span></span>

<span data-ttu-id="0ccd5-150">hello 회로 소유자는 권한 부여를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0ccd5-150">hello circuit owner creates an authorization.</span></span> <span data-ttu-id="0ccd5-151">이 인해 hello 생성 될 수 있는 권한 부여 키의 해당 가상 네트워크 게이트웨이 toohello ExpressRoute 회로 회로 사용자 tooconnect에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ccd5-151">This results in hello creation of an authorization key that can be used by a circuit user tooconnect their virtual network gateways toohello ExpressRoute circuit.</span></span> <span data-ttu-id="0ccd5-152">권한 부여는 하나의 연결에만 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="0ccd5-152">An authorization is valid for only one connection.</span></span>

<span data-ttu-id="0ccd5-153">hello cmdlet 조각과 방법을 따르는 toocreate 권한 부여:</span><span class="sxs-lookup"><span data-stu-id="0ccd5-153">hello following cmdlet snippet shows how toocreate an authorization:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
Add-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization1"
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit

$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$auth1 = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization1"
```


<span data-ttu-id="0ccd5-154">hello 응답 toothis hello 인증 키 및 상태에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ccd5-154">hello response toothis will contain hello authorization key and status:</span></span>

    Name                   : MyAuthorization1
    Id                     : /subscriptions/&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&/resourceGroups/ERCrossSubTestRG/providers/Microsoft.Network/expressRouteCircuits/CrossSubTest/authorizations/MyAuthorization1
    Etag                   : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&& 
    AuthorizationKey       : ####################################
    AuthorizationUseStatus : Available
    ProvisioningState      : Succeeded



<span data-ttu-id="0ccd5-155">**tooreview 권한 부여**</span><span class="sxs-lookup"><span data-stu-id="0ccd5-155">**tooreview authorizations**</span></span>

<span data-ttu-id="0ccd5-156">hello 회로 소유자는 hello 다음 cmdlet을 실행 하 여 특정 회로에 발급 한 모든 권한 부여를 검토할 수 있습니다.:</span><span class="sxs-lookup"><span data-stu-id="0ccd5-156">hello circuit owner can review all authorizations that are issued on a particular circuit by running hello following cmdlet:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$authorizations = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit
```

<span data-ttu-id="0ccd5-157">**tooadd 권한 부여**</span><span class="sxs-lookup"><span data-stu-id="0ccd5-157">**tooadd authorizations**</span></span>

<span data-ttu-id="0ccd5-158">hello 회로 소유자는 hello 다음 cmdlet을 사용 하 여 권한 부여를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ccd5-158">hello circuit owner can add authorizations by using hello following cmdlet:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
Add-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization2"
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit

$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$authorizations = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit
```

<span data-ttu-id="0ccd5-159">**toodelete 권한 부여**</span><span class="sxs-lookup"><span data-stu-id="0ccd5-159">**toodelete authorizations**</span></span>

<span data-ttu-id="0ccd5-160">hello 회로 소유자 수 revoke/삭제 권한 부여 toohello 사용자 hello 다음 cmdlet을 실행 하 여:</span><span class="sxs-lookup"><span data-stu-id="0ccd5-160">hello circuit owner can revoke/delete authorizations toohello user by running hello following cmdlet:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuitAuthorization -Name "MyAuthorization2" -ExpressRouteCircuit $circuit
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit
```    

### <a name="circuit-user-operations"></a><span data-ttu-id="0ccd5-161">회로 사용자 작업</span><span class="sxs-lookup"><span data-stu-id="0ccd5-161">Circuit user operations</span></span>

<span data-ttu-id="0ccd5-162">hello 회로 사용자는 hello 피어 ID 및 권한 부여 hello 회로 소유자 로부터 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0ccd5-162">hello circuit user needs hello peer ID and an authorization key from hello circuit owner.</span></span> <span data-ttu-id="0ccd5-163">hello 인증 키 GUID입니다.</span><span class="sxs-lookup"><span data-stu-id="0ccd5-163">hello authorization key is a GUID.</span></span>

<span data-ttu-id="0ccd5-164">다음 명령을 hello에서 피어 ID는 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ccd5-164">Peer ID can be checked from hello following command:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
```

<span data-ttu-id="0ccd5-165">**tooredeem 연결 권한 부여**</span><span class="sxs-lookup"><span data-stu-id="0ccd5-165">**tooredeem a connection authorization**</span></span>

<span data-ttu-id="0ccd5-166">hello 회로 사용자 cmdlet tooredeem 다음 hello 링크 권한 부여를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ccd5-166">hello circuit user can run hello following cmdlet tooredeem a link authorization:</span></span>

```powershell
$id = "/subscriptions/********************************/resourceGroups/ERCrossSubTestRG/providers/Microsoft.Network/expressRouteCircuits/MyCircuit"    
$gw = Get-AzureRmVirtualNetworkGateway -Name "ExpressRouteGw" -ResourceGroupName "MyRG"
$connection = New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName "RemoteResourceGroup" -Location "East US" -VirtualNetworkGateway1 $gw -PeerId $id -ConnectionType ExpressRoute -AuthorizationKey "^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^"
```

<span data-ttu-id="0ccd5-167">**toorelease 연결 권한 부여**</span><span class="sxs-lookup"><span data-stu-id="0ccd5-167">**toorelease a connection authorization**</span></span>

<span data-ttu-id="0ccd5-168">Hello ExpressRoute 회로 toohello 가상 네트워크를 연결 하는 hello 연결을 삭제 하 여 권한 부여를 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ccd5-168">You can release an authorization by deleting hello connection that links hello ExpressRoute circuit toohello virtual network.</span></span>

## <a name="modify-a-virtual-network-connection"></a><span data-ttu-id="0ccd5-169">가상 네트워크 연결 수정</span><span class="sxs-lookup"><span data-stu-id="0ccd5-169">Modify a virtual network connection</span></span>
<span data-ttu-id="0ccd5-170">가상 네트워크 연결의 특정 속성을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ccd5-170">You can update certain properties of a virtual network connection.</span></span> 

<span data-ttu-id="0ccd5-171">**tooupdate hello 연결 가중치**</span><span class="sxs-lookup"><span data-stu-id="0ccd5-171">**tooupdate hello connection weight**</span></span>

<span data-ttu-id="0ccd5-172">가상 네트워크에 연결 된 toomultiple ExpressRoute 회로 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ccd5-172">Your virtual network can be connected toomultiple ExpressRoute circuits.</span></span> <span data-ttu-id="0ccd5-173">접두사는 hello에서 하나 이상의 ExpressRoute 회로 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ccd5-173">You may receive hello same prefix from more than one ExpressRoute circuit.</span></span> <span data-ttu-id="0ccd5-174">변경할 수 있습니다이 접두사에 대 한 연결 toosend 트래픽을 보내는 toochoose, *RoutingWeight* 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ccd5-174">toochoose which connection toosend traffic destined for this prefix, you can change *RoutingWeight* of a connection.</span></span> <span data-ttu-id="0ccd5-175">가장 높은 hello로 hello 연결에서 트래픽을 보낼 *RoutingWeight*합니다.</span><span class="sxs-lookup"><span data-stu-id="0ccd5-175">Traffic will be sent on hello connection with hello highest *RoutingWeight*.</span></span>

```powershell
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name "MyVirtualNetworkConnection" -ResourceGroupName "MyRG"
$connection.RoutingWeight = 100
Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection
```

<span data-ttu-id="0ccd5-176">다양 한 hello *RoutingWeight* 0 too32000 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ccd5-176">hello range of *RoutingWeight* is 0 too32000.</span></span> <span data-ttu-id="0ccd5-177">hello 기본값은 0입니다.</span><span class="sxs-lookup"><span data-stu-id="0ccd5-177">hello default value is 0.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0ccd5-178">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0ccd5-178">Next steps</span></span>
<span data-ttu-id="0ccd5-179">ExpressRoute에 대 한 자세한 내용은 참조 hello [express 경로 FAQ](expressroute-faqs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0ccd5-179">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

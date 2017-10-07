---
title: "가상 네트워크 tooan ExpressRoute 회로 연결: CLI: Azure | Microsoft Docs"
description: "이 문서는 가상 toolink (Vnet) tooExpressRoute 회로 hello 리소스 관리자 배포 모델 및 CLI를 사용 하 여 네트워크 하는 방법의 개요를 제공 합니다."
services: expressroute
documentationcenter: na
author: cherylmc
manager: timlit
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: anzaman,cherylmc
ms.openlocfilehash: 1251f016d9b94d3fee81de1df164cb085cbe9d78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit-using-cli"></a><span data-ttu-id="f0372-103">CLI를 사용 하 여 가상 네트워크 tooan ExpressRoute 회로 연결</span><span class="sxs-lookup"><span data-stu-id="f0372-103">Connect a virtual network tooan ExpressRoute circuit using CLI</span></span>

<span data-ttu-id="f0372-104">이 문서를 사용 하면 CLI를 사용 하 여 가상 네트워크 (Vnet) tooAzure ExpressRoute 회로 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0372-104">This article helps you link virtual networks (VNets) tooAzure ExpressRoute circuits using CLI.</span></span> <span data-ttu-id="f0372-105">Azure CLI를 사용 하 여 toolink hello 리소스 관리자 배포 모델을 사용 하 여 hello 가상 네트워크를 만들 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0372-105">toolink using Azure CLI, hello virtual networks must be created using hello Resource Manager deployment model.</span></span> <span data-ttu-id="f0372-106">Hello에 있어야 하거나 수 동일한 구독 또는 다른 구독에 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0372-106">They can either be in hello same subscription, or part of another subscription.</span></span> <span data-ttu-id="f0372-107">프로그램 VNet tooan ExpressRoute 회로 다른 방법 tooconnect toouse을 원하는 경우 아티클을 hello 다음 목록에서에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0372-107">If you want toouse a different method tooconnect your VNet tooan ExpressRoute circuit, you can select an article from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f0372-108">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="f0372-108">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="f0372-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f0372-109">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="f0372-110">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f0372-110">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="f0372-111">비디오 - Azure Portal</span><span class="sxs-lookup"><span data-stu-id="f0372-111">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="f0372-112">PowerShell(클래식)</span><span class="sxs-lookup"><span data-stu-id="f0372-112">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
> 

## <a name="configuration-prerequisites"></a><span data-ttu-id="f0372-113">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="f0372-113">Configuration prerequisites</span></span>

* <span data-ttu-id="f0372-114">Hello hello CLI (명령줄 인터페이스)의 최신 버전이 있어야합니다.</span><span class="sxs-lookup"><span data-stu-id="f0372-114">You need hello latest version of hello command-line interface (CLI).</span></span> <span data-ttu-id="f0372-115">자세한 내용은 [Azure CLI 2.0 설치](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f0372-115">For more information, see [Install Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span>
* <span data-ttu-id="f0372-116">Tooreview hello 필요한 [필수 구성 요소](expressroute-prerequisites.md), [라우팅 요구 사항](expressroute-routing.md), 및 [워크플로](expressroute-workflows.md) 구성을 시작 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="f0372-116">You need tooreview hello [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="f0372-117">활성화된 Express 경로 회로가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0372-117">You must have an active ExpressRoute circuit.</span></span> 
  * <span data-ttu-id="f0372-118">너무 hello 지침에 따라[ExpressRoute 회로 만들기](howto-circuit-cli.md) 있고 hello 회로 연결 공급자가 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0372-118">Follow hello instructions too[create an ExpressRoute circuit](howto-circuit-cli.md) and have hello circuit enabled by your connectivity provider.</span></span> 
  * <span data-ttu-id="f0372-119">회로에 구성된 Azure 개인 피어링이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f0372-119">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="f0372-120">Hello 참조 [라우팅 구성](howto-routing-cli.md) 라우팅 지침에 대 한 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="f0372-120">See hello [configure routing](howto-routing-cli.md) article for routing instructions.</span></span> 
  * <span data-ttu-id="f0372-121">Azure 개인 피어이링 구성되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f0372-121">Ensure that Azure private peering is configured.</span></span> <span data-ttu-id="f0372-122">종단 간 연결을 사용 하도록 설정할 수 있도록를 hello BGP 피어 링 네트워크와 Microsoft 사이 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0372-122">hello BGP peering between your network and Microsoft must be up so that you can enable end-to-end connectivity.</span></span>
  * <span data-ttu-id="f0372-123">가상 네트워크 및 가상 네트워크 게이트웨이를 만들어서 완전히 프로비전해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0372-123">Ensure that you have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="f0372-124">너무 hello 지침에 따라[ExpressRoute에 대 한 가상 네트워크 게이트웨이 구성](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="f0372-124">Follow hello instructions too[Configure a virtual network gateway for ExpressRoute](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).</span></span> <span data-ttu-id="f0372-125">수 있는지 toouse `--gateway-type ExpressRoute`합니다.</span><span class="sxs-lookup"><span data-stu-id="f0372-125">Be sure toouse `--gateway-type ExpressRoute`.</span></span>

* <span data-ttu-id="f0372-126">Too10 가상 네트워크 tooa 표준 ExpressRoute 회로를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0372-126">You can link up too10 virtual networks tooa standard ExpressRoute circuit.</span></span> <span data-ttu-id="f0372-127">모든 가상 네트워크 hello에 있어야 합니다. 동일한 지리적 지역 표준 ExpressRoute 회로 사용 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="f0372-127">All virtual networks must be in hello same geopolitical region when using a standard ExpressRoute circuit.</span></span> 

* <span data-ttu-id="f0372-128">Hello ExpressRoute premium 추가 기능을 사용 하도록 설정 하면 hello ExpressRoute 회로의 hello 지리적 영역 외부의 가상 네트워크 연결 또는 많은 수의 가상 네트워크 tooyour ExpressRoute 회로 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0372-128">If you enable hello ExpressRoute premium add-on, you can link a virtual network outside of hello geopolitical region of hello ExpressRoute circuit, or connect a larger number of virtual networks tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="f0372-129">Hello premium 추가 기능에 대 한 자세한 내용은 참조 hello [FAQ](expressroute-faqs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f0372-129">For more information about hello premium add-on, see hello [FAQ](expressroute-faqs.md).</span></span>

## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a><span data-ttu-id="f0372-130">Hello의 가상 네트워크 연결 동일한 구독 tooa 회로</span><span class="sxs-lookup"><span data-stu-id="f0372-130">Connect a virtual network in hello same subscription tooa circuit</span></span>

<span data-ttu-id="f0372-131">Hello 예제를 사용 하 여 가상 네트워크 게이트웨이 tooan ExpressRoute 회로 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0372-131">You can connect a virtual network gateway tooan ExpressRoute circuit by using hello example.</span></span> <span data-ttu-id="f0372-132">해당 hello 가상 네트워크 게이트웨이 만들어지고 hello 명령을 실행 하기 전에 연결을 위한 준비 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0372-132">Make sure that hello virtual network gateway is created and is ready for linking before you run hello command.</span></span>

```azurecli
az network vpn-connection create --name ERConnection --resource-group ExpressRouteResourceGroup --vnet-gateway1 VNet1GW --express-route-circuit2 MyCircuit
```

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a><span data-ttu-id="f0372-133">다른 구독 tooa 회로에 가상 네트워크에 연결</span><span class="sxs-lookup"><span data-stu-id="f0372-133">Connect a virtual network in a different subscription tooa circuit</span></span>

<span data-ttu-id="f0372-134">여러 구독에서 Express 경로 회로를 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0372-134">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="f0372-135">아래 hello 그림 간단한 계통도 나와의 ExpressRoute 회로 대 한 일정 공유 works 여러 구독에서.</span><span class="sxs-lookup"><span data-stu-id="f0372-135">hello figure below shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

<span data-ttu-id="f0372-136">사용 되는 toorepresent 속하는 구독에 조직 내의 toodifferent 부서는 각각 hello 작은 구름 hello 큰 구름 안에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0372-136">Each of hello smaller clouds within hello large cloud is used toorepresent subscriptions that belong toodifferent departments within an organization.</span></span> <span data-ttu-id="f0372-137">가 자신의 구독을 사용할 수 각각 hello 부서 hello 조직 내에서 배포를 위한 서비스-있지만 공유할 수 단일 express 경로 회로 tooconnect 백 tooyour 온-프레미스 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="f0372-137">Each of hello departments within hello organization can use their own subscription for deploying their services--but they can share a single ExpressRoute circuit tooconnect back tooyour on-premises network.</span></span> <span data-ttu-id="f0372-138">단일 부서 (이 예제의: IT) hello ExpressRoute 회로 소유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0372-138">A single department (in this example: IT) can own hello ExpressRoute circuit.</span></span> <span data-ttu-id="f0372-139">Hello 조직 내에서 다른 구독 hello ExpressRoute 회로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0372-139">Other subscriptions within hello organization can use hello ExpressRoute circuit.</span></span>

> [!NOTE]
> <span data-ttu-id="f0372-140">Hello 전용 회로 대 한 연결 및 대역폭 요금은 적용된 toohello ExpressRoute 회로 소유자 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0372-140">Connectivity and bandwidth charges for hello dedicated circuit will be applied toohello ExpressRoute Circuit Owner.</span></span> <span data-ttu-id="f0372-141">Hello를 공유 하는 모든 가상 네트워크 대역폭이 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0372-141">All virtual networks share hello same bandwidth.</span></span>
> 
> 

![구독 간 연결](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)

### <a name="administration---circuit-owners-and-circuit-users"></a><span data-ttu-id="f0372-143">관리 - 회로 소유자 및 회로 사용자</span><span class="sxs-lookup"><span data-stu-id="f0372-143">Administration - Circuit Owners and Circuit Users</span></span>

<span data-ttu-id="f0372-144">' 회로 소유자 ' hello는 hello ExpressRoute 회로 리소스의 인증된 된 전원 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="f0372-144">hello 'Circuit Owner' is an authorized Power User of hello ExpressRoute circuit resource.</span></span> <span data-ttu-id="f0372-145">hello 회로 소유자는 ' 회로 사용자 '가 교환할 수 있는 권한 부여를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0372-145">hello Circuit Owner can create authorizations that can be redeemed by 'Circuit Users'.</span></span> <span data-ttu-id="f0372-146">회로 사용자 가상 네트워크의 소유자가 없는 내 게이트웨이 ExpressRoute 회로 hello으로 동일한 구독 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0372-146">Circuit Users are owners of virtual network gateways that are not within hello same subscription as hello ExpressRoute circuit.</span></span> <span data-ttu-id="f0372-147">회로 사용자는 가상 네트워크당 하나의 권한 부여를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0372-147">Circuit Users can redeem authorizations (one authorization per virtual network).</span></span>

<span data-ttu-id="f0372-148">hello 회로 소유자는 언제 든 지 hello 전원 toomodify 및 revoke 권한 부여에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0372-148">hello Circuit Owner has hello power toomodify and revoke authorizations at any time.</span></span> <span data-ttu-id="f0372-149">권한 부여를 취소 하는 경우 모든 링크 연결 액세스가 해지 된 hello 구독에서 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0372-149">When an authorization is revoked, all link connections are deleted from hello subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="f0372-150">회로 소유자 작업</span><span class="sxs-lookup"><span data-stu-id="f0372-150">Circuit Owner operations</span></span>

<span data-ttu-id="f0372-151">**toocreate 권한 부여**</span><span class="sxs-lookup"><span data-stu-id="f0372-151">**toocreate an authorization**</span></span>

<span data-ttu-id="f0372-152">hello 회로 소유자는 권한 부여 될 수 있는 인증 키를 만드는 만듭니다 해당 가상 네트워크 게이트웨이 toohello ExpressRoute 회로 회로 사용자 tooconnect에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0372-152">hello Circuit Owner creates an authorization, which creates an authorization key that can be used by a Circuit User tooconnect their virtual network gateways toohello ExpressRoute circuit.</span></span> <span data-ttu-id="f0372-153">권한 부여는 하나의 연결에만 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="f0372-153">An authorization is valid for only one connection.</span></span>

<span data-ttu-id="f0372-154">hello 방법을 예제와 다음 toocreate 권한 부여:</span><span class="sxs-lookup"><span data-stu-id="f0372-154">hello following example shows how toocreate an authorization:</span></span>

```azurecli
az network express-route auth create --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization
```

<span data-ttu-id="f0372-155">hello 응답 hello 인증 키 및 상태에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0372-155">hello response contains hello authorization key and status:</span></span>

```azurecli
"authorizationKey": "0a7f3020-541f-4b4b-844a-5fb43472e3d7",
"authorizationUseStatus": "Available",
"etag": "W/\"010353d4-8955-4984-807a-585c21a22ae0\"",
"id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/authorizations/MyAuthorization1",
"name": "MyAuthorization1",
"provisioningState": "Succeeded",
"resourceGroup": "ExpressRouteResourceGroup"
```

<span data-ttu-id="f0372-156">**tooreview 권한 부여**</span><span class="sxs-lookup"><span data-stu-id="f0372-156">**tooreview authorizations**</span></span>

<span data-ttu-id="f0372-157">hello 회로 소유자는 다음 예제는 hello를 실행 하 여 특정 회로에 발급 한 모든 권한 부여를 검토할 수 있습니다.:</span><span class="sxs-lookup"><span data-stu-id="f0372-157">hello Circuit Owner can review all authorizations that are issued on a particular circuit by running hello following example:</span></span>

```azurecli
az network express-route auth list --circuit-name MyCircuit -g ExpressRouteResourceGroup
```

<span data-ttu-id="f0372-158">**tooadd 권한 부여**</span><span class="sxs-lookup"><span data-stu-id="f0372-158">**tooadd authorizations**</span></span>

<span data-ttu-id="f0372-159">hello 회로 소유자는 다음 예제는 hello를 사용 하 여 권한 부여를 추가할 수 있습니다.:</span><span class="sxs-lookup"><span data-stu-id="f0372-159">hello Circuit Owner can add authorizations by using hello following example:</span></span>

```azurecli
az network express-route auth create --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization1
```

<span data-ttu-id="f0372-160">**toodelete 권한 부여**</span><span class="sxs-lookup"><span data-stu-id="f0372-160">**toodelete authorizations**</span></span>

<span data-ttu-id="f0372-161">회로 소유자 hello 수 revoke/삭제 권한 부여 toohello 사용자 hello 다음 예제를 실행 하 여:</span><span class="sxs-lookup"><span data-stu-id="f0372-161">hello Circuit Owner can revoke/delete authorizations toohello user by running hello following example:</span></span>

```azurecli
az network express-route auth delete --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization1
```

### <a name="circuit-user-operations"></a><span data-ttu-id="f0372-162">회로 사용자 작업</span><span class="sxs-lookup"><span data-stu-id="f0372-162">Circuit User operations</span></span>

<span data-ttu-id="f0372-163">hello 회로 사용자 hello 피어 ID 및 hello 회로 소유자에서에서 권한 부여 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f0372-163">hello Circuit User needs hello peer ID and an authorization key from hello Circuit Owner.</span></span> <span data-ttu-id="f0372-164">hello 인증 키 GUID입니다.</span><span class="sxs-lookup"><span data-stu-id="f0372-164">hello authorization key is a GUID.</span></span>

```azurecli
Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
```

<span data-ttu-id="f0372-165">**tooredeem 연결 권한 부여**</span><span class="sxs-lookup"><span data-stu-id="f0372-165">**tooredeem a connection authorization**</span></span>

<span data-ttu-id="f0372-166">hello 회로 사용자 다음 예제에서는 tooredeem hello 링크 권한 부여를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0372-166">hello Circuit User can run hello following example tooredeem a link authorization:</span></span>

```azurecli
az network vpn-connection create --name ERConnection --resource-group ExpressRouteResourceGroup --vnet-gateway1 VNet1GW --express-route-circuit2 MyCircuit --authorization-key "^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^"
```

<span data-ttu-id="f0372-167">**toorelease 연결 권한 부여**</span><span class="sxs-lookup"><span data-stu-id="f0372-167">**toorelease a connection authorization**</span></span>

<span data-ttu-id="f0372-168">Hello ExpressRoute 회로 toohello 가상 네트워크를 연결 하는 hello 연결을 삭제 하 여 권한 부여를 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0372-168">You can release an authorization by deleting hello connection that links hello ExpressRoute circuit toohello virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f0372-169">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f0372-169">Next steps</span></span>

<span data-ttu-id="f0372-170">ExpressRoute에 대 한 자세한 내용은 참조 hello [express 경로 FAQ](expressroute-faqs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f0372-170">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

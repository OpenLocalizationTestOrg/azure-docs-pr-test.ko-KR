---
title: "ExpressRoute 회로에 가상 네트워크 연결: CLI: Azure | Microsoft Docs"
description: "이 문서는 Resource Manager 배포 모델 및 CLI를 사용하여 VNet(가상 네트워크)을 ExpressRoute 회로에 연결하는 방법에 대한 개요를 제공합니다."
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
ms.openlocfilehash: 0ea696e796ec3a943bc028f56da417978b728b82
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/29/2017
---
# <a name="connect-a-virtual-network-to-an-expressroute-circuit-using-cli"></a><span data-ttu-id="cb84b-103">CLI를 사용하여 가상 네트워크를 ExpressRoute 회로에 연결</span><span class="sxs-lookup"><span data-stu-id="cb84b-103">Connect a virtual network to an ExpressRoute circuit using CLI</span></span>

<span data-ttu-id="cb84b-104">이 문서는 CLI를 사용하여 VNet(가상 네트워크)을 Azure ExpressRoute 회로에 연결하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb84b-104">This article helps you link virtual networks (VNets) to Azure ExpressRoute circuits using CLI.</span></span> <span data-ttu-id="cb84b-105">Azure CLI를 사용하여 연결하려면 Resource Manager 배포 모델을 사용하여 가상 네트워크를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb84b-105">To link using Azure CLI, the virtual networks must be created using the Resource Manager deployment model.</span></span> <span data-ttu-id="cb84b-106">해당 항목은 같은 구독에 있을 수도 있고 다른 구독의 일부일 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb84b-106">They can either be in the same subscription, or part of another subscription.</span></span> <span data-ttu-id="cb84b-107">VNet을 ExpressRoute 회로에 연결하는 다른 방법을 사용하려는 경우 다음 목록에서 문서를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb84b-107">If you want to use a different method to connect your VNet to an ExpressRoute circuit, you can select an article from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="cb84b-108">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="cb84b-108">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="cb84b-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="cb84b-109">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="cb84b-110">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="cb84b-110">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="cb84b-111">비디오 - Azure Portal</span><span class="sxs-lookup"><span data-stu-id="cb84b-111">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="cb84b-112">PowerShell(클래식)</span><span class="sxs-lookup"><span data-stu-id="cb84b-112">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
> 

## <a name="configuration-prerequisites"></a><span data-ttu-id="cb84b-113">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="cb84b-113">Configuration prerequisites</span></span>

* <span data-ttu-id="cb84b-114">최신 버전의 CLI(명령줄 인터페이스)가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="cb84b-114">You need the latest version of the command-line interface (CLI).</span></span> <span data-ttu-id="cb84b-115">자세한 내용은 [Azure CLI 2.0 설치](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cb84b-115">For more information, see [Install Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span>
* <span data-ttu-id="cb84b-116">구성을 시작하기 전에 [필수 조건](expressroute-prerequisites.md), [라우팅 요구 사항](expressroute-routing.md) 및 [워크플로](expressroute-workflows.md)를 검토해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb84b-116">You need to review the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="cb84b-117">활성화된 Express 경로 회로가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb84b-117">You must have an active ExpressRoute circuit.</span></span> 
  * <span data-ttu-id="cb84b-118">지침을 수행하여 [Express 경로 회로를 만들고](howto-circuit-cli.md) 연결 공급자를 통해 회로를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cb84b-118">Follow the instructions to [create an ExpressRoute circuit](howto-circuit-cli.md) and have the circuit enabled by your connectivity provider.</span></span> 
  * <span data-ttu-id="cb84b-119">회로에 구성된 Azure 개인 피어링이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cb84b-119">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="cb84b-120">라우팅 지침에 대한 문서는 [라우팅 구성](howto-routing-cli.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cb84b-120">See the [configure routing](howto-routing-cli.md) article for routing instructions.</span></span> 
  * <span data-ttu-id="cb84b-121">Azure 개인 피어이링 구성되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cb84b-121">Ensure that Azure private peering is configured.</span></span> <span data-ttu-id="cb84b-122">네트워크와 Microsoft 간의 BGP 피어링이 종단 간 연결을 사용하도록 작동 중이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb84b-122">The BGP peering between your network and Microsoft must be up so that you can enable end-to-end connectivity.</span></span>
  * <span data-ttu-id="cb84b-123">가상 네트워크 및 가상 네트워크 게이트웨이를 만들어서 완전히 프로비전해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb84b-123">Ensure that you have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="cb84b-124">지침에 따라 [ExpressRoute에 대한 가상 네트워크 게이트웨이를 구성합니다](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).</span><span class="sxs-lookup"><span data-stu-id="cb84b-124">Follow the instructions to [Configure a virtual network gateway for ExpressRoute](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).</span></span> <span data-ttu-id="cb84b-125">`--gateway-type ExpressRoute`를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb84b-125">Be sure to use `--gateway-type ExpressRoute`.</span></span>

* <span data-ttu-id="cb84b-126">최대 10개의 가상 네트워크를 표준 Express 경로 회로에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb84b-126">You can link up to 10 virtual networks to a standard ExpressRoute circuit.</span></span> <span data-ttu-id="cb84b-127">표준 Express 경로 회로를 사용하는 경우 모든 가상 네트워크는 동일한 지역에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb84b-127">All virtual networks must be in the same geopolitical region when using a standard ExpressRoute circuit.</span></span> 

* <span data-ttu-id="cb84b-128">ExpressRoute 프리미엄 추가 기능을 사용하도록 설정하면 ExpressRoute 회로의 지역 외부에서 가상 네트워크를 연결하거나 ExpressRoute 회로에 많은 수의 가상 네트워크를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb84b-128">If you enable the ExpressRoute premium add-on, you can link a virtual network outside of the geopolitical region of the ExpressRoute circuit, or connect a larger number of virtual networks to your ExpressRoute circuit.</span></span> <span data-ttu-id="cb84b-129">Premium 추가 기능에 대한 자세한 내용은 [FAQ](expressroute-faqs.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cb84b-129">For more information about the premium add-on, see the [FAQ](expressroute-faqs.md).</span></span>

## <a name="connect-a-virtual-network-in-the-same-subscription-to-a-circuit"></a><span data-ttu-id="cb84b-130">동일한 구독에 있는 가상 네트워크를 회로에 연결</span><span class="sxs-lookup"><span data-stu-id="cb84b-130">Connect a virtual network in the same subscription to a circuit</span></span>

<span data-ttu-id="cb84b-131">다음 예제를 사용하여 ExpressRoute 회로에 가상 네트워크 게이트웨이를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb84b-131">You can connect a virtual network gateway to an ExpressRoute circuit by using the example.</span></span> <span data-ttu-id="cb84b-132">명령을 실행하기 전에 가상 네트워크 게이트웨이가 연결을 위해 생성되고 준비되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cb84b-132">Make sure that the virtual network gateway is created and is ready for linking before you run the command.</span></span>

```azurecli
az network vpn-connection create --name ERConnection --resource-group ExpressRouteResourceGroup --vnet-gateway1 VNet1GW --express-route-circuit2 MyCircuit
```

## <a name="connect-a-virtual-network-in-a-different-subscription-to-a-circuit"></a><span data-ttu-id="cb84b-133">다른 구독에 있는 가상 네트워크를 회로에 연결</span><span class="sxs-lookup"><span data-stu-id="cb84b-133">Connect a virtual network in a different subscription to a circuit</span></span>

<span data-ttu-id="cb84b-134">여러 구독에서 Express 경로 회로를 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb84b-134">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="cb84b-135">아래 그림에는 여러 구독에서 ExpressRoute 회로에 대한 작업을 공유하는 방법의 간단한 계통도가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb84b-135">The figure below shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

<span data-ttu-id="cb84b-136">큰 구름 안에 있는 각각의 작은 구름은 한 조직 내의 여러 부서에 속하는 구독을 나타내는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb84b-136">Each of the smaller clouds within the large cloud is used to represent subscriptions that belong to different departments within an organization.</span></span> <span data-ttu-id="cb84b-137">조직 내의 각 부서는 자체 구독을 사용하여 서비스를 배포하되, 단일 Express 경로 회로를 공유하여 온-프레미스 네트워크로 다시 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb84b-137">Each of the departments within the organization can use their own subscription for deploying their services--but they can share a single ExpressRoute circuit to connect back to your on-premises network.</span></span> <span data-ttu-id="cb84b-138">단일 부서(이 예제에서는 IT)가 Express 경로 회로를 소유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb84b-138">A single department (in this example: IT) can own the ExpressRoute circuit.</span></span> <span data-ttu-id="cb84b-139">조직 내의 기타 구독도 Express 경로 회로를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb84b-139">Other subscriptions within the organization can use the ExpressRoute circuit.</span></span>

> [!NOTE]
> <span data-ttu-id="cb84b-140">전용 회로에 대한 연결 및 대역폭 요금은 ExpressRoute 회로 소유자에게 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb84b-140">Connectivity and bandwidth charges for the dedicated circuit will be applied to the ExpressRoute Circuit Owner.</span></span> <span data-ttu-id="cb84b-141">모든 가상 네트워크는 동일한 대역폭을 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="cb84b-141">All virtual networks share the same bandwidth.</span></span>
> 
> 

![구독 간 연결](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)

### <a name="administration---circuit-owners-and-circuit-users"></a><span data-ttu-id="cb84b-143">관리 - 회로 소유자 및 회로 사용자</span><span class="sxs-lookup"><span data-stu-id="cb84b-143">Administration - Circuit Owners and Circuit Users</span></span>

<span data-ttu-id="cb84b-144">'회로 소유자'는 ExpressRoute 회로 리소스의 인증된 고급 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="cb84b-144">The 'Circuit Owner' is an authorized Power User of the ExpressRoute circuit resource.</span></span> <span data-ttu-id="cb84b-145">회로 소유자는 '회로 사용자'가 사용할 수 있는 권한 부여를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb84b-145">The Circuit Owner can create authorizations that can be redeemed by 'Circuit Users'.</span></span> <span data-ttu-id="cb84b-146">회로 사용자는 ExpressRoute 회로와 동일한 구독 내에 있지 않은 가상 네트워크 게이트웨이의 소유자입니다.</span><span class="sxs-lookup"><span data-stu-id="cb84b-146">Circuit Users are owners of virtual network gateways that are not within the same subscription as the ExpressRoute circuit.</span></span> <span data-ttu-id="cb84b-147">회로 사용자는 가상 네트워크당 하나의 권한 부여를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb84b-147">Circuit Users can redeem authorizations (one authorization per virtual network).</span></span>

<span data-ttu-id="cb84b-148">회로 소유자는 언제든지 부여된 권한을 수정하고 해지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb84b-148">The Circuit Owner has the power to modify and revoke authorizations at any time.</span></span> <span data-ttu-id="cb84b-149">권한 부여를 해지하면 액세스가 해지된 구독에서 모든 링크 연결이 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb84b-149">When an authorization is revoked, all link connections are deleted from the subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="cb84b-150">회로 소유자 작업</span><span class="sxs-lookup"><span data-stu-id="cb84b-150">Circuit Owner operations</span></span>

<span data-ttu-id="cb84b-151">**권한 부여를 만들려면**</span><span class="sxs-lookup"><span data-stu-id="cb84b-151">**To create an authorization**</span></span>

<span data-ttu-id="cb84b-152">회로 소유자가 권한 부여를 만들면 ExpressRoute 회로에 해당 가상 네트워크 게이트웨이를 연결하는 회로 사용자에 의해 사용할 수 있는 권한 부여 키가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="cb84b-152">The Circuit Owner creates an authorization, which creates an authorization key that can be used by a Circuit User to connect their virtual network gateways to the ExpressRoute circuit.</span></span> <span data-ttu-id="cb84b-153">권한 부여는 하나의 연결에만 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="cb84b-153">An authorization is valid for only one connection.</span></span>

<span data-ttu-id="cb84b-154">다음 예제에서는 권한 부여를 만드는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="cb84b-154">The following example shows how to create an authorization:</span></span>

```azurecli
az network express-route auth create --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization
```

<span data-ttu-id="cb84b-155">응답에는 권한 부여 키와 상태가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb84b-155">The response contains the authorization key and status:</span></span>

```azurecli
"authorizationKey": "0a7f3020-541f-4b4b-844a-5fb43472e3d7",
"authorizationUseStatus": "Available",
"etag": "W/\"010353d4-8955-4984-807a-585c21a22ae0\"",
"id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/authorizations/MyAuthorization1",
"name": "MyAuthorization1",
"provisioningState": "Succeeded",
"resourceGroup": "ExpressRouteResourceGroup"
```

<span data-ttu-id="cb84b-156">**권한 부여를 검토하려면**</span><span class="sxs-lookup"><span data-stu-id="cb84b-156">**To review authorizations**</span></span>

<span data-ttu-id="cb84b-157">회로 소유자는 다음 예제를 실행하여 특정 회로에 발급한 모든 권한 부여를 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb84b-157">The Circuit Owner can review all authorizations that are issued on a particular circuit by running the following example:</span></span>

```azurecli
az network express-route auth list --circuit-name MyCircuit -g ExpressRouteResourceGroup
```

<span data-ttu-id="cb84b-158">**권한 부여를 추가하려면**</span><span class="sxs-lookup"><span data-stu-id="cb84b-158">**To add authorizations**</span></span>

<span data-ttu-id="cb84b-159">회로 소유자는 다음 예제를 사용하여 권한 부여를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb84b-159">The Circuit Owner can add authorizations by using the following example:</span></span>

```azurecli
az network express-route auth create --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization1
```

<span data-ttu-id="cb84b-160">**권한 부여를 삭제하려면**</span><span class="sxs-lookup"><span data-stu-id="cb84b-160">**To delete authorizations**</span></span>

<span data-ttu-id="cb84b-161">회로 소유자는 다음 예제를 실행하여 권한 부여를 취소/삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb84b-161">The Circuit Owner can revoke/delete authorizations to the user by running the following example:</span></span>

```azurecli
az network express-route auth delete --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization1
```

### <a name="circuit-user-operations"></a><span data-ttu-id="cb84b-162">회로 사용자 작업</span><span class="sxs-lookup"><span data-stu-id="cb84b-162">Circuit User operations</span></span>

<span data-ttu-id="cb84b-163">회로 사용자는 회로 소유자의 피어 ID 및 권한 부여 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="cb84b-163">The Circuit User needs the peer ID and an authorization key from the Circuit Owner.</span></span> <span data-ttu-id="cb84b-164">권한 부여 키는 GUID입니다.</span><span class="sxs-lookup"><span data-stu-id="cb84b-164">The authorization key is a GUID.</span></span>

```azurecli
Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
```

<span data-ttu-id="cb84b-165">**연결 권한 부여를 사용하려면**</span><span class="sxs-lookup"><span data-stu-id="cb84b-165">**To redeem a connection authorization**</span></span>

<span data-ttu-id="cb84b-166">회로 사용자는 다음 예제를 실행하여 링크 권한 부여를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb84b-166">The Circuit User can run the following example to redeem a link authorization:</span></span>

```azurecli
az network vpn-connection create --name ERConnection --resource-group ExpressRouteResourceGroup --vnet-gateway1 VNet1GW --express-route-circuit2 MyCircuit --authorization-key "^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^"
```

<span data-ttu-id="cb84b-167">**연결 권한 부여를 해제하려면**</span><span class="sxs-lookup"><span data-stu-id="cb84b-167">**To release a connection authorization**</span></span>

<span data-ttu-id="cb84b-168">Express 경로 회로와 가상 네트워크의 연결을 삭제하여 권한 부여를 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb84b-168">You can release an authorization by deleting the connection that links the ExpressRoute circuit to the virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cb84b-169">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cb84b-169">Next steps</span></span>

<span data-ttu-id="cb84b-170">ExpressRoute에 대한 자세한 내용은 [ExpressRoute FAQ](expressroute-faqs.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cb84b-170">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
---
title: "ExpressRoute 회로에 가상 네트워크 연결: Azure Portal | Microsoft Docs"
description: "이 문서는 가상 네트워크(VNets)를 Express 경로 회로에 연결하는 방법에 대한 개요를 제공합니다."
services: expressroute
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f5cb5441-2fba-46d9-99a5-d1d586e7bda4
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: cherylmc
ms.openlocfilehash: 595c30ab5d9adc6061ad753d952adf894ba80b2f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="connect-a-virtual-network-to-an-expressroute-circuit"></a><span data-ttu-id="0c1da-103">Virtual Network를 ExpressRoute 회로에 연결</span><span class="sxs-lookup"><span data-stu-id="0c1da-103">Connect a virtual network to an ExpressRoute circuit</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0c1da-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="0c1da-104">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="0c1da-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0c1da-105">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="0c1da-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="0c1da-106">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="0c1da-107">비디오 - Azure Portal</span><span class="sxs-lookup"><span data-stu-id="0c1da-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="0c1da-108">PowerShell(클래식)</span><span class="sxs-lookup"><span data-stu-id="0c1da-108">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
> 

<span data-ttu-id="0c1da-109">이 문서를 참조하면 리소스 관리자 배포 모델 및 Azure Portal을 사용하여 VNet(가상 네트워크)을 Azure ExpressRoute 회로에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c1da-109">This article helps you link virtual networks (VNets) to Azure ExpressRoute circuits by using the Resource Manager deployment model and the Azure portal.</span></span> <span data-ttu-id="0c1da-110">가상 네트워크는 같은 구독에 있을 수도 있고 다른 구독의 일부일 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c1da-110">Virtual networks can either be in the same subscription, or they can be part of another subscription.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="0c1da-111">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="0c1da-111">Before you begin</span></span>
* <span data-ttu-id="0c1da-112">구성을 시작하기 전에 [필수 조건](expressroute-prerequisites.md), [라우팅 요구 사항](expressroute-routing.md) 및 [워크플로](expressroute-workflows.md)를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="0c1da-112">Review the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="0c1da-113">활성화된 Express 경로 회로가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c1da-113">You must have an active ExpressRoute circuit.</span></span>
  
  * <span data-ttu-id="0c1da-114">지침을 수행하여 [Express 경로 회로를 만들고](expressroute-howto-circuit-portal-resource-manager.md) 연결 공급자를 통해 회로를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0c1da-114">Follow the instructions to [create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have the circuit enabled by your connectivity provider.</span></span>
  * <span data-ttu-id="0c1da-115">회로에 구성된 Azure 개인 피어링이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0c1da-115">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="0c1da-116">라우팅 지침에 대한 문서는 [라우팅 구성](expressroute-howto-routing-portal-resource-manager.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0c1da-116">See the [Configure routing](expressroute-howto-routing-portal-resource-manager.md) article for routing instructions.</span></span>
  * <span data-ttu-id="0c1da-117">Azure 개인 피어링이 구성되어 있고 네트워크와 Microsoft 간의 BGP 피어링이 종단 간 연결을 사용하도록 작동 중이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c1da-117">Ensure that Azure private peering is configured and the BGP peering between your network and Microsoft is up so that you can enable end-to-end connectivity.</span></span>
  * <span data-ttu-id="0c1da-118">가상 네트워크 및 가상 네트워크 게이트웨이를 만들어서 완전히 프로비전해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c1da-118">Ensure that you have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="0c1da-119">지침에 따라 [ExpressRoute에 대한 가상 네트워크 게이트웨이를 만듭니다](expressroute-howto-add-gateway-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="0c1da-119">Follow the instructions to [create a virtual network gateway for ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span></span> <span data-ttu-id="0c1da-120">ExpressRoute의 가상 네트워크 게이트웨이는 GatewayType으로 VPN이 아닌 'ExpressRoute'를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0c1da-120">A virtual network gateway for ExpressRoute uses the GatewayType 'ExpressRoute', not VPN.</span></span>

* <span data-ttu-id="0c1da-121">최대 10개의 가상 네트워크를 표준 Express 경로 회로에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c1da-121">You can link up to 10 virtual networks to a standard ExpressRoute circuit.</span></span> <span data-ttu-id="0c1da-122">표준 Express 경로 회로를 사용하는 경우 모든 가상 네트워크는 동일한 지역에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c1da-122">All virtual networks must be in the same geopolitical region when using a standard ExpressRoute circuit.</span></span> 
* <span data-ttu-id="0c1da-123">ExpressRoute 프리미엄 추가 기능을 사용하도록 설정하면 ExpressRoute 회로의 지역 외부에서 가상 네트워크를 연결하거나 ExpressRoute 회로에 많은 수의 가상 네트워크를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c1da-123">You can link a virtual network outside of the geopolitical region of the ExpressRoute circuit, or connect a larger number of virtual networks to your ExpressRoute circuit if you enabled the ExpressRoute premium add-on.</span></span> <span data-ttu-id="0c1da-124">프리미엄 추가 기능에 대한 자세한 내용은 [FAQ](expressroute-faqs.md) 에서 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="0c1da-124">Check the [FAQ](expressroute-faqs.md) for more details on the premium add-on.</span></span>
* <span data-ttu-id="0c1da-125">시작 전에 [비디오 보기](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)로 단계를 더 잘 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c1da-125">You can [view a video](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit) before beginning to better understand the steps.</span></span>

## <a name="connect-a-virtual-network-in-the-same-subscription-to-a-circuit"></a><span data-ttu-id="0c1da-126">동일한 구독에 있는 가상 네트워크를 회로에 연결</span><span class="sxs-lookup"><span data-stu-id="0c1da-126">Connect a virtual network in the same subscription to a circuit</span></span>

### <a name="to-create-a-connection"></a><span data-ttu-id="0c1da-127">연결을 만들려면</span><span class="sxs-lookup"><span data-stu-id="0c1da-127">To create a connection</span></span>

> [!NOTE]
> <span data-ttu-id="0c1da-128">3계층 공급자가 피어링을 구성한 경우 BGP 구성 정보가 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0c1da-128">BGP configuration information will not show up if the layer 3 provider configured your peerings.</span></span> <span data-ttu-id="0c1da-129">회로가 프로비전된 상태인 경우 연결을 만들 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c1da-129">If your circuit is in a provisioned state, you should be able to create connections.</span></span>
>

1. <span data-ttu-id="0c1da-130">Express 경로 회로 및 Azure 개인 피어링이 성공적으로 구성되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0c1da-130">Ensure that your ExpressRoute circuit and Azure private peering have been configured successfully.</span></span> <span data-ttu-id="0c1da-131">[ExpressRoute 회로 만들기](expressroute-howto-circuit-arm.md) 및 [라우팅 구성](expressroute-howto-routing-arm.md)의 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="0c1da-131">Follow the instructions in [Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and [Configure routing](expressroute-howto-routing-arm.md).</span></span> <span data-ttu-id="0c1da-132">ExpressRoute 회로가 다음 이미지와 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c1da-132">Your ExpressRoute circuit should look like the following image:</span></span>

    ![Express 경로 회로 스크린샷](./media/expressroute-howto-linkvnet-portal-resource-manager/routing1.png)
   
2. <span data-ttu-id="0c1da-134">이제 연결 프로비전을 시작하여 가상 네트워크 게이트웨이를 Express 경로 회로에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c1da-134">You can now start provisioning a connection to link your virtual network gateway to your ExpressRoute circuit.</span></span> <span data-ttu-id="0c1da-135">**연결** > **추가**를 클릭하여 **연결 추가** 블레이드를 연 다음 값을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="0c1da-135">Click **Connection** > **Add** to open the **Add connection** blade, and then configure the values.</span></span>

    ![연결 추가 스크린샷](./media/expressroute-howto-linkvnet-portal-resource-manager/samesub1.png)  

3. <span data-ttu-id="0c1da-137">연결이 성공적으로 구성되면 연결 개체가 연결에 대한 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="0c1da-137">After your connection has been successfully configured, your connection object will show the information for the connection.</span></span>

     ![연결 개체 스크린샷](./media/expressroute-howto-linkvnet-portal-resource-manager/samesub2.png)

### <a name="to-delete-a-connection"></a><span data-ttu-id="0c1da-139">연결을 삭제하려면</span><span class="sxs-lookup"><span data-stu-id="0c1da-139">To delete a connection</span></span>
<span data-ttu-id="0c1da-140">연결에 대한 블레이드에서 **삭제** 아이콘을 선택하여 연결을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c1da-140">You can delete a connection by selecting the **Delete** icon on the blade for your connection.</span></span>

## <a name="connect-a-virtual-network-in-a-different-subscription-to-a-circuit"></a><span data-ttu-id="0c1da-141">다른 구독에 있는 가상 네트워크를 회로에 연결</span><span class="sxs-lookup"><span data-stu-id="0c1da-141">Connect a virtual network in a different subscription to a circuit</span></span>
<span data-ttu-id="0c1da-142">여러 구독에서 Express 경로 회로를 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c1da-142">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="0c1da-143">아래 그림에는 여러 구독에서 ExpressRoute 회로에 대한 작업을 공유하는 방법의 간단한 계통도가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c1da-143">The figure below shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

![구독 간 연결](./media/expressroute-howto-linkvnet-portal-resource-manager/cross-subscription.png)

- <span data-ttu-id="0c1da-145">큰 구름 안에 있는 각각의 작은 구름은 한 조직 내의 여러 부서에 속하는 구독을 나타내는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c1da-145">Each of the smaller clouds within the large cloud is used to represent subscriptions that belong to different departments within an organization.</span></span>
- <span data-ttu-id="0c1da-146">조직 내의 각 부서는 자체 구독을 사용하여 서비스를 배포하되, 단일 ExpressRoute 회로를 공유하여 온-프레미스 네트워크로 다시 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c1da-146">Each of the departments within the organization can use their own subscription for deploying their services, but they can share a single ExpressRoute circuit to connect back to your on-premises network.</span></span>
- <span data-ttu-id="0c1da-147">단일 부서(이 예제에서는 IT)가 Express 경로 회로를 소유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c1da-147">A single department (in this example: IT) can own the ExpressRoute circuit.</span></span> <span data-ttu-id="0c1da-148">조직 내의 기타 구독도 Express 경로 회로를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c1da-148">Other subscriptions within the organization can use the ExpressRoute circuit.</span></span>

    > [!NOTE]
    > <span data-ttu-id="0c1da-149">전용 회로에 대한 연결 및 대역폭 요금은 Express 경로 회로 소유자에게 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c1da-149">Connectivity and bandwidth charges for the dedicated circuit will be applied to the ExpressRoute circuit owner.</span></span> <span data-ttu-id="0c1da-150">모든 가상 네트워크는 동일한 대역폭을 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="0c1da-150">All virtual networks share the same bandwidth.</span></span>
    > 
    >

### <a name="administration---circuit-owners-and-circuit-users"></a><span data-ttu-id="0c1da-151">관리 - 회로 소유자 및 회로 사용자</span><span class="sxs-lookup"><span data-stu-id="0c1da-151">Administration - circuit owners and circuit users</span></span>

<span data-ttu-id="0c1da-152">’회로 소유자’는 ExpressRoute 회로 리소스의 인증된 고급 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="0c1da-152">The 'circuit owner' is an authorized Power User of the ExpressRoute circuit resource.</span></span> <span data-ttu-id="0c1da-153">회로 소유자는 '회로 사용자'가 사용할 수 있는 권한 부여를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c1da-153">The circuit owner can create authorizations that can be redeemed by 'circuit users'.</span></span> <span data-ttu-id="0c1da-154">회로 사용자는 ExpressRoute 회로와 동일한 구독 내에 있지 않은 가상 네트워크 게이트웨이의 소유자입니다.</span><span class="sxs-lookup"><span data-stu-id="0c1da-154">Circuit users are owners of virtual network gateways that are not within the same subscription as the ExpressRoute circuit.</span></span> <span data-ttu-id="0c1da-155">회로 사용자는 가상 네트워크당 하나의 권한 부여를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c1da-155">Circuit users can redeem authorizations (one authorization per virtual network).</span></span>

<span data-ttu-id="0c1da-156">회로 소유자는 언제든지 부여된 권한을 수정하고 해지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c1da-156">The circuit owner has the power to modify and revoke authorizations at any time.</span></span> <span data-ttu-id="0c1da-157">권한 부여를 해지하면 액세스가 해지된 구독에서 모든 링크 연결이 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c1da-157">Revoking an authorization results in all link connections being deleted from the subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="0c1da-158">회로 소유자 작업</span><span class="sxs-lookup"><span data-stu-id="0c1da-158">Circuit owner operations</span></span>

<span data-ttu-id="0c1da-159">**연결 권한 부여를 만들려면**</span><span class="sxs-lookup"><span data-stu-id="0c1da-159">**To create a connection authorization**</span></span>

<span data-ttu-id="0c1da-160">회로 소유자가 권한 부여를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0c1da-160">The circuit owner creates an authorization.</span></span> <span data-ttu-id="0c1da-161">그러면 회로 사용자가 Express 경로 회로에 가상 네트워크 게이트웨이를 연결하는 데 사용할 수 있는 권한 부여 키가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="0c1da-161">This results in the creation of an authorization key that can be used by a circuit user to connect their virtual network gateways to the ExpressRoute circuit.</span></span> <span data-ttu-id="0c1da-162">권한 부여는 하나의 연결에만 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="0c1da-162">An authorization is valid for only one connection.</span></span>

1. <span data-ttu-id="0c1da-163">ExpressRoute 블레이드에서 **권한 부여**를 클릭하고 권한 부여에 대한 **이름**을 입력한 후 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0c1da-163">In the ExpressRoute blade, Click **Authorizations** and then type a **name** for the authorization and click **Save**.</span></span>

    ![권한 부여](./media/expressroute-howto-linkvnet-portal-resource-manager/authorization.png)

2. <span data-ttu-id="0c1da-165">구성이 저장되면 **리소스 ID** 및 **권한 부여 키**를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="0c1da-165">Once the configuration is saved, copy the **Resource ID** and the **Authorization Key**.</span></span>

    ![인증 키](./media/expressroute-howto-linkvnet-portal-resource-manager/authkey.png)

<span data-ttu-id="0c1da-167">**연결 권한 부여를 삭제하려면**</span><span class="sxs-lookup"><span data-stu-id="0c1da-167">**To delete a connection authorization**</span></span>

<span data-ttu-id="0c1da-168">연결에 대한 블레이드에서 **삭제** 아이콘을 선택하여 연결을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c1da-168">You can delete a connection by selecting the **Delete** icon on the blade for your connection.</span></span>

### <a name="circuit-user-operations"></a><span data-ttu-id="0c1da-169">회로 사용자 작업</span><span class="sxs-lookup"><span data-stu-id="0c1da-169">Circuit user operations</span></span>

<span data-ttu-id="0c1da-170">회로 사용자는 회로 소유자로부터 권한 부여 키를 받아야 하며 리소스 ID가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0c1da-170">The circuit user needs the resource ID and an authorization key from the circuit owner.</span></span> 

<span data-ttu-id="0c1da-171">**연결 권한 부여를 사용하려면**</span><span class="sxs-lookup"><span data-stu-id="0c1da-171">**To redeem a connection authorization**</span></span>

1.  <span data-ttu-id="0c1da-172">**+새로 만들기** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0c1da-172">Click the **+New** button.</span></span>

    ![새로 만들기 클릭](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection1.png)

2.  <span data-ttu-id="0c1da-174">Marketplace에서 **“연결”**을 검색하고 선택한 후 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0c1da-174">Search for **"Connection"** in the Marketplace, select it, and click **Create**.</span></span>

    ![연결 검색](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection2.png)

3.  <span data-ttu-id="0c1da-176">**연결 유형**이 "ExpressRoute"로 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0c1da-176">Make sure the **Connection type** is set to "ExpressRoute".</span></span>


4.  <span data-ttu-id="0c1da-177">세부 정보를 입력하고 기본 사항 블레이드에서 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0c1da-177">Fill in the details, then click **OK** in the Basics blade.</span></span>

    ![기본 사항 블레이드](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection3.png)

5.  <span data-ttu-id="0c1da-179">**설정** 블레이드에서 **가상 네트워크 게이트웨이**를 선택하고 **권한 부여 상환** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0c1da-179">In the **Settings** blade, Select the **Virtual network gateway** and check the **Redeem authorization** check box.</span></span>

6.  <span data-ttu-id="0c1da-180">**권한 부여 키** 및 **피어 회로 URI**를 입력한 후 연결 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0c1da-180">Enter the **Authorization key** and the **Peer circuit URI** and give the connection a name.</span></span> <span data-ttu-id="0c1da-181">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0c1da-181">Click **OK**.</span></span>

    ![설정 블레이드](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection4.png)

7. <span data-ttu-id="0c1da-183">**요약** 블레이드에서 정보를 검토하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0c1da-183">Review the information in the **Summary** blade and click **OK**.</span></span>


<span data-ttu-id="0c1da-184">**연결 권한 부여를 해제하려면**</span><span class="sxs-lookup"><span data-stu-id="0c1da-184">**To release a connection authorization**</span></span>

<span data-ttu-id="0c1da-185">Express 경로 회로와 가상 네트워크의 연결을 삭제하여 권한 부여를 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c1da-185">You can release an authorization by deleting the connection that links the ExpressRoute circuit to the virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0c1da-186">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0c1da-186">Next steps</span></span>
<span data-ttu-id="0c1da-187">ExpressRoute에 대한 자세한 내용은 [ExpressRoute FAQ](expressroute-faqs.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0c1da-187">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

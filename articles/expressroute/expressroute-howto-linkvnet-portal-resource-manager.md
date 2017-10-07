---
title: "가상 네트워크 tooan ExpressRoute 회로 연결: Azure 포털 | Microsoft Docs"
description: "이 문서는 어떻게 toolink 가상 네트워크 (Vnet) tooExpressRoute 회로의 개요를 제공 합니다."
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
ms.openlocfilehash: 8bedcb11df7e30281fd439afdfb76cc67626a8f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit"></a><span data-ttu-id="665e8-103">가상 네트워크 tooan ExpressRoute 회로 연결</span><span class="sxs-lookup"><span data-stu-id="665e8-103">Connect a virtual network tooan ExpressRoute circuit</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="665e8-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="665e8-104">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="665e8-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="665e8-105">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="665e8-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="665e8-106">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="665e8-107">비디오 - Azure Portal</span><span class="sxs-lookup"><span data-stu-id="665e8-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="665e8-108">PowerShell(클래식)</span><span class="sxs-lookup"><span data-stu-id="665e8-108">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
> 

<span data-ttu-id="665e8-109">이 문서를 사용 하면 hello 리소스 관리자 배포 모델을 사용 하 여 가상 네트워크 (Vnet) tooAzure ExpressRoute 회로 연결 하 고 Azure 포털 hello 있습니다.</span><span class="sxs-lookup"><span data-stu-id="665e8-109">This article helps you link virtual networks (VNets) tooAzure ExpressRoute circuits by using hello Resource Manager deployment model and hello Azure portal.</span></span> <span data-ttu-id="665e8-110">가상 네트워크 수 hello에 동일한 구독 또는 있습니다 수의 일부가 될 다른 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="665e8-110">Virtual networks can either be in hello same subscription, or they can be part of another subscription.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="665e8-111">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="665e8-111">Before you begin</span></span>
* <span data-ttu-id="665e8-112">검토 hello [필수 구성 요소](expressroute-prerequisites.md), [라우팅 요구 사항](expressroute-routing.md), 및 [워크플로](expressroute-workflows.md) 구성을 시작 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="665e8-112">Review hello [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="665e8-113">활성화된 Express 경로 회로가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="665e8-113">You must have an active ExpressRoute circuit.</span></span>
  
  * <span data-ttu-id="665e8-114">너무 hello 지침에 따라[ExpressRoute 회로 만들기](expressroute-howto-circuit-portal-resource-manager.md) 있고 hello 회로 연결 공급자가 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="665e8-114">Follow hello instructions too[create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have hello circuit enabled by your connectivity provider.</span></span>
  * <span data-ttu-id="665e8-115">회로에 구성된 Azure 개인 피어링이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="665e8-115">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="665e8-116">Hello 참조 [구성 라우팅](expressroute-howto-routing-portal-resource-manager.md) 라우팅 지침에 대 한 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="665e8-116">See hello [Configure routing](expressroute-howto-routing-portal-resource-manager.md) article for routing instructions.</span></span>
  * <span data-ttu-id="665e8-117">구성 된 Azure 개인 피어 링 및 종단 간 연결을 사용 하도록 설정할 수 있도록 중일 hello 네트워크와 Microsoft 간에 BGP 피어 링을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="665e8-117">Ensure that Azure private peering is configured and hello BGP peering between your network and Microsoft is up so that you can enable end-to-end connectivity.</span></span>
  * <span data-ttu-id="665e8-118">가상 네트워크 및 가상 네트워크 게이트웨이를 만들어서 완전히 프로비전해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="665e8-118">Ensure that you have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="665e8-119">너무 hello 지침에 따라[ExpressRoute에 대 한 가상 네트워크 게이트웨이 만들](expressroute-howto-add-gateway-resource-manager.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="665e8-119">Follow hello instructions too[create a virtual network gateway for ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span></span> <span data-ttu-id="665e8-120">ExpressRoute에 대 한 가상 네트워크 게이트웨이 hello GatewayType 'ExpressRoute' 하지 VPN을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="665e8-120">A virtual network gateway for ExpressRoute uses hello GatewayType 'ExpressRoute', not VPN.</span></span>

* <span data-ttu-id="665e8-121">Too10 가상 네트워크 tooa 표준 ExpressRoute 회로를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="665e8-121">You can link up too10 virtual networks tooa standard ExpressRoute circuit.</span></span> <span data-ttu-id="665e8-122">모든 가상 네트워크 hello에 있어야 합니다. 동일한 지리적 지역 표준 ExpressRoute 회로 사용 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="665e8-122">All virtual networks must be in hello same geopolitical region when using a standard ExpressRoute circuit.</span></span> 
* <span data-ttu-id="665e8-123">Hello ExpressRoute 회로의 hello 지리적 영역 외부의 가상 네트워크 연결 또는 hello ExpressRoute premium 추가 기능을 사용 하는 경우 많은 수의 가상 네트워크 tooyour ExpressRoute 회로 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="665e8-123">You can link a virtual network outside of hello geopolitical region of hello ExpressRoute circuit, or connect a larger number of virtual networks tooyour ExpressRoute circuit if you enabled hello ExpressRoute premium add-on.</span></span> <span data-ttu-id="665e8-124">Hello 확인 [FAQ](expressroute-faqs.md) hello premium 추가 기능에 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="665e8-124">Check hello [FAQ](expressroute-faqs.md) for more details on hello premium add-on.</span></span>
* <span data-ttu-id="665e8-125">할 수 있습니다 [비디오를 보려면](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit) 전에 시작 toobetter hello 단계를 파악 합니다.</span><span class="sxs-lookup"><span data-stu-id="665e8-125">You can [view a video](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit) before beginning toobetter understand hello steps.</span></span>

## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a><span data-ttu-id="665e8-126">Hello의 가상 네트워크 연결 동일한 구독 tooa 회로</span><span class="sxs-lookup"><span data-stu-id="665e8-126">Connect a virtual network in hello same subscription tooa circuit</span></span>

### <a name="toocreate-a-connection"></a><span data-ttu-id="665e8-127">toocreate 연결</span><span class="sxs-lookup"><span data-stu-id="665e8-127">toocreate a connection</span></span>

> [!NOTE]
> <span data-ttu-id="665e8-128">BGP 구성 정보는 표시 되지 hello 계층 3 공급자에 피어 링을 구성 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="665e8-128">BGP configuration information will not show up if hello layer 3 provider configured your peerings.</span></span> <span data-ttu-id="665e8-129">회로 프로 비전 된 상태에 있으면 수 toocreate 연결 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="665e8-129">If your circuit is in a provisioned state, you should be able toocreate connections.</span></span>
>

1. <span data-ttu-id="665e8-130">Express 경로 회로 및 Azure 개인 피어링이 성공적으로 구성되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="665e8-130">Ensure that your ExpressRoute circuit and Azure private peering have been configured successfully.</span></span> <span data-ttu-id="665e8-131">Hello 지침에 따라 [ExpressRoute 회로 만들기](expressroute-howto-circuit-arm.md) 및 [구성 라우팅](expressroute-howto-routing-arm.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="665e8-131">Follow hello instructions in [Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and [Configure routing](expressroute-howto-routing-arm.md).</span></span> <span data-ttu-id="665e8-132">ExpressRoute 회로 hello 다음 이미지와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="665e8-132">Your ExpressRoute circuit should look like hello following image:</span></span>

    ![Express 경로 회로 스크린샷](./media/expressroute-howto-linkvnet-portal-resource-manager/routing1.png)
   
2. <span data-ttu-id="665e8-134">이제 연결 toolink 가상 네트워크 게이트웨이 tooyour ExpressRoute 회로 프로 비전을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="665e8-134">You can now start provisioning a connection toolink your virtual network gateway tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="665e8-135">클릭 **연결** > **추가** tooopen hello **연결 추가** 블레이드에서 hello 값을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="665e8-135">Click **Connection** > **Add** tooopen hello **Add connection** blade, and then configure hello values.</span></span>

    ![연결 추가 스크린샷](./media/expressroute-howto-linkvnet-portal-resource-manager/samesub1.png)  

3. <span data-ttu-id="665e8-137">연결이 성공적으로 구성 된 후 연결 개체에는 hello 연결에 대 한 hello 정보가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="665e8-137">After your connection has been successfully configured, your connection object will show hello information for hello connection.</span></span>

     ![연결 개체 스크린샷](./media/expressroute-howto-linkvnet-portal-resource-manager/samesub2.png)

### <a name="toodelete-a-connection"></a><span data-ttu-id="665e8-139">toodelete 연결</span><span class="sxs-lookup"><span data-stu-id="665e8-139">toodelete a connection</span></span>
<span data-ttu-id="665e8-140">Hello를 선택 하 여 연결을 삭제할 수 **삭제** 연결에 대 한 hello 블레이드에서 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="665e8-140">You can delete a connection by selecting hello **Delete** icon on hello blade for your connection.</span></span>

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a><span data-ttu-id="665e8-141">다른 구독 tooa 회로에 가상 네트워크에 연결</span><span class="sxs-lookup"><span data-stu-id="665e8-141">Connect a virtual network in a different subscription tooa circuit</span></span>
<span data-ttu-id="665e8-142">여러 구독에서 Express 경로 회로를 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="665e8-142">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="665e8-143">아래 hello 그림 간단한 계통도 나와의 ExpressRoute 회로 대 한 일정 공유 works 여러 구독에서.</span><span class="sxs-lookup"><span data-stu-id="665e8-143">hello figure below shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

![구독 간 연결](./media/expressroute-howto-linkvnet-portal-resource-manager/cross-subscription.png)

- <span data-ttu-id="665e8-145">사용 되는 toorepresent 속하는 구독에 조직 내의 toodifferent 부서는 각각 hello 작은 구름 hello 큰 구름 안에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="665e8-145">Each of hello smaller clouds within hello large cloud is used toorepresent subscriptions that belong toodifferent departments within an organization.</span></span>
- <span data-ttu-id="665e8-146">해당 서비스를 배포 각각 hello 부서 hello 조직 내에서 자체 구독 사용할 수 있지만 단일 express 경로 회로 tooconnect 백 tooyour 온-프레미스 네트워크를 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="665e8-146">Each of hello departments within hello organization can use their own subscription for deploying their services, but they can share a single ExpressRoute circuit tooconnect back tooyour on-premises network.</span></span>
- <span data-ttu-id="665e8-147">단일 부서 (이 예제의: IT) hello ExpressRoute 회로 소유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="665e8-147">A single department (in this example: IT) can own hello ExpressRoute circuit.</span></span> <span data-ttu-id="665e8-148">Hello 조직 내에서 다른 구독 hello ExpressRoute 회로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="665e8-148">Other subscriptions within hello organization can use hello ExpressRoute circuit.</span></span>

    > [!NOTE]
    > <span data-ttu-id="665e8-149">Hello 전용 회로 대 한 연결 및 대역폭 요금은 적용된 toohello ExpressRoute 회로 소유자 됩니다.</span><span class="sxs-lookup"><span data-stu-id="665e8-149">Connectivity and bandwidth charges for hello dedicated circuit will be applied toohello ExpressRoute circuit owner.</span></span> <span data-ttu-id="665e8-150">Hello를 공유 하는 모든 가상 네트워크 대역폭이 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="665e8-150">All virtual networks share hello same bandwidth.</span></span>
    > 
    >

### <a name="administration---circuit-owners-and-circuit-users"></a><span data-ttu-id="665e8-151">관리 - 회로 소유자 및 회로 사용자</span><span class="sxs-lookup"><span data-stu-id="665e8-151">Administration - circuit owners and circuit users</span></span>

<span data-ttu-id="665e8-152">'회로 소유자' hello는 hello ExpressRoute 회로 리소스의 인증된 된 전원 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="665e8-152">hello 'circuit owner' is an authorized Power User of hello ExpressRoute circuit resource.</span></span> <span data-ttu-id="665e8-153">hello 회로 소유자는 '회로 사용자'가 교환할 수 있는 권한 부여를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="665e8-153">hello circuit owner can create authorizations that can be redeemed by 'circuit users'.</span></span> <span data-ttu-id="665e8-154">회로 사용자 가상 네트워크의 소유자가 없는 내 게이트웨이 ExpressRoute 회로 hello으로 동일한 구독 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="665e8-154">Circuit users are owners of virtual network gateways that are not within hello same subscription as hello ExpressRoute circuit.</span></span> <span data-ttu-id="665e8-155">회로 사용자는 가상 네트워크당 하나의 권한 부여를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="665e8-155">Circuit users can redeem authorizations (one authorization per virtual network).</span></span>

<span data-ttu-id="665e8-156">hello 회로 소유자는 언제 든 지 hello 전원 toomodify 및 revoke 권한을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="665e8-156">hello circuit owner has hello power toomodify and revoke authorizations at any time.</span></span> <span data-ttu-id="665e8-157">액세스가 해지 된 hello 구독에서 삭제 되 고 모든 링크 연결에는 권한 부여 결과 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="665e8-157">Revoking an authorization results in all link connections being deleted from hello subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="665e8-158">회로 소유자 작업</span><span class="sxs-lookup"><span data-stu-id="665e8-158">Circuit owner operations</span></span>

<span data-ttu-id="665e8-159">**toocreate 연결 권한 부여**</span><span class="sxs-lookup"><span data-stu-id="665e8-159">**toocreate a connection authorization**</span></span>

<span data-ttu-id="665e8-160">hello 회로 소유자는 권한 부여를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="665e8-160">hello circuit owner creates an authorization.</span></span> <span data-ttu-id="665e8-161">이 인해 hello 생성 될 수 있는 권한 부여 키의 해당 가상 네트워크 게이트웨이 toohello ExpressRoute 회로 회로 사용자 tooconnect에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="665e8-161">This results in hello creation of an authorization key that can be used by a circuit user tooconnect their virtual network gateways toohello ExpressRoute circuit.</span></span> <span data-ttu-id="665e8-162">권한 부여는 하나의 연결에만 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="665e8-162">An authorization is valid for only one connection.</span></span>

1. <span data-ttu-id="665e8-163">Hello ExpressRoute 블레이드에서 클릭 **권한 부여** 한 다음를 입력 한 **이름** hello 권한 부여 및 클릭에 대 한 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="665e8-163">In hello ExpressRoute blade, Click **Authorizations** and then type a **name** for hello authorization and click **Save**.</span></span>

    ![권한 부여](./media/expressroute-howto-linkvnet-portal-resource-manager/authorization.png)

2. <span data-ttu-id="665e8-165">Hello 구성이 저장 되 고 나면 복사 hello **리소스 ID** 및 hello **인증 키**합니다.</span><span class="sxs-lookup"><span data-stu-id="665e8-165">Once hello configuration is saved, copy hello **Resource ID** and hello **Authorization Key**.</span></span>

    ![인증 키](./media/expressroute-howto-linkvnet-portal-resource-manager/authkey.png)

<span data-ttu-id="665e8-167">**toodelete 연결 권한 부여**</span><span class="sxs-lookup"><span data-stu-id="665e8-167">**toodelete a connection authorization**</span></span>

<span data-ttu-id="665e8-168">Hello를 선택 하 여 연결을 삭제할 수 **삭제** 연결에 대 한 hello 블레이드에서 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="665e8-168">You can delete a connection by selecting hello **Delete** icon on hello blade for your connection.</span></span>

### <a name="circuit-user-operations"></a><span data-ttu-id="665e8-169">회로 사용자 작업</span><span class="sxs-lookup"><span data-stu-id="665e8-169">Circuit user operations</span></span>

<span data-ttu-id="665e8-170">hello 회로 사용자는 hello 리소스 ID 및 권한 부여 키 hello 회로 소유자 로부터 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="665e8-170">hello circuit user needs hello resource ID and an authorization key from hello circuit owner.</span></span> 

<span data-ttu-id="665e8-171">**tooredeem 연결 권한 부여**</span><span class="sxs-lookup"><span data-stu-id="665e8-171">**tooredeem a connection authorization**</span></span>

1.  <span data-ttu-id="665e8-172">Hello 클릭 **+ 새로 만들기** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="665e8-172">Click hello **+New** button.</span></span>

    ![새로 만들기 클릭](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection1.png)

2.  <span data-ttu-id="665e8-174">검색할 **"연결"** 마켓플레이스 hello에서 선택 하 고 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="665e8-174">Search for **"Connection"** in hello Marketplace, select it, and click **Create**.</span></span>

    ![연결 검색](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection2.png)

3.  <span data-ttu-id="665e8-176">있는지 hello 확인 **연결 유형** 너무 설정 된 "express 경로"입니다.</span><span class="sxs-lookup"><span data-stu-id="665e8-176">Make sure hello **Connection type** is set too"ExpressRoute".</span></span>


4.  <span data-ttu-id="665e8-177">Hello 세부 정보를 입력 한 다음 클릭 **확인** hello 기본 사항 블레이드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="665e8-177">Fill in hello details, then click **OK** in hello Basics blade.</span></span>

    ![기본 사항 블레이드](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection3.png)

5.  <span data-ttu-id="665e8-179">Hello에 **설정** 블레이드, 선택 hello **가상 네트워크 게이트웨이** hello를 확인 하 고 **권한 부여 교환** 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="665e8-179">In hello **Settings** blade, Select hello **Virtual network gateway** and check hello **Redeem authorization** check box.</span></span>

6.  <span data-ttu-id="665e8-180">Hello 입력 **인증 키** 및 hello **회로 URI 피어** hello 연결 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="665e8-180">Enter hello **Authorization key** and hello **Peer circuit URI** and give hello connection a name.</span></span> <span data-ttu-id="665e8-181">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="665e8-181">Click **OK**.</span></span>

    ![설정 블레이드](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection4.png)

7. <span data-ttu-id="665e8-183">Hello hello 정보를 검토 **요약** 블레이드에 대 한 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="665e8-183">Review hello information in hello **Summary** blade and click **OK**.</span></span>


<span data-ttu-id="665e8-184">**toorelease 연결 권한 부여**</span><span class="sxs-lookup"><span data-stu-id="665e8-184">**toorelease a connection authorization**</span></span>

<span data-ttu-id="665e8-185">Hello ExpressRoute 회로 toohello 가상 네트워크를 연결 하는 hello 연결을 삭제 하 여 권한 부여를 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="665e8-185">You can release an authorization by deleting hello connection that links hello ExpressRoute circuit toohello virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="665e8-186">다음 단계</span><span class="sxs-lookup"><span data-stu-id="665e8-186">Next steps</span></span>
<span data-ttu-id="665e8-187">ExpressRoute에 대 한 자세한 내용은 참조 hello [express 경로 FAQ](expressroute-faqs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="665e8-187">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

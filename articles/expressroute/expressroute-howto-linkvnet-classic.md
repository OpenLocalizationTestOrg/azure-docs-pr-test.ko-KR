---
title: "가상 네트워크 tooan ExpressRoute 회로 연결: PowerShell: 클래식: Azure | Microsoft Docs"
description: "이 문서는 가상 toolink (Vnet) tooExpressRoute 회로 hello 클래식 배포 모델 및 PowerShell을 사용 하 여 네트워크 하는 방법의 개요를 제공 합니다."
services: expressroute
documentationcenter: na
author: ganesr
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: 9b53fd72-9b6b-4844-80b9-4e1d54fd0c17
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/28/2017
ms.author: ganesr
ms.openlocfilehash: 6b8a01dcd4bbb9618ec3dd438cf0107538fb2a7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit-using-powershell-classic"></a><span data-ttu-id="aaa08-103">PowerShell (클래식)를 사용 하 여 가상 네트워크 tooan ExpressRoute 회로 연결</span><span class="sxs-lookup"><span data-stu-id="aaa08-103">Connect a virtual network tooan ExpressRoute circuit using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="aaa08-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="aaa08-104">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="aaa08-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="aaa08-105">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="aaa08-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="aaa08-106">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="aaa08-107">비디오 - Azure Portal</span><span class="sxs-lookup"><span data-stu-id="aaa08-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="aaa08-108">PowerShell(클래식)</span><span class="sxs-lookup"><span data-stu-id="aaa08-108">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
>

<span data-ttu-id="aaa08-109">이 문서는 hello 클래식 배포 모델 및 PowerShell을 사용 하 여 가상 네트워크 (Vnet) tooAzure ExpressRoute 회로 연결 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aaa08-109">This article will help you link virtual networks (VNets) tooAzure ExpressRoute circuits by using hello classic deployment model and PowerShell.</span></span> <span data-ttu-id="aaa08-110">가상 네트워크에 동일한 구독 hello 이거나 수 다른 구독이 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aaa08-110">Virtual networks can either be in hello same subscription or can be part of another subscription.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="aaa08-111">**Azure 배포 모델 정보**</span><span class="sxs-lookup"><span data-stu-id="aaa08-111">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="configuration-prerequisites"></a><span data-ttu-id="aaa08-112">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="aaa08-112">Configuration prerequisites</span></span>
1. <span data-ttu-id="aaa08-113">Hello hello Azure PowerShell 모듈의 최신 버전이 있어야합니다.</span><span class="sxs-lookup"><span data-stu-id="aaa08-113">You need hello latest version of hello Azure PowerShell modules.</span></span> <span data-ttu-id="aaa08-114">Hello hello의 PowerShell 세션에서에서 hello 최신 PowerShell 모듈을 다운로드할 수 있습니다 [Azure 다운로드 페이지](https://azure.microsoft.com/downloads/)합니다.</span><span class="sxs-lookup"><span data-stu-id="aaa08-114">You can download hello latest PowerShell modules from hello PowerShell section of hello [Azure Downloads page](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="aaa08-115">Hello 지침에 따라 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview) 방법에 대 한 단계별 지침에 대 한 tooconfigure 컴퓨터 toouse hello Azure PowerShell 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="aaa08-115">Follow hello instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for step-by-step guidance on how tooconfigure your computer toouse hello Azure PowerShell modules.</span></span>
2. <span data-ttu-id="aaa08-116">Tooreview hello 필요한 [필수 구성 요소](expressroute-prerequisites.md), [라우팅 요구 사항](expressroute-routing.md), 및 [워크플로](expressroute-workflows.md) 구성을 시작 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="aaa08-116">You need tooreview hello [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
3. <span data-ttu-id="aaa08-117">활성화된 Express 경로 회로가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaa08-117">You must have an active ExpressRoute circuit.</span></span>
   * <span data-ttu-id="aaa08-118">너무 hello 지침에 따라[ExpressRoute 회로 만들기](expressroute-howto-circuit-classic.md) 있고 연결 공급자 hello 회로 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaa08-118">Follow hello instructions too[create an ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have your connectivity provider enable hello circuit.</span></span>
   * <span data-ttu-id="aaa08-119">회로에 구성된 Azure 개인 피어링이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="aaa08-119">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="aaa08-120">Hello 참조 [구성 라우팅](expressroute-howto-routing-classic.md) 라우팅 지침에 대 한 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="aaa08-120">See hello [Configure routing](expressroute-howto-routing-classic.md) article for routing instructions.</span></span>
   * <span data-ttu-id="aaa08-121">구성 된 Azure 개인 피어 링 및 종단 간 연결을 사용 하도록 설정할 수 있도록 중일 hello 네트워크와 Microsoft 간에 BGP 피어 링을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaa08-121">Ensure that Azure private peering is configured and hello BGP peering between your network and Microsoft is up so that you can enable end-to-end connectivity.</span></span>
   * <span data-ttu-id="aaa08-122">가상 네트워크 및 가상 네트워크 게이트웨이를 만들고 완전히 프로비전해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaa08-122">You must have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="aaa08-123">너무 hello 지침에 따라[ExpressRoute에 대 한 가상 네트워크 구성](expressroute-howto-vnet-portal-classic.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="aaa08-123">Follow hello instructions too[configure a virtual network for ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span></span>

<span data-ttu-id="aaa08-124">가상 네트워크 tooan too10 ExpressRoute 회로를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aaa08-124">You can link up too10 virtual networks tooan ExpressRoute circuit.</span></span> <span data-ttu-id="aaa08-125">모든 가상 네트워크 hello에 있어야 합니다. 동일한 지리적 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="aaa08-125">All virtual networks must be in hello same geopolitical region.</span></span> <span data-ttu-id="aaa08-126">많은 수의 가상 네트워크 tooyour ExpressRoute 회로 연결 하거나 hello ExpressRoute premium 추가 기능을 사용 하는 경우 다른 지리적 지역에 있는 가상 네트워크를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aaa08-126">You can link a larger number of virtual networks tooyour ExpressRoute circuit, or link virtual networks that are in other geopolitical regions if you enabled hello ExpressRoute premium add-on.</span></span> <span data-ttu-id="aaa08-127">Hello 확인 [FAQ](expressroute-faqs.md) hello premium 추가 기능에 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaa08-127">Check hello [FAQ](expressroute-faqs.md) for more details on hello premium add-on.</span></span>

## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a><span data-ttu-id="aaa08-128">Hello의 가상 네트워크 연결 동일한 구독 tooa 회로</span><span class="sxs-lookup"><span data-stu-id="aaa08-128">Connect a virtual network in hello same subscription tooa circuit</span></span>
<span data-ttu-id="aaa08-129">Hello 다음 cmdlet을 사용 하 여 가상 네트워크 tooan ExpressRoute 회로 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aaa08-129">You can link a virtual network tooan ExpressRoute circuit by using hello following cmdlet.</span></span> <span data-ttu-id="aaa08-130">해당 hello 가상 네트워크 게이트웨이 만들어지고 hello cmdlet을 실행 하기 전에 연결을 위한 준비 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaa08-130">Make sure that hello virtual network gateway is created and is ready for linking before you run hello cmdlet.</span></span>

    New-AzureDedicatedCircuitLink -ServiceKey "*****************************" -VNetName "MyVNet"
    Provisioned

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a><span data-ttu-id="aaa08-131">다른 구독 tooa 회로에 가상 네트워크에 연결</span><span class="sxs-lookup"><span data-stu-id="aaa08-131">Connect a virtual network in a different subscription tooa circuit</span></span>
<span data-ttu-id="aaa08-132">여러 구독에서 Express 경로 회로를 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aaa08-132">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="aaa08-133">다음 그림 hello 간단한 계통도 나와의 ExpressRoute 회로 대 한 일정 공유 works 여러 구독에서.</span><span class="sxs-lookup"><span data-stu-id="aaa08-133">hello following figure shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

<span data-ttu-id="aaa08-134">사용 되는 toorepresent 속하는 구독에 조직 내의 toodifferent 부서는 각각 hello 작은 구름 hello 큰 구름 안에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aaa08-134">Each of hello smaller clouds within hello large cloud is used toorepresent subscriptions that belong toodifferent departments within an organization.</span></span> <span data-ttu-id="aaa08-135">단일 express 경로 회로 tooconnect 백 tooyour 온-프레미스 네트워크를 공유할 수 자신의 서비스--하지만 hello 부서 배포에 대 한 자신의 구독을 사용할 수 각각 hello 조직 내의 hello 부서입니다.</span><span class="sxs-lookup"><span data-stu-id="aaa08-135">Each of hello departments within hello organization can use their own subscription for deploying their services--but hello departments can share a single ExpressRoute circuit tooconnect back tooyour on-premises network.</span></span> <span data-ttu-id="aaa08-136">단일 부서 (이 예제의: IT) hello ExpressRoute 회로 소유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aaa08-136">A single department (in this example: IT) can own hello ExpressRoute circuit.</span></span> <span data-ttu-id="aaa08-137">Hello 조직 내에서 다른 구독 hello ExpressRoute 회로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aaa08-137">Other subscriptions within hello organization can use hello ExpressRoute circuit.</span></span>

> [!NOTE]
> <span data-ttu-id="aaa08-138">Hello 전용 회로 대 한 연결 및 대역폭 요금은 적용된 toohello ExpressRoute 회로 소유자 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aaa08-138">Connectivity and bandwidth charges for hello dedicated circuit will be applied toohello ExpressRoute circuit owner.</span></span> <span data-ttu-id="aaa08-139">Hello를 공유 하는 모든 가상 네트워크 대역폭이 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaa08-139">All virtual networks share hello same bandwidth.</span></span>
> 
> 

![구독 간 연결](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)

### <a name="administration"></a><span data-ttu-id="aaa08-141">관리</span><span class="sxs-lookup"><span data-stu-id="aaa08-141">Administration</span></span>
<span data-ttu-id="aaa08-142">hello *회로 소유자* hello 관리자/는 hello ExpressRoute 회로 만드는 hello 구독 coadministrator 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aaa08-142">hello *circuit owner* is hello administrator/coadministrator of hello subscription in which hello ExpressRoute circuit is created.</span></span> <span data-ttu-id="aaa08-143">hello 회로 소유자 권한을 부여할 수는 참조 된 tooas 다른 구독의 관리자/coadministrators *회로 사용자*, toouse hello 전용 소유 하는 회로입니다.</span><span class="sxs-lookup"><span data-stu-id="aaa08-143">hello circuit owner can authorize administrators/coadministrators of other subscriptions, referred tooas *circuit users*, toouse hello dedicated circuit that they own.</span></span> <span data-ttu-id="aaa08-144">권한이 부여 된 후 hello 자신의 구독 toohello ExpressRoute 회로에 가상 네트워크를 연결 하는 회로 사용자는 권한 있는 toouse hello 조직의 ExpressRoute 회로 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aaa08-144">Circuit users who are authorized toouse hello organization's ExpressRoute circuit can link hello virtual network in their subscription toohello ExpressRoute circuit after they are authorized.</span></span>

<span data-ttu-id="aaa08-145">hello 회로 소유자는 언제 든 지 hello 전원 toomodify 및 revoke 권한을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="aaa08-145">hello circuit owner has hello power toomodify and revoke authorizations at any time.</span></span> <span data-ttu-id="aaa08-146">권한 부여를 해지 모든 링크가 액세스가 해지 된 hello 구독에서 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aaa08-146">Revoking an authorization will result in all links being deleted from hello subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="aaa08-147">회로 소유자 작업</span><span class="sxs-lookup"><span data-stu-id="aaa08-147">Circuit owner operations</span></span>

<span data-ttu-id="aaa08-148">**권한 부여 만들기**</span><span class="sxs-lookup"><span data-stu-id="aaa08-148">**Creating an authorization**</span></span>

<span data-ttu-id="aaa08-149">hello 회로 소유자에 게 권한을 부여 hello 다른 구독 관리자에 toouse hello 회로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaa08-149">hello circuit owner authorizes hello administrators of other subscriptions toouse hello specified circuit.</span></span> <span data-ttu-id="aaa08-150">다음 예제는 hello, hello 회로 (Contoso IT) 관리자에 게 tootwo 가상 네트워크 toohello 회로를 다른 구독 (개발-테스트) toolink의 관리자에 게를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaa08-150">In hello following example, hello administrator of hello circuit (Contoso IT) enables hello administrator of another subscription (Dev-Test) toolink up tootwo virtual networks toohello circuit.</span></span> <span data-ttu-id="aaa08-151">Contoso IT 관리자에 게 hello 개발 테스트 Microsoft ID를 지정 하 여 사용 하면</span><span class="sxs-lookup"><span data-stu-id="aaa08-151">hello Contoso IT administrator enables this by specifying hello Dev-Test Microsoft ID.</span></span> <span data-ttu-id="aaa08-152">전자 메일 toohello Microsoft ID를 지정 된 hello cmdlet 보내지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="aaa08-152">hello cmdlet doesn't send email toohello specified Microsoft ID.</span></span> <span data-ttu-id="aaa08-153">hello 회로 소유자 있어야 tooexplicitly 알리는 hello hello 권한 부여 하는 다른 구독 소유자 완료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="aaa08-153">hello circuit owner needs tooexplicitly notify hello other subscription owner that hello authorization is complete.</span></span>

    New-AzureDedicatedCircuitLinkAuthorization -ServiceKey "**************************" -Description "Dev-Test Links" -Limit 2 -MicrosoftIds 'devtest@contoso.com'

    Description         : Dev-Test Links
    Limit               : 2
    LinkAuthorizationId : **********************************
    MicrosoftIds        : devtest@contoso.com
    Used                : 0

<span data-ttu-id="aaa08-154">**권한 부여 검토**</span><span class="sxs-lookup"><span data-stu-id="aaa08-154">**Reviewing authorizations**</span></span>

<span data-ttu-id="aaa08-155">hello 회로 소유자는 hello 다음 cmdlet을 실행 하 여 특정 회로에 발급 한 모든 권한 부여를 검토할 수 있습니다.:</span><span class="sxs-lookup"><span data-stu-id="aaa08-155">hello circuit owner can review all authorizations that are issued on a particular circuit by running hello following cmdlet:</span></span>

    Get-AzureDedicatedCircuitLinkAuthorization -ServiceKey: "**************************"

    Description         : EngineeringTeam
    Limit               : 3
    LinkAuthorizationId : ####################################
    MicrosoftIds        : engadmin@contoso.com
    Used                : 1

    Description         : MarketingTeam
    Limit               : 1
    LinkAuthorizationId : @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
    MicrosoftIds        : marketingadmin@contoso.com
    Used                : 0

    Description         : Dev-Test Links
    Limit               : 2
    LinkAuthorizationId : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    MicrosoftIds        : salesadmin@contoso.com
    Used                : 2


<span data-ttu-id="aaa08-156">**권한 부여 업데이트**</span><span class="sxs-lookup"><span data-stu-id="aaa08-156">**Updating authorizations**</span></span>

<span data-ttu-id="aaa08-157">hello 회로 소유자는 hello 다음 cmdlet을 사용 하 여 권한 부여를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aaa08-157">hello circuit owner can modify authorizations by using hello following cmdlet:</span></span>

    Set-AzureDedicatedCircuitLinkAuthorization -ServiceKey "**************************" -AuthorizationId "&&&&&&&&&&&&&&&&&&&&&&&&&&&&"-Limit 5

    Description         : Dev-Test Links
    Limit               : 5
    LinkAuthorizationId : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    MicrosoftIds        : devtest@contoso.com
    Used                : 0


<span data-ttu-id="aaa08-158">**권한 부여 삭제**</span><span class="sxs-lookup"><span data-stu-id="aaa08-158">**Deleting authorizations**</span></span>

<span data-ttu-id="aaa08-159">hello 회로 소유자 수 revoke/삭제 권한 부여 toohello 사용자 hello 다음 cmdlet을 실행 하 여:</span><span class="sxs-lookup"><span data-stu-id="aaa08-159">hello circuit owner can revoke/delete authorizations toohello user by running hello following cmdlet:</span></span>

    Remove-AzureDedicatedCircuitLinkAuthorization -ServiceKey "*****************************" -AuthorizationId "###############################"


### <a name="circuit-user-operations"></a><span data-ttu-id="aaa08-160">회로 사용자 작업</span><span class="sxs-lookup"><span data-stu-id="aaa08-160">Circuit user operations</span></span>

<span data-ttu-id="aaa08-161">**권한 부여 검토**</span><span class="sxs-lookup"><span data-stu-id="aaa08-161">**Reviewing authorizations**</span></span>

<span data-ttu-id="aaa08-162">hello 회로 사용자 hello 다음 cmdlet을 사용 하 여 권한 부여를 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aaa08-162">hello circuit user can review authorizations by using hello following cmdlet:</span></span>

    Get-AzureAuthorizedDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : ContosoIT
    Location                         : Washington DC
    MaximumAllowedLinks              : 2
    ServiceKey                       : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled
    UsedLinks                        : 0

<span data-ttu-id="aaa08-163">**링크 권한 부여 사용**</span><span class="sxs-lookup"><span data-stu-id="aaa08-163">**Redeeming link authorizations**</span></span>

<span data-ttu-id="aaa08-164">hello 회로 사용자 cmdlet tooredeem 다음 hello 링크 권한 부여를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aaa08-164">hello circuit user can run hello following cmdlet tooredeem a link authorization:</span></span>

    New-AzureDedicatedCircuitLink –servicekey "&&&&&&&&&&&&&&&&&&&&&&&&&&" –VnetName 'SalesVNET1'

    State VnetName
    ----- --------
    Provisioned SalesVNET1

<span data-ttu-id="aaa08-165">Hello 가상 네트워크에 대 한 hello 새로 연결 된 구독에서이 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaa08-165">Run this command in hello newly linked subscription for hello virtual network:</span></span>

    New-AzureDedicatedCircuitLink -ServiceKey "*****************************" -VNetName "MyVNet"

## <a name="next-steps"></a><span data-ttu-id="aaa08-166">다음 단계</span><span class="sxs-lookup"><span data-stu-id="aaa08-166">Next steps</span></span>
<span data-ttu-id="aaa08-167">ExpressRoute에 대 한 자세한 내용은 참조 hello [express 경로 FAQ](expressroute-faqs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="aaa08-167">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>


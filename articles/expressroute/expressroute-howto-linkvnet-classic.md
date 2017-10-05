---
title: "ExpressRoute 회로에 가상 네트워크 연결: PowerShell: 클래식: Azure | Microsoft Docs"
description: "이 문서는 클래식 배포 모델 및 PowerShell을 사용하여 VNet(가상 네트워크)을 Express 경로 회로에 연결하는 방법에 대한 개요를 제공합니다."
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
ms.openlocfilehash: 8df8a4c6ff0897c821e13248e0494b17e1a4992d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="connect-a-virtual-network-to-an-expressroute-circuit-using-powershell-classic"></a><span data-ttu-id="f142f-103">PowerShell을 사용하여 ExpressRoute 회로에 가상 네트워크 연결(클래식)</span><span class="sxs-lookup"><span data-stu-id="f142f-103">Connect a virtual network to an ExpressRoute circuit using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f142f-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="f142f-104">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="f142f-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f142f-105">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="f142f-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f142f-106">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="f142f-107">비디오 - Azure Portal</span><span class="sxs-lookup"><span data-stu-id="f142f-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="f142f-108">PowerShell(클래식)</span><span class="sxs-lookup"><span data-stu-id="f142f-108">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
>

<span data-ttu-id="f142f-109">이 문서를 참조하면 클래식 배포 모델 및 PowerShell을 사용하여 VNet(가상 네트워크)을 Azure Express 경로 회로에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f142f-109">This article will help you link virtual networks (VNets) to Azure ExpressRoute circuits by using the classic deployment model and PowerShell.</span></span> <span data-ttu-id="f142f-110">가상 네트워크는 같은 구독에 있을 수도 있고 다른 구독의 일부일 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f142f-110">Virtual networks can either be in the same subscription or can be part of another subscription.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="f142f-111">**Azure 배포 모델 정보**</span><span class="sxs-lookup"><span data-stu-id="f142f-111">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="configuration-prerequisites"></a><span data-ttu-id="f142f-112">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="f142f-112">Configuration prerequisites</span></span>
1. <span data-ttu-id="f142f-113">Azure PowerShell 모듈의 최신 버전이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f142f-113">You need the latest version of the Azure PowerShell modules.</span></span> <span data-ttu-id="f142f-114">[Azure 다운로드 페이지](https://azure.microsoft.com/downloads/)의 PowerShell 섹션에서 최신 PowerShell 모듈을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f142f-114">You can download the latest PowerShell modules from the PowerShell section of the [Azure Downloads page](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="f142f-115">Azure PowerShell 모듈을 사용하도록 컴퓨터를 구성하는 방법에 대한 단계별 지침은 [Azure PowerShell 설치 및 구성 방법](/powershell/azure/overview) 의 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="f142f-115">Follow the instructions in [How to install and configure Azure PowerShell](/powershell/azure/overview) for step-by-step guidance on how to configure your computer to use the Azure PowerShell modules.</span></span>
2. <span data-ttu-id="f142f-116">구성을 시작하기 전에 [필수 조건](expressroute-prerequisites.md), [라우팅 요구 사항](expressroute-routing.md) 및 [워크플로](expressroute-workflows.md)를 검토해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f142f-116">You need to review the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
3. <span data-ttu-id="f142f-117">활성화된 Express 경로 회로가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f142f-117">You must have an active ExpressRoute circuit.</span></span>
   * <span data-ttu-id="f142f-118">지침에 따라 [Express 경로 회로를 만들고](expressroute-howto-circuit-classic.md) 연결 공급자가 회로를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f142f-118">Follow the instructions to [create an ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have your connectivity provider enable the circuit.</span></span>
   * <span data-ttu-id="f142f-119">회로에 구성된 Azure 개인 피어링이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f142f-119">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="f142f-120">라우팅 지침에 대한 문서는 [라우팅 구성](expressroute-howto-routing-classic.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f142f-120">See the [Configure routing](expressroute-howto-routing-classic.md) article for routing instructions.</span></span>
   * <span data-ttu-id="f142f-121">Azure 개인 피어링이 구성되어 있고 네트워크와 Microsoft 간의 BGP 피어링이 종단 간 연결을 사용하도록 작동 중이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f142f-121">Ensure that Azure private peering is configured and the BGP peering between your network and Microsoft is up so that you can enable end-to-end connectivity.</span></span>
   * <span data-ttu-id="f142f-122">가상 네트워크 및 가상 네트워크 게이트웨이를 만들고 완전히 프로비전해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f142f-122">You must have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="f142f-123">지침에 따라 [Express 경로에 대한 가상 네트워크를 구성합니다](expressroute-howto-vnet-portal-classic.md).</span><span class="sxs-lookup"><span data-stu-id="f142f-123">Follow the instructions to [configure a virtual network for ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span></span>

<span data-ttu-id="f142f-124">최대 10개의 가상 네트워크를 Express 경로 회로에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f142f-124">You can link up to 10 virtual networks to an ExpressRoute circuit.</span></span> <span data-ttu-id="f142f-125">모든 가상 네트워크는 같은 지정학적 지역에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f142f-125">All virtual networks must be in the same geopolitical region.</span></span> <span data-ttu-id="f142f-126">프리미엄 추가 기능을 사용하도록 설정하면 Express 경로 회로에 많은 수의 가상 네트워크를 연결하거나 다른 지역에 있는 가상 네트워크를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f142f-126">You can link a larger number of virtual networks to your ExpressRoute circuit, or link virtual networks that are in other geopolitical regions if you enabled the ExpressRoute premium add-on.</span></span> <span data-ttu-id="f142f-127">프리미엄 추가 기능에 대한 자세한 내용은 [FAQ](expressroute-faqs.md) 에서 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="f142f-127">Check the [FAQ](expressroute-faqs.md) for more details on the premium add-on.</span></span>

## <a name="connect-a-virtual-network-in-the-same-subscription-to-a-circuit"></a><span data-ttu-id="f142f-128">동일한 구독에 있는 가상 네트워크를 회로에 연결</span><span class="sxs-lookup"><span data-stu-id="f142f-128">Connect a virtual network in the same subscription to a circuit</span></span>
<span data-ttu-id="f142f-129">다음 cmdlet을 사용하여 Express 경로 회로에 가상 네트워크를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f142f-129">You can link a virtual network to an ExpressRoute circuit by using the following cmdlet.</span></span> <span data-ttu-id="f142f-130">cmdlet을 실행하기 전에 가상 네트워크 게이트웨이가 연결을 위해 생성되고 준비되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f142f-130">Make sure that the virtual network gateway is created and is ready for linking before you run the cmdlet.</span></span>

    New-AzureDedicatedCircuitLink -ServiceKey "*****************************" -VNetName "MyVNet"
    Provisioned

## <a name="connect-a-virtual-network-in-a-different-subscription-to-a-circuit"></a><span data-ttu-id="f142f-131">다른 구독에 있는 가상 네트워크를 회로에 연결</span><span class="sxs-lookup"><span data-stu-id="f142f-131">Connect a virtual network in a different subscription to a circuit</span></span>
<span data-ttu-id="f142f-132">여러 구독에서 Express 경로 회로를 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f142f-132">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="f142f-133">아래 그림에는 여러 구독에서 Express 경로 회로에 대한 작업을 공유하는 방법의 간단한 계통도가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f142f-133">The following figure shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

<span data-ttu-id="f142f-134">큰 구름 안에 있는 각각의 작은 구름은 한 조직 내의 여러 부서에 속하는 구독을 나타내는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f142f-134">Each of the smaller clouds within the large cloud is used to represent subscriptions that belong to different departments within an organization.</span></span> <span data-ttu-id="f142f-135">조직 내의 각 부서는 자체 구독을 사용하여 서비스를 배포하되, 부서는 단일 Express 경로 회로를 공유하여 온-프레미스 네트워크로 다시 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f142f-135">Each of the departments within the organization can use their own subscription for deploying their services--but the departments can share a single ExpressRoute circuit to connect back to your on-premises network.</span></span> <span data-ttu-id="f142f-136">단일 부서(이 예제에서는 IT)가 Express 경로 회로를 소유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f142f-136">A single department (in this example: IT) can own the ExpressRoute circuit.</span></span> <span data-ttu-id="f142f-137">조직 내의 기타 구독도 Express 경로 회로를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f142f-137">Other subscriptions within the organization can use the ExpressRoute circuit.</span></span>

> [!NOTE]
> <span data-ttu-id="f142f-138">전용 회로에 대한 연결 및 대역폭 요금은 Express 경로 회로 소유자에게 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f142f-138">Connectivity and bandwidth charges for the dedicated circuit will be applied to the ExpressRoute circuit owner.</span></span> <span data-ttu-id="f142f-139">모든 가상 네트워크는 동일한 대역폭을 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="f142f-139">All virtual networks share the same bandwidth.</span></span>
> 
> 

![구독 간 연결](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)

### <a name="administration"></a><span data-ttu-id="f142f-141">관리</span><span class="sxs-lookup"><span data-stu-id="f142f-141">Administration</span></span>
<span data-ttu-id="f142f-142">*회로 소유자* 는 Express 경로 회로를 만드는 구독의 관리자/공동 관리자입니다.</span><span class="sxs-lookup"><span data-stu-id="f142f-142">The *circuit owner* is the administrator/coadministrator of the subscription in which the ExpressRoute circuit is created.</span></span> <span data-ttu-id="f142f-143">회로 소유자는 자신이 소유한 전용 회로를 *회로 사용자*라고 지칭되는 다른 구독의 관리자/공동 관리자가 사용하도록 권한을 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f142f-143">The circuit owner can authorize administrators/coadministrators of other subscriptions, referred to as *circuit users*, to use the dedicated circuit that they own.</span></span> <span data-ttu-id="f142f-144">조직의 Express 경로 회로 사용 권한을 부여받은 회로 사용자는 권한이 부여된 후 구독의 가상 네트워크를 Express 경로 회로에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f142f-144">Circuit users who are authorized to use the organization's ExpressRoute circuit can link the virtual network in their subscription to the ExpressRoute circuit after they are authorized.</span></span>

<span data-ttu-id="f142f-145">회로 소유자는 언제든지 부여된 권한을 수정하고 해지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f142f-145">The circuit owner has the power to modify and revoke authorizations at any time.</span></span> <span data-ttu-id="f142f-146">권한 부여를 해지하면 액세스가 해지된 구독에서 모든 링크가 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="f142f-146">Revoking an authorization will result in all links being deleted from the subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="f142f-147">회로 소유자 작업</span><span class="sxs-lookup"><span data-stu-id="f142f-147">Circuit owner operations</span></span>

<span data-ttu-id="f142f-148">**권한 부여 만들기**</span><span class="sxs-lookup"><span data-stu-id="f142f-148">**Creating an authorization**</span></span>

<span data-ttu-id="f142f-149">회로 소유자는 다른 구독 관리자에게 지정한 회로를 사용할 수 있는 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="f142f-149">The circuit owner authorizes the administrators of other subscriptions to use the specified circuit.</span></span> <span data-ttu-id="f142f-150">아래 예제에서 회로 관리자는(Contoso IT) 다른 구독의 관리자가(Dev-Test) 회로에 대해 최대 2개의 가상 네트워크를 연결하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f142f-150">In the following example, the administrator of the circuit (Contoso IT) enables the administrator of another subscription (Dev-Test) to link up to two virtual networks to the circuit.</span></span> <span data-ttu-id="f142f-151">Contoso IT 관리자는 Dev-Test Microsoft ID를 지정하여 이것을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f142f-151">The Contoso IT administrator enables this by specifying the Dev-Test Microsoft ID.</span></span> <span data-ttu-id="f142f-152">다음 cmdlet은 지정된 Microsoft ID로 전자 메일을 보내지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f142f-152">The cmdlet doesn't send email to the specified Microsoft ID.</span></span> <span data-ttu-id="f142f-153">회로 소유자는 권한 부여가 완료된 사실을 다른 구독 소유자에게 명시적으로 알려야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f142f-153">The circuit owner needs to explicitly notify the other subscription owner that the authorization is complete.</span></span>

    New-AzureDedicatedCircuitLinkAuthorization -ServiceKey "**************************" -Description "Dev-Test Links" -Limit 2 -MicrosoftIds 'devtest@contoso.com'

    Description         : Dev-Test Links
    Limit               : 2
    LinkAuthorizationId : **********************************
    MicrosoftIds        : devtest@contoso.com
    Used                : 0

<span data-ttu-id="f142f-154">**권한 부여 검토**</span><span class="sxs-lookup"><span data-stu-id="f142f-154">**Reviewing authorizations**</span></span>

<span data-ttu-id="f142f-155">회로 소유자는 다음 cmdlet을 실행하여 특정 회로에 발급한 모든 권한 부여를 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f142f-155">The circuit owner can review all authorizations that are issued on a particular circuit by running the following cmdlet:</span></span>

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


<span data-ttu-id="f142f-156">**권한 부여 업데이트**</span><span class="sxs-lookup"><span data-stu-id="f142f-156">**Updating authorizations**</span></span>

<span data-ttu-id="f142f-157">회로 소유자는 다음 cmdlet을 사용하여 권한 부여를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f142f-157">The circuit owner can modify authorizations by using the following cmdlet:</span></span>

    Set-AzureDedicatedCircuitLinkAuthorization -ServiceKey "**************************" -AuthorizationId "&&&&&&&&&&&&&&&&&&&&&&&&&&&&"-Limit 5

    Description         : Dev-Test Links
    Limit               : 5
    LinkAuthorizationId : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    MicrosoftIds        : devtest@contoso.com
    Used                : 0


<span data-ttu-id="f142f-158">**권한 부여 삭제**</span><span class="sxs-lookup"><span data-stu-id="f142f-158">**Deleting authorizations**</span></span>

<span data-ttu-id="f142f-159">회로 소유자는 다음 cmdlet을 실행하여 권한 부여를 취소/삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f142f-159">The circuit owner can revoke/delete authorizations to the user by running the following cmdlet:</span></span>

    Remove-AzureDedicatedCircuitLinkAuthorization -ServiceKey "*****************************" -AuthorizationId "###############################"


### <a name="circuit-user-operations"></a><span data-ttu-id="f142f-160">회로 사용자 작업</span><span class="sxs-lookup"><span data-stu-id="f142f-160">Circuit user operations</span></span>

<span data-ttu-id="f142f-161">**권한 부여 검토**</span><span class="sxs-lookup"><span data-stu-id="f142f-161">**Reviewing authorizations**</span></span>

<span data-ttu-id="f142f-162">회로 사용자는 다음 cmdlet을 사용하여 권한 부여를 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f142f-162">The circuit user can review authorizations by using the following cmdlet:</span></span>

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

<span data-ttu-id="f142f-163">**링크 권한 부여 사용**</span><span class="sxs-lookup"><span data-stu-id="f142f-163">**Redeeming link authorizations**</span></span>

<span data-ttu-id="f142f-164">회로 사용자는 다음 cmdlet을 실행하여 링크 권한 부여를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f142f-164">The circuit user can run the following cmdlet to redeem a link authorization:</span></span>

    New-AzureDedicatedCircuitLink –servicekey "&&&&&&&&&&&&&&&&&&&&&&&&&&" –VnetName 'SalesVNET1'

    State VnetName
    ----- --------
    Provisioned SalesVNET1

<span data-ttu-id="f142f-165">가상 네트워크에 대해 새로 연결된 구독에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f142f-165">Run this command in the newly linked subscription for the virtual network:</span></span>

    New-AzureDedicatedCircuitLink -ServiceKey "*****************************" -VNetName "MyVNet"

## <a name="next-steps"></a><span data-ttu-id="f142f-166">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f142f-166">Next steps</span></span>
<span data-ttu-id="f142f-167">ExpressRoute에 대한 자세한 내용은 [ExpressRoute FAQ](expressroute-faqs.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f142f-167">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>


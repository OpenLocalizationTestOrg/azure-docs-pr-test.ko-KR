---
title: "연결 확인: Azure ExpressRoute 문제 해결 가이드 | Microsoft Docs"
description: "ExpressRoute 회로에 대한 종단 간 연결의 유효성 검사 및 문제 해결에 대한 지침을 제공합니다."
documentationcenter: na
services: expressroute
author: rambk
manager: tracsman
editor: 
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: 5a6360b56963d219ab576fb3e2636b6c51dd72ac
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="verifying-expressroute-connectivity"></a><span data-ttu-id="e953f-103">ExpressRoute 연결 확인</span><span class="sxs-lookup"><span data-stu-id="e953f-103">Verifying ExpressRoute connectivity</span></span>
<span data-ttu-id="e953f-104">연결 공급자가 지원하는 개인 연결을 통해 온-프레미스 네트워크를 Microsoft 클라우드로 확장하는 ExpressRoute에는 다음 세 가지 고유 네트워크 영역이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-104">ExpressRoute, which extends an on-premises network into the Microsoft cloud over a private connection that is facilitated by a connectivity provider, involves the following three distinct network zones:</span></span>

-   <span data-ttu-id="e953f-105">고객 네트워크</span><span class="sxs-lookup"><span data-stu-id="e953f-105">Customer Network</span></span>
-   <span data-ttu-id="e953f-106">공급자 네트워크</span><span class="sxs-lookup"><span data-stu-id="e953f-106">Provider Network</span></span>
-   <span data-ttu-id="e953f-107">Microsoft 데이터 센터</span><span class="sxs-lookup"><span data-stu-id="e953f-107">Microsoft Datacenter</span></span>

<span data-ttu-id="e953f-108">이 문서는 사용자가 연결 문제가 있는 위치와 해당 영역을 파악하여 문제를 해결할 수 있도록 적절한 팀에 지원을 요청하는 데 도움이 되기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-108">The purpose of this document is to help user to identify where (or even if) a connectivity issue exists and within which zone, thereby to seek help from appropriate team to resolve the issue.</span></span> <span data-ttu-id="e953f-109">문제를 해결하기 위해 지원이 필요하면 [Microsoft 지원][Support]에서 지원 티켓을 열어주세요.</span><span class="sxs-lookup"><span data-stu-id="e953f-109">If Microsoft support is needed to resolve an issue, open a support ticket with [Microsoft Support][Support].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e953f-110">이 문서는 간단한 문제를 진단하고 수정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-110">This document is intended to help diagnosing and fixing simple issues.</span></span> <span data-ttu-id="e953f-111">이 문서는 Microsoft 기술 지원 서비스를 대체하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-111">It is not intended to be a replacement for Microsoft support.</span></span> <span data-ttu-id="e953f-112">제공된 지침을 사용하여 문제를 해결할 수 없으면 [Microsoft 지원][Support]에서 지원 티켓을 열어주세요.</span><span class="sxs-lookup"><span data-stu-id="e953f-112">Open a support ticket with [Microsoft Support][Support] if you are unable to solve the problem using the guidance provided.</span></span>
>
>

## <a name="overview"></a><span data-ttu-id="e953f-113">개요</span><span class="sxs-lookup"><span data-stu-id="e953f-113">Overview</span></span>
<span data-ttu-id="e953f-114">다음 다이어그램에서는 ExpressRoute를 통한 고객 네트워크와 Microsoft 네트워크 간의 논리적 연결을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-114">The following diagram shows the logical connectivity of a customer network to Microsoft network using ExpressRoute.</span></span>
<span data-ttu-id="e953f-115">[![1]][1]</span><span class="sxs-lookup"><span data-stu-id="e953f-115">[![1]][1]</span></span>

<span data-ttu-id="e953f-116">위의 다이어그램에서 숫자는 주요 네트워크 지점을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-116">In the preceding diagram, the numbers indicate key network points.</span></span> <span data-ttu-id="e953f-117">이 문서에서 네트워크 지점은 관련 번호로 자주 참조됩니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-117">The network points are referenced often through this article by their associated number.</span></span>

<span data-ttu-id="e953f-118">ExpressRoute 연결 모델(Cloud Exchange Co-location, 지점 간 이더넷 연결 또는 Any-to-Any(IPVPN))에 따라 네트워크 지점 3 및 4는 스위치(계층 2 장치)일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-118">Depending on the ExpressRoute connectivity model (Cloud Exchange Co-location, Point-to-Point Ethernet Connection, or Any-to-any (IPVPN)) the network points 3 and 4 may be switches (Layer 2 devices).</span></span> <span data-ttu-id="e953f-119">위의 다이어그램에서 보여 주는 주요 네트워크 지점은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-119">The key network points illustrated are as follows:</span></span>

1.  <span data-ttu-id="e953f-120">고객 계산 장치(예: 서버 또는 PC)</span><span class="sxs-lookup"><span data-stu-id="e953f-120">Customer compute device (for example, a server or PC)</span></span>
2.  <span data-ttu-id="e953f-121">CE: 고객 에지 라우터</span><span class="sxs-lookup"><span data-stu-id="e953f-121">CEs: Customer edge routers</span></span> 
3.  <span data-ttu-id="e953f-122">PE(CE 연결): 고객 에지 라우터에 연결되는 공급자 에지 라우터/스위치입니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-122">PEs (CE facing): Provider edge routers/switches that are facing customer edge routers.</span></span> <span data-ttu-id="e953f-123">이 문서에서는 PE-CE라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-123">Referred to as PE-CEs in this document.</span></span>
4.  <span data-ttu-id="e953f-124">PE(MSEE 연결): MSEE에 연결되는 공급자 에지 라우터/스위치입니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-124">PEs (MSEE facing): Provider edge routers/switches that are facing MSEEs.</span></span> <span data-ttu-id="e953f-125">이 문서에서는 PE-MSEE라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-125">Referred to as PE-MSEEs in this document.</span></span>
5.  <span data-ttu-id="e953f-126">MSEE: MSEE(Microsoft Enterprise Edge) ExpressRoute 라우터</span><span class="sxs-lookup"><span data-stu-id="e953f-126">MSEEs: Microsoft Enterprise Edge (MSEE) ExpressRoute routers</span></span>
6.  <span data-ttu-id="e953f-127">VNet(가상 네트워크) 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="e953f-127">Virtual Network (VNet) Gateway</span></span>
7.  <span data-ttu-id="e953f-128">Azure VNet의 계산 장치</span><span class="sxs-lookup"><span data-stu-id="e953f-128">Compute device on the Azure VNet</span></span>

<span data-ttu-id="e953f-129">연결 모델로 Cloud Exchange Co-location 또는 지점 간 이더넷 연결을 사용하는 경우 고객 에지 라우터(2)에서 MSEE(5)와의 BGP 피어링을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-129">If the Cloud Exchange Co-location or Point-to-Point Ethernet Connection connectivity models are used, the customer edge router (2) would establish BGP peering with MSEEs (5).</span></span> <span data-ttu-id="e953f-130">네트워크 지점 3과 4는 여전히 존재하지만 계층 2 장치로 다소 투명하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-130">Network points 3 and 4 would still exist but be somewhat transparent as Layer 2 devices.</span></span>

<span data-ttu-id="e953f-131">Any-to-Any(IPVPN) 연결 모델을 사용하는 경우 PE(MSEE 연결)(4)에서 MSEE(5)와의 BGP 피어링을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-131">If the Any-to-any (IPVPN) connectivity model is used, the PEs (MSEE facing) (4) would establish BGP peering with MSEEs (5).</span></span> <span data-ttu-id="e953f-132">그러면 경로가 IPVPN 서비스 공급자 네트워크를 통해 고객 네트워크로 다시 전파됩니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-132">Routes would then propagate back to the customer network via the IPVPN service provider network.</span></span>

>[!NOTE]
><span data-ttu-id="e953f-133">ExpressRoute 고가용성을 위해 MSEE(5)와 PE-MSEE(4) 간에 중복 쌍의 BGP 세션이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-133">For ExpressRoute high availability, Microsoft requires a redundant pair of BGP sessions between MSEEs (5) and PE-MSEEs (4).</span></span> <span data-ttu-id="e953f-134">고객 네트워크와 PE-CE 간에도 중복 쌍의 네트워크 경로를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-134">A redundant pair of network paths is also encouraged between customer network and PE-CEs.</span></span> <span data-ttu-id="e953f-135">그러나 Any-to-Any(IPVPN) 연결 모델에서는 단일 CE 장치(2)가 하나 이상의 PE(3)에 연결될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-135">However, in Any-to-any (IPVPN) connection model, a single CE device (2) may be connected to one or more PEs (3).</span></span>
>
>

<span data-ttu-id="e953f-136">ExpressRoute 회로의 유효성을 검사하기 위해 다음 단계가 적용됩니다(관련 번호로 표시된 네트워크 지점 사용).</span><span class="sxs-lookup"><span data-stu-id="e953f-136">To validate an ExpressRoute circuit, the following steps are covered (with the network point indicated by the associated number):</span></span>
1. [<span data-ttu-id="e953f-137">회로 프로비전 및 상태 확인 유효성 검사(5)</span><span class="sxs-lookup"><span data-stu-id="e953f-137">Validate circuit provisioning and state (5)</span></span>](#validate-circuit-provisioning-and-state)
2. [<span data-ttu-id="e953f-138">하나 이상의 ExpressRoute 피어링이 구성되었는지 확인(5)</span><span class="sxs-lookup"><span data-stu-id="e953f-138">Validate at least one ExpressRoute peering is configured (5)</span></span>](#validate-peering-configuration)
3. [<span data-ttu-id="e953f-139">Microsoft와 서비스 공급자 간의 ARP 유효성 검사(4와 5 사이의 링크)</span><span class="sxs-lookup"><span data-stu-id="e953f-139">Validate ARP between Microsoft and the service provider (link between 4 and 5)</span></span>](#validate-arp-between-microsoft-and-the-service-provider)
4. [<span data-ttu-id="e953f-140">MSEE에서 BGP 및 경로 유효성 검사(VNet이 연결된 경우 4와 5, 5와 6 사이의 BGP)</span><span class="sxs-lookup"><span data-stu-id="e953f-140">Validate BGP and routes on the MSEE (BGP between 4 to 5, and 5 to 6 if a VNet is connected)</span></span>](#validate-bgp-and-routes-on-the-msee)
5. [<span data-ttu-id="e953f-141">트래픽 통계 확인(5를 통과하는 트래픽)</span><span class="sxs-lookup"><span data-stu-id="e953f-141">Check the Traffic Statistics (Traffic passing through 5)</span></span>](#check-the-traffic-statistics)

<span data-ttu-id="e953f-142">나중에 더 많은 유효성 검사와 확인이 추가되며 매월 다시 확인해 주세요!</span><span class="sxs-lookup"><span data-stu-id="e953f-142">More validations and checks will be added in the future, check back monthly!</span></span>

##<a name="validate-circuit-provisioning-and-state"></a><span data-ttu-id="e953f-143">회로 프로비전 및 상태 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="e953f-143">Validate circuit provisioning and state</span></span>
<span data-ttu-id="e953f-144">연결 모델에 관계 없이 ExpressRoute 회로를 만들어야 하므로 회로 프로비전을 위해 생성된 서비스 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-144">Regardless of the connectivity model, an ExpressRoute circuit has to be created and thus a service key generated for circuit provisioning.</span></span> <span data-ttu-id="e953f-145">ExpressRoute 회로를 프로비전하면 PE-MSEE(4)와 MSEE(5) 간에 계층 2 중복 연결이 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-145">Provisioning an ExpressRoute circuit establishes a redundant Layer 2 connections between PE-MSEEs (4) and MSEEs (5).</span></span> <span data-ttu-id="e953f-146">ExpressRoute 회로 만들기, 수정, 프로비전 및 확인 방법에 대한 자세한 내용은 [ExpressRoute 회로 만들기 및 수정][CreateCircuit] 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e953f-146">For more information on how to create, modify, provision, and verify an ExpressRoute circuit, see the article [Create and modify an ExpressRoute circuit][CreateCircuit].</span></span>

>[!TIP]
><span data-ttu-id="e953f-147">서비스 키는 ExpressRoute 회로를 고유하게 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-147">A service key uniquely identifies an ExpressRoute circuit.</span></span> <span data-ttu-id="e953f-148">이 키는 이 문서에서 언급하는 PowerShell 명령 대부분에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-148">This key is required for most of the powershell commands mentioned in this document.</span></span> <span data-ttu-id="e953f-149">또한 Microsoft 또는 ExpressRoute 파트너로부터 도움을 받아 ExpressRoute 문제를 해결하려면 회로를 쉽게 식별할 수 있도록 서비스 키를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-149">Also, should you need assistance from Microsoft or from an ExpressRoute partner to troubleshoot an ExpressRoute issue, provide the service key to readily identify the circuit.</span></span>
>
>

###<a name="verification-via-the-azure-portal"></a><span data-ttu-id="e953f-150">Azure Portal을 통한 확인</span><span class="sxs-lookup"><span data-stu-id="e953f-150">Verification via the Azure portal</span></span>
<span data-ttu-id="e953f-151">Azure Portal에서 ExpressRoute 회로의 상태는 왼쪽 세로 막대 메뉴에서 ![2][2]를 선택한 다음 ExpressRoute 회로를 선택하여 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-151">In the Azure portal, the status of an ExpressRoute circuit can be checked by selecting ![2][2] on the left-side-bar menu and then selecting the ExpressRoute circuit.</span></span> <span data-ttu-id="e953f-152">"모든 리소스" 아래에 나열된 ExpressRoute 회로를 선택하면 ExpressRoute 회로 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-152">Selecting an ExpressRoute circuit listed under "All resources" opens the ExpressRoute circuit blade.</span></span> <span data-ttu-id="e953f-153">블레이드의 ![3][3] 섹션에는 ExpressRoute Essentials가 다음 스크린샷과 같이 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-153">In the ![3][3] section of the blade, the ExpressRoute essentials are listed as shown in the following screen shot:</span></span>

<span data-ttu-id="e953f-154">![4][4]</span><span class="sxs-lookup"><span data-stu-id="e953f-154">![4][4]</span></span>    

<span data-ttu-id="e953f-155">ExpressRoute Essentials에서 *회로 상태*는 Microsoft 쪽 회로 상태를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-155">In the ExpressRoute Essentials, *Circuit status* indicates the status of the circuit on the Microsoft side.</span></span> <span data-ttu-id="e953f-156">*공급자 상태*는 서비스 공급자 쪽에서 회로가 *프로비전됨/프로비전되지 않음*인지를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-156">*Provider status* indicates if the circuit has been *Provisioned/Not provisioned* on the service-provider side.</span></span> 

<span data-ttu-id="e953f-157">ExpressRoute 회로가 작동하려면 *회로 상태*가 *사용*이고, *공급자 상태*가 *프로비전됨*이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-157">For an ExpressRoute circuit to be operational, the *Circuit status* must be *Enabled* and the *Provider status* must be *Provisioned*.</span></span>

>[!NOTE]
><span data-ttu-id="e953f-158">*회로 상태*가 ‘사용’이 아니면 [Microsoft 지원][Support]에 문의하고,</span><span class="sxs-lookup"><span data-stu-id="e953f-158">If the *Circuit status* is not enabled, contact [Microsoft Support][Support].</span></span> <span data-ttu-id="e953f-159">*공급자 상태*가 ‘프로비전되지 않음’이면 서비스 공급자에게 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="e953f-159">If the *Provider status* is not provisioned, contact your service provider.</span></span>
>
>

###<a name="verification-via-powershell"></a><span data-ttu-id="e953f-160">PowerShell을 통한 확인</span><span class="sxs-lookup"><span data-stu-id="e953f-160">Verification via PowerShell</span></span>
<span data-ttu-id="e953f-161">리소스 그룹의 모든 ExpressRoute 회로를 나열하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-161">To list all the ExpressRoute circuits in a Resource Group, use the following command:</span></span>

    Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG"

>[!TIP]
><span data-ttu-id="e953f-162">Azure Portal을 통해 리소스 그룹 이름을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-162">You can get your resource group name through the Azure portal.</span></span> <span data-ttu-id="e953f-163">이 문서의 이전 하위 섹션을 참조하고, 리소스 그룹 이름은 예제 스크린샷에 나열되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-163">See the previous subsection of this document and note that the resource group name is listed in the example screen shot.</span></span>
>
>

<span data-ttu-id="e953f-164">[리소스 그룹]에서 특정 ExpressRoute 회로를 선택하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-164">To select a particular ExpressRoute circuit in a Resource Group, use the following command:</span></span>

    Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"

<span data-ttu-id="e953f-165">샘플 응답은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-165">A sample response is:</span></span>

    Name                             : Test-ER-Ckt
    ResourceGroupName                : Test-ER-RG
    Location                         : westus2
    Id                               : /subscriptions/***************************/resourceGroups/Test-ER-RG/providers/***********/expressRouteCircuits/Test-ER-Ckt
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                        "Name": "Standard_UnlimitedData",
                                        "Tier": "Standard",
                                        "Family": "UnlimitedData"
                                        }
    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned
    ServiceProviderNotes             : 
    ServiceProviderProperties        : {
                                        "ServiceProviderName": "****",
                                        "PeeringLocation": "******",
                                        "BandwidthInMbps": 100
                                        }
    ServiceKey                       : **************************************
    Peerings                         : []
    Authorizations                   : []

<span data-ttu-id="e953f-166">ExpressRoute 회로가 작동하는지 확인하려면 다음 필드에 특히 주의하세요.</span><span class="sxs-lookup"><span data-stu-id="e953f-166">To confirm if an ExpressRoute circuit is operational, pay particular attention to the following fields:</span></span>

    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned

>[!NOTE]
><span data-ttu-id="e953f-167">*CircuitProvisioningState*가 '사용'이 아니면 [Microsoft 지원][Support]에 문의하고,</span><span class="sxs-lookup"><span data-stu-id="e953f-167">If the *CircuitProvisioningState* is not enabled, contact [Microsoft Support][Support].</span></span> <span data-ttu-id="e953f-168">*ServiceProviderProvisioningState*가 '프로비전되지 않음'이면 서비스 공급자에게 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="e953f-168">If the *ServiceProviderProvisioningState* is not provisioned, contact your service provider.</span></span>
>
>

###<a name="verification-via-powershell-classic"></a><span data-ttu-id="e953f-169">PowerShell(클래식)을 통한 확인</span><span class="sxs-lookup"><span data-stu-id="e953f-169">Verification via PowerShell (Classic)</span></span>
<span data-ttu-id="e953f-170">구독 중인 모든 ExpressRoute 회로를 나열하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-170">To list all the ExpressRoute circuits under a subscription, use the following command:</span></span>

    Get-AzureDedicatedCircuit

<span data-ttu-id="e953f-171">특정 ExpressRoute 회로를 선택하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-171">To select a particular ExpressRoute circuit, use the following command:</span></span>

    Get-AzureDedicatedCircuit -ServiceKey **************************************

<span data-ttu-id="e953f-172">샘플 응답은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-172">A sample response is:</span></span>

    andwidth                         : 100
    BillingType                      : UnlimitedData
    CircuitName                      : Test-ER-Ckt
    Location                         : westus2
    ServiceKey                       : **************************************
    ServiceProviderName              : ****
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="e953f-173">ExpressRoute 회로가 작동하는지 확인하려면 ServiceProviderProvisioningState : Provisioned Status                           : Enabled 필드에 특히 주의하세요.</span><span class="sxs-lookup"><span data-stu-id="e953f-173">To confirm if an ExpressRoute circuit is operational, pay particular attention to the following fields: ServiceProviderProvisioningState : Provisioned Status                           : Enabled</span></span>

>[!NOTE]
><span data-ttu-id="e953f-174">*상태*가 ‘사용’이 아니면 [Microsoft 지원][Support]에 문의하고,</span><span class="sxs-lookup"><span data-stu-id="e953f-174">If the *Status* is not enabled, contact [Microsoft Support][Support].</span></span> <span data-ttu-id="e953f-175">*ServiceProviderProvisioningState*가 '프로비전되지 않음'이면 서비스 공급자에게 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="e953f-175">If the *ServiceProviderProvisioningState* is not provisioned, contact your service provider.</span></span>
>
>

##<a name="validate-peering-configuration"></a><span data-ttu-id="e953f-176">피어링 구성 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="e953f-176">Validate Peering Configuration</span></span>
<span data-ttu-id="e953f-177">서비스 공급자가 ExpressRoute 회로 프로비전을 완료하면 MSEE-PR(4)와 MSEE(5) 사이의 ExpressRoute 회로를 통해 라우팅 구성을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-177">After the service provider has completed the provisioning the ExpressRoute circuit, a routing configuration can be created over the ExpressRoute circuit between MSEE-PRs (4) and MSEEs (5).</span></span> <span data-ttu-id="e953f-178">ExpressRoute 회로마다 하나, 둘 또는 셋의 라우팅 컨텍스트, 즉 Azure 개인 피어링(Azure에서 개인 가상 네트워크로의 트래픽), Azure 공용 피어링(Azure에서 공용 IP 주소로의 트래픽) 및 Microsoft 피어링(Office 365 및 Dynamics 365로의 트래픽)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-178">Each ExpressRoute circuit can have one, two, or three routing contexts enabled: Azure private peering (traffic to private virtual networks in Azure), Azure public peering (traffic to public IP addresses in Azure), and Microsoft peering (traffic to Office 365 and Dynamics 365).</span></span> <span data-ttu-id="e953f-179">라우팅 구성을 만들고 수정하는 방법에 대한 자세한 내용은 [ExpressRoute 회로의 라우팅 만들기 및 수정][CreatePeering] 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e953f-179">For more information on how to create and modify routing configuration, see the article [Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>

###<a name="verification-via-the-azure-portal"></a><span data-ttu-id="e953f-180">Azure Portal을 통한 확인</span><span class="sxs-lookup"><span data-stu-id="e953f-180">Verification via the Azure portal</span></span>
>[!IMPORTANT]
><span data-ttu-id="e953f-181">서비스 공급자가 ExpressRoute 피어링을 구성한 경우 해당 피어링이 Azure Portal에 포털에 *표시되지 않는* 알려진 버그가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-181">There is a known bug in the Azure portal wherein ExpressRoute peerings are *NOT* shown in the portal if configured by the service provider.</span></span> <span data-ttu-id="e953f-182">포털 또는 PowerShell을 통해 ExpressRoute 피어링을 추가하면 *서비스 공급자 설정을 덮어씁니다*.</span><span class="sxs-lookup"><span data-stu-id="e953f-182">Adding ExpressRoute peerings via the portal or PowerShell *overwrites the service provider settings*.</span></span> <span data-ttu-id="e953f-183">이 작업을 수행하면 ExpressRoute 회로의 라우팅이 중단되며, 설정을 복원하고 일반 라우팅을 다시 설정하려면 서비스 공급자의 지원이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-183">This action breaks the routing on the ExpressRoute circuit and requires the support of the service provider to restore the settings and reestablish normal routing.</span></span> <span data-ttu-id="e953f-184">서비스 공급자가 계층 2 서비스만 제공하는 것이 확실한 경우에만 ExpressRoute 피어링을 수정하세요!</span><span class="sxs-lookup"><span data-stu-id="e953f-184">Only modify the ExpressRoute peerings if it is certain that the service provider is providing layer 2 services only!</span></span>
>
>

<p/>
>[!NOTE]
><span data-ttu-id="e953f-185">서비스 공급자가 계층 3을 제공하고 포털에서 피어링이 비어 있는 경우 PowerShell을 사용하여 서비스 공급자가 구성한 설정을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-185">If layer 3 is provided by the service provider and the peerings are blank in the portal, PowerShell can be used to see the service provider configured settings.</span></span>
>
>

<span data-ttu-id="e953f-186">Azure Portal에서 ExpressRoute 회로의 상태는 왼쪽 세로 막대 메뉴에서 ![2][2]를 선택한 다음 ExpressRoute 회로를 선택하여 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-186">In the Azure portal, status of an ExpressRoute circuit can be checked by selecting ![2][2] on the left-side-bar menu and then selecting the ExpressRoute circuit.</span></span> <span data-ttu-id="e953f-187">"모든 리소스" 아래에 나열된 ExpressRoute 회로를 선택하면 ExpressRoute 회로 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-187">Selecting an ExpressRoute circuit listed under "All resources" would open the ExpressRoute circuit blade.</span></span> <span data-ttu-id="e953f-188">블레이드의 ![3][3] 섹션에는 ExpressRoute Essentials가 다음 스크린샷과 같이 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-188">In the ![3][3] section of the blade, the ExpressRoute essentials would be listed as shown in the following screen shot:</span></span>

<span data-ttu-id="e953f-189">![5][5]</span><span class="sxs-lookup"><span data-stu-id="e953f-189">![5][5]</span></span>

<span data-ttu-id="e953f-190">앞의 예제에서 명시한 대로 Azure 개인 피어링 라우팅 컨텍스트는 사용할 수 있지만, Azure 공용 피어링 및 Microsoft 피어링 라우팅 컨텍스트는 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-190">In the preceding example, as noted Azure private peering routing context is enabled, whereas Azure public and Microsoft peering routing contexts are not enabled.</span></span> <span data-ttu-id="e953f-191">또한 성공적으로 사용되는 피어링 컨텍스트에는 기본 및 보조 지점 간(BGP에 필수) 서브넷이 나열되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-191">A successfully enabled peering context would also have the primary and secondary point-to-point (required for BGP) subnets listed.</span></span> <span data-ttu-id="e953f-192">/30 서브넷은 MSEE 및 PE-MSEE의 인터페이스 IP 주소에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-192">The /30 subnets are used for the interface IP address of the MSEEs and PE-MSEEs.</span></span> 

>[!NOTE]
><span data-ttu-id="e953f-193">피어링을 사용하지 않는 경우 할당된 기본 및 보조 서브넷이 PE-MSEE의 구성과 일치하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-193">If a peering is not enabled, check if the primary and secondary subnets assigned match the configuration on PE-MSEEs.</span></span> <span data-ttu-id="e953f-194">그렇지 않은 경우 MSEE 라우터의 구성을 변경하려면 [ExpressRoute 회로의 라우팅 만들기 및 수정][CreatePeering]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e953f-194">If not, to change the configuration on MSEE routers, refer to [Create and modify routing for an ExpressRoute circuit][CreatePeering]</span></span>
>
>

###<a name="verification-via-powershell"></a><span data-ttu-id="e953f-195">PowerShell을 통한 확인</span><span class="sxs-lookup"><span data-stu-id="e953f-195">Verification via PowerShell</span></span>
<span data-ttu-id="e953f-196">Azure 개인 피어링 구성 세부 정보를 가져오려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-196">To get the Azure private peering configuration details, use the following commands:</span></span>

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -Circuit $ckt

<span data-ttu-id="e953f-197">성공적으로 구성된 개인 피어링에 대한 샘플 응답은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-197">A sample response, for a successfully configured private peering, is:</span></span>

    Name                       : AzurePrivatePeering
    Id                         : /subscriptions/***************************/resourceGroups/Test-ER-RG/providers/***********/expressRouteCircuits/Test-ER-Ckt/peerings/AzurePrivatePeering
    Etag                       : W/"################################"
    PeeringType                : AzurePrivatePeering
    AzureASN                   : 12076
    PeerASN                    : ####
    PrimaryPeerAddressPrefix   : 172.16.0.0/30
    SecondaryPeerAddressPrefix : 172.16.0.4/30
    PrimaryAzurePort           : 
    SecondaryAzurePort         : 
    SharedKey                  : 
    VlanId                     : 300
    MicrosoftPeeringConfig     : null
    ProvisioningState          : Succeeded

 <span data-ttu-id="e953f-198">성공적으로 사용되는 피어링 컨텍스트에는 기본 및 보조 주소 접두사가 나열되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-198">A successfully enabled peering context would have the primary and secondary address prefixes listed.</span></span> <span data-ttu-id="e953f-199">/30 서브넷은 MSEE 및 PE-MSEE의 인터페이스 IP 주소에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-199">The /30 subnets are used for the interface IP address of the MSEEs and PE-MSEEs.</span></span>

<span data-ttu-id="e953f-200">Azure 공용 피어링 구성 세부 정보를 가져오려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-200">To get the Azure public peering configuration details, use the following commands:</span></span>

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -Circuit $ckt

<span data-ttu-id="e953f-201">Microsoft 피어링 구성 세부 정보를 가져오려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-201">To get the Microsoft peering configuration details, use the following commands:</span></span>

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -Circuit $ckt

<span data-ttu-id="e953f-202">피어링이 구성되어 있지 않으면 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-202">If a peering is not configured, there would be an error message.</span></span> <span data-ttu-id="e953f-203">명시된 피어링(이 예제에서는 Azure 공용 피어링)이 회로 내에 구성되지 않은 경우 샘플 응답은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-203">A sample response, when the stated peering (Azure Public peering in this example) is not configured within the circuit:</span></span>

    Get-AzureRmExpressRouteCircuitPeeringConfig : Sequence contains no matching element
    At line:1 char:1
        + Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering ...
        + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
            + CategoryInfo          : CloseError: (:) [Get-AzureRmExpr...itPeeringConfig], InvalidOperationException
            + FullyQualifiedErrorId : Microsoft.Azure.Commands.Network.GetAzureExpressRouteCircuitPeeringConfigCommand


<p/>
>[!NOTE]
><span data-ttu-id="e953f-204">피어링을 사용하지 않는 경우 할당된 기본 및 보조 서브넷이 연결된 PE-MSEE의 구성과 일치하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-204">If a peering is not enabled, check if the primary and secondary subnets assigned match the configuration on the linked PE-MSEE.</span></span> <span data-ttu-id="e953f-205">또한 올바른 *VlanId*, *AzureASN* 및 *PeerASN*이 MSEE에서 사용되는지 여부와 이러한 값이 연결된 PE-MSEE에서 사용된 값에 매핑되는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-205">Also check if the correct *VlanId*, *AzureASN*, and *PeerASN* are used on MSEEs and if these values maps to the ones used on the linked PE-MSEE.</span></span> <span data-ttu-id="e953f-206">MD5 해싱을 선택하는 경우 공유 키가 MSEE 및 PE-MSEE 쌍에서 동일해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-206">If MD5 hashing is chosen, the shared key should be same on MSEE and PE-MSEE pair.</span></span> <span data-ttu-id="e953f-207">MSEE 라우터의 구성을 변경하려면 [ExpressRoute 회로의 라우팅 만들기 및 수정][CreatePeering]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e953f-207">To change the configuration on the MSEE routers, refer to [Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>  
>
>

### <a name="verification-via-powershell-classic"></a><span data-ttu-id="e953f-208">PowerShell(클래식)을 통한 확인</span><span class="sxs-lookup"><span data-stu-id="e953f-208">Verification via PowerShell (Classic)</span></span>
<span data-ttu-id="e953f-209">Azure 개인 피어링 구성 세부 정보를 가져오려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-209">To get the Azure private peering configuration details, use the following command:</span></span>

    Get-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"

<span data-ttu-id="e953f-210">성공적으로 구성된 개인 피어링에 대한 샘플 응답은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-210">A sample response, for a successfully configured private peering is:</span></span>

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : ####
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 100

<span data-ttu-id="e953f-211">성공적으로 사용되는 피어링 컨텍스트에는 기본 및 보조 피어 서브넷이 나열되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-211">A successfully, enabled peering context would have the primary and secondary peer subnets listed.</span></span> <span data-ttu-id="e953f-212">/30 서브넷은 MSEE 및 PE-MSEE의 인터페이스 IP 주소에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-212">The /30 subnets are used for the interface IP address of the MSEEs and PE-MSEEs.</span></span>

<span data-ttu-id="e953f-213">Azure 공용 피어링 구성 세부 정보를 가져오려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-213">To get the Azure public peering configuration details, use the following commands:</span></span>

    Get-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

<span data-ttu-id="e953f-214">Microsoft 피어링 구성 세부 정보를 가져오려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-214">To get the Microsoft peering configuration details, use the following commands:</span></span>

    Get-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

>[!IMPORTANT]
><span data-ttu-id="e953f-215">서비스 공급자가 계층 3 피어링을 설정한 경우 포털 또는 PowerShell을 통해 ExpressRoute 피어링을 설정하면 서비스 공급자 설정을 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-215">If layer 3 peerings were set by the service provider, setting the ExpressRoute peerings via the portal or PowerShell overwrites the service provider settings.</span></span> <span data-ttu-id="e953f-216">공급자 쪽 피어링 설정을 다시 설정하려면 서비스 공급자의 지원이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-216">Resetting the provider side peering settings requires the support of the service provider.</span></span> <span data-ttu-id="e953f-217">서비스 공급자가 계층 2 서비스만 제공하는 것이 확실한 경우에만 ExpressRoute 피어링을 수정하세요!</span><span class="sxs-lookup"><span data-stu-id="e953f-217">Only modify the ExpressRoute peerings if it is certain that the service provider is providing layer 2 services only!</span></span>
>
>

<p/>
>[!NOTE]
><span data-ttu-id="e953f-218">피어링을 사용하지 않는 경우 할당된 기본 및 보조 피어 서브넷이 연결된 PE-MSEE의 구성과 일치하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-218">If a peering is not enabled, check if the primary and secondary peer subnets assigned match the configuration on the linked PE-MSEE.</span></span> <span data-ttu-id="e953f-219">또한 올바른 *VlanId*, *AzureAsn* 및 *PeerAsn*이 MSEE에서 사용되는지 여부와 이러한 값이 연결된 PE-MSEE에서 사용된 값에 매핑되는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-219">Also check if the correct *VlanId*, *AzureAsn*, and *PeerAsn* are used on MSEEs and if these values maps to the ones used on the linked PE-MSEE.</span></span> <span data-ttu-id="e953f-220">MSEE 라우터의 구성을 변경하려면 [ExpressRoute 회로의 라우팅 만들기 및 수정][CreatePeering]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e953f-220">To change the configuration on the MSEE routers, refer to [Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>
>
>

## <a name="validate-arp-between-microsoft-and-the-service-provider"></a><span data-ttu-id="e953f-221">Microsoft와 서비스 공급자 간의 ARP 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="e953f-221">Validate ARP between Microsoft and the service provider</span></span>
<span data-ttu-id="e953f-222">이 섹션에서는 PowerShell(클래식) 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-222">This section uses PowerShell (Classic) commands.</span></span> <span data-ttu-id="e953f-223">PowerShell Azure Resource Manager 명령을 사용하고 있으면 [Azure 클래식 포털][OldPortal]을 통해 관리자/공동 관리자로서 구독에 액세스할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-223">If you have been using PowerShell Azure Resource Manager commands, ensure that you have admin/co-admin access to the subscription via [Azure classic portal][OldPortal].</span></span> <span data-ttu-id="e953f-224">Azure Resource Manager 명령 사용과 관련된 문제를 해결하려면 [Resource Manager 배포 모델에서 ARP 테이블 가져오기][ARP] 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e953f-224">For troubleshooting using Azure Resource Manager commands please refer to the [Getting ARP tables in the Resource Manager deployment model][ARP] document.</span></span>

>[!NOTE]
><span data-ttu-id="e953f-225">ARP를 가져오려면 Azure Portal 및 Azure Resource Manager PowerShell 명령을 모두 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-225">To get ARP, both the Azure portal and Azure Resource Manager PowerShell commands can be used.</span></span> <span data-ttu-id="e953f-226">Azure Resource Manager PowerShell 명령에 오류가 발생하는 경우 클래식 PowerShell 명령은 Azure Resource Manager ExpressRoute 회로에서도 작동하므로 클래식 PowerShell 명령이 작동해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-226">If errors are encountered with the Azure Resource Manager PowerShell commands, classic PowerShell commands should work as Classic PowerShell commands also work with Azure Resource Manager ExpressRoute circuits.</span></span>
>
>

<span data-ttu-id="e953f-227">개인 피어링을 위해 기본 MSEE 라우터에서 ARP 테이블을 가져오려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-227">To get the ARP table from the primary MSEE router for the private peering, use the following command:</span></span>

    Get-AzureDedicatedCircuitPeeringArpInfo -AccessType Private -Path Primary -ServiceKey "*********************************"

<span data-ttu-id="e953f-228">성공적인 시나리오에서 명령에 대한 응답 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-228">An example response for the command, in the successful scenario:</span></span>

    ARP Info:

                 Age           Interface           IpAddress          MacAddress
                 113             On-Prem       10.0.0.1           e8ed.f335.4ca9
                   0           Microsoft       10.0.0.2           7c0e.ce85.4fc9

<span data-ttu-id="e953f-229">마찬가지로 *개인*/*공용*/*Microsoft* 피어링의 *기본*/*보조* 경로에 있는 MSEE에서 ARP 테이블을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-229">Similarly, you can check the ARP table from the MSEE in the *Primary*/*Secondary* path, for *Private*/*Public*/*Microsoft* peerings.</span></span>

<span data-ttu-id="e953f-230">다음 예제에서는 피어링에 대한 명령의 응답이 없음을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-230">The following example shows the response of the command for a peering does not exist.</span></span>

    ARP Info:
       
>[!NOTE]
><span data-ttu-id="e953f-231">ARP 테이블에 MAC 주소에 매핑된 인터페이스의 IP 주소가 없으면 다음 정보를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-231">If the ARP table does not have IP addresses of the interfaces mapped to MAC addresses, review the following information:</span></span>
>1. <span data-ttu-id="e953f-232">MSEE-PR과 MSEE 사이의 링크에 할당된 /30 서브넷의 첫 번째 IP 주소가 MSEE-PR의 인터페이스에서 사용되는 경우</span><span class="sxs-lookup"><span data-stu-id="e953f-232">If the first IP address of the /30 subnet assigned for the link between the MSEE-PR and MSEE is used on the interface of MSEE-PR.</span></span> <span data-ttu-id="e953f-233">Azure에서 항상 두 번째 IP 주소를 MSEE에 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-233">Azure always uses the second IP address for MSEEs.</span></span>
>2. <span data-ttu-id="e953f-234">고객(C-Tag) 및 서비스(S-Tag) VLAN 태그가 MSEE-PR 및 MSEE 쌍 모두와 일치하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-234">Verify if the customer (C-Tag) and service (S-Tag) VLAN tags match both on MSEE-PR and MSEE pair.</span></span>
>
>

## <a name="validate-bgp-and-routes-on-the-msee"></a><span data-ttu-id="e953f-235">MSEE에서 BGP 및 경로 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="e953f-235">Validate BGP and routes on the MSEE</span></span>
<span data-ttu-id="e953f-236">이 섹션에서는 PowerShell(클래식) 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-236">This section uses PowerShell (Classic) commands.</span></span> <span data-ttu-id="e953f-237">PowerShell Azure Resource Manager 명령을 사용하고 있으면 [Azure 클래식 포털][OldPortal]을 통해 관리자/공동 관리자로서 구독에 액세스할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-237">If you have been using PowerShell Azure Resource Manager commands, ensure that you have admin/co-admin access to the subscription via [Azure classic portal][OldPortal]</span></span>

>[!NOTE]
><span data-ttu-id="e953f-238">BGP 정보를 가져오려면 Azure Portal 및 Azure Resource Manager PowerShell 명령을 모두 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-238">To get BGP information, both the Azure portal and Azure Resource Manager PowerShell commands can be used.</span></span> <span data-ttu-id="e953f-239">Azure Resource Manager PowerShell 명령에 오류가 발생하는 경우 클래식 PowerShell 명령은 Azure Resource Manager ExpressRoute 회로에서도 작동하므로 클래식 PowerShell 명령이 작동해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-239">If errors are encountered with the Azure Resource Manager PowerShell commands, classic PowerShell commands should work as classic PowerShell commands also work with Azure Resource Manager ExpressRoute circuits.</span></span>
>
>

<span data-ttu-id="e953f-240">특정 라우팅 컨텍스트에 대한 라우팅 테이블(BGP 인접 라우터) 요약을 가져오려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-240">To get the routing table (BGP neighbor) summary for a particular routing context, use the following command:</span></span>

    Get-AzureDedicatedCircuitPeeringRouteTableSummary -AccessType Private -Path Primary -ServiceKey "*********************************"

<span data-ttu-id="e953f-241">예제 응답은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-241">An example response is:</span></span>

    Route Table Summary:

            Neighbor                   V                  AS              UpDown         StatePfxRcd
            10.0.0.1                   4                ####                8w4d                  50

<span data-ttu-id="e953f-242">앞의 예제와 같이 이 명령은 라우팅 컨텍스트가 설정된 기간을 확인하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-242">As shown in the preceding example, the command is useful to determine for how long the routing context has been established.</span></span> <span data-ttu-id="e953f-243">또한 피어링 라우터에서 보급하는 경로 접두사의 수도 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-243">It also indicates number of route prefixes advertised by the peering router.</span></span>

>[!NOTE]
><span data-ttu-id="e953f-244">상태가 활성 또는 유휴 상태이면 할당된 기본 및 보조 피어 서브넷이 연결된 PE-MSEE의 구성과 일치하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-244">If the state is in Active or Idle, check if the primary and secondary peer subnets assigned match the configuration on the linked PE-MSEE.</span></span> <span data-ttu-id="e953f-245">또한 올바른 *VlanId*, *AzureAsn* 및 *PeerAsn*이 MSEE에서 사용되는지 여부와 이러한 값이 연결된 PE-MSEE에서 사용된 값에 매핑되는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-245">Also check if the correct *VlanId*, *AzureAsn*, and *PeerAsn* are used on MSEEs and if these values maps to the ones used on the linked PE-MSEE.</span></span> <span data-ttu-id="e953f-246">MD5 해싱을 선택하는 경우 공유 키가 MSEE 및 PE-MSEE 쌍에서 동일해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-246">If MD5 hashing is chosen, the shared key should be same on MSEE and PE-MSEE pair.</span></span> <span data-ttu-id="e953f-247">MSEE 라우터의 구성을 변경하려면 [ExpressRoute 회로의 라우팅 만들기 및 수정][CreatePeering]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e953f-247">To change the configuration on the MSEE routers, refer to [Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>
>
>

<p/>
>[!NOTE]
><span data-ttu-id="e953f-248">특정 피어링을 통해 특정 대상에 연결할 수 없는 경우 특정 피어링 컨텍스트에 속한 MSEE의 경로 테이블을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="e953f-248">If certain destinations are not reachable over a particular peering, check the route table of the MSEEs belonging to the particular peering context.</span></span> <span data-ttu-id="e953f-249">라우팅 테이블에 일치하는 접두사(NATed IP일 수 있음)가 있는 경우 경로에 방화벽/NSG/ACL이 있는지와 트래픽을 허용하는지를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="e953f-249">If a matching prefix (could be NATed IP) is present in the routing table, then check if there are firewalls/NSG/ACLs on the path and if they permit the traffic.</span></span>
>
>

<span data-ttu-id="e953f-250">특정 *개인* 라우팅 컨텍스트의 *기본* 경로에 있는 MSEE에서 전체 라우팅 테이블을 가져오려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-250">To get the full routing table from MSEE on the *Primary* path for the particular *Private* routing context, use the following command:</span></span>

    Get-AzureDedicatedCircuitPeeringRouteTableInfo -AccessType Private -Path Primary -ServiceKey "*********************************"

<span data-ttu-id="e953f-251">명령의 성공적인 예제 결과는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-251">An example successful outcome for the command is:</span></span>

    Route Table Info:

             Network             NextHop              LocPrf              Weight                Path
         10.1.0.0/16            10.0.0.1                                       0    #### ##### #####     
         10.2.0.0/16            10.0.0.1                                       0    #### ##### #####
    ...

<span data-ttu-id="e953f-252">마찬가지로 *개인*/*공용*/*Microsoft* 피어링 컨텍스트의 *기본*/*보조* 경로에 있는 MSEE에서 라우팅 테이블을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-252">Similarly, you can check the routing table from the MSEE in the *Primary*/*Secondary* path, for *Private*/*Public*/*Microsoft* a peering context.</span></span>

<span data-ttu-id="e953f-253">다음 예제에서는 피어링에 대한 명령의 응답이 없음을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-253">The following example shows the response of the command for a peering does not exist:</span></span>

    Route Table Info:

##<a name="check-the-traffic-statistics"></a><span data-ttu-id="e953f-254">트래픽 통계 확인</span><span class="sxs-lookup"><span data-stu-id="e953f-254">Check the Traffic Statistics</span></span>
<span data-ttu-id="e953f-255">피어링 컨텍스트의 기본 및 보조 경로 트래픽 통계(송/수신 바이트 수)를 가져오려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-255">To get the combined primary and secondary path traffic statistics--bytes in and out--of a peering context, use the following command:</span></span>

    Get-AzureDedicatedCircuitStats -ServiceKey 97f85950-01dd-4d30-a73c-bf683b3a6e5c -AccessType Private

<span data-ttu-id="e953f-256">명령 출력의 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-256">A sample output of the command is:</span></span>

    PrimaryBytesIn PrimaryBytesOut SecondaryBytesIn SecondaryBytesOut
    -------------- --------------- ---------------- -----------------
         240780020       239863857        240565035         239628474

<span data-ttu-id="e953f-257">존재하지 않는 피어링에 대한 명령 출력의 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e953f-257">A sample output of the command for a non-existent peering is:</span></span>

    Get-AzureDedicatedCircuitStats : ResourceNotFound: Can not find any subinterface for peering type 'Public' for circuit '97f85950-01dd-4d30-a73c-bf683b3a6e5c' .
    At line:1 char:1
    + Get-AzureDedicatedCircuitStats -ServiceKey 97f85950-01dd-4d30-a73c-bf ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : CloseError: (:) [Get-AzureDedicatedCircuitStats], CloudException
        + FullyQualifiedErrorId : Microsoft.WindowsAzure.Commands.ExpressRoute.GetAzureDedicatedCircuitPeeringStatsCommand

## <a name="next-steps"></a><span data-ttu-id="e953f-258">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e953f-258">Next Steps</span></span>
<span data-ttu-id="e953f-259">자세한 정보 또는 도움말을 보려면 다음 링크를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="e953f-259">For more information or help, check out the following links:</span></span>

- <span data-ttu-id="e953f-260">[Microsoft 지원][Support]</span><span class="sxs-lookup"><span data-stu-id="e953f-260">[Microsoft Support][Support]</span></span>
- <span data-ttu-id="e953f-261">[ExpressRoute 회로 만들기 및 수정][CreateCircuit]</span><span class="sxs-lookup"><span data-stu-id="e953f-261">[Create and modify an ExpressRoute circuit][CreateCircuit]</span></span>
- <span data-ttu-id="e953f-262">[ExpressRoute 회로의 라우팅 만들기 및 수정][CreatePeering]</span><span class="sxs-lookup"><span data-stu-id="e953f-262">[Create and modify routing for an ExpressRoute circuit][CreatePeering]</span></span>

<!--Image References-->
<span data-ttu-id="e953f-263">[1]: ./media/expressroute-troubleshooting-expressroute-overview/expressroute-logical-diagram.png "논리 ExpressRoute 연결"</span><span class="sxs-lookup"><span data-stu-id="e953f-263">[1]: ./media/expressroute-troubleshooting-expressroute-overview/expressroute-logical-diagram.png "Logical Express Route Connectivity"</span></span>
<span data-ttu-id="e953f-264">[2]: ./media/expressroute-troubleshooting-expressroute-overview/portal-all-resources.png "모든 리소스 아이콘"</span><span class="sxs-lookup"><span data-stu-id="e953f-264">[2]: ./media/expressroute-troubleshooting-expressroute-overview/portal-all-resources.png "All resources icon"</span></span>
<span data-ttu-id="e953f-265">[3]: ./media/expressroute-troubleshooting-expressroute-overview/portal-overview.png "개요 아이콘"</span><span class="sxs-lookup"><span data-stu-id="e953f-265">[3]: ./media/expressroute-troubleshooting-expressroute-overview/portal-overview.png "Overview icon"</span></span>
<span data-ttu-id="e953f-266">[4]: ./media/expressroute-troubleshooting-expressroute-overview/portal-circuit-status.png "ExpressRoute Essentials 샘플 스크린샷"</span><span class="sxs-lookup"><span data-stu-id="e953f-266">[4]: ./media/expressroute-troubleshooting-expressroute-overview/portal-circuit-status.png "ExpressRoute Essentials sample screenshot"</span></span>
<span data-ttu-id="e953f-267">[5]: ./media/expressroute-troubleshooting-expressroute-overview/portal-private-peering.png "ExpressRoute Essentials 샘플 스크린샷"</span><span class="sxs-lookup"><span data-stu-id="e953f-267">[5]: ./media/expressroute-troubleshooting-expressroute-overview/portal-private-peering.png "ExpressRoute Essentials sample screenshot"</span></span>

<!--Link References-->
[Support]: https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[CreateCircuit]: https://docs.microsoft.com/azure/expressroute/expressroute-howto-circuit-portal-resource-manager 
[CreatePeering]: https://docs.microsoft.com/azure/expressroute/expressroute-howto-routing-portal-resource-manager
[OldPortal]: https://manage.windowsazure.com
[ARP]: https://docs.microsoft.com/en-us/azure/expressroute/expressroute-troubleshooting-arp-resource-manager







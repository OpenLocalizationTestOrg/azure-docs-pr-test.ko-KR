---
title: "연결 확인: Azure ExpressRoute 문제 해결 가이드 | Microsoft Docs"
description: "이 페이지는 ExpressRoute 회로의 최종 tooend 연결 유효성 검사 및 문제 해결에 지침을 제공 합니다."
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
ms.openlocfilehash: 713c39c7eafd77a4380b2a91902a9686f2ce1d85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="verifying-expressroute-connectivity"></a><span data-ttu-id="41bd6-103">ExpressRoute 연결 확인</span><span class="sxs-lookup"><span data-stu-id="41bd6-103">Verifying ExpressRoute connectivity</span></span>
<span data-ttu-id="41bd6-104">ExpressRoute 연결 공급자를 통해 이루어집니다 개인 연결을 통해 hello Microsoft 클라우드로 온-프레미스 네트워크를 확장 하는 hello 다음 3 개의 고유한 네트워크 영역에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-104">ExpressRoute, which extends an on-premises network into hello Microsoft cloud over a private connection that is facilitated by a connectivity provider, involves hello following three distinct network zones:</span></span>

-   <span data-ttu-id="41bd6-105">고객 네트워크</span><span class="sxs-lookup"><span data-stu-id="41bd6-105">Customer Network</span></span>
-   <span data-ttu-id="41bd6-106">공급자 네트워크</span><span class="sxs-lookup"><span data-stu-id="41bd6-106">Provider Network</span></span>
-   <span data-ttu-id="41bd6-107">Microsoft 데이터 센터</span><span class="sxs-lookup"><span data-stu-id="41bd6-107">Microsoft Datacenter</span></span>

<span data-ttu-id="41bd6-108">이 문서의 hello 목적은 toohelp 사용자 tooidentify 위치 (또는 경우에) 연결 문제가 존재 하 고, 영역 내에서 tooseek 쉽게에서 적합 한 팀 tooresolve hello 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-108">hello purpose of this document is toohelp user tooidentify where (or even if) a connectivity issue exists and within which zone, thereby tooseek help from appropriate team tooresolve hello issue.</span></span> <span data-ttu-id="41bd6-109">Microsoft 지원에 필요한 tooresolve 문제 이면와 지원 티켓을 개설할 [Microsoft 지원][Support]합니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-109">If Microsoft support is needed tooresolve an issue, open a support ticket with [Microsoft Support][Support].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="41bd6-110">이 문서가 의도 한 toohelp 진단 및 간단한 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-110">This document is intended toohelp diagnosing and fixing simple issues.</span></span> <span data-ttu-id="41bd6-111">의도 한 toobe Microsoft 지원에 대 한 대체 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-111">It is not intended toobe a replacement for Microsoft support.</span></span> <span data-ttu-id="41bd6-112">지원 티켓을 열고 [Microsoft 지원] [ Support] 제공 하는 hello 지침을 사용 하 여 없습니다 toosolve hello 문제가 있다면 합니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-112">Open a support ticket with [Microsoft Support][Support] if you are unable toosolve hello problem using hello guidance provided.</span></span>
>
>

## <a name="overview"></a><span data-ttu-id="41bd6-113">개요</span><span class="sxs-lookup"><span data-stu-id="41bd6-113">Overview</span></span>
<span data-ttu-id="41bd6-114">hello 다음 그림에 hello ExpressRoute를 사용 하는 고객 네트워크 tooMicrosoft 네트워크의 논리적 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-114">hello following diagram shows hello logical connectivity of a customer network tooMicrosoft network using ExpressRoute.</span></span>
<span data-ttu-id="41bd6-115">[![1]][1]</span><span class="sxs-lookup"><span data-stu-id="41bd6-115">[![1]][1]</span></span>

<span data-ttu-id="41bd6-116">Hello 다이어그램 앞, hello 숫자 키 네트워크 지점을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-116">In hello preceding diagram, hello numbers indicate key network points.</span></span> <span data-ttu-id="41bd6-117">hello 네트워크 지점 관련 번호로이 문서를 통해 자주 참조 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-117">hello network points are referenced often through this article by their associated number.</span></span>

<span data-ttu-id="41bd6-118">Hello ExpressRoute 연결에 따라 모델 (클라우드 Exchange 공동 배치, 지점 간 이더넷 연결 또는 Any-에-any (IPVPN)) hello 네트워크 지점 3과 4 (계층 2 장치) 스위치를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-118">Depending on hello ExpressRoute connectivity model (Cloud Exchange Co-location, Point-to-Point Ethernet Connection, or Any-to-any (IPVPN)) hello network points 3 and 4 may be switches (Layer 2 devices).</span></span> <span data-ttu-id="41bd6-119">hello 키 네트워크 지점 예시는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-119">hello key network points illustrated are as follows:</span></span>

1.  <span data-ttu-id="41bd6-120">고객 계산 장치(예: 서버 또는 PC)</span><span class="sxs-lookup"><span data-stu-id="41bd6-120">Customer compute device (for example, a server or PC)</span></span>
2.  <span data-ttu-id="41bd6-121">CE: 고객 에지 라우터</span><span class="sxs-lookup"><span data-stu-id="41bd6-121">CEs: Customer edge routers</span></span> 
3.  <span data-ttu-id="41bd6-122">PE(CE 연결): 고객 에지 라우터에 연결되는 공급자 에지 라우터/스위치입니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-122">PEs (CE facing): Provider edge routers/switches that are facing customer edge routers.</span></span> <span data-ttu-id="41bd6-123">이 문서에서 PE CEs tooas를 라고합니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-123">Referred tooas PE-CEs in this document.</span></span>
4.  <span data-ttu-id="41bd6-124">PE(MSEE 연결): MSEE에 연결되는 공급자 에지 라우터/스위치입니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-124">PEs (MSEE facing): Provider edge routers/switches that are facing MSEEs.</span></span> <span data-ttu-id="41bd6-125">이 문서에서 PE MSEEs tooas를 라고합니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-125">Referred tooas PE-MSEEs in this document.</span></span>
5.  <span data-ttu-id="41bd6-126">MSEE: MSEE(Microsoft Enterprise Edge) ExpressRoute 라우터</span><span class="sxs-lookup"><span data-stu-id="41bd6-126">MSEEs: Microsoft Enterprise Edge (MSEE) ExpressRoute routers</span></span>
6.  <span data-ttu-id="41bd6-127">VNet(가상 네트워크) 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="41bd6-127">Virtual Network (VNet) Gateway</span></span>
7.  <span data-ttu-id="41bd6-128">Hello Azure VNet에서 장치를 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-128">Compute device on hello Azure VNet</span></span>

<span data-ttu-id="41bd6-129">Hello 클라우드 교환 공동 배치 또는 이더넷 연결 지점 간 연결 모델을 사용 하는 경우 hello 고객에 지 라우터가 (2)는 MSEEs (5)와 피어 링 BGP를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-129">If hello Cloud Exchange Co-location or Point-to-Point Ethernet Connection connectivity models are used, hello customer edge router (2) would establish BGP peering with MSEEs (5).</span></span> <span data-ttu-id="41bd6-130">네트워크 지점 3과 4는 여전히 존재하지만 계층 2 장치로 다소 투명하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-130">Network points 3 and 4 would still exist but be somewhat transparent as Layer 2 devices.</span></span>

<span data-ttu-id="41bd6-131">Hello Any-에-any (IPVPN) 연결 모델을 사용 하는 경우에 pes가 있습니다 (연결 된 MSEE) hello (4) MSEEs (5)와 피어 링 BGP를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-131">If hello Any-to-any (IPVPN) connectivity model is used, hello PEs (MSEE facing) (4) would establish BGP peering with MSEEs (5).</span></span> <span data-ttu-id="41bd6-132">다음 경로 hello IPVPN 서비스 공급자 네트워크를 통해 백 toohello 고객 네트워크를 전파 합니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-132">Routes would then propagate back toohello customer network via hello IPVPN service provider network.</span></span>

>[!NOTE]
><span data-ttu-id="41bd6-133">ExpressRoute 고가용성을 위해 MSEE(5)와 PE-MSEE(4) 간에 중복 쌍의 BGP 세션이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-133">For ExpressRoute high availability, Microsoft requires a redundant pair of BGP sessions between MSEEs (5) and PE-MSEEs (4).</span></span> <span data-ttu-id="41bd6-134">고객 네트워크와 PE-CE 간에도 중복 쌍의 네트워크 경로를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-134">A redundant pair of network paths is also encouraged between customer network and PE-CEs.</span></span> <span data-ttu-id="41bd6-135">그러나 Any-에-any (IPVPN) 연결 모델에서 단일 CE 장치 (2) 연결 된 tooone 또는 자세한에 pes가 있습니다 (3) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-135">However, in Any-to-any (IPVPN) connection model, a single CE device (2) may be connected tooone or more PEs (3).</span></span>
>
>

<span data-ttu-id="41bd6-136">ExpressRoute 회로 단계를 수행 하는 hello toovalidate (지점과 hello 네트워크에 연결 하는 hello 수로 표시 된) 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-136">toovalidate an ExpressRoute circuit, hello following steps are covered (with hello network point indicated by hello associated number):</span></span>
1. [<span data-ttu-id="41bd6-137">회로 프로비전 및 상태 확인 유효성 검사(5)</span><span class="sxs-lookup"><span data-stu-id="41bd6-137">Validate circuit provisioning and state (5)</span></span>](#validate-circuit-provisioning-and-state)
2. [<span data-ttu-id="41bd6-138">하나 이상의 ExpressRoute 피어링이 구성되었는지 확인(5)</span><span class="sxs-lookup"><span data-stu-id="41bd6-138">Validate at least one ExpressRoute peering is configured (5)</span></span>](#validate-peering-configuration)
3. [<span data-ttu-id="41bd6-139">Microsoft 및 hello 서비스 공급자 (4와 5 사이의 링크) 간의 ARP 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="41bd6-139">Validate ARP between Microsoft and hello service provider (link between 4 and 5)</span></span>](#validate-arp-between-microsoft-and-the-service-provider)
4. [<span data-ttu-id="41bd6-140">BGP 및 hello MSEE (BGP 4 too5 사이의 5 too6 VNet 연결 되어 있는 경우)에서 경로 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="41bd6-140">Validate BGP and routes on hello MSEE (BGP between 4 too5, and 5 too6 if a VNet is connected)</span></span>](#validate-bgp-and-routes-on-the-msee)
5. [<span data-ttu-id="41bd6-141">Hello 트래픽 통계 (5 전달 되는 트래픽에)를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-141">Check hello Traffic Statistics (Traffic passing through 5)</span></span>](#check-the-traffic-statistics)

<span data-ttu-id="41bd6-142">유효성 검사 및 검사를 더 추가 될 예정 hello 미래 다시 확인 매월!</span><span class="sxs-lookup"><span data-stu-id="41bd6-142">More validations and checks will be added in hello future, check back monthly!</span></span>

##<a name="validate-circuit-provisioning-and-state"></a><span data-ttu-id="41bd6-143">회로 프로비전 및 상태 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="41bd6-143">Validate circuit provisioning and state</span></span>
<span data-ttu-id="41bd6-144">Hello 연결 모델에 관계 없이 ExpressRoute 회로 만든 toobe 및 서비스 회로 프로 비전 하기 위해 생성 된 키입니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-144">Regardless of hello connectivity model, an ExpressRoute circuit has toobe created and thus a service key generated for circuit provisioning.</span></span> <span data-ttu-id="41bd6-145">ExpressRoute 회로를 프로비전하면 PE-MSEE(4)와 MSEE(5) 간에 계층 2 중복 연결이 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-145">Provisioning an ExpressRoute circuit establishes a redundant Layer 2 connections between PE-MSEEs (4) and MSEEs (5).</span></span> <span data-ttu-id="41bd6-146">Toocreate를 수정, 프로 비전, 고 ExpressRoute 회로 확인 방법에 대 한 자세한 내용은 hello 문서 참조 [만들기 ExpressRoute 회로 수정 하 고][CreateCircuit]합니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-146">For more information on how toocreate, modify, provision, and verify an ExpressRoute circuit, see hello article [Create and modify an ExpressRoute circuit][CreateCircuit].</span></span>

>[!TIP]
><span data-ttu-id="41bd6-147">서비스 키는 ExpressRoute 회로를 고유하게 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-147">A service key uniquely identifies an ExpressRoute circuit.</span></span> <span data-ttu-id="41bd6-148">이 키는이 문서에 언급 된 hello powershell 명령의 대부분에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-148">This key is required for most of hello powershell commands mentioned in this document.</span></span> <span data-ttu-id="41bd6-149">또한 필요한 경우에 지원 Microsoft 또는 express 경로 파트너 tootroubleshoot ExpressRoute 문제에서 hello 서비스 제공 키 tooreadily hello 회로 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-149">Also, should you need assistance from Microsoft or from an ExpressRoute partner tootroubleshoot an ExpressRoute issue, provide hello service key tooreadily identify hello circuit.</span></span>
>
>

###<a name="verification-via-hello-azure-portal"></a><span data-ttu-id="41bd6-150">Hello Azure 포털을 통해 확인</span><span class="sxs-lookup"><span data-stu-id="41bd6-150">Verification via hello Azure portal</span></span>
<span data-ttu-id="41bd6-151">Azure 포털 hello, hello 상태 ExpressRoute 회로를 선택 하 여 확인할 수 있습니다 ![2][2] 사이드바 왼쪽 메뉴에서 다음 hello ExpressRoute 회로 hello에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-151">In hello Azure portal, hello status of an ExpressRoute circuit can be checked by selecting ![2][2] on hello left-side-bar menu and then selecting hello ExpressRoute circuit.</span></span> <span data-ttu-id="41bd6-152">Express 경로 선택 하면 "모든 리소스" 아래에 나열 하는 회로 hello ExpressRoute 회로 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-152">Selecting an ExpressRoute circuit listed under "All resources" opens hello ExpressRoute circuit blade.</span></span> <span data-ttu-id="41bd6-153">Hello에 ![3][3] hello 블레이드에서 hello essentials hello 스크린 샷 뒤에 표시 된 것으로 나열 된 ExpressRoute의 섹션:</span><span class="sxs-lookup"><span data-stu-id="41bd6-153">In hello ![3][3] section of hello blade, hello ExpressRoute essentials are listed as shown in hello following screen shot:</span></span>

<span data-ttu-id="41bd6-154">![4][4]</span><span class="sxs-lookup"><span data-stu-id="41bd6-154">![4][4]</span></span>    

<span data-ttu-id="41bd6-155">ExpressRoute Essentials hello에 *상태 회로* hello 회로 hello Microsoft 쪽에서의 hello 상태를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-155">In hello ExpressRoute Essentials, *Circuit status* indicates hello status of hello circuit on hello Microsoft side.</span></span> <span data-ttu-id="41bd6-156">*공급자 상태* hello 회로 되었음을 나타냅니다 *프로 비전 됨/Not 프로 비전* hello 서비스 공급자 쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-156">*Provider status* indicates if hello circuit has been *Provisioned/Not provisioned* on hello service-provider side.</span></span> 

<span data-ttu-id="41bd6-157">Operational ExpressRoute 회로 toobe는, hello *상태 회로* 여야 *Enabled* 및 hello *공급자 상태* 이어야 합니다 *프로비전됨*.</span><span class="sxs-lookup"><span data-stu-id="41bd6-157">For an ExpressRoute circuit toobe operational, hello *Circuit status* must be *Enabled* and hello *Provider status* must be *Provisioned*.</span></span>

>[!NOTE]
><span data-ttu-id="41bd6-158">경우 hello *상태 회로* 는 문의 사용할 수 없는 [Microsoft 지원][Support]합니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-158">If hello *Circuit status* is not enabled, contact [Microsoft Support][Support].</span></span> <span data-ttu-id="41bd6-159">경우 hello *공급자 상태* 은 서비스 공급자에 게 문의 프로 비전 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-159">If hello *Provider status* is not provisioned, contact your service provider.</span></span>
>
>

###<a name="verification-via-powershell"></a><span data-ttu-id="41bd6-160">PowerShell을 통한 확인</span><span class="sxs-lookup"><span data-stu-id="41bd6-160">Verification via PowerShell</span></span>
<span data-ttu-id="41bd6-161">toolist은 리소스 그룹의 ExpressRoute 회로 hello 모두, 다음 명령을 hello를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="41bd6-161">toolist all hello ExpressRoute circuits in a Resource Group, use hello following command:</span></span>

    Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG"

>[!TIP]
><span data-ttu-id="41bd6-162">리소스 그룹 이름은 Azure 포털 hello를 통해 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-162">You can get your resource group name through hello Azure portal.</span></span> <span data-ttu-id="41bd6-163">이 문서의 이전 섹션에 있는 hello 참조 및 해당 hello 리소스 그룹 이름은 hello 예제에서는 화면에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-163">See hello previous subsection of this document and note that hello resource group name is listed in hello example screen shot.</span></span>
>
>

<span data-ttu-id="41bd6-164">리소스 그룹에서 다음 명령을 사용 하 여 hello 특정 ExpressRoute 회로 tooselect:</span><span class="sxs-lookup"><span data-stu-id="41bd6-164">tooselect a particular ExpressRoute circuit in a Resource Group, use hello following command:</span></span>

    Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"

<span data-ttu-id="41bd6-165">샘플 응답은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-165">A sample response is:</span></span>

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

<span data-ttu-id="41bd6-166">tooconfirm은 ExpressRoute 회로 작동 하는 경우에 특히 주의 toohello 필드 뒤 지불:</span><span class="sxs-lookup"><span data-stu-id="41bd6-166">tooconfirm if an ExpressRoute circuit is operational, pay particular attention toohello following fields:</span></span>

    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned

>[!NOTE]
><span data-ttu-id="41bd6-167">경우 hello *CircuitProvisioningState* 는 문의 사용할 수 없는 [Microsoft 지원][Support]합니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-167">If hello *CircuitProvisioningState* is not enabled, contact [Microsoft Support][Support].</span></span> <span data-ttu-id="41bd6-168">경우 hello *ServiceProviderProvisioningState* 은 서비스 공급자에 게 문의 프로 비전 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-168">If hello *ServiceProviderProvisioningState* is not provisioned, contact your service provider.</span></span>
>
>

###<a name="verification-via-powershell-classic"></a><span data-ttu-id="41bd6-169">PowerShell(클래식)을 통한 확인</span><span class="sxs-lookup"><span data-stu-id="41bd6-169">Verification via PowerShell (Classic)</span></span>
<span data-ttu-id="41bd6-170">toolist 구독에서 ExpressRoute 회로 hello 모두, 다음 명령을 hello를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="41bd6-170">toolist all hello ExpressRoute circuits under a subscription, use hello following command:</span></span>

    Get-AzureDedicatedCircuit

<span data-ttu-id="41bd6-171">tooselect 특정 ExpressRoute 회로 다음 명령을 사용 하 여 hello:</span><span class="sxs-lookup"><span data-stu-id="41bd6-171">tooselect a particular ExpressRoute circuit, use hello following command:</span></span>

    Get-AzureDedicatedCircuit -ServiceKey **************************************

<span data-ttu-id="41bd6-172">샘플 응답은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-172">A sample response is:</span></span>

    andwidth                         : 100
    BillingType                      : UnlimitedData
    CircuitName                      : Test-ER-Ckt
    Location                         : westus2
    ServiceKey                       : **************************************
    ServiceProviderName              : ****
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="41bd6-173">tooconfirm ExpressRoute 회로 작동 하는 경우 지불 필드를 수행 하는 특별 한 주의 toohello: ServiceProviderProvisioningState: 사용자를 프로 비전 상태: 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="41bd6-173">tooconfirm if an ExpressRoute circuit is operational, pay particular attention toohello following fields: ServiceProviderProvisioningState : Provisioned Status                           : Enabled</span></span>

>[!NOTE]
><span data-ttu-id="41bd6-174">경우 hello *상태* 는 문의 사용할 수 없는 [Microsoft 지원][Support]합니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-174">If hello *Status* is not enabled, contact [Microsoft Support][Support].</span></span> <span data-ttu-id="41bd6-175">경우 hello *ServiceProviderProvisioningState* 은 서비스 공급자에 게 문의 프로 비전 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-175">If hello *ServiceProviderProvisioningState* is not provisioned, contact your service provider.</span></span>
>
>

##<a name="validate-peering-configuration"></a><span data-ttu-id="41bd6-176">피어링 구성 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="41bd6-176">Validate Peering Configuration</span></span>
<span data-ttu-id="41bd6-177">Hello 서비스 공급자가 완료 된 hello hello ExpressRoute 회로 프로 비전 한 후에 라우팅 구성은 hello MSEE-Pr (4)와 (5) MSEEs 간의 ExpressRoute 회로 통해 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-177">After hello service provider has completed hello provisioning hello ExpressRoute circuit, a routing configuration can be created over hello ExpressRoute circuit between MSEE-PRs (4) and MSEEs (5).</span></span> <span data-ttu-id="41bd6-178">각 ExpressRoute 회로 하나, 두 개 또는 세 개의 라우팅 컨텍스트에 사용할 수 있을 수 있습니다: Azure 개인 피어 링 (트래픽 tooprivate Azure에서 가상 네트워크), Azure 공용 피어 링 (트래픽 toopublic IP 주소 Azure의) 및 Microsoft (트래픽 tooOffice 365 피어 링 및 Dynamics 365)입니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-178">Each ExpressRoute circuit can have one, two, or three routing contexts enabled: Azure private peering (traffic tooprivate virtual networks in Azure), Azure public peering (traffic toopublic IP addresses in Azure), and Microsoft peering (traffic tooOffice 365 and Dynamics 365).</span></span> <span data-ttu-id="41bd6-179">방법에 대 한 자세한 내용은 toocreate 라우팅 구성을 수정 하 고 hello 문서를 참조 하십시오 [만들기 및 수정 ExpressRoute 회로 대 한 라우팅][CreatePeering]합니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-179">For more information on how toocreate and modify routing configuration, see hello article [Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>

###<a name="verification-via-hello-azure-portal"></a><span data-ttu-id="41bd6-180">Hello Azure 포털을 통해 확인</span><span class="sxs-lookup"><span data-stu-id="41bd6-180">Verification via hello Azure portal</span></span>
>[!IMPORTANT]
><span data-ttu-id="41bd6-181">Hello에 express 경로 피어 링은 Azure 포털의 알려진된 버그가 있습니다 *하지* hello 포털 hello 서비스 공급자가 구성 된 경우에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-181">There is a known bug in hello Azure portal wherein ExpressRoute peerings are *NOT* shown in hello portal if configured by hello service provider.</span></span> <span data-ttu-id="41bd6-182">Express 경로 피어 링 hello 포털 또는 PowerShell을 통해 추가 *hello 서비스 공급자 설정을 덮어씁니다*합니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-182">Adding ExpressRoute peerings via hello portal or PowerShell *overwrites hello service provider settings*.</span></span> <span data-ttu-id="41bd6-183">이 작업 hello hello ExpressRoute 회로 대해 라우팅 및 hello 서비스 공급자 toorestore hello 설정의 hello 지원이 필요로 끊어지고 일반 라우팅 다시 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-183">This action breaks hello routing on hello ExpressRoute circuit and requires hello support of hello service provider toorestore hello settings and reestablish normal routing.</span></span> <span data-ttu-id="41bd6-184">것이 확실 hello 서비스 공급자에는 계층 2 서비스에만 제공 하는 경우에 hello express 경로 피어 링을 수정!</span><span class="sxs-lookup"><span data-stu-id="41bd6-184">Only modify hello ExpressRoute peerings if it is certain that hello service provider is providing layer 2 services only!</span></span>
>
>

<p/>
>[!NOTE]
><span data-ttu-id="41bd6-185">계층 3 제공 서비스 공급자 및 hello 피어 링 hello 하 여 hello 포털에서 비어 있는 경우 PowerShell 사용된 toosee hello 서비스 공급자 구성 설정 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-185">If layer 3 is provided by hello service provider and hello peerings are blank in hello portal, PowerShell can be used toosee hello service provider configured settings.</span></span>
>
>

<span data-ttu-id="41bd6-186">Azure 포털 hello, 상태 ExpressRoute 회로를 선택 하 여 확인할 수 있습니다 ![2][2] 사이드바 왼쪽 메뉴에서 다음 hello ExpressRoute 회로 hello에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-186">In hello Azure portal, status of an ExpressRoute circuit can be checked by selecting ![2][2] on hello left-side-bar menu and then selecting hello ExpressRoute circuit.</span></span> <span data-ttu-id="41bd6-187">Express 경로 선택 하면 "모든 리소스" 아래에 나열 하는 회로 hello ExpressRoute 회로 블레이드를 점 열립니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-187">Selecting an ExpressRoute circuit listed under "All resources" would open hello ExpressRoute circuit blade.</span></span> <span data-ttu-id="41bd6-188">Hello에 ![3][3] hello 블레이드에서 hello essentials는 hello 스크린 샷 뒤에 표시 된 대로 표시 되는 ExpressRoute의 섹션:</span><span class="sxs-lookup"><span data-stu-id="41bd6-188">In hello ![3][3] section of hello blade, hello ExpressRoute essentials would be listed as shown in hello following screen shot:</span></span>

<span data-ttu-id="41bd6-189">![5][5]</span><span class="sxs-lookup"><span data-stu-id="41bd6-189">![5][5]</span></span>

<span data-ttu-id="41bd6-190">앞 예제는 hello에 명시 된 Azure로 개인 피어 링 라우팅 컨텍스트를 사용할 수, 공용 Azure 및 Microsoft 피어 링 라우팅 컨텍스트를 사용할 수 있지만 합니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-190">In hello preceding example, as noted Azure private peering routing context is enabled, whereas Azure public and Microsoft peering routing contexts are not enabled.</span></span> <span data-ttu-id="41bd6-191">성공적으로 활성화 된 피어 링 컨텍스트 hello (BGP에 필요) 하는 기본 및 보조 지점 간 서브넷 나열 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-191">A successfully enabled peering context would also have hello primary and secondary point-to-point (required for BGP) subnets listed.</span></span> <span data-ttu-id="41bd6-192">hello/30 서브넷의 hello MSEEs hello 인터페이스 IP 주소 및 PE MSEEs에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-192">hello /30 subnets are used for hello interface IP address of hello MSEEs and PE-MSEEs.</span></span> 

>[!NOTE]
><span data-ttu-id="41bd6-193">피어 링을 사용 하지 않는 경우 할당 된 hello 기본 및 보조 서브넷와 일치 하는 경우 확인 PE MSEEs에 hello 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-193">If a peering is not enabled, check if hello primary and secondary subnets assigned match hello configuration on PE-MSEEs.</span></span> <span data-ttu-id="41bd6-194">하는 경우 not, toochange hello 구성 MSEE 라우터에서 너무 참조[만들기 및 수정 ExpressRoute 회로 대 한 라우팅][CreatePeering]</span><span class="sxs-lookup"><span data-stu-id="41bd6-194">If not, toochange hello configuration on MSEE routers, refer too[Create and modify routing for an ExpressRoute circuit][CreatePeering]</span></span>
>
>

###<a name="verification-via-powershell"></a><span data-ttu-id="41bd6-195">PowerShell을 통한 확인</span><span class="sxs-lookup"><span data-stu-id="41bd6-195">Verification via PowerShell</span></span>
<span data-ttu-id="41bd6-196">tooget hello 개인 Azure hello 다음 명령을 사용 하 여 구성 세부 정보를 피어 링:</span><span class="sxs-lookup"><span data-stu-id="41bd6-196">tooget hello Azure private peering configuration details, use hello following commands:</span></span>

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -Circuit $ckt

<span data-ttu-id="41bd6-197">성공적으로 구성된 개인 피어링에 대한 샘플 응답은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-197">A sample response, for a successfully configured private peering, is:</span></span>

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

 <span data-ttu-id="41bd6-198">성공적으로 활성화 된 피어 링 컨텍스트 hello 기본 및 보조 주소 접두사를 나열 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-198">A successfully enabled peering context would have hello primary and secondary address prefixes listed.</span></span> <span data-ttu-id="41bd6-199">hello/30 서브넷의 hello MSEEs hello 인터페이스 IP 주소 및 PE MSEEs에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-199">hello /30 subnets are used for hello interface IP address of hello MSEEs and PE-MSEEs.</span></span>

<span data-ttu-id="41bd6-200">tooget hello Azure 공용 구성 세부 정보를 피어 링 명령 뒤 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-200">tooget hello Azure public peering configuration details, use hello following commands:</span></span>

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -Circuit $ckt

<span data-ttu-id="41bd6-201">tooget hello 한 Microsoft 피어 링 구성 세부 정보를 다음 명령 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-201">tooget hello Microsoft peering configuration details, use hello following commands:</span></span>

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -Circuit $ckt

<span data-ttu-id="41bd6-202">피어링이 구성되어 있지 않으면 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-202">If a peering is not configured, there would be an error message.</span></span> <span data-ttu-id="41bd6-203">Hello 피어 링 (Azure 공용이 예에서 피어 링) 될 때 샘플 응답 hello 회로 내의 구성 되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-203">A sample response, when hello stated peering (Azure Public peering in this example) is not configured within hello circuit:</span></span>

    Get-AzureRmExpressRouteCircuitPeeringConfig : Sequence contains no matching element
    At line:1 char:1
        + Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering ...
        + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
            + CategoryInfo          : CloseError: (:) [Get-AzureRmExpr...itPeeringConfig], InvalidOperationException
            + FullyQualifiedErrorId : Microsoft.Azure.Commands.Network.GetAzureExpressRouteCircuitPeeringConfigCommand


<p/>
>[!NOTE]
><span data-ttu-id="41bd6-204">피어 링을 사용 하지 않는 경우에 PE MSEE hello hello에 할당 된 기본 및 보조 서브넷 일치 hello 구성에 연결 된 경우를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-204">If a peering is not enabled, check if hello primary and secondary subnets assigned match hello configuration on hello linked PE-MSEE.</span></span> <span data-ttu-id="41bd6-205">있는지 확인 합니다. hello 올바른 *VlanId*, *AzureASN*, 및 *PeerASN* MSEEs에서 사용 되 고 이러한 값 매핑되 toohello hello에는 데 사용 되는 경우 PE MSEE 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-205">Also check if hello correct *VlanId*, *AzureASN*, and *PeerASN* are used on MSEEs and if these values maps toohello ones used on hello linked PE-MSEE.</span></span> <span data-ttu-id="41bd6-206">MD5 해시를 선택한 경우 공유 키 hello MSEE 및 PE MSEE 쌍에서 동일 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-206">If MD5 hashing is chosen, hello shared key should be same on MSEE and PE-MSEE pair.</span></span> <span data-ttu-id="41bd6-207">hello MSEE 라우터에서 toochange hello 구성 참조 너무 [만들기 및 수정 ExpressRoute 회로 대 한 라우팅] [CreatePeering].</span><span class="sxs-lookup"><span data-stu-id="41bd6-207">toochange hello configuration on hello MSEE routers, refer too[Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>  
>
>

### <a name="verification-via-powershell-classic"></a><span data-ttu-id="41bd6-208">PowerShell(클래식)을 통한 확인</span><span class="sxs-lookup"><span data-stu-id="41bd6-208">Verification via PowerShell (Classic)</span></span>
<span data-ttu-id="41bd6-209">tooget hello 개인 Azure hello 다음 명령을 사용 하 여 구성 세부 정보를 피어 링:</span><span class="sxs-lookup"><span data-stu-id="41bd6-209">tooget hello Azure private peering configuration details, use hello following command:</span></span>

    Get-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"

<span data-ttu-id="41bd6-210">성공적으로 구성된 개인 피어링에 대한 샘플 응답은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-210">A sample response, for a successfully configured private peering is:</span></span>

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

<span data-ttu-id="41bd6-211">A가 성공적으로 활성화 피어 링 상황에 맞는 나열 된 hello 기본 및 보조 피어 서브넷이 있는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-211">A successfully, enabled peering context would have hello primary and secondary peer subnets listed.</span></span> <span data-ttu-id="41bd6-212">hello/30 서브넷의 hello MSEEs hello 인터페이스 IP 주소 및 PE MSEEs에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-212">hello /30 subnets are used for hello interface IP address of hello MSEEs and PE-MSEEs.</span></span>

<span data-ttu-id="41bd6-213">tooget hello Azure 공용 구성 세부 정보를 피어 링 명령 뒤 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-213">tooget hello Azure public peering configuration details, use hello following commands:</span></span>

    Get-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

<span data-ttu-id="41bd6-214">tooget hello 한 Microsoft 피어 링 구성 세부 정보를 다음 명령 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-214">tooget hello Microsoft peering configuration details, use hello following commands:</span></span>

    Get-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

>[!IMPORTANT]
><span data-ttu-id="41bd6-215">3 계층 피어 링 hello 서비스 공급자가로 설정 된 hello 포털 또는 PowerShell을 통해 hello express 경로 피어 링 설정 hello 서비스 공급자 설정을 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-215">If layer 3 peerings were set by hello service provider, setting hello ExpressRoute peerings via hello portal or PowerShell overwrites hello service provider settings.</span></span> <span data-ttu-id="41bd6-216">Hello 서비스 공급자의 hello 지원이 필요 hello 공급자 측에 대 한 피어 링 설정을 다시 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-216">Resetting hello provider side peering settings requires hello support of hello service provider.</span></span> <span data-ttu-id="41bd6-217">것이 확실 hello 서비스 공급자에는 계층 2 서비스에만 제공 하는 경우에 hello express 경로 피어 링을 수정!</span><span class="sxs-lookup"><span data-stu-id="41bd6-217">Only modify hello ExpressRoute peerings if it is certain that hello service provider is providing layer 2 services only!</span></span>
>
>

<p/>
>[!NOTE]
><span data-ttu-id="41bd6-218">피어 링을 사용 하지 않는 경우에 PE MSEE hello에 hello 기본 및 보조 피어 서브넷 할당 일치 hello 구성에 연결 된 경우를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-218">If a peering is not enabled, check if hello primary and secondary peer subnets assigned match hello configuration on hello linked PE-MSEE.</span></span> <span data-ttu-id="41bd6-219">있는지 확인 합니다. hello 올바른 *VlanId*, *AzureAsn*, 및 *PeerAsn* MSEEs에서 사용 되 고 이러한 값 매핑되 toohello hello에는 데 사용 되는 경우 PE MSEE 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-219">Also check if hello correct *VlanId*, *AzureAsn*, and *PeerAsn* are used on MSEEs and if these values maps toohello ones used on hello linked PE-MSEE.</span></span> <span data-ttu-id="41bd6-220">hello MSEE 라우터에서 toochange hello 구성 참조 너무 [만들기 및 수정 ExpressRoute 회로 대 한 라우팅] [CreatePeering].</span><span class="sxs-lookup"><span data-stu-id="41bd6-220">toochange hello configuration on hello MSEE routers, refer too[Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>
>
>

## <a name="validate-arp-between-microsoft-and-hello-service-provider"></a><span data-ttu-id="41bd6-221">Microsoft 및 hello 서비스 공급자 간의 ARP 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="41bd6-221">Validate ARP between Microsoft and hello service provider</span></span>
<span data-ttu-id="41bd6-222">이 섹션에서는 PowerShell(클래식) 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-222">This section uses PowerShell (Classic) commands.</span></span> <span data-ttu-id="41bd6-223">Azure 리소스 관리자 PowerShell 명령을 사용 하는 경우 확인을 통해 관리자/공동 관리자 액세스 toohello 구독이 있는지 [Azure 클래식 포털][OldPortal]합니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-223">If you have been using PowerShell Azure Resource Manager commands, ensure that you have admin/co-admin access toohello subscription via [Azure classic portal][OldPortal].</span></span> <span data-ttu-id="41bd6-224">Azure 리소스 관리자를 사용 하 여 문제 해결에 대 한 명령을 참조 하십시오 toohello [hello 리소스 관리자 배포 모델에서 가져오기 ARP 테이블] [ ARP] 문서.</span><span class="sxs-lookup"><span data-stu-id="41bd6-224">For troubleshooting using Azure Resource Manager commands please refer toohello [Getting ARP tables in hello Resource Manager deployment model][ARP] document.</span></span>

>[!NOTE]
><span data-ttu-id="41bd6-225">tooget ARP를 hello Azure 포털 및 Azure 리소스 관리자 PowerShell 명령을 둘 다 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-225">tooget ARP, both hello Azure portal and Azure Resource Manager PowerShell commands can be used.</span></span> <span data-ttu-id="41bd6-226">Hello Azure 리소스 관리자 PowerShell 명령을 사용 하 여 오류가 발생 하는 경우 클래식 PowerShell 명령의 명령을 Azure 리소스 관리자 ExpressRoute 회로를 사용할 수도 클래식 PowerShell로 작동 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-226">If errors are encountered with hello Azure Resource Manager PowerShell commands, classic PowerShell commands should work as Classic PowerShell commands also work with Azure Resource Manager ExpressRoute circuits.</span></span>
>
>

<span data-ttu-id="41bd6-227">tooget hello hello hello 개인 피어 링에 대 한 기본 MSEE 라우터의 ARP 테이블, 다음 명령을 hello를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="41bd6-227">tooget hello ARP table from hello primary MSEE router for hello private peering, use hello following command:</span></span>

    Get-AzureDedicatedCircuitPeeringArpInfo -AccessType Private -Path Primary -ServiceKey "*********************************"

<span data-ttu-id="41bd6-228">성공 시나리오 hello hello 명령에 대 한 예제 응답:</span><span class="sxs-lookup"><span data-stu-id="41bd6-228">An example response for hello command, in hello successful scenario:</span></span>

    ARP Info:

                 Age           Interface           IpAddress          MacAddress
                 113             On-Prem       10.0.0.1           e8ed.f335.4ca9
                   0           Microsoft       10.0.0.2           7c0e.ce85.4fc9

<span data-ttu-id="41bd6-229">마찬가지로, hello ARP 테이블 hello에 MSEE hello에서 확인할 수 있습니다 *기본*/*보조* 경로 대 한 *개인* /  *공용*/*Microsoft* 피어 링입니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-229">Similarly, you can check hello ARP table from hello MSEE in hello *Primary*/*Secondary* path, for *Private*/*Public*/*Microsoft* peerings.</span></span>

<span data-ttu-id="41bd6-230">hello 다음 예제에서는 피어 링에 대 한 hello 명령의 응답 hello 존재 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-230">hello following example shows hello response of hello command for a peering does not exist.</span></span>

    ARP Info:
       
>[!NOTE]
><span data-ttu-id="41bd6-231">Hello ARP 테이블에 없는 경우 다음 정보 검토 hello tooMAC 주소 hello 인터페이스의 IP 주소에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-231">If hello ARP table does not have IP addresses of hello interfaces mapped tooMAC addresses, review hello following information:</span></span>
>1. <span data-ttu-id="41bd6-232">Hello hello/30 서브넷의 첫 번째 IP 주소 간의 hello 링크에 대 한 할당 된 경우 hello MSEE PR 및 MSEE MSEE 프로의 hello 인터페이스에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-232">If hello first IP address of hello /30 subnet assigned for hello link between hello MSEE-PR and MSEE is used on hello interface of MSEE-PR.</span></span> <span data-ttu-id="41bd6-233">Azure는 항상 MSEEs에 대 한 hello 두 번째 IP 주소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-233">Azure always uses hello second IP address for MSEEs.</span></span>
>2. <span data-ttu-id="41bd6-234">Hello 고객 (C 태그)와 서비스 (S 태그) VLAN 태그 일치 모두 MSEE PR 및 MSEE 쌍에서 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="41bd6-234">Verify if hello customer (C-Tag) and service (S-Tag) VLAN tags match both on MSEE-PR and MSEE pair.</span></span>
>
>

## <a name="validate-bgp-and-routes-on-hello-msee"></a><span data-ttu-id="41bd6-235">BGP 및 hello MSEE에서 경로 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="41bd6-235">Validate BGP and routes on hello MSEE</span></span>
<span data-ttu-id="41bd6-236">이 섹션에서는 PowerShell(클래식) 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-236">This section uses PowerShell (Classic) commands.</span></span> <span data-ttu-id="41bd6-237">Azure 리소스 관리자 PowerShell 명령을 사용 하는 경우 확인을 통해 관리자/공동 관리자 액세스 toohello 구독이 있는지 [Azure 클래식 포털][OldPortal]</span><span class="sxs-lookup"><span data-stu-id="41bd6-237">If you have been using PowerShell Azure Resource Manager commands, ensure that you have admin/co-admin access toohello subscription via [Azure classic portal][OldPortal]</span></span>

>[!NOTE]
><span data-ttu-id="41bd6-238">tooget BGP 정보를 모두 hello Azure 포털 및 Azure 리소스 관리자 PowerShell 명령을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-238">tooget BGP information, both hello Azure portal and Azure Resource Manager PowerShell commands can be used.</span></span> <span data-ttu-id="41bd6-239">Hello Azure 리소스 관리자 PowerShell 명령을 사용 하 여 오류가 발생 하는 경우 클래식 PowerShell 명령의 명령을 Azure 리소스 관리자 ExpressRoute 회로를 사용할 수도 클래식 PowerShell로 작동 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-239">If errors are encountered with hello Azure Resource Manager PowerShell commands, classic PowerShell commands should work as classic PowerShell commands also work with Azure Resource Manager ExpressRoute circuits.</span></span>
>
>

<span data-ttu-id="41bd6-240">tooget hello 라우팅 테이블 (BGP 인접 한 항목)는 특정 라우팅 컨텍스트에 대 한 요약, hello 다음 명령을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="41bd6-240">tooget hello routing table (BGP neighbor) summary for a particular routing context, use hello following command:</span></span>

    Get-AzureDedicatedCircuitPeeringRouteTableSummary -AccessType Private -Path Primary -ServiceKey "*********************************"

<span data-ttu-id="41bd6-241">예제 응답은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-241">An example response is:</span></span>

    Route Table Summary:

            Neighbor                   V                  AS              UpDown         StatePfxRcd
            10.0.0.1                   4                ####                8w4d                  50

<span data-ttu-id="41bd6-242">Hello 이전 예제와 같이 hello 명령 hello 라우팅 컨텍스트가 설정 기간에 대 한 유용한 toodetermine입니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-242">As shown in hello preceding example, hello command is useful toodetermine for how long hello routing context has been established.</span></span> <span data-ttu-id="41bd6-243">또한 hello 피어 링 라우터에서 보급 된 경로 접두사의 수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-243">It also indicates number of route prefixes advertised by hello peering router.</span></span>

>[!NOTE]
><span data-ttu-id="41bd6-244">Hello 상태 이면 정상 또는 유휴 hello에 hello 기본 및 보조 피어 서브넷 할당 일치 hello 구성 PE MSEE 하는 경우 연결을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-244">If hello state is in Active or Idle, check if hello primary and secondary peer subnets assigned match hello configuration on hello linked PE-MSEE.</span></span> <span data-ttu-id="41bd6-245">있는지 확인 합니다. hello 올바른 *VlanId*, *AzureAsn*, 및 *PeerAsn* MSEEs에서 사용 되 고 이러한 값 매핑되 toohello hello에는 데 사용 되는 경우 PE MSEE 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-245">Also check if hello correct *VlanId*, *AzureAsn*, and *PeerAsn* are used on MSEEs and if these values maps toohello ones used on hello linked PE-MSEE.</span></span> <span data-ttu-id="41bd6-246">MD5 해시를 선택한 경우 공유 키 hello MSEE 및 PE MSEE 쌍에서 동일 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-246">If MD5 hashing is chosen, hello shared key should be same on MSEE and PE-MSEE pair.</span></span> <span data-ttu-id="41bd6-247">hello MSEE 라우터에서 toochange hello 구성 참조 너무[만들기 및 수정 ExpressRoute 회로 대 한 라우팅][CreatePeering]합니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-247">toochange hello configuration on hello MSEE routers, refer too[Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>
>
>

<p/>
>[!NOTE]
><span data-ttu-id="41bd6-248">특정 피어 링을 통해 특정 대상을 연결할 수 없는 경우 toohello 특정 피어 링 컨텍스트에 속하는 hello MSEEs의 hello 경로 테이블을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-248">If certain destinations are not reachable over a particular peering, check hello route table of hello MSEEs belonging toohello particular peering context.</span></span> <span data-ttu-id="41bd6-249">일치 하는 접두사 (NATed IP 수 있음)가 hello 라우팅 테이블에 있는 경우에 hello 경로에 방화벽/NSG Acl이 있는 경우 고 hello 트래픽을 허용 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-249">If a matching prefix (could be NATed IP) is present in hello routing table, then check if there are firewalls/NSG/ACLs on hello path and if they permit hello traffic.</span></span>
>
>

<span data-ttu-id="41bd6-250">tooget hello 전체 라우팅 테이블에서 MSEE hello *기본* 특정 hello에 대 한 경로 *개인* 라우팅 컨텍스트, 다음 명령을 사용 하 여 hello:</span><span class="sxs-lookup"><span data-stu-id="41bd6-250">tooget hello full routing table from MSEE on hello *Primary* path for hello particular *Private* routing context, use hello following command:</span></span>

    Get-AzureDedicatedCircuitPeeringRouteTableInfo -AccessType Private -Path Primary -ServiceKey "*********************************"

<span data-ttu-id="41bd6-251">다음은 hello 명령에 대 한 예제 성공적인 결과가입니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-251">An example successful outcome for hello command is:</span></span>

    Route Table Info:

             Network             NextHop              LocPrf              Weight                Path
         10.1.0.0/16            10.0.0.1                                       0    #### ##### #####     
         10.2.0.0/16            10.0.0.1                                       0    #### ##### #####
    ...

<span data-ttu-id="41bd6-252">마찬가지로, hello hello에 MSEE hello에서 라우팅 테이블을 확인할 수 있습니다 *기본*/*보조* 경로 대 한 *개인* / *공용*/*Microsoft* 피어 링 컨텍스트.</span><span class="sxs-lookup"><span data-stu-id="41bd6-252">Similarly, you can check hello routing table from hello MSEE in hello *Primary*/*Secondary* path, for *Private*/*Public*/*Microsoft* a peering context.</span></span>

<span data-ttu-id="41bd6-253">hello 다음 예제에서는 피어 링에 대 한 hello 명령의 응답 hello 없습니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-253">hello following example shows hello response of hello command for a peering does not exist:</span></span>

    Route Table Info:

##<a name="check-hello-traffic-statistics"></a><span data-ttu-id="41bd6-254">Hello 트래픽 통계를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-254">Check hello Traffic Statistics</span></span>
<span data-ttu-id="41bd6-255">tooget hello에 따라 다음 명령을 사용 하 여 hello 피어 링 컨텍스트의 기본 및 보조 경로 트래픽 통계-바이트 결합 하는 및 축소.</span><span class="sxs-lookup"><span data-stu-id="41bd6-255">tooget hello combined primary and secondary path traffic statistics--bytes in and out--of a peering context, use hello following command:</span></span>

    Get-AzureDedicatedCircuitStats -ServiceKey 97f85950-01dd-4d30-a73c-bf683b3a6e5c -AccessType Private

<span data-ttu-id="41bd6-256">Hello 명령의 예제 출력은입니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-256">A sample output of hello command is:</span></span>

    PrimaryBytesIn PrimaryBytesOut SecondaryBytesIn SecondaryBytesOut
    -------------- --------------- ---------------- -----------------
         240780020       239863857        240565035         239628474

<span data-ttu-id="41bd6-257">존재 하지 않는 피어 링에 대 한 hello 명령의 예제 출력은입니다.</span><span class="sxs-lookup"><span data-stu-id="41bd6-257">A sample output of hello command for a non-existent peering is:</span></span>

    Get-AzureDedicatedCircuitStats : ResourceNotFound: Can not find any subinterface for peering type 'Public' for circuit '97f85950-01dd-4d30-a73c-bf683b3a6e5c' .
    At line:1 char:1
    + Get-AzureDedicatedCircuitStats -ServiceKey 97f85950-01dd-4d30-a73c-bf ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : CloseError: (:) [Get-AzureDedicatedCircuitStats], CloudException
        + FullyQualifiedErrorId : Microsoft.WindowsAzure.Commands.ExpressRoute.GetAzureDedicatedCircuitPeeringStatsCommand

## <a name="next-steps"></a><span data-ttu-id="41bd6-258">다음 단계</span><span class="sxs-lookup"><span data-stu-id="41bd6-258">Next Steps</span></span>
<span data-ttu-id="41bd6-259">자세한 정보나 도움말에 대 한 링크를 따라 hello 확인해 보세요.</span><span class="sxs-lookup"><span data-stu-id="41bd6-259">For more information or help, check out hello following links:</span></span>

- <span data-ttu-id="41bd6-260">[Microsoft 지원][Support]</span><span class="sxs-lookup"><span data-stu-id="41bd6-260">[Microsoft Support][Support]</span></span>
- <span data-ttu-id="41bd6-261">[ExpressRoute 회로 만들기 및 수정][CreateCircuit]</span><span class="sxs-lookup"><span data-stu-id="41bd6-261">[Create and modify an ExpressRoute circuit][CreateCircuit]</span></span>
- <span data-ttu-id="41bd6-262">[ExpressRoute 회로의 라우팅 만들기 및 수정][CreatePeering]</span><span class="sxs-lookup"><span data-stu-id="41bd6-262">[Create and modify routing for an ExpressRoute circuit][CreatePeering]</span></span>

<!--Image References-->
[1]: ./media/expressroute-troubleshooting-expressroute-overview/expressroute-logical-diagram.png "논리 ExpressRoute 연결"
[2]: ./media/expressroute-troubleshooting-expressroute-overview/portal-all-resources.png "모든 리소스 아이콘"
[3]: ./media/expressroute-troubleshooting-expressroute-overview/portal-overview.png "개요 아이콘"
[4]: ./media/expressroute-troubleshooting-expressroute-overview/portal-circuit-status.png "ExpressRoute Essentials 샘플 스크린샷"
[5]: ./media/expressroute-troubleshooting-expressroute-overview/portal-private-peering.png "ExpressRoute Essentials 샘플 스크린샷"

<!--Link References-->
[Support]: https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[CreateCircuit]: https://docs.microsoft.com/azure/expressroute/expressroute-howto-circuit-portal-resource-manager 
[CreatePeering]: https://docs.microsoft.com/azure/expressroute/expressroute-howto-routing-portal-resource-manager
[OldPortal]: https://manage.windowsazure.com
[ARP]: https://docs.microsoft.com/en-us/azure/expressroute/expressroute-troubleshooting-arp-resource-manager







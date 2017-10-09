---
title: "express 경로 FAQ aaaAzure | Microsoft Docs"
description: "express 경로 FAQ hello Azure 서비스 지원, 비용, 데이터 및 연결, SLA, 공급자 및 위치, 대역폭 및 추가 기술 세부 정보에 대 한 정보를 포함합니다."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
ms.assetid: 09b17bc4-d0b3-4ab0-8c14-eed730e1446e
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: c01e83f1497103e2fa85251dce6fb41844e46e9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-faq"></a><span data-ttu-id="2bc47-103">ExpressRoute FAQ</span><span class="sxs-lookup"><span data-stu-id="2bc47-103">ExpressRoute FAQ</span></span>

## <a name="what-is-expressroute"></a><span data-ttu-id="2bc47-104">ExpressRoute란?</span><span class="sxs-lookup"><span data-stu-id="2bc47-104">What is ExpressRoute?</span></span>

<span data-ttu-id="2bc47-105">ExpressRoute는 온-프레미스 또는 공동 장소 환경의 Microsoft 데이터 센터와 인프라 사이에 개인 연결을 만들 수 있게 해 주는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-105">ExpressRoute is an Azure service that lets you create private connections between Microsoft datacenters and infrastructure that’s on your premises or in a colocation facility.</span></span> <span data-ttu-id="2bc47-106">ExpressRoute 연결은 공용 인터넷 및 보안을 강화 하는 제품 신뢰성 hello 보다 내려가지 않는지, 속도와 일반 연결 보다 대기 시간이 hello 인터넷을 통해입니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-106">ExpressRoute connections do not go over hello public Internet, and offer higher security, reliability, and speeds with lower latencies than typical connections over hello Internet.</span></span>

### <a name="what-are-hello-benefits-of-using-expressroute-and-private-network-connections"></a><span data-ttu-id="2bc47-107">ExpressRoute 및 개인 네트워크 연결을 사용 하 여 hello 장점은 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="2bc47-107">What are hello benefits of using ExpressRoute and private network connections?</span></span>

<span data-ttu-id="2bc47-108">ExpressRoute 연결은 hello를 통해 이동 하지 않도록 공용 인터넷 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-108">ExpressRoute connections do not go over hello public Internet.</span></span> <span data-ttu-id="2bc47-109">보안, 안정성 및 속도 일관 된 대기 시간이 hello 인터넷을 통한 일반 연결 보다 더 높은 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-109">They offer higher security, reliability, and speeds, with lower and consistent latencies than typical connections over hello Internet.</span></span> <span data-ttu-id="2bc47-110">경우에 따라 간에 ExpressRoute 연결 tootransfer 데이터를 사용 하 여 온-프레미스 장치 및 Azure 상당한 비용 혜택을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-110">In some cases, using ExpressRoute connections tootransfer data between on-premises devices and Azure can yield significant cost benefits.</span></span>

### <a name="where-is-hello-service-available"></a><span data-ttu-id="2bc47-111">Hello 서비스는 사용할 수 있는 어디 입니까?</span><span class="sxs-lookup"><span data-stu-id="2bc47-111">Where is hello service available?</span></span>

<span data-ttu-id="2bc47-112">서비스 위치 및 가용성은 [ExpressRoute 파트너 및 위치](expressroute-locations.md)페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2bc47-112">See this page for service location and availability: [ExpressRoute partners and locations](expressroute-locations.md).</span></span>

### <a name="how-can-i-use-expressroute-tooconnect-toomicrosoft-if-i-dont-have-partnerships-with-one-of-hello-expressroute-carrier-partners"></a><span data-ttu-id="2bc47-113">Hello ExpressRoute 통신 업체 중 하 나와 파트너 관계 없는 경우 tooconnect tooMicrosoft ExpressRoute를 사용 하는 방법</span><span class="sxs-lookup"><span data-stu-id="2bc47-113">How can I use ExpressRoute tooconnect tooMicrosoft if I don’t have partnerships with one of hello ExpressRoute-carrier partners?</span></span>

<span data-ttu-id="2bc47-114">지역 통신 업체를 선택할 수 있으며 이더넷 연결 tooone 지원 hello exchange 공급자 위치를 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-114">You can select a regional carrier and land Ethernet connections tooone of hello supported exchange provider locations.</span></span> <span data-ttu-id="2bc47-115">그러면 hello 공급자 위치에서 microsoft 피어 링 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-115">You can then peer with Microsoft at hello provider location.</span></span> <span data-ttu-id="2bc47-116">마지막 부분 hello [express 경로 파트너 및 위치](expressroute-locations.md) toosee 서비스 공급자 hello exchange 위치 중 하나에 있는 경우.</span><span class="sxs-lookup"><span data-stu-id="2bc47-116">Check hello last section of [ExpressRoute partners and locations](expressroute-locations.md) toosee if your service provider is present in any of hello exchange locations.</span></span> <span data-ttu-id="2bc47-117">그런 다음 서비스 공급자 tooconnect tooAzure hello 통해 ExpressRoute 회로 주문할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-117">You can then order an ExpressRoute circuit through hello service provider tooconnect tooAzure.</span></span>

### <a name="how-much-does-expressroute-cost"></a><span data-ttu-id="2bc47-118">Express 경로 비용</span><span class="sxs-lookup"><span data-stu-id="2bc47-118">How much does ExpressRoute cost?</span></span>

<span data-ttu-id="2bc47-119">가격 정보는 [가격 정보](https://azure.microsoft.com/pricing/details/expressroute/) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2bc47-119">Check [pricing details](https://azure.microsoft.com/pricing/details/expressroute/) for pricing information.</span></span>

### <a name="if-i-pay-for-an-expressroute-circuit-of-a-given-bandwidth-does-hello-vpn-connection-i-purchase-from-my-network-service-provider-have-toobe-hello-same-speed"></a><span data-ttu-id="2bc47-120">가 지정된 된 대역폭의 ExpressRoute 회로 내 네트워크 서비스 공급자 로부터 구매 하는 VPN 연결을 hello에 대 한 비용을 지불할 경우 toobe hello 동일한 속도?</span><span class="sxs-lookup"><span data-stu-id="2bc47-120">If I pay for an ExpressRoute circuit of a given bandwidth, does hello VPN connection I purchase from my network service provider have toobe hello same speed?</span></span>

<span data-ttu-id="2bc47-121">아니요.</span><span class="sxs-lookup"><span data-stu-id="2bc47-121">No.</span></span> <span data-ttu-id="2bc47-122">서비스 공급자로부터 모든 속도의 VPN 연결을 구입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-122">You can purchase a VPN connection of any speed from your service provider.</span></span> <span data-ttu-id="2bc47-123">그러나 연결 tooAzure 제한 toohello ExpressRoute 회로 대역폭을 구입할 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-123">However, your connection tooAzure is limited toohello ExpressRoute circuit bandwidth that you purchase.</span></span>

### <a name="if-i-pay-for-an-expressroute-circuit-of-a-given-bandwidth-do-i-have-hello-ability-tooburst-up-toohigher-speeds-if-necessary"></a><span data-ttu-id="2bc47-124">비용을 지불할 경우 지정된 된 대역폭의 ExpressRoute 회로 필요에 따라 toohigher 속도를 hello 기능 tooburst 있습니까?</span><span class="sxs-lookup"><span data-stu-id="2bc47-124">If I pay for an ExpressRoute circuit of a given bandwidth, do I have hello ability tooburst up toohigher speeds if necessary?</span></span>

<span data-ttu-id="2bc47-125">예.</span><span class="sxs-lookup"><span data-stu-id="2bc47-125">Yes.</span></span> <span data-ttu-id="2bc47-126">ExpressRoute 회로 구성 된 tooallow tootwo 시간 tooburst hello에 대 한 추가 비용 없이 확보 하는 대역폭 제한입니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-126">ExpressRoute circuits are configured tooallow you tooburst up tootwo times hello bandwidth limit you procured for no additional cost.</span></span> <span data-ttu-id="2bc47-127">이 기능을 지원 하는 경우 서비스 공급자 toosee 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="2bc47-127">Check with your service provider toosee if they support this capability.</span></span>

### <a name="can-i-use-hello-same-private-network-connection-with-virtual-network-and-other-azure-services-simultaneously"></a><span data-ttu-id="2bc47-128">사용할 수 있습니까 hello 동일한 개인 가상 네트워크 및 기타 Azure 서비스와의 연결을 동시에 네트워크?</span><span class="sxs-lookup"><span data-stu-id="2bc47-128">Can I use hello same private network connection with virtual network and other Azure services simultaneously?</span></span>

<span data-ttu-id="2bc47-129">예.</span><span class="sxs-lookup"><span data-stu-id="2bc47-129">Yes.</span></span> <span data-ttu-id="2bc47-130">ExpressRoute 회로 한 번 설정 하면 가상 네트워크 내에서 tooaccess 서비스 및 다른 Azure 서비스가 동시에.</span><span class="sxs-lookup"><span data-stu-id="2bc47-130">An ExpressRoute circuit, once set up, allows you tooaccess services within a virtual network and other Azure services simultaneously.</span></span> <span data-ttu-id="2bc47-131">개인 피어 링 경로 hello 및 tooother 서비스를 통해 hello 공용 피어 링 경로 통해 toovirtual 네트워크를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-131">You connect toovirtual networks over hello private peering path, and tooother services over hello public peering path.</span></span>

### <a name="does-expressroute-offer-a-service-level-agreement-sla"></a><span data-ttu-id="2bc47-132">ExpressRoute는 SLA(서비스 수준 계약)을 제공하나요?</span><span class="sxs-lookup"><span data-stu-id="2bc47-132">Does ExpressRoute offer a Service Level Agreement (SLA)?</span></span>

<span data-ttu-id="2bc47-133">내용은 hello를 참조 하십시오. [ExpressRoute SLA](https://azure.microsoft.com/support/legal/sla/) 페이지.</span><span class="sxs-lookup"><span data-stu-id="2bc47-133">For information, see hello [ExpressRoute SLA](https://azure.microsoft.com/support/legal/sla/) page.</span></span>

## <a name="supported-services"></a><span data-ttu-id="2bc47-134">지원되는 서비스</span><span class="sxs-lookup"><span data-stu-id="2bc47-134">Supported services</span></span>

<span data-ttu-id="2bc47-135">ExpressRoute는 다양한 유형의 서비스에 대해 [세 개의 라우팅 도메인](expressroute-circuit-peerings.md)을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-135">ExpressRoute supports [three routing domains](expressroute-circuit-peerings.md) for various types of services.</span></span>

### <a name="private-peering"></a><span data-ttu-id="2bc47-136">개인 피어링</span><span class="sxs-lookup"><span data-stu-id="2bc47-136">Private peering</span></span>

* <span data-ttu-id="2bc47-137">모든 가상 컴퓨터 및 클라우드 서비스를 포함한 가상 네트워크</span><span class="sxs-lookup"><span data-stu-id="2bc47-137">Virtual networks, including all virtual machines and cloud services</span></span>

### <a name="public-peering"></a><span data-ttu-id="2bc47-138">공용 피어링</span><span class="sxs-lookup"><span data-stu-id="2bc47-138">Public peering</span></span>

* <span data-ttu-id="2bc47-139">Power BI</span><span class="sxs-lookup"><span data-stu-id="2bc47-139">Power BI</span></span>
* <span data-ttu-id="2bc47-140">Dynamics 365 for Finance and Operations(이전의 Dynamics AX Online)</span><span class="sxs-lookup"><span data-stu-id="2bc47-140">Dynamics 365 for Finance and Operations (formerly known as Dynamics AX Online)</span></span>
* <span data-ttu-id="2bc47-141">대부분 hello Azure의 hello 다음 몇 가지 예외를 사용 하 여 서비스:</span><span class="sxs-lookup"><span data-stu-id="2bc47-141">Most of hello Azure services, with hello following few exceptions:</span></span>
  * <span data-ttu-id="2bc47-142">CDN</span><span class="sxs-lookup"><span data-stu-id="2bc47-142">CDN</span></span>
  * <span data-ttu-id="2bc47-143">Visual Studio Team Services 부하 테스트</span><span class="sxs-lookup"><span data-stu-id="2bc47-143">Visual Studio Team Services Load Testing</span></span>
  * <span data-ttu-id="2bc47-144">Multi-Factor 인증</span><span class="sxs-lookup"><span data-stu-id="2bc47-144">Multi-factor Authentication</span></span>
  * <span data-ttu-id="2bc47-145">Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="2bc47-145">Traffic Manager</span></span>

### <a name="microsoft-peering"></a><span data-ttu-id="2bc47-146">Microsoft 피어링</span><span class="sxs-lookup"><span data-stu-id="2bc47-146">Microsoft peering</span></span>

* [<span data-ttu-id="2bc47-147">Office 365</span><span class="sxs-lookup"><span data-stu-id="2bc47-147">Office 365</span></span>](http://aka.ms/ExpressRouteOffice365)
* <span data-ttu-id="2bc47-148">Dynamics 365 Customer Engagement 응용 프로그램(이전의 CRM Online)</span><span class="sxs-lookup"><span data-stu-id="2bc47-148">Dynamics 365 Customer Engagement applications (formerly known as CRM Online)</span></span>
  * <span data-ttu-id="2bc47-149">Dynamics 365 for Sales</span><span class="sxs-lookup"><span data-stu-id="2bc47-149">Dynamics 365 for Sales</span></span>
  * <span data-ttu-id="2bc47-150">Dynamics 365 for Customer Service</span><span class="sxs-lookup"><span data-stu-id="2bc47-150">Dynamics 365 for Customer Service</span></span>
  * <span data-ttu-id="2bc47-151">Dynamics 365 for Field Service</span><span class="sxs-lookup"><span data-stu-id="2bc47-151">Dynamics 365 for Field Service</span></span>
  * <span data-ttu-id="2bc47-152">Dynamics 365 for Project Service</span><span class="sxs-lookup"><span data-stu-id="2bc47-152">Dynamics 365 for Project Service</span></span>

## <a name="data-and-connections"></a><span data-ttu-id="2bc47-153">데이터 및 연결</span><span class="sxs-lookup"><span data-stu-id="2bc47-153">Data and connections</span></span>

### <a name="are-there-limits-on-hello-amount-of-data-that-i-can-transfer-using-expressroute"></a><span data-ttu-id="2bc47-154">ExpressRoute를 사용 하 여 전송할 수 있습니까 하는 데이터 양 hello에 대 한 제한 사항이 있습니까?</span><span class="sxs-lookup"><span data-stu-id="2bc47-154">Are there limits on hello amount of data that I can transfer using ExpressRoute?</span></span>

<span data-ttu-id="2bc47-155">Hello 데이터 전송 양에 대 한 제한의 설정 하지 마십시오 했습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-155">We do not set a limit on hello amount of data transfer.</span></span> <span data-ttu-id="2bc47-156">너무 참조[가격 정보](https://azure.microsoft.com/pricing/details/expressroute/) 대역폭 속도에 대 한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-156">Refer too[pricing details](https://azure.microsoft.com/pricing/details/expressroute/) for information on bandwidth rates.</span></span>

### <a name="what-connection-speeds-are-supported-by-expressroute"></a><span data-ttu-id="2bc47-157">ExpressRoute에서 지원되는 연결 속도는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="2bc47-157">What connection speeds are supported by ExpressRoute?</span></span>

<span data-ttu-id="2bc47-158">지원되는 대역폭은 다음을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-158">Supported bandwidth offers:</span></span>

<span data-ttu-id="2bc47-159">50Mbps, 100Mbps, 200Mbps, 500Mbps, 1Gbps, 2Gbps, 5Gbps, 10Gbps</span><span class="sxs-lookup"><span data-stu-id="2bc47-159">50 Mbps, 100 Mbps, 200 Mbps, 500 Mbps, 1 Gbps, 2 Gbps, 5 Gbps, 10 Gbps</span></span>

### <a name="which-service-providers-are-available"></a><span data-ttu-id="2bc47-160">어떤 서비스 공급자를 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="2bc47-160">Which service providers are available?</span></span>

<span data-ttu-id="2bc47-161">참조 [express 경로 파트너 및 위치](expressroute-locations.md) hello 목록은 서비스 공급자 및 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-161">See [ExpressRoute partners and locations](expressroute-locations.md) for hello list of service providers and locations.</span></span>

## <a name="technical-details"></a><span data-ttu-id="2bc47-162">기술 세부 정보</span><span class="sxs-lookup"><span data-stu-id="2bc47-162">Technical details</span></span>

### <a name="what-are-hello-technical-requirements-for-connecting-my-on-premises-location-tooazure"></a><span data-ttu-id="2bc47-163">내 온-프레미스 위치 tooAzure 연결 하기 위한 hello 기술 요구 사항은 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="2bc47-163">What are hello technical requirements for connecting my on-premises location tooAzure?</span></span>

<span data-ttu-id="2bc47-164">요구 사항은 [ExpressRoute 필수 구성 요소 페이지](expressroute-prerequisites.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2bc47-164">See [ExpressRoute prerequisites page](expressroute-prerequisites.md) for requirements.</span></span>

### <a name="are-connections-tooexpressroute-redundant"></a><span data-ttu-id="2bc47-165">중복 연결 tooExpressRoute?</span><span class="sxs-lookup"><span data-stu-id="2bc47-165">Are connections tooExpressRoute redundant?</span></span>

<span data-ttu-id="2bc47-166">예.</span><span class="sxs-lookup"><span data-stu-id="2bc47-166">Yes.</span></span> <span data-ttu-id="2bc47-167">각 ExpressRoute 회로 구성 된 연결 tooprovide 고가용성 크로스 중복 쌍 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-167">Each ExpressRoute circuit has a redundant pair of cross connections configured tooprovide high availability.</span></span>

### <a name="will-i-lose-connectivity-if-one-of-my-expressroute-links-fail"></a><span data-ttu-id="2bc47-168">내 ExpressRoute 링크 중 하나가 실패하면 연결이 끊어지나요?</span><span class="sxs-lookup"><span data-stu-id="2bc47-168">Will I lose connectivity if one of my ExpressRoute links fail?</span></span>

<span data-ttu-id="2bc47-169">한 경우 연결이 손실 되지 것입니다의 hello 교차 연결 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-169">You will not lose connectivity if one of hello cross connections fails.</span></span> <span data-ttu-id="2bc47-170">네트워크의 사용 가능한 toosupport hello 부하 중복 연결이합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-170">A redundant connection is available toosupport hello load of your network.</span></span> <span data-ttu-id="2bc47-171">또한 다른 피어 링 위치 tooachieve 오류 복구에 여러 회로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-171">You can additionally create multiple circuits in a different peering location tooachieve failure resilience.</span></span>

### <span data-ttu-id="2bc47-172"><a name="onep2plink"></a>클라우드 교환에서 같은 위치에 배치 하지 않겠습니다 내 서비스 공급자 지점 간 연결을 제공 하는 경우 내 온-프레미스 네트워크와 Microsoft tooorder 두 개의 실제 연결 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="2bc47-172"><a name="onep2plink"></a>If I'm not co-located at a cloud exchange and my service provider offers point-to-point connection, do I need tooorder two physical connections between my on-premises network and Microsoft?</span></span>

<span data-ttu-id="2bc47-173">서비스 공급자를 설정 하려면 두 이더넷 가상 회로 hello 물리적 연결을 통해 경우 하나의 실제 연결을 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-173">If your service provider can establish two Ethernet virtual circuits over hello physical connection, you only need one physical connection.</span></span> <span data-ttu-id="2bc47-174">hello 물리적 연결 (예를 들어 광학 파이버)에서 종료 되는 계층 (L1) 장치 1 개 (hello 이미지 참조).</span><span class="sxs-lookup"><span data-stu-id="2bc47-174">hello physical connection (for example, an optical fiber) is terminated on a layer 1 (L1) device (see hello image).</span></span> <span data-ttu-id="2bc47-175">hello 2 이더넷 가상 회로 hello 기본 회로 대 한 서로 다른 VLAN Id로 태그가 지정 하 고 보조 hello에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-175">hello two Ethernet virtual circuits are tagged with different VLAN IDs, one for hello primary circuit, and one for hello secondary.</span></span> <span data-ttu-id="2bc47-176">Hello 외부 802.1 q 이더넷 헤더에 해당 VLAN Id가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-176">Those VLAN IDs are in hello outer 802.1Q Ethernet header.</span></span> <span data-ttu-id="2bc47-177">hello 내부 802.1 q 이더넷 헤더 (표시 되지 않음)은 특정 매핑된 tooa [ExpressRoute 라우팅 도메인](expressroute-circuit-peerings.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-177">hello inner 802.1Q Ethernet header (not shown) is mapped tooa specific [ExpressRoute routing domain](expressroute-circuit-peerings.md).</span></span>

![](./media/expressroute-faqs/expressroute-p2p-ref-arch.png)

### <a name="can-i-extend-one-of-my-vlans-tooazure-using-expressroute"></a><span data-ttu-id="2bc47-178">확장할 수 있습니까 ExpressRoute를 사용 하 여 내 Vlan tooAzure 중?</span><span class="sxs-lookup"><span data-stu-id="2bc47-178">Can I extend one of my VLANs tooAzure using ExpressRoute?</span></span>

<span data-ttu-id="2bc47-179">아니요.</span><span class="sxs-lookup"><span data-stu-id="2bc47-179">No.</span></span> <span data-ttu-id="2bc47-180">Azure까지의 계층 2 연결 확장을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-180">We do not support layer 2 connectivity extensions into Azure.</span></span>

### <a name="can-i-have-more-than-one-expressroute-circuit-in-my-subscription"></a><span data-ttu-id="2bc47-181">내 구독에 둘 이상의 ExpressRoute 회로가 있을 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="2bc47-181">Can I have more than one ExpressRoute circuit in my subscription?</span></span>

<span data-ttu-id="2bc47-182">예.</span><span class="sxs-lookup"><span data-stu-id="2bc47-182">Yes.</span></span> <span data-ttu-id="2bc47-183">사용자 구독에 둘 이상의 ExpressRoute 회로가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-183">You can have more than one ExpressRoute circuit in your subscription.</span></span> <span data-ttu-id="2bc47-184">hello 기본 제한은 too10을 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-184">hello default limit is set too10.</span></span> <span data-ttu-id="2bc47-185">필요한 경우 Microsoft 지원 tooincrease hello 제한을 문의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-185">You can contact Microsoft Support tooincrease hello limit, if needed.</span></span>

### <a name="can-i-have-expressroute-circuits-from-different-service-providers"></a><span data-ttu-id="2bc47-186">다른 서비스 공급자의 ExpressRoute 회로를 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="2bc47-186">Can I have ExpressRoute circuits from different service providers?</span></span>

<span data-ttu-id="2bc47-187">예.</span><span class="sxs-lookup"><span data-stu-id="2bc47-187">Yes.</span></span> <span data-ttu-id="2bc47-188">여러 서비스 공급자의 ExpressRoute 회로가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-188">You can have ExpressRoute circuits with many service providers.</span></span> <span data-ttu-id="2bc47-189">각 ExpressRoute 회로마다 하나의 서비스 공급자와만 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-189">Each ExpressRoute circuit is associated with one service provider only.</span></span> 

### <a name="can-i-have-multiple-expressroute-circuits-in-hello-same-location"></a><span data-ttu-id="2bc47-190">Hello에 여러 개의 ExpressRoute 회로 있을 수 같은 위치?</span><span class="sxs-lookup"><span data-stu-id="2bc47-190">Can I have multiple ExpressRoute circuits in hello same location?</span></span>

<span data-ttu-id="2bc47-191">예.</span><span class="sxs-lookup"><span data-stu-id="2bc47-191">Yes.</span></span> <span data-ttu-id="2bc47-192">동일 hello, 여러 개의 ExpressRoute 회로 라도 보유할 수 있습니다 또는 다른 서비스 공급자에서 동일한 위치를 환영 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-192">You can have multiple ExpressRoute circuits, with hello same or different service providers in hello same location.</span></span> <span data-ttu-id="2bc47-193">그러나 둘 이상의 ExpressRoute 회로 toohello를 연결할 수 없습니다 동일한 가상 네트워크 hello에서 동일 위치 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-193">However, you can't link more than one ExpressRoute circuit toohello same virtual network from hello same location.</span></span>

### <a name="how-do-i-connect-my-virtual-networks-tooan-expressroute-circuit"></a><span data-ttu-id="2bc47-194">내 가상 네트워크 tooan ExpressRoute 회로 연결 어떻게 하나요</span><span class="sxs-lookup"><span data-stu-id="2bc47-194">How do I connect my virtual networks tooan ExpressRoute circuit</span></span>

<span data-ttu-id="2bc47-195">hello 기본 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-195">hello basic steps are:</span></span>

* <span data-ttu-id="2bc47-196">ExpressRoute 회로 설정 하 고 hello 서비스 공급자를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-196">Establish an ExpressRoute circuit and have hello service provider enable it.</span></span>
* <span data-ttu-id="2bc47-197">또는 hello 공급자 hello BGP 피어 링 (s)를 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-197">You, or hello provider, must configure hello BGP peering(s).</span></span>
* <span data-ttu-id="2bc47-198">Hello 가상 네트워크 toohello ExpressRoute 회로 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-198">Link hello virtual network toohello ExpressRoute circuit.</span></span>

<span data-ttu-id="2bc47-199">자세한 내용은 [회로 프로비전 및 회로 상태에 대한 ExpressRoute 워크플로](expressroute-workflows.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2bc47-199">For more information, see [ExpressRoute workflows for circuit provisioning and circuit states](expressroute-workflows.md).</span></span>

### <a name="are-there-connectivity-boundaries-for-my-expressroute-circuit"></a><span data-ttu-id="2bc47-200">내 ExpressRoute 회로에 대한 연결 경계가 있나요?</span><span class="sxs-lookup"><span data-stu-id="2bc47-200">Are there connectivity boundaries for my ExpressRoute circuit?</span></span>

<span data-ttu-id="2bc47-201">예.</span><span class="sxs-lookup"><span data-stu-id="2bc47-201">Yes.</span></span> <span data-ttu-id="2bc47-202">hello [express 경로 파트너 및 위치](expressroute-locations.md) 문서 ExpressRoute 회로 대 한 hello 연결 경계에 대 한 개요를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-202">hello [ExpressRoute partners and locations](expressroute-locations.md) article provides an overview of hello connectivity boundaries for an ExpressRoute circuit.</span></span> <span data-ttu-id="2bc47-203">ExpressRoute 회로 대 한 연결에는 제한 된 tooa 단일 지리적 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-203">Connectivity for an ExpressRoute circuit is limited tooa single geopolitical region.</span></span> <span data-ttu-id="2bc47-204">연결은 hello ExpressRoute premium 기능을 사용 하 여 확장 된 toocross 지리적 영역을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-204">Connectivity can be expanded toocross geopolitical regions by enabling hello ExpressRoute premium feature.</span></span>

### <a name="can-i-link-toomore-than-one-virtual-network-tooan-expressroute-circuit"></a><span data-ttu-id="2bc47-205">ExpressRoute 회로 하나의 가상 네트워크 tooan 보다 toomore를 연결할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="2bc47-205">Can I link toomore than one virtual network tooan ExpressRoute circuit?</span></span>

<span data-ttu-id="2bc47-206">예.</span><span class="sxs-lookup"><span data-stu-id="2bc47-206">Yes.</span></span> <span data-ttu-id="2bc47-207">표준 ExpressRoute 회로 too10 가상 네트워크 연결을 및 too100 드릴업에 있을 수 있습니다는 [프리미엄 ExpressRoute 회로](#expressroute-premium)합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-207">You can have up too10 virtual networks connections on a standard ExpressRoute circuit, and up too100 on a [premium ExpressRoute circuit](#expressroute-premium).</span></span> 

### <a name="i-have-multiple-azure-subscriptions-that-contain-virtual-networks-can-i-connect-virtual-networks-that-are-in-separate-subscriptions-tooa-single-expressroute-circuit"></a><span data-ttu-id="2bc47-208">가상 네트워크를 포함하는 여러 Azure 구독을 가지고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-208">I have multiple Azure subscriptions that contain virtual networks.</span></span> <span data-ttu-id="2bc47-209">별도 구독 tooa 단일 ExpressRoute 회로에 있는 가상 네트워크를 연결할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="2bc47-209">Can I connect virtual networks that are in separate subscriptions tooa single ExpressRoute circuit?</span></span>

<span data-ttu-id="2bc47-210">예.</span><span class="sxs-lookup"><span data-stu-id="2bc47-210">Yes.</span></span> <span data-ttu-id="2bc47-211">Too10를 권한을 부여할 수 있습니다 다른 Azure 구독에 단일 ExpressRoute 회로 toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-211">You can authorize up too10 other Azure subscriptions toouse a single ExpressRoute circuit.</span></span> <span data-ttu-id="2bc47-212">Hello ExpressRoute premium 기능을 사용 하 여이 한도 늘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-212">This limit can be increased by enabling hello ExpressRoute premium feature.</span></span>

<span data-ttu-id="2bc47-213">자세한 내용은 [여러 구독에서 ExpressRoute 회로 공유](expressroute-howto-linkvnet-arm.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2bc47-213">For more information, see [Sharing an ExpressRoute circuit across multiple subscriptions](expressroute-howto-linkvnet-arm.md).</span></span>

### <a name="are-virtual-networks-connected-toohello-same-circuit-isolated-from-each-other"></a><span data-ttu-id="2bc47-214">각 가상 네트워크 연결 된 toohello 동일한 회로 격리?</span><span class="sxs-lookup"><span data-stu-id="2bc47-214">Are virtual networks connected toohello same circuit isolated from each other?</span></span>

<span data-ttu-id="2bc47-215">아니요.</span><span class="sxs-lookup"><span data-stu-id="2bc47-215">No.</span></span> <span data-ttu-id="2bc47-216">큐브 뷰, 모든 가상 네트워크 연결 된 toohello 라우팅에서 동일한 ExpressRoute 회로의 일부인 hello 동일한 라우팅 도메인 및 서로 분리 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-216">From a routing perspective, all virtual networks linked toohello same ExpressRoute circuit are part of hello same routing domain and are not isolated from each other.</span></span> <span data-ttu-id="2bc47-217">격리를 라우팅할 필요한 별도 ExpressRoute 회로 toocreate를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-217">If you need route isolation, you need toocreate a separate ExpressRoute circuit.</span></span>

### <a name="can-i-have-one-virtual-network-connected-toomore-than-one-expressroute-circuit"></a><span data-ttu-id="2bc47-218">하나의 ExpressRoute 회로 보다 하나의 연결 된 가상 네트워크 toomore 있습니까?</span><span class="sxs-lookup"><span data-stu-id="2bc47-218">Can I have one virtual network connected toomore than one ExpressRoute circuit?</span></span>

<span data-ttu-id="2bc47-219">예.</span><span class="sxs-lookup"><span data-stu-id="2bc47-219">Yes.</span></span> <span data-ttu-id="2bc47-220">Toofour ExpressRoute 회로를 단일 가상 네트워크와 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-220">You can link a single virtual network with up toofour ExpressRoute circuits.</span></span> <span data-ttu-id="2bc47-221">4개의 다른 [ExpressRoute 위치](expressroute-locations.md)를 통해 순서를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-221">They must be ordered through four different [ExpressRoute locations](expressroute-locations.md).</span></span>

### <a name="can-i-access-hello-internet-from-my-virtual-networks-connected-tooexpressroute-circuits"></a><span data-ttu-id="2bc47-222">내 가상 네트워크 연결 된 tooExpressRoute 회로에서 hello 인터넷에 액세스할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="2bc47-222">Can I access hello Internet from my virtual networks connected tooExpressRoute circuits?</span></span>

<span data-ttu-id="2bc47-223">예.</span><span class="sxs-lookup"><span data-stu-id="2bc47-223">Yes.</span></span> <span data-ttu-id="2bc47-224">기본 경로 (0.0.0.0/0) 또는 hello BGP 세션을 통해 인터넷 경로 접두사를 보급 하지 않았다면, 경우에 연결 된 가상 네트워크 tooan ExpressRoute 회로를 toohello 인터넷을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-224">If you have not advertised default routes (0.0.0.0/0) or Internet route prefixes through hello BGP session, you can connect toohello Internet from a virtual network linked tooan ExpressRoute circuit.</span></span>

### <a name="can-i-block-internet-connectivity-toovirtual-networks-connected-tooexpressroute-circuits"></a><span data-ttu-id="2bc47-225">인터넷 연결 toovirtual 네트워크 연결 된 tooExpressRoute 회로 차단할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="2bc47-225">Can I block Internet connectivity toovirtual networks connected tooExpressRoute circuits?</span></span>

<span data-ttu-id="2bc47-226">예.</span><span class="sxs-lookup"><span data-stu-id="2bc47-226">Yes.</span></span> <span data-ttu-id="2bc47-227">기본 경로 (0.0.0.0/0) tooblock 모든 인터넷 연결 toovirtual 컴퓨터 가상 네트워크 내에 배포 되며 hello ExpressRoute 회로 통해 모든 트래픽을 밖 라우팅할 광고할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-227">You can advertise default routes (0.0.0.0/0) tooblock all Internet connectivity toovirtual machines deployed within a virtual network and route all traffic out through hello ExpressRoute circuit.</span></span>

<span data-ttu-id="2bc47-228">기본 경로 보급 하는 경우 (예: Azure 저장소 및 SQL DB) 피어 링 공용 백 tooyour 프레미스를 통해 제공 되는 트래픽 tooservices를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-228">If you advertise default routes, we force traffic tooservices offered over public peering (such as Azure storage and SQL DB) back tooyour premises.</span></span> <span data-ttu-id="2bc47-229">Tooconfigure hello 공용 피어 링 경로 통해 또는 hello 인터넷을 통해 프로그램 라우터 tooreturn 트래픽 tooAzure 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-229">You will have tooconfigure your routers tooreturn traffic tooAzure through hello public peering path or over hello Internet.</span></span>

### <a name="can-virtual-networks-linked-toohello-same-expressroute-circuit-talk-tooeach-other"></a><span data-ttu-id="2bc47-230">가상 네트워크에 연결 된 toohello 수 있습니다. 동일한 ExpressRoute 회로 통신 tooeach 다른?</span><span class="sxs-lookup"><span data-stu-id="2bc47-230">Can virtual networks linked toohello same ExpressRoute circuit talk tooeach other?</span></span>

<span data-ttu-id="2bc47-231">예.</span><span class="sxs-lookup"><span data-stu-id="2bc47-231">Yes.</span></span> <span data-ttu-id="2bc47-232">동일한 ExpressRoute 회로 서로 통신할 수 있는 연결 된 toohello를 가상 네트워크에 배포 된 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="2bc47-232">Virtual machines deployed in virtual networks connected toohello same ExpressRoute circuit can communicate with each other.</span></span>

### <a name="can-i-use-site-to-site-connectivity-for-virtual-networks-in-conjunction-with-expressroute"></a><span data-ttu-id="2bc47-233">ExpressRoute와 함께 가상 네트워크에 대한 사이트 간 연결을 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="2bc47-233">Can I use site-to-site connectivity for virtual networks in conjunction with ExpressRoute?</span></span>

<span data-ttu-id="2bc47-234">예.</span><span class="sxs-lookup"><span data-stu-id="2bc47-234">Yes.</span></span> <span data-ttu-id="2bc47-235">ExpressRoute는 사이트 간 VPN과 공존할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-235">ExpressRoute can coexist with site-to-site VPNs.</span></span>

### <a name="can-i-move-a-virtual-network-from-site-to-site--point-to-site-configuration-toouse-expressroute"></a><span data-ttu-id="2bc47-236">사이트 간 / 지점 및 사이트 구성 toouse ExpressRoute에서에서 가상 네트워크를 이동할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="2bc47-236">Can I move a virtual network from site-to-site / point-to-site configuration toouse ExpressRoute?</span></span>

<span data-ttu-id="2bc47-237">예.</span><span class="sxs-lookup"><span data-stu-id="2bc47-237">Yes.</span></span> <span data-ttu-id="2bc47-238">가상 네트워크 내에서 express 경로 게이트웨이 toocreate를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-238">You will have toocreate an ExpressRoute gateway within your virtual network.</span></span> <span data-ttu-id="2bc47-239">Hello 프로세스와 관련 된 작은 가동 중지 시간이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-239">There is a small downtime associated with hello process.</span></span>

### <a name="why-is-there-a-public-ip-address-associated-with-hello-expressroute-gateway-on-a-virtual-network"></a><span data-ttu-id="2bc47-240">연결 된 가상 네트워크에 hello express 경로 게이트웨이 공용 IP 주소 있는 이유는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="2bc47-240">Why is there a public IP address associated with hello ExpressRoute gateway on a virtual network?</span></span>

<span data-ttu-id="2bc47-241">공용 IP 주소 hello만 내부 관리에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-241">hello public IP address is used for internal management only.</span></span> <span data-ttu-id="2bc47-242">이 공용 IP 주소 인터넷에 노출 된 toohello 아니며 가상 네트워크의 보안 노출을 것을 구성 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-242">This public IP address is not exposed toohello Internet, and does not constitute a security exposure of your virtual network.</span></span>

### <a name="what-do-i-need-tooconnect-tooazure-storage-over-expressroute"></a><span data-ttu-id="2bc47-243">무엇을 ExpressRoute를 통해 tooconnect tooAzure 저장소가 필요 합니까?</span><span class="sxs-lookup"><span data-stu-id="2bc47-243">What do I need tooconnect tooAzure storage over ExpressRoute?</span></span>

<span data-ttu-id="2bc47-244">ExpressRoute 회로를 설정하고 공용 피어링에 대한 경로를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-244">You must establish an ExpressRoute circuit and configure routes for public peering.</span></span>

### <a name="are-there-limits-on-hello-number-of-routes-i-can-advertise"></a><span data-ttu-id="2bc47-245">보급할 수 있는 I 경로 hello 수에 대 한 제한 사항이 있습니까?</span><span class="sxs-lookup"><span data-stu-id="2bc47-245">Are there limits on hello number of routes I can advertise?</span></span>

<span data-ttu-id="2bc47-246">예.</span><span class="sxs-lookup"><span data-stu-id="2bc47-246">Yes.</span></span> <span data-ttu-id="2bc47-247">개인 피어 링 용 경로 접두사 too4000와 각 200 공용 피어 링 및 Microsoft 피어 링에 대 한를 수락합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-247">We accept up too4000 route prefixes for private peering and 200 each for public peering and Microsoft peering.</span></span> <span data-ttu-id="2bc47-248">이 too10 hello ExpressRoute 고급 기능을 사용 하는 경우 개인 피어 링 용 000 경로 늘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-248">You can increase this too10,000 routes for private peering if you enable hello ExpressRoute premium feature.</span></span>

### <a name="are-there-restrictions-on-ip-ranges-i-can-advertise-over-hello-bgp-session"></a><span data-ttu-id="2bc47-249">I hello BGP 세션을 통해 보급할 수 있는 IP 범위에 대 한 제한 사항이 있습니까?</span><span class="sxs-lookup"><span data-stu-id="2bc47-249">Are there restrictions on IP ranges I can advertise over hello BGP session?</span></span>

<span data-ttu-id="2bc47-250">공용 hello 개인 접두사 (RFC1918) 및 Microsoft 피어 링 BGP 세션을 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-250">We do not accept private prefixes (RFC1918) in hello public and Microsoft peering BGP session.</span></span>

### <a name="what-happens-if-i-exceed-hello-bgp-limits"></a><span data-ttu-id="2bc47-251">Hello BGP 제한을 초과한 경우 어떻게 되나요?</span><span class="sxs-lookup"><span data-stu-id="2bc47-251">What happens if I exceed hello BGP limits?</span></span>

<span data-ttu-id="2bc47-252">BGP 세션이 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-252">BGP sessions will be dropped.</span></span> <span data-ttu-id="2bc47-253">Hello 접두사 횟수가 hello 제한 아래로 되 면 재설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-253">They will be reset once hello prefix count goes below hello limit.</span></span>

### <a name="what-is-hello-expressroute-bgp-hold-time-can-it-be-adjusted"></a><span data-ttu-id="2bc47-254">Express 경로 BGP 보유 시간 hello 이란?</span><span class="sxs-lookup"><span data-stu-id="2bc47-254">What is hello ExpressRoute BGP hold time?</span></span> <span data-ttu-id="2bc47-255">조정할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="2bc47-255">Can it be adjusted?</span></span>

<span data-ttu-id="2bc47-256">hello 대기 시간은 180입니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-256">hello hold time is 180.</span></span> <span data-ttu-id="2bc47-257">hello 연결 유지 메시지 60 초 마다 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-257">hello keep-alive messages are sent every 60 seconds.</span></span> <span data-ttu-id="2bc47-258">설정은 변경할 수 없는 Microsoft의 hello에 수정이 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-258">These are fixed settings on hello Microsoft side that cannot be changed.</span></span> <span data-ttu-id="2bc47-259">Tooconfigure 다른 타이머 있습니다 되며 hello BGP 세션 매개 변수를 적절 하 게 협상 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-259">It is possible for you tooconfigure different timers, and hello BGP session parameters will be negotiated accordingly.</span></span>

### <a name="after-i-advertise-hello-default-route-00000-toomy-virtual-networks-i-cant-activate-windows-running-on-my-azure-vms-how-tooi-fix-this"></a><span data-ttu-id="2bc47-260">Hello 기본 경로 (0.0.0.0/0) toomy 가상 네트워크를 보급 I 후 Azure Vm 내에서 실행 되는 Windows를 활성화할 수 없습니다 I.</span><span class="sxs-lookup"><span data-stu-id="2bc47-260">After I advertise hello default route (0.0.0.0/0) toomy virtual networks, I can't activate Windows running on my Azure VMs.</span></span> <span data-ttu-id="2bc47-261">어떻게 tooI이 문제 해결?</span><span class="sxs-lookup"><span data-stu-id="2bc47-261">How tooI fix this?</span></span>

<span data-ttu-id="2bc47-262">단계를 수행 하는 hello Azure hello 정품 인증 요청을 인식 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-262">hello following steps help Azure recognize hello activation request:</span></span>

1. <span data-ttu-id="2bc47-263">Hello 공용 피어 링 express 경로 회로 대 한 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-263">Establish hello public peering for your ExpressRoute circuit.</span></span>
2. <span data-ttu-id="2bc47-264">DNS 조회를 수행 하 고 hello IP 주소를 찾을 **kms.core.windows.net**</span><span class="sxs-lookup"><span data-stu-id="2bc47-264">Perform a DNS lookup and find hello IP address of **kms.core.windows.net**</span></span>
3. <span data-ttu-id="2bc47-265">hello 키 관리 서비스 인식 해야 Azure와 honor hello에서 hello 정품 인증 요청에 해당 하는 요청입니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-265">hello Key Management Service must recognize that hello activation request comes from Azure and honor hello request.</span></span> <span data-ttu-id="2bc47-266">Hello 다음 세 가지 작업 중 하나를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-266">Perform one of hello following three tasks:</span></span>

   * <span data-ttu-id="2bc47-267">온-프레미스 네트워크에 경로 hello 트래픽을 보내는 hello에 대 한 공용 피어 링 hello를 통해 백 tooAzure 2 단계에서에서 가져온 IP 주소 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-267">On your on-premises network, route hello traffic destined for hello IP address that you obtained in step 2 back tooAzure via hello public peering.</span></span>
   * <span data-ttu-id="2bc47-268">프로그램 NSP 공급자 머리 핀 hello 트래픽이 백 tooAzure hello 공용 피어 링을 통해 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-268">Have your NSP provider hair-pin hello traffic back tooAzure via hello public peering.</span></span>
   * <span data-ttu-id="2bc47-269">사용자 정의 경로 다음 홉으로 인터넷에 있는 해당 지점 hello IP를 만들고 이러한 가상 컴퓨터는 여기서 toohello ब 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-269">Create a user-defined route that points hello IP that has Internet as a next hop, and apply it toohello subnet(s) where these virtual machines are.</span></span>

### <a name="can-i-change-hello-bandwidth-of-an-expressroute-circuit"></a><span data-ttu-id="2bc47-270">Hello 대역폭의 ExpressRoute 회로 변경할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="2bc47-270">Can I change hello bandwidth of an ExpressRoute circuit?</span></span>

<span data-ttu-id="2bc47-271">예, tooincrease hello 대역폭의 ExpressRoute 회로 hello Azure 포털 또는 PowerShell을 사용 하 여 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-271">Yes, you can attempt tooincrease hello bandwidth of your ExpressRoute circuit in hello Azure portal, or by using PowerShell.</span></span> <span data-ttu-id="2bc47-272">회로가 만들어진 hello 실제 포트에 사용할 수 있는 용량이 있으면, 변경 내용을 성공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-272">If there is capacity available on hello physical port on which your circuit was created, your change succeeds.</span></span> 

<span data-ttu-id="2bc47-273">Hello 현재 포트에 남아 있는 충분 한 용량이 없는 고 toocreate hello 더 높은 대역폭을 새 ExpressRoute 회로 또는 해당 위치에서 추가 용량이 있는,이 경우 없게 필요 중 하나 있음을 의미 프로그램 변경에 실패 하는 경우 tooincrease hello 대역폭입니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-273">If your change fails, it means either there isn’t enough capacity left on hello current port and you need toocreate a new ExpressRoute circuit with hello higher bandwidth, or that there is no additional capacity at that location, in which case you won't be able tooincrease hello bandwidth.</span></span> 

<span data-ttu-id="2bc47-274">수 제공 됩니다 toofollow 연결 공급자 tooensure와 해당 네트워크 toosupport hello 대역폭 증가 내 hello 스로틀을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-274">You will also have toofollow up with your connectivity provider tooensure that they update hello throttles within their networks toosupport hello bandwidth increase.</span></span> <span data-ttu-id="2bc47-275">그러나 hello 대역폭의 ExpressRoute 회로 줄일 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-275">You cannot, however, reduce hello bandwidth of your ExpressRoute circuit.</span></span> <span data-ttu-id="2bc47-276">Toocreate 낮은 대역폭 새 ExpressRoute 회로 있고 hello 이전 회로 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-276">You have toocreate a new ExpressRoute circuit with lower bandwidth and delete hello old circuit.</span></span>

### <a name="how-do-i-change-hello-bandwidth-of-an-expressroute-circuit"></a><span data-ttu-id="2bc47-277">Hello 대역폭의 ExpressRoute 회로 변경 하려면 어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="2bc47-277">How do I change hello bandwidth of an ExpressRoute circuit?</span></span>

<span data-ttu-id="2bc47-278">Hello hello REST API 또는 PowerShell cmdlet을 사용 하 여 hello ExpressRoute 회로 대역폭을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-278">You can update hello bandwidth of hello ExpressRoute circuit using hello REST API or PowerShell cmdlet.</span></span>

## <a name="expressroute-premium"></a><span data-ttu-id="2bc47-279">ExpressRoute Premium</span><span class="sxs-lookup"><span data-stu-id="2bc47-279">ExpressRoute premium</span></span>

### <a name="what-is-expressroute-premium"></a><span data-ttu-id="2bc47-280">ExpressRoute 프리미엄이란?</span><span class="sxs-lookup"><span data-stu-id="2bc47-280">What is ExpressRoute premium?</span></span>

<span data-ttu-id="2bc47-281">ExpressRoute premium에는 같은 기능 hello의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-281">ExpressRoute premium is a collection of hello following features:</span></span>

* <span data-ttu-id="2bc47-282">개인 피어 링 용 000 경로 4000 경로 too10에서 라우팅 테이블 한도 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-282">Increased routing table limit from 4000 routes too10,000 routes for private peering.</span></span>
* <span data-ttu-id="2bc47-283">연결 된 toohello ExpressRoute 회로 될 수 있는 Vnet 수가 증가 (기본값은 10).</span><span class="sxs-lookup"><span data-stu-id="2bc47-283">Increased number of VNets that can be connected toohello ExpressRoute circuit (default is 10).</span></span> <span data-ttu-id="2bc47-284">자세한 내용은 참조 hello [ExpressRoute 제한](#limits) 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-284">For more information, see hello [ExpressRoute Limits](#limits) table.</span></span>
* <span data-ttu-id="2bc47-285">연결 tooOffice 365 및 Dynamics 365 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-285">Connectivity tooOffice 365 and Dynamics 365.</span></span>
* <span data-ttu-id="2bc47-286">Hello Microsoft 핵심 네트워크를 통해 전역 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-286">Global connectivity over hello Microsoft core network.</span></span> <span data-ttu-id="2bc47-287">이제 한 지리적 지역의 VNet을 다른 지역의 ExpressRoute 회로와 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-287">You can now link a VNet in one geopolitical region with an ExpressRoute circuit in another region.</span></span><br>
    <span data-ttu-id="2bc47-288">**예제:**</span><span class="sxs-lookup"><span data-stu-id="2bc47-288">**Examples:**</span></span>

    *  <span data-ttu-id="2bc47-289">서유럽 tooan Silicon Valley에 만든 ExpressRoute 회로에 만든 VNet을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-289">You can link a VNet created in Europe West tooan ExpressRoute circuit created in Silicon Valley.</span></span> 
    *  <span data-ttu-id="2bc47-290">공용 피어 링 hello에 Silicon Valley에 회로에서 인도 서 부 유럽 예를 들어 SQL Azure에 연결할 수 있도록 다른 지리적 지역에서 접두사는 보급 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-290">On hello public peering, prefixes from other geopolitical regions are advertised such that you can connect to, for example, SQL Azure in Europe West from a circuit in Silicon Valley.</span></span>


### <span data-ttu-id="2bc47-291"><a name="limits"></a>개수 Vnet을 연결 하는 tooan ExpressRoute 회로 ExpressRoute premium을 사용 합니까?</span><span class="sxs-lookup"><span data-stu-id="2bc47-291"><a name="limits"></a>How many VNets can I link tooan ExpressRoute circuit if I enabled ExpressRoute premium?</span></span>

<span data-ttu-id="2bc47-292">hello 다음 표에서 보여 hello ExpressRoute 제한 및 express 경로 회로 당 Vnet의 hello 수 있습니다:</span><span class="sxs-lookup"><span data-stu-id="2bc47-292">hello following tables show hello ExpressRoute limits and hello number of VNets per ExpressRoute circuit:</span></span>

[!INCLUDE [ExpressRoute limits](../../includes/expressroute-limits.md)]

### <a name="how-do-i-enable-expressroute-premium"></a><span data-ttu-id="2bc47-293">ExpressRoute Premium을 사용하려면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="2bc47-293">How do I enable ExpressRoute premium?</span></span>

<span data-ttu-id="2bc47-294">ExpressRoute 프리미엄 기능 hello 기능을 사용 하는 경우 사용할 수 있습니다 및 hello 회로 상태를 업데이트 하 여 종료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-294">ExpressRoute premium features can be enabled when hello feature is enabled, and can be shut down by updating hello circuit state.</span></span> <span data-ttu-id="2bc47-295">회로가 만들어질 때 ExpressRoute 프리미엄을 활성화 수 또는 hello REST API를 호출할 수 / PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2bc47-295">You can enable ExpressRoute premium at circuit creation time, or can call hello REST API / PowerShell cmdlet.</span></span>

### <a name="how-do-i-disable-expressroute-premium"></a><span data-ttu-id="2bc47-296">ExpressRoute Premium을 사용하지 않도록 하려면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="2bc47-296">How do I disable ExpressRoute premium?</span></span>

<span data-ttu-id="2bc47-297">ExpressRoute 프리미엄 hello REST API 또는 PowerShell cmdlet을 호출 하 여 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-297">You can disable ExpressRoute premium by calling hello REST API or PowerShell cmdlet.</span></span> <span data-ttu-id="2bc47-298">ExpressRoute premium을 사용 하지 않도록 설정 하기 전에 연결 요구 toomeet hello 기본 제한을 조정 했 있는지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-298">You must make sure that you have scaled your connectivity needs toomeet hello default limits before you disable ExpressRoute premium.</span></span> <span data-ttu-id="2bc47-299">Hello 기본도 넘어 확장 하면 사용률 hello 요청 toodisable ExpressRoute 프리미엄 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-299">If your utilization scales beyond hello default limits, hello request toodisable ExpressRoute premium fails.</span></span>

### <a name="can-i-pick-and-choose-hello-features-i-want-from-hello-premium-feature-set"></a><span data-ttu-id="2bc47-300">I 선택할 수 hello 프리미엄 기능 집합에서 원하는 hello 기능이 있습니까?</span><span class="sxs-lookup"><span data-stu-id="2bc47-300">Can I pick and choose hello features I want from hello premium feature set?</span></span>

<span data-ttu-id="2bc47-301">아니요.</span><span class="sxs-lookup"><span data-stu-id="2bc47-301">No.</span></span> <span data-ttu-id="2bc47-302">Hello 기능을 선택할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-302">You can't pick hello features.</span></span> <span data-ttu-id="2bc47-303">ExpressRoute Premium을 켜면 모든 기능을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-303">We enable all features when you turn on ExpressRoute premium.</span></span>

### <a name="how-much-does-expressroute-premium-cost"></a><span data-ttu-id="2bc47-304">ExpressRoute Premium 비용</span><span class="sxs-lookup"><span data-stu-id="2bc47-304">How much does ExpressRoute premium cost?</span></span>

<span data-ttu-id="2bc47-305">너무 참조[가격 정보](https://azure.microsoft.com/pricing/details/expressroute/) 비용에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-305">Refer too[pricing details](https://azure.microsoft.com/pricing/details/expressroute/) for cost.</span></span>

### <a name="do-i-pay-for-expressroute-premium-in-addition-toostandard-expressroute-charges"></a><span data-ttu-id="2bc47-306">납부 ExpressRoute 프리미엄에 대 한 또한 toostandard ExpressRoute 요금?</span><span class="sxs-lookup"><span data-stu-id="2bc47-306">Do I pay for ExpressRoute premium in addition toostandard ExpressRoute charges?</span></span>

<span data-ttu-id="2bc47-307">예.</span><span class="sxs-lookup"><span data-stu-id="2bc47-307">Yes.</span></span> <span data-ttu-id="2bc47-308">Express 경로 회로 요금과 hello 연결 공급자에 필요한 요금이 위에 ExpressRoute 프리미엄 요금이 부과 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-308">ExpressRoute premium charges apply on top of ExpressRoute circuit charges and charges required by hello connectivity provider.</span></span>

## <a name="expressroute-for-office-365-and-dynamics-365"></a><span data-ttu-id="2bc47-309">Office 365 및 Dynamics 365에 대한 ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="2bc47-309">ExpressRoute for Office 365 and Dynamics 365</span></span>

[!INCLUDE [expressroute-office365-include](../../includes/expressroute-office365-include.md)]

### <a name="how-do-i-create-an-expressroute-circuit-tooconnect-toooffice-365-services-and-dynamics-365"></a><span data-ttu-id="2bc47-310">어떻게 만드나요 ExpressRoute 회로 tooconnect tooOffice 365 서비스 및 Dynamics 365?</span><span class="sxs-lookup"><span data-stu-id="2bc47-310">How do I create an ExpressRoute circuit tooconnect tooOffice 365 services and Dynamics 365?</span></span>

1. <span data-ttu-id="2bc47-311">검토 hello [ExpressRoute 필수 구성 요소 페이지](expressroute-prerequisites.md) toomake hello 요구 사항을 충족 하는지 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-311">Review hello [ExpressRoute prerequisites page](expressroute-prerequisites.md) toomake sure you meet hello requirements.</span></span>
2. <span data-ttu-id="2bc47-312">충족 하 고 연결 tooensure, 서비스 공급자 및 위치 hello에 hello 목록을 검토 [express 경로 파트너 및 위치](expressroute-locations.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="2bc47-312">tooensure that your connectivity needs are met, review hello list of service providers and locations in hello [ExpressRoute partners and locations](expressroute-locations.md) article.</span></span>
3. <span data-ttu-id="2bc47-313">[Office 365에 대한 네트워크 계획 및 성능 튜닝](http://aka.ms/tune/)을 검토하여 용량 요구 사항을 계획합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-313">Plan your capacity requirements by reviewing [Network planning and performance tuning for Office 365](http://aka.ms/tune/).</span></span>
4. <span data-ttu-id="2bc47-314">연결을 워크플로 tooset hello에에서 나열 된 hello 단계에 따라 [회선 프로비저닝 및 회선 상태에 대 한 express 경로 워크플로](expressroute-workflows.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-314">Follow hello steps listed in hello workflows tooset up connectivity [ExpressRoute workflows for circuit provisioning and circuit states](expressroute-workflows.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2bc47-315">연결 tooOffice 365 서비스 및 Dynamics 365 구성할 때 ExpressRoute premium 추가 기능을 설정 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-315">Make sure that you have enabled ExpressRoute premium add-on when configuring connectivity tooOffice 365 services and Dynamics 365.</span></span>
> 
> 

### <a name="do-i-need-tooenable-azure-public-peering-tooconnect-toooffice-365-services-and-dynamics-365"></a><span data-ttu-id="2bc47-316">해야 Azure tooenable tooconnect tooOffice 365 서비스와 Dynamics 365 피어 링 공용?</span><span class="sxs-lookup"><span data-stu-id="2bc47-316">Do I need tooenable Azure public peering tooconnect tooOffice 365 services and Dynamics 365?</span></span>

<span data-ttu-id="2bc47-317">아니요, Microsoft 피어 링 tooenable만 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-317">No, you only need tooenable Microsoft Peering.</span></span> <span data-ttu-id="2bc47-318">인증 트래픽 tooAzure AD Microsoft 피어 링을 통해 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-318">Authentication traffic tooAzure AD is sent through Microsoft Peering.</span></span> 

### <a name="can-my-existing-expressroute-circuits-support-connectivity-toooffice-365-services-and-dynamics-365"></a><span data-ttu-id="2bc47-319">연결 tooOffice 365 서비스 및 Dynamics 365 내 기존 express 경로 회로 지원할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="2bc47-319">Can my existing ExpressRoute circuits support connectivity tooOffice 365 services and Dynamics 365?</span></span>

<span data-ttu-id="2bc47-320">예.</span><span class="sxs-lookup"><span data-stu-id="2bc47-320">Yes.</span></span> <span data-ttu-id="2bc47-321">기존 express 경로 회로 구성 된 toosupport 연결 tooOffice 365 서비스 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-321">Your existing ExpressRoute circuit can be configured toosupport connectivity tooOffice 365 services.</span></span> <span data-ttu-id="2bc47-322">충분 한 용량 tooconnect tooOffice 365 서비스가 하며 premium 추가 기능을 설정 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-322">Make sure that you have sufficient capacity tooconnect tooOffice 365 services and that you have enabled premium add-on.</span></span> <span data-ttu-id="2bc47-323">[Office 365의 네트워크 계획 및 성능 조정](http://aka.ms/tune/)을 참조하면 연결 요구 사항을 계획할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-323">[Network planning and performance tuning for Office 365](http://aka.ms/tune/) helps you plan your connectivity needs.</span></span> <span data-ttu-id="2bc47-324">[ExpressRoute 회로 만들기 및 수정](expressroute-howto-circuit-classic.md)도 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2bc47-324">Also, see [Create and modify an ExpressRoute circuit](expressroute-howto-circuit-classic.md).</span></span>

### <a name="what-office-365-services-can-be-accessed-over-an-expressroute-connection"></a><span data-ttu-id="2bc47-325">ExpressRoute 연결을 통해 어느 Office 365 서비스에 액세스할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="2bc47-325">What Office 365 services can be accessed over an ExpressRoute connection?</span></span>

<span data-ttu-id="2bc47-326">너무 참조[Office 365 Url 및 IP 주소 범위](http://aka.ms/o365endpoints) ExpressRoute를 통해 지원 되는 서비스의 최신 목록에 대 한 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-326">Refer too[Office 365 URLs and IP address ranges](http://aka.ms/o365endpoints) page for an up-to-date list of services supported over ExpressRoute.</span></span>

### <a name="how-much-does-expressroute-for-office-365-services-and-dynamics-365-cost"></a><span data-ttu-id="2bc47-327">Office 365 서비스 및 Dynamics 365용 ExpressRoute 비용은 얼마인가요?</span><span class="sxs-lookup"><span data-stu-id="2bc47-327">How much does ExpressRoute for Office 365 services and Dynamics 365 cost?</span></span>

<span data-ttu-id="2bc47-328">Office 365 서비스와 Dynamics 365 premium 추가 기능 toobe 활성화 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-328">Office 365 services and Dynamics 365 require premium add-on toobe enabled.</span></span> <span data-ttu-id="2bc47-329">Hello 참조 [가격 책정 세부 정보 페이지](https://azure.microsoft.com/pricing/details/expressroute/) 비용에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-329">See hello [pricing details page](https://azure.microsoft.com/pricing/details/expressroute/) for costs.</span></span>

### <a name="what-regions-is-expressroute-for-office-365-supported-in"></a><span data-ttu-id="2bc47-330">Office 365용 ExpressRoute가 지원하는 영역</span><span class="sxs-lookup"><span data-stu-id="2bc47-330">What regions is ExpressRoute for Office 365 supported in?</span></span>

<span data-ttu-id="2bc47-331">[ExpressRoute 파트너 및 위치](expressroute-locations.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2bc47-331">See [ExpressRoute partners and locations](expressroute-locations.md) for information.</span></span>

### <a name="can-i-access-office-365-over-hello-internet-even-if-expressroute-was-configured-for-my-organization"></a><span data-ttu-id="2bc47-332">에 액세스할 수 Office 365 hello 인터넷을 통해 ExpressRoute 내 조직에 대해 구성 된 경우에?</span><span class="sxs-lookup"><span data-stu-id="2bc47-332">Can I access Office 365 over hello Internet, even if ExpressRoute was configured for my organization?</span></span>

<span data-ttu-id="2bc47-333">예.</span><span class="sxs-lookup"><span data-stu-id="2bc47-333">Yes.</span></span> <span data-ttu-id="2bc47-334">Office 365 서비스 끝점은 네트워크에 대 한 express 경로 구성한 경우에 hello 인터넷을 통해 연결할 수 있는입니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-334">Office 365 service endpoints are reachable through hello Internet, even though ExpressRoute has been configured for your network.</span></span> <span data-ttu-id="2bc47-335">ExpressRoute 통해 구성 된 tooconnect tooOffice 365 서비스에 있는 위치에 있는 경우 ExpressRoute를 통해 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-335">If you are in a location that is configured tooconnect tooOffice 365 services through ExpressRoute, you will connect through ExpressRoute.</span></span>

### <a name="can-i-access-office-365-us-government-community-gcc-services-over-an-azure-us-government-expressroute-circuit"></a><span data-ttu-id="2bc47-336">Azure 미국 정부 ExpressRoute 회로를 통해 Office 365 미국 정부 커뮤니티(GCC) 서비스에 액세스할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="2bc47-336">Can I access Office 365 US Government Community (GCC) services over an Azure US Government ExpressRoute circuit?</span></span>

<span data-ttu-id="2bc47-337">예.</span><span class="sxs-lookup"><span data-stu-id="2bc47-337">Yes.</span></span> <span data-ttu-id="2bc47-338">Office 365 GCC 서비스 끝점은 Azure 미국 정부 ExpressRoute hello를 통해 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-338">Office 365 GCC service endpoints are reachable through hello Azure US Government ExpressRoute.</span></span> <span data-ttu-id="2bc47-339">그러나 하면 첫 번째 필요 tooopen 지원 티켓에 hello tooadvertise tooMicrosoft를 만들려는 경우 Azure 포털 tooprovide hello 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-339">However, you first need tooopen a support ticket on hello Azure portal tooprovide hello prefixes you intend tooadvertise tooMicrosoft.</span></span> <span data-ttu-id="2bc47-340">사용자 연결 tooOffice 365 GCC 서비스는 hello 지원 티켓 해결 된 후 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-340">Your connectivity tooOffice 365 GCC services will be established after hello support ticket is resolved.</span></span> 

### <a name="can-dynamics-365-for-operations-formerly-known-as-dynamics-ax-online-be-accessed-over-an-expressroute-connection"></a><span data-ttu-id="2bc47-341">ExpressRoute 연결을 통해 Dynamics 365 for Operations(이전의 Dynamics AX Online)에 액세스할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="2bc47-341">Can Dynamics 365 for Operations (formerly known as Dynamics AX Online) be accessed over an ExpressRoute connection?</span></span>

<span data-ttu-id="2bc47-342">예.</span><span class="sxs-lookup"><span data-stu-id="2bc47-342">Yes.</span></span> <span data-ttu-id="2bc47-343">[Dynamics 365 for Operations](https://www.microsoft.com/dynamics365/operations)가 Azure에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-343">[Dynamics 365 for Operations](https://www.microsoft.com/dynamics365/operations) is hosted on Azure.</span></span> <span data-ttu-id="2bc47-344">Azure 공용 피어 링 express 경로 회로 tooconnect tooit 프로그램에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-344">You can enable Azure public peering on your ExpressRoute circuit tooconnect tooit.</span></span>

## <a name="route-filters-for-microsoft-peering"></a><span data-ttu-id="2bc47-345">Microsoft 피어링용 경로 필터</span><span class="sxs-lookup"><span data-stu-id="2bc47-345">Route filters for Microsoft peering</span></span>

### <a name="i-am-turning-on-microsoft-peering-for-hello-first-time-what-routes-will-i-see"></a><span data-ttu-id="2bc47-346">처음으로 hello에 대 한 피어 링 Microsoft 켜기, 어떤 경로 얼마나?</span><span class="sxs-lookup"><span data-stu-id="2bc47-346">I am turning on Microsoft peering for hello first time, what routes will I see?</span></span>

<span data-ttu-id="2bc47-347">경로는 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-347">You will not see any routes.</span></span> <span data-ttu-id="2bc47-348">Tooattach는 경로 필터 tooyour 회로 toostart 접두사 알림을 만들어야합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-348">You have tooattach a route filter tooyour circuit toostart prefix advertisements.</span></span> <span data-ttu-id="2bc47-349">자세한 내용은 [Microsoft 피어링용 경로 필터 구성](how-to-routefilter-powershell.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2bc47-349">For instructions, see [Configure route filters for Microsoft peering](how-to-routefilter-powershell.md).</span></span>

### <a name="i-turned-on-microsoft-peering-and-now-i-am-trying-tooselect-exchange-online-but-it-is-giving-me-an-error-that-i-am-not-authorized-toodo-it"></a><span data-ttu-id="2bc47-350">필자는 Microsoft 피어 링에 있고 Exchange Online 동안 tooselect 저는 걸리지만 것은 me는 없는 권한이 부여 된 toodo 오류가 이제 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-350">I turned on Microsoft peering and now I am trying tooselect Exchange Online, but it is giving me an error that I am not authorized toodo it.</span></span>

<span data-ttu-id="2bc47-351">경로 필터를 사용하면 모든 고객이 Microsoft 피어링을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-351">When using route filters, any customer can turn on Microsoft peering.</span></span> <span data-ttu-id="2bc47-352">그러나 Office 365 서비스를 사용 하 고에 대 한 보내야 tooget Office 365에 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-352">However, for consuming Office 365 services, you still need tooget authorized by Office 365.</span></span>

### <a name="do-i-need-tooget-authorization-for-turning-on-dynamics-365-over-microsoft-peering"></a><span data-ttu-id="2bc47-353">Microsoft 피어 링을 통해 Dynamics 365 켜는 tooget 권한 부여 필요 합니까?</span><span class="sxs-lookup"><span data-stu-id="2bc47-353">Do I need tooget authorization for turning on Dynamics 365 over Microsoft peering?</span></span>

<span data-ttu-id="2bc47-354">아니요, Dynamics 365에 대해 권한을 부여받을 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-354">No, you do not need authorization for Dynamics 365.</span></span> <span data-ttu-id="2bc47-355">규칙을 만든 다음, 권한을 부여받지 않고 Dynamics 365 커뮤니티를 선택하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-355">You can create a rule and select Dynamics 365 community without authorization.</span></span>

### <a name="i-already-have-microsoft-peering-how-can-i-take-advantage-of-route-filters"></a><span data-ttu-id="2bc47-356">Microsoft 피어링을 이미 사용하고 있습니다. 경로 필터를 사용하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="2bc47-356">I already have Microsoft peering, how can I take advantage of route filters?</span></span>

<span data-ttu-id="2bc47-357">선택 hello 서비스를 toouse, 연결 hello 필터 tooyour Microsoft 피어 링, 경로 필터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-357">You can create a route filter, select hello services you want toouse, and attach hello filter tooyour Microsoft peering.</span></span> <span data-ttu-id="2bc47-358">자세한 내용은 [Microsoft 피어링용 경로 필터 구성](how-to-routefilter-powershell.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2bc47-358">For instructions, see [Configure route filters for Microsoft peering](how-to-routefilter-powershell.md).</span></span>

### <a name="i-have-microsoft-peering-at-one-location-now-i-am-trying-tooenable-it-at-another-location-and-i-am-not-seeing-any-prefixes"></a><span data-ttu-id="2bc47-359">이제 tooenable 려 한 위치에서 피어 링 하는 Microsoft가 다른 위치에서 모든 접두사가 표시 되지 않는 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-359">I have Microsoft peering at one location, now I am trying tooenable it at another location and I am not seeing any prefixes.</span></span>

* <span data-ttu-id="2bc47-360">이전 tooAugust 1에 구성 된 ExpressRoute 회로의 Microsoft 피어 링, 경로 필터 정의 되어 있지 않은 경우에 2017 Microsoft 피어 링을 통해 보급 되는 모든 서비스 접두사를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-360">Microsoft peering of ExpressRoute circuits that were configured prior tooAugust 1, 2017 will have all service prefixes advertised through Microsoft peering, even if route filters are not defined.</span></span>

* <span data-ttu-id="2bc47-361">Microsoft 또는 그 이후에 2017 년 8 월 1 구성한 ExpressRoute 회로의 피어 링 수는 없습니다 모든 접두사 필터는 연결 될 때까지 보급 toohello 회로 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-361">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached toohello circuit.</span></span> <span data-ttu-id="2bc47-362">접두사는 기본적으로 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc47-362">You will see no prefixes by default.</span></span>

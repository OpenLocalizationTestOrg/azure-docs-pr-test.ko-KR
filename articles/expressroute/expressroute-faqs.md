---
title: Azure ExpressRoute FAQ | Microsoft Docs
description: "ExpressRoute FAQ는 Azure 서비스, 비용, 데이터 및 연결, SLA, 공급자 및 위치, 대역폭 및 추가 기술 세부 정보에 대한 정보를 포함합니다."
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
ms.openlocfilehash: 39b79dce555ba1b57f48ca2b431c13b1c1e4d90b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="expressroute-faq"></a><span data-ttu-id="7664d-103">ExpressRoute FAQ</span><span class="sxs-lookup"><span data-stu-id="7664d-103">ExpressRoute FAQ</span></span>

## <a name="what-is-expressroute"></a><span data-ttu-id="7664d-104">ExpressRoute란?</span><span class="sxs-lookup"><span data-stu-id="7664d-104">What is ExpressRoute?</span></span>

<span data-ttu-id="7664d-105">ExpressRoute는 온-프레미스 또는 공동 장소 환경의 Microsoft 데이터 센터와 인프라 사이에 개인 연결을 만들 수 있게 해 주는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-105">ExpressRoute is an Azure service that lets you create private connections between Microsoft datacenters and infrastructure that’s on your premises or in a colocation facility.</span></span> <span data-ttu-id="7664d-106">ExpressRoute 연결은 공용 인터넷을 사용하지 않으며 인터넷을 통한 일반 연결보다 안정적이고 속도가 빠르며 대기 시간이 짧고 보안성이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-106">ExpressRoute connections do not go over the public Internet, and offer higher security, reliability, and speeds with lower latencies than typical connections over the Internet.</span></span>

### <a name="what-are-the-benefits-of-using-expressroute-and-private-network-connections"></a><span data-ttu-id="7664d-107">ExpressRoute 및 개인 네트워크 연결을 사용할 경우 이점은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="7664d-107">What are the benefits of using ExpressRoute and private network connections?</span></span>

<span data-ttu-id="7664d-108">ExpressRoute 연결은 공용 인터넷을 통해 이동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-108">ExpressRoute connections do not go over the public Internet.</span></span> <span data-ttu-id="7664d-109">인터넷을 통한 일반적인 연결보다 더 짧고 일관된 대기 시간으로 더 높은 보안, 안정성 및 속도를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-109">They offer higher security, reliability, and speeds, with lower and consistent latencies than typical connections over the Internet.</span></span> <span data-ttu-id="7664d-110">경우에 따라 온-프레미스 장치와 Azure 간 데이터 전송에 ExpressRoute 연결을 사용하면 상당한 비용 혜택을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-110">In some cases, using ExpressRoute connections to transfer data between on-premises devices and Azure can yield significant cost benefits.</span></span>

### <a name="where-is-the-service-available"></a><span data-ttu-id="7664d-111">서비스를 사용할 수 있는 곳은 어디인가요?</span><span class="sxs-lookup"><span data-stu-id="7664d-111">Where is the service available?</span></span>

<span data-ttu-id="7664d-112">서비스 위치 및 가용성은 [ExpressRoute 파트너 및 위치](expressroute-locations.md)페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7664d-112">See this page for service location and availability: [ExpressRoute partners and locations](expressroute-locations.md).</span></span>

### <a name="how-can-i-use-expressroute-to-connect-to-microsoft-if-i-dont-have-partnerships-with-one-of-the-expressroute-carrier-partners"></a><span data-ttu-id="7664d-113">ExpressRoute 통신 업체 중 하나와 파트너의 관계가 아닌 경우, ExpressRoute를 사용하여 Microsoft에 연결할 수 있는 방법이 있나요?</span><span class="sxs-lookup"><span data-stu-id="7664d-113">How can I use ExpressRoute to connect to Microsoft if I don’t have partnerships with one of the ExpressRoute-carrier partners?</span></span>

<span data-ttu-id="7664d-114">지역 통신 업체를 선택하고 지원되는 exchange 공급자 위치 중 하나에 이더넷 연결을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-114">You can select a regional carrier and land Ethernet connections to one of the supported exchange provider locations.</span></span> <span data-ttu-id="7664d-115">그러면 공급자 위치에서 Microsoft와 피어링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-115">You can then peer with Microsoft at the provider location.</span></span> <span data-ttu-id="7664d-116">[ExpressRoute 파트너 및 위치](expressroute-locations.md) 의 마지막 섹션을 검사하여 서비스 공급자가 Exchange 위치 중 하나에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-116">Check the last section of [ExpressRoute partners and locations](expressroute-locations.md) to see if your service provider is present in any of the exchange locations.</span></span> <span data-ttu-id="7664d-117">그런 다음 Azure에 연결하려면 서비스 공급자를 통해 Express 경로 회로를 주문할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-117">You can then order an ExpressRoute circuit through the service provider to connect to Azure.</span></span>

### <a name="how-much-does-expressroute-cost"></a><span data-ttu-id="7664d-118">Express 경로 비용</span><span class="sxs-lookup"><span data-stu-id="7664d-118">How much does ExpressRoute cost?</span></span>

<span data-ttu-id="7664d-119">가격 정보는 [가격 정보](https://azure.microsoft.com/pricing/details/expressroute/) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7664d-119">Check [pricing details](https://azure.microsoft.com/pricing/details/expressroute/) for pricing information.</span></span>

### <a name="if-i-pay-for-an-expressroute-circuit-of-a-given-bandwidth-does-the-vpn-connection-i-purchase-from-my-network-service-provider-have-to-be-the-same-speed"></a><span data-ttu-id="7664d-120">지정된 대역폭의 ExpressRoute 회로에 대한 비용을 지불하는 경우, 네트워크 서비스 공급자로부터 구입한 VPN 연결은 동일한 속도여야 하나요?</span><span class="sxs-lookup"><span data-stu-id="7664d-120">If I pay for an ExpressRoute circuit of a given bandwidth, does the VPN connection I purchase from my network service provider have to be the same speed?</span></span>

<span data-ttu-id="7664d-121">아니요.</span><span class="sxs-lookup"><span data-stu-id="7664d-121">No.</span></span> <span data-ttu-id="7664d-122">서비스 공급자로부터 모든 속도의 VPN 연결을 구입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-122">You can purchase a VPN connection of any speed from your service provider.</span></span> <span data-ttu-id="7664d-123">그러나 Azure에 대한 연결은 구입한 ExpressRoute 회로 대역폭으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-123">However, your connection to Azure is limited to the ExpressRoute circuit bandwidth that you purchase.</span></span>

### <a name="if-i-pay-for-an-expressroute-circuit-of-a-given-bandwidth-do-i-have-the-ability-to-burst-up-to-higher-speeds-if-necessary"></a><span data-ttu-id="7664d-124">지정된 대역폭의 ExpressRoute 회로에 대해 비용을 지불한다면 필요한 경우 더 높은 속도로 버스트할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="7664d-124">If I pay for an ExpressRoute circuit of a given bandwidth, do I have the ability to burst up to higher speeds if necessary?</span></span>

<span data-ttu-id="7664d-125">예.</span><span class="sxs-lookup"><span data-stu-id="7664d-125">Yes.</span></span> <span data-ttu-id="7664d-126">ExpressRoute 회로는 추가 비용 없이 확보한 대역폭 제한의 최대 2배까지 버스트할 수 있도록 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-126">ExpressRoute circuits are configured to allow you to burst up to two times the bandwidth limit you procured for no additional cost.</span></span> <span data-ttu-id="7664d-127">이 기능을 지원하는지 확인하려면 해당 서비스 공급자에게 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="7664d-127">Check with your service provider to see if they support this capability.</span></span>

### <a name="can-i-use-the-same-private-network-connection-with-virtual-network-and-other-azure-services-simultaneously"></a><span data-ttu-id="7664d-128">가상 네트워크 및 다른 Azure 서비스와 동일한 개인 네트워크 연결을 동시에 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="7664d-128">Can I use the same private network connection with virtual network and other Azure services simultaneously?</span></span>

<span data-ttu-id="7664d-129">예.</span><span class="sxs-lookup"><span data-stu-id="7664d-129">Yes.</span></span> <span data-ttu-id="7664d-130">ExpressRoute 회로는 일단 설정되면 가상 네트워크 내 서비스와 다른 Azure 서비스에 동시에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-130">An ExpressRoute circuit, once set up, allows you to access services within a virtual network and other Azure services simultaneously.</span></span> <span data-ttu-id="7664d-131">개인 피어링 경로를 통해 가상 네트워크에 연결하고, 공용 피어링 경로를 통해 다른 서비스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-131">You connect to virtual networks over the private peering path, and to other services over the public peering path.</span></span>

### <a name="does-expressroute-offer-a-service-level-agreement-sla"></a><span data-ttu-id="7664d-132">ExpressRoute는 SLA(서비스 수준 계약)을 제공하나요?</span><span class="sxs-lookup"><span data-stu-id="7664d-132">Does ExpressRoute offer a Service Level Agreement (SLA)?</span></span>

<span data-ttu-id="7664d-133">자세한 내용은 [ExpressRoute SLA](https://azure.microsoft.com/support/legal/sla/) 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7664d-133">For information, see the [ExpressRoute SLA](https://azure.microsoft.com/support/legal/sla/) page.</span></span>

## <a name="supported-services"></a><span data-ttu-id="7664d-134">지원되는 서비스</span><span class="sxs-lookup"><span data-stu-id="7664d-134">Supported services</span></span>

<span data-ttu-id="7664d-135">ExpressRoute는 다양한 유형의 서비스에 대해 [세 개의 라우팅 도메인](expressroute-circuit-peerings.md)을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-135">ExpressRoute supports [three routing domains](expressroute-circuit-peerings.md) for various types of services.</span></span>

### <a name="private-peering"></a><span data-ttu-id="7664d-136">개인 피어링</span><span class="sxs-lookup"><span data-stu-id="7664d-136">Private peering</span></span>

* <span data-ttu-id="7664d-137">모든 가상 컴퓨터 및 클라우드 서비스를 포함한 가상 네트워크</span><span class="sxs-lookup"><span data-stu-id="7664d-137">Virtual networks, including all virtual machines and cloud services</span></span>

### <a name="public-peering"></a><span data-ttu-id="7664d-138">공용 피어링</span><span class="sxs-lookup"><span data-stu-id="7664d-138">Public peering</span></span>

* <span data-ttu-id="7664d-139">Power BI</span><span class="sxs-lookup"><span data-stu-id="7664d-139">Power BI</span></span>
* <span data-ttu-id="7664d-140">Dynamics 365 for Finance and Operations(이전의 Dynamics AX Online)</span><span class="sxs-lookup"><span data-stu-id="7664d-140">Dynamics 365 for Finance and Operations (formerly known as Dynamics AX Online)</span></span>
* <span data-ttu-id="7664d-141">다음 몇 가지 예외를 제외한 대부분의 Azure 서비스</span><span class="sxs-lookup"><span data-stu-id="7664d-141">Most of the Azure services, with the following few exceptions:</span></span>
  * <span data-ttu-id="7664d-142">CDN</span><span class="sxs-lookup"><span data-stu-id="7664d-142">CDN</span></span>
  * <span data-ttu-id="7664d-143">Visual Studio Team Services 부하 테스트</span><span class="sxs-lookup"><span data-stu-id="7664d-143">Visual Studio Team Services Load Testing</span></span>
  * <span data-ttu-id="7664d-144">Multi-Factor 인증</span><span class="sxs-lookup"><span data-stu-id="7664d-144">Multi-factor Authentication</span></span>
  * <span data-ttu-id="7664d-145">Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="7664d-145">Traffic Manager</span></span>

### <a name="microsoft-peering"></a><span data-ttu-id="7664d-146">Microsoft 피어링</span><span class="sxs-lookup"><span data-stu-id="7664d-146">Microsoft peering</span></span>

* [<span data-ttu-id="7664d-147">Office 365</span><span class="sxs-lookup"><span data-stu-id="7664d-147">Office 365</span></span>](http://aka.ms/ExpressRouteOffice365)
* <span data-ttu-id="7664d-148">Dynamics 365 Customer Engagement 응용 프로그램(이전의 CRM Online)</span><span class="sxs-lookup"><span data-stu-id="7664d-148">Dynamics 365 Customer Engagement applications (formerly known as CRM Online)</span></span>
  * <span data-ttu-id="7664d-149">Dynamics 365 for Sales</span><span class="sxs-lookup"><span data-stu-id="7664d-149">Dynamics 365 for Sales</span></span>
  * <span data-ttu-id="7664d-150">Dynamics 365 for Customer Service</span><span class="sxs-lookup"><span data-stu-id="7664d-150">Dynamics 365 for Customer Service</span></span>
  * <span data-ttu-id="7664d-151">Dynamics 365 for Field Service</span><span class="sxs-lookup"><span data-stu-id="7664d-151">Dynamics 365 for Field Service</span></span>
  * <span data-ttu-id="7664d-152">Dynamics 365 for Project Service</span><span class="sxs-lookup"><span data-stu-id="7664d-152">Dynamics 365 for Project Service</span></span>

## <a name="data-and-connections"></a><span data-ttu-id="7664d-153">데이터 및 연결</span><span class="sxs-lookup"><span data-stu-id="7664d-153">Data and connections</span></span>

### <a name="are-there-limits-on-the-amount-of-data-that-i-can-transfer-using-expressroute"></a><span data-ttu-id="7664d-154">ExpressRoute를 사용하여 전송할 수 있는 데이터의 양에 제한이 있나요?</span><span class="sxs-lookup"><span data-stu-id="7664d-154">Are there limits on the amount of data that I can transfer using ExpressRoute?</span></span>

<span data-ttu-id="7664d-155">데이터 전송 크기에 대한 제한을 설정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-155">We do not set a limit on the amount of data transfer.</span></span> <span data-ttu-id="7664d-156">대역폭 요금에 대한 정보는 [가격 정보](https://azure.microsoft.com/pricing/details/expressroute/) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7664d-156">Refer to [pricing details](https://azure.microsoft.com/pricing/details/expressroute/) for information on bandwidth rates.</span></span>

### <a name="what-connection-speeds-are-supported-by-expressroute"></a><span data-ttu-id="7664d-157">ExpressRoute에서 지원되는 연결 속도는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="7664d-157">What connection speeds are supported by ExpressRoute?</span></span>

<span data-ttu-id="7664d-158">지원되는 대역폭은 다음을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-158">Supported bandwidth offers:</span></span>

<span data-ttu-id="7664d-159">50Mbps, 100Mbps, 200Mbps, 500Mbps, 1Gbps, 2Gbps, 5Gbps, 10Gbps</span><span class="sxs-lookup"><span data-stu-id="7664d-159">50 Mbps, 100 Mbps, 200 Mbps, 500 Mbps, 1 Gbps, 2 Gbps, 5 Gbps, 10 Gbps</span></span>

### <a name="which-service-providers-are-available"></a><span data-ttu-id="7664d-160">어떤 서비스 공급자를 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="7664d-160">Which service providers are available?</span></span>

<span data-ttu-id="7664d-161">서비스 공급자 및 위치 목록은 [ExpressRoute 파트너 및 위치](expressroute-locations.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7664d-161">See [ExpressRoute partners and locations](expressroute-locations.md) for the list of service providers and locations.</span></span>

## <a name="technical-details"></a><span data-ttu-id="7664d-162">기술 세부 정보</span><span class="sxs-lookup"><span data-stu-id="7664d-162">Technical details</span></span>

### <a name="what-are-the-technical-requirements-for-connecting-my-on-premises-location-to-azure"></a><span data-ttu-id="7664d-163">내 온-프레미스 위치를 Azure에 연결하기 위한 기술 요구 사항은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="7664d-163">What are the technical requirements for connecting my on-premises location to Azure?</span></span>

<span data-ttu-id="7664d-164">요구 사항은 [ExpressRoute 필수 구성 요소 페이지](expressroute-prerequisites.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7664d-164">See [ExpressRoute prerequisites page](expressroute-prerequisites.md) for requirements.</span></span>

### <a name="are-connections-to-expressroute-redundant"></a><span data-ttu-id="7664d-165">ExpressRoute에 대한 연결이 중복되나요?</span><span class="sxs-lookup"><span data-stu-id="7664d-165">Are connections to ExpressRoute redundant?</span></span>

<span data-ttu-id="7664d-166">예.</span><span class="sxs-lookup"><span data-stu-id="7664d-166">Yes.</span></span> <span data-ttu-id="7664d-167">각 ExpressRoute 회로에는 고가용성을 제공하도록 구성된 중복 쌍의 교차연결이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-167">Each ExpressRoute circuit has a redundant pair of cross connections configured to provide high availability.</span></span>

### <a name="will-i-lose-connectivity-if-one-of-my-expressroute-links-fail"></a><span data-ttu-id="7664d-168">내 ExpressRoute 링크 중 하나가 실패하면 연결이 끊어지나요?</span><span class="sxs-lookup"><span data-stu-id="7664d-168">Will I lose connectivity if one of my ExpressRoute links fail?</span></span>

<span data-ttu-id="7664d-169">교차 연결 중 하나가 실패할 경우 연결이 손실되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-169">You will not lose connectivity if one of the cross connections fails.</span></span> <span data-ttu-id="7664d-170">중복 연결은 네트워크의 로드를 지원하기 위해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-170">A redundant connection is available to support the load of your network.</span></span> <span data-ttu-id="7664d-171">오류 복구를 수행할 다른 피어링 위치에 여러 회로를 추가로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-171">You can additionally create multiple circuits in a different peering location to achieve failure resilience.</span></span>

### <span data-ttu-id="7664d-172"><a name="onep2plink"></a>클라우드 교환에 공동 배치되지 않았으며 서비스 공급자가 점 대 점 연결을 공급하는 경우 온-프레미스 네트워크와 Microsoft 간에 두 개의 실제 연결을 주문해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="7664d-172"><a name="onep2plink"></a>If I'm not co-located at a cloud exchange and my service provider offers point-to-point connection, do I need to order two physical connections between my on-premises network and Microsoft?</span></span>

<span data-ttu-id="7664d-173">서비스 공급자가 실제 연결을 통해 두 개의 이더넷 가상 회로를 설정할 수 있으면 하나의 실제 연결만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-173">If your service provider can establish two Ethernet virtual circuits over the physical connection, you only need one physical connection.</span></span> <span data-ttu-id="7664d-174">실제 연결(예: 광섬유)은 레이어 1(L1) 장치에서 종료됩니다(이미지 참조).</span><span class="sxs-lookup"><span data-stu-id="7664d-174">The physical connection (for example, an optical fiber) is terminated on a layer 1 (L1) device (see the image).</span></span> <span data-ttu-id="7664d-175">두 개의 이더넷 가상 회로에는 서로 다른 VLAN ID로 태그가 지정되는데, 하나는 기본 회로용이고 다른 하나는 보조 회로용입니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-175">The two Ethernet virtual circuits are tagged with different VLAN IDs, one for the primary circuit, and one for the secondary.</span></span> <span data-ttu-id="7664d-176">해당 VLAN ID는 외부 802.1Q 이더넷 헤더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-176">Those VLAN IDs are in the outer 802.1Q Ethernet header.</span></span> <span data-ttu-id="7664d-177">내부 802.1Q 이더넷 헤더(표시되지 않음)는 특정 [ExpressRoute 라우팅 도메인](expressroute-circuit-peerings.md)에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-177">The inner 802.1Q Ethernet header (not shown) is mapped to a specific [ExpressRoute routing domain](expressroute-circuit-peerings.md).</span></span>

![](./media/expressroute-faqs/expressroute-p2p-ref-arch.png)

### <a name="can-i-extend-one-of-my-vlans-to-azure-using-expressroute"></a><span data-ttu-id="7664d-178">ExpressRoute를 사용하여 Azure에 대한 내 VLAN 중 하나를 확장할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="7664d-178">Can I extend one of my VLANs to Azure using ExpressRoute?</span></span>

<span data-ttu-id="7664d-179">아니요.</span><span class="sxs-lookup"><span data-stu-id="7664d-179">No.</span></span> <span data-ttu-id="7664d-180">Azure까지의 계층 2 연결 확장을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-180">We do not support layer 2 connectivity extensions into Azure.</span></span>

### <a name="can-i-have-more-than-one-expressroute-circuit-in-my-subscription"></a><span data-ttu-id="7664d-181">내 구독에 둘 이상의 ExpressRoute 회로가 있을 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="7664d-181">Can I have more than one ExpressRoute circuit in my subscription?</span></span>

<span data-ttu-id="7664d-182">예.</span><span class="sxs-lookup"><span data-stu-id="7664d-182">Yes.</span></span> <span data-ttu-id="7664d-183">사용자 구독에 둘 이상의 ExpressRoute 회로가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-183">You can have more than one ExpressRoute circuit in your subscription.</span></span> <span data-ttu-id="7664d-184">기본 제한은 10으로 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-184">The default limit is set to 10.</span></span> <span data-ttu-id="7664d-185">필요한 경우 Microsoft 지원에 문의하여 제한을 늘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-185">You can contact Microsoft Support to increase the limit, if needed.</span></span>

### <a name="can-i-have-expressroute-circuits-from-different-service-providers"></a><span data-ttu-id="7664d-186">다른 서비스 공급자의 ExpressRoute 회로를 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="7664d-186">Can I have ExpressRoute circuits from different service providers?</span></span>

<span data-ttu-id="7664d-187">예.</span><span class="sxs-lookup"><span data-stu-id="7664d-187">Yes.</span></span> <span data-ttu-id="7664d-188">여러 서비스 공급자의 ExpressRoute 회로가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-188">You can have ExpressRoute circuits with many service providers.</span></span> <span data-ttu-id="7664d-189">각 ExpressRoute 회로마다 하나의 서비스 공급자와만 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-189">Each ExpressRoute circuit is associated with one service provider only.</span></span> 

### <a name="can-i-have-multiple-expressroute-circuits-in-the-same-location"></a><span data-ttu-id="7664d-190">같은 위치에 여러 ExpressRoute 회로를 포함할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="7664d-190">Can I have multiple ExpressRoute circuits in the same location?</span></span>

<span data-ttu-id="7664d-191">예.</span><span class="sxs-lookup"><span data-stu-id="7664d-191">Yes.</span></span> <span data-ttu-id="7664d-192">같은 위치에서, 같거나 다른 서비스 공급자로 여러 ExpressRoute 회로를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-192">You can have multiple ExpressRoute circuits, with the same or different service providers in the same location.</span></span> <span data-ttu-id="7664d-193">하지만 동일한 위치에서 동일한 가상 네트워크로 둘 이상의 ExpressRoute 회로를 연결할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-193">However, you can't link more than one ExpressRoute circuit to the same virtual network from the same location.</span></span>

### <a name="how-do-i-connect-my-virtual-networks-to-an-expressroute-circuit"></a><span data-ttu-id="7664d-194">가상 네트워크를 ExpressRoute 회로에 연결하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="7664d-194">How do I connect my virtual networks to an ExpressRoute circuit</span></span>

<span data-ttu-id="7664d-195">기본 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-195">The basic steps are:</span></span>

* <span data-ttu-id="7664d-196">ExpressRoute 회로를 설정하고 서비스 공급자가 이를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-196">Establish an ExpressRoute circuit and have the service provider enable it.</span></span>
* <span data-ttu-id="7664d-197">사용자 또는 공급자가 BGP 피어링을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-197">You, or the provider, must configure the BGP peering(s).</span></span>
* <span data-ttu-id="7664d-198">가상 네트워크를 ExpressRoute 회로에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-198">Link the virtual network to the ExpressRoute circuit.</span></span>

<span data-ttu-id="7664d-199">자세한 내용은 [회로 프로비전 및 회로 상태에 대한 ExpressRoute 워크플로](expressroute-workflows.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7664d-199">For more information, see [ExpressRoute workflows for circuit provisioning and circuit states](expressroute-workflows.md).</span></span>

### <a name="are-there-connectivity-boundaries-for-my-expressroute-circuit"></a><span data-ttu-id="7664d-200">내 ExpressRoute 회로에 대한 연결 경계가 있나요?</span><span class="sxs-lookup"><span data-stu-id="7664d-200">Are there connectivity boundaries for my ExpressRoute circuit?</span></span>

<span data-ttu-id="7664d-201">예.</span><span class="sxs-lookup"><span data-stu-id="7664d-201">Yes.</span></span> <span data-ttu-id="7664d-202">[ExpressRoute 파트너 및 위치](expressroute-locations.md) 문서에서 ExpressRoute 회로에 대한 연결 경계를 간략하게 설명하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-202">The [ExpressRoute partners and locations](expressroute-locations.md) article provides an overview of the connectivity boundaries for an ExpressRoute circuit.</span></span> <span data-ttu-id="7664d-203">ExpressRoute 회로에 대한 연결은 단일 지역으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-203">Connectivity for an ExpressRoute circuit is limited to a single geopolitical region.</span></span> <span data-ttu-id="7664d-204">연결은 ExpressRoute 프리미엄 기능을 사용하여 지역을 교차하도록 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-204">Connectivity can be expanded to cross geopolitical regions by enabling the ExpressRoute premium feature.</span></span>

### <a name="can-i-link-to-more-than-one-virtual-network-to-an-expressroute-circuit"></a><span data-ttu-id="7664d-205">둘 이상의 가상 네트워크를 ExpressRoute 회로에 연결할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="7664d-205">Can I link to more than one virtual network to an ExpressRoute circuit?</span></span>

<span data-ttu-id="7664d-206">예.</span><span class="sxs-lookup"><span data-stu-id="7664d-206">Yes.</span></span> <span data-ttu-id="7664d-207">표준 ExpressRoute 회로에는 가상 네트워크 연결을 최대 10개, [프리미엄 ExpressRoute 회로](#expressroute-premium)에는 최대 100개를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-207">You can have up to 10 virtual networks connections on a standard ExpressRoute circuit, and up to 100 on a [premium ExpressRoute circuit](#expressroute-premium).</span></span> 

### <a name="i-have-multiple-azure-subscriptions-that-contain-virtual-networks-can-i-connect-virtual-networks-that-are-in-separate-subscriptions-to-a-single-expressroute-circuit"></a><span data-ttu-id="7664d-208">가상 네트워크를 포함하는 여러 Azure 구독을 가지고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-208">I have multiple Azure subscriptions that contain virtual networks.</span></span> <span data-ttu-id="7664d-209">개별 구독에 속한 가상 네트워크를 단일 ExpressRoute 회로에 연결할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="7664d-209">Can I connect virtual networks that are in separate subscriptions to a single ExpressRoute circuit?</span></span>

<span data-ttu-id="7664d-210">예.</span><span class="sxs-lookup"><span data-stu-id="7664d-210">Yes.</span></span> <span data-ttu-id="7664d-211">단일 ExpressRoute 회로를 사용하여 다른 Azure 구독을 최대 10개까지 권한을 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-211">You can authorize up to 10 other Azure subscriptions to use a single ExpressRoute circuit.</span></span> <span data-ttu-id="7664d-212">ExpressRoute 프리미엄 기능을 사용하여 이 한도를 늘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-212">This limit can be increased by enabling the ExpressRoute premium feature.</span></span>

<span data-ttu-id="7664d-213">자세한 내용은 [여러 구독에서 ExpressRoute 회로 공유](expressroute-howto-linkvnet-arm.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7664d-213">For more information, see [Sharing an ExpressRoute circuit across multiple subscriptions](expressroute-howto-linkvnet-arm.md).</span></span>

### <a name="are-virtual-networks-connected-to-the-same-circuit-isolated-from-each-other"></a><span data-ttu-id="7664d-214">가상 네트워크가 서로 격리된 동일한 회로에 연결되어 있나요?</span><span class="sxs-lookup"><span data-stu-id="7664d-214">Are virtual networks connected to the same circuit isolated from each other?</span></span>

<span data-ttu-id="7664d-215">번호</span><span class="sxs-lookup"><span data-stu-id="7664d-215">No.</span></span> <span data-ttu-id="7664d-216">라우팅 관점에서 동일한 ExpressRoute 회로에 연결된 모든 가상 네트워크는 동일한 라우팅 도메인의 일부이며 서로 격리되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-216">From a routing perspective, all virtual networks linked to the same ExpressRoute circuit are part of the same routing domain and are not isolated from each other.</span></span> <span data-ttu-id="7664d-217">경로 격리가 필요하면 별도의 ExpressRoute 회로를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-217">If you need route isolation, you need to create a separate ExpressRoute circuit.</span></span>

### <a name="can-i-have-one-virtual-network-connected-to-more-than-one-expressroute-circuit"></a><span data-ttu-id="7664d-218">하나의 가상 네트워크를 둘 이상의 ExpressRoute 회로에 연결할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="7664d-218">Can I have one virtual network connected to more than one ExpressRoute circuit?</span></span>

<span data-ttu-id="7664d-219">예.</span><span class="sxs-lookup"><span data-stu-id="7664d-219">Yes.</span></span> <span data-ttu-id="7664d-220">단일 가상 네트워크를 최대 4개의 ExpressRoute 회로와 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-220">You can link a single virtual network with up to four ExpressRoute circuits.</span></span> <span data-ttu-id="7664d-221">4개의 다른 [ExpressRoute 위치](expressroute-locations.md)를 통해 순서를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-221">They must be ordered through four different [ExpressRoute locations](expressroute-locations.md).</span></span>

### <a name="can-i-access-the-internet-from-my-virtual-networks-connected-to-expressroute-circuits"></a><span data-ttu-id="7664d-222">ExpressRoute 회로에 연결된 가상 네트워크에서 인터넷에 액세스할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="7664d-222">Can I access the Internet from my virtual networks connected to ExpressRoute circuits?</span></span>

<span data-ttu-id="7664d-223">예.</span><span class="sxs-lookup"><span data-stu-id="7664d-223">Yes.</span></span> <span data-ttu-id="7664d-224">BGP 세션을 통해 기본 경로(0.0.0.0/0) 또는 인터넷 경로 접두사를 보급하지 않았다면 ExpressRoute 회로에 연결된 가상 네트워크에서 인터넷에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-224">If you have not advertised default routes (0.0.0.0/0) or Internet route prefixes through the BGP session, you can connect to the Internet from a virtual network linked to an ExpressRoute circuit.</span></span>

### <a name="can-i-block-internet-connectivity-to-virtual-networks-connected-to-expressroute-circuits"></a><span data-ttu-id="7664d-225">ExpressRoute 회로에 연결된 가상 네트워크에 대한 인터넷 연결을 차단할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="7664d-225">Can I block Internet connectivity to virtual networks connected to ExpressRoute circuits?</span></span>

<span data-ttu-id="7664d-226">예.</span><span class="sxs-lookup"><span data-stu-id="7664d-226">Yes.</span></span> <span data-ttu-id="7664d-227">기본 경로(0.0.0.0/0)를 보급하여 가상 네트워크 내에 배포된 가상 컴퓨터에 대한 모든 인터넷 연결을 차단하고 ExpressRoute 회로를 통해 모든 트래픽을 라우팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-227">You can advertise default routes (0.0.0.0/0) to block all Internet connectivity to virtual machines deployed within a virtual network and route all traffic out through the ExpressRoute circuit.</span></span>

<span data-ttu-id="7664d-228">기본 경로를 보급하는 경우 공용 피어링(예: Azure storage 및 SQL DB)을 통해 프레미스에 다시 제공된 서비스로 트래픽을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-228">If you advertise default routes, we force traffic to services offered over public peering (such as Azure storage and SQL DB) back to your premises.</span></span> <span data-ttu-id="7664d-229">공용 피어링 경로 또는 인터넷을 통해 트래픽을 Azure로 반환하도록 라우터를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-229">You will have to configure your routers to return traffic to Azure through the public peering path or over the Internet.</span></span>

### <a name="can-virtual-networks-linked-to-the-same-expressroute-circuit-talk-to-each-other"></a><span data-ttu-id="7664d-230">동일한 ExpressRoute 회로에 연결된 가상 네트워크가 서로 통신할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="7664d-230">Can virtual networks linked to the same ExpressRoute circuit talk to each other?</span></span>

<span data-ttu-id="7664d-231">예.</span><span class="sxs-lookup"><span data-stu-id="7664d-231">Yes.</span></span> <span data-ttu-id="7664d-232">동일한 ExpressRoute 회로에 연결된 가상 네트워크에 배포된 가상 컴퓨터는 서로 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-232">Virtual machines deployed in virtual networks connected to the same ExpressRoute circuit can communicate with each other.</span></span>

### <a name="can-i-use-site-to-site-connectivity-for-virtual-networks-in-conjunction-with-expressroute"></a><span data-ttu-id="7664d-233">ExpressRoute와 함께 가상 네트워크에 대한 사이트 간 연결을 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="7664d-233">Can I use site-to-site connectivity for virtual networks in conjunction with ExpressRoute?</span></span>

<span data-ttu-id="7664d-234">예.</span><span class="sxs-lookup"><span data-stu-id="7664d-234">Yes.</span></span> <span data-ttu-id="7664d-235">ExpressRoute는 사이트 간 VPN과 공존할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-235">ExpressRoute can coexist with site-to-site VPNs.</span></span>

### <a name="can-i-move-a-virtual-network-from-site-to-site--point-to-site-configuration-to-use-expressroute"></a><span data-ttu-id="7664d-236">ExpressRoute를 사용하여 사이트 간 / 지점과 사이트 간 구성에서 가상 네트워크를 이동할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="7664d-236">Can I move a virtual network from site-to-site / point-to-site configuration to use ExpressRoute?</span></span>

<span data-ttu-id="7664d-237">예.</span><span class="sxs-lookup"><span data-stu-id="7664d-237">Yes.</span></span> <span data-ttu-id="7664d-238">가상 네트워크 내에 ExpressRoute 게이트웨이를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-238">You will have to create an ExpressRoute gateway within your virtual network.</span></span> <span data-ttu-id="7664d-239">프로세스와 관련된 가동 중지 시간이 짧습니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-239">There is a small downtime associated with the process.</span></span>

### <a name="why-is-there-a-public-ip-address-associated-with-the-expressroute-gateway-on-a-virtual-network"></a><span data-ttu-id="7664d-240">가상 네트워크에서 ExpressRoute 게이트웨이와 연결된 공용 IP 주소가 있는 이유는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="7664d-240">Why is there a public IP address associated with the ExpressRoute gateway on a virtual network?</span></span>

<span data-ttu-id="7664d-241">공용 IP 주소는 내부 관리를 위해서만 사용되므로</span><span class="sxs-lookup"><span data-stu-id="7664d-241">The public IP address is used for internal management only.</span></span> <span data-ttu-id="7664d-242">인터넷에 공개되지 않으며 가상 네트워크의 보안 노출을 구성하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-242">This public IP address is not exposed to the Internet, and does not constitute a security exposure of your virtual network.</span></span>

### <a name="what-do-i-need-to-connect-to-azure-storage-over-expressroute"></a><span data-ttu-id="7664d-243">ExpressRoute를 통해 Azure storage에 연결해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="7664d-243">What do I need to connect to Azure storage over ExpressRoute?</span></span>

<span data-ttu-id="7664d-244">ExpressRoute 회로를 설정하고 공용 피어링에 대한 경로를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-244">You must establish an ExpressRoute circuit and configure routes for public peering.</span></span>

### <a name="are-there-limits-on-the-number-of-routes-i-can-advertise"></a><span data-ttu-id="7664d-245">보급할 수 있는 경로의 수에 제한이 있나요?</span><span class="sxs-lookup"><span data-stu-id="7664d-245">Are there limits on the number of routes I can advertise?</span></span>

<span data-ttu-id="7664d-246">예.</span><span class="sxs-lookup"><span data-stu-id="7664d-246">Yes.</span></span> <span data-ttu-id="7664d-247">개인 피어링에 대해 최대 4000개의 경로 접두사를 허용하고, 공용 피어링과 Microsoft 피어링에 대해 각각 200개의 경로 접두사를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-247">We accept up to 4000 route prefixes for private peering and 200 each for public peering and Microsoft peering.</span></span> <span data-ttu-id="7664d-248">ExpressRoute 프리미엄 기능을 사용하도록 설정하면 개인 피어링에 대해 10,000개의 경로까지 늘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-248">You can increase this to 10,000 routes for private peering if you enable the ExpressRoute premium feature.</span></span>

### <a name="are-there-restrictions-on-ip-ranges-i-can-advertise-over-the-bgp-session"></a><span data-ttu-id="7664d-249">BGP 세션을 통해 보급할 수 있는 IP 범위에 제한 사항이 있나요?</span><span class="sxs-lookup"><span data-stu-id="7664d-249">Are there restrictions on IP ranges I can advertise over the BGP session?</span></span>

<span data-ttu-id="7664d-250">공용 및 Microsoft 피어링 BGP 세션에서 개인 접두사(RFC1918)는 허용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-250">We do not accept private prefixes (RFC1918) in the public and Microsoft peering BGP session.</span></span>

### <a name="what-happens-if-i-exceed-the-bgp-limits"></a><span data-ttu-id="7664d-251">BGP 제한을 초과하면 어떻게 되나요?</span><span class="sxs-lookup"><span data-stu-id="7664d-251">What happens if I exceed the BGP limits?</span></span>

<span data-ttu-id="7664d-252">BGP 세션이 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-252">BGP sessions will be dropped.</span></span> <span data-ttu-id="7664d-253">접두사 개수가 제한보다 적으면 재설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-253">They will be reset once the prefix count goes below the limit.</span></span>

### <a name="what-is-the-expressroute-bgp-hold-time-can-it-be-adjusted"></a><span data-ttu-id="7664d-254">ExpressRoute BGP 확보 시간이란 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="7664d-254">What is the ExpressRoute BGP hold time?</span></span> <span data-ttu-id="7664d-255">조정할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="7664d-255">Can it be adjusted?</span></span>

<span data-ttu-id="7664d-256">확보 시간은 180입니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-256">The hold time is 180.</span></span> <span data-ttu-id="7664d-257">연결 유지 메시지는 60초마다 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-257">The keep-alive messages are sent every 60 seconds.</span></span> <span data-ttu-id="7664d-258">이 설정은 Microsoft 쪽에서 고정된 설정으로, 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-258">These are fixed settings on the Microsoft side that cannot be changed.</span></span> <span data-ttu-id="7664d-259">다른 타이머를 구성 할 수 있으며, 이에 따라 BGP 세션 매개 변수가 협상됩니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-259">It is possible for you to configure different timers, and the BGP session parameters will be negotiated accordingly.</span></span>

### <a name="after-i-advertise-the-default-route-00000-to-my-virtual-networks-i-cant-activate-windows-running-on-my-azure-vms-how-to-i-fix-this"></a><span data-ttu-id="7664d-260">가상 네트워크에 기본 경로(0.0.0.0/0)를 보급한 후 Azure VM에서 실행되는 Windows를 활성화할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-260">After I advertise the default route (0.0.0.0/0) to my virtual networks, I can't activate Windows running on my Azure VMs.</span></span> <span data-ttu-id="7664d-261">이 문제를 해결하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="7664d-261">How to I fix this?</span></span>

<span data-ttu-id="7664d-262">다음 단계는 Azure에서 활성화 요청을 인식하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-262">The following steps help Azure recognize the activation request:</span></span>

1. <span data-ttu-id="7664d-263">ExpressRoute 회로에 공용 피어링을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-263">Establish the public peering for your ExpressRoute circuit.</span></span>
2. <span data-ttu-id="7664d-264">DNS 조회를 수행하고 **kms.core.windows.net**</span><span class="sxs-lookup"><span data-stu-id="7664d-264">Perform a DNS lookup and find the IP address of **kms.core.windows.net**</span></span>
3. <span data-ttu-id="7664d-265">키 관리 서비스는 활성화 요청이 Azure에서 제공됨을 인식하고 해당 요청을 승인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-265">The Key Management Service must recognize that the activation request comes from Azure and honor the request.</span></span> <span data-ttu-id="7664d-266">다음 세 가지 작업 중 하나를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-266">Perform one of the following three tasks:</span></span>

   * <span data-ttu-id="7664d-267">온-프레미스 네트워크에서 2단계에서 얻은 IP 주소로 향하는 트래픽을 공용 피어링을 통해 Azure로 다시 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-267">On your on-premises network, route the traffic destined for the IP address that you obtained in step 2 back to Azure via the public peering.</span></span>
   * <span data-ttu-id="7664d-268">NSP 공급자는 공용 피어링을 통해 Azure에 다시 트래픽을 hair-pin합니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-268">Have your NSP provider hair-pin the traffic back to Azure via the public peering.</span></span>
   * <span data-ttu-id="7664d-269">인터넷을 다음 홉으로 사용하는 IP를 가리키는 사용자 정의 경로를 만들고 이러한 가상 컴퓨터가 있는 서브넷에 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-269">Create a user-defined route that points the IP that has Internet as a next hop, and apply it to the subnet(s) where these virtual machines are.</span></span>

### <a name="can-i-change-the-bandwidth-of-an-expressroute-circuit"></a><span data-ttu-id="7664d-270">ExpressRoute 회로의 대역폭을 변경할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="7664d-270">Can I change the bandwidth of an ExpressRoute circuit?</span></span>

<span data-ttu-id="7664d-271">예, Azure Portal 또는 PowerShell을 사용하여 ExpressRoute 회로의 대역폭을 늘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-271">Yes, you can attempt to increase the bandwidth of your ExpressRoute circuit in the Azure portal, or by using PowerShell.</span></span> <span data-ttu-id="7664d-272">회로가 만들어진 실제 포트에 사용 가능한 용량이 있으면 성공적으로 변경된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-272">If there is capacity available on the physical port on which your circuit was created, your change succeeds.</span></span> 

<span data-ttu-id="7664d-273">변경이 실패하면 현재 포트에 남아 있는 용량이 부족하거나(이 경우 더 높은 대역폭으로 새 ExpressRoute 회로를 만들어야 함) 해당 위치에 추가 용량이 없습니다(이 경우 대역폭을 늘릴 수 없음).</span><span class="sxs-lookup"><span data-stu-id="7664d-273">If your change fails, it means either there isn’t enough capacity left on the current port and you need to create a new ExpressRoute circuit with the higher bandwidth, or that there is no additional capacity at that location, in which case you won't be able to increase the bandwidth.</span></span> 

<span data-ttu-id="7664d-274">또한 연결 공급자는 네트워크 내 제한을 업데이트하여 대역폭 증가를 지원하도록 후속 작업해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-274">You will also have to follow up with your connectivity provider to ensure that they update the throttles within their networks to support the bandwidth increase.</span></span> <span data-ttu-id="7664d-275">하지만 ExpressRoute 회로의 대역폭은 줄일 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-275">You cannot, however, reduce the bandwidth of your ExpressRoute circuit.</span></span> <span data-ttu-id="7664d-276">낮은 대역폭으로 새 ExpressRoute 회로를 만들고, 이전 회로는 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-276">You have to create a new ExpressRoute circuit with lower bandwidth and delete the old circuit.</span></span>

### <a name="how-do-i-change-the-bandwidth-of-an-expressroute-circuit"></a><span data-ttu-id="7664d-277">ExpressRoute 회로의 대역폭을 변경하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="7664d-277">How do I change the bandwidth of an ExpressRoute circuit?</span></span>

<span data-ttu-id="7664d-278">REST API 및 PowerShell cmdlet을 사용하여 ExpressRoute 회로의 대역폭을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-278">You can update the bandwidth of the ExpressRoute circuit using the REST API or PowerShell cmdlet.</span></span>

## <a name="expressroute-premium"></a><span data-ttu-id="7664d-279">ExpressRoute Premium</span><span class="sxs-lookup"><span data-stu-id="7664d-279">ExpressRoute premium</span></span>

### <a name="what-is-expressroute-premium"></a><span data-ttu-id="7664d-280">ExpressRoute 프리미엄이란?</span><span class="sxs-lookup"><span data-stu-id="7664d-280">What is ExpressRoute premium?</span></span>

<span data-ttu-id="7664d-281">ExpressRoute Premium은 다음 기능의 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-281">ExpressRoute premium is a collection of the following features:</span></span>

* <span data-ttu-id="7664d-282">증가된 라우팅 테이블은 개인 피어링에 대해 4000개의 경로에서 경로 10, 000개의 경로로 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-282">Increased routing table limit from 4000 routes to 10,000 routes for private peering.</span></span>
* <span data-ttu-id="7664d-283">ExpressRoute 회로에 연결할 수 있는 VNets 수가 증가합니다(기본값은 10).</span><span class="sxs-lookup"><span data-stu-id="7664d-283">Increased number of VNets that can be connected to the ExpressRoute circuit (default is 10).</span></span> <span data-ttu-id="7664d-284">자세한 내용은 [ExpressRoute 제한](#limits) 표를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7664d-284">For more information, see the [ExpressRoute Limits](#limits) table.</span></span>
* <span data-ttu-id="7664d-285">Office 365 및 Dynamics 365에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-285">Connectivity to Office 365 and Dynamics 365.</span></span>
* <span data-ttu-id="7664d-286">Microsoft 핵심 네트워크를 통해 전역 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-286">Global connectivity over the Microsoft core network.</span></span> <span data-ttu-id="7664d-287">이제 한 지리적 지역의 VNet을 다른 지역의 ExpressRoute 회로와 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-287">You can now link a VNet in one geopolitical region with an ExpressRoute circuit in another region.</span></span><br>
    <span data-ttu-id="7664d-288">**예제:**</span><span class="sxs-lookup"><span data-stu-id="7664d-288">**Examples:**</span></span>

    *  <span data-ttu-id="7664d-289">유럽 서부에서 만든 VNet을 실리콘밸리에서 만든 ExpressRoute 회로에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-289">You can link a VNet created in Europe West to an ExpressRoute circuit created in Silicon Valley.</span></span> 
    *  <span data-ttu-id="7664d-290">공용 피어링에서는 실리콘밸리의 회로에서 유럽 서부의 SQL Azure에 연결할 수 있는 것처럼 다른 지리적 지역의 접두사가 보급됩니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-290">On the public peering, prefixes from other geopolitical regions are advertised such that you can connect to, for example, SQL Azure in Europe West from a circuit in Silicon Valley.</span></span>


### <span data-ttu-id="7664d-291"><a name="limits"></a>ExpressRoute Premium을 사용하는 경우 ExpressRoute 회로에 연결할 수 있는 VNet의 수는 어떻게 되나요?</span><span class="sxs-lookup"><span data-stu-id="7664d-291"><a name="limits"></a>How many VNets can I link to an ExpressRoute circuit if I enabled ExpressRoute premium?</span></span>

<span data-ttu-id="7664d-292">아래 표에서는 ExpressRoute 제한 및 ExpressRoute 회로당 VNet 수를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-292">The following tables show the ExpressRoute limits and the number of VNets per ExpressRoute circuit:</span></span>

[!INCLUDE [ExpressRoute limits](../../includes/expressroute-limits.md)]

### <a name="how-do-i-enable-expressroute-premium"></a><span data-ttu-id="7664d-293">ExpressRoute Premium을 사용하려면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="7664d-293">How do I enable ExpressRoute premium?</span></span>

<span data-ttu-id="7664d-294">ExpressRoute Premium 기능은 사용하도록 설정되면 활성화할 수 있으며, 회로 상태를 업데이트하여 종료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-294">ExpressRoute premium features can be enabled when the feature is enabled, and can be shut down by updating the circuit state.</span></span> <span data-ttu-id="7664d-295">ExpressRoute Premium은 회로를 만들 때 또는 REST API/PowerShell cmdlet을 호출하여 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-295">You can enable ExpressRoute premium at circuit creation time, or can call the REST API / PowerShell cmdlet.</span></span>

### <a name="how-do-i-disable-expressroute-premium"></a><span data-ttu-id="7664d-296">ExpressRoute Premium을 사용하지 않도록 하려면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="7664d-296">How do I disable ExpressRoute premium?</span></span>

<span data-ttu-id="7664d-297">ExpressRoute Premium은 REST API/PowerShell cmdlet을 호출하여 사용하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-297">You can disable ExpressRoute premium by calling the REST API or PowerShell cmdlet.</span></span> <span data-ttu-id="7664d-298">ExpressRoute Premium을 사용하지 않도록 설정하기 전에 기본 제한을 충족하도록 연결 요구 사항을 조정했는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-298">You must make sure that you have scaled your connectivity needs to meet the default limits before you disable ExpressRoute premium.</span></span> <span data-ttu-id="7664d-299">사용률이 기본 제한을 초과하면 ExpressRoute Premium을 사용하지 않도록 설정하는 요청이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-299">If your utilization scales beyond the default limits, the request to disable ExpressRoute premium fails.</span></span>

### <a name="can-i-pick-and-choose-the-features-i-want-from-the-premium-feature-set"></a><span data-ttu-id="7664d-300">프리미엄 기능 집합에서 원하는 기능을 선택할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="7664d-300">Can I pick and choose the features I want from the premium feature set?</span></span>

<span data-ttu-id="7664d-301">아니요.</span><span class="sxs-lookup"><span data-stu-id="7664d-301">No.</span></span> <span data-ttu-id="7664d-302">기능은 선택할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-302">You can't pick the features.</span></span> <span data-ttu-id="7664d-303">ExpressRoute Premium을 켜면 모든 기능을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-303">We enable all features when you turn on ExpressRoute premium.</span></span>

### <a name="how-much-does-expressroute-premium-cost"></a><span data-ttu-id="7664d-304">ExpressRoute Premium 비용</span><span class="sxs-lookup"><span data-stu-id="7664d-304">How much does ExpressRoute premium cost?</span></span>

<span data-ttu-id="7664d-305">비용은 [가격 정보](https://azure.microsoft.com/pricing/details/expressroute/) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7664d-305">Refer to [pricing details](https://azure.microsoft.com/pricing/details/expressroute/) for cost.</span></span>

### <a name="do-i-pay-for-expressroute-premium-in-addition-to-standard-expressroute-charges"></a><span data-ttu-id="7664d-306">표준 ExpressRoute 요금 외에도 ExpressRoute premium에 대한 납부 여부</span><span class="sxs-lookup"><span data-stu-id="7664d-306">Do I pay for ExpressRoute premium in addition to standard ExpressRoute charges?</span></span>

<span data-ttu-id="7664d-307">예.</span><span class="sxs-lookup"><span data-stu-id="7664d-307">Yes.</span></span> <span data-ttu-id="7664d-308">ExpressRoute premium 요금은 ExpressRoute 회로 요금 및 연결 공급자에서 필요한 요금 위에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-308">ExpressRoute premium charges apply on top of ExpressRoute circuit charges and charges required by the connectivity provider.</span></span>

## <a name="expressroute-for-office-365-and-dynamics-365"></a><span data-ttu-id="7664d-309">Office 365 및 Dynamics 365에 대한 ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="7664d-309">ExpressRoute for Office 365 and Dynamics 365</span></span>

[!INCLUDE [expressroute-office365-include](../../includes/expressroute-office365-include.md)]

### <a name="how-do-i-create-an-expressroute-circuit-to-connect-to-office-365-services-and-dynamics-365"></a><span data-ttu-id="7664d-310">Office 365 서비스 및 Dynamics 365에 연결하려면 어떻게 ExpressRoute 회로를 만드나요?</span><span class="sxs-lookup"><span data-stu-id="7664d-310">How do I create an ExpressRoute circuit to connect to Office 365 services and Dynamics 365?</span></span>

1. <span data-ttu-id="7664d-311">[ExpressRoute 필수 구성 요소 페이지](expressroute-prerequisites.md)를 검토하여 요구 사항을 충족하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-311">Review the [ExpressRoute prerequisites page](expressroute-prerequisites.md) to make sure you meet the requirements.</span></span>
2. <span data-ttu-id="7664d-312">사용자 연결 요구 사항이 충족되는지 확인하려면 [ExpressRoute 파트너 및 위치](expressroute-locations.md) 문서에서 서비스 공급자 및 위치 목록을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-312">To ensure that your connectivity needs are met, review the list of service providers and locations in the [ExpressRoute partners and locations](expressroute-locations.md) article.</span></span>
3. <span data-ttu-id="7664d-313">[Office 365에 대한 네트워크 계획 및 성능 튜닝](http://aka.ms/tune/)을 검토하여 용량 요구 사항을 계획합니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-313">Plan your capacity requirements by reviewing [Network planning and performance tuning for Office 365](http://aka.ms/tune/).</span></span>
4. <span data-ttu-id="7664d-314">[회로 프로비전 및 회로 상태에 대한 ExpressRoute 워크플로](expressroute-workflows.md)의 연결 설정 워크플로에 나열된 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-314">Follow the steps listed in the workflows to set up connectivity [ExpressRoute workflows for circuit provisioning and circuit states](expressroute-workflows.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7664d-315">Office 365 서비스 및 Dynamics 365에 대한 연결을 구성할 때 ExpressRoute Premium 추가 기능을 사용하도록 설정했는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="7664d-315">Make sure that you have enabled ExpressRoute premium add-on when configuring connectivity to Office 365 services and Dynamics 365.</span></span>
> 
> 

### <a name="do-i-need-to-enable-azure-public-peering-to-connect-to-office-365-services-and-dynamics-365"></a><span data-ttu-id="7664d-316">Office 365 서비스 및 Dynamics 365에 연결하려면 Azure 공용 피어링을 사용하도록 설정해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="7664d-316">Do I need to enable Azure public peering to connect to Office 365 services and Dynamics 365?</span></span>

<span data-ttu-id="7664d-317">아니요, Microsoft 피어링을 사용하도록 설정하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-317">No, you only need to enable Microsoft Peering.</span></span> <span data-ttu-id="7664d-318">Azure AD에 대한 인증 트래픽은 Microsoft 피어링을 통해 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-318">Authentication traffic to Azure AD is sent through Microsoft Peering.</span></span> 

### <a name="can-my-existing-expressroute-circuits-support-connectivity-to-office-365-services-and-dynamics-365"></a><span data-ttu-id="7664d-319">기존 ExpressRoute 회로가 Office 365 서비스 및 Dynamics 365에 대한 연결을 지원할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="7664d-319">Can my existing ExpressRoute circuits support connectivity to Office 365 services and Dynamics 365?</span></span>

<span data-ttu-id="7664d-320">예.</span><span class="sxs-lookup"><span data-stu-id="7664d-320">Yes.</span></span> <span data-ttu-id="7664d-321">기존 ExpressRoute 회로가 Office 365 서비스에 대한 연결을 지원하도록 구성할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="7664d-321">Your existing ExpressRoute circuit can be configured to support connectivity to Office 365 services.</span></span> <span data-ttu-id="7664d-322">Office 365 서비스에 연결하는 데 충분한 용량이 있는지와 프리미엄 추가 기능을 사용하도록 설정했는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-322">Make sure that you have sufficient capacity to connect to Office 365 services and that you have enabled premium add-on.</span></span> <span data-ttu-id="7664d-323">[Office 365의 네트워크 계획 및 성능 조정](http://aka.ms/tune/)을 참조하면 연결 요구 사항을 계획할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-323">[Network planning and performance tuning for Office 365](http://aka.ms/tune/) helps you plan your connectivity needs.</span></span> <span data-ttu-id="7664d-324">[ExpressRoute 회로 만들기 및 수정](expressroute-howto-circuit-classic.md)도 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7664d-324">Also, see [Create and modify an ExpressRoute circuit](expressroute-howto-circuit-classic.md).</span></span>

### <a name="what-office-365-services-can-be-accessed-over-an-expressroute-connection"></a><span data-ttu-id="7664d-325">ExpressRoute 연결을 통해 어느 Office 365 서비스에 액세스할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="7664d-325">What Office 365 services can be accessed over an ExpressRoute connection?</span></span>

<span data-ttu-id="7664d-326">ExpressRoute에서 지원되는 최신 서비스 목록은 [Office 365 URL 및 IP 주소 범위](http://aka.ms/o365endpoints) 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7664d-326">Refer to [Office 365 URLs and IP address ranges](http://aka.ms/o365endpoints) page for an up-to-date list of services supported over ExpressRoute.</span></span>

### <a name="how-much-does-expressroute-for-office-365-services-and-dynamics-365-cost"></a><span data-ttu-id="7664d-327">Office 365 서비스 및 Dynamics 365용 ExpressRoute 비용은 얼마인가요?</span><span class="sxs-lookup"><span data-stu-id="7664d-327">How much does ExpressRoute for Office 365 services and Dynamics 365 cost?</span></span>

<span data-ttu-id="7664d-328">Office 365 서비스 및 Dynamics 365를 사용하려면 프리미엄 추가 기능을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-328">Office 365 services and Dynamics 365 require premium add-on to be enabled.</span></span> <span data-ttu-id="7664d-329">자세한 내용은 [가격 세부 정보 페이지](https://azure.microsoft.com/pricing/details/expressroute/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7664d-329">See the [pricing details page](https://azure.microsoft.com/pricing/details/expressroute/) for costs.</span></span>

### <a name="what-regions-is-expressroute-for-office-365-supported-in"></a><span data-ttu-id="7664d-330">Office 365용 ExpressRoute가 지원하는 영역</span><span class="sxs-lookup"><span data-stu-id="7664d-330">What regions is ExpressRoute for Office 365 supported in?</span></span>

<span data-ttu-id="7664d-331">[ExpressRoute 파트너 및 위치](expressroute-locations.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7664d-331">See [ExpressRoute partners and locations](expressroute-locations.md) for information.</span></span>

### <a name="can-i-access-office-365-over-the-internet-even-if-expressroute-was-configured-for-my-organization"></a><span data-ttu-id="7664d-332">ExpressRoute가 내 조직에 구성되어 있더라도 인터넷을 통해 Office 365에 액세스할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="7664d-332">Can I access Office 365 over the Internet, even if ExpressRoute was configured for my organization?</span></span>

<span data-ttu-id="7664d-333">예.</span><span class="sxs-lookup"><span data-stu-id="7664d-333">Yes.</span></span> <span data-ttu-id="7664d-334">ExpressRoute가 네트워크에 구성되어 있더라도 인터넷을 통해 Office 365 서비스 끝점에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-334">Office 365 service endpoints are reachable through the Internet, even though ExpressRoute has been configured for your network.</span></span> <span data-ttu-id="7664d-335">ExpressRoute를 통해 Office 365 서비스에 연결하도록 구성된 위치에 있는 경우 ExpressRoute를 통해 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-335">If you are in a location that is configured to connect to Office 365 services through ExpressRoute, you will connect through ExpressRoute.</span></span>

### <a name="can-i-access-office-365-us-government-community-gcc-services-over-an-azure-us-government-expressroute-circuit"></a><span data-ttu-id="7664d-336">Azure 미국 정부 ExpressRoute 회로를 통해 Office 365 미국 정부 커뮤니티(GCC) 서비스에 액세스할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="7664d-336">Can I access Office 365 US Government Community (GCC) services over an Azure US Government ExpressRoute circuit?</span></span>

<span data-ttu-id="7664d-337">예.</span><span class="sxs-lookup"><span data-stu-id="7664d-337">Yes.</span></span> <span data-ttu-id="7664d-338">Office 365 GCC 서비스 끝점은 Azure 미국 정부 ExpressRoute를 통해 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-338">Office 365 GCC service endpoints are reachable through the Azure US Government ExpressRoute.</span></span> <span data-ttu-id="7664d-339">그러나 먼저 Azure Portal에서 지원 티켓을 열어 Microsoft에 보급하려는 접두사를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-339">However, you first need to open a support ticket on the Azure portal to provide the prefixes you intend to advertise to Microsoft.</span></span> <span data-ttu-id="7664d-340">지원 티켓이 확인된 후 Office 365 GCC 서비스로의 연결이 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-340">Your connectivity to Office 365 GCC services will be established after the support ticket is resolved.</span></span> 

### <a name="can-dynamics-365-for-operations-formerly-known-as-dynamics-ax-online-be-accessed-over-an-expressroute-connection"></a><span data-ttu-id="7664d-341">ExpressRoute 연결을 통해 Dynamics 365 for Operations(이전의 Dynamics AX Online)에 액세스할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="7664d-341">Can Dynamics 365 for Operations (formerly known as Dynamics AX Online) be accessed over an ExpressRoute connection?</span></span>

<span data-ttu-id="7664d-342">예.</span><span class="sxs-lookup"><span data-stu-id="7664d-342">Yes.</span></span> <span data-ttu-id="7664d-343">[Dynamics 365 for Operations](https://www.microsoft.com/dynamics365/operations)가 Azure에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-343">[Dynamics 365 for Operations](https://www.microsoft.com/dynamics365/operations) is hosted on Azure.</span></span> <span data-ttu-id="7664d-344">연결할 ExpressRoute 회로에서 Azure 공용 피어링을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-344">You can enable Azure public peering on your ExpressRoute circuit to connect to it.</span></span>

## <a name="route-filters-for-microsoft-peering"></a><span data-ttu-id="7664d-345">Microsoft 피어링용 경로 필터</span><span class="sxs-lookup"><span data-stu-id="7664d-345">Route filters for Microsoft peering</span></span>

### <a name="i-am-turning-on-microsoft-peering-for-the-first-time-what-routes-will-i-see"></a><span data-ttu-id="7664d-346">Microsoft 피어링을 처음 설정해 봅니다. 어떤 경로를 확인해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="7664d-346">I am turning on Microsoft peering for the first time, what routes will I see?</span></span>

<span data-ttu-id="7664d-347">경로는 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-347">You will not see any routes.</span></span> <span data-ttu-id="7664d-348">접두사 보급을 시작하려면 회로에 경로 필터를 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-348">You have to attach a route filter to your circuit to start prefix advertisements.</span></span> <span data-ttu-id="7664d-349">자세한 내용은 [Microsoft 피어링용 경로 필터 구성](how-to-routefilter-powershell.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7664d-349">For instructions, see [Configure route filters for Microsoft peering](how-to-routefilter-powershell.md).</span></span>

### <a name="i-turned-on-microsoft-peering-and-now-i-am-trying-to-select-exchange-online-but-it-is-giving-me-an-error-that-i-am-not-authorized-to-do-it"></a><span data-ttu-id="7664d-350">Microsoft 피어링을 사용하도록 설정했고, 지금은 Exchange Online을 선택하려고 했지만 이 작업을 수행할 권한이 없다는 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-350">I turned on Microsoft peering and now I am trying to select Exchange Online, but it is giving me an error that I am not authorized to do it.</span></span>

<span data-ttu-id="7664d-351">경로 필터를 사용하면 모든 고객이 Microsoft 피어링을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-351">When using route filters, any customer can turn on Microsoft peering.</span></span> <span data-ttu-id="7664d-352">그러나 Office 365 서비스를 사용하려면 여전히 Office 365에서 권한을 부여받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-352">However, for consuming Office 365 services, you still need to get authorized by Office 365.</span></span>

### <a name="do-i-need-to-get-authorization-for-turning-on-dynamics-365-over-microsoft-peering"></a><span data-ttu-id="7664d-353">Microsoft 피어링을 통해 Dynamics 365를 설정하는 경우 필요한 권한을 부여받아야 하나요?</span><span class="sxs-lookup"><span data-stu-id="7664d-353">Do I need to get authorization for turning on Dynamics 365 over Microsoft peering?</span></span>

<span data-ttu-id="7664d-354">아니요, Dynamics 365에 대해 권한을 부여받을 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-354">No, you do not need authorization for Dynamics 365.</span></span> <span data-ttu-id="7664d-355">규칙을 만든 다음, 권한을 부여받지 않고 Dynamics 365 커뮤니티를 선택하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-355">You can create a rule and select Dynamics 365 community without authorization.</span></span>

### <a name="i-already-have-microsoft-peering-how-can-i-take-advantage-of-route-filters"></a><span data-ttu-id="7664d-356">Microsoft 피어링을 이미 사용하고 있습니다. 경로 필터를 사용하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="7664d-356">I already have Microsoft peering, how can I take advantage of route filters?</span></span>

<span data-ttu-id="7664d-357">경로 필터를 만들고, 사용할 서비스를 선택하고, 해당 필터를 Microsoft 피어링에 연결하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-357">You can create a route filter, select the services you want to use, and attach the filter to your Microsoft peering.</span></span> <span data-ttu-id="7664d-358">자세한 내용은 [Microsoft 피어링용 경로 필터 구성](how-to-routefilter-powershell.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7664d-358">For instructions, see [Configure route filters for Microsoft peering](how-to-routefilter-powershell.md).</span></span>

### <a name="i-have-microsoft-peering-at-one-location-now-i-am-trying-to-enable-it-at-another-location-and-i-am-not-seeing-any-prefixes"></a><span data-ttu-id="7664d-359">한 위치에서 Microsoft 피어링을 사용하고 있습니다. 이제 다른 위치에서 사용하도록 설정하려고 했지만 접두사가 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-359">I have Microsoft peering at one location, now I am trying to enable it at another location and I am not seeing any prefixes.</span></span>

* <span data-ttu-id="7664d-360">경로 필터를 정의하지 않은 경우에도 2017년 8월 1일 이전에 구성된 ExpressRoute 회로의 Microsoft 피어링에는 Microsoft 피어링을 통해 보급된 모든 서비스 접두사가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-360">Microsoft peering of ExpressRoute circuits that were configured prior to August 1, 2017 will have all service prefixes advertised through Microsoft peering, even if route filters are not defined.</span></span>

* <span data-ttu-id="7664d-361">2017년 8월 1일 이후에 구성되는 ExpressRoute 회로의 Microsoft 피어링에는 경로 필터를 회로에 연결할 때까지 접두사가 보급되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-361">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached to the circuit.</span></span> <span data-ttu-id="7664d-362">접두사는 기본적으로 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7664d-362">You will see no prefixes by default.</span></span>

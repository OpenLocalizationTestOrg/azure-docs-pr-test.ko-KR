---
title: "ExpressRoute 연결 모델: 네트워크 서비스 공급자, Exchange 및 이더넷 공급자를 통해 Microsoft Azure에 연결 | Microsoft Docs"
description: "이 문서는 고객 네트워크와 Microsoft Azure, Office 365 및 Dynamics 365 사이의 다양한 연결 모드를 설명합니다. 고객은 MPLS 공급자, 클라우드 Exchange 및 이더넷 공급자를 사용할 수 있습니다."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/09/2017
ms.author: cherylmc
ms.openlocfilehash: 00f97da2189491103c461b49ac82feb92d8f4b9b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="expressroute-connectivity-models"></a><span data-ttu-id="439f7-104">ExpressRoute 연결 모델</span><span class="sxs-lookup"><span data-stu-id="439f7-104">ExpressRoute connectivity models</span></span>
<span data-ttu-id="439f7-105">온-프레미스 네트워크와 Microsoft 클라우드 간 연결은 [CloudExchange 공동 배치](#CloudExchange), [지점 간 이더넷 연결](#Ethernet) 및 [임의(IPVPN) 연결](#IPVPN)이라는 세 가지 방법으로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="439f7-105">You can create a connection between your on-premises network and the Microsoft cloud in three different ways, [CloudExchange Co-location](#CloudExchange), [Point-to-point Ethernet Connection](#Ethernet), and [Any-to-any (IPVPN) Connection](#IPVPN).</span></span> <span data-ttu-id="439f7-106">연결 공급자는 하나 이상의 연결 모델을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="439f7-106">Connectivity providers can offer one or more connectivity models.</span></span> <span data-ttu-id="439f7-107">연결 공급자로 작업하여 사용자에게 적합한 다양한 모델을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="439f7-107">You can work with your connectivity provider to pick the model that works best for you.</span></span>
<br><br>

![ExpressRoute 연결 모델 다이어그램](./media/expressroute-connectivity-models/expressroute-connectivity-models-diagram.png)

## <span data-ttu-id="439f7-109"><a name="CloudExchange"></a>클라우드 Exchange에 배치</span><span class="sxs-lookup"><span data-stu-id="439f7-109"><a name="CloudExchange"></a>Co-located at a cloud exchange</span></span>
<span data-ttu-id="439f7-110">클라우드 Exchange를 사용하여 설비에 공존하는 경우 공동 배치 공급자의 이더넷 Exchange를 통해 Microsoft 클라우드로 가상 간 연결을 나열할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="439f7-110">If you are co-located in a facility with a cloud exchange, you can order virtual cross-connections to the Microsoft cloud through the co-location provider’s Ethernet exchange.</span></span> <span data-ttu-id="439f7-111">공동 배치 공급자는 공동 시설의 인프라와 Microsoft 클라우드 간에 2계층 간 연결 또는 관리된 3계층 간 연결을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="439f7-111">Co-location providers can offer either Layer 2 cross-connections, or managed Layer 3 cross-connections between your infrastructure in the co-location facility and the Microsoft cloud.</span></span>

## <span data-ttu-id="439f7-112"><a name="Ethernet"></a>지점 간 이더넷 연결</span><span class="sxs-lookup"><span data-stu-id="439f7-112"><a name="Ethernet"></a>Point-to-point Ethernet connections</span></span>
<span data-ttu-id="439f7-113">지점 간 이더넷 연결을 통해 온-프레미스 데이터 센터/사무소를 Microsoft 클라우드에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="439f7-113">You can connect your on-premises datacenters/offices to the Microsoft cloud through point-to-point Ethernet links.</span></span> <span data-ttu-id="439f7-114">지점 간 이더넷 공급자는 사이트와 Microsoft 클라우드 간에 2계층 연결 또는 관리된 3계층 연결을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="439f7-114">Point-to-point Ethernet providers can offer Layer 2 connections, or managed Layer 3 connections between your site and the Microsoft cloud.</span></span>

## <span data-ttu-id="439f7-115"><a name="IPVPN"></a>임의(IPVPN)의 네트워크</span><span class="sxs-lookup"><span data-stu-id="439f7-115"><a name="IPVPN"></a>Any-to-any (IPVPN) networks</span></span>
<span data-ttu-id="439f7-116">Microsoft 클라우드로 WAN을 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="439f7-116">You can integrate your WAN with the Microsoft cloud.</span></span> <span data-ttu-id="439f7-117">IPVPN 공급자(일반적으로 MPLS VPN)는 지사 및 데이터 센터 간에 임의의 연결을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="439f7-117">IPVPN providers (typically MPLS VPN) offer any-to-any connectivity between your branch offices and datacenters.</span></span> <span data-ttu-id="439f7-118">Microsoft 클라우드는 다른 지사와 마찬가지로 보이도록 WAN에 상호 연결될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="439f7-118">The Microsoft cloud can be interconnected to your WAN to make it look just like any other branch office.</span></span> <span data-ttu-id="439f7-119">WAN 공급자는 일반적으로 관리된 3계층 연결을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="439f7-119">WAN providers typically offer managed Layer 3 connectivity.</span></span> <span data-ttu-id="439f7-120">Express 경로 기능 및 특징은 위의 모든 연결 모델에 걸쳐 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="439f7-120">ExpressRoute capabilities and features are all identical across all of the above connectivity models.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="439f7-121">다음 단계</span><span class="sxs-lookup"><span data-stu-id="439f7-121">Next steps</span></span>
* <span data-ttu-id="439f7-122">Express 경로 연결 및 라우팅 도메인에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="439f7-122">Learn about ExpressRoute connections and routing domains.</span></span> <span data-ttu-id="439f7-123">[Express 경로 회로 및 라우팅 도메인](expressroute-circuit-peerings.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="439f7-123">See [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="439f7-124">ExpressRoute 기능에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="439f7-124">Learn about ExpressRoute features.</span></span> <span data-ttu-id="439f7-125">[ExpressRoute 기술 개요](expressroute-introduction.md) 참조</span><span class="sxs-lookup"><span data-stu-id="439f7-125">See the [ExpressRoute Technical Overview](expressroute-introduction.md)</span></span>
* <span data-ttu-id="439f7-126">서비스 공급자를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="439f7-126">Find a service provider.</span></span> <span data-ttu-id="439f7-127">[Express 경로 파트너 및 피어링 위치](expressroute-locations.md)를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="439f7-127">See [ExpressRoute partners and peering locations](expressroute-locations.md).</span></span>
* <span data-ttu-id="439f7-128">모든 필수 조건이 충족되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="439f7-128">Ensure that all prerequisites are met.</span></span> <span data-ttu-id="439f7-129">[Express 경로 필수 조건](expressroute-prerequisites.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="439f7-129">See [ExpressRoute prerequisites](expressroute-prerequisites.md).</span></span>
* <span data-ttu-id="439f7-130">[라우팅](expressroute-routing.md), [NAT](expressroute-nat.md) 및 [QoS](expressroute-qos.md)에 대한 요구 사항을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="439f7-130">Refer to the requirements for [Routing](expressroute-routing.md), [NAT](expressroute-nat.md), and [QoS](expressroute-qos.md).</span></span>
* <span data-ttu-id="439f7-131">Express 경로 연결을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="439f7-131">Configure your ExpressRoute connection.</span></span>
  * [<span data-ttu-id="439f7-132">ExpressRoute 회로 만들기</span><span class="sxs-lookup"><span data-stu-id="439f7-132">Create an ExpressRoute circuit</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
  * [<span data-ttu-id="439f7-133">라우팅 구성</span><span class="sxs-lookup"><span data-stu-id="439f7-133">Configure routing</span></span>](expressroute-howto-routing-portal-resource-manager.md)
  * [<span data-ttu-id="439f7-134">VNet을 ExpressRoute 회로에 연결</span><span class="sxs-lookup"><span data-stu-id="439f7-134">Link a VNet to an ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
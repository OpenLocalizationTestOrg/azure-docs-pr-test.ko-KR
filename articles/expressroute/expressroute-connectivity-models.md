---
title: "ExpressRoute 연결 모델: 네트워크 서비스 공급자, 교환 및 이더넷 공급자를 통해 Azure tooMicrosoft 연결 | Microsoft Docs"
description: "이 문서에서는 hello 고객 네트워크 및 Microsoft Azure, Office 365, Dynamics 365 서비스 간의 연결의 hello 다양 한 모드를 설명 합니다. 고객은 MPLS 공급자, 클라우드 Exchange 및 이더넷 공급자를 사용할 수 있습니다."
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
ms.openlocfilehash: 2682e6e45b2892869068f132bedb4bb08e3f89a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-connectivity-models"></a><span data-ttu-id="ef0e2-104">ExpressRoute 연결 모델</span><span class="sxs-lookup"><span data-stu-id="ef0e2-104">ExpressRoute connectivity models</span></span>
<span data-ttu-id="ef0e2-105">세 가지 방법으로 hello Microsoft 클라우드 및 온-프레미스 네트워크 간의 연결을 만들 수 [CloudExchange 공동 배치](#CloudExchange), [지점 간 이더넷 연결](#Ethernet), 및 [Any-에-any (IPVPN) 연결](#IPVPN)합니다.</span><span class="sxs-lookup"><span data-stu-id="ef0e2-105">You can create a connection between your on-premises network and hello Microsoft cloud in three different ways, [CloudExchange Co-location](#CloudExchange), [Point-to-point Ethernet Connection](#Ethernet), and [Any-to-any (IPVPN) Connection](#IPVPN).</span></span> <span data-ttu-id="ef0e2-106">연결 공급자는 하나 이상의 연결 모델을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef0e2-106">Connectivity providers can offer one or more connectivity models.</span></span> <span data-ttu-id="ef0e2-107">적합 한 사용자 연결 공급자 toopick hello 모델을 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef0e2-107">You can work with your connectivity provider toopick hello model that works best for you.</span></span>
<br><br>

![ExpressRoute 연결 모델 다이어그램](./media/expressroute-connectivity-models/expressroute-connectivity-models-diagram.png)

## <span data-ttu-id="ef0e2-109"><a name="CloudExchange"></a>클라우드 Exchange에 배치</span><span class="sxs-lookup"><span data-stu-id="ef0e2-109"><a name="CloudExchange"></a>Co-located at a cloud exchange</span></span>
<span data-ttu-id="ef0e2-110">클라우드 exchange와 본사에 공존 하는 경우에 가상 교차 연결 toohello hello 공동 배치 공급자의 이더넷 교환을 통해 Microsoft 클라우드를 주문할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef0e2-110">If you are co-located in a facility with a cloud exchange, you can order virtual cross-connections toohello Microsoft cloud through hello co-location provider’s Ethernet exchange.</span></span> <span data-ttu-id="ef0e2-111">공동 배치 공급자 계층 2 교차 연결 또는 관리 되는 계층 3 간에 교차 연결 hello 공동 배치 시설에서 인프라 및 hello Microsoft 클라우드를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef0e2-111">Co-location providers can offer either Layer 2 cross-connections, or managed Layer 3 cross-connections between your infrastructure in hello co-location facility and hello Microsoft cloud.</span></span>

## <span data-ttu-id="ef0e2-112"><a name="Ethernet"></a>지점 간 이더넷 연결</span><span class="sxs-lookup"><span data-stu-id="ef0e2-112"><a name="Ethernet"></a>Point-to-point Ethernet connections</span></span>
<span data-ttu-id="ef0e2-113">지점 간 이더넷 링크를 통해 온-프레미스 데이터 센터/사무실 toohello Microsoft 클라우드를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef0e2-113">You can connect your on-premises datacenters/offices toohello Microsoft cloud through point-to-point Ethernet links.</span></span> <span data-ttu-id="ef0e2-114">지점 간 이더넷 공급자 계층 2 연결을 제공할 수 있습니다 또는 관리 되는 사이트와 hello Microsoft 클라우드 간에 계층 3 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef0e2-114">Point-to-point Ethernet providers can offer Layer 2 connections, or managed Layer 3 connections between your site and hello Microsoft cloud.</span></span>

## <span data-ttu-id="ef0e2-115"><a name="IPVPN"></a>임의(IPVPN)의 네트워크</span><span class="sxs-lookup"><span data-stu-id="ef0e2-115"><a name="IPVPN"></a>Any-to-any (IPVPN) networks</span></span>
<span data-ttu-id="ef0e2-116">Microsoft 클라우드 hello로 WAN을 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef0e2-116">You can integrate your WAN with hello Microsoft cloud.</span></span> <span data-ttu-id="ef0e2-117">IPVPN 공급자(일반적으로 MPLS VPN)는 지사 및 데이터 센터 간에 임의의 연결을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ef0e2-117">IPVPN providers (typically MPLS VPN) offer any-to-any connectivity between your branch offices and datacenters.</span></span> <span data-ttu-id="ef0e2-118">Microsoft 클라우드 상호 연결 된 tooyour WAN toomake 것 바로 보일 수 hello 같은 다른 지점입니다.</span><span class="sxs-lookup"><span data-stu-id="ef0e2-118">hello Microsoft cloud can be interconnected tooyour WAN toomake it look just like any other branch office.</span></span> <span data-ttu-id="ef0e2-119">WAN 공급자는 일반적으로 관리된 3계층 연결을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ef0e2-119">WAN providers typically offer managed Layer 3 connectivity.</span></span> <span data-ttu-id="ef0e2-120">Express 경로 기능 및 특징은 모든 연결 모델 위에 hello 모두 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef0e2-120">ExpressRoute capabilities and features are all identical across all of hello above connectivity models.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="ef0e2-121">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ef0e2-121">Next steps</span></span>
* <span data-ttu-id="ef0e2-122">Express 경로 연결 및 라우팅 도메인에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ef0e2-122">Learn about ExpressRoute connections and routing domains.</span></span> <span data-ttu-id="ef0e2-123">[Express 경로 회로 및 라우팅 도메인](expressroute-circuit-peerings.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ef0e2-123">See [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="ef0e2-124">ExpressRoute 기능에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ef0e2-124">Learn about ExpressRoute features.</span></span> <span data-ttu-id="ef0e2-125">Hello 참조 [express 경로 기술 개요](expressroute-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="ef0e2-125">See hello [ExpressRoute Technical Overview](expressroute-introduction.md)</span></span>
* <span data-ttu-id="ef0e2-126">서비스 공급자를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="ef0e2-126">Find a service provider.</span></span> <span data-ttu-id="ef0e2-127">[Express 경로 파트너 및 피어링 위치](expressroute-locations.md)를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="ef0e2-127">See [ExpressRoute partners and peering locations](expressroute-locations.md).</span></span>
* <span data-ttu-id="ef0e2-128">모든 필수 조건이 충족되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ef0e2-128">Ensure that all prerequisites are met.</span></span> <span data-ttu-id="ef0e2-129">[ExpressRoute 필수 조건](expressroute-prerequisites.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ef0e2-129">See [ExpressRoute prerequisites](expressroute-prerequisites.md).</span></span>
* <span data-ttu-id="ef0e2-130">Toohello 요구 사항에 대 한 참조 [라우팅](expressroute-routing.md), [NAT](expressroute-nat.md), 및 [QoS](expressroute-qos.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ef0e2-130">Refer toohello requirements for [Routing](expressroute-routing.md), [NAT](expressroute-nat.md), and [QoS](expressroute-qos.md).</span></span>
* <span data-ttu-id="ef0e2-131">ExpressRoute 연결을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="ef0e2-131">Configure your ExpressRoute connection.</span></span>
  * [<span data-ttu-id="ef0e2-132">ExpressRoute 회로 만들기</span><span class="sxs-lookup"><span data-stu-id="ef0e2-132">Create an ExpressRoute circuit</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
  * [<span data-ttu-id="ef0e2-133">라우팅 구성</span><span class="sxs-lookup"><span data-stu-id="ef0e2-133">Configure routing</span></span>](expressroute-howto-routing-portal-resource-manager.md)
  * [<span data-ttu-id="ef0e2-134">VNet tooan ExpressRoute 회로 연결</span><span class="sxs-lookup"><span data-stu-id="ef0e2-134">Link a VNet tooan ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)

---
title: "aaaWhat Azure 릴레이 이며 왜 사용 개요 | Microsoft Docs"
description: "Azure 릴레이 개요"
services: service-bus-relay
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 1e3e971d-2a24-4f96-a88a-ce3ea2b1a1cd
ms.service: service-bus-relay
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: get-started-article
ms.date: 08/23/2017
ms.author: sethm
ms.openlocfilehash: 4cfd77048210a435c446b908b7896737cad0edbf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-relay"></a><span data-ttu-id="69832-103">Azure 릴레이란?</span><span class="sxs-lookup"><span data-stu-id="69832-103">What is Azure Relay?</span></span>

<span data-ttu-id="69832-104">hello Azure 릴레이 서비스에 하이브리드 toosecurely 있습니다를 사용 하 여 응용 프로그램 방화벽 연결 tooopen 필요 없이 회사의 엔터프라이즈 네트워크 toohello 공용 클라우드 내에 있는 서비스를 노출 하거나 침입적 인 필요로 용이 하 게 tooa 변경 회사 네트워크 인프라입니다.</span><span class="sxs-lookup"><span data-stu-id="69832-104">hello Azure Relay service facilitates hybrid applications by enabling you toosecurely expose services that reside within a corporate enterprise network toohello public cloud, without having tooopen a firewall connection, or require intrusive changes tooa corporate network infrastructure.</span></span> <span data-ttu-id="69832-105">릴레이는 다양한 전송 프로토콜 및 웹 서비스 표준을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="69832-105">Relay supports a variety of different transport protocols and web services standards.</span></span>

<span data-ttu-id="69832-106">hello 릴레이 서비스는 기존의 단방향, 요청/응답, 및 피어-투-피어 트래픽을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="69832-106">hello relay service supports traditional one-way, request/response, and peer-to-peer traffic.</span></span> <span data-ttu-id="69832-107">또한 인터넷 범위 tooenable 게시/구독 시나리오 및 양방향 소켓 통신에서 배포를 이벤트 분산과 지점 간 효율성에 대 한 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="69832-107">It also supports event distribution at internet-scope tooenable publish/subscribe scenarios and bi-directional socket communication for increased point-to-point efficiency.</span></span> 

<span data-ttu-id="69832-108">Hello 헤더 블록이 릴레이 데이터를 전송 하는 패턴에서 온-프레미스 서비스 toohello 릴레이 서비스는 아웃 바운드 포트를 통해 연결 하 고 연결 된 통신 tooa 특정 랑 데 부 주소에 대 한 양방향 소켓을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="69832-108">In hello relayed data transfer pattern, an on-premises service connects toohello relay service through an outbound port and creates a bi-directional socket for communication tied tooa particular rendezvous address.</span></span> <span data-ttu-id="69832-109">클라이언트 hello 다음 트래픽 toohello 릴레이 서비스 hello 랑 데 부 주소를 대상으로 전송 하 여 hello 온-프레미스 서비스와 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69832-109">hello client can then communicate with hello on-premises service by sending traffic toohello relay service targeting hello rendezvous address.</span></span> <span data-ttu-id="69832-110">hello 릴레이 서비스 다음 "릴레이" 양방향 소켓 전용된 tooeach 클라이언트를 통해 데이터 toohello 온-프레미스 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="69832-110">hello relay service then "relays" data toohello on-premises service through a bi-directional socket dedicated tooeach client.</span></span> <span data-ttu-id="69832-111">hello 클라이언트 필요가 없는 직접 연결 toohello 온-프레미스 서비스, 필요한 tooknow 여기서 hello 서비스가 상주 하 고 hello 온-프레미스 서비스는 인바운드 포트가 필요 없는 hello 방화벽에서 열려 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69832-111">hello client does not need a direct connection toohello on-premises service, it is not required tooknow where hello service resides, and hello on-premises service does not need any inbound ports open on hello firewall.</span></span>

<span data-ttu-id="69832-112">릴레이에서 제공 하는 hello 키 기능 요소는 양방향, 버퍼링 되지 않은 통신 TCP와 유사한 제한, 끝점 검색, 연결 상태를 사용 하 여 네트워크 경계 및에서 끝점 보안을 중첩 합니다.</span><span class="sxs-lookup"><span data-stu-id="69832-112">hello key capability elements provided by Relay are bi-directional, unbuffered communication across network boundaries with TCP-like throttling, endpoint discovery, connectivity status, and overlaid endpoint security.</span></span> <span data-ttu-id="69832-113">hello 릴레이 기능 VPN과 같은 네트워크 수준의 통합 기술에서 다를 해당 릴레이에 될 수 있습니다는 단일 컴퓨터에서 단일 응용 프로그램 끝점 범위 지정 된 tooa VPN 기술이 hello 네트워크 환경 변경 하므로 훨씬 더 개입 수준이 문제 .</span><span class="sxs-lookup"><span data-stu-id="69832-113">hello relay capabilities differ from network-level integration technologies such as VPN, in that relay can be scoped tooa single application endpoint on a single machine, while VPN technology is far more intrusive as it relies on altering hello network environment.</span></span>

<span data-ttu-id="69832-114">Azure 릴레이에는 다음과 같은 두 가지 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69832-114">Azure Relay has two features:</span></span>

1. <span data-ttu-id="69832-115">[하이브리드 연결](#hybrid-connections) -사용 하 여 hello open 표준 웹 소켓 다중 플랫폼 시나리오를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="69832-115">[Hybrid Connections](#hybrid-connections) - Uses hello open standard web sockets enabling multi-platform scenarios.</span></span>
2. <span data-ttu-id="69832-116">[WCF 릴레이](#wcf-relays) -tooenable 원격 프로시저 호출을 사용 하 여 Windows Communication Foundation (WCF).</span><span class="sxs-lookup"><span data-stu-id="69832-116">[WCF Relays](#wcf-relays) - Uses Windows Communication Foundation (WCF) tooenable remote procedure calls.</span></span> <span data-ttu-id="69832-117">WCF 릴레이 많은 고객이 이미 프로그래밍 모델의 WCF와 함께 사용 하는 제공 하는 hello 레거시 릴레이입니다.</span><span class="sxs-lookup"><span data-stu-id="69832-117">WCF Relay is hello legacy relay offering that many customers already use with their WCF programming models.</span></span>

<span data-ttu-id="69832-118">하이브리드 연결 및 WCF 릴레이 회사의 엔터프라이즈 네트워크 내에 존재 하는 보안 연결 tooassets 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="69832-118">Hybrid Connections and WCF Relays both enable secure connection tooassets that exist within a corporate enterprise network.</span></span> <span data-ttu-id="69832-119">다른 hello 이들 중 한 가지의 사용은 다음 표에 hello에 설명 된 대로 특정 요구 사항에 종속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69832-119">Use of one over hello other is dependent on your particular needs, as described in hello following table:</span></span>

|  | <span data-ttu-id="69832-120">WCF 릴레이</span><span class="sxs-lookup"><span data-stu-id="69832-120">WCF Relay</span></span> | <span data-ttu-id="69832-121">하이브리드 연결</span><span class="sxs-lookup"><span data-stu-id="69832-121">Hybrid Connections</span></span> |
| --- |:---:|:---:|
| <span data-ttu-id="69832-122">**WCF**</span><span class="sxs-lookup"><span data-stu-id="69832-122">**WCF**</span></span> |<span data-ttu-id="69832-123">x</span><span class="sxs-lookup"><span data-stu-id="69832-123">x</span></span> | |
| <span data-ttu-id="69832-124">**.NET Core**</span><span class="sxs-lookup"><span data-stu-id="69832-124">**.NET Core**</span></span> | |<span data-ttu-id="69832-125">x</span><span class="sxs-lookup"><span data-stu-id="69832-125">x</span></span> |
| <span data-ttu-id="69832-126">**.NET Framework**</span><span class="sxs-lookup"><span data-stu-id="69832-126">**.NET Framework**</span></span> |<span data-ttu-id="69832-127">x</span><span class="sxs-lookup"><span data-stu-id="69832-127">x</span></span> |<span data-ttu-id="69832-128">x</span><span class="sxs-lookup"><span data-stu-id="69832-128">x</span></span> |
| <span data-ttu-id="69832-129">**JavaScript/NodeJS**</span><span class="sxs-lookup"><span data-stu-id="69832-129">**JavaScript/NodeJS**</span></span> | |<span data-ttu-id="69832-130">x</span><span class="sxs-lookup"><span data-stu-id="69832-130">x</span></span> |
| <span data-ttu-id="69832-131">**표준 기반 개방형 프로토콜**</span><span class="sxs-lookup"><span data-stu-id="69832-131">**Standards-Based Open Protocol**</span></span> | |<span data-ttu-id="69832-132">x</span><span class="sxs-lookup"><span data-stu-id="69832-132">x</span></span> |
| <span data-ttu-id="69832-133">**여러 RPC 프로그래밍 모델**</span><span class="sxs-lookup"><span data-stu-id="69832-133">**Multiple RPC Programming Models**</span></span> | |<span data-ttu-id="69832-134">x</span><span class="sxs-lookup"><span data-stu-id="69832-134">x</span></span> |

## <a name="hybrid-connections"></a><span data-ttu-id="69832-135">하이브리드 연결</span><span class="sxs-lookup"><span data-stu-id="69832-135">Hybrid Connections</span></span>

<span data-ttu-id="69832-136">hello [Azure 릴레이 하이브리드 연결](relay-hybrid-connections-protocol.md) 기능은 어떤 플랫폼에서 고가 기본 WebSocket 기능을 모든 언어에서 구현할 수 있는 릴레이 기능을 기존 hello의 보안, 오픈 프로토콜 변화는 일반적인 웹 브라우저에서 WebSocket API hello를 명시적으로 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69832-136">hello [Azure Relay Hybrid Connections](relay-hybrid-connections-protocol.md) capability is a secure, open-protocol evolution of hello existing Relay features that can be implemented on any platform and in any language that has a basic WebSocket capability, which explicitly includes hello WebSocket API in common web browsers.</span></span> <span data-ttu-id="69832-137">하이브리드 연결은 HTTP 및 WebSockets를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="69832-137">Hybrid Connections is based on HTTP and WebSockets.</span></span>

### <a name="service-history"></a><span data-ttu-id="69832-138">서비스 변경 사항</span><span class="sxs-lookup"><span data-stu-id="69832-138">Service history</span></span>

<span data-ttu-id="69832-139">하이브리드 연결 hello 전자의 경우에 hello Azure 서비스 버스 WCF 릴레이 된 "BizTalk Services" 기능을 비슷한 이름의 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="69832-139">Hybrid Connections supplants hello former, similarly named "BizTalk Services" feature that was built on hello Azure Service Bus WCF Relay.</span></span> <span data-ttu-id="69832-140">hello 새 하이브리드 연결 기능 hello 기존 WCF 릴레이 기능을 보완 하 고 이러한 두 서비스 기능 나란히 hello Azure 릴레이 서비스에 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="69832-140">hello new Hybrid Connections capability complements hello existing WCF Relay feature and these two service capabilities exist side-by-side in hello Azure Relay service.</span></span> <span data-ttu-id="69832-141">일반적인 게이트웨이를 공유하지만 구현 방식은 서로 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="69832-141">They share a common gateway, but are otherwise different implementations.</span></span>

## <a name="wcf-relays"></a><span data-ttu-id="69832-142">WCF 릴레이</span><span class="sxs-lookup"><span data-stu-id="69832-142">WCF Relays</span></span>

<span data-ttu-id="69832-143">에 대 한 hello WCF 릴레이 works hello 전체.NET Framework (NETFX) 및 WCF에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="69832-143">hello WCF Relay works for hello full .NET Framework (NETFX) and for WCF.</span></span> <span data-ttu-id="69832-144">온-프레미스 서비스와 WCF "릴레이" 바인딩 집합을 사용 하 여 hello 릴레이 서비스 간의 hello 연결을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="69832-144">You initiate hello connection between your on-premises service and hello relay service using a suite of WCF "relay" bindings.</span></span> <span data-ttu-id="69832-145">Hello 백그라운드 hello 릴레이 바인딩은 toonew 전송 바인딩 요소 설계 toocreate WCF 채널 구성 요소를 hello 클라우드의 서비스 버스와 통합 하는 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="69832-145">Behind hello scenes, hello relay bindings map toonew transport binding elements designed toocreate WCF channel components that integrate with Service Bus in hello cloud.</span></span>

## <a name="architecture-processing-of-incoming-relay-requests"></a><span data-ttu-id="69832-146">아키텍처: 들어오는 릴레이 요청 처리</span><span class="sxs-lookup"><span data-stu-id="69832-146">Architecture: Processing of incoming relay requests</span></span>
<span data-ttu-id="69832-147">클라이언트 요청 toohello를 보낼 때 [Azure 릴레이](/azure/service-bus-relay/) hello Azure 부하 분산 장치가 서비스 hello 게이트웨이 노드 tooany 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="69832-147">When a client sends a request toohello [Azure Relay](/azure/service-bus-relay/) service, hello Azure load balancer routes it tooany of hello gateway nodes.</span></span> <span data-ttu-id="69832-148">Hello 요청은 수신 대기 요청 hello 게이트웨이 노드에 있습니다. 새 릴레이 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="69832-148">If hello request is a listening request, hello gateway node creates a new relay.</span></span> <span data-ttu-id="69832-149">Hello 요청이 연결 요청 tooa 특정 릴레이 인 경우 hello 게이트웨이 노드 hello 연결 요청 toohello 게이트웨이 소유한 노드에서 hello 릴레이 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="69832-149">If hello request is a connection request tooa specific relay, hello gateway node forwards hello connection request toohello gateway node that owns hello relay.</span></span> <span data-ttu-id="69832-150">hello 릴레이 소유 하는 hello 게이트웨이 노드는 랑 데 부 요청 toohello 수신 대기를 묻는 클라이언트를 hello 수신기 toocreate hello 연결 요청을 수신 하는 임시 채널 toohello 게이트웨이 노드를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="69832-150">hello gateway node that owns hello relay sends a rendezvous request toohello listening client, asking hello listener toocreate a temporary channel toohello gateway node that received hello connection request.</span></span>

<span data-ttu-id="69832-151">Hello 릴레이 연결이 설정 되 면 hello 클라이언트 hello rendezvous에 사용 되는 hello 게이트웨이 노드를 통해 메시지를 교환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69832-151">When hello relay connection is established, hello clients can exchange messages via hello gateway node that is used for hello rendezvous.</span></span>

![들어오는 WCF 릴레이 요청 처리](./media/relay-what-is-it/ic690645.png)

## <a name="next-steps"></a><span data-ttu-id="69832-153">다음 단계</span><span class="sxs-lookup"><span data-stu-id="69832-153">Next steps</span></span>

* [<span data-ttu-id="69832-154">릴레이 FAQ</span><span class="sxs-lookup"><span data-stu-id="69832-154">Relay FAQ</span></span>](relay-faq.md)
* [<span data-ttu-id="69832-155">네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="69832-155">Create a namespace</span></span>](relay-create-namespace-portal.md)
* [<span data-ttu-id="69832-156">.NET 시작</span><span class="sxs-lookup"><span data-stu-id="69832-156">Get started with .NET</span></span>](relay-hybrid-connections-dotnet-get-started.md)
* [<span data-ttu-id="69832-157">노드 시작</span><span class="sxs-lookup"><span data-stu-id="69832-157">Get started with Node</span></span>](relay-hybrid-connections-node-get-started.md)


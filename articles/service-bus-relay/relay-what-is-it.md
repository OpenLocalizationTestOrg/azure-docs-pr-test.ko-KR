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
# <a name="what-is-azure-relay"></a>Azure 릴레이란?

hello Azure 릴레이 서비스에 하이브리드 toosecurely 있습니다를 사용 하 여 응용 프로그램 방화벽 연결 tooopen 필요 없이 회사의 엔터프라이즈 네트워크 toohello 공용 클라우드 내에 있는 서비스를 노출 하거나 침입적 인 필요로 용이 하 게 tooa 변경 회사 네트워크 인프라입니다. 릴레이는 다양한 전송 프로토콜 및 웹 서비스 표준을 지원합니다.

hello 릴레이 서비스는 기존의 단방향, 요청/응답, 및 피어-투-피어 트래픽을 지원합니다. 또한 인터넷 범위 tooenable 게시/구독 시나리오 및 양방향 소켓 통신에서 배포를 이벤트 분산과 지점 간 효율성에 대 한 지원합니다. 

Hello 헤더 블록이 릴레이 데이터를 전송 하는 패턴에서 온-프레미스 서비스 toohello 릴레이 서비스는 아웃 바운드 포트를 통해 연결 하 고 연결 된 통신 tooa 특정 랑 데 부 주소에 대 한 양방향 소켓을 만듭니다. 클라이언트 hello 다음 트래픽 toohello 릴레이 서비스 hello 랑 데 부 주소를 대상으로 전송 하 여 hello 온-프레미스 서비스와 통신할 수 있습니다. hello 릴레이 서비스 다음 "릴레이" 양방향 소켓 전용된 tooeach 클라이언트를 통해 데이터 toohello 온-프레미스 서비스입니다. hello 클라이언트 필요가 없는 직접 연결 toohello 온-프레미스 서비스, 필요한 tooknow 여기서 hello 서비스가 상주 하 고 hello 온-프레미스 서비스는 인바운드 포트가 필요 없는 hello 방화벽에서 열려 있습니다.

릴레이에서 제공 하는 hello 키 기능 요소는 양방향, 버퍼링 되지 않은 통신 TCP와 유사한 제한, 끝점 검색, 연결 상태를 사용 하 여 네트워크 경계 및에서 끝점 보안을 중첩 합니다. hello 릴레이 기능 VPN과 같은 네트워크 수준의 통합 기술에서 다를 해당 릴레이에 될 수 있습니다는 단일 컴퓨터에서 단일 응용 프로그램 끝점 범위 지정 된 tooa VPN 기술이 hello 네트워크 환경 변경 하므로 훨씬 더 개입 수준이 문제 .

Azure 릴레이에는 다음과 같은 두 가지 기능이 있습니다.

1. [하이브리드 연결](#hybrid-connections) -사용 하 여 hello open 표준 웹 소켓 다중 플랫폼 시나리오를 사용 하도록 설정 합니다.
2. [WCF 릴레이](#wcf-relays) -tooenable 원격 프로시저 호출을 사용 하 여 Windows Communication Foundation (WCF). WCF 릴레이 많은 고객이 이미 프로그래밍 모델의 WCF와 함께 사용 하는 제공 하는 hello 레거시 릴레이입니다.

하이브리드 연결 및 WCF 릴레이 회사의 엔터프라이즈 네트워크 내에 존재 하는 보안 연결 tooassets 사용 하도록 설정 합니다. 다른 hello 이들 중 한 가지의 사용은 다음 표에 hello에 설명 된 대로 특정 요구 사항에 종속 됩니다.

|  | WCF 릴레이 | 하이브리드 연결 |
| --- |:---:|:---:|
| **WCF** |x | |
| **.NET Core** | |x |
| **.NET Framework** |x |x |
| **JavaScript/NodeJS** | |x |
| **표준 기반 개방형 프로토콜** | |x |
| **여러 RPC 프로그래밍 모델** | |x |

## <a name="hybrid-connections"></a>하이브리드 연결

hello [Azure 릴레이 하이브리드 연결](relay-hybrid-connections-protocol.md) 기능은 어떤 플랫폼에서 고가 기본 WebSocket 기능을 모든 언어에서 구현할 수 있는 릴레이 기능을 기존 hello의 보안, 오픈 프로토콜 변화는 일반적인 웹 브라우저에서 WebSocket API hello를 명시적으로 포함 됩니다. 하이브리드 연결은 HTTP 및 WebSockets를 기반으로 합니다.

### <a name="service-history"></a>서비스 변경 사항

하이브리드 연결 hello 전자의 경우에 hello Azure 서비스 버스 WCF 릴레이 된 "BizTalk Services" 기능을 비슷한 이름의 대신 합니다. hello 새 하이브리드 연결 기능 hello 기존 WCF 릴레이 기능을 보완 하 고 이러한 두 서비스 기능 나란히 hello Azure 릴레이 서비스에 존재 합니다. 일반적인 게이트웨이를 공유하지만 구현 방식은 서로 다릅니다.

## <a name="wcf-relays"></a>WCF 릴레이

에 대 한 hello WCF 릴레이 works hello 전체.NET Framework (NETFX) 및 WCF에 대 한 합니다. 온-프레미스 서비스와 WCF "릴레이" 바인딩 집합을 사용 하 여 hello 릴레이 서비스 간의 hello 연결을 시작 합니다. Hello 백그라운드 hello 릴레이 바인딩은 toonew 전송 바인딩 요소 설계 toocreate WCF 채널 구성 요소를 hello 클라우드의 서비스 버스와 통합 하는 매핑합니다.

## <a name="architecture-processing-of-incoming-relay-requests"></a>아키텍처: 들어오는 릴레이 요청 처리
클라이언트 요청 toohello를 보낼 때 [Azure 릴레이](/azure/service-bus-relay/) hello Azure 부하 분산 장치가 서비스 hello 게이트웨이 노드 tooany 라우팅합니다. Hello 요청은 수신 대기 요청 hello 게이트웨이 노드에 있습니다. 새 릴레이 만듭니다. Hello 요청이 연결 요청 tooa 특정 릴레이 인 경우 hello 게이트웨이 노드 hello 연결 요청 toohello 게이트웨이 소유한 노드에서 hello 릴레이 전달 합니다. hello 릴레이 소유 하는 hello 게이트웨이 노드는 랑 데 부 요청 toohello 수신 대기를 묻는 클라이언트를 hello 수신기 toocreate hello 연결 요청을 수신 하는 임시 채널 toohello 게이트웨이 노드를 보냅니다.

Hello 릴레이 연결이 설정 되 면 hello 클라이언트 hello rendezvous에 사용 되는 hello 게이트웨이 노드를 통해 메시지를 교환할 수 있습니다.

![들어오는 WCF 릴레이 요청 처리](./media/relay-what-is-it/ic690645.png)

## <a name="next-steps"></a>다음 단계

* [릴레이 FAQ](relay-faq.md)
* [네임스페이스 만들기](relay-create-namespace-portal.md)
* [.NET 시작](relay-hybrid-connections-dotnet-get-started.md)
* [노드 시작](relay-hybrid-connections-node-get-started.md)


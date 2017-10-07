---
title: "aaaAzure 서비스 버스 메시징 개요 | Microsoft Docs"
description: "Service Bus 메시지 및 Azure Relay에 대한 설명"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: f99766cb-8f4b-4baf-b061-4b1e2ae570e4
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: get-started-article
ms.date: 05/25/2017
ms.author: sethm
ms.openlocfilehash: ede2904e11544d8f9428a2d657dcc77dacd95ac4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-messaging-flexible-data-delivery-in-hello-cloud"></a>서비스 버스 메시징: hello 클라우드의 유연한 데이터 배달
Microsoft Azure Service Bus는 안정적인 정보 배달 서비스로, 이 서비스의 hello 목적은 toomake 통신을 보다 쉽게을 것입니다. 둘 이상의 파티 tooexchange 정보 시기 통신 촉진을 해야 합니다. Service Bus는 조정된 또는 타사 통신 메커니즘으로, Hello 실제 세계의 유사한 tooa 우편 서비스입니다. 우편 서비스를 통해 매우 쉽게 toosend 서로 다른 문자 및 다양 한 배달 보증을 사용 하 여 패키지의 아무 곳 이나의 hello world.

문자, 서비스 버스를 제공 하는 비슷한 toohello 우편 서비스는 hello 보낸 사람 및 받는 사람 hello 모두에서 유연한 정보 배달 합니다. 메시징 서비스는 hello 하면 hello 정보 hello 두 당사자는 모두 온라인 시간, 같거나 hello에 사용할 수 없는 경우 정확한 동일 hello에 경우에 배달는 시간입니다. 이러한 방식으로 메시징는 비슷한 toosending는 문자, 조정 된 비 통신은 비슷한 tooplacing 전화 통화 (또는 전화 통화 전에 조정 된 메시징 같은 보다 훨씬 호출 대기 및 발신자 ID toobe-를 사용 하는 방법).

hello 메시지 보낸 사람에 게 배달 특징 트랜잭션, 중복 검색, 시간 기반 만료를 포함 하 여 오케스트레이션 및 일괄 처리의 다양 한이 필요할 수도 있습니다. 이러한 패턴 역시 우편 서비스의 반복 배달, 서명 요청, 주소 변경, 회수 등과 비슷합니다.

Service Bus는 *Azure Relay*와 *Service Bus 메시지*의 두 가지 메시지 패턴을 지원합니다.

## <a name="azure-relay"></a>Azure Relay
hello [WCF 릴레이](../service-bus-relay/relay-what-is-it.md) Azure 릴레이의 구성 요소는 다양 한 전송 프로토콜을 지원 하는 중앙 집중식 (하지만 부하 분산이 뛰어난) 서비스 및 웹 서비스 표준입니다. 여기에는 SOAP, WS-* 및 REST가 포함됩니다. hello [릴레이 서비스](../service-bus-relay/service-bus-dotnet-how-to-use-relay.md) 다양 한 여러 릴레이 연결 옵션을 제공 하 고 가능한 경우 직접 피어-투-피어 연결을 협상 하는 데 도움이 됩니다. 서비스 버스는 hello WCF Windows Communication Foundation (), 큰지에 tooperformance 및 유용성을 모두 사용 하는.NET 개발자 용으로 최적화 하 고 모든 권한 tooits SOAP 및 REST 인터페이스를 통해 릴레이 서비스를 제공 합니다. 이렇게 하면 모든 SOAP 또는 REST 서비스 버스를 통해 환경 toointegrate 프로그래밍 가능 합니다.

hello 릴레이 서비스는 일반적인 단방향 메시징, 요청/응답 메시징 및 피어 투 피어 메시징을 지원 합니다. 이벤트 배포도 지원는 인터넷 범위의 tooenable 게시-구독 시나리오 및 분산과 지점 간 효율성에 대 한 양방향 소켓 통신 합니다. Hello 릴레이 된 메시징 패턴에서는 온-프레미스 서비스 toohello 릴레이 서비스는 아웃 바운드 포트를 통해 연결 하 고 연결 된 통신 tooa 특정 랑 데 부 주소에 대 한 양방향 소켓을 만듭니다. 클라이언트 hello 다음 toohello 릴레이 서비스 hello 랑 데 부 주소를 대상으로 메시지를 전송 하 여 hello 온-프레미스 서비스와 통신할 수 있습니다. hello 릴레이 서비스는 다음 "릴레이" 이미 있는 hello 양방향 소켓을 통해 메시지 toohello 온-프레미스 서비스입니다. hello 클라이언트 toohello 온-프레미스 서비스에 직접 연결 하지 않아도 없거나 이러한 속성이 필요한 it tooknow hello 서비스가 상주 하 고 hello 온-프레미스 서비스는 인바운드 포트가 필요 있는 hello 방화벽에서 열려 있습니다.

WCF "릴레이" 바인딩 집합을 사용 하 여 온-프레미스 서비스와 hello 릴레이 서비스 간의 hello 연결을 시작 합니다. Hello 백그라운드 hello 릴레이 바인딩은 tootransport 바인딩 요소 설계 toocreate WCF 채널 구성 요소 매핑 hello 클라우드의 서비스 버스와 통합 하는 합니다.

WCF 릴레이 다양 한 이점을 제공 하지만 필요 hello 서버 및 클라이언트 tooboth hello 동일한 순서 toosend 시간 메시지를 주고받을 온라인 상태 여야 합니다. HTTP 스타일 통신의 경우에 hello 요청 수 있습니다 일반적으로 수명이 긴 또는 모바일 응용 프로그램, 브라우저 등 가끔씩만 연결 하는 클라이언트에 대 한 최적의 아닙니다. 조정된 메시징은 분리된 통신을 지원하며, 클라이언트와 서버가 필요할 때 연결하고 비동기 방식으로 작업을 수행할 수 있는 고유한 이점이 있습니다.

## <a name="brokered-messaging"></a>조정된 메시징
Toohello 체계, 메시징, 서비스 버스 릴레이 하는 반면 또는 [조정 된 메시징](service-bus-queues-topics-subscriptions.md) "분리 시간적." 또는 비동기으로 생각할 수 있습니다 생산자 (보낸 사람)와 소비자 (받는 사람) toobe 온라인에 없는 hello 동시 합니다. hello 메시징 인프라를 안정적으로 저장 "브로커"에 있는 메시지 (예: 큐) hello 사용 중인 파티가 tooreceive 준비 될 때까지 해당 합니다. 이렇게 하면 연결이 해제 하거나 자발적으로; hello 분산 응용 프로그램 toobe의 hello 구성 요소 예를 들어, 유지 관리를 위해 또는 hello 전체 시스템 영향을 주지 않고 tooa 구성 요소 크래시 등 때문입니다. 또한 hello 수신 응용 프로그램은만 필요한 toorun에 있는 hello hello 업무 종료는 재고 관리 시스템 등 hello 하루 중 특정 시간 동안 toocome 온라인 하나만 될 수 있습니다.

hello 서비스 버스 조정 된 메시징 인프라의 hello 핵심 구성 요소는 큐, 토픽 및 구독 됩니다.  hello 주요 차이점은 항목 논리에 대 한 복잡 한 콘텐츠 기반 라우팅 및 배달, toomultiple 받는 사람에 게 보내기를 비롯 하 여 사용할 수 있는 게시/구독 기능을 지원 합니다. 이러한 구성 요소는 임시 분리, 게시/구독 및 부하 분산과 같은 새로운 비동기 메시징 시나리오를 가능하게 합니다. 이러한 메시징 엔터티에 대한 자세한 내용은 [Service Bus 큐, 토픽 및 구독](service-bus-queues-topics-subscriptions.md)을 참조하세요.

Hello WCF 릴레이 인프라와 hello 조정 된 메시징 기능 WCF 및.NET Framework 프로그래머를 위한 및 REST를 통해 제공 됩니다.

## <a name="next-steps"></a>다음 단계
서비스 버스 메시징에 대 한 더 toolearn hello 다음 항목을 참조 하십시오.

* [서비스 버스 기본 사항](service-bus-fundamentals-hybrid-solutions.md)
* [Service Bus 큐, 토픽 및 구독](service-bus-queues-topics-subscriptions.md)
* [어떻게 toouse 서비스 버스 큐](service-bus-dotnet-get-started-with-queues.md)
* [어떻게 toouse 서비스 버스 항목 및 구독](service-bus-dotnet-how-to-use-topics-subscriptions.md)


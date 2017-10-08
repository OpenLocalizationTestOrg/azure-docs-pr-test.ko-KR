---
title: "Azure 서비스 버스 기본 정보 aaaOverview | Microsoft Docs"
description: "소개 toousing 서비스 버스 tooconnect Azure 응용 프로그램 tooother 소프트웨어."
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 12654cdd-82ab-4b95-b56f-08a5a8bbc6f9
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/15/2017
ms.author: sethm
ms.openlocfilehash: 1abd5cf310ef06ba35e1e2489a7c0a07e1797736
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-bus"></a>Azure Service Bus

응용 프로그램 또는 서비스 hello 클라우드 또는 온-프레미스를 실행 하는지 여부를 다른 응용 프로그램 또는 서비스와 함께 toointeract 자주 필요 합니다. tooprovide 광범위 하 게 유용한 방법은 toodo이, Microsoft Azure 서비스 버스에서 제공 합니다. 이 문서에서는이 기술, 정의 및 toouse는 이유를 설명 하는 것입니다.

## <a name="service-bus-fundamentals"></a>서비스 버스 기본 사항

각 상황에 따라 다른 스타일의 통신이 요청됩니다. 경우에 따라 응용 프로그램 단순 큐를 통해 메시지를 주고받을 수 있도록이 hello 좋습니다. 다른 상황에서는 일반적인 큐로 충분하지 않고 게시 및 구독 메커니즘을 사용한 큐가 더 효율적입니다. 응용 프로그램 간의 연결만 필요하고 큐가 필요하지 않은 경우도 있습니다. 서비스 버스 여러 가지 방법으로 응용 프로그램 toointeract를 사용 하면 모든 세 가지 옵션을 제공 합니다.

서비스 버스는 hello 서비스에 여러 사용자가 공유 되는 것을 의미 하는 다중 테 넌 트 클라우드 서비스입니다. 응용 프로그램 개발자와 같은 각 사용자 생성 한 *네임 스페이스*, 한 다음 해당 네임 스페이스 내에서 필요한 hello 통신 메커니즘을 정의 합니다. 그림 1에서는 이 아키텍처는 모양을 보여줍니다.

![][1]

**그림 1: 서비스 버스 hello 클라우드를 통해 응용 프로그램을 연결 하기 위한 다중 테 넌 트 서비스를 제공 합니다.**

네임스페이스 내에서 각각 다른 방식으로 응용 프로그램을 연결하는 세 가지 통신 메커니즘 인스턴스를 하나 이상 사용할 수 있습니다. hello 선택할 수 있습니다.

* *큐*- 단방향 통신을 허용합니다. 각 큐는 수신될 때까지 전송된 메시지를 저장하는 중간자( *브로커*라고도 함) 역할을 합니다. 단일 수신자가 각 메시지를 수신합니다.
* *토픽* - *구독*을 사용하여 단방향 통신 기능을 제공합니다. 토픽 하나에 구독이 여러 개 포함될 수 있습니다. 큐와 같은 항목 브로커 역할을, 하지만 각 구독은 특정 조건과 일치 하는 필터 tooreceive만 메시지를 선택적으로 사용할 수 있습니다.
* *릴레이*- 양방향 통신을 제공합니다. 큐 및 토픽과 달리 릴레이는 처리 중인 메시지를 저장하지 않으며, 브로커 역할을 하지 않고 대신, 전달에 toohello 대상 응용 프로그램에 있습니다.

큐, 토픽 또는 릴레이를 만들 때 이름을 지정합니다. 이 이름은 네임 스페이스를 호출한 경우 모든 함께 hello 개체에 대 한 고유 식별자를 만듭니다. 응용 프로그램 이름 tooService 버스,이 제공 합니다. 다음 해당 큐, 항목 또는 릴레이 toocommunicate를 사용 하 여 서로 수 있습니다. 

toouse hello 릴레이 시나리오에서 이러한 개체를 Windows 응용 프로그램 Windows Communication Foundation (WCF)를 사용할 수 있습니다. 이 서비스는 [WCF 릴레이](../service-bus-relay/relay-what-is-it.md)라고 합니다. 큐와 토픽의 경우 Windows 응용 프로그램이 서비스 버스로 정의된 메시지 API를 사용할 수 있습니다. toomake 비 Windows 응용 프로그램에서 쉽게 toouse 개체를 이러한, Microsoft는 Java, Node.js, 및 다른 언어에 대 한 Sdk를 제공 합니다. HTTP를 통해 [REST API](/rest/api/servicebus/)를 사용하여 큐 및 토픽에 액세스할 수도 있습니다. 

Hello 클라우드에서 실행 되는 자체 않더라도 서비스 버스 toounderstand 반드시 (즉, Microsoft의 Azure 데이터 센터에서), 응용 프로그램을 사용 하는 원격 실행할 수 있습니다. 예를 들어 Azure 또는 자체 데이터 센터 내에서 실행 되는 응용 프로그램에서 실행 중인 서비스 버스 tooconnect 응용 프로그램을 사용할 수 있습니다. 사용할 수 있습니다도 tooconnect 또는 Azure에서 실행 중인 응용 프로그램는 온-프레미스 응용 프로그램 또는 태블릿 및 휴대폰과 클라우드 플랫폼입니다. 가능한 tooconnect 가구 어플라이언스, 센서, 및 기타 장치 tooa 중앙 응용 프로그램 또는 다른 tooone 않습니다. 서비스 버스는 거의 모든 위치에서 액세스할 수 있는 hello 클라우드에서 통신 메커니즘입니다. 방법 사용 하면 응용 프로그램 어떤 toodo 필요에 따라 다릅니다.

## <a name="queues"></a>큐

서비스 버스 큐를 사용 하 여 tooconnect 두 응용 프로그램을 결정 했다고 가정 합니다. 그림 2에서는 이 상황을 보여 줍니다.

![][2]

**그림 2: 서비스 버스 큐는 단방향 비동기 큐를 제공합니다.**

hello 과정은 간단: 보내는 메시지 tooa 서비스 버스 큐 및 수신자가이 나중에 해당 메시지를 선택 합니다. 센서가 메시지를 서비스 버스 큐로 보내면 수신기가 나중에 해당 메시지를 확인합니다. Hello에서 여러 응용 프로그램을 읽을 수 또는 동일한 큐입니다. Hello 후자의 경우, 각 메시지는 하나의 수신기에서 읽습니다. 멀티캐스트 서비스의 경우 대신 주제를 사용해야 합니다.

각 메시지는 각각 키/값 쌍인 속성 집합과 메시지 페이로드의 두 부분으로 이루어져 있습니다. hello 페이로드는 이진, 텍스트 또는 XML에도 될 수 있습니다. 사용 하는 방법 toodo를 시도 하는 응용 프로그램에 따라 달라 집니다. 최근 판매에 대 한 메시지를 보내는 응용 프로그램 수 hello 속성을 포함 하는 예를 들어 **판매자 "Ava" =** 및 **크기 = 10000**합니다. hello 메시지 본문 hello 판매 서명 된 계약의 스캔 한 이미지가 포함 될 수도 있습니다, 없는 경우를 빈 상태로 유지.

수신기는 두 가지 방법으로 서비스 버스 큐에서 메시지를 읽을 수 있습니다. 라는 첫 번째 옵션을 hello  *[ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode)*hello 큐에서 메시지를 제거 하 고 즉시 삭제 합니다. 이 옵션은 간단 하지만 hello 메시지 처리를 완료 하기 전에 hello 수신기가 충돌 하는 경우 hello 메시지가 손실 됩니다. Hello 큐에서 제거 되었으므로를 다른 수신기 없음 액세스할 수 있습니다. 

두 번째 옵션 hello  *[PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode)*, toohelp이 문제가 발생할 것입니다. 마찬가지로 **ReceiveAndDelete**, **PeekLock** 읽기 hello 큐에서 메시지를 제거 합니다. 그러나 hello 메시지를 삭제 되지 않습니다. 대신, 보이지 않는 tooother 수신기를 만드는 hello 메시지를 잠급니다 다음 세 가지 이벤트 중 하나가 될 때까지 대기 합니다.

* 수신기 프로세스 hello 메시지를 성공적으로 hello, 호출 [complete ()](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete), hello 큐 hello 메시지를 삭제 합니다. 
* Hello 수신기가 hello 메시지를 성공적으로 처리할 수 없다고를 결정 하는 경우 호출 [Abandon()](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon)합니다. 그런 다음 hello 큐 hello 잠금은 hello 메시지에서 제거 하 고 사용할 수 있는 tooother 수신기를 만듭니다.
* Hello 수신기에서는 이러한 메서드의 둘 다에서 구성 가능한 일정 기간 (기본적으로 60 초), hello 큐 hello 수신기 못한 가정 합니다. 이 경우 것 처럼 동작 hello 수신기 호출한 **중단**, hello 메시지 사용할 수 있는 tooother 수신기 만들기.

여기에 발생할 수 있는 결과 표시: hello 동일한 메시지 배달 될 수 있다는 두 번 tootwo 아마도 다른 수신기입니다. Service Bus 큐를 사용하는 응용 프로그램은 이 이벤트에 대비해야 합니다. toomake 쉽게 중복 감지, 각 메시지에는 고유한 [MessageID](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId) 큐에서 읽은 hello 메시지 횟수에 관계 없이 동일한 기본적으로 hello 상태를 유지 하는 속성입니다. 

큐는 다양한 상황에서 유용합니다. 응용 프로그램 toocommunicate 있도록 hello에서 모두 실행 하지 않는 경우에 동일한 시간, 일괄 처리 및 모바일 응용 프로그램에서 매우 편리에 있다는 것입니다. 여러 수신기가 있는 큐는 전송된 메시지가 이러한 수신기에 분산되므로 자동 부하 분산 기능도 제공합니다.

## <a name="topics"></a>토픽

유용한 멤버인, 큐 없는 경우도 hello 적합 한 솔루션입니다. 때로는 서비스 버스 토픽이 더 효율적입니다. 그림 3에서는 이 아이디어를 보여 줍니다.

![][3]

**그림 3: 등록 응용 프로그램을 지정 하는 hello 필터에 따라, 일부를 받을 수 또는 모든 hello 메시지가 전송 tooa 서비스 버스 항목입니다.**

A *항목* 여러 방법으로 tooa 큐에 있는 것과 비슷합니다. 보낸 사람 tooa 부분 hello에 메시지를 전송 tooa 큐 메시지를 전송할 때와 동일한 큐와 마찬가지로 이러한 메시지 모양을 hello 같은 방식으로 합니다. hello 차이점은 각 수신 응용 프로그램 toocreate을 사용 하는 항목 자체 *구독* 정의 하 여 한 *필터*합니다. 구독자는 다음 해당 필터와 일치 하는 hello 메시지만 표시 합니다. 예를 들어 그림 3에서는 각각 고유한 필터가 있는 세 명의 구독자가 포함된 토픽과 보낸 사람을 보여 줍니다.

* 구독자 1 hello 속성을 포함 하는 메시지만 받습니다 *판매자 "Ava" =*합니다.
* Hello 속성을 포함 하는 메시지를 수신 하는 구독자 2 *판매자 "Ruby" =* 포함 및/또는 *양* 100, 000 보다 큰 값으로 속성입니다. 아마도 Ruby 되므로 hello 영업 관리자가 자신의 판매와는 누가 관계 없이 모든 큰 판매 toosee 만들려고 합니다.
* 3 구독자가 해당 필터를 너무 설정*True*, 모든 메시지를 수신 했음을 의미 합니다. 예를 들어이 응용 프로그램 감사 내역을 유지 관리 해야 할 수 있습니다 및 따라서 필요한 toosee 모든 hello 메시지입니다.

큐와 구독자 tooa 항목 중 하나를 사용 하 여 메시지를 읽이 있는 [ReceiveAndDelete 또는 PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode)합니다. 그러나 큐와 달리 단일 메시지 전송 tooa 항목 여러 구독에서 받을 수 있습니다. 일반적으로 이라는이 방법을 사용 *게시 및 구독* (또는 *pub/sub*), 여러 응용 프로그램이 hello에 관심이 때마다 유용 같은 메시지입니다. Hello 오른쪽 필터를 정의 하 여 각 구독자 필요 하다 고 toosee hello 메시지 스트림의 hello 부분만 활용할 수 있습니다.

## <a name="relays"></a>릴레이

큐와 토픽은 둘 다 브로커를 통해 단방향 비동기 통신을 제공합니다. 트래픽이 한 방향으로만 진행되며, 보낸 사람과 받는 사람 간에 직접 연결이 없습니다. 그러나 이런 연결을 원하지 않는 경우 어떻게 해야 할까요? 응용 프로그램을 가정 필요 tooboth 보내고 메시지를 받을 또는 아마도 서로 직접 링크를 원하는 및 broker toostore 메시지 필요 하지 않습니다. 이와 같은 tooaddress 시나리오에서 서비스 버스를 제공 *릴레이*그림 4, 합니다.

![][4]

**그림 4: 서비스 버스 릴레이는 응용 프로그램 간에 양방향 동기 통신을 제공합니다.**

hello 릴레이 대 한 명확한 질문 tooask 이것이: 왜 사용 하나? 큐 필요 없음, 경우에 직접 상호 작용 뿐 아니라 클라우드 서비스를 통해 통신 하는 응용 프로그램을 만드는 이유? hello 대답이 통하게 직접 수 있도록 생각 보다 어렵습니다.

Tooconnect 두 온-프레미스 응용 프로그램을 가정해 기업 데이터 센터 내에서 둘 다 실행 합니다. 각 응용 프로그램은 방화벽 뒤에 있고, 각 데이터 센터에서 NAT(Network Address Translation)를 사용합니다. 각 응용 프로그램에서 실행 되는 hello 컴퓨터를 의미 하는 몇 가지 포트 및 NAT 제외한 모든 들어오는 데이터 hello 방화벽 블록 외부 hello 데이터 센터에서 직접 도달할 수 있는 고정된 IP 주소를 없는 합니다. 몇 가지 추가 도움 없이 hello를 통해 이러한 응용 프로그램 연결 공용 인터넷 문제가 될 수 있습니다.

Azure 서비스 버스 릴레이는 도움이 됩니다. 각 응용 프로그램에 대 한 릴레이 통해 양방향으로 toocommunicate 서비스 버스에 대 한 아웃 바운드 TCP 연결을 설정 후 열어 둡니다. Hello 두 응용 프로그램 간의 모든 통신이 이러한 연결을 통해 이동 합니다. 각 연결 때문에에서 hello 데이터 센터 내 hello 방화벽 허용 들어오는 트래픽을 tooeach 응용 프로그램이 새 포트를 열지 않고 합니다. 이 방법은 hello 클라우드의 hello 통신 전체에서 각 응용 프로그램에는 일관성 있는 끝점이 hello NAT 문제를 가져옵니다. Hello 릴레이 통해 데이터를 교환 하 여 hello 응용 프로그램은 그렇지 않은 경우 통신 어렵게 만드는 hello 문제를 방지할 수 있습니다. 

서비스 버스 릴레이 toouse, 응용 프로그램이 Windows Communication Foundation (WCF) hello를 사용 합니다. 서비스 버스 릴레이 통해 Windows 응용 프로그램 toointeract에 대 한 간단 하 게 확인 하는 WCF 바인딩을 제공 합니다. 이미 WCF를 사용 하는 응용 프로그램 일반적으로 이러한 바인딩 중 하나를 지정 다음 이야기 tooeach 릴레이 통해 다른 수 있습니다. 그러나 큐 및 토픽과 달리 Windows가 아닌 응용 프로그램에서 릴레이를 사용할 수는 있지만 이 경우 약간의 프로그래밍이 필요하며 표준 라이브러리가 제공되지 않습니다.

큐 및 토픽과 달리 응용 프로그램에서 명시적으로 릴레이를 만들지는 않습니다. 대신 서비스 버스에 TCP 연결을 설정 하는 tooreceive 메시지 하지 않고자 한다면 하는 응용 프로그램, 릴레이 자동으로 만들어집니다. Hello 연결을 삭제 하는 경우에 hello 릴레이 삭제 됩니다. 특정 수신기를 서비스 버스에서 만든 응용 프로그램 toofind hello 릴레이 tooenable 이름으로 응용 프로그램 toolocate 수 있도록 하는 레지스트리 특정 릴레이 제공 합니다.

응용 프로그램 간의 직접 통신 해야 하는 경우 릴레이 hello 오른쪽 솔루션입니다. 온-프레미스 데이터 센터에서 실행되는 항공편 예약 시스템을 체크 인 키오스크, 모바일 장치 및 기타 컴퓨터에서 액세스할 수 있어야 하는 경우를 예로 들어 보겠습니다. 이러한 모든 시스템에서 실행 중인 응용 프로그램 hello 클라우드 toocommunicate에서 서비스 버스 릴레이 의존 수 때마다 실행 될 수도 있습니다.

## <a name="summary"></a>요약

전체 솔루션을 작성의 일부 항상 있었지만 응용 프로그램에 연결 및 응용 프로그램 및 서비스 toocommunicate 서로 해야 하는 시나리오의 hello 범위 tooincrease 설정 되어 더 많은 응용 프로그램 및 장치에 연결 된 toohello로 인터넷 합니다. 클라우드 기반 기술인 큐, 항목 및 릴레이 통해 통신을 얻기 위해을 제공 하 여 서비스 버스 목표로 toomake이 필수 기능은 쉽게 tooimplement 보다 광범위 하 게 사용할 수 있습니다.

## <a name="next-steps"></a>다음 단계

Azure 서비스 버스의 hello 기본 사항 학습 한, 했으므로 이러한 링크 toolearn 자세한 수행 합니다.

* 어떻게 toouse [서비스 버스 큐](service-bus-dotnet-get-started-with-queues.md)
* 어떻게 toouse [서비스 버스 주제](service-bus-dotnet-how-to-use-topics-subscriptions.md)
* 어떻게 toouse [서비스 버스 릴레이](../service-bus-relay/service-bus-dotnet-how-to-use-relay.md)
* [서비스 버스 샘플](service-bus-samples.md)

[1]: ./media/service-bus-fundamentals-hybrid-solutions/SvcBus_01_architecture.png
[2]: ./media/service-bus-fundamentals-hybrid-solutions/SvcBus_02_queues.png
[3]: ./media/service-bus-fundamentals-hybrid-solutions/SvcBus_03_topicsandsubscriptions.png
[4]: ./media/service-bus-fundamentals-hybrid-solutions/SvcBus_04_relay.png

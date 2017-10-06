---
title: "Azure 서비스 버스 항목 및 구독을 사용 하는 aaaCreate 응용 | Microsoft Docs"
description: "소개 toohello 게시-구독 기능과 서비스 버스 항목 및 구독에서 제공 합니다."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a48fc9b0-b7b0-464e-8187-a517bf8b4eb4
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/07/2017
ms.author: sethm
ms.openlocfilehash: f6d7de46ace7bd5b49de612db213ced789308d91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-applications-that-use-service-bus-topics-and-subscriptions"></a>Service Bus 토픽 및 구독을 사용하는 응용 프로그램 만들기
Azure 서비스 버스는 신뢰할 수 있는 메시지 큐 및 지속형 게시/구독 메시징을 포함하여 클라우드 기반, 메시지 지향 미들웨어 기술 집합을 지원합니다. 이 문서에 제공 된 hello 정보에 빌드 [서비스 버스 큐를 사용 하는 응용 프로그램](service-bus-create-queues.md) 소개에서 서비스 버스 주제 제공 toohello 게시/구독 기능을 제공 합니다.

## <a name="evolving-retail-scenario"></a>유통업 확장 시나리오
이 문서에 사용 된 hello 소매 시나리오를 계속 [서비스 버스 큐를 사용 하는 응용 프로그램](service-bus-create-queues.md)합니다. 개별 판매 POS (Point of) 터미널의 판매 데이터 재고를 보충 toobe 때 해당 데이터 toodetermine를 사용 하는 라우트된 tooan 재고 관리 시스템 수 있어야 한다는 점에 유의 하세요. 각 POS 터미널 toohello 메시지를 전송 하 여 판매 데이터를 보고 **DataCollectionQueue** 있는 그대로 hello 재고 관리 시스템에서 수신 될 때까지 다음과 같이 큐:

![Service Bus 1](./media/service-bus-create-topics-subscriptions/IC657161.gif)

이 시나리오에서는 새 요구 사항이 되었습니다 tooevolve 추가 toohello 시스템: hello 스토어 소유자가 toobe 수 toomonitor hello 저장소를 실시간으로 수행 되는 방법을 합니다.

tooaddress이 요구이 사항을 hello 시스템 전송 해야 합니다"hello 판매 데이터 스트림을 해제 합니다. 이전에 toohello 재고 관리 시스템으로 전송 하는 hello POS 터미널 toobe 보낸 각 메시지 원하는 있지만 toopresent hello 대시보드 보기 toohello 저장소 소유자를 사용할 수 있는 각 메시지의 다른 복사본이 주시기 바랍니다.

여러 당사자가 사용 된 각 메시지 toobe 해야 이러한 상황에서 서비스 버스를 사용할 수 있습니다 *항목*합니다. 항목 게시 된 각 메시지 사용 가능한 tooone 수 또는 더 많은 구독 hello 항목으로 등록 게시/구독 패턴을 제공 합니다. 반면 큐에서는 각각의 메시지를 단일 소비자가 수신합니다.

메시지 tooa 항목 hello에서 같은 방식으로 tooa 큐 전송 됩니다. 그러나 메시지가 수신 되지 않은 hello 항목에서 직접; 구독에서 수신 됩니다. 구독 tooa 항목 toothat 항목 전송 되는 hello 메시지의 복사본을 받는 가상 큐로 생각할 수 있습니다. 구독에서 메시지를 받을 큐에서 수신 된 방식으로 hello 동일 합니다.

Toohello 소매 시나리오를 다시 살펴보자면, hello 큐 주제를 대신 표시 되며 hello 재고 관리 시스템 구성 요소 צ ְ ײ 구독이 추가 됩니다. hello 시스템은 이제 다음과 같이 나타납니다.

![Service Bus 2](./media/service-bus-create-topics-subscriptions/IC657165.gif)

hello 구성 여기 수행 toohello 이전 큐 기반 디자인과 동일 하 게 합니다. 즉, toohello 항목 전송 된 메시지는 라우트된 toohello **인벤토리** 구독을 어떤 hello **재고 관리 시스템** 사용 합니다.

순서 toosupport hello 관리 대시보드에 다음 그림과 같이 hello 항목에 두 번째 구독을 만듭니다.

![Service Bus 3](./media/service-bus-create-topics-subscriptions/IC657166.gif)

이 구성을 사용 하 여 각 메시지 hello POS 터미널에서 사용할 수 있는 tooboth hello 수 **대시보드** 및 **인벤토리** 구독 합니다.

## <a name="show-me-hello-code"></a>Hello 코드 보기
hello 문서 [서비스 버스 큐를 사용 하는 응용 프로그램](service-bus-create-queues.md) 설명 toosign Azure 계정에 대 한 최대 방법과 서비스 네임 스페이스를 만듭니다. hello 가장 쉬운 방법은 tooreference Service Bus 종속성은 tooinstall hello 서비스 버스 [Nuget 패키지](https://www.nuget.org/packages/WindowsAzure.ServiceBus/)합니다. 찾을 수도 있습니다 hello 서비스 버스 라이브러리 hello Azure SDK의 일부분으로 합니다. hello을 다운로드할 수 hello [Azure SDK 다운로드 페이지](https://azure.microsoft.com/downloads/)합니다.

### <a name="create-hello-topic-and-subscriptions"></a>Hello 항목 및 구독 만들기
서비스 버스 메시징 엔터티 (큐 및 게시/구독 항목) hello를 통해 수행 됩니다에 대 한 관리 작업 [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) 클래스입니다. 순서 toocreate에 적절 한 자격 증명이 필요는 **NamespaceManager** 특정 네임 스페이스에 대 한 인스턴스. Service Bus는 [SAS(공유 액세스 서명)](service-bus-sas.md) 기반 보안 모델을 사용합니다. hello [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#microsoft_servicebus_tokenprovider) 클래스 일부 잘 알려진 토큰 공급자를 반환 하는 기본 제공 팩터리 메서드로 보안 토큰 공급자를 나타냅니다. 에서는 한 [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) 메서드 toohold hello SAS 자격 증명입니다. hello [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) hello hello 서비스 버스 네임 스페이스 및 hello 토큰 공급자의 기본 주소를 가진 인스턴스 생성 합니다.

hello [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) toocreate 메서드를 제공 하는 클래스, 열거 및 메시징 엔터티를 삭제 합니다. 표시 된 코드는 여기 표시 방법을 hello hello **NamespaceManager** 인스턴스가 생성 되 고 사용 되는 toocreate hello **DataCollectionTopic** 항목입니다.

```csharp
Uri uri = ServiceBusEnvironment.CreateServiceUri("sb", "test-blog", string.Empty);
string name = "RootManageSharedAccessKey";
string key = "abcdefghijklmopqrstuvwxyz";

TokenProvider tokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider(name, key);
NamespaceManager namespaceManager = new NamespaceManager(uri, tokenProvider);

namespaceManager.CreateTopic("DataCollectionTopic");
```

Hello의 오버 로드는 [CreateTopic](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateTopic_System_String_) hello 항목의 tooset 속성을 사용 하는 메서드입니다. 예를 들어 toohello 항목 보낸 메시지에 대 한 hello 기본 활성 시간 (TTL) 값을 설정할 수 있습니다. 다음으로 hello 추가 **인벤토리** 및 **대시보드** 구독 합니다.

```csharp
namespaceManager.CreateSubscription("DataCollectionTopic", "Inventory");
namespaceManager.CreateSubscription("DataCollectionTopic", "Dashboard");
```

### <a name="send-messages-toohello-topic"></a>Toohello 부분 메시지 보내기
Service Bus 엔터티의 런타임 작업(예: 메시지 송수신)을 위해서는 응용 프로그램이 먼저[MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#microsoft_servicebus_messaging_messagingfactory) 개체를 만들어야 합니다. 비슷한 toohello [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) 클래스 hello **MessagingFactory** hello hello 서비스 네임 스페이스 및 hello 토큰 공급자의 기준 주소에서 인스턴스가 만들어집니다.

```
MessagingFactory factory = MessagingFactory.Create(uri, tokenProvider);
```

서비스 버스 주제에서 받은 메시지가 전송 tooand hello의 인스턴스인 [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) 클래스입니다. 이 클래스의 표준 속성 집합으로 구성 됩니다 (같은 [레이블](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.label?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) 및 [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.timetolive?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), 사용 되는 toohold 응용 프로그램 속성을 사전 및 임의 응용 프로그램 데이터의 본문입니다. 응용 프로그램 직렬화 된 개체에서를 전달 하 여 hello 본문을 설정할 수 있습니다 (hello 다음 예제에서는 전달에 **SalesData** hello POS 터미널에서 hello 판매 데이터를 나타내는 개체), 있으며 hello를 사용 합니다 [ DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer.aspx) tooserialize hello 개체입니다. 또는 [스트림](https://msdn.microsoft.com/library/system.io.stream.aspx) 개체를 제공할 수 있습니다.

```csharp
BrokeredMessage bm = new BrokeredMessage(salesData);
bm.Label = "SalesReport";
bm.Properties["StoreName"] = "Redmond";
bm.Properties["MachineID"] = "POS_1";
```

hello 가장 쉬운 방법은 toosend 메시지 toohello 항목은 toouse [CreateMessageSender](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageSender_System_String_) toocreate는 [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender) hello에서 직접 개체 [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) 인스턴스:

```csharp
MessageSender sender = factory.CreateMessageSender("DataCollectionTopic");
sender.Send(bm);
```

### <a name="receive-messages-from-a-subscription"></a>구독에서 메시지 받기
비슷한 toousing 큐, 사용할 수는 구독에서 tooreceive 메시지는 [MessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagereceiver) hello에서 직접 만들 수 있는 개체 [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) 를 사용 하 여 [ CreateMessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageReceiver_System_String_)합니다. 하나를 사용 하면 서로 다른 두 개의 수신 모드의 hello (**ReceiveAndDelete** 및 **PeekLock**)에 설명 된 대로 [서비스 버스 큐를 사용 하는 응용 프로그램](service-bus-create-queues.md)합니다.

만들 때 사용자에 게 유의 **MessageReceiver** 구독의 경우 hello *entityPath* hello 폼의 매개 변수는 `topicPath/subscriptions/subscriptionName`합니다. 따라서 toocreate는 **MessageReceiver** hello에 대 한 **인벤토리** hello의 구독 **DataCollectionTopic** 항목 *entityPath*너무 설정 되어 있어야`DataCollectionTopic/subscriptions/Inventory`합니다. hello 코드는 다음과 같이 나타납니다.

```csharp
MessageReceiver receiver = factory.CreateMessageReceiver("DataCollectionTopic/subscriptions/Inventory");
BrokeredMessage receivedMessage = receiver.Receive();
try
{
    ProcessMessage(receivedMessage);
    receivedMessage.Complete();
}
catch (Exception e)
{
    receivedMessage.Abandon();
}
```

## <a name="subscription-filters"></a>구독 필터
지금까지이 시나리오에서는 toohello 항목 보낸 모든 메시지에 등록 하는 사용 가능한 tooall 구독 수행 됩니다. hello 키 구 여기는 "사용할 수 있습니다." 서비스 버스 구독 toohello 항목 보낸 모든 메시지에 표시를 하는 동안 해당 메시지 toohello 가상 구독 큐의 하위 집합만을 복사할 수 있습니다. 이 작업은 구독 *필터*를 사용하여 수행합니다. 구독을 만들 때 hello hello 메시지의 hello 속성에 대해 작동 하는 SQL92 스타일 조건자 형식의 필터 식을 제공할 수 있습니다, 둘 다 hello 시스템 속성 (예를 들어 [레이블](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label)) 및 hello 응용 프로그램 속성을 같은 **StoreName** hello 이전 예제에서 합니다.

두 번째 매장 발전 하는 hello 시나리오 tooillustrate이 toobe 추가 tooour 소매 시나리오를입니다. 모든 저장소 모두에서 hello POS 터미널의 판매 데이터 라우팅 toobe 중앙 집중식 toohello 재고 관리 시스템 하지만 hello 대시보드 도구를 사용 하는 저장소 관리자가 해당 저장소의 hello 성능 관심이. 구독 tooachieve이 필터링을 사용할 수 있습니다. Hello POS 터미널은 메시지를 게시할 때 이러한 설정 hello **StoreName** hello 메시지에 응용 프로그램 속성입니다. 예를 들어 두 개의 저장소 제공 **Redmond** 및 **시애틀**, hello POS 터미널 hello Redmond에서에서 스탬프를 사용 하 여 판매 데이터 메시지를 저장 한 **StoreName** 너무 같은 **Redmond**, 시애틀 hello POS 터미널 사용 하 여 저장 하는 반면, 한 **StoreName** 너무 같은**시애틀**합니다. Redmond만 저장 하는 hello hello 매장 관리자가 해당 매장 POS 터미널에서 toosee 데이터입니다. hello 시스템 다음과 같이 나타납니다.

![Service-Bus4](./media/service-bus-create-topics-subscriptions/IC657167.gif)

이 라우팅 tooset를 만들면 hello **대시보드** 다음과 같이 구독 합니다.

```csharp
SqlFilter dashboardFilter = new SqlFilter("StoreName = 'Redmond'");
namespaceManager.CreateSubscription("DataCollectionTopic", "Dashboard", dashboardFilter);
```

이 [구독 필터](/dotnet/api/microsoft.servicebus.messaging.sqlfilter), hello 된 메시지만 **StoreName** 속성이 너무 설정**Redmond** hello에대한가상큐복사한toohello됩니다**대시보드** 구독 합니다. 그러나 필터링 훨씬 더 많은 toosubscription 있습니다. 응용 프로그램 전달 tooa 구독의 가상 큐 메시지의 추가 toohello 기능 toomodify hello 속성에는 구독 당 여러 필터 규칙을 가질 수 있습니다.

## <a name="summary"></a>요약
에 설명 된 hello 이유 toouse 큐의 모든 [서비스 버스 큐를 사용 하는 응용 프로그램](service-bus-create-queues.md) 도 tootopics, 특히 적용:

* 일시적 분리-메시지 생산자와 소비자 조정은 toobe 온라인에 없는 hello 동시 합니다.
* 부하 평준화-hello 항목 소비 응용 프로그램 toobe 최고 부하가 아닌 평균 부하에 대 한 사용자를 프로 비전을 사용 하도록 설정 하 여 부하 매끄럽게 됩니다.
* 부하 분산 – 비슷한 tooa 큐 tooonly 하나는 부하를 분산할 hello 소비자를 전달 하는 각 메시지와 함께 단일 구독에서 수신 대기 하는 여러 경쟁 소비자가 사용할 수 있습니다.
* 느슨한 결합-기존 끝점; 영향을 주지 않고 네트워크 메시징 hello를 개발할 수 있습니다 예를 들어 구독을 추가 또는 변경 새 소비자에 대 한 tooa 항목 tooallow을 필터링 합니다.

## <a name="next-steps"></a>다음 단계

참조 [서비스 버스 큐를 사용 하는 응용 프로그램](service-bus-create-queues.md) toouse hello POS 소매 시나리오에서 큐 대기 하는 방법에 대 한 정보에 대 한 합니다.


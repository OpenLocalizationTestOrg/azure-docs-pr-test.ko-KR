---
title: "Azure 서비스 버스 큐, 토픽 및 구독을 메시징 aaaOverview | Microsoft Docs"
description: "서비스 버스 메시징 엔터티의 개요"
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a306ced4-74e9-47c6-990a-d9c47efa31d5
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: sethm
ms.openlocfilehash: 73135d2658e341c14dbb114ab938faed91578ff1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-queues-topics-and-subscriptions"></a>Service Bus 큐, 토픽 및 구독

Microsoft Azure Service Bus는 신뢰할 수 있는 메시지 큐 및 지속형 게시/구독 메시징을 포함하여 클라우드 기반, 메시지 지향 미들웨어 기술 집합을 지원합니다. 이러한 "브로커" 메시징 기능으로 분리 된 메시징 기능을 지원 게시-구독, 임시 분리 및 hello 서비스 버스 메시징 패브릭을 사용한 부하 분산 시나리오 생각할 수 있습니다. 분리된 통신에는 많은 장점이 있습니다. 예를 들어 필요하면 클라이언트와 서버가 연결되고 비동기 방식으로 작업을 수행할 수 있습니다.

hello 메시징 기능에서 서비스 버스의 hello 핵심을 형성 하는 hello 메시징 엔터티는 큐, 항목 및 구독 및 규칙/작업 됩니다.

## <a name="queues"></a>큐

큐 제공 *첫 번째 In, First Out* (선출 FIFO) 메시지 배달 tooone 또는 자세한 경쟁 소비자입니다. 즉, 메시지는 일반적으로 예상된 toobe hello 수신기는 toohello 큐에 추가 된 각 메시지는 수신 처리 하며 하나의 메시지 소비자만 hello 순서에 의해 수신 및 처리 합니다. 큐를 사용 하 여의 주요 이점은 tooachieve "임시 분리"을 응용 프로그램 구성 요소입니다. 즉, 생산자 (보낸 사람) hello 및 소비자 (받는) 하지 않은 toobe 전송 및 메시지를 받을 hello에 동일한 메시지 hello 큐에 지속적으로 저장 되므로 시간입니다. 또한 hello 생산자가 되지 toowait hello 소비자의 회신에 대 한에 순서 toocontinue tooprocess 있고 메시지를 보낼 합니다.

관련 된이 점으로 "부하 평준화" 생산자와 소비자 조정은 toosend 있고 서로 다른 속도로 메시지를 수신을 합니다. 많은 응용 프로그램에서 시스템 부하 hello 시간에 따라; 그러나 hello 처리에 필요한 각 작업 단위에 시간은 일반적으로 일정 합니다. 여 메시지 생산자와 소비자를 큐에 응용 프로그램 에서만 사용 하는 hello에 toobe 프로 비전 된 toobe 수 toohandle 최고 부하가 아닌 평균 부하를 의미 합니다. 증가 하 고 hello 수신 부하가 변경 됨에 따라 축소 하는 hello 큐의 hello 깊이입니다. 이 관계 toohello 양의 인프라 필요한 tooservice hello 응용 프로그램 부하 money 직접 저장합니다. Hello로 로드 증가, 작업자 프로세스가 더 추가 된 tooread hello 큐에서 일 수 있습니다. Hello 작업자 프로세스 중 하나에만 각 메시지를 처리 합니다. 또한이 끌어오기 기반 부하 분산 하면 hello 작업자 컴퓨터의 최적 사용에 대 한 hello 작업자 컴퓨터 큰지에 tooprocessing 전원와 다른 경우에 자신의 최대 속도로 메시지를 가져올 때 있습니다. 이 패턴을 "경쟁 소비자" 패턴 hello 종종 있습니다.

메시지 생산자와 소비자 조정은 toointermediate 큐를 사용 하 여 hello 구성 요소 간의 기본적인 느슨한 결합을 제공 합니다. 생산자와 소비자가 서로 인식 없기 때문에 hello 생산자에 영향을 주지 않고 소비자를 업그레이드할 수 있습니다.

큐 만들기는 여러 단계의 프로세스입니다. 서비스 버스 메시징 엔터티 (큐 및 토픽)를 통해 hello에 대 한 관리 작업을 수행할 [Microsoft.ServiceBus.NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) hello hello 서비스 버스의 기준 주소를 제공 하 여 생성 된 클래스 네임 스페이스 및 hello 사용자 자격 증명입니다. [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) 메서드 toocreate 제공 열거 및 메시징 엔터티를 삭제 합니다. 만든 후는 [Microsoft.ServiceBus.TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#microsoft_servicebus_tokenprovider) 개체 hello SAS 이름 및 키 및 서비스 네임 스페이스 관리에서 개체를 hello를 사용할 수 있습니다 [Microsoft.ServiceBus.NamespaceManager.CreateQueue](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateQueue_System_String_) 메서드 toocreate hello 큐입니다. 예:

```csharp
// Create management credentials
TokenProvider credentials = TokenProvider.CreateSharedAccessSignatureTokenProvider(sasKeyName,sasKeyValue);
// Create namespace client
NamespaceManager namespaceClient = new NamespaceManager(ServiceBusEnvironment.CreateServiceUri("sb", ServiceNamespace, string.Empty), credentials);
```

인수로 서 서비스 버스 URI hello로 큐 개체와 메시징 팩터리 다음 만들 수 있습니다. 예:

```csharp
QueueDescription myQueue;
myQueue = namespaceClient.CreateQueue("TestQueue");
MessagingFactory factory = MessagingFactory.Create(ServiceBusEnvironment.CreateServiceUri("sb", ServiceNamespace, string.Empty), credentials); 
QueueClient myQueueClient = factory.CreateQueueClient("TestQueue");
```

그런 다음 toohello 큐 메시지를 보낼 수 있습니다. 예를 들어, 라는 조정 된 메시지의 목록이 있는 경우 `MessageList`, hello 코드가 비슷한 toohello 다음 나타납니다.

```csharp
for (int count = 0; count < 6; count++)
{
    var issue = MessageList[count];
    issue.Label = issue.Properties["IssueTitle"].ToString();
    myQueueClient.Send(issue);
}
```

그런 다음 메시지가 hello 큐에서 다음과 같이 합니다.

```csharp
while ((message = myQueueClient.Receive(new TimeSpan(hours: 0, minutes: 0, seconds: 5))) != null)
    {
        Console.WriteLine(string.Format("Message received: {0}, {1}, {2}", message.SequenceNumber, message.Label, message.MessageId));
        message.Complete();

        Console.WriteLine("Processing message (sleeping...)");
        Thread.Sleep(1000);
    }
```

Hello에 [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode) 모드 hello 수신 작업은 1 단계 즉, 서비스 버스 hello 요청을 받으면 hello 메시지 사용 되는 것을 표시 하 고을 toohello 응용 프로그램을 반환 합니다. **ReceiveAndDelete** 모드는 hello 가장 간단한 모델 이며 시나리오는 hello에 응용 프로그램 실패 하는 hello 이벤트의 메시지를 처리 하지 않아도 안전한 수에 가장 적합 합니다. toounderstand hello는 hello 소비자 문제에 요청을 수신 하는 시나리오 및 후 처리 하기 전에 크래시 합니다. 서비스 버스 hello 응용 프로그램 다시 시작 되 고 메시지 사용을 시작 하는 경우 사용 되는 것 hello 메시지를 표시 하기 때문에 누락 됩니다 hello 메시지 했던 이전 toohello 크래시를 사용 합니다.

[PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode) hello 수신 모드에서이 통해 누락 된 메시지를 허용할 수 없는 가능한 toosupport 응용 프로그램 작업은 2 단계. 서비스 버스 hello 요청을 받으면 hello 사용 되는 다음 메시지 toobe 찾습니다, tooprevent 잠급니다 다른 소비자가 수신할 toohello 응용 프로그램 반환 합니다. Hello hello의 두 번째 단계를 완료 후 hello 응용 프로그램 hello 메시지 처리를 완료 (또는 이후 처리를 위해 안정적으로 저장)를 호출 하 여 수신 프로세스 [완료](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) hello 받은 메시지에 합니다. 서비스 버스 hello를 표시 하는 경우 **완료** 호출, hello 메시지를 사용 중으로 표시 합니다.

Hello 응용 프로그램 수 없는 경우 몇 가지 이유로 tooprocess 환영 메시지가, hello 호출할 수 있는 [중단](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon) 메서드 hello 받은 메시지를 (대신 [완료](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete)). 동일한 소비자 hello 사용 하거나, 서비스 버스 toounlock hello 메시지를 통해이 고 수신 다시 사용할 수 있는 toobe 확인 또는 다른 경쟁 소비자가 있습니다. 둘째, 있습니다 tooprocess hello 응용 프로그램 실패 및 연결 된 hello 잠금 시간 초과가 환영 메시지가 만료 되기 전에 hello 잠금 제한 시간 (예를 들어 hello 응용 프로그램이 충돌할 경우), 서비스 버스 hello 메시지의 잠금을 해제 하 고 사용할 수 있는 toobe를 사용 하면 수신 다시 (기본적으로 수행 된 [중단](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon) 기본적으로 작업).

Hello에 hello 메시지 처리 전후에 그러나 hello 전에 hello 응용 프로그램 이벤트 충돌을 참고 **완료** 다시 시작할 때 hello 메시지는 다시 전달한 toohello 응용 프로그램, 요청이 발생 합니다. 이를 *최소 한 번 이상* 처리라고 합니다. 즉, 각 메시지가 최소 한 번 처리됩니다. 그러나 특정 상황 hello에 동일한 메시지 수를 다시 배달 합니다. Hello 시나리오 중복 처리가 허용 되지 않는 경우 hello에 따라 수행할 수 있는 hello 응용 프로그램 toodetect 중복 항목에 추가 논리가 필요 **MessageId** 상태로 남아 있는 hello 메시지의 속성 배달 시도 간에 상수입니다. *정확히 한번* 처리로 알려집니다.

## <a name="topics-and-subscriptions"></a>토픽 및 구독
각 메시지를 처리 하는 단일 소비자 하 되는 대비 tooqueues에서 *항목* 및 *구독* 에 일 대 다 형식의 통신을 제공는 *게시/구독* 패턴입니다. Toovery 많은 수의 받는 사람을 크기 조정에 대 한 유용한, 게시 된 각 메시지 hello 항목으로 등록 하는 사용 가능한 tooeach 구독을 구성 됩니다. Tooa 주제 및 배달된 tooone 또는 구독 단위로에 설정 될 수 있는 필터 규칙에 따라 연결 된 구독 더 메시지가 전송 됩니다. hello 구독 tooreceive 보고자 하는 추가 필터 toorestrict hello 메시지를 사용할 수 있습니다. 메시지 tooa 항목 hello 동일한 방식으로 전송 됩니다 tooa 큐 하지만 메시지는 hello 항목에서 직접 수신 되지 않습니다. 대신 구독에서 수신합니다. 항목 구독의 toohello 항목 전송 되는 hello 메시지의 복사본을 받는 가상 큐와 유사 합니다. 구독에서 동일 하 게 메시지를 받을 toohello 방식으로 큐에서 수신 됩니다.

비교를 통해 hello 큐의 메시지 전송 기능은 직접 tooa 항목 매핑되고 메시지 수신 기능은 해당 매핑됩니다 tooa 구독 합니다. 특히, 즉 구독을 지원 큰지에 tooqueues와이 섹션의 앞에서 설명한 동일한 패턴 hello: 경쟁 소비자, 임시 분리, 부하 평준화 및 부하 분산 합니다.

항목을 만들기 hello 이전 단원의 hello 예제에 나와 있는 것 처럼 유사한 toocreating 큐입니다. Hello 서비스 URI를 만들고 다음 hello를 사용 하 여 [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) 클래스 toocreate hello 네임 스페이스 클라이언트입니다. Hello를 사용 하 여 항목을 만들 수 있습니다 [CreateTopic](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateTopic_System_String_) 메서드. 예:

```csharp
TopicDescription dataCollectionTopic = namespaceClient.CreateTopic("DataCollectionTopic");
```

다음으로 원하는 대로 구독을 추가합니다.

```csharp
SubscriptionDescription myAgentSubscription = namespaceClient.CreateSubscription(myTopic.Path, "Inventory");
SubscriptionDescription myAuditSubscription = namespaceClient.CreateSubscription(myTopic.Path, "Dashboard");
```

그런 다음 토픽 클라이언트를 만들 수 있습니다. 예:

```csharp
MessagingFactory factory = MessagingFactory.Create(serviceUri, tokenProvider);
TopicClient myTopicClient = factory.CreateTopicClient(myTopic.Path)
```

Hello 메시지 보낸 사람을 사용 하 여 있습니다 보내고 받을 수 메시지 tooand hello 항목에서 hello 이전 섹션에 나와 있는 것 처럼 합니다. 예:

```csharp
foreach (BrokeredMessage message in messageList)
{
    myTopicClient.Send(message);
    Console.WriteLine(
    string.Format("Message sent: Id = {0}, Body = {1}", message.MessageId, message.GetBody<string>()));
}
```

비슷한 tooqueues, 메시지를 사용 하 여 구독에서 받는 [SubscriptionClient](/dotnet/api/microsoft.servicebus.messaging.subscriptionclient) 개체가 아니라는 [QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient) 개체입니다. Hello 구독의 이름으로 hello, hello 문서의 hello 이름을 전달 hello 구독 클라이언트를 만들고 (선택 사항) hello 수신 모드 매개 변수로 합니다. 예를 들어 hello로 **인벤토리** 구독:

```csharp
// Create hello subscription client
MessagingFactory factory = MessagingFactory.Create(serviceUri, tokenProvider); 

SubscriptionClient agentSubscriptionClient = factory.CreateSubscriptionClient("IssueTrackingTopic", "Inventory", ReceiveMode.PeekLock);
SubscriptionClient auditSubscriptionClient = factory.CreateSubscriptionClient("IssueTrackingTopic", "Dashboard", ReceiveMode.ReceiveAndDelete); 

while ((message = agentSubscriptionClient.Receive(TimeSpan.FromSeconds(5))) != null)
{
    Console.WriteLine("\nReceiving message from Inventory...");
    Console.WriteLine(string.Format("Message received: Id = {0}, Body = {1}", message.MessageId, message.GetBody<string>()));
    message.Complete();
}          

// Create a receiver using ReceiveAndDelete mode
while ((message = auditSubscriptionClient.Receive(TimeSpan.FromSeconds(5))) != null)
{
    Console.WriteLine("\nReceiving message from Dashboard...");
    Console.WriteLine(string.Format("Message received: Id = {0}, Body = {1}", message.MessageId, message.GetBody<string>()));
}
```

### <a name="rules-and-actions"></a>규칙 및 동작
대부분의 시나리오에서 특정 특성을 가진 메시지를 다른 방법으로 처리해야 합니다. tooenable이를 원하는 속성을 가진 및 다음 특정 수정 toothose 속성을 수행 하는 구독 toofind 메시지를 구성할 수 있습니다. 서비스 버스 구독 toohello 항목 보낸 모든 메시지에 표시를 하는 동안에 해당 메시지 toohello 가상 구독 큐의 하위 집합을 복사할 수 있습니다. 구독 필터를 사용하여 수행합니다. 이와 같은 수정을 *필터 동작*이라고 합니다. 구독을 만든 경우 hello 메시지의 hello 속성에 작동 하는 필터 식을 제공할 수 있습니다, 둘 다 hello 시스템 속성 (예를 들어 **레이블**) 및 사용자 지정 응용 프로그램 속성 (예를 들어 **StoreName**.) hello SQL 필터 식을이 예제의; 선택 사항 SQL 필터 식을 없이 구독에 정의 된 모든 필터 동작이 해당 구독에 대 한 모든 hello 메시지에 수행 됩니다.

Toofilter 메시지에서 들어오는 hello 앞의 예제를 사용 하 여 **Store1**를 다음과 같이 hello Dashboard 구독을 만듭니다.

```csharp
namespaceManager.CreateSubscription("IssueTrackingTopic", "Dashboard", new SqlFilter("StoreName = 'Store1'"));
```

메시지 hello를 현재 위치에서이 구독 필터 `StoreName` 속성이 너무 설정`Store1` hello에 대 한 복사 toohello 가상 큐는 `Dashboard` 구독 합니다.

가능한 필터 값에 대 한 자세한 내용은 hello에 대 한 hello 설명서를 참조 하십시오. [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) 및 [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) 클래스입니다. 참고: hello [조정 된 메시징: 고급 필터](http://code.msdn.microsoft.com/Brokered-Messaging-6b0d2749) 및 [항목 필터](https://github.com/Azure-Samples/azure-servicebus-messaging-samples/tree/master/TopicFilters) 샘플입니다.

## <a name="next-steps"></a>다음 단계
Hello 다음을 고급 자세한 내용 및 서비스 버스 메시징 사용 하는 예제에 대 한 항목을 참조 하십시오.

* [서비스 버스 메시징 개요](service-bus-messaging-overview.md)
* [Service Bus 조정된 메시징 .NET 자습서](service-bus-brokered-tutorial-dotnet.md)
* [Service Bus 조정된 메시징 REST 자습서](service-bus-brokered-tutorial-rest.md)
* [토픽 필터 샘플](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/TopicFilters)
* [조정된 메시징: 고급 필터 샘플](http://code.msdn.microsoft.com/Brokered-Messaging-6b0d2749)


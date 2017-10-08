---
title: "Azure 서비스 버스 큐를 사용 하는 aaaWrite 응용 프로그램 | Microsoft Docs"
description: "어떻게 toowrite 간단한 큐 기반 응용 프로그램이 Azure 서비스 버스를 사용 합니다."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 754d91b3-1426-405e-84b4-fd36d65b114a
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: 93b75902a06becd6e33e05298e09f5669d0e2aef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-applications-that-use-service-bus-queues"></a>서비스 버스 큐를 사용하는 응용 프로그램 만들기
이 항목 서비스 버스 큐에 설명 하 고 표시 방법을 toowrite 간단한 큐 기반 응용 프로그램 서비스 버스를 사용 하 합니다.

소매 판매 데이터에서 개별 판매 POS 터미널 해야 라우팅할 tooan 재고를 보충 toobe 때에 데이터 toodetermine hello를 사용 하는 재고 관리 시스템은 hello world에서 시나리오를 살펴보겠습니다. 이 솔루션에서는 hello 다음 그림에에서 설명 된 대로 hello 터미널과 hello 재고 관리 시스템 간 hello 통신에 대 한 서비스 버스 메시징 사용:

![Service Bus 큐 이미지 1](./media/service-bus-create-queues/IC657161.gif)

각 POS 터미널 toohello 메시지를 전송 하 여 판매 데이터를 보고 **DataCollectionQueue**합니다. 이러한 메시지는 hello 재고 관리 시스템에서 검색 될 때까지이 큐에 남아 있습니다. 이 패턴을 종종 *비동기 메시징*hello POS 터미널 hello 재고 관리 시스템 toocontinue 처리의 회신에 대 한 toowait 없기 때문에, 합니다.

## <a name="why-queuing"></a>큐 작업 이유
이 응용 프로그램을 필요한 tooset hello 코드를 살펴보기 전에 직접 (동기적) toohello 재고 관리 시스템 대신 hello POS 터미널이이 시나리오에서 큐를 사용할 때의 장점 hello와 통신 하는 것이 좋습니다.

### <a name="temporal-decoupling"></a>임시 분리
Hello 비동기 메시징 패턴을 사용한 생산자와 소비자 조정은 toobe 온라인에 없는 hello 동시 합니다. 사용 중인 파티가 hello tooreceive 준비 될 때까지 메시징 인프라 hello 메시지를 안정적으로 저장을 합니다. 즉, hello 분산 응용 프로그램의 hello 구성 연결이 끊어질 수 있습니다, 하거나 자발적으로; 예를 들어, 유지 관리를 위해 또는 hello 전체 시스템 영향을 주지 않고 tooa 구성 요소 크래시 등 때문입니다. 또한 응용 프로그램을 사용 하는 hello hello 하루 중 특정 시간 동안 toobe 온라인을 가질 수 있습니다. 예를 들어이 소매 시나리오 hello 재고 관리 시스템을 가질 수 toocome 온라인 hello hello 업무 종료 후.

### <a name="load-leveling"></a>부하 평준화 
많은 응용 프로그램에서 시스템 부하 hello 처리에 필요한 각 작업 단위에 시간은 일반적으로 일정 반면 시간에 따라 다릅니다. 조정은 메시지 생산자와 소비자 큐 사용 하 여 hello 소비 응용 프로그램 (hello 작업자)에에 toobe tooservice 최대 부하 대신 평균 부하를 프로 비전 합니다. hello 깊이 hello 큐의 크기가 계속 커집니다 및 계약 수신 부하가 hello 달라 집니다. 이 관계 toohello 양의 인프라 필요한 tooservice hello 응용 프로그램 부하 money 직접 저장합니다.

![Service Bus 큐 이미지 2](./media/service-bus-create-queues/IC657162.gif)

### <a name="load-balancing"></a>부하 분산
Hello로 로드 증가, 작업자 프로세스가 더 추가 된 tooread hello 작업자 큐에서 일 수 있습니다. Hello 작업자 프로세스 중 하나에만 각 메시지를 처리 합니다. 또한이 끌어오기 기반 부하 분산 하면 hello 작업자 컴퓨터의 최적 사용률 hello 작업자 컴퓨터 큰지에 tooprocessing 전원와 다른 경우에 자신의 최대 속도로 메시지를 가져올 때 있습니다. 이 패턴을 hello 경쟁 소비자 패턴을 종종 있습니다.

![Service Bus 큐 이미지 3](./media/service-bus-create-queues/IC657163.gif)

### <a name="loose-coupling"></a>느슨한 결합
메시지 큐 toointermediate 메시지 생산자와 소비자 사이 사용 하 여 hello 구성 요소 간의 내장 함수는 느슨한 결합을 제공 합니다. 생산자와 소비자가 서로 인식 없기 때문에 hello 생산자에 영향을 주지 않고 소비자를 업그레이드할 수 있습니다. 또한 메시징 토폴로지 hello hello 기존 끝점에 영향을 주지 않고 개발할 수 있습니다. 게시/구독에 대해 설명할 때 더 자세히 논의할 것입니다.

## <a name="show-me-hello-code"></a>Hello 코드 보기
섹션에서는 방법을 다음 hello toouse 서비스 버스 toobuild이 응용이 프로그램입니다.

### <a name="sign-up-for-an-azure-account"></a>Azure 계정 등록
서비스 버스 작업 순서 toostart에 Azure 계정이 필요 합니다. 아직 등록하지 않은 경우 [여기](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A85619ABF)에서 무료 계정을 등록할 수 있습니다.

### <a name="create-a-namespace"></a>네임스페이스 만들기
구독이 있으면 [네임스페이스를 만들](service-bus-create-namespace-portal.md) 수 있습니다. 각각의 네임스페이스는 서비스 버스 엔터티 집합에 대한 범위 컨테이너입니다. 모든 서비스 버스 계정에서 새 네임스페이스에 고유한 이름을 지정합니다. 

### <a name="install-hello-nuget-package"></a>Hello NuGet 패키지 설치
toouse hello 서비스 버스 네임 스페이스는 응용 프로그램 hello 서비스 버스 어셈블리, 특히 Microsoft.ServiceBus.dll 참조 해야 합니다. Hello Microsoft Azure SDK의 일부분으로이 어셈블리를 찾을 수 있습니다 및을 hello 다운로드할 hello 수 [Azure SDK 다운로드 페이지](https://azure.microsoft.com/downloads/)합니다. 그러나 hello [Service Bus NuGet 패키지](https://www.nuget.org/packages/WindowsAzure.ServiceBus) hello 가장 쉬운 방법은 tooget hello 서비스 버스 API 및 tooconfigure hello 서비스 버스 종속성의 모든 응용 프로그램은 합니다.

### <a name="create-hello-queue"></a>Hello 큐 만들기
서비스 버스 메시징 엔터티 (큐 및 게시/구독 항목) hello를 통해 수행 됩니다에 대 한 관리 작업 [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) 클래스입니다. Service Bus는 [SAS(공유 액세스 서명)](service-bus-sas.md) 기반 보안 모델을 사용합니다. hello [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) 클래스 일부 잘 알려진 토큰 공급자를 반환 하는 기본 제공 팩터리 메서드로 보안 토큰 공급자를 나타냅니다. 에서는 한 [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) 메서드 toohold hello SAS 자격 증명입니다. hello [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) hello hello 서비스 버스 네임 스페이스 및 hello 토큰 공급자의 기본 주소를 가진 인스턴스 생성 합니다.

hello [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) toocreate 메서드를 제공 하는 클래스, 열거 및 메시징 엔터티를 삭제 합니다. 표시 된 코드는 여기 표시 방법을 hello hello [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) 인스턴스가 생성 되 고 사용 되는 toocreate hello **DataCollectionQueue** 큐입니다.

```csharp
Uri uri = ServiceBusEnvironment.CreateServiceUri("sb", 
                "test-blog", string.Empty);
string name = "RootManageSharedAccessKey";
string key = "abcdefghijklmopqrstuvwxyz";

TokenProvider tokenProvider = 
    TokenProvider.CreateSharedAccessSignatureTokenProvider(name, key);
NamespaceManager namespaceManager = 
    new NamespaceManager(uri, tokenProvider);
namespaceManager.CreateQueue("DataCollectionQueue");
```

Hello의 오버 로드는 [CreateQueue](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateQueue_System_String_) hello 큐 toobe 튜닝의 속성을 사용 하도록 설정 하는 메서드입니다. 예를 들어 toohello 큐에 전송 된 메시지에 대 한 hello 기본 활성 시간 (TTL) 값을 설정할 수 있습니다.

### <a name="send-messages-toohello-queue"></a>송신 메시지 toohello 큐
Service Bus 엔터티의 런타임 작업(예: 메시지 송수신)을 위해서는 응용 프로그램이 먼저[MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) 개체를 만들어야 합니다. 비슷한 toohello [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) 클래스 hello [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) hello hello 서비스 네임 스페이스 및 hello 토큰 공급자의 기준 주소에서 인스턴스가 만들어집니다.

```csharp
 BrokeredMessage bm = new BrokeredMessage(salesData);
 bm.Label = "SalesReport";
 bm.Properties["StoreName"] = "Redmond";
 bm.Properties["MachineID"] = "POS_1";
```

메시지 전송 및 서비스 버스에서 수신 큐는 hello 인스턴스의 [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) 클래스입니다. 이 클래스의 표준 속성 집합으로 구성 됩니다 (같은 [레이블](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) 및 [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), 사용 되는 toohold 응용 프로그램 속성을 사전 및 임의 응용 프로그램 데이터의 본문입니다. 응용 프로그램 직렬화 된 개체에서를 전달 하 여 hello 본문을 설정할 수 있습니다 (hello 다음 예제에서는 전달에 **SalesData** hello POS 터미널에서 hello 판매 데이터를 나타내는 개체), 있으며 hello를 사용 합니다 [ DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer.aspx) tooserialize hello 개체입니다. 또는 [스트림](https://msdn.microsoft.com/library/system.io.stream.aspx) 개체를 제공할 수 있습니다.

가장 쉬운 방법은 toosend 메시지 tooa 우리의 사례 hello에 큐를 지정 된 hello **DataCollectionQueue**, toouse은 [CreateMessageSender](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageSender_System_String_) toocreate는 [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender) 개체 hello에서 직접 [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) 인스턴스.

```csharp
MessageSender sender = factory.CreateMessageSender("DataCollectionQueue");
sender.Send(bm);
```

### <a name="receiving-messages-from-hello-queue"></a>Hello 큐에서 메시지 받기
사용할 수 있습니다 tooreceive hello 큐에서 메시지는 [MessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagereceiver) hello에서 직접 만들 수 있는 개체 [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) 를 사용 하 여 [CreateMessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageReceiver_System_String_)합니다. 메시지 수신기는 **ReceiveAndDelete** 및 **PeekLock**의 두 가지 모드로 작동할 수 있습니다. hello [ReceiveMode](/dotnet/api/microsoft.servicebus.messaging.receivemode) 매개 변수 toohello로 hello 메시지 수신기를 만들 때 설정 됩니다 [CreateMessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagingfactory?redirectedfrom=MSDN#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageReceiver_System_String_Microsoft_ServiceBus_Messaging_ReceiveMode_) 호출 합니다.

Hello를 사용 하는 경우 **ReceiveAndDelete** 모드 hello 수신은 1 단계 작업입니다; 즉, 서비스 버스 hello 요청을 받으면 hello 메시지 사용 되는 것을 표시 하 고 toohello 응용 프로그램을 반환 합니다. **ReceiveAndDelete** 모드는 hello 가장 간단한 모델 이며는 hello에 응용 프로그램이 toooccur 실패할 경우 메시지를 처리 하지 감당할 수 없는 시나리오에 가장 적합 합니다. toounderstand hello는 hello 소비자 문제에 요청을 수신 하는 시나리오 및 후 처리 하기 전에 크래시 합니다. 서비스 버스 hello 메시지 사용 되는 것으로 표시 되어 있으므로 시기 hello 응용 프로그램 다시 시작 되 고 메시지를 사용 하는 시작 누락 됩니다 hello 크래시 전에 사용 된 hello 메시지입니다.

**PeekLock** 모드 hello 수신 하므로 누락 된 메시지를 허용할 수 없는 가능한 toosupport 응용 프로그램 2 단계 작업이 됩니다. 서비스 버스 hello 요청을 받은 다음 메시지 toobe hello 사용 다른 소비자가 수신할 tooprevent 잠근 하 고 toohello 응용 프로그램 반환 찾습니다. Hello hello의 두 번째 단계를 완료 후 hello 응용 프로그램 hello 메시지 처리를 완료 (또는 이후 처리를 위해 안정적으로 저장)를 호출 하 여 수신 프로세스 [완료](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) hello 받은 메시지에 합니다. 서비스 버스 hello를 표시 하는 경우 [완료](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) 호출, hello 메시지를 사용 중으로 표시 합니다.

다른 두 결과 가능합니다. 첫째, hello 응용 프로그램 수 없는 경우 몇 가지 이유로 tooprocess 환영 메시지가, 호출할 수 있는 [중단](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon) hello 받은 메시지에 (대신 [완료](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete)). 동일한 소비자 hello 사용 하거나, 서비스 버스 toounlock hello 메시지와 수신 다시 사용할 수 있는 toobe 확인이 또는 다른 완료 소비자입니다. 둘째, hello 잠금과 관련 있는 제한 시간은 및 hello 메시지 및 사용할 수 있는 toobe 확인 hello 잠금 제한 시간 만료 전에 (예를 들어 hello 응용 프로그램이 충돌할 경우), 서비스 버스에서 잠금 해제 한 후 hello 응용 hello 메시지를 처리할 수 없는 경우 수신 다시 (기본적으로 수행 된 [중단](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon) 기본적으로 작업).

경우 hello 응용 프로그램이 크래시 되 hello 메시지를 처리 한 후 하지만 hello 하기 전에 확인 [완료](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) 요청이 전달 된 경우 hello 메시지를 다시 시작할 때 다시 전달한 toohello 응용 프로그램 수입니다. 이 종종 * 적어도 한 번 * 처리 합니다. 즉, 각 메시지가 최소 한 번 처리 되지만 특정 상황 hello에 동일한 메시지를 다시 배달 될 수 있습니다. Hello 시나리오 중복 처리가 허용 되지 않는, 추가 논리는 hello 응용 프로그램 toodetect 중복 항목이 필요 합니다. Hello에 따라 수행할 수 있습니다 [MessageId](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId) hello 메시지의 속성입니다. 이 속성의 값 hello 배달 시도 간에 일정 하 게 유지 합니다. 이를 *정확히 한 번* 처리라고 합니다.

hello 여기에 표시 된 코드를 받아서 처리 hello를 사용 하는 메시지 **PeekLock** 되지 않은 경우 hello 기본 설정인 모드 [ReceiveMode](/dotnet/api/microsoft.servicebus.messaging.receivemode) 값이 명시적으로 제공 합니다.

```csharp
MessageReceiver receiver = factory.CreateMessageReceiver("DataCollectionQueue");
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

### <a name="use-hello-queue-client"></a>Hello 큐 클라이언트 사용
만든이 섹션의 앞부분에 나오는 예제 hello [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender) 및 [MessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagereceiver) hello에서 직접 개체 [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) toosend 및 메시지를 수신 합니다. hello 큐에서 각각. 또 다른 방법은 toouse는 [QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient) 개체를 지 원하는 모두 보내기 및 받기 작업에서 추가 toomore 고급 세션과 같은 기능을 합니다.

```csharp
QueueClient queueClient = factory.CreateQueueClient("DataCollectionQueue");
queueClient.Send(bm);

BrokeredMessage message = queueClient.Receive();

try
{
    ProcessMessage(message);
    message.Complete();
}
catch (Exception e)
{
    message.Abandon();
} 
```

## <a name="next-steps"></a>다음 단계
큐의 hello 기본 사항 학습 한, 했으므로 참조 [서비스 버스 항목 및 구독을 사용 하는 응용 프로그램을 만들](service-bus-create-topics-subscriptions.md) toocontinue 서비스 버스 주제의 hello 게시/구독 기능을 사용 하 여이 설명 하 고 구독입니다.


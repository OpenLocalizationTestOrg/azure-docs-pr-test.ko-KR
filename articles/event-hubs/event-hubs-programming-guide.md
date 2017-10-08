---
title: "Azure 이벤트 허브에 대 한 aaaProgramming 가이드 | Microsoft Docs"
description: "Hello Azure.NET SDK를 사용 하 여 Azure 이벤트 허브에 대 한 코드를 작성 합니다."
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 64cbfd3d-4a0e-4455-a90a-7f3d4f080323
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 08/17/2017
ms.author: sethm
ms.openlocfilehash: 43bebd126c2311af9e3daeb52324132b66cf0884
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-programming-guide"></a>이벤트 허브 프로그래밍 가이드

이 문서에서는 Azure 이벤트 허브 및 hello Azure.NET SDK를 사용 하 여 코드 작성의 몇 가지 일반적인 시나리오를 설명 합니다. 이벤트 허브에 대한 예비 이해가 있다고 가정합니다. 이벤트 허브의 개념적인 개요를 참조 hello [이벤트 허브 개요](event-hubs-what-is-event-hubs.md)합니다.

## <a name="event-publishers"></a>이벤트 게시자

이벤트 tooan 이벤트 허브를 POST 또는 AMQP 1.0 연결을 통해 HTTP를 사용 하 여 보냅니다. 다양 한 어떤 toouse hello 시기 및 해결 하는 hello 특정 시나리오에 따라 달라 집니다. AMQP 1.0 연결은 영구 메시징 채널을 제공하기 때문에 서비스 버스에서 조정된 연결로 계량되며 시나리오에서 자주 높은 메시지 볼륨 및 낮은 대기 시간 요구 사항에 적절합니다.

생성 하 고 hello를 사용 하 여 이벤트 허브 관리 [NamespaceManager][] 클래스입니다. Hello.NET을 사용 하 여 관리 Api, tooEvent 데이터를 게시 하기 위한 기본 hello 생성 허브는 hello [EventHubClient](/dotnet/api/microsoft.servicebus.messaging.eventhubclient) 및 [EventData][] 클래스입니다. [EventHubClient][] hello 이벤트 toohello 이벤트 허브는 전송 하는 AMQP 통신 채널을 제공 합니다. hello [EventData][] 클래스는 이벤트를 나타내며는 사용 되는 toopublish 메시지 tooan 이벤트 허브입니다. 이 클래스는 hello 본문, 일부 메타 데이터 및 hello 이벤트에 대 한 헤더 정보를 포함 합니다. 다른 속성은 toohello 추가 [EventData][] 이벤트 허브를 통과할 때 개체입니다.

## <a name="get-started"></a>시작

이벤트 허브를 지원 하는 hello.NET 클래스 hello Microsoft.ServiceBus.dll 어셈블리에에서 제공 됩니다. 가장 쉬운 방법은 tooreference hello 서비스 버스 API 및 tooconfigure hello hello 서비스 버스 종속성의 모든 응용 프로그램은 toodownload hello [Service Bus NuGet 패키지](https://www.nuget.org/packages/WindowsAzure.ServiceBus)합니다. Hello 또는 사용할 수 있습니다 [패키지 관리자 콘솔](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) Visual Studio에서. toodo 다음 hello에 명령을 hello를 따라서 발급 [패키지 관리자 콘솔](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) 창:

```
Install-Package WindowsAzure.ServiceBus
```

## <a name="create-an-event-hub"></a>이벤트 허브 만들기
Hello를 사용할 수 있습니다 [NamespaceManager][] toocreate 이벤트 허브 클래스입니다. 예:

```csharp
var manager = new Microsoft.ServiceBus.NamespaceManager("mynamespace.servicebus.windows.net");
var description = manager.CreateEventHub("MyEventHub");
```

대부분의 경우에서 것이 좋습니다 hello를 사용 하는 [CreateEventHubIfNotExists][] 메서드 tooavoid hello 서비스를 다시 시작 하는 경우 예외가 생성 됩니다. 예:

```csharp
var description = manager.CreateEventHubIfNotExists("MyEventHub");
```

모든 이벤트 허브 만들기 작업을 포함 하 여 [CreateEventHubIfNotExists][], 필요 **관리** hello는 네임 스페이스에 대 한 권한. 게시자 또는 소비자 응용 프로그램의 toolimit hello 사용 권한을 원하는 경우이 방지할 수 있습니다 제한 된 권한으로 자격 증명을 사용 하는 경우 프로덕션 코드에서 만들기 작업 호출 합니다.

hello [EventHubDescription](/dotnet/api/microsoft.servicebus.messaging.eventhubdescription) 클래스 hello 권한 부여 규칙, hello 메시지 보존 간격, 파티션 Id, 상태 및 경로 포함 하 여 이벤트 허브에 대 한 세부 정보를 포함 합니다. 이벤트 허브에서이 클래스 tooupdate hello 메타 데이터를 사용할 수 있습니다.

## <a name="create-an-event-hubs-client"></a>이벤트 허브 클라이언트 만들기
이벤트 허브와 상호 작용에 대 한 기본 클래스 hello는 [Microsoft.ServiceBus.Messaging.EventHubClient][EventHubClient]합니다. 이 클래스는 발신자와 수신자 기능을 모두 제공합니다. Hello를 사용 하 여이 클래스를 인스턴스화할 수 [만들기](/dotnet/api/microsoft.servicebus.messaging.eventhubclient.create) 메서드를 다음 예제는 hello와 같이 합니다.

```csharp
var client = EventHubClient.Create(description.Path);
```

이 메서드 hello 서비스 버스 연결 정보를 사용 하 여 hello App.config 파일에서 hello `appSettings` 섹션. Hello에 대 한 예제 `appSettings` toostore hello 서비스 버스 연결 정보를 사용 하는 XML hello에 대 한 hello 설명서를 참조 하십시오 [Microsoft.ServiceBus.Messaging.EventHubClient.Create(System.String)](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Create_System_String_) 메서드.

또 다른 옵션은 연결 문자열에서 toocreate hello 클라이언트입니다. 이 옵션은 hello 문자열 hello 작업자에 대 한 hello 구성 속성에 저장할 수 있으므로 Azure 작업자 역할을 사용 하는 경우에 작동 합니다. 예:

```csharp
EventHubClient.CreateFromConnectionString("your_connection_string");
```

연결 문자열 hello hello 앞의 두 방법에 대 한 hello App.config 파일에 표시 된 대로 동일한 형식 hello 됩니다.

```
Endpoint=sb://[namespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[key]
```

마지막으로, 것도 가능 toocreate는 [EventHubClient][] 에서 개체는 [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) hello 다음 예제와 같이 인스턴스.

```csharp
var factory = MessagingFactory.CreateFromConnectionString("your_connection_string");
var client = factory.CreateEventHubClient("MyEventHub");
```

중요 한 toonote는 추가 [EventHubClient][] 메시징 팩터리 인스턴스에서 생성 된 개체는 hello를 다시 사용 하는 기본 TCP 연결이 동일한 합니다. 따라서 이러한 개체는 처리량에 클라이언트쪽 한계를 갖습니다. hello [만들기](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Create_System_String_) 메서드는 단일 메시징 팩터리를 다시 사용 합니다. 단일 발신자에서 매우 높은 처리량이 필요한 경우 각 메시징 팩터리에서 다양한 메시지 팩터리 및 하나의 [EventHubClient][] 개체를 만들 수 있습니다.

## <a name="send-events-tooan-event-hub"></a>Tooan 이벤트 허브 이벤트 보내기
이벤트 tooan 이벤트 허브를 만들어서 보낼는 [EventData][] 인스턴스와 hello를 통해 보내는 [보낼](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Send_Microsoft_ServiceBus_Messaging_EventData_) 메서드. 이 메서드는 단일 [EventData][] 인스턴스 매개 변수 tooan 이벤트 허브 동기식으로 전송 합니다.

## <a name="event-serialization"></a>이벤트 직렬화
hello [EventData][] 클래스에 [생성자 오버 로드 된 4 개의](/dotnet/api/microsoft.servicebus.messaging.eventdata#constructors_) 다양 한 개체 및 직렬 변환기, 바이트 배열 또는 스트림과 등의 매개 변수를 이용 하는 합니다. 가능한 tooinstantiate hello 이기도 [EventData][] 클래스 및 hello 본문 스트림을 나중에 설정 합니다. JSON을 사용 하는 경우 [EventData][]를 사용할 수 있습니다 **Encoding.UTF8.GetBytes()** tooretrieve hello 바이트 배열에 대 한 JSON으로 인코딩된 문자열입니다.

## <a name="partition-key"></a>파티션 키
hello [EventData][] 클래스에는 [PartitionKey][] hello 보낸 사람 toospecify 값을 사용할 수 있는 속성 해시 tooproduce 파티션 할당 합니다. 파티션 키를 사용 하 여 동일한 키 보내집니다 hello로 이벤트를 hello 모든 하면 toohello hello 이벤트 허브 파티션에 동일 합니다. 공통 파티션 키에는 사용자 세션 ID 및 고유한 보낸 사람 ID가 있습니다. hello [PartitionKey][] 속성은 선택 사항이 며 hello를 사용 하는 경우 제공 될 수 있습니다 [Microsoft.ServiceBus.Messaging.EventHubClient.Send(Microsoft.ServiceBus.Messaging.EventData)](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Send_Microsoft_ServiceBus_Messaging_EventData_) 또는 [Microsoft.ServiceBus.Messaging.EventHubClient.SendAsync(Microsoft.ServiceBus.Messaging.EventData)](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_SendAsync_Microsoft_ServiceBus_Messaging_EventData_) 메서드. 에 대 한 값을 제공 하지 않으면 [PartitionKey][], 이벤트는 라운드 로빈 모델을 사용 하 여 분산된 toopartitions 전송 합니다.

### <a name="availability-considerations"></a>가용성 고려 사항

파티션 키를 사용 하는 선택 사항이 고 신중 하 게 고려해 야 할지 여부 toouse 하나입니다. 대부분의 경우에서 이벤트 순서 지정이 중요한 경우 파티션 키를 사용 하는 것이 좋습니다. 파티션 키를 사용할 경우 이러한 파티션은 단일 노드에서 가용성이 필요하며 시간이 지나면 중단이 발생할 수 있습니다(예: 연산 노드를 재부팅하고 패치할 경우). 따라서 파티션 ID를 설정 하 고 해당 파티션에 어떤 이유로 사용할 수 없게 되 면, 해당 파티션의 시도 tooaccess hello 데이터 실패 합니다. 항상 사용 가능한 가장 중요 한 경우 파티션 키;를 지정 하지 않으면 이 경우 이벤트 toopartitions 앞에서 설명한 hello 라운드 로빈 모델을 사용 하 여 전송 됩니다. 이 시나리오에서는 가용성 (파티션 ID 제외) 및 일관성 (이벤트 tooa 파티션 ID 고정) 간에 명시적인 사항을 만들게 됩니다.

이벤트 처리에서 지연을 처리하는 것도 고려해야 할 사항입니다. 경우에 따라 수 더 나은 toodrop 데이터 수 및 tootry 보다을 다시 시도 하 고 추가 다운스트림 처리 지연 발생 시킬 수 있는 처리를 따라 잡으려고 합니다. 예를 들어 주식 시세 이므로 완전 한 최신 데이터에 대 한 있지만 실시간 채팅 또는 구하려는 경우 hello 데이터 신속 하 게 VOIP 시나리오에 더 나은 toowait 완전 하지 않은 경우에 합니다.

이러한 가용성 고려 사항은 지정 된 이러한 시나리오에서 수도 있습니다 hello 오류 처리 전략을 다음 중 하나:

- 중지(문제가 해결될 때까지 Event Hubs에서 읽기 중지)
- 삭제(메시지가 중요하지 않을 경우에는 삭제)
- (다시 시도 hello를 메시지 표시 된 대로 맞는)을 다시 시도 하십시오.
- [배달 못 한 편지](../service-bus-messaging/service-bus-dead-letter-queues.md) (큐 또는 다른 이벤트 허브 toodead 문자로 hello 메시지에 사용 하 여 처리 하지 못했습니다.)

자세한 내용 및 hello 척도로 상대적 가용성 및 일관성에 대 한 토론에 대 한 참조 [가용성 및 이벤트 허브의 일관성](event-hubs-availability-and-consistency.md)합니다. 

## <a name="batch-event-send-operations"></a>배치 이벤트가 작업을 보냅니다
배치에서 이벤트를 보내면 처리량을 크게 향상시킬 수 있습니다. hello [SendBatch](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_SendBatch_System_Collections_Generic_IEnumerable_Microsoft_ServiceBus_Messaging_EventData__) 메서드는 **IEnumerable** 형식의 매개 변수 [EventData][] 보냅니다 hello 원자 단위 연산 toohello 이벤트 허브로 서 전체 일괄 처리 및 합니다.

```csharp
public void SendBatch(IEnumerable<EventData> eventDataList);
```

참고 단일 일괄 처리는 이벤트의 hello 256KB 제한을 넘지 않아야 합니다. Hello 일괄 처리의 각 메시지에서 hello를 사용 하는 또한 같은 게시자 id입니다. 되기 일괄 처리를 hello hello 보낸 사람 tooensure의 hello 책임 hello 최대 이벤트 크기를 초과 하지 않습니다. 그런 경우 클라이언트 **보내기** 오류가 생성됩니다.

## <a name="send-asynchronously-and-send-at-scale"></a>비동기적으로 보내고 규모로 보내기
또한 이벤트 tooan 이벤트 허브를 비동기적으로 보낼 수 있습니다. 비동기적으로 보내는 클라이언트 수 toosend 이벤트가 있는 hello 속도 높일 수 있습니다. 두 hello [보낼](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Send_Microsoft_ServiceBus_Messaging_EventData_) 및 [SendBatch](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_SendBatch_System_Collections_Generic_IEnumerable_Microsoft_ServiceBus_Messaging_EventData__) 메서드를 반환 하는 비동기 버전에서는 사용할 수는 [작업](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) 개체입니다. 이 기술은 처리량을 늘릴 수, 하는 동안 것도 하지 발생할 수 있습니다 hello 클라이언트 toocontinue toosend 이벤트 hello 이벤트 허브 서비스에 의해 제한 되 고 메시지가 손실된 되거나 hello 클라이언트 오류가 발생할 수 있습니다 하는 동안에 하는 경우를 제대로 구현 합니다. Hello를 사용할 수는 또한 [RetryPolicy](/dotnet/api/microsoft.servicebus.messaging.cliententity#Microsoft_ServiceBus_Messaging_ClientEntity_RetryPolicy) hello 클라이언트 toocontrol 클라이언트 다시 시도 옵션에는 속성입니다.

## <a name="create-a-partition-sender"></a>파티션 발신자 만들기
파티션 키가 없는 가장 일반적인 toosend 이벤트 tooan 이벤트 허브는 아니지만 일부 경우 보겠습니다 toosend 이벤트 지정 된 파티션에서 tooa 직접 합니다. 예:

```csharp
var partitionedSender = client.CreatePartitionedSender(description.PartitionIds[0]);
```

[CreatePartitionedSender](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_CreatePartitionedSender_System_String_) 반환는 [EventHubSender](/dotnet/api/microsoft.servicebus.messaging.eventhubsender) toopublish 이벤트 tooa 특정 이벤트 허브 파티션에 사용할 수 있는 개체입니다.

## <a name="event-consumers"></a>이벤트 소비자
Event Hubs에는 이벤트 사용에 대한 두 기본 모델인 직접 수신기 및 [EventProcessorHost][]와 같은 상위 수준의 추상화가 있습니다. 직접 수신자는 소비자 그룹 내의 액세스 toopartitions의 직접 조정 합니다.

### <a name="direct-consumer"></a>직접 소비자
소비자 그룹 내의 파티션에서 가장 직접적인 방법은 tooread hello는 toouse hello [EventHubReceiver](/dotnet/apie/microsoft.servicebus.messaging.eventhubreceiver) 클래스입니다. 이 클래스의 인스턴스가 toocreate, hello의 인스턴스를 사용 해야 [EventHubConsumerGroup](/dotnet/api/microsoft.servicebus.messaging.eventhubconsumergroup) 클래스입니다. 다음 예제는 hello, hello 파티션 ID hello 소비자 그룹에 대 한 hello 수신기를 만들 때 지정 해야 합니다.

```csharp
EventHubConsumerGroup group = client.GetDefaultConsumerGroup();
var receiver = group.CreateReceiver(client.GetRuntimeInformation().PartitionIds[0]);
```

hello [CreateReceiver](/dotnet/api/microsoft.servicebus.messaging.eventhubconsumergroup#methods_summary) 메서드에 만들려는 hello 판독기에 대 한 제어를 용이 하 게 하는 여러 오버 로드가 있습니다. 이러한 메서드는 오프셋을 지정 하는 문자열이 나 타임 스탬프를 포함 하 고 hello 기능 toospecify 스트림, 또는 그 다음 시작이 지정 된 오프셋 hello에서 반환 하는 tooinclude 여부. Hello 수신기를 만든 후에 개체를 반환 하는 hello에 대해 이벤트 수신을 시작할 수 있습니다. hello [수신](/dotnet/api/microsoft.servicebus.messaging.eventhubreceiver#methods_summary) 메서드에 4 개의 오버 로드가 해당 제어 hello 일괄 처리 크기 등의 작업 매개 변수를 수신 하 고 시간 동안 대기 합니다. Hello 소비자의 이러한 메서드 tooincrease hello 처리량의 비동기 버전을 사용할 수 있습니다. 예:

```csharp
bool receive = true;
string myOffset;
while(receive)
{
    var message = receiver.Receive();
    myOffset = message.Offset;
    string body = Encoding.UTF8.GetString(message.GetBytes());
    Console.WriteLine(String.Format("Received message offset: {0} \nbody: {1}", myOffset, body));
}
```

존중 tooa 특정 파티션과 hello 메시지 hello는 전송 된 순서 대로 toohello 이벤트 허브에서에서 수신 됩니다. hello 오프셋은 문자열 토큰 사용 되는 tooidentify은 파티션에서 메시지입니다.

소비자 그룹 내에서 단일 파티션은 언제든지 연결되는 5개의 동시 판독기를 가질 수 없다는 점에 유의해야 합니다. 독자가 연결 하거나 분리 되, hello 서비스 disconnected가 인식 하기 전에 몇 분 동안 해당 세션이 활성 상태로 유지 될 수 있습니다. 이 시간 동안 tooa 파티션 다시 실패할 수 있습니다. 이벤트 허브 용 직접 수신자 작성의 전체 예제는 hello 참조 [이벤트 허브 직접 수신자](https://code.msdn.microsoft.com/Event-Hub-Direct-Receivers-13fa95c6) 샘플.

### <a name="event-processor-host"></a>이벤트 프로세서 호스트
hello [EventProcessorHost][] 클래스에서 이벤트 허브에서 데이터를 처리 합니다. Hello.NET 플랫폼에서 이벤트 독자를 빌드할 때이 구현을 사용 해야 합니다. [EventProcessorHost][] 는 검사점 및 파티션 임대 관리를 제공하는 이벤트 처리기 구현에 대한 스레드 안전, 다중 프로세스, 안전한 런타임 환경을 제공합니다.

toouse hello [EventProcessorHost][] 클래스를 구현할 수 있습니다 [IEventProcessor](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor)합니다. 이 인터페이스는 세 가지 메서드가 포함합니다.

* [OpenAsync](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor#Microsoft_ServiceBus_Messaging_IEventProcessor_OpenAsync_Microsoft_ServiceBus_Messaging_PartitionContext_)
* [CloseAsync](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor#Microsoft_ServiceBus_Messaging_IEventProcessor_CloseAsync_Microsoft_ServiceBus_Messaging_PartitionContext_Microsoft_ServiceBus_Messaging_CloseReason_)
* [ProcessEventsAsync](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor#Microsoft_ServiceBus_Messaging_IEventProcessor_ProcessEventsAsync_Microsoft_ServiceBus_Messaging_PartitionContext_System_Collections_Generic_IEnumerable_Microsoft_ServiceBus_Messaging_EventData__)

toostart 이벤트 처리를 인스턴스화할 [EventProcessorHost][], 이벤트 허브에 대 한 hello 적절 한 매개 변수를 제공 합니다. 그런 다음 호출 [RegisterEventProcessorAsync](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost#Microsoft_ServiceBus_Messaging_EventProcessorHost_RegisterEventProcessorAsync__1) tooregister 프로그램 [IEventProcessor](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor) hello 런타임 구현 합니다. 이 시점에서 hello 호스트 tooacquire "과 대" 알고리즘을 사용 하 여 hello 이벤트 허브의 모든 파티션에 대 한 임 대권을 시도 합니다. 이러한 임대는 지정된 시간 프레임 동안 지속되며 갱신되어야 합니다. 새 노드로 작업자 인스턴스는이 경우 온라인 상태로, 임대를 예약을 배치 하 고 시간이 지남에 따라 hello 부하 이동 노드 간에 각 시도 tooacquire 임대가 더 합니다.

![이벤트 프로세서 호스트](./media/event-hubs-programming-guide/IC759863.png)

시간이 지남에 따라 평형이 설정됩니다. 이 동적 기능을 사용 하면 CPU 기반 자동 크기 조정을 적용 toobe tooconsumers 수직 확장 및 축소 모두에 대 한 합니다. 평균 CPU 사용률은 이벤트 허브에는 메시지 수의 직접적인 개념이 없으므로 hello 최상의 메커니즘 toomeasure 백 엔드 또는 소비자 규모 경우가 많습니다. 게시자에서 시작 하는 소비자에 게 보다 더 많은 이벤트를 처리할 수 toopublish 소비자에 대 한 hello CPU 증가 작업자 인스턴스 수에 사용 되는 toocause 자동으로 조정할 수 있습니다.

hello [EventProcessorHost][] 클래스는 Azure 저장소 기반 검사점 설정 메커니즘도 구현 합니다. 각 소비자는 hello 이전 소비자의 어떤 hello 마지막 검사점을 확인할 수 있도록에 파티션별로 오프셋이 메커니즘 저장소 hello가 했습니다. 파티션이 전환 될 때 임대를 통해 노드 간에 변화 하는 부하를 용이 하 게 하는 hello 동기화 메커니즘입니다.

## <a name="publisher-revocation"></a>게시자 해지
또한 toohello 런타임의 고급 기능 [EventProcessorHost][], 이벤트 허브 이벤트 tooan 이벤트 허브를 보내지 못하도록 순서 tooblock 특정 게시자에서 게시자 해지 수 있도록 합니다. 이러한 기능은 게시자 토큰이 손상 된 또는 소프트웨어 업데이트는 그 결과 toobehave 부적절 하 게 하는 경우에 특히 유용 합니다. 이러한 상황에서는 SAS 토큰의 일부인 hello 게시자의 id 이벤트 게시를 차단할 수 있습니다.

게시자 해지 및 toosend tooEvent 허브를 게시자로 확인 하려면 어떻게 해야 하는 방법에 대 한 자세한 내용은 hello [이벤트 허브 대규모 보안 게시](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-99ce67ab) 샘플.

## <a name="next-steps"></a>다음 단계
다음이 링크를 방문 하는 이벤트 허브 시나리오에 대해 자세히 toolearn:

* [이벤트 허브 API 개요](event-hubs-api-overview.md)
* [Event Hubs의 정의](event-hubs-what-is-event-hubs.md)
* [Event Hubs의 가용성 및 일관성](event-hubs-availability-and-consistency.md)
* [이벤트 프로세서 호스트 API 참조](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost)

[NamespaceManager]: /dotnet/api/microsoft.servicebus.namespacemanager
[EventHubClient]: /dotnet/api/microsoft.servicebus.messaging.eventhubclient
[EventData]: /dotnet/api/microsoft.servicebus.messaging.eventdata
[CreateEventHubIfNotExists]: /dotnet/api/microsoft.servicebus.namespacemanager.createeventhubifnotexists
[PartitionKey]: /dotnet/api/microsoft.servicebus.messaging.eventdata#Microsoft_ServiceBus_Messaging_EventData_PartitionKey
[EventProcessorHost]: /dotnet/api/microsoft.servicebus.messaging.eventprocessorhost

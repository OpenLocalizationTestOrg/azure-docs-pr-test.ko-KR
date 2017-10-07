---
title: "hello Azure 이벤트 허브.NET 표준 Api의 aaaOverview | Microsoft Docs"
description: ".NET Standard API 개요"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a173f8e4-556c-42b8-b856-838189f7e636
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: c97acecb35b69039e06ded7203c75fca41ce98f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-net-standard-api-overview"></a>Event Hubs .NET Standard API 개요
이 문서 hello 키 이벤트 허브 표준.NET 클라이언트 Api의 일부를 요약 합니다. 현재 다음과 같은 두 개의 .NET Standard 클라이언트 라이브러리가 있습니다.
* [Microsoft.Azure.EventHubs](/dotnet/api/microsoft.azure.eventhubs)
  *  이 라이브러리는 모든 기본 런타임 작업을 제공합니다.
* [Microsoft.Azure.EventHubs.Processor](/dotnet/api/microsoft.azure.eventhubs.processor)
  * 이 라이브러리는 처리 된 이벤트는 추적에 대 한 허용 하는 이벤트 허브에서 가장 쉬운 방법은 tooread hello 추가 기능을 추가 합니다.

## <a name="event-hubs-client"></a>Event Hubs 클라이언트
[EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) hello toosend 이벤트를 사용 하는 기본 개체가 만들어져 수신자, 그리고 tooget 런타임 정보입니다. 이 클라이언트는 연결 된 tooa 특정 이벤트 허브 하 고 새 연결 toohello 이벤트 허브 끝점을 만듭니다.

### <a name="create-an-event-hubs-client"></a>이벤트 허브 클라이언트 만들기
[EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) 개체는 연결 문자열에서 만들어집니다. 다음 예제는 hello hello 가장 간단한 방법은 tooinstantiate 새 클라이언트를 보여 줍니다.

```csharp
var eventHubClient = EventHubClient.CreateFromConnectionString("{Event Hubs connection string}");
```

tooprogrammatically hello 연결 문자열을 편집, hello를 사용할 수 있습니다 [EventHubsConnectionStringBuilder](/dotnet/api/microsoft.azure.eventhubs.eventhubsconnectionstringbuilder) 클래스를 매개 변수로 너무 hello 연결 문자열을 전달[EventHubClient.CreateFromConnectionString ](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_CreateFromConnectionString_System_String_).

```csharp
var connectionStringBuilder = new EventHubsConnectionStringBuilder("{Event Hubs connection string}")
{
    EntityPath = EhEntityPath
};

var eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());
```

### <a name="send-events"></a>이벤트 보내기
toosend 이벤트 tooan 이벤트 허브를 사용 하 여 hello [EventData](/dotnet/api/microsoft.azure.eventhubs.eventdata) 클래스입니다. hello 본문 이어야 합니다는 `byte` 배열 또는 `byte` 배열 세그먼트입니다.

```csharp
// Create a new EventData object by encoding a string as a byte array
var data = new EventData(Encoding.UTF8.GetBytes("This is my message..."));
// Set user properties if needed
data.Properties.Add("Type", "Informational");
// Send single message async
await eventHubClient.SendAsync(data);
```

### <a name="receive-events"></a>이벤트 수신
이벤트 허브에서 방식으로 tooreceive 이벤트 권장 hello hello를 사용 하는 [이벤트 프로세서 호스트](#event-processor-host-apis), tooautomatically 기능을 제공 하는 추적, 오프셋 및 파티션 정보입니다. 그러나 hello 코어 이벤트 허브 라이브러리 tooreceive 이벤트의 toouse hello 유연성 사용할 수 있는 특정 상황이 있습니다.

#### <a name="create-a-receiver"></a>수신기 만들기
수신기는 동 점된 toospecific 파티션, 하므로 순서 tooreceive 모든 이벤트에서 이벤트 허브, toocreate 여러 인스턴스가 필요 합니다. 일반적으로 것이 좋습니다 tooget hello 파티션 정보를 프로그래밍 방식으로 hello 파티션 id를 하드 코딩 하는 대신 합니다. toodo 하므로 순서, hello를 사용할 수 있습니다 [GetRuntimeInformationAsync](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_GetRuntimeInformationAsync) 메서드.

```csharp
// Create a list tookeep track of hello receivers
var receivers = new List<PartitionReceiver>();
// Use hello eventHubClient created above tooget hello runtime information
var runTimeInformation = await eventHubClient.GetRuntimeInformationAsync();
// Loop over hello resulting partition ids
foreach (var partitionId in runTimeInformation.PartitionIds)
{
    // Create hello receiver
    var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, PartitionReceiver.EndOfStream);
    // Add hello receiver toohello list
    receivers.Add(receiver);
}
```

이벤트 이벤트 허브에서 제거 되지 않습니다 (및만 만료) 있으므로 toospecify hello 적절 한 시작 지점이 필요 합니다. hello 다음 예제에서는 가능한 조합을 보여줍니다.

```csharp
// partitionId is assumed toocome from GetRuntimeInformationAsync()

// Using hello constant PartitionReceiver.EndOfStream only receives all messages from this point forward.
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, PartitionReceiver.EndOfStream);

// All messages available
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, "-1");

// From one day ago
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, DateTime.Now.AddDays(-1));
```

#### <a name="consume-an-event"></a>이벤트 소비
```csharp
// Receive a maximum of 100 messages in this call tooReceiveAsync
var ehEvents = await receiver.ReceiveAsync(100);
// ReceiveAsync can return null if there are no messages
if (ehEvents != null)
{
    // Since ReceiveAsync can return more than a single event you will need a loop tooprocess
    foreach (var ehEvent in ehEvents)
    {
        // Decode hello byte array segment
        var message = UnicodeEncoding.UTF8.GetString(ehEvent.Body.Array);
        // Load hello custom property that we set in hello send example
        var customType = ehEvent.Properties["Type"];
        // Implement processing logic here
    }
}       
```

## <a name="event-processor-host-apis"></a>이벤트 프로세서 호스트 API
이러한 Api는 사용 가능한 작업자 파티션에 배포 하 여 사용할 수 없게 될 수 있는 복원 력 tooworker 프로세스를 제공 합니다.

```csharp
// Checkpointing is done within hello SimpleEventProcessor and on a per-consumerGroup per-partition basis, workers resume from where they last left off.

// Read these connection strings from a secure location
var ehConnectionString = "{Event Hubs connection string}";
var ehEntityPath = "{event hub path/name}";
var storageConnectionString = "{Storage connection string}";
var storageContainerName = "{Storage account container name}";

var eventProcessorHost = new EventProcessorHost(
    ehEntityPath,
    PartitionReceiver.DefaultConsumerGroupName,
    ehConnectionString,
    storageConnectionString,
    storageContainerName);

// Start/register an EventProcessorHost
await eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>();

// Disposes of hello Event Processor Host
await eventProcessorHost.UnregisterEventProcessorAsync();
```

hello 다음은 샘플의 구현 hello [IEventProcessor](/dotnet/api/microsoft.azure.eventhubs.processor.ieventprocessor)합니다.

```csharp
public class SimpleEventProcessor : IEventProcessor
{
    public Task CloseAsync(PartitionContext context, CloseReason reason)
    {
        Console.WriteLine($"Processor Shutting Down. Partition '{context.PartitionId}', Reason: '{reason}'.");
        return Task.CompletedTask;
    }

    public Task OpenAsync(PartitionContext context)
    {
        Console.WriteLine($"SimpleEventProcessor initialized. Partition: '{context.PartitionId}'");
        return Task.CompletedTask;
    }

    public Task ProcessErrorAsync(PartitionContext context, Exception error)
    {
        Console.WriteLine($"Error on Partition: {context.PartitionId}, Error: {error.Message}");
        return Task.CompletedTask;
    }

    public Task ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
    {
        foreach (var eventData in messages)
        {
            var data = Encoding.UTF8.GetString(eventData.Body.Array, eventData.Body.Offset, eventData.Body.Count);
            Console.WriteLine($"Message received. Partition: '{context.PartitionId}', Data: '{data}'");
        }

        return context.CheckpointAsync();
    }
}
```

## <a name="next-steps"></a>다음 단계
다음이 링크를 방문 하는 이벤트 허브 시나리오에 대해 자세히 toolearn:

* [Azure 이벤트 허브 정의](event-hubs-what-is-event-hubs.md)
* [사용할 수 있는 Event Hubs API](event-hubs-api-overview.md)

hello.NET API 참조는 여기 있습니다.

* [Microsoft.Azure.EventHubs](/dotnet/api/microsoft.azure.eventhubs)
* [Microsoft.Azure.EventHubs.Processor](/dotnet/api/microsoft.azure.eventhubs.processor)
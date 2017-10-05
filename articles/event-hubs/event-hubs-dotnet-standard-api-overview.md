---
title: "Azure Event Hubs .NET Standard API 개요 | Microsoft Docs"
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
ms.openlocfilehash: eea682c40cd415b383a8b2f0004a5f3648e2f01f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="event-hubs-net-standard-api-overview"></a><span data-ttu-id="c933f-103">Event Hubs .NET Standard API 개요</span><span class="sxs-lookup"><span data-stu-id="c933f-103">Event Hubs .NET Standard API overview</span></span>
<span data-ttu-id="c933f-104">이 문서는 핵심 Event Hubs .NET Standard 클라이언트 API 일부를 요약해서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c933f-104">This article summarizes some of the key Event Hubs .NET Standard client APIs.</span></span> <span data-ttu-id="c933f-105">현재 다음과 같은 두 개의 .NET Standard 클라이언트 라이브러리가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c933f-105">There are currently two .NET Standard client libraries:</span></span>
* [<span data-ttu-id="c933f-106">Microsoft.Azure.EventHubs</span><span class="sxs-lookup"><span data-stu-id="c933f-106">Microsoft.Azure.EventHubs</span></span>](/dotnet/api/microsoft.azure.eventhubs)
  *  <span data-ttu-id="c933f-107">이 라이브러리는 모든 기본 런타임 작업을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c933f-107">This library provides all basic runtime operations.</span></span>
* [<span data-ttu-id="c933f-108">Microsoft.Azure.EventHubs.Processor</span><span class="sxs-lookup"><span data-stu-id="c933f-108">Microsoft.Azure.EventHubs.Processor</span></span>](/dotnet/api/microsoft.azure.eventhubs.processor)
  * <span data-ttu-id="c933f-109">이 라이브러리는 처리된 이벤트를 추적하는 추가 기능을 추가하며 이벤트 허브에서 읽는 가장 쉬운 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="c933f-109">This library adds additional functionality that allows for keeping track of processed events, and is the easiest way to read from an event hub.</span></span>

## <a name="event-hubs-client"></a><span data-ttu-id="c933f-110">Event Hubs 클라이언트</span><span class="sxs-lookup"><span data-stu-id="c933f-110">Event Hubs client</span></span>
<span data-ttu-id="c933f-111">[EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient)는 이벤트를 전송하고, 수신기를 만들고, 런타임 정보를 얻는 데 사용하는 기본 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="c933f-111">[EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) is the primary object you use to send events, create receivers, and to get run-time information.</span></span> <span data-ttu-id="c933f-112">이 클라이언트는 특정 이벤트 허브에 연결되며 Event Hubs 끝점에 대한 새 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c933f-112">This client is linked to a particular event hub, and creates a new connection to the Event Hubs endpoint.</span></span>

### <a name="create-an-event-hubs-client"></a><span data-ttu-id="c933f-113">이벤트 허브 클라이언트 만들기</span><span class="sxs-lookup"><span data-stu-id="c933f-113">Create an Event Hubs client</span></span>
<span data-ttu-id="c933f-114">[EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) 개체는 연결 문자열에서 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="c933f-114">An [EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) object is created from a connection string.</span></span> <span data-ttu-id="c933f-115">새 클라이언트를 인스턴스화하는 가장 간단한 방법은 다음 예제에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c933f-115">The simplest way to instantiate a new client is shown in the following example:</span></span>

```csharp
var eventHubClient = EventHubClient.CreateFromConnectionString("{Event Hubs connection string}");
```

<span data-ttu-id="c933f-116">프로그래밍 방식으로 연결 문자열을 편집하려면 [EventHubsConnectionStringBuilder](/dotnet/api/microsoft.azure.eventhubs.eventhubsconnectionstringbuilder) 클래스를 사용하고 연결 문자열을 [EventHubClient.CreateFromConnectionString](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_CreateFromConnectionString_System_String_)에 대한 매개 변수로 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c933f-116">To programmatically edit the connection string, you can use the [EventHubsConnectionStringBuilder](/dotnet/api/microsoft.azure.eventhubs.eventhubsconnectionstringbuilder) class, and pass the connection string as a parameter to [EventHubClient.CreateFromConnectionString](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_CreateFromConnectionString_System_String_).</span></span>

```csharp
var connectionStringBuilder = new EventHubsConnectionStringBuilder("{Event Hubs connection string}")
{
    EntityPath = EhEntityPath
};

var eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());
```

### <a name="send-events"></a><span data-ttu-id="c933f-117">이벤트 보내기</span><span class="sxs-lookup"><span data-stu-id="c933f-117">Send events</span></span>
<span data-ttu-id="c933f-118">이벤트 허브에 이벤트를 전송하려면 [EventData](/dotnet/api/microsoft.azure.eventhubs.eventdata) 클래스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c933f-118">To send events to an event hub, use the [EventData](/dotnet/api/microsoft.azure.eventhubs.eventdata) class.</span></span> <span data-ttu-id="c933f-119">본문은 `byte` 배열 또는 `byte` 배열 세그먼트여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c933f-119">The body must be a `byte` array, or a `byte` array segment.</span></span>

```csharp
// Create a new EventData object by encoding a string as a byte array
var data = new EventData(Encoding.UTF8.GetBytes("This is my message..."));
// Set user properties if needed
data.Properties.Add("Type", "Informational");
// Send single message async
await eventHubClient.SendAsync(data);
```

### <a name="receive-events"></a><span data-ttu-id="c933f-120">이벤트 수신</span><span class="sxs-lookup"><span data-stu-id="c933f-120">Receive events</span></span>
<span data-ttu-id="c933f-121">Event Hubs에서 이벤트를 수신하는 권장 방법은 오프셋을 자동으로 추적하는 기능과 파티션 정보를 제공하는 [Event Processor Host](#event-processor-host-apis)를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c933f-121">The recommended way to receive events from Event Hubs is using the [Event Processor Host](#event-processor-host-apis), which provides functionality to automatically keep track of offset, and partition information.</span></span> <span data-ttu-id="c933f-122">그러나 핵심 Event Hubs 라이브러리의 유연성을 활용하여 이벤트를 수신할 수 있는 상황도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c933f-122">However, there are certain situations in which you may want to use the flexibility of the core Event Hubs library to receive events.</span></span>

#### <a name="create-a-receiver"></a><span data-ttu-id="c933f-123">수신기 만들기</span><span class="sxs-lookup"><span data-stu-id="c933f-123">Create a receiver</span></span>
<span data-ttu-id="c933f-124">수신기는 특정 파티션에 연결되어 있으므로 이벤트 허브에서 모든 이벤트를 수신하려면 여러 인스턴스를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c933f-124">Receivers are tied to specific partitions, so in order to receive all events in an event hub, you will need to create multiple instances.</span></span> <span data-ttu-id="c933f-125">일반적으로 말해서 파티션 ID를 하드 코드하는 것보다는 프로그래밍 방식으로 파티션 정보를 얻는 것이 더 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c933f-125">Generally speaking, it is a good practice to get the partition information programatically, rather than hard-coding the partition ids.</span></span> <span data-ttu-id="c933f-126">이렇게 하기 위해 [GetRuntimeInformationAsync](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_GetRuntimeInformationAsync) 메서드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c933f-126">In order to do so, you can use the [GetRuntimeInformationAsync](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_GetRuntimeInformationAsync) method.</span></span>

```csharp
// Create a list to keep track of the receivers
var receivers = new List<PartitionReceiver>();
// Use the eventHubClient created above to get the runtime information
var runTimeInformation = await eventHubClient.GetRuntimeInformationAsync();
// Loop over the resulting partition ids
foreach (var partitionId in runTimeInformation.PartitionIds)
{
    // Create the receiver
    var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, PartitionReceiver.EndOfStream);
    // Add the receiver to the list
    receivers.Add(receiver);
}
```

<span data-ttu-id="c933f-127">이벤트는 이벤트 허브에서 절대 제거되지 않으므로(만료되기만 함) 적절한 시작 지점을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c933f-127">Since events are never removed from an event hub (and only expire), you need to specify the proper starting point.</span></span> <span data-ttu-id="c933f-128">다음 예제에서는 가능한 조합을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c933f-128">The following example shows possible combinations.</span></span>

```csharp
// partitionId is assumed to come from GetRuntimeInformationAsync()

// Using the constant PartitionReceiver.EndOfStream only receives all messages from this point forward.
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, PartitionReceiver.EndOfStream);

// All messages available
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, "-1");

// From one day ago
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, DateTime.Now.AddDays(-1));
```

#### <a name="consume-an-event"></a><span data-ttu-id="c933f-129">이벤트 소비</span><span class="sxs-lookup"><span data-stu-id="c933f-129">Consume an event</span></span>
```csharp
// Receive a maximum of 100 messages in this call to ReceiveAsync
var ehEvents = await receiver.ReceiveAsync(100);
// ReceiveAsync can return null if there are no messages
if (ehEvents != null)
{
    // Since ReceiveAsync can return more than a single event you will need a loop to process
    foreach (var ehEvent in ehEvents)
    {
        // Decode the byte array segment
        var message = UnicodeEncoding.UTF8.GetString(ehEvent.Body.Array);
        // Load the custom property that we set in the send example
        var customType = ehEvent.Properties["Type"];
        // Implement processing logic here
    }
}       
```

## <a name="event-processor-host-apis"></a><span data-ttu-id="c933f-130">이벤트 프로세서 호스트 API</span><span class="sxs-lookup"><span data-stu-id="c933f-130">Event Processor Host APIs</span></span>
<span data-ttu-id="c933f-131">이러한 API는 사용 가능한 작업자에 걸쳐 파티션을 분산하여 사용할 수 없게 되는 작업자 프로세스에 복구 성능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c933f-131">These APIs provide resiliency to worker processes that may become unavailable, by distributing partitions across available workers.</span></span>

```csharp
// Checkpointing is done within the SimpleEventProcessor and on a per-consumerGroup per-partition basis, workers resume from where they last left off.

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

// Disposes of the Event Processor Host
await eventProcessorHost.UnregisterEventProcessorAsync();
```

<span data-ttu-id="c933f-132">다음은 [IEventProcessor](/dotnet/api/microsoft.azure.eventhubs.processor.ieventprocessor)의 구현 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="c933f-132">The following is a sample implementation of the [IEventProcessor](/dotnet/api/microsoft.azure.eventhubs.processor.ieventprocessor).</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="c933f-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c933f-133">Next steps</span></span>
<span data-ttu-id="c933f-134">이벤트 허브 시나리오에 대한 자세한 내용은 다음 링크를 방문하십시오.</span><span class="sxs-lookup"><span data-stu-id="c933f-134">To learn more about Event Hubs scenarios, visit these links:</span></span>

* [<span data-ttu-id="c933f-135">Azure 이벤트 허브 정의</span><span class="sxs-lookup"><span data-stu-id="c933f-135">What is Azure Event Hubs?</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="c933f-136">사용할 수 있는 Event Hubs API</span><span class="sxs-lookup"><span data-stu-id="c933f-136">Available Event Hubs apis</span></span>](event-hubs-api-overview.md)

<span data-ttu-id="c933f-137">.NET API 참조는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c933f-137">The .NET API references are here:</span></span>

* [<span data-ttu-id="c933f-138">Microsoft.Azure.EventHubs</span><span class="sxs-lookup"><span data-stu-id="c933f-138">Microsoft.Azure.EventHubs</span></span>](/dotnet/api/microsoft.azure.eventhubs)
* [<span data-ttu-id="c933f-139">Microsoft.Azure.EventHubs.Processor</span><span class="sxs-lookup"><span data-stu-id="c933f-139">Microsoft.Azure.EventHubs.Processor</span></span>](/dotnet/api/microsoft.azure.eventhubs.processor)
---
title: "hello Azure 이벤트 허브.NET Framework Api의 aaaOverview | Microsoft Docs"
description: "요약 hello 주요 이벤트 허브.NET Framework 클라이언트 Api의 일부입니다."
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 7f3b6cc0-9600-417f-9e80-2345411bd036
ms.service: event-hubs
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: b0e12e43f91b025d7aa4ca03e664b9ff31b04097
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-net-framework-api-overview"></a><span data-ttu-id="ed5d0-103">Event Hubs .NET Framework API 개요</span><span class="sxs-lookup"><span data-stu-id="ed5d0-103">Event Hubs .NET Framework API overview</span></span>
<span data-ttu-id="ed5d0-104">이 문서 hello 키 이벤트 허브.NET Framework 클라이언트 Api의 일부를 요약 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5d0-104">This article summarizes some of hello key Event Hubs .NET Framework client APIs.</span></span> <span data-ttu-id="ed5d0-105">관리와 런타임 API 등 두 가지 범주가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed5d0-105">There are two categories: management and run-time APIs.</span></span> <span data-ttu-id="ed5d0-106">런타임 Api에는 메시지를 수신 및 모든 필요한 작업 toosend 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed5d0-106">Run-time APIs consist of all operations needed toosend and receive a message.</span></span> <span data-ttu-id="ed5d0-107">관리 작업을 통해 toomanage 만들기, 업데이트 및 삭제 엔터티는 이벤트 허브 엔터티 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="ed5d0-107">Management operations enable you toomanage an Event Hubs entity state by creating, updating, and deleting entities.</span></span>

<span data-ttu-id="ed5d0-108">모니터링 시나리오는 관리 및 런타임 모두에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed5d0-108">Monitoring scenarios span both management and run-time.</span></span> <span data-ttu-id="ed5d0-109">Hello.NET Api에서 자세한 참조 설명서를 참조 hello [서비스 버스.NET](/dotnet/api/microsoft.servicebus.messaging) 및 [EventProcessorHost API](/dotnet/api/microsoft.azure.eventhubs.processor) 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5d0-109">For detailed reference documentation on hello .NET APIs, see hello [Service Bus .NET](/dotnet/api/microsoft.servicebus.messaging) and [EventProcessorHost API](/dotnet/api/microsoft.azure.eventhubs.processor) references.</span></span>

## <a name="management-apis"></a><span data-ttu-id="ed5d0-110">관리 API</span><span class="sxs-lookup"><span data-stu-id="ed5d0-110">Management APIs</span></span>
<span data-ttu-id="ed5d0-111">tooperform 있어야 합니다. 관리 작업을 다음 hello **관리** hello 이벤트 허브 네임 스페이스에 대 한 권한:</span><span class="sxs-lookup"><span data-stu-id="ed5d0-111">tooperform hello following management operations, you must have **Manage** permissions on hello Event Hubs namespace:</span></span>

### <a name="create"></a><span data-ttu-id="ed5d0-112">생성</span><span class="sxs-lookup"><span data-stu-id="ed5d0-112">Create</span></span>
```csharp
// Create hello event hub
var ehd = new EventHubDescription(eventHubName);
ehd.PartitionCount = SampleManager.numPartitions;
await namespaceManager.CreateEventHubAsync(ehd);
```

### <a name="update"></a><span data-ttu-id="ed5d0-113">업데이트</span><span class="sxs-lookup"><span data-stu-id="ed5d0-113">Update</span></span>
```csharp
var ehd = await namespaceManager.GetEventHubAsync(eventHubName);

// Create a customer SAS rule with Manage permissions
ehd.UserMetadata = "Some updated info";
var ruleName = "myeventhubmanagerule";
var ruleKey = SharedAccessAuthorizationRule.GenerateRandomKey();
ehd.Authorization.Add(new SharedAccessAuthorizationRule(ruleName, ruleKey, new AccessRights[] {AccessRights.Manage, AccessRights.Listen, AccessRights.Send} )); 
await namespaceManager.UpdateEventHubAsync(ehd);
```

### <a name="delete"></a><span data-ttu-id="ed5d0-114">삭제</span><span class="sxs-lookup"><span data-stu-id="ed5d0-114">Delete</span></span>
```csharp
await namespaceManager.DeleteEventHubAsync("Event Hub name");
```

## <a name="run-time-apis"></a><span data-ttu-id="ed5d0-115">런타임 API</span><span class="sxs-lookup"><span data-stu-id="ed5d0-115">Run-time APIs</span></span>
### <a name="create-publisher"></a><span data-ttu-id="ed5d0-116">게시자 만들기</span><span class="sxs-lookup"><span data-stu-id="ed5d0-116">Create publisher</span></span>
```csharp
// EventHubClient model (uses implicit factory instance, so all links on same connection)
var eventHubClient = EventHubClient.Create("Event Hub name");
```

### <a name="publish-message"></a><span data-ttu-id="ed5d0-117">메시지 게시</span><span class="sxs-lookup"><span data-stu-id="ed5d0-117">Publish message</span></span>
```csharp
// Create hello device/temperature metric
var info = new MetricEvent() { DeviceId = random.Next(SampleManager.NumDevices), Temperature = random.Next(100) };
var data = new EventData(new byte[10]); // Byte array
var data = new EventData(Stream); // Stream 
var data = new EventData(info, serializer) //Object and serializer 
{
    PartitionKey = info.DeviceId.ToString()
};

// Set user properties if needed
data.Properties.Add("Type", "Telemetry_" + DateTime.Now.ToLongTimeString());

// Send single message async
await client.SendAsync(data);
```

### <a name="create-consumer"></a><span data-ttu-id="ed5d0-118">소비자 만들기</span><span class="sxs-lookup"><span data-stu-id="ed5d0-118">Create consumer</span></span>
```csharp
// Create hello Event Hubs client
var eventHubClient = EventHubClient.Create(EventHubName);

// Get hello default consumer group
var defaultConsumerGroup = eventHubClient.GetDefaultConsumerGroup();

// All messages
var consumer = await defaultConsumerGroup.CreateReceiverAsync(partitionId: index);

// From one day ago
var consumer = await defaultConsumerGroup.CreateReceiverAsync(partitionId: index, startingDateTimeUtc:DateTime.Now.AddDays(-1));

// From specific offset, -1 means oldest
var consumer = await defaultConsumerGroup.CreateReceiverAsync(partitionId: index,startingOffset:-1); 
```

### <a name="consume-message"></a><span data-ttu-id="ed5d0-119">메시지 사용</span><span class="sxs-lookup"><span data-stu-id="ed5d0-119">Consume message</span></span>
```csharp
var message = await consumer.ReceiveAsync();

// Provide a serializer
var info = message.GetBody<Type>(Serializer)

// Get a byte[]
var info = message.GetBytes(); 
msg = UnicodeEncoding.UTF8.GetString(info);
```

## <a name="event-processor-host-apis"></a><span data-ttu-id="ed5d0-120">이벤트 프로세서 호스트 API</span><span class="sxs-lookup"><span data-stu-id="ed5d0-120">Event Processor Host APIs</span></span>
<span data-ttu-id="ed5d0-121">이러한 Api는 사용 가능한 작업자 파티션에 배포 하 여 사용할 수 없게 될 수 있는 복원 력 tooworker 프로세스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed5d0-121">These APIs provide resiliency tooworker processes that may become unavailable, by distributing partitions across available workers.</span></span>

```csharp
// Checkpointing is done within hello SimpleEventProcessor and on a per-consumerGroup per-partition basis, workers resume from where they last left off.
// Use hello EventData.Offset value for checkpointing yourself, this value is unique per partition.

var eventHubConnectionString = System.Configuration.ConfigurationManager.AppSettings["Microsoft.ServiceBus.ConnectionString"];
var blobConnectionString = System.Configuration.ConfigurationManager.AppSettings["AzureStorageConnectionString"]; // Required for checkpoint/state

var eventHubDescription = new EventHubDescription(EventHubName);
var host = new EventProcessorHost(WorkerName, EventHubName, defaultConsumerGroup.GroupName, eventHubConnectionString, blobConnectionString);
await host.RegisterEventProcessorAsync<SimpleEventProcessor>();

// tooclose
await host.UnregisterEventProcessorAsync();
```

<span data-ttu-id="ed5d0-122">hello [IEventProcessor](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor) 인터페이스는 다음과 같이 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed5d0-122">hello [IEventProcessor](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor) interface is defined as follows:</span></span>

```csharp
public class SimpleEventProcessor : IEventProcessor
{
    IDictionary<string, string> map;
    PartitionContext partitionContext;

    public SimpleEventProcessor()
    {
        this.map = new Dictionary<string, string>();
    }

    public Task OpenAsync(PartitionContext context)
    {
        this.partitionContext = context;

        return Task.FromResult<object>(null);
    }

    public async Task ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
    {
        foreach (EventData message in messages)
        {
            // Process messages here
        }

        // Checkpoint when appropriate
        await context.CheckpointAsync();

    }

    public async Task CloseAsync(PartitionContext context, CloseReason reason)
    {
        if (reason == CloseReason.Shutdown)
        {
            await context.CheckpointAsync();
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="ed5d0-123">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ed5d0-123">Next steps</span></span>
<span data-ttu-id="ed5d0-124">다음이 링크를 방문 하는 이벤트 허브 시나리오에 대해 자세히 toolearn:</span><span class="sxs-lookup"><span data-stu-id="ed5d0-124">toolearn more about Event Hubs scenarios, visit these links:</span></span>

* [<span data-ttu-id="ed5d0-125">Azure 이벤트 허브 정의</span><span class="sxs-lookup"><span data-stu-id="ed5d0-125">What is Azure Event Hubs?</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="ed5d0-126">이벤트 허브 프로그래밍 가이드</span><span class="sxs-lookup"><span data-stu-id="ed5d0-126">Event Hubs programming guide</span></span>](event-hubs-programming-guide.md)

<span data-ttu-id="ed5d0-127">hello.NET API 참조는 여기 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed5d0-127">hello .NET API references are here:</span></span>

* [<span data-ttu-id="ed5d0-128">Microsoft.ServiceBus.Messaging</span><span class="sxs-lookup"><span data-stu-id="ed5d0-128">Microsoft.ServiceBus.Messaging</span></span>](/dotnet/api/microsoft.servicebus.messaging)
* [<span data-ttu-id="ed5d0-129">Microsoft.Azure.EventHubs.EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="ed5d0-129">Microsoft.Azure.EventHubs.EventProcessorHost</span></span>](/dotnet/api/microsoft.azure.eventhubs.processor.eventprocessorhost)

---
title: "Azure Service Bus 메시지 큐, 토픽 및 구독 개요 | Microsoft Docs"
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
ms.openlocfilehash: 00f9f38fbae028486270053dedb4df580a3f1a44
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="service-bus-queues-topics-and-subscriptions"></a><span data-ttu-id="63b7d-103">Service Bus 큐, 토픽 및 구독</span><span class="sxs-lookup"><span data-stu-id="63b7d-103">Service Bus queues, topics, and subscriptions</span></span>

<span data-ttu-id="63b7d-104">Microsoft Azure Service Bus는 신뢰할 수 있는 메시지 큐 및 지속형 게시/구독 메시징을 포함하여 클라우드 기반, 메시지 지향 미들웨어 기술 집합을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-104">Microsoft Azure Service Bus supports a set of cloud-based, message-oriented middleware technologies including reliable message queuing and durable publish/subscribe messaging.</span></span> <span data-ttu-id="63b7d-105">이러한 "조정된" 메시지 기능은 Service Bus 메시지 패브릭을 사용하여 분리된 메시지 기능 게시-구독, 임시 분리 및 부하 분산 시나리오로 여겨질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-105">These "brokered" messaging capabilities can be thought of as decoupled messaging features that support publish-subscribe, temporal decoupling, and load balancing scenarios using the Service Bus messaging fabric.</span></span> <span data-ttu-id="63b7d-106">분리된 통신에는 많은 장점이 있습니다. 예를 들어 필요하면 클라이언트와 서버가 연결되고 비동기 방식으로 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-106">Decoupled communication has many advantages; for example, clients and servers can connect as needed and perform their operations in an asynchronous fashion.</span></span>

<span data-ttu-id="63b7d-107">Service Bus에서 메시지 기능의 핵심이 되는 메시지 엔터티는 큐, 토픽 및 구독, 규칙/동작입니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-107">The messaging entities that form the core of the messaging capabilities in Service Bus are queues, topics and subscriptions, and rules/actions.</span></span>

## <a name="queues"></a><span data-ttu-id="63b7d-108">큐</span><span class="sxs-lookup"><span data-stu-id="63b7d-108">Queues</span></span>

<span data-ttu-id="63b7d-109">큐는 하나 이상의 경쟁 소비자에게 *FIFO(선입선출)* 메시지 배달을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-109">Queues offer *First In, First Out* (FIFO) message delivery to one or more competing consumers.</span></span> <span data-ttu-id="63b7d-110">즉, 일반적으로 메시지가 큐에 추가된 순서대로 받는 사람이 메시지를 받고 처리하며, 각 메시지가 하나의 메시지 소비자에 의해서만 수신 및 처리될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-110">That is, messages are typically expected to be received and processed by the receivers in the order in which they were added to the queue, and each message is received and processed by only one message consumer.</span></span> <span data-ttu-id="63b7d-111">큐를 사용하는 주요 이점은 응용 프로그램 구성 요소를 "임시로 분리"할 수 있다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-111">A key benefit of using queues is to achieve "temporal decoupling" of application components.</span></span> <span data-ttu-id="63b7d-112">즉, 메시지가 큐에서 영구적으로 저장되기 때문에 생산자(발신자) 및 소비자(수신자)가 동시에 메시지를 보내고 받을 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-112">In other words, the producers (senders) and consumers (receivers) do not have to be sending and receiving messages at the same time, because messages are stored durably in the queue.</span></span> <span data-ttu-id="63b7d-113">또한 생산자는 계속해서 메시지를 처리하고 보내기 위해 소비자의 회신을 기다릴 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-113">Furthermore, the producer does not have to wait for a reply from the consumer in order to continue to process and send messages.</span></span>

<span data-ttu-id="63b7d-114">관련된 이점은 “부하 평준화”로 생산자와 소비자가 서로 다른 속도로 메시지를 주고받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-114">A related benefit is "load leveling," which enables producers and consumers to send and receive messages at different rates.</span></span> <span data-ttu-id="63b7d-115">많은 응용 프로그램에서 시스템 부하는 시간에 따라 다르지만 각 작업 단위에 필요한 처리 시간은 일반적으로 일정합니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-115">In many applications, the system load varies over time; however, the processing time required for each unit of work is typically constant.</span></span> <span data-ttu-id="63b7d-116">큐를 사용한 메시지 생산자와 소비자 조정은 최대 부하 대신 평균 부하를 다룰 수 있으려면 소비 응용 프로그램만 프로비전해야 함을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-116">Intermediating message producers and consumers with a queue means that the consuming application only has to be provisioned to be able to handle average load instead of peak load.</span></span> <span data-ttu-id="63b7d-117">수신 부하가 변경됨에 따라 큐의 깊이가 증가하고 축소됩니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-117">The depth of the queue grows and contracts as the incoming load varies.</span></span> <span data-ttu-id="63b7d-118">따라서 응용 프로그램 부하를 제공하는 데 필요한 인프라의 크기와 관련하여 비용이 직접적으로 절약됩니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-118">This directly saves money with regard to the amount of infrastructure required to service the application load.</span></span> <span data-ttu-id="63b7d-119">부하가 증가하면 큐에서 읽을 작업자 프로세스가 더 추가될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-119">As the load increases, more worker processes can be added to read from the queue.</span></span> <span data-ttu-id="63b7d-120">각 메시지는 하나의 작업자 프로세스를 통해서만 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-120">Each message is processed by only one of the worker processes.</span></span> <span data-ttu-id="63b7d-121">또한 이 가져오기 기반 부하 분산에서는 작업자 컴퓨터가 최대 속도로 메시지를 가져올 때 처리 능력이 다른 경우에도 작업자 컴퓨터의 최적 사용률을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-121">Furthermore, this pull-based load balancing allows for optimum use of the worker computers even if the worker computers differ with regard to processing power, as they will pull messages at their own maximum rate.</span></span> <span data-ttu-id="63b7d-122">이 패턴을 종종 “경쟁 소비자” 패턴이라고 부릅니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-122">This pattern is often termed the "competing consumer" pattern.</span></span>

<span data-ttu-id="63b7d-123">메시지 생산자와 소비자 간을 중개하는 큐를 사용하면 구성 요소 간에 내재하는 느슨한 연결을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-123">Using queues to intermediate between message producers and consumers provides an inherent loose coupling between the components.</span></span> <span data-ttu-id="63b7d-124">생산자와 소비자가 서로를 인식하지 않기 때문에 생산자에 영향을 주지 않고 소비자를 업그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-124">Because producers and consumers are not aware of each other, a consumer can be upgraded without having any effect on the producer.</span></span>

<span data-ttu-id="63b7d-125">큐 만들기는 여러 단계의 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-125">Creating a queue is a multi-step process.</span></span> <span data-ttu-id="63b7d-126">[Microsoft.ServiceBus.NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) 클래스를 통해 Service Bus 메시징 엔터티(큐 및 토픽 모두)에 대한 관리 작업을 수행하며 이는 Service Bus 네임스페이스 및 사용자 자격 증명의 기본 주소를 제공하여 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-126">You perform management operations for Service Bus messaging entities (both queues and topics) via the [Microsoft.ServiceBus.NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) class, which is constructed by supplying the base address of the Service Bus namespace and the user credentials.</span></span> <span data-ttu-id="63b7d-127">[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager)는 메시징 엔터티를 만들고 열거 및 삭제하기 위한 메서드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-127">[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) provides methods to create, enumerate and delete messaging entities.</span></span> <span data-ttu-id="63b7d-128">SAS 이름 및 키, 서비스 네임스페이스 관리 개체에서 [Microsoft.ServiceBus.TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#microsoft_servicebus_tokenprovider) 개체를 만든 후에 [Microsoft.ServiceBus.NamespaceManager.CreateQueue](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateQueue_System_String_) 메서드를 사용하여 큐를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-128">After creating a [Microsoft.ServiceBus.TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#microsoft_servicebus_tokenprovider) object from the SAS name and key, and a service namespace management object, you can use the [Microsoft.ServiceBus.NamespaceManager.CreateQueue](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateQueue_System_String_) method to create the queue.</span></span> <span data-ttu-id="63b7d-129">예:</span><span class="sxs-lookup"><span data-stu-id="63b7d-129">For example:</span></span>

```csharp
// Create management credentials
TokenProvider credentials = TokenProvider.CreateSharedAccessSignatureTokenProvider(sasKeyName,sasKeyValue);
// Create namespace client
NamespaceManager namespaceClient = new NamespaceManager(ServiceBusEnvironment.CreateServiceUri("sb", ServiceNamespace, string.Empty), credentials);
```

<span data-ttu-id="63b7d-130">서비스 버스 URI를 사용하여 큐 개체 및 메시징 팩터리를 인수로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-130">You can then create a queue object and a messaging factory with the Service Bus URI as an argument.</span></span> <span data-ttu-id="63b7d-131">예:</span><span class="sxs-lookup"><span data-stu-id="63b7d-131">For example:</span></span>

```csharp
QueueDescription myQueue;
myQueue = namespaceClient.CreateQueue("TestQueue");
MessagingFactory factory = MessagingFactory.Create(ServiceBusEnvironment.CreateServiceUri("sb", ServiceNamespace, string.Empty), credentials); 
QueueClient myQueueClient = factory.CreateQueueClient("TestQueue");
```

<span data-ttu-id="63b7d-132">그러면 큐로 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-132">You can then send messages to the queue.</span></span> <span data-ttu-id="63b7d-133">예를 들어 `MessageList`라는 조정된 메시지 목록이 있는 경우 코드는 다음과 유사하게 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-133">For example, if you have a list of brokered messages called `MessageList`, the code appears similar to the following:</span></span>

```csharp
for (int count = 0; count < 6; count++)
{
    var issue = MessageList[count];
    issue.Label = issue.Properties["IssueTitle"].ToString();
    myQueueClient.Send(issue);
}
```

<span data-ttu-id="63b7d-134">다음과 같이 큐에서 메시지를 받을 수 있습니다:</span><span class="sxs-lookup"><span data-stu-id="63b7d-134">You then receive messages from the queue as follows:</span></span>

```csharp
while ((message = myQueueClient.Receive(new TimeSpan(hours: 0, minutes: 0, seconds: 5))) != null)
    {
        Console.WriteLine(string.Format("Message received: {0}, {1}, {2}", message.SequenceNumber, message.Label, message.MessageId));
        message.Complete();

        Console.WriteLine("Processing message (sleeping...)");
        Thread.Sleep(1000);
    }
```

<span data-ttu-id="63b7d-135">[ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode) 모드에서 수신은 1단계 작업입니다. 즉, Service Bus가 요청을 받으면 메시지를 이용되는 것으로 표시하고 응용 프로그램에 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-135">In the [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, the receive operation is single-shot; that is, when Service Bus receives the request, it marks the message as being consumed and returns it to the application.</span></span> <span data-ttu-id="63b7d-136">**ReceiveAndDelete** 모드는 가장 단순한 모델이며, 응용 프로그램이 실패 이벤트 시 메시지를 처리하지 않아도 안전한 시나리오에서 효과적입니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-136">**ReceiveAndDelete** mode is the simplest model and works best for scenarios in which the application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="63b7d-137">이해를 돕기 위해 소비자가 수신 요청을 실행한 후 처리하기 전에 크래시되는 시나리오를 고려해 보세요.</span><span class="sxs-lookup"><span data-stu-id="63b7d-137">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="63b7d-138">서비스 버스가 메시지를 이용되는 것으로 표시했기 때문에 응용 프로그램이 다시 시작되고 메시지 이용을 다시 시작할 때 크래시 전에 이용된 메시지는 누락됩니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-138">Because Service Bus marks the message as being consumed, when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="63b7d-139">[PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode) 모드에서는 수신 작업이 2단계이므로 메시지 누락이 허용되지 않는 응용 프로그램을 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-139">In [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, the receive operation becomes two-stage, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="63b7d-140">서비스 버스는 요청을 받으면 소비할 다음 메시지를 찾아서 다른 소비자가 수신할 수 없도록 잠근 후 응용 프로그램에 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-140">When Service Bus receives the request, it finds the next message to be consumed, locks it to prevent other consumers from receiving it, and then returns it to the application.</span></span> <span data-ttu-id="63b7d-141">응용 프로그램은 메시지 처리를 완료하거나 추가 처리를 위해 안전하게 저장한 후 수신된 메시지에 대해 [Complete](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete)를 호출하여 수신 프로세스의 두 번째 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-141">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling [Complete](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) on the received message.</span></span> <span data-ttu-id="63b7d-142">Service Bus가 **Complete** 호출을 확인하면 메시지를 이용한 것으로 표시하고 큐에서 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-142">When Service Bus sees the **Complete** call, it marks the message as being consumed.</span></span>

<span data-ttu-id="63b7d-143">어떤 이유로든 수신 응용 프로그램이 메시지를 처리할 수 없는 경우 받은 메시지에 [Complete](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) 메서드 대신 [Abandon](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon) 메서드를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-143">If the application is unable to process the message for some reason, it can call the [Abandon](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon) method on the received message (instead of [Complete](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete)).</span></span> <span data-ttu-id="63b7d-144">그러면 서비스 버스에서 메시지의 잠금을 해제하므로 동일한 소비나 다른 경쟁적 소비자에게서 메시지를 다시 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-144">This enables Service Bus to unlock the message and make it available to be received again, either by the same consumer or by another competing consumer.</span></span> <span data-ttu-id="63b7d-145">두 번째로 잠금과 연결된 시간 제한도 있으며, 응용 프로그램에서 잠금 시간 제한이 만료되기 전에 메시지를 처리하지 못하는 경우(예: 응용 프로그램이 크래시되는 경우) Service Bus가 메시지를 잠금 해제하여 다시 받을 수 있게 합니다(기본적으로 [Abandon](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon) 작업 수행).</span><span class="sxs-lookup"><span data-stu-id="63b7d-145">Secondly, there is a timeout associated with the lock and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus unlocks the message and makes it available to be received again (essentially performing an [Abandon](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon) operation by default).</span></span>

<span data-ttu-id="63b7d-146">응용 프로그램이 메시지를 처리한 후 **Complete** 요청이 실행되기 전에 크래시되는 경우 다시 시작될 때 메시지가 응용 프로그램에 다시 배달됩니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-146">Note that in the event that the application crashes after processing the message, but before the **Complete** request is issued, the message is redelivered to the application when it restarts.</span></span> <span data-ttu-id="63b7d-147">이를 *최소 한 번 이상* 처리라고 합니다. 즉, 각 메시지가 최소 한 번 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-147">This is often called *At Least Once* processing; that is, each message is processed at least once.</span></span> <span data-ttu-id="63b7d-148">그러나 특정 상황에서는 동일한 메시지가 다시 배달될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-148">However, in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="63b7d-149">시나리오가 중복 처리를 허용하지 않는 경우 메시지의 **MessageId** 속성에 따라 얻을 수 있는 중복을 검색하려면 응용 프로그램에 추가 논리가 필요하며 이는 전달 시도를 걸쳐 일관성을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-149">If the scenario cannot tolerate duplicate processing, then additional logic is required in the application to detect duplicates which can be achieved based upon the **MessageId** property of the message, which remains constant across delivery attempts.</span></span> <span data-ttu-id="63b7d-150">*정확히 한번* 처리로 알려집니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-150">This is known as *Exactly Once* processing.</span></span>

## <a name="topics-and-subscriptions"></a><span data-ttu-id="63b7d-151">토픽 및 구독</span><span class="sxs-lookup"><span data-stu-id="63b7d-151">Topics and subscriptions</span></span>
<span data-ttu-id="63b7d-152">각 메시지가 단일 소비자에 의해 처리되는 큐와 반대로, *토픽*과 *구독*은 *게시/구독* 패턴을 사용하여 일 대 다 형태의 통신을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-152">In contrast to queues, in which each message is processed by a single consumer, *topics* and *subscriptions* provide a one-to-many form of communication, in a *publish/subscribe* pattern.</span></span> <span data-ttu-id="63b7d-153">많은 수혜자 수를 조정할 수 있도록 각 게시된 메시지를 토픽에 등록된 각 구독에서 사용할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-153">Useful for scaling to very large numbers of recipients, each published message is made available to each subscription registered with the topic.</span></span> <span data-ttu-id="63b7d-154">메시지를 토픽에 보내고 구독 단위로 설정할 수 있는 필터 규칙에 따라 하나 이상의 연결된 구독에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-154">Messages are sent to a topic and delivered to one or more associated subscriptions, depending on filter rules that can be set on a per-subscription basis.</span></span> <span data-ttu-id="63b7d-155">구독은 추가 필터를 사용하여 수신하려는 메시지를 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-155">The subscriptions can use additional filters to restrict the messages that they want to receive.</span></span> <span data-ttu-id="63b7d-156">메시지는 큐로 전송된 것과 동일한 방식으로 토픽에 전송되지만 메시지는 토픽에서 직접 수신되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-156">Messages are sent to a topic in the same way they are sent to a queue, but messages are not received from the topic directly.</span></span> <span data-ttu-id="63b7d-157">대신 구독에서 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-157">Instead, they are received from subscriptions.</span></span> <span data-ttu-id="63b7d-158">토픽 구독은 토픽에 전송된 메시지의 복사본을 받는 가상 큐와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-158">A topic subscription resembles a virtual queue that receives copies of the messages that are sent to the topic.</span></span> <span data-ttu-id="63b7d-159">메시지는 큐에서 수신하는 방식과 동일하게 구독에서 수신됩니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-159">Messages are received from a subscription identically to the way they are received from a queue.</span></span>

<span data-ttu-id="63b7d-160">비교를 통해 큐의 메시지 보내기 기능은 토픽에 직접 매핑하고 해당 메시지 받기 기능은 구독에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-160">By way of comparison, the message-sending functionality of a queue maps directly to a topic and its message-receiving functionality maps to a subscription.</span></span> <span data-ttu-id="63b7d-161">무엇보다도 즉, 구독은 큐와 관련하여 경쟁적 소비자, 임시 분리, 부하 평준화 및 부하 분산 등 이 섹션 앞 부분에서 설명한 동일한 패턴을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-161">Among other things, this means that subscriptions support the same patterns described earlier in this section with regard to queues: competing consumer, temporal decoupling, load leveling, and load balancing.</span></span>

<span data-ttu-id="63b7d-162">이전 섹션의 예제와 같이 토픽을 만드는 것은 큐를 만드는 것과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-162">Creating a topic is similar to creating a queue, as shown in the example in the previous section.</span></span> <span data-ttu-id="63b7d-163">서비스 URI를 만든 다음 [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) 클래스를 사용하여 네임스페이스 클라이언트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-163">Create the service URI, and then use the [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) class to create the namespace client.</span></span> <span data-ttu-id="63b7d-164">[CreateTopic](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateTopic_System_String_) 메서드를 사용하여 토픽을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-164">You can then create a topic using the [CreateTopic](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateTopic_System_String_) method.</span></span> <span data-ttu-id="63b7d-165">예:</span><span class="sxs-lookup"><span data-stu-id="63b7d-165">For example:</span></span>

```csharp
TopicDescription dataCollectionTopic = namespaceClient.CreateTopic("DataCollectionTopic");
```

<span data-ttu-id="63b7d-166">다음으로 원하는 대로 구독을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-166">Next, add subscriptions as desired:</span></span>

```csharp
SubscriptionDescription myAgentSubscription = namespaceClient.CreateSubscription(myTopic.Path, "Inventory");
SubscriptionDescription myAuditSubscription = namespaceClient.CreateSubscription(myTopic.Path, "Dashboard");
```

<span data-ttu-id="63b7d-167">그런 다음 토픽 클라이언트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-167">You can then create a topic client.</span></span> <span data-ttu-id="63b7d-168">예:</span><span class="sxs-lookup"><span data-stu-id="63b7d-168">For example:</span></span>

```csharp
MessagingFactory factory = MessagingFactory.Create(serviceUri, tokenProvider);
TopicClient myTopicClient = factory.CreateTopicClient(myTopic.Path)
```

<span data-ttu-id="63b7d-169">메시지 발신자를 사용하여 이전 섹션에서 보여준 것처럼 토픽에서 메시지를 보내고 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-169">Using the message sender, you can send and receive messages to and from the topic, as shown in the previous section.</span></span> <span data-ttu-id="63b7d-170">예:</span><span class="sxs-lookup"><span data-stu-id="63b7d-170">For example:</span></span>

```csharp
foreach (BrokeredMessage message in messageList)
{
    myTopicClient.Send(message);
    Console.WriteLine(
    string.Format("Message sent: Id = {0}, Body = {1}", message.MessageId, message.GetBody<string>()));
}
```

<span data-ttu-id="63b7d-171">큐와 마찬가지로 [QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient) 개체 대신 [SubscriptionClient](/dotnet/api/microsoft.servicebus.messaging.subscriptionclient) 개체를 사용하여 구독에서 메시지를 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-171">Similar to queues, messages are received from a subscription using a [SubscriptionClient](/dotnet/api/microsoft.servicebus.messaging.subscriptionclient) object instead of a [QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient) object.</span></span> <span data-ttu-id="63b7d-172">토픽의 이름, 구독의 이름 및 (선택 사항)수신 모드를 매개 변수로 전달하는 구독 클라이언트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-172">Create the subscription client, passing the name of the topic, the name of the subscription, and (optionally) the receive mode as parameters.</span></span> <span data-ttu-id="63b7d-173">예를 들어 **인벤토리** 구독을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-173">For example, with the **Inventory** subscription:</span></span>

```csharp
// Create the subscription client
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

### <a name="rules-and-actions"></a><span data-ttu-id="63b7d-174">규칙 및 동작</span><span class="sxs-lookup"><span data-stu-id="63b7d-174">Rules and actions</span></span>
<span data-ttu-id="63b7d-175">대부분의 시나리오에서 특정 특성을 가진 메시지를 다른 방법으로 처리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-175">In many scenarios, messages that have specific characteristics must be processed in different ways.</span></span> <span data-ttu-id="63b7d-176">이 기능을 사용하려면 구독을 구성하여 원하는 속성을 갖는 메시지를 찾은 다음 해당 속성에 특정 수정 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-176">To enable this, you can configure subscriptions to find messages that have desired properties and then perform certain modifications to those properties.</span></span> <span data-ttu-id="63b7d-177">Service Bus 구독이 토픽으로 전송된 모든 메시지를 확인하는 동안 가상 구독 큐로 이러한 메시지의 하위 집합을 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-177">While Service Bus subscriptions see all messages sent to the topic, you can only copy a subset of those messages to the virtual subscription queue.</span></span> <span data-ttu-id="63b7d-178">구독 필터를 사용하여 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-178">This is accomplished using subscription filters.</span></span> <span data-ttu-id="63b7d-179">이와 같은 수정을 *필터 동작*이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-179">Such modifications are called *filter actions*.</span></span> <span data-ttu-id="63b7d-180">구독을 만들 경우 메시지의 속성, 즉 시스템 속성(예: **Label**) 및 사용자 지정 응용 프로그램 속성(예:**StoreName**) 모두에서 작동하는 필터 식을 제공할 수 있습니다. 이 경우에 SQL 필터 식은 선택 사항입니다. SQL 필터 식 없이 구독에 정의된 필터 작업을 구독에 대한 모든 메시지에서 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-180">When a subscription is created, you can supply a filter expression that operates on the properties of the message, both the system properties (for example, **Label**) and custom application properties (for example, **StoreName**.) The SQL filter expression is optional in this case; without a SQL filter expression, any filter action defined on a subscription will be performed on all the messages for that subscription.</span></span>

<span data-ttu-id="63b7d-181">이전 예제를 사용하여 **저장소1**에서 오는 메시지를 필터링하려면 대시보드 구독을 다음과 같이 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-181">Using the previous example, to filter messages coming only from **Store1**, you would create the Dashboard subscription as follows:</span></span>

```csharp
namespaceManager.CreateSubscription("IssueTrackingTopic", "Dashboard", new SqlFilter("StoreName = 'Store1'"));
```

<span data-ttu-id="63b7d-182">구독 필터가 준비된 경우 `StoreName` 속성이 `Store1`로 설정된 메시지만이 `Dashboard` 구독에 대해 가상 큐에 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="63b7d-182">With this subscription filter in place, only messages that have the `StoreName` property set to `Store1` are copied to the virtual queue for the `Dashboard` subscription.</span></span>

<span data-ttu-id="63b7d-183">가능한 필터 값에 대한 자세한 내용은 [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) 및 [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) 클래스에 대한 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="63b7d-183">For more information about possible filter values, see the documentation for the [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) and [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) classes.</span></span> <span data-ttu-id="63b7d-184">또한 [조정된 메시징: 고급 필터](http://code.msdn.microsoft.com/Brokered-Messaging-6b0d2749) 및 [토픽 필터](https://github.com/Azure-Samples/azure-servicebus-messaging-samples/tree/master/TopicFilters) 샘플을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="63b7d-184">Also, see the [Brokered Messaging: Advanced Filters](http://code.msdn.microsoft.com/Brokered-Messaging-6b0d2749) and [Topic Filters](https://github.com/Azure-Samples/azure-servicebus-messaging-samples/tree/master/TopicFilters) samples.</span></span>

## <a name="next-steps"></a><span data-ttu-id="63b7d-185">다음 단계</span><span class="sxs-lookup"><span data-stu-id="63b7d-185">Next steps</span></span>
<span data-ttu-id="63b7d-186">Service Bus 메시지 사용에 대한 자세한 내용 및 예제는 다음 고급 토픽을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="63b7d-186">See the following advanced topics for more information and examples of using Service Bus messaging.</span></span>

* [<span data-ttu-id="63b7d-187">서비스 버스 메시징 개요</span><span class="sxs-lookup"><span data-stu-id="63b7d-187">Service Bus messaging overview</span></span>](service-bus-messaging-overview.md)
* [<span data-ttu-id="63b7d-188">Service Bus 조정된 메시징 .NET 자습서</span><span class="sxs-lookup"><span data-stu-id="63b7d-188">Service Bus brokered messaging .NET tutorial</span></span>](service-bus-brokered-tutorial-dotnet.md)
* [<span data-ttu-id="63b7d-189">Service Bus 조정된 메시징 REST 자습서</span><span class="sxs-lookup"><span data-stu-id="63b7d-189">Service Bus brokered messaging REST tutorial</span></span>](service-bus-brokered-tutorial-rest.md)
* [<span data-ttu-id="63b7d-190">토픽 필터 샘플</span><span class="sxs-lookup"><span data-stu-id="63b7d-190">Topic Filters sample </span></span>](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/TopicFilters)
* [<span data-ttu-id="63b7d-191">조정된 메시징: 고급 필터 샘플</span><span class="sxs-lookup"><span data-stu-id="63b7d-191">Brokered Messaging: Advanced Filters sample</span></span>](http://code.msdn.microsoft.com/Brokered-Messaging-6b0d2749)


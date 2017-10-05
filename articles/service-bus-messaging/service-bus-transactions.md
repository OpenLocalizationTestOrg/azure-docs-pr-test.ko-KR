---
title: "Azure Service Bus의 트랜잭션 처리 개요 | Microsoft Docs"
description: "Azure 서비스 버스 원자성 트랜잭션 및 send via에 대한 개요"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 64449247-1026-44ba-b15a-9610f9385ed8
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/17/2017
ms.author: clemensv;sethm
ms.openlocfilehash: a88f2d81ab43e38c9363a67aaefc178b47bfb259
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="overview-of-service-bus-transaction-processing"></a><span data-ttu-id="2a1e0-103">서비스 버스 트랜잭션 처리의 개요</span><span class="sxs-lookup"><span data-stu-id="2a1e0-103">Overview of Service Bus transaction processing</span></span>
<span data-ttu-id="2a1e0-104">이 문서에서는 Azure 서비스 버스의 트랜잭션 기능을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1e0-104">This article discusses the transaction capabilities of Azure Service Bus.</span></span> <span data-ttu-id="2a1e0-105">논의의 대부분은 [Service Bus와의 원자적 트랜잭선 샘플](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions)에서 다루고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1e0-105">Much of the discussion is illustrated by the [Atomic Transactions with Service Bus sample](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions).</span></span> <span data-ttu-id="2a1e0-106">이 문서는 트래잭션 처리에 대한 개요와 Service Bus의 *send via* 기능으로 제한되며 원자적 트랜잭선 샘플의 범위는 훨씬 광범위하고 더 복잡합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1e0-106">This article is limited to an overview of transaction processing and the *send via* feature in Service Bus, while the Atomic Transactions sample is broader and more complex in scope.</span></span>

## <a name="transactions-in-service-bus"></a><span data-ttu-id="2a1e0-107">서비스 버스의 트랜잭션</span><span class="sxs-lookup"><span data-stu-id="2a1e0-107">Transactions in Service Bus</span></span>
<span data-ttu-id="2a1e0-108">[트랜잭션](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions#what-are-transactions)은 두 개 이상의 작업을 *실행 범위*로 그룹화합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1e0-108">A [transaction](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions#what-are-transactions) groups two or more operations together into an *execution scope*.</span></span> <span data-ttu-id="2a1e0-109">기본적으로 이러한 트랜잭션은 지정된 작업 그룹에 속한 모든 작업이 성공 또는 실패해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1e0-109">By nature, such a transaction must ensure that all operations belonging to a given group of operations either succeed or fail jointly.</span></span> <span data-ttu-id="2a1e0-110">이러한 점에서 트랜잭션은 하나의 단위(또는 *원자성*이라고 함)로 작용합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1e0-110">In this respect transactions act as one unit, which is often referred to as *atomicity*.</span></span> 

<span data-ttu-id="2a1e0-111">서비스 버스는 트랜잭션 메시지 broker이며 메시지 저장소에 대한 모든 내부 작업의 트랜잭션 무결성을 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1e0-111">Service Bus is a transactional message broker and ensures transactional integrity for all internal operations against its message stores.</span></span> <span data-ttu-id="2a1e0-112">엔터티 간 메시지의 [원자성 전달](service-bus-auto-forwarding.md) 또는 [배달 못한 편지 큐](service-bus-dead-letter-queues.md)로 메시지 이동과 같이 서비스 버스 내 메시지의 모든 전송은 트랜잭션입니다.</span><span class="sxs-lookup"><span data-stu-id="2a1e0-112">All transfers of messages inside of Service Bus, such as moving messages to a [dead-letter queue](service-bus-dead-letter-queues.md) or [automatic forwarding](service-bus-auto-forwarding.md) of messages between entities, are transactional.</span></span> <span data-ttu-id="2a1e0-113">따라서 서비스 버스에서 메시지를 수락할 경우 이미 저장되어 시퀀스 번호가 레이블로 지정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1e0-113">As such, if Service Bus accepts a message, it has already been stored and labeled with a sequence number.</span></span> <span data-ttu-id="2a1e0-114">이후로 서비스 버스 내 메시지 전송은 엔터티 전반에서 조정된 작업으로 손실(원본 성공 및 대상 실패) 또는 메시지의 중복(원본 실패 및 대상 성공)이 발생하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1e0-114">From then on, any message transfers within Service Bus are coordinated operations across entities, and will neither lead to loss (source succeeds and target fails) or to duplication (source fails and target succeeds) of the message.</span></span>

<span data-ttu-id="2a1e0-115">Service Bus는 트랜잭션 범위 내에서 단일 메시징 엔터티(큐, 토픽, 구독)에 대한 그룹화 작업을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1e0-115">Service Bus supports grouping operations against a single messaging entity (queue, topic, subscription) within the scope of a transaction.</span></span> <span data-ttu-id="2a1e0-116">예를 들어 트랜잭션 범위 내에서 하나의 큐에 여러 메시지를 보낼 수 있으며, 트랜잭션이 성공적으로 완료되면 메시지가 큐의 로그에만 커밋됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a1e0-116">For example, you can send several messages to one queue from within a transaction scope, and the messages will only be committed to the queue's log when the transaction successfully completes.</span></span>

## <a name="operations-within-a-transaction-scope"></a><span data-ttu-id="2a1e0-117">트랜잭션 범위 내 작업</span><span class="sxs-lookup"><span data-stu-id="2a1e0-117">Operations within a transaction scope</span></span>
<span data-ttu-id="2a1e0-118">트랜잭션 범위 내에서 수행할 수 있는 작업은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1e0-118">The operations that can be performed within a transaction scope are as follows:</span></span>

* <span data-ttu-id="2a1e0-119">**[QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient), [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender), [TopicClient](/dotnet/api/microsoft.servicebus.messaging.topicclient)**: Send, SendAsync, SendBatch, SendBatchAsync</span><span class="sxs-lookup"><span data-stu-id="2a1e0-119">**[QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient), [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender), [TopicClient](/dotnet/api/microsoft.servicebus.messaging.topicclient)**: Send, SendAsync, SendBatch, SendBatchAsync</span></span> 
* <span data-ttu-id="2a1e0-120">**[BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)**: Complete, CompleteAsync, Abandon, AbandonAsync, Deadletter, DeadletterAsync, Defer, DeferAsync, RenewLock, RenewLockAsync</span><span class="sxs-lookup"><span data-stu-id="2a1e0-120">**[BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)**: Complete, CompleteAsync, Abandon, AbandonAsync, Deadletter, DeadletterAsync, Defer, DeferAsync, RenewLock, RenewLockAsync</span></span> 

<span data-ttu-id="2a1e0-121">응용 프로그램이 일부 수신 루프 내에서 또는 [OnMessage](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_OnMessage_System_Action_Microsoft_ServiceBus_Messaging_BrokeredMessage__Microsoft_ServiceBus_Messaging_OnMessageOptions_) 콜백과 함께 [ReceiveMode.PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode) 모드를 사용하여 메시지를 획득한다고 가정하므로 수신 작업은 포함되지 않으며, 메시지 처리에 대한 트랜잭션 범위만 열립니다.</span><span class="sxs-lookup"><span data-stu-id="2a1e0-121">Receive operations are not included, because it is assumed that the application acquires messages using the [ReceiveMode.PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, inside some receive loop or with an [OnMessage](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_OnMessage_System_Action_Microsoft_ServiceBus_Messaging_BrokeredMessage__Microsoft_ServiceBus_Messaging_OnMessageOptions_) callback, and only then opens a transaction scope for processing the message.</span></span>

<span data-ttu-id="2a1e0-122">메시지 처리(완료, 중단, 배달 못 한 편지, 지연)가 범위 내에서 그리고 전반적인 트랜잭션 결과에 다라 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1e0-122">The disposition of the message (complete, abandon, dead-letter, defer) then occurs within the scope of, and dependent on, the overall outcome of the transaction.</span></span>

## <a name="transfers-and-send-via"></a><span data-ttu-id="2a1e0-123">전송 및 "send via"</span><span class="sxs-lookup"><span data-stu-id="2a1e0-123">Transfers and "send via"</span></span>
<span data-ttu-id="2a1e0-124">큐에서 프로세서, 그런 다음 다른 큐로 데이터의 트랜잭션을 인도하기 위해 Service Bus는 *전송*을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1e0-124">To enable transactional handover of data from a queue to a processor, and then to another queue, Service Bus supports *transfers*.</span></span> <span data-ttu-id="2a1e0-125">전송 작업에서 발신자는 “전송 큐”로 메시지를 전송하며 전송 큐는 자동 전달 기능이 적용된 것과 같은 강력한 전송 구현을 사용하여 의도된 대상 큐로 메시지를 즉시 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1e0-125">In a transfer operation, a sender first sends a message to a "transfer queue" and the transfer queue immediately moves the message to the intended destination queue using the same robust transfer implementation that the auto-forward capability relies on.</span></span> <span data-ttu-id="2a1e0-126">이 메시지는 전송 큐의 소비자에게 표시되는 방식으로 전송 큐의 로그에 커밋되지 안습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1e0-126">The message is never committed to the transfer queue's log in a way that it becomes visible for the transfer queue's consumers.</span></span>

<span data-ttu-id="2a1e0-127">이 트랜잭션 기능 자체는 전송 큐가 발신자의 입력 메시지 원본인 경우에 분명해집니다.</span><span class="sxs-lookup"><span data-stu-id="2a1e0-127">The power of this transactional capability becomes apparent when the transfer queue itself is the source of the sender's input messages.</span></span> <span data-ttu-id="2a1e0-128">즉, 서비스 버스는 하나의 통합된 원자성 작업으로 입력 메시지에 대한 완료(또는 지연, 또는 배달 못 한 편지) 작업을 수행하면서 메시지를 전송 큐를 “통해" 대상 큐로 메시지를 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1e0-128">In other words, Service Bus can transfer the message to the destination queue "via" the transfer queue, while performing a complete (or defer, or dead-letter) operation on the input message, all in one atomic operation.</span></span> 

### <a name="see-it-in-code"></a><span data-ttu-id="2a1e0-129">실제 코드 엿보기</span><span class="sxs-lookup"><span data-stu-id="2a1e0-129">See it in code</span></span>
<span data-ttu-id="2a1e0-130">이러한 전송을 설정하기 위해 전송 큐를 통해 대상 큐를 목표로 하는 메시지 보낸 사람을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1e0-130">To set up such transfers, you create a message sender that targets the destination queue via the transfer queue.</span></span> <span data-ttu-id="2a1e0-131">또한, 같은 큐에서 메시지를 풀링하는 수신기가 있을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a1e0-131">You will also have a receiver that pulls messages from that same queue.</span></span> <span data-ttu-id="2a1e0-132">예:</span><span class="sxs-lookup"><span data-stu-id="2a1e0-132">For example:</span></span>

```csharp
var sender = this.messagingFactory.CreateMessageSender(destinationQueue, myQueueName);
var receiver = this.messagingFactory.CreateMessageReceiver(myQueueName);
```

<span data-ttu-id="2a1e0-133">다음 예와 같이 간단한 트랜잭션이 이러한 요소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2a1e0-133">A simple transaction then uses these elements, as in the following example:</span></span>

```csharp
var msg = receiver.Receive();

using (scope = new TransactionScope())
{
    // Do whatever work is required 

    var newmsg = ... // package the result 

    msg.Complete(); // mark the message as done
    sender.Send(newmsg); // forward the result

    scope.Complete(); // declare the transaction done
} 
```

## <a name="next-steps"></a><span data-ttu-id="2a1e0-134">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2a1e0-134">Next steps</span></span>

<span data-ttu-id="2a1e0-135">서비스 버스 큐에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2a1e0-135">See the following articles for more information about Service Bus queues:</span></span>

* [<span data-ttu-id="2a1e0-136">자동 전달을 사용한 Service Bus 엔터티 연결</span><span class="sxs-lookup"><span data-stu-id="2a1e0-136">Chaining Service Bus entities with auto-forwarding</span></span>](service-bus-auto-forwarding.md)
* [<span data-ttu-id="2a1e0-137">자동 전달 샘플</span><span class="sxs-lookup"><span data-stu-id="2a1e0-137">Auto-forward sample</span></span>](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AutoForward)
* [<span data-ttu-id="2a1e0-138">Service Bus 샘플과 함께 원자성 트랜잭션</span><span class="sxs-lookup"><span data-stu-id="2a1e0-138">Atomic Transactions with Service Bus sample</span></span>](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions)
* [<span data-ttu-id="2a1e0-139">Azure 큐와 Service Bus 큐 비교</span><span class="sxs-lookup"><span data-stu-id="2a1e0-139">Azure Queues and Service Bus queues compared</span></span>](service-bus-azure-and-service-bus-queues-compared-contrasted.md)
* [<span data-ttu-id="2a1e0-140">서비스 버스 큐를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="2a1e0-140">How to use Service Bus queues</span></span>](service-bus-dotnet-get-started-with-queues.md)


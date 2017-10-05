---
title: "Azure Service Bus 메시징 엔터티 자동 전달 | Microsoft Docs"
description: "Service Bus 큐 또는 구독을 다른 큐 또는 토픽에 연결하는 방법"
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: f7060778-3421-402c-97c7-735dbf6a61e8
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: 2656b3a276c542ca836b3949e4e493d7c7f48f16
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="chaining-service-bus-entities-with-auto-forwarding"></a><span data-ttu-id="2c316-103">자동 전달을 사용한 Service Bus 엔터티 연결</span><span class="sxs-lookup"><span data-stu-id="2c316-103">Chaining Service Bus entities with auto-forwarding</span></span>

<span data-ttu-id="2c316-104">Service Bus *자동 전달* 기능을 통해 동일한 네임스페이스의 일부인 다른 큐 또는 토픽에 큐 또는 구독을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c316-104">The Service Bus *auto-forwarding* feature enables you to chain a queue or subscription to another queue or topic that is part of the same namespace.</span></span> <span data-ttu-id="2c316-105">자동 전달을 사용하도록 설정하면 Service Bus가 자동으로 첫 번째 큐 또는 구독(원본)에 있는 메시지를 제거하고 두 번째 큐 또는 토픽(대상)에 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="2c316-105">When auto-forwarding is enabled, Service Bus automatically removes messages that are placed in the first queue or subscription (source) and puts them in the second queue or topic (destination).</span></span> <span data-ttu-id="2c316-106">대상 엔터티에 직접 메시지를 보내는 것은 여전히 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="2c316-106">Note that it is still possible to send a message to the destination entity directly.</span></span> <span data-ttu-id="2c316-107">또한 배달 못한 메시지 큐와 같은 하위 큐를 다른 큐나 토픽으로 연결할 수도 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2c316-107">Also, it is not possible to chain a subqueue, such as a deadletter queue, to another queue or topic.</span></span>

## <a name="using-auto-forwarding"></a><span data-ttu-id="2c316-108">자동 전달 사용</span><span class="sxs-lookup"><span data-stu-id="2c316-108">Using auto-forwarding</span></span>
<span data-ttu-id="2c316-109">자동 전달은 다음 예와 같이 [QueueDescription][QueueDescription] 또는 [SubscriptionDescription][SubscriptionDescription] 개체를 원본으로 하는 [QueueDescription.ForwardTo][QueueDescription.ForwardTo] 또는 [SubscriptionDescription.ForwardTo][SubscriptionDescription.ForwardTo] 속성을 설정하여 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c316-109">You can enable auto-forwarding by setting the [QueueDescription.ForwardTo][QueueDescription.ForwardTo] or [SubscriptionDescription.ForwardTo][SubscriptionDescription.ForwardTo] properties on the [QueueDescription][QueueDescription] or [SubscriptionDescription][SubscriptionDescription] objects for the source, as in the following example.</span></span>

```csharp
SubscriptionDescription srcSubscription = new SubscriptionDescription (srcTopic, srcSubscriptionName);
srcSubscription.ForwardTo = destTopic;
namespaceManager.CreateSubscription(srcSubscription));
```

<span data-ttu-id="2c316-110">원본 엔터티가 생성될 시점에 대상 엔터티가 존재해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c316-110">The destination entity must exist at the time the source entity is created.</span></span> <span data-ttu-id="2c316-111">대상 엔터티가 없는 경우 Service Bus에 원본 엔터티를 만드는 요청을 보내면 예외가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c316-111">If the destination entity does not exist, Service Bus returns an exception when asked to create the source entity.</span></span>

<span data-ttu-id="2c316-112">개별 토픽을 자동 전달하도록 확장할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c316-112">You can use auto-forwarding to scale out an individual topic.</span></span> <span data-ttu-id="2c316-113">Service Bus는 [지정된 토픽에 대한 구독 수](service-bus-quotas.md)를 2,000으로 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="2c316-113">Service Bus limits the [number of subscriptions on a given topic](service-bus-quotas.md) to 2,000.</span></span> <span data-ttu-id="2c316-114">두 번째 수준의 토픽을 만들면 구독의 수를 늘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c316-114">You can accommodate additional subscriptions by creating second-level topics.</span></span> <span data-ttu-id="2c316-115">Service Bus의 구독 수 제한에 묶여 있는 경우가 아니라도, 두 번째 수준의 토픽을 추가하면 토픽의 전체적인 처리량을 늘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c316-115">Note that even if you are not bound by the Service Bus limitation on the number of subscriptions, adding a second level of topics can improve the overall throughput of your topic.</span></span>

![자동 전달 시나리오][0]

<span data-ttu-id="2c316-117">자동 전달 기능을 메시지 발신자와 수신자를 분리하는 데에도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c316-117">You can also use auto-forwarding to decouple message senders from receivers.</span></span> <span data-ttu-id="2c316-118">주문 처리, 재고 관리 및 고객 관계 관리라는 세 모듈로 구성된 ERP 시스템을 예로 들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2c316-118">For example, consider an ERP system that consists of three modules: order processing, inventory management, and customer relations management.</span></span> <span data-ttu-id="2c316-119">이러한 각 모듈은 해당 토픽의 큐에 저장되는 메시지를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="2c316-119">Each of these modules generates messages that are enqueued into a corresponding topic.</span></span> <span data-ttu-id="2c316-120">Alice와 Bob은 고객에 관련된 모든 메시지에 관심이 있는 영업 담당자입니다.</span><span class="sxs-lookup"><span data-stu-id="2c316-120">Alice and Bob are sales representatives that are interested in all messages that relate to their customers.</span></span> <span data-ttu-id="2c316-121">Alice와 Bob이 이러한 메시지를 받으려면 각 ERP 토픽에 개인 큐와 구독을 만들어 모든 메시지가 자신의 큐로 자동으로 전달되도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c316-121">To receive those messages, Alice and Bob each create a personal queue and a subscription on each of the ERP topics that automatically forward all messages to their queue.</span></span>

![자동 전달 시나리오][1]

<span data-ttu-id="2c316-123">Alice가 휴가를 가면 ERP 토픽이 아닌 그녀의 개인 큐가 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="2c316-123">If Alice goes on vacation, her personal queue, rather than the ERP topic, fills up.</span></span> <span data-ttu-id="2c316-124">이러한 경우 영업 담당자가 메시지를 확인하지 못하기 때문에 어떤 ERP 토픽도 할당량에 도달하지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="2c316-124">In this scenario, because a sales representative has not received any messages, none of the ERP topics ever reach quota.</span></span>

## <a name="auto-forwarding-considerations"></a><span data-ttu-id="2c316-125">자동 전달 고려 사항</span><span class="sxs-lookup"><span data-stu-id="2c316-125">Auto-forwarding considerations</span></span>

<span data-ttu-id="2c316-126">대상 엔터티에 많은 메시지가 누적되어 할당량을 초과하거나 대상 엔터티가 사용하지 않도록 설정되는 경우, 원본 엔터티는 대상에 공간이 생길 때까지(또는 엔터티가 다시 사용하도록 설정됨) 메시지를 [배달 못 한 편지 큐](service-bus-dead-letter-queues.md)에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2c316-126">If the destination entity accumulates too many messages and exceeds the quota, or the destination entity is disabled, the source entity adds the messages to its [dead-letter queue](service-bus-dead-letter-queues.md) until there is space in the destination (or the entity is re-enabled).</span></span> <span data-ttu-id="2c316-127">이러한 메시지는 배달 못한 큐에 계속 남아 있으므로, 배달 못한 큐에서 직접 수령하여 처리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c316-127">Those messages will continue to live in the dead-letter queue, so you must explicitly receive and process them from the dead-letter queue.</span></span>

<span data-ttu-id="2c316-128">여러 구독이 있는 복합 토픽을 받기 위해 개별 토픽을 연결하는 경우, 첫 번째 수준의 토픽에 있는 구독의 수를 조정하고 두 번째 수준의 토픽에 많은 구독이 있도록 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2c316-128">When chaining together individual topics to obtain a composite topic with many subscriptions, it is recommended that you have a moderate number of subscriptions on the first-level topic and many subscriptions on the second-level topics.</span></span> <span data-ttu-id="2c316-129">예를 들어 첫 번째 수준의 토픽에 20개의 구독이 있고, 각 구독이 두 번째 수준의 토픽에 있는 200개 구독에 연결될 경우, 첫 번째 수준의 토픽에 200개 구독이 있고 각 구독이 두 번째 토픽에 있는 20개의 구독에 연결되는 것보다 처리량이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="2c316-129">For example, a first-level topic with 20 subscriptions, each of them chained to a second-level topic with 200 subscriptions, allows for higher throughput than a first-level topic with 200 subscriptions, each chained to a second-level topic with 20 subscriptions.</span></span>

<span data-ttu-id="2c316-130">Service Bus는 전달된 각 메시지당 하나의 작업을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="2c316-130">Service Bus bills one operation for each forwarded message.</span></span> <span data-ttu-id="2c316-131">예를 들어, 20개의 구독이 있는 토픽이 다른 큐나 토픽으로 메시지를 자동 전달하도록 구성된 경우, 이 토픽으로 메시지를 보내면 모든 첫 번째 수준의 구독이 메시지 복사본을 받을 경우 21개 작업이 요청됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c316-131">For example, sending a message to a topic with 20 subscriptions, each of them configured to auto-forward messages to another queue or topic, is billed as 21 operations if all first-level subscriptions receive a copy of the message.</span></span>

<span data-ttu-id="2c316-132">다른 큐나 토픽에 연결될 구독을 만들려면 구독을 만든 사람에게 원본과 대상 엔터티에 대한 **관리** 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c316-132">To create a subscription that is chained to another queue or topic, the creator of the subscription must have **Manage** permissions on both the source and the destination entity.</span></span> <span data-ttu-id="2c316-133">원본 토픽에 메시지를 보낼 때는 원본 토픽에 대한 **보내기** 권한만 있으면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c316-133">Sending messages to the source topic only requires **Send** permissions on the source topic.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2c316-134">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2c316-134">Next steps</span></span>

<span data-ttu-id="2c316-135">자동 전달에 대한 자세한 내용은 다음 참조 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2c316-135">For detailed information about auto-forwarding, see the following reference topics:</span></span>

* <span data-ttu-id="2c316-136">[ForwardTo][QueueDescription.ForwardTo]</span><span class="sxs-lookup"><span data-stu-id="2c316-136">[ForwardTo][QueueDescription.ForwardTo]</span></span>
* <span data-ttu-id="2c316-137">[QueueDescription][QueueDescription]</span><span class="sxs-lookup"><span data-stu-id="2c316-137">[QueueDescription][QueueDescription]</span></span>
* <span data-ttu-id="2c316-138">[SubscriptionDescription][SubscriptionDescription]</span><span class="sxs-lookup"><span data-stu-id="2c316-138">[SubscriptionDescription][SubscriptionDescription]</span></span>

<span data-ttu-id="2c316-139">Service Bus 성능 향상에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2c316-139">To learn more about Service Bus performance improvements, see</span></span> 

* [<span data-ttu-id="2c316-140">Service Bus 메시징을 사용한 성능 향상의 모범 사례</span><span class="sxs-lookup"><span data-stu-id="2c316-140">Best Practices for performance improvements using Service Bus Messaging</span></span>](service-bus-performance-improvements.md)
* <span data-ttu-id="2c316-141">[분할된 메시징 엔터티][Partitioned messaging entities]</span><span class="sxs-lookup"><span data-stu-id="2c316-141">[Partitioned messaging entities][Partitioned messaging entities].</span></span>

[QueueDescription.ForwardTo]: /dotnet/api/microsoft.servicebus.messaging.queuedescription.forwardto#Microsoft_ServiceBus_Messaging_QueueDescription_ForwardTo
[SubscriptionDescription.ForwardTo]: /dotnet/api/microsoft.servicebus.messaging.subscriptiondescription.forwardto#Microsoft_ServiceBus_Messaging_SubscriptionDescription_ForwardTo
[QueueDescription]: /dotnet/api/microsoft.servicebus.messaging.queuedescription
[SubscriptionDescription]: /dotnet/api/microsoft.servicebus.messaging.queuedescription
[0]: ./media/service-bus-auto-forwarding/IC628631.gif
[1]: ./media/service-bus-auto-forwarding/IC628632.gif
[Partitioned messaging entities]: service-bus-partitioning.md

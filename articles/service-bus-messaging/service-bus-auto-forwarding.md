---
title: "Azure 서비스 버스 메시징 엔터티 aaaAuto 전달 | Microsoft Docs"
description: "어떻게 toochain 서비스 버스 큐 또는 구독 tooanother 큐 또는 항목."
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
ms.openlocfilehash: af18273e4e2f81c5363eb830c7decf313afd8307
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="chaining-service-bus-entities-with-auto-forwarding"></a><span data-ttu-id="03a7c-103">자동 전달을 사용한 Service Bus 엔터티 연결</span><span class="sxs-lookup"><span data-stu-id="03a7c-103">Chaining Service Bus entities with auto-forwarding</span></span>

<span data-ttu-id="03a7c-104">서비스 버스 hello *자동 전달* 기능 하면 toochain 큐 또는 구독 tooanother 큐 또는 항목 hello의 일부인 동일한 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="03a7c-104">hello Service Bus *auto-forwarding* feature enables you toochain a queue or subscription tooanother queue or topic that is part of hello same namespace.</span></span> <span data-ttu-id="03a7c-105">자동 전달을 사용 하면 서비스 버스 자동으로 hello 첫 번째 큐 나 구독 (원본)에 저장 된 메시지를 제거 하 고 hello 두 번째 큐 나 항목 (대상)에 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="03a7c-105">When auto-forwarding is enabled, Service Bus automatically removes messages that are placed in hello first queue or subscription (source) and puts them in hello second queue or topic (destination).</span></span> <span data-ttu-id="03a7c-106">여전히 가능한 toosend 메시지 toohello 대상 엔터티에 직접 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="03a7c-106">Note that it is still possible toosend a message toohello destination entity directly.</span></span> <span data-ttu-id="03a7c-107">또한, 가능한 toochain 같은 배달 못한 편지 큐, tooanother 큐 또는 항목 하위 않습니다.</span><span class="sxs-lookup"><span data-stu-id="03a7c-107">Also, it is not possible toochain a subqueue, such as a deadletter queue, tooanother queue or topic.</span></span>

## <a name="using-auto-forwarding"></a><span data-ttu-id="03a7c-108">자동 전달 사용</span><span class="sxs-lookup"><span data-stu-id="03a7c-108">Using auto-forwarding</span></span>
<span data-ttu-id="03a7c-109">Hello 설정 하 여 자동 전달을 활성화할 수 [QueueDescription.ForwardTo] [ QueueDescription.ForwardTo] 또는 [SubscriptionDescription.ForwardTo] [ SubscriptionDescription.ForwardTo] hello에 대 한 속성 [QueueDescription] [ QueueDescription] 또는 [SubscriptionDescription] [ SubscriptionDescription] hello와 같이 hello 소스에 대 한 개체 다음 예제에서는 합니다.</span><span class="sxs-lookup"><span data-stu-id="03a7c-109">You can enable auto-forwarding by setting hello [QueueDescription.ForwardTo][QueueDescription.ForwardTo] or [SubscriptionDescription.ForwardTo][SubscriptionDescription.ForwardTo] properties on hello [QueueDescription][QueueDescription] or [SubscriptionDescription][SubscriptionDescription] objects for hello source, as in hello following example.</span></span>

```csharp
SubscriptionDescription srcSubscription = new SubscriptionDescription (srcTopic, srcSubscriptionName);
srcSubscription.ForwardTo = destTopic;
namespaceManager.CreateSubscription(srcSubscription));
```

<span data-ttu-id="03a7c-110">hello 대상 엔터티에 원본 엔터티를 hello hello 시 존재 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="03a7c-110">hello destination entity must exist at hello time hello source entity is created.</span></span> <span data-ttu-id="03a7c-111">Hello 대상 엔터티가 없는 경우 서비스 버스 묻는 toocreate hello 소스 엔터티의 경우 예외를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="03a7c-111">If hello destination entity does not exist, Service Bus returns an exception when asked toocreate hello source entity.</span></span>

<span data-ttu-id="03a7c-112">개별 항목으로 자동 전달 tooscale를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03a7c-112">You can use auto-forwarding tooscale out an individual topic.</span></span> <span data-ttu-id="03a7c-113">서비스 버스 제한 hello [구독에 지정된 된 항목 수가](service-bus-quotas.md) too2, 000입니다.</span><span class="sxs-lookup"><span data-stu-id="03a7c-113">Service Bus limits hello [number of subscriptions on a given topic](service-bus-quotas.md) too2,000.</span></span> <span data-ttu-id="03a7c-114">두 번째 수준의 토픽을 만들면 구독의 수를 늘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03a7c-114">You can accommodate additional subscriptions by creating second-level topics.</span></span> <span data-ttu-id="03a7c-115">Hello로 바인딩되지 않은 경우에 서비스 버스 구독을 두 번째 수준의 항목을 추가 hello 수 한계를 향상 시킬 수 있습니다 hello 항목의 전체 처리량을 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="03a7c-115">Note that even if you are not bound by hello Service Bus limitation on hello number of subscriptions, adding a second level of topics can improve hello overall throughput of your topic.</span></span>

![자동 전달 시나리오][0]

<span data-ttu-id="03a7c-117">또한 자동 전달을 toodecouple 메시지 발신자와 수신자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03a7c-117">You can also use auto-forwarding toodecouple message senders from receivers.</span></span> <span data-ttu-id="03a7c-118">주문 처리, 재고 관리 및 고객 관계 관리라는 세 모듈로 구성된 ERP 시스템을 예로 들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="03a7c-118">For example, consider an ERP system that consists of three modules: order processing, inventory management, and customer relations management.</span></span> <span data-ttu-id="03a7c-119">이러한 각 모듈은 해당 토픽의 큐에 저장되는 메시지를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="03a7c-119">Each of these modules generates messages that are enqueued into a corresponding topic.</span></span> <span data-ttu-id="03a7c-120">Alice와 Bob은 tootheir 고객 관련 된 모든 메시지에 관심이 있는 영업 담당자입니다.</span><span class="sxs-lookup"><span data-stu-id="03a7c-120">Alice and Bob are sales representatives that are interested in all messages that relate tootheir customers.</span></span> <span data-ttu-id="03a7c-121">tooreceive 해당 메시지를 Alice 및 Bob은 각 개인 큐 및 구독을 만들 각 자동으로 모든 메시지 tootheir 큐를 전달 하는 hello ERP 항목에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03a7c-121">tooreceive those messages, Alice and Bob each create a personal queue and a subscription on each of hello ERP topics that automatically forward all messages tootheir queue.</span></span>

![자동 전달 시나리오][1]

<span data-ttu-id="03a7c-123">Alice 휴가, 그녀의 개인 큐 아닌 이동 hello ERP 항목, 꽉 됩니다.</span><span class="sxs-lookup"><span data-stu-id="03a7c-123">If Alice goes on vacation, her personal queue, rather than hello ERP topic, fills up.</span></span> <span data-ttu-id="03a7c-124">이 시나리오에서는 영업 담당자는 모든 메시지를 수신 하지 못했기 때문에 어떤 hello ERP 항목도 할당량에 도달 하지 합니다.</span><span class="sxs-lookup"><span data-stu-id="03a7c-124">In this scenario, because a sales representative has not received any messages, none of hello ERP topics ever reach quota.</span></span>

## <a name="auto-forwarding-considerations"></a><span data-ttu-id="03a7c-125">자동 전달 고려 사항</span><span class="sxs-lookup"><span data-stu-id="03a7c-125">Auto-forwarding considerations</span></span>

<span data-ttu-id="03a7c-126">Hello 소스 엔터티 hello 메시지 tooits hello 대상 엔터티에 너무 많은 메시지를 누적 및 hello 할당량 초과 또는 hello 대상 엔터티를 사용 하지 않도록 설정 하는 경우 추가 [배달 못 한 편지 큐](service-bus-dead-letter-queues.md) hello 대상에 공간이 없을 때까지 (또는 hello 엔터티는 다시 사용 하도록 설정).</span><span class="sxs-lookup"><span data-stu-id="03a7c-126">If hello destination entity accumulates too many messages and exceeds hello quota, or hello destination entity is disabled, hello source entity adds hello messages tooits [dead-letter queue](service-bus-dead-letter-queues.md) until there is space in hello destination (or hello entity is re-enabled).</span></span> <span data-ttu-id="03a7c-127">이러한 메시지는 명시적으로 수신 하 고 hello 배달 못 한 편지 큐에서 처리 해야 하므로 toolive hello 배달 못 한 편지 큐에 계속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="03a7c-127">Those messages will continue toolive in hello dead-letter queue, so you must explicitly receive and process them from hello dead-letter queue.</span></span>

<span data-ttu-id="03a7c-128">개별 항목 tooobtain 많은 구독이 있는 복합 항목을 함께 연결, hello 첫 번째 수준 항목에는 구독 및 hello 두 번째 수준 항목에 대해 많은 구독 수가 적당 한지 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="03a7c-128">When chaining together individual topics tooobtain a composite topic with many subscriptions, it is recommended that you have a moderate number of subscriptions on hello first-level topic and many subscriptions on hello second-level topics.</span></span> <span data-ttu-id="03a7c-129">예를 들어 첫 번째 수준 항목에 20 개의 구독이 연결 하는 각 200 개의 구독이 있는 첫 번째 수준 항목 보다 더 높은 처리량 200 개의 구독이 있는 tooa 두 번째 수준 항목에서는 각 연결에 20 개의 구독이 tooa 두 번째 수준 항목 .</span><span class="sxs-lookup"><span data-stu-id="03a7c-129">For example, a first-level topic with 20 subscriptions, each of them chained tooa second-level topic with 200 subscriptions, allows for higher throughput than a first-level topic with 200 subscriptions, each chained tooa second-level topic with 20 subscriptions.</span></span>

<span data-ttu-id="03a7c-130">Service Bus는 전달된 각 메시지당 하나의 작업을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="03a7c-130">Service Bus bills one operation for each forwarded message.</span></span> <span data-ttu-id="03a7c-131">예를 들어 tooauto 정방향 메시지 모든 첫 번째 수준의 구독이 hello 메시지의 복사본을 받을 경우 tooanother 큐 또는 항목 21 개의 작업으로 청구 됩니다 구성 된에 20 개의 구독이 메시지 tooa 항목 보내기, 각각의 합니다.</span><span class="sxs-lookup"><span data-stu-id="03a7c-131">For example, sending a message tooa topic with 20 subscriptions, each of them configured tooauto-forward messages tooanother queue or topic, is billed as 21 operations if all first-level subscriptions receive a copy of hello message.</span></span>

<span data-ttu-id="03a7c-132">tooanother 체인으로 연결 된 큐 또는 항목은 구독을 toocreate hello 구독의 hello 작성자 있어야 **관리** hello 원본과 hello 대상 엔터티 모두에 대 한 권한.</span><span class="sxs-lookup"><span data-stu-id="03a7c-132">toocreate a subscription that is chained tooanother queue or topic, hello creator of hello subscription must have **Manage** permissions on both hello source and hello destination entity.</span></span> <span data-ttu-id="03a7c-133">보내는 메시지 toohello 소스 항목 필요 **보낼** hello 소스 항목에 대 한 권한.</span><span class="sxs-lookup"><span data-stu-id="03a7c-133">Sending messages toohello source topic only requires **Send** permissions on hello source topic.</span></span>

## <a name="next-steps"></a><span data-ttu-id="03a7c-134">다음 단계</span><span class="sxs-lookup"><span data-stu-id="03a7c-134">Next steps</span></span>

<span data-ttu-id="03a7c-135">자동 전달에 대 한 자세한 내용은 hello 다음 참조 항목을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="03a7c-135">For detailed information about auto-forwarding, see hello following reference topics:</span></span>

* <span data-ttu-id="03a7c-136">[ForwardTo][QueueDescription.ForwardTo]</span><span class="sxs-lookup"><span data-stu-id="03a7c-136">[ForwardTo][QueueDescription.ForwardTo]</span></span>
* <span data-ttu-id="03a7c-137">[QueueDescription][QueueDescription]</span><span class="sxs-lookup"><span data-stu-id="03a7c-137">[QueueDescription][QueueDescription]</span></span>
* <span data-ttu-id="03a7c-138">[SubscriptionDescription][SubscriptionDescription]</span><span class="sxs-lookup"><span data-stu-id="03a7c-138">[SubscriptionDescription][SubscriptionDescription]</span></span>

<span data-ttu-id="03a7c-139">서비스 버스 성능 향상에 대해 자세히 toolearn 참조</span><span class="sxs-lookup"><span data-stu-id="03a7c-139">toolearn more about Service Bus performance improvements, see</span></span> 

* [<span data-ttu-id="03a7c-140">Service Bus 메시징을 사용한 성능 향상의 모범 사례</span><span class="sxs-lookup"><span data-stu-id="03a7c-140">Best Practices for performance improvements using Service Bus Messaging</span></span>](service-bus-performance-improvements.md)
* <span data-ttu-id="03a7c-141">[분할된 메시징 엔터티][Partitioned messaging entities]</span><span class="sxs-lookup"><span data-stu-id="03a7c-141">[Partitioned messaging entities][Partitioned messaging entities].</span></span>

[QueueDescription.ForwardTo]: /dotnet/api/microsoft.servicebus.messaging.queuedescription.forwardto#Microsoft_ServiceBus_Messaging_QueueDescription_ForwardTo
[SubscriptionDescription.ForwardTo]: /dotnet/api/microsoft.servicebus.messaging.subscriptiondescription.forwardto#Microsoft_ServiceBus_Messaging_SubscriptionDescription_ForwardTo
[QueueDescription]: /dotnet/api/microsoft.servicebus.messaging.queuedescription
[SubscriptionDescription]: /dotnet/api/microsoft.servicebus.messaging.queuedescription
[0]: ./media/service-bus-auto-forwarding/IC628631.gif
[1]: ./media/service-bus-auto-forwarding/IC628632.gif
[Partitioned messaging entities]: service-bus-partitioning.md

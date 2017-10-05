---
title: "Service Bus 토픽을 사용하는 방법(Ruby) | Microsoft Docs"
description: "Azure에서 서비스 버스 토픽 및 구독을 사용하는 방법에 대해 알아봅니다. 코드 샘플은 Ruby 응용 프로그램용으로 작성되었습니다."
services: service-bus-messaging
documentationcenter: ruby
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 3ef2295e-7c5f-4c54-a13b-a69c8045d4b6
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 4a4c9949843b16ae6be2f516de4fd1e3f7415959
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-service-bus-topics-and-subscriptions-with-ruby"></a><span data-ttu-id="3da1d-104">Ruby에서 Service Bus 토픽 및 구독을 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="3da1d-104">How to use Service Bus topics and subscriptions with Ruby</span></span>
 
[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="3da1d-105">이 문서에서는 Ruby 응용 프로그램에서 Service Bus 토픽과 구독을 사용하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3da1d-105">This article describes how to use Service Bus topics and subscriptions from Ruby applications.</span></span> <span data-ttu-id="3da1d-106">여기서 다루는 시나리오에는 **토픽 및 구독 만들기, 구독 필터 만들기, 토픽에** 메시지 보내기, **구독에서 메시지 받기**, **토픽 및 구독 삭제** 등이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="3da1d-106">The scenarios covered include **creating topics and subscriptions, creating subscription filters, sending messages** to a topic, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span> <span data-ttu-id="3da1d-107">토픽 및 구독에 대한 자세한 내용은 [다음 단계](#next-steps) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3da1d-107">For more information on topics and subscriptions, see the [Next Steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

[!INCLUDE [service-bus-ruby-setup](../../includes/service-bus-ruby-setup.md)]

## <a name="create-a-topic"></a><span data-ttu-id="3da1d-108">토픽 만들기</span><span class="sxs-lookup"><span data-stu-id="3da1d-108">Create a topic</span></span>
<span data-ttu-id="3da1d-109">**Azure::ServiceBusService** 개체를 사용하면 토픽으로 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3da1d-109">The **Azure::ServiceBusService** object enables you to work with topics.</span></span> <span data-ttu-id="3da1d-110">다음 코드는 **Azure::ServiceBusService** 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3da1d-110">The following code creates an **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="3da1d-111">토픽을 만들려면 `create_topic()` 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3da1d-111">To create a topic, use the `create_topic()` method.</span></span> <span data-ttu-id="3da1d-112">다음 예제에서는 토픽을 만들거나 오류가 있는 경우 오류를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="3da1d-112">The following example creates a topic or prints out the errors if there are any.</span></span>

```ruby
azure_service_bus_service = Azure::ServiceBus::ServiceBusService.new(sb_host, { signer: signer})
begin
  topic = azure_service_bus_service.create_queue("test-topic")
rescue
  puts $!
end
```

<span data-ttu-id="3da1d-113">추가 옵션을 사용하여 **Azure::ServiceBus::Topic** 개체를 전달할 수도 있습니다. 그러면 메시지 TTL(Time to Live) 또는 최대 큐 크기와 같은 기본 토픽 설정을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3da1d-113">You can also pass an **Azure::ServiceBus::Topic** object with additional options, which enable you to override default topic settings such as message time to live or maximum queue size.</span></span> <span data-ttu-id="3da1d-114">다음 예제에서는 최대 큐 크기를 5GB로 설정하고 TTL(Time to Live)을 1분으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3da1d-114">The following example shows setting the maximum queue size to 5 GB and time to live to 1 minute:</span></span>

```ruby
topic = Azure::ServiceBus::Topic.new("test-topic")
topic.max_size_in_megabytes = 5120
topic.default_message_time_to_live = "PT1M"

topic = azure_service_bus_service.create_topic(topic)
```

## <a name="create-subscriptions"></a><span data-ttu-id="3da1d-115">구독 만들기</span><span class="sxs-lookup"><span data-stu-id="3da1d-115">Create subscriptions</span></span>
<span data-ttu-id="3da1d-116">토픽 구독은 **Azure::ServiceBusService** 개체로도 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3da1d-116">Topic subscriptions are also created with the **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="3da1d-117">구독에는 이름이 지정되며, 구독의 가상 큐에 전달되는 메시지 집합을 제한하는 선택적 필터가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3da1d-117">Subscriptions are named and can have an optional filter that restricts the set of messages delivered to the subscription's virtual queue.</span></span>

<span data-ttu-id="3da1d-118">구독은 영구적이며, 구독 자체 또는 구독과 연결된 토픽이 삭제될 때까지 계속 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="3da1d-118">Subscriptions are persistent and will continue to exist until either they, or the topic they are associated with, are deleted.</span></span> <span data-ttu-id="3da1d-119">응용 프로그램에 구독을 만들기 위한 논리가 포함된 경우, getSubscription 메서드를 사용하여 구독이 이미 존재하는지를 먼저 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3da1d-119">If your application contains logic to create a subscription, it should first check if the subscription already exists by using the getSubscription method.</span></span>

### <a name="create-a-subscription-with-the-default-matchall-filter"></a><span data-ttu-id="3da1d-120">기본(MatchAll) 필터를 사용하여 구독 만들기</span><span class="sxs-lookup"><span data-stu-id="3da1d-120">Create a subscription with the default (MatchAll) filter</span></span>
<span data-ttu-id="3da1d-121">**MatchAll** 필터는 새 구독을 만들 때 필터를 지정하지 않은 경우 사용되는 기본 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="3da1d-121">The **MatchAll** filter is the default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="3da1d-122">**MatchAll** 필터를 사용하면 토픽에 게시된 모든 메시지가 구독의 가상 큐에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="3da1d-122">When the **MatchAll** filter is used, all messages published to the topic are placed in the subscription's virtual queue.</span></span> <span data-ttu-id="3da1d-123">다음 예제에서는 "all-messages"라는 구독을 만들고 기본 **MatchAll** 필터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3da1d-123">The following example creates a subscription named "all-messages" and uses the default **MatchAll** filter.</span></span>

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "all-messages")
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="3da1d-124">필터를 사용하여 구독 만들기</span><span class="sxs-lookup"><span data-stu-id="3da1d-124">Create subscriptions with filters</span></span>
<span data-ttu-id="3da1d-125">토픽으로 전송된 메시지 중 특정 구독 내에 표시되어야 하는 메시지의 범위를 지정하는 필터를 정의할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3da1d-125">You can also define filters that enable you to specify which messages sent to a topic should show up within a specific subscription.</span></span>

<span data-ttu-id="3da1d-126">구독에서 지원하는 가장 유연한 유형의 필터는 SQL92 하위 집합을 구현하는 **Azure::ServiceBus::SqlFilter**입니다.</span><span class="sxs-lookup"><span data-stu-id="3da1d-126">The most flexible type of filter supported by subscriptions is the **Azure::ServiceBus::SqlFilter**, which implements a subset of SQL92.</span></span> <span data-ttu-id="3da1d-127">SQL 필터는 토픽에 게시된 메시지의 속성에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3da1d-127">SQL filters operate on the properties of the messages that are published to the topic.</span></span> <span data-ttu-id="3da1d-128">SQL 필터와 함께 사용할 수 있는 식에 대한 자세한 내용은 [SqlFilter](service-bus-messaging-sql-filter.md) 구문을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3da1d-128">For more details about the expressions that can be used with a SQL filter, review the [SqlFilter](service-bus-messaging-sql-filter.md) syntax.</span></span>

<span data-ttu-id="3da1d-129">**Azure::ServiceBusService** 개체의 `create_rule()` 메서드를 사용하여 구독에 필터를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3da1d-129">You can add filters to a subscription by using the `create_rule()` method of the **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="3da1d-130">이 메서드를 사용하면 기존 구독에 새 필터를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3da1d-130">This method enables you to add new filters to an existing subscription.</span></span>

<span data-ttu-id="3da1d-131">기본 필터는 모든 새로운 구독에 자동으로 적용되므로 먼저 기본 필터를 제거해야 합니다. 그렇지 않으면 **MatchAll**이 사용자가 지정하는 기타 필터를 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="3da1d-131">Since the default filter is applied automatically to all new subscriptions, you must first remove the default filter, or the **MatchAll** will override any other filters you may specify.</span></span> <span data-ttu-id="3da1d-132">**Azure::ServiceBusService** 개체의 `delete_rule()` 메서드를 사용하여 기본 규칙을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3da1d-132">You can remove the default rule by using the `delete_rule()` method on the **Azure::ServiceBusService** object.</span></span>

<span data-ttu-id="3da1d-133">다음 예제에서는 사용자 지정 `message_number` 속성이 3보다 큰 메시지만 선택하는 **Azure::ServiceBus::SqlFilter**를 사용하여 "high-messages"라는 구독을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3da1d-133">The following example creates a subscription named "high-messages" with an **Azure::ServiceBus::SqlFilter** that only selects messages that have a custom `message_number` property greater than 3:</span></span>

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "high-messages")
azure_service_bus_service.delete_rule("test-topic", "high-messages", "$Default")

rule = Azure::ServiceBus::Rule.new("high-messages-rule")
rule.topic = "test-topic"
rule.subscription = "high-messages"
rule.filter = Azure::ServiceBus::SqlFilter.new({
  :sql_expression => "message_number > 3" })
rule = azure_service_bus_service.create_rule(rule)
```

<span data-ttu-id="3da1d-134">마찬가지로, 다음 예제에서는 `message_number` 속성이 3보다 작거나 같은 메시지만 선택하는 **Azure::ServiceBus::SqlFilter**를 사용하여 `low-messages`라는 구독을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3da1d-134">Similarly, the following example creates a subscription named `low-messages` with an **Azure::ServiceBus::SqlFilter** that only selects messages that have a `message_number` property less than or equal to 3:</span></span>

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "low-messages")
azure_service_bus_service.delete_rule("test-topic", "low-messages", "$Default")

rule = Azure::ServiceBus::Rule.new("low-messages-rule")
rule.topic = "test-topic"
rule.subscription = "low-messages"
rule.filter = Azure::ServiceBus::SqlFilter.new({
  :sql_expression => "message_number <= 3" })
rule = azure_service_bus_service.create_rule(rule)
```

<span data-ttu-id="3da1d-135">이제 `test-topic`으로 메시지를 보내는 경우 `all-messages` 토픽 구독을 구독하는 수신자에게는 항상 배달되고, `high-messages` 및 `low-messages` 토픽 구독을 구독하는 수신자에게는 메시지 내용에 따라 선택적으로 배달됩니다.</span><span class="sxs-lookup"><span data-stu-id="3da1d-135">When a message is now sent to `test-topic`, it is always be delivered to receivers subscribed to the `all-messages` topic subscription, and selectively delivered to receivers subscribed to the `high-messages` and `low-messages` topic subscriptions (depending upon the message content).</span></span>

## <a name="send-messages-to-a-topic"></a><span data-ttu-id="3da1d-136">토픽에 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="3da1d-136">Send messages to a topic</span></span>
<span data-ttu-id="3da1d-137">Service Bus 토픽에 메시지를 보내려면 응용 프로그램에서 **Azure::ServiceBusService** 개체의 `send_topic_message()` 메서드를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3da1d-137">To send a message to a Service Bus topic, your application must use the `send_topic_message()` method on the **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="3da1d-138">Service Bus 토픽으로 전송되는 메시지는 **Azure::ServiceBus::BrokeredMessage** 개체의 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="3da1d-138">Messages sent to Service Bus topics are instances of the **Azure::ServiceBus::BrokeredMessage** objects.</span></span> <span data-ttu-id="3da1d-139">**Azure::ServiceBus::BrokeredMessage** 개체에는 표준 속성 집합(예: `label` 및 `time_to_live`), 응용 프로그램별 사용자 지정 속성을 저장하는 데 사용되는 사전 및 문자열 데이터의 본문이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3da1d-139">**Azure::ServiceBus::BrokeredMessage** objects have a set of standard properties (such as `label` and `time_to_live`), a dictionary that is used to hold custom application-specific properties, and a body of string data.</span></span> <span data-ttu-id="3da1d-140">응용 프로그램은 문자열 값을 `send_topic_message()` 메서드에 전달하여 메시지의 본문을 설정할 수 있습니다. 그러면 필수 표준 속성이 기본값으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="3da1d-140">An application can set the body of the message by passing a string value to the `send_topic_message()` method and any required standard properties will be populated by default values.</span></span>

<span data-ttu-id="3da1d-141">다음 예제에서는 5개의 테스트 메시지를 `test-topic`에 보내는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3da1d-141">The following example demonstrates how to send five test messages to `test-topic`.</span></span> <span data-ttu-id="3da1d-142">루프가 반복될 때마다 각 메시지의 `message_number` 사용자 지정 속성 값이 달라지는 것을 알 수 있습니다(메시지를 수신하는 구독 결정).</span><span class="sxs-lookup"><span data-stu-id="3da1d-142">Note that the `message_number` custom property value of each message varies on the iteration of the loop (this determines which subscription receives it):</span></span>

```ruby
5.times do |i|
  message = Azure::ServiceBus::BrokeredMessage.new("test message " + i,
    { :message_number => i })
  azure_service_bus_service.send_topic_message("test-topic", message)
end
```

<span data-ttu-id="3da1d-143">Service Bus 토픽은 [표준 계층](service-bus-premium-messaging.md)에서 256KB의 최대 메시지 크기를 [프리미엄 계층](service-bus-premium-messaging.md)에서 1MB를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3da1d-143">Service Bus topics support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="3da1d-144">표준 및 사용자 지정 응용 프로그램 속성이 포함된 헤더의 최대 크기는 64KB입니다.</span><span class="sxs-lookup"><span data-stu-id="3da1d-144">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="3da1d-145">한 토픽에 저장되는 메시지 수에는 제한이 없지만 한 토픽에 저장되는 총 메시지 크기는 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="3da1d-145">There is no limit on the number of messages held in a topic but there is a cap on the total size of the messages held by a topic.</span></span> <span data-ttu-id="3da1d-146">이 토픽 크기는 생성 시 정의되며 상한이 5GB입니다.</span><span class="sxs-lookup"><span data-stu-id="3da1d-146">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="3da1d-147">구독에서 메시지 받기</span><span class="sxs-lookup"><span data-stu-id="3da1d-147">Receive messages from a subscription</span></span>
<span data-ttu-id="3da1d-148">**Azure::ServiceBusService** 개체의 `receive_subscription_message()` 메서드를 사용하여 구독에서 메시지를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="3da1d-148">Messages are received from a subscription using the `receive_subscription_message()` method on the **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="3da1d-149">기본적으로 메시지는 구독에서 삭제하지 않고 읽고(피크) 잠급니다.</span><span class="sxs-lookup"><span data-stu-id="3da1d-149">By default, messages are read(peak) and locked without deleting it from the subscription.</span></span> <span data-ttu-id="3da1d-150">`peek_lock` 옵션을 **false**로 설정하여 메시지를 구독에서 읽고 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3da1d-150">You can read and delete the message from the subscription by setting the `peek_lock` option to **false**.</span></span>

<span data-ttu-id="3da1d-151">기본 동작은 읽기 및 삭제가 2단계 작업으로 수행되도록 하므로 메시지 누락이 허용되지 않는 응용 프로그램도 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3da1d-151">The default behavior makes the reading and deleting a two-stage operation, which also makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="3da1d-152">서비스 버스는 요청을 받으면 소비할 다음 메시지를 찾아서 다른 소비자가 수신할 수 없도록 잠근 후 응용 프로그램에 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="3da1d-152">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span> <span data-ttu-id="3da1d-153">응용 프로그램은 메시지 처리를 완료하거나 추가 처리를 위해 안전하게 저장한 후, `delete_subscription_message()` 메서드를 호출하고 삭제될 메시지를 매개 변수로 제공하여 수신 프로세스의 두 번째 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="3da1d-153">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling `delete_subscription_message()` method and providing the message to be deleted as a parameter.</span></span> <span data-ttu-id="3da1d-154">`delete_subscription_message()` 메서드는 메시지를 소비 중인 것으로 표시하고 구독에서 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="3da1d-154">The `delete_subscription_message()` method will mark the message as being consumed and remove it from the subscription.</span></span>

<span data-ttu-id="3da1d-155">`:peek_lock` 매개 변수를 **false**로 설정하면 메시지 읽기 및 삭제가 가장 간단한 모델이 되며, 오류 발생 시 메시지를 처리하지 않는 것을 허용하는 응용 프로그램의 시나리오에 가장 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="3da1d-155">If the `:peek_lock` parameter is set to **false**, reading and deleting the message becomes the simplest model, and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="3da1d-156">이해를 돕기 위해 소비자가 수신 요청을 실행한 후 처리하기 전에 크래시되는 시나리오를 고려해 보세요.</span><span class="sxs-lookup"><span data-stu-id="3da1d-156">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="3da1d-157">서비스 버스는 메시지를 이용되는 것으로 표시하기 때문에 응용 프로그램이 다시 시작되고 메시지 소비를 다시 시작할 경우 크래시 전에 소비된 메시지가 누락됩니다.</span><span class="sxs-lookup"><span data-stu-id="3da1d-157">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="3da1d-158">다음 예제에서는 `receive_subscription_message()`를 사용하여 메시지를 받고 처리하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="3da1d-158">The following example demonstrates how messages can be received and processed using `receive_subscription_message()`.</span></span> <span data-ttu-id="3da1d-159">이 예제에서는 먼저 **false**로 설정된 `:peek_lock`을 사용하여 `low-messages` 구독에서 메시지를 받고 삭제한 후 `high-messages`에서 다른 메시지를 받고 `delete_subscription_message()`를 사용하여 메시지를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="3da1d-159">The example first receives and deletes a message from the `low-messages` subscription by using `:peek_lock` set to **false**, then it receives another message from the `high-messages` and then deletes the message using `delete_subscription_message()`:</span></span>

```ruby
message = azure_service_bus_service.receive_subscription_message(
  "test-topic", "low-messages", { :peek_lock => false })
message = azure_service_bus_service.receive_subscription_message(
  "test-topic", "high-messages")
azure_service_bus_service.delete_subscription_message(message)
```

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="3da1d-160">응용 프로그램 작동 중단 및 읽을 수 없는 메시지를 처리하는 방법</span><span class="sxs-lookup"><span data-stu-id="3da1d-160">How to handle application crashes and unreadable messages</span></span>
<span data-ttu-id="3da1d-161">서비스 버스는 응용 프로그램 오류나 메시지 처리 문제를 정상적으로 복구하는 데 유용한 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3da1d-161">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="3da1d-162">어떤 이유로든 수신 응용 프로그램이 메시지를 처리할 수 없는 경우 **Azure::ServiceBusService** 개체의 `unlock_subscription_message()` 메서드를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3da1d-162">If a receiver application is unable to process the message for some reason, then it can call the `unlock_subscription_message()` method on the **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="3da1d-163">그러면 Service Bus에서 구독 내 메시지의 잠금을 해제하고 동일한 소비 응용 프로그램이나 다른 소비 응용 프로그램에서 메시지를 다시 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3da1d-163">This causes Service Bus to unlock the message within the subscription and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="3da1d-164">구독 내에서 잠긴 메시지와 연결된 제한 시간도 있으며, 응용 프로그램에서 잠금 제한 시간이 만료되기 전에 메시지를 처리하지 못하는 경우(예: 응용 프로그램이 크래시되는 경우) Service Bus가 메시지를 자동으로 잠금 해제하여 다시 받을 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="3da1d-164">There is also a timeout associated with a message locked within the subscription, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus will unlock the message automatically and make it available to be received again.</span></span>

<span data-ttu-id="3da1d-165">응용 프로그램이 메시지를 처리한 후 `delete_subscription_message()` 메서드가 호출되기 전에 충돌하는 경우, 다시 시작될 때 메시지가 응용 프로그램에 다시 배달됩니다.</span><span class="sxs-lookup"><span data-stu-id="3da1d-165">In the event that the application crashes after processing the message but before the `delete_subscription_message()` method is called, then the message is redelivered to the application when it restarts.</span></span> <span data-ttu-id="3da1d-166">이를 *최소 한 번 이상 처리*라고 합니다. 즉, 각 메시지가 최소 한 번 이상 처리되지만 특정 상황에서는 동일한 메시지가 다시 배달될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3da1d-166">This is often called *At Least Once Processing*; that is, each message will be processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="3da1d-167">중복 처리가 허용되지 않는 시나리오에서는 응용 프로그램 개발자가 중복 메시지 배달을 처리하는 논리를 응용 프로그램에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3da1d-167">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span></span> <span data-ttu-id="3da1d-168">이 경우 대체로 배달 시도 간에 일정하게 유지되는 메시지의 `message_id` 속성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3da1d-168">This logic is often achieved using the `message_id` property of the message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="3da1d-169">토픽 및 구독 삭제</span><span class="sxs-lookup"><span data-stu-id="3da1d-169">Delete topics and subscriptions</span></span>
<span data-ttu-id="3da1d-170">토픽과 구독은 영구적이므로, [Azure Portal][Azure portal] 또는 프로그래밍 방식을 통해 명시적으로 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3da1d-170">Topics and subscriptions are persistent, and must be explicitly deleted either through the [Azure portal][Azure portal] or programmatically.</span></span> <span data-ttu-id="3da1d-171">아래 예제에서는 `test-topic`이라는 토픽을 삭제하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="3da1d-171">The example below demonstrates how to delete the topic named `test-topic`.</span></span>

```ruby
azure_service_bus_service.delete_topic("test-topic")
```

<span data-ttu-id="3da1d-172">토픽을 삭제하면 토픽에 등록된 모든 구독도 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="3da1d-172">Deleting a topic also deletes any subscriptions that are registered with the topic.</span></span> <span data-ttu-id="3da1d-173">구독을 개별적으로 삭제할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3da1d-173">Subscriptions can also be deleted independently.</span></span> <span data-ttu-id="3da1d-174">다음 코드는 이름이 `high-messages`인 구독을 `test-topic` 토픽에서 삭제하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="3da1d-174">The following code demonstrates how to delete the subscription named `high-messages` from the `test-topic` topic:</span></span>

```ruby
azure_service_bus_service.delete_subscription("test-topic", "high-messages")
```

## <a name="next-steps"></a><span data-ttu-id="3da1d-175">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3da1d-175">Next steps</span></span>
<span data-ttu-id="3da1d-176">이제 서비스 버스 토픽의 기본 사항을 익혔으므로 다음 링크를 따라 이동하여 자세한 내용을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3da1d-176">Now that you've learned the basics of Service Bus topics, follow these links to learn more.</span></span>

* <span data-ttu-id="3da1d-177">[큐, 토픽 및 구독](service-bus-queues-topics-subscriptions.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3da1d-177">See [Queues, topics, and subscriptions](service-bus-queues-topics-subscriptions.md).</span></span>
* <span data-ttu-id="3da1d-178">[SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter)에 대한 API 참조.</span><span class="sxs-lookup"><span data-stu-id="3da1d-178">API reference for [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter).</span></span>
* <span data-ttu-id="3da1d-179">GitHub에서 [Azure SDK for Ruby](https://github.com/Azure/azure-sdk-for-ruby) 리포지토리를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="3da1d-179">Visit the [Azure SDK for Ruby](https://github.com/Azure/azure-sdk-for-ruby) repository on GitHub.</span></span>

[Azure portal]: https://portal.azure.com

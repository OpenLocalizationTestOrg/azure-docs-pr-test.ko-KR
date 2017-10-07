---
title: "aaaHow toouse 서비스 버스 주제 (Ruby) | Microsoft Docs"
description: "자세한 방법을 toouse 서비스 버스 항목 및 Azure에서 구독 합니다. 코드 샘플은 Ruby 응용 프로그램용으로 작성되었습니다."
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
ms.openlocfilehash: 236d6495825e68e336c23e1b500d0764ee512e49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-ruby"></a><span data-ttu-id="19fb9-104">어떻게 toouse 서비스 버스 토픽 및 구독 Ruby</span><span class="sxs-lookup"><span data-stu-id="19fb9-104">How toouse Service Bus topics and subscriptions with Ruby</span></span>
 
[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="19fb9-105">이 문서에서는 설명 방법을 toouse 서비스 버스 항목 및 Ruby 응용 프로그램에서 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="19fb9-105">This article describes how toouse Service Bus topics and subscriptions from Ruby applications.</span></span> <span data-ttu-id="19fb9-106">hello 가이드에서 다루는 시나리오 포함 **항목 및 구독 필터를 메시지를 보내는 구독을 만드는** tooa 항목 **구독에서 메시지를 받는**, 및  **항목 및 구독을 삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="19fb9-106">hello scenarios covered include **creating topics and subscriptions, creating subscription filters, sending messages** tooa topic, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span> <span data-ttu-id="19fb9-107">항목 및 구독에 대 한 자세한 내용은 참조 hello [다음 단계](#next-steps) 섹션.</span><span class="sxs-lookup"><span data-stu-id="19fb9-107">For more information on topics and subscriptions, see hello [Next Steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

[!INCLUDE [service-bus-ruby-setup](../../includes/service-bus-ruby-setup.md)]

## <a name="create-a-topic"></a><span data-ttu-id="19fb9-108">토픽 만들기</span><span class="sxs-lookup"><span data-stu-id="19fb9-108">Create a topic</span></span>
<span data-ttu-id="19fb9-109">hello **Azure::ServiceBusService** 개체를 사용 하면 toowork 항목과 함께 합니다.</span><span class="sxs-lookup"><span data-stu-id="19fb9-109">hello **Azure::ServiceBusService** object enables you toowork with topics.</span></span> <span data-ttu-id="19fb9-110">hello 다음 코드에서는 **Azure::ServiceBusService** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="19fb9-110">hello following code creates an **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="19fb9-111">toocreate 항목을 사용 하 여 hello `create_topic()` 메서드.</span><span class="sxs-lookup"><span data-stu-id="19fb9-111">toocreate a topic, use hello `create_topic()` method.</span></span> <span data-ttu-id="19fb9-112">다음 예제는 hello 항목을 만들거나 hello 오류가 있는 경우 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="19fb9-112">hello following example creates a topic or prints out hello errors if there are any.</span></span>

```ruby
azure_service_bus_service = Azure::ServiceBus::ServiceBusService.new(sb_host, { signer: signer})
begin
  topic = azure_service_bus_service.create_queue("test-topic")
rescue
  puts $!
end
```

<span data-ttu-id="19fb9-113">전달할 수도 있습니다는 **Azure::ServiceBus::Topic** 메시지 시간 toolive 또는 최대 큐 크기와 같은 toooverride 기본 항목 설정을 사용할 수 있는 추가 옵션이 포함 된 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="19fb9-113">You can also pass an **Azure::ServiceBus::Topic** object with additional options, which enable you toooverride default topic settings such as message time toolive or maximum queue size.</span></span> <span data-ttu-id="19fb9-114">hello hello 최대 큐를 설정 하는 다음 예제와 size too5 GB 및 toolive too1 분 시간:</span><span class="sxs-lookup"><span data-stu-id="19fb9-114">hello following example shows setting hello maximum queue size too5 GB and time toolive too1 minute:</span></span>

```ruby
topic = Azure::ServiceBus::Topic.new("test-topic")
topic.max_size_in_megabytes = 5120
topic.default_message_time_to_live = "PT1M"

topic = azure_service_bus_service.create_topic(topic)
```

## <a name="create-subscriptions"></a><span data-ttu-id="19fb9-115">구독 만들기</span><span class="sxs-lookup"><span data-stu-id="19fb9-115">Create subscriptions</span></span>
<span data-ttu-id="19fb9-116">주제 구독에도 hello를 사용 하 여 만들어진 **Azure::ServiceBusService** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="19fb9-116">Topic subscriptions are also created with hello **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="19fb9-117">이름이 지정 된 구독과 hello toohello 구독의 가상 큐에 배달 된 메시지 집합을 제한 하는 선택적 필터가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19fb9-117">Subscriptions are named and can have an optional filter that restricts hello set of messages delivered toohello subscription's virtual queue.</span></span>

<span data-ttu-id="19fb9-118">구독 영구 tooexist 중 하나가 될 때까지 계속 사용 되며 또는 hello이 항목은 연관 된, 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="19fb9-118">Subscriptions are persistent and will continue tooexist until either they, or hello topic they are associated with, are deleted.</span></span> <span data-ttu-id="19fb9-119">응용 프로그램 논리 toocreate 구독 있으면 hello getSubscription 메서드를 사용 하 여 hello 구독에 이미 존재 하는 경우 확인 먼저 합니다.</span><span class="sxs-lookup"><span data-stu-id="19fb9-119">If your application contains logic toocreate a subscription, it should first check if hello subscription already exists by using hello getSubscription method.</span></span>

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a><span data-ttu-id="19fb9-120">Hello 기본 (MatchAll) 필터와 구독 만들기</span><span class="sxs-lookup"><span data-stu-id="19fb9-120">Create a subscription with hello default (MatchAll) filter</span></span>
<span data-ttu-id="19fb9-121">hello **MatchAll** 필터는 필터 지정 하지 않으면은 새 구독을 만들 때 사용 되는 hello 기본 필터.</span><span class="sxs-lookup"><span data-stu-id="19fb9-121">hello **MatchAll** filter is hello default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="19fb9-122">Hello 때 **MatchAll** 필터 사용 하는 경우 모든 부분 메시지 게시 된 toohello hello 구독의 가상 큐에 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="19fb9-122">When hello **MatchAll** filter is used, all messages published toohello topic are placed in hello subscription's virtual queue.</span></span> <span data-ttu-id="19fb9-123">hello 다음 예제에서는 "전체 메시지" 이라는 구독을 만들고 사용 하 여 기본 hello **MatchAll** 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="19fb9-123">hello following example creates a subscription named "all-messages" and uses hello default **MatchAll** filter.</span></span>

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "all-messages")
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="19fb9-124">필터를 사용하여 구독 만들기</span><span class="sxs-lookup"><span data-stu-id="19fb9-124">Create subscriptions with filters</span></span>
<span data-ttu-id="19fb9-125">Toospecify tooa 항목에 특정 구독 내에서 표시 됩니다. 보낸 메시지 수 있도록 하는 필터를 정의할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19fb9-125">You can also define filters that enable you toospecify which messages sent tooa topic should show up within a specific subscription.</span></span>

<span data-ttu-id="19fb9-126">hello 가장 유연한 구독에서 지 원하는 필터 형식은 hello **Azure::ServiceBus::SqlFilter**를 구현 하는 SQL92의 하위 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="19fb9-126">hello most flexible type of filter supported by subscriptions is hello **Azure::ServiceBus::SqlFilter**, which implements a subset of SQL92.</span></span> <span data-ttu-id="19fb9-127">SQL 필터가 있는 게시 된 toohello 항목 hello 메시지의 hello 속성에서 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="19fb9-127">SQL filters operate on hello properties of hello messages that are published toohello topic.</span></span> <span data-ttu-id="19fb9-128">SQL 필터와 함께 사용할 수 있는 hello 식에 대 한 자세한 내용은 hello 검토 [SqlFilter](service-bus-messaging-sql-filter.md) 구문입니다.</span><span class="sxs-lookup"><span data-stu-id="19fb9-128">For more details about hello expressions that can be used with a SQL filter, review hello [SqlFilter](service-bus-messaging-sql-filter.md) syntax.</span></span>

<span data-ttu-id="19fb9-129">Hello를 사용 하 여 필터 tooa 구독을 추가 하려면 `create_rule()` hello 방식의 **Azure::ServiceBusService** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="19fb9-129">You can add filters tooa subscription by using hello `create_rule()` method of hello **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="19fb9-130">이 방법을 사용 하면 tooadd 새 필터 tooan 기존 구독이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19fb9-130">This method enables you tooadd new filters tooan existing subscription.</span></span>

<span data-ttu-id="19fb9-131">Hello 기본 필터는 자동으로 적용 한 이후 tooall 새 구독을 먼저 hello 기본 필터를 제거 하거나 hello **MatchAll** 지정할 수 있는 필터를 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="19fb9-131">Since hello default filter is applied automatically tooall new subscriptions, you must first remove hello default filter, or hello **MatchAll** will override any other filters you may specify.</span></span> <span data-ttu-id="19fb9-132">Hello를 사용 하 여 hello 기본 규칙을 제거할 수 있습니다 `delete_rule()` 메서드 hello **Azure::ServiceBusService** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="19fb9-132">You can remove hello default rule by using hello `delete_rule()` method on hello **Azure::ServiceBusService** object.</span></span>

<span data-ttu-id="19fb9-133">hello 다음 예제에서는 구독을 만드는 "높은 메시지" 이라는 **Azure::ServiceBus::SqlFilter** 만 사용자 지정 하는 메시지를 선택 하는 `message_number` 3 보다 큰 속성:</span><span class="sxs-lookup"><span data-stu-id="19fb9-133">hello following example creates a subscription named "high-messages" with an **Azure::ServiceBus::SqlFilter** that only selects messages that have a custom `message_number` property greater than 3:</span></span>

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

<span data-ttu-id="19fb9-134">마찬가지로, hello 다음 예제에서는 구독을 만드는 라는 `low-messages` 와 **Azure::ServiceBus::SqlFilter** 만 설정 된 메시지를 선택 하는 `message_number` 속성 작은 보다 짧거나 too3:</span><span class="sxs-lookup"><span data-stu-id="19fb9-134">Similarly, hello following example creates a subscription named `low-messages` with an **Azure::ServiceBus::SqlFilter** that only selects messages that have a `message_number` property less than or equal too3:</span></span>

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

<span data-ttu-id="19fb9-135">메시지는 이제 보내면 너무`test-topic`, 구독 배달된 tooreceivers toohello 항상 수는 `all-messages` 항목 구독 및 구독 하는 선택적으로 배달 된 tooreceivers toohello `high-messages` 및 `low-messages` 항목 구독 ( 에 따라 hello 메시지 내용을).</span><span class="sxs-lookup"><span data-stu-id="19fb9-135">When a message is now sent too`test-topic`, it is always be delivered tooreceivers subscribed toohello `all-messages` topic subscription, and selectively delivered tooreceivers subscribed toohello `high-messages` and `low-messages` topic subscriptions (depending upon hello message content).</span></span>

## <a name="send-messages-tooa-topic"></a><span data-ttu-id="19fb9-136">Tooa 부분 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="19fb9-136">Send messages tooa topic</span></span>
<span data-ttu-id="19fb9-137">메시지 tooa 서비스 버스 항목 toosend 응용 프로그램 hello를 사용 해야 `send_topic_message()` 메서드 hello **Azure::ServiceBusService** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="19fb9-137">toosend a message tooa Service Bus topic, your application must use hello `send_topic_message()` method on hello **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="19fb9-138">메시지가 전송 tooService 버스 주제는 hello 인스턴스의 **Azure::ServiceBus::BrokeredMessage** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="19fb9-138">Messages sent tooService Bus topics are instances of hello **Azure::ServiceBus::BrokeredMessage** objects.</span></span> <span data-ttu-id="19fb9-139">**Azure::ServiceBus::BrokeredMessage** 개체에는 표준 속성 집합이 있습니다 (같은 `label` 및 `time_to_live`), 사용자 지정 응용 프로그램 특정 속성 사용 되는 toohold 있는 사전 및 문자열 데이터의 본문입니다.</span><span class="sxs-lookup"><span data-stu-id="19fb9-139">**Azure::ServiceBus::BrokeredMessage** objects have a set of standard properties (such as `label` and `time_to_live`), a dictionary that is used toohold custom application-specific properties, and a body of string data.</span></span> <span data-ttu-id="19fb9-140">응용 프로그램 문자열 값 toohello 전달 하 여 hello hello 메시지 본문을 설정할 수 `send_topic_message()` 메서드 및 필수 표준 속성 기본 값으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="19fb9-140">An application can set hello body of hello message by passing a string value toohello `send_topic_message()` method and any required standard properties will be populated by default values.</span></span>

<span data-ttu-id="19fb9-141">hello 다음 예제에서는 5 toosend 테스트 너무 메시지 방법을`test-topic`합니다.</span><span class="sxs-lookup"><span data-stu-id="19fb9-141">hello following example demonstrates how toosend five test messages too`test-topic`.</span></span> <span data-ttu-id="19fb9-142">해당 hello 참고 `message_number` hello 루프의 반복 hello에 각 메시지의 사용자 지정 속성 값 달라 집니다 (결정 구독 수신):</span><span class="sxs-lookup"><span data-stu-id="19fb9-142">Note that hello `message_number` custom property value of each message varies on hello iteration of hello loop (this determines which subscription receives it):</span></span>

```ruby
5.times do |i|
  message = Azure::ServiceBus::BrokeredMessage.new("test message " + i,
    { :message_number => i })
  azure_service_bus_service.send_topic_message("test-topic", message)
end
```

<span data-ttu-id="19fb9-143">서비스 버스 주제 hello에서 최대 메시지 크기는 256KB 지원 [표준 계층](service-bus-premium-messaging.md) 및 hello에서 1 MB [Premium 계층](service-bus-premium-messaging.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="19fb9-143">Service Bus topics support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="19fb9-144">hello 표준 및 사용자 지정 응용 프로그램 속성을 포함 하는 hello 헤더는 64KB의 최대 크기를 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19fb9-144">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="19fb9-145">Hello 메시지에 항목을 보유할 수에 제한이 없음을 않으며 항목을 보유 하는 hello 메시지의 총 크기 hello 켜져 캡입니다.</span><span class="sxs-lookup"><span data-stu-id="19fb9-145">There is no limit on hello number of messages held in a topic but there is a cap on hello total size of hello messages held by a topic.</span></span> <span data-ttu-id="19fb9-146">이 토픽 크기는 생성 시 정의되며 상한이 5GB입니다.</span><span class="sxs-lookup"><span data-stu-id="19fb9-146">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="19fb9-147">구독에서 메시지 받기</span><span class="sxs-lookup"><span data-stu-id="19fb9-147">Receive messages from a subscription</span></span>
<span data-ttu-id="19fb9-148">Hello를 사용 하 여 구독에서 메시지를 받을 `receive_subscription_message()` 메서드 hello **Azure::ServiceBusService** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="19fb9-148">Messages are received from a subscription using hello `receive_subscription_message()` method on hello **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="19fb9-149">기본적으로 메시지 read(peak) 되며 hello 구독에서 삭제 하지 않고 잠겨 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19fb9-149">By default, messages are read(peak) and locked without deleting it from hello subscription.</span></span> <span data-ttu-id="19fb9-150">읽을 수 있으며 hello 설정 하 여 hello 메시지 hello 구독에서 삭제 `peek_lock` 옵션**false**합니다.</span><span class="sxs-lookup"><span data-stu-id="19fb9-150">You can read and delete hello message from hello subscription by setting hello `peek_lock` option too**false**.</span></span>

<span data-ttu-id="19fb9-151">hello 기본 동작을 사용 하면 hello 읽기 및 삭제는 2 단계 작업을 사용 하면 누락 된 메시지를 허용할 수 없는 가능한 toosupport 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="19fb9-151">hello default behavior makes hello reading and deleting a two-stage operation, which also makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="19fb9-152">서비스 버스 요청을 받으면 다음 메시지 toobe hello 사용 다른 소비자가 수신할 tooprevent 잠근 하 고 toohello 응용 프로그램 반환 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="19fb9-152">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="19fb9-153">Hello hello의 두 번째 단계를 완료 hello 응용 프로그램 hello 메시지 처리를 완료 (또는 이후 처리를 위해 안정적으로 저장) 한 후 호출 하 여 수신 프로세스 `delete_subscription_message()` 메서드와 hello 메시지 toobe 삭제 매개 변수로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="19fb9-153">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling `delete_subscription_message()` method and providing hello message toobe deleted as a parameter.</span></span> <span data-ttu-id="19fb9-154">hello `delete_subscription_message()` 메서드 hello 메시지를 사용 되 고 표시 하 고 hello 구독에서 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="19fb9-154">hello `delete_subscription_message()` method will mark hello message as being consumed and remove it from hello subscription.</span></span>

<span data-ttu-id="19fb9-155">경우 hello `:peek_lock` 매개 변수가 너무 설정 된**false**, 읽기 및 hello 가장 간단한 모델 hello 메시지를 삭제 되며 시나리오는 응용 프로그램의 hello 이벤트에서 메시지를 처리 하지 않아도 안전한 수에 가장 적합 한 오류가 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="19fb9-155">If hello `:peek_lock` parameter is set too**false**, reading and deleting hello message becomes hello simplest model, and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="19fb9-156">toounderstand hello는 hello 소비자 문제에 요청을 수신 하는 시나리오 및 후 처리 하기 전에 크래시 합니다.</span><span class="sxs-lookup"><span data-stu-id="19fb9-156">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="19fb9-157">서비스 버스 사용 되는 것을 다음 hello 응용 프로그램 다시 시작 되 고 메시지 사용을 시작할 때 hello 메시지를 표시 한 됩니다, 때문에 누락 됩니다 hello 메시지 했던 이전 toohello 크래시를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="19fb9-157">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="19fb9-158">hello 다음 예제에서는 메시지를 수신할 수 방법 및 처리를 사용 하 여 `receive_subscription_message()`합니다.</span><span class="sxs-lookup"><span data-stu-id="19fb9-158">hello following example demonstrates how messages can be received and processed using `receive_subscription_message()`.</span></span> <span data-ttu-id="19fb9-159">hello 예제에서 먼저 수신 하 고 hello에서 메시지를 삭제 `low-messages` 를 사용 하 여 구독 `:peek_lock` 도**false**, hello에서 다른 메시지를 받고 다음 `high-messages` 다음 삭제 hello 메시지를 사용 하 고 `delete_subscription_message()`:</span><span class="sxs-lookup"><span data-stu-id="19fb9-159">hello example first receives and deletes a message from hello `low-messages` subscription by using `:peek_lock` set too**false**, then it receives another message from hello `high-messages` and then deletes hello message using `delete_subscription_message()`:</span></span>

```ruby
message = azure_service_bus_service.receive_subscription_message(
  "test-topic", "low-messages", { :peek_lock => false })
message = azure_service_bus_service.receive_subscription_message(
  "test-topic", "high-messages")
azure_service_bus_service.delete_subscription_message(message)
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="19fb9-160">Toohandle 응용 프로그램이 크래시 되는 방법 및 읽을 수 없는 메시지</span><span class="sxs-lookup"><span data-stu-id="19fb9-160">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="19fb9-161">서비스 버스 기능 toohelp 정상적으로 응용 프로그램 또는 메시지를 처리 하는 데 문제가 오류 로부터 복구를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="19fb9-161">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="19fb9-162">수신기 응용 프로그램 수 없는 경우 몇 가지 이유로 tooprocess 환영 메시지가 다음 hello 호출할 수 있는 `unlock_subscription_message()` 메서드 hello **Azure::ServiceBusService** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="19fb9-162">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlock_subscription_message()` method on hello **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="19fb9-163">이 인해 서비스 버스 toounlock hello hello 구독 내에서 메시지와 수신, 다시 사용할 수 있는 toobe 확인 하거나으로 hello를 많이 사용 응용 프로그램 또는 다른 소비 응용 프로그램에서 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="19fb9-163">This causes Service Bus toounlock hello message within hello subscription and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="19fb9-164">또한 hello 구독 내에서 잠긴 메시지와 관련 된 제한 시간 집합과 hello 응용 프로그램 실패 하기 전에 hello 메시지 tooprocess hello 잠금 제한 시간이 만료 (예를 들어 hello 응용 프로그램이 충돌할 경우), 서비스 버스에서 hello 메시지를 잠금 해제 한 다음 자동으로 사용할 수 있는 toobe 수신 다시 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="19fb9-164">There is also a timeout associated with a message locked within hello subscription, and if hello application fails tooprocess hello message before hello lock timeout expires (for example, if hello application crashes), then Service Bus will unlock hello message automatically and make it available toobe received again.</span></span>

<span data-ttu-id="19fb9-165">Hello hello 응용 프로그램 이벤트 충돌 hello 메시지 처리 전후에 그러나 hello 전에 `delete_subscription_message()` 메서드는 다음 다시 시작할 때 hello 메시지는 다시 전달한 toohello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="19fb9-165">In hello event that hello application crashes after processing hello message but before hello `delete_subscription_message()` method is called, then hello message is redelivered toohello application when it restarts.</span></span> <span data-ttu-id="19fb9-166">이 이라고 하는데 *일단 처리 이상*; 즉, 각 메시지가 최소 한 번 처리 되지만 특정 상황 hello에 동일한 메시지를 다시 배달 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19fb9-166">This is often called *At Least Once Processing*; that is, each message will be processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="19fb9-167">Hello 시나리오 중복 처리가 허용 되지 않는, 응용 프로그램 개발자가 추가 논리 tootheir 응용 프로그램을 toohandle 중복 메시지 배달을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="19fb9-167">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="19fb9-168">이 논리 자주 사용 하 여 이루어집니다 hello `message_id` 배달 시도 간에 일정 남아 있는 hello 메시지의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="19fb9-168">This logic is often achieved using hello `message_id` property of hello message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="19fb9-169">토픽 및 구독 삭제</span><span class="sxs-lookup"><span data-stu-id="19fb9-169">Delete topics and subscriptions</span></span>
<span data-ttu-id="19fb9-170">항목과 구독은 영구적이 고 명시적으로 해야 hello 통해 삭제 [Azure 포털] [ Azure portal] 또는 프로그래밍 방식으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="19fb9-170">Topics and subscriptions are persistent, and must be explicitly deleted either through hello [Azure portal][Azure portal] or programmatically.</span></span> <span data-ttu-id="19fb9-171">hello 아래 예제 toodelete hello 항목 이름을 지정 하는 방법 `test-topic`합니다.</span><span class="sxs-lookup"><span data-stu-id="19fb9-171">hello example below demonstrates how toodelete hello topic named `test-topic`.</span></span>

```ruby
azure_service_bus_service.delete_topic("test-topic")
```

<span data-ttu-id="19fb9-172">항목을 삭제 하면 모든 구독에 등록 된 hello 항목을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="19fb9-172">Deleting a topic also deletes any subscriptions that are registered with hello topic.</span></span> <span data-ttu-id="19fb9-173">구독을 개별적으로 삭제할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19fb9-173">Subscriptions can also be deleted independently.</span></span> <span data-ttu-id="19fb9-174">hello 다음 코드에서는 toodelete hello 구독 이름을 지정 하는 방법 `high-messages` hello에서 `test-topic` 항목:</span><span class="sxs-lookup"><span data-stu-id="19fb9-174">hello following code demonstrates how toodelete hello subscription named `high-messages` from hello `test-topic` topic:</span></span>

```ruby
azure_service_bus_service.delete_subscription("test-topic", "high-messages")
```

## <a name="next-steps"></a><span data-ttu-id="19fb9-175">다음 단계</span><span class="sxs-lookup"><span data-stu-id="19fb9-175">Next steps</span></span>
<span data-ttu-id="19fb9-176">서비스 버스 항목의 hello 기본 사항 학습 한, 했으므로 이러한 링크 toolearn 자세한 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="19fb9-176">Now that you've learned hello basics of Service Bus topics, follow these links toolearn more.</span></span>

* <span data-ttu-id="19fb9-177">[큐, 토픽 및 구독](service-bus-queues-topics-subscriptions.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="19fb9-177">See [Queues, topics, and subscriptions](service-bus-queues-topics-subscriptions.md).</span></span>
* <span data-ttu-id="19fb9-178">[SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter)에 대한 API 참조.</span><span class="sxs-lookup"><span data-stu-id="19fb9-178">API reference for [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter).</span></span>
* <span data-ttu-id="19fb9-179">Hello 방문 [Ruby 용 Azure SDK](https://github.com/Azure/azure-sdk-for-ruby) GitHub의 리포지토리 합니다.</span><span class="sxs-lookup"><span data-stu-id="19fb9-179">Visit hello [Azure SDK for Ruby](https://github.com/Azure/azure-sdk-for-ruby) repository on GitHub.</span></span>

[Azure portal]: https://portal.azure.com

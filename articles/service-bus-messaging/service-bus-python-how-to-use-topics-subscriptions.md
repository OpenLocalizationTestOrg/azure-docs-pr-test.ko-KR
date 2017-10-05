---
title: "Python과 함께 Azure Service Bus 토픽을 사용하는 방법 | Microsoft Docs"
description: "Python에서 Azure Service Bus 토픽 및 구독을 사용하는 방법에 대해 알아봅니다."
services: service-bus-messaging
documentationcenter: python
author: sethmanheim
manager: timlt
editor: 
ms.assetid: c4f1d76c-7567-4b33-9193-3788f82934e4
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 15269f9728e9dc45e6436e53b1859f76d4a7a0c9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-service-bus-topics-and-subscriptions-with-python"></a><span data-ttu-id="9056f-103">Python에서 Service Bus 토픽 및 구독을 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="9056f-103">How to use Service Bus topics and subscriptions with Python</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="9056f-104">이 문서에서는 Service Bus 토픽과 구독을 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9056f-104">This article describes how to use Service Bus topics and subscriptions.</span></span> <span data-ttu-id="9056f-105">샘플은 Python으로 작성되었으며 [Azure Python SDK 패키지][Azure Python package]를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9056f-105">The samples are written in Python and use the [Azure Python SDK package][Azure Python package].</span></span> <span data-ttu-id="9056f-106">여기서 다루는 시나리오에는 **토픽 및 구독 만들기**, **구독 필터 만들기**, **토픽에 메시지 보내기**, **구독에서 메시지 받기**, **토픽 및 구독 삭제** 등이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="9056f-106">The scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages to a topic**, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span> <span data-ttu-id="9056f-107">토픽 및 구독에 대한 자세한 내용은 [다음 단계](#next-steps) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9056f-107">For more information about topics and subscriptions, see the [Next Steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

> [!NOTE] 
> <span data-ttu-id="9056f-108">Python 또는 [Azure Python 패키지][Azure Python package]를 설치해야 하는 경우 [Python 설치 가이드](../python-how-to-install.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9056f-108">If you need to install Python or the [Azure Python package][Azure Python package], see the [Python Installation Guide](../python-how-to-install.md).</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="9056f-109">주제 만들기</span><span class="sxs-lookup"><span data-stu-id="9056f-109">Create a topic</span></span>
<span data-ttu-id="9056f-110">**ServiceBusService** 개체를 사용하면 토픽으로 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9056f-110">The **ServiceBusService** object enables you to work with topics.</span></span> <span data-ttu-id="9056f-111">프로그래밍 방식으로 서비스 버스에 액세스하려는 Python 파일의 맨 위쪽에 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9056f-111">Add the following near the top of any Python file in which you wish to programmatically access Service Bus:</span></span>

```python
from azure.servicebus import ServiceBusService, Message, Topic, Rule, DEFAULT_RULE_NAME
```

<span data-ttu-id="9056f-112">다음 코드는 **ServiceBusService** 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9056f-112">The following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="9056f-113">`mynamespace`, `sharedaccesskeyname` 및 `sharedaccesskey`를 실제 네임스페이스, SAS(공유 액세스 서명) 키 이름 및 키 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9056f-113">Replace `mynamespace`, `sharedaccesskeyname`, and `sharedaccesskey` with your actual namespace, Shared Access Signature (SAS) key name, and key value.</span></span>

```python
bus_service = ServiceBusService(
    service_namespace='mynamespace',
    shared_access_key_name='sharedaccesskeyname',
    shared_access_key_value='sharedaccesskey')
```

<span data-ttu-id="9056f-114">[Azure Portal][Azure portal]에서 SAS 키 이름 값 및 키 값을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9056f-114">You can obtain the values for the SAS key name and value from the [Azure portal][Azure portal].</span></span>

```python
bus_service.create_topic('mytopic')
```

<span data-ttu-id="9056f-115">`create_topic` 메서드는 추가 옵션도 지원합니다. 이러한 옵션을 통해 메시지 TTL(Time to Live)이나 최대 토픽 크기 등 기본 토픽 설정을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9056f-115">The `create_topic` method also supports additional options, which enable you to override default topic settings such as message time to live or maximum topic size.</span></span> <span data-ttu-id="9056f-116">다음은 최대 토픽 크기를 5GB, TTL(Time to Live)을 1분으로 설정하는 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="9056f-116">The following example sets the maximum topic size to 5 GB, and a time to live (TTL) value of 1 minute:</span></span>

```python
topic_options = Topic()
topic_options.max_size_in_megabytes = '5120'
topic_options.default_message_time_to_live = 'PT1M'

bus_service.create_topic('mytopic', topic_options)
```

## <a name="create-subscriptions"></a><span data-ttu-id="9056f-117">구독 만들기</span><span class="sxs-lookup"><span data-stu-id="9056f-117">Create subscriptions</span></span>
<span data-ttu-id="9056f-118">토픽에 대한 구독은 **ServiceBusService** 개체로도 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9056f-118">Subscriptions to topics are also created with the **ServiceBusService** object.</span></span> <span data-ttu-id="9056f-119">구독에는 이름이 지정되며, 구독의 가상 큐에 전달되는 메시지 집합을 제한하는 선택적 필터가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9056f-119">Subscriptions are named and can have an optional filter that restricts the set of messages delivered to the subscription's virtual queue.</span></span>

> [!NOTE]
> <span data-ttu-id="9056f-120">구독은 영구적이며, 구독 자체 또는 구독하는 토픽이 삭제될 때까지 계속 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="9056f-120">Subscriptions are persistent and will continue to exist until either they, or the topic to which they are subscribed, are deleted.</span></span>
> 
> 

### <a name="create-a-subscription-with-the-default-matchall-filter"></a><span data-ttu-id="9056f-121">기본(MatchAll) 필터를 사용하여 구독 만들기</span><span class="sxs-lookup"><span data-stu-id="9056f-121">Create a subscription with the default (MatchAll) filter</span></span>
<span data-ttu-id="9056f-122">**MatchAll** 필터는 새 구독을 만들 때 필터를 지정하지 않은 경우 사용되는 기본 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="9056f-122">The **MatchAll** filter is the default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="9056f-123">**MatchAll** 필터를 사용하면 토픽에 게시된 모든 메시지가 구독의 가상 큐에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="9056f-123">When the **MatchAll** filter is used, all messages published to the topic are placed in the subscription's virtual queue.</span></span> <span data-ttu-id="9056f-124">다음 예제에서는 `AllMessages`라는 구독을 만들고 기본 **MatchAll** 필터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9056f-124">The following example creates a subscription named `AllMessages` and uses the default **MatchAll** filter.</span></span>

```python
bus_service.create_subscription('mytopic', 'AllMessages')
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="9056f-125">필터를 사용하여 구독 만들기</span><span class="sxs-lookup"><span data-stu-id="9056f-125">Create subscriptions with filters</span></span>
<span data-ttu-id="9056f-126">토픽으로 전송된 메시지 중 특정 토픽 구독 내에 표시되어야 하는 메시지의 범위를 지정하는 필터를 정의할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9056f-126">You can also define filters that enable you to specify which messages sent to a topic should show up within a specific topic subscription.</span></span>

<span data-ttu-id="9056f-127">구독에서 지원하는 가장 유연한 유형의 필터는 SQL92 하위 집합을 구현하는 **SqlFilter**입니다.</span><span class="sxs-lookup"><span data-stu-id="9056f-127">The most flexible type of filter supported by subscriptions is a **SqlFilter**, which implements a subset of SQL92.</span></span> <span data-ttu-id="9056f-128">SQL 필터는 토픽에 게시된 메시지의 속성에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9056f-128">SQL filters operate on the properties of the messages that are published to the topic.</span></span> <span data-ttu-id="9056f-129">SQL 필터와 함께 사용할 수 있는 식에 대한 자세한 내용은 [SqlFilter.SqlExpression][SqlFilter.SqlExpression] 구문을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9056f-129">For more information about the expressions that can be used with a SQL filter, see the [SqlFilter.SqlExpression][SqlFilter.SqlExpression] syntax.</span></span>

<span data-ttu-id="9056f-130">**ServiceBusService** 개체의 **create\_rule** 메서드를 사용하여 구독에 필터를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9056f-130">You can add filters to a subscription by using the **create\_rule** method of the **ServiceBusService** object.</span></span> <span data-ttu-id="9056f-131">이 메서드를 사용하면 기존 구독에 새 필터를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9056f-131">This method allows you to add new filters to an existing subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="9056f-132">기본 필터는 모든 새로운 구독에 자동으로 적용되므로 먼저 기본 필터를 제거해야 합니다. 그렇지 않으면 **MatchAll**이 사용자가 지정하는 기타 필터를 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="9056f-132">Because the default filter is applied automatically to all new subscriptions, you must first remove the default filter or the **MatchAll** will override any other filters you may specify.</span></span> <span data-ttu-id="9056f-133">**ServiceBusService** 개체의 `delete_rule` 메서드를 사용하여 기본 규칙을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9056f-133">You can remove the default rule by using the `delete_rule` method of the **ServiceBusService** object.</span></span>
> 
> 

<span data-ttu-id="9056f-134">다음 예제에서는 사용자 지정 `messagenumber` 속성이 3보다 큰 메시지만 선택하는 **SqlFilter**를 사용하여 이름이 `HighMessages`인 구독을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9056f-134">The following example creates a subscription named `HighMessages` with a **SqlFilter** that only selects messages that have a custom `messagenumber` property greater than 3:</span></span>

```python
bus_service.create_subscription('mytopic', 'HighMessages')

rule = Rule()
rule.filter_type = 'SqlFilter'
rule.filter_expression = 'messagenumber > 3'

bus_service.create_rule('mytopic', 'HighMessages', 'HighMessageFilter', rule)
bus_service.delete_rule('mytopic', 'HighMessages', DEFAULT_RULE_NAME)
```

<span data-ttu-id="9056f-135">마찬가지로, 다음 예제에서는 `messagenumber` 속성이 3 이하인 메시지만 선택하는 **SqlFilter**가 있는 이름이 `LowMessages`인 구독을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9056f-135">Similarly, the following example creates a subscription named `LowMessages` with a **SqlFilter** that only selects messages that have a `messagenumber` property less than or equal to 3:</span></span>

```python
bus_service.create_subscription('mytopic', 'LowMessages')

rule = Rule()
rule.filter_type = 'SqlFilter'
rule.filter_expression = 'messagenumber <= 3'

bus_service.create_rule('mytopic', 'LowMessages', 'LowMessageFilter', rule)
bus_service.delete_rule('mytopic', 'LowMessages', DEFAULT_RULE_NAME)
```

<span data-ttu-id="9056f-136">이제 `mytopic`으로 메시지를 보내는 경우 **AllMessages** 토픽 구독을 구독하는 수신자에게는 항상 배달되고, **HighMessages** 및 **LowMessages** 토픽 구독을 구독하는 수신자에게는 메시지 콘텐츠에 따라 선택적으로 배달됩니다.</span><span class="sxs-lookup"><span data-stu-id="9056f-136">Now, when a message is sent to `mytopic` it is always delivered to receivers subscribed to the **AllMessages** topic subscription, and selectively delivered to receivers subscribed to the **HighMessages** and **LowMessages** topic subscriptions (depending on the message content).</span></span>

## <a name="send-messages-to-a-topic"></a><span data-ttu-id="9056f-137">토픽에 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="9056f-137">Send messages to a topic</span></span>
<span data-ttu-id="9056f-138">Service Bus 토픽에 메시지를 보내려면 응용 프로그램에서 **ServiceBusService** 개체의 `send_topic_message` 메서드를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9056f-138">To send a message to a Service Bus topic, your application must use the `send_topic_message` method of the **ServiceBusService** object.</span></span>

<span data-ttu-id="9056f-139">다음 예제에서는 5개의 테스트 메시지를 `mytopic`에 보내는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9056f-139">The following example demonstrates how to send five test messages to `mytopic`.</span></span> <span data-ttu-id="9056f-140">루프가 반복될 때마다 각 메시지의 `messagenumber` 속성 값이 변경되며 이 값에 따라 해당 메시지를 받는 구독이 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="9056f-140">Note that the `messagenumber` property value of each message varies on the iteration of the loop (this determines which subscriptions receive it):</span></span>

```python
for i in range(5):
    msg = Message('Msg {0}'.format(i).encode('utf-8'), custom_properties={'messagenumber':i})
    bus_service.send_topic_message('mytopic', msg)
```

<span data-ttu-id="9056f-141">Service Bus 토픽은 [표준 계층](service-bus-premium-messaging.md)에서 256KB의 최대 메시지 크기를 [프리미엄 계층](service-bus-premium-messaging.md)에서 1MB를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="9056f-141">Service Bus topics support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="9056f-142">표준 및 사용자 지정 응용 프로그램 속성이 포함된 헤더의 최대 크기는 64KB입니다.</span><span class="sxs-lookup"><span data-stu-id="9056f-142">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="9056f-143">한 토픽에 저장되는 메시지 수에는 제한이 없지만 한 토픽에 저장되는 총 메시지 크기는 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="9056f-143">There is no limit on the number of messages held in a topic but there is a cap on the total size of the messages held by a topic.</span></span> <span data-ttu-id="9056f-144">이 토픽 크기는 생성 시 정의되며 상한이 5GB입니다.</span><span class="sxs-lookup"><span data-stu-id="9056f-144">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span> <span data-ttu-id="9056f-145">할당량에 대한 자세한 내용은 [Service Bus 할당량][Service Bus quotas]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9056f-145">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="9056f-146">구독에서 메시지 받기</span><span class="sxs-lookup"><span data-stu-id="9056f-146">Receive messages from a subscription</span></span>
<span data-ttu-id="9056f-147">**ServiceBusService** 개체의 `receive_subscription_message` 메서드를 사용하여 구독에서 메시지를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="9056f-147">Messages are received from a subscription using the `receive_subscription_message` method on the **ServiceBusService** object:</span></span>

```python
msg = bus_service.receive_subscription_message('mytopic', 'LowMessages', peek_lock=False)
print(msg.body)
```

<span data-ttu-id="9056f-148">`peek_lock` 매개 변수가 **False**로 설정된 경우 메시지를 읽으면 구독에서 해당 메시지가 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="9056f-148">Messages are deleted from the subscription as they are read when the parameter `peek_lock` is set to **False**.</span></span> <span data-ttu-id="9056f-149">`peek_lock` 매개 변수를 **True**로 설정하여 큐에서 삭제되지 않도록 메시지를 읽은(peek) 후 잠글 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9056f-149">You can read (peek) and lock the message without deleting it from the queue by setting the parameter `peek_lock` to **True**.</span></span>

<span data-ttu-id="9056f-150">받기 작업의 일부로 메시지를 읽고 삭제하는 동작은 가장 단순한 모델이며, 실패할 경우 응용 프로그램이 메시지를 처리하지 않아도 되는 시나리오에서 가장 효과적입니다.</span><span class="sxs-lookup"><span data-stu-id="9056f-150">The behavior of reading and deleting the message as part of the receive operation is the simplest model, and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="9056f-151">이해를 돕기 위해 소비자가 수신 요청을 실행한 후 처리하기 전에 크래시되는 시나리오를 고려해 보세요.</span><span class="sxs-lookup"><span data-stu-id="9056f-151">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="9056f-152">서비스 버스는 메시지를 이용되는 것으로 표시하기 때문에 응용 프로그램이 다시 시작되고 메시지 소비를 다시 시작할 경우 크래시 전에 소비된 메시지가 누락됩니다.</span><span class="sxs-lookup"><span data-stu-id="9056f-152">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="9056f-153">`peek_lock` 매개 변수를 **True**로 설정하면 수신은 2단계 작업이 되므로, 메시지 누락을 허용하지 않는 응용 프로그램을 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9056f-153">If the `peek_lock` parameter is set to **True**, the receive becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="9056f-154">서비스 버스는 요청을 받으면 소비할 다음 메시지를 찾아서 다른 소비자가 수신할 수 없도록 잠근 후 응용 프로그램에 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="9056f-154">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span> <span data-ttu-id="9056f-155">응용 프로그램은 메시지 처리를 완료하거나 추가 처리를 위해 안전하게 저장한 후 **Message** 개체에 대해 `delete` 메서드를 호출하여 수신 프로세스의 두 번째 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="9056f-155">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling `delete` method on the **Message** object.</span></span> <span data-ttu-id="9056f-156">`delete` 메서드는 메시지를 사용 중인 것으로 표시하고 구독에서 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="9056f-156">The `delete` method marks the message as being consumed and removes it from the subscription.</span></span>

```python
msg = bus_service.receive_subscription_message('mytopic', 'LowMessages', peek_lock=True)
print(msg.body)

msg.delete()
```

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="9056f-157">응용 프로그램 작동 중단 및 읽을 수 없는 메시지를 처리하는 방법</span><span class="sxs-lookup"><span data-stu-id="9056f-157">How to handle application crashes and unreadable messages</span></span>
<span data-ttu-id="9056f-158">서비스 버스는 응용 프로그램 오류나 메시지 처리 문제를 정상적으로 복구하는 데 유용한 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9056f-158">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="9056f-159">어떤 이유로든 수신 응용 프로그램이 메시지를 처리할 수 없는 경우 **Message** 개체의 `unlock` 메서드를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9056f-159">If a receiver application is unable to process the message for some reason, then it can call the `unlock` method on the **Message** object.</span></span> <span data-ttu-id="9056f-160">그러면 Service Bus에서 구독 내 메시지의 잠금을 해제하므로 동일한 소비 응용 프로그램이나 다른 소비 응용 프로그램에서 메시지를 다시 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9056f-160">This will cause Service Bus to unlock the message within the subscription and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="9056f-161">구독 내에서 잠긴 메시지와 연결된 제한 시간도 있으며, 응용 프로그램에서 잠금 시간 제한이 만료되기 전에 메시지를 처리하지 못하는 경우(예: 응용 프로그램이 크래시되는 경우) Service Bus가 메시지를 자동으로 잠금 해제하여 다시 받을 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="9056f-161">There is also a timeout associated with a message locked within the subscription, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus unlocks the message automatically and makes it available to be received again.</span></span>

<span data-ttu-id="9056f-162">응용 프로그램이 메시지를 처리한 후 `delete` 메서드가 호출되기 전에 충돌하는 경우, 다시 시작될 때 메시지가 응용 프로그램에 다시 배달됩니다.</span><span class="sxs-lookup"><span data-stu-id="9056f-162">In the event that the application crashes after processing the message but before the `delete` method is called, then the message will be redelivered to the application when it restarts.</span></span> <span data-ttu-id="9056f-163">이를 *최소 한 번 이상 처리*라고 합니다. 즉, 각 메시지가 최소 한 번 이상 처리되지만 특정 상황에서는 동일한 메시지가 다시 배달될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9056f-163">This is often called *At Least Once Processing*, that is, each message will be processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="9056f-164">중복 처리가 허용되지 않는 시나리오에서는 응용 프로그램 개발자가 중복 메시지 배달을 처리하는 논리를 응용 프로그램에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9056f-164">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span></span> <span data-ttu-id="9056f-165">이 경우 대체로 배달 시도 간에 일정하게 유지되는 메시지의 **MessageId** 속성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9056f-165">This is often achieved using the **MessageId** property of the message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="9056f-166">토픽 및 구독 삭제</span><span class="sxs-lookup"><span data-stu-id="9056f-166">Delete topics and subscriptions</span></span>
<span data-ttu-id="9056f-167">토픽과 구독은 영구적이므로, [Azure Portal][Azure portal] 또는 프로그래밍 방식을 통해 명시적으로 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9056f-167">Topics and subscriptions are persistent, and must be explicitly deleted either through the [Azure portal][Azure portal] or programmatically.</span></span> <span data-ttu-id="9056f-168">다음 예제에서는 이름이 `mytopic`인 토픽을 삭제하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9056f-168">The following example shows how to delete the topic named `mytopic`:</span></span>

```python
bus_service.delete_topic('mytopic')
```

<span data-ttu-id="9056f-169">토픽을 삭제하면 토픽에 등록된 모든 구독도 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="9056f-169">Deleting a topic also deletes any subscriptions that are registered with the topic.</span></span> <span data-ttu-id="9056f-170">구독을 개별적으로 삭제할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9056f-170">Subscriptions can also be deleted independently.</span></span> <span data-ttu-id="9056f-171">다음 코드는 이름이 `HighMessages`인 구독을 `mytopic` 토픽에서 삭제하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9056f-171">The following code shows how to delete a subscription named `HighMessages` from the `mytopic` topic:</span></span>

```python
bus_service.delete_subscription('mytopic', 'HighMessages')
```

## <a name="next-steps"></a><span data-ttu-id="9056f-172">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9056f-172">Next steps</span></span>
<span data-ttu-id="9056f-173">이제 서비스 버스 토픽의 기본 사항을 익혔으므로 다음 링크를 따라 이동하여 자세한 내용을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9056f-173">Now that you've learned the basics of Service Bus topics, follow these links to learn more.</span></span>

* <span data-ttu-id="9056f-174">[큐, 토픽 및 구독][Queues, topics, and subscriptions]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9056f-174">See [Queues, topics, and subscriptions][Queues, topics, and subscriptions].</span></span>
* <span data-ttu-id="9056f-175">[SqlFilter.SqlExpression][SqlFilter.SqlExpression]에 대한 참조입니다.</span><span class="sxs-lookup"><span data-stu-id="9056f-175">Reference for [SqlFilter.SqlExpression][SqlFilter.SqlExpression].</span></span>

[Azure portal]: https://portal.azure.com
[Azure Python package]: https://pypi.python.org/pypi/azure  
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter.SqlExpression]: service-bus-messaging-sql-filter.md
[Service Bus quotas]: service-bus-quotas.md 

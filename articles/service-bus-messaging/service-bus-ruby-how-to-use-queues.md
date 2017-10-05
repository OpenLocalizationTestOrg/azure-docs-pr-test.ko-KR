---
title: "Ruby를 통해 Azure Service Bus 큐를 사용하는 방법 | Microsoft Docs"
description: "Azure에서 서비스 버스 큐를 사용하는 방법에 대해 알아봅니다. 코드 샘플은 Ruby로 작성되었습니다."
services: service-bus-messaging
documentationcenter: ruby
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 0a11eab2-823f-4cc7-842b-fbbe0f953751
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 357a7277dd42b6973cf35a9f642b8eec36a745e3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-service-bus-queues-with-ruby"></a><span data-ttu-id="9a591-104">Ruby에서 Service Bus 큐를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="9a591-104">How to use Service Bus queues with Ruby</span></span>

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="9a591-105">이 가이드에서는 서비스 버스 큐를 사용하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9a591-105">This guide describes how to use Service Bus queues.</span></span> <span data-ttu-id="9a591-106">샘플은 Ruby로 작성되었으며 Azure gem을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9a591-106">The samples are written in Ruby and use the Azure gem.</span></span> <span data-ttu-id="9a591-107">여기서 다루는 시나리오에는 **큐 만들기, 메시지 보내기 및 받기**, **큐 삭제** 등이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a591-107">The scenarios covered include **creating queues, sending and receiving messages**, and **deleting queues**.</span></span> <span data-ttu-id="9a591-108">Service Bus 큐에 대한 자세한 내용은 [다음 단계](#next-steps) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9a591-108">For more information about Service Bus queues, see the [Next Steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]
   
[!INCLUDE [service-bus-ruby-setup](../../includes/service-bus-ruby-setup.md)]

## <a name="how-to-create-a-queue"></a><span data-ttu-id="9a591-109">큐를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="9a591-109">How to create a queue</span></span>
<span data-ttu-id="9a591-110">**Azure::ServiceBusService** 개체를 사용하면 큐로 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a591-110">The **Azure::ServiceBusService** object enables you to work with queues.</span></span> <span data-ttu-id="9a591-111">큐를 만들려면 `create_queue()` 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9a591-111">To create a queue, use the `create_queue()` method.</span></span> <span data-ttu-id="9a591-112">다음 예제에서는 큐를 만들거나 오류를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="9a591-112">The following example creates a queue or prints out any errors.</span></span>

```ruby
azure_service_bus_service = Azure::ServiceBus::ServiceBusService.new(sb_host, { signer: signer})
begin
  queue = azure_service_bus_service.create_queue("test-queue")
rescue
  puts $!
end
```

<span data-ttu-id="9a591-113">추가 옵션을 사용하여 **Azure::ServiceBus::Queue** 개체를 전달할 수도 있습니다. 추가 옵션을 사용하면 메시지 TTL(Time to Live) 또는 최대 큐 크기와 같은 기본 큐 설정을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a591-113">You can also pass a **Azure::ServiceBus::Queue** object with additional options, which enables you to override the default queue settings, such as message time to live or maximum queue size.</span></span> <span data-ttu-id="9a591-114">다음 예제에서는 최대 큐 크기를 5GB로 설정하고 TTL(Time to Live)을 1분으로 설정하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="9a591-114">The following example shows how to set the maximum queue size to 5 GB and time to live to 1 minute:</span></span>

```ruby
queue = Azure::ServiceBus::Queue.new("test-queue")
queue.max_size_in_megabytes = 5120
queue.default_message_time_to_live = "PT1M"

queue = azure_service_bus_service.create_queue(queue)
```

## <a name="how-to-send-messages-to-a-queue"></a><span data-ttu-id="9a591-115">큐에 메시지를 보내는 방법</span><span class="sxs-lookup"><span data-stu-id="9a591-115">How to send messages to a queue</span></span>
<span data-ttu-id="9a591-116">Service Bus 큐에 메시지를 보내기 위해 응용 프로그램은 **Azure::ServiceBusService** 개체에 대해 `send_queue_message()` 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="9a591-116">To send a message to a Service Bus queue, your application calls the `send_queue_message()` method on the **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="9a591-117">Service Bus 큐로 보내고 받는 메시지는 **Azure::ServiceBus::BrokeredMessage** 개체이며 표준 속성 집합(예: `label` 및 `time_to_live`), 응용 프로그램별 사용자 지정 속성을 저장하는 데 사용되는 사전 및 임의 응용 프로그램 데이터 본문을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="9a591-117">Messages sent to (and received from) Service Bus queues are **Azure::ServiceBus::BrokeredMessage** objects, and have a set of standard properties (such as `label` and `time_to_live`), a dictionary that is used to hold custom application-specific properties, and a body of arbitrary application data.</span></span> <span data-ttu-id="9a591-118">응용 프로그램은 문자열 값을 메시지로 전달하여 메시지의 본문을 설정할 수 있습니다. 그러면 필수 표준 속성이 기본값으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="9a591-118">An application can set the body of the message by passing a string value as the message and any required standard properties are populated with default values.</span></span>

<span data-ttu-id="9a591-119">다음 예제에서는 `send_queue_message()`를 사용하여 `test-queue`라는 큐에 테스트 메시지를 보내는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="9a591-119">The following example demonstrates how to send a test message to the queue named `test-queue` using `send_queue_message()`:</span></span>

```ruby
message = Azure::ServiceBus::BrokeredMessage.new("test queue message")
message.correlation_id = "test-correlation-id"
azure_service_bus_service.send_queue_message("test-queue", message)
```

<span data-ttu-id="9a591-120">Service Bus 큐는 [표준 계층](service-bus-premium-messaging.md)에서 256KB의 최대 메시지 크기를 [프리미엄 계층](service-bus-premium-messaging.md)에서 1MB를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="9a591-120">Service Bus queues support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="9a591-121">표준 및 사용자 지정 응용 프로그램 속성이 포함된 헤더의 최대 크기는 64KB입니다.</span><span class="sxs-lookup"><span data-stu-id="9a591-121">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="9a591-122">한 큐에 저장되는 메시지 수에는 제한이 없지만 한 큐에 저장되는 총 메시지 크기는 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a591-122">There is no limit on the number of messages held in a queue but there is a cap on the total size of the messages held by a queue.</span></span> <span data-ttu-id="9a591-123">이 큐 크기는 생성 시 정의되며 상한이 5GB입니다.</span><span class="sxs-lookup"><span data-stu-id="9a591-123">This queue size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="how-to-receive-messages-from-a-queue"></a><span data-ttu-id="9a591-124">큐에서 메시지를 받는 방법</span><span class="sxs-lookup"><span data-stu-id="9a591-124">How to receive messages from a queue</span></span>
<span data-ttu-id="9a591-125">**Azure::ServiceBusService** 개체의 `receive_queue_message()` 메서드를 사용하여 큐에서 메시지를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="9a591-125">Messages are received from a queue using the `receive_queue_message()` method on the **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="9a591-126">기본적으로 메시지는 큐에서 삭제하지 않고 읽고 잠급니다.</span><span class="sxs-lookup"><span data-stu-id="9a591-126">By default, messages are read and locked without being deleted from the queue.</span></span> <span data-ttu-id="9a591-127">그러나 `:peek_lock` 옵션을 **false**로 설정하여 메시지를 읽고 큐에서 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a591-127">However, you can delete messages from the queue as they are read by setting the `:peek_lock` option to **false**.</span></span>

<span data-ttu-id="9a591-128">기본 동작은 읽기 및 삭제가 2단계 작업으로 수행되도록 하므로 메시지 누락이 허용되지 않는 응용 프로그램도 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a591-128">The default behavior makes the reading and deleting a two-stage operation, which also makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="9a591-129">서비스 버스는 요청을 받으면 소비할 다음 메시지를 찾아서 다른 소비자가 수신할 수 없도록 잠근 후 응용 프로그램에 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="9a591-129">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span> <span data-ttu-id="9a591-130">응용 프로그램은 메시지 처리를 완료하거나 추가 처리를 위해 안전하게 저장한 후, `delete_queue_message()` 메서드를 호출하고 삭제될 메시지를 매개 변수로 제공하여 수신 프로세스의 두 번째 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="9a591-130">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling `delete_queue_message()` method and providing the message to be deleted as a parameter.</span></span> <span data-ttu-id="9a591-131">`delete_queue_message()` 메서드는 메시지를 이용되는 것으로 표시하고 큐에서 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="9a591-131">The `delete_queue_message()` method will mark the message as being consumed and remove it from the queue.</span></span>

<span data-ttu-id="9a591-132">`:peek_lock` 매개 변수를 **false**로 설정하면 메시지 읽기 및 삭제가 가장 간단한 모델이 되며, 오류 발생 시 메시지를 처리하지 않는 것을 허용하는 응용 프로그램의 시나리오에 가장 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="9a591-132">If the `:peek_lock` parameter is set to **false**, reading and deleting the message becomes the simplest model, and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="9a591-133">이해를 돕기 위해 소비자가 수신 요청을 실행한 후 처리하기 전에 크래시되는 시나리오를 고려해 보세요.</span><span class="sxs-lookup"><span data-stu-id="9a591-133">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="9a591-134">Service Bus가 메시지를 사용되는 것으로 표시했기 때문에 응용 프로그램이 다시 시작되고 메시지를 다시 사용하기 시작할 때 충돌 전에 사용한 메시지는 누락됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a591-134">Because Service Bus has marked the message as being consumed, when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="9a591-135">다음 예제에서는 `receive_queue_message()`를 사용하여 메시지를 받고 처리하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="9a591-135">The following example demonstrates how to receive and process messages using `receive_queue_message()`.</span></span> <span data-ttu-id="9a591-136">이 예제에서는 먼저 **false**로 설정된 `:peek_lock`을 사용하여 메시지를 받고 삭제한 후 다른 메시지를 받고 그런 다음 `delete_queue_message()`를 사용하여 메시지를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="9a591-136">The example first receives and deletes a message by using `:peek_lock` set to **false**, then it receives another message and then deletes the message using `delete_queue_message()`:</span></span>

```ruby
message = azure_service_bus_service.receive_queue_message("test-queue",
  { :peek_lock => false })
message = azure_service_bus_service.receive_queue_message("test-queue")
azure_service_bus_service.delete_queue_message(message)
```

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="9a591-137">응용 프로그램 작동 중단 및 읽을 수 없는 메시지를 처리하는 방법</span><span class="sxs-lookup"><span data-stu-id="9a591-137">How to handle application crashes and unreadable messages</span></span>
<span data-ttu-id="9a591-138">서비스 버스는 응용 프로그램 오류나 메시지 처리 문제를 정상적으로 복구하는 데 유용한 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9a591-138">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="9a591-139">어떤 이유로든 수신 응용 프로그램이 메시지를 처리할 수 없는 경우 **Azure::ServiceBusService** 개체의 `unlock_queue_message()` 메서드를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a591-139">If a receiver application is unable to process the message for some reason, then it can call the `unlock_queue_message()` method on the **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="9a591-140">이 호출은 Service Bus에서 큐 메시지의 잠금을 해제하므로 동일한 소비 응용 프로그램이나 다른 소비 응용 프로그램에서 메시지를 다시 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a591-140">This call causes Service Bus to unlock the message within the queue and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="9a591-141">큐 내에서 잠긴 메시지와 연결된 시간 제한도 있으며, 응용 프로그램에서 잠금 시간 제한이 만료되기 전에 메시지를 처리하지 못하는 경우(예: 응용 프로그램이 크래시되는 경우) 서비스 버스가 메시지를 자동으로 잠금 해제하여 다시 받을 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a591-141">There is also a timeout associated with a message locked within the queue, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus unlocks the message automatically and makes it available to be received again.</span></span>

<span data-ttu-id="9a591-142">응용 프로그램이 메시지를 처리한 후 `delete_queue_message()` 메서드가 호출되기 전에 충돌하는 경우, 다시 시작될 때 메시지가 응용 프로그램에 다시 배달됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a591-142">In the event that the application crashes after processing the message but before the `delete_queue_message()` method is called, then the message is redelivered to the application when it restarts.</span></span> <span data-ttu-id="9a591-143">이 프로세스를 *최소 한 번 이상 처리*라고 합니다. 즉, 각 메시지가 최소 한 번 이상 처리되지만 특정 상황에서는 동일한 메시지가 다시 배달될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a591-143">This process is often called *At Least Once Processing*; that is, each message is processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="9a591-144">중복 처리가 허용되지 않는 시나리오에서는 응용 프로그램 개발자가 중복 메시지 배달을 처리하는 논리를 응용 프로그램에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a591-144">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span></span> <span data-ttu-id="9a591-145">이 경우 대체로 배달 시도 간에 일정하게 유지되는 메시지의 `message_id` 속성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9a591-145">This is often achieved using the `message_id` property of the message, which remains constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9a591-146">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9a591-146">Next steps</span></span>
<span data-ttu-id="9a591-147">이제 서비스 버스 큐의 기본 사항을 익혔으므로 다음 링크를 따라 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="9a591-147">Now that you've learned the basics of Service Bus queues, follow these links to learn more.</span></span>

* <span data-ttu-id="9a591-148">[큐, 토픽 및 구독](service-bus-queues-topics-subscriptions.md) 개요.</span><span class="sxs-lookup"><span data-stu-id="9a591-148">Overview of [queues, topics, and subscriptions](service-bus-queues-topics-subscriptions.md).</span></span>
* <span data-ttu-id="9a591-149">GitHub에서 [Azure SDK for Ruby](https://github.com/Azure/azure-sdk-for-ruby) 리포지토리를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="9a591-149">Visit the [Azure SDK for Ruby](https://github.com/Azure/azure-sdk-for-ruby) repository on GitHub.</span></span>

<span data-ttu-id="9a591-150">이 문서에서 설명한 Azure Service Bus 큐와 [Ruby에서 큐 Storage를 사용하는 방법](../storage/queues/storage-ruby-how-to-use-queue-storage.md) 문서에서 설명한 Azure 큐를 비교하려면 [Azure 큐 및 Azure Service Bus 큐 - 비교 및 대조](service-bus-azure-and-service-bus-queues-compared-contrasted.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9a591-150">For a comparison between the Azure Service Bus queues discussed in this article and Azure Queues discussed in the [How to use Queue storage from Ruby](../storage/queues/storage-ruby-how-to-use-queue-storage.md) article, see [Azure Queues and Azure Service Bus Queues - Compared and Contrasted](service-bus-azure-and-service-bus-queues-compared-contrasted.md)</span></span>


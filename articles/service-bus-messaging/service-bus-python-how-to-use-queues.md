---
title: "Python에서 Azure Service Bus 큐를 사용하는 방법 | Microsoft Docs"
description: "Python에서 Azure 서비스 버스 큐를 사용하는 방법에 대해 알아봅니다."
services: service-bus-messaging
documentationcenter: python
author: sethmanheim
manager: timlt
editor: 
ms.assetid: b95ee5cd-3b31-459c-a7f3-cf8bcf77858b
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm;lmazuel
ms.openlocfilehash: e1e81ad1d7b4fe0e044917f090cac59dfd5b6332
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-service-bus-queues-with-python"></a><span data-ttu-id="f2e97-103">Python에서 Service Bus 큐를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="f2e97-103">How to use Service Bus queues with Python</span></span>

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="f2e97-104">이 문서에서는 서비스 버스 큐를 사용하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f2e97-104">This article describes how to use Service Bus queues.</span></span> <span data-ttu-id="f2e97-105">샘플은 Python으로 작성되었으며 [Python Azure Service Bus 패키지][Python Azure Service Bus package]를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f2e97-105">The samples are written in Python and use the [Python Azure Service Bus package][Python Azure Service Bus package].</span></span> <span data-ttu-id="f2e97-106">여기서 다루는 시나리오에는 **큐 만들기, 메시지 보내기 및 받기**, **큐 삭제** 등이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2e97-106">The scenarios covered include **creating queues, sending and receiving messages**, and **deleting queues**.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

> [!NOTE]
> <span data-ttu-id="f2e97-107">Python 또는 [Python Azure Service Bus 패키지][Python Azure Service Bus package]를 설치해야 하는 경우 [Python 설치 가이드](../python-how-to-install.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f2e97-107">To install Python or the [Python Azure Service Bus package][Python Azure Service Bus package], see the [Python Installation Guide](../python-how-to-install.md).</span></span>
> 
> 

## <a name="create-a-queue"></a><span data-ttu-id="f2e97-108">큐 만들기</span><span class="sxs-lookup"><span data-stu-id="f2e97-108">Create a queue</span></span>
<span data-ttu-id="f2e97-109">**ServiceBusService** 개체를 사용하면 큐로 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2e97-109">The **ServiceBusService** object enables you to work with queues.</span></span> <span data-ttu-id="f2e97-110">프로그래밍 방식으로 서비스 버스에 액세스하려는 Python 파일의 맨 위쪽에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f2e97-110">Add the following code near the top of any Python file in which you wish to programmatically access Service Bus:</span></span>

```python
from azure.servicebus import ServiceBusService, Message, Queue
```

<span data-ttu-id="f2e97-111">다음 코드는 **ServiceBusService** 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f2e97-111">The following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="f2e97-112">`mynamespace`, `sharedaccesskeyname` 및 `sharedaccesskey`를 네임스페이스, SAS(공유 액세스 서명) 키 이름 및 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f2e97-112">Replace `mynamespace`, `sharedaccesskeyname`, and `sharedaccesskey` with your namespace, shared access signature (SAS) key name, and value.</span></span>

```python
bus_service = ServiceBusService(
    service_namespace='mynamespace',
    shared_access_key_name='sharedaccesskeyname',
    shared_access_key_value='sharedaccesskey')
```

<span data-ttu-id="f2e97-113">SAS 키 이름 및 값에 대한 값은 [Azure Portal][Azure portal] 연결 정보 또는 Visual Studio **속성** 창(이전 섹션에 표시된 대로 서버 탐색기에서 Service Bus 네임스페이스 선택)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2e97-113">The values for the SAS key name and value can be found in the [Azure portal][Azure portal] connection information, or in the Visual Studio **Properties** pane when selecting the Service Bus namespace in Server Explorer (as shown in the previous section).</span></span>

```python
bus_service.create_queue('taskqueue')
```

<span data-ttu-id="f2e97-114">`create_queue`는 추가 옵션도 지원합니다. 이러한 옵션을 통해 메시지 TTL(Time to Live)이나 최대 큐 크기 등 기본 큐 설정을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2e97-114">The `create_queue` method also supports additional options, which enable you to override default queue settings such as message time to live (TTL) or maximum queue size.</span></span> <span data-ttu-id="f2e97-115">다음은 최대 큐 크기를 5GB로, TTL 값을 1분으로 설정하는 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="f2e97-115">The following example sets the maximum queue size to 5 GB, and the TTL value to 1 minute:</span></span>

```python
queue_options = Queue()
queue_options.max_size_in_megabytes = '5120'
queue_options.default_message_time_to_live = 'PT1M'

bus_service.create_queue('taskqueue', queue_options)
```

## <a name="send-messages-to-a-queue"></a><span data-ttu-id="f2e97-116">큐에 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="f2e97-116">Send messages to a queue</span></span>
<span data-ttu-id="f2e97-117">Service Bus 큐에 메시지를 보내기 위해 응용 프로그램은 **ServiceBusService** 개체에 대해 `send_queue_message` 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="f2e97-117">To send a message to a Service Bus queue, your application calls the `send_queue_message` method on the **ServiceBusService** object.</span></span>

<span data-ttu-id="f2e97-118">다음 예제에서는 `send_queue_message`를 사용하여 `taskqueue`라는 큐에 테스트 메시지를 보내는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="f2e97-118">The following example demonstrates how to send a test message to the queue named `taskqueue` using `send_queue_message`:</span></span>

```python
msg = Message(b'Test Message')
bus_service.send_queue_message('taskqueue', msg)
```

<span data-ttu-id="f2e97-119">Service Bus 큐는 [표준 계층](service-bus-premium-messaging.md)에서 256KB의 최대 메시지 크기를 [프리미엄 계층](service-bus-premium-messaging.md)에서 1MB를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="f2e97-119">Service Bus queues support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="f2e97-120">표준 및 사용자 지정 응용 프로그램 속성이 포함된 헤더의 최대 크기는 64KB입니다.</span><span class="sxs-lookup"><span data-stu-id="f2e97-120">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="f2e97-121">한 큐에 저장되는 메시지 수에는 제한이 없지만 한 큐에 저장되는 총 메시지 크기는 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2e97-121">There is no limit on the number of messages held in a queue but there is a cap on the total size of the messages held by a queue.</span></span> <span data-ttu-id="f2e97-122">이 큐 크기는 생성 시 정의되며 상한이 5GB입니다.</span><span class="sxs-lookup"><span data-stu-id="f2e97-122">This queue size is defined at creation time, with an upper limit of 5 GB.</span></span> <span data-ttu-id="f2e97-123">할당량에 대한 자세한 내용은 [Service Bus 할당량][Service Bus quotas]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f2e97-123">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="f2e97-124">큐에서 메시지 받기</span><span class="sxs-lookup"><span data-stu-id="f2e97-124">Receive messages from a queue</span></span>
<span data-ttu-id="f2e97-125">**ServiceBusService** 개체의 `receive_queue_message` 메서드를 사용하여 큐에서 메시지를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="f2e97-125">Messages are received from a queue using the `receive_queue_message` method on the **ServiceBusService** object:</span></span>

```python
msg = bus_service.receive_queue_message('taskqueue', peek_lock=False)
print(msg.body)
```

<span data-ttu-id="f2e97-126">`peek_lock` 매개 변수가 **False**로 설정된 경우 메시지를 읽으면 큐에서 해당 메시지가 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2e97-126">Messages are deleted from the queue as they are read when the parameter `peek_lock` is set to **False**.</span></span> <span data-ttu-id="f2e97-127">`peek_lock` 매개 변수를 **True**로 설정하여 큐에서 삭제되지 않도록 메시지를 읽은(peek) 후 잠글 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2e97-127">You can read (peek) and lock the message without deleting it from the queue by setting the parameter `peek_lock` to **True**.</span></span>

<span data-ttu-id="f2e97-128">받기 작업의 일부로 메시지를 읽고 삭제하는 동작은 가장 단순한 모델이며, 실패할 경우 응용 프로그램이 메시지를 처리하지 않아도 되는 시나리오에서 가장 효과적입니다.</span><span class="sxs-lookup"><span data-stu-id="f2e97-128">The behavior of reading and deleting the message as part of the receive operation is the simplest model, and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="f2e97-129">이해를 돕기 위해 소비자가 수신 요청을 실행한 후 처리하기 전에 크래시되는 시나리오를 고려해 보세요.</span><span class="sxs-lookup"><span data-stu-id="f2e97-129">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="f2e97-130">서비스 버스는 메시지를 이용되는 것으로 표시하기 때문에 응용 프로그램이 다시 시작되고 메시지 소비를 다시 시작할 경우 크래시 전에 소비된 메시지가 누락됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2e97-130">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="f2e97-131">`peek_lock` 매개 변수를 **True**로 설정하면 수신은 2단계 작업이 되므로, 메시지 누락을 허용하지 않는 응용 프로그램을 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2e97-131">If the `peek_lock` parameter is set to **True**, the receive becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="f2e97-132">서비스 버스는 요청을 받으면 소비할 다음 메시지를 찾아서 다른 소비자가 수신할 수 없도록 잠근 후 응용 프로그램에 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="f2e97-132">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span> <span data-ttu-id="f2e97-133">응용 프로그램은 메시지 처리를 완료하거나 추가 처리를 위해 안전하게 저장한 후 **Message** 개체에 대해 **delete** 메서드를 호출하여 수신 프로세스의 두 번째 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="f2e97-133">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling the **delete** method on the **Message** object.</span></span> <span data-ttu-id="f2e97-134">**delete** 메서드는 메시지를 이용되는 것으로 표시하고 큐에서 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="f2e97-134">The **delete** method will mark the message as being consumed and remove it from the queue.</span></span>

```python
msg = bus_service.receive_queue_message('taskqueue', peek_lock=True)
print(msg.body)

msg.delete()
```

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="f2e97-135">응용 프로그램 작동 중단 및 읽을 수 없는 메시지를 처리하는 방법</span><span class="sxs-lookup"><span data-stu-id="f2e97-135">How to handle application crashes and unreadable messages</span></span>
<span data-ttu-id="f2e97-136">서비스 버스는 응용 프로그램 오류나 메시지 처리 문제를 정상적으로 복구하는 데 유용한 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f2e97-136">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="f2e97-137">어떤 이유로든 수신 응용 프로그램이 메시지를 처리할 수 없는 경우 **Message** 개체의 **unlock** 메서드를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2e97-137">If a receiver application is unable to process the message for some reason, then it can call the **unlock** method on the **Message** object.</span></span> <span data-ttu-id="f2e97-138">그러면 서비스 버스에서 큐 메시지의 잠금을 해제하므로 동일한 소비 응용 프로그램이나 다른 소비 응용 프로그램에서 메시지를 다시 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2e97-138">This will cause Service Bus to unlock the message within the queue and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="f2e97-139">큐 내에서 잠긴 메시지와 연결된 시간 제한도 있으며, 응용 프로그램에서 잠금 시간 제한이 만료되기 전에 메시지를 처리하지 못하는 경우(예: 응용 프로그램이 크래시되는 경우) 서비스 버스가 메시지를 자동으로 잠금 해제하여 다시 받을 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2e97-139">There is also a timeout associated with a message locked within the queue, and if the application fails to process the message before the lock timeout expires (e.g., if the application crashes), then Service Bus will unlock the message automatically and make it available to be received again.</span></span>

<span data-ttu-id="f2e97-140">응용 프로그램이 메시지를 처리한 후 **delete** 메서드가 호출되기 전에 크래시되는 경우, 다시 시작될 때 메시지가 응용 프로그램에 다시 배달됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2e97-140">In the event that the application crashes after processing the message but before the **delete** method is called, then the message will be redelivered to the application when it restarts.</span></span> <span data-ttu-id="f2e97-141">이를 **최소 한 번 이상 처리**라고 합니다. 즉, 각 메시지가 최소 한 번 이상 처리되지만 특정 상황에서는 동일한 메시지가 다시 배달될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2e97-141">This is often called **At Least Once Processing**, that is, each message will be processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="f2e97-142">중복 처리가 허용되지 않는 시나리오에서는 응용 프로그램 개발자가 중복 메시지 배달을 처리하는 논리를 응용 프로그램에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2e97-142">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span></span> <span data-ttu-id="f2e97-143">이 경우 대체로 배달 시도 간에 일정하게 유지되는 메시지의 **MessageId** 속성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f2e97-143">This is often achieved using the **MessageId** property of the message, which will remain constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f2e97-144">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f2e97-144">Next steps</span></span>
<span data-ttu-id="f2e97-145">이제 Service Bus 큐의 기본 사항을 익혔으므로 다음 문서를 따라 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="f2e97-145">Now that you have learned the basics of Service Bus queues, see these articles to learn more.</span></span>

* <span data-ttu-id="f2e97-146">[큐, 토픽 및 구독][Queues, topics, and subscriptions]</span><span class="sxs-lookup"><span data-stu-id="f2e97-146">[Queues, topics, and subscriptions][Queues, topics, and subscriptions]</span></span>

[Azure portal]: https://portal.azure.com
[Python Azure Service Bus package]: https://pypi.python.org/pypi/azure-servicebus  
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[Service Bus quotas]: service-bus-quotas.md


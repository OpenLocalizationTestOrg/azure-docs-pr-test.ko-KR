---
title: "Ruby와 aaaHow toouse Azure 서비스 버스 큐 | Microsoft Docs"
description: "Azure에서 서비스 버스 toouse 큐 대기 하는 방법에 대해 알아봅니다. 코드 샘플은 Ruby로 작성되었습니다."
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
ms.openlocfilehash: 7270154583f98e3372e82efbb967ea7a5acd1686
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-ruby"></a><span data-ttu-id="7d475-104">Ruby와 toouse 서비스 버스 큐 대기 하는 방법</span><span class="sxs-lookup"><span data-stu-id="7d475-104">How toouse Service Bus queues with Ruby</span></span>

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="7d475-105">이 가이드에서는 설명 방법을 toouse 서비스 버스 큐입니다.</span><span class="sxs-lookup"><span data-stu-id="7d475-105">This guide describes how toouse Service Bus queues.</span></span> <span data-ttu-id="7d475-106">hello 샘플 Ruby 작성 되 고 Azure 보석 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d475-106">hello samples are written in Ruby and use hello Azure gem.</span></span> <span data-ttu-id="7d475-107">hello 가이드에서 다루는 시나리오 포함 **메시지 송신 및 수신 큐를 만드는**, 및 **큐 삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="7d475-107">hello scenarios covered include **creating queues, sending and receiving messages**, and **deleting queues**.</span></span> <span data-ttu-id="7d475-108">서비스 버스 큐에 대 한 자세한 내용은 참조 hello [다음 단계](#next-steps) 섹션.</span><span class="sxs-lookup"><span data-stu-id="7d475-108">For more information about Service Bus queues, see hello [Next Steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]
   
[!INCLUDE [service-bus-ruby-setup](../../includes/service-bus-ruby-setup.md)]

## <a name="how-toocreate-a-queue"></a><span data-ttu-id="7d475-109">어떻게 toocreate 큐</span><span class="sxs-lookup"><span data-stu-id="7d475-109">How toocreate a queue</span></span>
<span data-ttu-id="7d475-110">hello **Azure::ServiceBusService** 개체를 사용 하면 큐와 toowork 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d475-110">hello **Azure::ServiceBusService** object enables you toowork with queues.</span></span> <span data-ttu-id="7d475-111">toocreate 큐를 사용 하 여 hello `create_queue()` 메서드.</span><span class="sxs-lookup"><span data-stu-id="7d475-111">toocreate a queue, use hello `create_queue()` method.</span></span> <span data-ttu-id="7d475-112">hello 다음 예제에서는 큐를 만듭니다 또는 모든 오류를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d475-112">hello following example creates a queue or prints out any errors.</span></span>

```ruby
azure_service_bus_service = Azure::ServiceBus::ServiceBusService.new(sb_host, { signer: signer})
begin
  queue = azure_service_bus_service.create_queue("test-queue")
rescue
  puts $!
end
```

<span data-ttu-id="7d475-113">전달할 수도 있습니다는 **Azure::ServiceBus::Queue** 메시지 시간 toolive 또는 최대 큐 크기 같은 toooverride hello 기본 큐 설정 수 있는 추가 옵션이 포함 된 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="7d475-113">You can also pass a **Azure::ServiceBus::Queue** object with additional options, which enables you toooverride hello default queue settings, such as message time toolive or maximum queue size.</span></span> <span data-ttu-id="7d475-114">다음 예제는 hello tooset 최대 큐 크기 too5 GB hello 방법과 toolive too1 분 시간을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7d475-114">hello following example shows how tooset hello maximum queue size too5 GB and time toolive too1 minute:</span></span>

```ruby
queue = Azure::ServiceBus::Queue.new("test-queue")
queue.max_size_in_megabytes = 5120
queue.default_message_time_to_live = "PT1M"

queue = azure_service_bus_service.create_queue(queue)
```

## <a name="how-toosend-messages-tooa-queue"></a><span data-ttu-id="7d475-115">Toosend 메시지 큐가 tooa 방법</span><span class="sxs-lookup"><span data-stu-id="7d475-115">How toosend messages tooa queue</span></span>
<span data-ttu-id="7d475-116">메시지 tooa 서비스 버스 큐 toosend 응용 프로그램 호출 hello `send_queue_message()` 메서드 hello **Azure::ServiceBusService** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="7d475-116">toosend a message tooa Service Bus queue, your application calls hello `send_queue_message()` method on hello **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="7d475-117">너무 (보내고 받은에서) 서비스 버스 큐는 메시지 **Azure::ServiceBus::BrokeredMessage** 개체, 및 표준 속성 집합이 있습니다 (같은 `label` 및 `time_to_live`), 사용 되는 toohold 사전 사용자 지정 응용 프로그램 관련 속성 및 임의 응용 프로그램 데이터의 본문입니다.</span><span class="sxs-lookup"><span data-stu-id="7d475-117">Messages sent too(and received from) Service Bus queues are **Azure::ServiceBus::BrokeredMessage** objects, and have a set of standard properties (such as `label` and `time_to_live`), a dictionary that is used toohold custom application-specific properties, and a body of arbitrary application data.</span></span> <span data-ttu-id="7d475-118">응용 프로그램 hello 메시지와 문자열 값을 전달 하 여 hello hello 메시지 본문을 설정할 수 있습니다 및 모든 필수 표준 속성은 기본 값으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="7d475-118">An application can set hello body of hello message by passing a string value as hello message and any required standard properties are populated with default values.</span></span>

<span data-ttu-id="7d475-119">hello 다음 예제에서는 toosend toohello 큐 테스트 메시지의 이름을 지정 방법 `test-queue` 를 사용 하 여 `send_queue_message()`:</span><span class="sxs-lookup"><span data-stu-id="7d475-119">hello following example demonstrates how toosend a test message toohello queue named `test-queue` using `send_queue_message()`:</span></span>

```ruby
message = Azure::ServiceBus::BrokeredMessage.new("test queue message")
message.correlation_id = "test-correlation-id"
azure_service_bus_service.send_queue_message("test-queue", message)
```

<span data-ttu-id="7d475-120">서비스 버스 큐 최대 메시지 크기는 256KB hello 지원 [표준 계층](service-bus-premium-messaging.md) 및 hello에서 1 MB [Premium 계층](service-bus-premium-messaging.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7d475-120">Service Bus queues support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="7d475-121">hello 표준 및 사용자 지정 응용 프로그램 속성을 포함 하는 hello 헤더는 64KB의 최대 크기를 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d475-121">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="7d475-122">큐에 유지 하는 메시지의 hello 수를 제한 하지 않으며 cap hello 총 크기는 큐에서 대기 하는 hello 메시지에입니다.</span><span class="sxs-lookup"><span data-stu-id="7d475-122">There is no limit on hello number of messages held in a queue but there is a cap on hello total size of hello messages held by a queue.</span></span> <span data-ttu-id="7d475-123">이 큐 크기는 생성 시 정의되며 상한이 5GB입니다.</span><span class="sxs-lookup"><span data-stu-id="7d475-123">This queue size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="how-tooreceive-messages-from-a-queue"></a><span data-ttu-id="7d475-124">큐에서 메시지를 tooreceive 방법</span><span class="sxs-lookup"><span data-stu-id="7d475-124">How tooreceive messages from a queue</span></span>
<span data-ttu-id="7d475-125">Hello를 사용 하 여 큐에서 메시지가 수신 되 `receive_queue_message()` 메서드 hello **Azure::ServiceBusService** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="7d475-125">Messages are received from a queue using hello `receive_queue_message()` method on hello **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="7d475-126">기본적으로 메시지는 읽고 hello 큐에서 삭제 되지 않고 잠겨 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d475-126">By default, messages are read and locked without being deleted from hello queue.</span></span> <span data-ttu-id="7d475-127">그러나에서 삭제할 수 있습니다 메시지 큐 hello hello 설정 하 여 읽어 `:peek_lock` 옵션**false**합니다.</span><span class="sxs-lookup"><span data-stu-id="7d475-127">However, you can delete messages from hello queue as they are read by setting hello `:peek_lock` option too**false**.</span></span>

<span data-ttu-id="7d475-128">hello 기본 동작을 사용 하면 hello 읽기 및 삭제는 2 단계 작업을 사용 하면 누락 된 메시지를 허용할 수 없는 가능한 toosupport 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="7d475-128">hello default behavior makes hello reading and deleting a two-stage operation, which also makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="7d475-129">서비스 버스 요청을 받으면 다음 메시지 toobe hello 사용 다른 소비자가 수신할 tooprevent 잠근 하 고 toohello 응용 프로그램 반환 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="7d475-129">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="7d475-130">Hello hello의 두 번째 단계를 완료 hello 응용 프로그램 hello 메시지 처리를 완료 (또는 이후 처리를 위해 안정적으로 저장) 한 후 호출 하 여 수신 프로세스 `delete_queue_message()` 메서드와 hello 메시지 toobe 삭제 매개 변수로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d475-130">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling `delete_queue_message()` method and providing hello message toobe deleted as a parameter.</span></span> <span data-ttu-id="7d475-131">hello `delete_queue_message()` 메서드 hello 메시지를 사용 되 고 표시 하 고 hello 큐에서 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d475-131">hello `delete_queue_message()` method will mark hello message as being consumed and remove it from hello queue.</span></span>

<span data-ttu-id="7d475-132">경우 hello `:peek_lock` 매개 변수가 너무 설정 된**false**, 읽기 및 hello 가장 간단한 모델 hello 메시지를 삭제 되며 시나리오는 응용 프로그램의 hello 이벤트에서 메시지를 처리 하지 않아도 안전한 수에 가장 적합 한 오류가 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="7d475-132">If hello `:peek_lock` parameter is set too**false**, reading and deleting hello message becomes hello simplest model, and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="7d475-133">toounderstand hello는 hello 소비자 문제에 요청을 수신 하는 시나리오 및 후 처리 하기 전에 크래시 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d475-133">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="7d475-134">서비스 버스에 hello 메시지 hello 응용 프로그램 다시 시작 되 고 메시지 사용을 시작 하는 경우 사용 되는 것으로 표시 하기 때문에 누락 됩니다 hello 메시지 했던 이전 toohello 크래시를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d475-134">Because Service Bus has marked hello message as being consumed, when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="7d475-135">hello 다음 예제에서는 tooreceive 및 프로세스 메시지 방법을 사용 하 여 `receive_queue_message()`합니다.</span><span class="sxs-lookup"><span data-stu-id="7d475-135">hello following example demonstrates how tooreceive and process messages using `receive_queue_message()`.</span></span> <span data-ttu-id="7d475-136">hello 예제에서 먼저 수신 하 고 사용 하 여 메시지를 삭제 `:peek_lock` 도**false**다음 다른 메시지를 수신 하 고 다음 삭제 hello 메시지를 사용 하 여 `delete_queue_message()`:</span><span class="sxs-lookup"><span data-stu-id="7d475-136">hello example first receives and deletes a message by using `:peek_lock` set too**false**, then it receives another message and then deletes hello message using `delete_queue_message()`:</span></span>

```ruby
message = azure_service_bus_service.receive_queue_message("test-queue",
  { :peek_lock => false })
message = azure_service_bus_service.receive_queue_message("test-queue")
azure_service_bus_service.delete_queue_message(message)
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="7d475-137">Toohandle 응용 프로그램이 크래시 되는 방법 및 읽을 수 없는 메시지</span><span class="sxs-lookup"><span data-stu-id="7d475-137">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="7d475-138">서비스 버스 기능 toohelp 정상적으로 응용 프로그램 또는 메시지를 처리 하는 데 문제가 오류 로부터 복구를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d475-138">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="7d475-139">수신기 응용 프로그램 수 없는 경우 몇 가지 이유로 tooprocess 환영 메시지가 다음 hello 호출할 수 있는 `unlock_queue_message()` 메서드 hello **Azure::ServiceBusService** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="7d475-139">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlock_queue_message()` method on hello **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="7d475-140">이 호출으로 인해 서비스 버스 toounlock hello hello 큐 내에서 메시지와 수신, 다시 사용할 수 있는 toobe 확인 하거나으로 hello를 많이 사용 응용 프로그램 또는 다른 소비 응용 프로그램에서 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d475-140">This call causes Service Bus toounlock hello message within hello queue and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="7d475-141">또한 hello 큐 내에서 잠긴 메시지와 관련 된 제한 시간 집합과 hello 응용 프로그램 실패 하기 전에 hello 메시지 tooprocess hello 잠금 제한 시간이 만료 (예를 들어 hello 응용 프로그램이 충돌할 경우), 서비스 버스 hello 메시지의 잠금을 해제 한 다음 자동으로 수신 다시 사용할 수 있는 toobe로 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d475-141">There is also a timeout associated with a message locked within hello queue, and if hello application fails tooprocess hello message before hello lock timeout expires (for example, if hello application crashes), then Service Bus unlocks hello message automatically and makes it available toobe received again.</span></span>

<span data-ttu-id="7d475-142">Hello hello 응용 프로그램 이벤트 충돌 hello 메시지 처리 전후에 그러나 hello 전에 `delete_queue_message()` 메서드는 다음 다시 시작할 때 hello 메시지는 다시 전달한 toohello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="7d475-142">In hello event that hello application crashes after processing hello message but before hello `delete_queue_message()` method is called, then hello message is redelivered toohello application when it restarts.</span></span> <span data-ttu-id="7d475-143">이 프로세스를 일반적으로 라고 *일단 처리 이상*; 즉, 각 메시지가 최소 한 번 처리 되지만 특정 상황 hello에 동일한 메시지를 다시 배달 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d475-143">This process is often called *At Least Once Processing*; that is, each message is processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="7d475-144">Hello 시나리오 중복 처리가 허용 되지 않는, 응용 프로그램 개발자가 추가 논리 tootheir 응용 프로그램을 toohandle 중복 메시지 배달을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d475-144">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="7d475-145">이 대개 달성 hello를 사용 하 여 `message_id` 배달 시도 간에 일정 하 게 유지 하는 hello 메시지의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="7d475-145">This is often achieved using hello `message_id` property of hello message, which remains constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7d475-146">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7d475-146">Next steps</span></span>
<span data-ttu-id="7d475-147">서비스 버스 큐의 hello 기본 사항 학습 한, 했으므로 이러한 링크 toolearn 자세한 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d475-147">Now that you've learned hello basics of Service Bus queues, follow these links toolearn more.</span></span>

* <span data-ttu-id="7d475-148">[큐, 토픽 및 구독](service-bus-queues-topics-subscriptions.md) 개요.</span><span class="sxs-lookup"><span data-stu-id="7d475-148">Overview of [queues, topics, and subscriptions](service-bus-queues-topics-subscriptions.md).</span></span>
* <span data-ttu-id="7d475-149">Hello 방문 [Ruby 용 Azure SDK](https://github.com/Azure/azure-sdk-for-ruby) GitHub의 리포지토리 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d475-149">Visit hello [Azure SDK for Ruby](https://github.com/Azure/azure-sdk-for-ruby) repository on GitHub.</span></span>

<span data-ttu-id="7d475-150">이 문서에서 설명 하는 hello Azure 서비스 버스 큐 및 hello에서 설명 하는 Azure 큐 간의 비교에 대 한 [어떻게 toouse Ruby에서 큐 저장소](../storage/queues/storage-ruby-how-to-use-queue-storage.md) 문서를 참조 하십시오. [Azure 큐 및 Azure 서비스 버스 큐-비교 및 대조](service-bus-azure-and-service-bus-queues-compared-contrasted.md)</span><span class="sxs-lookup"><span data-stu-id="7d475-150">For a comparison between hello Azure Service Bus queues discussed in this article and Azure Queues discussed in hello [How toouse Queue storage from Ruby](../storage/queues/storage-ruby-how-to-use-queue-storage.md) article, see [Azure Queues and Azure Service Bus Queues - Compared and Contrasted](service-bus-azure-and-service-bus-queues-compared-contrasted.md)</span></span>


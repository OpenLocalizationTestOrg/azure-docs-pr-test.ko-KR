---
title: "python aaaHow toouse Azure 서비스 버스 큐 | Microsoft Docs"
description: "Python에서 toouse Azure 서비스 버스 큐 대기 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: bceb84d04ff3445c3087a9c246c583d6630f07af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-python"></a><span data-ttu-id="66884-103">Python toouse 서비스 버스 큐 대기 하는 방법</span><span class="sxs-lookup"><span data-stu-id="66884-103">How toouse Service Bus queues with Python</span></span>

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="66884-104">이 문서에서는 설명 방법을 toouse 서비스 버스 큐입니다.</span><span class="sxs-lookup"><span data-stu-id="66884-104">This article describes how toouse Service Bus queues.</span></span> <span data-ttu-id="66884-105">hello 샘플 Python에서 작성 되 고 hello를 사용 하 여 [Python Azure 서비스 버스 패키지][Python Azure Service Bus package]합니다.</span><span class="sxs-lookup"><span data-stu-id="66884-105">hello samples are written in Python and use hello [Python Azure Service Bus package][Python Azure Service Bus package].</span></span> <span data-ttu-id="66884-106">hello 가이드에서 다루는 시나리오 포함 **메시지 송신 및 수신 큐를 만드는**, 및 **큐 삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="66884-106">hello scenarios covered include **creating queues, sending and receiving messages**, and **deleting queues**.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

> [!NOTE]
> <span data-ttu-id="66884-107">Python 또는 hello tooinstall [Python Azure 서비스 버스 패키지][Python Azure Service Bus package], hello 참조 [Python 설치 가이드](../python-how-to-install.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="66884-107">tooinstall Python or hello [Python Azure Service Bus package][Python Azure Service Bus package], see hello [Python Installation Guide](../python-how-to-install.md).</span></span>
> 
> 

## <a name="create-a-queue"></a><span data-ttu-id="66884-108">큐 만들기</span><span class="sxs-lookup"><span data-stu-id="66884-108">Create a queue</span></span>
<span data-ttu-id="66884-109">hello **ServiceBusService** 개체를 사용 하면 큐와 toowork 합니다.</span><span class="sxs-lookup"><span data-stu-id="66884-109">hello **ServiceBusService** object enables you toowork with queues.</span></span> <span data-ttu-id="66884-110">서비스 버스 tooprogrammatically 액세스 원하는 모든 Python 파일의 hello 맨 위 근처 코드 다음 hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="66884-110">Add hello following code near hello top of any Python file in which you wish tooprogrammatically access Service Bus:</span></span>

```python
from azure.servicebus import ServiceBusService, Message, Queue
```

<span data-ttu-id="66884-111">hello 다음 코드에서는 **ServiceBusService** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="66884-111">hello following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="66884-112">`mynamespace`, `sharedaccesskeyname` 및 `sharedaccesskey`를 네임스페이스, SAS(공유 액세스 서명) 키 이름 및 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="66884-112">Replace `mynamespace`, `sharedaccesskeyname`, and `sharedaccesskey` with your namespace, shared access signature (SAS) key name, and value.</span></span>

```python
bus_service = ServiceBusService(
    service_namespace='mynamespace',
    shared_access_key_name='sharedaccesskeyname',
    shared_access_key_value='sharedaccesskey')
```

<span data-ttu-id="66884-113">hello hello SAS 키 이름 및 값에 대 한 값에서에서 확인할 수 있습니다 hello [Azure 포털] [ Azure portal] 연결 정보 또는 Visual Studio hello **속성** 창을 선택 하는 경우 서버 탐색기에서 서비스 버스 네임 스페이스를 hello (같이 hello 이전 섹션에서).</span><span class="sxs-lookup"><span data-stu-id="66884-113">hello values for hello SAS key name and value can be found in hello [Azure portal][Azure portal] connection information, or in hello Visual Studio **Properties** pane when selecting hello Service Bus namespace in Server Explorer (as shown in hello previous section).</span></span>

```python
bus_service.create_queue('taskqueue')
```

<span data-ttu-id="66884-114">hello `create_queue` 메서드는 또한 메시지 toolive TTL (time) 또는 최대 큐 크기와 같은 toooverride 기본 큐 설정을 사용할 수 있는 추가 옵션을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="66884-114">hello `create_queue` method also supports additional options, which enable you toooverride default queue settings such as message time toolive (TTL) or maximum queue size.</span></span> <span data-ttu-id="66884-115">hello 다음 예제에서는 설정 hello 최대 큐 크기 too5 증가 하 고 hello TTL 값 too1 분:</span><span class="sxs-lookup"><span data-stu-id="66884-115">hello following example sets hello maximum queue size too5 GB, and hello TTL value too1 minute:</span></span>

```python
queue_options = Queue()
queue_options.max_size_in_megabytes = '5120'
queue_options.default_message_time_to_live = 'PT1M'

bus_service.create_queue('taskqueue', queue_options)
```

## <a name="send-messages-tooa-queue"></a><span data-ttu-id="66884-116">송신 메시지 tooa 큐</span><span class="sxs-lookup"><span data-stu-id="66884-116">Send messages tooa queue</span></span>
<span data-ttu-id="66884-117">메시지 tooa 서비스 버스 큐 toosend 응용 프로그램 호출 hello `send_queue_message` 메서드 hello **ServiceBusService** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="66884-117">toosend a message tooa Service Bus queue, your application calls hello `send_queue_message` method on hello **ServiceBusService** object.</span></span>

<span data-ttu-id="66884-118">hello 다음 예제에서는 toosend toohello 큐 테스트 메시지의 이름을 지정 방법 `taskqueue` 를 사용 하 여 `send_queue_message`:</span><span class="sxs-lookup"><span data-stu-id="66884-118">hello following example demonstrates how toosend a test message toohello queue named `taskqueue` using `send_queue_message`:</span></span>

```python
msg = Message(b'Test Message')
bus_service.send_queue_message('taskqueue', msg)
```

<span data-ttu-id="66884-119">서비스 버스 큐 최대 메시지 크기는 256KB hello 지원 [표준 계층](service-bus-premium-messaging.md) 및 hello에서 1 MB [Premium 계층](service-bus-premium-messaging.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="66884-119">Service Bus queues support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="66884-120">hello 표준 및 사용자 지정 응용 프로그램 속성을 포함 하는 hello 헤더는 64KB의 최대 크기를 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66884-120">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="66884-121">큐에 유지 하는 메시지의 hello 수를 제한 하지 않으며 cap hello 총 크기는 큐에서 대기 하는 hello 메시지에입니다.</span><span class="sxs-lookup"><span data-stu-id="66884-121">There is no limit on hello number of messages held in a queue but there is a cap on hello total size of hello messages held by a queue.</span></span> <span data-ttu-id="66884-122">이 큐 크기는 생성 시 정의되며 상한이 5GB입니다.</span><span class="sxs-lookup"><span data-stu-id="66884-122">This queue size is defined at creation time, with an upper limit of 5 GB.</span></span> <span data-ttu-id="66884-123">할당량에 대한 자세한 내용은 [Service Bus 할당량][Service Bus quotas]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="66884-123">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="66884-124">큐에서 메시지 받기</span><span class="sxs-lookup"><span data-stu-id="66884-124">Receive messages from a queue</span></span>
<span data-ttu-id="66884-125">Hello를 사용 하 여 큐에서 메시지가 수신 되 `receive_queue_message` 메서드 hello **ServiceBusService** 개체:</span><span class="sxs-lookup"><span data-stu-id="66884-125">Messages are received from a queue using hello `receive_queue_message` method on hello **ServiceBusService** object:</span></span>

```python
msg = bus_service.receive_queue_message('taskqueue', peek_lock=False)
print(msg.body)
```

<span data-ttu-id="66884-126">읽어 때 hello 큐에서 메시지가 삭제 되도록 hello 매개 변수 `peek_lock` 너무 설정**False**합니다.</span><span class="sxs-lookup"><span data-stu-id="66884-126">Messages are deleted from hello queue as they are read when hello parameter `peek_lock` is set too**False**.</span></span> <span data-ttu-id="66884-127">(미리 보기)를 읽을 수 있으며 hello 매개 변수를 설정 하 여 hello 큐에서 삭제 하지 않고 hello 메시지 잠금 `peek_lock` 너무**True**합니다.</span><span class="sxs-lookup"><span data-stu-id="66884-127">You can read (peek) and lock hello message without deleting it from hello queue by setting hello parameter `peek_lock` too**True**.</span></span>

<span data-ttu-id="66884-128">읽기의 동작은 hello 및 hello의 일부 수신 작업으로 hello 메시지를 삭제 합니다.는 hello 간단한 모델 시나리오는 응용 프로그램 실패 하는 hello 이벤트의 메시지를 처리 하지 않아도 안전한 수에 가장 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="66884-128">hello behavior of reading and deleting hello message as part of hello receive operation is hello simplest model, and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="66884-129">toounderstand hello는 hello 소비자 문제에 요청을 수신 하는 시나리오 및 후 처리 하기 전에 크래시 합니다.</span><span class="sxs-lookup"><span data-stu-id="66884-129">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="66884-130">서비스 버스 사용 되는 것을 다음 hello 응용 프로그램 다시 시작 되 고 메시지 사용을 시작할 때 hello 메시지를 표시 한 됩니다, 때문에 누락 됩니다 hello 메시지 했던 이전 toohello 크래시를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="66884-130">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="66884-131">경우 hello `peek_lock` 매개 변수가 너무 설정 된**True**, hello 수신 하므로 누락 된 메시지를 허용할 수 없는 가능한 toosupport 응용 프로그램 2 단계 작업이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="66884-131">If hello `peek_lock` parameter is set too**True**, hello receive becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="66884-132">서비스 버스 요청을 받으면 다음 메시지 toobe hello 사용 다른 소비자가 수신할 tooprevent 잠근 하 고 toohello 응용 프로그램 반환 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="66884-132">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="66884-133">Hello hello의 두 번째 단계를 완료 hello 응용 프로그램 hello 메시지 처리를 완료 (또는 이후 처리를 위해 안정적으로 저장) 한 후 hello를 호출 하 여 수신 프로세스 **삭제** 메서드 hello **메시지** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="66884-133">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling hello **delete** method on hello **Message** object.</span></span> <span data-ttu-id="66884-134">hello **삭제** 메서드 hello 메시지를 사용 되 고 표시 하 고 hello 큐에서 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="66884-134">hello **delete** method will mark hello message as being consumed and remove it from hello queue.</span></span>

```python
msg = bus_service.receive_queue_message('taskqueue', peek_lock=True)
print(msg.body)

msg.delete()
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="66884-135">Toohandle 응용 프로그램이 크래시 되는 방법 및 읽을 수 없는 메시지</span><span class="sxs-lookup"><span data-stu-id="66884-135">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="66884-136">서비스 버스 기능 toohelp 정상적으로 응용 프로그램 또는 메시지를 처리 하는 데 문제가 오류 로부터 복구를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="66884-136">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="66884-137">수신기 응용 프로그램 수 없는 경우 몇 가지 이유로 tooprocess 환영 메시지가 다음 hello 호출할 수 있는 **잠금 해제** 메서드 hello **메시지** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="66884-137">If a receiver application is unable tooprocess hello message for some reason, then it can call hello **unlock** method on hello **Message** object.</span></span> <span data-ttu-id="66884-138">Hello 큐 내에서 서비스 버스 toounlock hello 메시지 시키며 수신 다시 사용할 수 있는 toobe 확인, 사용자가 여를 많이 사용 응용 프로그램 또는 다른 소비 응용 프로그램에서 동일한 hello 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="66884-138">This will cause Service Bus toounlock hello message within hello queue and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="66884-139">또한 hello 큐 내에서 잠긴 메시지와 관련 된 제한 시간 집합과 tooprocess hello 메시지 하기 전에 hello 응용 프로그램 실패 hello 잠금 제한 시간이 만료 (예: hello 응용 프로그램이 충돌할 경우), 서비스 버스는 hello 메시지 잠금을 자동으로 해제 한 다음 사용할 수 있는 toobe 수신 다시 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="66884-139">There is also a timeout associated with a message locked within hello queue, and if hello application fails tooprocess hello message before hello lock timeout expires (e.g., if hello application crashes), then Service Bus will unlock hello message automatically and make it available toobe received again.</span></span>

<span data-ttu-id="66884-140">Hello hello 응용 프로그램 이벤트 충돌 hello 메시지 처리 전후에 그러나 hello 전에 **삭제** 메서드는 다음 다시 시작할 때 hello 메시지 다시 전달한 toohello 응용 프로그램 됩니다.</span><span class="sxs-lookup"><span data-stu-id="66884-140">In hello event that hello application crashes after processing hello message but before hello **delete** method is called, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="66884-141">이 이라고 하는데 **일단 처리 이상**, 즉, 각 메시지가 최소 한 번 처리 되지만 특정 상황 hello에 동일한 메시지를 다시 배달 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66884-141">This is often called **At Least Once Processing**, that is, each message will be processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="66884-142">Hello 시나리오 중복 처리가 허용 되지 않는, 응용 프로그램 개발자가 추가 논리 tootheir 응용 프로그램을 toohandle 중복 메시지 배달을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66884-142">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="66884-143">이 대개 달성 hello를 사용 하 여 **MessageId** 배달 시도 간에 일정 남아 있는 hello 메시지의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="66884-143">This is often achieved using hello **MessageId** property of hello message, which will remain constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="66884-144">다음 단계</span><span class="sxs-lookup"><span data-stu-id="66884-144">Next steps</span></span>
<span data-ttu-id="66884-145">서비스 버스 큐의 hello 기본 사항을 파악 했으므로, 이제는 이러한 문서 toolearn 자세한를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="66884-145">Now that you have learned hello basics of Service Bus queues, see these articles toolearn more.</span></span>

* <span data-ttu-id="66884-146">[큐, 토픽 및 구독][Queues, topics, and subscriptions]</span><span class="sxs-lookup"><span data-stu-id="66884-146">[Queues, topics, and subscriptions][Queues, topics, and subscriptions]</span></span>

[Azure portal]: https://portal.azure.com
[Python Azure Service Bus package]: https://pypi.python.org/pypi/azure-servicebus  
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[Service Bus quotas]: service-bus-quotas.md


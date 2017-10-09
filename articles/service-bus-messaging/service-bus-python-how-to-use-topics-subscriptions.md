---
title: "python aaaHow toouse Azure 서비스 버스 주제 | Microsoft Docs"
description: "자세한 방법을 toouse Azure 서비스 버스 항목 및 Python에서 구독 합니다."
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
ms.openlocfilehash: 1171cbe8061bb3d73e2ce92ecc0cf45afae37054
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-python"></a><span data-ttu-id="93a8f-103">어떻게 toouse 서비스 버스 항목 및 구독 python</span><span class="sxs-lookup"><span data-stu-id="93a8f-103">How toouse Service Bus topics and subscriptions with Python</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="93a8f-104">이 문서에서는 설명 방법을 toouse 서비스 버스 항목 및 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="93a8f-104">This article describes how toouse Service Bus topics and subscriptions.</span></span> <span data-ttu-id="93a8f-105">hello 샘플 Python에서 작성 되 고 hello를 사용 하 여 [Azure Python SDK 패키지][Azure Python package]합니다.</span><span class="sxs-lookup"><span data-stu-id="93a8f-105">hello samples are written in Python and use hello [Azure Python SDK package][Azure Python package].</span></span> <span data-ttu-id="93a8f-106">hello 가이드에서 다루는 시나리오 포함 **항목 및 구독을 만드는**, **구독 필터를 만드는**, **tooa 부분 메시지를 보내는**, **받기 구독에서 메시지**, 및 **항목 및 구독을 삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="93a8f-106">hello scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages tooa topic**, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span> <span data-ttu-id="93a8f-107">항목 및 구독에 대 한 자세한 내용은 참조 hello [다음 단계](#next-steps) 섹션.</span><span class="sxs-lookup"><span data-stu-id="93a8f-107">For more information about topics and subscriptions, see hello [Next Steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

> [!NOTE] 
> <span data-ttu-id="93a8f-108">Python tooinstall 또는 hello 필요 하면 [Azure Python 패키지][Azure Python package], hello 참조 [Python 설치 가이드](../python-how-to-install.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="93a8f-108">If you need tooinstall Python or hello [Azure Python package][Azure Python package], see hello [Python Installation Guide](../python-how-to-install.md).</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="93a8f-109">토픽 만들기</span><span class="sxs-lookup"><span data-stu-id="93a8f-109">Create a topic</span></span>
<span data-ttu-id="93a8f-110">hello **ServiceBusService** 개체를 사용 하면 toowork 항목과 함께 합니다.</span><span class="sxs-lookup"><span data-stu-id="93a8f-110">hello **ServiceBusService** object enables you toowork with topics.</span></span> <span data-ttu-id="93a8f-111">서비스 버스 tooprogrammatically 액세스 원하는 모든 Python 파일의 hello 맨 위 근처에 hello 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="93a8f-111">Add hello following near hello top of any Python file in which you wish tooprogrammatically access Service Bus:</span></span>

```python
from azure.servicebus import ServiceBusService, Message, Topic, Rule, DEFAULT_RULE_NAME
```

<span data-ttu-id="93a8f-112">hello 다음 코드에서는 **ServiceBusService** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="93a8f-112">hello following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="93a8f-113">`mynamespace`, `sharedaccesskeyname` 및 `sharedaccesskey`를 실제 네임스페이스, SAS(공유 액세스 서명) 키 이름 및 키 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="93a8f-113">Replace `mynamespace`, `sharedaccesskeyname`, and `sharedaccesskey` with your actual namespace, Shared Access Signature (SAS) key name, and key value.</span></span>

```python
bus_service = ServiceBusService(
    service_namespace='mynamespace',
    shared_access_key_name='sharedaccesskeyname',
    shared_access_key_value='sharedaccesskey')
```

<span data-ttu-id="93a8f-114">Hello에서 hello SAS 키 이름에 대 한 hello 값 및 값을 얻을 수 있습니다 [Azure 포털][Azure portal]합니다.</span><span class="sxs-lookup"><span data-stu-id="93a8f-114">You can obtain hello values for hello SAS key name and value from hello [Azure portal][Azure portal].</span></span>

```python
bus_service.create_topic('mytopic')
```

<span data-ttu-id="93a8f-115">hello `create_topic` 메서드는 또한 메시지 시간 toolive 또는 최대 항목 크기와 같은 toooverride 기본 항목 설정을 사용할 수 있는 추가 옵션을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="93a8f-115">hello `create_topic` method also supports additional options, which enable you toooverride default topic settings such as message time toolive or maximum topic size.</span></span> <span data-ttu-id="93a8f-116">hello 다음 예제에서는 설정 hello 최대 항목 크기 too5 GB 인데 1 분의 시간 toolive (TTL) 값:</span><span class="sxs-lookup"><span data-stu-id="93a8f-116">hello following example sets hello maximum topic size too5 GB, and a time toolive (TTL) value of 1 minute:</span></span>

```python
topic_options = Topic()
topic_options.max_size_in_megabytes = '5120'
topic_options.default_message_time_to_live = 'PT1M'

bus_service.create_topic('mytopic', topic_options)
```

## <a name="create-subscriptions"></a><span data-ttu-id="93a8f-117">구독 만들기</span><span class="sxs-lookup"><span data-stu-id="93a8f-117">Create subscriptions</span></span>
<span data-ttu-id="93a8f-118">Hello로 만들어집니다 구독 tootopics **ServiceBusService** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="93a8f-118">Subscriptions tootopics are also created with hello **ServiceBusService** object.</span></span> <span data-ttu-id="93a8f-119">이름이 지정 된 구독과 hello toohello 구독의 가상 큐에 배달 된 메시지 집합을 제한 하는 선택적 필터가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93a8f-119">Subscriptions are named and can have an optional filter that restricts hello set of messages delivered toohello subscription's virtual queue.</span></span>

> [!NOTE]
> <span data-ttu-id="93a8f-120">구독 영구 tooexist 중 하나가 될 때까지 계속 사용 되며 또는 hello toowhich 항목은 구독, 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93a8f-120">Subscriptions are persistent and will continue tooexist until either they, or hello topic toowhich they are subscribed, are deleted.</span></span>
> 
> 

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a><span data-ttu-id="93a8f-121">Hello 기본 (MatchAll) 필터와 구독 만들기</span><span class="sxs-lookup"><span data-stu-id="93a8f-121">Create a subscription with hello default (MatchAll) filter</span></span>
<span data-ttu-id="93a8f-122">hello **MatchAll** 필터는 필터 지정 하지 않으면은 새 구독을 만들 때 사용 되는 hello 기본 필터.</span><span class="sxs-lookup"><span data-stu-id="93a8f-122">hello **MatchAll** filter is hello default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="93a8f-123">Hello 때 **MatchAll** 필터 사용 하는 경우 모든 부분 메시지 게시 된 toohello hello 구독의 가상 큐에 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93a8f-123">When hello **MatchAll** filter is used, all messages published toohello topic are placed in hello subscription's virtual queue.</span></span> <span data-ttu-id="93a8f-124">hello 다음 예제에서는 구독을 만드는 라는 `AllMessages` 사용 하 여 기본 hello 및 **MatchAll** 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="93a8f-124">hello following example creates a subscription named `AllMessages` and uses hello default **MatchAll** filter.</span></span>

```python
bus_service.create_subscription('mytopic', 'AllMessages')
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="93a8f-125">필터를 사용하여 구독 만들기</span><span class="sxs-lookup"><span data-stu-id="93a8f-125">Create subscriptions with filters</span></span>
<span data-ttu-id="93a8f-126">Toospecify tooa 항목에 특정 항목을 구독 내에서 표시 됩니다. 보낸 메시지 수 있도록 하는 필터를 정의할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93a8f-126">You can also define filters that enable you toospecify which messages sent tooa topic should show up within a specific topic subscription.</span></span>

<span data-ttu-id="93a8f-127">hello 가장 유연한 구독에서 지 원하는 필터 형식은 **SqlFilter**, SQL92의 하위 집합을 구현 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="93a8f-127">hello most flexible type of filter supported by subscriptions is a **SqlFilter**, which implements a subset of SQL92.</span></span> <span data-ttu-id="93a8f-128">SQL 필터가 있는 게시 된 toohello 항목 hello 메시지의 hello 속성에서 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="93a8f-128">SQL filters operate on hello properties of hello messages that are published toohello topic.</span></span> <span data-ttu-id="93a8f-129">SQL 필터와 함께 사용할 수 있는 hello 식에 대 한 자세한 내용은 참조 hello [SqlFilter.SqlExpression] [ SqlFilter.SqlExpression] 구문입니다.</span><span class="sxs-lookup"><span data-stu-id="93a8f-129">For more information about hello expressions that can be used with a SQL filter, see hello [SqlFilter.SqlExpression][SqlFilter.SqlExpression] syntax.</span></span>

<span data-ttu-id="93a8f-130">Hello를 사용 하 여 필터 tooa 구독을 추가 하려면 **만들\_규칙** hello 방식의 **ServiceBusService** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="93a8f-130">You can add filters tooa subscription by using hello **create\_rule** method of hello **ServiceBusService** object.</span></span> <span data-ttu-id="93a8f-131">이 방법을 사용 하면 tooadd 새 필터 tooan 기존 구독이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93a8f-131">This method allows you tooadd new filters tooan existing subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="93a8f-132">Hello 기본 필터를 자동으로 적용 되기 때문에 tooall 새 구독 hello 기본 필터 또는 hello를 먼저 제거 해야 **MatchAll** 지정할 수 있는 필터를 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="93a8f-132">Because hello default filter is applied automatically tooall new subscriptions, you must first remove hello default filter or hello **MatchAll** will override any other filters you may specify.</span></span> <span data-ttu-id="93a8f-133">Hello를 사용 하 여 hello 기본 규칙을 제거할 수 있습니다 `delete_rule` hello 방식의 **ServiceBusService** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="93a8f-133">You can remove hello default rule by using hello `delete_rule` method of hello **ServiceBusService** object.</span></span>
> 
> 

<span data-ttu-id="93a8f-134">hello 다음 예제에서는 구독을 만드는 라는 `HighMessages` 와 **SqlFilter** 만 사용자 지정 하는 메시지를 선택 하는 `messagenumber` 3 보다 큰 속성:</span><span class="sxs-lookup"><span data-stu-id="93a8f-134">hello following example creates a subscription named `HighMessages` with a **SqlFilter** that only selects messages that have a custom `messagenumber` property greater than 3:</span></span>

```python
bus_service.create_subscription('mytopic', 'HighMessages')

rule = Rule()
rule.filter_type = 'SqlFilter'
rule.filter_expression = 'messagenumber > 3'

bus_service.create_rule('mytopic', 'HighMessages', 'HighMessageFilter', rule)
bus_service.delete_rule('mytopic', 'HighMessages', DEFAULT_RULE_NAME)
```

<span data-ttu-id="93a8f-135">마찬가지로, hello 다음 예제에서는 구독을 만드는 라는 `LowMessages` 와 **SqlFilter** 만 설정 된 메시지를 선택 하는 `messagenumber` 속성 작은 보다 짧거나 too3:</span><span class="sxs-lookup"><span data-stu-id="93a8f-135">Similarly, hello following example creates a subscription named `LowMessages` with a **SqlFilter** that only selects messages that have a `messagenumber` property less than or equal too3:</span></span>

```python
bus_service.create_subscription('mytopic', 'LowMessages')

rule = Rule()
rule.filter_type = 'SqlFilter'
rule.filter_expression = 'messagenumber <= 3'

bus_service.create_rule('mytopic', 'LowMessages', 'LowMessageFilter', rule)
bus_service.delete_rule('mytopic', 'LowMessages', DEFAULT_RULE_NAME)
```

<span data-ttu-id="93a8f-136">이제 메시지를 보내면 너무`mytopic` 구독 tooreceivers toohello 항상 제공 된다는 **AllMessages** 항목 구독 및 구독 하는 선택적으로 배달 된 tooreceivers toohello **HighMessages**  및 **LowMessages** 주제 구독 (에 따라 hello 메시지 콘텐츠 포함).</span><span class="sxs-lookup"><span data-stu-id="93a8f-136">Now, when a message is sent too`mytopic` it is always delivered tooreceivers subscribed toohello **AllMessages** topic subscription, and selectively delivered tooreceivers subscribed toohello **HighMessages** and **LowMessages** topic subscriptions (depending on hello message content).</span></span>

## <a name="send-messages-tooa-topic"></a><span data-ttu-id="93a8f-137">Tooa 부분 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="93a8f-137">Send messages tooa topic</span></span>
<span data-ttu-id="93a8f-138">메시지 tooa 서비스 버스 항목 toosend 응용 프로그램 hello를 사용 해야 `send_topic_message` hello 방식의 **ServiceBusService** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="93a8f-138">toosend a message tooa Service Bus topic, your application must use hello `send_topic_message` method of hello **ServiceBusService** object.</span></span>

<span data-ttu-id="93a8f-139">hello 다음 예제에서는 5 toosend 테스트 너무 메시지 방법을`mytopic`합니다.</span><span class="sxs-lookup"><span data-stu-id="93a8f-139">hello following example demonstrates how toosend five test messages too`mytopic`.</span></span> <span data-ttu-id="93a8f-140">해당 hello 참고 `messagenumber` hello 루프의 반복 hello에 각 메시지의 속성 값 달라 집니다 (결정 구독 받는):</span><span class="sxs-lookup"><span data-stu-id="93a8f-140">Note that hello `messagenumber` property value of each message varies on hello iteration of hello loop (this determines which subscriptions receive it):</span></span>

```python
for i in range(5):
    msg = Message('Msg {0}'.format(i).encode('utf-8'), custom_properties={'messagenumber':i})
    bus_service.send_topic_message('mytopic', msg)
```

<span data-ttu-id="93a8f-141">서비스 버스 주제 hello에서 최대 메시지 크기는 256KB 지원 [표준 계층](service-bus-premium-messaging.md) 및 hello에서 1 MB [Premium 계층](service-bus-premium-messaging.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="93a8f-141">Service Bus topics support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="93a8f-142">hello 표준 및 사용자 지정 응용 프로그램 속성을 포함 하는 hello 헤더는 64KB의 최대 크기를 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93a8f-142">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="93a8f-143">Hello 메시지에 항목을 보유할 수에 제한이 없음을 않으며 항목을 보유 하는 hello 메시지의 총 크기 hello 켜져 캡입니다.</span><span class="sxs-lookup"><span data-stu-id="93a8f-143">There is no limit on hello number of messages held in a topic but there is a cap on hello total size of hello messages held by a topic.</span></span> <span data-ttu-id="93a8f-144">이 토픽 크기는 생성 시 정의되며 상한이 5GB입니다.</span><span class="sxs-lookup"><span data-stu-id="93a8f-144">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span> <span data-ttu-id="93a8f-145">할당량에 대한 자세한 내용은 [Service Bus 할당량][Service Bus quotas]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="93a8f-145">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="93a8f-146">구독에서 메시지 받기</span><span class="sxs-lookup"><span data-stu-id="93a8f-146">Receive messages from a subscription</span></span>
<span data-ttu-id="93a8f-147">Hello를 사용 하 여 구독에서 메시지를 받을 `receive_subscription_message` 메서드 hello **ServiceBusService** 개체:</span><span class="sxs-lookup"><span data-stu-id="93a8f-147">Messages are received from a subscription using hello `receive_subscription_message` method on hello **ServiceBusService** object:</span></span>

```python
msg = bus_service.receive_subscription_message('mytopic', 'LowMessages', peek_lock=False)
print(msg.body)
```

<span data-ttu-id="93a8f-148">메시지를 읽고 때 hello 구독에서 삭제 됩니다 매개 변수를 hello `peek_lock` 너무 설정 되어**False**합니다.</span><span class="sxs-lookup"><span data-stu-id="93a8f-148">Messages are deleted from hello subscription as they are read when hello parameter `peek_lock` is set too**False**.</span></span> <span data-ttu-id="93a8f-149">(미리 보기)를 읽을 수 있으며 hello 매개 변수를 설정 하 여 hello 큐에서 삭제 하지 않고 hello 메시지 잠금 `peek_lock` 너무**True**합니다.</span><span class="sxs-lookup"><span data-stu-id="93a8f-149">You can read (peek) and lock hello message without deleting it from hello queue by setting hello parameter `peek_lock` too**True**.</span></span>

<span data-ttu-id="93a8f-150">읽기의 동작은 hello 및 hello의 일부 수신 작업으로 hello 메시지를 삭제 합니다.는 hello 간단한 모델 시나리오는 응용 프로그램 실패 하는 hello 이벤트의 메시지를 처리 하지 않아도 안전한 수에 가장 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="93a8f-150">hello behavior of reading and deleting hello message as part of hello receive operation is hello simplest model, and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="93a8f-151">toounderstand hello는 hello 소비자 문제에 요청을 수신 하는 시나리오 및 후 처리 하기 전에 크래시 합니다.</span><span class="sxs-lookup"><span data-stu-id="93a8f-151">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="93a8f-152">서비스 버스 사용 되는 것을 다음 hello 응용 프로그램 다시 시작 되 고 메시지 사용을 시작할 때 hello 메시지를 표시 한 됩니다, 때문에 누락 됩니다 hello 메시지 했던 이전 toohello 크래시를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="93a8f-152">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="93a8f-153">경우 hello `peek_lock` 매개 변수가 너무 설정 된**True**, hello 수신 하므로 누락 된 메시지를 허용할 수 없는 가능한 toosupport 응용 프로그램 2 단계 작업이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93a8f-153">If hello `peek_lock` parameter is set too**True**, hello receive becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="93a8f-154">서비스 버스 요청을 받으면 다음 메시지 toobe hello 사용 다른 소비자가 수신할 tooprevent 잠근 하 고 toohello 응용 프로그램 반환 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="93a8f-154">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="93a8f-155">Hello hello의 두 번째 단계를 완료 후 hello 응용 프로그램 hello 메시지 처리를 완료 (또는 이후 처리를 위해 안정적으로 저장)를 호출 하 여 수신 프로세스 `delete` hello에 대 한 메서드 **메시지** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="93a8f-155">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling `delete` method on hello **Message** object.</span></span> <span data-ttu-id="93a8f-156">hello `delete` 메서드 사용 되는 것 hello 메시지를 표시 하 고 hello 구독에서 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="93a8f-156">hello `delete` method marks hello message as being consumed and removes it from hello subscription.</span></span>

```python
msg = bus_service.receive_subscription_message('mytopic', 'LowMessages', peek_lock=True)
print(msg.body)

msg.delete()
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="93a8f-157">Toohandle 응용 프로그램이 크래시 되는 방법 및 읽을 수 없는 메시지</span><span class="sxs-lookup"><span data-stu-id="93a8f-157">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="93a8f-158">서비스 버스 기능 toohelp 정상적으로 응용 프로그램 또는 메시지를 처리 하는 데 문제가 오류 로부터 복구를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="93a8f-158">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="93a8f-159">수신기 응용 프로그램 수 없는 경우 몇 가지 이유로 tooprocess 환영 메시지가 다음 hello 호출할 수 있는 `unlock` 메서드 hello **메시지** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="93a8f-159">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlock` method on hello **Message** object.</span></span> <span data-ttu-id="93a8f-160">Hello 구독 내에서 서비스 버스 toounlock hello 메시지 시키며 수신 다시 사용할 수 있는 toobe 확인, 사용자가 여를 많이 사용 응용 프로그램 또는 다른 소비 응용 프로그램에서 동일한 hello 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="93a8f-160">This will cause Service Bus toounlock hello message within hello subscription and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="93a8f-161">또한 hello 구독 내에서 잠긴 메시지와 관련 된 제한 시간 집합과 hello 응용 프로그램 실패 하기 전에 hello 메시지 tooprocess hello 잠금 제한 시간이 만료 (예를 들어 hello 응용 프로그램이 충돌할 경우), 서비스 버스 hello 메시지의 잠금을 해제 한 다음 자동으로 수신 다시 사용할 수 있는 toobe로 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="93a8f-161">There is also a timeout associated with a message locked within hello subscription, and if hello application fails tooprocess hello message before hello lock timeout expires (for example, if hello application crashes), then Service Bus unlocks hello message automatically and makes it available toobe received again.</span></span>

<span data-ttu-id="93a8f-162">Hello hello 응용 프로그램 이벤트 충돌 hello 메시지 처리 전후에 그러나 hello 전에 `delete` 메서드는 다음 다시 시작할 때 hello 메시지 다시 전달한 toohello 응용 프로그램 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93a8f-162">In hello event that hello application crashes after processing hello message but before hello `delete` method is called, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="93a8f-163">이 이라고 하는데 *일단 처리 이상*, 즉, 각 메시지가 최소 한 번 처리 되지만 특정 상황 hello에 동일한 메시지를 다시 배달 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93a8f-163">This is often called *At Least Once Processing*, that is, each message will be processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="93a8f-164">Hello 시나리오 중복 처리가 허용 되지 않는, 응용 프로그램 개발자가 추가 논리 tootheir 응용 프로그램을 toohandle 중복 메시지 배달을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93a8f-164">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="93a8f-165">이 대개 달성 hello를 사용 하 여 **MessageId** 배달 시도 간에 일정 남아 있는 hello 메시지의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="93a8f-165">This is often achieved using hello **MessageId** property of hello message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="93a8f-166">토픽 및 구독 삭제</span><span class="sxs-lookup"><span data-stu-id="93a8f-166">Delete topics and subscriptions</span></span>
<span data-ttu-id="93a8f-167">항목과 구독은 영구적이 고 명시적으로 해야 hello 통해 삭제 [Azure 포털] [ Azure portal] 또는 프로그래밍 방식으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="93a8f-167">Topics and subscriptions are persistent, and must be explicitly deleted either through hello [Azure portal][Azure portal] or programmatically.</span></span> <span data-ttu-id="93a8f-168">hello 다음 예제에서는 toodelete hello 항목 이름을 지정 하는 방법 `mytopic`:</span><span class="sxs-lookup"><span data-stu-id="93a8f-168">hello following example shows how toodelete hello topic named `mytopic`:</span></span>

```python
bus_service.delete_topic('mytopic')
```

<span data-ttu-id="93a8f-169">항목을 삭제 하면 모든 구독에 등록 된 hello 항목을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="93a8f-169">Deleting a topic also deletes any subscriptions that are registered with hello topic.</span></span> <span data-ttu-id="93a8f-170">구독을 개별적으로 삭제할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93a8f-170">Subscriptions can also be deleted independently.</span></span> <span data-ttu-id="93a8f-171">hello 다음 코드를 보여 줍니다 방법과 toodelete 구독 이름 `HighMessages` hello에서 `mytopic` 항목:</span><span class="sxs-lookup"><span data-stu-id="93a8f-171">hello following code shows how toodelete a subscription named `HighMessages` from hello `mytopic` topic:</span></span>

```python
bus_service.delete_subscription('mytopic', 'HighMessages')
```

## <a name="next-steps"></a><span data-ttu-id="93a8f-172">다음 단계</span><span class="sxs-lookup"><span data-stu-id="93a8f-172">Next steps</span></span>
<span data-ttu-id="93a8f-173">서비스 버스 항목의 hello 기본 사항 학습 한, 했으므로 이러한 링크 toolearn 자세한 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="93a8f-173">Now that you've learned hello basics of Service Bus topics, follow these links toolearn more.</span></span>

* <span data-ttu-id="93a8f-174">[큐, 토픽 및 구독][Queues, topics, and subscriptions]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="93a8f-174">See [Queues, topics, and subscriptions][Queues, topics, and subscriptions].</span></span>
* <span data-ttu-id="93a8f-175">[SqlFilter.SqlExpression][SqlFilter.SqlExpression]에 대한 참조입니다.</span><span class="sxs-lookup"><span data-stu-id="93a8f-175">Reference for [SqlFilter.SqlExpression][SqlFilter.SqlExpression].</span></span>

[Azure portal]: https://portal.azure.com
[Azure Python package]: https://pypi.python.org/pypi/azure  
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter.SqlExpression]: service-bus-messaging-sql-filter.md
[Service Bus quotas]: service-bus-quotas.md 

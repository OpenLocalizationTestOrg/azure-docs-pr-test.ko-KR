---
title: "Azure 서비스 버스 큐, 토픽 및 구독을 메시징 aaaOverview | Microsoft Docs"
description: "서비스 버스 메시징 엔터티의 개요"
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a306ced4-74e9-47c6-990a-d9c47efa31d5
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: sethm
ms.openlocfilehash: 73135d2658e341c14dbb114ab938faed91578ff1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-queues-topics-and-subscriptions"></a><span data-ttu-id="a0107-103">Service Bus 큐, 토픽 및 구독</span><span class="sxs-lookup"><span data-stu-id="a0107-103">Service Bus queues, topics, and subscriptions</span></span>

<span data-ttu-id="a0107-104">Microsoft Azure Service Bus는 신뢰할 수 있는 메시지 큐 및 지속형 게시/구독 메시징을 포함하여 클라우드 기반, 메시지 지향 미들웨어 기술 집합을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-104">Microsoft Azure Service Bus supports a set of cloud-based, message-oriented middleware technologies including reliable message queuing and durable publish/subscribe messaging.</span></span> <span data-ttu-id="a0107-105">이러한 "브로커" 메시징 기능으로 분리 된 메시징 기능을 지원 게시-구독, 임시 분리 및 hello 서비스 버스 메시징 패브릭을 사용한 부하 분산 시나리오 생각할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-105">These "brokered" messaging capabilities can be thought of as decoupled messaging features that support publish-subscribe, temporal decoupling, and load balancing scenarios using hello Service Bus messaging fabric.</span></span> <span data-ttu-id="a0107-106">분리된 통신에는 많은 장점이 있습니다. 예를 들어 필요하면 클라이언트와 서버가 연결되고 비동기 방식으로 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-106">Decoupled communication has many advantages; for example, clients and servers can connect as needed and perform their operations in an asynchronous fashion.</span></span>

<span data-ttu-id="a0107-107">hello 메시징 기능에서 서비스 버스의 hello 핵심을 형성 하는 hello 메시징 엔터티는 큐, 항목 및 구독 및 규칙/작업 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-107">hello messaging entities that form hello core of hello messaging capabilities in Service Bus are queues, topics and subscriptions, and rules/actions.</span></span>

## <a name="queues"></a><span data-ttu-id="a0107-108">큐</span><span class="sxs-lookup"><span data-stu-id="a0107-108">Queues</span></span>

<span data-ttu-id="a0107-109">큐 제공 *첫 번째 In, First Out* (선출 FIFO) 메시지 배달 tooone 또는 자세한 경쟁 소비자입니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-109">Queues offer *First In, First Out* (FIFO) message delivery tooone or more competing consumers.</span></span> <span data-ttu-id="a0107-110">즉, 메시지는 일반적으로 예상된 toobe hello 수신기는 toohello 큐에 추가 된 각 메시지는 수신 처리 하며 하나의 메시지 소비자만 hello 순서에 의해 수신 및 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-110">That is, messages are typically expected toobe received and processed by hello receivers in hello order in which they were added toohello queue, and each message is received and processed by only one message consumer.</span></span> <span data-ttu-id="a0107-111">큐를 사용 하 여의 주요 이점은 tooachieve "임시 분리"을 응용 프로그램 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-111">A key benefit of using queues is tooachieve "temporal decoupling" of application components.</span></span> <span data-ttu-id="a0107-112">즉, 생산자 (보낸 사람) hello 및 소비자 (받는) 하지 않은 toobe 전송 및 메시지를 받을 hello에 동일한 메시지 hello 큐에 지속적으로 저장 되므로 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-112">In other words, hello producers (senders) and consumers (receivers) do not have toobe sending and receiving messages at hello same time, because messages are stored durably in hello queue.</span></span> <span data-ttu-id="a0107-113">또한 hello 생산자가 되지 toowait hello 소비자의 회신에 대 한에 순서 toocontinue tooprocess 있고 메시지를 보낼 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-113">Furthermore, hello producer does not have toowait for a reply from hello consumer in order toocontinue tooprocess and send messages.</span></span>

<span data-ttu-id="a0107-114">관련 된이 점으로 "부하 평준화" 생산자와 소비자 조정은 toosend 있고 서로 다른 속도로 메시지를 수신을 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-114">A related benefit is "load leveling," which enables producers and consumers toosend and receive messages at different rates.</span></span> <span data-ttu-id="a0107-115">많은 응용 프로그램에서 시스템 부하 hello 시간에 따라; 그러나 hello 처리에 필요한 각 작업 단위에 시간은 일반적으로 일정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-115">In many applications, hello system load varies over time; however, hello processing time required for each unit of work is typically constant.</span></span> <span data-ttu-id="a0107-116">여 메시지 생산자와 소비자를 큐에 응용 프로그램 에서만 사용 하는 hello에 toobe 프로 비전 된 toobe 수 toohandle 최고 부하가 아닌 평균 부하를 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-116">Intermediating message producers and consumers with a queue means that hello consuming application only has toobe provisioned toobe able toohandle average load instead of peak load.</span></span> <span data-ttu-id="a0107-117">증가 하 고 hello 수신 부하가 변경 됨에 따라 축소 하는 hello 큐의 hello 깊이입니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-117">hello depth of hello queue grows and contracts as hello incoming load varies.</span></span> <span data-ttu-id="a0107-118">이 관계 toohello 양의 인프라 필요한 tooservice hello 응용 프로그램 부하 money 직접 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-118">This directly saves money with regard toohello amount of infrastructure required tooservice hello application load.</span></span> <span data-ttu-id="a0107-119">Hello로 로드 증가, 작업자 프로세스가 더 추가 된 tooread hello 큐에서 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-119">As hello load increases, more worker processes can be added tooread from hello queue.</span></span> <span data-ttu-id="a0107-120">Hello 작업자 프로세스 중 하나에만 각 메시지를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-120">Each message is processed by only one of hello worker processes.</span></span> <span data-ttu-id="a0107-121">또한이 끌어오기 기반 부하 분산 하면 hello 작업자 컴퓨터의 최적 사용에 대 한 hello 작업자 컴퓨터 큰지에 tooprocessing 전원와 다른 경우에 자신의 최대 속도로 메시지를 가져올 때 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-121">Furthermore, this pull-based load balancing allows for optimum use of hello worker computers even if hello worker computers differ with regard tooprocessing power, as they will pull messages at their own maximum rate.</span></span> <span data-ttu-id="a0107-122">이 패턴을 "경쟁 소비자" 패턴 hello 종종 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-122">This pattern is often termed hello "competing consumer" pattern.</span></span>

<span data-ttu-id="a0107-123">메시지 생산자와 소비자 조정은 toointermediate 큐를 사용 하 여 hello 구성 요소 간의 기본적인 느슨한 결합을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-123">Using queues toointermediate between message producers and consumers provides an inherent loose coupling between hello components.</span></span> <span data-ttu-id="a0107-124">생산자와 소비자가 서로 인식 없기 때문에 hello 생산자에 영향을 주지 않고 소비자를 업그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-124">Because producers and consumers are not aware of each other, a consumer can be upgraded without having any effect on hello producer.</span></span>

<span data-ttu-id="a0107-125">큐 만들기는 여러 단계의 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-125">Creating a queue is a multi-step process.</span></span> <span data-ttu-id="a0107-126">서비스 버스 메시징 엔터티 (큐 및 토픽)를 통해 hello에 대 한 관리 작업을 수행할 [Microsoft.ServiceBus.NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) hello hello 서비스 버스의 기준 주소를 제공 하 여 생성 된 클래스 네임 스페이스 및 hello 사용자 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-126">You perform management operations for Service Bus messaging entities (both queues and topics) via hello [Microsoft.ServiceBus.NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) class, which is constructed by supplying hello base address of hello Service Bus namespace and hello user credentials.</span></span> <span data-ttu-id="a0107-127">[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) 메서드 toocreate 제공 열거 및 메시징 엔터티를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-127">[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) provides methods toocreate, enumerate and delete messaging entities.</span></span> <span data-ttu-id="a0107-128">만든 후는 [Microsoft.ServiceBus.TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#microsoft_servicebus_tokenprovider) 개체 hello SAS 이름 및 키 및 서비스 네임 스페이스 관리에서 개체를 hello를 사용할 수 있습니다 [Microsoft.ServiceBus.NamespaceManager.CreateQueue](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateQueue_System_String_) 메서드 toocreate hello 큐입니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-128">After creating a [Microsoft.ServiceBus.TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#microsoft_servicebus_tokenprovider) object from hello SAS name and key, and a service namespace management object, you can use hello [Microsoft.ServiceBus.NamespaceManager.CreateQueue](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateQueue_System_String_) method toocreate hello queue.</span></span> <span data-ttu-id="a0107-129">예:</span><span class="sxs-lookup"><span data-stu-id="a0107-129">For example:</span></span>

```csharp
// Create management credentials
TokenProvider credentials = TokenProvider.CreateSharedAccessSignatureTokenProvider(sasKeyName,sasKeyValue);
// Create namespace client
NamespaceManager namespaceClient = new NamespaceManager(ServiceBusEnvironment.CreateServiceUri("sb", ServiceNamespace, string.Empty), credentials);
```

<span data-ttu-id="a0107-130">인수로 서 서비스 버스 URI hello로 큐 개체와 메시징 팩터리 다음 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-130">You can then create a queue object and a messaging factory with hello Service Bus URI as an argument.</span></span> <span data-ttu-id="a0107-131">예:</span><span class="sxs-lookup"><span data-stu-id="a0107-131">For example:</span></span>

```csharp
QueueDescription myQueue;
myQueue = namespaceClient.CreateQueue("TestQueue");
MessagingFactory factory = MessagingFactory.Create(ServiceBusEnvironment.CreateServiceUri("sb", ServiceNamespace, string.Empty), credentials); 
QueueClient myQueueClient = factory.CreateQueueClient("TestQueue");
```

<span data-ttu-id="a0107-132">그런 다음 toohello 큐 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-132">You can then send messages toohello queue.</span></span> <span data-ttu-id="a0107-133">예를 들어, 라는 조정 된 메시지의 목록이 있는 경우 `MessageList`, hello 코드가 비슷한 toohello 다음 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-133">For example, if you have a list of brokered messages called `MessageList`, hello code appears similar toohello following:</span></span>

```csharp
for (int count = 0; count < 6; count++)
{
    var issue = MessageList[count];
    issue.Label = issue.Properties["IssueTitle"].ToString();
    myQueueClient.Send(issue);
}
```

<span data-ttu-id="a0107-134">그런 다음 메시지가 hello 큐에서 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-134">You then receive messages from hello queue as follows:</span></span>

```csharp
while ((message = myQueueClient.Receive(new TimeSpan(hours: 0, minutes: 0, seconds: 5))) != null)
    {
        Console.WriteLine(string.Format("Message received: {0}, {1}, {2}", message.SequenceNumber, message.Label, message.MessageId));
        message.Complete();

        Console.WriteLine("Processing message (sleeping...)");
        Thread.Sleep(1000);
    }
```

<span data-ttu-id="a0107-135">Hello에 [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode) 모드 hello 수신 작업은 1 단계 즉, 서비스 버스 hello 요청을 받으면 hello 메시지 사용 되는 것을 표시 하 고을 toohello 응용 프로그램을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-135">In hello [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, hello receive operation is single-shot; that is, when Service Bus receives hello request, it marks hello message as being consumed and returns it toohello application.</span></span> <span data-ttu-id="a0107-136">**ReceiveAndDelete** 모드는 hello 가장 간단한 모델 이며 시나리오는 hello에 응용 프로그램 실패 하는 hello 이벤트의 메시지를 처리 하지 않아도 안전한 수에 가장 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-136">**ReceiveAndDelete** mode is hello simplest model and works best for scenarios in which hello application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="a0107-137">toounderstand hello는 hello 소비자 문제에 요청을 수신 하는 시나리오 및 후 처리 하기 전에 크래시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-137">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="a0107-138">서비스 버스 hello 응용 프로그램 다시 시작 되 고 메시지 사용을 시작 하는 경우 사용 되는 것 hello 메시지를 표시 하기 때문에 누락 됩니다 hello 메시지 했던 이전 toohello 크래시를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-138">Because Service Bus marks hello message as being consumed, when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="a0107-139">[PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode) hello 수신 모드에서이 통해 누락 된 메시지를 허용할 수 없는 가능한 toosupport 응용 프로그램 작업은 2 단계.</span><span class="sxs-lookup"><span data-stu-id="a0107-139">In [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, hello receive operation becomes two-stage, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="a0107-140">서비스 버스 hello 요청을 받으면 hello 사용 되는 다음 메시지 toobe 찾습니다, tooprevent 잠급니다 다른 소비자가 수신할 toohello 응용 프로그램 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-140">When Service Bus receives hello request, it finds hello next message toobe consumed, locks it tooprevent other consumers from receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="a0107-141">Hello hello의 두 번째 단계를 완료 후 hello 응용 프로그램 hello 메시지 처리를 완료 (또는 이후 처리를 위해 안정적으로 저장)를 호출 하 여 수신 프로세스 [완료](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) hello 받은 메시지에 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-141">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling [Complete](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) on hello received message.</span></span> <span data-ttu-id="a0107-142">서비스 버스 hello를 표시 하는 경우 **완료** 호출, hello 메시지를 사용 중으로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-142">When Service Bus sees hello **Complete** call, it marks hello message as being consumed.</span></span>

<span data-ttu-id="a0107-143">Hello 응용 프로그램 수 없는 경우 몇 가지 이유로 tooprocess 환영 메시지가, hello 호출할 수 있는 [중단](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon) 메서드 hello 받은 메시지를 (대신 [완료](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete)).</span><span class="sxs-lookup"><span data-stu-id="a0107-143">If hello application is unable tooprocess hello message for some reason, it can call hello [Abandon](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon) method on hello received message (instead of [Complete](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete)).</span></span> <span data-ttu-id="a0107-144">동일한 소비자 hello 사용 하거나, 서비스 버스 toounlock hello 메시지를 통해이 고 수신 다시 사용할 수 있는 toobe 확인 또는 다른 경쟁 소비자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-144">This enables Service Bus toounlock hello message and make it available toobe received again, either by hello same consumer or by another competing consumer.</span></span> <span data-ttu-id="a0107-145">둘째, 있습니다 tooprocess hello 응용 프로그램 실패 및 연결 된 hello 잠금 시간 초과가 환영 메시지가 만료 되기 전에 hello 잠금 제한 시간 (예를 들어 hello 응용 프로그램이 충돌할 경우), 서비스 버스 hello 메시지의 잠금을 해제 하 고 사용할 수 있는 toobe를 사용 하면 수신 다시 (기본적으로 수행 된 [중단](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon) 기본적으로 작업).</span><span class="sxs-lookup"><span data-stu-id="a0107-145">Secondly, there is a timeout associated with hello lock and if hello application fails tooprocess hello message before hello lock timeout expires (for example, if hello application crashes), then Service Bus unlocks hello message and makes it available toobe received again (essentially performing an [Abandon](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon) operation by default).</span></span>

<span data-ttu-id="a0107-146">Hello에 hello 메시지 처리 전후에 그러나 hello 전에 hello 응용 프로그램 이벤트 충돌을 참고 **완료** 다시 시작할 때 hello 메시지는 다시 전달한 toohello 응용 프로그램, 요청이 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-146">Note that in hello event that hello application crashes after processing hello message, but before hello **Complete** request is issued, hello message is redelivered toohello application when it restarts.</span></span> <span data-ttu-id="a0107-147">이를 *최소 한 번 이상* 처리라고 합니다. 즉, 각 메시지가 최소 한 번 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-147">This is often called *At Least Once* processing; that is, each message is processed at least once.</span></span> <span data-ttu-id="a0107-148">그러나 특정 상황 hello에 동일한 메시지 수를 다시 배달 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-148">However, in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="a0107-149">Hello 시나리오 중복 처리가 허용 되지 않는 경우 hello에 따라 수행할 수 있는 hello 응용 프로그램 toodetect 중복 항목에 추가 논리가 필요 **MessageId** 상태로 남아 있는 hello 메시지의 속성 배달 시도 간에 상수입니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-149">If hello scenario cannot tolerate duplicate processing, then additional logic is required in hello application toodetect duplicates which can be achieved based upon hello **MessageId** property of hello message, which remains constant across delivery attempts.</span></span> <span data-ttu-id="a0107-150">*정확히 한번* 처리로 알려집니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-150">This is known as *Exactly Once* processing.</span></span>

## <a name="topics-and-subscriptions"></a><span data-ttu-id="a0107-151">토픽 및 구독</span><span class="sxs-lookup"><span data-stu-id="a0107-151">Topics and subscriptions</span></span>
<span data-ttu-id="a0107-152">각 메시지를 처리 하는 단일 소비자 하 되는 대비 tooqueues에서 *항목* 및 *구독* 에 일 대 다 형식의 통신을 제공는 *게시/구독* 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-152">In contrast tooqueues, in which each message is processed by a single consumer, *topics* and *subscriptions* provide a one-to-many form of communication, in a *publish/subscribe* pattern.</span></span> <span data-ttu-id="a0107-153">Toovery 많은 수의 받는 사람을 크기 조정에 대 한 유용한, 게시 된 각 메시지 hello 항목으로 등록 하는 사용 가능한 tooeach 구독을 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-153">Useful for scaling toovery large numbers of recipients, each published message is made available tooeach subscription registered with hello topic.</span></span> <span data-ttu-id="a0107-154">Tooa 주제 및 배달된 tooone 또는 구독 단위로에 설정 될 수 있는 필터 규칙에 따라 연결 된 구독 더 메시지가 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-154">Messages are sent tooa topic and delivered tooone or more associated subscriptions, depending on filter rules that can be set on a per-subscription basis.</span></span> <span data-ttu-id="a0107-155">hello 구독 tooreceive 보고자 하는 추가 필터 toorestrict hello 메시지를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-155">hello subscriptions can use additional filters toorestrict hello messages that they want tooreceive.</span></span> <span data-ttu-id="a0107-156">메시지 tooa 항목 hello 동일한 방식으로 전송 됩니다 tooa 큐 하지만 메시지는 hello 항목에서 직접 수신 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-156">Messages are sent tooa topic in hello same way they are sent tooa queue, but messages are not received from hello topic directly.</span></span> <span data-ttu-id="a0107-157">대신 구독에서 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-157">Instead, they are received from subscriptions.</span></span> <span data-ttu-id="a0107-158">항목 구독의 toohello 항목 전송 되는 hello 메시지의 복사본을 받는 가상 큐와 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-158">A topic subscription resembles a virtual queue that receives copies of hello messages that are sent toohello topic.</span></span> <span data-ttu-id="a0107-159">구독에서 동일 하 게 메시지를 받을 toohello 방식으로 큐에서 수신 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-159">Messages are received from a subscription identically toohello way they are received from a queue.</span></span>

<span data-ttu-id="a0107-160">비교를 통해 hello 큐의 메시지 전송 기능은 직접 tooa 항목 매핑되고 메시지 수신 기능은 해당 매핑됩니다 tooa 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-160">By way of comparison, hello message-sending functionality of a queue maps directly tooa topic and its message-receiving functionality maps tooa subscription.</span></span> <span data-ttu-id="a0107-161">특히, 즉 구독을 지원 큰지에 tooqueues와이 섹션의 앞에서 설명한 동일한 패턴 hello: 경쟁 소비자, 임시 분리, 부하 평준화 및 부하 분산 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-161">Among other things, this means that subscriptions support hello same patterns described earlier in this section with regard tooqueues: competing consumer, temporal decoupling, load leveling, and load balancing.</span></span>

<span data-ttu-id="a0107-162">항목을 만들기 hello 이전 단원의 hello 예제에 나와 있는 것 처럼 유사한 toocreating 큐입니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-162">Creating a topic is similar toocreating a queue, as shown in hello example in hello previous section.</span></span> <span data-ttu-id="a0107-163">Hello 서비스 URI를 만들고 다음 hello를 사용 하 여 [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) 클래스 toocreate hello 네임 스페이스 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-163">Create hello service URI, and then use hello [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) class toocreate hello namespace client.</span></span> <span data-ttu-id="a0107-164">Hello를 사용 하 여 항목을 만들 수 있습니다 [CreateTopic](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateTopic_System_String_) 메서드.</span><span class="sxs-lookup"><span data-stu-id="a0107-164">You can then create a topic using hello [CreateTopic](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateTopic_System_String_) method.</span></span> <span data-ttu-id="a0107-165">예:</span><span class="sxs-lookup"><span data-stu-id="a0107-165">For example:</span></span>

```csharp
TopicDescription dataCollectionTopic = namespaceClient.CreateTopic("DataCollectionTopic");
```

<span data-ttu-id="a0107-166">다음으로 원하는 대로 구독을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-166">Next, add subscriptions as desired:</span></span>

```csharp
SubscriptionDescription myAgentSubscription = namespaceClient.CreateSubscription(myTopic.Path, "Inventory");
SubscriptionDescription myAuditSubscription = namespaceClient.CreateSubscription(myTopic.Path, "Dashboard");
```

<span data-ttu-id="a0107-167">그런 다음 토픽 클라이언트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-167">You can then create a topic client.</span></span> <span data-ttu-id="a0107-168">예:</span><span class="sxs-lookup"><span data-stu-id="a0107-168">For example:</span></span>

```csharp
MessagingFactory factory = MessagingFactory.Create(serviceUri, tokenProvider);
TopicClient myTopicClient = factory.CreateTopicClient(myTopic.Path)
```

<span data-ttu-id="a0107-169">Hello 메시지 보낸 사람을 사용 하 여 있습니다 보내고 받을 수 메시지 tooand hello 항목에서 hello 이전 섹션에 나와 있는 것 처럼 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-169">Using hello message sender, you can send and receive messages tooand from hello topic, as shown in hello previous section.</span></span> <span data-ttu-id="a0107-170">예:</span><span class="sxs-lookup"><span data-stu-id="a0107-170">For example:</span></span>

```csharp
foreach (BrokeredMessage message in messageList)
{
    myTopicClient.Send(message);
    Console.WriteLine(
    string.Format("Message sent: Id = {0}, Body = {1}", message.MessageId, message.GetBody<string>()));
}
```

<span data-ttu-id="a0107-171">비슷한 tooqueues, 메시지를 사용 하 여 구독에서 받는 [SubscriptionClient](/dotnet/api/microsoft.servicebus.messaging.subscriptionclient) 개체가 아니라는 [QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient) 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-171">Similar tooqueues, messages are received from a subscription using a [SubscriptionClient](/dotnet/api/microsoft.servicebus.messaging.subscriptionclient) object instead of a [QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient) object.</span></span> <span data-ttu-id="a0107-172">Hello 구독의 이름으로 hello, hello 문서의 hello 이름을 전달 hello 구독 클라이언트를 만들고 (선택 사항) hello 수신 모드 매개 변수로 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-172">Create hello subscription client, passing hello name of hello topic, hello name of hello subscription, and (optionally) hello receive mode as parameters.</span></span> <span data-ttu-id="a0107-173">예를 들어 hello로 **인벤토리** 구독:</span><span class="sxs-lookup"><span data-stu-id="a0107-173">For example, with hello **Inventory** subscription:</span></span>

```csharp
// Create hello subscription client
MessagingFactory factory = MessagingFactory.Create(serviceUri, tokenProvider); 

SubscriptionClient agentSubscriptionClient = factory.CreateSubscriptionClient("IssueTrackingTopic", "Inventory", ReceiveMode.PeekLock);
SubscriptionClient auditSubscriptionClient = factory.CreateSubscriptionClient("IssueTrackingTopic", "Dashboard", ReceiveMode.ReceiveAndDelete); 

while ((message = agentSubscriptionClient.Receive(TimeSpan.FromSeconds(5))) != null)
{
    Console.WriteLine("\nReceiving message from Inventory...");
    Console.WriteLine(string.Format("Message received: Id = {0}, Body = {1}", message.MessageId, message.GetBody<string>()));
    message.Complete();
}          

// Create a receiver using ReceiveAndDelete mode
while ((message = auditSubscriptionClient.Receive(TimeSpan.FromSeconds(5))) != null)
{
    Console.WriteLine("\nReceiving message from Dashboard...");
    Console.WriteLine(string.Format("Message received: Id = {0}, Body = {1}", message.MessageId, message.GetBody<string>()));
}
```

### <a name="rules-and-actions"></a><span data-ttu-id="a0107-174">규칙 및 동작</span><span class="sxs-lookup"><span data-stu-id="a0107-174">Rules and actions</span></span>
<span data-ttu-id="a0107-175">대부분의 시나리오에서 특정 특성을 가진 메시지를 다른 방법으로 처리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-175">In many scenarios, messages that have specific characteristics must be processed in different ways.</span></span> <span data-ttu-id="a0107-176">tooenable이를 원하는 속성을 가진 및 다음 특정 수정 toothose 속성을 수행 하는 구독 toofind 메시지를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-176">tooenable this, you can configure subscriptions toofind messages that have desired properties and then perform certain modifications toothose properties.</span></span> <span data-ttu-id="a0107-177">서비스 버스 구독 toohello 항목 보낸 모든 메시지에 표시를 하는 동안에 해당 메시지 toohello 가상 구독 큐의 하위 집합을 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-177">While Service Bus subscriptions see all messages sent toohello topic, you can only copy a subset of those messages toohello virtual subscription queue.</span></span> <span data-ttu-id="a0107-178">구독 필터를 사용하여 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-178">This is accomplished using subscription filters.</span></span> <span data-ttu-id="a0107-179">이와 같은 수정을 *필터 동작*이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-179">Such modifications are called *filter actions*.</span></span> <span data-ttu-id="a0107-180">구독을 만든 경우 hello 메시지의 hello 속성에 작동 하는 필터 식을 제공할 수 있습니다, 둘 다 hello 시스템 속성 (예를 들어 **레이블**) 및 사용자 지정 응용 프로그램 속성 (예를 들어 **StoreName**.) hello SQL 필터 식을이 예제의; 선택 사항 SQL 필터 식을 없이 구독에 정의 된 모든 필터 동작이 해당 구독에 대 한 모든 hello 메시지에 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-180">When a subscription is created, you can supply a filter expression that operates on hello properties of hello message, both hello system properties (for example, **Label**) and custom application properties (for example, **StoreName**.) hello SQL filter expression is optional in this case; without a SQL filter expression, any filter action defined on a subscription will be performed on all hello messages for that subscription.</span></span>

<span data-ttu-id="a0107-181">Toofilter 메시지에서 들어오는 hello 앞의 예제를 사용 하 여 **Store1**를 다음과 같이 hello Dashboard 구독을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-181">Using hello previous example, toofilter messages coming only from **Store1**, you would create hello Dashboard subscription as follows:</span></span>

```csharp
namespaceManager.CreateSubscription("IssueTrackingTopic", "Dashboard", new SqlFilter("StoreName = 'Store1'"));
```

<span data-ttu-id="a0107-182">메시지 hello를 현재 위치에서이 구독 필터 `StoreName` 속성이 너무 설정`Store1` hello에 대 한 복사 toohello 가상 큐는 `Dashboard` 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-182">With this subscription filter in place, only messages that have hello `StoreName` property set too`Store1` are copied toohello virtual queue for hello `Dashboard` subscription.</span></span>

<span data-ttu-id="a0107-183">가능한 필터 값에 대 한 자세한 내용은 hello에 대 한 hello 설명서를 참조 하십시오. [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) 및 [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-183">For more information about possible filter values, see hello documentation for hello [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) and [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) classes.</span></span> <span data-ttu-id="a0107-184">참고: hello [조정 된 메시징: 고급 필터](http://code.msdn.microsoft.com/Brokered-Messaging-6b0d2749) 및 [항목 필터](https://github.com/Azure-Samples/azure-servicebus-messaging-samples/tree/master/TopicFilters) 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="a0107-184">Also, see hello [Brokered Messaging: Advanced Filters](http://code.msdn.microsoft.com/Brokered-Messaging-6b0d2749) and [Topic Filters](https://github.com/Azure-Samples/azure-servicebus-messaging-samples/tree/master/TopicFilters) samples.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a0107-185">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a0107-185">Next steps</span></span>
<span data-ttu-id="a0107-186">Hello 다음을 고급 자세한 내용 및 서비스 버스 메시징 사용 하는 예제에 대 한 항목을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="a0107-186">See hello following advanced topics for more information and examples of using Service Bus messaging.</span></span>

* [<span data-ttu-id="a0107-187">서비스 버스 메시징 개요</span><span class="sxs-lookup"><span data-stu-id="a0107-187">Service Bus messaging overview</span></span>](service-bus-messaging-overview.md)
* [<span data-ttu-id="a0107-188">Service Bus 조정된 메시징 .NET 자습서</span><span class="sxs-lookup"><span data-stu-id="a0107-188">Service Bus brokered messaging .NET tutorial</span></span>](service-bus-brokered-tutorial-dotnet.md)
* [<span data-ttu-id="a0107-189">Service Bus 조정된 메시징 REST 자습서</span><span class="sxs-lookup"><span data-stu-id="a0107-189">Service Bus brokered messaging REST tutorial</span></span>](service-bus-brokered-tutorial-rest.md)
* [<span data-ttu-id="a0107-190">토픽 필터 샘플</span><span class="sxs-lookup"><span data-stu-id="a0107-190">Topic Filters sample </span></span>](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/TopicFilters)
* [<span data-ttu-id="a0107-191">조정된 메시징: 고급 필터 샘플</span><span class="sxs-lookup"><span data-stu-id="a0107-191">Brokered Messaging: Advanced Filters sample</span></span>](http://code.msdn.microsoft.com/Brokered-Messaging-6b0d2749)


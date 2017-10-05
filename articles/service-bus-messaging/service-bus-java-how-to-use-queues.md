---
title: "Java와 함께 Azure Service Bus 큐를 사용하는 방법 | Microsoft Docs"
description: "Azure에서 서비스 버스 큐를 사용하는 방법에 대해 알아봅니다. 코드 샘플은 Java로 작성되었습니다."
services: service-bus-messaging
documentationcenter: java
author: sethmanheim
manager: timlt
ms.assetid: f701439c-553e-402c-94a7-64400f997d59
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 170f431525ffdc93a01fc085e48e69c3a774968e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-service-bus-queues-with-java"></a><span data-ttu-id="ce624-104">Java에서 Service Bus 큐를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="ce624-104">How to use Service Bus queues with Java</span></span>
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="ce624-105">이 문서에서는 서비스 버스 큐를 사용하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="ce624-105">This article describes how to use Service Bus queues.</span></span> <span data-ttu-id="ce624-106">샘플은 Java로 작성되었으며 [Java용 Azure SDK][Azure SDK for Java]를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ce624-106">The samples are written in Java and use the [Azure SDK for Java][Azure SDK for Java].</span></span> <span data-ttu-id="ce624-107">여기서 다루는 시나리오에는 **큐 만들기**, **메시지 보내기 및 받기**, **큐 삭제** 등이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce624-107">The scenarios covered include **creating queues**, **sending and receiving messages**, and **deleting queues**.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="configure-your-application-to-use-service-bus"></a><span data-ttu-id="ce624-108">서비스 버스를 사용하도록 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="ce624-108">Configure your application to use Service Bus</span></span>
<span data-ttu-id="ce624-109">이 샘플을 빌드하기 전에 [Java용 Azure SDK][Azure SDK for Java]를 설치했는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="ce624-109">Make sure you have installed the [Azure SDK for Java][Azure SDK for Java] before building this sample.</span></span> <span data-ttu-id="ce624-110">Eclipse를 사용하는 경우 Azure SDK for Java를 포함하고 있는 [Eclipse용 Azure Toolkit][Azure Toolkit for Eclipse]를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce624-110">If you are using Eclipse, you can install the [Azure Toolkit for Eclipse][Azure Toolkit for Eclipse] that includes the Azure SDK for Java.</span></span> <span data-ttu-id="ce624-111">그런 다음 **Java용 Microsoft Azure 라이브러리**를 프로젝트에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce624-111">You can then add the **Microsoft Azure Libraries for Java** to your project:</span></span>

![](./media/service-bus-java-how-to-use-queues/eclipselibs.png)

<span data-ttu-id="ce624-112">Java 파일 맨 위에 다음 `import` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ce624-112">Add the following `import` statements to the top of the Java file:</span></span>

```java
// Include the following imports to use Service Bus APIs
import com.microsoft.windowsazure.services.servicebus.*;
import com.microsoft.windowsazure.services.servicebus.models.*;
import com.microsoft.windowsazure.core.*;
import javax.xml.datatype.*;
```

## <a name="create-a-queue"></a><span data-ttu-id="ce624-113">큐 만들기</span><span class="sxs-lookup"><span data-stu-id="ce624-113">Create a queue</span></span>
<span data-ttu-id="ce624-114">**ServiceBusContract** 클래스를 통해 Service Bus 큐에 대한 관리 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce624-114">Management operations for Service Bus queues can be performed via the **ServiceBusContract** class.</span></span> <span data-ttu-id="ce624-115">**ServiceBusContract** 개체는 관리에 필요한 SAS 토큰 사용 권한을 캡슐화하는 적합한 구성으로 생성되며, Azure와의 통신 지점은 **ServiceBusContract** 클래스뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="ce624-115">A **ServiceBusContract** object is constructed with an appropriate configuration that encapsulates the SAS token with permissions to manage it, and the **ServiceBusContract** class is the sole point of communication with Azure.</span></span>

<span data-ttu-id="ce624-116">**ServiceBusService** 클래스는 큐를 만들고 열거 및 삭제하기 위한 메서드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ce624-116">The **ServiceBusService** class provides methods to create, enumerate, and delete queues.</span></span> <span data-ttu-id="ce624-117">아래 예제에서는 **ServiceBusService** 개체를 사용하여 `HowToSample` 네임스페이스로 `TestQueue` 큐를 만드는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="ce624-117">The example below shows how a **ServiceBusService** object can be used to create a queue named `TestQueue`, with a namespace named `HowToSample`:</span></span>

```java
Configuration config =
    ServiceBusConfiguration.configureWithSASAuthentication(
            "HowToSample",
            "RootManageSharedAccessKey",
            "SAS_key_value",
            ".servicebus.windows.net"
            );

ServiceBusContract service = ServiceBusService.create(config);
QueueInfo queueInfo = new QueueInfo("TestQueue");
try
{
    CreateQueueResult result = service.createQueue(queueInfo);
}
catch (ServiceException e)
{
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

<span data-ttu-id="ce624-118">`QueueInfo`에는 큐의 속성을 조정하는 데 사용할 수 있는 메서드가 있습니다. 예를 들어 큐에 전송되는 메시지에 적용할 기본 TTL(Time-To-Live) 값을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce624-118">There are methods on `QueueInfo` that allow properties of the queue to be tuned (for example: to set the default time-to-live (TTL) value to be applied to messages sent to the queue).</span></span> <span data-ttu-id="ce624-119">다음 예제에서는 최대 크기가 5GB인 `TestQueue` 큐를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ce624-119">The following example shows how to create a queue named `TestQueue` with a maximum size of 5GB:</span></span>

````java
long maxSizeInMegabytes = 5120;
QueueInfo queueInfo = new QueueInfo("TestQueue");
queueInfo.setMaxSizeInMegabytes(maxSizeInMegabytes);
CreateQueueResult result = service.createQueue(queueInfo);
````

<span data-ttu-id="ce624-120">**ServiceBusContract** 개체의 `listQueues` 메서드를 사용하여 서비스 네임스페이스 내에 지정된 이름의 큐가 이미 있는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce624-120">Note that you can use the `listQueues` method on **ServiceBusContract** objects to check if a queue with a specified name already exists within a service namespace.</span></span>

## <a name="send-messages-to-a-queue"></a><span data-ttu-id="ce624-121">큐에 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="ce624-121">Send messages to a queue</span></span>
<span data-ttu-id="ce624-122">Service Bus 큐에 메시지를 보내기 위해 응용 프로그램은 **ServiceBusContract** 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ce624-122">To send a message to a Service Bus queue, your application obtains a **ServiceBusContract** object.</span></span> <span data-ttu-id="ce624-123">다음 코드는 위에서 `HowToSample` 네임스페이스 내에서 이전에 만든 `TestQueue` 큐에 대한 메시지를 보내는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ce624-123">The following code shows how to send a message for the `TestQueue` queue previously created in the `HowToSample` namespace:</span></span>

```java
try
{
    BrokeredMessage message = new BrokeredMessage("MyMessage");
    service.sendQueueMessage("TestQueue", message);
}
catch (ServiceException e)
{
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

<span data-ttu-id="ce624-124">Service Bus 큐로 보내고 받은 메시지는 [BrokeredMessage][BrokeredMessage] 클래스 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="ce624-124">Messages sent to, and received from Service Bus queues are instances of the [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="ce624-125">[BrokeredMessage][BrokeredMessage] 개체에는 표준 속성 집합(예: [Label](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.label#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) 및 [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.timetolive#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), 응용 프로그램별 사용자 지정 속성을 저장하는 데 사용되는 사전 및 임의 응용 프로그램 데이터 본문이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce624-125">[BrokeredMessage][BrokeredMessage] objects have a set of standard properties (such as [Label](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.label#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) and [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.timetolive#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), a dictionary that is used to hold custom application-specific properties, and a body of arbitrary application data.</span></span> <span data-ttu-id="ce624-126">응용 프로그램은 [BrokeredMessage][BrokeredMessage] 생성자에 직렬화 가능 개체를 전달하여 메시지 본문을 설정할 수 있으며, 적절한 직렬 변환기가 개체를 직렬화하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce624-126">An application can set the body of the message by passing any serializable object into the constructor of the [BrokeredMessage][BrokeredMessage], and the appropriate serializer will then be used to serialize the object.</span></span> <span data-ttu-id="ce624-127">또는 **java.IO.InputStream** 개체를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce624-127">Alternatively, you can provide a **java.IO.InputStream** object.</span></span>

<span data-ttu-id="ce624-128">다음 예제에서는 5개의 테스트 메시지를 이전 코드 조각에서 얻은 `TestQueue` **MessageSender**에 보내는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ce624-128">The following example demonstrates how to send five test messages to the `TestQueue` **MessageSender** we obtained in the previous code snippet:</span></span>

```java
for (int i=0; i<5; i++)
{
     // Create message, passing a string message for the body.
     BrokeredMessage message = new BrokeredMessage("Test message " + i);
     // Set an additional app-specific property.
     message.setProperty("MyProperty", i);
     // Send message to the queue
     service.sendQueueMessage("TestQueue", message);
}
```

<span data-ttu-id="ce624-129">Service Bus 큐는 [표준 계층](service-bus-premium-messaging.md)에서 256KB의 최대 메시지 크기를 [프리미엄 계층](service-bus-premium-messaging.md)에서 1MB를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ce624-129">Service Bus queues support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="ce624-130">표준 및 사용자 지정 응용 프로그램 속성이 포함된 헤더의 최대 크기는 64KB입니다.</span><span class="sxs-lookup"><span data-stu-id="ce624-130">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="ce624-131">한 큐에 저장되는 메시지 수에는 제한이 없지만 한 큐에 저장되는 총 메시지 크기는 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce624-131">There is no limit on the number of messages held in a queue but there is a cap on the total size of the messages held by a queue.</span></span> <span data-ttu-id="ce624-132">이 큐 크기는 생성 시 정의되며 상한이 5GB입니다.</span><span class="sxs-lookup"><span data-stu-id="ce624-132">This queue size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="ce624-133">큐에서 메시지 받기</span><span class="sxs-lookup"><span data-stu-id="ce624-133">Receive messages from a queue</span></span>
<span data-ttu-id="ce624-134">큐에서 메시지를 받는 기본 방법은 **ServiceBusContract** 개체를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ce624-134">The primary way to receive messages from a queue is to use a **ServiceBusContract** object.</span></span> <span data-ttu-id="ce624-135">받은 메시지는 **ReceiveAndDelete** 및 **PeekLock**의 두 가지 모드로 작동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce624-135">Received messages can work in two different modes: **ReceiveAndDelete** and **PeekLock**.</span></span>

<span data-ttu-id="ce624-136">**ReceiveAndDelete** 모드를 사용하는 경우 수신은 1단계 작업입니다. 즉, Service Bus가 큐 메시지에 대한 읽기 요청을 받으면 메시지를 이용되는 것으로 표시하고 응용 프로그램에 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ce624-136">When using the **ReceiveAndDelete** mode, receive is a single-shot operation - that is, when Service Bus receives a read request for a message in a queue, it marks the message as being consumed and returns it to the application.</span></span> <span data-ttu-id="ce624-137">**ReceiveAndDelete** 모드(기본 모드임)는 가장 단순한 모델이며, 응용 프로그램이 실패 이벤트 시 메시지를 처리하지 않아도 안전한 시나리오에서 효과적입니다.</span><span class="sxs-lookup"><span data-stu-id="ce624-137">**ReceiveAndDelete** mode (which is the default mode) is the simplest model and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="ce624-138">이해를 돕기 위해 소비자가 수신 요청을 실행한 후 처리하기 전에 크래시되는 시나리오를 고려해 보세요.</span><span class="sxs-lookup"><span data-stu-id="ce624-138">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span>
<span data-ttu-id="ce624-139">서비스 버스는 메시지를 이용되는 것으로 표시하기 때문에 응용 프로그램이 다시 시작되고 메시지 소비를 다시 시작할 경우 크래시 전에 소비된 메시지가 누락됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce624-139">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="ce624-140">**PeekLock** 모드에서 수신은 2단계 작업이므로 메시지 누락이 허용되지 않는 응용 프로그램을 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce624-140">In **PeekLock** mode, receive becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="ce624-141">서비스 버스는 요청을 받으면 소비할 다음 메시지를 찾아서 다른 소비자가 수신할 수 없도록 잠근 후 응용 프로그램에 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ce624-141">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span> <span data-ttu-id="ce624-142">응용 프로그램은 메시지 처리를 완료하거나 추가 처리를 위해 안전하게 저장한 후 수신된 메시지에 대해 **Delete**를 호출하여 수신 프로세스의 두 번째 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="ce624-142">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling **Delete** on the received message.</span></span> <span data-ttu-id="ce624-143">Service Bus는 **Delete** 호출을 확인한 후 메시지를 이용되는 것으로 표시하고 큐에서 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="ce624-143">When Service Bus sees the **Delete** call, it will mark the message as being consumed and remove it from the queue.</span></span>

<span data-ttu-id="ce624-144">다음 예제에서는 **PeekLock** 모드(기본 모드가 아님)를 사용하여 메시지를 받고 처리하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ce624-144">The following example demonstrates how messages can be received and processed using **PeekLock** mode (not the default mode).</span></span> <span data-ttu-id="ce624-145">아래 예제는 무한 루프를 만들고 메시지가 `TestQueue`에 도착하면 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="ce624-145">The example below does an infinite loop and processes messages as they arrive into our `TestQueue`:</span></span>

```java
try
{
    ReceiveMessageOptions opts = ReceiveMessageOptions.DEFAULT;
    opts.setReceiveMode(ReceiveMode.PEEK_LOCK);

    while(true)  {
         ReceiveQueueMessageResult resultQM =
                 service.receiveQueueMessage("TestQueue", opts);
        BrokeredMessage message = resultQM.getValue();
        if (message != null && message.getMessageId() != null)
        {
            System.out.println("MessageID: " + message.getMessageId());
            // Display the queue message.
            System.out.print("From queue: ");
            byte[] b = new byte[200];
            String s = null;
            int numRead = message.getBody().read(b);
            while (-1 != numRead)
            {
                s = new String(b);
                s = s.trim();
                System.out.print(s);
                numRead = message.getBody().read(b);
            }
            System.out.println();
            System.out.println("Custom Property: " +
                message.getProperty("MyProperty"));
            // Remove message from queue.
            System.out.println("Deleting this message.");
            //service.deleteMessage(message);
        }  
        else  
        {
            System.out.println("Finishing up - no more messages.");
            break;
            // Added to handle no more messages.
            // Could instead wait for more messages to be added.
        }
    }
}
catch (ServiceException e) {
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
catch (Exception e) {
    System.out.print("Generic exception encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="ce624-146">응용 프로그램 작동 중단 및 읽을 수 없는 메시지를 처리하는 방법</span><span class="sxs-lookup"><span data-stu-id="ce624-146">How to handle application crashes and unreadable messages</span></span>
<span data-ttu-id="ce624-147">서비스 버스는 응용 프로그램 오류나 메시지 처리 문제를 정상적으로 복구하는 데 유용한 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ce624-147">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="ce624-148">어떤 이유로든 수신 응용 프로그램이 메시지를 처리할 수 없는 경우 받은 메시지에 대해 **deleteMessage** 메서드 대신 **unlockMessage** 메서드를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce624-148">If a receiver application is unable to process the message for some reason, then it can call the **unlockMessage** method on the received message (instead of the **deleteMessage** method).</span></span> <span data-ttu-id="ce624-149">그러면 서비스 버스에서 큐 메시지의 잠금을 해제하므로 동일한 소비 응용 프로그램이나 다른 소비 응용 프로그램에서 메시지를 다시 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce624-149">This causes Service Bus to unlock the message within the queue and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="ce624-150">큐 내에서 잠긴 메시지와 연결된 시간 제한도 있으며, 응용 프로그램에서 잠금 시간 제한이 만료되기 전에 메시지를 처리하지 못하는 경우(예: 응용 프로그램이 크래시되는 경우) 서비스 버스가 메시지를 자동으로 잠금 해제하여 다시 받을 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce624-150">There is also a timeout associated with a message locked within the queue, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus unlocks the message automatically and makes it available to be received again.</span></span>

<span data-ttu-id="ce624-151">응용 프로그램이 메시지를 처리한 후 **deleteMessage** 요청이 실행되기 전에 크래시되는 경우 다시 시작될 때 메시지가 응용 프로그램에 다시 배달됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce624-151">In the event that the application crashes after processing the message but before the **deleteMessage** request is issued, then the message is redelivered to the application when it restarts.</span></span> <span data-ttu-id="ce624-152">이를 *최소 한 번 이상 처리*라고 합니다. 즉, 각 메시지가 최소 한 번 이상 처리되지만 특정 상황에서는 동일한 메시지가 다시 배달될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce624-152">This is often called *At Least Once Processing*; that is, each message is processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="ce624-153">중복 처리가 허용되지 않는 시나리오에서는 응용 프로그램 개발자가 중복 메시지 배달을 처리하는 논리를 응용 프로그램에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce624-153">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span></span> <span data-ttu-id="ce624-154">이 작업은 배달을 여러 번 시도해도 일정하게 유지되는 메시지의 **getMessageId** 메서드를 사용하여 수행하는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="ce624-154">This is often achieved using the **getMessageId** method of the message, which remains constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ce624-155">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ce624-155">Next Steps</span></span>
<span data-ttu-id="ce624-156">지금까지 Service Bus 큐의 기본 사항에 대해 알아보았습니다. 자세한 내용은 [큐, 토픽 및 구독][Queues, topics, and subscriptions]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ce624-156">Now that you've learned the basics of Service Bus queues, see [Queues, topics, and subscriptions][Queues, topics, and subscriptions] for more information.</span></span>

<span data-ttu-id="ce624-157">자세한 내용은 [Java개발자 센터](https://azure.microsoft.com/develop/java/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ce624-157">For more information, see the [Java Developer Center](https://azure.microsoft.com/develop/java/).</span></span>

[Azure SDK for Java]: http://azure.microsoft.com/develop/java/
[Azure Toolkit for Eclipse]: https://msdn.microsoft.com/library/azure/hh694271.aspx
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage

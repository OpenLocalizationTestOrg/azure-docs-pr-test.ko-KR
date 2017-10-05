---
title: "Java와 함께 Azure Service Bus 항목을 사용하는 방법 | Microsoft Docs"
description: "Azure에서 Service Bus 토픽 및 구독을 사용합니다."
services: service-bus-messaging
documentationcenter: java
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 63d6c8bd-8a22-4292-befc-545ffb52e8eb
ms.service: service-bus-messaging
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 06/28/2017
ms.author: sethm
ms.openlocfilehash: b561d6fdcf4fb2839908ac8f53832fb0830dd576
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-service-bus-topics-and-subscriptions-with-java"></a><span data-ttu-id="32f85-103">Java에서 Service Bus 토픽 및 구독을 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="32f85-103">How to use Service Bus topics and subscriptions with Java</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="32f85-104">이 가이드에서는 서비스 버스 토픽과 구독을 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-104">This guide describes how to use Service Bus topics and subscriptions.</span></span> <span data-ttu-id="32f85-105">샘플은 Java로 작성되었으며 [Java용 Azure SDK][Azure SDK for Java]를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-105">The samples are written in Java and use the [Azure SDK for Java][Azure SDK for Java].</span></span> <span data-ttu-id="32f85-106">여기서 다루는 시나리오에는 **토픽 및 구독 만들기**, **구독 필터 만들기**, **토픽에 메시지 보내기**, **구독에서 메시지 받기**, **토픽 및 구독 삭제** 등이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-106">The scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages to a topic**, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span>

## <a name="what-are-service-bus-topics-and-subscriptions"></a><span data-ttu-id="32f85-107">서비스 버스 토픽 및 구독 정의</span><span class="sxs-lookup"><span data-stu-id="32f85-107">What are Service Bus topics and subscriptions?</span></span>
<span data-ttu-id="32f85-108">서비스 버스 토픽 및 구독은 *게시/구독* 메시징 통신 모델을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-108">Service Bus topics and subscriptions support a *publish/subscribe* messaging communication model.</span></span> <span data-ttu-id="32f85-109">토픽 및 구독을 사용하는 경우 분산 응용 프로그램의 구성 요소가 서로 직접 통신하지 않고 중간자 역할을 하는 토픽을 통해 메시지를 교환합니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-109">When using topics and subscriptions, components of a distributed application do not communicate directly with each other; instead they exchange messages via a topic, which acts as an intermediary.</span></span>

![TopicConcepts](./media/service-bus-java-how-to-use-topics-subscriptions/sb-topics-01.png)

<span data-ttu-id="32f85-111">각 메시지가 단일 소비자에 의해 처리되는 서비스 버스 큐와 반대로, 토픽과 구독은 게시/구독 패턴을 사용하여 "일 대 다" 형태의 통신을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-111">In contrast with Service Bus queues, in which each message is processed by a single consumer, topics and subscriptions provide a "one-to-many" form of communication, using a publish/subscribe pattern.</span></span> <span data-ttu-id="32f85-112">하나의 토픽에 여러 구독을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-112">It is possible to register multiple subscriptions to a topic.</span></span> <span data-ttu-id="32f85-113">토픽에 메시지를 전송하면 각 구독에서 독립적으로 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-113">When a message is sent to a topic, it is then made available to each subscription to handle/process independently.</span></span>

<span data-ttu-id="32f85-114">토픽 구독은 토픽에 전송된 메시지의 복사본을 받는 가상 큐와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-114">A subscription to a topic resembles a virtual queue that receives copies of the messages that were sent to the topic.</span></span> <span data-ttu-id="32f85-115">선택적으로 구독별 토픽에 대한 필터 규칙을 등록할 수 있으며, 이렇게 하면 각 토픽 구독에서 받는 토픽 메시지를 필터링/제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-115">You can optionally register filter rules for a topic on a per-subscription basis, which allows you to filter/restrict which messages to a topic are received by which topic subscriptions.</span></span>

<span data-ttu-id="32f85-116">서비스 버스 토픽 및 구독을 사용하면 다수의 사용자와 응용 프로그램에 대해 다수의 메시지를 처리하도록 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-116">Service Bus topics and subscriptions enable you to scale to process a very large number of messages across a very large number of users and applications.</span></span>

## <a name="create-a-service-namespace"></a><span data-ttu-id="32f85-117">서비스 네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="32f85-117">Create a service namespace</span></span>
<span data-ttu-id="32f85-118">Azure에서 Service Bus 항목 및 구독을 사용하려면 먼저 응용 프로그램 내에서 Service Bus 리소스의 주소 지정을 위한 범위 컨테이너를 제공하는 네임스페이스를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-118">To begin using Service Bus topics and subscriptions in Azure, you must first create a namespace, which provides a scoping container for addressing Service Bus resources within your application.</span></span>

<span data-ttu-id="32f85-119">네임스페이스를 만들려면</span><span class="sxs-lookup"><span data-stu-id="32f85-119">To create a namespace:</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="configure-your-application-to-use-service-bus"></a><span data-ttu-id="32f85-120">서비스 버스를 사용하도록 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="32f85-120">Configure your application to use Service Bus</span></span>
<span data-ttu-id="32f85-121">이 샘플을 빌드하기 전에 [Java용 Azure SDK][Azure SDK for Java]를 설치했는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="32f85-121">Make sure you have installed the [Azure SDK for Java][Azure SDK for Java] before building this sample.</span></span> <span data-ttu-id="32f85-122">Eclipse를 사용하는 경우 Azure SDK for Java를 포함하고 있는 [Eclipse용 Azure Toolkit][Azure Toolkit for Eclipse]를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-122">If you are using Eclipse, you can install the [Azure Toolkit for Eclipse][Azure Toolkit for Eclipse] that includes the Azure SDK for Java.</span></span> <span data-ttu-id="32f85-123">그런 다음 **Java용 Microsoft Azure 라이브러리**를 프로젝트에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-123">You can then add the **Microsoft Azure Libraries for Java** to your project:</span></span>

![](media/service-bus-java-how-to-use-topics-subscriptions/eclipselibs.png)

<span data-ttu-id="32f85-124">Java 파일 맨 위에 다음 `import` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-124">Add the following `import` statements to the top of the Java file:</span></span>

```java
import com.microsoft.windowsazure.services.servicebus.*;
import com.microsoft.windowsazure.services.servicebus.models.*;
import com.microsoft.windowsazure.core.*;
import javax.xml.datatype.*;
```

<span data-ttu-id="32f85-125">Java용 Azure 라이브러리를 빌드 경로에 추가하고 프로젝트 배포 어셈블리에 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-125">Add the Azure Libraries for Java to your build path and include it in your project deployment assembly.</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="32f85-126">토픽 만들기</span><span class="sxs-lookup"><span data-stu-id="32f85-126">Create a topic</span></span>
<span data-ttu-id="32f85-127">**ServiceBusContract** 클래스를 통해 Service Bus 토픽에 대한 관리 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-127">Management operations for Service Bus topics can be performed via the **ServiceBusContract** class.</span></span> <span data-ttu-id="32f85-128">**ServiceBusContract** 개체는 관리에 필요한 SAS 토큰 사용 권한을 캡슐화하는 적합한 구성으로 생성되며, Azure와의 통신 지점은 **ServiceBusContract** 클래스뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-128">A **ServiceBusContract** object is constructed with an appropriate configuration that encapsulates the SAS token with permissions to manage it, and the **ServiceBusContract** class is the sole point of communication with Azure.</span></span>

<span data-ttu-id="32f85-129">**ServiceBusService** 클래스는 토픽을 만들고 열거 및 삭제하기 위한 메서드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-129">The **ServiceBusService** class provides methods to create, enumerate, and delete topics.</span></span> <span data-ttu-id="32f85-130">다음 예제에서는 **ServiceBusService** 개체를 사용하여 `HowToSample` 네임스페이스로 `TestTopic`라는 토픽을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-130">The following example shows how a **ServiceBusService** object can be used to create a topic named `TestTopic`, with a namespace called `HowToSample`:</span></span>

```java
Configuration config =
    ServiceBusConfiguration.configureWithSASAuthentication(
      "HowToSample",
      "RootManageSharedAccessKey",
      "SAS_key_value",
      ".servicebus.windows.net"
      );

ServiceBusContract service = ServiceBusService.create(config);
TopicInfo topicInfo = new TopicInfo("TestTopic");
try  
{
    CreateTopicResult result = service.createTopic(topicInfo);
}
catch (ServiceException e) {
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

<span data-ttu-id="32f85-131">**TopicInfo**에는 토픽의 속성을 조정하는 데 사용할 수 있는 메서드가 있습니다. 예를 들어 토픽에 전송되는 메시지에 적용할 기본 TTL(Time-To-Live) 값을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-131">There are methods on **TopicInfo** that enable properties of the topic to be set (for example: to set the default time-to-live (TTL) value to be applied to messages sent to the topic).</span></span> <span data-ttu-id="32f85-132">다음 예제에서는 최대 크기가 5GB인 `TestTopic` 토픽을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-132">The following example shows how to create a topic named `TestTopic` with a maximum size of 5 GB:</span></span>

```java
long maxSizeInMegabytes = 5120;  
TopicInfo topicInfo = new TopicInfo("TestTopic");  
topicInfo.setMaxSizeInMegabytes(maxSizeInMegabytes);
CreateTopicResult result = service.createTopic(topicInfo);
```

<span data-ttu-id="32f85-133">**ServiceBusContract** 개체의 **listTopics** 메서드를 사용하여 서비스 네임스페이스 내에 지정된 이름의 토픽이 이미 있는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-133">Note that you can use the **listTopics** method on **ServiceBusContract** objects to check if a topic with a specified name already exists within a service namespace.</span></span>

## <a name="create-subscriptions"></a><span data-ttu-id="32f85-134">구독 만들기</span><span class="sxs-lookup"><span data-stu-id="32f85-134">Create subscriptions</span></span>
<span data-ttu-id="32f85-135">토픽에 대한 구독은 **ServiceBusService** 클래스로도 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-135">Subscriptions to topics are also created with the **ServiceBusService** class.</span></span> <span data-ttu-id="32f85-136">구독에는 이름이 지정되며, 구독의 가상 큐에 전달되는 메시지 집합을 제한하는 선택적 필터가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-136">Subscriptions are named and can have an optional filter that restricts the set of messages passed to the subscription's virtual queue.</span></span>

### <a name="create-a-subscription-with-the-default-matchall-filter"></a><span data-ttu-id="32f85-137">기본(MatchAll) 필터를 사용하여 구독 만들기</span><span class="sxs-lookup"><span data-stu-id="32f85-137">Create a subscription with the default (MatchAll) filter</span></span>
<span data-ttu-id="32f85-138">**MatchAll** 필터는 새 구독을 만들 때 필터를 지정하지 않은 경우 사용되는 기본 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-138">The **MatchAll** filter is the default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="32f85-139">**MatchAll** 필터를 사용하면 토픽에 게시된 모든 메시지가 구독의 가상 큐에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-139">When the **MatchAll** filter is used, all messages published to the topic are placed in the subscription's virtual queue.</span></span> <span data-ttu-id="32f85-140">다음 예제에서는 "AllMessages"라는 구독을 만들고 기본 **MatchAll** 필터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-140">The following example creates a subscription named "AllMessages" and uses the default **MatchAll** filter.</span></span>

```java
SubscriptionInfo subInfo = new SubscriptionInfo("AllMessages");
CreateSubscriptionResult result =
    service.createSubscription("TestTopic", subInfo);
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="32f85-141">필터를 사용하여 구독 만들기</span><span class="sxs-lookup"><span data-stu-id="32f85-141">Create subscriptions with filters</span></span>
<span data-ttu-id="32f85-142">토픽으로 전송된 메시지 중 특정 토픽 구독 내에 표시되어야 하는 메시지의 범위를 지정하는 필터를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-142">You can also create filters that enable you to scope which messages sent to a topic should show up within a specific topic subscription.</span></span>

<span data-ttu-id="32f85-143">구독에서 지원하는 가장 유연한 유형의 필터는 SQL92 하위 집합을 구현하는 [SqlFilter][SqlFilter]입니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-143">The most flexible type of filter supported by subscriptions is the [SqlFilter][SqlFilter], which implements a subset of SQL92.</span></span> <span data-ttu-id="32f85-144">SQL 필터는 토픽에 게시된 메시지의 속성에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-144">SQL filters operate on the properties of the messages that are published to the topic.</span></span> <span data-ttu-id="32f85-145">SQL 필터와 함께 사용할 수 있는 식에 대한 자세한 내용은 [SqlFilter.SqlExpression][SqlFilter.SqlExpression] 구문을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="32f85-145">For more details about the expressions that can be used with a SQL filter, review the [SqlFilter.SqlExpression][SqlFilter.SqlExpression] syntax.</span></span>

<span data-ttu-id="32f85-146">다음 예제에서는 사용자 지정 **MessageNumber** 속성이 3보다 큰 메시지만 선택하는 [SqlFilter][SqlFilter] 개체를 사용하여 `HighMessages`(이)라는 구독을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-146">The following example creates a subscription named `HighMessages` with a [SqlFilter][SqlFilter] object that only selects messages that have a custom **MessageNumber** property greater than 3:</span></span>

```java
// Create a "HighMessages" filtered subscription  
SubscriptionInfo subInfo = new SubscriptionInfo("HighMessages");
CreateSubscriptionResult result = service.createSubscription("TestTopic", subInfo);
RuleInfo ruleInfo = new RuleInfo("myRuleGT3");
ruleInfo = ruleInfo.withSqlExpressionFilter("MessageNumber > 3");
CreateRuleResult ruleResult = service.createRule("TestTopic", "HighMessages", ruleInfo);
// Delete the default rule, otherwise the new rule won't be invoked.
service.deleteRule("TestTopic", "HighMessages", "$Default");
```

<span data-ttu-id="32f85-147">마찬가지로, 다음 예제에서는 **MessageNumber** 속성이 3보다 작거나 같은 메시지만 선택하는 [SqlFilter][SqlFilter] 개체를 사용하여 `LowMessages`(이)라는 구독을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-147">Similarly, the following example creates a subscription named `LowMessages` with a [SqlFilter][SqlFilter] object that only selects messages that have a **MessageNumber** property less than or equal to 3:</span></span>

```java
// Create a "LowMessages" filtered subscription
SubscriptionInfo subInfo = new SubscriptionInfo("LowMessages");
CreateSubscriptionResult result = service.createSubscription("TestTopic", subInfo);
RuleInfo ruleInfo = new RuleInfo("myRuleLE3");
ruleInfo = ruleInfo.withSqlExpressionFilter("MessageNumber <= 3");
CreateRuleResult ruleResult = service.createRule("TestTopic", "LowMessages", ruleInfo);
// Delete the default rule, otherwise the new rule won't be invoked.
service.deleteRule("TestTopic", "LowMessages", "$Default");
```

<span data-ttu-id="32f85-148">이제 `TestTopic`(으)로 메시지를 보내는 경우 `AllMessages` 구독을 구독하는 수신자에게는 항상 배달되고, `HighMessages` 및 `LowMessages` 구독을 구독하는 수신자에게는 메시지 내용에 따라 선택적으로 배달됩니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-148">When a message is now sent to `TestTopic`, it will always be delivered to receivers subscribed to the `AllMessages` subscription, and selectively delivered to receivers subscribed to the `HighMessages` and `LowMessages` subscriptions (depending upon the message content).</span></span>

## <a name="send-messages-to-a-topic"></a><span data-ttu-id="32f85-149">토픽에 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="32f85-149">Send messages to a topic</span></span>
<span data-ttu-id="32f85-150">Service Bus 토픽에 메시지를 보내기 위해 응용 프로그램은 **ServiceBusContract** 개체를 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-150">To send a message to a Service Bus topic, your application obtains a **ServiceBusContract** object.</span></span> <span data-ttu-id="32f85-151">다음 코드는 위에서 `HowToSample` 서비스 네임스페이스 내에서 이전에 만든 `TestTopic` 항목에 메시지를 보내는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-151">The following code demonstrates how to send a message for the `TestTopic` topic created previously within the `HowToSample` namespace:</span></span>

```java
BrokeredMessage message = new BrokeredMessage("MyMessage");
service.sendTopicMessage("TestTopic", message);
```

<span data-ttu-id="32f85-152">Service Bus 토픽으로 전송된 메시지는 [BrokeredMessage][BrokeredMessage] 클래스의 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-152">Messages sent to Service Bus Topics are instances of the [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="32f85-153">[BrokeredMessage][BrokeredMessage]* 개체에는 표준 메서드 집합(예: **setLabel** 및 **TimeToLive**), 응용 프로그램별 사용자 지정 속성을 저장하는 데 사용되는 사전 및 임의 응용 프로그램 데이터 본문이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-153">[BrokeredMessage][BrokeredMessage]* objects have a set of standard methods (such as **setLabel** and **TimeToLive**), a dictionary that is used to hold custom application-specific properties, and a body of arbitrary application data.</span></span> <span data-ttu-id="32f85-154">응용 프로그램은 [BrokeredMessage][BrokeredMessage] 생성자에 직렬화된 개체를 전달하여 메시지 본문을 설정할 수 있으며, 적절한 **DataContractSerializer**가 개체를 직렬화하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-154">An application can set the body of the message by passing any serializable object into the constructor of the [BrokeredMessage][BrokeredMessage], and the appropriate **DataContractSerializer** will then be used to serialize the object.</span></span> <span data-ttu-id="32f85-155">또는 **java.io.InputStream**을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-155">Alternatively, a **java.io.InputStream** can be provided.</span></span>

<span data-ttu-id="32f85-156">다음 예제는 위의 코드 조각에서 얻은 `TestTopic` **MessageSender**에 테스트 메시지 5개를 보내는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-156">The following example demonstrates how to send five test messages to the `TestTopic` **MessageSender** we obtained in the code snippet above.</span></span>
<span data-ttu-id="32f85-157">루프가 반복될 때마다 각 메시지의 **MessageNumber** 속성 값이 어떻게 달라지는지 확인합니다(메시지를 수신하는 구독 결정).</span><span class="sxs-lookup"><span data-stu-id="32f85-157">Note how the **MessageNumber** property value of each message varies on the iteration of the loop (this will determine which subscriptions receive it):</span></span>

```java
for (int i=0; i<5; i++)  {
// Create message, passing a string message for the body
BrokeredMessage message = new BrokeredMessage("Test message " + i);
// Set some additional custom app-specific property
message.setProperty("MessageNumber", i);
// Send message to the topic
service.sendTopicMessage("TestTopic", message);
}
```

<span data-ttu-id="32f85-158">Service Bus 토픽은 [표준 계층](service-bus-premium-messaging.md)에서 256KB의 최대 메시지 크기를 [프리미엄 계층](service-bus-premium-messaging.md)에서 1MB를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-158">Service Bus topics support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="32f85-159">표준 및 사용자 지정 응용 프로그램 속성이 포함된 헤더의 최대 크기는 64KB입니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-159">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="32f85-160">한 토픽에 저장되는 메시지 수에는 제한이 없지만 한 토픽에 저장되는 총 메시지 크기는 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-160">There is no limit on the number of messages held in a topic but there is a limit on the total size of the messages held by a topic.</span></span> <span data-ttu-id="32f85-161">이 토픽 크기는 생성 시 정의되며 상한이 5GB입니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-161">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="how-to-receive-messages-from-a-subscription"></a><span data-ttu-id="32f85-162">구독에서 메시지를 받는 방법</span><span class="sxs-lookup"><span data-stu-id="32f85-162">How to receive messages from a subscription</span></span>
<span data-ttu-id="32f85-163">구독에서 메시지를 받으려면 **ServiceBusContract** 개체를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="32f85-163">To receive messages from a subscription, use a **ServiceBusContract** object.</span></span> <span data-ttu-id="32f85-164">받은 메시지는 **ReceiveAndDelete** 및 **PeekLock**의 두 가지 모드로 작동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-164">Received messages can work in two different modes: **ReceiveAndDelete** and **PeekLock**.</span></span>

<span data-ttu-id="32f85-165">**ReceiveAndDelete** 모드를 사용하는 경우 수신은 1단계 작업입니다. 즉, Service Bus가 메시지에 대한 읽기 요청을 받으면 메시지를 이용되는 것으로 표시하고 응용 프로그램에 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-165">When using the **ReceiveAndDelete** mode, receive is a single-shot operation - that is, when Service Bus receives a read request for a message, it marks the message as being consumed and returns it to the application.</span></span> <span data-ttu-id="32f85-166">**ReceiveAndDelete** 모드는 가장 단순한 모델이며, 응용 프로그램이 실패 이벤트 시 메시지를 처리하지 않아도 안전한 시나리오에서 효과적입니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-166">**ReceiveAndDelete** mode is the simplest model and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="32f85-167">이해를 돕기 위해 소비자가 수신 요청을 실행한 후 처리하기 전에 크래시되는 시나리오를 고려해 보세요.</span><span class="sxs-lookup"><span data-stu-id="32f85-167">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="32f85-168">서비스 버스는 메시지를 이용되는 것으로 표시하기 때문에 응용 프로그램이 다시 시작되고 메시지 소비를 다시 시작할 경우 크래시 전에 소비된 메시지가 누락됩니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-168">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="32f85-169">**PeekLock** 모드에서 수신은 2단계 작업이므로 메시지 누락이 허용되지 않는 응용 프로그램을 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-169">In **PeekLock** mode, receive becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="32f85-170">서비스 버스는 요청을 받으면 소비할 다음 메시지를 찾아서 다른 소비자가 수신할 수 없도록 잠근 후 응용 프로그램에 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-170">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span> <span data-ttu-id="32f85-171">응용 프로그램은 메시지 처리를 완료하거나 추가 처리를 위해 안전하게 저장한 후 수신된 메시지에 대해 **Delete**를 호출하여 수신 프로세스의 두 번째 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-171">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling **Delete** on the received message.</span></span> <span data-ttu-id="32f85-172">Service Bus는 **Delete** 호출을 확인한 후 메시지를 이용되는 것으로 표시하고 토픽에서 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-172">When Service Bus sees the **Delete** call, it will mark the message as being consumed and remove it from the topic.</span></span>

<span data-ttu-id="32f85-173">아래 예제에서는 **PeekLock** 모드(기본 모드 아님)를 사용하여 메시지를 받고 처리하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-173">The example below demonstrates how messages can be received and processed using **PeekLock** mode (not the default mode).</span></span> <span data-ttu-id="32f85-174">아래 예는 루프를 수행하고 "HighMessages" 구독 메시지를 처리한 후 추가 메시지가 없으면 종료됩니다(또는 새 메시지를 기다리도록 설정할 수 있음).</span><span class="sxs-lookup"><span data-stu-id="32f85-174">The example below performs a loop and processes messages in the "HighMessages" subscription and then exits when there are no more messages (alternatively, it could be set to wait for new messages).</span></span>

```java
try
{
    ReceiveMessageOptions opts = ReceiveMessageOptions.DEFAULT;
    opts.setReceiveMode(ReceiveMode.PEEK_LOCK);

    while(true)  {
        ReceiveSubscriptionMessageResult  resultSubMsg =
            service.receiveSubscriptionMessage("TestTopic", "HighMessages", opts);
        BrokeredMessage message = resultSubMsg.getValue();
        if (message != null && message.getMessageId() != null)
        {
            System.out.println("MessageID: " + message.getMessageId());
            // Display the topic message.
            System.out.print("From topic: ");
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
                message.getProperty("MessageNumber"));
            // Delete message.
            System.out.println("Deleting this message.");
            service.deleteMessage(message);
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

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="32f85-175">응용 프로그램 작동 중단 및 읽을 수 없는 메시지를 처리하는 방법</span><span class="sxs-lookup"><span data-stu-id="32f85-175">How to handle application crashes and unreadable messages</span></span>
<span data-ttu-id="32f85-176">서비스 버스는 응용 프로그램 오류나 메시지 처리 문제를 정상적으로 복구하는 데 유용한 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-176">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="32f85-177">어떤 이유로든 수신 응용 프로그램이 메시지를 처리할 수 없는 경우 받은 메시지에 대해 **deleteMessage** 메서드 대신 **unlockMessage** 메서드를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-177">If a receiver application is unable to process the message for some reason, then it can call the **unlockMessage** method on the received message (instead of the **deleteMessage** method).</span></span> <span data-ttu-id="32f85-178">그러면 서비스 버스에서 토픽 내 메시지의 잠금을 해제하므로 동일한 소비 응용 프로그램이나 다른 소비 응용 프로그램에서 메시지를 다시 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-178">This will cause Service Bus to unlock the message within the topic and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="32f85-179">토픽 내에서 잠긴 메시지와 연결된 제한 시간도 있으며, 응용 프로그램에서 잠금 제한 시간이 만료되기 전에 메시지를 처리하지 못하는 경우(예: 응용 프로그램이 크래시되는 경우) 서비스 버스가 메시지를 자동으로 잠금 해제하여 다시 받을 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-179">There is also a timeout associated with a message locked within the topic, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus will unlock the message automatically and make it available to be received again.</span></span>

<span data-ttu-id="32f85-180">응용 프로그램이 메시지를 처리한 후 **deleteMessage** 요청이 실행되기 전에 크래시되는 경우 다시 시작될 때 메시지가 응용 프로그램에 다시 배달됩니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-180">In the event that the application crashes after processing the message but before the **deleteMessage** request is issued, then the message will be redelivered to the application when it restarts.</span></span> <span data-ttu-id="32f85-181">이를 **최소 한 번 이상 처리**라고 합니다. 즉, 각 메시지가 최소 한 번 이상 처리되지만 특정 상황에서는 동일한 메시지가 다시 배달될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-181">This is often called **At Least Once Processing**, that is, each message will be processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="32f85-182">중복 처리가 허용되지 않는 시나리오에서는 응용 프로그램 개발자가 중복 메시지 배달을 처리하는 논리를 응용 프로그램에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-182">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span></span> <span data-ttu-id="32f85-183">이 경우 대체로 배달 시도 간에 일정하게 유지되는 메시지의 **getMessageId** 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-183">This is often achieved using the **getMessageId** method of the message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="32f85-184">토픽 및 구독 삭제</span><span class="sxs-lookup"><span data-stu-id="32f85-184">Delete topics and subscriptions</span></span>
<span data-ttu-id="32f85-185">토픽 및 구독을 삭제하는 기본 방법은 **ServiceBusContract** 개체를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-185">The primary way to delete topics and subscriptions is to use a **ServiceBusContract** object.</span></span> <span data-ttu-id="32f85-186">토픽을 삭제하면 토픽에 등록된 모든 구독도 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-186">Deleting a topic will also delete any subscriptions that are registered with the topic.</span></span> <span data-ttu-id="32f85-187">구독을 개별적으로 삭제할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32f85-187">Subscriptions can also be deleted independently.</span></span>

```java
// Delete subscriptions
service.deleteSubscription("TestTopic", "AllMessages");
service.deleteSubscription("TestTopic", "HighMessages");
service.deleteSubscription("TestTopic", "LowMessages");

// Delete a topic
service.deleteTopic("TestTopic");
```

## <a name="next-steps"></a><span data-ttu-id="32f85-188">다음 단계</span><span class="sxs-lookup"><span data-stu-id="32f85-188">Next Steps</span></span>
<span data-ttu-id="32f85-189">지금까지 Service Bus 큐의 기본 사항에 대해 알아보았습니다. 자세한 내용은 [Service Bus 큐, 토픽 및 구독][Service Bus queues, topics, and subscriptions]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="32f85-189">Now that you've learned the basics of Service Bus queues, see [Service Bus queues, topics, and subscriptions][Service Bus queues, topics, and subscriptions] for more information.</span></span>

[Azure SDK for Java]: http://azure.microsoft.com/develop/java/
[Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse.md
[Service Bus queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter 
[SqlFilter.SqlExpression]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter#Microsoft_ServiceBus_Messaging_SqlFilter_SqlExpression
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage

[0]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-13.png
[2]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-04.png
[3]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-09.png

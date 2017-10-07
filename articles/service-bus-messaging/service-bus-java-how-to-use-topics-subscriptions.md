---
title: "Java 통해 aaaHow toouse Azure 서비스 버스 주제 | Microsoft Docs"
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
ms.openlocfilehash: 1aad16fdb5d68a5782b85c8dfda9d695babd57ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-java"></a><span data-ttu-id="2953e-103">어떻게 toouse 서비스 버스 항목 및 Java 통해 구독</span><span class="sxs-lookup"><span data-stu-id="2953e-103">How toouse Service Bus topics and subscriptions with Java</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="2953e-104">이 가이드에서는 설명 방법을 toouse 서비스 버스 항목 및 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="2953e-104">This guide describes how toouse Service Bus topics and subscriptions.</span></span> <span data-ttu-id="2953e-105">hello 샘플 Java 작성 되 고 hello를 사용 하 여 [Azure SDK for Java][Azure SDK for Java]합니다.</span><span class="sxs-lookup"><span data-stu-id="2953e-105">hello samples are written in Java and use hello [Azure SDK for Java][Azure SDK for Java].</span></span> <span data-ttu-id="2953e-106">hello 가이드에서 다루는 시나리오 포함 **항목 및 구독을 만드는**, **구독 필터를 만드는**, **tooa 부분 메시지를 보내는**, **받기 구독에서 메시지**, 및 **항목 및 구독을 삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="2953e-106">hello scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages tooa topic**, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span>

## <a name="what-are-service-bus-topics-and-subscriptions"></a><span data-ttu-id="2953e-107">서비스 버스 토픽 및 구독 정의</span><span class="sxs-lookup"><span data-stu-id="2953e-107">What are Service Bus topics and subscriptions?</span></span>
<span data-ttu-id="2953e-108">서비스 버스 토픽 및 구독은 *게시/구독* 메시징 통신 모델을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="2953e-108">Service Bus topics and subscriptions support a *publish/subscribe* messaging communication model.</span></span> <span data-ttu-id="2953e-109">토픽 및 구독을 사용하는 경우 분산 응용 프로그램의 구성 요소가 서로 직접 통신하지 않고 중간자 역할을 하는 토픽을 통해 메시지를 교환합니다.</span><span class="sxs-lookup"><span data-stu-id="2953e-109">When using topics and subscriptions, components of a distributed application do not communicate directly with each other; instead they exchange messages via a topic, which acts as an intermediary.</span></span>

![TopicConcepts](./media/service-bus-java-how-to-use-topics-subscriptions/sb-topics-01.png)

<span data-ttu-id="2953e-111">각 메시지가 단일 소비자에 의해 처리되는 서비스 버스 큐와 반대로, 토픽과 구독은 게시/구독 패턴을 사용하여 "일 대 다" 형태의 통신을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2953e-111">In contrast with Service Bus queues, in which each message is processed by a single consumer, topics and subscriptions provide a "one-to-many" form of communication, using a publish/subscribe pattern.</span></span> <span data-ttu-id="2953e-112">여러 구독 tooa 항목을 등록 하는 것이 불가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="2953e-112">It is possible to register multiple subscriptions tooa topic.</span></span> <span data-ttu-id="2953e-113">메시지 tooa 항목을 보낼 때 것은 다음 사용할 수 있는 tooeach 구독 toohandle/프로세스 독립적으로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2953e-113">When a message is sent tooa topic, it is then made available tooeach subscription toohandle/process independently.</span></span>

<span data-ttu-id="2953e-114">구독 tooa 항목 toohello 항목 보낸 hello 메시지의 복사본을 받는 가상 큐와 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="2953e-114">A subscription tooa topic resembles a virtual queue that receives copies of hello messages that were sent toohello topic.</span></span> <span data-ttu-id="2953e-115">항목 구독에서 받은 메시지 tooa 주제 toofilter/제한할 수 있는 구독 당 기준 항목에 대 한 필터 규칙을 선택적으로 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2953e-115">You can optionally register filter rules for a topic on a per-subscription basis, which allows you toofilter/restrict which messages tooa topic are received by which topic subscriptions.</span></span>

<span data-ttu-id="2953e-116">서비스 버스 항목 및 구독 사용 하면 tooscale tooprocess는 매우 큰 메시지 수가 매우 많은 수의 사용자와 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="2953e-116">Service Bus topics and subscriptions enable you tooscale tooprocess a very large number of messages across a very large number of users and applications.</span></span>

## <a name="create-a-service-namespace"></a><span data-ttu-id="2953e-117">서비스 네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="2953e-117">Create a service namespace</span></span>
<span data-ttu-id="2953e-118">서비스 버스 항목 및 구독을 사용 하 여 Azure에서 toobegin 먼저 응용 프로그램 내에서 서비스 버스 리소스 주소 지정에 대 한 범위 지정 컨테이너를 제공 하는 네임 스페이스를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2953e-118">toobegin using Service Bus topics and subscriptions in Azure, you must first create a namespace, which provides a scoping container for addressing Service Bus resources within your application.</span></span>

<span data-ttu-id="2953e-119">toocreate 네임 스페이스:</span><span class="sxs-lookup"><span data-stu-id="2953e-119">toocreate a namespace:</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="2953e-120">사용자 응용 프로그램 toouse 서비스 버스를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2953e-120">Configure your application toouse Service Bus</span></span>
<span data-ttu-id="2953e-121">Hello를 설치 했는지 확인 [Azure SDK for Java] [ Azure SDK for Java] 이 샘플을 작성 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="2953e-121">Make sure you have installed hello [Azure SDK for Java][Azure SDK for Java] before building this sample.</span></span> <span data-ttu-id="2953e-122">Eclipse를 사용 하는 경우에 hello을 설치할 수 있습니다 [Azure Toolkit for Eclipse] [ Azure Toolkit for Eclipse] hello Java 용 Azure SDK를 포함 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="2953e-122">If you are using Eclipse, you can install hello [Azure Toolkit for Eclipse][Azure Toolkit for Eclipse] that includes hello Azure SDK for Java.</span></span> <span data-ttu-id="2953e-123">Hello를 추가할 수 있습니다 **Microsoft Azure Libraries for Java** tooyour 프로젝트:</span><span class="sxs-lookup"><span data-stu-id="2953e-123">You can then add hello **Microsoft Azure Libraries for Java** tooyour project:</span></span>

![](media/service-bus-java-how-to-use-topics-subscriptions/eclipselibs.png)

<span data-ttu-id="2953e-124">Hello 다음 추가 `import` 문 toohello 맨 hello Java 파일:</span><span class="sxs-lookup"><span data-stu-id="2953e-124">Add hello following `import` statements toohello top of hello Java file:</span></span>

```java
import com.microsoft.windowsazure.services.servicebus.*;
import com.microsoft.windowsazure.services.servicebus.models.*;
import com.microsoft.windowsazure.core.*;
import javax.xml.datatype.*;
```

<span data-ttu-id="2953e-125">Hello Azure Libraries for Java tooyour 빌드 경로 및 프로젝트 배포 어셈블리에 포함할 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2953e-125">Add hello Azure Libraries for Java tooyour build path and include it in your project deployment assembly.</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="2953e-126">토픽 만들기</span><span class="sxs-lookup"><span data-stu-id="2953e-126">Create a topic</span></span>
<span data-ttu-id="2953e-127">**ServiceBusContract** 클래스를 통해 Service Bus 토픽에 대한 관리 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2953e-127">Management operations for Service Bus topics can be performed via the **ServiceBusContract** class.</span></span> <span data-ttu-id="2953e-128">A **ServiceBusContract** 개체,와 hello toomanage 사용 권한 사용 하 여 SAS 토큰을 캡슐화 하는 적절 한 구성이로 구성 되며 **ServiceBusContract** 클래스는 hello 유일한 지점 Azure와 통신 합니다.</span><span class="sxs-lookup"><span data-stu-id="2953e-128">A **ServiceBusContract** object is constructed with an appropriate configuration that encapsulates the SAS token with permissions toomanage it, and hello **ServiceBusContract** class is hello sole point of communication with Azure.</span></span>

<span data-ttu-id="2953e-129">hello **ServiceBusService** toocreate 메서드를 제공 하는 클래스, 열거 및 항목을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="2953e-129">hello **ServiceBusService** class provides methods toocreate, enumerate, and delete topics.</span></span> <span data-ttu-id="2953e-130">방법을 예제와 다음 hello는 **ServiceBusService** 개체는 명명 된 항목을 사용 하는 toocreate 수 `TestTopic`, 라는 네임 스페이스와 `HowToSample`:</span><span class="sxs-lookup"><span data-stu-id="2953e-130">hello following example shows how a **ServiceBusService** object can be used toocreate a topic named `TestTopic`, with a namespace called `HowToSample`:</span></span>

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

<span data-ttu-id="2953e-131">에 메서드가 있습니다 **TopicInfo** 설정할 hello 항목의 속성 수 있도록 하는 (예: tooset hello 기본 활성 시간 (TTL) 값 적용 toobe toomessages toohello 항목 전송) 합니다.</span><span class="sxs-lookup"><span data-stu-id="2953e-131">There are methods on **TopicInfo** that enable properties of hello topic to be set (for example: tooset hello default time-to-live (TTL) value toobe applied toomessages sent toohello topic).</span></span> <span data-ttu-id="2953e-132">hello 다음 예제에서는 방법과 toocreate 주제 이름 `TestTopic` 5GB의 최대 크기:</span><span class="sxs-lookup"><span data-stu-id="2953e-132">hello following example shows how toocreate a topic named `TestTopic` with a maximum size of 5 GB:</span></span>

```java
long maxSizeInMegabytes = 5120;  
TopicInfo topicInfo = new TopicInfo("TestTopic");  
topicInfo.setMaxSizeInMegabytes(maxSizeInMegabytes);
CreateTopicResult result = service.createTopic(topicInfo);
```

<span data-ttu-id="2953e-133">Hello를 사용할 수 있는 참고 **listTopics** 메서드를 **ServiceBusContract** 서비스 네임 스페이스 내에서 지정한 이름 가진 항목을 이미 있는 경우 toocheck 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="2953e-133">Note that you can use hello **listTopics** method on **ServiceBusContract** objects toocheck if a topic with a specified name already exists within a service namespace.</span></span>

## <a name="create-subscriptions"></a><span data-ttu-id="2953e-134">구독 만들기</span><span class="sxs-lookup"><span data-stu-id="2953e-134">Create subscriptions</span></span>
<span data-ttu-id="2953e-135">Hello로 만들어집니다 구독 tootopics **ServiceBusService** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="2953e-135">Subscriptions tootopics are also created with hello **ServiceBusService** class.</span></span> <span data-ttu-id="2953e-136">이름이 지정 된 구독과 hello toohello 구독의 가상 큐에 전달 된 메시지 집합을 제한 하는 선택적 필터가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2953e-136">Subscriptions are named and can have an optional filter that restricts hello set of messages passed toohello subscription's virtual queue.</span></span>

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a><span data-ttu-id="2953e-137">Hello 기본 (MatchAll) 필터와 구독 만들기</span><span class="sxs-lookup"><span data-stu-id="2953e-137">Create a subscription with hello default (MatchAll) filter</span></span>
<span data-ttu-id="2953e-138">hello **MatchAll** 필터는 필터 지정 하지 않으면은 새 구독을 만들 때 사용 되는 hello 기본 필터.</span><span class="sxs-lookup"><span data-stu-id="2953e-138">hello **MatchAll** filter is hello default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="2953e-139">Hello 때 **MatchAll** 필터 사용 하는 경우 모든 메시지 게시 된 toohello 항목 구독의 가상 큐에 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2953e-139">When hello **MatchAll** filter is used, all messages published toohello topic are placed in the subscription's virtual queue.</span></span> <span data-ttu-id="2953e-140">hello 다음 예제에서는 "AllMessages" 이라는 구독을 만들고 사용 하 여 기본 hello **MatchAll** 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="2953e-140">hello following example creates a subscription named "AllMessages" and uses hello default **MatchAll** filter.</span></span>

```java
SubscriptionInfo subInfo = new SubscriptionInfo("AllMessages");
CreateSubscriptionResult result =
    service.createSubscription("TestTopic", subInfo);
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="2953e-141">필터를 사용하여 구독 만들기</span><span class="sxs-lookup"><span data-stu-id="2953e-141">Create subscriptions with filters</span></span>
<span data-ttu-id="2953e-142">또한 tooscope tooa 항목에 특정 항목을 구독 내에서 표시 됩니다. 보낸 메시지 수 있는 필터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2953e-142">You can also create filters that enable you tooscope which messages sent tooa topic should show up within a specific topic subscription.</span></span>

<span data-ttu-id="2953e-143">hello 가장 유연한 구독에서 지 원하는 필터 형식은 [SqlFilter][SqlFilter], SQL92의 하위 집합을 구현 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="2953e-143">hello most flexible type of filter supported by subscriptions is the [SqlFilter][SqlFilter], which implements a subset of SQL92.</span></span> <span data-ttu-id="2953e-144">SQL 필터가 있는 게시 된 toohello 항목 hello 메시지의 hello 속성에서 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="2953e-144">SQL filters operate on hello properties of hello messages that are published toohello topic.</span></span> <span data-ttu-id="2953e-145">SQL 필터와 함께 사용할 수 있는 hello 식에 대 한 자세한 내용은 hello 검토 [SqlFilter.SqlExpression] [ SqlFilter.SqlExpression] 구문입니다.</span><span class="sxs-lookup"><span data-stu-id="2953e-145">For more details about hello expressions that can be used with a SQL filter, review hello [SqlFilter.SqlExpression][SqlFilter.SqlExpression] syntax.</span></span>

<span data-ttu-id="2953e-146">hello 다음 예제에서는 구독을 만드는 라는 `HighMessages` 와 [SqlFilter] [ SqlFilter] 만 사용자 지정 하는 메시지를 선택 하는 개체 **MessageNumber** 3 보다 큰 속성:</span><span class="sxs-lookup"><span data-stu-id="2953e-146">hello following example creates a subscription named `HighMessages` with a [SqlFilter][SqlFilter] object that only selects messages that have a custom **MessageNumber** property greater than 3:</span></span>

```java
// Create a "HighMessages" filtered subscription  
SubscriptionInfo subInfo = new SubscriptionInfo("HighMessages");
CreateSubscriptionResult result = service.createSubscription("TestTopic", subInfo);
RuleInfo ruleInfo = new RuleInfo("myRuleGT3");
ruleInfo = ruleInfo.withSqlExpressionFilter("MessageNumber > 3");
CreateRuleResult ruleResult = service.createRule("TestTopic", "HighMessages", ruleInfo);
// Delete hello default rule, otherwise hello new rule won't be invoked.
service.deleteRule("TestTopic", "HighMessages", "$Default");
```

<span data-ttu-id="2953e-147">마찬가지로, hello 다음 예제에서는 구독을 만드는 라는 `LowMessages` 와 [SqlFilter] [ SqlFilter] 만 메시지를 선택 하는 개체는 **MessageNumber** 보다 작음 같으면 속성 too3:</span><span class="sxs-lookup"><span data-stu-id="2953e-147">Similarly, hello following example creates a subscription named `LowMessages` with a [SqlFilter][SqlFilter] object that only selects messages that have a **MessageNumber** property less than or equal too3:</span></span>

```java
// Create a "LowMessages" filtered subscription
SubscriptionInfo subInfo = new SubscriptionInfo("LowMessages");
CreateSubscriptionResult result = service.createSubscription("TestTopic", subInfo);
RuleInfo ruleInfo = new RuleInfo("myRuleLE3");
ruleInfo = ruleInfo.withSqlExpressionFilter("MessageNumber <= 3");
CreateRuleResult ruleResult = service.createRule("TestTopic", "LowMessages", ruleInfo);
// Delete hello default rule, otherwise hello new rule won't be invoked.
service.deleteRule("TestTopic", "LowMessages", "$Default");
```

<span data-ttu-id="2953e-148">메시지는 이제 보내면 너무`TestTopic`, 구독 tooreceivers toohello 배달 항상 됩니다 `AllMessages` 구독 및 구독 하는 선택적으로 배달 된 tooreceivers toohello `HighMessages` 및 `LowMessages` 구독 드 ( 내용에 따라 메시지).</span><span class="sxs-lookup"><span data-stu-id="2953e-148">When a message is now sent too`TestTopic`, it will always be delivered tooreceivers subscribed toohello `AllMessages` subscription, and selectively delivered tooreceivers subscribed toohello `HighMessages` and `LowMessages` subscriptions (depending upon the message content).</span></span>

## <a name="send-messages-tooa-topic"></a><span data-ttu-id="2953e-149">Tooa 부분 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="2953e-149">Send messages tooa topic</span></span>
<span data-ttu-id="2953e-150">메시지 tooa 서비스 버스 항목 toosend 프로그램 응용 프로그램 구성 파일을 **ServiceBusContract** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="2953e-150">toosend a message tooa Service Bus topic, your application obtains a **ServiceBusContract** object.</span></span> <span data-ttu-id="2953e-151">hello 다음 코드에서는 방법을 toosend hello에 대 한 메시지 `TestTopic` hello 내에서 이전에 만든 항목 `HowToSample` 네임 스페이스:</span><span class="sxs-lookup"><span data-stu-id="2953e-151">hello following code demonstrates how toosend a message for hello `TestTopic` topic created previously within hello `HowToSample` namespace:</span></span>

```java
BrokeredMessage message = new BrokeredMessage("MyMessage");
service.sendTopicMessage("TestTopic", message);
```

<span data-ttu-id="2953e-152">TooService 버스 주제를 보낸 메시지는의 인스턴스는 [BrokeredMessage] [ BrokeredMessage] 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="2953e-152">Messages sent tooService Bus Topics are instances of the [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="2953e-153">[BrokeredMessage][BrokeredMessage]* 개체는 표준 메서드 집합 (같은 **setLabel** 및 **TimeToLive**), 사용 되는 toohold 사용자 지정 사전 응용 프로그램 관련 속성 및 임의 응용 프로그램 데이터의 본문입니다.</span><span class="sxs-lookup"><span data-stu-id="2953e-153">[BrokeredMessage][BrokeredMessage]* objects have a set of standard methods (such as **setLabel** and **TimeToLive**), a dictionary that is used toohold custom application-specific properties, and a body of arbitrary application data.</span></span> <span data-ttu-id="2953e-154">응용 프로그램의 hello 생성자에 직렬화 된 개체를 전달 하 여 hello 메시지 본문을 설정할 수는 [BrokeredMessage][BrokeredMessage], 및 적절 한 hello **DataContractSerializer**  사용된 tooserialize hello 개체 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2953e-154">An application can set hello body of the message by passing any serializable object into hello constructor of the [BrokeredMessage][BrokeredMessage], and hello appropriate **DataContractSerializer** will then be used tooserialize hello object.</span></span> <span data-ttu-id="2953e-155">또는 **java.io.InputStream**을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2953e-155">Alternatively, a **java.io.InputStream** can be provided.</span></span>

<span data-ttu-id="2953e-156">hello 다음 예제에서는 5 toosend 테스트 toothe 메시지 방법을 `TestTopic` **MessageSender** hello 위의 코드 조각에서 가져온 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2953e-156">hello following example demonstrates how toosend five test messages toothe `TestTopic` **MessageSender** we obtained in hello code snippet above.</span></span>
<span data-ttu-id="2953e-157">참고 어떻게 hello **MessageNumber** hello 루프의 반복 hello에 각 메시지의 속성 값 달라 집니다 (이 결정 합니다 구독 받는):</span><span class="sxs-lookup"><span data-stu-id="2953e-157">Note how hello **MessageNumber** property value of each message varies on hello iteration of hello loop (this will determine which subscriptions receive it):</span></span>

```java
for (int i=0; i<5; i++)  {
// Create message, passing a string message for hello body
BrokeredMessage message = new BrokeredMessage("Test message " + i);
// Set some additional custom app-specific property
message.setProperty("MessageNumber", i);
// Send message toohello topic
service.sendTopicMessage("TestTopic", message);
}
```

<span data-ttu-id="2953e-158">서비스 버스 주제 hello에서 최대 메시지 크기는 256KB 지원 [표준 계층](service-bus-premium-messaging.md) 및 hello에서 1 MB [Premium 계층](service-bus-premium-messaging.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2953e-158">Service Bus topics support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="2953e-159">hello 표준 및 사용자 지정 응용 프로그램 속성을 포함 하는 hello 헤더는 64KB의 최대 크기를 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2953e-159">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="2953e-160">hello 메시지에 항목을 보유할 수에 제한이 있지만 hello 항목을 보유 하는 hello 메시지의 총 크기에 제한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2953e-160">There is no limit on hello number of messages held in a topic but there is a limit on hello total size of hello messages held by a topic.</span></span> <span data-ttu-id="2953e-161">이 토픽 크기는 생성 시 정의되며 상한이 5GB입니다.</span><span class="sxs-lookup"><span data-stu-id="2953e-161">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="how-tooreceive-messages-from-a-subscription"></a><span data-ttu-id="2953e-162">구독에서 tooreceive 메시지 하는 방법</span><span class="sxs-lookup"><span data-stu-id="2953e-162">How tooreceive messages from a subscription</span></span>
<span data-ttu-id="2953e-163">tooreceive 메시지는 구독에서 사용 하 여 한 **ServiceBusContract** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="2953e-163">tooreceive messages from a subscription, use a **ServiceBusContract** object.</span></span> <span data-ttu-id="2953e-164">받은 메시지는 **ReceiveAndDelete** 및 **PeekLock**의 두 가지 모드로 작동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2953e-164">Received messages can work in two different modes: **ReceiveAndDelete** and **PeekLock**.</span></span>

<span data-ttu-id="2953e-165">Hello를 사용 하는 경우 **ReceiveAndDelete** 모드에서는 수신은 1 단계 작업-즉, 서비스 버스 메시지에 대 한 읽기 요청을 받으면 hello 메시지 사용 되는 것을 표시 하 고 toothe 응용 프로그램을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="2953e-165">When using hello **ReceiveAndDelete** mode, receive is a single-shot operation - that is, when Service Bus receives a read request for a message, it marks hello message as being consumed and returns it toothe application.</span></span> <span data-ttu-id="2953e-166">**ReceiveAndDelete** 모드는 hello 가장 간단한 모델 이며는 응용 프로그램은 오류의 hello 이벤트에서 메시지를 처리 하지 허용할 수 없는 시나리오에 가장 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="2953e-166">**ReceiveAndDelete** mode is hello simplest model and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="2953e-167">toounderstand hello는 hello 소비자 문제에 요청을 수신 하는 시나리오 및 후 처리 하기 전에 크래시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2953e-167">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="2953e-168">서비스 버스 사용 되는 것을 다음 hello 응용 프로그램 다시 시작 되 고 메시지 사용을 시작 하는 경우 메시지가 표시 됩니다, 때문에 누락 됩니다 hello 메시지 했던 이전 toohello 크래시를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2953e-168">Because Service Bus will have marked the message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="2953e-169">**PeekLock** 모드에서는 수신 하므로 누락 된 메시지를 허용할 수 없는 가능한 toosupport 응용 프로그램 2 단계 작업이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2953e-169">In **PeekLock** mode, receive becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="2953e-170">서비스 버스 요청을 받으면 다음 메시지 toobe hello 사용 다른 소비자가 수신할 tooprevent 잠근 하 고 toohello 응용 프로그램 반환 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="2953e-170">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="2953e-171">Hello hello의 두 번째 단계를 완료 후 hello 응용 프로그램 hello 메시지 처리를 완료 (또는 이후 처리를 위해 안정적으로 저장)를 호출 하 여 수신 프로세스 **삭제** hello 받은 메시지에 합니다.</span><span class="sxs-lookup"><span data-stu-id="2953e-171">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling **Delete** on hello received message.</span></span> <span data-ttu-id="2953e-172">서비스 버스 hello를 표시 하는 경우 **삭제** 호출 hello 메시지를 사용 되 고 표시 하 고 hello 항목에서 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="2953e-172">When Service Bus sees hello **Delete** call, it will mark hello message as being consumed and remove it from hello topic.</span></span>

<span data-ttu-id="2953e-173">hello 다음 예제에서는 메시지를 수신할 수 방식 및 처리를 사용 하 여 **PeekLock** 모드 (하지 hello 기본 모드).</span><span class="sxs-lookup"><span data-stu-id="2953e-173">hello example below demonstrates how messages can be received and processed using **PeekLock** mode (not hello default mode).</span></span> <span data-ttu-id="2953e-174">hello 아래 예제에서는 루프를 수행 하 고 hello "HighMessages" 구독에서에서 메시지를 처리 하 고 종료 됩니다 메시지가 더 이상 없는 경우 (또는 설정 될 수 toowait 새 메시지에 대 한).</span><span class="sxs-lookup"><span data-stu-id="2953e-174">hello example below performs a loop and processes messages in hello "HighMessages" subscription and then exits when there are no more messages (alternatively, it could be set toowait for new messages).</span></span>

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
            // Display hello topic message.
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
            // Added toohandle no more messages.
            // Could instead wait for more messages toobe added.
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

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="2953e-175">Toohandle 응용 프로그램이 크래시 되는 방법 및 읽을 수 없는 메시지</span><span class="sxs-lookup"><span data-stu-id="2953e-175">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="2953e-176">서비스 버스 기능 toohelp 정상적으로 응용 프로그램 또는 메시지를 처리 하는 데 문제가 오류 로부터 복구를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2953e-176">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="2953e-177">수신기 응용 프로그램 수 없는 경우 몇 가지 이유로 tooprocess 환영 메시지가 다음 hello를 호출할 수 있습니다 **unlockMessage** 메서드를 수신 하는 hello 메시지 (hello 대신 **deleteMessage** 메서드).</span><span class="sxs-lookup"><span data-stu-id="2953e-177">If a receiver application is unable tooprocess hello message for some reason, then it can call hello **unlockMessage** method on hello received message (instead of hello **deleteMessage** method).</span></span> <span data-ttu-id="2953e-178">Hello 항목 내에서 서비스 버스 toounlock hello 메시지 시키며 수신 다시 사용할 수 있는 toobe 확인, 사용자가 여를 많이 사용 응용 프로그램 또는 다른 소비 응용 프로그램에서 동일한 hello 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="2953e-178">This will cause Service Bus toounlock hello message within hello topic and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="2953e-179">또한 항목 내에서 잠긴 메시지와 관련 된 제한 시간 집합과 hello 응용 프로그램 실패 하기 전에 tooprocess hello 메시지 잠금 제한 시간이 만료 (예를 들어 hello 응용 프로그램이 충돌할 경우), 서비스 버스는 hello 메시지 잠금을 자동으로 해제 한 다음 사용할 수 있는 toobe 수신 다시 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2953e-179">There is also a timeout associated with a message locked within the topic, and if hello application fails tooprocess hello message before the lock timeout expires (for example, if hello application crashes), then Service Bus will unlock hello message automatically and make it available toobe received again.</span></span>

<span data-ttu-id="2953e-180">Hello hello 응용 프로그램 이벤트 충돌 hello 메시지 처리 전후에 그러나 hello 전에 **deleteMessage** 요청이 발생 한 후 다시 시작할 때 hello 메시지 다시 전달한 toohello 응용 프로그램 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2953e-180">In hello event that hello application crashes after processing hello message but before hello **deleteMessage** request is issued, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="2953e-181">이 이라고 하는데 **일단 처리 이상**, 즉, 각 메시지가 최소 한 번 처리 되지만 특정 상황 hello에 동일한 메시지를 다시 배달 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2953e-181">This is often called **At Least Once Processing**, that is, each message will be processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="2953e-182">Hello 시나리오 중복 처리가 허용 되지 않는, 응용 프로그램 개발자가 추가 논리 tootheir 응용 프로그램을 toohandle 중복 메시지 배달을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2953e-182">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="2953e-183">이 대개 달성 hello를 사용 하 여 **getMessageId** 메서드 hello 메시지를 배달 시도 간에 일정 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2953e-183">This is often achieved using hello **getMessageId** method of hello message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="2953e-184">토픽 및 구독 삭제</span><span class="sxs-lookup"><span data-stu-id="2953e-184">Delete topics and subscriptions</span></span>
<span data-ttu-id="2953e-185">hello 기본적인 방법은 toodelete 항목 및 구독을 toouse는 **ServiceBusContract** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="2953e-185">hello primary way toodelete topics and subscriptions is toouse a **ServiceBusContract** object.</span></span> <span data-ttu-id="2953e-186">항목 삭제 hello 항목으로 등록 하는 모든 구독도 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2953e-186">Deleting a topic will also delete any subscriptions that are registered with hello topic.</span></span> <span data-ttu-id="2953e-187">구독을 개별적으로 삭제할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2953e-187">Subscriptions can also be deleted independently.</span></span>

```java
// Delete subscriptions
service.deleteSubscription("TestTopic", "AllMessages");
service.deleteSubscription("TestTopic", "HighMessages");
service.deleteSubscription("TestTopic", "LowMessages");

// Delete a topic
service.deleteTopic("TestTopic");
```

## <a name="next-steps"></a><span data-ttu-id="2953e-188">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2953e-188">Next Steps</span></span>
<span data-ttu-id="2953e-189">서비스 버스 큐의 hello 기본 사항 학습 한, 했으므로 참조 [서비스 버스 큐, 항목 및 구독] [ Service Bus queues, topics, and subscriptions] 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="2953e-189">Now that you've learned hello basics of Service Bus queues, see [Service Bus queues, topics, and subscriptions][Service Bus queues, topics, and subscriptions] for more information.</span></span>

[Azure SDK for Java]: http://azure.microsoft.com/develop/java/
[Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse.md
[Service Bus queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter 
[SqlFilter.SqlExpression]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter#Microsoft_ServiceBus_Messaging_SqlFilter_SqlExpression
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage

[0]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-13.png
[2]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-04.png
[3]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-09.png

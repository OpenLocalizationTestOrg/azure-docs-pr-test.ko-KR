---
title: "PHP와 함께 Service Bus 토픽을 사용하는 방법 | Microsoft Docs"
description: "Azure에서 PHP와 함께 Service Bus 토픽을 사용하는 방법에 대해 알아봅니다."
services: service-bus-messaging
documentationcenter: php
author: sethmanheim
manager: timlt
editor: 
ms.assetid: faaa4bbd-f6ef-42ff-aca7-fc4353976449
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/27/2017
ms.author: sethm
ms.openlocfilehash: afa9efcb6335786198021ec81dd087287c39bda9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-service-bus-topics-and-subscriptions-with-php"></a><span data-ttu-id="0f8f2-103">PHP에서 Service Bus 토픽 및 구독을 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="0f8f2-103">How to use Service Bus topics and subscriptions with PHP</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="0f8f2-104">이 문서에서는 Service Bus 토픽과 구독을 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-104">This article shows you how to use Service Bus topics and subscriptions.</span></span> <span data-ttu-id="0f8f2-105">샘플은 PHP로 작성되었으며 [PHP용 Azure SDK](../php-download-sdk.md)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-105">The samples are written in PHP and use the [Azure SDK for PHP](../php-download-sdk.md).</span></span> <span data-ttu-id="0f8f2-106">여기서 다루는 시나리오에는 **토픽 및 구독 만들기**, **구독 필터 만들기**, **토픽에 메시지 보내기**, **구독에서 메시지 받기**, **토픽 및 구독 삭제** 등이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-106">The scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages to a topic**, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="0f8f2-107">PHP 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="0f8f2-107">Create a PHP application</span></span>
<span data-ttu-id="0f8f2-108">Azure Blob service에 액세스하는 PHP 응용 프로그램을 만드는 데 유일한 요구 사항은 코드 내에서 [PHP용 Azure SDK](../php-download-sdk.md)의 클래스를 참조하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-108">The only requirement for creating a PHP application that accesses the Azure Blob service is to reference classes in the [Azure SDK for PHP](../php-download-sdk.md) from within your code.</span></span> <span data-ttu-id="0f8f2-109">어떠한 개발 도구를 사용해도 응용 프로그램 또는 메모장을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-109">You can use any development tools to create your application, or Notepad.</span></span>

> [!NOTE]
> <span data-ttu-id="0f8f2-110">PHP를 설치하려면 [OpenSSL 확장](http://php.net/openssl)도 설치되어 있고 사용하도록 설정되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-110">Your PHP installation must also have the [OpenSSL extension](http://php.net/openssl) installed and enabled.</span></span>
> 
> 

<span data-ttu-id="0f8f2-111">이 항목에서는 PHP 응용 프로그램 내에서 로컬로 또는 Azure 웹 역할, 작업자 역할 또는 웹 사이트 내에서 실행되는 코드에서 호출할 수 있는 서비스 기능을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-111">This article describes how to use service features that can be called within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-the-azure-client-libraries"></a><span data-ttu-id="0f8f2-112">Azure 클라이언트 라이브러리 가져오기</span><span class="sxs-lookup"><span data-stu-id="0f8f2-112">Get the Azure client libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-to-use-service-bus"></a><span data-ttu-id="0f8f2-113">서비스 버스를 사용하도록 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="0f8f2-113">Configure your application to use Service Bus</span></span>
<span data-ttu-id="0f8f2-114">서비스 버스 API를 사용하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-114">To use the Service Bus APIs:</span></span>

1. <span data-ttu-id="0f8f2-115">[require_once][require-once] 문을 사용하여 자동 로더 파일을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-115">Reference the autoloader file using the [require_once][require-once] statement.</span></span>
2. <span data-ttu-id="0f8f2-116">사용할 수 있는 모든 클래스 참조</span><span class="sxs-lookup"><span data-stu-id="0f8f2-116">Reference any classes you might use.</span></span>

<span data-ttu-id="0f8f2-117">다음 예제에서는 자동 로더 파일을 포함하고 **ServiceBusService** 클래스를 참조하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-117">The following example shows how to include the autoloader file and reference the **ServiceBusService** class.</span></span>

> [!NOTE]
> <span data-ttu-id="0f8f2-118">이 예제 및 이 문서의 다른 예제에서는 작성기를 통해 Azure용 PHP 클라이언트 라이브러리를 설치했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-118">This example (and other examples in this article) assumes you have installed the PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="0f8f2-119">라이브러리를 수동으로 또는 PEAR 패키지로 설치한 경우 **WindowsAzure.php** 자동 로더 파일을 참조해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-119">If you installed the libraries manually or as a PEAR package, you must reference the **WindowsAzure.php** autoloader file.</span></span>
> 
> 

```php
require_once 'vendor\autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="0f8f2-120">다음 예제에서 `require_once` 문은 항상 표시되지만 예제를 실행하는 데 필요한 클래스만 참조됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-120">In the following examples, the `require_once` statement will always be shown, but only the classes necessary for the example to execute are referenced.</span></span>

## <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="0f8f2-121">서비스 버스 연결 설정</span><span class="sxs-lookup"><span data-stu-id="0f8f2-121">Set up a Service Bus connection</span></span>
<span data-ttu-id="0f8f2-122">Service Bus 클라이언트를 인스턴스화하려면 먼저 다음 형식의 유효한 연결 문자열이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-122">To instantiate a Service Bus client you must first have a valid connection string in this format:</span></span>

```
Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]
```

<span data-ttu-id="0f8f2-123">여기서 `Endpoint`는 일반적으로 `https://[yourNamespace].servicebus.windows.net` 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-123">Where `Endpoint` is typically of the format `https://[yourNamespace].servicebus.windows.net`.</span></span>

<span data-ttu-id="0f8f2-124">Azure 서비스 클라이언트를 만들려면 `ServicesBuilder` 클래스를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-124">To create any Azure service client you must use the `ServicesBuilder` class.</span></span> <span data-ttu-id="0f8f2-125">다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-125">You can:</span></span>

* <span data-ttu-id="0f8f2-126">연결 문자열을 직접 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-126">Pass the connection string directly to it.</span></span>
* <span data-ttu-id="0f8f2-127">**CCM(CloudConfigurationManager)** 을 사용하여 여러 외부 소스에서 연결 문자열을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-127">Use the **CloudConfigurationManager (CCM)** to check multiple external sources for the connection string:</span></span>
  * <span data-ttu-id="0f8f2-128">기본적으로 하나의 외부 소스, 환경 변수에 대한 지원이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-128">By default it comes with support for one external source - environmental variables.</span></span>
  * <span data-ttu-id="0f8f2-129">`ConnectionStringSource` 클래스를 확장하여 새 소스를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-129">You can add new sources by extending the `ConnectionStringSource` class.</span></span>

<span data-ttu-id="0f8f2-130">여기에 설명된 예제의 경우 연결 문자열이 직접 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-130">For the examples outlined here, the connection string is passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$connectionString = "Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]";

$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);
```

## <a name="create-a-topic"></a><span data-ttu-id="0f8f2-131">토픽 만들기</span><span class="sxs-lookup"><span data-stu-id="0f8f2-131">Create a topic</span></span>
<span data-ttu-id="0f8f2-132">`ServiceBusRestProxy` 클래스를 통해 Service Bus 토픽에 대한 관리 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-132">You can perform management operations for Service Bus topics via the `ServiceBusRestProxy` class.</span></span> <span data-ttu-id="0f8f2-133">`ServiceBusRestProxy` 개체는 관리에 필요한 토큰 사용 권한을 캡슐화하는 적절한 연결 문자열을 사용한 `ServicesBuilder::createServiceBusService` 팩터리 메서드를 통해 구성됩니다. </span><span class="sxs-lookup"><span data-stu-id="0f8f2-133">A `ServiceBusRestProxy` object is constructed via the `ServicesBuilder::createServiceBusService` factory method with an appropriate connection string that encapsulates the token permissions to manage it.</span></span>

<span data-ttu-id="0f8f2-134">다음 예제에서는 `ServiceBusRestProxy`를 인스턴스화하고 `ServiceBusRestProxy->createTopic`을 호출하여 `MySBNamespace` 네임스페이스 내에 이름이 `mytopic`인 토픽을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-134">The following example shows how to instantiate a `ServiceBusRestProxy` and call `ServiceBusRestProxy->createTopic` to create a topic named `mytopic` within a `MySBNamespace` namespace:</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\TopicInfo;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {        
    // Create topic.
    $topicInfo = new TopicInfo("mytopic");
    $serviceBusRestProxy->createTopic($topicInfo);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here: 
    // https://docs.microsoft.com/rest/api/storageservices/Common-REST-API-Error-Codes
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

> [!NOTE]
> <span data-ttu-id="0f8f2-135">`ServiceBusRestProxy` 개체의 `listTopics` 메서드를 사용하여 서비스 네임스페이스 내에 지정된 이름의 토픽이 이미 있는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-135">You can use the `listTopics` method on `ServiceBusRestProxy` objects to check if a topic with a specified name already exists within a service namespace.</span></span>
> 
> 

## <a name="create-a-subscription"></a><span data-ttu-id="0f8f2-136">구독 만들기</span><span class="sxs-lookup"><span data-stu-id="0f8f2-136">Create a subscription</span></span>
<span data-ttu-id="0f8f2-137">토픽 구독은 `ServiceBusRestProxy->createSubscription` 메서드로도 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-137">Topic subscriptions are also created with the `ServiceBusRestProxy->createSubscription` method.</span></span> <span data-ttu-id="0f8f2-138">구독에는 이름이 지정되며, 구독의 가상 큐에 전달되는 메시지 집합을 제한하는 선택적 필터가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-138">Subscriptions are named and can have an optional filter that restricts the set of messages passed to the subscription's virtual queue.</span></span>

### <a name="create-a-subscription-with-the-default-matchall-filter"></a><span data-ttu-id="0f8f2-139">기본(MatchAll) 필터를 사용하여 구독 만들기</span><span class="sxs-lookup"><span data-stu-id="0f8f2-139">Create a subscription with the default (MatchAll) filter</span></span>
<span data-ttu-id="0f8f2-140">**MatchAll** 필터는 새 구독을 만들 때 필터를 지정하지 않은 경우 사용되는 기본 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-140">The **MatchAll** filter is the default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="0f8f2-141">**MatchAll** 필터를 사용하면 토픽에 게시된 모든 메시지가 구독의 가상 큐에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-141">When the **MatchAll** filter is used, all messages published to the topic are placed in the subscription's virtual queue.</span></span> <span data-ttu-id="0f8f2-142">다음 예제에서는 'mysubscription'이라는 구독을 만들고 기본 **MatchAll** 필터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-142">The following example creates a subscription named 'mysubscription' and uses the default **MatchAll** filter.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\SubscriptionInfo;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Create subscription.
    $subscriptionInfo = new SubscriptionInfo("mysubscription");
    $serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here: 
    // https://docs.microsoft.com/rest/api/storageservices/Common-REST-API-Error-Codes
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="0f8f2-143">필터를 사용하여 구독 만들기</span><span class="sxs-lookup"><span data-stu-id="0f8f2-143">Create subscriptions with filters</span></span>
<span data-ttu-id="0f8f2-144">토픽에 전송된 메시지 중 특정 토픽 구독 내에 표시되어야 하는 메시지를 지정하는 필터를 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-144">You can also set up filters that enable you to specify which messages sent to a topic should appear within a specific topic subscription.</span></span> <span data-ttu-id="0f8f2-145">구독에서 지원하는 가장 유연한 유형의 필터는 SQL92 하위 집합을 구현하는 [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter)입니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-145">The most flexible type of filter supported by subscriptions is the [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter), which implements a subset of SQL92.</span></span> <span data-ttu-id="0f8f2-146">SQL 필터는 토픽에 게시된 메시지의 속성에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-146">SQL filters operate on the properties of the messages that are published to the topic.</span></span> <span data-ttu-id="0f8f2-147">SqlFilter에 대한 자세한 내용은 [SqlFilter.SqlExpression 속성][sqlfilter]을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-147">For more information about SqlFilters, see [SqlFilter.SqlExpression Property][sqlfilter].</span></span>

> [!NOTE]
> <span data-ttu-id="0f8f2-148">구독에 대한 각 규칙은 들어오는 메시지를 독립적으로 처리하여 해당 결과 메시지를 구독에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-148">Each rule on a subscription processes incoming messages independently, adding their result messages to the subscription.</span></span> <span data-ttu-id="0f8f2-149">또한 각 새 구독에는 토픽의 모든 메시지를 구독에 추가하는 필터가 포함된 기본 **규칙** 개체가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-149">In addition, each new subscription has a default **Rule** object with a filter that adds all messages from the topic to the subscription.</span></span> <span data-ttu-id="0f8f2-150">필터와 일치하는 메시지만 받으려면 기본 규칙을 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-150">To receive only messages matching your filter, you must remove the default rule.</span></span> <span data-ttu-id="0f8f2-151">`ServiceBusRestProxy->deleteRule` 메서드를 사용하여 기본 규칙을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-151">You can remove the default rule by using the `ServiceBusRestProxy->deleteRule` method.</span></span>
> 
> 

<span data-ttu-id="0f8f2-152">다음 예제에서는 사용자 지정 `MessageNumber` 속성이 3보다 큰 메시지만 선택하는 **SqlFilter**를 사용하여 이름이 `HighMessages`인 구독을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-152">The following example creates a subscription named `HighMessages` with a **SqlFilter** that only selects messages that have a custom `MessageNumber` property greater than 3.</span></span> <span data-ttu-id="0f8f2-153">사용자 지정 속성을 메시지에 추가하는 것과 관련한 정보는 [토픽에 메시지 보내기](#send-messages-to-a-topic)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-153">See [Send messages to a topic](#send-messages-to-a-topic) for information about adding custom properties to messages.</span></span>

```php
$subscriptionInfo = new SubscriptionInfo("HighMessages");
$serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);

$serviceBusRestProxy->deleteRule("mytopic", "HighMessages", '$Default');

$ruleInfo = new RuleInfo("HighMessagesRule");
$ruleInfo->withSqlFilter("MessageNumber > 3");
$ruleResult = $serviceBusRestProxy->createRule("mytopic", "HighMessages", $ruleInfo);
```

<span data-ttu-id="0f8f2-154">이 코드에서는 추가 네임스페이스: `WindowsAzure\ServiceBus\Models\SubscriptionInfo`를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-154">Note that this code requires the use of an additional namespace: `WindowsAzure\ServiceBus\Models\SubscriptionInfo`.</span></span>

<span data-ttu-id="0f8f2-155">마찬가지로, 다음 예제에서는 `MessageNumber` 속성이 3 이하인 메시지만 선택하는 `SqlFilter`가 있는 이름이 `LowMessages`인 구독을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-155">Similarly, the following example creates a subscription named `LowMessages` with a `SqlFilter` that only selects messages that have a `MessageNumber` property less than or equal to 3.</span></span>

```php
$subscriptionInfo = new SubscriptionInfo("LowMessages");
$serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);

$serviceBusRestProxy->deleteRule("mytopic", "LowMessages", '$Default');

$ruleInfo = new RuleInfo("LowMessagesRule");
$ruleInfo->withSqlFilter("MessageNumber <= 3");
$ruleResult = $serviceBusRestProxy->createRule("mytopic", "LowMessages", $ruleInfo);
```

<span data-ttu-id="0f8f2-156">이제 `mytopic` 토픽으로 메시지를 보내는 경우 `mysubscription` 구독을 구독하는 수신자에게는 항상 배달되며, `HighMessages` 및 `LowMessages` 구독을 구독하는 수신자에게는 메시지 내용에 따라 선택적으로 배달됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-156">Now, when a message is sent to the `mytopic` topic, it is always delivered to receivers subscribed to the `mysubscription` subscription, and selectively delivered to receivers subscribed to the `HighMessages` and `LowMessages` subscriptions (depending upon the message content).</span></span>

## <a name="send-messages-to-a-topic"></a><span data-ttu-id="0f8f2-157">토픽에 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="0f8f2-157">Send messages to a topic</span></span>
<span data-ttu-id="0f8f2-158">Service Bus 토픽에 메시지를 보내기 위해 응용 프로그램은 `ServiceBusRestProxy->sendTopicMessage` 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-158">To send a message to a Service Bus topic, your application calls the `ServiceBusRestProxy->sendTopicMessage` method.</span></span> <span data-ttu-id="0f8f2-159">다음 코드는 위에서 `MySBNamespace` 서비스 네임스페이스 내에서 이전에 만든 `mytopic` 토픽에 메시지를 보내는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-159">The following code shows how to send a message to the `mytopic` topic previously created within the `MySBNamespace` service namespace.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\BrokeredMessage;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Create message.
    $message = new BrokeredMessage();
    $message->setBody("my message");

    // Send message.
    $serviceBusRestProxy->sendTopicMessage("mytopic", $message);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here: 
    // https://docs.microsoft.com/rest/api/storageservices/Common-REST-API-Error-Codes
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

<span data-ttu-id="0f8f2-160">Service Bus 토픽으로 전송된 메시지는 [BrokeredMessage][BrokeredMessage] 클래스의 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-160">Messages sent to Service Bus topics are instances of the [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="0f8f2-161">[BrokeredMessage][BrokeredMessage] 개체는 표준 속성 및 메서드 집합과, 응용 프로그램별 사용자 지정 속성을 저장하는 데 사용될 수 있는 속성을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-161">[BrokeredMessage][BrokeredMessage] objects have a set of standard properties and methods, as well as properties that can be used to hold custom application-specific properties.</span></span> <span data-ttu-id="0f8f2-162">다음 예제에서는 이전에 만든 `mytopic` 토픽에 테스트 메시지 5개를 보내는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-162">The following example shows how to send 5 test messages to the `mytopic` topic previously created.</span></span> <span data-ttu-id="0f8f2-163">`setProperty` 메서드는 각 메시지에 사용자 지정 속성(`MessageNumber`)을 추가하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-163">The `setProperty` method is used to add a custom property (`MessageNumber`) to each message.</span></span> <span data-ttu-id="0f8f2-164">참고로 `MessageNumber` 속성 값은 각 메시지에 따라 달라집니다(이 값을 사용하여 [구독 만들기](#create-a-subscription) 섹션에 나타난 대로 메시지를 수신하는 구독을 결정할 수 있음).</span><span class="sxs-lookup"><span data-stu-id="0f8f2-164">Note that the `MessageNumber` property value varies on each message (you can use this value to determine which subscriptions receive it, as shown in the [Create a subscription](#create-a-subscription) section):</span></span>

```php
for($i = 0; $i < 5; $i++){
    // Create message.
    $message = new BrokeredMessage();
    $message->setBody("my message ".$i);

    // Set custom property.
    $message->setProperty("MessageNumber", $i);

    // Send message.
    $serviceBusRestProxy->sendTopicMessage("mytopic", $message);
}
```

<span data-ttu-id="0f8f2-165">Service Bus 토픽은 [표준 계층](service-bus-premium-messaging.md)에서 256KB의 최대 메시지 크기를 [프리미엄 계층](service-bus-premium-messaging.md)에서 1MB를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-165">Service Bus topics support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="0f8f2-166">표준 및 사용자 지정 응용 프로그램 속성이 포함된 헤더의 최대 크기는 64KB입니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-166">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="0f8f2-167">한 토픽에 저장되는 메시지 수에는 제한이 없지만 한 토픽에 저장되는 총 메시지 크기는 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-167">There is no limit on the number of messages held in a topic but there is a cap on the total size of the messages held by a topic.</span></span> <span data-ttu-id="0f8f2-168">토픽 크기의 상한은 5GB입니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-168">This upper limit on topic size is 5 GB.</span></span> <span data-ttu-id="0f8f2-169">할당량에 대한 자세한 내용은 [Service Bus 할당량][Service Bus quotas]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-169">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="0f8f2-170">구독에서 메시지 받기</span><span class="sxs-lookup"><span data-stu-id="0f8f2-170">Receive messages from a subscription</span></span>
<span data-ttu-id="0f8f2-171">구독에서 메시지를 받는 가장 좋은 방법은 `ServiceBusRestProxy->receiveSubscriptionMessage` 메서드를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-171">The best way to receive messages from a subscription is to use a `ServiceBusRestProxy->receiveSubscriptionMessage` method.</span></span> <span data-ttu-id="0f8f2-172">메시지는 [*ReceiveAndDelete* 및 *PeekLock*](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode)의 두 가지 모드로 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-172">Messages can be received in two different modes: [*ReceiveAndDelete* and *PeekLock*](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode).</span></span> <span data-ttu-id="0f8f2-173">**PeekLock**이 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-173">**PeekLock** is the default.</span></span>

<span data-ttu-id="0f8f2-174">[ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) 모드를 사용하는 경우 수신은 1단계 작업입니다. 즉, Service Bus가 구독에서 메시지에 대한 읽기 요청을 받으면 메시지를 사용하는 것으로 표시하고 응용 프로그램에 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-174">When using the [ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, receive is a single-shot operation; that is, when Service Bus receives a read request for a message in a subscription, it marks the message as being consumed and returns it to the application.</span></span> <span data-ttu-id="0f8f2-175">[ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) * 모드는 가장 단순한 모델이며, 응용 프로그램이 실패 이벤트 시 메시지를 처리하지 않아도 안전한 시나리오에서 효과적입니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-175">[ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) * mode is the simplest model and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="0f8f2-176">이해를 돕기 위해 소비자가 수신 요청을 실행한 후 처리하기 전에 크래시되는 시나리오를 고려해 보세요.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-176">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="0f8f2-177">서비스 버스는 메시지를 이용되는 것으로 표시하기 때문에 응용 프로그램이 다시 시작되고 메시지 소비를 다시 시작할 경우 크래시 전에 소비된 메시지가 누락됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-177">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="0f8f2-178">기본값인 [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) 모드에서는 메시지 수신이 2단계 작업이므로 메시지 누락이 허용되지 않는 응용 프로그램을 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-178">In the default [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, receiving a message becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="0f8f2-179">서비스 버스는 요청을 받으면 소비할 다음 메시지를 찾아서 다른 소비자가 수신할 수 없도록 잠근 후 응용 프로그램에 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-179">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span> <span data-ttu-id="0f8f2-180">응용 프로그램은 메시지 처리를 완료하거나 추가 처리를 위해 안전하게 저장한 후에 받은 메시지를 `ServiceBusRestProxy->deleteMessage`에 전달하여 수신 프로세스의 두 번째 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-180">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by passing the received message to `ServiceBusRestProxy->deleteMessage`.</span></span> <span data-ttu-id="0f8f2-181">Service Bus는 `deleteMessage` 호출을 확인한 후 메시지를 이용되는 것으로 표시하고 큐에서 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-181">When Service Bus sees the `deleteMessage` call, it will mark the message as being consumed and remove it from the queue.</span></span>

<span data-ttu-id="0f8f2-182">다음 예제에서는 [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) 모드(기본 모드)를 사용하여 메시지를 받고 처리하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-182">The following example shows how to receive and process a message using [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode (the default mode).</span></span> 

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\ReceiveMessageOptions;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Set receive mode to PeekLock (default is ReceiveAndDelete)
    $options = new ReceiveMessageOptions();
    $options->setPeekLock();

    // Get message.
    $message = $serviceBusRestProxy->receiveSubscriptionMessage("mytopic", "mysubscription", $options);

    echo "Body: ".$message->getBody()."<br />";
    echo "MessageID: ".$message->getMessageId()."<br />";

    /*---------------------------
        Process message here.
    ----------------------------*/

    // Delete message. Not necessary if peek lock is not set.
    echo "Deleting message...<br />";
    $serviceBusRestProxy->deleteMessage($message);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // https://docs.microsoft.com/rest/api/storageservices/Common-REST-API-Error-Codes
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="0f8f2-183">응용 프로그램 작동이 중단되어 메시지를 읽을 수 없는 문제를 처리하는 방법</span><span class="sxs-lookup"><span data-stu-id="0f8f2-183">How to: handle application crashes and unreadable messages</span></span>
<span data-ttu-id="0f8f2-184">서비스 버스는 응용 프로그램 오류나 메시지 처리 문제를 정상적으로 복구하는 데 유용한 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-184">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="0f8f2-185">어떤 이유로든 수신자 응용 프로그램이 메시지를 처리할 수 없는 경우 받은 메시지에 대해 `deleteMessage` 메서드 대신 `unlockMessage` 메서드를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-185">If a receiver application is unable to process the message for some reason, then it can call the `unlockMessage` method on the received message (instead of the `deleteMessage` method).</span></span> <span data-ttu-id="0f8f2-186">그러면 서비스 버스에서 큐 메시지의 잠금을 해제하므로 동일한 소비 응용 프로그램이나 다른 소비 응용 프로그램에서 메시지를 다시 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-186">This will cause Service Bus to unlock the message within the queue and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="0f8f2-187">큐 내에서 잠긴 메시지와 연결된 제한 시간도 있으며, 응용 프로그램에서 잠금 제한 시간이 만료되기 전에 메시지를 처리하지 못하는 경우(예: 응용 프로그램이 크래시되는 경우) 서비스 버스가 메시지를 자동으로 잠금 해제하여 다시 받을 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-187">There is also a timeout associated with a message locked within the queue, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus will unlock the message automatically and make it available to be received again.</span></span>

<span data-ttu-id="0f8f2-188">응용 프로그램이 메시지를 처리한 후 `deleteMessage` 요청이 실행되기 전에 크래시되는 경우 다시 시작될 때 메시지가 응용 프로그램에 다시 배달됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-188">In the event that the application crashes after processing the message but before the `deleteMessage` request is issued, then the message will be redelivered to the application when it restarts.</span></span> <span data-ttu-id="0f8f2-189">이를 *최소 한 번 이상 처리*라고 합니다. 즉, 각 메시지가 최소 한 번 이상 처리되지만 특정 상황에서는 동일한 메시지가 다시 배달될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-189">This is often called *At Least Once* processing; that is, each message is processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="0f8f2-190">중복 처리가 허용되지 않는 시나리오에서는 응용 프로그램 개발자가 중복 메시지 배달을 처리하는 논리를 응용 프로그램에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-190">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to applications to handle duplicate message delivery.</span></span> <span data-ttu-id="0f8f2-191">이 경우 대체로 배달 시도 간에 일정하게 유지되는 메시지의 `getMessageId` 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-191">This is often achieved using the `getMessageId` method of the message, which remains constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="0f8f2-192">토픽 및 구독 삭제</span><span class="sxs-lookup"><span data-stu-id="0f8f2-192">Delete topics and subscriptions</span></span>
<span data-ttu-id="0f8f2-193">토픽이나 구독을 삭제하려면 각각 `ServiceBusRestProxy->deleteTopic` 또는 `ServiceBusRestProxy->deleteSubscripton` 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-193">To delete a topic or a subscription, use the `ServiceBusRestProxy->deleteTopic` or the `ServiceBusRestProxy->deleteSubscripton` methods, respectively.</span></span> <span data-ttu-id="0f8f2-194">참고로 토픽을 삭제하면 토픽에 등록된 모든 구독도 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-194">Note that deleting a topic also deletes any subscriptions that are registered with the topic.</span></span>

<span data-ttu-id="0f8f2-195">다음 예제에서는 이름이 `mytopic`인 토픽 및 등록된 해당 구독을 삭제하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-195">The following example shows how to delete a topic named `mytopic` and its registered subscriptions.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\ServiceBus\ServiceBusService;
use WindowsAzure\ServiceBus\ServiceBusSettings;
use WindowsAzure\Common\ServiceException;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {        
    // Delete topic.
    $serviceBusRestProxy->deleteTopic("mytopic");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here: 
    // https://docs.microsoft.com/rest/api/storageservices/Common-REST-API-Error-Codes
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

<span data-ttu-id="0f8f2-196">`deleteSubscription` 메서드를 사용하여 구독을 독립적으로 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-196">By using the `deleteSubscription` method, you can delete a subscription independently:</span></span>

```php
$serviceBusRestProxy->deleteSubscription("mytopic", "mysubscription");
```

## <a name="next-steps"></a><span data-ttu-id="0f8f2-197">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0f8f2-197">Next steps</span></span>
<span data-ttu-id="0f8f2-198">지금까지 Service Bus 큐의 기본 사항에 대해 알아보았습니다. 자세한 내용은 [큐, 토픽 및 구독][Queues, topics, and subscriptions]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0f8f2-198">Now that you've learned the basics of Service Bus queues, see [Queues, topics, and subscriptions][Queues, topics, and subscriptions] for more information.</span></span>

[BrokeredMessage]: https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[sqlfilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter
[require-once]: http://php.net/require_once
[Service Bus quotas]: service-bus-quotas.md

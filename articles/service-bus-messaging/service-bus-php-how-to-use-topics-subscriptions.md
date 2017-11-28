---
title: "php aaaHow toouse 서비스 버스 주제 | Microsoft Docs"
description: "자세한 내용은 방법 Azure에서 PHP에서 서비스 버스 주제 toouse 합니다."
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
ms.openlocfilehash: 0ca8625fa3edc5854c0d6c1c2f6adab6a2d42f91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-php"></a><span data-ttu-id="c041f-103">어떻게 toouse 서비스 버스 토픽 및 구독 PHP</span><span class="sxs-lookup"><span data-stu-id="c041f-103">How toouse Service Bus topics and subscriptions with PHP</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="c041f-104">이 문서에서는 어떻게 toouse 서비스 버스 항목 및 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="c041f-104">This article shows you how toouse Service Bus topics and subscriptions.</span></span> <span data-ttu-id="c041f-105">hello PHP로 작성 된 100 개의 샘플과 hello를 사용 하 여 [PHP 용 Azure SDK](../php-download-sdk.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c041f-105">hello samples are written in PHP and use hello [Azure SDK for PHP](../php-download-sdk.md).</span></span> <span data-ttu-id="c041f-106">hello 가이드에서 다루는 시나리오 포함 **항목 및 구독을 만드는**, **구독 필터를 만드는**, **tooa 부분 메시지를 보내는**, **받기 구독에서 메시지**, 및 **항목 및 구독을 삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="c041f-106">hello scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages tooa topic**, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="c041f-107">PHP 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="c041f-107">Create a PHP application</span></span>
<span data-ttu-id="c041f-108">hello Azure Blob 서비스에 액세스 하는 PHP 응용 프로그램을 만들기 위한 요구 사항 hello의 tooreference 클래스 파일인 hello [PHP 용 Azure SDK](../php-download-sdk.md) 에서 코드 내에서.</span><span class="sxs-lookup"><span data-stu-id="c041f-108">hello only requirement for creating a PHP application that accesses hello Azure Blob service is tooreference classes in hello [Azure SDK for PHP](../php-download-sdk.md) from within your code.</span></span> <span data-ttu-id="c041f-109">응용 프로그램 또는 메모장 모든 개발 도구 toocreate를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c041f-109">You can use any development tools toocreate your application, or Notepad.</span></span>

> [!NOTE]
> <span data-ttu-id="c041f-110">PHP 설치 hello 있어야 [OpenSSL 확장](http://php.net/openssl) 설치 되어 있고 활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="c041f-110">Your PHP installation must also have hello [OpenSSL extension](http://php.net/openssl) installed and enabled.</span></span>
> 
> 

<span data-ttu-id="c041f-111">이 문서에서는 toouse PHP 응용 프로그램을 로컬로 또는 Azure 웹 역할, 작업자 역할 또는 웹 사이트 내에서 실행 되는 코드에서 호출할 수 있는 기능을 서비스 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c041f-111">This article describes how toouse service features that can be called within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-hello-azure-client-libraries"></a><span data-ttu-id="c041f-112">Hello Azure 클라이언트 라이브러리 가져오기</span><span class="sxs-lookup"><span data-stu-id="c041f-112">Get hello Azure client libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="c041f-113">사용자 응용 프로그램 toouse 서비스 버스를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c041f-113">Configure your application toouse Service Bus</span></span>
<span data-ttu-id="c041f-114">toouse hello 서비스 버스 Api:</span><span class="sxs-lookup"><span data-stu-id="c041f-114">toouse hello Service Bus APIs:</span></span>

1. <span data-ttu-id="c041f-115">Hello를 사용 하 여 참조 hello 자동 로더에 파일 [require_once] [ require-once] 문.</span><span class="sxs-lookup"><span data-stu-id="c041f-115">Reference hello autoloader file using hello [require_once][require-once] statement.</span></span>
2. <span data-ttu-id="c041f-116">사용할 수 있는 모든 클래스 참조</span><span class="sxs-lookup"><span data-stu-id="c041f-116">Reference any classes you might use.</span></span>

<span data-ttu-id="c041f-117">hello 다음 예제에서는 어떻게 tooinclude hello 자동 로더 파일과 참조 hello **ServiceBusService** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="c041f-117">hello following example shows how tooinclude hello autoloader file and reference hello **ServiceBusService** class.</span></span>

> [!NOTE]
> <span data-ttu-id="c041f-118">이 예제 (및이 문서의 다른 예제) 작성기를 통해 Azure에 대 한 hello PHP 클라이언트 라이브러리를 설치 했다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c041f-118">This example (and other examples in this article) assumes you have installed hello PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="c041f-119">수동으로 또는 배 패키지로 hello 라이브러리를 설치 하는 경우에 hello 참조 해야 **WindowsAzure.php** 자동 로더에 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c041f-119">If you installed hello libraries manually or as a PEAR package, you must reference hello **WindowsAzure.php** autoloader file.</span></span>
> 
> 

```php
require_once 'vendor\autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="c041f-120">예제 따르는 hello에서 hello `require_once` hello 예제 tooexecute에 필요한 hello 클래스가 참조 하지만 문에 항상 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c041f-120">In hello following examples, hello `require_once` statement will always be shown, but only hello classes necessary for hello example tooexecute are referenced.</span></span>

## <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="c041f-121">서비스 버스 연결 설정</span><span class="sxs-lookup"><span data-stu-id="c041f-121">Set up a Service Bus connection</span></span>
<span data-ttu-id="c041f-122">이 형식의 올바른 연결 문자열을이 있는 tooinstantiate 먼저 서비스 버스 클라이언트:</span><span class="sxs-lookup"><span data-stu-id="c041f-122">tooinstantiate a Service Bus client you must first have a valid connection string in this format:</span></span>

```
Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]
```

<span data-ttu-id="c041f-123">여기서 `Endpoint` hello 형식의 일반적으로 `https://[yourNamespace].servicebus.windows.net`합니다.</span><span class="sxs-lookup"><span data-stu-id="c041f-123">Where `Endpoint` is typically of hello format `https://[yourNamespace].servicebus.windows.net`.</span></span>

<span data-ttu-id="c041f-124">toocreate hello를 사용 해야 하는 모든 Azure 서비스 클라이언트 `ServicesBuilder` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="c041f-124">toocreate any Azure service client you must use hello `ServicesBuilder` class.</span></span> <span data-ttu-id="c041f-125">다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c041f-125">You can:</span></span>

* <span data-ttu-id="c041f-126">Hello 연결을 통과할 tooit 직접 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="c041f-126">Pass hello connection string directly tooit.</span></span>
* <span data-ttu-id="c041f-127">사용 하 여 hello **CloudConfigurationManager (CCM)** toocheck hello 연결 문자열에 대 한 여러 외부 원본:</span><span class="sxs-lookup"><span data-stu-id="c041f-127">Use hello **CloudConfigurationManager (CCM)** toocheck multiple external sources for hello connection string:</span></span>
  * <span data-ttu-id="c041f-128">기본적으로 하나의 외부 소스, 환경 변수에 대한 지원이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="c041f-128">By default it comes with support for one external source - environmental variables.</span></span>
  * <span data-ttu-id="c041f-129">Hello를 확장 하 여 새 원본을 추가할 수 있습니다 `ConnectionStringSource` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="c041f-129">You can add new sources by extending hello `ConnectionStringSource` class.</span></span>

<span data-ttu-id="c041f-130">Hello 여기에 설명 된 예제를 보려면 hello 연결 문자열은 직접 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="c041f-130">For hello examples outlined here, hello connection string is passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$connectionString = "Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]";

$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);
```

## <a name="create-a-topic"></a><span data-ttu-id="c041f-131">토픽 만들기</span><span class="sxs-lookup"><span data-stu-id="c041f-131">Create a topic</span></span>
<span data-ttu-id="c041f-132">Hello 통해 서비스 버스 주제에 대 한 관리 작업을 수행할 수 `ServiceBusRestProxy` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="c041f-132">You can perform management operations for Service Bus topics via hello `ServiceBusRestProxy` class.</span></span> <span data-ttu-id="c041f-133">A `ServiceBusRestProxy` hello를 통해 개체가 생성 된 `ServicesBuilder::createServiceBusService` hello 토큰 권한 toomanage 캡슐화 하는 적절 한 연결 문자열의 팩터리 메서드 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c041f-133">A `ServiceBusRestProxy` object is constructed via hello `ServicesBuilder::createServiceBusService` factory method with an appropriate connection string that encapsulates hello token permissions toomanage it.</span></span>

<span data-ttu-id="c041f-134">hello 방법을 예제와 다음 tooinstantiate는 `ServiceBusRestProxy` 호출 `ServiceBusRestProxy->createTopic` toocreate 이라는 항목 `mytopic` 내에서 한 `MySBNamespace` 네임 스페이스:</span><span class="sxs-lookup"><span data-stu-id="c041f-134">hello following example shows how tooinstantiate a `ServiceBusRestProxy` and call `ServiceBusRestProxy->createTopic` toocreate a topic named `mytopic` within a `MySBNamespace` namespace:</span></span>

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
> <span data-ttu-id="c041f-135">Hello를 사용할 수 있습니다 `listTopics` 메서드를 `ServiceBusRestProxy` 서비스 네임 스페이스 내에서 지정한 이름 가진 항목을 이미 있는 경우 toocheck 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="c041f-135">You can use hello `listTopics` method on `ServiceBusRestProxy` objects toocheck if a topic with a specified name already exists within a service namespace.</span></span>
> 
> 

## <a name="create-a-subscription"></a><span data-ttu-id="c041f-136">구독 만들기</span><span class="sxs-lookup"><span data-stu-id="c041f-136">Create a subscription</span></span>
<span data-ttu-id="c041f-137">주제 구독에도 hello를 사용 하 여 만들어진 `ServiceBusRestProxy->createSubscription` 메서드.</span><span class="sxs-lookup"><span data-stu-id="c041f-137">Topic subscriptions are also created with hello `ServiceBusRestProxy->createSubscription` method.</span></span> <span data-ttu-id="c041f-138">이름이 지정 된 구독과 hello toohello 구독의 가상 큐에 전달 된 메시지 집합을 제한 하는 선택적 필터가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c041f-138">Subscriptions are named and can have an optional filter that restricts hello set of messages passed toohello subscription's virtual queue.</span></span>

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a><span data-ttu-id="c041f-139">Hello 기본 (MatchAll) 필터와 구독 만들기</span><span class="sxs-lookup"><span data-stu-id="c041f-139">Create a subscription with hello default (MatchAll) filter</span></span>
<span data-ttu-id="c041f-140">hello **MatchAll** 필터는 필터 지정 하지 않으면은 새 구독을 만들 때 사용 되는 hello 기본 필터.</span><span class="sxs-lookup"><span data-stu-id="c041f-140">hello **MatchAll** filter is hello default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="c041f-141">Hello 때 **MatchAll** 필터 사용 하는 경우 모든 부분 메시지 게시 된 toohello hello 구독의 가상 큐에 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c041f-141">When hello **MatchAll** filter is used, all messages published toohello topic are placed in hello subscription's virtual queue.</span></span> <span data-ttu-id="c041f-142">hello 다음 예제에서는 'mysubscription' 이라는 구독을 만들고 사용 하 여 기본 hello **MatchAll** 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="c041f-142">hello following example creates a subscription named 'mysubscription' and uses hello default **MatchAll** filter.</span></span>

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

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="c041f-143">필터를 사용하여 구독 만들기</span><span class="sxs-lookup"><span data-stu-id="c041f-143">Create subscriptions with filters</span></span>
<span data-ttu-id="c041f-144">Toospecify tooa 항목 특정 항목을 구독 내에서 표시 되어야 보낸 메시지 수 있도록 하는 필터를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c041f-144">You can also set up filters that enable you toospecify which messages sent tooa topic should appear within a specific topic subscription.</span></span> <span data-ttu-id="c041f-145">hello 가장 유연한 구독에서 지 원하는 필터 형식은 hello [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter)를 구현 하는 SQL92의 하위 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="c041f-145">hello most flexible type of filter supported by subscriptions is hello [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter), which implements a subset of SQL92.</span></span> <span data-ttu-id="c041f-146">SQL 필터가 있는 게시 된 toohello 항목 hello 메시지의 hello 속성에서 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="c041f-146">SQL filters operate on hello properties of hello messages that are published toohello topic.</span></span> <span data-ttu-id="c041f-147">SqlFilter에 대한 자세한 내용은 [SqlFilter.SqlExpression 속성][sqlfilter]을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="c041f-147">For more information about SqlFilters, see [SqlFilter.SqlExpression Property][sqlfilter].</span></span>

> [!NOTE]
> <span data-ttu-id="c041f-148">구독에 각 규칙 하지 들어오는 메시지를 처리, 독립적으로 해당 결과 메시지 toohello 구독을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c041f-148">Each rule on a subscription processes incoming messages independently, adding their result messages toohello subscription.</span></span> <span data-ttu-id="c041f-149">또한, 각각의 새 구독에는 기본 **규칙** hello 항목 toohello 구독에서 모든 메시지를 추가 하는 필터를 사용 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="c041f-149">In addition, each new subscription has a default **Rule** object with a filter that adds all messages from hello topic toohello subscription.</span></span> <span data-ttu-id="c041f-150">tooreceive만 메시지 필터와 일치 하는 hello 기본 규칙을 제거 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c041f-150">tooreceive only messages matching your filter, you must remove hello default rule.</span></span> <span data-ttu-id="c041f-151">Hello를 사용 하 여 hello 기본 규칙을 제거할 수 있습니다 `ServiceBusRestProxy->deleteRule` 메서드.</span><span class="sxs-lookup"><span data-stu-id="c041f-151">You can remove hello default rule by using hello `ServiceBusRestProxy->deleteRule` method.</span></span>
> 
> 

<span data-ttu-id="c041f-152">hello 다음 예제에서는 구독을 만드는 라는 `HighMessages` 와 **SqlFilter** 만 사용자 지정 하는 메시지를 선택 하는 `MessageNumber` 3 보다 큰 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="c041f-152">hello following example creates a subscription named `HighMessages` with a **SqlFilter** that only selects messages that have a custom `MessageNumber` property greater than 3.</span></span> <span data-ttu-id="c041f-153">참조 [송신 메시지 tooa 항목](#send-messages-to-a-topic) toomessages 사용자 지정 속성을 추가 하는 방법에 대 한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c041f-153">See [Send messages tooa topic](#send-messages-to-a-topic) for information about adding custom properties toomessages.</span></span>

```php
$subscriptionInfo = new SubscriptionInfo("HighMessages");
$serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);

$serviceBusRestProxy->deleteRule("mytopic", "HighMessages", '$Default');

$ruleInfo = new RuleInfo("HighMessagesRule");
$ruleInfo->withSqlFilter("MessageNumber > 3");
$ruleResult = $serviceBusRestProxy->createRule("mytopic", "HighMessages", $ruleInfo);
```

<span data-ttu-id="c041f-154">이 코드를 추가 네임 스페이스의 hello 사용 해야 함을 참고: `WindowsAzure\ServiceBus\Models\SubscriptionInfo`합니다.</span><span class="sxs-lookup"><span data-stu-id="c041f-154">Note that this code requires hello use of an additional namespace: `WindowsAzure\ServiceBus\Models\SubscriptionInfo`.</span></span>

<span data-ttu-id="c041f-155">마찬가지로, hello 다음 예제에서는 구독을 만드는 라는 `LowMessages` 와 `SqlFilter` 만 설정 된 메시지를 선택 하는 `MessageNumber` 속성 작은 보다 짧거나 too3 합니다.</span><span class="sxs-lookup"><span data-stu-id="c041f-155">Similarly, hello following example creates a subscription named `LowMessages` with a `SqlFilter` that only selects messages that have a `MessageNumber` property less than or equal too3.</span></span>

```php
$subscriptionInfo = new SubscriptionInfo("LowMessages");
$serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);

$serviceBusRestProxy->deleteRule("mytopic", "LowMessages", '$Default');

$ruleInfo = new RuleInfo("LowMessagesRule");
$ruleInfo->withSqlFilter("MessageNumber <= 3");
$ruleResult = $serviceBusRestProxy->createRule("mytopic", "LowMessages", $ruleInfo);
```

<span data-ttu-id="c041f-156">이제 메시지를 보내면 toohello `mytopic` 항목을 항상 제공 된다는 구독 tooreceivers toohello `mysubscription` 구독 및 구독 하는 선택적으로 배달 된 tooreceivers toohello `HighMessages` 및 `LowMessages` 구독 드 ( 에 따라 hello 메시지 내용을).</span><span class="sxs-lookup"><span data-stu-id="c041f-156">Now, when a message is sent toohello `mytopic` topic, it is always delivered tooreceivers subscribed toohello `mysubscription` subscription, and selectively delivered tooreceivers subscribed toohello `HighMessages` and `LowMessages` subscriptions (depending upon hello message content).</span></span>

## <a name="send-messages-tooa-topic"></a><span data-ttu-id="c041f-157">Tooa 부분 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="c041f-157">Send messages tooa topic</span></span>
<span data-ttu-id="c041f-158">메시지 tooa 서비스 버스 항목 toosend 응용 프로그램 호출 hello `ServiceBusRestProxy->sendTopicMessage` 메서드.</span><span class="sxs-lookup"><span data-stu-id="c041f-158">toosend a message tooa Service Bus topic, your application calls hello `ServiceBusRestProxy->sendTopicMessage` method.</span></span> <span data-ttu-id="c041f-159">코드에서 보여 주는 방법을 다음 hello 메시지 toohello toosend `mytopic` 항목 내에서 이전에 만든는 `MySBNamespace` 서비스 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="c041f-159">hello following code shows how toosend a message toohello `mytopic` topic previously created within the `MySBNamespace` service namespace.</span></span>

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

<span data-ttu-id="c041f-160">메시지가 전송 tooService 버스 주제는 hello 인스턴스의 [BrokeredMessage] [ BrokeredMessage] 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="c041f-160">Messages sent tooService Bus topics are instances of hello [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="c041f-161">[BrokeredMessage] [ BrokeredMessage] 개체 표준 속성 및 메서드 뿐 아니라 사용자 지정 응용 프로그램 특정 속성 사용된 toohold 될 수 있는 속성 집합이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c041f-161">[BrokeredMessage][BrokeredMessage] objects have a set of standard properties and methods, as well as properties that can be used toohold custom application-specific properties.</span></span> <span data-ttu-id="c041f-162">hello 다음 예제에서는 5 toosend 테스트 toohello 메시지 방법을 `mytopic` 이전에 만든 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="c041f-162">hello following example shows how toosend 5 test messages toohello `mytopic` topic previously created.</span></span> <span data-ttu-id="c041f-163">hello `setProperty` 메서드는 사용 되는 tooadd 사용자 지정 속성 (`MessageNumber`) tooeach 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="c041f-163">hello `setProperty` method is used tooadd a custom property (`MessageNumber`) tooeach message.</span></span> <span data-ttu-id="c041f-164">해당 hello 참고 `MessageNumber` 각 메시지에 속성 값에 따라 다릅니다 (hello에 나와 있는 것 처럼 구독 받는 값 toodetermine이를 사용할 수 있습니다 [구독을 만들](#create-a-subscription) 섹션):</span><span class="sxs-lookup"><span data-stu-id="c041f-164">Note that hello `MessageNumber` property value varies on each message (you can use this value toodetermine which subscriptions receive it, as shown in hello [Create a subscription](#create-a-subscription) section):</span></span>

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

<span data-ttu-id="c041f-165">서비스 버스 주제 hello에서 최대 메시지 크기는 256KB 지원 [표준 계층](service-bus-premium-messaging.md) 및 hello에서 1 MB [Premium 계층](service-bus-premium-messaging.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c041f-165">Service Bus topics support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="c041f-166">hello 표준 및 사용자 지정 응용 프로그램 속성을 포함 하는 hello 헤더는 64KB의 최대 크기를 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c041f-166">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="c041f-167">Hello 메시지에 항목을 보유할 수에 제한이 없음을 않으며 항목을 보유 하는 hello 메시지의 총 크기 hello 켜져 캡입니다.</span><span class="sxs-lookup"><span data-stu-id="c041f-167">There is no limit on hello number of messages held in a topic but there is a cap on hello total size of hello messages held by a topic.</span></span> <span data-ttu-id="c041f-168">토픽 크기의 상한은 5GB입니다.</span><span class="sxs-lookup"><span data-stu-id="c041f-168">This upper limit on topic size is 5 GB.</span></span> <span data-ttu-id="c041f-169">할당량에 대한 자세한 내용은 [Service Bus 할당량][Service Bus quotas]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c041f-169">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="c041f-170">구독에서 메시지 받기</span><span class="sxs-lookup"><span data-stu-id="c041f-170">Receive messages from a subscription</span></span>
<span data-ttu-id="c041f-171">구독에서 hello 가장 좋은 방법은 tooreceive 메시지는 toouse는 `ServiceBusRestProxy->receiveSubscriptionMessage` 메서드.</span><span class="sxs-lookup"><span data-stu-id="c041f-171">hello best way tooreceive messages from a subscription is toouse a `ServiceBusRestProxy->receiveSubscriptionMessage` method.</span></span> <span data-ttu-id="c041f-172">메시지는 [*ReceiveAndDelete* 및 *PeekLock*](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode)의 두 가지 모드로 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c041f-172">Messages can be received in two different modes: [*ReceiveAndDelete* and *PeekLock*](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode).</span></span> <span data-ttu-id="c041f-173">**PeekLock** hello 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="c041f-173">**PeekLock** is hello default.</span></span>

<span data-ttu-id="c041f-174">Hello를 사용 하는 경우 [ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) 모드에서는 수신은 1 단계 작업입니다; 즉, 서비스 버스 구독에서 메시지에 대 한 읽기 요청을 받으면 hello 메시지 사용 되는 것을 표시 하 고 toohello 반환 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="c041f-174">When using hello [ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, receive is a single-shot operation; that is, when Service Bus receives a read request for a message in a subscription, it marks hello message as being consumed and returns it toohello application.</span></span> <span data-ttu-id="c041f-175">[ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) * 모드는 hello 가장 간단한 모델 이며는 응용 프로그램은 오류의 hello 이벤트에서 메시지를 처리 하지 허용할 수 없는 시나리오에 가장 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="c041f-175">[ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) * mode is hello simplest model and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="c041f-176">toounderstand hello는 hello 소비자 문제에 요청을 수신 하는 시나리오 및 후 처리 하기 전에 크래시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c041f-176">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="c041f-177">서비스 버스 사용 되는 것을 다음 hello 응용 프로그램 다시 시작 되 고 메시지 사용을 시작할 때 hello 메시지를 표시 한 됩니다, 때문에 누락 됩니다 hello 메시지 했던 이전 toohello 크래시를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c041f-177">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="c041f-178">Hello 기본에서 [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) 모드에서는 메시지를 표시 하므로 누락 된 메시지를 허용할 수 없는 가능한 toosupport 응용 프로그램 2 단계 작업을 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c041f-178">In hello default [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, receiving a message becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="c041f-179">서비스 버스 요청을 받으면 다음 메시지 toobe hello 사용 다른 소비자가 수신할 tooprevent 잠근 하 고 toohello 응용 프로그램 반환 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="c041f-179">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="c041f-180">Hello hello의 두 번째 단계를 완료 hello 응용 프로그램 hello 메시지 처리를 완료 (또는 이후 처리를 위해 안정적으로 저장) 한 후 너무 hello 받은 메시지를 전달 하 여 수신 프로세스`ServiceBusRestProxy->deleteMessage`합니다.</span><span class="sxs-lookup"><span data-stu-id="c041f-180">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by passing hello received message too`ServiceBusRestProxy->deleteMessage`.</span></span> <span data-ttu-id="c041f-181">서비스 버스 hello를 표시 하는 경우 `deleteMessage` 호출 hello 메시지를 사용 되 고 표시 하 고 hello 큐에서 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="c041f-181">When Service Bus sees hello `deleteMessage` call, it will mark hello message as being consumed and remove it from hello queue.</span></span>

<span data-ttu-id="c041f-182">hello 방법을 예제와 다음 tooreceive 하 고 사용 하 여 메시지 처리 [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) 모드 (hello 기본 모드).</span><span class="sxs-lookup"><span data-stu-id="c041f-182">hello following example shows how tooreceive and process a message using [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode (hello default mode).</span></span> 

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\ReceiveMessageOptions;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Set receive mode tooPeekLock (default is ReceiveAndDelete)
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

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="c041f-183">응용 프로그램 작동이 중단되어 메시지를 읽을 수 없는 문제를 처리하는 방법</span><span class="sxs-lookup"><span data-stu-id="c041f-183">How to: handle application crashes and unreadable messages</span></span>
<span data-ttu-id="c041f-184">서비스 버스 기능 toohelp 정상적으로 응용 프로그램 또는 메시지를 처리 하는 데 문제가 오류 로부터 복구를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c041f-184">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="c041f-185">수신기 응용 프로그램 수 없는 경우 몇 가지 이유로 tooprocess 환영 메시지가 다음 hello를 호출할 수 있습니다 `unlockMessage` 메서드를 수신 하는 hello 메시지 (hello 대신 `deleteMessage` 메서드).</span><span class="sxs-lookup"><span data-stu-id="c041f-185">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlockMessage` method on hello received message (instead of hello `deleteMessage` method).</span></span> <span data-ttu-id="c041f-186">Hello 큐 내에서 서비스 버스 toounlock hello 메시지 시키며 수신 다시 사용할 수 있는 toobe 확인, 사용자가 여를 많이 사용 응용 프로그램 또는 다른 소비 응용 프로그램에서 동일한 hello 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="c041f-186">This will cause Service Bus toounlock hello message within hello queue and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="c041f-187">또한 hello 큐 내에서 잠긴 메시지와 관련 된 제한 시간 집합과 hello 응용 프로그램 실패 하기 전에 hello 메시지 tooprocess hello 잠금 제한 시간이 만료 (예를 들어 hello 응용 프로그램이 충돌할 경우), 서비스 버스에서 hello 메시지를 잠금 해제 한 다음 자동으로 사용할 수 있는 toobe 수신 다시 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c041f-187">There is also a timeout associated with a message locked within hello queue, and if hello application fails tooprocess hello message before hello lock timeout expires (for example, if hello application crashes), then Service Bus will unlock hello message automatically and make it available toobe received again.</span></span>

<span data-ttu-id="c041f-188">Hello hello 응용 프로그램 이벤트 충돌 hello 메시지 처리 전후에 그러나 hello 전에 `deleteMessage` 요청이 발생 한 후 다시 시작할 때 hello 메시지 다시 전달한 toohello 응용 프로그램 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c041f-188">In hello event that hello application crashes after processing hello message but before hello `deleteMessage` request is issued, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="c041f-189">이 이라고 하는데 *최소 한 번* 처리; 즉, 각 메시지는 한 번 이상 처리 되지만 특정 상황 hello에 동일한 메시지를 다시 배달 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c041f-189">This is often called *At Least Once* processing; that is, each message is processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="c041f-190">Hello 시나리오 중복 처리가 허용 되지 않는, 응용 프로그램 개발자가 tooapplications toohandle 중복 메시지 배달 추가 논리를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c041f-190">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tooapplications toohandle duplicate message delivery.</span></span> <span data-ttu-id="c041f-191">이 대개 달성 hello를 사용 하 여 `getMessageId` 메서드 hello 메시지를 배달 시도에서 일관적으로 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="c041f-191">This is often achieved using hello `getMessageId` method of hello message, which remains constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="c041f-192">토픽 및 구독 삭제</span><span class="sxs-lookup"><span data-stu-id="c041f-192">Delete topics and subscriptions</span></span>
<span data-ttu-id="c041f-193">항목 또는 구독을 사용 하 여 hello toodelete `ServiceBusRestProxy->deleteTopic` 또는 hello `ServiceBusRestProxy->deleteSubscripton` 메서드를 각각.</span><span class="sxs-lookup"><span data-stu-id="c041f-193">toodelete a topic or a subscription, use hello `ServiceBusRestProxy->deleteTopic` or hello `ServiceBusRestProxy->deleteSubscripton` methods, respectively.</span></span> <span data-ttu-id="c041f-194">Note는 항목을 삭제 하면 hello 항목으로 등록 하는 모든 구독도 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="c041f-194">Note that deleting a topic also deletes any subscriptions that are registered with hello topic.</span></span>

<span data-ttu-id="c041f-195">hello 다음 예제에서는 방법과 toodelete 주제 이름 `mytopic` 및 등록 된 구독에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="c041f-195">hello following example shows how toodelete a topic named `mytopic` and its registered subscriptions.</span></span>

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

<span data-ttu-id="c041f-196">Hello를 사용 하 여 `deleteSubscription` 메서드를 하면 구독을 삭제 하지 독립적으로:</span><span class="sxs-lookup"><span data-stu-id="c041f-196">By using hello `deleteSubscription` method, you can delete a subscription independently:</span></span>

```php
$serviceBusRestProxy->deleteSubscription("mytopic", "mysubscription");
```

## <a name="next-steps"></a><span data-ttu-id="c041f-197">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c041f-197">Next steps</span></span>
<span data-ttu-id="c041f-198">서비스 버스 큐의 hello 기본 사항 학습 한, 했으므로 참조 [큐, 토픽 및 구독] [ Queues, topics, and subscriptions] 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c041f-198">Now that you've learned hello basics of Service Bus queues, see [Queues, topics, and subscriptions][Queues, topics, and subscriptions] for more information.</span></span>

[BrokeredMessage]: https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[sqlfilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter
[require-once]: http://php.net/require_once
[Service Bus quotas]: service-bus-quotas.md

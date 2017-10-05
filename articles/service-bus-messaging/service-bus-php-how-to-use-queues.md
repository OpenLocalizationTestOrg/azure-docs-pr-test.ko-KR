---
title: "PHP에서 Service Bus 큐를 사용하는 방법 | Microsoft Docs"
description: "Azure에서 서비스 버스 큐를 사용하는 방법에 대해 알아봅니다. 코드 샘플은 PHP로 작성되었습니다."
services: service-bus-messaging
documentationcenter: php
author: sethmanheim
manager: timlt
editor: 
ms.assetid: e29c829b-44c5-4350-8f2e-39e0c380a9f2
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 3514812f7f087582035dad5d9a4d620652aa4da9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-service-bus-queues-with-php"></a><span data-ttu-id="1ea69-104">PHP에서 Service Bus 큐를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="1ea69-104">How to use Service Bus queues with PHP</span></span>
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="1ea69-105">이 가이드에서는 서비스 버스 큐를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1ea69-105">This guide shows you how to use Service Bus queues.</span></span> <span data-ttu-id="1ea69-106">샘플은 PHP로 작성되었으며 [PHP용 Azure SDK](../php-download-sdk.md)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1ea69-106">The samples are written in PHP and use the [Azure SDK for PHP](../php-download-sdk.md).</span></span> <span data-ttu-id="1ea69-107">여기서 다루는 시나리오에는 **큐 만들기**, **메시지 보내기 및 받기**, **큐 삭제** 등이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ea69-107">The scenarios covered include **creating queues**, **sending and receiving messages**, and **deleting queues**.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="1ea69-108">PHP 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="1ea69-108">Create a PHP application</span></span>
<span data-ttu-id="1ea69-109">Azure Blob service에 액세스하는 PHP 응용 프로그램을 만드는 데 유일한 요구 사항은 코드 내에서 [PHP용 Azure SDK](../php-download-sdk.md)의 클래스를 참조하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1ea69-109">The only requirement for creating a PHP application that accesses the Azure Blob service is the referencing of classes in the [Azure SDK for PHP](../php-download-sdk.md) from within your code.</span></span> <span data-ttu-id="1ea69-110">어떠한 개발 도구를 사용해도 응용 프로그램 또는 메모장을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ea69-110">You can use any development tools to create your application, or Notepad.</span></span>

> [!NOTE]
> <span data-ttu-id="1ea69-111">PHP를 설치하려면 [OpenSSL 확장](http://php.net/openssl)도 설치되어 있고 사용하도록 설정되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ea69-111">Your PHP installation must also have the [OpenSSL extension](http://php.net/openssl) installed and enabled.</span></span>
> 
> 

<span data-ttu-id="1ea69-112">이 가이드에서는 PHP 응용 프로그램 내에서 로컬로 또는 Azure 웹 역할, 작업자 역할 또는 웹 사이트 내에서 실행되는 코드에서 호출할 수 있는 서비스 기능을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1ea69-112">In this guide, you will use service features which can be called from within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-the-azure-client-libraries"></a><span data-ttu-id="1ea69-113">Azure 클라이언트 라이브러리 가져오기</span><span class="sxs-lookup"><span data-stu-id="1ea69-113">Get the Azure client libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-to-use-service-bus"></a><span data-ttu-id="1ea69-114">서비스 버스를 사용하도록 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="1ea69-114">Configure your application to use Service Bus</span></span>
<span data-ttu-id="1ea69-115">서비스 버스 큐 API를 사용하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1ea69-115">To use the Service Bus queue APIs, do the following:</span></span>

1. <span data-ttu-id="1ea69-116">[require_once][require_once] 문을 사용하여 자동 로더 파일을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="1ea69-116">Reference the autoloader file using the [require_once][require_once] statement.</span></span>
2. <span data-ttu-id="1ea69-117">사용할 수 있는 모든 클래스 참조</span><span class="sxs-lookup"><span data-stu-id="1ea69-117">Reference any classes you might use.</span></span>

<span data-ttu-id="1ea69-118">다음 예제에서는 자동 로더 파일을 포함하고 `ServicesBuilder` 클래스를 참조하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1ea69-118">The following example shows how to include the autoloader file and reference the `ServicesBuilder` class.</span></span>

> [!NOTE]
> <span data-ttu-id="1ea69-119">이 예제 및 이 문서의 다른 예제에서는 작성기를 통해 Azure용 PHP 클라이언트 라이브러리를 설치했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="1ea69-119">This example (and other examples in this article) assumes you have installed the PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="1ea69-120">라이브러리를 수동으로 또는 PEAR 패키지로 설치한 경우 **WindowsAzure.php** 자동 로더 파일을 참조해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ea69-120">If you installed the libraries manually or as a PEAR package, you must reference the **WindowsAzure.php** autoloader file.</span></span>
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="1ea69-121">아래 예제에서 `require_once` 문은 항상 표시되지만 예제를 실행하는 데 필요한 클래스만 참조됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ea69-121">In the examples below, the `require_once` statement will always be shown, but only the classes necessary for the example to execute are referenced.</span></span>

## <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="1ea69-122">서비스 버스 연결 설정</span><span class="sxs-lookup"><span data-stu-id="1ea69-122">Set up a Service Bus connection</span></span>
<span data-ttu-id="1ea69-123">서비스 버스 클라이언트를 인스턴스화하려면 먼저 다음 형식의 유효한 연결 문자열이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ea69-123">To instantiate a Service Bus client, you must first have a valid connection string in this format:</span></span>

```
Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]
```

<span data-ttu-id="1ea69-124">여기서 `Endpoint`는 일반적으로 `[yourNamespace].servicebus.windows.net` 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="1ea69-124">Where `Endpoint` is typically of the format `[yourNamespace].servicebus.windows.net`.</span></span>

<span data-ttu-id="1ea69-125">Azure 서비스 클라이언트를 만들려면 `ServicesBuilder` 클래스를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ea69-125">To create any Azure service client you must use the `ServicesBuilder` class.</span></span> <span data-ttu-id="1ea69-126">다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ea69-126">You can:</span></span>

* <span data-ttu-id="1ea69-127">연결 문자열을 직접 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="1ea69-127">Pass the connection string directly to it.</span></span>
* <span data-ttu-id="1ea69-128">**CCM(CloudConfigurationManager)** 을 사용하여 여러 외부 소스에서 연결 문자열을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ea69-128">Use the **CloudConfigurationManager (CCM)** to check multiple external sources for the connection string:</span></span>
  * <span data-ttu-id="1ea69-129">기본적으로 하나의 외부 소스, 환경 변수에 대한 지원이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ea69-129">By default it comes with support for one external source - environmental variables</span></span>
  * <span data-ttu-id="1ea69-130">`ConnectionStringSource` 클래스를 확장하여 새 소스를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ea69-130">You can add new sources by extending the `ConnectionStringSource` class</span></span>

<span data-ttu-id="1ea69-131">여기에 설명된 예제의 경우 연결 문자열이 직접 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ea69-131">For the examples outlined here, the connection string is passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$connectionString = "Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]";

$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);
```

## <a name="create-a-queue"></a><span data-ttu-id="1ea69-132">큐 만들기</span><span class="sxs-lookup"><span data-stu-id="1ea69-132">Create a queue</span></span>
<span data-ttu-id="1ea69-133">`ServiceBusRestProxy` 클래스를 사용하여 Service Bus 큐에 대한 관리 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ea69-133">You can perform management operations for Service Bus queues via the `ServiceBusRestProxy` class.</span></span> <span data-ttu-id="1ea69-134">`ServiceBusRestProxy` 개체는 관리에 필요한 토큰 사용 권한을 캡슐화하는 적절한 연결 문자열을 사용한 `ServicesBuilder::createServiceBusService` 팩터리 메서드를 통해 구성됩니다. </span><span class="sxs-lookup"><span data-stu-id="1ea69-134">A `ServiceBusRestProxy` object is constructed via the `ServicesBuilder::createServiceBusService` factory method with an appropriate connection string that encapsulates the token permissions to manage it.</span></span>

<span data-ttu-id="1ea69-135">다음 예제에서는 `ServiceBusRestProxy`를 인스턴스화하고 `ServiceBusRestProxy->createQueue`을 호출하여 `MySBNamespace` 네임스페이스 내에 이름이 `myqueue`인 큐를 만드는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="1ea69-135">The following example shows how to instantiate a `ServiceBusRestProxy` and call `ServiceBusRestProxy->createQueue` to create a queue named `myqueue` within a `MySBNamespace` service namespace:</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\QueueInfo;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    $queueInfo = new QueueInfo("myqueue");

    // Create queue.
    $serviceBusRestProxy->createQueue($queueInfo);
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
> <span data-ttu-id="1ea69-136">`ServiceBusRestProxy` 개체의 `listQueues` 메서드를 사용하여 네임스페이스 내에 지정된 이름의 큐가 이미 있는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ea69-136">You can use the `listQueues` method on `ServiceBusRestProxy` objects to check if a queue with a specified name already exists within a namespace.</span></span>
> 
> 

## <a name="send-messages-to-a-queue"></a><span data-ttu-id="1ea69-137">큐에 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="1ea69-137">Send messages to a queue</span></span>
<span data-ttu-id="1ea69-138">Service Bus 큐에 메시지를 보내기 위해 응용 프로그램은 `ServiceBusRestProxy->sendQueueMessage` 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="1ea69-138">To send a message to a Service Bus queue, your application calls the `ServiceBusRestProxy->sendQueueMessage` method.</span></span> <span data-ttu-id="1ea69-139">다음 코드는 위에서 `MySBNamespace` 서비스 네임스페이스 내에서 이전에 만든 `myqueue` 큐에 메시지를 보내는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1ea69-139">The following code shows how to send a message to the `myqueue` queue previously created within the `MySBNamespace` service namespace.</span></span>

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
    $serviceBusRestProxy->sendQueueMessage("myqueue", $message);
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

<span data-ttu-id="1ea69-140">Service Bus 큐로 보내고 받은 메시지는 [BrokeredMessage][BrokeredMessage] 클래스의 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="1ea69-140">Messages sent to (and received from ) Service Bus queues are instances of the [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="1ea69-141">[BrokeredMessage][BrokeredMessage] 개체에는 표준 메서드 집합과, 응용 프로그램별 사용자 지정 속성을 저장하는 데 사용되는 사전 및 임의 응용 프로그램 데이터 본문이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ea69-141">[BrokeredMessage][BrokeredMessage] objects have a set of standard methods and properties that are used to hold custom application-specific properties, and a body of arbitrary application data.</span></span>

<span data-ttu-id="1ea69-142">Service Bus 큐는 [표준 계층](service-bus-premium-messaging.md)에서 256KB의 최대 메시지 크기를 [프리미엄 계층](service-bus-premium-messaging.md)에서 1MB를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="1ea69-142">Service Bus queues support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="1ea69-143">표준 및 사용자 지정 응용 프로그램 속성이 포함된 헤더의 최대 크기는 64KB입니다.</span><span class="sxs-lookup"><span data-stu-id="1ea69-143">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="1ea69-144">한 큐에 저장되는 메시지 수에는 제한이 없지만 한 큐에 저장되는 총 메시지 크기는 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ea69-144">There is no limit on the number of messages held in a queue but there is a cap on the total size of the messages held by a queue.</span></span> <span data-ttu-id="1ea69-145">큐 크기의 상한은 5GB입니다.</span><span class="sxs-lookup"><span data-stu-id="1ea69-145">This upper limit on queue size is 5 GB.</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="1ea69-146">큐에서 메시지 받기</span><span class="sxs-lookup"><span data-stu-id="1ea69-146">Receive messages from a queue</span></span>

<span data-ttu-id="1ea69-147">큐에서 메시지를 받는 가장 쉬운 방법은 `ServiceBusRestProxy->receiveQueueMessage` 메서드를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1ea69-147">The best way to receive messages from a queue is to use a `ServiceBusRestProxy->receiveQueueMessage` method.</span></span> <span data-ttu-id="1ea69-148">메시지는 [*ReceiveAndDelete*](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) 및 [*PeekLock*](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock)의 두 가지 모드로 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ea69-148">Messages can be received in two different modes: [*ReceiveAndDelete*](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) and [*PeekLock*](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock).</span></span> <span data-ttu-id="1ea69-149">**PeekLock**이 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="1ea69-149">**PeekLock** is the default.</span></span>

<span data-ttu-id="1ea69-150">[ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) 모드를 사용하는 경우 수신은 1단계 작업입니다. 즉, Service Bus가 큐의 메시지에 대한 읽기 요청을 받으면 메시지를 이용되는 것으로 표시하고 응용 프로그램에 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="1ea69-150">When using [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) mode, receive is a single-shot operation; that is, when Service Bus receives a read request for a message in a queue, it marks the message as being consumed and returns it to the application.</span></span> <span data-ttu-id="1ea69-151">[ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) 모드는 가장 단순한 모델이며, 응용 프로그램이 실패 이벤트 시 메시지를 처리하지 않아도 안전한 시나리오에서 효과적입니다.</span><span class="sxs-lookup"><span data-stu-id="1ea69-151">[ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) mode is the simplest model and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="1ea69-152">이해를 돕기 위해 소비자가 수신 요청을 실행한 후 처리하기 전에 크래시되는 시나리오를 고려해 보세요.</span><span class="sxs-lookup"><span data-stu-id="1ea69-152">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="1ea69-153">서비스 버스는 메시지를 이용되는 것으로 표시하기 때문에 응용 프로그램이 다시 시작되고 메시지 소비를 다시 시작할 경우 크래시 전에 소비된 메시지가 누락됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ea69-153">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="1ea69-154">기본값인 [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) 모드에서는 메시지 수신이 2단계 작업이므로 메시지 누락이 허용되지 않는 응용 프로그램을 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ea69-154">In the default [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) mode, receiving a message becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="1ea69-155">서비스 버스는 요청을 받으면 소비할 다음 메시지를 찾아서 다른 소비자가 수신할 수 없도록 잠근 후 응용 프로그램에 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="1ea69-155">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers from receiving it, and then returns it to the application.</span></span> <span data-ttu-id="1ea69-156">응용 프로그램은 메시지 처리를 완료하거나 추가 처리를 위해 안전하게 저장한 후에 받은 메시지를 `ServiceBusRestProxy->deleteMessage`에 전달하여 수신 프로세스의 두 번째 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="1ea69-156">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by passing the received message to `ServiceBusRestProxy->deleteMessage`.</span></span> <span data-ttu-id="1ea69-157">Service Bus는 `deleteMessage` 호출을 확인한 후 메시지를 이용되는 것으로 표시하고 큐에서 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="1ea69-157">When Service Bus sees the `deleteMessage` call, it will mark the message as being consumed and remove it from the queue.</span></span>

<span data-ttu-id="1ea69-158">다음 예제에서는 [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) 모드(기본 모드)를 사용하여 메시지를 받고 처리하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1ea69-158">The following example shows how to receive and process a message using [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) mode (the default mode).</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\ReceiveMessageOptions;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Set the receive mode to PeekLock (default is ReceiveAndDelete).
    $options = new ReceiveMessageOptions();
    $options->setPeekLock();

    // Receive message.
    $message = $serviceBusRestProxy->receiveQueueMessage("myqueue", $options);
    echo "Body: ".$message->getBody()."<br />";
    echo "MessageID: ".$message->getMessageId()."<br />";

    /*---------------------------
        Process message here.
    ----------------------------*/

    // Delete message. Not necessary if peek lock is not set.
    echo "Message deleted.<br />";
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

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="1ea69-159">응용 프로그램 작동 중단 및 읽을 수 없는 메시지를 처리하는 방법</span><span class="sxs-lookup"><span data-stu-id="1ea69-159">How to handle application crashes and unreadable messages</span></span>

<span data-ttu-id="1ea69-160">서비스 버스는 응용 프로그램 오류나 메시지 처리 문제를 정상적으로 복구하는 데 유용한 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1ea69-160">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="1ea69-161">어떤 이유로든 수신자 응용 프로그램이 메시지를 처리할 수 없는 경우 받은 메시지에 대해 `deleteMessage` 메서드 대신 `unlockMessage` 메서드를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ea69-161">If a receiver application is unable to process the message for some reason, then it can call the `unlockMessage` method on the received message (instead of the `deleteMessage` method).</span></span> <span data-ttu-id="1ea69-162">그러면 서비스 버스에서 큐 메시지의 잠금을 해제하므로 동일한 소비 응용 프로그램이나 다른 소비 응용 프로그램에서 메시지를 다시 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ea69-162">This will cause Service Bus to unlock the message within the queue and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="1ea69-163">큐 내에서 잠긴 메시지와 연결된 제한 시간도 있으며, 응용 프로그램에서 잠금 제한 시간이 만료되기 전에 메시지를 처리하지 못하는 경우(예: 응용 프로그램이 크래시되는 경우) 서비스 버스가 메시지를 자동으로 잠금 해제하여 다시 받을 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ea69-163">There is also a timeout associated with a message locked within the queue, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus will unlock the message automatically and make it available to be received again.</span></span>

<span data-ttu-id="1ea69-164">응용 프로그램이 메시지를 처리한 후 `deleteMessage` 요청이 실행되기 전에 크래시되는 경우 다시 시작될 때 메시지가 응용 프로그램에 다시 배달됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ea69-164">In the event that the application crashes after processing the message but before the `deleteMessage` request is issued, then the message will be redelivered to the application when it restarts.</span></span> <span data-ttu-id="1ea69-165">이를 *최소 한 번 이상 처리*라고 합니다. 즉, 각 메시지가 최소 한 번 이상 처리되지만 특정 상황에서는 동일한 메시지가 다시 배달될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ea69-165">This is often called *At Least Once* processing; that is, each message is processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="1ea69-166">중복 처리가 허용되지 않는 시나리오에서는 중복 메시지 배달을 처리하는 논리를 응용 프로그램에 추가하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1ea69-166">If the scenario cannot tolerate duplicate processing, then adding additional logic to applications to handle duplicate message delivery is recommended.</span></span> <span data-ttu-id="1ea69-167">이 경우 대체로 배달 시도 간에 일정하게 유지되는 메시지의 `getMessageId` 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1ea69-167">This is often achieved using the `getMessageId` method of the message, which remains constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1ea69-168">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1ea69-168">Next steps</span></span>
<span data-ttu-id="1ea69-169">지금까지 Service Bus 큐의 기본 사항에 대해 알아보았습니다. 자세한 내용은 [큐, 토픽 및 구독][Queues, topics, and subscriptions]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ea69-169">Now that you've learned the basics of Service Bus queues, see [Queues, topics, and subscriptions][Queues, topics, and subscriptions] for more information.</span></span>

<span data-ttu-id="1ea69-170">자세한 내용은 [PHP 개발자 센터](https://azure.microsoft.com/develop/php/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ea69-170">For more information, also visit the [PHP Developer Center](https://azure.microsoft.com/develop/php/).</span></span>

[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[require_once]: http://php.net/require_once



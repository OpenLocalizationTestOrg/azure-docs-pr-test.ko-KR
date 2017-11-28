---
title: "php aaaHow toouse 서비스 버스 큐 | Microsoft Docs"
description: "Azure에서 서비스 버스 toouse 큐 대기 하는 방법에 대해 알아봅니다. 코드 샘플은 PHP로 작성되었습니다."
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
ms.openlocfilehash: 8cf233176029b679d172eaf713632087beca5e4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-php"></a><span data-ttu-id="70a7a-104">Php toouse 서비스 버스 큐 대기 하는 방법</span><span class="sxs-lookup"><span data-stu-id="70a7a-104">How toouse Service Bus queues with PHP</span></span>
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="70a7a-105">이 가이드에서는 toouse 서비스 버스 큐입니다.</span><span class="sxs-lookup"><span data-stu-id="70a7a-105">This guide shows you how toouse Service Bus queues.</span></span> <span data-ttu-id="70a7a-106">hello PHP로 작성 된 100 개의 샘플과 hello를 사용 하 여 [PHP 용 Azure SDK](../php-download-sdk.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="70a7a-106">hello samples are written in PHP and use hello [Azure SDK for PHP](../php-download-sdk.md).</span></span> <span data-ttu-id="70a7a-107">hello 가이드에서 다루는 시나리오 포함 **큐를 만드는**, **메시지 보내기 및 받기**, 및 **큐 삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="70a7a-107">hello scenarios covered include **creating queues**, **sending and receiving messages**, and **deleting queues**.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="70a7a-108">PHP 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="70a7a-108">Create a PHP application</span></span>
<span data-ttu-id="70a7a-109">hello Azure Blob 서비스에 액세스 하는 PHP 응용 프로그램을 만들기 위한 요구 사항은 hello만 hello hello에 클래스 참조 [PHP 용 Azure SDK](../php-download-sdk.md) 에서 코드 내에서.</span><span class="sxs-lookup"><span data-stu-id="70a7a-109">hello only requirement for creating a PHP application that accesses hello Azure Blob service is hello referencing of classes in hello [Azure SDK for PHP](../php-download-sdk.md) from within your code.</span></span> <span data-ttu-id="70a7a-110">응용 프로그램 또는 메모장 모든 개발 도구 toocreate를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70a7a-110">You can use any development tools toocreate your application, or Notepad.</span></span>

> [!NOTE]
> <span data-ttu-id="70a7a-111">PHP 설치 hello 있어야 [OpenSSL 확장](http://php.net/openssl) 설치 되어 있고 활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="70a7a-111">Your PHP installation must also have hello [OpenSSL extension](http://php.net/openssl) installed and enabled.</span></span>
> 
> 

<span data-ttu-id="70a7a-112">이 가이드에서는 PHP 응용 프로그램 내에서 로컬로 또는 Azure 웹 역할, 작업자 역할 또는 웹 사이트 내에서 실행되는 코드에서 호출할 수 있는 서비스 기능을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="70a7a-112">In this guide, you will use service features which can be called from within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-hello-azure-client-libraries"></a><span data-ttu-id="70a7a-113">Hello Azure 클라이언트 라이브러리 가져오기</span><span class="sxs-lookup"><span data-stu-id="70a7a-113">Get hello Azure client libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="70a7a-114">사용자 응용 프로그램 toouse 서비스 버스를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="70a7a-114">Configure your application toouse Service Bus</span></span>
<span data-ttu-id="70a7a-115">toouse hello 서비스 버스 큐 Api를 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="70a7a-115">toouse hello Service Bus queue APIs, do hello following:</span></span>

1. <span data-ttu-id="70a7a-116">Hello를 사용 하 여 참조 hello 자동 로더에 파일 [require_once] [ require_once] 문.</span><span class="sxs-lookup"><span data-stu-id="70a7a-116">Reference hello autoloader file using hello [require_once][require_once] statement.</span></span>
2. <span data-ttu-id="70a7a-117">사용할 수 있는 모든 클래스 참조</span><span class="sxs-lookup"><span data-stu-id="70a7a-117">Reference any classes you might use.</span></span>

<span data-ttu-id="70a7a-118">hello 다음 예제에서는 어떻게 tooinclude hello 자동 로더 파일과 참조 hello `ServicesBuilder` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="70a7a-118">hello following example shows how tooinclude hello autoloader file and reference hello `ServicesBuilder` class.</span></span>

> [!NOTE]
> <span data-ttu-id="70a7a-119">이 예제 (및이 문서의 다른 예제) 작성기를 통해 Azure에 대 한 hello PHP 클라이언트 라이브러리를 설치 했다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="70a7a-119">This example (and other examples in this article) assumes you have installed hello PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="70a7a-120">수동으로 또는 배 패키지로 hello 라이브러리를 설치 하는 경우에 hello 참조 해야 **WindowsAzure.php** 자동 로더에 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="70a7a-120">If you installed hello libraries manually or as a PEAR package, you must reference hello **WindowsAzure.php** autoloader file.</span></span>
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="70a7a-121">아래의 hello 예제 hello `require_once` hello 예제 tooexecute에 필요한 hello 클래스가 참조 하지만 문에 항상 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="70a7a-121">In hello examples below, hello `require_once` statement will always be shown, but only hello classes necessary for hello example tooexecute are referenced.</span></span>

## <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="70a7a-122">서비스 버스 연결 설정</span><span class="sxs-lookup"><span data-stu-id="70a7a-122">Set up a Service Bus connection</span></span>
<span data-ttu-id="70a7a-123">서비스 버스 클라이언트 tooinstantiate 있어야 유효한 연결 문자열 형식:</span><span class="sxs-lookup"><span data-stu-id="70a7a-123">tooinstantiate a Service Bus client, you must first have a valid connection string in this format:</span></span>

```
Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]
```

<span data-ttu-id="70a7a-124">여기서 `Endpoint` hello 형식의 일반적으로 `[yourNamespace].servicebus.windows.net`합니다.</span><span class="sxs-lookup"><span data-stu-id="70a7a-124">Where `Endpoint` is typically of hello format `[yourNamespace].servicebus.windows.net`.</span></span>

<span data-ttu-id="70a7a-125">toocreate hello를 사용 해야 하는 모든 Azure 서비스 클라이언트 `ServicesBuilder` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="70a7a-125">toocreate any Azure service client you must use hello `ServicesBuilder` class.</span></span> <span data-ttu-id="70a7a-126">다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70a7a-126">You can:</span></span>

* <span data-ttu-id="70a7a-127">Hello 연결을 통과할 tooit 직접 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="70a7a-127">Pass hello connection string directly tooit.</span></span>
* <span data-ttu-id="70a7a-128">사용 하 여 hello **CloudConfigurationManager (CCM)** toocheck hello 연결 문자열에 대 한 여러 외부 원본:</span><span class="sxs-lookup"><span data-stu-id="70a7a-128">Use hello **CloudConfigurationManager (CCM)** toocheck multiple external sources for hello connection string:</span></span>
  * <span data-ttu-id="70a7a-129">기본적으로 하나의 외부 소스, 환경 변수에 대한 지원이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="70a7a-129">By default it comes with support for one external source - environmental variables</span></span>
  * <span data-ttu-id="70a7a-130">Hello를 확장 하 여 새 원본을 추가할 수 있습니다 `ConnectionStringSource` 클래스</span><span class="sxs-lookup"><span data-stu-id="70a7a-130">You can add new sources by extending hello `ConnectionStringSource` class</span></span>

<span data-ttu-id="70a7a-131">Hello 여기에 설명 된 예제를 보려면 hello 연결 문자열은 직접 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="70a7a-131">For hello examples outlined here, hello connection string is passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$connectionString = "Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]";

$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);
```

## <a name="create-a-queue"></a><span data-ttu-id="70a7a-132">큐 만들기</span><span class="sxs-lookup"><span data-stu-id="70a7a-132">Create a queue</span></span>
<span data-ttu-id="70a7a-133">Hello 통해 서비스 버스 큐에 대 한 관리 작업을 수행할 수 `ServiceBusRestProxy` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="70a7a-133">You can perform management operations for Service Bus queues via hello `ServiceBusRestProxy` class.</span></span> <span data-ttu-id="70a7a-134">A `ServiceBusRestProxy` hello를 통해 개체가 생성 된 `ServicesBuilder::createServiceBusService` hello 토큰 권한 toomanage 캡슐화 하는 적절 한 연결 문자열의 팩터리 메서드 것입니다.</span><span class="sxs-lookup"><span data-stu-id="70a7a-134">A `ServiceBusRestProxy` object is constructed via hello `ServicesBuilder::createServiceBusService` factory method with an appropriate connection string that encapsulates hello token permissions toomanage it.</span></span>

<span data-ttu-id="70a7a-135">hello 방법을 예제와 다음 tooinstantiate는 `ServiceBusRestProxy` 호출 `ServiceBusRestProxy->createQueue` toocreate 라는 큐 `myqueue` 내에서 한 `MySBNamespace` 서비스 네임 스페이스:</span><span class="sxs-lookup"><span data-stu-id="70a7a-135">hello following example shows how tooinstantiate a `ServiceBusRestProxy` and call `ServiceBusRestProxy->createQueue` toocreate a queue named `myqueue` within a `MySBNamespace` service namespace:</span></span>

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
> <span data-ttu-id="70a7a-136">Hello를 사용할 수 있습니다 `listQueues` 메서드를 `ServiceBusRestProxy` 네임 스페이스 내에서 지정 된 이름의 큐가 이미 있으면 toocheck 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="70a7a-136">You can use hello `listQueues` method on `ServiceBusRestProxy` objects toocheck if a queue with a specified name already exists within a namespace.</span></span>
> 
> 

## <a name="send-messages-tooa-queue"></a><span data-ttu-id="70a7a-137">송신 메시지 tooa 큐</span><span class="sxs-lookup"><span data-stu-id="70a7a-137">Send messages tooa queue</span></span>
<span data-ttu-id="70a7a-138">메시지 tooa 서비스 버스 큐 toosend 응용 프로그램 호출 hello `ServiceBusRestProxy->sendQueueMessage` 메서드.</span><span class="sxs-lookup"><span data-stu-id="70a7a-138">toosend a message tooa Service Bus queue, your application calls hello `ServiceBusRestProxy->sendQueueMessage` method.</span></span> <span data-ttu-id="70a7a-139">코드에서 보여 주는 방법을 다음 hello 메시지 toohello toosend `myqueue` 내에서 이전에 만든 큐는 `MySBNamespace` 서비스 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="70a7a-139">hello following code shows how toosend a message toohello `myqueue` queue previously created within the `MySBNamespace` service namespace.</span></span>

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

<span data-ttu-id="70a7a-140">너무 (보내고 받은에서) 서비스 버스 큐는 hello의 인스턴스 메시지 [BrokeredMessage] [ BrokeredMessage] 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="70a7a-140">Messages sent too(and received from ) Service Bus queues are instances of hello [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="70a7a-141">[BrokeredMessage] [ BrokeredMessage] 개체 toohold 사용 되는 사용자 지정 하는 응용 프로그램 관련 속성 및 임의 응용 프로그램 데이터의 본문이 되는 표준 메서드 및 속성 집합이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70a7a-141">[BrokeredMessage][BrokeredMessage] objects have a set of standard methods and properties that are used toohold custom application-specific properties, and a body of arbitrary application data.</span></span>

<span data-ttu-id="70a7a-142">서비스 버스 큐 최대 메시지 크기는 256KB hello 지원 [표준 계층](service-bus-premium-messaging.md) 및 hello에서 1 MB [Premium 계층](service-bus-premium-messaging.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="70a7a-142">Service Bus queues support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="70a7a-143">hello 표준 및 사용자 지정 응용 프로그램 속성을 포함 하는 hello 헤더는 64KB의 최대 크기를 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70a7a-143">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="70a7a-144">큐에 유지 하는 메시지의 hello 수를 제한 하지 않으며 cap hello 총 크기는 큐에서 대기 하는 hello 메시지에입니다.</span><span class="sxs-lookup"><span data-stu-id="70a7a-144">There is no limit on hello number of messages held in a queue but there is a cap on hello total size of hello messages held by a queue.</span></span> <span data-ttu-id="70a7a-145">큐 크기의 상한은 5GB입니다.</span><span class="sxs-lookup"><span data-stu-id="70a7a-145">This upper limit on queue size is 5 GB.</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="70a7a-146">큐에서 메시지 받기</span><span class="sxs-lookup"><span data-stu-id="70a7a-146">Receive messages from a queue</span></span>

<span data-ttu-id="70a7a-147">hello 가장 좋은 방법은 tooreceive 메시지 큐에서은 toouse는 `ServiceBusRestProxy->receiveQueueMessage` 메서드.</span><span class="sxs-lookup"><span data-stu-id="70a7a-147">hello best way tooreceive messages from a queue is toouse a `ServiceBusRestProxy->receiveQueueMessage` method.</span></span> <span data-ttu-id="70a7a-148">메시지는 [*ReceiveAndDelete*](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) 및 [*PeekLock*](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock)의 두 가지 모드로 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70a7a-148">Messages can be received in two different modes: [*ReceiveAndDelete*](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) and [*PeekLock*](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock).</span></span> <span data-ttu-id="70a7a-149">**PeekLock** hello 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="70a7a-149">**PeekLock** is hello default.</span></span>

<span data-ttu-id="70a7a-150">사용 하는 경우 [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) 모드에서는 수신은 1 단계 작업입니다; 즉, 서비스 버스 큐의 메시지에 대 한 읽기 요청을 받으면 hello 메시지 사용 되는 것을 표시 하 고 toohello 응용 프로그램을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="70a7a-150">When using [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) mode, receive is a single-shot operation; that is, when Service Bus receives a read request for a message in a queue, it marks hello message as being consumed and returns it toohello application.</span></span> <span data-ttu-id="70a7a-151">[ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) 모드는 hello 가장 간단한 모델 이며는 응용 프로그램은 오류의 hello 이벤트에서 메시지를 처리 하지 허용할 수 없는 시나리오에 가장 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="70a7a-151">[ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) mode is hello simplest model and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="70a7a-152">toounderstand hello는 hello 소비자 문제에 요청을 수신 하는 시나리오 및 후 처리 하기 전에 크래시 합니다.</span><span class="sxs-lookup"><span data-stu-id="70a7a-152">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="70a7a-153">서비스 버스 사용 되는 것을 다음 hello 응용 프로그램 다시 시작 되 고 메시지 사용을 시작할 때 hello 메시지를 표시 한 됩니다, 때문에 누락 됩니다 hello 메시지 했던 이전 toohello 크래시를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="70a7a-153">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="70a7a-154">Hello 기본에서 [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) 모드에서는 메시지를 표시 하므로 누락 된 메시지를 허용할 수 없는 가능한 toosupport 응용 프로그램 2 단계 작업을 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="70a7a-154">In hello default [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) mode, receiving a message becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="70a7a-155">서비스 버스 요청을 받으면 hello 사용 되는 다음 메시지 toobe 찾습니다, tooprevent 잠급니다 다른 소비자가 수신할 toohello 응용 프로그램 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="70a7a-155">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers from receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="70a7a-156">Hello hello의 두 번째 단계를 완료 hello 응용 프로그램 hello 메시지 처리를 완료 (또는 이후 처리를 위해 안정적으로 저장) 한 후 너무 hello 받은 메시지를 전달 하 여 수신 프로세스`ServiceBusRestProxy->deleteMessage`합니다.</span><span class="sxs-lookup"><span data-stu-id="70a7a-156">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by passing hello received message too`ServiceBusRestProxy->deleteMessage`.</span></span> <span data-ttu-id="70a7a-157">서비스 버스 hello를 표시 하는 경우 `deleteMessage` 호출 hello 메시지를 사용 되 고 표시 하 고 hello 큐에서 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="70a7a-157">When Service Bus sees hello `deleteMessage` call, it will mark hello message as being consumed and remove it from hello queue.</span></span>

<span data-ttu-id="70a7a-158">hello 방법을 예제와 다음 tooreceive 하 고 사용 하 여 메시지 처리 [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) 모드 (hello 기본 모드).</span><span class="sxs-lookup"><span data-stu-id="70a7a-158">hello following example shows how tooreceive and process a message using [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) mode (hello default mode).</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\ReceiveMessageOptions;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Set hello receive mode tooPeekLock (default is ReceiveAndDelete).
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

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="70a7a-159">Toohandle 응용 프로그램이 크래시 되는 방법 및 읽을 수 없는 메시지</span><span class="sxs-lookup"><span data-stu-id="70a7a-159">How toohandle application crashes and unreadable messages</span></span>

<span data-ttu-id="70a7a-160">서비스 버스 기능 toohelp 정상적으로 응용 프로그램 또는 메시지를 처리 하는 데 문제가 오류 로부터 복구를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="70a7a-160">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="70a7a-161">수신기 응용 프로그램 수 없는 경우 몇 가지 이유로 tooprocess 환영 메시지가 다음 hello를 호출할 수 있습니다 `unlockMessage` 메서드를 수신 하는 hello 메시지 (hello 대신 `deleteMessage` 메서드).</span><span class="sxs-lookup"><span data-stu-id="70a7a-161">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlockMessage` method on hello received message (instead of hello `deleteMessage` method).</span></span> <span data-ttu-id="70a7a-162">Hello 큐 내에서 서비스 버스 toounlock hello 메시지 시키며 수신 다시 사용할 수 있는 toobe 확인, 사용자가 여를 많이 사용 응용 프로그램 또는 다른 소비 응용 프로그램에서 동일한 hello 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="70a7a-162">This will cause Service Bus toounlock hello message within hello queue and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="70a7a-163">또한 hello 큐 내에서 잠긴 메시지와 관련 된 제한 시간 집합과 hello 응용 프로그램 실패 하기 전에 hello 메시지 tooprocess hello 잠금 제한 시간이 만료 (예를 들어 hello 응용 프로그램이 충돌할 경우), 서비스 버스에서 hello 메시지를 잠금 해제 한 다음 자동으로 사용할 수 있는 toobe 수신 다시 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="70a7a-163">There is also a timeout associated with a message locked within hello queue, and if hello application fails tooprocess hello message before hello lock timeout expires (for example, if hello application crashes), then Service Bus will unlock hello message automatically and make it available toobe received again.</span></span>

<span data-ttu-id="70a7a-164">Hello hello 응용 프로그램 이벤트 충돌 hello 메시지 처리 전후에 그러나 hello 전에 `deleteMessage` 요청이 발생 한 후 다시 시작할 때 hello 메시지 다시 전달한 toohello 응용 프로그램 됩니다.</span><span class="sxs-lookup"><span data-stu-id="70a7a-164">In hello event that hello application crashes after processing hello message but before hello `deleteMessage` request is issued, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="70a7a-165">이 이라고 하는데 *최소 한 번* 처리; 즉, 각 메시지는 한 번 이상 처리 되지만 특정 상황 hello에 동일한 메시지를 다시 배달 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70a7a-165">This is often called *At Least Once* processing; that is, each message is processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="70a7a-166">중복 처리가 다음 추가 추가 hello 시나리오 허용할 수 없는 경우 논리 tooapplications toohandle 중복 메시지 배달이 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="70a7a-166">If hello scenario cannot tolerate duplicate processing, then adding additional logic tooapplications toohandle duplicate message delivery is recommended.</span></span> <span data-ttu-id="70a7a-167">이 대개 달성 hello를 사용 하 여 `getMessageId` 메서드 hello 메시지를 배달 시도에서 일관적으로 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="70a7a-167">This is often achieved using hello `getMessageId` method of hello message, which remains constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="70a7a-168">다음 단계</span><span class="sxs-lookup"><span data-stu-id="70a7a-168">Next steps</span></span>
<span data-ttu-id="70a7a-169">서비스 버스 큐의 hello 기본 사항 학습 한, 했으므로 참조 [큐, 토픽 및 구독] [ Queues, topics, and subscriptions] 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="70a7a-169">Now that you've learned hello basics of Service Bus queues, see [Queues, topics, and subscriptions][Queues, topics, and subscriptions] for more information.</span></span>

<span data-ttu-id="70a7a-170">자세한 내용은 hello 또한 방문 [PHP 개발자 센터](https://azure.microsoft.com/develop/php/)합니다.</span><span class="sxs-lookup"><span data-stu-id="70a7a-170">For more information, also visit hello [PHP Developer Center](https://azure.microsoft.com/develop/php/).</span></span>

[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[require_once]: http://php.net/require_once



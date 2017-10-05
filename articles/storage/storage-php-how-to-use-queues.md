---
title: "Python에서 큐 저장소를 사용하는 방법 | Microsoft Docs"
description: "Azure 큐 저장소를 사용하여 큐를 작성 및 삭제하고 메시지를 삽입하고 가져오고 삭제하는 방법을 알아봅니다. 샘플은 PHP로 작성되었습니다."
documentationcenter: php
services: storage
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 7582b208-4851-4489-a74a-bb952569f55b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 3c8f799a917cfc9d74412d90f27f2ea8c21265d4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-queue-storage-from-php"></a><span data-ttu-id="1acb4-104">PHP에서 큐 저장소를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="1acb4-104">How to use Queue storage from PHP</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="1acb4-105">개요</span><span class="sxs-lookup"><span data-stu-id="1acb4-105">Overview</span></span>
<span data-ttu-id="1acb4-106">이 가이드에서는 Azure 큐 저장소 서비스를 사용하여 일반 시나리오를 수행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1acb4-106">This guide will show you how to perform common scenarios by using the Azure Queue storage service.</span></span> <span data-ttu-id="1acb4-107">샘플은 PHP용 Windows SDK의 클래스를 통해 작성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1acb4-107">The samples are written via classes from the Windows SDK for PHP.</span></span> <span data-ttu-id="1acb4-108">여기서 다루는 시나리오에는 큐 메시지 삽입, 보기, 가져오기 및 삭제와 큐 만들기 및 삭제가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="1acb4-108">The covered scenarios include inserting, peeking, getting, and deleting queue messages, as well as creating and deleting queues.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="1acb4-109">PHP 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="1acb4-109">Create a PHP application</span></span>
<span data-ttu-id="1acb4-110">Azure 큐 저장소에 액세스하는 PHP 응용 프로그램을 만들 때 충족해야 하는 유일한 요구 사항은 코드 내에서 PHP용 Azure SDK의 클래스를 참조하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1acb4-110">The only requirement for creating a PHP application that accesses Azure Queue storage is the referencing of classes from the Azure SDK for PHP from within your code.</span></span> <span data-ttu-id="1acb4-111">응용 프로그램을 만드는 데는 메모장을 포함한 어떠한 개발 도구도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1acb4-111">You can use any development tools to create your application, including Notepad.</span></span>

<span data-ttu-id="1acb4-112">이 가이드에서는 PHP 응용 프로그램 내에서 로컬로 또는 Azure 웹 역할, 작업자 역할 또는 웹 사이트 내에서 실행되는 코드에서 호출할 수 있는 큐 저장소 기능을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1acb4-112">In this guide, you will use Queue storage features that can be called within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-the-azure-client-libraries"></a><span data-ttu-id="1acb4-113">Azure 클라이언트 라이브러리 가져오기</span><span class="sxs-lookup"><span data-stu-id="1acb4-113">Get the Azure Client Libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-to-access-queue-storage"></a><span data-ttu-id="1acb4-114">큐 저장소에 액세스하도록 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="1acb4-114">Configure your application to access Queue storage</span></span>
<span data-ttu-id="1acb4-115">Azure 큐 저장소에 대한 API를 사용하려면 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1acb4-115">To use the APIs for Azure Queue storage, you need to:</span></span>

1. <span data-ttu-id="1acb4-116">[require_once] 문을 사용하여 자동 로더 파일을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="1acb4-116">Reference the autoloader file by using the [require_once] statement.</span></span>
2. <span data-ttu-id="1acb4-117">사용할 수 있는 모든 클래스를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="1acb4-117">Reference any classes that you might use.</span></span>

<span data-ttu-id="1acb4-118">다음 예제에서는 자동 로더 파일을 포함하고 **ServicesBuilder** 클래스를 참조하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1acb4-118">The following example shows how to include the autoloader file and reference the **ServicesBuilder** class.</span></span>

> [!NOTE]
> <span data-ttu-id="1acb4-119">이 예제 및 이 문서의 다른 예제에서는 작성기를 통해 Azure용 PHP 클라이언트 라이브러리를 설치했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="1acb4-119">This example (and other examples in this article) assumes that you have installed the PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="1acb4-120">라이브러리를 수동으로 설치한 경우 `WindowsAzure.php` 자동 로더 파일을 참조해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1acb4-120">If you installed the libraries manually, you will need to reference the `WindowsAzure.php` autoloader file.</span></span>
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;

```

<span data-ttu-id="1acb4-121">아래 예제에서 `require_once` 문은 항상 표시되지만 예제를 실행하는 데 필요한 클래스만 참조됩니다.</span><span class="sxs-lookup"><span data-stu-id="1acb4-121">In the examples below, the `require_once` statement will be shown always, but only the classes that are necessary for the example to execute will be referenced.</span></span>

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="1acb4-122">Azure 저장소 연결 설정</span><span class="sxs-lookup"><span data-stu-id="1acb4-122">Set up an Azure storage connection</span></span>
<span data-ttu-id="1acb4-123">Azure 큐 저장소 클라이언트를 인스턴스화하려면 먼저 유효한 연결 문자열이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1acb4-123">To instantiate an Azure Queue storage client, you must first have a valid connection string.</span></span> <span data-ttu-id="1acb4-124">큐 저장소 연결 문자열 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1acb4-124">The format for the queue service connection string is as follows.</span></span>

<span data-ttu-id="1acb4-125">Live 서비스에 액세스하는 경우:</span><span class="sxs-lookup"><span data-stu-id="1acb4-125">For accessing a live service:</span></span>

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

<span data-ttu-id="1acb4-126">에뮬레이터 저장소에 액세스하는 경우:</span><span class="sxs-lookup"><span data-stu-id="1acb4-126">For accessing the emulator storage:</span></span>

```php
UseDevelopmentStorage=true
```

<span data-ttu-id="1acb4-127">Azure 서비스 클라이언트를 만들려면 **ServicesBuilder** 클래스를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1acb4-127">To create any Azure service client, you need to use the **ServicesBuilder** class.</span></span> <span data-ttu-id="1acb4-128">다음 기술 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1acb4-128">You can use either of the following techniques:</span></span>

* <span data-ttu-id="1acb4-129">연결 문자열을 직접 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="1acb4-129">Pass the connection string directly to it.</span></span>
* <span data-ttu-id="1acb4-130">**CCM(CloudConfigurationManager)** 을 사용하여 여러 외부 소스에서 연결 문자열을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1acb4-130">Use **CloudConfigurationManager (CCM)** to check multiple external sources for the connection string:</span></span>
  * <span data-ttu-id="1acb4-131">기본적으로 하나의 외부 소스, 환경 변수에 대한 지원이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="1acb4-131">By default, it comes with support for one external source—environmental variables.</span></span>
  * <span data-ttu-id="1acb4-132">**ConnectionStringSource** 클래스를 확장하여 새 소스를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1acb4-132">You can add new sources by extending the **ConnectionStringSource** class.</span></span>

<span data-ttu-id="1acb4-133">여기에 설명된 예제의 경우 연결 문자열이 직접 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="1acb4-133">For the examples outlined here, the connection string will be passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);
```

## <a name="create-a-queue"></a><span data-ttu-id="1acb4-134">큐 만들기</span><span class="sxs-lookup"><span data-stu-id="1acb4-134">Create a queue</span></span>
<span data-ttu-id="1acb4-135">**QueueRestProxy** 개체를 통해 **createQueue** 메서드를 사용하여 큐를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1acb4-135">A **QueueRestProxy** object lets you create a queue by using the **createQueue** method.</span></span> <span data-ttu-id="1acb4-136">큐를 만드는 경우 큐에 대한 옵션을 설정할 수 있으나 반드시 옵션을 설정해야 하는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="1acb4-136">When creating a queue, you can set options on the queue, but doing so is not required.</span></span> <span data-ttu-id="1acb4-137">아래 예제에서는 큐에 대해 메타데이터를 설정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1acb4-137">(The example below shows how to set metadata on a queue.)</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Queue\Models\CreateQueueOptions;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

// OPTIONAL: Set queue metadata.
$createQueueOptions = new CreateQueueOptions();
$createQueueOptions->addMetaData("key1", "value1");
$createQueueOptions->addMetaData("key2", "value2");

try    {
    // Create queue.
    $queueRestProxy->createQueue("myqueue", $createQueueOptions);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

> [!NOTE]
> <span data-ttu-id="1acb4-138">메타데이터 키에서 대/소문자를 구분하려고 하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1acb4-138">You should not rely on case sensitivity for metadata keys.</span></span> <span data-ttu-id="1acb4-139">모든 키는 서비스에서 소문자로 읽혀집니다.</span><span class="sxs-lookup"><span data-stu-id="1acb4-139">All keys are read from the service in lowercase.</span></span>
> 
> 

## <a name="add-a-message-to-a-queue"></a><span data-ttu-id="1acb4-140">큐에 메시지 추가</span><span class="sxs-lookup"><span data-stu-id="1acb4-140">Add a message to a queue</span></span>
<span data-ttu-id="1acb4-141">큐에 메시지를 추가하려면 **QueueRestProxy->createMessage**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1acb4-141">To add a message to a queue, use **QueueRestProxy->createMessage**.</span></span> <span data-ttu-id="1acb4-142">이 메서드는 큐 이름, 메시지 텍스트 및 메시지 옵션(선택적)을 인수로 받아들입니다.</span><span class="sxs-lookup"><span data-stu-id="1acb4-142">The method takes the queue name, the message text, and message options (which are optional).</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Queue\Models\CreateMessageOptions;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

try    {
    // Create message.
    $builder = new ServicesBuilder();
    $queueRestProxy->createMessage("myqueue", "Hello World!");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="peek-at-the-next-message"></a><span data-ttu-id="1acb4-143">다음 메시지 보기</span><span class="sxs-lookup"><span data-stu-id="1acb4-143">Peek at the next message</span></span>
<span data-ttu-id="1acb4-144">큐에서 메시지를 제거하지 않고도 **QueueRestProxy->peekMessages**를 호출하여 큐의 맨 앞에서 단일 메시지 또는 여러 메시지를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1acb4-144">You can peek at a message (or messages) at the front of a queue without removing it from the queue by calling **QueueRestProxy->peekMessages**.</span></span> <span data-ttu-id="1acb4-145">기본적으로, **peekMessage** 메서드는 단일 메시지를 반환하지만 **PeekMessagesOptions->setNumberOfMessages** 메서드를 사용하면 이 값을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1acb4-145">By default, the **peekMessage** method returns a single message, but you can change that value by using the **PeekMessagesOptions->setNumberOfMessages** method.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Queue\Models\PeekMessagesOptions;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

// OPTIONAL: Set peek message options.
$message_options = new PeekMessagesOptions();
$message_options->setNumberOfMessages(1); // Default value is 1.

try    {
    $peekMessagesResult = $queueRestProxy->peekMessages("myqueue", $message_options);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

$messages = $peekMessagesResult->getQueueMessages();

// View messages.
$messageCount = count($messages);
if($messageCount <= 0){
    echo "There are no messages.<br />";
}
else{
    foreach($messages as $message)    {
        echo "Peeked message:<br />";
        echo "Message Id: ".$message->getMessageId()."<br />";
        echo "Date: ".date_format($message->getInsertionDate(), 'Y-m-d')."<br />";
        echo "Message text: ".$message->getMessageText()."<br /><br />";
    }
}
```

## <a name="de-queue-the-next-message"></a><span data-ttu-id="1acb4-146">큐에서 다음 메시지 제거</span><span class="sxs-lookup"><span data-stu-id="1acb4-146">De-queue the next message</span></span>
<span data-ttu-id="1acb4-147">다음 코드는 2단계를 거쳐 큐에서 메시지를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="1acb4-147">Your code removes a message from a queue in two steps.</span></span> <span data-ttu-id="1acb4-148">먼저 **QueueRestProxy->listMessages**를 호출하여 큐에서 읽어들이는 메시지가 다른 코드에 표시되지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1acb4-148">First, you call **QueueRestProxy->listMessages**, which makes the message invisible to any other code that's reading from the queue.</span></span> <span data-ttu-id="1acb4-149">기본적으로 이 메시지는 30초간 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1acb4-149">By default, this message will stay invisible for 30 seconds.</span></span> <span data-ttu-id="1acb4-150">이 기간 동안 메시지를 삭제하지 않으면 큐에서 해당 메시지가 다시 표시됩니다. 큐에서 메시지 제거를 완료하려면 **QueueRestProxy->deleteMessage**를 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1acb4-150">(If the message is not deleted in this time period, it will become visible on the queue again.) To finish removing the message from the queue, you must call **QueueRestProxy->deleteMessage**.</span></span> <span data-ttu-id="1acb4-151">메시지를 제거하는 이 2단계 프로세스는 코드가 하드웨어 또는 소프트웨어 오류로 인해 메시지를 처리하지 못하는 경우 코드의 다른 인스턴스가 동일한 메시지를 가져와서 다시 시도할 수 있도록 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="1acb4-151">This two-step process of removing a message assures that when your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="1acb4-152">코드는 메시지가 처리된 직후에 **deleteMessage** 를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="1acb4-152">Your code calls **deleteMessage** right after the message has been processed.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

// Get message.
$listMessagesResult = $queueRestProxy->listMessages("myqueue");
$messages = $listMessagesResult->getQueueMessages();
$message = $messages[0];

/* ---------------------
    Process message.
   --------------------- */

// Get message ID and pop receipt.
$messageId = $message->getMessageId();
$popReceipt = $message->getPopReceipt();

try    {
    // Delete message.
    $queueRestProxy->deleteMessage("myqueue", $messageId, $popReceipt);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="change-the-contents-of-a-queued-message"></a><span data-ttu-id="1acb4-153">대기 중인 메시지의 콘텐츠 변경</span><span class="sxs-lookup"><span data-stu-id="1acb4-153">Change the contents of a queued message</span></span>
<span data-ttu-id="1acb4-154">**QueueRestProxy->updateMessage**를 호출하여 큐에 있는 메시지의 콘텐츠를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1acb4-154">You can change the contents of a message in-place in the queue by calling **QueueRestProxy->updateMessage**.</span></span> <span data-ttu-id="1acb4-155">메시지가 작업을 나타내는 경우 이 기능을 사용하여 작업의 상태를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1acb4-155">If the message represents a work task, you could use this feature to update the status of the work task.</span></span> <span data-ttu-id="1acb4-156">다음 코드는 큐 메시지를 새로운 콘텐츠로 업데이트하고 표시 제한 시간이 60초 더 늘어나도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1acb4-156">The following code updates the queue message with new contents, and it sets the visibility timeout to extend another 60 seconds.</span></span> <span data-ttu-id="1acb4-157">그러면 메시지와 연결된 작업의 상태가 저장되고 클라이언트에서 메시지에 대한 작업을 계속할 수 있는 시간이 1분 더 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1acb4-157">This saves the state of work that's associated with the message, and it gives the client another minute to continue working on the message.</span></span> <span data-ttu-id="1acb4-158">이 기술을 사용하여 처리 단계가 하드웨어 또는 소프트웨어 오류로 인해 실패하는 경우 처음부터 시작하지 않고도 큐 메시지에 대한 여러 단계의 워크플로를 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1acb4-158">You could use this technique to track multi-step workflows on queue messages, without having to start over from the beginning if a processing step fails due to hardware or software failure.</span></span> <span data-ttu-id="1acb4-159">일반적으로 재시도 횟수도 유지하고, 메시지가 *n*번 이상 다시 시도되면 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="1acb4-159">Typically, you would keep a retry count as well, and if the message is retried more than *n* times, you would delete it.</span></span> <span data-ttu-id="1acb4-160">이 기능은 처리될 때마다 응용 프로그램 오류를 트리거하는 메시지를 차단하여 보호해 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1acb4-160">This protects against a message that triggers an application error each time it is processed.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

// Get message.
$listMessagesResult = $queueRestProxy->listMessages("myqueue");
$messages = $listMessagesResult->getQueueMessages();
$message = $messages[0];

// Define new message properties.
$new_message_text = "New message text.";
$new_visibility_timeout = 5; // Measured in seconds.

// Get message ID and pop receipt.
$messageId = $message->getMessageId();
$popReceipt = $message->getPopReceipt();

try    {
    // Update message.
    $queueRestProxy->updateMessage("myqueue",
                                $messageId,
                                $popReceipt,
                                $new_message_text,
                                $new_visibility_timeout);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="additional-options-for-de-queuing-messages"></a><span data-ttu-id="1acb4-161">큐에서 메시지를 제거하기 위한 추가적인 옵션</span><span class="sxs-lookup"><span data-stu-id="1acb4-161">Additional options for de-queuing messages</span></span>
<span data-ttu-id="1acb4-162">큐에서 메시지 검색을 사용자 지정할 수 있는 방법으로는 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1acb4-162">There are two ways that you can customize message retrieval from a queue.</span></span> <span data-ttu-id="1acb4-163">먼저, 메시지의 배치(최대 32개)를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1acb4-163">First, you can get a batch of messages (up to 32).</span></span> <span data-ttu-id="1acb4-164">두 번째로, 표시 제한 시간을 더 길거나 더 짧게 설정하여 코드에서 각 메시지를 완전히 처리하는 시간을 늘리거나 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1acb4-164">Second, you can set a longer or shorter visibility timeout, allowing your code more or less time to fully process each message.</span></span> <span data-ttu-id="1acb4-165">다음 코드 예제는 **getMessages** 메서드를 사용하여 한 번 호출에 16개의 메시지를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1acb4-165">The following code example uses the **getMessages** method to get 16 messages in one call.</span></span> <span data-ttu-id="1acb4-166">그런 다음에 **for** 루프를 사용하여 각 메시지를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="1acb4-166">Then it processes each message by using a **for** loop.</span></span> <span data-ttu-id="1acb4-167">또한 각 메시지에 대해 표시하지 않는 제한 시간을 5분으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1acb4-167">It also sets the invisibility timeout to five minutes for each message.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Queue\Models\ListMessagesOptions;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

// Set list message options.
$message_options = new ListMessagesOptions();
$message_options->setVisibilityTimeoutInSeconds(300);
$message_options->setNumberOfMessages(16);

// Get messages.
try{
    $listMessagesResult = $queueRestProxy->listMessages("myqueue",
                                                     $message_options);
    $messages = $listMessagesResult->getQueueMessages();

    foreach($messages as $message){

        /* ---------------------
            Process message.
        --------------------- */

        // Get message Id and pop receipt.
        $messageId = $message->getMessageId();
        $popReceipt = $message->getPopReceipt();

        // Delete message.
        $queueRestProxy->deleteMessage("myqueue", $messageId, $popReceipt);
    }
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="get-queue-length"></a><span data-ttu-id="1acb4-168">큐 길이 가져오기</span><span class="sxs-lookup"><span data-stu-id="1acb4-168">Get queue length</span></span>
<span data-ttu-id="1acb4-169">큐에 있는 메시지의 추정된 개수를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1acb4-169">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="1acb4-170">**QueueRestProxy->getQueueMetadata** 메서드는 큐에 대한 메타데이터를 반환하도록 큐 서비스에 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="1acb4-170">The **QueueRestProxy->getQueueMetadata** method asks the queue service to return metadata about the queue.</span></span> <span data-ttu-id="1acb4-171">반환된 개체에 대해 **getApproximateMessageCount** 메서드를 호출하면 큐에 얼마나 많은 메시지가 있는지 나타내는 개수를 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1acb4-171">Calling the **getApproximateMessageCount** method on the returned object provides a count of how many messages are in a queue.</span></span> <span data-ttu-id="1acb4-172">큐 서비스가 요청에 응답한 후 메시지가 추가되거나 제거될 수 있으므로 이 메시지 수는 근사치일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="1acb4-172">The count is only approximate because messages can be added or removed after the queue service responds to your request.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

try    {
    // Get queue metadata.
    $queue_metadata = $queueRestProxy->getQueueMetadata("myqueue");
    $approx_msg_count = $queue_metadata->getApproximateMessageCount();
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

echo $approx_msg_count;
```

## <a name="delete-a-queue"></a><span data-ttu-id="1acb4-173">큐 삭제</span><span class="sxs-lookup"><span data-stu-id="1acb4-173">Delete a queue</span></span>
<span data-ttu-id="1acb4-174">큐 및 해당 큐의 모든 메시지를 삭제하려면 **QueueRestProxy->deleteQueue** 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="1acb4-174">To delete a queue and all the messages in it, call the **QueueRestProxy->deleteQueue** method.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

try    {
    // Delete queue.
    $queueRestProxy->deleteQueue("myqueue");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="next-steps"></a><span data-ttu-id="1acb4-175">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1acb4-175">Next steps</span></span>
<span data-ttu-id="1acb4-176">이제 Azure 큐 저장소의 기본 사항을 배웠으므로 다음 링크를 따라 좀더 복잡한 저장소 작업에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="1acb4-176">Now that you've learned the basics of Azure Queue storage, follow these links to learn about more complex storage tasks:</span></span>

* <span data-ttu-id="1acb4-177">[Azure 저장소 팀 블로그](http://blogs.msdn.com/b/windowsazurestorage/)(영문)를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="1acb4-177">Visit the [Azure Storage Team blog](http://blogs.msdn.com/b/windowsazurestorage/).</span></span>

<span data-ttu-id="1acb4-178">자세한 내용은 [PHP 개발자 센터](/develop/php/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1acb4-178">For more information, see also the [PHP Developer Center](/develop/php/).</span></span>

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
<span data-ttu-id="1acb4-179">[require_once]: http://www.php.net/manual/en/function.require-once.php</span><span class="sxs-lookup"><span data-stu-id="1acb4-179">[require_once]: http://www.php.net/manual/en/function.require-once.php</span></span>
[Azure Portal]: https://portal.azure.com


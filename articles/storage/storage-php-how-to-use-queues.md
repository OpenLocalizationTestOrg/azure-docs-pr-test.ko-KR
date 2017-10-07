---
title: "PHP에서 큐 저장소 aaaHow toouse | Microsoft Docs"
description: "방법 toouse hello Azure 큐 저장소 서비스 toocreate 및 큐 삭제 및 삽입, 및 메시지 삭제에 대해 알아봅니다. 샘플은 PHP로 작성되었습니다."
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
ms.openlocfilehash: 5034faf3b5f28f72d5b56ac1ce7a5723be697ce6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-php"></a><span data-ttu-id="3e6d5-104">어떻게 toouse PHP에서 큐 저장소</span><span class="sxs-lookup"><span data-stu-id="3e6d5-104">How toouse Queue storage from PHP</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="3e6d5-105">개요</span><span class="sxs-lookup"><span data-stu-id="3e6d5-105">Overview</span></span>
<span data-ttu-id="3e6d5-106">이 가이드 어떻게 tooperform 일반적인 시나리오를 사용 하 여 hello Azure 큐 저장소 서비스에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e6d5-106">This guide will show you how tooperform common scenarios by using hello Azure Queue storage service.</span></span> <span data-ttu-id="3e6d5-107">hello 예제는 PHP 용 Windows SDK hello에서 클래스를 통해 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e6d5-107">hello samples are written via classes from hello Windows SDK for PHP.</span></span> <span data-ttu-id="3e6d5-108">hello 대상된 시나리오 포함 관찰, 및 삭제 큐 메시지 뿐만 아니라 만들기 및 큐 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e6d5-108">hello covered scenarios include inserting, peeking, getting, and deleting queue messages, as well as creating and deleting queues.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="3e6d5-109">PHP 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="3e6d5-109">Create a PHP application</span></span>
<span data-ttu-id="3e6d5-110">Azure 큐 저장소에 액세스 하는 PHP 응용 프로그램 만들기에 대 한 중요 한 점은 hello만 hello 코드 내에서 php의 hello Azure SDK의에서 클래스를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e6d5-110">hello only requirement for creating a PHP application that accesses Azure Queue storage is hello referencing of classes from hello Azure SDK for PHP from within your code.</span></span> <span data-ttu-id="3e6d5-111">모든 개발 도구 toocreate 메모장 등 응용 프로그램을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e6d5-111">You can use any development tools toocreate your application, including Notepad.</span></span>

<span data-ttu-id="3e6d5-112">이 가이드에서는 PHP 응용 프로그램 내에서 로컬로 또는 Azure 웹 역할, 작업자 역할 또는 웹 사이트 내에서 실행되는 코드에서 호출할 수 있는 큐 저장소 기능을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3e6d5-112">In this guide, you will use Queue storage features that can be called within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-hello-azure-client-libraries"></a><span data-ttu-id="3e6d5-113">Hello Azure 클라이언트 라이브러리 가져오기</span><span class="sxs-lookup"><span data-stu-id="3e6d5-113">Get hello Azure Client Libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-tooaccess-queue-storage"></a><span data-ttu-id="3e6d5-114">사용자 응용 프로그램 tooaccess 큐 저장소를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e6d5-114">Configure your application tooaccess Queue storage</span></span>
<span data-ttu-id="3e6d5-115">toouse hello Api 해야 Azure 큐 저장소:</span><span class="sxs-lookup"><span data-stu-id="3e6d5-115">toouse hello APIs for Azure Queue storage, you need to:</span></span>

1. <span data-ttu-id="3e6d5-116">Hello를 사용 하 여 hello 자동 로더 파일 참조 [require_once] 문.</span><span class="sxs-lookup"><span data-stu-id="3e6d5-116">Reference hello autoloader file by using hello [require_once] statement.</span></span>
2. <span data-ttu-id="3e6d5-117">사용할 수 있는 모든 클래스를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="3e6d5-117">Reference any classes that you might use.</span></span>

<span data-ttu-id="3e6d5-118">hello 다음 예제에서는 어떻게 tooinclude hello 자동 로더 파일과 참조 hello **ServicesBuilder** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="3e6d5-118">hello following example shows how tooinclude hello autoloader file and reference hello **ServicesBuilder** class.</span></span>

> [!NOTE]
> <span data-ttu-id="3e6d5-119">이 예제 (및이 문서의 다른 예제) 작성기를 통해 Azure에 대 한 hello PHP 클라이언트 라이브러리를 설치 했는지 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e6d5-119">This example (and other examples in this article) assumes that you have installed hello PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="3e6d5-120">Tooreference hello 할 hello 라이브러리를 수동으로 설치 하는 경우 `WindowsAzure.php` 자동 로더에 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="3e6d5-120">If you installed hello libraries manually, you will need tooreference hello `WindowsAzure.php` autoloader file.</span></span>
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;

```

<span data-ttu-id="3e6d5-121">아래의 hello 예제 hello `require_once` 문에 항상 표시 되지만 hello 예제 tooexecute에 필요한 hello 클래스 에서만 참조 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e6d5-121">In hello examples below, hello `require_once` statement will be shown always, but only hello classes that are necessary for hello example tooexecute will be referenced.</span></span>

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="3e6d5-122">Azure 저장소 연결 설정</span><span class="sxs-lookup"><span data-stu-id="3e6d5-122">Set up an Azure storage connection</span></span>
<span data-ttu-id="3e6d5-123">Azure 큐 저장소 클라이언트 tooinstantiate 먼저 유효한 연결 문자열이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e6d5-123">tooinstantiate an Azure Queue storage client, you must first have a valid connection string.</span></span> <span data-ttu-id="3e6d5-124">hello hello 큐 서비스 연결 문자열에 대 한 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3e6d5-124">hello format for hello queue service connection string is as follows.</span></span>

<span data-ttu-id="3e6d5-125">Live 서비스에 액세스하는 경우:</span><span class="sxs-lookup"><span data-stu-id="3e6d5-125">For accessing a live service:</span></span>

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

<span data-ttu-id="3e6d5-126">Hello 에뮬레이터 저장소에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e6d5-126">For accessing hello emulator storage:</span></span>

```php
UseDevelopmentStorage=true
```

<span data-ttu-id="3e6d5-127">toocreate 모든 Azure 서비스 클라이언트 toouse hello 해야 **ServicesBuilder** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="3e6d5-127">toocreate any Azure service client, you need toouse hello **ServicesBuilder** class.</span></span> <span data-ttu-id="3e6d5-128">Hello 다음 기술 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e6d5-128">You can use either of hello following techniques:</span></span>

* <span data-ttu-id="3e6d5-129">Hello 연결을 통과할 tooit 직접 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="3e6d5-129">Pass hello connection string directly tooit.</span></span>
* <span data-ttu-id="3e6d5-130">사용 하 여 **CloudConfigurationManager (CCM)** toocheck hello 연결 문자열에 대 한 여러 외부 원본:</span><span class="sxs-lookup"><span data-stu-id="3e6d5-130">Use **CloudConfigurationManager (CCM)** toocheck multiple external sources for hello connection string:</span></span>
  * <span data-ttu-id="3e6d5-131">기본적으로 하나의 외부 소스, 환경 변수에 대한 지원이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e6d5-131">By default, it comes with support for one external source—environmental variables.</span></span>
  * <span data-ttu-id="3e6d5-132">Hello를 확장 하 여 새 원본을 추가할 수 있습니다 **ConnectionStringSource** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="3e6d5-132">You can add new sources by extending hello **ConnectionStringSource** class.</span></span>

<span data-ttu-id="3e6d5-133">Hello 여기에 설명 된 예제를 보려면 hello 연결 문자열을 직접 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e6d5-133">For hello examples outlined here, hello connection string will be passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);
```

## <a name="create-a-queue"></a><span data-ttu-id="3e6d5-134">큐 만들기</span><span class="sxs-lookup"><span data-stu-id="3e6d5-134">Create a queue</span></span>
<span data-ttu-id="3e6d5-135">A **QueueRestProxy** 개체를 사용 하면 hello를 사용 하 여 큐를 만들 **createQueue** 메서드.</span><span class="sxs-lookup"><span data-stu-id="3e6d5-135">A **QueueRestProxy** object lets you create a queue by using hello **createQueue** method.</span></span> <span data-ttu-id="3e6d5-136">큐를 만들 때에 hello 큐에는 옵션을 설정할 수 있지만, 이렇게 하면 하지 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e6d5-136">When creating a queue, you can set options on hello queue, but doing so is not required.</span></span> <span data-ttu-id="3e6d5-137">(다음 예제에서는 어떻게 hello 큐에 tooset 메타 데이터입니다.)</span><span class="sxs-lookup"><span data-stu-id="3e6d5-137">(hello example below shows how tooset metadata on a queue.)</span></span>

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
> <span data-ttu-id="3e6d5-138">메타데이터 키에서 대/소문자를 구분하려고 하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e6d5-138">You should not rely on case sensitivity for metadata keys.</span></span> <span data-ttu-id="3e6d5-139">키를 모두 소문자로 hello 서비스에서 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="3e6d5-139">All keys are read from hello service in lowercase.</span></span>
> 
> 

## <a name="add-a-message-tooa-queue"></a><span data-ttu-id="3e6d5-140">메시지 tooa 큐 추가</span><span class="sxs-lookup"><span data-stu-id="3e6d5-140">Add a message tooa queue</span></span>
<span data-ttu-id="3e6d5-141">tooadd 메시지 tooa 큐를 사용 하 여 **QueueRestProxy createMessage->**합니다.</span><span class="sxs-lookup"><span data-stu-id="3e6d5-141">tooadd a message tooa queue, use **QueueRestProxy->createMessage**.</span></span> <span data-ttu-id="3e6d5-142">hello 메서드 hello 큐 이름, hello 메시지 텍스트 및 메시지 (하는 옵션은 선택 사항)을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e6d5-142">hello method takes hello queue name, hello message text, and message options (which are optional).</span></span>

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

## <a name="peek-at-hello-next-message"></a><span data-ttu-id="3e6d5-143">Hello 다음 메시지 피킹</span><span class="sxs-lookup"><span data-stu-id="3e6d5-143">Peek at hello next message</span></span>
<span data-ttu-id="3e6d5-144">호출 하 여 hello 큐에서 제거 하지 않고 큐의 hello 앞에 메시지 (또는 메시지)에서 피킹 수 **QueueRestProxy peekMessages->**합니다.</span><span class="sxs-lookup"><span data-stu-id="3e6d5-144">You can peek at a message (or messages) at hello front of a queue without removing it from hello queue by calling **QueueRestProxy->peekMessages**.</span></span> <span data-ttu-id="3e6d5-145">기본적으로 hello **peekMessage** 메서드는 단일 메시지를 반환 하지만 hello를 사용 하 여 해당 값을 변경할 수 있습니다 **PeekMessagesOptions setNumberOfMessages->** 메서드.</span><span class="sxs-lookup"><span data-stu-id="3e6d5-145">By default, hello **peekMessage** method returns a single message, but you can change that value by using hello **PeekMessagesOptions->setNumberOfMessages** method.</span></span>

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

## <a name="de-queue-hello-next-message"></a><span data-ttu-id="3e6d5-146">Hello 다음 메시지 큐에서 제거</span><span class="sxs-lookup"><span data-stu-id="3e6d5-146">De-queue hello next message</span></span>
<span data-ttu-id="3e6d5-147">다음 코드는 2단계를 거쳐 큐에서 메시지를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="3e6d5-147">Your code removes a message from a queue in two steps.</span></span> <span data-ttu-id="3e6d5-148">먼저, 호출 **QueueRestProxy listMessages->**, hello 메시지에 대 한 보이지 않는 tooany hello 큐에서 읽기를 수행 하는 다른 코드 있게 해줍니다.</span><span class="sxs-lookup"><span data-stu-id="3e6d5-148">First, you call **QueueRestProxy->listMessages**, which makes hello message invisible tooany other code that's reading from hello queue.</span></span> <span data-ttu-id="3e6d5-149">기본적으로 이 메시지는 30초간 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3e6d5-149">By default, this message will stay invisible for 30 seconds.</span></span> <span data-ttu-id="3e6d5-150">(이 기간에 hello 메시지는 삭제 되지 됩니다 hello 큐에 다시.) 호출 해야 toofinish 제거 hello 큐에서에서 메시지를 hello, **QueueRestProxy deleteMessage->**합니다.</span><span class="sxs-lookup"><span data-stu-id="3e6d5-150">(If hello message is not deleted in this time period, it will become visible on hello queue again.) toofinish removing hello message from hello queue, you must call **QueueRestProxy->deleteMessage**.</span></span> <span data-ttu-id="3e6d5-151">이러한 2 단계 프로세스의 메시지를 제거 되었는지를 확인 다시 toohardware 또는 소프트웨어 오류가, 코드의 다른 인스턴스는 메시지를 가져올 수 하 여 코드 실패 tooprocess hello 같은 메시지와 시도 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="3e6d5-151">This two-step process of removing a message assures that when your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="3e6d5-152">코드 호출 **deleteMessage** 직후 hello 메시지를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e6d5-152">Your code calls **deleteMessage** right after hello message has been processed.</span></span>

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

## <a name="change-hello-contents-of-a-queued-message"></a><span data-ttu-id="3e6d5-153">대기 중인된 메시지의 hello 내용을 변경합니다</span><span class="sxs-lookup"><span data-stu-id="3e6d5-153">Change hello contents of a queued message</span></span>
<span data-ttu-id="3e6d5-154">호출 하 여 hello는 메시지 전체 hello 큐에 있는 내용의 압축을 변경할 수 있습니다 **QueueRestProxy updateMessage->**합니다.</span><span class="sxs-lookup"><span data-stu-id="3e6d5-154">You can change hello contents of a message in-place in hello queue by calling **QueueRestProxy->updateMessage**.</span></span> <span data-ttu-id="3e6d5-155">Hello 메시지 작업 작업을 나타내는 경우에이 기능 tooupdate hello hello 작업 작업의 상태를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e6d5-155">If hello message represents a work task, you could use this feature tooupdate hello status of hello work task.</span></span> <span data-ttu-id="3e6d5-156">코드 다음 hello hello 큐 메시지를 새 내용으로 업데이트 하 고 다른 60 초 hello 가시성 제한 시간 tooextend 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e6d5-156">hello following code updates hello queue message with new contents, and it sets hello visibility timeout tooextend another 60 seconds.</span></span> <span data-ttu-id="3e6d5-157">이렇게 하면 hello 메시지와 관련 된 작업의 hello 상태 저장 및 hello 클라이언트 hello 메시지에서 작업 하는 다른 분 toocontinue 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e6d5-157">This saves hello state of work that's associated with hello message, and it gives hello client another minute toocontinue working on hello message.</span></span> <span data-ttu-id="3e6d5-158">부터 hello toohardware 또는 소프트웨어 오류로 인해 실패 하면 처리 단계를 통해 toostart 필요 없이 큐의 메시지에이 기술을 tootrack multi-step 워크플로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e6d5-158">You could use this technique tootrack multi-step workflows on queue messages, without having toostart over from hello beginning if a processing step fails due toohardware or software failure.</span></span> <span data-ttu-id="3e6d5-159">일반적으로는 다시 시도 횟수를 보관할 때 하 고 메시지를 다시 시도 하는 경우 hello 이상  *n*  시간,는 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e6d5-159">Typically, you would keep a retry count as well, and if hello message is retried more than *n* times, you would delete it.</span></span> <span data-ttu-id="3e6d5-160">이 기능은 처리될 때마다 응용 프로그램 오류를 트리거하는 메시지를 차단하여 보호해 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3e6d5-160">This protects against a message that triggers an application error each time it is processed.</span></span>

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

## <a name="additional-options-for-de-queuing-messages"></a><span data-ttu-id="3e6d5-161">큐에서 메시지를 제거하기 위한 추가적인 옵션</span><span class="sxs-lookup"><span data-stu-id="3e6d5-161">Additional options for de-queuing messages</span></span>
<span data-ttu-id="3e6d5-162">큐에서 메시지 검색을 사용자 지정할 수 있는 방법으로는 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e6d5-162">There are two ways that you can customize message retrieval from a queue.</span></span> <span data-ttu-id="3e6d5-163">첫째, 일괄 처리 메시지 (위쪽 too32)을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e6d5-163">First, you can get a batch of messages (up too32).</span></span> <span data-ttu-id="3e6d5-164">둘째, 하면 프로그램 코드를 더 길거나 더 짧은 표시 제한 시간을 설정할 수 있습니다 또는 적은 시간 toofully 각 메시지를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e6d5-164">Second, you can set a longer or shorter visibility timeout, allowing your code more or less time toofully process each message.</span></span> <span data-ttu-id="3e6d5-165">hello 다음 코드 예제에서는 hello **getMessages** 메서드 tooget 16 메시지 한 번 호출에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e6d5-165">hello following code example uses hello **getMessages** method tooget 16 messages in one call.</span></span> <span data-ttu-id="3e6d5-166">그런 다음에 **for** 루프를 사용하여 각 메시지를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="3e6d5-166">Then it processes each message by using a **for** loop.</span></span> <span data-ttu-id="3e6d5-167">또한 각 메시지에 대 한 hello 표시 안 함 시간 초과 toofive 분을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3e6d5-167">It also sets hello invisibility timeout toofive minutes for each message.</span></span>

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

## <a name="get-queue-length"></a><span data-ttu-id="3e6d5-168">큐 길이 가져오기</span><span class="sxs-lookup"><span data-stu-id="3e6d5-168">Get queue length</span></span>
<span data-ttu-id="3e6d5-169">큐에 있는 hello 메시지 수의 예측을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e6d5-169">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="3e6d5-170">hello **QueueRestProxy getQueueMetadata->** 메서드 hello 큐에 대 한 hello 큐 서비스 tooreturn 메타 데이터를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e6d5-170">hello **QueueRestProxy->getQueueMetadata** method asks hello queue service tooreturn metadata about hello queue.</span></span> <span data-ttu-id="3e6d5-171">호출 hello **getApproximateMessageCount** hello에 대 한 메서드는 큐에 있는 메시지의 개수를 제공 하는 개체를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e6d5-171">Calling hello **getApproximateMessageCount** method on hello returned object provides a count of how many messages are in a queue.</span></span> <span data-ttu-id="3e6d5-172">메시지를 추가 하거나 hello 큐 서비스 tooyour 요청 응답 한 후 제거 하기 때문에 hello count 대략적인 값만입니다.</span><span class="sxs-lookup"><span data-stu-id="3e6d5-172">hello count is only approximate because messages can be added or removed after hello queue service responds tooyour request.</span></span>

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

## <a name="delete-a-queue"></a><span data-ttu-id="3e6d5-173">큐 삭제</span><span class="sxs-lookup"><span data-stu-id="3e6d5-173">Delete a queue</span></span>
<span data-ttu-id="3e6d5-174">toodelete는 큐와,에 있는 모든 hello 메시지 호출 hello **QueueRestProxy deleteQueue->** 메서드.</span><span class="sxs-lookup"><span data-stu-id="3e6d5-174">toodelete a queue and all hello messages in it, call hello **QueueRestProxy->deleteQueue** method.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="3e6d5-175">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3e6d5-175">Next steps</span></span>
<span data-ttu-id="3e6d5-176">Azure 큐 저장소의 hello 기본 사항 학습 한, 했으므로 더 복잡 한 저장소 작업에 대 한 이러한 링크 toolearn를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e6d5-176">Now that you've learned hello basics of Azure Queue storage, follow these links toolearn about more complex storage tasks:</span></span>

* <span data-ttu-id="3e6d5-177">Hello 방문 [Azure 저장소 팀 블로그의](http://blogs.msdn.com/b/windowsazurestorage/)합니다.</span><span class="sxs-lookup"><span data-stu-id="3e6d5-177">Visit hello [Azure Storage Team blog](http://blogs.msdn.com/b/windowsazurestorage/).</span></span>

<span data-ttu-id="3e6d5-178">자세한 내용은 참고 항목 hello [PHP 개발자 센터](/develop/php/)합니다.</span><span class="sxs-lookup"><span data-stu-id="3e6d5-178">For more information, see also hello [PHP Developer Center](/develop/php/).</span></span>

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[require_once]: http://www.php.net/manual/en/function.require-once.php
[Azure Portal]: https://portal.azure.com


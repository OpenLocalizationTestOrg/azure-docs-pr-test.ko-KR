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
# <a name="how-toouse-queue-storage-from-php"></a>어떻게 toouse PHP에서 큐 저장소
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>개요
이 가이드 어떻게 tooperform 일반적인 시나리오를 사용 하 여 hello Azure 큐 저장소 서비스에 표시 됩니다. hello 예제는 PHP 용 Windows SDK hello에서 클래스를 통해 기록 됩니다. hello 대상된 시나리오 포함 관찰, 및 삭제 큐 메시지 뿐만 아니라 만들기 및 큐 삭제 됩니다.

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a>PHP 응용 프로그램 만들기
Azure 큐 저장소에 액세스 하는 PHP 응용 프로그램 만들기에 대 한 중요 한 점은 hello만 hello 코드 내에서 php의 hello Azure SDK의에서 클래스를 참조 합니다. 모든 개발 도구 toocreate 메모장 등 응용 프로그램을 사용할 수 있습니다.

이 가이드에서는 PHP 응용 프로그램 내에서 로컬로 또는 Azure 웹 역할, 작업자 역할 또는 웹 사이트 내에서 실행되는 코드에서 호출할 수 있는 큐 저장소 기능을 사용합니다.

## <a name="get-hello-azure-client-libraries"></a>Hello Azure 클라이언트 라이브러리 가져오기
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-tooaccess-queue-storage"></a>사용자 응용 프로그램 tooaccess 큐 저장소를 구성 합니다.
toouse hello Api 해야 Azure 큐 저장소:

1. Hello를 사용 하 여 hello 자동 로더 파일 참조 [require_once] 문.
2. 사용할 수 있는 모든 클래스를 참조합니다.

hello 다음 예제에서는 어떻게 tooinclude hello 자동 로더 파일과 참조 hello **ServicesBuilder** 클래스입니다.

> [!NOTE]
> 이 예제 (및이 문서의 다른 예제) 작성기를 통해 Azure에 대 한 hello PHP 클라이언트 라이브러리를 설치 했는지 가정 합니다. Tooreference hello 할 hello 라이브러리를 수동으로 설치 하는 경우 `WindowsAzure.php` 자동 로더에 파일입니다.
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;

```

아래의 hello 예제 hello `require_once` 문에 항상 표시 되지만 hello 예제 tooexecute에 필요한 hello 클래스 에서만 참조 됩니다.

## <a name="set-up-an-azure-storage-connection"></a>Azure 저장소 연결 설정
Azure 큐 저장소 클라이언트 tooinstantiate 먼저 유효한 연결 문자열이 있어야 합니다. hello hello 큐 서비스 연결 문자열에 대 한 형식은 다음과 같습니다.

Live 서비스에 액세스하는 경우:

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

Hello 에뮬레이터 저장소에 액세스 합니다.

```php
UseDevelopmentStorage=true
```

toocreate 모든 Azure 서비스 클라이언트 toouse hello 해야 **ServicesBuilder** 클래스입니다. Hello 다음 기술 중 하나를 사용할 수 있습니다.

* Hello 연결을 통과할 tooit 직접 문자열입니다.
* 사용 하 여 **CloudConfigurationManager (CCM)** toocheck hello 연결 문자열에 대 한 여러 외부 원본:
  * 기본적으로 하나의 외부 소스, 환경 변수에 대한 지원이 제공됩니다.
  * Hello를 확장 하 여 새 원본을 추가할 수 있습니다 **ConnectionStringSource** 클래스입니다.

Hello 여기에 설명 된 예제를 보려면 hello 연결 문자열을 직접 전달 됩니다.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);
```

## <a name="create-a-queue"></a>큐 만들기
A **QueueRestProxy** 개체를 사용 하면 hello를 사용 하 여 큐를 만들 **createQueue** 메서드. 큐를 만들 때에 hello 큐에는 옵션을 설정할 수 있지만, 이렇게 하면 하지 필요 합니다. (다음 예제에서는 어떻게 hello 큐에 tooset 메타 데이터입니다.)

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
> 메타데이터 키에서 대/소문자를 구분하려고 하면 안 됩니다. 키를 모두 소문자로 hello 서비스에서 읽습니다.
> 
> 

## <a name="add-a-message-tooa-queue"></a>메시지 tooa 큐 추가
tooadd 메시지 tooa 큐를 사용 하 여 **QueueRestProxy createMessage->**합니다. hello 메서드 hello 큐 이름, hello 메시지 텍스트 및 메시지 (하는 옵션은 선택 사항)을 사용 합니다.

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

## <a name="peek-at-hello-next-message"></a>Hello 다음 메시지 피킹
호출 하 여 hello 큐에서 제거 하지 않고 큐의 hello 앞에 메시지 (또는 메시지)에서 피킹 수 **QueueRestProxy peekMessages->**합니다. 기본적으로 hello **peekMessage** 메서드는 단일 메시지를 반환 하지만 hello를 사용 하 여 해당 값을 변경할 수 있습니다 **PeekMessagesOptions setNumberOfMessages->** 메서드.

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

## <a name="de-queue-hello-next-message"></a>Hello 다음 메시지 큐에서 제거
다음 코드는 2단계를 거쳐 큐에서 메시지를 제거합니다. 먼저, 호출 **QueueRestProxy listMessages->**, hello 메시지에 대 한 보이지 않는 tooany hello 큐에서 읽기를 수행 하는 다른 코드 있게 해줍니다. 기본적으로 이 메시지는 30초간 표시되지 않습니다. (이 기간에 hello 메시지는 삭제 되지 됩니다 hello 큐에 다시.) 호출 해야 toofinish 제거 hello 큐에서에서 메시지를 hello, **QueueRestProxy deleteMessage->**합니다. 이러한 2 단계 프로세스의 메시지를 제거 되었는지를 확인 다시 toohardware 또는 소프트웨어 오류가, 코드의 다른 인스턴스는 메시지를 가져올 수 하 여 코드 실패 tooprocess hello 같은 메시지와 시도 하는 경우. 코드 호출 **deleteMessage** 직후 hello 메시지를 처리 합니다.

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

## <a name="change-hello-contents-of-a-queued-message"></a>대기 중인된 메시지의 hello 내용을 변경합니다
호출 하 여 hello는 메시지 전체 hello 큐에 있는 내용의 압축을 변경할 수 있습니다 **QueueRestProxy updateMessage->**합니다. Hello 메시지 작업 작업을 나타내는 경우에이 기능 tooupdate hello hello 작업 작업의 상태를 사용할 수 있습니다. 코드 다음 hello hello 큐 메시지를 새 내용으로 업데이트 하 고 다른 60 초 hello 가시성 제한 시간 tooextend 설정 합니다. 이렇게 하면 hello 메시지와 관련 된 작업의 hello 상태 저장 및 hello 클라이언트 hello 메시지에서 작업 하는 다른 분 toocontinue 제공 합니다. 부터 hello toohardware 또는 소프트웨어 오류로 인해 실패 하면 처리 단계를 통해 toostart 필요 없이 큐의 메시지에이 기술을 tootrack multi-step 워크플로 사용할 수 있습니다. 일반적으로는 다시 시도 횟수를 보관할 때 하 고 메시지를 다시 시도 하는 경우 hello 이상  *n*  시간,는 삭제 합니다. 이 기능은 처리될 때마다 응용 프로그램 오류를 트리거하는 메시지를 차단하여 보호해 줍니다.

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

## <a name="additional-options-for-de-queuing-messages"></a>큐에서 메시지를 제거하기 위한 추가적인 옵션
큐에서 메시지 검색을 사용자 지정할 수 있는 방법으로는 두 가지가 있습니다. 첫째, 일괄 처리 메시지 (위쪽 too32)을 얻을 수 있습니다. 둘째, 하면 프로그램 코드를 더 길거나 더 짧은 표시 제한 시간을 설정할 수 있습니다 또는 적은 시간 toofully 각 메시지를 처리 합니다. hello 다음 코드 예제에서는 hello **getMessages** 메서드 tooget 16 메시지 한 번 호출에서 합니다. 그런 다음에 **for** 루프를 사용하여 각 메시지를 처리합니다. 또한 각 메시지에 대 한 hello 표시 안 함 시간 초과 toofive 분을 설정합니다.

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

## <a name="get-queue-length"></a>큐 길이 가져오기
큐에 있는 hello 메시지 수의 예측을 얻을 수 있습니다. hello **QueueRestProxy getQueueMetadata->** 메서드 hello 큐에 대 한 hello 큐 서비스 tooreturn 메타 데이터를 요청 합니다. 호출 hello **getApproximateMessageCount** hello에 대 한 메서드는 큐에 있는 메시지의 개수를 제공 하는 개체를 반환 합니다. 메시지를 추가 하거나 hello 큐 서비스 tooyour 요청 응답 한 후 제거 하기 때문에 hello count 대략적인 값만입니다.

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

## <a name="delete-a-queue"></a>큐 삭제
toodelete는 큐와,에 있는 모든 hello 메시지 호출 hello **QueueRestProxy deleteQueue->** 메서드.

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

## <a name="next-steps"></a>다음 단계
Azure 큐 저장소의 hello 기본 사항 학습 한, 했으므로 더 복잡 한 저장소 작업에 대 한 이러한 링크 toolearn를 수행 합니다.

* Hello 방문 [Azure 저장소 팀 블로그의](http://blogs.msdn.com/b/windowsazurestorage/)합니다.

자세한 내용은 참고 항목 hello [PHP 개발자 센터](/develop/php/)합니다.

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[require_once]: http://www.php.net/manual/en/function.require-once.php
[Azure Portal]: https://portal.azure.com


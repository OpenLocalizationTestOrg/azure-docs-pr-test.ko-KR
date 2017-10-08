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
# <a name="how-toouse-service-bus-queues-with-php"></a>Php toouse 서비스 버스 큐 대기 하는 방법
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

이 가이드에서는 toouse 서비스 버스 큐입니다. hello PHP로 작성 된 100 개의 샘플과 hello를 사용 하 여 [PHP 용 Azure SDK](../php-download-sdk.md)합니다. hello 가이드에서 다루는 시나리오 포함 **큐를 만드는**, **메시지 보내기 및 받기**, 및 **큐 삭제**합니다.

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

## <a name="create-a-php-application"></a>PHP 응용 프로그램 만들기
hello Azure Blob 서비스에 액세스 하는 PHP 응용 프로그램을 만들기 위한 요구 사항은 hello만 hello hello에 클래스 참조 [PHP 용 Azure SDK](../php-download-sdk.md) 에서 코드 내에서. 응용 프로그램 또는 메모장 모든 개발 도구 toocreate를 사용할 수 있습니다.

> [!NOTE]
> PHP 설치 hello 있어야 [OpenSSL 확장](http://php.net/openssl) 설치 되어 있고 활성화 합니다.
> 
> 

이 가이드에서는 PHP 응용 프로그램 내에서 로컬로 또는 Azure 웹 역할, 작업자 역할 또는 웹 사이트 내에서 실행되는 코드에서 호출할 수 있는 서비스 기능을 사용합니다.

## <a name="get-hello-azure-client-libraries"></a>Hello Azure 클라이언트 라이브러리 가져오기
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-toouse-service-bus"></a>사용자 응용 프로그램 toouse 서비스 버스를 구성 합니다.
toouse hello 서비스 버스 큐 Api를 다음 hello지 않습니다.

1. Hello를 사용 하 여 참조 hello 자동 로더에 파일 [require_once] [ require_once] 문.
2. 사용할 수 있는 모든 클래스 참조

hello 다음 예제에서는 어떻게 tooinclude hello 자동 로더 파일과 참조 hello `ServicesBuilder` 클래스입니다.

> [!NOTE]
> 이 예제 (및이 문서의 다른 예제) 작성기를 통해 Azure에 대 한 hello PHP 클라이언트 라이브러리를 설치 했다고 가정 합니다. 수동으로 또는 배 패키지로 hello 라이브러리를 설치 하는 경우에 hello 참조 해야 **WindowsAzure.php** 자동 로더에 파일입니다.
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

아래의 hello 예제 hello `require_once` hello 예제 tooexecute에 필요한 hello 클래스가 참조 하지만 문에 항상 표시 됩니다.

## <a name="set-up-a-service-bus-connection"></a>서비스 버스 연결 설정
서비스 버스 클라이언트 tooinstantiate 있어야 유효한 연결 문자열 형식:

```
Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]
```

여기서 `Endpoint` hello 형식의 일반적으로 `[yourNamespace].servicebus.windows.net`합니다.

toocreate hello를 사용 해야 하는 모든 Azure 서비스 클라이언트 `ServicesBuilder` 클래스입니다. 다음을 수행할 수 있습니다.

* Hello 연결을 통과할 tooit 직접 문자열입니다.
* 사용 하 여 hello **CloudConfigurationManager (CCM)** toocheck hello 연결 문자열에 대 한 여러 외부 원본:
  * 기본적으로 하나의 외부 소스, 환경 변수에 대한 지원이 제공됩니다.
  * Hello를 확장 하 여 새 원본을 추가할 수 있습니다 `ConnectionStringSource` 클래스

Hello 여기에 설명 된 예제를 보려면 hello 연결 문자열은 직접 전달 합니다.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$connectionString = "Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]";

$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);
```

## <a name="create-a-queue"></a>큐 만들기
Hello 통해 서비스 버스 큐에 대 한 관리 작업을 수행할 수 `ServiceBusRestProxy` 클래스입니다. A `ServiceBusRestProxy` hello를 통해 개체가 생성 된 `ServicesBuilder::createServiceBusService` hello 토큰 권한 toomanage 캡슐화 하는 적절 한 연결 문자열의 팩터리 메서드 것입니다.

hello 방법을 예제와 다음 tooinstantiate는 `ServiceBusRestProxy` 호출 `ServiceBusRestProxy->createQueue` toocreate 라는 큐 `myqueue` 내에서 한 `MySBNamespace` 서비스 네임 스페이스:

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
> Hello를 사용할 수 있습니다 `listQueues` 메서드를 `ServiceBusRestProxy` 네임 스페이스 내에서 지정 된 이름의 큐가 이미 있으면 toocheck 개체입니다.
> 
> 

## <a name="send-messages-tooa-queue"></a>송신 메시지 tooa 큐
메시지 tooa 서비스 버스 큐 toosend 응용 프로그램 호출 hello `ServiceBusRestProxy->sendQueueMessage` 메서드. 코드에서 보여 주는 방법을 다음 hello 메시지 toohello toosend `myqueue` 내에서 이전에 만든 큐는 `MySBNamespace` 서비스 네임 스페이스입니다.

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

너무 (보내고 받은에서) 서비스 버스 큐는 hello의 인스턴스 메시지 [BrokeredMessage] [ BrokeredMessage] 클래스입니다. [BrokeredMessage] [ BrokeredMessage] 개체 toohold 사용 되는 사용자 지정 하는 응용 프로그램 관련 속성 및 임의 응용 프로그램 데이터의 본문이 되는 표준 메서드 및 속성 집합이 있습니다.

서비스 버스 큐 최대 메시지 크기는 256KB hello 지원 [표준 계층](service-bus-premium-messaging.md) 및 hello에서 1 MB [Premium 계층](service-bus-premium-messaging.md)합니다. hello 표준 및 사용자 지정 응용 프로그램 속성을 포함 하는 hello 헤더는 64KB의 최대 크기를 가질 수 있습니다. 큐에 유지 하는 메시지의 hello 수를 제한 하지 않으며 cap hello 총 크기는 큐에서 대기 하는 hello 메시지에입니다. 큐 크기의 상한은 5GB입니다.

## <a name="receive-messages-from-a-queue"></a>큐에서 메시지 받기

hello 가장 좋은 방법은 tooreceive 메시지 큐에서은 toouse는 `ServiceBusRestProxy->receiveQueueMessage` 메서드. 메시지는 [*ReceiveAndDelete*](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) 및 [*PeekLock*](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock)의 두 가지 모드로 받을 수 있습니다. **PeekLock** hello 기본값입니다.

사용 하는 경우 [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) 모드에서는 수신은 1 단계 작업입니다; 즉, 서비스 버스 큐의 메시지에 대 한 읽기 요청을 받으면 hello 메시지 사용 되는 것을 표시 하 고 toohello 응용 프로그램을 반환 합니다. [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) 모드는 hello 가장 간단한 모델 이며는 응용 프로그램은 오류의 hello 이벤트에서 메시지를 처리 하지 허용할 수 없는 시나리오에 가장 적합 합니다. toounderstand hello는 hello 소비자 문제에 요청을 수신 하는 시나리오 및 후 처리 하기 전에 크래시 합니다. 서비스 버스 사용 되는 것을 다음 hello 응용 프로그램 다시 시작 되 고 메시지 사용을 시작할 때 hello 메시지를 표시 한 됩니다, 때문에 누락 됩니다 hello 메시지 했던 이전 toohello 크래시를 사용 합니다.

Hello 기본에서 [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) 모드에서는 메시지를 표시 하므로 누락 된 메시지를 허용할 수 없는 가능한 toosupport 응용 프로그램 2 단계 작업을 지정 됩니다. 서비스 버스 요청을 받으면 hello 사용 되는 다음 메시지 toobe 찾습니다, tooprevent 잠급니다 다른 소비자가 수신할 toohello 응용 프로그램 반환 합니다. Hello hello의 두 번째 단계를 완료 hello 응용 프로그램 hello 메시지 처리를 완료 (또는 이후 처리를 위해 안정적으로 저장) 한 후 너무 hello 받은 메시지를 전달 하 여 수신 프로세스`ServiceBusRestProxy->deleteMessage`합니다. 서비스 버스 hello를 표시 하는 경우 `deleteMessage` 호출 hello 메시지를 사용 되 고 표시 하 고 hello 큐에서 제거 합니다.

hello 방법을 예제와 다음 tooreceive 하 고 사용 하 여 메시지 처리 [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) 모드 (hello 기본 모드).

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

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Toohandle 응용 프로그램이 크래시 되는 방법 및 읽을 수 없는 메시지

서비스 버스 기능 toohelp 정상적으로 응용 프로그램 또는 메시지를 처리 하는 데 문제가 오류 로부터 복구를 제공 합니다. 수신기 응용 프로그램 수 없는 경우 몇 가지 이유로 tooprocess 환영 메시지가 다음 hello를 호출할 수 있습니다 `unlockMessage` 메서드를 수신 하는 hello 메시지 (hello 대신 `deleteMessage` 메서드). Hello 큐 내에서 서비스 버스 toounlock hello 메시지 시키며 수신 다시 사용할 수 있는 toobe 확인, 사용자가 여를 많이 사용 응용 프로그램 또는 다른 소비 응용 프로그램에서 동일한 hello 중 하나입니다.

또한 hello 큐 내에서 잠긴 메시지와 관련 된 제한 시간 집합과 hello 응용 프로그램 실패 하기 전에 hello 메시지 tooprocess hello 잠금 제한 시간이 만료 (예를 들어 hello 응용 프로그램이 충돌할 경우), 서비스 버스에서 hello 메시지를 잠금 해제 한 다음 자동으로 사용할 수 있는 toobe 수신 다시 확인 합니다.

Hello hello 응용 프로그램 이벤트 충돌 hello 메시지 처리 전후에 그러나 hello 전에 `deleteMessage` 요청이 발생 한 후 다시 시작할 때 hello 메시지 다시 전달한 toohello 응용 프로그램 됩니다. 이 이라고 하는데 *최소 한 번* 처리; 즉, 각 메시지는 한 번 이상 처리 되지만 특정 상황 hello에 동일한 메시지를 다시 배달 될 수 있습니다. 중복 처리가 다음 추가 추가 hello 시나리오 허용할 수 없는 경우 논리 tooapplications toohandle 중복 메시지 배달이 것이 좋습니다. 이 대개 달성 hello를 사용 하 여 `getMessageId` 메서드 hello 메시지를 배달 시도에서 일관적으로 유지 합니다.

## <a name="next-steps"></a>다음 단계
서비스 버스 큐의 hello 기본 사항 학습 한, 했으므로 참조 [큐, 토픽 및 구독] [ Queues, topics, and subscriptions] 자세한 정보에 대 한 합니다.

자세한 내용은 hello 또한 방문 [PHP 개발자 센터](https://azure.microsoft.com/develop/php/)합니다.

[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[require_once]: http://php.net/require_once



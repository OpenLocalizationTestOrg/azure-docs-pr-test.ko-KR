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
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-php"></a>어떻게 toouse 서비스 버스 토픽 및 구독 PHP

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

이 문서에서는 어떻게 toouse 서비스 버스 항목 및 구독 합니다. hello PHP로 작성 된 100 개의 샘플과 hello를 사용 하 여 [PHP 용 Azure SDK](../php-download-sdk.md)합니다. hello 가이드에서 다루는 시나리오 포함 **항목 및 구독을 만드는**, **구독 필터를 만드는**, **tooa 부분 메시지를 보내는**, **받기 구독에서 메시지**, 및 **항목 및 구독을 삭제**합니다.

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

## <a name="create-a-php-application"></a>PHP 응용 프로그램 만들기
hello Azure Blob 서비스에 액세스 하는 PHP 응용 프로그램을 만들기 위한 요구 사항 hello의 tooreference 클래스 파일인 hello [PHP 용 Azure SDK](../php-download-sdk.md) 에서 코드 내에서. 응용 프로그램 또는 메모장 모든 개발 도구 toocreate를 사용할 수 있습니다.

> [!NOTE]
> PHP 설치 hello 있어야 [OpenSSL 확장](http://php.net/openssl) 설치 되어 있고 활성화 합니다.
> 
> 

이 문서에서는 toouse PHP 응용 프로그램을 로컬로 또는 Azure 웹 역할, 작업자 역할 또는 웹 사이트 내에서 실행 되는 코드에서 호출할 수 있는 기능을 서비스 하는 방법을 설명 합니다.

## <a name="get-hello-azure-client-libraries"></a>Hello Azure 클라이언트 라이브러리 가져오기
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-toouse-service-bus"></a>사용자 응용 프로그램 toouse 서비스 버스를 구성 합니다.
toouse hello 서비스 버스 Api:

1. Hello를 사용 하 여 참조 hello 자동 로더에 파일 [require_once] [ require-once] 문.
2. 사용할 수 있는 모든 클래스 참조

hello 다음 예제에서는 어떻게 tooinclude hello 자동 로더 파일과 참조 hello **ServiceBusService** 클래스입니다.

> [!NOTE]
> 이 예제 (및이 문서의 다른 예제) 작성기를 통해 Azure에 대 한 hello PHP 클라이언트 라이브러리를 설치 했다고 가정 합니다. 수동으로 또는 배 패키지로 hello 라이브러리를 설치 하는 경우에 hello 참조 해야 **WindowsAzure.php** 자동 로더에 파일입니다.
> 
> 

```php
require_once 'vendor\autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

예제 따르는 hello에서 hello `require_once` hello 예제 tooexecute에 필요한 hello 클래스가 참조 하지만 문에 항상 표시 됩니다.

## <a name="set-up-a-service-bus-connection"></a>서비스 버스 연결 설정
이 형식의 올바른 연결 문자열을이 있는 tooinstantiate 먼저 서비스 버스 클라이언트:

```
Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]
```

여기서 `Endpoint` hello 형식의 일반적으로 `https://[yourNamespace].servicebus.windows.net`합니다.

toocreate hello를 사용 해야 하는 모든 Azure 서비스 클라이언트 `ServicesBuilder` 클래스입니다. 다음을 수행할 수 있습니다.

* Hello 연결을 통과할 tooit 직접 문자열입니다.
* 사용 하 여 hello **CloudConfigurationManager (CCM)** toocheck hello 연결 문자열에 대 한 여러 외부 원본:
  * 기본적으로 하나의 외부 소스, 환경 변수에 대한 지원이 제공됩니다.
  * Hello를 확장 하 여 새 원본을 추가할 수 있습니다 `ConnectionStringSource` 클래스입니다.

Hello 여기에 설명 된 예제를 보려면 hello 연결 문자열은 직접 전달 합니다.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$connectionString = "Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]";

$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);
```

## <a name="create-a-topic"></a>토픽 만들기
Hello 통해 서비스 버스 주제에 대 한 관리 작업을 수행할 수 `ServiceBusRestProxy` 클래스입니다. A `ServiceBusRestProxy` hello를 통해 개체가 생성 된 `ServicesBuilder::createServiceBusService` hello 토큰 권한 toomanage 캡슐화 하는 적절 한 연결 문자열의 팩터리 메서드 것입니다.

hello 방법을 예제와 다음 tooinstantiate는 `ServiceBusRestProxy` 호출 `ServiceBusRestProxy->createTopic` toocreate 이라는 항목 `mytopic` 내에서 한 `MySBNamespace` 네임 스페이스:

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
> Hello를 사용할 수 있습니다 `listTopics` 메서드를 `ServiceBusRestProxy` 서비스 네임 스페이스 내에서 지정한 이름 가진 항목을 이미 있는 경우 toocheck 개체입니다.
> 
> 

## <a name="create-a-subscription"></a>구독 만들기
주제 구독에도 hello를 사용 하 여 만들어진 `ServiceBusRestProxy->createSubscription` 메서드. 이름이 지정 된 구독과 hello toohello 구독의 가상 큐에 전달 된 메시지 집합을 제한 하는 선택적 필터가 있을 수 있습니다.

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a>Hello 기본 (MatchAll) 필터와 구독 만들기
hello **MatchAll** 필터는 필터 지정 하지 않으면은 새 구독을 만들 때 사용 되는 hello 기본 필터. Hello 때 **MatchAll** 필터 사용 하는 경우 모든 부분 메시지 게시 된 toohello hello 구독의 가상 큐에 배치 됩니다. hello 다음 예제에서는 'mysubscription' 이라는 구독을 만들고 사용 하 여 기본 hello **MatchAll** 필터입니다.

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

### <a name="create-subscriptions-with-filters"></a>필터를 사용하여 구독 만들기
Toospecify tooa 항목 특정 항목을 구독 내에서 표시 되어야 보낸 메시지 수 있도록 하는 필터를 설정할 수 있습니다. hello 가장 유연한 구독에서 지 원하는 필터 형식은 hello [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter)를 구현 하는 SQL92의 하위 집합입니다. SQL 필터가 있는 게시 된 toohello 항목 hello 메시지의 hello 속성에서 작동 합니다. SqlFilter에 대한 자세한 내용은 [SqlFilter.SqlExpression 속성][sqlfilter]을 참조하십시오.

> [!NOTE]
> 구독에 각 규칙 하지 들어오는 메시지를 처리, 독립적으로 해당 결과 메시지 toohello 구독을 추가 합니다. 또한, 각각의 새 구독에는 기본 **규칙** hello 항목 toohello 구독에서 모든 메시지를 추가 하는 필터를 사용 하는 개체입니다. tooreceive만 메시지 필터와 일치 하는 hello 기본 규칙을 제거 해야 합니다. Hello를 사용 하 여 hello 기본 규칙을 제거할 수 있습니다 `ServiceBusRestProxy->deleteRule` 메서드.
> 
> 

hello 다음 예제에서는 구독을 만드는 라는 `HighMessages` 와 **SqlFilter** 만 사용자 지정 하는 메시지를 선택 하는 `MessageNumber` 3 보다 큰 속성입니다. 참조 [송신 메시지 tooa 항목](#send-messages-to-a-topic) toomessages 사용자 지정 속성을 추가 하는 방법에 대 한 정보에 대 한 합니다.

```php
$subscriptionInfo = new SubscriptionInfo("HighMessages");
$serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);

$serviceBusRestProxy->deleteRule("mytopic", "HighMessages", '$Default');

$ruleInfo = new RuleInfo("HighMessagesRule");
$ruleInfo->withSqlFilter("MessageNumber > 3");
$ruleResult = $serviceBusRestProxy->createRule("mytopic", "HighMessages", $ruleInfo);
```

이 코드를 추가 네임 스페이스의 hello 사용 해야 함을 참고: `WindowsAzure\ServiceBus\Models\SubscriptionInfo`합니다.

마찬가지로, hello 다음 예제에서는 구독을 만드는 라는 `LowMessages` 와 `SqlFilter` 만 설정 된 메시지를 선택 하는 `MessageNumber` 속성 작은 보다 짧거나 too3 합니다.

```php
$subscriptionInfo = new SubscriptionInfo("LowMessages");
$serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);

$serviceBusRestProxy->deleteRule("mytopic", "LowMessages", '$Default');

$ruleInfo = new RuleInfo("LowMessagesRule");
$ruleInfo->withSqlFilter("MessageNumber <= 3");
$ruleResult = $serviceBusRestProxy->createRule("mytopic", "LowMessages", $ruleInfo);
```

이제 메시지를 보내면 toohello `mytopic` 항목을 항상 제공 된다는 구독 tooreceivers toohello `mysubscription` 구독 및 구독 하는 선택적으로 배달 된 tooreceivers toohello `HighMessages` 및 `LowMessages` 구독 드 ( 에 따라 hello 메시지 내용을).

## <a name="send-messages-tooa-topic"></a>Tooa 부분 메시지 보내기
메시지 tooa 서비스 버스 항목 toosend 응용 프로그램 호출 hello `ServiceBusRestProxy->sendTopicMessage` 메서드. 코드에서 보여 주는 방법을 다음 hello 메시지 toohello toosend `mytopic` 항목 내에서 이전에 만든는 `MySBNamespace` 서비스 네임 스페이스입니다.

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

메시지가 전송 tooService 버스 주제는 hello 인스턴스의 [BrokeredMessage] [ BrokeredMessage] 클래스입니다. [BrokeredMessage] [ BrokeredMessage] 개체 표준 속성 및 메서드 뿐 아니라 사용자 지정 응용 프로그램 특정 속성 사용된 toohold 될 수 있는 속성 집합이 있습니다. hello 다음 예제에서는 5 toosend 테스트 toohello 메시지 방법을 `mytopic` 이전에 만든 항목입니다. hello `setProperty` 메서드는 사용 되는 tooadd 사용자 지정 속성 (`MessageNumber`) tooeach 메시지입니다. 해당 hello 참고 `MessageNumber` 각 메시지에 속성 값에 따라 다릅니다 (hello에 나와 있는 것 처럼 구독 받는 값 toodetermine이를 사용할 수 있습니다 [구독을 만들](#create-a-subscription) 섹션):

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

서비스 버스 주제 hello에서 최대 메시지 크기는 256KB 지원 [표준 계층](service-bus-premium-messaging.md) 및 hello에서 1 MB [Premium 계층](service-bus-premium-messaging.md)합니다. hello 표준 및 사용자 지정 응용 프로그램 속성을 포함 하는 hello 헤더는 64KB의 최대 크기를 가질 수 있습니다. Hello 메시지에 항목을 보유할 수에 제한이 없음을 않으며 항목을 보유 하는 hello 메시지의 총 크기 hello 켜져 캡입니다. 토픽 크기의 상한은 5GB입니다. 할당량에 대한 자세한 내용은 [Service Bus 할당량][Service Bus quotas]을 참조하세요.

## <a name="receive-messages-from-a-subscription"></a>구독에서 메시지 받기
구독에서 hello 가장 좋은 방법은 tooreceive 메시지는 toouse는 `ServiceBusRestProxy->receiveSubscriptionMessage` 메서드. 메시지는 [*ReceiveAndDelete* 및 *PeekLock*](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode)의 두 가지 모드로 받을 수 있습니다. **PeekLock** hello 기본값입니다.

Hello를 사용 하는 경우 [ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) 모드에서는 수신은 1 단계 작업입니다; 즉, 서비스 버스 구독에서 메시지에 대 한 읽기 요청을 받으면 hello 메시지 사용 되는 것을 표시 하 고 toohello 반환 응용 프로그램입니다. [ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) * 모드는 hello 가장 간단한 모델 이며는 응용 프로그램은 오류의 hello 이벤트에서 메시지를 처리 하지 허용할 수 없는 시나리오에 가장 적합 합니다. toounderstand hello는 hello 소비자 문제에 요청을 수신 하는 시나리오 및 후 처리 하기 전에 크래시 합니다. 서비스 버스 사용 되는 것을 다음 hello 응용 프로그램 다시 시작 되 고 메시지 사용을 시작할 때 hello 메시지를 표시 한 됩니다, 때문에 누락 됩니다 hello 메시지 했던 이전 toohello 크래시를 사용 합니다.

Hello 기본에서 [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) 모드에서는 메시지를 표시 하므로 누락 된 메시지를 허용할 수 없는 가능한 toosupport 응용 프로그램 2 단계 작업을 지정 됩니다. 서비스 버스 요청을 받으면 다음 메시지 toobe hello 사용 다른 소비자가 수신할 tooprevent 잠근 하 고 toohello 응용 프로그램 반환 찾습니다. Hello hello의 두 번째 단계를 완료 hello 응용 프로그램 hello 메시지 처리를 완료 (또는 이후 처리를 위해 안정적으로 저장) 한 후 너무 hello 받은 메시지를 전달 하 여 수신 프로세스`ServiceBusRestProxy->deleteMessage`합니다. 서비스 버스 hello를 표시 하는 경우 `deleteMessage` 호출 hello 메시지를 사용 되 고 표시 하 고 hello 큐에서 제거 합니다.

hello 방법을 예제와 다음 tooreceive 하 고 사용 하 여 메시지 처리 [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) 모드 (hello 기본 모드). 

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

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a>응용 프로그램 작동이 중단되어 메시지를 읽을 수 없는 문제를 처리하는 방법
서비스 버스 기능 toohelp 정상적으로 응용 프로그램 또는 메시지를 처리 하는 데 문제가 오류 로부터 복구를 제공 합니다. 수신기 응용 프로그램 수 없는 경우 몇 가지 이유로 tooprocess 환영 메시지가 다음 hello를 호출할 수 있습니다 `unlockMessage` 메서드를 수신 하는 hello 메시지 (hello 대신 `deleteMessage` 메서드). Hello 큐 내에서 서비스 버스 toounlock hello 메시지 시키며 수신 다시 사용할 수 있는 toobe 확인, 사용자가 여를 많이 사용 응용 프로그램 또는 다른 소비 응용 프로그램에서 동일한 hello 중 하나입니다.

또한 hello 큐 내에서 잠긴 메시지와 관련 된 제한 시간 집합과 hello 응용 프로그램 실패 하기 전에 hello 메시지 tooprocess hello 잠금 제한 시간이 만료 (예를 들어 hello 응용 프로그램이 충돌할 경우), 서비스 버스에서 hello 메시지를 잠금 해제 한 다음 자동으로 사용할 수 있는 toobe 수신 다시 확인 합니다.

Hello hello 응용 프로그램 이벤트 충돌 hello 메시지 처리 전후에 그러나 hello 전에 `deleteMessage` 요청이 발생 한 후 다시 시작할 때 hello 메시지 다시 전달한 toohello 응용 프로그램 됩니다. 이 이라고 하는데 *최소 한 번* 처리; 즉, 각 메시지는 한 번 이상 처리 되지만 특정 상황 hello에 동일한 메시지를 다시 배달 될 수 있습니다. Hello 시나리오 중복 처리가 허용 되지 않는, 응용 프로그램 개발자가 tooapplications toohandle 중복 메시지 배달 추가 논리를 추가 해야 합니다. 이 대개 달성 hello를 사용 하 여 `getMessageId` 메서드 hello 메시지를 배달 시도에서 일관적으로 유지 합니다.

## <a name="delete-topics-and-subscriptions"></a>토픽 및 구독 삭제
항목 또는 구독을 사용 하 여 hello toodelete `ServiceBusRestProxy->deleteTopic` 또는 hello `ServiceBusRestProxy->deleteSubscripton` 메서드를 각각. Note는 항목을 삭제 하면 hello 항목으로 등록 하는 모든 구독도 삭제 합니다.

hello 다음 예제에서는 방법과 toodelete 주제 이름 `mytopic` 및 등록 된 구독에 해당 합니다.

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

Hello를 사용 하 여 `deleteSubscription` 메서드를 하면 구독을 삭제 하지 독립적으로:

```php
$serviceBusRestProxy->deleteSubscription("mytopic", "mysubscription");
```

## <a name="next-steps"></a>다음 단계
서비스 버스 큐의 hello 기본 사항 학습 한, 했으므로 참조 [큐, 토픽 및 구독] [ Queues, topics, and subscriptions] 자세한 정보에 대 한 합니다.

[BrokeredMessage]: https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[sqlfilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter
[require-once]: http://php.net/require_once
[Service Bus quotas]: service-bus-quotas.md

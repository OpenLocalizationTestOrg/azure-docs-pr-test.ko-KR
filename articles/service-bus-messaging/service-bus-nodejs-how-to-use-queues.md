---
title: "Node.js의 aaaHow toouse 서비스 버스 큐 | Microsoft Docs"
description: "서비스 버스 toouse Azure에서 Node.js 응용 프로그램에서 대기 하는 방법을 알아봅니다."
services: service-bus-messaging
documentationcenter: nodejs
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a87a00f9-9aba-4c49-a0df-f900a8b67b3f
ms.service: service-bus-messaging
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: c55354b2061c41aba1093cc3f12ce2a1bc37a3cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-nodejs"></a>Node.js와 함께 toouse 서비스 버스 큐 대기 하는 방법

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

이 문서에서는 Node.js와 함께 toouse 서비스 버스 큐 대기 하는 방법을 설명 합니다. JavaScript로 작성 된 hello Node.js Azure 모듈을 사용 하는 hello 샘플 합니다. hello 가이드에서 다루는 시나리오 포함 **큐를 만드는**, **메시지 보내기 및 받기**, 및 **큐 삭제**합니다. 큐에 대 한 자세한 내용은 참조 hello [다음 단계](#next-steps) 섹션.

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="create-a-nodejs-application"></a>Node.js 응용 프로그램 만들기
빈 Node.js 응용 프로그램을 만듭니다. 방법에 대 한 지침은 toocreate는 Node.js 응용 프로그램 참조 [만들기 Node.js 응용 프로그램 tooan Azure 웹 사이트를 배포 하 고][Create and deploy a Node.js application tooan Azure Website], 또는 [Node.js 클라우드 서비스] [ Node.js Cloud Service] Windows PowerShell을 사용 합니다.

## <a name="configure-your-application-toouse-service-bus"></a>사용자 응용 프로그램 toouse 서비스 버스를 구성 합니다.
Azure 서비스 버스 toouse 다운로드 하 여 hello Node.js Azure 패키지를 사용 하 여 합니다. 이 패키지는 hello 서비스 버스 REST 서비스와 통신 하는 라이브러리 집합에 포함 되어 있습니다.

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a>노드 패키지 관리자 (NPM) tooobtain hello 패키지 사용
1. 사용 하 여 hello **Node.js 용 Windows PowerShell** 명령 창 toonavigate toohello **c:\\노드\\sbqueues\\WebRole1** 폴더를 만든 사용자 샘플 응용 프로그램입니다.
2. 형식 **npm 설치 azure** hello 명령 창에서 응답이 느려져서 해야 될 비슷한 toohello 다음 예제 출력:

    ```
    azure@0.7.5 node_modules\azure
        ├── dateformat@1.0.2-1.2.3
        ├── xmlbuilder@0.4.2
        ├── node-uuid@1.2.0
        ├── mime@1.2.9
        ├── underscore@1.4.4
        ├── validator@1.1.1
        ├── tunnel@0.0.2
        ├── wns@0.5.3
        ├── xml2js@0.2.7 (sax@0.5.2)
        └── request@2.21.0 (json-stringify-safe@4.0.0, forever-agent@0.5.0, aws-sign@0.3.0, tunnel-agent@0.3.0, oauth-sign@0.3.0, qs@0.6.5, cookie-jar@0.3.0, node-uuid@1.4.0, http-signature@0.9.11, form-data@0.0.8, hawk@0.13.1)
    ```
3. Hello를 수동으로 실행할 수 있습니다 **ls** 명령 tooverify 하는 **node_modules** 폴더를 만들었습니다. 폴더 찾기 hello 해당 내부 **azure** hello 필요한 라이브러리를 tooaccess 서비스 버스 큐를 포함 하는 패키지입니다.

### <a name="import-hello-module"></a>Hello 모듈 가져오기
메모장 이나 다른 텍스트 편집기를 사용 하 여 추가 hello toohello 맨 뒤 hello **server.js** hello 응용 프로그램의 파일:

```javascript
var azure = require('azure');
```

### <a name="set-up-an-azure-service-bus-connection"></a>Azure 서비스 버스 연결 설정
hello Azure 모듈 읽고 hello 환경 변수 `AZURE_SERVICEBUS_CONNECTION_STRING` tooobtain 정보가 tooconnect tooService 버스 필요 합니다. 호출할 때 hello 계정 정보를 지정 해야이 환경 변수를 설정 하지 않으면 `createServiceBusService`합니다.

Azure 클라우드 서비스에 대 한 구성 파일에서 hello 환경 변수 설정의 예제를 보려면 [저장소와 클라우드 서비스 Node.js][Node.js Cloud Service with Storage]합니다.

Hello에 hello 환경 변수 설정에 대 한 예제 [Azure 포털] [ Azure portal] 는 Azure 웹 사이트를 참조 하십시오. [Node.js 웹 응용 프로그램 저장소와] [ Node.js Web Application with Storage].

## <a name="create-a-queue"></a>큐 만들기
hello **ServiceBusService** 개체를 사용 하면 서비스 버스 큐와 toowork 합니다. hello 다음 코드에서는 **ServiceBusService** 개체입니다. Hello의 hello 위쪽 추가 **server.js** 후 hello 문 tooimport hello Azure 모듈 파일:

```javascript
var serviceBusService = azure.createServiceBusService();
```

호출 하 여 `createQueueIfNotExists` hello에 **ServiceBusService** hello 큐 (있는 경우)에 반환 되 면 지정 된 또는 hello 지정한 이름 가진 새 큐를 만들 개체입니다. hello 다음 코드에서는 `createQueueIfNotExists` toocreate 라는 toohello 큐 연결 또는 `myqueue`:

```javascript
serviceBusService.createQueueIfNotExists('myqueue', function(error){
    if(!error){
        // Queue exists
    }
});
```

hello `createServiceBusService` 메서드는 또한 메시지 시간 toolive 또는 최대 큐 크기와 같은 toooverride 기본 큐 설정을 사용할 수 있는 추가 옵션을 지원 합니다. hello 다음 예제에서는 설정 hello 최대 큐 크기 too5 GB 인데 1 분의 시간 toolive (TTL) 값:

```javascript
var queueOptions = {
      MaxSizeInMegabytes: '5120',
      DefaultMessageTimeToLive: 'PT1M'
    };

serviceBusService.createQueueIfNotExists('myqueue', queueOptions, function(error){
    if(!error){
        // Queue exists
    }
});
```

### <a name="filters"></a>필터
(옵션) 필터링 작업이 적용 된 toooperations 사용 하 여 수행 될 수 있습니다 **ServiceBusService**합니다. 필터링 작업은 로깅, 자동 재시도 등을 포함할 수 있습니다. 필터는 hello 서명으로 메서드를 구현 하는 개체:

```javascript
function handle (requestOptions, next)
```

Hello 요청 옵션에 사전 처리를 수행한 후 hello 메서드를 호출 해야 `next`, 콜백을 뒤 서명에 hello로 전달 합니다.

```javascript
function (returnObject, finalCallback, next)
```

이 콜백 및 후 처리 hello `returnObject` (hello 요청 toohello 서버 로부터 응답 hello) hello 콜백을 호출 해야 하거나 `next` 존재 toocontinue 다른 필터를 처리 하는 경우 또는 간단히 호출할 `finalCallback`, 끝남 hello 서비스 호출 합니다.

재시도 논리를 구현 하는 두 개의 필터 hello Node.js 용 Azure SDK에 포함 된 `ExponentialRetryPolicyFilter` 및 `LinearRetryPolicyFilter`합니다. hello 다음 코드에서는 `ServiceBusService` hello를 사용 하는 개체 `ExponentialRetryPolicyFilter`:

```javascript
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var serviceBusService = azure.createServiceBusService().withFilter(retryOperations);
```

## <a name="send-messages-tooa-queue"></a>송신 메시지 tooa 큐
메시지 tooa 서비스 버스 큐 toosend 응용 프로그램 호출 hello `sendQueueMessage` 메서드 hello **ServiceBusService** 개체입니다. 너무 (보내고 받은에서) 서비스 버스 큐는 메시지 **BrokeredMessage** 개체, 및 표준 속성 집합이 있습니다 (예: **레이블** 및 **TimeToLive**), toohold 사용 되는 사용자 지정 하는 응용 프로그램 관련 속성 및 임의 응용 프로그램 데이터의 본문이 되는 사전입니다. 응용 프로그램 hello 메시지와 문자열을 전달 하 여 hello hello 메시지 본문을 설정할 수 있습니다. 필수 표준 속성이 기본값으로 채워집니다.

hello 다음 예제에서는 toosend toohello 큐 테스트 메시지의 이름을 지정 방법 `myqueue` 를 사용 하 여 `sendQueueMessage`:

```javascript
var message = {
    body: 'Test message',
    customProperties: {
        testproperty: 'TestValue'
    }};
serviceBusService.sendQueueMessage('myqueue', message, function(error){
    if(!error){
        // message sent
    }
});
```

서비스 버스 큐 최대 메시지 크기는 256KB hello 지원 [표준 계층](service-bus-premium-messaging.md) 및 hello에서 1 MB [Premium 계층](service-bus-premium-messaging.md)합니다. hello 표준 및 사용자 지정 응용 프로그램 속성을 포함 하는 hello 헤더는 64KB의 최대 크기를 가질 수 있습니다. 큐에 유지 하는 메시지의 hello 수를 제한 하지 않으며 cap hello 총 크기는 큐에서 대기 하는 hello 메시지에입니다. 이 큐 크기는 생성 시 정의되며 상한이 5GB입니다. 할당량에 대한 자세한 내용은 [Service Bus 할당량][Service Bus quotas]을 참조하세요.

## <a name="receive-messages-from-a-queue"></a>큐에서 메시지 받기
Hello를 사용 하 여 큐에서 메시지가 수신 되 `receiveQueueMessage` 메서드 hello **ServiceBusService** 개체입니다. 기본적으로 메시지는 큐에서 삭제 hello 읽어; 그러나 (미리 보기)를 읽을 수 있으며 설정 hello 선택적 매개 변수 여 hello 큐에서 삭제 하지 않고 hello 메시지 잠금 `isPeekLock` 너무**true**합니다.

읽기의 기본 동작을 hello 및 hello의 일부 수신 작업으로 hello 메시지를 삭제 합니다.는 hello 간단한 모델은 응용 프로그램은 오류의 hello 이벤트에서 메시지를 처리 하지 허용할 수 없는 시나리오에 가장 적합 합니다. toounderstand hello는 hello 소비자 문제에 요청을 수신 하는 시나리오 및 후 처리 하기 전에 크래시 합니다. 서비스 버스 사용 되는 것을 다음 hello 응용 프로그램 다시 시작 되 고 메시지 사용을 시작할 때 hello 메시지를 표시 한 됩니다, 때문에 누락 됩니다 hello 메시지 했던 이전 toohello 크래시를 사용 합니다.

경우 hello `isPeekLock` 매개 변수가 너무 설정 된**true**, hello 수신 하므로 누락 된 메시지를 허용할 수 없는 가능한 toosupport 응용 프로그램 2 단계 작업이 됩니다. 서비스 버스 요청을 받으면 다음 메시지 toobe hello 사용 다른 소비자가 수신할 tooprevent 잠근 하 고 toohello 응용 프로그램 반환 찾습니다. Hello hello의 두 번째 단계를 완료 hello 응용 프로그램 hello 메시지 처리를 완료 (또는 이후 처리를 위해 안정적으로 저장) 한 후 호출 하 여 수신 프로세스 `deleteMessage` 메서드와 hello 메시지 toobe 삭제 매개 변수로 제공 합니다. hello `deleteMessage` 메서드 사용 되는 것 hello 메시지를 표시 하 고 hello 큐에서 제거 합니다.

hello 다음 예제에서는 tooreceive 및 프로세스 메시지 방법을 사용 하 여 `receiveQueueMessage`합니다. hello 예제에서는 먼저 수신 및 삭제 메시지를 한 다음 사용 하 여 메시지를 받는 `isPeekLock` 도**true**, 삭제 hello 메시지를 사용 하 여 다음 `deleteMessage`:

```javascript
serviceBusService.receiveQueueMessage('myqueue', function(error, receivedMessage){
    if(!error){
        // Message received and deleted
    }
});
serviceBusService.receiveQueueMessage('myqueue', { isPeekLock: true }, function(error, lockedMessage){
    if(!error){
        // Message received and locked
        serviceBusService.deleteMessage(lockedMessage, function (deleteError){
            if(!deleteError){
                // Message deleted
            }
        });
    }
});
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Toohandle 응용 프로그램이 크래시 되는 방법 및 읽을 수 없는 메시지
서비스 버스 기능 toohelp 정상적으로 응용 프로그램 또는 메시지를 처리 하는 데 문제가 오류 로부터 복구를 제공 합니다. 수신기 응용 프로그램 수 없는 경우 몇 가지 이유로 tooprocess 환영 메시지가 다음 hello 호출할 수 있는 `unlockMessage` 메서드 hello **ServiceBusService** 개체입니다. 이 서비스 버스 toounlock hello 큐 내에서 메시지 되며 수신 다시 사용할 수 있는 toobe 확인, 사용자가 여를 많이 사용 응용 프로그램 또는 다른 소비 응용 프로그램에서 동일한 hello 중 하나입니다.

또한 hello 큐 내에서 잠긴 메시지와 관련 된 제한 시간 집합과 tooprocess hello 메시지 하기 전에 hello 응용 프로그램 실패 hello 잠금 제한 시간이 만료 (예: hello 응용 프로그램이 충돌할 경우), 서비스 버스는 hello 메시지 잠금을 자동으로 해제 한 다음 사용할 수 있는 toobe 수신 다시 확인 합니다.

Hello hello 응용 프로그램 이벤트 충돌 hello 메시지 처리 전후에 그러나 hello 전에 `deleteMessage` 메서드는 다음 다시 시작할 때 hello 메시지 다시 전달한 toohello 응용 프로그램 됩니다. 이 이라고 하는데 *일단 처리 이상*, 즉, 각 메시지가 최소 한 번 처리 되지만 특정 상황 hello에 동일한 메시지를 다시 배달 될 수 있습니다. Hello 시나리오 중복 처리가 허용 되지 않는, 응용 프로그램 개발자가 추가 논리 tootheir 응용 프로그램을 toohandle 중복 메시지 배달을 추가 해야 합니다. 이 대개 달성 hello를 사용 하 여 **MessageId** 배달 시도 간에 일정 남아 있는 hello 메시지의 속성입니다.

## <a name="next-steps"></a>다음 단계
큐에 대해 자세히 toolearn hello 다음 리소스를 참조 하십시오.

* [큐, 토픽 및 구독][Queues, topics, and subscriptions]
* GitHub의 [Node용 Azure SDK][Azure SDK for Node] 리포지토리
* [Node.js 개발자 센터](https://azure.microsoft.com/develop/nodejs/)

[Azure SDK for Node]: https://github.com/Azure/azure-sdk-for-node
[Azure portal]: https://portal.azure.com

[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[Create and deploy a Node.js application tooan Azure Website]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js Cloud Service with Storage]:../cosmos-db/table-storage-cloud-service-nodejs.md
[Node.js Web Application with Storage]:../cosmos-db/table-storage-how-to-use-nodejs.md
[Service Bus quotas]: service-bus-quotas.md

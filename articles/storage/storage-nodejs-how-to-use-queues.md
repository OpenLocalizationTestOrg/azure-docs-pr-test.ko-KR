---
title: "Node.js에서 큐 저장소 aaaHow toouse | Microsoft Docs"
description: "방법 toouse hello Azure 큐 서비스 toocreate 및 큐 삭제 및 삽입, 및 메시지 삭제에 대해 알아봅니다. 샘플은 Node.js로 작성되었습니다."
services: storage
documentationcenter: nodejs
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: a8a92db0-4333-43dd-a116-28b3147ea401
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 977e5994c0be1b5d71c60b7479698ccb694ab860
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-nodejs"></a>어떻게 toouse Node.js에서 큐 저장소
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-all](../../includes/storage-check-out-samples-all.md)]

## <a name="overview"></a>개요
이 가이드에서는 tooperform 일반적인 시나리오를 사용 하 여 Microsoft Azure 큐 서비스를 hello 하는 방법을 보여 줍니다. hello 샘플 hello Node.js API를 사용 하 여 기록 됩니다. hello 가이드에서 다루는 시나리오 포함 **삽입**, **관찰**, **가져오는**, 및 **삭제** 메시지를 큐와  **만들기 및 큐 삭제**합니다.

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-nodejs-application"></a>Node.js 응용 프로그램 만들기
빈 Node.js 응용 프로그램을 만듭니다. Node.js 응용 프로그램을 만드는 지침은 [Azure 앱 서비스에 Node.js 웹 응용 프로그램을 만들], [빌드하고 Node.js 응용 프로그램 tooan Azure 클라우드 서비스 배포] 또는WindowsPowerShell을사용하여[ 빌드 및 배포 웹 매트릭스를 사용 하는 Node.js 웹 응용 프로그램 tooAzure]합니다.

## <a name="configure-your-application-tooaccess-storage"></a>응용 프로그램 tooAccess 저장소 구성
Azure 저장소 toouse hello 저장소 REST 서비스와 통신 하는 편리한 라이브러리의 집합을 포함 하는 Node.js 용 hello Azure 저장소 SDK 할 수 있습니다.

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a>노드 패키지 관리자 (NPM) tooobtain hello 패키지 사용
1. 와 같은 명령줄 인터페이스를 사용 하 여 **PowerShell** (Windows) **터미널** (Mac) 또는 **를 이용한 적** (Unix) toohello 폴더 예제 응용 프로그램을 만들 위치를 이동 합니다.
2. 형식 **npm 설치 azure storage** hello 명령 창에서. Hello 명령 출력은 다음 예제와 비슷한 toohello입니다.
 
    ```
    azure-storage@0.5.0 node_modules\azure-storage
    +-- extend@1.2.1
    +-- xmlbuilder@0.4.3
    +-- mime@1.2.11
    +-- node-uuid@1.4.3
    +-- validator@3.22.2
    +-- underscore@1.4.4
    +-- readable-stream@1.0.33 (string_decoder@0.10.31, isarray@0.0.1, inherits@2.0.1, core-util-is@1.0.1)
    +-- xml2js@0.2.7 (sax@0.5.2)
    +-- request@2.57.0 (caseless@0.10.0, aws-sign2@0.5.0, forever-agent@0.6.1, stringstream@0.0.4, oauth-sign@0.8.0, tunnel-agent@0.4.1, isstream@0.1.2, json-stringify-safe@5.0.1, bl@0.9.4, combined-stream@1.0.5, qs@3.1.0, mime-types@2.0.14, form-data@0.2.0, http-signature@0.11.0, tough-cookie@2.0.0, hawk@2.3.1, har-validator@1.8.0)
    ```

3. Hello를 수동으로 실행할 수 있습니다 **ls** 명령 tooverify 하는 **노드\_모듈** 폴더를 만들었습니다. 해당 폴더에 있습니다. hello **azure 저장소** 저장소에 액세스 해야 하는 hello 라이브러리를 포함 하는 패키지입니다.

### <a name="import-hello-package"></a>Hello 패키지 가져오기
메모장 이나 다른 텍스트 편집기를 사용 하 여 추가 toohello 위쪽 다음 hello는 **server.js** toouse 저장소 이점을 얻을 수 hello 응용 프로그램의 파일:

```
var azure = require('azure-storage');
```

## <a name="setup-an-azure-storage-connection"></a>Azure 저장소 연결 설정
hello azure 모듈 AZURE hello 환경 변수는 읽기\_저장소\_계정 및 AZURE\_저장소\_액세스\_키 또는 AZURE\_저장소\_연결 \_필요한 정보 tooconnect tooyour Azure 저장소 계정에 대 한 문자열입니다. 호출할 때 hello 계정 정보를 지정 해야 이러한 환경 변수가 설정 되지 않은 경우 **createQueueService**합니다.

Hello에 hello 환경 변수 설정에 대 한 예제 [Azure 포털](https://portal.azure.com) 는 Azure 웹 사이트를 참조 하십시오. [Azure 테이블 서비스 hello 사용 하 여 Node.js 웹 응용 프로그램]합니다.

## <a name="how-to-create-a-queue"></a>큐를 만드는 방법
hello 다음 코드에서는 **QueueService** toowork 큐로 사용할 수 있는 개체입니다.

```
var queueSvc = azure.createQueueService();
```

사용 하 여 hello **createQueueIfNotExists** 이미 존재 하거나 존재 하지 않는 경우 hello 지정한 이름을 가진 새 큐를 만듭니다 경우 hello 지정 된 큐를 반환 하는 메서드.

```
queueSvc.createQueueIfNotExists('myqueue', function(error, result, response){
  if(!error){
    // Queue created or exists
  }
});
```

Hello 큐를 만든 경우 `result.created` 그렇습니다. Hello 큐가 있는 경우 `result.created` 은 false입니다.

### <a name="filters"></a>필터
(옵션) 필터링 작업이 적용 된 toooperations 사용 하 여 수행 될 수 있습니다 **QueueService**합니다. 필터링 작업은 로깅, 자동 재시도 등을 포함할 수 있습니다. 필터는 hello 서명으로 메서드를 구현 하는 개체:

```
function handle (requestOptions, next)
```

Hello 요청 옵션에 전처리를 수행한 후 hello 메서드 toocall "다음" 콜백을 뒤 서명에 hello로 전달 해야 합니다.

```
function (returnObject, finalCallback, next)
```

이 콜백에서 hello returnObject (hello toohello 서버 요청에서에서 응답 hello)를 처리 한 후, hello 콜백 필요 tooeither 단순히 finalCallback를 호출 하거나 다른 필터를 처리 하는 toocontinue 있는 경우 다음에 호출할 hello 그렇지 않으면 tooend 서비스 호출 합니다.

재시도 논리를 구현 하는 두 개의 필터 hello Node.js 용 Azure SDK에 포함 된 **ExponentialRetryPolicyFilter** 및 **LinearRetryPolicyFilter**합니다. hello 다음 만듭니다는 **QueueService** hello를 사용 하는 개체 **ExponentialRetryPolicyFilter**:

```
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var queueSvc = azure.createQueueService().withFilter(retryOperations);
```

## <a name="how-to-insert-a-message-into-a-queue"></a>큐에 메시지를 삽입하는 방법
tooinsert 큐로 사용 하 여 hello 메시지 **createMessage** 메서드를 새 메시지를 만들고 toohello 큐를 추가 합니다.

```
queueSvc.createMessage('myqueue', "Hello world!", function(error, result, response){
  if(!error){
    // Message inserted
  }
});
```

## <a name="how-to-peek-at-hello-next-message"></a>방법: hello 다음 메시지 피킹
Hello를 호출 하 여 hello 큐에서 제거 하지 않고 큐의 hello 앞에 hello 메시지를 피킹할 수 있습니다 **peekMessages** 메서드. 기본적으로 **peekMessages** 는 단일 메시지를 볼 수 있게 해 줍니다.

```
queueSvc.peekMessages('myqueue', function(error, result, response){
  if(!error){
    // Message text is in messages[0].messageText
  }
});
```

hello `result` hello 메시지를 포함 합니다.

> [!NOTE]
> 사용 하 여 **peekMessages** hello 큐에 메시지가 없는 경우 오류가 반환 되지는, 있지만 메시지가 반환 됩니다.
> 
> 

## <a name="how-to-dequeue-hello-next-message"></a>방법: hello 다음 메시지 큐에서 제거
메시지 처리는 2단계 프로세스입니다.

1. Hello 메시지를 큐에서 제거 합니다.
2. Hello 메시지를 삭제 합니다.

toodequeue 메시지를 사용 하 여 **getMessages**합니다. 따라서 hello 메시지 hello 큐에 표시 되지 않는 다른 클라이언트가 처리할 수 있도록 합니다. 메시지를 처리 하는 응용 프로그램 나면 호출할 **deleteMessage** toodelete hello 큐에서 합니다. 다음 예제는 hello 메시지를 가져오고 삭제:

```
queueSvc.getMessages('myqueue', function(error, result, response){
  if(!error){
    // Message text is in messages[0].messageText
    var message = result[0];
    queueSvc.deleteMessage('myqueue', message.messageId, message.popReceipt, function(error, response){
      if(!error){
        //message deleted
      }
    });
  }
});
```

> [!NOTE]
> 기본적으로는 메시지는 이후에 표시 tooother 클라이언트는 30 초 동안만 숨겨집니다. `options.visibilityTimeout` 와 **getMessages**를 사용하여 다른 값을 지정할 수 있습니다.
> 
> [!NOTE]
> 사용 하 여 **getMessages** hello 큐에 메시지가 없는 경우 오류가 반환 되지는, 있지만 메시지가 반환 됩니다.
> 
> 

## <a name="how-to-change-hello-contents-of-a-queued-message"></a>방법: 대기 중인 메시지의 내용을 hello 변경
메시지 내부에서 사용 하 여 hello 큐의 hello 내용을 변경할 수 있습니다 **updateMessage**합니다. 다음 예제는 hello 메시지의 hello 텍스트를 업데이트 합니다.

```
queueSvc.getMessages('myqueue', function(error, result, response){
  if(!error){
    // Got hello message
    var message = result[0];
    queueSvc.updateMessage('myqueue', message.messageId, message.popReceipt, 10, {messageText: 'new text'}, function(error, result, response){
      if(!error){
        // Message updated successfully
      }
    });
  }
});
```

## <a name="how-to-additional-options-for-dequeuing-messages"></a>dequeuing 메시지의 추가옵션을 설정하는 방법
큐에서 메시지 검색을 사용자 지정할 수 있는 방법으로는 두 가지가 있습니다.

* `options.numOfMessages`-일괄 처리 메시지 (위쪽 too32.)를 검색 합니다.
* `options.visibilityTimeout` - 표시하지 않는 시간 제한을 더 길거나 짧게 설정합니다.

hello 다음 예제에서는 hello **getMessages** 메서드 tooget 15 메시지 한 번 호출에서 합니다. 그런 다음에 for 루프를 사용하여 각 메시지를 처리합니다. 또한이 메서드에서 반환 된 모든 메시지에 대 한 hello 표시 안 함 시간 초과 toofive 분을 설정 합니다.

```
queueSvc.getMessages('myqueue', {numOfMessages: 15, visibilityTimeout: 5 * 60}, function(error, result, response){
  if(!error){
    // Messages retreived
    for(var index in result){
      // text is available in result[index].messageText
      var message = result[index];
      queueSvc.deleteMessage(queueName, message.messageId, message.popReceipt, function(error, response){
        if(!error){
          // Message deleted
        }
      });
    }
  }
});
```

## <a name="how-to-get-hello-queue-length"></a>방법: hello 큐 길이 가져오기
hello **getQueueMetadata** hello 대략적인 hello 큐에 대기 중인 메시지 수를 포함 하 여 hello 큐에 대 한 메타 데이터를 반환 합니다.

```
queueSvc.getQueueMetadata('myqueue', function(error, result, response){
  if(!error){
    // Queue length is available in result.approximateMessageCount
  }
});
```

## <a name="how-to-list-queues"></a>큐 나열하는 방법
큐를 사용 하 여 목록 tooretrieve **listQueuesSegmented**합니다. tooretrieve 특정 접두사를 기준으로 목록을 필터링 할 사용 하 여 **listQueuesSegmentedWithPrefix**합니다.

```
queueSvc.listQueuesSegmented(null, function(error, result, response){
  if(!error){
    // result.entries contains hello list of queues
  }
});
```

모든 큐를 반환할 수 없는 경우 `result.continuationToken` hello 첫 번째 매개 변수에 사용할 수 **listQueuesSegmented** 또는의 두 번째 매개 변수를 환영 **listQueuesSegmentedWithPrefix** tooretrieve 더 결과입니다.

## <a name="how-to-delete-a-queue"></a>방법: 큐 삭제
toodelete는 큐와 모든 hello 메시지에 포함 된, 호출 된 **deleteQueue** hello 큐 개체에서 메서드.

```
queueSvc.deleteQueue(queueName, function(error, response){
  if(!error){
    // Queue has been deleted
  }
});
```

모든 메시지를 삭제 하지 않고 큐에서 사용 하 여 tooclear **clearMessages**합니다.

## <a name="how-to-work-with-shared-access-signatures"></a>공유 액세스 서명 작업 방법
공유 액세스 서명 (SAS) 저장소 계정 이름 또는 키를 제공 하지 않고 안전 하 게 tooprovide 세부적인 액세스 tooqueues 됩니다. SAS는 toosubmit 메시지 모바일 앱을 허용 하는 등 사용 되는 tooprovide 제한 된 액세스 tooyour 큐 경우가 많습니다.

Hello를 사용 하 여 SAS를 생성 하는 클라우드 기반 서비스 등는 신뢰할 수 있는 응용 프로그램 **generateSharedAccessSignature** 의 hello **QueueService**, tooan 제공 하 고 신뢰할 수 없는 또는 부분적으로 신뢰할 수 있는 응용 프로그램입니다. 예를 들면 모바일 앱이 여기에 해당됩니다. hello SAS hello 시작에 설명 하는 정책 및 SAS는 hello 하는 동안 유효는 종료 날짜를 사용 하 여 생성으로 액세스 수준 부여한 toohello SAS 소유자 hello.

다음 예제는 hello hello SAS 소유자 tooadd 메시지 toohello 큐 수 있는 새로운 공유 액세스 정책을 생성 이며 100 분 만들어질 hello 시간이 지난 후 만료 됩니다.

```
var startDate = new Date();
var expiryDate = new Date(startDate);
expiryDate.setMinutes(startDate.getMinutes() + 100);
startDate.setMinutes(startDate.getMinutes() - 100);

var sharedAccessPolicy = {
  AccessPolicy: {
    Permissions: azure.QueueUtilities.SharedAccessPermissions.ADD,
    Start: startDate,
    Expiry: expiryDate
  }
};

var queueSAS = queueSvc.generateSharedAccessSignature('myqueue', sharedAccessPolicy);
var host = queueSvc.host;
```

Note 또한 필요에 따라 hello SAS 소유자가 시도할 때 tooaccess hello 큐 제공 hello 호스트 정보 이어야 합니다.

클라이언트 응용 프로그램을 사용 하 여 hello SAS와 다음 hello **QueueServiceWithSAS** hello 큐에 대 한 tooperform 작업 합니다. 다음 예제는 hello toohello 큐를 연결 하 고 메시지를 만듭니다.

```
var sharedQueueService = azure.createQueueServiceWithSas(host, queueSAS);
sharedQueueService.createMessage('myqueue', 'Hello world from SAS!', function(error, result, response){
  if(!error){
    //message added
  }
});
```

Hello SAS가 생성 된 후 추가 액세스를 시도 tooread, 업데이트 또는 메시지 삭제 된 경우, 오류가 반환 됩니다.

### <a name="access-control-lists"></a>액세스 제어 목록
SAS에 대 한 액세스 제어 목록 (ACL) tooset hello 액세스 정책을 사용할 수도 있습니다. 각 클라이언트에 대 한 다른 액세스 정책을 제공 하지만 여러 클라이언트 tooaccess hello 큐 tooallow 원하는 경우에 유용 합니다.

ACL은 각 정책에 ID가 연결된 액세스 정책 배열을 사용하여 구현됩니다. 다음 예제는 hello 두 정책을; 정의 '사용자 1' 및 'user2'에 대 한 하나입니다.

```
var sharedAccessPolicy = {
  user1: {
    Permissions: azure.QueueUtilities.SharedAccessPermissions.PROCESS,
    Start: startDate,
    Expiry: expiryDate
  },
  user2: {
    Permissions: azure.QueueUtilities.SharedAccessPermissions.ADD,
    Start: startDate,
    Expiry: expiryDate
  }
};
```

다음 예제에서는 hello hello에 대 한 현재 ACL **myqueue**, 다음 사용 하 여 hello 새 정책을 추가 **setQueueAcl**합니다. 이 접근 방식을 통해 다음을 수행할 수 있습니다.

```
var extend = require('extend');
queueSvc.getQueueAcl('myqueue', function(error, result, response) {
  if(!error){
    var newSignedIdentifiers = extend(true, result.signedIdentifiers, sharedAccessPolicy);
    queueSvc.setQueueAcl('myqueue', newSignedIdentifiers, function(error, result, response){
      if(!error){
        // ACL set
      }
    });
  }
});
```

한 번 ACL 설정 된 hello, 만들 수 있습니다는 정책에 대 한 hello ID에 따라 SAS 합니다. 다음 예제는 hello 사용자 '2'에 대 한 새 SAS를 만듭니다.

```
queueSAS = queueSvc.generateSharedAccessSignature('myqueue', { Id: 'user2' });
```

## <a name="next-steps"></a>다음 단계
큐 저장소의 hello 기본 사항 학습 한, 했으므로 더 복잡 한 저장소 작업에 대 한 이러한 링크 toolearn을 따릅니다.

* Hello 방문 [Azure 저장소 팀 블로그][Azure Storage Team Blog]합니다.
* Hello 방문 [노드에 대 한 Azure 저장소 SDK] [ Azure Storage SDK for Node] GitHub의 리포지토리 합니다.

[Azure Storage SDK for Node]: https://github.com/Azure/azure-storage-node
[using hello REST API]: http://msdn.microsoft.com/library/azure/hh264518.aspx
[Azure Portal]: https://portal.azure.com
[Azure 앱 서비스에 Node.js 웹 응용 프로그램을 만들]: ../app-service-web/app-service-web-get-started-nodejs.md
[Azure 테이블 서비스 hello 사용 하 여 Node.js 웹 응용 프로그램]: ../app-service-web/storage-nodejs-use-table-storage-web-site.md


[빌드하고 Node.js 응용 프로그램 tooan Azure 클라우드 서비스 배포]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[ 빌드 및 배포 웹 매트릭스를 사용 하는 Node.js 웹 응용 프로그램 tooAzure]: ../app-service-web/web-sites-nodejs-use-webmatrix.md

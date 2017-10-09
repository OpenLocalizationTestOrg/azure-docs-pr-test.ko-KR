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
# <a name="how-toouse-queue-storage-from-nodejs"></a><span data-ttu-id="b83b1-104">어떻게 toouse Node.js에서 큐 저장소</span><span class="sxs-lookup"><span data-stu-id="b83b1-104">How toouse Queue storage from Node.js</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-all](../../includes/storage-check-out-samples-all.md)]

## <a name="overview"></a><span data-ttu-id="b83b1-105">개요</span><span class="sxs-lookup"><span data-stu-id="b83b1-105">Overview</span></span>
<span data-ttu-id="b83b1-106">이 가이드에서는 tooperform 일반적인 시나리오를 사용 하 여 Microsoft Azure 큐 서비스를 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-106">This guide shows you how tooperform common scenarios using hello Microsoft Azure Queue service.</span></span> <span data-ttu-id="b83b1-107">hello 샘플 hello Node.js API를 사용 하 여 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-107">hello samples are written using hello Node.js API.</span></span> <span data-ttu-id="b83b1-108">hello 가이드에서 다루는 시나리오 포함 **삽입**, **관찰**, **가져오는**, 및 **삭제** 메시지를 큐와  **만들기 및 큐 삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-108">hello scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="b83b1-109">Node.js 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="b83b1-109">Create a Node.js Application</span></span>
<span data-ttu-id="b83b1-110">빈 Node.js 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-110">Create a blank Node.js application.</span></span> <span data-ttu-id="b83b1-111">Node.js 응용 프로그램을 만드는 지침은 [Azure 앱 서비스에 Node.js 웹 응용 프로그램을 만들], [빌드하고 Node.js 응용 프로그램 tooan Azure 클라우드 서비스 배포] 또는WindowsPowerShell을사용하여[ 빌드 및 배포 웹 매트릭스를 사용 하는 Node.js 웹 응용 프로그램 tooAzure]합니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-111">For instructions creating a Node.js application, see [Create a Node.js web app in Azure App Service], [Build and deploy a Node.js application tooan Azure Cloud Service] using Windows PowerShell, or [Build and deploy a Node.js web app tooAzure using Web Matrix].</span></span>

## <a name="configure-your-application-tooaccess-storage"></a><span data-ttu-id="b83b1-112">응용 프로그램 tooAccess 저장소 구성</span><span class="sxs-lookup"><span data-stu-id="b83b1-112">Configure Your Application tooAccess Storage</span></span>
<span data-ttu-id="b83b1-113">Azure 저장소 toouse hello 저장소 REST 서비스와 통신 하는 편리한 라이브러리의 집합을 포함 하는 Node.js 용 hello Azure 저장소 SDK 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-113">toouse Azure storage, you need hello Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a><span data-ttu-id="b83b1-114">노드 패키지 관리자 (NPM) tooobtain hello 패키지 사용</span><span class="sxs-lookup"><span data-stu-id="b83b1-114">Use Node Package Manager (NPM) tooobtain hello package</span></span>
1. <span data-ttu-id="b83b1-115">와 같은 명령줄 인터페이스를 사용 하 여 **PowerShell** (Windows) **터미널** (Mac) 또는 **를 이용한 적** (Unix) toohello 폴더 예제 응용 프로그램을 만들 위치를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-115">Use a command-line interface such as **PowerShell** (Windows,) **Terminal** (Mac,) or **Bash** (Unix), navigate toohello folder where you created your sample application.</span></span>
2. <span data-ttu-id="b83b1-116">형식 **npm 설치 azure storage** hello 명령 창에서.</span><span class="sxs-lookup"><span data-stu-id="b83b1-116">Type **npm install azure-storage** in hello command window.</span></span> <span data-ttu-id="b83b1-117">Hello 명령 출력은 다음 예제와 비슷한 toohello입니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-117">Output from hello command is similar toohello following example.</span></span>
 
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

3. <span data-ttu-id="b83b1-118">Hello를 수동으로 실행할 수 있습니다 **ls** 명령 tooverify 하는 **노드\_모듈** 폴더를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-118">You can manually run hello **ls** command tooverify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="b83b1-119">해당 폴더에 있습니다. hello **azure 저장소** 저장소에 액세스 해야 하는 hello 라이브러리를 포함 하는 패키지입니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-119">Inside that folder you will find hello **azure-storage** package, which contains hello libraries you need to access storage.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="b83b1-120">Hello 패키지 가져오기</span><span class="sxs-lookup"><span data-stu-id="b83b1-120">Import hello package</span></span>
<span data-ttu-id="b83b1-121">메모장 이나 다른 텍스트 편집기를 사용 하 여 추가 toohello 위쪽 다음 hello는 **server.js** toouse 저장소 이점을 얻을 수 hello 응용 프로그램의 파일:</span><span class="sxs-lookup"><span data-stu-id="b83b1-121">Using Notepad or another text editor, add hello following toohello top the **server.js** file of hello application where you intend toouse storage:</span></span>

```
var azure = require('azure-storage');
```

## <a name="setup-an-azure-storage-connection"></a><span data-ttu-id="b83b1-122">Azure 저장소 연결 설정</span><span class="sxs-lookup"><span data-stu-id="b83b1-122">Setup an Azure Storage Connection</span></span>
<span data-ttu-id="b83b1-123">hello azure 모듈 AZURE hello 환경 변수는 읽기\_저장소\_계정 및 AZURE\_저장소\_액세스\_키 또는 AZURE\_저장소\_연결 \_필요한 정보 tooconnect tooyour Azure 저장소 계정에 대 한 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-123">hello azure module will read hello environment variables AZURE\_STORAGE\_ACCOUNT and AZURE\_STORAGE\_ACCESS\_KEY, or AZURE\_STORAGE\_CONNECTION\_STRING for information required tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="b83b1-124">호출할 때 hello 계정 정보를 지정 해야 이러한 환경 변수가 설정 되지 않은 경우 **createQueueService**합니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-124">If these environment variables are not set, you must specify hello account information when calling **createQueueService**.</span></span>

<span data-ttu-id="b83b1-125">Hello에 hello 환경 변수 설정에 대 한 예제 [Azure 포털](https://portal.azure.com) 는 Azure 웹 사이트를 참조 하십시오. [Azure 테이블 서비스 hello 사용 하 여 Node.js 웹 응용 프로그램]합니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-125">For an example of setting hello environment variables in hello [Azure Portal](https://portal.azure.com) for an Azure Website, see [Node.js web app using hello Azure Table Service].</span></span>

## <a name="how-to-create-a-queue"></a><span data-ttu-id="b83b1-126">큐를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="b83b1-126">How To: Create a Queue</span></span>
<span data-ttu-id="b83b1-127">hello 다음 코드에서는 **QueueService** toowork 큐로 사용할 수 있는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-127">hello following code creates a **QueueService** object, which enables you toowork with queues.</span></span>

```
var queueSvc = azure.createQueueService();
```

<span data-ttu-id="b83b1-128">사용 하 여 hello **createQueueIfNotExists** 이미 존재 하거나 존재 하지 않는 경우 hello 지정한 이름을 가진 새 큐를 만듭니다 경우 hello 지정 된 큐를 반환 하는 메서드.</span><span class="sxs-lookup"><span data-stu-id="b83b1-128">Use hello **createQueueIfNotExists** method, which returns hello specified queue if it already exists or creates a new queue with hello specified name if it does not already exist.</span></span>

```
queueSvc.createQueueIfNotExists('myqueue', function(error, result, response){
  if(!error){
    // Queue created or exists
  }
});
```

<span data-ttu-id="b83b1-129">Hello 큐를 만든 경우 `result.created` 그렇습니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-129">If hello queue is created, `result.created` is true.</span></span> <span data-ttu-id="b83b1-130">Hello 큐가 있는 경우 `result.created` 은 false입니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-130">If hello queue exists, `result.created` is false.</span></span>

### <a name="filters"></a><span data-ttu-id="b83b1-131">필터</span><span class="sxs-lookup"><span data-stu-id="b83b1-131">Filters</span></span>
<span data-ttu-id="b83b1-132">(옵션) 필터링 작업이 적용 된 toooperations 사용 하 여 수행 될 수 있습니다 **QueueService**합니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-132">Optional filtering operations can be applied toooperations performed using **QueueService**.</span></span> <span data-ttu-id="b83b1-133">필터링 작업은 로깅, 자동 재시도 등을 포함할 수 있습니다. 필터는 hello 서명으로 메서드를 구현 하는 개체:</span><span class="sxs-lookup"><span data-stu-id="b83b1-133">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with hello signature:</span></span>

```
function handle (requestOptions, next)
```

<span data-ttu-id="b83b1-134">Hello 요청 옵션에 전처리를 수행한 후 hello 메서드 toocall "다음" 콜백을 뒤 서명에 hello로 전달 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-134">After doing its preprocessing on hello request options, hello method needs toocall "next" passing a callback with hello following signature:</span></span>

```
function (returnObject, finalCallback, next)
```

<span data-ttu-id="b83b1-135">이 콜백에서 hello returnObject (hello toohello 서버 요청에서에서 응답 hello)를 처리 한 후, hello 콜백 필요 tooeither 단순히 finalCallback를 호출 하거나 다른 필터를 처리 하는 toocontinue 있는 경우 다음에 호출할 hello 그렇지 않으면 tooend 서비스 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-135">In this callback, and after processing hello returnObject (hello response from hello request toohello server), hello callback needs tooeither invoke next if it exists toocontinue processing other filters or simply invoke finalCallback otherwise tooend up hello service invocation.</span></span>

<span data-ttu-id="b83b1-136">재시도 논리를 구현 하는 두 개의 필터 hello Node.js 용 Azure SDK에 포함 된 **ExponentialRetryPolicyFilter** 및 **LinearRetryPolicyFilter**합니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-136">Two filters that implement retry logic are included with hello Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="b83b1-137">hello 다음 만듭니다는 **QueueService** hello를 사용 하는 개체 **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="b83b1-137">hello following creates a **QueueService** object that uses hello **ExponentialRetryPolicyFilter**:</span></span>

```
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var queueSvc = azure.createQueueService().withFilter(retryOperations);
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="b83b1-138">큐에 메시지를 삽입하는 방법</span><span class="sxs-lookup"><span data-stu-id="b83b1-138">How To: Insert a Message into a Queue</span></span>
<span data-ttu-id="b83b1-139">tooinsert 큐로 사용 하 여 hello 메시지 **createMessage** 메서드를 새 메시지를 만들고 toohello 큐를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-139">tooinsert a message into a queue, use hello **createMessage** method to create a new message and add it toohello queue.</span></span>

```
queueSvc.createMessage('myqueue', "Hello world!", function(error, result, response){
  if(!error){
    // Message inserted
  }
});
```

## <a name="how-to-peek-at-hello-next-message"></a><span data-ttu-id="b83b1-140">방법: hello 다음 메시지 피킹</span><span class="sxs-lookup"><span data-stu-id="b83b1-140">How To: Peek at hello Next Message</span></span>
<span data-ttu-id="b83b1-141">Hello를 호출 하 여 hello 큐에서 제거 하지 않고 큐의 hello 앞에 hello 메시지를 피킹할 수 있습니다 **peekMessages** 메서드.</span><span class="sxs-lookup"><span data-stu-id="b83b1-141">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **peekMessages** method.</span></span> <span data-ttu-id="b83b1-142">기본적으로 **peekMessages** 는 단일 메시지를 볼 수 있게 해 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-142">By default, **peekMessages** peeks at a single message.</span></span>

```
queueSvc.peekMessages('myqueue', function(error, result, response){
  if(!error){
    // Message text is in messages[0].messageText
  }
});
```

<span data-ttu-id="b83b1-143">hello `result` hello 메시지를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-143">hello `result` contains hello message.</span></span>

> [!NOTE]
> <span data-ttu-id="b83b1-144">사용 하 여 **peekMessages** hello 큐에 메시지가 없는 경우 오류가 반환 되지는, 있지만 메시지가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-144">Using **peekMessages** when there are no messages in hello queue will not return an error, however no messages will be returned.</span></span>
> 
> 

## <a name="how-to-dequeue-hello-next-message"></a><span data-ttu-id="b83b1-145">방법: hello 다음 메시지 큐에서 제거</span><span class="sxs-lookup"><span data-stu-id="b83b1-145">How To: Dequeue hello Next Message</span></span>
<span data-ttu-id="b83b1-146">메시지 처리는 2단계 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-146">Processing a message is a two-stage process:</span></span>

1. <span data-ttu-id="b83b1-147">Hello 메시지를 큐에서 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-147">Dequeue hello message.</span></span>
2. <span data-ttu-id="b83b1-148">Hello 메시지를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-148">Delete hello message.</span></span>

<span data-ttu-id="b83b1-149">toodequeue 메시지를 사용 하 여 **getMessages**합니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-149">toodequeue a message, use **getMessages**.</span></span> <span data-ttu-id="b83b1-150">따라서 hello 메시지 hello 큐에 표시 되지 않는 다른 클라이언트가 처리할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-150">This makes hello messages invisible in hello queue, so no other clients can process them.</span></span> <span data-ttu-id="b83b1-151">메시지를 처리 하는 응용 프로그램 나면 호출할 **deleteMessage** toodelete hello 큐에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-151">Once your application has processed a message, call **deleteMessage** toodelete it from hello queue.</span></span> <span data-ttu-id="b83b1-152">다음 예제는 hello 메시지를 가져오고 삭제:</span><span class="sxs-lookup"><span data-stu-id="b83b1-152">hello following example gets a message, then deletes it:</span></span>

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
> <span data-ttu-id="b83b1-153">기본적으로는 메시지는 이후에 표시 tooother 클라이언트는 30 초 동안만 숨겨집니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-153">By default, a message is only hidden for 30 seconds, after which it is visible tooother clients.</span></span> <span data-ttu-id="b83b1-154">`options.visibilityTimeout` 와 **getMessages**를 사용하여 다른 값을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-154">You can specify a different value by using `options.visibilityTimeout` with **getMessages**.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="b83b1-155">사용 하 여 **getMessages** hello 큐에 메시지가 없는 경우 오류가 반환 되지는, 있지만 메시지가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-155">Using **getMessages** when there are no messages in hello queue will not return an error, however no messages will be returned.</span></span>
> 
> 

## <a name="how-to-change-hello-contents-of-a-queued-message"></a><span data-ttu-id="b83b1-156">방법: 대기 중인 메시지의 내용을 hello 변경</span><span class="sxs-lookup"><span data-stu-id="b83b1-156">How To: Change hello Contents of a Queued Message</span></span>
<span data-ttu-id="b83b1-157">메시지 내부에서 사용 하 여 hello 큐의 hello 내용을 변경할 수 있습니다 **updateMessage**합니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-157">You can change hello contents of a message in-place in hello queue using **updateMessage**.</span></span> <span data-ttu-id="b83b1-158">다음 예제는 hello 메시지의 hello 텍스트를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-158">hello following example updates hello text of a message:</span></span>

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

## <a name="how-to-additional-options-for-dequeuing-messages"></a><span data-ttu-id="b83b1-159">dequeuing 메시지의 추가옵션을 설정하는 방법</span><span class="sxs-lookup"><span data-stu-id="b83b1-159">How To: Additional Options for Dequeuing Messages</span></span>
<span data-ttu-id="b83b1-160">큐에서 메시지 검색을 사용자 지정할 수 있는 방법으로는 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-160">There are two ways you can customize message retrieval from a queue:</span></span>

* <span data-ttu-id="b83b1-161">`options.numOfMessages`-일괄 처리 메시지 (위쪽 too32.)를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-161">`options.numOfMessages` - Retrieve a batch of messages (up too32.)</span></span>
* <span data-ttu-id="b83b1-162">`options.visibilityTimeout` - 표시하지 않는 시간 제한을 더 길거나 짧게 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-162">`options.visibilityTimeout` - Set a longer or shorter invisibility timeout.</span></span>

<span data-ttu-id="b83b1-163">hello 다음 예제에서는 hello **getMessages** 메서드 tooget 15 메시지 한 번 호출에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-163">hello following example uses hello **getMessages** method tooget 15 messages in one call.</span></span> <span data-ttu-id="b83b1-164">그런 다음에 for 루프를 사용하여 각 메시지를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-164">Then it processes each message using a for loop.</span></span> <span data-ttu-id="b83b1-165">또한이 메서드에서 반환 된 모든 메시지에 대 한 hello 표시 안 함 시간 초과 toofive 분을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-165">It also sets hello invisibility timeout toofive minutes for all messages returned by this method.</span></span>

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

## <a name="how-to-get-hello-queue-length"></a><span data-ttu-id="b83b1-166">방법: hello 큐 길이 가져오기</span><span class="sxs-lookup"><span data-stu-id="b83b1-166">How To: Get hello Queue Length</span></span>
<span data-ttu-id="b83b1-167">hello **getQueueMetadata** hello 대략적인 hello 큐에 대기 중인 메시지 수를 포함 하 여 hello 큐에 대 한 메타 데이터를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-167">hello **getQueueMetadata** returns metadata about hello queue, including hello approximate number of messages waiting in hello queue.</span></span>

```
queueSvc.getQueueMetadata('myqueue', function(error, result, response){
  if(!error){
    // Queue length is available in result.approximateMessageCount
  }
});
```

## <a name="how-to-list-queues"></a><span data-ttu-id="b83b1-168">큐 나열하는 방법</span><span class="sxs-lookup"><span data-stu-id="b83b1-168">How To: List Queues</span></span>
<span data-ttu-id="b83b1-169">큐를 사용 하 여 목록 tooretrieve **listQueuesSegmented**합니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-169">tooretrieve a list of queues, use **listQueuesSegmented**.</span></span> <span data-ttu-id="b83b1-170">tooretrieve 특정 접두사를 기준으로 목록을 필터링 할 사용 하 여 **listQueuesSegmentedWithPrefix**합니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-170">tooretrieve a list filtered by a specific prefix, use **listQueuesSegmentedWithPrefix**.</span></span>

```
queueSvc.listQueuesSegmented(null, function(error, result, response){
  if(!error){
    // result.entries contains hello list of queues
  }
});
```

<span data-ttu-id="b83b1-171">모든 큐를 반환할 수 없는 경우 `result.continuationToken` hello 첫 번째 매개 변수에 사용할 수 **listQueuesSegmented** 또는의 두 번째 매개 변수를 환영 **listQueuesSegmentedWithPrefix** tooretrieve 더 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-171">If all queues cannot be returned, `result.continuationToken` can be used as hello first parameter of **listQueuesSegmented** or hello second parameter of **listQueuesSegmentedWithPrefix** tooretrieve more results.</span></span>

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="b83b1-172">방법: 큐 삭제</span><span class="sxs-lookup"><span data-stu-id="b83b1-172">How To: Delete a Queue</span></span>
<span data-ttu-id="b83b1-173">toodelete는 큐와 모든 hello 메시지에 포함 된, 호출 된 **deleteQueue** hello 큐 개체에서 메서드.</span><span class="sxs-lookup"><span data-stu-id="b83b1-173">toodelete a queue and all hello messages contained in it, call the **deleteQueue** method on hello queue object.</span></span>

```
queueSvc.deleteQueue(queueName, function(error, response){
  if(!error){
    // Queue has been deleted
  }
});
```

<span data-ttu-id="b83b1-174">모든 메시지를 삭제 하지 않고 큐에서 사용 하 여 tooclear **clearMessages**합니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-174">tooclear all messages from a queue without deleting it, use **clearMessages**.</span></span>

## <a name="how-to-work-with-shared-access-signatures"></a><span data-ttu-id="b83b1-175">공유 액세스 서명 작업 방법</span><span class="sxs-lookup"><span data-stu-id="b83b1-175">How to: Work with Shared Access Signatures</span></span>
<span data-ttu-id="b83b1-176">공유 액세스 서명 (SAS) 저장소 계정 이름 또는 키를 제공 하지 않고 안전 하 게 tooprovide 세부적인 액세스 tooqueues 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-176">Shared Access Signatures (SAS) are a secure way tooprovide granular access tooqueues without providing your storage account name or keys.</span></span> <span data-ttu-id="b83b1-177">SAS는 toosubmit 메시지 모바일 앱을 허용 하는 등 사용 되는 tooprovide 제한 된 액세스 tooyour 큐 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-177">SAS are often used tooprovide limited access tooyour queues, such as allowing a mobile app toosubmit messages.</span></span>

<span data-ttu-id="b83b1-178">Hello를 사용 하 여 SAS를 생성 하는 클라우드 기반 서비스 등는 신뢰할 수 있는 응용 프로그램 **generateSharedAccessSignature** 의 hello **QueueService**, tooan 제공 하 고 신뢰할 수 없는 또는 부분적으로 신뢰할 수 있는 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-178">A trusted application such as a cloud-based service generates a SAS using hello **generateSharedAccessSignature** of hello **QueueService**, and provides it tooan untrusted or semi-trusted application.</span></span> <span data-ttu-id="b83b1-179">예를 들면 모바일 앱이 여기에 해당됩니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-179">For example, a mobile app.</span></span> <span data-ttu-id="b83b1-180">hello SAS hello 시작에 설명 하는 정책 및 SAS는 hello 하는 동안 유효는 종료 날짜를 사용 하 여 생성으로 액세스 수준 부여한 toohello SAS 소유자 hello.</span><span class="sxs-lookup"><span data-stu-id="b83b1-180">hello SAS is generated using a policy, which describes hello start and end dates during which hello SAS is valid, as well as hello access level granted toohello SAS holder.</span></span>

<span data-ttu-id="b83b1-181">다음 예제는 hello hello SAS 소유자 tooadd 메시지 toohello 큐 수 있는 새로운 공유 액세스 정책을 생성 이며 100 분 만들어질 hello 시간이 지난 후 만료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-181">hello following example generates a new shared access policy that will allow hello SAS holder tooadd messages toohello queue, and expires 100 minutes after hello time it is created.</span></span>

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

<span data-ttu-id="b83b1-182">Note 또한 필요에 따라 hello SAS 소유자가 시도할 때 tooaccess hello 큐 제공 hello 호스트 정보 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-182">Note that hello host information must be provided also, as it is required when hello SAS holder attempts tooaccess hello queue.</span></span>

<span data-ttu-id="b83b1-183">클라이언트 응용 프로그램을 사용 하 여 hello SAS와 다음 hello **QueueServiceWithSAS** hello 큐에 대 한 tooperform 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-183">hello client application then uses hello SAS with **QueueServiceWithSAS** tooperform operations against hello queue.</span></span> <span data-ttu-id="b83b1-184">다음 예제는 hello toohello 큐를 연결 하 고 메시지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-184">hello following example connects toohello queue and creates a message.</span></span>

```
var sharedQueueService = azure.createQueueServiceWithSas(host, queueSAS);
sharedQueueService.createMessage('myqueue', 'Hello world from SAS!', function(error, result, response){
  if(!error){
    //message added
  }
});
```

<span data-ttu-id="b83b1-185">Hello SAS가 생성 된 후 추가 액세스를 시도 tooread, 업데이트 또는 메시지 삭제 된 경우, 오류가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-185">Since hello SAS was generated with add access, if an attempt were made tooread, update or delete messages, an error would be returned.</span></span>

### <a name="access-control-lists"></a><span data-ttu-id="b83b1-186">액세스 제어 목록</span><span class="sxs-lookup"><span data-stu-id="b83b1-186">Access control lists</span></span>
<span data-ttu-id="b83b1-187">SAS에 대 한 액세스 제어 목록 (ACL) tooset hello 액세스 정책을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-187">You can also use an Access Control List (ACL) tooset hello access policy for a SAS.</span></span> <span data-ttu-id="b83b1-188">각 클라이언트에 대 한 다른 액세스 정책을 제공 하지만 여러 클라이언트 tooaccess hello 큐 tooallow 원하는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-188">This is useful if you wish tooallow multiple clients tooaccess hello queue, but provide different access policies for each client.</span></span>

<span data-ttu-id="b83b1-189">ACL은 각 정책에 ID가 연결된 액세스 정책 배열을 사용하여 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-189">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span></span> <span data-ttu-id="b83b1-190">다음 예제는 hello 두 정책을; 정의 '사용자 1' 및 'user2'에 대 한 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-190">hello  following example defines two policies; one for 'user1' and one for 'user2':</span></span>

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

<span data-ttu-id="b83b1-191">다음 예제에서는 hello hello에 대 한 현재 ACL **myqueue**, 다음 사용 하 여 hello 새 정책을 추가 **setQueueAcl**합니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-191">hello following example gets hello current ACL for **myqueue**, then adds hello new policies using **setQueueAcl**.</span></span> <span data-ttu-id="b83b1-192">이 접근 방식을 통해 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-192">This approach allows:</span></span>

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

<span data-ttu-id="b83b1-193">한 번 ACL 설정 된 hello, 만들 수 있습니다는 정책에 대 한 hello ID에 따라 SAS 합니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-193">Once hello ACL has been set, you can then create a SAS based on hello ID for a policy.</span></span> <span data-ttu-id="b83b1-194">다음 예제는 hello 사용자 '2'에 대 한 새 SAS를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-194">hello following example creates a new SAS for 'user2':</span></span>

```
queueSAS = queueSvc.generateSharedAccessSignature('myqueue', { Id: 'user2' });
```

## <a name="next-steps"></a><span data-ttu-id="b83b1-195">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b83b1-195">Next Steps</span></span>
<span data-ttu-id="b83b1-196">큐 저장소의 hello 기본 사항 학습 한, 했으므로 더 복잡 한 저장소 작업에 대 한 이러한 링크 toolearn을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-196">Now that you've learned hello basics of queue storage, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="b83b1-197">Hello 방문 [Azure 저장소 팀 블로그][Azure Storage Team Blog]합니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-197">Visit hello [Azure Storage Team Blog][Azure Storage Team Blog].</span></span>
* <span data-ttu-id="b83b1-198">Hello 방문 [노드에 대 한 Azure 저장소 SDK] [ Azure Storage SDK for Node] GitHub의 리포지토리 합니다.</span><span class="sxs-lookup"><span data-stu-id="b83b1-198">Visit hello [Azure Storage SDK for Node][Azure Storage SDK for Node] repository on GitHub.</span></span>

[Azure Storage SDK for Node]: https://github.com/Azure/azure-storage-node
[using hello REST API]: http://msdn.microsoft.com/library/azure/hh264518.aspx
[Azure Portal]: https://portal.azure.com
[Azure 앱 서비스에 Node.js 웹 응용 프로그램을 만들]: ../app-service-web/app-service-web-get-started-nodejs.md
[Azure 테이블 서비스 hello 사용 하 여 Node.js 웹 응용 프로그램]: ../app-service-web/storage-nodejs-use-table-storage-web-site.md


[빌드하고 Node.js 응용 프로그램 tooan Azure 클라우드 서비스 배포]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[ 빌드 및 배포 웹 매트릭스를 사용 하는 Node.js 웹 응용 프로그램 tooAzure]: ../app-service-web/web-sites-nodejs-use-webmatrix.md

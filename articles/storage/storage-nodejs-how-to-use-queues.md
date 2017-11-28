---
title: "Node.js에서 큐 저장소를 사용하는 방법 | Microsoft Docs"
description: "Azure 큐 서비스를 사용하여 큐를 작성 및 삭제하고 메시지를 삽입하고 가져오고 삭제하는 방법을 알아봅니다. 샘플은 Node.js로 작성되었습니다."
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
ms.openlocfilehash: e30297bd0cc65105c92d6428035d2e6c156448af
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-queue-storage-from-nodejs"></a><span data-ttu-id="2c3f0-104">Node.js에서 큐 저장소를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="2c3f0-104">How to use Queue storage from Node.js</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-all](../../includes/storage-check-out-samples-all.md)]

## <a name="overview"></a><span data-ttu-id="2c3f0-105">개요</span><span class="sxs-lookup"><span data-stu-id="2c3f0-105">Overview</span></span>
<span data-ttu-id="2c3f0-106">이 가이드에서는 Microsoft Azure 큐 서비스를 사용하여 일반 시나리오를 수행하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-106">This guide shows you how to perform common scenarios using the Microsoft Azure Queue service.</span></span> <span data-ttu-id="2c3f0-107">샘플은 Node.js API를 사용하여 작성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-107">The samples are written using the Node.js API.</span></span> <span data-ttu-id="2c3f0-108">여기서 다루는 시나리오에는 **큐 만들기 및 삭제**뿐만 아니라 큐 메시지 **삽입**, **보기**, **가져오기** 및 **삭제**가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-108">The scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="2c3f0-109">Node.js 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="2c3f0-109">Create a Node.js Application</span></span>
<span data-ttu-id="2c3f0-110">빈 Node.js 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-110">Create a blank Node.js application.</span></span> <span data-ttu-id="2c3f0-111">Node.js 응용 프로그램을 만드는 방법에 대한 지침은 [Azure App Service에서 Node.js 웹앱 만들기], [Azure Cloud Service에 Node.js 응용 프로그램 빌드 및 배포](Windows PowerShell 사용) 또는 [Web Matrix를 사용하여 Azure에 Node.js 웹앱 빌드 및 배포]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-111">For instructions creating a Node.js application, see [Create a Node.js web app in Azure App Service], [Build and deploy a Node.js application to an Azure Cloud Service] using Windows PowerShell, or [Build and deploy a Node.js web app to Azure using Web Matrix].</span></span>

## <a name="configure-your-application-to-access-storage"></a><span data-ttu-id="2c3f0-112">저장소에 액세스하도록 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="2c3f0-112">Configure Your Application to Access Storage</span></span>
<span data-ttu-id="2c3f0-113">Azure 저장소를 사용하려면 저장소 REST 서비스와 통신하는 편리한 라이브러리 집합이 포함되어 있는 Node.js용 Azure 저장소 SDK가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-113">To use Azure storage, you need the Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with the storage REST services.</span></span>

### <a name="use-node-package-manager-npm-to-obtain-the-package"></a><span data-ttu-id="2c3f0-114">NPM(Node Package Manager)을 사용하여 패키지 가져오기</span><span class="sxs-lookup"><span data-stu-id="2c3f0-114">Use Node Package Manager (NPM) to obtain the package</span></span>
1. <span data-ttu-id="2c3f0-115">**PowerShell**(Windows), **Terminal**(Mac) 또는 **Bash** (Unix)과 같은 명령줄 인터페이스를 사용하여 샘플 응용 프로그램을 만든 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-115">Use a command-line interface such as **PowerShell** (Windows,) **Terminal** (Mac,) or **Bash** (Unix), navigate to the folder where you created your sample application.</span></span>
2. <span data-ttu-id="2c3f0-116">명령 창에 **npm install azure-storage** 를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-116">Type **npm install azure-storage** in the command window.</span></span> <span data-ttu-id="2c3f0-117">명령 출력은 다음 예제와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-117">Output from the command is similar to the following example.</span></span>
 
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

3. <span data-ttu-id="2c3f0-118">**ls** 명령을 수동으로 실행하여 **node\_modules** 폴더가 만들어졌는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-118">You can manually run the **ls** command to verify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="2c3f0-119">이 폴더에서 저장소에 액세스하는 데 필요한 라이브러리가 들어 있는 **azure-storage** 패키지를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-119">Inside that folder you will find the **azure-storage** package, which contains the libraries you need to access storage.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="2c3f0-120">패키지 가져오기</span><span class="sxs-lookup"><span data-stu-id="2c3f0-120">Import the package</span></span>
<span data-ttu-id="2c3f0-121">메모장 또는 다른 텍스트 편집기를 사용하여 저장소를 사용할 응용 프로그램의 **server.js** 파일 맨 위에 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-121">Using Notepad or another text editor, add the following to the top the **server.js** file of the application where you intend to use storage:</span></span>

```
var azure = require('azure-storage');
```

## <a name="setup-an-azure-storage-connection"></a><span data-ttu-id="2c3f0-122">Azure 저장소 연결 설정</span><span class="sxs-lookup"><span data-stu-id="2c3f0-122">Setup an Azure Storage Connection</span></span>
<span data-ttu-id="2c3f0-123">Azure 모듈은 AZURE\_STORAGE\_ACCOUNT 및 AZURE\_STORAGE\_ACCESS\_KEY 또는 AZURE\_STORAGE\_CONNECTION\_STRING 환경 변수를 읽고 Azure Storage 계정에 연결하는 데 필요한 정보를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-123">The azure module will read the environment variables AZURE\_STORAGE\_ACCOUNT and AZURE\_STORAGE\_ACCESS\_KEY, or AZURE\_STORAGE\_CONNECTION\_STRING for information required to connect to your Azure storage account.</span></span> <span data-ttu-id="2c3f0-124">이러한 환경 변수가 설정되지 않은 경우 **createQueueService**를 호출할 때 계정 정보를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-124">If these environment variables are not set, you must specify the account information when calling **createQueueService**.</span></span>

<span data-ttu-id="2c3f0-125">Azure 웹 사이트의 [Azure Portal](https://portal.azure.com)에서 환경 변수를 설정하는 방법에 대한 예제는 [Azure Table Service를 사용하는 Node.js 웹앱]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-125">For an example of setting the environment variables in the [Azure Portal](https://portal.azure.com) for an Azure Website, see [Node.js web app using the Azure Table Service].</span></span>

## <a name="how-to-create-a-queue"></a><span data-ttu-id="2c3f0-126">큐를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="2c3f0-126">How To: Create a Queue</span></span>
<span data-ttu-id="2c3f0-127">다음 코드는 **QueueService** 개체를 만들어 큐 작업을 수행할 수 있게 해 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-127">The following code creates a **QueueService** object, which enables you to work with queues.</span></span>

```
var queueSvc = azure.createQueueService();
```

<span data-ttu-id="2c3f0-128">**createQueueIfNotExists** 메서드를 사용합니다. 이 메서드는 지정된 큐가 이미 있으면 해당 큐를 반환하고 지정된 큐가 아직 없으면 지정한 이름으로 새 큐를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-128">Use the **createQueueIfNotExists** method, which returns the specified queue if it already exists or creates a new queue with the specified name if it does not already exist.</span></span>

```
queueSvc.createQueueIfNotExists('myqueue', function(error, result, response){
  if(!error){
    // Queue created or exists
  }
});
```

<span data-ttu-id="2c3f0-129">큐가 만들어지면 `result.created` 는 true가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-129">If the queue is created, `result.created` is true.</span></span> <span data-ttu-id="2c3f0-130">큐가 있을 경우 `result.created` 는 false가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-130">If the queue exists, `result.created` is false.</span></span>

### <a name="filters"></a><span data-ttu-id="2c3f0-131">필터</span><span class="sxs-lookup"><span data-stu-id="2c3f0-131">Filters</span></span>
<span data-ttu-id="2c3f0-132">**QueueService**를 사용하여 수행되는 작업에 선택적 필터링 작업을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-132">Optional filtering operations can be applied to operations performed using **QueueService**.</span></span> <span data-ttu-id="2c3f0-133">필터링 작업은 로깅, 자동 재시도 등을 포함할 수 있습니다. 필터는 시그니쳐가 있는 메서드를 구현하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-133">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with the signature:</span></span>

```
function handle (requestOptions, next)
```

<span data-ttu-id="2c3f0-134">요청 옵션에 대한 전처리를 수행한 후 메서드는 다음 서명을 사용하여 콜백을 전달하는 "next"를 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-134">After doing its preprocessing on the request options, the method needs to call "next" passing a callback with the following signature:</span></span>

```
function (returnObject, finalCallback, next)
```

<span data-ttu-id="2c3f0-135">이 콜백에서 returnObject(서버에 요청 응답 반환)를 처리한 후 콜백은 next(있는 경우)를 호출하여 다른 필터를 계속 처리하거나 finalCallback을 호출하여 서비스 호출을 종료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-135">In this callback, and after processing the returnObject (the response from the request to the server), the callback needs to either invoke next if it exists to continue processing other filters or simply invoke finalCallback otherwise to end up the service invocation.</span></span>

<span data-ttu-id="2c3f0-136">Node.js용 Azure SDK에는 재시도 논리를 구현하는 두 필터 **ExponentialRetryPolicyFilter** 및 **LinearRetryPolicyFilter**가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-136">Two filters that implement retry logic are included with the Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="2c3f0-137">다음은 **ExponentialRetryPolicyFilter**를 사용하는 **QueueService** 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-137">The following creates a **QueueService** object that uses the **ExponentialRetryPolicyFilter**:</span></span>

```
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var queueSvc = azure.createQueueService().withFilter(retryOperations);
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="2c3f0-138">큐에 메시지를 삽입하는 방법</span><span class="sxs-lookup"><span data-stu-id="2c3f0-138">How To: Insert a Message into a Queue</span></span>
<span data-ttu-id="2c3f0-139">큐에 메시지를 삽입하려면 **createMessage** 메서드를 사용하여 새 메시지를 만들고 이 메시지를 큐에 추가하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-139">To insert a message into a queue, use the **createMessage** method to create a new message and add it to the queue.</span></span>

```
queueSvc.createMessage('myqueue', "Hello world!", function(error, result, response){
  if(!error){
    // Message inserted
  }
});
```

## <a name="how-to-peek-at-the-next-message"></a><span data-ttu-id="2c3f0-140">다음 메시지를 보는 방법</span><span class="sxs-lookup"><span data-stu-id="2c3f0-140">How To: Peek at the Next Message</span></span>
<span data-ttu-id="2c3f0-141">큐에서 메시지를 제거하지 않고도 **peekMessages** 메서드를 호출하여 큐의 맨 앞에서 원하는 메시지를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-141">You can peek at the message in the front of a queue without removing it from the queue by calling the **peekMessages** method.</span></span> <span data-ttu-id="2c3f0-142">기본적으로 **peekMessages** 는 단일 메시지를 볼 수 있게 해 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-142">By default, **peekMessages** peeks at a single message.</span></span>

```
queueSvc.peekMessages('myqueue', function(error, result, response){
  if(!error){
    // Message text is in messages[0].messageText
  }
});
```

<span data-ttu-id="2c3f0-143">`result` 에 메시지가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-143">The `result` contains the message.</span></span>

> [!NOTE]
> <span data-ttu-id="2c3f0-144">큐에 메시지가 없을 때 **peekMessages** 를 사용하면 오류가 반환되지 않지만 메시지도 반환되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-144">Using **peekMessages** when there are no messages in the queue will not return an error, however no messages will be returned.</span></span>
> 
> 

## <a name="how-to-dequeue-the-next-message"></a><span data-ttu-id="2c3f0-145">큐에서 다음 메시지를 제거하는 방법</span><span class="sxs-lookup"><span data-stu-id="2c3f0-145">How To: Dequeue the Next Message</span></span>
<span data-ttu-id="2c3f0-146">메시지 처리는 2단계 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-146">Processing a message is a two-stage process:</span></span>

1. <span data-ttu-id="2c3f0-147">메시지를 큐에서 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-147">Dequeue the message.</span></span>
2. <span data-ttu-id="2c3f0-148">메시지를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-148">Delete the message.</span></span>

<span data-ttu-id="2c3f0-149">메시지를 큐에서 제거하려면 **getMessage**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-149">To dequeue a message, use **getMessages**.</span></span> <span data-ttu-id="2c3f0-150">그러면 큐에서 메시지가 보이지 않으므로 다른 클라이언트에서 처리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-150">This makes the messages invisible in the queue, so no other clients can process them.</span></span> <span data-ttu-id="2c3f0-151">응용 프로그램에서 메시지를 처리하고 나면 **deleteMessage** 를 호출하여 큐에서 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-151">Once your application has processed a message, call **deleteMessage** to delete it from the queue.</span></span> <span data-ttu-id="2c3f0-152">다음 예제에서는 메시지를 가져온 후 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-152">The following example gets a message, then deletes it:</span></span>

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
> <span data-ttu-id="2c3f0-153">기본적으로 메시지는 30초 동안만 숨겨져 있다가 다른 클라이언트에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-153">By default, a message is only hidden for 30 seconds, after which it is visible to other clients.</span></span> <span data-ttu-id="2c3f0-154">`options.visibilityTimeout` 와 **getMessages**를 사용하여 다른 값을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-154">You can specify a different value by using `options.visibilityTimeout` with **getMessages**.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="2c3f0-155">큐에 메시지가 없을 때 **getMessages** 를 사용하면 오류가 반환되지 않지만 메시지도 반환되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-155">Using **getMessages** when there are no messages in the queue will not return an error, however no messages will be returned.</span></span>
> 
> 

## <a name="how-to-change-the-contents-of-a-queued-message"></a><span data-ttu-id="2c3f0-156">대기 중인 메시지의 콘텐츠 변경 방법</span><span class="sxs-lookup"><span data-stu-id="2c3f0-156">How To: Change the Contents of a Queued Message</span></span>
<span data-ttu-id="2c3f0-157">**updateMessage**를 사용하면 큐에 있는 메시지의 콘텐츠를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-157">You can change the contents of a message in-place in the queue using **updateMessage**.</span></span> <span data-ttu-id="2c3f0-158">다음 예제에서는 메시지의 텍스트를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-158">The following example updates the text of a message:</span></span>

```
queueSvc.getMessages('myqueue', function(error, result, response){
  if(!error){
    // Got the message
    var message = result[0];
    queueSvc.updateMessage('myqueue', message.messageId, message.popReceipt, 10, {messageText: 'new text'}, function(error, result, response){
      if(!error){
        // Message updated successfully
      }
    });
  }
});
```

## <a name="how-to-additional-options-for-dequeuing-messages"></a><span data-ttu-id="2c3f0-159">dequeuing 메시지의 추가옵션을 설정하는 방법</span><span class="sxs-lookup"><span data-stu-id="2c3f0-159">How To: Additional Options for Dequeuing Messages</span></span>
<span data-ttu-id="2c3f0-160">큐에서 메시지 검색을 사용자 지정할 수 있는 방법으로는 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-160">There are two ways you can customize message retrieval from a queue:</span></span>

* <span data-ttu-id="2c3f0-161">`options.numOfMessages` - 메시지 배치를 검색합니다(최대 32개).</span><span class="sxs-lookup"><span data-stu-id="2c3f0-161">`options.numOfMessages` - Retrieve a batch of messages (up to 32.)</span></span>
* <span data-ttu-id="2c3f0-162">`options.visibilityTimeout` - 표시하지 않는 시간 제한을 더 길거나 짧게 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-162">`options.visibilityTimeout` - Set a longer or shorter invisibility timeout.</span></span>

<span data-ttu-id="2c3f0-163">다음 예에서는 **getMessages** 메서드를 사용하여 한 번 호출에 15개의 메시지를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-163">The following example uses the **getMessages** method to get 15 messages in one call.</span></span> <span data-ttu-id="2c3f0-164">그런 다음에 for 루프를 사용하여 각 메시지를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-164">Then it processes each message using a for loop.</span></span> <span data-ttu-id="2c3f0-165">또한 이 메서드에서 반환되는 모든 메시지의 표시하지 않는 시간 제한을 5분으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-165">It also sets the invisibility timeout to five minutes for all messages returned by this method.</span></span>

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

## <a name="how-to-get-the-queue-length"></a><span data-ttu-id="2c3f0-166">방법: 큐 길이 가져오기</span><span class="sxs-lookup"><span data-stu-id="2c3f0-166">How To: Get the Queue Length</span></span>
<span data-ttu-id="2c3f0-167">**getQueueMetadata** 에서는 큐에서 대기 중인 메시지의 대략적인 수와 같이 큐에 관련된 메타데이터를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-167">The **getQueueMetadata** returns metadata about the queue, including the approximate number of messages waiting in the queue.</span></span>

```
queueSvc.getQueueMetadata('myqueue', function(error, result, response){
  if(!error){
    // Queue length is available in result.approximateMessageCount
  }
});
```

## <a name="how-to-list-queues"></a><span data-ttu-id="2c3f0-168">큐 나열하는 방법</span><span class="sxs-lookup"><span data-stu-id="2c3f0-168">How To: List Queues</span></span>
<span data-ttu-id="2c3f0-169">큐 목록을 검색하려면 **listQueuesSegmented**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-169">To retrieve a list of queues, use **listQueuesSegmented**.</span></span> <span data-ttu-id="2c3f0-170">특정 접두사를 기준으로 필터링된 목록을 검색하려면 **listQueuesSegmentedWithPrefix**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-170">To retrieve a list filtered by a specific prefix, use **listQueuesSegmentedWithPrefix**.</span></span>

```
queueSvc.listQueuesSegmented(null, function(error, result, response){
  if(!error){
    // result.entries contains the list of queues
  }
});
```

<span data-ttu-id="2c3f0-171">큐를 모두 반환할 수 없는 경우에는 `result.continuationToken`을 **listQueuesSegmented**의 첫 번째 매개 변수나 **listQueuesSegmentedWithPrefix**의 두 번째 매개 변수로 사용하여 더 많은 결과를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-171">If all queues cannot be returned, `result.continuationToken` can be used as the first parameter of **listQueuesSegmented** or the second parameter of **listQueuesSegmentedWithPrefix** to retrieve more results.</span></span>

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="2c3f0-172">방법: 큐 삭제</span><span class="sxs-lookup"><span data-stu-id="2c3f0-172">How To: Delete a Queue</span></span>
<span data-ttu-id="2c3f0-173">큐 및 해당 큐의 모든 메시지를 삭제하려면 큐 개체의 **deleteQueue** 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-173">To delete a queue and all the messages contained in it, call the **deleteQueue** method on the queue object.</span></span>

```
queueSvc.deleteQueue(queueName, function(error, response){
  if(!error){
    // Queue has been deleted
  }
});
```

<span data-ttu-id="2c3f0-174">큐를 삭제하지 않고 모든 메시지를 지우려면 **clearMessages**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-174">To clear all messages from a queue without deleting it, use **clearMessages**.</span></span>

## <a name="how-to-work-with-shared-access-signatures"></a><span data-ttu-id="2c3f0-175">공유 액세스 서명 작업 방법</span><span class="sxs-lookup"><span data-stu-id="2c3f0-175">How to: Work with Shared Access Signatures</span></span>
<span data-ttu-id="2c3f0-176">SAS(공유 액세스 서명)는 저장소 계정 이름이나 키를 제공하지 않으면서 큐에 세분화된 액세스 권한을 안전하게 제공하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-176">Shared Access Signatures (SAS) are a secure way to provide granular access to queues without providing your storage account name or keys.</span></span> <span data-ttu-id="2c3f0-177">SAS는 모바일 앱에서 메시지를 제출하도록 허용하는 경우와 같이 큐에 대해 제한된 액세스를 제공하는 경우에 자주 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-177">SAS are often used to provide limited access to your queues, such as allowing a mobile app to submit messages.</span></span>

<span data-ttu-id="2c3f0-178">클라우드 기반 서비스와 같이 신뢰할 수 있는 응용 프로그램에서는 **QueueService**의 **generateSharedAccessSignature**를 사용하여 SAS를 생성하고 신뢰할 수 없거나 신뢰가 약한 응용 프로그램에 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-178">A trusted application such as a cloud-based service generates a SAS using the **generateSharedAccessSignature** of the **QueueService**, and provides it to an untrusted or semi-trusted application.</span></span> <span data-ttu-id="2c3f0-179">예를 들면 모바일 앱이 여기에 해당됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-179">For example, a mobile app.</span></span> <span data-ttu-id="2c3f0-180">SAS는 SAS가 유효한 시작 및 종료 날짜와 SAS 소유자에게 부여되는 액세스 수준을 설명하는 정책을 사용하여 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-180">The SAS is generated using a policy, which describes the start and end dates during which the SAS is valid, as well as the access level granted to the SAS holder.</span></span>

<span data-ttu-id="2c3f0-181">다음 예에서는 SAS 소유자가 큐에 메시지를 추가할 수 있도록 허용하며 만든 후 100분이 지나면 만료되는 새 공유 액세스 정책을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-181">The following example generates a new shared access policy that will allow the SAS holder to add messages to the queue, and expires 100 minutes after the time it is created.</span></span>

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

<span data-ttu-id="2c3f0-182">SAS 소유자가 큐에 액세스할 때 필요하므로 호스트 정보도 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-182">Note that the host information must be provided also, as it is required when the SAS holder attempts to access the queue.</span></span>

<span data-ttu-id="2c3f0-183">그러고 나면 클라이언트 응용 프로그램에서 **QueueServiceWithSAS** 에 SAS를 사용하여 큐에 대한 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-183">The client application then uses the SAS with **QueueServiceWithSAS** to perform operations against the queue.</span></span> <span data-ttu-id="2c3f0-184">다음 예에서는 큐를 연결하고 메시지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-184">The following example connects to the queue and creates a message.</span></span>

```
var sharedQueueService = azure.createQueueServiceWithSas(host, queueSAS);
sharedQueueService.createMessage('myqueue', 'Hello world from SAS!', function(error, result, response){
  if(!error){
    //message added
  }
});
```

<span data-ttu-id="2c3f0-185">SAS가 추가 액세스만으로 생성되었기 때문에 메시지를 읽거나 업데이트, 삭제하려고 하면 오류가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-185">Since the SAS was generated with add access, if an attempt were made to read, update or delete messages, an error would be returned.</span></span>

### <a name="access-control-lists"></a><span data-ttu-id="2c3f0-186">액세스 제어 목록</span><span class="sxs-lookup"><span data-stu-id="2c3f0-186">Access control lists</span></span>
<span data-ttu-id="2c3f0-187">ACL(액세스 제어 목록)을 사용하여 SAS에 액세스 정책을 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-187">You can also use an Access Control List (ACL) to set the access policy for a SAS.</span></span> <span data-ttu-id="2c3f0-188">이 방법은 여러 클라이언트에서 큐에 액세스하게 하면서 각 클라이언트에 서로 다른 액세스 정책을 제공하려는 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-188">This is useful if you wish to allow multiple clients to access the queue, but provide different access policies for each client.</span></span>

<span data-ttu-id="2c3f0-189">ACL은 각 정책에 ID가 연결된 액세스 정책 배열을 사용하여 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-189">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span></span> <span data-ttu-id="2c3f0-190">다음 예에서는 'user1'과 'user2'에 대해 하나씩, 두 개의 정책을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-190">The  following example defines two policies; one for 'user1' and one for 'user2':</span></span>

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

<span data-ttu-id="2c3f0-191">다음 예에서는 **myqueue**에 대한 현재 ACL을 가져온 다음 **setQueueAcl**을 사용하여 새 정책을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-191">The following example gets the current ACL for **myqueue**, then adds the new policies using **setQueueAcl**.</span></span> <span data-ttu-id="2c3f0-192">이 접근 방식을 통해 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-192">This approach allows:</span></span>

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

<span data-ttu-id="2c3f0-193">ACL이 설정되고 나면 정책의 ID를 기반으로 SAS를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-193">Once the ACL has been set, you can then create a SAS based on the ID for a policy.</span></span> <span data-ttu-id="2c3f0-194">다음 예에서는 'user2'에 대해 새 SAS를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-194">The following example creates a new SAS for 'user2':</span></span>

```
queueSAS = queueSvc.generateSharedAccessSignature('myqueue', { Id: 'user2' });
```

## <a name="next-steps"></a><span data-ttu-id="2c3f0-195">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2c3f0-195">Next Steps</span></span>
<span data-ttu-id="2c3f0-196">이제 큐 저장소의 기본 사항을 배웠으므로 다음 링크를 따라 좀 더 복잡한 저장소 작업에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-196">Now that you've learned the basics of queue storage, follow these links to learn about more complex storage tasks.</span></span>

* <span data-ttu-id="2c3f0-197">[Azure Storage 팀 블로그][Azure Storage Team Blog](영문)를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-197">Visit the [Azure Storage Team Blog][Azure Storage Team Blog].</span></span>
* <span data-ttu-id="2c3f0-198">GitHub에서 [Azure Storage SDK for Node][Azure Storage SDK for Node] 리포지토리를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="2c3f0-198">Visit the [Azure Storage SDK for Node][Azure Storage SDK for Node] repository on GitHub.</span></span>

[Azure Storage SDK for Node]: https://github.com/Azure/azure-storage-node
[using the REST API]: http://msdn.microsoft.com/library/azure/hh264518.aspx
[Azure Portal]: https://portal.azure.com
<span data-ttu-id="2c3f0-199">[Azure App Service에서 Node.js 웹앱 만들기]: ../app-service-web/app-service-web-get-started-nodejs.md</span><span class="sxs-lookup"><span data-stu-id="2c3f0-199">[Create a Node.js web app in Azure App Service]: ../app-service-web/app-service-web-get-started-nodejs.md</span></span>
<span data-ttu-id="2c3f0-200">[Azure Table Service를 사용하는 Node.js 웹앱]: ../app-service-web/storage-nodejs-use-table-storage-web-site.md</span><span class="sxs-lookup"><span data-stu-id="2c3f0-200">[Node.js web app using the Azure Table Service]: ../app-service-web/storage-nodejs-use-table-storage-web-site.md</span></span>


<span data-ttu-id="2c3f0-201">[Azure Cloud Service에 Node.js 응용 프로그램 빌드 및 배포]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md</span><span class="sxs-lookup"><span data-stu-id="2c3f0-201">[Build and deploy a Node.js application to an Azure Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md</span></span>
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
<span data-ttu-id="2c3f0-202">[Web Matrix를 사용하여 Azure에 Node.js 웹앱 빌드 및 배포]: ../app-service-web/web-sites-nodejs-use-webmatrix.md</span><span class="sxs-lookup"><span data-stu-id="2c3f0-202">[Build and deploy a Node.js web app to Azure using Web Matrix]: ../app-service-web/web-sites-nodejs-use-webmatrix.md</span></span>

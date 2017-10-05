---
title: "Node.js에서 Service Bus 큐를 사용하는 방법 | Microsoft Docs"
description: "Node.js app에서 Azure의 서비스 버스 큐를 사용하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: fe2c02534996d99c190593a419a4823888f03d31
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-service-bus-queues-with-nodejs"></a><span data-ttu-id="36bfe-103">Node.js에서 Service Bus 큐를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="36bfe-103">How to use Service Bus queues with Node.js</span></span>

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="36bfe-104">이 문서에서는 Node.js에서 Service Bus 큐를 사용하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="36bfe-104">This article describes how to use Service Bus queues with Node.js.</span></span> <span data-ttu-id="36bfe-105">샘플은 JavaScript로 작성되었으며 Node.js Azure 모듈을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="36bfe-105">The samples are written in JavaScript and use the Node.js Azure module.</span></span> <span data-ttu-id="36bfe-106">여기서 다루는 시나리오에는 **큐 만들기**, **메시지 보내기 및 받기**, **큐 삭제** 등이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="36bfe-106">The scenarios covered include **creating queues**, **sending and receiving messages**, and **deleting queues**.</span></span> <span data-ttu-id="36bfe-107">큐에 대한 자세한 내용은 [다음 단계](#next-steps) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="36bfe-107">For more information on queues, see the [Next steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="36bfe-108">Node.js 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="36bfe-108">Create a Node.js application</span></span>
<span data-ttu-id="36bfe-109">빈 Node.js 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="36bfe-109">Create a blank Node.js application.</span></span> <span data-ttu-id="36bfe-110">Node.js 응용 프로그램을 만드는 방법에 대한 지침은 [Node.js 응용 프로그램을 만들어 Azure 웹 사이트에 배포][Create and deploy a Node.js application to an Azure Website] 또는 Windows PowerShell을 사용하는 [Node.js 클라우드 서비스][Node.js Cloud Service]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="36bfe-110">For instructions on how to create a Node.js application, see [Create and deploy a Node.js application to an Azure Website][Create and deploy a Node.js application to an Azure Website], or [Node.js Cloud Service][Node.js Cloud Service] using Windows PowerShell.</span></span>

## <a name="configure-your-application-to-use-service-bus"></a><span data-ttu-id="36bfe-111">서비스 버스를 사용하도록 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="36bfe-111">Configure your application to use Service Bus</span></span>
<span data-ttu-id="36bfe-112">Azure 서비스 버스를 사용하려면 Node.js Azure 패키지를 다운로드하여 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="36bfe-112">To use Azure Service Bus, download and use the Node.js Azure package.</span></span> <span data-ttu-id="36bfe-113">이 패키지에는 서비스 버스 REST 서비스와 통신하는 라이브러리 집합이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36bfe-113">This package includes a set of libraries that communicate with the Service Bus REST services.</span></span>

### <a name="use-node-package-manager-npm-to-obtain-the-package"></a><span data-ttu-id="36bfe-114">NPM(Node Package Manager)을 사용하여 패키지 가져오기</span><span class="sxs-lookup"><span data-stu-id="36bfe-114">Use Node Package Manager (NPM) to obtain the package</span></span>
1. <span data-ttu-id="36bfe-115">**Windows PowerShell for Node.js** 명령 창을 사용하여 응용 프로그램 예제를 만든 **c:\\node\\sbqueues\\WebRole1** 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="36bfe-115">Use the **Windows PowerShell for Node.js** command window to navigate to the **c:\\node\\sbqueues\\WebRole1** folder in which you created your sample application.</span></span>
2. <span data-ttu-id="36bfe-116">명령 창에 **npm install azure**를 입력합니다. 그러면 다음과 같이 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="36bfe-116">Type **npm install azure** in the command window, which should result in output similar to the following:</span></span>

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
3. <span data-ttu-id="36bfe-117">**ls** 명령을 수동으로 실행하여 **node_modules** 폴더가 만들어졌는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36bfe-117">You can manually run the **ls** command to verify that a **node_modules** folder was created.</span></span> <span data-ttu-id="36bfe-118">이 폴더에서 Service Bus 큐에 액세스하는 데 필요한 라이브러리가 포함된 **azure** 패키지를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="36bfe-118">Inside that folder find the **azure** package, which contains the libraries you need to access Service Bus queues.</span></span>

### <a name="import-the-module"></a><span data-ttu-id="36bfe-119">모듈 가져오기</span><span class="sxs-lookup"><span data-stu-id="36bfe-119">Import the module</span></span>
<span data-ttu-id="36bfe-120">메모장 또는 다른 텍스트 편집기를 사용하여 다음을 응용 프로그램의 **server.js** 파일 맨 위에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="36bfe-120">Using Notepad or another text editor, add the following to the top of the **server.js** file of the application:</span></span>

```javascript
var azure = require('azure');
```

### <a name="set-up-an-azure-service-bus-connection"></a><span data-ttu-id="36bfe-121">Azure 서비스 버스 연결 설정</span><span class="sxs-lookup"><span data-stu-id="36bfe-121">Set up an Azure Service Bus connection</span></span>
<span data-ttu-id="36bfe-122">Azure 모듈은 `AZURE_SERVICEBUS_CONNECTION_STRING` 환경 변수를 읽어 Service Bus에 연결하는 데 필요한 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="36bfe-122">The Azure module reads the environment variable `AZURE_SERVICEBUS_CONNECTION_STRING` to obtain information required to connect to Service Bus.</span></span> <span data-ttu-id="36bfe-123">이러한 환경 변수가 설정되어 있지 않은 경우 `createServiceBusService`를 호출할 때 계정 정보를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="36bfe-123">If this environment variable is not set, you must specify the account information when calling `createServiceBusService`.</span></span>

<span data-ttu-id="36bfe-124">Azure 클라우드 서비스의 구성 파일에서 환경 변수를 설정하는 방법에 대한 예제는 [저장소를 포함한 Node.js 클라우드 서비스][Node.js Cloud Service with Storage]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="36bfe-124">For an example of setting the environment variables in a configuration file for an Azure Cloud Service, see [Node.js Cloud Service with Storage][Node.js Cloud Service with Storage].</span></span>

<span data-ttu-id="36bfe-125">Azure 웹 사이트의 [Azure Portal][Azure portal]에서 환경 변수를 설정하는 방법에 대한 예제는 [저장소를 포함한 Node.js 웹 응용 프로그램][Node.js Web Application with Storage]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="36bfe-125">For an example of setting the environment variables in the [Azure portal][Azure portal] for an Azure Website, see [Node.js Web Application with Storage][Node.js Web Application with Storage].</span></span>

## <a name="create-a-queue"></a><span data-ttu-id="36bfe-126">큐 만들기</span><span class="sxs-lookup"><span data-stu-id="36bfe-126">Create a queue</span></span>
<span data-ttu-id="36bfe-127">**ServiceBusService** 개체를 사용하면 Service Bus 큐로 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36bfe-127">The **ServiceBusService** object enables you to work with Service Bus queues.</span></span> <span data-ttu-id="36bfe-128">다음 코드는 **ServiceBusService** 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="36bfe-128">The following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="36bfe-129">이 코드를 **server.js** 파일의 위쪽, Azure 모듈을 가져오기 위한 문 뒤에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="36bfe-129">Add it near the top of the **server.js** file, after the statement to import the Azure module:</span></span>

```javascript
var serviceBusService = azure.createServiceBusService();
```

<span data-ttu-id="36bfe-130">**ServiceBusService** 개체의 `createQueueIfNotExists`를 호출하면 지정한 큐가 반환되거나(있는 경우) 지정한 이름의 새 큐가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="36bfe-130">By calling `createQueueIfNotExists` on the **ServiceBusService** object, the specified queue is returned (if it exists), or a new queue with the specified name is created.</span></span> <span data-ttu-id="36bfe-131">다음 코드는 `createQueueIfNotExists`를 사용하여 `myqueue`이라는 큐를 만들거나 이 큐에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="36bfe-131">The following code uses `createQueueIfNotExists` to create or connect to the queue named `myqueue`:</span></span>

```javascript
serviceBusService.createQueueIfNotExists('myqueue', function(error){
    if(!error){
        // Queue exists
    }
});
```

<span data-ttu-id="36bfe-132">`createServiceBusService`는 추가 옵션도 지원합니다. 이러한 옵션을 통해 메시지 TTL(Time to Live)이나 최대 큐 크기 등 기본 큐 설정을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36bfe-132">The `createServiceBusService` method also supports additional options, which enable you to override default queue settings such as message time to live or maximum queue size.</span></span> <span data-ttu-id="36bfe-133">다음은 최대 큐 크기를 5GB,TTL(Time to Live)을 1분으로 설정하는 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="36bfe-133">The following example sets the maximum queue size to 5 GB, and a time to live (TTL) value of 1 minute:</span></span>

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

### <a name="filters"></a><span data-ttu-id="36bfe-134">필터</span><span class="sxs-lookup"><span data-stu-id="36bfe-134">Filters</span></span>
<span data-ttu-id="36bfe-135">**ServiceBusService**를 사용하여 수행되는 작업에 선택적 필터링 작업을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36bfe-135">Optional filtering operations can be applied to operations performed using **ServiceBusService**.</span></span> <span data-ttu-id="36bfe-136">필터링 작업은 로깅, 자동 재시도 등을 포함할 수 있습니다. 필터는 시그니쳐가 있는 메서드를 구현하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="36bfe-136">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with the signature:</span></span>

```javascript
function handle (requestOptions, next)
```

<span data-ttu-id="36bfe-137">요청 옵션에 대한 전처리를 수행한 후 메서드는 다음 서명을 사용하여 콜백을 전달하는 `next`를 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="36bfe-137">After doing its pre-processing on the request options, the method must call `next`, passing a callback with the following signature:</span></span>

```javascript
function (returnObject, finalCallback, next)
```

<span data-ttu-id="36bfe-138">이 콜백에서 `returnObject`(서버에 요청 응답 반환)를 처리한 후 콜백은 `next`(있는 경우)를 호출하여 다른 필터를 계속 처리하거나 `finalCallback`을 호출하여 서비스 호출을 종료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="36bfe-138">In this callback, and after processing the `returnObject` (the response from the request to the server), the callback must either invoke `next` if it exists to continue processing other filters, or simply invoke `finalCallback`, which ends the service invocation.</span></span>

<span data-ttu-id="36bfe-139">재시도 논리를 구현하는 두 개의 필터는 Node.js용 Azure SDK, `ExponentialRetryPolicyFilter` 및 `LinearRetryPolicyFilter`를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="36bfe-139">Two filters that implement retry logic are included with the Azure SDK for Node.js, `ExponentialRetryPolicyFilter` and `LinearRetryPolicyFilter`.</span></span> <span data-ttu-id="36bfe-140">다음 코드는 `ExponentialRetryPolicyFilter`를 사용하는 `ServiceBusService` 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="36bfe-140">The following code creates a `ServiceBusService` object that uses the `ExponentialRetryPolicyFilter`:</span></span>

```javascript
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var serviceBusService = azure.createServiceBusService().withFilter(retryOperations);
```

## <a name="send-messages-to-a-queue"></a><span data-ttu-id="36bfe-141">큐에 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="36bfe-141">Send messages to a queue</span></span>
<span data-ttu-id="36bfe-142">Service Bus 큐에 메시지를 보내기 위해 응용 프로그램은 **ServiceBusService** 개체에 대해 `sendQueueMessage` 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="36bfe-142">To send a message to a Service Bus queue, your application calls the `sendQueueMessage` method on the **ServiceBusService** object.</span></span> <span data-ttu-id="36bfe-143">Service Bus 큐로 보내고 받는 메시지는 **BrokeredMessage** 개체이며 표준 속성 집합(예: **Label** 및 **TimeToLive**), 응용 프로그램별 사용자 지정 속성을 저장하는 데 사용되는 사전 및 임의 응용 프로그램 데이터 본문이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36bfe-143">Messages sent to (and received from) Service Bus queues are **BrokeredMessage** objects, and have a set of standard properties (such as **Label** and **TimeToLive**), a dictionary that is used to hold custom application-specific properties, and a body of arbitrary application data.</span></span> <span data-ttu-id="36bfe-144">응용 프로그램은 문자열을 메시지로 전달하여 메시지 본문을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36bfe-144">An application can set the body of the message by passing a string as the message.</span></span> <span data-ttu-id="36bfe-145">필수 표준 속성이 기본값으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="36bfe-145">Any required standard properties are populated with default values.</span></span>

<span data-ttu-id="36bfe-146">다음 예제에서는 `sendQueueMessage`를 사용하여 `myqueue`라는 큐에 테스트 메시지를 보내는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="36bfe-146">The following example demonstrates how to send a test message to the queue named `myqueue` using `sendQueueMessage`:</span></span>

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

<span data-ttu-id="36bfe-147">Service Bus 큐는 [표준 계층](service-bus-premium-messaging.md)에서 256KB의 최대 메시지 크기를 [프리미엄 계층](service-bus-premium-messaging.md)에서 1MB를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="36bfe-147">Service Bus queues support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="36bfe-148">표준 및 사용자 지정 응용 프로그램 속성이 포함된 헤더의 최대 크기는 64KB입니다.</span><span class="sxs-lookup"><span data-stu-id="36bfe-148">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="36bfe-149">한 큐에 저장되는 메시지 수에는 제한이 없지만 한 큐에 저장되는 총 메시지 크기는 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="36bfe-149">There is no limit on the number of messages held in a queue but there is a cap on the total size of the messages held by a queue.</span></span> <span data-ttu-id="36bfe-150">이 큐 크기는 생성 시 정의되며 상한이 5GB입니다.</span><span class="sxs-lookup"><span data-stu-id="36bfe-150">This queue size is defined at creation time, with an upper limit of 5 GB.</span></span> <span data-ttu-id="36bfe-151">할당량에 대한 자세한 내용은 [Service Bus 할당량][Service Bus quotas]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="36bfe-151">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="36bfe-152">큐에서 메시지 받기</span><span class="sxs-lookup"><span data-stu-id="36bfe-152">Receive messages from a queue</span></span>
<span data-ttu-id="36bfe-153">**ServiceBusService** 개체의 `receiveQueueMessage` 메서드를 사용하여 큐에서 메시지를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="36bfe-153">Messages are received from a queue using the `receiveQueueMessage` method on the **ServiceBusService** object.</span></span> <span data-ttu-id="36bfe-154">기본적으로 읽은 메시지는 큐에서 삭제됩니다. 그러나 선택적 매개 변수 `isPeekLock`을 **true**로 설정하여 큐에서 삭제되지 않도록 메시지를 읽은(최대) 후 잠글 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36bfe-154">By default, messages are deleted from the queue as they are read; however, you can read (peek) and lock the message without deleting it from the queue by setting the optional parameter `isPeekLock` to **true**.</span></span>

<span data-ttu-id="36bfe-155">받기 작업의 일부로 메시지를 읽고 삭제하는 기본 동작은 가장 단순한 모델이며, 실패할 경우 응용 프로그램이 메시지를 처리하지 않아도 되는 시나리오에서 가장 효과적입니다.</span><span class="sxs-lookup"><span data-stu-id="36bfe-155">The default behavior of reading and deleting the message as part of the receive operation is the simplest model, and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="36bfe-156">이해를 돕기 위해 소비자가 수신 요청을 실행한 후 처리하기 전에 크래시되는 시나리오를 고려해 보세요.</span><span class="sxs-lookup"><span data-stu-id="36bfe-156">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="36bfe-157">서비스 버스는 메시지를 이용되는 것으로 표시하기 때문에 응용 프로그램이 다시 시작되고 메시지 소비를 다시 시작할 경우 크래시 전에 소비된 메시지가 누락됩니다.</span><span class="sxs-lookup"><span data-stu-id="36bfe-157">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="36bfe-158">`isPeekLock` 매개 변수를 **true**로 설정하면 수신은 2단계 작업이 되므로, 메시지 누락을 허용하지 않는 응용 프로그램을 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36bfe-158">If the `isPeekLock` parameter is set to **true**, the receive becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="36bfe-159">서비스 버스는 요청을 받으면 소비할 다음 메시지를 찾아서 다른 소비자가 수신할 수 없도록 잠근 후 응용 프로그램에 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="36bfe-159">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span> <span data-ttu-id="36bfe-160">응용 프로그램은 메시지 처리를 완료하거나 추가 처리를 위해 안전하게 저장한 후, `deleteMessage` 메서드를 호출하고 삭제될 메시지를 매개 변수로 제공하여 수신 프로세스의 두 번째 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="36bfe-160">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling `deleteMessage` method and providing the message to be deleted as a parameter.</span></span> <span data-ttu-id="36bfe-161">`deleteMessage` 메서드는 메시지를 사용 중인 것으로 표시하고 큐에서 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="36bfe-161">The `deleteMessage` method marks the message as being consumed and removes it from the queue.</span></span>

<span data-ttu-id="36bfe-162">다음 예제에서는 `receiveQueueMessage`를 사용하여 메시지를 받고 처리하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="36bfe-162">The following example demonstrates how to receive and process messages using `receiveQueueMessage`.</span></span> <span data-ttu-id="36bfe-163">먼저 메시지를 받고 삭제한 다음 **true**로 설정된 `isPeekLock`을 사용하여 메시지를 받고 `deleteMessage`를 사용하여 메시지를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="36bfe-163">The example first receives and deletes a message, and then receives a message using `isPeekLock` set to **true**, then deletes the message using `deleteMessage`:</span></span>

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

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="36bfe-164">응용 프로그램 작동 중단 및 읽을 수 없는 메시지를 처리하는 방법</span><span class="sxs-lookup"><span data-stu-id="36bfe-164">How to handle application crashes and unreadable messages</span></span>
<span data-ttu-id="36bfe-165">서비스 버스는 응용 프로그램 오류나 메시지 처리 문제를 정상적으로 복구하는 데 유용한 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="36bfe-165">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="36bfe-166">어떤 이유로든 수신 응용 프로그램이 메시지를 처리할 수 없는 경우 **ServiceBusService** 개체의 `unlockMessage` 메서드를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36bfe-166">If a receiver application is unable to process the message for some reason, then it can call the `unlockMessage` method on the **ServiceBusService** object.</span></span> <span data-ttu-id="36bfe-167">그러면 서비스 버스에서 큐 메시지의 잠금을 해제하므로 동일한 소비 응용 프로그램이나 다른 소비 응용 프로그램에서 메시지를 다시 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36bfe-167">This will cause Service Bus to unlock the message within the queue and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="36bfe-168">큐 내에서 잠긴 메시지와 연결된 시간 제한도 있으며, 응용 프로그램에서 잠금 시간 제한이 만료되기 전에 메시지를 처리하지 못하는 경우(예: 응용 프로그램이 크래시되는 경우) 서비스 버스가 메시지를 자동으로 잠금 해제하여 다시 받을 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="36bfe-168">There is also a timeout associated with a message locked within the queue, and if the application fails to process the message before the lock timeout expires (e.g., if the application crashes), then Service Bus will unlock the message automatically and make it available to be received again.</span></span>

<span data-ttu-id="36bfe-169">응용 프로그램이 메시지를 처리한 후 `deleteMessage` 메서드가 호출되기 전에 충돌하는 경우, 다시 시작될 때 메시지가 응용 프로그램에 다시 배달됩니다.</span><span class="sxs-lookup"><span data-stu-id="36bfe-169">In the event that the application crashes after processing the message but before the `deleteMessage` method is called, then the message will be redelivered to the application when it restarts.</span></span> <span data-ttu-id="36bfe-170">이를 *최소 한 번 이상 처리*라고 합니다. 즉, 각 메시지가 최소 한 번 이상 처리되지만 특정 상황에서는 동일한 메시지가 다시 배달될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36bfe-170">This is often called *At Least Once Processing*, that is, each message will be processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="36bfe-171">중복 처리가 허용되지 않는 시나리오에서는 응용 프로그램 개발자가 중복 메시지 배달을 처리하는 논리를 응용 프로그램에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="36bfe-171">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span></span> <span data-ttu-id="36bfe-172">이 경우 대체로 배달 시도 간에 일정하게 유지되는 메시지의 **MessageId** 속성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="36bfe-172">This is often achieved using the **MessageId** property of the message, which will remain constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="36bfe-173">다음 단계</span><span class="sxs-lookup"><span data-stu-id="36bfe-173">Next steps</span></span>
<span data-ttu-id="36bfe-174">큐에 대한 자세한 내용은 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="36bfe-174">To learn more about queues, see the following resources.</span></span>

* <span data-ttu-id="36bfe-175">[큐, 토픽 및 구독][Queues, topics, and subscriptions]</span><span class="sxs-lookup"><span data-stu-id="36bfe-175">[Queues, topics, and subscriptions][Queues, topics, and subscriptions]</span></span>
* <span data-ttu-id="36bfe-176">GitHub의 [Node용 Azure SDK][Azure SDK for Node] 리포지토리</span><span class="sxs-lookup"><span data-stu-id="36bfe-176">[Azure SDK for Node][Azure SDK for Node] repository on GitHub</span></span>
* [<span data-ttu-id="36bfe-177">Node.js 개발자 센터</span><span class="sxs-lookup"><span data-stu-id="36bfe-177">Node.js Developer Center</span></span>](https://azure.microsoft.com/develop/nodejs/)

[Azure SDK for Node]: https://github.com/Azure/azure-sdk-for-node
[Azure portal]: https://portal.azure.com

[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[Create and deploy a Node.js application to an Azure Website]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js Cloud Service with Storage]:../cosmos-db/table-storage-cloud-service-nodejs.md
[Node.js Web Application with Storage]:../cosmos-db/table-storage-how-to-use-nodejs.md
[Service Bus quotas]: service-bus-quotas.md

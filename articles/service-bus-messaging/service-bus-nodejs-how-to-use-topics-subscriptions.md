---
title: "Node.js에서 Azure Service Bus 토픽 및 구독을 사용하는 방법 | Microsoft Docs"
description: "Node.js app에서 Azure의 Service Bus 토픽 및 구독을 사용하는 방법에 대해 알아봅니다."
services: service-bus-messaging
documentationcenter: nodejs
author: sethmanheim
manager: timlt
editor: 
ms.assetid: b9f5db85-7b6c-4cc7-bd2c-bd3087c99875
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 24ae9b80f75531c5e4a84c3b4a6666a6f8a83d2c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-service-bus-topics-and-subscriptions-with-nodejs"></a><span data-ttu-id="f930b-103">Node.js에서 Service Bus 토픽 및 구독을 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="f930b-103">How to Use Service Bus topics and subscriptions with Node.js</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="f930b-104">이 가이드에서는 Node.js 응용 프로그램에서 Service Bus 토픽과 구독을 사용하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-104">This guide describes how to use Service Bus topics and subscriptions from Node.js applications.</span></span> <span data-ttu-id="f930b-105">여기서 다루는 시나리오에는 **토픽 및 구독 만들기**, **구독 필터 만들기**, **토픽에 메시지 보내기**, **구독에서 메시지 받기**, **토픽 및 구독 삭제** 등이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-105">The scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages** to a topic, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span> <span data-ttu-id="f930b-106">토픽 및 구독에 대한 자세한 내용은 [다음 단계](#next-steps) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f930b-106">For more information about topics and subscriptions, see the [Next steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="f930b-107">Node.js 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="f930b-107">Create a Node.js application</span></span>
<span data-ttu-id="f930b-108">빈 Node.js 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-108">Create a blank Node.js application.</span></span> <span data-ttu-id="f930b-109">Node.js 응용 프로그램을 만드는 방법에 대한 지침은 [Node.js 응용 프로그램을 만들어 Azure 웹 사이트에 배포], Windows PowerShell을 사용하는 [Node.js 클라우드 서비스][Node.js Cloud Service] 또는 WebMatrix를 사용하는 웹 사이트를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f930b-109">For instructions on creating a Node.js application, see [Create and deploy a Node.js application to an Azure Web Site], [Node.js Cloud Service][Node.js Cloud Service] using Windows PowerShell, or Web Site with WebMatrix.</span></span>

## <a name="configure-your-application-to-use-service-bus"></a><span data-ttu-id="f930b-110">서비스 버스를 사용하도록 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="f930b-110">Configure your application to use Service Bus</span></span>
<span data-ttu-id="f930b-111">서비스 버스를 사용하려면 Node.js Azure 패키지를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-111">To use Service Bus, download the Node.js Azure package.</span></span> <span data-ttu-id="f930b-112">이 패키지에는 서비스 버스 REST 서비스와 통신하는 라이브러리 집합이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-112">This package includes a set of libraries that communicate with the Service Bus REST services.</span></span>

### <a name="use-node-package-manager-npm-to-obtain-the-package"></a><span data-ttu-id="f930b-113">NPM(Node Package Manager)을 사용하여 패키지 가져오기</span><span class="sxs-lookup"><span data-stu-id="f930b-113">Use Node Package Manager (NPM) to obtain the package</span></span>
1. <span data-ttu-id="f930b-114">**PowerShell**(Windows), **Terminal**(Mac) 또는 **Bash** (Unix)과 같은 명령줄 인터페이스를 사용하여 샘플 응용 프로그램을 만든 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-114">Use a command-line interface such as **PowerShell** (Windows,) **Terminal** (Mac,) or **Bash** (Unix), navigate to the folder where you created your sample application.</span></span>
2. <span data-ttu-id="f930b-115">명령 창에 **npm install azure**를 입력합니다. 그러면 다음과 같이 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-115">Type **npm install azure** in the command window, which should result in the following output:</span></span>

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
3. <span data-ttu-id="f930b-116">**ls** 명령을 수동으로 실행하여 **node\_modules** 폴더가 만들어졌는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-116">You can manually run the **ls** command to verify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="f930b-117">이 폴더에서 Service Bus 토픽에 액세스하는 데 필요한 라이브러리가 들어 있는 **Azure** 패키지를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-117">Inside that folder find the **azure** package, which contains the libraries you need to access Service Bus topics.</span></span>

### <a name="import-the-module"></a><span data-ttu-id="f930b-118">모듈 가져오기</span><span class="sxs-lookup"><span data-stu-id="f930b-118">Import the module</span></span>
<span data-ttu-id="f930b-119">메모장 또는 다른 텍스트 편집기를 사용하여 다음을 응용 프로그램의 **server.js** 파일 맨 위에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-119">Using Notepad or another text editor, add the following to the top of the **server.js** file of the application:</span></span>

```javascript
var azure = require('azure');
```

### <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="f930b-120">서비스 버스 연결 설정</span><span class="sxs-lookup"><span data-stu-id="f930b-120">Set up a Service Bus connection</span></span>
<span data-ttu-id="f930b-121">Azure 모듈은 `AZURE_SERVICEBUS_NAMESPACE` 및 `AZURE_SERVICEBUS_ACCESS_KEY` 환경 변수를 읽어 Service Bus에 연결하는 데 필요한 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-121">The Azure module reads the environment variables `AZURE_SERVICEBUS_NAMESPACE` and `AZURE_SERVICEBUS_ACCESS_KEY` for information required to connect to Service Bus.</span></span> <span data-ttu-id="f930b-122">이러한 환경 변수가 설정되어 있지 않은 경우 `createServiceBusService`를 호출할 때 계정 정보를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-122">If these environment variables are not set, you must specify the account information when calling `createServiceBusService`.</span></span>

<span data-ttu-id="f930b-123">Azure Cloud Service에 대한 환경 변수를 설정하는 방법에 대한 예제는 [저장소를 포함한 Node.js 클라우드 서비스][Node.js Cloud Service with Storage]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f930b-123">For an example of setting the environment variables for an Azure Cloud Service, see [Node.js Cloud Service with Storage][Node.js Cloud Service with Storage].</span></span>

<span data-ttu-id="f930b-124">Azure Website에 대한 환경 변수를 설정하는 방법에 대한 예제는 [저장소를 포함한 Node.js 웹 응용 프로그램][Node.js Web Application with Storage]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f930b-124">For an example of setting the environment variables for an Azure Website, see [Node.js Web Application with Storage][Node.js Web Application with Storage].</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="f930b-125">토픽 만들기</span><span class="sxs-lookup"><span data-stu-id="f930b-125">Create a topic</span></span>
<span data-ttu-id="f930b-126">**ServiceBusService** 개체를 사용하면 토픽으로 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-126">The **ServiceBusService** object enables you to work with topics.</span></span> <span data-ttu-id="f930b-127">다음 코드는 **ServiceBusService** 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-127">The following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="f930b-128">이 코드를 **server.js** 파일의 위쪽, Azure 모듈을 가져오기 위한 문 뒤에 추가하십시오.</span><span class="sxs-lookup"><span data-stu-id="f930b-128">Add it near the top of the **server.js** file, after the statement to import the azure module:</span></span>

```javascript
var serviceBusService = azure.createServiceBusService();
```

<span data-ttu-id="f930b-129">**ServiceBusService** 개체의 `createTopicIfNotExists`를 호출하면 지정한 토픽이 반환되거나(있는 경우) 지정한 이름의 새 토픽이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-129">By calling `createTopicIfNotExists` on the **ServiceBusService** object, the specified topic will be returned (if it exists,) or a new topic with the specified name will be created.</span></span> <span data-ttu-id="f930b-130">다음 코드는 `createTopicIfNotExists`를 사용하여 `MyTopic`이라는 토픽을 만들거나 이 토픽에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-130">The following code uses `createTopicIfNotExists` to create or connect to the topic named `MyTopic`:</span></span>

```javascript
serviceBusService.createTopicIfNotExists('MyTopic',function(error){
    if(!error){
        // Topic was created or exists
        console.log('topic created or exists.');
    }
});
```

<span data-ttu-id="f930b-131">`createServiceBusService` 메서드는 추가 옵션도 지원합니다. 이러한 옵션을 통해 메시지 TTL(Time to Live)이나 최대 토픽 크기 등 기본 토픽 설정을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-131">The `createServiceBusService` method also supports additional options, which enable you to override default topic settings such as message time to live or maximum topic size.</span></span> <span data-ttu-id="f930b-132">다음은 최대 토픽 크기를 5GB, TTL(Time to Live)을 1분으로 설정하는 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-132">The following example sets the maximum topic size to 5GB with a time to live of 1 minute:</span></span>

```javascript
var topicOptions = {
        MaxSizeInMegabytes: '5120',
        DefaultMessageTimeToLive: 'PT1M'
    };

serviceBusService.createTopicIfNotExists('MyTopic', topicOptions, function(error){
    if(!error){
        // topic was created or exists
    }
});
```

### <a name="filters"></a><span data-ttu-id="f930b-133">필터</span><span class="sxs-lookup"><span data-stu-id="f930b-133">Filters</span></span>
<span data-ttu-id="f930b-134">**ServiceBusService**를 사용하여 수행되는 작업에 선택적 필터링 작업을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-134">Optional filtering operations can be applied to operations performed using **ServiceBusService**.</span></span> <span data-ttu-id="f930b-135">필터링 작업은 로깅, 자동 재시도 등을 포함할 수 있습니다. 필터는 시그니쳐가 있는 메서드를 구현하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-135">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with the signature:</span></span>

```javascript
function handle (requestOptions, next)
```

<span data-ttu-id="f930b-136">요청 옵션에 대한 전처리를 수행한 후 메서드는 다음 서명을 사용하여 콜백을 전달하는 `next`를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-136">After performing preprocessing on the request options, the method calls `next`, passing a callback with the following signature:</span></span>

```javascript
function (returnObject, finalCallback, next)
```

<span data-ttu-id="f930b-137">이 콜백에서 `returnObject`(서버에 요청 응답 반환)를 처리한 후 콜백은 next(있는 경우)를 호출하여 다른 필터를 계속 처리하거나 `finalCallback`을 호출하여 서비스 호출을 종료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-137">In this callback, and after processing the `returnObject` (the response from the request to the server), the callback needs to either invoke next if it exists to continue processing other filters or invoke `finalCallback` otherwise, to end the service invocation.</span></span>

<span data-ttu-id="f930b-138">Node.js용 Azure SDK에는 재시도 논리를 구현하는 두 필터 **ExponentialRetryPolicyFilter** 및 **LinearRetryPolicyFilter**가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-138">Two filters that implement retry logic are included with the Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="f930b-139">다음은 **ExponentialRetryPolicyFilter**를 사용하는 **ServiceBusService** 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-139">The following creates a **ServiceBusService** object that uses the **ExponentialRetryPolicyFilter**:</span></span>

```javascript
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var serviceBusService = azure.createServiceBusService().withFilter(retryOperations);
```

## <a name="create-subscriptions"></a><span data-ttu-id="f930b-140">구독 만들기</span><span class="sxs-lookup"><span data-stu-id="f930b-140">Create subscriptions</span></span>
<span data-ttu-id="f930b-141">토픽 구독은 **ServiceBusService** 개체로도 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-141">Topic subscriptions are also created with the **ServiceBusService** object.</span></span> <span data-ttu-id="f930b-142">구독에는 이름이 지정되며, 구독의 가상 큐에 전달되는 메시지 집합을 제한하는 선택적 필터가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-142">Subscriptions are named and can have an optional filter that restricts the set of messages delivered to the subscription's virtual queue.</span></span>

> [!NOTE]
> <span data-ttu-id="f930b-143">구독은 영구적이며, 구독 자체 또는 구독과 연결된 토픽이 삭제될 때까지 계속 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-143">Subscriptions are persistent and will continue to exist until either they, or the topic they are associated with, are deleted.</span></span> <span data-ttu-id="f930b-144">응용 프로그램에 구독을 만들기 위한 논리가 포함된 경우, `getSubscription` 메서드를 사용하여 구독이 이미 존재하는지를 먼저 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-144">If your application contains logic to create a subscription, it should first check if the subscription already exists by using the `getSubscription` method.</span></span>
>
>

### <a name="create-a-subscription-with-the-default-matchall-filter"></a><span data-ttu-id="f930b-145">기본(MatchAll) 필터를 사용하여 구독 만들기</span><span class="sxs-lookup"><span data-stu-id="f930b-145">Create a subscription with the default (MatchAll) filter</span></span>
<span data-ttu-id="f930b-146">**MatchAll** 필터는 새 구독을 만들 때 필터를 지정하지 않은 경우 사용되는 기본 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-146">The **MatchAll** filter is the default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="f930b-147">**MatchAll** 필터를 사용하면 토픽에 게시된 모든 메시지가 구독의 가상 큐에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-147">When the **MatchAll** filter is used, all messages published to the topic are placed in the subscription's virtual queue.</span></span> <span data-ttu-id="f930b-148">다음 예제에서는 'AllMessages'라는 구독을 만들고 기본 **MatchAll** 필터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-148">The following example creates a subscription named 'AllMessages' and uses the default **MatchAll** filter.</span></span>

```javascript
serviceBusService.createSubscription('MyTopic','AllMessages',function(error){
    if(!error){
        // subscription created
    }
});
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="f930b-149">필터를 사용하여 구독 만들기</span><span class="sxs-lookup"><span data-stu-id="f930b-149">Create subscriptions with filters</span></span>
<span data-ttu-id="f930b-150">토픽으로 전송된 메시지 중 특정 토픽 구독 내에 표시되어야 하는 메시지의 범위를 지정하는 필터를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-150">You can also create filters that allow you to scope which messages sent to a topic should show up within a specific topic subscription.</span></span>

<span data-ttu-id="f930b-151">구독에서 지원하는 가장 유연한 유형의 필터는 SQL92 하위 집합을 구현하는 **SqlFilter**입니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-151">The most flexible type of filter supported by subscriptions is the **SqlFilter**, which implements a subset of SQL92.</span></span> <span data-ttu-id="f930b-152">SQL 필터는 토픽에 게시된 메시지의 속성에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-152">SQL filters operate on the properties of the messages that are published to the topic.</span></span> <span data-ttu-id="f930b-153">SQL 필터와 함께 사용할 수 있는 식에 대한 자세한 내용은 [SqlFilter.SqlExpression][SqlFilter.SqlExpression] 구문을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f930b-153">For more details about the expressions that can be used with a SQL filter, review the [SqlFilter.SqlExpression][SqlFilter.SqlExpression] syntax.</span></span>

<span data-ttu-id="f930b-154">**ServiceBusService** 개체의 `createRule` 메서드를 사용하여 구독에 필터를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-154">Filters can be added to a subscription by using the `createRule` method of the **ServiceBusService** object.</span></span> <span data-ttu-id="f930b-155">이 메서드를 사용하면 기존 구독에 새 필터를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-155">This method allows you to add new filters to an existing subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="f930b-156">기본 필터는 모든 새로운 구독에 자동으로 적용되므로 먼저 기본 필터를 제거해야 합니다. 그렇지 않으면 **MatchAll**이 사용자가 지정하는 기타 필터를 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-156">Because the default filter is applied automatically to all new subscriptions, you must first remove the default filter or the **MatchAll** will override any other filters you may specify.</span></span> <span data-ttu-id="f930b-157">**ServiceBusService** 개체의 `deleteRule` 메서드를 사용하여 기본 규칙을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-157">You can remove the default rule by using the `deleteRule` method of the **ServiceBusService** object.</span></span>
>
>

<span data-ttu-id="f930b-158">다음 예제에서는 사용자 지정 `messagenumber` 속성이 3보다 큰 메시지만 선택하는 **SqlFilter**를 사용하여 이름이 `HighMessages`인 구독을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-158">The following example creates a subscription named `HighMessages` with a **SqlFilter** that only selects messages that have a custom `messagenumber` property greater than 3:</span></span>

```javascript
serviceBusService.createSubscription('MyTopic', 'HighMessages', function (error){
    if(!error){
        // subscription created
        rule.create();
    }
});
var rule={
    deleteDefault: function(){
        serviceBusService.deleteRule('MyTopic',
            'HighMessages',
            azure.Constants.ServiceBusConstants.DEFAULT_RULE_NAME,
            rule.handleError);
    },
    create: function(){
        var ruleOptions = {
            sqlExpressionFilter: 'messagenumber > 3'
        };
        rule.deleteDefault();
        serviceBusService.createRule('MyTopic',
            'HighMessages',
            'HighMessageFilter',
            ruleOptions,
            rule.handleError);
    },
    handleError: function(error){
        if(error){
            console.log(error)
        }
    }
}
```

<span data-ttu-id="f930b-159">마찬가지로, 다음 예제에서는 `messagenumber` 속성이 3 이하인 메시지만 선택하는 **SqlFilter**가 있는 이름이 `LowMessages`인 구독을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-159">Similarly, the following example creates a subscription named `LowMessages` with a **SqlFilter** that only selects messages that have a `messagenumber` property less than or equal to 3:</span></span>

```javascript
serviceBusService.createSubscription('MyTopic', 'LowMessages', function (error){
    if(!error){
        // subscription created
        rule.create();
    }
});
var rule={
    deleteDefault: function(){
        serviceBusService.deleteRule('MyTopic',
            'LowMessages',
            azure.Constants.ServiceBusConstants.DEFAULT_RULE_NAME,
            rule.handleError);
    },
    create: function(){
        var ruleOptions = {
            sqlExpressionFilter: 'messagenumber <= 3'
        };
        rule.deleteDefault();
        serviceBusService.createRule('MyTopic',
            'LowMessages',
            'LowMessageFilter',
            ruleOptions,
            rule.handleError);
    },
    handleError: function(error){
        if(error){
            console.log(error)
        }
    }
}
```

<span data-ttu-id="f930b-160">이제 `MyTopic`으로 메시지를 보내는 경우 `AllMessages` 토픽 구독을 구독하는 수신자에게는 항상 배달되고, `HighMessages` 및 `LowMessages` 토픽 구독을 구독하는 수신자에게는 메시지 내용에 따라 선택적으로 배달됩니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-160">When a message is now sent to `MyTopic`, it will always be delivered to receivers subscribed to the `AllMessages` topic subscription, and selectively delivered to receivers subscribed to the `HighMessages` and `LowMessages` topic subscriptions (depending upon the message content).</span></span>

## <a name="how-to-send-messages-to-a-topic"></a><span data-ttu-id="f930b-161">토픽에 메시지를 보내는 방법</span><span class="sxs-lookup"><span data-stu-id="f930b-161">How to send messages to a topic</span></span>
<span data-ttu-id="f930b-162">Service Bus 토픽에 메시지를 보내려면 응용 프로그램에서 **ServiceBusService** 개체의 `sendTopicMessage` 메서드를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-162">To send a message to a Service Bus topic, your application must use the `sendTopicMessage` method of the **ServiceBusService** object.</span></span>
<span data-ttu-id="f930b-163">Service Bus 토픽으로 보내는 메시지는 **BrokeredMessage** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-163">Messages sent to Service Bus topics are **BrokeredMessage** objects.</span></span>
<span data-ttu-id="f930b-164">**BrokeredMessage** 개체에는 표준 속성 집합(예: `Label` 및 `TimeToLive`), 응용 프로그램별 사용자 지정 속성을 저장하는 데 사용되는 사전 및 문자열 데이터의 본문이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-164">**BrokeredMessage** objects have a set of standard properties (such as `Label` and `TimeToLive`), a dictionary that is used to hold custom application-specific properties, and a body of string data.</span></span> <span data-ttu-id="f930b-165">응용 프로그램은 문자열 값을 `sendTopicMessage`에 전달하여 메시지의 본문을 설정할 수 있습니다. 그러면 필수 표준 속성이 기본값으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-165">An application can set the body of the message by passing a string value to the `sendTopicMessage` and any required standard properties will be populated by default values.</span></span>

<span data-ttu-id="f930b-166">다음 예제에서는 5개의 테스트 메시지를 `MyTopic`에 보내는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-166">The following example demonstrates how to send five test messages to `MyTopic`.</span></span> <span data-ttu-id="f930b-167">루프가 반복될 때마다 각 메시지의 `messagenumber` 속성 값이 달라지는 것을 알 수 있습니다(메시지를 수신하는 구독 결정).</span><span class="sxs-lookup"><span data-stu-id="f930b-167">Note that the `messagenumber` property value of each message varies on the iteration of the loop (this will determine which subscriptions receive it):</span></span>

```javascript
var message = {
    body: '',
    customProperties: {
        messagenumber: 0
    }
}

for (i = 0;i < 5;i++) {
    message.customProperties.messagenumber=i;
    message.body='This is Message #'+i;
    serviceBusService.sendTopicMessage(topic, message, function(error) {
      if (error) {
        console.log(error);
      }
    });
}
```

<span data-ttu-id="f930b-168">Service Bus 토픽은 [표준 계층](service-bus-premium-messaging.md)에서 256KB의 최대 메시지 크기를 [프리미엄 계층](service-bus-premium-messaging.md)에서 1MB를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-168">Service Bus topics support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="f930b-169">표준 및 사용자 지정 응용 프로그램 속성이 포함된 헤더의 최대 크기는 64KB입니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-169">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="f930b-170">한 토픽에 저장되는 메시지 수에는 제한이 없지만 한 토픽에 저장되는 총 메시지 크기는 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-170">There is no limit on the number of messages held in a topic but there is a cap on the total size of the messages held by a topic.</span></span> <span data-ttu-id="f930b-171">이 토픽 크기는 생성 시 정의되며 상한이 5GB입니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-171">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="f930b-172">구독에서 메시지 받기</span><span class="sxs-lookup"><span data-stu-id="f930b-172">Receive messages from a subscription</span></span>
<span data-ttu-id="f930b-173">**ServiceBusService** 개체의 `receiveSubscriptionMessage` 메서드를 사용하여 구독에서 메시지를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-173">Messages are received from a subscription using the `receiveSubscriptionMessage` method on the **ServiceBusService** object.</span></span> <span data-ttu-id="f930b-174">기본적으로 읽은 메시지는 구독에서 삭제됩니다. 그러나 선택적 매개 변수 `isPeekLock`을 **true**로 설정하여, 구독에서 삭제되지 않도록 메시지를 읽은(최대) 후 잠글 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-174">By default, messages are deleted from the subscription as they are read; however, you can read (peek) and lock the message without deleting it from the subscription by setting the optional parameter `isPeekLock` to **true**.</span></span>

<span data-ttu-id="f930b-175">받기 작업의 일부로 메시지를 읽고 삭제하는 기본 동작은 가장 단순한 모델이며, 실패할 경우 응용 프로그램이 메시지를 처리하지 않아도 되는 시나리오에서 가장 효과적입니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-175">The default behavior of reading and deleting the message as part of the receive operation is the simplest model, and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="f930b-176">이해를 돕기 위해 소비자가 수신 요청을 실행한 후 처리하기 전에 크래시되는 시나리오를 고려해 보세요.</span><span class="sxs-lookup"><span data-stu-id="f930b-176">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="f930b-177">서비스 버스는 메시지를 이용되는 것으로 표시하기 때문에 응용 프로그램이 다시 시작되고 메시지 소비를 다시 시작할 경우 크래시 전에 소비된 메시지가 누락됩니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-177">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="f930b-178">`isPeekLock` 매개 변수를 **true**로 설정하면 수신은 2단계 작업이 되므로, 메시지 누락을 허용하지 않는 응용 프로그램을 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-178">If the `isPeekLock` parameter is set to **true**, the receive becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="f930b-179">서비스 버스는 요청을 받으면 소비할 다음 메시지를 찾아서 다른 소비자가 수신할 수 없도록 잠근 후 응용 프로그램에 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-179">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span>
<span data-ttu-id="f930b-180">응용 프로그램은 메시지 처리를 완료하거나 추가 처리를 위해 안전하게 저장한 후, **deleteMessage** 메서드를 호출하고 삭제될 메시지를 매개 변수로 제공하여 수신 프로세스의 두 번째 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-180">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling **deleteMessage** method and providing the message to be deleted as a parameter.</span></span> <span data-ttu-id="f930b-181">**deleteMessage** 메서드는 메시지를 소비 중인 것으로 표시하고 구독에서 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-181">The **deleteMessage** method will mark the message as being consumed and remove it from the subscription.</span></span>

<span data-ttu-id="f930b-182">다음 예제에서는 `receiveSubscriptionMessage`를 사용하여 메시지를 받고 처리하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-182">The following example demonstrates how messages can be received and processed using `receiveSubscriptionMessage`.</span></span> <span data-ttu-id="f930b-183">먼저 'LowMessages' 구독에서 메시지를 받고 삭제한 다음, true로 설정된 `isPeekLock`을 사용하여 'HighMessages' 구독에서 메시지를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-183">The example first receives and deletes a message from the 'LowMessages' subscription, and then receives a message from the 'HighMessages' subscription using `isPeekLock` set to true.</span></span> <span data-ttu-id="f930b-184">그런 다음 `deleteMessage`를 사용하여 메시지를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-184">It then deletes the message using `deleteMessage`:</span></span>

```javascript
serviceBusService.receiveSubscriptionMessage('MyTopic', 'LowMessages', function(error, receivedMessage){
    if(!error){
        // Message received and deleted
        console.log(receivedMessage);
    }
});
serviceBusService.receiveSubscriptionMessage('MyTopic', 'HighMessages', { isPeekLock: true }, function(error, lockedMessage){
    if(!error){
        // Message received and locked
        console.log(lockedMessage);
        serviceBusService.deleteMessage(lockedMessage, function (deleteError){
            if(!deleteError){
                // Message deleted
                console.log('message has been deleted.');
            }
        }
    }
});
```

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="f930b-185">응용 프로그램 작동 중단 및 읽을 수 없는 메시지를 처리하는 방법</span><span class="sxs-lookup"><span data-stu-id="f930b-185">How to handle application crashes and unreadable messages</span></span>
<span data-ttu-id="f930b-186">서비스 버스는 응용 프로그램 오류나 메시지 처리 문제를 정상적으로 복구하는 데 유용한 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-186">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="f930b-187">어떤 이유로든 수신 응용 프로그램이 메시지를 처리할 수 없는 경우 **ServiceBusService** 개체의 `unlockMessage` 메서드를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-187">If a receiver application is unable to process the message for some reason, then it can call the `unlockMessage` method on the **ServiceBusService** object.</span></span> <span data-ttu-id="f930b-188">그러면 Service Bus에서 구독 내 메시지의 잠금을 해제하므로 동일한 소비 응용 프로그램이나 다른 소비 응용 프로그램에서 메시지를 다시 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-188">This will cause Service Bus to unlock the message within the subscription and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="f930b-189">구독 내에서 잠긴 메시지와 연결된 제한 시간도 있으며, 응용 프로그램에서 잠금 시간 제한이 만료되기 전에 메시지를 처리하지 못하는 경우(예: 응용 프로그램이 크래시되는 경우) Service Bus가 메시지를 자동으로 잠금 해제하여 다시 받을 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-189">There is also a timeout associated with a message locked within the subscription, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus unlocks the message automatically and makes it available to be received again.</span></span>

<span data-ttu-id="f930b-190">응용 프로그램이 메시지를 처리한 후 `deleteMessage` 메서드가 호출되기 전에 충돌하는 경우, 다시 시작될 때 메시지가 응용 프로그램에 다시 배달됩니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-190">In the event that the application crashes after processing the message but before the `deleteMessage` method is called, then the message will be redelivered to the application when it restarts.</span></span> <span data-ttu-id="f930b-191">이를 *최소 한 번 이상 처리*라고 합니다. 즉, 각 메시지가 최소 한 번 이상 처리되지만 특정 상황에서는 동일한 메시지가 다시 배달될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-191">This is often called *At Least Once Processing*, that is, each message will be processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="f930b-192">중복 처리가 허용되지 않는 시나리오에서는 응용 프로그램 개발자가 중복 메시지 배달을 처리하는 논리를 응용 프로그램에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-192">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span></span> <span data-ttu-id="f930b-193">이 경우 대체로 배달 시도 간에 일정하게 유지되는 메시지의 **MessageId** 속성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-193">This is often achieved using the **MessageId** property of the message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="f930b-194">토픽 및 구독 삭제</span><span class="sxs-lookup"><span data-stu-id="f930b-194">Delete topics and subscriptions</span></span>
<span data-ttu-id="f930b-195">토픽과 구독은 영구적이므로, [Azure Portal][Azure portal] 또는 프로그래밍 방식을 통해 명시적으로 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-195">Topics and subscriptions are persistent, and must be explicitly deleted either through the [Azure portal][Azure portal] or programmatically.</span></span>
<span data-ttu-id="f930b-196">다음 예제는 `MyTopic` 토픽을 삭제하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-196">The following example demonstrates how to delete the topic named `MyTopic`:</span></span>

```javascript
serviceBusService.deleteTopic('MyTopic', function (error) {
    if (error) {
        console.log(error);
    }
});
```

<span data-ttu-id="f930b-197">토픽을 삭제하면 토픽에 등록된 모든 구독도 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-197">Deleting a topic will also delete any subscriptions that are registered with the topic.</span></span> <span data-ttu-id="f930b-198">구독을 개별적으로 삭제할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-198">Subscriptions can also be deleted independently.</span></span> <span data-ttu-id="f930b-199">아래 예제는 `HighMessages` 구독을 `MyTopic` 토픽에서 삭제하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-199">The following example shows how to delete a subscription named `HighMessages` from the `MyTopic` topic:</span></span>

```javascript
serviceBusService.deleteSubscription('MyTopic', 'HighMessages', function (error) {
    if(error) {
        console.log(error);
    }
});
```

## <a name="next-steps"></a><span data-ttu-id="f930b-200">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f930b-200">Next Steps</span></span>
<span data-ttu-id="f930b-201">이제 서비스 버스 토픽의 기본 사항을 익혔으므로 다음 링크를 따라 이동하여 자세한 내용을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f930b-201">Now that you've learned the basics of Service Bus topics, follow these links to learn more.</span></span>

* <span data-ttu-id="f930b-202">[큐, 토픽 및 구독][Queues, topics, and subscriptions]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f930b-202">See [Queues, topics, and subscriptions][Queues, topics, and subscriptions].</span></span>
* <span data-ttu-id="f930b-203">[SqlFilter][SqlFilter]에 대한 API 참조</span><span class="sxs-lookup"><span data-stu-id="f930b-203">API reference for [SqlFilter][SqlFilter].</span></span>
* <span data-ttu-id="f930b-204">GitHub에서 [Node용 Azure SDK][Azure SDK for Node] 리포지토리를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="f930b-204">Visit the [Azure SDK for Node][Azure SDK for Node] repository on GitHub.</span></span>

[Azure SDK for Node]: https://github.com/Azure/azure-sdk-for-node
[Azure portal]: https://portal.azure.com
[SqlFilter.SqlExpression]: service-bus-messaging-sql-filter.md
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter
[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Node.js 응용 프로그램을 만들어 Azure 웹 사이트에 배포]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js Cloud Service with Storage]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Node.js Web Application with Storage]:../cosmos-db/table-storage-cloud-service-nodejs.md

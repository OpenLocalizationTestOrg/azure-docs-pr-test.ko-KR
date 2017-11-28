---
title: "aaaHow toouse Azure 서비스 버스 토픽 및 구독 Node.js | Microsoft Docs"
description: "자세한 방법을 toouse 서비스 버스 항목 및 Azure에서 Node.js 응용 프로그램에서 구독 합니다."
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
ms.openlocfilehash: e8f6e7ad6ed16d844c408337ac9e50f990e3fafd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-nodejs"></a><span data-ttu-id="85a3f-103">어떻게 tooUse 서비스 버스 항목 및 구독 Node.js와 함께</span><span class="sxs-lookup"><span data-stu-id="85a3f-103">How tooUse Service Bus topics and subscriptions with Node.js</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="85a3f-104">이 가이드에서는 설명 방법을 toouse 서비스 버스 항목 및 Node.js 응용 프로그램에서 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-104">This guide describes how toouse Service Bus topics and subscriptions from Node.js applications.</span></span> <span data-ttu-id="85a3f-105">hello 가이드에서 다루는 시나리오 포함 **항목 및 구독을 만드는**, **구독 필터를 만드는**, **메시지를 보내는** tooa 항목 **받기 구독에서 메시지**, 및 **항목 및 구독을 삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-105">hello scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages** tooa topic, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span> <span data-ttu-id="85a3f-106">항목 및 구독에 대 한 자세한 내용은 참조 hello [다음 단계](#next-steps) 섹션.</span><span class="sxs-lookup"><span data-stu-id="85a3f-106">For more information about topics and subscriptions, see hello [Next steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="85a3f-107">Node.js 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="85a3f-107">Create a Node.js application</span></span>
<span data-ttu-id="85a3f-108">빈 Node.js 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-108">Create a blank Node.js application.</span></span> <span data-ttu-id="85a3f-109">Node.js 응용 프로그램을 만드는 방법에 지침은 [만들기 Node.js 응용 프로그램 tooan Azure 웹 사이트를 배포 하 고], [Node.js 클라우드 서비스] [ Node.js Cloud Service] 창을 사용 하 여 PowerShell 또는 WebMatrix로 웹 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-109">For instructions on creating a Node.js application, see [Create and deploy a Node.js application tooan Azure Web Site], [Node.js Cloud Service][Node.js Cloud Service] using Windows PowerShell, or Web Site with WebMatrix.</span></span>

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="85a3f-110">사용자 응용 프로그램 toouse 서비스 버스를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-110">Configure your application toouse Service Bus</span></span>
<span data-ttu-id="85a3f-111">서비스 버스 toouse hello Node.js Azure 패키지를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-111">toouse Service Bus, download hello Node.js Azure package.</span></span> <span data-ttu-id="85a3f-112">이 패키지는 hello 서비스 버스 REST 서비스와 통신 하는 라이브러리 집합에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-112">This package includes a set of libraries that communicate with hello Service Bus REST services.</span></span>

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a><span data-ttu-id="85a3f-113">노드 패키지 관리자 (NPM) tooobtain hello 패키지 사용</span><span class="sxs-lookup"><span data-stu-id="85a3f-113">Use Node Package Manager (NPM) tooobtain hello package</span></span>
1. <span data-ttu-id="85a3f-114">와 같은 명령줄 인터페이스를 사용 하 여 **PowerShell** (Windows) **터미널** (Mac) 또는 **를 이용한 적** (Unix) toohello 폴더 예제 응용 프로그램을 만들 위치를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-114">Use a command-line interface such as **PowerShell** (Windows,) **Terminal** (Mac,) or **Bash** (Unix), navigate toohello folder where you created your sample application.</span></span>
2. <span data-ttu-id="85a3f-115">형식 **npm 설치 azure** hello 명령 창에서 느려져서 해야에 저장 될 출력에 따라 hello:</span><span class="sxs-lookup"><span data-stu-id="85a3f-115">Type **npm install azure** in hello command window, which should result in hello following output:</span></span>

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
3. <span data-ttu-id="85a3f-116">Hello를 수동으로 실행할 수 있습니다 **ls** 명령 tooverify 하는 **노드\_모듈** 폴더를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-116">You can manually run hello **ls** command tooverify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="85a3f-117">해당 폴더를 찾습니다는 **azure** hello 필요한 라이브러리를 tooaccess 서비스 버스 주제를 포함 하는 패키지입니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-117">Inside that folder find the **azure** package, which contains hello libraries you need tooaccess Service Bus topics.</span></span>

### <a name="import-hello-module"></a><span data-ttu-id="85a3f-118">Hello 모듈 가져오기</span><span class="sxs-lookup"><span data-stu-id="85a3f-118">Import hello module</span></span>
<span data-ttu-id="85a3f-119">메모장 이나 다른 텍스트 편집기를 사용 하 여 추가 hello toohello 맨 뒤 hello **server.js** hello 응용 프로그램의 파일:</span><span class="sxs-lookup"><span data-stu-id="85a3f-119">Using Notepad or another text editor, add hello following toohello top of hello **server.js** file of hello application:</span></span>

```javascript
var azure = require('azure');
```

### <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="85a3f-120">서비스 버스 연결 설정</span><span class="sxs-lookup"><span data-stu-id="85a3f-120">Set up a Service Bus connection</span></span>
<span data-ttu-id="85a3f-121">hello Azure 모듈 hello 환경 변수를 읽습니다 `AZURE_SERVICEBUS_NAMESPACE` 및 `AZURE_SERVICEBUS_ACCESS_KEY` tooconnect tooService 버스는 데 필요한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-121">hello Azure module reads hello environment variables `AZURE_SERVICEBUS_NAMESPACE` and `AZURE_SERVICEBUS_ACCESS_KEY` for information required tooconnect tooService Bus.</span></span> <span data-ttu-id="85a3f-122">호출할 때 hello 계정 정보를 지정 해야 이러한 환경 변수가 설정 되지 않은 경우 `createServiceBusService`합니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-122">If these environment variables are not set, you must specify hello account information when calling `createServiceBusService`.</span></span>

<span data-ttu-id="85a3f-123">Azure 클라우드 서비스에 대 한 hello 환경 변수 설정의 예제를 보려면 [저장소와 클라우드 서비스 Node.js][Node.js Cloud Service with Storage]합니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-123">For an example of setting hello environment variables for an Azure Cloud Service, see [Node.js Cloud Service with Storage][Node.js Cloud Service with Storage].</span></span>

<span data-ttu-id="85a3f-124">Azure 웹 사이트에 대 한 hello 환경 변수 설정의 예제를 보려면 [Node.js 웹 응용 프로그램 저장소와][Node.js Web Application with Storage]합니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-124">For an example of setting hello environment variables for an Azure Website, see [Node.js Web Application with Storage][Node.js Web Application with Storage].</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="85a3f-125">토픽 만들기</span><span class="sxs-lookup"><span data-stu-id="85a3f-125">Create a topic</span></span>
<span data-ttu-id="85a3f-126">hello **ServiceBusService** 개체를 사용 하면 toowork 항목과 함께 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-126">hello **ServiceBusService** object enables you toowork with topics.</span></span> <span data-ttu-id="85a3f-127">다음 코드는 **ServiceBusService** 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-127">The following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="85a3f-128">Hello 맨 위 근처 추가 **server.js** 후 hello 문 tooimport hello azure 모듈 파일:</span><span class="sxs-lookup"><span data-stu-id="85a3f-128">Add it near the top of hello **server.js** file, after hello statement tooimport hello azure module:</span></span>

```javascript
var serviceBusService = azure.createServiceBusService();
```

<span data-ttu-id="85a3f-129">호출 하 여 `createTopicIfNotExists` hello에 **ServiceBusService** 개체, hello 항목 (있는 경우) 하는 경우 반환 될 지정 된 hello 지정한 이름 가진 새 항목을 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-129">By calling `createTopicIfNotExists` on hello **ServiceBusService** object, hello specified topic will be returned (if it exists,) or a new topic with hello specified name will be created.</span></span> <span data-ttu-id="85a3f-130">hello 다음 코드에서는 `createTopicIfNotExists` toocreate 이라는 toohello 항목을 연결 하거나 `MyTopic`:</span><span class="sxs-lookup"><span data-stu-id="85a3f-130">hello following code uses `createTopicIfNotExists` toocreate or connect toohello topic named `MyTopic`:</span></span>

```javascript
serviceBusService.createTopicIfNotExists('MyTopic',function(error){
    if(!error){
        // Topic was created or exists
        console.log('topic created or exists.');
    }
});
```

<span data-ttu-id="85a3f-131">hello `createServiceBusService` 메서드는 또한 메시지 시간 제한 또는 최대 항목 크기와 같은 toooverride 기본 항목 설정을 사용할 수 있는 추가 옵션을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-131">hello `createServiceBusService` method also supports additional options, which enable you toooverride default topic settings such as message time to live or maximum topic size.</span></span> <span data-ttu-id="85a3f-132">hello 다음 예제에서는 설정 hello 최대 항목 크기 too5GB 시간이 1 분의 toolive:</span><span class="sxs-lookup"><span data-stu-id="85a3f-132">hello following example sets hello maximum topic size too5GB with a time toolive of 1 minute:</span></span>

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

### <a name="filters"></a><span data-ttu-id="85a3f-133">필터</span><span class="sxs-lookup"><span data-stu-id="85a3f-133">Filters</span></span>
<span data-ttu-id="85a3f-134">(옵션) 필터링 작업이 적용 된 toooperations 사용 하 여 수행 될 수 있습니다 **ServiceBusService**합니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-134">Optional filtering operations can be applied toooperations performed using **ServiceBusService**.</span></span> <span data-ttu-id="85a3f-135">필터링 작업은 로깅, 자동 재시도 등을 포함할 수 있습니다. 필터는 hello 서명으로 메서드를 구현 하는 개체:</span><span class="sxs-lookup"><span data-stu-id="85a3f-135">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with hello signature:</span></span>

```javascript
function handle (requestOptions, next)
```

<span data-ttu-id="85a3f-136">Hello 요청 옵션에 전처리를 수행한 후 메서드 호출을 hello `next`, 콜백을 뒤 서명에 hello로 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-136">After performing preprocessing on hello request options, hello method calls `next`, passing a callback with hello following signature:</span></span>

```javascript
function (returnObject, finalCallback, next)
```

<span data-ttu-id="85a3f-137">이 콜백 및 후 처리 hello `returnObject` (hello 요청 toohello 서버 로부터 응답 hello) hello 콜백에 필요한 tooeither 호출 하거나 다른 필터를 처리 하는 toocontinue 있는 경우 다음에 호출할 `finalCallback` 그렇지 tooend hello 서비스 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-137">In this callback, and after processing hello `returnObject` (hello response from hello request toohello server), hello callback needs tooeither invoke next if it exists toocontinue processing other filters or invoke `finalCallback` otherwise, tooend hello service invocation.</span></span>

<span data-ttu-id="85a3f-138">재시도 논리를 구현 하는 두 개의 필터 hello Node.js 용 Azure SDK에 포함 된 **ExponentialRetryPolicyFilter** 및 **LinearRetryPolicyFilter**합니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-138">Two filters that implement retry logic are included with hello Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="85a3f-139">hello 다음 만듭니다는 **ServiceBusService** hello를 사용 하는 개체 **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="85a3f-139">hello following creates a **ServiceBusService** object that uses hello **ExponentialRetryPolicyFilter**:</span></span>

```javascript
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var serviceBusService = azure.createServiceBusService().withFilter(retryOperations);
```

## <a name="create-subscriptions"></a><span data-ttu-id="85a3f-140">구독 만들기</span><span class="sxs-lookup"><span data-stu-id="85a3f-140">Create subscriptions</span></span>
<span data-ttu-id="85a3f-141">주제 구독에도 hello를 사용 하 여 만들어진 **ServiceBusService** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-141">Topic subscriptions are also created with hello **ServiceBusService** object.</span></span> <span data-ttu-id="85a3f-142">이름이 지정 된 구독과 hello toohello 구독의 가상 큐에 배달 된 메시지 집합을 제한 하는 선택적 필터가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-142">Subscriptions are named and can have an optional filter that restricts hello set of messages delivered toohello subscription's virtual queue.</span></span>

> [!NOTE]
> <span data-ttu-id="85a3f-143">구독 영구 tooexist 중 하나가 될 때까지 계속 사용 되며 또는 hello이 항목은 연관 된, 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-143">Subscriptions are persistent and will continue tooexist until either they, or hello topic they are associated with, are deleted.</span></span> <span data-ttu-id="85a3f-144">응용 프로그램 논리 toocreate 구독 있으면 먼저 체크 사용 하 여 hello 구독에 이미 존재 하는 경우는 `getSubscription` 메서드.</span><span class="sxs-lookup"><span data-stu-id="85a3f-144">If your application contains logic toocreate a subscription, it should first check if hello subscription already exists by using the `getSubscription` method.</span></span>
>
>

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a><span data-ttu-id="85a3f-145">Hello 기본 (MatchAll) 필터와 구독 만들기</span><span class="sxs-lookup"><span data-stu-id="85a3f-145">Create a subscription with hello default (MatchAll) filter</span></span>
<span data-ttu-id="85a3f-146">hello **MatchAll** 필터는 필터 지정 하지 않으면은 새 구독을 만들 때 사용 되는 hello 기본 필터.</span><span class="sxs-lookup"><span data-stu-id="85a3f-146">hello **MatchAll** filter is hello default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="85a3f-147">Hello 때 **MatchAll** 필터 사용 하는 경우 모든 메시지 게시 된 toohello 항목 구독의 가상 큐에 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-147">When hello **MatchAll** filter is used, all messages published toohello topic are placed in the subscription's virtual queue.</span></span> <span data-ttu-id="85a3f-148">hello 다음 예제에서는 'AllMessages' 이라는 구독을 만들고 사용 하 여 기본 hello **MatchAll** 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-148">hello following example creates a subscription named 'AllMessages' and uses hello default **MatchAll** filter.</span></span>

```javascript
serviceBusService.createSubscription('MyTopic','AllMessages',function(error){
    if(!error){
        // subscription created
    }
});
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="85a3f-149">필터를 사용하여 구독 만들기</span><span class="sxs-lookup"><span data-stu-id="85a3f-149">Create subscriptions with filters</span></span>
<span data-ttu-id="85a3f-150">Tooscope tooa 항목에 특정 항목을 구독 내에서 표시 됩니다. 보낸 메시지를 허용 하는 필터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-150">You can also create filters that allow you tooscope which messages sent tooa topic should show up within a specific topic subscription.</span></span>

<span data-ttu-id="85a3f-151">hello 가장 유연한 구독에서 지 원하는 필터 형식은 **SqlFilter**, SQL92의 하위 집합을 구현 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-151">hello most flexible type of filter supported by subscriptions is the **SqlFilter**, which implements a subset of SQL92.</span></span> <span data-ttu-id="85a3f-152">SQL 필터가 있는 게시 된 toohello 항목 hello 메시지의 hello 속성에서 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-152">SQL filters operate on hello properties of hello messages that are published toohello topic.</span></span> <span data-ttu-id="85a3f-153">SQL 필터와 함께 사용할 수 있는 hello 식에 대 한 자세한 내용은 hello 검토 [SqlFilter.SqlExpression] [ SqlFilter.SqlExpression] 구문입니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-153">For more details about hello expressions that can be used with a SQL filter, review hello [SqlFilter.SqlExpression][SqlFilter.SqlExpression] syntax.</span></span>

<span data-ttu-id="85a3f-154">필터 hello를 사용 하 여 tooa 구독 추가할 수 있습니다 `createRule` hello 방식의 **ServiceBusService** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-154">Filters can be added tooa subscription by using hello `createRule` method of hello **ServiceBusService** object.</span></span> <span data-ttu-id="85a3f-155">이 메서드를 사용 하면 새 필터 tooan 기존 구독을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-155">This method allows you to add new filters tooan existing subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="85a3f-156">Hello 기본 필터를 자동으로 적용 되기 때문에 tooall 새 구독 hello 기본 필터를 먼저 제거 해야 또는 **MatchAll** 지정할 수 있는 필터를 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-156">Because hello default filter is applied automatically tooall new subscriptions, you must first remove hello default filter or the **MatchAll** will override any other filters you may specify.</span></span> <span data-ttu-id="85a3f-157">Hello를 사용 하 여 hello 기본 규칙을 제거할 수 있습니다 `deleteRule` 의 메서드는 **ServiceBusService** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-157">You can remove hello default rule by using hello `deleteRule` method of the **ServiceBusService** object.</span></span>
>
>

<span data-ttu-id="85a3f-158">hello 다음 예제에서는 구독을 만드는 라는 `HighMessages` 와 **SqlFilter** 만 사용자 지정 하는 메시지를 선택 하는 `messagenumber` 3 보다 큰 속성:</span><span class="sxs-lookup"><span data-stu-id="85a3f-158">hello following example creates a subscription named `HighMessages` with a **SqlFilter** that only selects messages that have a custom `messagenumber` property greater than 3:</span></span>

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

<span data-ttu-id="85a3f-159">마찬가지로, hello 다음 예제에서는 구독을 만드는 라는 `LowMessages` 와 **SqlFilter** 만 설정 된 메시지를 선택 하는 `messagenumber` 속성 작은 보다 짧거나 too3:</span><span class="sxs-lookup"><span data-stu-id="85a3f-159">Similarly, hello following example creates a subscription named `LowMessages` with a **SqlFilter** that only selects messages that have a `messagenumber` property less than or equal too3:</span></span>

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

<span data-ttu-id="85a3f-160">메시지는 이제 보내면 너무`MyTopic`, toohello 구독 하는 수신기로 배달 항상 됩니다 `AllMessages` 항목 구독 및 구독 하는 선택적으로 배달 된 tooreceivers toohello `HighMessages` 및 `LowMessages` 주제 구독 (hello 메시지 내용에 따라).</span><span class="sxs-lookup"><span data-stu-id="85a3f-160">When a message is now sent too`MyTopic`, it will always be delivered to receivers subscribed toohello `AllMessages` topic subscription, and selectively delivered tooreceivers subscribed toohello `HighMessages` and `LowMessages` topic subscriptions (depending upon hello message content).</span></span>

## <a name="how-toosend-messages-tooa-topic"></a><span data-ttu-id="85a3f-161">Toosend는 tooa 항목 메시지 방법을</span><span class="sxs-lookup"><span data-stu-id="85a3f-161">How toosend messages tooa topic</span></span>
<span data-ttu-id="85a3f-162">응용 프로그램에서 사용 해야 메시지 tooa 서비스 버스 항목 toosend는 `sendTopicMessage` hello 방식의 **ServiceBusService** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-162">toosend a message tooa Service Bus topic, your application must use the `sendTopicMessage` method of hello **ServiceBusService** object.</span></span>
<span data-ttu-id="85a3f-163">메시지가 전송 tooService 버스 주제는 **BrokeredMessage** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-163">Messages sent tooService Bus topics are **BrokeredMessage** objects.</span></span>
<span data-ttu-id="85a3f-164">**BrokeredMessage** 개체에는 표준 속성 집합이 있습니다 (같은 `Label` 및 `TimeToLive`), 사용자 지정 응용 프로그램 특정 속성 사용 되는 toohold 있는 사전 및 문자열 데이터의 본문입니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-164">**BrokeredMessage** objects have a set of standard properties (such as `Label` and `TimeToLive`), a dictionary that is used toohold custom application-specific properties, and a body of string data.</span></span> <span data-ttu-id="85a3f-165">응용 프로그램 hello에는 문자열 값을 전달 하 여 hello hello 메시지 본문을 설정할 수 `sendTopicMessage` 필요한 표준 속성 기본 값으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-165">An application can set hello body of hello message by passing a string value to hello `sendTopicMessage` and any required standard properties will be populated by default values.</span></span>

<span data-ttu-id="85a3f-166">hello 다음 예제에서는 어떻게 toosend 5 테스트 메시지를 `MyTopic`합니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-166">hello following example demonstrates how toosend five test messages to `MyTopic`.</span></span> <span data-ttu-id="85a3f-167">해당 hello 참고 `messagenumber` hello 루프의 반복 hello에 각 메시지의 속성 값 달라 집니다 (이 결정 합니다 구독 받는):</span><span class="sxs-lookup"><span data-stu-id="85a3f-167">Note that hello `messagenumber` property value of each message varies on hello iteration of hello loop (this will determine which subscriptions receive it):</span></span>

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

<span data-ttu-id="85a3f-168">서비스 버스 주제 hello에서 최대 메시지 크기는 256KB 지원 [표준 계층](service-bus-premium-messaging.md) 및 hello에서 1 MB [Premium 계층](service-bus-premium-messaging.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-168">Service Bus topics support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="85a3f-169">hello 표준 및 사용자 지정 응용 프로그램 속성을 포함 하는 hello 헤더는 64KB의 최대 크기를 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-169">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="85a3f-170">Hello 메시지에 항목을 보유할 수에 제한이 없음을 않으며 항목을 보유 하는 hello 메시지의 총 크기 hello 켜져 캡입니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-170">There is no limit on hello number of messages held in a topic but there is a cap on hello total size of hello messages held by a topic.</span></span> <span data-ttu-id="85a3f-171">이 토픽 크기는 생성 시 정의되며 상한이 5GB입니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-171">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="85a3f-172">구독에서 메시지 받기</span><span class="sxs-lookup"><span data-stu-id="85a3f-172">Receive messages from a subscription</span></span>
<span data-ttu-id="85a3f-173">사용 하 여 구독에서 메시지가 수신 되는 `receiveSubscriptionMessage` 메서드 hello **ServiceBusService** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-173">Messages are received from a subscription using the `receiveSubscriptionMessage` method on hello **ServiceBusService** object.</span></span> <span data-ttu-id="85a3f-174">기본적으로 메시지는 구독에서 삭제 hello 읽어; 그러나 (미리 보기)를 읽을 수 있으며 설정 hello 선택적 매개 변수 여 hello 구독에서 삭제 하지 않고 hello 메시지 잠금 `isPeekLock` 너무**true**합니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-174">By default, messages are deleted from hello subscription as they are read; however, you can read (peek) and lock hello message without deleting it from hello subscription by setting hello optional parameter `isPeekLock` too**true**.</span></span>

<span data-ttu-id="85a3f-175">hello 읽고 수신 작업의 일부로 hello 가장 간단한 모델 이며 가장 적합 한 시나리오는 응용 프로그램 실패 하는 hello 이벤트의 메시지를 처리 하지 않아도 안전한 수으로 hello 메시지를 삭제 합니다. 기본 동작입니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-175">hello default behavior of reading and deleting hello message as part of the receive operation is hello simplest model, and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="85a3f-176">toounderstand 소비자 문제 hello는 요청을 수신 하는 시나리오 및 후 처리 하기 전에 크래시 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-176">toounderstand this, consider a scenario in which the consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="85a3f-177">서비스 버스 사용 되는 것을 다음 hello 응용 프로그램 다시 시작 되 고 메시지 사용을 시작할 때 hello 메시지를 표시 한 됩니다, 때문에 누락 됩니다 hello 메시지 했던 이전 toohello 크래시를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-177">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="85a3f-178">경우 hello `isPeekLock` 매개 변수가 너무 설정 된**true**, hello 수신 하므로 누락 된 메시지를 허용할 수 없는 가능한 toosupport 응용 프로그램 2 단계 작업이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-178">If hello `isPeekLock` parameter is set too**true**, hello receive becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="85a3f-179">서비스 버스 요청을 받으면 다음 메시지 toobe hello 사용 다른 소비자가 수신할 tooprevent 잠근 하 고 toohello 응용 프로그램 반환 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-179">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span>
<span data-ttu-id="85a3f-180">호출 하 여 수신 프로세스의 2 단계 hello hello 응용 프로그램 hello 메시지 처리를 완료 (또는 이후 처리를 위해 안정적으로 저장) 한 후 완료 **deleteMessage** 메서드와 메시지 toobe 제공 매개 변수로 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-180">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of the receive process by calling **deleteMessage** method and providing the message toobe deleted as a parameter.</span></span> <span data-ttu-id="85a3f-181">hello **deleteMessage** 메서드 hello 메시지를 사용 되 고 표시 하 고 hello 구독에서 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-181">hello **deleteMessage** method will mark hello message as being consumed and remove it from hello subscription.</span></span>

<span data-ttu-id="85a3f-182">hello 다음 예제에서는 메시지를 수신할 수 방법 및 처리를 사용 하 여 `receiveSubscriptionMessage`합니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-182">hello following example demonstrates how messages can be received and processed using `receiveSubscriptionMessage`.</span></span> <span data-ttu-id="85a3f-183">hello 예에서는 먼저 수신 하 고 hello 'LowMessages' 구독에서에서 메시지를 삭제 하 고 사용 하 여 hello 'HighMessages' 구독에서 메시지를 받습니다 `isPeekLock` tootrue를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-183">hello example first receives and deletes a message from hello 'LowMessages' subscription, and then receives a message from hello 'HighMessages' subscription using `isPeekLock` set tootrue.</span></span> <span data-ttu-id="85a3f-184">다음 사용 하 여 hello 메시지 삭제 `deleteMessage`:</span><span class="sxs-lookup"><span data-stu-id="85a3f-184">It then deletes hello message using `deleteMessage`:</span></span>

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

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="85a3f-185">Toohandle 응용 프로그램이 크래시 되는 방법 및 읽을 수 없는 메시지</span><span class="sxs-lookup"><span data-stu-id="85a3f-185">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="85a3f-186">서비스 버스 기능 toohelp 정상적으로 응용 프로그램 또는 메시지를 처리 하는 데 문제가 오류 로부터 복구를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-186">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="85a3f-187">수신기 응용 프로그램 수 없는 경우 몇 가지 이유로 tooprocess 환영 메시지가 다음 hello 호출할 수 있는 `unlockMessage` 에서 메서드는 **ServiceBusService** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-187">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlockMessage` method on the **ServiceBusService** object.</span></span> <span data-ttu-id="85a3f-188">이 서비스 버스 toounlock hello 구독 내에서 메시지 되며 수신 다시 사용할 수 있는 toobe 확인, 사용자가 여를 많이 사용 응용 프로그램 또는 다른 소비 응용 프로그램에서 동일한 hello 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-188">This will cause Service Bus toounlock the message within hello subscription and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="85a3f-189">또한 시간 초과 구독 내에서 잠긴 메시지와 관련 된 집합과 hello 응용 프로그램 실패 하기 전에 hello 메시지 tooprocess hello 잠금 제한 시간이 만료 (예를 들어 hello 응용 프로그램이 충돌할 경우), 서비스 버스 hello 메시지의 잠금을 해제 한 다음 자동으로 수신 다시 사용할 수 있는 toobe로 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-189">There is also a timeout associated with a message locked within the subscription, and if hello application fails tooprocess hello message before hello lock timeout expires (for example, if hello application crashes), then Service Bus unlocks hello message automatically and makes it available toobe received again.</span></span>

<span data-ttu-id="85a3f-190">Hello hello 응용 프로그램 이벤트 충돌 hello 메시지 처리 전후에 그러나 hello 전에 `deleteMessage` 메서드는 다음 다시 시작할 때 hello 메시지 다시 전달한 toohello 응용 프로그램 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-190">In hello event that hello application crashes after processing hello message but before hello `deleteMessage` method is called, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="85a3f-191">이 이라고 하는데 *일단 처리 이상*, 즉, 각 메시지가 최소 한 번 처리 되지만 특정 상황 hello에 동일한 메시지를 다시 배달 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-191">This is often called *At Least Once Processing*, that is, each message will be processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="85a3f-192">Hello 시나리오 중복 처리가 허용 되지 않는, 응용 프로그램 개발자가 추가 논리 tootheir 응용 프로그램을 toohandle 중복 메시지 배달을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-192">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="85a3f-193">이 대개 달성를 사용 하 여는 **MessageId** 배달 시도 간에 일정 남아 있는 hello 메시지의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-193">This is often achieved using the **MessageId** property of hello message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="85a3f-194">토픽 및 구독 삭제</span><span class="sxs-lookup"><span data-stu-id="85a3f-194">Delete topics and subscriptions</span></span>
<span data-ttu-id="85a3f-195">항목과 구독은 영구적이 고 명시적으로 해야 hello 통해 삭제 [Azure 포털] [ Azure portal] 또는 프로그래밍 방식으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-195">Topics and subscriptions are persistent, and must be explicitly deleted either through hello [Azure portal][Azure portal] or programmatically.</span></span>
<span data-ttu-id="85a3f-196">hello 다음 예제에서는 toodelete hello 항목 이름을 지정 하는 방법 `MyTopic`:</span><span class="sxs-lookup"><span data-stu-id="85a3f-196">hello following example demonstrates how toodelete hello topic named `MyTopic`:</span></span>

```javascript
serviceBusService.deleteTopic('MyTopic', function (error) {
    if (error) {
        console.log(error);
    }
});
```

<span data-ttu-id="85a3f-197">항목 삭제 hello 항목으로 등록 하는 모든 구독도 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-197">Deleting a topic will also delete any subscriptions that are registered with hello topic.</span></span> <span data-ttu-id="85a3f-198">구독을 개별적으로 삭제할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-198">Subscriptions can also be deleted independently.</span></span> <span data-ttu-id="85a3f-199">다음 예제에서는 어떻게 toodelete 구독 이라는 `HighMessages` hello에서 `MyTopic` 항목:</span><span class="sxs-lookup"><span data-stu-id="85a3f-199">The following example shows how toodelete a subscription named `HighMessages` from hello `MyTopic` topic:</span></span>

```javascript
serviceBusService.deleteSubscription('MyTopic', 'HighMessages', function (error) {
    if(error) {
        console.log(error);
    }
});
```

## <a name="next-steps"></a><span data-ttu-id="85a3f-200">다음 단계</span><span class="sxs-lookup"><span data-stu-id="85a3f-200">Next Steps</span></span>
<span data-ttu-id="85a3f-201">서비스 버스 항목의 hello 기본 사항 학습 한, 했으므로 이러한 링크 toolearn 자세한 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-201">Now that you've learned hello basics of Service Bus topics, follow these links toolearn more.</span></span>

* <span data-ttu-id="85a3f-202">[큐, 토픽 및 구독][Queues, topics, and subscriptions]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="85a3f-202">See [Queues, topics, and subscriptions][Queues, topics, and subscriptions].</span></span>
* <span data-ttu-id="85a3f-203">[SqlFilter][SqlFilter]에 대한 API 참조</span><span class="sxs-lookup"><span data-stu-id="85a3f-203">API reference for [SqlFilter][SqlFilter].</span></span>
* <span data-ttu-id="85a3f-204">Hello 방문 [노드 용 Azure SDK] [ Azure SDK for Node] GitHub의 리포지토리 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a3f-204">Visit hello [Azure SDK for Node][Azure SDK for Node] repository on GitHub.</span></span>

[Azure SDK for Node]: https://github.com/Azure/azure-sdk-for-node
[Azure portal]: https://portal.azure.com
[SqlFilter.SqlExpression]: service-bus-messaging-sql-filter.md
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter
[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[만들기 Node.js 응용 프로그램 tooan Azure 웹 사이트를 배포 하 고]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js Cloud Service with Storage]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Node.js Web Application with Storage]:../cosmos-db/table-storage-cloud-service-nodejs.md

---
title: "aaaAzure 함수 이벤트 허브 바인딩 | Microsoft Docs"
description: "이해 어떻게 Azure 함수에서 toouse Azure 이벤트 허브 바인딩."
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: "Azure Functions, 함수, 이벤트 처리, 동적 계산, 서버를 사용하지 않는 아키텍처"
ms.assetid: daf81798-7acc-419a-bc32-b5a41c6db56b
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/20/2017
ms.author: wesmc
ms.openlocfilehash: e864f032ad5ac58d318c9843c3844b5642733a70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-event-hubs-bindings"></a><span data-ttu-id="91e46-104">Azure Functions Event Hubs 바인딩</span><span class="sxs-lookup"><span data-stu-id="91e46-104">Azure Functions Event Hubs bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="91e46-105">이 문서에서는 설명 어떻게 tooconfigure 사용 하 여 [Azure 이벤트 허브](../event-hubs/event-hubs-what-is-event-hubs.md) Azure 함수에 대 한 바인딩을 합니다.</span><span class="sxs-lookup"><span data-stu-id="91e46-105">This article explains how tooconfigure and use [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md) bindings for Azure Functions.</span></span>
<span data-ttu-id="91e46-106">Azure Functions는 이벤트 허브에 대한 트리거 및 출력 바인딩을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="91e46-106">Azure Functions supports trigger and output bindings for Event Hubs.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="91e46-107">새 tooAzure 이벤트 허브 인 경우 참조 hello [이벤트 허브 개요](../event-hubs/event-hubs-what-is-event-hubs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="91e46-107">If you are new tooAzure Event Hubs, see hello [Event Hubs overview](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span>

<a name="trigger"></a>

## <a name="event-hub-trigger"></a><span data-ttu-id="91e46-108">Event Hubs 트리거</span><span class="sxs-lookup"><span data-stu-id="91e46-108">Event hub trigger</span></span>
<span data-ttu-id="91e46-109">사용 하 여 hello 이벤트 허브 tooan 이벤트 허브 이벤트 스트림을 전송 toorespond tooan 이벤트를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="91e46-109">Use hello Event Hubs trigger toorespond tooan event sent tooan event hub event stream.</span></span> <span data-ttu-id="91e46-110">Hello 트리거를 toohello 이벤트 허브 tooset 읽기 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91e46-110">You must have read access toohello event hub tooset up hello trigger.</span></span>

<span data-ttu-id="91e46-111">hello hello에 대 한 JSON 개체를 다음을 사용 하 여 hello 이벤트 허브 함수 트리거 `bindings` 배열 function.json입니다.</span><span class="sxs-lookup"><span data-stu-id="91e46-111">hello Event Hubs function trigger uses hello following JSON object in hello `bindings` array of function.json:</span></span>

```json
{
    "type": "eventHubTrigger",
    "name": "<Name of trigger parameter in function signature>",
    "direction": "in",
    "path": "<Name of hello event hub>",
    "consumerGroup": "Consumer group toouse - see below",
    "connection": "<Name of app setting with connection string - see below>"
}
```

<span data-ttu-id="91e46-112">`consumerGroup`사용 되는 속성 (옵션) tooset hello [소비자 그룹](../event-hubs/event-hubs-features.md#event-consumers) toosubscribe tooevents hello 허브에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="91e46-112">`consumerGroup` is an optional property used tooset hello [consumer group](../event-hubs/event-hubs-features.md#event-consumers) used toosubscribe tooevents in hello hub.</span></span> <span data-ttu-id="91e46-113">생략 하면 hello `$Default` 소비자 그룹이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="91e46-113">If omitted, hello `$Default` consumer group is used.</span></span>  
<span data-ttu-id="91e46-114">`connection`hello 연결 문자열 toohello 이벤트 허브의 네임 스페이스를 포함 하는 응용 프로그램 설정의 hello 이름 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91e46-114">`connection` must be hello name of an app setting that contains hello connection string toohello event hub's namespace.</span></span>
<span data-ttu-id="91e46-115">Hello를 클릭 하 여이 연결 문자열을 복사 **연결 정보** hello에 대 한 단추 *네임 스페이스*, 하지 hello 이벤트 허브 자체입니다.</span><span class="sxs-lookup"><span data-stu-id="91e46-115">Copy this connection string by clicking hello **Connection Information** button for hello *namespace*, not hello event hub itself.</span></span> <span data-ttu-id="91e46-116">이 연결 문자열 사용 권한 tooactivate hello 트리거 최소한 읽기 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91e46-116">This connection string must have at least read permissions tooactivate hello trigger.</span></span>

<span data-ttu-id="91e46-117">[추가 설정을](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) 파일 toofurther 미세 하 게 한 host.json에서는 이벤트 허브 트리거를 튜닝할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91e46-117">[Additional settings](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) can be provided in a host.json file toofurther fine tune Event Hubs triggers.</span></span>  

<a name="triggerusage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="91e46-118">트리거 사용</span><span class="sxs-lookup"><span data-stu-id="91e46-118">Trigger usage</span></span>
<span data-ttu-id="91e46-119">이벤트 허브 트리거 기능 트리거되면를 트리거하는 hello 메시지를 문자열로 hello 함수에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="91e46-119">When an Event Hubs trigger function is triggered, hello message that triggers it is passed into hello function as a string.</span></span>

<a name="triggersample"></a>

## <a name="trigger-sample"></a><span data-ttu-id="91e46-120">트리거 샘플</span><span class="sxs-lookup"><span data-stu-id="91e46-120">Trigger sample</span></span>
<span data-ttu-id="91e46-121">있다고 가정 하면 다음과 같은 이벤트 허브 hello 트리거할 hello `bindings` function.json의 배열:</span><span class="sxs-lookup"><span data-stu-id="91e46-121">Suppose you have hello following Event Hubs trigger in hello `bindings` array of function.json:</span></span>

```json
{
  "type": "eventHubTrigger",
  "name": "myEventHubMessage",
  "direction": "in",
  "path": "MyEventHub",
  "connection": "myEventHubReadConnectionString"
}
```

<span data-ttu-id="91e46-122">이벤트 허브 트리거 hello hello 메시지 본문을 기록 하는 hello 언어 관련 샘플을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="91e46-122">See hello language-specific sample that logs hello message body of hello event hub trigger.</span></span>

* [<span data-ttu-id="91e46-123">C#</span><span class="sxs-lookup"><span data-stu-id="91e46-123">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="91e46-124">F#</span><span class="sxs-lookup"><span data-stu-id="91e46-124">F#</span></span>](#triggerfsharp)
* [<span data-ttu-id="91e46-125">Node.JS</span><span class="sxs-lookup"><span data-stu-id="91e46-125">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="91e46-126">C#에서 트리거 샘플</span><span class="sxs-lookup"><span data-stu-id="91e46-126">Trigger sample in C#</span></span> #

```cs
using System;

public static void Run(string myEventHubMessage, TraceWriter log)
{
    log.Info($"C# Event Hub trigger function processed a message: {myEventHubMessage}");
}
```

<span data-ttu-id="91e46-127">또한으로 hello 이벤트를 받을 수 있습니다는 [EventData](/dotnet/api/microsoft.servicebus.messaging.eventdata) toohello 이벤트 메타 데이터를 액세스 하는 개체 수 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="91e46-127">You can also receive hello event as an [EventData](/dotnet/api/microsoft.servicebus.messaging.eventdata) object, which gives you access toohello event metadata.</span></span>

```cs
#r "Microsoft.ServiceBus"
using System.Text;
using Microsoft.ServiceBus.Messaging;

public static void Run(EventData myEventHubMessage, TraceWriter log)
{
    log.Info($"{Encoding.UTF8.GetString(myEventHubMessage.GetBytes())}");
}
```

<span data-ttu-id="91e46-128">hello 메서드 시그니처를 너무 변경 tooreceive 이벤트는 일괄 처리에서`string[]` 또는 `EventData[]`합니다.</span><span class="sxs-lookup"><span data-stu-id="91e46-128">tooreceive events in a batch, change hello method signature too`string[]` or `EventData[]`.</span></span>

```cs
public static void Run(string[] eventHubMessages, TraceWriter log)
{
    foreach (var message in eventHubMessages)
    {
        log.Info($"C# Event Hub trigger function processed a message: {message}");
    }
}
```

<a name="triggerfsharp"></a>

### <a name="trigger-sample-in-f"></a><span data-ttu-id="91e46-129">F#에서 트리거 샘플</span><span class="sxs-lookup"><span data-stu-id="91e46-129">Trigger sample in F#</span></span> #

```fsharp
let Run(myEventHubMessage: string, log: TraceWriter) =
    log.Info(sprintf "F# eventhub trigger function processed work item: %s" myEventHubMessage)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="91e46-130">Node.js에서 트리거 샘플</span><span class="sxs-lookup"><span data-stu-id="91e46-130">Trigger sample in Node.js</span></span>

```javascript
module.exports = function (context, myEventHubMessage) {
    context.log('Node.js eventhub trigger function processed work item', myEventHubMessage);    
    context.done();
};
```

<a name="output"></a>

## <a name="event-hubs-output-binding"></a><span data-ttu-id="91e46-131">Event Hubs 출력 바인딩</span><span class="sxs-lookup"><span data-stu-id="91e46-131">Event Hubs output binding</span></span>
<span data-ttu-id="91e46-132">이벤트 허브 사용 하 여 hello 바인딩 toowrite 이벤트 tooan 이벤트 허브 이벤트 스트림을 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="91e46-132">Use hello Event Hubs output binding toowrite events tooan event hub event stream.</span></span> <span data-ttu-id="91e46-133">Send 권한 tooan 이벤트 허브 toowrite 이벤트 tooit이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91e46-133">You must have send permission tooan event hub toowrite events tooit.</span></span>

<span data-ttu-id="91e46-134">hello 출력 바인딩이 사용 하 여 hello에 대 한 JSON 개체를 다음 hello `bindings` function.json의 배열:</span><span class="sxs-lookup"><span data-stu-id="91e46-134">hello output binding uses hello following JSON object in hello `bindings` array of function.json:</span></span>

```json
{
    "type": "eventHub",
    "name": "<Name of output parameter in function signature>",
    "path": "<Name of event hub>",
    "connection": "<Name of app setting with connection string - see below>"
    "direction": "out"
}
```

<span data-ttu-id="91e46-135">`connection`hello 연결 문자열 toohello 이벤트 허브의 네임 스페이스를 포함 하는 응용 프로그램 설정의 hello 이름 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91e46-135">`connection` must be hello name of an app setting that contains hello connection string toohello event hub's namespace.</span></span>
<span data-ttu-id="91e46-136">Hello를 클릭 하 여이 연결 문자열을 복사 **연결 정보** hello에 대 한 단추 *네임 스페이스*, 하지 hello 이벤트 허브 자체입니다.</span><span class="sxs-lookup"><span data-stu-id="91e46-136">Copy this connection string by clicking hello **Connection Information** button for hello *namespace*, not hello event hub itself.</span></span> <span data-ttu-id="91e46-137">이 연결 문자열에는 send 권한을 toosend hello 메시지 toohello 이벤트 스트림에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91e46-137">This connection string must have send permissions toosend hello message toohello event stream.</span></span>

## <a name="output-usage"></a><span data-ttu-id="91e46-138">출력 사용</span><span class="sxs-lookup"><span data-stu-id="91e46-138">Output usage</span></span>
<span data-ttu-id="91e46-139">이 섹션에서는 어떻게 toouse 이벤트 허브 출력 함수 코드에서 바인딩을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="91e46-139">This section shows you how toouse your Event Hubs output binding in your function code.</span></span>

<span data-ttu-id="91e46-140">매개 변수 유형만 hello로 메시지 구성 toohello 이벤트 허브를 출력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91e46-140">You can output messages toohello configured event hub with hello following parameter types:</span></span>

* `out string`
* <span data-ttu-id="91e46-141">`ICollector<string>`(toooutput 여러 메시지)</span><span class="sxs-lookup"><span data-stu-id="91e46-141">`ICollector<string>` (toooutput multiple messages)</span></span>
* <span data-ttu-id="91e46-142">`IAsyncCollector<string>`(비동기 버전의 `ICollector<T>`)</span><span class="sxs-lookup"><span data-stu-id="91e46-142">`IAsyncCollector<string>` (async version of `ICollector<T>`)</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="91e46-143">출력 샘플</span><span class="sxs-lookup"><span data-stu-id="91e46-143">Output sample</span></span>
<span data-ttu-id="91e46-144">이벤트 허브 출력 바인딩 hello에 있다고 가정 하면 hello 다음 `bindings` function.json의 배열:</span><span class="sxs-lookup"><span data-stu-id="91e46-144">Suppose you have hello following Event Hubs output binding in hello `bindings` array of function.json:</span></span>

```json
{
    "type": "eventHub",
    "name": "outputEventHubMessage",
    "path": "myeventhub",
    "connection": "MyEventHubSend",
    "direction": "out"
}
```

<span data-ttu-id="91e46-145">이벤트 toohello 짝수 스트림을 작성 하는 hello 언어 관련 샘플을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="91e46-145">See hello language-specific sample that writes an event toohello even stream.</span></span>

* [<span data-ttu-id="91e46-146">C#</span><span class="sxs-lookup"><span data-stu-id="91e46-146">C#</span></span>](#outcsharp)
* [<span data-ttu-id="91e46-147">F#</span><span class="sxs-lookup"><span data-stu-id="91e46-147">F#</span></span>](#outfsharp)
* [<span data-ttu-id="91e46-148">Node.JS</span><span class="sxs-lookup"><span data-stu-id="91e46-148">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="91e46-149">C#에서 출력 샘플</span><span class="sxs-lookup"><span data-stu-id="91e46-149">Output sample in C#</span></span> #

```cs
using System;

public static void Run(TimerInfo myTimer, out string outputEventHubMessage, TraceWriter log)
{
    String msg = $"TimerTriggerCSharp1 executed at: {DateTime.Now}";
    log.Verbose(msg);   
    outputEventHubMessage = msg;
}
```

<span data-ttu-id="91e46-150">또는 toocreate 여러 메시지:</span><span class="sxs-lookup"><span data-stu-id="91e46-150">Or, toocreate multiple messages:</span></span>

```cs
public static void Run(TimerInfo myTimer, ICollector<string> outputEventHubMessage, TraceWriter log)
{
    string message = $"Event Hub message created at: {DateTime.Now}";
    log.Info(message);
    outputEventHubMessage.Add("1 " + message);
    outputEventHubMessage.Add("2 " + message);
}
```

<a name="outfsharp"></a>

### <a name="output-sample-in-f"></a><span data-ttu-id="91e46-151">F#에서 출력 샘플</span><span class="sxs-lookup"><span data-stu-id="91e46-151">Output sample in F#</span></span> #

```fsharp
let Run(myTimer: TimerInfo, outputEventHubMessage: byref<string>, log: TraceWriter) =
    let msg = sprintf "TimerTriggerFSharp1 executed at: %s" DateTime.Now.ToString()
    log.Verbose(msg);
    outputEventHubMessage <- msg;
```

<a name="outnodejs"></a>

### <a name="output-sample-for-nodejs"></a><span data-ttu-id="91e46-152">Node.js에서 출력 샘플</span><span class="sxs-lookup"><span data-stu-id="91e46-152">Output sample for Node.js</span></span>

```javascript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();
    context.log('Event Hub message created at: ', timeStamp);   
    context.bindings.outputEventHubMessage = "Event Hub message created at: " + timeStamp;
    context.done();
};
```

<span data-ttu-id="91e46-153">또는 toosend 여러 개의 메시지를</span><span class="sxs-lookup"><span data-stu-id="91e46-153">Or, toosend multiple messages,</span></span>

```javascript
module.exports = function(context) {
    var timeStamp = new Date().toISOString();
    var message = 'Event Hub message created at: ' + timeStamp;

    context.bindings.outputEventHubMessage = [];

    context.bindings.outputEventHubMessage.push("1 " + message);
    context.bindings.outputEventHubMessage.push("2 " + message);
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="91e46-154">다음 단계</span><span class="sxs-lookup"><span data-stu-id="91e46-154">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

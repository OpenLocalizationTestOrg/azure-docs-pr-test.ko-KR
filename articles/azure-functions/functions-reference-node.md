---
title: "Azure Functions에 대한 JavaScript 개발자 참조 | Microsoft Docs"
description: "JavaScript를 사용하여 함수를 개발하는 방법을 알아봅니다."
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: "Azure Functions, 함수, 이벤트 처리, webhook, 동적 계산, 서버가 없는 아키텍처"
ms.assetid: 45dedd78-3ff9-411f-bb4b-16d29a11384c
ms.service: functions
ms.devlang: nodejs
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/25/2017
ms.author: glenga
ms.openlocfilehash: 7ea81ed47f391fbce1432c2b11ac176ab6c04ae0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-javascript-developer-guide"></a><span data-ttu-id="e2a02-104">Azure Functions JavaScript 개발자 가이드</span><span class="sxs-lookup"><span data-stu-id="e2a02-104">Azure Functions JavaScript developer guide</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e2a02-105">C# 스크립트</span><span class="sxs-lookup"><span data-stu-id="e2a02-105">C# script</span></span>](functions-reference-csharp.md)
> * [<span data-ttu-id="e2a02-106">F# 스크립트</span><span class="sxs-lookup"><span data-stu-id="e2a02-106">F# script</span></span>](functions-reference-fsharp.md)
> * [<span data-ttu-id="e2a02-107">JavaScript</span><span class="sxs-lookup"><span data-stu-id="e2a02-107">JavaScript</span></span>](functions-reference-node.md)
> 
> 

<span data-ttu-id="e2a02-108">Azure Functions의 JavaScript 환경은 런타임과 통신하고 바인딩을 통해 데이터를 보내고 받는 `context` 개체를 전달하는 함수를 쉽게 내보낼 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-108">The JavaScript experience for Azure Functions makes it easy to export a function, which is passed as a `context` object for communicating with the runtime and for receiving and sending data via bindings.</span></span>

<span data-ttu-id="e2a02-109">이 문서에서는 [Azure Functions 개발자 참조](functions-reference.md)를 이미 읽었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-109">This article assumes that you've already read the [Azure Functions developer reference](functions-reference.md).</span></span>

## <a name="exporting-a-function"></a><span data-ttu-id="e2a02-110">함수 내보내기</span><span class="sxs-lookup"><span data-stu-id="e2a02-110">Exporting a function</span></span>
<span data-ttu-id="e2a02-111">모든 JavaScript 함수는 런타임에 대한 `module.exports`를 통해 단일 `function`을 내보내 함수를 찾고 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-111">All JavaScript functions must export a single `function` via `module.exports` for the runtime to find the function and run it.</span></span> <span data-ttu-id="e2a02-112">이 함수에는 `context` 개체가 항상 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-112">This function must always include a `context` object.</span></span>

```javascript
// You must include a context, but other arguments are optional
module.exports = function(context) {
    // Additional inputs can be accessed by the arguments property
    if(arguments.length === 4) {
        context.log('This function has 4 inputs');
    }
};
// or you can include additional inputs in your arguments
module.exports = function(context, myTrigger, myInput, myOtherInput) {
    // function logic goes here :)
};
```

<span data-ttu-id="e2a02-113">`direction === "in"`의 바인딩은 함수 인수로 전달됩니다. 즉, [`arguments`](https://msdn.microsoft.com/library/87dw3w1k.aspx)를 사용하여 동적으로 새 입력을 처리할 수 있습니다(예: 모든 입력에 대해 반복되는 `arguments.length` 사용).</span><span class="sxs-lookup"><span data-stu-id="e2a02-113">Bindings of `direction === "in"` are passed along as function arguments, which means that you can use [`arguments`](https://msdn.microsoft.com/library/87dw3w1k.aspx) to dynamically handle new inputs (for example, by using `arguments.length` to iterate over all your inputs).</span></span> <span data-ttu-id="e2a02-114">이 기능은 `context` 개체를 참조하지 않고 트리거 데이터에 예측 가능한 방식으로 액세스할 수 있으므로 트리거만 있고 추가 입력이 없는 경우에 편리합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-114">This functionality is convenient when you have only a trigger and no additional inputs, because you can predictably access your trigger data without referencing your `context` object.</span></span>

<span data-ttu-id="e2a02-115">내보내기 문에 인수를 지정하지 않은 경우에도 *function.json*에서 발생하는 순서에 따라 인수가 항상 함수에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-115">The arguments are always passed along to the function in the order in which they occur in *function.json*, even if you don't specify them in your exports statement.</span></span> <span data-ttu-id="e2a02-116">예를 들어 `function(context, a, b)`을 `function(context, a)`으로 변경하는 경우 `arguments[3]`를 참조하여 여전히 함수 코드의 `b` 값을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-116">For example, if you have `function(context, a, b)` and change it to `function(context, a)`, you can still get the value of `b` in function code by referring to `arguments[3]`.</span></span>

<span data-ttu-id="e2a02-117">또한 방향에 관계없이 모든 바인딩은 `context` 개체로 전달됩니다(다음 스크립트 참조).</span><span class="sxs-lookup"><span data-stu-id="e2a02-117">All bindings, regardless of direction, are also passed along on the `context` object (see the following script).</span></span> 

## <a name="context-object"></a><span data-ttu-id="e2a02-118">context 개체</span><span class="sxs-lookup"><span data-stu-id="e2a02-118">context object</span></span>
<span data-ttu-id="e2a02-119">런타임은 함수로 데이터를 전달하거나 전달받으며 사용자가 런타임과 통신할 수 있도록 하는 `context` 개체를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-119">The runtime uses a `context` object to pass data to and from your function and to let you communicate with the runtime.</span></span>

<span data-ttu-id="e2a02-120">context 개체는 항상 함수의 첫 번째 매개 변수이며 런타임을 올바르게 사용하는 데 필요한 `context.done` 및 `context.log`와 같은 메서드를 가지고 있으므로 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-120">The context object is always the first parameter to a function and must be included because it has methods such as `context.done` and `context.log`, which are required to use the runtime correctly.</span></span> <span data-ttu-id="e2a02-121">원하는 개체 이름(예: `ctx` 또는 `c`)을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-121">You can name the object whatever you would like (for example, `ctx` or `c`).</span></span>

```javascript
// You must include a context, but other arguments are optional
module.exports = function(context) {
    // function logic goes here :)
};
```

### <a name="contextbindings-property"></a><span data-ttu-id="e2a02-122">context.bindings 속성</span><span class="sxs-lookup"><span data-stu-id="e2a02-122">context.bindings property</span></span>

```
context.bindings
```
<span data-ttu-id="e2a02-123">모든 입력 및 출력 데이터를 포함하는 명명된 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-123">Returns a named object that contains all your input and output data.</span></span> <span data-ttu-id="e2a02-124">예를 들어 *function.json*의 다음 바인딩 정의를 사용하면 `context.bindings.myInput` 개체에서 큐의 콘텐츠에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-124">For example, the following binding definition in your *function.json* lets you access the contents of the queue from the `context.bindings.myInput` object.</span></span> 

```json
{
    "type":"queue",
    "direction":"in",
    "name":"myInput"
    ...
}
```

```javascript
// myInput contains the input data, which may have properties such as "name"
var author = context.bindings.myInput.name;
// Similarly, you can set your output data
context.bindings.myOutput = { 
        some_text: 'hello world', 
        a_number: 1 };
```

### <a name="contextdone-method"></a><span data-ttu-id="e2a02-125">context.done 메서드</span><span class="sxs-lookup"><span data-stu-id="e2a02-125">context.done method</span></span>
```
context.done([err],[propertyBag])
```

<span data-ttu-id="e2a02-126">코드가 완료되었음을 런타임에 알립니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-126">Informs the runtime that your code has finished.</span></span> <span data-ttu-id="e2a02-127">`context.done`을 호출해야 하나 그렇지 않으면 런타임에서 함수가 완료되었음을 알 수 없으므로 실행 시간이 초과됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-127">You must call `context.done`, or else the runtime never knows that your function is complete, and the execution will time out.</span></span> 

<span data-ttu-id="e2a02-128">`context.done` 메서드를 사용하면 `context.bindings` 개체의 속성을 덮어쓸 속성의 속성 모음뿐만 아니라 사용자 정의 오류도 런타임에 다시 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-128">The `context.done` method allows you to pass back both a user-defined error to the runtime and a property bag of properties that overwrite the properties on the `context.bindings` object.</span></span>

```javascript
// Even though we set myOutput to have:
//  -> text: hello world, number: 123
context.bindings.myOutput = { text: 'hello world', number: 123 };
// If we pass an object to the done function...
context.done(null, { myOutput: { text: 'hello there, world', noNumber: true }});
// the done method will overwrite the myOutput binding to be: 
//  -> text: hello there, world, noNumber: true
```

### <a name="contextlog-method"></a><span data-ttu-id="e2a02-129">context.log 메서드</span><span class="sxs-lookup"><span data-stu-id="e2a02-129">context.log method</span></span>  

```
context.log(message)
```
<span data-ttu-id="e2a02-130">기본 추적 수준에서 스트리밍 콘솔 로그에 기록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-130">Allows you to write to the streaming console logs at the default trace level.</span></span> <span data-ttu-id="e2a02-131">`context.log`에서 다른 추적 수준에서 콘솔 로그에 쓸 수 있는 추가 로깅 메서드가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-131">On `context.log`, additional logging methods are available that let you write to the console log at other trace levels:</span></span>


| <span data-ttu-id="e2a02-132">메서드</span><span class="sxs-lookup"><span data-stu-id="e2a02-132">Method</span></span>                 | <span data-ttu-id="e2a02-133">설명</span><span class="sxs-lookup"><span data-stu-id="e2a02-133">Description</span></span>                                |
| ---------------------- | ------------------------------------------ |
| <span data-ttu-id="e2a02-134">**error(_message_)**</span><span class="sxs-lookup"><span data-stu-id="e2a02-134">**error(_message_)**</span></span>   | <span data-ttu-id="e2a02-135">오류 수준 로깅 또는 더 낮은 수준의 로깅에 씁니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-135">Writes to error level logging, or lower.</span></span>   |
| <span data-ttu-id="e2a02-136">**warn(_message_)**</span><span class="sxs-lookup"><span data-stu-id="e2a02-136">**warn(_message_)**</span></span>    | <span data-ttu-id="e2a02-137">경고 수준 로깅 또는 더 낮은 수준의 로깅에 씁니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-137">Writes to warning level logging, or lower.</span></span> |
| <span data-ttu-id="e2a02-138">**info(_message_)**</span><span class="sxs-lookup"><span data-stu-id="e2a02-138">**info(_message_)**</span></span>    | <span data-ttu-id="e2a02-139">정보 수준 로깅 또는 더 낮은 수준의 로깅에 씁니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-139">Writes to info level logging, or lower.</span></span>    |
| <span data-ttu-id="e2a02-140">**verbose(_message_)**</span><span class="sxs-lookup"><span data-stu-id="e2a02-140">**verbose(_message_)**</span></span> | <span data-ttu-id="e2a02-141">자세한 정보 표시 수준 로깅에 씁니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-141">Writes to verbose level logging.</span></span>           |

<span data-ttu-id="e2a02-142">다음 예제는 경고 추적 수준에서 콘솔에 씁니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-142">The following example writes to the console at the warning trace level:</span></span>

```javascript
context.log.warn("Something has happened."); 
```
<span data-ttu-id="e2a02-143">host.json 파일에 로그인하기 위한 추적 수준 임계값을 설정하거나 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-143">You can set the trace-level threshold for logging in the host.json file, or turn it off.</span></span>  <span data-ttu-id="e2a02-144">로그에 쓰는 방법에 대한 자세한 내용은 다음 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e2a02-144">For more information about how to write to the logs, see the next section.</span></span>

## <a name="binding-data-type"></a><span data-ttu-id="e2a02-145">바인딩 데이터 형식</span><span class="sxs-lookup"><span data-stu-id="e2a02-145">Binding data type</span></span>

<span data-ttu-id="e2a02-146">입력 바인딩에 대한 데이터 형식을 정의하려면 바인딩 정의에서 `dataType` 속성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-146">To define the data type for an input binding, use the `dataType` property in the binding definition.</span></span> <span data-ttu-id="e2a02-147">예를 들어 이진 형식의 HTTP 요청 내용을 읽으려면 `binary` 형식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-147">For example, to read the content of an HTTP request in binary format, use the type `binary`:</span></span>

```json
{
    "type": "httpTrigger",
    "name": "req",
    "direction": "in",
    "dataType": "binary"
}
```

<span data-ttu-id="e2a02-148">`dataType`에 대한 다른 옵션은 `stream` 및 `string`입니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-148">Other options for `dataType` are `stream` and `string`.</span></span>

## <a name="writing-trace-output-to-the-console"></a><span data-ttu-id="e2a02-149">콘솔에 추적 출력 작성</span><span class="sxs-lookup"><span data-stu-id="e2a02-149">Writing trace output to the console</span></span> 

<span data-ttu-id="e2a02-150">Functions에서 `context.log` 메서드를 사용하여 추적 출력을 콘솔에 씁니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-150">In Functions, you use the `context.log` methods to write trace output to the console.</span></span> <span data-ttu-id="e2a02-151">이 시점에서는 `console.log`를 사용하여 콘솔에 쓸 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-151">At this point, you cannot use `console.log` to write to the console.</span></span>

<span data-ttu-id="e2a02-152">`context.log()`를 호출하면 메시지를 _정보_ 추적 수준인 기본 추적 수준에서 콘솔에 씁니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-152">When you call `context.log()`, your message is written to the console at the default trace level, which is the _info_ trace level.</span></span> <span data-ttu-id="e2a02-153">다음 코드는 정보 추적 수준에서 콘솔에 씁니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-153">The following code writes to the console at the info trace level:</span></span>

```javascript
context.log({hello: 'world'});  
```

<span data-ttu-id="e2a02-154">이전 코드는 다음 코드와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-154">The preceding code is equivalent to the following code:</span></span>

```javascript
context.log.info({hello: 'world'});  
```

<span data-ttu-id="e2a02-155">다음 코드는 오류 수준에서 콘솔에 씁니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-155">The following code writes to the console at the error level:</span></span>

```javascript
context.log.error("An error has occurred.");  
```

<span data-ttu-id="e2a02-156">_error_(오류)가 가장 높은 추적 수준이므로 로깅이 활성화되어 있는 한 이 추적은 모든 추적 수준에서 출력에 씁니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-156">Because _error_ is the highest trace level, this trace is written to the output at all trace levels as long as logging is enabled.</span></span>  


<span data-ttu-id="e2a02-157">모든 `context.log` 메서드는 Node.js [util.format 메서드](https://nodejs.org/api/util.html#util_util_format_format)에서 지원하는 것과 동일한 매개 변수 형식을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-157">All `context.log` methods support the same parameter format that's supported by the Node.js [util.format method](https://nodejs.org/api/util.html#util_util_format_format).</span></span> <span data-ttu-id="e2a02-158">기본 추적 수준을 사용하여 콘솔에 쓰는 다음 코드를 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="e2a02-158">Consider the following code, which writes to the console by using the default trace level:</span></span>

```javascript
context.log('Node.js HTTP trigger function processed a request. RequestUri=' + req.originalUrl);
context.log('Request Headers = ' + JSON.stringify(req.headers));
```

<span data-ttu-id="e2a02-159">또한 동일한 코드를 다음과 같은 형식으로 작성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-159">You can also write the same code in the following format:</span></span>

```javascript
context.log('Node.js HTTP trigger function processed a request. RequestUri=%s', req.originalUrl);
context.log('Request Headers = ', JSON.stringify(req.headers));
```

### <a name="configure-the-trace-level-for-console-logging"></a><span data-ttu-id="e2a02-160">콘솔 로깅에 대한 추적 수준 구성</span><span class="sxs-lookup"><span data-stu-id="e2a02-160">Configure the trace level for console logging</span></span>

<span data-ttu-id="e2a02-161">Functions를 통해 콘솔에 쓸 임계값 추적 수준을 정의할 수 있으므로 추적을 함수에서 콘솔로 쓰는 방식을 쉽게 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-161">Functions lets you define the threshold trace level for writing to the console, which makes it easy to control the way traces are written to the console from your functions.</span></span> <span data-ttu-id="e2a02-162">콘솔에 기록되는 모든 추적에 대한 임계값을 설정하려면 host.json 파일의 `tracing.consoleLevel` 속성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-162">To set the threshold for all traces written to the console, use the `tracing.consoleLevel` property in the host.json file.</span></span> <span data-ttu-id="e2a02-163">이 설정은 함수 앱의 모든 함수에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-163">This setting applies to all functions in your function app.</span></span> <span data-ttu-id="e2a02-164">다음 예제에서는 추적 임계값을 설정하여 자세한 정보 표시 로깅을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-164">The following example sets the trace threshold to enable verbose logging:</span></span>

```json
{ 
    "tracing": {      
        "consoleLevel": "verbose"     
    }
}  
```

<span data-ttu-id="e2a02-165">**consoleLevel**의 값은 `context.log` 메서드의 이름에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-165">Values of **consoleLevel** correspond to the names of the `context.log` methods.</span></span> <span data-ttu-id="e2a02-166">콘솔에 대한 모든 추적 로깅을 사용하지 않으려면 **consoleLevel**을 _off_로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-166">To disable all trace logging to the console, set **consoleLevel** to _off_.</span></span> <span data-ttu-id="e2a02-167">host.json 파일에 대한 자세한 내용은 [host.json 참조 항목](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json)(영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e2a02-167">For more information about the host.json file, see the [host.json reference topic](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span>

## <a name="http-triggers-and-bindings"></a><span data-ttu-id="e2a02-168">HTTP 트리거 및 바인딩</span><span class="sxs-lookup"><span data-stu-id="e2a02-168">HTTP triggers and bindings</span></span>

<span data-ttu-id="e2a02-169">HTTP, 웹후크 트리거 및 HTTP 출력 바인딩은 요청 및 응답 개체를 사용하여 HTTP 메시지를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-169">HTTP and webhook triggers and HTTP output bindings use request and response objects to represent the HTTP messaging.</span></span>  

### <a name="request-object"></a><span data-ttu-id="e2a02-170">요청 개체</span><span class="sxs-lookup"><span data-stu-id="e2a02-170">Request object</span></span>

<span data-ttu-id="e2a02-171">`request` 개체의 속성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-171">The `request` object has the following properties:</span></span>

| <span data-ttu-id="e2a02-172">속성</span><span class="sxs-lookup"><span data-stu-id="e2a02-172">Property</span></span>      | <span data-ttu-id="e2a02-173">설명</span><span class="sxs-lookup"><span data-stu-id="e2a02-173">Description</span></span>                                                    |
| ------------- | -------------------------------------------------------------- |
| <span data-ttu-id="e2a02-174">_body_</span><span class="sxs-lookup"><span data-stu-id="e2a02-174">_body_</span></span>        | <span data-ttu-id="e2a02-175">요청의 본문을 포함하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-175">An object that contains the body of the request.</span></span>               |
| <span data-ttu-id="e2a02-176">_headers_</span><span class="sxs-lookup"><span data-stu-id="e2a02-176">_headers_</span></span>     | <span data-ttu-id="e2a02-177">요청 헤더를 포함하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-177">An object that contains the request headers.</span></span>                   |
| <span data-ttu-id="e2a02-178">_method_</span><span class="sxs-lookup"><span data-stu-id="e2a02-178">_method_</span></span>      | <span data-ttu-id="e2a02-179">요청의 HTTP 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-179">The HTTP method of the request.</span></span>                                |
| <span data-ttu-id="e2a02-180">_originalUrl_</span><span class="sxs-lookup"><span data-stu-id="e2a02-180">_originalUrl_</span></span> | <span data-ttu-id="e2a02-181">요청의 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-181">The URL of the request.</span></span>                                        |
| <span data-ttu-id="e2a02-182">_params_</span><span class="sxs-lookup"><span data-stu-id="e2a02-182">_params_</span></span>      | <span data-ttu-id="e2a02-183">요청의 라우팅 매개 변수를 포함하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-183">An object that contains the routing parameters of the request.</span></span> |
| <span data-ttu-id="e2a02-184">_query_</span><span class="sxs-lookup"><span data-stu-id="e2a02-184">_query_</span></span>       | <span data-ttu-id="e2a02-185">쿼리 매개 변수를 포함하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-185">An object that contains the query parameters.</span></span>                  |
| <span data-ttu-id="e2a02-186">_rawBody_</span><span class="sxs-lookup"><span data-stu-id="e2a02-186">_rawBody_</span></span>     | <span data-ttu-id="e2a02-187">문자열 형식의 메시지 본문입니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-187">The body of the message as a string.</span></span>                           |


### <a name="response-object"></a><span data-ttu-id="e2a02-188">응답 개체</span><span class="sxs-lookup"><span data-stu-id="e2a02-188">Response object</span></span>

<span data-ttu-id="e2a02-189">`response` 개체의 속성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-189">The `response` object has the following properties:</span></span>

| <span data-ttu-id="e2a02-190">속성</span><span class="sxs-lookup"><span data-stu-id="e2a02-190">Property</span></span>  | <span data-ttu-id="e2a02-191">설명</span><span class="sxs-lookup"><span data-stu-id="e2a02-191">Description</span></span>                                               |
| --------- | --------------------------------------------------------- |
| <span data-ttu-id="e2a02-192">_body_</span><span class="sxs-lookup"><span data-stu-id="e2a02-192">_body_</span></span>    | <span data-ttu-id="e2a02-193">응답의 본문을 포함하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-193">An object that contains the body of the response.</span></span>         |
| <span data-ttu-id="e2a02-194">_headers_</span><span class="sxs-lookup"><span data-stu-id="e2a02-194">_headers_</span></span> | <span data-ttu-id="e2a02-195">응답 헤더를 포함하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-195">An object that contains the response headers.</span></span>             |
| <span data-ttu-id="e2a02-196">_isRaw_</span><span class="sxs-lookup"><span data-stu-id="e2a02-196">_isRaw_</span></span>   | <span data-ttu-id="e2a02-197">응답에 대한 서식 지정을 건너뜀을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-197">Indicates that formatting is skipped for the response.</span></span>    |
| <span data-ttu-id="e2a02-198">_상태_</span><span class="sxs-lookup"><span data-stu-id="e2a02-198">_status_</span></span>  | <span data-ttu-id="e2a02-199">응답의 HTTP 상태 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-199">The HTTP status code of the response.</span></span>                     |

### <a name="accessing-the-request-and-response"></a><span data-ttu-id="e2a02-200">요청 및 응답 액세스</span><span class="sxs-lookup"><span data-stu-id="e2a02-200">Accessing the request and response</span></span> 

<span data-ttu-id="e2a02-201">HTTP 트리거로 작업할 때 세 가지 방법으로 HTTP 요청 및 응답 개체에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-201">When you work with HTTP triggers, you can access the HTTP request and response objects in any of three ways:</span></span>

+ <span data-ttu-id="e2a02-202">명명된 입출력 바인딩에서.</span><span class="sxs-lookup"><span data-stu-id="e2a02-202">From the named input and output bindings.</span></span> <span data-ttu-id="e2a02-203">이러한 방식으로 HTTP 트리거와 바인딩은 다른 바인딩과 동일하게 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-203">In this way, the HTTP trigger and bindings work the same as any other binding.</span></span> <span data-ttu-id="e2a02-204">다음 예제에서는 명명된 `response` 바인딩을 사용하여 응답 개체를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-204">The following example sets the response object by using a named `response` binding:</span></span> 

    ```javascript
    context.bindings.response = { status: 201, body: "Insert succeeded." };
    ```

+ <span data-ttu-id="e2a02-205">`context` 개체의 `req` 및 `res` 속성에서.</span><span class="sxs-lookup"><span data-stu-id="e2a02-205">From `req` and `res` properties on the `context` object.</span></span> <span data-ttu-id="e2a02-206">이러한 방식으로 전체 `context.bindings.name` 패턴을 사용하지 않고 대신 기존 패턴을 사용하여 context 개체에서 HTTP 데이터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-206">In this way, you can use the conventional pattern to access HTTP data from the context object, instead of having to use the full `context.bindings.name` pattern.</span></span> <span data-ttu-id="e2a02-207">다음 예제에서는 `context`의 `req` 및 `res` 개체에 액세스하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-207">The following example shows how to access the `req` and `res` objects on the `context`:</span></span>

    ```javascript
    // You can access your http request off the context ...
    if(context.req.body.emoji === ':pizza:') context.log('Yay!');
    // and also set your http response
    context.res = { status: 202, body: 'You successfully ordered more coffee!' }; 
    ```

+ <span data-ttu-id="e2a02-208">`context.done()`을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-208">By calling `context.done()`.</span></span> <span data-ttu-id="e2a02-209">`context.done()` 메서드에 전달되는 응답을 반환하는 특별한 종류의 HTTP 바인딩이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-209">A special kind of HTTP binding returns the response that is passed to the `context.done()` method.</span></span> <span data-ttu-id="e2a02-210">다음 HTTP 출력 바인딩은 `$return` 출력 매개 변수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-210">The following HTTP output binding defines a `$return` output parameter:</span></span>

    ```json
    {
      "type": "http",
      "direction": "out",
      "name": "$return"
    }
    ``` 
    <span data-ttu-id="e2a02-211">이 출력 바인딩은 다음과 같이 `done()`을 호출할 때 응답을 제공할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-211">This output binding expects you to supply the response when you call `done()`, as follows:</span></span>

    ```javascript
     // Define a valid response object.
    res = { status: 201, body: "Insert succeeded." };
    context.done(null, res);   
    ```  

## <a name="node-version-and-package-management"></a><span data-ttu-id="e2a02-212">노드 버전 및 패키지 관리</span><span class="sxs-lookup"><span data-stu-id="e2a02-212">Node version and Package Management</span></span>
<span data-ttu-id="e2a02-213">노드 버전이 현재 `6.5.0`에서 잠겨 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-213">The node version is currently locked at `6.5.0`.</span></span> <span data-ttu-id="e2a02-214">더 많은 버전에 대한 지원을 추가하고 구성할 수 있도록 연구 중입니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-214">We're investigating adding support for more versions and making it configurable.</span></span>

<span data-ttu-id="e2a02-215">다음 단계를 사용하면 함수 앱에 패키지를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-215">The following steps let you include packages in your function app:</span></span> 

1. <span data-ttu-id="e2a02-216">`https://<function_app_name>.scm.azurewebsites.net`로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-216">Go to `https://<function_app_name>.scm.azurewebsites.net`.</span></span>

2. <span data-ttu-id="e2a02-217">**디버그 콘솔** > **CMD**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-217">Click **Debug Console** > **CMD**.</span></span>

3. <span data-ttu-id="e2a02-218">`D:\home\site\wwwroot`로 이동한 다음 package.json 파일을 페이지 위쪽의 **wwwroot** 폴더로 끌어갑니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-218">Go to `D:\home\site\wwwroot`, and then drag your package.json file to the **wwwroot** folder at the top half of the page.</span></span>  
    <span data-ttu-id="e2a02-219">다른 방법으로 함수 앱에 파일을 업로드할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-219">You can upload files to your function app in other ways also.</span></span> <span data-ttu-id="e2a02-220">자세한 내용은 [함수 앱 파일을 업데이트하는 방법](functions-reference.md#fileupdate)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e2a02-220">For more information, see [How to update function app files](functions-reference.md#fileupdate).</span></span> 

4. <span data-ttu-id="e2a02-221">package.json 파일을 업로드한 후 **Kudu 원격 실행 콘솔**에서 `npm install` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-221">After the package.json file is uploaded, run the `npm install` command in the **Kudu remote execution console**.</span></span>  
    <span data-ttu-id="e2a02-222">이 작업은 package.json 파일에 표시된 패키지를 다운로드하고 함수 앱을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-222">This action downloads the packages indicated in the package.json file and restarts the function app.</span></span>

<span data-ttu-id="e2a02-223">필요한 패키지가 설치되면 다음 예제와 같이 `require('packagename')`을 호출하여 함수로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-223">After the packages you need are installed, you import them to your function by calling `require('packagename')`, as in the following example:</span></span>

```javascript
// Import the underscore.js library
var _ = require('underscore');
var version = process.version; // version === 'v6.5.0'

module.exports = function(context) {
    // Using our imported underscore.js library
    var matched_names = _
        .where(context.bindings.myInput.names, {first: 'Carla'});
```

<span data-ttu-id="e2a02-224">함수 앱의 루트에 `package.json` 파일을 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-224">You should define a `package.json` file at the root of your function app.</span></span> <span data-ttu-id="e2a02-225">파일을 정의하면 앱의 모든 함수에서 동일한 캐시된 패키지를 공유할 수 있으므로 최상의 성능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-225">Defining the file lets all functions in the app share the same cached packages, which gives the best performance.</span></span> <span data-ttu-id="e2a02-226">버전 충돌이 발생하는 경우 특정 함수의 폴더에 `package.json` 파일을 추가하여 이 충돌을 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-226">If a version conflict arises, you can resolve it by adding a `package.json` file in the folder of a specific function.</span></span>  

## <a name="environment-variables"></a><span data-ttu-id="e2a02-227">환경 변수</span><span class="sxs-lookup"><span data-stu-id="e2a02-227">Environment variables</span></span>
<span data-ttu-id="e2a02-228">환경 변수 또는 앱 설정 값을 가져오려면 다음 코드 예제와 같이 `process.env`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-228">To get an environment variable or an app setting value, use `process.env`, as shown in the following code example:</span></span>

```javascript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();

    context.log('Node.js timer trigger function ran!', timeStamp);   
    context.log(GetEnvironmentVariable("AzureWebJobsStorage"));
    context.log(GetEnvironmentVariable("WEBSITE_SITE_NAME"));

    context.done();
};

function GetEnvironmentVariable(name)
{
    return name + ": " + process.env[name];
}
```
## <a name="considerations-for-javascript-functions"></a><span data-ttu-id="e2a02-229">JavaScript 함수에 대한 고려 사항</span><span class="sxs-lookup"><span data-stu-id="e2a02-229">Considerations for JavaScript functions</span></span>

<span data-ttu-id="e2a02-230">JavaScript 함수로 작업하는 경우 다음 두 섹션에서 고려 사항을 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-230">When you work with JavaScript functions, be aware of the considerations in the following two sections.</span></span>

### <a name="choose-single-core-app-service-plans"></a><span data-ttu-id="e2a02-231">단일 코어 App Service 계획 선택</span><span class="sxs-lookup"><span data-stu-id="e2a02-231">Choose single-core App Service plans</span></span>

<span data-ttu-id="e2a02-232">App Service 계획을 사용하는 함수 앱을 만들 때 여러 코어가 있는 계획보다는 단일 코어 계획을 선택하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-232">When you create a function app that uses the App Service plan, we recommend that you select a single-core plan rather than a plan with multiple cores.</span></span> <span data-ttu-id="e2a02-233">현재 Functions는 단일 코어 VM에서 JavaScript 함수를 더 효율적으로 실행합니다. 더 큰 VM을 사용하면 예상된 성능 향상을 보여 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-233">Today, Functions runs JavaScript functions more efficiently on single-core VMs, and using larger VMs does not produce the expected performance improvements.</span></span> <span data-ttu-id="e2a02-234">필요한 경우 더 많은 단일 코어 VM 인스턴스를 추가하여 수동으로 확장하거나 자동 크기 조정을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-234">When necessary, you can manually scale out by adding more single-core VM instances, or you can enable auto-scale.</span></span> <span data-ttu-id="e2a02-235">자세한 내용은 [수동 또는 자동으로 인스턴스 개수 조정](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e2a02-235">For more information, see [Scale instance count manually or automatically](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json).</span></span>    

### <a name="typescript-and-coffeescript-support"></a><span data-ttu-id="e2a02-236">TypeScript 및 CoffeeScript 지원</span><span class="sxs-lookup"><span data-stu-id="e2a02-236">TypeScript and CoffeeScript support</span></span>
<span data-ttu-id="e2a02-237">아직 런타임을 통해 TypeScript 또는 CoffeeScript 자동 컴파일에 대한 직접 지원이 없으므로 배포 시 런타임 외부에서 이러한 지원이 처리되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a02-237">Because direct support does not yet exist for auto-compiling TypeScript or CoffeeScript via the runtime, such support needs to be handled outside the runtime, at deployment time.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="e2a02-238">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e2a02-238">Next steps</span></span>
<span data-ttu-id="e2a02-239">자세한 내용은 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e2a02-239">For more information, see the following resources:</span></span>

* [<span data-ttu-id="e2a02-240">Azure Functions에 대한 모범 사례</span><span class="sxs-lookup"><span data-stu-id="e2a02-240">Best practices for Azure Functions</span></span>](functions-best-practices.md)
* [<span data-ttu-id="e2a02-241">Azure Functions 개발자 참조</span><span class="sxs-lookup"><span data-stu-id="e2a02-241">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="e2a02-242">Azure Functions C# 개발자 참조</span><span class="sxs-lookup"><span data-stu-id="e2a02-242">Azure Functions C# developer reference</span></span>](functions-reference-csharp.md)
* [<span data-ttu-id="e2a02-243">Azure Functions F# 개발자 참조</span><span class="sxs-lookup"><span data-stu-id="e2a02-243">Azure Functions F# developer reference</span></span>](functions-reference-fsharp.md)
* [<span data-ttu-id="e2a02-244">Azure Functions 트리거 및 바인딩</span><span class="sxs-lookup"><span data-stu-id="e2a02-244">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)


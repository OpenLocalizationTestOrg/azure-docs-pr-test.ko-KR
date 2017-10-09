---
title: "Azure 함수에 대 한 aaaJavaScript 개발자 참조 | Microsoft Docs"
description: "JavaScript를 사용 하 여 toodevelop 작동 하는 방식을 이해 합니다."
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
ms.openlocfilehash: 6220b42f965b6ee2463341aaf270836623fdf7fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-javascript-developer-guide"></a><span data-ttu-id="8f2af-104">Azure Functions JavaScript 개발자 가이드</span><span class="sxs-lookup"><span data-stu-id="8f2af-104">Azure Functions JavaScript developer guide</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8f2af-105">C# 스크립트</span><span class="sxs-lookup"><span data-stu-id="8f2af-105">C# script</span></span>](functions-reference-csharp.md)
> * [<span data-ttu-id="8f2af-106">F# 스크립트</span><span class="sxs-lookup"><span data-stu-id="8f2af-106">F# script</span></span>](functions-reference-fsharp.md)
> * [<span data-ttu-id="8f2af-107">JavaScript</span><span class="sxs-lookup"><span data-stu-id="8f2af-107">JavaScript</span></span>](functions-reference-node.md)
> 
> 

<span data-ttu-id="8f2af-108">Azure 함수 쉽게 tooexport 변수로 전달 되는 함수를 사용 하면에 대 한 JavaScript 경험 hello는 `context` hello 런타임와의 통신에 대 한 데이터 바인딩을 통해 전송 및 수신 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-108">hello JavaScript experience for Azure Functions makes it easy tooexport a function, which is passed as a `context` object for communicating with hello runtime and for receiving and sending data via bindings.</span></span>

<span data-ttu-id="8f2af-109">이 문서에서는 hello 이미 읽어본 가정 [Azure 함수 개발자 참조](functions-reference.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-109">This article assumes that you've already read hello [Azure Functions developer reference](functions-reference.md).</span></span>

## <a name="exporting-a-function"></a><span data-ttu-id="8f2af-110">함수 내보내기</span><span class="sxs-lookup"><span data-stu-id="8f2af-110">Exporting a function</span></span>
<span data-ttu-id="8f2af-111">모든 JavaScript 함수는 단일 내보내야 `function` 통해 `module.exports` hello 런타임용 toofind 함수 hello 하 고 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-111">All JavaScript functions must export a single `function` via `module.exports` for hello runtime toofind hello function and run it.</span></span> <span data-ttu-id="8f2af-112">이 함수에는 `context` 개체가 항상 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-112">This function must always include a `context` object.</span></span>

```javascript
// You must include a context, but other arguments are optional
module.exports = function(context) {
    // Additional inputs can be accessed by hello arguments property
    if(arguments.length === 4) {
        context.log('This function has 4 inputs');
    }
};
// or you can include additional inputs in your arguments
module.exports = function(context, myTrigger, myInput, myOtherInput) {
    // function logic goes here :)
};
```

<span data-ttu-id="8f2af-113">바인딩 `direction === "in"` 있습니다 사용할 수 있다는 의미 이므로 함수 인수로 전달 됩니다 [ `arguments` ](https://msdn.microsoft.com/library/87dw3w1k.aspx) toodynamically 새로운 입력 처리 (사용 하 여 예를 들어 `arguments.length` tooiterate 모든 입력을 통해).</span><span class="sxs-lookup"><span data-stu-id="8f2af-113">Bindings of `direction === "in"` are passed along as function arguments, which means that you can use [`arguments`](https://msdn.microsoft.com/library/87dw3w1k.aspx) toodynamically handle new inputs (for example, by using `arguments.length` tooiterate over all your inputs).</span></span> <span data-ttu-id="8f2af-114">이 기능은 `context` 개체를 참조하지 않고 트리거 데이터에 예측 가능한 방식으로 액세스할 수 있으므로 트리거만 있고 추가 입력이 없는 경우에 편리합니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-114">This functionality is convenient when you have only a trigger and no additional inputs, because you can predictably access your trigger data without referencing your `context` object.</span></span>

<span data-ttu-id="8f2af-115">hello 인수는 항상 toohello 함수에서 발생 하는 hello 순서에 따라 전달 *function.json*내보내기 문에 지정 하지 않으면 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-115">hello arguments are always passed along toohello function in hello order in which they occur in *function.json*, even if you don't specify them in your exports statement.</span></span> <span data-ttu-id="8f2af-116">예를 들어 `function(context, a, b)` 너무 변경`function(context, a)`, hello 값을 가져올 수 있습니다 `b` 너무 참조 하 여 함수 코드에서`arguments[3]`합니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-116">For example, if you have `function(context, a, b)` and change it too`function(context, a)`, you can still get hello value of `b` in function code by referring too`arguments[3]`.</span></span>

<span data-ttu-id="8f2af-117">방향에 관계 없이 모든 바인딩은 hello에 따라 전송 되도 `context` 개체 (hello 다음 스크립트 참조).</span><span class="sxs-lookup"><span data-stu-id="8f2af-117">All bindings, regardless of direction, are also passed along on hello `context` object (see hello following script).</span></span> 

## <a name="context-object"></a><span data-ttu-id="8f2af-118">context 개체</span><span class="sxs-lookup"><span data-stu-id="8f2af-118">context object</span></span>
<span data-ttu-id="8f2af-119">hello 런타임에서 사용 하 여 한 `context` 개체 toopass 데이터 tooand 함수 및 toolet hello 런타임과 통신 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-119">hello runtime uses a `context` object toopass data tooand from your function and toolet you communicate with hello runtime.</span></span>

<span data-ttu-id="8f2af-120">hello 컨텍스트 개체는 항상 첫 번째 매개 변수 tooa 함수 hello 및 메서드를 같은 있기 때문에 포함 되어야 합니다 `context.done` 및 `context.log`, 필요한 toouse hello 런타임을 올바르게 않는 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-120">hello context object is always hello first parameter tooa function and must be included because it has methods such as `context.done` and `context.log`, which are required toouse hello runtime correctly.</span></span> <span data-ttu-id="8f2af-121">원하는 대로 지정 hello 개체 이름을 지정할 수 있습니다 (예를 들어 `ctx` 또는 `c`).</span><span class="sxs-lookup"><span data-stu-id="8f2af-121">You can name hello object whatever you would like (for example, `ctx` or `c`).</span></span>

```javascript
// You must include a context, but other arguments are optional
module.exports = function(context) {
    // function logic goes here :)
};
```

### <a name="contextbindings-property"></a><span data-ttu-id="8f2af-122">context.bindings 속성</span><span class="sxs-lookup"><span data-stu-id="8f2af-122">context.bindings property</span></span>

```
context.bindings
```
<span data-ttu-id="8f2af-123">모든 입력 및 출력 데이터를 포함하는 명명된 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-123">Returns a named object that contains all your input and output data.</span></span> <span data-ttu-id="8f2af-124">예를 들어 다음 바인딩 정의 hello 프로그램 *function.json* 액세스할 수 있습니다 hello hello에서 hello 큐의 내용을 `context.bindings.myInput` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-124">For example, hello following binding definition in your *function.json* lets you access hello contents of hello queue from hello `context.bindings.myInput` object.</span></span> 

```json
{
    "type":"queue",
    "direction":"in",
    "name":"myInput"
    ...
}
```

```javascript
// myInput contains hello input data, which may have properties such as "name"
var author = context.bindings.myInput.name;
// Similarly, you can set your output data
context.bindings.myOutput = { 
        some_text: 'hello world', 
        a_number: 1 };
```

### <a name="contextdone-method"></a><span data-ttu-id="8f2af-125">context.done 메서드</span><span class="sxs-lookup"><span data-stu-id="8f2af-125">context.done method</span></span>
```
context.done([err],[propertyBag])
```

<span data-ttu-id="8f2af-126">Hello 런타임을 코드 완료 되었음을 알립니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-126">Informs hello runtime that your code has finished.</span></span> <span data-ttu-id="8f2af-127">호출 해야 `context.done`, 또는 다른 hello 런타임 모릅니다 함수가 완료 되 고 hello 실행 시간이 초과 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-127">You must call `context.done`, or else hello runtime never knows that your function is complete, and hello execution will time out.</span></span> 

<span data-ttu-id="8f2af-128">hello `context.done` 메서드를 사용 하면 toopass 백업 하는 사용자 정의 오류 toohello 런타임과 hello에 hello 속성을 덮어쓸 수 있는 속성의 속성 모음은 `context.bindings` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-128">hello `context.done` method allows you toopass back both a user-defined error toohello runtime and a property bag of properties that overwrite hello properties on hello `context.bindings` object.</span></span>

```javascript
// Even though we set myOutput toohave:
//  -> text: hello world, number: 123
context.bindings.myOutput = { text: 'hello world', number: 123 };
// If we pass an object toohello done function...
context.done(null, { myOutput: { text: 'hello there, world', noNumber: true }});
// hello done method will overwrite hello myOutput binding toobe: 
//  -> text: hello there, world, noNumber: true
```

### <a name="contextlog-method"></a><span data-ttu-id="8f2af-129">context.log 메서드</span><span class="sxs-lookup"><span data-stu-id="8f2af-129">context.log method</span></span>  

```
context.log(message)
```
<span data-ttu-id="8f2af-130">Hello 기본 추적 수준의 toowrite toohello 스트리밍 콘솔 로그 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-130">Allows you toowrite toohello streaming console logs at hello default trace level.</span></span> <span data-ttu-id="8f2af-131">`context.log`추가 로깅이 메서드, 다른 추적 수준 toohello 콘솔 로그를 작성할 수 있는 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-131">On `context.log`, additional logging methods are available that let you write toohello console log at other trace levels:</span></span>


| <span data-ttu-id="8f2af-132">메서드</span><span class="sxs-lookup"><span data-stu-id="8f2af-132">Method</span></span>                 | <span data-ttu-id="8f2af-133">설명</span><span class="sxs-lookup"><span data-stu-id="8f2af-133">Description</span></span>                                |
| ---------------------- | ------------------------------------------ |
| <span data-ttu-id="8f2af-134">**error(_message_)**</span><span class="sxs-lookup"><span data-stu-id="8f2af-134">**error(_message_)**</span></span>   | <span data-ttu-id="8f2af-135">Tooerror 수준을 로깅, 또는 더 낮은 씁니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-135">Writes tooerror level logging, or lower.</span></span>   |
| <span data-ttu-id="8f2af-136">**warn(_message_)**</span><span class="sxs-lookup"><span data-stu-id="8f2af-136">**warn(_message_)**</span></span>    | <span data-ttu-id="8f2af-137">Toowarning 수준을 로깅, 또는 더 낮은 씁니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-137">Writes toowarning level logging, or lower.</span></span> |
| <span data-ttu-id="8f2af-138">**info(_message_)**</span><span class="sxs-lookup"><span data-stu-id="8f2af-138">**info(_message_)**</span></span>    | <span data-ttu-id="8f2af-139">Tooinfo 수준을 로깅, 또는 더 낮은 씁니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-139">Writes tooinfo level logging, or lower.</span></span>    |
| <span data-ttu-id="8f2af-140">**verbose(_message_)**</span><span class="sxs-lookup"><span data-stu-id="8f2af-140">**verbose(_message_)**</span></span> | <span data-ttu-id="8f2af-141">Tooverbose 수준 로깅을 씁니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-141">Writes tooverbose level logging.</span></span>           |

<span data-ttu-id="8f2af-142">hello 다음 예제에서는 기록 hello 경고 추적 수준에서 toohello 콘솔:</span><span class="sxs-lookup"><span data-stu-id="8f2af-142">hello following example writes toohello console at hello warning trace level:</span></span>

```javascript
context.log.warn("Something has happened."); 
```
<span data-ttu-id="8f2af-143">Hello host.json 파일에서 로그인을 위한 hello 추적 수준이 임계값을 설정 하거나 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-143">You can set hello trace-level threshold for logging in hello host.json file, or turn it off.</span></span>  <span data-ttu-id="8f2af-144">Toowrite toohello 기록 하는 방법에 대 한 자세한 내용은 hello 다음 섹션을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="8f2af-144">For more information about how toowrite toohello logs, see hello next section.</span></span>

## <a name="binding-data-type"></a><span data-ttu-id="8f2af-145">바인딩 데이터 형식</span><span class="sxs-lookup"><span data-stu-id="8f2af-145">Binding data type</span></span>

<span data-ttu-id="8f2af-146">toodefine hello 데이터 형식 입력 바인딩의 경우 hello를 사용 하 여 `dataType` hello 바인딩 정의에 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-146">toodefine hello data type for an input binding, use hello `dataType` property in hello binding definition.</span></span> <span data-ttu-id="8f2af-147">예를 들어 tooread hello 이진 형식으로 HTTP 요청 콘텐츠 형식을 사용 하십시오 hello `binary`:</span><span class="sxs-lookup"><span data-stu-id="8f2af-147">For example, tooread hello content of an HTTP request in binary format, use hello type `binary`:</span></span>

```json
{
    "type": "httpTrigger",
    "name": "req",
    "direction": "in",
    "dataType": "binary"
}
```

<span data-ttu-id="8f2af-148">`dataType`에 대한 다른 옵션은 `stream` 및 `string`입니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-148">Other options for `dataType` are `stream` and `string`.</span></span>

## <a name="writing-trace-output-toohello-console"></a><span data-ttu-id="8f2af-149">쓰기 추적 출력 toohello 콘솔</span><span class="sxs-lookup"><span data-stu-id="8f2af-149">Writing trace output toohello console</span></span> 

<span data-ttu-id="8f2af-150">함수를 사용 하 여 hello `context.log` 메서드 toowrite 추적 출력 toohello 콘솔.</span><span class="sxs-lookup"><span data-stu-id="8f2af-150">In Functions, you use hello `context.log` methods toowrite trace output toohello console.</span></span> <span data-ttu-id="8f2af-151">이 시점에서 사용할 수 없습니다 `console.log` toowrite toohello 콘솔.</span><span class="sxs-lookup"><span data-stu-id="8f2af-151">At this point, you cannot use `console.log` toowrite toohello console.</span></span>

<span data-ttu-id="8f2af-152">호출 하는 경우 `context.log()`, 메시지는 hello는 hello 기본 추적 수준 toohello 콘솔 쓰여집니다 _정보_ 추적 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-152">When you call `context.log()`, your message is written toohello console at hello default trace level, which is hello _info_ trace level.</span></span> <span data-ttu-id="8f2af-153">hello 다음 코드를 작성 hello 정보 추적 수준에서 toohello 콘솔 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-153">hello following code writes toohello console at hello info trace level:</span></span>

```javascript
context.log({hello: 'world'});  
```

<span data-ttu-id="8f2af-154">hello 위 코드는 해당 toohello 코드 다음:</span><span class="sxs-lookup"><span data-stu-id="8f2af-154">hello preceding code is equivalent toohello following code:</span></span>

```javascript
context.log.info({hello: 'world'});  
```

<span data-ttu-id="8f2af-155">hello 다음 코드를 작성 hello 오류 수준에서 toohello 콘솔 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-155">hello following code writes toohello console at hello error level:</span></span>

```javascript
context.log.error("An error has occurred.");  
```

<span data-ttu-id="8f2af-156">때문에 _오류_ 은 hello 가장 높은 추적 수준에서이 추적이 기록 됩니다 모든 추적 수준에서 toohello 출력으로 로깅은 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-156">Because _error_ is hello highest trace level, this trace is written toohello output at all trace levels as long as logging is enabled.</span></span>  


<span data-ttu-id="8f2af-157">모든 `context.log` 메서드 지원 hello hello Node.js에서 지원 되는 동일한 매개 변수 형식이 [util.format 메서드](https://nodejs.org/api/util.html#util_util_format_format)합니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-157">All `context.log` methods support hello same parameter format that's supported by hello Node.js [util.format method](https://nodejs.org/api/util.html#util_util_format_format).</span></span> <span data-ttu-id="8f2af-158">Hello toohello 콘솔 hello 기본 추적 수준을 사용 하 여 작성 하는 코드를 다음을 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-158">Consider hello following code, which writes toohello console by using hello default trace level:</span></span>

```javascript
context.log('Node.js HTTP trigger function processed a request. RequestUri=' + req.originalUrl);
context.log('Request Headers = ' + JSON.stringify(req.headers));
```

<span data-ttu-id="8f2af-159">또한 쓰기 hello 동일의 코드 형식에 따라 hello에서 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-159">You can also write hello same code in hello following format:</span></span>

```javascript
context.log('Node.js HTTP trigger function processed a request. RequestUri=%s', req.originalUrl);
context.log('Request Headers = ', JSON.stringify(req.headers));
```

### <a name="configure-hello-trace-level-for-console-logging"></a><span data-ttu-id="8f2af-160">콘솔 로깅에 대 한 추적 수준을 hello 구성</span><span class="sxs-lookup"><span data-stu-id="8f2af-160">Configure hello trace level for console logging</span></span>

<span data-ttu-id="8f2af-161">함수에는 쉽게 toocontrol hello 방식으로 추적 toohello 콘솔 함수에서 작성 하므로 toohello 콘솔 작성 하기 위한 hello 임계값 추적 수준을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-161">Functions lets you define hello threshold trace level for writing toohello console, which makes it easy toocontrol hello way traces are written toohello console from your functions.</span></span> <span data-ttu-id="8f2af-162">toohello 콘솔을 사용 하 여 hello를 작성 하는 모든 추적에 대 한 tooset hello 임계값 `tracing.consoleLevel` hello host.json 파일의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-162">tooset hello threshold for all traces written toohello console, use hello `tracing.consoleLevel` property in hello host.json file.</span></span> <span data-ttu-id="8f2af-163">이 설정은 tooall 앱에서 함수에 함수를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-163">This setting applies tooall functions in your function app.</span></span> <span data-ttu-id="8f2af-164">hello 다음 예제에서는 설정 hello 추적 임계값 tooenable 자세한 정보 로깅:</span><span class="sxs-lookup"><span data-stu-id="8f2af-164">hello following example sets hello trace threshold tooenable verbose logging:</span></span>

```json
{ 
    "tracing": {      
        "consoleLevel": "verbose"     
    }
}  
```

<span data-ttu-id="8f2af-165">값 **consoleLevel** hello toohello 이름을 해당 `context.log` 메서드.</span><span class="sxs-lookup"><span data-stu-id="8f2af-165">Values of **consoleLevel** correspond toohello names of hello `context.log` methods.</span></span> <span data-ttu-id="8f2af-166">toodisable 모든 추적 toohello 콘솔 로깅이 설정 **consoleLevel** too_off_ 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-166">toodisable all trace logging toohello console, set **consoleLevel** too_off_.</span></span> <span data-ttu-id="8f2af-167">Hello host.json 파일에 대 한 자세한 내용은 참조 hello [host.json 참조 항목](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-167">For more information about hello host.json file, see hello [host.json reference topic](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span>

## <a name="http-triggers-and-bindings"></a><span data-ttu-id="8f2af-168">HTTP 트리거 및 바인딩</span><span class="sxs-lookup"><span data-stu-id="8f2af-168">HTTP triggers and bindings</span></span>

<span data-ttu-id="8f2af-169">HTTP 및 webhook 트리거 및 HTTP 요청 및 응답 개체 toorepresent hello HTTP 메시징 바인딩을 사용 하 여 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-169">HTTP and webhook triggers and HTTP output bindings use request and response objects toorepresent hello HTTP messaging.</span></span>  

### <a name="request-object"></a><span data-ttu-id="8f2af-170">요청 개체</span><span class="sxs-lookup"><span data-stu-id="8f2af-170">Request object</span></span>

<span data-ttu-id="8f2af-171">hello `request` 개체에 hello 다음과 같은 속성:</span><span class="sxs-lookup"><span data-stu-id="8f2af-171">hello `request` object has hello following properties:</span></span>

| <span data-ttu-id="8f2af-172">속성</span><span class="sxs-lookup"><span data-stu-id="8f2af-172">Property</span></span>      | <span data-ttu-id="8f2af-173">설명</span><span class="sxs-lookup"><span data-stu-id="8f2af-173">Description</span></span>                                                    |
| ------------- | -------------------------------------------------------------- |
| <span data-ttu-id="8f2af-174">_body_</span><span class="sxs-lookup"><span data-stu-id="8f2af-174">_body_</span></span>        | <span data-ttu-id="8f2af-175">Hello hello 요청 본문을 포함 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-175">An object that contains hello body of hello request.</span></span>               |
| <span data-ttu-id="8f2af-176">_headers_</span><span class="sxs-lookup"><span data-stu-id="8f2af-176">_headers_</span></span>     | <span data-ttu-id="8f2af-177">Hello 요청 헤더를 포함 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-177">An object that contains hello request headers.</span></span>                   |
| <span data-ttu-id="8f2af-178">_method_</span><span class="sxs-lookup"><span data-stu-id="8f2af-178">_method_</span></span>      | <span data-ttu-id="8f2af-179">hello hello 요청의 HTTP 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-179">hello HTTP method of hello request.</span></span>                                |
| <span data-ttu-id="8f2af-180">_originalUrl_</span><span class="sxs-lookup"><span data-stu-id="8f2af-180">_originalUrl_</span></span> | <span data-ttu-id="8f2af-181">hello 요청의 hello URL입니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-181">hello URL of hello request.</span></span>                                        |
| <span data-ttu-id="8f2af-182">_params_</span><span class="sxs-lookup"><span data-stu-id="8f2af-182">_params_</span></span>      | <span data-ttu-id="8f2af-183">Hello 요청의 hello 라우팅 매개 변수를 포함 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-183">An object that contains hello routing parameters of hello request.</span></span> |
| <span data-ttu-id="8f2af-184">_query_</span><span class="sxs-lookup"><span data-stu-id="8f2af-184">_query_</span></span>       | <span data-ttu-id="8f2af-185">Hello 쿼리 매개 변수를 포함 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-185">An object that contains hello query parameters.</span></span>                  |
| <span data-ttu-id="8f2af-186">_rawBody_</span><span class="sxs-lookup"><span data-stu-id="8f2af-186">_rawBody_</span></span>     | <span data-ttu-id="8f2af-187">hello 본문을 문자열로 hello 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-187">hello body of hello message as a string.</span></span>                           |


### <a name="response-object"></a><span data-ttu-id="8f2af-188">응답 개체</span><span class="sxs-lookup"><span data-stu-id="8f2af-188">Response object</span></span>

<span data-ttu-id="8f2af-189">hello `response` 개체에 hello 다음과 같은 속성:</span><span class="sxs-lookup"><span data-stu-id="8f2af-189">hello `response` object has hello following properties:</span></span>

| <span data-ttu-id="8f2af-190">속성</span><span class="sxs-lookup"><span data-stu-id="8f2af-190">Property</span></span>  | <span data-ttu-id="8f2af-191">설명</span><span class="sxs-lookup"><span data-stu-id="8f2af-191">Description</span></span>                                               |
| --------- | --------------------------------------------------------- |
| <span data-ttu-id="8f2af-192">_body_</span><span class="sxs-lookup"><span data-stu-id="8f2af-192">_body_</span></span>    | <span data-ttu-id="8f2af-193">Hello hello 응답 본문을 포함 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-193">An object that contains hello body of hello response.</span></span>         |
| <span data-ttu-id="8f2af-194">_headers_</span><span class="sxs-lookup"><span data-stu-id="8f2af-194">_headers_</span></span> | <span data-ttu-id="8f2af-195">Hello 응답 헤더를 포함 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-195">An object that contains hello response headers.</span></span>             |
| <span data-ttu-id="8f2af-196">_isRaw_</span><span class="sxs-lookup"><span data-stu-id="8f2af-196">_isRaw_</span></span>   | <span data-ttu-id="8f2af-197">Hello 응답에 대 한 서식 지정을 건너뜀을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-197">Indicates that formatting is skipped for hello response.</span></span>    |
| <span data-ttu-id="8f2af-198">_상태_</span><span class="sxs-lookup"><span data-stu-id="8f2af-198">_status_</span></span>  | <span data-ttu-id="8f2af-199">hello hello 응답의 HTTP 상태 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-199">hello HTTP status code of hello response.</span></span>                     |

### <a name="accessing-hello-request-and-response"></a><span data-ttu-id="8f2af-200">Hello 요청 및 응답에 액세스</span><span class="sxs-lookup"><span data-stu-id="8f2af-200">Accessing hello request and response</span></span> 

<span data-ttu-id="8f2af-201">HTTP 트리거와 함께 작업할 때 세 가지 방법 중 하나로 hello HTTP 요청 및 응답 개체를 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-201">When you work with HTTP triggers, you can access hello HTTP request and response objects in any of three ways:</span></span>

+ <span data-ttu-id="8f2af-202">Hello 명명 된 입력 및 출력 바인딩 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-202">From hello named input and output bindings.</span></span> <span data-ttu-id="8f2af-203">이러한 방식으로 hello HTTP 트리거와 바인딩 작업 hello 동일 다른 바인딩으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-203">In this way, hello HTTP trigger and bindings work hello same as any other binding.</span></span> <span data-ttu-id="8f2af-204">hello 다음 예제에서는 설정 hello 응답 개체 명명 된를 사용 하 여 `response` 바인딩:</span><span class="sxs-lookup"><span data-stu-id="8f2af-204">hello following example sets hello response object by using a named `response` binding:</span></span> 

    ```javascript
    context.bindings.response = { status: 201, body: "Insert succeeded." };
    ```

+ <span data-ttu-id="8f2af-205">`req` 및 `res` hello에 대 한 속성 `context` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-205">From `req` and `res` properties on hello `context` object.</span></span> <span data-ttu-id="8f2af-206">이러한 방식으로 전체 toouse hello 대신 hello 컨텍스트 개체에서 hello 규칙에 따른 패턴 tooaccess HTTP 데이터를 사용할 수 있습니다 `context.bindings.name` 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-206">In this way, you can use hello conventional pattern tooaccess HTTP data from hello context object, instead of having toouse hello full `context.bindings.name` pattern.</span></span> <span data-ttu-id="8f2af-207">hello 방법을 예제와 다음 tooaccess hello `req` 및 `res` 개체에 hello `context`:</span><span class="sxs-lookup"><span data-stu-id="8f2af-207">hello following example shows how tooaccess hello `req` and `res` objects on hello `context`:</span></span>

    ```javascript
    // You can access your http request off hello context ...
    if(context.req.body.emoji === ':pizza:') context.log('Yay!');
    // and also set your http response
    context.res = { status: 202, body: 'You successfully ordered more coffee!' }; 
    ```

+ <span data-ttu-id="8f2af-208">`context.done()`을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-208">By calling `context.done()`.</span></span> <span data-ttu-id="8f2af-209">Toohello 전달 되는 hello 응답을 반환 하는 특수 한 유형의 HTTP 바인딩 `context.done()` 메서드.</span><span class="sxs-lookup"><span data-stu-id="8f2af-209">A special kind of HTTP binding returns hello response that is passed toohello `context.done()` method.</span></span> <span data-ttu-id="8f2af-210">다음 HTTP hello 출력 바인딩이 정의 하는 `$return` 출력 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="8f2af-210">hello following HTTP output binding defines a `$return` output parameter:</span></span>

    ```json
    {
      "type": "http",
      "direction": "out",
      "name": "$return"
    }
    ``` 
    <span data-ttu-id="8f2af-211">이 출력 바인딩의 프로시저 해야 toosupply hello 응답을 호출할 때 `done()`, 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-211">This output binding expects you toosupply hello response when you call `done()`, as follows:</span></span>

    ```javascript
     // Define a valid response object.
    res = { status: 201, body: "Insert succeeded." };
    context.done(null, res);   
    ```  

## <a name="node-version-and-package-management"></a><span data-ttu-id="8f2af-212">노드 버전 및 패키지 관리</span><span class="sxs-lookup"><span data-stu-id="8f2af-212">Node version and Package Management</span></span>
<span data-ttu-id="8f2af-213">hello 노드 버전에서 현재 잠겨 `6.5.0`합니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-213">hello node version is currently locked at `6.5.0`.</span></span> <span data-ttu-id="8f2af-214">더 많은 버전에 대한 지원을 추가하고 구성할 수 있도록 연구 중입니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-214">We're investigating adding support for more versions and making it configurable.</span></span>

<span data-ttu-id="8f2af-215">단계를 수행 하는 hello 함수 응용 프로그램에 패키지를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-215">hello following steps let you include packages in your function app:</span></span> 

1. <span data-ttu-id="8f2af-216">너무 이동`https://<function_app_name>.scm.azurewebsites.net`합니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-216">Go too`https://<function_app_name>.scm.azurewebsites.net`.</span></span>

2. <span data-ttu-id="8f2af-217">**디버그 콘솔** > **CMD**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-217">Click **Debug Console** > **CMD**.</span></span>

3. <span data-ttu-id="8f2af-218">너무 이동`D:\home\site\wwwroot`, package.json 파일 toohello 끌어와서 **wwwroot** hello 페이지의 위쪽 절반 hello 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-218">Go too`D:\home\site\wwwroot`, and then drag your package.json file toohello **wwwroot** folder at hello top half of hello page.</span></span>  
    <span data-ttu-id="8f2af-219">또한 다른 방법으로 tooyour 함수 응용 프로그램 파일을 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-219">You can upload files tooyour function app in other ways also.</span></span> <span data-ttu-id="8f2af-220">자세한 내용은 참조 [tooupdate 앱 파일을 어떻게 작동 하는지](functions-reference.md#fileupdate)합니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-220">For more information, see [How tooupdate function app files](functions-reference.md#fileupdate).</span></span> 

4. <span data-ttu-id="8f2af-221">Hello package.json 파일을 업로드 한 후 실행 hello `npm install` hello 명령을 **Kudu 원격 실행 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-221">After hello package.json file is uploaded, run hello `npm install` command in hello **Kudu remote execution console**.</span></span>  
    <span data-ttu-id="8f2af-222">이 작업 hello package.json 파일에 표시 된 hello 패키지를 다운로드 하 고 hello 함수 응용 프로그램을 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-222">This action downloads hello packages indicated in hello package.json file and restarts hello function app.</span></span>

<span data-ttu-id="8f2af-223">Hello 필요한 패키지를 설치한 후 가져올 tooyour 함수를 호출 하 여 `require('packagename')`와 같이, 다음 예제는 hello:</span><span class="sxs-lookup"><span data-stu-id="8f2af-223">After hello packages you need are installed, you import them tooyour function by calling `require('packagename')`, as in hello following example:</span></span>

```javascript
// Import hello underscore.js library
var _ = require('underscore');
var version = process.version; // version === 'v6.5.0'

module.exports = function(context) {
    // Using our imported underscore.js library
    var matched_names = _
        .where(context.bindings.myInput.names, {first: 'Carla'});
```

<span data-ttu-id="8f2af-224">정의 해야는 `package.json` 함수 응용 프로그램의 hello 루트에 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-224">You should define a `package.json` file at hello root of your function app.</span></span> <span data-ttu-id="8f2af-225">정의 hello 파일 hello 최상의 성능을 제공 하는 동일한 캐시 된 패키지를 hello hello 앱 공유의 모든 기능을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-225">Defining hello file lets all functions in hello app share hello same cached packages, which gives hello best performance.</span></span> <span data-ttu-id="8f2af-226">버전 충돌이 발생할 경우 추가 하 여 해결할 수 있습니다는 `package.json` 특정 함수 hello 폴더의 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-226">If a version conflict arises, you can resolve it by adding a `package.json` file in hello folder of a specific function.</span></span>  

## <a name="environment-variables"></a><span data-ttu-id="8f2af-227">환경 변수</span><span class="sxs-lookup"><span data-stu-id="8f2af-227">Environment variables</span></span>
<span data-ttu-id="8f2af-228">tooget 환경 변수 또는 응용 프로그램 설정 값을 사용 하 여 `process.env`hello 다음 코드 예제에에서 나온 것 처럼:</span><span class="sxs-lookup"><span data-stu-id="8f2af-228">tooget an environment variable or an app setting value, use `process.env`, as shown in hello following code example:</span></span>

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
## <a name="considerations-for-javascript-functions"></a><span data-ttu-id="8f2af-229">JavaScript 함수에 대한 고려 사항</span><span class="sxs-lookup"><span data-stu-id="8f2af-229">Considerations for JavaScript functions</span></span>

<span data-ttu-id="8f2af-230">JavaScript 함수를 사용 하는 경우에 다음 두 섹션 hello에 hello 고려 사항에 주의 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-230">When you work with JavaScript functions, be aware of hello considerations in hello following two sections.</span></span>

### <a name="choose-single-core-app-service-plans"></a><span data-ttu-id="8f2af-231">단일 코어 App Service 계획 선택</span><span class="sxs-lookup"><span data-stu-id="8f2af-231">Choose single-core App Service plans</span></span>

<span data-ttu-id="8f2af-232">앱 서비스 계획 hello를 사용 하는 함수 앱을 만들 때 여러 코어를 사용 하 여 계획 보다는 단일 코어 계획을 선택 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-232">When you create a function app that uses hello App Service plan, we recommend that you select a single-core plan rather than a plan with multiple cores.</span></span> <span data-ttu-id="8f2af-233">오늘날 함수 실행 JavaScript 함수가 더 효율적으로 단일 코어 Vm에서 되며 더 큰 Vm을 사용 하 여 hello 예상 성능 향상을 생성 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-233">Today, Functions runs JavaScript functions more efficiently on single-core VMs, and using larger VMs does not produce hello expected performance improvements.</span></span> <span data-ttu-id="8f2af-234">필요한 경우 더 많은 단일 코어 VM 인스턴스를 추가하여 수동으로 확장하거나 자동 크기 조정을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-234">When necessary, you can manually scale out by adding more single-core VM instances, or you can enable auto-scale.</span></span> <span data-ttu-id="8f2af-235">자세한 내용은 [수동 또는 자동으로 인스턴스 개수 조정](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8f2af-235">For more information, see [Scale instance count manually or automatically](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json).</span></span>    

### <a name="typescript-and-coffeescript-support"></a><span data-ttu-id="8f2af-236">TypeScript 및 CoffeeScript 지원</span><span class="sxs-lookup"><span data-stu-id="8f2af-236">TypeScript and CoffeeScript support</span></span>
<span data-ttu-id="8f2af-237">직접적으로 지원 아직 존재 하지 않는 자동 컴파일 TypeScript 또는 CoffeeScript에 대 한 hello 런타임을 통해, 때문에 이러한 지원이 toobe 배포 시 hello 런타임 외부 처리 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f2af-237">Because direct support does not yet exist for auto-compiling TypeScript or CoffeeScript via hello runtime, such support needs toobe handled outside hello runtime, at deployment time.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="8f2af-238">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8f2af-238">Next steps</span></span>
<span data-ttu-id="8f2af-239">자세한 내용은 다음 리소스는 hello 참조:</span><span class="sxs-lookup"><span data-stu-id="8f2af-239">For more information, see hello following resources:</span></span>

* [<span data-ttu-id="8f2af-240">Azure Functions에 대한 모범 사례</span><span class="sxs-lookup"><span data-stu-id="8f2af-240">Best practices for Azure Functions</span></span>](functions-best-practices.md)
* [<span data-ttu-id="8f2af-241">Azure Functions 개발자 참조</span><span class="sxs-lookup"><span data-stu-id="8f2af-241">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="8f2af-242">Azure Functions C# 개발자 참조</span><span class="sxs-lookup"><span data-stu-id="8f2af-242">Azure Functions C# developer reference</span></span>](functions-reference-csharp.md)
* [<span data-ttu-id="8f2af-243">Azure Functions F# 개발자 참조</span><span class="sxs-lookup"><span data-stu-id="8f2af-243">Azure Functions F# developer reference</span></span>](functions-reference-fsharp.md)
* [<span data-ttu-id="8f2af-244">Azure Functions 트리거 및 바인딩</span><span class="sxs-lookup"><span data-stu-id="8f2af-244">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)


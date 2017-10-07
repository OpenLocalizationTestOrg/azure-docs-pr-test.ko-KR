---
title: "aaaAzure 함수 모바일 앱 바인딩 | Microsoft Docs"
description: "이해 어떻게 Azure 함수에서 toouse Azure 모바일 앱 바인딩."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
keywords: "Azure Functions, 함수, 이벤트 처리, 동적 계산, 서버를 사용하지 않는 아키텍처"
ms.assetid: faad1263-0fa5-41a9-964f-aecbc0be706a
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 10/31/2016
ms.author: glenga
ms.openlocfilehash: d3679a5d5c66705b32e422ec17e3a1e6d6ac063c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-mobile-apps-bindings"></a><span data-ttu-id="6dd69-104">Azure Functions 모바일 앱 바인딩</span><span class="sxs-lookup"><span data-stu-id="6dd69-104">Azure Functions Mobile Apps bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="6dd69-105">이 문서에서는 설명 어떻게 tooconfigure 및 코드 [Azure 모바일 앱](../app-service-mobile/app-service-mobile-value-prop.md) Azure 함수에서 바인딩.</span><span class="sxs-lookup"><span data-stu-id="6dd69-105">This article explains how tooconfigure and code [Azure Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) bindings in Azure Functions.</span></span> <span data-ttu-id="6dd69-106">Azure Functions는 Mobile Apps에 대한 입력 및 출력 바인딩을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd69-106">Azure Functions supports input and output bindings for Mobile Apps.</span></span>

<span data-ttu-id="6dd69-107">hello 모바일 앱 입력 및 출력 바인딩을 사용 하면 [읽기 / 쓰기 작업 toodata 테이블](../app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations) 모바일 앱에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6dd69-107">hello Mobile Apps input and output bindings let you [read from and write toodata tables](../app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations) in your mobile app.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="input"></a>

## <a name="mobile-apps-input-binding"></a><span data-ttu-id="6dd69-108">Mobile Apps 입력 바인딩</span><span class="sxs-lookup"><span data-stu-id="6dd69-108">Mobile Apps input binding</span></span>
<span data-ttu-id="6dd69-109">모바일 앱 입력된 바인딩 hello 모바일 테이블 끝점에서 레코드를 로드 하 고 함수에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd69-109">hello Mobile Apps input binding loads a record from a mobile table endpoint and passes it into your function.</span></span> <span data-ttu-id="6dd69-110">C# 및 F # 함수를 모든 변경 내용을 toohello 레코드가 자동으로 전송 됩니다 백 toohello 테이블 hello 함수는 성공적으로 종료 될 때.</span><span class="sxs-lookup"><span data-stu-id="6dd69-110">In a C# and F# functions, any changes made toohello record are automatically sent back toohello table when hello function exits successfully.</span></span>

<span data-ttu-id="6dd69-111">모바일 앱 hello tooa 함수 hello 다음 JSON 개체 hello에서 사용 하 여 입력 `bindings` function.json의 배열:</span><span class="sxs-lookup"><span data-stu-id="6dd69-111">hello Mobile Apps input tooa function uses hello following JSON object in hello `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "mobileTable",
    "tableName": "<Name of your mobile app's data table>",
    "id" : "<Id of hello record tooretrieve - see below>",
    "connection": "<Name of app setting that has your mobile app's URL - see below>",
    "apiKey": "<Name of app setting that has your mobile app's API key - see below>",
    "direction": "in"
}
```

<span data-ttu-id="6dd69-112">참고 hello 다음.</span><span class="sxs-lookup"><span data-stu-id="6dd69-112">Note hello following:</span></span>

* <span data-ttu-id="6dd69-113">`id`정적 이거나 hello 함수를 호출 하는 hello 트리거 기반 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6dd69-113">`id` can be static, or it can be based on hello trigger that invokes hello function.</span></span> <span data-ttu-id="6dd69-114">예를 들어, 사용 하는 경우는 [큐 트리거]() 다음 함수에 대 한 `"id": "{queueTrigger}"` 레코드 ID tooretrieve hello으로 사용 하 여 hello hello 큐 메시지의 문자열 값입니다.</span><span class="sxs-lookup"><span data-stu-id="6dd69-114">For example, if you use a [queue trigger]() for your function, then `"id": "{queueTrigger}"` uses hello string value of hello queue message as hello record ID tooretrieve.</span></span>
* <span data-ttu-id="6dd69-115">`connection`모바일 앱의 hello URL을 포함 함수 응용 프로그램에 응용 프로그램 설정의 hello 이름을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd69-115">`connection` should contain hello name of an app setting in your function app, which in turn contains hello URL of your mobile app.</span></span> <span data-ttu-id="6dd69-116">hello 함수 모바일 앱에 대 한이 URL tooconstruct hello 필요한 나머지 작업을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd69-116">hello function uses this URL tooconstruct hello required REST operations against your mobile app.</span></span> <span data-ttu-id="6dd69-117">있습니다 [함수 응용 프로그램에 응용 프로그램 설정 만들기]() 모바일 앱의 URL을 포함 하 (모양의 `http://<appname>.azurewebsites.net`), hello에 hello 앱 설정의 hello 이름을 지정 합니다 `connection` 입력된 바인딩에서 속성 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd69-117">You [create an app setting in your function app]() that contains your mobile app's URL (which looks like `http://<appname>.azurewebsites.net`), then specify hello name of hello app setting in hello `connection` property in your input binding.</span></span> 
* <span data-ttu-id="6dd69-118">Toospecify 해야 `apiKey` 경우 있습니다 [Node.js 모바일 앱 백 엔드에서 API 키를 구현](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), 또는 [.NET 모바일 앱 백 엔드에서 API 키 구현](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key)합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd69-118">You need toospecify `apiKey` if you [implement an API key in your Node.js mobile app backend](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), or [implement an API key in your .NET mobile app backend](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span></span> <span data-ttu-id="6dd69-119">toodo이를 있습니다 [함수 응용 프로그램에서 프로그램 응용 프로그램 설정을 만들려면]() hello API 키가 들어, 다음 hello 추가 `apiKey` hello 응용 프로그램 설정의 hello 이름의 입력된 바인딩에서 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="6dd69-119">toodo this, you [create an app setting in your function app]() that contains hello API key, then add hello `apiKey` property in your input binding with hello name of hello app setting.</span></span> 
  
  > [!IMPORTANT]
  > <span data-ttu-id="6dd69-120">이 API 키는 모바일 앱 클라이언트와 공유해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6dd69-120">This API key must not be shared with your mobile app clients.</span></span> <span data-ttu-id="6dd69-121">Azure 함수 처럼 분산된 안전 하 게 tooservice 측 클라이언트 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd69-121">It should only be distributed securely tooservice-side clients, like Azure Functions.</span></span> 
  > 
  > [!NOTE]
  > <span data-ttu-id="6dd69-122">Azure Functions는 사용자의 소스 제어 리포지토리를 확인하지 않도록 사용자 연결 정보 및 API 키를 앱 설정으로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd69-122">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span></span> <span data-ttu-id="6dd69-123">이는 사용자의 중요한 정보를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd69-123">This safeguards your sensitive information.</span></span>
  > 
  > 

<a name="inputusage"></a>

## <a name="input-usage"></a><span data-ttu-id="6dd69-124">입력 사용</span><span class="sxs-lookup"><span data-stu-id="6dd69-124">Input usage</span></span>
<span data-ttu-id="6dd69-125">이 섹션에서는 toouse 모바일 앱 입력 방식 함수 코드에서 바인딩을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6dd69-125">This section shows you how toouse your Mobile Apps input binding in your function code.</span></span> 

<span data-ttu-id="6dd69-126">명명 된 hello에 전달 될 hello로 hello 레코드 테이블과 레코드 ID를 찾을 수를 지정 하면 [JObject](http://www.newtonsoft.com/json/help/html/t_newtonsoft_json_linq_jobject.htm) 매개 변수 (또는 Node.js에서에 전달 될 hello `context.bindings.<name>` 개체).</span><span class="sxs-lookup"><span data-stu-id="6dd69-126">When hello record with hello specified table and record ID is found, it is passed into hello named [JObject](http://www.newtonsoft.com/json/help/html/t_newtonsoft_json_linq_jobject.htm) parameter (or, in Node.js, it is passed into hello `context.bindings.<name>` object).</span></span> <span data-ttu-id="6dd69-127">Hello 매개 변수는 hello 레코드를 찾지 못한 경우 `null`합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd69-127">When hello record is not found, hello parameter is `null`.</span></span> 

<span data-ttu-id="6dd69-128">C# 및 F # 함수에서 입력 toohello 레코드 (입력된 매개 변수)를 수행한 변경 내용 자동으로 전송 됩니다 백 toohello 모바일 앱 테이블 hello 함수는 성공적으로 종료 될 때입니다.</span><span class="sxs-lookup"><span data-stu-id="6dd69-128">In C# and F# functions, any changes you make toohello input record (input parameter) is automatically sent back toohello Mobile Apps table when hello function exits successfully.</span></span> <span data-ttu-id="6dd69-129">Node.js 함수에서 사용 하 여 `context.bindings.<name>` tooaccess hello 입력된 레코드입니다.</span><span class="sxs-lookup"><span data-stu-id="6dd69-129">In Node.js functions, use `context.bindings.<name>` tooaccess hello input record.</span></span> <span data-ttu-id="6dd69-130">Node.js에서 레코드를 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6dd69-130">You cannot modify a record in Node.js.</span></span>

<a name="inputsample"></a>

## <a name="input-sample"></a><span data-ttu-id="6dd69-131">입력 샘플</span><span class="sxs-lookup"><span data-stu-id="6dd69-131">Input sample</span></span>
<span data-ttu-id="6dd69-132">다음 function.json hello 가정 hello 큐 트리거 메시지의 hello id 인 모바일 앱 테이블 레코드를 검색 하는:</span><span class="sxs-lookup"><span data-stu-id="6dd69-132">Suppose you have hello following function.json, that retrieves a Mobile App table record with hello id of hello queue trigger message:</span></span>

```json
{
"bindings": [
    {
    "name": "myQueueItem",
    "queueName": "myqueue-items",
    "connection":"",
    "type": "queueTrigger",
    "direction": "in"
    },
    {
        "name": "record",
        "type": "mobileTable",
        "tableName": "MyTable",
        "id" : "{queueTrigger}",
        "connection": "My_MobileApp_Url",
        "apiKey": "My_MobileApp_Key",
        "direction": "in"
    }
],
"disabled": false
}
```

<span data-ttu-id="6dd69-133">Hello 바인딩에서 hello 입력된 레코드를 사용 하는 hello 언어 관련 샘플을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="6dd69-133">See hello language-specific sample that uses hello input record from hello binding.</span></span> <span data-ttu-id="6dd69-134">hello C# 및 F # 샘플 hello 레코드를 수정할 수도 `text` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="6dd69-134">hello C# and F# samples also modify hello record's `text` property.</span></span>

* [<span data-ttu-id="6dd69-135">C#</span><span class="sxs-lookup"><span data-stu-id="6dd69-135">C#</span></span>](#inputcsharp)
* [<span data-ttu-id="6dd69-136">Node.JS</span><span class="sxs-lookup"><span data-stu-id="6dd69-136">Node.js</span></span>](#inputnodejs)

<a name="inputcsharp"></a>

### <a name="input-sample-in-c"></a><span data-ttu-id="6dd69-137">C#의 입력 샘플</span><span class="sxs-lookup"><span data-stu-id="6dd69-137">Input sample in C#</span></span> #

```cs
#r "Newtonsoft.Json"    
using Newtonsoft.Json.Linq;

public static void Run(string myQueueItem, JObject record)
{
    if (record != null)
    {
        record["Text"] = "This has changed.";
    }    
}
```

<!--
<a name="inputfsharp"></a>
### Input sample in F# ## 

```fsharp
#r "Newtonsoft.Json"    
open Newtonsoft.Json.Linq
let Run(myQueueItem: string, record: JObject) =
  inputDocument?text <- "This has changed."
```
-->

<a name="inputnodejs"></a>

### <a name="input-sample-in-nodejs"></a><span data-ttu-id="6dd69-138">Node.js에서 입력 샘플</span><span class="sxs-lookup"><span data-stu-id="6dd69-138">Input sample in Node.js</span></span>

```javascript
module.exports = function (context, myQueueItem) {    
    context.log(context.bindings.record);
    context.done();
};
```

<a name="output"></a>

## <a name="mobile-apps-output-binding"></a><span data-ttu-id="6dd69-139">Mobile Apps 출력 바인딩</span><span class="sxs-lookup"><span data-stu-id="6dd69-139">Mobile Apps output binding</span></span>
<span data-ttu-id="6dd69-140">Hello 모바일 앱 출력 바인딩 toowrite 새 레코드 tooa 모바일 앱 테이블 끝점을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd69-140">Use hello Mobile Apps output binding toowrite a new record tooa Mobile Apps table endpoint.</span></span>  

<span data-ttu-id="6dd69-141">hello 함수를 사용 하는 다음 JSON 개체에 hello hello를 출력 하는 모바일 앱 `bindings` function.json의 배열:</span><span class="sxs-lookup"><span data-stu-id="6dd69-141">hello Mobile Apps output for a function uses hello following JSON object in hello `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of output parameter in function signature>",
    "type": "mobileTable",
    "tableName": "<Name of your mobile app's data table>",
    "connection": "<Name of app setting that has your mobile app's URL - see below>",
    "apiKey": "<Name of app setting that has your mobile app's API key - see below>",
    "direction": "out"
}
```

<span data-ttu-id="6dd69-142">참고 hello 다음.</span><span class="sxs-lookup"><span data-stu-id="6dd69-142">Note hello following:</span></span>

* <span data-ttu-id="6dd69-143">`connection`모바일 앱의 hello URL을 포함 함수 응용 프로그램에 응용 프로그램 설정의 hello 이름을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd69-143">`connection` should contain hello name of an app setting in your function app, which in turn contains hello URL of your mobile app.</span></span> <span data-ttu-id="6dd69-144">hello 함수 모바일 앱에 대 한이 URL tooconstruct hello 필요한 나머지 작업을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd69-144">hello function uses this URL tooconstruct hello required REST operations against your mobile app.</span></span> <span data-ttu-id="6dd69-145">있습니다 [함수 응용 프로그램에 응용 프로그램 설정 만들기]() 모바일 앱의 URL을 포함 하 (모양의 `http://<appname>.azurewebsites.net`), hello에 hello 앱 설정의 hello 이름을 지정 합니다 `connection` 입력된 바인딩에서 속성 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd69-145">You [create an app setting in your function app]() that contains your mobile app's URL (which looks like `http://<appname>.azurewebsites.net`), then specify hello name of hello app setting in hello `connection` property in your input binding.</span></span> 
* <span data-ttu-id="6dd69-146">Toospecify 해야 `apiKey` 경우 있습니다 [Node.js 모바일 앱 백 엔드에서 API 키를 구현](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), 또는 [.NET 모바일 앱 백 엔드에서 API 키 구현](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key)합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd69-146">You need toospecify `apiKey` if you [implement an API key in your Node.js mobile app backend](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), or [implement an API key in your .NET mobile app backend](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span></span> <span data-ttu-id="6dd69-147">toodo이를 있습니다 [함수 응용 프로그램에서 프로그램 응용 프로그램 설정을 만들려면]() hello API 키가 들어, 다음 hello 추가 `apiKey` hello 응용 프로그램 설정의 hello 이름의 입력된 바인딩에서 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="6dd69-147">toodo this, you [create an app setting in your function app]() that contains hello API key, then add hello `apiKey` property in your input binding with hello name of hello app setting.</span></span> 
  
  > [!IMPORTANT]
  > <span data-ttu-id="6dd69-148">이 API 키는 모바일 앱 클라이언트와 공유해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6dd69-148">This API key must not be shared with your mobile app clients.</span></span> <span data-ttu-id="6dd69-149">Azure 함수 처럼 분산된 안전 하 게 tooservice 측 클라이언트 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd69-149">It should only be distributed securely tooservice-side clients, like Azure Functions.</span></span> 
  > 
  > [!NOTE]
  > <span data-ttu-id="6dd69-150">Azure Functions는 사용자의 소스 제어 리포지토리를 확인하지 않도록 사용자 연결 정보 및 API 키를 앱 설정으로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd69-150">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span></span> <span data-ttu-id="6dd69-151">이는 사용자의 중요한 정보를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd69-151">This safeguards your sensitive information.</span></span>
  > 
  > 

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="6dd69-152">출력 사용</span><span class="sxs-lookup"><span data-stu-id="6dd69-152">Output usage</span></span>
<span data-ttu-id="6dd69-153">이 섹션에서는 어떻게 toouse 모바일 앱 출력 함수 코드에서 바인딩을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6dd69-153">This section shows you how toouse your Mobile Apps output binding in your function code.</span></span> 

<span data-ttu-id="6dd69-154">C# 함수에서 형식의 명명 된 출력 매개 변수를 사용 하 여 `out object` tooaccess hello 레코드를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd69-154">In C# functions, use a named output parameter of type `out object` tooaccess hello output record.</span></span> <span data-ttu-id="6dd69-155">Node.js 함수에서 사용 하 여 `context.bindings.<name>` tooaccess hello 레코드를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd69-155">In Node.js functions, use `context.bindings.<name>` tooaccess hello output record.</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="6dd69-156">출력 샘플</span><span class="sxs-lookup"><span data-stu-id="6dd69-156">Output sample</span></span>
<span data-ttu-id="6dd69-157">Hello function.json 큐 트리거 및 모바일 응용 프로그램 출력을 정의 하는 다음 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd69-157">Suppose you have hello following function.json, that defines a queue trigger and a Mobile Apps output:</span></span>

```json
{
"bindings": [
    {
    "name": "myQueueItem",
    "queueName": "myqueue-items",
    "connection":"",
    "type": "queueTrigger",
    "direction": "in"
    },
    {
    "name": "record",
    "type": "mobileTable",
    "tableName": "MyTable",
    "connection": "My_MobileApp_Url",
    "apiKey": "My_MobileApp_Key",
    "direction": "out"
    }
],
"disabled": false
}
```

<span data-ttu-id="6dd69-158">Hello 큐 메시지의 hello 콘텐츠로 hello 모바일 앱 테이블 끝점에서 레코드를 작성 하는 hello 언어 관련 샘플을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="6dd69-158">See hello language-specific sample that creates a record in hello Mobile Apps table endpoint with hello content of hello queue message.</span></span>

* [<span data-ttu-id="6dd69-159">C#</span><span class="sxs-lookup"><span data-stu-id="6dd69-159">C#</span></span>](#outcsharp)
* [<span data-ttu-id="6dd69-160">Node.JS</span><span class="sxs-lookup"><span data-stu-id="6dd69-160">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="6dd69-161">C#에서 출력 샘플</span><span class="sxs-lookup"><span data-stu-id="6dd69-161">Output sample in C#</span></span> #

```cs
public static void Run(string myQueueItem, out object record)
{
    record = new {
        Text = $"I'm running in a C# function! {myQueueItem}"
    };
}
```

<!--
<a name="outfsharp"></a>
### Output sample in F# ## 
```fsharp

```
-->
<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a><span data-ttu-id="6dd69-162">Node.js에서 출력 샘플</span><span class="sxs-lookup"><span data-stu-id="6dd69-162">Output sample in Node.js</span></span>

```javascript
module.exports = function (context, myQueueItem) {

    context.bindings.record = {
        text : "I'm running in a Node function! Data: '" + myQueueItem + "'"
    }   

    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="6dd69-163">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6dd69-163">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]


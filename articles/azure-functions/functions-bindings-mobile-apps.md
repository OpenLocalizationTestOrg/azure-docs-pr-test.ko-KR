---
title: "Azure Functions Mobile Apps 바인딩 | Microsoft Docs"
description: "Azure Functions에서 Azure 모바일 앱 바인딩을 사용하는 방법을 파악합니다."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
keywords: "Azure 함수, 함수, 이벤트 처리, 동적 계산, 서버를 사용하지 않는 아키텍처"
ms.assetid: faad1263-0fa5-41a9-964f-aecbc0be706a
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 10/31/2016
ms.author: glenga
ms.openlocfilehash: c5e1c02984f9773b263c0bee7685c7d5ff62e658
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-mobile-apps-bindings"></a><span data-ttu-id="fffb4-104">Azure Functions 모바일 앱 바인딩</span><span class="sxs-lookup"><span data-stu-id="fffb4-104">Azure Functions Mobile Apps bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="fffb4-105">이 문서에서는 Azure Functions에서 [Azure Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) 바인딩을 구성하고 코딩하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="fffb4-105">This article explains how to configure and code [Azure Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) bindings in Azure Functions.</span></span> <span data-ttu-id="fffb4-106">Azure Functions는 Mobile Apps에 대한 입력 및 출력 바인딩을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="fffb4-106">Azure Functions supports input and output bindings for Mobile Apps.</span></span>

<span data-ttu-id="fffb4-107">Mobile Apps 입력 및 출력 바인딩을 사용하면 모바일 앱에서 [데이터 테이블에서 읽고 쓸](../app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fffb4-107">The Mobile Apps input and output bindings let you [read from and write to data tables](../app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations) in your mobile app.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="input"></a>

## <a name="mobile-apps-input-binding"></a><span data-ttu-id="fffb4-108">Mobile Apps 입력 바인딩</span><span class="sxs-lookup"><span data-stu-id="fffb4-108">Mobile Apps input binding</span></span>
<span data-ttu-id="fffb4-109">Mobile Apps 입력 바인딩은 모바일 테이블 끝점에서 레코드를 로드하여 함수에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="fffb4-109">The Mobile Apps input binding loads a record from a mobile table endpoint and passes it into your function.</span></span> <span data-ttu-id="fffb4-110">C# 및 F# 함수에서 함수가 성공적으로 종료되면 레코드에 변경한 내용을 자동으로 다시 테이블에 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="fffb4-110">In a C# and F# functions, any changes made to the record are automatically sent back to the table when the function exits successfully.</span></span>

<span data-ttu-id="fffb4-111">함수에 대한 Mobile Apps 입력은 function.json의 `bindings` 배열에서 다음과 같은 JSON 개체를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fffb4-111">The Mobile Apps input to a function uses the following JSON object in the `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "mobileTable",
    "tableName": "<Name of your mobile app's data table>",
    "id" : "<Id of the record to retrieve - see below>",
    "connection": "<Name of app setting that has your mobile app's URL - see below>",
    "apiKey": "<Name of app setting that has your mobile app's API key - see below>",
    "direction": "in"
}
```

<span data-ttu-id="fffb4-112">다음 사항에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="fffb4-112">Note the following:</span></span>

* <span data-ttu-id="fffb4-113">`id`는 정적이거나 함수를 호출하는 트리거를 기반으로 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fffb4-113">`id` can be static, or it can be based on the trigger that invokes the function.</span></span> <span data-ttu-id="fffb4-114">예를 들어, 함수에 대해 [큐 트리거]()를 사용하는 경우 `"id": "{queueTrigger}"`는 검색할 레코드 ID로 큐 메시지의 문자열 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fffb4-114">For example, if you use a [queue trigger]() for your function, then `"id": "{queueTrigger}"` uses the string value of the queue message as the record ID to retrieve.</span></span>
* <span data-ttu-id="fffb4-115">`connection`에는 모바일 앱의 URL이 포함되어 있는 함수 앱의 앱 설정 이름이 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fffb4-115">`connection` should contain the name of an app setting in your function app, which in turn contains the URL of your mobile app.</span></span> <span data-ttu-id="fffb4-116">함수는 이 URL을 사용하여 모바일 앱에 대해 필요한 나머지 작업을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="fffb4-116">The function uses this URL to construct the required REST operations against your mobile app.</span></span> <span data-ttu-id="fffb4-117">모바일 앱의 URL(`http://<appname>.azurewebsites.net`과 유사)을 포함하는 [함수 앱의 앱 설정을 만들고](), 다음으로 입력 바인딩의 `connection` 속성에서 앱 설정의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fffb4-117">You [create an app setting in your function app]() that contains your mobile app's URL (which looks like `http://<appname>.azurewebsites.net`), then specify the name of the app setting in the `connection` property in your input binding.</span></span> 
* <span data-ttu-id="fffb4-118">[Node.js 모바일 앱 백 엔드에 API 키를 구현](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key)하거나 [.NET 모바일 앱 백 엔드에 API 키를 구현](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key)한 경우 `apiKey`를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fffb4-118">You need to specify `apiKey` if you [implement an API key in your Node.js mobile app backend](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), or [implement an API key in your .NET mobile app backend](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span></span> <span data-ttu-id="fffb4-119">이렇게 하려면 API 키가 포함된 [함수 앱의 앱 설정을 만들고](), 다음으로 `apiKey` 속성을 앱 설정의 이름과 함께 입력 바인딩에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="fffb4-119">To do this, you [create an app setting in your function app]() that contains the API key, then add the `apiKey` property in your input binding with the name of the app setting.</span></span> 
  
  > [!IMPORTANT]
  > <span data-ttu-id="fffb4-120">이 API 키는 모바일 앱 클라이언트와 공유해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fffb4-120">This API key must not be shared with your mobile app clients.</span></span> <span data-ttu-id="fffb4-121">Azure Functions처럼 서비스 측 클라이언트에게만 안전하게 배포되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fffb4-121">It should only be distributed securely to service-side clients, like Azure Functions.</span></span> 
  > 
  > [!NOTE]
  > <span data-ttu-id="fffb4-122">Azure Functions는 사용자의 소스 제어 리포지토리를 확인하지 않도록 사용자 연결 정보 및 API 키를 앱 설정으로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="fffb4-122">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span></span> <span data-ttu-id="fffb4-123">이는 사용자의 중요한 정보를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="fffb4-123">This safeguards your sensitive information.</span></span>
  > 
  > 

<a name="inputusage"></a>

## <a name="input-usage"></a><span data-ttu-id="fffb4-124">입력 사용</span><span class="sxs-lookup"><span data-stu-id="fffb4-124">Input usage</span></span>
<span data-ttu-id="fffb4-125">이 섹션에서는 함수 코드에서 Mobile Apps 입력 바인딩을 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fffb4-125">This section shows you how to use your Mobile Apps input binding in your function code.</span></span> 

<span data-ttu-id="fffb4-126">지정된 테이블 및 레코드 ID를 사용하는 레코드가 발견되면 명명된 [JObject](http://www.newtonsoft.com/json/help/html/t_newtonsoft_json_linq_jobject.htm) 매개 변수로 전달됩니다(또는 Node.js에서는 `context.bindings.<name>` 개체로 전달됨).</span><span class="sxs-lookup"><span data-stu-id="fffb4-126">When the record with the specified table and record ID is found, it is passed into the named [JObject](http://www.newtonsoft.com/json/help/html/t_newtonsoft_json_linq_jobject.htm) parameter (or, in Node.js, it is passed into the `context.bindings.<name>` object).</span></span> <span data-ttu-id="fffb4-127">레코드가 없는 경우 매개 변수는 `null`입니다.</span><span class="sxs-lookup"><span data-stu-id="fffb4-127">When the record is not found, the parameter is `null`.</span></span> 

<span data-ttu-id="fffb4-128">C# 및 F# 함수에서 함수가 성공적으로 종료되면 입력 레코드에 변경한 내용(입력 매개 변수)을 자동으로 다시 Mobile Apps 테이블에 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="fffb4-128">In C# and F# functions, any changes you make to the input record (input parameter) is automatically sent back to the Mobile Apps table when the function exits successfully.</span></span> <span data-ttu-id="fffb4-129">Node.js 함수에서 `context.bindings.<name>`을 사용하여 입력 레코드에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="fffb4-129">In Node.js functions, use `context.bindings.<name>` to access the input record.</span></span> <span data-ttu-id="fffb4-130">Node.js에서 레코드를 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fffb4-130">You cannot modify a record in Node.js.</span></span>

<a name="inputsample"></a>

## <a name="input-sample"></a><span data-ttu-id="fffb4-131">입력 샘플</span><span class="sxs-lookup"><span data-stu-id="fffb4-131">Input sample</span></span>
<span data-ttu-id="fffb4-132">큐 트리거 메시지의 Id로 Mobile App 테이블 레코드를 검색하는 다음과 같은 function.json이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="fffb4-132">Suppose you have the following function.json, that retrieves a Mobile App table record with the id of the queue trigger message:</span></span>

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

<span data-ttu-id="fffb4-133">바인딩에서 입력 레코드를 사용하는 언어별 샘플을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fffb4-133">See the language-specific sample that uses the input record from the binding.</span></span> <span data-ttu-id="fffb4-134">C# 및 F # 샘플은 레코드의 `text` 속성도 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="fffb4-134">The C# and F# samples also modify the record's `text` property.</span></span>

* [<span data-ttu-id="fffb4-135">C#</span><span class="sxs-lookup"><span data-stu-id="fffb4-135">C#</span></span>](#inputcsharp)
* [<span data-ttu-id="fffb4-136">Node.JS</span><span class="sxs-lookup"><span data-stu-id="fffb4-136">Node.js</span></span>](#inputnodejs)

<a name="inputcsharp"></a>

### <a name="input-sample-in-c"></a><span data-ttu-id="fffb4-137">C#의 입력 샘플</span><span class="sxs-lookup"><span data-stu-id="fffb4-137">Input sample in C#</span></span> #

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

### <a name="input-sample-in-nodejs"></a><span data-ttu-id="fffb4-138">Node.js에서 입력 샘플</span><span class="sxs-lookup"><span data-stu-id="fffb4-138">Input sample in Node.js</span></span>

```javascript
module.exports = function (context, myQueueItem) {    
    context.log(context.bindings.record);
    context.done();
};
```

<a name="output"></a>

## <a name="mobile-apps-output-binding"></a><span data-ttu-id="fffb4-139">Mobile Apps 출력 바인딩</span><span class="sxs-lookup"><span data-stu-id="fffb4-139">Mobile Apps output binding</span></span>
<span data-ttu-id="fffb4-140">Mobile Apps 출력 바인딩을 사용하여 Mobile Apps 테이블 끝점에 새 레코드를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fffb4-140">Use the Mobile Apps output binding to write a new record to a Mobile Apps table endpoint.</span></span>  

<span data-ttu-id="fffb4-141">함수에 대한 Mobile Apps 출력은 function.json의 `bindings` 배열에서 다음과 같은 JSON 개체를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fffb4-141">The Mobile Apps output for a function uses the following JSON object in the `bindings` array of function.json:</span></span>

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

<span data-ttu-id="fffb4-142">다음 사항에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="fffb4-142">Note the following:</span></span>

* <span data-ttu-id="fffb4-143">`connection`에는 모바일 앱의 URL이 포함되어 있는 함수 앱의 앱 설정 이름이 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fffb4-143">`connection` should contain the name of an app setting in your function app, which in turn contains the URL of your mobile app.</span></span> <span data-ttu-id="fffb4-144">함수는 이 URL을 사용하여 모바일 앱에 대해 필요한 나머지 작업을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="fffb4-144">The function uses this URL to construct the required REST operations against your mobile app.</span></span> <span data-ttu-id="fffb4-145">모바일 앱의 URL(`http://<appname>.azurewebsites.net`과 유사)을 포함하는 [함수 앱의 앱 설정을 만들고](), 다음으로 입력 바인딩의 `connection` 속성에서 앱 설정의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fffb4-145">You [create an app setting in your function app]() that contains your mobile app's URL (which looks like `http://<appname>.azurewebsites.net`), then specify the name of the app setting in the `connection` property in your input binding.</span></span> 
* <span data-ttu-id="fffb4-146">[Node.js 모바일 앱 백 엔드에 API 키를 구현](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key)하거나 [.NET 모바일 앱 백 엔드에 API 키를 구현](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key)한 경우 `apiKey`를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fffb4-146">You need to specify `apiKey` if you [implement an API key in your Node.js mobile app backend](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), or [implement an API key in your .NET mobile app backend](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span></span> <span data-ttu-id="fffb4-147">이렇게 하려면 API 키가 포함된 [함수 앱의 앱 설정을 만들고](), 다음으로 `apiKey` 속성을 앱 설정의 이름과 함께 입력 바인딩에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="fffb4-147">To do this, you [create an app setting in your function app]() that contains the API key, then add the `apiKey` property in your input binding with the name of the app setting.</span></span> 
  
  > [!IMPORTANT]
  > <span data-ttu-id="fffb4-148">이 API 키는 모바일 앱 클라이언트와 공유해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fffb4-148">This API key must not be shared with your mobile app clients.</span></span> <span data-ttu-id="fffb4-149">Azure Functions처럼 서비스 측 클라이언트에게만 안전하게 배포되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fffb4-149">It should only be distributed securely to service-side clients, like Azure Functions.</span></span> 
  > 
  > [!NOTE]
  > <span data-ttu-id="fffb4-150">Azure Functions는 사용자의 소스 제어 리포지토리를 확인하지 않도록 사용자 연결 정보 및 API 키를 앱 설정으로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="fffb4-150">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span></span> <span data-ttu-id="fffb4-151">이는 사용자의 중요한 정보를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="fffb4-151">This safeguards your sensitive information.</span></span>
  > 
  > 

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="fffb4-152">출력 사용</span><span class="sxs-lookup"><span data-stu-id="fffb4-152">Output usage</span></span>
<span data-ttu-id="fffb4-153">이 섹션에서는 함수 코드에서 Mobile Apps 출력 바인딩을 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fffb4-153">This section shows you how to use your Mobile Apps output binding in your function code.</span></span> 

<span data-ttu-id="fffb4-154">C# 함수에서 `out object` 형식의 명명된 출력 매개 변수를 사용하여 출력 레코드에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="fffb4-154">In C# functions, use a named output parameter of type `out object` to access the output record.</span></span> <span data-ttu-id="fffb4-155">Node.js 함수에서 `context.bindings.<name>`을 사용하여 출력 레코드에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="fffb4-155">In Node.js functions, use `context.bindings.<name>` to access the output record.</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="fffb4-156">출력 샘플</span><span class="sxs-lookup"><span data-stu-id="fffb4-156">Output sample</span></span>
<span data-ttu-id="fffb4-157">큐 트리거 및 Mobile Apps 출력을 정의하는 다음과 같은 function.json이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="fffb4-157">Suppose you have the following function.json, that defines a queue trigger and a Mobile Apps output:</span></span>

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

<span data-ttu-id="fffb4-158">큐 메시지의 내용으로 Mobile Apps 테이블 끝점에 레코드를 작성하는 언어별 샘플을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fffb4-158">See the language-specific sample that creates a record in the Mobile Apps table endpoint with the content of the queue message.</span></span>

* [<span data-ttu-id="fffb4-159">C#</span><span class="sxs-lookup"><span data-stu-id="fffb4-159">C#</span></span>](#outcsharp)
* [<span data-ttu-id="fffb4-160">Node.JS</span><span class="sxs-lookup"><span data-stu-id="fffb4-160">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="fffb4-161">C#에서 출력 샘플</span><span class="sxs-lookup"><span data-stu-id="fffb4-161">Output sample in C#</span></span> #

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

### <a name="output-sample-in-nodejs"></a><span data-ttu-id="fffb4-162">Node.js에서 출력 샘플</span><span class="sxs-lookup"><span data-stu-id="fffb4-162">Output sample in Node.js</span></span>

```javascript
module.exports = function (context, myQueueItem) {

    context.bindings.record = {
        text : "I'm running in a Node function! Data: '" + myQueueItem + "'"
    }   

    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="fffb4-163">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fffb4-163">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]


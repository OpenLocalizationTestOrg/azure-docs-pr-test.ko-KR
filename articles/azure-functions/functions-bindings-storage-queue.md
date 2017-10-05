---
title: "Azure Functions Queue Storage 바인딩 | Microsoft Docs"
description: "Azure Functions에서 Azure Storage 트리거 및 바인딩을 사용하는 방법을 파악합니다."
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "Azure Functions, 함수, 이벤트 처리, 동적 계산, 서버를 사용하지 않는 아키텍처"
ms.assetid: 4e6a837d-e64f-45a0-87b7-aa02688a75f3
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/30/2017
ms.author: glenga
ms.openlocfilehash: e007acd75a2210d54f512e2c6698c90919f0fcd2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-queue-storage-bindings"></a><span data-ttu-id="7acd5-104">Azure Functions Queue Storage 바인딩</span><span class="sxs-lookup"><span data-stu-id="7acd5-104">Azure Functions Queue Storage bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="7acd5-105">이 문서에서는 Azure Functions에서 Azure Queue Storage 큐 바인딩을 구성하고 코딩하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7acd5-105">This article describes how to configure and code Azure Queue storage bindings in Azure Functions.</span></span> <span data-ttu-id="7acd5-106">Azure Functions는 Azure 큐에 대한 트리거 및 출력 바인딩을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7acd5-106">Azure Functions supports trigger and output bindings for Azure queues.</span></span> <span data-ttu-id="7acd5-107">모든 바인딩에서 사용할 수 있는 기능은 [Azure Functions 트리거 및 바인딩 개념](functions-triggers-bindings.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7acd5-107">For features that are available in all bindings, see [Azure Functions triggers and bindings concepts](functions-triggers-bindings.md).</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="trigger"></a>

## <a name="queue-storage-trigger"></a><span data-ttu-id="7acd5-108">Queue Storage 트리거</span><span class="sxs-lookup"><span data-stu-id="7acd5-108">Queue storage trigger</span></span>
<span data-ttu-id="7acd5-109">Azure Queue Storage 트리거를 사용하면 새 메시지에 대해 Queue Storage를 모니터링하고 이에 대응할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7acd5-109">The Azure Queue storage trigger enables you to monitor a queue storage for new messages and react to them.</span></span> 

<span data-ttu-id="7acd5-110">Functions 포털에서 **통합** 탭을 사용하여 큐 트리거를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="7acd5-110">Define a queue trigger using the **Integrate** tab in the Functions portal.</span></span> <span data-ttu-id="7acd5-111">이 포털에서는 *function.json*의 **bindings** 섹션에 다음 정의를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7acd5-111">The portal creates the following definition in the  **bindings** section of *function.json*:</span></span>

```json
{
    "type": "queueTrigger",
    "direction": "in",
    "name": "<The name used to identify the trigger data in your code>",
    "queueName": "<Name of queue to poll>",
    "connection":"<Name of app setting - see below>"
}
```

* <span data-ttu-id="7acd5-112">`connection` 속성은 저장소 연결 문자열을 포함하는 앱 설정의 이름을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7acd5-112">The `connection` property must contain the name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="7acd5-113">Azure Portal에서 **통합** 탭에 있는 표준 편집기는 저장소 계정을 선택하는 경우 이 앱 설정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="7acd5-113">In the Azure portal, the standard editor in the **Integrate** tab configures this app setting for you when you select a storage account.</span></span>

<span data-ttu-id="7acd5-114">host.json 파일에 [추가 설정](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json)을 입력하여 Queue Storage 트리거를 더욱 세밀하게 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7acd5-114">Additional settings can be provided in a [host.json file](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) to further fine-tune queue storage triggers.</span></span> <span data-ttu-id="7acd5-115">예를 들어 host.json에서 큐 폴링 간격을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7acd5-115">For example, you can change the queue polling interval in host.json.</span></span>

<a name="triggerusage"></a>

## <a name="using-a-queue-trigger"></a><span data-ttu-id="7acd5-116">큐 트리거 사용</span><span class="sxs-lookup"><span data-stu-id="7acd5-116">Using a queue trigger</span></span>
<span data-ttu-id="7acd5-117">Node.js 함수에서는 `context.bindings.<name>`을 사용하여 큐 데이터에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="7acd5-117">In Node.js functions, access the queue data using `context.bindings.<name>`.</span></span>


<span data-ttu-id="7acd5-118">.NET 함수에서는 `CloudQueueMessage paramName`과 같은 메서드 매개 변수를 사용하여 큐 페이로드에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="7acd5-118">In .NET functions, access the queue payload using a method parameter such as `CloudQueueMessage paramName`.</span></span> <span data-ttu-id="7acd5-119">여기에서 `paramName`은 [트리거 구성](#trigger)에서 지정한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="7acd5-119">Here, `paramName` is the value you specified in the [trigger configuration](#trigger).</span></span> <span data-ttu-id="7acd5-120">큐 메시지를 다음 중 원하는 형식으로 역직렬화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7acd5-120">The queue message can be deserialized to any of the following types:</span></span>

* <span data-ttu-id="7acd5-121">POCO 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="7acd5-121">POCO object.</span></span> <span data-ttu-id="7acd5-122">큐 페이로드가 JSON 개체인 경우에 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7acd5-122">Use if the queue payload is a JSON object.</span></span> <span data-ttu-id="7acd5-123">Functions 런타임은 페이로드를 POCO 개체로 deserialize합니다.</span><span class="sxs-lookup"><span data-stu-id="7acd5-123">The Functions runtime deserializes the payload into the POCO object.</span></span> 
* `string`
* `byte[]`
* [`CloudQueueMessage`]

<a name="meta"></a>

### <a name="queue-trigger-metadata"></a><span data-ttu-id="7acd5-124">큐 트리거 메타데이터</span><span class="sxs-lookup"><span data-stu-id="7acd5-124">Queue trigger metadata</span></span>
<span data-ttu-id="7acd5-125">큐 트리거는 몇 가지 메타데이터 속성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7acd5-125">The queue trigger provides several metadata properties.</span></span> <span data-ttu-id="7acd5-126">이러한 속성을 다른 바인딩에서 바인딩 식의 일부로 사용하거나 코드에서 매개 변수로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7acd5-126">These properties can be used as part of binding expressions in other bindings or as parameters in your code.</span></span> <span data-ttu-id="7acd5-127">값은 [`CloudQueueMessage`]와 동일한 의미 체계를 가집니다.</span><span class="sxs-lookup"><span data-stu-id="7acd5-127">The values have the same semantics as [`CloudQueueMessage`].</span></span>

* <span data-ttu-id="7acd5-128">**QueueTrigger** - 큐 페이로드(유효한 문자열인 경우)</span><span class="sxs-lookup"><span data-stu-id="7acd5-128">**QueueTrigger** - queue payload (if a valid string)</span></span>
* <span data-ttu-id="7acd5-129">**DequeueCount** - `int` 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="7acd5-129">**DequeueCount** - Type `int`.</span></span> <span data-ttu-id="7acd5-130">이 메시지가 큐에서 제거된 횟수입니다.</span><span class="sxs-lookup"><span data-stu-id="7acd5-130">The number of times this message has been dequeued.</span></span>
* <span data-ttu-id="7acd5-131">**ExpirationTime** - `DateTimeOffset?` 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="7acd5-131">**ExpirationTime** - Type `DateTimeOffset?`.</span></span> <span data-ttu-id="7acd5-132">메시지가 만료되는 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="7acd5-132">The time that the message expires.</span></span>
* <span data-ttu-id="7acd5-133">**Id** - `string` 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="7acd5-133">**Id** - Type `string`.</span></span> <span data-ttu-id="7acd5-134">큐 메시지 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="7acd5-134">Queue message ID.</span></span>
* <span data-ttu-id="7acd5-135">**InsertionTime** - `DateTimeOffset?` 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="7acd5-135">**InsertionTime** - Type `DateTimeOffset?`.</span></span> <span data-ttu-id="7acd5-136">메시지가 큐에 추가된 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="7acd5-136">The time that the message was added to the queue.</span></span>
* <span data-ttu-id="7acd5-137">**NextVisibleTime** - `DateTimeOffset?` 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="7acd5-137">**NextVisibleTime** - Type `DateTimeOffset?`.</span></span> <span data-ttu-id="7acd5-138">다음에 메시지가 표시되는 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="7acd5-138">The time that the message will next be visible.</span></span>
* <span data-ttu-id="7acd5-139">**PopReceipt** - `string` 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="7acd5-139">**PopReceipt** - Type `string`.</span></span> <span data-ttu-id="7acd5-140">메시지의 PopReceipt입니다.</span><span class="sxs-lookup"><span data-stu-id="7acd5-140">The message's pop receipt.</span></span>

<span data-ttu-id="7acd5-141">[트리거 샘플](#triggersample)에서 큐 메타데이터를 사용하는 방법을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7acd5-141">See how to use the queue metadata in [Trigger sample](#triggersample).</span></span>

<a name="triggersample"></a>

## <a name="trigger-sample"></a><span data-ttu-id="7acd5-142">트리거 샘플</span><span class="sxs-lookup"><span data-stu-id="7acd5-142">Trigger sample</span></span>
<span data-ttu-id="7acd5-143">큐 트리거를 정의하는 다음과 같은 function.json이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="7acd5-143">Suppose you have the following function.json that defines a queue trigger:</span></span>

```json
{
    "disabled": false,
    "bindings": [
        {
            "type": "queueTrigger",
            "direction": "in",
            "name": "myQueueItem",
            "queueName": "myqueue-items",
            "connection":"MyStorageConnectionString"
        }
    ]
}
```

<span data-ttu-id="7acd5-144">큐 메타데이터를 검색하고 기록하는 언어별 샘플을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7acd5-144">See the language-specific sample that retrieves and logs queue metadata.</span></span>

* [<span data-ttu-id="7acd5-145">C#</span><span class="sxs-lookup"><span data-stu-id="7acd5-145">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="7acd5-146">Node.JS</span><span class="sxs-lookup"><span data-stu-id="7acd5-146">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="7acd5-147">C#에서 트리거 샘플</span><span class="sxs-lookup"><span data-stu-id="7acd5-147">Trigger sample in C#</span></span> #
```csharp
#r "Microsoft.WindowsAzure.Storage"

using Microsoft.WindowsAzure.Storage.Queue;
using System;

public static void Run(CloudQueueMessage myQueueItem, 
    DateTimeOffset expirationTime, 
    DateTimeOffset insertionTime, 
    DateTimeOffset nextVisibleTime,
    string queueTrigger,
    string id,
    string popReceipt,
    int dequeueCount,
    TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem.AsString}\n" +
        $"queueTrigger={queueTrigger}\n" +
        $"expirationTime={expirationTime}\n" +
        $"insertionTime={insertionTime}\n" +
        $"nextVisibleTime={nextVisibleTime}\n" +
        $"id={id}\n" +
        $"popReceipt={popReceipt}\n" + 
        $"dequeueCount={dequeueCount}");
}
```

<!--
<a name="triggerfsharp"></a>
### Trigger sample in F# ## 
```fsharp

```
-->

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="7acd5-148">Node.js에서 트리거 샘플</span><span class="sxs-lookup"><span data-stu-id="7acd5-148">Trigger sample in Node.js</span></span>

```javascript
module.exports = function (context) {
    context.log('Node.js queue trigger function processed work item', context.bindings.myQueueItem);
    context.log('queueTrigger =', context.bindingData.queueTrigger);
    context.log('expirationTime =', context.bindingData.expirationTime);
    context.log('insertionTime =', context.bindingData.insertionTime);
    context.log('nextVisibleTime =', context.bindingData.nextVisibleTime);
    context.log('id=', context.bindingData.id);
    context.log('popReceipt =', context.bindingData.popReceipt);
    context.log('dequeueCount =', context.bindingData.dequeueCount);
    context.done();
};
```

### <a name="handling-poison-queue-messages"></a><span data-ttu-id="7acd5-149">포이즌 큐 메시지 처리</span><span class="sxs-lookup"><span data-stu-id="7acd5-149">Handling poison queue messages</span></span>
<span data-ttu-id="7acd5-150">큐 트리거 함수가 실패하는 경우 Azure Functions는 해당 함수를 지정된 큐 메시지에 대해 최대 5번(첫 번째 시도 포함) 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="7acd5-150">When a queue trigger function fails, Azure Functions retries that function up to five times for a given queue message, including the first try.</span></span> <span data-ttu-id="7acd5-151">5번 모두 실패할 경우 Functions 런타임은 *&lt;originalqueuename>-poison*이라는 Queue Storage에 메시지를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7acd5-151">If all five attempts fail, the functions runtime adds a message to a queue storage named *&lt;originalqueuename>-poison*.</span></span> <span data-ttu-id="7acd5-152">메시지를 기록하거나 수동 작업이 필요하다는 알림을 보내 포이즌 큐의 메시지를 처리하는 함수를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7acd5-152">You can write a function to process messages from the poison queue by logging them or sending a  notification that manual attention is needed.</span></span> 

<span data-ttu-id="7acd5-153">포이즌 메시지를 수동으로 처리하려면 큐 메시지의 `dequeueCount`를 확인합니다([큐 트리거 메타데이터](#meta) 참조).</span><span class="sxs-lookup"><span data-stu-id="7acd5-153">To handle poison messages manually, check the `dequeueCount` of the queue message (see [Queue trigger metadata](#meta)).</span></span>

<a name="output"></a>

## <a name="queue-storage-output-binding"></a><span data-ttu-id="7acd5-154">Queue Storage 출력 바인딩</span><span class="sxs-lookup"><span data-stu-id="7acd5-154">Queue storage output binding</span></span>
<span data-ttu-id="7acd5-155">Azure Queue Storage 출력 바인딩을 사용하면 메시지를 큐에 쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7acd5-155">The Azure queue storage output binding enables you to write messages to a queue.</span></span> 

<span data-ttu-id="7acd5-156">Functions 포털에서 **통합** 탭을 사용하여 큐 출력 바인딩을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="7acd5-156">Define a queue output binding using the **Integrate** tab in the Functions portal.</span></span> <span data-ttu-id="7acd5-157">이 포털에서는 *function.json*의 **bindings** 섹션에 다음 정의를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7acd5-157">The portal creates the following definition in the  **bindings** section of *function.json*:</span></span>

```json
{
   "type": "queue",
   "direction": "out",
   "name": "<The name used to identify the trigger data in your code>",
   "queueName": "<Name of queue to write to>",
   "connection":"<Name of app setting - see below>"
}
```

* <span data-ttu-id="7acd5-158">`connection` 속성은 저장소 연결 문자열을 포함하는 앱 설정의 이름을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7acd5-158">The `connection` property must contain the name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="7acd5-159">Azure Portal에서 **통합** 탭에 있는 표준 편집기는 저장소 계정을 선택하는 경우 이 앱 설정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="7acd5-159">In the Azure portal, the standard editor in the **Integrate** tab configures this app setting for you when you select a storage account.</span></span>

<a name="outputusage"></a>

## <a name="using-a-queue-output-binding"></a><span data-ttu-id="7acd5-160">큐 출력 바인딩 사용</span><span class="sxs-lookup"><span data-stu-id="7acd5-160">Using a queue output binding</span></span>
<span data-ttu-id="7acd5-161">Node.js 함수에서는 `context.bindings.<name>`을 사용하여 출력 큐에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="7acd5-161">In Node.js functions, you access the output queue using `context.bindings.<name>`.</span></span>

<span data-ttu-id="7acd5-162">.NET 함수에서는 다음 중 원하는 형식으로 출력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7acd5-162">In .NET functions, you can output to any of the following types.</span></span> <span data-ttu-id="7acd5-163">형식 매개 변수 `T`가 있는 경우 `T`는 지원되는 출력 형식(예: `string` 또는 POCO) 중 하나여야 합니다</span><span class="sxs-lookup"><span data-stu-id="7acd5-163">When there is a type parameter `T`, `T` must be one of the supported output types, such as `string` or a POCO.</span></span>

* <span data-ttu-id="7acd5-164">`out T`(JSON으로 serialize됨)</span><span class="sxs-lookup"><span data-stu-id="7acd5-164">`out T` (serialized as JSON)</span></span>
* `out string`
* `out byte[]`
* <span data-ttu-id="7acd5-165">`out` [`CloudQueueMessage`]</span><span class="sxs-lookup"><span data-stu-id="7acd5-165">`out` [`CloudQueueMessage`]</span></span> 
* `ICollector<T>`
* `IAsyncCollector<T>`
* [`CloudQueue`](/dotnet/api/microsoft.windowsazure.storage.queue.cloudqueue)

<span data-ttu-id="7acd5-166">또한 메서드 반환 형식을 출력 바인딩으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7acd5-166">You can also use the method return type as the output binding.</span></span>

<a name="outputsample"></a>

## <a name="queue-output-sample"></a><span data-ttu-id="7acd5-167">큐 출력 샘플</span><span class="sxs-lookup"><span data-stu-id="7acd5-167">Queue output sample</span></span>
<span data-ttu-id="7acd5-168">다음 *function.json*은 큐 출력 바인딩을 사용하여 HTTP 트리거를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="7acd5-168">The following *function.json* defines an HTTP trigger with a queue output binding:</span></span>

```json
{
  "bindings": [
    {
      "type": "httpTrigger",
      "direction": "in",
      "authLevel": "function",
      "name": "input"
    },
    {
      "type": "http",
      "direction": "out",
      "name": "return"
    },
    {
      "type": "queue",
      "direction": "out",
      "name": "$return",
      "queueName": "outqueue",
      "connection": "MyStorageConnectionString",
    }
  ]
}
``` 

<span data-ttu-id="7acd5-169">들어오는 HTTP 페이로드가 포함된 큐 메시지를 출력하는 언어별 샘플을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7acd5-169">See the language-specific sample that outputs a queue message with the incoming HTTP payload.</span></span>

* [<span data-ttu-id="7acd5-170">C#</span><span class="sxs-lookup"><span data-stu-id="7acd5-170">C#</span></span>](#outcsharp)
* [<span data-ttu-id="7acd5-171">Node.JS</span><span class="sxs-lookup"><span data-stu-id="7acd5-171">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="queue-output-sample-in-c"></a><span data-ttu-id="7acd5-172">C#의 큐 출력 샘플</span><span class="sxs-lookup"><span data-stu-id="7acd5-172">Queue output sample in C#</span></span> #

```cs
// C# example of HTTP trigger binding to a custom POCO, with a queue output binding
public class CustomQueueMessage
{
    public string PersonName { get; set; }
    public string Title { get; set; }
}

public static CustomQueueMessage Run(CustomQueueMessage input, TraceWriter log)
{
    return input;
}
```

<span data-ttu-id="7acd5-173">여러 메시지를 보내려면 `ICollector`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7acd5-173">To send multiple messages, use an `ICollector`:</span></span>

```cs
public static void Run(CustomQueueMessage input, ICollector<CustomQueueMessage> myQueueItem, TraceWriter log)
{
    myQueueItem.Add(input);
    myQueueItem.Add(new CustomQueueMessage { PersonName = "You", Title = "None" });
}
```

<a name="outnodejs"></a>

### <a name="queue-output-sample-in-nodejs"></a><span data-ttu-id="7acd5-174">Node.js의 큐 출력 샘플</span><span class="sxs-lookup"><span data-stu-id="7acd5-174">Queue output sample in Node.js</span></span>

```javascript
module.exports = function (context, input) {
    context.done(null, input.body);
};
```

<span data-ttu-id="7acd5-175">또는 여러 메시지를 전송하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7acd5-175">Or, to send multiple messages,</span></span>

```javascript
module.exports = function(context) {
    // Define a message array for the myQueueItem output binding. 
    context.bindings.myQueueItem = ["message 1","message 2"];
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="7acd5-176">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7acd5-176">Next steps</span></span>

<span data-ttu-id="7acd5-177">Queue Storage 트리거 및 바인딩을 사용하는 함수의 예제는 [Azure 서비스에 연결된 Azure Function 만들기](functions-create-an-azure-connected-function.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7acd5-177">For an example of a function that uses queue storage triggers and bindings, see [Create an Azure Function connected to an Azure service](functions-create-an-azure-connected-function.md).</span></span>

[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

<!-- LINKS -->

[`CloudQueueMessage`]: /dotnet/api/microsoft.windowsazure.storage.queue.cloudqueuemessage

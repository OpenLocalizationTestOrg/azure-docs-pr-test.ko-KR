---
title: "aaaAzure 함수 큐 저장소 바인딩 | Microsoft Docs"
description: "Toouse Azure 저장소의 트리거 방법 및 Azure 함수에서 바인딩 이해 합니다."
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
ms.openlocfilehash: 438b4f63e823149072c86fdefa7e15bfd2a2c4df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-queue-storage-bindings"></a><span data-ttu-id="0ce7c-104">Azure Functions Queue Storage 바인딩</span><span class="sxs-lookup"><span data-stu-id="0ce7c-104">Azure Functions Queue Storage bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="0ce7c-105">이 문서에서는 설명 어떻게 Azure 함수에서 tooconfigure 및 코드 Azure 큐 저장소 바인딩.</span><span class="sxs-lookup"><span data-stu-id="0ce7c-105">This article describes how tooconfigure and code Azure Queue storage bindings in Azure Functions.</span></span> <span data-ttu-id="0ce7c-106">Azure Functions는 Azure 큐에 대한 트리거 및 출력 바인딩을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0ce7c-106">Azure Functions supports trigger and output bindings for Azure queues.</span></span> <span data-ttu-id="0ce7c-107">모든 바인딩에서 사용할 수 있는 기능은 [Azure Functions 트리거 및 바인딩 개념](functions-triggers-bindings.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0ce7c-107">For features that are available in all bindings, see [Azure Functions triggers and bindings concepts](functions-triggers-bindings.md).</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="trigger"></a>

## <a name="queue-storage-trigger"></a><span data-ttu-id="0ce7c-108">Queue Storage 트리거</span><span class="sxs-lookup"><span data-stu-id="0ce7c-108">Queue storage trigger</span></span>
<span data-ttu-id="0ce7c-109">hello Azure 큐 저장소 트리거 새 메시지에 대 한 큐 저장소 toomonitor 있으며 특정 toothem 반응 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ce7c-109">hello Azure Queue storage trigger enables you toomonitor a queue storage for new messages and react toothem.</span></span> 

<span data-ttu-id="0ce7c-110">Hello를 사용 하 여 큐 트리거를 정의한 다음 **통합** hello 함수 포털에서 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ce7c-110">Define a queue trigger using hello **Integrate** tab in hello Functions portal.</span></span> <span data-ttu-id="0ce7c-111">hello 포털에서는 다음 hello에 정의 된 hello **바인딩** 섹션 *function.json*:</span><span class="sxs-lookup"><span data-stu-id="0ce7c-111">hello portal creates hello following definition in hello  **bindings** section of *function.json*:</span></span>

```json
{
    "type": "queueTrigger",
    "direction": "in",
    "name": "<hello name used tooidentify hello trigger data in your code>",
    "queueName": "<Name of queue toopoll>",
    "connection":"<Name of app setting - see below>"
}
```

* <span data-ttu-id="0ce7c-112">hello `connection` 저장소 연결 문자열을 포함 하는 응용 프로그램 설정의 hello 이름을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ce7c-112">hello `connection` property must contain hello name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="0ce7c-113">Hello Azure 포털에서에서 hello의 표준 편집기 hello **통합** 탭 저장소 계정을 선택할 때 응용 프로그램 설정을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ce7c-113">In hello Azure portal, hello standard editor in hello **Integrate** tab configures this app setting for you when you select a storage account.</span></span>

<span data-ttu-id="0ce7c-114">추가 설정을 제공 될 수 있습니다는 [host.json 파일](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) toofurther 큐 저장소 트리거 미세 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ce7c-114">Additional settings can be provided in a [host.json file](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) toofurther fine-tune queue storage triggers.</span></span> <span data-ttu-id="0ce7c-115">예를 들어 host.json hello 큐 폴링 간격을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ce7c-115">For example, you can change hello queue polling interval in host.json.</span></span>

<a name="triggerusage"></a>

## <a name="using-a-queue-trigger"></a><span data-ttu-id="0ce7c-116">큐 트리거 사용</span><span class="sxs-lookup"><span data-stu-id="0ce7c-116">Using a queue trigger</span></span>
<span data-ttu-id="0ce7c-117">Node.js 함수에서 사용 하 여 hello 큐 데이터에 액세스 `context.bindings.<name>`합니다.</span><span class="sxs-lookup"><span data-stu-id="0ce7c-117">In Node.js functions, access hello queue data using `context.bindings.<name>`.</span></span>


<span data-ttu-id="0ce7c-118">.NET 함수에 액세스 등의 메서드 매개 변수를 사용 하 여 hello 큐 페이로드 `CloudQueueMessage paramName`합니다.</span><span class="sxs-lookup"><span data-stu-id="0ce7c-118">In .NET functions, access hello queue payload using a method parameter such as `CloudQueueMessage paramName`.</span></span> <span data-ttu-id="0ce7c-119">여기에서 `paramName` hello에 지정 된 hello 값인 [트리거 구성](#trigger)합니다.</span><span class="sxs-lookup"><span data-stu-id="0ce7c-119">Here, `paramName` is hello value you specified in hello [trigger configuration](#trigger).</span></span> <span data-ttu-id="0ce7c-120">hello 큐 메시지 유형만 hello의 역직렬화 된 tooany 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ce7c-120">hello queue message can be deserialized tooany of hello following types:</span></span>

* <span data-ttu-id="0ce7c-121">POCO 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="0ce7c-121">POCO object.</span></span> <span data-ttu-id="0ce7c-122">Hello 큐 페이로드는 JSON 개체는 경우 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ce7c-122">Use if hello queue payload is a JSON object.</span></span> <span data-ttu-id="0ce7c-123">hello 함수 런타임 hello POCO 개체에 hello 페이로드를 역직렬화합니다.</span><span class="sxs-lookup"><span data-stu-id="0ce7c-123">hello Functions runtime deserializes hello payload into hello POCO object.</span></span> 
* `string`
* `byte[]`
* [`CloudQueueMessage`]

<a name="meta"></a>

### <a name="queue-trigger-metadata"></a><span data-ttu-id="0ce7c-124">큐 트리거 메타데이터</span><span class="sxs-lookup"><span data-stu-id="0ce7c-124">Queue trigger metadata</span></span>
<span data-ttu-id="0ce7c-125">hello 큐 트리거 여러 메타 데이터 속성을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ce7c-125">hello queue trigger provides several metadata properties.</span></span> <span data-ttu-id="0ce7c-126">이러한 속성을 다른 바인딩에서 바인딩 식의 일부로 사용하거나 코드에서 매개 변수로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ce7c-126">These properties can be used as part of binding expressions in other bindings or as parameters in your code.</span></span> <span data-ttu-id="0ce7c-127">hello 값은 hello와 동일한 의미 체계 [ `CloudQueueMessage` ]합니다.</span><span class="sxs-lookup"><span data-stu-id="0ce7c-127">hello values have hello same semantics as [`CloudQueueMessage`].</span></span>

* <span data-ttu-id="0ce7c-128">**QueueTrigger** - 큐 페이로드(유효한 문자열인 경우)</span><span class="sxs-lookup"><span data-stu-id="0ce7c-128">**QueueTrigger** - queue payload (if a valid string)</span></span>
* <span data-ttu-id="0ce7c-129">**DequeueCount** - `int` 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="0ce7c-129">**DequeueCount** - Type `int`.</span></span> <span data-ttu-id="0ce7c-130">이 메시지를 큐에서 제거 된 횟수 만큼을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ce7c-130">hello number of times this message has been dequeued.</span></span>
* <span data-ttu-id="0ce7c-131">**ExpirationTime** - `DateTimeOffset?` 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="0ce7c-131">**ExpirationTime** - Type `DateTimeOffset?`.</span></span> <span data-ttu-id="0ce7c-132">hello 시간 hello 메시지 만료 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ce7c-132">hello time that hello message expires.</span></span>
* <span data-ttu-id="0ce7c-133">**Id** - `string` 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="0ce7c-133">**Id** - Type `string`.</span></span> <span data-ttu-id="0ce7c-134">큐 메시지 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="0ce7c-134">Queue message ID.</span></span>
* <span data-ttu-id="0ce7c-135">**InsertionTime** - `DateTimeOffset?` 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="0ce7c-135">**InsertionTime** - Type `DateTimeOffset?`.</span></span> <span data-ttu-id="0ce7c-136">hello 시간 hello 메시지 toohello 큐에 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0ce7c-136">hello time that hello message was added toohello queue.</span></span>
* <span data-ttu-id="0ce7c-137">**NextVisibleTime** - `DateTimeOffset?` 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="0ce7c-137">**NextVisibleTime** - Type `DateTimeOffset?`.</span></span> <span data-ttu-id="0ce7c-138">hello 시간 hello 메시지 옆 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ce7c-138">hello time that hello message will next be visible.</span></span>
* <span data-ttu-id="0ce7c-139">**PopReceipt** - `string` 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="0ce7c-139">**PopReceipt** - Type `string`.</span></span> <span data-ttu-id="0ce7c-140">hello 메시지의 popreceipt입니다.</span><span class="sxs-lookup"><span data-stu-id="0ce7c-140">hello message's pop receipt.</span></span>

<span data-ttu-id="0ce7c-141">어떻게 toouse hello에 큐 메타 데이터 참조 [트리거 샘플](#triggersample)합니다.</span><span class="sxs-lookup"><span data-stu-id="0ce7c-141">See how toouse hello queue metadata in [Trigger sample](#triggersample).</span></span>

<a name="triggersample"></a>

## <a name="trigger-sample"></a><span data-ttu-id="0ce7c-142">트리거 샘플</span><span class="sxs-lookup"><span data-stu-id="0ce7c-142">Trigger sample</span></span>
<span data-ttu-id="0ce7c-143">다음 function.json 큐 트리거를 정의 하는 hello 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ce7c-143">Suppose you have hello following function.json that defines a queue trigger:</span></span>

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

<span data-ttu-id="0ce7c-144">검색 하 고 큐 메타 데이터를 기록 하는 hello 언어 관련 샘플을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="0ce7c-144">See hello language-specific sample that retrieves and logs queue metadata.</span></span>

* [<span data-ttu-id="0ce7c-145">C#</span><span class="sxs-lookup"><span data-stu-id="0ce7c-145">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="0ce7c-146">Node.JS</span><span class="sxs-lookup"><span data-stu-id="0ce7c-146">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="0ce7c-147">C#에서 트리거 샘플</span><span class="sxs-lookup"><span data-stu-id="0ce7c-147">Trigger sample in C#</span></span> #
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

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="0ce7c-148">Node.js에서 트리거 샘플</span><span class="sxs-lookup"><span data-stu-id="0ce7c-148">Trigger sample in Node.js</span></span>

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

### <a name="handling-poison-queue-messages"></a><span data-ttu-id="0ce7c-149">포이즌 큐 메시지 처리</span><span class="sxs-lookup"><span data-stu-id="0ce7c-149">Handling poison queue messages</span></span>
<span data-ttu-id="0ce7c-150">큐 트리거 함수가 실패 하면 Azure 함수에 해당 함수 toofive 먼저 hello를 포함 하는 특정된 큐 메시지에 대 한 번 시도를 다시 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ce7c-150">When a queue trigger function fails, Azure Functions retries that function up toofive times for a given queue message, including hello first try.</span></span> <span data-ttu-id="0ce7c-151">모든 다섯 번의 시도가 실패 하는 경우 hello 함수 런타임에서 이라는 메시지 tooa 큐 저장소를 추가 하는  *&lt;originalqueuename >-포이즌*합니다.</span><span class="sxs-lookup"><span data-stu-id="0ce7c-151">If all five attempts fail, hello functions runtime adds a message tooa queue storage named *&lt;originalqueuename>-poison*.</span></span> <span data-ttu-id="0ce7c-152">작성할 수 있습니다 함수 tooprocess 메시지 hello 포이즌 큐에서 해당 로그 하거나 수동 주의가 필요한 알림을 보내기.</span><span class="sxs-lookup"><span data-stu-id="0ce7c-152">You can write a function tooprocess messages from hello poison queue by logging them or sending a  notification that manual attention is needed.</span></span> 

<span data-ttu-id="0ce7c-153">toohandle 포이즌 메시지 hello를 수동으로 확인 `dequeueCount` hello 큐 메시지의 (참조 [큐 트리거 메타 데이터](#meta)).</span><span class="sxs-lookup"><span data-stu-id="0ce7c-153">toohandle poison messages manually, check hello `dequeueCount` of hello queue message (see [Queue trigger metadata](#meta)).</span></span>

<a name="output"></a>

## <a name="queue-storage-output-binding"></a><span data-ttu-id="0ce7c-154">Queue Storage 출력 바인딩</span><span class="sxs-lookup"><span data-stu-id="0ce7c-154">Queue storage output binding</span></span>
<span data-ttu-id="0ce7c-155">Azure 큐 저장소 hello 출력 바인딩을 통해 toowrite 메시지 tooa 큐 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ce7c-155">hello Azure queue storage output binding enables you toowrite messages tooa queue.</span></span> 

<span data-ttu-id="0ce7c-156">큐 정의 hello를 사용 하 여 출력 바인딩 **통합** hello 함수 포털에서 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ce7c-156">Define a queue output binding using hello **Integrate** tab in hello Functions portal.</span></span> <span data-ttu-id="0ce7c-157">hello 포털에서는 다음 hello에 정의 된 hello **바인딩** 섹션 *function.json*:</span><span class="sxs-lookup"><span data-stu-id="0ce7c-157">hello portal creates hello following definition in hello  **bindings** section of *function.json*:</span></span>

```json
{
   "type": "queue",
   "direction": "out",
   "name": "<hello name used tooidentify hello trigger data in your code>",
   "queueName": "<Name of queue toowrite to>",
   "connection":"<Name of app setting - see below>"
}
```

* <span data-ttu-id="0ce7c-158">hello `connection` 저장소 연결 문자열을 포함 하는 응용 프로그램 설정의 hello 이름을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ce7c-158">hello `connection` property must contain hello name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="0ce7c-159">Hello Azure 포털에서에서 hello의 표준 편집기 hello **통합** 탭 저장소 계정을 선택할 때 응용 프로그램 설정을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ce7c-159">In hello Azure portal, hello standard editor in hello **Integrate** tab configures this app setting for you when you select a storage account.</span></span>

<a name="outputusage"></a>

## <a name="using-a-queue-output-binding"></a><span data-ttu-id="0ce7c-160">큐 출력 바인딩 사용</span><span class="sxs-lookup"><span data-stu-id="0ce7c-160">Using a queue output binding</span></span>
<span data-ttu-id="0ce7c-161">에서는 Node.js 함수를 사용 하 여 hello 출력 큐 액세스 `context.bindings.<name>`합니다.</span><span class="sxs-lookup"><span data-stu-id="0ce7c-161">In Node.js functions, you access hello output queue using `context.bindings.<name>`.</span></span>

<span data-ttu-id="0ce7c-162">.NET 함수 hello 유형만의 tooany를 출력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ce7c-162">In .NET functions, you can output tooany of hello following types.</span></span> <span data-ttu-id="0ce7c-163">형식 매개 변수의 경우 `T`, `T` 와 같은 지원 되는 hello 출력 형식 중 하나 여야 합니다 `string` 또는 POCO 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ce7c-163">When there is a type parameter `T`, `T` must be one of hello supported output types, such as `string` or a POCO.</span></span>

* <span data-ttu-id="0ce7c-164">`out T`(JSON으로 serialize됨)</span><span class="sxs-lookup"><span data-stu-id="0ce7c-164">`out T` (serialized as JSON)</span></span>
* `out string`
* `out byte[]`
* <span data-ttu-id="0ce7c-165">`out` [`CloudQueueMessage`]</span><span class="sxs-lookup"><span data-stu-id="0ce7c-165">`out` [`CloudQueueMessage`]</span></span> 
* `ICollector<T>`
* `IAsyncCollector<T>`
* [`CloudQueue`](/dotnet/api/microsoft.windowsazure.storage.queue.cloudqueue)

<span data-ttu-id="0ce7c-166">Hello로 hello 메서드 반환 형식을 사용할 수도 있습니다 출력 바인딩이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ce7c-166">You can also use hello method return type as hello output binding.</span></span>

<a name="outputsample"></a>

## <a name="queue-output-sample"></a><span data-ttu-id="0ce7c-167">큐 출력 샘플</span><span class="sxs-lookup"><span data-stu-id="0ce7c-167">Queue output sample</span></span>
<span data-ttu-id="0ce7c-168">hello 다음 *function.json* 큐와 HTTP 트리거는 정의 바인딩 출력:</span><span class="sxs-lookup"><span data-stu-id="0ce7c-168">hello following *function.json* defines an HTTP trigger with a queue output binding:</span></span>

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

<span data-ttu-id="0ce7c-169">들어오는 HTTP 페이로드 hello 큐 메시지를 출력 하는 hello 언어 관련 샘플을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="0ce7c-169">See hello language-specific sample that outputs a queue message with hello incoming HTTP payload.</span></span>

* [<span data-ttu-id="0ce7c-170">C#</span><span class="sxs-lookup"><span data-stu-id="0ce7c-170">C#</span></span>](#outcsharp)
* [<span data-ttu-id="0ce7c-171">Node.JS</span><span class="sxs-lookup"><span data-stu-id="0ce7c-171">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="queue-output-sample-in-c"></a><span data-ttu-id="0ce7c-172">C#의 큐 출력 샘플</span><span class="sxs-lookup"><span data-stu-id="0ce7c-172">Queue output sample in C#</span></span> #

```cs
// C# example of HTTP trigger binding tooa custom POCO, with a queue output binding
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

<span data-ttu-id="0ce7c-173">여러 개의 메시지를 사용 하 여 toosend는 `ICollector`:</span><span class="sxs-lookup"><span data-stu-id="0ce7c-173">toosend multiple messages, use an `ICollector`:</span></span>

```cs
public static void Run(CustomQueueMessage input, ICollector<CustomQueueMessage> myQueueItem, TraceWriter log)
{
    myQueueItem.Add(input);
    myQueueItem.Add(new CustomQueueMessage { PersonName = "You", Title = "None" });
}
```

<a name="outnodejs"></a>

### <a name="queue-output-sample-in-nodejs"></a><span data-ttu-id="0ce7c-174">Node.js의 큐 출력 샘플</span><span class="sxs-lookup"><span data-stu-id="0ce7c-174">Queue output sample in Node.js</span></span>

```javascript
module.exports = function (context, input) {
    context.done(null, input.body);
};
```

<span data-ttu-id="0ce7c-175">또는 toosend 여러 개의 메시지를</span><span class="sxs-lookup"><span data-stu-id="0ce7c-175">Or, toosend multiple messages,</span></span>

```javascript
module.exports = function(context) {
    // Define a message array for hello myQueueItem output binding. 
    context.bindings.myQueueItem = ["message 1","message 2"];
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="0ce7c-176">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0ce7c-176">Next steps</span></span>

<span data-ttu-id="0ce7c-177">예를 보려면 큐 저장소 트리거 및 바인딩을 사용 하는 함수 참조 [연결 된 Azure 함수 tooan Azure 서비스 만들기](functions-create-an-azure-connected-function.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0ce7c-177">For an example of a function that uses queue storage triggers and bindings, see [Create an Azure Function connected tooan Azure service](functions-create-an-azure-connected-function.md).</span></span>

[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

<!-- LINKS -->

[`CloudQueueMessage`]: /dotnet/api/microsoft.windowsazure.storage.queue.cloudqueuemessage

---
title: "Azure Functions Service Bus 트리거 및 바인딩 | Microsoft Docs"
description: "Azure Functions에서 Azure 서비스 버스 트리거 및 바인딩을 사용하는 방법을 파악합니다."
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: "Azure Functions, 함수, 이벤트 처리, 동적 계산, 서버를 사용하지 않는 아키텍처"
ms.assetid: daedacf0-6546-4355-a65c-50873e74f66b
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 04/01/2017
ms.author: glenga
ms.openlocfilehash: b3ee306cd37ebf88dc9369ccc2dc6c670557fd5a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-service-bus-bindings"></a><span data-ttu-id="b4b9b-104">Azure Functions Service Bus 바인딩</span><span class="sxs-lookup"><span data-stu-id="b4b9b-104">Azure Functions Service Bus bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="b4b9b-105">이 문서에서는 Azure Functions에서 Azure Service Bus 바인딩을 구성하고 사용하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b4b9b-105">This article explains how to configure and work with Azure Service Bus bindings in Azure Functions.</span></span> 

<span data-ttu-id="b4b9b-106">Azure Functions는 Service Bus 큐 및 토픽에 대한 트리거 및 출력 바인딩을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b4b9b-106">Azure Functions supports trigger and output bindings for Service Bus queues and topics.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="trigger"></a>

## <a name="service-bus-trigger"></a><span data-ttu-id="b4b9b-107">Service Bus 트리거</span><span class="sxs-lookup"><span data-stu-id="b4b9b-107">Service Bus trigger</span></span>
<span data-ttu-id="b4b9b-108">Service Bus 트리거를 사용하여 Service Bus 큐 또는 토픽의 메시지에 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="b4b9b-108">Use the Service Bus trigger to respond to messages from a Service Bus queue or topic.</span></span> 

<span data-ttu-id="b4b9b-109">함수에 대한 Service Bus 큐 및 토픽 트리거는 function.json의 `bindings` 배열에 있는 다음과 같은 JSON 개체로 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4b9b-109">The Service Bus queue and topic triggers are defined by the following JSON objects in the `bindings` array of function.json:</span></span>

* <span data-ttu-id="b4b9b-110">*큐* 트리거:</span><span class="sxs-lookup"><span data-stu-id="b4b9b-110">*queue* trigger:</span></span>

    ```json
    {
        "name" : "<Name of input parameter in function signature>",
        "queueName" : "<Name of the queue>",
        "connection" : "<Name of app setting that has your queue's connection string - see below>",
        "accessRights" : "<Access rights for the connection string - see below>",
        "type" : "serviceBusTrigger",
        "direction" : "in"
    }
    ```

* <span data-ttu-id="b4b9b-111">*토픽* 트리거:</span><span class="sxs-lookup"><span data-stu-id="b4b9b-111">*topic* trigger:</span></span>

    ```json
    {
        "name" : "<Name of input parameter in function signature>",
        "topicName" : "<Name of the topic>",
        "subscriptionName" : "<Name of the subscription>",
        "connection" : "<Name of app setting that has your topic's connection string - see below>",
        "accessRights" : "<Access rights for the connection string - see below>",
        "type" : "serviceBusTrigger",
        "direction" : "in"
    }
    ```

<span data-ttu-id="b4b9b-112">다음 사항에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="b4b9b-112">Note the following:</span></span>

* <span data-ttu-id="b4b9b-113">`connection`의 경우 Service Bus의 네임스페이스에 대한 연결 문자열을 포함하는 [함수 앱의 앱 설정을 만들고](functions-how-to-use-azure-function-app-settings.md), 다음으로 트리거의 `connection` 속성에서 앱 설정의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b4b9b-113">For `connection`, [create an app setting in your function app](functions-how-to-use-azure-function-app-settings.md) that contains the connection string to your Service Bus namespace, then specify the name of the app setting in the `connection` property in your trigger.</span></span> <span data-ttu-id="b4b9b-114">[관리 자격 증명 얻기](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials)에 나온 단계에 따라 연결 문자열을 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="b4b9b-114">You obtain the connection string by following the steps shown at [Obtain the management credentials](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span></span>
  <span data-ttu-id="b4b9b-115">연결 문자열은 서비스 버스 네임스페이스에 대한 것이어야 하며, 특정 큐 또는 항목으로 제한되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b4b9b-115">The connection string must be for a Service Bus namespace, not limited to a specific queue or topic.</span></span>
  <span data-ttu-id="b4b9b-116">`connection`을 비워두면 트리거는 기본 Service Bus 연결 문자열이 `AzureWebJobsServiceBus`라는 앱 설정에서 지정한 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="b4b9b-116">If you leave `connection` empty, the trigger assumes that a default Service Bus connection string is specified in an app setting named `AzureWebJobsServiceBus`.</span></span>
* <span data-ttu-id="b4b9b-117">`accessRights`의 경우 사용 가능한 값은 `manage` 및 `listen`입니다.</span><span class="sxs-lookup"><span data-stu-id="b4b9b-117">For `accessRights`, available values are `manage` and `listen`.</span></span> <span data-ttu-id="b4b9b-118">기본값은 `manage`이며, `connection`에 **관리** 권한이 있음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="b4b9b-118">The default is `manage`, which indicates that the `connection` has the **Manage** permission.</span></span> <span data-ttu-id="b4b9b-119">**관리** 권한이 없는 연결 문자열을 사용하는 경우 `accessRights`을 `listen`으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b4b9b-119">If you use a connection string that does not have the **Manage** permission, set `accessRights` to `listen`.</span></span> <span data-ttu-id="b4b9b-120">그렇지 않으면 함수 런타임은 관리 권한이 필요한 작업 시도를 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4b9b-120">Otherwise, the Functions runtime might fail trying to do operations that require manage rights.</span></span>

## <a name="trigger-behavior"></a><span data-ttu-id="b4b9b-121">트리거 동작</span><span class="sxs-lookup"><span data-stu-id="b4b9b-121">Trigger behavior</span></span>
* <span data-ttu-id="b4b9b-122">**단일 스레딩** - 기본적으로 함수 런타임은 여러 개의 메시지를 동시에 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="b4b9b-122">**Single-threading** - By default, the Functions runtime processes multiple messages concurrently.</span></span> <span data-ttu-id="b4b9b-123">런타임이 큐 또는 토픽 메시지를 한 번에 하나만 처리하도록 하려면, *host.json*에서 `serviceBus.maxConcurrentCalls`를 1로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b4b9b-123">To direct the runtime to process only a single queue or topic message at a time, set `serviceBus.maxConcurrentCalls` to 1 in *host.json*.</span></span> 
  <span data-ttu-id="b4b9b-124">*host.json*에 대한 자세한 내용은 [폴더 구조](functions-reference.md#folder-structure) 및 [host.json](https://github .com/Azure/azure-webjobs-sdk-script/wiki/host.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b4b9b-124">For information about *host.json*, see [Folder Structure](functions-reference.md#folder-structure) and [host.json](https://github .com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span>
* <span data-ttu-id="b4b9b-125">**포이즌 메시지 처리** - Service Bus는 Azure Functions 구성 또는 코드로 제어되거나 구성될 수 없는 자체 포이즌 메시지 처리를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b4b9b-125">**Poison message handling** - Service Bus does its own poison message handling, which can't be controlled or configured in Azure Functions configuration or code.</span></span> 
* <span data-ttu-id="b4b9b-126">**PeekLock 동작** - 함수 런타임은 [`PeekLock` 모드](../service-bus-messaging/service-bus-performance-improvements.md#receive-mode)로 메시지를 받아 함수가 정상적으로 완료된 경우 메시지에서 `Complete`를 호출하고, 함수가 실패한 경우 `Abandon`을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="b4b9b-126">**PeekLock behavior** - The Functions runtime receives a message in [`PeekLock` mode](../service-bus-messaging/service-bus-performance-improvements.md#receive-mode) and calls `Complete` on the message if the function finishes successfully, or calls `Abandon` if the function fails.</span></span> 
  <span data-ttu-id="b4b9b-127">함수가 `PeekLock` 시간 제한보다 오래 실행되는 경우 잠금이 자동으로 갱신됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4b9b-127">If the function runs longer than the `PeekLock` timeout, the lock is automatically renewed.</span></span>

<a name="triggerusage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="b4b9b-128">트리거 사용</span><span class="sxs-lookup"><span data-stu-id="b4b9b-128">Trigger usage</span></span>
<span data-ttu-id="b4b9b-129">이 섹션에서는 함수 코드에서 Service Bus 트리거를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b4b9b-129">This section shows you how to use your Service Bus trigger in your function code.</span></span> 

<span data-ttu-id="b4b9b-130">C# 및 F#에서 Service Bus 트리거 메시지를 다음 입력 형식 중 하나로 deserialize할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4b9b-130">In C# and F#, the Service Bus trigger message can be deserialized to any of the following input types:</span></span>

* <span data-ttu-id="b4b9b-131">`string` - 문자열 메시지에 유용</span><span class="sxs-lookup"><span data-stu-id="b4b9b-131">`string` - useful for string messages</span></span>
* <span data-ttu-id="b4b9b-132">`byte[]` - 이진 데이터에 유용</span><span class="sxs-lookup"><span data-stu-id="b4b9b-132">`byte[]` - useful for binary data</span></span>
* <span data-ttu-id="b4b9b-133">모든 [개체](https://msdn.microsoft.com/library/system.object.aspx) - JSON 직렬화 데이터에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="b4b9b-133">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized data.</span></span>
  <span data-ttu-id="b4b9b-134">사용자 지정 입력 형식을 선언하는 경우(예: `CustomType`), Azure Functions에서 지정된 형식에 JSON 데이터를 deserialize하려고 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="b4b9b-134">If you declare a custom input type, such as `CustomType`, Azure Functions tries to deserialize the JSON data into your specified type.</span></span>
* <span data-ttu-id="b4b9b-135">`BrokeredMessage` - [BrokeredMessage.GetBody<T>()](https://msdn.microsoft.com/library/hh144211.aspx) 메서드를 사용하는 deserialize된 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4b9b-135">`BrokeredMessage` - gives you the deserialized message with the [BrokeredMessage.GetBody<T>()](https://msdn.microsoft.com/library/hh144211.aspx) method.</span></span>

<span data-ttu-id="b4b9b-136">Node.js에서 Service Bus 트리거 메시지가 문자열 또는 JSON 개체로 함수에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4b9b-136">In Node.js, the Service Bus trigger message is passed into the function as either a string or JSON object.</span></span>

<a name="triggersample"></a>

## <a name="trigger-sample"></a><span data-ttu-id="b4b9b-137">트리거 샘플</span><span class="sxs-lookup"><span data-stu-id="b4b9b-137">Trigger sample</span></span>
<span data-ttu-id="b4b9b-138">다음과 같은 function.json이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="b4b9b-138">Suppose you have the following function.json:</span></span>

```json
{
"bindings": [
    {
    "queueName": "testqueue",
    "connection": "MyServiceBusConnection",
    "name": "myQueueItem",
    "type": "serviceBusTrigger",
    "direction": "in"
    }
],
"disabled": false
}
```

<span data-ttu-id="b4b9b-139">Service Bus 큐 메시지를 처리하는 언어별 샘플을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b4b9b-139">See the language-specific sample that processes a Service Bus queue message.</span></span>

* [<span data-ttu-id="b4b9b-140">C#</span><span class="sxs-lookup"><span data-stu-id="b4b9b-140">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="b4b9b-141">F#</span><span class="sxs-lookup"><span data-stu-id="b4b9b-141">F#</span></span>](#triggerfsharp)
* [<span data-ttu-id="b4b9b-142">Node.JS</span><span class="sxs-lookup"><span data-stu-id="b4b9b-142">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="b4b9b-143">C#에서 트리거 샘플</span><span class="sxs-lookup"><span data-stu-id="b4b9b-143">Trigger sample in C#</span></span> #

```cs
public static void Run(string myQueueItem, TraceWriter log)
{
    log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
}
```

<a name="triggerfsharp"></a>

### <a name="trigger-sample-in-f"></a><span data-ttu-id="b4b9b-144">F#에서 트리거 샘플</span><span class="sxs-lookup"><span data-stu-id="b4b9b-144">Trigger sample in F#</span></span> #

```fsharp
let Run(myQueueItem: string, log: TraceWriter) =
    log.Info(sprintf "F# ServiceBus queue trigger function processed message: %s" myQueueItem)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="b4b9b-145">Node.js에서 트리거 샘플</span><span class="sxs-lookup"><span data-stu-id="b4b9b-145">Trigger sample in Node.js</span></span>

```javascript
module.exports = function(context, myQueueItem) {
    context.log('Node.js ServiceBus queue trigger function processed message', myQueueItem);
    context.done();
};
```

<a name="output"></a>

## <a name="service-bus-output-binding"></a><span data-ttu-id="b4b9b-146">Service Bus 출력 바인딩</span><span class="sxs-lookup"><span data-stu-id="b4b9b-146">Service Bus output binding</span></span>
<span data-ttu-id="b4b9b-147">함수에 대한 Service Bus 큐 및 토픽 출력은 function.json의 `bindings` 배열에서 다음과 같은 JSON 개체를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b4b9b-147">The Service Bus queue and topic output for a function use the following JSON objects in the `bindings` array of function.json:</span></span>

* <span data-ttu-id="b4b9b-148">*큐* 출력:</span><span class="sxs-lookup"><span data-stu-id="b4b9b-148">*queue* output:</span></span>

    ```json
    {
        "name" : "<Name of output parameter in function signature>",
        "queueName" : "<Name of the queue>",
        "connection" : "<Name of app setting that has your queue's connection string - see below>",
        "accessRights" : "<Access rights for the connection string - see below>",
        "type" : "serviceBus",
        "direction" : "out"
    }
    ```
* <span data-ttu-id="b4b9b-149">*토픽* 출력:</span><span class="sxs-lookup"><span data-stu-id="b4b9b-149">*topic* output:</span></span>

    ```json
    {
        "name" : "<Name of output parameter in function signature>",
        "topicName" : "<Name of the topic>",
        "subscriptionName" : "<Name of the subscription>",
        "connection" : "<Name of app setting that has your topic's connection string - see below>",
        "accessRights" : "<Access rights for the connection string - see below>",
        "type" : "serviceBus",
        "direction" : "out"
    }
    ```

<span data-ttu-id="b4b9b-150">다음 사항에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="b4b9b-150">Note the following:</span></span>

* <span data-ttu-id="b4b9b-151">`connection`의 경우 Service Bus의 네임스페이스에 대한 연결 문자열을 포함하는 [함수 앱의 앱 설정을 만들고](functions-how-to-use-azure-function-app-settings.md), 다음으로 출력 바인딩의 `connection` 속성에서 앱 설정의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b4b9b-151">For `connection`, [create an app setting in your function app](functions-how-to-use-azure-function-app-settings.md) that contains the connection string to your Service Bus namespace, then specify the name of the app setting in the `connection` property in your output binding.</span></span> <span data-ttu-id="b4b9b-152">[관리 자격 증명 얻기](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials)에 나온 단계에 따라 연결 문자열을 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="b4b9b-152">You obtain the connection string by following the steps shown at [Obtain the management credentials](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span></span>
  <span data-ttu-id="b4b9b-153">연결 문자열은 서비스 버스 네임스페이스에 대한 것이어야 하며, 특정 큐 또는 항목으로 제한되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b4b9b-153">The connection string must be for a Service Bus namespace, not limited to a specific queue or topic.</span></span>
  <span data-ttu-id="b4b9b-154">`connection`을 비워두면 출력 바인딩은 기본 Service Bus 연결 문자열이 `AzureWebJobsServiceBus`라는 앱 설정에서 지정한 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="b4b9b-154">If you leave `connection` empty, the output binding assumes that a default Service Bus connection string is specified in an app setting named `AzureWebJobsServiceBus`.</span></span>
* <span data-ttu-id="b4b9b-155">`accessRights`의 경우 사용 가능한 값은 `manage` 및 `listen`입니다.</span><span class="sxs-lookup"><span data-stu-id="b4b9b-155">For `accessRights`, available values are `manage` and `listen`.</span></span> <span data-ttu-id="b4b9b-156">기본값은 `manage`이며, `connection`에 **관리** 권한이 있음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="b4b9b-156">The default is `manage`, which indicates that the `connection` has the **Manage** permission.</span></span> <span data-ttu-id="b4b9b-157">**관리** 권한이 없는 연결 문자열을 사용하는 경우 `accessRights`을 `listen`으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b4b9b-157">If you use a connection string that does not have the **Manage** permission, set `accessRights` to `listen`.</span></span> <span data-ttu-id="b4b9b-158">그렇지 않으면 함수 런타임은 관리 권한이 필요한 작업 시도를 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4b9b-158">Otherwise, the Functions runtime might fail trying to do operations that require manage rights.</span></span>

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="b4b9b-159">출력 사용</span><span class="sxs-lookup"><span data-stu-id="b4b9b-159">Output usage</span></span>
<span data-ttu-id="b4b9b-160">C# 및 F#에서 Azure Functions은 다음 형식으로부터 Service Bus 큐 메시지를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4b9b-160">In C# and F#, Azure Functions can create a Service Bus queue message from any of the following types:</span></span>

* <span data-ttu-id="b4b9b-161">모든 [개체](https://msdn.microsoft.com/library/system.object.aspx) - 매개 변수 정의는 `out T paramName`(C#)과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b4b9b-161">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - Parameter definition looks like `out T paramName` (C#).</span></span>
  <span data-ttu-id="b4b9b-162">함수는 JSON 메시지에 개체를 deserialize합니다.</span><span class="sxs-lookup"><span data-stu-id="b4b9b-162">Functions deserializes the object into a JSON message.</span></span> <span data-ttu-id="b4b9b-163">함수가 종료될 때 출력 값이 null이면 함수는 null 개체와 메시지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b4b9b-163">If the output value is null when the function exits, Functions creates the message with a null object.</span></span>
* <span data-ttu-id="b4b9b-164">`string` - 매개 변수 정의는 `out string paraName`(C#)과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b4b9b-164">`string` - Parameter definition looks like `out string paraName` (C#).</span></span> <span data-ttu-id="b4b9b-165">함수가 종료될 때 매개 변수 값이 null이 아닌 경우 함수는 메시지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b4b9b-165">If the parameter value is non-null when the function exits, Functions creates a message.</span></span>
* <span data-ttu-id="b4b9b-166">`byte[]` - 매개 변수 정의는 `out byte[] paraName`(C#)과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b4b9b-166">`byte[]` - Parameter definition looks like `out byte[] paraName` (C#).</span></span> <span data-ttu-id="b4b9b-167">함수가 종료될 때 매개 변수 값이 null이 아닌 경우 함수는 메시지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b4b9b-167">If the parameter value is non-null when the function exits, Functions creates a message.</span></span>
* <span data-ttu-id="b4b9b-168">`BrokeredMessage` 매개 변수 정의는 `out BrokeredMessage paraName`(C#)과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b4b9b-168">`BrokeredMessage` Parameter definition looks like `out BrokeredMessage paraName` (C#).</span></span> <span data-ttu-id="b4b9b-169">함수가 종료될 때 매개 변수 값이 null이 아닌 경우 함수는 메시지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b4b9b-169">If the parameter value is non-null when the function exits, Functions creates a message.</span></span>

<span data-ttu-id="b4b9b-170">C# 함수에서 여러 메시지를 만들려면, `ICollector<T>` 또는 `IAsyncCollector<T>`를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4b9b-170">For creating multiple messages in a C# function, you can use `ICollector<T>` or `IAsyncCollector<T>`.</span></span> <span data-ttu-id="b4b9b-171">메시지는 `Add` 메서드를 호출할 때 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4b9b-171">A message is created when you call the `Add` method.</span></span>

<span data-ttu-id="b4b9b-172">Node.js에서 문자열, 바이트 배열 또는 Javascript 개체(JSON으로 deserialize됨)를 `context.binding.<paramName>`에 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4b9b-172">In Node.js, you can assign a string, a byte array, or a Javascript object (deserialized into JSON) to `context.binding.<paramName>`.</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="b4b9b-173">출력 샘플</span><span class="sxs-lookup"><span data-stu-id="b4b9b-173">Output sample</span></span>
<span data-ttu-id="b4b9b-174">Service Bus 큐 출력을 정의하는 다음과 같은 function.json이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="b4b9b-174">Suppose you have the following function.json, that defines a Service Bus queue output:</span></span>

```json
{
    "bindings": [
        {
            "schedule": "0/15 * * * * *",
            "name": "myTimer",
            "runsOnStartup": true,
            "type": "timerTrigger",
            "direction": "in"
        },
        {
            "name": "outputSbQueue",
            "type": "serviceBus",
            "queueName": "testqueue",
            "connection": "MyServiceBusConnection",
            "direction": "out"
        }
    ],
    "disabled": false
}
```

<span data-ttu-id="b4b9b-175">Service Bus 큐에 메시지를 전송하는 언어별 샘플을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b4b9b-175">See the language-specific sample that sends a message to the service bus queue.</span></span>

* [<span data-ttu-id="b4b9b-176">C#</span><span class="sxs-lookup"><span data-stu-id="b4b9b-176">C#</span></span>](#outcsharp)
* [<span data-ttu-id="b4b9b-177">F#</span><span class="sxs-lookup"><span data-stu-id="b4b9b-177">F#</span></span>](#outfsharp)
* [<span data-ttu-id="b4b9b-178">Node.JS</span><span class="sxs-lookup"><span data-stu-id="b4b9b-178">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="b4b9b-179">C#에서 출력 샘플</span><span class="sxs-lookup"><span data-stu-id="b4b9b-179">Output sample in C#</span></span> #

```cs
public static void Run(TimerInfo myTimer, TraceWriter log, out string outputSbQueue)
{
    string message = $"Service Bus queue message created at: {DateTime.Now}";
    log.Info(message); 
    outputSbQueue = message;
}
```

<span data-ttu-id="b4b9b-180">또는 여러 메시지 만들려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b4b9b-180">Or, to create multiple messages:</span></span>

```cs
public static void Run(TimerInfo myTimer, TraceWriter log, ICollector<string> outputSbQueue)
{
    string message = $"Service Bus queue message created at: {DateTime.Now}";
    log.Info(message); 
    outputSbQueue.Add("1 " + message);
    outputSbQueue.Add("2 " + message);
}
```

<a name="outfsharp"></a>

### <a name="output-sample-in-f"></a><span data-ttu-id="b4b9b-181">F#에서 출력 샘플</span><span class="sxs-lookup"><span data-stu-id="b4b9b-181">Output sample in F#</span></span> #

```fsharp
let Run(myTimer: TimerInfo, log: TraceWriter, outputSbQueue: byref<string>) =
    let message = sprintf "Service Bus queue message created at: %s" (DateTime.Now.ToString())
    log.Info(message)
    outputSbQueue = message
```

<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a><span data-ttu-id="b4b9b-182">Node.js에서 출력 샘플</span><span class="sxs-lookup"><span data-stu-id="b4b9b-182">Output sample in Node.js</span></span>

```javascript
module.exports = function (context, myTimer) {
    var message = 'Service Bus queue message created at ' + timeStamp;
    context.log(message);   
    context.bindings.outputSbQueueMsg = message;
    context.done();
};
```

<span data-ttu-id="b4b9b-183">또는 여러 메시지 만들려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b4b9b-183">Or, to create multiple messages:</span></span>

```javascript
module.exports = function (context, myTimer) {
    var message = 'Service Bus queue message created at ' + timeStamp;
    context.log(message);   
    context.bindings.outputSbQueueMsg = [];
    context.bindings.outputSbQueueMsg.push("1 " + message);
    context.bindings.outputSbQueueMsg.push("2 " + message);
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="b4b9b-184">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b4b9b-184">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]


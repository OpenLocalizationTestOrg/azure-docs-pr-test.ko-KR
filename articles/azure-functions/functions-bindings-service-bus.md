---
title: "서비스 버스 함수 aaaAzure 트리거 및 바인딩 | Microsoft Docs"
description: "Azure 서비스 버스 toouse 트리거합니다 방법 및 Azure 함수에서 바인딩 이해 합니다."
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
ms.openlocfilehash: dff9e89bd3840b8c11f91cae41e13502afc7aa60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-service-bus-bindings"></a><span data-ttu-id="33bf1-104">Azure Functions Service Bus 바인딩</span><span class="sxs-lookup"><span data-stu-id="33bf1-104">Azure Functions Service Bus bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="33bf1-105">이 문서에서는 설명 어떻게 tooconfigure Azure 함수에서 Azure 서비스 버스 바인딩 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="33bf1-105">This article explains how tooconfigure and work with Azure Service Bus bindings in Azure Functions.</span></span> 

<span data-ttu-id="33bf1-106">Azure Functions는 Service Bus 큐 및 토픽에 대한 트리거 및 출력 바인딩을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="33bf1-106">Azure Functions supports trigger and output bindings for Service Bus queues and topics.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="trigger"></a>

## <a name="service-bus-trigger"></a><span data-ttu-id="33bf1-107">Service Bus 트리거</span><span class="sxs-lookup"><span data-stu-id="33bf1-107">Service Bus trigger</span></span>
<span data-ttu-id="33bf1-108">서비스 버스 큐 또는 항목에서 서비스 버스 트리거 toorespond toomessages hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="33bf1-108">Use hello Service Bus trigger toorespond toomessages from a Service Bus queue or topic.</span></span> 

<span data-ttu-id="33bf1-109">hello 서비스 버스 큐 및 항목 정의 된 트리거는 다음 JSON 개체에 hello hello에서 `bindings` 배열 function.json입니다.</span><span class="sxs-lookup"><span data-stu-id="33bf1-109">hello Service Bus queue and topic triggers are defined by hello following JSON objects in hello `bindings` array of function.json:</span></span>

* <span data-ttu-id="33bf1-110">*큐* 트리거:</span><span class="sxs-lookup"><span data-stu-id="33bf1-110">*queue* trigger:</span></span>

    ```json
    {
        "name" : "<Name of input parameter in function signature>",
        "queueName" : "<Name of hello queue>",
        "connection" : "<Name of app setting that has your queue's connection string - see below>",
        "accessRights" : "<Access rights for hello connection string - see below>",
        "type" : "serviceBusTrigger",
        "direction" : "in"
    }
    ```

* <span data-ttu-id="33bf1-111">*토픽* 트리거:</span><span class="sxs-lookup"><span data-stu-id="33bf1-111">*topic* trigger:</span></span>

    ```json
    {
        "name" : "<Name of input parameter in function signature>",
        "topicName" : "<Name of hello topic>",
        "subscriptionName" : "<Name of hello subscription>",
        "connection" : "<Name of app setting that has your topic's connection string - see below>",
        "accessRights" : "<Access rights for hello connection string - see below>",
        "type" : "serviceBusTrigger",
        "direction" : "in"
    }
    ```

<span data-ttu-id="33bf1-112">참고 hello 다음.</span><span class="sxs-lookup"><span data-stu-id="33bf1-112">Note hello following:</span></span>

* <span data-ttu-id="33bf1-113">에 대 한 `connection`, [함수 응용 프로그램에서 프로그램 응용 프로그램 설정을 만들려면](functions-how-to-use-azure-function-app-settings.md) hello 연결 문자열 tooyour 서비스 버스 네임 스페이스를 포함 하는, hello에 hello 앱 설정의 hello 이름을 지정 합니다 `connection` 트리거가의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="33bf1-113">For `connection`, [create an app setting in your function app](functions-how-to-use-azure-function-app-settings.md) that contains hello connection string tooyour Service Bus namespace, then specify hello name of hello app setting in hello `connection` property in your trigger.</span></span> <span data-ttu-id="33bf1-114">Hello 연결 문자열 부분에 표시 된 hello 단계에 따라 가져올 [hello 관리 자격 증명을 가져올](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials)합니다.</span><span class="sxs-lookup"><span data-stu-id="33bf1-114">You obtain hello connection string by following hello steps shown at [Obtain hello management credentials](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span></span>
  <span data-ttu-id="33bf1-115">서비스 버스 네임 스페이스, 제한 되지 tooa 특정 큐 또는 항목에 대 한 hello 연결 문자열 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="33bf1-115">hello connection string must be for a Service Bus namespace, not limited tooa specific queue or topic.</span></span>
  <span data-ttu-id="33bf1-116">두면 `connection` 기본 서비스 버스 연결 문자열 설정 명명 된 응용 프로그램에 지정 된 비어 있는 경우 hello 트리거 가정 `AzureWebJobsServiceBus`합니다.</span><span class="sxs-lookup"><span data-stu-id="33bf1-116">If you leave `connection` empty, hello trigger assumes that a default Service Bus connection string is specified in an app setting named `AzureWebJobsServiceBus`.</span></span>
* <span data-ttu-id="33bf1-117">`accessRights`의 경우 사용 가능한 값은 `manage` 및 `listen`입니다.</span><span class="sxs-lookup"><span data-stu-id="33bf1-117">For `accessRights`, available values are `manage` and `listen`.</span></span> <span data-ttu-id="33bf1-118">hello 기본값은 `manage`, 해당 hello 나타냅니다 `connection` hello에 **관리** 권한.</span><span class="sxs-lookup"><span data-stu-id="33bf1-118">hello default is `manage`, which indicates that hello `connection` has hello **Manage** permission.</span></span> <span data-ttu-id="33bf1-119">Hello 하지 않은 연결 문자열을 사용 하는 경우 **관리** 권한 설정 `accessRights` 너무`listen`합니다.</span><span class="sxs-lookup"><span data-stu-id="33bf1-119">If you use a connection string that does not have hello **Manage** permission, set `accessRights` too`listen`.</span></span> <span data-ttu-id="33bf1-120">그렇지 않으면 런타임 동안 toodo 필요한 작업에 실패할 수 있습니다 hello 함수 권한 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="33bf1-120">Otherwise, hello Functions runtime might fail trying toodo operations that require manage rights.</span></span>

## <a name="trigger-behavior"></a><span data-ttu-id="33bf1-121">트리거 동작</span><span class="sxs-lookup"><span data-stu-id="33bf1-121">Trigger behavior</span></span>
* <span data-ttu-id="33bf1-122">**단일 스레드** -기본적으로 메시지를 동시에 여러 hello 함수 런타임 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="33bf1-122">**Single-threading** - By default, hello Functions runtime processes multiple messages concurrently.</span></span> <span data-ttu-id="33bf1-123">toodirect hello 런타임 tooprocess만 단일 큐 또는 항목에서 메시지를 한 번 설정 `serviceBus.maxConcurrentCalls` 에 too1 *host.json*합니다.</span><span class="sxs-lookup"><span data-stu-id="33bf1-123">toodirect hello runtime tooprocess only a single queue or topic message at a time, set `serviceBus.maxConcurrentCalls` too1 in *host.json*.</span></span> 
  <span data-ttu-id="33bf1-124">*host.json*에 대한 자세한 내용은 [폴더 구조](functions-reference.md#folder-structure) 및 [host.json](https://github .com/Azure/azure-webjobs-sdk-script/wiki/host.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="33bf1-124">For information about *host.json*, see [Folder Structure](functions-reference.md#folder-structure) and [host.json](https://github .com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span>
* <span data-ttu-id="33bf1-125">**포이즌 메시지 처리** - Service Bus는 Azure Functions 구성 또는 코드로 제어되거나 구성될 수 없는 자체 포이즌 메시지 처리를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="33bf1-125">**Poison message handling** - Service Bus does its own poison message handling, which can't be controlled or configured in Azure Functions configuration or code.</span></span> 
* <span data-ttu-id="33bf1-126">**PeekLock 동작** -에 메시지를 수신 하는 hello 함수 런타임 [ `PeekLock` 모드](../service-bus-messaging/service-bus-performance-improvements.md#receive-mode) 및 호출 `Complete` hello 함수는 성공적으로 완료 되 면 hello 메시지 또는 호출 `Abandon` 경우 hello 함수가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="33bf1-126">**PeekLock behavior** - hello Functions runtime receives a message in [`PeekLock` mode](../service-bus-messaging/service-bus-performance-improvements.md#receive-mode) and calls `Complete` on hello message if hello function finishes successfully, or calls `Abandon` if hello function fails.</span></span> 
  <span data-ttu-id="33bf1-127">Hello 함수 hello 보다 오래 실행 되 면 `PeekLock` hello 잠금 제한 시간이 자동으로 갱신 합니다.</span><span class="sxs-lookup"><span data-stu-id="33bf1-127">If hello function runs longer than hello `PeekLock` timeout, hello lock is automatically renewed.</span></span>

<a name="triggerusage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="33bf1-128">트리거 사용</span><span class="sxs-lookup"><span data-stu-id="33bf1-128">Trigger usage</span></span>
<span data-ttu-id="33bf1-129">이 섹션에서는 어떻게 toouse 서비스 버스 트리거할 함수 코드를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="33bf1-129">This section shows you how toouse your Service Bus trigger in your function code.</span></span> 

<span data-ttu-id="33bf1-130">C# 및 F # hello 서비스 버스 트리거 메시지의 입력 유형만 hello 역직렬화 된 tooany 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33bf1-130">In C# and F#, hello Service Bus trigger message can be deserialized tooany of hello following input types:</span></span>

* <span data-ttu-id="33bf1-131">`string` - 문자열 메시지에 유용</span><span class="sxs-lookup"><span data-stu-id="33bf1-131">`string` - useful for string messages</span></span>
* <span data-ttu-id="33bf1-132">`byte[]` - 이진 데이터에 유용</span><span class="sxs-lookup"><span data-stu-id="33bf1-132">`byte[]` - useful for binary data</span></span>
* <span data-ttu-id="33bf1-133">모든 [개체](https://msdn.microsoft.com/library/system.object.aspx) - JSON 직렬화 데이터에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="33bf1-133">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized data.</span></span>
  <span data-ttu-id="33bf1-134">사용자 입력된 형식을 같이 선언 하는 경우 `CustomType`, Azure 함수에 지정 된 형식으로 toodeserialize hello JSON 데이터를 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="33bf1-134">If you declare a custom input type, such as `CustomType`, Azure Functions tries toodeserialize hello JSON data into your specified type.</span></span>
* <span data-ttu-id="33bf1-135">`BrokeredMessage`-제공 하면 hello hello로 메시지를 역직렬화 할 [BrokeredMessage.GetBody<T>()](https://msdn.microsoft.com/library/hh144211.aspx) 메서드.</span><span class="sxs-lookup"><span data-stu-id="33bf1-135">`BrokeredMessage` - gives you hello deserialized message with hello [BrokeredMessage.GetBody<T>()](https://msdn.microsoft.com/library/hh144211.aspx) method.</span></span>

<span data-ttu-id="33bf1-136">Node.js hello 서비스 버스 트리거 메시지 문자열 또는 JSON 개체 hello 함수에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="33bf1-136">In Node.js, hello Service Bus trigger message is passed into hello function as either a string or JSON object.</span></span>

<a name="triggersample"></a>

## <a name="trigger-sample"></a><span data-ttu-id="33bf1-137">트리거 샘플</span><span class="sxs-lookup"><span data-stu-id="33bf1-137">Trigger sample</span></span>
<span data-ttu-id="33bf1-138">다음 function.json hello 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="33bf1-138">Suppose you have hello following function.json:</span></span>

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

<span data-ttu-id="33bf1-139">서비스 버스 큐 메시지를 처리 하는 hello 언어 관련 샘플을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="33bf1-139">See hello language-specific sample that processes a Service Bus queue message.</span></span>

* [<span data-ttu-id="33bf1-140">C#</span><span class="sxs-lookup"><span data-stu-id="33bf1-140">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="33bf1-141">F#</span><span class="sxs-lookup"><span data-stu-id="33bf1-141">F#</span></span>](#triggerfsharp)
* [<span data-ttu-id="33bf1-142">Node.JS</span><span class="sxs-lookup"><span data-stu-id="33bf1-142">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="33bf1-143">C#에서 트리거 샘플</span><span class="sxs-lookup"><span data-stu-id="33bf1-143">Trigger sample in C#</span></span> #

```cs
public static void Run(string myQueueItem, TraceWriter log)
{
    log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
}
```

<a name="triggerfsharp"></a>

### <a name="trigger-sample-in-f"></a><span data-ttu-id="33bf1-144">F#에서 트리거 샘플</span><span class="sxs-lookup"><span data-stu-id="33bf1-144">Trigger sample in F#</span></span> #

```fsharp
let Run(myQueueItem: string, log: TraceWriter) =
    log.Info(sprintf "F# ServiceBus queue trigger function processed message: %s" myQueueItem)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="33bf1-145">Node.js에서 트리거 샘플</span><span class="sxs-lookup"><span data-stu-id="33bf1-145">Trigger sample in Node.js</span></span>

```javascript
module.exports = function(context, myQueueItem) {
    context.log('Node.js ServiceBus queue trigger function processed message', myQueueItem);
    context.done();
};
```

<a name="output"></a>

## <a name="service-bus-output-binding"></a><span data-ttu-id="33bf1-146">Service Bus 출력 바인딩</span><span class="sxs-lookup"><span data-stu-id="33bf1-146">Service Bus output binding</span></span>
<span data-ttu-id="33bf1-147">다음 JSON 개체에 hello hello를 사용 하는 hello 함수에 대 한 서비스 버스 큐 및 항목 출력 `bindings` function.json의 배열:</span><span class="sxs-lookup"><span data-stu-id="33bf1-147">hello Service Bus queue and topic output for a function use hello following JSON objects in hello `bindings` array of function.json:</span></span>

* <span data-ttu-id="33bf1-148">*큐* 출력:</span><span class="sxs-lookup"><span data-stu-id="33bf1-148">*queue* output:</span></span>

    ```json
    {
        "name" : "<Name of output parameter in function signature>",
        "queueName" : "<Name of hello queue>",
        "connection" : "<Name of app setting that has your queue's connection string - see below>",
        "accessRights" : "<Access rights for hello connection string - see below>",
        "type" : "serviceBus",
        "direction" : "out"
    }
    ```
* <span data-ttu-id="33bf1-149">*토픽* 출력:</span><span class="sxs-lookup"><span data-stu-id="33bf1-149">*topic* output:</span></span>

    ```json
    {
        "name" : "<Name of output parameter in function signature>",
        "topicName" : "<Name of hello topic>",
        "subscriptionName" : "<Name of hello subscription>",
        "connection" : "<Name of app setting that has your topic's connection string - see below>",
        "accessRights" : "<Access rights for hello connection string - see below>",
        "type" : "serviceBus",
        "direction" : "out"
    }
    ```

<span data-ttu-id="33bf1-150">참고 hello 다음.</span><span class="sxs-lookup"><span data-stu-id="33bf1-150">Note hello following:</span></span>

* <span data-ttu-id="33bf1-151">에 대 한 `connection`, [함수 응용 프로그램에서 프로그램 응용 프로그램 설정을 만들려면](functions-how-to-use-azure-function-app-settings.md) hello 연결 문자열 tooyour 서비스 버스 네임 스페이스를 포함 하, 다음 hello에 hello 앱 설정의 hello 이름 지정 `connection` 출력에는 속성 바인딩입니다.</span><span class="sxs-lookup"><span data-stu-id="33bf1-151">For `connection`, [create an app setting in your function app](functions-how-to-use-azure-function-app-settings.md) that contains hello connection string tooyour Service Bus namespace, then specify hello name of hello app setting in hello `connection` property in your output binding.</span></span> <span data-ttu-id="33bf1-152">Hello 연결 문자열 부분에 표시 된 hello 단계에 따라 가져올 [hello 관리 자격 증명을 가져올](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials)합니다.</span><span class="sxs-lookup"><span data-stu-id="33bf1-152">You obtain hello connection string by following hello steps shown at [Obtain hello management credentials](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span></span>
  <span data-ttu-id="33bf1-153">서비스 버스 네임 스페이스, 제한 되지 tooa 특정 큐 또는 항목에 대 한 hello 연결 문자열 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="33bf1-153">hello connection string must be for a Service Bus namespace, not limited tooa specific queue or topic.</span></span>
  <span data-ttu-id="33bf1-154">두면 `connection` 비어 hello 출력 바인딩 가정 기본 서비스 버스 연결 문자열 설정 명명 된 응용 프로그램에 지정 된 `AzureWebJobsServiceBus`합니다.</span><span class="sxs-lookup"><span data-stu-id="33bf1-154">If you leave `connection` empty, hello output binding assumes that a default Service Bus connection string is specified in an app setting named `AzureWebJobsServiceBus`.</span></span>
* <span data-ttu-id="33bf1-155">`accessRights`의 경우 사용 가능한 값은 `manage` 및 `listen`입니다.</span><span class="sxs-lookup"><span data-stu-id="33bf1-155">For `accessRights`, available values are `manage` and `listen`.</span></span> <span data-ttu-id="33bf1-156">hello 기본값은 `manage`, 해당 hello 나타냅니다 `connection` hello에 **관리** 권한.</span><span class="sxs-lookup"><span data-stu-id="33bf1-156">hello default is `manage`, which indicates that hello `connection` has hello **Manage** permission.</span></span> <span data-ttu-id="33bf1-157">Hello 하지 않은 연결 문자열을 사용 하는 경우 **관리** 권한 설정 `accessRights` 너무`listen`합니다.</span><span class="sxs-lookup"><span data-stu-id="33bf1-157">If you use a connection string that does not have hello **Manage** permission, set `accessRights` too`listen`.</span></span> <span data-ttu-id="33bf1-158">그렇지 않으면 런타임 동안 toodo 필요한 작업에 실패할 수 있습니다 hello 함수 권한 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="33bf1-158">Otherwise, hello Functions runtime might fail trying toodo operations that require manage rights.</span></span>

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="33bf1-159">출력 사용</span><span class="sxs-lookup"><span data-stu-id="33bf1-159">Output usage</span></span>
<span data-ttu-id="33bf1-160">C# 및 F #에서는 Azure 함수 유형만 hello 중 하나에서 서비스 버스 큐 메시지를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33bf1-160">In C# and F#, Azure Functions can create a Service Bus queue message from any of hello following types:</span></span>

* <span data-ttu-id="33bf1-161">모든 [개체](https://msdn.microsoft.com/library/system.object.aspx) - 매개 변수 정의는 `out T paramName`(C#)과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="33bf1-161">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - Parameter definition looks like `out T paramName` (C#).</span></span>
  <span data-ttu-id="33bf1-162">함수는 JSON 메시지를 hello 개체를 역직렬화 합니다.</span><span class="sxs-lookup"><span data-stu-id="33bf1-162">Functions deserializes hello object into a JSON message.</span></span> <span data-ttu-id="33bf1-163">Hello 함수가 종료 되 면 hello 출력 값이 null 이면 함수는 null 개체에 hello 메시지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="33bf1-163">If hello output value is null when hello function exits, Functions creates hello message with a null object.</span></span>
* <span data-ttu-id="33bf1-164">`string` - 매개 변수 정의는 `out string paraName`(C#)과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="33bf1-164">`string` - Parameter definition looks like `out string paraName` (C#).</span></span> <span data-ttu-id="33bf1-165">Hello 매개 변수 값이 null이 아닌 hello 함수가 종료 되 면 이면 함수는 메시지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="33bf1-165">If hello parameter value is non-null when hello function exits, Functions creates a message.</span></span>
* <span data-ttu-id="33bf1-166">`byte[]` - 매개 변수 정의는 `out byte[] paraName`(C#)과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="33bf1-166">`byte[]` - Parameter definition looks like `out byte[] paraName` (C#).</span></span> <span data-ttu-id="33bf1-167">Hello 매개 변수 값이 null이 아닌 hello 함수가 종료 되 면 이면 함수는 메시지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="33bf1-167">If hello parameter value is non-null when hello function exits, Functions creates a message.</span></span>
* <span data-ttu-id="33bf1-168">`BrokeredMessage` 매개 변수 정의는 `out BrokeredMessage paraName`(C#)과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="33bf1-168">`BrokeredMessage` Parameter definition looks like `out BrokeredMessage paraName` (C#).</span></span> <span data-ttu-id="33bf1-169">Hello 매개 변수 값이 null이 아닌 hello 함수가 종료 되 면 이면 함수는 메시지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="33bf1-169">If hello parameter value is non-null when hello function exits, Functions creates a message.</span></span>

<span data-ttu-id="33bf1-170">C# 함수에서 여러 메시지를 만들려면, `ICollector<T>` 또는 `IAsyncCollector<T>`를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33bf1-170">For creating multiple messages in a C# function, you can use `ICollector<T>` or `IAsyncCollector<T>`.</span></span> <span data-ttu-id="33bf1-171">Hello를 호출 하는 경우 메시지를 만들 `Add` 메서드.</span><span class="sxs-lookup"><span data-stu-id="33bf1-171">A message is created when you call hello `Add` method.</span></span>

<span data-ttu-id="33bf1-172">Node.js에서 문자열, 바이트 배열 또는 Javascript 개체 (JSON으로 역직렬화 할) 너무를 할당할 수`context.binding.<paramName>`합니다.</span><span class="sxs-lookup"><span data-stu-id="33bf1-172">In Node.js, you can assign a string, a byte array, or a Javascript object (deserialized into JSON) too`context.binding.<paramName>`.</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="33bf1-173">출력 샘플</span><span class="sxs-lookup"><span data-stu-id="33bf1-173">Output sample</span></span>
<span data-ttu-id="33bf1-174">서비스 버스 큐 출력을 정의 하는 function.json 다음 hello 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="33bf1-174">Suppose you have hello following function.json, that defines a Service Bus queue output:</span></span>

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

<span data-ttu-id="33bf1-175">메시지 toohello 서비스 버스 큐에서 전송 하는 hello 언어 관련 샘플을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="33bf1-175">See hello language-specific sample that sends a message toohello service bus queue.</span></span>

* [<span data-ttu-id="33bf1-176">C#</span><span class="sxs-lookup"><span data-stu-id="33bf1-176">C#</span></span>](#outcsharp)
* [<span data-ttu-id="33bf1-177">F#</span><span class="sxs-lookup"><span data-stu-id="33bf1-177">F#</span></span>](#outfsharp)
* [<span data-ttu-id="33bf1-178">Node.JS</span><span class="sxs-lookup"><span data-stu-id="33bf1-178">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="33bf1-179">C#에서 출력 샘플</span><span class="sxs-lookup"><span data-stu-id="33bf1-179">Output sample in C#</span></span> #

```cs
public static void Run(TimerInfo myTimer, TraceWriter log, out string outputSbQueue)
{
    string message = $"Service Bus queue message created at: {DateTime.Now}";
    log.Info(message); 
    outputSbQueue = message;
}
```

<span data-ttu-id="33bf1-180">또는 toocreate 여러 메시지:</span><span class="sxs-lookup"><span data-stu-id="33bf1-180">Or, toocreate multiple messages:</span></span>

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

### <a name="output-sample-in-f"></a><span data-ttu-id="33bf1-181">F#에서 출력 샘플</span><span class="sxs-lookup"><span data-stu-id="33bf1-181">Output sample in F#</span></span> #

```fsharp
let Run(myTimer: TimerInfo, log: TraceWriter, outputSbQueue: byref<string>) =
    let message = sprintf "Service Bus queue message created at: %s" (DateTime.Now.ToString())
    log.Info(message)
    outputSbQueue = message
```

<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a><span data-ttu-id="33bf1-182">Node.js에서 출력 샘플</span><span class="sxs-lookup"><span data-stu-id="33bf1-182">Output sample in Node.js</span></span>

```javascript
module.exports = function (context, myTimer) {
    var message = 'Service Bus queue message created at ' + timeStamp;
    context.log(message);   
    context.bindings.outputSbQueueMsg = message;
    context.done();
};
```

<span data-ttu-id="33bf1-183">또는 toocreate 여러 메시지:</span><span class="sxs-lookup"><span data-stu-id="33bf1-183">Or, toocreate multiple messages:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="33bf1-184">다음 단계</span><span class="sxs-lookup"><span data-stu-id="33bf1-184">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]


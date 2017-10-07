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
# <a name="azure-functions-queue-storage-bindings"></a>Azure Functions Queue Storage 바인딩
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

이 문서에서는 설명 어떻게 Azure 함수에서 tooconfigure 및 코드 Azure 큐 저장소 바인딩. Azure Functions는 Azure 큐에 대한 트리거 및 출력 바인딩을 지원합니다. 모든 바인딩에서 사용할 수 있는 기능은 [Azure Functions 트리거 및 바인딩 개념](functions-triggers-bindings.md)을 참조하세요.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="trigger"></a>

## <a name="queue-storage-trigger"></a>Queue Storage 트리거
hello Azure 큐 저장소 트리거 새 메시지에 대 한 큐 저장소 toomonitor 있으며 특정 toothem 반응 합니다. 

Hello를 사용 하 여 큐 트리거를 정의한 다음 **통합** hello 함수 포털에서 탭 합니다. hello 포털에서는 다음 hello에 정의 된 hello **바인딩** 섹션 *function.json*:

```json
{
    "type": "queueTrigger",
    "direction": "in",
    "name": "<hello name used tooidentify hello trigger data in your code>",
    "queueName": "<Name of queue toopoll>",
    "connection":"<Name of app setting - see below>"
}
```

* hello `connection` 저장소 연결 문자열을 포함 하는 응용 프로그램 설정의 hello 이름을 포함 해야 합니다. Hello Azure 포털에서에서 hello의 표준 편집기 hello **통합** 탭 저장소 계정을 선택할 때 응용 프로그램 설정을 구성 합니다.

추가 설정을 제공 될 수 있습니다는 [host.json 파일](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) toofurther 큐 저장소 트리거 미세 조정 합니다. 예를 들어 host.json hello 큐 폴링 간격을 변경할 수 있습니다.

<a name="triggerusage"></a>

## <a name="using-a-queue-trigger"></a>큐 트리거 사용
Node.js 함수에서 사용 하 여 hello 큐 데이터에 액세스 `context.bindings.<name>`합니다.


.NET 함수에 액세스 등의 메서드 매개 변수를 사용 하 여 hello 큐 페이로드 `CloudQueueMessage paramName`합니다. 여기에서 `paramName` hello에 지정 된 hello 값인 [트리거 구성](#trigger)합니다. hello 큐 메시지 유형만 hello의 역직렬화 된 tooany 될 수 있습니다.

* POCO 개체입니다. Hello 큐 페이로드는 JSON 개체는 경우 사용 합니다. hello 함수 런타임 hello POCO 개체에 hello 페이로드를 역직렬화합니다. 
* `string`
* `byte[]`
* [`CloudQueueMessage`]

<a name="meta"></a>

### <a name="queue-trigger-metadata"></a>큐 트리거 메타데이터
hello 큐 트리거 여러 메타 데이터 속성을 제공 합니다. 이러한 속성을 다른 바인딩에서 바인딩 식의 일부로 사용하거나 코드에서 매개 변수로 사용할 수 있습니다. hello 값은 hello와 동일한 의미 체계 [ `CloudQueueMessage` ]합니다.

* **QueueTrigger** - 큐 페이로드(유효한 문자열인 경우)
* **DequeueCount** - `int` 형식입니다. 이 메시지를 큐에서 제거 된 횟수 만큼을 hello 합니다.
* **ExpirationTime** - `DateTimeOffset?` 형식입니다. hello 시간 hello 메시지 만료 합니다.
* **Id** - `string` 형식입니다. 큐 메시지 ID입니다.
* **InsertionTime** - `DateTimeOffset?` 형식입니다. hello 시간 hello 메시지 toohello 큐에 추가 되었습니다.
* **NextVisibleTime** - `DateTimeOffset?` 형식입니다. hello 시간 hello 메시지 옆 표시 됩니다.
* **PopReceipt** - `string` 형식입니다. hello 메시지의 popreceipt입니다.

어떻게 toouse hello에 큐 메타 데이터 참조 [트리거 샘플](#triggersample)합니다.

<a name="triggersample"></a>

## <a name="trigger-sample"></a>트리거 샘플
다음 function.json 큐 트리거를 정의 하는 hello 있다고 가정 합니다.

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

검색 하 고 큐 메타 데이터를 기록 하는 hello 언어 관련 샘플을 참조 하십시오.

* [C#](#triggercsharp)
* [Node.JS](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a>C#에서 트리거 샘플 #
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

### <a name="trigger-sample-in-nodejs"></a>Node.js에서 트리거 샘플

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

### <a name="handling-poison-queue-messages"></a>포이즌 큐 메시지 처리
큐 트리거 함수가 실패 하면 Azure 함수에 해당 함수 toofive 먼저 hello를 포함 하는 특정된 큐 메시지에 대 한 번 시도를 다시 시도 합니다. 모든 다섯 번의 시도가 실패 하는 경우 hello 함수 런타임에서 이라는 메시지 tooa 큐 저장소를 추가 하는  *&lt;originalqueuename >-포이즌*합니다. 작성할 수 있습니다 함수 tooprocess 메시지 hello 포이즌 큐에서 해당 로그 하거나 수동 주의가 필요한 알림을 보내기. 

toohandle 포이즌 메시지 hello를 수동으로 확인 `dequeueCount` hello 큐 메시지의 (참조 [큐 트리거 메타 데이터](#meta)).

<a name="output"></a>

## <a name="queue-storage-output-binding"></a>Queue Storage 출력 바인딩
Azure 큐 저장소 hello 출력 바인딩을 통해 toowrite 메시지 tooa 큐 수 있습니다. 

큐 정의 hello를 사용 하 여 출력 바인딩 **통합** hello 함수 포털에서 탭 합니다. hello 포털에서는 다음 hello에 정의 된 hello **바인딩** 섹션 *function.json*:

```json
{
   "type": "queue",
   "direction": "out",
   "name": "<hello name used tooidentify hello trigger data in your code>",
   "queueName": "<Name of queue toowrite to>",
   "connection":"<Name of app setting - see below>"
}
```

* hello `connection` 저장소 연결 문자열을 포함 하는 응용 프로그램 설정의 hello 이름을 포함 해야 합니다. Hello Azure 포털에서에서 hello의 표준 편집기 hello **통합** 탭 저장소 계정을 선택할 때 응용 프로그램 설정을 구성 합니다.

<a name="outputusage"></a>

## <a name="using-a-queue-output-binding"></a>큐 출력 바인딩 사용
에서는 Node.js 함수를 사용 하 여 hello 출력 큐 액세스 `context.bindings.<name>`합니다.

.NET 함수 hello 유형만의 tooany를 출력할 수 있습니다. 형식 매개 변수의 경우 `T`, `T` 와 같은 지원 되는 hello 출력 형식 중 하나 여야 합니다 `string` 또는 POCO 합니다.

* `out T`(JSON으로 serialize됨)
* `out string`
* `out byte[]`
* `out` [`CloudQueueMessage`] 
* `ICollector<T>`
* `IAsyncCollector<T>`
* [`CloudQueue`](/dotnet/api/microsoft.windowsazure.storage.queue.cloudqueue)

Hello로 hello 메서드 반환 형식을 사용할 수도 있습니다 출력 바인딩이 있습니다.

<a name="outputsample"></a>

## <a name="queue-output-sample"></a>큐 출력 샘플
hello 다음 *function.json* 큐와 HTTP 트리거는 정의 바인딩 출력:

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

들어오는 HTTP 페이로드 hello 큐 메시지를 출력 하는 hello 언어 관련 샘플을 참조 하십시오.

* [C#](#outcsharp)
* [Node.JS](#outnodejs)

<a name="outcsharp"></a>

### <a name="queue-output-sample-in-c"></a>C#의 큐 출력 샘플 #

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

여러 개의 메시지를 사용 하 여 toosend는 `ICollector`:

```cs
public static void Run(CustomQueueMessage input, ICollector<CustomQueueMessage> myQueueItem, TraceWriter log)
{
    myQueueItem.Add(input);
    myQueueItem.Add(new CustomQueueMessage { PersonName = "You", Title = "None" });
}
```

<a name="outnodejs"></a>

### <a name="queue-output-sample-in-nodejs"></a>Node.js의 큐 출력 샘플

```javascript
module.exports = function (context, input) {
    context.done(null, input.body);
};
```

또는 toosend 여러 개의 메시지를

```javascript
module.exports = function(context) {
    // Define a message array for hello myQueueItem output binding. 
    context.bindings.myQueueItem = ["message 1","message 2"];
    context.done();
};
```

## <a name="next-steps"></a>다음 단계

예를 보려면 큐 저장소 트리거 및 바인딩을 사용 하는 함수 참조 [연결 된 Azure 함수 tooan Azure 서비스 만들기](functions-create-an-azure-connected-function.md)합니다.

[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

<!-- LINKS -->

[`CloudQueueMessage`]: /dotnet/api/microsoft.windowsazure.storage.queue.cloudqueuemessage

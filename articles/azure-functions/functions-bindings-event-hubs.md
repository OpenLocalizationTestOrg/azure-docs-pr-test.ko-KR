---
title: "Azure Functions의 Azure Event Hubs 바인딩"
description: "Azure Functions에서 Azure Event Hubs 바인딩을 사용하는 방법을 이해합니다."
services: functions
documentationcenter: na
author: wesmc7777
manager: cfowler
editor: 
tags: 
keywords: "Azure Functions, 함수, 이벤트 처리, 동적 계산, 서버를 사용하지 않는 아키텍처"
ms.assetid: daf81798-7acc-419a-bc32-b5a41c6db56b
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/08/2017
ms.author: wesmc
ms.openlocfilehash: 0d48d0b008d76cfb2d7d7815a69774976e184467
ms.sourcegitcommit: 85012dbead7879f1f6c2965daa61302eb78bd366
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/02/2018
---
# <a name="azure-event-hubs-bindings-for-azure-functions"></a>Azure Functions의 Azure Event Hubs 바인딩

이 문서에서는 Azure Functions에 [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md) 바인딩을 사용하는 방법에 대해 설명합니다. Azure Functions는 Event Hubs에 대한 트리거 및 출력 바인딩을 지원합니다.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="trigger"></a>트리거

Event Hubs 트리거를 사용하여 이벤트 허브 이벤트 스트림으로 보낸 이벤트에 응답합니다. 트리거를 설정하려면 이벤트 허브에 대한 읽기 권한이 있어야 합니다.

Event Hubs 트리거 함수를 트리거하는 경우 트리거되는 메시지가 함수에 문자열로 전달됩니다.

## <a name="trigger---scaling"></a>트리거 - 크기 조정

Event Hub-Triggered 함수의 각 인스턴스는 하나의 EPH(EventProcessorHost) 인스턴스에서 지원됩니다. Event Hubs는 하나의 EPH가 지정된 파티션에 임대를 가져올 수 있도록 합니다.

예를 들어 Event Hub에 다음과 같은 설정 및 가정을 시작하겠습니다.

1. 10개의 파티션
1. 모든 파티션에 고르게 분산된 1000개의 이벤트 => 각 파티션에 100개의 메시지

기능을 처음 사용하는 경우 함수 인스턴스 1개가 있습니다. 이 기능 인스턴스를 Function_0이라고 하겠습니다. Function_0에는 10개의 모든 파티션에 대해 임대를 가져오도록 관리하는 하나의 EPH가 있습니다. 0-9 파티션에서 이벤트를 읽기 시작합니다. 이 지점부터 다음 중 하나가 발생합니다.

* **하나의 함수 인스턴스가 필요함** - Function_0은 Azure Functions의 크기 조정 논리가 시작하기 전에 1000개를 모두 처리할 수 있습니다. 따라서 모든 1000개의 메시지는 Function_0에서 처리됩니다.

* **하나의 기능 인스턴스 추가** - Azure Functions의 크기 조정 논리는 Function_0에 처리할 수 있는 것보다 더 많은 메시지가 있는지를 확인하고 Function_1이라는 새 인스턴스를 만듭니다. Event Hubs는 새 EPH 인스턴스에서 메시지를 읽으려는 시도를 감지합니다. Event Hubs는 EPH 인스턴스에서 파티션의 부하를 분산하기 시작합니다(예: 파티션 0-4를 Function_0에 할당하고 파티션 5-9를 Function_1에 할당함). 

* **N 이상 함수 인스턴스 추가** - Azure Functions의 크기 조정 논리는 Function_0와 Function_1 모두에 처리할 수 있는 것보다 더 많은 메시지가 있는지 확인합니다. Function_2...N에 대해 다시 크기를 조정합니다. 여기서 N은 Event Hub 파티션보다 큽니다. Event Hubs는 Function_0...9 인스턴스에서 파티션의 부하를 분산합니다.

Azure Functions의 현재 크기 조정 논리에서 고유한 점은 N이 파티션 수보다 크다는 사실입니다. EPH의 인스턴스를 다른 인스턴스에서 사용할 수 있게 되면 해당 인스턴스를 사용하여 파티션에서 잠금을 신속하게 수행할 수 있도록 수행합니다. 사용자에게는 함수 인스턴스가 실행될 때 사용되는 리소스에 대한 요금이 청구되고 과도한 프로비전에 대한 비용이 청구되지 않습니다.

모든 함수 실행이 오류 없이 성공하면 연결된 저장소 계정에 검사점이 추가됩니다. 검사점이 성공하면 모든 1000개의 메시지는 다시 검색되지 않아야 합니다.

## <a name="trigger---example"></a>트리거 - 예제

언어 관련 예제를 참조하세요.

* [C#](#trigger---c-example)
* [C# 스크립트(.csx)](#trigger---c-script-example)
* [F#](#trigger---f-example)
* [JavaScript](#trigger---javascript-example)

### <a name="trigger---c-example"></a>트리거 - C# 예제

다음 예제에서는 이벤트 허브 트리거의 메시지 본문을 기록하는 [C# 함수](functions-dotnet-class-library.md)를 보여줍니다.

```csharp
[FunctionName("EventHubTriggerCSharp")]
public static void Run([EventHubTrigger("samples-workitems", Connection = "EventHubConnection")] string myEventHubMessage, TraceWriter log)
{
    log.Info($"C# Event Hub trigger function processed a message: {myEventHubMessage}");
}
```

이벤트 메타데이터에 대한 액세스를 얻으려면 [EventData](/dotnet/api/microsoft.servicebus.messaging.eventdata) 개체에 바인딩합니다(`Microsoft.ServiceBus.Messaging`에 `using` 문이 필요함).

```csharp
[FunctionName("EventHubTriggerCSharp")]
public static void Run([EventHubTrigger("samples-workitems", Connection = "EventHubConnection")] EventData myEventHubMessage, TraceWriter log)
{
    log.Info($"{Encoding.UTF8.GetString(myEventHubMessage.GetBytes())}");
}
```
일괄 처리에서 이벤트를 수신하려면 `string` 또는 `EventData` 배열을 만듭니다.

```cs
[FunctionName("EventHubTriggerCSharp")]
public static void Run([EventHubTrigger("samples-workitems", Connection = "EventHubConnection")] string[] eventHubMessages, TraceWriter log)
{
    foreach (var message in eventHubMessages)
    {
        log.Info($"C# Event Hub trigger function processed a message: {message}");
    }
}
```

### <a name="trigger---c-script-example"></a>트리거 - C# 스크립트 예제

다음 예에서는 *function.json* 파일의 이벤트 허브 트리거 바인딩 및 바인딩을 사용하는 [C# 스크립트 함수](functions-reference-csharp.md)를 보여줍니다. 함수는 이벤트 허브 트리거의 메시지 본문을 기록합니다.

*function.json* 파일의 바인딩 데이터는 다음과 같습니다.

```json
{
  "type": "eventHubTrigger",
  "name": "myEventHubMessage",
  "direction": "in",
  "path": "MyEventHub",
  "connection": "myEventHubReadConnectionString"
}
```
C# 스크립트 코드는 다음과 같습니다.

```cs
using System;

public static void Run(string myEventHubMessage, TraceWriter log)
{
    log.Info($"C# Event Hub trigger function processed a message: {myEventHubMessage}");
}
```

이벤트 메타데이터에 대한 액세스를 얻으려면 [EventData](/dotnet/api/microsoft.servicebus.messaging.eventdata) 개체에 바인딩합니다(`Microsoft.ServiceBus.Messaging`에 using 문이 필요함).

```cs
#r "Microsoft.ServiceBus"
using System.Text;
using Microsoft.ServiceBus.Messaging;

public static void Run(EventData myEventHubMessage, TraceWriter log)
{
    log.Info($"{Encoding.UTF8.GetString(myEventHubMessage.GetBytes())}");
}
```

일괄 처리에서 이벤트를 수신하려면 `string` 또는 `EventData` 배열을 만듭니다.

```cs
public static void Run(string[] eventHubMessages, TraceWriter log)
{
    foreach (var message in eventHubMessages)
    {
        log.Info($"C# Event Hub trigger function processed a message: {message}");
    }
}
```

### <a name="trigger---f-example"></a>트리거 - F# 예제

다음 예에서는 *function.json* 파일의 이벤트 허브 트리거 바인딩 및 바인딩을 사용하는 [F# 함수](functions-reference-fsharp.md)를 보여줍니다. 함수는 이벤트 허브 트리거의 메시지 본문을 기록합니다.

*function.json* 파일의 바인딩 데이터는 다음과 같습니다.

```json
{
  "type": "eventHubTrigger",
  "name": "myEventHubMessage",
  "direction": "in",
  "path": "MyEventHub",
  "connection": "myEventHubReadConnectionString"
}
```

F# 코드는 다음과 같습니다.

```fsharp
let Run(myEventHubMessage: string, log: TraceWriter) =
    log.Info(sprintf "F# eventhub trigger function processed work item: %s" myEventHubMessage)
```

### <a name="trigger---javascript-example"></a>트리거 - JavaScript 예제

다음 예에서는 *function.json* 파일의 이벤트 허브 트리거 바인딩 및 바인딩을 사용하는 [JavaScript 함수](functions-reference-node.md)를 보여줍니다. 함수는 이벤트 허브 트리거의 메시지 본문을 기록합니다.

*function.json* 파일의 바인딩 데이터는 다음과 같습니다.

```json
{
  "type": "eventHubTrigger",
  "name": "myEventHubMessage",
  "direction": "in",
  "path": "MyEventHub",
  "connection": "myEventHubReadConnectionString"
}
```

JavaScript 코드는 다음과 같습니다.

```javascript
module.exports = function (context, myEventHubMessage) {
    context.log('Node.js eventhub trigger function processed work item', myEventHubMessage);    
    context.done();
};
```

## <a name="trigger---attributes"></a>트리거 - 특성

[C# 클래스 라이브러리](functions-dotnet-class-library.md)에서는 [Microsoft.Azure.WebJobs.ServiceBus](http://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus) NuGet 패키지에 정의되어 있는 [EventHubTriggerAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubTriggerAttribute.cs) 특성을 사용합니다.

특성의 생성자는 이벤트 허브의 이름, 소비자 그룹의 이름 및 연결 문자열을 포함하는 앱 설정의 이름을 사용합니다. 이러한 설정에 대한 자세한 내용은 [트리거 구성 섹션](#trigger---configuration)을 참조하세요. `EventHubTriggerAttribute` 특성 예제는 다음과 같습니다.

```csharp
[FunctionName("EventHubTriggerCSharp")]
public static void Run([EventHubTrigger("samples-workitems", Connection = "EventHubConnection")] string myEventHubMessage, TraceWriter log)
{
    ...
}
```

전체 예제는 [트리거 - C# 예제](#trigger---c-example)를 참조하세요.

## <a name="trigger---configuration"></a>트리거 - 구성

다음 표에서는 *function.json* 파일 및 `EventHubTrigger` 특성에 설정된 바인딩 구성 속성을 설명합니다.

|function.json 속성 | 특성 속성 |설명|
|---------|---------|----------------------|
|**type** | 해당 없음 | `eventHubTrigger`로 설정해야 합니다. 이 속성은 사용자가 Azure Portal에서 트리거를 만들 때 자동으로 설정됩니다.|
|**direction** | 해당 없음 | `in`로 설정해야 합니다. 이 속성은 사용자가 Azure Portal에서 트리거를 만들 때 자동으로 설정됩니다. |
|**name** | 해당 없음 | 함수 코드에서 이벤트 항목을 나타내는 변수의 이름입니다. | 
|**path** |**EventHubName** | 이벤트 허브의 이름입니다. | 
|**consumerGroup** |**ConsumerGroup** | 허브에서 이벤트를 구독하는 데 사용되는 [소비자 그룹](../event-hubs/event-hubs-features.md#event-consumers)을 설정하는 선택적 속성입니다. 생략한 경우 `$Default` 소비자 그룹이 사용됩니다. | 
|**연결** |**연결** | 이벤트 허브의 네임스페이스에 대한 연결 문자열을 포함하는 앱 설정의 이름입니다. 이벤트 허브 자체가 아닌 *네임스페이스*에 대한 **연결 정보** 단추를 클릭하여 이 연결 문자열을 복사합니다. 트리거를 활성화하려면 이 연결 문자열은 적어도 읽기 권한이 있어야 합니다.|

[!INCLUDE [app settings to local.settings.json](../../includes/functions-app-settings-local.md)]

## <a name="trigger---hostjson-properties"></a>트리거 - host.json 속성

[host.json](functions-host-json.md#eventhub) 파일에는 Event Hubs 트리거 동작을 제어하는 설정이 포함됩니다.

[!INCLUDE [functions-host-json-event-hubs](../../includes/functions-host-json-event-hubs.md)]

## <a name="output"></a>출력

Event Hubs 출력 바인딩을 사용하여 이벤트 스트림에 이벤트를 씁니다. 이벤트를 쓰려면 이벤트 허브에 대한 보내기 사용 권한이 있어야 합니다.

## <a name="output---example"></a>출력 - 예제

언어 관련 예제를 참조하세요.

* [C#](#output---c-example)
* [C# 스크립트(.csx)](#output---c-script-example)
* [F#](#output---f-example)
* [JavaScript](#output---javascript-example)

### <a name="output---c-example"></a>출력 - C# 예제

다음 예제에서는 메서드 반환 값을 출력으로 사용하여 이벤트 허브로 메시지를 쓰는 [C# 함수](functions-dotnet-class-library.md)를 보여줍니다.

```csharp
[FunctionName("EventHubOutput")]
[return: EventHub("outputEventHubMessage", Connection = "EventHubConnection")]
public static string Run([TimerTrigger("0 */5 * * * *")] TimerInfo myTimer, TraceWriter log)
{
    log.Info($"C# Timer trigger function executed at: {DateTime.Now}");
    return $"{DateTime.Now}";
}
```

### <a name="output---c-script-example"></a>출력 - C# 스크립트 예제

다음 예에서는 *function.json* 파일의 이벤트 허브 트리거 바인딩 및 바인딩을 사용하는 [C# 스크립트 함수](functions-reference-csharp.md)를 보여줍니다. 함수는 이벤트 허브로 메시지를 씁니다.

*function.json* 파일의 바인딩 데이터는 다음과 같습니다.

```json
{
    "type": "eventHub",
    "name": "outputEventHubMessage",
    "path": "myeventhub",
    "connection": "MyEventHubSend",
    "direction": "out"
}
```

단일 메시지를 만드는 C# 스크립트 코드는 다음과 같습니다.

```cs
using System;

public static void Run(TimerInfo myTimer, out string outputEventHubMessage, TraceWriter log)
{
    String msg = $"TimerTriggerCSharp1 executed at: {DateTime.Now}";
    log.Verbose(msg);   
    outputEventHubMessage = msg;
}
```

여러 메시지를 만드는 C# 스크립트 코드는 다음과 같습니다.

```cs
public static void Run(TimerInfo myTimer, ICollector<string> outputEventHubMessage, TraceWriter log)
{
    string message = $"Event Hub message created at: {DateTime.Now}";
    log.Info(message);
    outputEventHubMessage.Add("1 " + message);
    outputEventHubMessage.Add("2 " + message);
}
```

### <a name="output---f-example"></a>출력 - F# 예제

다음 예에서는 *function.json* 파일의 이벤트 허브 트리거 바인딩 및 바인딩을 사용하는 [F# 함수](functions-reference-fsharp.md)를 보여줍니다. 함수는 이벤트 허브로 메시지를 씁니다.

*function.json* 파일의 바인딩 데이터는 다음과 같습니다.

```json
{
    "type": "eventHub",
    "name": "outputEventHubMessage",
    "path": "myeventhub",
    "connection": "MyEventHubSend",
    "direction": "out"
}
```

F# 코드는 다음과 같습니다.

```fsharp
let Run(myTimer: TimerInfo, outputEventHubMessage: byref<string>, log: TraceWriter) =
    let msg = sprintf "TimerTriggerFSharp1 executed at: %s" DateTime.Now.ToString()
    log.Verbose(msg);
    outputEventHubMessage <- msg;
```

### <a name="output---javascript-example"></a>출력 - JavaScript 예제

다음 예에서는 *function.json* 파일의 이벤트 허브 트리거 바인딩 및 바인딩을 사용하는 [JavaScript 함수](functions-reference-node.md)를 보여줍니다. 함수는 이벤트 허브로 메시지를 씁니다.

*function.json* 파일의 바인딩 데이터는 다음과 같습니다.

```json
{
    "type": "eventHub",
    "name": "outputEventHubMessage",
    "path": "myeventhub",
    "connection": "MyEventHubSend",
    "direction": "out"
}
```

단일 메시지를 보내는 JavaScript 코드는 다음과 같습니다.

```javascript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();
    context.log('Event Hub message created at: ', timeStamp);   
    context.bindings.outputEventHubMessage = "Event Hub message created at: " + timeStamp;
    context.done();
};
```

여러 메시지를 보내는 JavaScript 코드는 다음과 같습니다.

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

## <a name="output---attributes"></a>출력 - 특성

[C# 클래스 라이브러리](functions-dotnet-class-library.md)의 경우 [Microsoft.Azure.WebJobs.ServiceBus](http://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus) NuGet 패키지에 정의되어 있는 [EventHubAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs) 특성을 사용합니다.

특성의 생성자는 이벤트 허브의 이름 및 연결 문자열을 포함하는 앱 설정의 이름을 사용합니다. 이러한 설정에 대한 자세한 내용은 [출력 - 구성](#output---configuration)을 참조하세요. `EventHub` 특성 예제는 다음과 같습니다.

```csharp
[FunctionName("EventHubOutput")]
[return: EventHub("outputEventHubMessage", Connection = "EventHubConnection")]
public static string Run([TimerTrigger("0 */5 * * * *")] TimerInfo myTimer, TraceWriter log)
{
    ...
}
```

전체 예제는 [출력 - C# 예제](#output---c-example)를 참조하세요.

## <a name="output---configuration"></a>출력 - 구성

다음 표에서는 *function.json* 파일 및 `EventHub` 특성에 설정된 바인딩 구성 속성을 설명합니다.

|function.json 속성 | 특성 속성 |설명|
|---------|---------|----------------------|
|**type** | 해당 없음 | "eventHub"로 설정해야 합니다. |
|**direction** | 해당 없음 | "out"으로 설정해야 합니다. 이 매개 변수는 사용자가 Azure Portal에서 바인딩을 만들 때 자동으로 설정됩니다. |
|**name** | 해당 없음 | 이벤트를 나타내는 함수 코드에서 사용되는 변수 이름입니다. | 
|**path** |**EventHubName** | 이벤트 허브의 이름입니다. | 
|**연결** |**연결** | 이벤트 허브의 네임스페이스에 대한 연결 문자열을 포함하는 앱 설정의 이름입니다. 이벤트 허브 자체가 아닌 *네임스페이스*에 대한 **연결 정보** 단추를 클릭하여 이 연결 문자열을 복사합니다. 이 연결 문자열에는 이벤트 스트림으로 메시지를 보내기 위해 보내기 사용 권한이 있어야 합니다.|

[!INCLUDE [app settings to local.settings.json](../../includes/functions-app-settings-local.md)]

## <a name="output---usage"></a>출력 - 사용

C# 및 C# 스크립트에서는 `out string paramName`과 같은 메서드 매개 변수를 사용하여 메시지를 보냅니다. C# 스크립트에서 `paramName`은 *function.json*의 `name` 속성에 지정된 값입니다. 여러 메시지를 쓰려면 `out string` 대신 `ICollector<string>` 또는 `IAsyncCollector<string>`를 사용할 수 있습니다.

JavaScript에서 `context.bindings.<name>`를 사용하여 출력 이벤트에 액세스합니다. `<name>`은 *function.json*의 `name` 속성에 지정된 값입니다.

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [Azure Functions 트리거 및 바인딩에 대한 자세한 정보](functions-triggers-bindings.md)

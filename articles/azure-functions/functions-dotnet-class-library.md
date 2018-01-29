---
title: "Azure Functions C# 개발자 참조"
description: "C#을 사용하여 Azure Functions를 개발하는 방법을 알아봅니다."
services: functions
documentationcenter: na
author: ggailey777
manager: cfowler
editor: 
tags: 
keywords: "Azure Functions, 함수, 이벤트 처리, webhook, 동적 계산, 서버가 없는 아키텍처"
ms.service: functions
ms.devlang: dotnet
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 12/12/2017
ms.author: glenga
ms.openlocfilehash: 3de1e9b042a7a356c3c88e604e1e26c256d85657
ms.sourcegitcommit: 828cd4b47fbd7d7d620fbb93a592559256f9d234
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/18/2018
---
# <a name="azure-functions-c-developer-reference"></a>Azure Functions C# 개발자 참조

<!-- When updating this article, make corresponding changes to any duplicate content in functions-reference-csharp.md -->

이 문서는 .NET 클래스 라이브러리의 C#을 사용하여 Azure Functions를 개발하는 방법을 소개합니다.

Azure Functions는 C# 및 C# 스크립트 프로그래밍 언어를 지원합니다. [Azure Portal에서 C#을 사용하는 방법](functions-create-function-app-portal.md)에 대한 지침은 [C# 스크립트(.csx) 개발자 참조](functions-reference-csharp.md)를 참조하세요.

이 문서에서는 사용자가 이미 다음 문서를 읽었다고 가정합니다.

* [Azure Functions 개발자 가이드](functions-reference.md)
* [Azure Functions Visual Studio 2017 Tools](functions-develop-vs.md)

## <a name="functions-class-library-project"></a>Functions 클래스 라이브러리 프로젝트

Visual Studio에서 **Azure Functions** 프로젝트 템플릿은 다음 파일이 포함된 C# 클래스 라이브러리 프로젝트를 만듭니다.

* [host.json](functions-host-json.md) -로컬로 또는 Azure에서 실행될 경우 프로젝트의 모든 함수에 영향을 주는 구성 설정을 저장합니다.
* [local.settings.json](functions-run-local.md#local-settings-file) - 로컬로 실행될 때 사용되는 앱 설정 및 연결 문자열을 저장합니다.

### <a name="functionname-and-trigger-attributes"></a>FunctionName 및 트리거 특성

클래스 라이브러리에서 함수는 다음 예제와 같이 `FunctionName` 및 트리거 특성을 포함하는 정적 메서드입니다.

```csharp
public static class SimpleExample
{
    [FunctionName("QueueTrigger")]
    public static void Run(
        [QueueTrigger("myqueue-items")] string myQueueItem, 
        TraceWriter log)
    {
        log.Info($"C# function processed: {myQueueItem}");
    }
} 
```

`FunctionName` 특성은 메서드를 함수 진입점으로 표시합니다. 이름은 프로젝트 내에서 고유해야 합니다.

트리거 특성은 트리거 유형을 지정하고, 입력 데이터를 메서드 매개 변수에 바인딩합니다. 예제 함수는 큐 메시지에 의해 트리거되며, 큐 메시지는 `myQueueItem` 매개 변수의 메서드에 전달됩니다.

### <a name="additional-binding-attributes"></a>추가 바인딩 특성

추가 입력 및 출력 바인딩 특성을 사용할 수 있습니다. 다음 예제에서는 출력 큐 바인딩을 추가하여 이전 예제를 수정합니다. 이 함수는 입력 큐 메시지를 다른 큐의 새 큐 메시지에 씁니다.

```csharp
public static class SimpleExampleWithOutput
{
    [FunctionName("CopyQueueMessage")]
    public static void Run(
        [QueueTrigger("myqueue-items-source")] string myQueueItem, 
        [Queue("myqueue-items-destination")] out string myQueueItemCopy,
        TraceWriter log)
    {
        log.Info($"CopyQueueMessage function processed: {myQueueItem}");
        myQueueItemCopy = myQueueItem;
    }
}
```

### <a name="conversion-to-functionjson"></a>Function.json으로 변환

빌드 프로세스는 build 폴더의 function 폴더에 *function.json* 파일을 만듭니다. 이 파일은 직접 편집하는 용도로 사용되지 않습니다. 이 파일을 편집하여 바인딩 구성을 변경하거나 함수를 사용하지 않도록 설정할 수 없습니다. 

이 파일은 [소비 계획에 대한 크기 결정](functions-scale.md#how-the-consumption-plan-works)에 사용하기 위해 크기 조정 컨트롤러에 정보를 제공하는 데 필요합니다. 이러한 이유로 이 파일에는 트리거 정보만 있고 입력 또는 출력 바인딩은 없습니다.

생성된 *function.json* 파일에는 바인딩에 *function.json* 구성 대신 .NET 특성을 사용하도록 런타임에 지시하는 `configurationSource` 속성이 포함되어 있습니다. 예를 들면 다음과 같습니다.

```json
{
  "generatedBy": "Microsoft.NET.Sdk.Functions-1.0.0.0",
  "configurationSource": "attributes",
  "bindings": [
    {
      "type": "queueTrigger",
      "queueName": "%input-queue-name%",
      "name": "myQueueItem"
    }
  ],
  "disabled": false,
  "scriptFile": "..\\bin\\FunctionApp1.dll",
  "entryPoint": "FunctionApp1.QueueTrigger.Run"
}
```

*function.json* 파일 생성은 [Microsoft\.NET\.Sdk\.Functions](http://www.nuget.org/packages/Microsoft.NET.Sdk.Functions) NuGet 패키지에서 수행됩니다. 소스 코드는 [azure\-functions\-vs\-build\-sdk](https://github.com/Azure/azure-functions-vs-build-sdk) GitHub 리포지토리에서 사용할 수 있습니다.

## <a name="supported-types-for-bindings"></a>바인딩에 대해 지원되는 형식

각 바인딩에는 자체적인 지원 형식이 있습니다. 예를들 어, Blob 트리거 특성은 문자열 매개 변수, POCO 매개 변수, `CloudBlockBlob` 매개 변수 또는 지원되는 기타 몇 가지 형식에 적용될 수 있습니다. [Blob 바인딩에 대한 바인딩 참조 문서](functions-bindings-storage-blob.md#trigger---usage)에는 지원되는 모든 매개 변수 형식이 나와 있습니다. 자세한 내용은 [트리거 및 바인딩](functions-triggers-bindings.md) 및 [각 바인딩 형식에 대한 바인딩 참조 문서](functions-triggers-bindings.md#next-steps)를 참조하세요.

[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

## <a name="binding-to-method-return-value"></a>메서드 반환 값에 바인딩

다음 예제와 같이 출력 바인딩에 메서드 반환 값을 사용할 수 있습니다.

```csharp
public static class ReturnValueOutputBinding
{
    [FunctionName("CopyQueueMessageUsingReturnValue")]
    [return: Queue("myqueue-items-destination")]
    public static string Run(
        [QueueTrigger("myqueue-items-source-2")] string myQueueItem,
        TraceWriter log)
    {
        log.Info($"C# function processed: {myQueueItem}");
        return myQueueItem;
    }
}
```

## <a name="writing-multiple-output-values"></a>여러 출력 값 쓰기

출력 바인딩에 여러 값을 쓰려면 [`ICollector`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) 또는 [`IAsyncCollector`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) 형식을 사용합니다. 이러한 형식은 메서드가 완료될 때 출력 바인딩에 기록되는 쓰기 전용 컬렉션입니다.

이 예제에서는 `ICollector`를 사용하여 동일한 큐에 여러 큐 메시지를 씁니다.

```csharp
public static class ICollectorExample
{
    [FunctionName("CopyQueueMessageICollector")]
    public static void Run(
        [QueueTrigger("myqueue-items-source-3")] string myQueueItem,
        [Queue("myqueue-items-destination")] ICollector<string> myQueueItemCopy,
        TraceWriter log)
    {
        log.Info($"C# function processed: {myQueueItem}");
        myQueueItemCopy.Add($"Copy 1: {myQueueItem}");
        myQueueItemCopy.Add($"Copy 2: {myQueueItem}");
    }
}
```

## <a name="logging"></a>로깅

C#의 스트리밍 로그에 대한 출력을 기록하려면 `TraceWriter` 형식의 인수를 포함합니다. 이름을 `log`로 하는 것이 좋습니다. Azure Functions에서 `Console.Write`를 사용하지 마세요. 

`TraceWriter`는 [Azure WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/TraceWriter.cs)에 정의되어 있습니다. `TraceWriter`에 대한 로그 수준은 [host.json](functions-host-json.md)에서 구성할 수 있습니다.

```csharp
public static class SimpleExample
{
    [FunctionName("QueueTrigger")]
    public static void Run(
        [QueueTrigger("myqueue-items")] string myQueueItem, 
        TraceWriter log)
    {
        log.Info($"C# function processed: {myQueueItem}");
    }
} 
```

> [!NOTE]
> `TraceWriter` 대신 사용할 수 있는 최신 로깅 프레임워크에 대한 내용은 **Azure Functions 모니터링** 문서에서 [C# 함수로 로그 작성](functions-monitoring.md#write-logs-in-c-functions)을 참조하세요.

## <a name="async"></a>Async

비동기화 함수를 만들려면 `async` 키워드를 사용하고 `Task` 개체를 반환합니다.

```csharp
public static class AsyncExample
{
    [FunctionName("BlobCopy")]
    public static async Task RunAsync(
        [BlobTrigger("sample-images/{blobName}")] Stream blobInput,
        [Blob("sample-images-copies/{blobName}", FileAccess.Write)] Stream blobOutput,
        CancellationToken token,
        TraceWriter log)
    {
        log.Info($"BlobCopy function processed.");
        await blobInput.CopyToAsync(blobOutput, 4096, token);
    }
}
```

## <a name="cancellation-tokens"></a>취소 토큰

일부 작업에는 정상 종료가 필요합니다. 충돌을 처리할 수 있는 코드를 작성하는 데 가장 좋은 방법이지만 종료 요청을 처리하려는 경우 [CancellationToken](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) 형식의 인수를 정의합니다.  `CancellationToken`은 호스트 종료가 트리거되는 신호에 제공됩니다.

```csharp
public static class CancellationTokenExample
{
    [FunctionName("BlobCopy")]
    public static async Task RunAsync(
        [BlobTrigger("sample-images/{blobName}")] Stream blobInput,
        [Blob("sample-images-copies/{blobName}", FileAccess.Write)] Stream blobOutput,
        CancellationToken token)
    {
        await blobInput.CopyToAsync(blobOutput, 4096, token);
    }
}
```

## <a name="environment-variables"></a>환경 변수

환경 변수 또는 앱 설정 값을 가져오려면 다음 코드 예제와 같이 `System.Environment.GetEnvironmentVariable`을 사용합니다.

```csharp
public static class EnvironmentVariablesExample
{
    [FunctionName("GetEnvironmentVariables")]
    public static void Run([TimerTrigger("0 */5 * * * *")]TimerInfo myTimer, TraceWriter log)
    {
        log.Info($"C# Timer trigger function executed at: {DateTime.Now}");
        log.Info(GetEnvironmentVariable("AzureWebJobsStorage"));
        log.Info(GetEnvironmentVariable("WEBSITE_SITE_NAME"));
    }

    public static string GetEnvironmentVariable(string name)
    {
        return name + ": " +
            System.Environment.GetEnvironmentVariable(name, EnvironmentVariableTarget.Process);
    }
}
```

## <a name="binding-at-runtime"></a>런타임에 바인딩

C# 및 기타 .NET 언어에서는 특성의 [*declarative*](https://en.wikipedia.org/wiki/Declarative_programming) 바인딩과 달리 [명령적](https://en.wikipedia.org/wiki/Imperative_programming) 바인딩 패턴을 사용할 수 있습니다. 명령적 바인딩은 바인딩 매개 변수를 디자인 타임이 아닌 런타임에 계산해야 할 경우 유용합니다. 이 패턴을 사용하면 함수 코드에서 지원되는 입력 및 출력 바인딩을 즉시 바인딩할 수 있습니다.

다음과 같이 명령적 바인딩을 정의합니다.

- 원하는 명령적 바인딩에 대한 함수 시그니처에 특성을 포함하지 **마세요**.
- 입력 매개 변수 [`Binder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/Bindings/Runtime/Binder.cs) 또는 [`IBinder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IBinder.cs)에 전달합니다.
- 다음 C# 패턴을 사용하여 데이터 바인딩을 수행합니다.

  ```cs
  using (var output = await binder.BindAsync<T>(new BindingTypeAttribute(...)))
  {
      ...
  }
  ```

  `BindingTypeAttribute`는 바인딩을 정의하는 .NET 특성이며, `T`는 해당 바인딩 형식에서 지원되는 입력 또는 출력 형식입니다. `T`는 `out` 매개 변수 형식(예: `out JObject`)일 수 없습니다. 예를 들어, Mobile Apps 테이블 출력 바인딩은 [6가지 출력 형식](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22)을 지원하지만 명령적 바인딩에는 [ICollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) 또는 [IAsyncCollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs)만 사용할 수 있습니다.

### <a name="single-attribute-example"></a>단일 특성 예제

다음 예제 코드에서는 런타임에서 정의된 Blob경로를 사용하는 [Storage Blob 출력 바인딩](functions-bindings-storage-blob.md#output)을 만든 다음, Blob에 문자열을 씁니다.

```cs
public static class IBinderExample
{
    [FunctionName("CreateBlobUsingBinder")]
    public static void Run(
        [QueueTrigger("myqueue-items-source-4")] string myQueueItem,
        IBinder binder,
        TraceWriter log)
    {
        log.Info($"CreateBlobUsingBinder function processed: {myQueueItem}");
        using (var writer = binder.Bind<TextWriter>(new BlobAttribute(
                    $"samples-output/{myQueueItem}", FileAccess.Write)))
        {
            writer.Write("Hello World!");
        };
    }
}
```

[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs)는 [Storage Blob](functions-bindings-storage-blob.md) 입력 또는 출력 바인딩을 정의하며, [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx)는 지원되는 출력 바인딩 형식입니다.

### <a name="multiple-attribute-example"></a>다중 특성 예제

앞의 예제에서는 함수 앱의 주 Storage 계정 연결 문자열(`AzureWebJobsStorage`)에 대한 앱 설정을 가져옵니다. [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)를 추가하고 `BindAsync<T>()`에 특성 배열을 전달하여 저장소 계정에 사용할 사용자 지정 앱 설정을 지정할 수 있습니다. `IBinder`가 아닌 `Binder` 매개 변수를 사용합니다.  예: 

```cs
public static class IBinderExampleMultipleAttributes
{
    [FunctionName("CreateBlobInDifferentStorageAccount")]
    public async static Task RunAsync(
            [QueueTrigger("myqueue-items-source-binder2")] string myQueueItem,
            Binder binder,
            TraceWriter log)
    {
        log.Info($"CreateBlobInDifferentStorageAccount function processed: {myQueueItem}");
        var attributes = new Attribute[]
        {
        new BlobAttribute($"samples-output/{myQueueItem}", FileAccess.Write),
        new StorageAccountAttribute("MyStorageAccount")
        };
        using (var writer = await binder.BindAsync<TextWriter>(attributes))
        {
            await writer.WriteAsync("Hello World!!");
        }
    }
}
```

## <a name="triggers-and-bindings"></a>트리거 및 바인딩 

다음 표에서는 Azure Functions 클래스 라이브러리 프로젝트에서 사용할 수 있는 트리거 및 바인딩 특성을 나열합니다. 모든 특성은 `Microsoft.Azure.WebJobs` 네임스페이스에 있습니다.

| 트리거 | 입력 | 출력|
|------   | ------    | ------  |
| [BlobTrigger](functions-bindings-storage-blob.md#trigger---attributes)| [Blob](functions-bindings-storage-blob.md#input---attributes)| [Blob](functions-bindings-storage-blob.md#output---attributes)|
| [CosmosDBTrigger](functions-bindings-cosmosdb.md#trigger---attributes)| [DocumentDB](functions-bindings-cosmosdb.md#input---attributes)| [DocumentDB](functions-bindings-cosmosdb.md#output---attributes) |
| [EventHubTrigger](functions-bindings-event-hubs.md#trigger---attributes)|| [EventHub](functions-bindings-event-hubs.md#output---attributes) |
| [HTTPTrigger](functions-bindings-http-webhook.md#trigger---attributes)|||
| [QueueTrigger](functions-bindings-storage-queue.md#trigger---attributes)|| [큐](functions-bindings-storage-queue.md#output---attributes) |
| [ServiceBusTrigger](functions-bindings-service-bus.md#trigger---attributes)|| [Service Bus](functions-bindings-service-bus.md#output---attributes) |
| [TimerTrigger](functions-bindings-timer.md#attributes) | ||
| |[ApiHubFile](functions-bindings-external-file.md)| [ApiHubFile](functions-bindings-external-file.md)|
| |[MobileTable](functions-bindings-mobile-apps.md#input---attributes)| [MobileTable](functions-bindings-mobile-apps.md#output---attributes) | 
| |[테이블](functions-bindings-storage-table.md#input---attributes)| [테이블](functions-bindings-storage-table.md#output---attributes)  | 
| ||[NotificationHub](functions-bindings-notification-hubs.md#attributes) |
| ||[SendGrid](functions-bindings-sendgrid.md#attributes) |
| ||[Twilio](functions-bindings-twilio.md#attributes)| 

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [트리거 및 바인딩에 대해 자세히 알아보기](functions-triggers-bindings.md)

> [!div class="nextstepaction"]
> [Azure Functions에 대한 모범 사례에 대해 자세히 알아보기](functions-best-practices.md)

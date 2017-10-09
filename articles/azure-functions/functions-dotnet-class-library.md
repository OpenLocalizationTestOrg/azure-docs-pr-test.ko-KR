---
title: "aaaUsing.NET 클래스 라이브러리 Azure 함수로 | Microsoft Docs"
description: "Tooauthor.NET 클래스 라이브러리에 대 한 Azure 함수와 함께 사용 하는 방법을 알아봅니다"
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "Azure Functions, 함수, 이벤트 처리, 동적 계산, 서버를 사용하지 않는 아키텍처"
ms.assetid: 9f5db0c2-a88e-4fa8-9b59-37a7096fc828
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/09/2017
ms.author: donnam
ms.openlocfilehash: 4e0fd954b554006ba1d8ecc47403a9fb1c67c3b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-net-class-libraries-with-azure-functions"></a>Azure Functions에서 .NET 클래스 라이브러리 사용

또한 tooscript 파일을 Azure 함수는 하나 이상의 함수에 대 한 hello 구현으로 클래스 라이브러리에 게시를 지원 합니다. Hello를 사용 하는 것이 좋습니다 [Azure 함수 Visual Studio 2017 도구](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/)합니다.

## <a name="prerequisites"></a>필수 조건 

이 문서에는 hello 다음 필수 구성 요소에 있습니다.

- [Visual Studio 2017 15.3 미리 보기](https://www.visualstudio.com/vs/preview/) - Hello 작업 설치 **ASP.NET 및 웹 개발** 및 **Azure 개발**합니다.
- [Azure Function Tools for Visual Studio 2017](https://marketplace.visualstudio.com/items?itemName=AndrewBHall-MSFT.AzureFunctionToolsforVisualStudio2017)

## <a name="functions-class-library-project"></a>Functions 클래스 라이브러리 프로젝트

Visual Studio에서 새 Azure Functions 프로젝트를 만듭니다. 새 프로젝트 템플릿이 hello hello 파일을 만듭니다 *host.json* 및 *local.settings.json*합니다. [host.json에서 Azure Functions 런타임 설정을 사용자 지정](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json)할 수 있습니다. 

hello 파일 *local.settings.json* 응용 프로그램 설정, 연결 문자열 및 Azure 함수 핵심 도구에 대 한 설정을 저장 합니다. 해당 구조에 대해 자세히 toolearn 참조 [코드 및 Azure 함수 로컬로 테스트](functions-run-local.md#local-settings)합니다.

### <a name="functionname-attribute"></a>FunctionName 특성

hello 특성 [ `FunctionNameAttribute` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/FunctionNameAttribute.cs) 함수 진입점으로 메서드를 표시 합니다. 정확히 하나의 트리거와 0개 이상의 입력 및 출력 바인딩을 포함하여 사용해야 합니다.

### <a name="conversion-toofunctionjson"></a>변환 toofunction.json

파일을 생성 한 Azure 기능 프로젝트를 빌드할 때 `function.json` hello 디렉터리에 의해 정의 hello 함수 이름과 일치 하는 `[FunctionName]`합니다. 바인딩과 포인트 toohello 프로젝트 어셈블리 파일 및 트리거를 지정합니다.

이 변환은 hello NuGet 패키지에 의해 수행 됩니다 [Microsoft\.NET\.Sdk\.함수](http://www.nuget.org/packages/Microsoft.NET.Sdk.Functions)합니다. hello 소스가 나타나므로 hello GitHub 리포지토리 [azure\-함수\-vs\-빌드\-sdk](https://github.com/Azure/azure-functions-vs-build-sdk)합니다.

## <a name="triggers-and-bindings"></a>트리거 및 바인딩

hello 다음 표에 hello 트리거 및 Azure 함수 클래스 라이브러리 프로젝트에서 사용할 수 있는 바인딩이 있습니다. 모든 특성은 hello 네임 스페이스 `Microsoft.Azure.WebJobs`합니다.

| 바인딩 | 특성 | NuGet 패키지 |
|------   | ------    | ------        |
| [Blob 저장소 트리거, 입력, 출력](#blob-storage) | [BlobAttribute], [StorageAccountAttribute] | [Microsoft.Azure.WebJobs] | [Blob 저장소] |
| [Cosmos DB 입력 및 출력 바인딩](#cosmos-db) | [DocumentDBAttribute] | [Microsoft.Azure.WebJobs.Extensions.DocumentDB] | 
| [Event Hubs 트리거 및 출력](#event-hub) | [EventHubTriggerAttribute], [EventHubAttribute] | [Microsoft.Azure.WebJobs.ServiceBus] |
| [외부 파일 입력 및 출력](#api-hub) | [ApiHubFileAttribute] | [Microsoft.Azure.WebJobs.Extensions.ApiHub] |
| [HTTP 및 웹후크 트리거](#http) | [HttpTriggerAttribute] | [Microsoft.Azure.WebJobs.Extensions.Http] |
| [Mobile Apps 입력 및 출력](#mobile-apps) | [MobileTableAttribute] | [Microsoft.Azure.WebJobs.Extensions.MobileApps] | 
| [Notification Hubs 출력](#nh) | [NotificationHubAttribute] | [Microsoft.Azure.WebJobs.Extensions.NotificationHubs] | 
| [큐 저장소 트리거 및 출력](#queue) | [QueueAttribute], [StorageAccountAttribute] | [Microsoft.Azure.WebJobs] | 
| [SendGrid 출력](#sendgrid) | [SendGridAttribute] | [Microsoft.Azure.WebJobs.Extensions.SendGrid] | 
| [Service Bus 트리거 및 출력](#service-bus) | [ServiceBusAttribute], [ServiceBusAccountAttribute] | [Microsoft.Azure.WebJobs.ServiceBus]
| [테이블 저장소 입력 및 출력](#table) | [TableAttribute], [StorageAccountAttribute] | [Microsoft.Azure.WebJobs] | 
| [타이머 트리거](#timer) | [TimerTriggerAttribute] | [Microsoft.Azure.WebJobs.Extensions] | 
| [Twilio 출력](#twilio) | [TwilioSmsAttribute] | [Microsoft.Azure.WebJobs.Extensions.Twilio] | 

<a name="blob-storage"></a>

### <a name="blob-storage-trigger-input-and-output-bindings"></a>Blob 저장소 트리거, 입력 및 출력 바인딩

Azure Functions는 Azure Blob Storage에 대한 트리거, 입력 및 출력 바인딩을 지원합니다. 식 및 메타데이터 바인딩에 대한 자세한 내용은 [Azure Functions Blob Storage 바인딩](functions-bindings-storage-blob.md)을 참조하세요.

Blob 트리거가 hello로 정의 된 `[BlobTrigger]` 특성입니다. Hello 특성을 사용할 수 `[StorageAccount]` 전체 함수 또는 클래스에서 사용 되는 toodefine hello 저장소 계정입니다.

```csharp
[StorageAccount("AzureWebJobsStorage")]
[FunctionName("BlobTriggerCSharp")]        
public static void Run([BlobTrigger("samples-workitems/{name}")] Stream myBlob, string name, TraceWriter log)
{
    log.Info($"C# Blob trigger function Processed blob\n Name:{name} \n Size: {myBlob.Length} Bytes");
}
```

Blob 입력 및 출력 hello를 사용 하 여 정의 된 `[Blob]` 방향으로 표시 된 특성을 `FileAccess` 읽기 또는 쓰기 매개 변수를 나타내는입니다. 다음 예제에서는 blob 트리거 hello 및 출력 바인딩 blob입니다.

```csharp
[FunctionName("ResizeImage")]
[StorageAccount("AzureWebJobsStorage")]
public static void Run(
    [BlobTrigger("sample-images/{name}")] Stream image, 
    [Blob("sample-images-sm/{name}", FileAccess.Write)] Stream imageSmall, 
    [Blob("sample-images-md/{name}", FileAccess.Write)] Stream imageMedium)
{
    var imageBuilder = ImageResizer.ImageBuilder.Current;
    var size = imageDimensionsTable[ImageSize.Small];

    imageBuilder.Build(image, imageSmall,
        new ResizeSettings(size.Item1, size.Item2, FitMode.Max, null), false);

    image.Position = 0;
    size = imageDimensionsTable[ImageSize.Medium];

    imageBuilder.Build(image, imageMedium,
        new ResizeSettings(size.Item1, size.Item2, FitMode.Max, null), false);
}

public enum ImageSize { ExtraSmall, Small, Medium }

private static Dictionary<ImageSize, (int, int)> imageDimensionsTable = new Dictionary<ImageSize, (int, int)>() {
    { ImageSize.ExtraSmall, (320, 200) },
    { ImageSize.Small,      (640, 400) },
    { ImageSize.Medium,     (800, 600) }
};
```        

<a name="cosmos-db"></a>

### <a name="cosmos-db-input-and-output-bindings"></a>Cosmos DB 입력 및 출력 바인딩

Azure Functions는 Cosmos DB에 대한 입력 및 출력 바인딩을 지원합니다. hello Cosmos DB 바인딩의 hello 기능에 대해 자세히 toolearn 참조 [Azure 함수 Cosmos DB 바인딩](functions-bindings-documentdb.md)합니다.

hello 특성을 사용 하 여 toobind tooa Cosmos DB 문서 `[DocumentDB]` hello NuGet 패키지에 [Microsoft.Azure.WebJobs.Extensions.DocumentDB]합니다. 다음 예제는 hello에 큐 트리거 및 출력 바인딩이 DocumentDB API.

```csharp
[FunctionName("QueueToDocDB")]        
public static void Run(
    [QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] string myQueueItem, 
    [DocumentDB("ToDoList", "Items", ConnectionStringSetting = "DocDBConnection")] out dynamic document)
{
    document = new { Text = myQueueItem, id = Guid.NewGuid() };
}

```

<a name="event-hub"></a>

### <a name="event-hubs-trigger-and-output"></a>Event Hubs 트리거 및 출력

Azure Functions는 이벤트 허브에 대한 트리거 및 출력 바인딩을 지원합니다. 자세한 내용은 [Azure Functions Event Hub 바인딩](functions-bindings-event-hubs.md)를 참조하세요.

형식 hello `[Microsoft.Azure.WebJobs.ServiceBus.EventHubTriggerAttribute]` 및 `[Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute]` hello NuGet 패키지에 정의 된 [Microsoft.Azure.WebJobs.ServiceBus]합니다. 

hello 다음 예제에서는 이벤트 허브 트리거:

```csharp
[FunctionName("EventHubTriggerCSharp")]
public static void Run([EventHubTrigger("samples-workitems", Connection = "EventHubConnection")] string myEventHubMessage, TraceWriter log)
{
    log.Info($"C# Event Hub trigger function processed a message: {myEventHubMessage}");
}
```

hello 다음 예제는 hello 메서드 반환 값을 사용 하 여 hello 출력으로 출력을 이벤트 허브 있습니다.

```csharp
[FunctionName("EventHubOutput")]
[return: EventHub("outputEventHubMessage", Connection = "EventHubConnection")]
public static string Run([TimerTrigger("0 */5 * * * *")] TimerInfo myTimer, TraceWriter log)
{
    log.Info($"C# Timer trigger function executed at: {DateTime.Now}");
    return $"{DateTime.Now}";
}
```

<a name="api-hub"></a>

### <a name="external-file-input-and-output"></a>외부 파일 입력 및 출력

Azure Functions는 외부 파일(예: Google Drive, Dropbox 및 OneDrive)에 대한 트리거, 입력 및 출력 바인딩을 지원합니다. toolearn 더 참조 [Azure 함수 외부 파일 바인딩을](functions-bindings-external-file.md)합니다. 특성 hello `[ExternalFileTrigger]` 및 `[ExternalFile]` hello NuGet 패키지에 정의 된 [Microsoft.Azure.WebJobs.Extensions.ApiHub]합니다.

다음 C# 예제는 hello에 외부 파일 입력 및 출력 바인딩이 보여 줍니다. hello 코드 복사본 hello 입력된 파일 toohello 출력 파일입니다.

```csharp
[StorageAccount("MyStorageConnection")]
[FunctionName("ExternalFile")]
[return: ApiHubFile("MyFileConnection", "samples-workitems/{queueTrigger}-Copy", FileAccess.Write)]
public static string Run([QueueTrigger("myqueue-items")] string myQueueItem, 
    [ApiHubFile("MyFileConnection", "samples-workitems/{queueTrigger}", FileAccess.Read)] string myInputFile, 
    TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    return myInputFile;
}
```

<a name="http"></a>

### <a name="http-and-webhooks"></a>HTTP 및 웹후크

사용 하 여 hello `HttpTrigger` 특성 toodefine HTTP 트리거나 webhook 합니다. 이 특성은 hello NuGet 패키지에 정의 된 [Microsoft.Azure.WebJobs.Extensions.Http]합니다. Hello 인증 단계로, webhook 유형, 경로 및 메서드를 사용자 지정할 수 있습니다. hello 다음 예제에서는 트리거를 정의 HTTP 익명 인증을 사용 하 고 _genericJson_ webhook 유형입니다.

```csharp
[FunctionName("HttpTriggerCSharp")]
public static HttpResponseMessage Run([HttpTrigger(AuthorizationLevel.Anonymous, WebHookType = "genericJson")] HttpRequestMessage req)
{
    return req.CreateResponse(HttpStatusCode.OK);
}
```

<a name="mobile-apps"></a>

### <a name="mobile-apps-input-and-output"></a>Mobile Apps 입력 및 출력

Azure Functions는 Mobile Apps에 대한 입력 및 출력 바인딩을 지원합니다. toolearn 더 참조 [Azure 함수 모바일 앱 바인딩](functions-bindings-mobile-apps.md)합니다. hello 특성 `[MobileTable]` hello NuGet 패키지에 정의 된 [Microsoft.Azure.WebJobs.Extensions.MobileApps]합니다.

hello 다음 예제에서는 모바일 앱 바인딩 출력:

```csharp
[FunctionName("MobileAppsOutput")]        
[return: MobileTable(ApiKeySetting = "MyMobileAppKey", TableName = "MyTable", MobileAppUriSetting = "MyMobileAppUri")]
public static object Run([QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] string myQueueItem, TraceWriter log)
{
    return new { Text = $"I'm running in a C# function! {myQueueItem}" };
}
```

<a name="nh"></a>

### <a name="notification-hubs-output"></a>Notification Hubs 출력

Azure Functions는 Notification Hubs에 대한 출력 바인딩을 지원합니다. toolearn 더 참조 [Azure 함수 알림 허브 출력 바인딩이](functions-bindings-notification-hubs.md)합니다. hello 특성 `[NotificationHub]` hello NuGet 패키지에 정의 된 [Microsoft.Azure.WebJobs.Extensions.NotificationHubs]합니다.

<a name="queue"></a>

### <a name="queue-storage-trigger-and-output"></a>큐 저장소 트리거 및 출력

Azure Functions는 Azure 큐에 대한 트리거 및 출력 바인딩을 지원합니다. 자세한 내용은 [Azure Functions Queue Storage 바인딩](functions-bindings-storage-queue.md)을 참조하세요.

hello 다음 보여 주는 예제 toouse hello 함수 형식을 바인딩, hello를 사용 하 여 큐 출력으로 반환 하는 방법을 `[Queue]` 특성입니다. toodefine 큐 트리거를 사용 하 여 hello `[QueueTrigger]` 특성입니다.

```csharp
[StorageAccount("AzureWebJobsStorage")]
public static class QueueFunctions
{
    // HTTP trigger with queue output binding
    [FunctionName("QueueOutput")]
    [return: Queue("myqueue-items")]
    public static string QueueOutput([HttpTrigger] dynamic input,  TraceWriter log)
    {
        log.Info($"C# function processed: {input.Text}");
        return input.Text;
    }

    // Queue trigger
    [FunctionName("QueueTrigger")]
    [StorageAccount("AzureWebJobsStorage")]
    public static void QueueTrigger([QueueTrigger("myqueue-items")] string myQueueItem, TraceWriter log)
    {
        log.Info($"C# function processed: {myQueueItem}");
    }
}

```

<a name="sendgrid"></a>

### <a name="sendgrid-output"></a>SendGrid 출력

Azure Functions는 프로그래밍 방식으로 전자 메일을 보내기 위한 SendGrid 출력 바인딩을 지원합니다. toolearn 더 참조 [Azure 함수 SendGrid 바인딩](functions-bindings-sendgrid.md)합니다.

hello 특성 `[SendGrid]` hello NuGet 패키지에 정의 된 [Microsoft.Azure.WebJobs.Extensions.SendGrid]합니다.

hello 다음은 예제 서비스 버스 큐 트리거 사용 및 사용 하 여 SendGrid 출력 바인딩 `SendGridMessage`:

```csharp
[FunctionName("SendEmail")]
public static void Run(
    [ServiceBusTrigger("myqueue", AccessRights.Manage, Connection = "ServiceBusConnection")] OutgoingEmail email,
    [SendGrid] out SendGridMessage message)
{
    message = new SendGridMessage();
    message.AddTo(email.To);
    message.AddContent("text/html", email.Body);
    message.SetFrom(new EmailAddress(email.From));
    message.SetSubject(email.Subject);
}

public class OutgoingEmail
{
    public string too{ get; set; }
    public string From { get; set; }
    public string Subject { get; set; }
    public string Body { get; set; }
}
```

<a name="service-bus"></a>

### <a name="service-bus-trigger-and-output"></a>Service Bus 트리거 및 출력

Azure Functions는 Service Bus 큐 및 토픽에 대한 트리거 및 출력 바인딩을 지원합니다. 바인딩 구성에 대한 자세한 내용은 [Azure Functions Service Bus 바인딩](functions-bindings-service-bus.md)을 참조하세요.

특성 hello `[ServiceBusTrigger]` 및 `[ServiceBus]` hello NuGet 패키지에 정의 된 [Microsoft.Azure.WebJobs.ServiceBus]합니다. 

hello 다음은 서비스 버스 큐 트리거의 예:

```csharp
[FunctionName("ServiceBusQueueTriggerCSharp")]                    
public static void Run([ServiceBusTrigger("myqueue", AccessRights.Manage, Connection = "ServiceBusConnection")] string myQueueItem, TraceWriter log)
{
    log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
}
```

hello 다음은 바인딩, hello 메서드 반환 형식 hello 출력으로 사용 하 여 서비스 버스 출력의 예입니다.

```csharp
[FunctionName("ServiceBusOutput")]
[return: ServiceBus("myqueue", Connection = "ServiceBusConnection")]
public static string ServiceBusOutput([HttpTrigger] dynamic input, TraceWriter log)
{
    log.Info($"C# function processed: {input.Text}");
    return input.Text;
}
```        

<a name="table"></a>

### <a name="table-storage-input-and-output"></a>테이블 저장소 입력 및 출력

Azure Functions는 Azure Table 저장소에 대한 입력 및 출력 바인딩을 지원합니다. toolearn 더 참조 [Azure 함수 테이블 저장소 바인딩](functions-bindings-storage-table.md)합니다.

hello 다음 예제는 테이블 저장소 출력 및 입력된 바인딩을 보여 주는 두 개의 함수를 사용 하는 클래스입니다. 

```csharp
[StorageAccount("AzureWebJobsStorage")]
public class TableStorage
{
    public class MyPoco
    {
        public string PartitionKey { get; set; }
        public string RowKey { get; set; }
        public string Text { get; set; }
    }

    [FunctionName("TableOutput")]
    [return: Table("MyTable")]
    public static MyPoco TableOutput([HttpTrigger] dynamic input, TraceWriter log)
    {
        log.Info($"C# http trigger function processed: {input.Text}");
        return new MyPoco { PartitionKey = "Http", RowKey = Guid.NewGuid().ToString(), Text = input.Text };
    }

    // use hello metadata parameter "queueTrigger" toobind hello queue payload
    [FunctionName("TableInput")]
    public static void TableInput([QueueTrigger("table-items")] string input, [Table("MyTable", "Http", "{queueTrigger}")] MyPoco poco, TraceWriter log)
    {
        log.Info($"C# function processed: {poco.Text}");
    }
}

```

<a name="timer"></a>

### <a name="timer-trigger"></a>타이머 트리거

Azure Functions에는 정의된 일정에 따라 함수 코드를 실행할 수 있는 타이머 트리거 바인딩이 있습니다. hello 바인딩의 hello 기능에 대해 자세히 toolearn 참조 [Azure 함수를 사용 하 여 코드 실행을 예약](functions-bindings-timer.md)합니다.

Hello 소비 계획을 사용 하 여 일정을 정의할 수 있습니다는 [CRON 식](http://en.wikipedia.org/wiki/Cron#CRON_expression)합니다. App Service 계획을 사용하는 경우 TimeSpan 문자열을 사용할 수도 있습니다. 

다음 예제는 hello 5 분 마다 실행 하는 타이머 트리거를 정의 합니다.

```csharp
[FunctionName("TimerTriggerCSharp")]
public static void Run([TimerTrigger("0 */5 * * * *")]TimerInfo myTimer, TraceWriter log)
{
    log.Info($"C# Timer trigger function executed at: {DateTime.Now}");
}
```

<a name="twilio"></a>

### <a name="twilio-output"></a>Twilio 출력

Azure 기능 지원 Twilio 바인딩 tooenable 함수 toosend SMS 텍스트 메시지를 출력합니다. toolearn 더 참조 [hello Twilio를 사용 하 여 Azure 함수에서 보낼 SMS 메시지 출력 바인딩이](functions-bindings-twilio.md)합니다. 

hello 특성 `[TwilioSms]` hello 패키지에 정의 된 [Microsoft.Azure.WebJobs.Extensions.Twilio]합니다.

hello 다음 C# 예제에서는 큐 트리거와 Twilio 출력 바인딩:

```csharp
[FunctionName("QueueTwilio")]
[return: TwilioSms(AccountSidSetting = "TwilioAccountSid", AuthTokenSetting = "TwilioAuthToken", From = "+1425XXXXXXX" )]
public static SMSMessage Run([QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] JObject order, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {order}");

    var message = new SMSMessage()
    {
        Body = $"Hello {order["name"]}, thanks for your order!",
        too= order["mobileNumber"].ToString()
    };

    return message;
}
```

## <a name="next-steps"></a>다음 단계

C# 스크립팅에서 Azure Functions 사용에 대한 자세한 내용은 [Azure Functions C\# 스크립트 개발자 참조](functions-reference-csharp.md)를 참조하세요.

[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]


<!-- NuGet packages --> 
[Microsoft.Azure.WebJobs]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs/2.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.DocumentDB]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.DocumentDB/1.1.0-beta1
[Microsoft.Azure.WebJobs.ServiceBus]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/2.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.MobileApps]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.MobileApps/1.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.NotificationHubs]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.NotificationHubs/1.1.0-beta1
[Microsoft.Azure.WebJobs.ServiceBus]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/2.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.SendGrid]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.SendGrid/2.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.Http]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Http/1.0.0-beta1
[Microsoft.Azure.WebJobs.Extensions.BotFramework]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.BotFramework/1.0.15-beta
[Microsoft.Azure.WebJobs.Extensions.ApiHub]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.ApiHub/1.0.0-beta4
[Microsoft.Azure.WebJobs.Extensions.Twilio]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Twilio/1.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions/2.1.0-beta1


<!-- Links toosource --> 
[DocumentDBAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs
[EventHubAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs
[EventHubTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubTriggerAttribute.cs
[MobileTableAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs
[NotificationHubAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.NotificationHubs/NotificationHubAttribute.cs 
[ServiceBusAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs
[ServiceBusAccountAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs
[QueueAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs
[StorageAccountAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs
[BlobAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs
[TableAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs
[TwilioSmsAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.Twilio/TwilioSMSAttribute.cs
[SendGridAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.SendGrid/SendGridAttribute.cs
[HttpTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/dev/src/WebJobs.Extensions.Http/HttpTriggerAttribute.cs
[ApiHubFileAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.ApiHub/ApiHubFileAttribute.cs
[TimerTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerTriggerAttribute.cs

---
title: "aaaAzure 함수 C# 스크립트 개발자 참조 | Microsoft Docs"
description: "이해 방법을 toodevelop C#을 사용 하 여 Azure 함수입니다."
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "Azure Functions, 함수, 이벤트 처리, webhook, 동적 계산, 서버가 없는 아키텍처"
ms.assetid: f28cda01-15f3-4047-83f3-e89d5728301c
ms.service: functions
ms.devlang: dotnet
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/07/2017
ms.author: donnam
ms.openlocfilehash: 27a8f4eb77497a373ff4031539e2e930585e48e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-c-script-developer-reference"></a>Azure Functions C# 스크립트 개발자 참조
> [!div class="op_single_selector"]
> * [C# 스크립트](functions-reference-csharp.md)
> * [F# 스크립트](functions-reference-fsharp.md)
> * [Node.JS](functions-reference-node.md)
>
>

hello Azure 함수에 대 한 C# 스크립트 환경 hello Azure WebJobs SDK를 기반으로 합니다. 데이터는 메서드 인수를 통해 C# 함수로 흐릅니다. 인수 이름에 지정 된 `function.json`로 거 및 cancellation 토큰 함수 hello 등의 작업에 액세스 하기 위한 미리 정의 된 이름이 고 합니다.

이 문서에서는 hello 이미 읽어본 가정 [Azure 함수 개발자 참조](functions-reference.md)합니다.

C# 클래스 라이브러리 사용에 대한 자세한 내용은 [Azure Functions에서 .NET 클래스 라이브러리 사용](functions-dotnet-class-library.md)을 참조하세요.

## <a name="how-csx-works"></a>.csx의 작동 원리
hello `.csx` 형식에서는 "상용구"에 초점을 방금 C# 함수를 작성 하는 덜 toowrite 있습니다. 모든 어셈블리 참조 및 hello hello 파일 시작 부분에서 네임 스페이스를 일반적으로 포함 됩니다. 네임스페이스 및 클래스의 모든 항목을 래핑하는 대신 `Run` 메서드만 정의합니다. Tooinclude 해야 할 경우 인스턴스 toodefine 일반 이전 CLR 개체에서 개체, 내부 클래스를 포함할 수 있습니다에 대 한 모든 클래스 hello 같은 파일입니다.   

## <a name="binding-tooarguments"></a>바인딩 tooarguments
hello 다양 한 바인딩은 hello 통해 바인딩된 tooa C# 함수 `name` hello에 대 한 속성 *function.json* 구성 합니다. 각 바인딩에는 지원되는 고유한 형식이 있습니다. 예를 들어 Blob 트리거는 문자열, POCO 또는 CloudBlockBlob을 지원할 수 있습니다. 각 바인딩에 대 한 hello 참조 지원 hello 형식이 설명 되어 있습니다. POCO 개체는 각 속성에 대해 정의된 Getter 및 setter가 있어야 합니다.

```csharp
public static void Run(string myBlob, out MyClass myQueueItem)
{
    log.Verbose($"C# Blob trigger function processed: {myBlob}");
    myQueueItem = new MyClass() { Id = "myid" };
}

public class MyClass
{
    public string Id { get; set; }
}
```

[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

## <a name="using-method-return-value-for-output-binding"></a>출력 바인딩에 메서드 반환 값 사용

Hello 이름을 사용 하 여 출력 바인딩에 대 한 메서드 반환 값을 사용할 수 있습니다 `$return` 에 *function.json*:

```json
{
    "type": "queue",
    "direction": "out",
    "name": "$return",
    "queueName": "outqueue",
    "connection": "MyStorageConnectionString",
}
```

```csharp
public static string Run(string input, TraceWriter log)
{
    return input;
}
```

## <a name="writing-multiple-output-values"></a>여러 출력 값 쓰기

toowrite 여러 값 tooan 출력 바인딩, hello를 사용 하 여 [ `ICollector` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) 또는 [ `IAsyncCollector` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) 형식입니다. 이러한 유형은 서 면된 toohello 출력 바인딩 hello 메서드가 완료 되는 쓰기 전용 컬렉션입니다.

이 예에서는 `ICollector`를 사용하여 여러 큐 메시지를 씁니다.

```csharp
public static void Run(ICollector<string> myQueueItem, TraceWriter log)
{
    myQueueItem.Add("Hello");
    myQueueItem.Add("World!");
}
```

## <a name="logging"></a>로깅
형식의 인수를 포함 합니다 toolog tooyour C#에서 스트리밍 로그를 출력 `TraceWriter`합니다. 이름을 `log`로 하는 것이 좋습니다. Azure Functions에서 `Console.Write`를 사용하지 마세요. 

`TraceWriter`hello에 정의 된 [Azure WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/TraceWriter.cs)합니다. 로그 수준에 대 한 hello `TraceWriter` 에서 구성할 수 있습니다 [호스트\.json]합니다.

```csharp
public static void Run(string myBlob, TraceWriter log)
{
    log.Info($"C# Blob trigger function processed: {myBlob}");
}
```

## <a name="async"></a>Async
toomake 비동기 함수 hello를 사용 하 여 `async` 키워드 및 반환 된 `Task` 개체입니다.

```csharp
public async static Task ProcessQueueMessageAsync(
        string blobName,
        Stream blobInput,
        Stream blobOutput)
{
    await blobInput.CopyToAsync(blobOutput, 4096, token);
}
```

## <a name="cancellation-token"></a>취소 토큰
일부 작업에는 정상 종료가 필요합니다. Toohandle 정상 종료 요청을 저장할 경우에서 충돌을 처리할 수 있는 최상의 toowrite 코드 항상 하지만 정의 [ `CancellationToken` ](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) 인수를 입력 합니다.  A `CancellationToken` 호스트 종료 트리거될 toosignal 제공 됩니다.

```csharp
public async static Task ProcessQueueMessageAsyncCancellationToken(
        string blobName,
        Stream blobInput,
        Stream blobOutput,
        CancellationToken token)
    {
        await blobInput.CopyToAsync(blobOutput, 4096, token);
    }
```

## <a name="importing-namespaces"></a>네임스페이스 가져오기
Tooimport 네임 스페이스를 필요 하면 그렇게 할 수 있습니다 평소와 같이 hello로 `using` 절.

```csharp
using System.Net;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

hello 다음 네임 스페이스를 자동으로 가져오는 되며 따라서 선택 사항:

* `System`
* `System.Collections.Generic`
* `System.IO`
* `System.Linq`
* `System.Net.Http`
* `System.Threading.Tasks`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`

## <a name="referencing-external-assemblies"></a>외부 어셈블리 참조
프레임 워크 어셈블리에 대 한 hello를 사용 하 여 참조를 추가할 `#r "AssemblyName"` 지시문입니다.

```csharp
#r "System.Web.Http"

using System.Net;
using System.Net.Http;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

hello 다음 어셈블리는 자동으로 함수로 추가한 hello Azure 호스팅 환경:

* `mscorlib`
* `System`
* `System.Core`
* `System.Xml`
* `System.Net.Http`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`
* `Microsoft.Azure.WebJobs.Extensions`
* `System.Web.Http`
* `System.Net.Http.Formatting`

hello 다음 어셈블리 참조할 수 있습니다 단순한 이름 (예를 들어 `#r "AssemblyName"`):

* `Newtonsoft.Json`
* `Microsoft.WindowsAzure.Storage`
* `Microsoft.ServiceBus`
* `Microsoft.AspNet.WebHooks.Receivers`
* `Microsoft.AspNet.WebHooks.Common`
* `Microsoft.Azure.NotificationHubs`

## <a name="referencing-custom-assemblies"></a>사용자 지정 어셈블리 참조

tooreference 사용자 지정 어셈블리를 사용할 수 있습니다는 *공유* 어셈블리 또는 *개인* 어셈블리:
- 공유 어셈블리는 함수 앱 내의 모든 함수에서 공유됩니다. tooreference 사용자 지정 어셈블리와 같은 hello 어셈블리 tooyour 함수 앱에서 업로드 한 `bin` hello 함수 응용 프로그램 루트의 폴더입니다. 
- 전용 어셈블리는 지정된 함수 컨텍스트의 일부이며 여러 버전의 테스트용 로드를 지원합니다. 에 업로드 해야 합니다. 전용 어셈블리는 `bin` hello 함수 디렉터리 폴더에에서 있습니다. 와 같은 hello 파일 이름을 사용 하 여 참조 `#r "MyAssembly.dll"`합니다. 

Tooupload tooyour 함수 폴더 파일 하는 방법에 대 한 내용은 hello 패키지 관리에 대 한 섹션을 다음을 참조 하세요.

### <a name="watched-directories"></a>감시 디렉터리

변경 내용 tooassemblies hello 함수 스크립트 파일이 포함 된 hello 디렉터리 자동으로 감시 합니다. 어셈블리 변경 다른 디렉터리에 대 한 toowatch 추가할 toohello `watchDirectories` 목록에 [호스트\.json]합니다.

## <a name="using-nuget-packages"></a>NuGet 패키지 사용
C# 함수에서 toouse NuGet 패키지를 업로드 한 *project.json* toohello 함수 폴더 hello 함수 앱의 파일 시스템 파일입니다. 다음은 예제 *project.json* 참조 tooMicrosoft.ProjectOxford.Face 버전 1.1.0을 추가 하는 파일:

```json
{
  "frameworks": {
    "net46":{
      "dependencies": {
        "Microsoft.ProjectOxford.Face": "1.1.0"
      }
    }
   }
}
```

Hello.NET Framework 4.6 지원만 해야 하는 프로그램 *project.json* 파일 지정 `net46` 다음과 같이 합니다.

업로드 하는 경우는 *project.json* 파일, hello 런타임 hello 패키지를 가져오고 toohello 패키지 어셈블리 참조를 자동으로 추가 합니다. Tooadd 않아도 `#r "AssemblyName"` 지시문입니다. hello NuGet 패키지에 정의 된 toouse hello 형식을 추가 필요한 hello `using` 문 tooyour *run.csx* 파일 

Hello 함수 런타임에서 NuGet 복원 하는 비교 하 여 `project.json` 및 `project.lock.json`합니다. 경우 hello 파일의 날짜 및 시간 스탬프를 hello **없는** 일치 하는 NuGet 복원을 실행 하 고 다운로드 NuGet 패키지를 업데이트 합니다. 그러나 경우 hello, hello 파일의 날짜 및 시간 스탬프 **않습니다** 일치 하는 NuGet 복원을 수행 하지 않습니다. 따라서 `project.lock.json` NuGet tooskip 패키지를 복원 하므로 배포 하지 말아야 합니다. hello 잠금 배포 tooavoid 파일, hello 추가 `project.lock.json` toohello `.gitignore` 파일입니다.

사용자 지정 NuGet 피드를 toouse 지정 hello에 피드는 *Nuget.Config* hello 함수 응용 프로그램 루트에 파일입니다. 자세한 내용은 참조 [NuGet 동작 구성](/nuget/consume-packages/configuring-nuget-behavior)을 참조하세요.

### <a name="using-a-projectjson-file"></a>project.json 파일 사용
1. Hello Azure 포털에서에서 hello 함수를 엽니다. hello 기록 탭 hello 패키지 설치 출력을 표시 합니다.
2. project.json 파일 tooupload hello에 설명 된 hello 방법 중 하나를 사용 합니다. [tooupdate 앱 파일을 어떻게 작동 하는지](functions-reference.md#fileupdate) hello Azure 함수 개발자 참조 항목에서입니다.
3. Hello 후 *project.json* 파일 업로드, 다음 예제에서는 함수에서 hello 같은 출력이 스트리밍 로그를 참조 하십시오.

```
2016-04-04T19:02:48.745 Restoring packages.
2016-04-04T19:02:48.745 Starting NuGet restore
2016-04-04T19:02:50.183 MSBuild auto-detection: using msbuild version '14.0' from 'D:\Program Files (x86)\MSBuild\14.0\bin'.
2016-04-04T19:02:50.261 Feeds used:
2016-04-04T19:02:50.261 C:\DWASFiles\Sites\facavalfunctest\LocalAppData\NuGet\Cache
2016-04-04T19:02:50.261 https://api.nuget.org/v3/index.json
2016-04-04T19:02:50.261
2016-04-04T19:02:50.511 Restoring packages for D:\home\site\wwwroot\HttpTriggerCSharp1\Project.json...
2016-04-04T19:02:52.800 Installing Newtonsoft.Json 6.0.8.
2016-04-04T19:02:52.800 Installing Microsoft.ProjectOxford.Face 1.1.0.
2016-04-04T19:02:57.095 All packages are compatible with .NETFramework,Version=v4.6.
2016-04-04T19:02:57.189
2016-04-04T19:02:57.189
2016-04-04T19:02:57.455 Packages restored.
```

## <a name="environment-variables"></a>환경 변수
tooget 환경 변수 또는 응용 프로그램 설정 값을 사용 하 여 `System.Environment.GetEnvironmentVariable`hello 다음 코드 예제에에서 나온 것 처럼:

```csharp
public static void Run(TimerInfo myTimer, TraceWriter log)
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
```

## <a name="reusing-csx-code"></a>.csx 코드 재사용
*run.csx* 파일에 있는 다른 *.csx* 파일에 정의된 클래스와 메서드를 사용할 수 있습니다. 사용 하는 toodo `#load` 지시문에 프로그램 *run.csx* 파일입니다. 다음 예제는 hello, 로깅 루틴 이름은 `MyLogger` 의 공유 *myLogger.csx* 에 로드 하 고 *run.csx* hello를 사용 하 여 `#load` 지시문:

예제 *run.csx*:

```csharp
#load "mylogger.csx"

public static void Run(TimerInfo myTimer, TraceWriter log)
{
    log.Verbose($"Log by run.csx: {DateTime.Now}");
    MyLogger(log, $"Log by MyLogger: {DateTime.Now}");
}
```

예제 *mylogger.csx*:

```csharp
public static void MyLogger(TraceWriter log, string logtext)
{
    log.Verbose(logtext);
}
```

공유를 사용 하 여 *.csx* toostrongly 하려는 경우에 일반적인 패턴은 인수가 POCO 개체를 사용 하는 함수 사이 입력 됩니다. 다음 예에서는 간단한 hello, HTTP 트리거와 큐 트리거를 공유 라는 POCO 개체 `Order` toostrongly 형식 hello 주문 데이터:

HTTP 트리거를 위한 *run.csx* 예제:

```cs
#load "..\shared\order.csx"

using System.Net;

public static async Task<HttpResponseMessage> Run(Order req, IAsyncCollector<Order> outputQueueItem, TraceWriter log)
{
    log.Info("C# HTTP trigger function received an order.");
    log.Info(req.ToString());
    log.Info("Submitting tooprocessing queue.");

    if (req.orderId == null)
    {
        return new HttpResponseMessage(HttpStatusCode.BadRequest);
    }
    else
    {
        await outputQueueItem.AddAsync(req);
        return new HttpResponseMessage(HttpStatusCode.OK);
    }
}
```

큐 트리거를 위한 *run.csx* 예제:

```cs
#load "..\shared\order.csx"

using System;

public static void Run(Order myQueueItem, out Order outputQueueItem,TraceWriter log)
{
    log.Info($"C# Queue trigger function processed order...");
    log.Info(myQueueItem.ToString());

    outputQueueItem = myQueueItem;
}
```

*order.csx* 예제:

```cs
public class Order
{
    public string orderId {get; set; }
    public string custName {get; set;}
    public string custAddress {get; set;}
    public string custEmail {get; set;}
    public string cartId {get; set; }

    public override String ToString()
    {
        return "\n{\n\torderId : " + orderId +
                  "\n\tcustName : " + custName +             
                  "\n\tcustAddress : " + custAddress +             
                  "\n\tcustEmail : " + custEmail +             
                  "\n\tcartId : " + cartId + "\n}";             
    }
}
```

상대 경로 사용 하 여 hello로 `#load` 지시문:

* `#load "mylogger.csx"`hello 함수 폴더에 있는 파일을 로드 합니다.
* `#load "loadedfiles\mylogger.csx"`hello 함수 폴더에 있는 폴더에 있는 파일을 로드 합니다.
* `#load "..\shared\mylogger.csx"`즉, hello 함수 폴더로 수준 동일 hello에 폴더에 있는 파일을 로드 바로 아래 *wwwroot*합니다.

hello `#load` 지시문은 에서만 *.csx* (C# 스크립트) 파일 아닌 *.cs* 파일입니다.

<a name="imperative-bindings"></a> 

## <a name="binding-at-runtime-via-imperative-bindings"></a>명령적 바인딩을 통해 런타임에 바인딩

C#과 다른.NET 언어에서 사용할 수 있습니다는 [명령적](https://en.wikipedia.org/wiki/Imperative_programming) 바인딩 패턴 것과 반대로 toohello로 [ *선언적* ](https://en.wikipedia.org/wiki/Declarative_programming) 의 바인딩은 *function.json*. 명령적 바인딩 바인딩 매개 변수에 필요한 toobe 디자인 보다는 런타임 시 계산 하는 경우에 유용 합니다. 이러한 패턴에서는 toosupported 입력 바인딩하고 함수 코드에서 바인딩을 즉시 출력 수 있습니다.

다음과 같이 명령적 바인딩을 정의합니다.

- 원하는 명령적 바인딩에 대한 *function.json*에 항목을 포함하지 **마세요**.
- 입력 매개 변수 [`Binder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/Bindings/Runtime/Binder.cs) 또는 [`IBinder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IBinder.cs)에 전달합니다.
- 다음 C# 패턴 tooperform hello 데이터 바인딩을 hello를 사용 합니다.

```cs
using (var output = await binder.BindAsync<T>(new BindingTypeAttribute(...)))
{
    ...
}
```

여기서 `BindingTypeAttribute` hello.NET 특성 바인딩을 정의 하는 및 `T` 해당 바인딩 형식으로 지원 되는 입력 또는 출력 유형을 hello 됩니다. 또한 `T`는 `out` 매개 변수 형식(예: `out JObject`)일 수 없습니다. 예를 들어, Mobile Apps 테이블 출력 바인딩은 [6가지 출력 형식](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22)을 지원하지만 `T`에는 [ICollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) 또는 [IAsyncCollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs)만 사용할 수 있습니다.

다음 예제 코드는 hello 만듭니다는 [저장소 blob 출력 바인딩이](functions-bindings-storage-blob.md#using-a-blob-output-binding) blob과 런타임 시 정의 된 경로 다음 blob에 기록 문자열 toohello 합니다.

```cs
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Host.Bindings.Runtime;

public static async Task Run(string input, Binder binder)
{
    using (var writer = await binder.BindAsync<TextWriter>(new BlobAttribute("samples-output/path")))
    {
        writer.Write("Hello World!!");
    }
}
```

[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs) hello 정의 [저장소 blob](functions-bindings-storage-blob.md) 입력 또는 출력 바인딩 및 [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) 지원 되는 출력 바인딩 형식입니다.
Hello 코드 hello 저장소 계정 연결 문자열에 대 한 hello 기본 응용 프로그램 설정을 가져옵니다 이라면 (변수인 `AzureWebJobsStorage`). 추가 하 여 사용자 지정 응용 프로그램 설정을 toouse를 지정할 수는 [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) hello 특성 배열 전달 `BindAsync<T>()`합니다. 예를 들면 다음과 같습니다.

```cs
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Host.Bindings.Runtime;

public static async Task Run(string input, Binder binder)
{
    var attributes = new Attribute[]
    {    
        new BlobAttribute("samples-output/path"),
        new StorageAccountAttribute("MyStorageAccount")
    };

    using (var writer = await binder.BindAsync<TextWriter>(attributes))
    {
        writer.Write("Hello World!");
    }
}
```

hello 다음 표에 정의 되어 있는 각 바인딩 유형 및 hello 패키지에 대 한 hello.NET 특성입니다.

> [!div class="mx-codeBreakAll"]
| 바인딩 | 특성 | 추가 참조 |
|------|------|------|
| Cosmos DB | [`Microsoft.Azure.WebJobs.DocumentDBAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.DocumentDB"` |
| Event Hubs | [`Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs) | `#r "Microsoft.Azure.Jobs.ServiceBus"` |
| Mobile Apps | [`Microsoft.Azure.WebJobs.MobileTableAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.MobileApps"` |
| Notification Hubs | [`Microsoft.Azure.WebJobs.NotificationHubAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.NotificationHubs/NotificationHubAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.NotificationHubs"` |
| Service Bus | [`Microsoft.Azure.WebJobs.ServiceBusAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs) | `#r "Microsoft.Azure.WebJobs.ServiceBus"` |
| Storage 큐 | [`Microsoft.Azure.WebJobs.QueueAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) | |
| Storage Blob | [`Microsoft.Azure.WebJobs.BlobAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) | |
| Storage 테이블 | [`Microsoft.Azure.WebJobs.TableAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) | |
| Twilio | [`Microsoft.Azure.WebJobs.TwilioSmsAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.Twilio/TwilioSMSAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.Twilio"` |



## <a name="next-steps"></a>다음 단계
자세한 내용은 다음 리소스는 hello 참조:

* [Azure Functions에 대한 모범 사례](functions-best-practices.md)
* [Azure Functions 개발자 참조](functions-reference.md)
* [Azure Functions F# 개발자 참조](functions-reference-fsharp.md)
* [Azure Functions NodeJS 개발자 참조](functions-reference-node.md)
* [Azure Functions 트리거 및 바인딩](functions-triggers-bindings.md)

[host\.json]: https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json

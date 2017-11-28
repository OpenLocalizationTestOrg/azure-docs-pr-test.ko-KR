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
# <a name="azure-functions-c-script-developer-reference"></a><span data-ttu-id="ae360-104">Azure Functions C# 스크립트 개발자 참조</span><span class="sxs-lookup"><span data-stu-id="ae360-104">Azure Functions C# script developer reference</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ae360-105">C# 스크립트</span><span class="sxs-lookup"><span data-stu-id="ae360-105">C# script</span></span>](functions-reference-csharp.md)
> * [<span data-ttu-id="ae360-106">F# 스크립트</span><span class="sxs-lookup"><span data-stu-id="ae360-106">F# script</span></span>](functions-reference-fsharp.md)
> * [<span data-ttu-id="ae360-107">Node.JS</span><span class="sxs-lookup"><span data-stu-id="ae360-107">Node.js</span></span>](functions-reference-node.md)
>
>

<span data-ttu-id="ae360-108">hello Azure 함수에 대 한 C# 스크립트 환경 hello Azure WebJobs SDK를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae360-108">hello C# script experience for Azure Functions is based on hello Azure WebJobs SDK.</span></span> <span data-ttu-id="ae360-109">데이터는 메서드 인수를 통해 C# 함수로 흐릅니다.</span><span class="sxs-lookup"><span data-stu-id="ae360-109">Data flows into your C# function via method arguments.</span></span> <span data-ttu-id="ae360-110">인수 이름에 지정 된 `function.json`로 거 및 cancellation 토큰 함수 hello 등의 작업에 액세스 하기 위한 미리 정의 된 이름이 고 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae360-110">Argument names are specified in `function.json`, and there are predefined names for accessing things like hello function logger and cancellation tokens.</span></span>

<span data-ttu-id="ae360-111">이 문서에서는 hello 이미 읽어본 가정 [Azure 함수 개발자 참조](functions-reference.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ae360-111">This article assumes that you've already read hello [Azure Functions developer reference](functions-reference.md).</span></span>

<span data-ttu-id="ae360-112">C# 클래스 라이브러리 사용에 대한 자세한 내용은 [Azure Functions에서 .NET 클래스 라이브러리 사용](functions-dotnet-class-library.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ae360-112">For information on using C# class libraries, see [Using .NET class libraries with Azure Functions](functions-dotnet-class-library.md).</span></span>

## <a name="how-csx-works"></a><span data-ttu-id="ae360-113">.csx의 작동 원리</span><span class="sxs-lookup"><span data-stu-id="ae360-113">How .csx works</span></span>
<span data-ttu-id="ae360-114">hello `.csx` 형식에서는 "상용구"에 초점을 방금 C# 함수를 작성 하는 덜 toowrite 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae360-114">hello `.csx` format allows you toowrite less "boilerplate" and focus on writing just a C# function.</span></span> <span data-ttu-id="ae360-115">모든 어셈블리 참조 및 hello hello 파일 시작 부분에서 네임 스페이스를 일반적으로 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae360-115">Include any assembly references and namespaces at hello beginning of hello file as usual.</span></span> <span data-ttu-id="ae360-116">네임스페이스 및 클래스의 모든 항목을 래핑하는 대신 `Run` 메서드만 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="ae360-116">Instead of wrapping everything in a namespace and class, just define a `Run` method.</span></span> <span data-ttu-id="ae360-117">Tooinclude 해야 할 경우 인스턴스 toodefine 일반 이전 CLR 개체에서 개체, 내부 클래스를 포함할 수 있습니다에 대 한 모든 클래스 hello 같은 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="ae360-117">If you need tooinclude any classes, for instance toodefine Plain Old CLR Object (POCO) objects, you can include a class inside hello same file.</span></span>   

## <a name="binding-tooarguments"></a><span data-ttu-id="ae360-118">바인딩 tooarguments</span><span class="sxs-lookup"><span data-stu-id="ae360-118">Binding tooarguments</span></span>
<span data-ttu-id="ae360-119">hello 다양 한 바인딩은 hello 통해 바인딩된 tooa C# 함수 `name` hello에 대 한 속성 *function.json* 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae360-119">hello various bindings are bound tooa C# function via hello `name` property in hello *function.json* configuration.</span></span> <span data-ttu-id="ae360-120">각 바인딩에는 지원되는 고유한 형식이 있습니다. 예를 들어 Blob 트리거는 문자열, POCO 또는 CloudBlockBlob을 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae360-120">Each binding has its own supported types; for instance, a blob trigger can support a string, a POCO, or a CloudBlockBlob.</span></span> <span data-ttu-id="ae360-121">각 바인딩에 대 한 hello 참조 지원 hello 형식이 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae360-121">hello supported types are documented in hello reference for each binding.</span></span> <span data-ttu-id="ae360-122">POCO 개체는 각 속성에 대해 정의된 Getter 및 setter가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae360-122">A POCO object must have a getter and setter defined for each property.</span></span>

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

## <a name="using-method-return-value-for-output-binding"></a><span data-ttu-id="ae360-123">출력 바인딩에 메서드 반환 값 사용</span><span class="sxs-lookup"><span data-stu-id="ae360-123">Using method return value for output binding</span></span>

<span data-ttu-id="ae360-124">Hello 이름을 사용 하 여 출력 바인딩에 대 한 메서드 반환 값을 사용할 수 있습니다 `$return` 에 *function.json*:</span><span class="sxs-lookup"><span data-stu-id="ae360-124">You can use a method return value for an output binding, by using hello name `$return` in *function.json*:</span></span>

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

## <a name="writing-multiple-output-values"></a><span data-ttu-id="ae360-125">여러 출력 값 쓰기</span><span class="sxs-lookup"><span data-stu-id="ae360-125">Writing multiple output values</span></span>

<span data-ttu-id="ae360-126">toowrite 여러 값 tooan 출력 바인딩, hello를 사용 하 여 [ `ICollector` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) 또는 [ `IAsyncCollector` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="ae360-126">toowrite multiple values tooan output binding, use hello [`ICollector`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) or [`IAsyncCollector`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) types.</span></span> <span data-ttu-id="ae360-127">이러한 유형은 서 면된 toohello 출력 바인딩 hello 메서드가 완료 되는 쓰기 전용 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="ae360-127">These types are write-only collections that are written toohello output binding when hello method completes.</span></span>

<span data-ttu-id="ae360-128">이 예에서는 `ICollector`를 사용하여 여러 큐 메시지를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="ae360-128">This example writes multiple queue messages using `ICollector`:</span></span>

```csharp
public static void Run(ICollector<string> myQueueItem, TraceWriter log)
{
    myQueueItem.Add("Hello");
    myQueueItem.Add("World!");
}
```

## <a name="logging"></a><span data-ttu-id="ae360-129">로깅</span><span class="sxs-lookup"><span data-stu-id="ae360-129">Logging</span></span>
<span data-ttu-id="ae360-130">형식의 인수를 포함 합니다 toolog tooyour C#에서 스트리밍 로그를 출력 `TraceWriter`합니다.</span><span class="sxs-lookup"><span data-stu-id="ae360-130">toolog output tooyour streaming logs in C#, include an argument of type `TraceWriter`.</span></span> <span data-ttu-id="ae360-131">이름을 `log`로 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ae360-131">We recommend that you name it `log`.</span></span> <span data-ttu-id="ae360-132">Azure Functions에서 `Console.Write`를 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="ae360-132">Avoid using `Console.Write` in Azure Functions.</span></span> 

<span data-ttu-id="ae360-133">`TraceWriter`hello에 정의 된 [Azure WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/TraceWriter.cs)합니다.</span><span class="sxs-lookup"><span data-stu-id="ae360-133">`TraceWriter` is defined in hello [Azure WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/TraceWriter.cs).</span></span> <span data-ttu-id="ae360-134">로그 수준에 대 한 hello `TraceWriter` 에서 구성할 수 있습니다 [호스트\.json]합니다.</span><span class="sxs-lookup"><span data-stu-id="ae360-134">hello log level for `TraceWriter` can be configured in [host\.json].</span></span>

```csharp
public static void Run(string myBlob, TraceWriter log)
{
    log.Info($"C# Blob trigger function processed: {myBlob}");
}
```

## <a name="async"></a><span data-ttu-id="ae360-135">Async</span><span class="sxs-lookup"><span data-stu-id="ae360-135">Async</span></span>
<span data-ttu-id="ae360-136">toomake 비동기 함수 hello를 사용 하 여 `async` 키워드 및 반환 된 `Task` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="ae360-136">toomake a function asynchronous, use hello `async` keyword and return a `Task` object.</span></span>

```csharp
public async static Task ProcessQueueMessageAsync(
        string blobName,
        Stream blobInput,
        Stream blobOutput)
{
    await blobInput.CopyToAsync(blobOutput, 4096, token);
}
```

## <a name="cancellation-token"></a><span data-ttu-id="ae360-137">취소 토큰</span><span class="sxs-lookup"><span data-stu-id="ae360-137">Cancellation Token</span></span>
<span data-ttu-id="ae360-138">일부 작업에는 정상 종료가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ae360-138">Some operations require graceful shutdown.</span></span> <span data-ttu-id="ae360-139">Toohandle 정상 종료 요청을 저장할 경우에서 충돌을 처리할 수 있는 최상의 toowrite 코드 항상 하지만 정의 [ `CancellationToken` ](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) 인수를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae360-139">While it's always best toowrite code that can handle crashing,  in cases where you want toohandle graceful shutdown requests, you define a [`CancellationToken`](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) typed argument.</span></span>  <span data-ttu-id="ae360-140">A `CancellationToken` 호스트 종료 트리거될 toosignal 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae360-140">A `CancellationToken` is provided toosignal that a host shutdown is triggered.</span></span>

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

## <a name="importing-namespaces"></a><span data-ttu-id="ae360-141">네임스페이스 가져오기</span><span class="sxs-lookup"><span data-stu-id="ae360-141">Importing namespaces</span></span>
<span data-ttu-id="ae360-142">Tooimport 네임 스페이스를 필요 하면 그렇게 할 수 있습니다 평소와 같이 hello로 `using` 절.</span><span class="sxs-lookup"><span data-stu-id="ae360-142">If you need tooimport namespaces, you can do so as usual, with hello `using` clause.</span></span>

```csharp
using System.Net;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

<span data-ttu-id="ae360-143">hello 다음 네임 스페이스를 자동으로 가져오는 되며 따라서 선택 사항:</span><span class="sxs-lookup"><span data-stu-id="ae360-143">hello following namespaces are automatically imported and are therefore optional:</span></span>

* `System`
* `System.Collections.Generic`
* `System.IO`
* `System.Linq`
* `System.Net.Http`
* `System.Threading.Tasks`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`

## <a name="referencing-external-assemblies"></a><span data-ttu-id="ae360-144">외부 어셈블리 참조</span><span class="sxs-lookup"><span data-stu-id="ae360-144">Referencing External Assemblies</span></span>
<span data-ttu-id="ae360-145">프레임 워크 어셈블리에 대 한 hello를 사용 하 여 참조를 추가할 `#r "AssemblyName"` 지시문입니다.</span><span class="sxs-lookup"><span data-stu-id="ae360-145">For framework assemblies, add references by using hello `#r "AssemblyName"` directive.</span></span>

```csharp
#r "System.Web.Http"

using System.Net;
using System.Net.Http;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

<span data-ttu-id="ae360-146">hello 다음 어셈블리는 자동으로 함수로 추가한 hello Azure 호스팅 환경:</span><span class="sxs-lookup"><span data-stu-id="ae360-146">hello following assemblies are automatically added by hello Azure Functions hosting environment:</span></span>

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

<span data-ttu-id="ae360-147">hello 다음 어셈블리 참조할 수 있습니다 단순한 이름 (예를 들어 `#r "AssemblyName"`):</span><span class="sxs-lookup"><span data-stu-id="ae360-147">hello following assemblies may be referenced by simple-name (for example, `#r "AssemblyName"`):</span></span>

* `Newtonsoft.Json`
* `Microsoft.WindowsAzure.Storage`
* `Microsoft.ServiceBus`
* `Microsoft.AspNet.WebHooks.Receivers`
* `Microsoft.AspNet.WebHooks.Common`
* `Microsoft.Azure.NotificationHubs`

## <a name="referencing-custom-assemblies"></a><span data-ttu-id="ae360-148">사용자 지정 어셈블리 참조</span><span class="sxs-lookup"><span data-stu-id="ae360-148">Referencing custom assemblies</span></span>

<span data-ttu-id="ae360-149">tooreference 사용자 지정 어셈블리를 사용할 수 있습니다는 *공유* 어셈블리 또는 *개인* 어셈블리:</span><span class="sxs-lookup"><span data-stu-id="ae360-149">tooreference a custom assembly, you can use either a *shared* assembly or a *private* assembly:</span></span>
- <span data-ttu-id="ae360-150">공유 어셈블리는 함수 앱 내의 모든 함수에서 공유됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae360-150">Shared assemblies are shared across all functions within a function app.</span></span> <span data-ttu-id="ae360-151">tooreference 사용자 지정 어셈블리와 같은 hello 어셈블리 tooyour 함수 앱에서 업로드 한 `bin` hello 함수 응용 프로그램 루트의 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="ae360-151">tooreference a custom assembly, upload hello assembly tooyour function app, such as in a `bin` folder in hello function app root.</span></span> 
- <span data-ttu-id="ae360-152">전용 어셈블리는 지정된 함수 컨텍스트의 일부이며 여러 버전의 테스트용 로드를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ae360-152">Private assemblies are part of a given function's context, and support side-loading of different versions.</span></span> <span data-ttu-id="ae360-153">에 업로드 해야 합니다. 전용 어셈블리는 `bin` hello 함수 디렉터리 폴더에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae360-153">Private assemblies should be uploaded in a `bin` folder in hello function directory.</span></span> <span data-ttu-id="ae360-154">와 같은 hello 파일 이름을 사용 하 여 참조 `#r "MyAssembly.dll"`합니다.</span><span class="sxs-lookup"><span data-stu-id="ae360-154">Reference using hello file name, such as  `#r "MyAssembly.dll"`.</span></span> 

<span data-ttu-id="ae360-155">Tooupload tooyour 함수 폴더 파일 하는 방법에 대 한 내용은 hello 패키지 관리에 대 한 섹션을 다음을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="ae360-155">For information on how tooupload files tooyour function folder, see hello following section on package management.</span></span>

### <a name="watched-directories"></a><span data-ttu-id="ae360-156">감시 디렉터리</span><span class="sxs-lookup"><span data-stu-id="ae360-156">Watched directories</span></span>

<span data-ttu-id="ae360-157">변경 내용 tooassemblies hello 함수 스크립트 파일이 포함 된 hello 디렉터리 자동으로 감시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae360-157">hello directory that contains hello function script file is automatically watched for changes tooassemblies.</span></span> <span data-ttu-id="ae360-158">어셈블리 변경 다른 디렉터리에 대 한 toowatch 추가할 toohello `watchDirectories` 목록에 [호스트\.json]합니다.</span><span class="sxs-lookup"><span data-stu-id="ae360-158">toowatch for assembly changes in other directories, add them toohello `watchDirectories` list in [host\.json].</span></span>

## <a name="using-nuget-packages"></a><span data-ttu-id="ae360-159">NuGet 패키지 사용</span><span class="sxs-lookup"><span data-stu-id="ae360-159">Using NuGet packages</span></span>
<span data-ttu-id="ae360-160">C# 함수에서 toouse NuGet 패키지를 업로드 한 *project.json* toohello 함수 폴더 hello 함수 앱의 파일 시스템 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="ae360-160">toouse NuGet packages in a C# function, upload a *project.json* file toohello function's folder in hello function app's file system.</span></span> <span data-ttu-id="ae360-161">다음은 예제 *project.json* 참조 tooMicrosoft.ProjectOxford.Face 버전 1.1.0을 추가 하는 파일:</span><span class="sxs-lookup"><span data-stu-id="ae360-161">Here is an example *project.json* file that adds a reference tooMicrosoft.ProjectOxford.Face version 1.1.0:</span></span>

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

<span data-ttu-id="ae360-162">Hello.NET Framework 4.6 지원만 해야 하는 프로그램 *project.json* 파일 지정 `net46` 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae360-162">Only hello .NET Framework 4.6 is supported, so make sure that your *project.json* file specifies `net46` as shown here.</span></span>

<span data-ttu-id="ae360-163">업로드 하는 경우는 *project.json* 파일, hello 런타임 hello 패키지를 가져오고 toohello 패키지 어셈블리 참조를 자동으로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae360-163">When you upload a *project.json* file, hello runtime gets hello packages and automatically adds references toohello package assemblies.</span></span> <span data-ttu-id="ae360-164">Tooadd 않아도 `#r "AssemblyName"` 지시문입니다.</span><span class="sxs-lookup"><span data-stu-id="ae360-164">You don't need tooadd `#r "AssemblyName"` directives.</span></span> <span data-ttu-id="ae360-165">hello NuGet 패키지에 정의 된 toouse hello 형식을 추가 필요한 hello `using` 문 tooyour *run.csx* 파일</span><span class="sxs-lookup"><span data-stu-id="ae360-165">toouse hello types defined in hello NuGet packages, add hello required `using` statements tooyour *run.csx* file</span></span> 

<span data-ttu-id="ae360-166">Hello 함수 런타임에서 NuGet 복원 하는 비교 하 여 `project.json` 및 `project.lock.json`합니다.</span><span class="sxs-lookup"><span data-stu-id="ae360-166">In hello Functions runtime, NuGet restore works by comparing `project.json` and `project.lock.json`.</span></span> <span data-ttu-id="ae360-167">경우 hello 파일의 날짜 및 시간 스탬프를 hello **없는** 일치 하는 NuGet 복원을 실행 하 고 다운로드 NuGet 패키지를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae360-167">If hello date and time stamps of hello files **do not** match, a NuGet restore runs and NuGet downloads updated packages.</span></span> <span data-ttu-id="ae360-168">그러나 경우 hello, hello 파일의 날짜 및 시간 스탬프 **않습니다** 일치 하는 NuGet 복원을 수행 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ae360-168">However, if hello date and time stamps of hello files **do** match, NuGet does not perform a restore.</span></span> <span data-ttu-id="ae360-169">따라서 `project.lock.json` NuGet tooskip 패키지를 복원 하므로 배포 하지 말아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae360-169">Therefore, `project.lock.json` should not be deployed as it causes NuGet tooskip package restore.</span></span> <span data-ttu-id="ae360-170">hello 잠금 배포 tooavoid 파일, hello 추가 `project.lock.json` toohello `.gitignore` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="ae360-170">tooavoid deploying hello lock file, add hello `project.lock.json` toohello `.gitignore` file.</span></span>

<span data-ttu-id="ae360-171">사용자 지정 NuGet 피드를 toouse 지정 hello에 피드는 *Nuget.Config* hello 함수 응용 프로그램 루트에 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="ae360-171">toouse a custom NuGet feed, specify hello feed in a *Nuget.Config* file in hello Function App root.</span></span> <span data-ttu-id="ae360-172">자세한 내용은 참조 [NuGet 동작 구성](/nuget/consume-packages/configuring-nuget-behavior)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ae360-172">For more information, see [Configuring NuGet behavior](/nuget/consume-packages/configuring-nuget-behavior).</span></span>

### <a name="using-a-projectjson-file"></a><span data-ttu-id="ae360-173">project.json 파일 사용</span><span class="sxs-lookup"><span data-stu-id="ae360-173">Using a project.json file</span></span>
1. <span data-ttu-id="ae360-174">Hello Azure 포털에서에서 hello 함수를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ae360-174">Open hello function in hello Azure portal.</span></span> <span data-ttu-id="ae360-175">hello 기록 탭 hello 패키지 설치 출력을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae360-175">hello logs tab displays hello package installation output.</span></span>
2. <span data-ttu-id="ae360-176">project.json 파일 tooupload hello에 설명 된 hello 방법 중 하나를 사용 합니다. [tooupdate 앱 파일을 어떻게 작동 하는지](functions-reference.md#fileupdate) hello Azure 함수 개발자 참조 항목에서입니다.</span><span class="sxs-lookup"><span data-stu-id="ae360-176">tooupload a project.json file, use one of hello methods described in hello [How tooupdate function app files](functions-reference.md#fileupdate) in hello Azure Functions developer reference topic.</span></span>
3. <span data-ttu-id="ae360-177">Hello 후 *project.json* 파일 업로드, 다음 예제에서는 함수에서 hello 같은 출력이 스트리밍 로그를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="ae360-177">After hello *project.json* file is uploaded, you see output like hello following example in your function's streaming log:</span></span>

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

## <a name="environment-variables"></a><span data-ttu-id="ae360-178">환경 변수</span><span class="sxs-lookup"><span data-stu-id="ae360-178">Environment variables</span></span>
<span data-ttu-id="ae360-179">tooget 환경 변수 또는 응용 프로그램 설정 값을 사용 하 여 `System.Environment.GetEnvironmentVariable`hello 다음 코드 예제에에서 나온 것 처럼:</span><span class="sxs-lookup"><span data-stu-id="ae360-179">tooget an environment variable or an app setting value, use `System.Environment.GetEnvironmentVariable`, as shown in hello following code example:</span></span>

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

## <a name="reusing-csx-code"></a><span data-ttu-id="ae360-180">.csx 코드 재사용</span><span class="sxs-lookup"><span data-stu-id="ae360-180">Reusing .csx code</span></span>
<span data-ttu-id="ae360-181">*run.csx* 파일에 있는 다른 *.csx* 파일에 정의된 클래스와 메서드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae360-181">You can use classes and methods defined in other *.csx* files in your *run.csx* file.</span></span> <span data-ttu-id="ae360-182">사용 하는 toodo `#load` 지시문에 프로그램 *run.csx* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="ae360-182">toodo that, use `#load` directives in your *run.csx* file.</span></span> <span data-ttu-id="ae360-183">다음 예제는 hello, 로깅 루틴 이름은 `MyLogger` 의 공유 *myLogger.csx* 에 로드 하 고 *run.csx* hello를 사용 하 여 `#load` 지시문:</span><span class="sxs-lookup"><span data-stu-id="ae360-183">In hello following example, a logging routine named `MyLogger` is shared in *myLogger.csx* and loaded into *run.csx* using hello `#load` directive:</span></span>

<span data-ttu-id="ae360-184">예제 *run.csx*:</span><span class="sxs-lookup"><span data-stu-id="ae360-184">Example *run.csx*:</span></span>

```csharp
#load "mylogger.csx"

public static void Run(TimerInfo myTimer, TraceWriter log)
{
    log.Verbose($"Log by run.csx: {DateTime.Now}");
    MyLogger(log, $"Log by MyLogger: {DateTime.Now}");
}
```

<span data-ttu-id="ae360-185">예제 *mylogger.csx*:</span><span class="sxs-lookup"><span data-stu-id="ae360-185">Example *mylogger.csx*:</span></span>

```csharp
public static void MyLogger(TraceWriter log, string logtext)
{
    log.Verbose(logtext);
}
```

<span data-ttu-id="ae360-186">공유를 사용 하 여 *.csx* toostrongly 하려는 경우에 일반적인 패턴은 인수가 POCO 개체를 사용 하는 함수 사이 입력 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae360-186">Using a shared *.csx* is a common pattern when you want toostrongly type your arguments between functions using a POCO object.</span></span> <span data-ttu-id="ae360-187">다음 예에서는 간단한 hello, HTTP 트리거와 큐 트리거를 공유 라는 POCO 개체 `Order` toostrongly 형식 hello 주문 데이터:</span><span class="sxs-lookup"><span data-stu-id="ae360-187">In hello following simplified example, an HTTP trigger and queue trigger share a POCO object named `Order` toostrongly type hello order data:</span></span>

<span data-ttu-id="ae360-188">HTTP 트리거를 위한 *run.csx* 예제:</span><span class="sxs-lookup"><span data-stu-id="ae360-188">Example *run.csx* for HTTP trigger:</span></span>

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

<span data-ttu-id="ae360-189">큐 트리거를 위한 *run.csx* 예제:</span><span class="sxs-lookup"><span data-stu-id="ae360-189">Example *run.csx* for queue trigger:</span></span>

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

<span data-ttu-id="ae360-190">*order.csx* 예제:</span><span class="sxs-lookup"><span data-stu-id="ae360-190">Example *order.csx*:</span></span>

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

<span data-ttu-id="ae360-191">상대 경로 사용 하 여 hello로 `#load` 지시문:</span><span class="sxs-lookup"><span data-stu-id="ae360-191">You can use a relative path with hello `#load` directive:</span></span>

* <span data-ttu-id="ae360-192">`#load "mylogger.csx"`hello 함수 폴더에 있는 파일을 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae360-192">`#load "mylogger.csx"` loads a file located in hello function folder.</span></span>
* <span data-ttu-id="ae360-193">`#load "loadedfiles\mylogger.csx"`hello 함수 폴더에 있는 폴더에 있는 파일을 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae360-193">`#load "loadedfiles\mylogger.csx"` loads a file located in a folder in hello function folder.</span></span>
* <span data-ttu-id="ae360-194">`#load "..\shared\mylogger.csx"`즉, hello 함수 폴더로 수준 동일 hello에 폴더에 있는 파일을 로드 바로 아래 *wwwroot*합니다.</span><span class="sxs-lookup"><span data-stu-id="ae360-194">`#load "..\shared\mylogger.csx"` loads a file located in a folder at hello same level as hello function folder, that is, directly under *wwwroot*.</span></span>

<span data-ttu-id="ae360-195">hello `#load` 지시문은 에서만 *.csx* (C# 스크립트) 파일 아닌 *.cs* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="ae360-195">hello `#load` directive works only with *.csx* (C# script) files, not with *.cs* files.</span></span>

<a name="imperative-bindings"></a> 

## <a name="binding-at-runtime-via-imperative-bindings"></a><span data-ttu-id="ae360-196">명령적 바인딩을 통해 런타임에 바인딩</span><span class="sxs-lookup"><span data-stu-id="ae360-196">Binding at runtime via imperative bindings</span></span>

<span data-ttu-id="ae360-197">C#과 다른.NET 언어에서 사용할 수 있습니다는 [명령적](https://en.wikipedia.org/wiki/Imperative_programming) 바인딩 패턴 것과 반대로 toohello로 [ *선언적* ](https://en.wikipedia.org/wiki/Declarative_programming) 의 바인딩은 *function.json*.</span><span class="sxs-lookup"><span data-stu-id="ae360-197">In C# and other .NET languages, you can use an [imperative](https://en.wikipedia.org/wiki/Imperative_programming) binding pattern, as opposed toohello [*declarative*](https://en.wikipedia.org/wiki/Declarative_programming) bindings in *function.json*.</span></span> <span data-ttu-id="ae360-198">명령적 바인딩 바인딩 매개 변수에 필요한 toobe 디자인 보다는 런타임 시 계산 하는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae360-198">Imperative binding is useful when binding parameters need toobe computed at runtime rather than design time.</span></span> <span data-ttu-id="ae360-199">이러한 패턴에서는 toosupported 입력 바인딩하고 함수 코드에서 바인딩을 즉시 출력 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae360-199">With this pattern, you can bind toosupported input and output binding on-the-fly in your function code.</span></span>

<span data-ttu-id="ae360-200">다음과 같이 명령적 바인딩을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="ae360-200">Define an imperative binding as follows:</span></span>

- <span data-ttu-id="ae360-201">원하는 명령적 바인딩에 대한 *function.json*에 항목을 포함하지 **마세요**.</span><span class="sxs-lookup"><span data-stu-id="ae360-201">**Do not** include an entry in *function.json* for your desired imperative bindings.</span></span>
- <span data-ttu-id="ae360-202">입력 매개 변수 [`Binder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/Bindings/Runtime/Binder.cs) 또는 [`IBinder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IBinder.cs)에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="ae360-202">Pass in an input parameter [`Binder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/Bindings/Runtime/Binder.cs) or [`IBinder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IBinder.cs).</span></span>
- <span data-ttu-id="ae360-203">다음 C# 패턴 tooperform hello 데이터 바인딩을 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae360-203">Use hello following C# pattern tooperform hello data binding.</span></span>

```cs
using (var output = await binder.BindAsync<T>(new BindingTypeAttribute(...)))
{
    ...
}
```

<span data-ttu-id="ae360-204">여기서 `BindingTypeAttribute` hello.NET 특성 바인딩을 정의 하는 및 `T` 해당 바인딩 형식으로 지원 되는 입력 또는 출력 유형을 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae360-204">where `BindingTypeAttribute` is hello .NET attribute that defines your binding and `T` is hello input or output type that's supported by that binding type.</span></span> <span data-ttu-id="ae360-205">또한 `T`는 `out` 매개 변수 형식(예: `out JObject`)일 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ae360-205">`T` also cannot be an `out` parameter type (such as `out JObject`).</span></span> <span data-ttu-id="ae360-206">예를 들어, Mobile Apps 테이블 출력 바인딩은 [6가지 출력 형식](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22)을 지원하지만 `T`에는 [ICollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) 또는 [IAsyncCollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs)만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae360-206">For example, the Mobile Apps table output binding supports [six output types](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22), but you can only use [ICollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) or [IAsyncCollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) for `T`.</span></span>

<span data-ttu-id="ae360-207">다음 예제 코드는 hello 만듭니다는 [저장소 blob 출력 바인딩이](functions-bindings-storage-blob.md#using-a-blob-output-binding) blob과 런타임 시 정의 된 경로 다음 blob에 기록 문자열 toohello 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae360-207">hello following example code creates a [Storage blob output binding](functions-bindings-storage-blob.md#using-a-blob-output-binding) with blob path that's defined at run time, then writes a string toohello blob.</span></span>

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

<span data-ttu-id="ae360-208">[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs) hello 정의 [저장소 blob](functions-bindings-storage-blob.md) 입력 또는 출력 바인딩 및 [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) 지원 되는 출력 바인딩 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="ae360-208">[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs) defines hello [Storage blob](functions-bindings-storage-blob.md) input or output binding, and [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) is a supported output binding type.</span></span>
<span data-ttu-id="ae360-209">Hello 코드 hello 저장소 계정 연결 문자열에 대 한 hello 기본 응용 프로그램 설정을 가져옵니다 이라면 (변수인 `AzureWebJobsStorage`).</span><span class="sxs-lookup"><span data-stu-id="ae360-209">As is, hello code gets hello default app setting for hello Storage account connection string (which is `AzureWebJobsStorage`).</span></span> <span data-ttu-id="ae360-210">추가 하 여 사용자 지정 응용 프로그램 설정을 toouse를 지정할 수는 [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) hello 특성 배열 전달 `BindAsync<T>()`합니다.</span><span class="sxs-lookup"><span data-stu-id="ae360-210">You can specify a custom app setting toouse by adding the [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) and passing hello attribute array into `BindAsync<T>()`.</span></span> <span data-ttu-id="ae360-211">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ae360-211">For example,</span></span>

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

<span data-ttu-id="ae360-212">hello 다음 표에 정의 되어 있는 각 바인딩 유형 및 hello 패키지에 대 한 hello.NET 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="ae360-212">hello following table lists hello .NET attributes for each binding type and hello packages in which they are defined.</span></span>

> [!div class="mx-codeBreakAll"]
| <span data-ttu-id="ae360-213">바인딩</span><span class="sxs-lookup"><span data-stu-id="ae360-213">Binding</span></span> | <span data-ttu-id="ae360-214">특성</span><span class="sxs-lookup"><span data-stu-id="ae360-214">Attribute</span></span> | <span data-ttu-id="ae360-215">추가 참조</span><span class="sxs-lookup"><span data-stu-id="ae360-215">Add reference</span></span> |
|------|------|------|
| <span data-ttu-id="ae360-216">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="ae360-216">Cosmos DB</span></span> | [`Microsoft.Azure.WebJobs.DocumentDBAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.DocumentDB"` |
| <span data-ttu-id="ae360-217">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="ae360-217">Event Hubs</span></span> | <span data-ttu-id="ae360-218">[`Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="ae360-218">[`Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span></span> | `#r "Microsoft.Azure.Jobs.ServiceBus"` |
| <span data-ttu-id="ae360-219">Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="ae360-219">Mobile Apps</span></span> | [`Microsoft.Azure.WebJobs.MobileTableAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.MobileApps"` |
| <span data-ttu-id="ae360-220">Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="ae360-220">Notification Hubs</span></span> | [`Microsoft.Azure.WebJobs.NotificationHubAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.NotificationHubs/NotificationHubAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.NotificationHubs"` |
| <span data-ttu-id="ae360-221">Service Bus</span><span class="sxs-lookup"><span data-stu-id="ae360-221">Service Bus</span></span> | <span data-ttu-id="ae360-222">[`Microsoft.Azure.WebJobs.ServiceBusAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="ae360-222">[`Microsoft.Azure.WebJobs.ServiceBusAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span></span> | `#r "Microsoft.Azure.WebJobs.ServiceBus"` |
| <span data-ttu-id="ae360-223">Storage 큐</span><span class="sxs-lookup"><span data-stu-id="ae360-223">Storage queue</span></span> | <span data-ttu-id="ae360-224">[`Microsoft.Azure.WebJobs.QueueAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="ae360-224">[`Microsoft.Azure.WebJobs.QueueAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span></span> | |
| <span data-ttu-id="ae360-225">Storage Blob</span><span class="sxs-lookup"><span data-stu-id="ae360-225">Storage blob</span></span> | <span data-ttu-id="ae360-226">[`Microsoft.Azure.WebJobs.BlobAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="ae360-226">[`Microsoft.Azure.WebJobs.BlobAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span></span> | |
| <span data-ttu-id="ae360-227">Storage 테이블</span><span class="sxs-lookup"><span data-stu-id="ae360-227">Storage table</span></span> | <span data-ttu-id="ae360-228">[`Microsoft.Azure.WebJobs.TableAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="ae360-228">[`Microsoft.Azure.WebJobs.TableAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span></span> | |
| <span data-ttu-id="ae360-229">Twilio</span><span class="sxs-lookup"><span data-stu-id="ae360-229">Twilio</span></span> | [`Microsoft.Azure.WebJobs.TwilioSmsAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.Twilio/TwilioSMSAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.Twilio"` |



## <a name="next-steps"></a><span data-ttu-id="ae360-230">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ae360-230">Next steps</span></span>
<span data-ttu-id="ae360-231">자세한 내용은 다음 리소스는 hello 참조:</span><span class="sxs-lookup"><span data-stu-id="ae360-231">For more information, see hello following resources:</span></span>

* [<span data-ttu-id="ae360-232">Azure Functions에 대한 모범 사례</span><span class="sxs-lookup"><span data-stu-id="ae360-232">Best Practices for Azure Functions</span></span>](functions-best-practices.md)
* [<span data-ttu-id="ae360-233">Azure Functions 개발자 참조</span><span class="sxs-lookup"><span data-stu-id="ae360-233">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="ae360-234">Azure Functions F# 개발자 참조</span><span class="sxs-lookup"><span data-stu-id="ae360-234">Azure Functions F# developer reference</span></span>](functions-reference-fsharp.md)
* [<span data-ttu-id="ae360-235">Azure Functions NodeJS 개발자 참조</span><span class="sxs-lookup"><span data-stu-id="ae360-235">Azure Functions NodeJS developer reference</span></span>](functions-reference-node.md)
* [<span data-ttu-id="ae360-236">Azure Functions 트리거 및 바인딩</span><span class="sxs-lookup"><span data-stu-id="ae360-236">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)

[host\.json]: https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json

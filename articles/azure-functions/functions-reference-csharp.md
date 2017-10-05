---
title: "Azure Functions C# 스크립트 개발자 참조 | Microsoft Docs"
description: "C#을 사용하여 Azure Functions를 개발하는 방법을 알아봅니다."
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
ms.openlocfilehash: 83a351ce0279ada8ce7fe0513497349471334a86
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-c-script-developer-reference"></a><span data-ttu-id="5d241-104">Azure Functions C# 스크립트 개발자 참조</span><span class="sxs-lookup"><span data-stu-id="5d241-104">Azure Functions C# script developer reference</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5d241-105">C# 스크립트</span><span class="sxs-lookup"><span data-stu-id="5d241-105">C# script</span></span>](functions-reference-csharp.md)
> * [<span data-ttu-id="5d241-106">F# 스크립트</span><span class="sxs-lookup"><span data-stu-id="5d241-106">F# script</span></span>](functions-reference-fsharp.md)
> * [<span data-ttu-id="5d241-107">Node.JS</span><span class="sxs-lookup"><span data-stu-id="5d241-107">Node.js</span></span>](functions-reference-node.md)
>
>

<span data-ttu-id="5d241-108">Azure Functions에 대한 C# 스크립트 환경은 Azure WebJobs SDK를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-108">The C# script experience for Azure Functions is based on the Azure WebJobs SDK.</span></span> <span data-ttu-id="5d241-109">데이터는 메서드 인수를 통해 C# 함수로 흐릅니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-109">Data flows into your C# function via method arguments.</span></span> <span data-ttu-id="5d241-110">인수 이름은 `function.json`에 지정되며 함수 로거 및 취소 토큰 같은 항목에 액세스하기 위해 미리 정의된 이름이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-110">Argument names are specified in `function.json`, and there are predefined names for accessing things like the function logger and cancellation tokens.</span></span>

<span data-ttu-id="5d241-111">이 문서에서는 [Azure Functions 개발자 참조](functions-reference.md)를 이미 읽었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-111">This article assumes that you've already read the [Azure Functions developer reference](functions-reference.md).</span></span>

<span data-ttu-id="5d241-112">C# 클래스 라이브러리 사용에 대한 자세한 내용은 [Azure Functions에서 .NET 클래스 라이브러리 사용](functions-dotnet-class-library.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5d241-112">For information on using C# class libraries, see [Using .NET class libraries with Azure Functions](functions-dotnet-class-library.md).</span></span>

## <a name="how-csx-works"></a><span data-ttu-id="5d241-113">.csx의 작동 원리</span><span class="sxs-lookup"><span data-stu-id="5d241-113">How .csx works</span></span>
<span data-ttu-id="5d241-114">`.csx` 서식을 사용하면 "상용구"를 덜 작성하고 C# 함수를 작성하는 데 집중할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-114">The `.csx` format allows you to write less "boilerplate" and focus on writing just a C# function.</span></span> <span data-ttu-id="5d241-115">일반적으로 파일의 시작 부분에 모든 어셈블리 참조 및 네임스페이스를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-115">Include any assembly references and namespaces at the beginning of the file as usual.</span></span> <span data-ttu-id="5d241-116">네임스페이스 및 클래스의 모든 항목을 래핑하는 대신 `Run` 메서드만 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-116">Instead of wrapping everything in a namespace and class, just define a `Run` method.</span></span> <span data-ttu-id="5d241-117">모든 클래스를 포함해야 하는 경우 예를 들어 POCO(Plain Old CLR Object) 개체를 정의하려면 동일한 파일 내에 클래스를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-117">If you need to include any classes, for instance to define Plain Old CLR Object (POCO) objects, you can include a class inside the same file.</span></span>   

## <a name="binding-to-arguments"></a><span data-ttu-id="5d241-118">인수에 바인딩</span><span class="sxs-lookup"><span data-stu-id="5d241-118">Binding to arguments</span></span>
<span data-ttu-id="5d241-119">다양한 바인딩은 *function.json* 구성의 `name` 속성을 통해 C# 함수에 바인딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-119">The various bindings are bound to a C# function via the `name` property in the *function.json* configuration.</span></span> <span data-ttu-id="5d241-120">각 바인딩에는 지원되는 고유한 형식이 있습니다. 예를 들어 Blob 트리거는 문자열, POCO 또는 CloudBlockBlob을 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-120">Each binding has its own supported types; for instance, a blob trigger can support a string, a POCO, or a CloudBlockBlob.</span></span> <span data-ttu-id="5d241-121">지원되는 형식은 각 바인딩에 대한 참조에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-121">The supported types are documented in the reference for each binding.</span></span> <span data-ttu-id="5d241-122">POCO 개체는 각 속성에 대해 정의된 Getter 및 setter가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-122">A POCO object must have a getter and setter defined for each property.</span></span>

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

## <a name="using-method-return-value-for-output-binding"></a><span data-ttu-id="5d241-123">출력 바인딩에 메서드 반환 값 사용</span><span class="sxs-lookup"><span data-stu-id="5d241-123">Using method return value for output binding</span></span>

<span data-ttu-id="5d241-124">*function.json*에서 이름 `$return`을 사용하여 출력 바인딩에 메서드 반환 값을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-124">You can use a method return value for an output binding, by using the name `$return` in *function.json*:</span></span>

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

## <a name="writing-multiple-output-values"></a><span data-ttu-id="5d241-125">여러 출력 값 쓰기</span><span class="sxs-lookup"><span data-stu-id="5d241-125">Writing multiple output values</span></span>

<span data-ttu-id="5d241-126">출력 바인딩에 여러 값을 쓰려면 [`ICollector`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) 또는 [`IAsyncCollector`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) 형식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-126">To write multiple values to an output binding, use the [`ICollector`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) or [`IAsyncCollector`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) types.</span></span> <span data-ttu-id="5d241-127">이러한 형식은 메서드가 완료될 때 출력 바인딩에 기록되는 쓰기 전용 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-127">These types are write-only collections that are written to the output binding when the method completes.</span></span>

<span data-ttu-id="5d241-128">이 예에서는 `ICollector`를 사용하여 여러 큐 메시지를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-128">This example writes multiple queue messages using `ICollector`:</span></span>

```csharp
public static void Run(ICollector<string> myQueueItem, TraceWriter log)
{
    myQueueItem.Add("Hello");
    myQueueItem.Add("World!");
}
```

## <a name="logging"></a><span data-ttu-id="5d241-129">로깅</span><span class="sxs-lookup"><span data-stu-id="5d241-129">Logging</span></span>
<span data-ttu-id="5d241-130">C#의 스트리밍 로그에 대한 출력을 기록하려면 `TraceWriter` 형식의 인수를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-130">To log output to your streaming logs in C#, include an argument of type `TraceWriter`.</span></span> <span data-ttu-id="5d241-131">이름을 `log`로 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-131">We recommend that you name it `log`.</span></span> <span data-ttu-id="5d241-132">Azure Functions에서 `Console.Write`를 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="5d241-132">Avoid using `Console.Write` in Azure Functions.</span></span> 

<span data-ttu-id="5d241-133">`TraceWriter`는 [Azure WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/TraceWriter.cs)에 정의되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-133">`TraceWriter` is defined in the [Azure WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/TraceWriter.cs).</span></span> <span data-ttu-id="5d241-134">`TraceWriter`에 대한 로그 수준은 [host\.json]에서 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-134">The log level for `TraceWriter` can be configured in [host\.json].</span></span>

```csharp
public static void Run(string myBlob, TraceWriter log)
{
    log.Info($"C# Blob trigger function processed: {myBlob}");
}
```

## <a name="async"></a><span data-ttu-id="5d241-135">Async</span><span class="sxs-lookup"><span data-stu-id="5d241-135">Async</span></span>
<span data-ttu-id="5d241-136">비동기화 함수를 만들려면 `async` 키워드를 사용하고 `Task` 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-136">To make a function asynchronous, use the `async` keyword and return a `Task` object.</span></span>

```csharp
public async static Task ProcessQueueMessageAsync(
        string blobName,
        Stream blobInput,
        Stream blobOutput)
{
    await blobInput.CopyToAsync(blobOutput, 4096, token);
}
```

## <a name="cancellation-token"></a><span data-ttu-id="5d241-137">취소 토큰</span><span class="sxs-lookup"><span data-stu-id="5d241-137">Cancellation Token</span></span>
<span data-ttu-id="5d241-138">일부 작업에는 정상 종료가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-138">Some operations require graceful shutdown.</span></span> <span data-ttu-id="5d241-139">충돌을 처리할 수 있는 코드를 작성하는 데 가장 좋은 방법이지만 정상 종료 요청을 처리하려는 경우 [`CancellationToken`](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) 형식의 인수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-139">While it's always best to write code that can handle crashing,  in cases where you want to handle graceful shutdown requests, you define a [`CancellationToken`](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) typed argument.</span></span>  <span data-ttu-id="5d241-140">`CancellationToken`은 호스트 종료가 트리거되는 신호에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-140">A `CancellationToken` is provided to signal that a host shutdown is triggered.</span></span>

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

## <a name="importing-namespaces"></a><span data-ttu-id="5d241-141">네임스페이스 가져오기</span><span class="sxs-lookup"><span data-stu-id="5d241-141">Importing namespaces</span></span>
<span data-ttu-id="5d241-142">네임스페이스를 가져와야 하는 경우 `using` 절과 함께 정상적으로 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-142">If you need to import namespaces, you can do so as usual, with the `using` clause.</span></span>

```csharp
using System.Net;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

<span data-ttu-id="5d241-143">다음 네임스페이스를 자동으로 가져오므로 다음은 선택적입니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-143">The following namespaces are automatically imported and are therefore optional:</span></span>

* `System`
* `System.Collections.Generic`
* `System.IO`
* `System.Linq`
* `System.Net.Http`
* `System.Threading.Tasks`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`

## <a name="referencing-external-assemblies"></a><span data-ttu-id="5d241-144">외부 어셈블리 참조</span><span class="sxs-lookup"><span data-stu-id="5d241-144">Referencing External Assemblies</span></span>
<span data-ttu-id="5d241-145">프레임워크 어셈블리의 경우 `#r "AssemblyName"` 지시문을 사용하여 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-145">For framework assemblies, add references by using the `#r "AssemblyName"` directive.</span></span>

```csharp
#r "System.Web.Http"

using System.Net;
using System.Net.Http;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

<span data-ttu-id="5d241-146">다음 어셈블리는 Azure Functions 호스팅 환경에 의해 자동으로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-146">The following assemblies are automatically added by the Azure Functions hosting environment:</span></span>

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

<span data-ttu-id="5d241-147">다음 어셈블리는 단순한 이름(예: `#r "AssemblyName"`)으로 참조될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-147">The following assemblies may be referenced by simple-name (for example, `#r "AssemblyName"`):</span></span>

* `Newtonsoft.Json`
* `Microsoft.WindowsAzure.Storage`
* `Microsoft.ServiceBus`
* `Microsoft.AspNet.WebHooks.Receivers`
* `Microsoft.AspNet.WebHooks.Common`
* `Microsoft.Azure.NotificationHubs`

## <a name="referencing-custom-assemblies"></a><span data-ttu-id="5d241-148">사용자 지정 어셈블리 참조</span><span class="sxs-lookup"><span data-stu-id="5d241-148">Referencing custom assemblies</span></span>

<span data-ttu-id="5d241-149">사용자 지정 어셈블리를 참조하려면 *공유* 어셈블리 또는 *전용* 어셈블리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-149">To reference a custom assembly, you can use either a *shared* assembly or a *private* assembly:</span></span>
- <span data-ttu-id="5d241-150">공유 어셈블리는 함수 앱 내의 모든 함수에서 공유됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-150">Shared assemblies are shared across all functions within a function app.</span></span> <span data-ttu-id="5d241-151">사용자 지정 어셈블리를 참조하려면 해당 어셈블리를 함수 앱(예: 함수 앱 루트의 `bin` 폴더)에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-151">To reference a custom assembly, upload the assembly to your function app, such as in a `bin` folder in the function app root.</span></span> 
- <span data-ttu-id="5d241-152">전용 어셈블리는 지정된 함수 컨텍스트의 일부이며 여러 버전의 테스트용 로드를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-152">Private assemblies are part of a given function's context, and support side-loading of different versions.</span></span> <span data-ttu-id="5d241-153">전용 어셈블리는 함수 디렉터리의 `bin` 폴더에 업로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-153">Private assemblies should be uploaded in a `bin` folder in the function directory.</span></span> <span data-ttu-id="5d241-154">파일 이름을 사용하여 참조합니다(예: `#r "MyAssembly.dll"`).</span><span class="sxs-lookup"><span data-stu-id="5d241-154">Reference using the file name, such as  `#r "MyAssembly.dll"`.</span></span> 

<span data-ttu-id="5d241-155">함수 폴더에 파일을 업로드하는 방법에 대한 내용은 패키지 관리에 대한 다음 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5d241-155">For information on how to upload files to your function folder, see the following section on package management.</span></span>

### <a name="watched-directories"></a><span data-ttu-id="5d241-156">감시 디렉터리</span><span class="sxs-lookup"><span data-stu-id="5d241-156">Watched directories</span></span>

<span data-ttu-id="5d241-157">함수 스크립트 파일을 포함하는 디렉터리는 어셈블리 변경 내용이 자동으로 감시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-157">The directory that contains the function script file is automatically watched for changes to assemblies.</span></span> <span data-ttu-id="5d241-158">다른 디렉터리의 어셈블리 변경 내용을 감시하려면 [host\.json]의 `watchDirectories` 목록에 해당 디렉터리를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-158">To watch for assembly changes in other directories, add them to the `watchDirectories` list in [host\.json].</span></span>

## <a name="using-nuget-packages"></a><span data-ttu-id="5d241-159">NuGet 패키지 사용</span><span class="sxs-lookup"><span data-stu-id="5d241-159">Using NuGet packages</span></span>
<span data-ttu-id="5d241-160">C# 함수에서 NuGet 패키지를 사용하려면 *project.json* 파일을 함수 앱의 파일 시스템에 있는 함수의 폴더에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-160">To use NuGet packages in a C# function, upload a *project.json* file to the function's folder in the function app's file system.</span></span> <span data-ttu-id="5d241-161">다음은 Microsoft.ProjectOxford.Face 버전 1.1.0에 참조를 추가하는 예제 *project.json* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-161">Here is an example *project.json* file that adds a reference to Microsoft.ProjectOxford.Face version 1.1.0:</span></span>

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

<span data-ttu-id="5d241-162">.NET Framework 4.6만 지원되므로 *project.json* 파일이 다음과 같이 `net46`을 지정하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-162">Only the .NET Framework 4.6 is supported, so make sure that your *project.json* file specifies `net46` as shown here.</span></span>

<span data-ttu-id="5d241-163">*project.json* 파일을 업로드하는 경우 런타임은 패키지를 가져오고 패키지 어셈블리에 참조를 자동으로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-163">When you upload a *project.json* file, the runtime gets the packages and automatically adds references to the package assemblies.</span></span> <span data-ttu-id="5d241-164">`#r "AssemblyName"` 지시문을 추가할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-164">You don't need to add `#r "AssemblyName"` directives.</span></span> <span data-ttu-id="5d241-165">NuGet 패키지에 정의된 형식을 사용하려면 필요한 `using` 문을 *run.csx* 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-165">To use the types defined in the NuGet packages, add the required `using` statements to your *run.csx* file</span></span> 

<span data-ttu-id="5d241-166">함수 런타임에서 NuGet 복원은 `project.json` 및 `project.lock.json`를 비교하여 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-166">In the Functions runtime, NuGet restore works by comparing `project.json` and `project.lock.json`.</span></span> <span data-ttu-id="5d241-167">파일의 날짜와 타임스탬프가 일치하지 **않으면** NuGet에서는 복원을 실행하고 업데이트된 패키지를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-167">If the date and time stamps of the files **do not** match, a NuGet restore runs and NuGet downloads updated packages.</span></span> <span data-ttu-id="5d241-168">그러나 파일의 날짜 및 타임스탬프가 **일치하는** 경우 NuGet은 복원을 수행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-168">However, if the date and time stamps of the files **do** match, NuGet does not perform a restore.</span></span> <span data-ttu-id="5d241-169">따라서 `project.lock.json`을 배포하면 NuGet이 패키지 복원을 건너뛰므로 배포해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-169">Therefore, `project.lock.json` should not be deployed as it causes NuGet to skip package restore.</span></span> <span data-ttu-id="5d241-170">잠금 파일의 배포를 방지하려면 `project.lock.json`을 `.gitignore` 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-170">To avoid deploying the lock file, add the `project.lock.json` to the `.gitignore` file.</span></span>

<span data-ttu-id="5d241-171">사용자 지정 NuGet 피드를 사용하려면 함수 앱 루트의 *Nuget.Config* 파일에서 피드를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-171">To use a custom NuGet feed, specify the feed in a *Nuget.Config* file in the Function App root.</span></span> <span data-ttu-id="5d241-172">자세한 내용은 참조 [NuGet 동작 구성](/nuget/consume-packages/configuring-nuget-behavior)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5d241-172">For more information, see [Configuring NuGet behavior](/nuget/consume-packages/configuring-nuget-behavior).</span></span>

### <a name="using-a-projectjson-file"></a><span data-ttu-id="5d241-173">project.json 파일 사용</span><span class="sxs-lookup"><span data-stu-id="5d241-173">Using a project.json file</span></span>
1. <span data-ttu-id="5d241-174">Azure Portal에서 함수를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-174">Open the function in the Azure portal.</span></span> <span data-ttu-id="5d241-175">로그 탭에 패키지 설치 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-175">The logs tab displays the package installation output.</span></span>
2. <span data-ttu-id="5d241-176">project.json 파일을 업로드하려면 Azure Functions 개발자 참조 토픽의 [함수 앱 파일을 업데이트하는 방법](functions-reference.md#fileupdate)에 설명되어 있는 방법 중 하나를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-176">To upload a project.json file, use one of the methods described in the [How to update function app files](functions-reference.md#fileupdate) in the Azure Functions developer reference topic.</span></span>
3. <span data-ttu-id="5d241-177">*project.json* 파일을 업로드하면 함수의 스트리밍 로그에 다음 예제와 같은 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-177">After the *project.json* file is uploaded, you see output like the following example in your function's streaming log:</span></span>

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

## <a name="environment-variables"></a><span data-ttu-id="5d241-178">환경 변수</span><span class="sxs-lookup"><span data-stu-id="5d241-178">Environment variables</span></span>
<span data-ttu-id="5d241-179">환경 변수 또는 앱 설정 값을 가져오려면 다음 코드 예제와 같이 `System.Environment.GetEnvironmentVariable`을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-179">To get an environment variable or an app setting value, use `System.Environment.GetEnvironmentVariable`, as shown in the following code example:</span></span>

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

## <a name="reusing-csx-code"></a><span data-ttu-id="5d241-180">.csx 코드 재사용</span><span class="sxs-lookup"><span data-stu-id="5d241-180">Reusing .csx code</span></span>
<span data-ttu-id="5d241-181">*run.csx* 파일에 있는 다른 *.csx* 파일에 정의된 클래스와 메서드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-181">You can use classes and methods defined in other *.csx* files in your *run.csx* file.</span></span> <span data-ttu-id="5d241-182">이를 위해 *run.csx* 파일의 `#load` 지시문을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-182">To do that, use `#load` directives in your *run.csx* file.</span></span> <span data-ttu-id="5d241-183">다음 예제에서는 `MyLogger`이라는 이름의 로깅 루틴이 *myLogger.csx*에서 공유되고 `#load` 지시문을 사용하여 *run.csx*로 로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-183">In the following example, a logging routine named `MyLogger` is shared in *myLogger.csx* and loaded into *run.csx* using the `#load` directive:</span></span>

<span data-ttu-id="5d241-184">예제 *run.csx*:</span><span class="sxs-lookup"><span data-stu-id="5d241-184">Example *run.csx*:</span></span>

```csharp
#load "mylogger.csx"

public static void Run(TimerInfo myTimer, TraceWriter log)
{
    log.Verbose($"Log by run.csx: {DateTime.Now}");
    MyLogger(log, $"Log by MyLogger: {DateTime.Now}");
}
```

<span data-ttu-id="5d241-185">예제 *mylogger.csx*:</span><span class="sxs-lookup"><span data-stu-id="5d241-185">Example *mylogger.csx*:</span></span>

```csharp
public static void MyLogger(TraceWriter log, string logtext)
{
    log.Verbose(logtext);
}
```

<span data-ttu-id="5d241-186">공유된 *.csx*를 사용하는 것은 POCO 개체를 사용하는 함수 간 인수를 강력한 형식으로 만들려는 경우에 일반적인 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-186">Using a shared *.csx* is a common pattern when you want to strongly type your arguments between functions using a POCO object.</span></span> <span data-ttu-id="5d241-187">다음 간단한 예제에서는 HTTP 트리거 및 큐 트리거는 `Order`라는 이름의 POCO 개체를 공유하여 주문 데이터를 강력한 형식으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-187">In the following simplified example, an HTTP trigger and queue trigger share a POCO object named `Order` to strongly type the order data:</span></span>

<span data-ttu-id="5d241-188">HTTP 트리거를 위한 *run.csx* 예제:</span><span class="sxs-lookup"><span data-stu-id="5d241-188">Example *run.csx* for HTTP trigger:</span></span>

```cs
#load "..\shared\order.csx"

using System.Net;

public static async Task<HttpResponseMessage> Run(Order req, IAsyncCollector<Order> outputQueueItem, TraceWriter log)
{
    log.Info("C# HTTP trigger function received an order.");
    log.Info(req.ToString());
    log.Info("Submitting to processing queue.");

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

<span data-ttu-id="5d241-189">큐 트리거를 위한 *run.csx* 예제:</span><span class="sxs-lookup"><span data-stu-id="5d241-189">Example *run.csx* for queue trigger:</span></span>

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

<span data-ttu-id="5d241-190">*order.csx* 예제:</span><span class="sxs-lookup"><span data-stu-id="5d241-190">Example *order.csx*:</span></span>

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

<span data-ttu-id="5d241-191">`#load` 지시문으로 상대 경로를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-191">You can use a relative path with the `#load` directive:</span></span>

* <span data-ttu-id="5d241-192">`#load "mylogger.csx"` 는 함수 폴더에 있는 파일을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-192">`#load "mylogger.csx"` loads a file located in the function folder.</span></span>
* <span data-ttu-id="5d241-193">`#load "loadedfiles\mylogger.csx"` 는 함수 폴더의 폴더에 있는 파일을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-193">`#load "loadedfiles\mylogger.csx"` loads a file located in a folder in the function folder.</span></span>
* <span data-ttu-id="5d241-194">`#load "..\shared\mylogger.csx"` 는 함수 폴더와 동일한 수준의 폴더 즉, *wwwroot*에 있는 파일을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-194">`#load "..\shared\mylogger.csx"` loads a file located in a folder at the same level as the function folder, that is, directly under *wwwroot*.</span></span>

<span data-ttu-id="5d241-195">`#load` 지시문은 *.cs* 파일이 아닌 *.csx*(C# 스크립트) 파일에서만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-195">The `#load` directive works only with *.csx* (C# script) files, not with *.cs* files.</span></span>

<a name="imperative-bindings"></a> 

## <a name="binding-at-runtime-via-imperative-bindings"></a><span data-ttu-id="5d241-196">명령적 바인딩을 통해 런타임에 바인딩</span><span class="sxs-lookup"><span data-stu-id="5d241-196">Binding at runtime via imperative bindings</span></span>

<span data-ttu-id="5d241-197">C# 및 기타 .NET 언어에서는 *function.json*의 [*declarative*](https://en.wikipedia.org/wiki/Declarative_programming) 바인딩과 달리 [명령적](https://en.wikipedia.org/wiki/Imperative_programming) 바인딩 패턴을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-197">In C# and other .NET languages, you can use an [imperative](https://en.wikipedia.org/wiki/Imperative_programming) binding pattern, as opposed to the [*declarative*](https://en.wikipedia.org/wiki/Declarative_programming) bindings in *function.json*.</span></span> <span data-ttu-id="5d241-198">명령적 바인딩은 바인딩 매개 변수를 디자인 타임이 아닌 런타임에 계산해야 할 경우 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-198">Imperative binding is useful when binding parameters need to be computed at runtime rather than design time.</span></span> <span data-ttu-id="5d241-199">이 패턴을 사용하면 함수 코드에서 지원되는 입력 및 출력 바인딩을 즉시 바인딩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-199">With this pattern, you can bind to supported input and output binding on-the-fly in your function code.</span></span>

<span data-ttu-id="5d241-200">다음과 같이 명령적 바인딩을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-200">Define an imperative binding as follows:</span></span>

- <span data-ttu-id="5d241-201">원하는 명령적 바인딩에 대한 *function.json*에 항목을 포함하지 **마세요**.</span><span class="sxs-lookup"><span data-stu-id="5d241-201">**Do not** include an entry in *function.json* for your desired imperative bindings.</span></span>
- <span data-ttu-id="5d241-202">입력 매개 변수 [`Binder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/Bindings/Runtime/Binder.cs) 또는 [`IBinder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IBinder.cs)에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-202">Pass in an input parameter [`Binder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/Bindings/Runtime/Binder.cs) or [`IBinder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IBinder.cs).</span></span>
- <span data-ttu-id="5d241-203">다음 C# 패턴을 사용하여 데이터 바인딩을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-203">Use the following C# pattern to perform the data binding.</span></span>

```cs
using (var output = await binder.BindAsync<T>(new BindingTypeAttribute(...)))
{
    ...
}
```

<span data-ttu-id="5d241-204">여기서 `BindingTypeAttribute`는 바인딩을 정의하는 .NET 특성이며, `T`는 해당 바인딩 형식에서 지원되는 입력 또는 출력 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-204">where `BindingTypeAttribute` is the .NET attribute that defines your binding and `T` is the input or output type that's supported by that binding type.</span></span> <span data-ttu-id="5d241-205">또한 `T`는 `out` 매개 변수 형식(예: `out JObject`)일 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-205">`T` also cannot be an `out` parameter type (such as `out JObject`).</span></span> <span data-ttu-id="5d241-206">예를 들어, Mobile Apps 테이블 출력 바인딩은 [6가지 출력 형식](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22)을 지원하지만 `T`에는 [ICollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) 또는 [IAsyncCollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs)만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-206">For example, the Mobile Apps table output binding supports [six output types](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22), but you can only use [ICollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) or [IAsyncCollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) for `T`.</span></span>

<span data-ttu-id="5d241-207">다음 예제 코드에서는 런타임에서 정의된 Blob경로를 사용하는 [Storage Blob 출력 바인딩](functions-bindings-storage-blob.md#using-a-blob-output-binding)을 만든 다음, Blob에 문자열을 씁니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-207">The following example code creates a [Storage blob output binding](functions-bindings-storage-blob.md#using-a-blob-output-binding) with blob path that's defined at run time, then writes a string to the blob.</span></span>

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

<span data-ttu-id="5d241-208">[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs)는 [Storage Blob](functions-bindings-storage-blob.md) 입력 또는 출력 바인딩을 정의하며, [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx)는 지원되는 출력 바인딩 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-208">[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs) defines the [Storage blob](functions-bindings-storage-blob.md) input or output binding, and [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) is a supported output binding type.</span></span>
<span data-ttu-id="5d241-209">코드는 저장소 계정 연결 문자열(즉 `AzureWebJobsStorage`)에 대한 기본 앱 설정을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-209">As is, the code gets the default app setting for the Storage account connection string (which is `AzureWebJobsStorage`).</span></span> <span data-ttu-id="5d241-210">[StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)를 추가하고 `BindAsync<T>()`에 특성 배열을 전달하여 사용할 사용자 지정 앱 설정을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-210">You can specify a custom app setting to use by adding the [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) and passing the attribute array into `BindAsync<T>()`.</span></span> <span data-ttu-id="5d241-211">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-211">For example,</span></span>

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

<span data-ttu-id="5d241-212">다음 표에는 각 바인딩 유형의 .NET 특성과 해당 특성이 정의된 패키지가 나열되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d241-212">The following table lists the .NET attributes for each binding type and the packages in which they are defined.</span></span>

> [!div class="mx-codeBreakAll"]
| <span data-ttu-id="5d241-213">바인딩</span><span class="sxs-lookup"><span data-stu-id="5d241-213">Binding</span></span> | <span data-ttu-id="5d241-214">특성</span><span class="sxs-lookup"><span data-stu-id="5d241-214">Attribute</span></span> | <span data-ttu-id="5d241-215">추가 참조</span><span class="sxs-lookup"><span data-stu-id="5d241-215">Add reference</span></span> |
|------|------|------|
| <span data-ttu-id="5d241-216">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="5d241-216">Cosmos DB</span></span> | [`Microsoft.Azure.WebJobs.DocumentDBAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.DocumentDB"` |
| <span data-ttu-id="5d241-217">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="5d241-217">Event Hubs</span></span> | <span data-ttu-id="5d241-218">[`Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="5d241-218">[`Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span></span> | `#r "Microsoft.Azure.Jobs.ServiceBus"` |
| <span data-ttu-id="5d241-219">Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="5d241-219">Mobile Apps</span></span> | [`Microsoft.Azure.WebJobs.MobileTableAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.MobileApps"` |
| <span data-ttu-id="5d241-220">Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="5d241-220">Notification Hubs</span></span> | [`Microsoft.Azure.WebJobs.NotificationHubAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.NotificationHubs/NotificationHubAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.NotificationHubs"` |
| <span data-ttu-id="5d241-221">Service Bus</span><span class="sxs-lookup"><span data-stu-id="5d241-221">Service Bus</span></span> | <span data-ttu-id="5d241-222">[`Microsoft.Azure.WebJobs.ServiceBusAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="5d241-222">[`Microsoft.Azure.WebJobs.ServiceBusAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span></span> | `#r "Microsoft.Azure.WebJobs.ServiceBus"` |
| <span data-ttu-id="5d241-223">Storage 큐</span><span class="sxs-lookup"><span data-stu-id="5d241-223">Storage queue</span></span> | <span data-ttu-id="5d241-224">[`Microsoft.Azure.WebJobs.QueueAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="5d241-224">[`Microsoft.Azure.WebJobs.QueueAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span></span> | |
| <span data-ttu-id="5d241-225">Storage Blob</span><span class="sxs-lookup"><span data-stu-id="5d241-225">Storage blob</span></span> | <span data-ttu-id="5d241-226">[`Microsoft.Azure.WebJobs.BlobAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="5d241-226">[`Microsoft.Azure.WebJobs.BlobAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span></span> | |
| <span data-ttu-id="5d241-227">Storage 테이블</span><span class="sxs-lookup"><span data-stu-id="5d241-227">Storage table</span></span> | <span data-ttu-id="5d241-228">[`Microsoft.Azure.WebJobs.TableAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="5d241-228">[`Microsoft.Azure.WebJobs.TableAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span></span> | |
| <span data-ttu-id="5d241-229">Twilio</span><span class="sxs-lookup"><span data-stu-id="5d241-229">Twilio</span></span> | [`Microsoft.Azure.WebJobs.TwilioSmsAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.Twilio/TwilioSMSAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.Twilio"` |



## <a name="next-steps"></a><span data-ttu-id="5d241-230">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5d241-230">Next steps</span></span>
<span data-ttu-id="5d241-231">자세한 내용은 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5d241-231">For more information, see the following resources:</span></span>

* [<span data-ttu-id="5d241-232">Azure Functions에 대한 모범 사례</span><span class="sxs-lookup"><span data-stu-id="5d241-232">Best Practices for Azure Functions</span></span>](functions-best-practices.md)
* [<span data-ttu-id="5d241-233">Azure Functions 개발자 참조</span><span class="sxs-lookup"><span data-stu-id="5d241-233">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="5d241-234">Azure Functions F# 개발자 참조</span><span class="sxs-lookup"><span data-stu-id="5d241-234">Azure Functions F# developer reference</span></span>](functions-reference-fsharp.md)
* [<span data-ttu-id="5d241-235">Azure Functions NodeJS 개발자 참조</span><span class="sxs-lookup"><span data-stu-id="5d241-235">Azure Functions NodeJS developer reference</span></span>](functions-reference-node.md)
* [<span data-ttu-id="5d241-236">Azure Functions 트리거 및 바인딩</span><span class="sxs-lookup"><span data-stu-id="5d241-236">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)

[host\.json]: https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json

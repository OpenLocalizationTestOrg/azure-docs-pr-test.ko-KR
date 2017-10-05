---
title: "Azure Functions F# 개발자 참조 | Microsoft Docs"
description: "F#을 사용하여 Azure Functions를 개발하는 방법을 알아봅니다."
services: functions
documentationcenter: fsharp
author: sylvanc
manager: jbronsk
editor: 
tags: 
keywords: "azure 함수, 함수, 처리, webhook, 동적 계산, 서버가 없는 아키텍처, F # 이벤트"
ms.assetid: e60226e5-2630-41d7-9e5b-9f9e5acc8e50
ms.service: functions
ms.devlang: fsharp
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 09/09/2016
ms.author: syclebsc
ms.openlocfilehash: 1691d378263f6b4ce5072f5c621d8db02f774b5f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-f-developer-reference"></a><span data-ttu-id="59b81-104">Azure Functions F# 개발자 참조</span><span class="sxs-lookup"><span data-stu-id="59b81-104">Azure Functions F# Developer Reference</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="59b81-105">C# 스크립트</span><span class="sxs-lookup"><span data-stu-id="59b81-105">C# script</span></span>](functions-reference-csharp.md)
> * [<span data-ttu-id="59b81-106">F# 스크립트</span><span class="sxs-lookup"><span data-stu-id="59b81-106">F# script</span></span>](functions-reference-fsharp.md)
> * [<span data-ttu-id="59b81-107">Node.JS</span><span class="sxs-lookup"><span data-stu-id="59b81-107">Node.js</span></span>](functions-reference-node.md)
> 
> 

<span data-ttu-id="59b81-108">Azure Functions용 F#란 클라우드에서 작은 코드 또는 "함수"를 쉽게 실행하기 위한 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="59b81-108">F# for Azure Functions is a solution for easily running small pieces of code, or "functions," in the cloud.</span></span> <span data-ttu-id="59b81-109">데이터는 함수 인수를 통해 F# 함수로 흐릅니다.</span><span class="sxs-lookup"><span data-stu-id="59b81-109">Data flows into your F# function via function arguments.</span></span> <span data-ttu-id="59b81-110">인수 이름은 `function.json`에 지정되며 함수 로거 및 취소 토큰 같은 항목에 액세스하기 위해 미리 정의된 이름이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59b81-110">Argument names are specified in `function.json`, and there are predefined names for accessing things like the function logger and cancellation tokens.</span></span>

<span data-ttu-id="59b81-111">이 문서에서는 [Azure Functions 개발자 참조](functions-reference.md)를 이미 읽었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="59b81-111">This article assumes that you've already read the [Azure Functions developer reference](functions-reference.md).</span></span>

## <a name="how-fsx-works"></a><span data-ttu-id="59b81-112">.fsx의 작동 방식</span><span class="sxs-lookup"><span data-stu-id="59b81-112">How .fsx works</span></span>
<span data-ttu-id="59b81-113">`.fsx` 파일은 F# 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="59b81-113">An `.fsx` file is an F# script.</span></span> <span data-ttu-id="59b81-114">단일 파일에 포함된 F# 프로젝트로 생각할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59b81-114">It can be thought of as an F# project that's contained in a single file.</span></span> <span data-ttu-id="59b81-115">파일은 프로그램(이 경우 Azure Function)에 대한 코드 및 종속성 관리를 위한 지시문을 모두 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="59b81-115">The file contains both the code for your program (in this case, your Azure Function) and directives for managing dependencies.</span></span>

<span data-ttu-id="59b81-116">Azure Function에 `.fsx` 를 사용하는 경우 "상용구" 코드 대신 함수에 집중할 수 있도록 자주 필요한 어셈블리가 자동으로 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="59b81-116">When you use an `.fsx` for an Azure Function, commonly required assemblies are automatically included for you, allowing you to focus on the function rather than "boilerplate" code.</span></span>

## <a name="binding-to-arguments"></a><span data-ttu-id="59b81-117">인수에 바인딩</span><span class="sxs-lookup"><span data-stu-id="59b81-117">Binding to arguments</span></span>
<span data-ttu-id="59b81-118">각 바인딩은 [Azure Functions 트리거 및 바인딩 개발자 참조](functions-triggers-bindings.md)에 설명된 대로 일부 인수 집합을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="59b81-118">Each binding supports some set of arguments, as detailed in the [Azure Functions triggers and bindings developer reference](functions-triggers-bindings.md).</span></span> <span data-ttu-id="59b81-119">예를 들어 Blob 트리거가 지원하는 인수 바인딩 중 하나는 F# 레코드를 사용하여 표현될 수 있는 POCO입니다.</span><span class="sxs-lookup"><span data-stu-id="59b81-119">For example, one of the argument bindings a blob trigger supports is a POCO, which can be expressed using an F# record.</span></span> <span data-ttu-id="59b81-120">예:</span><span class="sxs-lookup"><span data-stu-id="59b81-120">For example:</span></span>

```fsharp
type Item = { Id: string }

let Run(blob: string, output: byref<Item>) =
    let item = { Id = "Some ID" }
    output <- item
```

<span data-ttu-id="59b81-121">이 F# Azure Function에서는 하나 이상의 인수를 사용하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="59b81-121">Your F# Azure Function will take one or more arguments.</span></span> <span data-ttu-id="59b81-122">Azure Functions 인수에 대해 이야기할 때 *입력* 인수 및 *출력* 인수를 언급합니다.</span><span class="sxs-lookup"><span data-stu-id="59b81-122">When we talk about Azure Functions arguments, we refer to *input* arguments and *output* arguments.</span></span> <span data-ttu-id="59b81-123">입력 인수란 표현 그대로 F# Azure Function에 입력하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="59b81-123">An input argument is exactly what it sounds like: input to your F# Azure Function.</span></span> <span data-ttu-id="59b81-124">*출력* 인수란 함수에서 데이터를 *출력*하여 다시 전달하는 방식으로 사용되는 변경 가능한 데이터 또는 `byref<>` 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="59b81-124">An *output* argument is mutable data or a `byref<>` argument that serves as a way to pass data back *out* of your function.</span></span>

<span data-ttu-id="59b81-125">위의 예에서 `blob`은 입력 인수이며 `output`은 출력 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="59b81-125">In the example above, `blob` is an input argument, and `output` is an output argument.</span></span> <span data-ttu-id="59b81-126">여기서는 `output`에 `byref<>`를 사용합니다(`[<Out>]` 주석을 추가할 필요 없음).</span><span class="sxs-lookup"><span data-stu-id="59b81-126">Notice that we used `byref<>` for `output` (there's no need to add the `[<Out>]` annotation).</span></span> <span data-ttu-id="59b81-127">`byref<>` 형식을 사용하면 인수가 참조하는 레코드 또는 개체를 함수를 통해 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59b81-127">Using a `byref<>` type allows your function to change which record or object the argument refers to.</span></span>

<span data-ttu-id="59b81-128">F# 레코드를 입력 형식으로 사용한 경우, Azure Functions 프레임워크에서 필드를 적절하게 설정하려면 레코드를 함수로 전달하기 전에 레코드 정의를 `[<CLIMutable>]` 로 표시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59b81-128">When an F# record is used as an input type, the record definition must be marked with `[<CLIMutable>]` in order to allow the Azure Functions framework to set the fields appropriately before passing the record to your function.</span></span> <span data-ttu-id="59b81-129">내부적으로 `[<CLIMutable>]` 은 레코드 속성에 대한 setter를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="59b81-129">Under the hood, `[<CLIMutable>]` generates setters for the record properties.</span></span> <span data-ttu-id="59b81-130">예:</span><span class="sxs-lookup"><span data-stu-id="59b81-130">For example:</span></span>

```fsharp
[<CLIMutable>]
type TestObject =
    { SenderName : string
      Greeting : string }

let Run(req: TestObject, log: TraceWriter) =
    { req with Greeting = sprintf "Hello, %s" req.SenderName }
```

<span data-ttu-id="59b81-131">F# 클래스는 들어오고 나가는 인수 모두에 대해서도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59b81-131">An F# class can also be used for both in and out arguments.</span></span> <span data-ttu-id="59b81-132">클래스의 경우 일반적으로 속성은 getter 및 setter가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="59b81-132">For a class, properties will usually need getters and setters.</span></span> <span data-ttu-id="59b81-133">예:</span><span class="sxs-lookup"><span data-stu-id="59b81-133">For example:</span></span>

```fsharp
type Item() =
    member val Id = "" with get,set
    member val Text = "" with get,set

let Run(input: string, item: byref<Item>) =
    let result = Item(Id = input, Text = "Hello from F#!")
    item <- result
```

## <a name="logging"></a><span data-ttu-id="59b81-134">로깅</span><span class="sxs-lookup"><span data-stu-id="59b81-134">Logging</span></span>
<span data-ttu-id="59b81-135">출력을 F#의 [스트리밍 로그](../app-service-web/web-sites-streaming-logs-and-console.md)에 로그하려면 함수에 `TraceWriter` 형식의 인수를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59b81-135">To log output to your [streaming logs](../app-service-web/web-sites-streaming-logs-and-console.md) in F#, your function should take an argument of type `TraceWriter`.</span></span> <span data-ttu-id="59b81-136">일관성을 위해 이 인수의 이름을 `log`로 지정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="59b81-136">For consistency, we recommend this argument is named `log`.</span></span> <span data-ttu-id="59b81-137">예:</span><span class="sxs-lookup"><span data-stu-id="59b81-137">For example:</span></span>

```fsharp
let Run(blob: string, output: byref<string>, log: TraceWriter) =
    log.Verbose(sprintf "F# Azure Function processed a blob: %s" blob)
    output <- input
```

## <a name="async"></a><span data-ttu-id="59b81-138">Async</span><span class="sxs-lookup"><span data-stu-id="59b81-138">Async</span></span>
<span data-ttu-id="59b81-139">`async` 워크플로를 사용할 수 있지만 결과는 `Task`를 반환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59b81-139">The `async` workflow can be used, but the result needs to return a `Task`.</span></span> <span data-ttu-id="59b81-140">`Async.StartAsTask`를 사용하여 이를 확인할 수 있습니다. 예:</span><span class="sxs-lookup"><span data-stu-id="59b81-140">This can be done with `Async.StartAsTask`, for example:</span></span>

```fsharp
let Run(req: HttpRequestMessage) =
    async {
        return new HttpResponseMessage(HttpStatusCode.OK)
    } |> Async.StartAsTask
```

## <a name="cancellation-token"></a><span data-ttu-id="59b81-141">취소 토큰</span><span class="sxs-lookup"><span data-stu-id="59b81-141">Cancellation Token</span></span>
<span data-ttu-id="59b81-142">함수가 정상적인 종료를 처리해야 하는 경우 [`CancellationToken`](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) 인수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59b81-142">If your function needs to handle shutdown gracefully, you can give it a [`CancellationToken`](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) argument.</span></span> <span data-ttu-id="59b81-143">이는 `async`와 결합할 수 있습니다. 예:</span><span class="sxs-lookup"><span data-stu-id="59b81-143">This can be combined with `async`, for example:</span></span>

```fsharp
let Run(req: HttpRequestMessage, token: CancellationToken)
    let f = async {
        do! Async.Sleep(10)
        return new HttpResponseMessage(HttpStatusCode.OK)
    }
    Async.StartAsTask(f, token)
```

## <a name="importing-namespaces"></a><span data-ttu-id="59b81-144">네임스페이스 가져오기</span><span class="sxs-lookup"><span data-stu-id="59b81-144">Importing namespaces</span></span>
<span data-ttu-id="59b81-145">네임스페이스는 다음과 같은 일반적인 방법으로 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59b81-145">Namespaces can be opened in the usual way:</span></span>

```fsharp
open System.Net
open System.Threading.Tasks

let Run(req: HttpRequestMessage, log: TraceWriter) =
    ...
```

<span data-ttu-id="59b81-146">다음과 같은 네임스페이스는 자동으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="59b81-146">The following namespaces are automatically opened:</span></span>

* `System`
* `System.Collections.Generic`
* `System.IO`
* `System.Linq`
* `System.Net.Http`
* `System.Threading.Tasks`
* `Microsoft.Azure.WebJobs`
* <span data-ttu-id="59b81-147">`Microsoft.Azure.WebJobs.Host`.</span><span class="sxs-lookup"><span data-stu-id="59b81-147">`Microsoft.Azure.WebJobs.Host`.</span></span>

## <a name="referencing-external-assemblies"></a><span data-ttu-id="59b81-148">외부 어셈블리 참조</span><span class="sxs-lookup"><span data-stu-id="59b81-148">Referencing External Assemblies</span></span>
<span data-ttu-id="59b81-149">마찬가지로, 프레임워크 어셈블리 참조에 `#r "AssemblyName"` 지시문이 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="59b81-149">Similarly, framework assembly references be added with the `#r "AssemblyName"` directive.</span></span>

```fsharp
#r "System.Web.Http"

open System.Net
open System.Net.Http
open System.Threading.Tasks

let Run(req: HttpRequestMessage, log: TraceWriter) =
    ...
```

<span data-ttu-id="59b81-150">다음 어셈블리는 Azure Functions 호스팅 환경에 의해 자동으로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="59b81-150">The following assemblies are automatically added by the Azure Functions hosting environment:</span></span>

* <span data-ttu-id="59b81-151">`mscorlib`,</span><span class="sxs-lookup"><span data-stu-id="59b81-151">`mscorlib`,</span></span>
* `System`
* `System.Core`
* `System.Xml`
* `System.Net.Http`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`
* `Microsoft.Azure.WebJobs.Extensions`
* `System.Web.Http`
* <span data-ttu-id="59b81-152">`System.Net.Http.Formatting`.</span><span class="sxs-lookup"><span data-stu-id="59b81-152">`System.Net.Http.Formatting`.</span></span>

<span data-ttu-id="59b81-153">또한 다음 어셈블리는 특수한 경우이며 simplename으로 참조할 수 있습니다(예: `#r "AssemblyName"`).</span><span class="sxs-lookup"><span data-stu-id="59b81-153">In addition, the following assemblies are special cased and may be referenced by simplename (e.g. `#r "AssemblyName"`):</span></span>

* `Newtonsoft.Json`
* `Microsoft.WindowsAzure.Storage`
* `Microsoft.ServiceBus`
* `Microsoft.AspNet.WebHooks.Receivers`
* <span data-ttu-id="59b81-154">`Microsoft.AspNEt.WebHooks.Common`.</span><span class="sxs-lookup"><span data-stu-id="59b81-154">`Microsoft.AspNEt.WebHooks.Common`.</span></span>

<span data-ttu-id="59b81-155">개인 어셈블리를 참조해야 하는 경우 어셈블리 파일을 함수에 상대적인 `bin` 폴더에 업로드하고 파일 이름(예: `#r "MyAssembly.dll"`)을 사용하여 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59b81-155">If you need to reference a private assembly, you can upload the assembly file into a `bin` folder relative to your function and reference it by using the file name (e.g.  `#r "MyAssembly.dll"`).</span></span> <span data-ttu-id="59b81-156">함수 폴더에 파일을 업로드하는 방법에 대한 내용은 패키지 관리에 대한 다음 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59b81-156">For information on how to upload files to your function folder, see the following section on package management.</span></span>

## <a name="editor-prelude"></a><span data-ttu-id="59b81-157">Editor Prelude</span><span class="sxs-lookup"><span data-stu-id="59b81-157">Editor Prelude</span></span>
<span data-ttu-id="59b81-158">F# 컴파일러 서비스를 지원하는 편집기는 Azure Functions에 자동으로 포함되는 네임스페이스 및 어셈블리를 인식하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="59b81-158">An editor that supports F# Compiler Services will not be aware of the namespaces and assemblies that Azure Functions automatically includes.</span></span> <span data-ttu-id="59b81-159">따라서 편집기가 사용 중인 어셈블리를 찾고 네임스페이스를 명시적으로 여는 데 도움이 되는 Prelude를 포함하는 것이 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59b81-159">As such, it can be useful to include a prelude that helps the editor find the assemblies you are using, and to explicitly open namespaces.</span></span> <span data-ttu-id="59b81-160">예:</span><span class="sxs-lookup"><span data-stu-id="59b81-160">For example:</span></span>

```fsharp
#if !COMPILED
#I "../../bin/Binaries/WebJobs.Script.Host"
#r "Microsoft.Azure.WebJobs.Host.dll"
#endif

open Sytem
open Microsoft.Azure.WebJobs.Host

let Run(blob: string, output: byref<string>, log: TraceWriter) =
    ...
```

<span data-ttu-id="59b81-161">Azure Functions에서 코드를 실행하는 경우 `COMPILED` 정의된 소스를 처리하므로 Editor Prelude는 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="59b81-161">When Azure Functions executes your code, it processes the source with `COMPILED` defined, so the editor prelude will be ignored.</span></span>

<a name="package"></a>

## <a name="package-management"></a><span data-ttu-id="59b81-162">패키지 관리</span><span class="sxs-lookup"><span data-stu-id="59b81-162">Package management</span></span>
<span data-ttu-id="59b81-163">F# 함수에서 NuGet 패키지를 사용하려면 `project.json` 파일을 함수 앱의 파일 시스템에 있는 함수의 폴더에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="59b81-163">To use NuGet packages in an F# function, add a `project.json` file to the the function's folder in the function app's file system.</span></span> <span data-ttu-id="59b81-164">다음은 NuGet 패키지 참조를 `Microsoft.ProjectOxford.Face` 버전 1.1.0에 추가하는 예제 `project.json` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="59b81-164">Here is an example `project.json` file that adds a NuGet package reference to `Microsoft.ProjectOxford.Face` version 1.1.0:</span></span>

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

<span data-ttu-id="59b81-165">.NET Framework 4.6만 지원되므로 `project.json` 파일이 다음과 같이 `net46`을 지정하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="59b81-165">Only the .NET Framework 4.6 is supported, so make sure that your `project.json` file specifies `net46` as shown here.</span></span>

<span data-ttu-id="59b81-166">`project.json` 파일을 업로드하는 경우 런타임은 패키지를 가져오고 패키지 어셈블리에 참조를 자동으로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="59b81-166">When you upload a `project.json` file, the runtime gets the packages and automatically adds references to the package assemblies.</span></span> <span data-ttu-id="59b81-167">`#r "AssemblyName"` 지시문을 추가할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="59b81-167">You don't need to add `#r "AssemblyName"` directives.</span></span> <span data-ttu-id="59b81-168">필요한 `open` 문만 `.fsx` 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="59b81-168">Just add the required `open` statements to your `.fsx` file.</span></span>

<span data-ttu-id="59b81-169">편집기와 F# Compile Services의 더 나은 상호 작용을 위해 참조 어셈블리를 Editor Prelude에 자동으로 넣고 싶을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59b81-169">You may wish to put automatically references assemblies in your editor prelude, to improve your editor's interaction with F# Compile Services.</span></span>

### <a name="how-to-add-a-projectjson-file-to-your-azure-function"></a><span data-ttu-id="59b81-170">`project.json` 파일을 Azure Function에 추가하는 방법</span><span class="sxs-lookup"><span data-stu-id="59b81-170">How to add a `project.json` file to your Azure Function</span></span>
1. <span data-ttu-id="59b81-171">함수 앱을 실행하여 시작하며 이는 Azure 포털에서 함수를 열어 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59b81-171">Begin by making sure your function app is running, which you can do by opening your function in the Azure portal.</span></span> <span data-ttu-id="59b81-172">또한 패키지 설치 출력이 표시되는 스트리밍 로그에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59b81-172">This also gives access to the streaming logs where package installation output will be displayed.</span></span>
2. <span data-ttu-id="59b81-173">`project.json` 파일을 업로드하려면 [함수 앱 파일을 업데이트하는 방법](functions-reference.md#fileupdate)에 설명되어 있는 것 중 하나를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="59b81-173">To upload a `project.json` file, use one of the methods described in [how to update function app files](functions-reference.md#fileupdate).</span></span> <span data-ttu-id="59b81-174">[Azure Functions에 대한 연속 배포](functions-continuous-deployment.md)를 사용하는 경우 `project.json` 파일을 배포 분기에 추가하기 전에 시험삼아 스테이징 분기에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59b81-174">If you are using [Continuous Deployment for Azure Functions](functions-continuous-deployment.md), you can add a `project.json` file to your staging branch in order to experiment with it before adding it to your deployment branch.</span></span>
3. <span data-ttu-id="59b81-175">`project.json` 파일을 추가하면 함수의 스트리밍 로그에 다음 예제와 유사한 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="59b81-175">After the `project.json` file is added, you will see output similar to the following example in your function's streaming log:</span></span>

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

## <a name="environment-variables"></a><span data-ttu-id="59b81-176">환경 변수</span><span class="sxs-lookup"><span data-stu-id="59b81-176">Environment variables</span></span>
<span data-ttu-id="59b81-177">환경 변수 또는 앱 설정 값을 가져오려면 다음 예제와 같이 `System.Environment.GetEnvironmentVariable`을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="59b81-177">To get an environment variable or an app setting value, use `System.Environment.GetEnvironmentVariable`, for example:</span></span>

```fsharp
open System.Environment

let Run(timer: TimerInfo, log: TraceWriter) =
    log.Info("Storage = " + GetEnvironmentVariable("AzureWebJobsStorage"))
    log.Info("Site = " + GetEnvironmentVariable("WEBSITE_SITE_NAME"))
```

## <a name="reusing-fsx-code"></a><span data-ttu-id="59b81-178">.fsx 코드 다시 사용</span><span class="sxs-lookup"><span data-stu-id="59b81-178">Reusing .fsx code</span></span>
<span data-ttu-id="59b81-179">`#load` 지시문을 사용하면 다른 `.fsx` 파일의 코드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59b81-179">You can use code from other `.fsx` files by using a `#load` directive.</span></span> <span data-ttu-id="59b81-180">예:</span><span class="sxs-lookup"><span data-stu-id="59b81-180">For example:</span></span>

`run.fsx`

```fsharp
#load "logger.fsx"

let Run(timer: TimerInfo, log: TraceWriter) =
    mylog log (sprintf "Timer: %s" DateTime.Now.ToString())
```

`logger.fsx`

```fsharp
let mylog(log: TraceWriter, text: string) =
    log.Verbose(text);
```

<span data-ttu-id="59b81-181">`#load` 지시문에 제공하는 경로는 `.fsx` 파일의 위치에 상대적입니다.</span><span class="sxs-lookup"><span data-stu-id="59b81-181">Paths provides to the `#load` directive are relative to the location of your `.fsx` file.</span></span>

* <span data-ttu-id="59b81-182">`#load "logger.fsx"`는 함수 폴더에 있는 파일을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="59b81-182">`#load "logger.fsx"` loads a file located in the function folder.</span></span>
* <span data-ttu-id="59b81-183">`#load "package\logger.fsx"`는 함수 폴더의 `package` 폴더에 있는 파일을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="59b81-183">`#load "package\logger.fsx"` loads a file located in the `package` folder in the function folder.</span></span>
* <span data-ttu-id="59b81-184">`#load "..\shared\mylogger.fsx"`는 함수 폴더와 동일한 수준의 `shared` 폴더 즉, `wwwroot`에 있는 파일을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="59b81-184">`#load "..\shared\mylogger.fsx"` loads a file located in the `shared` folder at the same level as the function folder, that is, directly under `wwwroot`.</span></span>

<span data-ttu-id="59b81-185">`#load` 지시문은 `.fs`파일이 아닌 `.fsx`(F# 스크립트) 파일에서만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="59b81-185">The `#load` directive only works with `.fsx` (F# script) files, and not with `.fs` files.</span></span>

## <a name="next-steps"></a><span data-ttu-id="59b81-186">다음 단계</span><span class="sxs-lookup"><span data-stu-id="59b81-186">Next steps</span></span>
<span data-ttu-id="59b81-187">자세한 내용은 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59b81-187">For more information, see the following resources:</span></span>

* [<span data-ttu-id="59b81-188">F# 가이드</span><span class="sxs-lookup"><span data-stu-id="59b81-188">F# Guide</span></span>](/dotnet/articles/fsharp/index)
* [<span data-ttu-id="59b81-189">Azure Functions에 대한 모범 사례</span><span class="sxs-lookup"><span data-stu-id="59b81-189">Best Practices for Azure Functions</span></span>](functions-best-practices.md)
* [<span data-ttu-id="59b81-190">Azure Functions 개발자 참조</span><span class="sxs-lookup"><span data-stu-id="59b81-190">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="59b81-191">Azure Functions C# 개발자 참조</span><span class="sxs-lookup"><span data-stu-id="59b81-191">Azure Functions C# developer reference</span></span>](functions-reference-csharp.md)
* [<span data-ttu-id="59b81-192">Azure Functions NodeJS 개발자 참조</span><span class="sxs-lookup"><span data-stu-id="59b81-192">Azure Functions NodeJS developer reference</span></span>](functions-reference-node.md)
* [<span data-ttu-id="59b81-193">Azure Functions 트리거 및 바인딩</span><span class="sxs-lookup"><span data-stu-id="59b81-193">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)
* [<span data-ttu-id="59b81-194">Azure Functions 테스트</span><span class="sxs-lookup"><span data-stu-id="59b81-194">Azure Functions testing</span></span>](functions-test-a-function.md)
* [<span data-ttu-id="59b81-195">Azure Functions 크기 조정</span><span class="sxs-lookup"><span data-stu-id="59b81-195">Azure Functions scaling</span></span>](functions-scale.md)


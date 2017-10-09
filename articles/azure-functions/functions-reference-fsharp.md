---
title: "aaaAzure 함수 F # 개발자 참조 | Microsoft Docs"
description: "이해 방법을 toodevelop F #을 사용 하 여 Azure 함수입니다."
services: functions
documentationcenter: fsharp
author: sylvanc
manager: jbronsk
editor: 
tags: 
keywords: "Azure Functions, 함수, 이벤트 처리, 웹후크, 동적 계산, 서버가 없는 아키텍처, F#"
ms.assetid: e60226e5-2630-41d7-9e5b-9f9e5acc8e50
ms.service: functions
ms.devlang: fsharp
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 09/09/2016
ms.author: syclebsc
ms.openlocfilehash: 1ac366ba6f73d191c582dcd9214b688ef719617a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-f-developer-reference"></a><span data-ttu-id="a72a7-104">Azure Functions F# 개발자 참조</span><span class="sxs-lookup"><span data-stu-id="a72a7-104">Azure Functions F# Developer Reference</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a72a7-105">C# 스크립트</span><span class="sxs-lookup"><span data-stu-id="a72a7-105">C# script</span></span>](functions-reference-csharp.md)
> * [<span data-ttu-id="a72a7-106">F# 스크립트</span><span class="sxs-lookup"><span data-stu-id="a72a7-106">F# script</span></span>](functions-reference-fsharp.md)
> * [<span data-ttu-id="a72a7-107">Node.JS</span><span class="sxs-lookup"><span data-stu-id="a72a7-107">Node.js</span></span>](functions-reference-node.md)
> 
> 

<span data-ttu-id="a72a7-108">F # Azure 기능에 쉽게 소량의 코드 또는 "함수를" hello 클라우드에서 실행 하기 위한 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="a72a7-108">F# for Azure Functions is a solution for easily running small pieces of code, or "functions," in hello cloud.</span></span> <span data-ttu-id="a72a7-109">데이터는 함수 인수를 통해 F# 함수로 흐릅니다.</span><span class="sxs-lookup"><span data-stu-id="a72a7-109">Data flows into your F# function via function arguments.</span></span> <span data-ttu-id="a72a7-110">인수 이름에 지정 된 `function.json`로 거 및 cancellation 토큰 함수 hello 등의 작업에 액세스 하기 위한 미리 정의 된 이름이 고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a72a7-110">Argument names are specified in `function.json`, and there are predefined names for accessing things like hello function logger and cancellation tokens.</span></span>

<span data-ttu-id="a72a7-111">이 문서에서는 hello 이미 읽어본 가정 [Azure 함수 개발자 참조](functions-reference.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a72a7-111">This article assumes that you've already read hello [Azure Functions developer reference](functions-reference.md).</span></span>

## <a name="how-fsx-works"></a><span data-ttu-id="a72a7-112">.fsx의 작동 방식</span><span class="sxs-lookup"><span data-stu-id="a72a7-112">How .fsx works</span></span>
<span data-ttu-id="a72a7-113">`.fsx` 파일은 F# 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="a72a7-113">An `.fsx` file is an F# script.</span></span> <span data-ttu-id="a72a7-114">단일 파일에 포함된 F# 프로젝트로 생각할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a72a7-114">It can be thought of as an F# project that's contained in a single file.</span></span> <span data-ttu-id="a72a7-115">hello 파일 포함 (이 경우 Azure 함수)에서 프로그램에 대 한 두 hello 코드 및 종속성을 관리 하기 위한 지시문입니다.</span><span class="sxs-lookup"><span data-stu-id="a72a7-115">hello file contains both hello code for your program (in this case, your Azure Function) and directives for managing dependencies.</span></span>

<span data-ttu-id="a72a7-116">사용 하는 경우는 `.fsx` Azure 함수에 대 한 일반적으로 필요한 어셈블리가 hello "상용구" 보다는 함수 코드에서 toofocus를 허용 하기 위해 자동으로 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="a72a7-116">When you use an `.fsx` for an Azure Function, commonly required assemblies are automatically included for you, allowing you toofocus on hello function rather than "boilerplate" code.</span></span>

## <a name="binding-tooarguments"></a><span data-ttu-id="a72a7-117">바인딩 tooarguments</span><span class="sxs-lookup"><span data-stu-id="a72a7-117">Binding tooarguments</span></span>
<span data-ttu-id="a72a7-118">각 바인딩은 지원 몇 가지 인수 집합에 설명된 된 hello로 [Azure 함수 트리거 및 바인딩 개발자 참조](functions-triggers-bindings.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a72a7-118">Each binding supports some set of arguments, as detailed in hello [Azure Functions triggers and bindings developer reference](functions-triggers-bindings.md).</span></span> <span data-ttu-id="a72a7-119">예를 들어 blob 트리거가 지원 hello 인수 바인딩 중 하나는 F # 레코드를 사용 하 여 표현 될 수 있는 POCO입니다.</span><span class="sxs-lookup"><span data-stu-id="a72a7-119">For example, one of hello argument bindings a blob trigger supports is a POCO, which can be expressed using an F# record.</span></span> <span data-ttu-id="a72a7-120">예:</span><span class="sxs-lookup"><span data-stu-id="a72a7-120">For example:</span></span>

```fsharp
type Item = { Id: string }

let Run(blob: string, output: byref<Item>) =
    let item = { Id = "Some ID" }
    output <- item
```

<span data-ttu-id="a72a7-121">이 F# Azure Function에서는 하나 이상의 인수를 사용하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a72a7-121">Your F# Azure Function will take one or more arguments.</span></span> <span data-ttu-id="a72a7-122">너무 이라고 Azure 함수 인수에 대해 논의할 때*입력* 인수 및 *출력* 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="a72a7-122">When we talk about Azure Functions arguments, we refer too*input* arguments and *output* arguments.</span></span> <span data-ttu-id="a72a7-123">입력 인수가 정확 하 게 그 말: tooyour F # Azure 함수를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a72a7-123">An input argument is exactly what it sounds like: input tooyour F# Azure Function.</span></span> <span data-ttu-id="a72a7-124">*출력* 인수는 변경할 수 있는 데이터 또는 `byref<>` 방식으로 toopass 데이터 백업으로 사용 되는 인수 *아웃* 함수의 합니다.</span><span class="sxs-lookup"><span data-stu-id="a72a7-124">An *output* argument is mutable data or a `byref<>` argument that serves as a way toopass data back *out* of your function.</span></span>

<span data-ttu-id="a72a7-125">위의 hello 예에서 `blob` 은 입력된 인수로 및 `output` 출력 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="a72a7-125">In hello example above, `blob` is an input argument, and `output` is an output argument.</span></span> <span data-ttu-id="a72a7-126">사용 하는 `byref<>` 에 대 한 `output` (필요 tooadd hello는 `[<Out>]` 주석).</span><span class="sxs-lookup"><span data-stu-id="a72a7-126">Notice that we used `byref<>` for `output` (there's no need tooadd hello `[<Out>]` annotation).</span></span> <span data-ttu-id="a72a7-127">사용 하 여 한 `byref<>` 형식에는 레코드 또는 개체 hello 인수를 참조 하 여 함수 toochange 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a72a7-127">Using a `byref<>` type allows your function toochange which record or object hello argument refers to.</span></span>

<span data-ttu-id="a72a7-128">입력된 유형으로는 F # 레코드를 사용 하면 레코드 정의 hello로 표시 되어야 `[<CLIMutable>]` 의 순서로 tooallow hello Azure 기능 프레임 워크 tooset hello 필드를 적절 하 게 하기 전에 hello 레코드 tooyour 함수를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="a72a7-128">When an F# record is used as an input type, hello record definition must be marked with `[<CLIMutable>]` in order tooallow hello Azure Functions framework tooset hello fields appropriately before passing hello record tooyour function.</span></span> <span data-ttu-id="a72a7-129">Hello 내부적 `[<CLIMutable>]` hello 레코드 속성의 setter를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="a72a7-129">Under hello hood, `[<CLIMutable>]` generates setters for hello record properties.</span></span> <span data-ttu-id="a72a7-130">예:</span><span class="sxs-lookup"><span data-stu-id="a72a7-130">For example:</span></span>

```fsharp
[<CLIMutable>]
type TestObject =
    { SenderName : string
      Greeting : string }

let Run(req: TestObject, log: TraceWriter) =
    { req with Greeting = sprintf "Hello, %s" req.SenderName }
```

<span data-ttu-id="a72a7-131">F# 클래스는 들어오고 나가는 인수 모두에 대해서도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a72a7-131">An F# class can also be used for both in and out arguments.</span></span> <span data-ttu-id="a72a7-132">클래스의 경우 일반적으로 속성은 getter 및 setter가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a72a7-132">For a class, properties will usually need getters and setters.</span></span> <span data-ttu-id="a72a7-133">예:</span><span class="sxs-lookup"><span data-stu-id="a72a7-133">For example:</span></span>

```fsharp
type Item() =
    member val Id = "" with get,set
    member val Text = "" with get,set

let Run(input: string, item: byref<Item>) =
    let result = Item(Id = input, Text = "Hello from F#!")
    item <- result
```

## <a name="logging"></a><span data-ttu-id="a72a7-134">로깅</span><span class="sxs-lookup"><span data-stu-id="a72a7-134">Logging</span></span>
<span data-ttu-id="a72a7-135">toolog 출력 tooyour [스트리밍 로그](../app-service-web/web-sites-streaming-logs-and-console.md) F #에서 함수 형식의 인수를 사용 해야 `TraceWriter`합니다.</span><span class="sxs-lookup"><span data-stu-id="a72a7-135">toolog output tooyour [streaming logs](../app-service-web/web-sites-streaming-logs-and-console.md) in F#, your function should take an argument of type `TraceWriter`.</span></span> <span data-ttu-id="a72a7-136">일관성을 위해 이 인수의 이름을 `log`로 지정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a72a7-136">For consistency, we recommend this argument is named `log`.</span></span> <span data-ttu-id="a72a7-137">예:</span><span class="sxs-lookup"><span data-stu-id="a72a7-137">For example:</span></span>

```fsharp
let Run(blob: string, output: byref<string>, log: TraceWriter) =
    log.Verbose(sprintf "F# Azure Function processed a blob: %s" blob)
    output <- input
```

## <a name="async"></a><span data-ttu-id="a72a7-138">Async</span><span class="sxs-lookup"><span data-stu-id="a72a7-138">Async</span></span>
<span data-ttu-id="a72a7-139">hello `async` 워크플로 사용할 수 있습니다, 이지만 hello 결과 tooreturn는 `Task`합니다.</span><span class="sxs-lookup"><span data-stu-id="a72a7-139">hello `async` workflow can be used, but hello result needs tooreturn a `Task`.</span></span> <span data-ttu-id="a72a7-140">`Async.StartAsTask`를 사용하여 이를 확인할 수 있습니다. 예:</span><span class="sxs-lookup"><span data-stu-id="a72a7-140">This can be done with `Async.StartAsTask`, for example:</span></span>

```fsharp
let Run(req: HttpRequestMessage) =
    async {
        return new HttpResponseMessage(HttpStatusCode.OK)
    } |> Async.StartAsTask
```

## <a name="cancellation-token"></a><span data-ttu-id="a72a7-141">취소 토큰</span><span class="sxs-lookup"><span data-stu-id="a72a7-141">Cancellation Token</span></span>
<span data-ttu-id="a72a7-142">함수에서 toohandle 종료를 정상적으로 필요한 경우 파일을 지정할 수는 [ `CancellationToken` ](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="a72a7-142">If your function needs toohandle shutdown gracefully, you can give it a [`CancellationToken`](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) argument.</span></span> <span data-ttu-id="a72a7-143">이는 `async`와 결합할 수 있습니다. 예:</span><span class="sxs-lookup"><span data-stu-id="a72a7-143">This can be combined with `async`, for example:</span></span>

```fsharp
let Run(req: HttpRequestMessage, token: CancellationToken)
    let f = async {
        do! Async.Sleep(10)
        return new HttpResponseMessage(HttpStatusCode.OK)
    }
    Async.StartAsTask(f, token)
```

## <a name="importing-namespaces"></a><span data-ttu-id="a72a7-144">네임스페이스 가져오기</span><span class="sxs-lookup"><span data-stu-id="a72a7-144">Importing namespaces</span></span>
<span data-ttu-id="a72a7-145">네임 스페이스 hello에서 열 수 일반적인 방법으로:</span><span class="sxs-lookup"><span data-stu-id="a72a7-145">Namespaces can be opened in hello usual way:</span></span>

```fsharp
open System.Net
open System.Threading.Tasks

let Run(req: HttpRequestMessage, log: TraceWriter) =
    ...
```

<span data-ttu-id="a72a7-146">다음 네임 스페이스 hello은 자동으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="a72a7-146">hello following namespaces are automatically opened:</span></span>

* `System`
* `System.Collections.Generic`
* `System.IO`
* `System.Linq`
* `System.Net.Http`
* `System.Threading.Tasks`
* `Microsoft.Azure.WebJobs`
* <span data-ttu-id="a72a7-147">`Microsoft.Azure.WebJobs.Host`</span><span class="sxs-lookup"><span data-stu-id="a72a7-147">`Microsoft.Azure.WebJobs.Host`.</span></span>

## <a name="referencing-external-assemblies"></a><span data-ttu-id="a72a7-148">외부 어셈블리 참조</span><span class="sxs-lookup"><span data-stu-id="a72a7-148">Referencing External Assemblies</span></span>
<span data-ttu-id="a72a7-149">마찬가지로, 프레임 워크 어셈블리 참조가 추가 hello로 `#r "AssemblyName"` 지시문입니다.</span><span class="sxs-lookup"><span data-stu-id="a72a7-149">Similarly, framework assembly references be added with hello `#r "AssemblyName"` directive.</span></span>

```fsharp
#r "System.Web.Http"

open System.Net
open System.Net.Http
open System.Threading.Tasks

let Run(req: HttpRequestMessage, log: TraceWriter) =
    ...
```

<span data-ttu-id="a72a7-150">hello 다음 어셈블리는 자동으로 함수로 추가한 hello Azure 호스팅 환경:</span><span class="sxs-lookup"><span data-stu-id="a72a7-150">hello following assemblies are automatically added by hello Azure Functions hosting environment:</span></span>

* <span data-ttu-id="a72a7-151">`mscorlib`,</span><span class="sxs-lookup"><span data-stu-id="a72a7-151">`mscorlib`,</span></span>
* `System`
* `System.Core`
* `System.Xml`
* `System.Net.Http`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`
* `Microsoft.Azure.WebJobs.Extensions`
* `System.Web.Http`
* <span data-ttu-id="a72a7-152">`System.Net.Http.Formatting`</span><span class="sxs-lookup"><span data-stu-id="a72a7-152">`System.Net.Http.Formatting`.</span></span>

<span data-ttu-id="a72a7-153">또한 hello 다음 어셈블리는 특수 대/소문자 및 simplename 참조할 수 있습니다 (예: `#r "AssemblyName"`):</span><span class="sxs-lookup"><span data-stu-id="a72a7-153">In addition, hello following assemblies are special cased and may be referenced by simplename (e.g. `#r "AssemblyName"`):</span></span>

* `Newtonsoft.Json`
* `Microsoft.WindowsAzure.Storage`
* `Microsoft.ServiceBus`
* `Microsoft.AspNet.WebHooks.Receivers`
* <span data-ttu-id="a72a7-154">`Microsoft.AspNEt.WebHooks.Common`</span><span class="sxs-lookup"><span data-stu-id="a72a7-154">`Microsoft.AspNEt.WebHooks.Common`.</span></span>

<span data-ttu-id="a72a7-155">전용 어셈블리 tooreference 해야 할 경우 hello 어셈블리 파일을 업로드할 수 있습니다는 `bin` 상대 tooyour 함수 폴더 및 파일 이름 (예: hello 사용 하 여 참조  `#r "MyAssembly.dll"`).</span><span class="sxs-lookup"><span data-stu-id="a72a7-155">If you need tooreference a private assembly, you can upload hello assembly file into a `bin` folder relative tooyour function and reference it by using hello file name (e.g.  `#r "MyAssembly.dll"`).</span></span> <span data-ttu-id="a72a7-156">Tooupload tooyour 함수 폴더 파일 하는 방법에 대 한 내용은 hello 패키지 관리에 대 한 섹션을 다음을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="a72a7-156">For information on how tooupload files tooyour function folder, see hello following section on package management.</span></span>

## <a name="editor-prelude"></a><span data-ttu-id="a72a7-157">Editor Prelude</span><span class="sxs-lookup"><span data-stu-id="a72a7-157">Editor Prelude</span></span>
<span data-ttu-id="a72a7-158">F # 컴파일러 서비스를 지 원하는 편집기 hello 네임 스페이스 및 Azure 기능을 자동으로 포함 하는 어셈블리의 알 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a72a7-158">An editor that supports F# Compiler Services will not be aware of hello namespaces and assemblies that Azure Functions automatically includes.</span></span> <span data-ttu-id="a72a7-159">따라서 유용한 tooinclude hello 편집기를 사용 하는 hello 어셈블리를 찾을 수 있도록에 대해 궁금할 수 있습니다 및 tooexplicitly 네임 스페이스를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a72a7-159">As such, it can be useful tooinclude a prelude that helps hello editor find hello assemblies you are using, and tooexplicitly open namespaces.</span></span> <span data-ttu-id="a72a7-160">예:</span><span class="sxs-lookup"><span data-stu-id="a72a7-160">For example:</span></span>

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

<span data-ttu-id="a72a7-161">코드를 실행 하는 Azure 함수를 사용 하 여 hello 원본 처리 `COMPILED` 정의 없으므로 hello 편집기 궁금할 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a72a7-161">When Azure Functions executes your code, it processes hello source with `COMPILED` defined, so hello editor prelude will be ignored.</span></span>

<a name="package"></a>

## <a name="package-management"></a><span data-ttu-id="a72a7-162">패키지 관리</span><span class="sxs-lookup"><span data-stu-id="a72a7-162">Package management</span></span>
<span data-ttu-id="a72a7-163">F # 함수를에서 toouse NuGet 패키지 추가 `project.json` toohello hello 함수 폴더 hello 함수 앱의 파일 시스템 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="a72a7-163">toouse NuGet packages in an F# function, add a `project.json` file toohello hello function's folder in hello function app's file system.</span></span> <span data-ttu-id="a72a7-164">다음은 예제 `project.json` 너무 NuGet 패키지 참조를 추가 하는 파일`Microsoft.ProjectOxford.Face` 1.1.0 버전:</span><span class="sxs-lookup"><span data-stu-id="a72a7-164">Here is an example `project.json` file that adds a NuGet package reference too`Microsoft.ProjectOxford.Face` version 1.1.0:</span></span>

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

<span data-ttu-id="a72a7-165">Hello.NET Framework 4.6 지원만 해야 하는 프로그램 `project.json` 파일 지정 `net46` 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="a72a7-165">Only hello .NET Framework 4.6 is supported, so make sure that your `project.json` file specifies `net46` as shown here.</span></span>

<span data-ttu-id="a72a7-166">업로드 하는 경우는 `project.json` 파일, hello 런타임 hello 패키지를 가져오고 toohello 패키지 어셈블리 참조를 자동으로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a72a7-166">When you upload a `project.json` file, hello runtime gets hello packages and automatically adds references toohello package assemblies.</span></span> <span data-ttu-id="a72a7-167">Tooadd 않아도 `#r "AssemblyName"` 지시문입니다.</span><span class="sxs-lookup"><span data-stu-id="a72a7-167">You don't need tooadd `#r "AssemblyName"` directives.</span></span> <span data-ttu-id="a72a7-168">필요한 hello 추가 `open` 문 tooyour `.fsx` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="a72a7-168">Just add hello required `open` statements tooyour `.fsx` file.</span></span>

<span data-ttu-id="a72a7-169">Tooput 자동으로 어셈블리를 참조 하면 편집기 궁금할 tooimprove에서에서 F # 컴파일 서비스와의 편집기의 상호 작용을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a72a7-169">You may wish tooput automatically references assemblies in your editor prelude, tooimprove your editor's interaction with F# Compile Services.</span></span>

### <a name="how-tooadd-a-projectjson-file-tooyour-azure-function"></a><span data-ttu-id="a72a7-170">어떻게 tooadd는 `project.json` 파일 tooyour Azure 함수</span><span class="sxs-lookup"><span data-stu-id="a72a7-170">How tooadd a `project.json` file tooyour Azure Function</span></span>
1. <span data-ttu-id="a72a7-171">Hello Azure 포털에서에서 사용자가 함수를 열어 할 수 있는 함수 앱 하는지 확인 하 여 시작 합니다.이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a72a7-171">Begin by making sure your function app is running, which you can do by opening your function in hello Azure portal.</span></span> <span data-ttu-id="a72a7-172">또한 액세스할 toohello 스트리밍 로그 패키지 설치 출력 내용이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a72a7-172">This also gives access toohello streaming logs where package installation output will be displayed.</span></span>
2. <span data-ttu-id="a72a7-173">tooupload는 `project.json` 파일에 설명 된 hello 방법 중 하나를 사용 하 여, [tooupdate 앱 파일을 어떻게 작동 하는지](functions-reference.md#fileupdate)합니다.</span><span class="sxs-lookup"><span data-stu-id="a72a7-173">tooupload a `project.json` file, use one of hello methods described in [how tooupdate function app files](functions-reference.md#fileupdate).</span></span> <span data-ttu-id="a72a7-174">사용 중인 경우 [Azure 함수에 대 한 연속 배포](functions-continuous-deployment.md)를 추가할 수 있습니다는 `project.json` 파일 tooyour tooyour 배포 지점에 추가 하기 전에 함께 순서 tooexperiment의 분기를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="a72a7-174">If you are using [Continuous Deployment for Azure Functions](functions-continuous-deployment.md), you can add a `project.json` file tooyour staging branch in order tooexperiment with it before adding it tooyour deployment branch.</span></span>
3. <span data-ttu-id="a72a7-175">Hello 후 `project.json` 파일을 추가, 다음 예제에서는 함수에서 출력 유사한 toohello 스트리밍 로그 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a72a7-175">After hello `project.json` file is added, you will see output similar toohello following example in your function's streaming log:</span></span>

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

## <a name="environment-variables"></a><span data-ttu-id="a72a7-176">환경 변수</span><span class="sxs-lookup"><span data-stu-id="a72a7-176">Environment variables</span></span>
<span data-ttu-id="a72a7-177">tooget 환경 변수 또는 응용 프로그램 설정 값을 사용 하 여 `System.Environment.GetEnvironmentVariable`, 예:</span><span class="sxs-lookup"><span data-stu-id="a72a7-177">tooget an environment variable or an app setting value, use `System.Environment.GetEnvironmentVariable`, for example:</span></span>

```fsharp
open System.Environment

let Run(timer: TimerInfo, log: TraceWriter) =
    log.Info("Storage = " + GetEnvironmentVariable("AzureWebJobsStorage"))
    log.Info("Site = " + GetEnvironmentVariable("WEBSITE_SITE_NAME"))
```

## <a name="reusing-fsx-code"></a><span data-ttu-id="a72a7-178">.fsx 코드 다시 사용</span><span class="sxs-lookup"><span data-stu-id="a72a7-178">Reusing .fsx code</span></span>
<span data-ttu-id="a72a7-179">`#load` 지시문을 사용하면 다른 `.fsx` 파일의 코드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a72a7-179">You can use code from other `.fsx` files by using a `#load` directive.</span></span> <span data-ttu-id="a72a7-180">예:</span><span class="sxs-lookup"><span data-stu-id="a72a7-180">For example:</span></span>

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

<span data-ttu-id="a72a7-181">경로 제공 toohello `#load` 지시문의 상대 toohello 위치는 프로그램 `.fsx` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="a72a7-181">Paths provides toohello `#load` directive are relative toohello location of your `.fsx` file.</span></span>

* <span data-ttu-id="a72a7-182">`#load "logger.fsx"`hello 함수 폴더에 있는 파일을 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="a72a7-182">`#load "logger.fsx"` loads a file located in hello function folder.</span></span>
* <span data-ttu-id="a72a7-183">`#load "package\logger.fsx"`hello에 있는 파일을 로드 `package` hello 함수 폴더의 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="a72a7-183">`#load "package\logger.fsx"` loads a file located in hello `package` folder in hello function folder.</span></span>
* <span data-ttu-id="a72a7-184">`#load "..\shared\mylogger.fsx"`hello에 있는 파일을 로드 `shared` hello 동일 수준이 hello 함수 폴더와 폴더 바로 아래 `wwwroot`합니다.</span><span class="sxs-lookup"><span data-stu-id="a72a7-184">`#load "..\shared\mylogger.fsx"` loads a file located in hello `shared` folder at hello same level as hello function folder, that is, directly under `wwwroot`.</span></span>

<span data-ttu-id="a72a7-185">hello `#load` 지시문에만 작동 `.fsx` (F # 스크립트) 파일을 사용할 수 없는 `.fs` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="a72a7-185">hello `#load` directive only works with `.fsx` (F# script) files, and not with `.fs` files.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a72a7-186">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a72a7-186">Next steps</span></span>
<span data-ttu-id="a72a7-187">자세한 내용은 다음 리소스는 hello 참조:</span><span class="sxs-lookup"><span data-stu-id="a72a7-187">For more information, see hello following resources:</span></span>

* [<span data-ttu-id="a72a7-188">F# 가이드</span><span class="sxs-lookup"><span data-stu-id="a72a7-188">F# Guide</span></span>](/dotnet/articles/fsharp/index)
* [<span data-ttu-id="a72a7-189">Azure Functions에 대한 모범 사례</span><span class="sxs-lookup"><span data-stu-id="a72a7-189">Best Practices for Azure Functions</span></span>](functions-best-practices.md)
* [<span data-ttu-id="a72a7-190">Azure Functions 개발자 참조</span><span class="sxs-lookup"><span data-stu-id="a72a7-190">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="a72a7-191">Azure Functions C# 개발자 참조</span><span class="sxs-lookup"><span data-stu-id="a72a7-191">Azure Functions C# developer reference</span></span>](functions-reference-csharp.md)
* [<span data-ttu-id="a72a7-192">Azure Functions NodeJS 개발자 참조</span><span class="sxs-lookup"><span data-stu-id="a72a7-192">Azure Functions NodeJS developer reference</span></span>](functions-reference-node.md)
* [<span data-ttu-id="a72a7-193">Azure Functions 트리거 및 바인딩</span><span class="sxs-lookup"><span data-stu-id="a72a7-193">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)
* [<span data-ttu-id="a72a7-194">Azure Functions 테스트</span><span class="sxs-lookup"><span data-stu-id="a72a7-194">Azure Functions testing</span></span>](functions-test-a-function.md)
* [<span data-ttu-id="a72a7-195">Azure Functions 크기 조정</span><span class="sxs-lookup"><span data-stu-id="a72a7-195">Azure Functions scaling</span></span>](functions-scale.md)


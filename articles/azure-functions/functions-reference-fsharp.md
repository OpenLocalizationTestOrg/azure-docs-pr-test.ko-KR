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
# <a name="azure-functions-f-developer-reference"></a>Azure Functions F# 개발자 참조
> [!div class="op_single_selector"]
> * [C# 스크립트](functions-reference-csharp.md)
> * [F# 스크립트](functions-reference-fsharp.md)
> * [Node.JS](functions-reference-node.md)
> 
> 

F # Azure 기능에 쉽게 소량의 코드 또는 "함수를" hello 클라우드에서 실행 하기 위한 솔루션입니다. 데이터는 함수 인수를 통해 F# 함수로 흐릅니다. 인수 이름에 지정 된 `function.json`로 거 및 cancellation 토큰 함수 hello 등의 작업에 액세스 하기 위한 미리 정의 된 이름이 고 합니다.

이 문서에서는 hello 이미 읽어본 가정 [Azure 함수 개발자 참조](functions-reference.md)합니다.

## <a name="how-fsx-works"></a>.fsx의 작동 방식
`.fsx` 파일은 F# 스크립트입니다. 단일 파일에 포함된 F# 프로젝트로 생각할 수 있습니다. hello 파일 포함 (이 경우 Azure 함수)에서 프로그램에 대 한 두 hello 코드 및 종속성을 관리 하기 위한 지시문입니다.

사용 하는 경우는 `.fsx` Azure 함수에 대 한 일반적으로 필요한 어셈블리가 hello "상용구" 보다는 함수 코드에서 toofocus를 허용 하기 위해 자동으로 포함 합니다.

## <a name="binding-tooarguments"></a>바인딩 tooarguments
각 바인딩은 지원 몇 가지 인수 집합에 설명된 된 hello로 [Azure 함수 트리거 및 바인딩 개발자 참조](functions-triggers-bindings.md)합니다. 예를 들어 blob 트리거가 지원 hello 인수 바인딩 중 하나는 F # 레코드를 사용 하 여 표현 될 수 있는 POCO입니다. 예:

```fsharp
type Item = { Id: string }

let Run(blob: string, output: byref<Item>) =
    let item = { Id = "Some ID" }
    output <- item
```

이 F# Azure Function에서는 하나 이상의 인수를 사용하게 됩니다. 너무 이라고 Azure 함수 인수에 대해 논의할 때*입력* 인수 및 *출력* 인수입니다. 입력 인수가 정확 하 게 그 말: tooyour F # Azure 함수를 입력 합니다. *출력* 인수는 변경할 수 있는 데이터 또는 `byref<>` 방식으로 toopass 데이터 백업으로 사용 되는 인수 *아웃* 함수의 합니다.

위의 hello 예에서 `blob` 은 입력된 인수로 및 `output` 출력 인수입니다. 사용 하는 `byref<>` 에 대 한 `output` (필요 tooadd hello는 `[<Out>]` 주석). 사용 하 여 한 `byref<>` 형식에는 레코드 또는 개체 hello 인수를 참조 하 여 함수 toochange 허용 합니다.

입력된 유형으로는 F # 레코드를 사용 하면 레코드 정의 hello로 표시 되어야 `[<CLIMutable>]` 의 순서로 tooallow hello Azure 기능 프레임 워크 tooset hello 필드를 적절 하 게 하기 전에 hello 레코드 tooyour 함수를 전달 합니다. Hello 내부적 `[<CLIMutable>]` hello 레코드 속성의 setter를 생성 합니다. 예:

```fsharp
[<CLIMutable>]
type TestObject =
    { SenderName : string
      Greeting : string }

let Run(req: TestObject, log: TraceWriter) =
    { req with Greeting = sprintf "Hello, %s" req.SenderName }
```

F# 클래스는 들어오고 나가는 인수 모두에 대해서도 사용할 수 있습니다. 클래스의 경우 일반적으로 속성은 getter 및 setter가 필요합니다. 예:

```fsharp
type Item() =
    member val Id = "" with get,set
    member val Text = "" with get,set

let Run(input: string, item: byref<Item>) =
    let result = Item(Id = input, Text = "Hello from F#!")
    item <- result
```

## <a name="logging"></a>로깅
toolog 출력 tooyour [스트리밍 로그](../app-service-web/web-sites-streaming-logs-and-console.md) F #에서 함수 형식의 인수를 사용 해야 `TraceWriter`합니다. 일관성을 위해 이 인수의 이름을 `log`로 지정하는 것이 좋습니다. 예:

```fsharp
let Run(blob: string, output: byref<string>, log: TraceWriter) =
    log.Verbose(sprintf "F# Azure Function processed a blob: %s" blob)
    output <- input
```

## <a name="async"></a>Async
hello `async` 워크플로 사용할 수 있습니다, 이지만 hello 결과 tooreturn는 `Task`합니다. `Async.StartAsTask`를 사용하여 이를 확인할 수 있습니다. 예:

```fsharp
let Run(req: HttpRequestMessage) =
    async {
        return new HttpResponseMessage(HttpStatusCode.OK)
    } |> Async.StartAsTask
```

## <a name="cancellation-token"></a>취소 토큰
함수에서 toohandle 종료를 정상적으로 필요한 경우 파일을 지정할 수는 [ `CancellationToken` ](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) 인수입니다. 이는 `async`와 결합할 수 있습니다. 예:

```fsharp
let Run(req: HttpRequestMessage, token: CancellationToken)
    let f = async {
        do! Async.Sleep(10)
        return new HttpResponseMessage(HttpStatusCode.OK)
    }
    Async.StartAsTask(f, token)
```

## <a name="importing-namespaces"></a>네임스페이스 가져오기
네임 스페이스 hello에서 열 수 일반적인 방법으로:

```fsharp
open System.Net
open System.Threading.Tasks

let Run(req: HttpRequestMessage, log: TraceWriter) =
    ...
```

다음 네임 스페이스 hello은 자동으로 열립니다.

* `System`
* `System.Collections.Generic`
* `System.IO`
* `System.Linq`
* `System.Net.Http`
* `System.Threading.Tasks`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`

## <a name="referencing-external-assemblies"></a>외부 어셈블리 참조
마찬가지로, 프레임 워크 어셈블리 참조가 추가 hello로 `#r "AssemblyName"` 지시문입니다.

```fsharp
#r "System.Web.Http"

open System.Net
open System.Net.Http
open System.Threading.Tasks

let Run(req: HttpRequestMessage, log: TraceWriter) =
    ...
```

hello 다음 어셈블리는 자동으로 함수로 추가한 hello Azure 호스팅 환경:

* `mscorlib`,
* `System`
* `System.Core`
* `System.Xml`
* `System.Net.Http`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`
* `Microsoft.Azure.WebJobs.Extensions`
* `System.Web.Http`
* `System.Net.Http.Formatting`

또한 hello 다음 어셈블리는 특수 대/소문자 및 simplename 참조할 수 있습니다 (예: `#r "AssemblyName"`):

* `Newtonsoft.Json`
* `Microsoft.WindowsAzure.Storage`
* `Microsoft.ServiceBus`
* `Microsoft.AspNet.WebHooks.Receivers`
* `Microsoft.AspNEt.WebHooks.Common`

전용 어셈블리 tooreference 해야 할 경우 hello 어셈블리 파일을 업로드할 수 있습니다는 `bin` 상대 tooyour 함수 폴더 및 파일 이름 (예: hello 사용 하 여 참조  `#r "MyAssembly.dll"`). Tooupload tooyour 함수 폴더 파일 하는 방법에 대 한 내용은 hello 패키지 관리에 대 한 섹션을 다음을 참조 하세요.

## <a name="editor-prelude"></a>Editor Prelude
F # 컴파일러 서비스를 지 원하는 편집기 hello 네임 스페이스 및 Azure 기능을 자동으로 포함 하는 어셈블리의 알 수 없습니다. 따라서 유용한 tooinclude hello 편집기를 사용 하는 hello 어셈블리를 찾을 수 있도록에 대해 궁금할 수 있습니다 및 tooexplicitly 네임 스페이스를 엽니다. 예:

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

코드를 실행 하는 Azure 함수를 사용 하 여 hello 원본 처리 `COMPILED` 정의 없으므로 hello 편집기 궁금할 무시 됩니다.

<a name="package"></a>

## <a name="package-management"></a>패키지 관리
F # 함수를에서 toouse NuGet 패키지 추가 `project.json` toohello hello 함수 폴더 hello 함수 앱의 파일 시스템 파일입니다. 다음은 예제 `project.json` 너무 NuGet 패키지 참조를 추가 하는 파일`Microsoft.ProjectOxford.Face` 1.1.0 버전:

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

Hello.NET Framework 4.6 지원만 해야 하는 프로그램 `project.json` 파일 지정 `net46` 다음과 같이 합니다.

업로드 하는 경우는 `project.json` 파일, hello 런타임 hello 패키지를 가져오고 toohello 패키지 어셈블리 참조를 자동으로 추가 합니다. Tooadd 않아도 `#r "AssemblyName"` 지시문입니다. 필요한 hello 추가 `open` 문 tooyour `.fsx` 파일입니다.

Tooput 자동으로 어셈블리를 참조 하면 편집기 궁금할 tooimprove에서에서 F # 컴파일 서비스와의 편집기의 상호 작용을 지정할 수 있습니다.

### <a name="how-tooadd-a-projectjson-file-tooyour-azure-function"></a>어떻게 tooadd는 `project.json` 파일 tooyour Azure 함수
1. Hello Azure 포털에서에서 사용자가 함수를 열어 할 수 있는 함수 앱 하는지 확인 하 여 시작 합니다.이 실행 됩니다. 또한 액세스할 toohello 스트리밍 로그 패키지 설치 출력 내용이 표시 됩니다.
2. tooupload는 `project.json` 파일에 설명 된 hello 방법 중 하나를 사용 하 여, [tooupdate 앱 파일을 어떻게 작동 하는지](functions-reference.md#fileupdate)합니다. 사용 중인 경우 [Azure 함수에 대 한 연속 배포](functions-continuous-deployment.md)를 추가할 수 있습니다는 `project.json` 파일 tooyour tooyour 배포 지점에 추가 하기 전에 함께 순서 tooexperiment의 분기를 준비 합니다.
3. Hello 후 `project.json` 파일을 추가, 다음 예제에서는 함수에서 출력 유사한 toohello 스트리밍 로그 표시 됩니다.

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
tooget 환경 변수 또는 응용 프로그램 설정 값을 사용 하 여 `System.Environment.GetEnvironmentVariable`, 예:

```fsharp
open System.Environment

let Run(timer: TimerInfo, log: TraceWriter) =
    log.Info("Storage = " + GetEnvironmentVariable("AzureWebJobsStorage"))
    log.Info("Site = " + GetEnvironmentVariable("WEBSITE_SITE_NAME"))
```

## <a name="reusing-fsx-code"></a>.fsx 코드 다시 사용
`#load` 지시문을 사용하면 다른 `.fsx` 파일의 코드를 사용할 수 있습니다. 예:

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

경로 제공 toohello `#load` 지시문의 상대 toohello 위치는 프로그램 `.fsx` 파일입니다.

* `#load "logger.fsx"`hello 함수 폴더에 있는 파일을 로드 합니다.
* `#load "package\logger.fsx"`hello에 있는 파일을 로드 `package` hello 함수 폴더의 폴더입니다.
* `#load "..\shared\mylogger.fsx"`hello에 있는 파일을 로드 `shared` hello 동일 수준이 hello 함수 폴더와 폴더 바로 아래 `wwwroot`합니다.

hello `#load` 지시문에만 작동 `.fsx` (F # 스크립트) 파일을 사용할 수 없는 `.fs` 파일입니다.

## <a name="next-steps"></a>다음 단계
자세한 내용은 다음 리소스는 hello 참조:

* [F# 가이드](/dotnet/articles/fsharp/index)
* [Azure Functions에 대한 모범 사례](functions-best-practices.md)
* [Azure Functions 개발자 참조](functions-reference.md)
* [Azure Functions C# 개발자 참조](functions-reference-csharp.md)
* [Azure Functions NodeJS 개발자 참조](functions-reference-node.md)
* [Azure Functions 트리거 및 바인딩](functions-triggers-bindings.md)
* [Azure Functions 테스트](functions-test-a-function.md)
* [Azure Functions 크기 조정](functions-scale.md)


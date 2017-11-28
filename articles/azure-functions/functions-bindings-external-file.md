---
title: "aaaAzure 함수 외부 파일 바인딩 (미리 보기) | Microsoft Docs"
description: "Azure Functions에서 외부 파일 바인딩 사용"
services: functions
documentationcenter: 
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 04/12/2017
ms.author: alkarche
ms.openlocfilehash: 583d9c0b871dc68a79614749ba6ac6711fa820fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-external-file-bindings-preview"></a><span data-ttu-id="4edad-103">Azure Functions 외부 파일 바인딩(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="4edad-103">Azure Functions External File bindings (Preview)</span></span>
<span data-ttu-id="4edad-104">이 문서에서는 어떻게 toomanipulate에서에서 파일을 다른 SaaS 공급자 (예: OneDrive, Dropbox) 기본 제공 바인딩을 사용 하 여 함수 내에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="4edad-104">This article shows how toomanipulate files from different SaaS providers (e.g. OneDrive, Dropbox) within your function utilizing built-in bindings.</span></span> <span data-ttu-id="4edad-105">Azure Functions는 외부 파일에 대한 트리거, 입력 및 출력 바인딩을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="4edad-105">Azure functions supports trigger, input, and output bindings for external file.</span></span>

<span data-ttu-id="4edad-106">이 바인딩은 API 연결 tooSaaS 공급자 만들거나 함수 응용 프로그램의 리소스 그룹에서 기존 API 연결을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4edad-106">This binding creates API connections tooSaaS providers, or uses existing API connections from your Function App's resource group.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="supported-file-connections"></a><span data-ttu-id="4edad-107">지원되는 파일 연결</span><span class="sxs-lookup"><span data-stu-id="4edad-107">Supported File connections</span></span>

|<span data-ttu-id="4edad-108">커넥터</span><span class="sxs-lookup"><span data-stu-id="4edad-108">Connector</span></span>|<span data-ttu-id="4edad-109">트리거</span><span class="sxs-lookup"><span data-stu-id="4edad-109">Trigger</span></span>|<span data-ttu-id="4edad-110">입력</span><span class="sxs-lookup"><span data-stu-id="4edad-110">Input</span></span>|<span data-ttu-id="4edad-111">출력</span><span class="sxs-lookup"><span data-stu-id="4edad-111">Output</span></span>|
|:-----|:---:|:---:|:---:|
|[<span data-ttu-id="4edad-112">Box</span><span class="sxs-lookup"><span data-stu-id="4edad-112">Box</span></span>](https://www.box.com)|<span data-ttu-id="4edad-113">x</span><span class="sxs-lookup"><span data-stu-id="4edad-113">x</span></span>|<span data-ttu-id="4edad-114">x</span><span class="sxs-lookup"><span data-stu-id="4edad-114">x</span></span>|<span data-ttu-id="4edad-115">x</span><span class="sxs-lookup"><span data-stu-id="4edad-115">x</span></span>
|[<span data-ttu-id="4edad-116">Dropbox</span><span class="sxs-lookup"><span data-stu-id="4edad-116">Dropbox</span></span>](https://www.dropbox.com)|<span data-ttu-id="4edad-117">x</span><span class="sxs-lookup"><span data-stu-id="4edad-117">x</span></span>|<span data-ttu-id="4edad-118">x</span><span class="sxs-lookup"><span data-stu-id="4edad-118">x</span></span>|<span data-ttu-id="4edad-119">x</span><span class="sxs-lookup"><span data-stu-id="4edad-119">x</span></span>
|[<span data-ttu-id="4edad-120">FTP</span><span class="sxs-lookup"><span data-stu-id="4edad-120">FTP</span></span>](https://docs.microsoft.com/azure/app-service-web/app-service-deploy-ftp)|<span data-ttu-id="4edad-121">x</span><span class="sxs-lookup"><span data-stu-id="4edad-121">x</span></span>|<span data-ttu-id="4edad-122">x</span><span class="sxs-lookup"><span data-stu-id="4edad-122">x</span></span>|<span data-ttu-id="4edad-123">x</span><span class="sxs-lookup"><span data-stu-id="4edad-123">x</span></span>
|[<span data-ttu-id="4edad-124">OneDrive</span><span class="sxs-lookup"><span data-stu-id="4edad-124">OneDrive</span></span>](https://onedrive.live.com)|<span data-ttu-id="4edad-125">x</span><span class="sxs-lookup"><span data-stu-id="4edad-125">x</span></span>|<span data-ttu-id="4edad-126">x</span><span class="sxs-lookup"><span data-stu-id="4edad-126">x</span></span>|<span data-ttu-id="4edad-127">x</span><span class="sxs-lookup"><span data-stu-id="4edad-127">x</span></span>
|[<span data-ttu-id="4edad-128">OneDrive for Business</span><span class="sxs-lookup"><span data-stu-id="4edad-128">OneDrive for Business</span></span>](https://onedrive.live.com/about/business/)|<span data-ttu-id="4edad-129">x</span><span class="sxs-lookup"><span data-stu-id="4edad-129">x</span></span>|<span data-ttu-id="4edad-130">x</span><span class="sxs-lookup"><span data-stu-id="4edad-130">x</span></span>|<span data-ttu-id="4edad-131">x</span><span class="sxs-lookup"><span data-stu-id="4edad-131">x</span></span>
|[<span data-ttu-id="4edad-132">SFTP</span><span class="sxs-lookup"><span data-stu-id="4edad-132">SFTP</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-sftp)|<span data-ttu-id="4edad-133">x</span><span class="sxs-lookup"><span data-stu-id="4edad-133">x</span></span>|<span data-ttu-id="4edad-134">x</span><span class="sxs-lookup"><span data-stu-id="4edad-134">x</span></span>|<span data-ttu-id="4edad-135">x</span><span class="sxs-lookup"><span data-stu-id="4edad-135">x</span></span>
|[<span data-ttu-id="4edad-136">Google 드라이브</span><span class="sxs-lookup"><span data-stu-id="4edad-136">Google Drive</span></span>](https://www.google.com/drive/)||<span data-ttu-id="4edad-137">x</span><span class="sxs-lookup"><span data-stu-id="4edad-137">x</span></span>|<span data-ttu-id="4edad-138">x</span><span class="sxs-lookup"><span data-stu-id="4edad-138">x</span></span>|

> [!NOTE]
> <span data-ttu-id="4edad-139">외부 파일 연결은 [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list)에서도 사용할 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="4edad-139">External File connections can also be used in [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list)</span></span>

## <a name="external-file-trigger-binding"></a><span data-ttu-id="4edad-140">외부 파일 트리거 바인딩</span><span class="sxs-lookup"><span data-stu-id="4edad-140">External File trigger binding</span></span>

<span data-ttu-id="4edad-141">hello Azure 외부 파일 트리거를 사용 하 여 원격 폴더를 모니터링 하 고 변경 되 면 함수 코드를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4edad-141">hello Azure external file trigger lets you monitor a remote folder and run your function code when changes are detected.</span></span>

<span data-ttu-id="4edad-142">다음 JSON 개체에 hello hello를 사용 하는 hello 외부 파일 트리거 `bindings` function.json의 배열</span><span class="sxs-lookup"><span data-stu-id="4edad-142">hello external file trigger uses hello following JSON objects in hello `bindings` array of function.json</span></span>

```json
{
  "type": "apiHubFileTrigger",
  "name": "<Name of input parameter in function signature>",
  "direction": "in",
  "path": "<folder toomonitor, and optionally a name pattern - see below>",
  "connection": "<name of external file connection - see above>"
}
```
<!---
See one of hello following subheadings for more information:

* [Name patterns](#pattern)
* [File receipts](#receipts)
* [Handling poison files](#poison)
--->

<a name="pattern"></a>

### <a name="name-patterns"></a><span data-ttu-id="4edad-143">이름 패턴</span><span class="sxs-lookup"><span data-stu-id="4edad-143">Name patterns</span></span>
<span data-ttu-id="4edad-144">Hello에 파일 이름 패턴을 지정할 수 있습니다 `path` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="4edad-144">You can specify a file name pattern in hello `path` property.</span></span> <span data-ttu-id="4edad-145">참조 된 hello 폴더 hello SaaS 공급자에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4edad-145">hello folder referenced must exist in hello SaaS provider.</span></span>
<span data-ttu-id="4edad-146">예제:</span><span class="sxs-lookup"><span data-stu-id="4edad-146">Examples:</span></span>

```json
"path": "input/original-{name}",
```

<span data-ttu-id="4edad-147">이 경로 명명 된 파일을 찾을 *원래 File1.txt* hello에 *입력* 폴더 및 hello hello 값 `name` 함수 코드에서 변수 것 `File1.txt`합니다.</span><span class="sxs-lookup"><span data-stu-id="4edad-147">This path would find a file named *original-File1.txt* in hello *input* folder, and hello value of hello `name` variable in function code would be `File1.txt`.</span></span>

<span data-ttu-id="4edad-148">다른 예제:</span><span class="sxs-lookup"><span data-stu-id="4edad-148">Another example:</span></span>

```json
"path": "input/{filename}.{fileextension}",
```

<span data-ttu-id="4edad-149">이 경로 라는 파일을 찾을 수도 *원래 File1.txt*, 및의 hello hello 값 `filename` 및 `fileextension` 함수 코드에서 변수 것 *원래 File1* 및  *txt*합니다.</span><span class="sxs-lookup"><span data-stu-id="4edad-149">This path would also find a file named *original-File1.txt*, and hello value of hello `filename` and `fileextension` variables in function code would be *original-File1* and *txt*.</span></span>

<span data-ttu-id="4edad-150">Hello 파일 확장명에 대 한 고정된 값을 사용 하 여 hello 파일 형식의 파일을 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4edad-150">You can restrict hello file type of files by using a fixed value for hello file extension.</span></span> <span data-ttu-id="4edad-151">예:</span><span class="sxs-lookup"><span data-stu-id="4edad-151">For example:</span></span>

```json
"path": "samples/{name}.png",
```

<span data-ttu-id="4edad-152">이 경우만 *.png* hello에 대 한 파일 *샘플* 폴더 트리거 hello 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="4edad-152">In this case, only *.png* files in hello *samples* folder trigger hello function.</span></span>

<span data-ttu-id="4edad-153">중괄호는 이름 패턴에서 특수 문자입니다.</span><span class="sxs-lookup"><span data-stu-id="4edad-153">Curly braces are special characters in name patterns.</span></span> <span data-ttu-id="4edad-154">중괄호 hello 이름, 이중 hello 중괄호에에서 포함 된 toospecify 파일 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="4edad-154">toospecify file names that have curly braces in hello name, double hello curly braces.</span></span>
<span data-ttu-id="4edad-155">예:</span><span class="sxs-lookup"><span data-stu-id="4edad-155">For example:</span></span>

```json
"path": "images/{{20140101}}-{name}",
```

<span data-ttu-id="4edad-156">이 경로 명명 된 파일을 찾을 *{20140101}-soundfile.mp3* hello에 *이미지* 폴더 및 hello `name` 번호 hello 함수 코드에서 변수 값은 *soundfile.mp3*.</span><span class="sxs-lookup"><span data-stu-id="4edad-156">This path would find a file named *{20140101}-soundfile.mp3* in hello *images* folder, and hello `name` variable value in hello function code would be *soundfile.mp3*.</span></span>

<a name="receipts"></a>

<!--- ### File receipts
hello Azure Functions runtime makes sure that no external file trigger function gets called more than once for hello same new or updated file.
It does so by maintaining *file receipts* toodetermine if a given file version has been processed.

File receipts are stored in a folder named *azure-webjobs-hosts* in hello Azure storage account for your function app
(specified by hello `AzureWebJobsStorage` app setting). A file receipt has hello following information:

* hello triggered function ("*&lt;function app name>*.Functions.*&lt;function name>*", for example: "functionsf74b96f7.Functions.CopyFile")
* hello folder name
* hello file type ("BlockFile" or "PageFile")
* hello file name
* hello ETag (a file version identifier, for example: "0x8D1DC6E70A277EF")

tooforce reprocessing of a file, delete hello file receipt for that file from hello *azure-webjobs-hosts* folder manually.
--->
<a name="poison"></a>

### <a name="handling-poison-files"></a><span data-ttu-id="4edad-157">포이즌 파일 처리</span><span class="sxs-lookup"><span data-stu-id="4edad-157">Handling poison files</span></span>
<span data-ttu-id="4edad-158">외부 파일 트리거 함수가 실패 하면 Azure 함수 기본적으로 (hello 첫 번째 시도가 포함)에 대해 지정된 된 파일에의 한 too5 시간 해당 기능을 다시 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="4edad-158">When an external file trigger function fails, Azure Functions retries that function up too5 times by default (including hello first try) for a given file.</span></span>
<span data-ttu-id="4edad-159">함수 라는 메시지 tooa 저장소 큐 5 모든 시도 실패 하는 경우 추가 *webjobs-apihubtrigger-포이즌*합니다.</span><span class="sxs-lookup"><span data-stu-id="4edad-159">If all 5 tries fail, Functions adds a message tooa Storage queue named *webjobs-apihubtrigger-poison*.</span></span> <span data-ttu-id="4edad-160">포이즌 파일에 대 한 hello 큐 메시지는 hello 다음과 같은 속성을 포함 하는 JSON 개체:</span><span class="sxs-lookup"><span data-stu-id="4edad-160">hello queue message for poison files is a JSON object that contains hello following properties:</span></span>

* <span data-ttu-id="4edad-161">FunctionId (hello 형태로 표시  *&lt;함수 응용 프로그램 이름 >*합니다. 함수입니다.  *&lt;함수 이름 >*)</span><span class="sxs-lookup"><span data-stu-id="4edad-161">FunctionId (in hello format *&lt;function app name>*.Functions.*&lt;function name>*)</span></span>
* <span data-ttu-id="4edad-162">FileType</span><span class="sxs-lookup"><span data-stu-id="4edad-162">FileType</span></span>
* <span data-ttu-id="4edad-163">FolderName</span><span class="sxs-lookup"><span data-stu-id="4edad-163">FolderName</span></span>
* <span data-ttu-id="4edad-164">FileName</span><span class="sxs-lookup"><span data-stu-id="4edad-164">FileName</span></span>
* <span data-ttu-id="4edad-165">ETag(파일 버전 식별자, 예: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="4edad-165">ETag (a file version identifier, for example: "0x8D1DC6E70A277EF")</span></span>


<a name="triggerusage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="4edad-166">트리거 사용</span><span class="sxs-lookup"><span data-stu-id="4edad-166">Trigger usage</span></span>
<span data-ttu-id="4edad-167">C# 기능을 같은 프로그램 함수 서명에서 명명된 된 매개 변수를 사용 하 여 toohello 입력된 파일 데이터 바인딩할 `<T> <name>`합니다.</span><span class="sxs-lookup"><span data-stu-id="4edad-167">In C# functions, you bind toohello input file data by using a named parameter in your function signature, like `<T> <name>`.</span></span>
<span data-ttu-id="4edad-168">여기서 `T` hello 데이터 형식은 toodeserialize hello 데이터를 원하는 및 `paramName` hello 이름에 지정 된는 [JSON 트리거할](#trigger)합니다.</span><span class="sxs-lookup"><span data-stu-id="4edad-168">Where `T` is hello data type that you want toodeserialize hello data into, and `paramName` is hello name you specified in the [trigger JSON](#trigger).</span></span> <span data-ttu-id="4edad-169">에서는 Node.js 함수를 사용 하 여 hello 입력된 파일 데이터 액세스 `context.bindings.<name>`합니다.</span><span class="sxs-lookup"><span data-stu-id="4edad-169">In Node.js functions, you access hello input file data using `context.bindings.<name>`.</span></span>

<span data-ttu-id="4edad-170">hello 다음 형식 중 하나로 hello 파일을 deserialize 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4edad-170">hello file can be deserialized into any of hello following types:</span></span>

* <span data-ttu-id="4edad-171">모든 [개체](https://msdn.microsoft.com/library/system.object.aspx)는 JSON 직렬화된 파일 데이터에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="4edad-171">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized file data.</span></span>
  <span data-ttu-id="4edad-172">사용자 지정 입력된 형식을 선언 하는 경우 (예: `FooType`), Azure 함수에 지정 된 형식으로 toodeserialize hello JSON 데이터를 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="4edad-172">If you declare a custom input type (e.g. `FooType`), Azure Functions attempts toodeserialize hello JSON data into your specified type.</span></span>
* <span data-ttu-id="4edad-173">문자열은 텍스트 파일 데이터에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="4edad-173">String - useful for text file data.</span></span>

<span data-ttu-id="4edad-174">C# 기능을에서 형식에 따라 hello tooany을 바인딩할 수 있습니다 하 고 hello 함수 런타임에서 해당 형식을 사용 하 여 hello 파일 데이터를 deserialize 하려고 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="4edad-174">In C# functions, you can also bind tooany of hello following types, and hello Functions runtime attempts to deserialize hello file data using that type:</span></span>

* `string`
* `byte[]`
* `Stream`
* `StreamReader`
* `TextReader`

## <a name="trigger-sample"></a><span data-ttu-id="4edad-175">트리거 샘플</span><span class="sxs-lookup"><span data-stu-id="4edad-175">Trigger sample</span></span>
<span data-ttu-id="4edad-176">있다고 가정 하면 다음 function.json hello, 외부 파일 트리거를 정의 하는:</span><span class="sxs-lookup"><span data-stu-id="4edad-176">Suppose you have hello following function.json, that defines an external file trigger:</span></span>

```json
{
    "disabled": false,
    "bindings": [
        {
            "name": "myFile",
            "type": "apiHubFileTrigger",
            "direction": "in",
            "path": "samples-workitems",
            "connection": "<name of external file connection>"
        }
    ]
}
```

<span data-ttu-id="4edad-177">모니터링 되는 폴더로 toohello 추가 된 각 파일의 hello 내용을 기록 하는 hello 언어 관련 샘플을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="4edad-177">See hello language-specific sample that logs hello contents of each file that is added toohello monitored folder.</span></span>

* [<span data-ttu-id="4edad-178">C#</span><span class="sxs-lookup"><span data-stu-id="4edad-178">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="4edad-179">Node.JS</span><span class="sxs-lookup"><span data-stu-id="4edad-179">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-usage-in-c"></a><span data-ttu-id="4edad-180">C#에서 트리거 사용</span><span class="sxs-lookup"><span data-stu-id="4edad-180">Trigger usage in C#</span></span> #

```cs
public static void Run(string myFile, TraceWriter log)
{
    log.Info($"C# File trigger function processed: {myFile}");
}
```

<!--
<a name="triggerfsharp"></a>
### Trigger usage in F# ##
```fsharp

```
-->

<a name="triggernodejs"></a>

### <a name="trigger-usage-in-nodejs"></a><span data-ttu-id="4edad-181">Node.js에서 트리거 사용</span><span class="sxs-lookup"><span data-stu-id="4edad-181">Trigger usage in Node.js</span></span>

```javascript
module.exports = function(context) {
    context.log('Node.js File trigger function processed', context.bindings.myFile);
    context.done();
};
```

<a name="input"></a>

## <a name="external-file-input-binding"></a><span data-ttu-id="4edad-182">외부 파일 입력 바인딩</span><span class="sxs-lookup"><span data-stu-id="4edad-182">External File input binding</span></span>
<span data-ttu-id="4edad-183">hello Azure 외부 파일 입력된 바인딩을 통해 toouse를 함수에서 외부 폴더에서 파일을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4edad-183">hello Azure external file input binding enables you toouse a file from an external folder in your function.</span></span>

<span data-ttu-id="4edad-184">hello 외부 파일 입력된 tooa 함수 사용 하 여 다음 JSON 개체에 hello hello `bindings` function.json의 배열:</span><span class="sxs-lookup"><span data-stu-id="4edad-184">hello external file input tooa function uses hello following JSON objects in hello `bindings` array of function.json:</span></span>

```json
{
  "name": "<Name of input parameter in function signature>",
  "type": "apiHubFile",
  "direction": "in",
  "path": "<Path of input file - see below>",
  "connection": "<name of external file connection>"
},
```

<span data-ttu-id="4edad-185">참고 hello 다음.</span><span class="sxs-lookup"><span data-stu-id="4edad-185">Note hello following:</span></span>

* <span data-ttu-id="4edad-186">`path`hello 폴더 이름 및 hello 파일 이름을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4edad-186">`path` must contain hello folder name and hello file name.</span></span> <span data-ttu-id="4edad-187">예를 들어, 있는 경우는 [큐 트리거](functions-bindings-storage-queue.md) 함수에서 사용할 수 있습니다 `"path": "samples-workitems/{queueTrigger}"` hello에서 toopoint tooa 파일 `samples-workitems` hello 트리거 메시지에 지정 된 hello 파일 이름과 일치 하는 이름으로 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="4edad-187">For example, if you have a [queue trigger](functions-bindings-storage-queue.md) in your function, you can use `"path": "samples-workitems/{queueTrigger}"` toopoint tooa file in hello `samples-workitems` folder with a name that matches hello file name specified in hello trigger message.</span></span>   

<a name="inputusage"></a>

## <a name="input-usage"></a><span data-ttu-id="4edad-188">입력 사용</span><span class="sxs-lookup"><span data-stu-id="4edad-188">Input usage</span></span>
<span data-ttu-id="4edad-189">C# 기능을 같은 프로그램 함수 서명에서 명명된 된 매개 변수를 사용 하 여 toohello 입력된 파일 데이터 바인딩할 `<T> <name>`합니다.</span><span class="sxs-lookup"><span data-stu-id="4edad-189">In C# functions, you bind toohello input file data by using a named parameter in your function signature, like `<T> <name>`.</span></span>
<span data-ttu-id="4edad-190">여기서 `T` hello 데이터 형식은 toodeserialize hello 데이터를 지정 하 고 `paramName` hello 이름에 지정 된는 [입력 바인딩의](#input)합니다.</span><span class="sxs-lookup"><span data-stu-id="4edad-190">Where `T` is hello data type that you want toodeserialize hello data into, and `paramName` is hello name you specified in the [input binding](#input).</span></span> <span data-ttu-id="4edad-191">에서는 Node.js 함수를 사용 하 여 hello 입력된 파일 데이터 액세스 `context.bindings.<name>`합니다.</span><span class="sxs-lookup"><span data-stu-id="4edad-191">In Node.js functions, you access hello input file data using `context.bindings.<name>`.</span></span>

<span data-ttu-id="4edad-192">hello 다음 형식 중 하나로 hello 파일을 deserialize 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4edad-192">hello file can be deserialized into any of hello following types:</span></span>

* <span data-ttu-id="4edad-193">모든 [개체](https://msdn.microsoft.com/library/system.object.aspx)는 JSON 직렬화된 파일 데이터에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="4edad-193">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized file data.</span></span>
  <span data-ttu-id="4edad-194">사용자 지정 입력된 형식을 선언 하는 경우 (예: `InputType`), Azure 함수에 지정 된 형식으로 toodeserialize hello JSON 데이터를 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="4edad-194">If you declare a custom input type (e.g. `InputType`), Azure Functions attempts toodeserialize hello JSON data into your specified type.</span></span>
* <span data-ttu-id="4edad-195">문자열은 텍스트 파일 데이터에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="4edad-195">String - useful for text file data.</span></span>

<span data-ttu-id="4edad-196">C# 기능을에서 형식에 따라 hello tooany을 바인딩할 수 있습니다 하 고 hello 함수 런타임에서 해당 형식을 사용 하 여 hello 파일 데이터를 deserialize 하려고 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="4edad-196">In C# functions, you can also bind tooany of hello following types, and hello Functions runtime attempts to deserialize hello file data using that type:</span></span>

* `string`
* `byte[]`
* `Stream`
* `StreamReader`
* `TextReader`


<a name="output"></a>

## <a name="external-file-output-binding"></a><span data-ttu-id="4edad-197">외부 파일 출력 바인딩</span><span class="sxs-lookup"><span data-stu-id="4edad-197">External File output binding</span></span>
<span data-ttu-id="4edad-198">hello Azure 외부 파일 출력 바인딩을 통해 toowrite 파일 tooan 함수에서 외부 폴더 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4edad-198">hello Azure external file output binding enables you toowrite files tooan external folder in your function.</span></span>

<span data-ttu-id="4edad-199">다음 JSON 개체에 hello hello를 사용 하는 함수 출력 hello 외부 파일 `bindings` function.json의 배열:</span><span class="sxs-lookup"><span data-stu-id="4edad-199">hello external file output for a function uses hello following JSON objects in hello `bindings` array of function.json:</span></span>

```json
{
  "name": "<Name of output parameter in function signature>",
  "type": "apiHubFile",
  "direction": "out",
  "path": "<Path of input file - see below>",
  "connection": "<name of external file connection>"
}
```

<span data-ttu-id="4edad-200">참고 hello 다음.</span><span class="sxs-lookup"><span data-stu-id="4edad-200">Note hello following:</span></span>

* <span data-ttu-id="4edad-201">`path`hello 폴더 이름 및 hello 파일 이름 toowrite를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4edad-201">`path` must contain hello folder name and hello file name toowrite to.</span></span> <span data-ttu-id="4edad-202">예를 들어, 있는 경우는 [큐 트리거](functions-bindings-storage-queue.md) 함수에서 사용할 수 있습니다 `"path": "samples-workitems/{queueTrigger}"` hello에서 toopoint tooa 파일 `samples-workitems` hello 트리거 메시지에 지정 된 hello 파일 이름과 일치 하는 이름으로 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="4edad-202">For example, if you have a [queue trigger](functions-bindings-storage-queue.md) in your function, you can use `"path": "samples-workitems/{queueTrigger}"` toopoint tooa file in hello `samples-workitems` folder with a name that matches hello file name specified in hello trigger message.</span></span>   

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="4edad-203">출력 사용</span><span class="sxs-lookup"><span data-stu-id="4edad-203">Output usage</span></span>
<span data-ttu-id="4edad-204">C# 함수를 명명 된 hello를 사용 하 여 toohello 출력 파일 바인딩할 `out` 함수 시그니처의 매개 변수 같은 `out <T> <name>`여기서 `T` hello 데이터 형식은 tooserialize hello 데이터를 지정 하 고 `paramName` 는 hello 이름을 에 지정 된 된 [출력 바인딩이](#output)합니다.</span><span class="sxs-lookup"><span data-stu-id="4edad-204">In C# functions, you bind toohello output file by using hello named `out` parameter in your function signature, like `out <T> <name>`, where `T` is hello data type that you want tooserialize hello data into, and `paramName` is hello name you specified in the [output binding](#output).</span></span> <span data-ttu-id="4edad-205">에서는 Node.js 함수를 사용 하 여 hello 출력 파일 액세스 `context.bindings.<name>`합니다.</span><span class="sxs-lookup"><span data-stu-id="4edad-205">In Node.js functions, you access hello output file using `context.bindings.<name>`.</span></span>

<span data-ttu-id="4edad-206">유형만 hello를 사용 하 여 toohello 출력 파일을 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4edad-206">You can write toohello output file using any of hello following types:</span></span>

* <span data-ttu-id="4edad-207">모든 [개체](https://msdn.microsoft.com/library/system.object.aspx)는 JSON 직렬화에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="4edad-207">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialization.</span></span>
  <span data-ttu-id="4edad-208">사용자 지정 출력 형식을 선언 하는 경우 (예: `out OutputType paramName`), Azure 함수 tooserialize 개체를 JSON으로 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="4edad-208">If you declare a custom output type (e.g. `out OutputType paramName`), Azure Functions attempts tooserialize object into JSON.</span></span> <span data-ttu-id="4edad-209">Hello 함수가 종료 되 면 hello 출력 매개 변수가 null 이면 hello 함수 런타임 개체를 null로 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4edad-209">If hello output parameter is null when hello function exits, hello Functions runtime creates a file as a null object.</span></span>
* <span data-ttu-id="4edad-210">문자열(`out string paramName`)은 텍스트 파일 데이터에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="4edad-210">String - (`out string paramName`) useful for text file data.</span></span> <span data-ttu-id="4edad-211">hello 함수 런타임 hello 함수가 종료 되 면 문자열 매개 변수는 null이 아닌 경우에 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4edad-211">hello Functions runtime creates a file only if the string parameter is non-null when hello function exits.</span></span>

<span data-ttu-id="4edad-212">C# 함수에서의 hello 유형만 tooany를 출력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4edad-212">In C# functions you can also output tooany of hello following types:</span></span>

* `TextWriter`
* `Stream`
* `CloudFileStream`
* `ICloudFile`
* `CloudBlockFile`
* `CloudPageFile`

<a name="outputsample"></a>

<a name="sample"></a>

## <a name="input--output-sample"></a><span data-ttu-id="4edad-213">입력 + 출력 샘플</span><span class="sxs-lookup"><span data-stu-id="4edad-213">Input + Output sample</span></span>
<span data-ttu-id="4edad-214">정의 하는 hello function.json 다음 가정는 [저장소 큐 트리거](functions-bindings-storage-queue.md), 외부 파일 입력 및 출력 외부 파일:</span><span class="sxs-lookup"><span data-stu-id="4edad-214">Suppose you have hello following function.json, that defines a [Storage queue trigger](functions-bindings-storage-queue.md), an external file input, and an external file output:</span></span>

```json
{
  "bindings": [
    {
      "queueName": "myqueue-items",
      "connection": "MyStorageConnection",
      "name": "myQueueItem",
      "type": "queueTrigger",
      "direction": "in"
    },
    {
      "name": "myInputFile",
      "type": "apiHubFile",
      "path": "samples-workitems/{queueTrigger}",
      "connection": "<name of external file connection>",
      "direction": "in"
    },
    {
      "name": "myOutputFile",
      "type": "apiHubFile",
      "path": "samples-workitems/{queueTrigger}-Copy",
      "connection": "<name of external file connection>",
      "direction": "out"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="4edad-215">Hello 입력된 파일 toohello 출력 파일을 복사 하는 hello 언어 관련 샘플을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="4edad-215">See hello language-specific sample that copies hello input file toohello output file.</span></span>

* [<span data-ttu-id="4edad-216">C#</span><span class="sxs-lookup"><span data-stu-id="4edad-216">C#</span></span>](#incsharp)
* [<span data-ttu-id="4edad-217">Node.JS</span><span class="sxs-lookup"><span data-stu-id="4edad-217">Node.js</span></span>](#innodejs)

<a name="incsharp"></a>

### <a name="usage-in-c"></a><span data-ttu-id="4edad-218">C#에서 사용</span><span class="sxs-lookup"><span data-stu-id="4edad-218">Usage in C#</span></span> #

```cs
public static void Run(string myQueueItem, string myInputFile, out string myOutputFile, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    myOutputFile = myInputFile;
}
```

<!--
<a name="infsharp"></a>
### Input usage in F# ##
```fsharp

```
-->

<a name="innodejs"></a>

### <a name="usage-in-nodejs"></a><span data-ttu-id="4edad-219">Node.js에서 사용</span><span class="sxs-lookup"><span data-stu-id="4edad-219">Usage in Node.js</span></span>

```javascript
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputFile = context.bindings.myInputFile;
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="4edad-220">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4edad-220">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

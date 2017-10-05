---
title: "Azure Functions 외부 파일 바인딩(미리 보기) | Microsoft Docs"
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
ms.openlocfilehash: 2082e4e9b23271be93f3e3ab43997c3243238da8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-functions-external-file-bindings-preview"></a><span data-ttu-id="cb470-103">Azure Functions 외부 파일 바인딩(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="cb470-103">Azure Functions External File bindings (Preview)</span></span>
<span data-ttu-id="cb470-104">이 문서에서는 기본 제공 바인딩을 활용하는 사용자 함수 내에서 다양한 SaaS 공급자(예: OneDrive, Dropbox)의 파일을 조작하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cb470-104">This article shows how to manipulate files from different SaaS providers (e.g. OneDrive, Dropbox) within your function utilizing built-in bindings.</span></span> <span data-ttu-id="cb470-105">Azure Functions는 외부 파일에 대한 트리거, 입력 및 출력 바인딩을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="cb470-105">Azure functions supports trigger, input, and output bindings for external file.</span></span>

<span data-ttu-id="cb470-106">이 바인딩은 SaaS 공급자에 대한 API 연결을 만들거나 함수 앱의 리소스 그룹에서 기존 API 연결을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cb470-106">This binding creates API connections to SaaS providers, or uses existing API connections from your Function App's resource group.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="supported-file-connections"></a><span data-ttu-id="cb470-107">지원되는 파일 연결</span><span class="sxs-lookup"><span data-stu-id="cb470-107">Supported File connections</span></span>

|<span data-ttu-id="cb470-108">커넥터</span><span class="sxs-lookup"><span data-stu-id="cb470-108">Connector</span></span>|<span data-ttu-id="cb470-109">트리거</span><span class="sxs-lookup"><span data-stu-id="cb470-109">Trigger</span></span>|<span data-ttu-id="cb470-110">입력</span><span class="sxs-lookup"><span data-stu-id="cb470-110">Input</span></span>|<span data-ttu-id="cb470-111">출력</span><span class="sxs-lookup"><span data-stu-id="cb470-111">Output</span></span>|
|:-----|:---:|:---:|:---:|
|[<span data-ttu-id="cb470-112">Box</span><span class="sxs-lookup"><span data-stu-id="cb470-112">Box</span></span>](https://www.box.com)|<span data-ttu-id="cb470-113">x</span><span class="sxs-lookup"><span data-stu-id="cb470-113">x</span></span>|<span data-ttu-id="cb470-114">x</span><span class="sxs-lookup"><span data-stu-id="cb470-114">x</span></span>|<span data-ttu-id="cb470-115">x</span><span class="sxs-lookup"><span data-stu-id="cb470-115">x</span></span>
|[<span data-ttu-id="cb470-116">Dropbox</span><span class="sxs-lookup"><span data-stu-id="cb470-116">Dropbox</span></span>](https://www.dropbox.com)|<span data-ttu-id="cb470-117">x</span><span class="sxs-lookup"><span data-stu-id="cb470-117">x</span></span>|<span data-ttu-id="cb470-118">x</span><span class="sxs-lookup"><span data-stu-id="cb470-118">x</span></span>|<span data-ttu-id="cb470-119">x</span><span class="sxs-lookup"><span data-stu-id="cb470-119">x</span></span>
|[<span data-ttu-id="cb470-120">FTP</span><span class="sxs-lookup"><span data-stu-id="cb470-120">FTP</span></span>](https://docs.microsoft.com/azure/app-service-web/app-service-deploy-ftp)|<span data-ttu-id="cb470-121">x</span><span class="sxs-lookup"><span data-stu-id="cb470-121">x</span></span>|<span data-ttu-id="cb470-122">x</span><span class="sxs-lookup"><span data-stu-id="cb470-122">x</span></span>|<span data-ttu-id="cb470-123">x</span><span class="sxs-lookup"><span data-stu-id="cb470-123">x</span></span>
|[<span data-ttu-id="cb470-124">OneDrive</span><span class="sxs-lookup"><span data-stu-id="cb470-124">OneDrive</span></span>](https://onedrive.live.com)|<span data-ttu-id="cb470-125">x</span><span class="sxs-lookup"><span data-stu-id="cb470-125">x</span></span>|<span data-ttu-id="cb470-126">x</span><span class="sxs-lookup"><span data-stu-id="cb470-126">x</span></span>|<span data-ttu-id="cb470-127">x</span><span class="sxs-lookup"><span data-stu-id="cb470-127">x</span></span>
|[<span data-ttu-id="cb470-128">OneDrive for Business</span><span class="sxs-lookup"><span data-stu-id="cb470-128">OneDrive for Business</span></span>](https://onedrive.live.com/about/business/)|<span data-ttu-id="cb470-129">x</span><span class="sxs-lookup"><span data-stu-id="cb470-129">x</span></span>|<span data-ttu-id="cb470-130">x</span><span class="sxs-lookup"><span data-stu-id="cb470-130">x</span></span>|<span data-ttu-id="cb470-131">x</span><span class="sxs-lookup"><span data-stu-id="cb470-131">x</span></span>
|[<span data-ttu-id="cb470-132">SFTP</span><span class="sxs-lookup"><span data-stu-id="cb470-132">SFTP</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-sftp)|<span data-ttu-id="cb470-133">x</span><span class="sxs-lookup"><span data-stu-id="cb470-133">x</span></span>|<span data-ttu-id="cb470-134">x</span><span class="sxs-lookup"><span data-stu-id="cb470-134">x</span></span>|<span data-ttu-id="cb470-135">x</span><span class="sxs-lookup"><span data-stu-id="cb470-135">x</span></span>
|[<span data-ttu-id="cb470-136">Google 드라이브</span><span class="sxs-lookup"><span data-stu-id="cb470-136">Google Drive</span></span>](https://www.google.com/drive/)||<span data-ttu-id="cb470-137">x</span><span class="sxs-lookup"><span data-stu-id="cb470-137">x</span></span>|<span data-ttu-id="cb470-138">x</span><span class="sxs-lookup"><span data-stu-id="cb470-138">x</span></span>|

> [!NOTE]
> <span data-ttu-id="cb470-139">외부 파일 연결은 [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list)에서도 사용할 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="cb470-139">External File connections can also be used in [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list)</span></span>

## <a name="external-file-trigger-binding"></a><span data-ttu-id="cb470-140">외부 파일 트리거 바인딩</span><span class="sxs-lookup"><span data-stu-id="cb470-140">External File trigger binding</span></span>

<span data-ttu-id="cb470-141">Azure 외부 파일 트리거를 사용하면 원격 폴더를 모니터링하고 변경 사항이 감지될 때 함수 코드를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb470-141">The Azure external file trigger lets you monitor a remote folder and run your function code when changes are detected.</span></span>

<span data-ttu-id="cb470-142">외부 파일 트리거는 function.json의 `bindings` 배열에서 다음 JSON 개체를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cb470-142">The external file trigger uses the following JSON objects in the `bindings` array of function.json</span></span>

```json
{
  "type": "apiHubFileTrigger",
  "name": "<Name of input parameter in function signature>",
  "direction": "in",
  "path": "<folder to monitor, and optionally a name pattern - see below>",
  "connection": "<name of external file connection - see above>"
}
```
<!---
See one of the following subheadings for more information:

* [Name patterns](#pattern)
* [File receipts](#receipts)
* [Handling poison files](#poison)
--->

<a name="pattern"></a>

### <a name="name-patterns"></a><span data-ttu-id="cb470-143">이름 패턴</span><span class="sxs-lookup"><span data-stu-id="cb470-143">Name patterns</span></span>
<span data-ttu-id="cb470-144">`path` 속성에서 파일 이름 패턴을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb470-144">You can specify a file name pattern in the `path` property.</span></span> <span data-ttu-id="cb470-145">참조된 폴더는 SaaS 공급자에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb470-145">The folder referenced must exist in the SaaS provider.</span></span>
<span data-ttu-id="cb470-146">예제:</span><span class="sxs-lookup"><span data-stu-id="cb470-146">Examples:</span></span>

```json
"path": "input/original-{name}",
```

<span data-ttu-id="cb470-147">이 경로에는 *input* 폴더에서 *original-File1.txt*라는 파일이 있으며 함수 코드의 `name` 변수값은 `File1.txt`이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb470-147">This path would find a file named *original-File1.txt* in the *input* folder, and the value of the `name` variable in function code would be `File1.txt`.</span></span>

<span data-ttu-id="cb470-148">다른 예제:</span><span class="sxs-lookup"><span data-stu-id="cb470-148">Another example:</span></span>

```json
"path": "input/{filename}.{fileextension}",
```

<span data-ttu-id="cb470-149">또한 이 경로에는 *original-File1.txt*라는 파일이 있으며 함수 코드에 있는 `filename` 및 `fileextension` 변수값은 *original-File1* 및 *txt*입니다.</span><span class="sxs-lookup"><span data-stu-id="cb470-149">This path would also find a file named *original-File1.txt*, and the value of the `filename` and `fileextension` variables in function code would be *original-File1* and *txt*.</span></span>

<span data-ttu-id="cb470-150">파일 확장명에 고정된 값을 사용하여 파일의 파일 형식을 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb470-150">You can restrict the file type of files by using a fixed value for the file extension.</span></span> <span data-ttu-id="cb470-151">예:</span><span class="sxs-lookup"><span data-stu-id="cb470-151">For example:</span></span>

```json
"path": "samples/{name}.png",
```

<span data-ttu-id="cb470-152">이 경우 *samples* 폴더의 *.png* 파일만 함수를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="cb470-152">In this case, only *.png* files in the *samples* folder trigger the function.</span></span>

<span data-ttu-id="cb470-153">중괄호는 이름 패턴에서 특수 문자입니다.</span><span class="sxs-lookup"><span data-stu-id="cb470-153">Curly braces are special characters in name patterns.</span></span> <span data-ttu-id="cb470-154">이름에 중괄호가 있는 파일 이름을 지정하려면 이중 중괄호를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cb470-154">To specify file names that have curly braces in the name, double the curly braces.</span></span>
<span data-ttu-id="cb470-155">예:</span><span class="sxs-lookup"><span data-stu-id="cb470-155">For example:</span></span>

```json
"path": "images/{{20140101}}-{name}",
```

<span data-ttu-id="cb470-156">이 경로에는 *images* 폴더에 *{20140101}-soundfile.mp3*라는 파일이 있으며 함수 코드에 있는 `name` 변수값은 *soundfile.mp3*입니다.</span><span class="sxs-lookup"><span data-stu-id="cb470-156">This path would find a file named *{20140101}-soundfile.mp3* in the *images* folder, and the `name` variable value in the function code would be *soundfile.mp3*.</span></span>

<a name="receipts"></a>

<!--- ### File receipts
The Azure Functions runtime makes sure that no external file trigger function gets called more than once for the same new or updated file.
It does so by maintaining *file receipts* to determine if a given file version has been processed.

File receipts are stored in a folder named *azure-webjobs-hosts* in the Azure storage account for your function app
(specified by the `AzureWebJobsStorage` app setting). A file receipt has the following information:

* The triggered function ("*&lt;function app name>*.Functions.*&lt;function name>*", for example: "functionsf74b96f7.Functions.CopyFile")
* The folder name
* The file type ("BlockFile" or "PageFile")
* The file name
* The ETag (a file version identifier, for example: "0x8D1DC6E70A277EF")

To force reprocessing of a file, delete the file receipt for that file from the *azure-webjobs-hosts* folder manually.
--->
<a name="poison"></a>

### <a name="handling-poison-files"></a><span data-ttu-id="cb470-157">포이즌 파일 처리</span><span class="sxs-lookup"><span data-stu-id="cb470-157">Handling poison files</span></span>
<span data-ttu-id="cb470-158">외부 파일 트리거 함수가 실패하는 경우 Azure Functions는 해당 함수를 지정된 파일에 대해 기본적으로 최대 5번(첫 번째 시도 포함) 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="cb470-158">When an external file trigger function fails, Azure Functions retries that function up to 5 times by default (including the first try) for a given file.</span></span>
<span data-ttu-id="cb470-159">5번 모두 실패할 경우 Functions는 메시지를 *webjobs-apihubtrigger-poison*이라는 Storage 큐에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cb470-159">If all 5 tries fail, Functions adds a message to a Storage queue named *webjobs-apihubtrigger-poison*.</span></span> <span data-ttu-id="cb470-160">포이즌 파일에 대한 큐 메시지는 다음 속성을 포함하는 JSON 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="cb470-160">The queue message for poison files is a JSON object that contains the following properties:</span></span>

* <span data-ttu-id="cb470-161">FunctionId(형식에서 *&lt;함수 앱 이름>*.Functions.*&lt;함수 이름>*)</span><span class="sxs-lookup"><span data-stu-id="cb470-161">FunctionId (in the format *&lt;function app name>*.Functions.*&lt;function name>*)</span></span>
* <span data-ttu-id="cb470-162">FileType</span><span class="sxs-lookup"><span data-stu-id="cb470-162">FileType</span></span>
* <span data-ttu-id="cb470-163">FolderName</span><span class="sxs-lookup"><span data-stu-id="cb470-163">FolderName</span></span>
* <span data-ttu-id="cb470-164">FileName</span><span class="sxs-lookup"><span data-stu-id="cb470-164">FileName</span></span>
* <span data-ttu-id="cb470-165">ETag(파일 버전 식별자, 예: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="cb470-165">ETag (a file version identifier, for example: "0x8D1DC6E70A277EF")</span></span>


<a name="triggerusage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="cb470-166">트리거 사용</span><span class="sxs-lookup"><span data-stu-id="cb470-166">Trigger usage</span></span>
<span data-ttu-id="cb470-167">C# 함수에서 `<T> <name>`같은 함수 시그니처의 명명된 매개 변수를 사용하여 입력 파일 데이터를 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="cb470-167">In C# functions, you bind to the input file data by using a named parameter in your function signature, like `<T> <name>`.</span></span>
<span data-ttu-id="cb470-168">여기서 `T`는 데이터를 deserialize할 데이터 형식이며, `paramName`은 [JSON 트리거](#trigger)에서 사용자가 지정한 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="cb470-168">Where `T` is the data type that you want to deserialize the data into, and `paramName` is the name you specified in the [trigger JSON](#trigger).</span></span> <span data-ttu-id="cb470-169">Node.js 함수에서 `context.bindings.<name>`을 사용하여 입력 파일 데이터에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="cb470-169">In Node.js functions, you access the input file data using `context.bindings.<name>`.</span></span>

<span data-ttu-id="cb470-170">다음 중 원하는 형식으로 파일을 deserialize할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb470-170">The file can be deserialized into any of the following types:</span></span>

* <span data-ttu-id="cb470-171">모든 [개체](https://msdn.microsoft.com/library/system.object.aspx)는 JSON 직렬화된 파일 데이터에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="cb470-171">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized file data.</span></span>
  <span data-ttu-id="cb470-172">사용자 지정 입력 형식을 선언하는 경우(예: `FooType`), Azure Functions에서 지정된 형식에 JSON 데이터를 deserialize하려고 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="cb470-172">If you declare a custom input type (e.g. `FooType`), Azure Functions attempts to deserialize the JSON data into your specified type.</span></span>
* <span data-ttu-id="cb470-173">문자열은 텍스트 파일 데이터에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="cb470-173">String - useful for text file data.</span></span>

<span data-ttu-id="cb470-174">C# 함수에서 다음 형식 중 하나에 바인딩할 수도 있으며, Functions 런타임이 해당 형식을 사용하여 파일 데이터를 deserialize하려고 시도하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb470-174">In C# functions, you can also bind to any of the following types, and the Functions runtime attempts to deserialize the file data using that type:</span></span>

* `string`
* `byte[]`
* `Stream`
* `StreamReader`
* `TextReader`

## <a name="trigger-sample"></a><span data-ttu-id="cb470-175">트리거 샘플</span><span class="sxs-lookup"><span data-stu-id="cb470-175">Trigger sample</span></span>
<span data-ttu-id="cb470-176">외부 파일 트리거를 정의하는 다음과 같은 function.json이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="cb470-176">Suppose you have the following function.json, that defines an external file trigger:</span></span>

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

<span data-ttu-id="cb470-177">모니터링되는 폴더에 추가된 각 파일의 콘텐츠를 기록하는 언어별 샘플을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cb470-177">See the language-specific sample that logs the contents of each file that is added to the monitored folder.</span></span>

* [<span data-ttu-id="cb470-178">C#</span><span class="sxs-lookup"><span data-stu-id="cb470-178">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="cb470-179">Node.JS</span><span class="sxs-lookup"><span data-stu-id="cb470-179">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-usage-in-c"></a><span data-ttu-id="cb470-180">C#에서 트리거 사용</span><span class="sxs-lookup"><span data-stu-id="cb470-180">Trigger usage in C#</span></span> #

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

### <a name="trigger-usage-in-nodejs"></a><span data-ttu-id="cb470-181">Node.js에서 트리거 사용</span><span class="sxs-lookup"><span data-stu-id="cb470-181">Trigger usage in Node.js</span></span>

```javascript
module.exports = function(context) {
    context.log('Node.js File trigger function processed', context.bindings.myFile);
    context.done();
};
```

<a name="input"></a>

## <a name="external-file-input-binding"></a><span data-ttu-id="cb470-182">외부 파일 입력 바인딩</span><span class="sxs-lookup"><span data-stu-id="cb470-182">External File input binding</span></span>
<span data-ttu-id="cb470-183">Azure 외부 파일 입력 바인딩을 사용하면 함수에 외부 폴더의 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb470-183">The Azure external file input binding enables you to use a file from an external folder in your function.</span></span>

<span data-ttu-id="cb470-184">함수에 대한 외부 파일 입력은 function.json의 `bindings` 배열에서 다음과 같은 JSON 개체를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cb470-184">The external file input to a function uses the following JSON objects in the `bindings` array of function.json:</span></span>

```json
{
  "name": "<Name of input parameter in function signature>",
  "type": "apiHubFile",
  "direction": "in",
  "path": "<Path of input file - see below>",
  "connection": "<name of external file connection>"
},
```

<span data-ttu-id="cb470-185">다음 사항에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="cb470-185">Note the following:</span></span>

* <span data-ttu-id="cb470-186">`path`에는 폴더 이름과 파일 이름이 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb470-186">`path` must contain the folder name and the file name.</span></span> <span data-ttu-id="cb470-187">예를 들어 함수에 하나의 [큐 트리거](functions-bindings-storage-queue.md)가 있는 경우 `"path": "samples-workitems/{queueTrigger}"`를 사용하여 `samples-workitems` 폴더에서 트리거 메시지에 지정된 파일 이름과 일치하는 이름을 가진 파일을 가리킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb470-187">For example, if you have a [queue trigger](functions-bindings-storage-queue.md) in your function, you can use `"path": "samples-workitems/{queueTrigger}"` to point to a file in the `samples-workitems` folder with a name that matches the file name specified in the trigger message.</span></span>   

<a name="inputusage"></a>

## <a name="input-usage"></a><span data-ttu-id="cb470-188">입력 사용</span><span class="sxs-lookup"><span data-stu-id="cb470-188">Input usage</span></span>
<span data-ttu-id="cb470-189">C# 함수에서 `<T> <name>`같은 함수 시그니처의 명명된 매개 변수를 사용하여 입력 파일 데이터를 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="cb470-189">In C# functions, you bind to the input file data by using a named parameter in your function signature, like `<T> <name>`.</span></span>
<span data-ttu-id="cb470-190">여기서 `T`는 데이터를 deserialize할 데이터 형식이며, `paramName`은 [입력 바인딩](#input)에서 사용자가 지정한 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="cb470-190">Where `T` is the data type that you want to deserialize the data into, and `paramName` is the name you specified in the [input binding](#input).</span></span> <span data-ttu-id="cb470-191">Node.js 함수에서 `context.bindings.<name>`을 사용하여 입력 파일 데이터에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="cb470-191">In Node.js functions, you access the input file data using `context.bindings.<name>`.</span></span>

<span data-ttu-id="cb470-192">다음 중 원하는 형식으로 파일을 deserialize할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb470-192">The file can be deserialized into any of the following types:</span></span>

* <span data-ttu-id="cb470-193">모든 [개체](https://msdn.microsoft.com/library/system.object.aspx)는 JSON 직렬화된 파일 데이터에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="cb470-193">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized file data.</span></span>
  <span data-ttu-id="cb470-194">사용자 지정 입력 형식을 선언하는 경우(예: `InputType`), Azure Functions에서 지정된 형식에 JSON 데이터를 deserialize하려고 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="cb470-194">If you declare a custom input type (e.g. `InputType`), Azure Functions attempts to deserialize the JSON data into your specified type.</span></span>
* <span data-ttu-id="cb470-195">문자열은 텍스트 파일 데이터에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="cb470-195">String - useful for text file data.</span></span>

<span data-ttu-id="cb470-196">C# 함수에서 다음 형식 중 하나에 바인딩할 수도 있으며, Functions 런타임이 해당 형식을 사용하여 파일 데이터를 deserialize하려고 시도하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb470-196">In C# functions, you can also bind to any of the following types, and the Functions runtime attempts to deserialize the file data using that type:</span></span>

* `string`
* `byte[]`
* `Stream`
* `StreamReader`
* `TextReader`


<a name="output"></a>

## <a name="external-file-output-binding"></a><span data-ttu-id="cb470-197">외부 파일 출력 바인딩</span><span class="sxs-lookup"><span data-stu-id="cb470-197">External File output binding</span></span>
<span data-ttu-id="cb470-198">Azure 외부 파일 출력 바인딩을 사용하면 함수에 외부 폴더에 대한 파일을 쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb470-198">The Azure external file output binding enables you to write files to an external folder in your function.</span></span>

<span data-ttu-id="cb470-199">함수에 대한 외부 파일 출력은 function.json의 `bindings` 배열에서 다음과 같은 JSON 개체를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cb470-199">The external file output for a function uses the following JSON objects in the `bindings` array of function.json:</span></span>

```json
{
  "name": "<Name of output parameter in function signature>",
  "type": "apiHubFile",
  "direction": "out",
  "path": "<Path of input file - see below>",
  "connection": "<name of external file connection>"
}
```

<span data-ttu-id="cb470-200">다음 사항에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="cb470-200">Note the following:</span></span>

* <span data-ttu-id="cb470-201">`path`에는 쓸 수 있는 폴더 이름과 파일 이름이 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb470-201">`path` must contain the folder name and the file name to write to.</span></span> <span data-ttu-id="cb470-202">예를 들어 함수에 하나의 [큐 트리거](functions-bindings-storage-queue.md)가 있는 경우 `"path": "samples-workitems/{queueTrigger}"`를 사용하여 `samples-workitems` 폴더에서 트리거 메시지에 지정된 파일 이름과 일치하는 이름을 가진 파일을 가리킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb470-202">For example, if you have a [queue trigger](functions-bindings-storage-queue.md) in your function, you can use `"path": "samples-workitems/{queueTrigger}"` to point to a file in the `samples-workitems` folder with a name that matches the file name specified in the trigger message.</span></span>   

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="cb470-203">출력 사용</span><span class="sxs-lookup"><span data-stu-id="cb470-203">Output usage</span></span>
<span data-ttu-id="cb470-204">C# 함수에서 `out <T> <name>`같은 함수 시그니처의 명명된 `out` 매개 변수를 사용하여 출력 파일을 바인딩합니다. 여기서 `T`는 데이터를 serialize하려는 데이터 형식이며, `paramName`은 [출력 바인딩](#output)에서 사용자가 지정한 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="cb470-204">In C# functions, you bind to the output file by using the named `out` parameter in your function signature, like `out <T> <name>`, where `T` is the data type that you want to serialize the data into, and `paramName` is the name you specified in the [output binding](#output).</span></span> <span data-ttu-id="cb470-205">Node.js 함수에서 `context.bindings.<name>`을 사용하여 출력 파일 데이터에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="cb470-205">In Node.js functions, you access the output file using `context.bindings.<name>`.</span></span>

<span data-ttu-id="cb470-206">다음 형식 중 하나를 사용하여 출력 파일을 쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb470-206">You can write to the output file using any of the following types:</span></span>

* <span data-ttu-id="cb470-207">모든 [개체](https://msdn.microsoft.com/library/system.object.aspx)는 JSON 직렬화에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="cb470-207">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialization.</span></span>
  <span data-ttu-id="cb470-208">사용자 지정 출력 형식을 선언하는 경우(예: `out OutputType paramName`), Azure Functions에서 개체를 JSON으로 직렬화하려고 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="cb470-208">If you declare a custom output type (e.g. `out OutputType paramName`), Azure Functions attempts to serialize object into JSON.</span></span> <span data-ttu-id="cb470-209">함수가 종료될 때 출력 매개 변수가 null이면 Functions 런타임은 파일을 null 개체로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cb470-209">If the output parameter is null when the function exits, the Functions runtime creates a file as a null object.</span></span>
* <span data-ttu-id="cb470-210">문자열(`out string paramName`)은 텍스트 파일 데이터에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="cb470-210">String - (`out string paramName`) useful for text file data.</span></span> <span data-ttu-id="cb470-211">Functions 런타임은 함수가 종료될 때 문자열 매개 변수가 null이 아닌 경우에만 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="cb470-211">the Functions runtime creates a file only if the string parameter is non-null when the function exits.</span></span>

<span data-ttu-id="cb470-212">C# 함수에서 다음 중 원하는 형식으로 출력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb470-212">In C# functions you can also output to any of the following types:</span></span>

* `TextWriter`
* `Stream`
* `CloudFileStream`
* `ICloudFile`
* `CloudBlockFile`
* `CloudPageFile`

<a name="outputsample"></a>

<a name="sample"></a>

## <a name="input--output-sample"></a><span data-ttu-id="cb470-213">입력 + 출력 샘플</span><span class="sxs-lookup"><span data-stu-id="cb470-213">Input + Output sample</span></span>
<span data-ttu-id="cb470-214">다음과 같이 [Storage 큐 트리거](functions-bindings-storage-queue.md), n개의 외부 파일 입력, 외부 파일 출력을 정의하는 function.json이 있는 경우를 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="cb470-214">Suppose you have the following function.json, that defines a [Storage queue trigger](functions-bindings-storage-queue.md), an external file input, and an external file output:</span></span>

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

<span data-ttu-id="cb470-215">입력 파일을 출력 파일로 복사하는 언어별 샘플을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cb470-215">See the language-specific sample that copies the input file to the output file.</span></span>

* [<span data-ttu-id="cb470-216">C#</span><span class="sxs-lookup"><span data-stu-id="cb470-216">C#</span></span>](#incsharp)
* [<span data-ttu-id="cb470-217">Node.JS</span><span class="sxs-lookup"><span data-stu-id="cb470-217">Node.js</span></span>](#innodejs)

<a name="incsharp"></a>

### <a name="usage-in-c"></a><span data-ttu-id="cb470-218">C#에서 사용</span><span class="sxs-lookup"><span data-stu-id="cb470-218">Usage in C#</span></span> #

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

### <a name="usage-in-nodejs"></a><span data-ttu-id="cb470-219">Node.js에서 사용</span><span class="sxs-lookup"><span data-stu-id="cb470-219">Usage in Node.js</span></span>

```javascript
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputFile = context.bindings.myInputFile;
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="cb470-220">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cb470-220">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

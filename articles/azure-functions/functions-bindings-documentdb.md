---
title: "Azure Functions Cosmos DB 바인딩 | Microsoft Docs"
description: "Azure Functions에서 Azure Cosmos DB 바인딩을 사용하는 방법을 파악합니다."
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: "Azure Functions, 함수, 이벤트 처리, 동적 계산, 서버를 사용하지 않는 아키텍처"
ms.assetid: 3d8497f0-21f3-437d-ba24-5ece8c90ac85
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 04/18/2016
ms.author: glenga
ms.openlocfilehash: de95b0591eb95e76dbb7ba2382e9e14e1f66cda1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-cosmos-db-bindings"></a><span data-ttu-id="3b60a-104">Azure Functions Cosmos DB 바인딩</span><span class="sxs-lookup"><span data-stu-id="3b60a-104">Azure Functions Cosmos DB bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="3b60a-105">이 문서에서는 Azure Functions에서 Azure Cosmos DB 바인딩을 구성하고 코딩하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3b60a-105">This article explains how to configure and code Azure Cosmos DB bindings in Azure Functions.</span></span> <span data-ttu-id="3b60a-106">Azure Functions는 Cosmos DB에 대한 입력 및 출력 바인딩을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3b60a-106">Azure Functions supports input and output bindings for Cosmos DB.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="3b60a-107">Cosmos DB에 대한 자세한 내용은 [Cosmos DB 소개](../documentdb/documentdb-introduction.md) 및 [Cosmos DB 콘솔 응용 프로그램 빌드](../documentdb/documentdb-get-started.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b60a-107">For more information on Cosmos DB, see [Introduction to Cosmos DB](../documentdb/documentdb-introduction.md) and [Build a Cosmos DB console application](../documentdb/documentdb-get-started.md).</span></span>

<a id="docdbinput"></a>

## <a name="documentdb-api-input-binding"></a><span data-ttu-id="3b60a-108">DocumentDB API 입력 바인딩</span><span class="sxs-lookup"><span data-stu-id="3b60a-108">DocumentDB API input binding</span></span>
<span data-ttu-id="3b60a-109">DocumentDB API 입력 바인딩은 Cosmos DB 문서를 검색하고 함수의 명명된 입력 매개 변수를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="3b60a-109">The DocumentDB API input binding retrieves a Cosmos DB document and passes it to the named input parameter of the function.</span></span> <span data-ttu-id="3b60a-110">함수를 호출한 트리거에 따라 문서 ID를 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b60a-110">The document ID can be determined based on the trigger that invokes the function.</span></span> 

<span data-ttu-id="3b60a-111">DocumentDB API 입력 바인딩은 *function.json*에 다음 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b60a-111">The DocumentDB API input binding has the following properties in *function.json*:</span></span>

- <span data-ttu-id="3b60a-112">`name` : 문서에 대한 함수 코드에 사용되는 식별자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b60a-112">`name` : Identifier name used in function code for the document</span></span>
- <span data-ttu-id="3b60a-113">`type` : “documentdb”로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b60a-113">`type` : must be set to "documentdb"</span></span>
- <span data-ttu-id="3b60a-114">`databaseName` : 문서를 포함하는 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="3b60a-114">`databaseName` : The database containing the document</span></span>
- <span data-ttu-id="3b60a-115">`collectionName` : 문서를 포함하는 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="3b60a-115">`collectionName` : The collection containing the document</span></span>
- <span data-ttu-id="3b60a-116">`id` : 검색할 문서의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="3b60a-116">`id` : The Id of the document to retrieve.</span></span> <span data-ttu-id="3b60a-117">이 속성은 바인딩 매개 변수를 지원합니다. [Azure Functions 트리거 및 바인딩 개념](functions-triggers-bindings.md) 문서에서 [바인딩 식에서 사용자 지정 입력 속성에 바인딩](functions-triggers-bindings.md#bind-to-custom-input-properties-in-a-binding-expression)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b60a-117">This property supports bindings parameters; see [Bind to custom input properties in a binding expression](functions-triggers-bindings.md#bind-to-custom-input-properties-in-a-binding-expression) in the article [Azure Functions triggers and bindings concepts](functions-triggers-bindings.md).</span></span>
- <span data-ttu-id="3b60a-118">`sqlQuery`: 여러 문서를 검색하는 데 사용되는 Cosmos DB SQL 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="3b60a-118">`sqlQuery` : A Cosmos DB SQL query used for retrieving multiple documents.</span></span> <span data-ttu-id="3b60a-119">쿼리는 런타임 바인딩을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3b60a-119">The query supports runtime bindings.</span></span> <span data-ttu-id="3b60a-120">예: `SELECT * FROM c where c.departmentId = {departmentId}`</span><span class="sxs-lookup"><span data-stu-id="3b60a-120">For example: `SELECT * FROM c where c.departmentId = {departmentId}`</span></span>
- <span data-ttu-id="3b60a-121">`connection`: Cosmos DB 연결 문자열을 포함하는 앱 설정의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b60a-121">`connection` : The name of the app setting containing your Cosmos DB connection string</span></span>
- <span data-ttu-id="3b60a-122">`direction` : `"in"`으로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b60a-122">`direction`  : must be set to `"in"`.</span></span>

<span data-ttu-id="3b60a-123">속성 `id` 및 `sqlQuery`를 둘 다 지정할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3b60a-123">The properties `id` and `sqlQuery` cannot both be specified.</span></span> <span data-ttu-id="3b60a-124">`id` 및 `sqlQuery`를 둘 다 설정하지 않으면 전체 컬렉션이 검색됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b60a-124">If neither `id` nor `sqlQuery` is set, the entire collection is retrieved.</span></span>

## <a name="using-a-documentdb-api-input-binding"></a><span data-ttu-id="3b60a-125">DocumentDB API 입력 바인딩 사용</span><span class="sxs-lookup"><span data-stu-id="3b60a-125">Using a DocumentDB API input binding</span></span>

* <span data-ttu-id="3b60a-126">C# 및 F# 함수에서 함수가 성공적으로 종료되면 명명된 입력 매개 변수를 통해 입력 문서에 변경한 내용이 자동으로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b60a-126">In C# and F# functions, when the function exits successfully, any changes made to the input document via named input parameters are automatically persisted.</span></span> 
* <span data-ttu-id="3b60a-127">JavaScript 함수에서는 함수 종료 시 자동으로 업데이트되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3b60a-127">In JavaScript functions, updates are not made automatically upon function exit.</span></span> <span data-ttu-id="3b60a-128">대신 `context.bindings.<documentName>In` 및 `context.bindings.<documentName>Out`을 사용하여 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="3b60a-128">Instead, use `context.bindings.<documentName>In` and `context.bindings.<documentName>Out` to make updates.</span></span> <span data-ttu-id="3b60a-129">[JavaScript 샘플](#injavascript)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b60a-129">See the [JavaScript sample](#injavascript).</span></span>

<a name="inputsample"></a>

## <a name="input-sample-for-single-document"></a><span data-ttu-id="3b60a-130">단일 문서에 대한 입력 샘플</span><span class="sxs-lookup"><span data-stu-id="3b60a-130">Input sample for single document</span></span>
<span data-ttu-id="3b60a-131">function.json의 `bindings` 배열에 다음과 같은 DocumentDB API 입력 바인딩이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b60a-131">Suppose you have the following DocumentDB API input binding in the `bindings` array of function.json:</span></span>

```json
{
  "name": "inputDocument",
  "type": "documentDB",
  "databaseName": "MyDatabase",
  "collectionName": "MyCollection",
  "id" : "{queueTrigger}",
  "connection": "MyAccount_COSMOSDB",     
  "direction": "in"
}
```

<span data-ttu-id="3b60a-132">이 입력 바인딩을 사용하여 문서의 텍스트 값을 업데이트하는 언어별 샘플을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b60a-132">See the language-specific sample that uses this input binding to update the document's text value.</span></span>

* [<span data-ttu-id="3b60a-133">C#</span><span class="sxs-lookup"><span data-stu-id="3b60a-133">C#</span></span>](#incsharp)
* [<span data-ttu-id="3b60a-134">F#</span><span class="sxs-lookup"><span data-stu-id="3b60a-134">F#</span></span>](#infsharp)
* [<span data-ttu-id="3b60a-135">JavaScript</span><span class="sxs-lookup"><span data-stu-id="3b60a-135">JavaScript</span></span>](#injavascript)

<a name="incsharp"></a>
### <a name="input-sample-in-c"></a><span data-ttu-id="3b60a-136">C#의 입력 샘플</span><span class="sxs-lookup"><span data-stu-id="3b60a-136">Input sample in C#</span></span> #

```cs
// Change input document contents using DocumentDB API input binding 
public static void Run(string myQueueItem, dynamic inputDocument)
{   
  inputDocument.text = "This has changed.";
}
```
<a name="infsharp"></a>

### <a name="input-sample-in-f"></a><span data-ttu-id="3b60a-137">F#의 입력 샘플</span><span class="sxs-lookup"><span data-stu-id="3b60a-137">Input sample in F#</span></span> #

```fsharp
(* Change input document contents using DocumentDB API input binding *)
open FSharp.Interop.Dynamic
let Run(myQueueItem: string, inputDocument: obj) =
  inputDocument?text <- "This has changed."
```

<span data-ttu-id="3b60a-138">이 샘플에는 `FSharp.Interop.Dynamic` 및 `Dynamitey` NuGet 종속성을 지정하는 `project.json` 파일이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3b60a-138">This sample requires a `project.json` file that specifies the `FSharp.Interop.Dynamic` and `Dynamitey` NuGet dependencies:</span></span>

```json
{
  "frameworks": {
    "net46": {
      "dependencies": {
        "Dynamitey": "1.0.2",
        "FSharp.Interop.Dynamic": "3.0.0"
      }
    }
  }
}
```

<span data-ttu-id="3b60a-139">`project.json` 파일을 추가하려면 [F# 패키지 관리](functions-reference-fsharp.md#package)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b60a-139">To add a `project.json` file, see [F# package management](functions-reference-fsharp.md#package).</span></span>

<a name="injavascript"></a>

### <a name="input-sample-in-javascript"></a><span data-ttu-id="3b60a-140">JavaScript의 입력 샘플</span><span class="sxs-lookup"><span data-stu-id="3b60a-140">Input sample in JavaScript</span></span>

```javascript
// Change input document contents using DocumentDB API input binding, using context.bindings.inputDocumentOut
module.exports = function (context) {   
  context.bindings.inputDocumentOut = context.bindings.inputDocumentIn;
  context.bindings.inputDocumentOut.text = "This was updated!";
  context.done();
};
```

## <a name="input-sample-with-multiple-documents"></a><span data-ttu-id="3b60a-141">여러 문서가 있는 입력 샘플</span><span class="sxs-lookup"><span data-stu-id="3b60a-141">Input sample with multiple documents</span></span>

<span data-ttu-id="3b60a-142">SQL 쿼리로 지정된 여러 문서를 검색하려고 하며 큐 트리거를 사용하여 쿼리 매개 변수를 사용자 지정한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b60a-142">Suppose that you wish to retrieve multiple documents specified by a SQL query, using a queue trigger to customize the query parameters.</span></span> 

<span data-ttu-id="3b60a-143">이 예제에서 큐 트리거는 매개 변수 `departmentId`를 제공합니다. 큐 메시지 `{ "departmentId" : "Finance" }`는 재무 부서에 대한 모든 레코드를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="3b60a-143">In this example, the queue trigger provides a parameter `departmentId`.A queue message of `{ "departmentId" : "Finance" }` would return all records for the finance department.</span></span> <span data-ttu-id="3b60a-144">*function.json*에서 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3b60a-144">Use the following in *function.json*:</span></span>

```
{
    "name": "documents",
    "type": "documentdb",
    "direction": "in",
    "databaseName": "MyDb",
    "collectionName": "MyCollection",
    "sqlQuery": "SELECT * from c where c.departmentId = {departmentId}"
    "connection": "CosmosDBConnection"
}
```

### <a name="input-sample-with-multiple-documents-in-c"></a><span data-ttu-id="3b60a-145">C#으로 작성된 여러 문서가 있는 입력 샘플</span><span class="sxs-lookup"><span data-stu-id="3b60a-145">Input sample with multiple documents in C#</span></span>

```csharp
public static void Run(QueuePayload myQueueItem, IEnumerable<dynamic> documents)
{   
    foreach (var doc in documents)
    {
        // operate on each document
    }    
}

public class QueuePayload
{
    public string departmentId { get; set; }
}
```

### <a name="input-sample-with-multiple-documents-in-javascript"></a><span data-ttu-id="3b60a-146">JavaScript로 작성된 여러 문서가 있는 입력 샘플</span><span class="sxs-lookup"><span data-stu-id="3b60a-146">Input sample with multiple documents in JavaScript</span></span>

```javascript
module.exports = function (context, input) {    
    var documents = context.bindings.documents;
    for (var i = 0; i < documents.length; i++) {
        var document = documents[i];
        // operate on each document
    }       
    context.done();
};
```

## <span data-ttu-id="3b60a-147"><a id="docdboutput"></a>DocumentDB API 출력 바인딩</span><span class="sxs-lookup"><span data-stu-id="3b60a-147"><a id="docdboutput"></a>DocumentDB API output binding</span></span>
<span data-ttu-id="3b60a-148">DocumentDB API 출력 바인딩을 사용하면 Azure Cosmos DB 데이터베이스에 새 문서를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b60a-148">The DocumentDB API output binding lets you write a new document to an Azure Cosmos DB database.</span></span> <span data-ttu-id="3b60a-149">*function.json*에 다음 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b60a-149">It has the following properties in *function.json*:</span></span>

- <span data-ttu-id="3b60a-150">`name` : 새 문서에 대한 함수 코드에 사용되는 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="3b60a-150">`name` : Identifier used in function code for the new document</span></span>
- <span data-ttu-id="3b60a-151">`type` : `"documentdb"`로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b60a-151">`type` : must be set to `"documentdb"`</span></span>
- <span data-ttu-id="3b60a-152">`databaseName` : 새 문서를 만들 컬렉션을 포함하는 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="3b60a-152">`databaseName` : The database containing the collection where the new document will be created.</span></span>
- <span data-ttu-id="3b60a-153">`collectionName` : 새 문서를 만들 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="3b60a-153">`collectionName` : The collection where the new document will be created.</span></span>
- <span data-ttu-id="3b60a-154">`createIfNotExists` : 컬렉션이 존재하지 않는 경우 만들 수 있는지 여부를 나타내는 부울 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3b60a-154">`createIfNotExists` : A boolean value to indicate whether the collection will be created if it does not exist.</span></span> <span data-ttu-id="3b60a-155">기본값은 *false*입니다.</span><span class="sxs-lookup"><span data-stu-id="3b60a-155">The default is *false*.</span></span> <span data-ttu-id="3b60a-156">새 컬렉션이 예약된 처리량을 사용하여 만들어지면 가격 책정 면에서 의미하는 바가 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="3b60a-156">The reason for this is new collections are created with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="3b60a-157">자세한 내용은 [가격 책정 페이지](https://azure.microsoft.com/pricing/details/documentdb/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b60a-157">For more details, please visit the [pricing page](https://azure.microsoft.com/pricing/details/documentdb/).</span></span>
- <span data-ttu-id="3b60a-158">`connection`: Cosmos DB 연결 문자열을 포함하는 앱 설정의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b60a-158">`connection` : The name of the app setting containing your Cosmos DB connection string</span></span>
- <span data-ttu-id="3b60a-159">`direction` : `"out"`으로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b60a-159">`direction` : must be set to `"out"`</span></span>

## <a name="using-a-documentdb-api-output-binding"></a><span data-ttu-id="3b60a-160">DocumentDB API 출력 바인딩 사용</span><span class="sxs-lookup"><span data-stu-id="3b60a-160">Using a DocumentDB API output binding</span></span>
<span data-ttu-id="3b60a-161">이 섹션에서는 함수 코드에서 DocumentDB API 출력 바인딩을 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3b60a-161">This section shows you how to use your DocumentDB API output binding in your function code.</span></span>

<span data-ttu-id="3b60a-162">함수에서 출력 매개 변수를 작성하는 경우 기본적으로 새 문서는 사용자의 데이터베이스에 생성되며, 자동으로 생성된 GUID를 문서 ID로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3b60a-162">When you write to the output parameter in your function, by default a new document is generated in your database, with an automatically generated GUID as the document ID.</span></span> <span data-ttu-id="3b60a-163">출력 매개 변수의 `id` JSON 속성을 지정하여 출력 문서의 문서 ID를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b60a-163">You can specify the document ID of output document by specifying the `id` JSON property in the output parameter.</span></span> 

>[!Note]  
><span data-ttu-id="3b60a-164">기존 문서의 ID를 지정하면 새 출력 문서에 의해 덮어쓰여집니다.</span><span class="sxs-lookup"><span data-stu-id="3b60a-164">When you specify the ID of an existing document, it gets overwritten by the new output document.</span></span> 

<span data-ttu-id="3b60a-165">여러 문서를 출력하기 위해 `ICollector<T>` 또는 `IAsyncCollector<T>`에 바인딩할 수 있으며, 여기서 `T`는 지원되는 형식 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="3b60a-165">To output multiple documents, you can also bind to `ICollector<T>` or `IAsyncCollector<T>` where `T` is one of the supported types.</span></span>

<a name="outputsample"></a>

## <a name="documentdb-api-output-binding-sample"></a><span data-ttu-id="3b60a-166">DocumentDB API 출력 바인딩 샘플</span><span class="sxs-lookup"><span data-stu-id="3b60a-166">DocumentDB API output binding sample</span></span>
<span data-ttu-id="3b60a-167">function.json의 `bindings` 배열에 다음과 같은 DocumentDB API 출력 바인딩이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b60a-167">Suppose you have the following DocumentDB API output binding in the `bindings` array of function.json:</span></span>

```json
{
  "name": "employeeDocument",
  "type": "documentDB",
  "databaseName": "MyDatabase",
  "collectionName": "MyCollection",
  "createIfNotExists": true,
  "connection": "MyAccount_COSMOSDB",     
  "direction": "out"
}
```

<span data-ttu-id="3b60a-168">또한 다음과 같은 형식의 JSON을 수신하는 큐에 대한 큐 입력 바인딩이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b60a-168">And you have a queue input binding for a queue that receives JSON in the following format:</span></span>

```json
{
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

<span data-ttu-id="3b60a-169">그리고 각 레코드에 대해 다음과 같은 형식의 Cosmos DB 문서를 만들려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b60a-169">And you want to create Cosmos DB documents in the following format for each record:</span></span>

```json
{
  "id": "John Henry-123456",
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

<span data-ttu-id="3b60a-170">이 출력 바인딩을 사용하여 문서를 데이터베이스에 추가하는 언어별 샘플을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b60a-170">See the language-specific sample that uses this output binding to add documents to your database.</span></span>

* [<span data-ttu-id="3b60a-171">C#</span><span class="sxs-lookup"><span data-stu-id="3b60a-171">C#</span></span>](#outcsharp)
* [<span data-ttu-id="3b60a-172">F#</span><span class="sxs-lookup"><span data-stu-id="3b60a-172">F#</span></span>](#outfsharp)
* [<span data-ttu-id="3b60a-173">JavaScript</span><span class="sxs-lookup"><span data-stu-id="3b60a-173">JavaScript</span></span>](#outjavascript)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="3b60a-174">C#에서 출력 샘플</span><span class="sxs-lookup"><span data-stu-id="3b60a-174">Output sample in C#</span></span> #

```cs
#r "Newtonsoft.Json"

using System;
using Newtonsoft.Json;
using Newtonsoft.Json.Linq;

public static void Run(string myQueueItem, out object employeeDocument, TraceWriter log)
{
  log.Info($"C# Queue trigger function processed: {myQueueItem}");

  dynamic employee = JObject.Parse(myQueueItem);

  employeeDocument = new {
    id = employee.name + "-" + employee.employeeId,
    name = employee.name,
    employeeId = employee.employeeId,
    address = employee.address
  };
}
```

<a name="outfsharp"></a>

### <a name="output-sample-in-f"></a><span data-ttu-id="3b60a-175">F#에서 출력 샘플</span><span class="sxs-lookup"><span data-stu-id="3b60a-175">Output sample in F#</span></span> #

```fsharp
open FSharp.Interop.Dynamic
open Newtonsoft.Json

type Employee = {
  id: string
  name: string
  employeeId: string
  address: string
}

let Run(myQueueItem: string, employeeDocument: byref<obj>, log: TraceWriter) =
  log.Info(sprintf "F# Queue trigger function processed: %s" myQueueItem)
  let employee = JObject.Parse(myQueueItem)
  employeeDocument <-
    { id = sprintf "%s-%s" employee?name employee?employeeId
      name = employee?name
      employeeId = employee?employeeId
      address = employee?address }
```

<span data-ttu-id="3b60a-176">이 샘플에는 `FSharp.Interop.Dynamic` 및 `Dynamitey` NuGet 종속성을 지정하는 `project.json` 파일이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3b60a-176">This sample requires a `project.json` file that specifies the `FSharp.Interop.Dynamic` and `Dynamitey` NuGet dependencies:</span></span>

```json
{
  "frameworks": {
    "net46": {
      "dependencies": {
        "Dynamitey": "1.0.2",
        "FSharp.Interop.Dynamic": "3.0.0"
      }
    }
  }
}
```

<span data-ttu-id="3b60a-177">`project.json` 파일을 추가하려면 [F# 패키지 관리](functions-reference-fsharp.md#package)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b60a-177">To add a `project.json` file, see [F# package management](functions-reference-fsharp.md#package).</span></span>

<a name="outjavascript"></a>

### <a name="output-sample-in-javascript"></a><span data-ttu-id="3b60a-178">JavaScript의 출력 샘플</span><span class="sxs-lookup"><span data-stu-id="3b60a-178">Output sample in JavaScript</span></span>

```javascript
module.exports = function (context) {

  context.bindings.employeeDocument = JSON.stringify({ 
    id: context.bindings.myQueueItem.name + "-" + context.bindings.myQueueItem.employeeId,
    name: context.bindings.myQueueItem.name,
    employeeId: context.bindings.myQueueItem.employeeId,
    address: context.bindings.myQueueItem.address
  });

  context.done();
};
```

---
title: "aaaAzure 함수 Cosmos DB 바인딩 | Microsoft Docs"
description: "이해 어떻게 Azure 함수에서 toouse Azure Cosmos DB 바인딩."
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
ms.openlocfilehash: 76b89e8296db1dd28dff9528903b1f6a28f55232
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-cosmos-db-bindings"></a><span data-ttu-id="6dd32-104">Azure Functions Cosmos DB 바인딩</span><span class="sxs-lookup"><span data-stu-id="6dd32-104">Azure Functions Cosmos DB bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="6dd32-105">이 문서에서는 설명 어떻게 Azure 함수에서 tooconfigure 및 코드 Azure Cosmos DB 바인딩.</span><span class="sxs-lookup"><span data-stu-id="6dd32-105">This article explains how tooconfigure and code Azure Cosmos DB bindings in Azure Functions.</span></span> <span data-ttu-id="6dd32-106">Azure Functions는 Cosmos DB에 대한 입력 및 출력 바인딩을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd32-106">Azure Functions supports input and output bindings for Cosmos DB.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="6dd32-107">Cosmos DB에 대 한 자세한 내용은 참조 하십시오. [소개 tooCosmos DB](../documentdb/documentdb-introduction.md) 및 [Cosmos DB 콘솔 응용 프로그램 빌드](../documentdb/documentdb-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd32-107">For more information on Cosmos DB, see [Introduction tooCosmos DB](../documentdb/documentdb-introduction.md) and [Build a Cosmos DB console application](../documentdb/documentdb-get-started.md).</span></span>

<a id="docdbinput"></a>

## <a name="documentdb-api-input-binding"></a><span data-ttu-id="6dd32-108">DocumentDB API 입력 바인딩</span><span class="sxs-lookup"><span data-stu-id="6dd32-108">DocumentDB API input binding</span></span>
<span data-ttu-id="6dd32-109">Cosmos DB 문서를 검색 하 고 toohello 명명 된 hello 함수의 입력된 매개 변수를 전달 하는 hello DocumentDB API 입력된 바인딩 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd32-109">hello DocumentDB API input binding retrieves a Cosmos DB document and passes it toohello named input parameter of hello function.</span></span> <span data-ttu-id="6dd32-110">hello 함수를 호출 하는 hello 트리거를 기반으로 hello 문서 ID를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6dd32-110">hello document ID can be determined based on hello trigger that invokes hello function.</span></span> 

<span data-ttu-id="6dd32-111">DocumentDB API 입력된 바인딩 hello에 다음과 같은 속성에 hello *function.json*:</span><span class="sxs-lookup"><span data-stu-id="6dd32-111">hello DocumentDB API input binding has hello following properties in *function.json*:</span></span>

- <span data-ttu-id="6dd32-112">`name`: Hello 문서에 대 한 함수 코드에서 사용 하는 식별자 이름</span><span class="sxs-lookup"><span data-stu-id="6dd32-112">`name` : Identifier name used in function code for hello document</span></span>
- <span data-ttu-id="6dd32-113">`type`: 너무 설정 해야 합니다 "documentdb"</span><span class="sxs-lookup"><span data-stu-id="6dd32-113">`type` : must be set too"documentdb"</span></span>
- <span data-ttu-id="6dd32-114">`databaseName`: hello 문서를 포함 하는 hello 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="6dd32-114">`databaseName` : hello database containing hello document</span></span>
- <span data-ttu-id="6dd32-115">`collectionName`: hello 문서를 포함 하는 hello 컬렉션</span><span class="sxs-lookup"><span data-stu-id="6dd32-115">`collectionName` : hello collection containing hello document</span></span>
- <span data-ttu-id="6dd32-116">`id`: hello hello 문서 tooretrieve의 Id입니다.</span><span class="sxs-lookup"><span data-stu-id="6dd32-116">`id` : hello Id of hello document tooretrieve.</span></span> <span data-ttu-id="6dd32-117">이 속성은 바인딩 매개 변수 지원 참조 [바인딩 식에서 toocustom 입력된 속성을 바인딩할](functions-triggers-bindings.md#bind-to-custom-input-properties-in-a-binding-expression) hello 문서의 [Azure 함수 트리거 및 바인딩 개념](functions-triggers-bindings.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd32-117">This property supports bindings parameters; see [Bind toocustom input properties in a binding expression](functions-triggers-bindings.md#bind-to-custom-input-properties-in-a-binding-expression) in hello article [Azure Functions triggers and bindings concepts](functions-triggers-bindings.md).</span></span>
- <span data-ttu-id="6dd32-118">`sqlQuery`: 여러 문서를 검색하는 데 사용되는 Cosmos DB SQL 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="6dd32-118">`sqlQuery` : A Cosmos DB SQL query used for retrieving multiple documents.</span></span> <span data-ttu-id="6dd32-119">hello 쿼리 런타임 바인딩을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd32-119">hello query supports runtime bindings.</span></span> <span data-ttu-id="6dd32-120">예: `SELECT * FROM c where c.departmentId = {departmentId}`</span><span class="sxs-lookup"><span data-stu-id="6dd32-120">For example: `SELECT * FROM c where c.departmentId = {departmentId}`</span></span>
- <span data-ttu-id="6dd32-121">`connection`: Cosmos DB 연결 문자열을 포함 하는 hello 앱 설정의 hello 이름</span><span class="sxs-lookup"><span data-stu-id="6dd32-121">`connection` : hello name of hello app setting containing your Cosmos DB connection string</span></span>
- <span data-ttu-id="6dd32-122">`direction`: 너무 설정 되어 있어야`"in"`합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd32-122">`direction`  : must be set too`"in"`.</span></span>

<span data-ttu-id="6dd32-123">속성을 hello `id` 및 `sqlQuery` 모두 지정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6dd32-123">hello properties `id` and `sqlQuery` cannot both be specified.</span></span> <span data-ttu-id="6dd32-124">모두 `id` 나 `sqlQuery` 설정 되 면 hello 전체 컬렉션에서 검색 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6dd32-124">If neither `id` nor `sqlQuery` is set, hello entire collection is retrieved.</span></span>

## <a name="using-a-documentdb-api-input-binding"></a><span data-ttu-id="6dd32-125">DocumentDB API 입력 바인딩 사용</span><span class="sxs-lookup"><span data-stu-id="6dd32-125">Using a DocumentDB API input binding</span></span>

* <span data-ttu-id="6dd32-126">C# 및 F # 함수에서 hello 함수는 성공적으로 종료 될 때 명명 된 입력된 매개 변수를 통해 toohello 입력된 문서를 변경한 내용은 자동으로 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6dd32-126">In C# and F# functions, when hello function exits successfully, any changes made toohello input document via named input parameters are automatically persisted.</span></span> 
* <span data-ttu-id="6dd32-127">JavaScript 함수에서는 함수 종료 시 자동으로 업데이트되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6dd32-127">In JavaScript functions, updates are not made automatically upon function exit.</span></span> <span data-ttu-id="6dd32-128">대신를 사용 하 여 `context.bindings.<documentName>In` 및 `context.bindings.<documentName>Out` toomake 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd32-128">Instead, use `context.bindings.<documentName>In` and `context.bindings.<documentName>Out` toomake updates.</span></span> <span data-ttu-id="6dd32-129">Hello 참조 [JavaScript 샘플](#injavascript)합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd32-129">See hello [JavaScript sample](#injavascript).</span></span>

<a name="inputsample"></a>

## <a name="input-sample-for-single-document"></a><span data-ttu-id="6dd32-130">단일 문서에 대한 입력 샘플</span><span class="sxs-lookup"><span data-stu-id="6dd32-130">Input sample for single document</span></span>
<span data-ttu-id="6dd32-131">DocumentDB API 입력 바인딩 hello에 있다고 가정 하면 hello 다음 `bindings` function.json의 배열:</span><span class="sxs-lookup"><span data-stu-id="6dd32-131">Suppose you have hello following DocumentDB API input binding in hello `bindings` array of function.json:</span></span>

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

<span data-ttu-id="6dd32-132">이 입력된 바인딩의 tooupdate hello 문서의 텍스트 값을 사용 하는 hello 언어 관련 샘플을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="6dd32-132">See hello language-specific sample that uses this input binding tooupdate hello document's text value.</span></span>

* [<span data-ttu-id="6dd32-133">C#</span><span class="sxs-lookup"><span data-stu-id="6dd32-133">C#</span></span>](#incsharp)
* [<span data-ttu-id="6dd32-134">F#</span><span class="sxs-lookup"><span data-stu-id="6dd32-134">F#</span></span>](#infsharp)
* [<span data-ttu-id="6dd32-135">JavaScript</span><span class="sxs-lookup"><span data-stu-id="6dd32-135">JavaScript</span></span>](#injavascript)

<a name="incsharp"></a>
### <a name="input-sample-in-c"></a><span data-ttu-id="6dd32-136">C#의 입력 샘플</span><span class="sxs-lookup"><span data-stu-id="6dd32-136">Input sample in C#</span></span> #

```cs
// Change input document contents using DocumentDB API input binding 
public static void Run(string myQueueItem, dynamic inputDocument)
{   
  inputDocument.text = "This has changed.";
}
```
<a name="infsharp"></a>

### <a name="input-sample-in-f"></a><span data-ttu-id="6dd32-137">F#의 입력 샘플</span><span class="sxs-lookup"><span data-stu-id="6dd32-137">Input sample in F#</span></span> #

```fsharp
(* Change input document contents using DocumentDB API input binding *)
open FSharp.Interop.Dynamic
let Run(myQueueItem: string, inputDocument: obj) =
  inputDocument?text <- "This has changed."
```

<span data-ttu-id="6dd32-138">이 샘플을 사용 하려면 한 `project.json` hello를 지정 하는 파일 `FSharp.Interop.Dynamic` 및 `Dynamitey` NuGet 종속성:</span><span class="sxs-lookup"><span data-stu-id="6dd32-138">This sample requires a `project.json` file that specifies hello `FSharp.Interop.Dynamic` and `Dynamitey` NuGet dependencies:</span></span>

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

<span data-ttu-id="6dd32-139">tooadd는 `project.json` 파일, 참조 [F # 패키지 관리](functions-reference-fsharp.md#package)합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd32-139">tooadd a `project.json` file, see [F# package management](functions-reference-fsharp.md#package).</span></span>

<a name="injavascript"></a>

### <a name="input-sample-in-javascript"></a><span data-ttu-id="6dd32-140">JavaScript의 입력 샘플</span><span class="sxs-lookup"><span data-stu-id="6dd32-140">Input sample in JavaScript</span></span>

```javascript
// Change input document contents using DocumentDB API input binding, using context.bindings.inputDocumentOut
module.exports = function (context) {   
  context.bindings.inputDocumentOut = context.bindings.inputDocumentIn;
  context.bindings.inputDocumentOut.text = "This was updated!";
  context.done();
};
```

## <a name="input-sample-with-multiple-documents"></a><span data-ttu-id="6dd32-141">여러 문서가 있는 입력 샘플</span><span class="sxs-lookup"><span data-stu-id="6dd32-141">Input sample with multiple documents</span></span>

<span data-ttu-id="6dd32-142">한다고 tooretrieve SQL 쿼리로 지정 된 여러 문서는 큐 트리거 toocustomize hello 쿼리 매개 변수를 사용 하 여 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd32-142">Suppose that you wish tooretrieve multiple documents specified by a SQL query, using a queue trigger toocustomize hello query parameters.</span></span> 

<span data-ttu-id="6dd32-143">이 예제에서는 hello 큐 트리거 매개 변수를 제공 `departmentId`합니다. 큐 메시지의 `{ "departmentId" : "Finance" }` hello 재무 부서에 대 한 모든 레코드를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd32-143">In this example, hello queue trigger provides a parameter `departmentId`.A queue message of `{ "departmentId" : "Finance" }` would return all records for hello finance department.</span></span> <span data-ttu-id="6dd32-144">다음 hello를 사용 하 여 *function.json*:</span><span class="sxs-lookup"><span data-stu-id="6dd32-144">Use hello following in *function.json*:</span></span>

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

### <a name="input-sample-with-multiple-documents-in-c"></a><span data-ttu-id="6dd32-145">C#으로 작성된 여러 문서가 있는 입력 샘플</span><span class="sxs-lookup"><span data-stu-id="6dd32-145">Input sample with multiple documents in C#</span></span>

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

### <a name="input-sample-with-multiple-documents-in-javascript"></a><span data-ttu-id="6dd32-146">JavaScript로 작성된 여러 문서가 있는 입력 샘플</span><span class="sxs-lookup"><span data-stu-id="6dd32-146">Input sample with multiple documents in JavaScript</span></span>

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

## <span data-ttu-id="6dd32-147"><a id="docdboutput"></a>DocumentDB API 출력 바인딩</span><span class="sxs-lookup"><span data-stu-id="6dd32-147"><a id="docdboutput"></a>DocumentDB API output binding</span></span>
<span data-ttu-id="6dd32-148">DocumentDB API hello 작성할 새 문서 tooan Azure Cosmos DB 데이터베이스 바인딩 수를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd32-148">hello DocumentDB API output binding lets you write a new document tooan Azure Cosmos DB database.</span></span> <span data-ttu-id="6dd32-149">다음과 같은 속성에 hello 있기 *function.json*:</span><span class="sxs-lookup"><span data-stu-id="6dd32-149">It has hello following properties in *function.json*:</span></span>

- <span data-ttu-id="6dd32-150">`name`: Hello 새 문서에 대 한 함수 코드에서 사용 되는 식별자</span><span class="sxs-lookup"><span data-stu-id="6dd32-150">`name` : Identifier used in function code for hello new document</span></span>
- <span data-ttu-id="6dd32-151">`type`: 너무 설정 해야 합니다`"documentdb"`</span><span class="sxs-lookup"><span data-stu-id="6dd32-151">`type` : must be set too`"documentdb"`</span></span>
- <span data-ttu-id="6dd32-152">`databaseName`: hello 새 문서를 만들 위치 hello 컬렉션을 포함 하는 hello 데이터베이스.</span><span class="sxs-lookup"><span data-stu-id="6dd32-152">`databaseName` : hello database containing hello collection where hello new document will be created.</span></span>
- <span data-ttu-id="6dd32-153">`collectionName`: hello 컬렉션 hello 새 문서를 만들 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="6dd32-153">`collectionName` : hello collection where hello new document will be created.</span></span>
- <span data-ttu-id="6dd32-154">`createIfNotExists`: 부울 값이 존재 하지 않는 경우 hello 컬렉션을 만들 수는 여부를 tooindicate입니다.</span><span class="sxs-lookup"><span data-stu-id="6dd32-154">`createIfNotExists` : A boolean value tooindicate whether hello collection will be created if it does not exist.</span></span> <span data-ttu-id="6dd32-155">hello 기본값은 *false*합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd32-155">hello default is *false*.</span></span> <span data-ttu-id="6dd32-156">이유 hello 예약 된 처리량이 가격에 영향을 줄 수 있는 컬렉션을 만들고 새로운 기능이 며에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd32-156">hello reason for this is new collections are created with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="6dd32-157">자세한 내용은 hello를 방문 하세요 [가격 책정 페이지](https://azure.microsoft.com/pricing/details/documentdb/)합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd32-157">For more details, please visit hello [pricing page](https://azure.microsoft.com/pricing/details/documentdb/).</span></span>
- <span data-ttu-id="6dd32-158">`connection`: Cosmos DB 연결 문자열을 포함 하는 hello 앱 설정의 hello 이름</span><span class="sxs-lookup"><span data-stu-id="6dd32-158">`connection` : hello name of hello app setting containing your Cosmos DB connection string</span></span>
- <span data-ttu-id="6dd32-159">`direction`: 너무 설정 해야 합니다`"out"`</span><span class="sxs-lookup"><span data-stu-id="6dd32-159">`direction` : must be set too`"out"`</span></span>

## <a name="using-a-documentdb-api-output-binding"></a><span data-ttu-id="6dd32-160">DocumentDB API 출력 바인딩 사용</span><span class="sxs-lookup"><span data-stu-id="6dd32-160">Using a DocumentDB API output binding</span></span>
<span data-ttu-id="6dd32-161">이 섹션에서는 어떻게 toouse DocumentDB API 출력 함수 코드에서 바인딩을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6dd32-161">This section shows you how toouse your DocumentDB API output binding in your function code.</span></span>

<span data-ttu-id="6dd32-162">기본적으로 데이터베이스에 새 문서 생성은 함수에서 toohello 출력 매개 변수를 작성할 때 hello로 자동으로 생성된 된 GUID와 문서 id입니다.</span><span class="sxs-lookup"><span data-stu-id="6dd32-162">When you write toohello output parameter in your function, by default a new document is generated in your database, with an automatically generated GUID as hello document ID.</span></span> <span data-ttu-id="6dd32-163">Hello를 지정 하 여 출력 문서의 hello 문서 ID를 지정할 수 있습니다 `id` hello에 JSON 속성 매개 변수를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd32-163">You can specify hello document ID of output document by specifying hello `id` JSON property in hello output parameter.</span></span> 

>[!Note]  
><span data-ttu-id="6dd32-164">기존 문서 hello ID를 지정 하 여 hello 새 출력 문서가 덮어쓰기됩니다.</span><span class="sxs-lookup"><span data-stu-id="6dd32-164">When you specify hello ID of an existing document, it gets overwritten by hello new output document.</span></span> 

<span data-ttu-id="6dd32-165">toooutput 여러 문서를 바인딩할 수도 있습니다 너무`ICollector<T>` 또는 `IAsyncCollector<T>` 여기서 `T` hello 지원 형식 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="6dd32-165">toooutput multiple documents, you can also bind too`ICollector<T>` or `IAsyncCollector<T>` where `T` is one of hello supported types.</span></span>

<a name="outputsample"></a>

## <a name="documentdb-api-output-binding-sample"></a><span data-ttu-id="6dd32-166">DocumentDB API 출력 바인딩 샘플</span><span class="sxs-lookup"><span data-stu-id="6dd32-166">DocumentDB API output binding sample</span></span>
<span data-ttu-id="6dd32-167">DocumentDB API 출력 바인딩 hello에 있다고 가정 하면 hello 다음 `bindings` function.json의 배열:</span><span class="sxs-lookup"><span data-stu-id="6dd32-167">Suppose you have hello following DocumentDB API output binding in hello `bindings` array of function.json:</span></span>

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

<span data-ttu-id="6dd32-168">있고 JSON 형식에 따라 hello에서 부여 하는 큐에 대 한 큐 입력된 바인딩:</span><span class="sxs-lookup"><span data-stu-id="6dd32-168">And you have a queue input binding for a queue that receives JSON in hello following format:</span></span>

```json
{
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

<span data-ttu-id="6dd32-169">및 toocreate Cosmos DB 문서에서 각 레코드에 대 한 형식에 따라 hello에:</span><span class="sxs-lookup"><span data-stu-id="6dd32-169">And you want toocreate Cosmos DB documents in hello following format for each record:</span></span>

```json
{
  "id": "John Henry-123456",
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

<span data-ttu-id="6dd32-170">이 출력 바인딩 tooadd 문서 tooyour 데이터베이스를 사용 하는 hello 언어 관련 샘플을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="6dd32-170">See hello language-specific sample that uses this output binding tooadd documents tooyour database.</span></span>

* [<span data-ttu-id="6dd32-171">C#</span><span class="sxs-lookup"><span data-stu-id="6dd32-171">C#</span></span>](#outcsharp)
* [<span data-ttu-id="6dd32-172">F#</span><span class="sxs-lookup"><span data-stu-id="6dd32-172">F#</span></span>](#outfsharp)
* [<span data-ttu-id="6dd32-173">JavaScript</span><span class="sxs-lookup"><span data-stu-id="6dd32-173">JavaScript</span></span>](#outjavascript)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="6dd32-174">C#에서 출력 샘플</span><span class="sxs-lookup"><span data-stu-id="6dd32-174">Output sample in C#</span></span> #

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

### <a name="output-sample-in-f"></a><span data-ttu-id="6dd32-175">F#에서 출력 샘플</span><span class="sxs-lookup"><span data-stu-id="6dd32-175">Output sample in F#</span></span> #

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

<span data-ttu-id="6dd32-176">이 샘플을 사용 하려면 한 `project.json` hello를 지정 하는 파일 `FSharp.Interop.Dynamic` 및 `Dynamitey` NuGet 종속성:</span><span class="sxs-lookup"><span data-stu-id="6dd32-176">This sample requires a `project.json` file that specifies hello `FSharp.Interop.Dynamic` and `Dynamitey` NuGet dependencies:</span></span>

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

<span data-ttu-id="6dd32-177">tooadd는 `project.json` 파일, 참조 [F # 패키지 관리](functions-reference-fsharp.md#package)합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd32-177">tooadd a `project.json` file, see [F# package management](functions-reference-fsharp.md#package).</span></span>

<a name="outjavascript"></a>

### <a name="output-sample-in-javascript"></a><span data-ttu-id="6dd32-178">JavaScript의 출력 샘플</span><span class="sxs-lookup"><span data-stu-id="6dd32-178">Output sample in JavaScript</span></span>

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

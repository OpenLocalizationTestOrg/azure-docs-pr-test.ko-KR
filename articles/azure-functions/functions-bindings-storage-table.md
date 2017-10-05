---
title: "Azure Functions Storage 테이블 바인딩 | Microsoft Docs"
description: "Azure Functions에서 Azure Storage 바인딩을 사용하는 방법을 이해합니다."
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: "Azure Functions, 함수, 이벤트 처리, 동적 계산, 서버를 사용하지 않는 아키텍처"
ms.assetid: 65b3437e-2571-4d3f-a996-61a74b50a1c2
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 10/28/2016
ms.author: chrande
ms.openlocfilehash: bb01be3ee044f60376e0c9c2de7b3dd34f3b7aca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-storage-table-bindings"></a><span data-ttu-id="90de8-104">Azure Functions Storage 테이블 바인딩</span><span class="sxs-lookup"><span data-stu-id="90de8-104">Azure Functions Storage table bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="90de8-105">이 문서에서는 Azure Functions에서 Azure Storage 테이블 바인딩을 구성하고 코딩하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="90de8-105">This article explains how to configure and code Azure Storage table bindings in Azure Functions.</span></span> <span data-ttu-id="90de8-106">Azure Functions는 Azure Storage 테이블에 대한 입력 및 출력 바인딩을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="90de8-106">Azure Functions supports input and output bindings for Azure Storage tables.</span></span>

<span data-ttu-id="90de8-107">Storage 테이블 바인딩은 다음과 같은 시나리오를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="90de8-107">The Storage table binding supports the following scenarios:</span></span>

* <span data-ttu-id="90de8-108">**C# 또는 Node.js 함수에서 단일 행을 읽습니다.** - `partitionKey` 및 `rowKey`를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="90de8-108">**Read a single row in a C# or Node.js function** - Set `partitionKey` and `rowKey`.</span></span> <span data-ttu-id="90de8-109">`filter` 및 `take` 속성은 이 시나리오에서 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="90de8-109">The `filter` and `take` properties are not used in this scenario.</span></span>
* <span data-ttu-id="90de8-110">**C# 함수에서 여러 행을 읽습니다.** - 함수 런타임은 테이블에 바인딩된 `IQueryable<T>` 개체를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="90de8-110">**Read multiple rows in a C# function** - The Functions runtime provides an `IQueryable<T>` object bound to the table.</span></span> <span data-ttu-id="90de8-111">`T` 형식은 `TableEntity`에서 파생되거나 `ITableEntity`를 구현해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90de8-111">Type `T` must derive from `TableEntity` or implement `ITableEntity`.</span></span> <span data-ttu-id="90de8-112">`partitionKey`, `rowKey`, `filter` 및 `take` 속성은 이 시나리오에서 사용되지 않습니다. `IQueryable` 개체를 사용하여 필요한 모든 필터링 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90de8-112">The `partitionKey`, `rowKey`, `filter`, and `take` properties are not used in this scenario; you can use the `IQueryable` object to do any filtering required.</span></span> 
* <span data-ttu-id="90de8-113">**Node 함수에서 여러 행을 읽습니다.** - `filter` 및 `take` 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="90de8-113">**Read multiple rows in a Node function** - Set the `filter` and `take` properties.</span></span> <span data-ttu-id="90de8-114">`partitionKey` 또는 `rowKey`를 설정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="90de8-114">Don't set `partitionKey` or `rowKey`.</span></span>
* <span data-ttu-id="90de8-115">**C# 함수에서 하나 이상의 행을 작성합니다.** - 함수 런타임에서는 테이블에 바인딩된 `ICollector<T>` 또는 `IAsyncCollector<T>`를 제공하며 여기서 `T`는 추가하려는 엔터티의 스키마를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="90de8-115">**Write one or more rows in a C# function** - The Functions runtime provides an `ICollector<T>` or `IAsyncCollector<T>` bound to the table, where `T` specifies the schema of the entities you want to add.</span></span> <span data-ttu-id="90de8-116">일반적으로 `T` 형식은 `TableEntity`에서 파생되거나 `ITableEntity`을 구현하지만 반드시 그런 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="90de8-116">Typically, type `T` derives from `TableEntity` or implements `ITableEntity`, but it doesn't have to.</span></span> <span data-ttu-id="90de8-117">`partitionKey`, `rowKey`, `filter` 및 `take` 속성은 이 시나리오에서 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="90de8-117">The `partitionKey`, `rowKey`, `filter`, and `take` properties are not used in this scenario.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="input"></a>

## <a name="storage-table-input-binding"></a><span data-ttu-id="90de8-118">Storage 테이블 입력 바인딩</span><span class="sxs-lookup"><span data-stu-id="90de8-118">Storage table input binding</span></span>
<span data-ttu-id="90de8-119">Azure Storage 테이블 입력 바인딩을 사용하면 함수의 저장소 테이블을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90de8-119">The Azure Storage table input binding enables you to use a storage table in your function.</span></span> 

<span data-ttu-id="90de8-120">함수에 대한 Storage 테이블 입력은 function.json의 `bindings` 배열에서 다음과 같은 JSON 개체를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="90de8-120">The Storage table input to a function uses the following JSON objects in the `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "table",
    "direction": "in",
    "tableName": "<Name of Storage table>",
    "partitionKey": "<PartitionKey of table entity to read - see below>",
    "rowKey": "<RowKey of table entity to read - see below>",
    "take": "<Maximum number of entities to read in Node.js - optional>",
    "filter": "<OData filter expression for table input in Node.js - optional>",
    "connection": "<Name of app setting - see below>",
}
```

<span data-ttu-id="90de8-121">다음 사항에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="90de8-121">Note the following:</span></span> 

* <span data-ttu-id="90de8-122">`partitionKey` 및 `rowKey`를 함께 사용하여 단일 엔터티를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="90de8-122">Use `partitionKey` and `rowKey` together to read a single entity.</span></span> <span data-ttu-id="90de8-123">이러한 속성은 선택적입니다.</span><span class="sxs-lookup"><span data-stu-id="90de8-123">These properties are optional.</span></span> 
* <span data-ttu-id="90de8-124">`connection`은 저장소 연결 문자열을 포함하는 앱 설정의 이름을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90de8-124">`connection` must contain the name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="90de8-125">Azure Portal에서 **통합** 탭에 있는 표준 편집기는 저장소 계정을 만들거나 기존 계정을 선택하는 경우 사용하는 이 앱 설정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="90de8-125">In the Azure portal, the standard editor in the **Integrate** tab configures this app setting for you when you create a Storage account or selects an existing one.</span></span> <span data-ttu-id="90de8-126">또한 [이 앱 설정을 수동으로 구성](functions-how-to-use-azure-function-app-settings.md#settings)할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90de8-126">You can also [configure this app setting manually](functions-how-to-use-azure-function-app-settings.md#settings).</span></span>  

<a name="inputusage"></a>

## <a name="input-usage"></a><span data-ttu-id="90de8-127">입력 사용</span><span class="sxs-lookup"><span data-stu-id="90de8-127">Input usage</span></span>
<span data-ttu-id="90de8-128">C# 함수에서 `<T> <name>`같은 함수 시그니처의 명명된 매개 변수를 사용하여 입력 테이블 엔터티(또는 여러 엔터티)를 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="90de8-128">In C# functions, you bind to the input table entity (or entities) by using a named parameter in your function signature, like `<T> <name>`.</span></span>
<span data-ttu-id="90de8-129">여기서 `T`는 데이터를 deserialize할 데이터 형식이며, `paramName`은 [입력 바인딩](#input)에서 사용자가 지정한 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="90de8-129">Where `T` is the data type that you want to deserialize the data into, and `paramName` is the name you specified in the [input binding](#input).</span></span> <span data-ttu-id="90de8-130">Node.js 함수에서 `context.bindings.<name>`을 사용하여 입력 테이블 엔터티(또는 여러 엔터티)에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="90de8-130">In Node.js functions, you access the input table entity (or entities) using `context.bindings.<name>`.</span></span>

<span data-ttu-id="90de8-131">입력 데이터는 Node.js 또는 C# 함수에서 deserialize될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90de8-131">The input data can be deserialized in Node.js or C# functions.</span></span> <span data-ttu-id="90de8-132">Deserialize된 개체는 `RowKey` 및 `PartitionKey` 속성을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="90de8-132">The deserialized objects have `RowKey` and `PartitionKey` properties.</span></span>

<span data-ttu-id="90de8-133">C# 함수에서 다음 형식 중 하나에 바인딩할 수도 있으며, Functions 런타임이 해당 형식을 사용하여 테이블 데이터를 deserialize하려고 시도하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="90de8-133">In C# functions, you can also bind to any of the following types, and the Functions runtime will attempt to deserialize the table data using that type:</span></span>

* <span data-ttu-id="90de8-134">구현하는 모든 형식 `ITableEntity`</span><span class="sxs-lookup"><span data-stu-id="90de8-134">Any type that implements `ITableEntity`</span></span>
* `IQueryable<T>`

<a name="inputsample"></a>

## <a name="input-sample"></a><span data-ttu-id="90de8-135">입력 샘플</span><span class="sxs-lookup"><span data-stu-id="90de8-135">Input sample</span></span>
<span data-ttu-id="90de8-136">큐 트리거를 사용하여 단일 테이블 행을 읽는 다음과 같은 function.json이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="90de8-136">Supposed you have the following function.json, which uses a queue trigger to read a single table row.</span></span> <span data-ttu-id="90de8-137">JSON은 `PartitionKey` 
`RowKey`를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="90de8-137">The JSON specifies `PartitionKey` 
`RowKey`.</span></span> <span data-ttu-id="90de8-138">`"rowKey": "{queueTrigger}"`는 큐 메시지 문자열에서 나온 행 키를 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="90de8-138">`"rowKey": "{queueTrigger}"` indicates that the row key comes from the queue message string.</span></span>

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
      "name": "personEntity",
      "type": "table",
      "tableName": "Person",
      "partitionKey": "Test",
      "rowKey": "{queueTrigger}",
      "connection": "MyStorageConnection",
      "direction": "in"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="90de8-139">단일 테이블 엔터티를 읽는 언어별 샘플을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="90de8-139">See the language-specific sample that reads a single table entity.</span></span>

* [<span data-ttu-id="90de8-140">C#</span><span class="sxs-lookup"><span data-stu-id="90de8-140">C#</span></span>](#inputcsharp)
* [<span data-ttu-id="90de8-141">F#</span><span class="sxs-lookup"><span data-stu-id="90de8-141">F#</span></span>](#inputfsharp)
* [<span data-ttu-id="90de8-142">Node.JS</span><span class="sxs-lookup"><span data-stu-id="90de8-142">Node.js</span></span>](#inputnodejs)

<a name="inputcsharp"></a>

### <a name="input-sample-in-c"></a><span data-ttu-id="90de8-143">C#의 입력 샘플</span><span class="sxs-lookup"><span data-stu-id="90de8-143">Input sample in C#</span></span> #
```csharp
public static void Run(string myQueueItem, Person personEntity, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    log.Info($"Name in Person entity: {personEntity.Name}");
}

public class Person
{
    public string PartitionKey { get; set; }
    public string RowKey { get; set; }
    public string Name { get; set; }
}
```

<a name="inputfsharp"></a>

### <a name="input-sample-in-f"></a><span data-ttu-id="90de8-144">F#의 입력 샘플</span><span class="sxs-lookup"><span data-stu-id="90de8-144">Input sample in F#</span></span> #
```fsharp
[<CLIMutable>]
type Person = {
  PartitionKey: string
  RowKey: string
  Name: string
}

let Run(myQueueItem: string, personEntity: Person) =
    log.Info(sprintf "F# Queue trigger function processed: %s" myQueueItem)
    log.Info(sprintf "Name in Person entity: %s" personEntity.Name)
```

<a name="inputnodejs"></a>

### <a name="input-sample-in-nodejs"></a><span data-ttu-id="90de8-145">Node.js에서 입력 샘플</span><span class="sxs-lookup"><span data-stu-id="90de8-145">Input sample in Node.js</span></span>
```javascript
module.exports = function (context, myQueueItem) {
    context.log('Node.js queue trigger function processed work item', myQueueItem);
    context.log('Person entity name: ' + context.bindings.personEntity.Name);
    context.done();
};
```

<a name="output"></a>

## <a name="storage-table-output-binding"></a><span data-ttu-id="90de8-146">Storage 테이블 출력 바인딩</span><span class="sxs-lookup"><span data-stu-id="90de8-146">Storage table output binding</span></span>
<span data-ttu-id="90de8-147">Azure Storage 테이블 출력 바인딩을 사용하면 엔터티를 함수의 저장소 테이블에 쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90de8-147">The Azure Storage table output binding enables you to write entities to a Storage table in your function.</span></span> 

<span data-ttu-id="90de8-148">함수에 대한 Storage 테이블 출력은 function.json의 `bindings` 배열에서 다음과 같은 JSON 개체를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="90de8-148">The Storage table output for a function uses the following JSON objects in the `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "table",
    "direction": "out",
    "tableName": "<Name of Storage table>",
    "partitionKey": "<PartitionKey of table entity to write - see below>",
    "rowKey": "<RowKey of table entity to write - see below>",
    "connection": "<Name of app setting - see below>",
}
```

<span data-ttu-id="90de8-149">다음 사항에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="90de8-149">Note the following:</span></span> 

* <span data-ttu-id="90de8-150">`partitionKey` 및 `rowKey`를 함께 사용하여 단일 엔터티를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="90de8-150">Use `partitionKey` and `rowKey` together to write a single entity.</span></span> <span data-ttu-id="90de8-151">이러한 속성은 선택적입니다.</span><span class="sxs-lookup"><span data-stu-id="90de8-151">These properties are optional.</span></span> <span data-ttu-id="90de8-152">또한 함수 코드에 엔터티 개체를 만들 때 `PartitionKey` 및 `RowKey`를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90de8-152">You can also specify `PartitionKey` and `RowKey` when you create the entity objects in your function code.</span></span>
* <span data-ttu-id="90de8-153">`connection`은 저장소 연결 문자열을 포함하는 앱 설정의 이름을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90de8-153">`connection` must contain the name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="90de8-154">Azure Portal에서 **통합** 탭에 있는 표준 편집기는 저장소 계정을 만들거나 기존 계정을 선택하는 경우 사용하는 이 앱 설정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="90de8-154">In the Azure portal, the standard editor in the **Integrate** tab configures this app setting for you when you create a Storage account or selects an existing one.</span></span> <span data-ttu-id="90de8-155">또한 [이 앱 설정을 수동으로 구성](functions-how-to-use-azure-function-app-settings.md#settings)할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90de8-155">You can also [configure this app setting manually](functions-how-to-use-azure-function-app-settings.md#settings).</span></span> 

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="90de8-156">출력 사용</span><span class="sxs-lookup"><span data-stu-id="90de8-156">Output usage</span></span>
<span data-ttu-id="90de8-157">C# 함수에서 `out <T> <name>`같은 함수 시그니처의 명명된 `out` 매개 변수를 사용하여 테이블 출력을 바인딩합니다. 여기서 `T`는 데이터를 직렬화하려는 데이터 형식이며, `paramName`은 [출력 바인딩](#output)에서 사용자가 지정한 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="90de8-157">In C# functions, you bind to the table output by using the named `out` parameter in your function signature, like `out <T> <name>`, where `T` is the data type that you want to serialize the data into, and `paramName` is the name you specified in the [output binding](#output).</span></span> <span data-ttu-id="90de8-158">Node.js 함수에서 `context.bindings.<name>`을 사용하여 테이블 출력에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="90de8-158">In Node.js functions, you access the table output using `context.bindings.<name>`.</span></span>

<span data-ttu-id="90de8-159">Node.js 또는 C# 함수에서 개체를 직렬화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90de8-159">You can serialize objects in Node.js or C# functions.</span></span> <span data-ttu-id="90de8-160">C# 함수에서 다음 형식으로 바인딩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90de8-160">In C# functions, you can also bind to the following types:</span></span>

* <span data-ttu-id="90de8-161">구현하는 모든 형식 `ITableEntity`</span><span class="sxs-lookup"><span data-stu-id="90de8-161">Any type that implements `ITableEntity`</span></span>
* <span data-ttu-id="90de8-162">`ICollector<T>`(여러 엔터티를 출력.</span><span class="sxs-lookup"><span data-stu-id="90de8-162">`ICollector<T>` (to output multiple entities.</span></span> <span data-ttu-id="90de8-163">[샘플](#outcsharp)을 참조하세요.)</span><span class="sxs-lookup"><span data-stu-id="90de8-163">See [sample](#outcsharp).)</span></span>
* <span data-ttu-id="90de8-164">`IAsyncCollector<T>`(비동기 버전의 `ICollector<T>`)</span><span class="sxs-lookup"><span data-stu-id="90de8-164">`IAsyncCollector<T>` (async version of `ICollector<T>`)</span></span>
* <span data-ttu-id="90de8-165">`CloudTable` (Azure Storage SDK 사용.</span><span class="sxs-lookup"><span data-stu-id="90de8-165">`CloudTable` (using the Azure Storage SDK.</span></span> <span data-ttu-id="90de8-166">[샘플](#readmulti)을 참조하세요.)</span><span class="sxs-lookup"><span data-stu-id="90de8-166">See [sample](#readmulti).)</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="90de8-167">출력 샘플</span><span class="sxs-lookup"><span data-stu-id="90de8-167">Output sample</span></span>
<span data-ttu-id="90de8-168">다음 *function.json* 및 *run.csx* 예제에서는 여러 테이블 엔터티를 작성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="90de8-168">The following *function.json* and *run.csx* example shows how to write multiple table entities.</span></span>

```json
{
  "bindings": [
    {
      "name": "input",
      "type": "manualTrigger",
      "direction": "in"
    },
    {
      "tableName": "Person",
      "connection": "MyStorageConnection",
      "name": "tableBinding",
      "type": "table",
      "direction": "out"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="90de8-169">여러 테이블 엔터티를 만드는 언어별 샘플을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="90de8-169">See the language-specific sample that creates multiple table entities.</span></span>

* [<span data-ttu-id="90de8-170">C#</span><span class="sxs-lookup"><span data-stu-id="90de8-170">C#</span></span>](#outcsharp)
* [<span data-ttu-id="90de8-171">F#</span><span class="sxs-lookup"><span data-stu-id="90de8-171">F#</span></span>](#outfsharp)
* [<span data-ttu-id="90de8-172">Node.JS</span><span class="sxs-lookup"><span data-stu-id="90de8-172">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="90de8-173">C#에서 출력 샘플</span><span class="sxs-lookup"><span data-stu-id="90de8-173">Output sample in C#</span></span> #
```csharp
public static void Run(string input, ICollector<Person> tableBinding, TraceWriter log)
{
    for (int i = 1; i < 10; i++)
        {
            log.Info($"Adding Person entity {i}");
            tableBinding.Add(
                new Person() { 
                    PartitionKey = "Test", 
                    RowKey = i.ToString(), 
                    Name = "Name" + i.ToString() }
                );
        }

}

public class Person
{
    public string PartitionKey { get; set; }
    public string RowKey { get; set; }
    public string Name { get; set; }
}

```
<a name="outfsharp"></a>

### <a name="output-sample-in-f"></a><span data-ttu-id="90de8-174">F#에서 출력 샘플</span><span class="sxs-lookup"><span data-stu-id="90de8-174">Output sample in F#</span></span> #
```fsharp
[<CLIMutable>]
type Person = {
  PartitionKey: string
  RowKey: string
  Name: string
}

let Run(input: string, tableBinding: ICollector<Person>, log: TraceWriter) =
    for i = 1 to 10 do
        log.Info(sprintf "Adding Person entity %d" i)
        tableBinding.Add(
            { PartitionKey = "Test"
              RowKey = i.ToString()
              Name = "Name" + i.ToString() })
```

<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a><span data-ttu-id="90de8-175">Node.js에서 출력 샘플</span><span class="sxs-lookup"><span data-stu-id="90de8-175">Output sample in Node.js</span></span>
```javascript
module.exports = function (context) {

    context.bindings.tableBinding = [];

    for (var i = 1; i < 10; i++) {
        context.bindings.tableBinding.push({
            PartitionKey: "Test",
            RowKey: i.toString(),
            Name: "Name " + i
        });
    }
    
    context.done();
};
```

<a name="readmulti"></a>

## <a name="sample-read-multiple-table-entities-in-c"></a><span data-ttu-id="90de8-176">샘플: C#에서 여러 테이블 엔터티 읽기</span><span class="sxs-lookup"><span data-stu-id="90de8-176">Sample: Read multiple table entities in C#</span></span>  #
<span data-ttu-id="90de8-177">다음 *function.json* 및 C# 코드 예제에서는 큐 메시지에 지정된 파티션 키에 대한 엔터티를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="90de8-177">The following *function.json* and C# code example reads entities for a partition key that is specified in the queue message.</span></span>

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
      "name": "tableBinding",
      "type": "table",
      "connection": "MyStorageConnection",
      "tableName": "Person",
      "direction": "in"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="90de8-178">C# 코드는 엔터티 형식이 `TableEntity`에서 파생할 수 있도록 Azure 저장소 SDK에 대한 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="90de8-178">The C# code adds a reference to the Azure Storage SDK so that the entity type can derive from `TableEntity`.</span></span>

```csharp
#r "Microsoft.WindowsAzure.Storage"
using Microsoft.WindowsAzure.Storage.Table;

public static void Run(string myQueueItem, IQueryable<Person> tableBinding, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    foreach (Person person in tableBinding.Where(p => p.PartitionKey == myQueueItem).ToList())
    {
        log.Info($"Name: {person.Name}");
    }
}

public class Person : TableEntity
{
    public string Name { get; set; }
}
```

## <a name="next-steps"></a><span data-ttu-id="90de8-179">다음 단계</span><span class="sxs-lookup"><span data-stu-id="90de8-179">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]


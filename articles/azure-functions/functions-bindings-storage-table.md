---
title: "aaaAzure 함수 저장소 테이블 바인딩 | Microsoft Docs"
description: "이해 어떻게 Azure 함수에서 toouse Azure 저장소 바인딩."
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
ms.openlocfilehash: 90c2a73329139d4ab3504bc0e2c90370133158bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-storage-table-bindings"></a><span data-ttu-id="fae63-104">Azure Functions Storage 테이블 바인딩</span><span class="sxs-lookup"><span data-stu-id="fae63-104">Azure Functions Storage table bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="fae63-105">이 문서에서는 tooconfigure 및 코드 Azure 저장소 테이블 Azure 함수에서 바인딩 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="fae63-105">This article explains how tooconfigure and code Azure Storage table bindings in Azure Functions.</span></span> <span data-ttu-id="fae63-106">Azure Functions는 Azure Storage 테이블에 대한 입력 및 출력 바인딩을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="fae63-106">Azure Functions supports input and output bindings for Azure Storage tables.</span></span>

<span data-ttu-id="fae63-107">hello 저장소 테이블 바인딩은 hello를 다음 시나리오를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="fae63-107">hello Storage table binding supports hello following scenarios:</span></span>

* <span data-ttu-id="fae63-108">**C# 또는 Node.js 함수에서 단일 행을 읽습니다.** - `partitionKey` 및 `rowKey`를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="fae63-108">**Read a single row in a C# or Node.js function** - Set `partitionKey` and `rowKey`.</span></span> <span data-ttu-id="fae63-109">hello `filter` 및 `take` 속성이이 시나리오에서는 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fae63-109">hello `filter` and `take` properties are not used in this scenario.</span></span>
* <span data-ttu-id="fae63-110">**C# 함수에서 여러 행을 읽고** -hello 함수 런타임에서 제공는 `IQueryable<T>` 바인딩된 toohello 테이블 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="fae63-110">**Read multiple rows in a C# function** - hello Functions runtime provides an `IQueryable<T>` object bound toohello table.</span></span> <span data-ttu-id="fae63-111">`T` 형식은 `TableEntity`에서 파생되거나 `ITableEntity`를 구현해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fae63-111">Type `T` must derive from `TableEntity` or implement `ITableEntity`.</span></span> <span data-ttu-id="fae63-112">hello `partitionKey`, `rowKey`, `filter`, 및 `take` 속성은이 시나리오에서는 사용 되지 않으며 hello를 사용할 수 있습니다 `IQueryable` 개체 toodo 필요한 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="fae63-112">hello `partitionKey`, `rowKey`, `filter`, and `take` properties are not used in this scenario; you can use hello `IQueryable` object toodo any filtering required.</span></span> 
* <span data-ttu-id="fae63-113">**노드 함수에서 여러 행을 읽고** 설정 hello- `filter` 및 `take` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="fae63-113">**Read multiple rows in a Node function** - Set hello `filter` and `take` properties.</span></span> <span data-ttu-id="fae63-114">`partitionKey` 또는 `rowKey`를 설정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fae63-114">Don't set `partitionKey` or `rowKey`.</span></span>
* <span data-ttu-id="fae63-115">**C# 함수에서 하나 이상의 행을 작성** -hello 함수 런타임에서 제공는 `ICollector<T>` 또는 `IAsyncCollector<T>` 바인딩된 toohello 테이블 여기서 `T` hello 스키마 지정 원하는 tooadd hello 엔터티.</span><span class="sxs-lookup"><span data-stu-id="fae63-115">**Write one or more rows in a C# function** - hello Functions runtime provides an `ICollector<T>` or `IAsyncCollector<T>` bound toohello table, where `T` specifies hello schema of hello entities you want tooadd.</span></span> <span data-ttu-id="fae63-116">일반적으로 `T` 형식은 `TableEntity`에서 파생되거나 `ITableEntity`을 구현하지만 반드시 그런 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="fae63-116">Typically, type `T` derives from `TableEntity` or implements `ITableEntity`, but it doesn't have to.</span></span> <span data-ttu-id="fae63-117">hello `partitionKey`, `rowKey`, `filter`, 및 `take` 속성이이 시나리오에서는 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fae63-117">hello `partitionKey`, `rowKey`, `filter`, and `take` properties are not used in this scenario.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="input"></a>

## <a name="storage-table-input-binding"></a><span data-ttu-id="fae63-118">Storage 테이블 입력 바인딩</span><span class="sxs-lookup"><span data-stu-id="fae63-118">Storage table input binding</span></span>
<span data-ttu-id="fae63-119">Azure 저장소 테이블에 대 한 입력된 바인딩 hello toouse를 함수에서 저장소 테이블 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fae63-119">hello Azure Storage table input binding enables you toouse a storage table in your function.</span></span> 

<span data-ttu-id="fae63-120">다음 JSON 개체에 hello hello를 사용 하는 저장소 테이블 입력된 tooa 함수 hello `bindings` function.json의 배열:</span><span class="sxs-lookup"><span data-stu-id="fae63-120">hello Storage table input tooa function uses hello following JSON objects in hello `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "table",
    "direction": "in",
    "tableName": "<Name of Storage table>",
    "partitionKey": "<PartitionKey of table entity tooread - see below>",
    "rowKey": "<RowKey of table entity tooread - see below>",
    "take": "<Maximum number of entities tooread in Node.js - optional>",
    "filter": "<OData filter expression for table input in Node.js - optional>",
    "connection": "<Name of app setting - see below>",
}
```

<span data-ttu-id="fae63-121">참고 hello 다음.</span><span class="sxs-lookup"><span data-stu-id="fae63-121">Note hello following:</span></span> 

* <span data-ttu-id="fae63-122">사용 하 여 `partitionKey` 및 `rowKey` 함께 tooread 단일 엔터티.</span><span class="sxs-lookup"><span data-stu-id="fae63-122">Use `partitionKey` and `rowKey` together tooread a single entity.</span></span> <span data-ttu-id="fae63-123">이러한 속성은 선택적입니다.</span><span class="sxs-lookup"><span data-stu-id="fae63-123">These properties are optional.</span></span> 
* <span data-ttu-id="fae63-124">`connection`저장소 연결 문자열을 포함 하는 응용 프로그램 설정의 hello 이름을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fae63-124">`connection` must contain hello name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="fae63-125">Hello Azure 포털에서에서 hello의 표준 편집기 hello **통합** 계정 저장소를 만들 때 또는 기존 선택에 대 한 탭이 응용 프로그램 설정을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="fae63-125">In hello Azure portal, hello standard editor in hello **Integrate** tab configures this app setting for you when you create a Storage account or selects an existing one.</span></span> <span data-ttu-id="fae63-126">또한 [이 앱 설정을 수동으로 구성](functions-how-to-use-azure-function-app-settings.md#settings)할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fae63-126">You can also [configure this app setting manually](functions-how-to-use-azure-function-app-settings.md#settings).</span></span>  

<a name="inputusage"></a>

## <a name="input-usage"></a><span data-ttu-id="fae63-127">입력 사용</span><span class="sxs-lookup"><span data-stu-id="fae63-127">Input usage</span></span>
<span data-ttu-id="fae63-128">C# 함수를 바인딩할 있습니다 toohello 입력 테이블 엔터티 (또는 엔터티) 같은 프로그램 함수 서명에서 명명된 된 매개 변수를 사용 하 여 `<T> <name>`합니다.</span><span class="sxs-lookup"><span data-stu-id="fae63-128">In C# functions, you bind toohello input table entity (or entities) by using a named parameter in your function signature, like `<T> <name>`.</span></span>
<span data-ttu-id="fae63-129">여기서 `T` hello 데이터 형식은 toodeserialize hello 데이터를 지정 하 고 `paramName` hello 이름인 hello에 지정 된 [입력 바인딩의](#input)합니다.</span><span class="sxs-lookup"><span data-stu-id="fae63-129">Where `T` is hello data type that you want toodeserialize hello data into, and `paramName` is hello name you specified in hello [input binding](#input).</span></span> <span data-ttu-id="fae63-130">Hello 입력 테이블 엔터티 (또는 엔터티)를 사용 하 여 액세스 Node.js 함수에서 `context.bindings.<name>`합니다.</span><span class="sxs-lookup"><span data-stu-id="fae63-130">In Node.js functions, you access hello input table entity (or entities) using `context.bindings.<name>`.</span></span>

<span data-ttu-id="fae63-131">Node.js 또는 C# 함수 hello 입력된 데이터를 deserialize 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fae63-131">hello input data can be deserialized in Node.js or C# functions.</span></span> <span data-ttu-id="fae63-132">역직렬화 하는 hello 개체 `RowKey` 및 `PartitionKey` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="fae63-132">hello deserialized objects have `RowKey` and `PartitionKey` properties.</span></span>

<span data-ttu-id="fae63-133">C# 함수에서의 형식에 따라 hello tooany 바인딩할 수도 있습니다 런타임이 시도 하는 hello 함수 너무 데이터 및 deserialize hello 테이블 해당 형식을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="fae63-133">In C# functions, you can also bind tooany of hello following types, and hello Functions runtime will attempt too deserialize hello table data using that type:</span></span>

* <span data-ttu-id="fae63-134">구현하는 모든 형식 `ITableEntity`</span><span class="sxs-lookup"><span data-stu-id="fae63-134">Any type that implements `ITableEntity`</span></span>
* `IQueryable<T>`

<a name="inputsample"></a>

## <a name="input-sample"></a><span data-ttu-id="fae63-135">입력 샘플</span><span class="sxs-lookup"><span data-stu-id="fae63-135">Input sample</span></span>
<span data-ttu-id="fae63-136">Hello function.json 큐 트리거 tooread 단일 테이블 행을 사용 하 여 다음 있는 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fae63-136">Supposed you have hello following function.json, which uses a queue trigger tooread a single table row.</span></span> <span data-ttu-id="fae63-137">hello JSON 지정 `PartitionKey`  
 `RowKey`합니다.</span><span class="sxs-lookup"><span data-stu-id="fae63-137">hello JSON specifies `PartitionKey` 
`RowKey`.</span></span> <span data-ttu-id="fae63-138">`"rowKey": "{queueTrigger}"`hello 큐 메시지 문자열에서 해당 hello 행 키를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="fae63-138">`"rowKey": "{queueTrigger}"` indicates that hello row key comes from hello queue message string.</span></span>

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

<span data-ttu-id="fae63-139">단일 테이블 엔터티를 읽을 수 있는 hello 언어 관련 샘플을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="fae63-139">See hello language-specific sample that reads a single table entity.</span></span>

* [<span data-ttu-id="fae63-140">C#</span><span class="sxs-lookup"><span data-stu-id="fae63-140">C#</span></span>](#inputcsharp)
* [<span data-ttu-id="fae63-141">F#</span><span class="sxs-lookup"><span data-stu-id="fae63-141">F#</span></span>](#inputfsharp)
* [<span data-ttu-id="fae63-142">Node.JS</span><span class="sxs-lookup"><span data-stu-id="fae63-142">Node.js</span></span>](#inputnodejs)

<a name="inputcsharp"></a>

### <a name="input-sample-in-c"></a><span data-ttu-id="fae63-143">C#의 입력 샘플</span><span class="sxs-lookup"><span data-stu-id="fae63-143">Input sample in C#</span></span> #
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

### <a name="input-sample-in-f"></a><span data-ttu-id="fae63-144">F#의 입력 샘플</span><span class="sxs-lookup"><span data-stu-id="fae63-144">Input sample in F#</span></span> #
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

### <a name="input-sample-in-nodejs"></a><span data-ttu-id="fae63-145">Node.js에서 입력 샘플</span><span class="sxs-lookup"><span data-stu-id="fae63-145">Input sample in Node.js</span></span>
```javascript
module.exports = function (context, myQueueItem) {
    context.log('Node.js queue trigger function processed work item', myQueueItem);
    context.log('Person entity name: ' + context.bindings.personEntity.Name);
    context.done();
};
```

<a name="output"></a>

## <a name="storage-table-output-binding"></a><span data-ttu-id="fae63-146">Storage 테이블 출력 바인딩</span><span class="sxs-lookup"><span data-stu-id="fae63-146">Storage table output binding</span></span>
<span data-ttu-id="fae63-147">Azure 저장소 테이블 hello 바인딩 toowrite 엔터티 tooa 저장소 함수에서 테이블을 사용 하면 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="fae63-147">hello Azure Storage table output binding enables you toowrite entities tooa Storage table in your function.</span></span> 

<span data-ttu-id="fae63-148">다음 JSON 개체에 hello hello 함수를 사용 하는 저장소 테이블 출력 hello `bindings` function.json의 배열:</span><span class="sxs-lookup"><span data-stu-id="fae63-148">hello Storage table output for a function uses hello following JSON objects in hello `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "table",
    "direction": "out",
    "tableName": "<Name of Storage table>",
    "partitionKey": "<PartitionKey of table entity toowrite - see below>",
    "rowKey": "<RowKey of table entity toowrite - see below>",
    "connection": "<Name of app setting - see below>",
}
```

<span data-ttu-id="fae63-149">참고 hello 다음.</span><span class="sxs-lookup"><span data-stu-id="fae63-149">Note hello following:</span></span> 

* <span data-ttu-id="fae63-150">사용 하 여 `partitionKey` 및 `rowKey` 함께 toowrite 단일 엔터티.</span><span class="sxs-lookup"><span data-stu-id="fae63-150">Use `partitionKey` and `rowKey` together toowrite a single entity.</span></span> <span data-ttu-id="fae63-151">이러한 속성은 선택적입니다.</span><span class="sxs-lookup"><span data-stu-id="fae63-151">These properties are optional.</span></span> <span data-ttu-id="fae63-152">지정할 수 있습니다 `PartitionKey` 및 `RowKey` 개체를 만들 때는 hello 엔터티 함수 코드에서.</span><span class="sxs-lookup"><span data-stu-id="fae63-152">You can also specify `PartitionKey` and `RowKey` when you create hello entity objects in your function code.</span></span>
* <span data-ttu-id="fae63-153">`connection`저장소 연결 문자열을 포함 하는 응용 프로그램 설정의 hello 이름을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fae63-153">`connection` must contain hello name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="fae63-154">Hello Azure 포털에서에서 hello의 표준 편집기 hello **통합** 계정 저장소를 만들 때 또는 기존 선택에 대 한 탭이 응용 프로그램 설정을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="fae63-154">In hello Azure portal, hello standard editor in hello **Integrate** tab configures this app setting for you when you create a Storage account or selects an existing one.</span></span> <span data-ttu-id="fae63-155">또한 [이 앱 설정을 수동으로 구성](functions-how-to-use-azure-function-app-settings.md#settings)할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fae63-155">You can also [configure this app setting manually](functions-how-to-use-azure-function-app-settings.md#settings).</span></span> 

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="fae63-156">출력 사용</span><span class="sxs-lookup"><span data-stu-id="fae63-156">Output usage</span></span>
<span data-ttu-id="fae63-157">C# 함수를 명명 된 hello를 사용 하 여 toohello 테이블 출력 바인딩할 `out` 함수 시그니처의 매개 변수 같은 `out <T> <name>`여기서 `T` hello 데이터 형식은 tooserialize hello 데이터를 지정 하 고 `paramName` 는 hello 이름을 hello에 지정 된 [출력 바인딩이](#output)합니다.</span><span class="sxs-lookup"><span data-stu-id="fae63-157">In C# functions, you bind toohello table output by using hello named `out` parameter in your function signature, like `out <T> <name>`, where `T` is hello data type that you want tooserialize hello data into, and `paramName` is hello name you specified in hello [output binding](#output).</span></span> <span data-ttu-id="fae63-158">Node.js 함수 hello 표를 사용 하 여 출력 액세스 `context.bindings.<name>`합니다.</span><span class="sxs-lookup"><span data-stu-id="fae63-158">In Node.js functions, you access hello table output using `context.bindings.<name>`.</span></span>

<span data-ttu-id="fae63-159">Node.js 또는 C# 함수에서 개체를 직렬화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fae63-159">You can serialize objects in Node.js or C# functions.</span></span> <span data-ttu-id="fae63-160">C# 함수에서 유형만 toohello를 바인딩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fae63-160">In C# functions, you can also bind toohello following types:</span></span>

* <span data-ttu-id="fae63-161">구현하는 모든 형식 `ITableEntity`</span><span class="sxs-lookup"><span data-stu-id="fae63-161">Any type that implements `ITableEntity`</span></span>
* <span data-ttu-id="fae63-162">`ICollector<T>`(toooutput 여러 엔터티.</span><span class="sxs-lookup"><span data-stu-id="fae63-162">`ICollector<T>` (toooutput multiple entities.</span></span> <span data-ttu-id="fae63-163">[샘플](#outcsharp)을 참조하세요.)</span><span class="sxs-lookup"><span data-stu-id="fae63-163">See [sample](#outcsharp).)</span></span>
* <span data-ttu-id="fae63-164">`IAsyncCollector<T>`(비동기 버전의 `ICollector<T>`)</span><span class="sxs-lookup"><span data-stu-id="fae63-164">`IAsyncCollector<T>` (async version of `ICollector<T>`)</span></span>
* <span data-ttu-id="fae63-165">`CloudTable`(hello Azure 저장소 SDK를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fae63-165">`CloudTable` (using hello Azure Storage SDK.</span></span> <span data-ttu-id="fae63-166">[샘플](#readmulti)을 참조하세요.)</span><span class="sxs-lookup"><span data-stu-id="fae63-166">See [sample](#readmulti).)</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="fae63-167">출력 샘플</span><span class="sxs-lookup"><span data-stu-id="fae63-167">Output sample</span></span>
<span data-ttu-id="fae63-168">hello 다음 *function.json* 및 *run.csx* 예제와 방법을 toowrite 여러 테이블 엔터티.</span><span class="sxs-lookup"><span data-stu-id="fae63-168">hello following *function.json* and *run.csx* example shows how toowrite multiple table entities.</span></span>

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

<span data-ttu-id="fae63-169">여러 테이블 엔터티를 만드는 hello 언어 관련 샘플을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="fae63-169">See hello language-specific sample that creates multiple table entities.</span></span>

* [<span data-ttu-id="fae63-170">C#</span><span class="sxs-lookup"><span data-stu-id="fae63-170">C#</span></span>](#outcsharp)
* [<span data-ttu-id="fae63-171">F#</span><span class="sxs-lookup"><span data-stu-id="fae63-171">F#</span></span>](#outfsharp)
* [<span data-ttu-id="fae63-172">Node.JS</span><span class="sxs-lookup"><span data-stu-id="fae63-172">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="fae63-173">C#에서 출력 샘플</span><span class="sxs-lookup"><span data-stu-id="fae63-173">Output sample in C#</span></span> #
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

### <a name="output-sample-in-f"></a><span data-ttu-id="fae63-174">F#에서 출력 샘플</span><span class="sxs-lookup"><span data-stu-id="fae63-174">Output sample in F#</span></span> #
```fsharp
[<CLIMutable>]
type Person = {
  PartitionKey: string
  RowKey: string
  Name: string
}

let Run(input: string, tableBinding: ICollector<Person>, log: TraceWriter) =
    for i = 1 too10 do
        log.Info(sprintf "Adding Person entity %d" i)
        tableBinding.Add(
            { PartitionKey = "Test"
              RowKey = i.ToString()
              Name = "Name" + i.ToString() })
```

<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a><span data-ttu-id="fae63-175">Node.js에서 출력 샘플</span><span class="sxs-lookup"><span data-stu-id="fae63-175">Output sample in Node.js</span></span>
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

## <a name="sample-read-multiple-table-entities-in-c"></a><span data-ttu-id="fae63-176">샘플: C#에서 여러 테이블 엔터티 읽기</span><span class="sxs-lookup"><span data-stu-id="fae63-176">Sample: Read multiple table entities in C#</span></span>  #
<span data-ttu-id="fae63-177">hello 다음 *function.json* 및 C# 코드 예제에서는 hello 큐 메시지에 지정 된 파티션 키에 대 한 엔터티를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="fae63-177">hello following *function.json* and C# code example reads entities for a partition key that is specified in hello queue message.</span></span>

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

<span data-ttu-id="fae63-178">C# 코드 hello hello 엔터티 형식에서 파생 될 수 있도록 참조 toohello Azure 저장소 SDK를 추가 `TableEntity`합니다.</span><span class="sxs-lookup"><span data-stu-id="fae63-178">hello C# code adds a reference toohello Azure Storage SDK so that hello entity type can derive from `TableEntity`.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="fae63-179">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fae63-179">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]


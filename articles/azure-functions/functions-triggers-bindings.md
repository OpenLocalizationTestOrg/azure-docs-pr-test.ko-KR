---
title: "Azure Functions의 트리거 및 바인딩 작업 | Microsoft Docs"
description: "Azure Functions에서 트리거 및 바인딩을 사용하여 코드 실행을 온라인 이벤트 및 클라우드 기반 서비스에 연결하는 방법을 알아봅니다."
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "Azure Functions, 함수, 이벤트 처리, webhook, 동적 계산, 서버가 없는 아키텍처"
ms.assetid: cbc7460a-4d8a-423f-a63e-1cd33fef7252
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/30/2017
ms.author: donnam
ms.openlocfilehash: cc41debb2523df77be4db05817a4c7ac55604439
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-triggers-and-bindings-concepts"></a><span data-ttu-id="b7ed1-104">Azure Functions 트리거 및 바인딩 개념</span><span class="sxs-lookup"><span data-stu-id="b7ed1-104">Azure Functions triggers and bindings concepts</span></span>
<span data-ttu-id="b7ed1-105">Azure Functions에서는 *트리거* 및 *바인딩*을 통해 Azure 및 기타 서비스의 이벤트에 대응하는 코드를 쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-105">Azure Functions allows you to write code in response to events in Azure and other services, through *triggers* and *bindings*.</span></span> <span data-ttu-id="b7ed1-106">이 문서는 지원되는 모든 프로그래밍 언어의 트리거 및 바인딩에 대한 개념적 개요를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-106">This article is a conceptual overview of triggers and bindings for all supported programming languages.</span></span> <span data-ttu-id="b7ed1-107">여기에서는 모든 바인딩에 공통되는 기능을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-107">Features that are common to all bindings are described here.</span></span>

## <a name="overview"></a><span data-ttu-id="b7ed1-108">개요</span><span class="sxs-lookup"><span data-stu-id="b7ed1-108">Overview</span></span>

<span data-ttu-id="b7ed1-109">트리거와 바인딩은 함수가 호출되는 방식과 사용하는 데이터를 정의하는 선언적 방식입니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-109">Triggers and bindings are a declarative way to define how a function is invoked and what data it works with.</span></span> <span data-ttu-id="b7ed1-110">*트리거*는 함수가 호출되는 방식을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-110">A *trigger* defines how a function is invoked.</span></span> <span data-ttu-id="b7ed1-111">함수에는 정확히 하나의 트리거만 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-111">A function must have exactly one trigger.</span></span> <span data-ttu-id="b7ed1-112">트리거는 관련 데이터가 있으며, 이 데이터는 일반적으로 함수를 트리거한 페이로드입니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-112">Triggers have associated data, which is usually the payload that triggered the function.</span></span> 

<span data-ttu-id="b7ed1-113">입력 및 출력 *바인딩*은 코드에서 데이터에 연결하기 위한 선언적 방식을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-113">Input and output *bindings* provide a declarative way to connect to data from within your code.</span></span> <span data-ttu-id="b7ed1-114">트리거와 마찬가지로, 함수 구성에 연결 문자열과 기타 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-114">Similar to triggers, you specify connection strings and other properties in your function configuration.</span></span> <span data-ttu-id="b7ed1-115">바인딩은 선택 사항이며 함수는 여러 개의 입력 및 출력 바인딩을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-115">Bindings are optional and a function can have multiple input and output bindings.</span></span> 

<span data-ttu-id="b7ed1-116">트리거와 바인딩을 사용하면 더욱 일반적이면서 코드가 상호 작용하는 서비스의 상세 정보를 하드코딩하지 않는 코드를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-116">Using triggers and bindings, you can write code that is more generic and does not hardcode the details of the services with which it interacts.</span></span> <span data-ttu-id="b7ed1-117">서비스의 데이터가 함수 코드의 입력 값이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-117">Data coming from services simply become input values for your function code.</span></span> <span data-ttu-id="b7ed1-118">데이터를 다른 서비스(예: Azure Table Storage에서 새 행 만들기)로 출력하려면 메서드의 리턴값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-118">To output data to another service (such as creating a new row in Azure Table Storage), use the return value of the method.</span></span> <span data-ttu-id="b7ed1-119">복수 값을 출력해야 하는 경우에는 도우미 개체를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-119">Or, if you need to output multiple values, use a helper object.</span></span> <span data-ttu-id="b7ed1-120">트리거와 바인딩에는 **name** 속성이 있습니다. 이 속성은 바인딩에 액세스하기 위해 코드에서 사용하는 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-120">Triggers and bindings have a **name** property, which is an identifier you use in your code to access the binding.</span></span>

<span data-ttu-id="b7ed1-121">Azure Functions Portal의 **통합** 탭에서 트리거와 바인딩을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-121">You can configure triggers and bindings in the **Integrate** tab in the Azure Functions portal.</span></span> <span data-ttu-id="b7ed1-122">이때 UI는 function 디렉터리에 있는 *function.json* 파일을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-122">Under the covers, the UI modifies a file called *function.json* file in the function directory.</span></span> <span data-ttu-id="b7ed1-123">이 파일은 **고급 편집기**로 변경하여 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-123">You can edit this file by changing to the **Advanced editor**.</span></span>

<span data-ttu-id="b7ed1-124">다음 표에 Azure Functions에 지원되는 트리거와 바인딩이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-124">The following table shows the triggers and bindings that are supported with Azure Functions.</span></span> 

[!INCLUDE [Full bindings table](../../includes/functions-bindings.md)]

### <a name="example-queue-trigger-and-table-output-binding"></a><span data-ttu-id="b7ed1-125">예: 큐 트리거 및 테이블 출력 바인딩</span><span class="sxs-lookup"><span data-stu-id="b7ed1-125">Example: queue trigger and table output binding</span></span>

<span data-ttu-id="b7ed1-126">Azure Queue Storage에 새 메시지가 나타날 때마다 Azure Table Storage에 새 행을 쓰려는 경우를 가정하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-126">Suppose you want to write a new row to Azure Table Storage whenever a new message appears in Azure Queue Storage.</span></span> <span data-ttu-id="b7ed1-127">이 시나리오는 Azure Queue 트리거 및 Table 출력 바인딩을 사용하여 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-127">This scenario can be implemented using an Azure Queue trigger and a Table output binding.</span></span> 

<span data-ttu-id="b7ed1-128">큐 트리거는 **통합** 탭에 다음 정보가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-128">A queue trigger requires the following information in the **Integrate** tab:</span></span>

* <span data-ttu-id="b7ed1-129">큐에 대한 저장소 계정 연결 문자열이 포함된 앱 설정의 이름</span><span class="sxs-lookup"><span data-stu-id="b7ed1-129">The name of the app setting that contains the storage account connection string for the queue</span></span>
* <span data-ttu-id="b7ed1-130">큐 이름</span><span class="sxs-lookup"><span data-stu-id="b7ed1-130">The queue name</span></span>
* <span data-ttu-id="b7ed1-131">`order`와 같이 큐 메시지의 내용을 읽을 수 있는 코드 내 식별자</span><span class="sxs-lookup"><span data-stu-id="b7ed1-131">The identifier in your code to read the contents of the queue message, such as `order`.</span></span>

<span data-ttu-id="b7ed1-132">Azure Table Storage를 작성하려면 다음 정보로 출력 바인딩을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-132">To write to Azure Table Storage, use an output binding with the following details:</span></span>

* <span data-ttu-id="b7ed1-133">테이블의 저장소 계정 연결 문자열이 포함된 앱 설정의 이름</span><span class="sxs-lookup"><span data-stu-id="b7ed1-133">The name of the app setting that contains the storage account connection string for the table</span></span>
* <span data-ttu-id="b7ed1-134">테이블 이름</span><span class="sxs-lookup"><span data-stu-id="b7ed1-134">The table name</span></span>
* <span data-ttu-id="b7ed1-135">코드에서 출력 항목을 만들기 위한 식별자 또는 함수에서 반환된 값</span><span class="sxs-lookup"><span data-stu-id="b7ed1-135">The identifier in your code to create output items, or the return value from the function.</span></span>

<span data-ttu-id="b7ed1-136">바인딩은 *function.json*에 서비스 비밀이 포함되지 않은 모범 사례를 실행하기 위해 연결 문자열에 앱 설정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-136">Bindings use app settings for connection strings to enforce the best practice that *function.json* does not contain service secrets.</span></span>

<span data-ttu-id="b7ed1-137">그런 다음 코드에서 제공한 식별자를 사용하여 Azure Storage와 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-137">Then, use the identifiers you provided to integrate with Azure Storage in your code.</span></span>

```cs
#r "Newtonsoft.Json"

using Newtonsoft.Json.Linq;

// From an incoming queue message that is a JSON object, add fields and write to Table Storage
// The method return value creates a new row in Table Storage
public static Person Run(JObject order, TraceWriter log)
{
    return new Person() { 
            PartitionKey = "Orders", 
            RowKey = Guid.NewGuid().ToString(),  
            Name = order["Name"].ToString(),
            MobileNumber = order["MobileNumber"].ToString() };  
}
 
public class Person
{
    public string PartitionKey { get; set; }
    public string RowKey { get; set; }
    public string Name { get; set; }
    public string MobileNumber { get; set; }
}
```

```javascript
// From an incoming queue message that is a JSON object, add fields and write to Table Storage
// The second parameter to context.done is used as the value for the new row
module.exports = function (context, order) {
    order.PartitionKey = "Orders";
    order.RowKey = generateRandomId(); 

    context.done(null, order);
};

function generateRandomId() {
    return Math.random().toString(36).substring(2, 15) +
        Math.random().toString(36).substring(2, 15);
}
```

<span data-ttu-id="b7ed1-138">다음은 이전 코드에 해당하는 *function.json*입니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-138">Here is the *function.json* that corresponds to the preceding code.</span></span> <span data-ttu-id="b7ed1-139">함수 구현 언어와 상관없이 동일한 구성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-139">Note that the same configuration can be used, regardless of the language of the function implementation.</span></span>

```json
{
  "bindings": [
    {
      "name": "order",
      "type": "queueTrigger",
      "direction": "in",
      "queueName": "myqueue-items",
      "connection": "MY_STORAGE_ACCT_APP_SETTING"
    },
    {
      "name": "$return",
      "type": "table",
      "direction": "out",
      "tableName": "outTable",
      "connection": "MY_TABLE_STORAGE_ACCT_APP_SETTING"
    }
  ]
}
```
<span data-ttu-id="b7ed1-140">Azure Portal에서 *function.json*의 내용을 보고 편집하려면 함수의 **통합** 탭에서 **고급 편집기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-140">To view and edit the contents of *function.json* in the Azure portal, click the **Advanced editor** option on the **Integrate** tab of your function.</span></span>

<span data-ttu-id="b7ed1-141">Azure Storage 통합에 대한 추가 코드 예제와 상세 정보를 보려면 [Azure 저장소에 대한 Azure Functions 트리거 및 바인딩](functions-bindings-storage.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-141">For more code examples and details on integrating with Azure Storage, see [Azure Functions triggers and bindings for Azure Storage](functions-bindings-storage.md).</span></span>

### <a name="binding-direction"></a><span data-ttu-id="b7ed1-142">바인딩 방향</span><span class="sxs-lookup"><span data-stu-id="b7ed1-142">Binding direction</span></span>

<span data-ttu-id="b7ed1-143">모든 트리거와 바인딩에는 `direction` 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-143">All triggers and bindings have a `direction` property:</span></span>

- <span data-ttu-id="b7ed1-144">트리거의 경우 방향은 언제나 `in`입니다</span><span class="sxs-lookup"><span data-stu-id="b7ed1-144">For triggers, the direction is always `in`</span></span>
- <span data-ttu-id="b7ed1-145">입력 및 출력 바인딩은 `in`과 `out`을 사용합니다</span><span class="sxs-lookup"><span data-stu-id="b7ed1-145">Input and output bindings use `in` and `out`</span></span>
- <span data-ttu-id="b7ed1-146">일부 바인딩은 특수 방향인 `inout`을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-146">Some bindings support a special direction `inout`.</span></span> <span data-ttu-id="b7ed1-147">`inout`을 사용할 경우 **통합** 탭에서 **고급 편집기**만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-147">If you use `inout`, only the **Advanced editor** is available in the **Integrate** tab.</span></span>

## <a name="using-the-function-return-type-to-return-a-single-output"></a><span data-ttu-id="b7ed1-148">함수 반환 유형을 사용하여 단일 출력 반환</span><span class="sxs-lookup"><span data-stu-id="b7ed1-148">Using the function return type to return a single output</span></span>

<span data-ttu-id="b7ed1-149">위의 예제는 함수의 반환값을 사용하여 바인딩에 출력을 제공하는 방법을 보여줍니다. 이 경우 특수 이름 매개 변수인 `$return`을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-149">The preceding example shows how to use the function return value to provide output to a binding, which is achieved by using the special name parameter `$return`.</span></span> <span data-ttu-id="b7ed1-150">(C#, JavaScript, F#과 같이 반환값이 있는 언어에서만 지원됩니다.) 함수에 복수의 출력 바인딩이 있는 경우 출력 바인딩 중 하나에 대해서만 `$return`을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-150">(This is only supported in languages that have a return value, such as C#, JavaScript, and F#.) If a function has multiple output bindings, use `$return` for only one of the output bindings.</span></span> 

```json
// excerpt of function.json
{
    "name": "$return",
    "type": "blob",
    "direction": "out",
    "path": "output-container/{id}"
}
```

<span data-ttu-id="b7ed1-151">아래 예제는 C#, JavaScript, F#에서 반환 형식이 출력 바인딩과 함께 사용되는 방식을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-151">The examples below show how return types are used with output bindings in C#, JavaScript, and F#.</span></span>

```cs
// C# example: use method return value for output binding
public static string Run(WorkItem input, TraceWriter log)
{
    string json = string.Format("{{ \"id\": \"{0}\" }}", input.Id);
    log.Info($"C# script processed queue message. Item={json}");
    return json;
}
```

```cs
// C# example: async method, using return value for output binding
public static Task<string> Run(WorkItem input, TraceWriter log)
{
    string json = string.Format("{{ \"id\": \"{0}\" }}", input.Id);
    log.Info($"C# script processed queue message. Item={json}");
    return json;
}
```

```javascript
// JavaScript: return a value in the second parameter to context.done
module.exports = function (context, input) {
    var json = JSON.stringify(input);
    context.log('Node.js script processed queue message', json);
    context.done(null, json);
}
```

```fsharp
// F# example: use return value for output binding
let Run(input: WorkItem, log: TraceWriter) =
    let json = String.Format("{{ \"id\": \"{0}\" }}", input.Id)   
    log.Info(sprintf "F# script processed queue message '%s'" json)
    json
```

## <a name="binding-datatype-property"></a><span data-ttu-id="b7ed1-152">dataType 속성 바인딩</span><span class="sxs-lookup"><span data-stu-id="b7ed1-152">Binding dataType property</span></span>

<span data-ttu-id="b7ed1-153">.NET에서는 형식을 사용하여 입력 데이터에 대한 데이터 형식을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-153">In .NET, use the types to define the data type for input data.</span></span> <span data-ttu-id="b7ed1-154">예를 들어 `string`을 사용하여 이진으로 읽을 바이트 배열 및 큐 트리거의 텍스트에 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-154">For instance, use `string` to bind to the text of a queue trigger and a byte array to read as binary.</span></span>

<span data-ttu-id="b7ed1-155">JavaScript와 같은 동적으로 형식화되는 언어의 경우 바인딩 정의에 `dataType` 속성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-155">For languages that are dynamically typed such as JavaScript, use the `dataType` property in the binding definition.</span></span> <span data-ttu-id="b7ed1-156">예를 들어 이진 형식의 HTTP 요청 내용을 읽으려면 `binary` 형식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-156">For example, to read the content of an HTTP request in binary format, use the type `binary`:</span></span>

```json
{
    "type": "httpTrigger",
    "name": "req",
    "direction": "in",
    "dataType": "binary"
}
```

<span data-ttu-id="b7ed1-157">`dataType`에 대한 다른 옵션은 `stream` 및 `string`입니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-157">Other options for `dataType` are `stream` and `string`.</span></span>

## <a name="resolving-app-settings"></a><span data-ttu-id="b7ed1-158">앱 설정 해결</span><span class="sxs-lookup"><span data-stu-id="b7ed1-158">Resolving app settings</span></span>
<span data-ttu-id="b7ed1-159">비밀과 연결 문자열은 구성 파일이 아닌 앱 설정을 사용하여 관리하는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-159">As a best practice, secrets and connection strings should be managed using app settings, rather than configuration files.</span></span> <span data-ttu-id="b7ed1-160">그럴 경우 이러한 비밀에 대한 액세스가 제한되고 *function.json*을 공용 원본 제어 리포지토리에 안전하게 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-160">This limits access to these secrets and makes it safe to store *function.json* in a public source control repository.</span></span>

<span data-ttu-id="b7ed1-161">환경을 기준으로 구성을 변경하려는 경우에도 앱 설정이 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-161">App settings are also useful whenever you want to change configuration based on the environment.</span></span> <span data-ttu-id="b7ed1-162">예를 들어 테스트 환경에서 다른 큐 또는 Blob Storage 컨테이너를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-162">For example, in a test environment, you may want to monitor a different queue or blob storage container.</span></span>

<span data-ttu-id="b7ed1-163">앱 설정은 `%MyAppSetting%`과 같이 값이 퍼센트 기호로 둘러싸인 경우에만 확인됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-163">App settings are resolved whenever a value is enclosed in percent signs, such as `%MyAppSetting%`.</span></span> <span data-ttu-id="b7ed1-164">트리거 및 바인딩의 `connection` 속성은 특수한 경우이며 앱 설정으로 값을 자동 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-164">Note that the `connection` property of triggers and bindings is a special case and automatically resolves values as app settings.</span></span> 

<span data-ttu-id="b7ed1-165">다음 예제는 `%input-queue-name%` 앱 설정을 사용하여 트리거할 큐를 정의하는 큐 트리거입니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-165">The following example is a queue trigger that uses an app setting `%input-queue-name%` to define the queue to trigger on.</span></span>

```json
{
  "bindings": [
    {
      "name": "order",
      "type": "queueTrigger",
      "direction": "in",
      "queueName": "%input-queue-name%",
      "connection": "MY_STORAGE_ACCT_APP_SETTING"
    }
  ]
}
```

## <a name="trigger-metadata-properties"></a><span data-ttu-id="b7ed1-166">트리거 메타데이터 속성</span><span class="sxs-lookup"><span data-stu-id="b7ed1-166">Trigger metadata properties</span></span>

<span data-ttu-id="b7ed1-167">트리거가 제공한 데이터 페이로드(예: 함수를 트리거한 큐 메시지) 이외에 많은 트리거가 추가 메타데이터 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-167">In addition to the data payload provided by a trigger (such as the queue message that triggered a function), many triggers provide additional metadata values.</span></span> <span data-ttu-id="b7ed1-168">이러한 값은 C# 및 F#에서 입력 매개 변수로 사용하거나 JavaScript에서 `context.bindings` 개체의 속성으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-168">These values can be used as input parameters in C# and F# or properties on the `context.bindings` object in JavaScript.</span></span> 

<span data-ttu-id="b7ed1-169">예를 들어 큐 트리거는 다음 속성을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-169">For example, a queue trigger supports the following properties:</span></span>

* <span data-ttu-id="b7ed1-170">QueueTrigger - 유효한 문자열인 경우 트리거 메시지 내용</span><span class="sxs-lookup"><span data-stu-id="b7ed1-170">QueueTrigger - triggering message content if a valid string</span></span>
* <span data-ttu-id="b7ed1-171">DequeueCount</span><span class="sxs-lookup"><span data-stu-id="b7ed1-171">DequeueCount</span></span>
* <span data-ttu-id="b7ed1-172">ExpirationTime</span><span class="sxs-lookup"><span data-stu-id="b7ed1-172">ExpirationTime</span></span>
* <span data-ttu-id="b7ed1-173">Id</span><span class="sxs-lookup"><span data-stu-id="b7ed1-173">Id</span></span>
* <span data-ttu-id="b7ed1-174">InsertionTime</span><span class="sxs-lookup"><span data-stu-id="b7ed1-174">InsertionTime</span></span>
* <span data-ttu-id="b7ed1-175">NextVisibleTime</span><span class="sxs-lookup"><span data-stu-id="b7ed1-175">NextVisibleTime</span></span>
* <span data-ttu-id="b7ed1-176">PopReceipt</span><span class="sxs-lookup"><span data-stu-id="b7ed1-176">PopReceipt</span></span>

<span data-ttu-id="b7ed1-177">각 트리거의 메타데이터 속성은 해당 참조 항목에서 자세히 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-177">Details of metadata properties for each trigger are described in the corresponding reference topic.</span></span> <span data-ttu-id="b7ed1-178">설명서는 Portal에서 **통합** 탭의 바인딩 구성 영역 아래 **설명서** 섹션에서도 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-178">Documentation is also available in the **Integrate** tab of the portal, in the **Documentation** section below the binding configuration area.</span></span>  

<span data-ttu-id="b7ed1-179">예를 들어 Blob 트리거는 약간의 지연이 있으므로 큐 트리거를 사용하여 함수를 실행합니다([Blob Storage 트리거](functions-bindings-storage-blob.md#storage-blob-trigger) 참조).</span><span class="sxs-lookup"><span data-stu-id="b7ed1-179">For example, since blob triggers have some delays, you can use a queue trigger to run your function (see [Blob Storage Trigger](functions-bindings-storage-blob.md#storage-blob-trigger).</span></span> <span data-ttu-id="b7ed1-180">큐 메시지에는 트리거할 Blob 파일 이름이 있는 경우가 일반적입니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-180">The queue message would contain the blob filename to trigger on.</span></span> <span data-ttu-id="b7ed1-181">`queueTrigger` 메타데이터 속성을 사용하면 코드가 아닌 구성에서 이 동작을 모두 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-181">Using the `queueTrigger` metadata property, you can specify this behavior all in your configuration, rather than your code.</span></span>

```json
  "bindings": [
    {
      "name": "myQueueItem",
      "type": "queueTrigger",
      "queueName": "myqueue-items",
      "connection": "MyStorageConnection",
    },
    {
      "name": "myInputBlob",
      "type": "blob",
      "path": "samples-workitems/{queueTrigger}",
      "direction": "in",
      "connection": "MyStorageConnection"
    }
  ]
```

<span data-ttu-id="b7ed1-182">트리거의 메타데이터 속성도 다음 섹션에서 설명하는 바와 같이 다른 바인딩에 대한 *바인딩 식*에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-182">Metadata properties from a trigger can also be used in a *binding expression* for another binding, as described in the following section.</span></span>

## <a name="binding-expressions-and-patterns"></a><span data-ttu-id="b7ed1-183">바인딩 식 및 패턴</span><span class="sxs-lookup"><span data-stu-id="b7ed1-183">Binding expressions and patterns</span></span>

<span data-ttu-id="b7ed1-184">트리거와 바인딩의 가장 강력한 기능 중 하나는 *바인딩 식*입니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-184">One of the most powerful features of triggers and bindings is *binding expressions*.</span></span> <span data-ttu-id="b7ed1-185">바인딩 안에서 패턴 식을 정의한 다음 다른 바인딩 또는 코드에서 이 패턴 식을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-185">Within your binding, you can define pattern expressions which can then be used in other bindings or your code.</span></span> <span data-ttu-id="b7ed1-186">위 섹션의 샘플과 같이, 트리거 메타데이터도 바인딩 식에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-186">Trigger metadata can also be used in binding expressions, as show in the sample in the preceding section.</span></span>

<span data-ttu-id="b7ed1-187">예를 들어 **새 함수** 페이지의 **이미지 크기 조정** 템플릿과 같이 특정 Blob Storage 컨테이너에서 이미지 크기를 조정하려는 경우를 가정하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-187">For example, suppose you want to resize images in particular blob storage container, similar to the **Image Resizer** template in the **New Function** page.</span></span> <span data-ttu-id="b7ed1-188">**새 함수** -> 언어 **C#** -> 시나리오 **샘플** -> **ImageResizer-CSharp**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-188">Go to **New Function** -> Language **C#** -> Scenario **Samples** -> **ImageResizer-CSharp**.</span></span> 

<span data-ttu-id="b7ed1-189">*function.json* 정의는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-189">Here is the *function.json* definition:</span></span>

```json
{
  "bindings": [
    {
      "name": "image",
      "type": "blobTrigger",
      "path": "sample-images/{filename}",
      "direction": "in",
      "connection": "MyStorageConnection"
    },
    {
      "name": "imageSmall",
      "type": "blob",
      "path": "sample-images-sm/{filename}",
      "direction": "out",
      "connection": "MyStorageConnection"
    }
  ],
}
```

<span data-ttu-id="b7ed1-190">Blob 트리거 정의와 Blob 출력 바인딩에 `filename` 매개 변수가 사용되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-190">Notice that the `filename` parameter is used in both the blob trigger definition as well as the blob output binding.</span></span> <span data-ttu-id="b7ed1-191">이 매개 변수는 함수 코드에서도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-191">This parameter can also be used in function code.</span></span>

```csharp
// C# example of binding to {filename}
public static void Run(Stream image, string filename, Stream imageSmall, TraceWriter log)  
{
    log.Info($"Blob trigger processing: {filename}");
    // ...
} 
```

<!--TODO: add JavaScript example -->
<!-- Blocked by bug https://github.com/Azure/Azure-Functions/issues/248 -->


### <a name="random-guids"></a><span data-ttu-id="b7ed1-192">임의 GUID</span><span class="sxs-lookup"><span data-stu-id="b7ed1-192">Random GUIDs</span></span>
<span data-ttu-id="b7ed1-193">Azure Functions는 `{rand-guid}` 바인딩 식을 통해 바인딩에서 GUID를 편리하게 생성할 수 있는 구문을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-193">Azure Functions provides a convenience syntax for generating GUIDs in your bindings, through the `{rand-guid}` binding expression.</span></span> <span data-ttu-id="b7ed1-194">다음 예제는 이 식을 사용하여 고유한 Blob 이름을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-194">The following example uses this to generate a unique blob name:</span></span> 

```json
{
  "type": "blob",
  "name": "blobOutput",
  "direction": "out",
  "path": "my-output-container/{rand-guid}"
}
```

### <a name="current-time"></a><span data-ttu-id="b7ed1-195">현재 시간</span><span class="sxs-lookup"><span data-stu-id="b7ed1-195">Current time</span></span>

<span data-ttu-id="b7ed1-196">`DateTime.UtcNow`로 확인되는 바인딩 식 `DateTime`을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-196">You can use the binding expression `DateTime`, which resolves to `DateTime.UtcNow`.</span></span>

```json
{
  "type": "blob",
  "name": "blobOutput",
  "direction": "out",
  "path": "my-output-container/{DateTime}"
}
```

## <a name="bind-to-custom-input-properties-in-a-binding-expression"></a><span data-ttu-id="b7ed1-197">바인딩 식에서 사용자 지정 입력 속성에 바인딩</span><span class="sxs-lookup"><span data-stu-id="b7ed1-197">Bind to custom input properties in a binding expression</span></span>

<span data-ttu-id="b7ed1-198">바인딩 식은 트리거 페이로드 자체에 정의된 속성도 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-198">Binding expressions can also reference properties that are defined in the trigger payload itself.</span></span> <span data-ttu-id="b7ed1-199">예를 들어 webhook에 제공된 파일 이름에서 Blob Storage 파일에 동적으로 바인딩하는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-199">For example, you may want to dynamically bind to a blob storage file from a filename provided in a webhook.</span></span>

<span data-ttu-id="b7ed1-200">예를 들어 다음 *function.json*은 트리거 페이로드에서 `BlobName`이라는 속성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-200">For example, the following *function.json* uses a property called `BlobName` from the trigger payload:</span></span>

```json
{
  "bindings": [
    {
      "name": "info",
      "type": "httpTrigger",
      "direction": "in",
      "webHookType": "genericJson",
    },
    {
      "name": "blobContents",
      "type": "blob",
      "direction": "in",
      "path": "strings/{BlobName}",
      "connection": "AzureWebJobsStorage"
    },
    {
      "name": "res",
      "type": "http",
      "direction": "out"
    }
  ]
}
```

<span data-ttu-id="b7ed1-201">C# 및 F#에서 이를 달성하려면 트리거 페이로드에서 deserialize되는 필드를 정의하는 POCO를 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-201">To accomplish this in C# and F#, you must define a POCO that defines the fields that will be deserialized in the trigger payload.</span></span>

```csharp
using System.Net;

public class BlobInfo
{
    public string BlobName { get; set; }
}
  
public static HttpResponseMessage Run(HttpRequestMessage req, BlobInfo info, string blobContents)
{
    if (blobContents == null) {
        return req.CreateResponse(HttpStatusCode.NotFound);
    } 

    return req.CreateResponse(HttpStatusCode.OK, new {
        data = $"{blobContents}"
    });
}
```

<span data-ttu-id="b7ed1-202">JavaScript에서 JSON deserialization은 자동으로 실행되며 속성을 직접 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-202">In JavaScript, JSON deserialization is automatically performed and you can use the properties directly.</span></span>

```javascript
module.exports = function (context, info) {
    if ('BlobName' in info) {
        context.res = {
            body: { 'data': context.bindings.blobContents }
        }
    }
    else {
        context.res = {
            status: 404
        };
    }
    context.done();
}
```

## <a name="configuring-binding-data-at-runtime"></a><span data-ttu-id="b7ed1-203">런타임에 바인딩 데이터 구성</span><span class="sxs-lookup"><span data-stu-id="b7ed1-203">Configuring binding data at runtime</span></span>

<span data-ttu-id="b7ed1-204">C# 및 기타 .NET 언어에서는 *function.json*의 선언적 바인딩과 달리 명령적 바인딩 패턴을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-204">In C# and other .NET languages, you can use an imperative binding pattern, as opposed to the declarative bindings in *function.json*.</span></span> <span data-ttu-id="b7ed1-205">명령적 바인딩은 바인딩 매개 변수를 디자인 타임이 아닌 런타임에 계산해야 할 경우 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-205">Imperative binding is useful when binding parameters need to be computed at runtime rather than design time.</span></span> <span data-ttu-id="b7ed1-206">자세한 내용은 C# 개발자 참조에서 [명령적 바인딩을 통해 런타임 시 바인딩](functions-reference-csharp.md#imperative-bindings)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-206">To learn more, see [Binding at runtime via imperative bindings](functions-reference-csharp.md#imperative-bindings) in the C# developer reference.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b7ed1-207">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b7ed1-207">Next steps</span></span>
<span data-ttu-id="b7ed1-208">특성 바인딩에 대한 자세한 내용은 다음 문서를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="b7ed1-208">For more information on a specific binding, see the following articles:</span></span>

- [<span data-ttu-id="b7ed1-209">HTTP 및 webhook</span><span class="sxs-lookup"><span data-stu-id="b7ed1-209">HTTP and webhooks</span></span>](functions-bindings-http-webhook.md)
- [<span data-ttu-id="b7ed1-210">타이머</span><span class="sxs-lookup"><span data-stu-id="b7ed1-210">Timer</span></span>](functions-bindings-timer.md)
- [<span data-ttu-id="b7ed1-211">큐 저장소</span><span class="sxs-lookup"><span data-stu-id="b7ed1-211">Queue storage</span></span>](functions-bindings-storage-queue.md)
- [<span data-ttu-id="b7ed1-212">Blob 저장소</span><span class="sxs-lookup"><span data-stu-id="b7ed1-212">Blob storage</span></span>](functions-bindings-storage-blob.md)
- [<span data-ttu-id="b7ed1-213">Table Storage</span><span class="sxs-lookup"><span data-stu-id="b7ed1-213">Table storage</span></span>](functions-bindings-storage-table.md)
- [<span data-ttu-id="b7ed1-214">이벤트 허브</span><span class="sxs-lookup"><span data-stu-id="b7ed1-214">Event Hub</span></span>](functions-bindings-event-hubs.md)
- [<span data-ttu-id="b7ed1-215">서비스 버스</span><span class="sxs-lookup"><span data-stu-id="b7ed1-215">Service Bus</span></span>](functions-bindings-service-bus.md)
- [<span data-ttu-id="b7ed1-216">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b7ed1-216">Cosmos DB</span></span>](functions-bindings-documentdb.md)
- [<span data-ttu-id="b7ed1-217">SendGrid</span><span class="sxs-lookup"><span data-stu-id="b7ed1-217">SendGrid</span></span>](functions-bindings-sendgrid.md)
- [<span data-ttu-id="b7ed1-218">Twilio</span><span class="sxs-lookup"><span data-stu-id="b7ed1-218">Twilio</span></span>](functions-bindings-twilio.md)
- [<span data-ttu-id="b7ed1-219">알림 허브</span><span class="sxs-lookup"><span data-stu-id="b7ed1-219">Notification Hubs</span></span>](functions-bindings-notification-hubs.md)
- [<span data-ttu-id="b7ed1-220">모바일 앱</span><span class="sxs-lookup"><span data-stu-id="b7ed1-220">Mobile Apps</span></span>](functions-bindings-mobile-apps.md)
- [<span data-ttu-id="b7ed1-221">외부 파일</span><span class="sxs-lookup"><span data-stu-id="b7ed1-221">External file</span></span>](functions-bindings-external-file.md)

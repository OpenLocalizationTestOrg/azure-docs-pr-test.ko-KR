---
title: "트리거 및 Azure 함수에서 바인딩을 사용 하 여 aaaWork | Microsoft Docs"
description: "코드 실행 tooonline 이벤트 및 클라우드 기반 서비스 toouse 트리거합니다 방법 및 Azure 함수 tooconnect에 바인딩에 알아봅니다."
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
ms.openlocfilehash: eb2ebfca172fcc8c0f479adbcfec99e90fc33615
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-triggers-and-bindings-concepts"></a><span data-ttu-id="f452d-104">Azure Functions 트리거 및 바인딩 개념</span><span class="sxs-lookup"><span data-stu-id="f452d-104">Azure Functions triggers and bindings concepts</span></span>
<span data-ttu-id="f452d-105">Azure 기능 사용 하면 Azure 및 다른 서비스에서 응답 tooevents의 toowrite 코드를 통해 *트리거* 및 *바인딩*합니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-105">Azure Functions allows you toowrite code in response tooevents in Azure and other services, through *triggers* and *bindings*.</span></span> <span data-ttu-id="f452d-106">이 문서는 지원되는 모든 프로그래밍 언어의 트리거 및 바인딩에 대한 개념적 개요를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-106">This article is a conceptual overview of triggers and bindings for all supported programming languages.</span></span> <span data-ttu-id="f452d-107">일반적인 tooall 바인딩이 기능 여기 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-107">Features that are common tooall bindings are described here.</span></span>

## <a name="overview"></a><span data-ttu-id="f452d-108">개요</span><span class="sxs-lookup"><span data-stu-id="f452d-108">Overview</span></span>

<span data-ttu-id="f452d-109">트리거 및 바인딩은 선언적으로 toodefine는 함수를 호출 하는 방법 및 데이터와 함께 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-109">Triggers and bindings are a declarative way toodefine how a function is invoked and what data it works with.</span></span> <span data-ttu-id="f452d-110">*트리거*는 함수가 호출되는 방식을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-110">A *trigger* defines how a function is invoked.</span></span> <span data-ttu-id="f452d-111">함수에는 정확히 하나의 트리거만 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-111">A function must have exactly one trigger.</span></span> <span data-ttu-id="f452d-112">트리거는 hello 함수를 트리거 hello 페이로드는 일반적으로 데이터에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-112">Triggers have associated data, which is usually hello payload that triggered hello function.</span></span> 

<span data-ttu-id="f452d-113">입력 및 출력 *바인딩* 코드 내에서 선언적으로 tooconnect toodata를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-113">Input and output *bindings* provide a declarative way tooconnect toodata from within your code.</span></span> <span data-ttu-id="f452d-114">비슷한 tootriggers 함수 구성에 연결 문자열 및 기타 속성 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-114">Similar tootriggers, you specify connection strings and other properties in your function configuration.</span></span> <span data-ttu-id="f452d-115">바인딩은 선택 사항이며 함수는 여러 개의 입력 및 출력 바인딩을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-115">Bindings are optional and a function can have multiple input and output bindings.</span></span> 

<span data-ttu-id="f452d-116">트리거 및 바인딩을 사용 하 여, 보다 일반적인있지 않습니다 작용할 hello 서비스의 hello 정보를 하드 코드 되어 코드를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-116">Using triggers and bindings, you can write code that is more generic and does not hardcode hello details of hello services with which it interacts.</span></span> <span data-ttu-id="f452d-117">서비스의 데이터가 함수 코드의 입력 값이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-117">Data coming from services simply become input values for your function code.</span></span> <span data-ttu-id="f452d-118">toooutput 데이터 tooanother 서비스 (예: 새 행의 Azure 테이블 저장소)를 만드는 hello hello 메서드의 반환 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-118">toooutput data tooanother service (such as creating a new row in Azure Table Storage), use hello return value of hello method.</span></span> <span data-ttu-id="f452d-119">또는 여러 값 toooutput 해야 할 경우 도우미 개체를 사용 하세요.</span><span class="sxs-lookup"><span data-stu-id="f452d-119">Or, if you need toooutput multiple values, use a helper object.</span></span> <span data-ttu-id="f452d-120">트리거 및 바인딩은 **이름** 식별자 코드 tooaccess hello 바인딩을에서 사용 하는 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-120">Triggers and bindings have a **name** property, which is an identifier you use in your code tooaccess hello binding.</span></span>

<span data-ttu-id="f452d-121">Hello에 트리거 및 바인딩을 구성할 수 있습니다 **통합** hello 함수 Azure 포털에서 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-121">You can configure triggers and bindings in hello **Integrate** tab in hello Azure Functions portal.</span></span> <span data-ttu-id="f452d-122">Hello UI hello에서는 라는 파일을 수정 *function.json* hello 함수 디렉터리의 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-122">Under hello covers, hello UI modifies a file called *function.json* file in hello function directory.</span></span> <span data-ttu-id="f452d-123">Toohello 변경 하 여이 파일을 편집할 수 **고급 편집기**합니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-123">You can edit this file by changing toohello **Advanced editor**.</span></span>

<span data-ttu-id="f452d-124">hello 다음 표에 hello 트리거 및 Azure 함수로 지원 되는 바인딩에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-124">hello following table shows hello triggers and bindings that are supported with Azure Functions.</span></span> 

[!INCLUDE [Full bindings table](../../includes/functions-bindings.md)]

### <a name="example-queue-trigger-and-table-output-binding"></a><span data-ttu-id="f452d-125">예: 큐 트리거 및 테이블 출력 바인딩</span><span class="sxs-lookup"><span data-stu-id="f452d-125">Example: queue trigger and table output binding</span></span>

<span data-ttu-id="f452d-126">Azure 큐 저장소에 새 메시지가 표시 될 때마다 새 행 tooAzure 테이블 저장소 toowrite 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-126">Suppose you want toowrite a new row tooAzure Table Storage whenever a new message appears in Azure Queue Storage.</span></span> <span data-ttu-id="f452d-127">이 시나리오는 Azure Queue 트리거 및 Table 출력 바인딩을 사용하여 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-127">This scenario can be implemented using an Azure Queue trigger and a Table output binding.</span></span> 

<span data-ttu-id="f452d-128">큐 트리거 hello 다음 hello에 대 한 정보를 필요 **통합** 탭:</span><span class="sxs-lookup"><span data-stu-id="f452d-128">A queue trigger requires hello following information in hello **Integrate** tab:</span></span>

* <span data-ttu-id="f452d-129">hello hello 큐에 대 한 저장소 계정 연결 문자열을 포함 하는 hello 앱 설정의 hello 이름</span><span class="sxs-lookup"><span data-stu-id="f452d-129">hello name of hello app setting that contains hello storage account connection string for hello queue</span></span>
* <span data-ttu-id="f452d-130">hello 큐 이름</span><span class="sxs-lookup"><span data-stu-id="f452d-130">hello queue name</span></span>
* <span data-ttu-id="f452d-131">프로그램 코드 tooread hello hello 큐 메시지의 내용에는 식별자와 같은 hello `order`합니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-131">hello identifier in your code tooread hello contents of hello queue message, such as `order`.</span></span>

<span data-ttu-id="f452d-132">다음 세부 정보는 hello로 출력 바인딩을 사용 하는 테이블 저장소 toowrite tooAzure:</span><span class="sxs-lookup"><span data-stu-id="f452d-132">toowrite tooAzure Table Storage, use an output binding with hello following details:</span></span>

* <span data-ttu-id="f452d-133">hello hello 테이블에 대 한 저장소 계정 연결 문자열을 포함 하는 hello 앱 설정의 hello 이름</span><span class="sxs-lookup"><span data-stu-id="f452d-133">hello name of hello app setting that contains hello storage account connection string for hello table</span></span>
* <span data-ttu-id="f452d-134">hello 테이블 이름</span><span class="sxs-lookup"><span data-stu-id="f452d-134">hello table name</span></span>
* <span data-ttu-id="f452d-135">hello 식별자 코드 toocreate에서 항목 또는 hello hello 함수의 반환 값을 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-135">hello identifier in your code toocreate output items, or hello return value from hello function.</span></span>

<span data-ttu-id="f452d-136">바인딩에 연결 문자열 tooenforce hello 모범 사례에 대 한 응용 프로그램 설정을 사용 하 여 *function.json* 서비스 암호가 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-136">Bindings use app settings for connection strings tooenforce hello best practice that *function.json* does not contain service secrets.</span></span>

<span data-ttu-id="f452d-137">그런 다음 코드에서 Azure 저장소와 toointegrate를 제공 하는 hello 식별자를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-137">Then, use hello identifiers you provided toointegrate with Azure Storage in your code.</span></span>

```cs
#r "Newtonsoft.Json"

using Newtonsoft.Json.Linq;

// From an incoming queue message that is a JSON object, add fields and write tooTable Storage
// hello method return value creates a new row in Table Storage
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
// From an incoming queue message that is a JSON object, add fields and write tooTable Storage
// hello second parameter toocontext.done is used as hello value for hello new row
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

<span data-ttu-id="f452d-138">여기에 hello *function.json* toohello 코드 앞에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-138">Here is hello *function.json* that corresponds toohello preceding code.</span></span> <span data-ttu-id="f452d-139">동일한 구성을 사용할 수 hello 함수 구현 hello 언어에 관계 없이 해당 hello를 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-139">Note that hello same configuration can be used, regardless of hello language of hello function implementation.</span></span>

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
<span data-ttu-id="f452d-140">tooview 및 편집 hello 내용을 *function.json* hello Azure 포털에서에서 클릭 hello **고급 편집기** hello에 대 한 옵션 **통합** 함수의 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-140">tooview and edit hello contents of *function.json* in hello Azure portal, click hello **Advanced editor** option on hello **Integrate** tab of your function.</span></span>

<span data-ttu-id="f452d-141">Azure Storage 통합에 대한 추가 코드 예제와 상세 정보를 보려면 [Azure 저장소에 대한 Azure Functions 트리거 및 바인딩](functions-bindings-storage.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f452d-141">For more code examples and details on integrating with Azure Storage, see [Azure Functions triggers and bindings for Azure Storage](functions-bindings-storage.md).</span></span>

### <a name="binding-direction"></a><span data-ttu-id="f452d-142">바인딩 방향</span><span class="sxs-lookup"><span data-stu-id="f452d-142">Binding direction</span></span>

<span data-ttu-id="f452d-143">모든 트리거와 바인딩에는 `direction` 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-143">All triggers and bindings have a `direction` property:</span></span>

- <span data-ttu-id="f452d-144">트리거의 경우 hello 방향은 항상`in`</span><span class="sxs-lookup"><span data-stu-id="f452d-144">For triggers, hello direction is always `in`</span></span>
- <span data-ttu-id="f452d-145">입력 및 출력 바인딩은 `in`과 `out`을 사용합니다</span><span class="sxs-lookup"><span data-stu-id="f452d-145">Input and output bindings use `in` and `out`</span></span>
- <span data-ttu-id="f452d-146">일부 바인딩은 특수 방향인 `inout`을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-146">Some bindings support a special direction `inout`.</span></span> <span data-ttu-id="f452d-147">사용 하는 경우 `inout`만 hello **고급 편집기** hello에서 사용할 수 **통합** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-147">If you use `inout`, only hello **Advanced editor** is available in hello **Integrate** tab.</span></span>

## <a name="using-hello-function-return-type-tooreturn-a-single-output"></a><span data-ttu-id="f452d-148">Hello 함수 반환 형식 tooreturn 단일 출력을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="f452d-148">Using hello function return type tooreturn a single output</span></span>

<span data-ttu-id="f452d-149">hello 앞의 예제를 보여 줍니다 toouse hello 함수 반환 값 tooprovide hello 특수 name 매개 변수를 사용 하 여 tooa 바인딩을 출력 하는 방법을 `$return`합니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-149">hello preceding example shows how toouse hello function return value tooprovide output tooa binding, which is achieved by using hello special name parameter `$return`.</span></span> <span data-ttu-id="f452d-150">(C#, JavaScript, F#과 같이 반환값이 있는 언어에서만 지원됩니다.) 함수에 출력 바인딩이 여러 개를 사용 하 여 `$return` hello 출력 바인딩 중 하나에 합니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-150">(This is only supported in languages that have a return value, such as C#, JavaScript, and F#.) If a function has multiple output bindings, use `$return` for only one of hello output bindings.</span></span> 

```json
// excerpt of function.json
{
    "name": "$return",
    "type": "blob",
    "direction": "out",
    "path": "output-container/{id}"
}
```

<span data-ttu-id="f452d-151">hello 표시 아래 어떻게 반환 하는 예제 형식은 C#, JavaScript 및 F #에서 출력 바인딩과 함께 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-151">hello examples below show how return types are used with output bindings in C#, JavaScript, and F#.</span></span>

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
// JavaScript: return a value in hello second parameter toocontext.done
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

## <a name="binding-datatype-property"></a><span data-ttu-id="f452d-152">dataType 속성 바인딩</span><span class="sxs-lookup"><span data-stu-id="f452d-152">Binding dataType property</span></span>

<span data-ttu-id="f452d-153">.NET에서는 입력된 데이터에 대 한 hello 형식 toodefine hello 데이터 형식을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-153">In .NET, use hello types toodefine hello data type for input data.</span></span> <span data-ttu-id="f452d-154">예를 들어 `string` 큐 및 이진으로 바이트 배열 tooread toobind toohello 텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-154">For instance, use `string` toobind toohello text of a queue trigger and a byte array tooread as binary.</span></span>

<span data-ttu-id="f452d-155">JavaScript와 같은 동적으로 형식화 되는 언어에 대 한 hello를 사용 하 여 `dataType` hello 바인딩 정의에 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-155">For languages that are dynamically typed such as JavaScript, use hello `dataType` property in hello binding definition.</span></span> <span data-ttu-id="f452d-156">예를 들어 tooread hello 이진 형식으로 HTTP 요청 콘텐츠 형식을 사용 하십시오 hello `binary`:</span><span class="sxs-lookup"><span data-stu-id="f452d-156">For example, tooread hello content of an HTTP request in binary format, use hello type `binary`:</span></span>

```json
{
    "type": "httpTrigger",
    "name": "req",
    "direction": "in",
    "dataType": "binary"
}
```

<span data-ttu-id="f452d-157">`dataType`에 대한 다른 옵션은 `stream` 및 `string`입니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-157">Other options for `dataType` are `stream` and `string`.</span></span>

## <a name="resolving-app-settings"></a><span data-ttu-id="f452d-158">앱 설정 해결</span><span class="sxs-lookup"><span data-stu-id="f452d-158">Resolving app settings</span></span>
<span data-ttu-id="f452d-159">비밀과 연결 문자열은 구성 파일이 아닌 앱 설정을 사용하여 관리하는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-159">As a best practice, secrets and connection strings should be managed using app settings, rather than configuration files.</span></span> <span data-ttu-id="f452d-160">이 액세스 toothese 비밀 정보를 제한 하 고 안전 하 게 보호 toostore *function.json* 공개 소스 제어 리포지토리에 합니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-160">This limits access toothese secrets and makes it safe toostore *function.json* in a public source control repository.</span></span>

<span data-ttu-id="f452d-161">응용 프로그램 설정은 hello 환경에 따라 toochange 구성 하려는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-161">App settings are also useful whenever you want toochange configuration based on hello environment.</span></span> <span data-ttu-id="f452d-162">예를 들어 테스트 환경에서 좋습니다 toomonitor 다른 큐 또는 blob 저장소 컨테이너.</span><span class="sxs-lookup"><span data-stu-id="f452d-162">For example, in a test environment, you may want toomonitor a different queue or blob storage container.</span></span>

<span data-ttu-id="f452d-163">앱 설정은 `%MyAppSetting%`과 같이 값이 퍼센트 기호로 둘러싸인 경우에만 확인됩니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-163">App settings are resolved whenever a value is enclosed in percent signs, such as `%MyAppSetting%`.</span></span> <span data-ttu-id="f452d-164">해당 hello 참고 `connection` 트리거 및 바인딩 속성은 특별 한 경우 및 앱 설정과 같은 값을 자동으로 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-164">Note that hello `connection` property of triggers and bindings is a special case and automatically resolves values as app settings.</span></span> 

<span data-ttu-id="f452d-165">hello 다음 예제는 응용 프로그램 설정을 사용 하는 큐 트리거 `%input-queue-name%` toodefine hello 큐 tootrigger에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-165">hello following example is a queue trigger that uses an app setting `%input-queue-name%` toodefine hello queue tootrigger on.</span></span>

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

## <a name="trigger-metadata-properties"></a><span data-ttu-id="f452d-166">트리거 메타데이터 속성</span><span class="sxs-lookup"><span data-stu-id="f452d-166">Trigger metadata properties</span></span>

<span data-ttu-id="f452d-167">또한 toohello 데이터 페이로드를 트리거 (예: 함수를 트리거한 hello 큐 메시지)에서 제공, 많은 트리거는 추가 메타 데이터 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-167">In addition toohello data payload provided by a trigger (such as hello queue message that triggered a function), many triggers provide additional metadata values.</span></span> <span data-ttu-id="f452d-168">이러한 값은 C# 및 F # 또는 hello에 대 한 속성에서 입력된 매개 변수로 사용할 수 있습니다 `context.bindings` javascript에서 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-168">These values can be used as input parameters in C# and F# or properties on hello `context.bindings` object in JavaScript.</span></span> 

<span data-ttu-id="f452d-169">예를 들어 큐 트리거 hello 다음과 같은 속성을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-169">For example, a queue trigger supports hello following properties:</span></span>

* <span data-ttu-id="f452d-170">QueueTrigger - 유효한 문자열인 경우 트리거 메시지 내용</span><span class="sxs-lookup"><span data-stu-id="f452d-170">QueueTrigger - triggering message content if a valid string</span></span>
* <span data-ttu-id="f452d-171">DequeueCount</span><span class="sxs-lookup"><span data-stu-id="f452d-171">DequeueCount</span></span>
* <span data-ttu-id="f452d-172">ExpirationTime</span><span class="sxs-lookup"><span data-stu-id="f452d-172">ExpirationTime</span></span>
* <span data-ttu-id="f452d-173">Id</span><span class="sxs-lookup"><span data-stu-id="f452d-173">Id</span></span>
* <span data-ttu-id="f452d-174">InsertionTime</span><span class="sxs-lookup"><span data-stu-id="f452d-174">InsertionTime</span></span>
* <span data-ttu-id="f452d-175">NextVisibleTime</span><span class="sxs-lookup"><span data-stu-id="f452d-175">NextVisibleTime</span></span>
* <span data-ttu-id="f452d-176">PopReceipt</span><span class="sxs-lookup"><span data-stu-id="f452d-176">PopReceipt</span></span>

<span data-ttu-id="f452d-177">각 트리거에서 대 한 메타 데이터 속성의 세부 정보는 hello 해당 참조 항목에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-177">Details of metadata properties for each trigger are described in hello corresponding reference topic.</span></span> <span data-ttu-id="f452d-178">설명서는 hello에서 가능 **통합** hello에 hello 포털의 탭 **설명서** hello 바인딩 구성 영역 아래의 섹션.</span><span class="sxs-lookup"><span data-stu-id="f452d-178">Documentation is also available in hello **Integrate** tab of hello portal, in hello **Documentation** section below hello binding configuration area.</span></span>  

<span data-ttu-id="f452d-179">예를 들어 blob 트리거 지연 않았으므로 사용할 수 있습니다 큐 트리거 toorun 함수 (참조 [Blob 저장소 트리거](functions-bindings-storage-blob.md#storage-blob-trigger)합니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-179">For example, since blob triggers have some delays, you can use a queue trigger toorun your function (see [Blob Storage Trigger](functions-bindings-storage-blob.md#storage-blob-trigger).</span></span> <span data-ttu-id="f452d-180">hello 큐 메시지는 hello blob filename tootrigger에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-180">hello queue message would contain hello blob filename tootrigger on.</span></span> <span data-ttu-id="f452d-181">Hello를 사용 하 여 `queueTrigger` 메타 데이터 속성 모두에 코드를 사용 하지 않고 구성에이 동작을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-181">Using hello `queueTrigger` metadata property, you can specify this behavior all in your configuration, rather than your code.</span></span>

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

<span data-ttu-id="f452d-182">트리거에서 메타 데이터 속성에 사용할 수도 있습니다는 *바인딩 식* 다음 섹션에 설명 된 hello로 다른 바인딩에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-182">Metadata properties from a trigger can also be used in a *binding expression* for another binding, as described in hello following section.</span></span>

## <a name="binding-expressions-and-patterns"></a><span data-ttu-id="f452d-183">바인딩 식 및 패턴</span><span class="sxs-lookup"><span data-stu-id="f452d-183">Binding expressions and patterns</span></span>

<span data-ttu-id="f452d-184">트리거 및 바인딩 hello 가장 강력한 기능 중 하나는 *바인딩 식*합니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-184">One of hello most powerful features of triggers and bindings is *binding expressions*.</span></span> <span data-ttu-id="f452d-185">바인딩 안에서 패턴 식을 정의한 다음 다른 바인딩 또는 코드에서 이 패턴 식을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-185">Within your binding, you can define pattern expressions which can then be used in other bindings or your code.</span></span> <span data-ttu-id="f452d-186">Hello 섹션 앞의 hello 샘플에 표시 된 대로 바인딩 식에서 트리거 메타 데이터를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-186">Trigger metadata can also be used in binding expressions, as show in hello sample in hello preceding section.</span></span>

<span data-ttu-id="f452d-187">예를 들어, 특정 blob 저장소 컨테이너에 비슷한 toohello tooresize 이미지를 원하는 **이미지 나타날** hello에서 서식 파일 **새 함수** 페이지.</span><span class="sxs-lookup"><span data-stu-id="f452d-187">For example, suppose you want tooresize images in particular blob storage container, similar toohello **Image Resizer** template in hello **New Function** page.</span></span> <span data-ttu-id="f452d-188">너무 이동**새 함수** 언어-> **C#** 시나리오-> **샘플** -> **ImageResizer CSharp**합니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-188">Go too**New Function** -> Language **C#** -> Scenario **Samples** -> **ImageResizer-CSharp**.</span></span> 

<span data-ttu-id="f452d-189">여기에 hello *function.json* 정의:</span><span class="sxs-lookup"><span data-stu-id="f452d-189">Here is hello *function.json* definition:</span></span>

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

<span data-ttu-id="f452d-190">해당 hello 확인 `filename` hello blob 트리거 정의 뿐만 아니라 hello blob에서 매개 변수를 사용 하는 출력 바인딩이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-190">Notice that hello `filename` parameter is used in both hello blob trigger definition as well as hello blob output binding.</span></span> <span data-ttu-id="f452d-191">이 매개 변수는 함수 코드에서도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-191">This parameter can also be used in function code.</span></span>

```csharp
// C# example of binding too{filename}
public static void Run(Stream image, string filename, Stream imageSmall, TraceWriter log)  
{
    log.Info($"Blob trigger processing: {filename}");
    // ...
} 
```

<!--TODO: add JavaScript example -->
<!-- Blocked by bug https://github.com/Azure/Azure-Functions/issues/248 -->


### <a name="random-guids"></a><span data-ttu-id="f452d-192">임의 GUID</span><span class="sxs-lookup"><span data-stu-id="f452d-192">Random GUIDs</span></span>
<span data-ttu-id="f452d-193">Azure 함수 hello 통해 사용자 바인딩을에서 Guid를 생성 하기 위한 편리 하 게 구문을 제공 `{rand-guid}` 바인딩 식입니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-193">Azure Functions provides a convenience syntax for generating GUIDs in your bindings, through hello `{rand-guid}` binding expression.</span></span> <span data-ttu-id="f452d-194">hello 다음 예제에서는이 toogenerate 고유 blob 이름:</span><span class="sxs-lookup"><span data-stu-id="f452d-194">hello following example uses this toogenerate a unique blob name:</span></span> 

```json
{
  "type": "blob",
  "name": "blobOutput",
  "direction": "out",
  "path": "my-output-container/{rand-guid}"
}
```

### <a name="current-time"></a><span data-ttu-id="f452d-195">현재 시간</span><span class="sxs-lookup"><span data-stu-id="f452d-195">Current time</span></span>

<span data-ttu-id="f452d-196">Hello 바인딩 식을 사용 하 여 `DateTime`, 너무 해결`DateTime.UtcNow`합니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-196">You can use hello binding expression `DateTime`, which resolves too`DateTime.UtcNow`.</span></span>

```json
{
  "type": "blob",
  "name": "blobOutput",
  "direction": "out",
  "path": "my-output-container/{DateTime}"
}
```

## <a name="bind-toocustom-input-properties-in-a-binding-expression"></a><span data-ttu-id="f452d-197">바인딩 식에서 입력된 속성 toocustom 바인딩</span><span class="sxs-lookup"><span data-stu-id="f452d-197">Bind toocustom input properties in a binding expression</span></span>

<span data-ttu-id="f452d-198">바인딩 식 자체 hello 트리거 페이로드에 정의 된 속성을 참조할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-198">Binding expressions can also reference properties that are defined in hello trigger payload itself.</span></span> <span data-ttu-id="f452d-199">예를 들어 여 webhook을 사용할지에 제공 된 파일 이름에서 toodynamically bind tooa blob 저장소 파일을 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-199">For example, you may want toodynamically bind tooa blob storage file from a filename provided in a webhook.</span></span>

<span data-ttu-id="f452d-200">다음 예를 들어 hello *function.json* 라는 속성을 사용 하 여 `BlobName` hello 트리거 페이로드에서:</span><span class="sxs-lookup"><span data-stu-id="f452d-200">For example, hello following *function.json* uses a property called `BlobName` from hello trigger payload:</span></span>

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

<span data-ttu-id="f452d-201">tooaccomplish이에서 C# 및 F #에서는 hello 트리거 페이로드에 deserialize 되는 hello 필드를 정의 하는 POCO 정의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-201">tooaccomplish this in C# and F#, you must define a POCO that defines hello fields that will be deserialized in hello trigger payload.</span></span>

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

<span data-ttu-id="f452d-202">JavaScript에서 JSON 역직렬화 자동으로 수행 하 고 hello 속성을 직접 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-202">In JavaScript, JSON deserialization is automatically performed and you can use hello properties directly.</span></span>

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

## <a name="configuring-binding-data-at-runtime"></a><span data-ttu-id="f452d-203">런타임에 바인딩 데이터 구성</span><span class="sxs-lookup"><span data-stu-id="f452d-203">Configuring binding data at runtime</span></span>

<span data-ttu-id="f452d-204">C#과 다른.NET 언어를 사용할 수 있습니다는 명령적 바인딩 패턴 것과 반대로 toohello 선언적 바인딩으로 *function.json*합니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-204">In C# and other .NET languages, you can use an imperative binding pattern, as opposed toohello declarative bindings in *function.json*.</span></span> <span data-ttu-id="f452d-205">명령적 바인딩 바인딩 매개 변수에 필요한 toobe 디자인 보다는 런타임 시 계산 하는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-205">Imperative binding is useful when binding parameters need toobe computed at runtime rather than design time.</span></span> <span data-ttu-id="f452d-206">toolearn 더 참조 [명령적 바인딩을 통해 런타임 시 바인딩](functions-reference-csharp.md#imperative-bindings) hello C# 개발자 참조에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f452d-206">toolearn more, see [Binding at runtime via imperative bindings](functions-reference-csharp.md#imperative-bindings) in hello C# developer reference.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f452d-207">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f452d-207">Next steps</span></span>
<span data-ttu-id="f452d-208">특정 바인딩에 대 한 자세한 내용은 다음 문서는 hello 참조:</span><span class="sxs-lookup"><span data-stu-id="f452d-208">For more information on a specific binding, see hello following articles:</span></span>

- [<span data-ttu-id="f452d-209">HTTP 및 webhook</span><span class="sxs-lookup"><span data-stu-id="f452d-209">HTTP and webhooks</span></span>](functions-bindings-http-webhook.md)
- [<span data-ttu-id="f452d-210">타이머</span><span class="sxs-lookup"><span data-stu-id="f452d-210">Timer</span></span>](functions-bindings-timer.md)
- [<span data-ttu-id="f452d-211">큐 저장소</span><span class="sxs-lookup"><span data-stu-id="f452d-211">Queue storage</span></span>](functions-bindings-storage-queue.md)
- [<span data-ttu-id="f452d-212">Blob 저장소</span><span class="sxs-lookup"><span data-stu-id="f452d-212">Blob storage</span></span>](functions-bindings-storage-blob.md)
- [<span data-ttu-id="f452d-213">Table Storage</span><span class="sxs-lookup"><span data-stu-id="f452d-213">Table storage</span></span>](functions-bindings-storage-table.md)
- [<span data-ttu-id="f452d-214">이벤트 허브</span><span class="sxs-lookup"><span data-stu-id="f452d-214">Event Hub</span></span>](functions-bindings-event-hubs.md)
- [<span data-ttu-id="f452d-215">서비스 버스</span><span class="sxs-lookup"><span data-stu-id="f452d-215">Service Bus</span></span>](functions-bindings-service-bus.md)
- [<span data-ttu-id="f452d-216">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f452d-216">Cosmos DB</span></span>](functions-bindings-documentdb.md)
- [<span data-ttu-id="f452d-217">SendGrid</span><span class="sxs-lookup"><span data-stu-id="f452d-217">SendGrid</span></span>](functions-bindings-sendgrid.md)
- [<span data-ttu-id="f452d-218">Twilio</span><span class="sxs-lookup"><span data-stu-id="f452d-218">Twilio</span></span>](functions-bindings-twilio.md)
- [<span data-ttu-id="f452d-219">알림 허브</span><span class="sxs-lookup"><span data-stu-id="f452d-219">Notification Hubs</span></span>](functions-bindings-notification-hubs.md)
- [<span data-ttu-id="f452d-220">모바일 앱</span><span class="sxs-lookup"><span data-stu-id="f452d-220">Mobile Apps</span></span>](functions-bindings-mobile-apps.md)
- [<span data-ttu-id="f452d-221">외부 파일</span><span class="sxs-lookup"><span data-stu-id="f452d-221">External file</span></span>](functions-bindings-external-file.md)

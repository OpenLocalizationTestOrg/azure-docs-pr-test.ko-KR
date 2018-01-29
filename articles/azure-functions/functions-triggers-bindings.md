---
title: "Azure Functions의 트리거 및 바인딩"
description: "Azure Functions에서 트리거 및 바인딩을 사용하여 코드 실행을 온라인 이벤트 및 클라우드 기반 서비스에 연결하는 방법을 알아봅니다."
services: functions
documentationcenter: na
author: ggailey777
manager: cfowler
editor: 
tags: 
keywords: "Azure Functions, 함수, 이벤트 처리, webhook, 동적 계산, 서버가 없는 아키텍처"
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/21/2017
ms.author: glenga
ms.openlocfilehash: a122271b5fdffd9db33a7dca5908e15f002041d7
ms.sourcegitcommit: 71fa59e97b01b65f25bcae318d834358fea5224a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/11/2018
---
# <a name="azure-functions-triggers-and-bindings-concepts"></a>Azure Functions 트리거 및 바인딩 개념

이 문서는 Azure Functions의 트리거 및 바인딩에 대한 개념적 개요를 제공합니다. 여기에서는 모든 바인딩 및 지원되는 모든 언어에 공통되는 기능을 설명합니다.

## <a name="overview"></a>개요

*트리거*는 함수가 호출되는 방식을 정의합니다. 함수에는 정확히 하나의 트리거만 있어야 합니다. 트리거는 관련 데이터가 있으며, 이 데이터는 일반적으로 함수를 트리거한 페이로드입니다.

입력 및 출력 *바인딩*은 코드에서 데이터에 연결하기 위한 선언적 방식을 제공합니다. 바인딩은 선택 사항이며 함수는 여러 개의 입력 및 출력 바인딩을 가질 수 있습니다. 

트리거 및 바인딩을 통해 작업하는 서비스 세부 정보의 하드 코딩을 방지할 수 있습니다. 함수는 함수 매개 변수에서 데이터를 수신합니다(예: 큐 메시지의 콘텐츠). 함수의 반환 값, `out` 매개 변수 또는 [collector 개체](functions-reference-csharp.md#writing-multiple-output-values)를 사용하여 데이터를 보냅니다(예: 큐 메시지를 만들기 위해).

Azure Portal을 사용하여 함수를 개발하는 경우 트리거 및 바인딩은 *function.json* 파일에서 구성됩니다. 포털은 이 구성에 대한 UI를 제공하지만 **고급 편집기**로 변경하여 파일을 직접 편집할 수 있습니다.

클래스 라이브러리를 만들기 위해 Visual Studio를 사용하여 함수를 개발하는 경우 특성으로 메서드 및 매개 변수를 데코레이트하여 트리거 및 바인딩을 구성합니다.

## <a name="supported-bindings"></a>지원되는 바인딩

[!INCLUDE [Full bindings table](../../includes/functions-bindings.md)]

미리 보기 상태 바인딩 또는 프로덕션 용도로 승인된 바인딩에 대한 자세한 내용은 [지원되는 언어](supported-languages.md)를 참조하세요.

## <a name="example-queue-trigger-and-table-output-binding"></a>예: 큐 트리거 및 테이블 출력 바인딩

Azure Queue 저장소에 새 메시지가 나타날 때마다 Azure Table 저장소에 새 행을 쓰려는 경우를 가정하겠습니다. 이 시나리오는 Azure Queue 저장소 트리거 및 Azure Table 저장소 출력 바인딩을 사용하여 구현할 수 있습니다. 

다음은 이 시나리오에 대한 *function.json* 파일입니다. 

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

`bindings` 배열의 첫 번째 요소는 큐 저장소 트리거입니다. `type` 및 `direction` 속성은 트리거를 식별합니다. `name` 속성은 큐 메시지 콘텐츠를 받는 함수 매개 변수를 식별합니다. 모니터링하는 큐 이름은 `queueName`에 있으며 연결 문자열은 `connection`으로 식별되는 앱 설정에 있습니다.

`bindings` 배열의 두 번째 요소는 Azure Table Storage 출력 바인딩입니다. `type` 및 `direction` 속성은 바인딩을 식별합니다. `name` 속성은 함수가 새 테이블 행을 제공하는 방법을 지정하며 이 경우 함수 반환 값을 사용합니다. 테이블의 이름은 `tableName`에 있으며 연결 문자열은 `connection`으로 식별되는 앱 설정에 있습니다.

Azure Portal에서 *function.json*의 내용을 보고 편집하려면 함수의 **통합** 탭에서 **고급 편집기**를 클릭합니다.

> [!NOTE]
> `connection`의 값은 연결 문자열 자체가 아닌 연결 문자열을 포함하는 앱 설정의 이름입니다. 바인딩은 *function.json*에 서비스 비밀이 포함되지 않은 모범 사례를 실행하기 위해 앱 설정에 저장된 연결 문자열을 사용합니다.

이 트리거 및 바인딩을 사용하는 C# 스크립트 코드는 다음과 같습니다. 큐 메시지 콘텐츠를 제공하는 매개 변수 이름은 `order`이며 *function.json*의 `name` 속성 값은 `order`이므로 이 이름이 필요합니다. 

```cs
#r "Newtonsoft.Json"

using Newtonsoft.Json.Linq;

// From an incoming queue message that is a JSON object, add fields and write to Table storage
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

동일한 function.json 파일을 JavaScript 함수로 사용할 수 있습니다.

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

클래스 라이브러리에서 동일한 트리거 및 바인딩 정보 &mdash; 큐 및 테이블 이름, 저장소 계정, 입력 및 출력에 대한 함수 매개 변수 &mdash;는 특성에 의해 제공됩니다.

```csharp
 public static class QueueTriggerTableOutput
 {
     [FunctionName("QueueTriggerTableOutput")]
     [return: Table("outTable", Connection = "MY_TABLE_STORAGE_ACCT_APP_SETTING")]
     public static Person Run(
         [QueueTrigger("myqueue-items", Connection = "MY_STORAGE_ACCT_APP_SETTING")]JObject order, 
         TraceWriter log)
     {
         return new Person() {
                 PartitionKey = "Orders",
                 RowKey = Guid.NewGuid().ToString(),
                 Name = order["Name"].ToString(),
                 MobileNumber = order["MobileNumber"].ToString() };
     }
 }

 public class Person
 {
     public string PartitionKey { get; set; }
     public string RowKey { get; set; }
     public string Name { get; set; }
     public string MobileNumber { get; set; }
 }
```

## <a name="binding-direction"></a>바인딩 방향

모든 트리거와 바인딩은 *function.json* 파일에 `direction` 속성이 있습니다.

- 트리거의 경우 방향은 언제나 `in`입니다
- 입력 및 출력 바인딩은 `in`과 `out`을 사용합니다
- 일부 바인딩은 특수 방향인 `inout`을 사용합니다. `inout`을 사용할 경우 **통합** 탭에서 **고급 편집기**만 사용할 수 있습니다.

[클래스 라이브러리의 특성](functions-dotnet-class-library.md)을 사용하여 트리거 및 바인딩을 구성하는 경우 방향은 특성 생성자에서 제공되거나 매개 변수 형식에서 유추됩니다.

## <a name="using-the-function-return-type-to-return-a-single-output"></a>함수 반환 유형을 사용하여 단일 출력 반환

위의 예제는 함수 반환 값을 사용하여 바인딩에 출력을 제공하는 방법을 보여 줍니다. 이 경우 `name` 속성에 대한 특수 값 `$return`을 사용하여 *function.json*에서 지정됩니다. (C# 스크립트, JavaScript, F#과 같이 반환 값이 있는 언어에서만 지원됩니다.) 함수에 복수의 출력 바인딩이 있는 경우 출력 바인딩 중 하나에 대해서만 `$return`을 사용합니다. 

```json
// excerpt of function.json
{
    "name": "$return",
    "type": "blob",
    "direction": "out",
    "path": "output-container/{id}"
}
```

아래 예제는 C# 스크립트, JavaScript, F#에서 반환 형식이 출력 바인딩과 함께 사용되는 방식을 보여 줍니다.

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
    return Task.FromResult(json);
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

## <a name="binding-datatype-property"></a>dataType 속성 바인딩

.NET에서는 매개 변수 형식을 사용하여 입력 데이터에 대한 데이터 형식을 정의합니다. 예를 들어 `string`을 사용하여 큐 트리거의 텍스트, 이진으로 읽을 바이트 배열 및 POCO 개체로 직렬화할 사용자 지정 형식에 바인딩합니다.

JavaScript와 같은 동적으로 형식화되는 언어의 경우 *function.json* 파일의 `dataType` 속성을 사용합니다. 예를 들어 이진 형식의 HTTP 요청 내용을 읽으려면 `dataType`을 `binary`로 설정합니다.

```json
{
    "type": "httpTrigger",
    "name": "req",
    "direction": "in",
    "dataType": "binary"
}
```

`dataType`에 대한 다른 옵션은 `stream` 및 `string`입니다.

## <a name="resolving-app-settings"></a>앱 설정 해결

비밀과 연결 문자열은 구성 파일이 아닌 앱 설정을 사용하여 관리하는 것이 가장 좋습니다. 그럴 경우 이러한 비밀에 대한 액세스가 제한되고 *function.json*을 공용 원본 제어 리포지토리에 안전하게 저장할 수 있습니다.

환경을 기준으로 구성을 변경하려는 경우에도 앱 설정이 유용합니다. 예를 들어 테스트 환경에서 다른 큐 또는 Blob Storage 컨테이너를 모니터링할 수 있습니다.

앱 설정은 `%MyAppSetting%`과 같이 값이 퍼센트 기호로 둘러싸인 경우에만 확인됩니다. 트리거 및 바인딩의 `connection` 속성은 특수한 경우이며 앱 설정으로 값을 자동 확인합니다. 

다음 예제는 `%input-queue-name%` 앱 설정을 사용하여 트리거할 큐를 정의하는 Azure Queue Storage 트리거입니다.

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

클래스 라이브러리에서 동일한 방법을 사용할 수 있습니다.

```csharp
[FunctionName("QueueTrigger")]
public static void Run(
    [QueueTrigger("%input-queue-name%")]string myQueueItem, 
    TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
}
```

## <a name="trigger-metadata-properties"></a>트리거 메타데이터 속성

트리거가 제공한 데이터 페이로드(예: 함수를 트리거한 큐 메시지) 이외에 많은 트리거가 추가 메타데이터 값을 제공합니다. 이러한 값은 C# 및 F#에서 입력 매개 변수로 사용하거나 JavaScript에서 `context.bindings` 개체의 속성으로 사용할 수 있습니다. 

예를 들어 Azure Queue 저장소 트리거는 다음 속성을 지원합니다.

* QueueTrigger - 유효한 문자열인 경우 트리거 메시지 내용
* DequeueCount
* ExpirationTime
* Id
* InsertionTime
* NextVisibleTime
* PopReceipt

이러한 메타데이터 값은 *function.json* 파일 속성에서 액세스할 수 있습니다. 예를 들어 큐 트리거를 사용하고 큐 메시지는 읽으려는 Blob의 이름을 포함한다고 가정합니다. *function.json* 파일에서 다음 예제와 같이 Blob `path` 속성에서 `queueTrigger` 메타데이터 속성을 사용할 수 있습니다.

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

각 트리거의 메타데이터 속성은 해당 참조 문서에서 자세히 설명되어 있습니다. 예를 들어 [큐 트리거 메타데이터](functions-bindings-storage-queue.md#trigger---message-metadata)를 참조하세요. 설명서는 Portal에서 **통합** 탭의 바인딩 구성 영역 아래 **설명서** 섹션에서도 참조할 수 있습니다.  

## <a name="binding-expressions-and-patterns"></a>바인딩 식 및 패턴

트리거와 바인딩의 가장 강력한 기능 중 하나는 *바인딩 식*입니다. 바인딩에 대한 구성에서 패턴 식을 정의한 다음 다른 바인딩 또는 코드에서 이 패턴 식을 사용할 수 있습니다. 위 섹션과 같이 트리거 메타데이터도 바인딩 식에 사용할 수 있습니다.

예를 들어 Azure Portal의 **새 함수** 페이지에서 **이미지 크기 조정** 템플릿과 같이 특정 Blob 저장소 컨테이너에서 이미지 크기를 조정하려는 경우를 가정하겠습니다(**샘플** 시나리오 참조). 

*function.json* 정의는 다음과 같습니다.

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

Blob 트리거 정의와 Blob 출력 바인딩에 `filename` 매개 변수가 사용됩니다. 이 매개 변수는 함수 코드에서도 사용할 수 있습니다.

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

바인딩 식 및 패턴을 사용하는 동일한 기능은 클래스 라이브러리의 특성에 적용됩니다. 예를 들어 다음은 클래스 라이브러리에서 이미지 크기 조정 함수입니다.

```csharp
[FunctionName("ResizeImage")]
[StorageAccount("AzureWebJobsStorage")]
public static void Run(
    [BlobTrigger("sample-images/{name}")] Stream image, 
    [Blob("sample-images-sm/{name}", FileAccess.Write)] Stream imageSmall, 
    [Blob("sample-images-md/{name}", FileAccess.Write)] Stream imageMedium)
{
    var imageBuilder = ImageResizer.ImageBuilder.Current;
    var size = imageDimensionsTable[ImageSize.Small];

    imageBuilder.Build(image, imageSmall,
        new ResizeSettings(size.Item1, size.Item2, FitMode.Max, null), false);

    image.Position = 0;
    size = imageDimensionsTable[ImageSize.Medium];

    imageBuilder.Build(image, imageMedium,
        new ResizeSettings(size.Item1, size.Item2, FitMode.Max, null), false);
}

public enum ImageSize { ExtraSmall, Small, Medium }

private static Dictionary<ImageSize, (int, int)> imageDimensionsTable = new Dictionary<ImageSize, (int, int)>() {
    { ImageSize.ExtraSmall, (320, 200) },
    { ImageSize.Small,      (640, 400) },
    { ImageSize.Medium,     (800, 600) }
};
```

### <a name="create-guids"></a>GUID 만들기

`{rand-guid}` 바인딩 식은 GUID를 만듭니다. 다음 예제는 GUID를 사용하여 고유한 Blob 이름을 생성합니다. 

```json
{
  "type": "blob",
  "name": "blobOutput",
  "direction": "out",
  "path": "my-output-container/{rand-guid}"
}
```

### <a name="current-time"></a>현재 시간

바인딩 식 `DateTime`은 `DateTime.UtcNow`로 확인됩니다.

```json
{
  "type": "blob",
  "name": "blobOutput",
  "direction": "out",
  "path": "my-output-container/{DateTime}"
}
```

## <a name="bind-to-custom-input-properties"></a>사용자 지정 입력 속성으로 바인딩

바인딩 식은 트리거 페이로드 자체에 정의된 속성도 참조할 수 있습니다. 예를 들어 webhook에 제공된 파일 이름에서 Blob Storage 파일에 동적으로 바인딩하는 경우가 있습니다.

예를 들어 다음 *function.json*은 트리거 페이로드에서 `BlobName`이라는 속성을 사용합니다.

```json
{
  "bindings": [
    {
      "name": "info",
      "type": "httpTrigger",
      "direction": "in",
      "webHookType": "genericJson"
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

C# 및 F#에서 이를 달성하려면 트리거 페이로드에서 deserialize되는 필드를 정의하는 POCO를 정의해야 합니다.

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

JavaScript에서 JSON deserialization은 자동으로 실행되며 속성을 직접 사용할 수 있습니다.

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

## <a name="configuring-binding-data-at-runtime"></a>런타임에 바인딩 데이터 구성

C# 및 기타 .NET 언어에서는 *function.json* 및 특성의 바인딩과 달리 명령적 바인딩 패턴을 사용할 수 있습니다. 명령적 바인딩은 바인딩 매개 변수를 디자인 타임이 아닌 런타임에 계산해야 할 경우 유용합니다. 자세한 내용은 C# 개발자 참조에서 [명령적 바인딩을 통해 런타임 시 바인딩](functions-reference-csharp.md#imperative-bindings)을 참조하세요.

## <a name="functionjson-file-schema"></a>function.json 파일 스키마

*function.json* 파일 스키마는 [http://json.schemastore.org/function](http://json.schemastore.org/function)에서 제공됩니다.

## <a name="next-steps"></a>다음 단계

특성 바인딩에 대한 자세한 내용은 다음 문서를 참조하십시오.

- [HTTP 및 webhook](functions-bindings-http-webhook.md)
- [타이머](functions-bindings-timer.md)
- [Queue storage](functions-bindings-storage-queue.md)
- [Blob storage](functions-bindings-storage-blob.md)
- [Table Storage](functions-bindings-storage-table.md)
- [이벤트 허브](functions-bindings-event-hubs.md)
- [Service Bus](functions-bindings-service-bus.md)
- [Azure Cosmos DB](functions-bindings-cosmosdb.md)
- [Microsoft Graph](functions-bindings-microsoft-graph.md)
- [SendGrid](functions-bindings-sendgrid.md)
- [Twilio](functions-bindings-twilio.md)
- [Notification Hubs](functions-bindings-notification-hubs.md)
- [Mobile Apps](functions-bindings-mobile-apps.md)
- [외부 파일](functions-bindings-external-file.md)

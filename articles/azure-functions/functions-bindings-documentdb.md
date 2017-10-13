---
title: "Functions에 대한 Azure Cosmos DB 바인딩 | Microsoft Docs"
description: "Azure Functions에서 Azure Cosmos DB 트리거 및 바인딩을 사용하는 방법을 파악합니다."
services: functions
documentationcenter: na
author: christopheranderson
manager: cfowler
editor: 
tags: 
keywords: "Azure Functions, 함수, 이벤트 처리, 동적 계산, 서버를 사용하지 않는 아키텍처"
ms.assetid: 3d8497f0-21f3-437d-ba24-5ece8c90ac85
ms.service: functions; cosmos-db
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 09/19/2017
ms.author: glenga
ms.openlocfilehash: ad058929eb888920823fddf549ada4ce2c6d9eee
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/11/2017
---
# <a name="azure-cosmos-db-bindings-for-functions"></a>Functions에 대한 Azure Cosmos DB 바인딩
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

이 문서에서는 Azure Functions에서 Azure Cosmos DB 바인딩을 구성하고 코딩하는 방법을 설명합니다. Functions는 Azure Cosmos DB에 대한 트리거, 입력 및 출력 바인딩을 지원합니다.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

Azure Cosmos DB를 통한 서버를 사용하지 않는 컴퓨팅에 대한 자세한 내용은 [Azure Cosmos DB: Azure Functions를 통한, 서버를 사용하지 않는 데이터베이스 컴퓨팅](..\cosmos-db\serverless-computing-database.md)을 참조하세요.

<a id="trigger"></a>
<a id="cosmosdbtrigger"></a>

## <a name="azure-cosmos-db-trigger"></a>Azure Cosmos DB 트리거

Azure Cosmos DB 트리거는 [Azure Cosmos DB 변경 피드](../cosmos-db/change-feed.md)를 사용하여 파티션의 변경 내용을 수신 대기합니다. 트리거에는 파티션에 _임대_를 저장하는 데 사용할 보조 컬렉션이 필요합니다.

트리거가 작동할 수 있도록 모니터링되는 컬렉션과 임대를 포함하고 있는 컬렉션을 모두 사용할 수 있어야 합니다.

Azure Cosmos DB 트리거는 다음 속성을 지원합니다.

|속성  |설명  |
|---------|---------|
|**type** | `cosmosDBTrigger`로 설정해야 합니다. |
|**name** | 변경 사항이 포함된 문서 목록을 나타내는 함수 코드에 사용되는 변수 이름. | 
|**direction** | `in`로 설정해야 합니다. 이 매개 변수는 사용자가 Azure Portal에서 트리거를 만들 때 자동으로 설정됩니다. |
|**connectionStringSetting** | 모니터링되는 Azure Cosmos DB 계정에 연결하는 데 사용되는 연결 문자열을 포함하고 있는 앱 설정의 이름입니다. |
|**databaseName** | 컬렉션이 모니터링되는 Azure Cosmos DB 데이터베이스의 이름입니다. |
|**collectionName** | 모니터링되는 컬렉션의 이름입니다. |
| **leaseConnectionStringSetting** | (선택 사항) 임대 컬렉션을 보유하고 있는 서비스에 대한 연결 문자열을 포함하는 앱 설정의 이름입니다. 설정하지 않으면 `connectionStringSetting` 값이 사용됩니다. 이 매개 변수는 포털에서 바인딩이 생성될 때 자동으로 설정됩니다. |
| **leaseDatabaseName** | (선택 사항) 임대를 저장하는 데 사용되는 컬렉션을 보유하는 데이터베이스의 이름입니다. 설정하지 않으면 `databaseName` 설정 값이 사용됩니다. 이 매개 변수는 포털에서 바인딩이 생성될 때 자동으로 설정됩니다. |
| **leaseCollectionName** | (선택 사항) 임대를 저장하는 데 사용되는 컬렉션의 이름입니다. 설정하지 않으면 `leases` 값이 사용됩니다. |
| **createLeaseCollectionIfNotExists** | (선택 사항) `true`로 설정하면 임대 컬렉션이 없는 경우 자동으로 임대 컬렉션이 생성됩니다. 기본값은 `false`입니다. |
| **leaseCollectionThroughput** | (선택 사항) 임대 컬렉션이 생성될 때 할당할 요청 단위의 양을 정의합니다. 이 설정은 `createLeaseCollectionIfNotExists`가 `true`로 설정된 경우에만 사용됩니다. 이 매개 변수는 포털을 사용하여 바인딩이 생성될 때 자동으로 설정됩니다.

>[!NOTE] 
>임대 컬렉션에 연결하는 데 사용되는 연결 문자열에 쓰기 권한이 있어야 합니다.

이러한 속성은 Azure Portal에서 함수의 통합 탭에서 설정하거나 `function.json` 프로젝트 파일을 편집하여 설정할 수 있습니다.

## <a name="using-an-azure-cosmos-db-trigger"></a>Azure Cosmos DB 트리거 사용

이 섹션에는 Azure Cosmos DB 트리거를 사용하는 방법에 대한 예제가 포함되어 있습니다. 예제에서는 다음과 같은 트리거 메타데이터를 가정합니다.

```json
{
  "type": "cosmosDBTrigger",
  "name": "documents",
  "direction": "in",
  "leaseCollectionName": "leases",
  "connectionStringSetting": "<connection-app-setting>",
  "databaseName": "Tasks",
  "collectionName": "Items",
  "createLeaseCollectionIfNotExists": true
}
```
 
포털에서 함수 앱을 사용하여 Azure Cosmos DB 트리거를 만드는 방법에 대한 예제는 [Azure Cosmos DB에 의해 트리거되는 함수 만들기](functions-create-cosmos-db-triggered-function.md)를 참조하세요. 

### <a name="trigger-sample-in-c"></a>C#에서 트리거 샘플 #
```cs 
    #r "Microsoft.Azure.Documents.Client"
    using Microsoft.Azure.Documents;
    using System.Collections.Generic;
    using System;
    public static void Run(IReadOnlyList<Document> documents, TraceWriter log)
    {
        log.Verbose("Documents modified " + documents.Count);
        log.Verbose("First document Id " + documents[0].Id);
    }
```


### <a name="trigger-sample-in-javascript"></a>JavaScript의 트리거 샘플
```javascript
    module.exports = function (context, documents) {
        context.log('First document Id modified : ', documents[0].id);

        context.done();
    }
```

<a id="docdbinput"></a>

## <a name="documentdb-api-input-binding"></a>DocumentDB API 입력 바인딩
DocumentDB API 입력 바인딩은 Azure Cosmos DB 문서를 검색하여 함수의 명명된 입력 매개 변수에 전달합니다. 함수를 호출한 트리거에 따라 문서 ID를 결정할 수 있습니다. 

DocumentDB API 입력 바인딩은 *function.json*에 다음 속성이 있습니다.

|속성  |설명  |
|---------|---------|
|**name**     | 함수에서 문서를 나타내는 바인딩 매개 변수의 이름입니다.  |
|**type**     | `documentdb`로 설정해야 합니다.        |
|**databaseName** | 문서를 포함하는 데이터베이스입니다.        |
|**collectionName**  | 문서를 포함하는 컬렉션의 이름입니다. |
|**id**     | 검색할 문서의 ID입니다. 이 속성은 바인딩 매개 변수를 지원합니다. 자세한 내용은 [바인딩 식에서 사용자 지정 입력 속성에 바인딩](functions-triggers-bindings.md#bind-to-custom-input-properties-in-a-binding-expression)을 참조하세요. |
|**sqlQuery**     | 여러 문서를 검색하는 데 사용되는 Azure Cosmos DB SQL 쿼리입니다. 쿼리는 `SELECT * FROM c where c.departmentId = {departmentId}` 예제와 같이 런타임 바인딩을 지원합니다.        |
|**연결**     |Azure Cosmos DB 연결 문자열을 포함하는 앱 설정의 이름입니다.        |
|**direction**     | `in`로 설정해야 합니다.         |

**id** 및 **sqlQuery** 속성을 둘 다 설정할 수는 없습니다. 둘 다 설정하지 않으면 전체 컬렉션이 검색됩니다.

## <a name="using-a-documentdb-api-input-binding"></a>DocumentDB API 입력 바인딩 사용

* C# 및 F# 함수에서 함수가 성공적으로 종료되면 명명된 입력 매개 변수를 통해 입력 문서에 변경한 내용이 자동으로 유지됩니다. 
* JavaScript 함수에서는 함수 종료 시 자동으로 업데이트되지 않습니다. 대신 `context.bindings.<documentName>In` 및 `context.bindings.<documentName>Out`을 사용하여 업데이트합니다. [JavaScript 샘플](#injavascript)을 참조하세요.

<a name="inputsample"></a>

## <a name="input-sample-for-single-document"></a>단일 문서에 대한 입력 샘플
function.json의 `bindings` 배열에 다음과 같은 DocumentDB API 입력 바인딩이 있다고 가정합니다.

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

이 입력 바인딩을 사용하여 문서의 텍스트 값을 업데이트하는 언어별 샘플을 참조하세요.

* [C#](#incsharp)
* [F#](#infsharp)
* [JavaScript](#injavascript)

<a name="incsharp"></a>
### <a name="input-sample-in-c"></a>C#의 입력 샘플 #

```cs
// Change input document contents using DocumentDB API input binding 
public static void Run(string myQueueItem, dynamic inputDocument)
{   
  inputDocument.text = "This has changed.";
}
```
<a name="infsharp"></a>

### <a name="input-sample-in-f"></a>F#의 입력 샘플 #

```fsharp
(* Change input document contents using DocumentDB API input binding *)
open FSharp.Interop.Dynamic
let Run(myQueueItem: string, inputDocument: obj) =
  inputDocument?text <- "This has changed."
```

이 샘플에는 `FSharp.Interop.Dynamic` 및 `Dynamitey` NuGet 종속성을 지정하는 `project.json` 파일이 필요합니다.

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

`project.json` 파일을 추가하려면 [F# 패키지 관리](functions-reference-fsharp.md#package)를 참조하세요.

<a name="injavascript"></a>

### <a name="input-sample-in-javascript"></a>JavaScript의 입력 샘플

```javascript
// Change input document contents using DocumentDB API input binding, using context.bindings.inputDocumentOut
module.exports = function (context) {   
  context.bindings.inputDocumentOut = context.bindings.inputDocumentIn;
  context.bindings.inputDocumentOut.text = "This was updated!";
  context.done();
};
```

## <a name="input-sample-with-multiple-documents"></a>여러 문서가 있는 입력 샘플

SQL 쿼리로 지정된 여러 문서를 검색하려고 하며 큐 트리거를 사용하여 쿼리 매개 변수를 사용자 지정한다고 가정합니다. 

이 예제에서 큐 트리거는 매개 변수 `departmentId`를 제공합니다. 큐 메시지 `{ "departmentId" : "Finance" }`는 재무 부서에 대한 모든 레코드를 반환합니다. *function.json*에서 다음을 사용합니다.

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

### <a name="input-sample-with-multiple-documents-in-c"></a>C#으로 작성된 여러 문서가 있는 입력 샘플

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

### <a name="input-sample-with-multiple-documents-in-javascript"></a>JavaScript로 작성된 여러 문서가 있는 입력 샘플

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

## <a id="docdboutput"></a>DocumentDB API 출력 바인딩
DocumentDB API 출력 바인딩을 사용하면 Azure Cosmos DB 데이터베이스에 새 문서를 작성할 수 있습니다. *function.json*에 다음 속성이 있습니다.

|속성  |설명  |
|---------|---------|
|**name**     | 함수에서 문서를 나타내는 바인딩 매개 변수의 이름입니다.  |
|**type**     | `documentdb`로 설정해야 합니다.        |
|**databaseName** | 문서가 만들어진 컬렉션을 포함하는 데이터베이스입니다.     |
|**collectionName**  | 문서가 만들어진 컬렉션의 이름입니다. |
|**createIfNotExists**     | 컬렉션이 존재하지 않는 경우 만들 수 있는지 여부를 나타내는 부울 값입니다. 기본값은 *false*입니다. 새 컬렉션이 예약된 처리량으로 만들어져 비용이 부과되기 때문입니다. 자세한 내용은 [가격 책정 페이지](https://azure.microsoft.com/pricing/details/documentdb/)를 참조하세요.  |
|**연결**     |Azure Cosmos DB 연결 문자열을 포함하는 앱 설정의 이름입니다.        |
|**direction**     | `out`로 설정해야 합니다.         |

## <a name="using-a-documentdb-api-output-binding"></a>DocumentDB API 출력 바인딩 사용
이 섹션에서는 함수 코드에서 DocumentDB API 출력 바인딩을 사용하는 방법을 보여 줍니다.

기본적으로 함수에서 출력 매개 변수에 쓸 경우 데이터베이스에서 문서가 생성됩니다. 이 문서에는 자동으로 생성된 GUID가 문서 ID로 지정되어 있습니다. 출력 매개 변수에 전달되는 JSON 개체에 `id` JSON 속성을 지정하여 출력 문서의 문서 ID를 지정할 수 있습니다. 

>[!Note]  
>기존 문서의 ID를 지정하면 새 출력 문서에 의해 덮어쓰여집니다. 

여러 문서를 출력하기 위해 `ICollector<T>` 또는 `IAsyncCollector<T>`에 바인딩할 수 있으며, 여기서 `T`는 지원되는 형식 중 하나입니다.

<a name="outputsample"></a>

## <a name="documentdb-api-output-binding-sample"></a>DocumentDB API 출력 바인딩 샘플
function.json의 `bindings` 배열에 다음과 같은 DocumentDB API 출력 바인딩이 있다고 가정합니다.

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

또한 다음과 같은 형식의 JSON을 수신하는 큐에 대한 큐 입력 바인딩이 있습니다.

```json
{
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

그리고 각 레코드에 대해 다음과 같은 형식의 Azure Cosmos DB 문서를 만들려고 합니다.

```json
{
  "id": "John Henry-123456",
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

이 출력 바인딩을 사용하여 문서를 데이터베이스에 추가하는 언어별 샘플을 참조하세요.

* [C#](#outcsharp)
* [F#](#outfsharp)
* [JavaScript](#outjavascript)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a>C#에서 출력 샘플 #

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

### <a name="output-sample-in-f"></a>F#에서 출력 샘플 #

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

이 샘플에는 `FSharp.Interop.Dynamic` 및 `Dynamitey` NuGet 종속성을 지정하는 `project.json` 파일이 필요합니다.

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

`project.json` 파일을 추가하려면 [F# 패키지 관리](functions-reference-fsharp.md#package)를 참조하세요.

<a name="outjavascript"></a>

### <a name="output-sample-in-javascript"></a>JavaScript의 출력 샘플

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

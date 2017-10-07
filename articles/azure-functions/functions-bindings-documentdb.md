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
# <a name="azure-functions-cosmos-db-bindings"></a>Azure Functions Cosmos DB 바인딩
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

이 문서에서는 설명 어떻게 Azure 함수에서 tooconfigure 및 코드 Azure Cosmos DB 바인딩. Azure Functions는 Cosmos DB에 대한 입력 및 출력 바인딩을 지원합니다.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

Cosmos DB에 대 한 자세한 내용은 참조 하십시오. [소개 tooCosmos DB](../documentdb/documentdb-introduction.md) 및 [Cosmos DB 콘솔 응용 프로그램 빌드](../documentdb/documentdb-get-started.md)합니다.

<a id="docdbinput"></a>

## <a name="documentdb-api-input-binding"></a>DocumentDB API 입력 바인딩
Cosmos DB 문서를 검색 하 고 toohello 명명 된 hello 함수의 입력된 매개 변수를 전달 하는 hello DocumentDB API 입력된 바인딩 합니다. hello 함수를 호출 하는 hello 트리거를 기반으로 hello 문서 ID를 확인할 수 있습니다. 

DocumentDB API 입력된 바인딩 hello에 다음과 같은 속성에 hello *function.json*:

- `name`: Hello 문서에 대 한 함수 코드에서 사용 하는 식별자 이름
- `type`: 너무 설정 해야 합니다 "documentdb"
- `databaseName`: hello 문서를 포함 하는 hello 데이터베이스
- `collectionName`: hello 문서를 포함 하는 hello 컬렉션
- `id`: hello hello 문서 tooretrieve의 Id입니다. 이 속성은 바인딩 매개 변수 지원 참조 [바인딩 식에서 toocustom 입력된 속성을 바인딩할](functions-triggers-bindings.md#bind-to-custom-input-properties-in-a-binding-expression) hello 문서의 [Azure 함수 트리거 및 바인딩 개념](functions-triggers-bindings.md)합니다.
- `sqlQuery`: 여러 문서를 검색하는 데 사용되는 Cosmos DB SQL 쿼리입니다. hello 쿼리 런타임 바인딩을 지원합니다. 예: `SELECT * FROM c where c.departmentId = {departmentId}`
- `connection`: Cosmos DB 연결 문자열을 포함 하는 hello 앱 설정의 hello 이름
- `direction`: 너무 설정 되어 있어야`"in"`합니다.

속성을 hello `id` 및 `sqlQuery` 모두 지정할 수 없습니다. 모두 `id` 나 `sqlQuery` 설정 되 면 hello 전체 컬렉션에서 검색 됩니다.

## <a name="using-a-documentdb-api-input-binding"></a>DocumentDB API 입력 바인딩 사용

* C# 및 F # 함수에서 hello 함수는 성공적으로 종료 될 때 명명 된 입력된 매개 변수를 통해 toohello 입력된 문서를 변경한 내용은 자동으로 유지 됩니다. 
* JavaScript 함수에서는 함수 종료 시 자동으로 업데이트되지 않습니다. 대신를 사용 하 여 `context.bindings.<documentName>In` 및 `context.bindings.<documentName>Out` toomake 업데이트 합니다. Hello 참조 [JavaScript 샘플](#injavascript)합니다.

<a name="inputsample"></a>

## <a name="input-sample-for-single-document"></a>단일 문서에 대한 입력 샘플
DocumentDB API 입력 바인딩 hello에 있다고 가정 하면 hello 다음 `bindings` function.json의 배열:

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

이 입력된 바인딩의 tooupdate hello 문서의 텍스트 값을 사용 하는 hello 언어 관련 샘플을 참조 하십시오.

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

이 샘플을 사용 하려면 한 `project.json` hello를 지정 하는 파일 `FSharp.Interop.Dynamic` 및 `Dynamitey` NuGet 종속성:

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

tooadd는 `project.json` 파일, 참조 [F # 패키지 관리](functions-reference-fsharp.md#package)합니다.

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

한다고 tooretrieve SQL 쿼리로 지정 된 여러 문서는 큐 트리거 toocustomize hello 쿼리 매개 변수를 사용 하 여 가정 합니다. 

이 예제에서는 hello 큐 트리거 매개 변수를 제공 `departmentId`합니다. 큐 메시지의 `{ "departmentId" : "Finance" }` hello 재무 부서에 대 한 모든 레코드를 반환 합니다. 다음 hello를 사용 하 여 *function.json*:

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
DocumentDB API hello 작성할 새 문서 tooan Azure Cosmos DB 데이터베이스 바인딩 수를 출력 합니다. 다음과 같은 속성에 hello 있기 *function.json*:

- `name`: Hello 새 문서에 대 한 함수 코드에서 사용 되는 식별자
- `type`: 너무 설정 해야 합니다`"documentdb"`
- `databaseName`: hello 새 문서를 만들 위치 hello 컬렉션을 포함 하는 hello 데이터베이스.
- `collectionName`: hello 컬렉션 hello 새 문서를 만들 위치입니다.
- `createIfNotExists`: 부울 값이 존재 하지 않는 경우 hello 컬렉션을 만들 수는 여부를 tooindicate입니다. hello 기본값은 *false*합니다. 이유 hello 예약 된 처리량이 가격에 영향을 줄 수 있는 컬렉션을 만들고 새로운 기능이 며에 대 한 합니다. 자세한 내용은 hello를 방문 하세요 [가격 책정 페이지](https://azure.microsoft.com/pricing/details/documentdb/)합니다.
- `connection`: Cosmos DB 연결 문자열을 포함 하는 hello 앱 설정의 hello 이름
- `direction`: 너무 설정 해야 합니다`"out"`

## <a name="using-a-documentdb-api-output-binding"></a>DocumentDB API 출력 바인딩 사용
이 섹션에서는 어떻게 toouse DocumentDB API 출력 함수 코드에서 바인딩을 보여 줍니다.

기본적으로 데이터베이스에 새 문서 생성은 함수에서 toohello 출력 매개 변수를 작성할 때 hello로 자동으로 생성된 된 GUID와 문서 id입니다. Hello를 지정 하 여 출력 문서의 hello 문서 ID를 지정할 수 있습니다 `id` hello에 JSON 속성 매개 변수를 출력 합니다. 

>[!Note]  
>기존 문서 hello ID를 지정 하 여 hello 새 출력 문서가 덮어쓰기됩니다. 

toooutput 여러 문서를 바인딩할 수도 있습니다 너무`ICollector<T>` 또는 `IAsyncCollector<T>` 여기서 `T` hello 지원 형식 중 하나입니다.

<a name="outputsample"></a>

## <a name="documentdb-api-output-binding-sample"></a>DocumentDB API 출력 바인딩 샘플
DocumentDB API 출력 바인딩 hello에 있다고 가정 하면 hello 다음 `bindings` function.json의 배열:

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

있고 JSON 형식에 따라 hello에서 부여 하는 큐에 대 한 큐 입력된 바인딩:

```json
{
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

및 toocreate Cosmos DB 문서에서 각 레코드에 대 한 형식에 따라 hello에:

```json
{
  "id": "John Henry-123456",
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

이 출력 바인딩 tooadd 문서 tooyour 데이터베이스를 사용 하는 hello 언어 관련 샘플을 참조 하십시오.

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

이 샘플을 사용 하려면 한 `project.json` hello를 지정 하는 파일 `FSharp.Interop.Dynamic` 및 `Dynamitey` NuGet 종속성:

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

tooadd는 `project.json` 파일, 참조 [F # 패키지 관리](functions-reference-fsharp.md#package)합니다.

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

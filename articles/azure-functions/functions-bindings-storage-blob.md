---
title: "aaaAzure 함수 Blob 저장소 바인딩 | Microsoft Docs"
description: "Toouse Azure 저장소의 트리거 방법 및 Azure 함수에서 바인딩 이해 합니다."
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "Azure Functions, 함수, 이벤트 처리, 동적 계산, 서버를 사용하지 않는 아키텍처"
ms.assetid: aba8976c-6568-4ec7-86f5-410efd6b0fb9
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/25/2017
ms.author: glenga
ms.openlocfilehash: cef44bd2154d0b97cca9220b6c5024a5b620c80d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-blob-storage-bindings"></a>Azure Functions Blob Storage 바인딩
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

이 문서에서는 설명 어떻게 tooconfigure 정보와 Azure 함수에서 Azure Blob 저장소 바인딩을 사용 하는 작업입니다. Azure Functions는 Azure Blob Storage에 대한 트리거, 입력 및 출력 바인딩을 지원합니다. 모든 바인딩에서 사용할 수 있는 기능은 [Azure Functions 트리거 및 바인딩 개념](functions-triggers-bindings.md)을 참조하세요.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

> [!NOTE]
> [Blob 전용 저장소 계정](../storage/common/storage-create-storage-account.md#blob-storage-accounts)은 지원되지 않습니다. Blob Storage 트리거 및 바인딩에는 범용 저장소 계정이 필요합니다. 
> 

<a name="trigger"></a>
<a name="storage-blob-trigger"></a>
## <a name="blob-storage-triggers-and-bindings"></a>Blob Storage 트리거 및 바인딩

함수 코드는 hello Azure Blob 저장소 트리거를 사용 하 여 신규 또는 업데이트 된 blob 검색 되 면 호출 됩니다. 입력된 toohello 함수 hello blob 콘텐츠가 제공 됩니다.

Hello를 사용 하 여 blob 저장소 트리거를 정의한 다음 **통합** hello 함수 포털에서 탭 합니다. hello 포털에서는 다음 hello에 정의 된 hello **바인딩** 섹션 *function.json*:

```json
{
    "name": "<hello name used tooidentify hello trigger data in your code>",
    "type": "blobTrigger",
    "direction": "in",
    "path": "<container toomonitor, and optionally a blob name pattern - see below>",
    "connection": "<Name of app setting - see below>"
}
```

Blob 입력 및 출력 바인딩을 사용 하 여 정의 `blob` hello 바인딩 형식으로:

```json
{
  "name": "<hello name used tooidentify hello blob input in your code>",
  "type": "blob",
  "direction": "in", // other supported directions are "inout" and "out"
  "path": "<Path of input blob - see below>",
  "connection":"<Name of app setting - see below>"
},
```

* hello `path` 바인딩 식 및 필터 매개 변수 속성은 지원 합니다. [이름 패턴](#pattern)을 참조하세요.
* hello `connection` 저장소 연결 문자열을 포함 하는 응용 프로그램 설정의 hello 이름을 포함 해야 합니다. Hello Azure 포털에서에서 hello의 표준 편집기 hello **통합** 탭 저장소 계정을 선택할 때 응용 프로그램 설정을 구성 합니다.

> [!NOTE]
> Blob 트리거 소비 계획을 사용 하는 경우에 있을 수 있습니다 켜기 tooa 10 분 지연 함수 앱이 유휴 내려갔습니다 후 새 blob을 처리 합니다. Hello 함수 응용 프로그램을 실행 한 후 blob 즉시 처리 됩니다. 이 초기 tooavoid 지연 hello 다음 옵션 중 하나를 고려 하십시오.
> - 무중단이 사용되는 App Service 계획을 사용합니다.
> - 예: hello blob 이름을 포함 하는 큐 메시지 처리, 다른 메커니즘 tootrigger hello blob을 사용 합니다. 예를 들어 [Blob 입력 바인딩을 사용하여 큐 트리거](#input-sample)를 참조하세요.

<a name="pattern"></a>

### <a name="name-patterns"></a>이름 패턴
Hello에 blob 이름 패턴을 지정할 수 있습니다 `path` 속성 필터 또는 바인딩 식이 될 수 있습니다. [바인딩 식 및 패턴](functions-triggers-bindings.md#binding-expressions-and-patterns)을 참조하세요.

예를 들어 toofilter tooblobs hello 문자열 "원래"로 시작 하는 정의 다음 hello를 사용 합니다. 이 경로 라는 blob를 찾습니다 *원래 Blob1.txt* hello에 *입력* 컨테이너 및 hello hello 값 `name` 함수 코드에서 변수는 `Blob1`합니다.

```json
"path": "input/original-{name}",
```

toobind toohello blob 파일 이름과 확장명을 별도로 두 개의 패턴을 사용합니다. 이 경로 또한 라는 blob 찾습니다 *원래 Blob1.txt*, 및의 hello hello 값 `blobname` 및 `blobextension` 함수 코드에서 변수는 *원래 Blob1* 및 *txt*.

```json
"path": "input/{blobname}.{blobextension}",
```

Hello 파일 확장명에 대 한 고정된 값을 사용 하 여 hello 파일 유형의 blob 제한할 수 있습니다. 예를 들어, tootrigger.png 파일에 대해서만 사용 하 여 hello 패턴:

```json
"path": "samples/{name}.png",
```

중괄호는 이름 패턴에서 특수 문자입니다. 중괄호 hello 이름에 포함 된 toospecify blob 이름은 중괄호 2 개를 사용 하 여 hello 중괄호를 이스케이프 확인할 수 있습니다. hello 다음 예제에서는 찾습니다 라는 blob *{20140101}-soundfile.mp3* hello에 *이미지* 컨테이너 및 hello `name` hello 함수 코드에서 변수 값이  *soundfile.mp3*합니다. 

```json
"path": "images/{{20140101}}-{name}",
```

### <a name="trigger-metadata"></a>트리거 메타데이터

hello blob 트리거는 여러 가지 메타 데이터 속성을 제공합니다. 이러한 속성을 다른 바인딩에서 바인딩 식의 일부로 사용하거나 코드에서 매개 변수로 사용할 수 있습니다. 이러한 값은 hello와 동일한 의미 체계 [CloudBlob](https://docs.microsoft.com/en-us/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob?view=azure-dotnet)합니다.

- **BlobTrigger**. `string`을 입력합니다. hello 트리거 blob 경로
- **Uri**. `System.Uri`을 입력합니다. hello 기본 위치에 대 한 hello blob의 URI입니다.
- **Properties**. `Microsoft.WindowsAzure.Storage.Blob.BlobProperties`을 입력합니다. blob의 시스템 속성 hello 합니다.
- **Metadata**. `IDictionary<string,string>`을 입력합니다. hello hello blob에 대 한 사용자 정의 메타 데이터입니다.

<a name="receipts"></a>

### <a name="blob-receipts"></a>Blob 수신 확인
런타임 하면 blob 트리거 함수에 대 한 두 번 이상 호출 가져옵니다 hello Azure 함수 hello 동일한 신규 또는 업데이트 된 blob입니다. 유지 toodetermine 특정된 blob 버전 처리 된 경우, *수령액 blob*합니다.

기능 저장소를 azure blob 라는 컨테이너에 수신 확인 *azure webjobs 호스트* hello 함수 앱에 대 한 Azure 저장소 계정에서에서 (hello 응용 프로그램 설정으로 정의 된 `AzureWebJobsStorage`). Blob 수신 확인에는 다음 정보는 hello에 있습니다.

* hello 함수를 트리거 ("*&lt;함수 응용 프로그램 이름 >*합니다. 함수입니다.  *&lt;함수 이름 >*", 예:"MyFunctionApp.Functions.CopyBlob")
* hello 컨테이너 이름
* hello blob 유형 ("BlockBlob" 또는 "PageBlob")
* hello blob 이름
* hello ETag (예: blob 버전 식별자: "0x8D1DC6E70A277EF")

hello에서 해당 blob에 대 한 hello blob 확인을 삭제 하는 blob의 tooforce 재처리 *azure webjobs 호스트* 컨테이너 수동으로 합니다.

<a name="poison"></a>

### <a name="handling-poison-blobs"></a>포이즌 Blob 처리
지정된 Blob에 대한 Blob 트리거 함수가 실패한 경우 Azure Functions는 기본적으로 총 5번 해당 함수를 다시 시도합니다. 

모든 5 시도 실패 하는 경우 Azure 함수 추가 라는 메시지 tooa 저장소 큐 *webjobs-blobtrigger-포이즌*합니다. 포이즌 blob에 대 한 hello 큐 메시지는 hello 다음과 같은 속성을 포함 하는 JSON 개체:

* FunctionId (hello 형태로 표시  *&lt;함수 응용 프로그램 이름 >*합니다. 함수입니다.  *&lt;함수 이름 >*)
* BlobType("BlockBlob" 또는 "PageBlob")
* ContainerName
* BlobName
* ETag(Blob 버전 식별자, 예: "0x8D1DC6E70A277EF")

### <a name="blob-polling-for-large-containers"></a>큰 컨테이너에 대한 Blob 폴링
모니터링 되 고 hello blob 컨테이너에 10, 000 개 이상의 blob이 있으면 런타임 검사 hello 함수 파일 toowatch 새롭거나 변경 된 blob에 대 한 로그입니다. 이 프로세스는 실시간으로 하지 않습니다. 함수 수 트리거되지 몇 분까지 또는 그 이상 hello blob가 생성 한 후 합니다. 또한 [저장소 로그는 "최선을 다해" 생성됩니다](/rest/api/storageservices/About-Storage-Analytics-Logging). 하지만 모든 이벤트가 캡처되는 것은 아닙니다. 경우에 따라 로그가 누락될 수 있습니다. 더 빠르거나 안정적인 blob 처리를 필요로 하는 경우 만드십시오는 [큐 메시지](../storage/queues/storage-dotnet-how-to-use-queues.md) hello blob를 만들 때. 그런 다음 사용 하는 [큐 트리거](functions-bindings-storage-queue.md) blob 트리거 tooprocess hello blob 대신 합니다.

<a name="triggerusage"></a>

## <a name="using-a-blob-trigger-and-input-binding"></a>Blob 트리거 및 입력 바인딩 사용
.NET 함수에서와 같은 메서드 매개 변수를 사용 하 여 hello blob 데이터에 액세스 `Stream paramName`합니다. 여기에서 `paramName` hello에 지정 된 hello 값인 [트리거 구성](#trigger)합니다. Node.js 함수에서 액세스 hello blob 데이터를 사용 하 여 입력 `context.bindings.<name>`합니다.

.NET에서는 hello 형식의 tooany hello 목록 아래에 바인딩할 수 있습니다. 입력 바인딩으로 사용되는 경우 이러한 형식 중 일부에는 *function.json*에서 `inout` 바인딩 방향이 필요합니다. 고급 편집기 hello를 사용 해야 하므로이 방향 hello 표준 편집기에서 지원 되지 않습니다.

* `TextReader`
* `Stream`
* `ICloudBlob`("inout" 바인딩 방향 필요)
* `CloudBlockBlob`("inout" 바인딩 방향 필요)
* `CloudPageBlob`("inout" 바인딩 방향 필요)
* `CloudAppendBlob`("inout" 바인딩 방향 필요)

텍스트 blob 예상 되는 경우 바인딩할 수도 있습니다 tooa.NET `string` 유형입니다. 이 hello blob 크기가 작으면 hello 전체 blob 콘텐츠가 메모리에 로드 될 때에 권장 됩니다. 일반적으로 선호 toouse을가 `Stream` 또는 `CloudBlockBlob` 유형입니다.

## <a name="trigger-sample"></a>트리거 샘플
Blob 저장소 트리거를 정의 하는 function.json 다음 hello 있다고 가정 합니다.

```json
{
    "disabled": false,
    "bindings": [
        {
            "name": "myBlob",
            "type": "blobTrigger",
            "direction": "in",
            "path": "samples-workitems",
            "connection":"MyStorageAccount"
        }
    ]
}
```

Toohello 모니터링 대상된 컨테이너에 추가 된 각 blob의 hello 내용을 기록 하는 hello 언어 관련 샘플을 참조 하십시오.

* [C#](#triggercsharp)
* [Node.JS](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="blob-trigger-examples-in-c"></a>C#의 Blob 트리거 예 #

```cs
// Blob trigger sample using a Stream binding
public static void Run(Stream myBlob, TraceWriter log)
{
   log.Info($"C# Blob trigger function Processed blob\n Name:{name} \n Size: {myBlob.Length} Bytes");
}
```

```cs
// Blob trigger binding tooa CloudBlockBlob
#r "Microsoft.WindowsAzure.Storage"

using Microsoft.WindowsAzure.Storage.Blob;

public static void Run(CloudBlockBlob myBlob, string name, TraceWriter log)
{
    log.Info($"C# Blob trigger function Processed blob\n Name:{name}\nURI:{myBlob.StorageUri}");
}
```

<a name="triggernodejs"></a>

### <a name="trigger-example-in-nodejs"></a>Node.js의 트리거 예

```javascript
module.exports = function(context) {
    context.log('Node.js Blob trigger function processed', context.bindings.myBlob);
    context.done();
};
```
<a name="outputusage"></a>
<a name="storage-blob-output-binding"></a>

## <a name="using-a-blob-output-binding"></a>Blob 출력 바인딩 사용

.NET 함수에서 사용 해야는 `out string` 매개 변수 함수 서명 또는 hello 목록 다음의 hello 형식 중 하나를 사용 합니다. 에서는 Node.js 함수를 사용 하 여 hello 출력 blob 액세스 `context.bindings.<name>`합니다.

.NET 함수 hello 유형만의 tooany를 출력할 수 있습니다.

* `out string`
* `TextWriter`
* `Stream`
* `CloudBlobStream`
* `ICloudBlob`
* `CloudBlockBlob` 
* `CloudPageBlob` 

<a name="input-sample"></a>

## <a name="queue-trigger-with-blob-input-and-output-sample"></a>Blob 입력 및 출력이 있는 큐 트리거 샘플
정의 하는 hello function.json 다음 가정는 [큐 저장소 트리거](functions-bindings-storage-queue.md), blob 저장소 입력 및 blob 저장소에 출력 합니다. Hello 공지 hello 사용 `queueTrigger` 메타 데이터 속성입니다. hello blob 입력 및 출력에 `path` 속성:

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
      "name": "myInputBlob",
      "type": "blob",
      "path": "samples-workitems/{queueTrigger}",
      "connection": "MyStorageConnection",
      "direction": "in"
    },
    {
      "name": "myOutputBlob",
      "type": "blob",
      "path": "samples-workitems/{queueTrigger}-Copy",
      "connection": "MyStorageConnection",
      "direction": "out"
    }
  ],
  "disabled": false
}
``` 

Hello 입력된 blob toohello 출력 blob를 복사 하는 hello 언어 관련 샘플을 참조 하십시오.

* [C#](#incsharp)
* [Node.JS](#innodejs)

<a name="incsharp"></a>

### <a name="blob-binding-example-in-c"></a>C#의 Blob 바인딩 예 #

```cs
// Copy blob from input toooutput, based on a queue trigger
public static void Run(string myQueueItem, Stream myInputBlob, out string myOutputBlob, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    myOutputBlob = myInputBlob;
}
```

<a name="innodejs"></a>

### <a name="blob-binding-example-in-nodejs"></a>Node.js의 Blob 바인딩 예

```javascript
// Copy blob from input toooutput, based on a queue trigger
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputBlob = context.bindings.myInputBlob;
    context.done();
};
```

## <a name="next-steps"></a>다음 단계
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]


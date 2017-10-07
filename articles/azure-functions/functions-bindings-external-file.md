---
title: "aaaAzure 함수 외부 파일 바인딩 (미리 보기) | Microsoft Docs"
description: "Azure Functions에서 외부 파일 바인딩 사용"
services: functions
documentationcenter: 
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 04/12/2017
ms.author: alkarche
ms.openlocfilehash: 583d9c0b871dc68a79614749ba6ac6711fa820fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-external-file-bindings-preview"></a>Azure Functions 외부 파일 바인딩(미리 보기)
이 문서에서는 어떻게 toomanipulate에서에서 파일을 다른 SaaS 공급자 (예: OneDrive, Dropbox) 기본 제공 바인딩을 사용 하 여 함수 내에서 설명 합니다. Azure Functions는 외부 파일에 대한 트리거, 입력 및 출력 바인딩을 지원합니다.

이 바인딩은 API 연결 tooSaaS 공급자 만들거나 함수 응용 프로그램의 리소스 그룹에서 기존 API 연결을 사용 합니다.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="supported-file-connections"></a>지원되는 파일 연결

|커넥터|트리거|입력|출력|
|:-----|:---:|:---:|:---:|
|[Box](https://www.box.com)|x|x|x
|[Dropbox](https://www.dropbox.com)|x|x|x
|[FTP](https://docs.microsoft.com/azure/app-service-web/app-service-deploy-ftp)|x|x|x
|[OneDrive](https://onedrive.live.com)|x|x|x
|[OneDrive for Business](https://onedrive.live.com/about/business/)|x|x|x
|[SFTP](https://docs.microsoft.com/azure/connectors/connectors-create-api-sftp)|x|x|x
|[Google 드라이브](https://www.google.com/drive/)||x|x|

> [!NOTE]
> 외부 파일 연결은 [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list)에서도 사용할 수 있습니다

## <a name="external-file-trigger-binding"></a>외부 파일 트리거 바인딩

hello Azure 외부 파일 트리거를 사용 하 여 원격 폴더를 모니터링 하 고 변경 되 면 함수 코드를 실행할 수 있습니다.

다음 JSON 개체에 hello hello를 사용 하는 hello 외부 파일 트리거 `bindings` function.json의 배열

```json
{
  "type": "apiHubFileTrigger",
  "name": "<Name of input parameter in function signature>",
  "direction": "in",
  "path": "<folder toomonitor, and optionally a name pattern - see below>",
  "connection": "<name of external file connection - see above>"
}
```
<!---
See one of hello following subheadings for more information:

* [Name patterns](#pattern)
* [File receipts](#receipts)
* [Handling poison files](#poison)
--->

<a name="pattern"></a>

### <a name="name-patterns"></a>이름 패턴
Hello에 파일 이름 패턴을 지정할 수 있습니다 `path` 속성입니다. 참조 된 hello 폴더 hello SaaS 공급자에 있어야 합니다.
예제:

```json
"path": "input/original-{name}",
```

이 경로 명명 된 파일을 찾을 *원래 File1.txt* hello에 *입력* 폴더 및 hello hello 값 `name` 함수 코드에서 변수 것 `File1.txt`합니다.

다른 예제:

```json
"path": "input/{filename}.{fileextension}",
```

이 경로 라는 파일을 찾을 수도 *원래 File1.txt*, 및의 hello hello 값 `filename` 및 `fileextension` 함수 코드에서 변수 것 *원래 File1* 및  *txt*합니다.

Hello 파일 확장명에 대 한 고정된 값을 사용 하 여 hello 파일 형식의 파일을 제한할 수 있습니다. 예:

```json
"path": "samples/{name}.png",
```

이 경우만 *.png* hello에 대 한 파일 *샘플* 폴더 트리거 hello 기능입니다.

중괄호는 이름 패턴에서 특수 문자입니다. 중괄호 hello 이름, 이중 hello 중괄호에에서 포함 된 toospecify 파일 이름입니다.
예:

```json
"path": "images/{{20140101}}-{name}",
```

이 경로 명명 된 파일을 찾을 *{20140101}-soundfile.mp3* hello에 *이미지* 폴더 및 hello `name` 번호 hello 함수 코드에서 변수 값은 *soundfile.mp3*.

<a name="receipts"></a>

<!--- ### File receipts
hello Azure Functions runtime makes sure that no external file trigger function gets called more than once for hello same new or updated file.
It does so by maintaining *file receipts* toodetermine if a given file version has been processed.

File receipts are stored in a folder named *azure-webjobs-hosts* in hello Azure storage account for your function app
(specified by hello `AzureWebJobsStorage` app setting). A file receipt has hello following information:

* hello triggered function ("*&lt;function app name>*.Functions.*&lt;function name>*", for example: "functionsf74b96f7.Functions.CopyFile")
* hello folder name
* hello file type ("BlockFile" or "PageFile")
* hello file name
* hello ETag (a file version identifier, for example: "0x8D1DC6E70A277EF")

tooforce reprocessing of a file, delete hello file receipt for that file from hello *azure-webjobs-hosts* folder manually.
--->
<a name="poison"></a>

### <a name="handling-poison-files"></a>포이즌 파일 처리
외부 파일 트리거 함수가 실패 하면 Azure 함수 기본적으로 (hello 첫 번째 시도가 포함)에 대해 지정된 된 파일에의 한 too5 시간 해당 기능을 다시 시도 합니다.
함수 라는 메시지 tooa 저장소 큐 5 모든 시도 실패 하는 경우 추가 *webjobs-apihubtrigger-포이즌*합니다. 포이즌 파일에 대 한 hello 큐 메시지는 hello 다음과 같은 속성을 포함 하는 JSON 개체:

* FunctionId (hello 형태로 표시  *&lt;함수 응용 프로그램 이름 >*합니다. 함수입니다.  *&lt;함수 이름 >*)
* FileType
* FolderName
* FileName
* ETag(파일 버전 식별자, 예: "0x8D1DC6E70A277EF")


<a name="triggerusage"></a>

## <a name="trigger-usage"></a>트리거 사용
C# 기능을 같은 프로그램 함수 서명에서 명명된 된 매개 변수를 사용 하 여 toohello 입력된 파일 데이터 바인딩할 `<T> <name>`합니다.
여기서 `T` hello 데이터 형식은 toodeserialize hello 데이터를 원하는 및 `paramName` hello 이름에 지정 된는 [JSON 트리거할](#trigger)합니다. 에서는 Node.js 함수를 사용 하 여 hello 입력된 파일 데이터 액세스 `context.bindings.<name>`합니다.

hello 다음 형식 중 하나로 hello 파일을 deserialize 할 수 있습니다.

* 모든 [개체](https://msdn.microsoft.com/library/system.object.aspx)는 JSON 직렬화된 파일 데이터에 유용합니다.
  사용자 지정 입력된 형식을 선언 하는 경우 (예: `FooType`), Azure 함수에 지정 된 형식으로 toodeserialize hello JSON 데이터를 시도 합니다.
* 문자열은 텍스트 파일 데이터에 유용합니다.

C# 기능을에서 형식에 따라 hello tooany을 바인딩할 수 있습니다 하 고 hello 함수 런타임에서 해당 형식을 사용 하 여 hello 파일 데이터를 deserialize 하려고 시도 합니다.

* `string`
* `byte[]`
* `Stream`
* `StreamReader`
* `TextReader`

## <a name="trigger-sample"></a>트리거 샘플
있다고 가정 하면 다음 function.json hello, 외부 파일 트리거를 정의 하는:

```json
{
    "disabled": false,
    "bindings": [
        {
            "name": "myFile",
            "type": "apiHubFileTrigger",
            "direction": "in",
            "path": "samples-workitems",
            "connection": "<name of external file connection>"
        }
    ]
}
```

모니터링 되는 폴더로 toohello 추가 된 각 파일의 hello 내용을 기록 하는 hello 언어 관련 샘플을 참조 하십시오.

* [C#](#triggercsharp)
* [Node.JS](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-usage-in-c"></a>C#에서 트리거 사용 #

```cs
public static void Run(string myFile, TraceWriter log)
{
    log.Info($"C# File trigger function processed: {myFile}");
}
```

<!--
<a name="triggerfsharp"></a>
### Trigger usage in F# ##
```fsharp

```
-->

<a name="triggernodejs"></a>

### <a name="trigger-usage-in-nodejs"></a>Node.js에서 트리거 사용

```javascript
module.exports = function(context) {
    context.log('Node.js File trigger function processed', context.bindings.myFile);
    context.done();
};
```

<a name="input"></a>

## <a name="external-file-input-binding"></a>외부 파일 입력 바인딩
hello Azure 외부 파일 입력된 바인딩을 통해 toouse를 함수에서 외부 폴더에서 파일을 수 있습니다.

hello 외부 파일 입력된 tooa 함수 사용 하 여 다음 JSON 개체에 hello hello `bindings` function.json의 배열:

```json
{
  "name": "<Name of input parameter in function signature>",
  "type": "apiHubFile",
  "direction": "in",
  "path": "<Path of input file - see below>",
  "connection": "<name of external file connection>"
},
```

참고 hello 다음.

* `path`hello 폴더 이름 및 hello 파일 이름을 포함 해야 합니다. 예를 들어, 있는 경우는 [큐 트리거](functions-bindings-storage-queue.md) 함수에서 사용할 수 있습니다 `"path": "samples-workitems/{queueTrigger}"` hello에서 toopoint tooa 파일 `samples-workitems` hello 트리거 메시지에 지정 된 hello 파일 이름과 일치 하는 이름으로 폴더입니다.   

<a name="inputusage"></a>

## <a name="input-usage"></a>입력 사용
C# 기능을 같은 프로그램 함수 서명에서 명명된 된 매개 변수를 사용 하 여 toohello 입력된 파일 데이터 바인딩할 `<T> <name>`합니다.
여기서 `T` hello 데이터 형식은 toodeserialize hello 데이터를 지정 하 고 `paramName` hello 이름에 지정 된는 [입력 바인딩의](#input)합니다. 에서는 Node.js 함수를 사용 하 여 hello 입력된 파일 데이터 액세스 `context.bindings.<name>`합니다.

hello 다음 형식 중 하나로 hello 파일을 deserialize 할 수 있습니다.

* 모든 [개체](https://msdn.microsoft.com/library/system.object.aspx)는 JSON 직렬화된 파일 데이터에 유용합니다.
  사용자 지정 입력된 형식을 선언 하는 경우 (예: `InputType`), Azure 함수에 지정 된 형식으로 toodeserialize hello JSON 데이터를 시도 합니다.
* 문자열은 텍스트 파일 데이터에 유용합니다.

C# 기능을에서 형식에 따라 hello tooany을 바인딩할 수 있습니다 하 고 hello 함수 런타임에서 해당 형식을 사용 하 여 hello 파일 데이터를 deserialize 하려고 시도 합니다.

* `string`
* `byte[]`
* `Stream`
* `StreamReader`
* `TextReader`


<a name="output"></a>

## <a name="external-file-output-binding"></a>외부 파일 출력 바인딩
hello Azure 외부 파일 출력 바인딩을 통해 toowrite 파일 tooan 함수에서 외부 폴더 수 있습니다.

다음 JSON 개체에 hello hello를 사용 하는 함수 출력 hello 외부 파일 `bindings` function.json의 배열:

```json
{
  "name": "<Name of output parameter in function signature>",
  "type": "apiHubFile",
  "direction": "out",
  "path": "<Path of input file - see below>",
  "connection": "<name of external file connection>"
}
```

참고 hello 다음.

* `path`hello 폴더 이름 및 hello 파일 이름 toowrite를 포함 해야 합니다. 예를 들어, 있는 경우는 [큐 트리거](functions-bindings-storage-queue.md) 함수에서 사용할 수 있습니다 `"path": "samples-workitems/{queueTrigger}"` hello에서 toopoint tooa 파일 `samples-workitems` hello 트리거 메시지에 지정 된 hello 파일 이름과 일치 하는 이름으로 폴더입니다.   

<a name="outputusage"></a>

## <a name="output-usage"></a>출력 사용
C# 함수를 명명 된 hello를 사용 하 여 toohello 출력 파일 바인딩할 `out` 함수 시그니처의 매개 변수 같은 `out <T> <name>`여기서 `T` hello 데이터 형식은 tooserialize hello 데이터를 지정 하 고 `paramName` 는 hello 이름을 에 지정 된 된 [출력 바인딩이](#output)합니다. 에서는 Node.js 함수를 사용 하 여 hello 출력 파일 액세스 `context.bindings.<name>`합니다.

유형만 hello를 사용 하 여 toohello 출력 파일을 작성할 수 있습니다.

* 모든 [개체](https://msdn.microsoft.com/library/system.object.aspx)는 JSON 직렬화에 유용합니다.
  사용자 지정 출력 형식을 선언 하는 경우 (예: `out OutputType paramName`), Azure 함수 tooserialize 개체를 JSON으로 시도 합니다. Hello 함수가 종료 되 면 hello 출력 매개 변수가 null 이면 hello 함수 런타임 개체를 null로 파일을 만듭니다.
* 문자열(`out string paramName`)은 텍스트 파일 데이터에 유용합니다. hello 함수 런타임 hello 함수가 종료 되 면 문자열 매개 변수는 null이 아닌 경우에 파일을 만듭니다.

C# 함수에서의 hello 유형만 tooany를 출력할 수 있습니다.

* `TextWriter`
* `Stream`
* `CloudFileStream`
* `ICloudFile`
* `CloudBlockFile`
* `CloudPageFile`

<a name="outputsample"></a>

<a name="sample"></a>

## <a name="input--output-sample"></a>입력 + 출력 샘플
정의 하는 hello function.json 다음 가정는 [저장소 큐 트리거](functions-bindings-storage-queue.md), 외부 파일 입력 및 출력 외부 파일:

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
      "name": "myInputFile",
      "type": "apiHubFile",
      "path": "samples-workitems/{queueTrigger}",
      "connection": "<name of external file connection>",
      "direction": "in"
    },
    {
      "name": "myOutputFile",
      "type": "apiHubFile",
      "path": "samples-workitems/{queueTrigger}-Copy",
      "connection": "<name of external file connection>",
      "direction": "out"
    }
  ],
  "disabled": false
}
```

Hello 입력된 파일 toohello 출력 파일을 복사 하는 hello 언어 관련 샘플을 참조 하십시오.

* [C#](#incsharp)
* [Node.JS](#innodejs)

<a name="incsharp"></a>

### <a name="usage-in-c"></a>C#에서 사용 #

```cs
public static void Run(string myQueueItem, string myInputFile, out string myOutputFile, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    myOutputFile = myInputFile;
}
```

<!--
<a name="infsharp"></a>
### Input usage in F# ##
```fsharp

```
-->

<a name="innodejs"></a>

### <a name="usage-in-nodejs"></a>Node.js에서 사용

```javascript
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputFile = context.bindings.myInputFile;
    context.done();
};
```

## <a name="next-steps"></a>다음 단계
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

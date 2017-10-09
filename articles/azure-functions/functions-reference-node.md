---
title: "Azure 함수에 대 한 aaaJavaScript 개발자 참조 | Microsoft Docs"
description: "JavaScript를 사용 하 여 toodevelop 작동 하는 방식을 이해 합니다."
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: "Azure Functions, 함수, 이벤트 처리, webhook, 동적 계산, 서버가 없는 아키텍처"
ms.assetid: 45dedd78-3ff9-411f-bb4b-16d29a11384c
ms.service: functions
ms.devlang: nodejs
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/25/2017
ms.author: glenga
ms.openlocfilehash: 6220b42f965b6ee2463341aaf270836623fdf7fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-javascript-developer-guide"></a>Azure Functions JavaScript 개발자 가이드
> [!div class="op_single_selector"]
> * [C# 스크립트](functions-reference-csharp.md)
> * [F# 스크립트](functions-reference-fsharp.md)
> * [JavaScript](functions-reference-node.md)
> 
> 

Azure 함수 쉽게 tooexport 변수로 전달 되는 함수를 사용 하면에 대 한 JavaScript 경험 hello는 `context` hello 런타임와의 통신에 대 한 데이터 바인딩을 통해 전송 및 수신 하는 개체입니다.

이 문서에서는 hello 이미 읽어본 가정 [Azure 함수 개발자 참조](functions-reference.md)합니다.

## <a name="exporting-a-function"></a>함수 내보내기
모든 JavaScript 함수는 단일 내보내야 `function` 통해 `module.exports` hello 런타임용 toofind 함수 hello 하 고 실행 합니다. 이 함수에는 `context` 개체가 항상 포함되어야 합니다.

```javascript
// You must include a context, but other arguments are optional
module.exports = function(context) {
    // Additional inputs can be accessed by hello arguments property
    if(arguments.length === 4) {
        context.log('This function has 4 inputs');
    }
};
// or you can include additional inputs in your arguments
module.exports = function(context, myTrigger, myInput, myOtherInput) {
    // function logic goes here :)
};
```

바인딩 `direction === "in"` 있습니다 사용할 수 있다는 의미 이므로 함수 인수로 전달 됩니다 [ `arguments` ](https://msdn.microsoft.com/library/87dw3w1k.aspx) toodynamically 새로운 입력 처리 (사용 하 여 예를 들어 `arguments.length` tooiterate 모든 입력을 통해). 이 기능은 `context` 개체를 참조하지 않고 트리거 데이터에 예측 가능한 방식으로 액세스할 수 있으므로 트리거만 있고 추가 입력이 없는 경우에 편리합니다.

hello 인수는 항상 toohello 함수에서 발생 하는 hello 순서에 따라 전달 *function.json*내보내기 문에 지정 하지 않으면 경우에 합니다. 예를 들어 `function(context, a, b)` 너무 변경`function(context, a)`, hello 값을 가져올 수 있습니다 `b` 너무 참조 하 여 함수 코드에서`arguments[3]`합니다.

방향에 관계 없이 모든 바인딩은 hello에 따라 전송 되도 `context` 개체 (hello 다음 스크립트 참조). 

## <a name="context-object"></a>context 개체
hello 런타임에서 사용 하 여 한 `context` 개체 toopass 데이터 tooand 함수 및 toolet hello 런타임과 통신 합니다.

hello 컨텍스트 개체는 항상 첫 번째 매개 변수 tooa 함수 hello 및 메서드를 같은 있기 때문에 포함 되어야 합니다 `context.done` 및 `context.log`, 필요한 toouse hello 런타임을 올바르게 않는 합니다. 원하는 대로 지정 hello 개체 이름을 지정할 수 있습니다 (예를 들어 `ctx` 또는 `c`).

```javascript
// You must include a context, but other arguments are optional
module.exports = function(context) {
    // function logic goes here :)
};
```

### <a name="contextbindings-property"></a>context.bindings 속성

```
context.bindings
```
모든 입력 및 출력 데이터를 포함하는 명명된 개체를 반환합니다. 예를 들어 다음 바인딩 정의 hello 프로그램 *function.json* 액세스할 수 있습니다 hello hello에서 hello 큐의 내용을 `context.bindings.myInput` 개체입니다. 

```json
{
    "type":"queue",
    "direction":"in",
    "name":"myInput"
    ...
}
```

```javascript
// myInput contains hello input data, which may have properties such as "name"
var author = context.bindings.myInput.name;
// Similarly, you can set your output data
context.bindings.myOutput = { 
        some_text: 'hello world', 
        a_number: 1 };
```

### <a name="contextdone-method"></a>context.done 메서드
```
context.done([err],[propertyBag])
```

Hello 런타임을 코드 완료 되었음을 알립니다. 호출 해야 `context.done`, 또는 다른 hello 런타임 모릅니다 함수가 완료 되 고 hello 실행 시간이 초과 됩니다. 

hello `context.done` 메서드를 사용 하면 toopass 백업 하는 사용자 정의 오류 toohello 런타임과 hello에 hello 속성을 덮어쓸 수 있는 속성의 속성 모음은 `context.bindings` 개체입니다.

```javascript
// Even though we set myOutput toohave:
//  -> text: hello world, number: 123
context.bindings.myOutput = { text: 'hello world', number: 123 };
// If we pass an object toohello done function...
context.done(null, { myOutput: { text: 'hello there, world', noNumber: true }});
// hello done method will overwrite hello myOutput binding toobe: 
//  -> text: hello there, world, noNumber: true
```

### <a name="contextlog-method"></a>context.log 메서드  

```
context.log(message)
```
Hello 기본 추적 수준의 toowrite toohello 스트리밍 콘솔 로그 수 있습니다. `context.log`추가 로깅이 메서드, 다른 추적 수준 toohello 콘솔 로그를 작성할 수 있는 사용할 수 없습니다.


| 메서드                 | 설명                                |
| ---------------------- | ------------------------------------------ |
| **error(_message_)**   | Tooerror 수준을 로깅, 또는 더 낮은 씁니다.   |
| **warn(_message_)**    | Toowarning 수준을 로깅, 또는 더 낮은 씁니다. |
| **info(_message_)**    | Tooinfo 수준을 로깅, 또는 더 낮은 씁니다.    |
| **verbose(_message_)** | Tooverbose 수준 로깅을 씁니다.           |

hello 다음 예제에서는 기록 hello 경고 추적 수준에서 toohello 콘솔:

```javascript
context.log.warn("Something has happened."); 
```
Hello host.json 파일에서 로그인을 위한 hello 추적 수준이 임계값을 설정 하거나 해제할 수 있습니다.  Toowrite toohello 기록 하는 방법에 대 한 자세한 내용은 hello 다음 섹션을 참조 하세요.

## <a name="binding-data-type"></a>바인딩 데이터 형식

toodefine hello 데이터 형식 입력 바인딩의 경우 hello를 사용 하 여 `dataType` hello 바인딩 정의에 속성입니다. 예를 들어 tooread hello 이진 형식으로 HTTP 요청 콘텐츠 형식을 사용 하십시오 hello `binary`:

```json
{
    "type": "httpTrigger",
    "name": "req",
    "direction": "in",
    "dataType": "binary"
}
```

`dataType`에 대한 다른 옵션은 `stream` 및 `string`입니다.

## <a name="writing-trace-output-toohello-console"></a>쓰기 추적 출력 toohello 콘솔 

함수를 사용 하 여 hello `context.log` 메서드 toowrite 추적 출력 toohello 콘솔. 이 시점에서 사용할 수 없습니다 `console.log` toowrite toohello 콘솔.

호출 하는 경우 `context.log()`, 메시지는 hello는 hello 기본 추적 수준 toohello 콘솔 쓰여집니다 _정보_ 추적 수준입니다. hello 다음 코드를 작성 hello 정보 추적 수준에서 toohello 콘솔 합니다.

```javascript
context.log({hello: 'world'});  
```

hello 위 코드는 해당 toohello 코드 다음:

```javascript
context.log.info({hello: 'world'});  
```

hello 다음 코드를 작성 hello 오류 수준에서 toohello 콘솔 합니다.

```javascript
context.log.error("An error has occurred.");  
```

때문에 _오류_ 은 hello 가장 높은 추적 수준에서이 추적이 기록 됩니다 모든 추적 수준에서 toohello 출력으로 로깅은 사용 됩니다.  


모든 `context.log` 메서드 지원 hello hello Node.js에서 지원 되는 동일한 매개 변수 형식이 [util.format 메서드](https://nodejs.org/api/util.html#util_util_format_format)합니다. Hello toohello 콘솔 hello 기본 추적 수준을 사용 하 여 작성 하는 코드를 다음을 고려 합니다.

```javascript
context.log('Node.js HTTP trigger function processed a request. RequestUri=' + req.originalUrl);
context.log('Request Headers = ' + JSON.stringify(req.headers));
```

또한 쓰기 hello 동일의 코드 형식에 따라 hello에서 수행할 수 있습니다.

```javascript
context.log('Node.js HTTP trigger function processed a request. RequestUri=%s', req.originalUrl);
context.log('Request Headers = ', JSON.stringify(req.headers));
```

### <a name="configure-hello-trace-level-for-console-logging"></a>콘솔 로깅에 대 한 추적 수준을 hello 구성

함수에는 쉽게 toocontrol hello 방식으로 추적 toohello 콘솔 함수에서 작성 하므로 toohello 콘솔 작성 하기 위한 hello 임계값 추적 수준을 정의할 수 있습니다. toohello 콘솔을 사용 하 여 hello를 작성 하는 모든 추적에 대 한 tooset hello 임계값 `tracing.consoleLevel` hello host.json 파일의 속성입니다. 이 설정은 tooall 앱에서 함수에 함수를 적용합니다. hello 다음 예제에서는 설정 hello 추적 임계값 tooenable 자세한 정보 로깅:

```json
{ 
    "tracing": {      
        "consoleLevel": "verbose"     
    }
}  
```

값 **consoleLevel** hello toohello 이름을 해당 `context.log` 메서드. toodisable 모든 추적 toohello 콘솔 로깅이 설정 **consoleLevel** too_off_ 합니다. Hello host.json 파일에 대 한 자세한 내용은 참조 hello [host.json 참조 항목](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json)합니다.

## <a name="http-triggers-and-bindings"></a>HTTP 트리거 및 바인딩

HTTP 및 webhook 트리거 및 HTTP 요청 및 응답 개체 toorepresent hello HTTP 메시징 바인딩을 사용 하 여 출력 합니다.  

### <a name="request-object"></a>요청 개체

hello `request` 개체에 hello 다음과 같은 속성:

| 속성      | 설명                                                    |
| ------------- | -------------------------------------------------------------- |
| _body_        | Hello hello 요청 본문을 포함 하는 개체입니다.               |
| _headers_     | Hello 요청 헤더를 포함 하는 개체입니다.                   |
| _method_      | hello hello 요청의 HTTP 메서드입니다.                                |
| _originalUrl_ | hello 요청의 hello URL입니다.                                        |
| _params_      | Hello 요청의 hello 라우팅 매개 변수를 포함 하는 개체입니다. |
| _query_       | Hello 쿼리 매개 변수를 포함 하는 개체입니다.                  |
| _rawBody_     | hello 본문을 문자열로 hello 메시지입니다.                           |


### <a name="response-object"></a>응답 개체

hello `response` 개체에 hello 다음과 같은 속성:

| 속성  | 설명                                               |
| --------- | --------------------------------------------------------- |
| _body_    | Hello hello 응답 본문을 포함 하는 개체입니다.         |
| _headers_ | Hello 응답 헤더를 포함 하는 개체입니다.             |
| _isRaw_   | Hello 응답에 대 한 서식 지정을 건너뜀을 나타냅니다.    |
| _상태_  | hello hello 응답의 HTTP 상태 코드입니다.                     |

### <a name="accessing-hello-request-and-response"></a>Hello 요청 및 응답에 액세스 

HTTP 트리거와 함께 작업할 때 세 가지 방법 중 하나로 hello HTTP 요청 및 응답 개체를 액세스할 수 있습니다.

+ Hello 명명 된 입력 및 출력 바인딩 합니다. 이러한 방식으로 hello HTTP 트리거와 바인딩 작업 hello 동일 다른 바인딩으로 합니다. hello 다음 예제에서는 설정 hello 응답 개체 명명 된를 사용 하 여 `response` 바인딩: 

    ```javascript
    context.bindings.response = { status: 201, body: "Insert succeeded." };
    ```

+ `req` 및 `res` hello에 대 한 속성 `context` 개체입니다. 이러한 방식으로 전체 toouse hello 대신 hello 컨텍스트 개체에서 hello 규칙에 따른 패턴 tooaccess HTTP 데이터를 사용할 수 있습니다 `context.bindings.name` 패턴입니다. hello 방법을 예제와 다음 tooaccess hello `req` 및 `res` 개체에 hello `context`:

    ```javascript
    // You can access your http request off hello context ...
    if(context.req.body.emoji === ':pizza:') context.log('Yay!');
    // and also set your http response
    context.res = { status: 202, body: 'You successfully ordered more coffee!' }; 
    ```

+ `context.done()`을 호출합니다. Toohello 전달 되는 hello 응답을 반환 하는 특수 한 유형의 HTTP 바인딩 `context.done()` 메서드. 다음 HTTP hello 출력 바인딩이 정의 하는 `$return` 출력 매개 변수:

    ```json
    {
      "type": "http",
      "direction": "out",
      "name": "$return"
    }
    ``` 
    이 출력 바인딩의 프로시저 해야 toosupply hello 응답을 호출할 때 `done()`, 다음과 같습니다.

    ```javascript
     // Define a valid response object.
    res = { status: 201, body: "Insert succeeded." };
    context.done(null, res);   
    ```  

## <a name="node-version-and-package-management"></a>노드 버전 및 패키지 관리
hello 노드 버전에서 현재 잠겨 `6.5.0`합니다. 더 많은 버전에 대한 지원을 추가하고 구성할 수 있도록 연구 중입니다.

단계를 수행 하는 hello 함수 응용 프로그램에 패키지를 포함할 수 있습니다. 

1. 너무 이동`https://<function_app_name>.scm.azurewebsites.net`합니다.

2. **디버그 콘솔** > **CMD**를 클릭합니다.

3. 너무 이동`D:\home\site\wwwroot`, package.json 파일 toohello 끌어와서 **wwwroot** hello 페이지의 위쪽 절반 hello 폴더입니다.  
    또한 다른 방법으로 tooyour 함수 응용 프로그램 파일을 업로드할 수 있습니다. 자세한 내용은 참조 [tooupdate 앱 파일을 어떻게 작동 하는지](functions-reference.md#fileupdate)합니다. 

4. Hello package.json 파일을 업로드 한 후 실행 hello `npm install` hello 명령을 **Kudu 원격 실행 콘솔**합니다.  
    이 작업 hello package.json 파일에 표시 된 hello 패키지를 다운로드 하 고 hello 함수 응용 프로그램을 다시 시작 합니다.

Hello 필요한 패키지를 설치한 후 가져올 tooyour 함수를 호출 하 여 `require('packagename')`와 같이, 다음 예제는 hello:

```javascript
// Import hello underscore.js library
var _ = require('underscore');
var version = process.version; // version === 'v6.5.0'

module.exports = function(context) {
    // Using our imported underscore.js library
    var matched_names = _
        .where(context.bindings.myInput.names, {first: 'Carla'});
```

정의 해야는 `package.json` 함수 응용 프로그램의 hello 루트에 파일입니다. 정의 hello 파일 hello 최상의 성능을 제공 하는 동일한 캐시 된 패키지를 hello hello 앱 공유의 모든 기능을 사용 합니다. 버전 충돌이 발생할 경우 추가 하 여 해결할 수 있습니다는 `package.json` 특정 함수 hello 폴더의 파일입니다.  

## <a name="environment-variables"></a>환경 변수
tooget 환경 변수 또는 응용 프로그램 설정 값을 사용 하 여 `process.env`hello 다음 코드 예제에에서 나온 것 처럼:

```javascript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();

    context.log('Node.js timer trigger function ran!', timeStamp);   
    context.log(GetEnvironmentVariable("AzureWebJobsStorage"));
    context.log(GetEnvironmentVariable("WEBSITE_SITE_NAME"));

    context.done();
};

function GetEnvironmentVariable(name)
{
    return name + ": " + process.env[name];
}
```
## <a name="considerations-for-javascript-functions"></a>JavaScript 함수에 대한 고려 사항

JavaScript 함수를 사용 하는 경우에 다음 두 섹션 hello에 hello 고려 사항에 주의 합니다.

### <a name="choose-single-core-app-service-plans"></a>단일 코어 App Service 계획 선택

앱 서비스 계획 hello를 사용 하는 함수 앱을 만들 때 여러 코어를 사용 하 여 계획 보다는 단일 코어 계획을 선택 하는 것이 좋습니다. 오늘날 함수 실행 JavaScript 함수가 더 효율적으로 단일 코어 Vm에서 되며 더 큰 Vm을 사용 하 여 hello 예상 성능 향상을 생성 하지 않습니다. 필요한 경우 더 많은 단일 코어 VM 인스턴스를 추가하여 수동으로 확장하거나 자동 크기 조정을 사용하도록 설정할 수 있습니다. 자세한 내용은 [수동 또는 자동으로 인스턴스 개수 조정](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json)을 참조하세요.    

### <a name="typescript-and-coffeescript-support"></a>TypeScript 및 CoffeeScript 지원
직접적으로 지원 아직 존재 하지 않는 자동 컴파일 TypeScript 또는 CoffeeScript에 대 한 hello 런타임을 통해, 때문에 이러한 지원이 toobe 배포 시 hello 런타임 외부 처리 해야 합니다. 

## <a name="next-steps"></a>다음 단계
자세한 내용은 다음 리소스는 hello 참조:

* [Azure Functions에 대한 모범 사례](functions-best-practices.md)
* [Azure Functions 개발자 참조](functions-reference.md)
* [Azure Functions C# 개발자 참조](functions-reference-csharp.md)
* [Azure Functions F# 개발자 참조](functions-reference-fsharp.md)
* [Azure Functions 트리거 및 바인딩](functions-triggers-bindings.md)


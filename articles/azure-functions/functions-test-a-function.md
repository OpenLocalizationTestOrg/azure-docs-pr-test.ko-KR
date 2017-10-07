---
title: "Azure 함수 aaaTesting | Microsoft Docs"
description: "Postman, cURL 및 Node.js를 사용하여 Azure 함수를 테스트합니다."
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: "Azure Functions, 함수, 이벤트 처리, webhook, 동적 계산, 서버가 없는 아키텍처, 테스트"
ms.assetid: c00f3082-30d2-46b3-96ea-34faf2f15f77
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 02/02/2017
ms.author: wesmc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a084f8dbc8089356c3c19d789dc9098f2bb63052
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="strategies-for-testing-your-code-in-azure-functions"></a>Azure Functions에서 코드를 테스트하기 위한 전략

이 항목 뒤 일반 hello를 사용 하는 등의 다양 한 방법으로 tootest 함수에 도달 하는 hello를 보여 줍니다.

+ cURL, Postman, 웹 기반 트리거에 대한 웹 브라우저 등의 HTTP 기반 도구
+ Azure 저장소 탐색기, tootest Azure 저장소 기반 트리거
+ Hello 함수 Azure 포털의 테스트 탭
+ 타이머로 트리거되는 함수
+ 테스트 응용 프로그램 또는 프레임워크

모든 이러한 테스트 메서드 함수를 사용할 HTTP 트리거 중 하나를 통해 입력을 허용 하는 쿼리 문자열 매개 변수 또는 hello 요청 본문. Hello 첫 번째 섹션에서이 함수를 만듭니다.

## <a name="create-a-function-for-testing"></a>테스트용 함수 만들기
이 자습서의 대부분의 경우 약간 수정 된 버전의 hello 함수를 만들 때 사용할 수 있는 HttpTrigger JavaScript 함수 템플릿 사용 합니다. 함수를 만드는 데 도움이 필요한 경우 이 [자습서](functions-create-first-azure-function.md)를 검토하세요. Hello 선택 **HttpTrigger-JavaScript** hello에서 hello 테스트 함수를 만들 때 템플릿을 [Azure 포털]합니다.

hello 기본 함수 서식 파일은 기본적으로 hello 요청 본문 또는 쿼리 문자열 매개 변수에서 뒤로 hello 이름을 에코 하는 "hello world" 함수 `name=<your name>`합니다.  에 업데이트 하는 hello 코드 tooalso 사용 tooprovide hello 이름 및 주소 hello 요청 본문의 JSON 콘텐츠입니다. 그런 다음 hello 함수는 사용 가능한 경우 이러한 백 toohello 클라이언트를 에코 합니다.   

테스트를 위해 사용 하는 코드를 다음 hello로 hello 함수를 업데이트 합니다.

```javascript
module.exports = function (context, req) {
    context.log("HTTP trigger function processed a request. RequestUri=%s", req.originalUrl);
    context.log("Request Headers = " + JSON.stringify(req.headers));
    var res;

    if (req.query.name || (req.body && req.body.name)) {
        if (typeof req.query.name != "undefined") {
            context.log("Name was provided as a query string param...");
            res = ProcessNewUserInformation(context, req.query.name);
        }
        else {
            context.log("Processing user info from request body...");
            res = ProcessNewUserInformation(context, req.body.name, req.body.address);
        }
    }
    else {
        res = {
            status: 400,
            body: "Please pass a name on hello query string or in hello request body"
        };
    }
    context.done(null, res);
};
function ProcessNewUserInformation(context, name, address) {
    context.log("Processing user information...");
    context.log("name = " + name);
    var echoString = "Hello " + name;
    var res;

    if (typeof address != "undefined") {
        echoString += "\n" + "hello address you provided is " + address;
        context.log("address = " + address);
    }
    res = {
        // status: 200, /* Defaults too200 */
        body: echoString
    };
    return res;
}
```

## <a name="test-a-function-with-tools"></a>도구를 사용하여 함수 테스트
외부 hello Azure 포털을 사용할 수 있는 tootrigger 함수를 테스트 하기 위한 다양 한 도구가 있습니다. 여기에는 UI 기반 및 명령줄 도구를 모두 포함하는 HTTP 테스트 도구, Azure Storage 액세스 도구 및 간단한 웹 브라우저도 포함됩니다.

### <a name="test-with-a-browser"></a>브라우저를 사용하여 테스트
hello 웹 브라우저는 HTTP 통해 제공 하기 위한 간단한 방법을 tootrigger 함수입니다. 본문 페이로드가 필요하지 않으며 쿼리 문자열 매개 변수만 사용하는 GET 요청에 대해서는 브라우저를 사용할 수 있습니다.

이전에 정의한 복사 hello tootest hello 함수 **함수 Url** hello 포털에서 합니다. 여기에 다음 폼 hello에 있습니다.

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

Hello 추가 `name` toohello 쿼리 문자열 매개 변수입니다. Hello에 대 한 실제 이름을 사용 하 여 `<Enter a name here>` 자리 표시자입니다.

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>&name=<Enter a name here>

응답 비슷한 toohello 다음 브라우저에 붙여넣기 hello URL을 받아야 합니다.

![테스트 응답이 표시된 Chrome 브라우저 탭의 스크린샷](./media/functions-test-a-function/browser-test.png)

이 예제는 XML 문자열을 반환 하는 hello를 래핑하는 hello Chrome 브라우저. 다른 브라우저 hello 문자열 값만 표시 됩니다.

Hello 포털에서 **로그** 창, 출력 유사한 toohello 다음 hello 함수 실행에 기록 됩니다.

    2016-03-23T07:34:59  Welcome, you are now connected toolog-streaming service.
    2016-03-23T07:35:09.195 Function started (Id=61a8c5a9-5e44-4da0-909d-91d293f20445)
    2016-03-23T07:35:10.338 Node.js HTTP trigger function processed a request. RequestUri=https://functionsExample.azurewebsites.net/api/WesmcHttpTriggerNodeJS1?code=XXXXXXXXXX==&name=Glenn from a browser
    2016-03-23T07:35:10.338 Request Headers = {"cache-control":"max-age=0","connection":"Keep-Alive","accept":"text/html","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T07:35:10.338 Name was provided as a query string param.
    2016-03-23T07:35:10.338 Processing User Information...
    2016-03-23T07:35:10.369 Function completed (Success, Id=61a8c5a9-5e44-4da0-909d-91d293f20445)

### <a name="test-with-postman"></a>Postman을 사용하여 테스트
권장 도구 tootest hello 함수 대부분 우체부 hello Chrome 브라우저 통합 하는 것입니다. tooinstall 우체부, 참조 [가져오기 우체부](https://www.getpostman.com/)합니다. Postman은 다양한 특성의 HTTP 요청에 대한 제어를 제공합니다.

> [!TIP]
> 와 가장 편리 하 게 hello HTTP 테스트 도구를 사용 합니다. 다음은 몇 가지 대안 tooPostman입니다.  
>
> * [Fiddler](http://www.telerik.com/fiddler)  
> * [Paw](https://luckymarmot.com/paw)  
>
>

우체부에는 요청 본문으로 tootest hello 함수:

1. Hello에서 우체부 시작 **앱** Chrome 브라우저 창의 hello 왼쪽 위 모퉁이의 단추입니다.
2. **함수 Url**을 복사하여 Postman에 붙여 넣습니다. Hello 액세스 코드 쿼리 문자열 매개 변수를 포함합니다.
3. Hello HTTP 메서드를도 변경**POST**합니다.
4. 클릭 **본문** > **원시**, JSON 요청 본문 비슷한 toohello 다음 추가:

    ```json
    {
        "name" : "Wes testing with Postman",
        "address" : "Seattle, WA 98101"
    }
    ```
5. **보내기**를 클릭합니다.

hello 다음 이미지 예를 보여 줍니다 테스트 hello 간단한 에코 함수가이 자습서에서는 합니다.

![Postman 사용자 인터페이스의 스크린샷](./media/functions-test-a-function/postman-test.png)

Hello 포털에서 **로그** 창, 출력 유사한 toohello 다음 hello 함수 실행에 기록 됩니다.

    2016-03-23T08:04:51  Welcome, you are now connected toolog-streaming service.
    2016-03-23T08:04:57.107 Function started (Id=dc5db8b1-6f1c-4117-b5c4-f6b602d538f7)
    2016-03-23T08:04:57.763 HTTP trigger function processed a request. RequestUri=https://functions841def78.azurewebsites.net/api/WesmcHttpTriggerNodeJS1?code=XXXXXXXXXX==
    2016-03-23T08:04:57.763 Request Headers = {"cache-control":"no-cache","connection":"Keep-Alive","accept":"*/*","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T08:04:57.763 Processing user info from request body...
    2016-03-23T08:04:57.763 Processing User Information...
    2016-03-23T08:04:57.763 name = Wes testing with Postman
    2016-03-23T08:04:57.763 address = Seattle, W.A. 98101
    2016-03-23T08:04:57.795 Function completed (Success, Id=dc5db8b1-6f1c-4117-b5c4-f6b602d538f7)

### <a name="test-with-curl-from-hello-command-line"></a>CURL hello 명령줄에서 테스트
소프트웨어를 테스트 하는 경우에 종종 아닙니다 필요한 toolook 어떤 hello 명령줄 toohelp 디버그 응용 프로그램 보다 더 이상. 테스트 함수와 전혀 차이가 없습니다. 참고 hello cURL은 Linux 기반 시스템에서 기본적으로 사용할 수 있습니다. Windows에서는 먼저 다운로드 하 여 hello 설치 [cURL 도구](https://curl.haxx.se/)합니다.

tootest hello 함수는 앞에서 정의한, 복사 hello **함수 URL** hello 포털에서 합니다. 여기에 다음 폼 hello에 있습니다.

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

함수를 트리거할 기준이 hello URL입니다. 이 테스트 hello 명령줄 toomake hello cURL 명령을 사용 하 여 GET (`-G` 또는 `--get`) hello 함수에 대 한 요청:

    curl -G https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

이 특정 예제 데이터로 전달 될 수 있는 쿼리 문자열 매개 변수를 (`-d`) hello에 cURL 명령:

    curl -G https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code> -d name=<Enter a name here>

실행된 hello 명령 및 있습니다 hello hello 함수의 출력 hello 명령줄에서 다음을 참조 하십시오.

![명령 프롬프트 출력의 스크린샷](./media/functions-test-a-function/curl-test.png)

Hello 포털에서 **로그** 창, 출력 유사한 toohello 다음 hello 함수 실행에 기록 됩니다.

    2016-04-05T21:55:09  Welcome, you are now connected toolog-streaming service.
    2016-04-05T21:55:30.738 Function started (Id=ae6955da-29db-401a-b706-482fcd1b8f7a)
    2016-04-05T21:55:30.738 Node.js HTTP trigger function processed a request. RequestUri=https://functionsExample.azurewebsites.net/api/HttpTriggerNodeJS1?code=XXXXXXX&name=Azure Functions
    2016-04-05T21:55:30.738 Function completed (Success, Id=ae6955da-29db-401a-b706-482fcd1b8f7a)

### <a name="test-a-blob-trigger-by-using-storage-explorer"></a>저장소 탐색기를 사용하여 Blob 트리거 테스트
[Azure Storage 탐색기](http://storageexplorer.com/)를 사용하여 Blob 트리거 함수를 테스트할 수 있습니다.

1. Hello에 [Azure 포털] 함수 앱에 대 한 C#, F # 또는 JavaScript blob 트리거 함수를 만듭니다. Blob 컨테이너의 hello 경로 toomonitor toohello 이름을 설정 합니다. 예:

        files
2. Hello 클릭  **+**  tooselect 단추 또는 toouse 원하는 hello 저장소 계정을 만듭니다. 그런 다음 **Create**를 클릭합니다.
3. 텍스트를 다음 hello로 텍스트 파일을 만들고 저장:

        A text file for blob trigger function testing.
4. 실행 [Azure 저장소 탐색기](http://storageexplorer.com/), 모니터링 되 고 hello 저장소 계정에서 toohello blob 컨테이너를 연결 합니다.
5. 클릭 **업로드** tooupload hello 텍스트 파일입니다.

    ![저장소 탐색기의 스크린샷](./media/functions-test-a-function/azure-storage-explorer-test.png)

hello 기본 blob 트리거 함수 코드 hello 로그에 hello blob의 hello 처리를 보고합니다.

    2016-03-24T11:30:10  Welcome, you are now connected toolog-streaming service.
    2016-03-24T11:30:34.472 Function started (Id=739ebc07-ff9e-4ec4-a444-e479cec2e460)
    2016-03-24T11:30:34.472 C# Blob trigger function processed: A text file for blob trigger function testing.
    2016-03-24T11:30:34.472 Function completed (Success, Id=739ebc07-ff9e-4ec4-a444-e479cec2e460)

## <a name="test-a-function-within-functions"></a>함수 내에서 함수 테스트
hello Azure 함수 포털은 설계 된 함수를 트리거한 toolet HTTP 및 타이머를 테스트 합니다. 또한 다른 함수는 테스트할 tootrigger 함수를 만들 수 있습니다.

### <a name="test-with-hello-functions-portal-run-button"></a>테스트 실행 단추 포털 hello 함수
hello 포털에서 제공 된 **실행** 단추 toodo 일부 사용할 수 있는 테스트 제한 합니다. Hello 단추를 사용 하 여 요청 본문을 제공할 수 있지만 쿼리 문자열 매개 변수를 제공 하거나 요청 헤더를 업데이트할 수 없습니다.

다음 JSON 문자열 비슷한 toohello hello에 추가 하 여 앞에서 만든 hello HTTP 트리거 기능 테스트 **요청 본문** 필드입니다. Hello 클릭 **실행** 단추입니다.

```json
{
    "name" : "Wes testing Run button",
    "address" : "USA"
}
```

Hello 포털에서 **로그** 창, 출력 유사한 toohello 다음 hello 함수 실행에 기록 됩니다.

    2016-03-23T08:03:12  Welcome, you are now connected toolog-streaming service.
    2016-03-23T08:03:17.357 Function started (Id=753a01b0-45a8-4125-a030-3ad543a89409)
    2016-03-23T08:03:18.697 HTTP trigger function processed a request. RequestUri=https://functions841def78.azurewebsites.net/api/wesmchttptriggernodejs1
    2016-03-23T08:03:18.697 Request Headers = {"connection":"Keep-Alive","accept":"*/*","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T08:03:18.697 Processing user info from request body...
    2016-03-23T08:03:18.697 Processing User Information...
    2016-03-23T08:03:18.697 name = Wes testing Run button
    2016-03-23T08:03:18.697 address = USA
    2016-03-23T08:03:18.744 Function completed (Success, Id=753a01b0-45a8-4125-a030-3ad543a89409)


### <a name="test-with-a-timer-trigger"></a>타이머 트리거를 사용하여 테스트
일부 함수는 앞에서 언급 한 hello 도구로 적절 하 게 테스트할 수 없습니다. 예를 들어 [Azure 큐 저장소](../storage/queues/storage-dotnet-how-to-use-queues.md)에 메시지를 놓을 때 실행되는 큐 트리거 함수를 생각해 보세요. 항상 작성할 수 코드 toodrop 메시지 큐로 있으며 콘솔 프로젝트에서 이러한 예는이 문서의 뒷부분에 제공 됩니다. 그러나 함수를 직접 테스트하는 데 사용할 수 있는 또 다른 방법이 있습니다.  

큐 출력 바인딩으로 구성된 타이머 트리거를 사용할 수 있습니다. 그런 다음 해당 타이머 트리거 코드가 hello 메시지 toohello 큐 테스트를 작성할 수 있습니다. 이 섹션에서는 그에 대한 예를 살펴보겠습니다.

보다 자세한 내용을 보려면 Azure 함수 바인딩 사용에 대 한 참조 hello [Azure 함수 개발자 참조](functions-reference.md)합니다.

#### <a name="create-a-queue-trigger-for-testing"></a>테스트용 큐 트리거 만들기
toodemonstrate이이 방법에서는 먼저 큐 트리거 함수를 만들 tootest 라는 큐에 대 한 원하는 `queue-newusers`합니다. 이 함수는 큐 저장소에 놓은 새 사용자의 이름 및 주소 정보를 처리합니다.

> [!NOTE]
> 다른 큐 이름을 사용 하는 경우 사용 하는 hello 이름이 toohello를 준수 하는지 확인 [명명 큐 및 메타 데이터](https://msdn.microsoft.com/library/dd179349.aspx) 규칙입니다. 그렇지 않으면 오류가 발생합니다.
>
>

1. Hello에 [Azure 포털] 함수 앱에 대 한 클릭 **새 함수** > **QueueTrigger-C#**합니다.
2. Hello 큐 이름 toobe hello 큐 함수에 의해 모니터링을 입력 합니다.

        queue-newusers
3. Hello 클릭  **+**  tooselect 단추 또는 toouse 원하는 hello 저장소 계정을 만듭니다. 그런 다음 **Create**를 클릭합니다.
4. 이 포털 브라우저 창을 열고, hello 기본 큐 함수 템플릿 코드에 대 한 hello 로그 항목을 모니터링할 수 있도록 합니다.

#### <a name="create-a-timer-trigger-toodrop-a-message-in-hello-queue"></a>Hello 큐에 타이머 트리거 toodrop 메시지 만들기
1. 열기 hello [Azure 포털] 새 브라우저 창에서 tooyour 함수 응용 프로그램을 이동 합니다.
2. **새 함수** > **TimerTrigger - C#**을 클릭합니다. Cron 식 tooset 입력 얼마나 자주 hello 타이머 코드 테스트 큐 함수입니다. 그런 다음 **Create**를 클릭합니다. 30 초 마다 테스트 toorun hello을 원하는 경우에 hello 다음을 사용할 수 있습니다 [CRON 식](https://wikipedia.org/wiki/Cron#CRON_expression):

        */30 * * * * *
3. Hello 클릭 **통합** 새 타이머 트리거의 탭 합니다.
4. **출력**에서 **+ 새 출력**을 클릭합니다. 그런 다음 **큐** 및 **선택**을 클릭합니다.
5. Hello에 사용할 참고 hello 이름을 **큐 메시지 개체**합니다. Hello 타이머 함수 코드에서이 사용합니다.

        myQueue
6. Hello 메시지를 보내는 위치 hello 큐 이름을 입력 합니다.

        queue-newusers
7. Hello 클릭  **+**  단추 tooselect hello 저장소 계정 큐 트리거 hello와 이전에 사용 합니다. 그런 다음 **Save**를 클릭합니다.
8. Hello 클릭 **개발** 타이머 트리거를 탭 합니다.
9. Hello 메시지 개체 이름 앞에 표시 된 동일한 큐를 사용으로 hello C# 타이머 함수에 대 한 코드 다음 hello를 사용할 수 있습니다. 그런 다음 **Save**를 클릭합니다.

    ```cs
    using System;

    public static void Run(TimerInfo myTimer, out String myQueue, TraceWriter log)
    {
        String newUser =
        "{\"name\":\"User testing from C# timer function\",\"address\":\"XYZ\"}";

        log.Verbose($"C# Timer trigger function executed at: {DateTime.Now}");   
        log.Verbose($"{newUser}");   

        myQueue = newUser;
    }
    ```

이 시점에서 C# 타이머 함수 hello hello 예제 cron 식을 사용 하는 경우 30 초 마다 실행 합니다. hello 타이머 함수에 대 한 hello 로그는 각 실행을 보고합니다.

    2016-03-24T10:27:02  Welcome, you are now connected toolog-streaming service.
    2016-03-24T10:27:30.004 Function started (Id=04061790-974f-4043-b851-48bd4ac424d1)
    2016-03-24T10:27:30.004 C# Timer trigger function executed at: 3/24/2016 10:27:30 AM
    2016-03-24T10:27:30.004 {"name":"User testing from C# timer function","address":"XYZ"}
    2016-03-24T10:27:30.004 Function completed (Success, Id=04061790-974f-4043-b851-48bd4ac424d1)

Hello 큐 함수에 대 한 hello 브라우저 창에서 처리 되 고 각 메시지를 확인할 수 있습니다.

    2016-03-24T10:27:06  Welcome, you are now connected toolog-streaming service.
    2016-03-24T10:27:30.607 Function started (Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)
    2016-03-24T10:27:30.607 C# Queue trigger function processed: {"name":"User testing from C# timer function","address":"XYZ"}
    2016-03-24T10:27:30.607 Function completed (Success, Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)

## <a name="test-a-function-with-code"></a>코드를 사용하여 함수 테스트
외부 응용 프로그램 또는 프레임 워크 tootest toocreate 함수 할 수 있습니다.

### <a name="test-an-http-trigger-function-with-code-nodejs"></a>코드를 사용하여 HTTP 트리거 함수 테스트: Node.js
Node.js 앱 tooexecute HTTP 요청 tootest 함수를 사용할 수 있습니다.
Tooset 있는지 확인 하십시오.

* hello `host` hello 요청 옵션 tooyour 기능 응용 프로그램 호스트에 있습니다.
* Hello에서 함수 이름을 `path`합니다.
* 액세스 코드 (`<your code>`) hello에 `path`합니다.

코드 예제:

```javascript
var http = require("http");

var nameQueryString = "name=Wes%20Query%20String%20Test%20From%20Node.js";

var nameBodyJSON = {
    name : "Wes testing with Node.JS code",
    address : "Dallas, T.X. 75201"
};

var bodyString = JSON.stringify(nameBodyJSON);

var options = {
  host: "functions841def78.azurewebsites.net",
  //path: "/api/HttpTriggerNodeJS2?code=sc1wt62opn7k9buhrm8jpds4ikxvvj42m5ojdt0p91lz5jnhfr2c74ipoujyq26wab3wk5gkfbt9&" + nameQueryString,
  path: "/api/HttpTriggerNodeJS2?code=sc1wt62opn7k9buhrm8jpds4ikxvvj42m5ojdt0p91lz5jnhfr2c74ipoujyq26wab3wk5gkfbt9",
  method: "POST",
  headers : {
      "Content-Type":"application/json",
      "Content-Length": Buffer.byteLength(bodyString)
    }    
};

callback = function(response) {
  var str = ""
  response.on("data", function (chunk) {
    str += chunk;
  });

  response.on("end", function () {
    console.log(str);
  });
}

var req = http.request(options, callback);
console.log("*** Sending name and address in body ***");
console.log(bodyString);
req.end(bodyString);
```


출력:

    C:\Users\Wesley\testing\Node.js>node testHttpTriggerExample.js
    *** Sending name and address in body ***
    {"name" : "Wes testing with Node.JS code","address" : "Dallas, T.X. 75201"}
    Hello Wes testing with Node.JS code
    hello address you provided is Dallas, T.X. 75201

Hello 포털에서 **로그** 창, 출력 유사한 toohello 다음 hello 함수 실행에 기록 됩니다.

    2016-03-23T08:08:55  Welcome, you are now connected toolog-streaming service.
    2016-03-23T08:08:59.736 Function started (Id=607b891c-08a1-427f-910c-af64ae4f7f9c)
    2016-03-23T08:09:01.153 HTTP trigger function processed a request. RequestUri=http://functionsExample.azurewebsites.net/api/WesmcHttpTriggerNodeJS1/?code=XXXXXXXXXX==
    2016-03-23T08:09:01.153 Request Headers = {"connection":"Keep-Alive","host":"functionsExample.azurewebsites.net"}
    2016-03-23T08:09:01.153 Name not provided as query string param. Checking body...
    2016-03-23T08:09:01.153 Request Body Type = object
    2016-03-23T08:09:01.153 Request Body = [object Object]
    2016-03-23T08:09:01.153 Processing User Information...
    2016-03-23T08:09:01.215 Function completed (Success, Id=607b891c-08a1-427f-910c-af64ae4f7f9c)


### <a name="test-a-queue-trigger-function-with-code-c"></a>코드를 사용하여 큐 트리거 함수 테스트: C# #
앞서 설명한 코드 toodrop 메시지 큐에 사용 하 여 큐 트리거를 테스트할 수 있습니다. hello에 제공 된 hello C# 코드를 기반으로 하는 예제 코드를 다음 hello [Azure 큐 저장소 시작](../storage/queues/storage-dotnet-how-to-use-queues.md) 자습서입니다. 해당 링크에서 다른 언어에 대한 코드를 사용할 수도 있습니다.

tootest 콘솔 응용 프로그램에서이 코드에서 수행 해야 합니다.

* [저장소 연결 문자열 hello app.config 파일에서 구성](../storage/queues/storage-dotnet-how-to-use-queues.md)합니다.
* 전달 된 `name` 및 `address` 매개 변수 toohello 응용 프로그램으로 합니다. 예: `C:\myQueueConsoleApp\test.exe "Wes testing queues" "in a console app"`. (이 코드 수락 hello 이름 및 새 사용자의 주소를 명령줄 인수로 런타임 동안.)

C# 코드 예제:

```cs
static void Main(string[] args)
{
    string name = null;
    string address = null;
    string queueName = "queue-newusers";
    string JSON = null;

    if (args.Length > 0)
    {
        name = args[0];
    }
    if (args.Length > 1)
    {
        address = args[1];
    }

    // Retrieve storage account from connection string
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConfigurationManager.AppSettings["StorageConnectionString"]);

    // Create hello queue client
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

    // Retrieve a reference tooa queue
    CloudQueue queue = queueClient.GetQueueReference(queueName);

    // Create hello queue if it doesn't already exist
    queue.CreateIfNotExists();

    // Create a message and add it toohello queue.
    if (name != null)
    {
        if (address != null)
            JSON = String.Format("{{\"name\":\"{0}\",\"address\":\"{1}\"}}", name, address);
        else
            JSON = String.Format("{{\"name\":\"{0}\"}}", name);
    }

    Console.WriteLine("Adding message too" + queueName + "...");
    Console.WriteLine(JSON);

    CloudQueueMessage message = new CloudQueueMessage(JSON);
    queue.AddMessage(message);
}
```

Hello 큐 함수에 대 한 hello 브라우저 창에서 처리 되 고 각 메시지를 확인할 수 있습니다.

    2016-03-24T10:27:06  Welcome, you are now connected toolog-streaming service.
    2016-03-24T10:27:30.607 Function started (Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)
    2016-03-24T10:27:30.607 C# Queue trigger function processed: {"name":"Wes testing queues","address":"in a console app"}
    2016-03-24T10:27:30.607 Function completed (Success, Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)


<!-- URLs. -->

[Azure 포털]: https://portal.azure.com

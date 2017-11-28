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
# <a name="strategies-for-testing-your-code-in-azure-functions"></a><span data-ttu-id="08876-104">Azure Functions에서 코드를 테스트하기 위한 전략</span><span class="sxs-lookup"><span data-stu-id="08876-104">Strategies for testing your code in Azure Functions</span></span>

<span data-ttu-id="08876-105">이 항목 뒤 일반 hello를 사용 하는 등의 다양 한 방법으로 tootest 함수에 도달 하는 hello를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="08876-105">This topic demonstrates hello various ways tootest functions, including using hello following general approaches:</span></span>

+ <span data-ttu-id="08876-106">cURL, Postman, 웹 기반 트리거에 대한 웹 브라우저 등의 HTTP 기반 도구</span><span class="sxs-lookup"><span data-stu-id="08876-106">HTTP-based tools, such as cURL, Postman, and even a web browser for web-based triggers</span></span>
+ <span data-ttu-id="08876-107">Azure 저장소 탐색기, tootest Azure 저장소 기반 트리거</span><span class="sxs-lookup"><span data-stu-id="08876-107">Azure Storage Explorer, tootest Azure Storage-based triggers</span></span>
+ <span data-ttu-id="08876-108">Hello 함수 Azure 포털의 테스트 탭</span><span class="sxs-lookup"><span data-stu-id="08876-108">Test tab in hello Azure Functions portal</span></span>
+ <span data-ttu-id="08876-109">타이머로 트리거되는 함수</span><span class="sxs-lookup"><span data-stu-id="08876-109">Timer-triggered function</span></span>
+ <span data-ttu-id="08876-110">테스트 응용 프로그램 또는 프레임워크</span><span class="sxs-lookup"><span data-stu-id="08876-110">Testing application or framework</span></span>

<span data-ttu-id="08876-111">모든 이러한 테스트 메서드 함수를 사용할 HTTP 트리거 중 하나를 통해 입력을 허용 하는 쿼리 문자열 매개 변수 또는 hello 요청 본문.</span><span class="sxs-lookup"><span data-stu-id="08876-111">All these testing methods use an HTTP trigger function that accepts input through either a query string parameter or hello request body.</span></span> <span data-ttu-id="08876-112">Hello 첫 번째 섹션에서이 함수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="08876-112">You create this function in hello first section.</span></span>

## <a name="create-a-function-for-testing"></a><span data-ttu-id="08876-113">테스트용 함수 만들기</span><span class="sxs-lookup"><span data-stu-id="08876-113">Create a function for testing</span></span>
<span data-ttu-id="08876-114">이 자습서의 대부분의 경우 약간 수정 된 버전의 hello 함수를 만들 때 사용할 수 있는 HttpTrigger JavaScript 함수 템플릿 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="08876-114">For most of this tutorial, we use a slightly modified version of hello HttpTrigger JavaScript function template that is available when you create a function.</span></span> <span data-ttu-id="08876-115">함수를 만드는 데 도움이 필요한 경우 이 [자습서](functions-create-first-azure-function.md)를 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="08876-115">If you need help creating a function, review this [tutorial](functions-create-first-azure-function.md).</span></span> <span data-ttu-id="08876-116">Hello 선택 **HttpTrigger-JavaScript** hello에서 hello 테스트 함수를 만들 때 템플릿을 [Azure 포털]합니다.</span><span class="sxs-lookup"><span data-stu-id="08876-116">Choose hello **HttpTrigger- JavaScript** template when creating hello test function in hello [Azure portal].</span></span>

<span data-ttu-id="08876-117">hello 기본 함수 서식 파일은 기본적으로 hello 요청 본문 또는 쿼리 문자열 매개 변수에서 뒤로 hello 이름을 에코 하는 "hello world" 함수 `name=<your name>`합니다.</span><span class="sxs-lookup"><span data-stu-id="08876-117">hello default function template is basically a "hello world" function that echoes back hello name from hello request body or query string parameter, `name=<your name>`.</span></span>  <span data-ttu-id="08876-118">에 업데이트 하는 hello 코드 tooalso 사용 tooprovide hello 이름 및 주소 hello 요청 본문의 JSON 콘텐츠입니다.</span><span class="sxs-lookup"><span data-stu-id="08876-118">We'll update hello code tooalso allow you tooprovide hello name and an address as JSON content in hello request body.</span></span> <span data-ttu-id="08876-119">그런 다음 hello 함수는 사용 가능한 경우 이러한 백 toohello 클라이언트를 에코 합니다.</span><span class="sxs-lookup"><span data-stu-id="08876-119">Then hello function echoes these back toohello client when available.</span></span>   

<span data-ttu-id="08876-120">테스트를 위해 사용 하는 코드를 다음 hello로 hello 함수를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="08876-120">Update hello function with hello following code, which we will use for testing:</span></span>

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

## <a name="test-a-function-with-tools"></a><span data-ttu-id="08876-121">도구를 사용하여 함수 테스트</span><span class="sxs-lookup"><span data-stu-id="08876-121">Test a function with tools</span></span>
<span data-ttu-id="08876-122">외부 hello Azure 포털을 사용할 수 있는 tootrigger 함수를 테스트 하기 위한 다양 한 도구가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08876-122">Outside hello Azure portal, there are various tools that you can use tootrigger your functions for testing.</span></span> <span data-ttu-id="08876-123">여기에는 UI 기반 및 명령줄 도구를 모두 포함하는 HTTP 테스트 도구, Azure Storage 액세스 도구 및 간단한 웹 브라우저도 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="08876-123">These include HTTP testing tools (both UI-based and command line), Azure Storage access tools, and even a simple web browser.</span></span>

### <a name="test-with-a-browser"></a><span data-ttu-id="08876-124">브라우저를 사용하여 테스트</span><span class="sxs-lookup"><span data-stu-id="08876-124">Test with a browser</span></span>
<span data-ttu-id="08876-125">hello 웹 브라우저는 HTTP 통해 제공 하기 위한 간단한 방법을 tootrigger 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="08876-125">hello web browser is a simple way tootrigger functions via HTTP.</span></span> <span data-ttu-id="08876-126">본문 페이로드가 필요하지 않으며 쿼리 문자열 매개 변수만 사용하는 GET 요청에 대해서는 브라우저를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08876-126">You can use a browser for GET requests that do not require a body payload, and that use only query string parameters.</span></span>

<span data-ttu-id="08876-127">이전에 정의한 복사 hello tootest hello 함수 **함수 Url** hello 포털에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="08876-127">tootest hello function we defined earlier, copy hello **Function Url** from hello portal.</span></span> <span data-ttu-id="08876-128">여기에 다음 폼 hello에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08876-128">It has hello following form:</span></span>

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

<span data-ttu-id="08876-129">Hello 추가 `name` toohello 쿼리 문자열 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="08876-129">Append hello `name` parameter toohello query string.</span></span> <span data-ttu-id="08876-130">Hello에 대 한 실제 이름을 사용 하 여 `<Enter a name here>` 자리 표시자입니다.</span><span class="sxs-lookup"><span data-stu-id="08876-130">Use an actual name for hello `<Enter a name here>` placeholder.</span></span>

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>&name=<Enter a name here>

<span data-ttu-id="08876-131">응답 비슷한 toohello 다음 브라우저에 붙여넣기 hello URL을 받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="08876-131">Paste hello URL into your browser, and you should get a response similar toohello following.</span></span>

![테스트 응답이 표시된 Chrome 브라우저 탭의 스크린샷](./media/functions-test-a-function/browser-test.png)

<span data-ttu-id="08876-133">이 예제는 XML 문자열을 반환 하는 hello를 래핑하는 hello Chrome 브라우저.</span><span class="sxs-lookup"><span data-stu-id="08876-133">This example is hello Chrome browser, which wraps hello returned string in XML.</span></span> <span data-ttu-id="08876-134">다른 브라우저 hello 문자열 값만 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="08876-134">Other browsers display just hello string value.</span></span>

<span data-ttu-id="08876-135">Hello 포털에서 **로그** 창, 출력 유사한 toohello 다음 hello 함수 실행에 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="08876-135">In hello portal **Logs** window, output similar toohello following is logged in executing hello function:</span></span>

    2016-03-23T07:34:59  Welcome, you are now connected toolog-streaming service.
    2016-03-23T07:35:09.195 Function started (Id=61a8c5a9-5e44-4da0-909d-91d293f20445)
    2016-03-23T07:35:10.338 Node.js HTTP trigger function processed a request. RequestUri=https://functionsExample.azurewebsites.net/api/WesmcHttpTriggerNodeJS1?code=XXXXXXXXXX==&name=Glenn from a browser
    2016-03-23T07:35:10.338 Request Headers = {"cache-control":"max-age=0","connection":"Keep-Alive","accept":"text/html","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T07:35:10.338 Name was provided as a query string param.
    2016-03-23T07:35:10.338 Processing User Information...
    2016-03-23T07:35:10.369 Function completed (Success, Id=61a8c5a9-5e44-4da0-909d-91d293f20445)

### <a name="test-with-postman"></a><span data-ttu-id="08876-136">Postman을 사용하여 테스트</span><span class="sxs-lookup"><span data-stu-id="08876-136">Test with Postman</span></span>
<span data-ttu-id="08876-137">권장 도구 tootest hello 함수 대부분 우체부 hello Chrome 브라우저 통합 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="08876-137">hello recommended tool tootest most of your functions is Postman, which integrates with hello Chrome browser.</span></span> <span data-ttu-id="08876-138">tooinstall 우체부, 참조 [가져오기 우체부](https://www.getpostman.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="08876-138">tooinstall Postman, see [Get Postman](https://www.getpostman.com/).</span></span> <span data-ttu-id="08876-139">Postman은 다양한 특성의 HTTP 요청에 대한 제어를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="08876-139">Postman provides control over many more attributes of an HTTP request.</span></span>

> [!TIP]
> <span data-ttu-id="08876-140">와 가장 편리 하 게 hello HTTP 테스트 도구를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="08876-140">Use hello HTTP testing tool that you are most comfortable with.</span></span> <span data-ttu-id="08876-141">다음은 몇 가지 대안 tooPostman입니다.</span><span class="sxs-lookup"><span data-stu-id="08876-141">Here are some alternatives tooPostman:</span></span>  
>
> * [<span data-ttu-id="08876-142">Fiddler</span><span class="sxs-lookup"><span data-stu-id="08876-142">Fiddler</span></span>](http://www.telerik.com/fiddler)  
> * [<span data-ttu-id="08876-143">Paw</span><span class="sxs-lookup"><span data-stu-id="08876-143">Paw</span></span>](https://luckymarmot.com/paw)  
>
>

<span data-ttu-id="08876-144">우체부에는 요청 본문으로 tootest hello 함수:</span><span class="sxs-lookup"><span data-stu-id="08876-144">tootest hello function with a request body in Postman:</span></span>

1. <span data-ttu-id="08876-145">Hello에서 우체부 시작 **앱** Chrome 브라우저 창의 hello 왼쪽 위 모퉁이의 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="08876-145">Start Postman from hello **Apps** button in hello upper-left corner of a Chrome browser window.</span></span>
2. <span data-ttu-id="08876-146">**함수 Url**을 복사하여 Postman에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="08876-146">Copy your **Function Url**, and paste it into Postman.</span></span> <span data-ttu-id="08876-147">Hello 액세스 코드 쿼리 문자열 매개 변수를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="08876-147">It includes hello access code query string parameter.</span></span>
3. <span data-ttu-id="08876-148">Hello HTTP 메서드를도 변경**POST**합니다.</span><span class="sxs-lookup"><span data-stu-id="08876-148">Change hello HTTP method too**POST**.</span></span>
4. <span data-ttu-id="08876-149">클릭 **본문** > **원시**, JSON 요청 본문 비슷한 toohello 다음 추가:</span><span class="sxs-lookup"><span data-stu-id="08876-149">Click **Body** > **raw**, and add a JSON request body similar toohello following:</span></span>

    ```json
    {
        "name" : "Wes testing with Postman",
        "address" : "Seattle, WA 98101"
    }
    ```
5. <span data-ttu-id="08876-150">**보내기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="08876-150">Click **Send**.</span></span>

<span data-ttu-id="08876-151">hello 다음 이미지 예를 보여 줍니다 테스트 hello 간단한 에코 함수가이 자습서에서는 합니다.</span><span class="sxs-lookup"><span data-stu-id="08876-151">hello following image shows testing hello simple echo function example in this tutorial.</span></span>

![Postman 사용자 인터페이스의 스크린샷](./media/functions-test-a-function/postman-test.png)

<span data-ttu-id="08876-153">Hello 포털에서 **로그** 창, 출력 유사한 toohello 다음 hello 함수 실행에 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="08876-153">In hello portal **Logs** window, output similar toohello following is logged in executing hello function:</span></span>

    2016-03-23T08:04:51  Welcome, you are now connected toolog-streaming service.
    2016-03-23T08:04:57.107 Function started (Id=dc5db8b1-6f1c-4117-b5c4-f6b602d538f7)
    2016-03-23T08:04:57.763 HTTP trigger function processed a request. RequestUri=https://functions841def78.azurewebsites.net/api/WesmcHttpTriggerNodeJS1?code=XXXXXXXXXX==
    2016-03-23T08:04:57.763 Request Headers = {"cache-control":"no-cache","connection":"Keep-Alive","accept":"*/*","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T08:04:57.763 Processing user info from request body...
    2016-03-23T08:04:57.763 Processing User Information...
    2016-03-23T08:04:57.763 name = Wes testing with Postman
    2016-03-23T08:04:57.763 address = Seattle, W.A. 98101
    2016-03-23T08:04:57.795 Function completed (Success, Id=dc5db8b1-6f1c-4117-b5c4-f6b602d538f7)

### <a name="test-with-curl-from-hello-command-line"></a><span data-ttu-id="08876-154">CURL hello 명령줄에서 테스트</span><span class="sxs-lookup"><span data-stu-id="08876-154">Test with cURL from hello command line</span></span>
<span data-ttu-id="08876-155">소프트웨어를 테스트 하는 경우에 종종 아닙니다 필요한 toolook 어떤 hello 명령줄 toohelp 디버그 응용 프로그램 보다 더 이상.</span><span class="sxs-lookup"><span data-stu-id="08876-155">Often when you're testing software, it's not necessary toolook any further than hello command line toohelp debug your application.</span></span> <span data-ttu-id="08876-156">테스트 함수와 전혀 차이가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="08876-156">This is no different with testing functions.</span></span> <span data-ttu-id="08876-157">참고 hello cURL은 Linux 기반 시스템에서 기본적으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08876-157">Note that hello cURL is available by default on Linux-based systems.</span></span> <span data-ttu-id="08876-158">Windows에서는 먼저 다운로드 하 여 hello 설치 [cURL 도구](https://curl.haxx.se/)합니다.</span><span class="sxs-lookup"><span data-stu-id="08876-158">On Windows, you must first download and install hello [cURL tool](https://curl.haxx.se/).</span></span>

<span data-ttu-id="08876-159">tootest hello 함수는 앞에서 정의한, 복사 hello **함수 URL** hello 포털에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="08876-159">tootest hello function that we defined earlier, copy hello **Function URL** from hello portal.</span></span> <span data-ttu-id="08876-160">여기에 다음 폼 hello에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08876-160">It has hello following form:</span></span>

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

<span data-ttu-id="08876-161">함수를 트리거할 기준이 hello URL입니다.</span><span class="sxs-lookup"><span data-stu-id="08876-161">This is hello URL for triggering your function.</span></span> <span data-ttu-id="08876-162">이 테스트 hello 명령줄 toomake hello cURL 명령을 사용 하 여 GET (`-G` 또는 `--get`) hello 함수에 대 한 요청:</span><span class="sxs-lookup"><span data-stu-id="08876-162">Test this by using hello cURL command on hello command line toomake a GET (`-G` or `--get`) request against hello function:</span></span>

    curl -G https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

<span data-ttu-id="08876-163">이 특정 예제 데이터로 전달 될 수 있는 쿼리 문자열 매개 변수를 (`-d`) hello에 cURL 명령:</span><span class="sxs-lookup"><span data-stu-id="08876-163">This particular example requires a query string parameter, which can be passed as Data (`-d`) in hello cURL command:</span></span>

    curl -G https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code> -d name=<Enter a name here>

<span data-ttu-id="08876-164">실행된 hello 명령 및 있습니다 hello hello 함수의 출력 hello 명령줄에서 다음을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="08876-164">Run hello command, and you see hello following output of hello function on hello command line:</span></span>

![명령 프롬프트 출력의 스크린샷](./media/functions-test-a-function/curl-test.png)

<span data-ttu-id="08876-166">Hello 포털에서 **로그** 창, 출력 유사한 toohello 다음 hello 함수 실행에 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="08876-166">In hello portal **Logs** window, output similar toohello following is logged in executing hello function:</span></span>

    2016-04-05T21:55:09  Welcome, you are now connected toolog-streaming service.
    2016-04-05T21:55:30.738 Function started (Id=ae6955da-29db-401a-b706-482fcd1b8f7a)
    2016-04-05T21:55:30.738 Node.js HTTP trigger function processed a request. RequestUri=https://functionsExample.azurewebsites.net/api/HttpTriggerNodeJS1?code=XXXXXXX&name=Azure Functions
    2016-04-05T21:55:30.738 Function completed (Success, Id=ae6955da-29db-401a-b706-482fcd1b8f7a)

### <a name="test-a-blob-trigger-by-using-storage-explorer"></a><span data-ttu-id="08876-167">저장소 탐색기를 사용하여 Blob 트리거 테스트</span><span class="sxs-lookup"><span data-stu-id="08876-167">Test a blob trigger by using Storage Explorer</span></span>
<span data-ttu-id="08876-168">[Azure Storage 탐색기](http://storageexplorer.com/)를 사용하여 Blob 트리거 함수를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08876-168">You can test a blob trigger function by using [Azure Storage Explorer](http://storageexplorer.com/).</span></span>

1. <span data-ttu-id="08876-169">Hello에 [Azure 포털] 함수 앱에 대 한 C#, F # 또는 JavaScript blob 트리거 함수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="08876-169">In hello [Azure portal] for your function app, create a C#, F# or JavaScript blob trigger function.</span></span> <span data-ttu-id="08876-170">Blob 컨테이너의 hello 경로 toomonitor toohello 이름을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="08876-170">Set hello path toomonitor toohello name of your blob container.</span></span> <span data-ttu-id="08876-171">예:</span><span class="sxs-lookup"><span data-stu-id="08876-171">For example:</span></span>

        files
2. <span data-ttu-id="08876-172">Hello 클릭  **+**  tooselect 단추 또는 toouse 원하는 hello 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="08876-172">Click hello **+** button tooselect or create hello storage account you want toouse.</span></span> <span data-ttu-id="08876-173">그런 다음 **Create**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="08876-173">Then click **Create**.</span></span>
3. <span data-ttu-id="08876-174">텍스트를 다음 hello로 텍스트 파일을 만들고 저장:</span><span class="sxs-lookup"><span data-stu-id="08876-174">Create a text file with hello following text, and save it:</span></span>

        A text file for blob trigger function testing.
4. <span data-ttu-id="08876-175">실행 [Azure 저장소 탐색기](http://storageexplorer.com/), 모니터링 되 고 hello 저장소 계정에서 toohello blob 컨테이너를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="08876-175">Run [Azure Storage Explorer](http://storageexplorer.com/), and connect toohello blob container in hello storage account being monitored.</span></span>
5. <span data-ttu-id="08876-176">클릭 **업로드** tooupload hello 텍스트 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="08876-176">Click **Upload** tooupload hello text file.</span></span>

    ![저장소 탐색기의 스크린샷](./media/functions-test-a-function/azure-storage-explorer-test.png)

<span data-ttu-id="08876-178">hello 기본 blob 트리거 함수 코드 hello 로그에 hello blob의 hello 처리를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="08876-178">hello default blob trigger function code reports hello processing of hello blob in hello logs:</span></span>

    2016-03-24T11:30:10  Welcome, you are now connected toolog-streaming service.
    2016-03-24T11:30:34.472 Function started (Id=739ebc07-ff9e-4ec4-a444-e479cec2e460)
    2016-03-24T11:30:34.472 C# Blob trigger function processed: A text file for blob trigger function testing.
    2016-03-24T11:30:34.472 Function completed (Success, Id=739ebc07-ff9e-4ec4-a444-e479cec2e460)

## <a name="test-a-function-within-functions"></a><span data-ttu-id="08876-179">함수 내에서 함수 테스트</span><span class="sxs-lookup"><span data-stu-id="08876-179">Test a function within functions</span></span>
<span data-ttu-id="08876-180">hello Azure 함수 포털은 설계 된 함수를 트리거한 toolet HTTP 및 타이머를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="08876-180">hello Azure Functions portal is designed toolet you test HTTP and timer triggered functions.</span></span> <span data-ttu-id="08876-181">또한 다른 함수는 테스트할 tootrigger 함수를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08876-181">You can also create functions tootrigger other functions that you are testing.</span></span>

### <a name="test-with-hello-functions-portal-run-button"></a><span data-ttu-id="08876-182">테스트 실행 단추 포털 hello 함수</span><span class="sxs-lookup"><span data-stu-id="08876-182">Test with hello Functions portal Run button</span></span>
<span data-ttu-id="08876-183">hello 포털에서 제공 된 **실행** 단추 toodo 일부 사용할 수 있는 테스트 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="08876-183">hello portal provides a **Run** button that you can use toodo some limited testing.</span></span> <span data-ttu-id="08876-184">Hello 단추를 사용 하 여 요청 본문을 제공할 수 있지만 쿼리 문자열 매개 변수를 제공 하거나 요청 헤더를 업데이트할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="08876-184">You can provide a request body by using hello button, but you can't provide query string parameters or update request headers.</span></span>

<span data-ttu-id="08876-185">다음 JSON 문자열 비슷한 toohello hello에 추가 하 여 앞에서 만든 hello HTTP 트리거 기능 테스트 **요청 본문** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="08876-185">Test hello HTTP trigger function we created earlier by adding a JSON string similar toohello following in hello **Request body** field.</span></span> <span data-ttu-id="08876-186">Hello 클릭 **실행** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="08876-186">Then click hello **Run** button.</span></span>

```json
{
    "name" : "Wes testing Run button",
    "address" : "USA"
}
```

<span data-ttu-id="08876-187">Hello 포털에서 **로그** 창, 출력 유사한 toohello 다음 hello 함수 실행에 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="08876-187">In hello portal **Logs** window, output similar toohello following is logged in executing hello function:</span></span>

    2016-03-23T08:03:12  Welcome, you are now connected toolog-streaming service.
    2016-03-23T08:03:17.357 Function started (Id=753a01b0-45a8-4125-a030-3ad543a89409)
    2016-03-23T08:03:18.697 HTTP trigger function processed a request. RequestUri=https://functions841def78.azurewebsites.net/api/wesmchttptriggernodejs1
    2016-03-23T08:03:18.697 Request Headers = {"connection":"Keep-Alive","accept":"*/*","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T08:03:18.697 Processing user info from request body...
    2016-03-23T08:03:18.697 Processing User Information...
    2016-03-23T08:03:18.697 name = Wes testing Run button
    2016-03-23T08:03:18.697 address = USA
    2016-03-23T08:03:18.744 Function completed (Success, Id=753a01b0-45a8-4125-a030-3ad543a89409)


### <a name="test-with-a-timer-trigger"></a><span data-ttu-id="08876-188">타이머 트리거를 사용하여 테스트</span><span class="sxs-lookup"><span data-stu-id="08876-188">Test with a timer trigger</span></span>
<span data-ttu-id="08876-189">일부 함수는 앞에서 언급 한 hello 도구로 적절 하 게 테스트할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="08876-189">Some functions can't be adequately tested with hello tools mentioned previously.</span></span> <span data-ttu-id="08876-190">예를 들어 [Azure 큐 저장소](../storage/queues/storage-dotnet-how-to-use-queues.md)에 메시지를 놓을 때 실행되는 큐 트리거 함수를 생각해 보세요.</span><span class="sxs-lookup"><span data-stu-id="08876-190">For example, consider a queue trigger function that runs when a message is dropped into [Azure Queue storage](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span> <span data-ttu-id="08876-191">항상 작성할 수 코드 toodrop 메시지 큐로 있으며 콘솔 프로젝트에서 이러한 예는이 문서의 뒷부분에 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="08876-191">You can always write code toodrop a message into your queue, and an example of this in a console project is provided later in this article.</span></span> <span data-ttu-id="08876-192">그러나 함수를 직접 테스트하는 데 사용할 수 있는 또 다른 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08876-192">However, there is another approach you can use that tests functions directly.</span></span>  

<span data-ttu-id="08876-193">큐 출력 바인딩으로 구성된 타이머 트리거를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08876-193">You can use a timer trigger configured with a queue output binding.</span></span> <span data-ttu-id="08876-194">그런 다음 해당 타이머 트리거 코드가 hello 메시지 toohello 큐 테스트를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08876-194">That timer trigger code can then write hello test messages toohello queue.</span></span> <span data-ttu-id="08876-195">이 섹션에서는 그에 대한 예를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="08876-195">This section walks through an example.</span></span>

<span data-ttu-id="08876-196">보다 자세한 내용을 보려면 Azure 함수 바인딩 사용에 대 한 참조 hello [Azure 함수 개발자 참조](functions-reference.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="08876-196">For more in-depth information on using bindings with Azure Functions, see hello [Azure Functions developer reference](functions-reference.md).</span></span>

#### <a name="create-a-queue-trigger-for-testing"></a><span data-ttu-id="08876-197">테스트용 큐 트리거 만들기</span><span class="sxs-lookup"><span data-stu-id="08876-197">Create a queue trigger for testing</span></span>
<span data-ttu-id="08876-198">toodemonstrate이이 방법에서는 먼저 큐 트리거 함수를 만들 tootest 라는 큐에 대 한 원하는 `queue-newusers`합니다.</span><span class="sxs-lookup"><span data-stu-id="08876-198">toodemonstrate this approach, we first create a queue trigger function that we want tootest for a queue named `queue-newusers`.</span></span> <span data-ttu-id="08876-199">이 함수는 큐 저장소에 놓은 새 사용자의 이름 및 주소 정보를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="08876-199">This function processes name and address information dropped into Queue storage for a new user.</span></span>

> [!NOTE]
> <span data-ttu-id="08876-200">다른 큐 이름을 사용 하는 경우 사용 하는 hello 이름이 toohello를 준수 하는지 확인 [명명 큐 및 메타 데이터](https://msdn.microsoft.com/library/dd179349.aspx) 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="08876-200">If you use a different queue name, make sure hello name you use conforms toohello [Naming Queues and MetaData](https://msdn.microsoft.com/library/dd179349.aspx) rules.</span></span> <span data-ttu-id="08876-201">그렇지 않으면 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="08876-201">Otherwise, you get an error.</span></span>
>
>

1. <span data-ttu-id="08876-202">Hello에 [Azure 포털] 함수 앱에 대 한 클릭 **새 함수** > **QueueTrigger-C#**합니다.</span><span class="sxs-lookup"><span data-stu-id="08876-202">In hello [Azure portal] for your function app, click **New Function** > **QueueTrigger - C#**.</span></span>
2. <span data-ttu-id="08876-203">Hello 큐 이름 toobe hello 큐 함수에 의해 모니터링을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="08876-203">Enter hello queue name toobe monitored by hello queue function:</span></span>

        queue-newusers
3. <span data-ttu-id="08876-204">Hello 클릭  **+**  tooselect 단추 또는 toouse 원하는 hello 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="08876-204">Click hello **+** button tooselect or create hello storage account you want toouse.</span></span> <span data-ttu-id="08876-205">그런 다음 **Create**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="08876-205">Then click **Create**.</span></span>
4. <span data-ttu-id="08876-206">이 포털 브라우저 창을 열고, hello 기본 큐 함수 템플릿 코드에 대 한 hello 로그 항목을 모니터링할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="08876-206">Leave this portal browser window open, so you can monitor hello log entries for hello default queue function template code.</span></span>

#### <a name="create-a-timer-trigger-toodrop-a-message-in-hello-queue"></a><span data-ttu-id="08876-207">Hello 큐에 타이머 트리거 toodrop 메시지 만들기</span><span class="sxs-lookup"><span data-stu-id="08876-207">Create a timer trigger toodrop a message in hello queue</span></span>
1. <span data-ttu-id="08876-208">열기 hello [Azure 포털] 새 브라우저 창에서 tooyour 함수 응용 프로그램을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="08876-208">Open hello [Azure portal] in a new browser window, and navigate tooyour function app.</span></span>
2. <span data-ttu-id="08876-209">**새 함수** > **TimerTrigger - C#**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="08876-209">Click **New Function** > **TimerTrigger - C#**.</span></span> <span data-ttu-id="08876-210">Cron 식 tooset 입력 얼마나 자주 hello 타이머 코드 테스트 큐 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="08876-210">Enter a cron expression tooset how often hello timer code tests your queue function.</span></span> <span data-ttu-id="08876-211">그런 다음 **Create**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="08876-211">Then click **Create**.</span></span> <span data-ttu-id="08876-212">30 초 마다 테스트 toorun hello을 원하는 경우에 hello 다음을 사용할 수 있습니다 [CRON 식](https://wikipedia.org/wiki/Cron#CRON_expression):</span><span class="sxs-lookup"><span data-stu-id="08876-212">If you want hello test toorun every 30 seconds, you can use hello following [CRON expression](https://wikipedia.org/wiki/Cron#CRON_expression):</span></span>

        */30 * * * * *
3. <span data-ttu-id="08876-213">Hello 클릭 **통합** 새 타이머 트리거의 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="08876-213">Click hello **Integrate** tab for your new timer trigger.</span></span>
4. <span data-ttu-id="08876-214">**출력**에서 **+ 새 출력**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="08876-214">Under **Output**, click **+ New Output**.</span></span> <span data-ttu-id="08876-215">그런 다음 **큐** 및 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="08876-215">Then click **queue** and **Select**.</span></span>
5. <span data-ttu-id="08876-216">Hello에 사용할 참고 hello 이름을 **큐 메시지 개체**합니다.</span><span class="sxs-lookup"><span data-stu-id="08876-216">Note hello name you use for hello **queue message object**.</span></span> <span data-ttu-id="08876-217">Hello 타이머 함수 코드에서이 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="08876-217">You use this in hello timer function code.</span></span>

        myQueue
6. <span data-ttu-id="08876-218">Hello 메시지를 보내는 위치 hello 큐 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="08876-218">Enter hello queue name where hello message is sent:</span></span>

        queue-newusers
7. <span data-ttu-id="08876-219">Hello 클릭  **+**  단추 tooselect hello 저장소 계정 큐 트리거 hello와 이전에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="08876-219">Click hello **+** button tooselect hello storage account you used previously with hello queue trigger.</span></span> <span data-ttu-id="08876-220">그런 다음 **Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="08876-220">Then click **Save**.</span></span>
8. <span data-ttu-id="08876-221">Hello 클릭 **개발** 타이머 트리거를 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="08876-221">Click hello **Develop** tab for your timer trigger.</span></span>
9. <span data-ttu-id="08876-222">Hello 메시지 개체 이름 앞에 표시 된 동일한 큐를 사용으로 hello C# 타이머 함수에 대 한 코드 다음 hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08876-222">You can use hello following code for hello C# timer function, as long as you used hello same queue message object name shown earlier.</span></span> <span data-ttu-id="08876-223">그런 다음 **Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="08876-223">Then click **Save**.</span></span>

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

<span data-ttu-id="08876-224">이 시점에서 C# 타이머 함수 hello hello 예제 cron 식을 사용 하는 경우 30 초 마다 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="08876-224">At this point, hello C# timer function executes every 30 seconds if you used hello example cron expression.</span></span> <span data-ttu-id="08876-225">hello 타이머 함수에 대 한 hello 로그는 각 실행을 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="08876-225">hello logs for hello timer function report each execution:</span></span>

    2016-03-24T10:27:02  Welcome, you are now connected toolog-streaming service.
    2016-03-24T10:27:30.004 Function started (Id=04061790-974f-4043-b851-48bd4ac424d1)
    2016-03-24T10:27:30.004 C# Timer trigger function executed at: 3/24/2016 10:27:30 AM
    2016-03-24T10:27:30.004 {"name":"User testing from C# timer function","address":"XYZ"}
    2016-03-24T10:27:30.004 Function completed (Success, Id=04061790-974f-4043-b851-48bd4ac424d1)

<span data-ttu-id="08876-226">Hello 큐 함수에 대 한 hello 브라우저 창에서 처리 되 고 각 메시지를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08876-226">In hello browser window for hello queue function, you can see each message being processed:</span></span>

    2016-03-24T10:27:06  Welcome, you are now connected toolog-streaming service.
    2016-03-24T10:27:30.607 Function started (Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)
    2016-03-24T10:27:30.607 C# Queue trigger function processed: {"name":"User testing from C# timer function","address":"XYZ"}
    2016-03-24T10:27:30.607 Function completed (Success, Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)

## <a name="test-a-function-with-code"></a><span data-ttu-id="08876-227">코드를 사용하여 함수 테스트</span><span class="sxs-lookup"><span data-stu-id="08876-227">Test a function with code</span></span>
<span data-ttu-id="08876-228">외부 응용 프로그램 또는 프레임 워크 tootest toocreate 함수 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08876-228">You may need toocreate an external application or framework tootest your functions.</span></span>

### <a name="test-an-http-trigger-function-with-code-nodejs"></a><span data-ttu-id="08876-229">코드를 사용하여 HTTP 트리거 함수 테스트: Node.js</span><span class="sxs-lookup"><span data-stu-id="08876-229">Test an HTTP trigger function with code: Node.js</span></span>
<span data-ttu-id="08876-230">Node.js 앱 tooexecute HTTP 요청 tootest 함수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08876-230">You can use a Node.js app tooexecute an HTTP request tootest your function.</span></span>
<span data-ttu-id="08876-231">Tooset 있는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="08876-231">Make sure tooset:</span></span>

* <span data-ttu-id="08876-232">hello `host` hello 요청 옵션 tooyour 기능 응용 프로그램 호스트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08876-232">hello `host` in hello request options tooyour function app host.</span></span>
* <span data-ttu-id="08876-233">Hello에서 함수 이름을 `path`합니다.</span><span class="sxs-lookup"><span data-stu-id="08876-233">Your function name in hello `path`.</span></span>
* <span data-ttu-id="08876-234">액세스 코드 (`<your code>`) hello에 `path`합니다.</span><span class="sxs-lookup"><span data-stu-id="08876-234">Your access code (`<your code>`) in hello `path`.</span></span>

<span data-ttu-id="08876-235">코드 예제:</span><span class="sxs-lookup"><span data-stu-id="08876-235">Code example:</span></span>

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


<span data-ttu-id="08876-236">출력:</span><span class="sxs-lookup"><span data-stu-id="08876-236">Output:</span></span>

    C:\Users\Wesley\testing\Node.js>node testHttpTriggerExample.js
    *** Sending name and address in body ***
    {"name" : "Wes testing with Node.JS code","address" : "Dallas, T.X. 75201"}
    Hello Wes testing with Node.JS code
    hello address you provided is Dallas, T.X. 75201

<span data-ttu-id="08876-237">Hello 포털에서 **로그** 창, 출력 유사한 toohello 다음 hello 함수 실행에 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="08876-237">In hello portal **Logs** window, output similar toohello following is logged in executing hello function:</span></span>

    2016-03-23T08:08:55  Welcome, you are now connected toolog-streaming service.
    2016-03-23T08:08:59.736 Function started (Id=607b891c-08a1-427f-910c-af64ae4f7f9c)
    2016-03-23T08:09:01.153 HTTP trigger function processed a request. RequestUri=http://functionsExample.azurewebsites.net/api/WesmcHttpTriggerNodeJS1/?code=XXXXXXXXXX==
    2016-03-23T08:09:01.153 Request Headers = {"connection":"Keep-Alive","host":"functionsExample.azurewebsites.net"}
    2016-03-23T08:09:01.153 Name not provided as query string param. Checking body...
    2016-03-23T08:09:01.153 Request Body Type = object
    2016-03-23T08:09:01.153 Request Body = [object Object]
    2016-03-23T08:09:01.153 Processing User Information...
    2016-03-23T08:09:01.215 Function completed (Success, Id=607b891c-08a1-427f-910c-af64ae4f7f9c)


### <a name="test-a-queue-trigger-function-with-code-c"></a><span data-ttu-id="08876-238">코드를 사용하여 큐 트리거 함수 테스트: C#</span><span class="sxs-lookup"><span data-stu-id="08876-238">Test a queue trigger function with code: C#</span></span> #
<span data-ttu-id="08876-239">앞서 설명한 코드 toodrop 메시지 큐에 사용 하 여 큐 트리거를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08876-239">We mentioned earlier that you can test a queue trigger by using code toodrop a message in your queue.</span></span> <span data-ttu-id="08876-240">hello에 제공 된 hello C# 코드를 기반으로 하는 예제 코드를 다음 hello [Azure 큐 저장소 시작](../storage/queues/storage-dotnet-how-to-use-queues.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="08876-240">hello following example code is based on hello C# code presented in hello [Getting started with Azure Queue storage](../storage/queues/storage-dotnet-how-to-use-queues.md) tutorial.</span></span> <span data-ttu-id="08876-241">해당 링크에서 다른 언어에 대한 코드를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08876-241">Code for other languages is also available from that link.</span></span>

<span data-ttu-id="08876-242">tootest 콘솔 응용 프로그램에서이 코드에서 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="08876-242">tootest this code in a console app, you must:</span></span>

* <span data-ttu-id="08876-243">[저장소 연결 문자열 hello app.config 파일에서 구성](../storage/queues/storage-dotnet-how-to-use-queues.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="08876-243">[Configure your storage connection string in hello app.config file](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span>
* <span data-ttu-id="08876-244">전달 된 `name` 및 `address` 매개 변수 toohello 응용 프로그램으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="08876-244">Pass a `name` and `address` as parameters toohello app.</span></span> <span data-ttu-id="08876-245">예: `C:\myQueueConsoleApp\test.exe "Wes testing queues" "in a console app"`.</span><span class="sxs-lookup"><span data-stu-id="08876-245">For example, `C:\myQueueConsoleApp\test.exe "Wes testing queues" "in a console app"`.</span></span> <span data-ttu-id="08876-246">(이 코드 수락 hello 이름 및 새 사용자의 주소를 명령줄 인수로 런타임 동안.)</span><span class="sxs-lookup"><span data-stu-id="08876-246">(This code accepts hello name and address for a new user as command-line arguments during runtime.)</span></span>

<span data-ttu-id="08876-247">C# 코드 예제:</span><span class="sxs-lookup"><span data-stu-id="08876-247">Example C# code:</span></span>

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

<span data-ttu-id="08876-248">Hello 큐 함수에 대 한 hello 브라우저 창에서 처리 되 고 각 메시지를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08876-248">In hello browser window for hello queue function, you can see each message being processed:</span></span>

    2016-03-24T10:27:06  Welcome, you are now connected toolog-streaming service.
    2016-03-24T10:27:30.607 Function started (Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)
    2016-03-24T10:27:30.607 C# Queue trigger function processed: {"name":"Wes testing queues","address":"in a console app"}
    2016-03-24T10:27:30.607 Function completed (Success, Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)


<!-- URLs. -->

[Azure 포털]: https://portal.azure.com

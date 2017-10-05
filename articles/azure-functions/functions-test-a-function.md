---
title: "Azure Functions 테스트 | Microsoft Docs"
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
ms.openlocfilehash: aca03ba4137893157fcbe6650336782ab88cd234
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="strategies-for-testing-your-code-in-azure-functions"></a><span data-ttu-id="37b41-104">Azure Functions에서 코드를 테스트하기 위한 전략</span><span class="sxs-lookup"><span data-stu-id="37b41-104">Strategies for testing your code in Azure Functions</span></span>

<span data-ttu-id="37b41-105">이 토픽에서는 다음과 같은 일반적인 방법을 사용하여 함수를 테스트하는 다양한 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-105">This topic demonstrates the various ways to test functions, including using the following general approaches:</span></span>

+ <span data-ttu-id="37b41-106">cURL, Postman, 웹 기반 트리거에 대한 웹 브라우저 등의 HTTP 기반 도구</span><span class="sxs-lookup"><span data-stu-id="37b41-106">HTTP-based tools, such as cURL, Postman, and even a web browser for web-based triggers</span></span>
+ <span data-ttu-id="37b41-107">Azure Storage 기반 트리거를 테스트하기 위한 Azure Storage 탐색기</span><span class="sxs-lookup"><span data-stu-id="37b41-107">Azure Storage Explorer, to test Azure Storage-based triggers</span></span>
+ <span data-ttu-id="37b41-108">Azure Functions 포털의 테스트 탭</span><span class="sxs-lookup"><span data-stu-id="37b41-108">Test tab in the Azure Functions portal</span></span>
+ <span data-ttu-id="37b41-109">타이머로 트리거되는 함수</span><span class="sxs-lookup"><span data-stu-id="37b41-109">Timer-triggered function</span></span>
+ <span data-ttu-id="37b41-110">테스트 응용 프로그램 또는 프레임워크</span><span class="sxs-lookup"><span data-stu-id="37b41-110">Testing application or framework</span></span>

<span data-ttu-id="37b41-111">이 모든 테스트 방법은 쿼리 문자열 매개 변수 또는 요청 본문을 통해 입력을 허용하는 HTTP 트리거 함수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-111">All these testing methods use an HTTP trigger function that accepts input through either a query string parameter or the request body.</span></span> <span data-ttu-id="37b41-112">첫 번째 섹션에서는 이 함수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-112">You create this function in the first section.</span></span>

## <a name="create-a-function-for-testing"></a><span data-ttu-id="37b41-113">테스트용 함수 만들기</span><span class="sxs-lookup"><span data-stu-id="37b41-113">Create a function for testing</span></span>
<span data-ttu-id="37b41-114">이 자습서의 대부분에서는 함수를 만들 때 제공되는 HttpTrigger JavaScript 함수 템플릿의 약간 수정된 버전을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-114">For most of this tutorial, we use a slightly modified version of the HttpTrigger JavaScript function template that is available when you create a function.</span></span> <span data-ttu-id="37b41-115">함수를 만드는 데 도움이 필요한 경우 이 [자습서](functions-create-first-azure-function.md)를 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="37b41-115">If you need help creating a function, review this [tutorial](functions-create-first-azure-function.md).</span></span> <span data-ttu-id="37b41-116">[Azure Portal]에서 테스트 함수를 만들 때에는 **HttpTrigger- JavaScript** 템플릿을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-116">Choose the **HttpTrigger- JavaScript** template when creating the test function in the [Azure portal].</span></span>

<span data-ttu-id="37b41-117">기본 함수 템플릿은 기본적으로 요청 본문 또는 쿼리 문자열 매개 변수의 이름(`name=<your name>`)을 되돌려 주는 hello world 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-117">The default function template is basically a "hello world" function that echoes back the name from the request body or query string parameter, `name=<your name>`.</span></span>  <span data-ttu-id="37b41-118">요청 본문의 JSON 콘텐츠로 이름 및 주소를 입력할 수 있도록 코드를 업데이트할 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-118">We'll update the code to also allow you to provide the name and an address as JSON content in the request body.</span></span> <span data-ttu-id="37b41-119">그렇게 되면 함수는 사용 가능한 경우 이를 다시 클라이언트에 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-119">Then the function echoes these back to the client when available.</span></span>   

<span data-ttu-id="37b41-120">함수를 테스트에 사용할 다음 코드로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-120">Update the function with the following code, which we will use for testing:</span></span>

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
            body: "Please pass a name on the query string or in the request body"
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
        echoString += "\n" + "The address you provided is " + address;
        context.log("address = " + address);
    }
    res = {
        // status: 200, /* Defaults to 200 */
        body: echoString
    };
    return res;
}
```

## <a name="test-a-function-with-tools"></a><span data-ttu-id="37b41-121">도구를 사용하여 함수 테스트</span><span class="sxs-lookup"><span data-stu-id="37b41-121">Test a function with tools</span></span>
<span data-ttu-id="37b41-122">Azure Portal 외부에는 테스트용 함수를 트리거하는 데 사용할 수 있는 다양한 도구가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-122">Outside the Azure portal, there are various tools that you can use to trigger your functions for testing.</span></span> <span data-ttu-id="37b41-123">여기에는 UI 기반 및 명령줄 도구를 모두 포함하는 HTTP 테스트 도구, Azure Storage 액세스 도구 및 간단한 웹 브라우저도 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-123">These include HTTP testing tools (both UI-based and command line), Azure Storage access tools, and even a simple web browser.</span></span>

### <a name="test-with-a-browser"></a><span data-ttu-id="37b41-124">브라우저를 사용하여 테스트</span><span class="sxs-lookup"><span data-stu-id="37b41-124">Test with a browser</span></span>
<span data-ttu-id="37b41-125">웹 브라우저는 HTTP 통해 함수를 트리거하는 간단한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-125">The web browser is a simple way to trigger functions via HTTP.</span></span> <span data-ttu-id="37b41-126">본문 페이로드가 필요하지 않으며 쿼리 문자열 매개 변수만 사용하는 GET 요청에 대해서는 브라우저를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-126">You can use a browser for GET requests that do not require a body payload, and that use only query string parameters.</span></span>

<span data-ttu-id="37b41-127">위에서 정의한 함수를 테스트하려면 포털에서 **함수 Url**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-127">To test the function we defined earlier, copy the **Function Url** from the portal.</span></span> <span data-ttu-id="37b41-128">다음과 같은 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-128">It has the following form:</span></span>

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

<span data-ttu-id="37b41-129">쿼리 문자열에 `name` 매개 변수를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-129">Append the `name` parameter to the query string.</span></span> <span data-ttu-id="37b41-130">`<Enter a name here>` 자리 표시자의 실제 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-130">Use an actual name for the `<Enter a name here>` placeholder.</span></span>

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>&name=<Enter a name here>

<span data-ttu-id="37b41-131">브라우저에 URL을 붙여 넣으면 다음과 유사한 응답을 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-131">Paste the URL into your browser, and you should get a response similar to the following.</span></span>

![테스트 응답이 표시된 Chrome 브라우저 탭의 스크린샷](./media/functions-test-a-function/browser-test.png)

<span data-ttu-id="37b41-133">이 예제는 반환되는 문자열을 XML에 래핑하는 Chrome 브라우저입니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-133">This example is the Chrome browser, which wraps the returned string in XML.</span></span> <span data-ttu-id="37b41-134">다른 브라우저에는 문자열 값만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-134">Other browsers display just the string value.</span></span>

<span data-ttu-id="37b41-135">함수를 실행하는 동안 포털 **로그** 창에 다음과 유사한 출력이 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-135">In the portal **Logs** window, output similar to the following is logged in executing the function:</span></span>

    2016-03-23T07:34:59  Welcome, you are now connected to log-streaming service.
    2016-03-23T07:35:09.195 Function started (Id=61a8c5a9-5e44-4da0-909d-91d293f20445)
    2016-03-23T07:35:10.338 Node.js HTTP trigger function processed a request. RequestUri=https://functionsExample.azurewebsites.net/api/WesmcHttpTriggerNodeJS1?code=XXXXXXXXXX==&name=Glenn from a browser
    2016-03-23T07:35:10.338 Request Headers = {"cache-control":"max-age=0","connection":"Keep-Alive","accept":"text/html","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T07:35:10.338 Name was provided as a query string param.
    2016-03-23T07:35:10.338 Processing User Information...
    2016-03-23T07:35:10.369 Function completed (Success, Id=61a8c5a9-5e44-4da0-909d-91d293f20445)

### <a name="test-with-postman"></a><span data-ttu-id="37b41-136">Postman을 사용하여 테스트</span><span class="sxs-lookup"><span data-stu-id="37b41-136">Test with Postman</span></span>
<span data-ttu-id="37b41-137">대부분의 함수를 테스트하는 데 권장되는 도구는 Chrome 브라우저에 통합되는 Postman입니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-137">The recommended tool to test most of your functions is Postman, which integrates with the Chrome browser.</span></span> <span data-ttu-id="37b41-138">Postman을 설치하려면 [Postman 가져오기](https://www.getpostman.com/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="37b41-138">To install Postman, see [Get Postman](https://www.getpostman.com/).</span></span> <span data-ttu-id="37b41-139">Postman은 다양한 특성의 HTTP 요청에 대한 제어를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-139">Postman provides control over many more attributes of an HTTP request.</span></span>

> [!TIP]
> <span data-ttu-id="37b41-140">가장 익숙한 HTTP 테스트 도구를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="37b41-140">Use the HTTP testing tool that you are most comfortable with.</span></span> <span data-ttu-id="37b41-141">다음은 Postman의 몇 가지 대안입니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-141">Here are some alternatives to Postman:</span></span>  
>
> * [<span data-ttu-id="37b41-142">Fiddler</span><span class="sxs-lookup"><span data-stu-id="37b41-142">Fiddler</span></span>](http://www.telerik.com/fiddler)  
> * [<span data-ttu-id="37b41-143">Paw</span><span class="sxs-lookup"><span data-stu-id="37b41-143">Paw</span></span>](https://luckymarmot.com/paw)  
>
>

<span data-ttu-id="37b41-144">Postman에서 요청 본문을 사용하여 함수를 테스트하려면</span><span class="sxs-lookup"><span data-stu-id="37b41-144">To test the function with a request body in Postman:</span></span>

1. <span data-ttu-id="37b41-145">Chrome 브라우저 창의 왼쪽 위에 있는 **앱** 단추에서 Postman을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-145">Start Postman from the **Apps** button in the upper-left corner of a Chrome browser window.</span></span>
2. <span data-ttu-id="37b41-146">**함수 Url**을 복사하여 Postman에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-146">Copy your **Function Url**, and paste it into Postman.</span></span> <span data-ttu-id="37b41-147">액세스 코드 쿼리 문자열 매개 변수를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-147">It includes the access code query string parameter.</span></span>
3. <span data-ttu-id="37b41-148">HTTP 메서드를 **POST**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-148">Change the HTTP method to **POST**.</span></span>
4. <span data-ttu-id="37b41-149">**본문** > **원시**를 클릭하고, 다음과 유사한 JSON 요청 본문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-149">Click **Body** > **raw**, and add a JSON request body similar to the following:</span></span>

    ```json
    {
        "name" : "Wes testing with Postman",
        "address" : "Seattle, WA 98101"
    }
    ```
5. <span data-ttu-id="37b41-150">**보내기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-150">Click **Send**.</span></span>

<span data-ttu-id="37b41-151">다음 이미지는 이 자습서의 간단한 에코 함수 예제 테스트를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-151">The following image shows testing the simple echo function example in this tutorial.</span></span>

![Postman 사용자 인터페이스의 스크린샷](./media/functions-test-a-function/postman-test.png)

<span data-ttu-id="37b41-153">함수를 실행하는 동안 포털 **로그** 창에 다음과 유사한 출력이 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-153">In the portal **Logs** window, output similar to the following is logged in executing the function:</span></span>

    2016-03-23T08:04:51  Welcome, you are now connected to log-streaming service.
    2016-03-23T08:04:57.107 Function started (Id=dc5db8b1-6f1c-4117-b5c4-f6b602d538f7)
    2016-03-23T08:04:57.763 HTTP trigger function processed a request. RequestUri=https://functions841def78.azurewebsites.net/api/WesmcHttpTriggerNodeJS1?code=XXXXXXXXXX==
    2016-03-23T08:04:57.763 Request Headers = {"cache-control":"no-cache","connection":"Keep-Alive","accept":"*/*","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T08:04:57.763 Processing user info from request body...
    2016-03-23T08:04:57.763 Processing User Information...
    2016-03-23T08:04:57.763 name = Wes testing with Postman
    2016-03-23T08:04:57.763 address = Seattle, W.A. 98101
    2016-03-23T08:04:57.795 Function completed (Success, Id=dc5db8b1-6f1c-4117-b5c4-f6b602d538f7)

### <a name="test-with-curl-from-the-command-line"></a><span data-ttu-id="37b41-154">명령줄에서 cURL을 사용하여 테스트</span><span class="sxs-lookup"><span data-stu-id="37b41-154">Test with cURL from the command line</span></span>
<span data-ttu-id="37b41-155">소프트웨어를 테스트할 때 명령줄만 살펴보아도 응용 프로그램을 디버그하는 데 전혀 문제가 없는 경우가 종종 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-155">Often when you're testing software, it's not necessary to look any further than the command line to help debug your application.</span></span> <span data-ttu-id="37b41-156">테스트 함수와 전혀 차이가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-156">This is no different with testing functions.</span></span> <span data-ttu-id="37b41-157">cURL은 Linux 기반 시스템에서 기본적으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-157">Note that the cURL is available by default on Linux-based systems.</span></span> <span data-ttu-id="37b41-158">Windows에서는 먼저 [cURL 도구](https://curl.haxx.se/)를 다운로드한 후 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-158">On Windows, you must first download and install the [cURL tool](https://curl.haxx.se/).</span></span>

<span data-ttu-id="37b41-159">위에서 정의한 함수를 테스트하려면 포털에서 **함수 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-159">To test the function that we defined earlier, copy the **Function URL** from the portal.</span></span> <span data-ttu-id="37b41-160">다음과 같은 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-160">It has the following form:</span></span>

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

<span data-ttu-id="37b41-161">함수를 트리거하는 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-161">This is the URL for triggering your function.</span></span> <span data-ttu-id="37b41-162">명령줄에서 cURL 명령을 사용하여 함수에 대한 GET(`-G` 또는 `--get`) 요청을 만들어서 테스트를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-162">Test this by using the cURL command on the command line to make a GET (`-G` or `--get`) request against the function:</span></span>

    curl -G https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

<span data-ttu-id="37b41-163">이 예제에서는 cURL 명령에서 데이터(`-d`)로 전달할 수 있는 쿼리 문자열 매개 변수가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-163">This particular example requires a query string parameter, which can be passed as Data (`-d`) in the cURL command:</span></span>

    curl -G https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code> -d name=<Enter a name here>

<span data-ttu-id="37b41-164">명령을 실행하면 명령줄에 다음과 같은 함수 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-164">Run the command, and you see the following output of the function on the command line:</span></span>

![명령 프롬프트 출력의 스크린샷](./media/functions-test-a-function/curl-test.png)

<span data-ttu-id="37b41-166">함수를 실행하는 동안 포털 **로그** 창에 다음과 유사한 출력이 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-166">In the portal **Logs** window, output similar to the following is logged in executing the function:</span></span>

    2016-04-05T21:55:09  Welcome, you are now connected to log-streaming service.
    2016-04-05T21:55:30.738 Function started (Id=ae6955da-29db-401a-b706-482fcd1b8f7a)
    2016-04-05T21:55:30.738 Node.js HTTP trigger function processed a request. RequestUri=https://functionsExample.azurewebsites.net/api/HttpTriggerNodeJS1?code=XXXXXXX&name=Azure Functions
    2016-04-05T21:55:30.738 Function completed (Success, Id=ae6955da-29db-401a-b706-482fcd1b8f7a)

### <a name="test-a-blob-trigger-by-using-storage-explorer"></a><span data-ttu-id="37b41-167">저장소 탐색기를 사용하여 Blob 트리거 테스트</span><span class="sxs-lookup"><span data-stu-id="37b41-167">Test a blob trigger by using Storage Explorer</span></span>
<span data-ttu-id="37b41-168">[Azure Storage 탐색기](http://storageexplorer.com/)를 사용하여 Blob 트리거 함수를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-168">You can test a blob trigger function by using [Azure Storage Explorer](http://storageexplorer.com/).</span></span>

1. <span data-ttu-id="37b41-169">함수 앱에 대한 [Azure Portal]에서 C#, F# 또는 JavaScript Blob 트리거 함수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-169">In the [Azure portal] for your function app, create a C#, F# or JavaScript blob trigger function.</span></span> <span data-ttu-id="37b41-170">모니터링할 경로를 Blob 컨테이너의 이름으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-170">Set the path to monitor to the name of your blob container.</span></span> <span data-ttu-id="37b41-171">예:</span><span class="sxs-lookup"><span data-stu-id="37b41-171">For example:</span></span>

        files
2. <span data-ttu-id="37b41-172">사용하려는 저장소 계정을 선택하거나 만들려면 **+** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-172">Click the **+** button to select or create the storage account you want to use.</span></span> <span data-ttu-id="37b41-173">그런 다음 **Create**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-173">Then click **Create**.</span></span>
3. <span data-ttu-id="37b41-174">다음 텍스트를 사용하여 텍스트 파일을 만들고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-174">Create a text file with the following text, and save it:</span></span>

        A text file for blob trigger function testing.
4. <span data-ttu-id="37b41-175">[Azure Storage 탐색기](http://storageexplorer.com/)를 실행하고 모니터링되고 있는 저장소 계정의 Blob 컨테이너에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-175">Run [Azure Storage Explorer](http://storageexplorer.com/), and connect to the blob container in the storage account being monitored.</span></span>
5. <span data-ttu-id="37b41-176">**업로드**를 클릭하여 텍스트 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-176">Click **Upload** to upload the text file.</span></span>

    ![저장소 탐색기의 스크린샷](./media/functions-test-a-function/azure-storage-explorer-test.png)

<span data-ttu-id="37b41-178">기본 Blob 트리거 함수 코드는 로그에 Blob 처리 상황을 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-178">The default blob trigger function code reports the processing of the blob in the logs:</span></span>

    2016-03-24T11:30:10  Welcome, you are now connected to log-streaming service.
    2016-03-24T11:30:34.472 Function started (Id=739ebc07-ff9e-4ec4-a444-e479cec2e460)
    2016-03-24T11:30:34.472 C# Blob trigger function processed: A text file for blob trigger function testing.
    2016-03-24T11:30:34.472 Function completed (Success, Id=739ebc07-ff9e-4ec4-a444-e479cec2e460)

## <a name="test-a-function-within-functions"></a><span data-ttu-id="37b41-179">함수 내에서 함수 테스트</span><span class="sxs-lookup"><span data-stu-id="37b41-179">Test a function within functions</span></span>
<span data-ttu-id="37b41-180">Azure Functions 포털은 HTTP 및 타이머 트리거 함수를 테스트할 수 있도록 디자인되었습니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-180">The Azure Functions portal is designed to let you test HTTP and timer triggered functions.</span></span> <span data-ttu-id="37b41-181">테스트하려는 다른 함수를 트리거하는 함수를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-181">You can also create functions to trigger other functions that you are testing.</span></span>

### <a name="test-with-the-functions-portal-run-button"></a><span data-ttu-id="37b41-182">함수 포털 실행 단추를 사용하여 테스트</span><span class="sxs-lookup"><span data-stu-id="37b41-182">Test with the Functions portal Run button</span></span>
<span data-ttu-id="37b41-183">포털에서는 몇 가지 제한된 테스트를 수행할 수 있는 **실행** 단추를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-183">The portal provides a **Run** button that you can use to do some limited testing.</span></span> <span data-ttu-id="37b41-184">이 단추를 사용하여 요청 본문을 제공할 수 있지만 쿼리 문자열 매개 변수를 제공하거나 요청 헤더를 업데이트할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-184">You can provide a request body by using the button, but you can't provide query string parameters or update request headers.</span></span>

<span data-ttu-id="37b41-185">**요청 본문** 필드에 다음과 유사한 JSON 문자열을 추가하여 앞에서 만든 HTTP 트리거 함수를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-185">Test the HTTP trigger function we created earlier by adding a JSON string similar to the following in the **Request body** field.</span></span> <span data-ttu-id="37b41-186">그런 다음 **실행** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-186">Then click the **Run** button.</span></span>

```json
{
    "name" : "Wes testing Run button",
    "address" : "USA"
}
```

<span data-ttu-id="37b41-187">함수를 실행하는 동안 포털 **로그** 창에 다음과 유사한 출력이 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-187">In the portal **Logs** window, output similar to the following is logged in executing the function:</span></span>

    2016-03-23T08:03:12  Welcome, you are now connected to log-streaming service.
    2016-03-23T08:03:17.357 Function started (Id=753a01b0-45a8-4125-a030-3ad543a89409)
    2016-03-23T08:03:18.697 HTTP trigger function processed a request. RequestUri=https://functions841def78.azurewebsites.net/api/wesmchttptriggernodejs1
    2016-03-23T08:03:18.697 Request Headers = {"connection":"Keep-Alive","accept":"*/*","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T08:03:18.697 Processing user info from request body...
    2016-03-23T08:03:18.697 Processing User Information...
    2016-03-23T08:03:18.697 name = Wes testing Run button
    2016-03-23T08:03:18.697 address = USA
    2016-03-23T08:03:18.744 Function completed (Success, Id=753a01b0-45a8-4125-a030-3ad543a89409)


### <a name="test-with-a-timer-trigger"></a><span data-ttu-id="37b41-188">타이머 트리거를 사용하여 테스트</span><span class="sxs-lookup"><span data-stu-id="37b41-188">Test with a timer trigger</span></span>
<span data-ttu-id="37b41-189">일부 함수는 앞에서 언급한 도구를 사용하여 제대로 테스트할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-189">Some functions can't be adequately tested with the tools mentioned previously.</span></span> <span data-ttu-id="37b41-190">예를 들어 [Azure 큐 저장소](../storage/queues/storage-dotnet-how-to-use-queues.md)에 메시지를 놓을 때 실행되는 큐 트리거 함수를 생각해 보세요.</span><span class="sxs-lookup"><span data-stu-id="37b41-190">For example, consider a queue trigger function that runs when a message is dropped into [Azure Queue storage](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span> <span data-ttu-id="37b41-191">언제든지 큐에 메시지를 놓는 코드를 작성할 수 있으며, 콘솔 프로젝트의 이러한 예는 이 문서의 후반부에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-191">You can always write code to drop a message into your queue, and an example of this in a console project is provided later in this article.</span></span> <span data-ttu-id="37b41-192">그러나 함수를 직접 테스트하는 데 사용할 수 있는 또 다른 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-192">However, there is another approach you can use that tests functions directly.</span></span>  

<span data-ttu-id="37b41-193">큐 출력 바인딩으로 구성된 타이머 트리거를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-193">You can use a timer trigger configured with a queue output binding.</span></span> <span data-ttu-id="37b41-194">이 타이머 트리거 코드는 큐에 테스트 메시지를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-194">That timer trigger code can then write the test messages to the queue.</span></span> <span data-ttu-id="37b41-195">이 섹션에서는 그에 대한 예를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-195">This section walks through an example.</span></span>

<span data-ttu-id="37b41-196">Azure Functions 바인딩 사용에 대한 자세한 내용은 [Azure Functions 개발자 참조](functions-reference.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="37b41-196">For more in-depth information on using bindings with Azure Functions, see the [Azure Functions developer reference](functions-reference.md).</span></span>

#### <a name="create-a-queue-trigger-for-testing"></a><span data-ttu-id="37b41-197">테스트용 큐 트리거 만들기</span><span class="sxs-lookup"><span data-stu-id="37b41-197">Create a queue trigger for testing</span></span>
<span data-ttu-id="37b41-198">이 방법을 시연하기 위해 먼저 `queue-newusers`라는 큐를 테스트하려는 큐 트리거 함수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-198">To demonstrate this approach, we first create a queue trigger function that we want to test for a queue named `queue-newusers`.</span></span> <span data-ttu-id="37b41-199">이 함수는 큐 저장소에 놓은 새 사용자의 이름 및 주소 정보를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-199">This function processes name and address information dropped into Queue storage for a new user.</span></span>

> [!NOTE]
> <span data-ttu-id="37b41-200">다른 큐 이름을 사용하는 경우 해당 이름이 [큐 및 메타데이터 명명](https://msdn.microsoft.com/library/dd179349.aspx) 규칙을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-200">If you use a different queue name, make sure the name you use conforms to the [Naming Queues and MetaData](https://msdn.microsoft.com/library/dd179349.aspx) rules.</span></span> <span data-ttu-id="37b41-201">그렇지 않으면 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-201">Otherwise, you get an error.</span></span>
>
>

1. <span data-ttu-id="37b41-202">함수 앱에 대한 [Azure Portal]에서 **새 함수** > **QueueTrigger - C#**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-202">In the [Azure portal] for your function app, click **New Function** > **QueueTrigger - C#**.</span></span>
2. <span data-ttu-id="37b41-203">큐 함수가 모니터링할 큐 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-203">Enter the queue name to be monitored by the queue function:</span></span>

        queue-newusers
3. <span data-ttu-id="37b41-204">사용하려는 저장소 계정을 선택하거나 만들려면 **+** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-204">Click the **+** button to select or create the storage account you want to use.</span></span> <span data-ttu-id="37b41-205">그런 다음 **Create**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-205">Then click **Create**.</span></span>
4. <span data-ttu-id="37b41-206">기본 큐 함수 템플릿 코드에 대한 로그 항목을 모니터링할 수 있도록 포털 브라우저 창을 그대로 열어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-206">Leave this portal browser window open, so you can monitor the log entries for the default queue function template code.</span></span>

#### <a name="create-a-timer-trigger-to-drop-a-message-in-the-queue"></a><span data-ttu-id="37b41-207">큐에 메시지를 놓는 타이머 트리거 만들기</span><span class="sxs-lookup"><span data-stu-id="37b41-207">Create a timer trigger to drop a message in the queue</span></span>
1. <span data-ttu-id="37b41-208">새 브라우저 창에서 [Azure Portal]을 열고 함수 앱으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-208">Open the [Azure portal] in a new browser window, and navigate to your function app.</span></span>
2. <span data-ttu-id="37b41-209">**새 함수** > **TimerTrigger - C#**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-209">Click **New Function** > **TimerTrigger - C#**.</span></span> <span data-ttu-id="37b41-210">타이머 코드가 큐 함수 테스트할 빈도를 설정하는 cron 식을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-210">Enter a cron expression to set how often the timer code tests your queue function.</span></span> <span data-ttu-id="37b41-211">그런 다음 **Create**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-211">Then click **Create**.</span></span> <span data-ttu-id="37b41-212">테스트를 30초마다 실행하려는 경우 다음 [CRON 식](https://wikipedia.org/wiki/Cron#CRON_expression)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-212">If you want the test to run every 30 seconds, you can use the following [CRON expression](https://wikipedia.org/wiki/Cron#CRON_expression):</span></span>

        */30 * * * * *
3. <span data-ttu-id="37b41-213">새 타이머 트리거에 대한 **통합** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-213">Click the **Integrate** tab for your new timer trigger.</span></span>
4. <span data-ttu-id="37b41-214">**출력**에서 **+ 새 출력**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-214">Under **Output**, click **+ New Output**.</span></span> <span data-ttu-id="37b41-215">그런 다음 **큐** 및 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-215">Then click **queue** and **Select**.</span></span>
5. <span data-ttu-id="37b41-216">**큐 메시지 개체**에 사용한 이름을 메모해 두세요.</span><span class="sxs-lookup"><span data-stu-id="37b41-216">Note the name you use for the **queue message object**.</span></span> <span data-ttu-id="37b41-217">이 이름은 타이머 함수 코드에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-217">You use this in the timer function code.</span></span>

        myQueue
6. <span data-ttu-id="37b41-218">메시지가 전송되는 큐 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-218">Enter the queue name where the message is sent:</span></span>

        queue-newusers
7. <span data-ttu-id="37b41-219">**+** 단추를 클릭하여 이전에 큐 트리거와 함께 사용한 저장소 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-219">Click the **+** button to select the storage account you used previously with the queue trigger.</span></span> <span data-ttu-id="37b41-220">그런 다음 **Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-220">Then click **Save**.</span></span>
8. <span data-ttu-id="37b41-221">타이머 트리거에 대한 **개발** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-221">Click the **Develop** tab for your timer trigger.</span></span>
9. <span data-ttu-id="37b41-222">위에 표시된 것과 동일한 큐 메시지 개체 이름을 사용하는 한 C# 타이머 함수에 다음 코드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-222">You can use the following code for the C# timer function, as long as you used the same queue message object name shown earlier.</span></span> <span data-ttu-id="37b41-223">그런 다음 **Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-223">Then click **Save**.</span></span>

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

<span data-ttu-id="37b41-224">예제 cron 식을 사용했다면 C# 타이머 함수가 30초마다 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-224">At this point, the C# timer function executes every 30 seconds if you used the example cron expression.</span></span> <span data-ttu-id="37b41-225">타이머 함수의 로그에서 각 실행을 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-225">The logs for the timer function report each execution:</span></span>

    2016-03-24T10:27:02  Welcome, you are now connected to log-streaming service.
    2016-03-24T10:27:30.004 Function started (Id=04061790-974f-4043-b851-48bd4ac424d1)
    2016-03-24T10:27:30.004 C# Timer trigger function executed at: 3/24/2016 10:27:30 AM
    2016-03-24T10:27:30.004 {"name":"User testing from C# timer function","address":"XYZ"}
    2016-03-24T10:27:30.004 Function completed (Success, Id=04061790-974f-4043-b851-48bd4ac424d1)

<span data-ttu-id="37b41-226">큐 함수에 대한 브라우저 창에 처리 중인 각 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-226">In the browser window for the queue function, you can see each message being processed:</span></span>

    2016-03-24T10:27:06  Welcome, you are now connected to log-streaming service.
    2016-03-24T10:27:30.607 Function started (Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)
    2016-03-24T10:27:30.607 C# Queue trigger function processed: {"name":"User testing from C# timer function","address":"XYZ"}
    2016-03-24T10:27:30.607 Function completed (Success, Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)

## <a name="test-a-function-with-code"></a><span data-ttu-id="37b41-227">코드를 사용하여 함수 테스트</span><span class="sxs-lookup"><span data-stu-id="37b41-227">Test a function with code</span></span>
<span data-ttu-id="37b41-228">함수를 테스트하기 위해 외부 응용 프로그램 또는 프레임워크를 만들어야 하는 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-228">You may need to create an external application or framework to test your functions.</span></span>

### <a name="test-an-http-trigger-function-with-code-nodejs"></a><span data-ttu-id="37b41-229">코드를 사용하여 HTTP 트리거 함수 테스트: Node.js</span><span class="sxs-lookup"><span data-stu-id="37b41-229">Test an HTTP trigger function with code: Node.js</span></span>
<span data-ttu-id="37b41-230">Node.js 앱을 사용하여 함수를 테스트하기 위한 HTTP 요청을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-230">You can use a Node.js app to execute an HTTP request to test your function.</span></span>
<span data-ttu-id="37b41-231">다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-231">Make sure to set:</span></span>

* <span data-ttu-id="37b41-232">요청 옵션에서 `host`를 함수 앱 호스트로 설정</span><span class="sxs-lookup"><span data-stu-id="37b41-232">The `host` in the request options to your function app host.</span></span>
* <span data-ttu-id="37b41-233">`path`에서 함수 이름 설정</span><span class="sxs-lookup"><span data-stu-id="37b41-233">Your function name in the `path`.</span></span>
* <span data-ttu-id="37b41-234">`path`에서 액세스 코드(`<your code>`) 설정</span><span class="sxs-lookup"><span data-stu-id="37b41-234">Your access code (`<your code>`) in the `path`.</span></span>

<span data-ttu-id="37b41-235">코드 예제:</span><span class="sxs-lookup"><span data-stu-id="37b41-235">Code example:</span></span>

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


<span data-ttu-id="37b41-236">출력:</span><span class="sxs-lookup"><span data-stu-id="37b41-236">Output:</span></span>

    C:\Users\Wesley\testing\Node.js>node testHttpTriggerExample.js
    *** Sending name and address in body ***
    {"name" : "Wes testing with Node.JS code","address" : "Dallas, T.X. 75201"}
    Hello Wes testing with Node.JS code
    The address you provided is Dallas, T.X. 75201

<span data-ttu-id="37b41-237">함수를 실행하는 동안 포털 **로그** 창에 다음과 유사한 출력이 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-237">In the portal **Logs** window, output similar to the following is logged in executing the function:</span></span>

    2016-03-23T08:08:55  Welcome, you are now connected to log-streaming service.
    2016-03-23T08:08:59.736 Function started (Id=607b891c-08a1-427f-910c-af64ae4f7f9c)
    2016-03-23T08:09:01.153 HTTP trigger function processed a request. RequestUri=http://functionsExample.azurewebsites.net/api/WesmcHttpTriggerNodeJS1/?code=XXXXXXXXXX==
    2016-03-23T08:09:01.153 Request Headers = {"connection":"Keep-Alive","host":"functionsExample.azurewebsites.net"}
    2016-03-23T08:09:01.153 Name not provided as query string param. Checking body...
    2016-03-23T08:09:01.153 Request Body Type = object
    2016-03-23T08:09:01.153 Request Body = [object Object]
    2016-03-23T08:09:01.153 Processing User Information...
    2016-03-23T08:09:01.215 Function completed (Success, Id=607b891c-08a1-427f-910c-af64ae4f7f9c)


### <a name="test-a-queue-trigger-function-with-code-c"></a><span data-ttu-id="37b41-238">코드를 사용하여 큐 트리거 함수 테스트: C#</span><span class="sxs-lookup"><span data-stu-id="37b41-238">Test a queue trigger function with code: C#</span></span> #
<span data-ttu-id="37b41-239">앞에서 큐에 메시지를 놓는 코드를 사용하여 큐 트리거를 테스트하는 방법에 대해 설명했습니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-239">We mentioned earlier that you can test a queue trigger by using code to drop a message in your queue.</span></span> <span data-ttu-id="37b41-240">다음 예제 코드는 [Azure 큐 저장소 시작](../storage/queues/storage-dotnet-how-to-use-queues.md) 자습서에 제공된 C# 코드를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-240">The following example code is based on the C# code presented in the [Getting started with Azure Queue storage](../storage/queues/storage-dotnet-how-to-use-queues.md) tutorial.</span></span> <span data-ttu-id="37b41-241">해당 링크에서 다른 언어에 대한 코드를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-241">Code for other languages is also available from that link.</span></span>

<span data-ttu-id="37b41-242">콘솔 앱에서 이 코드를 테스트하려면 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-242">To test this code in a console app, you must:</span></span>

* <span data-ttu-id="37b41-243">[app.config 파일에서 저장소 연결 문자열을 구성합니다](../storage/queues/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="37b41-243">[Configure your storage connection string in the app.config file](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span>
* <span data-ttu-id="37b41-244">앱에 대한 매개 변수로 `name` 및 `address`를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-244">Pass a `name` and `address` as parameters to the app.</span></span> <span data-ttu-id="37b41-245">예: `C:\myQueueConsoleApp\test.exe "Wes testing queues" "in a console app"`.</span><span class="sxs-lookup"><span data-stu-id="37b41-245">For example, `C:\myQueueConsoleApp\test.exe "Wes testing queues" "in a console app"`.</span></span> <span data-ttu-id="37b41-246">이 코드는 런타임 동안 새 사용자에 대한 이름 및 주소를 명령줄 인수로 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-246">(This code accepts the name and address for a new user as command-line arguments during runtime.)</span></span>

<span data-ttu-id="37b41-247">C# 코드 예제:</span><span class="sxs-lookup"><span data-stu-id="37b41-247">Example C# code:</span></span>

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

    // Create the queue client
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

    // Retrieve a reference to a queue
    CloudQueue queue = queueClient.GetQueueReference(queueName);

    // Create the queue if it doesn't already exist
    queue.CreateIfNotExists();

    // Create a message and add it to the queue.
    if (name != null)
    {
        if (address != null)
            JSON = String.Format("{{\"name\":\"{0}\",\"address\":\"{1}\"}}", name, address);
        else
            JSON = String.Format("{{\"name\":\"{0}\"}}", name);
    }

    Console.WriteLine("Adding message to " + queueName + "...");
    Console.WriteLine(JSON);

    CloudQueueMessage message = new CloudQueueMessage(JSON);
    queue.AddMessage(message);
}
```

<span data-ttu-id="37b41-248">큐 함수에 대한 브라우저 창에 처리 중인 각 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="37b41-248">In the browser window for the queue function, you can see each message being processed:</span></span>

    2016-03-24T10:27:06  Welcome, you are now connected to log-streaming service.
    2016-03-24T10:27:30.607 Function started (Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)
    2016-03-24T10:27:30.607 C# Queue trigger function processed: {"name":"Wes testing queues","address":"in a console app"}
    2016-03-24T10:27:30.607 Function completed (Success, Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)


<!-- URLs. -->

[Azure Portal]: https://portal.azure.com

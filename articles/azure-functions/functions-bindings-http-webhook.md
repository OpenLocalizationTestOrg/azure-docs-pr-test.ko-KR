---
title: "aaaAzure 함수 HTTP 및 webhook 바인딩을 | Microsoft Docs"
description: "Toouse HTTP 및 webhook 트리거 하는 방법을 이해 및 Azure 함수에서 바인딩."
services: functions
documentationcenter: na
author: mattchenderson
manager: erikre
editor: 
tags: 
keywords: "Azure Functions, 함수, 이벤트 처리, webhook, 동적 계산, 서버가 없는 아키텍처, HTTP, API, REST"
ms.assetid: 2b12200d-63d8-4ec1-9da8-39831d5a51b1
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/18/2016
ms.author: mahender
ms.openlocfilehash: c23b7a1443d492ed78c595e97d1d778a7ab12416
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-http-and-webhook-bindings"></a><span data-ttu-id="6aafd-104">Azure Functions HTTP 및 WebHook 바인딩</span><span class="sxs-lookup"><span data-stu-id="6aafd-104">Azure Functions HTTP and webhook bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="6aafd-105">이 문서에서는 tooconfigure 및 http 작업의 트리거 방법을 설명 및 Azure 함수에서 바인딩.</span><span class="sxs-lookup"><span data-stu-id="6aafd-105">This article explains how tooconfigure and work with HTTP triggers and bindings in Azure Functions.</span></span>
<span data-ttu-id="6aafd-106">이러한 Azure 함수 toobuild 서버가 없는 Api 및 응답 toowebhooks를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-106">With these, you can use Azure Functions toobuild serverless APIs and respond toowebhooks.</span></span>

<span data-ttu-id="6aafd-107">Azure 함수 hello를 바인딩은 다음을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-107">Azure Functions provides hello following bindings:</span></span>
- <span data-ttu-id="6aafd-108">[HTTP 트리거](#httptrigger)를 사용하면 HTTP 요청으로 함수를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-108">An [HTTP trigger](#httptrigger) lets you invoke a function with an HTTP request.</span></span> <span data-ttu-id="6aafd-109">사용자 지정 된 toorespond 너무 일 수 있습니다[webhook](#hooktrigger)합니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-109">This can be customized toorespond too[webhooks](#hooktrigger).</span></span>
- <span data-ttu-id="6aafd-110">[HTTP 출력 바인딩이](#output) toorespond toohello 요청을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-110">An [HTTP output binding](#output) allows you toorespond toohello request.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

<a name="httptrigger"></a>

## <a name="http-trigger"></a><span data-ttu-id="6aafd-111">HTTP 트리거</span><span class="sxs-lookup"><span data-stu-id="6aafd-111">HTTP trigger</span></span>
<span data-ttu-id="6aafd-112">hello HTTP 트리거 응답 tooan HTTP 요청에서 함수를 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-112">hello HTTP trigger will execute your function in response tooan HTTP request.</span></span> <span data-ttu-id="6aafd-113">Toorespond tooa 특정 URL 또는 HTTP 메서드 집합을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-113">You can customize it toorespond tooa particular URL or set of HTTP methods.</span></span> <span data-ttu-id="6aafd-114">HTTP 트리거를 사용 하는 구성 된 toorespond toowebhooks 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-114">An HTTP trigger can also be configured toorespond toowebhooks.</span></span> 

<span data-ttu-id="6aafd-115">Hello 함수 포털을 사용 하는 경우 시작할 수 있습니다도 미리 만든된 서식 파일을 사용 하 여 바로 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-115">If using hello Functions portal, you can also get started right away using a pre-made template.</span></span> <span data-ttu-id="6aafd-116">선택 **새 함수** hello에서 "API 및 Webhook"를 선택 하 고 **시나리오** 드롭다운입니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-116">Select **New function** and choose "API & Webhooks" from hello **Scenario** dropdown.</span></span> <span data-ttu-id="6aafd-117">Hello 템플릿 중 하나를 선택 하 고 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-117">Select one of hello templates and click **Create**.</span></span>

<span data-ttu-id="6aafd-118">기본적으로 HTTP 트리거는 HTTP 200 OK 상태 코드 및 빈 본문이 toohello 요청을 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-118">By default, an HTTP trigger will respond toohello request with an HTTP 200 OK status code and an empty body.</span></span> <span data-ttu-id="6aafd-119">toomodify 응답 hello, 구성 프로그램 [HTTP 출력 바인딩](#output)</span><span class="sxs-lookup"><span data-stu-id="6aafd-119">toomodify hello response, configure an [HTTP output binding](#output)</span></span>

### <a name="configuring-an-http-trigger"></a><span data-ttu-id="6aafd-120">HTTP 트리거 구성</span><span class="sxs-lookup"><span data-stu-id="6aafd-120">Configuring an HTTP trigger</span></span>
<span data-ttu-id="6aafd-121">Hello에서 다음 JSON 개체와 유사한 toohello를 포함 하 여 HTTP 트리거는 정의 된 `bindings` 배열 function.json입니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-121">An HTTP trigger is defined by including a JSON object similar toohello following in hello `bindings` array of function.json:</span></span>

```json
{
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
    "authLevel": "function",
    "methods": [ "get" ],
    "route": "values/{id}"
},
```
<span data-ttu-id="6aafd-122">hello 바인딩은 hello를 다음과 같은 속성을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-122">hello binding supports hello following properties:</span></span>

* <span data-ttu-id="6aafd-123">**이름** : 필요-hello 요청 또는 요청 본문에 대 한 함수 코드에서 사용 하는 hello 변수 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-123">**name** : Required - hello variable name used in function code for hello request or request body.</span></span> <span data-ttu-id="6aafd-124">[코드에서 HTTP 트리거 사용](#httptriggerusage)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6aafd-124">See [Working with an HTTP trigger from code](#httptriggerusage).</span></span>
* <span data-ttu-id="6aafd-125">**형식** : 필요-설정 해야 너무 "httpTrigger"입니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-125">**type** : Required - must be set too"httpTrigger".</span></span>
* <span data-ttu-id="6aafd-126">**방향** : 필요-"의 in" 너무 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-126">**direction** : Required - must be set too"in".</span></span>
* <span data-ttu-id="6aafd-127">_authLevel_ : toobe 순서 tooinvoke hello 함수에서 hello 요청에 있는 할 수 있는 경우 어떤 키를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-127">_authLevel_ : This determines what keys, if any, need toobe present on hello request in order tooinvoke hello function.</span></span> <span data-ttu-id="6aafd-128">아래의 [키 사용](#keys)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6aafd-128">See [Working with keys](#keys) below.</span></span> <span data-ttu-id="6aafd-129">hello 값 hello 다음 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-129">hello value can be one of hello following:</span></span>
    * <span data-ttu-id="6aafd-130">_anonymous_: API 키가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-130">_anonymous_: No API key is required.</span></span>
    * <span data-ttu-id="6aafd-131">_function_: 함수 전용 API 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-131">_function_: A function-specific API key is required.</span></span> <span data-ttu-id="6aafd-132">아무 것도 제공 하는 경우 hello 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-132">This is hello default value if none is provided.</span></span>
    * <span data-ttu-id="6aafd-133">_관리자_ : hello 마스터 키가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-133">_admin_ : hello master key is required.</span></span>
* <span data-ttu-id="6aafd-134">**메서드** : hello HTTP 메서드 toowhich hello 함수는 응답의 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-134">**methods** : This is an array of hello HTTP methods toowhich hello function will respond.</span></span> <span data-ttu-id="6aafd-135">지정 하지 않으면 hello 함수 tooall HTTP 메서드에 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-135">If not specified, hello function will respond tooall HTTP methods.</span></span> <span data-ttu-id="6aafd-136">참조 [hello HTTP 끝점을 사용자 지정](#url)합니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-136">See [Customizing hello HTTP endpoint](#url).</span></span>
* <span data-ttu-id="6aafd-137">**경로** : toowhich 제어 되는 hello 경로 템플릿을 정의 합니다. 요청 Url 함수 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-137">**route** : This defines hello route template, controlling toowhich request URLs your function will respond.</span></span> <span data-ttu-id="6aafd-138">hello 제공 하지 않으면 기본값은 `<functionname>`합니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-138">hello default value if none is provided is `<functionname>`.</span></span> <span data-ttu-id="6aafd-139">참조 [hello HTTP 끝점을 사용자 지정](#url)합니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-139">See [Customizing hello HTTP endpoint](#url).</span></span>
* <span data-ttu-id="6aafd-140">**webHookType** : 그러면 HTTP hello 트리거 tooact hello 지정 된 공급자에 대 한 webhook 수신기로 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-140">**webHookType** : This configures hello HTTP trigger tooact as a webhook reciever for hello specified provider.</span></span> <span data-ttu-id="6aafd-141">hello _메서드_ 선택이 속성을 설정 하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-141">hello _methods_ property should not be set if this is chosen.</span></span> <span data-ttu-id="6aafd-142">참조 [응답 중 toowebhooks](#hooktrigger)합니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-142">See [Responding toowebhooks](#hooktrigger).</span></span> <span data-ttu-id="6aafd-143">hello 값 hello 다음 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-143">hello value can be one of hello following:</span></span>
    * <span data-ttu-id="6aafd-144">_genericJson_: 특정 공급자를 위한 논리가 없는 범용 webhook 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-144">_genericJson_ : A general purpose webhook endpoint without logic for a specific provider.</span></span>
    * <span data-ttu-id="6aafd-145">_github_ : hello 함수 tooGitHub webhook 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-145">_github_ : hello function will respond tooGitHub webhooks.</span></span> <span data-ttu-id="6aafd-146">hello _authLevel_ 선택이 속성을 설정 하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-146">hello _authLevel_ property should not be set if this is chosen.</span></span>
    * <span data-ttu-id="6aafd-147">_slack_ : hello 함수 tooSlack webhook 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-147">_slack_ : hello function will respond tooSlack webhooks.</span></span> <span data-ttu-id="6aafd-148">hello _authLevel_ 선택이 속성을 설정 하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-148">hello _authLevel_ property should not be set if this is chosen.</span></span>

<a name="httptriggerusage"></a>
### <a name="working-with-an-http-trigger-from-code"></a><span data-ttu-id="6aafd-149">코드에서 HTTP 트리거 사용</span><span class="sxs-lookup"><span data-stu-id="6aafd-149">Working with an HTTP trigger from code</span></span>
<span data-ttu-id="6aafd-150">C# 및 F # 함수에 대 한 형식을 선언할 수 있습니다 hello 트리거 입력된 toobe의 하거나 `HttpRequestMessage` 또는 사용자 지정 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-150">For C# and F# functions, you can declare hello type of your trigger input toobe either `HttpRequestMessage` or a custom type.</span></span> <span data-ttu-id="6aafd-151">선택 하면 `HttpRequestMessage`, 모든 액세스 toohello 요청 개체를 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-151">If you choose `HttpRequestMessage`, then you will get full access toohello request object.</span></span> <span data-ttu-id="6aafd-152">사용자 지정 형식 (예: POCO)에 대 한 함수는 JSON toopopulate hello 개체 속성으로 tooparse hello 요청 본문을 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-152">For a custom type (such as a POCO), Functions will attempt tooparse hello request body as JSON toopopulate hello object properties.</span></span>

<span data-ttu-id="6aafd-153">Node.js 함수에 대 한 hello 함수 런타임은 hello 요청 개체 대신 hello 요청 본문을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-153">For Node.js functions, hello Functions runtime provides hello request body instead of hello request object.</span></span>

<span data-ttu-id="6aafd-154">사용 예제는 [HTTP 트리거 샘플](#httptriggersample)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6aafd-154">See [HTTP trigger samples](#httptriggersample) for example usages.</span></span>


<a name="output"></a>
## <a name="http-response-output-binding"></a><span data-ttu-id="6aafd-155">HTTP 응답 출력 바인딩</span><span class="sxs-lookup"><span data-stu-id="6aafd-155">HTTP response output binding</span></span>
<span data-ttu-id="6aafd-156">Hello HTTP 출력 바인딩 toorespond toohello HTTP 요청 발신자를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-156">Use hello HTTP output binding toorespond toohello HTTP request sender.</span></span> <span data-ttu-id="6aafd-157">이 바인딩은 HTTP 트리거는 걸리며 hello 트리거 요청과 연결 된 toocustomize hello 응답 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-157">This binding requires an HTTP trigger and allows you toocustomize hello response associated with hello trigger's request.</span></span> <span data-ttu-id="6aafd-158">HTTP 출력 바인딩이 제공되지 않으면 HTTP 트리거는 빈 본문과 함께 HTTP 200 OK를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-158">If an HTTP output binding is not provided, an HTTP trigger will return HTTP 200 OK with an empty body.</span></span> 

### <a name="configuring-an-http-output-binding"></a><span data-ttu-id="6aafd-159">HTTP 출력 바인딩 구성</span><span class="sxs-lookup"><span data-stu-id="6aafd-159">Configuring an HTTP output binding</span></span>
<span data-ttu-id="6aafd-160">hello HTTP 바인딩이 hello에서 다음 JSON 개체와 유사한 toohello를 포함 하 여 정의 된 출력 `bindings` function.json의 배열:</span><span class="sxs-lookup"><span data-stu-id="6aafd-160">hello HTTP output binding is defined by including a JSON object similar toohello following in hello `bindings` array of function.json:</span></span>

```json
{
    "name": "res",
    "type": "http",
    "direction": "out"
}
```
<span data-ttu-id="6aafd-161">hello 바인딩에 hello 다음 속성이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-161">hello binding contains hello following properties:</span></span>

* <span data-ttu-id="6aafd-162">**이름** : hello 응답에 대 한 함수 코드에서 사용 되는 변수 이름 hello 필요-합니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-162">**name** : Required - hello variable name used in function code for hello response.</span></span> <span data-ttu-id="6aafd-163">[코드에서 HTTP 출력 바인딩 사용](#outputusage)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6aafd-163">See [Working with an HTTP output binding from code](#outputusage).</span></span>
* <span data-ttu-id="6aafd-164">**형식** : 필요-설정 해야 너무 "http"입니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-164">**type** : Required - must be set too"http".</span></span>
* <span data-ttu-id="6aafd-165">**방향** : 필요-"out" 너무 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-165">**direction** : Required - must be set too"out".</span></span>

<a name="outputusage"></a>
### <a name="working-with-an-http-output-binding-from-code"></a><span data-ttu-id="6aafd-166">코드에서 HTTP 출력 바인딩 사용</span><span class="sxs-lookup"><span data-stu-id="6aafd-166">Working with an HTTP output binding from code</span></span>
<span data-ttu-id="6aafd-167">Hello 출력 매개 변수 (예: "res") toorespond toohello http 또는 webhook 호출자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-167">You can use hello output parameter (e.g., "res") toorespond toohello http or webhook caller.</span></span> <span data-ttu-id="6aafd-168">또는 표준을 사용할 수 있습니다 `Request.CreateResponse()` (C#) 또는 `context.res` (Node.JS) 패턴 tooreturn 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-168">Alternatively, you can use the standard `Request.CreateResponse()` (C#) or `context.res` (Node.JS) pattern tooreturn your response.</span></span> <span data-ttu-id="6aafd-169">Toouse 두 번째 방법을 hello 하는 방법에 대 한 예제를 보려면 [HTTP 트리거 샘플](#httptriggersample) 및 [Webhook 트리거 샘플](#hooktriggersample)합니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-169">For examples on how toouse hello latter method, see [HTTP trigger samples](#httptriggersample) and [Webhook trigger samples](#hooktriggersample).</span></span>


<a name="hooktrigger"></a>
## <a name="responding-toowebhooks"></a><span data-ttu-id="6aafd-170">Toowebhooks 응답</span><span class="sxs-lookup"><span data-stu-id="6aafd-170">Responding toowebhooks</span></span>
<span data-ttu-id="6aafd-171">Hello로 HTTP 트리거는 _webHookType_ 속성이 되 구성된 toorespond 너무[webhook](https://en.wikipedia.org/wiki/Webhook)합니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-171">An HTTP trigger with hello _webHookType_ property will be configured toorespond too[webhooks](https://en.wikipedia.org/wiki/Webhook).</span></span> <span data-ttu-id="6aafd-172">hello 기본 구성에는 hello "genericJson" 설정이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-172">hello basic configuration uses hello "genericJson" setting.</span></span> <span data-ttu-id="6aafd-173">이 경우 제한 요청 tooonly hello로 POST 및 HTTP를 사용 하 여 `application/json` 콘텐츠 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-173">This restricts requests tooonly those using HTTP POST and with hello `application/json` content type.</span></span>

<span data-ttu-id="6aafd-174">hello 트리거 일 수 있습니다 또한 맞춤형된 tooa 특정 webhook 공급자 (예: [GitHub](https://developer.github.com/webhooks/) 및 [Slack](https://api.slack.com/outgoing-webhooks)).</span><span class="sxs-lookup"><span data-stu-id="6aafd-174">hello trigger can additionally be tailored tooa specific webhook provider (e.g., [GitHub](https://developer.github.com/webhooks/) and [Slack](https://api.slack.com/outgoing-webhooks)).</span></span> <span data-ttu-id="6aafd-175">공급자를 지정 하는 경우를 hello 함수 런타임 hello 공급자의 유효성 검사 논리를 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-175">If a provider is specified, hello Functions runtime can take care of hello provider's validation logic for you.</span></span>  

### <a name="configuring-github-as-a-webhook-provider"></a><span data-ttu-id="6aafd-176">GitHub를 웹후크 공급자로 구성</span><span class="sxs-lookup"><span data-stu-id="6aafd-176">Configuring GitHub as a webhook provider</span></span>
<span data-ttu-id="6aafd-177">toorespond tooGitHub webhook을 먼저 함수는 HTTP 트리거를 만들고 설정 hello _webHookType_ 속성 너무 "github"입니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-177">toorespond tooGitHub webhooks, first create your function with an HTTP Trigger, and set hello _webHookType_ property too"github".</span></span> <span data-ttu-id="6aafd-178">그런 다음 [URL](#url) 및 [API 키](#keys)를 GitHub 리포지토리의 **webhook 추가** 페이지에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-178">Then copy its [URL](#url) and [API key](#keys) into your GitHub repository's **Add webhook** page.</span></span> <span data-ttu-id="6aafd-179">자세한 내용은 GitHub의 [Webhook 만들기](http://go.microsoft.com/fwlink/?LinkID=761099&clcid=0x409) 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6aafd-179">See GitHub's [Creating Webhooks](http://go.microsoft.com/fwlink/?LinkID=761099&clcid=0x409) documentation for more.</span></span>

![](./media/functions-bindings-http-webhook/github-add-webhook.png)

### <a name="configuring-slack-as-a-webhook-provider"></a><span data-ttu-id="6aafd-180">Slack을 webhook 공급자로 구성</span><span class="sxs-lookup"><span data-stu-id="6aafd-180">Configuring Slack as a webhook provider</span></span>
<span data-ttu-id="6aafd-181">hello Slack webhook 대신 Slack hello 토큰으로 함수 전용 키를 구성 해야 하므로, 지정할 수 있습니다에 대 한 토큰을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-181">hello Slack webhook generates a token for you instead of letting you specify it, so you must configure a function-specific key with hello token from Slack.</span></span> <span data-ttu-id="6aafd-182">[키 사용](#keys)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6aafd-182">See [Working with keys](#keys).</span></span>

<a name="url"></a>
## <a name="customizing-hello-http-endpoint"></a><span data-ttu-id="6aafd-183">Hello HTTP 끝점을 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="6aafd-183">Customizing hello HTTP endpoint</span></span>
<span data-ttu-id="6aafd-184">기본적으로 HTTP 트리거나, WebHook에 대 한 함수를 만들 때 hello 함수는 hello 폼의 경로와 주소 지정 가능.</span><span class="sxs-lookup"><span data-stu-id="6aafd-184">By default when you create a function for an HTTP trigger, or WebHook, hello function is addressable with a route of hello form:</span></span>

    http://<yourapp>.azurewebsites.net/api/<funcname> 

<span data-ttu-id="6aafd-185">선택적 hello를 사용 하 여이 경로 사용자 지정할 수 있습니다 `route` hello HTTP 트리거에 대 한 속성이 바인딩을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-185">You can customize this route using hello optional `route` property on hello HTTP trigger's input binding.</span></span> <span data-ttu-id="6aafd-186">예를 들어, 다음 hello *function.json* 파일 정의 `route` HTTP 트리거는에 대 한 속성:</span><span class="sxs-lookup"><span data-stu-id="6aafd-186">As an example, hello following *function.json* file defines a `route` property for an HTTP trigger:</span></span>

```json
    {
      "bindings": [
        {
          "type": "httpTrigger",
          "name": "req",
          "direction": "in",
          "methods": [ "get" ],
          "route": "products/{category:alpha}/{id:int?}"
        },
        {
          "type": "http",
          "name": "res",
          "direction": "out"
        }
      ]
    }
```

<span data-ttu-id="6aafd-187">이 구성을 사용 하 여, hello 함수는 현재 주소 지정 가능 경로 hello 원래 경로 대신 다음 hello로 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-187">Using this configuration, hello function is now addressable with hello following route instead of hello original route.</span></span>

    http://<yourapp>.azurewebsites.net/api/products/electronics/357

<span data-ttu-id="6aafd-188">이렇게 하면 hello 함수 코드 hello 주소, "범주" 및 "id" toosupport 두 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-188">This allows hello function code toosupport two parameters in hello address, "category" and "id".</span></span> <span data-ttu-id="6aafd-189">매개 변수에서 [웹 API 경로 제약 조건](https://www.asp.net/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2#constraints)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-189">You can use any [Web API Route Constraint](https://www.asp.net/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2#constraints) with your parameters.</span></span> <span data-ttu-id="6aafd-190">C# 함수 코드 다음 hello에서는 두 매개 변수를 활용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-190">hello following C# function code makes use of both parameters.</span></span>

```csharp
    public static Task<HttpResponseMessage> Run(HttpRequestMessage req, string category, int? id, 
                                                    TraceWriter log)
    {
        if (id == null)
           return  req.CreateResponse(HttpStatusCode.OK, $"All {category} items were requested.");
        else
           return  req.CreateResponse(HttpStatusCode.OK, $"{category} item with id = {id} has been requested.");
    }
```

<span data-ttu-id="6aafd-191">여기서는 Node.js 함수 코드 toouse hello 동일한 경로 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-191">Here is Node.js function code toouse hello same route parameters.</span></span>

```javascript
    module.exports = function (context, req) {

        var category = context.bindingData.category;
        var id = context.bindingData.id;

        if (!id) {
            context.res = {
                // status: 200, /* Defaults too200 */
                body: "All " + category + " items were requested."
            };
        }
        else {
            context.res = {
                // status: 200, /* Defaults too200 */
                body: category + " item with id = " + id + " was requested."
            };
        }

        context.done();
    } 
```

<span data-ttu-id="6aafd-192">기본적으로 모든 함수 경로에는 *api* 접두사가 붙습니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-192">By default, all function routes are prefixed with *api*.</span></span> <span data-ttu-id="6aafd-193">또한 사용자 지정 하거나 hello를 사용 하 여 hello 접두사를 제거할 수 `http.routePrefix` 속성에 프로그램 *host.json* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-193">You can also customize or remove hello prefix using hello `http.routePrefix` property in your *host.json* file.</span></span> <span data-ttu-id="6aafd-194">hello 다음 예제에서는 제거 hello *api* hello에 hello 접두사에 대 한 빈 문자열을 사용 하 여 경로 접두사 *host.json* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-194">hello following example removes hello *api* route prefix by using an empty string for hello prefix in hello *host.json* file.</span></span>

```json
    {
      "http": {
        "routePrefix": ""
      }
    }
```

<span data-ttu-id="6aafd-195">에 대 한 자세한 내용은 방법 tooupdate hello *host.json* 참조, 함수에 대 한 파일 [tooupdate 앱 파일을 어떻게 작동 하는지](functions-reference.md#fileupdate)합니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-195">For detailed information on how tooupdate hello *host.json* file for your function, See, [How tooupdate function app files](functions-reference.md#fileupdate).</span></span> 

<span data-ttu-id="6aafd-196">*host.json* 파일에서 구성할 수 있는 다른 속성에 대한 자세한 내용은 [host.json 참조](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6aafd-196">For information on other properties you can configure in your *host.json* file, see [host.json reference](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span>


<a name="keys"></a>
## <a name="working-with-keys"></a><span data-ttu-id="6aafd-197">키 사용</span><span class="sxs-lookup"><span data-stu-id="6aafd-197">Working with keys</span></span>
<span data-ttu-id="6aafd-198">HttpTriggers는 보안 강화를 위해 키를 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-198">HttpTriggers can leverage keys for added security.</span></span> <span data-ttu-id="6aafd-199">표준 HttpTrigger צ ְ ײ API 키로 이러한 hello 요청에 있는 키 toobe hello 요구 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-199">A standard HttpTrigger can use these as an API key, requiring hello key toobe present on hello request.</span></span> <span data-ttu-id="6aafd-200">또한 Webhook 키 tooauthorize 요청에서 다양 한 방법으로 어떤 hello 공급자 지원에 따라 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-200">Webhooks can use keys tooauthorize requests in a variety of ways, depending on what hello provider supports.</span></span>

<span data-ttu-id="6aafd-201">키는 Azure에 함수 앱의 일부로 저장되며 나머지는 암호화되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-201">Keys are stored as part of your function app in Azure and are encrypted at rest.</span></span> <span data-ttu-id="6aafd-202">tooview 키를 새 데이터베이스를 만들고 또는 롤 toonew 값 키 hello 포털 내에서 함수 tooone 이동한 "Manage"를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-202">tooview your keys, create new ones, or roll keys toonew values, navigate tooone of your functions within hello portal and select "Manage."</span></span> 

<span data-ttu-id="6aafd-203">다음과 같이 두 가지 유형의 키가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-203">There are two types of keys:</span></span>
- <span data-ttu-id="6aafd-204">**호스트에서 호스트 키**: hello 함수 앱 내에서 모든 기능에서 이러한 키를 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-204">**Host keys**: These keys are shared by all functions within hello function app.</span></span> <span data-ttu-id="6aafd-205">API 키로 사용할 경우 hello 함수 앱 내에서 access tooany 함수를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-205">When used as an API key, these allow access tooany function within hello function app.</span></span>
- <span data-ttu-id="6aafd-206">**기능 키**: 이러한 키 toohello 특정 함수만는 정의 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-206">**Function keys**: These keys apply only toohello specific functions under which they are defined.</span></span> <span data-ttu-id="6aafd-207">API 키로 사용할 경우 액세스 toothat 함수 이러한만 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-207">When used as an API key, these only allow access toothat function.</span></span>

<span data-ttu-id="6aafd-208">참조를 위해 각 키의 이름을 지정 하 고 hello 함수 및 호스트 수준에서 기본 키 (이름: "default")가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-208">Each key is named for reference, and there is a default key (named "default") at hello function and host level.</span></span> <span data-ttu-id="6aafd-209">hello **마스터 키** 기본 호스트 키를 각각 함수 앱에 대해 정의 되 고 해지할 수 없습니다 "_master" 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-209">hello **master key** is a default host key named "_master" that is defined for each function app and cannot be revoked.</span></span> <span data-ttu-id="6aafd-210">관리 액세스 toohello 런타임 Api를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-210">It provides administrative access toohello runtime APIs.</span></span> <span data-ttu-id="6aafd-211">사용 하 여 `"authLevel": "admin"` hello JSON 바인딩 필요 합니다 hello 요청에 표시 된이 키 toobe; 다른 키 권한 부여 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-211">Using `"authLevel": "admin"` in hello binding JSON will require this key toobe presented on hello request; any other key will result in a authorization failure.</span></span>

> [!NOTE]
> <span data-ttu-id="6aafd-212">기한 toohello 높은 권한을 hello 마스터 키로 부여 제 3 자와이 키를 공유 하거나 네이티브 클라이언트 응용 프로그램에 배포 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-212">Due toohello elevated permissions granted by hello master key, you should not share this key with third parties or distribute it in native client applications.</span></span> <span data-ttu-id="6aafd-213">Hello 관리자 권한 수준을 선택할 때는 주의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-213">Exercise caution when choosing hello admin authorization level.</span></span>
> 
> 

### <a name="api-key-authorization"></a><span data-ttu-id="6aafd-214">API 키 권한 부여</span><span class="sxs-lookup"><span data-stu-id="6aafd-214">API key authorization</span></span>
<span data-ttu-id="6aafd-215">기본적으로는 HttpTrigger hello HTTP 요청에 있는 API 키를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-215">By default, an HttpTrigger requires an API key in hello HTTP request.</span></span> <span data-ttu-id="6aafd-216">따라서 HTTP 요청은 일반적으로 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-216">So your HTTP request normally looks like this:</span></span>

    https://<yourapp>.azurewebsites.net/api/<function>?code=<ApiKey>

<span data-ttu-id="6aafd-217">명명 된 쿼리 문자열 변수에 hello 키를 포함 될 수 있습니다 `code`, 위의 설명 참조 또는에 포함 될 수는 `x-functions-key` HTTP 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-217">hello key can be included in a query string variable named `code`, as above, or it can be included in an `x-functions-key` HTTP header.</span></span> <span data-ttu-id="6aafd-218">기능 키 hello 함수에 대해 정의 된 또는 모든 호스트 키 hello hello 키 값 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-218">hello value of hello key can be any function key defined for hello function, or any host key.</span></span>

<span data-ttu-id="6aafd-219">키가 없는 tooallow 요청에서 선택 하거나 hello를 변경 하 여 hello 마스터 키를 사용 해야 지정할 수 있습니다 `authLevel` JSON 바인딩 hello에 대 한 속성 (참조 [HTTP 트리거](#httptrigger)).</span><span class="sxs-lookup"><span data-stu-id="6aafd-219">You can choose tooallow requests without keys or specify that hello master key must be used by changing hello `authLevel` property in hello binding JSON (see [HTTP trigger](#httptrigger)).</span></span>

### <a name="keys-and-webhooks"></a><span data-ttu-id="6aafd-220">키 및 webhook</span><span class="sxs-lookup"><span data-stu-id="6aafd-220">Keys and webhooks</span></span>
<span data-ttu-id="6aafd-221">Hello webhook 수신기 구성 요소에 의해 Webhook 권한 부여를 처리, HttpTrigger, hello 및 hello 메커니즘의 일부는 hello webhook 형식에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-221">Webhook authorization is handled by hello webhook reciever component, part of hello HttpTrigger, and hello mechanism varies based on hello webhook type.</span></span> <span data-ttu-id="6aafd-222">그러나 각 메커니즘마다 키를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-222">Each mechanism does, however rely on a key.</span></span> <span data-ttu-id="6aafd-223">기본적으로 "default" 라는 hello 기능 키 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-223">By default, hello function key named "default" will be used.</span></span> <span data-ttu-id="6aafd-224">다른 키 toouse을 원할 경우 tooconfigure hello webhook 공급자 toosend hello 키 이름을 hello 같은 방법으로 다음 중 하나에 hello 요청 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-224">If you wish toouse a different key, you will need tooconfigure hello webhook provider toosend hello key name with hello request in one of hello following ways:</span></span>

- <span data-ttu-id="6aafd-225">**쿼리 문자열**: hello 공급자 hello hello 키 이름 전달 `clientid` 쿼리 문자열 매개 변수 (예: `https://<yourapp>.azurewebsites.net/api/<funcname>?clientid=<keyname>`).</span><span class="sxs-lookup"><span data-stu-id="6aafd-225">**Query string**: hello provider passes hello key name in hello `clientid` query string parameter (e.g., `https://<yourapp>.azurewebsites.net/api/<funcname>?clientid=<keyname>`).</span></span>
- <span data-ttu-id="6aafd-226">**요청 헤더**: hello 공급자 hello hello 키 이름 전달 `x-functions-clientid` 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-226">**Request header**: hello provider passes hello key name in hello `x-functions-clientid` header.</span></span>

> [!NOTE]
> <span data-ttu-id="6aafd-227">function 키는 호스트 키보다 우선합니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-227">Function keys take precedence over host keys.</span></span> <span data-ttu-id="6aafd-228">동일한 이름, hello hello로 두 키가 정의 하는 경우 기능 키를 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-228">If two keys are defined with hello same name, hello function key will be used.</span></span>
> 
> 


<a name="httptriggersample"></a>
## <a name="http-trigger-samples"></a><span data-ttu-id="6aafd-229">HTTP 트리거 샘플</span><span class="sxs-lookup"><span data-stu-id="6aafd-229">HTTP trigger samples</span></span>
<span data-ttu-id="6aafd-230">있다고 가정 하면 다음 hello에서 HTTP 트리거 hello `bindings` function.json의 배열:</span><span class="sxs-lookup"><span data-stu-id="6aafd-230">Suppose you have hello following HTTP trigger in hello `bindings` array of function.json:</span></span>

```json
{
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
    "authLevel": "function"
},
```

<span data-ttu-id="6aafd-231">검색 하는 hello 언어 관련 샘플을 참조 한 `name` hello 쿼리 문자열 또는 hello hello HTTP 요청 본문에서 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-231">See hello language-specific sample that looks for a `name` parameter either in hello query string or hello body of hello HTTP request.</span></span>

* [<span data-ttu-id="6aafd-232">C#</span><span class="sxs-lookup"><span data-stu-id="6aafd-232">C#</span></span>](#httptriggercsharp)
* [<span data-ttu-id="6aafd-233">F#</span><span class="sxs-lookup"><span data-stu-id="6aafd-233">F#</span></span>](#httptriggerfsharp)
* [<span data-ttu-id="6aafd-234">Node.JS</span><span class="sxs-lookup"><span data-stu-id="6aafd-234">Node.js</span></span>](#httptriggernodejs)


<a name="httptriggercsharp"></a>
### <a name="http-trigger-sample-in-c"></a><span data-ttu-id="6aafd-235">C#의 HTTP 트리거 샘플</span><span class="sxs-lookup"><span data-stu-id="6aafd-235">HTTP trigger sample in C#</span></span> #
```csharp
using System.Net;
using System.Threading.Tasks;

public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
{
    log.Info($"C# HTTP trigger function processed a request. RequestUri={req.RequestUri}");

    // parse query parameter
    string name = req.GetQueryNameValuePairs()
        .FirstOrDefault(q => string.Compare(q.Key, "name", true) == 0)
        .Value;

    // Get request body
    dynamic data = await req.Content.ReadAsAsync<object>();

    // Set name tooquery string or body data
    name = name ?? data?.name;

    return name == null
        ? req.CreateResponse(HttpStatusCode.BadRequest, "Please pass a name on hello query string or in hello request body")
        : req.CreateResponse(HttpStatusCode.OK, "Hello " + name);
}
```

<span data-ttu-id="6aafd-236">POCO tooa 바인딩할 수도 있습니다 대신 `HttpRequestMessage`합니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-236">You can also bind tooa POCO instead of `HttpRequestMessage`.</span></span> <span data-ttu-id="6aafd-237">이 hello 요청을 JSON으로 구문 분석의 hello 본문에서 하이드레이션 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-237">This will be hydrated from hello body of hello request, parsed as JSON.</span></span> <span data-ttu-id="6aafd-238">마찬가지로, 형식, 바인딩 toohello HTTP 응답 출력을 전달할 수 있습니다 및 200 상태 코드와 함께 hello 응답 본문으로 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-238">Similarly, a type can be passed toohello HTTP response output binding, and this will be returned as hello response body, with a 200 status code.</span></span>
```csharp
using System.Net;
using System.Threading.Tasks;

public static string Run(CustomObject req, TraceWriter log)
{
    return "Hello " + req?.name;
}

public class CustomObject {
     public String name {get; set;}
}
}
```

<a name="httptriggerfsharp"></a>
### <a name="http-trigger-sample-in-f"></a><span data-ttu-id="6aafd-239">F#의 HTTP 트리거 샘플</span><span class="sxs-lookup"><span data-stu-id="6aafd-239">HTTP trigger sample in F#</span></span> #
```fsharp
open System.Net
open System.Net.Http
open FSharp.Interop.Dynamic

let Run(req: HttpRequestMessage) =
    async {
        let q =
            req.GetQueryNameValuePairs()
                |> Seq.tryFind (fun kv -> kv.Key = "name")
        match q with
        | Some kv ->
            return req.CreateResponse(HttpStatusCode.OK, "Hello " + kv.Value)
        | None ->
            let! data = Async.AwaitTask(req.Content.ReadAsAsync<obj>())
            try
                return req.CreateResponse(HttpStatusCode.OK, "Hello " + data?name)
            with e ->
                return req.CreateErrorResponse(HttpStatusCode.BadRequest, "Please pass a name on hello query string or in hello request body")
    } |> Async.StartAsTask
```

<span data-ttu-id="6aafd-240">필요한는 `project.json` NuGet tooreference hello를 사용 하는 파일 `FSharp.Interop.Dynamic` 및 `Dynamitey` 다음과 같이 어셈블리:</span><span class="sxs-lookup"><span data-stu-id="6aafd-240">You need a `project.json` file that uses NuGet tooreference hello `FSharp.Interop.Dynamic` and `Dynamitey` assemblies, like this:</span></span>

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

<span data-ttu-id="6aafd-241">사용 NuGet toofetch 종속성 하 고 스크립트에서 개체를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aafd-241">This will use NuGet toofetch your dependencies and will reference them in your script.</span></span>

<a name="httptriggernodejs"></a>
### <a name="http-trigger-sample-in-nodejs"></a><span data-ttu-id="6aafd-242">Node.js의 트리거 샘플</span><span class="sxs-lookup"><span data-stu-id="6aafd-242">HTTP trigger sample in Node.JS</span></span>
```javascript
module.exports = function(context, req) {
    context.log('Node.js HTTP trigger function processed a request. RequestUri=%s', req.originalUrl);

    if (req.query.name || (req.body && req.body.name)) {
        context.res = {
            // status: 200, /* Defaults too200 */
            body: "Hello " + (req.query.name || req.body.name)
        };
    }
    else {
        context.res = {
            status: 400,
            body: "Please pass a name on hello query string or in hello request body"
        };
    }
    context.done();
};
```



<a name="hooktriggersample"></a>
## <a name="webhook-samples"></a><span data-ttu-id="6aafd-243">Webhook 샘플</span><span class="sxs-lookup"><span data-stu-id="6aafd-243">Webhook samples</span></span>
<span data-ttu-id="6aafd-244">있다고 가정 하면 다음 hello에 대 한 webhook 트리거 hello `bindings` function.json의 배열:</span><span class="sxs-lookup"><span data-stu-id="6aafd-244">Suppose you have hello following webhook trigger in hello `bindings` array of function.json:</span></span>

```json
{
    "webHookType": "github",
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
},
```

<span data-ttu-id="6aafd-245">GitHub 문제 설명을 기록 하는 hello 언어 관련 샘플을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="6aafd-245">See hello language-specific sample that logs GitHub issue comments.</span></span>

* [<span data-ttu-id="6aafd-246">C#</span><span class="sxs-lookup"><span data-stu-id="6aafd-246">C#</span></span>](#hooktriggercsharp)
* [<span data-ttu-id="6aafd-247">F#</span><span class="sxs-lookup"><span data-stu-id="6aafd-247">F#</span></span>](#hooktriggerfsharp)
* [<span data-ttu-id="6aafd-248">Node.JS</span><span class="sxs-lookup"><span data-stu-id="6aafd-248">Node.js</span></span>](#hooktriggernodejs)

<a name="hooktriggercsharp"></a>

### <a name="webhook-sample-in-c"></a><span data-ttu-id="6aafd-249">C#의 웹후크 샘플</span><span class="sxs-lookup"><span data-stu-id="6aafd-249">Webhook sample in C#</span></span> #
```csharp
#r "Newtonsoft.Json"

using System;
using System.Net;
using System.Threading.Tasks;
using Newtonsoft.Json;

public static async Task<object> Run(HttpRequestMessage req, TraceWriter log)
{
    string jsonContent = await req.Content.ReadAsStringAsync();
    dynamic data = JsonConvert.DeserializeObject(jsonContent);

    log.Info($"WebHook was triggered! Comment: {data.comment.body}");

    return req.CreateResponse(HttpStatusCode.OK, new {
        body = $"New GitHub comment: {data.comment.body}"
    });
}
```

<a name="hooktriggerfsharp"></a>

### <a name="webhook-sample-in-f"></a><span data-ttu-id="6aafd-250">F#의 웹후크 샘플</span><span class="sxs-lookup"><span data-stu-id="6aafd-250">Webhook sample in F#</span></span> #
```fsharp
open System.Net
open System.Net.Http
open FSharp.Interop.Dynamic
open Newtonsoft.Json

type Response = {
    body: string
}

let Run(req: HttpRequestMessage, log: TraceWriter) =
    async {
        let! content = req.Content.ReadAsStringAsync() |> Async.AwaitTask
        let data = content |> JsonConvert.DeserializeObject
        log.Info(sprintf "GitHub WebHook triggered! %s" data?comment?body)
        return req.CreateResponse(
            HttpStatusCode.OK,
            { body = sprintf "New GitHub comment: %s" data?comment?body })
    } |> Async.StartAsTask
```

<a name="hooktriggernodejs"></a>

### <a name="webhook-sample-in-nodejs"></a><span data-ttu-id="6aafd-251">Node.JS의 Webhook 샘플</span><span class="sxs-lookup"><span data-stu-id="6aafd-251">Webhook sample in Node.JS</span></span>
```javascript
module.exports = function (context, data) {
    context.log('GitHub WebHook triggered!', data.comment.body);
    context.res = { body: 'New GitHub comment: ' + data.comment.body };
    context.done();
};
```


## <a name="next-steps"></a><span data-ttu-id="6aafd-252">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6aafd-252">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]


---
title: "Azure Functions HTTP 및 webhook 바인딩 | Microsoft 문서"
description: "Azure Functions에서 HTTP와 WebHook 트리거 및 바인딩을 사용하는 방법을 파악합니다."
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
ms.openlocfilehash: 71c0d22c4b1824078982b9d1cc76645f947ae603
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-functions-http-and-webhook-bindings"></a><span data-ttu-id="8b67b-104">Azure Functions HTTP 및 WebHook 바인딩</span><span class="sxs-lookup"><span data-stu-id="8b67b-104">Azure Functions HTTP and webhook bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="8b67b-105">이 문서에서는 Azure Functions에서 HTTP 트리거 및 바인딩을 구성하고 사용하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-105">This article explains how to configure and work with HTTP triggers and bindings in Azure Functions.</span></span>
<span data-ttu-id="8b67b-106">이러한 트리거와 바인딩을 사용하면 Azure Functions에서 서버가 없는 API를 만들고 webhook에 응답할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-106">With these, you can use Azure Functions to build serverless APIs and respond to webhooks.</span></span>

<span data-ttu-id="8b67b-107">Azure Functions에서 제공하는 바인딩은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-107">Azure Functions provides the following bindings:</span></span>
- <span data-ttu-id="8b67b-108">[HTTP 트리거](#httptrigger)를 사용하면 HTTP 요청으로 함수를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-108">An [HTTP trigger](#httptrigger) lets you invoke a function with an HTTP request.</span></span> <span data-ttu-id="8b67b-109">이 트리거는 [webhook](#hooktrigger)에 응답하도록 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-109">This can be customized to respond to [webhooks](#hooktrigger).</span></span>
- <span data-ttu-id="8b67b-110">[HTTP 출력 바인딩](#output)을 사용하면 요청에 응답할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-110">An [HTTP output binding](#output) allows you to respond to the request.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

<a name="httptrigger"></a>

## <a name="http-trigger"></a><span data-ttu-id="8b67b-111">HTTP 트리거</span><span class="sxs-lookup"><span data-stu-id="8b67b-111">HTTP trigger</span></span>
<span data-ttu-id="8b67b-112">HTTP 트리거는 HTTP 요청에 대한 응답으로 함수를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-112">The HTTP trigger will execute your function in response to an HTTP request.</span></span> <span data-ttu-id="8b67b-113">특정 URL 또는 HTTP 메서드 집합에 응답하도록 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-113">You can customize it to respond to a particular URL or set of HTTP methods.</span></span> <span data-ttu-id="8b67b-114">또한 HTTP 트리거는 webhook에도 응답하도록 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-114">An HTTP trigger can also be configured to respond to webhooks.</span></span> 

<span data-ttu-id="8b67b-115">Functions 포털을 사용하는 경우 미리 만든 템플릿을 사용하여 바로 시작할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-115">If using the Functions portal, you can also get started right away using a pre-made template.</span></span> <span data-ttu-id="8b67b-116">**새 함수**를 선택하고 **시나리오** 드롭다운에서 [API & Webhooks]를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-116">Select **New function** and choose "API & Webhooks" from the **Scenario** dropdown.</span></span> <span data-ttu-id="8b67b-117">템플릿 중 하나를 선택하고 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-117">Select one of the templates and click **Create**.</span></span>

<span data-ttu-id="8b67b-118">기본적으로 HTTP 트리거는 HTTP 200 OK 상태 코드와 비어 있는 본문을 포함한 요청에 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-118">By default, an HTTP trigger will respond to the request with an HTTP 200 OK status code and an empty body.</span></span> <span data-ttu-id="8b67b-119">응답을 수정하려면 [HTTP 바인딩 출력](#output)을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-119">To modify the response, configure an [HTTP output binding](#output)</span></span>

### <a name="configuring-an-http-trigger"></a><span data-ttu-id="8b67b-120">HTTP 트리거 구성</span><span class="sxs-lookup"><span data-stu-id="8b67b-120">Configuring an HTTP trigger</span></span>
<span data-ttu-id="8b67b-121">HTTP 트리거는 function.json의 `bindings` 배열에 다음과 유사한 JSON 개체를 포함하여 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-121">An HTTP trigger is defined by including a JSON object similar to the following in the `bindings` array of function.json:</span></span>

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
<span data-ttu-id="8b67b-122">바인딩에서 지원하는 속성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-122">The binding supports the following properties:</span></span>

* <span data-ttu-id="8b67b-123">**name**: 필수 - 요청 또는 요청 본문의 함수 코드에 사용되는 변수 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-123">**name** : Required - the variable name used in function code for the request or request body.</span></span> <span data-ttu-id="8b67b-124">[코드에서 HTTP 트리거 사용](#httptriggerusage)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8b67b-124">See [Working with an HTTP trigger from code](#httptriggerusage).</span></span>
* <span data-ttu-id="8b67b-125">**type**: 필수 - "httpTrigger"로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-125">**type** : Required - must be set to "httpTrigger".</span></span>
* <span data-ttu-id="8b67b-126">**direction**: 필수 - "in"으로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-126">**direction** : Required - must be set to "in".</span></span>
* <span data-ttu-id="8b67b-127">_authLevel_: 키가 있는 경우 함수를 호출하기 위해 요청에 포함되어야 하는 키를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-127">_authLevel_ : This determines what keys, if any, need to be present on the request in order to invoke the function.</span></span> <span data-ttu-id="8b67b-128">아래의 [키 사용](#keys)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8b67b-128">See [Working with keys](#keys) below.</span></span> <span data-ttu-id="8b67b-129">값은 다음 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-129">The value can be one of the following:</span></span>
    * <span data-ttu-id="8b67b-130">_anonymous_: API 키가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-130">_anonymous_: No API key is required.</span></span>
    * <span data-ttu-id="8b67b-131">_function_: 함수 전용 API 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-131">_function_: A function-specific API key is required.</span></span> <span data-ttu-id="8b67b-132">authLevel 속성 값을 제공하지 않을 경우 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-132">This is the default value if none is provided.</span></span>
    * <span data-ttu-id="8b67b-133">_admin_: 마스터 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-133">_admin_ : The master key is required.</span></span>
* <span data-ttu-id="8b67b-134">**methods**: 함수에서 응답할 HTTP 메서드의 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-134">**methods** : This is an array of the HTTP methods to which the function will respond.</span></span> <span data-ttu-id="8b67b-135">이 속성을 지정하지 않으면 함수에서 모든 HTTP 메서드에 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-135">If not specified, the function will respond to all HTTP methods.</span></span> <span data-ttu-id="8b67b-136">[HTTP 끝점 사용자 지정](#url)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8b67b-136">See [Customizing the HTTP endpoint](#url).</span></span>
* <span data-ttu-id="8b67b-137">**route**: 경로 템플릿을 정의하여 함수에서 응답할 요청 URL을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-137">**route** : This defines the route template, controlling to which request URLs your function will respond.</span></span> <span data-ttu-id="8b67b-138">값을 제공하지 않을 경우 기본값은 `<functionname>`입니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-138">The default value if none is provided is `<functionname>`.</span></span> <span data-ttu-id="8b67b-139">[HTTP 끝점 사용자 지정](#url)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8b67b-139">See [Customizing the HTTP endpoint](#url).</span></span>
* <span data-ttu-id="8b67b-140">**webHookType**: HTTP 트리거가 지정된 공급자의 webhook 수신기(receiver)로 작동하도록 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-140">**webHookType** : This configures the HTTP trigger to act as a webhook reciever for the specified provider.</span></span> <span data-ttu-id="8b67b-141">이 속성을 선택하는 경우 _methods_ 속성을 설정하면 안됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-141">The _methods_ property should not be set if this is chosen.</span></span> <span data-ttu-id="8b67b-142">[webhook에 응답](#hooktrigger)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8b67b-142">See [Responding to webhooks](#hooktrigger).</span></span> <span data-ttu-id="8b67b-143">값은 다음 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-143">The value can be one of the following:</span></span>
    * <span data-ttu-id="8b67b-144">_genericJson_: 특정 공급자를 위한 논리가 없는 범용 webhook 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-144">_genericJson_ : A general purpose webhook endpoint without logic for a specific provider.</span></span>
    * <span data-ttu-id="8b67b-145">_github_: GitHub webhook에 응답하는 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-145">_github_ : The function will respond to GitHub webhooks.</span></span> <span data-ttu-id="8b67b-146">이 값을 선택하는 경우 _authLevel_ 속성을 설정하면 안됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-146">The _authLevel_ property should not be set if this is chosen.</span></span>
    * <span data-ttu-id="8b67b-147">_slack_: Slack webhook에 응답하는 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-147">_slack_ : The function will respond to Slack webhooks.</span></span> <span data-ttu-id="8b67b-148">이 값을 선택하는 경우 _authLevel_ 속성을 설정하면 안됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-148">The _authLevel_ property should not be set if this is chosen.</span></span>

<a name="httptriggerusage"></a>
### <a name="working-with-an-http-trigger-from-code"></a><span data-ttu-id="8b67b-149">코드에서 HTTP 트리거 사용</span><span class="sxs-lookup"><span data-stu-id="8b67b-149">Working with an HTTP trigger from code</span></span>
<span data-ttu-id="8b67b-150">C# 및 F# 함수의 경우 트리거 입력 형식을 `HttpRequestMessage` 또는 사용자 지정 형식으로 선언할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-150">For C# and F# functions, you can declare the type of your trigger input to be either `HttpRequestMessage` or a custom type.</span></span> <span data-ttu-id="8b67b-151">`HttpRequestMessage`를 선택하면 요청 개체에 대한 모든 권한을 갖게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-151">If you choose `HttpRequestMessage`, then you will get full access to the request object.</span></span> <span data-ttu-id="8b67b-152">사용자 지정 형식(예: POCO)의 경우 함수는 요청 본문을 JSON으로 구문 분석하여 개체 속성을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-152">For a custom type (such as a POCO), Functions will attempt to parse the request body as JSON to populate the object properties.</span></span>

<span data-ttu-id="8b67b-153">Node.js 함수의 경우 함수 런타임은 요청 개체 대신 요청 본문을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-153">For Node.js functions, the Functions runtime provides the request body instead of the request object.</span></span>

<span data-ttu-id="8b67b-154">사용 예제는 [HTTP 트리거 샘플](#httptriggersample)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8b67b-154">See [HTTP trigger samples](#httptriggersample) for example usages.</span></span>


<a name="output"></a>
## <a name="http-response-output-binding"></a><span data-ttu-id="8b67b-155">HTTP 응답 출력 바인딩</span><span class="sxs-lookup"><span data-stu-id="8b67b-155">HTTP response output binding</span></span>
<span data-ttu-id="8b67b-156">HTTP 요청 발신기(sender)에 응답하려면 HTTP 출력 바인딩을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-156">Use the HTTP output binding to respond to the HTTP request sender.</span></span> <span data-ttu-id="8b67b-157">이 바인딩에는 HTTP 트리거가 필요하며 트리거 요청과 관련된 응답을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-157">This binding requires an HTTP trigger and allows you to customize the response associated with the trigger's request.</span></span> <span data-ttu-id="8b67b-158">HTTP 출력 바인딩이 제공되지 않으면 HTTP 트리거는 빈 본문과 함께 HTTP 200 OK를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-158">If an HTTP output binding is not provided, an HTTP trigger will return HTTP 200 OK with an empty body.</span></span> 

### <a name="configuring-an-http-output-binding"></a><span data-ttu-id="8b67b-159">HTTP 출력 바인딩 구성</span><span class="sxs-lookup"><span data-stu-id="8b67b-159">Configuring an HTTP output binding</span></span>
<span data-ttu-id="8b67b-160">HTTP 출력 바인딩은 function.json의 `bindings` 배열에 다음과 유사한 JSON 개체를 포함하여 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-160">The HTTP output binding is defined by including a JSON object similar to the following in the `bindings` array of function.json:</span></span>

```json
{
    "name": "res",
    "type": "http",
    "direction": "out"
}
```
<span data-ttu-id="8b67b-161">바인딩에서 포함하는 속성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-161">The binding contains the following properties:</span></span>

* <span data-ttu-id="8b67b-162">**name**: 필수 - 응답의 함수 코드에 사용되는 변수 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-162">**name** : Required - the variable name used in function code for the response.</span></span> <span data-ttu-id="8b67b-163">[코드에서 HTTP 출력 바인딩 사용](#outputusage)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8b67b-163">See [Working with an HTTP output binding from code](#outputusage).</span></span>
* <span data-ttu-id="8b67b-164">**type**: 필수 - "http"로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-164">**type** : Required - must be set to "http".</span></span>
* <span data-ttu-id="8b67b-165">**direction**: 필수 - "out"으로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-165">**direction** : Required - must be set to "out".</span></span>

<a name="outputusage"></a>
### <a name="working-with-an-http-output-binding-from-code"></a><span data-ttu-id="8b67b-166">코드에서 HTTP 출력 바인딩 사용</span><span class="sxs-lookup"><span data-stu-id="8b67b-166">Working with an HTTP output binding from code</span></span>
<span data-ttu-id="8b67b-167">출력 매개 변수(예: "res")를 사용하여 http 또는 webhook 호출기(caller)에 응답할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-167">You can use the output parameter (e.g., "res") to respond to the http or webhook caller.</span></span> <span data-ttu-id="8b67b-168">또는 표준 `Request.CreateResponse()`(C#) 또는 `context.res`(Node.JS) 패턴을 사용하여 응답을 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-168">Alternatively, you can use the standard `Request.CreateResponse()` (C#) or `context.res` (Node.JS) pattern to return your response.</span></span> <span data-ttu-id="8b67b-169">후자의 메서드를 사용하는 방법에 대한 예제는 [HTTP 트리거 샘플](#httptriggersample) 및 [Webhook 트리거 샘플](#hooktriggersample)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8b67b-169">For examples on how to use the latter method, see [HTTP trigger samples](#httptriggersample) and [Webhook trigger samples](#hooktriggersample).</span></span>


<a name="hooktrigger"></a>
## <a name="responding-to-webhooks"></a><span data-ttu-id="8b67b-170">webhook에 응답</span><span class="sxs-lookup"><span data-stu-id="8b67b-170">Responding to webhooks</span></span>
<span data-ttu-id="8b67b-171">_webHookType_ 속성이 있는 HTTP 트리거에서 [webhook](https://en.wikipedia.org/wiki/Webhook)에 응답하도록 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-171">An HTTP trigger with the _webHookType_ property will be configured to respond to [webhooks](https://en.wikipedia.org/wiki/Webhook).</span></span> <span data-ttu-id="8b67b-172">기본 구성에서는 "genericJson" 설정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-172">The basic configuration uses the "genericJson" setting.</span></span> <span data-ttu-id="8b67b-173">이렇게 하면 HTTP POST 및 `application/json` 콘텐츠 형식을 사용하는 요청으로만 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-173">This restricts requests to only those using HTTP POST and with the `application/json` content type.</span></span>

<span data-ttu-id="8b67b-174">또한 트리거는 특정 webhook 공급자(예: [GitHub](https://developer.github.com/webhooks/) 및 [Slack](https://api.slack.com/outgoing-webhooks))에 맞춰 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-174">The trigger can additionally be tailored to a specific webhook provider (e.g., [GitHub](https://developer.github.com/webhooks/) and [Slack](https://api.slack.com/outgoing-webhooks)).</span></span> <span data-ttu-id="8b67b-175">공급자를 지정하면 Functions 런타임에서 공급자의 유효성 검사 논리를 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-175">If a provider is specified, the Functions runtime can take care of the provider's validation logic for you.</span></span>  

### <a name="configuring-github-as-a-webhook-provider"></a><span data-ttu-id="8b67b-176">GitHub를 웹후크 공급자로 구성</span><span class="sxs-lookup"><span data-stu-id="8b67b-176">Configuring GitHub as a webhook provider</span></span>
<span data-ttu-id="8b67b-177">GitHub webhook에 응답하려면 먼저 HTTP 트리거를 사용하여 함수를 만들고 _webHookType_ 속성을 "github"로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-177">To respond to GitHub webhooks, first create your function with an HTTP Trigger, and set the _webHookType_ property to "github".</span></span> <span data-ttu-id="8b67b-178">그런 다음 [URL](#url) 및 [API 키](#keys)를 GitHub 리포지토리의 **webhook 추가** 페이지에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-178">Then copy its [URL](#url) and [API key](#keys) into your GitHub repository's **Add webhook** page.</span></span> <span data-ttu-id="8b67b-179">자세한 내용은 GitHub의 [Webhook 만들기](http://go.microsoft.com/fwlink/?LinkID=761099&clcid=0x409) 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8b67b-179">See GitHub's [Creating Webhooks](http://go.microsoft.com/fwlink/?LinkID=761099&clcid=0x409) documentation for more.</span></span>

![](./media/functions-bindings-http-webhook/github-add-webhook.png)

### <a name="configuring-slack-as-a-webhook-provider"></a><span data-ttu-id="8b67b-180">Slack을 webhook 공급자로 구성</span><span class="sxs-lookup"><span data-stu-id="8b67b-180">Configuring Slack as a webhook provider</span></span>
<span data-ttu-id="8b67b-181">Slack webhook은 함수 전용 키를 지정하는 대신 사용자를 위한 토큰을 생성하므로 Slack의 토큰을 사용하여 함수 전용 키를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-181">The Slack webhook generates a token for you instead of letting you specify it, so you must configure a function-specific key with the token from Slack.</span></span> <span data-ttu-id="8b67b-182">[키 사용](#keys)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8b67b-182">See [Working with keys](#keys).</span></span>

<a name="url"></a>
## <a name="customizing-the-http-endpoint"></a><span data-ttu-id="8b67b-183">HTTP 끝점 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="8b67b-183">Customizing the HTTP endpoint</span></span>
<span data-ttu-id="8b67b-184">기본적으로 HTTP 트리거 또는 WebHook용 함수를 만드는 경우 폼의 경로를 사용하여 이 함수의 주소를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-184">By default when you create a function for an HTTP trigger, or WebHook, the function is addressable with a route of the form:</span></span>

    http://<yourapp>.azurewebsites.net/api/<funcname> 

<span data-ttu-id="8b67b-185">HTTP 트리거의 입력 바인딩에서 선택적 `route` 속성을 사용하여 이 경로를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-185">You can customize this route using the optional `route` property on the HTTP trigger's input binding.</span></span> <span data-ttu-id="8b67b-186">예를 들어 다음 *function.json* 파일은 HTTP 트리거에 대한 `route` 속성을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-186">As an example, the following *function.json* file defines a `route` property for an HTTP trigger:</span></span>

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

<span data-ttu-id="8b67b-187">이 구성을 사용하면 원래 경로 대신 다음 경로를 사용하여 함수의 주소를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-187">Using this configuration, the function is now addressable with the following route instead of the original route.</span></span>

    http://<yourapp>.azurewebsites.net/api/products/electronics/357

<span data-ttu-id="8b67b-188">이렇게 하면 함수 코드에서 주소의 두 매개 변수, "category" 및 "id"를 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-188">This allows the function code to support two parameters in the address, "category" and "id".</span></span> <span data-ttu-id="8b67b-189">매개 변수에서 [웹 API 경로 제약 조건](https://www.asp.net/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2#constraints)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-189">You can use any [Web API Route Constraint](https://www.asp.net/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2#constraints) with your parameters.</span></span> <span data-ttu-id="8b67b-190">다음 C# 함수 코드는 두 매개 변수를 모두 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-190">The following C# function code makes use of both parameters.</span></span>

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

<span data-ttu-id="8b67b-191">다음은 동일한 경로 매개 변수를 사용하는 Node.js 함수 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-191">Here is Node.js function code to use the same route parameters.</span></span>

```javascript
    module.exports = function (context, req) {

        var category = context.bindingData.category;
        var id = context.bindingData.id;

        if (!id) {
            context.res = {
                // status: 200, /* Defaults to 200 */
                body: "All " + category + " items were requested."
            };
        }
        else {
            context.res = {
                // status: 200, /* Defaults to 200 */
                body: category + " item with id = " + id + " was requested."
            };
        }

        context.done();
    } 
```

<span data-ttu-id="8b67b-192">기본적으로 모든 함수 경로에는 *api* 접두사가 붙습니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-192">By default, all function routes are prefixed with *api*.</span></span> <span data-ttu-id="8b67b-193">*host.json* 파일에서 `http.routePrefix` 속성을 사용하여 접두사를 사용자 지정하거나 제거할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-193">You can also customize or remove the prefix using the `http.routePrefix` property in your *host.json* file.</span></span> <span data-ttu-id="8b67b-194">다음 예제에서는 *host.json* 파일에서 빈 문자열을 접두사로 사용하여 *api* 경로 접두사를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-194">The following example removes the *api* route prefix by using an empty string for the prefix in the *host.json* file.</span></span>

```json
    {
      "http": {
        "routePrefix": ""
      }
    }
```

<span data-ttu-id="8b67b-195">함수의 *host.json* 파일을 업데이트하는 방법에 대한 자세한 내용은 [함수 앱 파일을 업데이트하는 방법](functions-reference.md#fileupdate)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8b67b-195">For detailed information on how to update the *host.json* file for your function, See, [How to update function app files](functions-reference.md#fileupdate).</span></span> 

<span data-ttu-id="8b67b-196">*host.json* 파일에서 구성할 수 있는 다른 속성에 대한 자세한 내용은 [host.json 참조](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8b67b-196">For information on other properties you can configure in your *host.json* file, see [host.json reference](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span>


<a name="keys"></a>
## <a name="working-with-keys"></a><span data-ttu-id="8b67b-197">키 사용</span><span class="sxs-lookup"><span data-stu-id="8b67b-197">Working with keys</span></span>
<span data-ttu-id="8b67b-198">HttpTriggers는 보안 강화를 위해 키를 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-198">HttpTriggers can leverage keys for added security.</span></span> <span data-ttu-id="8b67b-199">표준 HttpTrigger에서 이러한 키는 API 키로 사용될 수 있으므로 요청 시에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-199">A standard HttpTrigger can use these as an API key, requiring the key to be present on the request.</span></span> <span data-ttu-id="8b67b-200">Webhooks에서는 공급자가 지원하는 항목에 따라 다양한 방식으로 요청을 인증하는 데 키를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-200">Webhooks can use keys to authorize requests in a variety of ways, depending on what the provider supports.</span></span>

<span data-ttu-id="8b67b-201">키는 Azure에 함수 앱의 일부로 저장되며 나머지는 암호화되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-201">Keys are stored as part of your function app in Azure and are encrypted at rest.</span></span> <span data-ttu-id="8b67b-202">키를 보거나, 새 키를 만들거나, 키를 새 값으로 전환하려면 포털에 있는 함수 중 하나를 탐색하여 [관리]를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-202">To view your keys, create new ones, or roll keys to new values, navigate to one of your functions within the portal and select "Manage."</span></span> 

<span data-ttu-id="8b67b-203">다음과 같이 두 가지 유형의 키가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-203">There are two types of keys:</span></span>
- <span data-ttu-id="8b67b-204">**호스트 키**: 함수 앱 내의 모든 함수에서 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-204">**Host keys**: These keys are shared by all functions within the function app.</span></span> <span data-ttu-id="8b67b-205">API 키로 사용되면 이 키를 통해 함수 앱 내의 모든 함수에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-205">When used as an API key, these allow access to any function within the function app.</span></span>
- <span data-ttu-id="8b67b-206">**function 키**: 정의된 특정 함수에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-206">**Function keys**: These keys apply only to the specific functions under which they are defined.</span></span> <span data-ttu-id="8b67b-207">API 키로 사용되면 이 키를 통해 해당 함수에만 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-207">When used as an API key, these only allow access to that function.</span></span>

<span data-ttu-id="8b67b-208">각 키의 이름은 참조될 수 있도록 지정되며 함수 및 호스트 수준에서는 "default"라는 기본 키가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-208">Each key is named for reference, and there is a default key (named "default") at the function and host level.</span></span> <span data-ttu-id="8b67b-209">**master 키**는 각 함수 앱에 대해 정의하고 취소할 수 없는 "_master"라는 기본 호스트 키입니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-209">The **master key** is a default host key named "_master" that is defined for each function app and cannot be revoked.</span></span> <span data-ttu-id="8b67b-210">런타임 API에 대한 관리 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-210">It provides administrative access to the runtime APIs.</span></span> <span data-ttu-id="8b67b-211">바인딩 JSON에서 `"authLevel": "admin"`을 사용하면 요청 시 이 키가 필요합니다. 다른 키는 권한 부여 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-211">Using `"authLevel": "admin"` in the binding JSON will require this key to be presented on the request; any other key will result in a authorization failure.</span></span>

> [!NOTE]
> <span data-ttu-id="8b67b-212">master 키에서 부여하는 승격된 권한으로 인해 이 키를 타사와 공유하거나 네이티브 클라이언트 응용 프로그램에 배포해서는 안됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-212">Due to the elevated permissions granted by the master key, you should not share this key with third parties or distribute it in native client applications.</span></span> <span data-ttu-id="8b67b-213">따라서 관리자 권한 부여 수준을 선택할 때는 주의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-213">Exercise caution when choosing the admin authorization level.</span></span>
> 
> 

### <a name="api-key-authorization"></a><span data-ttu-id="8b67b-214">API 키 권한 부여</span><span class="sxs-lookup"><span data-stu-id="8b67b-214">API key authorization</span></span>
<span data-ttu-id="8b67b-215">기본적으로 HttpTrigger는 HTTP 요청에서 API 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-215">By default, an HttpTrigger requires an API key in the HTTP request.</span></span> <span data-ttu-id="8b67b-216">따라서 HTTP 요청은 일반적으로 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-216">So your HTTP request normally looks like this:</span></span>

    https://<yourapp>.azurewebsites.net/api/<function>?code=<ApiKey>

<span data-ttu-id="8b67b-217">키는 위와 같이 `code`라는 쿼리 문자열 변수에 포함되거나 `x-functions-key` HTTP 헤더에 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-217">The key can be included in a query string variable named `code`, as above, or it can be included in an `x-functions-key` HTTP header.</span></span> <span data-ttu-id="8b67b-218">키 값은 함수에 대해 정의된 모든 function 키 또는 모든 호스트 키일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-218">The value of the key can be any function key defined for the function, or any host key.</span></span>

<span data-ttu-id="8b67b-219">키가 없는 요청을 허용하도록 선택하거나 바인딩 JSON([HTTP 트리거](#httptrigger) 참조)에서 `authLevel` 속성을 변경하여 master 키를 사용해야 한다고 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-219">You can choose to allow requests without keys or specify that the master key must be used by changing the `authLevel` property in the binding JSON (see [HTTP trigger](#httptrigger)).</span></span>

### <a name="keys-and-webhooks"></a><span data-ttu-id="8b67b-220">키 및 webhook</span><span class="sxs-lookup"><span data-stu-id="8b67b-220">Keys and webhooks</span></span>
<span data-ttu-id="8b67b-221">Webhook 인증은 HttpTrigger의 일부로 Webhook 수신기 구성 요소에서 처리하며 메커니즘은 Webhook 유형에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-221">Webhook authorization is handled by the webhook reciever component, part of the HttpTrigger, and the mechanism varies based on the webhook type.</span></span> <span data-ttu-id="8b67b-222">그러나 각 메커니즘마다 키를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-222">Each mechanism does, however rely on a key.</span></span> <span data-ttu-id="8b67b-223">기본적으로 "default"라는 function 키가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-223">By default, the function key named "default" will be used.</span></span> <span data-ttu-id="8b67b-224">다른 키를 사용하려면 다음 중 한 가지 방법으로 요청과 함께 키 이름을 보내도록 webhook 공급자를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-224">If you wish to use a different key, you will need to configure the webhook provider to send the key name with the request in one of the following ways:</span></span>

- <span data-ttu-id="8b67b-225">**쿼리 문자열**: 공급자에서 `clientid` 쿼리 문자열 매개 변수에 키 이름을 전달합니다(예제: `https://<yourapp>.azurewebsites.net/api/<funcname>?clientid=<keyname>`).</span><span class="sxs-lookup"><span data-stu-id="8b67b-225">**Query string**: The provider passes the key name in the `clientid` query string parameter (e.g., `https://<yourapp>.azurewebsites.net/api/<funcname>?clientid=<keyname>`).</span></span>
- <span data-ttu-id="8b67b-226">**요청 헤더**: 공급자에서 `x-functions-clientid` 헤더에 키 이름을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-226">**Request header**: The provider passes the key name in the `x-functions-clientid` header.</span></span>

> [!NOTE]
> <span data-ttu-id="8b67b-227">function 키는 호스트 키보다 우선합니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-227">Function keys take precedence over host keys.</span></span> <span data-ttu-id="8b67b-228">두 키가 동일한 이름으로 정의되면 function 키가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-228">If two keys are defined with the same name, the function key will be used.</span></span>
> 
> 


<a name="httptriggersample"></a>
## <a name="http-trigger-samples"></a><span data-ttu-id="8b67b-229">HTTP 트리거 샘플</span><span class="sxs-lookup"><span data-stu-id="8b67b-229">HTTP trigger samples</span></span>
<span data-ttu-id="8b67b-230">function.json의 `bindings` 배열에 다음과 같은 HTTP 트리거가 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-230">Suppose you have the following HTTP trigger in the `bindings` array of function.json:</span></span>

```json
{
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
    "authLevel": "function"
},
```

<span data-ttu-id="8b67b-231">쿼리 문자열 또는 HTTP 요청 본문에서 `name` 매개 변수를 찾는 언어 특정 샘플을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8b67b-231">See the language-specific sample that looks for a `name` parameter either in the query string or the body of the HTTP request.</span></span>

* [<span data-ttu-id="8b67b-232">C#</span><span class="sxs-lookup"><span data-stu-id="8b67b-232">C#</span></span>](#httptriggercsharp)
* [<span data-ttu-id="8b67b-233">F#</span><span class="sxs-lookup"><span data-stu-id="8b67b-233">F#</span></span>](#httptriggerfsharp)
* [<span data-ttu-id="8b67b-234">Node.JS</span><span class="sxs-lookup"><span data-stu-id="8b67b-234">Node.js</span></span>](#httptriggernodejs)


<a name="httptriggercsharp"></a>
### <a name="http-trigger-sample-in-c"></a><span data-ttu-id="8b67b-235">C#의 HTTP 트리거 샘플</span><span class="sxs-lookup"><span data-stu-id="8b67b-235">HTTP trigger sample in C#</span></span> #
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

    // Set name to query string or body data
    name = name ?? data?.name;

    return name == null
        ? req.CreateResponse(HttpStatusCode.BadRequest, "Please pass a name on the query string or in the request body")
        : req.CreateResponse(HttpStatusCode.OK, "Hello " + name);
}
```

<span data-ttu-id="8b67b-236">`HttpRequestMessage` 대신 POCO에 바인딩할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-236">You can also bind to a POCO instead of `HttpRequestMessage`.</span></span> <span data-ttu-id="8b67b-237">이 샘플은 요청 본문에서 하이드레이션되고 JSON으로 구문 분석됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-237">This will be hydrated from the body of the request, parsed as JSON.</span></span> <span data-ttu-id="8b67b-238">마찬가지로, 형식을 HTTP 응답 출력 바인딩으로 전달할 수도 있습니다. 그러면 200 상태 코드를 갖는 응답 본문으로 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-238">Similarly, a type can be passed to the HTTP response output binding, and this will be returned as the response body, with a 200 status code.</span></span>
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
### <a name="http-trigger-sample-in-f"></a><span data-ttu-id="8b67b-239">F#의 HTTP 트리거 샘플</span><span class="sxs-lookup"><span data-stu-id="8b67b-239">HTTP trigger sample in F#</span></span> #
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
                return req.CreateErrorResponse(HttpStatusCode.BadRequest, "Please pass a name on the query string or in the request body")
    } |> Async.StartAsTask
```

<span data-ttu-id="8b67b-240">다음과 같이 NuGet을 사용하여 `FSharp.Interop.Dynamic` 및 `Dynamitey` 어셈블리를 참조하는 `project.json` 파일이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-240">You need a `project.json` file that uses NuGet to reference the `FSharp.Interop.Dynamic` and `Dynamitey` assemblies, like this:</span></span>

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

<span data-ttu-id="8b67b-241">그러면 NuGet을 사용하여 종속성을 가져오고 스크립트에서 해당 항목을 참조하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-241">This will use NuGet to fetch your dependencies and will reference them in your script.</span></span>

<a name="httptriggernodejs"></a>
### <a name="http-trigger-sample-in-nodejs"></a><span data-ttu-id="8b67b-242">Node.js의 트리거 샘플</span><span class="sxs-lookup"><span data-stu-id="8b67b-242">HTTP trigger sample in Node.JS</span></span>
```javascript
module.exports = function(context, req) {
    context.log('Node.js HTTP trigger function processed a request. RequestUri=%s', req.originalUrl);

    if (req.query.name || (req.body && req.body.name)) {
        context.res = {
            // status: 200, /* Defaults to 200 */
            body: "Hello " + (req.query.name || req.body.name)
        };
    }
    else {
        context.res = {
            status: 400,
            body: "Please pass a name on the query string or in the request body"
        };
    }
    context.done();
};
```



<a name="hooktriggersample"></a>
## <a name="webhook-samples"></a><span data-ttu-id="8b67b-243">Webhook 샘플</span><span class="sxs-lookup"><span data-stu-id="8b67b-243">Webhook samples</span></span>
<span data-ttu-id="8b67b-244">function.json의 `bindings` 배열에 다음과 같은 webhook 트리거가 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="8b67b-244">Suppose you have the following webhook trigger in the `bindings` array of function.json:</span></span>

```json
{
    "webHookType": "github",
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
},
```

<span data-ttu-id="8b67b-245">GitHub 문제 설명을 기록하는 언어 특정 샘플을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8b67b-245">See the language-specific sample that logs GitHub issue comments.</span></span>

* [<span data-ttu-id="8b67b-246">C#</span><span class="sxs-lookup"><span data-stu-id="8b67b-246">C#</span></span>](#hooktriggercsharp)
* [<span data-ttu-id="8b67b-247">F#</span><span class="sxs-lookup"><span data-stu-id="8b67b-247">F#</span></span>](#hooktriggerfsharp)
* [<span data-ttu-id="8b67b-248">Node.JS</span><span class="sxs-lookup"><span data-stu-id="8b67b-248">Node.js</span></span>](#hooktriggernodejs)

<a name="hooktriggercsharp"></a>

### <a name="webhook-sample-in-c"></a><span data-ttu-id="8b67b-249">C#의 웹후크 샘플</span><span class="sxs-lookup"><span data-stu-id="8b67b-249">Webhook sample in C#</span></span> #
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

### <a name="webhook-sample-in-f"></a><span data-ttu-id="8b67b-250">F#의 웹후크 샘플</span><span class="sxs-lookup"><span data-stu-id="8b67b-250">Webhook sample in F#</span></span> #
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

### <a name="webhook-sample-in-nodejs"></a><span data-ttu-id="8b67b-251">Node.JS의 Webhook 샘플</span><span class="sxs-lookup"><span data-stu-id="8b67b-251">Webhook sample in Node.JS</span></span>
```javascript
module.exports = function (context, data) {
    context.log('GitHub WebHook triggered!', data.comment.body);
    context.res = { body: 'New GitHub comment: ' + data.comment.body };
    context.done();
};
```


## <a name="next-steps"></a><span data-ttu-id="8b67b-252">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8b67b-252">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]


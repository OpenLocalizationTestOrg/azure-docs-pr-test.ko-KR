---
title: "Azure 함수를 사용 하는 서버가 없는 API aaaCreate | Microsoft Docs"
description: "어떻게 toocreate Azure 함수를 사용 하는 서버가 없는 API"
services: functions
author: mattchenderson
manager: erikre
ms.service: functions
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: tutorial
ms.date: 05/04/2017
ms.author: mahender
ms.custom: mvc
ms.openlocfilehash: 877e3b229d5477fc5fec594ccd284fb55d7f3c07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-serverless-api-using-azure-functions"></a><span data-ttu-id="b28f8-103">Azure Functions를 사용하여 서버 없는 API 만들기</span><span class="sxs-lookup"><span data-stu-id="b28f8-103">Create a serverless API using Azure Functions</span></span>

<span data-ttu-id="b28f8-104">이 자습서에 설명 합니다 방법을 Azure 함수 사용 하면 toobuild 고도로 확장 가능한 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-104">In this tutorial you will learn how Azure Functions allows you toobuild highly-scalable APIs.</span></span> <span data-ttu-id="b28f8-105">Azure 함수는 다양 한 언어로, Node.JS, C# 등을 포함 하 여 끝점의 기본 제공 HTTP 트리거 및 쉽게 tooauthor 하도록 하는 바인딩 컬렉션 함께 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-105">Azure Functions comes with a collection of built-in HTTP triggers and bindings which make it easy tooauthor an endpoint in a variety of languages, including Node.JS, C#, and more.</span></span> <span data-ttu-id="b28f8-106">이 자습서에서는 API 디자인에 HTTP 트리거 toohandle 특정 작업을 사용자 지정 하면 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-106">In this tutorial, you will customize an HTTP trigger toohandle specific actions in your API design.</span></span> <span data-ttu-id="b28f8-107">또한 Azure Functions 프록시와 통합하고 모의 API를 설정하여 API를 확장할 준비를 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-107">You will also prepare for growing your API by integrating it with Azure Functions Proxies and setting up mock APIs.</span></span> <span data-ttu-id="b28f8-108">이 모든는 리소스 확장에 대 한 tooworry 없는-API 논리에만 집중할 수 있도록 hello 함수 서버가 없는 계산 환경을 기반으로 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-108">All of this is accomplished on top of hello Functions serverless compute environment, so you don't have tooworry about scaling resources - you can just focus on your API logic.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b28f8-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b28f8-109">Prerequisites</span></span> 

[!INCLUDE [Previous quickstart note](../../includes/functions-quickstart-previous-topics.md)]

<span data-ttu-id="b28f8-110">이 자습서의 나머지 부분 hello에 대 한 hello 결과 함수가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-110">hello resulting function will be used for hello rest of this tutorial.</span></span>

### <a name="sign-in-tooazure"></a><span data-ttu-id="b28f8-111">TooAzure에 로그인</span><span class="sxs-lookup"><span data-stu-id="b28f8-111">Sign in tooAzure</span></span>

<span data-ttu-id="b28f8-112">Azure 포털 hello를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-112">Open hello Azure portal.</span></span> <span data-ttu-id="b28f8-113">toodo이 너무 로그인[https://portal.azure.com](https://portal.azure.com) Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="b28f8-113">toodo this, sign in too[https://portal.azure.com](https://portal.azure.com) with your Azure account.</span></span>

## <a name="customize-your-http-function"></a><span data-ttu-id="b28f8-114">HTTP 함수 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="b28f8-114">Customize your HTTP function</span></span>

<span data-ttu-id="b28f8-115">기본적으로 HTTP 트리거 함수는 구성 된 tooaccept 모든 HTTP 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-115">By default, your HTTP-triggered function is configured tooaccept any HTTP method.</span></span> <span data-ttu-id="b28f8-116">Hello 폼의 기본 URL은 또한 `http://<yourapp>.azurewebsites.net/api/<funcname>?code=<functionkey>`합니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-116">There is also a default URL of hello form `http://<yourapp>.azurewebsites.net/api/<funcname>?code=<functionkey>`.</span></span> <span data-ttu-id="b28f8-117">다음 hello 퀵 스타트를 따른 경우 `<funcname>` "HttpTriggerJS1" 같은 내용이 보일 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-117">If you followed hello quickstart, then `<funcname>` probably looks something like "HttpTriggerJS1".</span></span> <span data-ttu-id="b28f8-118">이 섹션에서는 hello에 대 한 함수 toorespond만 tooGET 요청을 수정 합니다 `/api/hello` 대신 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-118">In this section, you will modify hello function toorespond only tooGET requests against `/api/hello` route instead.</span></span> 

<span data-ttu-id="b28f8-119">Hello Azure 포털에서에서 tooyour 함수를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-119">Navigate tooyour function in hello Azure portal.</span></span> <span data-ttu-id="b28f8-120">선택 **통합** 왼쪽 탐색 hello에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-120">Select **Integrate** in hello left navigation.</span></span>

![HTTP 함수 사용자 지정](./media/functions-create-serverless-api/customizing-http.png)

<span data-ttu-id="b28f8-122">Hello 테이블에 지정 된 HTTP 트리거 설정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-122">Use the HTTP trigger settings as specified in hello table.</span></span>

| <span data-ttu-id="b28f8-123">필드</span><span class="sxs-lookup"><span data-stu-id="b28f8-123">Field</span></span> | <span data-ttu-id="b28f8-124">샘플 값</span><span class="sxs-lookup"><span data-stu-id="b28f8-124">Sample value</span></span> | <span data-ttu-id="b28f8-125">설명</span><span class="sxs-lookup"><span data-stu-id="b28f8-125">Description</span></span> |
|---|---|---|
| <span data-ttu-id="b28f8-126">허용된 HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="b28f8-126">Allowed HTTP methods</span></span> | <span data-ttu-id="b28f8-127">선택된 메서드</span><span class="sxs-lookup"><span data-stu-id="b28f8-127">Selected methods</span></span> | <span data-ttu-id="b28f8-128">HTTP 메서드를 사용 하는 tooinvoke 수 판단한이 함수</span><span class="sxs-lookup"><span data-stu-id="b28f8-128">Determines what HTTP methods may be used tooinvoke this function</span></span> |
| <span data-ttu-id="b28f8-129">선택한 HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="b28f8-129">Selected HTTP methods</span></span> | <span data-ttu-id="b28f8-130">GET</span><span class="sxs-lookup"><span data-stu-id="b28f8-130">GET</span></span> | <span data-ttu-id="b28f8-131">통해 선택 된 HTTP 메서드 toobe만 tooinvoke를이 함수 사용</span><span class="sxs-lookup"><span data-stu-id="b28f8-131">Allows only selected HTTP methods toobe used tooinvoke this function</span></span> |
| <span data-ttu-id="b28f8-132">경로 템플릿</span><span class="sxs-lookup"><span data-stu-id="b28f8-132">Route template</span></span> | <span data-ttu-id="b28f8-133">/hello</span><span class="sxs-lookup"><span data-stu-id="b28f8-133">/hello</span></span> | <span data-ttu-id="b28f8-134">경로 사용 되는 tooinvoke 결정이 함수</span><span class="sxs-lookup"><span data-stu-id="b28f8-134">Determines what route is used tooinvoke this function</span></span> |

<span data-ttu-id="b28f8-135">Hello 포함 되지 않은 `/api` 이 전역 설정에 의해 처리 되므로 hello 경로 서식 파일의 경로 접두사를 기반 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-135">Note that you did not include hello `/api` base path prefix in hello route template, as this is handled by a global setting.</span></span>

<span data-ttu-id="b28f8-136">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-136">Click **Save**.</span></span>

<span data-ttu-id="b28f8-137">[Azure Functions HTTP 및 웹후크 바인딩](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#customizing-the-http-endpoint)에서 HTTP 함수 사용자 지정에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="b28f8-137">You can learn more about customizing HTTP functions in [Azure Functions HTTP and webhook bindings](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#customizing-the-http-endpoint).</span></span>

### <a name="test-your-api"></a><span data-ttu-id="b28f8-138">API 테스트</span><span class="sxs-lookup"><span data-stu-id="b28f8-138">Test your API</span></span>

<span data-ttu-id="b28f8-139">다음으로 테스트 함수 toosee hello 새 API 화면을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-139">Next, test your function toosee it working with hello new API surface.</span></span>

<span data-ttu-id="b28f8-140">왼쪽 탐색 hello에 hello 함수 이름을 클릭 하 여 뒤로 toohello 개발 페이지를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-140">Navigate back toohello development page by clicking on hello function's name in hello left navigation.</span></span>

<span data-ttu-id="b28f8-141">클릭 **함수 URL을 가져올** hello URL을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-141">Click **Get function URL** and copy hello URL.</span></span> <span data-ttu-id="b28f8-142">Hello를 사용 하도록 표시 되어야 `/api/hello` 이제 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-142">You should see that it uses hello `/api/hello` route now.</span></span>

<span data-ttu-id="b28f8-143">새 브라우저 탭 또는 기본 REST 클라이언트 hello URL을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-143">Copy hello URL into a new browser tab or your preferred REST client.</span></span> <span data-ttu-id="b28f8-144">브라우저는 기본적으로 GET을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-144">Browsers will use GET by default.</span></span>

<span data-ttu-id="b28f8-145">Hello 함수를 실행 하 고 작동 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-145">Run hello function and confirm that it is working.</span></span> <span data-ttu-id="b28f8-146">쿼리 문자열 toosatisfy hello 빠른 시작 코드와 tooprovide hello "name" 매개 변수를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-146">You may need tooprovide hello "name" parameter as a query string toosatisfy hello quickstart code.</span></span>

<span data-ttu-id="b28f8-147">다른 HTTP 메서드에 tooconfirm hello 함수 실행 되지 않도록 있는 hello 끝점 호출을 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-147">You can also try calling hello endpoint with another HTTP method tooconfirm that hello function is not executed.</span></span> <span data-ttu-id="b28f8-148">이 경우 toouse cURL, 우체부, 또는 Fiddler와 같은 REST 클라이언트에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-148">For this, you will need toouse a REST client, such as cURL, Postman, or Fiddler.</span></span>

## <a name="proxies-overview"></a><span data-ttu-id="b28f8-149">프록시 개요</span><span class="sxs-lookup"><span data-stu-id="b28f8-149">Proxies overview</span></span>

<span data-ttu-id="b28f8-150">Hello 다음 섹션에서 프록시를 통해 API를 노출할 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-150">In hello next section, you will surface your API through a proxy.</span></span> <span data-ttu-id="b28f8-151">Azure 함수 프록시는 tooforward 요청 tooother 리소스 수 있는 미리 보기 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-151">Azure Functions Proxies is a preview feature that allows you tooforward requests tooother resources.</span></span> <span data-ttu-id="b28f8-152">HTTP 트리거가 있는 것과 마찬가지로 HTTP 끝점을 정의 하지만 URL tooa 원격 구현으로 지정 하면 해당 끝점에서 호출 될 때 코드 tooexecute를 작성 하는 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-152">You define an HTTP endpoint just like with HTTP trigger, but instead of writing code tooexecute when that endpoint is called, you provide a URL tooa remote implementation.</span></span> <span data-ttu-id="b28f8-153">이렇게 하면 클라이언트 tooconsume에 대 한 쉬운 단일 API 화면에 여러 API 원본 toocompose 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-153">This allows you toocompose multiple API sources into a single API surface which is easy for clients tooconsume.</span></span> <span data-ttu-id="b28f8-154">Toobuild microservices로 API를 하려는 경우 특히 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-154">This is particularly useful if you wish toobuild your API as microservices.</span></span>

<span data-ttu-id="b28f8-155">프록시는와 같은 tooany HTTP 리소스를 가리킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-155">A proxy can point tooany HTTP resource, such as:</span></span>
- <span data-ttu-id="b28f8-156">Azure 기능</span><span class="sxs-lookup"><span data-stu-id="b28f8-156">Azure Functions</span></span> 
- <span data-ttu-id="b28f8-157">[Azure App Service](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is)의 API 앱</span><span class="sxs-lookup"><span data-stu-id="b28f8-157">API apps in [Azure App Service](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is)</span></span>
- <span data-ttu-id="b28f8-158">[Linux의 App Service](https://docs.microsoft.com/azure/app-service/app-service-linux-readme)에 있는 Docker 컨테이너</span><span class="sxs-lookup"><span data-stu-id="b28f8-158">Docker containers in [App Service on Linux](https://docs.microsoft.com/azure/app-service/app-service-linux-readme)</span></span>
- <span data-ttu-id="b28f8-159">기타 호스트된 API</span><span class="sxs-lookup"><span data-stu-id="b28f8-159">Any other hosted API</span></span>

<span data-ttu-id="b28f8-160">프록시에 대해 자세히 toolearn 참조 [Azure 함수 프록시 (미리 보기) 작업]합니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-160">toolearn more about proxies, see [Working with Azure Functions Proxies (preview)].</span></span>

## <a name="create-your-first-proxy"></a><span data-ttu-id="b28f8-161">첫 번째 프록시 만들기</span><span class="sxs-lookup"><span data-stu-id="b28f8-161">Create your first proxy</span></span>

<span data-ttu-id="b28f8-162">이 섹션에서는 새 프록시 사용으로 만들어 프런트 엔드 tooyour 전체 API입니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-162">In this section, you will create a new proxy which serves as a frontend tooyour overall API.</span></span> 

### <a name="setting-up-hello-frontend-environment"></a><span data-ttu-id="b28f8-163">Hello 프런트 엔드 환경 설정</span><span class="sxs-lookup"><span data-stu-id="b28f8-163">Setting up hello frontend environment</span></span>

<span data-ttu-id="b28f8-164"> ° ט hello 너무[함수 앱 만들기](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function#create-a-function-app) toocreate 새 함수 응용 프로그램 프록시 만들 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-164">Repeat hello steps too[Create a function app](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function#create-a-function-app) toocreate a new function app in which you will create your proxy.</span></span> <span data-ttu-id="b28f8-165">이 새 응용 프로그램 역할을 수행 hello 프런트 엔드 우리의 API에 대 한 하며 이전에 편집 중이 던 hello 함수 앱 백 엔드 역할을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-165">This new app will serve as hello frontend for our API, and hello function app you were previously editing will serve as a backend.</span></span>

<span data-ttu-id="b28f8-166">Tooyour 새 프런트 엔드 함수 앱 hello 포털에서 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-166">Navigate tooyour new frontend function app in hello portal.</span></span>

<span data-ttu-id="b28f8-167">**설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-167">Select **Settings**.</span></span> <span data-ttu-id="b28f8-168">다음 설정/해제 **사용 Azure 함수 프록시 (미리 보기)** 너무 "On"입니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-168">Then toggle **Enable Azure Functions Proxies (preview)** too"On".</span></span>

<span data-ttu-id="b28f8-169">**플랫폼 설정**을 선택하고 **응용 프로그램 설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-169">Select **Platform Settings** and choose **Application Settings**.</span></span>

<span data-ttu-id="b28f8-170">너무 아래로 스크롤하여**앱 설정** "HELLO_HOST" 키를 가진 새 설정을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-170">Scroll down too**App settings** and create a new setting with key "HELLO_HOST".</span></span> <span data-ttu-id="b28f8-171">와 같은 백 엔드 함수 응용 프로그램의 해당 값 toohello 호스트 설정 `<YourApp>.azurewebsites.net`합니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-171">Set its value toohello host of your backend function app, such as `<YourApp>.azurewebsites.net`.</span></span> <span data-ttu-id="b28f8-172">HTTP 기능을 테스트할 때 앞에서 복사한 hello URL의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-172">This is part of hello URL that you copied earlier when testing your HTTP function.</span></span> <span data-ttu-id="b28f8-173">Hello 구성 나중에이 설정을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-173">You'll reference this setting in hello configuration later.</span></span>

> [!NOTE] 
> <span data-ttu-id="b28f8-174">응용 프로그램 설정은 hello 프록시에 대 한 환경 하드 코드 된 종속성 hello 호스트 구성 tooprevent에 권장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-174">App settings are recommended for hello host configuration tooprevent a hard-coded environment dependency for hello proxy.</span></span> <span data-ttu-id="b28f8-175">응용 프로그램 설정을 사용 하 여 있음을 나타내고 hello 프록시 구성을 환경 간에 이동할 수 hello 환경 관련 응용 프로그램 설정이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-175">Using app settings means that you can move hello proxy configuration between environments, and hello environment-specific app settings will be applied.</span></span>

<span data-ttu-id="b28f8-176">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-176">Click **Save**.</span></span>

### <a name="creating-a-proxy-on-hello-frontend"></a><span data-ttu-id="b28f8-177">Hello 프런트 엔드에는 프록시를 만들고</span><span class="sxs-lookup"><span data-stu-id="b28f8-177">Creating a proxy on hello frontend</span></span>

<span data-ttu-id="b28f8-178">Hello 포털에서 뒤로 tooyour 프런트 엔드 함수 응용 프로그램을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-178">Navigate back tooyour frontend function app in hello portal.</span></span>

<span data-ttu-id="b28f8-179">Hello 왼쪽 탐색 hello '+' 다음 더하기 기호를 너무 클릭 "프록시 (미리 보기)"입니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-179">In hello left-hand navigation, click hello plus sign '+' next too"Proxies (preview)".</span></span>

![프록시 만들기](./media/functions-create-serverless-api/creating-proxy.png)

<span data-ttu-id="b28f8-181">Hello 테이블에 지정 된 프록시 설정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-181">Use proxy settings as specified in hello table.</span></span>

| <span data-ttu-id="b28f8-182">필드</span><span class="sxs-lookup"><span data-stu-id="b28f8-182">Field</span></span> | <span data-ttu-id="b28f8-183">샘플 값</span><span class="sxs-lookup"><span data-stu-id="b28f8-183">Sample value</span></span> | <span data-ttu-id="b28f8-184">설명</span><span class="sxs-lookup"><span data-stu-id="b28f8-184">Description</span></span> |
|---|---|---|
| <span data-ttu-id="b28f8-185">이름</span><span class="sxs-lookup"><span data-stu-id="b28f8-185">Name</span></span> | <span data-ttu-id="b28f8-186">HelloProxy</span><span class="sxs-lookup"><span data-stu-id="b28f8-186">HelloProxy</span></span> | <span data-ttu-id="b28f8-187">관리에 대해서만 사용되는 이름</span><span class="sxs-lookup"><span data-stu-id="b28f8-187">A friendly name used only for management</span></span> |
| <span data-ttu-id="b28f8-188">경로 템플릿</span><span class="sxs-lookup"><span data-stu-id="b28f8-188">Route template</span></span> | <span data-ttu-id="b28f8-189">/api/hello</span><span class="sxs-lookup"><span data-stu-id="b28f8-189">/api/hello</span></span> | <span data-ttu-id="b28f8-190">경로 사용 되는 tooinvoke 결정이 프록시</span><span class="sxs-lookup"><span data-stu-id="b28f8-190">Determines what route is used tooinvoke this proxy</span></span> |
| <span data-ttu-id="b28f8-191">백 엔드 URL</span><span class="sxs-lookup"><span data-stu-id="b28f8-191">Backend URL</span></span> | <span data-ttu-id="b28f8-192">https://%HELLO_HOST%/api/hello</span><span class="sxs-lookup"><span data-stu-id="b28f8-192">https://%HELLO_HOST%/api/hello</span></span> | <span data-ttu-id="b28f8-193">Hello 끝점 toowhich hello 요청 프록시 되어야 지정</span><span class="sxs-lookup"><span data-stu-id="b28f8-193">Specifies hello endpoint toowhich hello request should be proxied</span></span> |

<span data-ttu-id="b28f8-194">프록시 hello를 제공 하지 않는 `/api` 기본 경로 접두사와 hello 경로 템플릿을에 포함 해야이 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-194">Note that Proxies does not provide hello `/api` base path prefix, and this must be included in hello route template.</span></span>

<span data-ttu-id="b28f8-195">hello `%HELLO_HOST%` 구문 앞에서 만든 hello 응용 프로그램 설정을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-195">hello `%HELLO_HOST%` syntax will reference hello app setting you created earlier.</span></span> <span data-ttu-id="b28f8-196">hello 확인 URL은 tooyour 원래 함수를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-196">hello resolved URL will point tooyour original function.</span></span>

<span data-ttu-id="b28f8-197">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-197">Click **Create**.</span></span>

<span data-ttu-id="b28f8-198">새 프록시 hello 프록시 URL을 복사 하 고 테스트 hello 브라우저 또는에서 자주 사용 하 여 HTTP 클라이언트와 여 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-198">You can try out your new proxy by copying hello Proxy URL and testing it in hello browser or with your favorite HTTP client.</span></span>

## <a name="create-a-mock-api"></a><span data-ttu-id="b28f8-199">모의 API 만들기</span><span class="sxs-lookup"><span data-stu-id="b28f8-199">Create a mock API</span></span>

<span data-ttu-id="b28f8-200">다음으로, 솔루션에 대 한 프록시 toocreate 모의 API를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-200">Next, you will use a proxy toocreate a mock API for your solution.</span></span> <span data-ttu-id="b28f8-201">이렇게 하면 클라이언트 개발 tooprogress 완전히 구현 하는 hello 백 엔드 몰라도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-201">This allows client development tooprogress, without needing hello backend fully implemented.</span></span> <span data-ttu-id="b28f8-202">개발의 뒷부분에 나오는이 논리를 지원 하는 새 함수 앱을 만들고 프록시 tooit 리디렉션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-202">Later in development, you could create a new function app which supports this logic and redirect your proxy tooit.</span></span>

<span data-ttu-id="b28f8-203">toocreate이 API의 모의 알림, 새 프록시 hello를 사용 하 여이 시간 만듭니다 [응용 프로그램 서비스 편집기](https://github.com/projectkudu/kudu/wiki/App-Service-Editor)합니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-203">toocreate this mock API, we will create a new proxy, this time using hello [App Service Editor](https://github.com/projectkudu/kudu/wiki/App-Service-Editor).</span></span> <span data-ttu-id="b28f8-204">시작 tooget hello 포털에서 tooyour 함수 응용 프로그램을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-204">tooget started, navigate tooyour function app in hello portal.</span></span> <span data-ttu-id="b28f8-205">**플랫폼 기능**을 선택하고 **App Service 편집기**를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-205">Select **Platform features** and find **App Service Editor**.</span></span> <span data-ttu-id="b28f8-206">이 클릭 하면 새 탭에서 응용 프로그램 서비스 편집기 hello를 열립니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-206">Clicking this will open hello App Service Editor in a new tab.</span></span>

<span data-ttu-id="b28f8-207">선택 `proxies.json` 왼쪽 탐색 hello에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-207">Select `proxies.json` in hello left navigation.</span></span> <span data-ttu-id="b28f8-208">모든 프록시에 대 한 hello 구성을 저장 하는 hello 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-208">This is hello file which stores hello configuration for all of your proxies.</span></span> <span data-ttu-id="b28f8-209">Hello 중 하나를 사용 하는 경우 [배포 방법 함수](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment),이 hello 파일을 소스 제어에 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-209">If you use one of hello [Functions deployment methods](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment), this is hello file you will maintain in source control.</span></span> <span data-ttu-id="b28f8-210">이 파일에 대해 자세히 toolearn 참조 [프록시 고급 구성](https://docs.microsoft.com/azure/azure-functions/functions-proxies#advanced-configuration)합니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-210">toolearn more about this file, see [Proxies advanced configuration](https://docs.microsoft.com/azure/azure-functions/functions-proxies#advanced-configuration).</span></span>

<span data-ttu-id="b28f8-211">따랐다면 지금까지, 프로그램 proxies.json hello 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-211">If you've followed along so far, your proxies.json should look like hello following:</span></span>

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "HelloProxy": {
            "matchCondition": {
                "route": "/api/hello"
            },
            "backendUri": "https://%HELLO_HOST%/api/hello"
        }
    }
}
```

<span data-ttu-id="b28f8-212">다음으로 모의 API를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-212">Next you'll add your mock API.</span></span> <span data-ttu-id="b28f8-213">Proxies.json 파일을 hello 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-213">Replace your proxies.json file with hello following:</span></span>

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "HelloProxy": {
            "matchCondition": {
                "route": "/api/hello"
            },
            "backendUri": "https://%HELLO_HOST%/api/hello"
        },
        "GetUserByName" : {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/users/{username}"
            },
            "responseOverrides": {
                "response.statusCode": "200",
                "response.headers.Content-Type" : "application/json",
                "response.body": {
                    "name": "{username}",
                    "description": "Awesome developer and master of serverless APIs",
                    "skills": [
                        "Serverless",
                        "APIs",
                        "Azure",
                        "Cloud"
                    ]
                }
            }
        }
    }
}
```

<span data-ttu-id="b28f8-214">이 새 프록시 "GetUserByName" hello backendUri 속성 없이 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-214">This adds a new proxy, "GetUserByName", without hello backendUri property.</span></span> <span data-ttu-id="b28f8-215">다른 리소스를 호출 하는 대신 응답 재정의 사용 하 여 프록시에서 hello 기본 응답을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-215">Instead of calling another resource, it modifies hello default response from Proxies using a response override.</span></span> <span data-ttu-id="b28f8-216">요청 및 응답 재정의를 백 엔드 URL과 함께 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-216">Request and response overrides can also be used in conjunction with a backend URL.</span></span> <span data-ttu-id="b28f8-217">프록싱 tooa 레거시 시스템 해야 toomodify 헤더, 쿼리 매개 변수, 등 toolearn 요청 및 응답 재정의 대 한 자세한를 참조 하는 경우 특히 유용 [요청과 응답을 프록시 수정](https://docs.microsoft.com/azure/azure-functions/functions-proxies#a-namemodify-requests-responsesamodifying-requests-and-responses)합니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-217">This is particularly useful when proxying tooa legacy system, where you might need toomodify headers, query parameters, etc. toolearn more about request and response overrides, see [Modifying requests and responses in Proxies](https://docs.microsoft.com/azure/azure-functions/functions-proxies#a-namemodify-requests-responsesamodifying-requests-and-responses).</span></span>

<span data-ttu-id="b28f8-218">호출 hello 여 모의 API 테스트 `/api/users/{username}` 브라우저 또는 자주 사용 하 여 REST 클라이언트를 사용 하 여 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-218">Test your mock API by calling hello `/api/users/{username}` endpoint using a browser or your favorite REST client.</span></span> <span data-ttu-id="b28f8-219">수 있는지 tooreplace _{username}_ 사용자 이름을 나타내는 문자열 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-219">Be sure tooreplace _{username}_ with a string value representing a username.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b28f8-220">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b28f8-220">Next steps</span></span>

<span data-ttu-id="b28f8-221">이 자습서에서는 방법에 대해 배웠습니다 toobuild 및 Azure 기능에는 API를 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-221">In this tutorial, you learned how toobuild and customize an API on Azure Functions.</span></span> <span data-ttu-id="b28f8-222">또한 어떻게 toobring 여러 Api를 포함 하 여 mocks, 함께 통합된 API 화면으로 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-222">You also learned how toobring multiple APIs, including mocks, together as a unified API surface.</span></span> <span data-ttu-id="b28f8-223">이러한 기술을 toobuild Api의 복잡성에 관계 없이 아웃을 사용할 수 있는데, 서버가 없는 hello에서 실행 하는 동안 모든 Azure 기능에서 제공 하는 모델을 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="b28f8-223">You can use these techniques toobuild out APIs of any complexity, all while running on hello serverless compute model provided by Azure Functions.</span></span>

<span data-ttu-id="b28f8-224">hello 다음 참조 도움이 될 추가 API를 개발 하는 경우:</span><span class="sxs-lookup"><span data-stu-id="b28f8-224">hello following references may be helpful as you develop your API further:</span></span>

- [<span data-ttu-id="b28f8-225">Azure Functions HTTP 및 웹후크 바인딩</span><span class="sxs-lookup"><span data-stu-id="b28f8-225">Azure Functions HTTP and webhook bindings</span></span>](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook)
- <span data-ttu-id="b28f8-226">[Azure 함수 프록시 (미리 보기) 작업]</span><span class="sxs-lookup"><span data-stu-id="b28f8-226">[Working with Azure Functions Proxies (preview)]</span></span>
- [<span data-ttu-id="b28f8-227">Azure Functions API 문서화(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="b28f8-227">Documenting an Azure Functions API (preview)</span></span>](https://docs.microsoft.com/azure/azure-functions/functions-api-definition-getting-started)


[Create your first function]: https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function
[Azure 함수 프록시 (미리 보기) 작업]: https://docs.microsoft.com/azure/azure-functions/functions-proxies

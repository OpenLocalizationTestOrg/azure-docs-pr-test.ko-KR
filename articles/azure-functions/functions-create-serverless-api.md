---
title: "Azure Functions를 사용하여 서버 없는 API 만들기 | Microsoft Docs"
description: "Azure Functions를 사용하여 서버 없는 API를 만드는 방법"
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
ms.openlocfilehash: 28056a385b058f7daeca2253ccb304116b49eba0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-serverless-api-using-azure-functions"></a><span data-ttu-id="dd739-103">Azure Functions를 사용하여 서버 없는 API 만들기</span><span class="sxs-lookup"><span data-stu-id="dd739-103">Create a serverless API using Azure Functions</span></span>

<span data-ttu-id="dd739-104">이 자습서에서는 Azure Functions를 사용하여 확장성이 뛰어난 API를 빌드하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-104">In this tutorial you will learn how Azure Functions allows you to build highly-scalable APIs.</span></span> <span data-ttu-id="dd739-105">Azure Functions에는 Node.JS, C# 등을 비롯한 다양한 언어로 쉽게 끝점을 작성할 수 있도록 하는 기본 제공 HTTP 트리거 및 바인딩 컬렉션이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-105">Azure Functions comes with a collection of built-in HTTP triggers and bindings which make it easy to author an endpoint in a variety of languages, including Node.JS, C#, and more.</span></span> <span data-ttu-id="dd739-106">이 자습서에서는 API 디자인의 특정 작업을 처리하도록 HTTP 트리거를 사용자 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-106">In this tutorial, you will customize an HTTP trigger to handle specific actions in your API design.</span></span> <span data-ttu-id="dd739-107">또한 Azure Functions 프록시와 통합하고 모의 API를 설정하여 API를 확장할 준비를 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-107">You will also prepare for growing your API by integrating it with Azure Functions Proxies and setting up mock APIs.</span></span> <span data-ttu-id="dd739-108">이러한 모든 작업은 Functions의 서버 없는 Compute 환경에서 수행되므로 리소스 확장 문제를 걱정할 필요가 없으며 API 논리에만 집중하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-108">All of this is accomplished on top of the Functions serverless compute environment, so you don't have to worry about scaling resources - you can just focus on your API logic.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dd739-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="dd739-109">Prerequisites</span></span> 

[!INCLUDE [Previous quickstart note](../../includes/functions-quickstart-previous-topics.md)]

<span data-ttu-id="dd739-110">결과 함수가 이 자습서의 나머지 부분에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-110">The resulting function will be used for the rest of this tutorial.</span></span>

### <a name="sign-in-to-azure"></a><span data-ttu-id="dd739-111">Azure에 로그인</span><span class="sxs-lookup"><span data-stu-id="dd739-111">Sign in to Azure</span></span>

<span data-ttu-id="dd739-112">Azure Portal을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-112">Open the Azure portal.</span></span> <span data-ttu-id="dd739-113">이 작업을 수행하려면 사용자의 Azure 계정으로 [https://portal.azure.com](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-113">To do this, sign in to [https://portal.azure.com](https://portal.azure.com) with your Azure account.</span></span>

## <a name="customize-your-http-function"></a><span data-ttu-id="dd739-114">HTTP 함수 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="dd739-114">Customize your HTTP function</span></span>

<span data-ttu-id="dd739-115">기본적으로 HTTP 트리거 함수는 모든 HTTP 메서드를 허용하도록 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-115">By default, your HTTP-triggered function is configured to accept any HTTP method.</span></span> <span data-ttu-id="dd739-116">`http://<yourapp>.azurewebsites.net/api/<funcname>?code=<functionkey>` 형식의 기본 URL도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-116">There is also a default URL of the form `http://<yourapp>.azurewebsites.net/api/<funcname>?code=<functionkey>`.</span></span> <span data-ttu-id="dd739-117">빠른 시작을 진행한 경우 `<funcname>`이 "HttpTriggerJS1"과 같을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-117">If you followed the quickstart, then `<funcname>` probably looks something like "HttpTriggerJS1".</span></span> <span data-ttu-id="dd739-118">이 섹션에서는 대신 `/api/hello` 경로에 대한 GET 요청에만 응답하도록 함수를 수정할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-118">In this section, you will modify the function to respond only to GET requests against `/api/hello` route instead.</span></span> 

<span data-ttu-id="dd739-119">Azure Portal에서 해당 함수로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-119">Navigate to your function in the Azure portal.</span></span> <span data-ttu-id="dd739-120">왼쪽 탐색 영역에서 **통합**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-120">Select **Integrate** in the left navigation.</span></span>

![HTTP 함수 사용자 지정](./media/functions-create-serverless-api/customizing-http.png)

<span data-ttu-id="dd739-122">표에 지정된 것처럼 HTTP 트리거 설정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-122">Use the HTTP trigger settings as specified in the table.</span></span>

| <span data-ttu-id="dd739-123">필드</span><span class="sxs-lookup"><span data-stu-id="dd739-123">Field</span></span> | <span data-ttu-id="dd739-124">샘플 값</span><span class="sxs-lookup"><span data-stu-id="dd739-124">Sample value</span></span> | <span data-ttu-id="dd739-125">설명</span><span class="sxs-lookup"><span data-stu-id="dd739-125">Description</span></span> |
|---|---|---|
| <span data-ttu-id="dd739-126">허용된 HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="dd739-126">Allowed HTTP methods</span></span> | <span data-ttu-id="dd739-127">선택된 메서드</span><span class="sxs-lookup"><span data-stu-id="dd739-127">Selected methods</span></span> | <span data-ttu-id="dd739-128">이 함수를 호출하는 데 사용할 수 있는 HTTP 메서드 결정</span><span class="sxs-lookup"><span data-stu-id="dd739-128">Determines what HTTP methods may be used to invoke this function</span></span> |
| <span data-ttu-id="dd739-129">선택한 HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="dd739-129">Selected HTTP methods</span></span> | <span data-ttu-id="dd739-130">GET</span><span class="sxs-lookup"><span data-stu-id="dd739-130">GET</span></span> | <span data-ttu-id="dd739-131">선택한 HTTP 메서드만 이 함수를 호출하는 데 사용할 수 있도록 허용</span><span class="sxs-lookup"><span data-stu-id="dd739-131">Allows only selected HTTP methods to be used to invoke this function</span></span> |
| <span data-ttu-id="dd739-132">경로 템플릿</span><span class="sxs-lookup"><span data-stu-id="dd739-132">Route template</span></span> | <span data-ttu-id="dd739-133">/hello</span><span class="sxs-lookup"><span data-stu-id="dd739-133">/hello</span></span> | <span data-ttu-id="dd739-134">이 함수를 호출하는 데 사용할 경로 결정</span><span class="sxs-lookup"><span data-stu-id="dd739-134">Determines what route is used to invoke this function</span></span> |

<span data-ttu-id="dd739-135">`/api` 기본 경로 접두사는 전역 설정에 의해 처리되므로 경로 템플릿에 포함하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-135">Note that you did not include the `/api` base path prefix in the route template, as this is handled by a global setting.</span></span>

<span data-ttu-id="dd739-136">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-136">Click **Save**.</span></span>

<span data-ttu-id="dd739-137">[Azure Functions HTTP 및 웹후크 바인딩](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#customizing-the-http-endpoint)에서 HTTP 함수 사용자 지정에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="dd739-137">You can learn more about customizing HTTP functions in [Azure Functions HTTP and webhook bindings](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#customizing-the-http-endpoint).</span></span>

### <a name="test-your-api"></a><span data-ttu-id="dd739-138">API 테스트</span><span class="sxs-lookup"><span data-stu-id="dd739-138">Test your API</span></span>

<span data-ttu-id="dd739-139">다음에는 함수를 테스트하여 새 API 화면에서 작동하는 모습을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-139">Next, test your function to see it working with the new API surface.</span></span>

<span data-ttu-id="dd739-140">왼쪽 탐색 영역에서 함수 이름을 클릭하여 개발 페이지로 다시 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-140">Navigate back to the development page by clicking on the function's name in the left navigation.</span></span>

<span data-ttu-id="dd739-141">**함수 URL 가져오기**를 클릭하고 URL을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-141">Click **Get function URL** and copy the URL.</span></span> <span data-ttu-id="dd739-142">이제 `/api/hello` 경로가 사용되는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-142">You should see that it uses the `/api/hello` route now.</span></span>

<span data-ttu-id="dd739-143">새 브라우저 탭 또는 기본 REST 클라이언트에 URL을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-143">Copy the URL into a new browser tab or your preferred REST client.</span></span> <span data-ttu-id="dd739-144">브라우저는 기본적으로 GET을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-144">Browsers will use GET by default.</span></span>

<span data-ttu-id="dd739-145">함수를 실행하고 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-145">Run the function and confirm that it is working.</span></span> <span data-ttu-id="dd739-146">빠른 시작 코드를 충족하려면 "name" 매개 변수를 쿼리 문자열로 제공해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-146">You may need to provide the "name" parameter as a query string to satisfy the quickstart code.</span></span>

<span data-ttu-id="dd739-147">다른 HTTP 메서드로 끝점을 호출하여 함수가 실행되지 않는지 확인할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-147">You can also try calling the endpoint with another HTTP method to confirm that the function is not executed.</span></span> <span data-ttu-id="dd739-148">이 경우 cURL, Postman 또는 Fiddler와 같은 REST 클라이언트를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-148">For this, you will need to use a REST client, such as cURL, Postman, or Fiddler.</span></span>

## <a name="proxies-overview"></a><span data-ttu-id="dd739-149">프록시 개요</span><span class="sxs-lookup"><span data-stu-id="dd739-149">Proxies overview</span></span>

<span data-ttu-id="dd739-150">다음 섹션에서는 프록시를 통해 API를 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-150">In the next section, you will surface your API through a proxy.</span></span> <span data-ttu-id="dd739-151">Azure Functions 프록시는 기타 리소스로 요청을 전달할 수 있도록 하는 미리 보기 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-151">Azure Functions Proxies is a preview feature that allows you to forward requests to other resources.</span></span> <span data-ttu-id="dd739-152">HTTP 트리거를 사용할 때처럼 HTTP 끝점을 정의하지만, 해당 끝점이 호출될 때 실행할 코드를 작성하지 않고 원격 구현에 대한 URL을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-152">You define an HTTP endpoint just like with HTTP trigger, but instead of writing code to execute when that endpoint is called, you provide a URL to a remote implementation.</span></span> <span data-ttu-id="dd739-153">이렇게 하면 여러 API 원본을 클라이언트가 쉽게 사용할 수 있는 단일 API 화면으로 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-153">This allows you to compose multiple API sources into a single API surface which is easy for clients to consume.</span></span> <span data-ttu-id="dd739-154">이러한 방식은 API를 마이크로 서비스로 빌드하려는 경우에 특히 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-154">This is particularly useful if you wish to build your API as microservices.</span></span>

<span data-ttu-id="dd739-155">프록시는 다음과 같은 HTTP 리소스를 가리킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-155">A proxy can point to any HTTP resource, such as:</span></span>
- <span data-ttu-id="dd739-156">Azure 기능</span><span class="sxs-lookup"><span data-stu-id="dd739-156">Azure Functions</span></span> 
- <span data-ttu-id="dd739-157">[Azure App Service](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is)의 API 앱</span><span class="sxs-lookup"><span data-stu-id="dd739-157">API apps in [Azure App Service](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is)</span></span>
- <span data-ttu-id="dd739-158">[Linux의 App Service](https://docs.microsoft.com/azure/app-service/app-service-linux-readme)에 있는 Docker 컨테이너</span><span class="sxs-lookup"><span data-stu-id="dd739-158">Docker containers in [App Service on Linux](https://docs.microsoft.com/azure/app-service/app-service-linux-readme)</span></span>
- <span data-ttu-id="dd739-159">기타 호스트된 API</span><span class="sxs-lookup"><span data-stu-id="dd739-159">Any other hosted API</span></span>

<span data-ttu-id="dd739-160">프록시에 대해 자세한 알아보려면 [Azure Functions 프록시 사용(미리 보기)]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dd739-160">To learn more about proxies, see [Working with Azure Functions Proxies (preview)].</span></span>

## <a name="create-your-first-proxy"></a><span data-ttu-id="dd739-161">첫 번째 프록시 만들기</span><span class="sxs-lookup"><span data-stu-id="dd739-161">Create your first proxy</span></span>

<span data-ttu-id="dd739-162">이 섹션에서는 전체 API에 대한 프런트 엔드로 사용되는 새 프록시를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-162">In this section, you will create a new proxy which serves as a frontend to your overall API.</span></span> 

### <a name="setting-up-the-frontend-environment"></a><span data-ttu-id="dd739-163">프런트 엔드 환경 설정</span><span class="sxs-lookup"><span data-stu-id="dd739-163">Setting up the frontend environment</span></span>

<span data-ttu-id="dd739-164">[함수 앱 만들기](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function#create-a-function-app) 단계를 반복하여 프록시를 만들 새 함수 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-164">Repeat the steps to [Create a function app](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function#create-a-function-app) to create a new function app in which you will create your proxy.</span></span> <span data-ttu-id="dd739-165">이 새로운 앱은 API에 대한 프런트 엔드로 사용되고 이전에 편집하던 함수 앱은 백 엔드로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-165">This new app will serve as the frontend for our API, and the function app you were previously editing will serve as a backend.</span></span>

<span data-ttu-id="dd739-166">포털의 새 프런트 엔드 함수 앱으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-166">Navigate to your new frontend function app in the portal.</span></span>

<span data-ttu-id="dd739-167">**설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-167">Select **Settings**.</span></span> <span data-ttu-id="dd739-168">그런 후 **Azure Functions 프록시 사용(미리 보기)**을 "설정"으로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-168">Then toggle **Enable Azure Functions Proxies (preview)** to "On".</span></span>

<span data-ttu-id="dd739-169">**플랫폼 설정**을 선택하고 **응용 프로그램 설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-169">Select **Platform Settings** and choose **Application Settings**.</span></span>

<span data-ttu-id="dd739-170">**앱 설정** 아래로 스크롤하고 "HELLO_HOST" 키를 갖는 새 설정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-170">Scroll down to **App settings** and create a new setting with key "HELLO_HOST".</span></span> <span data-ttu-id="dd739-171">해당 값을 백 엔드 함수 앱의 호스트(예: `<YourApp>.azurewebsites.net`)로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-171">Set its value to the host of your backend function app, such as `<YourApp>.azurewebsites.net`.</span></span> <span data-ttu-id="dd739-172">이것은 HTTP 함수를 테스트할 때 이전에 복사한 URL의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-172">This is part of the URL that you copied earlier when testing your HTTP function.</span></span> <span data-ttu-id="dd739-173">나중에 구성에서 이 설정을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-173">You'll reference this setting in the configuration later.</span></span>

> [!NOTE] 
> <span data-ttu-id="dd739-174">프록시에 대한 하드 코드된 환경 종속성을 방지하려면 호스트 구성에 대해 앱 설정이 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-174">App settings are recommended for the host configuration to prevent a hard-coded environment dependency for the proxy.</span></span> <span data-ttu-id="dd739-175">앱 설정을 사용할 경우 환경 간에 프록시 구성을 이동할 수 있고 환경 관련 앱 설정이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-175">Using app settings means that you can move the proxy configuration between environments, and the environment-specific app settings will be applied.</span></span>

<span data-ttu-id="dd739-176">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-176">Click **Save**.</span></span>

### <a name="creating-a-proxy-on-the-frontend"></a><span data-ttu-id="dd739-177">프런트 엔드에 프록시 만들기</span><span class="sxs-lookup"><span data-stu-id="dd739-177">Creating a proxy on the frontend</span></span>

<span data-ttu-id="dd739-178">포털의 프런트 엔드 함수 앱으로 다시 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-178">Navigate back to your frontend function app in the portal.</span></span>

<span data-ttu-id="dd739-179">왼쪽 탐색 영역에서 "프록시 (미리 보기)" 옆의 더하기 기호 '+'를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-179">In the left-hand navigation, click the plus sign '+' next to "Proxies (preview)".</span></span>

![프록시 만들기](./media/functions-create-serverless-api/creating-proxy.png)

<span data-ttu-id="dd739-181">표에 지정된 것처럼 프록시 설정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-181">Use proxy settings as specified in the table.</span></span>

| <span data-ttu-id="dd739-182">필드</span><span class="sxs-lookup"><span data-stu-id="dd739-182">Field</span></span> | <span data-ttu-id="dd739-183">샘플 값</span><span class="sxs-lookup"><span data-stu-id="dd739-183">Sample value</span></span> | <span data-ttu-id="dd739-184">설명</span><span class="sxs-lookup"><span data-stu-id="dd739-184">Description</span></span> |
|---|---|---|
| <span data-ttu-id="dd739-185">이름</span><span class="sxs-lookup"><span data-stu-id="dd739-185">Name</span></span> | <span data-ttu-id="dd739-186">HelloProxy</span><span class="sxs-lookup"><span data-stu-id="dd739-186">HelloProxy</span></span> | <span data-ttu-id="dd739-187">관리에 대해서만 사용되는 이름</span><span class="sxs-lookup"><span data-stu-id="dd739-187">A friendly name used only for management</span></span> |
| <span data-ttu-id="dd739-188">경로 템플릿</span><span class="sxs-lookup"><span data-stu-id="dd739-188">Route template</span></span> | <span data-ttu-id="dd739-189">/api/hello</span><span class="sxs-lookup"><span data-stu-id="dd739-189">/api/hello</span></span> | <span data-ttu-id="dd739-190">이 프록시를 호출하는 데 사용할 경로 결정</span><span class="sxs-lookup"><span data-stu-id="dd739-190">Determines what route is used to invoke this proxy</span></span> |
| <span data-ttu-id="dd739-191">백 엔드 URL</span><span class="sxs-lookup"><span data-stu-id="dd739-191">Backend URL</span></span> | <span data-ttu-id="dd739-192">https://%HELLO_HOST%/api/hello</span><span class="sxs-lookup"><span data-stu-id="dd739-192">https://%HELLO_HOST%/api/hello</span></span> | <span data-ttu-id="dd739-193">요청을 프록시 처리할 끝점을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-193">Specifies the endpoint to which the request should be proxied</span></span> |

<span data-ttu-id="dd739-194">프록시는 `/api` 기본 경로 접두사를 제공하지 않으며 경로 템플릿에 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-194">Note that Proxies does not provide the `/api` base path prefix, and this must be included in the route template.</span></span>

<span data-ttu-id="dd739-195">`%HELLO_HOST%` 구문은 이전에 만든 앱 설정을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-195">The `%HELLO_HOST%` syntax will reference the app setting you created earlier.</span></span> <span data-ttu-id="dd739-196">확인된 URL은 원래 함수를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-196">The resolved URL will point to your original function.</span></span>

<span data-ttu-id="dd739-197">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-197">Click **Create**.</span></span>

<span data-ttu-id="dd739-198">프록시 URL을 복사하고 브라우저 또는 자주 사용하는 HTTP 클라이언트에서 테스트하여 새 프록시를 시험해볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-198">You can try out your new proxy by copying the Proxy URL and testing it in the browser or with your favorite HTTP client.</span></span>

## <a name="create-a-mock-api"></a><span data-ttu-id="dd739-199">모의 API 만들기</span><span class="sxs-lookup"><span data-stu-id="dd739-199">Create a mock API</span></span>

<span data-ttu-id="dd739-200">다음으로 프록시를 사용하여 솔루션에 대한 모의 API 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-200">Next, you will use a proxy to create a mock API for your solution.</span></span> <span data-ttu-id="dd739-201">이를 통해 백 엔드를 완전히 구현하지 않고도 클라이언트 개발을 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-201">This allows client development to progress, without needing the backend fully implemented.</span></span> <span data-ttu-id="dd739-202">개발 후반부에 이 논리를 지원하는 새 함수 앱을 만들고 프록시를 해당 앱으로 리디렉션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-202">Later in development, you could create a new function app which supports this logic and redirect your proxy to it.</span></span>

<span data-ttu-id="dd739-203">이 모의 API를 만들려면 이번에는 [App Service 편집기](https://github.com/projectkudu/kudu/wiki/App-Service-Editor)를 사용하여 새 프록시를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-203">To create this mock API, we will create a new proxy, this time using the [App Service Editor](https://github.com/projectkudu/kudu/wiki/App-Service-Editor).</span></span> <span data-ttu-id="dd739-204">시작하려면 포털의 함수 앱으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-204">To get started, navigate to your function app in the portal.</span></span> <span data-ttu-id="dd739-205">**플랫폼 기능**을 선택하고 **App Service 편집기**를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-205">Select **Platform features** and find **App Service Editor**.</span></span> <span data-ttu-id="dd739-206">이를 클릭하면 새 탭에서 App Service 편집기가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-206">Clicking this will open the App Service Editor in a new tab.</span></span>

<span data-ttu-id="dd739-207">왼쪽 탐색 영역에서 `proxies.json`을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-207">Select `proxies.json` in the left navigation.</span></span> <span data-ttu-id="dd739-208">모든 사용자 프록시에 대한 구성이 저장되는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-208">This is the file which stores the configuration for all of your proxies.</span></span> <span data-ttu-id="dd739-209">[함수 배포 방법](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment) 중 하나를 사용하는 경우 이 파일이 소스 제어에 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-209">If you use one of the [Functions deployment methods](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment), this is the file you will maintain in source control.</span></span> <span data-ttu-id="dd739-210">이 파일에 대한 자세한 내용은 [프록시 고급 구성](https://docs.microsoft.com/azure/azure-functions/functions-proxies#advanced-configuration)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dd739-210">To learn more about this file, see [Proxies advanced configuration](https://docs.microsoft.com/azure/azure-functions/functions-proxies#advanced-configuration).</span></span>

<span data-ttu-id="dd739-211">지금까지 작업을 잘 진행했으면 proxies.json이 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-211">If you've followed along so far, your proxies.json should look like the following:</span></span>

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

<span data-ttu-id="dd739-212">다음으로 모의 API를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-212">Next you'll add your mock API.</span></span> <span data-ttu-id="dd739-213">proxies.json 파일을 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-213">Replace your proxies.json file with the following:</span></span>

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

<span data-ttu-id="dd739-214">이렇게 하면 backendUri 속성을 제외한 새 프록시 "GetUserByName"이 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-214">This adds a new proxy, "GetUserByName", without the backendUri property.</span></span> <span data-ttu-id="dd739-215">다른 리소스를 호출하지 않고 응답 재정의를 사용하여 프록시의 기본 응답을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-215">Instead of calling another resource, it modifies the default response from Proxies using a response override.</span></span> <span data-ttu-id="dd739-216">요청 및 응답 재정의를 백 엔드 URL과 함께 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-216">Request and response overrides can also be used in conjunction with a backend URL.</span></span> <span data-ttu-id="dd739-217">레거시 시스템으로 프록시할 때, 헤더를 수정하거나 매개 변수를 쿼리하는 등의 작업이 필요할 때 특히 유용합니다. 요청 및 응답 재정의에 대한 자세한 내용은 [프록시에서 요청 및 응답 수정](https://docs.microsoft.com/azure/azure-functions/functions-proxies#a-namemodify-requests-responsesamodifying-requests-and-responses)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dd739-217">This is particularly useful when proxying to a legacy system, where you might need to modify headers, query parameters, etc. To learn more about request and response overrides, see [Modifying requests and responses in Proxies](https://docs.microsoft.com/azure/azure-functions/functions-proxies#a-namemodify-requests-responsesamodifying-requests-and-responses).</span></span>

<span data-ttu-id="dd739-218">브라우저 또는 자주 사용하는 REST 클라이언트를 통해 `/api/users/{username}` 끝점을 호출하여 모의 API를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-218">Test your mock API by calling the `/api/users/{username}` endpoint using a browser or your favorite REST client.</span></span> <span data-ttu-id="dd739-219">_{username}_을 사용자 이름을 나타내는 문자열 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-219">Be sure to replace _{username}_ with a string value representing a username.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dd739-220">다음 단계</span><span class="sxs-lookup"><span data-stu-id="dd739-220">Next steps</span></span>

<span data-ttu-id="dd739-221">이 자습서에서는 Azure Functions에서 API를 빌드하고 사용자 지정하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-221">In this tutorial, you learned how to build and customize an API on Azure Functions.</span></span> <span data-ttu-id="dd739-222">또한 모의 API를 비롯한 여러 API를 하나의 통합 API 화면에 표시하는 방법도 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-222">You also learned how to bring multiple APIs, including mocks, together as a unified API surface.</span></span> <span data-ttu-id="dd739-223">이러한 기법을 사용하여 복잡성에 관계없이 Azure Functions에서 제공하는 서버 없는 Compute 모델에서 실행되는 API를 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-223">You can use these techniques to build out APIs of any complexity, all while running on the serverless compute model provided by Azure Functions.</span></span>

<span data-ttu-id="dd739-224">다음 참조는 API를 추가로 개발하는 경우 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd739-224">The following references may be helpful as you develop your API further:</span></span>

- [<span data-ttu-id="dd739-225">Azure Functions HTTP 및 웹후크 바인딩</span><span class="sxs-lookup"><span data-stu-id="dd739-225">Azure Functions HTTP and webhook bindings</span></span>](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook)
- <span data-ttu-id="dd739-226">[Azure Functions 프록시 사용(미리 보기)]</span><span class="sxs-lookup"><span data-stu-id="dd739-226">[Working with Azure Functions Proxies (preview)]</span></span>
- [<span data-ttu-id="dd739-227">Azure Functions API 문서화(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="dd739-227">Documenting an Azure Functions API (preview)</span></span>](https://docs.microsoft.com/azure/azure-functions/functions-api-definition-getting-started)


[Create your first function]: https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function
[Azure Functions 프록시 사용(미리 보기)]: https://docs.microsoft.com/azure/azure-functions/functions-proxies

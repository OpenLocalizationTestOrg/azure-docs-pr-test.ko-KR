---
title: "Azure Functions에서 프록시 사용 | Microsoft Docs"
description: "Azure Functions 프록시를 사용하는 방법의 개요"
services: functions
documentationcenter: 
author: mattchenderson
manager: erikre
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 04/11/2017
ms.author: mahender
ms.openlocfilehash: 102e54627a8fee721d3ed85e86a8009e706bb5b1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="work-with-azure-functions-proxies-preview"></a><span data-ttu-id="62328-103">Azure Functions 프록시 사용(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="62328-103">Work with Azure Functions Proxies (preview)</span></span>

> [!NOTE] 
> <span data-ttu-id="62328-104">Azure Functions 프록시는 현재 미리 보기 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="62328-104">Azure Functions Proxies is currently in preview.</span></span> <span data-ttu-id="62328-105">미리 보기에서는 무료로 사용할 수 있지만 프록시 실행에는 표준 함수 요금이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="62328-105">It is free while in preview, but standard Functions billing applies to proxy executions.</span></span> <span data-ttu-id="62328-106">자세한 내용은 [Azure Functions 가격 책정](https://azure.microsoft.com/pricing/details/functions/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="62328-106">For more information, see [Azure Functions pricing](https://azure.microsoft.com/pricing/details/functions/).</span></span>

<span data-ttu-id="62328-107">이 문서에서는 Azure Functions 프록시를 구성하고 사용하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="62328-107">This article explains how to configure and work with Azure Functions Proxies.</span></span> <span data-ttu-id="62328-108">이 기능을 사용하면 다른 리소스에서 구현된 함수 앱에 끝점을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62328-108">With this feature, you can specify endpoints on your function app that are implemented by another resource.</span></span> <span data-ttu-id="62328-109">이러한 프록시를 사용하면 클라이언트에 대해 단일 API 화면을 계속 제공하면서 큰 API를 여러 개의 함수 앱으로 나눌 수 있습니다(마이크로 서비스 아키텍처 참조).</span><span class="sxs-lookup"><span data-stu-id="62328-109">You can use these proxies to break a large API into multiple function apps (as in a microservice architecture), while still presenting a single API surface for clients.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]


## <span data-ttu-id="62328-110"><a name="enable"></a>Azure Functions 프록시 사용</span><span class="sxs-lookup"><span data-stu-id="62328-110"><a name="enable"></a>Enable Azure Functions Proxies</span></span>

<span data-ttu-id="62328-111">프록시는 기본적으로 사용하도록 설정되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="62328-111">Proxies are not enabled by default.</span></span> <span data-ttu-id="62328-112">이 기능이 사용되지 않도록 설정된 동안에도 프록시를 만들 수 있지만 실행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="62328-112">You can create proxies while the feature is disabled, but they will not execute.</span></span> <span data-ttu-id="62328-113">프록시를 사용하도록 설정하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="62328-113">To enable proxies, do the following:</span></span>

1. <span data-ttu-id="62328-114">[Azure Portal]을 열고 함수 앱으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="62328-114">Open the [Azure portal], and then go to your function app.</span></span>
2. <span data-ttu-id="62328-115">**함수 앱 설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="62328-115">Select **Function app settings**.</span></span>
3. <span data-ttu-id="62328-116">**Azure Functions 프록시 사용(미리 보기)**을 **설정**으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="62328-116">Switch **Enable Azure Functions Proxies (preview)** to **On**.</span></span>

<span data-ttu-id="62328-117">새 기능을 사용할 수 있게 되면 여기로 돌아와 프록시 런타임을 업데이트할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62328-117">You can also return here to update the proxy runtime as new features become available.</span></span>


## <span data-ttu-id="62328-118"><a name="create"></a>프록시 만들기</span><span class="sxs-lookup"><span data-stu-id="62328-118"><a name="create"></a>Create a proxy</span></span>

<span data-ttu-id="62328-119">이 섹션에서는 함수 포털에서 프록시를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="62328-119">This section shows you how to create a proxy in the Functions portal.</span></span>

1. <span data-ttu-id="62328-120">[Azure Portal]을 열고 함수 앱으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="62328-120">Open the [Azure portal], and then go to your function app.</span></span>
2. <span data-ttu-id="62328-121">왼쪽 창에서 **새 프록시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="62328-121">In the left pane, select **New proxy**.</span></span>
3. <span data-ttu-id="62328-122">프록시의 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="62328-122">Provide a name for your proxy.</span></span>
4. <span data-ttu-id="62328-123">**경로 템플릿** 및 **HTTP 메서드**를 지정하여 이 함수 앱에 노출되는 끝점을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="62328-123">Configure the endpoint that's exposed on this function app by specifying the **route template** and **HTTP methods**.</span></span> <span data-ttu-id="62328-124">이러한 매개 변수는 [HTTP 트리거]에 대한 규칙에 따라 동작합니다.</span><span class="sxs-lookup"><span data-stu-id="62328-124">These parameters behave according to the rules for [HTTP triggers].</span></span>
5. <span data-ttu-id="62328-125">**백 엔드 URL**을 다른 끝점으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="62328-125">Set the **backend URL** to another endpoint.</span></span> <span data-ttu-id="62328-126">이러한 끝점은 다른 함수 앱의 함수이거나 다른 API일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62328-126">This endpoint could be a function in another function app, or it could be any other API.</span></span> <span data-ttu-id="62328-127">정적 값이 아니어도 되며 [응용 프로그램 설정] 및 [원래 클라이언트 요청의 매개 변수]를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62328-127">The value does not need to be static, and it can reference [application settings] and [parameters from the original client request].</span></span>
6. <span data-ttu-id="62328-128">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="62328-128">Click **Create**.</span></span>

<span data-ttu-id="62328-129">이제 프록시는 함수 앱에서 새 끝점으로 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="62328-129">Your proxy now exists as a new endpoint on your function app.</span></span> <span data-ttu-id="62328-130">클라이언트 관점에서 Azure Functions의 HttpTrigger에 같습니다.</span><span class="sxs-lookup"><span data-stu-id="62328-130">From a client perspective, it is equivalent to an HttpTrigger in Azure Functions.</span></span> <span data-ttu-id="62328-131">프록시 URL을 복사하고 자주 사용하는 HTTP 클라이언트에서 테스트하여 새 프록시를 시험해볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62328-131">You can try out your new proxy by copying the Proxy URL and testing it with your favorite HTTP client.</span></span>

## <span data-ttu-id="62328-132"><a name="modify-requests-responses"></a>요청 및 응답 수정</span><span class="sxs-lookup"><span data-stu-id="62328-132"><a name="modify-requests-responses"></a>Modify requests and responses</span></span>

<span data-ttu-id="62328-133">Azure Functions 프록시를 사용해서 백 엔드에서 요청 및 응답을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62328-133">With Azure Functions Proxies, you can modify requests to and responses from the back end.</span></span> <span data-ttu-id="62328-134">이러한 변환은 [변수 사용]에 정의된 대로 변수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62328-134">These transformations can use variables as defined in [Use variables].</span></span>

### <span data-ttu-id="62328-135"><a name="modify-backend-request"></a>백 엔드 요청 수정</span><span class="sxs-lookup"><span data-stu-id="62328-135"><a name="modify-backend-request"></a>Modify the back-end request</span></span>

<span data-ttu-id="62328-136">기본적으로 백 엔드 요청은 원래 요청의 복사본으로 초기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="62328-136">By default, the back-end request is initialized as a copy of the original request.</span></span> <span data-ttu-id="62328-137">백 엔드 URL을 설정하는 것 외에도 HTTP 메서드, 헤더 및 쿼리 문자열 매개 변수를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62328-137">In addition to setting the back-end URL, you can make changes to the HTTP method, headers, and query string parameters.</span></span> <span data-ttu-id="62328-138">수정된 값은 [응용 프로그램 설정] 및 [원래 클라이언트 요청의 매개 변수]를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62328-138">The modified values can reference [application settings] and [parameters from the original client request].</span></span>

<span data-ttu-id="62328-139">현재 백 엔드 요청을 수정하기 위한 포털 환경은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="62328-139">Currently, there is no portal experience for modifying back-end requests.</span></span> <span data-ttu-id="62328-140">proxies.json에서 이 기능을 적용하는 방법을 알아보려면 [requestOverrides 개체 정의]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="62328-140">To learn how to apply this capability from proxies.json, see [Define a requestOverrides object].</span></span>

### <span data-ttu-id="62328-141"><a name="modify-response"></a>응답 수정</span><span class="sxs-lookup"><span data-stu-id="62328-141"><a name="modify-response"></a>Modify the response</span></span>

<span data-ttu-id="62328-142">기본적으로 클라이언트 요청은 원래 응답의 복사본으로 초기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="62328-142">By default, the client response is initialized as a copy of the back-end response.</span></span> <span data-ttu-id="62328-143">응답의 상태 코드, 이유 구문, 헤더 및 본문을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62328-143">You can make changes to the response's status code, reason phrase, headers, and body.</span></span> <span data-ttu-id="62328-144">수정된 값은 [응용 프로그램 설정], [원래 클라이언트 요청의 매개 변수] 및 [백 엔드 응답의 매개 변수]를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62328-144">The modified values can reference [application settings], [parameters from the original client request], and [parameters from the back-end response].</span></span>

<span data-ttu-id="62328-145">현재 응답을 수정하기 위한 포털 환경은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="62328-145">Currently, there is no portal experience for modifying responses.</span></span> <span data-ttu-id="62328-146">proxies.json에서 이 기능을 적용하는 방법을 알아보려면 [ 개체 정의]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="62328-146">To learn how to apply this capability from proxies.json, see [Define a responseOverrides object].</span></span>

## <span data-ttu-id="62328-147"><a name="using-variables"></a>변수 사용</span><span class="sxs-lookup"><span data-stu-id="62328-147"><a name="using-variables"></a>Use variables</span></span>

<span data-ttu-id="62328-148">프록시에 대한 구성은 정적일 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="62328-148">The configuration for a proxy does not need to be static.</span></span> <span data-ttu-id="62328-149">원래 요청, 백 엔드 응답 또는 응용 프로그램 설정의 변수를 사용하도록 조건을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62328-149">You can condition it to use variables from the original request, the back-end response, or application settings.</span></span>

### <span data-ttu-id="62328-150"><a name="request-parameters"></a>요청 매개 변수 참조</span><span class="sxs-lookup"><span data-stu-id="62328-150"><a name="request-parameters"></a>Reference request parameters</span></span>

<span data-ttu-id="62328-151">요청 매개 변수는 백 엔드 URL 속성에 대한 입력 또는 요청 및 응답을 수정하는 일부로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62328-151">You can use request parameters as inputs to the back-end URL property or as part of modifying requests and responses.</span></span> <span data-ttu-id="62328-152">기본 프록시 구성에 지정된 경로 템플릿에서 제한할 수 있는 매개 변수도 있고 들어오는 요청의 속성에서 가져올 수 있는 매개 변수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62328-152">Some parameters can be bound from the route template that's specified in the base proxy configuration, and others can come from properties of the incoming request.</span></span>

#### <a name="route-template-parameters"></a><span data-ttu-id="62328-153">경로 템플릿 매개 변수</span><span class="sxs-lookup"><span data-stu-id="62328-153">Route template parameters</span></span>
<span data-ttu-id="62328-154">경로 템플릿에 사용된 매개 변수는 이름으로 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62328-154">Parameters that are used in the route template are available to be referenced by name.</span></span> <span data-ttu-id="62328-155">이러한 매개 변수 이름은 중괄호({})로 묶습니다.</span><span class="sxs-lookup"><span data-stu-id="62328-155">The parameter names are enclosed in braces ({}).</span></span>

<span data-ttu-id="62328-156">예를 들어 프록시에 `/pets/{petId}`와 같은 경로 템플릿이 있는 경우 백 엔드 URL은 `https://<AnotherApp>.azurewebsites.net/api/pets/{petId}`와 같이 `{petId}` 값을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62328-156">For example, if a proxy has a route template, such as `/pets/{petId}`, the back-end URL can include the value of `{petId}`, as in `https://<AnotherApp>.azurewebsites.net/api/pets/{petId}`.</span></span> <span data-ttu-id="62328-157">경로 템플릿이 와일드카드로 끝나면(예: `/api/{*restOfPath}`) 값 `{restOfPath}`는 들어오는 요청의 나머지 경로 세그먼트에 대한 문자열 표현이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="62328-157">If the route template terminates in a wildcard, such as `/api/{*restOfPath}`, the value `{restOfPath}` is a string representation of the remaining path segments from the incoming request.</span></span>

#### <a name="additional-request-parameters"></a><span data-ttu-id="62328-158">추가 요청 매개 변수</span><span class="sxs-lookup"><span data-stu-id="62328-158">Additional request parameters</span></span>
<span data-ttu-id="62328-159">경로 템플릿 매개 변수 외에도 구성 값에 다음 값을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62328-159">In addition to the route template parameters, the following values can be used in config values:</span></span>

* <span data-ttu-id="62328-160">**{request.method}** : 원래 요청에 사용된 HTTP 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="62328-160">**{request.method}**: The HTTP method that's used on the original request.</span></span>
* <span data-ttu-id="62328-161">**{request.headers.\<HeaderName\>}**: 원래 요청에서 읽어올 수 있는 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="62328-161">**{request.headers.\<HeaderName\>}**: A header that can be read from the original request.</span></span> <span data-ttu-id="62328-162">*\<HeaderName\>*을 읽으려는 헤더 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="62328-162">Replace *\<HeaderName\>* with the name of the header that you want to read.</span></span> <span data-ttu-id="62328-163">헤더가 요청에 포함되지 않으면 값은 비어 있는 문자열이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="62328-163">If the header is not included on the request, the value will be the empty string.</span></span>
* <span data-ttu-id="62328-164">**{request.querystring.\<ParameterName\>}**: 원래 요청에서 읽어올 수 있는 쿼리 문자열 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="62328-164">**{request.querystring.\<ParameterName\>}**: A query string parameter that can be read from the original request.</span></span> <span data-ttu-id="62328-165">*\<ParameterName\>*을 읽으려는 매개 변수 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="62328-165">Replace *\<ParameterName\>* with the name of the parameter that you want to read.</span></span> <span data-ttu-id="62328-166">매개 변수가 요청에 포함되지 않으면 값은 비어 있는 문자열이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="62328-166">If the parameter is not included on the request, the value will be the empty string.</span></span>

### <span data-ttu-id="62328-167"><a name="response-parameters"></a>백 엔드 응답 매개 변수 참조</span><span class="sxs-lookup"><span data-stu-id="62328-167"><a name="response-parameters"></a>Reference back-end response parameters</span></span>

<span data-ttu-id="62328-168">응답 매개 변수는 클라이언트에 대한 응답을 수정하는 일부로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62328-168">Response parameters can be used as part of modifying the response to the client.</span></span> <span data-ttu-id="62328-169">구성 값에 다음 값을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62328-169">The following values can be used in config values:</span></span>

* <span data-ttu-id="62328-170">**{backend.response.statusCode}**: 백 엔드 응답에 반환할 HTTP 상태 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="62328-170">**{backend.response.statusCode}**: The HTTP status code that's returned on the back-end response.</span></span>
* <span data-ttu-id="62328-171">**{backend.response.statusReason}**: 백 엔드 응답에 반환할 HTTP 이유 구문입니다.</span><span class="sxs-lookup"><span data-stu-id="62328-171">**{backend.response.statusReason}**: The HTTP reason phrase that's returned on the back-end response.</span></span>
* <span data-ttu-id="62328-172">**{backend.response.headers.\<HeaderName\>}**: 백 엔드 응답에서 읽어올 수 있는 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="62328-172">**{backend.response.headers.\<HeaderName\>}**: A header that can be read from the back-end response.</span></span> <span data-ttu-id="62328-173">*\<HeaderName\>*을 읽으려는 헤더 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="62328-173">Replace *\<HeaderName\>* with the name of the header you want to read.</span></span> <span data-ttu-id="62328-174">헤더가 요청에 포함되지 않으면 값은 비어 있는 문자열이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="62328-174">If the header is not included on the request, the value will be the empty string.</span></span>

### <span data-ttu-id="62328-175"><a name="use-appsettings"></a>응용 프로그램 설정 참조</span><span class="sxs-lookup"><span data-stu-id="62328-175"><a name="use-appsettings"></a>Reference application settings</span></span>

<span data-ttu-id="62328-176">설정 이름을 백분율 기호(%)로 묶어 [함수 앱에 대해 정의된 응용 프로그램 설정](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#develop)을 참조할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62328-176">You can also reference [application settings defined for the function app](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#develop) by surrounding the setting name with percent signs (%).</span></span>

<span data-ttu-id="62328-177">예를 들어 *https://%ORDER_PROCESSING_HOST%/api/orders*의 백 엔드 URL에서 “%ORDER_PROCESSING_HOST%”는 ORDER_PROCESSING_HOS 설정 값으로 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="62328-177">For example, a back-end URL of *https://%ORDER_PROCESSING_HOST%/api/orders* would have "%ORDER_PROCESSING_HOST%" replaced with the value of the ORDER_PROCESSING_HOST setting.</span></span>

> [!TIP] 
> <span data-ttu-id="62328-178">배포 또는 테스트 환경이 여러 개 있는 경우 백 엔드 호스트에 대해 응용 프로그램 설정을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="62328-178">Use application settings for back-end hosts when you have multiple deployments or test environments.</span></span> <span data-ttu-id="62328-179">이러한 방식으로 항상 해당 환경에 적합한 백 엔드에 정보를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62328-179">That way, you can make sure that you are always talking to the right back end for that environment.</span></span>

## <a name="advanced-configuration"></a><span data-ttu-id="62328-180">고급 구성</span><span class="sxs-lookup"><span data-stu-id="62328-180">Advanced configuration</span></span>

<span data-ttu-id="62328-181">구성하는 프록시는 함수 앱 디렉터리의 루트에 있는 proxies.json 파일에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="62328-181">The proxies that you configure are stored in a proxies.json file, which is located in the root of a function app directory.</span></span> <span data-ttu-id="62328-182">이 파일을 수동으로 편집하고 함수가 지원하는 [배포 방법](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment) 중 하나를 사용하여 앱의 일부로 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62328-182">You can manually edit this file and deploy it as part of your app when you use any of the [deployment methods](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment) that Functions supports.</span></span> <span data-ttu-id="62328-183">파일이 처리되려면 이 기능이 [사용되도록 설정](#enable)되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="62328-183">The feature must be [enabled](#enable) for the file to be processed.</span></span> 

> [!TIP] 
> <span data-ttu-id="62328-184">배포 방법 중 하나를 설정하지 않은 경우 포털에서 proxies.json 파일로 작업할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62328-184">If you have not set up one of the deployment methods, you can also work with the proxies.json file in the portal.</span></span> <span data-ttu-id="62328-185">함수 앱으로 이동하여 **플랫폼 기능**을 선택한 후 **App Service 편집기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="62328-185">Go to your function app, select **Platform features**, and then select **App Service Editor**.</span></span> <span data-ttu-id="62328-186">이렇게 하여 함수 앱의 전체 파일 구조를 보고 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62328-186">By doing so, you can view the entire file structure of your function app and then make changes.</span></span>

<span data-ttu-id="62328-187">Proxies.json은 명명된 프록시 및 해당 정의로 구성된 프록시 개체로 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="62328-187">Proxies.json is defined by a proxies object, which is composed of named proxies and their definitions.</span></span> <span data-ttu-id="62328-188">편집기에서 코드 완성을 지원하는 경우 필요에 따라 [JSON 스키마](http://json.schemastore.org/proxies)를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62328-188">Optionally, if your editor supports it, you can reference a [JSON schema](http://json.schemastore.org/proxies) for code completion.</span></span> <span data-ttu-id="62328-189">예제 파일은 다음과 유사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62328-189">An example file might look like the following:</span></span>

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "proxy1": {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/{test}"
            },
            "backendUri": "https://<AnotherApp>.azurewebsites.net/api/<FunctionName>"
        }
    }
}
```

<span data-ttu-id="62328-190">각 프록시에는 위의 코드 예제의 *proxy1*과 같은 이름이 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="62328-190">Each proxy has a friendly name, such as *proxy1* in the preceding example.</span></span> <span data-ttu-id="62328-191">해당하는 프록시 정의 개체는 다음과 같은 속성으로 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="62328-191">The corresponding proxy definition object is defined by the following properties:</span></span>

* <span data-ttu-id="62328-192">**matchCondition**: 필수--이 프록시의 실행을 트리거하는 요청을 정의하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="62328-192">**matchCondition**: Required--an object defining the requests that trigger the execution of this proxy.</span></span> <span data-ttu-id="62328-193">[HTTP 트리거]와 공유되는 두 가지 속성이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62328-193">It contains two properties that are shared with [HTTP triggers]:</span></span>
    * <span data-ttu-id="62328-194">_메서드_: 프록시가 응답하는 HTTP 메서드의 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="62328-194">_methods_: An array of the HTTP methods that the proxy responds to.</span></span> <span data-ttu-id="62328-195">이 속성을 지정하지 않으면 프록시는 경로의 모든 HTTP 메서드에 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="62328-195">If it is not specified, the proxy responds to all HTTP methods on the route.</span></span>
    * <span data-ttu-id="62328-196">_route_: 필수--경로 템플릿을 정의하여 프록시에서 응답할 요청 URL을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="62328-196">_route_: Required--defines the route template, controlling which request URLs your proxy responds to.</span></span> <span data-ttu-id="62328-197">HTTP 트리거와 달리 기본값이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="62328-197">Unlike in HTTP triggers, there is no default value.</span></span>
* <span data-ttu-id="62328-198">**backendUri**: 요청이 프록시되어야 하는 백 엔드 리소스의 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="62328-198">**backendUri**: The URL of the back-end resource to which the request should be proxied.</span></span> <span data-ttu-id="62328-199">이 값은 응용 프로그램 설정 및 원래 클라이언트 요청의 매개 변수를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62328-199">This value can reference application settings and parameters from the original client request.</span></span> <span data-ttu-id="62328-200">이 속성을 포함하지 않으면 Azure Functions는 HTTP 200 OK로 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="62328-200">If this property is not included, Azure Functions responds with an HTTP 200 OK.</span></span>
* <span data-ttu-id="62328-201">**requestOverrides**: 변환을 백 엔드 요청으로 정의하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="62328-201">**requestOverrides**: An object that defines transformations to the back-end request.</span></span> <span data-ttu-id="62328-202">[requestOverrides 개체 정의]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="62328-202">See [Define a requestOverrides object].</span></span>
* <span data-ttu-id="62328-203">**responseOverrides**: 클라이언트 응답으로 변환을 정의하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="62328-203">**responseOverrides**: An object that defines transformations to the client response.</span></span> <span data-ttu-id="62328-204">[ 개체 정의]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="62328-204">See [Define a responseOverrides object].</span></span>

> [!NOTE] 
> <span data-ttu-id="62328-205">경로 속성 Azure Functions 프록시는 함수 호스트 구성의 routePrefix 속성을 유지하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="62328-205">The route property Azure Functions Proxies does not honor the routePrefix property of the Functions host configuration.</span></span> <span data-ttu-id="62328-206">/api 같은 접두사를 포함하려는 경우 경로 속성에 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="62328-206">If you want to include a prefix such as /api, it must be included in the route property.</span></span>

### <span data-ttu-id="62328-207"><a name="requestOverrides"></a>requestOverrides 개체 정의</span><span class="sxs-lookup"><span data-stu-id="62328-207"><a name="requestOverrides"></a>Define a requestOverrides object</span></span>

<span data-ttu-id="62328-208">requestOverrides 개체는 백 엔드 리소스가 호출될 때 요청에 대한 변경 내용을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="62328-208">The requestOverrides object defines changes made to the request when the back-end resource is called.</span></span> <span data-ttu-id="62328-209">개체는 다음 속성으로 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="62328-209">The object is defined by the following properties:</span></span>

* <span data-ttu-id="62328-210">**backend.request.method**: 백 엔드를 호출하는 데 사용될 HTTP 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="62328-210">**backend.request.method**: The HTTP method that's used to call the back end.</span></span>
* <span data-ttu-id="62328-211">**backend.request.querystring.\<ParameterName\>**: 백 엔드에 대한 호출에 설정할 수 있는 쿼리 문자열 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="62328-211">**backend.request.querystring.\<ParameterName\>**: A query string parameter that can be set for the call to the back end.</span></span> <span data-ttu-id="62328-212">*\<ParameterName\>*을 설정하려는 매개 변수 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="62328-212">Replace *\<ParameterName\>* with the name of the parameter that you want to set.</span></span> <span data-ttu-id="62328-213">빈 문자열이 제공되면 매개 변수는 백 엔드 요청에 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="62328-213">If the empty string is provided, the parameter is not included on the back-end request.</span></span>
* <span data-ttu-id="62328-214">**backend.request.headers.\<HeaderName\>**: 백 엔드 호출을 위해 설정할 수 있는 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="62328-214">**backend.request.headers.\<HeaderName\>**: A header that can be set for the call to the back end.</span></span> <span data-ttu-id="62328-215">*\<HeaderName\>*을 설정하려는 헤더 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="62328-215">Replace *\<HeaderName\>* with the name of the header that you want to set.</span></span> <span data-ttu-id="62328-216">빈 문자열을 제공하면 헤더는 백 엔드 요청에 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="62328-216">If you provide the empty string, the header is not included on the back-end request.</span></span>

<span data-ttu-id="62328-217">값은 응용 프로그램 설정 및 원래 클라이언트 요청의 매개 변수를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62328-217">Values can reference application settings and parameters from the original client request.</span></span>

<span data-ttu-id="62328-218">예제 구성은 다음과 유사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62328-218">An example configuration might look like the following:</span></span>

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "proxy1": {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/{test}"
            },
            "backendUri": "https://<AnotherApp>.azurewebsites.net/api/<FunctionName>",
            "requestOverrides": {
                "backend.request.headers.Accept": "application/xml",
                "backend.request.headers.x-functions-key": "%ANOTHERAPP_API_KEY%"
            }
        }
    }
}
```

### <span data-ttu-id="62328-219"><a name="responseOverrides"></a>responseOverrides 개체 정의</span><span class="sxs-lookup"><span data-stu-id="62328-219"><a name="responseOverrides"></a>Define a responseOverrides object</span></span>

<span data-ttu-id="62328-220">requestOverrides 개체는 클라이언트에 다시 전달된 응답에 대한 변경 내용을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="62328-220">The requestOverrides object defines changes that are made to the response that's passed back to the client.</span></span> <span data-ttu-id="62328-221">개체는 다음 속성으로 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="62328-221">The object is defined by the following properties:</span></span>

* <span data-ttu-id="62328-222">**response.statusCode**: 클라이언트에 반환할 HTTP 상태 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="62328-222">**response.statusCode**: The HTTP status code to be returned to the client.</span></span>
* <span data-ttu-id="62328-223">**response.statusReason**: 클라이언트에 반환할 HTTP 이유 구문입니다.</span><span class="sxs-lookup"><span data-stu-id="62328-223">**response.statusReason**: The HTTP reason phrase to be returned to the client.</span></span>
* <span data-ttu-id="62328-224">**response.body**: 클라이언트에 반환할 본문의 문자열 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="62328-224">**response.body**: The string representation of the body to be returned to the client.</span></span>
* <span data-ttu-id="62328-225">**response.headers.\<HeaderName\>**: 클라이언트에 대한 응답에 설정할 수 있는 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="62328-225">**response.headers.\<HeaderName\>**: A header that can be set for the response to the client.</span></span> <span data-ttu-id="62328-226">*\<HeaderName\>*을 설정하려는 헤더 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="62328-226">Replace *\<HeaderName\>* with the name of the header that you want to set.</span></span> <span data-ttu-id="62328-227">빈 문자열을 제공하면 헤더는 응답에 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="62328-227">If you provide the empty string, the header is not included on the response.</span></span>

<span data-ttu-id="62328-228">값은 응용 프로그램 설정, 원래 클라이언트 요청의 매개 변수 및 백 엔드 응답의 매개 변수를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62328-228">Values can reference application settings, parameters from the original client request, and parameters from the back-end response.</span></span>

<span data-ttu-id="62328-229">예제 구성은 다음과 유사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62328-229">An example configuration might look like the following:</span></span>

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "proxy1": {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/{test}"
            },
            "responseOverrides": {
                "response.body": "Hello, {test}",
                "response.headers.Content-Type": "text/plain"
            }
        }
    }
}
```
> [!NOTE] 
> <span data-ttu-id="62328-230">이 예제에서 분문은 직접 설정되므로 `backendUri` 속성이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="62328-230">In this example, the body is being set directly, so no `backendUri` property is needed.</span></span> <span data-ttu-id="62328-231">다음 예제에서는 모의 API에 Azure Functions 프록시를 어떻게 사용할 수 있는지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="62328-231">The example shows how you might use Azure Functions Proxies for mocking APIs.</span></span>

<span data-ttu-id="62328-232">[Azure Portal]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="62328-232">[Azure portal]: https://portal.azure.com</span></span>
<span data-ttu-id="62328-233">[HTTP 트리거]: https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#http-trigger</span><span class="sxs-lookup"><span data-stu-id="62328-233">[HTTP triggers]: https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#http-trigger</span></span>
[Modify the back-end request]: #modify-backend-request
[Modify the response]: #modify-response
<span data-ttu-id="62328-234">[requestOverrides 개체 정의]: #requestOverrides</span><span class="sxs-lookup"><span data-stu-id="62328-234">[Define a requestOverrides object]: #requestOverrides</span></span>
<span data-ttu-id="62328-235">[ 개체 정의]: #responseOverrides</span><span class="sxs-lookup"><span data-stu-id="62328-235">[Define a responseOverrides object]: #responseOverrides</span></span>
<span data-ttu-id="62328-236">[응용 프로그램 설정]: #use-appsettings</span><span class="sxs-lookup"><span data-stu-id="62328-236">[application settings]: #use-appsettings</span></span>
<span data-ttu-id="62328-237">[변수 사용]: #using-variables</span><span class="sxs-lookup"><span data-stu-id="62328-237">[Use variables]: #using-variables</span></span>
<span data-ttu-id="62328-238">[원래 클라이언트 요청의 매개 변수]: #request-parameters</span><span class="sxs-lookup"><span data-stu-id="62328-238">[parameters from the original client request]: #request-parameters</span></span>
<span data-ttu-id="62328-239">[백 엔드 응답의 매개 변수]: #response-parameters</span><span class="sxs-lookup"><span data-stu-id="62328-239">[parameters from the back-end response]: #response-parameters</span></span>

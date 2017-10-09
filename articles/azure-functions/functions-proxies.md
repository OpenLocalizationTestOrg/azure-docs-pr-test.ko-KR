---
title: "Azure 함수에서 프록시와 aaaWork | Microsoft Docs"
description: "방법의 개요 toouse Azure 함수 프록시"
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
ms.openlocfilehash: 4d94c89e8f8f2d2c771b01bae142bf9a4f3b7f2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="work-with-azure-functions-proxies-preview"></a><span data-ttu-id="f678b-103">Azure Functions 프록시 사용(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="f678b-103">Work with Azure Functions Proxies (preview)</span></span>

> [!NOTE] 
> <span data-ttu-id="f678b-104">Azure Functions 프록시는 현재 미리 보기 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-104">Azure Functions Proxies is currently in preview.</span></span> <span data-ttu-id="f678b-105">대금 청구 미리 보기, 하지만 표준 함수 tooproxy 실행을 적용 하는 동안 무료입니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-105">It is free while in preview, but standard Functions billing applies tooproxy executions.</span></span> <span data-ttu-id="f678b-106">자세한 내용은 [Azure Functions 가격 책정](https://azure.microsoft.com/pricing/details/functions/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f678b-106">For more information, see [Azure Functions pricing](https://azure.microsoft.com/pricing/details/functions/).</span></span>

<span data-ttu-id="f678b-107">이 문서에서는 설명 어떻게 tooconfigure Azure 함수 프록시와 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-107">This article explains how tooconfigure and work with Azure Functions Proxies.</span></span> <span data-ttu-id="f678b-108">이 기능을 사용하면 다른 리소스에서 구현된 함수 앱에 끝점을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-108">With this feature, you can specify endpoints on your function app that are implemented by another resource.</span></span> <span data-ttu-id="f678b-109">여전히 클라이언트에 대 한 단일 API 화면을 표시 하는 동안 여러 기능 앱 (예: 마이크로 서비스 아키텍처의 경우)에 이러한 프록시 toobreak 큰 API를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-109">You can use these proxies toobreak a large API into multiple function apps (as in a microservice architecture), while still presenting a single API surface for clients.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]


## <span data-ttu-id="f678b-110"><a name="enable"></a>Azure Functions 프록시 사용</span><span class="sxs-lookup"><span data-stu-id="f678b-110"><a name="enable"></a>Enable Azure Functions Proxies</span></span>

<span data-ttu-id="f678b-111">프록시는 기본적으로 사용하도록 설정되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-111">Proxies are not enabled by default.</span></span> <span data-ttu-id="f678b-112">Hello 기능을 해제 하지만 실행 되지 것입니다 프록시를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-112">You can create proxies while hello feature is disabled, but they will not execute.</span></span> <span data-ttu-id="f678b-113">tooenable 프록시 뒤 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-113">tooenable proxies, do hello following:</span></span>

1. <span data-ttu-id="f678b-114">열기 hello [Azure 포털], tooyour 함수 응용 프로그램을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-114">Open hello [Azure portal], and then go tooyour function app.</span></span>
2. <span data-ttu-id="f678b-115">**함수 앱 설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-115">Select **Function app settings**.</span></span>
3. <span data-ttu-id="f678b-116">스위치 **사용 Azure 함수 프록시 (미리 보기)** 너무**에**합니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-116">Switch **Enable Azure Functions Proxies (preview)** too**On**.</span></span>

<span data-ttu-id="f678b-117">또한 변수로 반환할 수 있습니다 여기 tooupdate hello 프록시 런타임 새 기능을 사용할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-117">You can also return here tooupdate hello proxy runtime as new features become available.</span></span>


## <span data-ttu-id="f678b-118"><a name="create"></a>프록시 만들기</span><span class="sxs-lookup"><span data-stu-id="f678b-118"><a name="create"></a>Create a proxy</span></span>

<span data-ttu-id="f678b-119">이 섹션에서는 a에서 프록시 toocreate 함수 포털 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-119">This section shows you how toocreate a proxy in hello Functions portal.</span></span>

1. <span data-ttu-id="f678b-120">열기 hello [Azure 포털], tooyour 함수 응용 프로그램을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-120">Open hello [Azure portal], and then go tooyour function app.</span></span>
2. <span data-ttu-id="f678b-121">Hello 왼쪽된 창에서 선택 **새 프록시**합니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-121">In hello left pane, select **New proxy**.</span></span>
3. <span data-ttu-id="f678b-122">프록시의 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-122">Provide a name for your proxy.</span></span>
4. <span data-ttu-id="f678b-123">Hello를 지정 하 여이 함수 응용 프로그램에 노출 되는 hello 끝점을 구성 **경로 템플릿을** 및 **HTTP 메서드**합니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-123">Configure hello endpoint that's exposed on this function app by specifying hello **route template** and **HTTP methods**.</span></span> <span data-ttu-id="f678b-124">이러한 매개 변수 동작에 대 한 따라 toohello 규칙 [HTTP 트리거]합니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-124">These parameters behave according toohello rules for [HTTP triggers].</span></span>
5. <span data-ttu-id="f678b-125">집합 hello **백 엔드 URL** tooanother 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-125">Set hello **backend URL** tooanother endpoint.</span></span> <span data-ttu-id="f678b-126">이러한 끝점은 다른 함수 앱의 함수이거나 다른 API일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-126">This endpoint could be a function in another function app, or it could be any other API.</span></span> <span data-ttu-id="f678b-127">hello 값 필요 toobe 정적이 고 참조할 수 있는 [응용 프로그램 설정] 및 [hello 원래 클라이언트 요청에서 매개 변수]합니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-127">hello value does not need toobe static, and it can reference [application settings] and [parameters from hello original client request].</span></span>
6. <span data-ttu-id="f678b-128">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-128">Click **Create**.</span></span>

<span data-ttu-id="f678b-129">이제 프록시는 함수 앱에서 새 끝점으로 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-129">Your proxy now exists as a new endpoint on your function app.</span></span> <span data-ttu-id="f678b-130">클라이언트 관점에서 해당 tooan Azure 함수에서 HttpTrigger 것합니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-130">From a client perspective, it is equivalent tooan HttpTrigger in Azure Functions.</span></span> <span data-ttu-id="f678b-131">Hello 프록시 URL을 복사 하 고 자주 사용 하 여 HTTP 클라이언트를 테스트 하 여 새 프록시를 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-131">You can try out your new proxy by copying hello Proxy URL and testing it with your favorite HTTP client.</span></span>

## <span data-ttu-id="f678b-132"><a name="modify-requests-responses"></a>요청 및 응답 수정</span><span class="sxs-lookup"><span data-stu-id="f678b-132"><a name="modify-requests-responses"></a>Modify requests and responses</span></span>

<span data-ttu-id="f678b-133">Azure 함수 프록시와 hello 백 엔드에서 요청 tooand 응답을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-133">With Azure Functions Proxies, you can modify requests tooand responses from hello back end.</span></span> <span data-ttu-id="f678b-134">이러한 변환은 [변수 사용]에 정의된 대로 변수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-134">These transformations can use variables as defined in [Use variables].</span></span>

### <span data-ttu-id="f678b-135"><a name="modify-backend-request"></a>Hello 백 엔드에서 요청을 수정</span><span class="sxs-lookup"><span data-stu-id="f678b-135"><a name="modify-backend-request"></a>Modify hello back-end request</span></span>

<span data-ttu-id="f678b-136">기본적으로 hello 백 엔드에서 요청 hello 원래 요청 항목의 복사본으로 초기화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-136">By default, hello back-end request is initialized as a copy of hello original request.</span></span> <span data-ttu-id="f678b-137">또한 toosetting hello 백 엔드 URL 변경 toohello HTTP 메서드, 헤더 및 쿼리 문자열 매개 변수를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-137">In addition toosetting hello back-end URL, you can make changes toohello HTTP method, headers, and query string parameters.</span></span> <span data-ttu-id="f678b-138">hello 수정된 값 참조할 수 [응용 프로그램 설정] 및 [hello 원래 클라이언트 요청에서 매개 변수]합니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-138">hello modified values can reference [application settings] and [parameters from hello original client request].</span></span>

<span data-ttu-id="f678b-139">현재 백 엔드 요청을 수정하기 위한 포털 환경은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-139">Currently, there is no portal experience for modifying back-end requests.</span></span> <span data-ttu-id="f678b-140">toolearn tooapply proxies.json에서이 기능 확인 하려면 어떻게 해야 [requestOverrides 개체 정의]합니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-140">toolearn how tooapply this capability from proxies.json, see [Define a requestOverrides object].</span></span>

### <span data-ttu-id="f678b-141"><a name="modify-response"></a>Hello 응답 수정</span><span class="sxs-lookup"><span data-stu-id="f678b-141"><a name="modify-response"></a>Modify hello response</span></span>

<span data-ttu-id="f678b-142">기본적으로 hello 클라이언트 응답 hello 백 엔드 응답의 복사본으로 초기화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-142">By default, hello client response is initialized as a copy of hello back-end response.</span></span> <span data-ttu-id="f678b-143">변경 내용 toohello 응답 상태 코드, 이유 구문, 헤더 및 본문을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-143">You can make changes toohello response's status code, reason phrase, headers, and body.</span></span> <span data-ttu-id="f678b-144">hello 수정된 값 참조할 수 [응용 프로그램 설정], [hello 원래 클라이언트 요청에서 매개 변수], 및 [hello 백 엔드 응답에서 매개 변수]합니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-144">hello modified values can reference [application settings], [parameters from hello original client request], and [parameters from hello back-end response].</span></span>

<span data-ttu-id="f678b-145">현재 응답을 수정하기 위한 포털 환경은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-145">Currently, there is no portal experience for modifying responses.</span></span> <span data-ttu-id="f678b-146">toolearn tooapply proxies.json에서이 기능 확인 하려면 어떻게 해야 [responseOverrides 개체 정의]합니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-146">toolearn how tooapply this capability from proxies.json, see [Define a responseOverrides object].</span></span>

## <span data-ttu-id="f678b-147"><a name="using-variables"></a>변수 사용</span><span class="sxs-lookup"><span data-stu-id="f678b-147"><a name="using-variables"></a>Use variables</span></span>

<span data-ttu-id="f678b-148">작업에 대 한 hello 구성 하지 않아도 toobe 정적입니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-148">hello configuration for a proxy does not need toobe static.</span></span> <span data-ttu-id="f678b-149">Hello 원래 요청, hello 백 엔드 응답 또는 응용 프로그램 설정에서 toouse 변수 조건 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-149">You can condition it toouse variables from hello original request, hello back-end response, or application settings.</span></span>

### <span data-ttu-id="f678b-150"><a name="request-parameters"></a>요청 매개 변수 참조</span><span class="sxs-lookup"><span data-stu-id="f678b-150"><a name="request-parameters"></a>Reference request parameters</span></span>

<span data-ttu-id="f678b-151">Toohello 백 엔드 URL 속성을 입력으로 또는 수정 요청 및 응답의 일부로 요청 매개 변수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-151">You can use request parameters as inputs toohello back-end URL property or as part of modifying requests and responses.</span></span> <span data-ttu-id="f678b-152">Hello 기본 프록시 구성에 지정 된 hello 경로 서식 파일에서 일부 매개 변수에 바인딩할 수 있으며 다른 hello 들어오는 요청의 속성에서 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-152">Some parameters can be bound from hello route template that's specified in hello base proxy configuration, and others can come from properties of hello incoming request.</span></span>

#### <a name="route-template-parameters"></a><span data-ttu-id="f678b-153">경로 템플릿 매개 변수</span><span class="sxs-lookup"><span data-stu-id="f678b-153">Route template parameters</span></span>
<span data-ttu-id="f678b-154">Hello 경로 템플릿을에 사용 되는 매개 변수 이름으로 참조 되는 사용 가능한 toobe 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-154">Parameters that are used in hello route template are available toobe referenced by name.</span></span> <span data-ttu-id="f678b-155">hello 매개 변수 이름은 중괄호 ({})에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-155">hello parameter names are enclosed in braces ({}).</span></span>

<span data-ttu-id="f678b-156">예를 들어, 프록시에는 경로 템플릿을 같은 경우 `/pets/{petId}`, hello 백 엔드 URL의 hello 값을 포함할 수 있습니다 `{petId}`에서 같이 `https://<AnotherApp>.azurewebsites.net/api/pets/{petId}`합니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-156">For example, if a proxy has a route template, such as `/pets/{petId}`, hello back-end URL can include hello value of `{petId}`, as in `https://<AnotherApp>.azurewebsites.net/api/pets/{petId}`.</span></span> <span data-ttu-id="f678b-157">Hello 경로 템플릿을에 와일드 카드와 같은 종료 `/api/{*restOfPath}`, 값 hello `{restOfPath}` hello 남은 hello 들어오는 요청에서 경로 세그먼트의 문자열 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-157">If hello route template terminates in a wildcard, such as `/api/{*restOfPath}`, hello value `{restOfPath}` is a string representation of hello remaining path segments from hello incoming request.</span></span>

#### <a name="additional-request-parameters"></a><span data-ttu-id="f678b-158">추가 요청 매개 변수</span><span class="sxs-lookup"><span data-stu-id="f678b-158">Additional request parameters</span></span>
<span data-ttu-id="f678b-159">또한 toohello 라우팅할 템플릿 매개 변수, 다음 값에는 hello 구성 값에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-159">In addition toohello route template parameters, hello following values can be used in config values:</span></span>

* <span data-ttu-id="f678b-160">**{request.method}** : hello hello 원래 요청에 사용 되는 HTTP 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-160">**{request.method}**: hello HTTP method that's used on hello original request.</span></span>
* <span data-ttu-id="f678b-161">**{request.headers 합니다. \<HeaderName\>}**: hello 원래 요청에서 읽을 수 있는 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-161">**{request.headers.\<HeaderName\>}**: A header that can be read from hello original request.</span></span> <span data-ttu-id="f678b-162">대체  *\<HeaderName\>*  tooread hello 헤더의 hello 이름으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-162">Replace *\<HeaderName\>* with hello name of hello header that you want tooread.</span></span> <span data-ttu-id="f678b-163">Hello 헤더 hello 요청에 포함 되어 있지 않으면, hello 값 hello 빈 문자열이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-163">If hello header is not included on hello request, hello value will be hello empty string.</span></span>
* <span data-ttu-id="f678b-164">**{request.querystring 합니다. \<ParameterName\>}**: hello 원래 요청에서 읽을 수 있는 쿼리 문자열 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-164">**{request.querystring.\<ParameterName\>}**: A query string parameter that can be read from hello original request.</span></span> <span data-ttu-id="f678b-165">대체  *\<ParameterName\>*  hello tooread 원하는 hello 매개 변수 이름으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-165">Replace *\<ParameterName\>* with hello name of hello parameter that you want tooread.</span></span> <span data-ttu-id="f678b-166">Hello 매개 변수는 hello 요청에 포함 되어 있지 않으면, hello 값 hello 빈 문자열이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-166">If hello parameter is not included on hello request, hello value will be hello empty string.</span></span>

### <span data-ttu-id="f678b-167"><a name="response-parameters"></a>백 엔드 응답 매개 변수 참조</span><span class="sxs-lookup"><span data-stu-id="f678b-167"><a name="response-parameters"></a>Reference back-end response parameters</span></span>

<span data-ttu-id="f678b-168">응답 매개 변수 수정 hello 응답 toohello 클라이언트의 일부로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-168">Response parameters can be used as part of modifying hello response toohello client.</span></span> <span data-ttu-id="f678b-169">다음 값에는 hello 구성 값에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-169">hello following values can be used in config values:</span></span>

* <span data-ttu-id="f678b-170">**{backend.response.statusCode}** : hello hello 백 엔드 응답에 반환 되는 HTTP 상태 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-170">**{backend.response.statusCode}**: hello HTTP status code that's returned on hello back-end response.</span></span>
* <span data-ttu-id="f678b-171">**{backend.response.statusReason}** : hello 백 엔드 응답에 반환 되는 HTTP hello 이유 구문입니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-171">**{backend.response.statusReason}**: hello HTTP reason phrase that's returned on hello back-end response.</span></span>
* <span data-ttu-id="f678b-172">**{backend.response.headers 합니다. \<HeaderName\>}**: hello 백 엔드 응답에서 읽을 수 있는 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-172">**{backend.response.headers.\<HeaderName\>}**: A header that can be read from hello back-end response.</span></span> <span data-ttu-id="f678b-173">대체  *\<HeaderName\>*  tooread hello 헤더의 hello 이름으로 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-173">Replace *\<HeaderName\>* with hello name of hello header you want tooread.</span></span> <span data-ttu-id="f678b-174">Hello 헤더 hello 요청에 포함 되어 있지 않으면, hello 값 hello 빈 문자열이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-174">If hello header is not included on hello request, hello value will be hello empty string.</span></span>

### <span data-ttu-id="f678b-175"><a name="use-appsettings"></a>응용 프로그램 설정 참조</span><span class="sxs-lookup"><span data-stu-id="f678b-175"><a name="use-appsettings"></a>Reference application settings</span></span>

<span data-ttu-id="f678b-176">참조할 수도 있습니다 [hello 함수 앱에 대해 정의 된 응용 프로그램 설정](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#develop) hello 설정 이름은 백분율 기호 (%)로 묶어 합니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-176">You can also reference [application settings defined for hello function app](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#develop) by surrounding hello setting name with percent signs (%).</span></span>

<span data-ttu-id="f678b-177">백 엔드 URL 예를 들어 *https://%ORDER_PROCESSING_HOST%/api/orders* "% ORDER_PROCESSING_HOST %" hello hello ORDER_PROCESSING_HOST 설정 값으로 대체 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-177">For example, a back-end URL of *https://%ORDER_PROCESSING_HOST%/api/orders* would have "%ORDER_PROCESSING_HOST%" replaced with hello value of hello ORDER_PROCESSING_HOST setting.</span></span>

> [!TIP] 
> <span data-ttu-id="f678b-178">배포 또는 테스트 환경이 여러 개 있는 경우 백 엔드 호스트에 대해 응용 프로그램 설정을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="f678b-178">Use application settings for back-end hosts when you have multiple deployments or test environments.</span></span> <span data-ttu-id="f678b-179">이렇게 할 수 있습니다는 항상 통신의 대상이 해당 환경에 대 한 다시 toohello 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-179">That way, you can make sure that you are always talking toohello right back end for that environment.</span></span>

## <a name="advanced-configuration"></a><span data-ttu-id="f678b-180">고급 구성</span><span class="sxs-lookup"><span data-stu-id="f678b-180">Advanced configuration</span></span>

<span data-ttu-id="f678b-181">구성 하는 hello 프록시 함수 응용 프로그램 디렉터리의 hello 루트에 있는 proxies.json 파일에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-181">hello proxies that you configure are stored in a proxies.json file, which is located in hello root of a function app directory.</span></span> <span data-ttu-id="f678b-182">수동으로이 파일을 편집 하 고 hello 중 하나를 사용 하는 경우 응용 프로그램의 일부분으로 배포할 수 [배포 방법](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment) 함수를 지 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-182">You can manually edit this file and deploy it as part of your app when you use any of hello [deployment methods](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment) that Functions supports.</span></span> <span data-ttu-id="f678b-183">hello 기능 이어야 합니다 [활성화](#enable) hello 파일 toobe 처리에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-183">hello feature must be [enabled](#enable) for hello file toobe processed.</span></span> 

> [!TIP] 
> <span data-ttu-id="f678b-184">Hello 배포 방법 중 하나를 설정 하지 않은 경우 있습니다 작업할 수도 hello 포털에서 hello proxies.json 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-184">If you have not set up one of hello deployment methods, you can also work with hello proxies.json file in hello portal.</span></span> <span data-ttu-id="f678b-185">선택 이동 tooyour 함수 앱 **플랫폼 기능**를 선택한 후 **응용 프로그램 서비스 편집기**합니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-185">Go tooyour function app, select **Platform features**, and then select **App Service Editor**.</span></span> <span data-ttu-id="f678b-186">이렇게 함으로써 함수 응용 프로그램의 hello 전체 파일 구조를 볼 수 있으며 다음 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-186">By doing so, you can view hello entire file structure of your function app and then make changes.</span></span>

<span data-ttu-id="f678b-187">Proxies.json은 명명된 프록시 및 해당 정의로 구성된 프록시 개체로 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-187">Proxies.json is defined by a proxies object, which is composed of named proxies and their definitions.</span></span> <span data-ttu-id="f678b-188">편집기에서 코드 완성을 지원하는 경우 필요에 따라 [JSON 스키마](http://json.schemastore.org/proxies)를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-188">Optionally, if your editor supports it, you can reference a [JSON schema](http://json.schemastore.org/proxies) for code completion.</span></span> <span data-ttu-id="f678b-189">파일의 예는 hello 다음과 같을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-189">An example file might look like hello following:</span></span>

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

<span data-ttu-id="f678b-190">각 프록시는 이름와 같은 *proxy1* hello 예제 앞에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-190">Each proxy has a friendly name, such as *proxy1* in hello preceding example.</span></span> <span data-ttu-id="f678b-191">프록시 정의 개체를 해당 하는 hello hello 다음과 같은 속성으로 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-191">hello corresponding proxy definition object is defined by hello following properties:</span></span>

* <span data-ttu-id="f678b-192">**matchCondition**: 필요 합니다--이 프록시의 hello 실행을 트리거하는 hello 요청을 정의 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-192">**matchCondition**: Required--an object defining hello requests that trigger hello execution of this proxy.</span></span> <span data-ttu-id="f678b-193">[HTTP 트리거]와 공유되는 두 가지 속성이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-193">It contains two properties that are shared with [HTTP triggers]:</span></span>
    * <span data-ttu-id="f678b-194">_메서드_: 프록시 hello hello HTTP 메서드 배열을에 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-194">_methods_: An array of hello HTTP methods that hello proxy responds to.</span></span> <span data-ttu-id="f678b-195">지정 하지 않으면 hello 프록시 hello 경로에 tooall HTTP 메서드에 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-195">If it is not specified, hello proxy responds tooall HTTP methods on hello route.</span></span>
    * <span data-ttu-id="f678b-196">_경로_: 필수-hello 경로 템플릿, Url 프록시 요청 제어 정의에 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-196">_route_: Required--defines hello route template, controlling which request URLs your proxy responds to.</span></span> <span data-ttu-id="f678b-197">HTTP 트리거와 달리 기본값이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-197">Unlike in HTTP triggers, there is no default value.</span></span>
* <span data-ttu-id="f678b-198">**backendUri**: hello 백 엔드 리소스 toowhich hello 요청의 hello URL 프록시 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-198">**backendUri**: hello URL of hello back-end resource toowhich hello request should be proxied.</span></span> <span data-ttu-id="f678b-199">이 값 hello 원래 클라이언트 요청에서 응용 프로그램 설정 및 매개 변수를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-199">This value can reference application settings and parameters from hello original client request.</span></span> <span data-ttu-id="f678b-200">이 속성을 포함하지 않으면 Azure Functions는 HTTP 200 OK로 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-200">If this property is not included, Azure Functions responds with an HTTP 200 OK.</span></span>
* <span data-ttu-id="f678b-201">**requestOverrides**: 변환 toohello 백 엔드에서 요청을 정의 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-201">**requestOverrides**: An object that defines transformations toohello back-end request.</span></span> <span data-ttu-id="f678b-202">[requestOverrides 개체 정의]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f678b-202">See [Define a requestOverrides object].</span></span>
* <span data-ttu-id="f678b-203">**responseOverrides**: 변환 toohello 클라이언트 응답을 정의 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-203">**responseOverrides**: An object that defines transformations toohello client response.</span></span> <span data-ttu-id="f678b-204">[responseOverrides 개체 정의]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f678b-204">See [Define a responseOverrides object].</span></span>

> [!NOTE] 
> <span data-ttu-id="f678b-205">hello 경로 속성 Azure 함수 프록시 hello 함수 호스트 구성의 hello routePrefix 속성을 준수 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-205">hello route property Azure Functions Proxies does not honor hello routePrefix property of hello Functions host configuration.</span></span> <span data-ttu-id="f678b-206">Tooinclude /api 같은 접두사를 사용 하도록 하려는 경우에 hello 경로 속성에 포함 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-206">If you want tooinclude a prefix such as /api, it must be included in hello route property.</span></span>

### <span data-ttu-id="f678b-207"><a name="requestOverrides"></a>requestOverrides 개체 정의</span><span class="sxs-lookup"><span data-stu-id="f678b-207"><a name="requestOverrides"></a>Define a requestOverrides object</span></span>

<span data-ttu-id="f678b-208">hello requestOverrides 개체 정의 toohello 요청 될 때 변경 hello 백 엔드 리소스 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-208">hello requestOverrides object defines changes made toohello request when hello back-end resource is called.</span></span> <span data-ttu-id="f678b-209">hello 개체 hello 다음과 같은 속성으로 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-209">hello object is defined by hello following properties:</span></span>

* <span data-ttu-id="f678b-210">**backend.request.method**: hello toocall hello 백 엔드를 사용 하는 HTTP 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-210">**backend.request.method**: hello HTTP method that's used toocall hello back end.</span></span>
* <span data-ttu-id="f678b-211">**backend.request.querystring 합니다. \<ParameterName\>**: hello 호출 toohello 백 엔드에 설정 될 수 있는 쿼리 문자열 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-211">**backend.request.querystring.\<ParameterName\>**: A query string parameter that can be set for hello call toohello back end.</span></span> <span data-ttu-id="f678b-212">대체  *\<ParameterName\>*  hello tooset 원하는 hello 매개 변수 이름으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-212">Replace *\<ParameterName\>* with hello name of hello parameter that you want tooset.</span></span> <span data-ttu-id="f678b-213">Hello 빈 문자열이 지정 된 hello 매개 변수는 hello 백 엔드에서 요청에 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-213">If hello empty string is provided, hello parameter is not included on hello back-end request.</span></span>
* <span data-ttu-id="f678b-214">**backend.request.headers 합니다. \<HeaderName\>**: hello 호출 toohello 백 엔드에 설정 될 수 있는 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-214">**backend.request.headers.\<HeaderName\>**: A header that can be set for hello call toohello back end.</span></span> <span data-ttu-id="f678b-215">대체  *\<HeaderName\>*  tooset hello 헤더의 hello 이름으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-215">Replace *\<HeaderName\>* with hello name of hello header that you want tooset.</span></span> <span data-ttu-id="f678b-216">Hello 빈 문자열을 제공 하는 경우 hello 헤더 hello 백 엔드에서 요청에 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-216">If you provide hello empty string, hello header is not included on hello back-end request.</span></span>

<span data-ttu-id="f678b-217">값은 hello 원래 클라이언트 요청에서 응용 프로그램 설정 및 매개 변수를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-217">Values can reference application settings and parameters from hello original client request.</span></span>

<span data-ttu-id="f678b-218">예제 구성 hello 다음과 같을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-218">An example configuration might look like hello following:</span></span>

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

### <span data-ttu-id="f678b-219"><a name="responseOverrides"></a>responseOverrides 개체 정의</span><span class="sxs-lookup"><span data-stu-id="f678b-219"><a name="responseOverrides"></a>Define a responseOverrides object</span></span>

<span data-ttu-id="f678b-220">hello requestOverrides 개체 정의 뒤로 toohello 클라이언트 통과 toohello 응답 적용 된 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-220">hello requestOverrides object defines changes that are made toohello response that's passed back toohello client.</span></span> <span data-ttu-id="f678b-221">hello 개체 hello 다음과 같은 속성으로 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-221">hello object is defined by hello following properties:</span></span>

* <span data-ttu-id="f678b-222">**response.statusCode**: hello HTTP 상태 코드 toobe toohello 클라이언트를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-222">**response.statusCode**: hello HTTP status code toobe returned toohello client.</span></span>
* <span data-ttu-id="f678b-223">**response.statusReason**: hello HTTP 이유 구 toobe toohello 클라이언트를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-223">**response.statusReason**: hello HTTP reason phrase toobe returned toohello client.</span></span>
* <span data-ttu-id="f678b-224">**response.body**: hello 본문 toobe의 문자열 표현을 hello toohello 클라이언트를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-224">**response.body**: hello string representation of hello body toobe returned toohello client.</span></span>
* <span data-ttu-id="f678b-225">**response.headers 합니다. \<HeaderName\>**: hello 응답 toohello 클라이언트에 대해 설정할 수 있는 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-225">**response.headers.\<HeaderName\>**: A header that can be set for hello response toohello client.</span></span> <span data-ttu-id="f678b-226">대체  *\<HeaderName\>*  tooset hello 헤더의 hello 이름으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-226">Replace *\<HeaderName\>* with hello name of hello header that you want tooset.</span></span> <span data-ttu-id="f678b-227">Hello 빈 문자열을 제공 하는 경우 hello 헤더 hello 응답에 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-227">If you provide hello empty string, hello header is not included on hello response.</span></span>

<span data-ttu-id="f678b-228">값은 hello 백 엔드 응답에서 응용 프로그램 설정, hello 원래 클라이언트 요청에서 매개 변수 및 매개 변수를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-228">Values can reference application settings, parameters from hello original client request, and parameters from hello back-end response.</span></span>

<span data-ttu-id="f678b-229">예제 구성 hello 다음과 같을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-229">An example configuration might look like hello following:</span></span>

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
> <span data-ttu-id="f678b-230">이 예제에서는 hello 본문 설정 되어 직접 하므로 아니요 `backendUri` 속성이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-230">In this example, hello body is being set directly, so no `backendUri` property is needed.</span></span> <span data-ttu-id="f678b-231">hello 예제 모의 Api에 대 한 Azure 기능 프록시를 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f678b-231">hello example shows how you might use Azure Functions Proxies for mocking APIs.</span></span>

[Azure 포털]: https://portal.azure.com
[HTTP 트리거]: https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#http-trigger
[Modify hello back-end request]: #modify-backend-request
[Modify hello response]: #modify-response
[requestOverrides 개체 정의]: #requestOverrides
[responseOverrides 개체 정의]: #responseOverrides
[응용 프로그램 설정]: #use-appsettings
[변수 사용]: #using-variables
[hello 원래 클라이언트 요청에서 매개 변수]: #request-parameters
[hello 백 엔드 응답에서 매개 변수]: #response-parameters

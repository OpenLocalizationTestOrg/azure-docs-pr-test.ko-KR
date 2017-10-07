---
title: "hello Azure Active Directory v2.0 끝점에 대 한 aaaApp 형식 | Microsoft Docs"
description: "응용 프로그램 및 hello Azure Active Directory v2.0 끝점에서 지 원하는 시나리오 hello 형식입니다."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 494a06b8-0f9b-44e1-a7a2-d728cf2077ae
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: db95c88d6865abac8ce80378ccd6b63cb38e0a01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="app-types-for-hello-azure-active-directory-v20-endpoint"></a><span data-ttu-id="24fd6-103">Hello Azure Active Directory v2.0 끝점에 대 한 응용 프로그램 형식</span><span class="sxs-lookup"><span data-stu-id="24fd6-103">App types for hello Azure Active Directory v2.0 endpoint</span></span>
<span data-ttu-id="24fd6-104">hello Azure Active Directory (Azure AD) v 2.0 끝점 인증에 대 한 지원의 업계 표준 프로토콜에 따라 모든 최신 응용 프로그램 아키텍처의 다양 한 [OAuth 2.0, OpenID Connect](active-directory-v2-protocols.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="24fd6-104">hello Azure Active Directory (Azure AD) v2.0 endpoint supports authentication for a variety of modern app architectures, all of them based on industry-standard protocols [OAuth 2.0 or OpenID Connect](active-directory-v2-protocols.md).</span></span> <span data-ttu-id="24fd6-105">이 문서에서는 hello 유형의 기본 설정된 언어 또는 플랫폼에 관계 없이 Azure AD v 2.0을 사용 하 여 빌드할 수 있는 앱을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="24fd6-105">This article describes hello types of apps that you can build by using Azure AD v2.0, regardless of your preferred language or platform.</span></span> <span data-ttu-id="24fd6-106">hello이 문서의 정보는 하기 전에 높은 수준의 시나리오를 이해 하는 디자인 된 toohelp [hello 코드 작업 시작](active-directory-appmodel-v2-overview.md#getting-started)합니다.</span><span class="sxs-lookup"><span data-stu-id="24fd6-106">hello information in this article is designed toohelp you understand high-level scenarios before you [start working with hello code](active-directory-appmodel-v2-overview.md#getting-started).</span></span>

> [!NOTE]
> <span data-ttu-id="24fd6-107">hello v2.0 끝점은 모든 Azure Active Directory 시나리오 및 기능을 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="24fd6-107">hello v2.0 endpoint doesn't support all Azure Active Directory scenarios and features.</span></span> <span data-ttu-id="24fd6-108">에 대해 알아보세요 hello v2.0 끝점을 사용 해야 하는지를 toodetermine [v2.0 제한](active-directory-v2-limitations.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="24fd6-108">toodetermine whether you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="hello-basics"></a><span data-ttu-id="24fd6-109">hello 기본 사항</span><span class="sxs-lookup"><span data-stu-id="24fd6-109">hello basics</span></span>
<span data-ttu-id="24fd6-110">Hello의 hello v2.0 끝점을 사용 하 여 각 앱을 등록 해야 [Microsoft 응용 프로그램 등록 포털](https://apps.dev.microsoft.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="24fd6-110">You must register each app that uses hello v2.0 endpoint in hello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com).</span></span> <span data-ttu-id="24fd6-111">hello 응용 프로그램 등록 프로세스는 수집 하 고 앱에 대 한 이러한 값을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="24fd6-111">hello app registration process collects and assigns these values for your app:</span></span>

* <span data-ttu-id="24fd6-112">앱을 고유하게 식별하는 **응용 프로그램 ID**</span><span class="sxs-lookup"><span data-stu-id="24fd6-112">An **Application ID** that uniquely identifies your app</span></span>
* <span data-ttu-id="24fd6-113">A **리디렉션 URI** toodirect 응답 백 tooyour 응용 프로그램을 사용할 수 있는</span><span class="sxs-lookup"><span data-stu-id="24fd6-113">A **Redirect URI** that you can use toodirect responses back tooyour app</span></span>
* <span data-ttu-id="24fd6-114">다른 몇 가지 시나리오 관련 값.</span><span class="sxs-lookup"><span data-stu-id="24fd6-114">A few other scenario-specific values</span></span>

<span data-ttu-id="24fd6-115">자세한 내용은 자세한 방법을 너무[앱을 등록](active-directory-v2-app-registration.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="24fd6-115">For details, learn how too[register an app](active-directory-v2-app-registration.md).</span></span>

<span data-ttu-id="24fd6-116">Hello 앱 등록 되 면 hello 앱 toohello Azure AD v2.0 끝점 요청을 전송 하 여 Azure AD와 통신 합니다.</span><span class="sxs-lookup"><span data-stu-id="24fd6-116">After hello app is registered, hello app communicates with Azure AD by sending requests toohello Azure AD v2.0 endpoint.</span></span> <span data-ttu-id="24fd6-117">오픈 소스 프레임 워크 및 이러한 요청의 hello 세부 사항을 처리 하는 라이브러리를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="24fd6-117">We provide open-source frameworks and libraries that handle hello details of these requests.</span></span> <span data-ttu-id="24fd6-118">있습니다 hello 옵션 tooimplement hello 인증 논리 직접 만들어 요청 toothese 끝점:</span><span class="sxs-lookup"><span data-stu-id="24fd6-118">You also have hello option tooimplement hello authentication logic yourself by creating requests toothese endpoints:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
https://login.microsoftonline.com/common/oauth2/v2.0/token
```
<!-- TODO: Need a page for libraries toolink too-->

## <a name="web-apps"></a><span data-ttu-id="24fd6-119">웹 앱</span><span class="sxs-lookup"><span data-stu-id="24fd6-119">Web apps</span></span>
<span data-ttu-id="24fd6-120">웹 응용 프로그램 (.NET, PHP, Java, Ruby, Python, 노드)는 hello 브라우저를 통해 사용자 액세스를 사용할 수 있습니다 [OpenID Connect](active-directory-v2-protocols.md) 사용자 로그인에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="24fd6-120">For web apps (.NET, PHP, Java, Ruby, Python, Node) that hello user accesses through a browser, you can use [OpenID Connect](active-directory-v2-protocols.md) for user sign-in.</span></span> <span data-ttu-id="24fd6-121">OpenID Connect의 hello 웹 응용 프로그램 ID 토큰을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="24fd6-121">In OpenID Connect, hello web app receives an ID token.</span></span> <span data-ttu-id="24fd6-122">ID 토큰은 hello 사용자의 id를 확인 하 고 클레임의 hello 형태로 hello 사용자에 대 한 정보를 제공 하는 보안 토큰:</span><span class="sxs-lookup"><span data-stu-id="24fd6-122">An ID token is a security token that verifies hello user's identity and provides information about hello user in hello form of claims:</span></span>

```
// Partial raw ID token
eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6ImtyaU1QZG1Cd...

// Partial content of a decoded ID token
{
    "name": "John Smith",
    "email": "john.smith@gmail.com",
    "oid": "d9674823-dffc-4e3f-a6eb-62fe4bd48a58"
    ...
}
```

<span data-ttu-id="24fd6-123">토큰 및 클레임 hello에서 사용할 수 있는 tooan 응용 프로그램은 hello 형식 모두에 대해 학습할 수 있는 [v2.0 토큰 참조](active-directory-v2-tokens.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="24fd6-123">You can learn about all hello types of tokens and claims that are available tooan app in hello [v2.0 tokens reference](active-directory-v2-tokens.md).</span></span>

<span data-ttu-id="24fd6-124">웹 서버 응용 프로그램 hello 로그인 인증 흐름 같은 대략적인 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="24fd6-124">In web server apps, hello sign-in authentication flow takes these high-level steps:</span></span>

![웹앱 인증 흐름](../../media/active-directory-v2-flows/convergence_scenarios_webapp.png)

<span data-ttu-id="24fd6-126">Hello v2.0 끝점에서 수신 되는 공개 서명 키 hello ID 토큰을 확인 하 여 hello 사용자의 id를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24fd6-126">You can ensure hello user's identity by validating hello ID token with a public signing key that is received from hello v2.0 endpoint.</span></span> <span data-ttu-id="24fd6-127">다음 페이지 요청에 사용 되는 tooidentify hello 사용자 일 수 있는 세션 쿠키 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="24fd6-127">A session cookie is set, which can be used tooidentify hello user on subsequent page requests.</span></span>

<span data-ttu-id="24fd6-128">우리의 v 2.0에서 toosee 작업 시도 hello 웹 앱에 로그인 코드 중 하나에서이 시나리오 샘플 [시작](active-directory-appmodel-v2-overview.md#getting-started) 섹션.</span><span class="sxs-lookup"><span data-stu-id="24fd6-128">toosee this scenario in action, try one of hello web app sign-in code samples in our v2.0 [Getting Started](active-directory-appmodel-v2-overview.md#getting-started) section.</span></span>

<span data-ttu-id="24fd6-129">또한 toosimple 로그인, 웹 서버 앱 tooaccess REST API와 같은 다른 웹 서비스를 필요로 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24fd6-129">In addition toosimple sign-in, a web server app might need tooaccess another web service, such as a REST API.</span></span> <span data-ttu-id="24fd6-130">이 경우 hello 웹 서버 응용 프로그램은에 참여 결합 된 OAuth 2.0 및 OpenID Connect 흐름 hello를 사용 하 여 [OAuth 2.0 인증 코드 흐름](active-directory-v2-protocols.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="24fd6-130">In this case, hello web server app engages in a combined OpenID Connect and OAuth 2.0 flow, by using hello [OAuth 2.0 authorization code flow](active-directory-v2-protocols.md).</span></span> <span data-ttu-id="24fd6-131">이 시나리오에 대한 자세한 내용은 [웹앱 및 Web API 시작](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="24fd6-131">For more information about this scenario, read about [getting started with web apps and Web APIs](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md).</span></span>

## <a name="web-apis"></a><span data-ttu-id="24fd6-132">Web API</span><span class="sxs-lookup"><span data-stu-id="24fd6-132">Web APIs</span></span>
<span data-ttu-id="24fd6-133">Hello v2.0 끝점 toosecure와 같은 웹 서비스 응용 프로그램의 RESTful 웹 API를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24fd6-133">You can use hello v2.0 endpoint toosecure web services, such as your app's RESTful Web API.</span></span> <span data-ttu-id="24fd6-134">ID 토큰 및 세션 쿠키는 대신 웹 API를 사용 하 여 OAuth 2.0 액세스 토큰 toosecure의 데이터 및 tooauthenticate 들어오는 요청입니다.</span><span class="sxs-lookup"><span data-stu-id="24fd6-134">Instead of ID tokens and session cookies, a Web API uses an OAuth 2.0 access token toosecure its data and tooauthenticate incoming requests.</span></span> <span data-ttu-id="24fd6-135">웹 API의 hello 호출자의 HTTP 요청을 다음과 같이 hello 인증 헤더에 액세스 토큰을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="24fd6-135">hello caller of a Web API appends an access token in hello authorization header of an HTTP request, like this:</span></span>

```
GET /api/items HTTP/1.1
Host: www.mywebapi.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6...
Accept: application/json
...
```

<span data-ttu-id="24fd6-136">웹 API hello hello 액세스 토큰에서 인코딩 되는 클레임에서 hello 호출자에 대 한 hello 액세스 토큰 tooverify hello API 호출자의 id 및 tooextract 정보를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="24fd6-136">hello Web API uses hello access token tooverify hello API caller's identity and tooextract information about hello caller from claims that are encoded in hello access token.</span></span> <span data-ttu-id="24fd6-137">토큰 및 클레임을 사용할 수 있는 tooan 앱 hello 형식 모두에 대해 toolearn 참조 hello [v2.0 토큰 참조](active-directory-v2-tokens.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="24fd6-137">toolearn about all hello types of tokens and claims that are available tooan app, see hello [v2.0 tokens reference](active-directory-v2-tokens.md).</span></span>

<span data-ttu-id="24fd6-138">웹 API에 사용자가 hello 전원 tooopt 제공 하거나 권한을 라고도 노출 하 여 특정 기능이 나 데이터 옵트아웃 수 [범위](active-directory-v2-scopes.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="24fd6-138">A Web API can give users hello power tooopt in or opt out of specific functionality or data by exposing permissions, also known as [scopes](active-directory-v2-scopes.md).</span></span> <span data-ttu-id="24fd6-139">호출 응용 프로그램 tooacquire 권한 tooa 범위, hello 사용자 toohello 범위는 흐름 중 동의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="24fd6-139">For a calling app tooacquire permission tooa scope, hello user must consent toohello scope during a flow.</span></span> <span data-ttu-id="24fd6-140">hello v2.0 끝점 권한에 대 한 hello 사용자에 게 요청 하 고 모든 액세스 토큰에 사용 권한을 웹 API 수신 하는 hello 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="24fd6-140">hello v2.0 endpoint asks hello user for permission, and then records permissions in all access tokens that hello Web API receives.</span></span> <span data-ttu-id="24fd6-141">hello 웹 API에는 각 호출에서 수신 하 고 인증 검사를 수행 hello 액세스 토큰을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="24fd6-141">hello Web API validates hello access tokens it receives on each call and performs authorization checks.</span></span>

<span data-ttu-id="24fd6-142">Web API는 웹 서버 앱, 데스크톱 및 모바일 앱, 단일 페이지 앱, 서버 쪽 데몬 및 다른 Web API까지 포함하여 모든 유형의 앱에서 액세스 토큰을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24fd6-142">A Web API can receive access tokens from all types of apps, including web server apps, desktop and mobile apps, single-page apps, server-side daemons, and even other Web APIs.</span></span> <span data-ttu-id="24fd6-143">hello 웹 API에 대 한 상위 수준 흐름은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="24fd6-143">hello high-level flow for a Web API looks like this:</span></span>

![Web API 인증 흐름](../../media/active-directory-v2-flows/convergence_scenarios_webapi.png)

<span data-ttu-id="24fd6-145">toosecure OAuth2 액세스 토큰을 체크 아웃 hello 웹 API 코드를 사용 하 여 Web API에서 샘플링 하는 방법을 toolearn 우리의 [시작](active-directory-appmodel-v2-overview.md#getting-started) 섹션.</span><span class="sxs-lookup"><span data-stu-id="24fd6-145">toolearn how toosecure a Web API by using OAuth2 access tokens, check out hello Web API code samples in our [Getting Started](active-directory-appmodel-v2-overview.md#getting-started) section.</span></span>

<span data-ttu-id="24fd6-146">대부분의 경우에서 web Api는 toomake tooother 다운스트림 웹 Api를 Azure Active Directory를 통해 보안이 유지 되는 아웃 바운드 요청도 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="24fd6-146">In many cases, web APIs also need toomake outbound requests tooother downstream web APIs secured by Azure Active Directory.</span></span>  <span data-ttu-id="24fd6-147">toodo, 웹 Api 활용할 수 Azure AD의 **를 대신 하 여의에서** 흐름 hello web API tooexchange 아웃 바운드 요청에 사용 되는 다른 액세스 토큰 toobe에 대 한 수신 액세스 토큰을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="24fd6-147">toodo so, web APIs can take advantage of Azure AD's **On Behalf Of** flow, which allows hello web API tooexchange an incoming access token for another access token toobe used in outbound requests.</span></span>  <span data-ttu-id="24fd6-148">에 설명 된 hello v 2.0 끝점의 흐름을 대신 하 여 [여기에 대해 자세히 설명](active-directory-v2-protocols-oauth-on-behalf-of.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="24fd6-148">hello v2.0 endpoint's On Behalf Of flow is described in [detail here](active-directory-v2-protocols-oauth-on-behalf-of.md).</span></span>

## <a name="mobile-and-native-apps"></a><span data-ttu-id="24fd6-149">모바일 및 네이티브 앱</span><span class="sxs-lookup"><span data-stu-id="24fd6-149">Mobile and native apps</span></span>
<span data-ttu-id="24fd6-150">Tooaccess 백 엔드 서비스 또는 웹 Api 데이터를 저장 하 고 사용자를 대신 하는 기능을 수행 하는 장치 설치 된 앱은 모바일 및 데스크톱 앱 필요한 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="24fd6-150">Device-installed apps, such as mobile and desktop apps, often need tooaccess back-end services or Web APIs that store data and perform functions on behalf of a user.</span></span> <span data-ttu-id="24fd6-151">이러한 앱 hello를 사용 하 여 로그인 및 권한 부여 tooback 간 서비스를 추가할 수 [OAuth 2.0 인증 코드 흐름](active-directory-v2-protocols-oauth-code.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="24fd6-151">These apps can add sign-in and authorization tooback-end services by using hello [OAuth 2.0 authorization code flow](active-directory-v2-protocols-oauth-code.md).</span></span>

<span data-ttu-id="24fd6-152">이 흐름에서 hello 앱 hello 사용자가 로그인 할 때 hello v2.0 끝점에서 인증 코드를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="24fd6-152">In this flow, hello app receives an authorization code from hello v2.0 endpoint when hello user signs in.</span></span> <span data-ttu-id="24fd6-153">hello 권한 부여 코드 나타냅니다 hello hello 사용자가 로그인를 위해 응용 프로그램의 사용 권한 toocall 백 엔드 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="24fd6-153">hello authorization code represents hello app's permission toocall back-end services on behalf of hello user who is signed in.</span></span> <span data-ttu-id="24fd6-154">hello 앱 OAuth 2.0 액세스 토큰 및 새로 고침 토큰에 대 한 hello 백그라운드로 hello 인증 코드를 교환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24fd6-154">hello app can exchange hello authorization code in hello background for an OAuth 2.0 access token and a refresh token.</span></span> <span data-ttu-id="24fd6-155">hello 앱 HTTP 요청 시에서 hello 액세스 토큰 tooauthenticate tooWeb Api를 사용 하 여 하 고 이전 액세스 토큰이 만료 되 면 hello 새로 고침 토큰 tooget 새 액세스 토큰을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24fd6-155">hello app can use hello access token tooauthenticate tooWeb APIs in HTTP requests, and use hello refresh token tooget new access tokens when older access tokens expire.</span></span>

![네이티브 앱 인증 흐름](../../media/active-directory-v2-flows/convergence_scenarios_native.png)

## <a name="single-page-apps-javascript"></a><span data-ttu-id="24fd6-157">단일 페이지 앱(JavaScript)</span><span class="sxs-lookup"><span data-stu-id="24fd6-157">Single-page apps (JavaScript)</span></span>
<span data-ttu-id="24fd6-158">대부분의 최신 앱에는 주로 Javascript로 작성되고 AngularJS, Ember.js, Durandal 등과 같은 프레임워크로도 작성되는</span><span class="sxs-lookup"><span data-stu-id="24fd6-158">Many modern apps have a single-page app front end that primarily is written in JavaScript.</span></span> <span data-ttu-id="24fd6-159">단일 페이지 앱 프런트 엔드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24fd6-159">Often, it's written by using a framework like AngularJS, Ember.js, or Durandal.js.</span></span> <span data-ttu-id="24fd6-160">Azure AD hello v2.0 끝점 hello를 사용 하 여 이러한 응용 프로그램 지원 [OAuth 2.0 암시적 흐름](active-directory-v2-protocols-implicit.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="24fd6-160">hello Azure AD v2.0 endpoint supports these apps by using hello [OAuth 2.0 implicit flow](active-directory-v2-protocols-implicit.md).</span></span>

<span data-ttu-id="24fd6-161">이 흐름에서 hello 앱에서 hello에서 직접 토큰을 수신 v2.0 모든 서버 간 교환 하지 않고 끝점에 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="24fd6-161">In this flow, hello app receives tokens directly from hello v2.0 authorize endpoint, without any server-to-server exchanges.</span></span> <span data-ttu-id="24fd6-162">모든 인증 논리 및 세션 처리는 전적으로 추가 하는 페이지 리디렉션도 없이 hello JavaScript 클라이언트에서 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="24fd6-162">All authentication logic and session handling takes place entirely in hello JavaScript client, without extra page redirects.</span></span>

![암시적 인증 흐름](../../media/active-directory-v2-flows/convergence_scenarios_implicit.png)

<span data-ttu-id="24fd6-164">toosee 작업에서이 시나리오 중 하나를 시도 hello 단일 페이지 응용 프로그램 코드 샘플에서는 우리의 [시작](active-directory-appmodel-v2-overview.md#getting-started) 섹션.</span><span class="sxs-lookup"><span data-stu-id="24fd6-164">toosee this scenario in action, try one of hello single-page app code samples in our [Getting Started](active-directory-appmodel-v2-overview.md#getting-started) section.</span></span>

## <a name="daemons-and-server-side-apps"></a><span data-ttu-id="24fd6-165">디먼 및 서버 쪽 앱</span><span class="sxs-lookup"><span data-stu-id="24fd6-165">Daemons and server-side apps</span></span>
<span data-ttu-id="24fd6-166">장기 실행 프로세스 또는 사용자와 상호 작용 없이 작동 하는 앱 tooaccess 웹 Api와 같은 리소스를 보호 하는 방법이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="24fd6-166">Apps that have long-running processes or that operate without interaction with a user also need a way tooaccess secured resources, such as Web APIs.</span></span> <span data-ttu-id="24fd6-167">이러한 응용 프로그램에서 인증 하 고 hello 응용 프로그램의 id를 사용 하 여 토큰을 가져올 수 대신 사용자의 id hello OAuth 2.0 클라이언트 자격 증명 흐름을 위임 합니다.</span><span class="sxs-lookup"><span data-stu-id="24fd6-167">These apps can authenticate and get tokens by using hello app's identity, rather than a user's delegated identity, with hello OAuth 2.0 client credentials flow.</span></span>

<span data-ttu-id="24fd6-168">이 흐름에서 hello와 직접 상호 작용 hello 앱 `/token` 끝점 tooobtain 끝점:</span><span class="sxs-lookup"><span data-stu-id="24fd6-168">In this flow, hello app interacts directly with hello `/token` endpoint tooobtain endpoints:</span></span>

![디먼 앱 인증 흐름](../../media/active-directory-v2-flows/convergence_scenarios_daemon.png)

<span data-ttu-id="24fd6-170">toobuild 데몬 앱에서 hello 클라이언트 자격 증명 설명서를 참조 하십시오. 우리의 [시작](active-directory-appmodel-v2-overview.md#getting-started) 섹션 또는 시도 [.NET 예제 응용 프로그램](https://github.com/Azure-Samples/active-directory-dotnet-daemon-v2)합니다.</span><span class="sxs-lookup"><span data-stu-id="24fd6-170">toobuild a daemon app, see hello client credentials documentation in our [Getting Started](active-directory-appmodel-v2-overview.md#getting-started) section, or try a [.NET sample app](https://github.com/Azure-Samples/active-directory-dotnet-daemon-v2).</span></span>

---
title: "Azure Active Directory v2.0 끝점에 대한 앱 형식 | Microsoft Docs"
description: "Azure Active Directory v2.0 끝점에서 지원되는 앱 형식 및 시나리오입니다."
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
ms.openlocfilehash: 9d59e7f0e8f326c40be86e199d7712f6c565cc13
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="app-types-for-the-azure-active-directory-v20-endpoint"></a><span data-ttu-id="46f36-103">Azure Active Directory v2.0 끝점에 대한 앱 형식</span><span class="sxs-lookup"><span data-stu-id="46f36-103">App types for the Azure Active Directory v2.0 endpoint</span></span>
<span data-ttu-id="46f36-104">Azure AD(Azure Active Directory) v2.0 끝점은 모두 업계 표준 프로토콜 [OAuth 2.0 또는 OpenID Connect](active-directory-v2-protocols.md)를 기반으로 하는 다양한 최신 앱 아키텍처에 대한 인증을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="46f36-104">The Azure Active Directory (Azure AD) v2.0 endpoint supports authentication for a variety of modern app architectures, all of them based on industry-standard protocols [OAuth 2.0 or OpenID Connect](active-directory-v2-protocols.md).</span></span> <span data-ttu-id="46f36-105">이 문서에서는 기본 설정 언어 또는 플랫폼에 관계없이 Azure AD v2.0을 사용하여 빌드할 수 있는 앱 형식을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="46f36-105">This article describes the types of apps that you can build by using Azure AD v2.0, regardless of your preferred language or platform.</span></span> <span data-ttu-id="46f36-106">이 문서의 정보는 [코드 작업을 시작](active-directory-appmodel-v2-overview.md#getting-started)하기 전에 개략적인 시나리오를 이해하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="46f36-106">The information in this article is designed to help you understand high-level scenarios before you [start working with the code](active-directory-appmodel-v2-overview.md#getting-started).</span></span>

> [!NOTE]
> <span data-ttu-id="46f36-107">v2.0 끝점에서는 일부 Azure Active Directory 시나리오 및 기능만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="46f36-107">The v2.0 endpoint doesn't support all Azure Active Directory scenarios and features.</span></span> <span data-ttu-id="46f36-108">v2.0 끝점을 사용해야 하는지 확인하려면 [v2.0 제한 사항](active-directory-v2-limitations.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="46f36-108">To determine whether you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="the-basics"></a><span data-ttu-id="46f36-109">기본 사항</span><span class="sxs-lookup"><span data-stu-id="46f36-109">The basics</span></span>
<span data-ttu-id="46f36-110">v2.0 끝점을 사용하는 각 앱을 [Microsoft 응용 프로그램 등록 포털](https://apps.dev.microsoft.com)에 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="46f36-110">You must register each app that uses the v2.0 endpoint in the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com).</span></span> <span data-ttu-id="46f36-111">앱 등록 프로세스는 앱에 대한 다음 값을 수집하고 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="46f36-111">The app registration process collects and assigns these values for your app:</span></span>

* <span data-ttu-id="46f36-112">앱을 고유하게 식별하는 **응용 프로그램 ID**</span><span class="sxs-lookup"><span data-stu-id="46f36-112">An **Application ID** that uniquely identifies your app</span></span>
* <span data-ttu-id="46f36-113">응답을 다시 앱으로 보내는 데 사용할 수 있는 **리디렉션 URI**</span><span class="sxs-lookup"><span data-stu-id="46f36-113">A **Redirect URI** that you can use to direct responses back to your app</span></span>
* <span data-ttu-id="46f36-114">다른 몇 가지 시나리오 관련 값.</span><span class="sxs-lookup"><span data-stu-id="46f36-114">A few other scenario-specific values</span></span>

<span data-ttu-id="46f36-115">자세한 내용은 [앱 등록](active-directory-v2-app-registration.md)방법을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="46f36-115">For details, learn how to [register an app](active-directory-v2-app-registration.md).</span></span>

<span data-ttu-id="46f36-116">앱을 등록하면 앱에서 Azure AD v2.0 끝점으로 요청을 보내 Azure AD와 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="46f36-116">After the app is registered, the app communicates with Azure AD by sending requests to the Azure AD v2.0 endpoint.</span></span> <span data-ttu-id="46f36-117">Microsoft에서는 이러한 요청에 대한 세부 정보를 처리하는 오픈 소스 프레임워크 및 라이브러리를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="46f36-117">We provide open-source frameworks and libraries that handle the details of these requests.</span></span> <span data-ttu-id="46f36-118">또한 이러한 끝점에 대한 요청을 만들어 인증 논리를 직접 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46f36-118">You also have the option to implement the authentication logic yourself by creating requests to these endpoints:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
https://login.microsoftonline.com/common/oauth2/v2.0/token
```
<!-- TODO: Need a page for libraries to link to -->

## <a name="web-apps"></a><span data-ttu-id="46f36-119">웹 앱</span><span class="sxs-lookup"><span data-stu-id="46f36-119">Web apps</span></span>
<span data-ttu-id="46f36-120">사용자가 브라우저를 통해 액세스하는 웹앱(.NET, PHP, Java, Ruby, Python, Node)의 경우 사용자 로그인에 [OpenID Connect](active-directory-v2-protocols.md)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46f36-120">For web apps (.NET, PHP, Java, Ruby, Python, Node) that the user accesses through a browser, you can use [OpenID Connect](active-directory-v2-protocols.md) for user sign-in.</span></span> <span data-ttu-id="46f36-121">OpenID Connect에서는 웹앱이 ID 토큰을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="46f36-121">In OpenID Connect, the web app receives an ID token.</span></span> <span data-ttu-id="46f36-122">ID 토큰은 사용자 ID를 확인하고 클레임 형태로 사용자 정보를 제공하는 보안 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="46f36-122">An ID token is a security token that verifies the user's identity and provides information about the user in the form of claims:</span></span>

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

<span data-ttu-id="46f36-123">[v2.0 토큰 참조](active-directory-v2-tokens.md)에서 앱이 사용할 수 있는 모든 토큰 및 클레임 형식에 대해 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46f36-123">You can learn about all the types of tokens and claims that are available to an app in the [v2.0 tokens reference](active-directory-v2-tokens.md).</span></span>

<span data-ttu-id="46f36-124">웹 서버 앱에서 로그인 인증 흐름은 다음과 같은 높은 수준의 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="46f36-124">In web server apps, the sign-in authentication flow takes these high-level steps:</span></span>

![웹앱 인증 흐름](../../media/active-directory-v2-flows/convergence_scenarios_webapp.png)

<span data-ttu-id="46f36-126">v2.0 끝점에서 받은 공개 서명 키로 ID 토큰의 유효성을 검사하여 사용자 ID를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46f36-126">You can ensure the user's identity by validating the ID token with a public signing key that is received from the v2.0 endpoint.</span></span> <span data-ttu-id="46f36-127">후속 페이지 요청에서 사용자를 식별하는 데 사용할 수 있는 세션 쿠키가 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="46f36-127">A session cookie is set, which can be used to identify the user on subsequent page requests.</span></span>

<span data-ttu-id="46f36-128">이 시나리오의 작동 방식을 확인하려면 v2.0 [시작](active-directory-appmodel-v2-overview.md#getting-started) 섹션의 웹앱 로그인 코드 샘플 중 하나를 체험해 보세요.</span><span class="sxs-lookup"><span data-stu-id="46f36-128">To see this scenario in action, try one of the web app sign-in code samples in our v2.0 [Getting Started](active-directory-appmodel-v2-overview.md#getting-started) section.</span></span>

<span data-ttu-id="46f36-129">간단한 로그인뿐 아니라 웹 서버 앱은 REST API와 같은 다른 웹 서비스에 액세스해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46f36-129">In addition to simple sign-in, a web server app might need to access another web service, such as a REST API.</span></span> <span data-ttu-id="46f36-130">이 경우 웹 서버 앱은 [OAuth 2.0 권한 부여 코드 흐름](active-directory-v2-protocols.md)을 사용하여 결합된 OpenID Connect 및 OAuth 2.0 흐름에 참여합니다.</span><span class="sxs-lookup"><span data-stu-id="46f36-130">In this case, the web server app engages in a combined OpenID Connect and OAuth 2.0 flow, by using the [OAuth 2.0 authorization code flow](active-directory-v2-protocols.md).</span></span> <span data-ttu-id="46f36-131">이 시나리오에 대한 자세한 내용은 [웹앱 및 Web API 시작](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="46f36-131">For more information about this scenario, read about [getting started with web apps and Web APIs](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md).</span></span>

## <a name="web-apis"></a><span data-ttu-id="46f36-132">Web API</span><span class="sxs-lookup"><span data-stu-id="46f36-132">Web APIs</span></span>
<span data-ttu-id="46f36-133">v2.0 끝점을 사용하여 앱의 RESTful Web API와 같은 웹 서비스의 보안을 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46f36-133">You can use the v2.0 endpoint to secure web services, such as your app's RESTful Web API.</span></span> <span data-ttu-id="46f36-134">ID 토큰 및 세션 쿠키 대신 Web API는 OAuth 2.0 액세스 토큰을 사용하여 데이터 보안을 유지하고 들어오는 요청을 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="46f36-134">Instead of ID tokens and session cookies, a Web API uses an OAuth 2.0 access token to secure its data and to authenticate incoming requests.</span></span> <span data-ttu-id="46f36-135">Web API 호출자는 다음과 같이 HTTP 요청의 인증 헤더에 액세스 토큰을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="46f36-135">The caller of a Web API appends an access token in the authorization header of an HTTP request, like this:</span></span>

```
GET /api/items HTTP/1.1
Host: www.mywebapi.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6...
Accept: application/json
...
```

<span data-ttu-id="46f36-136">Web API는 액세스 토큰을 사용하여 API 호출자의 ID를 확인하고 액세스 토큰에 인코딩된 클레임에서 호출자에 대한 정보를 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="46f36-136">The Web API uses the access token to verify the API caller's identity and to extract information about the caller from claims that are encoded in the access token.</span></span> <span data-ttu-id="46f36-137">앱에 사용할 수 있는 모든 토큰 및 클레임 형식에 대한 자세한 내용은 [v2.0 토큰 참조](active-directory-v2-tokens.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="46f36-137">To learn about all the types of tokens and claims that are available to an app, see the [v2.0 tokens reference](active-directory-v2-tokens.md).</span></span>

<span data-ttu-id="46f36-138">Web API를 통해 사용자는 [범위](active-directory-v2-scopes.md)라고도 하는 사용 권한을 노출하여 특정 기능이나 데이터를 옵트인(opt-in)하거나 옵트아웃(opt-out)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46f36-138">A Web API can give users the power to opt in or opt out of specific functionality or data by exposing permissions, also known as [scopes](active-directory-v2-scopes.md).</span></span> <span data-ttu-id="46f36-139">호출 앱이 범위에 대한 사용 권한을 얻으려면 사용자가 흐름 중 범위에 동의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="46f36-139">For a calling app to acquire permission to a scope, the user must consent to the scope during a flow.</span></span> <span data-ttu-id="46f36-140">v2.0 끝점은 사용자에게 사용 권한을 요청한 다음 Web API가 받은 모든 액세스 토큰에 이러한 사용 권한을 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="46f36-140">The v2.0 endpoint asks the user for permission, and then records permissions in all access tokens that the Web API receives.</span></span> <span data-ttu-id="46f36-141">Web API는 각 호출에서 받은 액세스 토큰의 유효성을 검사하고 권한 부여 검사를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="46f36-141">The Web API validates the access tokens it receives on each call and performs authorization checks.</span></span>

<span data-ttu-id="46f36-142">Web API는 웹 서버 앱, 데스크톱 및 모바일 앱, 단일 페이지 앱, 서버 쪽 데몬 및 다른 Web API까지 포함하여 모든 유형의 앱에서 액세스 토큰을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46f36-142">A Web API can receive access tokens from all types of apps, including web server apps, desktop and mobile apps, single-page apps, server-side daemons, and even other Web APIs.</span></span> <span data-ttu-id="46f36-143">Web API에 대한 개략적인 흐름은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="46f36-143">The high-level flow for a Web API looks like this:</span></span>

![Web API 인증 흐름](../../media/active-directory-v2-flows/convergence_scenarios_webapi.png)

<span data-ttu-id="46f36-145">OAuth 2.0 액세스 토큰을 사용하여 Web API 보안을 유지하는 방법을 알아보려면 [시작 섹션](active-directory-appmodel-v2-overview.md#getting-started)에서 Web API 코드 샘플을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="46f36-145">To learn how to secure a Web API by using OAuth2 access tokens, check out the Web API code samples in our [Getting Started](active-directory-appmodel-v2-overview.md#getting-started) section.</span></span>

<span data-ttu-id="46f36-146">대부분의 경우 웹 API는 Azure Active Directory로 보호되는 다른 다운스트림 API에 대해 아웃바운드 요청도 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="46f36-146">In many cases, web APIs also need to make outbound requests to other downstream web APIs secured by Azure Active Directory.</span></span>  <span data-ttu-id="46f36-147">이렇게 하기 위해 웹 API는 Azure AD의 **On Behalf Of** 흐름을 활용하여 웹 API가 아웃바운드 요청에서 사용할 다른 액세스 토큰에 대해 들어오는 액세스 토큰을 교환하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46f36-147">To do so, web APIs can take advantage of Azure AD's **On Behalf Of** flow, which allows the web API to exchange an incoming access token for another access token to be used in outbound requests.</span></span>  <span data-ttu-id="46f36-148">v2.0 끝점의 On Behalf Of 흐름은 [여기서 자세히 설명](active-directory-v2-protocols-oauth-on-behalf-of.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="46f36-148">The v2.0 endpoint's On Behalf Of flow is described in [detail here](active-directory-v2-protocols-oauth-on-behalf-of.md).</span></span>

## <a name="mobile-and-native-apps"></a><span data-ttu-id="46f36-149">모바일 및 네이티브 앱</span><span class="sxs-lookup"><span data-stu-id="46f36-149">Mobile and native apps</span></span>
<span data-ttu-id="46f36-150">모바일 및 데스크톱 앱과 같은 장치 설치 앱은 데이터를 저장하고 사용자 대신 기능을 수행하는 백 엔드 서비스 또는 Web API에 액세스해야 하는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="46f36-150">Device-installed apps, such as mobile and desktop apps, often need to access back-end services or Web APIs that store data and perform functions on behalf of a user.</span></span> <span data-ttu-id="46f36-151">이러한 앱은 [OAuth 2.0 권한 부여 코드 흐름](active-directory-v2-protocols-oauth-code.md)을 사용하여 백 엔드 서비스에 로그인 및 권한 부여를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46f36-151">These apps can add sign-in and authorization to back-end services by using the [OAuth 2.0 authorization code flow](active-directory-v2-protocols-oauth-code.md).</span></span>

<span data-ttu-id="46f36-152">이 흐름에서 앱은 사용자 로그인 시 v2.0 끝점에서 권한 부여 코드를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="46f36-152">In this flow, the app receives an authorization code from the v2.0 endpoint when the user signs in.</span></span> <span data-ttu-id="46f36-153">권한 부여 코드는 현재 로그인한 사용자를 대신해 백 엔드 서비스를 호출할 앱의 사용 권한을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="46f36-153">The authorization code represents the app's permission to call back-end services on behalf of the user who is signed in.</span></span> <span data-ttu-id="46f36-154">앱은 백그라운드에서 권한 부여 코드를 OAuth 2.0 액세스 토큰 및 새로 고침 토큰으로 교환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46f36-154">The app can exchange the authorization code in the background for an OAuth 2.0 access token and a refresh token.</span></span> <span data-ttu-id="46f36-155">앱은 액세스 토큰을 사용하여 HTTP 요청 시 Web API에 인증할 수 있고 새로 고침 토큰을 사용하여 이전 액세스 토큰 만료 시 새 액세스 토큰을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46f36-155">The app can use the access token to authenticate to Web APIs in HTTP requests, and use the refresh token to get new access tokens when older access tokens expire.</span></span>

![네이티브 앱 인증 흐름](../../media/active-directory-v2-flows/convergence_scenarios_native.png)

## <a name="single-page-apps-javascript"></a><span data-ttu-id="46f36-157">단일 페이지 앱(JavaScript)</span><span class="sxs-lookup"><span data-stu-id="46f36-157">Single-page apps (JavaScript)</span></span>
<span data-ttu-id="46f36-158">대부분의 최신 앱에는 주로 Javascript로 작성되고 AngularJS, Ember.js, Durandal 등과 같은 프레임워크로도 작성되는</span><span class="sxs-lookup"><span data-stu-id="46f36-158">Many modern apps have a single-page app front end that primarily is written in JavaScript.</span></span> <span data-ttu-id="46f36-159">단일 페이지 앱 프런트 엔드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46f36-159">Often, it's written by using a framework like AngularJS, Ember.js, or Durandal.js.</span></span> <span data-ttu-id="46f36-160">Azure AD v2.0 끝점은 [OAuth 2.0 암시적 흐름](active-directory-v2-protocols-implicit.md)을 사용하여 이러한 앱을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="46f36-160">The Azure AD v2.0 endpoint supports these apps by using the [OAuth 2.0 implicit flow](active-directory-v2-protocols-implicit.md).</span></span>

<span data-ttu-id="46f36-161">이 흐름에서 앱은 서버 간 교환 없이 v 2.0 인증 끝점에서 직접 토큰을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="46f36-161">In this flow, the app receives tokens directly from the v2.0 authorize endpoint, without any server-to-server exchanges.</span></span> <span data-ttu-id="46f36-162">모든 인증 논리 및 세션 처리가 추가 페이지 리디렉션 없이 전적으로 JavaScript 클라이언트에서 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="46f36-162">All authentication logic and session handling takes place entirely in the JavaScript client, without extra page redirects.</span></span>

![암시적 인증 흐름](../../media/active-directory-v2-flows/convergence_scenarios_implicit.png)

<span data-ttu-id="46f36-164">이 시나리오의 작동 방식을 확인하려면 [시작](active-directory-appmodel-v2-overview.md#getting-started) 섹션의 단일 페이지 앱 코드 샘플 중 하나를 시도해 보세요.</span><span class="sxs-lookup"><span data-stu-id="46f36-164">To see this scenario in action, try one of the single-page app code samples in our [Getting Started](active-directory-appmodel-v2-overview.md#getting-started) section.</span></span>

## <a name="daemons-and-server-side-apps"></a><span data-ttu-id="46f36-165">디먼 및 서버 쪽 앱</span><span class="sxs-lookup"><span data-stu-id="46f36-165">Daemons and server-side apps</span></span>
<span data-ttu-id="46f36-166">장기 실행 프로세스가 있거나 사용자와의 상호 작용 없이 작동하는 앱은 Web API와 같은 보안 리소스에 액세스하는 방법도 필요로 합니다.</span><span class="sxs-lookup"><span data-stu-id="46f36-166">Apps that have long-running processes or that operate without interaction with a user also need a way to access secured resources, such as Web APIs.</span></span> <span data-ttu-id="46f36-167">이러한 앱은 OAuth 2.0 클라이언트 자격 증명 흐름을 사용하여 사용자의 위임된 ID 대신 앱 ID로 인증하고 토큰을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46f36-167">These apps can authenticate and get tokens by using the app's identity, rather than a user's delegated identity, with the OAuth 2.0 client credentials flow.</span></span>

<span data-ttu-id="46f36-168">이 흐름에서 앱은 `/token` 끝점과 직접 상호 작용하여 끝점을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="46f36-168">In this flow, the app interacts directly with the `/token` endpoint to obtain endpoints:</span></span>

![디먼 앱 인증 흐름](../../media/active-directory-v2-flows/convergence_scenarios_daemon.png)

<span data-ttu-id="46f36-170">디먼 앱을 작성하려면 [시작](active-directory-appmodel-v2-overview.md#getting-started) 섹션에서 클라이언트 자격 증명 설명서를 참조하거나 [.NET 샘플 앱](https://github.com/Azure-Samples/active-directory-dotnet-daemon-v2)을 사용해 보세요.</span><span class="sxs-lookup"><span data-stu-id="46f36-170">To build a daemon app, see the client credentials documentation in our [Getting Started](active-directory-appmodel-v2-overview.md#getting-started) section, or try a [.NET sample app](https://github.com/Azure-Samples/active-directory-dotnet-daemon-v2).</span></span>

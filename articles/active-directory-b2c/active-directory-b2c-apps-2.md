---
title: "응용 프로그램의 형식 - Azure AD B2C | Microsoft Docs"
description: "Azure Active Directory B2C에서 빌드할 수 있는 응용 프로그램의 유형입니다."
services: active-directory-b2c
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: bb9d4abe-0db7-4bd9-b0c4-2f43b2c9cf33
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 12/06/2016
ms.author: dastrock
ms.openlocfilehash: 6dd3864fb8f08e92231e04c5b1ed546760ec3526
ms.sourcegitcommit: 70b1af4ad0b53009cb30aadc54e9609134aa0d72
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/11/2017
---
# <a name="azure-active-directory-b2c-types-of-applications"></a><span data-ttu-id="f7259-103">Azure Active Directory B2C: 응용 프로그램 유형</span><span class="sxs-lookup"><span data-stu-id="f7259-103">Azure Active Directory B2C: Types of applications</span></span>
<span data-ttu-id="f7259-104">회선 prehandoff에서 파일을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-104">Changing line to make file in prehandoff.</span></span>
<span data-ttu-id="f7259-105">Azure AD(Azure Active Directory) B2C는 다양한 최신 앱 아키텍처의 인증을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-105">Azure Active Directory (Azure AD) B2C supports authentication for a variety of modern app architectures.</span></span> <span data-ttu-id="f7259-106">모두 업계 표준 프로토콜인 [OAuth 2.0](active-directory-b2c-reference-protocols.md) 또는 [OpenID Connect](active-directory-b2c-reference-protocols.md)를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-106">All of them are based on the industry standard protocols [OAuth 2.0](active-directory-b2c-reference-protocols.md) or [OpenID Connect](active-directory-b2c-reference-protocols.md).</span></span> <span data-ttu-id="f7259-107">이 문서에서는 선호하는 언어 또는 플랫폼에 독립적으로 빌드할 수 있는 앱 유형에 대해 간략하게 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-107">This document briefly describes the types of apps that you can build, independent of the language or platform you prefer.</span></span> <span data-ttu-id="f7259-108">또한 [응용 프로그램 빌드를 시작](active-directory-b2c-overview.md#get-started)하기 전에 대략적인 시나리오에 대한 이해를 돕습니다</span><span class="sxs-lookup"><span data-stu-id="f7259-108">It also helps you understand the high-level scenarios before you [start building applications](active-directory-b2c-overview.md#get-started).</span></span>

## <a name="the-basics"></a><span data-ttu-id="f7259-109">기본 사항</span><span class="sxs-lookup"><span data-stu-id="f7259-109">The basics</span></span>
<span data-ttu-id="f7259-110">Azure AD B2C를 사용하는 모든 앱은 [Azure Portal](https://portal.azure.com/)을 통해 [B2C 디렉터리](active-directory-b2c-get-started.md)에 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-110">Every app that uses Azure AD B2C must be registered in your [B2C directory](active-directory-b2c-get-started.md) via the [Azure Portal](https://portal.azure.com/).</span></span> <span data-ttu-id="f7259-111">앱 등록 프로세스는 몇 개의 값을 수집하고 앱에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-111">The app registration process collects and assigns a few values to your app:</span></span>

* <span data-ttu-id="f7259-112">앱을 고유하게 식별하는 **응용 프로그램 ID**</span><span class="sxs-lookup"><span data-stu-id="f7259-112">An **Application ID** that uniquely identifies your app.</span></span>
* <span data-ttu-id="f7259-113">응답을 다시 앱으로 보내는 데 사용할 수 있는 **리디렉션 URI**</span><span class="sxs-lookup"><span data-stu-id="f7259-113">A **Redirect URI** that can be used to direct responses back to your app.</span></span>
* <span data-ttu-id="f7259-114">다른 모든 시나리오 관련 값.</span><span class="sxs-lookup"><span data-stu-id="f7259-114">Any other scenario-specific values.</span></span> <span data-ttu-id="f7259-115">자세한 내용은 [앱 등록](active-directory-b2c-app-registration.md)방법을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f7259-115">For more details, learn how to [register an app](active-directory-b2c-app-registration.md).</span></span>

<span data-ttu-id="f7259-116">앱이 등록되면 Azure AD v2.0 끝점에 요청을 보내 Azure AD와 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-116">After the app is registered, it communicates with Azure AD by sending requests to the Azure AD v2.0 endpoint:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
https://login.microsoftonline.com/common/oauth2/v2.0/token
```

<span data-ttu-id="f7259-117">Azure AD B2C에 전송되는 각 요청은 **정책**을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-117">Each request that is sent to Azure AD B2C specifies a **policy**.</span></span> <span data-ttu-id="f7259-118">정책은 Azure AD의 동작을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-118">A policy controls the behavior of Azure AD.</span></span> <span data-ttu-id="f7259-119">또한 이러한 끝점을 사용하여 사용자 환경에 대해 고도로 사용자 지정 가능한 집합을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-119">You can also use these endpoints to create a highly customizable set of user experiences.</span></span> <span data-ttu-id="f7259-120">공통 정책에는 등록 정책, 로그인 정책 및 프로필 편집 정책이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-120">Common policies include sign-up, sign-in, and profile-edit policies.</span></span> <span data-ttu-id="f7259-121">정책에 익숙하지 않은 경우 계속 읽기 전에 Azure AD B2C의 [확장할 수 있는 정책 프레임워크](active-directory-b2c-reference-policies.md) 에 대해 읽어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-121">If you are not familiar with policies, you should read about the Azure AD B2C [extensible policy framework](active-directory-b2c-reference-policies.md) before you continue.</span></span>

<span data-ttu-id="f7259-122">v2.0 끝점과 각 앱의 상호 작용은 높은 수준에서 비슷한 패턴을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-122">The interaction of every app with a v2.0 endpoint follows a similar high-level pattern:</span></span>

1. <span data-ttu-id="f7259-123">앱이 사용자를 v2.0 끝점으로 보내어 [정책](active-directory-b2c-reference-policies.md)을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-123">The app directs the user to the v2.0 endpoint to execute a [policy](active-directory-b2c-reference-policies.md).</span></span>
2. <span data-ttu-id="f7259-124">사용자는 정책 정의에 따라 정책을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-124">The user completes the policy according to the policy definition.</span></span>
3. <span data-ttu-id="f7259-125">앱이 v2.0 끝점에서 일종의 보안 토큰을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-125">The app receives some kind of security token from the v2.0 endpoint.</span></span>
4. <span data-ttu-id="f7259-126">앱이 보안 토큰을 사용하여 보호된 정보 또는 보호된 리소스에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-126">The app uses the security token to access protected information or a protected resource.</span></span>
5. <span data-ttu-id="f7259-127">리소스 서버가 보안 토큰의 유효성을 검사하여 액세스 권한을 부여할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-127">The resource server validates the security token to verify that access can be granted.</span></span>
6. <span data-ttu-id="f7259-128">앱이 주기적으로 보안 토큰을 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-128">The app periodically refreshes the security token.</span></span>

<!-- TODO: Need a page for libraries to link to -->
<span data-ttu-id="f7259-129">이러한 단계는 빌드 중인 앱의 유형에 따라 약간씩 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-129">These steps can differ slightly based on the type of app you're building.</span></span> <span data-ttu-id="f7259-130">오픈 소스 라이브러리로 사용자에 대한 세부 정보를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-130">Open source libraries can address the details for you.</span></span>

## <a name="web-apps"></a><span data-ttu-id="f7259-131">웹 앱</span><span class="sxs-lookup"><span data-stu-id="f7259-131">Web apps</span></span>
<span data-ttu-id="f7259-132">서버에서 호스팅되며 브라우저를 통해 액세스하는 웹앱(.NET, PHP, Java, Ruby, Python, Node.js 등)의 경우 Azure AD B2C는 모든 사용자 환경에 [OpenID Connect](active-directory-b2c-reference-protocols.md) 를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-132">For web apps (including .NET, PHP, Java, Ruby, Python, and Node.js) that are hosted on a server and accessed through a browser, Azure AD B2C supports [OpenID Connect](active-directory-b2c-reference-protocols.md) for all user experiences.</span></span> <span data-ttu-id="f7259-133">여기에는 로그인, 등록 및 프로필 관리가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-133">This includes sign-in, sign-up, and profile management.</span></span> <span data-ttu-id="f7259-134">OpenID Connect의 Azure AD B2C 구현에서 웹앱은 Azure AD로 인증 요청을 발급하여 이러한 사용자 환경을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-134">In the Azure AD B2C implementation of OpenID Connect, your web app initiates these user experiences by issuing authentication requests to Azure AD.</span></span> <span data-ttu-id="f7259-135">요청의 결과는 `id_token`입니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-135">The result of the request is an `id_token`.</span></span> <span data-ttu-id="f7259-136">이 보안 토큰은 사용자의 ID를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-136">This security token represents the user's identity.</span></span> <span data-ttu-id="f7259-137">또한 클레임 형태로 사용자에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-137">It also provides information about the user in the form of claims:</span></span>

```
// Partial raw id_token
eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6ImtyaU1QZG1Cd...

// Partial content of a decoded id_token
{
    "name": "John Smith",
    "email": "john.smith@gmail.com",
    "oid": "d9674823-dffc-4e3f-a6eb-62fe4bd48a58"
    ...
}
```

<span data-ttu-id="f7259-138">[B2C 토큰 참조](active-directory-b2c-reference-tokens.md)에서 앱이 사용할 수 있는 토큰 및 클레임 유형에 대해 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-138">Learn more about the types of tokens and claims available to an app in the [B2C token reference](active-directory-b2c-reference-tokens.md).</span></span>

<span data-ttu-id="f7259-139">웹앱에서 [정책](active-directory-b2c-reference-policies.md) 의 각 실행에서는 이러한 수준 높은 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-139">In a web app, each execution of a [policy](active-directory-b2c-reference-policies.md) takes these high-level steps:</span></span>

![웹앱 스윔 레인 이미지](./media/active-directory-b2c-apps/webapp.png)

<span data-ttu-id="f7259-141">Azure AD에서 수신한 공개 서명 키를 사용하여 `id_token` 의 유효성을 확인하는 것으로 사용자의 ID를 충분히 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-141">Validation of the `id_token` by using a public signing key that is received from Azure AD is sufficient to verify the identity of the user.</span></span> <span data-ttu-id="f7259-142">또한 후속 페이지 요청에서 사용자를 식별하는 데 사용할 수 있는 세션 쿠키도 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-142">This also sets a session cookie that can be used to identify the user on subsequent page requests.</span></span>

<span data-ttu-id="f7259-143">이 시나리오의 작동 방식을 확인하려면 [시작 섹션](active-directory-b2c-overview.md#get-started)의 웹앱 로그인 코드 샘플 중 하나를 체험해 보세요.</span><span class="sxs-lookup"><span data-stu-id="f7259-143">To see this scenario in action, try one of the web app sign-in code samples in our [Getting started section](active-directory-b2c-overview.md#get-started).</span></span>

<span data-ttu-id="f7259-144">간단한 로그인뿐 아니라 웹 서버 앱은 백 엔드 웹 서비스에 액세스해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-144">In addition to facilitating simple sign-in, a web server app might also need to access a back-end web service.</span></span> <span data-ttu-id="f7259-145">이 경우 웹앱은 약간 다른 [OpenID Connect 흐름](active-directory-b2c-reference-oidc.md) 을 수행하고 권한 부여 코드를 사용하여 토큰을 획득하며 토큰을 새로 고칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-145">In this case, the web app can perform a slightly different [OpenID Connect flow](active-directory-b2c-reference-oidc.md) and acquire tokens by using authorization codes and refresh tokens.</span></span> <span data-ttu-id="f7259-146">이 시나리오는 다음 [Web API 섹션](#web-apis)에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-146">This scenario is depicted in the following [Web APIs section](#web-apis).</span></span>

<!--, and in our [WebApp-WebAPI Getting started topic](active-directory-b2c-devquickstarts-web-api-dotnet.md).-->

## <a name="web-apis"></a><span data-ttu-id="f7259-147">Web API</span><span class="sxs-lookup"><span data-stu-id="f7259-147">Web APIs</span></span>
<span data-ttu-id="f7259-148">Azure AD B2C을 사용하여 앱의 RESTful Web API와 같은 웹 서비스의 보안을 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-148">You can use Azure AD B2C to secure web services such as your app's RESTful web API.</span></span> <span data-ttu-id="f7259-149">Web API는 토큰을 사용하는 들어오는 HTTP 요청을 인증하여 해당 데이터를 보호하는 데 OAuth 2.0을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-149">Web APIs can use OAuth 2.0 to secure their data, by authenticating incoming HTTP requests using tokens.</span></span> <span data-ttu-id="f7259-150">Web API 호출자는 HTTP 요청의 권한 부여 헤더에 토큰을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-150">The caller of a web API appends a token in the authorization header of an HTTP request:</span></span>

```
GET /api/items HTTP/1.1
Host: www.mywebapi.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6...
Accept: application/json
...
```

<span data-ttu-id="f7259-151">그러면 Web API는 토큰을 사용하여 API 호출자의 ID를 확인하고 토큰에 인코드된 클레임에서 호출자에 대한 정보를 추출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-151">The web API can then use the token to verify the API caller's identity and to extract information about the caller from claims that are encoded in the token.</span></span> <span data-ttu-id="f7259-152">[Azure AD B2C 토큰 참조](active-directory-b2c-reference-tokens.md)에서 앱이 사용할 수 있는 토큰 및 클레임 유형에 대해 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-152">Learn more about the types of tokens and claims available to an app in the [Azure AD B2C token reference](active-directory-b2c-reference-tokens.md).</span></span>

> [!NOTE]
> <span data-ttu-id="f7259-153">Azure AD B2C는 현재 고유한 잘 알려진 클라이언트에서 액세스하는 Web API만을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-153">Azure AD B2C currently supports only web APIs that are accessed by their own well-known clients.</span></span> <span data-ttu-id="f7259-154">예를 들어 전체 앱이 iOS 앱, Android 앱 및 백 엔드 Web API를 포함할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-154">For instance, your complete app may include an iOS app, an Android app, and a back-end web API.</span></span> <span data-ttu-id="f7259-155">이 아키텍처를 완전히 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-155">This architecture is fully supported.</span></span> <span data-ttu-id="f7259-156">다른 iOS 앱과 같은 파트너 클라이언트에서 동일한 Web API에 액세스하는 것은 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-156">Allowing a partner client, such as another iOS app, to access the same web API is not currently supported.</span></span> <span data-ttu-id="f7259-157">전체 앱의 모든 구성 요소는 단일 응용 프로그램 ID를 공유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-157">All of the components of your complete app must share a single application ID.</span></span>
>
>

<span data-ttu-id="f7259-158">Web API는 웹앱, 데스크톱 및 모바일 앱, 단일 페이지 앱, 서버 쪽 데몬 및 다른 Web API까지 포함하여 많은 유형의 클라이언트에서 토큰을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-158">A web API can receive tokens from many types of clients, including web apps, desktop and mobile apps, single page apps, server-side daemons, and other web APIs.</span></span> <span data-ttu-id="f7259-159">다음은 Web API를 호출하는 웹앱에 대한 전체 흐름을 보여주는 예입니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-159">Here's an example of the complete flow for a web app that calls a web API:</span></span>

![웹앱 Web API 스윔 레인 이미지](./media/active-directory-b2c-apps/webapi.png)

<span data-ttu-id="f7259-161">권한 부여 코드, 새로 고침 토큰 및 토큰을 가져오는 단계에 대한 자세한 내용은 [OAuth 2.0 프로토콜](active-directory-b2c-reference-oauth-code.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f7259-161">To learn more about authorization codes, refresh tokens, and the steps for getting tokens, read about the [OAuth 2.0 protocol](active-directory-b2c-reference-oauth-code.md).</span></span>

<span data-ttu-id="f7259-162">Azure AD B2C를 사용하여 Web API를 보호하는 방법을 알아보려면 [시작 섹션](active-directory-b2c-overview.md#get-started)에서 Web API 자습서를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="f7259-162">To learn how to secure a web API by using Azure AD B2C, check out the web API tutorials in our [Getting started section](active-directory-b2c-overview.md#get-started).</span></span>

## <a name="mobile-and-native-apps"></a><span data-ttu-id="f7259-163">모바일 및 네이티브 앱</span><span class="sxs-lookup"><span data-stu-id="f7259-163">Mobile and native apps</span></span>
<span data-ttu-id="f7259-164">모바일 및 데스크톱 앱과 같은 장치에 설치된 앱은 사용자 대신 백 엔드 서비스 또는 Web API에 액세스해야 하는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-164">Apps that are installed on devices, such as mobile and desktop apps, often need to access back-end services or web APIs on behalf of users.</span></span> <span data-ttu-id="f7259-165">네이티브 앱에 사용자 지정된 ID 관리 환경을 추가하고 Azure AD B2C 및 [OAuth 2.0 권한 부여 코드 흐름](active-directory-b2c-reference-oauth-code.md)을 사용하여 안전하게 백 엔드 서비스를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-165">You can add customized identity management experiences to your native apps and securely call back-end services by using Azure AD B2C and the [OAuth 2.0 authorization code flow](active-directory-b2c-reference-oauth-code.md).</span></span>  

<span data-ttu-id="f7259-166">이 흐름에서 앱은 [정책](active-directory-b2c-reference-policies.md)을 실행하고 사용자가 정책을 완료하면 Azure AD에서 `authorization_code`을(를) 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-166">In this flow, the app executes [policies](active-directory-b2c-reference-policies.md) and receives an `authorization_code` from Azure AD after the user completes the policy.</span></span> <span data-ttu-id="f7259-167">`authorization_code` 는 현재 로그인한 사용자를 대신하여 백 엔드 서비스를 호출할 앱의 사용 권한을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-167">The `authorization_code` represents the app's permission to call back-end services on behalf of the user who is currently signed in.</span></span> <span data-ttu-id="f7259-168">그러면 앱은 백그라운드에서 `id_token` 및 `refresh_token`에 대한 `authorization_code`을(를) 교환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-168">The app can then exchange the `authorization_code` in the background for an `id_token` and a `refresh_token`.</span></span>  <span data-ttu-id="f7259-169">앱은 HTTP 요청에서 백 엔드 Web API를 인증하는 데 `id_token` 을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-169">The app can use the `id_token` to authenticate to a back-end web API in HTTP requests.</span></span> <span data-ttu-id="f7259-170">또한 이전 항목이 만료된 경우 `refresh_token`을 사용하여 새 `id_token`을 가져올 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-170">It can also use the `refresh_token` to get a new `id_token` when an older one expires.</span></span>

> [!NOTE]
> <span data-ttu-id="f7259-171">Azure AD B2C는 현재 앱 자체의 백 엔드 웹 서비스에 액세스하는 데 사용되는 토큰만을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-171">Azure AD B2C currently supports only tokens that are used to access an app's own back-end web service.</span></span> <span data-ttu-id="f7259-172">예를 들어 전체 앱이 iOS 앱, Android 앱 및 백 엔드 Web API를 포함할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-172">For instance, your complete app may include an iOS app, an Android app, and a back-end web API.</span></span> <span data-ttu-id="f7259-173">이 아키텍처를 완전히 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-173">This architecture is fully supported.</span></span> <span data-ttu-id="f7259-174">iOS 앱이 OAuth 2.0 액세스 토큰을 사용하여 파트너 Web API에 액세스하는 작업은 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-174">Allowing your iOS app to access a partner web API by using OAuth 2.0 access tokens is not currently supported.</span></span> <span data-ttu-id="f7259-175">전체 앱의 모든 구성 요소는 단일 응용 프로그램 ID를 공유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-175">All of the components of your complete app must share a single application ID.</span></span>
>
>

![네이티브 앱 스윔 레인 이미지](./media/active-directory-b2c-apps/native.png)

## <a name="current-limitations"></a><span data-ttu-id="f7259-177">현재 제한 사항</span><span class="sxs-lookup"><span data-stu-id="f7259-177">Current limitations</span></span>
<span data-ttu-id="f7259-178">Azure AD B2C는 다음과 같은 유형의 앱을 현재 지원하지 않지만 로드맵에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-178">Azure AD B2C does not currently support the following types of apps, but they are on the roadmap.</span></span> 

### <a name="daemonsserver-side-apps"></a><span data-ttu-id="f7259-179">디먼/서버 쪽 앱</span><span class="sxs-lookup"><span data-stu-id="f7259-179">Daemons/server-side apps</span></span>
<span data-ttu-id="f7259-180">장기 실행 프로세스를 포함하거나 사용자 없이 작동하는 앱은 Web API와 같은 보안 리소스에 액세스하는 방법도 필요로 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-180">Apps that contain long-running processes or that operate without the presence of a user also need a way to access secured resources such as web APIs.</span></span> <span data-ttu-id="f7259-181">이러한 앱은 OAuth 2.0 클라이언트 자격 증명 흐름을 사용하여 사용자의 위임된 ID 대신 앱 ID를 사용하여 인증하고 토큰을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-181">These apps can authenticate and get tokens by using the app's identity (rather than a user's delegated identity) and by using the OAuth 2.0 client credentials flow.</span></span>

<span data-ttu-id="f7259-182">이 흐름은 Azure AD B2C에서 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-182">This flow is not currently supported by Azure AD B2C.</span></span> <span data-ttu-id="f7259-183">이러한 앱은 대화형 사용자 흐름이 발생한 후에만 토큰을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-183">These apps can get tokens only after an interactive user flow has occurred.</span></span>

### <a name="web-api-chains-on-behalf-of-flow"></a><span data-ttu-id="f7259-184">Web API 체인(On-Behalf-Of 흐름)</span><span class="sxs-lookup"><span data-stu-id="f7259-184">Web API chains (on-behalf-of flow)</span></span>
<span data-ttu-id="f7259-185">많은 아키텍처에는 다른 다운스트림 Web API를 호출해야 하는 Web API가 포함되어 있으며 둘 다 Azure AD B2C로 보안됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-185">Many architectures include a web API that needs to call another downstream web API, where both are secured by Azure AD B2C.</span></span> <span data-ttu-id="f7259-186">이 시나리오는 Web API 백 엔드를 가지고 있는 네이티브 클라이언트에서 일반적입니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-186">This scenario is common in native clients that have a Web API back-end.</span></span> <span data-ttu-id="f7259-187">그런 다음 Azure AD Graph API와 같은 Microsoft 온라인 서비스를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-187">This then calls a Microsoft online service such as the Azure AD Graph API.</span></span>

<span data-ttu-id="f7259-188">On-Behalf-Of 흐름이라고도 하는 OAuth 2.0 JWT 전달자 자격 증명 권한 부여를 사용하여 이 연결된 Web API 시나리오를 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-188">This chained web API scenario can be supported by using the OAuth 2.0 JWT bearer credential grant, also known as the on-behalf-of flow.</span></span>  <span data-ttu-id="f7259-189">그러나 On-Behalf-Of 흐름은 현재 Azure AD B2C에 구현되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f7259-189">However, the on-behalf-of flow is not currently implemented in the Azure AD B2C.</span></span>

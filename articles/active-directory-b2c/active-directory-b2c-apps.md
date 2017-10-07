---
title: AD B2C aaaAzure | Microsoft Docs
description: "hello 유형의 응용 프로그램 hello Azure Active Directory B2C에에서 빌드할 수 있습니다."
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
ms.openlocfilehash: 7dd3dac781fb7e1553dd0f2d112b1956489a7dfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-types-of-applications"></a><span data-ttu-id="3684d-103">Azure Active Directory B2C: 응용 프로그램 유형</span><span class="sxs-lookup"><span data-stu-id="3684d-103">Azure Active Directory B2C: Types of applications</span></span>
<span data-ttu-id="3684d-104">Azure AD(Azure Active Directory) B2C는 다양한 최신 앱 아키텍처의 인증을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-104">Azure Active Directory (Azure AD) B2C supports authentication for a variety of modern app architectures.</span></span> <span data-ttu-id="3684d-105">Hello 업계 표준 프로토콜을 기반 모두 [OAuth 2.0](active-directory-b2c-reference-protocols.md) 또는 [OpenID Connect](active-directory-b2c-reference-protocols.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-105">All of them are based on hello industry standard protocols [OAuth 2.0](active-directory-b2c-reference-protocols.md) or [OpenID Connect](active-directory-b2c-reference-protocols.md).</span></span> <span data-ttu-id="3684d-106">이 문서에는 간단 하 게 빌드할 수 있는 앱의 hello 유형에 대해 설명, hello 언어 및 플랫폼에 관계 없이 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-106">This document briefly describes hello types of apps that you can build, independent of hello language or platform you prefer.</span></span> <span data-ttu-id="3684d-107">또한 이해 하도록 하기 전에 hello 높은 수준의 시나리오 [응용 프로그램을 빌드](active-directory-b2c-overview.md#get-started)합니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-107">It also helps you understand hello high-level scenarios before you [start building applications](active-directory-b2c-overview.md#get-started).</span></span>

## <a name="hello-basics"></a><span data-ttu-id="3684d-108">hello 기본 사항</span><span class="sxs-lookup"><span data-stu-id="3684d-108">hello basics</span></span>
<span data-ttu-id="3684d-109">Azure AD B2C를 사용 하는 모든 응용 프로그램에 등록 해야 프로그램 [B2C 디렉터리](active-directory-b2c-get-started.md) hello를 통해 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-109">Every app that uses Azure AD B2C must be registered in your [B2C directory](active-directory-b2c-get-started.md) via hello [Azure Portal](https://portal.azure.com/).</span></span> <span data-ttu-id="3684d-110">수집 하 고 몇 가지 값 tooyour 응용 프로그램을 할당 하는 hello 응용 프로그램 등록 프로세스:</span><span class="sxs-lookup"><span data-stu-id="3684d-110">hello app registration process collects and assigns a few values tooyour app:</span></span>

* <span data-ttu-id="3684d-111">앱을 고유하게 식별하는 **응용 프로그램 ID**</span><span class="sxs-lookup"><span data-stu-id="3684d-111">An **Application ID** that uniquely identifies your app.</span></span>
* <span data-ttu-id="3684d-112">A **리디렉션 URI** 사용된 toodirect 응답 백 tooyour 앱 일 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-112">A **Redirect URI** that can be used toodirect responses back tooyour app.</span></span>
* <span data-ttu-id="3684d-113">다른 모든 시나리오 관련 값.</span><span class="sxs-lookup"><span data-stu-id="3684d-113">Any other scenario-specific values.</span></span> <span data-ttu-id="3684d-114">자세한 내용은 자세한 방법을 너무[앱을 등록](active-directory-b2c-app-registration.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-114">For more details, learn how too[register an app](active-directory-b2c-app-registration.md).</span></span>

<span data-ttu-id="3684d-115">Hello 앱을 등록 한 후 통신 Azure AD와 Azure AD toohello v2.0 끝점 요청을 전송 하 여:</span><span class="sxs-lookup"><span data-stu-id="3684d-115">After hello app is registered, it communicates with Azure AD by sending requests toohello Azure AD v2.0 endpoint:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
https://login.microsoftonline.com/common/oauth2/v2.0/token
```

<span data-ttu-id="3684d-116">각 전송 된 요청은 AD B2C tooAzure 지정는 **정책**합니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-116">Each request that is sent tooAzure AD B2C specifies a **policy**.</span></span> <span data-ttu-id="3684d-117">Azure AD의 hello 동작을 제어 하는 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-117">A policy controls hello behavior of Azure AD.</span></span> <span data-ttu-id="3684d-118">또한 이러한 끝점 toocreate 고도로 사용자 지정 가능한 집합이 사용자 환경 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-118">You can also use these endpoints toocreate a highly customizable set of user experiences.</span></span> <span data-ttu-id="3684d-119">공통 정책에는 등록 정책, 로그인 정책 및 프로필 편집 정책이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-119">Common policies include sign-up, sign-in, and profile-edit policies.</span></span> <span data-ttu-id="3684d-120">정책을 사용 하 여 잘 모르는 경우 읽어야 할 Azure AD B2C hello [확장 가능한 정책 프레임 워크](active-directory-b2c-reference-policies.md) 계속 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="3684d-120">If you are not familiar with policies, you should read about hello Azure AD B2C [extensible policy framework](active-directory-b2c-reference-policies.md) before you continue.</span></span>

<span data-ttu-id="3684d-121">v2.0 끝점이 있는 모든 응용 프로그램의 hello 상호 작용 비슷한 높은 수준의 패턴을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-121">hello interaction of every app with a v2.0 endpoint follows a similar high-level pattern:</span></span>

1. <span data-ttu-id="3684d-122">hello 앱 hello 사용자 toohello v2.0 끝점 tooexecute 보냅니다는 [정책](active-directory-b2c-reference-policies.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-122">hello app directs hello user toohello v2.0 endpoint tooexecute a [policy](active-directory-b2c-reference-policies.md).</span></span>
2. <span data-ttu-id="3684d-123">hello 사용자 hello 정책 toohello 정책 정의 따라 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-123">hello user completes hello policy according toohello policy definition.</span></span>
3. <span data-ttu-id="3684d-124">hello 앱 hello v2.0 끝점에서 일종의 보안 토큰을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-124">hello app receives some kind of security token from hello v2.0 endpoint.</span></span>
4. <span data-ttu-id="3684d-125">hello 앱 hello 보안 보호 토큰 tooaccess 정보 또는 보호 된 리소스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-125">hello app uses hello security token tooaccess protected information or a protected resource.</span></span>
5. <span data-ttu-id="3684d-126">hello 리소스 서버에 대 한 액세스를 부여할 수 있는 hello 보안 토큰 tooverify를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-126">hello resource server validates hello security token tooverify that access can be granted.</span></span>
6. <span data-ttu-id="3684d-127">hello 앱 hello 보안 토큰을 주기적으로 새로 고쳐집니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-127">hello app periodically refreshes hello security token.</span></span>

<!-- TODO: Need a page for libraries toolink too-->
<span data-ttu-id="3684d-128">다음이 단계 hello 유형의 작성 하는 응용 프로그램에 따라 약간씩 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-128">These steps can differ slightly based on hello type of app you're building.</span></span> <span data-ttu-id="3684d-129">오픈 소스 라이브러리를 hello 세부 정보를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-129">Open source libraries can address hello details for you.</span></span>

## <a name="web-apps"></a><span data-ttu-id="3684d-130">웹 앱</span><span class="sxs-lookup"><span data-stu-id="3684d-130">Web apps</span></span>
<span data-ttu-id="3684d-131">서버에서 호스팅되며 브라우저를 통해 액세스하는 웹앱(.NET, PHP, Java, Ruby, Python, Node.js 등)의 경우 Azure AD B2C는 모든 사용자 환경에 [OpenID Connect](active-directory-b2c-reference-protocols.md) 를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-131">For web apps (including .NET, PHP, Java, Ruby, Python, and Node.js) that are hosted on a server and accessed through a browser, Azure AD B2C supports [OpenID Connect](active-directory-b2c-reference-protocols.md) for all user experiences.</span></span> <span data-ttu-id="3684d-132">여기에는 로그인, 등록 및 프로필 관리가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-132">This includes sign-in, sign-up, and profile management.</span></span> <span data-ttu-id="3684d-133">OpenID Connect의 Azure AD B2C hello 구현에서 웹 앱 인증 요청 tooAzure AD를 실행 하 여 이러한 사용자 환경을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-133">In hello Azure AD B2C implementation of OpenID Connect, your web app initiates these user experiences by issuing authentication requests tooAzure AD.</span></span> <span data-ttu-id="3684d-134">hello 요청의 hello 결과는 `id_token`합니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-134">hello result of hello request is an `id_token`.</span></span> <span data-ttu-id="3684d-135">이 보안 토큰이 hello 사용자의 id를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-135">This security token represents hello user's identity.</span></span> <span data-ttu-id="3684d-136">또한 클레임의 hello 형태로 hello 사용자에 대 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-136">It also provides information about hello user in hello form of claims:</span></span>

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

<span data-ttu-id="3684d-137">Hello에 사용할 수 있는 tooan 앱 토큰 및 클레임 유형의 hello에 대 한 자세한 정보 [B2C 토큰 참조](active-directory-b2c-reference-tokens.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-137">Learn more about hello types of tokens and claims available tooan app in hello [B2C token reference](active-directory-b2c-reference-tokens.md).</span></span>

<span data-ttu-id="3684d-138">웹앱에서 [정책](active-directory-b2c-reference-policies.md) 의 각 실행에서는 이러한 수준 높은 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-138">In a web app, each execution of a [policy](active-directory-b2c-reference-policies.md) takes these high-level steps:</span></span>

![웹앱 스윔 레인 이미지](./media/active-directory-b2c-apps/webapp.png)

<span data-ttu-id="3684d-140">유효성 검사의 hello `id_token` Azure AD에서 받은 공개 서명 키를 사용 하 여 hello 사용자 충분 한 tooverify hello id입니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-140">Validation of hello `id_token` by using a public signing key that is received from Azure AD is sufficient tooverify hello identity of hello user.</span></span> <span data-ttu-id="3684d-141">또한 후속 페이지 요청에서 사용 되는 tooidentify hello 사용자 일 수 있는 세션 쿠키를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-141">This also sets a session cookie that can be used tooidentify hello user on subsequent page requests.</span></span>

<span data-ttu-id="3684d-142">toosee 작업에서이 시나리오 중 하나를 시도 hello 웹 응용 프로그램 로그인 코드 샘플에서는 우리의 [섹션 시작](active-directory-b2c-overview.md#get-started)합니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-142">toosee this scenario in action, try one of hello web app sign-in code samples in our [Getting started section](active-directory-b2c-overview.md#get-started).</span></span>

<span data-ttu-id="3684d-143">웹 서버 응용 프로그램 추가 toofacilitating 간단한 로그인에서는 tooaccess 백 엔드 웹 서비스 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-143">In addition toofacilitating simple sign-in, a web server app might also need tooaccess a back-end web service.</span></span> <span data-ttu-id="3684d-144">이 경우 hello 웹 앱 약간 다른 수행할 수 [OpenID Connect 흐름](active-directory-b2c-reference-oidc.md) 및 권한 부여 코드를 사용 하 여 토큰을 획득 하 고 새로 고침 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-144">In this case, hello web app can perform a slightly different [OpenID Connect flow](active-directory-b2c-reference-oidc.md) and acquire tokens by using authorization codes and refresh tokens.</span></span> <span data-ttu-id="3684d-145">이 시나리오는 hello 다음에 표시 된 [웹 Api 섹션](#web-apis)합니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-145">This scenario is depicted in hello following [Web APIs section](#web-apis).</span></span>

<!--, and in our [WebApp-WebAPI Getting started topic](active-directory-b2c-devquickstarts-web-api-dotnet.md).-->

## <a name="web-apis"></a><span data-ttu-id="3684d-146">Web API</span><span class="sxs-lookup"><span data-stu-id="3684d-146">Web APIs</span></span>
<span data-ttu-id="3684d-147">앱의 RESTful 웹 API와 같은 Azure AD B2C toosecure 웹 서비스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-147">You can use Azure AD B2C toosecure web services such as your app's RESTful web API.</span></span> <span data-ttu-id="3684d-148">웹 Api 토큰을 사용 하 여 들어오는 HTTP 요청을 인증 하 여 OAuth 2.0 toosecure 해당 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-148">Web APIs can use OAuth 2.0 toosecure their data, by authenticating incoming HTTP requests using tokens.</span></span> <span data-ttu-id="3684d-149">web API의 hello 호출자의 HTTP 요청 hello 인증 헤더에 토큰을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-149">hello caller of a web API appends a token in hello authorization header of an HTTP request:</span></span>

```
GET /api/items HTTP/1.1
Host: www.mywebapi.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6...
Accept: application/json
...
```

<span data-ttu-id="3684d-150">hello 웹 API hello 토큰에서 인코딩 되는 클레임에서 hello 호출자에 대 한 hello 토큰 tooverify hello API 호출자의 id 및 tooextract 정보를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-150">hello web API can then use hello token tooverify hello API caller's identity and tooextract information about hello caller from claims that are encoded in hello token.</span></span> <span data-ttu-id="3684d-151">Hello에 사용할 수 있는 tooan 앱 토큰 및 클레임 유형의 hello에 대 한 자세한 정보 [Azure AD B2C 토큰 참조](active-directory-b2c-reference-tokens.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-151">Learn more about hello types of tokens and claims available tooan app in hello [Azure AD B2C token reference](active-directory-b2c-reference-tokens.md).</span></span>

> [!NOTE]
> <span data-ttu-id="3684d-152">Azure AD B2C는 현재 고유한 잘 알려진 클라이언트에서 액세스하는 Web API만을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-152">Azure AD B2C currently supports only web APIs that are accessed by their own well-known clients.</span></span> <span data-ttu-id="3684d-153">예를 들어 전체 앱이 iOS 앱, Android 앱 및 백 엔드 Web API를 포함할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-153">For instance, your complete app may include an iOS app, an Android app, and a back-end web API.</span></span> <span data-ttu-id="3684d-154">이 아키텍처를 완전히 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-154">This architecture is fully supported.</span></span> <span data-ttu-id="3684d-155">동일한 웹 API 현재 지원 되지 않습니다를 tooaccess hello 다른 iOS 앱 같은 파트너 클라이언트를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-155">Allowing a partner client, such as another iOS app, tooaccess hello same web API is not currently supported.</span></span> <span data-ttu-id="3684d-156">단일 응용 프로그램 ID를 공유 해야 전체 응용 프로그램의 hello 구성 요소를 모두</span><span class="sxs-lookup"><span data-stu-id="3684d-156">All of hello components of your complete app must share a single application ID.</span></span>
>
>

<span data-ttu-id="3684d-157">Web API는 웹앱, 데스크톱 및 모바일 앱, 단일 페이지 앱, 서버 쪽 데몬 및 다른 Web API까지 포함하여 많은 유형의 클라이언트에서 토큰을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-157">A web API can receive tokens from many types of clients, including web apps, desktop and mobile apps, single page apps, server-side daemons, and other web APIs.</span></span> <span data-ttu-id="3684d-158">Web API를 호출 하는 웹 앱에 대 한 hello 전체 흐름의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-158">Here's an example of hello complete flow for a web app that calls a web API:</span></span>

![웹앱 Web API 스윔 레인 이미지](./media/active-directory-b2c-apps/webapi.png)

<span data-ttu-id="3684d-160">hello에 대 한 읽기 권한 부여 코드, 새로 고침 토큰 및 토큰을 가져오기 위한 hello 단계에 대해 자세히 toolearn [OAuth 2.0 프로토콜](active-directory-b2c-reference-oauth-code.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-160">toolearn more about authorization codes, refresh tokens, and hello steps for getting tokens, read about hello [OAuth 2.0 protocol](active-directory-b2c-reference-oauth-code.md).</span></span>

<span data-ttu-id="3684d-161">방법을 Azure AD B2C 체크 아웃 hello 사용 하 여 웹 API toosecure 웹의 자습서에서는 API toolearn 우리의 [섹션 시작](active-directory-b2c-overview.md#get-started)합니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-161">toolearn how toosecure a web API by using Azure AD B2C, check out hello web API tutorials in our [Getting started section](active-directory-b2c-overview.md#get-started).</span></span>

## <a name="mobile-and-native-apps"></a><span data-ttu-id="3684d-162">모바일 및 네이티브 앱</span><span class="sxs-lookup"><span data-stu-id="3684d-162">Mobile and native apps</span></span>
<span data-ttu-id="3684d-163">모바일 및 데스크톱 앱 같은 장치에 설치 된 앱을 tooaccess 백 엔드 서비스 또는 사용자 대신 웹 Api 필요한 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-163">Apps that are installed on devices, such as mobile and desktop apps, often need tooaccess back-end services or web APIs on behalf of users.</span></span> <span data-ttu-id="3684d-164">사용자 지정 된 id 관리 환경을 tooyour 네이티브 앱을 추가 하 고 안전 하 게 Azure AD B2C 및 hello를 사용 하 여 백 엔드 서비스를 호출할 수 [OAuth 2.0 인증 코드 흐름](active-directory-b2c-reference-oauth-code.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-164">You can add customized identity management experiences tooyour native apps and securely call back-end services by using Azure AD B2C and hello [OAuth 2.0 authorization code flow](active-directory-b2c-reference-oauth-code.md).</span></span>  

<span data-ttu-id="3684d-165">Hello 응용 프로그램 실행이 흐름에서 [정책](active-directory-b2c-reference-policies.md) 수신는 `authorization_code` hello 사용자 hello 정책 완료 된 후에 Azure AD에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-165">In this flow, hello app executes [policies](active-directory-b2c-reference-policies.md) and receives an `authorization_code` from Azure AD after hello user completes hello policy.</span></span> <span data-ttu-id="3684d-166">hello `authorization_code` 나타냅니다 hello hello 사용자가 현재 로그인를 위해 응용 프로그램의 사용 권한 toocall 백 엔드 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-166">hello `authorization_code` represents hello app's permission toocall back-end services on behalf of hello user who is currently signed in.</span></span> <span data-ttu-id="3684d-167">hello 앱 hello를 교환할 수 있습니다 `authorization_code` 에 대 한 hello 백그라운드로 `id_token` 및 `refresh_token`합니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-167">hello app can then exchange hello `authorization_code` in hello background for an `id_token` and a `refresh_token`.</span></span>  <span data-ttu-id="3684d-168">hello 앱 hello צ ְ ײ `id_token` tooauthenticate tooa 백 엔드에 web API의 HTTP 요청입니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-168">hello app can use hello `id_token` tooauthenticate tooa back-end web API in HTTP requests.</span></span> <span data-ttu-id="3684d-169">Hello를 사용할 수도 있습니다 `refresh_token` 새 tooget `id_token` 이전 만료 될 때입니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-169">It can also use hello `refresh_token` tooget a new `id_token` when an older one expires.</span></span>

> [!NOTE]
> <span data-ttu-id="3684d-170">Azure AD B2C는 현재 토큰을 사용 하는 tooaccess 응용 프로그램 자체의 백 엔드 웹 서비스를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-170">Azure AD B2C currently supports only tokens that are used tooaccess an app's own back-end web service.</span></span> <span data-ttu-id="3684d-171">예를 들어 전체 앱이 iOS 앱, Android 앱 및 백 엔드 Web API를 포함할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-171">For instance, your complete app may include an iOS app, an Android app, and a back-end web API.</span></span> <span data-ttu-id="3684d-172">이 아키텍처를 완전히 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-172">This architecture is fully supported.</span></span> <span data-ttu-id="3684d-173">OAuth 2.0 액세스 토큰을 사용 하 여 iOS 앱 tooaccess 파트너 웹 API를 허용 현재 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-173">Allowing your iOS app tooaccess a partner web API by using OAuth 2.0 access tokens is not currently supported.</span></span> <span data-ttu-id="3684d-174">단일 응용 프로그램 ID를 공유 해야 전체 응용 프로그램의 hello 구성 요소를 모두</span><span class="sxs-lookup"><span data-stu-id="3684d-174">All of hello components of your complete app must share a single application ID.</span></span>
>
>

![네이티브 앱 스윔 레인 이미지](./media/active-directory-b2c-apps/native.png)

## <a name="current-limitations"></a><span data-ttu-id="3684d-176">현재 제한 사항</span><span class="sxs-lookup"><span data-stu-id="3684d-176">Current limitations</span></span>
<span data-ttu-id="3684d-177">Azure AD B2C hello 유형의 앱을 다음 현재 지원 하지 않지만 hello 로드맵에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-177">Azure AD B2C does not currently support hello following types of apps, but they are on hello roadmap.</span></span> 

### <a name="daemonsserver-side-apps"></a><span data-ttu-id="3684d-178">디먼/서버 쪽 앱</span><span class="sxs-lookup"><span data-stu-id="3684d-178">Daemons/server-side apps</span></span>
<span data-ttu-id="3684d-179">장기 실행 프로세스를 포함 하는 또는 사용자의 hello 존재 하지 않고 작동 하는 앱 tooaccess 웹 Api와 같은 리소스를 보호 하는 방법이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-179">Apps that contain long-running processes or that operate without hello presence of a user also need a way tooaccess secured resources such as web APIs.</span></span> <span data-ttu-id="3684d-180">이러한 응용 프로그램 인증 하 고 hello 응용 프로그램 id (사용자의 위임 된 id 아님)를 사용 하 고 hello OAuth 2.0 클라이언트 자격 증명 흐름을 사용 하 여 토큰을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-180">These apps can authenticate and get tokens by using hello app's identity (rather than a user's delegated identity) and by using hello OAuth 2.0 client credentials flow.</span></span>

<span data-ttu-id="3684d-181">이 흐름은 Azure AD B2C에서 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-181">This flow is not currently supported by Azure AD B2C.</span></span> <span data-ttu-id="3684d-182">이러한 앱은 대화형 사용자 흐름이 발생한 후에만 토큰을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-182">These apps can get tokens only after an interactive user flow has occurred.</span></span>

### <a name="web-api-chains-on-behalf-of-flow"></a><span data-ttu-id="3684d-183">Web API 체인(On-Behalf-Of 흐름)</span><span class="sxs-lookup"><span data-stu-id="3684d-183">Web API chains (on-behalf-of flow)</span></span>
<span data-ttu-id="3684d-184">웹 API에 필요한 toocall 여기서 Azure AD B2C 통해 보안 되며 둘 다 다른 다운스트림 웹 API를 포함 하는 많은 아키텍처.</span><span class="sxs-lookup"><span data-stu-id="3684d-184">Many architectures include a web API that needs toocall another downstream web API, where both are secured by Azure AD B2C.</span></span> <span data-ttu-id="3684d-185">이 시나리오는 Web API 백 엔드를 가지고 있는 네이티브 클라이언트에서 일반적입니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-185">This scenario is common in native clients that have a Web API back-end.</span></span> <span data-ttu-id="3684d-186">이 다음 hello Azure AD Graph API와 같은 Microsoft 온라인 서비스를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-186">This then calls a Microsoft online service such as hello Azure AD Graph API.</span></span>

<span data-ttu-id="3684d-187">Hello OAuth 2.0 JWT 전달자 자격 증명 부여 라고도 hello에-를 대신 하 여-의 흐름을 사용 하 여이 연결 된 웹 API 시나리오를 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-187">This chained web API scenario can be supported by using hello OAuth 2.0 JWT bearer credential grant, also known as hello on-behalf-of flow.</span></span>  <span data-ttu-id="3684d-188">그러나 Azure AD B2C hello에 hello에 대신-흐름 현재 구현 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3684d-188">However, hello on-behalf-of flow is not currently implemented in hello Azure AD B2C.</span></span>

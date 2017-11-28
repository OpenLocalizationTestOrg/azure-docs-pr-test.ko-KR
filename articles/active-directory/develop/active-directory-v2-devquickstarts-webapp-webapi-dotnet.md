---
title: "AD aaaAzure v2.0.NET 웹 응용 프로그램 API를 호출 시작 | Microsoft Docs"
description: "어떻게 toobuild 호출 하는.NET MVC 웹 응용 프로그램 웹 개인 Microsoft를 사용 하 여 서비스 계정 되 및 회사 또는 학교 계정을 로그인에 대 한."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 56be906e-71de-469d-9a5c-9fc08aae4223
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 1a70791418bc2a7d1fdfbafb9b5126a033a32292
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="calling-a-web-api-from-a-net-web-app"></a><span data-ttu-id="9d0b8-103">.NET 웹앱에서 Web API 호출</span><span class="sxs-lookup"><span data-stu-id="9d0b8-103">Calling a web API from a .NET web app</span></span>
<span data-ttu-id="9d0b8-104">Hello v2.0 끝점과 인증 tooyour 웹 앱을 추가 하 고 두 개인 Microsoft 계정에 대 한 지원 및 회사 또는 학교 계정을 사용 하 여 웹 Api 신속 하 게 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d0b8-104">With hello v2.0 endpoint, you can quickly add authentication tooyour web apps and web APIs with support for both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="9d0b8-105">여기서는 Microsoft OWIN 미들웨어를 활용하여 OpenID Connect로 사용자를 로그인하는 MVC 웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9d0b8-105">Here, we'll build an MVC web app that signs users in using OpenID Connect, with some help from Microsoft's OWIN middleware.</span></span>  <span data-ttu-id="9d0b8-106">hello 웹 응용 프로그램 허용 하는 OAuth 2.0으로 보호 되는 api 만들기 웹에 대 한 OAuth 2.0 액세스 토큰 가져오기, 읽기 및 삭제는 지정 된 사용자의 "할 일 목록에" 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9d0b8-106">hello web app will get OAuth 2.0 access tokens for a web api secured by OAuth 2.0 that allows create, read, and delete on a given user's "To-Do List".</span></span>

<span data-ttu-id="9d0b8-107">이 자습서 MSAL tooacquire 사용에 초점을 전체에 설명 된 웹 응용 프로그램에서 액세스 토큰을 사용 하 여 [여기](active-directory-v2-flows.md#web-apps)합니다.</span><span class="sxs-lookup"><span data-stu-id="9d0b8-107">This tutorial will focus primarily on using MSAL tooacquire and use access tokens in a web app, described in full [here](active-directory-v2-flows.md#web-apps).</span></span>  <span data-ttu-id="9d0b8-108">서 필수 구성 요소를 만들 수 있습니다 toofirst 너무 방법을 알아보려면[tooa 로그인 기본 웹 응용 프로그램 추가](active-directory-v2-devquickstarts-dotnet-web.md) 또는 너무 어떻게[web API를 제대로 보호](active-directory-v2-devquickstarts-dotnet-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9d0b8-108">As prerequisites, you may want toofirst learn how too[add basic sign-in tooa web app](active-directory-v2-devquickstarts-dotnet-web.md) or how too[properly secure a web API](active-directory-v2-devquickstarts-dotnet-api.md).</span></span>

> [!NOTE]
> <span data-ttu-id="9d0b8-109">모든 Azure Active Directory 시나리오 및 기능 hello v2.0 끝점에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d0b8-109">Not all Azure Active Directory scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="9d0b8-110">에 대해 알아보세요 hello v2.0 끝점을 사용 해야 하는 경우 toodetermine [v2.0 제한](active-directory-v2-limitations.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9d0b8-110">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download-sample-code"></a><span data-ttu-id="9d0b8-111">샘플 코드 다운로드</span><span class="sxs-lookup"><span data-stu-id="9d0b8-111">Download sample code</span></span>
<span data-ttu-id="9d0b8-112">이 자습서에 대 한 hello 코드 유지 관리 [GitHub에서](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet)합니다.</span><span class="sxs-lookup"><span data-stu-id="9d0b8-112">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet).</span></span>  <span data-ttu-id="9d0b8-113">수에 따라 toofollow, [.zip으로 hello 응용 프로그램의 기본 정의 다운로드](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/skeleton.zip) 또는 복제 hello 스 켈 레 톤:</span><span class="sxs-lookup"><span data-stu-id="9d0b8-113">toofollow along, you can [download hello app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/skeleton.zip) or clone hello skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet.git```

<span data-ttu-id="9d0b8-114">수 또는 [.zip으로 완료 하는 hello 앱을 다운로드](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip) 또는 복제를 완료 하는 hello 앱:</span><span class="sxs-lookup"><span data-stu-id="9d0b8-114">Alternatively, you can [download hello completed app as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip) or clone hello completed app:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet.git```

## <a name="register-an-app"></a><span data-ttu-id="9d0b8-115">앱 등록</span><span class="sxs-lookup"><span data-stu-id="9d0b8-115">Register an app</span></span>
<span data-ttu-id="9d0b8-116">[apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)에서 새 앱을 만들거나 다음 [세부 단계](active-directory-v2-app-registration.md)를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="9d0b8-116">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="9d0b8-117">다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d0b8-117">Make sure to:</span></span>

* <span data-ttu-id="9d0b8-118">Hello 아래로 복사 **응용 프로그램 Id** tooyour 응용 프로그램에 할당 해야 곧 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d0b8-118">Copy down hello **Application Id** assigned tooyour app, you'll need it soon.</span></span>
* <span data-ttu-id="9d0b8-119">만들기는 **응용 프로그램 암호** 의 hello **암호** 유형 및 나중에 해당 값 아래로 복사</span><span class="sxs-lookup"><span data-stu-id="9d0b8-119">Create an **App Secret** of hello **Password** type, and copy down its value for later</span></span>
* <span data-ttu-id="9d0b8-120">Hello 추가 **웹** 응용 프로그램을 위한 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="9d0b8-120">Add hello **Web** platform for your app.</span></span>
* <span data-ttu-id="9d0b8-121">올바른 hello 입력 **리디렉션 URI**합니다.</span><span class="sxs-lookup"><span data-stu-id="9d0b8-121">Enter hello correct **Redirect URI**.</span></span> <span data-ttu-id="9d0b8-122">hello 리디렉션 uri 나타냅니다 tooAzure AD에 인증 응답 디렉션할-hello 기본적으로이 자습서는 `https://localhost:44326/`합니다.</span><span class="sxs-lookup"><span data-stu-id="9d0b8-122">hello redirect uri indicates tooAzure AD where authentication responses should be directed - hello default for this tutorial is `https://localhost:44326/`.</span></span>

## <a name="install-owin"></a><span data-ttu-id="9d0b8-123">OWIN 설치</span><span class="sxs-lookup"><span data-stu-id="9d0b8-123">Install OWIN</span></span>
<span data-ttu-id="9d0b8-124">Hello OWIN 미들웨어 NuGet 패키지 toohello 추가 `TodoList-WebApp` 패키지 관리자 콘솔 hello 사용 하 여 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="9d0b8-124">Add hello OWIN middleware NuGet packages toohello `TodoList-WebApp` project using hello Package Manager Console.</span></span>  <span data-ttu-id="9d0b8-125">hello OWIN 미들웨어 tooissue 사용 되는 로그인 및 로그 아웃 요청, hello 사용자의 세션을 관리 되며 다른 작업 간에 hello 사용자에 대 한 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="9d0b8-125">hello OWIN middleware will be used tooissue sign-in and sign-out requests, manage hello user's session, and get information about hello user, amongst other things.</span></span>

```
PM> Install-Package Microsoft.Owin.Security.OpenIdConnect -ProjectName TodoList-WebApp
PM> Install-Package Microsoft.Owin.Security.Cookies -ProjectName TodoList-WebApp
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoList-WebApp
```

## <a name="sign-hello-user-in"></a><span data-ttu-id="9d0b8-126">로그인 hello 사용자</span><span class="sxs-lookup"><span data-stu-id="9d0b8-126">Sign hello user in</span></span>
<span data-ttu-id="9d0b8-127">이제 hello OWIN 미들웨어 toouse hello 구성할 [OpenID Connect 인증 프로토콜](active-directory-v2-protocols.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9d0b8-127">Now configure hello OWIN middleware toouse hello [OpenID Connect authentication protocol](active-directory-v2-protocols.md).</span></span>  

* <span data-ttu-id="9d0b8-128">열기 hello `web.config` hello의 hello 루트에 파일 `TodoList-WebApp` hello에 응용 프로그램의 구성 값을 입력 하 고 프로젝트를 `<appSettings>` 섹션.</span><span class="sxs-lookup"><span data-stu-id="9d0b8-128">Open hello `web.config` file in hello root of hello `TodoList-WebApp` project, and enter your app's configuration values in hello `<appSettings>` section.</span></span>
  * <span data-ttu-id="9d0b8-129">hello `ida:ClientId` 는 hello **응용 프로그램 Id** hello 등록 포털에서 tooyour 응용 프로그램을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d0b8-129">hello `ida:ClientId` is hello **Application Id** assigned tooyour app in hello registration portal.</span></span>
  * <span data-ttu-id="9d0b8-130">hello `ida:ClientSecret` 는 hello **응용 프로그램 암호** hello 등록 포털에서 만든 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d0b8-130">hello `ida:ClientSecret` is hello **App Secret** you created in hello registration portal.</span></span>
  * <span data-ttu-id="9d0b8-131">hello `ida:RedirectUri` 는 hello **리디렉션 Uri** hello 포털에 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d0b8-131">hello `ida:RedirectUri` is hello **Redirect Uri** you entered in hello portal.</span></span>
* <span data-ttu-id="9d0b8-132">열기 hello `web.config` hello의 hello 루트에 파일 `TodoList-Service` 프로젝트를 바꾸고 hello `ida:Audience` 동일 hello **응용 프로그램 Id** 위와 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d0b8-132">Open hello `web.config` file in hello root of hello `TodoList-Service` project, and replace hello `ida:Audience` with hello same **Application Id** as above.</span></span>
* <span data-ttu-id="9d0b8-133">파일 열기 hello `App_Start\Startup.Auth.cs` 추가 `using` 위에서 hello 라이브러리에 대 한 문.</span><span class="sxs-lookup"><span data-stu-id="9d0b8-133">Open hello file `App_Start\Startup.Auth.cs` and add `using` statements for hello libraries from above.</span></span>
* <span data-ttu-id="9d0b8-134">동일한 파일 hello 하 hello 구현 `ConfigureAuth(...)` 메서드.</span><span class="sxs-lookup"><span data-stu-id="9d0b8-134">In hello same file, implement hello `ConfigureAuth(...)` method.</span></span>  <span data-ttu-id="9d0b8-135">매개 변수가 hello `OpenIDConnectAuthenticationOptions` 좌표 Azure AD와 앱 toocommunicate 프로그램에 대 한 역할을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d0b8-135">hello parameters you provide in `OpenIDConnectAuthenticationOptions` will serve as coordinates for your app toocommunicate with Azure AD.</span></span>

```C#
public void ConfigureAuth(IAppBuilder app)
{
    app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

    app.UseCookieAuthentication(new CookieAuthenticationOptions());

    app.UseOpenIdConnectAuthentication(
        new OpenIdConnectAuthenticationOptions
        {

                    // hello `Authority` represents hello v2.0 endpoint - https://login.microsoftonline.com/common/v2.0
                    // hello `Scope` describes hello permissions that your app will need.  See https://azure.microsoft.com/documentation/articles/active-directory-v2-scopes/
                    // In a real application you could use issuer validation for additional checks, like making sure hello user's organization has signed up for your app, for instance.

                    ClientId = clientId,
                    Authority = String.Format(CultureInfo.InvariantCulture, aadInstance, "common", "/v2.0 "),
                    Scope = "openid email profile offline_access",
                    RedirectUri = redirectUri,
                    PostLogoutRedirectUri = redirectUri,
                    TokenValidationParameters = new TokenValidationParameters
                    {
                        ValidateIssuer = false,
                    },

                    // hello `AuthorizationCodeReceived` notification is used toocapture and redeem hello authorization_code that hello v2.0 endpoint returns tooyour app.

                    Notifications = new OpenIdConnectAuthenticationNotifications
                    {
                        AuthenticationFailed = OnAuthenticationFailed,
                        AuthorizationCodeReceived = OnAuthorizationCodeReceived,
                    }

        });
}
// ...
```

## <a name="use-msal-tooget-access-tokens"></a><span data-ttu-id="9d0b8-136">MSAL tooget 액세스 토큰을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="9d0b8-136">Use MSAL tooget access tokens</span></span>
<span data-ttu-id="9d0b8-137">Hello에 `AuthorizationCodeReceived` 알림을 toouse 원하는 [OpenID Connect와 함께에서 OAuth 2.0](active-directory-v2-protocols.md) tooredeem hello authorization_code 액세스 토큰 toohello 할 일 목록 서비스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d0b8-137">In hello `AuthorizationCodeReceived` notification, we want toouse [OAuth 2.0 in tandem with OpenID Connect](active-directory-v2-protocols.md) tooredeem hello authorization_code for an access token toohello To-Do List Service.</span></span>  <span data-ttu-id="9d0b8-138">MSAL을 통해 이 프로세스를 쉽게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d0b8-138">MSAL can make this process easy for you:</span></span>

* <span data-ttu-id="9d0b8-139">먼저, MSAL의 hello 미리 보기 버전을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d0b8-139">First, install hello preview version of MSAL:</span></span>

```PM> Install-Package Microsoft.Identity.Client -ProjectName TodoList-WebApp -IncludePrerelease```

* <span data-ttu-id="9d0b8-140">다른 항목 추가 및 `using` 문 toohello `App_Start\Startup.Auth.cs` MSAL에 대 한 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="9d0b8-140">And add another `using` statement toohello `App_Start\Startup.Auth.cs` file for MSAL.</span></span>
* <span data-ttu-id="9d0b8-141">이제는 새 메서드를 추가할 hello `OnAuthorizationCodeReceived` 이벤트 처리기입니다.</span><span class="sxs-lookup"><span data-stu-id="9d0b8-141">Now add a new method, hello `OnAuthorizationCodeReceived` event handler.</span></span>  <span data-ttu-id="9d0b8-142">이 처리기는 MSAL tooacquire 액세스 토큰 toohello 할 일 목록 API를 사용 하 고 나중에 대 한 hello 토큰 MSAL의 토큰 캐시에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9d0b8-142">This handler will use MSAL tooacquire an access token toohello To-Do List API, and will store hello token in MSAL's token cache for later:</span></span>

```C#
private async Task OnAuthorizationCodeReceived(AuthorizationCodeReceivedNotification notification)
{
        string userObjectId = notification.AuthenticationTicket.Identity.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
        string tenantID = notification.AuthenticationTicket.Identity.FindFirst("http://schemas.microsoft.com/identity/claims/tenantid").Value;
        string authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenantID, string.Empty);
        ClientCredential cred = new ClientCredential(clientId, clientSecret);

        // Here you ask for a token using hello web app's clientId as hello scope, since hello web app and service share hello same clientId.
        app = new ConfidentialClientApplication(Startup.clientId, redirectUri, cred, new NaiveSessionCache(userObjectId, notification.OwinContext.Environment["System.Web.HttpContextBase"] as HttpContextBase)) {};
        var authResult = await app.AcquireTokenByAuthorizationCodeAsync(new string[] { clientId }, notification.Code);
}
// ...
```

* <span data-ttu-id="9d0b8-143">웹 앱에서 MSAL 사용된 toostore 토큰 일 수 있는 확장 가능한 토큰 캐시는에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d0b8-143">In web apps, MSAL has an extensible token cache that can be used toostore tokens.</span></span>  <span data-ttu-id="9d0b8-144">이 샘플 구현 hello `NaiveSessionCache` http 세션 저장소 toocache 토큰을 사용 하 여입니다.</span><span class="sxs-lookup"><span data-stu-id="9d0b8-144">This sample implements hello `NaiveSessionCache` which uses http session storage toocache tokens.</span></span>

<!-- TODO: Token Cache article -->


## <a name="call-hello-web-api"></a><span data-ttu-id="9d0b8-145">Hello 웹 API를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d0b8-145">Call hello Web API</span></span>
<span data-ttu-id="9d0b8-146">이제 tooactually 3 단계에서 복사한 hello access_token을 사용 하는 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="9d0b8-146">Now it's time tooactually use hello access_token you acquired in step 3.</span></span>  <span data-ttu-id="9d0b8-147">열기 hello 웹 앱의 `Controllers\TodoListController.cs` 파일, toohello 할 일 목록 API 요청 모든 hello CRUD 수 있게 해줍니다.</span><span class="sxs-lookup"><span data-stu-id="9d0b8-147">Open hello web app's `Controllers\TodoListController.cs` file, which makes all hello CRUD requests toohello To-Do List API.</span></span>

* <span data-ttu-id="9d0b8-148">MSAL를 사용할 수 있습니다 다시 여기 hello MSAL 캐시에서 toofetch access_tokens 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d0b8-148">You can use MSAL again here toofetch access_tokens from hello MSAL cache.</span></span>  <span data-ttu-id="9d0b8-149">먼저 추가 하는 `using` MSAL toothis 파일에 대 한 문입니다.</span><span class="sxs-lookup"><span data-stu-id="9d0b8-149">First, add a `using` statement for MSAL toothis file.</span></span>
  
    `using Microsoft.Identity.Client;`
* <span data-ttu-id="9d0b8-150">Hello에 `Index` 동작을 사용 하 여 MSAL의 `AcquireTokenSilentAsync` 메서드 tooget hello 할 일 목록 서비스에서에서 사용 되는 tooread 데이터 일 수 있는 access_token:</span><span class="sxs-lookup"><span data-stu-id="9d0b8-150">In hello `Index` action, use MSAL's `AcquireTokenSilentAsync` method tooget an access_token that can be used tooread data from hello To-Do List service:</span></span>

```C#
// ...
string userObjectID = ClaimsPrincipal.Current.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
string tenantID = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/tenantid").Value;
string authority = String.Format(CultureInfo.InvariantCulture, Startup.aadInstance, tenantID, string.Empty);
ClientCredential credential = new ClientCredential(Startup.clientId, Startup.clientSecret);

// Here you ask for a token using hello web app's clientId as hello scope, since hello web app and service share hello same clientId.
app = new ConfidentialClientApplication(Startup.clientId, redirectUri, credential, new NaiveSessionCache(userObjectID, this.HttpContext)){};
result = await app.AcquireTokenSilentAsync(new string[] { Startup.clientId });
// ...
```

* <span data-ttu-id="9d0b8-151">hello 추가 hello 나타나는 토큰 toohello HTTP GET 요청으로 hello `Authorization` tooauthenticate hello 요청을 사용 하 여 hello 할 일 목록 서비스 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="9d0b8-151">hello sample then adds hello resulting token toohello HTTP GET request as hello `Authorization` header, which hello To-Do List service uses tooauthenticate hello request.</span></span>
* <span data-ttu-id="9d0b8-152">Hello 할 일 목록 서비스에서 반환 하는 경우는 `401 Unauthorized` 응답으로 hello access_tokens MSAL에서 무효화 된 몇 가지 이유로 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d0b8-152">If hello To-Do List service returns a `401 Unauthorized` response, hello access_tokens in MSAL have become invalid for some reason.</span></span>  <span data-ttu-id="9d0b8-153">이 경우 모든 access_tokens hello MSAL 캐시에서에서 삭제 하 고 hello 사용자를 다시는 다시 시작 됩니다 hello 토큰 획득 흐름에서 toosign 할 수 있습니다 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d0b8-153">In this case, you should drop any access_tokens from hello MSAL cache and show hello user a message that they may need toosign in again, which will restart hello token acquisition flow.</span></span>

```C#
// ...
// If hello call failed with access denied, then drop hello current access token from hello cache,
// and show hello user an error indicating they might need toosign-in again.
if (response.StatusCode == System.Net.HttpStatusCode.Unauthorized)
{
        app.AppTokenCache.Clear(Startup.clientId);

        return new RedirectResult("/Error?message=Error: " + response.ReasonPhrase + " You might need toosign in again.");
}
// ...
```

* <span data-ttu-id="9d0b8-154">마찬가지로, MSAL 어떤 이유로 든 없습니다 tooreturn는 access_token 경우에 hello 사용자 toosign에서 다시 지시 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d0b8-154">Similarly, if MSAL is unable tooreturn an access_token for any reason, you should instruct hello user toosign in again.</span></span>  <span data-ttu-id="9d0b8-155">이는 `MSALException` catch만큼 단순합니다.</span><span class="sxs-lookup"><span data-stu-id="9d0b8-155">This is as simple as catching any `MSALException`:</span></span>

```C#
// ...
catch (MsalException ee)
{
        // If MSAL could not get a token silently, show hello user an error indicating they might need toosign in again.
        return new RedirectResult("/Error?message=An Error Occurred Reading tooDo List: " + ee.Message + " You might need toolog out and log back in.");
}
// ...
```

* <span data-ttu-id="9d0b8-156">hello 정확히 동일한 `AcquireTokenSilentAsync` 호출은 hello에 implementd `Create` 및 `Delete` 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d0b8-156">hello exact same `AcquireTokenSilentAsync` call is implementd in hello `Create` and `Delete` actions.</span></span>  <span data-ttu-id="9d0b8-157">웹 응용 프로그램에서 응용 프로그램에서 필요할 때마다이 MSAL 메서드 tooget access_tokens를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d0b8-157">In web apps, you can use this MSAL method tooget access_tokens whenever you need them in your app.</span></span>  <span data-ttu-id="9d0b8-158">MSAL이 자동으로 토큰 획득, 캐싱 및 새로 고침을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="9d0b8-158">MSAL will take care of acquiring, caching, and refreshing tokens for you.</span></span>

<span data-ttu-id="9d0b8-159">마지막으로 앱을 빌드하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9d0b8-159">Finally, build and run your app!</span></span>  <span data-ttu-id="9d0b8-160">Microsoft 계정 또는 Azure AD 계정을 사용 하 여 로그인 하 고 hello 사용자의 id hello 위쪽 탐색 모음에 어떻게 반영 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9d0b8-160">Sign in with either a Microsoft Account or an Azure AD Account, and notice how hello user's identity is reflected in hello top navigation bar.</span></span>  <span data-ttu-id="9d0b8-161">추가 하 고 hello 사용자의 할 일 목록 toosee hello OAuth 2.0 API 보호 작업의 호출에서 일부 항목을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d0b8-161">Add and delete some items from hello user's To-Do List toosee hello OAuth 2.0 secured API calls in action.</span></span>  <span data-ttu-id="9d0b8-162">이제 개인 및 회사/학교 계정으로 사용자를 인증할 수 있는 업계 표준 프로토콜을 사용하여 웹앱 및 Web API가 보안되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9d0b8-162">You now have a web app & web API, both secured using industry standard protocols, that can authenticate users with both their personal and work/school accounts.</span></span>

<span data-ttu-id="9d0b8-163">참조용으로 hello 완료 (구성 값) 없이 샘플 [을 제공](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip)합니다.</span><span class="sxs-lookup"><span data-stu-id="9d0b8-163">For reference, hello completed sample (without your configuration values) [is provided here](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip).</span></span>  

## <a name="next-steps"></a><span data-ttu-id="9d0b8-164">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9d0b8-164">Next Steps</span></span>
<span data-ttu-id="9d0b8-165">추가 리소스는 다음을 확인해보세요.</span><span class="sxs-lookup"><span data-stu-id="9d0b8-165">For additional resources, check out:</span></span>

* [<span data-ttu-id="9d0b8-166">hello v2.0 개발자 가이드 >></span><span class="sxs-lookup"><span data-stu-id="9d0b8-166">hello v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="9d0b8-167">StackOverflow "azure-active-directory" 태그 >></span><span class="sxs-lookup"><span data-stu-id="9d0b8-167">StackOverflow "azure-active-directory" tag >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="9d0b8-168">당사 제품에 대한 보안 업데이트 가져오기</span><span class="sxs-lookup"><span data-stu-id="9d0b8-168">Get security updates for our products</span></span>
<span data-ttu-id="9d0b8-169">보안 사고를 방문 하 여 발생 하는 경우의 알림 tooget 좋습니다 [이 페이지](https://technet.microsoft.com/security/dd252948) 및 tooSecurity 자문 경고를 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d0b8-169">We encourage you tooget notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>


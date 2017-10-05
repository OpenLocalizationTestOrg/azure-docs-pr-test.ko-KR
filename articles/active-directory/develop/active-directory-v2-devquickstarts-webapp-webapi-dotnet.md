---
title: "Azure AD v2.0 .NET 호출 API 시작하기 | Microsoft Docs"
description: "개인 Microsoft 계정과 회사 또는 학교 계정을 로그인에 사용하여 웹 서비스를 호출하는 .NET MVC 웹앱을 빌드하는 방법입니다."
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
ms.openlocfilehash: dc3162ae8e6ce622139125c2e78fa45d2e90d534
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="calling-a-web-api-from-a-net-web-app"></a><span data-ttu-id="7d2d2-103">.NET 웹앱에서 Web API 호출</span><span class="sxs-lookup"><span data-stu-id="7d2d2-103">Calling a web API from a .NET web app</span></span>
<span data-ttu-id="7d2d2-104">v2.0 끝점에서는 개인 Microsoft 계정과 회사 또는 학교 계정 둘 다를 지원하는 인증을 웹앱 및 Web API에 빠르게 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-104">With the v2.0 endpoint, you can quickly add authentication to your web apps and web APIs with support for both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="7d2d2-105">여기서는 Microsoft OWIN 미들웨어를 활용하여 OpenID Connect로 사용자를 로그인하는 MVC 웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-105">Here, we'll build an MVC web app that signs users in using OpenID Connect, with some help from Microsoft's OWIN middleware.</span></span>  <span data-ttu-id="7d2d2-106">이 웹앱은 OAuth 2.0에서 보호 된 웹 API에 대한 OAuth 2.0 액세스 토큰을 가져와서 지정된 사용자의 “할 일 목록"을 만들고, 읽고, 삭제할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-106">The web app will get OAuth 2.0 access tokens for a web api secured by OAuth 2.0 that allows create, read, and delete on a given user's "To-Do List".</span></span>

<span data-ttu-id="7d2d2-107">이 자습서에서는 주로 MSAL을 사용하여 웹앱에서 액세스 토큰을 가져오고 사용하는 방법에 중점을 두며 [여기](active-directory-v2-flows.md#web-apps)서 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-107">This tutorial will focus primarily on using MSAL to acquire and use access tokens in a web app, described in full [here](active-directory-v2-flows.md#web-apps).</span></span>  <span data-ttu-id="7d2d2-108">필수 조건으로 먼저 [웹앱에 기본 로그인을 추가](active-directory-v2-devquickstarts-dotnet-web.md)하는 방법 또는 [Web API 보안을 적절하게 유지](active-directory-v2-devquickstarts-dotnet-api.md)하는 방법을 알아보는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-108">As prerequisites, you may want to first learn how to [add basic sign-in to a web app](active-directory-v2-devquickstarts-dotnet-web.md) or how to [properly secure a web API](active-directory-v2-devquickstarts-dotnet-api.md).</span></span>

> [!NOTE]
> <span data-ttu-id="7d2d2-109">일부 Azure Active Directory 시나리오 및 기능만 v2.0 끝점에서 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-109">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="7d2d2-110">v2.0 끝점을 사용해야 하는지 확인하려면 [v2.0 제한 사항](active-directory-v2-limitations.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-110">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download-sample-code"></a><span data-ttu-id="7d2d2-111">샘플 코드 다운로드</span><span class="sxs-lookup"><span data-stu-id="7d2d2-111">Download sample code</span></span>
<span data-ttu-id="7d2d2-112">이 자습서에 대한 코드는 [GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet)에서 유지 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-112">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet).</span></span>  <span data-ttu-id="7d2d2-113">자습서에 따라 [.zip으로 앱 구조를 다운로드](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/skeleton.zip) 하거나 구조를 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-113">To follow along, you can [download the app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/skeleton.zip) or clone the skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet.git```

<span data-ttu-id="7d2d2-114">또는 [완성된 앱을 .zip으로 다운로드](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip) 하거나 완성된 된 앱을 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-114">Alternatively, you can [download the completed app as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip) or clone the completed app:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet.git```

## <a name="register-an-app"></a><span data-ttu-id="7d2d2-115">앱 등록</span><span class="sxs-lookup"><span data-stu-id="7d2d2-115">Register an app</span></span>
<span data-ttu-id="7d2d2-116">[apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)에서 새 앱을 만들거나 다음 [세부 단계](active-directory-v2-app-registration.md)를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-116">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="7d2d2-117">다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-117">Make sure to:</span></span>

* <span data-ttu-id="7d2d2-118">곧 필요하게 되므로 앱에 할당된 **응용 프로그램 ID** 를 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-118">Copy down the **Application Id** assigned to your app, you'll need it soon.</span></span>
* <span data-ttu-id="7d2d2-119">**암호** 형식의 **앱 암호**를 만들고 나중에 사용할 수 있도록 해당 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-119">Create an **App Secret** of the **Password** type, and copy down its value for later</span></span>
* <span data-ttu-id="7d2d2-120">앱에 대한 **웹** 플랫폼을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-120">Add the **Web** platform for your app.</span></span>
* <span data-ttu-id="7d2d2-121">올바른 **리디렉션 URI**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-121">Enter the correct **Redirect URI**.</span></span> <span data-ttu-id="7d2d2-122">리디렉션 URI는 인증 응답을 보내야 하는 Azure AD를 나타냅니다. 이 자습서에 대한 기본값은 `https://localhost:44326/`입니다.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-122">The redirect uri indicates to Azure AD where authentication responses should be directed - the default for this tutorial is `https://localhost:44326/`.</span></span>

## <a name="install-owin"></a><span data-ttu-id="7d2d2-123">OWIN 설치</span><span class="sxs-lookup"><span data-stu-id="7d2d2-123">Install OWIN</span></span>
<span data-ttu-id="7d2d2-124">패키지 관리자 콘솔을 사용하여 OWIN 미들웨어 NuGet 패키지를 `TodoList-WebApp` 프로젝트에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-124">Add the OWIN middleware NuGet packages to the `TodoList-WebApp` project using the Package Manager Console.</span></span>  <span data-ttu-id="7d2d2-125">OWIN 미들웨어는 로그인 및 로그아웃 요청을 실행하고, 사용자의 세션을 관리하고, 사용자에 대한 정보를 가져오는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-125">The OWIN middleware will be used to issue sign-in and sign-out requests, manage the user's session, and get information about the user, amongst other things.</span></span>

```
PM> Install-Package Microsoft.Owin.Security.OpenIdConnect -ProjectName TodoList-WebApp
PM> Install-Package Microsoft.Owin.Security.Cookies -ProjectName TodoList-WebApp
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoList-WebApp
```

## <a name="sign-the-user-in"></a><span data-ttu-id="7d2d2-126">사용자를 로그인</span><span class="sxs-lookup"><span data-stu-id="7d2d2-126">Sign the user in</span></span>
<span data-ttu-id="7d2d2-127">이제 [OpenID Connect 인증 프로토콜](active-directory-v2-protocols.md)을 사용하도록 OWIN 미들웨어를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-127">Now configure the OWIN middleware to use the [OpenID Connect authentication protocol](active-directory-v2-protocols.md).</span></span>  

* <span data-ttu-id="7d2d2-128">`TodoList-WebApp` 프로젝트 루트에 있는 `web.config` 파일을 열고 `<appSettings>` 섹션에 앱의 구성 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-128">Open the `web.config` file in the root of the `TodoList-WebApp` project, and enter your app's configuration values in the `<appSettings>` section.</span></span>
  * <span data-ttu-id="7d2d2-129">`ida:ClientId` 는 등록 포털에서 앱에 할당된 **응용 프로그램 ID** 입니다.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-129">The `ida:ClientId` is the **Application Id** assigned to your app in the registration portal.</span></span>
  * <span data-ttu-id="7d2d2-130">`ida:ClientSecret` 는 등록 포털에서 만든 **앱 암호** 입니다.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-130">The `ida:ClientSecret` is the **App Secret** you created in the registration portal.</span></span>
  * <span data-ttu-id="7d2d2-131">`ida:RedirectUri` 는 포털에서 입력한 **리디렉션 URI** 입니다.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-131">The `ida:RedirectUri` is the **Redirect Uri** you entered in the portal.</span></span>
* <span data-ttu-id="7d2d2-132">`TodoList-Service` 프로젝트의 루트에 있는 `web.config` 파일을 열고 `ida:Audience`를 위와 동일한 **응용 프로그램 ID**로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-132">Open the `web.config` file in the root of the `TodoList-Service` project, and replace the `ida:Audience` with the same **Application Id** as above.</span></span>
* <span data-ttu-id="7d2d2-133">`App_Start\Startup.Auth.cs` 파일을 열고 위의 라이브러리에 대한 `using` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-133">Open the file `App_Start\Startup.Auth.cs` and add `using` statements for the libraries from above.</span></span>
* <span data-ttu-id="7d2d2-134">동일한 파일에서 `ConfigureAuth(...)` 메서드를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-134">In the same file, implement the `ConfigureAuth(...)` method.</span></span>  <span data-ttu-id="7d2d2-135">`OpenIDConnectAuthenticationOptions` 에 제공하는 매개 변수는 앱이 Azure AD와 통신하기 위한 좌표로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-135">The parameters you provide in `OpenIDConnectAuthenticationOptions` will serve as coordinates for your app to communicate with Azure AD.</span></span>

```C#
public void ConfigureAuth(IAppBuilder app)
{
    app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

    app.UseCookieAuthentication(new CookieAuthenticationOptions());

    app.UseOpenIdConnectAuthentication(
        new OpenIdConnectAuthenticationOptions
        {

                    // The `Authority` represents the v2.0 endpoint - https://login.microsoftonline.com/common/v2.0
                    // The `Scope` describes the permissions that your app will need.  See https://azure.microsoft.com/documentation/articles/active-directory-v2-scopes/
                    // In a real application you could use issuer validation for additional checks, like making sure the user's organization has signed up for your app, for instance.

                    ClientId = clientId,
                    Authority = String.Format(CultureInfo.InvariantCulture, aadInstance, "common", "/v2.0 "),
                    Scope = "openid email profile offline_access",
                    RedirectUri = redirectUri,
                    PostLogoutRedirectUri = redirectUri,
                    TokenValidationParameters = new TokenValidationParameters
                    {
                        ValidateIssuer = false,
                    },

                    // The `AuthorizationCodeReceived` notification is used to capture and redeem the authorization_code that the v2.0 endpoint returns to your app.

                    Notifications = new OpenIdConnectAuthenticationNotifications
                    {
                        AuthenticationFailed = OnAuthenticationFailed,
                        AuthorizationCodeReceived = OnAuthorizationCodeReceived,
                    }

        });
}
// ...
```

## <a name="use-msal-to-get-access-tokens"></a><span data-ttu-id="7d2d2-136">MSAL을 사용하여 액세스 토큰 가져오기</span><span class="sxs-lookup"><span data-stu-id="7d2d2-136">Use MSAL to get access tokens</span></span>
<span data-ttu-id="7d2d2-137">`AuthorizationCodeReceived` 알림에서 [OpenID Connect와 함께 OAuth 2.0](active-directory-v2-protocols.md)을 사용하여 authorization_code를 To-Do List Service에 대한 액세스 토큰으로 교환하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-137">In the `AuthorizationCodeReceived` notification, we want to use [OAuth 2.0 in tandem with OpenID Connect](active-directory-v2-protocols.md) to redeem the authorization_code for an access token to the To-Do List Service.</span></span>  <span data-ttu-id="7d2d2-138">MSAL을 통해 이 프로세스를 쉽게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-138">MSAL can make this process easy for you:</span></span>

* <span data-ttu-id="7d2d2-139">먼저 MSAL 미리 보기 버전을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-139">First, install the preview version of MSAL:</span></span>

```PM> Install-Package Microsoft.Identity.Client -ProjectName TodoList-WebApp -IncludePrerelease```

* <span data-ttu-id="7d2d2-140">또 다른 `using` 문을 MSAL용 `App_Start\Startup.Auth.cs` 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-140">And add another `using` statement to the `App_Start\Startup.Auth.cs` file for MSAL.</span></span>
* <span data-ttu-id="7d2d2-141">이제 새 메서드인 `OnAuthorizationCodeReceived` 이벤트 처리기를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-141">Now add a new method, the `OnAuthorizationCodeReceived` event handler.</span></span>  <span data-ttu-id="7d2d2-142">이 처리기는 MSAL을 사용하여 할 일 목록 API에 대한 액세스 토큰을 가져오는 데 사용하며, 나중에 MSAL의 토큰 캐시에 토큰을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-142">This handler will use MSAL to acquire an access token to the To-Do List API, and will store the token in MSAL's token cache for later:</span></span>

```C#
private async Task OnAuthorizationCodeReceived(AuthorizationCodeReceivedNotification notification)
{
        string userObjectId = notification.AuthenticationTicket.Identity.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
        string tenantID = notification.AuthenticationTicket.Identity.FindFirst("http://schemas.microsoft.com/identity/claims/tenantid").Value;
        string authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenantID, string.Empty);
        ClientCredential cred = new ClientCredential(clientId, clientSecret);

        // Here you ask for a token using the web app's clientId as the scope, since the web app and service share the same clientId.
        app = new ConfidentialClientApplication(Startup.clientId, redirectUri, cred, new NaiveSessionCache(userObjectId, notification.OwinContext.Environment["System.Web.HttpContextBase"] as HttpContextBase)) {};
        var authResult = await app.AcquireTokenByAuthorizationCodeAsync(new string[] { clientId }, notification.Code);
}
// ...
```

* <span data-ttu-id="7d2d2-143">웹앱에서는 MSAL에 토큰을 저장하는 데 사용할 수 있는 확장 가능한 토큰 캐시가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-143">In web apps, MSAL has an extensible token cache that can be used to store tokens.</span></span>  <span data-ttu-id="7d2d2-144">이 샘플에서는 HTTP 세션 저장소를 사용하여 토큰을 캐시하는 `NaiveSessionCache` 를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-144">This sample implements the `NaiveSessionCache` which uses http session storage to cache tokens.</span></span>

<!-- TODO: Token Cache article -->


## <a name="call-the-web-api"></a><span data-ttu-id="7d2d2-145">Web API 호출</span><span class="sxs-lookup"><span data-stu-id="7d2d2-145">Call the Web API</span></span>
<span data-ttu-id="7d2d2-146">이제 3단계에서 획득한 access_token을 실제로 사용해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-146">Now it's time to actually use the access_token you acquired in step 3.</span></span>  <span data-ttu-id="7d2d2-147">To-Do List API에 대한 모든 CRUD 요청을 수행하는 웹앱의 `Controllers\TodoListController.cs` 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-147">Open the web app's `Controllers\TodoListController.cs` file, which makes all the CRUD requests to the To-Do List API.</span></span>

* <span data-ttu-id="7d2d2-148">여기서 MSAL을 다시 사용하여 MSAL 캐시에서 access_token을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-148">You can use MSAL again here to fetch access_tokens from the MSAL cache.</span></span>  <span data-ttu-id="7d2d2-149">먼저 MSAL에 대한 `using` 문을 이 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-149">First, add a `using` statement for MSAL to this file.</span></span>
  
    `using Microsoft.Identity.Client;`
* <span data-ttu-id="7d2d2-150">`Index` 작업에 MSAL의 `AcquireTokenSilentAsync` 메서드를 사용하여 To-Do List 서비스에서 데이터를 읽는 데 사용할 수 있는 access_token을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-150">In the `Index` action, use MSAL's `AcquireTokenSilentAsync` method to get an access_token that can be used to read data from the To-Do List service:</span></span>

```C#
// ...
string userObjectID = ClaimsPrincipal.Current.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
string tenantID = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/tenantid").Value;
string authority = String.Format(CultureInfo.InvariantCulture, Startup.aadInstance, tenantID, string.Empty);
ClientCredential credential = new ClientCredential(Startup.clientId, Startup.clientSecret);

// Here you ask for a token using the web app's clientId as the scope, since the web app and service share the same clientId.
app = new ConfidentialClientApplication(Startup.clientId, redirectUri, credential, new NaiveSessionCache(userObjectID, this.HttpContext)){};
result = await app.AcquireTokenSilentAsync(new string[] { Startup.clientId });
// ...
```

* <span data-ttu-id="7d2d2-151">그런 다음 샘플에서는 결과 토큰을 `Authorization` 헤더로 HTTP GET 요청에 추가합니다. To-Do List 서비스는 이 헤더를 사용하여 요청을 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-151">The sample then adds the resulting token to the HTTP GET request as the `Authorization` header, which the To-Do List service uses to authenticate the request.</span></span>
* <span data-ttu-id="7d2d2-152">To-Do List 서비스에서 `401 Unauthorized` 응답을 반환하는 경우 MSAL의 access_token이 어떤 이유로든 잘못된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-152">If the To-Do List service returns a `401 Unauthorized` response, the access_tokens in MSAL have become invalid for some reason.</span></span>  <span data-ttu-id="7d2d2-153">이 경우 MSAL 캐시에서 모든 access_token을 삭제하고 사용자에게 다시 로그인해야 할 수도 있다는 메시지를 표시해야 합니다. 다시 로그인하면 토큰 획득 흐름이 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-153">In this case, you should drop any access_tokens from the MSAL cache and show the user a message that they may need to sign in again, which will restart the token acquisition flow.</span></span>

```C#
// ...
// If the call failed with access denied, then drop the current access token from the cache,
// and show the user an error indicating they might need to sign-in again.
if (response.StatusCode == System.Net.HttpStatusCode.Unauthorized)
{
        app.AppTokenCache.Clear(Startup.clientId);

        return new RedirectResult("/Error?message=Error: " + response.ReasonPhrase + " You might need to sign in again.");
}
// ...
```

* <span data-ttu-id="7d2d2-154">마찬가지로, MSAL이 어떤 이유로든 access_token을 반환할 수 없는 경우 다시 로그인하도록 사용자에게 지시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-154">Similarly, if MSAL is unable to return an access_token for any reason, you should instruct the user to sign in again.</span></span>  <span data-ttu-id="7d2d2-155">이는 `MSALException` catch만큼 단순합니다.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-155">This is as simple as catching any `MSALException`:</span></span>

```C#
// ...
catch (MsalException ee)
{
        // If MSAL could not get a token silently, show the user an error indicating they might need to sign in again.
        return new RedirectResult("/Error?message=An Error Occurred Reading To Do List: " + ee.Message + " You might need to log out and log back in.");
}
// ...
```

* <span data-ttu-id="7d2d2-156">정확히 동일한 `AcquireTokenSilentAsync` 호출이 `Create` 및 `Delete` 작업에서 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-156">The exact same `AcquireTokenSilentAsync` call is implementd in the `Create` and `Delete` actions.</span></span>  <span data-ttu-id="7d2d2-157">웹앱에서 이 MSAL 메서드를 사용하여 앱에 필요할 때마다 access_token을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-157">In web apps, you can use this MSAL method to get access_tokens whenever you need them in your app.</span></span>  <span data-ttu-id="7d2d2-158">MSAL이 자동으로 토큰 획득, 캐싱 및 새로 고침을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-158">MSAL will take care of acquiring, caching, and refreshing tokens for you.</span></span>

<span data-ttu-id="7d2d2-159">마지막으로 앱을 빌드하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-159">Finally, build and run your app!</span></span>  <span data-ttu-id="7d2d2-160">Microsoft 계정이나 Azure AD 계정으로 로그인하고 위쪽 탐색 모음에 사용자 ID가 반영되는 방식을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-160">Sign in with either a Microsoft Account or an Azure AD Account, and notice how the user's identity is reflected in the top navigation bar.</span></span>  <span data-ttu-id="7d2d2-161">사용자의 할 일 모음에서 일부 항목을 추가 및 삭제하여 OAuth 2.0 보안 API 호출의 작동 방식을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-161">Add and delete some items from the user's To-Do List to see the OAuth 2.0 secured API calls in action.</span></span>  <span data-ttu-id="7d2d2-162">이제 개인 및 회사/학교 계정으로 사용자를 인증할 수 있는 업계 표준 프로토콜을 사용하여 웹앱 및 Web API가 보안되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-162">You now have a web app & web API, both secured using industry standard protocols, that can authenticate users with both their personal and work/school accounts.</span></span>

<span data-ttu-id="7d2d2-163">참조를 위해 완성된 샘플(사용자 구성 값 제외)이 [여기](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip)에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-163">For reference, the completed sample (without your configuration values) [is provided here](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip).</span></span>  

## <a name="next-steps"></a><span data-ttu-id="7d2d2-164">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7d2d2-164">Next Steps</span></span>
<span data-ttu-id="7d2d2-165">추가 리소스는 다음을 확인해보세요.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-165">For additional resources, check out:</span></span>

* [<span data-ttu-id="7d2d2-166">개발자 가이드 v2.0 >></span><span class="sxs-lookup"><span data-stu-id="7d2d2-166">The v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="7d2d2-167">StackOverflow "azure-active-directory" 태그 >></span><span class="sxs-lookup"><span data-stu-id="7d2d2-167">StackOverflow "azure-active-directory" tag >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="7d2d2-168">당사 제품에 대한 보안 업데이트 가져오기</span><span class="sxs-lookup"><span data-stu-id="7d2d2-168">Get security updates for our products</span></span>
<span data-ttu-id="7d2d2-169">[이 페이지](https://technet.microsoft.com/security/dd252948) 를 방문해서 보안 공지 경고를 구독하여 보안 사건이 발생할 때 알림을 받는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7d2d2-169">We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>


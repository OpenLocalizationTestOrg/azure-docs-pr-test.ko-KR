---
title: "AD aaaAzure v2.0.NET 웹 앱을 시작 하는 데 로그인 | Microsoft Docs"
description: "어떻게 toobuild.NET MVC 웹 응용 프로그램 하는 로그인 사용자 두 개인 Microsoft 계정으로 하 고 회사 또는 학교 계정."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: c8b97ac6-0a06-4367-81b6-7d1d98152b14
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 241e9c90bd752fbecc3696ce4f1bed3f9772189d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooan-net-mvc-web-app"></a><span data-ttu-id="9b827-103">로그인 tooan.NET MVC 웹 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="9b827-103">Add sign-in tooan .NET MVC web app</span></span>
<span data-ttu-id="9b827-104">Hello v2.0 끝점과 두 개인 Microsoft 계정에 대 한 지원 및 회사 또는 학교 계정으로 인증 tooyour 웹 앱을 신속 하 게 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b827-104">With hello v2.0 endpoint, you can quickly add authentication tooyour web apps with support for both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="9b827-105">Asp.NET 웹앱에서는 .NET Framework 4.5에 포함된 Microsoft OWIN 미들웨어를 사용하여 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b827-105">In ASP.NET web apps, you can accomplish this using Microsoft's OWIN middleware included in .NET Framework 4.5.</span></span>

> [!NOTE]
> <span data-ttu-id="9b827-106">모든 Azure Active Directory 시나리오 및 기능 hello v2.0 끝점에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b827-106">Not all Azure Active Directory scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="9b827-107">에 대해 알아보세요 hello v2.0 끝점을 사용 해야 하는 경우 toodetermine [v2.0 제한](active-directory-v2-limitations.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9b827-107">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
>
>

 <span data-ttu-id="9b827-108">여기 빌드합니다 OWIN toosign hello 사용자 표시에 사용 하는 웹 앱 hello 사용자에 대 한 정보 및 기호 hello hello 앱에서 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="9b827-108">Here we'll build an web app that uses OWIN toosign hello user in, display some information about hello user, and sign hello user out of hello app.</span></span>

## <a name="download"></a><span data-ttu-id="9b827-109">다운로드</span><span class="sxs-lookup"><span data-stu-id="9b827-109">Download</span></span>
<span data-ttu-id="9b827-110">이 자습서에 대 한 hello 코드 유지 관리 [GitHub에서](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet)합니다.</span><span class="sxs-lookup"><span data-stu-id="9b827-110">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet).</span></span>  <span data-ttu-id="9b827-111">수에 따라 toofollow, [.zip으로 hello 응용 프로그램의 기본 정의 다운로드](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) 또는 복제 hello 스 켈 레 톤:</span><span class="sxs-lookup"><span data-stu-id="9b827-111">toofollow along, you can [download hello app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) or clone hello skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet.git```

<span data-ttu-id="9b827-112">완료 하는 hello 앱도이 자습서의 hello 끝에 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b827-112">hello completed app is provided at hello end of this tutorial as well.</span></span>

## <a name="register-an-app"></a><span data-ttu-id="9b827-113">앱 등록</span><span class="sxs-lookup"><span data-stu-id="9b827-113">Register an app</span></span>
<span data-ttu-id="9b827-114">[apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)에서 새 앱을 만들거나 다음 [세부 단계](active-directory-v2-app-registration.md)를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="9b827-114">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="9b827-115">다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b827-115">Make sure to:</span></span>

* <span data-ttu-id="9b827-116">Hello 아래로 복사 **응용 프로그램 Id** tooyour 응용 프로그램에 할당 해야 곧 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b827-116">Copy down hello **Application Id** assigned tooyour app, you'll need it soon.</span></span>
* <span data-ttu-id="9b827-117">Hello 추가 **웹** 응용 프로그램을 위한 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="9b827-117">Add hello **Web** platform for your app.</span></span>
* <span data-ttu-id="9b827-118">올바른 hello 입력 **리디렉션 URI**합니다.</span><span class="sxs-lookup"><span data-stu-id="9b827-118">Enter hello correct **Redirect URI**.</span></span> <span data-ttu-id="9b827-119">hello 리디렉션 uri 나타냅니다 tooAzure AD에 인증 응답 디렉션할-hello 기본적으로이 자습서는 `https://localhost:44326/`합니다.</span><span class="sxs-lookup"><span data-stu-id="9b827-119">hello redirect uri indicates tooAzure AD where authentication responses should be directed - hello default for this tutorial is `https://localhost:44326/`.</span></span>

## <a name="install--configure-owin-authentication"></a><span data-ttu-id="9b827-120">OWIN 인증 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="9b827-120">Install & configure OWIN authentication</span></span>
<span data-ttu-id="9b827-121">여기서 hello OWIN 미들웨어 toouse hello OpenID Connect 인증 프로토콜을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b827-121">Here, we'll configure hello OWIN middleware toouse hello OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="9b827-122">OWIN tooissue 사용 되는 로그인 및 로그 아웃 요청, hello 사용자의 세션을 관리 되며 다른 작업 간에 hello 사용자에 대 한 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="9b827-122">OWIN will be used tooissue sign-in and sign-out requests, manage hello user's session, and get information about hello user, amongst other things.</span></span>

1. <span data-ttu-id="9b827-123">toobegin, 열기 hello `web.config` hello 프로젝트의 hello 루트에서 파일을 hello에 응용 프로그램의 구성 값을 입력 `<appSettings>` 섹션.</span><span class="sxs-lookup"><span data-stu-id="9b827-123">toobegin, open hello `web.config` file in hello root of hello project, and enter your app's configuration values in hello `<appSettings>` section.</span></span>

  * <span data-ttu-id="9b827-124">hello `ida:ClientId` 는 hello **응용 프로그램 Id** hello 등록 포털에서 tooyour 응용 프로그램을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b827-124">hello `ida:ClientId` is hello **Application Id** assigned tooyour app in hello registration portal.</span></span>
  * <span data-ttu-id="9b827-125">hello `ida:RedirectUri` 는 hello **리디렉션 Uri** hello 포털에 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b827-125">hello `ida:RedirectUri` is hello **Redirect Uri** you entered in hello portal.</span></span>

2. <span data-ttu-id="9b827-126">다음으로 hello 패키지 관리자 콘솔을 사용 하 여 hello OWIN 미들웨어 NuGet 패키지 toohello 프로젝트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b827-126">Next, add hello OWIN middleware NuGet packages toohello project using hello Package Manager Console.</span></span>

        ```
        PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
        PM> Install-Package Microsoft.Owin.Security.Cookies
        PM> Install-Package Microsoft.Owin.Host.SystemWeb
        ```  

3. <span data-ttu-id="9b827-127">"OWIN 시작 클래스" toohello 프로젝트 라는 추가 `Startup.cs` hello 프로젝트 클릭--> 오른쪽 **추가** --> **새 항목** "OWIN"에 대 한 검색--> 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b827-127">Add an "OWIN Startup Class" toohello project called `Startup.cs`  Right click on hello project --> **Add** --> **New Item** --> Search for "OWIN".</span></span>  <span data-ttu-id="9b827-128">hello OWIN 미들웨어는 hello를 호출 하는 `Configuration(...)` 메서드 앱이 시작 되는 경우.</span><span class="sxs-lookup"><span data-stu-id="9b827-128">hello OWIN middleware will invoke hello `Configuration(...)` method when your app starts.</span></span>
4. <span data-ttu-id="9b827-129">Hello 클래스 선언에도 변경`public partial class Startup` -이미 구현 했습니다이 클래스의 일부를 다른 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b827-129">Change hello class declaration too`public partial class Startup` - we've already implemented part of this class for you in another file.</span></span>  <span data-ttu-id="9b827-130">Hello에 `Configuration(...)` 메서드를 웹 앱에 대 한 인증을 호출 tooConfigureAuth(...) tooset 확인</span><span class="sxs-lookup"><span data-stu-id="9b827-130">In hello `Configuration(...)` method, make a call tooConfigureAuth(...) tooset up authentication for your web app</span></span>  

        ```C#
        [assembly: OwinStartup(typeof(Startup))]
        
        namespace TodoList_WebApp
        {
            public partial class Startup
            {
                public void Configuration(IAppBuilder app)
                {
                    ConfigureAuth(app);
                }
            }
        }
        ```

5. <span data-ttu-id="9b827-131">파일 열기 hello `App_Start\Startup.Auth.cs` hello를 구현 하 고 `ConfigureAuth(...)` 메서드.</span><span class="sxs-lookup"><span data-stu-id="9b827-131">Open hello file `App_Start\Startup.Auth.cs` and implement hello `ConfigureAuth(...)` method.</span></span>  <span data-ttu-id="9b827-132">매개 변수가 hello `OpenIdConnectAuthenticationOptions` 좌표 Azure AD와 앱 toocommunicate 프로그램에 대 한 역할을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b827-132">hello parameters you provide in `OpenIdConnectAuthenticationOptions` will serve as coordinates for your app toocommunicate with Azure AD.</span></span>  <span data-ttu-id="9b827-133">또한 tooset 쿠키 인증을 해야-hello OpenID Connect 미들웨어 hello 표지 아래 쿠키를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b827-133">You'll also need tooset up Cookie Authentication - hello OpenID Connect middleware uses cookies underneath hello covers.</span></span>

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
                                             Authority = String.Format(CultureInfo.InvariantCulture, aadInstance, "common", "/v2.0"),
                                             RedirectUri = redirectUri,
                                             Scope = "openid email profile",
                                             ResponseType = "id_token",
                                             PostLogoutRedirectUri = redirectUri,
                                             TokenValidationParameters = new TokenValidationParameters
                                             {
                                                     ValidateIssuer = false,
                                             },
                                             Notifications = new OpenIdConnectAuthenticationNotifications
                                             {
                                                     AuthenticationFailed = OnAuthenticationFailed,
                                             }
                                     });
                     }
        ```

## <a name="send-authentication-requests"></a><span data-ttu-id="9b827-134">인증 요청 보내기</span><span class="sxs-lookup"><span data-stu-id="9b827-134">Send authentication requests</span></span>
<span data-ttu-id="9b827-135">이제 앱이 올바르게 구성 된 toocommunicate hello OpenID Connect 인증 프로토콜을 사용 하 여 hello v2.0 끝점을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b827-135">Your app is now properly configured toocommunicate with hello v2.0 endpoint using hello OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="9b827-136">OWIN 모든 인증 메시지를 만들어, Azure AD에서 토큰의 유효성 검사 및 사용자 세션을 유지 관리의 hello 까다로운 세부 정보가 처리 했습니다.</span><span class="sxs-lookup"><span data-stu-id="9b827-136">OWIN has taken care of all of hello ugly details of crafting authentication messages, validating tokens from Azure AD, and maintaining user session.</span></span>  <span data-ttu-id="9b827-137">나머지 작업은 toogive 사용자의 방식으로 toosign 및 로그 아웃 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b827-137">All that remains is toogive your users a way toosign in and sign out.</span></span>

- <span data-ttu-id="9b827-138">사용할 수 있습니다 태그에 권한을 부여 컨트롤러 toorequire에 사용자가 로그인 특정 페이지에 액세스 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="9b827-138">You can use authorize tags in your controllers toorequire that user signs in before accessing a certain page.</span></span>  <span data-ttu-id="9b827-139">열기 `Controllers\HomeController.cs`, hello 추가 `[Authorize]` toohello 컨트롤러에 대 한 태그를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b827-139">Open `Controllers\HomeController.cs`, and add hello `[Authorize]` tag toohello About controller.</span></span>
        
        ```C#
        [Authorize]
        public ActionResult About()
        {
          ...
        ```

- <span data-ttu-id="9b827-140">OWIN toodirectly 문제에서 오는 인증 요청이 코드 내에서 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b827-140">You can also use OWIN toodirectly issue authentication requests from within your code.</span></span>  <span data-ttu-id="9b827-141">`Controllers\AccountController.cs`을(를) 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9b827-141">Open `Controllers\AccountController.cs`.</span></span>  <span data-ttu-id="9b827-142">SignIn() hello 및 SignOut() 동작에 각각 챌린지 OpenID Connect 및 로그 아웃 요청을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b827-142">In hello SignIn() and SignOut() actions, issue OpenID Connect challenge and sign-out requests, respectively.</span></span>

        ```C#
        public void SignIn()
        {
            // Send an OpenID Connect sign-in request.
            if (!Request.IsAuthenticated)
            {
                HttpContext.GetOwinContext().Authentication.Challenge(new AuthenticationProperties { RedirectUri = "/" }, OpenIdConnectAuthenticationDefaults.AuthenticationType);
            }
        }
        
        // BUGBUG: Ending a session with hello v2.0 endpoint is not yet supported.  Here, we just end hello session with hello web app.  
        public void SignOut()
        {
            // Send an OpenID Connect sign-out request.
            HttpContext.GetOwinContext().Authentication.SignOut(CookieAuthenticationDefaults.AuthenticationType);
            Response.Redirect("/");
        }
        ```

- <span data-ttu-id="9b827-143">이제 `Views\Shared\_LoginPartial.cshtml`을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9b827-143">Now, open `Views\Shared\_LoginPartial.cshtml`.</span></span>  <span data-ttu-id="9b827-144">이 hello 사용자 응용 프로그램의 로그인 및 로그 아웃 링크를 표시 하 고 뷰에서 hello 사용자의 이름을 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b827-144">This is where you'll show hello user your app's sign-in and sign-out links, and print out hello user's name in a view.</span></span>

        ```HTML
        @if (Request.IsAuthenticated)
        {
            <text>
                <ul class="nav navbar-nav navbar-right">
                    <li class="navbar-text">
        
                        @*hello 'preferred_username' claim can be used for showing hello user's primary way of identifying themselves.*@
        
                        Hello, @(System.Security.Claims.ClaimsPrincipal.Current.FindFirst("preferred_username").Value)!
                    </li>
                    <li>
                        @Html.ActionLink("Sign out", "SignOut", "Account")
                    </li>
                </ul>
            </text>
        }
        else
        {
            <ul class="nav navbar-nav navbar-right">
                <li>@Html.ActionLink("Sign in", "SignIn", "Account", routeValues: null, htmlAttributes: new { id = "loginLink" })</li>
            </ul>
        }
        ```

## <a name="display-user-information"></a><span data-ttu-id="9b827-145">사용자 정보 표시</span><span class="sxs-lookup"><span data-stu-id="9b827-145">Display user information</span></span>
<span data-ttu-id="9b827-146">OpenID Connect와 사용자를 인증할 때 hello v2.0 끝점 hello 사용자에 대 한 어설션 또는 클레임을 포함 하는 id_token toohello 응용 프로그램을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b827-146">When authenticating users with OpenID Connect, hello v2.0 endpoint returns an id_token toohello app that contains claims, or assertions about hello user.</span></span>  <span data-ttu-id="9b827-147">이러한 클레임 toopersonalize 앱을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b827-147">You can use these claims toopersonalize your app:</span></span>

- <span data-ttu-id="9b827-148">열기 hello `Controllers\HomeController.cs` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="9b827-148">Open hello `Controllers\HomeController.cs` file.</span></span>  <span data-ttu-id="9b827-149">Hello 사용자의 클레임 hello 통해 컨트롤러에 액세스할 수 있습니다 `ClaimsPrincipal.Current` 보안 주체 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="9b827-149">You can access hello user's claims in your controllers via hello `ClaimsPrincipal.Current` security principal object.</span></span>

        ```C#
        [Authorize]
        public ActionResult About()
        {
            ViewBag.Name = ClaimsPrincipal.Current.FindFirst("name").Value;
        
            // hello object ID claim will only be emitted for work or school accounts at this time.
            Claim oid = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier");
            ViewBag.ObjectId = oid == null ? string.Empty : oid.Value;
        
            // hello 'preferred_username' claim can be used for showing hello user's primary way of identifying themselves
            ViewBag.Username = ClaimsPrincipal.Current.FindFirst("preferred_username").Value;
        
            // hello subject or nameidentifier claim can be used toouniquely identify hello user
            ViewBag.Subject = ClaimsPrincipal.Current.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
        
            return View();
        }
        ```

## <a name="run"></a><span data-ttu-id="9b827-150">실행</span><span class="sxs-lookup"><span data-stu-id="9b827-150">Run</span></span>
<span data-ttu-id="9b827-151">마지막으로 앱을 빌드하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9b827-151">Finally, build and run your app!</span></span>   <span data-ttu-id="9b827-152">개인 Microsoft 계정 또는 회사 또는 학교 계정으로 로그인 하 고 hello 사용자의 id hello 위쪽 탐색 모음에 어떻게 반영 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b827-152">Sign in with either a personal Microsoft Account or a work or school account, and notice how hello user's identity is reflected in hello top navigation bar.</span></span>  <span data-ttu-id="9b827-153">이제 개인 및 회사/학교 계정으로 사용자를 인증할 수 있는 업계 표준 프로토콜을 사용하여 웹앱이 보안되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9b827-153">You now have a web app secured using industry standard protocols that can authenticate users with both their personal and work/school accounts.</span></span>

<span data-ttu-id="9b827-154">참조용으로 hello 구성 값) (없이 샘플을 완료 [.zip을 여기로 제공 됩니다](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/complete.zip), 또는 GitHub에서 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b827-154">For reference, hello completed sample (without your configuration values) [is provided as a .zip here](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet.git```

## <a name="next-steps"></a><span data-ttu-id="9b827-155">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9b827-155">Next steps</span></span>
<span data-ttu-id="9b827-156">이제 좀 더 고급 항목으로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b827-156">You can now move onto more advanced topics.</span></span>  <span data-ttu-id="9b827-157">Tootry를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b827-157">You may want tootry:</span></span>

[<span data-ttu-id="9b827-158">Hello hello v2.0 끝점과 웹 API 보안 >></span><span class="sxs-lookup"><span data-stu-id="9b827-158">Secure a Web API with hello hello v2.0 endpoint >></span></span>](active-directory-devquickstarts-webapi-dotnet.md)

<span data-ttu-id="9b827-159">추가 리소스는 다음을 확인해보세요.</span><span class="sxs-lookup"><span data-stu-id="9b827-159">For additional resources, check out:</span></span>

* [<span data-ttu-id="9b827-160">hello v2.0 개발자 가이드 >></span><span class="sxs-lookup"><span data-stu-id="9b827-160">hello v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="9b827-161">StackOverflow "azure-active-directory" 태그 >></span><span class="sxs-lookup"><span data-stu-id="9b827-161">StackOverflow "azure-active-directory" tag >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="9b827-162">당사 제품에 대한 보안 업데이트 가져오기</span><span class="sxs-lookup"><span data-stu-id="9b827-162">Get security updates for our products</span></span>
<span data-ttu-id="9b827-163">보안 사고를 방문 하 여 발생 하는 경우의 알림 tooget 좋습니다 [이 페이지](https://technet.microsoft.com/security/dd252948) 및 tooSecurity 자문 경고를 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b827-163">We encourage you tooget notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>

---
title: "Azure AD v2.0 .NET 웹앱 로그인 시작하기 | Microsoft Docs"
description: "개인 Microsoft 계정과 회사 또는 학교 계정 둘 다로 사용자를 로그인하는 .NET MVC Web 웹앱을 빌드하는 방법입니다."
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
ms.openlocfilehash: ba5bdf7daba6086b70aec54ebe25d4445fa708c3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-to-an-net-mvc-web-app"></a><span data-ttu-id="9cc65-103">.NET MVC 웹앱에 로그인 추가</span><span class="sxs-lookup"><span data-stu-id="9cc65-103">Add sign-in to an .NET MVC web app</span></span>
<span data-ttu-id="9cc65-104">v2.0 끝점을 사용하면 개인 Microsoft 계정과 회사 또는 학교 계정 둘 다를 지원하는 인증을 웹앱에 빠르게 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc65-104">With the v2.0 endpoint, you can quickly add authentication to your web apps with support for both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="9cc65-105">Asp.NET 웹앱에서는 .NET Framework 4.5에 포함된 Microsoft OWIN 미들웨어를 사용하여 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc65-105">In ASP.NET web apps, you can accomplish this using Microsoft's OWIN middleware included in .NET Framework 4.5.</span></span>

> [!NOTE]
> <span data-ttu-id="9cc65-106">일부 Azure Active Directory 시나리오 및 기능만 v2.0 끝점에서 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc65-106">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="9cc65-107">v2.0 끝점을 사용해야 하는지 확인하려면 [v2.0 제한 사항](active-directory-v2-limitations.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9cc65-107">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
>
>

 <span data-ttu-id="9cc65-108">여기서는 OWIN을 사용하여 사용자를 로그인하고, 사용자에 관한 일부 정보를 표시하고, 사용자를 앱에서 로그아웃하는 웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9cc65-108">Here we'll build an web app that uses OWIN to sign the user in, display some information about the user, and sign the user out of the app.</span></span>

## <a name="download"></a><span data-ttu-id="9cc65-109">다운로드</span><span class="sxs-lookup"><span data-stu-id="9cc65-109">Download</span></span>
<span data-ttu-id="9cc65-110">이 자습서에 대한 코드는 [GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet)에서 유지 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cc65-110">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet).</span></span>  <span data-ttu-id="9cc65-111">자습서에 따라 [.zip으로 앱 구조를 다운로드](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) 하거나 구조를 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc65-111">To follow along, you can [download the app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) or clone the skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet.git```

<span data-ttu-id="9cc65-112">전체 앱은 이 자습서 마지막 부분에서도 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cc65-112">The completed app is provided at the end of this tutorial as well.</span></span>

## <a name="register-an-app"></a><span data-ttu-id="9cc65-113">앱 등록</span><span class="sxs-lookup"><span data-stu-id="9cc65-113">Register an app</span></span>
<span data-ttu-id="9cc65-114">[apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)에서 새 앱을 만들거나 다음 [세부 단계](active-directory-v2-app-registration.md)를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="9cc65-114">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="9cc65-115">다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc65-115">Make sure to:</span></span>

* <span data-ttu-id="9cc65-116">곧 필요하게 되므로 앱에 할당된 **응용 프로그램 ID** 를 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="9cc65-116">Copy down the **Application Id** assigned to your app, you'll need it soon.</span></span>
* <span data-ttu-id="9cc65-117">앱에 대한 **웹** 플랫폼을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc65-117">Add the **Web** platform for your app.</span></span>
* <span data-ttu-id="9cc65-118">올바른 **리디렉션 URI**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc65-118">Enter the correct **Redirect URI**.</span></span> <span data-ttu-id="9cc65-119">리디렉션 URI는 인증 응답을 보내야 하는 Azure AD를 나타냅니다. 이 자습서에 대한 기본값은 `https://localhost:44326/`입니다.</span><span class="sxs-lookup"><span data-stu-id="9cc65-119">The redirect uri indicates to Azure AD where authentication responses should be directed - the default for this tutorial is `https://localhost:44326/`.</span></span>

## <a name="install--configure-owin-authentication"></a><span data-ttu-id="9cc65-120">OWIN 인증 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="9cc65-120">Install & configure OWIN authentication</span></span>
<span data-ttu-id="9cc65-121">여기서는 OpenID Connect 인증 프로토콜을 사용하도록 OWIN 미들웨어를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc65-121">Here, we'll configure the OWIN middleware to use the OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="9cc65-122">OWIN은 로그인 및 로그아웃 요청을 실행하고, 사용자의 세션을 관리하고, 사용자에 대한 정보를 가져오는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cc65-122">OWIN will be used to issue sign-in and sign-out requests, manage the user's session, and get information about the user, amongst other things.</span></span>

1. <span data-ttu-id="9cc65-123">먼저 프로젝트의 루트에서 `web.config` 파일을 열고 `<appSettings>` 섹션에 앱의 구성 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc65-123">To begin, open the `web.config` file in the root of the project, and enter your app's configuration values in the `<appSettings>` section.</span></span>

  * <span data-ttu-id="9cc65-124">`ida:ClientId` 는 등록 포털에서 앱에 할당된 **응용 프로그램 ID** 입니다.</span><span class="sxs-lookup"><span data-stu-id="9cc65-124">The `ida:ClientId` is the **Application Id** assigned to your app in the registration portal.</span></span>
  * <span data-ttu-id="9cc65-125">`ida:RedirectUri` 은(는) 포털에서 입력한 **리디렉션 URI** 입니다.</span><span class="sxs-lookup"><span data-stu-id="9cc65-125">The `ida:RedirectUri` is the **Redirect Uri** you entered in the portal.</span></span>

2. <span data-ttu-id="9cc65-126">그 다음, 패키지 관리자 콘솔을 사용하여 OWIN 미들웨어 NuGet 패키지를 프로젝트에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc65-126">Next, add the OWIN middleware NuGet packages to the project using the Package Manager Console.</span></span>

        ```
        PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
        PM> Install-Package Microsoft.Owin.Security.Cookies
        PM> Install-Package Microsoft.Owin.Host.SystemWeb
        ```  

3. <span data-ttu-id="9cc65-127">`Startup.cs` 프로젝트에 "OWIN Startup 클래스"를 추가하고, 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가** --> **새 항목** --> "OWIN" 검색을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc65-127">Add an "OWIN Startup Class" to the project called `Startup.cs`  Right click on the project --> **Add** --> **New Item** --> Search for "OWIN".</span></span>  <span data-ttu-id="9cc65-128">OWIN 미들웨어는 앱이 시작되면 `Configuration(...)` 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc65-128">The OWIN middleware will invoke the `Configuration(...)` method when your app starts.</span></span>
4. <span data-ttu-id="9cc65-129">클래스 선언을 이미 다른 파일에서 이 클래스의 일부를 구현했던 `public partial class Startup` 으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc65-129">Change the class declaration to `public partial class Startup` - we've already implemented part of this class for you in another file.</span></span>  <span data-ttu-id="9cc65-130">`Configuration(...)` 메서드에서 ConfigureAuth(...)를 호출하여 웹앱에 대한 인증을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc65-130">In the `Configuration(...)` method, make a call to ConfigureAuth(...) to set up authentication for your web app</span></span>  

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

5. <span data-ttu-id="9cc65-131">`App_Start\Startup.Auth.cs` 파일을 열고 `ConfigureAuth(...)` 메서드를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc65-131">Open the file `App_Start\Startup.Auth.cs` and implement the `ConfigureAuth(...)` method.</span></span>  <span data-ttu-id="9cc65-132">`OpenIdConnectAuthenticationOptions` 에 제공하는 매개 변수는 앱이 Azure AD와 통신하기 위한 좌표로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cc65-132">The parameters you provide in `OpenIdConnectAuthenticationOptions` will serve as coordinates for your app to communicate with Azure AD.</span></span>  <span data-ttu-id="9cc65-133">보이지 않지만 OpenID Connect 미들웨어는 쿠키를 사용하므로 쿠키 인증도 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc65-133">You'll also need to set up Cookie Authentication - the OpenID Connect middleware uses cookies underneath the covers.</span></span>

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

## <a name="send-authentication-requests"></a><span data-ttu-id="9cc65-134">인증 요청 보내기</span><span class="sxs-lookup"><span data-stu-id="9cc65-134">Send authentication requests</span></span>
<span data-ttu-id="9cc65-135">이제 앱이 OpenID Connect 인증 프로토콜을 사용하여 v2.0 끝점 끝점과 통신하도록 올바르게 구성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc65-135">Your app is now properly configured to communicate with the v2.0 endpoint using the OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="9cc65-136">OWIN이 인증 메시지를 작성하고, Azure AD에서 토큰의 유효성을 검사하고, 사용자 세션을 유지 관리하는 까다로운 모든 세부 과정을 처리했습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc65-136">OWIN has taken care of all of the ugly details of crafting authentication messages, validating tokens from Azure AD, and maintaining user session.</span></span>  <span data-ttu-id="9cc65-137">이제 사용자에게 로그인하고 로그아웃하는 방법을 알려주기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cc65-137">All that remains is to give your users a way to sign in and sign out.</span></span>

- <span data-ttu-id="9cc65-138">컨트롤러에서 권한 부여 태그를 사용하여 사용자가 특정 페이지에 액세스하기 전에 로그인하도록 요구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc65-138">You can use authorize tags in your controllers to require that user signs in before accessing a certain page.</span></span>  <span data-ttu-id="9cc65-139">`Controllers\HomeController.cs`를 열고 About 컨트롤러에 `[Authorize]` 태그를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc65-139">Open `Controllers\HomeController.cs`, and add the `[Authorize]` tag to the About controller.</span></span>
        
        ```C#
        [Authorize]
        public ActionResult About()
        {
          ...
        ```

- <span data-ttu-id="9cc65-140">또한 OWIN을 사용하여 코드 내에서 직접 인증 요청을 실행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc65-140">You can also use OWIN to directly issue authentication requests from within your code.</span></span>  <span data-ttu-id="9cc65-141">`Controllers\AccountController.cs`을(를) 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9cc65-141">Open `Controllers\AccountController.cs`.</span></span>  <span data-ttu-id="9cc65-142">SignIn() 및 SignOut() 작업에서 각각 OpenID Connect 챌린지 및 로그아웃 요청을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc65-142">In the SignIn() and SignOut() actions, issue OpenID Connect challenge and sign-out requests, respectively.</span></span>

        ```C#
        public void SignIn()
        {
            // Send an OpenID Connect sign-in request.
            if (!Request.IsAuthenticated)
            {
                HttpContext.GetOwinContext().Authentication.Challenge(new AuthenticationProperties { RedirectUri = "/" }, OpenIdConnectAuthenticationDefaults.AuthenticationType);
            }
        }
        
        // BUGBUG: Ending a session with the v2.0 endpoint is not yet supported.  Here, we just end the session with the web app.  
        public void SignOut()
        {
            // Send an OpenID Connect sign-out request.
            HttpContext.GetOwinContext().Authentication.SignOut(CookieAuthenticationDefaults.AuthenticationType);
            Response.Redirect("/");
        }
        ```

- <span data-ttu-id="9cc65-143">이제 `Views\Shared\_LoginPartial.cshtml`을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9cc65-143">Now, open `Views\Shared\_LoginPartial.cshtml`.</span></span>  <span data-ttu-id="9cc65-144">여기서 사용자에게 앱 로그인 및 로그아웃 링크를 표시하고 보기에 사용자 이름을 출력하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cc65-144">This is where you'll show the user your app's sign-in and sign-out links, and print out the user's name in a view.</span></span>

        ```HTML
        @if (Request.IsAuthenticated)
        {
            <text>
                <ul class="nav navbar-nav navbar-right">
                    <li class="navbar-text">
        
                        @*The 'preferred_username' claim can be used for showing the user's primary way of identifying themselves.*@
        
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

## <a name="display-user-information"></a><span data-ttu-id="9cc65-145">사용자 정보 표시</span><span class="sxs-lookup"><span data-stu-id="9cc65-145">Display user information</span></span>
<span data-ttu-id="9cc65-146">OpenID Connect로 사용자를 인증할 때 v2.0 끝점은 클레임 또는 사용자에 대한 어설션을 포함하는 id_token을 앱에 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc65-146">When authenticating users with OpenID Connect, the v2.0 endpoint returns an id_token to the app that contains claims, or assertions about the user.</span></span>  <span data-ttu-id="9cc65-147">이러한 클레임을 사용하여 앱 개인 설정을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc65-147">You can use these claims to personalize your app:</span></span>

- <span data-ttu-id="9cc65-148">`Controllers\HomeController.cs` 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9cc65-148">Open the `Controllers\HomeController.cs` file.</span></span>  <span data-ttu-id="9cc65-149">`ClaimsPrincipal.Current` 보안 주체 개체를 통해 컨트롤러의 사용자 클레임에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc65-149">You can access the user's claims in your controllers via the `ClaimsPrincipal.Current` security principal object.</span></span>

        ```C#
        [Authorize]
        public ActionResult About()
        {
            ViewBag.Name = ClaimsPrincipal.Current.FindFirst("name").Value;
        
            // The object ID claim will only be emitted for work or school accounts at this time.
            Claim oid = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier");
            ViewBag.ObjectId = oid == null ? string.Empty : oid.Value;
        
            // The 'preferred_username' claim can be used for showing the user's primary way of identifying themselves
            ViewBag.Username = ClaimsPrincipal.Current.FindFirst("preferred_username").Value;
        
            // The subject or nameidentifier claim can be used to uniquely identify the user
            ViewBag.Subject = ClaimsPrincipal.Current.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
        
            return View();
        }
        ```

## <a name="run"></a><span data-ttu-id="9cc65-150">실행</span><span class="sxs-lookup"><span data-stu-id="9cc65-150">Run</span></span>
<span data-ttu-id="9cc65-151">마지막으로 앱을 빌드하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc65-151">Finally, build and run your app!</span></span>   <span data-ttu-id="9cc65-152">개인 Microsoft 계정이나 회사 또는 학교 계정으로 로그인하고 위쪽 탐색 모음에 사용자 ID가 반영되는 방식을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc65-152">Sign in with either a personal Microsoft Account or a work or school account, and notice how the user's identity is reflected in the top navigation bar.</span></span>  <span data-ttu-id="9cc65-153">이제 개인 및 회사/학교 계정으로 사용자를 인증할 수 있는 업계 표준 프로토콜을 사용하여 웹앱이 보안되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc65-153">You now have a web app secured using industry standard protocols that can authenticate users with both their personal and work/school accounts.</span></span>

<span data-ttu-id="9cc65-154">참조를 위해 완료된 샘플(사용자 구성 값 제외)이 [여기에 .zip으로 제공](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/complete.zip)되거나 GitHub에서 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc65-154">For reference, the completed sample (without your configuration values) [is provided as a .zip here](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet.git```

## <a name="next-steps"></a><span data-ttu-id="9cc65-155">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9cc65-155">Next steps</span></span>
<span data-ttu-id="9cc65-156">이제 좀 더 고급 항목으로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc65-156">You can now move onto more advanced topics.</span></span>  <span data-ttu-id="9cc65-157">다음 작업을 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc65-157">You may want to try:</span></span>

[<span data-ttu-id="9cc65-158">v2.0 끝점을 사용하여 웹 API 보안 유지>></span><span class="sxs-lookup"><span data-stu-id="9cc65-158">Secure a Web API with the the v2.0 endpoint >></span></span>](active-directory-devquickstarts-webapi-dotnet.md)

<span data-ttu-id="9cc65-159">추가 리소스는 다음을 확인해보세요.</span><span class="sxs-lookup"><span data-stu-id="9cc65-159">For additional resources, check out:</span></span>

* [<span data-ttu-id="9cc65-160">개발자 가이드 v2.0 >></span><span class="sxs-lookup"><span data-stu-id="9cc65-160">The v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="9cc65-161">StackOverflow "azure-active-directory" 태그 >></span><span class="sxs-lookup"><span data-stu-id="9cc65-161">StackOverflow "azure-active-directory" tag >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="9cc65-162">당사 제품에 대한 보안 업데이트 가져오기</span><span class="sxs-lookup"><span data-stu-id="9cc65-162">Get security updates for our products</span></span>
<span data-ttu-id="9cc65-163">[이 페이지](https://technet.microsoft.com/security/dd252948) 를 방문해서 보안 공지 경고를 구독하여 보안 사건이 발생할 때 알림을 받는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc65-163">We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>

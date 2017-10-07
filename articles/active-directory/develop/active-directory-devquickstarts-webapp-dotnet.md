---
title: "AD aaaAzure.NET 웹 응용 프로그램 시작 | Microsoft Docs"
description: "로그인을 위해 Azure AD와 통합되는 .NET MVC 웹앱을 빌드합니다."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: e15a41a4-dc5d-4c90-b3fe-5dc33b9a1e96
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 6d3098c9e3d7e1916ccb110c703f501ae52e788f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="aspnet-web-app-sign-in-and-sign-out-with-azure-ad"></a><span data-ttu-id="4c1df-103">Azure AD에서 ASP.NET 웹앱 로그인 및 로그아웃</span><span class="sxs-lookup"><span data-stu-id="4c1df-103">ASP.NET web app sign-in and sign-out with Azure AD</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="4c1df-104">로그인 및 로그 아웃 하는 단일 단 몇 줄의 코드를 제공 함으로써 Azure Active Directory (Azure AD) 간단 하 게 하면 toooutsource 웹 응용 프로그램 id 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1df-104">By providing a single sign-in and sign-out with only a few lines of code, Azure Active Directory (Azure AD) makes it simple for you toooutsource web-app identity management.</span></span> <span data-ttu-id="4c1df-105">.NET (OWIN) 미들웨어에 대 한 Open Web Interface의 Microsoft 구현 hello를 사용 하 여 ASP.NET 웹 응용 프로그램 내부 및 외부 사용자가 서명할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c1df-105">You can sign users in and out of ASP.NET web apps by using hello Microsoft implementation of Open Web Interface for .NET (OWIN) middleware.</span></span> <span data-ttu-id="4c1df-106">커뮤니티 기반 OWIN 미들웨어는 .NET Framework 4.5에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c1df-106">Community-driven OWIN middleware is included in .NET Framework 4.5.</span></span> <span data-ttu-id="4c1df-107">이 문서에서는 어떻게 toouse OWIN에:</span><span class="sxs-lookup"><span data-stu-id="4c1df-107">This article shows how toouse OWIN to:</span></span>

* <span data-ttu-id="4c1df-108">Hello id 공급자로 Azure AD를 사용 하 여 tooweb 앱에서 사용자를 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1df-108">Sign users in tooweb apps by using Azure AD as hello identity provider.</span></span>
* <span data-ttu-id="4c1df-109">일부 사용자 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1df-109">Display some user information.</span></span>
* <span data-ttu-id="4c1df-110">Hello 앱에서 사용자를 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1df-110">Sign users out of hello apps.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="4c1df-111">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="4c1df-111">Before you get started</span></span>
* <span data-ttu-id="4c1df-112">Hello 다운로드 [앱 스 켈 레 톤](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) hello 다운로드 또는 [완성 된 샘플](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip)합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1df-112">Download hello [app skeleton](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) or download hello [completed sample](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip).</span></span>
* <span data-ttu-id="4c1df-113">어떤 tooregister hello 앱에서 Azure AD 테 넌 트가 있어야합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1df-113">You also need an Azure AD tenant in which tooregister hello app.</span></span> <span data-ttu-id="4c1df-114">Azure AD 테 넌 트가 아직 없는 경우 [자세한 방법을 하나 tooget](active-directory-howto-tenant.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1df-114">If you don't already have an Azure AD tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="4c1df-115">준비 되 면 다음 절차에 따라 hello hello 다음 네 개의 절.</span><span class="sxs-lookup"><span data-stu-id="4c1df-115">When you are ready, follow hello procedures in hello next four sections.</span></span>

## <a name="step-1-register-hello-new-app-with-azure-ad"></a><span data-ttu-id="4c1df-116">1 단계: Azure AD와 hello 새 앱 등록</span><span class="sxs-lookup"><span data-stu-id="4c1df-116">Step 1: Register hello new app with Azure AD</span></span>
<span data-ttu-id="4c1df-117">tooset hello 앱 tooauthenticate 사용자를 처음 등록할 테 넌 트에 hello 다음을 수행 하 여:</span><span class="sxs-lookup"><span data-stu-id="4c1df-117">tooset up hello app tooauthenticate users, first register it in your tenant by doing hello following:</span></span>

1. <span data-ttu-id="4c1df-118">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1df-118">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="4c1df-119">Hello 위쪽 막대에서 계정 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1df-119">On hello top bar, click your account name.</span></span> <span data-ttu-id="4c1df-120">Hello에서 **디렉터리** 목록, 선택 hello Active Directory 테 넌 트 tooregister hello 앱을 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1df-120">Under hello **Directory** list, select hello Active Directory tenant where you want tooregister hello app.</span></span>
3. <span data-ttu-id="4c1df-121">클릭 **더 서비스** 에 hello 왼쪽된 창에서 선택한 후 **Azure Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1df-121">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="4c1df-122">**앱 등록**을 클릭하고 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1df-122">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="4c1df-123">에 따라 hello에서 묻는 메시지를 표시 하는 새 toocreate **웹 응용 프로그램 및/또는 WebAPI**합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1df-123">Follow hello prompts toocreate a new **Web Application and/or WebAPI**.</span></span>
  * <span data-ttu-id="4c1df-124">**이름** hello 앱 toousers에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1df-124">**Name** describes hello app toousers.</span></span>
  * <span data-ttu-id="4c1df-125">**로그온 URL** hello hello 응용 프로그램의 기본 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="4c1df-125">**Sign-On URL** is hello base URL of hello app.</span></span> <span data-ttu-id="4c1df-126">hello 뼈대 기본 URL은 https://localhost:44320 / 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1df-126">hello skeleton's default URL is https://localhost:44320/.</span></span>
6. <span data-ttu-id="4c1df-127">Azure AD를 hello 등록을 완료 한 후 hello 앱 고유한 응용 프로그램 ID를 할당</span><span class="sxs-lookup"><span data-stu-id="4c1df-127">After you've completed hello registration, Azure AD assigns hello app a unique application ID.</span></span> <span data-ttu-id="4c1df-128">Hello 다음 섹션의 앱 페이지 toouse hello에서에서 hello 값을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1df-128">Copy hello value from hello app page toouse in hello next sections.</span></span>
7. <span data-ttu-id="4c1df-129">Hello에서 **설정** -> **속성** 응용 프로그램에 대 한 페이지를 hello 앱 ID URI를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1df-129">From hello **Settings** -> **Properties** page for your application, update hello App ID URI.</span></span> <span data-ttu-id="4c1df-130">hello **앱 ID URI** hello 앱에 대 한 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="4c1df-130">hello **App ID URI** is a unique identifier for hello app.</span></span> <span data-ttu-id="4c1df-131">hello 명명 규칙은 `https://<tenant-domain>/<app-name>` (예를 들어 `https://contoso.onmicrosoft.com/my-first-aad-app`).</span><span class="sxs-lookup"><span data-stu-id="4c1df-131">hello naming convention is `https://<tenant-domain>/<app-name>` (for example, `https://contoso.onmicrosoft.com/my-first-aad-app`).</span></span>

## <a name="step-2-set-up-hello-app-toouse-hello-owin-authentication-pipeline"></a><span data-ttu-id="4c1df-132">2 단계: hello 앱 toouse hello OWIN 인증 파이프라인 설정</span><span class="sxs-lookup"><span data-stu-id="4c1df-132">Step 2: Set up hello app toouse hello OWIN authentication pipeline</span></span>
<span data-ttu-id="4c1df-133">이 단계에서는 hello OWIN 미들웨어 toouse hello OpenID Connect 인증 프로토콜을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1df-133">In this step, you configure hello OWIN middleware toouse hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="4c1df-134">OWIN tooissue 로그인 및 로그 아웃 요청을 사용 하 여, 관리 사용자 세션, 사용자 정보를 가져오기 하 등입니다.</span><span class="sxs-lookup"><span data-stu-id="4c1df-134">You use OWIN tooissue sign-in and sign-out requests, manage user sessions, get user information, and so forth.</span></span>

1. <span data-ttu-id="4c1df-135">toobegin, hello 패키지 관리자 콘솔을 사용 하 여 hello OWIN 미들웨어 NuGet 패키지 toohello 프로젝트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1df-135">toobegin, add hello OWIN middleware NuGet packages toohello project by using hello Package Manager Console.</span></span>

     ```
     PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
     PM> Install-Package Microsoft.Owin.Security.Cookies
     PM> Install-Package Microsoft.Owin.Host.SystemWeb
     ```

2. <span data-ttu-id="4c1df-136">OWIN 시작 클래스 toohello 프로젝트 라는 tooadd `Startup.cs`hello 프로젝트를 마우스 오른쪽 단추로 선택 **추가**선택, **새 항목**, 검색할 **OWIN**합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1df-136">tooadd an OWIN Startup class toohello project called `Startup.cs`, right-click hello project, select **Add**, select **New Item**, and then search for **OWIN**.</span></span> <span data-ttu-id="4c1df-137">hello를 호출 하는 OWIN 미들웨어입니다. hello **Configuration(...)**  hello 앱이 시작 될 때 메서드.</span><span class="sxs-lookup"><span data-stu-id="4c1df-137">hello OWIN middleware invokes hello **Configuration(...)** method when hello app starts.</span></span>
3. <span data-ttu-id="4c1df-138">Hello 클래스 선언에도 변경`public partial class Startup`합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1df-138">Change hello class declaration too`public partial class Startup`.</span></span> <span data-ttu-id="4c1df-139">다른 파일에서 이 클래스의 일부를 구현했습니다.</span><span class="sxs-lookup"><span data-stu-id="4c1df-139">We've already implemented part of this class for you in another file.</span></span> <span data-ttu-id="4c1df-140">Hello에 **Configuration(...)**  메서드를 너무 호출할**ConfgureAuth(...)**  tooset hello 앱에 대 한 인증을 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1df-140">In hello **Configuration(...)** method, make a call too**ConfgureAuth(...)** tooset up authentication for hello app.</span></span>  

     ```C#
     public partial class Startup
     {
         public void Configuration(IAppBuilder app)
         {
             ConfigureAuth(app);
         }
     }
     ```

4. <span data-ttu-id="4c1df-141">그런 다음 hello를 구현 하 고 hello App_Start\Startup.Auth.cs 파일을 열고 **ConfigureAuth(...)**  메서드.</span><span class="sxs-lookup"><span data-stu-id="4c1df-141">Open hello App_Start\Startup.Auth.cs file, and then implement hello **ConfigureAuth(...)** method.</span></span> <span data-ttu-id="4c1df-142">매개 변수가 hello *OpenIDConnectAuthenticationOptions* 역할을 Azure AD와 앱 toocommunicate hello에 대 한 좌표입니다.</span><span class="sxs-lookup"><span data-stu-id="4c1df-142">hello parameters you provide in *OpenIDConnectAuthenticationOptions* serve as coordinates for hello app toocommunicate with Azure AD.</span></span> <span data-ttu-id="4c1df-143">또한 필요 하면 tooset 쿠키 인증을 hello OpenID Connect 미들웨어 hello 백그라운드에서 쿠키를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1df-143">You also need tooset up cookie authentication, because hello OpenID Connect middleware uses cookies in hello background.</span></span>

     ```C#
     public void ConfigureAuth(IAppBuilder app)
     {
         app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

         app.UseCookieAuthentication(new CookieAuthenticationOptions());

         app.UseOpenIdConnectAuthentication(
             new OpenIdConnectAuthenticationOptions
             {
                 ClientId = clientId,
                 Authority = authority,
                 PostLogoutRedirectUri = postLogoutRedirectUri,
                 Notifications = new OpenIdConnectAuthenticationNotifications
                    {
                        AuthenticationFailed = context =>
                        {
                            context.HandleResponse();
                            context.Response.Redirect("/Error?message=" + context.Exception.Message);
                            return Task.FromResult(0);
                        }
                    }
             });
     }
     ```

5. <span data-ttu-id="4c1df-144">Hello 프로젝트의 hello 루트에서 hello web.config 파일을 연 다음 hello에 hello 구성 값을 입력 `<appSettings>` 섹션.</span><span class="sxs-lookup"><span data-stu-id="4c1df-144">Open hello web.config file in hello root of hello project, and then enter hello configuration values in hello `<appSettings>` section.</span></span>
  * <span data-ttu-id="4c1df-145">`ida:ClientId`: Azure 포털에서 hello에서 복사한 GUID hello "1 단계: Azure AD와 hello 새 앱 등록 합니다."</span><span class="sxs-lookup"><span data-stu-id="4c1df-145">`ida:ClientId`: hello GUID you copied from hello Azure portal in "Step 1: Register hello new app with Azure AD."</span></span>
  * <span data-ttu-id="4c1df-146">`ida:Tenant`: hello 이름에 Azure AD 테 넌 트 (예: contoso.onmicrosoft.com)입니다.</span><span class="sxs-lookup"><span data-stu-id="4c1df-146">`ida:Tenant`: hello name of your Azure AD tenant (for example, contoso.onmicrosoft.com).</span></span>
  * <span data-ttu-id="4c1df-147">`ida:PostLogoutRedirectUri`: 사용자 리디렉션해야 로그 아웃 요청을 성공적으로 완료 된 후에 Azure AD를 알려 주는 hello 표시기입니다.</span><span class="sxs-lookup"><span data-stu-id="4c1df-147">`ida:PostLogoutRedirectUri`: hello indicator that tells Azure AD where a user should be redirected after a sign-out request is successfully completed.</span></span>

## <a name="step-3-use-owin-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a><span data-ttu-id="4c1df-148">3 단계: 사용 tooAzure 광고를 요청 하는 OWIN tooissue 로그인 및 로그 아웃</span><span class="sxs-lookup"><span data-stu-id="4c1df-148">Step 3: Use OWIN tooissue sign-in and sign-out requests tooAzure AD</span></span>
<span data-ttu-id="4c1df-149">hello 이제 앱을 Azure AD와 올바르게 구성 된 toocommunicate hello OpenID Connect 인증 프로토콜을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1df-149">hello app is now properly configured toocommunicate with Azure AD by using hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="4c1df-150">OWIN 인증 메시지를 만들어, Azure AD에서 토큰의 유효성 검사 및 사용자 세션을 유지 관리의 hello 세부 정보를 모두 처리 했습니다.</span><span class="sxs-lookup"><span data-stu-id="4c1df-150">OWIN has handled all of hello details of crafting authentication messages, validating tokens from Azure AD, and maintaining user sessions.</span></span> <span data-ttu-id="4c1df-151">나머지 작업은 toogive 사용자의 방식으로 toosign 및 로그 아웃 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1df-151">All that remains is toogive your users a way toosign in and sign out.</span></span>

1. <span data-ttu-id="4c1df-152">에서는 특정 페이지를 액세스 하기 전에 태그에는 컨트롤러 toorequire 사용자 toosign에 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1df-152">You can use authorize tags in your controllers toorequire users toosign in before they access certain pages.</span></span> <span data-ttu-id="4c1df-153">toodo 따라서 Controllers\HomeController.cs를 열고 다음 추가 hello `[Authorize]` toohello 컨트롤러에 대 한 태그를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1df-153">toodo so, open Controllers\HomeController.cs, and then add hello `[Authorize]` tag toohello About controller.</span></span>

     ```C#
     [Authorize]
     public ActionResult About()
     {
       ...
     ```

2. <span data-ttu-id="4c1df-154">OWIN toodirectly 문제에서 오는 인증 요청이 코드 내에서 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c1df-154">You can also use OWIN toodirectly issue authentication requests from within your code.</span></span> <span data-ttu-id="4c1df-155">따라서 toodo Controllers\AccountController.cs를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4c1df-155">toodo so, open Controllers\AccountController.cs.</span></span> <span data-ttu-id="4c1df-156">그런 다음 hello SignIn() 및 SignOut() 작업의 OpenID Connect 챌린지 및 로그 아웃 요청을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1df-156">Then, in hello SignIn() and SignOut() actions, issue OpenID Connect challenge and sign-out requests.</span></span>

     ```C#
     public void SignIn()
     {
         // Send an OpenID Connect sign-in request.
         if (!Request.IsAuthenticated)
         {
             HttpContext.GetOwinContext().Authentication.Challenge(new AuthenticationProperties { RedirectUri = "/" }, OpenIdConnectAuthenticationDefaults.AuthenticationType);
         }
     }
     public void SignOut()
     {
         // Send an OpenID Connect sign-out request.
         HttpContext.GetOwinContext().Authentication.SignOut(
              OpenIdConnectAuthenticationDefaults.AuthenticationType, CookieAuthenticationDefaults.AuthenticationType);
     }
     ```

3. <span data-ttu-id="4c1df-157">Views\Shared 열고\_LoginPartial.cshtml tooshow hello 사용자 hello 응용 프로그램 로그인 및 로그 아웃 링크 및 tooprint 뷰에서 hello 사용자의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="4c1df-157">Open Views\Shared\_LoginPartial.cshtml tooshow hello user hello app sign-in and sign-out links, and tooprint out hello user's name in a view.</span></span>

    ```HTML
    @if (Request.IsAuthenticated)
    {
     <text>
         <ul class="nav navbar-nav navbar-right">
             <li class="navbar-text">
                 Hello, @User.Identity.Name!
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

## <a name="step-4-display-user-information"></a><span data-ttu-id="4c1df-158">4단계: 사용자 정보 표시</span><span class="sxs-lookup"><span data-stu-id="4c1df-158">Step 4: Display user information</span></span>
<span data-ttu-id="4c1df-159">OpenID Connect와 사용자를 인증할 때 Azure AD는 "클레임" 또는 hello 사용자에 대 한 어설션을 포함 하는 id_token toohello 응용 프로그램을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1df-159">When it authenticates users with OpenID Connect, Azure AD returns an id_token toohello app that contains "claims," or assertions about hello user.</span></span> <span data-ttu-id="4c1df-160">Hello 다음을 수행 하 여 이러한 클레임 toopersonalize hello 응용 프로그램을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c1df-160">You can use these claims toopersonalize hello app by doing hello following:</span></span>

1. <span data-ttu-id="4c1df-161">Hello Controllers\HomeController.cs 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4c1df-161">Open hello Controllers\HomeController.cs file.</span></span> <span data-ttu-id="4c1df-162">Hello 사용자의 클레임 hello 통해 컨트롤러에 액세스할 수 있습니다 `ClaimsPrincipal.Current` 보안 주체 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="4c1df-162">You can access hello user's claims in your controllers via hello `ClaimsPrincipal.Current` security principal object.</span></span>

 ```C#
 public ActionResult About()
 {
     ViewBag.Name = ClaimsPrincipal.Current.FindFirst(ClaimTypes.Name).Value;
     ViewBag.ObjectId = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
     ViewBag.GivenName = ClaimsPrincipal.Current.FindFirst(ClaimTypes.GivenName).Value;
     ViewBag.Surname = ClaimsPrincipal.Current.FindFirst(ClaimTypes.Surname).Value;
     ViewBag.UPN = ClaimsPrincipal.Current.FindFirst(ClaimTypes.Upn).Value;

     return View();
 }
 ```

2. <span data-ttu-id="4c1df-163">빌드하고 hello 앱을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1df-163">Build and run hello app.</span></span> <span data-ttu-id="4c1df-164">Onmicrosoft.com 도메인 테 넌 트에 새 사용자를 만들지 않았으면, 이제 경우 hello 시간 toodo 하므로입니다.</span><span class="sxs-lookup"><span data-stu-id="4c1df-164">If you haven't already created a new user in your tenant with an onmicrosoft.com domain, now is hello time toodo so.</span></span> <span data-ttu-id="4c1df-165">방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4c1df-165">Here's how:</span></span>

  <span data-ttu-id="4c1df-166">a.</span><span class="sxs-lookup"><span data-stu-id="4c1df-166">a.</span></span> <span data-ttu-id="4c1df-167">해당 사용자도 로그인 하 고 hello 위쪽 막대에 hello 사용자의 id는 반영 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="4c1df-167">Sign in with that user, and note how hello user's identity is reflected on hello top bar.</span></span>

  <span data-ttu-id="4c1df-168">b.</span><span class="sxs-lookup"><span data-stu-id="4c1df-168">b.</span></span> <span data-ttu-id="4c1df-169">로그아웃하고 테넌트의 다른 사용자로 다시 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1df-169">Sign out, and then sign back in as another user in your tenant.</span></span>

  <span data-ttu-id="4c1df-170">c.</span><span class="sxs-lookup"><span data-stu-id="4c1df-170">c.</span></span> <span data-ttu-id="4c1df-171">관심이 있으면 이 앱의 다른 인스턴스를 등록 및 실행하고(자체 clientId 사용) SSO(Single Sign-On) 작동을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="4c1df-171">If you're feeling particularly ambitious, register and run another instance of this app (with its own clientId), and watch single sign-in in action.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4c1df-172">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4c1df-172">Next steps</span></span>
<span data-ttu-id="4c1df-173">참조를 참조 하십시오. [완료 hello 샘플](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip) (없이 구성 값).</span><span class="sxs-lookup"><span data-stu-id="4c1df-173">For reference, see [hello completed sample](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip) (without your configuration values).</span></span>

<span data-ttu-id="4c1df-174">고급 항목 toomore에 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c1df-174">You can now move on toomore advanced topics.</span></span> <span data-ttu-id="4c1df-175">예를 들어 [Azure AD를 사용하여 Web API 보안 유지](active-directory-devquickstarts-webapi-dotnet.md)를 시도해 보세요.</span><span class="sxs-lookup"><span data-stu-id="4c1df-175">For example, try [Secure a Web API with Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

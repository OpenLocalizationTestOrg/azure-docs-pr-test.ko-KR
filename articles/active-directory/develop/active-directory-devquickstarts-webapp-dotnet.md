---
title: "Azure AD .NET 웹앱 시작 | Microsoft Docs"
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
ms.openlocfilehash: 7ac5d3e5cc28ead993e159d003244e6451acb0cc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="aspnet-web-app-sign-in-and-sign-out-with-azure-ad"></a><span data-ttu-id="61247-103">Azure AD에서 ASP.NET 웹앱 로그인 및 로그아웃</span><span class="sxs-lookup"><span data-stu-id="61247-103">ASP.NET web app sign-in and sign-out with Azure AD</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="61247-104">Azure AD(Azure Active Directory)는 몇 개의 코드 줄만으로 단일 로그인 및 로그아웃을 제공하여 간단하게 웹앱의 ID 관리를 아웃소싱할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="61247-104">By providing a single sign-in and sign-out with only a few lines of code, Azure Active Directory (Azure AD) makes it simple for you to outsource web-app identity management.</span></span> <span data-ttu-id="61247-105">.NET (OWIN) 미들웨어에 대한 공개 웹 인터페이스의 Microsoft 구현을 사용하여 ASP.NET 웹앱 내부 및 외부 사용자를 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61247-105">You can sign users in and out of ASP.NET web apps by using the Microsoft implementation of Open Web Interface for .NET (OWIN) middleware.</span></span> <span data-ttu-id="61247-106">커뮤니티 기반 OWIN 미들웨어는 .NET Framework 4.5에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="61247-106">Community-driven OWIN middleware is included in .NET Framework 4.5.</span></span> <span data-ttu-id="61247-107">이 문서에서는 다음에 OWIN을 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="61247-107">This article shows how to use OWIN to:</span></span>

* <span data-ttu-id="61247-108">Azure AD를 ID 공급자로 사용하여 사용자를 웹앱에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="61247-108">Sign users in to web apps by using Azure AD as the identity provider.</span></span>
* <span data-ttu-id="61247-109">일부 사용자 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="61247-109">Display some user information.</span></span>
* <span data-ttu-id="61247-110">앱에서 사용자를 로그아웃합니다.</span><span class="sxs-lookup"><span data-stu-id="61247-110">Sign users out of the apps.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="61247-111">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="61247-111">Before you get started</span></span>
* <span data-ttu-id="61247-112">[앱 기본 사항](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/skeleton.zip)을 다운로드하거나 [완성된 샘플](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip)을 다운로드하세요.</span><span class="sxs-lookup"><span data-stu-id="61247-112">Download the [app skeleton](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) or download the [completed sample](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip).</span></span>
* <span data-ttu-id="61247-113">앱을 등록할 Azure AD 테넌트도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="61247-113">You also need an Azure AD tenant in which to register the app.</span></span> <span data-ttu-id="61247-114">Azure AD 테넌트가 아직 없는 경우 [가져오는 방법을 알아봅니다](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="61247-114">If you don't already have an Azure AD tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="61247-115">준비가 완료되면 다음 4가지 섹션의 절차를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="61247-115">When you are ready, follow the procedures in the next four sections.</span></span>

## <a name="step-1-register-the-new-app-with-azure-ad"></a><span data-ttu-id="61247-116">1단계: Azure AD에 새 앱 등록</span><span class="sxs-lookup"><span data-stu-id="61247-116">Step 1: Register the new app with Azure AD</span></span>
<span data-ttu-id="61247-117">사용자를 인증하도록 앱을 설정하려면 먼저 다음을 수행하여 앱을 테넌트에 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="61247-117">To set up the app to authenticate users, first register it in your tenant by doing the following:</span></span>

1. <span data-ttu-id="61247-118">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="61247-118">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="61247-119">위쪽 모음에서 계정 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="61247-119">On the top bar, click your account name.</span></span> <span data-ttu-id="61247-120">**디렉터리** 목록에서 앱을 등록할 Active Directory 테넌트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="61247-120">Under the **Directory** list, select the Active Directory tenant where you want to register the app.</span></span>
3. <span data-ttu-id="61247-121">왼쪽 창에서 **더 많은 서비스**를 클릭하고 **Azure Active Directory**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="61247-121">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="61247-122">**앱 등록**을 클릭하고 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="61247-122">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="61247-123">프롬프트에 따라 새 **웹 응용 프로그램 및/또는 WebAPI**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="61247-123">Follow the prompts to create a new **Web Application and/or WebAPI**.</span></span>
  * <span data-ttu-id="61247-124">**이름**은 사용자에게 앱에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="61247-124">**Name** describes the app to users.</span></span>
  * <span data-ttu-id="61247-125">**로그온 URL**은 앱의 기본 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="61247-125">**Sign-On URL** is the base URL of the app.</span></span> <span data-ttu-id="61247-126">기본 사항의 기본 URL은 http://localhost:44320/입니다.</span><span class="sxs-lookup"><span data-stu-id="61247-126">The skeleton's default URL is https://localhost:44320/.</span></span>
6. <span data-ttu-id="61247-127">등록이 완료되면 Azure AD가 앱에 고유한 응용 프로그램 ID를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="61247-127">After you've completed the registration, Azure AD assigns the app a unique application ID.</span></span> <span data-ttu-id="61247-128">다음 섹션에서 사용할 수 있도록 앱 페이지의 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="61247-128">Copy the value from the app page to use in the next sections.</span></span>
7. <span data-ttu-id="61247-129">응용 프로그램에 대한 **설정** -> **속성** 페이지에서 앱 ID URI를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="61247-129">From the **Settings** -> **Properties** page for your application, update the App ID URI.</span></span> <span data-ttu-id="61247-130">**앱 ID URI**는 앱의 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="61247-130">The **App ID URI** is a unique identifier for the app.</span></span> <span data-ttu-id="61247-131">명명 규칙은 `https://<tenant-domain>/<app-name>`(예: `https://contoso.onmicrosoft.com/my-first-aad-app`)입니다.</span><span class="sxs-lookup"><span data-stu-id="61247-131">The naming convention is `https://<tenant-domain>/<app-name>` (for example, `https://contoso.onmicrosoft.com/my-first-aad-app`).</span></span>

## <a name="step-2-set-up-the-app-to-use-the-owin-authentication-pipeline"></a><span data-ttu-id="61247-132">2단계: OWIN 인증 파이프라인을 사용하도록 앱 설정</span><span class="sxs-lookup"><span data-stu-id="61247-132">Step 2: Set up the app to use the OWIN authentication pipeline</span></span>
<span data-ttu-id="61247-133">이 단계에서 OpenID Connect 인증 프로토콜을 사용하도록 OWIN 미들웨어를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="61247-133">In this step, you configure the OWIN middleware to use the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="61247-134">OWIN을 사용하여 로그인 및 로그아웃 요청을 실행하고, 사용자 세션을 관리하고, 사용자 정보를 가져오는 등의 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61247-134">You use OWIN to issue sign-in and sign-out requests, manage user sessions, get user information, and so forth.</span></span>

1. <span data-ttu-id="61247-135">시작하려면 패키지 관리자 콘솔을 사용하여 OWIN 미들웨어 NuGet 패키지를 프로젝트에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="61247-135">To begin, add the OWIN middleware NuGet packages to the project by using the Package Manager Console.</span></span>

     ```
     PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
     PM> Install-Package Microsoft.Owin.Security.Cookies
     PM> Install-Package Microsoft.Owin.Host.SystemWeb
     ```

2. <span data-ttu-id="61247-136">`Startup.cs`라는 프로젝트에 OWIN Startup 클래스를 추가하려면 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가**를 선택하고 **새 항목**을 선택한 다음 **OWIN**을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="61247-136">To add an OWIN Startup class to the project called `Startup.cs`, right-click the project, select **Add**, select **New Item**, and then search for **OWIN**.</span></span> <span data-ttu-id="61247-137">OWIN 미들웨어는 앱을 시작하면 **Configuration(...)** 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="61247-137">The OWIN middleware invokes the **Configuration(...)** method when the app starts.</span></span>
3. <span data-ttu-id="61247-138">클래스 선언을 `public partial class Startup`으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="61247-138">Change the class declaration to `public partial class Startup`.</span></span> <span data-ttu-id="61247-139">다른 파일에서 이 클래스의 일부를 구현했습니다.</span><span class="sxs-lookup"><span data-stu-id="61247-139">We've already implemented part of this class for you in another file.</span></span> <span data-ttu-id="61247-140">**Configuration(...)** 메서드에서 **ConfgureAuth(...)**를 호출하여 앱에 대한 인증을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="61247-140">In the **Configuration(...)** method, make a call to **ConfgureAuth(...)** to set up authentication for the app.</span></span>  

     ```C#
     public partial class Startup
     {
         public void Configuration(IAppBuilder app)
         {
             ConfigureAuth(app);
         }
     }
     ```

4. <span data-ttu-id="61247-141">App_Start\Startup.Auth.cs 파일을 연 다음 **ConfigureAuth(...)** 메서드를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="61247-141">Open the App_Start\Startup.Auth.cs file, and then implement the **ConfigureAuth(...)** method.</span></span> <span data-ttu-id="61247-142">*OpenIDConnectAuthenticationOptions*에 제공하는 매개 변수는 앱이 Azure AD와 통신하기 위한 좌표로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="61247-142">The parameters you provide in *OpenIDConnectAuthenticationOptions* serve as coordinates for the app to communicate with Azure AD.</span></span> <span data-ttu-id="61247-143">OpenID Connect 미들웨어는 백그라운드에 쿠키를 사용하므로 쿠키 인증도 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="61247-143">You also need to set up cookie authentication, because the OpenID Connect middleware uses cookies in the background.</span></span>

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

5. <span data-ttu-id="61247-144">프로젝트 루트에 있는 web.config 파일을 연 다음 `<appSettings>` 섹션에 구성 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="61247-144">Open the web.config file in the root of the project, and then enter the configuration values in the `<appSettings>` section.</span></span>
  * <span data-ttu-id="61247-145">`ida:ClientId`: "1단계: Azure AD에 새 앱 등록"에서 Azure Portal에서 복사한 GUID입니다.</span><span class="sxs-lookup"><span data-stu-id="61247-145">`ida:ClientId`: The GUID you copied from the Azure portal in "Step 1: Register the new app with Azure AD."</span></span>
  * <span data-ttu-id="61247-146">`ida:Tenant`: Azure AD 테넌트의 이름(예: contoso.onmicrosoft.com)입니다.</span><span class="sxs-lookup"><span data-stu-id="61247-146">`ida:Tenant`: The name of your Azure AD tenant (for example, contoso.onmicrosoft.com).</span></span>
  * <span data-ttu-id="61247-147">`ida:PostLogoutRedirectUri`: 로그아웃 요청이 성공적으로 완료된 후 사용자가 리디렉션되는 Azure AD를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="61247-147">`ida:PostLogoutRedirectUri`: The indicator that tells Azure AD where a user should be redirected after a sign-out request is successfully completed.</span></span>

## <a name="step-3-use-owin-to-issue-sign-in-and-sign-out-requests-to-azure-ad"></a><span data-ttu-id="61247-148">3단계: OWIN을 사용하여 Azure AD에 로그인 및 로그아웃 요청 실행</span><span class="sxs-lookup"><span data-stu-id="61247-148">Step 3: Use OWIN to issue sign-in and sign-out requests to Azure AD</span></span>
<span data-ttu-id="61247-149">이제 앱은 OpenID Connect 인증 프로토콜을 사용하여 Azure AD와 통신하도록 올바르게 구성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="61247-149">The app is now properly configured to communicate with Azure AD by using the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="61247-150">OWIN이 인증 메시지를 작성하고, Azure AD에서 토큰의 유효성을 검사하고, 사용자 세션을 유지 관리하는 모든 세부 과정을 처리했습니다.</span><span class="sxs-lookup"><span data-stu-id="61247-150">OWIN has handled all of the details of crafting authentication messages, validating tokens from Azure AD, and maintaining user sessions.</span></span> <span data-ttu-id="61247-151">이제 사용자에게 로그인하고 로그아웃하는 방법을 알려주기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="61247-151">All that remains is to give your users a way to sign in and sign out.</span></span>

1. <span data-ttu-id="61247-152">컨트롤러에서 권한 부여 태그를 사용하여 사용자가 특정 페이지에 액세스하기 전에 로그인하도록 요구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61247-152">You can use authorize tags in your controllers to require users to sign in before they access certain pages.</span></span> <span data-ttu-id="61247-153">이렇게 하려면 controllers\ homecontroller.cs를 연 다음 About 컨트롤러에는 `[Authorize]` 태그를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="61247-153">To do so, open Controllers\HomeController.cs, and then add the `[Authorize]` tag to the About controller.</span></span>

     ```C#
     [Authorize]
     public ActionResult About()
     {
       ...
     ```

2. <span data-ttu-id="61247-154">또한 OWIN을 사용하여 코드 내에서 직접 인증 요청을 실행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61247-154">You can also use OWIN to directly issue authentication requests from within your code.</span></span> <span data-ttu-id="61247-155">이렇게 하려면 Controllers\AccountController.cs를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="61247-155">To do so, open Controllers\AccountController.cs.</span></span> <span data-ttu-id="61247-156">그런 다음 SignIn() 및 SignOut() 작업에서 OpenID Connect 챌린지 및 로그아웃 요청을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="61247-156">Then, in the SignIn() and SignOut() actions, issue OpenID Connect challenge and sign-out requests.</span></span>

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

3. <span data-ttu-id="61247-157">Views\Shared\_LoginPartial.cshtml을 열고 사용자에게 앱 로그인 및 로그 아웃 링크를 표시하고 보기에서 사용자의 이름을 인쇄합니다.</span><span class="sxs-lookup"><span data-stu-id="61247-157">Open Views\Shared\_LoginPartial.cshtml to show the user the app sign-in and sign-out links, and to print out the user's name in a view.</span></span>

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

## <a name="step-4-display-user-information"></a><span data-ttu-id="61247-158">4단계: 사용자 정보 표시</span><span class="sxs-lookup"><span data-stu-id="61247-158">Step 4: Display user information</span></span>
<span data-ttu-id="61247-159">OpenID Connect로 사용자를 인증할 때 Azure AD는 “클레임” 또는 사용자에 대한 어설션을 포함하는 id_token을 앱에 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="61247-159">When it authenticates users with OpenID Connect, Azure AD returns an id_token to the app that contains "claims," or assertions about the user.</span></span> <span data-ttu-id="61247-160">다음을 수행하여 앱 개인에 맞게 이러한 클레임을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61247-160">You can use these claims to personalize the app by doing the following:</span></span>

1. <span data-ttu-id="61247-161">Controllers\HomeController.cs 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="61247-161">Open the Controllers\HomeController.cs file.</span></span> <span data-ttu-id="61247-162">`ClaimsPrincipal.Current` 보안 주체 개체를 통해 컨트롤러의 사용자 클레임에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61247-162">You can access the user's claims in your controllers via the `ClaimsPrincipal.Current` security principal object.</span></span>

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

2. <span data-ttu-id="61247-163">앱을 빌드 및 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="61247-163">Build and run the app.</span></span> <span data-ttu-id="61247-164">onmicrosoft.com 도메인을 사용하여 테넌트에 아직 새 사용자를 만들지 않았으면 이제 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="61247-164">If you haven't already created a new user in your tenant with an onmicrosoft.com domain, now is the time to do so.</span></span> <span data-ttu-id="61247-165">방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="61247-165">Here's how:</span></span>

  <span data-ttu-id="61247-166">a.</span><span class="sxs-lookup"><span data-stu-id="61247-166">a.</span></span> <span data-ttu-id="61247-167">해당 사용자로 로그인하고 위쪽 모음에 사용자 ID가 반영되는 방식을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="61247-167">Sign in with that user, and note how the user's identity is reflected on the top bar.</span></span>

  <span data-ttu-id="61247-168">b.</span><span class="sxs-lookup"><span data-stu-id="61247-168">b.</span></span> <span data-ttu-id="61247-169">로그아웃하고 테넌트의 다른 사용자로 다시 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="61247-169">Sign out, and then sign back in as another user in your tenant.</span></span>

  <span data-ttu-id="61247-170">c.</span><span class="sxs-lookup"><span data-stu-id="61247-170">c.</span></span> <span data-ttu-id="61247-171">관심이 있으면 이 앱의 다른 인스턴스를 등록 및 실행하고(자체 clientId 사용) SSO(Single Sign-On) 작동을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="61247-171">If you're feeling particularly ambitious, register and run another instance of this app (with its own clientId), and watch single sign-in in action.</span></span>

## <a name="next-steps"></a><span data-ttu-id="61247-172">다음 단계</span><span class="sxs-lookup"><span data-stu-id="61247-172">Next steps</span></span>
<span data-ttu-id="61247-173">참조용 자료로 [완성된 샘플](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip)(사용자 구성 값 제외)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="61247-173">For reference, see [the completed sample](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip) (without your configuration values).</span></span>

<span data-ttu-id="61247-174">이제 좀 더 고급 항목으로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61247-174">You can now move on to more advanced topics.</span></span> <span data-ttu-id="61247-175">예를 들어 [Azure AD를 사용하여 Web API 보안 유지](active-directory-devquickstarts-webapi-dotnet.md)를 시도해 보세요.</span><span class="sxs-lookup"><span data-stu-id="61247-175">For example, try [Secure a Web API with Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

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
# <a name="aspnet-web-app-sign-in-and-sign-out-with-azure-ad"></a>Azure AD에서 ASP.NET 웹앱 로그인 및 로그아웃
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

로그인 및 로그 아웃 하는 단일 단 몇 줄의 코드를 제공 함으로써 Azure Active Directory (Azure AD) 간단 하 게 하면 toooutsource 웹 응용 프로그램 id 관리 합니다. .NET (OWIN) 미들웨어에 대 한 Open Web Interface의 Microsoft 구현 hello를 사용 하 여 ASP.NET 웹 응용 프로그램 내부 및 외부 사용자가 서명할 수 있습니다. 커뮤니티 기반 OWIN 미들웨어는 .NET Framework 4.5에 포함됩니다. 이 문서에서는 어떻게 toouse OWIN에:

* Hello id 공급자로 Azure AD를 사용 하 여 tooweb 앱에서 사용자를 로그인 합니다.
* 일부 사용자 정보를 표시합니다.
* Hello 앱에서 사용자를 로그인 합니다.

## <a name="before-you-get-started"></a>시작하기 전에
* Hello 다운로드 [앱 스 켈 레 톤](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) hello 다운로드 또는 [완성 된 샘플](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip)합니다.
* 어떤 tooregister hello 앱에서 Azure AD 테 넌 트가 있어야합니다. Azure AD 테 넌 트가 아직 없는 경우 [자세한 방법을 하나 tooget](active-directory-howto-tenant.md)합니다.

준비 되 면 다음 절차에 따라 hello hello 다음 네 개의 절.

## <a name="step-1-register-hello-new-app-with-azure-ad"></a>1 단계: Azure AD와 hello 새 앱 등록
tooset hello 앱 tooauthenticate 사용자를 처음 등록할 테 넌 트에 hello 다음을 수행 하 여:

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. Hello 위쪽 막대에서 계정 이름을 클릭 합니다. Hello에서 **디렉터리** 목록, 선택 hello Active Directory 테 넌 트 tooregister hello 앱을 원하는 합니다.
3. 클릭 **더 서비스** 에 hello 왼쪽된 창에서 선택한 후 **Azure Active Directory**합니다.
4. **앱 등록**을 클릭하고 **추가**를 선택합니다.
5. 에 따라 hello에서 묻는 메시지를 표시 하는 새 toocreate **웹 응용 프로그램 및/또는 WebAPI**합니다.
  * **이름** hello 앱 toousers에 설명 합니다.
  * **로그온 URL** hello hello 응용 프로그램의 기본 URL입니다. hello 뼈대 기본 URL은 https://localhost:44320 / 합니다.
6. Azure AD를 hello 등록을 완료 한 후 hello 앱 고유한 응용 프로그램 ID를 할당 Hello 다음 섹션의 앱 페이지 toouse hello에서에서 hello 값을 복사 합니다.
7. Hello에서 **설정** -> **속성** 응용 프로그램에 대 한 페이지를 hello 앱 ID URI를 업데이트 합니다. hello **앱 ID URI** hello 앱에 대 한 고유 식별자입니다. hello 명명 규칙은 `https://<tenant-domain>/<app-name>` (예를 들어 `https://contoso.onmicrosoft.com/my-first-aad-app`).

## <a name="step-2-set-up-hello-app-toouse-hello-owin-authentication-pipeline"></a>2 단계: hello 앱 toouse hello OWIN 인증 파이프라인 설정
이 단계에서는 hello OWIN 미들웨어 toouse hello OpenID Connect 인증 프로토콜을 구성 합니다. OWIN tooissue 로그인 및 로그 아웃 요청을 사용 하 여, 관리 사용자 세션, 사용자 정보를 가져오기 하 등입니다.

1. toobegin, hello 패키지 관리자 콘솔을 사용 하 여 hello OWIN 미들웨어 NuGet 패키지 toohello 프로젝트를 추가 합니다.

     ```
     PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
     PM> Install-Package Microsoft.Owin.Security.Cookies
     PM> Install-Package Microsoft.Owin.Host.SystemWeb
     ```

2. OWIN 시작 클래스 toohello 프로젝트 라는 tooadd `Startup.cs`hello 프로젝트를 마우스 오른쪽 단추로 선택 **추가**선택, **새 항목**, 검색할 **OWIN**합니다. hello를 호출 하는 OWIN 미들웨어입니다. hello **Configuration(...)**  hello 앱이 시작 될 때 메서드.
3. Hello 클래스 선언에도 변경`public partial class Startup`합니다. 다른 파일에서 이 클래스의 일부를 구현했습니다. Hello에 **Configuration(...)**  메서드를 너무 호출할**ConfgureAuth(...)**  tooset hello 앱에 대 한 인증을 합니다.  

     ```C#
     public partial class Startup
     {
         public void Configuration(IAppBuilder app)
         {
             ConfigureAuth(app);
         }
     }
     ```

4. 그런 다음 hello를 구현 하 고 hello App_Start\Startup.Auth.cs 파일을 열고 **ConfigureAuth(...)**  메서드. 매개 변수가 hello *OpenIDConnectAuthenticationOptions* 역할을 Azure AD와 앱 toocommunicate hello에 대 한 좌표입니다. 또한 필요 하면 tooset 쿠키 인증을 hello OpenID Connect 미들웨어 hello 백그라운드에서 쿠키를 사용 합니다.

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

5. Hello 프로젝트의 hello 루트에서 hello web.config 파일을 연 다음 hello에 hello 구성 값을 입력 `<appSettings>` 섹션.
  * `ida:ClientId`: Azure 포털에서 hello에서 복사한 GUID hello "1 단계: Azure AD와 hello 새 앱 등록 합니다."
  * `ida:Tenant`: hello 이름에 Azure AD 테 넌 트 (예: contoso.onmicrosoft.com)입니다.
  * `ida:PostLogoutRedirectUri`: 사용자 리디렉션해야 로그 아웃 요청을 성공적으로 완료 된 후에 Azure AD를 알려 주는 hello 표시기입니다.

## <a name="step-3-use-owin-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a>3 단계: 사용 tooAzure 광고를 요청 하는 OWIN tooissue 로그인 및 로그 아웃
hello 이제 앱을 Azure AD와 올바르게 구성 된 toocommunicate hello OpenID Connect 인증 프로토콜을 사용 하 여 합니다. OWIN 인증 메시지를 만들어, Azure AD에서 토큰의 유효성 검사 및 사용자 세션을 유지 관리의 hello 세부 정보를 모두 처리 했습니다. 나머지 작업은 toogive 사용자의 방식으로 toosign 및 로그 아웃 합니다.

1. 에서는 특정 페이지를 액세스 하기 전에 태그에는 컨트롤러 toorequire 사용자 toosign에 권한을 부여 합니다. toodo 따라서 Controllers\HomeController.cs를 열고 다음 추가 hello `[Authorize]` toohello 컨트롤러에 대 한 태그를 지정 합니다.

     ```C#
     [Authorize]
     public ActionResult About()
     {
       ...
     ```

2. OWIN toodirectly 문제에서 오는 인증 요청이 코드 내에서 사용할 수도 있습니다. 따라서 toodo Controllers\AccountController.cs를 엽니다. 그런 다음 hello SignIn() 및 SignOut() 작업의 OpenID Connect 챌린지 및 로그 아웃 요청을 실행 합니다.

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

3. Views\Shared 열고\_LoginPartial.cshtml tooshow hello 사용자 hello 응용 프로그램 로그인 및 로그 아웃 링크 및 tooprint 뷰에서 hello 사용자의 이름입니다.

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

## <a name="step-4-display-user-information"></a>4단계: 사용자 정보 표시
OpenID Connect와 사용자를 인증할 때 Azure AD는 "클레임" 또는 hello 사용자에 대 한 어설션을 포함 하는 id_token toohello 응용 프로그램을 반환 합니다. Hello 다음을 수행 하 여 이러한 클레임 toopersonalize hello 응용 프로그램을 사용할 수 있습니다.

1. Hello Controllers\HomeController.cs 파일을 엽니다. Hello 사용자의 클레임 hello 통해 컨트롤러에 액세스할 수 있습니다 `ClaimsPrincipal.Current` 보안 주체 개체입니다.

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

2. 빌드하고 hello 앱을 실행 합니다. Onmicrosoft.com 도메인 테 넌 트에 새 사용자를 만들지 않았으면, 이제 경우 hello 시간 toodo 하므로입니다. 방법은 다음과 같습니다.

  a. 해당 사용자도 로그인 하 고 hello 위쪽 막대에 hello 사용자의 id는 반영 하는 방법입니다.

  b. 로그아웃하고 테넌트의 다른 사용자로 다시 로그인합니다.

  c. 관심이 있으면 이 앱의 다른 인스턴스를 등록 및 실행하고(자체 clientId 사용) SSO(Single Sign-On) 작동을 살펴봅니다.

## <a name="next-steps"></a>다음 단계
참조를 참조 하십시오. [완료 hello 샘플](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip) (없이 구성 값).

고급 항목 toomore에 이동할 수 있습니다. 예를 들어 [Azure AD를 사용하여 Web API 보안 유지](active-directory-devquickstarts-webapi-dotnet.md)를 시도해 보세요.

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

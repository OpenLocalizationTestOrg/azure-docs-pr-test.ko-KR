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
# <a name="add-sign-in-tooan-net-mvc-web-app"></a>로그인 tooan.NET MVC 웹 응용 프로그램 추가
Hello v2.0 끝점과 두 개인 Microsoft 계정에 대 한 지원 및 회사 또는 학교 계정으로 인증 tooyour 웹 앱을 신속 하 게 추가할 수 있습니다.  Asp.NET 웹앱에서는 .NET Framework 4.5에 포함된 Microsoft OWIN 미들웨어를 사용하여 이 작업을 수행할 수 있습니다.

> [!NOTE]
> 모든 Azure Active Directory 시나리오 및 기능 hello v2.0 끝점에서 사용할 수 있습니다.  에 대해 알아보세요 hello v2.0 끝점을 사용 해야 하는 경우 toodetermine [v2.0 제한](active-directory-v2-limitations.md)합니다.
>
>

 여기 빌드합니다 OWIN toosign hello 사용자 표시에 사용 하는 웹 앱 hello 사용자에 대 한 정보 및 기호 hello hello 앱에서 사용자입니다.

## <a name="download"></a>다운로드
이 자습서에 대 한 hello 코드 유지 관리 [GitHub에서](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet)합니다.  수에 따라 toofollow, [.zip으로 hello 응용 프로그램의 기본 정의 다운로드](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) 또는 복제 hello 스 켈 레 톤:

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet.git```

완료 하는 hello 앱도이 자습서의 hello 끝에 제공 됩니다.

## <a name="register-an-app"></a>앱 등록
[apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)에서 새 앱을 만들거나 다음 [세부 단계](active-directory-v2-app-registration.md)를 따릅니다.  다음을 수행해야 합니다.

* Hello 아래로 복사 **응용 프로그램 Id** tooyour 응용 프로그램에 할당 해야 곧 합니다.
* Hello 추가 **웹** 응용 프로그램을 위한 플랫폼입니다.
* 올바른 hello 입력 **리디렉션 URI**합니다. hello 리디렉션 uri 나타냅니다 tooAzure AD에 인증 응답 디렉션할-hello 기본적으로이 자습서는 `https://localhost:44326/`합니다.

## <a name="install--configure-owin-authentication"></a>OWIN 인증 설치 및 구성
여기서 hello OWIN 미들웨어 toouse hello OpenID Connect 인증 프로토콜을 구성 합니다.  OWIN tooissue 사용 되는 로그인 및 로그 아웃 요청, hello 사용자의 세션을 관리 되며 다른 작업 간에 hello 사용자에 대 한 정보를 가져옵니다.

1. toobegin, 열기 hello `web.config` hello 프로젝트의 hello 루트에서 파일을 hello에 응용 프로그램의 구성 값을 입력 `<appSettings>` 섹션.

  * hello `ida:ClientId` 는 hello **응용 프로그램 Id** hello 등록 포털에서 tooyour 응용 프로그램을 할당 합니다.
  * hello `ida:RedirectUri` 는 hello **리디렉션 Uri** hello 포털에 입력 합니다.

2. 다음으로 hello 패키지 관리자 콘솔을 사용 하 여 hello OWIN 미들웨어 NuGet 패키지 toohello 프로젝트를 추가 합니다.

        ```
        PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
        PM> Install-Package Microsoft.Owin.Security.Cookies
        PM> Install-Package Microsoft.Owin.Host.SystemWeb
        ```  

3. "OWIN 시작 클래스" toohello 프로젝트 라는 추가 `Startup.cs` hello 프로젝트 클릭--> 오른쪽 **추가** --> **새 항목** "OWIN"에 대 한 검색--> 합니다.  hello OWIN 미들웨어는 hello를 호출 하는 `Configuration(...)` 메서드 앱이 시작 되는 경우.
4. Hello 클래스 선언에도 변경`public partial class Startup` -이미 구현 했습니다이 클래스의 일부를 다른 파일에 있습니다.  Hello에 `Configuration(...)` 메서드를 웹 앱에 대 한 인증을 호출 tooConfigureAuth(...) tooset 확인  

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

5. 파일 열기 hello `App_Start\Startup.Auth.cs` hello를 구현 하 고 `ConfigureAuth(...)` 메서드.  매개 변수가 hello `OpenIdConnectAuthenticationOptions` 좌표 Azure AD와 앱 toocommunicate 프로그램에 대 한 역할을 수행 합니다.  또한 tooset 쿠키 인증을 해야-hello OpenID Connect 미들웨어 hello 표지 아래 쿠키를 사용 합니다.

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

## <a name="send-authentication-requests"></a>인증 요청 보내기
이제 앱이 올바르게 구성 된 toocommunicate hello OpenID Connect 인증 프로토콜을 사용 하 여 hello v2.0 끝점을 사용 합니다.  OWIN 모든 인증 메시지를 만들어, Azure AD에서 토큰의 유효성 검사 및 사용자 세션을 유지 관리의 hello 까다로운 세부 정보가 처리 했습니다.  나머지 작업은 toogive 사용자의 방식으로 toosign 및 로그 아웃 합니다.

- 사용할 수 있습니다 태그에 권한을 부여 컨트롤러 toorequire에 사용자가 로그인 특정 페이지에 액세스 하기 전에.  열기 `Controllers\HomeController.cs`, hello 추가 `[Authorize]` toohello 컨트롤러에 대 한 태그를 지정 합니다.
        
        ```C#
        [Authorize]
        public ActionResult About()
        {
          ...
        ```

- OWIN toodirectly 문제에서 오는 인증 요청이 코드 내에서 사용할 수도 있습니다.  `Controllers\AccountController.cs`을(를) 엽니다.  SignIn() hello 및 SignOut() 동작에 각각 챌린지 OpenID Connect 및 로그 아웃 요청을 실행 합니다.

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

- 이제 `Views\Shared\_LoginPartial.cshtml`을 엽니다.  이 hello 사용자 응용 프로그램의 로그인 및 로그 아웃 링크를 표시 하 고 뷰에서 hello 사용자의 이름을 출력 합니다.

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

## <a name="display-user-information"></a>사용자 정보 표시
OpenID Connect와 사용자를 인증할 때 hello v2.0 끝점 hello 사용자에 대 한 어설션 또는 클레임을 포함 하는 id_token toohello 응용 프로그램을 반환 합니다.  이러한 클레임 toopersonalize 앱을 사용할 수 있습니다.

- 열기 hello `Controllers\HomeController.cs` 파일입니다.  Hello 사용자의 클레임 hello 통해 컨트롤러에 액세스할 수 있습니다 `ClaimsPrincipal.Current` 보안 주체 개체입니다.

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

## <a name="run"></a>실행
마지막으로 앱을 빌드하고 실행합니다.   개인 Microsoft 계정 또는 회사 또는 학교 계정으로 로그인 하 고 hello 사용자의 id hello 위쪽 탐색 모음에 어떻게 반영 됩니다.  이제 개인 및 회사/학교 계정으로 사용자를 인증할 수 있는 업계 표준 프로토콜을 사용하여 웹앱이 보안되었습니다.

참조용으로 hello 구성 값) (없이 샘플을 완료 [.zip을 여기로 제공 됩니다](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/complete.zip), 또는 GitHub에서 복제할 수 있습니다.

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet.git```

## <a name="next-steps"></a>다음 단계
이제 좀 더 고급 항목으로 이동할 수 있습니다.  Tootry를 사용할 수 있습니다.

[Hello hello v2.0 끝점과 웹 API 보안 >>](active-directory-devquickstarts-webapi-dotnet.md)

추가 리소스는 다음을 확인해보세요.

* [hello v2.0 개발자 가이드 >>](active-directory-appmodel-v2-overview.md)
* [StackOverflow "azure-active-directory" 태그 >>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a>당사 제품에 대한 보안 업데이트 가져오기
보안 사고를 방문 하 여 발생 하는 경우의 알림 tooget 좋습니다 [이 페이지](https://technet.microsoft.com/security/dd252948) 및 tooSecurity 자문 경고를 구독 합니다.

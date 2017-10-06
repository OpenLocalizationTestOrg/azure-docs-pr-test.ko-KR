---
title: Active Directory B2C aaaAzure | Microsoft Docs
description: "어떻게 toobuild 웹 응용 프로그램 로그-up/로그인을 프로필 편집 및 Azure Active Directory B2C를 사용 하 여 다시 설정 하는 암호입니다."
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: barbaraselden
ms.assetid: 30261336-d7a5-4a6d-8c1a-7943ad76ed25
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/17/2017
ms.author: parakhj
ms.openlocfilehash: 187f99a8dd50d212de4f0517f552cdbbe5a8edf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-web-app-with-azure-active-directory-b2c-sign-up-sign-in-profile-edit-and-password-reset"></a>Azure Active Directory B2C 등록, 로그인, 프로필 편집 및 암호 재설정을 사용하여 ASP.NET 웹앱 만들기

이 자습서에서는 다음을 수행하는 방법에 대해 설명합니다.

> [!div class="checklist"]
> * Azure AD B2C identity 기능 tooyour 웹 응용 프로그램 추가
> * Azure AD B2C 디렉터리에 웹앱 등록
> * 웹앱에 대한 사용자 등록/로그인, 프로필 편집 및 암호 재설정 정책 만들기

## <a name="prerequisites"></a>필수 조건

- 프로그램 B2C 테 넌 트 tooan Azure 계정을 연결 해야 합니다. [여기](https://azure.microsoft.com/en-us/)에서 Azure 계정을 만들 수 있습니다.
- 필요한 [Microsoft Visual Studio](https://www.visualstudio.com/) 또는 유사한 tooview 프로그래밍 하 고 hello 샘플 코드를 수정 합니다.

## <a name="create-an-azure-ad-b2c-directory"></a>Azure AD B2C 디렉터리 만들기

Azure AD B2C를 사용하기 전에 디렉터리 또는 테넌트를 만들어야 합니다. 디렉터리는 모든 사용자, 앱, 그룹 등을 위한 컨테이너입니다. 아직 없는 경우 B2C 디렉터리를 만든 후에 이 가이드를 계속 진행합니다.

[!INCLUDE [active-directory-b2c-create-tenant](../../includes/active-directory-b2c-create-tenant.md)]

> [!NOTE]
> 
> Tooconnect hello B2C 테 넌 트 tooyour Azure 구독이 필요합니다. 선택한 후 **만들기**을 선택 hello **링크 기존 Azure AD B2C 테 넌 트 toomy Azure 구독** 옵션을 선택한 다음 hello **Azure AD B2C 테 넌 트** 드롭다운을 선택 hello tooassociate 원하는 테 넌 트.

## <a name="create-and-register-an-application"></a>응용 프로그램 만들기 및 등록

다음으로 toocreate 필요 하 고 B2C 디렉터리 hello 앱을 등록 합니다. 이렇게 하면 필요한 정보를 Azure AD B2C toosecurely 앱과 통신 합니다. 

[!INCLUDE [active-directory-b2c-register-web-api](../../includes/active-directory-b2c-register-web-api.md)]

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

완료되면 응용 프로그램 설정에 API 및 네이티브 응용 프로그램 모두를 갖습니다.

## <a name="create-policies-on-your-b2c-tenant"></a>B2C 테넌트에 정책 만들기

Azure AD B2C에서 모든 사용자 환경은 [정책](active-directory-b2c-reference-policies.md)에 의해 정의됩니다. 이 코드 샘플은 **등록 및 로그인**, **프로필 편집** 및 **암호 재설정**의 세 가지 ID 환경을 포함합니다.  Hello에 설명 된 대로 각 유형의 toocreate 하나의 정책이 필요한 [정책 참조 문서](active-directory-b2c-reference-policies.md)합니다. 각 정책에 대 한 tooselect hello 표시 이름 특성 또는 클레임 있으며 나중에 사용할 정책 hello 이름 아래로 toocopy 수 있습니다.

### <a name="add-your-identity-providers"></a>ID 공급자 추가

설정에서 **ID 공급자**를 선택하고 사용자 이름 등록 또는 전자 메일 등록을 선택합니다.

### <a name="create-a-sign-up-and-sign-in-policy"></a>등록 및 로그인 정책 만들기

[!INCLUDE [active-directory-b2c-create-sign-in-sign-up-policy](../../includes/active-directory-b2c-create-sign-in-sign-up-policy.md)]

### <a name="create-a-profile-editing-policy"></a>프로필 편집 정책 만들기

[!INCLUDE [active-directory-b2c-create-profile-editing-policy](../../includes/active-directory-b2c-create-profile-editing-policy.md)]

### <a name="create-a-password-reset-policy"></a>암호 재설정 정책 만들기

[!INCLUDE [active-directory-b2c-create-password-reset-policy](../../includes/active-directory-b2c-create-password-reset-policy.md)]

준비 toobuild 하 여 정책을 만든 후 응용 프로그램입니다.

## <a name="download-hello-sample-code"></a>Hello 샘플 코드 다운로드

이 자습서에 대 한 hello 코드에서 유지 관리 됩니다 [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi)합니다. 실행 하 여 hello 샘플을 복제할 수 있습니다.

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

Hello 샘플 코드를 다운로드 한 후 hello open Visual Studio.sln 파일 tooget 시작 합니다. hello 솔루션 파일에는 두 개의 프로젝트가 포함 되어: `TaskWebApp` 및 `TaskService`합니다. `TaskWebApp`상호 작용 하는 hello 사용자 hello MVC 웹 응용 프로그램입니다. `TaskService`각 사용자의 할 일 목록에 저장 하는 hello 앱 백 엔드 웹 API입니다. 이 문서에서는 hello 설명만 `TaskWebApp` 응용 프로그램입니다. toolearn 어떻게 toobuild `TaskService` Azure AD B2C를 사용 하 여 참조 [우리의.NET 웹 api 자습서](active-directory-b2c-devquickstarts-api-dotnet.md)합니다.

## <a name="update-code-toouse-your-tenant-and-policies"></a>테 넌 트 및 정책에 맞게 코드 toouse 업데이트

이 샘플은 구성 된 toouse hello 정책 및 클라이언트 ID 우리의 데모 테 넌 트입니다. tooconnect 것 tooyour 자체 테 넌 트 tooopen 해야 `web.config` hello에 `TaskWebApp` 프로젝트 및 다음 값에는 hello 바꾸기:

* `ida:Tenant`를 테넌트 이름으로 바꿉니다.
* `ida:ClientId`를 웹앱 응용 프로그램 ID로 바꿉니다.
* `ida:ClientSecret`을 웹앱 비밀 키로 바꿉니다.
* `ida:SignUpSignInPolicyId`를 "등록 또는 로그인" 정책 이름으로 바꿉니다.
* `ida:EditProfilePolicyId`를 "프로필 편집" 정책 이름으로 바꿉니다.
* `ida:ResetPasswordPolicyId`를 "암호 재설정" 정책 이름으로 바꿉니다.

## <a name="launch-hello-app"></a>Hello 앱 시작
Visual Studio 내에서 hello 앱을 시작 합니다. URl은 참고 hello 및 toohello 할 일 목록 탭 탐색: https://login.microsoftonline.com/*YourTenantName*/oauth2/v2.0/authorize?p=*YourSignUpPolicyName*& client_id =* YourclientID*...

전자 메일 주소 또는 사용자 이름을 사용 하 여 hello 앱 등록 합니다. 로그 아웃 한 다음 다시 로그인 하 고 hello 프로필을 편집 하거나 hello 암호 다시 설정 로그아웃했다가 다른 사용자로 로그인합니다. 

## <a name="add-social-idps"></a>소셜 IDP 추가

현재 hello 앱에서 등록 및 로그인 사용자만 사용 하 여 **로컬 계정**; 사용자 이름 및 암호를 사용 하는 계정을 B2C 디렉터리에 저장 합니다. Azure AD B2C를 사용하면 코드를 변경하지 않고도 다른 **IDP(ID 공급자)** 에 대한 지원을 추가할 수 있습니다.

tooadd 소셜 IDPs tooyour 응용 프로그램에 따라 hello 방법을 다음이 문서에 자세히 설명 합니다. 에 대 한 각 IDP toosupport 5d; 응용 프로그램 tooregister 해당 시스템에 필요 하 고 클라이언트 ID를 얻습니다.

* [Facebook을 IDP로 설정](active-directory-b2c-setup-fb-app.md)
* [Google을 IDP로 설정](active-directory-b2c-setup-goog-app.md)
* [Amazon을 IDP로 설정](active-directory-b2c-setup-amzn-app.md)
* [LinkedIn을 IDP로 설정](active-directory-b2c-setup-li-app.md)

Hello identity 공급자 tooyour B2C 디렉터리, 각 편집의 세 가지 정책 tooinclude hello에 설명 된 대로 새 IDPs hello 추가한 후 [정책 참조 문서](active-directory-b2c-reference-policies.md)합니다. 정책을 저장 한 후 hello 앱을 다시 실행 합니다.  각 identity 경험 있는 로그인 및 등록 옵션으로 새 IDPs 추가 hello를 표시 되어야 합니다.

정책을 테스트 하 여 및 샘플 앱에 hello 결과 확인할 수 있습니다. IDP를 추가 또는 제거하거나 응용 프로그램 클레임을 조작하거나 등록 특성을 변경합니다. 어떻게 정책, 인증 요청 및 OWIN을 모두 함께 연결하는지 확인할 수 있을 때까지 실험해 보세요.

## <a name="sample-code-walkthrough"></a>샘플 코드 연습
다음 섹션 hello hello 예제 응용 프로그램 코드 구성 하는 방법을 보여 줍니다. 이후 앱 개발에서 지침으로 사용할 수 있습니다.

### <a name="add-authentication-support"></a>인증 지원 추가

이제 Azure AD B2C 하 여 응용 프로그램 toouse를 구성할 수 있습니다. 앱은 OpenID Connect 인증 요청을 보내 Azure AD B2C와 통신합니다. hello 요청 사항이 hello 사용자 경험 앱 hello 정책을 지정 하 여 tooexecute 하려고 합니다. 이러한 요청을 Microsoft의 OWIN 라이브러리 toosend 사용 지정, 정책 실행, 사용자 세션을 관리 합니다.

#### <a name="install-owin"></a>OWIN 설치

toobegin, hello Visual Studio 패키지 관리자 콘솔을 사용 하 여 hello OWIN 미들웨어 NuGet 패키지 toohello 프로젝트를 추가 합니다.

```Console
PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
PM> Install-Package Microsoft.Owin.Security.Cookies
PM> Install-Package Microsoft.Owin.Host.SystemWeb
```

#### <a name="add-an-owin-startup-class"></a>OWIN 시작 클래스 추가

OWIN 시작 클래스 toohello API 호출 추가 `Startup.cs`합니다.  Hello 프로젝트를 마우스 오른쪽 단추로 클릭 **추가** 및 **새 항목**, 한 다음 OWIN에 대 한 검색 합니다. hello OWIN 미들웨어는 hello를 호출 하는 `Configuration(…)` 메서드 앱이 시작 되는 경우.

이 예제에서는 변경 했습니다 hello 클래스 선언 너무`public partial class Startup` 구현에서 hello 클래스의 다른 부분을 hello `App_Start\Startup.Auth.cs`합니다. 내부 hello `Configuration` 메서드를 호출 너무 추가`ConfigureAuth`에 정의 된 `Startup.Auth.cs`합니다. Hello 수정한 다음 `Startup.cs` hello 다음과 같습니다.

```CSharp
// Startup.cs

public partial class Startup
{
    // hello OWIN middleware will invoke this method when hello app starts
    public void Configuration(IAppBuilder app)
    {
        // ConfigureAuth defined in other part of hello class
        ConfigureAuth(app);
    }
}
```

#### <a name="configure-hello-authentication-middleware"></a>Hello 인증 미들웨어를 구성 합니다.

파일 열기 hello `App_Start\Startup.Auth.cs` hello를 구현 하 고 `ConfigureAuth(...)` 메서드. 매개 변수가 hello `OpenIdConnectAuthenticationOptions` 좌표와 Azure AD B2C 앱 toocommunicate 프로그램에 대 한으로 사용 합니다. 특정 매개 변수를 지정 하지 않으면 hello 기본값을 사용 합니다. 예를 들어 hello를 지정 하지 않는 `ResponseType` hello 샘플에서 기본값 이므로 hello `code id_token` 각 나가는 요청 tooAzure AD B2C에에서 사용 됩니다.

Tooset 쿠키 인증을 해야합니다. hello OpenID Connect 미들웨어 무엇 보다도 쿠키 toomaintain 사용자 세션을 사용합니다.

```CSharp
// App_Start\Startup.Auth.cs

public partial class Startup
{
    // Initialize variables ...

    // Configure hello OWIN middleware
    public void ConfigureAuth(IAppBuilder app)
    {
        app.UseCookieAuthentication(new CookieAuthenticationOptions());
        app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

        app.UseOpenIdConnectAuthentication(
            new OpenIdConnectAuthenticationOptions
            {
                // Generate hello metadata address using hello tenant and policy information
                MetadataAddress = String.Format(AadInstance, Tenant, DefaultPolicy),

                // These are standard OpenID Connect parameters, with values pulled from web.config
                ClientId = ClientId,
                RedirectUri = RedirectUri,
                PostLogoutRedirectUri = RedirectUri,

                // Specify hello callbacks for each type of notifications
                Notifications = new OpenIdConnectAuthenticationNotifications
                {
                    RedirectToIdentityProvider = OnRedirectToIdentityProvider,
                    AuthorizationCodeReceived = OnAuthorizationCodeReceived,
                    AuthenticationFailed = OnAuthenticationFailed,
                },

                // Specify hello claims toovalidate
                TokenValidationParameters = new TokenValidationParameters
                {
                    NameClaimType = "name"
                },

                // Specify hello scope by appending all of hello scopes requested into one string (seperated by a blank space)
                Scope = $"{OpenIdConnectScopes.OpenId} {ReadTasksScope} {WriteTasksScope}"
            }
        );
    }

    // Implement hello "Notification" methods...
}
```

`OpenIdConnectAuthenticationOptions` 위, hello OpenID Connect 미들웨어에서 수신 되는 특정 알림에 대 한 콜백 함수의 집합을 정의 합니다. 이러한 동작은 사용 하 여 정의 됩니다는 `OpenIdConnectAuthenticationNotifications` 개체 및 hello에 저장 된 `Notifications` 변수입니다. 이 예제에서는 세 가지 콜백이 hello 이벤트에 따라 정의 됩니다.

### <a name="using-different-policies"></a>다른 정책 사용

hello `RedirectToIdentityProvider` tooAzure AD B2C은 요청 될 때마다 알림이 트리거됩니다. Hello 콜백 함수에서 `OnRedirectToIdentityProvider`, 체크인 toouse 할까요 호출을 나가는 hello 다른 정책입니다. 순서 toodo 암호 다시 설정 또는 프로필을 편집할 hello 암호 재설정 정책 hello 기본 "등록 또는 로그인" 정책 대신 같은 toouse hello 해당 정책이 필요 합니다.

이 샘플에서는 사용자가 tooreset hello 암호 또는 hello 프로 파일을 편집 하는 경우에서는 추가 hello 정책 hello OWIN 컨텍스트로 toouse 것이 좋습니다. hello 다음을 수행 하 여 수행할 수 있습니다.

```CSharp
    // Let hello middleware know you are trying toouse hello edit profile policy
    HttpContext.GetOwinContext().Set("Policy", EditProfilePolicyId);
```

Hello 콜백 함수를 구현할 수 있습니다 및 `OnRedirectToIdentityProvider` hello 다음을 수행 하 여:

```CSharp
/*
*  On each call tooAzure AD B2C, check if a policy (e.g. hello profile edit or password reset policy) has been specified in hello OWIN context.
*  If so, use that policy when making hello call. Also, don't request a code (since it won't be needed).
*/
private Task OnRedirectToIdentityProvider(RedirectToIdentityProviderNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> notification)
{
    var policy = notification.OwinContext.Get<string>("Policy");

    if (!string.IsNullOrEmpty(policy) && !policy.Equals(DefaultPolicy))
    {
        notification.ProtocolMessage.Scope = OpenIdConnectScopes.OpenId;
        notification.ProtocolMessage.ResponseType = OpenIdConnectResponseTypes.IdToken;
        notification.ProtocolMessage.IssuerAddress = notification.ProtocolMessage.IssuerAddress.Replace(DefaultPolicy, policy);
    }

    return Task.FromResult(0);
}
```

### <a name="handling-authorization-codes"></a>권한 부여 코드 처리

hello `AuthorizationCodeReceived` 인증 코드를 받을 때 알림이 트리거됩니다. hello OpenID Connect 미들웨어 액세스 토큰에 대 한 교환 코드를 지원 하지 않습니다. 수동으로 hello 토큰에 콜백 함수에 대 한 hello 코드를 교환할 수 있습니다. 자세한 내용은 참조 하십시오 hello [설명서](active-directory-b2c-devquickstarts-web-api-dotnet.md) 설명 하는 방법입니다.

### <a name="handling-errors"></a>오류 처리

hello `AuthenticationFailed` 인증이 실패 한 경우 알림이 트리거됩니다. 해당 콜백 메서드를 원하는 대로 hello 오류를 처리할 수 있습니다. 그러나 추가할지를 묻는 hello 오류 코드에 대 한 확인 `AADB2C90118`합니다. "등록 또는 로그인" 정책 hello hello 실행 중 hello 사용자에 게 hello 기회 tooselect는 **암호를 잊으셨습니까?** 링크 합니다. 이 이벤트의 경우 Azure AD B2C는 응용 프로그램 응용 프로그램 대신 hello 암호 재설정 정책을 사용 하 여 요청을 수행 해야 해당 오류 코드가 나타내는 보냅니다.

```CSharp
/*
* Catch any failures received by hello authentication middleware and handle appropriately
*/
private Task OnAuthenticationFailed(AuthenticationFailedNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> notification)
{
    notification.HandleResponse();

    // Handle hello error code that Azure AD B2C throws when trying tooreset a password from hello login page
    // because password reset is not supported by a "sign-up or sign-in policy"
    if (notification.ProtocolMessage.ErrorDescription != null && notification.ProtocolMessage.ErrorDescription.Contains("AADB2C90118"))
    {
        // If hello user clicked hello reset password link, redirect toohello reset password route
        notification.Response.Redirect("/Account/ResetPassword");
    }
    else if (notification.Exception.Message == "access_denied")
    {
        notification.Response.Redirect("/");
    }
    else
    {
        notification.Response.Redirect("/Home/Error?message=" + notification.Exception.Message);
    }

    return Task.FromResult(0);
}
```

### <a name="send-authentication-requests-tooazure-ad"></a>인증 요청 tooAzure AD 보내기

이제 앱이 Azure AD B2C와 올바르게 구성 된 toocommunicate hello OpenID Connect 인증 프로토콜을 사용 하 여 합니다. OWIN 인증 메시지를 만들어, Azure AD B2C에서 토큰의 유효성 검사 및 사용자 세션을 유지 관리의 hello 세부 정보를 관리 합니다. 나머지 각 사용자의 흐름 tooinitiate입니다.

사용자가 선택할 때 **기호 위쪽/로그인**, **프로필 편집**, 또는 **암호 재설정** hello web app에서에 연결 된 hello 작업을 호출할 `Controllers\AccountController.cs`:

```CSharp
// Controllers\AccountController.cs

/*
*  Called when requesting toosign up or sign in
*/
public void SignUpSignIn()
{
    // Use hello default policy tooprocess hello sign up / sign in flow
    if (!Request.IsAuthenticated)
    {
        HttpContext.GetOwinContext().Authentication.Challenge();
        return;
    }

    Response.Redirect("/");
}

/*
*  Called when requesting tooedit a profile
*/
public void EditProfile()
{
    if (Request.IsAuthenticated)
    {
        // Let hello middleware know you are trying toouse hello edit profile policy (see OnRedirectToIdentityProvider in Startup.Auth.cs)
        HttpContext.GetOwinContext().Set("Policy", Startup.EditProfilePolicyId);

        // Set hello page tooredirect tooafter editing hello profile
        var authenticationProperties = new AuthenticationProperties { RedirectUri = "/" };
        HttpContext.GetOwinContext().Authentication.Challenge(authenticationProperties);

        return;
    }

    Response.Redirect("/");

}

/*
*  Called when requesting tooreset a password
*/
public void ResetPassword()
{
    // Let hello middleware know you are trying toouse hello reset password policy (see OnRedirectToIdentityProvider in Startup.Auth.cs)
    HttpContext.GetOwinContext().Set("Policy", Startup.ResetPasswordPolicyId);

    // Set hello page tooredirect tooafter changing passwords
    var authenticationProperties = new AuthenticationProperties { RedirectUri = "/" };
    HttpContext.GetOwinContext().Authentication.Challenge(authenticationProperties);

    return;
}
```

OWIN toosign hello 앱에서 사용자 hello out를 사용할 수 있습니다. `Controllers\AccountController.cs`에서 다음을 가집니다.

```CSharp
// Controllers\AccountController.cs

/*
*  Called when requesting toosign out
*/
public void SignOut()
{
    // toosign out hello user, you should issue an OpenIDConnect sign out request.
    if (Request.IsAuthenticated)
    {
        IEnumerable<AuthenticationDescription> authTypes = HttpContext.GetOwinContext().Authentication.GetAuthenticationTypes();
        HttpContext.GetOwinContext().Authentication.SignOut(authTypes.Select(t => t.AuthenticationType).ToArray());
        Request.GetOwinContext().Authentication.GetAuthenticationTypes();
    }
}
```

정책을 호출 또한 tooexplicitly를 사용할 수 있습니다는 `[Authorize]` hello 사용자가 로그인 되지 않은 경우 정책을 실행 하 여 컨트롤러에서 태그입니다. 열기 `Controllers\HomeController.cs` hello 추가 `[Authorize]` 태그 toohello 컨트롤러를 클레임 합니다.  Hello 마지막 정책 때 hello 구성를 선택 하는 OWIN `[Authorize]` 태그 적중 됩니다.

```CSharp
// Controllers\HomeController.cs

// You can use hello Authorize decorator tooexecute a certain policy if hello user is not already signed into hello app.
[Authorize]
public ActionResult Claims()
{
  ...
```

### <a name="display-user-information"></a>사용자 정보 표시

OpenID Connect를 사용 하 여 사용자를 인증 하는 경우 Azure AD B2C 반환을 포함 하는 ID 토큰 toohello 응용 프로그램 **클레임**합니다. 이들은 hello 사용자에 대 한 어설션입니다. 앱 클레임 toopersonalize를 사용할 수 있습니다.

열기 hello `Controllers\HomeController.cs` 파일입니다. 사용자 클레임 hello 통해 컨트롤러에 액세스할 수 있습니다 `ClaimsPrincipal.Current` 보안 주체 개체입니다.

```CSharp
// Controllers\HomeController.cs

[Authorize]
public ActionResult Claims()
{
    Claim displayName = ClaimsPrincipal.Current.FindFirst(ClaimsPrincipal.Current.Identities.First().NameClaimType);
    ViewBag.DisplayName = displayName != null ? displayName.Value : string.Empty;
    return View();
}
```

응용 프로그램 받는다고 hello에 동일한 클레임을 액세스할 수 방식으로 합니다.  Hello 앱 받는 모든 hello 클레임의 목록은 hello에 사용할 수 있습니다 **클레임** 페이지.

---
title: Active Directory B2C aaaAzure | Microsoft Docs
description: "어떻게 toobuild.NET 웹 응용 프로그램 web를 호출 하 고 Azure Active Directory B2C 및 OAuth 2.0 액세스 토큰을 사용 하 여 api입니다."
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: 
ms.assetid: d3888556-2647-4a42-b068-027f9374aa61
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/17/2017
ms.author: parakhj
ms.openlocfilehash: 9b248e3bf18968e12aae73c07083fa8278befb3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-call-a-net-web-api-from-a-net-web-app"></a>Azure AD B2C: .NET 웹앱에서 .NET 웹 API 호출

Azure AD B2C를 사용 하 여 강력한 id 관리 기능 tooyour 웹 앱 및 웹 Api 추가할 수 있습니다. 이 문서에서는 방법을 알아보고 toorequest 액세스 토큰 호출 "할 일 목록".NET에서 웹 앱 tooa.NET 웹 api입니다.

이 적용 되지 않습니다 어떻게 tooimplement 로그인 등록, Azure AD B2C를 사용 하 여 관리 프로필 및 합니다. Hello 사용자가 이미 인증 된 후 호출 웹 Api에 집중 합니다. 아직 하지 않은 경우 다음을 수행해야 합니다.

* [.NET 웹앱](active-directory-b2c-devquickstarts-web-dotnet-susi.md) 시작
* [.NET 웹 API](active-directory-b2c-devquickstarts-api-dotnet.md) 시작

## <a name="prerequisite"></a>필수 요소

toobuild web를 호출 하는 웹 응용 프로그램에 필요한 api:

1. [Azure AD B2C 테넌트를 만듭니다](active-directory-b2c-get-started.md).
2. [웹 API를 등록합니다](active-directory-b2c-app-registration.md#register-a-web-api).
3. [웹앱을 등록합니다](active-directory-b2c-app-registration.md#register-a-web-app).
4. [정책을 설정합니다](active-directory-b2c-reference-policies.md).
5. [Grant hello 웹 응용 프로그램 사용 권한 toouse hello 웹 api](active-directory-b2c-access-tokens.md#publishing-permissions)합니다.

> [!IMPORTANT]
> hello 클라이언트 응용 프로그램 및 web API hello 동일한 Azure AD B2C 디렉터리를 사용 해야 합니다.
>

## <a name="download-hello-code"></a>Hello 코드 다운로드

이 자습서에 대 한 hello 코드에서 유지 관리 됩니다 [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi)합니다. 실행 하 여 hello 샘플을 복제할 수 있습니다.

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

Hello 샘플 코드를 다운로드 한 후 hello open Visual Studio.sln 파일 tooget 시작 합니다. hello 솔루션 파일에는 두 개의 프로젝트가 포함 되어: `TaskWebApp` 및 `TaskService`합니다. `TaskWebApp`와 상호 작용 사용자 hello MVC 웹 응용 프로그램입니다. `TaskService`각 사용자의 할 일 목록에 저장 하는 hello 앱 백 엔드 웹 API입니다. 이 문서 작성 hello를 다루지 않습니다 `TaskWebApp` 웹 응용 프로그램 또는 hello `TaskService` 웹 api입니다. toolearn toobuild hello.NET 웹 응용 프로그램을 Azure AD B2C를 사용 하 여 참조 우리의 [.NET 웹 응용 프로그램 자습서](active-directory-b2c-devquickstarts-web-dotnet-susi.md)합니다. toolearn toobuild hello.NET web API Azure AD B2C를 사용 하 여 보안 하는 방법을 참조 우리의 [.NET web API 자습서](active-directory-b2c-devquickstarts-api-dotnet.md)합니다.

### <a name="update-hello-azure-ad-b2c-configuration"></a>Azure AD B2C hello 구성 업데이트

이 샘플은 구성 된 toouse hello 정책 및 클라이언트 ID 우리의 데모 테 넌 트입니다. Toouse 원하는 경우 자신의 테 넌 트:

1. 열기 `web.config` hello에 `TaskService` 프로젝트 및에 대 한 hello 값 바꾸기

    * `ida:Tenant`를 테넌트 이름으로 바꿉니다.
    * `ida:ClientId`를 웹 API 응용 프로그램 ID로 바꿉니다.
    * `ida:SignUpSignInPolicyId`를 "등록 또는 로그인" 정책 이름으로 바꿉니다.

2. 열기 `web.config` hello에 `TaskWebApp` 프로젝트 및에 대 한 hello 값 바꾸기

    * `ida:Tenant`를 테넌트 이름으로 바꿉니다.
    * `ida:ClientId`를 웹앱 응용 프로그램 ID로 바꿉니다.
    * `ida:ClientSecret`을 웹앱 비밀 키로 바꿉니다.
    * `ida:SignUpSignInPolicyId`를 "등록 또는 로그인" 정책 이름으로 바꿉니다.
    * `ida:EditProfilePolicyId`를 "프로필 편집" 정책 이름으로 바꿉니다.
    * `ida:ResetPasswordPolicyId`를 "암호 재설정" 정책 이름으로 바꿉니다.



## <a name="requesting-and-saving-an-access-token"></a>액세스 토큰 요청 및 저장

### <a name="specify-hello-permissions"></a>Hello 사용 권한을 지정합니다

순서 toomake hello 호출 toohello web API의 tooauthenticate hello 사용자 (로그-up/로그인 정책 사용)가 필요 하 고 [액세스 토큰을 받는](active-directory-b2c-access-tokens.md) Azure AD B2C에서 합니다. 순서 tooreceive 액세스 토큰에서에서 먼저 hello 액세스 토큰 toogrant 원하는 hello 사용 권한을 지정 해야 합니다. hello에 지정 된 hello 권한 `scope` hello 요청 toohello 확인 될 때 매개 변수 `/authorize` 끝점입니다. 예를 들어 hello로 액세스 토큰 "읽기" 권한 toohello 리소스 응용 프로그램을 tooacquire hello의 앱 ID URI `https://contoso.onmicrosoft.com/tasks`, hello 범위 것 `https://contoso.onmicrosoft.com/tasks/read`합니다.

샘플을 열고 hello 파일에서 toospecify hello 범위 `App_Start\Startup.Auth.cs` hello를 정의 하 고 `Scope` OpenIdConnectAuthenticationOptions에 변수입니다.

```CSharp
// App_Start\Startup.Auth.cs

    app.UseOpenIdConnectAuthentication(
        new OpenIdConnectAuthenticationOptions
        {
            ...

            // Specify hello scope by appending all of hello scopes requested into one string (seperated by a blank space)
            Scope = $"{OpenIdConnectScopes.OpenId} {ReadTasksScope} {WriteTasksScope}"
        }
    );
}
```

### <a name="exchange-hello-authorization-code-for-an-access-token"></a>액세스 토큰에 대 한 Exchange hello 인증 코드

Hello 등록 또는 로그인 환경을 사용자 인 완료 된 후 앱이 Azure AD B2C에서 인증 코드를 받습니다. hello OpenID Connect OWIN 미들웨어는 hello 코드를 저장 하지만 액세스 토큰에 대 한 교환 하지 않습니다. Hello를 사용할 수 있습니다 [MSAL 라이브러리](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) toomake hello 교환 합니다. 이 샘플에서는 구성 했습니다 알림 콜백을 hello OpenID Connect 미들웨어에 인증 코드를 받을 때마다. Hello 콜백에서는 MSAL tooexchange hello 코드를 사용 하 여 토큰에 대 하 고 hello 토큰 hello 캐시에 저장 합니다.

```CSharp
/*
* Callback function when an authorization code is received
*/
private async Task OnAuthorizationCodeReceived(AuthorizationCodeReceivedNotification notification)
{
    // Extract hello code from hello response notification
    var code = notification.Code;

    var userObjectId = notification.AuthenticationTicket.Identity.FindFirst(ObjectIdElement).Value;
    var authority = String.Format(AadInstance, Tenant, DefaultPolicy);
    var httpContext = notification.OwinContext.Environment["System.Web.HttpContextBase"] as HttpContextBase;

    // Exchange hello code for a token. Make sure toospecify hello necessary scopes
    ClientCredential cred = new ClientCredential(ClientSecret);
    ConfidentialClientApplication app = new ConfidentialClientApplication(authority, Startup.ClientId,
                                            RedirectUri, cred, new NaiveSessionCache(userObjectId, httpContext));
    var authResult = await app.AcquireTokenByAuthorizationCodeAsync(new string[] { ReadTasksScope, WriteTasksScope }, code, DefaultPolicy);
}
```

## <a name="calling-hello-web-api"></a>Hello 웹 API를 호출합니다.

이 섹션에서는 동안 toouse hello 토큰을 수신 하는 방법을 설명 로그-up/사용 하 여 로그인 Azure AD B2C 순서로 tooaccess hello 웹 API입니다.

### <a name="retrieve-hello-saved-token-in-hello-controllers"></a>Hello 컨트롤러에 저장 하는 hello 토큰을 가져옵니다.

hello `TasksController` hello web API와의 통신을 담당 하 고 HTTP 요청 toohello API tooread 전송용 만들고 작업을 삭제 합니다. Hello API, Azure AD B2C 하 여 보안 된 셀 이므로 toofirst 검색 hello 토큰 단계 위에 hello에 저장 해야 합니다.

```CSharp
// Controllers\TasksController.cs

/*
* Uses MSAL tooretrieve hello token from hello cache
*/
private async void acquireToken(String[] scope)
{
    string userObjectID = ClaimsPrincipal.Current.FindFirst(Startup.ObjectIdElement).Value;
    string authority = String.Format(Startup.AadInstance, Startup.Tenant, Startup.DefaultPolicy);

    ClientCredential credential = new ClientCredential(Startup.ClientSecret);

    // Retrieve hello token using hello provided scopes
    ConfidentialClientApplication app = new ConfidentialClientApplication(authority, Startup.ClientId,
                                        Startup.RedirectUri, credential,
                                        new NaiveSessionCache(userObjectID, this.HttpContext));
    AuthenticationResult result = await app.AcquireTokenSilentAsync(scope);

    accessToken = result.Token;
}
```

### <a name="read-tasks-from-hello-web-api"></a>Hello web API 로부터 작업 읽기

토큰을 사용 하는 경우 연결 toohello HTTP `GET` hello에 대 한 요청 `Authorization` 헤더 toosecurely 호출 `TaskService`:

```CSharp
// Controllers\TasksController.cs

public async Task<ActionResult> Index()
{
    try {

        // Retrieve hello token with hello specified scopes
        acquireToken(new string[] { Startup.ReadTasksScope });

        HttpClient client = new HttpClient();
        HttpRequestMessage request = new HttpRequestMessage(HttpMethod.Get, apiEndpoint);

        // Add token toohello Authorization header and make hello request
        request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", accessToken);
        HttpResponseMessage response = await client.SendAsync(request);

        // Handle response ...
}

```

### <a name="create-and-delete-tasks-on-hello-web-api"></a>만들기 및 hello 웹 API에서 작업 삭제

보낼 때 같은 패턴에 따라 hello `POST` 및 `DELETE` MSAL tooretrieve hello 액세스 토큰을 사용 하 여 hello 캐시에서 toohello 웹 API를 요청 합니다.

## <a name="run-hello-sample-app"></a>Hello 샘플 응용 프로그램 실행

마지막으로, 빌드 및 두 hello 앱을 실행 합니다. 등록 및 로그인 한 hello 로그인 한 사용자에 대 한 작업을 만듭니다. 로그아웃했다가 다른 사용자로 로그인합니다. 해당 사용자에 대한 작업을 만듭니다. 수신한 hello 토큰에서 hello 사용자의 id를 추출 하는 hello API 때문에 hello 작업 저장된 사용자별 hello API에는 하는 방법을 확인 합니다. 또한 hello 범위가 재생 해 봅니다. Hello 권한을 제거 너무 "쓰기" 및 다음 작업을 추가 해 보십시오. 단지 있는지 toosign을 hello 범위를 변경할 때마다 아웃 합니다.


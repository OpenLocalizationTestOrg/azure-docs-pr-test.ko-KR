---
title: AD B2C aaaAzure | Microsoft Docs
description: "Toobuild Azure Active Directory B2C를 사용 하 여.NET 웹 API 인증에 대 한 OAuth 2.0 액세스 토큰을 사용 하 여 보호 하는 방법"
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: 
ms.assetid: 7146ed7f-2eb5-49e9-8d8b-ea1a895e1966
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 03/17/2017
ms.author: parakhj
ms.openlocfilehash: d45364216deda38ef44b60dd11e86d9a089ad509
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-build-a-net-web-api"></a>Azure Active Directory B2C: .NET Web API 빌드

Azure AD(Azure Active Directory) B2C로 OAuth 2.0 액세스 토큰을 사용하여 Web API를 보호할 수 있습니다. 이러한 토큰을 사용 하 여 클라이언트 앱 tooauthenticate toohello API 있습니다. 이 문서에서는 어떻게 toocreate.NET MVC "할 일 목록" API를 허용 하 여 클라이언트의 사용자가 응용 프로그램 tooCRUD 작업 합니다. hello 웹 API는 Azure AD B2C를 사용 하 여 보안 처리 되며 toomanage 인증 된 사용자의 할 일 목록을 허용 합니다.

## <a name="create-an-azure-ad-b2c-directory"></a>Azure AD B2C 디렉터리 만들기

Azure AD B2C를 사용하기 전에 디렉터리 또는 테넌트를 만들어야 합니다. 디렉터리는 모든 사용자, 앱, 그룹 등을 위한 컨테이너입니다. 아직 없는 경우 [B2C 디렉터리를 만든](active-directory-b2c-get-started.md) 후에 이 가이드를 계속 진행합니다.

> [!NOTE]
> hello 클라이언트 응용 프로그램 및 web API hello 동일한 Azure AD B2C 디렉터리를 사용 해야 합니다.
>

## <a name="create-a-web-api"></a>Web API 만들기

다음으로, 웹 API 앱 toocreate B2C 디렉터리에 있어야합니다. Azure AD 정보가 필요한 toosecurely 통신할 수 있는지 응용 프로그램에 게 제공 합니다. 응용 프로그램, 프로그램 toocreate 따라 [이러한 지침](active-directory-b2c-app-registration.md)합니다. 다음을 수행해야 합니다.

* 포함 된 **웹 앱** 또는 **웹 API** hello 응용 프로그램에서 합니다.
* 사용 하 여 hello **리디렉션 URI** `https://localhost:44332/` hello 웹 앱에 대 한 합니다. 이 코드 샘플에 대 한 웹 앱 클라이언트 hello의 hello 기본 위치입니다.
* 복사 hello **응용 프로그램 ID** 할당된 tooyour 앱입니다. 나중에 필요합니다.
* 앱 식별자를 **앱 ID URI**에 입력합니다.
* Hello 통해 사용 권한을 추가 **범위 게시** 메뉴.

  [!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>정책 만들기

Azure AD B2C에서 모든 사용자 환경은 [정책](active-directory-b2c-reference-policies.md)에 의해 정의됩니다. Azure AD B2C와 정책 toocommunicate toocreate가 필요 합니다. 권장 로그-up/로그인 정책 결합 hello를 사용 하 여 hello에 설명 된 대로 [정책 참조 문서](active-directory-b2c-reference-policies.md)합니다. 정책을 만들 때 다음을 확인합니다.

* 정책에서 **표시 이름** 및 다른 등록 특성을 선택합니다.
* 모든 정책에 대한 응용 프로그램 클레임으로 **표시 이름** 및 **개체 ID** 클레임을 선택합니다. 물론 다른 클레임을 선택할 수 있습니다.
* 복사 hello **이름** 를 만든 후 각 정책의 합니다. Hello 정책 이름을 나중에 필요 합니다.

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

준비 toobuild 하는 hello 정책을 성공적으로 만든 후 응용 프로그램입니다.

## <a name="download-hello-code"></a>Hello 코드 다운로드

이 자습서에 대 한 hello 코드에서 유지 관리 됩니다 [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi)합니다. 실행 하 여 hello 샘플을 복제할 수 있습니다.

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

Hello 샘플 코드를 다운로드 한 후 hello open Visual Studio.sln 파일 tooget 시작 합니다. hello 솔루션 파일에는 두 개의 프로젝트가 포함 되어: `TaskWebApp` 및 `TaskService`합니다. `TaskWebApp`와 상호 작용 사용자 hello MVC 웹 응용 프로그램입니다. `TaskService`각 사용자의 할 일 목록에 저장 하는 hello 앱 백 엔드 웹 API입니다. 이 문서에서는 hello 설명만 `TaskService` 응용 프로그램입니다. toolearn 어떻게 toobuild `TaskWebApp` Azure AD B2C를 사용 하 여 참조 [이.NET 웹 응용 프로그램 자습서](active-directory-b2c-devquickstarts-web-dotnet-susi.md)합니다.

### <a name="update-hello-azure-ad-b2c-configuration"></a>Azure AD B2C hello 구성 업데이트

이 샘플은 구성 된 toouse hello 정책 및 클라이언트 ID 우리의 데모 테 넌 트입니다. Toouse 원하는 경우 고유한 테 넌 트 다음 toodo hello 필요 합니다.

1. 열기 `web.config` hello에 `TaskService` 프로젝트 및에 대 한 hello 값 바꾸기
    * `ida:Tenant`를 테넌트 이름으로 바꿉니다.
    * `ida:ClientId`을 Web API 응용 프로그램 ID로 바꿉니다.
    * `ida:SignUpSignInPolicyId`를 "등록 또는 로그인" 정책 이름으로 바꿉니다.

2. 열기 `web.config` hello에 `TaskWebApp` 프로젝트 및에 대 한 hello 값 바꾸기
    * `ida:Tenant`를 테넌트 이름으로 바꿉니다.
    * `ida:ClientId`를 웹앱 응용 프로그램 ID로 바꿉니다.
    * `ida:ClientSecret`을 웹앱 비밀 키로 바꿉니다.
    * `ida:SignUpSignInPolicyId`를 "등록 또는 로그인" 정책 이름으로 바꿉니다.
    * `ida:EditProfilePolicyId`를 "프로필 편집" 정책 이름으로 바꿉니다.
    * `ida:ResetPasswordPolicyId`를 "암호 재설정" 정책 이름으로 바꿉니다.


## <a name="secure-hello-api"></a>Hello API 보호

API를 호출하는 클라이언트가 있는 경우 OAuth 2.0 전달자 토큰을 사용하여 API(예: `TaskService`)를 보호할 수 있습니다. 이렇게 하면 각 요청 tooyour API만 되도록 hello 요청은 전달자 토큰을 하는 경우에 유효 합니다. API는 Microsoft OWIN(Open Web Interface for .NET)을 사용하여 전달자 토큰을 허용하고 유효성을 검사할 수 있습니다.

### <a name="install-owin"></a>OWIN 설치

Hello OWIN OAuth 인증 파이프라인 hello Visual Studio 패키지 관리자 콘솔을 사용 하 여 설치 하 여 시작 합니다.

```Console
PM> Install-Package Microsoft.Owin.Security.OAuth -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Security.Jwt -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TaskService
```

그러면 hello OWIN 미들웨어 있고 전달자 토큰의 유효성을 검사 되도록 설치 됩니다.

### <a name="add-an-owin-startup-class"></a>OWIN 시작 클래스 추가

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

### <a name="configure-oauth-20-authentication"></a>OAuth 2.0 인증 구성

파일 열기 hello `App_Start\Startup.Auth.cs`, 고 hello 구현 `ConfigureAuth(...)` 메서드. 예를 들어 것 hello 다음과 같을 수 있습니다.

```CSharp
// App_Start\Startup.Auth.cs

 public partial class Startup
    {
        // These values are pulled from web.config
        public static string AadInstance = ConfigurationManager.AppSettings["ida:AadInstance"];
        public static string Tenant = ConfigurationManager.AppSettings["ida:Tenant"];
        public static string ClientId = ConfigurationManager.AppSettings["ida:ClientId"];
        public static string SignUpSignInPolicy = ConfigurationManager.AppSettings["ida:SignUpSignInPolicyId"];
        public static string DefaultPolicy = SignUpSignInPolicy;

        /*
         * Configure hello authorization OWIN middleware.
         */
        public void ConfigureAuth(IAppBuilder app)
        {
            TokenValidationParameters tvps = new TokenValidationParameters
            {
                // Accept only those tokens where hello audience of hello token is equal toohello client ID of this app
                ValidAudience = ClientId,
                AuthenticationType = Startup.DefaultPolicy
            };

            app.UseOAuthBearerAuthentication(new OAuthBearerAuthenticationOptions
            {
                // This SecurityTokenProvider fetches hello Azure AD B2C metadata & signing keys from hello OpenIDConnect metadata endpoint
                AccessTokenFormat = new JwtFormat(tvps, new OpenIdConnectCachingSecurityTokenProvider(String.Format(AadInstance, Tenant, DefaultPolicy)))
            });
        }
    }
```

### <a name="secure-hello-task-controller"></a>보안 hello 작업 컨트롤러

Hello 앱 구성된 toouse OAuth 2.0 인증을 추가 하 여 web API를 보호할 수 있습니다는 `[Authorize]` 태그 toohello 작업 컨트롤러입니다. 모든 할 일 목록 조작 발생, hello 전체 컨트롤러 hello 클래스 수준에서 보안을 설정 해야 하므로 hello 컨트롤러입니다. Hello를 추가할 수도 있습니다 `[Authorize]` 보다 세부적으로 제어에 대 한 tooindividual 작업 태그를 지정 합니다.

```CSharp
// Controllers\TasksController.cs

[Authorize]
public class TasksController : ApiController
{
    ...
}
```

### <a name="get-user-information-from-hello-token"></a>사용자 정보 hello에서 토큰 가져오기

`TasksController`각 작업에 "소유" hello 작업 하 고 연결된 된 사용자 데이터베이스에서 작업을 저장 합니다. hello 소유자 hello 사용자로 식별 되 **개체 ID**합니다. (이 때문에 응용 프로그램으로 tooadd hello 개체 ID를 필요한 모든 정책에서 클레임입니다.)

```CSharp
// Controllers\TasksController.cs

public IEnumerable<Models.Task> Get()
{
    string owner = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
    IEnumerable<Models.Task> userTasks = db.Tasks.Where(t => t.owner == owner);
    return userTasks;
}
```

### <a name="validate-hello-permissions-in-hello-token"></a>Hello 권한을 hello 토큰의 유효성 검사

웹 Api에 대 한 일반적인 요구 사항은 toovalidate hello "범위" hello 토큰에 있는입니다. 이렇게 하면 해당 hello 사용자가 동의 toohello 권한이 필요한 tooaccess hello 할 일 목록 서비스.

```CSharp
public IEnumerable<Models.Task> Get()
{
    if (ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/scope").Value != "read")
    {
        throw new HttpResponseException(new HttpResponseMessage {
            StatusCode = HttpStatusCode.Unauthorized,
            ReasonPhrase = "hello Scope claim does not contain 'read' or scope claim not found"
        });
    }
    ...
}
```

## <a name="run-hello-sample-app"></a>Hello 샘플 응용 프로그램 실행

마지막으로 `TaskWebApp`과 `TaskService`를 모두 빌드하고 실행합니다. Hello 사용자의 할 일 목록에서 몇 가지 작업을 만들고 어떻게 유지 하기 hello API에서에서 중지 하 고 hello 클라이언트를 다시 시작 후에 확인 합니다.

## <a name="edit-your-policies"></a>청책 편집

Azure AD B2C를 사용 하 여 API을 확보 한 후 사용자 로그인-에/등록 정책 및 hello 효과 보기 (또는 결핍) hello API에를 테스트할 수 있습니다. Hello 정책에서 응용 프로그램 클레임 hello를 조작 하 고 hello web API에서에서 제공 하는 hello 사용자 정보를 변경할 수 있습니다. 추가 하는 모든 클레임을 사용할 수 있는 tooyour.NET MVC 웹 API hello 수 `ClaimsPrincipal` 이 문서의 앞부분에 설명 된 대로 개체입니다.

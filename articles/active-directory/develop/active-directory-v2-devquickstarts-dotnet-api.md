---
title: "Azure AD v2.0 끝점 hello aaaAdd 로그인 tooa.NET MVC 웹 API를 사용 하 여 | Microsoft Docs"
description: "어떻게 toobuild 회사 또는 학교 계정 및 두 개인 Microsoft 계정에서 보낸 토큰을 허용 하는.NET MVC 웹 Api입니다."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: e77bc4e0-d0c9-4075-a3f6-769e2c810206
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 4e517145422bb6e9368e82a7eef4a5c57cce530a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-an-mvc-web-api"></a>MVC 웹 API 보안 유지
사용 하 여 웹 API 보호 하려면 Azure Active Directory hello v2.0 끝점과 [OAuth 2.0](active-directory-v2-protocols.md) 액세스 토큰을 두 개인 Microsoft 계정 가진 사용자 및 toosecurely 웹 API에 액세스 하는 회사 또는 학교 계정을 사용 하도록 설정 합니다.

> [!NOTE]
> 모든 Azure Active Directory 시나리오 및 기능 hello v2.0 끝점에서 사용할 수 있습니다.  에 대해 알아보세요 hello v2.0 끝점을 사용 해야 하는 경우 toodetermine [v2.0 제한](active-directory-v2-limitations.md)합니다.
>
>

ASP.NET Web API에서는 .NET Framework 4.5에 포함된 Microsoft OWIN 미들웨어를 사용하여 이 작업을 수행할 수 있습니다.  여기에서는 OWIN toobuild toocreate 이며 읽기 작업을 사용자의 할 일 목록 클라이언트를 허용 하는 "tooDo 목록" MVC 웹 API를 사용 합니다.  hello web API는 들어오는 요청을 유효한 액세스 토큰을 포함 하 고 보호 된 경로에 유효성 검사를 통과 하지 못한 모든 요청을 거부 확인 합니다.  이 샘플은 Visual Studio 2015를 사용하여 구축되었습니다.

## <a name="download"></a>다운로드
이 자습서에 대 한 hello 코드 유지 관리 [GitHub에서](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet)합니다.  수에 따라 toofollow, [.zip으로 hello 응용 프로그램의 기본 정의 다운로드](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) 또는 복제 hello 스 켈 레 톤:

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git
```

hello 뼈대 앱 간단한 API에 대 한 모든 hello 상용구 코드를 포함 하지만 모든 hello id 관련 조각을 없습니다. 대신 복제할 수 toofollow와 함께 사용 하지 않으려는 경우 또는 [완료 hello 샘플 다운로드](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip)합니다.

```
git clone https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git
```

## <a name="register-an-app"></a>앱 등록
[apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)에서 새 앱을 만들거나 다음 [세부 단계](active-directory-v2-app-registration.md)를 따릅니다.  다음을 수행해야 합니다.

* Hello 아래로 복사 **응용 프로그램 Id** tooyour 응용 프로그램에 할당 해야 곧 합니다.

또한 이 visual studio 솔루션에는 간단한 WPF 앱인 "TodoListClient"가 포함되어 있습니다.  hello TodoListClient 방법을 사용자가 로그인에 사용 되는 toodemonstrate 이며 tooyour 웹 API 요청 방법을 클라이언트를 실행할 수 있습니다.  이 경우 둘 다 TodoListClient hello와 hello TodoListService 표현 된 hello 동일한 응용 프로그램입니다.  tooconfigure TodoListClient hello, 또한 해야 합니다.

* Hello 추가 **모바일** 응용 프로그램을 위한 플랫폼입니다.

## <a name="install-owin"></a>OWIN 설치
응용 프로그램을 등록 한 사용자 앱 toocommunicate 순서 toovalidate 들어오는 요청 및 토큰에 대 한 hello v2.0 끝점과 tooset이 필요한 합니다.

* toobegin, hello 솔루션을 열고 hello OWIN 미들웨어 NuGet 패키지 toohello TodoListService 프로젝트 hello 패키지 관리자 콘솔을 사용 하 여 추가 합니다.

```
PM> Install-Package Microsoft.Owin.Security.OAuth -ProjectName TodoListService
PM> Install-Package Microsoft.Owin.Security.Jwt -ProjectName TodoListService
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoListService
PM> Install-Package Microsoft.IdentityModel.Protocol.Extensions -ProjectName TodoListService
```

## <a name="configure-oauth-authentication"></a>OAuth 인증 구성
* OWIN 시작 클래스 toohello TodoListService 프로젝트 라는 추가 `Startup.cs`합니다.  Hello 프로젝트에서 마우스 오른쪽 단추로 클릭--> **추가** --> **새 항목** "OWIN"에 대 한 검색--> 합니다.  hello OWIN 미들웨어는 hello를 호출 하는 `Configuration(…)` 메서드 앱이 시작 되는 경우.
* Hello 클래스 선언에도 변경`public partial class Startup` -이미 구현 했습니다이 클래스의 일부를 다른 파일에 있습니다.  Hello에 `Configuration(…)` 메서드는 호출 tooConfgureAuth(...) tooset 웹 앱에 대 한 인증을 확인 합니다.

```C#
public partial class Startup
{
    public void Configuration(IAppBuilder app)
    {
        ConfigureAuth(app);
    }
}
```

* 파일 열기 hello `App_Start\Startup.Auth.cs` hello를 구현 하 고 `ConfigureAuth(…)` 메서드 hello v2.0 끝점에서 hello 웹 API tooaccept 토큰을 설정 합니다.

```C#
public void ConfigureAuth(IAppBuilder app)
{
        var tvps = new TokenValidationParameters
        {
                // In this app, hello TodoListClient and TodoListService
                // are represented using hello same Application Id - we use
                // hello Application Id toorepresent hello audience, or the
                // intended recipient of tokens.

                ValidAudience = clientId,

                // In a real applicaiton, you might use issuer validation to
                // verify that hello user's organization (if applicable) has
                // signed up for hello app.  Here, we'll just turn it off.

                ValidateIssuer = false,
        };

        // Set up hello OWIN pipeline toouse OAuth 2.0 Bearer authentication.
        // hello options provided here tell hello middleware about hello type of tokens
        // that will be recieved, which are JWTs for hello v2.0 endpoint.

        // NOTE: hello usual WindowsAzureActiveDirectoryBearerAuthenticaitonMiddleware uses a
        // metadata endpoint which is not supported by hello v2.0 endpoint.  Instead, this
        // OpenIdConenctCachingSecurityTokenProvider can be used toofetch & use hello OpenIdConnect
        // metadata document.

        app.UseOAuthBearerAuthentication(new OAuthBearerAuthenticationOptions
        {
                AccessTokenFormat = new Microsoft.Owin.Security.Jwt.JwtFormat(tvps, new OpenIdConnectCachingSecurityTokenProvider("https://login.microsoftonline.com/common/v2.0/.well-known/openid-configuration")),
        });
}
```

* 에서는 이제 `[Authorize]` tooprotect 특성을 컨트롤러 및 OAuth 2.0 전달자 인증을 사용 하 여 작업 합니다.  Hello 데코레이팅 `Controllers\TodoListController.cs` authorize 태그를 사용 하 여 클래스입니다.  이렇게 하면 해당 페이지에 액세스 하기 전에 hello 사용자 toosign에서 시작 합니다.

```C#
[Authorize]
public class TodoListController : ApiController
{
```

* 하면 권한 있는 발신자를 성공적으로 중 하나를 호출 hello `TodoListController` Api hello 작업 해야에 액세스할 수 tooinformation hello 호출자에 대 한 합니다.  OWIN hello 통해 hello 전달자 토큰에 대 한 액세스 toohello 클레임을 제공 `ClaimsPrincpal` 개체입니다.  

```C#
public IEnumerable<TodoItem> Get()
{
    // You can use hello ClaimsPrincipal tooaccess information about the
    // user making hello call.  In this case, we use hello 'sub' or
    // NameIdentifier claim tooserve as a key for hello tasks in hello data store.

    Claim subject = ClaimsPrincipal.Current.FindFirst(ClaimTypes.NameIdentifier);

    return from todo in todoBag
           where todo.Owner == subject.Value
           select todo;
}
```

* 마지막으로 hello를 열고 `web.config` hello TodoListService 프로젝트의 hello 루트에서 파일을 hello에 구성 값을 입력 `<appSettings>` 섹션.
  * 프로그램 `ida:Audience` 는 hello **응용 프로그램 Id** hello 포털에 입력 한 hello 앱입니다.

## <a name="configure-hello-client-app"></a>Hello 클라이언트 응용 프로그램 구성
작업에 할 일 목록 서비스 hello 볼 수 있듯이 먼저 tooconfigure hello 할 일 목록 클라이언트 hello v2.0 끝점에서 토큰을 가져올 고 toohello 서비스 호출을 높일 수 있도록 합니다.

* Hello TodoListClient 프로젝트를 열고 `App.config` hello에 구성 값을 입력 하 고 `<appSettings>` 섹션.
  * 프로그램 `ida:ClientId` hello 포털에서 복사 하는 응용 프로그램 Id입니다.

마지막으로, 각 프로젝트를 정리하고 빌드한 후 실행합니다.  이제 개인 Microsoft 계정과 회사 또는 학교 계정 둘 다의 토큰을 허용하는 .NET MVC Web API가 있습니다.  Hello TodoListClient에 로그인 하 고 웹 api tooadd 작업 toohello 사용자의 할 일 목록을 호출 합니다.

참조용으로 hello 구성 값) (없이 샘플을 완료 [.zip을 여기로 제공 됩니다](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip), 또는 GitHub에서 복제할 수 있습니다.

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git```

## <a name="next-steps"></a>다음 단계
이제 추가 항목으로 이동할 수 있습니다.  Tootry를 사용할 수 있습니다.

[웹앱에서 웹 API 호출 >>](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md)

추가 리소스는 다음을 확인해보세요.

* [hello v2.0 개발자 가이드 >>](active-directory-appmodel-v2-overview.md)
* [StackOverflow "azure-active-directory" 태그 >>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a>당사 제품에 대한 보안 업데이트 가져오기
보안 사고를 방문 하 여 발생 하는 경우의 알림 tooget 좋습니다 [이 페이지](https://technet.microsoft.com/security/dd252948) 및 tooSecurity 자문 경고를 구독 합니다.

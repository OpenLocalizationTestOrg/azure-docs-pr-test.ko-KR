---
title: "aaaAzure AD.NET 웹 API 시작 | Microsoft Docs"
description: "어떻게 toobuild.NET MVC 웹 API는 Azure AD와 통합 인증 및 권한 부여에 대 한 합니다."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 67e74774-1748-43ea-8130-55275a18320f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 91c93e1fe18855f5648076e59e2ccf081eec34bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="help-protect-a-web-api-by-using-bearer-tokens-from-azure-ad"></a>Azure AD에서 전달자 토큰을 사용하여 Web API 보호
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Tooknow 필요한 tooprotected 리소스 액세스를 제공 하는 응용 프로그램을 빌드하는 경우 어떻게 tooprevent 초래 toothose 리소스에 액세스 합니다.
Azure Active Directory (Azure AD)을 사용 하면 간단 하 고 간단 하 게 toohelp 단 몇 줄의 코드 함께 OAuth 2.0 전달자 액세스 토큰을 사용 하 여 web API를 보호 합니다.

ASP.NET 웹 응용 프로그램에서 hello 커뮤니티 기반 OWIN 미들웨어의.NET Framework 4.5에 포함 된 Microsoft 구현 hello를 사용 하 여이 보호를 수행할 수 있습니다. 여기에서는 "tooDo 목록" web API OWIN toobuild입니다.

* 보호되는 API를 지정합니다.
* Hello 웹 API 호출에 유효한 액세스 토큰이 포함 유효성을 검사 합니다.

toobuild hello tooDo 목록 API를 먼저 하도록 설정 해야 합니다.

1. Azure AD에 응용 프로그램을 등록합니다.
2. Hello 앱 toouse hello OWIN 인증 파이프라인을 설정 합니다.
3. 클라이언트 응용 프로그램 toocall hello 웹 API를 구성 합니다.

시작 tooget [hello 응용 프로그램의 기본 정의 다운로드](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/skeleton.zip) 또는 [완료 hello 샘플 다운로드](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip)합니다. 각 샘플은 Visual Studio 2013 솔루션입니다. 또한 해야 어떤 tooregister에 Azure AD 테 넌 트 응용 프로그램입니다. 없는 경우 하나 이미 [자세한 방법을 하나 tooget](active-directory-howto-tenant.md)합니다.

## <a name="step-1-register-an-application-with-azure-ad"></a>1단계: Azure AD에 응용 프로그램 등록
toohelp secure 응용 프로그램에 먼저 테 넌 트에 응용 프로그램 toocreate 필요 하 고 Azure AD 몇 가지 중요 한 내용을 제공 합니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.

2. Hello 위쪽 막대에서 계정을 클릭 합니다. Hello에 **디렉터리** 목록 tooregister 원하는 hello Azure AD 테 넌 트 응용 프로그램을 선택 합니다.

3. 클릭 **더 서비스** 에 hello 왼쪽된 창에서 선택한 후 **Azure Active Directory**합니다.

4. **앱 등록**을 클릭하고 **추가**를 선택합니다.

5. Hello 화면에 따라 수행 하 고 새 **웹 응용 프로그램 및/또는 Web API**합니다.
  * **이름** 응용 프로그램 toousers에 설명 합니다. 입력 **tooDo 목록 서비스**합니다.
  * **리디렉션 Uri** 는 구성표 및 문자열 조합 tooreturn 응용 프로그램을 요청 했습니다 모든 토큰을 사용 하 여 Azure AD입니다. 이 값으로 `https://localhost:44321/` 을 입력합니다.

6. Hello에서 **설정** -> **속성** 응용 프로그램에 대 한 페이지를 hello 앱 ID URI를 업데이트 합니다. 테넌트별 식별자를 입력합니다. 예를 들어 `https://contoso.onmicrosoft.com/TodoListService`을 입력합니다.

7. Hello 구성을 저장 합니다. 또한 필요 하므로 tooregister 클라이언트 응용 프로그램이 곧 hello 포털을 열어를 둡니다.

## <a name="step-2-set-up-hello-app-toouse-hello-owin-authentication-pipeline"></a>2 단계: hello 앱 toouse hello OWIN 인증 파이프라인 설정
toovalidate 들어오는 요청 및 토큰을 Azure AD와 응용 프로그램 toocommunicate 프로그램 tooset이 필요 합니다.

1. toobegin, hello 솔루션을 열고 hello 패키지 관리자 콘솔을 사용 하 여 hello OWIN 미들웨어 NuGet 패키지 toohello TodoListService 프로젝트를 추가 합니다.

    ```
    PM> Install-Package Microsoft.Owin.Security.ActiveDirectory -ProjectName TodoListService
    PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoListService
    ```

2. OWIN 시작 클래스 toohello TodoListService 프로젝트 라는 추가 `Startup.cs`합니다.  마우스 오른쪽 단추로 클릭 hello 프로젝트를 선택 **추가** > **새 항목**, 검색할 **OWIN**합니다. hello OWIN 미들웨어는 hello를 호출 하는 `Configuration(…)` 메서드 앱이 시작 되는 경우.

3. Hello 클래스 선언에도 변경`public partial class Startup`합니다. 다른 파일에서 이 클래스의 일부를 이미 구현했습니다. Hello에 `Configuration(…)` 메서드를 너무 호출할`ConfgureAuth(…)` tooset 웹 앱에 대 한 인증을 합니다.

    ```C#
    public partial class Startup
    {
        public void Configuration(IAppBuilder app)
        {
            ConfigureAuth(app);
        }
    }
    ```

4. 파일 열기 hello `App_Start\Startup.Auth.cs` hello를 구현 하 고 `ConfigureAuth(…)` 메서드. 매개 변수에서 제공 하는 hello `WindowsAzureActiveDirectoryBearerAuthenticationOptions` 좌표 Azure AD와 앱 toocommunicate 프로그램에 대 한 역할을 수행 합니다.

    ```C#
    public void ConfigureAuth(IAppBuilder app)
    {
        app.UseWindowsAzureActiveDirectoryBearerAuthentication(
            new WindowsAzureActiveDirectoryBearerAuthenticationOptions
            {
                Audience = ConfigurationManager.AppSettings["ida:Audience"],
                Tenant = ConfigurationManager.AppSettings["ida:Tenant"]
            });
    }
    ```

5. 에서는 이제 `[Authorize]` 특성 toohelp 컨트롤러와 JSON 웹 토큰 (JWT) 전달자 인증을 사용 하 여 작업을 보호 합니다. Hello 데코레이팅 `Controllers\TodoListController.cs` authorize 태그를 사용 하 여 클래스입니다. 이렇게 하면 해당 페이지에 액세스 하기 전에 hello 사용자 toosign에서 시작 합니다.

    ```C#
    [Authorize]
    public class TodoListController : ApiController
    {
    ```

    하면 권한 있는 발신자를 성공적으로 중 하나를 호출 hello `TodoListController` Api hello 작업 해야에 액세스할 수 tooinformation hello 호출자에 대 한 합니다. OWIN hello 통해 hello 전달자 토큰에 대 한 액세스 toohello 클레임을 제공 `ClaimsPrincpal` 개체입니다.  

6. 웹 Api에 대 한 일반적인 요구 사항은 toovalidate hello "범위" hello 토큰에 있는입니다. 이렇게 하면 해당 hello 사용자가 동의 toohello 권한이 필요한 tooaccess hello tooDo 목록 서비스.

    ```C#
    public IEnumerable<TodoItem> Get()
    {
        // user_impersonation is hello default permission exposed by applications in Azure AD
        if (ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/scope").Value != "user_impersonation")
        {
            throw new HttpResponseException(new HttpResponseMessage {
              StatusCode = HttpStatusCode.Unauthorized,
              ReasonPhrase = "hello Scope claim does not contain 'user_impersonation' or scope claim not found"
            });
        }
        ...
    }
    ```

7. 열기 hello `web.config` hello TodoListService 프로젝트의 hello 루트에서 파일을 hello에 구성 값을 입력 `<appSettings>` 섹션.
  * `ida:Tenant`Azure AD 테 넌 트-예를 들어 contoso.onmicrosoft.com hello 이름이입니다.
  * `ida:Audience`hello hello Azure 포털에에서 입력 된 hello 응용 프로그램의 앱 ID URI입니다.

## <a name="step-3-configure-a-client-application-and-run-hello-service"></a>3 단계: 클라이언트 응용 프로그램을 구성 하 고 hello 서비스 실행
Hello tooDo 목록 서비스 실행에서 하기 전에 Azure AD에서 토큰을 가져오기 고 toohello 서비스 호출을 높일 수 있도록 tooconfigure hello tooDo 목록 클라이언트가 필요 합니다.

1. Toohello 돌아가서 [Azure 포털](https://portal.azure.com)합니다.

2. Azure AD 테 넌 트에 새 응용 프로그램을 만들고 선택 **네이티브 클라이언트 응용 프로그램** hello 프롬프트에 있습니다.
  * **이름** 응용 프로그램 toousers에 설명 합니다.
  * 입력 `http://TodoListClient/` hello에 대 한 **리디렉션 Uri** 값입니다.

3. 등록을 완료 한 후 Azure AD는 고유한 응용 프로그램 ID tooyour 응용 프로그램에 할당 합니다. 이 값이 필요 합니다 hello 다음 단계에서 하므로에서 복사 hello 응용 프로그램 페이지.

4. Hello에서 **설정** 페이지에서 **필요한 권한**를 선택한 후 **추가**합니다. 찾기 및 hello tooDo 목록 서비스를 선택, 추가 hello **액세스 TodoListService** 에 따른 권한 **위임 된 권한**, 클릭 하 고 **수행**합니다.

5. Visual Studio에서 열고 `App.config` 에 hello TodoListClient 프로젝트를 선택한 다음 hello에 구성 값을 입력 `<appSettings>` 섹션.

  * `ida:Tenant`Azure AD 테 넌 트-예를 들어 contoso.onmicrosoft.com hello 이름이입니다.
  * `ida:ClientId`hello Azure 포털에서에서 복사한 hello 응용 프로그램 ID입니다.
  * `todo:TodoListResourceId`hello hello tooDo hello Azure 포털에에서 입력 된 목록 서비스 응용 프로그램의 앱 ID URI입니다.

## <a name="next-steps"></a>다음 단계
마지막으로, 각 프로젝트를 정리하고 빌드한 후 실행합니다. 아직 하지 않는 경우 이제는 hello 시간 toocreate와 테 넌 트에 새 사용자는 *. onmicrosoft.com 도메인입니다. 해당 사용자와 toohello tooDo 목록 클라이언트에 로그인 하 고 일부 작업 toohello 사용자의 할 일 목록에 추가 합니다.

구성 값) (없이 hello 완료 샘플은에서 사용할 수 있는 참조를 위해 [GitHub](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip)합니다. 이제 toomore id 시나리오에서 이동할 수 있습니다.

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

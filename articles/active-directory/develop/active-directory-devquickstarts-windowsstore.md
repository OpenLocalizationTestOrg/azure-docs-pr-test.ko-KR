---
title: "aaaAzure AD Windows 스토어를 시작 | Microsoft Docs"
description: "로그인을 위해 Azure AD와 통합되고 OAuth를 사용하여 Azure AD로 보호되는 API를 호출하는 Windows 스토어 앱을 빌드합니다."
services: active-directory
documentationcenter: windows
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 3b96a6d1-270b-4ac1-b9b5-58070c896a68
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 09/16/2016
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 1d12c7b928bc0e94fb823f8db4a09ff416205e2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-windows-store-apps"></a>Azure AD와 Windows 스토어 앱 통합
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

> [!NOTE]
> Windows Store 8.1 및 이전 버전 프로젝트는 Visual Studio 2017에서 지원되지 않습니다.  자세한 내용은 [Visual Studio 2017 플랫폼 대상 지정 및 호환성](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs)을 참조하세요.

Hello Windows 스토어 용 앱을 개발 하는 경우 Azure Active Directory (Azure AD) 사용 하면 쉽고 간단 tooauthenticate 사용자의 Active Directory 계정 사용 합니다. Azure AD와 통합 하 여 응용 프로그램 웹 hello Office 365 Api 또는 hello Azure API와 같은 Azure AD로 보호 되는 API를 안전 하 게 사용할 수 있습니다.

Windows 스토어 데스크톱 응용 프로그램의 tooaccess 보호 된 리소스를 필요로 하는 경우 Azure AD hello Active Directory 인증 라이브러리 (ADAL)를 제공 합니다. hello ADAL의 목적으로 toomake hello 앱 tooget 액세스 토큰을 쉽게 합니다. toodemonstrate 얼마나 쉬운지 이면이 문서에서는 어떻게 toobuild DirectorySearcher Windows 저장 응용 프로그램입니다.

* 가져옵니다 액세스 hello를 사용 하 여 hello Azure AD Graph API를 호출 하기 위한 토큰 [OAuth 2.0 인증 프로토콜](https://msdn.microsoft.com/library/azure/dn645545.aspx)합니다.
* 지정된 UPN(사용자 계정 이름)을 가진 사용자를 디렉터리에서 검색합니다.
* 사용자를 로그아웃합니다.

## <a name="before-you-get-started"></a>시작하기 전에
* Hello 다운로드 [기초 프로젝트](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/skeleton.zip), hello 다운로드 또는 [완성 된 샘플](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip)합니다. 각 다운로드는 Visual Studio 2015 솔루션입니다.
* Toocreate 사용자 및 레지스터 hello 앱에서 Azure AD 테 넌 트가 있어야합니다. 테 넌 트 아직 없는 경우 [자세한 방법을 하나 tooget](active-directory-howto-tenant.md)합니다.

준비 되 면 다음 절차에 따라 hello hello 다음 3 개의 섹션.

## <a name="step-1-register-hello-directorysearcher-app"></a>1 단계: hello DirectorySearcher 앱 등록
tooenable hello 앱 tooget 토큰 먼저 tooregister에서 Azure AD 테 넌 트 및 사용 권한 tooaccess hello Azure AD Graph API에 부여 합니다. 방법은 다음과 같습니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. Hello 위쪽 막대에서 계정을 클릭 합니다. 그런 다음 hello **디렉터리** 목록, 선택 hello Active Directory 테 넌 트 tooregister hello 앱을 원하는 합니다.
3. 클릭 **더 서비스** 에 hello 왼쪽된 창에서 선택한 후 **Azure Active Directory**합니다.
4. **앱 등록**을 클릭하고 **추가**를 선택합니다.
5. Hello 프롬프트 toocreate에 따라 한 **네이티브 클라이언트 응용 프로그램**합니다.
  * **이름** hello 앱 toousers에 설명 합니다.
  * **리디렉션 URI** Azure AD에서는 tooreturn 토큰 응답 체계 및 문자열 조합입니다. 이제 자리 표시자 값(예: **http://DirectorySearcher**)을 입력합니다. 나중에 hello 값을 대체 합니다.
6. Azure AD를 hello 등록을 완료 한 후 hello 앱 고유한 응용 프로그램 ID를 할당 Hello에 hello 값 복사 **응용 프로그램** 탭, 나중에 필요 합니다.
7. Hello에 **설정** 페이지에서 **필요한 권한**를 선택한 후 **추가**합니다.
8. Hello에 대 한 **Azure Active Directory** 앱을 **Microsoft Graph** API hello으로 합니다.
9. 아래 **위임 된 권한**, hello 추가 **hello 로그인 한 사용자로 디렉터리에 액세스 hello** 권한. 이렇게 하면 특정 사용자에 대 한 hello 앱 tooquery hello Graph API입니다.

## <a name="step-2-install-and-configure-adal"></a>2단계: ADAL 설치 및 구성
Azure AD에 앱이 있으므로 ADAL을 설치하고 ID 관련 코드를 작성할 수 있습니다. Azure AD와 tooenable ADAL toocommunicate hello 앱 등록에 대 한 정보를 지정 합니다.

1. Hello 패키지 관리자 콘솔을 사용 하 여 ADAL toohello DirectorySearcher 프로젝트를 추가 합니다.

    ```
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
    ```

2. Hello DirectorySearcher 프로젝트에서 MainPage.xaml.cs를 엽니다.
3. Hello hello 값을 교체 **구성 값** hello Azure 포털에에서 입력 hello 값을 사용 하 여 영역입니다. ADAL를 사용 하 여 때마다 코드 toothese 값을 참조 합니다.
  * hello *테 넌 트* 여 Azure AD 테 넌 트 (예: contoso.onmicrosoft.com) hello 도메인입니다.
  * hello *clientId* hello 포털에서 복사 된 hello 앱으로의 hello 클라이언트 ID입니다.
4. 이제 Windows 스토어 앱에 대 한 toodiscover hello 콜백 URI를 필요 합니다. Hello에서이 줄에 중단점을 설정 `MainPage` 메서드:
    ```
    redirectURI = Windows.Security.Authentication.Web.WebAuthenticationBroker.GetCurrentApplicationCallbackUri();
    ```
5. 모든 패키지 참조는 복원 되었는지 확인 하는 hello 솔루션을 빌드하십시오. 패키지가 누락 되 면 hello NuGet 패키지 관리자를 열고 복원할 합니다.
6. Hello 응용 프로그램을 실행 하 고 hello 값의 복사 `redirectUri` hello 중단점이 적중 될 때입니다. hello 값 hello 다음과 같아야 합니다.

    ```
    ms-app://s-1-15-2-1352796503-54529114-405753024-3540103335-3203256200-511895534-1429095407/
    ```

7. Hello에 다시 **설정** hello Azure 포털에서에서 hello 앱의 탭 추가 **RedirectUri** 값 앞에 오는 hello로 합니다.  

## <a name="step-3-use-adal-tooget-tokens-from-azure-ad"></a>3 단계: Azure AD에서 ADAL tooget 토큰 사용
hello ADAL 뒤에 있는 기본 원리는는 hello 앱 액세스 토큰을 필요할 때마다 단순히 호출 `authContext.AcquireToken(…)`, ADAL rest hello는 및입니다.  

1. Hello 앱 초기화 `AuthenticationContext`, ADAL의 기본 클래스인 hello 합니다. 이 작업을 Azure AD와 toocommunicate 하며 방법 설명 ADAL hello 좌표 전달 toocache 토큰입니다.

    ```C#
    public MainPage()
    {
        ...

        authContext = new AuthenticationContext(authority);
    }
    ```

2. Hello 찾을 `Search(...)` hello를 클릭할 때 호출 되는 메서드를 **검색** hello 응용 프로그램의 UI에서 단추입니다. 이 메서드는 해당 UPN 검색 단어를 지정 하는 hello로 시작 하는 사용자에 대 한 get 요청 toohello Azure AD Graph API tooquery를 만듭니다. tooquery hello Graph API hello 요청에서 액세스 토큰을 포함 **권한 부여** 헤더입니다. 여기로 ADAL이 들어옵니다.

    ```C#
    private async void Search(object sender, RoutedEventArgs e)
    {
        ...
        AuthenticationResult result = null;
        try
        {
            result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectURI, new PlatformParameters(PromptBehavior.Auto, false));
        }
        catch (AdalException ex)
        {
            if (ex.ErrorCode != "authentication_canceled")
            {
                ShowAuthError(string.Format("If hello error continues, please contact your administrator.\n\nError: {0}\n\nError Description:\n\n{1}", ex.ErrorCode, ex.Message));
            }
            return;
        }
        ...
    }
    ```
    호출 하 여 hello 앱 토큰을 요청할 때 `AcquireTokenAsync(...)`, ADAL hello 사용자 자격 증명을 요청 하지 않고 tooreturn 토큰을 시도 합니다. ADAL 해당 hello 사용자에 게 toosign tooget 토큰에에서 필요한 데이터를 결정 하는 경우 로그인 대화 상자를 표시, hello 사용자의 자격 증명을 수집 하 고 인증에 성공한 후 토큰을 반환 합니다. ADAL 어떤 이유로 든 없습니다 tooreturn 토큰 이면 hello *AuthenticationResult* 상태는 오류가 발생 합니다.
3. 이제 방금 확보 하는 시간 toouse hello 액세스 토큰입니다. Hello에도 `Search(...)` 메서드를 get 요청을 hello에서 Graph API hello 토큰 toohello 연결 **권한 부여** 헤더:

    ```C#
    // Add hello access token toohello Authorization header of hello call toohello Graph API, and call hello Graph API.
    httpClient.DefaultRequestHeaders.Authorization = new HttpCredentialsHeaderValue("Bearer", result.AccessToken);

    ```
4. Hello를 사용할 수 있습니다 `AuthenticationResult` 개체 hello 사용자의 ID와 같은 hello 응용 프로그램에서 사용자 hello에 대 한 toodisplay 정보:

    ```C#
    // Update hello page UI toorepresent hello signed-in user
    ActiveUser.Text = result.UserInfo.DisplayableId;
    ```
5. Hello 앱에서 ADAL toosign 사용자를 사용할 수 있습니다. Hello을 클릭할 때 hello **로그 아웃** 단추, 너무 hello 다음 호출 하는 확인`AcquireTokenAsync(...)` 로그인 뷰를 보여 줍니다. ADAL이이 작업 hello 토큰 캐시를 지우는 것 처럼 쉽게 표시 됩니다.

    ```C#
    private void SignOut()
    {
        // Clear session state from hello token cache.
        authContext.TokenCache.Clear();

        ...
    }
    ```

## <a name="whats-next"></a>다음 단계
이제 작업 중인 Windows 스토어 앱이 사용자를 인증, 안전 하 게 웹 OAuth 2.0을 사용 하 여 Api를 호출 하 고 수 있는 hello 사용자에 대 한 기본 정보를 가져올 해야 합니다.

사용자와 테 넌 트 채워진 이미 하지 않은 경우 지금은 hello 시간 toodo 이므로 합니다.
1. DirectorySearcher 응용 프로그램을 실행 하 고 hello 사용자 중 하나를 사용 하 여 로그인 합니다.
2. 해당 UPN에 따라 다른 사용자를 검색합니다.
3. Hello 응용 프로그램을 닫고 다시 실행 합니다. Hello 사용자의 세션 그대로 유지 방법을 확인 합니다.
4. Toodisplay hello 아래쪽 표시줄을 마우스 오른쪽 단추로 클릭 하 여 로그 아웃 한 다음 다른 사용자로 다시 로그인 합니다.

ADAL 쉽게 tooincorporate를 사용 하면 이러한 일반적인 모든 id 기능 hello 응용 프로그램에 있습니다. 관리의 모든 hello dirty 작업, 캐시 관리와 같은 OAuth 프로토콜 지원 등 hello 사용자 로그인 UI 제시 하 고 토큰 만료를 새로 고치 합니다. Tooknow 단일 API 호출 해야 `authContext.AcquireToken*(…)`합니다.

참조용으로 hello 다운로드 [완성 된 샘플](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip) (없이 구성 값).

이제 tooadditional id 시나리오에서 이동할 수 있습니다. 예를 들어 [Azure AD를 사용하여 .NET Web API 보안 유지](active-directory-devquickstarts-webapi-dotnet.md)를 시도해 보세요.

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

---
title: "AD aaaAzure.NET 시작 | Microsoft Docs"
description: "어떻게 toobuild 로그인에 대 한 Azure AD와 통합 하 고 Azure AD를 호출 하는.NET Windows 데스크톱 응용 프로그램 Api OAuth를 사용 하 여 보호 합니다."
services: active-directory
documentationcenter: .net
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: ed33574f-6fa3-402c-b030-fae76fba84e1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: c09b358f24c7bfb371b34cf72ca48c0a45042f5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-into-a-windows-desktop-wpf-app"></a>Windows Desktop WPF 앱에 Azure AD 통합
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

데스크톱 응용 프로그램을 개발 하는 경우 Azure AD는 간단 하 고 간단 하 게 하면 tooauthenticate 자신의 Active Directory 계정에 사용자가 있습니다.  응용 프로그램 toosecurely 해줍니다 모든 웹 Azure AD로 보호 되는 API를 사용와 같은 Office 365 Api hello 또는 Azure API를 환영 합니다.

.NET 네이티브 클라이언트의 tooaccess 보호 된 리소스를 필요로 하는 경우 Azure AD hello ADAL 또는 Active Directory 인증 라이브러리를 제공 합니다.  생활에서 ADAL의 목적으로 toomake 사용자가 앱 tooget 액세스 토큰을 쉽게 합니다.  이면 작업이 얼마나 쉬운지 toodemonstrate 여기 빌드합니다.NET WPF 할 일 목록 응용 프로그램입니다.

* 가져옵니다 hello를 사용 하 여 hello Azure AD Graph API 호출에 대 한 토큰에 액세스 [OAuth 2.0 인증 프로토콜](https://msdn.microsoft.com/library/azure/dn645545.aspx)합니다.
* 지정된 별칭을 가진 사용자를 디렉터리에서 검색합니다.
* 사용자를 로그아웃합니다.

toobuild hello 완료 작업 응용 프로그램에 필요 합니다.

1. Azure AD에 응용 프로그램을 등록합니다.
2. ADAL을 설치 및 구성합니다.
3. Azure AD에서 ADAL tooget 토큰을 사용 합니다.

시작 tooget [hello 응용 프로그램의 기본 정의 다운로드](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/skeleton.zip) 또는 [완료 hello 샘플 다운로드](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip)합니다.  또한 사용자를 만들고 응용 프로그램을 등록할 수 있는 Azure AD 테넌트도 필요합니다.  테 넌 트 아직 없는 경우 [자세한 방법을 하나 tooget](active-directory-howto-tenant.md)합니다.

## <a name="1-register-hello-directorysearcher-application"></a>1. Hello DirectorySearcher 응용 프로그램 등록
tooenable 먼저 해야 사용자가 앱 tooget 토큰 tooregister에서 Azure AD 테 넌 트 권한 tooaccess hello Azure AD Graph API에 부여 합니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. Hello 위쪽 막대에서 계정에 및 hello에서 클릭 **디렉터리** 목록에서 원하는 위치 tooregister 응용 프로그램 hello Active Directory 테 넌 트를 선택 합니다.
3. 클릭 **더 서비스** 왼쪽 nav hello와 선택 **Azure Active Directory**합니다.
4. **앱 등록**을 클릭하고 **추가**를 선택합니다.
5. Hello 화면에 따라 수행 하 고 새 **네이티브 클라이언트 응용 프로그램**합니다.
  * hello **이름** 응용 프로그램의 hello 응용 프로그램 tooend-사용자가 설명 합니다
  * hello **리디렉션 Uri** 체계 및 문자열 조합 tooreturn 토큰 응답을 Azure AD에 사용 됩니다.  값 특정 tooyour 응용 프로그램을 입력 합니다. `http://DirectorySearcher`합니다.
6. 등록을 완료하면 AAD는 앱에 고유한 응용 프로그램 ID를 할당합니다.  이 값이 필요 합니다 hello 다음 섹션의 하므로에서 복사 hello 응용 프로그램 페이지.
7. Hello에서 **설정** 페이지에서 선택 **필요한 권한** 선택 **추가**합니다. 선택 hello **Microsoft Graph** 으로 hello를 더하고 API hello **디렉터리 데이터 읽기** 에 따른 권한 **위임 된 권한**합니다.  이렇게 하면 응용 프로그램 tooquery hello Graph API 사용자에 대 한 활성화 됩니다.

## <a name="2-install--configure-adal"></a>2. ADAL 설치 및 구성
Azure AD에서 응용 프로그램이 있으므로 ADAL을 설치하고 ID 관련 코드를 작성할 수 있습니다.  해야 tooprovide에서 Azure AD와 ADAL toobe 수 toocommunicate 사용 하 여 응용 프로그램 등록에 대 한 정보입니다.

* Hello 패키지 관리자 콘솔을 사용 하 여 ADAL toohello DirectorySearcher 프로젝트를 추가 하 여 시작 합니다.

```
PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

* Hello DirectorySearcher 프로젝트를 열고 `app.config`합니다.  Hello에 hello 요소 hello 값 바꾸기 `<appSettings>` 섹션 tooreflect hello hello Azure 포털에 대 한 입력 값입니다.  코드는 ADAL을 사용할 때마다 이러한 값을 참조합니다.
  * hello `ida:Tenant` hello 도메인은의 Azure AD 테 넌 트, 예: contoso.onmicrosoft.com
  * hello `ida:ClientId` hello 포털에서 복사 하는 응용 프로그램의 hello clientId 됩니다.
  * hello `ida:RedirectUri` 는 hello 리디렉션 url hello 포털에 등록 합니다.

## <a name="3----use-adal-tooget-tokens-from-aad"></a>3.    AAD에서 ADAL tooGet 토큰 사용
hello ADAL 기본 원칙 되는 응용 프로그램 액세스 토큰을 필요할 때마다 단순히 호출 `authContext.AcquireTokenAsync(...)`, 및 ADAL rest hello지 않습니다.  

* Hello에 `DirectorySearcher` 프로젝트, 열기 `MainWindow.xaml.cs` hello 찾습니다 `MainWindow()` 메서드.  hello 첫 번째 단계는 tooinitialize 앱의 `AuthenticationContext` -ADAL의 기본 클래스입니다.  이 ADAL을 전달 하는 Azure AD와 toocommunicate 필요한 좌표 hello 및 방법에 설명 toocache 토큰입니다.

```C#
public MainWindow()
{
    InitializeComponent();

    authContext = new AuthenticationContext(authority, new FileCache());

    CheckForCachedToken();
}
```

* 이제 hello를 찾을 `Search(...)` 메서드 hello 사용자 cliks hello hello 응용 프로그램의 UI에서 "검색" 단추 때 호출 됩니다.  이 메서드는 해당 UPN 검색 단어를 지정 하는 hello로 시작 하는 사용자에 대 한 GET 요청 toohello Azure AD Graph API tooquery를 만듭니다.  순서 tooquery hello Graph API, tooinclude hello에서 access_token 필요 하지만 `Authorization` 이 경우에 ADAL-hello의 헤더를 요청 합니다.

```C#
private async void Search(object sender, RoutedEventArgs e)
{
    // Validate hello Input String
    if (string.IsNullOrEmpty(SearchText.Text))
    {
        MessageBox.Show("Please enter a value for hello tooDo item name");
        return;
    }

    // Get an Access Token for hello Graph API
    AuthenticationResult result = null;
    try
    {
        result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectUri, new PlatformParameters(PromptBehavior.Auto));
        UserNameLabel.Content = result.UserInfo.DisplayableId;
        SignOutButton.Visibility = Visibility.Visible;
    }
    catch (AdalException ex)
    {
        // An unexpected error occurred, or user canceled hello sign in.
        if (ex.ErrorCode != "access_denied")
            MessageBox.Show(ex.Message);

        return;
    }

    ...
}
```
* 응용 프로그램 호출 하 여 토큰을 요청 하는 경우 `AcquireTokenAsync(...)`, ADAL hello 사용자 자격 증명을 요청 하지 않고 tooreturn 토큰을 시도 합니다.  ADAL 해당 hello 사용자에 게 toosign tooget 토큰에에서 필요한 데이터를 결정 하는 경우 로그인 대화 상자를 표시, hello 사용자의 자격 증명을 수집 되며 인증 성공 시 토큰을 반환 합니다.  ADAL 어떤 이유로 든 없습니다 tooreturn 토큰 이면 예외를 throw 한 `AdalException`합니다.
* 해당 hello 확인 `AuthenticationResult` 개체에 포함 되어는 `UserInfo` 앱 할 수는 사용 되는 toocollect 정보 일 수 있는 개체입니다.  Hello DirectorySearcher에서 `UserInfo` hello 사용자의 id와 함께 사용 되는 toocustomize hello 응용 프로그램의 UI가 있습니다.
* Hello 사용자가 hello "로그 아웃" 단추를 클릭 한 다음 호출을 너무 hello tooensure 원하는`AcquireTokenAsync(...)` hello 사용자 toosign에 게 표시 합니다.  ADAL,이 hello 토큰 캐시를 지우는 것 처럼 쉽게:

```C#
private void SignOut(object sender = null, RoutedEventArgs args = null)
{
    // Clear hello token cache
    authContext.TokenCache.Clear();

    ...
}
```

* 그러나 hello 사용자 hello "로그 아웃" 단추를 클릭 하지 않는 경우 다음 DirectorySearcher hello를 실행할 때 hello에 대 한 toomaintain hello 사용자의 세션을 합니다.  Hello 앱이 시작 되 면 기존 토큰에 대 한 ADAL의 토큰 캐시를 확인 하 고 hello UI를 적절 하 게 업데이트할 수 있습니다.  Hello에 `CheckForCachedToken()` 메서드를 다른 호출할 너무`AcquireTokenAsync(...)`, hello를 전달 하는이 시간 `PromptBehavior.Never` 매개 변수입니다.  `PromptBehavior.Never`명령은 hello 사용자 로그인을 위해 묻지 해야 및 ADAL 대신 예외를 throw 해야 없습니다 tooreturn 이면 토큰 ADAL 알려줍니다.

```C#
public async void CheckForCachedToken() 
{
    // As hello application starts, try tooget an access token without prompting hello user.  If one exists, show hello user as signed in.
    AuthenticationResult result = null;
    try
    {
        result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectUri, new PlatformParameters(PromptBehavior.Never));
    }
    catch (AdalException ex)
    {
        if (ex.ErrorCode != "user_interaction_required")
        {
            // An unexpected error occurred.
            MessageBox.Show(ex.Message);
        }

        // If user interaction is required, proceed toomain page without singing hello user in.
        return;
    }

    // A valid token is in hello cache
    SignOutButton.Visibility = Visibility.Visible;
    UserNameLabel.Content = result.UserInfo.DisplayableId;
}
```

축하합니다. 이제 정상 작동 hello 기능 tooauthenticate 사용자가 있는.NET WPF 응용 프로그램, 안전 하 게 OAuth 2.0을 사용 하 여 웹 Api를 호출 하 고 hello 사용자에 대 한 기본 정보를 얻을 합니다.  아직 하지 않는 이제 경우 hello 시간 toopopulate 사용자로 구성 된 테 넌 트입니다.  DirectorySearcher 앱을 실행하고 해당 사용자 중 하나로 로그인합니다.  해당 UPN에 따라 다른 사용자를 검색합니다.  Hello 응용 프로그램을 닫고 다시 실행 합니다.  Hello 사용자의 세션 그대로 유지 방법을 확인 합니다.  로그아웃했다가 다른 사용자로 다시 로그인합니다.

ADAL 쉽게 tooincorporate를 사용 하면 모든 응용 프로그램에 이러한 일반적인 id 기능입니다.  있습니다-캐시 관리, 로그인 토큰이 만료 등 새로 고침 UI hello 사용자 제시 되는 OAuth 프로토콜 지원에 대 한 모든 hello dirty 작업의 관리 합니다.  Tooknow 실제로 필요한 것은 단일 API 호출 `authContext.AcquireTokenAsync(...)`합니다.

구성 값) (없이 완료 hello 샘플은 제공 참조용으로 [여기](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip)합니다.  이제 tooadditional 시나리오에 이동할 수 있습니다.  Tootry를 사용할 수 있습니다.

[Azure AD를 사용하여 .NET Web API 보안 유지 >>](active-directory-devquickstarts-webapi-dotnet.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]


---
title: "시작 하는 AD AngularJS aaaAzure | Microsoft Docs"
description: "Toobuild AngularJS 단일 페이지 응용 프로그램 하는 로그인에 대 한 Azure AD와 통합 되어 방법과 OAuth를 사용 하 여 Azure AD로 보호 된 Api를 호출 합니다."
services: active-directory
documentationcenter: 
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: f2991054-8146-4718-a5f7-59b892230ad7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: eca5e1c9662186dfae4f96ca3041f9350583cf79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="help-secure-angularjs-single-page-apps-by-using-azure-ad"></a>Azure AD를 사용하여 AngularJS 단일 페이지 앱 보안 지원

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Azure Active Directory (Azure AD)를 사용 하면 간단 하 고 tooadd 로그인, 로그 아웃에 대 한 간단한 보안 OAuth API 호출 tooyour 단일 페이지 응용 프로그램 및입니다.  앱 tooauthenticate 사용자의 Windows Server Active Directory 계정 사용 하 고 모든 웹 보호 하는 Azure AD를 Office 365 Api hello 또는 hello Azure API와 같은 API를 사용 합니다.

브라우저에서 실행 되는 JavaScript 응용 프로그램에 대 한 Azure AD는 hello 제공 adal.js 또는 Active Directory 인증 라이브러리 (ADAL). hello adal.js는 목적 toomake 사용자가 앱 tooget 액세스 토큰을 쉽게 합니다. 이면 작업이 얼마나 쉬운지 toodemonstrate 여기 빌드합니다 AngularJS tooDo 목록 응용 프로그램입니다.

* Hello id 공급자로 Azure AD를 사용 하 여 toohello 응용 프로그램에서 기호 hello 사용자입니다.

* Hello 사용자에 대 한 정보를 표시합니다.
* 안전 하 게 호출 응용 프로그램의 tooDo 목록 API를 Azure AD에서 전달자 토큰을 사용 하 여 hello 합니다.
* 기호 hello hello 앱에서 사용자입니다.

toobuild hello 완료 작업 응용 프로그램을 해야합니다.

1. Azure AD에 앱을 등록합니다.
2. ADAL을 설치 하 고 hello 단일 페이지 응용 프로그램을 구성 합니다.
3. Hello 단일 페이지 응용 프로그램에서 ADAL toohelp 보안 페이지를 사용 합니다.

시작 tooget [hello 응용 프로그램의 기본 정의 다운로드](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) 또는 [완료 hello 샘플 다운로드](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip)합니다. 또한 사용자를 만들고 응용 프로그램을 등록할 수 있는 Azure AD 테넌트도 필요합니다. 테 넌 트 아직 없는 경우 [자세한 방법을 하나 tooget](active-directory-howto-tenant.md)합니다.

## <a name="step-1-register-hello-directorysearcher-application"></a>1 단계: hello DirectorySearcher 응용 프로그램 등록
tooenable tooauthenticate 사용자 응용 프로그램 및 get 토큰을 먼저 tooregister에서 Azure AD 테 넌 트:

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. Toomultiple 디렉터리에 로그인 한 경우에 hello 올바른 디렉터리를 보려는 tooensure를 할 수 있습니다. toodo 따라서 hello 위쪽 막대에서 계정을 클릭 합니다. Hello에서 **디렉터리** 목록 tooregister 원하는 hello Azure AD 테 넌 트 응용 프로그램을 선택 합니다.
3. 클릭 **더 서비스** 에 hello 왼쪽된 창에서 선택한 후 **Azure Active Directory**합니다.
4. **앱 등록**을 클릭하고 **추가**를 선택합니다.
5. Hello 화면에 따라 수행 하 고 새 웹 응용 프로그램 및/또는 web API를 만듭니다.
  * **이름** 응용 프로그램 toousers에 설명 합니다.
  * **리디렉션 Uri** 는 hello 위치 toowhich Azure AD 토큰을 반환 합니다. 이 샘플에 대 한 hello 기본 위치는 `https://localhost:44326/`합니다.
6. 등록을 완료 한 후 Azure AD는 고유한 응용 프로그램 ID tooyour 응용 프로그램에 할당 합니다.  이 값이 필요 합니다 hello 다음 섹션의 하므로에서 복사 hello 응용 프로그램 탭 합니다.
7. Adal.js를 Azure AD OAuth 암시적 흐름 toocommunicate hello를 사용합니다. 응용 프로그램에 대 한 hello 암시적 흐름을 사용 해야 합니다.
  1. Hello 응용 프로그램을 클릭 하 고 선택 **매니페스트** tooopen hello 인라인 매니페스트 편집기입니다.
  2. Hello 찾을 `oauth2AllowImplicitFlow` 속성입니다. 해당 값을 너무 설정`true`합니다.
  3. 클릭 **저장** toosave hello 매니페스트 합니다.
8. 응용 프로그램에 대해 테넌트 전체에서 권한을 부여합니다. 너무 이동**설정** > **속성** > **필요한 권한**, hello 클릭 **사용 권한 부여**hello 위쪽 막대 단추입니다. 클릭 **예** tooconfirm 합니다.

## <a name="step-2-install-adal-and-configure-hello-single-page-app"></a>2 단계: ADAL 설치 하 고 hello 단일 페이지 응용 프로그램 구성
Azure AD에서 응용 프로그램이 있으므로 adal.js를 설치하고 ID 관련 코드를 작성할 수 있습니다.

### <a name="configure-hello-javascript-client"></a>Hello JavaScript 클라이언트 구성
Hello 패키지 관리자 콘솔을 사용 하 여 adal.js toohello TodoSPA 프로젝트를 추가 하 여 시작 합니다.
  1. 다운로드 [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal.js) toohello 추가 `App/Scripts/` 프로젝트 디렉터리.
  2. 다운로드 [adal angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal-angular.js) toohello 추가 `App/Scripts/` 프로젝트 디렉터리.
  3. 각 스크립트의 hello hello 종료 하기 전에 로드 `</body>` 에 `index.html`:

    ```js
    ...
    <script src="App/Scripts/adal.js"></script>
    <script src="App/Scripts/adal-angular.js"></script>
    ...
    ```

### <a name="configure-hello-back-end-server"></a>Hello 백 엔드 서버 구성
Hello 단일 페이지 앱 백 엔드에서 tooDo 목록 API tooaccept 토큰 hello 브라우저에서에 대 한 hello 백 엔드는 hello 응용 프로그램 등록에 대 한 구성 정보가 필요합니다. Hello TodoSPA 프로젝트를 열고 `web.config`합니다. Hello에 hello 요소 hello 값 바꾸기 `<appSettings>` tooreflect hello 값 값 섹션에서 사용한 hello Azure 포털입니다. 코드는 ADAL을 사용할 때마다 이러한 값을 참조합니다.
  * `ida:Tenant`Azure AD 테 넌 트의-예를 들어 contoso.onmicrosoft.com hello 도메인이입니다.
  * `ida:Audience`hello hello 포털에서 복사 하는 응용 프로그램 클라이언트 ID입니다.

## <a name="step-3-use-adal-toohelp-secure-pages-in-hello-single-page-app"></a>3 단계: 사용 하 여 ADAL toohelp hello 단일 페이지 응용 프로그램의 보안 페이지
Adal.js는 AngularJS 경로 및 HTTP 공급자와 통합되므로 단일 페이지 앱에서 개별 뷰의 보안을 지원할 수 있습니다.

1. `App/Scripts/app.js`, hello adal.js 모듈 가져오기:

    ```js
    angular.module('todoApp', ['ngRoute','AdalAngular'])
    .config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
     function ($routeProvider, $httpProvider, adalProvider) {
    ...
    ```
2. 초기화 `adalProvider` 에 프로그램 응용 프로그램 등록의 hello 구성 값을 사용 하 여 `App/Scripts/app.js`:

    ```js
    adalProvider.init(
      {
          instance: 'https://login.microsoftonline.com/',
          tenant: 'Enter your tenant name here e.g. contoso.onmicrosoft.com',
          clientId: 'Enter your client ID here e.g. e9a5a8b6-8af7-4719-9821-0deef255f68e',
          extraQueryParameter: 'nux=1',
          //cacheLocation: 'localStorage', // enable this for IE, as sessionStorage does not work for localhost.
      },
      $httpProvider
    );
    ```
3. 보안 hello 도움말 `TodoList` 한 줄의 코드를 사용 하 여 hello 앱에서 보기: `requireADLogin`합니다.

    ```js
    ...
    }).when("/TodoList", {
            controller: "todoListCtrl",
            templateUrl: "/App/Views/TodoList.html",
            requireADLogin: true,
    ...
    ```

## <a name="summary"></a>요약
이제 사용자가 로그인 하 고 요청 전달자 토큰 보호 tooits 백 엔드 API를 발급할 수 있는 안전한 단일 페이지 앱을 준비 되었습니다. Hello 클릭 하면 **TodoList** 링크, adal.js는 로그인에 대해 필요한 경우 AD tooAzure 리디렉션합니다 자동으로 합니다. 또한 adal.js에서 자동으로 액세스 토큰 tooany Ajax 요청 toohello 앱 백 엔드 보낸 연결 됩니다.  

hello 앞 단계는 hello 완전 최소 필요한 toobuild 단일 페이지 앱 adal.js를 사용 하 여 합니다. 하지만 단일 페이지 앱에서 유용한 몇 가지 다른 기능이 있습니다.

* tooexplicitly 로그인 및 로그 아웃 요청을 실행할 adal.js를 호출 하는 컨트롤러에서 함수를 정의할 수 있습니다.  `App/Scripts/homeCtrl.js`:

    ```js
    ...
    $scope.login = function () {
        adalService.login();
    };
    $scope.logout = function () {
        adalService.logOut();
    };
    ...
    ```
* Hello 응용 프로그램의 UI에서 toopresent 사용자 정보를 할 수 있습니다. hello ADAL 서비스 이미 추가 되어 toohello `userDataCtrl` hello에 액세스할 수 있도록 컨트롤러 `userInfo` hello에 개체 관련 보기, `App/Views/UserData.html`:

    ```js
    <p>{{userInfo.userName}}</p>
    <p>aud:{{userInfo.profile.aud}}</p>
    <p>iss:{{userInfo.profile.iss}}</p>
    ...
    ```

* 에 있는 합니다 tooknow hello 사용자의 로그인 한 경우 많은 시나리오가 있습니다. Hello를 사용할 수도 있습니다 `userInfo` toogather이이 정보 개체입니다.  예를 들어, `index.html`, 어느 hello를 표시할 수 있습니다 **로그인** 또는 **로그 아웃** 인증 상태에 따라 단추:

    ```js
    <li><a class="btn btn-link" ng-show="userInfo.isAuthenticated" ng-click="logout()">Logout</a></li>
    <li><a class="btn btn-link" ng-hide=" userInfo.isAuthenticated" ng-click="login()">Login</a></li>
    ```

Azure AD에 통합 된 단일 페이지 응용 프로그램 인증 사용자, 안전 하 게 OAuth 2.0을 사용 하 여 해당 백 엔드를 호출 하 고 수 hello 사용자에 대 한 기본 정보를 얻을 합니다. 아직 하지 않는 이제 경우 hello 시간 toopopulate 사용자로 구성 된 테 넌 트입니다. TooDo 목록 단일 페이지 응용 프로그램을 실행 하 고 해당 사용자 중 하나를 사용 하 여 로그인 합니다. 작업 toohello 사용자의 할 일 목록 추가, 로그 아웃 하 고 다시 로그인 합니다.

Adal.js를 응용 프로그램으로 쉽게 tooincorporate 일반적인 id 기능이 있습니다. 사용자에 대 한 모든 hello dirty 작업은 담당: 캐시 관리, OAuth 프로토콜 지원 등 hello 사용자는 로그인 UI, 만료 된 토큰 등을 새로 고치면 제시 합니다.

구성 값) (없이 hello 완료 샘플은에서 사용할 수 있는 참조를 위해 [GitHub](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip)합니다.

## <a name="next-steps"></a>다음 단계
이제 tooadditional 시나리오에 이동할 수 있습니다. Tootry 할 수 있습니다: [단일 페이지 앱에서 CORS web API를 호출할](https://github.com/AzureAdSamples/SinglePageApp-WebAPI-AngularJS-DotNet)합니다.

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

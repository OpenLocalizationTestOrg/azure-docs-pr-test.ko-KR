---
title: "AD aaaAzure v2.0.NET AngularJS 단일 페이지 응용 프로그램 시작 | Microsoft Docs"
description: "Toobuild 두 개인 Microsoft와 사용자가 로그인 하는 각도 JS 단일 페이지 응용 프로그램 계정 및 작동 방법 또는 학교 계정입니다."
services: active-directory
documentationcenter: 
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 6a341781-278f-461b-92ca-7572a06e6852
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/23/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: bd3fc8dce91eb0bedcbfed47a9b3ef52c5568c6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooan-angularjs-single-page-app---net"></a>로그인 tooan AngularJS 단일 페이지 앱 추가-.NET
이 문서의 hello Azure Active Directory v2.0 endpoint를 사용 하 여 전원이 Microsoft 계정 tooan AngularJS 앱을 사용 하 여 로그인을 추가 합니다.  hello v2.0 끝점 tooperform 단일 통합 앱에 있으며 사용자 개인 정보와 작업/학교 계정으로 인증 합니다.

이 샘플은 백 엔드 hello.NET 4.5 MVC 프레임 워크를 사용 하 여 작성 하 고 Azure AD에서 OAuth 전달자 토큰을 사용 하 여 보안 REST API 작업을 저장 하는 간단한 할 일 목록 단일 페이지 앱.  hello AngularJS 응용 프로그램은 사용이 오픈 소스 JavaScript 인증 라이브러리 [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) toohandle 전체 로그인 프로세스를 hello 및 REST API 호출 hello에 대 한 토큰을 획득 합니다.  hello 동일한 패턴 수 hello와 같은 적용된 tooauthenticate tooother REST Api [Microsoft Graph](https://graph.microsoft.com)합니다.

> [!NOTE]
> 모든 Azure Active Directory 시나리오 및 기능 hello v2.0 끝점에서 사용할 수 있습니다.  에 대해 알아보세요 hello v2.0 끝점을 사용 해야 하는 경우 toodetermine [v2.0 제한](active-directory-v2-limitations.md)합니다.
> 
> 

## <a name="download"></a>다운로드
시작 tooget toodownload 필요한 및 Visual Studio를 설치 합니다.  그 후 골격 앱을 복제하거나 [다운로드](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) 합니다.

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet.git
```

hello 기본 응용 프로그램에는 간단한 AngularJS 앱에 대 한 모든 hello 상용구 코드가 포함 되어 있지만 모든 hello id 관련 조각이 없습니다.  대신 복제할 수 toofollow와 함께 사용 하지 않으려는 경우 또는 [다운로드](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet/archive/complete.zip) 완료 hello 샘플입니다.

```
git clone https://github.com/AzureADSamples/SinglePageApp-AngularJS-DotNet.git
```

## <a name="register-an-app"></a>앱 등록
첫째, hello에서 앱을 만들 [응용 프로그램 등록 포털](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), 있고이 따라 [자세한 단계는](active-directory-v2-app-registration.md)합니다.  다음을 수행해야 합니다.

* Hello 추가 **웹** 응용 프로그램을 위한 플랫폼입니다.
* 올바른 hello 입력 **리디렉션 URI**합니다. 이 샘플에 대 한 hello 기본값은 `https://localhost:44326/`합니다.
* Hello 둡니다 **암시적 흐름 허용** 사용 하도록 설정 하는 확인란을 선택 합니다. 

Hello 아래로 복사 **응용 프로그램 ID** 할당된 tooyour 응용 프로그램을 잠시 후에 필요 합니다. 

## <a name="install-adaljs"></a>adal.js 설치
toostart, 다운로드 한 tooproject 이동한 adal.js를 설치 합니다.  [bower](http://bower.io/) 가 설치되어 있는 경우 이 명령을 실행하기만 하면 됩니다.  모든 종속성 버전 불일치 hello 더 높은 버전을 선택 하기만 합니다.

```
bower install adal-angular#experimental
```

또는 [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js)와 [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js)를 수동으로 다운로드할 수 있습니다.  두 파일 toohello 추가 `app/lib/adal-angular-experimental/dist` hello 디렉터리로 `TodoSPA` 프로젝트.

Visual Studio에서 hello 프로젝트를 열고 hello 기본 페이지 본문의 hello 끝에 adal.js 로드 이제 합니다.

```html
<!--index.html-->

...

<script src="App/bower_components/dist/adal.min.js"></script>
<script src="App/bower_components/dist/adal-angular.min.js"></script>

...
```

## <a name="set-up-hello-rest-api"></a>REST API hello 설정
에서는 설정 중, 있지만 hello 백 엔드 REST API 작업을 볼 보겠습니다.  Hello hello 프로젝트의 루트에서 열고 `web.config` hello 바꾸고 `audience` 값입니다.  hello REST API는 hello 각도 앱 AJAX 요청에서 받은이 값 toovalidate 토큰을 사용 합니다.

```xml
<!--web.config-->

...

    <appSettings>
        <add key="ida:Audience" value="[Your-application-id]" />
    </appSettings>

...
```

그 hello 시간 toospend hello REST API의 작동 방식에 대해 논의 가져오겠습니다.  웹 Api와 Azure AD 보안에 대 한 자세한 toolearn 원한다 면 체크 아웃 않고 hello 코드에서 가능한 toopoke 생각 될 [이 여기서](active-directory-v2-devquickstarts-dotnet-api.md)합니다. 

## <a name="sign-users-in"></a>사용자 로그인
Toowrite 일부 identity 코드를 시간입니다.  이미 눈치채셨겠지만, adal.js는 AngularJS 공급자를 포함하며, 이것은 Angular 라우팅 메커니즘을 잘 활용합니다.  Hello adal 모듈 toohello 앱을 추가 하 여 시작 합니다.

```js
// app/scripts/app.js

angular.module('todoApp', ['ngRoute','AdalAngular'])
.config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
 function ($routeProvider, $httpProvider, adalProvider) {

...
```

이제 hello를 초기화할 수 `adalProvider` 응용 프로그램 id:

```js
// app/scripts/app.js

...

adalProvider.init({

        // Use this value for hello public instance of Azure AD
        instance: 'https://login.microsoftonline.com/', 

        // hello 'common' endpoint is used for multi-tenant applications like this one
        tenant: 'common',

        // Your application id from hello registration portal
        clientId: '<Your-application-id>',

        // If you're using IE, uncommment this line - hello default HTML5 sessionStorage does not work for localhost.
        //cacheLocation: 'localStorage',

    }, $httpProvider);
```

이제 adal.js에 모든 hello 정보 크지 필요한 toosecure에 있는 앱과 로그인 사용자입니다.  걸리는 모든 hello 응용 프로그램에서 특정 경로 대 한 로그인 tooforce은 한 줄의 코드.

```js
// app/scripts/app.js

...

}).when("/TodoList", {
    controller: "todoListCtrl",
    templateUrl: "/static/views/TodoList.html",
    requireADLogin: true, // Ensures that hello user must be logged in tooaccess hello route
})

...
```

이제 사용자가 클릭할 때 hello `TodoList` 링크, adal.js는 로그인에 대해 필요한 경우 AD tooAzure 리디렉션합니다 자동으로 합니다.  컨트롤러에서 adal.js를 호출하여 명시적으로 로그인 및 로그아웃 요청을 보낼 수 있습니다.

```js
// app/scripts/homeCtrl.js

angular.module('todoApp')
// Load adal.js hello same way for use in controllers and views   
.controller('homeCtrl', ['$scope', 'adalAuthenticationService','$location', function ($scope, adalService, $location) {
    $scope.login = function () {

        // Redirect hello user toosign in
        adalService.login();

    };
    $scope.logout = function () {

        // Redirect hello user toolog out    
        adalService.logOut();

    };
...
```

## <a name="display-user-info"></a>사용자 정보 표시
Hello 사용자가 로그인 했으므로 응용 프로그램에 tooaccess hello 로그인 한 사용자의 인증 데이터를 아마도 필요 합니다.  Adal.js hello에이 정보를 노출 `userInfo` 개체입니다.  tooaccess 뷰에서이 개체에는 먼저 hello 해당 컨트롤러의 adal.js toohello 루트 범위 추가:

```js
// app/scripts/userDataCtrl.js

angular.module('todoApp')
// Load ADAL for use in view
.controller('userDataCtrl', ['$scope', 'adalAuthenticationService', function ($scope, adalService) {}]);
```

Hello를 직접 처리 한 다음 `userInfo` 보기에서 개체: 

```html
<!--app/views/UserData.html-->

...

    <!--Get hello user's profile information from hello ADAL userInfo object-->
    <tr ng-repeat="(key, value) in userInfo.profile">
        <td>{{key}}</td>
        <td>{{value}}</td>
    </tr>
...
```

Hello를 사용할 수도 있습니다 `userInfo` hello 사용자의 로그인 한 경우 toodetermine 개체입니다.

```html
<!--index.html-->

...

    <!--Use hello ADAL userInfo object tooshow hello right login/logout button-->
    <ul class="nav navbar-nav navbar-right">
        <li><a class="btn btn-link" ng-show="userInfo.isAuthenticated" ng-click="logout()">Logout</a></li>
        <li><a class="btn btn-link" ng-hide="userInfo.isAuthenticated" ng-click="login()">Login</a></li>
    </ul>
...
```

## <a name="call-hello-rest-api"></a>Hello REST API를 호출 합니다.
마지막으로 일부 토큰 및 호출 REST API toocreate hello, 읽기, 업데이트 및 삭제 작업의 시간 tooget를입니다.  무엇이 필요할까요?  Toodo 없는 *사물*합니다.  Adal.js에서 토큰 가져오기, 캐싱, 새로 고침 작업을 자동으로 처리합니다.  또한 자동으로 수행 됩니다 toooutgoing AJAX 요청 toohello REST API를 보내 해당 토큰을 연결 합니다.  

작동 원리는 바로 이렇습니다. 모든 감사 toohello 매직은 [AngularJS 인터셉터](https://docs.angularjs.org/api/ng/service/$http), adal.js tootransform 들어오고 나가는 http 메시지 있습니다.  또한 adal.js 가정는 모든 요청 toohello를 전송 하는 동일한 도메인 hello 창을 위한 토큰을 사용 해야 하는 대로 hello 응용 프로그램 ID 같은 hello AngularJS 앱으로 합니다.  이 때문에 hello 사용 hello NodeJS REST API 및 hello 각도 앱 모두에 동일한 응용 프로그램 ID입니다.  물론,이 동작을 재정의 하 고 adal.js tooget 토큰-필요한 경우 다른 REST Api에 대 한 알 수 있지만이 간단한 시나리오 hello 기본값 작업으로 충분 합니다.

얼마나 쉬운지 Azure AD에서 전달자 토큰을 사용 하 여 toosend 요청을 보여 주는 코드 조각은 다음과 같습니다.

```js
// app/scripts/todoListSvc.js

...
return $http.get('/api/tasks');
...
```

축하합니다.  Azure AD 통합 단일 페이지 앱이 완성되었습니다.  수고 많으셨습니다.  수 사용자 인증, 안전 하 게 해당 백 엔드 OpenID Connect를 사용 하 여 REST API를 호출 하 고 hello 사용자에 대 한 기본 정보를 얻을 합니다.  Hello 초기 개인 Microsoft 계정 또는 Azure AD에서 작업/학교 계정이 있는 모든 사용자를 지원합니다.  Hello 응용 프로그램을 실행 하 고 브라우저에서 탐색 너무`https://localhost:44326/`합니다.  개인 Microsoft 계정 또는 회사/학교 계정을 사용하여 로그인합니다.  작업 toohello 사용자의 할 일 목록에 추가 하 고 로그 아웃 합니다.  다른 유형의 계정 hello 시도 된에 서명 합니다. Azure AD 테 넌 트 toocreate 작업/학교 사용자 해야 할 경우 [자세한 방법을 tooget 한 여기](active-directory-howto-tenant.md) (가능한 경우).

헤드 백 tooour hello v2.0 끝점에 대해 알아보기 toocontinue [v2.0 개발자 가이드](active-directory-appmodel-v2-overview.md)합니다.  추가 리소스는 다음을 확인해보세요.

* [GitHub의 Azure 샘플(영문) >>](https://github.com/Azure-Samples)
* [스택 오버플로의 Azure AD(영문) >>](http://stackoverflow.com/questions/tagged/azure-active-directory)
* [Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)의 Azure AD 설명서

## <a name="get-security-updates-for-our-products"></a>당사 제품에 대한 보안 업데이트 가져오기
보안 사고를 방문 하 여 발생 하는 경우의 알림 tooget 좋습니다 [이 페이지](https://technet.microsoft.com/security/dd252948) 및 tooSecurity 자문 경고를 구독 합니다.


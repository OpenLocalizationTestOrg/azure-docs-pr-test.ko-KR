---
title: "AD aaaAzure v2.0 NodeJS AngularJS 단일 페이지 응용 프로그램 시작 | Microsoft Docs"
description: "Toobuild 두 개인 Microsoft와 사용자가 로그인 하는 각도 JS 단일 페이지 응용 프로그램 계정 및 작동 방법 또는 학교 계정입니다."
services: active-directory
documentationcenter: 
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: d286aa33-8a94-452f-beb7-ddc6c6daa5c8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/23/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 1ab450caf08ab05fba140b94b1b8de652e99cbc1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooan-angularjs-single-page-app---nodejs"></a><span data-ttu-id="d2318-103">로그인 tooan AngularJS 단일 페이지 앱 추가-NodeJS</span><span class="sxs-lookup"><span data-stu-id="d2318-103">Add sign-in tooan AngularJS single page app - NodeJS</span></span>
<span data-ttu-id="d2318-104">이 문서의 hello Azure Active Directory v2.0 endpoint를 사용 하 여 전원이 Microsoft 계정 tooan AngularJS 앱을 사용 하 여 로그인을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2318-104">In this article we'll add sign in with Microsoft powered accounts tooan AngularJS app using hello Azure Active Directory v2.0 endpoint.</span></span> <span data-ttu-id="d2318-105">hello v2.0 끝점 tooperform 응용 프로그램에서 단일 통합을 사용 하 고 개인 정보와 작업/학교 계정이 있는 사용자를 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2318-105">hello v2.0 endpoint enable you tooperform a single integration in your app and authenticate users with both personal and work/school accounts.</span></span>

<span data-ttu-id="d2318-106">이 샘플은 Azure AD의 OAuth 전달자 토큰을 사용하여 보안이 유지되고 NodeJS로 작성된 백 엔드 REST API에 작업을 저장하는 간단한 To-Do List 단일 페이지 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="d2318-106">This sample is a simple To-Do List single page app that stores tasks in a backend REST API, written in NodeJS and secured using OAuth bearer tokens from Azure AD.</span></span>  <span data-ttu-id="d2318-107">hello AngularJS 응용 프로그램은 사용이 오픈 소스 JavaScript 인증 라이브러리 [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) toohandle 전체 로그인 프로세스를 hello 및 REST API 호출 hello에 대 한 토큰을 획득 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2318-107">hello AngularJS app will use our open source JavaScript authentication library [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) toohandle hello entire sign in process and acquire tokens for calling hello REST API.</span></span>  <span data-ttu-id="d2318-108">hello 동일한 패턴 수 hello와 같은 적용된 tooauthenticate tooother REST Api [Microsoft Graph](https://graph.microsoft.com) 또는 Azure 리소스 관리자 Api를 환영 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2318-108">hello same pattern can be applied tooauthenticate tooother REST APIs, like hello [Microsoft Graph](https://graph.microsoft.com) or hello Azure Resource Manager APIs.</span></span>

> [!NOTE]
> <span data-ttu-id="d2318-109">모든 Azure Active Directory 시나리오 및 기능 hello v2.0 끝점에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2318-109">Not all Azure Active Directory scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="d2318-110">에 대해 알아보세요 hello v2.0 끝점을 사용 해야 하는 경우 toodetermine [v2.0 제한](active-directory-v2-limitations.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d2318-110">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download"></a><span data-ttu-id="d2318-111">다운로드</span><span class="sxs-lookup"><span data-stu-id="d2318-111">Download</span></span>
<span data-ttu-id="d2318-112">필요한 tooget 시작, 설치 및 toodownload [node.js](https://nodejs.org)합니다.</span><span class="sxs-lookup"><span data-stu-id="d2318-112">tooget started, you'll need toodownload & install [node.js](https://nodejs.org).</span></span>  <span data-ttu-id="d2318-113">그 후 골격 앱을 복제하거나 [다운로드](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/skeleton.zip) 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2318-113">Then you can clone or [download](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/skeleton.zip) a skeleton app:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS.git
```

<span data-ttu-id="d2318-114">hello 기본 응용 프로그램에는 간단한 AngularJS 앱에 대 한 모든 hello 상용구 코드가 포함 되어 있지만 모든 hello id 관련 조각이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d2318-114">hello skeleton app includes all hello boilerplate code for a simple AngularJS app, but is missing all of hello identity-related pieces.</span></span>  <span data-ttu-id="d2318-115">대신 복제할 수 toofollow와 함께 사용 하지 않으려는 경우 또는 [다운로드](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/complete.zip) 완료 hello 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="d2318-115">If you don't want toofollow along, you can instead clone or [download](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/complete.zip) hello completed sample.</span></span>

```
git clone https://github.com/AzureADSamples/SinglePageApp-AngularJS-NodeJS.git
```

## <a name="register-an-app"></a><span data-ttu-id="d2318-116">앱 등록</span><span class="sxs-lookup"><span data-stu-id="d2318-116">Register an app</span></span>
<span data-ttu-id="d2318-117">첫째, hello에서 앱을 만들 [응용 프로그램 등록 포털](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), 있고이 따라 [자세한 단계는](active-directory-v2-app-registration.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d2318-117">First, create an app in hello [App Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="d2318-118">다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2318-118">Make sure to:</span></span>

* <span data-ttu-id="d2318-119">Hello 추가 **웹** 응용 프로그램을 위한 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="d2318-119">Add hello **Web** platform for your app.</span></span>
* <span data-ttu-id="d2318-120">올바른 hello 입력 **리디렉션 URI**합니다.</span><span class="sxs-lookup"><span data-stu-id="d2318-120">Enter hello correct **Redirect URI**.</span></span> <span data-ttu-id="d2318-121">이 샘플에 대 한 hello 기본값은 `http://localhost:8080`합니다.</span><span class="sxs-lookup"><span data-stu-id="d2318-121">hello default for this sample is `http://localhost:8080`.</span></span>
* <span data-ttu-id="d2318-122">Hello 둡니다 **암시적 흐름 허용** 사용 하도록 설정 하는 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2318-122">Leave hello **Allow Implicit Flow** checkbox enabled.</span></span> 

<span data-ttu-id="d2318-123">Hello 아래로 복사 **응용 프로그램 ID** 할당된 tooyour 응용 프로그램을 잠시 후에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2318-123">Copy down hello **Application ID** that is assigned tooyour app, you'll need it shortly.</span></span> 

## <a name="install-adaljs"></a><span data-ttu-id="d2318-124">adal.js 설치</span><span class="sxs-lookup"><span data-stu-id="d2318-124">Install adal.js</span></span>
<span data-ttu-id="d2318-125">toostart, 다운로드 한 tooproject 이동한 adal.js를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2318-125">toostart, navigate tooproject you downloaded and install adal.js.</span></span>  <span data-ttu-id="d2318-126">[bower](http://bower.io/) 가 설치되어 있는 경우 이 명령을 실행하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2318-126">If you have [bower](http://bower.io/) installed, you can just run this command.</span></span>  <span data-ttu-id="d2318-127">모든 종속성 버전 불일치 hello 더 높은 버전을 선택 하기만 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2318-127">For any dependency version mismatches, just choose hello higher version.</span></span>

```
bower install adal-angular#experimental
```

<span data-ttu-id="d2318-128">또는 [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js)와 [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js)를 수동으로 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2318-128">Alternatively, you can manually download [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) and [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js).</span></span>  <span data-ttu-id="d2318-129">두 파일 toohello 추가 `app/lib/adal-angular-experimental/dist` 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="d2318-129">Add both files toohello `app/lib/adal-angular-experimental/dist` directory.</span></span>

<span data-ttu-id="d2318-130">원하는 텍스트 편집기에서 hello 프로젝트를 열고 hello 페이지 본문의 hello 끝에 adal.js 로드 이제:</span><span class="sxs-lookup"><span data-stu-id="d2318-130">Now open hello project in your favorite text editor, and load adal.js at hello end of hello page body:</span></span>

```html
<!--index.html-->

...

<script src="App/bower_components/dist/adal.min.js"></script>
<script src="App/bower_components/dist/adal-angular.min.js"></script>

...
```

## <a name="set-up-hello-rest-api"></a><span data-ttu-id="d2318-131">REST API hello 설정</span><span class="sxs-lookup"><span data-stu-id="d2318-131">Set up hello REST API</span></span>
<span data-ttu-id="d2318-132">에서는 설정 중, 동안 get hello 백 엔드 REST API 작업을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2318-132">While we're setting things up, lets get hello backend REST API working.</span></span>  <span data-ttu-id="d2318-133">명령 프롬프트에서 실행 하 여 hello 필요한 패키지가 모두 설치 (hello hello 프로젝트의 최상위 디렉터리에 있는지 확인):</span><span class="sxs-lookup"><span data-stu-id="d2318-133">In a command prompt, install all hello necessary packages by running (make sure you're in hello top-level directory of hello project):</span></span>

```
npm install
```

<span data-ttu-id="d2318-134">이제 열 `config.js` hello 바꾸고 `audience` 값:</span><span class="sxs-lookup"><span data-stu-id="d2318-134">Now open `config.js` and replace hello `audience` value:</span></span>

```js
exports.creds = {

     // TODO: Replace this value with hello Application ID from hello registration portal
     audience: '<Your-application-id>',

     ...
}
```

<span data-ttu-id="d2318-135">hello REST API는 hello 각도 앱 AJAX 요청에서 받은이 값 toovalidate 토큰을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2318-135">hello REST API will use this value toovalidate tokens it receives from hello Angular app on AJAX requests.</span></span>  <span data-ttu-id="d2318-136">Note이 간단한 REST API에는 메모리 내 데이터-각 시간 toostop hello 서버 저장, 이전에 만든된 모든 작업이 손실 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2318-136">Note that this simple REST API stores data in-memory - so each time toostop hello server, you will lose all previously created tasks.</span></span>

<span data-ttu-id="d2318-137">그 hello 시간 toospend hello REST API의 작동 방식에 대해 논의 가져오겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d2318-137">That's all hello time we're going toospend discussing how hello REST API works.</span></span>  <span data-ttu-id="d2318-138">웹 Api와 Azure AD 보안에 대 한 자세한 toolearn 원한다 면 체크 아웃 않고 hello 코드에서 가능한 toopoke 생각 될 [이 여기서](active-directory-v2-devquickstarts-node-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d2318-138">Feel free toopoke around in hello code, but if you want toolearn more about securing web APIs with Azure AD, check out [this article](active-directory-v2-devquickstarts-node-api.md).</span></span> 

## <a name="sign-users-in"></a><span data-ttu-id="d2318-139">사용자 로그인</span><span class="sxs-lookup"><span data-stu-id="d2318-139">Sign users in</span></span>
<span data-ttu-id="d2318-140">Toowrite 일부 identity 코드를 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="d2318-140">Time toowrite some identity code.</span></span>  <span data-ttu-id="d2318-141">이미 눈치채셨겠지만, adal.js는 AngularJS 공급자를 포함하며, 이것은 Angular 라우팅 메커니즘을 잘 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2318-141">You might have already noticed that adal.js contains an AngularJS provider, which plays nicely with Angular routing mechanisms.</span></span>  <span data-ttu-id="d2318-142">Hello adal 모듈 toohello 앱을 추가 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2318-142">Start by adding hello adal module toohello app:</span></span>

```js
// app/scripts/app.js

angular.module('todoApp', ['ngRoute','AdalAngular'])
.config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
 function ($routeProvider, $httpProvider, adalProvider) {

...
```

<span data-ttu-id="d2318-143">이제 hello를 초기화할 수 `adalProvider` 응용 프로그램 id:</span><span class="sxs-lookup"><span data-stu-id="d2318-143">You can now initialize hello `adalProvider` with your Application ID:</span></span>

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

<span data-ttu-id="d2318-144">이제 adal.js에 모든 hello 정보 크지 필요한 toosecure에 있는 앱과 로그인 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="d2318-144">Great, now adal.js has all hello information it needs toosecure your app and sign users in.</span></span>  <span data-ttu-id="d2318-145">걸리는 모든 hello 응용 프로그램에서 특정 경로 대 한 로그인 tooforce은 한 줄의 코드.</span><span class="sxs-lookup"><span data-stu-id="d2318-145">tooforce sign in for a particular route in hello app, all it takes is one line of code:</span></span>

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

<span data-ttu-id="d2318-146">이제 사용자가 클릭할 때 hello `TodoList` 링크, adal.js는 로그인에 대해 필요한 경우 AD tooAzure 리디렉션합니다 자동으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2318-146">Now when a user clicks hello `TodoList` link, adal.js will automatically redirect tooAzure AD for sign-in if necessary.</span></span>  <span data-ttu-id="d2318-147">컨트롤러에서 adal.js를 호출하여 명시적으로 로그인 및 로그아웃 요청을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2318-147">You can also explicitly send sign-in and sign-out requests by invoking adal.js in your controllers:</span></span>

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

## <a name="display-user-info"></a><span data-ttu-id="d2318-148">사용자 정보 표시</span><span class="sxs-lookup"><span data-stu-id="d2318-148">Display user info</span></span>
<span data-ttu-id="d2318-149">Hello 사용자가 로그인 했으므로 응용 프로그램에 tooaccess hello 로그인 한 사용자의 인증 데이터를 아마도 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2318-149">Now that hello user is signed in, you'll probably need tooaccess hello signed-in user's authentication data in your application.</span></span>  <span data-ttu-id="d2318-150">Adal.js hello에이 정보를 노출 `userInfo` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="d2318-150">Adal.js exposes this information for you in hello `userInfo` object.</span></span>  <span data-ttu-id="d2318-151">tooaccess 뷰에서이 개체에는 먼저 hello 해당 컨트롤러의 adal.js toohello 루트 범위 추가:</span><span class="sxs-lookup"><span data-stu-id="d2318-151">tooaccess this object in a view, first add adal.js toohello root scope of hello corresponding controller:</span></span>

```js
// app/scripts/userDataCtrl.js

angular.module('todoApp')
// Load ADAL for use in view
.controller('userDataCtrl', ['$scope', 'adalAuthenticationService', function ($scope, adalService) {}]);
```

<span data-ttu-id="d2318-152">Hello를 직접 처리 한 다음 `userInfo` 보기에서 개체:</span><span class="sxs-lookup"><span data-stu-id="d2318-152">Then you can directly address hello `userInfo` object in your view:</span></span> 

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

<span data-ttu-id="d2318-153">Hello를 사용할 수도 있습니다 `userInfo` hello 사용자의 로그인 한 경우 toodetermine 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="d2318-153">You can also use hello `userInfo` object toodetermine if hello user is signed in or not.</span></span>

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

## <a name="call-hello-rest-api"></a><span data-ttu-id="d2318-154">Hello REST API를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2318-154">Call hello REST API</span></span>
<span data-ttu-id="d2318-155">마지막으로 일부 토큰 및 호출 REST API toocreate hello, 읽기, 업데이트 및 삭제 작업의 시간 tooget를입니다.</span><span class="sxs-lookup"><span data-stu-id="d2318-155">Finally, it's time tooget some tokens and call hello REST API toocreate, read, update, and delete tasks.</span></span>  <span data-ttu-id="d2318-156">무엇이 필요할까요?</span><span class="sxs-lookup"><span data-stu-id="d2318-156">Well guess what?</span></span>  <span data-ttu-id="d2318-157">Toodo 없는 *사물*합니다.</span><span class="sxs-lookup"><span data-stu-id="d2318-157">You don't have toodo *a thing*.</span></span>  <span data-ttu-id="d2318-158">Adal.js에서 토큰 가져오기, 캐싱, 새로 고침 작업을 자동으로 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="d2318-158">Adal.js will automatically take care of getting, caching, and refreshing tokens.</span></span>  <span data-ttu-id="d2318-159">또한 자동으로 수행 됩니다 toooutgoing AJAX 요청 toohello REST API를 보내 해당 토큰을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2318-159">It will also take care of attaching those tokens toooutgoing AJAX requests that you send toohello REST API.</span></span>  

<span data-ttu-id="d2318-160">작동 원리는 바로 이렇습니다.</span><span class="sxs-lookup"><span data-stu-id="d2318-160">How exactly does this work?</span></span> <span data-ttu-id="d2318-161">모든 감사 toohello 매직은 [AngularJS 인터셉터](https://docs.angularjs.org/api/ng/service/$http), adal.js tootransform 들어오고 나가는 http 메시지 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2318-161">It's all thanks toohello magic of [AngularJS interceptors](https://docs.angularjs.org/api/ng/service/$http), which allows adal.js tootransform outgoing and incoming http messages.</span></span>  <span data-ttu-id="d2318-162">또한 adal.js 가정는 모든 요청 toohello를 전송 하는 동일한 도메인 hello 창을 위한 토큰을 사용 해야 하는 대로 hello 응용 프로그램 ID 같은 hello AngularJS 앱으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2318-162">Furthermore, adal.js assumes that any requests send toohello same domain as hello window should use tokens intended for hello same Application ID as hello AngularJS app.</span></span>  <span data-ttu-id="d2318-163">이 때문에 hello 사용 hello NodeJS REST API 및 hello 각도 앱 모두에 동일한 응용 프로그램 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="d2318-163">This is why we used hello same Application ID in both hello Angular app and in hello NodeJS REST API.</span></span>  <span data-ttu-id="d2318-164">물론,이 동작을 재정의 하 고 adal.js tooget 토큰-필요한 경우 다른 REST Api에 대 한 알 수 있지만이 간단한 시나리오 hello 기본값 작업으로 충분 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2318-164">Of course, you can override this behavior and tell adal.js tooget tokens for other REST APIs if necessary - but for this simple scenario hello defaults will do.</span></span>

<span data-ttu-id="d2318-165">얼마나 쉬운지 Azure AD에서 전달자 토큰을 사용 하 여 toosend 요청을 보여 주는 코드 조각은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d2318-165">Here's a snippet that shows how easy it is toosend requests with bearer tokens from Azure AD:</span></span>

```js
// app/scripts/todoListSvc.js

...
return $http.get('/api/tasks');
...
```

<span data-ttu-id="d2318-166">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="d2318-166">Congratulations!</span></span>  <span data-ttu-id="d2318-167">Azure AD 통합 단일 페이지 앱이 완성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d2318-167">Your Azure AD integrated single page app is now complete.</span></span>  <span data-ttu-id="d2318-168">수고 많으셨습니다.</span><span class="sxs-lookup"><span data-stu-id="d2318-168">Go ahead, take a bow.</span></span>  <span data-ttu-id="d2318-169">수 사용자 인증, 안전 하 게 해당 백 엔드 OpenID Connect를 사용 하 여 REST API를 호출 하 고 hello 사용자에 대 한 기본 정보를 얻을 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2318-169">It can authenticate users, securely call its backend REST API using OpenID Connect, and get basic information about hello user.</span></span>  <span data-ttu-id="d2318-170">Hello 초기 개인 Microsoft 계정 또는 Azure AD에서 작업/학교 계정이 있는 모든 사용자를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d2318-170">Out of hello box, it supports any user with a personal Microsoft Account or a work/school account from Azure AD.</span></span>  <span data-ttu-id="d2318-171">실행 하 여 hello 앱 try를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2318-171">Give hello app a try by running:</span></span>

```
node server.js
```

<span data-ttu-id="d2318-172">브라우저에서 탐색 너무`http://localhost:8080`합니다.</span><span class="sxs-lookup"><span data-stu-id="d2318-172">In a browser navigate too`http://localhost:8080`.</span></span>  <span data-ttu-id="d2318-173">개인 Microsoft 계정 또는 회사/학교 계정을 사용하여 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="d2318-173">Sign in using either a personal Microsoft account or a work/school account.</span></span>  <span data-ttu-id="d2318-174">작업 toohello 사용자의 할 일 목록에 추가 하 고 로그 아웃 합니다.  다른 유형의 계정 hello 시도 된에 서명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2318-174">Add tasks toohello user's to-do list, and sign out.  Try signing in with hello other type of account.</span></span> <span data-ttu-id="d2318-175">Azure AD 테 넌 트 toocreate 작업/학교 사용자 해야 할 경우 [자세한 방법을 tooget 한 여기](active-directory-howto-tenant.md) (가능한 경우).</span><span class="sxs-lookup"><span data-stu-id="d2318-175">If you need an Azure AD tenant toocreate work/school users, [learn how tooget one here](active-directory-howto-tenant.md) (it's free).</span></span>

<span data-ttu-id="d2318-176">hello에 대 한 학습 toocontinue v2.0 끝점 hello, 백 tooour 헤드 [v2.0 개발자 가이드](active-directory-appmodel-v2-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d2318-176">toocontinue learning about hello hello v2.0 endpoint, head back tooour [v2.0 developer guide](active-directory-appmodel-v2-overview.md).</span></span>  <span data-ttu-id="d2318-177">추가 리소스는 다음을 확인해보세요.</span><span class="sxs-lookup"><span data-stu-id="d2318-177">For additional resources, check out:</span></span>

* [<span data-ttu-id="d2318-178">GitHub의 Azure 샘플(영문) >></span><span class="sxs-lookup"><span data-stu-id="d2318-178">Azure-Samples on GitHub >></span></span>](https://github.com/Azure-Samples)
* [<span data-ttu-id="d2318-179">스택 오버플로의 Azure AD(영문) >></span><span class="sxs-lookup"><span data-stu-id="d2318-179">Azure AD on Stack Overflow >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
* <span data-ttu-id="d2318-180">[Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)의 Azure AD 설명서</span><span class="sxs-lookup"><span data-stu-id="d2318-180">Azure AD documentation on [Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)</span></span>

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="d2318-181">당사 제품에 대한 보안 업데이트 가져오기</span><span class="sxs-lookup"><span data-stu-id="d2318-181">Get security updates for our products</span></span>
<span data-ttu-id="d2318-182">보안 사고를 방문 하 여 발생 하는 경우의 알림 tooget 좋습니다 [이 페이지](https://technet.microsoft.com/security/dd252948) 및 tooSecurity 자문 경고를 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2318-182">We encourage you tooget notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>


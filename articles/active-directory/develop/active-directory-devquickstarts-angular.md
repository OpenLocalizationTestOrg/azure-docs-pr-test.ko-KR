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
# <a name="help-secure-angularjs-single-page-apps-by-using-azure-ad"></a><span data-ttu-id="b3c74-103">Azure AD를 사용하여 AngularJS 단일 페이지 앱 보안 지원</span><span class="sxs-lookup"><span data-stu-id="b3c74-103">Help secure AngularJS single-page apps by using Azure AD</span></span>

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="b3c74-104">Azure Active Directory (Azure AD)를 사용 하면 간단 하 고 tooadd 로그인, 로그 아웃에 대 한 간단한 보안 OAuth API 호출 tooyour 단일 페이지 응용 프로그램 및입니다.</span><span class="sxs-lookup"><span data-stu-id="b3c74-104">Azure Active Directory (Azure AD) makes it simple and straightforward for you tooadd sign-in, sign-out, and secure OAuth API calls tooyour single-page apps.</span></span>  <span data-ttu-id="b3c74-105">앱 tooauthenticate 사용자의 Windows Server Active Directory 계정 사용 하 고 모든 웹 보호 하는 Azure AD를 Office 365 Api hello 또는 hello Azure API와 같은 API를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c74-105">It enables your apps tooauthenticate users with their Windows Server Active Directory accounts and consume any web API that Azure AD helps protect, such as hello Office 365 APIs or hello Azure API.</span></span>

<span data-ttu-id="b3c74-106">브라우저에서 실행 되는 JavaScript 응용 프로그램에 대 한 Azure AD는 hello 제공 adal.js 또는 Active Directory 인증 라이브러리 (ADAL).</span><span class="sxs-lookup"><span data-stu-id="b3c74-106">For JavaScript applications running in a browser, Azure AD provides hello Active Directory Authentication Library (ADAL), or adal.js.</span></span> <span data-ttu-id="b3c74-107">hello adal.js는 목적 toomake 사용자가 앱 tooget 액세스 토큰을 쉽게 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c74-107">hello sole purpose of adal.js is toomake it easy for your app tooget access tokens.</span></span> <span data-ttu-id="b3c74-108">이면 작업이 얼마나 쉬운지 toodemonstrate 여기 빌드합니다 AngularJS tooDo 목록 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="b3c74-108">toodemonstrate just how easy it is, here we'll build an AngularJS tooDo List application that:</span></span>

* <span data-ttu-id="b3c74-109">Hello id 공급자로 Azure AD를 사용 하 여 toohello 응용 프로그램에서 기호 hello 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="b3c74-109">Signs hello user in toohello app by using Azure AD as hello identity provider.</span></span>

* <span data-ttu-id="b3c74-110">Hello 사용자에 대 한 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c74-110">Displays some information about hello user.</span></span>
* <span data-ttu-id="b3c74-111">안전 하 게 호출 응용 프로그램의 tooDo 목록 API를 Azure AD에서 전달자 토큰을 사용 하 여 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c74-111">Securely calls hello app's tooDo List API by using bearer tokens from Azure AD.</span></span>
* <span data-ttu-id="b3c74-112">기호 hello hello 앱에서 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="b3c74-112">Signs hello user out of hello app.</span></span>

<span data-ttu-id="b3c74-113">toobuild hello 완료 작업 응용 프로그램을 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c74-113">toobuild hello complete, working application, you need to:</span></span>

1. <span data-ttu-id="b3c74-114">Azure AD에 앱을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c74-114">Register your app with Azure AD.</span></span>
2. <span data-ttu-id="b3c74-115">ADAL을 설치 하 고 hello 단일 페이지 응용 프로그램을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c74-115">Install ADAL and configure hello single-page app.</span></span>
3. <span data-ttu-id="b3c74-116">Hello 단일 페이지 응용 프로그램에서 ADAL toohelp 보안 페이지를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c74-116">Use ADAL toohelp secure pages in hello single-page app.</span></span>

<span data-ttu-id="b3c74-117">시작 tooget [hello 응용 프로그램의 기본 정의 다운로드](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) 또는 [완료 hello 샘플 다운로드](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip)합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c74-117">tooget started, [download hello app skeleton](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) or [download hello completed sample](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="b3c74-118">또한 사용자를 만들고 응용 프로그램을 등록할 수 있는 Azure AD 테넌트도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c74-118">You also need an Azure AD tenant in which you can create users and register an application.</span></span> <span data-ttu-id="b3c74-119">테 넌 트 아직 없는 경우 [자세한 방법을 하나 tooget](active-directory-howto-tenant.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c74-119">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

## <a name="step-1-register-hello-directorysearcher-application"></a><span data-ttu-id="b3c74-120">1 단계: hello DirectorySearcher 응용 프로그램 등록</span><span class="sxs-lookup"><span data-stu-id="b3c74-120">Step 1: Register hello DirectorySearcher application</span></span>
<span data-ttu-id="b3c74-121">tooenable tooauthenticate 사용자 응용 프로그램 및 get 토큰을 먼저 tooregister에서 Azure AD 테 넌 트:</span><span class="sxs-lookup"><span data-stu-id="b3c74-121">tooenable your app tooauthenticate users and get tokens, you first need tooregister it in your Azure AD tenant:</span></span>

1. <span data-ttu-id="b3c74-122">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c74-122">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b3c74-123">Toomultiple 디렉터리에 로그인 한 경우에 hello 올바른 디렉터리를 보려는 tooensure를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3c74-123">If you are signed in toomultiple directories, you may need tooensure you are viewing hello correct directory.</span></span> <span data-ttu-id="b3c74-124">toodo 따라서 hello 위쪽 막대에서 계정을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c74-124">toodo so, on hello top bar, click your account.</span></span> <span data-ttu-id="b3c74-125">Hello에서 **디렉터리** 목록 tooregister 원하는 hello Azure AD 테 넌 트 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c74-125">Under hello **Directory** list, choose hello Azure AD tenant where you want tooregister your application.</span></span>
3. <span data-ttu-id="b3c74-126">클릭 **더 서비스** 에 hello 왼쪽된 창에서 선택한 후 **Azure Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c74-126">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="b3c74-127">**앱 등록**을 클릭하고 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c74-127">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="b3c74-128">Hello 화면에 따라 수행 하 고 새 웹 응용 프로그램 및/또는 web API를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b3c74-128">Follow hello prompts and create a new web application and/or web API:</span></span>
  * <span data-ttu-id="b3c74-129">**이름** 응용 프로그램 toousers에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c74-129">**Name** describes your application toousers.</span></span>
  * <span data-ttu-id="b3c74-130">**리디렉션 Uri** 는 hello 위치 toowhich Azure AD 토큰을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c74-130">**Redirect Uri** is hello location toowhich Azure AD will return tokens.</span></span> <span data-ttu-id="b3c74-131">이 샘플에 대 한 hello 기본 위치는 `https://localhost:44326/`합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c74-131">hello default location for this sample is `https://localhost:44326/`.</span></span>
6. <span data-ttu-id="b3c74-132">등록을 완료 한 후 Azure AD는 고유한 응용 프로그램 ID tooyour 응용 프로그램에 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c74-132">After you finish registration, Azure AD assigns a unique application ID tooyour app.</span></span>  <span data-ttu-id="b3c74-133">이 값이 필요 합니다 hello 다음 섹션의 하므로에서 복사 hello 응용 프로그램 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c74-133">You'll need this value in hello next sections, so copy it from hello application tab.</span></span>
7. <span data-ttu-id="b3c74-134">Adal.js를 Azure AD OAuth 암시적 흐름 toocommunicate hello를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c74-134">Adal.js uses hello OAuth implicit flow toocommunicate with Azure AD.</span></span> <span data-ttu-id="b3c74-135">응용 프로그램에 대 한 hello 암시적 흐름을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c74-135">You must enable hello implicit flow for your application:</span></span>
  1. <span data-ttu-id="b3c74-136">Hello 응용 프로그램을 클릭 하 고 선택 **매니페스트** tooopen hello 인라인 매니페스트 편집기입니다.</span><span class="sxs-lookup"><span data-stu-id="b3c74-136">Click hello application and select **Manifest** tooopen hello inline manifest editor.</span></span>
  2. <span data-ttu-id="b3c74-137">Hello 찾을 `oauth2AllowImplicitFlow` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="b3c74-137">Locate hello `oauth2AllowImplicitFlow` property.</span></span> <span data-ttu-id="b3c74-138">해당 값을 너무 설정`true`합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c74-138">Set its value too`true`.</span></span>
  3. <span data-ttu-id="b3c74-139">클릭 **저장** toosave hello 매니페스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c74-139">Click **Save** toosave hello manifest.</span></span>
8. <span data-ttu-id="b3c74-140">응용 프로그램에 대해 테넌트 전체에서 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c74-140">Grant permissions across your tenant for your application.</span></span> <span data-ttu-id="b3c74-141">너무 이동**설정** > **속성** > **필요한 권한**, hello 클릭 **사용 권한 부여**hello 위쪽 막대 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="b3c74-141">Go too**Settings** > **Properties** > **Required Permissions**, and click hello **Grant Permissions** button on hello top bar.</span></span> <span data-ttu-id="b3c74-142">클릭 **예** tooconfirm 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c74-142">Click **Yes** tooconfirm.</span></span>

## <a name="step-2-install-adal-and-configure-hello-single-page-app"></a><span data-ttu-id="b3c74-143">2 단계: ADAL 설치 하 고 hello 단일 페이지 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="b3c74-143">Step 2: Install ADAL and configure hello single-page app</span></span>
<span data-ttu-id="b3c74-144">Azure AD에서 응용 프로그램이 있으므로 adal.js를 설치하고 ID 관련 코드를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3c74-144">Now that you have an application in Azure AD, you can install adal.js and write your identity-related code.</span></span>

### <a name="configure-hello-javascript-client"></a><span data-ttu-id="b3c74-145">Hello JavaScript 클라이언트 구성</span><span class="sxs-lookup"><span data-stu-id="b3c74-145">Configure hello JavaScript client</span></span>
<span data-ttu-id="b3c74-146">Hello 패키지 관리자 콘솔을 사용 하 여 adal.js toohello TodoSPA 프로젝트를 추가 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c74-146">Begin by adding adal.js toohello TodoSPA project by using hello Package Manager Console:</span></span>
  1. <span data-ttu-id="b3c74-147">다운로드 [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal.js) toohello 추가 `App/Scripts/` 프로젝트 디렉터리.</span><span class="sxs-lookup"><span data-stu-id="b3c74-147">Download [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal.js) and add it toohello `App/Scripts/` project directory.</span></span>
  2. <span data-ttu-id="b3c74-148">다운로드 [adal angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal-angular.js) toohello 추가 `App/Scripts/` 프로젝트 디렉터리.</span><span class="sxs-lookup"><span data-stu-id="b3c74-148">Download [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal-angular.js) and add it toohello `App/Scripts/` project directory.</span></span>
  3. <span data-ttu-id="b3c74-149">각 스크립트의 hello hello 종료 하기 전에 로드 `</body>` 에 `index.html`:</span><span class="sxs-lookup"><span data-stu-id="b3c74-149">Load each script before hello end of hello `</body>` in `index.html`:</span></span>

    ```js
    ...
    <script src="App/Scripts/adal.js"></script>
    <script src="App/Scripts/adal-angular.js"></script>
    ...
    ```

### <a name="configure-hello-back-end-server"></a><span data-ttu-id="b3c74-150">Hello 백 엔드 서버 구성</span><span class="sxs-lookup"><span data-stu-id="b3c74-150">Configure hello back end server</span></span>
<span data-ttu-id="b3c74-151">Hello 단일 페이지 앱 백 엔드에서 tooDo 목록 API tooaccept 토큰 hello 브라우저에서에 대 한 hello 백 엔드는 hello 응용 프로그램 등록에 대 한 구성 정보가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c74-151">For hello single-page app's back-end tooDo List API tooaccept tokens from hello browser, hello back end needs configuration information about hello app registration.</span></span> <span data-ttu-id="b3c74-152">Hello TodoSPA 프로젝트를 열고 `web.config`합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c74-152">In hello TodoSPA project, open `web.config`.</span></span> <span data-ttu-id="b3c74-153">Hello에 hello 요소 hello 값 바꾸기 `<appSettings>` tooreflect hello 값 값 섹션에서 사용한 hello Azure 포털입니다.</span><span class="sxs-lookup"><span data-stu-id="b3c74-153">Replace hello values of hello elements in hello `<appSettings>` section tooreflect hello values that you used in hello Azure portal.</span></span> <span data-ttu-id="b3c74-154">코드는 ADAL을 사용할 때마다 이러한 값을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c74-154">Your code will reference these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="b3c74-155">`ida:Tenant`Azure AD 테 넌 트의-예를 들어 contoso.onmicrosoft.com hello 도메인이입니다.</span><span class="sxs-lookup"><span data-stu-id="b3c74-155">`ida:Tenant` is hello domain of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="b3c74-156">`ida:Audience`hello hello 포털에서 복사 하는 응용 프로그램 클라이언트 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="b3c74-156">`ida:Audience` is hello client ID of your application that you copied from hello portal.</span></span>

## <a name="step-3-use-adal-toohelp-secure-pages-in-hello-single-page-app"></a><span data-ttu-id="b3c74-157">3 단계: 사용 하 여 ADAL toohelp hello 단일 페이지 응용 프로그램의 보안 페이지</span><span class="sxs-lookup"><span data-stu-id="b3c74-157">Step 3: Use ADAL toohelp secure pages in hello single-page app</span></span>
<span data-ttu-id="b3c74-158">Adal.js는 AngularJS 경로 및 HTTP 공급자와 통합되므로 단일 페이지 앱에서 개별 뷰의 보안을 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3c74-158">Adal.js integrates with AngularJS route and HTTP providers, so you can help secure individual views in your single-page app.</span></span>

1. <span data-ttu-id="b3c74-159">`App/Scripts/app.js`, hello adal.js 모듈 가져오기:</span><span class="sxs-lookup"><span data-stu-id="b3c74-159">In `App/Scripts/app.js`, bring in hello adal.js module:</span></span>

    ```js
    angular.module('todoApp', ['ngRoute','AdalAngular'])
    .config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
     function ($routeProvider, $httpProvider, adalProvider) {
    ...
    ```
2. <span data-ttu-id="b3c74-160">초기화 `adalProvider` 에 프로그램 응용 프로그램 등록의 hello 구성 값을 사용 하 여 `App/Scripts/app.js`:</span><span class="sxs-lookup"><span data-stu-id="b3c74-160">Initialize `adalProvider` by using hello configuration values of your application registration, also in `App/Scripts/app.js`:</span></span>

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
3. <span data-ttu-id="b3c74-161">보안 hello 도움말 `TodoList` 한 줄의 코드를 사용 하 여 hello 앱에서 보기: `requireADLogin`합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c74-161">Help secure hello `TodoList` view in hello app by using only one line of code: `requireADLogin`.</span></span>

    ```js
    ...
    }).when("/TodoList", {
            controller: "todoListCtrl",
            templateUrl: "/App/Views/TodoList.html",
            requireADLogin: true,
    ...
    ```

## <a name="summary"></a><span data-ttu-id="b3c74-162">요약</span><span class="sxs-lookup"><span data-stu-id="b3c74-162">Summary</span></span>
<span data-ttu-id="b3c74-163">이제 사용자가 로그인 하 고 요청 전달자 토큰 보호 tooits 백 엔드 API를 발급할 수 있는 안전한 단일 페이지 앱을 준비 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b3c74-163">You now have a secure single-page app that can sign in users and issue bearer-token-protected requests tooits back-end API.</span></span> <span data-ttu-id="b3c74-164">Hello 클릭 하면 **TodoList** 링크, adal.js는 로그인에 대해 필요한 경우 AD tooAzure 리디렉션합니다 자동으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c74-164">When a user clicks hello **TodoList** link, adal.js will automatically redirect tooAzure AD for sign-in if necessary.</span></span> <span data-ttu-id="b3c74-165">또한 adal.js에서 자동으로 액세스 토큰 tooany Ajax 요청 toohello 앱 백 엔드 보낸 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3c74-165">In addition, adal.js will automatically attach an access token tooany Ajax requests that are sent toohello app's back end.</span></span>  

<span data-ttu-id="b3c74-166">hello 앞 단계는 hello 완전 최소 필요한 toobuild 단일 페이지 앱 adal.js를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c74-166">hello preceding steps are hello bare minimum necessary toobuild a single-page app by using adal.js.</span></span> <span data-ttu-id="b3c74-167">하지만 단일 페이지 앱에서 유용한 몇 가지 다른 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3c74-167">But a few other features are useful in single-page app:</span></span>

* <span data-ttu-id="b3c74-168">tooexplicitly 로그인 및 로그 아웃 요청을 실행할 adal.js를 호출 하는 컨트롤러에서 함수를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3c74-168">tooexplicitly issue sign-in and sign-out requests, you can define functions in your controllers that invoke adal.js.</span></span>  <span data-ttu-id="b3c74-169">`App/Scripts/homeCtrl.js`:</span><span class="sxs-lookup"><span data-stu-id="b3c74-169">In `App/Scripts/homeCtrl.js`:</span></span>

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
* <span data-ttu-id="b3c74-170">Hello 응용 프로그램의 UI에서 toopresent 사용자 정보를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3c74-170">You might want toopresent user information in hello app's UI.</span></span> <span data-ttu-id="b3c74-171">hello ADAL 서비스 이미 추가 되어 toohello `userDataCtrl` hello에 액세스할 수 있도록 컨트롤러 `userInfo` hello에 개체 관련 보기, `App/Views/UserData.html`:</span><span class="sxs-lookup"><span data-stu-id="b3c74-171">hello ADAL service has already been added toohello `userDataCtrl` controller, so you can access hello `userInfo` object in hello associated view, `App/Views/UserData.html`:</span></span>

    ```js
    <p>{{userInfo.userName}}</p>
    <p>aud:{{userInfo.profile.aud}}</p>
    <p>iss:{{userInfo.profile.iss}}</p>
    ...
    ```

* <span data-ttu-id="b3c74-172">에 있는 합니다 tooknow hello 사용자의 로그인 한 경우 많은 시나리오가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3c74-172">There are many scenarios in which you'll want tooknow if hello user is signed in or not.</span></span> <span data-ttu-id="b3c74-173">Hello를 사용할 수도 있습니다 `userInfo` toogather이이 정보 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="b3c74-173">You can also use hello `userInfo` object toogather this information.</span></span>  <span data-ttu-id="b3c74-174">예를 들어, `index.html`, 어느 hello를 표시할 수 있습니다 **로그인** 또는 **로그 아웃** 인증 상태에 따라 단추:</span><span class="sxs-lookup"><span data-stu-id="b3c74-174">For instance, in `index.html`, you can show either hello **Login** or **Logout** button based on authentication status:</span></span>

    ```js
    <li><a class="btn btn-link" ng-show="userInfo.isAuthenticated" ng-click="logout()">Logout</a></li>
    <li><a class="btn btn-link" ng-hide=" userInfo.isAuthenticated" ng-click="login()">Login</a></li>
    ```

<span data-ttu-id="b3c74-175">Azure AD에 통합 된 단일 페이지 응용 프로그램 인증 사용자, 안전 하 게 OAuth 2.0을 사용 하 여 해당 백 엔드를 호출 하 고 수 hello 사용자에 대 한 기본 정보를 얻을 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c74-175">Your Azure AD-integrated single-page app can authenticate users, securely call its back end by using OAuth 2.0, and get basic information about hello user.</span></span> <span data-ttu-id="b3c74-176">아직 하지 않는 이제 경우 hello 시간 toopopulate 사용자로 구성 된 테 넌 트입니다.</span><span class="sxs-lookup"><span data-stu-id="b3c74-176">If you haven't already, now is hello time toopopulate your tenant with some users.</span></span> <span data-ttu-id="b3c74-177">TooDo 목록 단일 페이지 응용 프로그램을 실행 하 고 해당 사용자 중 하나를 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c74-177">Run your tooDo List single-page app, and sign in with one of those users.</span></span> <span data-ttu-id="b3c74-178">작업 toohello 사용자의 할 일 목록 추가, 로그 아웃 하 고 다시 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c74-178">Add tasks toohello user's to-do list, sign out, and sign back in.</span></span>

<span data-ttu-id="b3c74-179">Adal.js를 응용 프로그램으로 쉽게 tooincorporate 일반적인 id 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3c74-179">Adal.js makes it easy tooincorporate common identity features into your application.</span></span> <span data-ttu-id="b3c74-180">사용자에 대 한 모든 hello dirty 작업은 담당: 캐시 관리, OAuth 프로토콜 지원 등 hello 사용자는 로그인 UI, 만료 된 토큰 등을 새로 고치면 제시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c74-180">It takes care of all hello dirty work for you: cache management, OAuth protocol support, presenting hello user with a sign-in UI, refreshing expired tokens, and more.</span></span>

<span data-ttu-id="b3c74-181">구성 값) (없이 hello 완료 샘플은에서 사용할 수 있는 참조를 위해 [GitHub](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip)합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c74-181">For reference, hello completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b3c74-182">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b3c74-182">Next steps</span></span>
<span data-ttu-id="b3c74-183">이제 tooadditional 시나리오에 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3c74-183">You can now move on tooadditional scenarios.</span></span> <span data-ttu-id="b3c74-184">Tootry 할 수 있습니다: [단일 페이지 앱에서 CORS web API를 호출할](https://github.com/AzureAdSamples/SinglePageApp-WebAPI-AngularJS-DotNet)합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c74-184">You might want tootry: [Call a CORS web API from a single-page app](https://github.com/AzureAdSamples/SinglePageApp-WebAPI-AngularJS-DotNet).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

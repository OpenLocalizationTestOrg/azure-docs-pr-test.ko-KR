---
title: "Azure AD AngularJS 시작 | Microsoft 문서"
description: "로그인을 위해 Azure AD와 통합되고 OAuth를 사용하여 Azure AD로 보호되는 API를 호출하는 AngularJS 단일 페이지 응용 프로그램을 빌드하는 방법."
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
ms.openlocfilehash: 4153910bc03f112f84c26cda6f9c78f11028b934
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="help-secure-angularjs-single-page-apps-by-using-azure-ad"></a><span data-ttu-id="9cace-103">Azure AD를 사용하여 AngularJS 단일 페이지 앱 보안 지원</span><span class="sxs-lookup"><span data-stu-id="9cace-103">Help secure AngularJS single-page apps by using Azure AD</span></span>

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="9cace-104">Azure AD(Azure Active Directory)를 사용하면 단일 페이지 앱에 단순하고 간편하게 로그인, 로그아웃 및 보안 OAuth API 호출을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-104">Azure Active Directory (Azure AD) makes it simple and straightforward for you to add sign-in, sign-out, and secure OAuth API calls to your single-page apps.</span></span>  <span data-ttu-id="9cace-105">또한 앱에서 Windows Server Active Directory 계정으로 사용자를 인증하고 Azure AD를 통해 보호되는 Web API(예: Office 365 API) 또는 Azure API를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-105">It enables your apps to authenticate users with their Windows Server Active Directory accounts and consume any web API that Azure AD helps protect, such as the Office 365 APIs or the Azure API.</span></span>

<span data-ttu-id="9cace-106">브라우저에서 실행되는 JavaScript 응용 프로그램의 경우 Azure AD가 ADAL(Active Directory 인증 라이브러리) 또는 adal.js를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-106">For JavaScript applications running in a browser, Azure AD provides the Active Directory Authentication Library (ADAL), or adal.js.</span></span> <span data-ttu-id="9cace-107">adal.js의 유일한 용도는 앱이 쉽게 액세스 토큰을 가져오도록 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-107">The sole purpose of adal.js is to make it easy for your app to get access tokens.</span></span> <span data-ttu-id="9cace-108">이 작업이 얼마나 쉬운지 보여 주기 위해 여기서는 다음 작업을 수행하는 AngularJS To Do List 응용 프로그램을 빌드할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-108">To demonstrate just how easy it is, here we'll build an AngularJS To Do List application that:</span></span>

* <span data-ttu-id="9cace-109">Azure AD를 ID 공급자로 사용하여 사용자를 앱에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-109">Signs the user in to the app by using Azure AD as the identity provider.</span></span>

* <span data-ttu-id="9cace-110">사용자에 대한 일부 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-110">Displays some information about the user.</span></span>
* <span data-ttu-id="9cace-111">Azure AD의 전달자 토큰을 사용하여 앱의 To Do List API를 안전하게 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-111">Securely calls the app's To Do List API by using bearer tokens from Azure AD.</span></span>
* <span data-ttu-id="9cace-112">앱에서 사용자를 로그아웃합니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-112">Signs the user out of the app.</span></span>

<span data-ttu-id="9cace-113">완전하게 작동하는 응용 프로그램을 빌드하려면 다음 작업이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-113">To build the complete, working application, you need to:</span></span>

1. <span data-ttu-id="9cace-114">Azure AD에 앱을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-114">Register your app with Azure AD.</span></span>
2. <span data-ttu-id="9cace-115">ADAL을 설치하고 단일 페이지 앱을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-115">Install ADAL and configure the single-page app.</span></span>
3. <span data-ttu-id="9cace-116">ADAL을 사용하여 단일 페이지 앱에서 페이지 보안을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-116">Use ADAL to help secure pages in the single-page app.</span></span>

<span data-ttu-id="9cace-117">시작하려면 [앱 기본 사항을 다운로드](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/skeleton.zip)하거나 [완성된 샘플을 다운로드](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip)하세요.</span><span class="sxs-lookup"><span data-stu-id="9cace-117">To get started, [download the app skeleton](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) or [download the completed sample](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="9cace-118">또한 사용자를 만들고 응용 프로그램을 등록할 수 있는 Azure AD 테넌트도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-118">You also need an Azure AD tenant in which you can create users and register an application.</span></span> <span data-ttu-id="9cace-119">테넌트가 아직 없는 경우 [얻는 방법을 알아보세요](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="9cace-119">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

## <a name="step-1-register-the-directorysearcher-application"></a><span data-ttu-id="9cace-120">1단계: DirectorySearcher 응용 프로그램 등록</span><span class="sxs-lookup"><span data-stu-id="9cace-120">Step 1: Register the DirectorySearcher application</span></span>
<span data-ttu-id="9cace-121">앱에서 사용자를 인증하고 토큰을 가져올 수 있게 하려면 먼저 앱을 Azure AD 테넌트에 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-121">To enable your app to authenticate users and get tokens, you first need to register it in your Azure AD tenant:</span></span>

1. <span data-ttu-id="9cace-122">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-122">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9cace-123">여러 디렉터리에 로그인된 경우 올바른 디렉터리를 보고 있는지 확인해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-123">If you are signed in to multiple directories, you may need to ensure you are viewing the correct directory.</span></span> <span data-ttu-id="9cace-124">이렇게 하려면 위쪽 모음에서 계정을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-124">To do so, on the top bar, click your account.</span></span> <span data-ttu-id="9cace-125">**디렉터리** 목록에서 응용 프로그램을 등록할 Azure AD 테넌트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-125">Under the **Directory** list, choose the Azure AD tenant where you want to register your application.</span></span>
3. <span data-ttu-id="9cace-126">왼쪽 창에서 **더 많은 서비스**를 클릭하고 **Azure Active Directory**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-126">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="9cace-127">**앱 등록**을 클릭하고 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-127">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="9cace-128">프롬프트에 따라 새 웹 응용 프로그램 및/또는 Web API를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-128">Follow the prompts and create a new web application and/or web API:</span></span>
  * <span data-ttu-id="9cace-129">**이름**은 사용자에게 응용 프로그램을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-129">**Name** describes your application to users.</span></span>
  * <span data-ttu-id="9cace-130">**리디렉션 Uri**는 Azure AD가 토큰을 반환할 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-130">**Redirect Uri** is the location to which Azure AD will return tokens.</span></span> <span data-ttu-id="9cace-131">이 샘플의 기본 위치는 `https://localhost:44326/`입니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-131">The default location for this sample is `https://localhost:44326/`.</span></span>
6. <span data-ttu-id="9cace-132">등록을 완료한 후에는 Azure AD가 사용자 앱에 고유한 응용 프로그램 ID를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-132">After you finish registration, Azure AD assigns a unique application ID to your app.</span></span>  <span data-ttu-id="9cace-133">이 값은 다음 섹션에서 필요하므로 응용 프로그램 탭에서 복사해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-133">You'll need this value in the next sections, so copy it from the application tab.</span></span>
7. <span data-ttu-id="9cace-134">Adal.js는 OAuth 암시적 흐름을 사용하여 Azure AD와 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-134">Adal.js uses the OAuth implicit flow to communicate with Azure AD.</span></span> <span data-ttu-id="9cace-135">응용 프로그램에 대한 암시적 흐름을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-135">You must enable the implicit flow for your application:</span></span>
  1. <span data-ttu-id="9cace-136">응용 프로그램을 클릭하고 **매니페스트**를 선택하여 인라인 매니페스트 편집기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-136">Click the application and select **Manifest** to open the inline manifest editor.</span></span>
  2. <span data-ttu-id="9cace-137">`oauth2AllowImplicitFlow` 속성을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-137">Locate the `oauth2AllowImplicitFlow` property.</span></span> <span data-ttu-id="9cace-138">해당 값을 `true`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-138">Set its value to `true`.</span></span>
  3. <span data-ttu-id="9cace-139">**저장**을 클릭하여 매니페스트를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-139">Click **Save** to save the manifest.</span></span>
8. <span data-ttu-id="9cace-140">응용 프로그램에 대해 테넌트 전체에서 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-140">Grant permissions across your tenant for your application.</span></span> <span data-ttu-id="9cace-141">**설정** > **속성** > **필요한 권한**으로 이동하고 위쪽 막대에서 **권한 부여** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-141">Go to **Settings** > **Properties** > **Required Permissions**, and click the **Grant Permissions** button on the top bar.</span></span> <span data-ttu-id="9cace-142">**예** 를 클릭하여 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-142">Click **Yes** to confirm.</span></span>

## <a name="step-2-install-adal-and-configure-the-single-page-app"></a><span data-ttu-id="9cace-143">2단계: ADAL 설치 및 단일 페이지 앱 구성</span><span class="sxs-lookup"><span data-stu-id="9cace-143">Step 2: Install ADAL and configure the single-page app</span></span>
<span data-ttu-id="9cace-144">Azure AD에서 응용 프로그램이 있으므로 adal.js를 설치하고 ID 관련 코드를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-144">Now that you have an application in Azure AD, you can install adal.js and write your identity-related code.</span></span>

### <a name="configure-the-javascript-client"></a><span data-ttu-id="9cace-145">JavaScript 클라이언트 구성</span><span class="sxs-lookup"><span data-stu-id="9cace-145">Configure the JavaScript client</span></span>
<span data-ttu-id="9cace-146">먼저 패키지 관리자 콘솔을 사용하여 TodoSPA 프로젝트에 Adal.js를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-146">Begin by adding adal.js to the TodoSPA project by using the Package Manager Console:</span></span>
  1. <span data-ttu-id="9cace-147">[adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal.js)를 다운로드하여 `App/Scripts/` 프로젝트 디렉터리에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-147">Download [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal.js) and add it to the `App/Scripts/` project directory.</span></span>
  2. <span data-ttu-id="9cace-148">[adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal-angular.js)를 다운로드하여 `App/Scripts/` 프로젝트 디렉터리에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-148">Download [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal-angular.js) and add it to the `App/Scripts/` project directory.</span></span>
  3. <span data-ttu-id="9cace-149">`</body>` in `index.html`끝 이전에 각 스크립트를 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-149">Load each script before the end of the `</body>` in `index.html`:</span></span>

    ```js
    ...
    <script src="App/Scripts/adal.js"></script>
    <script src="App/Scripts/adal-angular.js"></script>
    ...
    ```

### <a name="configure-the-back-end-server"></a><span data-ttu-id="9cace-150">백 엔드 서버 구성</span><span class="sxs-lookup"><span data-stu-id="9cace-150">Configure the back end server</span></span>
<span data-ttu-id="9cace-151">단일 페이지 앱의 백 엔드 To Do List API가 브라우저에서 토큰을 수락하도록 하려면 백 엔드에 앱 등록에 대한 구성 정보가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-151">For the single-page app's back-end To Do List API to accept tokens from the browser, the back end needs configuration information about the app registration.</span></span> <span data-ttu-id="9cace-152">TodoSPA 프로젝트에서 `web.config`를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-152">In the TodoSPA project, open `web.config`.</span></span> <span data-ttu-id="9cace-153">Azure Portal에 사용한 값을 반영하도록 `<appSettings>` 섹션의 요소 값을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-153">Replace the values of the elements in the `<appSettings>` section to reflect the values that you used in the Azure portal.</span></span> <span data-ttu-id="9cace-154">코드는 ADAL을 사용할 때마다 이러한 값을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-154">Your code will reference these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="9cace-155">`ida:Tenant`는 Azure AD 테넌트의 도메인(예: contoso.onmicrosoft.com)입니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-155">`ida:Tenant` is the domain of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="9cace-156">`ida:Audience`는 포털에서 복사한 응용 프로그램의 클라이언트 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-156">`ida:Audience` is the client ID of your application that you copied from the portal.</span></span>

## <a name="step-3-use-adal-to-help-secure-pages-in-the-single-page-app"></a><span data-ttu-id="9cace-157">3단계: ADAL을 사용하여 단일 페이지 앱에서 페이지 보안 지원</span><span class="sxs-lookup"><span data-stu-id="9cace-157">Step 3: Use ADAL to help secure pages in the single-page app</span></span>
<span data-ttu-id="9cace-158">Adal.js는 AngularJS 경로 및 HTTP 공급자와 통합되므로 단일 페이지 앱에서 개별 뷰의 보안을 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-158">Adal.js integrates with AngularJS route and HTTP providers, so you can help secure individual views in your single-page app.</span></span>

1. <span data-ttu-id="9cace-159">`App/Scripts/app.js`에서 다음과 같이 adal.js 모듈을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-159">In `App/Scripts/app.js`, bring in the adal.js module:</span></span>

    ```js
    angular.module('todoApp', ['ngRoute','AdalAngular'])
    .config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
     function ($routeProvider, $httpProvider, adalProvider) {
    ...
    ```
2. <span data-ttu-id="9cace-160">`App/Scripts/app.js`에서도 응용 프로그램 등록의 구성 값을 사용하여 `adalProvider`를 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-160">Initialize `adalProvider` by using the configuration values of your application registration, also in `App/Scripts/app.js`:</span></span>

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
3. <span data-ttu-id="9cace-161">코드 줄 `requireADLogin` 하나만 사용하여 앱에서 `TodoList` 뷰의 보안을 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-161">Help secure the `TodoList` view in the app by using only one line of code: `requireADLogin`.</span></span>

    ```js
    ...
    }).when("/TodoList", {
            controller: "todoListCtrl",
            templateUrl: "/App/Views/TodoList.html",
            requireADLogin: true,
    ...
    ```

## <a name="summary"></a><span data-ttu-id="9cace-162">요약</span><span class="sxs-lookup"><span data-stu-id="9cace-162">Summary</span></span>
<span data-ttu-id="9cace-163">이제 사용자를 로그인하고 전달자 토큰으로 보호된 요청을 해당 백 엔드 API에 실행할 수 있는 보안 단일 페이지 앱을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-163">You now have a secure single-page app that can sign in users and issue bearer-token-protected requests to its back-end API.</span></span> <span data-ttu-id="9cace-164">사용자가 **TodoList** 링크를 클릭하면 adal.js는 필요한 경우 로그인을 위해 Azure AD에 자동으로 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-164">When a user clicks the **TodoList** link, adal.js will automatically redirect to Azure AD for sign-in if necessary.</span></span> <span data-ttu-id="9cace-165">또한 adal.js는 앱의 백 엔드로 전송되는 모든 Ajax 요청에 자동으로 액세스 토큰을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-165">In addition, adal.js will automatically attach an access token to any Ajax requests that are sent to the app's back end.</span></span>  

<span data-ttu-id="9cace-166">위의 단계는 adal.js를 사용하여 단일 페이지 앱을 빌드하는 데 필요한 최소 기본 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-166">The preceding steps are the bare minimum necessary to build a single-page app by using adal.js.</span></span> <span data-ttu-id="9cace-167">하지만 단일 페이지 앱에서 유용한 몇 가지 다른 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-167">But a few other features are useful in single-page app:</span></span>

* <span data-ttu-id="9cace-168">로그인 및 로그아웃 요청을 명시적으로 실행하기 위해 adal.js를 호출하는 컨트롤러에서 함수를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-168">To explicitly issue sign-in and sign-out requests, you can define functions in your controllers that invoke adal.js.</span></span>  <span data-ttu-id="9cace-169">`App/Scripts/homeCtrl.js`:</span><span class="sxs-lookup"><span data-stu-id="9cace-169">In `App/Scripts/homeCtrl.js`:</span></span>

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
* <span data-ttu-id="9cace-170">앱의 UI에 사용자 정보를 표시하려고 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-170">You might want to present user information in the app's UI.</span></span> <span data-ttu-id="9cace-171">ADAL 서비스가 `userDataCtrl` 컨트롤러에 이미 추가되었으므로 관련 뷰 `App/Views/UserData.html`에서 `userInfo` 개체에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-171">The ADAL service has already been added to the `userDataCtrl` controller, so you can access the `userInfo` object in the associated view, `App/Views/UserData.html`:</span></span>

    ```js
    <p>{{userInfo.userName}}</p>
    <p>aud:{{userInfo.profile.aud}}</p>
    <p>iss:{{userInfo.profile.iss}}</p>
    ...
    ```

* <span data-ttu-id="9cace-172">사용자가 로그인했는지 여부를 확인하고 싶은 경우가 많이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-172">There are many scenarios in which you'll want to know if the user is signed in or not.</span></span> <span data-ttu-id="9cace-173">`userInfo` 개체를 사용하여 이 정보를 수집할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-173">You can also use the `userInfo` object to gather this information.</span></span>  <span data-ttu-id="9cace-174">예를 들어 `index.html`에서는 인증 상태에 따라 **로그인** 또는 **로그아웃** 단추를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-174">For instance, in `index.html`, you can show either the **Login** or **Logout** button based on authentication status:</span></span>

    ```js
    <li><a class="btn btn-link" ng-show="userInfo.isAuthenticated" ng-click="logout()">Logout</a></li>
    <li><a class="btn btn-link" ng-hide=" userInfo.isAuthenticated" ng-click="login()">Login</a></li>
    ```

<span data-ttu-id="9cace-175">Azure AD 통합 단일 페이지 앱에서는 사용자를 인증하고, OAuth 2.0을 사용하여 해당 백 엔드를 안전하게 호출하고, 사용자에 대한 기본 정보를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-175">Your Azure AD-integrated single-page app can authenticate users, securely call its back end by using OAuth 2.0, and get basic information about the user.</span></span> <span data-ttu-id="9cace-176">아직 일부 사용자로 테넌트를 채우지 않은 경우 지금 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-176">If you haven't already, now is the time to populate your tenant with some users.</span></span> <span data-ttu-id="9cace-177">To Do List 단일 페이지 앱을 실행하고 해당 사용자 중 하나로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-177">Run your To Do List single-page app, and sign in with one of those users.</span></span> <span data-ttu-id="9cace-178">사용자의 할 일 목록에 작업을 추가하고, 사용자를 로그아웃했다가 다시 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-178">Add tasks to the user's to-do list, sign out, and sign back in.</span></span>

<span data-ttu-id="9cace-179">Adal.js는 응용 프로그램에 일반적인 ID 기능을 쉽게 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-179">Adal.js makes it easy to incorporate common identity features into your application.</span></span> <span data-ttu-id="9cace-180">또한 캐시 관리, OAuth 프로토콜 지원, 사용자에게 로그인 UI 제공, 만료된 토큰 새로 고침 등의 모든 귀찮은 작업을 관리해줍니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-180">It takes care of all the dirty work for you: cache management, OAuth protocol support, presenting the user with a sign-in UI, refreshing expired tokens, and more.</span></span>

<span data-ttu-id="9cace-181">참조를 위해 완성된 샘플(사용자 구성 값 제외)이 [GitHub](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip)에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-181">For reference, the completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9cace-182">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9cace-182">Next steps</span></span>
<span data-ttu-id="9cace-183">이제 추가 시나리오로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cace-183">You can now move on to additional scenarios.</span></span> <span data-ttu-id="9cace-184">다음 작업을 시도할 수 있습니다. [단일 페이지 앱에서 CORS Web API 호출](https://github.com/AzureAdSamples/SinglePageApp-WebAPI-AngularJS-DotNet).</span><span class="sxs-lookup"><span data-stu-id="9cace-184">You might want to try: [Call a CORS web API from a single-page app](https://github.com/AzureAdSamples/SinglePageApp-WebAPI-AngularJS-DotNet).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

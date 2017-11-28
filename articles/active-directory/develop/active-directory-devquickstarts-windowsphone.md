---
title: "aaaAzure AD Windows Phone 시작 | Microsoft Docs"
description: "어떻게 toobuild 로그인에 대 한 Azure AD와 통합 하 고 Azure AD를 호출 하는 Windows Phone 응용 프로그램 Api OAuth를 사용 하 여 보호 합니다."
services: active-directory
documentationcenter: windows
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 66f5ac20-5e1f-4b9d-bb99-9b3305e26416
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: e766bfcdfae10483772154f4b5facdec05fc846f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-a-windows-phone-app"></a><span data-ttu-id="42242-103">Azure AD와 Windows Phone 앱 통합</span><span class="sxs-lookup"><span data-stu-id="42242-103">Integrate Azure AD with a Windows Phone App</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

> [!NOTE]
> <span data-ttu-id="42242-104">Windows Phone 8.1 및 이전 버전 프로젝트는 Visual Studio 2017에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="42242-104">Windows Phone 8.1 and prior version projects are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="42242-105">자세한 내용은 [Visual Studio 2017 플랫폼 대상 지정 및 호환성](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="42242-105">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

<span data-ttu-id="42242-106">Windows Phone 8.1 앱을 개발 하는 경우 Azure AD는 간단 하 고 간단 하 게 하면 tooauthenticate 자신의 Active Directory 계정에 사용자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42242-106">If you're developing a Windows Phone 8.1 app, Azure AD makes it simple and straightforward for you tooauthenticate your users with their Active Directory accounts.</span></span>  <span data-ttu-id="42242-107">응용 프로그램 toosecurely 해줍니다 모든 웹 Azure AD로 보호 되는 API를 사용와 같은 Office 365 Api hello 또는 Azure API를 환영 합니다.</span><span class="sxs-lookup"><span data-stu-id="42242-107">It also enables your application toosecurely consume any web API protected by Azure AD, such as hello Office 365 APIs or hello Azure API.</span></span>

> [!NOTE]
> <span data-ttu-id="42242-108">이 코드 샘플에서는 ADAL v2.0을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="42242-108">This code sample uses ADAL v2.0.</span></span>  <span data-ttu-id="42242-109">Hello 최신 기술에 대 한 tooinstead try 경우가 우리의 [ADAL v 3.0을 사용 하 여 Windows 유니버설 자습서](active-directory-devquickstarts-windowsstore.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="42242-109">For hello latest technology, you may want tooinstead try our [Windows Universal Tutorial using ADAL v3.0](active-directory-devquickstarts-windowsstore.md).</span></span>  <span data-ttu-id="42242-110">Windows Phone 8.1 용 앱을 한 실제로 작성 하는 경우 hello 오른쪽 자리입니다.</span><span class="sxs-lookup"><span data-stu-id="42242-110">If you are indeed building an app for Windows Phone 8.1, this is hello right place.</span></span>  <span data-ttu-id="42242-111">ADAL v 2.0은 여전히 완전 하 게 지원 하 고는 hello 개발 앱 agianst Windows Phone 8.1의 권장된 방법을 사용 하 여 Azure AD.</span><span class="sxs-lookup"><span data-stu-id="42242-111">ADAL v2.0 is still fully supported, and is hello recommended way of developing apps agianst Windows Phone 8.1 using Azure AD.</span></span>
> 
> 

<span data-ttu-id="42242-112">.NET 네이티브 클라이언트의 tooaccess 보호 된 리소스를 필요로 하는 경우 Azure AD hello ADAL 또는 Active Directory 인증 라이브러리를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="42242-112">For .NET native clients that need tooaccess protected resources, Azure AD provides hello Active Directory Authentication Library, or ADAL.</span></span>  <span data-ttu-id="42242-113">생활에서 ADAL의 목적으로 toomake 사용자가 앱 tooget 액세스 토큰을 쉽게 합니다.</span><span class="sxs-lookup"><span data-stu-id="42242-113">ADAL’s sole purpose in life is toomake it easy for your app tooget access tokens.</span></span>  <span data-ttu-id="42242-114">얼마나 쉬운지 이면 toodemonstrate 여기 빌드합니다 "디렉터리 사용자" Windows Phone 8.1 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="42242-114">toodemonstrate just how easy it is, here we’ll build a "Directory Searcher" Windows Phone 8.1 app that:</span></span>

* <span data-ttu-id="42242-115">가져옵니다 hello를 사용 하 여 hello Azure AD Graph API 호출에 대 한 토큰에 액세스 [OAuth 2.0 인증 프로토콜](https://msdn.microsoft.com/library/azure/dn645545.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="42242-115">Gets access tokens for calling hello Azure AD Graph API using hello [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="42242-116">지정된 UPN을 가진 사용자를 디렉터리에서 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="42242-116">Searches a directory for users with a given UPN.</span></span>
* <span data-ttu-id="42242-117">사용자를 로그아웃합니다.</span><span class="sxs-lookup"><span data-stu-id="42242-117">Signs users out.</span></span>

<span data-ttu-id="42242-118">toobuild hello 완료 작업 응용 프로그램에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="42242-118">toobuild hello complete working application, you’ll need to:</span></span>

1. <span data-ttu-id="42242-119">Azure AD에 응용 프로그램을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="42242-119">Register your application with Azure AD.</span></span>
2. <span data-ttu-id="42242-120">ADAL을 설치 및 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="42242-120">Install & Configure ADAL.</span></span>
3. <span data-ttu-id="42242-121">Azure AD에서 ADAL tooget 토큰을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="42242-121">Use ADAL tooget tokens from Azure AD.</span></span>

<span data-ttu-id="42242-122">시작 tooget [기본 프로젝트를 다운로드](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/skeleton.zip) 또는 [완료 hello 샘플 다운로드](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip)합니다.</span><span class="sxs-lookup"><span data-stu-id="42242-122">tooget started, [download a skeleton project](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/skeleton.zip) or [download hello completed sample](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span></span>  <span data-ttu-id="42242-123">각 샘플은 Visual Studio 2013 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="42242-123">Each is a Visual Studio 2013 solution.</span></span>  <span data-ttu-id="42242-124">또한 사용자를 만들고 응용 프로그램을 등록할 수 있는 Azure AD 테넌트도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="42242-124">You'll also need an Azure AD tenant in which you can create users and register an application.</span></span>  <span data-ttu-id="42242-125">테 넌 트 아직 없는 경우 [자세한 방법을 하나 tooget](active-directory-howto-tenant.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="42242-125">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

## <a name="1-register-hello-directory-searcher-application"></a><span data-ttu-id="42242-126">1. Hello 디렉터리 검색 응용 프로그램 등록</span><span class="sxs-lookup"><span data-stu-id="42242-126">1. Register hello Directory Searcher Application</span></span>
<span data-ttu-id="42242-127">tooenable 먼저 해야 사용자가 앱 tooget 토큰 tooregister에서 Azure AD 테 넌 트 권한 tooaccess hello Azure AD Graph API에 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="42242-127">tooenable your app tooget tokens, you’ll first need tooregister it in your Azure AD tenant and grant it permission tooaccess hello Azure AD Graph API:</span></span>

1. <span data-ttu-id="42242-128">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="42242-128">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="42242-129">Hello 위쪽 막대에서 계정에 및 hello에서 클릭 **디렉터리** 목록에서 원하는 위치 tooregister 응용 프로그램 hello Active Directory 테 넌 트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="42242-129">On hello top bar, click on your account and under hello **Directory** list, choose hello Active Directory tenant where you wish tooregister your application.</span></span>
3. <span data-ttu-id="42242-130">클릭 **더 서비스** 왼쪽 nav hello와 선택 **Azure Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="42242-130">Click on **More Services** in hello left hand nav, and choose **Azure Active Directory**.</span></span>
4. <span data-ttu-id="42242-131">**앱 등록**을 클릭하고 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="42242-131">Click on **App registrations** and choose **Add**.</span></span>
5. <span data-ttu-id="42242-132">Hello 화면에 따라 수행 하 고 새 **네이티브 클라이언트 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="42242-132">Follow hello prompts and create a new **Native Client Application**.</span></span>
  * <span data-ttu-id="42242-133">hello **이름** 응용 프로그램의 hello 응용 프로그램 tooend-사용자가 설명 합니다</span><span class="sxs-lookup"><span data-stu-id="42242-133">hello **Name** of hello application will describe your application tooend-users</span></span>
  * <span data-ttu-id="42242-134">hello **리디렉션 Uri** 체계 및 문자열 조합 tooreturn 토큰 응답을 Azure AD에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="42242-134">hello **Redirect Uri** is a scheme and string combination that Azure AD will use tooreturn token responses.</span></span>  <span data-ttu-id="42242-135">지금은 자리 표시자 값(예: `http://DirectorySearcher`)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="42242-135">Enter a placeholder value for now, e.g. `http://DirectorySearcher`.</span></span>  <span data-ttu-id="42242-136">이 값은 나중에 바꿀 것입니다.</span><span class="sxs-lookup"><span data-stu-id="42242-136">We'll replace this value later.</span></span>
6. <span data-ttu-id="42242-137">등록을 완료하면 AAD는 앱에 고유한 응용 프로그램 ID를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="42242-137">Once you’ve completed registration, AAD will assign your app a unique Application ID.</span></span>  <span data-ttu-id="42242-138">이 값이 필요 합니다 hello 다음 섹션의 하므로에서 복사 hello 응용 프로그램 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="42242-138">You’ll need this value in hello next sections, so copy it from hello application tab.</span></span>
7. <span data-ttu-id="42242-139">Hello에서 **설정** 페이지에서 선택 **필요한 권한** 선택 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="42242-139">From hello **Settings** page, choose **Required Permissions** and choose **Add**.</span></span> <span data-ttu-id="42242-140">선택 hello **Microsoft Graph** 으로 hello를 더하고 API hello **디렉터리 데이터 읽기** 에 따른 권한 **위임 된 권한**합니다.</span><span class="sxs-lookup"><span data-stu-id="42242-140">Select hello **Microsoft Graph** as hello API and add hello **Read Directory Data** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="42242-141">이렇게 하면 응용 프로그램 tooquery hello Graph API 사용자에 대 한 활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="42242-141">This will enable your application tooquery hello Graph API for users.</span></span>

## <a name="2-install--configure-adal"></a><span data-ttu-id="42242-142">2. ADAL 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="42242-142">2. Install & Configure ADAL</span></span>
<span data-ttu-id="42242-143">Azure AD에서 응용 프로그램이 있으므로 ADAL을 설치하고 ID 관련 코드를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42242-143">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span></span>  <span data-ttu-id="42242-144">해야 tooprovide에서 Azure AD와 ADAL toobe 수 toocommunicate 사용 하 여 응용 프로그램 등록에 대 한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="42242-144">In order for ADAL toobe able toocommunicate with Azure AD, you need tooprovide it with some information about your app registration.</span></span>

* <span data-ttu-id="42242-145">Hello 패키지 관리자 콘솔을 사용 하 여 ADAL toohello DirectorySearcher 프로젝트를 추가 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="42242-145">Begin by adding ADAL toohello DirectorySearcher project using hello Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

* <span data-ttu-id="42242-146">Hello DirectorySearcher 프로젝트를 열고 `MainPage.xaml.cs`합니다.</span><span class="sxs-lookup"><span data-stu-id="42242-146">In hello DirectorySearcher project, open `MainPage.xaml.cs`.</span></span>  <span data-ttu-id="42242-147">Hello hello 값을 교체 `Config Values` 지역 tooreflect hello hello Azure 포털에 대 한 입력 값입니다.</span><span class="sxs-lookup"><span data-stu-id="42242-147">Replace hello values in hello `Config Values` region tooreflect hello values you input into hello Azure Portal.</span></span>  <span data-ttu-id="42242-148">코드는 ADAL을 사용할 때마다 이러한 값을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="42242-148">Your code will reference these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="42242-149">hello `tenant` hello 도메인은의 Azure AD 테 넌 트, 예: contoso.onmicrosoft.com</span><span class="sxs-lookup"><span data-stu-id="42242-149">hello `tenant` is hello domain of your Azure AD tenant, e.g. contoso.onmicrosoft.com</span></span>
  * <span data-ttu-id="42242-150">hello `clientId` hello 포털에서 복사 하는 응용 프로그램의 hello clientId 됩니다.</span><span class="sxs-lookup"><span data-stu-id="42242-150">hello `clientId` is hello clientId of your application you copied from hello portal.</span></span>
* <span data-ttu-id="42242-151">이제 Windows Phone 앱에 대 한 toodiscover hello 콜백 uri를 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="42242-151">You now need toodiscover hello callback uri for your Windows Phone app.</span></span>  <span data-ttu-id="42242-152">Hello에서이 줄에 중단점을 설정 `MainPage` 메서드:</span><span class="sxs-lookup"><span data-stu-id="42242-152">Set a breakpoint on this line in hello `MainPage` method:</span></span>

```
redirectURI = Windows.Security.Authentication.Web.WebAuthenticationBroker.GetCurrentApplicationCallbackUri();
```
* <span data-ttu-id="42242-153">Hello 응용 프로그램을 실행 하 고의 hello 값을 따로 복사 `redirectUri` hello 중단점이 적중 될 때입니다.</span><span class="sxs-lookup"><span data-stu-id="42242-153">Run hello app, and copy aside hello value of `redirectUri` when hello breakpoint is hit.</span></span>  <span data-ttu-id="42242-154">다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="42242-154">It should look something like</span></span>

```
ms-app://s-1-15-2-1352796503-54529114-405753024-3540103335-3203256200-511895534-1429095407/
```

* <span data-ttu-id="42242-155">Hello에 다시 **구성** hello Azure 관리 포털에서에서 응용 프로그램의 탭의 hello hello 값을 대체 **RedirectUri** 이 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="42242-155">Back on hello **Configure** tab of your application in hello Azure Management Portal, replace hello value of hello **RedirectUri** with this value.</span></span>  

## <a name="3-use-adal-tooget-tokens-from-aad"></a><span data-ttu-id="42242-156">3. AAD에서 ADAL tooGet 토큰 사용</span><span class="sxs-lookup"><span data-stu-id="42242-156">3. Use ADAL tooGet Tokens from AAD</span></span>
<span data-ttu-id="42242-157">hello ADAL 기본 원칙 되는 응용 프로그램 액세스 토큰을 필요할 때마다 단순히 호출 `authContext.AcquireToken(…)`, 및 ADAL rest hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="42242-157">hello basic principle behind ADAL is that whenever your app needs an access token, it simply calls `authContext.AcquireToken(…)`, and ADAL does hello rest.</span></span>  

* <span data-ttu-id="42242-158">hello 첫 번째 단계는 tooinitialize 앱의 `AuthenticationContext` -ADAL의 기본 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="42242-158">hello first step is tooinitialize your app’s `AuthenticationContext` - ADAL’s primary class.</span></span>  <span data-ttu-id="42242-159">이 ADAL을 전달 하는 Azure AD와 toocommunicate 필요한 좌표 hello 및 방법에 설명 toocache 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="42242-159">This is where you pass ADAL hello coordinates it needs toocommunicate with Azure AD and tell it how toocache tokens.</span></span>

```C#
public MainPage()
{
    ...

    // ADAL for Windows Phone 8.1 builds AuthenticationContext instances through a factory
    authContext = AuthenticationContext.CreateAsync(authority).GetResults();
}
```

* <span data-ttu-id="42242-160">이제 hello를 찾을 `Search(...)` 메서드 hello 사용자 cliks hello hello 응용 프로그램의 UI에서 "검색" 단추 때 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="42242-160">Now locate hello `Search(...)` method, which will be invoked when hello user cliks hello "Search" button in hello app's UI.</span></span>  <span data-ttu-id="42242-161">이 메서드는 해당 UPN 검색 단어를 지정 하는 hello로 시작 하는 사용자에 대 한 GET 요청 toohello Azure AD Graph API tooquery를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="42242-161">This method makes a GET request toohello Azure AD Graph API tooquery for users whose UPN begins with hello given search term.</span></span>  <span data-ttu-id="42242-162">순서 tooquery hello Graph API, tooinclude hello에서 access_token 필요 하지만 `Authorization` 이 경우에 ADAL-hello의 헤더를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="42242-162">But in order tooquery hello Graph API, you need tooinclude an access_token in hello `Authorization` header of hello request - this is where ADAL comes in.</span></span>

```C#
private async void Search(object sender, RoutedEventArgs e)
{
    ...

    // Try tooget a token without triggering any user prompt.
    // ADAL will check whether hello requested token is in ADAL's token cache or can otherwise be obtained without user interaction.
    AuthenticationResult result = await authContext.AcquireTokenSilentAsync(graphResourceId, clientId);
    if (result != null && result.Status == AuthenticationStatus.Success)
    {
        // A token was successfully retrieved.
        QueryGraph(result);
    }
    else
    {
        // Acquiring a token without user interaction was not possible.
        // Trigger an authentication experience and specify that once a token has been obtained hello QueryGraph method should be called
        authContext.AcquireTokenAndContinue(graphResourceId, clientId, redirectURI, QueryGraph);
    }
}
```
* <span data-ttu-id="42242-163">대화형 인증이 필요한 경우 ADAL ´ ֲ Windows Phone 웹 인증 브로커 (WAB) 및 [연속 모델](http://www.cloudidentity.com/blog/2014/06/16/adal-for-windows-phone-8-1-deep-dive/) toodisplay hello Azure AD 로그인 페이지.</span><span class="sxs-lookup"><span data-stu-id="42242-163">If interactive authentication is necessary, ADAL will use Windows Phone's Web Authentication Broker (WAB) and [continuation model](http://www.cloudidentity.com/blog/2014/06/16/adal-for-windows-phone-8-1-deep-dive/) toodisplay hello Azure AD sign in page.</span></span>  <span data-ttu-id="42242-164">Hello 사용자가 로그인 하면 응용 프로그램의 hello WAB 상호 작용 toopass ADAL hello 결과 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="42242-164">When hello user signs in, your app needs toopass ADAL hello results of hello WAB interaction.</span></span>  <span data-ttu-id="42242-165">Hello 구현으로 간단 하 게 `ContinueWebAuthentication` 인터페이스:</span><span class="sxs-lookup"><span data-stu-id="42242-165">This is as simple as implementing hello `ContinueWebAuthentication` interface:</span></span>

```C#
// This method is automatically invoked when hello application
// is reactivated after an authentication interaction through WebAuthenticationBroker.
public async void ContinueWebAuthentication(WebAuthenticationBrokerContinuationEventArgs args)
{
    // pass hello authentication interaction results tooADAL, which will
    // conclude hello token acquisition operation and invoke hello callback specified in AcquireTokenAndContinue.
    await authContext.ContinueAcquireTokenAsync(args);
}
```

* <span data-ttu-id="42242-166">이제 시간 toouse hello `AuthenticationResult` 해당 ADAL tooyour 응용 프로그램을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="42242-166">Now it's time toouse hello `AuthenticationResult` that ADAL returned tooyour app.</span></span>  <span data-ttu-id="42242-167">Hello에 `QueryGraph(...)` 콜백을 hello 인증 헤더에 toohello GET 요청을 획득 하는 hello access_token 연결:</span><span class="sxs-lookup"><span data-stu-id="42242-167">In hello `QueryGraph(...)` callback, attach hello access_token you acquired toohello GET request in hello Authorization header:</span></span>

```C#
private async void QueryGraph(AuthenticationResult result)
{
    if (result.Status != AuthenticationStatus.Success)
    {
        MessageDialog dialog = new MessageDialog(string.Format("If hello error continues, please contact your administrator.\n\nError: {0}\n\nError Description:\n\n{1}", result.Error, result.ErrorDescription), "Sorry, an error occurred while signing you in.");
        await dialog.ShowAsync();
    }

    // Add hello access token toohello Authorization Header of hello call toohello Graph API, and call hello Graph API.
    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);

    ...
}
```
* <span data-ttu-id="42242-168">Hello를 사용할 수도 있습니다 `AuthenticationResult` hello 사용자 응용 프로그램에 대 한 toodisplay 정보 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="42242-168">You can also use hello `AuthenticationResult` object toodisplay information about hello user in your app.</span></span> <span data-ttu-id="42242-169">Hello에 `QueryGraph(...)` 메서드를 사용 하 여 hello 결과 tooshow hello 사용자의 id hello 페이지에서:</span><span class="sxs-lookup"><span data-stu-id="42242-169">In hello `QueryGraph(...)` method, use hello result tooshow hello user's id on hello page:</span></span>

```C#
// Update hello Page UI toorepresent hello signed in user
ActiveUser.Text = result.UserInfo.DisplayableId;
```
* <span data-ttu-id="42242-170">마지막으로, ADAL toosign hello 사용자도 응용 프로그램에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42242-170">Finally, you can use ADAL toosign hello user out of hte application as well.</span></span>  <span data-ttu-id="42242-171">Hello 사용자가 hello "로그 아웃" 단추를 클릭 한 다음 호출을 너무 hello tooensure 원하는`AcquireTokenSilentAsync(...)` 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="42242-171">When hello user clicks hello "Sign Out" button, we want tooensure that hello next call too`AcquireTokenSilentAsync(...)` will fail.</span></span>  <span data-ttu-id="42242-172">ADAL,이 hello 토큰 캐시를 지우는 것 처럼 쉽게:</span><span class="sxs-lookup"><span data-stu-id="42242-172">With ADAL, this is as easy as clearing hello token cache:</span></span>

```C#
private void SignOut()
{
    // Clear session state from hello token cache.
    authContext.TokenCache.Clear();

    ...
}
```

<span data-ttu-id="42242-173">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="42242-173">Congratulations!</span></span> <span data-ttu-id="42242-174">이제 hello 기능 tooauthenticate 사용자가 Windows Phone 앱이 작동, 안전 하 게 OAuth 2.0을 사용 하 여 웹 Api를 호출 하 고 hello 사용자에 대 한 기본 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="42242-174">You now have a working Windows Phone app that has hello ability tooauthenticate users, securely call Web APIs using OAuth 2.0, and get basic information about hello user.</span></span>  <span data-ttu-id="42242-175">아직 하지 않는 이제 경우 hello 시간 toopopulate 사용자로 구성 된 테 넌 트입니다.</span><span class="sxs-lookup"><span data-stu-id="42242-175">If you haven’t already, now is hello time toopopulate your tenant with some users.</span></span>  <span data-ttu-id="42242-176">DirectorySearcher 앱을 실행하고 해당 사용자 중 하나로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="42242-176">Run your DirectorySearcher app, and sign in with one of those users.</span></span>  <span data-ttu-id="42242-177">해당 UPN에 따라 다른 사용자를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="42242-177">Search for other users based on their UPN.</span></span>  <span data-ttu-id="42242-178">Hello 응용 프로그램을 닫고 다시 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="42242-178">Close hello app, and re-run it.</span></span>  <span data-ttu-id="42242-179">Hello 사용자의 세션 그대로 유지 방법을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="42242-179">Notice how hello user’s session remains intact.</span></span>  <span data-ttu-id="42242-180">로그아웃했다가 다른 사용자로 다시 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="42242-180">Sign out, and sign back in as another user.</span></span>

<span data-ttu-id="42242-181">ADAL 쉽게 tooincorporate를 사용 하면 모든 응용 프로그램에 이러한 일반적인 id 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="42242-181">ADAL makes it easy tooincorporate all of these common identity features into your application.</span></span>  <span data-ttu-id="42242-182">있습니다-캐시 관리, 로그인 토큰이 만료 등 새로 고침 UI hello 사용자 제시 되는 OAuth 프로토콜 지원에 대 한 모든 hello dirty 작업의 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="42242-182">It takes care of all hello dirty work for you - cache management, OAuth protocol support, presenting hello user with a login UI, refreshing expired tokens, and more.</span></span>  <span data-ttu-id="42242-183">Tooknow 실제로 필요한 것은 단일 API 호출 `authContext.AcquireToken*(…)`합니다.</span><span class="sxs-lookup"><span data-stu-id="42242-183">All you really need tooknow is a single API call, `authContext.AcquireToken*(…)`.</span></span>

<span data-ttu-id="42242-184">구성 값) (없이 완료 hello 샘플은 제공 참조용으로 [여기](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip)합니다.</span><span class="sxs-lookup"><span data-stu-id="42242-184">For reference, hello completed sample (without your configuration values) is provided [here](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span></span>  <span data-ttu-id="42242-185">이제 tooadditional id 시나리오에서 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42242-185">You can now move on tooadditional identity scenarios.</span></span>  <span data-ttu-id="42242-186">Tootry를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42242-186">You may want tootry:</span></span>

[<span data-ttu-id="42242-187">Azure AD를 사용하여 .NET Web API 보안 유지 >></span><span class="sxs-lookup"><span data-stu-id="42242-187">Secure a .NET Web API with Azure AD >></span></span>](active-directory-devquickstarts-webapi-dotnet.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]


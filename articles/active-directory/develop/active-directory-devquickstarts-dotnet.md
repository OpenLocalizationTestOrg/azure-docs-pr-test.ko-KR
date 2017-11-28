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
# <a name="integrate-azure-ad-into-a-windows-desktop-wpf-app"></a><span data-ttu-id="47989-103">Windows Desktop WPF 앱에 Azure AD 통합</span><span class="sxs-lookup"><span data-stu-id="47989-103">Integrate Azure AD into a Windows Desktop WPF App</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="47989-104">데스크톱 응용 프로그램을 개발 하는 경우 Azure AD는 간단 하 고 간단 하 게 하면 tooauthenticate 자신의 Active Directory 계정에 사용자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47989-104">If you're developing a desktop application, Azure AD makes it simple and straightforward for you tooauthenticate your users with their Active Directory accounts.</span></span>  <span data-ttu-id="47989-105">응용 프로그램 toosecurely 해줍니다 모든 웹 Azure AD로 보호 되는 API를 사용와 같은 Office 365 Api hello 또는 Azure API를 환영 합니다.</span><span class="sxs-lookup"><span data-stu-id="47989-105">It also enables your application toosecurely consume any web API protected by Azure AD, such as hello Office 365 APIs or hello Azure API.</span></span>

<span data-ttu-id="47989-106">.NET 네이티브 클라이언트의 tooaccess 보호 된 리소스를 필요로 하는 경우 Azure AD hello ADAL 또는 Active Directory 인증 라이브러리를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="47989-106">For .NET native clients that need tooaccess protected resources, Azure AD provides hello Active Directory Authentication Library, or ADAL.</span></span>  <span data-ttu-id="47989-107">생활에서 ADAL의 목적으로 toomake 사용자가 앱 tooget 액세스 토큰을 쉽게 합니다.</span><span class="sxs-lookup"><span data-stu-id="47989-107">ADAL's sole purpose in life is toomake it easy for your app tooget access tokens.</span></span>  <span data-ttu-id="47989-108">이면 작업이 얼마나 쉬운지 toodemonstrate 여기 빌드합니다.NET WPF 할 일 목록 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="47989-108">toodemonstrate just how easy it is, here we'll build a .NET WPF To-Do List application that:</span></span>

* <span data-ttu-id="47989-109">가져옵니다 hello를 사용 하 여 hello Azure AD Graph API 호출에 대 한 토큰에 액세스 [OAuth 2.0 인증 프로토콜](https://msdn.microsoft.com/library/azure/dn645545.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="47989-109">Gets access tokens for calling hello Azure AD Graph API using hello [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="47989-110">지정된 별칭을 가진 사용자를 디렉터리에서 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="47989-110">Searches a directory for users with a given alias.</span></span>
* <span data-ttu-id="47989-111">사용자를 로그아웃합니다.</span><span class="sxs-lookup"><span data-stu-id="47989-111">Signs users out.</span></span>

<span data-ttu-id="47989-112">toobuild hello 완료 작업 응용 프로그램에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="47989-112">toobuild hello complete working application, you'll need to:</span></span>

1. <span data-ttu-id="47989-113">Azure AD에 응용 프로그램을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="47989-113">Register your application with Azure AD.</span></span>
2. <span data-ttu-id="47989-114">ADAL을 설치 및 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="47989-114">Install & Configure ADAL.</span></span>
3. <span data-ttu-id="47989-115">Azure AD에서 ADAL tooget 토큰을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="47989-115">Use ADAL tooget tokens from Azure AD.</span></span>

<span data-ttu-id="47989-116">시작 tooget [hello 응용 프로그램의 기본 정의 다운로드](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/skeleton.zip) 또는 [완료 hello 샘플 다운로드](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip)합니다.</span><span class="sxs-lookup"><span data-stu-id="47989-116">tooget started, [download hello app skeleton](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/skeleton.zip) or [download hello completed sample](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span></span>  <span data-ttu-id="47989-117">또한 사용자를 만들고 응용 프로그램을 등록할 수 있는 Azure AD 테넌트도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="47989-117">You'll also need an Azure AD tenant in which you can create users and register an application.</span></span>  <span data-ttu-id="47989-118">테 넌 트 아직 없는 경우 [자세한 방법을 하나 tooget](active-directory-howto-tenant.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="47989-118">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

## <a name="1-register-hello-directorysearcher-application"></a><span data-ttu-id="47989-119">1. Hello DirectorySearcher 응용 프로그램 등록</span><span class="sxs-lookup"><span data-stu-id="47989-119">1. Register hello DirectorySearcher Application</span></span>
<span data-ttu-id="47989-120">tooenable 먼저 해야 사용자가 앱 tooget 토큰 tooregister에서 Azure AD 테 넌 트 권한 tooaccess hello Azure AD Graph API에 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="47989-120">tooenable your app tooget tokens, you'll first need tooregister it in your Azure AD tenant and grant it permission tooaccess hello Azure AD Graph API:</span></span>

1. <span data-ttu-id="47989-121">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="47989-121">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="47989-122">Hello 위쪽 막대에서 계정에 및 hello에서 클릭 **디렉터리** 목록에서 원하는 위치 tooregister 응용 프로그램 hello Active Directory 테 넌 트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="47989-122">On hello top bar, click on your account and under hello **Directory** list, choose hello Active Directory tenant where you wish tooregister your application.</span></span>
3. <span data-ttu-id="47989-123">클릭 **더 서비스** 왼쪽 nav hello와 선택 **Azure Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="47989-123">Click on **More Services** in hello left hand nav, and choose **Azure Active Directory**.</span></span>
4. <span data-ttu-id="47989-124">**앱 등록**을 클릭하고 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="47989-124">Click on **App registrations** and choose **Add**.</span></span>
5. <span data-ttu-id="47989-125">Hello 화면에 따라 수행 하 고 새 **네이티브 클라이언트 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="47989-125">Follow hello prompts and create a new **Native Client Application**.</span></span>
  * <span data-ttu-id="47989-126">hello **이름** 응용 프로그램의 hello 응용 프로그램 tooend-사용자가 설명 합니다</span><span class="sxs-lookup"><span data-stu-id="47989-126">hello **Name** of hello application will describe your application tooend-users</span></span>
  * <span data-ttu-id="47989-127">hello **리디렉션 Uri** 체계 및 문자열 조합 tooreturn 토큰 응답을 Azure AD에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="47989-127">hello **Redirect Uri** is a scheme and string combination that Azure AD will use tooreturn token responses.</span></span>  <span data-ttu-id="47989-128">값 특정 tooyour 응용 프로그램을 입력 합니다. `http://DirectorySearcher`합니다.</span><span class="sxs-lookup"><span data-stu-id="47989-128">Enter a value specific tooyour application, e.g. `http://DirectorySearcher`.</span></span>
6. <span data-ttu-id="47989-129">등록을 완료하면 AAD는 앱에 고유한 응용 프로그램 ID를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="47989-129">Once you've completed registration, AAD will assign your app a unique Application ID.</span></span>  <span data-ttu-id="47989-130">이 값이 필요 합니다 hello 다음 섹션의 하므로에서 복사 hello 응용 프로그램 페이지.</span><span class="sxs-lookup"><span data-stu-id="47989-130">You'll need this value in hello next sections, so copy it from hello application page.</span></span>
7. <span data-ttu-id="47989-131">Hello에서 **설정** 페이지에서 선택 **필요한 권한** 선택 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="47989-131">From hello **Settings** page, choose **Required Permissions** and choose **Add**.</span></span> <span data-ttu-id="47989-132">선택 hello **Microsoft Graph** 으로 hello를 더하고 API hello **디렉터리 데이터 읽기** 에 따른 권한 **위임 된 권한**합니다.</span><span class="sxs-lookup"><span data-stu-id="47989-132">Select hello **Microsoft Graph** as hello API and add hello **Read Directory Data** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="47989-133">이렇게 하면 응용 프로그램 tooquery hello Graph API 사용자에 대 한 활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="47989-133">This will enable your application tooquery hello Graph API for users.</span></span>

## <a name="2-install--configure-adal"></a><span data-ttu-id="47989-134">2. ADAL 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="47989-134">2. Install & Configure ADAL</span></span>
<span data-ttu-id="47989-135">Azure AD에서 응용 프로그램이 있으므로 ADAL을 설치하고 ID 관련 코드를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47989-135">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span></span>  <span data-ttu-id="47989-136">해야 tooprovide에서 Azure AD와 ADAL toobe 수 toocommunicate 사용 하 여 응용 프로그램 등록에 대 한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="47989-136">In order for ADAL toobe able toocommunicate with Azure AD, you need tooprovide it with some information about your app registration.</span></span>

* <span data-ttu-id="47989-137">Hello 패키지 관리자 콘솔을 사용 하 여 ADAL toohello DirectorySearcher 프로젝트를 추가 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="47989-137">Begin by adding ADAL toohello DirectorySearcher project using hello Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

* <span data-ttu-id="47989-138">Hello DirectorySearcher 프로젝트를 열고 `app.config`합니다.</span><span class="sxs-lookup"><span data-stu-id="47989-138">In hello DirectorySearcher project, open `app.config`.</span></span>  <span data-ttu-id="47989-139">Hello에 hello 요소 hello 값 바꾸기 `<appSettings>` 섹션 tooreflect hello hello Azure 포털에 대 한 입력 값입니다.</span><span class="sxs-lookup"><span data-stu-id="47989-139">Replace hello values of hello elements in hello `<appSettings>` section tooreflect hello values you input into hello Azure Portal.</span></span>  <span data-ttu-id="47989-140">코드는 ADAL을 사용할 때마다 이러한 값을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="47989-140">Your code will reference these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="47989-141">hello `ida:Tenant` hello 도메인은의 Azure AD 테 넌 트, 예: contoso.onmicrosoft.com</span><span class="sxs-lookup"><span data-stu-id="47989-141">hello `ida:Tenant` is hello domain of your Azure AD tenant, e.g. contoso.onmicrosoft.com</span></span>
  * <span data-ttu-id="47989-142">hello `ida:ClientId` hello 포털에서 복사 하는 응용 프로그램의 hello clientId 됩니다.</span><span class="sxs-lookup"><span data-stu-id="47989-142">hello `ida:ClientId` is hello clientId of your application you copied from hello portal.</span></span>
  * <span data-ttu-id="47989-143">hello `ida:RedirectUri` 는 hello 리디렉션 url hello 포털에 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="47989-143">hello `ida:RedirectUri` is hello redirect url you registered in hello portal.</span></span>

## <a name="3----use-adal-tooget-tokens-from-aad"></a><span data-ttu-id="47989-144">3.    AAD에서 ADAL tooGet 토큰 사용</span><span class="sxs-lookup"><span data-stu-id="47989-144">3.    Use ADAL tooGet Tokens from AAD</span></span>
<span data-ttu-id="47989-145">hello ADAL 기본 원칙 되는 응용 프로그램 액세스 토큰을 필요할 때마다 단순히 호출 `authContext.AcquireTokenAsync(...)`, 및 ADAL rest hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="47989-145">hello basic principle behind ADAL is that whenever your app needs an access token, it simply calls `authContext.AcquireTokenAsync(...)`, and ADAL does hello rest.</span></span>  

* <span data-ttu-id="47989-146">Hello에 `DirectorySearcher` 프로젝트, 열기 `MainWindow.xaml.cs` hello 찾습니다 `MainWindow()` 메서드.</span><span class="sxs-lookup"><span data-stu-id="47989-146">In hello `DirectorySearcher` project, open `MainWindow.xaml.cs` and locate hello `MainWindow()` method.</span></span>  <span data-ttu-id="47989-147">hello 첫 번째 단계는 tooinitialize 앱의 `AuthenticationContext` -ADAL의 기본 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="47989-147">hello first step is tooinitialize your app's `AuthenticationContext` - ADAL's primary class.</span></span>  <span data-ttu-id="47989-148">이 ADAL을 전달 하는 Azure AD와 toocommunicate 필요한 좌표 hello 및 방법에 설명 toocache 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="47989-148">This is where you pass ADAL hello coordinates it needs toocommunicate with Azure AD and tell it how toocache tokens.</span></span>

```C#
public MainWindow()
{
    InitializeComponent();

    authContext = new AuthenticationContext(authority, new FileCache());

    CheckForCachedToken();
}
```

* <span data-ttu-id="47989-149">이제 hello를 찾을 `Search(...)` 메서드 hello 사용자 cliks hello hello 응용 프로그램의 UI에서 "검색" 단추 때 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="47989-149">Now locate hello `Search(...)` method, which will be invoked when hello user cliks hello "Search" button in hello app's UI.</span></span>  <span data-ttu-id="47989-150">이 메서드는 해당 UPN 검색 단어를 지정 하는 hello로 시작 하는 사용자에 대 한 GET 요청 toohello Azure AD Graph API tooquery를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="47989-150">This method makes a GET request toohello Azure AD Graph API tooquery for users whose UPN begins with hello given search term.</span></span>  <span data-ttu-id="47989-151">순서 tooquery hello Graph API, tooinclude hello에서 access_token 필요 하지만 `Authorization` 이 경우에 ADAL-hello의 헤더를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="47989-151">But in order tooquery hello Graph API, you need tooinclude an access_token in hello `Authorization` header of hello request - this is where ADAL comes in.</span></span>

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
* <span data-ttu-id="47989-152">응용 프로그램 호출 하 여 토큰을 요청 하는 경우 `AcquireTokenAsync(...)`, ADAL hello 사용자 자격 증명을 요청 하지 않고 tooreturn 토큰을 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="47989-152">When your app requests a token by calling `AcquireTokenAsync(...)`, ADAL will attempt tooreturn a token without asking hello user for credentials.</span></span>  <span data-ttu-id="47989-153">ADAL 해당 hello 사용자에 게 toosign tooget 토큰에에서 필요한 데이터를 결정 하는 경우 로그인 대화 상자를 표시, hello 사용자의 자격 증명을 수집 되며 인증 성공 시 토큰을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="47989-153">If ADAL determines that hello user needs toosign in tooget a token, it will display a login dialog, collect hello user's credentials, and return a token upon successful authentication.</span></span>  <span data-ttu-id="47989-154">ADAL 어떤 이유로 든 없습니다 tooreturn 토큰 이면 예외를 throw 한 `AdalException`합니다.</span><span class="sxs-lookup"><span data-stu-id="47989-154">If ADAL is unable tooreturn a token for any reason, it will throw an `AdalException`.</span></span>
* <span data-ttu-id="47989-155">해당 hello 확인 `AuthenticationResult` 개체에 포함 되어는 `UserInfo` 앱 할 수는 사용 되는 toocollect 정보 일 수 있는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="47989-155">Notice that hello `AuthenticationResult` object contains a `UserInfo` object that can be used toocollect information your app may need.</span></span>  <span data-ttu-id="47989-156">Hello DirectorySearcher에서 `UserInfo` hello 사용자의 id와 함께 사용 되는 toocustomize hello 응용 프로그램의 UI가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47989-156">In hello DirectorySearcher, `UserInfo` is used toocustomize hello app's UI with hello user's id.</span></span>
* <span data-ttu-id="47989-157">Hello 사용자가 hello "로그 아웃" 단추를 클릭 한 다음 호출을 너무 hello tooensure 원하는`AcquireTokenAsync(...)` hello 사용자 toosign에 게 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="47989-157">When hello user clicks hello "Sign Out" button, we want tooensure that hello next call too`AcquireTokenAsync(...)` will ask hello user toosign in.</span></span>  <span data-ttu-id="47989-158">ADAL,이 hello 토큰 캐시를 지우는 것 처럼 쉽게:</span><span class="sxs-lookup"><span data-stu-id="47989-158">With ADAL, this is as easy as clearing hello token cache:</span></span>

```C#
private void SignOut(object sender = null, RoutedEventArgs args = null)
{
    // Clear hello token cache
    authContext.TokenCache.Clear();

    ...
}
```

* <span data-ttu-id="47989-159">그러나 hello 사용자 hello "로그 아웃" 단추를 클릭 하지 않는 경우 다음 DirectorySearcher hello를 실행할 때 hello에 대 한 toomaintain hello 사용자의 세션을 합니다.</span><span class="sxs-lookup"><span data-stu-id="47989-159">However, if hello user does not click hello "Sign Out" button, you will want toomaintain hello user's session for hello next time they run hello DirectorySearcher.</span></span>  <span data-ttu-id="47989-160">Hello 앱이 시작 되 면 기존 토큰에 대 한 ADAL의 토큰 캐시를 확인 하 고 hello UI를 적절 하 게 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47989-160">When hello app launches, you can check ADAL's token cache for an existing token and update hello UI accordingly.</span></span>  <span data-ttu-id="47989-161">Hello에 `CheckForCachedToken()` 메서드를 다른 호출할 너무`AcquireTokenAsync(...)`, hello를 전달 하는이 시간 `PromptBehavior.Never` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="47989-161">In hello `CheckForCachedToken()` method, make another call too`AcquireTokenAsync(...)`, this time passing in hello `PromptBehavior.Never` parameter.</span></span>  <span data-ttu-id="47989-162">`PromptBehavior.Never`명령은 hello 사용자 로그인을 위해 묻지 해야 및 ADAL 대신 예외를 throw 해야 없습니다 tooreturn 이면 토큰 ADAL 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="47989-162">`PromptBehavior.Never` will tell ADAL that hello user should not be prompted for sign in, and ADAL should instead throw an exception if it is unable tooreturn a token.</span></span>

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

<span data-ttu-id="47989-163">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="47989-163">Congratulations!</span></span> <span data-ttu-id="47989-164">이제 정상 작동 hello 기능 tooauthenticate 사용자가 있는.NET WPF 응용 프로그램, 안전 하 게 OAuth 2.0을 사용 하 여 웹 Api를 호출 하 고 hello 사용자에 대 한 기본 정보를 얻을 합니다.</span><span class="sxs-lookup"><span data-stu-id="47989-164">You now have a working .NET WPF application that has hello ability tooauthenticate users, securely call Web APIs using OAuth 2.0, and get basic information about hello user.</span></span>  <span data-ttu-id="47989-165">아직 하지 않는 이제 경우 hello 시간 toopopulate 사용자로 구성 된 테 넌 트입니다.</span><span class="sxs-lookup"><span data-stu-id="47989-165">If you haven't already, now is hello time toopopulate your tenant with some users.</span></span>  <span data-ttu-id="47989-166">DirectorySearcher 앱을 실행하고 해당 사용자 중 하나로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="47989-166">Run your DirectorySearcher app, and sign in with one of those users.</span></span>  <span data-ttu-id="47989-167">해당 UPN에 따라 다른 사용자를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="47989-167">Search for other users based on their UPN.</span></span>  <span data-ttu-id="47989-168">Hello 응용 프로그램을 닫고 다시 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="47989-168">Close hello app, and re-run it.</span></span>  <span data-ttu-id="47989-169">Hello 사용자의 세션 그대로 유지 방법을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="47989-169">Notice how hello user's session remains intact.</span></span>  <span data-ttu-id="47989-170">로그아웃했다가 다른 사용자로 다시 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="47989-170">Sign out, and sign back in as another user.</span></span>

<span data-ttu-id="47989-171">ADAL 쉽게 tooincorporate를 사용 하면 모든 응용 프로그램에 이러한 일반적인 id 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="47989-171">ADAL makes it easy tooincorporate all of these common identity features into your application.</span></span>  <span data-ttu-id="47989-172">있습니다-캐시 관리, 로그인 토큰이 만료 등 새로 고침 UI hello 사용자 제시 되는 OAuth 프로토콜 지원에 대 한 모든 hello dirty 작업의 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="47989-172">It takes care of all hello dirty work for you - cache management, OAuth protocol support, presenting hello user with a login UI, refreshing expired tokens, and more.</span></span>  <span data-ttu-id="47989-173">Tooknow 실제로 필요한 것은 단일 API 호출 `authContext.AcquireTokenAsync(...)`합니다.</span><span class="sxs-lookup"><span data-stu-id="47989-173">All you really need tooknow is a single API call, `authContext.AcquireTokenAsync(...)`.</span></span>

<span data-ttu-id="47989-174">구성 값) (없이 완료 hello 샘플은 제공 참조용으로 [여기](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip)합니다.</span><span class="sxs-lookup"><span data-stu-id="47989-174">For reference, hello completed sample (without your configuration values) is provided [here](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span></span>  <span data-ttu-id="47989-175">이제 tooadditional 시나리오에 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47989-175">You can now move on tooadditional scenarios.</span></span>  <span data-ttu-id="47989-176">Tootry를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47989-176">You may want tootry:</span></span>

[<span data-ttu-id="47989-177">Azure AD를 사용하여 .NET Web API 보안 유지 >></span><span class="sxs-lookup"><span data-stu-id="47989-177">Secure a .NET Web API with Azure AD >></span></span>](active-directory-devquickstarts-webapi-dotnet.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]


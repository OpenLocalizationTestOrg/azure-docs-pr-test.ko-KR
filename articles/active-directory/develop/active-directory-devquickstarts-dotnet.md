---
title: "Azure AD .NET 시작 | Microsoft Docs"
description: "로그인을 위해 Azure AD와 통합되고 OAuth를 사용하여 Azure AD로 보호되는 API를 호출하는 .NET Windows Desktop 응용 프로그램 빌드 방법"
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
ms.openlocfilehash: 7a252e0e5243c7b7489373845531cb913ca1f6aa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="integrate-azure-ad-into-a-windows-desktop-wpf-app"></a><span data-ttu-id="34dd8-103">Windows Desktop WPF 앱에 Azure AD 통합</span><span class="sxs-lookup"><span data-stu-id="34dd8-103">Integrate Azure AD into a Windows Desktop WPF App</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="34dd8-104">데스크톱 응용 프로그램을 개발하는 경우 Azure AD를 사용하면 간단하고 편리하게 Active Directory 계정에 사용하여 사용자를 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-104">If you're developing a desktop application, Azure AD makes it simple and straightforward for you to authenticate your users with their Active Directory accounts.</span></span>  <span data-ttu-id="34dd8-105">또한 응용 프로그램에서 Office 365 API 또는 Azure API와 같이 Azure AD를 통해 보호되는 웹 API를 안전하게 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-105">It also enables your application to securely consume any web API protected by Azure AD, such as the Office 365 APIs or the Azure API.</span></span>

<span data-ttu-id="34dd8-106">보호된 리소스에 액세스해야 하는 .NET 네이티브 클라이언트의 경우 Azure AD는 Active Directory 인증 라이브러리 또는 ADAL을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-106">For .NET native clients that need to access protected resources, Azure AD provides the Active Directory Authentication Library, or ADAL.</span></span>  <span data-ttu-id="34dd8-107">ADAL의 유일한 용도는 앱이 쉽게 액세스 토큰을 가져오도록 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-107">ADAL's sole purpose in life is to make it easy for your app to get access tokens.</span></span>  <span data-ttu-id="34dd8-108">액세스 토큰을 얼마나 쉽게 가져올 수 있는지 보여 주기 위해 다음을 수행하는 .NET WPF To-Do List 응용 프로그램을 빌드해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-108">To demonstrate just how easy it is, here we'll build a .NET WPF To-Do List application that:</span></span>

* <span data-ttu-id="34dd8-109">[OAuth 2.0 인증 프로토콜](https://msdn.microsoft.com/library/azure/dn645545.aspx)을 사용하여 Azure AD Graph API를 호출하기 위한 액세스 토큰을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-109">Gets access tokens for calling the Azure AD Graph API using the [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="34dd8-110">지정된 별칭을 가진 사용자를 디렉터리에서 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-110">Searches a directory for users with a given alias.</span></span>
* <span data-ttu-id="34dd8-111">사용자를 로그아웃합니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-111">Signs users out.</span></span>

<span data-ttu-id="34dd8-112">완전하게 작동하는 응용 프로그램을 빌드하려면 다음 작업이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-112">To build the complete working application, you'll need to:</span></span>

1. <span data-ttu-id="34dd8-113">Azure AD에 응용 프로그램을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-113">Register your application with Azure AD.</span></span>
2. <span data-ttu-id="34dd8-114">ADAL을 설치 및 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-114">Install & Configure ADAL.</span></span>
3. <span data-ttu-id="34dd8-115">ADAL을 사용하여 Azure AD에서 토큰을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-115">Use ADAL to get tokens from Azure AD.</span></span>

<span data-ttu-id="34dd8-116">시작하려면 [앱 기본 사항을 다운로드](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/skeleton.zip)하거나 [완성된 샘플을 다운로드](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip)하세요.</span><span class="sxs-lookup"><span data-stu-id="34dd8-116">To get started, [download the app skeleton](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/skeleton.zip) or [download the completed sample](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span></span>  <span data-ttu-id="34dd8-117">또한 사용자를 만들고 응용 프로그램을 등록할 수 있는 Azure AD 테넌트도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-117">You'll also need an Azure AD tenant in which you can create users and register an application.</span></span>  <span data-ttu-id="34dd8-118">테넌트가 아직 없는 경우 [얻는 방법을 알아보세요](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="34dd8-118">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

## <a name="1-register-the-directorysearcher-application"></a><span data-ttu-id="34dd8-119">1. DirectorySearcher 응용 프로그램 등록</span><span class="sxs-lookup"><span data-stu-id="34dd8-119">1. Register the DirectorySearcher Application</span></span>
<span data-ttu-id="34dd8-120">앱에서 토큰을 가져올 수 있게 하려면 먼저 Azure AD 테넌트에 등록하고 Azure AD Graph API에 액세스할 수 있는 권한을 부여해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-120">To enable your app to get tokens, you'll first need to register it in your Azure AD tenant and grant it permission to access the Azure AD Graph API:</span></span>

1. <span data-ttu-id="34dd8-121">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-121">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="34dd8-122">오른쪽 위에서 계정을 클릭하고 **디렉터리** 목록에서 응용 프로그램을 등록하려는 Active Directory 테넌트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-122">On the top bar, click on your account and under the **Directory** list, choose the Active Directory tenant where you wish to register your application.</span></span>
3. <span data-ttu-id="34dd8-123">왼쪽 탐색 창에서 **더 많은 서비스**를 클릭하고 **Azure Active Directory**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-123">Click on **More Services** in the left hand nav, and choose **Azure Active Directory**.</span></span>
4. <span data-ttu-id="34dd8-124">**앱 등록**을 클릭하고 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-124">Click on **App registrations** and choose **Add**.</span></span>
5. <span data-ttu-id="34dd8-125">프롬프트에 따라 새 **네이티브 클라이언트 응용 프로그램**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-125">Follow the prompts and create a new **Native Client Application**.</span></span>
  * <span data-ttu-id="34dd8-126">응용 프로그램의 **이름** 은 최종 사용자에게 응용 프로그램을 설명하는 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-126">The **Name** of the application will describe your application to end-users</span></span>
  * <span data-ttu-id="34dd8-127">**리디렉션 Uri** 는 Azure AD가 토큰 응답을 반환하는 데 사용하는 구성표 및 문자열 조합입니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-127">The **Redirect Uri** is a scheme and string combination that Azure AD will use to return token responses.</span></span>  <span data-ttu-id="34dd8-128">응용 프로그램에 고유하게 해당되는 값을 입력합니다(예: `http://DirectorySearcher`).</span><span class="sxs-lookup"><span data-stu-id="34dd8-128">Enter a value specific to your application, e.g. `http://DirectorySearcher`.</span></span>
6. <span data-ttu-id="34dd8-129">등록을 완료하면 AAD는 앱에 고유한 응용 프로그램 ID를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-129">Once you've completed registration, AAD will assign your app a unique Application ID.</span></span>  <span data-ttu-id="34dd8-130">이 값은 다음 섹션에서 필요하므로 응용 프로그램 페이지에서 복사해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-130">You'll need this value in the next sections, so copy it from the application page.</span></span>
7. <span data-ttu-id="34dd8-131">**설정** 페이지에서 **필요한 사용 권한**, **추가**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-131">From the **Settings** page, choose **Required Permissions** and choose **Add**.</span></span> <span data-ttu-id="34dd8-132">**Microsoft Graph**를 API로 선택하고 **위임된 사용 권한**에서 **디렉터리 데이터 읽기** 사용 권한을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-132">Select the **Microsoft Graph** as the API and add the **Read Directory Data** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="34dd8-133">이렇게 하면 응용 프로그램은 Graph API에서 사용자를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-133">This will enable your application to query the Graph API for users.</span></span>

## <a name="2-install--configure-adal"></a><span data-ttu-id="34dd8-134">2. ADAL 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="34dd8-134">2. Install & Configure ADAL</span></span>
<span data-ttu-id="34dd8-135">Azure AD에서 응용 프로그램이 있으므로 ADAL을 설치하고 ID 관련 코드를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-135">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span></span>  <span data-ttu-id="34dd8-136">ADAL이 Azura AD와 통신할 수 있게 하려면, 앱 등록에 관한 일부 정보를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-136">In order for ADAL to be able to communicate with Azure AD, you need to provide it with some information about your app registration.</span></span>

* <span data-ttu-id="34dd8-137">먼저 패키지 관리자 콘솔을 사용하여 ADAL을 DirectorySearcher 프로젝트에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-137">Begin by adding ADAL to the DirectorySearcher project using the Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

* <span data-ttu-id="34dd8-138">DirectorySearcher 프로젝트에서 `app.config`를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-138">In the DirectorySearcher project, open `app.config`.</span></span>  <span data-ttu-id="34dd8-139">Azure 포털에 입력한 값을 반영하도록 `<appSettings>` 섹션의 요소 값을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-139">Replace the values of the elements in the `<appSettings>` section to reflect the values you input into the Azure Portal.</span></span>  <span data-ttu-id="34dd8-140">코드는 ADAL을 사용할 때마다 이러한 값을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-140">Your code will reference these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="34dd8-141">`ida:Tenant` 는 Azure AD 테넌트의 도메인(예: contoso.onmicrosoft.com)입니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-141">The `ida:Tenant` is the domain of your Azure AD tenant, e.g. contoso.onmicrosoft.com</span></span>
  * <span data-ttu-id="34dd8-142">`ida:ClientId` 는 포털에서 복사한 응용 프로그램의 clientId여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-142">The `ida:ClientId` is the clientId of your application you copied from the portal.</span></span>
  * <span data-ttu-id="34dd8-143">`ida:RedirectUri`는 포털에 등록한 리디렉션 url입니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-143">The `ida:RedirectUri` is the redirect url you registered in the portal.</span></span>

## <a name="3----use-adal-to-get-tokens-from-aad"></a><span data-ttu-id="34dd8-144">3.    ADAL을 사용하여 AAD에서 토큰을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-144">3.    Use ADAL to Get Tokens from AAD</span></span>
<span data-ttu-id="34dd8-145">ADAL에서 확인되는 기본 원칙은 액세스 토큰이 필요할 때마다 앱이 `authContext.AcquireTokenAsync(...)`을 호출하고 나머지 작업은 ADAL이 수행한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-145">The basic principle behind ADAL is that whenever your app needs an access token, it simply calls `authContext.AcquireTokenAsync(...)`, and ADAL does the rest.</span></span>  

* <span data-ttu-id="34dd8-146">`DirectorySearcher` 프로젝트에서 `MainWindow.xaml.cs`를 열고 `MainWindow()` 메서드를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-146">In the `DirectorySearcher` project, open `MainWindow.xaml.cs` and locate the `MainWindow()` method.</span></span>  <span data-ttu-id="34dd8-147">첫 번째 단계는 앱의 `AuthenticationContext` , 즉 ADAL의 기본 클래스를 초기화하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-147">The first step is to initialize your app's `AuthenticationContext` - ADAL's primary class.</span></span>  <span data-ttu-id="34dd8-148">이 클래스에서 Azure AD와 통신하는 데 필요한 좌표를 ADAL에 전달하고 토큰 캐시 방법을 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-148">This is where you pass ADAL the coordinates it needs to communicate with Azure AD and tell it how to cache tokens.</span></span>

```C#
public MainWindow()
{
    InitializeComponent();

    authContext = new AuthenticationContext(authority, new FileCache());

    CheckForCachedToken();
}
```

* <span data-ttu-id="34dd8-149">이제 사용자가 앱의 UI에서 "검색" 단추를 클릭할 때 호출되는 `Search(...)` 메서드를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-149">Now locate the `Search(...)` method, which will be invoked when the user cliks the "Search" button in the app's UI.</span></span>  <span data-ttu-id="34dd8-150">이 메서드는 Azure AD Graph API에 해당 UPN이 지정된 검색어로 시작하는 사용자를 쿼리하라는 GET 요청을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-150">This method makes a GET request to the Azure AD Graph API to query for users whose UPN begins with the given search term.</span></span>  <span data-ttu-id="34dd8-151">그렇지만 Graph API를 쿼리하려면 ADAL이 연결되는 요청의 `Authorization` 헤더에 access_token을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-151">But in order to query the Graph API, you need to include an access_token in the `Authorization` header of the request - this is where ADAL comes in.</span></span>

```C#
private async void Search(object sender, RoutedEventArgs e)
{
    // Validate the Input String
    if (string.IsNullOrEmpty(SearchText.Text))
    {
        MessageBox.Show("Please enter a value for the To Do item name");
        return;
    }

    // Get an Access Token for the Graph API
    AuthenticationResult result = null;
    try
    {
        result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectUri, new PlatformParameters(PromptBehavior.Auto));
        UserNameLabel.Content = result.UserInfo.DisplayableId;
        SignOutButton.Visibility = Visibility.Visible;
    }
    catch (AdalException ex)
    {
        // An unexpected error occurred, or user canceled the sign in.
        if (ex.ErrorCode != "access_denied")
            MessageBox.Show(ex.Message);

        return;
    }

    ...
}
```
* <span data-ttu-id="34dd8-152">앱이 `AcquireTokenAsync(...)`을 호출하여 토큰을 요청하면 ADAL은 사용자에게 자격 증명을 요구하지 않고 토큰을 반환하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-152">When your app requests a token by calling `AcquireTokenAsync(...)`, ADAL will attempt to return a token without asking the user for credentials.</span></span>  <span data-ttu-id="34dd8-153">ADAL은 사용자가 토큰을 가져오기 위해 로그인해야 한다고 판단할 경우 로그인 대화 상자를 표시하고, 사용자의 자격 증명을 수집하고, 인증 성공 시 토큰을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-153">If ADAL determines that the user needs to sign in to get a token, it will display a login dialog, collect the user's credentials, and return a token upon successful authentication.</span></span>  <span data-ttu-id="34dd8-154">어떤 이유로든 ADAL이 토큰을 반환할 수 없는 경우 `AdalException`을 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-154">If ADAL is unable to return a token for any reason, it will throw an `AdalException`.</span></span>
* <span data-ttu-id="34dd8-155">`AuthenticationResult` 개체에는 사용자 앱에 필요할 수 있는 정보를 수집하는 데 사용할 수 있는 `UserInfo` 개체가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-155">Notice that the `AuthenticationResult` object contains a `UserInfo` object that can be used to collect information your app may need.</span></span>  <span data-ttu-id="34dd8-156">DirectorySearcher에서 `UserInfo` 는 사용자 ID로 앱 UI를 사용자 지정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-156">In the DirectorySearcher, `UserInfo` is used to customize the app's UI with the user's id.</span></span>
* <span data-ttu-id="34dd8-157">여기서는 사용자가 "로그아웃" 단추를 클릭한 경우 다음 `AcquireTokenAsync(...)` 호출 시 사용자에게 로그인하라는 메시지가 표시되도록 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-157">When the user clicks the "Sign Out" button, we want to ensure that the next call to `AcquireTokenAsync(...)` will ask the user to sign in.</span></span>  <span data-ttu-id="34dd8-158">ADAL을 사용하면 이 작업은 토큰 캐시를 지우는 것 만큼 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-158">With ADAL, this is as easy as clearing the token cache:</span></span>

```C#
private void SignOut(object sender = null, RoutedEventArgs args = null)
{
    // Clear the token cache
    authContext.TokenCache.Clear();

    ...
}
```

* <span data-ttu-id="34dd8-159">그러나 사용자가 "로그아웃" 단추를 클릭하지 않으면 다음에 DirectorySearcher를 실행할 때 사용자 세션이 유지되도록 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-159">However, if the user does not click the "Sign Out" button, you will want to maintain the user's session for the next time they run the DirectorySearcher.</span></span>  <span data-ttu-id="34dd8-160">앱이 시작되면 ADAL의 토큰 캐시에서 기존 토큰이 있는지 확인하고 그에 따라 UI를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-160">When the app launches, you can check ADAL's token cache for an existing token and update the UI accordingly.</span></span>  <span data-ttu-id="34dd8-161">`CheckForCachedToken()` 메서드에서 `AcquireTokenAsync(...)`를 다시 호출합니다. 이번에는 `PromptBehavior.Never` 매개 변수를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-161">In the `CheckForCachedToken()` method, make another call to `AcquireTokenAsync(...)`, this time passing in the `PromptBehavior.Never` parameter.</span></span>  <span data-ttu-id="34dd8-162">`PromptBehavior.Never` 는 사용자가 로그인하라는 메시지를 표시하지 않도록 ADAL에 지시하고, 대신 토큰을 반환할 수 없는 경우 ADAL에서는 예외를 발생해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-162">`PromptBehavior.Never` will tell ADAL that the user should not be prompted for sign in, and ADAL should instead throw an exception if it is unable to return a token.</span></span>

```C#
public async void CheckForCachedToken() 
{
    // As the application starts, try to get an access token without prompting the user.  If one exists, show the user as signed in.
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

        // If user interaction is required, proceed to main page without singing the user in.
        return;
    }

    // A valid token is in the cache
    SignOutButton.Visibility = Visibility.Visible;
    UserNameLabel.Content = result.UserInfo.DisplayableId;
}
```

<span data-ttu-id="34dd8-163">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-163">Congratulations!</span></span> <span data-ttu-id="34dd8-164">이제 사용자를 인증하고 OAuth 2.0을 사용하여 Web API를 안전하게 호출하고, 사용자에 대한 기본 정보를 가져올 수 있는 .NET WPF 응용 프로그램이 작성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-164">You now have a working .NET WPF application that has the ability to authenticate users, securely call Web APIs using OAuth 2.0, and get basic information about the user.</span></span>  <span data-ttu-id="34dd8-165">아직 일부 사용자로 테넌트를 채우지 않은 경우 지금 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-165">If you haven't already, now is the time to populate your tenant with some users.</span></span>  <span data-ttu-id="34dd8-166">DirectorySearcher 앱을 실행하고 해당 사용자 중 하나로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-166">Run your DirectorySearcher app, and sign in with one of those users.</span></span>  <span data-ttu-id="34dd8-167">해당 UPN에 따라 다른 사용자를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-167">Search for other users based on their UPN.</span></span>  <span data-ttu-id="34dd8-168">앱을 닫았다가 다시 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-168">Close the app, and re-run it.</span></span>  <span data-ttu-id="34dd8-169">사용자의 세션을 그대로 유지하는 방법을 알아두세요.</span><span class="sxs-lookup"><span data-stu-id="34dd8-169">Notice how the user's session remains intact.</span></span>  <span data-ttu-id="34dd8-170">로그아웃했다가 다른 사용자로 다시 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-170">Sign out, and sign back in as another user.</span></span>

<span data-ttu-id="34dd8-171">ADAL은 응용 프로그램에 이러한 모든 일반적인 ID 기능을 쉽게 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-171">ADAL makes it easy to incorporate all of these common identity features into your application.</span></span>  <span data-ttu-id="34dd8-172">또한 캐시 관리, OAuth 프로토콜 지원, 사용자에게 로그인 UI 제공, 만료된 토큰 새로 고침 등의 모든 귀찮은 작업을 관리해줍니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-172">It takes care of all the dirty work for you - cache management, OAuth protocol support, presenting the user with a login UI, refreshing expired tokens, and more.</span></span>  <span data-ttu-id="34dd8-173">실제로 알아두어야 할 모든 항목은 단일 API 호출, `authContext.AcquireTokenAsync(...)`입니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-173">All you really need to know is a single API call, `authContext.AcquireTokenAsync(...)`.</span></span>

<span data-ttu-id="34dd8-174">참조를 위해 완성된 샘플(사용자 구성 값 제외)이 [여기](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip)에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-174">For reference, the completed sample (without your configuration values) is provided [here](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span></span>  <span data-ttu-id="34dd8-175">이제 추가 시나리오로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-175">You can now move on to additional scenarios.</span></span>  <span data-ttu-id="34dd8-176">다음 작업을 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34dd8-176">You may want to try:</span></span>

[<span data-ttu-id="34dd8-177">Azure AD를 사용하여 .NET Web API 보안 유지 >></span><span class="sxs-lookup"><span data-stu-id="34dd8-177">Secure a .NET Web API with Azure AD >></span></span>](active-directory-devquickstarts-webapi-dotnet.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]


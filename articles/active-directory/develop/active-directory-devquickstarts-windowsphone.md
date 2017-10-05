---
title: "Azure AD Windows Phone 시작 | Microsoft 문서"
description: "로그인을 위해 Azure AD와 통합되고 OAuth를 사용하여 Azure AD로 보호되는 API를 호출하는 Windows Phone 응용 프로그램 빌드 방법"
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
ms.openlocfilehash: 03c4b6d225dce99d79ef6c1ba2af43af8dea3eae
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="integrate-azure-ad-with-a-windows-phone-app"></a><span data-ttu-id="f6155-103">Azure AD와 Windows Phone 앱 통합</span><span class="sxs-lookup"><span data-stu-id="f6155-103">Integrate Azure AD with a Windows Phone App</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

> [!NOTE]
> <span data-ttu-id="f6155-104">Windows Phone 8.1 및 이전 버전 프로젝트는 Visual Studio 2017에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-104">Windows Phone 8.1 and prior version projects are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="f6155-105">자세한 내용은 [Visual Studio 2017 플랫폼 대상 지정 및 호환성](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f6155-105">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

<span data-ttu-id="f6155-106">Windows Phone 8.1 앱을 개발하는 경우 Azure AD를 사용하면 간단하고 편리하게 Active Directory 계정에 사용하여 사용자를 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-106">If you're developing a Windows Phone 8.1 app, Azure AD makes it simple and straightforward for you to authenticate your users with their Active Directory accounts.</span></span>  <span data-ttu-id="f6155-107">또한 응용 프로그램에서 Office 365 API 또는 Azure API와 같이 Azure AD를 통해 보호되는 웹 API를 안전하게 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-107">It also enables your application to securely consume any web API protected by Azure AD, such as the Office 365 APIs or the Azure API.</span></span>

> [!NOTE]
> <span data-ttu-id="f6155-108">이 코드 샘플에서는 ADAL v2.0을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-108">This code sample uses ADAL v2.0.</span></span>  <span data-ttu-id="f6155-109">최신 기술의 경우 대신 [ADAL v3.0을 사용한 Windows 범용 자습서](active-directory-devquickstarts-windowsstore.md)를 시도하려고 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-109">For the latest technology, you may want to instead try our [Windows Universal Tutorial using ADAL v3.0](active-directory-devquickstarts-windowsstore.md).</span></span>  <span data-ttu-id="f6155-110">실제로 Windows Phone 8.1용 앱을 빌드하는 경우에 적절합니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-110">If you are indeed building an app for Windows Phone 8.1, this is the right place.</span></span>  <span data-ttu-id="f6155-111">ADAL v2.0을 완전히 지원하게 되면 Azure AD를 사용하여 Windows Phone 8.1에 대한 앱을 개발하는 경우에 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-111">ADAL v2.0 is still fully supported, and is the recommended way of developing apps agianst Windows Phone 8.1 using Azure AD.</span></span>
> 
> 

<span data-ttu-id="f6155-112">보호된 리소스에 액세스해야 하는 .NET 네이티브 클라이언트의 경우 Azure AD는 Active Directory 인증 라이브러리 또는 ADAL을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-112">For .NET native clients that need to access protected resources, Azure AD provides the Active Directory Authentication Library, or ADAL.</span></span>  <span data-ttu-id="f6155-113">ADAL의 유일한 용도는 앱이 쉽게 액세스 토큰을 가져오도록 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-113">ADAL’s sole purpose in life is to make it easy for your app to get access tokens.</span></span>  <span data-ttu-id="f6155-114">이 작업이 얼마나 쉬운지 보여 주기 위해 다음 작업을 수행하는 "Directory Searcher" Windows Phone 8.1 앱을 빌드해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-114">To demonstrate just how easy it is, here we’ll build a "Directory Searcher" Windows Phone 8.1 app that:</span></span>

* <span data-ttu-id="f6155-115">[OAuth 2.0 인증 프로토콜](https://msdn.microsoft.com/library/azure/dn645545.aspx)을 사용하여 Azure AD Graph API를 호출하기 위한 액세스 토큰을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-115">Gets access tokens for calling the Azure AD Graph API using the [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="f6155-116">지정된 UPN을 가진 사용자를 디렉터리에서 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-116">Searches a directory for users with a given UPN.</span></span>
* <span data-ttu-id="f6155-117">사용자를 로그아웃합니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-117">Signs users out.</span></span>

<span data-ttu-id="f6155-118">완전하게 작동하는 응용 프로그램을 빌드하려면 다음 작업이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-118">To build the complete working application, you’ll need to:</span></span>

1. <span data-ttu-id="f6155-119">Azure AD에 응용 프로그램을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-119">Register your application with Azure AD.</span></span>
2. <span data-ttu-id="f6155-120">ADAL을 설치 및 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-120">Install & Configure ADAL.</span></span>
3. <span data-ttu-id="f6155-121">ADAL을 사용하여 Azure AD에서 토큰을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-121">Use ADAL to get tokens from Azure AD.</span></span>

<span data-ttu-id="f6155-122">시작하려면 [기본 프로젝트를 다운로드](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/skeleton.zip)하거나 [완성된 샘플을 다운로드](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip)하세요.</span><span class="sxs-lookup"><span data-stu-id="f6155-122">To get started, [download a skeleton project](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/skeleton.zip) or [download the completed sample](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span></span>  <span data-ttu-id="f6155-123">각 샘플은 Visual Studio 2013 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-123">Each is a Visual Studio 2013 solution.</span></span>  <span data-ttu-id="f6155-124">또한 사용자를 만들고 응용 프로그램을 등록할 수 있는 Azure AD 테넌트도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-124">You'll also need an Azure AD tenant in which you can create users and register an application.</span></span>  <span data-ttu-id="f6155-125">테넌트가 아직 없는 경우 [얻는 방법을 알아보세요](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="f6155-125">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

## <a name="1-register-the-directory-searcher-application"></a><span data-ttu-id="f6155-126">1. Directory Searcher 응용 프로그램 등록</span><span class="sxs-lookup"><span data-stu-id="f6155-126">1. Register the Directory Searcher Application</span></span>
<span data-ttu-id="f6155-127">앱에서 토큰을 가져올 수 있게 하려면 먼저 Azure AD 테넌트에 등록하고 Azure AD Graph API에 액세스할 수 있는 권한을 부여해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-127">To enable your app to get tokens, you’ll first need to register it in your Azure AD tenant and grant it permission to access the Azure AD Graph API:</span></span>

1. <span data-ttu-id="f6155-128">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-128">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f6155-129">오른쪽 위에서 계정을 클릭하고 **디렉터리** 목록에서 응용 프로그램을 등록하려는 Active Directory 테넌트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-129">On the top bar, click on your account and under the **Directory** list, choose the Active Directory tenant where you wish to register your application.</span></span>
3. <span data-ttu-id="f6155-130">왼쪽 탐색 창에서 **더 많은 서비스**를 클릭하고 **Azure Active Directory**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-130">Click on **More Services** in the left hand nav, and choose **Azure Active Directory**.</span></span>
4. <span data-ttu-id="f6155-131">**앱 등록**을 클릭하고 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-131">Click on **App registrations** and choose **Add**.</span></span>
5. <span data-ttu-id="f6155-132">프롬프트에 따라 새 **네이티브 클라이언트 응용 프로그램**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-132">Follow the prompts and create a new **Native Client Application**.</span></span>
  * <span data-ttu-id="f6155-133">응용 프로그램의 **이름** 은 최종 사용자에게 응용 프로그램을 설명하는 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-133">The **Name** of the application will describe your application to end-users</span></span>
  * <span data-ttu-id="f6155-134">**리디렉션 Uri** 는 Azure AD가 토큰 응답을 반환하는 데 사용하는 구성표 및 문자열 조합입니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-134">The **Redirect Uri** is a scheme and string combination that Azure AD will use to return token responses.</span></span>  <span data-ttu-id="f6155-135">지금은 자리 표시자 값(예: `http://DirectorySearcher`)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-135">Enter a placeholder value for now, e.g. `http://DirectorySearcher`.</span></span>  <span data-ttu-id="f6155-136">이 값은 나중에 바꿀 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-136">We'll replace this value later.</span></span>
6. <span data-ttu-id="f6155-137">등록을 완료하면 AAD는 앱에 고유한 응용 프로그램 ID를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-137">Once you’ve completed registration, AAD will assign your app a unique Application ID.</span></span>  <span data-ttu-id="f6155-138">이 값은 다음 섹션에서 필요하므로 응용 프로그램 탭에서 복사해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-138">You’ll need this value in the next sections, so copy it from the application tab.</span></span>
7. <span data-ttu-id="f6155-139">**설정** 페이지에서 **필요한 사용 권한**, **추가**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-139">From the **Settings** page, choose **Required Permissions** and choose **Add**.</span></span> <span data-ttu-id="f6155-140">**Microsoft Graph**를 API로 선택하고 **위임된 사용 권한**에서 **디렉터리 데이터 읽기** 사용 권한을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-140">Select the **Microsoft Graph** as the API and add the **Read Directory Data** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="f6155-141">이렇게 하면 응용 프로그램은 Graph API에서 사용자를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-141">This will enable your application to query the Graph API for users.</span></span>

## <a name="2-install--configure-adal"></a><span data-ttu-id="f6155-142">2. ADAL 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="f6155-142">2. Install & Configure ADAL</span></span>
<span data-ttu-id="f6155-143">Azure AD에서 응용 프로그램이 있으므로 ADAL을 설치하고 ID 관련 코드를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-143">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span></span>  <span data-ttu-id="f6155-144">ADAL이 Azura AD와 통신할 수 있게 하려면, 앱 등록에 관한 일부 정보를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-144">In order for ADAL to be able to communicate with Azure AD, you need to provide it with some information about your app registration.</span></span>

* <span data-ttu-id="f6155-145">먼저 패키지 관리자 콘솔을 사용하여 ADAL을 DirectorySearcher 프로젝트에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-145">Begin by adding ADAL to the DirectorySearcher project using the Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

* <span data-ttu-id="f6155-146">DirectorySearcher 프로젝트에서 `MainPage.xaml.cs`를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-146">In the DirectorySearcher project, open `MainPage.xaml.cs`.</span></span>  <span data-ttu-id="f6155-147">Azure 포털에 입력한 값을 반영하도록 `Config Values` 영역의 값을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-147">Replace the values in the `Config Values` region to reflect the values you input into the Azure Portal.</span></span>  <span data-ttu-id="f6155-148">코드는 ADAL을 사용할 때마다 이러한 값을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-148">Your code will reference these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="f6155-149">`tenant` 는 Azure AD 테넌트의 도메인(예: contoso.onmicrosoft.com)입니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-149">The `tenant` is the domain of your Azure AD tenant, e.g. contoso.onmicrosoft.com</span></span>
  * <span data-ttu-id="f6155-150">`clientId` 는 포털에서 복사한 응용 프로그램의 clientId여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-150">The `clientId` is the clientId of your application you copied from the portal.</span></span>
* <span data-ttu-id="f6155-151">이제 Windows Phone 앱에 대한 콜백 uri를 검색해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-151">You now need to discover the callback uri for your Windows Phone app.</span></span>  <span data-ttu-id="f6155-152">이 줄의 `MainPage` 메서드에 중단점을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-152">Set a breakpoint on this line in the `MainPage` method:</span></span>

```
redirectURI = Windows.Security.Authentication.Web.WebAuthenticationBroker.GetCurrentApplicationCallbackUri();
```
* <span data-ttu-id="f6155-153">앱을 실행하고 중단점을 만나면 `redirectUri` 값을 따로 복사해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-153">Run the app, and copy aside the value of `redirectUri` when the breakpoint is hit.</span></span>  <span data-ttu-id="f6155-154">다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-154">It should look something like</span></span>

```
ms-app://s-1-15-2-1352796503-54529114-405753024-3540103335-3203256200-511895534-1429095407/
```

* <span data-ttu-id="f6155-155">Azure 관리 포털에서 응용 프로그램의 **구성** 탭으로 돌아가서 **RedirectUri** 값을 이 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-155">Back on the **Configure** tab of your application in the Azure Management Portal, replace the value of the **RedirectUri** with this value.</span></span>  

## <a name="3-use-adal-to-get-tokens-from-aad"></a><span data-ttu-id="f6155-156">3. ADAL을 사용하여 AAD에서 토큰을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-156">3. Use ADAL to Get Tokens from AAD</span></span>
<span data-ttu-id="f6155-157">ADAL에서 확인되는 기본 원칙은 액세스 토큰이 필요할 때마다 앱이 `authContext.AcquireToken(…)`을 호출하고 나머지 작업은 ADAL이 수행한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-157">The basic principle behind ADAL is that whenever your app needs an access token, it simply calls `authContext.AcquireToken(…)`, and ADAL does the rest.</span></span>  

* <span data-ttu-id="f6155-158">첫 번째 단계는 앱의 `AuthenticationContext` , 즉 ADAL의 기본 클래스를 초기화하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-158">The first step is to initialize your app’s `AuthenticationContext` - ADAL’s primary class.</span></span>  <span data-ttu-id="f6155-159">이 클래스에서 Azure AD와 통신하는 데 필요한 좌표를 ADAL에 전달하고 토큰 캐시 방법을 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-159">This is where you pass ADAL the coordinates it needs to communicate with Azure AD and tell it how to cache tokens.</span></span>

```C#
public MainPage()
{
    ...

    // ADAL for Windows Phone 8.1 builds AuthenticationContext instances through a factory
    authContext = AuthenticationContext.CreateAsync(authority).GetResults();
}
```

* <span data-ttu-id="f6155-160">이제 사용자가 앱의 UI에서 "검색" 단추를 클릭할 때 호출되는 `Search(...)` 메서드를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-160">Now locate the `Search(...)` method, which will be invoked when the user cliks the "Search" button in the app's UI.</span></span>  <span data-ttu-id="f6155-161">이 메서드는 Azure AD Graph API에 해당 UPN이 지정된 검색어로 시작하는 사용자를 쿼리하라는 GET 요청을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-161">This method makes a GET request to the Azure AD Graph API to query for users whose UPN begins with the given search term.</span></span>  <span data-ttu-id="f6155-162">그렇지만 Graph API를 쿼리하려면 ADAL이 연결되는 요청의 `Authorization` 헤더에 access_token을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-162">But in order to query the Graph API, you need to include an access_token in the `Authorization` header of the request - this is where ADAL comes in.</span></span>

```C#
private async void Search(object sender, RoutedEventArgs e)
{
    ...

    // Try to get a token without triggering any user prompt.
    // ADAL will check whether the requested token is in ADAL's token cache or can otherwise be obtained without user interaction.
    AuthenticationResult result = await authContext.AcquireTokenSilentAsync(graphResourceId, clientId);
    if (result != null && result.Status == AuthenticationStatus.Success)
    {
        // A token was successfully retrieved.
        QueryGraph(result);
    }
    else
    {
        // Acquiring a token without user interaction was not possible.
        // Trigger an authentication experience and specify that once a token has been obtained the QueryGraph method should be called
        authContext.AcquireTokenAndContinue(graphResourceId, clientId, redirectURI, QueryGraph);
    }
}
```
* <span data-ttu-id="f6155-163">대화형 인증이 필요한 경우 ADAL은 Windows Phone의 WAB(Web Authentication Broker) 및 [연속 모델](http://www.cloudidentity.com/blog/2014/06/16/adal-for-windows-phone-8-1-deep-dive/) 을 사용하여 Azure AD 로그인 페이지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-163">If interactive authentication is necessary, ADAL will use Windows Phone's Web Authentication Broker (WAB) and [continuation model](http://www.cloudidentity.com/blog/2014/06/16/adal-for-windows-phone-8-1-deep-dive/) to display the Azure AD sign in page.</span></span>  <span data-ttu-id="f6155-164">사용자가 로그인하는 경우 앱은 WAB 상호 작용의 결과를 ADAL에 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-164">When the user signs in, your app needs to pass ADAL the results of the WAB interaction.</span></span>  <span data-ttu-id="f6155-165">이 작업은 `ContinueWebAuthentication` 인터페이스를 구현하는 것만큼 간단합니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-165">This is as simple as implementing the `ContinueWebAuthentication` interface:</span></span>

```C#
// This method is automatically invoked when the application
// is reactivated after an authentication interaction through WebAuthenticationBroker.
public async void ContinueWebAuthentication(WebAuthenticationBrokerContinuationEventArgs args)
{
    // pass the authentication interaction results to ADAL, which will
    // conclude the token acquisition operation and invoke the callback specified in AcquireTokenAndContinue.
    await authContext.ContinueAcquireTokenAsync(args);
}
```

* <span data-ttu-id="f6155-166">이제 ADAL이 앱에 반환한 `AuthenticationResult` 를 사용할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-166">Now it's time to use the `AuthenticationResult` that ADAL returned to your app.</span></span>  <span data-ttu-id="f6155-167">`QueryGraph(...)` 콜백에서 획득한 access_token을 Authorization 헤더의 GET 요청에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-167">In the `QueryGraph(...)` callback, attach the access_token you acquired to the GET request in the Authorization header:</span></span>

```C#
private async void QueryGraph(AuthenticationResult result)
{
    if (result.Status != AuthenticationStatus.Success)
    {
        MessageDialog dialog = new MessageDialog(string.Format("If the error continues, please contact your administrator.\n\nError: {0}\n\nError Description:\n\n{1}", result.Error, result.ErrorDescription), "Sorry, an error occurred while signing you in.");
        await dialog.ShowAsync();
    }

    // Add the access token to the Authorization Header of the call to the Graph API, and call the Graph API.
    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);

    ...
}
```
* <span data-ttu-id="f6155-168">`AuthenticationResult` 개체를 사용하여 앱에 사용자에 대한 정보를 표시할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-168">You can also use the `AuthenticationResult` object to display information about the user in your app.</span></span> <span data-ttu-id="f6155-169">`QueryGraph(...)` 메서드에서 해당 결과를 사용하여 페이지에 사용자의 ID를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-169">In the `QueryGraph(...)` method, use the result to show the user's id on the page:</span></span>

```C#
// Update the Page UI to represent the signed in user
ActiveUser.Text = result.UserInfo.DisplayableId;
```
* <span data-ttu-id="f6155-170">마지막으로 ADAL을 사용하여 응용 프로그램에서 사용자를 로그아웃할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-170">Finally, you can use ADAL to sign the user out of hte application as well.</span></span>  <span data-ttu-id="f6155-171">여기서는 사용자가 "로그아웃" 단추를 클릭한 경우 다음 `AcquireTokenSilentAsync(...)` 호출이 실패하도록 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-171">When the user clicks the "Sign Out" button, we want to ensure that the next call to `AcquireTokenSilentAsync(...)` will fail.</span></span>  <span data-ttu-id="f6155-172">ADAL을 사용하면 이 작업은 토큰 캐시를 지우는 것 만큼 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-172">With ADAL, this is as easy as clearing the token cache:</span></span>

```C#
private void SignOut()
{
    // Clear session state from the token cache.
    authContext.TokenCache.Clear();

    ...
}
```

<span data-ttu-id="f6155-173">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-173">Congratulations!</span></span> <span data-ttu-id="f6155-174">이제 사용자를 인증하고 OAuth 2.0을 사용하여 Web API를 안전하게 호출하고, 사용자에 대한 기본 정보를 가져올 수 있는 Windows Phone 앱이 작성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-174">You now have a working Windows Phone app that has the ability to authenticate users, securely call Web APIs using OAuth 2.0, and get basic information about the user.</span></span>  <span data-ttu-id="f6155-175">아직 일부 사용자로 테넌트를 채우지 않은 경우 지금 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-175">If you haven’t already, now is the time to populate your tenant with some users.</span></span>  <span data-ttu-id="f6155-176">DirectorySearcher 앱을 실행하고 해당 사용자 중 하나로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-176">Run your DirectorySearcher app, and sign in with one of those users.</span></span>  <span data-ttu-id="f6155-177">해당 UPN에 따라 다른 사용자를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-177">Search for other users based on their UPN.</span></span>  <span data-ttu-id="f6155-178">앱을 닫았다가 다시 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-178">Close the app, and re-run it.</span></span>  <span data-ttu-id="f6155-179">사용자의 세션을 그대로 유지하는 방법을 알아두세요.</span><span class="sxs-lookup"><span data-stu-id="f6155-179">Notice how the user’s session remains intact.</span></span>  <span data-ttu-id="f6155-180">로그아웃했다가 다른 사용자로 다시 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-180">Sign out, and sign back in as another user.</span></span>

<span data-ttu-id="f6155-181">ADAL은 응용 프로그램에 이러한 모든 일반적인 ID 기능을 쉽게 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-181">ADAL makes it easy to incorporate all of these common identity features into your application.</span></span>  <span data-ttu-id="f6155-182">또한 캐시 관리, OAuth 프로토콜 지원, 사용자에게 로그인 UI 제공, 만료된 토큰 새로 고침 등의 모든 귀찮은 작업을 관리해줍니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-182">It takes care of all the dirty work for you - cache management, OAuth protocol support, presenting the user with a login UI, refreshing expired tokens, and more.</span></span>  <span data-ttu-id="f6155-183">실제로 알아두어야 할 모든 항목은 단일 API 호출, `authContext.AcquireToken*(…)`입니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-183">All you really need to know is a single API call, `authContext.AcquireToken*(…)`.</span></span>

<span data-ttu-id="f6155-184">참조를 위해 완성된 샘플(사용자 구성 값 제외)이 [여기](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip)에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-184">For reference, the completed sample (without your configuration values) is provided [here](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span></span>  <span data-ttu-id="f6155-185">이제 추가 ID 시나리오로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-185">You can now move on to additional identity scenarios.</span></span>  <span data-ttu-id="f6155-186">다음 작업을 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6155-186">You may want to try:</span></span>

[<span data-ttu-id="f6155-187">Azure AD를 사용하여 .NET Web API 보안 유지 >></span><span class="sxs-lookup"><span data-stu-id="f6155-187">Secure a .NET Web API with Azure AD >></span></span>](active-directory-devquickstarts-webapi-dotnet.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]


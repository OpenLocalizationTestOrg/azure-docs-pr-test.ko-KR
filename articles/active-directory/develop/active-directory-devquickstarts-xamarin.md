---
title: "Azure AD Xamarin 시작 | Microsoft 문서"
description: "로그인을 위해 Azure AD와 통합되고 OAuth를 사용하여 Azure AD로 보호되는 API를 호출하는 Xamarin 응용 프로그램을 빌드합니다."
services: active-directory
documentationcenter: xamarin
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 198cd2c3-f7c8-4ec2-b59d-dfdea9fe7d95
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 54ee403f283bc5dc79911e2e813dd513ff595828
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="integrate-azure-ad-with-xamarin-apps"></a><span data-ttu-id="568cf-103">Xamarin 앱에 Azure AD 통합</span><span class="sxs-lookup"><span data-stu-id="568cf-103">Integrate Azure AD with Xamarin apps</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="568cf-104">Xamarin을 사용하면 iOS, Android 및 Windows(모바일 장치 및 PC)에서 실행할 수 있는 Mobile Apps를 C#으로 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-104">With Xamarin, you can write mobile apps in C# that can run on iOS, Android, and Windows (mobile devices and PCs).</span></span> <span data-ttu-id="568cf-105">Xamarin을 사용하여 앱을 빌드하는 경우 Azure AD(Azure Active Directory)를 사용하면 간단하게 Azure AD 계정으로 사용자를 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-105">If you're building an app using Xamarin, Azure Active Directory (Azure AD) makes it simple to authenticate users with their Azure AD accounts.</span></span> <span data-ttu-id="568cf-106">또한 앱에서 Office 365 API 또는 Azure API 같은 Azure AD를 통해 보호되는 웹 API를 안전하게 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-106">The app can also securely consume any web API that's protected by Azure AD, such as the Office 365 APIs or the Azure API.</span></span>

<span data-ttu-id="568cf-107">보호된 리소스에 액세스해야 하는 Xamarin 앱의 경우 Azure AD는 ADAL(Active Directory 인증 라이브러리)을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-107">For Xamarin apps that need to access protected resources, Azure AD provides the Active Directory Authentication Library (ADAL).</span></span> <span data-ttu-id="568cf-108">ADAL의 유일한 용도는 앱이 쉽게 액세스 토큰을 가져오도록 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-108">The sole purpose of ADAL is to make it easy for apps to get access tokens.</span></span> <span data-ttu-id="568cf-109">이 작업이 얼마나 쉬운지 보여 드리기 위해 이 문서에서는 다음 작업을 수행하는 DirectorySearcher 앱을 빌드해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-109">To demonstrate how easy it is, this article shows how to build DirectorySearcher apps that:</span></span>

* <span data-ttu-id="568cf-110">iOS, Android, Windows 데스크톱, Windows Phone 및 Windows 스토어에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-110">Run on iOS, Android, Windows Desktop, Windows Phone, and Windows Store.</span></span>
* <span data-ttu-id="568cf-111">단일 PCL(이식 가능 클래스 라이브러리)을 사용하여 사용자를 인증하고 Azure AD Graph API에 대한 토큰을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-111">Use a single portable class library (PCL) to authenticate users and get tokens for the Azure AD Graph API.</span></span>
* <span data-ttu-id="568cf-112">지정된 UPN을 가진 사용자를 디렉터리에서 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-112">Search a directory for users with a given UPN.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="568cf-113">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="568cf-113">Before you get started</span></span>
* <span data-ttu-id="568cf-114">[기본 프로젝트](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/skeleton.zip)를 다운로드하거나 [완성된 샘플](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip)을 다운로드하세요.</span><span class="sxs-lookup"><span data-stu-id="568cf-114">Download the [skeleton project](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/skeleton.zip), or download the [completed sample](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="568cf-115">각 다운로드는 Visual Studio 2013 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-115">Each download is a Visual Studio 2013 solution.</span></span>
* <span data-ttu-id="568cf-116">또한 사용자를 만들고 앱을 등록할 Azure AD 테넌트도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-116">You also need an Azure AD tenant in which to create users and register the app.</span></span> <span data-ttu-id="568cf-117">테넌트가 아직 없는 경우 [얻는 방법을 알아보세요](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="568cf-117">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="568cf-118">준비가 완료되면 다음 4가지 섹션의 절차를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-118">When you are ready, follow the procedures in the next four sections.</span></span>

## <a name="step-1-set-up-your-xamarin-development-environment"></a><span data-ttu-id="568cf-119">1단계: Xamarin 개발 환경 설정</span><span class="sxs-lookup"><span data-stu-id="568cf-119">Step 1: Set up your Xamarin development environment</span></span>
<span data-ttu-id="568cf-120">이 자습서에는 iOS, Android 및 Windows용 프로젝트가 포함되어 있으므로 Visual Studio와 Xamarin이 둘 다 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-120">Because this tutorial includes projects for iOS, Android, and Windows, you need both Visual Studio and Xamarin.</span></span> <span data-ttu-id="568cf-121">필요한 환경을 만들려면 MSDN에서 [Visual Studio 및 Xamarin 설정 및 설치](https://msdn.microsoft.com/library/mt613162.aspx)의 프로세스를 완료하세요.</span><span class="sxs-lookup"><span data-stu-id="568cf-121">To create the necessary environment, complete the process in [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) on MSDN.</span></span> <span data-ttu-id="568cf-122">이러한 지침에는 설치 관리자가 완료되기를 기다리는 동안 Xamarin에 대해 자세히 알아보기 위해 검토할 수 있는 자료가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-122">The instructions include material that you can review to learn more about Xamarin while you're waiting for the installations to be completed.</span></span>

<span data-ttu-id="568cf-123">필요한 설정을 마치면 Visual Studio에서 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-123">After you've completed the setup, open the solution in Visual Studio.</span></span> <span data-ttu-id="568cf-124">그러면 5개의 플랫폼별 프로젝트와 모든 플랫폼에서 공유되는 1개의 PCL, DirectorySearcher.cs의 6개 프로젝트를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-124">There, you will find six projects: five platform-specific projects and one PCL, DirectorySearcher.cs, which will be shared across all platforms.</span></span>

## <a name="step-2-register-the-directorysearcher-app"></a><span data-ttu-id="568cf-125">2단계: DirectorySearcher 앱 등록</span><span class="sxs-lookup"><span data-stu-id="568cf-125">Step 2: Register the DirectorySearcher app</span></span>
<span data-ttu-id="568cf-126">앱에서 토큰을 가져올 수 있도록 먼저 Azure AD 테넌트에 앱을 등록하고 Azure AD Graph API에 액세스할 수 있는 권한을 부여해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-126">To enable the app to get tokens, you first need to register it in your Azure AD tenant and grant it permission to access the Azure AD Graph API.</span></span> <span data-ttu-id="568cf-127">방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-127">Here's how:</span></span>

1. <span data-ttu-id="568cf-128">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-128">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="568cf-129">위쪽 막대에서 계정을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-129">On the top bar, click your account.</span></span> <span data-ttu-id="568cf-130">그런 다음 **디렉터리** 목록에서 앱을 등록할 Active Directory 테넌트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-130">Then, under the **Directory** list, select the Active Directory tenant where you want to register the app.</span></span>
3. <span data-ttu-id="568cf-131">왼쪽 창에서 **더 많은 서비스**를 클릭하고 **Azure Active Directory**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-131">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="568cf-132">**앱 등록**을 클릭하고 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-132">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="568cf-133">새 **네이티브 클라이언트 응용 프로그램**을 만들려면 지시를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-133">To create a new **Native Client Application**, follow the prompts.</span></span>
  * <span data-ttu-id="568cf-134">**이름**은 사용자에게 앱에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-134">**Name** describes the app to users.</span></span>
  * <span data-ttu-id="568cf-135">**리디렉션 URI**는 Azure AD가 토큰 응답을 반환하는 데 사용하는 구성표 및 문자열의 조합입니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-135">**Redirect URI** is a scheme and string combination that Azure AD uses to return token responses.</span></span> <span data-ttu-id="568cf-136">값(예:  http://DirectorySearcher )을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-136">Enter a value (for example, http://DirectorySearcher).</span></span>
6. <span data-ttu-id="568cf-137">등록이 완료되면 Azure AD가 앱에 고유한 응용 프로그램 ID를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-137">After you’ve completed registration, Azure AD assigns the app a unique application ID.</span></span> <span data-ttu-id="568cf-138">**응용 프로그램** 탭에서 이 값을 복사해 둡니다. 나중에 이 값이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-138">Copy the value from the **Application** tab, because you'll need it later.</span></span>
7. <span data-ttu-id="568cf-139">**설정** 페이지에서 **필요한 사용 권한**, **추가**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-139">On the **Settings** page, select **Required Permissions**, and then select **Add**.</span></span>
8. <span data-ttu-id="568cf-140">API로 **Microsoft Graph**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-140">Select **Microsoft Graph** as the API.</span></span> <span data-ttu-id="568cf-141">**위임된 권한**에서 **디렉터리 데이터 읽기** 권한을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-141">Under **Delegated Permissions**, add the **Read Directory Data** permission.</span></span>  
<span data-ttu-id="568cf-142">이렇게 하면 앱에서 사용자의 Graph API를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-142">This action enables the app to query the Graph API for users.</span></span>

## <a name="step-3-install-and-configure-adal"></a><span data-ttu-id="568cf-143">3단계: ADAL 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="568cf-143">Step 3: Install and configure ADAL</span></span>
<span data-ttu-id="568cf-144">Azure AD에 앱이 있으므로 ADAL을 설치하고 ID 관련 코드를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-144">Now that you have an app in Azure AD, you can install ADAL and write your identity-related code.</span></span> <span data-ttu-id="568cf-145">ADAL이 Azure AD와 통신할 수 있도록 앱 등록에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-145">To enable ADAL to communicate with Azure AD, give it some information about the app registration.</span></span>

1. <span data-ttu-id="568cf-146">패키지 관리자 콘솔을 사용하여 ADAL을 DirectorySearcher 프로젝트에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-146">Add ADAL to the DirectorySearcher project by using the Package Manager Console.</span></span>

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirectorySearcherLib
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-Android
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-Desktop
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-iOS
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-Universal
    `

    <span data-ttu-id="568cf-147">ADAL의 PCL 부분과 플랫폼별 부분의 두 라이브러리 참조가 각 프로젝트에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-147">Note that two library references are added to each project: the PCL portion of ADAL and a platform-specific portion.</span></span>
2. <span data-ttu-id="568cf-148">DirectorySearcherLib 프로젝트에서 DirectorySearcher.cs를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-148">In the DirectorySearcherLib project, open DirectorySearcher.cs.</span></span>
3. <span data-ttu-id="568cf-149">클래스 멤버 값을 Azure Portal에서 입력한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-149">Replace the class member values with the values that you entered in the Azure portal.</span></span> <span data-ttu-id="568cf-150">코드에서 ADAL을 사용할 때마다 이러한 값을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-150">Your code refers to these values whenever it uses ADAL.</span></span>

  * <span data-ttu-id="568cf-151">*테넌트*는 Azure AD 테넌트의 도메인(예: contoso.onmicrosoft.com)입니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-151">The *tenant* is the domain of your Azure AD tenant (for example, contoso.onmicrosoft.com).</span></span>
  * <span data-ttu-id="568cf-152">*clientId*는 포털에서 복사한 앱의 클라이언트 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-152">The *clientId* is the client ID of the app, which you copied from the portal.</span></span>
  * <span data-ttu-id="568cf-153">*returnUri*는 포털에 입력한 리디렉션 URI(예: http://DirectorySearcher )입니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-153">The *returnUri* is the redirect URI that you entered in the portal (for example, http://DirectorySearcher).</span></span>

## <a name="step-4-use-adal-to-get-tokens-from-azure-ad"></a><span data-ttu-id="568cf-154">4단계: ADAL을 사용하여 Azure AD에서 토큰 가져오기</span><span class="sxs-lookup"><span data-stu-id="568cf-154">Step 4: Use ADAL to get tokens from Azure AD</span></span>
<span data-ttu-id="568cf-155">거의 모든 앱 인증 논리가 `DirectorySearcher.SearchByAlias(...)`에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-155">Almost all of the app's authentication logic lies in `DirectorySearcher.SearchByAlias(...)`.</span></span> <span data-ttu-id="568cf-156">플랫폼별 프로젝트에서는 `DirectorySearcher` PCL에 컨텍스트 매개 변수를 전달하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-156">All that's necessary in the platform-specific projects is to pass a contextual parameter to the `DirectorySearcher` PCL.</span></span>

1. <span data-ttu-id="568cf-157">DirectorySearcher.cs를 연 다음 새 매개 변수를 `SearchByAlias(...)` 메서드에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-157">Open DirectorySearcher.cs, and then add a new parameter to the `SearchByAlias(...)` method.</span></span> <span data-ttu-id="568cf-158">`IPlatformParameters`는 ADAL이 인증을 수행하는 데 필요한 플랫폼별 개체를 캡슐화하는 컨텍스트 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-158">`IPlatformParameters` is the contextual parameter that encapsulates the platform-specific objects that ADAL needs to perform the authentication.</span></span>

    ```C#
    public static async Task<List<User>> SearchByAlias(string alias, IPlatformParameters parent)
    {
    ```

2. <span data-ttu-id="568cf-159">ADAL의 기본 클래스인 `AuthenticationContext`를 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-159">Initialize `AuthenticationContext`, which is the primary class of ADAL.</span></span>  
<span data-ttu-id="568cf-160">이 작업을 수행하면 Azure AD와 통신하는 데 필요한 좌표가 ADAL에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-160">This action passes ADAL the coordinates it needs to communicate with Azure AD.</span></span>
3. <span data-ttu-id="568cf-161">그런 다음 `AcquireTokenAsync(...)`를 호출합니다. 이 메서드는 `IPlatformParameters` 개체를 수락하고 앱에 토큰을 반환하는 데 필요한 인증 흐름을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-161">Call `AcquireTokenAsync(...)`, which accepts the `IPlatformParameters` object and invokes the authentication flow that's necessary to return a token to the app.</span></span>

    ```C#
    ...
        AuthenticationResult authResult = null;
        try
        {
            AuthenticationContext authContext = new AuthenticationContext(authority);
            authResult = await authContext.AcquireTokenAsync(graphResourceUri, clientId, returnUri, parent);
        }
        catch (Exception ee)
        {
            results.Add(new User { error = ee.Message });
            return results;
        }
    ...
    ```

    <span data-ttu-id="568cf-162">`AcquireTokenAsync(...)`는 먼저 사용자에게 자격 증명을 요구하지 않고(이전 토큰을 캐시하거나 새로 고침) 요청된 리소스(이 경우 Graph API)에 대한 토큰을 반환하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-162">`AcquireTokenAsync(...)` first attempts to return a token for the requested resource (the Graph API in this case) without prompting users to enter their credentials (via caching or refreshing old tokens).</span></span> <span data-ttu-id="568cf-163">필요한 경우에만 요청된 토큰을 획득하기 전에 사용자에게 Azure AD 로그인 페이지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-163">As necessary, it shows users the Azure AD sign-in page before acquiring the requested token.</span></span>
4. <span data-ttu-id="568cf-164">**Authorization** 헤더의 Graph API GET 요청에 액세스 토큰을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-164">Attach the access token to the Graph API request in the **Authorization** header:</span></span>

    ```C#
    ...
        request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", authResult.AccessToken);
    ...
    ```

<span data-ttu-id="568cf-165">`DirectorySearcher` PCL 및 앱의 ID 관련 코드에 대한 작업이 끝났습니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-165">That's all for the `DirectorySearcher` PCL and the app's identity-related code.</span></span> <span data-ttu-id="568cf-166">이제 각 플랫폼 보기에서 `SearchByAlias(...)` 메서드를 호출하고, 필요한 경우 UI 수명 주기를 올바르게 처리하기 위한 코드를 추가하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-166">All that remains is to call the `SearchByAlias(...)` method in each platform's views and, where necessary, to add code for correctly handling the UI lifecycle.</span></span>

### <a name="android"></a><span data-ttu-id="568cf-167">Android</span><span class="sxs-lookup"><span data-stu-id="568cf-167">Android</span></span>
1. <span data-ttu-id="568cf-168">MainActivity.cs의 단추 클릭 처리기에서 `SearchByAlias(...)` 호출을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-168">In MainActivity.cs, add a call to `SearchByAlias(...)` in the button click handler:</span></span>

    ```C#
    List<User> results = await DirectorySearcher.SearchByAlias(searchTermText.Text, new PlatformParameters(this));
    ```
2. <span data-ttu-id="568cf-169">`OnActivityResult` 수명 주기 메서드를 재정의하여 인증 리디렉션을 해당 메서드로 다시 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-169">Override the `OnActivityResult` lifecycle method to forward any authentication redirects back to the appropriate method.</span></span> <span data-ttu-id="568cf-170">ADAL은 Android에서 이 작업을 위한 도우미 메서드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-170">ADAL provides a helper method for this in Android:</span></span>

    ```C#
    ...
    protected override void OnActivityResult(int requestCode, Result resultCode, Intent data)
    {
        base.OnActivityResult(requestCode, resultCode, data);
        AuthenticationAgentContinuationHelper.SetAuthenticationAgentContinuationEventArgs(requestCode, resultCode, data);
    }
    ...
    ```

### <a name="windows-desktop"></a><span data-ttu-id="568cf-171">Windows Desktop</span><span class="sxs-lookup"><span data-stu-id="568cf-171">Windows Desktop</span></span>
<span data-ttu-id="568cf-172">MainWindow.xaml.cs에서 데스크톱의 `PlatformParameters` 개체에 `WindowInteropHelper`를 전달하여 `SearchByAlias(...)`를 호출하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-172">In MainWindow.xaml.cs, make a call to `SearchByAlias(...)` by passing a `WindowInteropHelper` in the desktop's `PlatformParameters` object:</span></span>

```C#
List<User> results = await DirectorySearcher.SearchByAlias(
  SearchTermText.Text,
  new PlatformParameters(PromptBehavior.Auto, this.Handle));
```

#### <a name="ios"></a><span data-ttu-id="568cf-173">iOS</span><span class="sxs-lookup"><span data-stu-id="568cf-173">iOS</span></span>
<span data-ttu-id="568cf-174">DirSearchClient_iOSViewController.cs에서 iOS `PlatformParameters` 개체는 보기 컨트롤러에 대한 참조를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-174">In DirSearchClient_iOSViewController.cs, the iOS `PlatformParameters` object takes a reference to the View Controller:</span></span>

```C#
List<User> results = await DirectorySearcher.SearchByAlias(
  SearchTermText.Text,
  new PlatformParameters(PromptBehavior.Auto, this.Handle));
```

### <a name="windows-universal"></a><span data-ttu-id="568cf-175">Windows 범용</span><span class="sxs-lookup"><span data-stu-id="568cf-175">Windows Universal</span></span>
<span data-ttu-id="568cf-176">Windows 유니버설에서 MainPage.xaml.cs를 열고 `Search` 메서드를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-176">In Windows Universal, open MainPage.xaml.cs, and then implement the `Search` method.</span></span> <span data-ttu-id="568cf-177">이 메서드는 공유 프로젝트의 도우미 메서드를 사용하여 필요에 따라 UI를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-177">This method uses a helper method in a shared project to update UI as necessary.</span></span>

```C#
...
List<User> results = await DirectorySearcherLib.DirectorySearcher.SearchByAlias(SearchTermText.Text, new PlatformParameters(PromptBehavior.Auto, false));
...
```

## <a name="whats-next"></a><span data-ttu-id="568cf-178">다음 단계</span><span class="sxs-lookup"><span data-stu-id="568cf-178">What's next</span></span>
<span data-ttu-id="568cf-179">이제 5개의 서로 다른 플랫폼에서 OAuth 2.0을 사용하여 사용자를 인증하고 안전하게 Web API를 호출할 수 있는 Xamarin 앱이 작성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-179">You now have a working Xamarin app that can authenticate users and securely call web APIs by using OAuth 2.0 across five different platforms.</span></span>

<span data-ttu-id="568cf-180">아직 사용자로 테넌트를 채우지 않은 경우 지금 채울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-180">If you haven’t already populated your tenant with users, now is the time to do so.</span></span>

1. <span data-ttu-id="568cf-181">DirectorySearcher 앱을 실행하고 해당 사용자 중 하나로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-181">Run your DirectorySearcher app, and then sign in with one of the users.</span></span>
2. <span data-ttu-id="568cf-182">해당 UPN에 따라 다른 사용자를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-182">Search for other users based on their UPN.</span></span>

<span data-ttu-id="568cf-183">ADAL은 앱에 일반적인 ID 기능을 쉽게 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-183">ADAL makes it easy to incorporate common identity features into the app.</span></span> <span data-ttu-id="568cf-184">또한 캐시 관리, OAuth 프로토콜 지원, 사용자에게 로그인 UI 제공, 만료된 토큰 새로 고침 등의 모든 귀찮은 작업을 대신 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-184">It takes care of all the dirty work for you, such as cache management, OAuth protocol support, presenting the user with a login UI, and refreshing expired tokens.</span></span> <span data-ttu-id="568cf-185">사용자는 단일 API 호출 `authContext.AcquireToken*(…)`만 알고 있으면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-185">You need to know only a single API call, `authContext.AcquireToken*(…)`.</span></span>

<span data-ttu-id="568cf-186">참조용 자료로 [완성된 샘플](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip)(사용자 구성 값 제외)을 다운로드하세요.</span><span class="sxs-lookup"><span data-stu-id="568cf-186">For reference, download the [completed sample](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip) (without your configuration values).</span></span>

<span data-ttu-id="568cf-187">이제 추가 ID 시나리오로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="568cf-187">You can now move on to additional identity scenarios.</span></span> <span data-ttu-id="568cf-188">예를 들어 [Azure AD를 사용하여 .NET Web API 보안 유지](active-directory-devquickstarts-webapi-dotnet.md)를 시도해 보세요.</span><span class="sxs-lookup"><span data-stu-id="568cf-188">For example, try [Secure a .NET Web API with Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

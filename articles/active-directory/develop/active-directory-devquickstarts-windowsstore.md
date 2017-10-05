---
title: "Azure AD Windows 스토어 시작 | Microsoft 문서"
description: "로그인을 위해 Azure AD와 통합되고 OAuth를 사용하여 Azure AD로 보호되는 API를 호출하는 Windows 스토어 앱을 빌드합니다."
services: active-directory
documentationcenter: windows
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 3b96a6d1-270b-4ac1-b9b5-58070c896a68
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 09/16/2016
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 6b5189dc06d7f8b0ed4426944948b904feba847e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="integrate-azure-ad-with-windows-store-apps"></a><span data-ttu-id="7e1f7-103">Azure AD와 Windows 스토어 앱 통합</span><span class="sxs-lookup"><span data-stu-id="7e1f7-103">Integrate Azure AD with Windows Store apps</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

> [!NOTE]
> <span data-ttu-id="7e1f7-104">Windows Store 8.1 및 이전 버전 프로젝트는 Visual Studio 2017에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-104">Windows Store 8.1 and prior version projects are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="7e1f7-105">자세한 내용은 [Visual Studio 2017 플랫폼 대상 지정 및 호환성](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-105">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

<span data-ttu-id="7e1f7-106">Windows 스토어용 앱을 개발하는 경우 Azure AD(Azure Active Directory)를 사용하면 간단하고 편리하게 Active Directory 계정으로 사용자를 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-106">If you're developing apps for the Windows Store, Azure Active Directory (Azure AD) makes it simple and straightforward to authenticate your users with their Active Directory accounts.</span></span> <span data-ttu-id="7e1f7-107">Azure AD와 통합하면 앱에서 Office 365 API 또는 Azure API 같은 Azure AD를 통해 보호되는 웹 API를 안전하게 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-107">By integrating with Azure AD, an app can securely consume any web API that's protected by Azure AD, such as the Office 365 APIs or the Azure API.</span></span>

<span data-ttu-id="7e1f7-108">보호된 리소스에 액세스해야 하는 Windows 스토어 데스크톱 앱의 경우 Azure AD는 ADAL(Active Directory 인증 라이브러리)을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-108">For Windows Store desktop apps that need to access protected resources, Azure AD provides the Active Directory Authentication Library (ADAL).</span></span> <span data-ttu-id="7e1f7-109">ADAL의 유일한 용도는 앱이 쉽게 액세스 토큰을 가져오도록 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-109">The sole purpose of ADAL is to make it easy for the app to get access tokens.</span></span> <span data-ttu-id="7e1f7-110">이 작업이 얼마나 쉬운지 보여 드리기 위해 이 문서에서는 다음 작업을 수행하는 DirectorySearcher Windows 스토어 앱을 빌드해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-110">To demonstrate how easy it is, this article shows how to build a DirectorySearcher Windows Store app that:</span></span>

* <span data-ttu-id="7e1f7-111">[OAuth 2.0 인증 프로토콜](https://msdn.microsoft.com/library/azure/dn645545.aspx)을 사용하여 Azure AD Graph API를 호출하기 위한 액세스 토큰을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-111">Gets access tokens for calling the Azure AD Graph API by using the [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="7e1f7-112">지정된 UPN(사용자 계정 이름)을 가진 사용자를 디렉터리에서 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-112">Searches a directory for users with a given user principal name (UPN).</span></span>
* <span data-ttu-id="7e1f7-113">사용자를 로그아웃합니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-113">Signs users out.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="7e1f7-114">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="7e1f7-114">Before you get started</span></span>
* <span data-ttu-id="7e1f7-115">[기본 프로젝트](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/skeleton.zip)를 다운로드하거나 [완성된 샘플](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip)을 다운로드하세요.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-115">Download the [skeleton project](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/skeleton.zip), or download the [completed sample](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip).</span></span> <span data-ttu-id="7e1f7-116">각 다운로드는 Visual Studio 2015 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-116">Each download is a Visual Studio 2015 solution.</span></span>
* <span data-ttu-id="7e1f7-117">또한 사용자를 만들고 앱을 등록할 Azure AD 테넌트도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-117">You also need an Azure AD tenant in which to create users and register the app.</span></span> <span data-ttu-id="7e1f7-118">테넌트가 아직 없는 경우 [얻는 방법을 알아보세요](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="7e1f7-118">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="7e1f7-119">준비기 완료되면 다음 세 섹션의 절차를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-119">When you are ready, follow the procedures in the next three sections.</span></span>

## <a name="step-1-register-the-directorysearcher-app"></a><span data-ttu-id="7e1f7-120">1단계: DirectorySearcher 앱 등록</span><span class="sxs-lookup"><span data-stu-id="7e1f7-120">Step 1: Register the DirectorySearcher app</span></span>
<span data-ttu-id="7e1f7-121">앱에서 토큰을 가져올 수 있도록 먼저 Azure AD 테넌트에 앱을 등록하고 Azure AD Graph API에 액세스할 수 있는 권한을 부여해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-121">To enable the app to get tokens, you first need to register it in your Azure AD tenant and grant it permission to access the Azure AD Graph API.</span></span> <span data-ttu-id="7e1f7-122">방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-122">Here's how:</span></span>

1. <span data-ttu-id="7e1f7-123">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-123">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="7e1f7-124">위쪽 막대에서 계정을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-124">On the top bar, click your account.</span></span> <span data-ttu-id="7e1f7-125">그런 다음 **디렉터리** 목록에서 앱을 등록할 Active Directory 테넌트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-125">Then, under the **Directory** list, select the Active Directory tenant where you want to register the app.</span></span>
3. <span data-ttu-id="7e1f7-126">왼쪽 창에서 **더 많은 서비스**를 클릭하고 **Azure Active Directory**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-126">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="7e1f7-127">**앱 등록**을 클릭하고 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-127">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="7e1f7-128">프롬프트에 따라 **네이티브 클라이언트 응용 프로그램**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-128">Follow the prompts to create a **Native Client Application**.</span></span>
  * <span data-ttu-id="7e1f7-129">**이름**은 사용자에게 앱에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-129">**Name** describes the app to users.</span></span>
  * <span data-ttu-id="7e1f7-130">**리디렉션 URI**는 Azure AD가 토큰 응답을 반환하는 데 사용하는 구성표 및 문자열의 조합입니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-130">**Redirect URI** is a scheme and string combination that Azure AD uses to return token responses.</span></span> <span data-ttu-id="7e1f7-131">이제 자리 표시자 값(예: **http://DirectorySearcher**)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-131">Enter a placeholder value for now (for example, **http://DirectorySearcher**).</span></span> <span data-ttu-id="7e1f7-132">이 값은 나중에 바꿀 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-132">You'll replace the value later.</span></span>
6. <span data-ttu-id="7e1f7-133">등록이 완료되면 Azure AD가 앱에 고유한 응용 프로그램 ID를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-133">After you’ve completed the registration, Azure AD assigns the app a unique application ID.</span></span> <span data-ttu-id="7e1f7-134">**응용 프로그램** 탭에서 이 값을 복사해 둡니다. 나중에 이 값이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-134">Copy the value on the **Application** tab, because you'll need it later.</span></span>
7. <span data-ttu-id="7e1f7-135">**설정** 페이지에서 **필요한 사용 권한**, **추가**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-135">On the **Settings** page, select **Required Permissions**, and then select **Add**.</span></span>
8. <span data-ttu-id="7e1f7-136">**Azure Active Directory** 앱의 경우 API로 **Microsoft Graph**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-136">For the **Azure Active Directory** app, select **Microsoft Graph** as the API.</span></span>
9. <span data-ttu-id="7e1f7-137">**위임된 권한**에서 **로그인한 사용자로 디렉터리 액세스** 권한을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-137">Under **Delegated Permissions**, add the **Access the directory as the signed-in user** permission.</span></span> <span data-ttu-id="7e1f7-138">이렇게 하면 앱에서 사용자의 Graph API를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-138">Doing so enables the app to query the Graph API for users.</span></span>

## <a name="step-2-install-and-configure-adal"></a><span data-ttu-id="7e1f7-139">2단계: ADAL 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="7e1f7-139">Step 2: Install and configure ADAL</span></span>
<span data-ttu-id="7e1f7-140">Azure AD에 앱이 있으므로 ADAL을 설치하고 ID 관련 코드를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-140">Now that you have an app in Azure AD, you can install ADAL and write your identity-related code.</span></span> <span data-ttu-id="7e1f7-141">ADAL이 Azure AD와 통신할 수 있도록 앱 등록에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-141">To enable ADAL to communicate with Azure AD, give it some information about the app registration.</span></span>

1. <span data-ttu-id="7e1f7-142">패키지 관리자 콘솔을 사용하여 ADAL을 DirectorySearcher 프로젝트에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-142">Add ADAL to the DirectorySearcher project by using the Package Manager Console.</span></span>

    ```
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
    ```

2. <span data-ttu-id="7e1f7-143">DirectorySearcher 프로젝트에서 MainPage.xaml.cs를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-143">In the DirectorySearcher project, open MainPage.xaml.cs.</span></span>
3. <span data-ttu-id="7e1f7-144">**구성 값** 영역의 값을 Azure Portal에서 입력한 값으로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-144">Replace the values in the **Config Values** region with the values that you entered in the Azure portal.</span></span> <span data-ttu-id="7e1f7-145">코드에서 ADAL을 사용할 때마다 이러한 값을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-145">Your code refers to these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="7e1f7-146">*테넌트*는 Azure AD 테넌트의 도메인(예: contoso.onmicrosoft.com)입니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-146">The *tenant* is the domain of your Azure AD tenant (for example, contoso.onmicrosoft.com).</span></span>
  * <span data-ttu-id="7e1f7-147">*clientId*는 포털에서 복사한 앱의 클라이언트 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-147">The *clientId* is the client ID of the app, which you copied from the portal.</span></span>
4. <span data-ttu-id="7e1f7-148">이제 Windows 스토어 앱의 콜백 URI를 검색해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-148">You now need to discover the callback URI for your Windows Store app.</span></span> <span data-ttu-id="7e1f7-149">이 줄의 `MainPage` 메서드에 중단점을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-149">Set a breakpoint on this line in the `MainPage` method:</span></span>
    ```
    redirectURI = Windows.Security.Authentication.Web.WebAuthenticationBroker.GetCurrentApplicationCallbackUri();
    ```
5. <span data-ttu-id="7e1f7-150">솔루션을 빌드하고 모든 패키지 참조가 복원되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-150">Build the solution, making sure that all package references are restored.</span></span> <span data-ttu-id="7e1f7-151">일부 패키지가 누락된 경우 NuGet 패키지 관리자를 열고 누락된 패키지를 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-151">If any packages are missing, open the NuGet Package Manager and restore them.</span></span>
6. <span data-ttu-id="7e1f7-152">앱을 실행하고, 중단점을 만나면 `redirectUri` 값을 복사해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-152">Run the app, and copy the value of `redirectUri` when the breakpoint is hit.</span></span> <span data-ttu-id="7e1f7-153">이 값은 다음과 비슷한 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-153">The value should look something like the following:</span></span>

    ```
    ms-app://s-1-15-2-1352796503-54529114-405753024-3540103335-3203256200-511895534-1429095407/
    ```

7. <span data-ttu-id="7e1f7-154">Azure Portal에서 앱의 **설정** 탭으로 돌아가서 **RedirectUri**를 이전 값으로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-154">Back on the **Settings** tab of the app in the Azure portal, add a **RedirectUri** with the preceding value.</span></span>  

## <a name="step-3-use-adal-to-get-tokens-from-azure-ad"></a><span data-ttu-id="7e1f7-155">3단계: ADAL을 사용하여 Azure AD에서 토큰 가져오기</span><span class="sxs-lookup"><span data-stu-id="7e1f7-155">Step 3: Use ADAL to get tokens from Azure AD</span></span>
<span data-ttu-id="7e1f7-156">ADAL에서 확인되는 기본 원칙은 액세스 토큰이 필요할 때마다 앱이 `authContext.AcquireToken(…)`을 호출하고 나머지 작업은 ADAL이 수행한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-156">The basic principle behind ADAL is that whenever the app needs an access token, it simply calls `authContext.AcquireToken(…)`, and ADAL does the rest.</span></span>  

1. <span data-ttu-id="7e1f7-157">ADAL의 기본 클래스인 앱의 `AuthenticationContext`를 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-157">Initialize the app’s `AuthenticationContext`, which is the primary class of ADAL.</span></span> <span data-ttu-id="7e1f7-158">이 작업은 Azure AD와 통신하는 데 필요한 좌표를 ADAL에 전달하고 토큰 캐시 방법을 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-158">This action passes ADAL the coordinates it needs to communicate with Azure AD and tell it how to cache tokens.</span></span>

    ```C#
    public MainPage()
    {
        ...

        authContext = new AuthenticationContext(authority);
    }
    ```

2. <span data-ttu-id="7e1f7-159">`Search(...)` 메서드를 찾습니다. 이 메서드는 사용자가 앱의 UI에서 **검색** 단추를 클릭할 때 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-159">Locate the `Search(...)` method, which is invoked when users click the **Search** button on the app's UI.</span></span> <span data-ttu-id="7e1f7-160">이 메서드는 Azure AD Graph API에 해당 UPN이 지정된 검색어로 시작하는 사용자를 쿼리하라는 get 요청을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-160">This method makes a get request to the Azure AD Graph API to query for users whose UPN begins with the given search term.</span></span> <span data-ttu-id="7e1f7-161">Graph API를 쿼리하려면 요청의 **Authorization** 헤더에 액세스 토큰을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-161">To query the Graph API, include an access token in the request's **Authorization** header.</span></span> <span data-ttu-id="7e1f7-162">여기로 ADAL이 들어옵니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-162">This is where ADAL comes in.</span></span>

    ```C#
    private async void Search(object sender, RoutedEventArgs e)
    {
        ...
        AuthenticationResult result = null;
        try
        {
            result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectURI, new PlatformParameters(PromptBehavior.Auto, false));
        }
        catch (AdalException ex)
        {
            if (ex.ErrorCode != "authentication_canceled")
            {
                ShowAuthError(string.Format("If the error continues, please contact your administrator.\n\nError: {0}\n\nError Description:\n\n{1}", ex.ErrorCode, ex.Message));
            }
            return;
        }
        ...
    }
    ```
    <span data-ttu-id="7e1f7-163">앱에서 `AcquireTokenAsync(...)`을 호출하여 토큰을 요청하면 ADAL은 사용자에게 자격 증명을 요구하지 않고 토큰을 반환하려고 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-163">When the app requests a token by calling `AcquireTokenAsync(...)`, ADAL attempts to return a token without asking the user for credentials.</span></span> <span data-ttu-id="7e1f7-164">ADAL은 사용자가 토큰을 가져오기 위해 로그인해야 한다고 판단할 경우 로그인 대화 상자를 표시하고, 사용자의 자격 증명을 수집하고, 인증 성공 시 토큰을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-164">If ADAL determines that the user needs to sign in to get a token, it displays a sign-in dialog box, collects the user's credentials, and returns a token after authentication succeeds.</span></span> <span data-ttu-id="7e1f7-165">어떤 이유로든 ADAL이 토큰을 반환할 수 없는 경우 *AuthenticationResult* 상태는 오류가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-165">If ADAL is unable to return a token for any reason, the *AuthenticationResult* status is an error.</span></span>
3. <span data-ttu-id="7e1f7-166">이제 방금 획득한 액세스 토큰을 사용해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-166">Now it's time to use the access token you just acquired.</span></span> <span data-ttu-id="7e1f7-167">또한 `Search(...)` 메서드에서 **Authorization** 헤더의 Graph API get 요청에 이 토큰을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-167">Also in the `Search(...)` method, attach the token to the Graph API get request in the **Authorization** header:</span></span>

    ```C#
    // Add the access token to the Authorization header of the call to the Graph API, and call the Graph API.
    httpClient.DefaultRequestHeaders.Authorization = new HttpCredentialsHeaderValue("Bearer", result.AccessToken);

    ```
4. <span data-ttu-id="7e1f7-168">`AuthenticationResult` 개체를 사용하여 앱에 사용자에 대한 정보(예: 사용자 ID)를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-168">You can use the `AuthenticationResult` object to display information about the user in the app, such as the user's ID:</span></span>

    ```C#
    // Update the page UI to represent the signed-in user
    ActiveUser.Text = result.UserInfo.DisplayableId;
    ```
5. <span data-ttu-id="7e1f7-169">ADAL을 사용하여 앱에서 사용자를 로그아웃할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-169">You can also use ADAL to sign users out of the app.</span></span> <span data-ttu-id="7e1f7-170">사용자가 **로그아웃** 단추를 클릭하면 다음 `AcquireTokenAsync(...)` 호출이 로그인 보기를 표시하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-170">When the user clicks the **Sign Out** button, ensure that the next call to `AcquireTokenAsync(...)` shows a sign-in view.</span></span> <span data-ttu-id="7e1f7-171">ADAL을 사용하면 이 작업은 토큰 캐시를 지우는 것 만큼 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-171">With ADAL, this action is as easy as clearing the token cache:</span></span>

    ```C#
    private void SignOut()
    {
        // Clear session state from the token cache.
        authContext.TokenCache.Clear();

        ...
    }
    ```

## <a name="whats-next"></a><span data-ttu-id="7e1f7-172">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7e1f7-172">What's next</span></span>
<span data-ttu-id="7e1f7-173">이제 사용자를 인증하고 OAuth 2.0을 사용하여 Web API를 안전하게 호출하고, 사용자에 대한 기본 정보를 가져올 수 있는 Windows 스토어 앱이 작동하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-173">You now have a working Windows Store app that can authenticate users, securely call web APIs using OAuth 2.0, and get basic information about the user.</span></span>

<span data-ttu-id="7e1f7-174">아직 사용자로 테넌트를 채우지 않은 경우 지금 채울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-174">If you haven’t already populated your tenant with users, now is the time to do so.</span></span>
1. <span data-ttu-id="7e1f7-175">DirectorySearcher 앱을 실행하고 해당 사용자 중 하나로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-175">Run your DirectorySearcher app, and then sign in with one of the users.</span></span>
2. <span data-ttu-id="7e1f7-176">해당 UPN에 따라 다른 사용자를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-176">Search for other users based on their UPN.</span></span>
3. <span data-ttu-id="7e1f7-177">앱을 닫았다가 다시 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-177">Close the app, and rerun it.</span></span> <span data-ttu-id="7e1f7-178">사용자의 세션을 그대로 유지하는 방법을 알아두세요.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-178">Notice how the user’s session remains intact.</span></span>
4. <span data-ttu-id="7e1f7-179">마우스 오른쪽 단추를 클릭하고 아래쪽 막대를 표시하여 로그아웃했다가 다른 사용자로 다시 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-179">Sign out by right-clicking to display the bottom bar, and then sign back in as another user.</span></span>

<span data-ttu-id="7e1f7-180">ADAL은 이 모든 일반적인 ID 기능을 앱에 쉽게 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-180">ADAL makes it easy to incorporate all these common identity features into the app.</span></span> <span data-ttu-id="7e1f7-181">또한 캐시 관리, OAuth 프로토콜 지원, 사용자에게 로그인 UI 제공, 만료된 토큰 새로 고침 등의 모든 귀찮은 작업을 대신 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-181">It takes care of all the dirty work for you, such as cache management, OAuth protocol support, presenting the user with a login UI, and refreshing expired tokens.</span></span> <span data-ttu-id="7e1f7-182">사용자는 단일 API 호출 `authContext.AcquireToken*(…)`만 알고 있으면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-182">You need to know only a single API call, `authContext.AcquireToken*(…)`.</span></span>

<span data-ttu-id="7e1f7-183">참조용 자료로 [완성된 샘플](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip)(사용자 구성 값 제외)을 다운로드하세요.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-183">For reference, download the [completed sample](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip) (without your configuration values).</span></span>

<span data-ttu-id="7e1f7-184">이제 추가 ID 시나리오로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-184">You can now move on to additional identity scenarios.</span></span> <span data-ttu-id="7e1f7-185">예를 들어 [Azure AD를 사용하여 .NET Web API 보안 유지](active-directory-devquickstarts-webapi-dotnet.md)를 시도해 보세요.</span><span class="sxs-lookup"><span data-stu-id="7e1f7-185">For example, try [Secure a .NET Web API with Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

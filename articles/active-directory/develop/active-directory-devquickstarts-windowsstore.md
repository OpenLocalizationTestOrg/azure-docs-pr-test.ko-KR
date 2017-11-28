---
title: "aaaAzure AD Windows 스토어를 시작 | Microsoft Docs"
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
ms.openlocfilehash: 1d12c7b928bc0e94fb823f8db4a09ff416205e2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-windows-store-apps"></a><span data-ttu-id="e62b5-103">Azure AD와 Windows 스토어 앱 통합</span><span class="sxs-lookup"><span data-stu-id="e62b5-103">Integrate Azure AD with Windows Store apps</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

> [!NOTE]
> <span data-ttu-id="e62b5-104">Windows Store 8.1 및 이전 버전 프로젝트는 Visual Studio 2017에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-104">Windows Store 8.1 and prior version projects are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="e62b5-105">자세한 내용은 [Visual Studio 2017 플랫폼 대상 지정 및 호환성](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e62b5-105">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

<span data-ttu-id="e62b5-106">Hello Windows 스토어 용 앱을 개발 하는 경우 Azure Active Directory (Azure AD) 사용 하면 쉽고 간단 tooauthenticate 사용자의 Active Directory 계정 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-106">If you're developing apps for hello Windows Store, Azure Active Directory (Azure AD) makes it simple and straightforward tooauthenticate your users with their Active Directory accounts.</span></span> <span data-ttu-id="e62b5-107">Azure AD와 통합 하 여 응용 프로그램 웹 hello Office 365 Api 또는 hello Azure API와 같은 Azure AD로 보호 되는 API를 안전 하 게 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-107">By integrating with Azure AD, an app can securely consume any web API that's protected by Azure AD, such as hello Office 365 APIs or hello Azure API.</span></span>

<span data-ttu-id="e62b5-108">Windows 스토어 데스크톱 응용 프로그램의 tooaccess 보호 된 리소스를 필요로 하는 경우 Azure AD hello Active Directory 인증 라이브러리 (ADAL)를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-108">For Windows Store desktop apps that need tooaccess protected resources, Azure AD provides hello Active Directory Authentication Library (ADAL).</span></span> <span data-ttu-id="e62b5-109">hello ADAL의 목적으로 toomake hello 앱 tooget 액세스 토큰을 쉽게 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-109">hello sole purpose of ADAL is toomake it easy for hello app tooget access tokens.</span></span> <span data-ttu-id="e62b5-110">toodemonstrate 얼마나 쉬운지 이면이 문서에서는 어떻게 toobuild DirectorySearcher Windows 저장 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-110">toodemonstrate how easy it is, this article shows how toobuild a DirectorySearcher Windows Store app that:</span></span>

* <span data-ttu-id="e62b5-111">가져옵니다 액세스 hello를 사용 하 여 hello Azure AD Graph API를 호출 하기 위한 토큰 [OAuth 2.0 인증 프로토콜](https://msdn.microsoft.com/library/azure/dn645545.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-111">Gets access tokens for calling hello Azure AD Graph API by using hello [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="e62b5-112">지정된 UPN(사용자 계정 이름)을 가진 사용자를 디렉터리에서 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-112">Searches a directory for users with a given user principal name (UPN).</span></span>
* <span data-ttu-id="e62b5-113">사용자를 로그아웃합니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-113">Signs users out.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="e62b5-114">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="e62b5-114">Before you get started</span></span>
* <span data-ttu-id="e62b5-115">Hello 다운로드 [기초 프로젝트](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/skeleton.zip), hello 다운로드 또는 [완성 된 샘플](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip)합니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-115">Download hello [skeleton project](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/skeleton.zip), or download hello [completed sample](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip).</span></span> <span data-ttu-id="e62b5-116">각 다운로드는 Visual Studio 2015 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-116">Each download is a Visual Studio 2015 solution.</span></span>
* <span data-ttu-id="e62b5-117">Toocreate 사용자 및 레지스터 hello 앱에서 Azure AD 테 넌 트가 있어야합니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-117">You also need an Azure AD tenant in which toocreate users and register hello app.</span></span> <span data-ttu-id="e62b5-118">테 넌 트 아직 없는 경우 [자세한 방법을 하나 tooget](active-directory-howto-tenant.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-118">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="e62b5-119">준비 되 면 다음 절차에 따라 hello hello 다음 3 개의 섹션.</span><span class="sxs-lookup"><span data-stu-id="e62b5-119">When you are ready, follow hello procedures in hello next three sections.</span></span>

## <a name="step-1-register-hello-directorysearcher-app"></a><span data-ttu-id="e62b5-120">1 단계: hello DirectorySearcher 앱 등록</span><span class="sxs-lookup"><span data-stu-id="e62b5-120">Step 1: Register hello DirectorySearcher app</span></span>
<span data-ttu-id="e62b5-121">tooenable hello 앱 tooget 토큰 먼저 tooregister에서 Azure AD 테 넌 트 및 사용 권한 tooaccess hello Azure AD Graph API에 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-121">tooenable hello app tooget tokens, you first need tooregister it in your Azure AD tenant and grant it permission tooaccess hello Azure AD Graph API.</span></span> <span data-ttu-id="e62b5-122">방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-122">Here's how:</span></span>

1. <span data-ttu-id="e62b5-123">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-123">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e62b5-124">Hello 위쪽 막대에서 계정을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-124">On hello top bar, click your account.</span></span> <span data-ttu-id="e62b5-125">그런 다음 hello **디렉터리** 목록, 선택 hello Active Directory 테 넌 트 tooregister hello 앱을 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-125">Then, under hello **Directory** list, select hello Active Directory tenant where you want tooregister hello app.</span></span>
3. <span data-ttu-id="e62b5-126">클릭 **더 서비스** 에 hello 왼쪽된 창에서 선택한 후 **Azure Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-126">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="e62b5-127">**앱 등록**을 클릭하고 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-127">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="e62b5-128">Hello 프롬프트 toocreate에 따라 한 **네이티브 클라이언트 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-128">Follow hello prompts toocreate a **Native Client Application**.</span></span>
  * <span data-ttu-id="e62b5-129">**이름** hello 앱 toousers에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-129">**Name** describes hello app toousers.</span></span>
  * <span data-ttu-id="e62b5-130">**리디렉션 URI** Azure AD에서는 tooreturn 토큰 응답 체계 및 문자열 조합입니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-130">**Redirect URI** is a scheme and string combination that Azure AD uses tooreturn token responses.</span></span> <span data-ttu-id="e62b5-131">이제 자리 표시자 값(예: **http://DirectorySearcher**)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-131">Enter a placeholder value for now (for example, **http://DirectorySearcher**).</span></span> <span data-ttu-id="e62b5-132">나중에 hello 값을 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-132">You'll replace hello value later.</span></span>
6. <span data-ttu-id="e62b5-133">Azure AD를 hello 등록을 완료 한 후 hello 앱 고유한 응용 프로그램 ID를 할당</span><span class="sxs-lookup"><span data-stu-id="e62b5-133">After you’ve completed hello registration, Azure AD assigns hello app a unique application ID.</span></span> <span data-ttu-id="e62b5-134">Hello에 hello 값 복사 **응용 프로그램** 탭, 나중에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-134">Copy hello value on hello **Application** tab, because you'll need it later.</span></span>
7. <span data-ttu-id="e62b5-135">Hello에 **설정** 페이지에서 **필요한 권한**를 선택한 후 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-135">On hello **Settings** page, select **Required Permissions**, and then select **Add**.</span></span>
8. <span data-ttu-id="e62b5-136">Hello에 대 한 **Azure Active Directory** 앱을 **Microsoft Graph** API hello으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-136">For hello **Azure Active Directory** app, select **Microsoft Graph** as hello API.</span></span>
9. <span data-ttu-id="e62b5-137">아래 **위임 된 권한**, hello 추가 **hello 로그인 한 사용자로 디렉터리에 액세스 hello** 권한.</span><span class="sxs-lookup"><span data-stu-id="e62b5-137">Under **Delegated Permissions**, add hello **Access hello directory as hello signed-in user** permission.</span></span> <span data-ttu-id="e62b5-138">이렇게 하면 특정 사용자에 대 한 hello 앱 tooquery hello Graph API입니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-138">Doing so enables hello app tooquery hello Graph API for users.</span></span>

## <a name="step-2-install-and-configure-adal"></a><span data-ttu-id="e62b5-139">2단계: ADAL 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="e62b5-139">Step 2: Install and configure ADAL</span></span>
<span data-ttu-id="e62b5-140">Azure AD에 앱이 있으므로 ADAL을 설치하고 ID 관련 코드를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-140">Now that you have an app in Azure AD, you can install ADAL and write your identity-related code.</span></span> <span data-ttu-id="e62b5-141">Azure AD와 tooenable ADAL toocommunicate hello 앱 등록에 대 한 정보를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-141">tooenable ADAL toocommunicate with Azure AD, give it some information about hello app registration.</span></span>

1. <span data-ttu-id="e62b5-142">Hello 패키지 관리자 콘솔을 사용 하 여 ADAL toohello DirectorySearcher 프로젝트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-142">Add ADAL toohello DirectorySearcher project by using hello Package Manager Console.</span></span>

    ```
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
    ```

2. <span data-ttu-id="e62b5-143">Hello DirectorySearcher 프로젝트에서 MainPage.xaml.cs를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-143">In hello DirectorySearcher project, open MainPage.xaml.cs.</span></span>
3. <span data-ttu-id="e62b5-144">Hello hello 값을 교체 **구성 값** hello Azure 포털에에서 입력 hello 값을 사용 하 여 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-144">Replace hello values in hello **Config Values** region with hello values that you entered in hello Azure portal.</span></span> <span data-ttu-id="e62b5-145">ADAL를 사용 하 여 때마다 코드 toothese 값을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-145">Your code refers toothese values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="e62b5-146">hello *테 넌 트* 여 Azure AD 테 넌 트 (예: contoso.onmicrosoft.com) hello 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-146">hello *tenant* is hello domain of your Azure AD tenant (for example, contoso.onmicrosoft.com).</span></span>
  * <span data-ttu-id="e62b5-147">hello *clientId* hello 포털에서 복사 된 hello 앱으로의 hello 클라이언트 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-147">hello *clientId* is hello client ID of hello app, which you copied from hello portal.</span></span>
4. <span data-ttu-id="e62b5-148">이제 Windows 스토어 앱에 대 한 toodiscover hello 콜백 URI를 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-148">You now need toodiscover hello callback URI for your Windows Store app.</span></span> <span data-ttu-id="e62b5-149">Hello에서이 줄에 중단점을 설정 `MainPage` 메서드:</span><span class="sxs-lookup"><span data-stu-id="e62b5-149">Set a breakpoint on this line in hello `MainPage` method:</span></span>
    ```
    redirectURI = Windows.Security.Authentication.Web.WebAuthenticationBroker.GetCurrentApplicationCallbackUri();
    ```
5. <span data-ttu-id="e62b5-150">모든 패키지 참조는 복원 되었는지 확인 하는 hello 솔루션을 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="e62b5-150">Build hello solution, making sure that all package references are restored.</span></span> <span data-ttu-id="e62b5-151">패키지가 누락 되 면 hello NuGet 패키지 관리자를 열고 복원할 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-151">If any packages are missing, open hello NuGet Package Manager and restore them.</span></span>
6. <span data-ttu-id="e62b5-152">Hello 응용 프로그램을 실행 하 고 hello 값의 복사 `redirectUri` hello 중단점이 적중 될 때입니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-152">Run hello app, and copy hello value of `redirectUri` when hello breakpoint is hit.</span></span> <span data-ttu-id="e62b5-153">hello 값 hello 다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-153">hello value should look something like hello following:</span></span>

    ```
    ms-app://s-1-15-2-1352796503-54529114-405753024-3540103335-3203256200-511895534-1429095407/
    ```

7. <span data-ttu-id="e62b5-154">Hello에 다시 **설정** hello Azure 포털에서에서 hello 앱의 탭 추가 **RedirectUri** 값 앞에 오는 hello로 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-154">Back on hello **Settings** tab of hello app in hello Azure portal, add a **RedirectUri** with hello preceding value.</span></span>  

## <a name="step-3-use-adal-tooget-tokens-from-azure-ad"></a><span data-ttu-id="e62b5-155">3 단계: Azure AD에서 ADAL tooget 토큰 사용</span><span class="sxs-lookup"><span data-stu-id="e62b5-155">Step 3: Use ADAL tooget tokens from Azure AD</span></span>
<span data-ttu-id="e62b5-156">hello ADAL 뒤에 있는 기본 원리는는 hello 앱 액세스 토큰을 필요할 때마다 단순히 호출 `authContext.AcquireToken(…)`, ADAL rest hello는 및입니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-156">hello basic principle behind ADAL is that whenever hello app needs an access token, it simply calls `authContext.AcquireToken(…)`, and ADAL does hello rest.</span></span>  

1. <span data-ttu-id="e62b5-157">Hello 앱 초기화 `AuthenticationContext`, ADAL의 기본 클래스인 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-157">Initialize hello app’s `AuthenticationContext`, which is hello primary class of ADAL.</span></span> <span data-ttu-id="e62b5-158">이 작업을 Azure AD와 toocommunicate 하며 방법 설명 ADAL hello 좌표 전달 toocache 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-158">This action passes ADAL hello coordinates it needs toocommunicate with Azure AD and tell it how toocache tokens.</span></span>

    ```C#
    public MainPage()
    {
        ...

        authContext = new AuthenticationContext(authority);
    }
    ```

2. <span data-ttu-id="e62b5-159">Hello 찾을 `Search(...)` hello를 클릭할 때 호출 되는 메서드를 **검색** hello 응용 프로그램의 UI에서 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-159">Locate hello `Search(...)` method, which is invoked when users click hello **Search** button on hello app's UI.</span></span> <span data-ttu-id="e62b5-160">이 메서드는 해당 UPN 검색 단어를 지정 하는 hello로 시작 하는 사용자에 대 한 get 요청 toohello Azure AD Graph API tooquery를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-160">This method makes a get request toohello Azure AD Graph API tooquery for users whose UPN begins with hello given search term.</span></span> <span data-ttu-id="e62b5-161">tooquery hello Graph API hello 요청에서 액세스 토큰을 포함 **권한 부여** 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-161">tooquery hello Graph API, include an access token in hello request's **Authorization** header.</span></span> <span data-ttu-id="e62b5-162">여기로 ADAL이 들어옵니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-162">This is where ADAL comes in.</span></span>

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
                ShowAuthError(string.Format("If hello error continues, please contact your administrator.\n\nError: {0}\n\nError Description:\n\n{1}", ex.ErrorCode, ex.Message));
            }
            return;
        }
        ...
    }
    ```
    <span data-ttu-id="e62b5-163">호출 하 여 hello 앱 토큰을 요청할 때 `AcquireTokenAsync(...)`, ADAL hello 사용자 자격 증명을 요청 하지 않고 tooreturn 토큰을 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-163">When hello app requests a token by calling `AcquireTokenAsync(...)`, ADAL attempts tooreturn a token without asking hello user for credentials.</span></span> <span data-ttu-id="e62b5-164">ADAL 해당 hello 사용자에 게 toosign tooget 토큰에에서 필요한 데이터를 결정 하는 경우 로그인 대화 상자를 표시, hello 사용자의 자격 증명을 수집 하 고 인증에 성공한 후 토큰을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-164">If ADAL determines that hello user needs toosign in tooget a token, it displays a sign-in dialog box, collects hello user's credentials, and returns a token after authentication succeeds.</span></span> <span data-ttu-id="e62b5-165">ADAL 어떤 이유로 든 없습니다 tooreturn 토큰 이면 hello *AuthenticationResult* 상태는 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-165">If ADAL is unable tooreturn a token for any reason, hello *AuthenticationResult* status is an error.</span></span>
3. <span data-ttu-id="e62b5-166">이제 방금 확보 하는 시간 toouse hello 액세스 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-166">Now it's time toouse hello access token you just acquired.</span></span> <span data-ttu-id="e62b5-167">Hello에도 `Search(...)` 메서드를 get 요청을 hello에서 Graph API hello 토큰 toohello 연결 **권한 부여** 헤더:</span><span class="sxs-lookup"><span data-stu-id="e62b5-167">Also in hello `Search(...)` method, attach hello token toohello Graph API get request in hello **Authorization** header:</span></span>

    ```C#
    // Add hello access token toohello Authorization header of hello call toohello Graph API, and call hello Graph API.
    httpClient.DefaultRequestHeaders.Authorization = new HttpCredentialsHeaderValue("Bearer", result.AccessToken);

    ```
4. <span data-ttu-id="e62b5-168">Hello를 사용할 수 있습니다 `AuthenticationResult` 개체 hello 사용자의 ID와 같은 hello 응용 프로그램에서 사용자 hello에 대 한 toodisplay 정보:</span><span class="sxs-lookup"><span data-stu-id="e62b5-168">You can use hello `AuthenticationResult` object toodisplay information about hello user in hello app, such as hello user's ID:</span></span>

    ```C#
    // Update hello page UI toorepresent hello signed-in user
    ActiveUser.Text = result.UserInfo.DisplayableId;
    ```
5. <span data-ttu-id="e62b5-169">Hello 앱에서 ADAL toosign 사용자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-169">You can also use ADAL toosign users out of hello app.</span></span> <span data-ttu-id="e62b5-170">Hello을 클릭할 때 hello **로그 아웃** 단추, 너무 hello 다음 호출 하는 확인`AcquireTokenAsync(...)` 로그인 뷰를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-170">When hello user clicks hello **Sign Out** button, ensure that hello next call too`AcquireTokenAsync(...)` shows a sign-in view.</span></span> <span data-ttu-id="e62b5-171">ADAL이이 작업 hello 토큰 캐시를 지우는 것 처럼 쉽게 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-171">With ADAL, this action is as easy as clearing hello token cache:</span></span>

    ```C#
    private void SignOut()
    {
        // Clear session state from hello token cache.
        authContext.TokenCache.Clear();

        ...
    }
    ```

## <a name="whats-next"></a><span data-ttu-id="e62b5-172">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e62b5-172">What's next</span></span>
<span data-ttu-id="e62b5-173">이제 작업 중인 Windows 스토어 앱이 사용자를 인증, 안전 하 게 웹 OAuth 2.0을 사용 하 여 Api를 호출 하 고 수 있는 hello 사용자에 대 한 기본 정보를 가져올 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-173">You now have a working Windows Store app that can authenticate users, securely call web APIs using OAuth 2.0, and get basic information about hello user.</span></span>

<span data-ttu-id="e62b5-174">사용자와 테 넌 트 채워진 이미 하지 않은 경우 지금은 hello 시간 toodo 이므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-174">If you haven’t already populated your tenant with users, now is hello time toodo so.</span></span>
1. <span data-ttu-id="e62b5-175">DirectorySearcher 응용 프로그램을 실행 하 고 hello 사용자 중 하나를 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-175">Run your DirectorySearcher app, and then sign in with one of hello users.</span></span>
2. <span data-ttu-id="e62b5-176">해당 UPN에 따라 다른 사용자를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-176">Search for other users based on their UPN.</span></span>
3. <span data-ttu-id="e62b5-177">Hello 응용 프로그램을 닫고 다시 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-177">Close hello app, and rerun it.</span></span> <span data-ttu-id="e62b5-178">Hello 사용자의 세션 그대로 유지 방법을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-178">Notice how hello user’s session remains intact.</span></span>
4. <span data-ttu-id="e62b5-179">Toodisplay hello 아래쪽 표시줄을 마우스 오른쪽 단추로 클릭 하 여 로그 아웃 한 다음 다른 사용자로 다시 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-179">Sign out by right-clicking toodisplay hello bottom bar, and then sign back in as another user.</span></span>

<span data-ttu-id="e62b5-180">ADAL 쉽게 tooincorporate를 사용 하면 이러한 일반적인 모든 id 기능 hello 응용 프로그램에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-180">ADAL makes it easy tooincorporate all these common identity features into hello app.</span></span> <span data-ttu-id="e62b5-181">관리의 모든 hello dirty 작업, 캐시 관리와 같은 OAuth 프로토콜 지원 등 hello 사용자 로그인 UI 제시 하 고 토큰 만료를 새로 고치 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-181">It takes care of all hello dirty work for you, such as cache management, OAuth protocol support, presenting hello user with a login UI, and refreshing expired tokens.</span></span> <span data-ttu-id="e62b5-182">Tooknow 단일 API 호출 해야 `authContext.AcquireToken*(…)`합니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-182">You need tooknow only a single API call, `authContext.AcquireToken*(…)`.</span></span>

<span data-ttu-id="e62b5-183">참조용으로 hello 다운로드 [완성 된 샘플](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip) (없이 구성 값).</span><span class="sxs-lookup"><span data-stu-id="e62b5-183">For reference, download hello [completed sample](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip) (without your configuration values).</span></span>

<span data-ttu-id="e62b5-184">이제 tooadditional id 시나리오에서 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e62b5-184">You can now move on tooadditional identity scenarios.</span></span> <span data-ttu-id="e62b5-185">예를 들어 [Azure AD를 사용하여 .NET Web API 보안 유지](active-directory-devquickstarts-webapi-dotnet.md)를 시도해 보세요.</span><span class="sxs-lookup"><span data-stu-id="e62b5-185">For example, try [Secure a .NET Web API with Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

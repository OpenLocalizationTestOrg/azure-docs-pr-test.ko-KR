---
title: "aaaAzure AD Xamarin 시작 | Microsoft Docs"
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
ms.openlocfilehash: 6a0d189648b7071558ac1cf2b908808668960a4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-xamarin-apps"></a><span data-ttu-id="24fc5-103">Xamarin 앱에 Azure AD 통합</span><span class="sxs-lookup"><span data-stu-id="24fc5-103">Integrate Azure AD with Xamarin apps</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="24fc5-104">Xamarin을 사용하면 iOS, Android 및 Windows(모바일 장치 및 PC)에서 실행할 수 있는 Mobile Apps를 C#으로 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24fc5-104">With Xamarin, you can write mobile apps in C# that can run on iOS, Android, and Windows (mobile devices and PCs).</span></span> <span data-ttu-id="24fc5-105">Xamarin을 사용 하는 응용 프로그램을 빌드하는 경우 Azure Active Directory (Azure AD)는 Azure AD 계정 가진 단순 tooauthenticate 사용자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24fc5-105">If you're building an app using Xamarin, Azure Active Directory (Azure AD) makes it simple tooauthenticate users with their Azure AD accounts.</span></span> <span data-ttu-id="24fc5-106">hello 앱 Office 365 Api hello 또는 hello Azure API와 같은 Azure AD로 보호 되는 모든 웹 API를 사용할 안전 하 게 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24fc5-106">hello app can also securely consume any web API that's protected by Azure AD, such as hello Office 365 APIs or hello Azure API.</span></span>

<span data-ttu-id="24fc5-107">Azure AD tooaccess 보호 된 리소스를 필요로 하는 Xamarin 앱에 대 한 Active Directory 인증 라이브러리 (ADAL) hello를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="24fc5-107">For Xamarin apps that need tooaccess protected resources, Azure AD provides hello Active Directory Authentication Library (ADAL).</span></span> <span data-ttu-id="24fc5-108">hello ADAL의 목적으로 toomake 앱 tooget 액세스 토큰을 쉽게 합니다.</span><span class="sxs-lookup"><span data-stu-id="24fc5-108">hello sole purpose of ADAL is toomake it easy for apps tooget access tokens.</span></span> <span data-ttu-id="24fc5-109">이 문서에서는 얼마나 쉬운지 toodemonstrate 방법을 toobuild DirectorySearcher 앱 있는:</span><span class="sxs-lookup"><span data-stu-id="24fc5-109">toodemonstrate how easy it is, this article shows how toobuild DirectorySearcher apps that:</span></span>

* <span data-ttu-id="24fc5-110">iOS, Android, Windows 데스크톱, Windows Phone 및 Windows 스토어에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="24fc5-110">Run on iOS, Android, Windows Desktop, Windows Phone, and Windows Store.</span></span>
* <span data-ttu-id="24fc5-111">단일 이식 가능한 클래스 라이브러리 (PCL) tooauthenticate 사용자가 사용 하 고 hello Azure AD Graph API에 대 한 토큰을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="24fc5-111">Use a single portable class library (PCL) tooauthenticate users and get tokens for hello Azure AD Graph API.</span></span>
* <span data-ttu-id="24fc5-112">지정된 UPN을 가진 사용자를 디렉터리에서 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="24fc5-112">Search a directory for users with a given UPN.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="24fc5-113">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="24fc5-113">Before you get started</span></span>
* <span data-ttu-id="24fc5-114">Hello 다운로드 [기초 프로젝트](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/skeleton.zip), hello 다운로드 또는 [완성 된 샘플](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip)합니다.</span><span class="sxs-lookup"><span data-stu-id="24fc5-114">Download hello [skeleton project](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/skeleton.zip), or download hello [completed sample](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="24fc5-115">각 다운로드는 Visual Studio 2013 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="24fc5-115">Each download is a Visual Studio 2013 solution.</span></span>
* <span data-ttu-id="24fc5-116">Toocreate 사용자 및 레지스터 hello 앱에서 Azure AD 테 넌 트가 있어야합니다.</span><span class="sxs-lookup"><span data-stu-id="24fc5-116">You also need an Azure AD tenant in which toocreate users and register hello app.</span></span> <span data-ttu-id="24fc5-117">테 넌 트 아직 없는 경우 [자세한 방법을 하나 tooget](active-directory-howto-tenant.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="24fc5-117">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="24fc5-118">준비 되 면 다음 절차에 따라 hello hello 다음 네 개의 절.</span><span class="sxs-lookup"><span data-stu-id="24fc5-118">When you are ready, follow hello procedures in hello next four sections.</span></span>

## <a name="step-1-set-up-your-xamarin-development-environment"></a><span data-ttu-id="24fc5-119">1단계: Xamarin 개발 환경 설정</span><span class="sxs-lookup"><span data-stu-id="24fc5-119">Step 1: Set up your Xamarin development environment</span></span>
<span data-ttu-id="24fc5-120">이 자습서에는 iOS, Android 및 Windows용 프로젝트가 포함되어 있으므로 Visual Studio와 Xamarin이 둘 다 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="24fc5-120">Because this tutorial includes projects for iOS, Android, and Windows, you need both Visual Studio and Xamarin.</span></span> <span data-ttu-id="24fc5-121">toocreate hello 필요한 환경에서 전체 hello 프로세스 [설정 및 Visual Studio 및 Xamarin이 설치](https://msdn.microsoft.com/library/mt613162.aspx) msdn 합니다.</span><span class="sxs-lookup"><span data-stu-id="24fc5-121">toocreate hello necessary environment, complete hello process in [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) on MSDN.</span></span> <span data-ttu-id="24fc5-122">hello 지침 hello 설치 toobe 완료를 기다리는 동안 Xamarin에 대 한 자세한 toolearn를 검토할 수 있는 자료를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="24fc5-122">hello instructions include material that you can review toolearn more about Xamarin while you're waiting for hello installations toobe completed.</span></span>

<span data-ttu-id="24fc5-123">Hello 설치를 완료 한 후 Visual Studio에서 hello 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="24fc5-123">After you've completed hello setup, open hello solution in Visual Studio.</span></span> <span data-ttu-id="24fc5-124">그러면 5개의 플랫폼별 프로젝트와 모든 플랫폼에서 공유되는 1개의 PCL, DirectorySearcher.cs의 6개 프로젝트를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24fc5-124">There, you will find six projects: five platform-specific projects and one PCL, DirectorySearcher.cs, which will be shared across all platforms.</span></span>

## <a name="step-2-register-hello-directorysearcher-app"></a><span data-ttu-id="24fc5-125">2 단계: hello DirectorySearcher 앱 등록</span><span class="sxs-lookup"><span data-stu-id="24fc5-125">Step 2: Register hello DirectorySearcher app</span></span>
<span data-ttu-id="24fc5-126">tooenable hello 앱 tooget 토큰 먼저 tooregister에서 Azure AD 테 넌 트 및 사용 권한 tooaccess hello Azure AD Graph API에 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="24fc5-126">tooenable hello app tooget tokens, you first need tooregister it in your Azure AD tenant and grant it permission tooaccess hello Azure AD Graph API.</span></span> <span data-ttu-id="24fc5-127">방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="24fc5-127">Here's how:</span></span>

1. <span data-ttu-id="24fc5-128">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="24fc5-128">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="24fc5-129">Hello 위쪽 막대에서 계정을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="24fc5-129">On hello top bar, click your account.</span></span> <span data-ttu-id="24fc5-130">그런 다음 hello **디렉터리** 목록, 선택 hello Active Directory 테 넌 트 tooregister hello 앱을 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="24fc5-130">Then, under hello **Directory** list, select hello Active Directory tenant where you want tooregister hello app.</span></span>
3. <span data-ttu-id="24fc5-131">클릭 **더 서비스** 에 hello 왼쪽된 창에서 선택한 후 **Azure Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="24fc5-131">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="24fc5-132">**앱 등록**을 클릭하고 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="24fc5-132">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="24fc5-133">새 toocreate **네이티브 클라이언트 응용 프로그램**, hello 프롬프트를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="24fc5-133">toocreate a new **Native Client Application**, follow hello prompts.</span></span>
  * <span data-ttu-id="24fc5-134">**이름** hello 앱 toousers에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="24fc5-134">**Name** describes hello app toousers.</span></span>
  * <span data-ttu-id="24fc5-135">**리디렉션 URI** Azure AD에서는 tooreturn 토큰 응답 체계 및 문자열 조합입니다.</span><span class="sxs-lookup"><span data-stu-id="24fc5-135">**Redirect URI** is a scheme and string combination that Azure AD uses tooreturn token responses.</span></span> <span data-ttu-id="24fc5-136">값(예:  http://DirectorySearcher )을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="24fc5-136">Enter a value (for example, http://DirectorySearcher).</span></span>
6. <span data-ttu-id="24fc5-137">Azure AD를 등록을 완료 한 후 hello 앱 고유한 응용 프로그램 ID를 할당</span><span class="sxs-lookup"><span data-stu-id="24fc5-137">After you’ve completed registration, Azure AD assigns hello app a unique application ID.</span></span> <span data-ttu-id="24fc5-138">Hello에서 hello 값 복사 **응용 프로그램** 탭, 나중에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="24fc5-138">Copy hello value from hello **Application** tab, because you'll need it later.</span></span>
7. <span data-ttu-id="24fc5-139">Hello에 **설정** 페이지에서 **필요한 권한**를 선택한 후 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="24fc5-139">On hello **Settings** page, select **Required Permissions**, and then select **Add**.</span></span>
8. <span data-ttu-id="24fc5-140">선택 **Microsoft Graph** API hello으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="24fc5-140">Select **Microsoft Graph** as hello API.</span></span> <span data-ttu-id="24fc5-141">아래 **위임 된 권한**, hello 추가 **디렉터리 데이터 읽기** 권한.</span><span class="sxs-lookup"><span data-stu-id="24fc5-141">Under **Delegated Permissions**, add hello **Read Directory Data** permission.</span></span>  
<span data-ttu-id="24fc5-142">그러면 사용자에 대 한 hello 앱 tooquery hello Graph API 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24fc5-142">This action enables hello app tooquery hello Graph API for users.</span></span>

## <a name="step-3-install-and-configure-adal"></a><span data-ttu-id="24fc5-143">3단계: ADAL 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="24fc5-143">Step 3: Install and configure ADAL</span></span>
<span data-ttu-id="24fc5-144">Azure AD에 앱이 있으므로 ADAL을 설치하고 ID 관련 코드를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24fc5-144">Now that you have an app in Azure AD, you can install ADAL and write your identity-related code.</span></span> <span data-ttu-id="24fc5-145">Azure AD와 tooenable ADAL toocommunicate hello 앱 등록에 대 한 정보를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="24fc5-145">tooenable ADAL toocommunicate with Azure AD, give it some information about hello app registration.</span></span>

1. <span data-ttu-id="24fc5-146">Hello 패키지 관리자 콘솔을 사용 하 여 ADAL toohello DirectorySearcher 프로젝트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="24fc5-146">Add ADAL toohello DirectorySearcher project by using hello Package Manager Console.</span></span>

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

    <span data-ttu-id="24fc5-147">두 개의 라이브러리 참조 tooeach 프로젝트를 추가 하는 참고: hello PCL 부분의 ADAL와 플랫폼별 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="24fc5-147">Note that two library references are added tooeach project: hello PCL portion of ADAL and a platform-specific portion.</span></span>
2. <span data-ttu-id="24fc5-148">Hello DirectorySearcherLib 프로젝트에서 DirectorySearcher.cs를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="24fc5-148">In hello DirectorySearcherLib project, open DirectorySearcher.cs.</span></span>
3. <span data-ttu-id="24fc5-149">Hello Azure 포털에에서 입력 된 hello hello 클래스 멤버 값을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="24fc5-149">Replace hello class member values with hello values that you entered in hello Azure portal.</span></span> <span data-ttu-id="24fc5-150">ADAL를 사용 하 여 때마다 코드 toothese 값을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="24fc5-150">Your code refers toothese values whenever it uses ADAL.</span></span>

  * <span data-ttu-id="24fc5-151">hello *테 넌 트* 여 Azure AD 테 넌 트 (예: contoso.onmicrosoft.com) hello 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="24fc5-151">hello *tenant* is hello domain of your Azure AD tenant (for example, contoso.onmicrosoft.com).</span></span>
  * <span data-ttu-id="24fc5-152">hello *clientId* hello 포털에서 복사 된 hello 앱으로의 hello 클라이언트 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="24fc5-152">hello *clientId* is hello client ID of hello app, which you copied from hello portal.</span></span>
  * <span data-ttu-id="24fc5-153">hello *returnUri* 값 hello 리디렉션 URI (예를 들어 http://DirectorySearcher) hello 포털에 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="24fc5-153">hello *returnUri* is hello redirect URI that you entered in hello portal (for example, http://DirectorySearcher).</span></span>

## <a name="step-4-use-adal-tooget-tokens-from-azure-ad"></a><span data-ttu-id="24fc5-154">4 단계: Azure AD에서 ADAL tooget 토큰 사용</span><span class="sxs-lookup"><span data-stu-id="24fc5-154">Step 4: Use ADAL tooget tokens from Azure AD</span></span>
<span data-ttu-id="24fc5-155">있는 모든 hello 앱의 인증 논리를 거의 `DirectorySearcher.SearchByAlias(...)`합니다.</span><span class="sxs-lookup"><span data-stu-id="24fc5-155">Almost all of hello app's authentication logic lies in `DirectorySearcher.SearchByAlias(...)`.</span></span> <span data-ttu-id="24fc5-156">Hello 플랫폼별 프로젝트에 반드시 필요한 것은 컨텍스트 매개 변수에 toohello toopass `DirectorySearcher` PCL입니다.</span><span class="sxs-lookup"><span data-stu-id="24fc5-156">All that's necessary in hello platform-specific projects is toopass a contextual parameter toohello `DirectorySearcher` PCL.</span></span>

1. <span data-ttu-id="24fc5-157">DirectorySearcher.cs를 연 다음 새 매개 변수 toohello 추가 `SearchByAlias(...)` 메서드.</span><span class="sxs-lookup"><span data-stu-id="24fc5-157">Open DirectorySearcher.cs, and then add a new parameter toohello `SearchByAlias(...)` method.</span></span> <span data-ttu-id="24fc5-158">`IPlatformParameters`hello 플랫폼별 캡슐화 hello 컨텍스트 매개 변수는 ADAL 요구 tooperform hello 인증 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="24fc5-158">`IPlatformParameters` is hello contextual parameter that encapsulates hello platform-specific objects that ADAL needs tooperform hello authentication.</span></span>

    ```C#
    public static async Task<List<User>> SearchByAlias(string alias, IPlatformParameters parent)
    {
    ```

2. <span data-ttu-id="24fc5-159">초기화 `AuthenticationContext`, ADAL의 기본 클래스인 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="24fc5-159">Initialize `AuthenticationContext`, which is hello primary class of ADAL.</span></span>  
<span data-ttu-id="24fc5-160">이 작업 단계 ADAL hello 조정 요구 toocommunicate Azure AD와 것입니다.</span><span class="sxs-lookup"><span data-stu-id="24fc5-160">This action passes ADAL hello coordinates it needs toocommunicate with Azure AD.</span></span>
3. <span data-ttu-id="24fc5-161">호출 `AcquireTokenAsync(...)`, hello를 허용 하는 `IPlatformParameters` 개체 하 고 hello 인증 흐름은 필요한 tooreturn 토큰 toohello 응용 프로그램을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="24fc5-161">Call `AcquireTokenAsync(...)`, which accepts hello `IPlatformParameters` object and invokes hello authentication flow that's necessary tooreturn a token toohello app.</span></span>

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

    <span data-ttu-id="24fc5-162">`AcquireTokenAsync(...)`사용자가 tooenter 캐싱 또는 오래 된 토큰 새로 고침) (통해 자격 증명을 확인 하지 않고 리소스 (이 경우 Graph API hello)를 요청 하는 첫 번째 시도 tooreturn hello에 대 한 토큰.</span><span class="sxs-lookup"><span data-stu-id="24fc5-162">`AcquireTokenAsync(...)` first attempts tooreturn a token for hello requested resource (hello Graph API in this case) without prompting users tooenter their credentials (via caching or refreshing old tokens).</span></span> <span data-ttu-id="24fc5-163">필요에 따라 hello 요청한 토큰을 획득 하기 전에 사용자가 hello Azure AD 로그인 페이지를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="24fc5-163">As necessary, it shows users hello Azure AD sign-in page before acquiring hello requested token.</span></span>
4. <span data-ttu-id="24fc5-164">연결 hello hello에 대 한 액세스 토큰 toohello Graph API 요청 **권한 부여** 헤더:</span><span class="sxs-lookup"><span data-stu-id="24fc5-164">Attach hello access token toohello Graph API request in hello **Authorization** header:</span></span>

    ```C#
    ...
        request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", authResult.AccessToken);
    ...
    ```

<span data-ttu-id="24fc5-165">그 hello에 대 한 `DirectorySearcher` PCL 및 hello 응용 프로그램의 id 관련 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="24fc5-165">That's all for hello `DirectorySearcher` PCL and hello app's identity-related code.</span></span> <span data-ttu-id="24fc5-166">이제 남은 것 toocall hello `SearchByAlias(...)` 각 플랫폼의 보기에서 메서드 및 tooadd 코드 올바르게 처리 하기 위한 UI 수명 주기 hello 필요한 경우.</span><span class="sxs-lookup"><span data-stu-id="24fc5-166">All that remains is toocall hello `SearchByAlias(...)` method in each platform's views and, where necessary, tooadd code for correctly handling hello UI lifecycle.</span></span>

### <a name="android"></a><span data-ttu-id="24fc5-167">Android</span><span class="sxs-lookup"><span data-stu-id="24fc5-167">Android</span></span>
1. <span data-ttu-id="24fc5-168">MainActivity.cs에 대 한 호출을 너무 추가`SearchByAlias(...)` hello 단추 클릭 처리기:</span><span class="sxs-lookup"><span data-stu-id="24fc5-168">In MainActivity.cs, add a call too`SearchByAlias(...)` in hello button click handler:</span></span>

    ```C#
    List<User> results = await DirectorySearcher.SearchByAlias(searchTermText.Text, new PlatformParameters(this));
    ```
2. <span data-ttu-id="24fc5-169">Hello 재정의 `OnActivityResult` 수명 주기 메서드 tooforward 인증 백 toohello 적절 한 방법을 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="24fc5-169">Override hello `OnActivityResult` lifecycle method tooforward any authentication redirects back toohello appropriate method.</span></span> <span data-ttu-id="24fc5-170">ADAL은 Android에서 이 작업을 위한 도우미 메서드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="24fc5-170">ADAL provides a helper method for this in Android:</span></span>

    ```C#
    ...
    protected override void OnActivityResult(int requestCode, Result resultCode, Intent data)
    {
        base.OnActivityResult(requestCode, resultCode, data);
        AuthenticationAgentContinuationHelper.SetAuthenticationAgentContinuationEventArgs(requestCode, resultCode, data);
    }
    ...
    ```

### <a name="windows-desktop"></a><span data-ttu-id="24fc5-171">Windows Desktop</span><span class="sxs-lookup"><span data-stu-id="24fc5-171">Windows Desktop</span></span>
<span data-ttu-id="24fc5-172">MainWindow.xaml.cs를에 대 한 호출을 너무 확인`SearchByAlias(...)` 전달 하 여 한 `WindowInteropHelper` hello 데스크톱에서 `PlatformParameters` 개체:</span><span class="sxs-lookup"><span data-stu-id="24fc5-172">In MainWindow.xaml.cs, make a call too`SearchByAlias(...)` by passing a `WindowInteropHelper` in hello desktop's `PlatformParameters` object:</span></span>

```C#
List<User> results = await DirectorySearcher.SearchByAlias(
  SearchTermText.Text,
  new PlatformParameters(PromptBehavior.Auto, this.Handle));
```

#### <a name="ios"></a><span data-ttu-id="24fc5-173">iOS</span><span class="sxs-lookup"><span data-stu-id="24fc5-173">iOS</span></span>
<span data-ttu-id="24fc5-174">DirSearchClient_iOSViewController.cs에서 iOS hello `PlatformParameters` 개체는 참조 toohello 뷰-컨트롤러:</span><span class="sxs-lookup"><span data-stu-id="24fc5-174">In DirSearchClient_iOSViewController.cs, hello iOS `PlatformParameters` object takes a reference toohello View Controller:</span></span>

```C#
List<User> results = await DirectorySearcher.SearchByAlias(
  SearchTermText.Text,
  new PlatformParameters(PromptBehavior.Auto, this.Handle));
```

### <a name="windows-universal"></a><span data-ttu-id="24fc5-175">Windows 범용</span><span class="sxs-lookup"><span data-stu-id="24fc5-175">Windows Universal</span></span>
<span data-ttu-id="24fc5-176">Windows 유니버설에서 MainPage.xaml.cs를 연 다음 hello 구현 `Search` 메서드.</span><span class="sxs-lookup"><span data-stu-id="24fc5-176">In Windows Universal, open MainPage.xaml.cs, and then implement hello `Search` method.</span></span> <span data-ttu-id="24fc5-177">이 메서드는 필요에 따라 공유 프로젝트 tooupdate UI에에서는 도우미 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="24fc5-177">This method uses a helper method in a shared project tooupdate UI as necessary.</span></span>

```C#
...
List<User> results = await DirectorySearcherLib.DirectorySearcher.SearchByAlias(SearchTermText.Text, new PlatformParameters(PromptBehavior.Auto, false));
...
```

## <a name="whats-next"></a><span data-ttu-id="24fc5-178">다음 단계</span><span class="sxs-lookup"><span data-stu-id="24fc5-178">What's next</span></span>
<span data-ttu-id="24fc5-179">이제 5개의 서로 다른 플랫폼에서 OAuth 2.0을 사용하여 사용자를 인증하고 안전하게 Web API를 호출할 수 있는 Xamarin 앱이 작성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="24fc5-179">You now have a working Xamarin app that can authenticate users and securely call web APIs by using OAuth 2.0 across five different platforms.</span></span>

<span data-ttu-id="24fc5-180">사용자와 테 넌 트 채워진 이미 하지 않은 경우 지금은 hello 시간 toodo 이므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="24fc5-180">If you haven’t already populated your tenant with users, now is hello time toodo so.</span></span>

1. <span data-ttu-id="24fc5-181">DirectorySearcher 응용 프로그램을 실행 하 고 hello 사용자 중 하나를 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="24fc5-181">Run your DirectorySearcher app, and then sign in with one of hello users.</span></span>
2. <span data-ttu-id="24fc5-182">해당 UPN에 따라 다른 사용자를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="24fc5-182">Search for other users based on their UPN.</span></span>

<span data-ttu-id="24fc5-183">ADAL은 hello 응용 프로그램에 쉽게 tooincorporate 일반적인 id 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24fc5-183">ADAL makes it easy tooincorporate common identity features into hello app.</span></span> <span data-ttu-id="24fc5-184">관리의 모든 hello dirty 작업, 캐시 관리와 같은 OAuth 프로토콜 지원 등 hello 사용자 로그인 UI 제시 하 고 토큰 만료를 새로 고치 합니다.</span><span class="sxs-lookup"><span data-stu-id="24fc5-184">It takes care of all hello dirty work for you, such as cache management, OAuth protocol support, presenting hello user with a login UI, and refreshing expired tokens.</span></span> <span data-ttu-id="24fc5-185">Tooknow 단일 API 호출 해야 `authContext.AcquireToken*(…)`합니다.</span><span class="sxs-lookup"><span data-stu-id="24fc5-185">You need tooknow only a single API call, `authContext.AcquireToken*(…)`.</span></span>

<span data-ttu-id="24fc5-186">참조용으로 hello 다운로드 [완성 된 샘플](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip) (없이 구성 값).</span><span class="sxs-lookup"><span data-stu-id="24fc5-186">For reference, download hello [completed sample](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip) (without your configuration values).</span></span>

<span data-ttu-id="24fc5-187">이제 tooadditional id 시나리오에서 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24fc5-187">You can now move on tooadditional identity scenarios.</span></span> <span data-ttu-id="24fc5-188">예를 들어 [Azure AD를 사용하여 .NET Web API 보안 유지](active-directory-devquickstarts-webapi-dotnet.md)를 시도해 보세요.</span><span class="sxs-lookup"><span data-stu-id="24fc5-188">For example, try [Secure a .NET Web API with Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

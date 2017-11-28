---
title: "iOS 앱에 Azure AD aaaIntegrate | Microsoft Docs"
description: "어떻게 toobuild 로그인 및 Azure AD 호출에 대 한 Azure AD와 통합 하는 iOS 응용 프로그램 OAuth를 사용 하 여 Api를 보호 합니다."
services: active-directory
documentationcenter: ios
author: brandwe
manager: mbaldwin
editor: 
ms.assetid: 42303177-9566-48ed-8abb-279fcf1e6ddb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 01/07/2017
ms.author: brandwe
ms.custom: aaddev
ms.openlocfilehash: 6e05745b2b2b122995dcba896ab0f2ed32509e3a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-into-an-ios-app"></a><span data-ttu-id="98e7a-103">iOS 앱에 Azure AD 통합</span><span class="sxs-lookup"><span data-stu-id="98e7a-103">Integrate Azure AD into an iOS app</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

> [!TIP]
> <span data-ttu-id="98e7a-104">이 새로운 hello 미리 보기를 사용 [개발자 포털](https://identity.microsoft.com/Docs/iOS) 에서는 통해 몇 분만에 Azure Active Directory 실행 되 고 시작!</span><span class="sxs-lookup"><span data-stu-id="98e7a-104">Try hello preview of our new [developer portal](https://identity.microsoft.com/Docs/iOS) that helps you get up and running with Azure Active Directory in just a few minutes!</span></span>  <span data-ttu-id="98e7a-105">hello 개발자 포털 앱을 등록 하 고 코드에 Azure AD 통합의 hello 과정을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-105">hello developer portal guides you through hello process of registering an app and integrating Azure AD into your code.</span></span>  <span data-ttu-id="98e7a-106">이 과정을 완료하면 테넌트에서 사용자를 인증할 수 있는 간단한 응용 프로그램 및 토큰을 수락하고 유효성 검사를 수행할 수 있는 백 엔드가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-106">When you’re finished, you'll have a simple application that can authenticate users in your tenant and a backend that can accept tokens and perform validation.</span></span> 
> 
> 

<span data-ttu-id="98e7a-107">Azure Active Directory (Azure AD) tooaccess를 필요로 하는 iOS 클라이언트 보호 되는 리소스에 대 한 hello ADAL, 또는 Active Directory 인증 라이브러리를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-107">Azure Active Directory (Azure AD) provides hello Active Directory Authentication Library, or ADAL, for iOS clients that need tooaccess protected resources.</span></span> <span data-ttu-id="98e7a-108">ADAL 앱 tooobtain 액세스 토큰을 사용 하는 hello 프로세스를 단순화 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-108">ADAL simplifies hello process that your app uses tooobtain access tokens.</span></span> <span data-ttu-id="98e7a-109">toodemonstrate 얼마나 쉬운지이 문서에는 우리가 구축 Objective C 할 일 목록 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-109">toodemonstrate how easy it is, in this article we build an Objective C To-Do List application that:</span></span>

* <span data-ttu-id="98e7a-110">가져옵니다 액세스 hello를 사용 하 여 hello Azure AD Graph API를 호출 하기 위한 토큰 [OAuth 2.0 인증 프로토콜](https://msdn.microsoft.com/library/azure/dn645545.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-110">Gets access tokens for calling hello Azure AD Graph API by using hello [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="98e7a-111">지정된 별칭을 가진 사용자를 디렉터리에서 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-111">Searches a directory for users with a given alias.</span></span>

<span data-ttu-id="98e7a-112">해야 toobuild hello 전체 응용 프로그램을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-112">toobuild hello complete working application, you need to:</span></span>

1. <span data-ttu-id="98e7a-113">Azure AD에 응용 프로그램을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-113">Register your application with Azure AD.</span></span>
2. <span data-ttu-id="98e7a-114">ADAL을 설치 및 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-114">Install and configure ADAL.</span></span>
3. <span data-ttu-id="98e7a-115">Azure AD에서 ADAL tooget 토큰을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-115">Use ADAL tooget tokens from Azure AD.</span></span>

<span data-ttu-id="98e7a-116">시작 tooget [hello 응용 프로그램의 기본 정의 다운로드](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/skeleton.zip) 또는 [완료 hello 샘플 다운로드](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip)합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-116">tooget started, [download hello app skeleton](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/skeleton.zip) or [download hello completed sample](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span></span> <span data-ttu-id="98e7a-117">또한 사용자를 만들고 응용 프로그램을 등록할 수 있는 Azure AD 테넌트도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-117">You also need an Azure AD tenant in which you can create users and register an application.</span></span> <span data-ttu-id="98e7a-118">테 넌 트 아직 없는 경우 [자세한 방법을 하나 tooget](active-directory-howto-tenant.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-118">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>


> [!TIP]
> <span data-ttu-id="98e7a-119">이 새로운 hello 미리 보기를 사용 [개발자 포털](https://identity.microsoft.com/Docs/iOS) 에서는 단 몇 분 후에 Azure AD와 시작 및 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-119">Try hello preview of our new [developer portal](https://identity.microsoft.com/Docs/iOS) that helps you get up and running with Azure AD in just a few minutes.</span></span> <span data-ttu-id="98e7a-120">hello 개발자 포털 앱을 등록 하 고 코드에 Azure AD 통합의 hello 과정을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-120">hello developer portal guides you through hello process of registering an app and integrating Azure AD into your code.</span></span> <span data-ttu-id="98e7a-121">이 과정을 완료하면 테넌트에서 사용자를 인증할 수 있는 간단한 응용 프로그램 및 토큰을 수락하고 유효성 검사를 수행할 수 있는 백 엔드가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-121">When you’re finished, you'll have a simple application that can authenticate users in your tenant, and a back end that can accept tokens and perform validation.</span></span> 
> 
> 

## <a name="1-determine-what-your-redirect-uri-is-for-ios"></a><span data-ttu-id="98e7a-122">1. iOS에 대한 리디렉션 URI 결정</span><span class="sxs-lookup"><span data-stu-id="98e7a-122">1. Determine what your redirect URI is for iOS</span></span>
<span data-ttu-id="98e7a-123">toosecurely 특정 SSO 시나리오에서 응용 프로그램을 시작, 만들어야는 *리디렉션 URI* 를 특정 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-123">toosecurely start your applications in certain SSO scenarios, you must create a *redirect URI* in a particular format.</span></span> <span data-ttu-id="98e7a-124">리디렉션 URI는 토큰 반환 toohello 올바른 응용 프로그램을 요청 하는 hello 사용된 tooensure입니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-124">A redirect URI is used tooensure that hello tokens return toohello correct application that asked for them.</span></span>


<span data-ttu-id="98e7a-125">hello iOS 리디렉션 URI 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-125">hello iOS format for a redirect URI is:</span></span>

```
<app-scheme>://<bundle-id>
```

* <span data-ttu-id="98e7a-126">**app-scheme** - XCode 프로젝트에 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-126">**app-scheme** - This is registered in your XCode project.</span></span> <span data-ttu-id="98e7a-127">다른 응용 프로그램이 사용자를 호출할 수 있는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-127">It is how other applications can call you.</span></span> <span data-ttu-id="98e7a-128">Info.plist -> URL 형식 -> URL ID에 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-128">You can find this under Info.plist -> URL types -> URL Identifier.</span></span> <span data-ttu-id="98e7a-129">하나 이상이 구성되어 있지 않으면 하나를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-129">You should create one if you don't already have one or more configured.</span></span>
* <span data-ttu-id="98e7a-130">**번들 id** -이 hello 번들 식별자 "identity" 아래 취소 XCode에서 프로젝트 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-130">**bundle-id** - This is hello Bundle Identifier found under "identity" un your project settings in XCode.</span></span>

<span data-ttu-id="98e7a-131">이 빠른 시작 코드는 ***msquickstart://com.microsoft.azureactivedirectory.samples.graph.QuickStart***를 예로 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-131">An example for this QuickStart code: ***msquickstart://com.microsoft.azureactivedirectory.samples.graph.QuickStart***</span></span>

## <a name="2-register-hello-directorysearcher-application"></a><span data-ttu-id="98e7a-132">2. Hello DirectorySearcher 응용 프로그램 등록</span><span class="sxs-lookup"><span data-stu-id="98e7a-132">2. Register hello DirectorySearcher application</span></span>
<span data-ttu-id="98e7a-133">사용자가 앱 tooget 토큰을 tooset, 먼저 tooregister에서 Azure AD 테 넌 트 및 tooaccess hello Azure AD Graph API 권한 부여:</span><span class="sxs-lookup"><span data-stu-id="98e7a-133">tooset up your app tooget tokens, you first need tooregister it in your Azure AD tenant and grant it permission tooaccess hello Azure AD Graph API:</span></span>

1. <span data-ttu-id="98e7a-134">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-134">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="98e7a-135">Hello 위쪽 막대에서 계정을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-135">On hello top bar, click your account.</span></span> <span data-ttu-id="98e7a-136">Hello에서 **디렉터리** 목록 tooregister 원하는 hello Active Directory 테 넌 트 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-136">Under hello **Directory** list, choose hello Active Directory tenant where you want tooregister your application.</span></span>
3. <span data-ttu-id="98e7a-137">클릭 **더 서비스** 에 hello 맨 왼쪽 탐색 창에서 선택한 후 **Azure Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-137">Click **More Services** in hello leftmost navigation pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="98e7a-138">**앱 등록**을 클릭하고 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-138">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="98e7a-139">에 따라 hello에서 묻는 메시지를 표시 하는 새 toocreate **네이티브 클라이언트 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-139">Follow hello prompts toocreate a new **Native Client Application**.</span></span>
  * <span data-ttu-id="98e7a-140">hello **이름** 응용 프로그램의 hello 응용 프로그램 tooend 사용자에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-140">hello **Name** of hello application describes your application tooend users.</span></span>
  * <span data-ttu-id="98e7a-141">hello **리디렉션 Uri** Azure AD에서는 tooreturn 토큰 응답 체계 및 문자열 조합입니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-141">hello **Redirect Uri** is a scheme and string combination that Azure AD uses tooreturn token responses.</span></span>  <span data-ttu-id="98e7a-142">특정 tooyour 응용 프로그램이 고 hello 이전 리디렉션 URI 정보를 바탕으로 하는 값을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-142">Enter a value that is specific tooyour application and is based on hello previous redirect URI information.</span></span>
6. <span data-ttu-id="98e7a-143">Azure AD를 hello 등록을 완료 한 후 앱 고유한 응용 프로그램 ID를 할당</span><span class="sxs-lookup"><span data-stu-id="98e7a-143">After you've completed hello registration, Azure AD assigns your app a unique application ID.</span></span>  <span data-ttu-id="98e7a-144">이 값이 필요 합니다 hello 다음 섹션의 하므로에서 복사 hello 응용 프로그램 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-144">You'll need this value in hello next sections, so copy it from hello application tab.</span></span>
7. <span data-ttu-id="98e7a-145">Hello에서 **설정** 페이지에서 **필요한 권한** 선택한 후 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-145">From hello **Settings** page, select **Required Permissions** and then select **Add**.</span></span> <span data-ttu-id="98e7a-146">선택 **Microsoft Graph** hello API에 따라 다음 hello 추가 **디렉터리 데이터 읽기** 에 따른 권한 **위임 된 권한**합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-146">Select **Microsoft Graph** as hello API, and then add hello **Read Directory Data** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="98e7a-147">이 사용자에 대 한 프로그램 응용 프로그램 tooquery hello Azure AD Graph API 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-147">This sets up your application tooquery hello Azure AD Graph API for users.</span></span>

## <a name="3-install-and-configure-adal"></a><span data-ttu-id="98e7a-148">3. ADAL 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="98e7a-148">3. Install and configure ADAL</span></span>
<span data-ttu-id="98e7a-149">Azure AD에서 응용 프로그램이 있으므로 ADAL을 설치하고 ID 관련 코드를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-149">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span></span>  <span data-ttu-id="98e7a-150">Tooprovide 해야 Azure AD와 toocommunicate ADAL을 사용 하 여 응용 프로그램 등록에 대 한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-150">For ADAL toocommunicate with Azure AD, you need tooprovide it with some information about your app registration.</span></span>

1. <span data-ttu-id="98e7a-151">CocoaPods를 사용 하 여 ADAL toohello DirectorySearcher 프로젝트를 추가 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-151">Begin by adding ADAL toohello DirectorySearcher project by using CocoaPods.</span></span>

    ```
    $ vi Podfile
    ```
2. <span data-ttu-id="98e7a-152">Hello toothis podfile 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-152">Add hello following toothis podfile:</span></span>

    ```
    source 'https://github.com/CocoaPods/Specs.git'
    link_with ['QuickStart']
    xcodeproj 'QuickStart'

    pod 'ADALiOS'
    ```

3. <span data-ttu-id="98e7a-153">이제 hello podfile CocoaPods를 사용 하 여 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-153">Now load hello podfile by using CocoaPods.</span></span> <span data-ttu-id="98e7a-154">이 단계는 로드하는 새 XCode 작업 영역을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-154">This step creates a new XCode workspace that you load.</span></span>

    ```
    $ pod install
    ...
    $ open QuickStart.xcworkspace
    ```

4. <span data-ttu-id="98e7a-155">Hello 퀵 스타트 프로젝트를 열고 hello plist 파일 `settings.plist`합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-155">In hello QuickStart project, open hello plist file `settings.plist`.</span></span>  <span data-ttu-id="98e7a-156">Hello hello 요소 hello 섹션 tooreflect hello 값 hello Azure 포털에에서 입력 한 값을 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-156">Replace hello values of hello elements in hello section tooreflect hello values that you entered in hello Azure portal.</span></span> <span data-ttu-id="98e7a-157">코드에서 ADAL을 사용할 때마다 이러한 값을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-157">Your code references these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="98e7a-158">hello `tenant` Azure AD 테 넌 트 예를 들어 contoso.onmicrosoft.com hello 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-158">hello `tenant` is hello domain of your Azure AD tenant, for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="98e7a-159">hello `clientId` hello hello 포털에서 복사 하는 응용 프로그램 클라이언트 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-159">hello `clientId` is hello client ID of your application that you copied from hello portal.</span></span>
  * <span data-ttu-id="98e7a-160">hello `redirectUri` hello 포털에 등록 하는 hello 리디렉션 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-160">hello `redirectUri` is hello redirect URL that you registered in hello portal.</span></span>

## <a name="4----use-adal-tooget-tokens-from-azure-ad"></a><span data-ttu-id="98e7a-161">4.    Azure AD에서 ADAL tooget 토큰을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="98e7a-161">4.    Use ADAL tooget tokens from Azure AD</span></span>
<span data-ttu-id="98e7a-162">hello 기본적 ADAL 뒤에 응용 프로그램 액세스 토큰을 필요할 때마다 단순히는 completionBlock을 호출 하 `+(void) getToken : `, 및 ADAL rest hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-162">hello basic principle behind ADAL is that whenever your app needs an access token, it simply calls a completionBlock `+(void) getToken : `, and ADAL does hello rest.</span></span>  

1. <span data-ttu-id="98e7a-163">Hello에 `QuickStart` 프로젝트, 열기 `GraphAPICaller.m` hello 찾습니다 `// TODO: getToken for generic Web API flows. Returns a token with no additional parameters provided.` hello 맨 위 근처에 있는 주석입니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-163">In hello `QuickStart` project, open `GraphAPICaller.m` and locate hello `// TODO: getToken for generic Web API flows. Returns a token with no additional parameters provided.` comment near hello top.</span></span>  <span data-ttu-id="98e7a-164">ADAL hello 좌표는 CompletionBlock toocommunicate Azure ad를 통해 전달 하 고 방법 설명 toocache 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-164">This is where you pass ADAL hello coordinates through a CompletionBlock, toocommunicate with Azure AD, and tell it how toocache tokens.</span></span>

    ```ObjC
    +(void) getToken : (BOOL) clearCache
               parent:(UIViewController*) parent
    completionHandler:(void (^) (NSString*, NSError*))completionBlock;
    {
        AppData* data = [AppData getInstance];
        if(data.userItem){
            completionBlock(data.userItem.accessToken, nil);
            return;
        }

        ADAuthenticationError *error;
        authContext = [ADAuthenticationContext authenticationContextWithAuthority:data.authority error:&error];
        authContext.parentController = parent;
        NSURL *redirectUri = [[NSURL alloc]initWithString:data.redirectUriString];

        [ADAuthenticationSettings sharedInstance].enableFullScreen = YES;
        [authContext acquireTokenWithResource:data.resourceId
                                     clientId:data.clientId
                                  redirectUri:redirectUri
                               promptBehavior:AD_PROMPT_AUTO
                                       userId:data.userItem.userInformation.userId
                        extraQueryParameters: @"nux=1" // if this strikes you as strange it was legacy toodisplay hello correct mobile UX. You most likely won't need it in your code.
                             completionBlock:^(ADAuthenticationResult *result) {

                                  if (result.status != AD_SUCCEEDED)
                                  {
                                     completionBlock(nil, result.error);
                                  }
                                  else
                                  {
                                      data.userItem = result.tokenCacheStoreItem;
                                      completionBlock(result.tokenCacheStoreItem.accessToken, nil);
                                  }
                             }];
    }

    ```

2. <span data-ttu-id="98e7a-165">이제 필요 toouse이 토큰 toosearch hello 그래프에는 사용자에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-165">Now we need toouse this token toosearch for users in hello graph.</span></span> <span data-ttu-id="98e7a-166">Hello `// TODO: implement SearchUsersList` 메모 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-166">Find hello `// TODO: implement SearchUsersList` comment.</span></span> <span data-ttu-id="98e7a-167">이 메서드는 해당 UPN 검색 단어를 지정 하는 hello로 시작 하는 사용자에 대 한 GET 요청 toohello Azure AD Graph API tooquery를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-167">This method makes a GET request toohello Azure AD Graph API tooquery for users whose UPN begins with hello given search term.</span></span>  <span data-ttu-id="98e7a-168">tooinclude hello에서 access_token을 필요한 tooquery hello Azure AD Graph API `Authorization` hello 요청의 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-168">tooquery hello Azure AD Graph API, you need tooinclude an access_token in hello `Authorization` header of hello request.</span></span> <span data-ttu-id="98e7a-169">여기로 ADAL이 들어옵니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-169">This is where ADAL comes in.</span></span>

    ```ObjC
    +(void) searchUserList:(NSString*)searchString
                    parent:(UIViewController*) parent
          completionBlock:(void (^) (NSMutableArray* Users, NSError* error)) completionBlock
    {
        if (!loadedApplicationSettings)
       {
            [self readApplicationSettings];
        }
        
        AppData* data = [AppData getInstance];

        NSString *graphURL = [NSString stringWithFormat:@"%@%@/users?api-version=%@&$filter=startswith(userPrincipalName, '%@')", data.taskWebApiUrlString, data.tenant, data.apiversion, searchString];

        [self craftRequest:[self.class trimString:graphURL]
                    parent:parent
         completionHandler:^(NSMutableURLRequest *request, NSError *error) {

             if (error != nil)
             {
                 completionBlock(nil, error);
             }
             else
             {

                 NSOperationQueue *queue = [[NSOperationQueue alloc]init];

                 [NSURLConnection sendAsynchronousRequest:request queue:queue completionHandler:^(NSURLResponse *response, NSData *data, NSError *error) {

                     if (error == nil && data != nil){

                         NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:data options:0 error:nil];

                         // We can grab hello JSON node at hello top tooget our graph data.
                         NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                         // Don't be thrown off by hello key name being "value". It really is hello name of the
                         // first node. :-)

                         // Each object is a key value pair
                         NSDictionary *keyValuePairs;
                         NSMutableArray* Users = [[NSMutableArray alloc]init];

                         for(int i =0; i < graphDataArray.count; i++)
                         {
                             keyValuePairs = [graphDataArray objectAtIndex:i];

                             User *s = [[User alloc]init];
                             s.upn = [keyValuePairs valueForKey:@"userPrincipalName"];
                             s.name =[keyValuePairs valueForKey:@"givenName"];

                             [Users addObject:s];
                         }

                         completionBlock(Users, nil);
                     }
                     else
                     {
                         completionBlock(nil, error);
                     }

                }];
             }
         }];

    }

    ```


3. <span data-ttu-id="98e7a-170">응용 프로그램 호출 하 여 토큰을 요청 하는 경우 `getToken(...)`, ADAL hello 사용자 자격 증명을 요청 하지 않고 tooreturn 토큰을 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-170">When your app requests a token by calling `getToken(...)`, ADAL attempts tooreturn a token without asking hello user for credentials.</span></span>  <span data-ttu-id="98e7a-171">ADAL 해당 hello 사용자에 게 toosign tooget 토큰에에서 필요한 데이터를 결정 하는 경우 로그인에 대 한 대화 상자를 표시, hello 사용자의 자격 증명을 수집 되며 다음 인증을 거친 후 토큰을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-171">If ADAL determines that hello user needs toosign in tooget a token, it will display a dialog box for sign-in, collect hello user's credentials, and then return a token after successful authentication.</span></span>  <span data-ttu-id="98e7a-172">Throw ADAL 수 tooreturn 토큰 어떤 이유로 든을 없으면는 `AdalException`합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-172">If ADAL is not able tooreturn a token for any reason, it throws an `AdalException`.</span></span>

> [!Note] 
> <span data-ttu-id="98e7a-173">hello `AuthenticationResult` 개체에 포함 되어는 `tokenCacheStoreItem` 앱 필요할 수 있는 사용된 toocollect hello 정보 일 수 있는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-173">hello `AuthenticationResult` object contains a `tokenCacheStoreItem` object that can be used toocollect hello information that your app may need.</span></span> <span data-ttu-id="98e7a-174">Hello, 빠른 시작에서에서 `tokenCacheStoreItem` toodetermine 사용 되는 경우 인증이 이미 완료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-174">In hello QuickStart, `tokenCacheStoreItem` is used toodetermine if authentication is already done.</span></span>
>
>

## <a name="5-build-and-run-hello-application"></a><span data-ttu-id="98e7a-175">5. 빌드 및 hello 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="98e7a-175">5. Build and run hello application</span></span>
<span data-ttu-id="98e7a-176">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-176">Congratulations!</span></span> <span data-ttu-id="98e7a-177">IOS 응용 프로그램 사용자 인증, 안전 하 게 OAuth 2.0을 사용 하 여 웹 Api를 호출 하 고 수 있는 hello 사용자에 대 한 기본 정보를 가져올 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-177">You now have a working iOS application that can authenticate users, securely call Web APIs by using OAuth 2.0, and get basic information about hello user.</span></span>  <span data-ttu-id="98e7a-178">아직 하지 않는 이제 경우 hello 시간 toopopulate 사용자로 구성 된 테 넌 트입니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-178">If you haven't already, now is hello time toopopulate your tenant with some users.</span></span>  <span data-ttu-id="98e7a-179">빠른 시작 앱을 실행하고 해당 사용자 중 하나로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-179">Start your QuickStart app, and then sign in with one of those users.</span></span>  <span data-ttu-id="98e7a-180">해당 UPN에 따라 다른 사용자를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-180">Search for other users based on their UPN.</span></span>  <span data-ttu-id="98e7a-181">Hello 응용 프로그램을 닫은 다음 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-181">Close hello app, and then start it again.</span></span>  <span data-ttu-id="98e7a-182">Hello 사용자의 세션 그대로 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-182">Notice that hello user's session remains intact.</span></span>

<span data-ttu-id="98e7a-183">ADAL 쉽게 tooincorporate를 사용 하면 모든 응용 프로그램에 이러한 일반적인 id 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-183">ADAL makes it easy tooincorporate all of these common identity features into your application.</span></span>  <span data-ttu-id="98e7a-184">이 클래스는 담당 모든 hello dirty 작업, 캐시 관리와 같은 OAuth 프로토콜 지원 등, UI toosign hello 사용자 제시 하 고 만료 된 토큰을 새로 고친 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-184">It takes care of all hello dirty work for you, like cache management, OAuth protocol support, presenting hello user with a UI toosign in, and refreshing expired tokens.</span></span>  <span data-ttu-id="98e7a-185">Tooknow 실제로 필요한 것은 단일 API 호출 `getToken`합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-185">All you really need tooknow is a single API call, `getToken`.</span></span>

<span data-ttu-id="98e7a-186">제공 됩니다 (구성 값) 없이 완료 hello 샘플 참조용으로 [GitHub](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip)합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-186">For reference, hello completed sample (without your configuration values) is provided on [GitHub](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span></span>  

## <a name="next-steps"></a><span data-ttu-id="98e7a-187">다음 단계</span><span class="sxs-lookup"><span data-stu-id="98e7a-187">Next steps</span></span>
<span data-ttu-id="98e7a-188">이제 tooadditional 시나리오에 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-188">You can now move on tooadditional scenarios.</span></span>  <span data-ttu-id="98e7a-189">Tootry를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98e7a-189">You may want tootry:</span></span>

* [<span data-ttu-id="98e7a-190">Azure AD를 사용하여 Node.js Web API 보안 유지</span><span class="sxs-lookup"><span data-stu-id="98e7a-190">Secure a Node.JS Web API with Azure AD</span></span>](active-directory-devquickstarts-webapi-nodejs.md)
* <span data-ttu-id="98e7a-191">자세한 내용은 [어떻게 tooenable ADAL을 사용 하 여 iOS에서 응용 프로그램 간 SSO](active-directory-sso-ios.md)</span><span class="sxs-lookup"><span data-stu-id="98e7a-191">Learn [how tooenable cross-app SSO on iOS using ADAL](active-directory-sso-ios.md)</span></span>  

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]


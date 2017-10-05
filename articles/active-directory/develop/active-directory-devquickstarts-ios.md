---
title: "iOS 앱에 Azure AD 통합 | Microsoft Docs"
description: "로그인을 위해 Azure AD와 통합되고 OAuth를 사용하여 Azure AD로 보호되는 API를 호출하는 iOS 응용 프로그램 빌드 방법입니다."
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
ms.openlocfilehash: 57f465df99ac234466459b8031f61805d8334b59
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="integrate-azure-ad-into-an-ios-app"></a><span data-ttu-id="d0ff5-103">iOS 앱에 Azure AD 통합</span><span class="sxs-lookup"><span data-stu-id="d0ff5-103">Integrate Azure AD into an iOS app</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

> [!TIP]
> <span data-ttu-id="d0ff5-104">몇 분 안에 Azure Active Directory를 실행할 수 있는 새로운 [개발자 포털](https://identity.microsoft.com/Docs/iOS)의 미리 보기를 사용해 보세요.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-104">Try the preview of our new [developer portal](https://identity.microsoft.com/Docs/iOS) that helps you get up and running with Azure Active Directory in just a few minutes!</span></span>  <span data-ttu-id="d0ff5-105">개발자 포털은 앱을 등록하고 코드에 Azure AD를 통합하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-105">The developer portal guides you through the process of registering an app and integrating Azure AD into your code.</span></span>  <span data-ttu-id="d0ff5-106">이 과정을 완료하면 테넌트에서 사용자를 인증할 수 있는 간단한 응용 프로그램 및 토큰을 수락하고 유효성 검사를 수행할 수 있는 백 엔드가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-106">When you’re finished, you'll have a simple application that can authenticate users in your tenant and a backend that can accept tokens and perform validation.</span></span> 
> 
> 

<span data-ttu-id="d0ff5-107">Azure AD(Azure Active Directory)는 보호된 리소스에 액세스해야 하는 iOS 클라이언트의 경우 Active Directory 인증 라이브러리 또는 ADAL을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-107">Azure Active Directory (Azure AD) provides the Active Directory Authentication Library, or ADAL, for iOS clients that need to access protected resources.</span></span> <span data-ttu-id="d0ff5-108">ADAL은 앱에서 액세스 토큰을 가져오기 위해 사용하는 프로세스를 간소화합니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-108">ADAL simplifies the process that your app uses to obtain access tokens.</span></span> <span data-ttu-id="d0ff5-109">액세스 토큰을 얼마나 쉽게 가져올 수 있는지 보여 주기 위해 이 문서에서는 다음을 수행하는 Objective C 할 일 목록 응용 프로그램을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-109">To demonstrate how easy it is, in this article we build an Objective C To-Do List application that:</span></span>

* <span data-ttu-id="d0ff5-110">[OAuth 2.0 인증 프로토콜](https://msdn.microsoft.com/library/azure/dn645545.aspx)을 사용하여 Azure AD Graph API를 호출하기 위한 액세스 토큰을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-110">Gets access tokens for calling the Azure AD Graph API by using the [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="d0ff5-111">지정된 별칭을 가진 사용자를 디렉터리에서 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-111">Searches a directory for users with a given alias.</span></span>

<span data-ttu-id="d0ff5-112">완전하게 작동하는 응용 프로그램을 빌드하려면 다음 작업이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-112">To build the complete working application, you need to:</span></span>

1. <span data-ttu-id="d0ff5-113">Azure AD에 응용 프로그램을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-113">Register your application with Azure AD.</span></span>
2. <span data-ttu-id="d0ff5-114">ADAL을 설치 및 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-114">Install and configure ADAL.</span></span>
3. <span data-ttu-id="d0ff5-115">ADAL을 사용하여 Azure AD에서 토큰을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-115">Use ADAL to get tokens from Azure AD.</span></span>

<span data-ttu-id="d0ff5-116">시작하려면 [앱 기본 사항을 다운로드](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/skeleton.zip)하거나 [완성된 샘플을 다운로드](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip)하세요.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-116">To get started, [download the app skeleton](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/skeleton.zip) or [download the completed sample](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span></span> <span data-ttu-id="d0ff5-117">또한 사용자를 만들고 응용 프로그램을 등록할 수 있는 Azure AD 테넌트도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-117">You also need an Azure AD tenant in which you can create users and register an application.</span></span> <span data-ttu-id="d0ff5-118">테넌트가 아직 없는 경우 [얻는 방법을 알아보세요](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="d0ff5-118">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>


> [!TIP]
> <span data-ttu-id="d0ff5-119">몇 분 안에 Azure AD를 실행할 수 있는 새로운 [개발자 포털](https://identity.microsoft.com/Docs/iOS)의 미리 보기를 사용해 보세요.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-119">Try the preview of our new [developer portal](https://identity.microsoft.com/Docs/iOS) that helps you get up and running with Azure AD in just a few minutes.</span></span> <span data-ttu-id="d0ff5-120">개발자 포털은 앱을 등록하고 코드에 Azure AD를 통합하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-120">The developer portal guides you through the process of registering an app and integrating Azure AD into your code.</span></span> <span data-ttu-id="d0ff5-121">이 과정을 완료하면 테넌트에서 사용자를 인증할 수 있는 간단한 응용 프로그램 및 토큰을 수락하고 유효성 검사를 수행할 수 있는 백 엔드가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-121">When you’re finished, you'll have a simple application that can authenticate users in your tenant, and a back end that can accept tokens and perform validation.</span></span> 
> 
> 

## <a name="1-determine-what-your-redirect-uri-is-for-ios"></a><span data-ttu-id="d0ff5-122">1. iOS에 대한 리디렉션 URI 결정</span><span class="sxs-lookup"><span data-stu-id="d0ff5-122">1. Determine what your redirect URI is for iOS</span></span>
<span data-ttu-id="d0ff5-123">특정 SSO 시나리오에서 응용 프로그램을 안전하게 시작하려면, 특정 형식으로 *리디렉션 URI*를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-123">To securely start your applications in certain SSO scenarios, you must create a *redirect URI* in a particular format.</span></span> <span data-ttu-id="d0ff5-124">리디렉션 URI는 토큰을 요청하는 올바른 응용 프로그램에 반환하는데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-124">A redirect URI is used to ensure that the tokens return to the correct application that asked for them.</span></span>


<span data-ttu-id="d0ff5-125">리디렉션 URI에 대한 iOS 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-125">The iOS format for a redirect URI is:</span></span>

```
<app-scheme>://<bundle-id>
```

* <span data-ttu-id="d0ff5-126">**app-scheme** - XCode 프로젝트에 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-126">**app-scheme** - This is registered in your XCode project.</span></span> <span data-ttu-id="d0ff5-127">다른 응용 프로그램이 사용자를 호출할 수 있는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-127">It is how other applications can call you.</span></span> <span data-ttu-id="d0ff5-128">Info.plist -> URL 형식 -> URL ID에 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-128">You can find this under Info.plist -> URL types -> URL Identifier.</span></span> <span data-ttu-id="d0ff5-129">하나 이상이 구성되어 있지 않으면 하나를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-129">You should create one if you don't already have one or more configured.</span></span>
* <span data-ttu-id="d0ff5-130">**bundle-id** - XCode의 프로젝트 설정의 "ID" 아래에 있는 번들 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-130">**bundle-id** - This is the Bundle Identifier found under "identity" un your project settings in XCode.</span></span>

<span data-ttu-id="d0ff5-131">이 빠른 시작 코드는 ***msquickstart://com.microsoft.azureactivedirectory.samples.graph.QuickStart***를 예로 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-131">An example for this QuickStart code: ***msquickstart://com.microsoft.azureactivedirectory.samples.graph.QuickStart***</span></span>

## <a name="2-register-the-directorysearcher-application"></a><span data-ttu-id="d0ff5-132">2. DirectorySearcher 응용 프로그램 등록</span><span class="sxs-lookup"><span data-stu-id="d0ff5-132">2. Register the DirectorySearcher application</span></span>
<span data-ttu-id="d0ff5-133">앱에서 토큰을 가져오도록 설정하려면 먼저 Azure AD 테넌트에 앱을 등록하고 Azure AD Graph API에 액세스할 수 있는 권한을 부여해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-133">To set up your app to get tokens, you first need to register it in your Azure AD tenant and grant it permission to access the Azure AD Graph API:</span></span>

1. <span data-ttu-id="d0ff5-134">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-134">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="d0ff5-135">위쪽 막대에서 계정을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-135">On the top bar, click your account.</span></span> <span data-ttu-id="d0ff5-136">**디렉터리** 목록에서 응용 프로그램을 등록할 Active Directory 테넌트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-136">Under the **Directory** list, choose the Active Directory tenant where you want to register your application.</span></span>
3. <span data-ttu-id="d0ff5-137">왼쪽 탐색 창에서 **더 많은 서비스**를 클릭하고 **Azure Active Directory**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-137">Click **More Services** in the leftmost navigation pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="d0ff5-138">**앱 등록**을 클릭하고 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-138">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="d0ff5-139">표시되는 메시지에 따라 새 **네이티브 클라이언트 응용 프로그램**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-139">Follow the prompts to create a new **Native Client Application**.</span></span>
  * <span data-ttu-id="d0ff5-140">응용 프로그램의 **이름**은 최종 사용자에게 응용 프로그램을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-140">The **Name** of the application describes your application to end users.</span></span>
  * <span data-ttu-id="d0ff5-141">**리디렉션 Uri**는 Azure AD가 토큰 응답을 반환하는 데 사용하는 구성표 및 문자열의 조합입니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-141">The **Redirect Uri** is a scheme and string combination that Azure AD uses to return token responses.</span></span>  <span data-ttu-id="d0ff5-142">응용 프로그램과 관련되고 이전 리디렉션 URI 정보를 바탕으로 한 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-142">Enter a value that is specific to your application and is based on the previous redirect URI information.</span></span>
6. <span data-ttu-id="d0ff5-143">등록이 완료되면 Azure AD가 앱에 고유한 응용 프로그램 ID를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-143">After you've completed the registration, Azure AD assigns your app a unique application ID.</span></span>  <span data-ttu-id="d0ff5-144">이 값은 다음 섹션에서 필요하므로 응용 프로그램 탭에서 복사해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-144">You'll need this value in the next sections, so copy it from the application tab.</span></span>
7. <span data-ttu-id="d0ff5-145">**설정** 페이지에서 **필요한 사용 권한**, **추가**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-145">From the **Settings** page, select **Required Permissions** and then select **Add**.</span></span> <span data-ttu-id="d0ff5-146">**Microsoft Graph**를 API로 선택하고 **위임된 사용 권한**에서 **디렉터리 데이터 읽기** 사용 권한을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-146">Select **Microsoft Graph** as the API, and then add the **Read Directory Data** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="d0ff5-147">그러면 Azure AD Graph API에서 사용자를 쿼리하도록 응용 프로그램이 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-147">This sets up your application to query the Azure AD Graph API for users.</span></span>

## <a name="3-install-and-configure-adal"></a><span data-ttu-id="d0ff5-148">3. ADAL 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="d0ff5-148">3. Install and configure ADAL</span></span>
<span data-ttu-id="d0ff5-149">Azure AD에서 응용 프로그램이 있으므로 ADAL을 설치하고 ID 관련 코드를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-149">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span></span>  <span data-ttu-id="d0ff5-150">ADAL이 Azura AD와 통신할 수 있게 하려면, 앱 등록에 관한 일부 정보를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-150">For ADAL to communicate with Azure AD, you need to provide it with some information about your app registration.</span></span>

1. <span data-ttu-id="d0ff5-151">먼저 CocoaPods를 사용하여 DirectorySearcher 프로젝트에 ADAL을 추가하여 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-151">Begin by adding ADAL to the DirectorySearcher project by using CocoaPods.</span></span>

    ```
    $ vi Podfile
    ```
2. <span data-ttu-id="d0ff5-152">이 podfile에 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-152">Add the following to this podfile:</span></span>

    ```
    source 'https://github.com/CocoaPods/Specs.git'
    link_with ['QuickStart']
    xcodeproj 'QuickStart'

    pod 'ADALiOS'
    ```

3. <span data-ttu-id="d0ff5-153">이제 CocoaPods를 사용하여 podfile을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-153">Now load the podfile by using CocoaPods.</span></span> <span data-ttu-id="d0ff5-154">이 단계는 로드하는 새 XCode 작업 영역을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-154">This step creates a new XCode workspace that you load.</span></span>

    ```
    $ pod install
    ...
    $ open QuickStart.xcworkspace
    ```

4. <span data-ttu-id="d0ff5-155">빠른 시작 프로젝트에서.plist 파일 `settings.plist`을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-155">In the QuickStart project, open the plist file `settings.plist`.</span></span>  <span data-ttu-id="d0ff5-156">Azure Portal에 입력한 값을 반영하도록 섹션의 요소 값을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-156">Replace the values of the elements in the section to reflect the values that you entered in the Azure portal.</span></span> <span data-ttu-id="d0ff5-157">코드에서 ADAL을 사용할 때마다 이러한 값을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-157">Your code references these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="d0ff5-158">`tenant`는 Azure AD 테넌트의 도메인(예: contoso.onmicrosoft.com)입니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-158">The `tenant` is the domain of your Azure AD tenant, for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="d0ff5-159">`clientId` 는 포털에서 복사한 응용 프로그램의 클라이언트 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-159">The `clientId` is the client ID of your application that you copied from the portal.</span></span>
  * <span data-ttu-id="d0ff5-160">`redirectUri`는 포털에 등록한 리디렉션 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-160">The `redirectUri` is the redirect URL that you registered in the portal.</span></span>

## <a name="4----use-adal-to-get-tokens-from-azure-ad"></a><span data-ttu-id="d0ff5-161">4.    ADAL을 사용하여 Azure AD에서 토큰 가져오기</span><span class="sxs-lookup"><span data-stu-id="d0ff5-161">4.    Use ADAL to get tokens from Azure AD</span></span>
<span data-ttu-id="d0ff5-162">ADAL에서 확인되는 기본 원칙은 액세스 토큰이 필요할 때마다 앱이 completionBlock `+(void) getToken : `을 호출하고 나머지 작업은 ADAL이 수행한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-162">The basic principle behind ADAL is that whenever your app needs an access token, it simply calls a completionBlock `+(void) getToken : `, and ADAL does the rest.</span></span>  

1. <span data-ttu-id="d0ff5-163">`QuickStart` 프로젝트에서 `GraphAPICaller.m`를 열고 위쪽의 `// TODO: getToken for generic Web API flows. Returns a token with no additional parameters provided.` 주석을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-163">In the `QuickStart` project, open `GraphAPICaller.m` and locate the `// TODO: getToken for generic Web API flows. Returns a token with no additional parameters provided.` comment near the top.</span></span>  <span data-ttu-id="d0ff5-164">CompletionBlock을 통해 Azure AD와 통신하는 데 필요한 좌표를 ADAL에 전달하고 토큰 캐시 방법을 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-164">This is where you pass ADAL the coordinates through a CompletionBlock, to communicate with Azure AD, and tell it how to cache tokens.</span></span>

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
                        extraQueryParameters: @"nux=1" // if this strikes you as strange it was legacy to display the correct mobile UX. You most likely won't need it in your code.
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

2. <span data-ttu-id="d0ff5-165">이제 이 토큰을 사용하여 그래프에서 사용자에 대해 검색해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-165">Now we need to use this token to search for users in the graph.</span></span> <span data-ttu-id="d0ff5-166">`// TODO: implement SearchUsersList` 설명을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-166">Find the `// TODO: implement SearchUsersList` comment.</span></span> <span data-ttu-id="d0ff5-167">이 메서드는 Azure AD Graph API에 해당 UPN이 지정된 검색어로 시작하는 사용자를 쿼리하라는 GET 요청을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-167">This method makes a GET request to the Azure AD Graph API to query for users whose UPN begins with the given search term.</span></span>  <span data-ttu-id="d0ff5-168">Azure AD Graph API를 쿼리하려면 요청의 `Authorization` 헤더에 access_token을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-168">To query the Azure AD Graph API, you need to include an access_token in the `Authorization` header of the request.</span></span> <span data-ttu-id="d0ff5-169">여기로 ADAL이 들어옵니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-169">This is where ADAL comes in.</span></span>

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

                         // We can grab the JSON node at the top to get our graph data.
                         NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                         // Don't be thrown off by the key name being "value". It really is the name of the
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


3. <span data-ttu-id="d0ff5-170">앱에서 `getToken(...)`을 호출하여 토큰을 요청하면 ADAL은 사용자에게 자격 증명을 요구하지 않고 토큰을 반환하려고 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-170">When your app requests a token by calling `getToken(...)`, ADAL attempts to return a token without asking the user for credentials.</span></span>  <span data-ttu-id="d0ff5-171">ADAL은 사용자가 토큰을 가져오기 위해 로그인해야 한다고 판단할 경우 로그인 대화 상자를 표시하고, 사용자의 자격 증명을 수집하고, 인증 성공 후 토큰을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-171">If ADAL determines that the user needs to sign in to get a token, it will display a dialog box for sign-in, collect the user's credentials, and then return a token after successful authentication.</span></span>  <span data-ttu-id="d0ff5-172">어떤 이유로든 ADAL이 토큰을 반환할 수 없는 경우 `AdalException`을 throw합니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-172">If ADAL is not able to return a token for any reason, it throws an `AdalException`.</span></span>

> [!Note] 
> <span data-ttu-id="d0ff5-173">`AuthenticationResult` 개체에는 사용자 앱에 필요할 수 있는 정보를 수집하는 데 사용할 수 있는 `tokenCacheStoreItem` 개체가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-173">The `AuthenticationResult` object contains a `tokenCacheStoreItem` object that can be used to collect the information that your app may need.</span></span> <span data-ttu-id="d0ff5-174">빠른 시작에서 `tokenCacheStoreItem`은 인증이 이미 수행되었는지를 결정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-174">In the QuickStart, `tokenCacheStoreItem` is used to determine if authentication is already done.</span></span>
>
>

## <a name="5-build-and-run-the-application"></a><span data-ttu-id="d0ff5-175">5. 응용 프로그램 빌드 및 실행</span><span class="sxs-lookup"><span data-stu-id="d0ff5-175">5. Build and run the application</span></span>
<span data-ttu-id="d0ff5-176">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-176">Congratulations!</span></span> <span data-ttu-id="d0ff5-177">이제 사용자를 인증하고 OAuth 2.0을 사용하여 Web API를 안전하게 호출하고, 사용자에 대한 기본 정보를 가져올 수 있는 작동 중인 iOS 응용 프로그램이 작성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-177">You now have a working iOS application that can authenticate users, securely call Web APIs by using OAuth 2.0, and get basic information about the user.</span></span>  <span data-ttu-id="d0ff5-178">아직 일부 사용자로 테넌트를 채우지 않은 경우 지금 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-178">If you haven't already, now is the time to populate your tenant with some users.</span></span>  <span data-ttu-id="d0ff5-179">빠른 시작 앱을 실행하고 해당 사용자 중 하나로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-179">Start your QuickStart app, and then sign in with one of those users.</span></span>  <span data-ttu-id="d0ff5-180">해당 UPN에 따라 다른 사용자를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-180">Search for other users based on their UPN.</span></span>  <span data-ttu-id="d0ff5-181">앱을 닫은 다음 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-181">Close the app, and then start it again.</span></span>  <span data-ttu-id="d0ff5-182">사용자의 세션이 그대로 유지되는 것을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-182">Notice that the user's session remains intact.</span></span>

<span data-ttu-id="d0ff5-183">ADAL은 응용 프로그램에 이러한 모든 일반적인 ID 기능을 쉽게 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-183">ADAL makes it easy to incorporate all of these common identity features into your application.</span></span>  <span data-ttu-id="d0ff5-184">또한 캐시 관리, OAuth 프로토콜 지원, 사용자에게 로그인 UI 제공, 만료된 토큰 새로 고침 등의 모든 귀찮은 작업을 대신 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-184">It takes care of all the dirty work for you, like cache management, OAuth protocol support, presenting the user with a UI to sign in, and refreshing expired tokens.</span></span>  <span data-ttu-id="d0ff5-185">실제로 알아두어야 할 모든 항목은 단일 API 호출, `getToken`입니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-185">All you really need to know is a single API call, `getToken`.</span></span>

<span data-ttu-id="d0ff5-186">참조를 위해 완성된 샘플(사용자 구성 값 제외)이 [GitHub](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip)에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-186">For reference, the completed sample (without your configuration values) is provided on [GitHub](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span></span>  

## <a name="next-steps"></a><span data-ttu-id="d0ff5-187">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d0ff5-187">Next steps</span></span>
<span data-ttu-id="d0ff5-188">이제 추가 시나리오로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-188">You can now move on to additional scenarios.</span></span>  <span data-ttu-id="d0ff5-189">다음 작업을 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0ff5-189">You may want to try:</span></span>

* [<span data-ttu-id="d0ff5-190">Azure AD를 사용하여 Node.js Web API 보안 유지</span><span class="sxs-lookup"><span data-stu-id="d0ff5-190">Secure a Node.JS Web API with Azure AD</span></span>](active-directory-devquickstarts-webapi-nodejs.md)
* <span data-ttu-id="d0ff5-191">[ADAL을 사용하여 iOS에서 앱 간 SSO를 사용하도록 설정하는 방법](active-directory-sso-ios.md) 알아보기</span><span class="sxs-lookup"><span data-stu-id="d0ff5-191">Learn [how to enable cross-app SSO on iOS using ADAL](active-directory-sso-ios.md)</span></span>  

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]


---
title: "Azure AD v 2.0 끝점을 사용하여 iOS 응용 프로그램에 로그인 추가 | Microsoft Docs"
description: "타사 라이브러리를 사용하여 개인 Microsoft 계정과 회사 또는 학교 계정 둘 다로 사용자를 로그인하는 iOS 앱을 빌드하는 방법입니다."
services: active-directory
documentationcenter: 
author: brandwe
manager: mbaldwin
editor: 
ms.assetid: fd3603c0-42f7-438c-87b5-a52d20d6344b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 01/07/2017
ms.author: brandwe
ms.custom: aaddev
ms.openlocfilehash: cf1455dc3d55ea3581195f7a315556d134c23a26
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-to-an-ios-app-using-a-third-party-library-with-graph-api-using-the-v20-endpoint"></a><span data-ttu-id="d193d-103">v2.0 끝점을 사용하는 Graph API와 함께 타사 라이브러리를 사용하여 iOS 앱에 로그인 추가</span><span class="sxs-lookup"><span data-stu-id="d193d-103">Add sign-in to an iOS app using a third-party library with Graph API using the v2.0 endpoint</span></span>
<span data-ttu-id="d193d-104">Microsoft ID 플랫폼은 OAuth2 및 OpenID Connect와 같은 개방형 표준을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-104">The Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="d193d-105">개발자는 서비스와 통합하려는 모든 라이브러리를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-105">Developers can use any library they want to integrate with our services.</span></span> <span data-ttu-id="d193d-106">개발자가 플랫폼을 다른 라이브러리와 함께 사용할 수 있도록 돕기 위해, 타사 라이브러리를 Microsoft ID 플랫폼에 연결하도록 구성하는 방법을 설명하는 이와 같은 연습 몇 가지를 작성했습니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-106">To help developers use our platform with other libraries, we've written a few walkthroughs like this one to demonstrate how to configure third-party libraries to connect to the Microsoft identity platform.</span></span> <span data-ttu-id="d193d-107">[RFC6749 OAuth2 사양](https://tools.ietf.org/html/rfc6749) 을 구현하는 대부분의 라이브러리는 Microsoft ID 플랫폼에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-107">Most libraries that implement [the RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) can connect to the Microsoft identity platform.</span></span>

<span data-ttu-id="d193d-108">이 연습에서 만드는 응용 프로그램을 사용하여 해당 조직에 로그인한 다음 Graph API를 사용하여 조직에서 다른 사용자를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-108">With the application that this walkthrough creates, users can sign in to their organization and then search for others in their organization by using the Graph API.</span></span>

<span data-ttu-id="d193d-109">OAuth2 또는 OpenID Connect를 처음 접하는 경우 이 샘플 구성 대부분이 잘 이해되지 않을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-109">If you're new to OAuth2 or OpenID Connect, much of this sample configuration may not make sense to you.</span></span> <span data-ttu-id="d193d-110">배경 지식을 위해 [v2.0 프로토콜 - OAuth 2.0 권한 부여 코드 흐름](active-directory-v2-protocols-oauth-code.md)을 읽어보는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-110">We recommend that you read  [v2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md) for background.</span></span>

> [!NOTE]
> <span data-ttu-id="d193d-111">조건부 액세스 및 Intune 정책 관리 등과 같은 OAuth2 또는 OpenID Connect 표준의 식을 사용하는 플랫폼의 일부 기능은 수행하려면 오픈 소스인 Microsoft Azure ID 라이브러리를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-111">Some features of our platform that do have an expression in the OAuth2 or OpenID Connect standards, such as Conditional Access and Intune policy management, require you to use our open source Microsoft Azure Identity Libraries.</span></span>
> 
> 

<span data-ttu-id="d193d-112">v2.0 끝점에서는 일부 Azure Active Directory 시나리오 및 기능만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-112">The v2.0 endpoint does not support all Azure Active Directory scenarios and features.</span></span>

> [!NOTE]
> <span data-ttu-id="d193d-113">v2.0 끝점을 사용해야 하는지 확인하려면 [v2.0 제한 사항](active-directory-v2-limitations.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d193d-113">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download-code-from-github"></a><span data-ttu-id="d193d-114">GitHub에서 코드 다운로드</span><span class="sxs-lookup"><span data-stu-id="d193d-114">Download code from GitHub</span></span>
<span data-ttu-id="d193d-115">이 자습서에 대한 코드는 [GitHub](https://github.com/Azure-Samples/active-directory-ios-native-nxoauth2-v2)에서 유지 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-115">The code for this tutorial is maintained [on GitHub](https://github.com/Azure-Samples/active-directory-ios-native-nxoauth2-v2).</span></span>  <span data-ttu-id="d193d-116">자습서에 따라 [.zip으로 앱 구조를 다운로드](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) 하거나 구조를 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-116">To follow along, you can [download the app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) or clone the skeleton:</span></span>

```
git clone --branch skeleton git@github.com:Azure-Samples/active-directory-ios-native-nxoauth2-v2.git
```

<span data-ttu-id="d193d-117">샘플을 다운로드할 수도 있고 지금 바로 시작할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-117">You can also just download the sample and get started right away:</span></span>

```
git clone git@github.com:Azure-Samples/active-directory-ios-native-nxoauth2-v2.git
```

## <a name="register-an-app"></a><span data-ttu-id="d193d-118">앱 등록</span><span class="sxs-lookup"><span data-stu-id="d193d-118">Register an app</span></span>
<span data-ttu-id="d193d-119">[응용 프로그램 등록 포털](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)에서 새 앱을 만들거나 [v2.0 끝점을 사용하여 앱을 등록하는 방법](active-directory-v2-app-registration.md)의 자세한 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="d193d-119">Create a new app at the [Application registration portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow the detailed steps at  [How to register an app with the v2.0 endpoint](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="d193d-120">다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-120">Make sure to:</span></span>

* <span data-ttu-id="d193d-121">앱에 할당된 **응용 프로그램 ID** 는 곧 필요하므로 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-121">Copy the **Application Id** that's assigned to your app because you'll need it soon.</span></span>
* <span data-ttu-id="d193d-122">앱용 **Mobile** 플랫폼을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-122">Add the **Mobile** platform for your app.</span></span>
* <span data-ttu-id="d193d-123">포털에서 **리디렉션 URI** 를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-123">Copy the **Redirect URI** from the portal.</span></span> <span data-ttu-id="d193d-124">`urn:ietf:wg:oauth:2.0:oob`의 기본값을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-124">You must use the default value of `urn:ietf:wg:oauth:2.0:oob`.</span></span>

## <a name="download-the-third-party-nxoauth2-library-and-create-a-workspace"></a><span data-ttu-id="d193d-125">타사 NXOAuth2 라이브러리 다운로드 및 작업 영역 만들기</span><span class="sxs-lookup"><span data-stu-id="d193d-125">Download the third-party NXOAuth2 library and create a workspace</span></span>
<span data-ttu-id="d193d-126">이 연습에서는 Mac OS X 및 iOS(Cocoa 및 Cocoa touch)에 대한 OAuth2 라이브러리인 GitHub의 OAuth2Client를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-126">For this walkthrough, you will use the OAuth2Client from GitHub, which is an OAuth2 library for Mac OS X and iOS (Cocoa and Cocoa touch).</span></span> <span data-ttu-id="d193d-127">이 라이브러리는 OAuth2 사양의 초안 10에 기반을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-127">This library is based on draft 10 of the OAuth2 spec.</span></span> <span data-ttu-id="d193d-128">네이티브 응용 프로그램 프로필을 구현하고 사용자의 권한 부여 끝점을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-128">It implements the native application profile and supports the authorization endpoint of the user.</span></span> <span data-ttu-id="d193d-129">이것이 바로 Microsoft ID 플랫폼과 통합하기 위해 필요한 모든 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-129">These are all the things you'll need to integrate with the Microsoft identity platform.</span></span>

### <a name="add-the-library-to-your-project-by-using-cocoapods"></a><span data-ttu-id="d193d-130">CocoaPods를 사용하여 프로젝트에 라이브러리 추가하기</span><span class="sxs-lookup"><span data-stu-id="d193d-130">Add the library to your project by using CocoaPods</span></span>
<span data-ttu-id="d193d-131">CocoaPods는 Xcode 프로젝트에 대한 종속성 관리자입니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-131">CocoaPods is a dependency manager for Xcode projects.</span></span> <span data-ttu-id="d193d-132">이전 설치 단계를 자동으로 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-132">It manages the previous installation steps automatically.</span></span>

```
$ vi Podfile
```
1. <span data-ttu-id="d193d-133">이 podfile에 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-133">Add the following to this podfile:</span></span>
   
    ```
     platform :ios, '8.0'
   
     target 'QuickStart' do
   
     pod 'NXOAuth2Client'
   
     end
    ```
2. <span data-ttu-id="d193d-134">CocoaPods를 사용하여 podfile를 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-134">Load the podfile by using CocoaPods.</span></span> <span data-ttu-id="d193d-135">로드하려는 새 XCode 작업 영역을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-135">This will create a new Xcode workspace that you will load.</span></span>
   
    ```
    $ pod install
    ...
    $ open QuickStart.xcworkspace
    ```

## <a name="explore-the-structure-of-the-project"></a><span data-ttu-id="d193d-136">프로젝트의 구조 탐색</span><span class="sxs-lookup"><span data-stu-id="d193d-136">Explore the structure of the project</span></span>
<span data-ttu-id="d193d-137">프로젝트의 기본 골격 구조는 다음과 같이 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-137">The following structure is set up for our project in the skeleton:</span></span>

* <span data-ttu-id="d193d-138">UPN 검색으로 마스터 보기</span><span class="sxs-lookup"><span data-stu-id="d193d-138">A Master View with a UPN Search</span></span>
* <span data-ttu-id="d193d-139">선택한 사용자에 관한 데이터 세부 정보 보기</span><span class="sxs-lookup"><span data-stu-id="d193d-139">A Detail View for the data about the selected user</span></span>
* <span data-ttu-id="d193d-140">사용자가 앱에 로그인하여 그래프를 쿼리할 수 있도록 하는 로그인 뷰</span><span class="sxs-lookup"><span data-stu-id="d193d-140">A Login View where a user can sign in to the app to query the graph</span></span>

<span data-ttu-id="d193d-141">인증 추가를 위해 골격 구조의 다양한 파일로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-141">We will move to various files in the skeleton to add authentication.</span></span> <span data-ttu-id="d193d-142">시각적 코드와 같은 코드의 다른 부분은 ID와 밀접한 관련이 없으나 사용자에게 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-142">Other parts of the code, such as the visual code, do not pertain to identity but are provided for you.</span></span>

## <a name="set-up-the-settingsplst-file-in-the-library"></a><span data-ttu-id="d193d-143">라이브러리의 settings.plst 파일 설정</span><span class="sxs-lookup"><span data-stu-id="d193d-143">Set up the settings.plst file in the library</span></span>
* <span data-ttu-id="d193d-144">빠른 시작 프로젝트에서 `settings.plist` 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-144">In the QuickStart project, open the `settings.plist` file.</span></span> <span data-ttu-id="d193d-145">Azure 포털에 사용한 값을 반영하도록 섹션의 요소 값을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-145">Replace the values of the elements in the section to reflect the values that you used in the Azure portal.</span></span> <span data-ttu-id="d193d-146">코드는 Active Directory 인증 라이브러리를 사용할 때마다 이러한 값을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-146">Your code will reference these values whenever it uses the Active Directory Authentication Library.</span></span>
  * <span data-ttu-id="d193d-147">`clientId` 는 포털에서 복사한 응용 프로그램의 클라이언트 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-147">The `clientId` is the client ID of your application that you copied from the portal.</span></span>
  * <span data-ttu-id="d193d-148">`redirectUri` 는 포털에서 제공한 리디렉션 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-148">The `redirectUri` is the redirect URL that the portal provided.</span></span>

## <a name="set-up-the-nxoauth2client-library-in-your-loginviewcontroller"></a><span data-ttu-id="d193d-149">LoginViewController의 NXOAuth2Client 라이브러리 설정</span><span class="sxs-lookup"><span data-stu-id="d193d-149">Set up the NXOAuth2Client library in your LoginViewController</span></span>
<span data-ttu-id="d193d-150">NXOAuth2Client 라이브러리는 시작하기 위해 일부 값을 필요로 합니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-150">The NXOAuth2Client library requires some values to get set up.</span></span> <span data-ttu-id="d193d-151">해당 작업을 마친 후 획득한 토큰을 사용하여 Graph API를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-151">After you complete that task, you can use the acquired token to call the Graph API.</span></span> <span data-ttu-id="d193d-152">`LoginView` 는 인증이 필요할 때마다 호출되므로 해당 파일에 구성 값을 입력하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-152">Because `LoginView` will be called any time we need to authenticate, it makes sense to put configuration values in to that file.</span></span>

* <span data-ttu-id="d193d-153">`LoginViewController.m` 파일에 일부 값을 추가하여 인증 및 권한 부여에 대한 컨텍스트를 설정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-153">Let's add some values to the  `LoginViewController.m` file to set the context for authentication and authorization.</span></span> <span data-ttu-id="d193d-154">코드 다음에는 값에 대한 세부 정보가 나옵니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-154">Details about the values follow the code.</span></span>
  
    ```objc
    NSString *scopes = @"openid offline_access User.Read";
    NSString *authURL = @"https://login.microsoftonline.com/common/oauth2/v2.0/authorize";
    NSString *loginURL = @"https://login.microsoftonline.com/common/login";
    NSString *bhh = @"urn:ietf:wg:oauth:2.0:oob?code=";
    NSString *tokenURL = @"https://login.microsoftonline.com/common/oauth2/v2.0/token";
    NSString *keychain = @"com.microsoft.azureactivedirectory.samples.graph.QuickStart";
    static NSString * const kIDMOAuth2SuccessPagePrefix = @"session_state=";
    NSURL *myRequestedUrl;
    NSURL *myLoadedUrl;
    bool loginFlow = FALSE;
    bool isRequestBusy;
    NSURL *authcode;
    ```

<span data-ttu-id="d193d-155">코드에 대한 세부 정보를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-155">Let's look at details about the code.</span></span>

<span data-ttu-id="d193d-156">첫 번째 문자열은 `scopes`에 대한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-156">The first string is for `scopes`.</span></span>  <span data-ttu-id="d193d-157">`User.Read` 값을 사용하여 로그인한 사용자의 기본 프로필을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-157">The `User.Read` value allows you to read the basic profile of the signed in user.</span></span>

<span data-ttu-id="d193d-158">[Microsoft Graph 권한 범위](https://graph.microsoft.io/docs/authorization/permission_scopes)에서 사용 가능한 모든 범위에 대해 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-158">You can learn more about all the available scopes at [Microsoft Graph permission scopes](https://graph.microsoft.io/docs/authorization/permission_scopes).</span></span>

<span data-ttu-id="d193d-159">`authURL`, `loginURL`, `bhh` 및 `tokenURL`에서는 앞서 제공된 값을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-159">For `authURL`, `loginURL`, `bhh`, and `tokenURL`, you should use the values provided previously.</span></span> <span data-ttu-id="d193d-160">오픈 소스 Microsoft Azure Identity 라이브러리를 사용하는 경우 메타데이터 끝점을 사용하여 이 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-160">If you use the open source Microsoft Azure Identity Libraries, we pull this data down for you by using our metadata endpoint.</span></span> <span data-ttu-id="d193d-161">사용자를 위해 이러한 값을 추출하는 어려운 작업을 마쳤습니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-161">We've done the hard work of extracting these values for you.</span></span>

<span data-ttu-id="d193d-162">`keychain` 값은 NXOAuth2Client 라이브러리가 토큰을 저장하기 위해 키 집합을 만드는데 사용할 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-162">The `keychain` value is the container that the NXOAuth2Client library will use to create a keychain to store your tokens.</span></span> <span data-ttu-id="d193d-163">다양한 앱에서 SSO(Single Sign-On)를 가져오려 한다면 각 응용 프로그램에서 동일한 키 집합을 지정하는 것은 물론 Xcode 자격에서 그 키 집합의 사용을 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-163">If you'd like to get single sign-on (SSO) across numerous apps, you can specify the same keychain in each of your applications and request the use of that keychain in your Xcode entitlements.</span></span> <span data-ttu-id="d193d-164">이 내용은 Apple 설명서에서 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-164">This is explained in the Apple documentation.</span></span>

<span data-ttu-id="d193d-165">나머지 이런 값들은 라이브러리를 사용하여 값을 컨텍스트로 옮길 위치를 만드는 것이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-165">The rest of these values are required to use the library and create places for you to carry values to the context.</span></span>

### <a name="create-a-url-cache"></a><span data-ttu-id="d193d-166">URL 캐시 만들기</span><span class="sxs-lookup"><span data-stu-id="d193d-166">Create a URL cache</span></span>
<span data-ttu-id="d193d-167">항상 뷰를 로드한 후에 호출되는 `(void)viewDidLoad()`내부에서 다음 코드는 캐시를 사용할 수 있게 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-167">Inside `(void)viewDidLoad()`, which is always called after the view is loaded, the following code primes a cache for our use.</span></span>

<span data-ttu-id="d193d-168">다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-168">Add the following code:</span></span>

```objc
- (void)viewDidLoad {
    [super viewDidLoad];
    self.loginView.delegate = self;
    [self setupOAuth2AccountStore];
    [self requestOAuth2Access];
    NSURLCache *URLCache = [[NSURLCache alloc] initWithMemoryCapacity:4 * 1024 * 1024
                                                         diskCapacity:20 * 1024 * 1024
                                                             diskPath:nil];
    [NSURLCache setSharedURLCache:URLCache];

}
```

### <a name="create-a-webview-for-sign-in"></a><span data-ttu-id="d193d-169">로그인을 위한 WebView 만들기</span><span class="sxs-lookup"><span data-stu-id="d193d-169">Create a WebView for sign-in</span></span>
<span data-ttu-id="d193d-170">WebView는 사용자에게 SMS 텍스트 메시지(구성된 경우)와 같은 추가 요소에 대한 메시지를 표시하거나 사용자에게 오류 메시지를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-170">A WebView can prompt the user for additional factors like SMS text message (if configured) or return error messages to the user.</span></span> <span data-ttu-id="d193d-171">여기서 WebView를 설정한 후에 ID 서비스의 WebView에서 발생할 콜백을 처리할 코드를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-171">Here you'll set up the WebView and then later write the code to handle the callbacks that will happen in the WebView from the identity services.</span></span>

```objc
-(void)requestOAuth2Access {
    //to sign in to Microsoft APIs using OAuth2, we must show an embedded browser (UIWebView)
    [[NXOAuth2AccountStore sharedStore] requestAccessToAccountWithType:@"myGraphService"
                                   withPreparedAuthorizationURLHandler:^(NSURL *preparedURL) {
                                       //navigate to the URL returned by NXOAuth2Client

                                       NSURLRequest *r = [NSURLRequest requestWithURL:preparedURL];
                                       [self.loginView loadRequest:r];
                                   }];
}
```

### <a name="override-the-webview-methods-to-handle-authentication"></a><span data-ttu-id="d193d-172">인증을 처리하는 WebView 메서드 재정의</span><span class="sxs-lookup"><span data-stu-id="d193d-172">Override the WebView methods to handle authentication</span></span>
<span data-ttu-id="d193d-173">사용자가 이전에 설명한 대로 로그인해야 할 때 발생하는 상황을 WebView에 알리려면 다음 코드를 붙여넣을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-173">To tell the WebView what happens when a user needs to sign in as discussed previously, you can paste the following code.</span></span>

```objc
- (void)resolveUsingUIWebView:(NSURL *)URL {

    // We get the auth token from a redirect so we need to handle that in the webview.

    if (![NSThread isMainThread]) {
        [self performSelectorOnMainThread:@selector(resolveUsingUIWebView:) withObject:URL waitUntilDone:YES];
        return;
    }

    NSURLRequest *hostnameURLRequest = [NSURLRequest requestWithURL:URL cachePolicy:NSURLRequestUseProtocolCachePolicy timeoutInterval:10.0f];
    isRequestBusy = YES;
    [self.loginView loadRequest:hostnameURLRequest];

    NSLog(@"resolveUsingUIWebView ready (status: UNKNOWN, URL: %@)", self.loginView.request.URL);
}

- (BOOL)webView:(UIWebView *)webView shouldStartLoadWithRequest:(NSURLRequest *)request navigationType:(UIWebViewNavigationType)navigationType {

    NSLog(@"webView:shouldStartLoadWithRequest: %@ (%li)", request.URL, (long)navigationType);

    // The webview is where all the communication happens. Slightly complicated.

    myLoadedUrl = [webView.request mainDocumentURL];
    NSLog(@"***Loaded url: %@", myLoadedUrl);

    //if the UIWebView is showing our authorization URL or consent URL, show the UIWebView control
    if ([request.URL.absoluteString rangeOfString:authURL options:NSCaseInsensitiveSearch].location != NSNotFound) {
        self.loginView.hidden = NO;
    } else if ([request.URL.absoluteString rangeOfString:loginURL options:NSCaseInsensitiveSearch].location != NSNotFound) {
        //otherwise hide the UIWebView, we've left the authorization flow
        self.loginView.hidden = NO;
    } else if ([request.URL.absoluteString rangeOfString:bhh options:NSCaseInsensitiveSearch].location != NSNotFound) {
        //otherwise hide the UIWebView, we've left the authorization flow
        self.loginView.hidden = YES;
        [[NXOAuth2AccountStore sharedStore] handleRedirectURL:request.URL];
    }
    else {
        self.loginView.hidden = NO;
        //read the Location from the UIWebView, this is how Microsoft APIs is returning the
        //authentication code and relation information. This is controlled by the redirect URL we chose to use from Microsoft APIs
        //continue the OAuth2 flow
       // [[NXOAuth2AccountStore sharedStore] handleRedirectURL:request.URL];
    }

    return YES;

}
```

### <a name="write-code-to-handle-the-result-of-the-oauth2-request"></a><span data-ttu-id="d193d-174">OAuth2 요청의 결과를 처리할 코드를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-174">Write code to handle the result of the OAuth2 request</span></span>
<span data-ttu-id="d193d-175">다음 코드는 WebView에서 반환되는 redirectURL을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-175">The following code will handle the redirectURL that returns from the WebView.</span></span> <span data-ttu-id="d193d-176">인증이 실패하면 코드는 재시도합니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-176">If authentication wasn't successful, the code will try again.</span></span> <span data-ttu-id="d193d-177">한편 라이브러리는 콘솔에서 보거나 비동기식으로 처리할 수 있는 오류를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-177">Meanwhile, the library will provide the error that you can see in the console or handle asynchronously.</span></span>

```objc
- (void)handleOAuth2AccessResult:(NSString *)accessResult {

    AppData* data = [AppData getInstance];

    //parse the response for success or failure
     if (accessResult)
    //if success, complete the OAuth2 flow by handling the redirect URL and obtaining a token
     {
         [[NXOAuth2AccountStore sharedStore] handleRedirectURL:accessResult];
    } else {
        //start over
        [self requestOAuth2Access];
    }
}
```

### <a name="set-up-the-oauth-context-called-account-store"></a><span data-ttu-id="d193d-178">OAuth 컨텍스트 설정(호출된 계정 저장소)</span><span class="sxs-lookup"><span data-stu-id="d193d-178">Set up the OAuth Context (called account store)</span></span>
<span data-ttu-id="d193d-179">응용 프로그램에서 액세스할 수 있게 하려는 각 서비스에 대한 공유 계정 저장소의 `-[NXOAuth2AccountStore setClientID:secret:authorizationURL:tokenURL:redirectURL:forAccountType:]` 을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-179">Here you can call `-[NXOAuth2AccountStore setClientID:secret:authorizationURL:tokenURL:redirectURL:forAccountType:]` on the shared account store for each service that you want the application to be able to access.</span></span> <span data-ttu-id="d193d-180">계정 유형은 특정 서비스에 대한 식별자로 사용되는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-180">The account type is a string that is used as an identifier for a certain service.</span></span> <span data-ttu-id="d193d-181">Graph API에 액세스하게 되므로 코드는 `"myGraphService"`로 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-181">Because you are accessing the Graph API, the code refers to it as `"myGraphService"`.</span></span> <span data-ttu-id="d193d-182">그런 다음 토큰과 함께 뭔가가 변경될 때 알려주도록 관찰자를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-182">You then set up an observer that will tell you when anything changes with the token.</span></span> <span data-ttu-id="d193d-183">토큰을 가져온 후에는 사용자를 `masterView`로 다시 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-183">After you get the token, you return the user back to the `masterView`.</span></span>

```objc
- (void)setupOAuth2AccountStore {


        AppData* data = [AppData getInstance];

    [[NXOAuth2AccountStore sharedStore] setClientID:data.clientId
                                             secret:data.secret
                                              scope:[NSSet setWithObject:scopes]
                                   authorizationURL:[NSURL URLWithString:authURL]
                                           tokenURL:[NSURL URLWithString:tokenURL]
                                        redirectURL:[NSURL URLWithString:data.redirectUriString]
                                      keyChainGroup: keychain
                                     forAccountType:@"myGraphService"];

    [[NSNotificationCenter defaultCenter] addObserverForName:NXOAuth2AccountStoreAccountsDidChangeNotification
                                                      object:[NXOAuth2AccountStore sharedStore]
                                                       queue:nil
                                                  usingBlock:^(NSNotification *aNotification) {
                                                      if (aNotification.userInfo) {
                                                          //account added, we have access
                                                          //we can now request protected data
                                                          NSLog(@"Success!! We have an access token.");
                                                          dispatch_async(dispatch_get_main_queue(),^ {

                                                              MasterViewController* masterViewController = [self.storyboard instantiateViewControllerWithIdentifier:@"masterView"];
                                                              [self.navigationController pushViewController:masterViewController animated:YES];
                                                          });
                                                      } else {
                                                          //account removed, we lost access
                                                      }
                                                  }];

    [[NSNotificationCenter defaultCenter] addObserverForName:NXOAuth2AccountStoreDidFailToRequestAccessNotification
                                                      object:[NXOAuth2AccountStore sharedStore]
                                                       queue:nil
                                                  usingBlock:^(NSNotification *aNotification) {
                                                      NSError *error = [aNotification.userInfo objectForKey:NXOAuth2AccountStoreErrorKey];
                                                      NSLog(@"Error!! %@", error.localizedDescription);
                                                  }];
}
```

## <a name="set-up-the-master-view-to-search-and-display-the-users-from-the-graph-api"></a><span data-ttu-id="d193d-184">Graph API에서 사용자를 검색 및 표시하도록 MasterView 설정</span><span class="sxs-lookup"><span data-stu-id="d193d-184">Set up the Master View to search and display the users from the Graph API</span></span>
<span data-ttu-id="d193d-185">눈금에 반환된 데이터를 표시하는 MVC(Master-View-Controller) 앱은 이 연습에서 다루지 않으며 다양한 온라인 자습서에 해당 빌드 방법이 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-185">A Master-View-Controller (MVC) app that displays the returned data in the grid is beyond the scope of this walkthrough, and many online tutorials explain how to build one.</span></span> <span data-ttu-id="d193d-186">이러한 모든 코드는 기본 골격 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-186">All this code is in the skeleton file.</span></span> <span data-ttu-id="d193d-187">그러나 이 MVC 응용 프로그램에서 몇 가지를 다룰 필요가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-187">However, you do need to deal with a few things in this MVC application:</span></span>

* <span data-ttu-id="d193d-188">사용자가 뭔가를 검색 필드에 입력할 때 가로채기</span><span class="sxs-lookup"><span data-stu-id="d193d-188">Intercept when a user types something in the search field</span></span>
* <span data-ttu-id="d193d-189">결과를 눈금에 표시할 수 있도록 데이터의 개체를 MasterView에 다시 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-189">Provide an object of data back to the MasterView so it can display the results in the grid</span></span>

<span data-ttu-id="d193d-190">이를 아래와 같이 수행할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-190">We'll do those below.</span></span>

### <a name="add-a-check-to-see-if-youre-logged-in"></a><span data-ttu-id="d193d-191">로그인되었는지 보기 위한 확인란 추가</span><span class="sxs-lookup"><span data-stu-id="d193d-191">Add a check to see if you're logged in</span></span>
<span data-ttu-id="d193d-192">사용자가 로그인하지 않으면 응용 프로그램이 하는 일이 거의 없기 때문에 캐시에 토큰이 이미 있는지 확인하는 것이 현명합니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-192">The application does little if the user is not signed in, so it's smart to check if there is already a token in the cache.</span></span> <span data-ttu-id="d193d-193">그렇지 않은 경우 사용자가 로그인하도록 LoginView로 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-193">If not, you redirect to the LoginView for the user to sign in.</span></span> <span data-ttu-id="d193d-194">다시 말해서 뷰가 로드될 때 작업을 수행할 가장 좋은 방법은 Apple이 제공한 `viewDidLoad()` 메서드를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-194">If you recall, the best way to do actions when a view loads is to use the `viewDidLoad()` method that Apple provides us.</span></span>

```objc
- (void)viewDidLoad {
    [super viewDidLoad];


    NXOAuth2AccountStore *store = [NXOAuth2AccountStore sharedStore];
    NSArray *accounts = [store accountsWithAccountType:@"myGraphService"];

        if (accounts.count == 0) {

        dispatch_async(dispatch_get_main_queue(),^ {

            LoginViewController* userSelectController = [self.storyboard instantiateViewControllerWithIdentifier:@"LoginUserView"];
            [self.navigationController pushViewController:userSelectController animated:YES];
        });
        }
```

### <a name="update-the-table-view-when-data-is-received"></a><span data-ttu-id="d193d-195">데이터를 수신할 때 Table View 업데이트</span><span class="sxs-lookup"><span data-stu-id="d193d-195">Update the Table View when data is received</span></span>
<span data-ttu-id="d193d-196">Graph API에서 데이터를 반환할 때 해당 데이터를 표시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-196">When the Graph API returns data, you need to display the data.</span></span> <span data-ttu-id="d193d-197">편의상 여기에 테이블을 업데이트하기 위한 모든 코드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-197">For simplicity, here is all the code to update the table.</span></span> <span data-ttu-id="d193d-198">오른쪽 값을 MVC 상용구 코드에 붙여넣을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-198">You can just paste the right values in your MVC boilerplate code.</span></span>

```objc
#pragma mark - Table View

- (NSInteger)numberOfSectionsInTableView:(UITableView *)tableView {
    return 1;
}

- (NSInteger)tableView:(UITableView *)tableView numberOfRowsInSection:(NSInteger)section {

        return [upnArray count];
}

- (UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath {

    UITableViewCell *cell = [tableView dequeueReusableCellWithIdentifier:@"TaskPrototypeCell" forIndexPath:indexPath];

    if ( cell == nil ) {
        cell = [[UITableViewCell alloc] initWithStyle:UITableViewCellStyleDefault reuseIdentifier:@"TaskPrototypeCell"];
    }

    User *user = nil;
     user = [upnArray objectAtIndex:indexPath.row];


    // Configure the cell
    cell.textLabel.text = user.name;
    [cell setAccessoryType:UITableViewCellAccessoryDisclosureIndicator];

    return cell;
}

```

### <a name="provide-a-way-to-call-the-graph-api-when-someone-types-in-the-search-field"></a><span data-ttu-id="d193d-199">누군가가 검색 필드에 입력할 때 Graph API를 호출하는 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-199">Provide a way to call the Graph API when someone types in the search field</span></span>
<span data-ttu-id="d193d-200">사용자가 검색 상자에 입력할 때 입력된 내용을 Graph API로 넣을 필요가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-200">When a user types a search in the box, you need to shove that over to the Graph API.</span></span> <span data-ttu-id="d193d-201">다음 코드에서 빌드하게 되는 `GraphAPICaller` 클래스는 프레젠테이션에서 조회 기능을 분리합니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-201">The `GraphAPICaller` class, which you will build in the following code, separates the lookup functionality from the presentation.</span></span> <span data-ttu-id="d193d-202">이제, Graph API에 검색 문자를 공급하는 코드를 작성해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-202">For now, let's write the code that feeds any search characters to the Graph API.</span></span> <span data-ttu-id="d193d-203">검색할 문자열을 받는 `lookupInGraph`라는 메서드를 제공하여 이 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-203">We do this by providing a method called `lookupInGraph`, which takes the string that we want to search for.</span></span>

```objc

-(void)lookupInGraph:(NSString *)searchText {
if (searchText.length > 0) {

    };



        [GraphAPICaller searchUserList:searchText completionBlock:^(NSMutableArray* returnedUpns, NSError* error) {
            if (returnedUpns) {


                upnArray = returnedUpns;


            }
            else
            {
                UIAlertView *alertView = [[UIAlertView alloc]initWithTitle:nil message:[[NSString alloc]initWithFormat:@"Error : %@", error.localizedDescription] delegate:nil cancelButtonTitle:@"Retry" otherButtonTitles:@"Cancel", nil];

                [alertView setDelegate:self];

                dispatch_async(dispatch_get_main_queue(),^ {
                    [alertView show];
                });
            }


        }];


}
```

## <a name="write-a-helper-class-to-access-the-graph-api"></a><span data-ttu-id="d193d-204">Graph API에 액세스할 도우미 클래스 작성</span><span class="sxs-lookup"><span data-stu-id="d193d-204">Write a Helper class to access the Graph API</span></span>
<span data-ttu-id="d193d-205">이것이 응용 프로그램의 핵심입니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-205">This is the core of our application.</span></span> <span data-ttu-id="d193d-206">나머지는 Apple에서 기본 MVC 패턴으로 코드를 삽입한 반면, 여기서는 그래프를 사용자 유형으로 쿼리하고 그 데이터를 반환하는 코드를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-206">Whereas the rest was inserting code in the default MVC pattern from Apple, here you write code to query the graph as the user types and then return that data.</span></span> <span data-ttu-id="d193d-207">아래에는 코드와 자세한 설명이 차례대로 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-207">Here's the code, and a detailed explanation follows it.</span></span>

### <a name="create-a-new-objective-c-header-file"></a><span data-ttu-id="d193d-208">새 Objective C 헤더 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="d193d-208">Create a new Objective C header file</span></span>
<span data-ttu-id="d193d-209">파일 이름을 `GraphAPICaller.h`로 지정하고 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-209">Name the file `GraphAPICaller.h`, and add the following code.</span></span>

```objc
@interface GraphAPICaller : NSObject<NSURLConnectionDataDelegate>

+(void) searchUserList:(NSString*)searchString
       completionBlock:(void (^) (NSMutableArray*, NSError* error))completionBlock;

@end
```

<span data-ttu-id="d193d-210">여기서 지정된 메서드는 문자열을 가져와 completionBlock을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-210">Here you see that a specified method takes a string and returns a completionBlock.</span></span> <span data-ttu-id="d193d-211">이 completionBlock은 짐작할 수 있듯이 사용자가 검색할 때 실시간으로 데이터를 채워 넣는 개체를 제공하여 테이블을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-211">This completionBlock, as you may have guessed, will update the table by providing an object with populated data in real time as the user searches.</span></span>

### <a name="create-a-new-objective-c-file"></a><span data-ttu-id="d193d-212">새 Objective C 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="d193d-212">Create a new Objective C file</span></span>
<span data-ttu-id="d193d-213">파일 이름을 `GraphAPICaller.m`로 지정하고 다음 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-213">Name the file `GraphAPICaller.m`, and add the following method.</span></span>

```objc
+(void) searchUserList:(NSString*)searchString
       completionBlock:(void (^) (NSMutableArray* Users, NSError* error)) completionBlock
{
    if (!loadedApplicationSettings)
    {
        [self readApplicationSettings];
    }

    AppData* data = [AppData getInstance];

    NSString *graphURL = [NSString stringWithFormat:@"%@%@/users", data.graphApiUrlString, data.apiversion];

    NXOAuth2AccountStore *store = [NXOAuth2AccountStore sharedStore];
    NSDictionary* params = [self convertParamsToDictionary:searchString];

    NSArray *accounts = [store accountsWithAccountType:@"myGraphService"];
    [NXOAuth2Request performMethod:@"GET"
                        onResource:[NSURL URLWithString:graphURL]
                   usingParameters:params
                       withAccount:accounts[0]
               sendProgressHandler:^(unsigned long long bytesSend, unsigned long long bytesTotal) {
                   // e.g., update a progress indicator
               }
                   responseHandler:^(NSURLResponse *response, NSData *responseData, NSError *error) {
                       // Process the response
                       if (responseData) {
                           NSError *error;
                           NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:responseData options:0 error:nil];
                           NSLog(@"Graph Response was: %@", dataReturned);

                           // We can grab the top most JSON node to get our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                           // Don't be thrown off by the key name being "value". It really is the name of the
                           // first node. :-)

                           //each object is a key value pair
                           NSDictionary *keyValuePairs;
                           NSMutableArray* Users = [[NSMutableArray alloc]init];

                           for(int i =0; i < graphDataArray.count; i++)
                           {
                               keyValuePairs = [graphDataArray objectAtIndex:i];

                               User *s = [[User alloc]init];
                               s.upn = [keyValuePairs valueForKey:@"userPrincipalName"];
                               s.name =[keyValuePairs valueForKey:@"displayName"];
                               s.mail =[keyValuePairs valueForKey:@"mail"];
                               s.businessPhones =[keyValuePairs valueForKey:@"businessPhones"];
                               s.mobilePhones =[keyValuePairs valueForKey:@"mobilePhone"];


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

```

<span data-ttu-id="d193d-214">이 메서드를 자세히 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-214">Let's go through this method in detail.</span></span>

<span data-ttu-id="d193d-215">이 코드의 핵심은 초기에 settings.plist 파일 내에 미리 정의한 매개 변수를 사용하는 `NXOAuth2Request`메서드에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-215">The core of this code is in the `NXOAuth2Request`, method which takes the parameters that you've already defined in the settings.plist file.</span></span>

<span data-ttu-id="d193d-216">첫 번째 단계는 적절한 Graph API 호출을 생성하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-216">The first step is to construct the right Graph API call.</span></span> <span data-ttu-id="d193d-217">`/users`를 호출하게 되므로 버전과 함께 Graph API 리소스에 추가하여 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-217">Because you are calling `/users`, you specify that by appending it to the Graph API resource along with the version.</span></span> <span data-ttu-id="d193d-218">이것들이 API가 진화함에 따라 변화할 수 있으므로 외부 설정 파일에 놓는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-218">It makes sense to put these in an external settings file because these can change as the API evolves.</span></span>

```objc
NSString *graphURL = [NSString stringWithFormat:@"%@%@/users", data.graphApiUrlString, data.apiversion];
```

<span data-ttu-id="d193d-219">다음으로 Graph API 호출에 제공할 매개 변수를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-219">Next, you need to specify parameters that you will also provide to the Graph API call.</span></span> <span data-ttu-id="d193d-220">런타임 시 모든 URI 비합치 문자는 삭제됨으로 리소스 끝점에 매개 변수를 삽입하지 않는 것이 *매우 중요* 합니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-220">It is *very important* that you do not put the parameters in the resource endpoint because that is scrubbed for all non-URI conforming characters at runtime.</span></span> <span data-ttu-id="d193d-221">모든 쿼리 코드는 매개 변수에 제공되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-221">All query code must be provided in the parameters.</span></span>

```objc

NSDictionary* params = [self convertParamsToDictionary:searchString];
```

<span data-ttu-id="d193d-222">이것이 아직 작성하지 않은 메서드 `convertParamsToDictionary` 을 호출하는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-222">You might notice this calls a `convertParamsToDictionary` method that you haven't written yet.</span></span> <span data-ttu-id="d193d-223">이제 파일 끝에서 실행해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-223">Let's do so now at the end of the file:</span></span>

```objc
+(NSDictionary*) convertParamsToDictionary:(NSString*)searchString
{
    NSMutableDictionary* dictionary = [[NSMutableDictionary alloc]init];

        NSString *query = [NSString stringWithFormat:@"startswith(givenName, '%@')", searchString];

           [dictionary setValue:query forKey:@"$filter"];



    return dictionary;
}

```
<span data-ttu-id="d193d-224">다음으로 데이터를 API에서 JSON 형식으로 다시 가져오기 위해 `NXOAuth2Request` 메서드를 사용해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-224">Next, let's use the `NXOAuth2Request` method to get data back from the API in JSON format.</span></span>

```objc
NSArray *accounts = [store accountsWithAccountType:@"myGraphService"];
    [NXOAuth2Request performMethod:@"GET"
                        onResource:[NSURL URLWithString:graphURL]
                   usingParameters:params
                       withAccount:accounts[0]
               sendProgressHandler:^(unsigned long long bytesSend, unsigned long long bytesTotal) {
                   // e.g., update a progress indicator
               }
                   responseHandler:^(NSURLResponse *response, NSData *responseData, NSError *error) {
                       // Process the response
                       if (responseData) {
                           NSError *error;
                           NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:responseData options:0 error:nil];
                           NSLog(@"Graph Response was: %@", dataReturned);

                           // We can grab the top most JSON node to get our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];
```

<span data-ttu-id="d193d-225">마지막으로, 데이터를 MasterViewController에 반환하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-225">Finally, let's look at how you return the data to the MasterViewController.</span></span> <span data-ttu-id="d193d-226">데이터는 직렬화되어 반환되며 MainViewController가 사용할 수 있는 개체에 역직렬화되어 로드되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-226">The data returns as serialized and needs to be deserialized and loaded in an object that the MainViewController can consume.</span></span> <span data-ttu-id="d193d-227">이런 목적으로 기본 골격 구조에 User 개체를 만드는 `User.m/h` 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-227">For this purpose, the skeleton has a `User.m/h` file that creates a User object.</span></span> <span data-ttu-id="d193d-228">그래프의 정보로 User 개체를 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-228">You populate that User object with information from the graph.</span></span>

```objc
                           // We can grab the top most JSON node to get our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                           // Don't be thrown off by the key name being "value". It really is the name of the
                           // first node. :-)

                           //each object is a key value pair
                           NSDictionary *keyValuePairs;
                           NSMutableArray* Users = [[NSMutableArray alloc]init];

                           for(int i =0; i < graphDataArray.count; i++)
                           {
                               keyValuePairs = [graphDataArray objectAtIndex:i];

                               User *s = [[User alloc]init];
                               s.upn = [keyValuePairs valueForKey:@"userPrincipalName"];
                               s.name =[keyValuePairs valueForKey:@"displayName"];
                               s.mail =[keyValuePairs valueForKey:@"mail"];
                               s.businessPhones =[keyValuePairs valueForKey:@"businessPhones"];
                               s.mobilePhones =[keyValuePairs valueForKey:@"mobilePhone"];


                               [Users addObject:s];
```


## <a name="run-the-sample"></a><span data-ttu-id="d193d-229">샘플 실행</span><span class="sxs-lookup"><span data-stu-id="d193d-229">Run the sample</span></span>
<span data-ttu-id="d193d-230">기본 구조를 사용하거나 연습을 따라했다면 응용 프로그램이 이제 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-230">If you've used the skeleton or followed along with the walkthrough your application should now run.</span></span> <span data-ttu-id="d193d-231">시뮬레이터를 시작하고 **로그인** 을 클릭하여 응용 프로그램을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-231">Start the simulator and click **Sign in** to use the application.</span></span>

## <a name="get-security-updates-for-our-product"></a><span data-ttu-id="d193d-232">당사 제품에 대한 보안 업데이트 가져오기</span><span class="sxs-lookup"><span data-stu-id="d193d-232">Get security updates for our product</span></span>
<span data-ttu-id="d193d-233">[Security TechCenter](https://technet.microsoft.com/security/dd252948) 를 방문해서 보안 공지 경고를 구독하여 보안 사건이 발생할 때 알림을 받는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d193d-233">We encourage you to get notifications of when security incidents occur by visiting the [Security TechCenter](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>


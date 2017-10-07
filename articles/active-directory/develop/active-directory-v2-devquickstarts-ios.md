---
title: "Azure AD v2.0 끝점 hello aaaAdd 로그인 tooan iOS 응용 프로그램 사용 하 여 | Microsoft Docs"
description: "어떻게 toobuild iOS 앱 하는 서명 두 개인 Microsoft 계정으로 사용자와 회사 또는 학교 계정에 타사 라이브러리를 사용 하 여 합니다."
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
ms.openlocfilehash: a384062e6e4bd398a2b12318800728e627e05c32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooan-ios-app-using-a-third-party-library-with-graph-api-using-hello-v20-endpoint"></a><span data-ttu-id="d8095-103">타사 라이브러리를 사용 하 여 Graph api v 2.0 끝점 hello를 사용 하 여 로그인 tooan iOS 앱 추가</span><span class="sxs-lookup"><span data-stu-id="d8095-103">Add sign-in tooan iOS app using a third-party library with Graph API using hello v2.0 endpoint</span></span>
<span data-ttu-id="d8095-104">hello Microsoft id 플랫폼 OAuth2 및 OpenID Connect와 같은 개방형 표준을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-104">hello Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="d8095-105">개발자는 서비스와 toointegrate 원하는 모든 라이브러리를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-105">Developers can use any library they want toointegrate with our services.</span></span> <span data-ttu-id="d8095-106">toohelp 개발자 플랫폼을 사용 하 여 다른 라이브러리와을 작성 했습니다이 하나의 toodemonstrate와 같은 몇 가지 연습 어떻게 tooconfigure 타사 라이브러리 tooconnect toohello Microsoft id 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-106">toohelp developers use our platform with other libraries, we've written a few walkthroughs like this one toodemonstrate how tooconfigure third-party libraries tooconnect toohello Microsoft identity platform.</span></span> <span data-ttu-id="d8095-107">구현 하는 대부분의 라이브러리 [hello RFC6749 OAuth2 사양](https://tools.ietf.org/html/rfc6749) toohello Microsoft id 플랫폼을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-107">Most libraries that implement [hello RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) can connect toohello Microsoft identity platform.</span></span>

<span data-ttu-id="d8095-108">사용자는이 연습에서 만들어지는 hello 응용 프로그램을 사용 하 여 한 tootheir 조직 로그인 hello Graph API를 사용 하 여 조직에서 다른 사용자가 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-108">With hello application that this walkthrough creates, users can sign in tootheir organization and then search for others in their organization by using hello Graph API.</span></span>

<span data-ttu-id="d8095-109">이 예제 구성의 많은 새로운 tooOAuth2 또는 OpenID Connect를 사용 하는 경우 의미 tooyou를 하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-109">If you're new tooOAuth2 or OpenID Connect, much of this sample configuration may not make sense tooyou.</span></span> <span data-ttu-id="d8095-110">배경 지식을 위해 [v2.0 프로토콜 - OAuth 2.0 권한 부여 코드 흐름](active-directory-v2-protocols-oauth-code.md)을 읽어보는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-110">We recommend that you read  [v2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md) for background.</span></span>

> [!NOTE]
> <span data-ttu-id="d8095-111">OAuth2 hello 또는 조건부 액세스 및 Intune 정책 관리와 같은 OpenID Connect 표준을 식에서 없는 플랫폼의 일부 기능 있습니다 toouse 우리의 오픈 소스 Microsoft Azure Identity 라이브러리를 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-111">Some features of our platform that do have an expression in hello OAuth2 or OpenID Connect standards, such as Conditional Access and Intune policy management, require you toouse our open source Microsoft Azure Identity Libraries.</span></span>
> 
> 

<span data-ttu-id="d8095-112">hello v2.0 끝점에는 모든 Azure Active Directory 시나리오 및 기능을 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-112">hello v2.0 endpoint does not support all Azure Active Directory scenarios and features.</span></span>

> [!NOTE]
> <span data-ttu-id="d8095-113">에 대해 알아보세요 hello v2.0 끝점을 사용 해야 하는 경우 toodetermine [v2.0 제한](active-directory-v2-limitations.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-113">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download-code-from-github"></a><span data-ttu-id="d8095-114">GitHub에서 코드 다운로드</span><span class="sxs-lookup"><span data-stu-id="d8095-114">Download code from GitHub</span></span>
<span data-ttu-id="d8095-115">이 자습서에 대 한 hello 코드 유지 관리 [GitHub에서](https://github.com/Azure-Samples/active-directory-ios-native-nxoauth2-v2)합니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-115">hello code for this tutorial is maintained [on GitHub](https://github.com/Azure-Samples/active-directory-ios-native-nxoauth2-v2).</span></span>  <span data-ttu-id="d8095-116">수에 따라 toofollow, [.zip으로 hello 응용 프로그램의 기본 정의 다운로드](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) 또는 복제 hello 스 켈 레 톤:</span><span class="sxs-lookup"><span data-stu-id="d8095-116">toofollow along, you can [download hello app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) or clone hello skeleton:</span></span>

```
git clone --branch skeleton git@github.com:Azure-Samples/active-directory-ios-native-nxoauth2-v2.git
```

<span data-ttu-id="d8095-117">Hello 샘플을 다운로드할 수도 수 고를 지금 시작:</span><span class="sxs-lookup"><span data-stu-id="d8095-117">You can also just download hello sample and get started right away:</span></span>

```
git clone git@github.com:Azure-Samples/active-directory-ios-native-nxoauth2-v2.git
```

## <a name="register-an-app"></a><span data-ttu-id="d8095-118">앱 등록</span><span class="sxs-lookup"><span data-stu-id="d8095-118">Register an app</span></span>
<span data-ttu-id="d8095-119">Hello에 새 앱 만들기 [응용 프로그램 등록 포털](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), 또는 hello 세부 단계에 따라 [어떻게 tooregister hello v2.0 끝점을 사용 하 여 앱](active-directory-v2-app-registration.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-119">Create a new app at hello [Application registration portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow hello detailed steps at  [How tooregister an app with hello v2.0 endpoint](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="d8095-120">다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-120">Make sure to:</span></span>

* <span data-ttu-id="d8095-121">복사 hello **응용 프로그램 Id** 할당된 tooyour 응용 프로그램은 곧 필요 하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-121">Copy hello **Application Id** that's assigned tooyour app because you'll need it soon.</span></span>
* <span data-ttu-id="d8095-122">Hello 추가 **모바일** 응용 프로그램을 위한 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-122">Add hello **Mobile** platform for your app.</span></span>
* <span data-ttu-id="d8095-123">복사 hello **리디렉션 URI** hello 포털에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-123">Copy hello **Redirect URI** from hello portal.</span></span> <span data-ttu-id="d8095-124">기본값 hello를 사용 해야 `urn:ietf:wg:oauth:2.0:oob`합니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-124">You must use hello default value of `urn:ietf:wg:oauth:2.0:oob`.</span></span>

## <a name="download-hello-third-party-nxoauth2-library-and-create-a-workspace"></a><span data-ttu-id="d8095-125">Hello 제 3 자 NXOAuth2 라이브러리를 다운로드 하 고 작업 영역 만들기</span><span class="sxs-lookup"><span data-stu-id="d8095-125">Download hello third-party NXOAuth2 library and create a workspace</span></span>
<span data-ttu-id="d8095-126">이 연습에서는 (Cocoa 및 터치 Cocoa) iOS 및 Mac OS X에 대 한 OAuth2 라이브러리는 GitHub에서 OAuth2Client hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-126">For this walkthrough, you will use hello OAuth2Client from GitHub, which is an OAuth2 library for Mac OS X and iOS (Cocoa and Cocoa touch).</span></span> <span data-ttu-id="d8095-127">이 라이브러리의 hello OAuth2 사양 초안 10 기반으로 합니다. Hello 네이티브 응용 프로그램 프로필을 구현 하 고 hello 사용자의 hello 권한 부여 끝점을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-127">This library is based on draft 10 of hello OAuth2 spec. It implements hello native application profile and supports hello authorization endpoint of hello user.</span></span> <span data-ttu-id="d8095-128">이들은 toointegrate hello Microsoft id 플랫폼을 사용 해야 하는 모든 hello 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-128">These are all hello things you'll need toointegrate with hello Microsoft identity platform.</span></span>

### <a name="add-hello-library-tooyour-project-by-using-cocoapods"></a><span data-ttu-id="d8095-129">CocoaPods를 사용 하 여 hello 라이브러리 tooyour 프로젝트 추가</span><span class="sxs-lookup"><span data-stu-id="d8095-129">Add hello library tooyour project by using CocoaPods</span></span>
<span data-ttu-id="d8095-130">CocoaPods는 Xcode 프로젝트에 대한 종속성 관리자입니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-130">CocoaPods is a dependency manager for Xcode projects.</span></span> <span data-ttu-id="d8095-131">이전 설치 단계 hello을 자동으로 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-131">It manages hello previous installation steps automatically.</span></span>

```
$ vi Podfile
```
1. <span data-ttu-id="d8095-132">Hello toothis podfile 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-132">Add hello following toothis podfile:</span></span>
   
    ```
     platform :ios, '8.0'
   
     target 'QuickStart' do
   
     pod 'NXOAuth2Client'
   
     end
    ```
2. <span data-ttu-id="d8095-133">CocoaPods를 사용 하 여 hello podfile를 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-133">Load hello podfile by using CocoaPods.</span></span> <span data-ttu-id="d8095-134">로드하려는 새 XCode 작업 영역을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-134">This will create a new Xcode workspace that you will load.</span></span>
   
    ```
    $ pod install
    ...
    $ open QuickStart.xcworkspace
    ```

## <a name="explore-hello-structure-of-hello-project"></a><span data-ttu-id="d8095-135">Hello 프로젝트의 hello 구조 탐색</span><span class="sxs-lookup"><span data-stu-id="d8095-135">Explore hello structure of hello project</span></span>
<span data-ttu-id="d8095-136">구조를 다음 hello hello 스 켈 레 톤에서이 프로젝트에 대해 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-136">hello following structure is set up for our project in hello skeleton:</span></span>

* <span data-ttu-id="d8095-137">UPN 검색으로 마스터 보기</span><span class="sxs-lookup"><span data-stu-id="d8095-137">A Master View with a UPN Search</span></span>
* <span data-ttu-id="d8095-138">사용자를 선택 하는 hello에 대 한 hello 데이터에 대 한 세부 정보 보기</span><span class="sxs-lookup"><span data-stu-id="d8095-138">A Detail View for hello data about hello selected user</span></span>
* <span data-ttu-id="d8095-139">Toohello 앱 tooquery hello 그래프에는 사용자 로그인 수 있는 로그인 보기</span><span class="sxs-lookup"><span data-stu-id="d8095-139">A Login View where a user can sign in toohello app tooquery hello graph</span></span>

<span data-ttu-id="d8095-140">म hello 뼈대 tooadd 인증의 toovarious 파일을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-140">We will move toovarious files in hello skeleton tooadd authentication.</span></span> <span data-ttu-id="d8095-141">Hello 코드 hello 시각적 코드 등의 다른 부분 tooidentity 맞지 않는 있지만 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-141">Other parts of hello code, such as hello visual code, do not pertain tooidentity but are provided for you.</span></span>

## <a name="set-up-hello-settingsplst-file-in-hello-library"></a><span data-ttu-id="d8095-142">Hello 라이브러리의 hello settings.plst 파일 설정</span><span class="sxs-lookup"><span data-stu-id="d8095-142">Set up hello settings.plst file in hello library</span></span>
* <span data-ttu-id="d8095-143">Hello 퀵 스타트 프로젝트를 열고 hello `settings.plist` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-143">In hello QuickStart project, open hello `settings.plist` file.</span></span> <span data-ttu-id="d8095-144">Hello hello Azure 포털에서에서 사용 하는 hello 섹션 tooreflect hello 값 hello 요소 값을 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-144">Replace hello values of hello elements in hello section tooreflect hello values that you used in hello Azure portal.</span></span> <span data-ttu-id="d8095-145">Hello Active Directory 인증 라이브러리를 사용 하 여 때마다 코드는 이러한 값을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-145">Your code will reference these values whenever it uses hello Active Directory Authentication Library.</span></span>
  * <span data-ttu-id="d8095-146">hello `clientId` hello hello 포털에서 복사 하는 응용 프로그램 클라이언트 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-146">hello `clientId` is hello client ID of your application that you copied from hello portal.</span></span>
  * <span data-ttu-id="d8095-147">hello `redirectUri` hello 리디렉션 URL hello 포털이 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-147">hello `redirectUri` is hello redirect URL that hello portal provided.</span></span>

## <a name="set-up-hello-nxoauth2client-library-in-your-loginviewcontroller"></a><span data-ttu-id="d8095-148">프로그램 LoginViewController에 hello NXOAuth2Client 라이브러리 설정</span><span class="sxs-lookup"><span data-stu-id="d8095-148">Set up hello NXOAuth2Client library in your LoginViewController</span></span>
<span data-ttu-id="d8095-149">hello NXOAuth2Client 라이브러리를 설정 하는 일부 값 tooget이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-149">hello NXOAuth2Client library requires some values tooget set up.</span></span> <span data-ttu-id="d8095-150">해당 작업을 완료 한 후에 hello 토큰을 획득 한 toocall hello Graph API를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-150">After you complete that task, you can use hello acquired token toocall hello Graph API.</span></span> <span data-ttu-id="d8095-151">때문에 `LoginView` 언제 든 지 호출 됩니다는 의미가 tooput 구성 값 toothat 파일에, tooauthenticate 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-151">Because `LoginView` will be called any time we need tooauthenticate, it makes sense tooput configuration values in toothat file.</span></span>

* <span data-ttu-id="d8095-152">일부 값 toohello 추가해보겠습니다 `LoginViewController.m` 인증 및 권한 부여에 대 한 파일 tooset hello 컨텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-152">Let's add some values toohello  `LoginViewController.m` file tooset hello context for authentication and authorization.</span></span> <span data-ttu-id="d8095-153">Hello 값에 대 한 세부 정보는 hello 코드를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-153">Details about hello values follow hello code.</span></span>
  
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

<span data-ttu-id="d8095-154">Hello 코드에 대 한 세부 정보를 살펴 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-154">Let's look at details about hello code.</span></span>

<span data-ttu-id="d8095-155">에 대 한 hello 첫 번째 문자열은 `scopes`합니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-155">hello first string is for `scopes`.</span></span>  <span data-ttu-id="d8095-156">hello `User.Read` 값 tooread hello hello 사용자 로그인의 기본 프로필을 사용 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-156">hello `User.Read` value allows you tooread hello basic profile of hello signed in user.</span></span>

<span data-ttu-id="d8095-157">모든 hello 사용할 수 있는 범위에 대해 자세히 알아볼 수 있습니다 [Microsoft Graph 사용 권한 범위](https://graph.microsoft.io/docs/authorization/permission_scopes)합니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-157">You can learn more about all hello available scopes at [Microsoft Graph permission scopes](https://graph.microsoft.io/docs/authorization/permission_scopes).</span></span>

<span data-ttu-id="d8095-158">에 대 한 `authURL`, `loginURL`, `bhh`, 및 `tokenURL`, 이전에 제공 된 hello 값을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-158">For `authURL`, `loginURL`, `bhh`, and `tokenURL`, you should use hello values provided previously.</span></span> <span data-ttu-id="d8095-159">Hello 오픈 소스 Microsoft Azure Identity 라이브러리를 사용 하는 경우에서는 끌어오고이 데이터를 우리의 메타 데이터 끝점을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-159">If you use hello open source Microsoft Azure Identity Libraries, we pull this data down for you by using our metadata endpoint.</span></span> <span data-ttu-id="d8095-160">수행한 hello 복잡 한 작업을 사용자에 대 한 이러한 값을 추출 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-160">We've done hello hard work of extracting these values for you.</span></span>

<span data-ttu-id="d8095-161">hello `keychain` 값은 NXOAuth2Client 라이브러리 hello hello 컨테이너 toocreate 키 집합 toostore 프로그램 토큰을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-161">hello `keychain` value is hello container that hello NXOAuth2Client library will use toocreate a keychain toostore your tokens.</span></span> <span data-ttu-id="d8095-162">지정할 수는 경우 원하는 tooget single sign on (SSO) 여러 앱 간에 각 응용 프로그램에서 동일한 키 집합 hello 및 hello를 사용 하 여 Xcode 자격에 해당 키 집합의 요청을 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-162">If you'd like tooget single sign-on (SSO) across numerous apps, you can specify hello same keychain in each of your applications and request hello use of that keychain in your Xcode entitlements.</span></span> <span data-ttu-id="d8095-163">이 hello Apple 설명서에에서 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-163">This is explained in hello Apple documentation.</span></span>

<span data-ttu-id="d8095-164">이러한 값의 hello 나머지 필수 toouse hello 라이브러리 이며 toocarry 값 toohello 컨텍스트를 위치를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-164">hello rest of these values are required toouse hello library and create places for you toocarry values toohello context.</span></span>

### <a name="create-a-url-cache"></a><span data-ttu-id="d8095-165">URL 캐시 만들기</span><span class="sxs-lookup"><span data-stu-id="d8095-165">Create a URL cache</span></span>
<span data-ttu-id="d8095-166">내부 `(void)viewDidLoad()`, 이라고 하는 항상 hello 보기 로드 된 후, hello 다음 코드 primes 사용에 대 한 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-166">Inside `(void)viewDidLoad()`, which is always called after hello view is loaded, hello following code primes a cache for our use.</span></span>

<span data-ttu-id="d8095-167">Hello 코드 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-167">Add hello following code:</span></span>

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

### <a name="create-a-webview-for-sign-in"></a><span data-ttu-id="d8095-168">로그인을 위한 WebView 만들기</span><span class="sxs-lookup"><span data-stu-id="d8095-168">Create a WebView for sign-in</span></span>
<span data-ttu-id="d8095-169">웹 보기는 SMS 문자 메시지 (구성 된 경우)와 같은 추가 요소에 대 한 hello 사용자 메시지를 표시 하거나 메시지 toohello 사용자가 오류를 반환 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-169">A WebView can prompt hello user for additional factors like SMS text message (if configured) or return error messages toohello user.</span></span> <span data-ttu-id="d8095-170">여기를 설정 합니다 WebView hello 및 다음 나중 쓰기 hello 일이 발생 하는 코드 toohandle hello 콜백을 hello WebView의에서 hello id 서비스에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-170">Here you'll set up hello WebView and then later write hello code toohandle hello callbacks that will happen in hello WebView from hello identity services.</span></span>

```objc
-(void)requestOAuth2Access {
    //toosign in tooMicrosoft APIs using OAuth2, we must show an embedded browser (UIWebView)
    [[NXOAuth2AccountStore sharedStore] requestAccessToAccountWithType:@"myGraphService"
                                   withPreparedAuthorizationURLHandler:^(NSURL *preparedURL) {
                                       //navigate toohello URL returned by NXOAuth2Client

                                       NSURLRequest *r = [NSURLRequest requestWithURL:preparedURL];
                                       [self.loginView loadRequest:r];
                                   }];
}
```

### <a name="override-hello-webview-methods-toohandle-authentication"></a><span data-ttu-id="d8095-171">Hello WebView 메서드 toohandle 인증 재정의</span><span class="sxs-lookup"><span data-stu-id="d8095-171">Override hello WebView methods toohandle authentication</span></span>
<span data-ttu-id="d8095-172">tootell hello WebView 사용자는 이전에 설명한 대로 toosign에 있어야 하는 경우, 코드 다음 hello를 붙여넣을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-172">tootell hello WebView what happens when a user needs toosign in as discussed previously, you can paste hello following code.</span></span>

```objc
- (void)resolveUsingUIWebView:(NSURL *)URL {

    // We get hello auth token from a redirect so we need toohandle that in hello webview.

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

    // hello webview is where all hello communication happens. Slightly complicated.

    myLoadedUrl = [webView.request mainDocumentURL];
    NSLog(@"***Loaded url: %@", myLoadedUrl);

    //if hello UIWebView is showing our authorization URL or consent URL, show hello UIWebView control
    if ([request.URL.absoluteString rangeOfString:authURL options:NSCaseInsensitiveSearch].location != NSNotFound) {
        self.loginView.hidden = NO;
    } else if ([request.URL.absoluteString rangeOfString:loginURL options:NSCaseInsensitiveSearch].location != NSNotFound) {
        //otherwise hide hello UIWebView, we've left hello authorization flow
        self.loginView.hidden = NO;
    } else if ([request.URL.absoluteString rangeOfString:bhh options:NSCaseInsensitiveSearch].location != NSNotFound) {
        //otherwise hide hello UIWebView, we've left hello authorization flow
        self.loginView.hidden = YES;
        [[NXOAuth2AccountStore sharedStore] handleRedirectURL:request.URL];
    }
    else {
        self.loginView.hidden = NO;
        //read hello Location from hello UIWebView, this is how Microsoft APIs is returning the
        //authentication code and relation information. This is controlled by hello redirect URL we chose toouse from Microsoft APIs
        //continue hello OAuth2 flow
       // [[NXOAuth2AccountStore sharedStore] handleRedirectURL:request.URL];
    }

    return YES;

}
```

### <a name="write-code-toohandle-hello-result-of-hello-oauth2-request"></a><span data-ttu-id="d8095-173">Hello OAuth2 요청 결과인 toohandle hello 코드 작성</span><span class="sxs-lookup"><span data-stu-id="d8095-173">Write code toohandle hello result of hello OAuth2 request</span></span>
<span data-ttu-id="d8095-174">hello 다음 코드에서는 처리 hello 웹 보기에서에서 반환 하는 hello redirectURL 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-174">hello following code will handle hello redirectURL that returns from hello WebView.</span></span> <span data-ttu-id="d8095-175">인증 되지 않았지만, hello 코드 다시 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-175">If authentication wasn't successful, hello code will try again.</span></span> <span data-ttu-id="d8095-176">한편, hello 라이브러리는 비동기적으로 처리 하거나 hello 콘솔에서 볼 수 있는 hello 오류를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-176">Meanwhile, hello library will provide hello error that you can see in hello console or handle asynchronously.</span></span>

```objc
- (void)handleOAuth2AccessResult:(NSString *)accessResult {

    AppData* data = [AppData getInstance];

    //parse hello response for success or failure
     if (accessResult)
    //if success, complete hello OAuth2 flow by handling hello redirect URL and obtaining a token
     {
         [[NXOAuth2AccountStore sharedStore] handleRedirectURL:accessResult];
    } else {
        //start over
        [self requestOAuth2Access];
    }
}
```

### <a name="set-up-hello-oauth-context-called-account-store"></a><span data-ttu-id="d8095-177">Hello OAuth 컨텍스트 (계정 저장소 라고도 함)를 설정</span><span class="sxs-lookup"><span data-stu-id="d8095-177">Set up hello OAuth Context (called account store)</span></span>
<span data-ttu-id="d8095-178">호출할 수는 여기 `-[NXOAuth2AccountStore setClientID:secret:authorizationURL:tokenURL:redirectURL:forAccountType:]` hello 응용 프로그램 toobe 수 tooaccess 하려는 각 서비스에 대 한 hello 공유 계정 저장소에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-178">Here you can call `-[NXOAuth2AccountStore setClientID:secret:authorizationURL:tokenURL:redirectURL:forAccountType:]` on hello shared account store for each service that you want hello application toobe able tooaccess.</span></span> <span data-ttu-id="d8095-179">hello 계정 유형은 특정 서비스에 대 한 식별자로 사용 되는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-179">hello account type is a string that is used as an identifier for a certain service.</span></span> <span data-ttu-id="d8095-180">Hello 코드 참조로 tooit hello Graph API에 액세스 하는 때문에 `"myGraphService"`합니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-180">Because you are accessing hello Graph API, hello code refers tooit as `"myGraphService"`.</span></span> <span data-ttu-id="d8095-181">그런 다음 알려 hello 토큰 변경 사항이 관찰자를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-181">You then set up an observer that will tell you when anything changes with hello token.</span></span> <span data-ttu-id="d8095-182">Hello 사용자 백 toohello hello 토큰을 가져온 후 돌아가면 `masterView`합니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-182">After you get hello token, you return hello user back toohello `masterView`.</span></span>

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

## <a name="set-up-hello-master-view-toosearch-and-display-hello-users-from-hello-graph-api"></a><span data-ttu-id="d8095-183">마스터 뷰 toosearch hello를 설정 하 고 hello Graph API의에서 hello 사용자 표시</span><span class="sxs-lookup"><span data-stu-id="d8095-183">Set up hello Master View toosearch and display hello users from hello Graph API</span></span>
<span data-ttu-id="d8095-184">많은 온라인 자습서에 설명 하 고 hello 표에 데이터를 반환 하는 hello를 표시 하는 마스터-뷰-컨트롤러 (MVC) 앱은이 연습의 hello 다루지 않습니다 어떻게 toobuild 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-184">A Master-View-Controller (MVC) app that displays hello returned data in hello grid is beyond hello scope of this walkthrough, and many online tutorials explain how toobuild one.</span></span> <span data-ttu-id="d8095-185">이 모든 코드는 hello 뼈대 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-185">All this code is in hello skeleton file.</span></span> <span data-ttu-id="d8095-186">그러나이 MVC 응용 프로그램에는 몇 가지 사항을 toodeal 필요가:</span><span class="sxs-lookup"><span data-stu-id="d8095-186">However, you do need toodeal with a few things in this MVC application:</span></span>

* <span data-ttu-id="d8095-187">Intercept 사용자 hello 검색 필드에 값을 입력할 때</span><span class="sxs-lookup"><span data-stu-id="d8095-187">Intercept when a user types something in hello search field</span></span>
* <span data-ttu-id="d8095-188">Hello 표에 hello 결과 표시할 수 있도록 데이터 백 toohello MasterView의 개체를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-188">Provide an object of data back toohello MasterView so it can display hello results in hello grid</span></span>

<span data-ttu-id="d8095-189">이를 아래와 같이 수행할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-189">We'll do those below.</span></span>

### <a name="add-a-check-toosee-if-youre-logged-in"></a><span data-ttu-id="d8095-190">사용자가 로그인 하는 경우 확인 toosee 추가</span><span class="sxs-lookup"><span data-stu-id="d8095-190">Add a check toosee if you're logged in</span></span>
<span data-ttu-id="d8095-191">hello 응용 프로그램에 거의 hello 사용자가 로그인 되지 않은 경우 hello 캐시에서 토큰을 이미이 스마트 toocheck 되기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-191">hello application does little if hello user is not signed in, so it's smart toocheck if there is already a token in hello cache.</span></span> <span data-ttu-id="d8095-192">사용자 toosign hello에 대 한 LoginView toohello 리디렉션되지 그렇지 않은 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-192">If not, you redirect toohello LoginView for hello user toosign in.</span></span> <span data-ttu-id="d8095-193">Hello 가장 좋은 방법은 toodo 작업 보기를 로드 하는 경우는 toouse hello을 기억나지 `viewDidLoad()` Apple 제공 하는 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-193">If you recall, hello best way toodo actions when a view loads is toouse hello `viewDidLoad()` method that Apple provides us.</span></span>

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

### <a name="update-hello-table-view-when-data-is-received"></a><span data-ttu-id="d8095-194">데이터를 받을 때 hello 테이블 뷰 업데이트</span><span class="sxs-lookup"><span data-stu-id="d8095-194">Update hello Table View when data is received</span></span>
<span data-ttu-id="d8095-195">Graph API hello 데이터 반환 될 때 toodisplay hello 데이터가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-195">When hello Graph API returns data, you need toodisplay hello data.</span></span> <span data-ttu-id="d8095-196">간단히 하기 위해 모든 hello 코드 tooupdate hello 테이블 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-196">For simplicity, here is all hello code tooupdate hello table.</span></span> <span data-ttu-id="d8095-197">Hello 오른쪽 값 MVC 상용구 코드에 붙여넣을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-197">You can just paste hello right values in your MVC boilerplate code.</span></span>

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


    // Configure hello cell
    cell.textLabel.text = user.name;
    [cell setAccessoryType:UITableViewCellAccessoryDisclosureIndicator];

    return cell;
}

```

### <a name="provide-a-way-toocall-hello-graph-api-when-someone-types-in-hello-search-field"></a><span data-ttu-id="d8095-198">Hello 검색 필드에 입력할 때 방법을 toocall hello Graph API를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-198">Provide a way toocall hello Graph API when someone types in hello search field</span></span>
<span data-ttu-id="d8095-199">Tooshove hello 상자에 입력 한 검색 하는 경우 해야 toohello Graph API를 통해입니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-199">When a user types a search in hello box, you need tooshove that over toohello Graph API.</span></span> <span data-ttu-id="d8095-200">hello `GraphAPICaller` hello 코드 뒤에서 작성 하는 클래스를 hello 프레젠테이션에서 hello 조회 기능을 분리 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-200">hello `GraphAPICaller` class, which you will build in hello following code, separates hello lookup functionality from hello presentation.</span></span> <span data-ttu-id="d8095-201">지금은 Graph API의 모든 검색 문자 toohello 피드 hello 코드를 작성해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-201">For now, let's write hello code that feeds any search characters toohello Graph API.</span></span> <span data-ttu-id="d8095-202">라는 메서드를 제공 하 여 수행할 `lookupInGraph`, hello 문자열에 대 한 toosearch 원하는 사용 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-202">We do this by providing a method called `lookupInGraph`, which takes hello string that we want toosearch for.</span></span>

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

## <a name="write-a-helper-class-tooaccess-hello-graph-api"></a><span data-ttu-id="d8095-203">Graph API 도우미 클래스 tooaccess hello</span><span class="sxs-lookup"><span data-stu-id="d8095-203">Write a Helper class tooaccess hello Graph API</span></span>
<span data-ttu-id="d8095-204">응용 프로그램의 hello 핵심입니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-204">This is hello core of our application.</span></span> <span data-ttu-id="d8095-205">Hello rest Apple hello 기본 MVC 패턴에서 코드를 삽입 했습니다, 반면 여기 있습니다 작성 코드 tooquery hello 그래프 hello 사용자가 하 고 해당 데이터를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-205">Whereas hello rest was inserting code in hello default MVC pattern from Apple, here you write code tooquery hello graph as hello user types and then return that data.</span></span> <span data-ttu-id="d8095-206">다음은 hello 코드 및 대 한 자세한 내용은 뒤에 오는 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-206">Here's hello code, and a detailed explanation follows it.</span></span>

### <a name="create-a-new-objective-c-header-file"></a><span data-ttu-id="d8095-207">새 Objective C 헤더 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="d8095-207">Create a new Objective C header file</span></span>
<span data-ttu-id="d8095-208">이름 hello 파일 `GraphAPICaller.h`, 코드 다음 hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-208">Name hello file `GraphAPICaller.h`, and add hello following code.</span></span>

```objc
@interface GraphAPICaller : NSObject<NSURLConnectionDataDelegate>

+(void) searchUserList:(NSString*)searchString
       completionBlock:(void (^) (NSMutableArray*, NSError* error))completionBlock;

@end
```

<span data-ttu-id="d8095-209">여기서 지정된 메서드는 문자열을 가져와 completionBlock을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-209">Here you see that a specified method takes a string and returns a completionBlock.</span></span> <span data-ttu-id="d8095-210">이 completionBlock 짐작할 수 있습니다는 테이블을 업데이트할 hello hello 사용자 검색으로 실시간으로 채워진된 데이터에 개체를 제공 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-210">This completionBlock, as you may have guessed, will update hello table by providing an object with populated data in real time as hello user searches.</span></span>

### <a name="create-a-new-objective-c-file"></a><span data-ttu-id="d8095-211">새 Objective C 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="d8095-211">Create a new Objective C file</span></span>
<span data-ttu-id="d8095-212">이름 hello 파일 `GraphAPICaller.m`, hello 메서드 뒤에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-212">Name hello file `GraphAPICaller.m`, and add hello following method.</span></span>

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
                       // Process hello response
                       if (responseData) {
                           NSError *error;
                           NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:responseData options:0 error:nil];
                           NSLog(@"Graph Response was: %@", dataReturned);

                           // We can grab hello top most JSON node tooget our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                           // Don't be thrown off by hello key name being "value". It really is hello name of the
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

<span data-ttu-id="d8095-213">이 메서드를 자세히 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-213">Let's go through this method in detail.</span></span>

<span data-ttu-id="d8095-214">이 코드의 hello 핵심 hello 중인 `NXOAuth2Request`, hello 매개 변수를 사용 하면 이미 정의한 hello settings.plist 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-214">hello core of this code is in hello `NXOAuth2Request`, method which takes hello parameters that you've already defined in hello settings.plist file.</span></span>

<span data-ttu-id="d8095-215">hello 첫 번째 단계는 tooconstruct hello 오른쪽 Graph API 호출입니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-215">hello first step is tooconstruct hello right Graph API call.</span></span> <span data-ttu-id="d8095-216">호출 하는 때문에 `/users`, hello 버전과 함께 toohello Graph API 리소스를 추가 하 여 지정 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-216">Because you are calling `/users`, you specify that by appending it toohello Graph API resource along with hello version.</span></span> <span data-ttu-id="d8095-217">이렇게 하면 의미 tooput 외부 설정 파일에 이러한 내용을 hello API 진화 함에 따라 이러한가 변경 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-217">It makes sense tooput these in an external settings file because these can change as hello API evolves.</span></span>

```objc
NSString *graphURL = [NSString stringWithFormat:@"%@%@/users", data.graphApiUrlString, data.apiversion];
```

<span data-ttu-id="d8095-218">다음으로, 해야 toospecify 매개 변수 toohello Graph API 호출 또한 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-218">Next, you need toospecify parameters that you will also provide toohello Graph API call.</span></span> <span data-ttu-id="d8095-219">*매우 중요 한* 를 배치 하지 않는 hello 매개 변수 hello 리소스 끝점에서 런타임에 모든 URI가 아닌 표준에 맞는 문자에 대해 삭제 되는 때문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-219">It is *very important* that you do not put hello parameters in hello resource endpoint because that is scrubbed for all non-URI conforming characters at runtime.</span></span> <span data-ttu-id="d8095-220">모든 쿼리 코드 hello 매개 변수에서 제공 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-220">All query code must be provided in hello parameters.</span></span>

```objc

NSDictionary* params = [self convertParamsToDictionary:searchString];
```

<span data-ttu-id="d8095-221">이것이 아직 작성하지 않은 메서드 `convertParamsToDictionary` 을 호출하는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-221">You might notice this calls a `convertParamsToDictionary` method that you haven't written yet.</span></span> <span data-ttu-id="d8095-222">Hello hello 파일 끝에 이제 수행 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-222">Let's do so now at hello end of hello file:</span></span>

```objc
+(NSDictionary*) convertParamsToDictionary:(NSString*)searchString
{
    NSMutableDictionary* dictionary = [[NSMutableDictionary alloc]init];

        NSString *query = [NSString stringWithFormat:@"startswith(givenName, '%@')", searchString];

           [dictionary setValue:query forKey:@"$filter"];



    return dictionary;
}

```
<span data-ttu-id="d8095-223">다음으로 hello를 사용 하 여 보겠습니다 `NXOAuth2Request` 메서드 tooget 데이터를 JSON 형식으로 hello API에서에서 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-223">Next, let's use hello `NXOAuth2Request` method tooget data back from hello API in JSON format.</span></span>

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
                       // Process hello response
                       if (responseData) {
                           NSError *error;
                           NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:responseData options:0 error:nil];
                           NSLog(@"Graph Response was: %@", dataReturned);

                           // We can grab hello top most JSON node tooget our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];
```

<span data-ttu-id="d8095-224">마지막으로, 살펴보겠습니다 hello 데이터 toohello MasterViewController를 반환 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="d8095-224">Finally, let's look at how you return hello data toohello MasterViewController.</span></span> <span data-ttu-id="d8095-225">hello 데이터 직렬화 할를 반환 하 고 역직렬화 toobe 필요 하 고 개체에 로드 된 해당 hello MainViewController 소비할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-225">hello data returns as serialized and needs toobe deserialized and loaded in an object that hello MainViewController can consume.</span></span> <span data-ttu-id="d8095-226">이 작업을 위해 hello 구조에는 `User.m/h` 사용자 개체를 만드는 파일을 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-226">For this purpose, hello skeleton has a `User.m/h` file that creates a User object.</span></span> <span data-ttu-id="d8095-227">해당 사용자 개체를 hello 그래프의 정보로 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-227">You populate that User object with information from hello graph.</span></span>

```objc
                           // We can grab hello top most JSON node tooget our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                           // Don't be thrown off by hello key name being "value". It really is hello name of the
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


## <a name="run-hello-sample"></a><span data-ttu-id="d8095-228">Hello 예제 실행</span><span class="sxs-lookup"><span data-stu-id="d8095-228">Run hello sample</span></span>
<span data-ttu-id="d8095-229">Hello 구조를 사용 하거나 hello 연습 함께 다음 경우에 응용 프로그램 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-229">If you've used hello skeleton or followed along with hello walkthrough your application should now run.</span></span> <span data-ttu-id="d8095-230">Hello 시뮬레이터를 시작 하 고 클릭 **로그인** toouse hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-230">Start hello simulator and click **Sign in** toouse hello application.</span></span>

## <a name="get-security-updates-for-our-product"></a><span data-ttu-id="d8095-231">당사 제품에 대한 보안 업데이트 가져오기</span><span class="sxs-lookup"><span data-stu-id="d8095-231">Get security updates for our product</span></span>
<span data-ttu-id="d8095-232">보안 사고 hello를 방문 하 여 발생 하는 경우의 알림 tooget 좋습니다 [보안 TechCenter](https://technet.microsoft.com/security/dd252948) 및 tooSecurity 자문 경고를 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8095-232">We encourage you tooget notifications of when security incidents occur by visiting hello [Security TechCenter](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>


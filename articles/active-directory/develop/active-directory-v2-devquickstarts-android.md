---
title: "aaaAzure Active Directory v2.0 Android 앱 | Microsoft Docs"
description: "어떻게 toobuild 개인 Microsoft 계정 및 작업 또는 학교 계정 및 모두 호출 된 사용자가 로그인 하는 Android 응용 프로그램 타사 라이브러리를 사용 하 여 Graph API를 hello 합니다."
services: active-directory
documentationcenter: 
author: danieldobalian
manager: mbaldwin
editor: 
ms.assetid: 16294c07-f27d-45c9-833f-7dbb12083794
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: dadobali
ms.custom: aaddev
ms.openlocfilehash: 1dd40bd3bcea28c629abce09abaed66b38774162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooan-android-app-using-a-third-party-library-with-graph-api-using-hello-v20-endpoint"></a><span data-ttu-id="7f014-103">타사 라이브러리를 사용 하 여 Graph api v 2.0 끝점 hello를 사용 하 여 로그인 tooan Android 앱 추가</span><span class="sxs-lookup"><span data-stu-id="7f014-103">Add sign-in tooan Android app using a third-party library with Graph API using hello v2.0 endpoint</span></span>
<span data-ttu-id="7f014-104">hello Microsoft id 플랫폼 OAuth2 및 OpenID Connect와 같은 개방형 표준을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7f014-104">hello Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="7f014-105">개발자는 서비스와 toointegrate 원하는 모든 라이브러리를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f014-105">Developers can use any library they want toointegrate with our services.</span></span> <span data-ttu-id="7f014-106">toohelp 개발자 플랫폼을 사용 하 여 다른 라이브러리와을 작성 했습니다이 하나의 toodemonstrate와 같은 몇 가지 연습 어떻게 tooconfigure 타사 라이브러리 tooconnect toohello Microsoft id 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="7f014-106">toohelp developers use our platform with other libraries, we've written a few walkthroughs like this one toodemonstrate how tooconfigure third-party libraries tooconnect toohello Microsoft identity platform.</span></span> <span data-ttu-id="7f014-107">구현 하는 대부분의 라이브러리 [hello RFC6749 OAuth2 사양](https://tools.ietf.org/html/rfc6749) toohello Microsoft id 플랫폼을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f014-107">Most libraries that implement [hello RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) can connect toohello Microsoft identity platform.</span></span>

<span data-ttu-id="7f014-108">사용자는이 연습에서 만들어지는 hello 응용 프로그램을 사용 하 여 한 tootheir 조직 로그인 hello Graph API를 사용 하 여 조직에서 자신에 대 한을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f014-108">With hello application that this walkthrough creates, users can sign in tootheir organization and then search for themselves in their organization by using hello Graph API.</span></span>

<span data-ttu-id="7f014-109">이 예제 구성의 많은 새로운 tooOAuth2 또는 OpenID Connect를 사용 하는 경우 의미 tooyou를 하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f014-109">If you're new tooOAuth2 or OpenID Connect, much of this sample configuration may not make sense tooyou.</span></span> <span data-ttu-id="7f014-110">배경 지식을 위해 [2.0 프로토콜 - OAuth 2.0 권한 부여 코드 흐름](active-directory-v2-protocols-oauth-code.md)을 읽어보는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7f014-110">We recommend that you read [2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md) for background.</span></span>

> [!NOTE]
> <span data-ttu-id="7f014-111">OAuth2 hello 또는 조건부 액세스 및 Intune 정책 관리와 같은 OpenID Connect 표준을 식에서 없는 플랫폼의 일부 기능 있습니다 toouse 우리의 오픈 소스 Microsoft Azure Identity 라이브러리를 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f014-111">Some features of our platform that do have an expression in hello OAuth2 or OpenID Connect standards, such as Conditional Access and Intune policy management, require you toouse our open source Microsoft Azure Identity Libraries.</span></span>
> 
> 

<span data-ttu-id="7f014-112">hello v2.0 끝점에는 모든 Azure Active Directory 시나리오 및 기능을 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7f014-112">hello v2.0 endpoint does not support all Azure Active Directory scenarios and features.</span></span>

> [!NOTE]
> <span data-ttu-id="7f014-113">에 대해 알아보세요 hello v2.0 끝점을 사용 해야 하는 경우 toodetermine [v2.0 제한](active-directory-v2-limitations.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7f014-113">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download-hello-code-from-github"></a><span data-ttu-id="7f014-114">GitHub에서 hello 코드를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f014-114">Download hello code from GitHub</span></span>
<span data-ttu-id="7f014-115">이 자습서에 대 한 hello 코드 유지 관리 [GitHub에서](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2)합니다.</span><span class="sxs-lookup"><span data-stu-id="7f014-115">hello code for this tutorial is maintained [on GitHub](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2).</span></span>  <span data-ttu-id="7f014-116">수에 따라 toofollow, [.zip으로 hello 응용 프로그램의 기본 정의 다운로드](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2/archive/skeleton.zip) 또는 복제 hello 스 켈 레 톤:</span><span class="sxs-lookup"><span data-stu-id="7f014-116">toofollow along, you can  [download hello app's skeleton as a .zip](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2/archive/skeleton.zip) or clone hello skeleton:</span></span>

```
git clone --branch skeleton git@github.com:Azure-Samples/active-directory-android-native-oidcandroidlib-v2.git
```

<span data-ttu-id="7f014-117">Hello 샘플을 다운로드할 수도 수 고를 지금 시작:</span><span class="sxs-lookup"><span data-stu-id="7f014-117">You can also just download hello sample and get started right away:</span></span>

```
git@github.com:Azure-Samples/active-directory-android-native-oidcandroidlib-v2.git
```

## <a name="register-an-app"></a><span data-ttu-id="7f014-118">앱 등록</span><span class="sxs-lookup"><span data-stu-id="7f014-118">Register an app</span></span>
<span data-ttu-id="7f014-119">Hello에 새 앱 만들기 [응용 프로그램 등록 포털](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), 또는 hello 세부 단계에 따라 [어떻게 tooregister hello v2.0 끝점을 사용 하 여 앱](active-directory-v2-app-registration.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7f014-119">Create a new app at hello [Application registration portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow hello detailed steps at [How tooregister an app with hello v2.0 endpoint](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="7f014-120">다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f014-120">Make sure to:</span></span>

* <span data-ttu-id="7f014-121">복사 hello **응용 프로그램 Id** 할당된 tooyour 응용 프로그램은 곧 필요 하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="7f014-121">Copy hello **Application Id** that's assigned tooyour app because you'll need it soon.</span></span>
* <span data-ttu-id="7f014-122">Hello 추가 **모바일** 응용 프로그램을 위한 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="7f014-122">Add hello **Mobile** platform for your app.</span></span>

> <span data-ttu-id="7f014-123">참고: hello 응용 프로그램 등록 포털에서 제공 된 **리디렉션 URI** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="7f014-123">Note: hello Application registration portal provides a **Redirect URI** value.</span></span> <span data-ttu-id="7f014-124">그러나이 예제에서 사용 해야 hello 기본값인 `https://login.microsoftonline.com/common/oauth2/nativeclient`합니다.</span><span class="sxs-lookup"><span data-stu-id="7f014-124">However, in this example you must use hello default value of `https://login.microsoftonline.com/common/oauth2/nativeclient`.</span></span>
> 
> 

## <a name="download-hello-nxoauth2-third-party-library-and-create-a-workspace"></a><span data-ttu-id="7f014-125">Hello NXOAuth2 타사 라이브러리를 다운로드 하 고 작업 영역 만들기</span><span class="sxs-lookup"><span data-stu-id="7f014-125">Download hello NXOAuth2 third-party library and create a workspace</span></span>
<span data-ttu-id="7f014-126">이 연습에서는 OAuth2 라이브러리인 hello Google의 OpenID Connect 코드에 따라 GitHub에서 OIDCAndroidLib hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f014-126">For this walkthrough, you will use hello OIDCAndroidLib from GitHub, which is an OAuth2 library based on hello OpenID Connect code of Google.</span></span> <span data-ttu-id="7f014-127">Hello 네이티브 응용 프로그램 프로필을 구현 하 고 hello 사용자의 hello 권한 부여 끝점을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f014-127">It implements hello native application profile and supports hello authorization endpoint of hello user.</span></span> <span data-ttu-id="7f014-128">이들은 toointegrate hello Microsoft id 플랫폼을 사용 해야 하는 모든 hello 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7f014-128">These are all hello things that you'll need toointegrate with hello Microsoft identity platform.</span></span>

<span data-ttu-id="7f014-129">Hello OIDCAndroidLib 리포지토리 tooyour 컴퓨터를 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f014-129">Clone hello OIDCAndroidLib repo tooyour computer.</span></span>

```
git@github.com:kalemontes/OIDCAndroidLib.git
```

![androidStudio](../media/active-directory-android-native-oidcandroidlib-v2/emotes-url.png)

## <a name="set-up-your-android-studio-environment"></a><span data-ttu-id="7f014-131">Android Studio 환경 설정</span><span class="sxs-lookup"><span data-stu-id="7f014-131">Set up your Android Studio environment</span></span>
1. <span data-ttu-id="7f014-132">새 Android Studio 프로젝트를 만들고 hello 마법사에서 hello 기본값을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f014-132">Create a new Android Studio project and accept hello defaults in hello wizard.</span></span>
   
    ![Android Studio에서 새 프로젝트 만들기](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample1.PNG)
   
    ![대상 Android 장치](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample2.PNG)
   
    ![활동 toomobile 추가](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample3.PNG)
2. <span data-ttu-id="7f014-136">tooset 프로젝트 모듈을 복제 하는 hello 리포지토리 toohello 프로젝트 위치를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f014-136">tooset up your project modules, move hello cloned repo toohello project location.</span></span> <span data-ttu-id="7f014-137">또한 hello 프로젝트를 만들 수 있으며 다음 복제 직접 toohello 프로젝트 위치 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7f014-137">You can also create hello project and then clone it directly toohello project location.</span></span>
   
    ![프로젝트 모듈](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample4_1.PNG)
3. <span data-ttu-id="7f014-139">Hello 상황에 맞는 메뉴를 사용 하 여 또는 hello Ctrl + Alt + Maj + S 바로 가기를 사용 하 여 hello 프로젝트 모듈 설정을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7f014-139">Open hello project modules settings by using hello context menu or by using hello Ctrl+Alt+Maj+S shortcut.</span></span>
   
    ![프로젝트 모듈 설정](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample4.PNG)
4. <span data-ttu-id="7f014-141">Hello 프로젝트 컨테이너 설정만 하려고 하기 때문에 hello 기본 응용 프로그램 모듈을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f014-141">Remove hello default app module because you only want hello project container settings.</span></span>
   
    ![hello 기본 응용 프로그램 모듈](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample5.PNG)
5. <span data-ttu-id="7f014-143">Hello 복제 된 리포지토리 toohello 현재 프로젝트에서 모듈을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7f014-143">Import modules from hello cloned repo toohello current project.</span></span>
   
    <span data-ttu-id="7f014-144">![Gradle 프로젝트 가져오기](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample6.PNG) ![새 모듈 페이지 만들기](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample7.PNG)</span><span class="sxs-lookup"><span data-stu-id="7f014-144">![Import gradle project](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample6.PNG) ![Create new module page](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample7.PNG)</span></span>
6. <span data-ttu-id="7f014-145">Hello에 대 한 이러한 단계를 반복 `oidlib-sample` 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="7f014-145">Repeat these steps for hello `oidlib-sample` module.</span></span>
7. <span data-ttu-id="7f014-146">Hello에 대 한 hello oidclib 종속성 확인 `oidlib-sample` 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="7f014-146">Check hello oidclib dependencies on hello `oidlib-sample` module.</span></span>
   
    ![hello oidlib 샘플 모듈에 대 한 oidclib 종속성](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample8.PNG)
8. <span data-ttu-id="7f014-148">**확인** 을 클릭하고 Gradle 동기화를 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="7f014-148">Click **OK** and wait for gradle sync.</span></span>
   
    <span data-ttu-id="7f014-149">설정은 gradle처럼 보여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f014-149">Your settings.gradle should look like:</span></span>
   
    ![settings.gradle의 스크린샷](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample8_1.PNG)
9. <span data-ttu-id="7f014-151">Hello 샘플 앱 toomake 있는지 빌드 제대로 실행 되 고 hello 샘플에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f014-151">Build hello sample app toomake sure that hello sample running correctly.</span></span>
   
    <span data-ttu-id="7f014-152">있습니다 수 없습니다 수 toouse이 Azure Active Directory와 아직 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f014-152">You won't be able toouse this with Azure Active Directory yet.</span></span> <span data-ttu-id="7f014-153">해야 tooconfigure 일부 끝점 우선 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f014-153">We'll need tooconfigure some endpoints first.</span></span> <span data-ttu-id="7f014-154">이 hello 샘플 응용 프로그램을 사용자 지정을 시작 하기 전에 Android Studio 문제 없는 tooensure입니다.</span><span class="sxs-lookup"><span data-stu-id="7f014-154">This is tooensure you don't have an Android Studio issues before we start customizing hello sample app.</span></span>
10. <span data-ttu-id="7f014-155">빌드 및 실행 `oidlib-sample` Android Studio에서 hello 대상으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f014-155">Build and run `oidlib-sample` as hello target in Android Studio.</span></span>
    
    ![oidlib-sample 빌드의 진행률](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample9.png)
11. <span data-ttu-id="7f014-157">Hello 삭제 `app ` Android Studio 안전을를 삭제 하지 않으므로 hello 프로젝트에서 hello 모듈을 제거 하는 경우 남아 있는 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="7f014-157">Delete hello `app ` directory that was left when you removed hello module from hello project because Android Studio doesn't delete it for safety.</span></span>
    
    ![Hello 응용 프로그램 디렉터리를 포함 하는 파일 구조](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample12.PNG)
12. <span data-ttu-id="7f014-159">열기 hello **구성 편집** hello 프로젝트에서 hello 모듈을 제거 하는 경우에 두었습니다 메뉴 tooremove 실행 hello 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f014-159">Open hello **Edit Configurations** menu tooremove hello run configuration that was also left when you removed hello module from hello project.</span></span>
    
    <span data-ttu-id="7f014-160">![구성 편집 메뉴](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample10.PNG)
    ![앱의 구성 실행](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample11.PNG)</span><span class="sxs-lookup"><span data-stu-id="7f014-160">![Edit configurations menu](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample10.PNG)
![Run configuration of app](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample11.PNG)</span></span>

## <a name="configure-hello-endpoints-of-hello-sample"></a><span data-ttu-id="7f014-161">Hello 샘플의 hello 끝점 구성</span><span class="sxs-lookup"><span data-stu-id="7f014-161">Configure hello endpoints of hello sample</span></span>
<span data-ttu-id="7f014-162">Hello 했으므로 `oidlib-sample` 성공적으로 실행 편집 일부 끝점 tooget이 Azure Active Directory를이 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f014-162">Now that you have hello `oidlib-sample` running successfully, let's edit some endpoints tooget this working with Azure Active Directory.</span></span>

### <a name="configure-your-client-by-editing-hello-oidcclientconfxml-file"></a><span data-ttu-id="7f014-163">클라이언트 hello oidc_clientconf.xml 파일을 편집 하 여 구성</span><span class="sxs-lookup"><span data-stu-id="7f014-163">Configure your client by editing hello oidc_clientconf.xml file</span></span>
1. <span data-ttu-id="7f014-164">OAuth2 흐름만 tooget 토큰을 사용 하는 hello Graph API를 호출 하므로 hello 클라이언트 toodo OAuth2만 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f014-164">Because you are using OAuth2 flows only tooget a token and call hello Graph API, set hello client toodo OAuth2 only.</span></span> <span data-ttu-id="7f014-165">OIDC에 대해서는 향후 예제에서 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="7f014-165">OIDC will come in a later example.</span></span>
   
    ```xml
        <bool name="oidc_oauth2only">true</bool>
    ```
2. <span data-ttu-id="7f014-166">Hello 등록 포털에서 받은 클라이언트 ID를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f014-166">Configure your client ID that you received from hello registration portal.</span></span>
   
    ```xml
        <string name="oidc_clientId">86172f9d-a1ae-4348-aafa-7b3e5d1b36f5</string>
        <string name="oidc_clientSecret"></string>
    ```
3. <span data-ttu-id="7f014-167">아래 하나 hello로 리디렉션 URI를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f014-167">Configure your redirect URI with hello one below.</span></span>
   
    ```xml
        <string name="oidc_redirectUrl">https://login.microsoftonline.com/common/oauth2/nativeclient</string>
    ```
4. <span data-ttu-id="7f014-168">범위는 하면 필요한 순서 tooaccess에 hello Graph API를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f014-168">Configure your scopes that you need in order tooaccess hello Graph API.</span></span>
   
    ```xml
        <string-array name="oidc_scopes">
            <item>openid</item>
            <item>https://graph.microsoft.com/User.Read</item>
            <item>offline_access</item>
        </string-array>
    ```

<span data-ttu-id="7f014-169">hello `User.Read` 값 `oidc_scopes` 있습니다 tooread hello 기본 프로필 hello 사용자 로그인을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f014-169">hello `User.Read` value in `oidc_scopes` allows you tooread hello basic profile hello signed in user.</span></span>
<span data-ttu-id="7f014-170">모든 hello 사용할 수 있는 범위에 대해 자세히 알아볼 수 있습니다 [Microsoft Graph 사용 권한 범위](https://graph.microsoft.io/docs/authorization/permission_scopes)합니다.</span><span class="sxs-lookup"><span data-stu-id="7f014-170">You can learn more about all hello available scopes at [Microsoft Graph permission scopes](https://graph.microsoft.io/docs/authorization/permission_scopes).</span></span>

<span data-ttu-id="7f014-171">`openid` 또는 `offline_access`를 OpenID Connect의 범위로 구분해서 설명하는 내용을 보려면, [2.0 프로토콜 - OAuth 2.0 권한 부여 코드 흐름](active-directory-v2-protocols-oauth-code.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7f014-171">If you'd like explanations about `openid` or `offline_access` as scopes in OpenID Connect, see [2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md).</span></span>

### <a name="configure-your-client-endpoints-by-editing-hello-oidcendpointsxml-file"></a><span data-ttu-id="7f014-172">Hello oidc_endpoints.xml 파일을 편집 하 여 클라이언트 끝점 구성</span><span class="sxs-lookup"><span data-stu-id="7f014-172">Configure your client endpoints by editing hello oidc_endpoints.xml file</span></span>
* <span data-ttu-id="7f014-173">열기 hello `oidc_endpoints.xml` 파일을 hello 다음 변경 내용을 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="7f014-173">Open hello `oidc_endpoints.xml` file and make hello following changes:</span></span>
  
    ```xml
    <!-- Stores OpenID Connect provider endpoints. -->
    <resources>
        <string name="op_authorizationEnpoint">https://login.microsoftonline.com/common/oauth2/v2.0/authorize</string>
        <string name="op_tokenEndpoint">https://login.microsoftonline.com/common/oauth2/v2.0/token</string>
        <string name="op_userInfoEndpoint">https://www.example.com/oauth2/userinfo</string>
        <string name="op_revocationEndpoint">https://www.example.com/oauth2/revoketoken</string>
    </resources>
    ```

<span data-ttu-id="7f014-174">OAuth2를 프로토콜로 사용하는 경우 이러한 끝점은 변경되어서는 안됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f014-174">These endpoints should never change if you are using OAuth2 as your protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="7f014-175">에 대 한 끝점 hello `userInfoEndpoint` 및 `revocationEndpoint` Azure Active Directory에서 현재 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7f014-175">hello endpoints for `userInfoEndpoint` and `revocationEndpoint` are currently not supported by Azure Active Directory.</span></span> <span data-ttu-id="7f014-176">Hello example.com 기본값을 가진 두면 알려줍니다는 사용할 수 없는 경우 hello 샘플:-)</span><span class="sxs-lookup"><span data-stu-id="7f014-176">If you leave these with hello default example.com value, you will be reminded that they are not available in hello sample :-)</span></span>
> 
> 

## <a name="configure-a-graph-api-call"></a><span data-ttu-id="7f014-177">Graph API 호출 구성</span><span class="sxs-lookup"><span data-stu-id="7f014-177">Configure a Graph API call</span></span>
* <span data-ttu-id="7f014-178">열기 hello `HomeActivity.java` 파일을 hello 다음 변경 내용을 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="7f014-178">Open hello `HomeActivity.java` file and make hello following changes:</span></span>
  
    ```Java
       //TODO: set your protected resource url
        private static final String protectedResUrl = "https://graph.microsoft.com/v1.0/me/";
    ```

<span data-ttu-id="7f014-179">여기에 나오는 간단한 Graph API 호출이 예제 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="7f014-179">Here a simple Graph API call returns our information.</span></span>

<span data-ttu-id="7f014-180">Toodo 해야 하는 모든 hello 변경 내용을 모두입니다.</span><span class="sxs-lookup"><span data-stu-id="7f014-180">Those are all hello changes that you need toodo.</span></span> <span data-ttu-id="7f014-181">Hello 실행 `oidlib-sample` 응용 프로그램을 마우스 클릭 **로그인**합니다.</span><span class="sxs-lookup"><span data-stu-id="7f014-181">Run hello `oidlib-sample` application, and click **Sign in**.</span></span>

<span data-ttu-id="7f014-182">성공적으로 인증 한 후 선택 hello **보호 된 리소스 요청** tootest 프로그램 호출 toohello Graph API 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="7f014-182">After you've successfully authenticated, select hello **Request Protected Resource** button tootest your call toohello Graph API.</span></span>

## <a name="get-security-updates-for-our-product"></a><span data-ttu-id="7f014-183">당사 제품에 대한 보안 업데이트 가져오기</span><span class="sxs-lookup"><span data-stu-id="7f014-183">Get security updates for our product</span></span>
<span data-ttu-id="7f014-184">사용자는 좋습니다 보안 사고에 대 한 알림을 tooget hello를 방문 하 여 [보안 TechCenter](https://technet.microsoft.com/security/dd252948) 및 tooSecurity 자문 경고를 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f014-184">We encourage you tooget notifications about security incidents by visiting hello [Security TechCenter](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>


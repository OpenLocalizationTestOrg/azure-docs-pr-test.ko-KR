---
title: "Azure Active Directory v2.0 Android 앱 | Microsoft Docs"
description: "개인 Microsoft 계정과 회사 또는 학교 계정이 있는 사용자로 로그인하고 타사 라이브러리를 사용하여 Graph API를 호출하는 Android 앱을 빌드하는 방법입니다."
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
ms.openlocfilehash: c0a5a818c61f7af7ff04bf890b54e8364f3b21b1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-to-an-android-app-using-a-third-party-library-with-graph-api-using-the-v20-endpoint"></a><span data-ttu-id="e84a3-103">v2.0 끝점을 사용하는 Graph API와 함께 타사 라이브러리를 사용하여 Android 앱에 로그인 추가</span><span class="sxs-lookup"><span data-stu-id="e84a3-103">Add sign-in to an Android app using a third-party library with Graph API using the v2.0 endpoint</span></span>
<span data-ttu-id="e84a3-104">Microsoft ID 플랫폼은 OAuth2 및 OpenID Connect와 같은 개방형 표준을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e84a3-104">The Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="e84a3-105">개발자는 서비스와 통합하려는 모든 라이브러리를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e84a3-105">Developers can use any library they want to integrate with our services.</span></span> <span data-ttu-id="e84a3-106">개발자가 플랫폼을 다른 라이브러리와 함께 사용할 수 있도록 돕기 위해, 타사 라이브러리를 Microsoft ID 플랫폼에 연결하도록 구성하는 방법을 설명하는 이와 같은 연습 몇 가지를 작성했습니다.</span><span class="sxs-lookup"><span data-stu-id="e84a3-106">To help developers use our platform with other libraries, we've written a few walkthroughs like this one to demonstrate how to configure third-party libraries to connect to the Microsoft identity platform.</span></span> <span data-ttu-id="e84a3-107">[RFC6749 OAuth2 사양](https://tools.ietf.org/html/rfc6749) 을 구현하는 대부분의 라이브러리는 Microsoft ID 플랫폼에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e84a3-107">Most libraries that implement [the RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) can connect to the Microsoft identity platform.</span></span>

<span data-ttu-id="e84a3-108">이 연습에서 만드는 응용 프로그램을 사용하여 해당 조직에 로그인한 다음 Graph API를 사용하여 조직에서 자신을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e84a3-108">With the application that this walkthrough creates, users can sign in to their organization and then search for themselves in their organization by using the Graph API.</span></span>

<span data-ttu-id="e84a3-109">OAuth2 또는 OpenID Connect를 처음 접하는 경우 이 샘플 구성 대부분이 잘 이해되지 않을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e84a3-109">If you're new to OAuth2 or OpenID Connect, much of this sample configuration may not make sense to you.</span></span> <span data-ttu-id="e84a3-110">배경 지식을 위해 [2.0 프로토콜 - OAuth 2.0 권한 부여 코드 흐름](active-directory-v2-protocols-oauth-code.md)을 읽어보는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e84a3-110">We recommend that you read [2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md) for background.</span></span>

> [!NOTE]
> <span data-ttu-id="e84a3-111">조건부 액세스 및 Intune 정책 관리 등과 같은 OAuth2 또는 OpenID Connect 표준의 식을 사용하는 플랫폼의 일부 기능은 수행하려면 오픈 소스인 Microsoft Azure ID 라이브러리를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e84a3-111">Some features of our platform that do have an expression in the OAuth2 or OpenID Connect standards, such as Conditional Access and Intune policy management, require you to use our open source Microsoft Azure Identity Libraries.</span></span>
> 
> 

<span data-ttu-id="e84a3-112">v2.0 끝점에서는 일부 Azure Active Directory 시나리오 및 기능만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="e84a3-112">The v2.0 endpoint does not support all Azure Active Directory scenarios and features.</span></span>

> [!NOTE]
> <span data-ttu-id="e84a3-113">v2.0 끝점을 사용해야 하는지 확인하려면 [v2.0 제한 사항](active-directory-v2-limitations.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e84a3-113">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download-the-code-from-github"></a><span data-ttu-id="e84a3-114">GitHub에서 코드 다운로드</span><span class="sxs-lookup"><span data-stu-id="e84a3-114">Download the code from GitHub</span></span>
<span data-ttu-id="e84a3-115">이 자습서에 대한 코드는 [GitHub](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2)에서 유지 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="e84a3-115">The code for this tutorial is maintained [on GitHub](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2).</span></span>  <span data-ttu-id="e84a3-116">자습서에 따라 [.zip으로 앱 구조를 다운로드](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2/archive/skeleton.zip) 하거나 구조를 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e84a3-116">To follow along, you can  [download the app's skeleton as a .zip](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2/archive/skeleton.zip) or clone the skeleton:</span></span>

```
git clone --branch skeleton git@github.com:Azure-Samples/active-directory-android-native-oidcandroidlib-v2.git
```

<span data-ttu-id="e84a3-117">샘플을 다운로드할 수도 있고 지금 바로 시작할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e84a3-117">You can also just download the sample and get started right away:</span></span>

```
git@github.com:Azure-Samples/active-directory-android-native-oidcandroidlib-v2.git
```

## <a name="register-an-app"></a><span data-ttu-id="e84a3-118">앱 등록</span><span class="sxs-lookup"><span data-stu-id="e84a3-118">Register an app</span></span>
<span data-ttu-id="e84a3-119">[응용 프로그램 등록 포털](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)에서 새 앱을 만들거나 [v2.0 끝점을 사용하여 앱을 등록하는 방법](active-directory-v2-app-registration.md)의 자세한 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="e84a3-119">Create a new app at the [Application registration portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow the detailed steps at [How to register an app with the v2.0 endpoint](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="e84a3-120">다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e84a3-120">Make sure to:</span></span>

* <span data-ttu-id="e84a3-121">앱에 할당된 **응용 프로그램 ID** 는 곧 필요하므로 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="e84a3-121">Copy the **Application Id** that's assigned to your app because you'll need it soon.</span></span>
* <span data-ttu-id="e84a3-122">앱용 **Mobile** 플랫폼을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e84a3-122">Add the **Mobile** platform for your app.</span></span>

> <span data-ttu-id="e84a3-123">참고: 응용 프로그램 등록 포털은 **리디렉션 URI** 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e84a3-123">Note: The Application registration portal provides a **Redirect URI** value.</span></span> <span data-ttu-id="e84a3-124">그러나 이 예제에서 `https://login.microsoftonline.com/common/oauth2/nativeclient`의 기본값을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e84a3-124">However, in this example you must use the default value of `https://login.microsoftonline.com/common/oauth2/nativeclient`.</span></span>
> 
> 

## <a name="download-the-nxoauth2-third-party-library-and-create-a-workspace"></a><span data-ttu-id="e84a3-125">NXOAuth2 타사 라이브러리 다운로드 및 작업 영역 만들기</span><span class="sxs-lookup"><span data-stu-id="e84a3-125">Download the NXOAuth2 third-party library and create a workspace</span></span>
<span data-ttu-id="e84a3-126">이 연습에서는 Google의 OpenID Connect 코드를 기반으로 하는 OAuth2 라이브러리인 GitHub의 OIDCAndroidLib을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e84a3-126">For this walkthrough, you will use the OIDCAndroidLib from GitHub, which is an OAuth2 library based on the OpenID Connect code of Google.</span></span> <span data-ttu-id="e84a3-127">네이티브 응용 프로그램 프로필을 구현하고 사용자의 권한 부여 끝점을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="e84a3-127">It implements the native application profile and supports the authorization endpoint of the user.</span></span> <span data-ttu-id="e84a3-128">이것이 바로 Microsoft ID 플랫폼과 통합하기 위해 필요한 모든 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e84a3-128">These are all the things that you'll need to integrate with the Microsoft identity platform.</span></span>

<span data-ttu-id="e84a3-129">컴퓨터에 OIDCAndroidLib 리포지토리를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="e84a3-129">Clone the OIDCAndroidLib repo to your computer.</span></span>

```
git@github.com:kalemontes/OIDCAndroidLib.git
```

![androidStudio](../media/active-directory-android-native-oidcandroidlib-v2/emotes-url.png)

## <a name="set-up-your-android-studio-environment"></a><span data-ttu-id="e84a3-131">Android Studio 환경 설정</span><span class="sxs-lookup"><span data-stu-id="e84a3-131">Set up your Android Studio environment</span></span>
1. <span data-ttu-id="e84a3-132">새 Android Studio 프로젝트를 만들고 마법사의 기본값을 그대로 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="e84a3-132">Create a new Android Studio project and accept the defaults in the wizard.</span></span>
   
    ![Android Studio에서 새 프로젝트 만들기](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample1.PNG)
   
    ![대상 Android 장치](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample2.PNG)
   
    ![모바일에 작업 추가](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample3.PNG)
2. <span data-ttu-id="e84a3-136">프로젝트 모듈을 설정하려면 복제된 리포지토리를 프로젝트 위치로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e84a3-136">To set up your project modules, move the cloned repo to the project location.</span></span> <span data-ttu-id="e84a3-137">또한 프로젝트를 만든 다음 프로젝트 위치로 직접 복제할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e84a3-137">You can also create the project and then clone it directly to the project location.</span></span>
   
    ![프로젝트 모듈](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample4_1.PNG)
3. <span data-ttu-id="e84a3-139">상황에 맞는 메뉴를 사용하거나 Ctrl+Alt+Maj+S 바로 가기를 사용하여 프로젝트 모듈 설정을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e84a3-139">Open the project modules settings by using the context menu or by using the Ctrl+Alt+Maj+S shortcut.</span></span>
   
    ![프로젝트 모듈 설정](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample4.PNG)
4. <span data-ttu-id="e84a3-141">프로젝트 컨테이너 설정만 원한다면 기본 앱 모듈을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="e84a3-141">Remove the default app module because you only want the project container settings.</span></span>
   
    ![기본 앱 모듈](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample5.PNG)
5. <span data-ttu-id="e84a3-143">모듈을 복제 리포지토리에서 현재 프로젝트로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e84a3-143">Import modules from the cloned repo to the current project.</span></span>
   
    <span data-ttu-id="e84a3-144">![Gradle 프로젝트 가져오기](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample6.PNG) ![새 모듈 페이지 만들기](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample7.PNG)</span><span class="sxs-lookup"><span data-stu-id="e84a3-144">![Import gradle project](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample6.PNG) ![Create new module page](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample7.PNG)</span></span>
6. <span data-ttu-id="e84a3-145">`oidlib-sample` 모듈에 대해 이들 단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="e84a3-145">Repeat these steps for the `oidlib-sample` module.</span></span>
7. <span data-ttu-id="e84a3-146">`oidlib-sample` 모듈에서 Oidclib 종속성을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e84a3-146">Check the oidclib dependencies on the `oidlib-sample` module.</span></span>
   
    ![oidlib-sample 모듈의 Oidclib 종속성](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample8.PNG)
8. <span data-ttu-id="e84a3-148">**확인** 을 클릭하고 Gradle 동기화를 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="e84a3-148">Click **OK** and wait for gradle sync.</span></span>
   
    <span data-ttu-id="e84a3-149">설정은 gradle처럼 보여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e84a3-149">Your settings.gradle should look like:</span></span>
   
    ![settings.gradle의 스크린샷](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample8_1.PNG)
9. <span data-ttu-id="e84a3-151">샘플 앱을 빌드하여 샘플이 제대로 실행되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e84a3-151">Build the sample app to make sure that the sample running correctly.</span></span>
   
    <span data-ttu-id="e84a3-152">아직은 이것을 Azure Active Directory와 함께 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e84a3-152">You won't be able to use this with Azure Active Directory yet.</span></span> <span data-ttu-id="e84a3-153">먼저 일부 끝점을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e84a3-153">We'll need to configure some endpoints first.</span></span> <span data-ttu-id="e84a3-154">이는 샘플 앱을 사용자에 맞게 설정하기 전에 Android Studio 문제가 없도록 하기 위해서입니다.</span><span class="sxs-lookup"><span data-stu-id="e84a3-154">This is to ensure you don't have an Android Studio issues before we start customizing the sample app.</span></span>
10. <span data-ttu-id="e84a3-155">`oidlib-sample` 을 Android Studio의 대상으로 빌드하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e84a3-155">Build and run `oidlib-sample` as the target in Android Studio.</span></span>
    
    ![oidlib-sample 빌드의 진행률](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample9.png)
11. <span data-ttu-id="e84a3-157">프로젝트에서 모듈을 제거할 때 AndroidStudio가 안전을 위해 삭제하지 않아 남은 `app ` 디렉터리를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="e84a3-157">Delete the `app ` directory that was left when you removed the module from the project because Android Studio doesn't delete it for safety.</span></span>
    
    ![앱 디렉터리를 포함하는 파일 구조](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample12.PNG)
12. <span data-ttu-id="e84a3-159">또한 **구성 편집** 메뉴를 열어 프로젝트에서 모듈을 제거할 때 남겨진 실행 구성도 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e84a3-159">Open the **Edit Configurations** menu to remove the run configuration that was also left when you removed the module from the project.</span></span>
    
    <span data-ttu-id="e84a3-160">![구성 편집 메뉴](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample10.PNG)
    ![앱의 구성 실행](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample11.PNG)</span><span class="sxs-lookup"><span data-stu-id="e84a3-160">![Edit configurations menu](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample10.PNG)
![Run configuration of app](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample11.PNG)</span></span>

## <a name="configure-the-endpoints-of-the-sample"></a><span data-ttu-id="e84a3-161">샘플의 끝점 구성</span><span class="sxs-lookup"><span data-stu-id="e84a3-161">Configure the endpoints of the sample</span></span>
<span data-ttu-id="e84a3-162">이제 `oidlib-sample`이 성공적으로 실행됨으로 Azure Active Directory와 작동되도록 일부 끝점을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="e84a3-162">Now that you have the `oidlib-sample` running successfully, let's edit some endpoints to get this working with Azure Active Directory.</span></span>

### <a name="configure-your-client-by-editing-the-oidcclientconfxml-file"></a><span data-ttu-id="e84a3-163">oidc_clientconf.xml 파일을 편집하여 클라이언트 구성</span><span class="sxs-lookup"><span data-stu-id="e84a3-163">Configure your client by editing the oidc_clientconf.xml file</span></span>
1. <span data-ttu-id="e84a3-164">토큰을 가져오고 Graph API를 호출하기 위해 OAuth2 흐름만 사용하기 때문에 OAuth2만 수행하도록 클라이언트를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e84a3-164">Because you are using OAuth2 flows only to get a token and call the Graph API, set the client to do OAuth2 only.</span></span> <span data-ttu-id="e84a3-165">OIDC에 대해서는 향후 예제에서 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="e84a3-165">OIDC will come in a later example.</span></span>
   
    ```xml
        <bool name="oidc_oauth2only">true</bool>
    ```
2. <span data-ttu-id="e84a3-166">등록 포털에서 받은 클라이언트 ID를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="e84a3-166">Configure your client ID that you received from the registration portal.</span></span>
   
    ```xml
        <string name="oidc_clientId">86172f9d-a1ae-4348-aafa-7b3e5d1b36f5</string>
        <string name="oidc_clientSecret"></string>
    ```
3. <span data-ttu-id="e84a3-167">아래의 ID로 리디렉션 URI를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="e84a3-167">Configure your redirect URI with the one below.</span></span>
   
    ```xml
        <string name="oidc_redirectUrl">https://login.microsoftonline.com/common/oauth2/nativeclient</string>
    ```
4. <span data-ttu-id="e84a3-168">Graph API에 액세스하기 위해 필요한 범위를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="e84a3-168">Configure your scopes that you need in order to access the Graph API.</span></span>
   
    ```xml
        <string-array name="oidc_scopes">
            <item>openid</item>
            <item>https://graph.microsoft.com/User.Read</item>
            <item>offline_access</item>
        </string-array>
    ```

<span data-ttu-id="e84a3-169">`oidc_scopes`의 `User.Read` 값을 사용하여 로그인한 사용자의 기본 프로필을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e84a3-169">The `User.Read` value in `oidc_scopes` allows you to read the basic profile the signed in user.</span></span>
<span data-ttu-id="e84a3-170">[Microsoft Graph 권한 범위](https://graph.microsoft.io/docs/authorization/permission_scopes)에서 사용 가능한 모든 범위에 대해 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e84a3-170">You can learn more about all the available scopes at [Microsoft Graph permission scopes](https://graph.microsoft.io/docs/authorization/permission_scopes).</span></span>

<span data-ttu-id="e84a3-171">`openid` 또는 `offline_access`를 OpenID Connect의 범위로 구분해서 설명하는 내용을 보려면, [2.0 프로토콜 - OAuth 2.0 권한 부여 코드 흐름](active-directory-v2-protocols-oauth-code.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e84a3-171">If you'd like explanations about `openid` or `offline_access` as scopes in OpenID Connect, see [2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md).</span></span>

### <a name="configure-your-client-endpoints-by-editing-the-oidcendpointsxml-file"></a><span data-ttu-id="e84a3-172">oidc_endpoints.xml 파일을 편집하여 클라이언트 끝점 구성</span><span class="sxs-lookup"><span data-stu-id="e84a3-172">Configure your client endpoints by editing the oidc_endpoints.xml file</span></span>
* <span data-ttu-id="e84a3-173">`oidc_endpoints.xml` 파일을 열어 다음과 같이 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="e84a3-173">Open the `oidc_endpoints.xml` file and make the following changes:</span></span>
  
    ```xml
    <!-- Stores OpenID Connect provider endpoints. -->
    <resources>
        <string name="op_authorizationEnpoint">https://login.microsoftonline.com/common/oauth2/v2.0/authorize</string>
        <string name="op_tokenEndpoint">https://login.microsoftonline.com/common/oauth2/v2.0/token</string>
        <string name="op_userInfoEndpoint">https://www.example.com/oauth2/userinfo</string>
        <string name="op_revocationEndpoint">https://www.example.com/oauth2/revoketoken</string>
    </resources>
    ```

<span data-ttu-id="e84a3-174">OAuth2를 프로토콜로 사용하는 경우 이러한 끝점은 변경되어서는 안됩니다.</span><span class="sxs-lookup"><span data-stu-id="e84a3-174">These endpoints should never change if you are using OAuth2 as your protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="e84a3-175">`userInfoEndpoint` 및 `revocationEndpoint`에 대한 끝점은 현재 Azure Active Directory에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e84a3-175">The endpoints for `userInfoEndpoint` and `revocationEndpoint` are currently not supported by Azure Active Directory.</span></span> <span data-ttu-id="e84a3-176">이러한 기본 example.com 값 상태로 두면 샘플에서 사용할 수 없다는 것에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="e84a3-176">If you leave these with the default example.com value, you will be reminded that they are not available in the sample :-)</span></span>
> 
> 

## <a name="configure-a-graph-api-call"></a><span data-ttu-id="e84a3-177">Graph API 호출 구성</span><span class="sxs-lookup"><span data-stu-id="e84a3-177">Configure a Graph API call</span></span>
* <span data-ttu-id="e84a3-178">`HomeActivity.java` 파일을 열어 다음과 같이 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="e84a3-178">Open the `HomeActivity.java` file and make the following changes:</span></span>
  
    ```Java
       //TODO: set your protected resource url
        private static final String protectedResUrl = "https://graph.microsoft.com/v1.0/me/";
    ```

<span data-ttu-id="e84a3-179">여기에 나오는 간단한 Graph API 호출이 예제 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="e84a3-179">Here a simple Graph API call returns our information.</span></span>

<span data-ttu-id="e84a3-180">여기에 나오는 내용만 변경하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e84a3-180">Those are all the changes that you need to do.</span></span> <span data-ttu-id="e84a3-181">`oidlib-sample` 응용 프로그램을 실행하고 **로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e84a3-181">Run the `oidlib-sample` application, and click **Sign in**.</span></span>

<span data-ttu-id="e84a3-182">성공적으로 인증했으므로 Graph API로 호출을 테스트하려면 **보호된 리소스 요청** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e84a3-182">After you've successfully authenticated, select the **Request Protected Resource** button to test your call to the Graph API.</span></span>

## <a name="get-security-updates-for-our-product"></a><span data-ttu-id="e84a3-183">당사 제품에 대한 보안 업데이트 가져오기</span><span class="sxs-lookup"><span data-stu-id="e84a3-183">Get security updates for our product</span></span>
<span data-ttu-id="e84a3-184">[Security TechCenter](https://technet.microsoft.com/security/dd252948) 를 방문해서 보안 공지 경고를 구독하여 보안 사건이 발생할 때 알림을 받는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e84a3-184">We encourage you to get notifications about security incidents by visiting the [Security TechCenter](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>


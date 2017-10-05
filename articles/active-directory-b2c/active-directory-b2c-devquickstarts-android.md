---
title: "Azure Active Directory B2C: Android 응용 프로그램을 사용하여 토큰 가져오기 | Microsoft Docs"
description: "이 문서에서는 Azure Active Directory B2C와 함께 AppAuth를 사용하는 Android 앱을 만들어 사용자 ID를 관리하고 사용자를 인증하는 방법을 보여 줍니다."
services: active-directory-b2c
documentationcenter: android
author: parakhj
manager: krassk
editor: 
ms.assetid: d00947c3-dcaa-4cb3-8c2e-d94e0746d8b2
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 03/06/2017
ms.author: parakhj
ms.openlocfilehash: cd4b8048245be49ea79bcb1b364f2f99c56f8291
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-ad-b2c-sign-in-using-an-android-application"></a><span data-ttu-id="a1b31-103">Azure AD B2C: Android 응용 프로그램을 사용하여 로그인</span><span class="sxs-lookup"><span data-stu-id="a1b31-103">Azure AD B2C: Sign-in using an Android application</span></span>

<span data-ttu-id="a1b31-104">Microsoft ID 플랫폼은 OAuth2 및 OpenID Connect와 같은 개방형 표준을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a1b31-104">The Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="a1b31-105">이를 통해 개발자는 서비스와 통합하려는 모든 라이브러리를 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1b31-105">This allows developers to leverage any library they wish to integrate with our services.</span></span> <span data-ttu-id="a1b31-106">개발자가 플랫폼을 다른 라이브러리와 함께 사용할 수 있도록 돕기 위해, 타사 라이브러리를 Microsoft ID 플랫폼에 연결하도록 구성하는 방법을 설명하는 이와 같은 연습 몇 가지를 마련했습니다.</span><span class="sxs-lookup"><span data-stu-id="a1b31-106">To aid developers in using our platform with other libraries, we've written a few walkthroughs like this one to demonstrate how to configure 3rd party libraries to connect to the Microsoft identity platform.</span></span> <span data-ttu-id="a1b31-107">[RFC6749 OAuth2 사양](https://tools.ietf.org/html/rfc6749)을 구현하는 대부분의 라이브러리는 Microsoft ID 플랫폼에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1b31-107">Most libraries that implement [the RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) will be able to connect to the Microsoft Identity platform.</span></span>

> [!WARNING]
> <span data-ttu-id="a1b31-108">Microsoft는 타사 라이브러리에 대한 수정 사항을 제공하지 않으며 이러한 라이브러리의 검토를 완료하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="a1b31-108">Microsoft does not provide fixes for 3rd party libraries and has not done a review of those libraries.</span></span> <span data-ttu-id="a1b31-109">이 샘플은 기본 시나리오에서 Azure AD B2C와의 호환성이 테스트된 AppAuth라는 타사 라이브러리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a1b31-109">This sample is using a 3rd party library called AppAuth that has been tested for compatibility in basic scenarios with the Azure AD B2C.</span></span> <span data-ttu-id="a1b31-110">문제 및 기능 요청은 라이브러리의 오픈 소스 프로젝트로 리디렉션되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1b31-110">Issues and feature requests should be directed to the library's open-source project.</span></span> <span data-ttu-id="a1b31-111">자세한 내용은 [이 문서](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a1b31-111">Please see [this article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries) for more information.</span></span>  
>
>

<span data-ttu-id="a1b31-112">OAuth2 또는 OpenID Connect를 처음 접하는 경우 이 샘플 구성 대부분이 잘 이해되지 않을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1b31-112">If you're new to OAuth2 or OpenID Connect much of this sample configuration may not make much sense to you.</span></span> <span data-ttu-id="a1b31-113">[여기서 추천한 프로토콜에 관한 개요](active-directory-b2c-reference-protocols.md)를 간략히 살펴볼 것을 추천합니다.</span><span class="sxs-lookup"><span data-stu-id="a1b31-113">We recommend you look at a brief [overview of the protocol we've documented here](active-directory-b2c-reference-protocols.md).</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="a1b31-114">Azure AD B2C 디렉터리 가져오기</span><span class="sxs-lookup"><span data-stu-id="a1b31-114">Get an Azure AD B2C directory</span></span>

<span data-ttu-id="a1b31-115">Azure AD B2C를 사용하기 전에 디렉터리 또는 테넌트를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1b31-115">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="a1b31-116">디렉터리는 모든 사용자, 앱, 그룹 등을 위한 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="a1b31-116">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="a1b31-117">디렉터리가 없는 경우 계속하기 전에 [B2C 디렉터리를 만듭니다](active-directory-b2c-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="a1b31-117">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="a1b31-118">응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="a1b31-118">Create an application</span></span>

<span data-ttu-id="a1b31-119">다음으로 B2C 디렉터리에서 앱을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1b31-119">Next, you need to create an app in your B2C directory.</span></span> <span data-ttu-id="a1b31-120">앱과 안전하게 통신하는 데 필요한 Azure AD 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a1b31-120">This gives Azure AD information that it needs to communicate securely with your app.</span></span> <span data-ttu-id="a1b31-121">모바일 앱을 만들려면 [이러한 지침](active-directory-b2c-app-registration.md)에 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="a1b31-121">To create a mobile app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="a1b31-122">다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1b31-122">Be sure to:</span></span>

* <span data-ttu-id="a1b31-123">응용 프로그램에 **네이티브 클라이언트**를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a1b31-123">Include a **Native Client** in the application.</span></span>
* <span data-ttu-id="a1b31-124">앱에 할당된 **응용 프로그램 ID**를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="a1b31-124">Copy the **Application ID** that is assigned to your app.</span></span> <span data-ttu-id="a1b31-125">이 ID는 나중에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a1b31-125">You will need this later.</span></span>
* <span data-ttu-id="a1b31-126">네이티브 클라이언트 **리디렉션 URI**(예: com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect)를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a1b31-126">Set up a native client **Redirect URI** (e.g. com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span></span> <span data-ttu-id="a1b31-127">이 ID는 나중에도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a1b31-127">You will also need this later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="a1b31-128">정책 만들기</span><span class="sxs-lookup"><span data-stu-id="a1b31-128">Create your policies</span></span>

<span data-ttu-id="a1b31-129">Azure AD B2C에서 모든 사용자 환경은 [정책](active-directory-b2c-reference-policies.md)에 의해 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1b31-129">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="a1b31-130">이 앱은 결합된 로그인 및 등록의 하나의 ID 환경을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a1b31-130">This app contains one identity experience: a combined sign-in and sign-up.</span></span> <span data-ttu-id="a1b31-131">[정책 참조 문서](active-directory-b2c-reference-policies.md#create-a-sign-up-policy)에서 설명한 대로 이 정책을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1b31-131">You need to create this policy, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="a1b31-132">정책을 만들 때 다음을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a1b31-132">When you create the policy, be sure to:</span></span>

* <span data-ttu-id="a1b31-133">정책에서 **표시 이름**을 등록 특성으로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a1b31-133">Choose the **Display name** as a sign-up attribute in your policy.</span></span>
* <span data-ttu-id="a1b31-134">모든 정책에서 **표시 이름** 및 **개체 ID** 응용 프로그램 클레임을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a1b31-134">Choose the **Display name** and **Object ID** application claims in every policy.</span></span> <span data-ttu-id="a1b31-135">물론 다른 클레임을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1b31-135">You can choose other claims as well.</span></span>
* <span data-ttu-id="a1b31-136">각 정책을 만든 후에 **이름**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="a1b31-136">Copy the **Name** of each policy after you create it.</span></span> <span data-ttu-id="a1b31-137">접두사 `b2c_1_`이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1b31-137">It should have the prefix `b2c_1_`.</span></span>  <span data-ttu-id="a1b31-138">정책 이름이 나중에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a1b31-138">You'll need the policy name later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="a1b31-139">정책을 만들었다면 앱을 빌드할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a1b31-139">After you have created your policies, you're ready to build your app.</span></span>

## <a name="download-the-sample-code"></a><span data-ttu-id="a1b31-140">샘플 코드 다운로드</span><span class="sxs-lookup"><span data-stu-id="a1b31-140">Download the sample code</span></span>

<span data-ttu-id="a1b31-141">[GitHub에서](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c) Azure AD B2C와 함께 AppAuth를 사용하는 작업 샘플이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1b31-141">We have provided a working sample that uses AppAuth with Azure AD B2C [on GitHub](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span></span> <span data-ttu-id="a1b31-142">코드를 다운로드하고 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1b31-142">You can download the code and run it.</span></span> <span data-ttu-id="a1b31-143">[README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md)의 지침에 따라 사용자 고유의 Azure AD B2C 구성을 사용하는 자신만의 앱으로 빠르게 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1b31-143">You can quickly get started with your own app using your own Azure AD B2C configuration by following the instructions in the [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md).</span></span>

<span data-ttu-id="a1b31-144">샘플은 [AppAuth](https://openid.github.io/AppAuth-Android/)에서 제공되는 샘플의 수정본입니다.</span><span class="sxs-lookup"><span data-stu-id="a1b31-144">The sample is a modification of the sample provided by [AppAuth](https://openid.github.io/AppAuth-Android/).</span></span> <span data-ttu-id="a1b31-145">AppAuth 및 기능에 대한 자세한 정보는 해당 페이지를 방문해 보세요.</span><span class="sxs-lookup"><span data-stu-id="a1b31-145">Please visit their page to learn more about AppAuth and its features.</span></span>

## <a name="modifying-your-app-to-use-azure-ad-b2c-with-appauth"></a><span data-ttu-id="a1b31-146">AppAuth와 함께 Azure AD B2C를 사용하도록 앱 수정</span><span class="sxs-lookup"><span data-stu-id="a1b31-146">Modifying your app to use Azure AD B2C with AppAuth</span></span>

> [!NOTE]
> <span data-ttu-id="a1b31-147">AppAuth는 Android API 16(Jellybean) 이상을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="a1b31-147">AppAuth supports Android API 16 (Jellybean) and above.</span></span> <span data-ttu-id="a1b31-148">API 23 이상을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a1b31-148">We recommend using API 23 and above.</span></span>
>

### <a name="configuration"></a><span data-ttu-id="a1b31-149">구성</span><span class="sxs-lookup"><span data-stu-id="a1b31-149">Configuration</span></span>

<span data-ttu-id="a1b31-150">검색 URI를 지정하거나 권한 부여 끝점과 토큰 끝점 URI를 모두 지정하여 Azure AD B2C와의 통신을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1b31-150">You can configure communication with Azure AD B2C by either specifying the discovery URI or by specifying both the authorization endpoint and token endpoint URIs.</span></span> <span data-ttu-id="a1b31-151">두 경우 모두 다음 정보를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1b31-151">In either case, you will need the following information:</span></span>

* <span data-ttu-id="a1b31-152">테넌트 ID(예: contoso.onmicrosoft.com)</span><span class="sxs-lookup"><span data-stu-id="a1b31-152">Tenant ID (e.g. contoso.onmicrosoft.com)</span></span>
* <span data-ttu-id="a1b31-153">정책 이름(예: B2C\_1\_SignUpIn)</span><span class="sxs-lookup"><span data-stu-id="a1b31-153">Policy name (e.g. B2C\_1\_SignUpIn)</span></span>

<span data-ttu-id="a1b31-154">권한 부여 및 토큰 끝점 URI를 자동으로 검색하려는 경우 검색 URI에서 정보를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1b31-154">If you choose to automatically discover the authorization and token endpoint URIs, you will need to fetch information from the discovery URI.</span></span> <span data-ttu-id="a1b31-155">검색 URI는 다음 URL에서 테넌트\_ID 및 정책\_이름을 바꿔서 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1b31-155">The discovery URI can be generated by replacing the Tenant\_ID and the Policy\_Name in the following URL:</span></span>

```java
String mDiscoveryURI = "https://login.microsoftonline.com/<Tenant_ID>/v2.0/.well-known/openid-configuration?p=<Policy_Name>";
```

<span data-ttu-id="a1b31-156">다음을 실행하면 권한 부여 및 토큰 끝점 URI를 획득하고 AuthorizationServiceConfiguration 개체를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1b31-156">You can then acquire the authorization and token endpoint URIs and create an AuthorizationServiceConfiguration object by running the following:</span></span>

```java
final Uri issuerUri = Uri.parse(mDiscoveryURI);
AuthorizationServiceConfiguration config;

AuthorizationServiceConfiguration.fetchFromIssuer(
    issuerUri,
    new RetrieveConfigurationCallback() {
      @Override public void onFetchConfigurationCompleted(
          @Nullable AuthorizationServiceConfiguration serviceConfiguration,
          @Nullable AuthorizationException ex) {
        if (ex != null) {
            Log.w(TAG, "Failed to retrieve configuration for " + issuerUri, ex);
        } else {
            // service configuration retrieved, proceed to authorization...
        }
      }
  });
```

<span data-ttu-id="a1b31-157">권한 부여 및 토큰 끝점 URI를 가져오기 위해 검색을 사용하는 대신 아래 URL에서 테넌트\_ID 및 정책\_이름을 바꾸면 명시적으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1b31-157">Instead of using discovery to obtain the authorization and token endpoint URIs, you can also specify them explicitly by replacing the Tenant\_ID and the Policy\_Name in the URL's below:</span></span>

```java
String mAuthEndpoint = "https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/authorize?p=<Policy_Name>";

String mTokenEndpoint = "https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/token?p=<Policy_Name>";
```

<span data-ttu-id="a1b31-158">다음 코드를 실행하여 AuthorizationServiceConfiguration 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a1b31-158">Run the following code to create your AuthorizationServiceConfiguration object:</span></span>

```java
AuthorizationServiceConfiguration config =
        new AuthorizationServiceConfiguration(name, mAuthEndpoint, mTokenEndpoint);

// perform the auth request...
```

### <a name="authorizing"></a><span data-ttu-id="a1b31-159">권한 부여</span><span class="sxs-lookup"><span data-stu-id="a1b31-159">Authorizing</span></span>

<span data-ttu-id="a1b31-160">권한 부여 서비스 구성을 구성하거나 검색하면 권한 부여 요청을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1b31-160">After configuring or retrieving an authorization service configuration, an authorization request can be constructed.</span></span> <span data-ttu-id="a1b31-161">요청을 만들려면 다음 정보가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a1b31-161">To create the request, you will need the following information:</span></span>

* <span data-ttu-id="a1b31-162">클라이언트 ID(예: 00000000-0000-0000-0000-000000000000)</span><span class="sxs-lookup"><span data-stu-id="a1b31-162">Client ID (e.g. 00000000-0000-0000-0000-000000000000)</span></span>
* <span data-ttu-id="a1b31-163">사용자 지정 스키마를 사용하는 리디렉션 URI(예: com.onmicrosoft.fabrikamb2c.exampleapp://oauthredirect)</span><span class="sxs-lookup"><span data-stu-id="a1b31-163">Redirect URI with a custom scheme (e.g. com.onmicrosoft.fabrikamb2c.exampleapp://oauthredirect)</span></span>

<span data-ttu-id="a1b31-164">두 항목 모두 [앱을 등록](#create-an-application)할 때 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1b31-164">Both items should have been saved when you were [registering your app](#create-an-application).</span></span>

```java
AuthorizationRequest req = new AuthorizationRequest.Builder(
    config,
    clientId,
    ResponseTypeValues.CODE,
    redirectUri)
    .build();
```

<span data-ttu-id="a1b31-165">프로세스의 나머지 단계를 완료하는 방법은 [AppAuth 가이드](https://openid.github.io/AppAuth-Android/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a1b31-165">Please refer to the [AppAuth guide](https://openid.github.io/AppAuth-Android/) on how to complete the rest of the process.</span></span> <span data-ttu-id="a1b31-166">작업 중인 앱으로 빠르게 시작해야 하는 경우에는 [샘플](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c)을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="a1b31-166">If you need to quickly get started with a working app, check out [our sample](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span></span> <span data-ttu-id="a1b31-167">[README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md)에 나온 단계에 따라 사용자 고유의 Azure AD B2C 구성을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a1b31-167">Follow the steps in the [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md) to enter your own Azure AD B2C configuration.</span></span>

<span data-ttu-id="a1b31-168">Microsoft는 사용자 의견 및 제안을 항상 환영합니다!</span><span class="sxs-lookup"><span data-stu-id="a1b31-168">We are always open to feedback and suggestions!</span></span> <span data-ttu-id="a1b31-169">이 토픽을 완료하기가 어렵거나 이 콘텐츠를 개선할 사항이 있는 경우 페이지의 맨 아래에 의견을 보내주시면 감사하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a1b31-169">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at the bottom of the page.</span></span> <span data-ttu-id="a1b31-170">기능 요청이 있는 경우 [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c)에 추가해 주세요.</span><span class="sxs-lookup"><span data-stu-id="a1b31-170">For feature requests, add them to [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>


---
title: "iOS 응용 프로그램을 사용하여 토큰 가져오기 - Azure AD B2C | Microsoft Docs"
description: "이 문서에서는 Azure Active Directory B2C와 함께 AppAuth를 사용하여 iOS 앱을 만들고 사용자 ID를 관리하고 사용자를 인증하는 방법을 보여 줍니다."
services: active-directory-b2c
documentationcenter: ios
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: d818a634-42c2-4cbd-bf73-32fa0c8c69d3
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: mobile-ios
ms.devlang: objectivec
ms.topic: article
ms.date: 03/07/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: ebec5d910b8987dcc8155cd4ead00f87d219941c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-ad-b2c-sign-in-using-an-ios-application"></a><span data-ttu-id="f9c04-103">Azure AD B2C: iOS 응용 프로그램을 사용하여 로그인</span><span class="sxs-lookup"><span data-stu-id="f9c04-103">Azure AD B2C: Sign-in using an iOS application</span></span>

<span data-ttu-id="f9c04-104">Microsoft ID 플랫폼은 OAuth2 및 OpenID Connect와 같은 개방형 표준을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f9c04-104">The Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="f9c04-105">개방형 표준 프로토콜을 사용하면 서비스와 통합할 라이브러리를 선택할 때 더 많은 개발자 선택 옵션이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9c04-105">Using an open standard protocol offers more developer choice when selecting a library to integrate with our services.</span></span> <span data-ttu-id="f9c04-106">개발자가 Microsoft ID 플랫폼에 연결되는 응용 프로그램을 원활히 작성할 수 있도록 이 연습 및 다른 유사한 항목을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f9c04-106">We've provided this walkthrough and others like it to aid developers with writing applications that connect to the Microsoft Identity platform.</span></span> <span data-ttu-id="f9c04-107">[RFC6749 OAuth2 사양](https://tools.ietf.org/html/rfc6749)을 구현하는 대부분의 라이브러리는 Microsoft ID 플랫폼에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9c04-107">Most libraries that implement [the RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) are able to connect to the Microsoft Identity platform.</span></span>

> [!WARNING]
> <span data-ttu-id="f9c04-108">Microsoft는 타사 라이브러리에 대한 수정 사항을 제공하지 않으며 이러한 라이브러리의 검토를 완료하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="f9c04-108">Microsoft does not provide fixes for third-party libraries and has not done a review of those libraries.</span></span> <span data-ttu-id="f9c04-109">이 샘플은 기본 시나리오에서 Azure AD B2C와의 호환성이 테스트된 AppAuth라는 타사 라이브러리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f9c04-109">This sample is using a third-party library called AppAuth that has been tested for compatibility in basic scenarios with the Azure AD B2C.</span></span> <span data-ttu-id="f9c04-110">문제 및 기능 요청은 라이브러리의 오픈 소스 프로젝트로 리디렉션되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9c04-110">Issues and feature requests should be directed to the library's open-source project.</span></span> <span data-ttu-id="f9c04-111">자세한 내용은 [이 문서](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries)(영문)를 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="f9c04-111">For more information, see [this article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries).</span></span>
>
>

<span data-ttu-id="f9c04-112">OAuth2 또는 OpenID Connect를 처음 접하는 경우 이 샘플 구성 대부분이 잘 이해되지 않을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9c04-112">If you're new to OAuth2 or OpenID Connect, much of this sample configuration may not make much sense to you.</span></span> <span data-ttu-id="f9c04-113">[여기서 추천한 프로토콜에 관한 개요](active-directory-b2c-reference-protocols.md)를 간략히 살펴볼 것을 추천합니다.</span><span class="sxs-lookup"><span data-stu-id="f9c04-113">We recommend you look at a brief [overview of the protocol we've documented here](active-directory-b2c-reference-protocols.md).</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="f9c04-114">Azure AD B2C 디렉터리 가져오기</span><span class="sxs-lookup"><span data-stu-id="f9c04-114">Get an Azure AD B2C directory</span></span>
<span data-ttu-id="f9c04-115">Azure AD B2C를 사용하기 전에 디렉터리 또는 테넌트를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9c04-115">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="f9c04-116">디렉터리는 모든 사용자, 앱, 그룹 등을 위한 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="f9c04-116">A directory is a container for all your users, apps, groups, and more.</span></span> <span data-ttu-id="f9c04-117">디렉터리가 없는 경우 계속하기 전에 [B2C 디렉터리를 만듭니다](active-directory-b2c-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="f9c04-117">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="f9c04-118">응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="f9c04-118">Create an application</span></span>
<span data-ttu-id="f9c04-119">다음으로 B2C 디렉터리에서 앱을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9c04-119">Next, you need to create an app in your B2C directory.</span></span> <span data-ttu-id="f9c04-120">앱 등록은 앱과 안전하게 통신하는 데 필요한 Azure AD 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f9c04-120">The app registration gives Azure AD information that it needs to communicate securely with your app.</span></span> <span data-ttu-id="f9c04-121">모바일 앱을 만들려면 [이러한 지침](active-directory-b2c-app-registration.md)에 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="f9c04-121">To create a mobile app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="f9c04-122">다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9c04-122">Be sure to:</span></span>

* <span data-ttu-id="f9c04-123">응용 프로그램에 **네이티브 클라이언트**를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="f9c04-123">Include a **Native client** in the application.</span></span>
* <span data-ttu-id="f9c04-124">앱에 할당된 **응용 프로그램 ID** 를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="f9c04-124">Copy the **Application ID** that is assigned to your app.</span></span> <span data-ttu-id="f9c04-125">이 가이드는 나중에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f9c04-125">You need this GUID later.</span></span>
* <span data-ttu-id="f9c04-126">사용자 지정 스키마를 사용하는 **리디렉션 URI**(예: com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect)를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f9c04-126">Set up a **Redirect URI** with a custom scheme (for example, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span></span> <span data-ttu-id="f9c04-127">이 URI는 나중에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f9c04-127">You need this URI later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="f9c04-128">정책 만들기</span><span class="sxs-lookup"><span data-stu-id="f9c04-128">Create your policies</span></span>
<span data-ttu-id="f9c04-129">Azure AD B2C에서 모든 사용자 환경은 [정책](active-directory-b2c-reference-policies.md)에 의해 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9c04-129">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="f9c04-130">이 앱은 결합된 로그인 및 등록의 하나의 ID 환경을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="f9c04-130">This app contains one identity experience: a combined sign-in and sign-up.</span></span> <span data-ttu-id="f9c04-131">[정책 참조 문서](active-directory-b2c-reference-policies.md#create-a-sign-up-policy)에서 설명한 대로 이 정책을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9c04-131">Create this policy as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="f9c04-132">정책을 만들 때 다음을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f9c04-132">When you create the policy, be sure to:</span></span>

* <span data-ttu-id="f9c04-133">**등록 특성** 아래에서 **표시 이름** 특성을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f9c04-133">Under **Sign-up attributes**, select the attribute **Display name**.</span></span>  <span data-ttu-id="f9c04-134">다른 특성도 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9c04-134">You can select other attributes as well.</span></span>
* <span data-ttu-id="f9c04-135">**응용 프로그램 클레임** 아래에서 **표시 이름** 및 **사용자의 개체 ID** 클레임을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f9c04-135">Under **Application claims**, select the claims **Display name** and **User's Object ID**.</span></span> <span data-ttu-id="f9c04-136">다른 클레임도 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9c04-136">You can select other claims as well.</span></span>
* <span data-ttu-id="f9c04-137">각 정책을 만든 후에 **이름**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="f9c04-137">Copy the **Name** of each policy after you create it.</span></span> <span data-ttu-id="f9c04-138">정책을 저장하면 `b2c_1_`이 정책 이름의 접두사로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9c04-138">Your policy name is prefixed with `b2c_1_` when you save the policy.</span></span>  <span data-ttu-id="f9c04-139">정책 이름은 나중에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f9c04-139">You need the policy name later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="f9c04-140">정책을 만들었다면 앱을 빌드할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f9c04-140">After you have created your policies, you're ready to build your app.</span></span>

## <a name="download-the-sample-code"></a><span data-ttu-id="f9c04-141">샘플 코드 다운로드</span><span class="sxs-lookup"><span data-stu-id="f9c04-141">Download the sample code</span></span>
<span data-ttu-id="f9c04-142">[GitHub에서](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c) Azure AD B2C와 함께 AppAuth를 사용하는 작업 샘플이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9c04-142">We have provided a working sample that uses AppAuth with Azure AD B2C [on GitHub](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span></span> <span data-ttu-id="f9c04-143">코드를 다운로드하고 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9c04-143">You can download the code and run it.</span></span> <span data-ttu-id="f9c04-144">자신만의 Azure AD B2C 테넌트를 사용하려면 [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md) 지침에 따르세요.</span><span class="sxs-lookup"><span data-stu-id="f9c04-144">To use your own Azure AD B2C tenant, follow the instructions in the [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md).</span></span>

<span data-ttu-id="f9c04-145">이 샘플은 [GitHub의 iOS AppAuth 프로젝트](https://github.com/openid/AppAuth-iOS)의 추가 정보 지침에 따라 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="f9c04-145">This sample was created by following the README instructions by the [iOS AppAuth project on GitHub](https://github.com/openid/AppAuth-iOS).</span></span> <span data-ttu-id="f9c04-146">샘플 및 라이브러리의 작동 방식에 대한 자세한 내용은 GitHub의 AppAuth 추가 정보를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f9c04-146">For more details on how the sample and the library work, reference the AppAuth README on GitHub.</span></span>

## <a name="modifying-your-app-to-use-azure-ad-b2c-with-appauth"></a><span data-ttu-id="f9c04-147">AppAuth와 함께 Azure AD B2C를 사용하도록 앱 수정</span><span class="sxs-lookup"><span data-stu-id="f9c04-147">Modifying your app to use Azure AD B2C with AppAuth</span></span>

> [!NOTE]
> <span data-ttu-id="f9c04-148">AppAuth는 iOS 7 이상을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="f9c04-148">AppAuth supports iOS 7 and above.</span></span>  <span data-ttu-id="f9c04-149">그러나 Google에 소셜 로그인을 지원하려면 iOS 9 이상이 필요한 SFSafariViewController가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f9c04-149">However, to support social logins on Google, SFSafariViewController is needed which requires iOS 9 or higher.</span></span>
>

### <a name="configuration"></a><span data-ttu-id="f9c04-150">구성</span><span class="sxs-lookup"><span data-stu-id="f9c04-150">Configuration</span></span>

<span data-ttu-id="f9c04-151">권한 부여 끝점과 토큰 끝점 URI를 모두 지정하여 Azure AD B2C와의 통신을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9c04-151">You can configure communication with Azure AD B2C by specifying both the authorization endpoint and token endpoint URIs.</span></span>  <span data-ttu-id="f9c04-152">이러한 URI를 생성하려면 다음 정보가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f9c04-152">To generate these URIs, you need the following information:</span></span>
* <span data-ttu-id="f9c04-153">테넌트 ID(예: contoso.onmicrosoft.com)</span><span class="sxs-lookup"><span data-stu-id="f9c04-153">Tenant ID (for example, contoso.onmicrosoft.com)</span></span>
* <span data-ttu-id="f9c04-154">정책 이름(예: B2C\_1\_SignUpIn)</span><span class="sxs-lookup"><span data-stu-id="f9c04-154">Policy name (for example, B2C\_1\_SignUpIn)</span></span>

<span data-ttu-id="f9c04-155">토큰 끝점 URI는 다음 URL에서 테넌트\_ID 및 정책\_이름을 바꿔서 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9c04-155">The token endpoint URI can be generated by replacing the Tenant\_ID and the Policy\_Name in the following URL:</span></span>

```objc
static NSString *const tokenEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/token";
```

<span data-ttu-id="f9c04-156">권한 부여 끝점 URI는 다음 URL에서 테넌트\_ID 및 정책\_이름을 바꿔서 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9c04-156">The authorization endpoint URI can be generated by replacing the Tenant\_ID and the Policy\_Name in the following URL:</span></span>

```objc
static NSString *const authorizationEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/authorize";
```

<span data-ttu-id="f9c04-157">다음 코드를 실행하여 AuthorizationServiceConfiguration 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f9c04-157">Run the following code to create your AuthorizationServiceConfiguration object:</span></span>

```objc
OIDServiceConfiguration *configuration = 
    [[OIDServiceConfiguration alloc] initWithAuthorizationEndpoint:authorizationEndpoint tokenEndpoint:tokenEndpoint];
// now we are ready to perform the auth request...
```

### <a name="authorizing"></a><span data-ttu-id="f9c04-158">권한 부여</span><span class="sxs-lookup"><span data-stu-id="f9c04-158">Authorizing</span></span>

<span data-ttu-id="f9c04-159">권한 부여 서비스 구성을 구성하거나 검색하면 권한 부여 요청을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9c04-159">After configuring or retrieving an authorization service configuration, an authorization request can be constructed.</span></span> <span data-ttu-id="f9c04-160">요청을 만들려면 다음 정보가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f9c04-160">To create the request, you need the following information:</span></span>  
* <span data-ttu-id="f9c04-161">클라이언트 ID(예: 00000000-0000-0000-0000-000000000000)</span><span class="sxs-lookup"><span data-stu-id="f9c04-161">Client ID (for example, 00000000-0000-0000-0000-000000000000)</span></span>
* <span data-ttu-id="f9c04-162">사용자 지정 스키마를 사용하는 리디렉션 URI(예: com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect)</span><span class="sxs-lookup"><span data-stu-id="f9c04-162">Redirect URI with a custom scheme (for example, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect)</span></span>

<span data-ttu-id="f9c04-163">두 항목 모두 [앱을 등록](#create-an-application)할 때 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9c04-163">Both items should have been saved when you were [registering your app](#create-an-application).</span></span>

```objc
OIDAuthorizationRequest *request = 
    [[OIDAuthorizationRequest alloc] initWithConfiguration:configuration
                                                  clientId:kClientId
                                                    scopes:@[OIDScopeOpenID, OIDScopeProfile]
                                               redirectURL:[NSURL URLWithString:kRedirectUri]
                                              responseType:OIDResponseTypeCode
                                      additionalParameters:nil];

AppDelegate *appDelegate = (AppDelegate *)[UIApplication sharedApplication].delegate;
appDelegate.currentAuthorizationFlow = 
    [OIDAuthState authStateByPresentingAuthorizationRequest:request
                                   presentingViewController:self
                                                   callback:^(OIDAuthState *_Nullable authState, NSError *_Nullable error) {
        if (authState) {
            NSLog(@"Got authorization tokens. Access token: %@", authState.lastTokenResponse.accessToken);
            [self setAuthState:authState];
        } else {
            NSLog(@"Authorization error: %@", [error localizedDescription]);
            [self setAuthState:nil];
        }
    }];
```

<span data-ttu-id="f9c04-164">사용자 지정 스키마를 사용하는 URI에 대한 리디렉션을 처리하도록 응용 프로그램을 설정하려면 사용자의 Info.pList에서 'URL 스키마' 목록을 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9c04-164">To set up your application to handle the redirect to the URI with the custom scheme, you need to update the list of 'URL Schemes' in your Info.pList:</span></span>
* <span data-ttu-id="f9c04-165">Info.pList를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f9c04-165">Open Info.pList.</span></span>
* <span data-ttu-id="f9c04-166">'번들 OS 유형 코드'와 같은 행 위로 마우스를 가져가서 \+ 기호를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f9c04-166">Hover over a row like 'Bundle OS Type Code' and click the \+ symbol.</span></span>
* <span data-ttu-id="f9c04-167">새 행 'URL 형식'의 이름을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="f9c04-167">Rename the new row 'URL types'.</span></span>
* <span data-ttu-id="f9c04-168">'URL 형식'의 왼쪽에 있는 화살표를 클릭하여 트리를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f9c04-168">Click the arrow to the left of 'URL types' to open the tree.</span></span>
* <span data-ttu-id="f9c04-169">'항목 0'의 왼쪽에 있는 화살표를 클릭하여 트리를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f9c04-169">Click the arrow to the left of 'Item 0' to open the tree.</span></span>
* <span data-ttu-id="f9c04-170">항목 0 아래의 첫 번째 항목 이름을 'URL Schemes'로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f9c04-170">Rename first item underneath Item 0 to 'URL Schemes'.</span></span>
* <span data-ttu-id="f9c04-171">'URL Schemes'의 왼쪽에 있는 화살표를 클릭하여 트리를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f9c04-171">Click the arrow to the left of 'URL Schemes' to open the tree.</span></span>
* <span data-ttu-id="f9c04-172">'값' 열에서 'URL Schemes' 아래의 '항목 0' 왼쪽 필드가 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9c04-172">In the 'Value' column, there is a blank field to the left of 'Item 0' underneath 'URL Schemes'.</span></span>  <span data-ttu-id="f9c04-173">이 값을 응용 프로그램의 고유한 스키마로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f9c04-173">Set the value to your application's unique scheme.</span></span>  <span data-ttu-id="f9c04-174">OIDAuthorizationRequest 개체를 만들 때 redirectURL에 사용된 스키마와 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9c04-174">The value must match the scheme used in redirectURL when creating the OIDAuthorizationRequest object.</span></span>  <span data-ttu-id="f9c04-175">이 샘플에서는 스키마 'com.onmicrosoft.fabrikamb2c.exampleapp'을 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="f9c04-175">In our sample, we used the scheme 'com.onmicrosoft.fabrikamb2c.exampleapp'.</span></span>

<span data-ttu-id="f9c04-176">프로세스의 나머지 단계를 완료하는 방법은 [AppAuth 가이드](https://openid.github.io/AppAuth-iOS/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f9c04-176">Refer to the [AppAuth guide](https://openid.github.io/AppAuth-iOS/) on how to complete the rest of the process.</span></span> <span data-ttu-id="f9c04-177">작업 중인 앱으로 빠르게 시작해야 하는 경우에는 [샘플](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c)을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="f9c04-177">If you need to quickly get started with a working app, check out [our sample](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span></span> <span data-ttu-id="f9c04-178">[README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md)에 나온 단계에 따라 사용자 고유의 Azure AD B2C 구성을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f9c04-178">Follow the steps in the [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md) to enter your own Azure AD B2C configuration.</span></span>

<span data-ttu-id="f9c04-179">Microsoft는 사용자 의견 및 제안을 항상 환영합니다!</span><span class="sxs-lookup"><span data-stu-id="f9c04-179">We are always open to feedback and suggestions!</span></span> <span data-ttu-id="f9c04-180">이 토픽을 완료하기가 어렵거나 이 콘텐츠를 개선할 사항이 있는 경우 페이지의 맨 아래에 의견을 보내주시면 감사하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f9c04-180">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at the bottom of the page.</span></span> <span data-ttu-id="f9c04-181">기능 요청이 있는 경우 [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c)에 추가해 주세요.</span><span class="sxs-lookup"><span data-stu-id="f9c04-181">For feature requests, add them to [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>

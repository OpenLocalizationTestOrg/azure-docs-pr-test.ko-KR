---
title: "iOS 응용 프로그램을 사용하여 토큰 가져오기 - Azure AD B2C | Microsoft Docs"
description: "이 문서에서는 보여 어떻게 toocreate AppAuth Azure Active Directory B2C toomanage 사용자 id를 사용 하 고 사용자를 인증 하는 iOS 응용 프로그램입니다."
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
ms.openlocfilehash: e7cbe2de6e9ae3d45448cdd36292c457a0ef4887
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-sign-in-using-an-ios-application"></a><span data-ttu-id="eed89-103">Azure AD B2C: iOS 응용 프로그램을 사용하여 로그인</span><span class="sxs-lookup"><span data-stu-id="eed89-103">Azure AD B2C: Sign-in using an iOS application</span></span>

<span data-ttu-id="eed89-104">hello Microsoft id 플랫폼 OAuth2 및 OpenID Connect와 같은 개방형 표준을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="eed89-104">hello Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="eed89-105">개방형 표준 프로토콜을 사용 하 여 서비스와 라이브러리 toointegrate 선택할 때 더 많은 개발자 선택 옵션이 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="eed89-105">Using an open standard protocol offers more developer choice when selecting a library toointegrate with our services.</span></span> <span data-ttu-id="eed89-106">제공 했습니다이 연습에서는 등과 같은 tooaid 개발자 toohello Microsoft Id 플랫폼을 연결 하는 응용 프로그램을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="eed89-106">We've provided this walkthrough and others like it tooaid developers with writing applications that connect toohello Microsoft Identity platform.</span></span> <span data-ttu-id="eed89-107">구현 하는 대부분의 라이브러리 [hello RFC6749 OAuth2 사양](https://tools.ietf.org/html/rfc6749) 수 tooconnect toohello Microsoft Identity 플랫폼 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eed89-107">Most libraries that implement [hello RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) are able tooconnect toohello Microsoft Identity platform.</span></span>

> [!WARNING]
> <span data-ttu-id="eed89-108">Microsoft는 타사 라이브러리에 대한 수정 사항을 제공하지 않으며 이러한 라이브러리의 검토를 완료하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="eed89-108">Microsoft does not provide fixes for third-party libraries and has not done a review of those libraries.</span></span> <span data-ttu-id="eed89-109">이 샘플 테스트 된 AppAuth hello Azure AD B2C로 기본 시나리오의 호환성에 대 한 호출 타사 라이브러리를 사용 중입니다.</span><span class="sxs-lookup"><span data-stu-id="eed89-109">This sample is using a third-party library called AppAuth that has been tested for compatibility in basic scenarios with hello Azure AD B2C.</span></span> <span data-ttu-id="eed89-110">문제 및 기능 요청 toohello 방향이 지정 된 라이브러리의 오픈 소스 프로젝트 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eed89-110">Issues and feature requests should be directed toohello library's open-source project.</span></span> <span data-ttu-id="eed89-111">자세한 내용은 [이 문서](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries)(영문)를 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="eed89-111">For more information, see [this article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries).</span></span>
>
>

<span data-ttu-id="eed89-112">이 예제 구성의 많은 새로운 tooOAuth2 또는 OpenID Connect를 사용 하는 경우 많은 의미 tooyou를 하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eed89-112">If you're new tooOAuth2 or OpenID Connect, much of this sample configuration may not make much sense tooyou.</span></span> <span data-ttu-id="eed89-113">간단한 보면 하는 것이 좋습니다 [여기 기록할 म hello 프로토콜 개요](active-directory-b2c-reference-protocols.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="eed89-113">We recommend you look at a brief [overview of hello protocol we've documented here](active-directory-b2c-reference-protocols.md).</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="eed89-114">Azure AD B2C 디렉터리 가져오기</span><span class="sxs-lookup"><span data-stu-id="eed89-114">Get an Azure AD B2C directory</span></span>
<span data-ttu-id="eed89-115">Azure AD B2C를 사용하기 전에 디렉터리 또는 테넌트를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eed89-115">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="eed89-116">디렉터리는 모든 사용자, 앱, 그룹 등을 위한 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="eed89-116">A directory is a container for all your users, apps, groups, and more.</span></span> <span data-ttu-id="eed89-117">디렉터리가 없는 경우 계속하기 전에 [B2C 디렉터리를 만듭니다](active-directory-b2c-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="eed89-117">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="eed89-118">응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="eed89-118">Create an application</span></span>
<span data-ttu-id="eed89-119">다음으로 응용 프로그램 toocreate B2C 디렉터리에 있어야합니다.</span><span class="sxs-lookup"><span data-stu-id="eed89-119">Next, you need toocreate an app in your B2C directory.</span></span> <span data-ttu-id="eed89-120">hello 앱 등록 필요 하다 고 toocommunicate 응용 프로그램과 함께 안전 하 게 Azure AD 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="eed89-120">hello app registration gives Azure AD information that it needs toocommunicate securely with your app.</span></span> <span data-ttu-id="eed89-121">toocreate 모바일 앱에 따라 [이러한 지침](active-directory-b2c-app-registration.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="eed89-121">toocreate a mobile app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="eed89-122">다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eed89-122">Be sure to:</span></span>

* <span data-ttu-id="eed89-123">포함 된 **Native client** hello 응용 프로그램에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eed89-123">Include a **Native client** in hello application.</span></span>
* <span data-ttu-id="eed89-124">복사 hello **응용 프로그램 ID** 할당된 tooyour 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="eed89-124">Copy hello **Application ID** that is assigned tooyour app.</span></span> <span data-ttu-id="eed89-125">이 가이드는 나중에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="eed89-125">You need this GUID later.</span></span>
* <span data-ttu-id="eed89-126">사용자 지정 스키마를 사용하는 **리디렉션 URI**(예: com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect)를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="eed89-126">Set up a **Redirect URI** with a custom scheme (for example, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span></span> <span data-ttu-id="eed89-127">이 URI는 나중에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="eed89-127">You need this URI later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="eed89-128">정책 만들기</span><span class="sxs-lookup"><span data-stu-id="eed89-128">Create your policies</span></span>
<span data-ttu-id="eed89-129">Azure AD B2C에서 모든 사용자 환경은 [정책](active-directory-b2c-reference-policies.md)에 의해 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="eed89-129">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="eed89-130">이 앱은 결합된 로그인 및 등록의 하나의 ID 환경을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="eed89-130">This app contains one identity experience: a combined sign-in and sign-up.</span></span> <span data-ttu-id="eed89-131">[정책 참조 문서](active-directory-b2c-reference-policies.md#create-a-sign-up-policy)에서 설명한 대로 이 정책을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eed89-131">Create this policy as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="eed89-132">Hello 정책을 만들 때 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eed89-132">When you create hello policy, be sure to:</span></span>

* <span data-ttu-id="eed89-133">아래 **등록 특성**선택, hello 특성 **표시 이름**합니다.</span><span class="sxs-lookup"><span data-stu-id="eed89-133">Under **Sign-up attributes**, select hello attribute **Display name**.</span></span>  <span data-ttu-id="eed89-134">다른 특성도 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eed89-134">You can select other attributes as well.</span></span>
* <span data-ttu-id="eed89-135">아래 **응용 프로그램 클레임**, hello 클레임 선택 **표시 이름** 및 **사용자의 개체 ID**합니다.</span><span class="sxs-lookup"><span data-stu-id="eed89-135">Under **Application claims**, select hello claims **Display name** and **User's Object ID**.</span></span> <span data-ttu-id="eed89-136">다른 클레임도 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eed89-136">You can select other claims as well.</span></span>
* <span data-ttu-id="eed89-137">복사 hello **이름** 를 만든 후 각 정책의 합니다.</span><span class="sxs-lookup"><span data-stu-id="eed89-137">Copy hello **Name** of each policy after you create it.</span></span> <span data-ttu-id="eed89-138">정책 이름 앞에 `b2c_1_` hello 정책 저장할 때.</span><span class="sxs-lookup"><span data-stu-id="eed89-138">Your policy name is prefixed with `b2c_1_` when you save hello policy.</span></span>  <span data-ttu-id="eed89-139">Hello 정책 이름이 나중에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="eed89-139">You need hello policy name later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="eed89-140">준비 toobuild 하 여 정책을 만든 후 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="eed89-140">After you have created your policies, you're ready toobuild your app.</span></span>

## <a name="download-hello-sample-code"></a><span data-ttu-id="eed89-141">Hello 샘플 코드 다운로드</span><span class="sxs-lookup"><span data-stu-id="eed89-141">Download hello sample code</span></span>
<span data-ttu-id="eed89-142">[GitHub에서](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c) Azure AD B2C와 함께 AppAuth를 사용하는 작업 샘플이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="eed89-142">We have provided a working sample that uses AppAuth with Azure AD B2C [on GitHub](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span></span> <span data-ttu-id="eed89-143">Hello 코드를 다운로드 하 고 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eed89-143">You can download hello code and run it.</span></span> <span data-ttu-id="eed89-144">toouse 자신의 Azure AD B2C 테 넌 트를 hello 지침 hello에 따라 [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="eed89-144">toouse your own Azure AD B2C tenant, follow hello instructions in hello [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md).</span></span>

<span data-ttu-id="eed89-145">이 샘플은 hello 하 여 hello README 지침에 따라 만들어졌습니다 [GitHub의 iOS AppAuth 프로젝트](https://github.com/openid/AppAuth-iOS)합니다.</span><span class="sxs-lookup"><span data-stu-id="eed89-145">This sample was created by following hello README instructions by hello [iOS AppAuth project on GitHub](https://github.com/openid/AppAuth-iOS).</span></span> <span data-ttu-id="eed89-146">Hello 샘플 및 hello 라이브러리의 작동 방식에 대 한 자세한 내용은 hello GitHub에서 AppAuth 추가 정보를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="eed89-146">For more details on how hello sample and hello library work, reference hello AppAuth README on GitHub.</span></span>

## <a name="modifying-your-app-toouse-azure-ad-b2c-with-appauth"></a><span data-ttu-id="eed89-147">Azure AD B2C AppAuth와 사용자 응용 프로그램 toouse 수정</span><span class="sxs-lookup"><span data-stu-id="eed89-147">Modifying your app toouse Azure AD B2C with AppAuth</span></span>

> [!NOTE]
> <span data-ttu-id="eed89-148">AppAuth는 iOS 7 이상을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="eed89-148">AppAuth supports iOS 7 and above.</span></span>  <span data-ttu-id="eed89-149">그러나 iOS 9 이상이 필요로 하 toosupport Google, SFSafariViewController에서 소셜 로그인이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="eed89-149">However, toosupport social logins on Google, SFSafariViewController is needed which requires iOS 9 or higher.</span></span>
>

### <a name="configuration"></a><span data-ttu-id="eed89-150">구성</span><span class="sxs-lookup"><span data-stu-id="eed89-150">Configuration</span></span>

<span data-ttu-id="eed89-151">권한 부여 끝점 hello와 토큰 끝점 Uri 지정 하 여 Azure AD B2C와 통신을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eed89-151">You can configure communication with Azure AD B2C by specifying both hello authorization endpoint and token endpoint URIs.</span></span>  <span data-ttu-id="eed89-152">toogenerate 다음 정보는 hello 해야 이러한 Uri:</span><span class="sxs-lookup"><span data-stu-id="eed89-152">toogenerate these URIs, you need hello following information:</span></span>
* <span data-ttu-id="eed89-153">테넌트 ID(예: contoso.onmicrosoft.com)</span><span class="sxs-lookup"><span data-stu-id="eed89-153">Tenant ID (for example, contoso.onmicrosoft.com)</span></span>
* <span data-ttu-id="eed89-154">정책 이름(예: B2C\_1\_SignUpIn)</span><span class="sxs-lookup"><span data-stu-id="eed89-154">Policy name (for example, B2C\_1\_SignUpIn)</span></span>

<span data-ttu-id="eed89-155">hello 토큰 끝점 URI를 대체 하 여 생성할 수 hello 테 넌 트\_ID와 hello 정책\_hello url에 이름:</span><span class="sxs-lookup"><span data-stu-id="eed89-155">hello token endpoint URI can be generated by replacing hello Tenant\_ID and hello Policy\_Name in hello following URL:</span></span>

```objc
static NSString *const tokenEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/token";
```

<span data-ttu-id="eed89-156">hello 권한 부여 끝점 URI를 대체 하 여 생성할 수 hello 테 넌 트\_ID와 hello 정책\_hello url에 이름:</span><span class="sxs-lookup"><span data-stu-id="eed89-156">hello authorization endpoint URI can be generated by replacing hello Tenant\_ID and hello Policy\_Name in hello following URL:</span></span>

```objc
static NSString *const authorizationEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/authorize";
```

<span data-ttu-id="eed89-157">다음 코드 toocreate hello AuthorizationServiceConfiguration 개체를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="eed89-157">Run hello following code toocreate your AuthorizationServiceConfiguration object:</span></span>

```objc
OIDServiceConfiguration *configuration = 
    [[OIDServiceConfiguration alloc] initWithAuthorizationEndpoint:authorizationEndpoint tokenEndpoint:tokenEndpoint];
// now we are ready tooperform hello auth request...
```

### <a name="authorizing"></a><span data-ttu-id="eed89-158">권한 부여</span><span class="sxs-lookup"><span data-stu-id="eed89-158">Authorizing</span></span>

<span data-ttu-id="eed89-159">권한 부여 서비스 구성을 구성하거나 검색하면 권한 부여 요청을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eed89-159">After configuring or retrieving an authorization service configuration, an authorization request can be constructed.</span></span> <span data-ttu-id="eed89-160">다음 정보는 hello 필요한 toocreate hello 요청:</span><span class="sxs-lookup"><span data-stu-id="eed89-160">toocreate hello request, you need hello following information:</span></span>  
* <span data-ttu-id="eed89-161">클라이언트 ID(예: 00000000-0000-0000-0000-000000000000)</span><span class="sxs-lookup"><span data-stu-id="eed89-161">Client ID (for example, 00000000-0000-0000-0000-000000000000)</span></span>
* <span data-ttu-id="eed89-162">사용자 지정 스키마를 사용하는 리디렉션 URI(예: com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect)</span><span class="sxs-lookup"><span data-stu-id="eed89-162">Redirect URI with a custom scheme (for example, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect)</span></span>

<span data-ttu-id="eed89-163">두 항목 모두 [앱을 등록](#create-an-application)할 때 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eed89-163">Both items should have been saved when you were [registering your app](#create-an-application).</span></span>

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

<span data-ttu-id="eed89-164">프로그램 응용 프로그램 toohandle hello 리디렉션 toohello URI hello 사용자 지정 체계를 tooset, 프로그램 Info.pList에서 ' URL 구성표 ' tooupdate hello 목록이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="eed89-164">tooset up your application toohandle hello redirect toohello URI with hello custom scheme, you need tooupdate hello list of 'URL Schemes' in your Info.pList:</span></span>
* <span data-ttu-id="eed89-165">Info.pList를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="eed89-165">Open Info.pList.</span></span>
* <span data-ttu-id="eed89-166">' 번들 OS 형식 코드 '와 같은 행 위에 놓고 클릭 hello \+ 기호입니다.</span><span class="sxs-lookup"><span data-stu-id="eed89-166">Hover over a row like 'Bundle OS Type Code' and click hello \+ symbol.</span></span>
* <span data-ttu-id="eed89-167">Hello 새 행 'URL 형식을'의 이름을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="eed89-167">Rename hello new row 'URL types'.</span></span>
* <span data-ttu-id="eed89-168">'URL 형식' tooopen hello 트리의 hello 화살표 toohello 왼쪽을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="eed89-168">Click hello arrow toohello left of 'URL types' tooopen hello tree.</span></span>
* <span data-ttu-id="eed89-169">Tooopen hello 트리 '0 항목' hello 화살표 toohello 왼쪽을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="eed89-169">Click hello arrow toohello left of 'Item 0' tooopen hello tree.</span></span>
* <span data-ttu-id="eed89-170">항목 0 too'URL 구성표 아래에 첫 번째 항목을 이름을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="eed89-170">Rename first item underneath Item 0 too'URL Schemes'.</span></span>
* <span data-ttu-id="eed89-171">' URL Schemes' tooopen hello 트리의 hello 화살표 toohello 왼쪽을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="eed89-171">Click hello arrow toohello left of 'URL Schemes' tooopen hello tree.</span></span>
* <span data-ttu-id="eed89-172">Hello 'Value' 열에는 빈 필드 toohello 왼쪽에 '' URL Schemes' 아래 ' 0 항목.</span><span class="sxs-lookup"><span data-stu-id="eed89-172">In hello 'Value' column, there is a blank field toohello left of 'Item 0' underneath 'URL Schemes'.</span></span>  <span data-ttu-id="eed89-173">Hello 값 tooyour 응용 프로그램의 고유한 체계를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="eed89-173">Set hello value tooyour application's unique scheme.</span></span>  <span data-ttu-id="eed89-174">hello 값 redirectURL hello OIDAuthorizationRequest 개체를 만들 때 사용 된 hello 체계를 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eed89-174">hello value must match hello scheme used in redirectURL when creating hello OIDAuthorizationRequest object.</span></span>  <span data-ttu-id="eed89-175">이 샘플에서는 com.onmicrosoft.fabrikamb2c.exampleapp' hello 구성표'를 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="eed89-175">In our sample, we used hello scheme 'com.onmicrosoft.fabrikamb2c.exampleapp'.</span></span>

<span data-ttu-id="eed89-176">Toohello 참조 [AppAuth 가이드](https://openid.github.io/AppAuth-iOS/) 어떻게 toocomplete hello hello 프로세스의 나머지 부분에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eed89-176">Refer toohello [AppAuth guide](https://openid.github.io/AppAuth-iOS/) on how toocomplete hello rest of hello process.</span></span> <span data-ttu-id="eed89-177">Tooquickly 해야 할 경우 작업 중인 앱을 시작, 체크 아웃 [샘플](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c)합니다.</span><span class="sxs-lookup"><span data-stu-id="eed89-177">If you need tooquickly get started with a working app, check out [our sample](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span></span> <span data-ttu-id="eed89-178">Hello에 hello 단계를 따라 [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md) tooenter 자신의 Azure AD B2C 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="eed89-178">Follow hello steps in hello [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md) tooenter your own Azure AD B2C configuration.</span></span>

<span data-ttu-id="eed89-179">우리는 항상 열려 toofeedback 및 제안을!</span><span class="sxs-lookup"><span data-stu-id="eed89-179">We are always open toofeedback and suggestions!</span></span> <span data-ttu-id="eed89-180">이 항목에 문제가 발생 하거나이 콘텐츠를 개선 하기 위한 권장 사항이 있는 경우 hello hello 페이지 맨 아래에 사용자 의견 보내 주셔서 감사 합니다.</span><span class="sxs-lookup"><span data-stu-id="eed89-180">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at hello bottom of hello page.</span></span> <span data-ttu-id="eed89-181">기능 요청에 대 한 추가 너무[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c)합니다.</span><span class="sxs-lookup"><span data-stu-id="eed89-181">For feature requests, add them too[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>

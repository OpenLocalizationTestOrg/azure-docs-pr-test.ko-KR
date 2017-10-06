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
# <a name="azure-ad-b2c-sign-in-using-an-ios-application"></a>Azure AD B2C: iOS 응용 프로그램을 사용하여 로그인

hello Microsoft id 플랫폼 OAuth2 및 OpenID Connect와 같은 개방형 표준을 사용합니다. 개방형 표준 프로토콜을 사용 하 여 서비스와 라이브러리 toointegrate 선택할 때 더 많은 개발자 선택 옵션이 제공 합니다. 제공 했습니다이 연습에서는 등과 같은 tooaid 개발자 toohello Microsoft Id 플랫폼을 연결 하는 응용 프로그램을 작성 합니다. 구현 하는 대부분의 라이브러리 [hello RFC6749 OAuth2 사양](https://tools.ietf.org/html/rfc6749) 수 tooconnect toohello Microsoft Identity 플랫폼 사용 됩니다.

> [!WARNING]
> Microsoft는 타사 라이브러리에 대한 수정 사항을 제공하지 않으며 이러한 라이브러리의 검토를 완료하지 않았습니다. 이 샘플 테스트 된 AppAuth hello Azure AD B2C로 기본 시나리오의 호환성에 대 한 호출 타사 라이브러리를 사용 중입니다. 문제 및 기능 요청 toohello 방향이 지정 된 라이브러리의 오픈 소스 프로젝트 여야 합니다. 자세한 내용은 [이 문서](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries)(영문)를 읽어보세요.
>
>

이 예제 구성의 많은 새로운 tooOAuth2 또는 OpenID Connect를 사용 하는 경우 많은 의미 tooyou를 하면 안 됩니다. 간단한 보면 하는 것이 좋습니다 [여기 기록할 म hello 프로토콜 개요](active-directory-b2c-reference-protocols.md)합니다.

## <a name="get-an-azure-ad-b2c-directory"></a>Azure AD B2C 디렉터리 가져오기
Azure AD B2C를 사용하기 전에 디렉터리 또는 테넌트를 만들어야 합니다. 디렉터리는 모든 사용자, 앱, 그룹 등을 위한 컨테이너입니다. 디렉터리가 없는 경우 계속하기 전에 [B2C 디렉터리를 만듭니다](active-directory-b2c-get-started.md) .

## <a name="create-an-application"></a>응용 프로그램 만들기
다음으로 응용 프로그램 toocreate B2C 디렉터리에 있어야합니다. hello 앱 등록 필요 하다 고 toocommunicate 응용 프로그램과 함께 안전 하 게 Azure AD 정보를 제공 합니다. toocreate 모바일 앱에 따라 [이러한 지침](active-directory-b2c-app-registration.md)합니다. 다음을 수행해야 합니다.

* 포함 된 **Native client** hello 응용 프로그램에 있습니다.
* 복사 hello **응용 프로그램 ID** 할당된 tooyour 앱입니다. 이 가이드는 나중에 필요합니다.
* 사용자 지정 스키마를 사용하는 **리디렉션 URI**(예: com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect)를 설정합니다. 이 URI는 나중에 필요합니다.

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>정책 만들기
Azure AD B2C에서 모든 사용자 환경은 [정책](active-directory-b2c-reference-policies.md)에 의해 정의됩니다. 이 앱은 결합된 로그인 및 등록의 하나의 ID 환경을 포함합니다. [정책 참조 문서](active-directory-b2c-reference-policies.md#create-a-sign-up-policy)에서 설명한 대로 이 정책을 만들어야 합니다. Hello 정책을 만들 때 야 합니다.

* 아래 **등록 특성**선택, hello 특성 **표시 이름**합니다.  다른 특성도 선택할 수 있습니다.
* 아래 **응용 프로그램 클레임**, hello 클레임 선택 **표시 이름** 및 **사용자의 개체 ID**합니다. 다른 클레임도 선택할 수 있습니다.
* 복사 hello **이름** 를 만든 후 각 정책의 합니다. 정책 이름 앞에 `b2c_1_` hello 정책 저장할 때.  Hello 정책 이름이 나중에 필요합니다.

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

준비 toobuild 하 여 정책을 만든 후 응용 프로그램입니다.

## <a name="download-hello-sample-code"></a>Hello 샘플 코드 다운로드
[GitHub에서](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c) Azure AD B2C와 함께 AppAuth를 사용하는 작업 샘플이 제공됩니다. Hello 코드를 다운로드 하 고 실행할 수 있습니다. toouse 자신의 Azure AD B2C 테 넌 트를 hello 지침 hello에 따라 [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md)합니다.

이 샘플은 hello 하 여 hello README 지침에 따라 만들어졌습니다 [GitHub의 iOS AppAuth 프로젝트](https://github.com/openid/AppAuth-iOS)합니다. Hello 샘플 및 hello 라이브러리의 작동 방식에 대 한 자세한 내용은 hello GitHub에서 AppAuth 추가 정보를 참조 합니다.

## <a name="modifying-your-app-toouse-azure-ad-b2c-with-appauth"></a>Azure AD B2C AppAuth와 사용자 응용 프로그램 toouse 수정

> [!NOTE]
> AppAuth는 iOS 7 이상을 지원합니다.  그러나 iOS 9 이상이 필요로 하 toosupport Google, SFSafariViewController에서 소셜 로그인이 필요 합니다.
>

### <a name="configuration"></a>구성

권한 부여 끝점 hello와 토큰 끝점 Uri 지정 하 여 Azure AD B2C와 통신을 구성할 수 있습니다.  toogenerate 다음 정보는 hello 해야 이러한 Uri:
* 테넌트 ID(예: contoso.onmicrosoft.com)
* 정책 이름(예: B2C\_1\_SignUpIn)

hello 토큰 끝점 URI를 대체 하 여 생성할 수 hello 테 넌 트\_ID와 hello 정책\_hello url에 이름:

```objc
static NSString *const tokenEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/token";
```

hello 권한 부여 끝점 URI를 대체 하 여 생성할 수 hello 테 넌 트\_ID와 hello 정책\_hello url에 이름:

```objc
static NSString *const authorizationEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/authorize";
```

다음 코드 toocreate hello AuthorizationServiceConfiguration 개체를 실행 합니다.

```objc
OIDServiceConfiguration *configuration = 
    [[OIDServiceConfiguration alloc] initWithAuthorizationEndpoint:authorizationEndpoint tokenEndpoint:tokenEndpoint];
// now we are ready tooperform hello auth request...
```

### <a name="authorizing"></a>권한 부여

권한 부여 서비스 구성을 구성하거나 검색하면 권한 부여 요청을 생성할 수 있습니다. 다음 정보는 hello 필요한 toocreate hello 요청:  
* 클라이언트 ID(예: 00000000-0000-0000-0000-000000000000)
* 사용자 지정 스키마를 사용하는 리디렉션 URI(예: com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect)

두 항목 모두 [앱을 등록](#create-an-application)할 때 저장해야 합니다.

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

프로그램 응용 프로그램 toohandle hello 리디렉션 toohello URI hello 사용자 지정 체계를 tooset, 프로그램 Info.pList에서 ' URL 구성표 ' tooupdate hello 목록이 필요합니다.
* Info.pList를 엽니다.
* ' 번들 OS 형식 코드 '와 같은 행 위에 놓고 클릭 hello \+ 기호입니다.
* Hello 새 행 'URL 형식을'의 이름을 바꿉니다.
* 'URL 형식' tooopen hello 트리의 hello 화살표 toohello 왼쪽을 클릭 합니다.
* Tooopen hello 트리 '0 항목' hello 화살표 toohello 왼쪽을 클릭 합니다.
* 항목 0 too'URL 구성표 아래에 첫 번째 항목을 이름을 바꿉니다.
* ' URL Schemes' tooopen hello 트리의 hello 화살표 toohello 왼쪽을 클릭 합니다.
* Hello 'Value' 열에는 빈 필드 toohello 왼쪽에 '' URL Schemes' 아래 ' 0 항목.  Hello 값 tooyour 응용 프로그램의 고유한 체계를 설정 합니다.  hello 값 redirectURL hello OIDAuthorizationRequest 개체를 만들 때 사용 된 hello 체계를 일치 해야 합니다.  이 샘플에서는 com.onmicrosoft.fabrikamb2c.exampleapp' hello 구성표'를 사용 했습니다.

Toohello 참조 [AppAuth 가이드](https://openid.github.io/AppAuth-iOS/) 어떻게 toocomplete hello hello 프로세스의 나머지 부분에 있습니다. Tooquickly 해야 할 경우 작업 중인 앱을 시작, 체크 아웃 [샘플](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c)합니다. Hello에 hello 단계를 따라 [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md) tooenter 자신의 Azure AD B2C 구성 합니다.

우리는 항상 열려 toofeedback 및 제안을! 이 항목에 문제가 발생 하거나이 콘텐츠를 개선 하기 위한 권장 사항이 있는 경우 hello hello 페이지 맨 아래에 사용자 의견 보내 주셔서 감사 합니다. 기능 요청에 대 한 추가 너무[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c)합니다.

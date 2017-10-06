---
title: "Azure Active Directory B2C: Android 응용 프로그램을 사용하여 토큰 가져오기 | Microsoft Docs"
description: "이 문서에서는 보여 어떻게 toocreate AppAuth Azure Active Directory B2C toomanage 사용자 id를 사용 하 고 사용자를 인증 하는 Android 응용 프로그램입니다."
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
ms.openlocfilehash: 0236398673115a34951f035cb1e73e89417abf86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-sign-in-using-an-android-application"></a>Azure AD B2C: Android 응용 프로그램을 사용하여 로그인

hello Microsoft id 플랫폼 OAuth2 및 OpenID Connect와 같은 개방형 표준을 사용합니다. 이렇게 하면 개발자가 tooleverage 우리의 서비스로 toointegrate 만들려는 모든 라이브러리입니다. 다른 라이브러리와 플랫폼을 사용 하 여 tooaid 개발자 작성 했습니다이 하나의 toodemonstrate와 같은 몇 가지 연습 어떻게 tooconfigure 3rd 파티 라이브러리 tooconnect toohello Microsoft id 플랫폼입니다. 구현 하는 대부분의 라이브러리 [hello RFC6749 OAuth2 사양](https://tools.ietf.org/html/rfc6749) 수 tooconnect toohello Microsoft Id 플랫폼 됩니다.

> [!WARNING]
> Microsoft는 타사 라이브러리에 대한 수정 사항을 제공하지 않으며 이러한 라이브러리의 검토를 완료하지 않았습니다. 이 샘플 테스트 된 AppAuth hello Azure AD B2C로 기본 시나리오의 호환성에 대 한 호출 3rd 파티 라이브러리를 사용 중입니다. 문제 및 기능 요청 toohello 방향이 지정 된 라이브러리의 오픈 소스 프로젝트 여야 합니다. 자세한 내용은 [이 문서](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries)를 참조하세요.  
>
>

이 예제 구성의 대부분 새 tooOAuth2 또는 OpenID Connect 경우 많은 의미 tooyou를 하면 안 됩니다. 간단한 보면 하는 것이 좋습니다 [여기 기록할 म hello 프로토콜 개요](active-directory-b2c-reference-protocols.md)합니다.

## <a name="get-an-azure-ad-b2c-directory"></a>Azure AD B2C 디렉터리 가져오기

Azure AD B2C를 사용하기 전에 디렉터리 또는 테넌트를 만들어야 합니다. 디렉터리는 모든 사용자, 앱, 그룹 등을 위한 컨테이너입니다. 디렉터리가 없는 경우 계속하기 전에 [B2C 디렉터리를 만듭니다](active-directory-b2c-get-started.md) .

## <a name="create-an-application"></a>응용 프로그램 만들기

다음으로 응용 프로그램 toocreate B2C 디렉터리에 있어야합니다. 이렇게 하면 Azure AD 필요한 정보를 안전 하 게 응용 프로그램과 함께 toocommunicate 있습니다. toocreate 모바일 앱에 따라 [이러한 지침](active-directory-b2c-app-registration.md)합니다. 다음을 수행해야 합니다.

* 포함 된 **Native Client** hello 응용 프로그램에 있습니다.
* 복사 hello **응용 프로그램 ID** 할당된 tooyour 앱입니다. 이 ID는 나중에 필요합니다.
* 네이티브 클라이언트 **리디렉션 URI**(예: com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect)를 설정합니다. 이 ID는 나중에도 필요합니다.

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>정책 만들기

Azure AD B2C에서 모든 사용자 환경은 [정책](active-directory-b2c-reference-policies.md)에 의해 정의됩니다. 이 앱은 결합된 로그인 및 등록의 하나의 ID 환경을 포함합니다. 필요한 toocreate이이 정책에 설명 된 대로 [정책 참조 문서](active-directory-b2c-reference-policies.md#create-a-sign-up-policy)합니다. Hello 정책을 만들 때 야 합니다.

* Hello 선택 **표시 이름** 등록 정책에 특성으로 합니다.
* Hello 선택 **표시 이름** 및 **개체 ID** 모든 정책에 대 한 응용 프로그램 클레임입니다. 물론 다른 클레임을 선택할 수 있습니다.
* 복사 hello **이름** 를 만든 후 각 정책의 합니다. Hello 접두사 있어야 `b2c_1_`합니다.  Hello 정책 이름을 나중에 필요 합니다.

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

준비 toobuild 하 여 정책을 만든 후 응용 프로그램입니다.

## <a name="download-hello-sample-code"></a>Hello 샘플 코드 다운로드

[GitHub에서](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c) Azure AD B2C와 함께 AppAuth를 사용하는 작업 샘플이 제공됩니다. Hello 코드를 다운로드 하 고 실행할 수 있습니다. 있습니다 수 빠르게 시작 자신의 Azure AD B2C 구성을 사용 하 여 hello에 hello 지침에 따라 사용자 고유의 응용 프로그램 [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md)합니다.

hello 샘플에서 제공 하는 hello 샘플을 수정은 [AppAuth](https://openid.github.io/AppAuth-Android/)합니다. 해당 페이지 toolearn AppAuth 및 해당 기능에 대 한 자세한 참조 하십시오.

## <a name="modifying-your-app-toouse-azure-ad-b2c-with-appauth"></a>Azure AD B2C AppAuth와 사용자 응용 프로그램 toouse 수정

> [!NOTE]
> AppAuth는 Android API 16(Jellybean) 이상을 지원합니다. API 23 이상을 사용하는 것이 좋습니다.
>

### <a name="configuration"></a>구성

나 중 하나가 지정 하 여 hello 검색 URI hello 권한 부여 끝점와 토큰 끝점 Uri 지정 하 여 Azure AD B2C와 통신을 구성할 수 있습니다. 두 경우 모두 다음 정보는 hello이 필요 합니다.

* 테넌트 ID(예: contoso.onmicrosoft.com)
* 정책 이름(예: B2C\_1\_SignUpIn)

Tooautomatically hello 권한 부여 및 토큰 끝점 Uri를 검색, hello 검색 URI에서에서 toofetch 정보가 필요 합니다를 선택 하는 경우. hello 테 넌 트를 대체 하 여 URI를 생성할 수 hello 검색\_ID와 hello 정책\_hello url에 이름:

```java
String mDiscoveryURI = "https://login.microsoftonline.com/<Tenant_ID>/v2.0/.well-known/openid-configuration?p=<Policy_Name>";
```

그런 다음 hello 권한 부여 및 토큰 끝점 Uri 획득 하 고 hello 다음을 실행 하 여 AuthorizationServiceConfiguration 개체를 만들 수 있습니다.

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
            Log.w(TAG, "Failed tooretrieve configuration for " + issuerUri, ex);
        } else {
            // service configuration retrieved, proceed tooauthorization...
        }
      }
  });
```

검색 tooobtain hello 권한 부여 및 토큰 끝점 Uri 사용 하는 대신 지정할 수도 있습니다에 명시적으로 hello 테 넌 트를 대체 하 여\_ID와 hello 정책\_아래 hello URL에 이름:

```java
String mAuthEndpoint = "https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/authorize?p=<Policy_Name>";

String mTokenEndpoint = "https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/token?p=<Policy_Name>";
```

다음 코드 toocreate hello AuthorizationServiceConfiguration 개체를 실행 합니다.

```java
AuthorizationServiceConfiguration config =
        new AuthorizationServiceConfiguration(name, mAuthEndpoint, mTokenEndpoint);

// perform hello auth request...
```

### <a name="authorizing"></a>권한 부여

권한 부여 서비스 구성을 구성하거나 검색하면 권한 부여 요청을 생성할 수 있습니다. 다음 정보는 hello 해야 toocreate hello 요청:

* 클라이언트 ID(예: 00000000-0000-0000-0000-000000000000)
* 사용자 지정 스키마를 사용하는 리디렉션 URI(예: com.onmicrosoft.fabrikamb2c.exampleapp://oauthredirect)

두 항목 모두 [앱을 등록](#create-an-application)할 때 저장해야 합니다.

```java
AuthorizationRequest req = new AuthorizationRequest.Builder(
    config,
    clientId,
    ResponseTypeValues.CODE,
    redirectUri)
    .build();
```

Toohello를 참조 하십시오 [AppAuth 가이드](https://openid.github.io/AppAuth-Android/) 어떻게 toocomplete hello hello 프로세스의 나머지 부분에 있습니다. Tooquickly 해야 할 경우 작업 중인 앱을 시작, 체크 아웃 [샘플](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c)합니다. Hello에 hello 단계를 따라 [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md) tooenter 자신의 Azure AD B2C 구성 합니다.

우리는 항상 열려 toofeedback 및 제안을! 이 항목에 문제가 발생 하거나이 콘텐츠를 개선 하기 위한 권장 사항이 있는 경우 hello hello 페이지 맨 아래에 사용자 의견 보내 주셔서 감사 합니다. 기능 요청에 대 한 추가 너무[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c)합니다.


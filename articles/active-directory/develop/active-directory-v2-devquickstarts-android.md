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
# <a name="add-sign-in-tooan-android-app-using-a-third-party-library-with-graph-api-using-hello-v20-endpoint"></a>타사 라이브러리를 사용 하 여 Graph api v 2.0 끝점 hello를 사용 하 여 로그인 tooan Android 앱 추가
hello Microsoft id 플랫폼 OAuth2 및 OpenID Connect와 같은 개방형 표준을 사용합니다. 개발자는 서비스와 toointegrate 원하는 모든 라이브러리를 사용할 수 있습니다. toohelp 개발자 플랫폼을 사용 하 여 다른 라이브러리와을 작성 했습니다이 하나의 toodemonstrate와 같은 몇 가지 연습 어떻게 tooconfigure 타사 라이브러리 tooconnect toohello Microsoft id 플랫폼입니다. 구현 하는 대부분의 라이브러리 [hello RFC6749 OAuth2 사양](https://tools.ietf.org/html/rfc6749) toohello Microsoft id 플랫폼을 연결할 수 있습니다.

사용자는이 연습에서 만들어지는 hello 응용 프로그램을 사용 하 여 한 tootheir 조직 로그인 hello Graph API를 사용 하 여 조직에서 자신에 대 한을 검색할 수 있습니다.

이 예제 구성의 많은 새로운 tooOAuth2 또는 OpenID Connect를 사용 하는 경우 의미 tooyou를 하면 안 됩니다. 배경 지식을 위해 [2.0 프로토콜 - OAuth 2.0 권한 부여 코드 흐름](active-directory-v2-protocols-oauth-code.md)을 읽어보는 것이 좋습니다.

> [!NOTE]
> OAuth2 hello 또는 조건부 액세스 및 Intune 정책 관리와 같은 OpenID Connect 표준을 식에서 없는 플랫폼의 일부 기능 있습니다 toouse 우리의 오픈 소스 Microsoft Azure Identity 라이브러리를 필요 합니다.
> 
> 

hello v2.0 끝점에는 모든 Azure Active Directory 시나리오 및 기능을 지원 하지 않습니다.

> [!NOTE]
> 에 대해 알아보세요 hello v2.0 끝점을 사용 해야 하는 경우 toodetermine [v2.0 제한](active-directory-v2-limitations.md)합니다.
> 
> 

## <a name="download-hello-code-from-github"></a>GitHub에서 hello 코드를 다운로드 합니다.
이 자습서에 대 한 hello 코드 유지 관리 [GitHub에서](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2)합니다.  수에 따라 toofollow, [.zip으로 hello 응용 프로그램의 기본 정의 다운로드](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2/archive/skeleton.zip) 또는 복제 hello 스 켈 레 톤:

```
git clone --branch skeleton git@github.com:Azure-Samples/active-directory-android-native-oidcandroidlib-v2.git
```

Hello 샘플을 다운로드할 수도 수 고를 지금 시작:

```
git@github.com:Azure-Samples/active-directory-android-native-oidcandroidlib-v2.git
```

## <a name="register-an-app"></a>앱 등록
Hello에 새 앱 만들기 [응용 프로그램 등록 포털](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), 또는 hello 세부 단계에 따라 [어떻게 tooregister hello v2.0 끝점을 사용 하 여 앱](active-directory-v2-app-registration.md)합니다.  다음을 수행해야 합니다.

* 복사 hello **응용 프로그램 Id** 할당된 tooyour 응용 프로그램은 곧 필요 하기 때문입니다.
* Hello 추가 **모바일** 응용 프로그램을 위한 플랫폼입니다.

> 참고: hello 응용 프로그램 등록 포털에서 제공 된 **리디렉션 URI** 값입니다. 그러나이 예제에서 사용 해야 hello 기본값인 `https://login.microsoftonline.com/common/oauth2/nativeclient`합니다.
> 
> 

## <a name="download-hello-nxoauth2-third-party-library-and-create-a-workspace"></a>Hello NXOAuth2 타사 라이브러리를 다운로드 하 고 작업 영역 만들기
이 연습에서는 OAuth2 라이브러리인 hello Google의 OpenID Connect 코드에 따라 GitHub에서 OIDCAndroidLib hello를 사용 합니다. Hello 네이티브 응용 프로그램 프로필을 구현 하 고 hello 사용자의 hello 권한 부여 끝점을 지원 합니다. 이들은 toointegrate hello Microsoft id 플랫폼을 사용 해야 하는 모든 hello 것입니다.

Hello OIDCAndroidLib 리포지토리 tooyour 컴퓨터를 복제 합니다.

```
git@github.com:kalemontes/OIDCAndroidLib.git
```

![androidStudio](../media/active-directory-android-native-oidcandroidlib-v2/emotes-url.png)

## <a name="set-up-your-android-studio-environment"></a>Android Studio 환경 설정
1. 새 Android Studio 프로젝트를 만들고 hello 마법사에서 hello 기본값을 적용 합니다.
   
    ![Android Studio에서 새 프로젝트 만들기](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample1.PNG)
   
    ![대상 Android 장치](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample2.PNG)
   
    ![활동 toomobile 추가](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample3.PNG)
2. tooset 프로젝트 모듈을 복제 하는 hello 리포지토리 toohello 프로젝트 위치를 이동 합니다. 또한 hello 프로젝트를 만들 수 있으며 다음 복제 직접 toohello 프로젝트 위치 수 없습니다.
   
    ![프로젝트 모듈](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample4_1.PNG)
3. Hello 상황에 맞는 메뉴를 사용 하 여 또는 hello Ctrl + Alt + Maj + S 바로 가기를 사용 하 여 hello 프로젝트 모듈 설정을 엽니다.
   
    ![프로젝트 모듈 설정](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample4.PNG)
4. Hello 프로젝트 컨테이너 설정만 하려고 하기 때문에 hello 기본 응용 프로그램 모듈을 제거 합니다.
   
    ![hello 기본 응용 프로그램 모듈](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample5.PNG)
5. Hello 복제 된 리포지토리 toohello 현재 프로젝트에서 모듈을 가져옵니다.
   
    ![Gradle 프로젝트 가져오기](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample6.PNG) ![새 모듈 페이지 만들기](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample7.PNG)
6. Hello에 대 한 이러한 단계를 반복 `oidlib-sample` 모듈입니다.
7. Hello에 대 한 hello oidclib 종속성 확인 `oidlib-sample` 모듈입니다.
   
    ![hello oidlib 샘플 모듈에 대 한 oidclib 종속성](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample8.PNG)
8. **확인** 을 클릭하고 Gradle 동기화를 대기합니다.
   
    설정은 gradle처럼 보여야 합니다.
   
    ![settings.gradle의 스크린샷](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample8_1.PNG)
9. Hello 샘플 앱 toomake 있는지 빌드 제대로 실행 되 고 hello 샘플에 해당 합니다.
   
    있습니다 수 없습니다 수 toouse이 Azure Active Directory와 아직 합니다. 해야 tooconfigure 일부 끝점 우선 합니다. 이 hello 샘플 응용 프로그램을 사용자 지정을 시작 하기 전에 Android Studio 문제 없는 tooensure입니다.
10. 빌드 및 실행 `oidlib-sample` Android Studio에서 hello 대상으로 합니다.
    
    ![oidlib-sample 빌드의 진행률](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample9.png)
11. Hello 삭제 `app ` Android Studio 안전을를 삭제 하지 않으므로 hello 프로젝트에서 hello 모듈을 제거 하는 경우 남아 있는 디렉터리입니다.
    
    ![Hello 응용 프로그램 디렉터리를 포함 하는 파일 구조](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample12.PNG)
12. 열기 hello **구성 편집** hello 프로젝트에서 hello 모듈을 제거 하는 경우에 두었습니다 메뉴 tooremove 실행 hello 구성 합니다.
    
    ![구성 편집 메뉴](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample10.PNG)
    ![앱의 구성 실행](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample11.PNG)

## <a name="configure-hello-endpoints-of-hello-sample"></a>Hello 샘플의 hello 끝점 구성
Hello 했으므로 `oidlib-sample` 성공적으로 실행 편집 일부 끝점 tooget이 Azure Active Directory를이 사용 합니다.

### <a name="configure-your-client-by-editing-hello-oidcclientconfxml-file"></a>클라이언트 hello oidc_clientconf.xml 파일을 편집 하 여 구성
1. OAuth2 흐름만 tooget 토큰을 사용 하는 hello Graph API를 호출 하므로 hello 클라이언트 toodo OAuth2만 설정 합니다. OIDC에 대해서는 향후 예제에서 다룹니다.
   
    ```xml
        <bool name="oidc_oauth2only">true</bool>
    ```
2. Hello 등록 포털에서 받은 클라이언트 ID를 구성 합니다.
   
    ```xml
        <string name="oidc_clientId">86172f9d-a1ae-4348-aafa-7b3e5d1b36f5</string>
        <string name="oidc_clientSecret"></string>
    ```
3. 아래 하나 hello로 리디렉션 URI를 구성 합니다.
   
    ```xml
        <string name="oidc_redirectUrl">https://login.microsoftonline.com/common/oauth2/nativeclient</string>
    ```
4. 범위는 하면 필요한 순서 tooaccess에 hello Graph API를 구성 합니다.
   
    ```xml
        <string-array name="oidc_scopes">
            <item>openid</item>
            <item>https://graph.microsoft.com/User.Read</item>
            <item>offline_access</item>
        </string-array>
    ```

hello `User.Read` 값 `oidc_scopes` 있습니다 tooread hello 기본 프로필 hello 사용자 로그인을 허용 합니다.
모든 hello 사용할 수 있는 범위에 대해 자세히 알아볼 수 있습니다 [Microsoft Graph 사용 권한 범위](https://graph.microsoft.io/docs/authorization/permission_scopes)합니다.

`openid` 또는 `offline_access`를 OpenID Connect의 범위로 구분해서 설명하는 내용을 보려면, [2.0 프로토콜 - OAuth 2.0 권한 부여 코드 흐름](active-directory-v2-protocols-oauth-code.md)을 참조하세요.

### <a name="configure-your-client-endpoints-by-editing-hello-oidcendpointsxml-file"></a>Hello oidc_endpoints.xml 파일을 편집 하 여 클라이언트 끝점 구성
* 열기 hello `oidc_endpoints.xml` 파일을 hello 다음 변경 내용을 확인 하십시오.
  
    ```xml
    <!-- Stores OpenID Connect provider endpoints. -->
    <resources>
        <string name="op_authorizationEnpoint">https://login.microsoftonline.com/common/oauth2/v2.0/authorize</string>
        <string name="op_tokenEndpoint">https://login.microsoftonline.com/common/oauth2/v2.0/token</string>
        <string name="op_userInfoEndpoint">https://www.example.com/oauth2/userinfo</string>
        <string name="op_revocationEndpoint">https://www.example.com/oauth2/revoketoken</string>
    </resources>
    ```

OAuth2를 프로토콜로 사용하는 경우 이러한 끝점은 변경되어서는 안됩니다.

> [!NOTE]
> 에 대 한 끝점 hello `userInfoEndpoint` 및 `revocationEndpoint` Azure Active Directory에서 현재 지원 되지 않습니다. Hello example.com 기본값을 가진 두면 알려줍니다는 사용할 수 없는 경우 hello 샘플:-)
> 
> 

## <a name="configure-a-graph-api-call"></a>Graph API 호출 구성
* 열기 hello `HomeActivity.java` 파일을 hello 다음 변경 내용을 확인 하십시오.
  
    ```Java
       //TODO: set your protected resource url
        private static final String protectedResUrl = "https://graph.microsoft.com/v1.0/me/";
    ```

여기에 나오는 간단한 Graph API 호출이 예제 정보를 반환합니다.

Toodo 해야 하는 모든 hello 변경 내용을 모두입니다. Hello 실행 `oidlib-sample` 응용 프로그램을 마우스 클릭 **로그인**합니다.

성공적으로 인증 한 후 선택 hello **보호 된 리소스 요청** tootest 프로그램 호출 toohello Graph API 단추입니다.

## <a name="get-security-updates-for-our-product"></a>당사 제품에 대한 보안 업데이트 가져오기
사용자는 좋습니다 보안 사고에 대 한 알림을 tooget hello를 방문 하 여 [보안 TechCenter](https://technet.microsoft.com/security/dd252948) 및 tooSecurity 자문 경고를 구독 합니다.


---
title: "aaaHow tooenable에 ADAL을 사용 하 여 Android 응용 프로그램 간 SSO | Microsoft Docs"
description: "어떻게 toouse hello 기능을 응용 프로그램에서 Single Sign On ADAL SDK tooenable hello 합니다. "
services: active-directory
documentationcenter: 
author: danieldobalian
manager: mbaldwin
editor: 
ms.assetid: 40710225-05ab-40a3-9aec-8b4e96b6b5e7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: android
ms.devlang: java
ms.topic: article
ms.date: 04/07/2017
ms.author: dadobali
ms.custom: aaddev
ms.openlocfilehash: 3867e15030e5516464e4dbd92ba35894430daf00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooenable-cross-app-sso-on-android-using-adal"></a>어떻게 tooenable ADAL을 사용 하 여 android 응용 프로그램 간 SSO
사용자가 tooenter 자격 증명을 한 번만 필요 하 고 응용 프로그램에서 자동으로 회사 자격 증명을 갖게 있도록 Single Sign-on (SSO)를 제공 하 이제에서 예상 하는 고객 합니다. hello 어려움 작은 화면에 종종 시간 전화 통화 또는 문자로 전송 코드와 같은 추가 요소 (2FA)와 함께 자신의 사용자 이름과 암호를 입력 하는 경우 사용자 빠른 불만에 결과 toodo이 제품에 대 한 번 이상 있습니다.

또한 Microsoft 계정 또는 office 365에서 작업 계정과 같은 다른 응용 프로그램이 사용할 수 있는 id 플랫폼에 적용 하면 고객이 자신의 모든 응용 프로그램에서 이러한 자격 증명 toobe 사용 가능한 toouse hello 공급 업체 관계 없이 예상 합니다.

hello 우리의 Microsoft Identity Sdk와 함께 Microsoft Id 플랫폼 모든이 하드 작업을 수행 하 고 기능 toodelight SSO 하거나 응용 프로그램 또는 사용자 고유의 도구 모음 내에서 사용 하는 고객을 hello 제공 브로커 기능 및 인증자 hello 전체 장치에서 응용 프로그램

이 연습에서는 열에 표시 방법을 tooconfigure 우리의 SDK 응용 프로그램 tooprovide 내에서이 혜택 tooyour 고객 합니다.

이 연습은 다음에 적용됩니다.

* Azure Active Directory
* Azure Active Directory B2C
* Azure Active Directory B2B
* Azure Active Directory 조건부 액세스

위의 hello 문서 너무 방법을 알고 있는 것으로 가정[Azure Active Directory에 대 한 hello 레거시 포털에서 응용 프로그램을 프로 비전](active-directory-how-to-integrate.md) hello로 응용 프로그램 통합 및 [Microsoft Identity Android SDK](https://github.com/AzureAD/azure-activedirectory-library-for-android) .

## <a name="sso-concepts-in-hello-microsoft-identity-platform"></a>Microsoft Id 플랫폼 hello에 대 한 SSO 개념
### <a name="microsoft-identity-brokers"></a>Microsoft ID Broker
Microsoft hello 여러 공급 업체의 응용 프로그램 전체에서 자격 증명의 브리징에 대 한 허용 하는 모든 모바일 플랫폼에 대 한 응용 프로그램을 제공 하 고 어디에서 단일 안전한 곳을 필요로 하는 특별 한 향상 된 기능에 대 한 허용 toovalidate 자격 증명입니다. 이를 **브로커**라고 합니다. IOS 및 Android에서 고객에 독립적으로 설치 하거나 해당 직원에 대 한 일부 또는 모두 hello 장치를 관리 하는 회사에서 장치 toohello 푸시할 수는 다운로드 가능한 응용 프로그램을 통해 제공 됩니다 이러한. 이러한 브로커 일부 응용 프로그램 및 IT 관리자의 필요에 따라 hello 전체 장치에 대 한 관리 보안을 지원 합니다. Windows에서 기술적으로 웹 인증 브로커 hello 라고 toohello 운영 체제에서 기본적으로 제공 하는 계정 선택 하 여이 기능을 제공 합니다.

방법에 대 한 자세한 내용은 이러한 브로커 및 방법을 고객에 게 표시 될 수 하 hello Microsoft Id 플랫폼에 대 한 읽기에 대 한 자신의 로그인 흐름에 사용 합니다.

### <a name="patterns-for-logging-in-on-mobile-devices"></a>모바일 장치에 로그인하기 위한 패턴
장치에 대 한 액세스 toocredentials hello Microsoft Identity 플랫폼에 대 한 두 가지 기본 패턴을 따릅니다.

* 비 브로커 지원 로그인
* 브로커 지원 로그인

#### <a name="non-broker-assisted-logins"></a>비 브로커 지원 로그인
비 브로커 보조 로그인은 hello 응용 프로그램을 사용 하 여 인라인으로 발생 하지 않으며 해당 응용 프로그램에 대 한 hello 장치에서 hello 로컬 저장소를 사용 하는 로그인 환경을 제공 합니다. 이 저장소는 응용 프로그램 간에 공유 될 수 있습니다 하지만 hello 자격 증명이 밀접 하 게 toohello 응용 프로그램 또는 제품군이 자격 증명을 사용 하는 앱입니다. 경험해 본 있다면 대개이 많은 모바일 응용 프로그램에서 사용자 이름 및 hello 응용 프로그램 자체 내에 암호를 입력 합니다.

이러한 로그인 hello 이점을 뒤에

* Hello 응용 프로그램 내 사용자 환경이 있습니다.
* Hello로 서명 된 응용 프로그램에서 자격 증명을 공유할 수 동일한 인증서를 응용 프로그램 single sign on 환경을 tooyour 제품군을 제공 합니다.
* 로깅 hello 환경 전체에 제어를 이전 및 이후 로그인 toohello 응용 프로그램에 제공 됩니다.

이러한 로그인 있어야 hello 다음 단점이 있습니다.

* 사용자는 Microsoft ID를 사용하는 모든 앱이 아닌 응용 프로그램이 구성한 해당 Microsoft ID 간에서만 Single Sign-On을 경험할 수 있습니다.
* 응용 프로그램을 사용 하 여 hello InTune 제품군 또는 조건부 액세스 등의 고급 비즈니스 기능으로 사용할 수 없습니다.
* 응용 프로그램은 비즈니스 사용자에 대한 인증서 기반 인증을 지원할 수 없습니다.

Microsoft Identity Sdk hello 프로그램 응용 프로그램 tooenable SSO의 hello 공유 저장소에서 작동 하는 방법에 대 한 표현을 다음과 같습니다.

```
+------------+ +------------+  +-------------+
|            | |            |  |             |
|   App 1    | |   App 2    |  |   App 3     |
|            | |            |  |             |
|            | |            |  |             |
+------------+ +------------+  +-------------+
| Azure SDK  | | Azure SDK  |  | Azure SDK   |
+------------+-+------------+--+-------------+
|                                            |
|            App Shared Storage              |
+--------------------------------------------+
```

#### <a name="broker-assisted-logins"></a>브로커 지원 로그인
Broker 기반 로그인에는 hello 저장 및 hello 브로커 tooshare 자격 증명의 보안을 사용 하 여 hello Microsoft Id 플랫폼을 적용 하는 hello 장치에서 모든 응용 프로그램 사이의 hello broker 응용 프로그램 내에서 발생 하는 로그인 환경이 되어 있습니다. 이 응용 프로그램의 hello 브로커 toosign 사용자가 사용 한다는 것을 의미 합니다. IOS 및 Android에서 이러한 브로커는 고객에 독립적으로 설치 하거나 해당 사용자에 대 한 hello 장치를 관리 하는 회사에서 장치 toohello 푸시할 수는 다운로드 가능한 응용 프로그램을 통해 제공 됩니다. 이러한 유형의 응용 프로그램의 예는 iOS에서 hello Microsoft Authenticator 응용 프로그램입니다. Windows 웹 인증 브로커 hello 라고 기술적으로 toohello 운영 체제에서 기본적으로 제공 하는 계정 선택 하 여이 기능을 제공 합니다.
hello 경험 플랫폼에 따라 다르며 하며 중단 toousers 수 되지 않은 경우 올바르게 관리 합니다. 익숙한 아마도 가장이 패턴 hello Facebook 응용 프로그램이 설치 된 다른 응용 프로그램에서 Facebook Connect를 사용 하는 경우. hello Microsoft Identity 플랫폼 사용 하 여 hello 같은 패턴입니다.

IOS에 대 한이 인해 tooa "전환" 애니메이션 전송 대상에 응용 프로그램 toohello 백그라운드 hello Microsoft Authenticator 응용 프로그램 사용자 tooselect hello에 대 한 toohello 전경 제공 사용한 toosign 만족할 만한 계정.  

Android 및 Windows hello 계정에 대 한 선택은 덜 중단 toohello 사용자는 응용 프로그램 맨 위에 표시 됩니다.

#### <a name="how-hello-broker-gets-invoked"></a>Hello broker가 호출 하는 방법
호환 되는 broker hello Microsoft Authenticator 응용 프로그램, Microsoft Identity Sdk hello가 자동으로 같은 hello 장치가에 설치 된 경우에 사용자 toolog에서 모든 계정을 사용 하 여 만들려는 되었음을 나타낼 때 사용자에 대 한 hello 브로커 호출 작업 hello 수행 hello Microsoft Identity 플랫폼입니다. 이 계정은 개인 Microsoft 계정, 회사 또는 학교 계정 또는 B2C 및 B2B 제품을 사용하여 Azure에 제공 및 호스트하는 계정일 수 있습니다. 
 
 #### <a name="how-we-ensure-hello-application-is-valid"></a>올바른지 hello 응용 프로그램 인지 확인 하는 방법
 
 응용 프로그램 호출 hello 브로커 hello 필요 tooensure hello id가 중요 한 toohello 보안에서 지원 되는 broker 로그인을 제공 합니다. IOS 나 Android 악성 응용 프로그램이 "스푸핑"는 올바른 응용 프로그램의 식별자를 업데이트 하 고 hello 합법적인 응용 프로그램을 위한 hello 토큰을 수신할 수 있습니다 하므로 지정된 된 응용 프로그램에 대해서만 사용할 수 있는 고유 식별자를 적용 합니다. 런타임 시 hello 오른쪽 응용 프로그램과 알립니다 항상 tooensure, 반드시 hello 개발자 tooprovide 사용자 지정 redirectURI Microsoft와 응용 프로그램을 등록할 때 합니다. **개발자가 이 리디렉션 URI를 만드는 방법은 아래에 자세히 설명되어 있습니다.** 이 사용자 지정 redirectURI hello 응용 프로그램의 hello 인증서 지문을 있어서 hello Google Play 스토어에 의해 toobe 고유 toohello 응용 프로그램을 보장 됩니다. 응용 프로그램 호출 hello 브로커 hello 브로커 hello Android 운영 체제 tooprovide 요청 hello와 인증서 지문을 해당 호출된 hello 브로커 합니다. hello broker hello 호출 tooour id 시스템에이 인증서 지문 tooMicrosoft를 제공합니다. Hello 응용 프로그램의 지문 hello 인증서 지문에 맞지 않는 hello 인증서를 제공 하면 hello 개발자가 toous 등록 하는 동안에서는 액세스를 거부할 toohello 토큰 hello 리소스 hello 응용 프로그램이 요청에 대 한 합니다. 이 검사는 hello 개발자가 등록 된 hello 응용 프로그램이 토큰 수신 되는지 확인 합니다.

**hello 개발자는 Microsoft Identity SDK hello hello 브로커를 호출 하거나 hello 비 브로커 보조 흐름을 사용 하는 경우 hello 선택을 있습니다.** 그러나 하지 toouse hello 브로커 기반 흐름을 선택 하는 hello 개발자의 경우 이러한 hello의 이점을 잃게 SSO 자격 증명을 사용 하 여 해당 hello 사용자 hello 장치에 이미 추가한 수 없고을 Microsoft 비즈니스 기능과 함께 사용 하는 응용 프로그램 조건부 액세스, Intune 관리 기능 및 인증서 기반 인증 같은 고객을 제공합니다.

이러한 로그인 hello 이점을 뒤에

* Hello 공급 업체에 관계 없이 자신의 모든 응용 프로그램에 SSO를 경험 하는 사용자입니다.
* 응용 프로그램 조건부 액세스 등의 고급 비즈니스 기능을 사용 하거나 제품 hello InTune 그룹을 사용할 수 있습니다.
* 응용 프로그램은 비즈니스 사용자에 대한 인증서 기반 인증을 지원할 수 있습니다.
* 훨씬 더 안전한 로그인 환경의 hello broker 응용 프로그램 추가 보안 알고리즘 및 암호화가 hello hello 응용 프로그램 및 hello 사용자 신원을 확인 합니다.

이러한 로그인 있어야 hello 다음 단점이 있습니다.

* IOS에서 hello 사용자 자격 증명을 선택 하는 동안 응용 프로그램의 환경이 전환 됩니다.
* 응용 프로그램 내에서 고객에 대 한 hello 기능 toomanage hello 로그인의 손실 발생 합니다.

Hello Microsoft Identity Sdk 작업 hello로 응용 프로그램 tooenable SSO broker 하는 방법에 대 한 표현을 다음과 같습니다.

```
+------------+ +------------+   +-------------+
|            | |            |   |             |
|   App 1    | |   App 2    |   |   Someone   |
|            | |            |   |    Else's   |
|            | |            |   |     App     |
+------------+ +------------+   +-------------+
|  ADAL SDK  | |  ADAL SDK  |   |  ADAL SDK   |
+-----+------+-+-----+------+-  +-------+-----+
      |              |                  |
      |       +------v------+           |
      |       |             |           |
      |       | Microsoft   |           |
      +-------> Broker      |^----------+
              | Application
              |             |
              +-------------+
              |             |
              |   Broker    |
              |   Storage   |
              |             |
              +-------------+

```

이 배경 정보를 갖춘 있어야 수 toobetter 이해 하 고 hello Microsoft Id 플랫폼 및 Sdk를 사용 하 여 응용 프로그램 내에서 SSO를 구현 합니다.

## <a name="enabling-cross-app-sso-using-adal"></a>ADAL을 사용하여 앱 간 SSO 활성화
Hello ADAL Android SDK 사용 하 여 여기에:

* 앱 제품군에 대한 비 브로커 지원 SSO 설정
* 브로커 지원 SSO에 대한 지원 설정

### <a name="turning-on-sso-for-non-broker-assisted-sso"></a>비 브로커 지원 SSO에 대한 SSO 설정
비 브로커 보조 SSO 응용 프로그램 전반에 대 한 Microsoft Identity Sdk hello SSO의 hello 복잡성 많이를 관리 합니다. Hello 캐시에 hello 올바른 사용자를 찾아서 tooquery 있습니다에 대 한 로그인된 사용자의 목록을 유지 관리 포함 됩니다.

다음 toodo hello 필요를 소유 하는 응용 프로그램 전체에서 SSO tooenable:

1. 모든 사용자 응용 프로그램 사용자 hello 같은 클라이언트 ID 또는 id입니다. 응용 프로그램 확인
2. 모든 응용 프로그램이 동일한 SharedUserID 설정 hello 확인 하세요.
3. 모든 저장소를 공유할 수 있도록 hello Google Play에서에서 동일한 서명 인증서를 저장 하면 응용 프로그램 공유 hello 확인 합니다.

#### <a name="step-1-using-hello-same-client-id--application-id-for-all-hello-applications-in-your-suite-of-apps"></a>1 단계: 동일한 클라이언트 ID를 hello를 사용 하 여 / 응용 프로그램의 응용 프로그램 도구 모음에 모든 hello에 대 한 응용 프로그램 ID
Microsoft Identity 플랫폼 tooknow hello에 대 한 응용 프로그램에서 tooshare 토큰 수 있는지, 각 응용 프로그램이 있어야 tooshare hello 같은 클라이언트 ID 또는 응용 프로그램 id입니다. Hello 포털에서 첫 번째 응용 프로그램을 등록할 때 tooyou 제공한 hello 고유 식별자입니다.

다양 한 앱 식별 하는 방법 할까요 toohello Microsoft Id 서비스를 사용 하는 경우 hello 동일한 응용 프로그램 id입니다. hello 대답이 hello로 **리디렉션 Uri**합니다. 각 응용 프로그램에는 hello 등록 포털에 등록 한 리디렉션 Uri 여러 개 있을 수 있습니다. 제품의 각 앱은 다른 리디렉션 URI를 갖습니다. 표시되는 모양의 예는 다음과 같습니다.

App1 리디렉션 URI: `msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D`

App2 리디렉션 URI: `msauth://com.example.userapp1/KmB7PxIytyLkbGHuI%2UitkW%2Fejk%4E`

App3 리디렉션 URI: `msauth://com.example.userapp2/Pt85PxIyvbLkbKUtBI%2SitkW%2Fejk%9F`

....

아래에 중첩 된 이러한 동일한 클라이언트 ID를 hello / 응용 프로그램 ID 및 조회에 따라 hello에 대 한 리디렉션 URI SDK 구성에서 toous을 반환 합니다.

```
+-------------------+
|                   |
|  Client ID        |
+---------+---------+
          |
          |           +-----------------------------------+
          |           |  App 1 Redirect URI               |
          +----------^+                                   |
          |           +-----------------------------------+
          |
          |           +-----------------------------------+
          +----------^+  App 2 Redirect URI               |
          |           |                                   |
          |           +-----------------------------------+
          |
          +----------^+-----------------------------------+
                      |  App 3 Redirect URI               |
                      |                                   |
                      +-----------------------------------+

```


*이러한 리디렉션 Uri의 형식은 hello는 아래 설명 되어 있습니다. 이 경우 이러한 해야 다음과 같은 hello 위의 toosupport hello broker 싶지 않다면 모든 리디렉션 URI를 사용할 수 있습니다.*

#### <a name="step-2-configuring-shared-storage-in-android"></a>2단계: Android에서 공유 저장소 구성
설정 hello `SharedUserID` hello hello에 Google Android 설명서를 참조 하 여 피어에서 확인 될 수 있지만이 설명서의 hello 범위를 벗어납니다 [매니페스트](http://developer.android.com/guide/topics/manifest/manifest-element.html)합니다. 중요한 것은 사용자가 sharedUserID가 불리는 이름을 결정하는 것과 모든 응용 프로그램에서 이를 사용하는 것입니다.

Hello 있으면 `SharedUserID` 준비 toouse SSO는 응용 프로그램에서 합니다.

> [!WARNING]
> 응용 프로그램에서 저장소를 공유 하는 경우 모든 응용 프로그램 사용자를 삭제 하거나 나빠지는 지 응용 프로그램에서 모든 hello 토큰을 삭제할 수 있습니다. 이 hello 토큰 toodo 백그라운드 작업을 사용 하는 응용 프로그램의 경우에 특히 재해로입니다. 저장소를 공유 hello Microsoft Identity Sdk를 통해 모든 제거 작업에 특히 주의 이어야 한다는 것을 의미 합니다.
> 
> 

이것으로 끝입니다. 이제 Microsoft Identity SDK hello 응용 프로그램에서 자격 증명을 공유 합니다. hello 사용자 목록도 응용 프로그램 인스턴스 간에 공유 됩니다.

### <a name="turning-on-sso-for-broker-assisted-sso"></a>브로커 지원 SSO에 대한 SSO 설정
응용 프로그램 toouse hello 장치에 설치 되어 있는 모든 broker에 대 한 기능 hello **기본적으로 해제 되어**합니다. 순서로 toouse 응용 프로그램 hello 브로커와 몇 가지 추가 구성을 변경 하 고 일부 코드 tooyour 응용 프로그램을 추가 합니다.

hello 단계 toofollow가 됩니다.

1. 응용 프로그램 코드의 호출 toohello MS SDK에서에서 broker 모드를 사용 하도록 설정
2. 새 리디렉션 URI를 설정 하 고 해당 tooboth hello 앱 및 앱 등록을 제공 합니다.
3. 올바른 권한을 hello Android 매니페스트에서 hello 설정

#### <a name="step-1-enable-broker-mode-in-your-application"></a>1단계: 응용 프로그램에서 브로커 모드 활성화
"hello"설정 또는 인증 인스턴스의 초기 설정을 만들 때 응용 프로그램 toouse hello broker 프로그램에 대 한 hello 기능이 켜 집니다. 코드에서 ApplicationSettings 형식을 설정하여 이 작업을 수행합니다.

```
AuthenticationSettings.Instance.setUseBroker(true);
```


#### <a name="step-2-establish-a-new-redirect-uri-with-your-url-scheme"></a>2단계: URL 구성표와 함께 새 리디렉션 URI 설정
에 항상 반환 hello 자격 증명 토큰 toohello 올바른 응용 프로그램 순서 tooensure, toomake म 콜백할 hello Android 운영 체제가 설치 하는 방식으로 tooyour 응용 프로그램을 확인할 수 있는지 필요 합니다. hello Android 운영 체제 hello Google Play 스토어에에서 hello 인증서의 hello 해시를 사용합니다. 불량 응용 프로그램에서 이를 스푸핑할 수 없습니다. 따라서 활용 하 여이 hello hello 토큰 toohello 올바른 응용 프로그램으로 반환 됨 우리의 broker 응용 프로그램 tooensure의 URI와 함께 합니다. 필요 하면 tooestablish이 고유 리디렉션 URI를 모두 설정 하 여 응용 프로그램에서 리디렉션 URI로 우리의 개발자 포털에서.

Hello 적절 한 형태의 사용자 리디렉션 URI 이어야 합니다.

`msauth://packagename/Base64UrlencodedSignature`

예: *msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D*

이 리디렉션 URI toobe hello를 사용 하 여 응용 프로그램 등록에 지정 된 필요한 [Azure 포털](https://portal.azure.com/)합니다. Azure AD 앱 등록에 대한 자세한 내용은 [Azure Active Directory와 통합](active-directory-how-to-integrate.md)을 참조하세요.

#### <a name="step-3-set-up-hello-correct-permissions-in-your-application"></a>3 단계: 응용 프로그램에서 올바른 권한을 hello 설정
응용 프로그램 간에 hello Android OS toomanage 자격 증명의 hello 계정 관리자 기능을 사용 하는 Android에서 해당 broker 응용 프로그램입니다. Android에서 주문 toouse hello 브로커에서 응용 프로그램 매니페스트에 권한을 toouse AccountManager 계정이 있어야 합니다. Hello에 자세히 설명 되어 있음 [Google 계정 관리자에 대 한 설명서 센터의 설명서](http://developer.android.com/reference/android/accounts/AccountManager.html)

특히 이러한 사용 권한은 다음과 같습니다.

```
GET_ACCOUNTS
USE_CREDENTIALS
MANAGE_ACCOUNTS
```

### <a name="youve-configured-sso"></a>SSO를 구성했습니다.
이제 Microsoft Identity SDK hello에서는 자동으로 응용 프로그램에서 자격 증명을 공유를 자신의 장치에 표시 되지 않으면 hello 브로커를 호출 합니다.


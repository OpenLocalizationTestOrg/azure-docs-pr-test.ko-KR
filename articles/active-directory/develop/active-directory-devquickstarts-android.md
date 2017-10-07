---
title: "시작 하는 AD Android aaaAzure | Microsoft Docs"
description: "어떻게 toobuild 로그인 및 Azure AD 호출에 대 한 Azure AD와 통합 하는 Android 응용 프로그램 OAuth를 사용 하 여 Api를 보호 합니다."
services: active-directory
documentationcenter: android
author: danieldobalian
manager: mbaldwin
editor: 
ms.assetid: da1ee39f-89d3-4d36-96f1-4eabbc662343
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 01/07/2017
ms.author: dadobali
ms.custom: aaddev
ms.openlocfilehash: 1aedc8ff60874b405a182a4ccbfb2c8b4d9d3704
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-into-an-android-app"></a>Android 앱에 Azure AD 통합
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

> [!TIP]
> 새로운 우리의 hello 미리 보기를 사용 [개발자 포털](https://identity.microsoft.com/Docs/Android), 단 몇 분 후에 Azure AD와 실행 하는 데 도움이입니다. hello 개발자 포털에서는 응용 프로그램을 등록 하 고 코드에 Azure AD 통합 hello 과정을 단계별로 안내 합니다. 이 과정을 완료하면 테넌트에서 사용자를 인증할 수 있는 간단한 응용 프로그램 및 토큰을 수락하고 유효성 검사를 수행할 수 있는 백 엔드가 생성됩니다.
>
>

데스크톱 응용 프로그램을 개발 하는 경우 Azure Active Directory (Azure AD) 하면 간단 하 고 간단 하 게 하면 tooauthenticate 사용자가 자신의 온-프레미스 Active Directory 계정을 사용 하 여 있습니다. 응용 프로그램 toosecurely 해줍니다 모든 웹 Azure AD로 보호 되는 API를 사용와 같은 Office 365 Api hello 또는 Azure API를 환영 합니다.

Azure AD tooaccess 보호 된 리소스를 필요로 하는 Android 클라이언트에 대 한 Active Directory 인증 라이브러리 (ADAL) hello를 제공 합니다. hello ADAL의 목적으로 toomake 사용자가 앱 tooget 액세스 토큰을 쉽게 합니다. toodemonstrate 하는 Android 할 일 목록 응용 프로그램을 작성할 것이 얼마나 쉬운지:

* 가져옵니다 hello를 사용 하 여 할 일 목록 API 호출에 대 한 토큰에 액세스 [OAuth 2.0 인증 프로토콜](https://msdn.microsoft.com/library/azure/dn645545.aspx)합니다.
* 사용자의 할 일 목록을 가져옵니다.
* 사용자를 로그아웃합니다.

시작 tooget, Azure AD 테 넌 트가 있습니다 수 있는 사용자를 만들와 응용 프로그램을 등록 해야 합니다. 테 넌 트 아직 없는 경우 [자세한 방법을 하나 tooget](active-directory-howto-tenant.md)합니다.

## <a name="step-1-download-and-run-hello-nodejs-rest-api-todo-sample-server"></a>1 단계: 다운로드 하 여 hello Node.js REST API TODO 샘플 서버를 실행 합니다.
hello Node.js REST API TODO 샘플에는 Azure AD에 대 한 단일-테 넌 트 할 일 REST API를 구축 하기 위한 기존 샘플에 대해 toowork 구체적으로 기록 됩니다. 빠른 시작 hello에 대 한 필수 구성 요소입니다.

어떻게 tooset,이 기존 샘플 보기에 대 한 자세한 내용은 [Microsoft Azure Active Directory 샘플 REST API 서비스 Node.js 용](active-directory-devquickstarts-webapi-nodejs.md)합니다.


## <a name="step-2-register-your-web-api-with-your-azure-ad-tenant"></a>2단계: Azure AD 테넌트에 Web API 등록
Active Directory는 두 가지 유형의 응용 프로그램 추가를 지원합니다.

- 웹 서비스 toousers 제공 하는 Api
- 웹 Api 하는 것에 액세스 하는 응용 프로그램 (hello 웹 또는 장치에서 실행)

이 단계에서는이 샘플 테스트를 위해 로컬로 실행 하는 hello 웹 API를 등록 하는 합니다. 일반적으로이 웹 API는 앱 tooaccess 원하는 기능을 제공 하는 REST 서비스입니다. Azure AD는 끝점을 보호하는 데 도움이 될 수 있습니다.

Hello 앞서 참조 된 할 일 REST API를 등록 하는으로 가정 합니다. 하지만이 Azure Active Directory toohelp 보호 하려는 모든 웹 API에 대 한 작동 합니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. Hello 위쪽 막대에서 계정을 클릭 합니다. Hello에 **디렉터리** 목록 tooregister 원하는 hello Azure AD 테 넌 트 응용 프로그램을 선택 합니다.
3. 클릭 **더 서비스** 에 hello 왼쪽된 창에서 선택한 후 **Azure Active Directory**합니다.
4. **앱 등록**을 클릭하고 **추가**를 선택합니다.
5. Hello 응용 프로그램에 대 한 식별 이름을 입력 하세요 (예를 들어 **TodoListService**)을 선택 **웹 응용 프로그램 및/또는 Web API**를 클릭 하 고 **다음**합니다.
6. Hello 로그온 URL에 대 한 hello 샘플에 대 한 hello 기준 URL을 입력 합니다. 기본적으로 `https://localhost:8080`입니다.
7. 클릭 **확인** toocomplete hello 등록 합니다.
8. Hello Azure 포털에서에서 tooyour 응용 프로그램 페이지를 이동 하 고 hello 응용 프로그램 ID 값을 찾아 복사 합니다. 나중에 이 응용 프로그램을 구성하는 경우에 필요합니다.
9. Hello에서 **설정** -> **속성** 페이지, hello 앱 ID URI 업데이트-입력 `https://<your_tenant_name>/TodoListService`합니다. 대체 `<your_tenant_name>` Azure AD 테 넌 트의 hello 이름의 합니다.

## <a name="step-3-register-hello-sample-android-native-client-application"></a>3 단계: hello 샘플 Android 네이티브 클라이언트 응용 프로그램 등록
이 샘플에서는 웹 응용 프로그램을 등록해야 합니다. 이렇게 하면 hello 적시에 등록 된 web API 응용 프로그램 toocommunicate를 프로그램 있습니다. Azure AD는 거부 tooeven 등록 하지 않으면 로그인에 대 한 응용 프로그램 tooask 프로그램을 허용 합니다. Hello 모델의 hello 보안의 일부입니다.

앞서 참조 된 hello 샘플 응용 프로그램을 등록 하는으로 가정 합니다. 하지만 이 절차는 개발 중인 모든 앱에 대해 작동합니다.

> [!NOTE]
> 한 테넌트에 응용 프로그램과 Web API를 모두 배치하는 이유가 궁금할 수 있습니다. 짐작할 수에 있는 것처럼 다른 테넌트에서 Azure AD에 등록된 외부 API에 액세스하는 앱을 빌드할 수 있습니다. 이렇게 하면 고객 됩니다 tooconsent toohello hello 응용 프로그램에 API hello 사용 하 라는 메시지가 표시 됩니다. iOS용 Active Directory 인증 라이브러리가 자동으로 동의 과정을 진행합니다. 고급 기능을 살펴볼 때 이것이 hello 작업 필요한 tooaccess hello 제품군에서 다른 서비스 공급자 뿐만 아니라 Azure 및 Office, Microsoft Api의 중요 한 부분이 표시 됩니다. 이제 web API와 hello 대상 응용 프로그램을 등록 하기 때문에 동일한 테 넌 트, 동의 프롬프트 표시 되지 않습니다. 이 경우 일반적으로 hello 자신의 회사 toouse에 대 한 응용 프로그램을 개발 하는 경우 합니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. Hello 위쪽 막대에서 계정을 클릭 합니다. Hello에 **디렉터리** 목록 tooregister 원하는 hello Azure AD 테 넌 트 응용 프로그램을 선택 합니다.
3. 클릭 **더 서비스** 에 hello 왼쪽된 창에서 선택한 후 **Azure Active Directory**합니다.
4. **앱 등록**을 클릭하고 **추가**를 선택합니다.
5. Hello 응용 프로그램에 대 한 식별 이름을 입력 하세요 (예를 들어 **TodoListClient Android**)을 선택 **네이티브 클라이언트 응용 프로그램**를 클릭 하 고 **다음**합니다.
6. Hello에 대 한 리디렉션 URI를 입력 `http://TodoListClient`합니다. **마침**을 클릭합니다.
7. Hello 응용 프로그램 ID 값을 찾을 hello 응용 프로그램 페이지에서 복사 합니다. 나중에 이 응용 프로그램을 구성하는 경우에 필요합니다.
8. Hello에서 **설정** 페이지에서 **필요한 권한** 선택 **추가**합니다.  찾기 및 TodoListService 선택, 추가 hello **액세스 TodoListService** 에 따른 권한 **위임 된 권한**를 클릭 하 고 **수행**합니다.

Maven으로 toobuild, pom.xml hello 최상위 수준에서 사용할 수 있습니다.

1. 선택한 디렉터리에 다음 리포지토리를 복제합니다.

  `$ git clone git@github.com:AzureADSamples/NativeClient-Android.git`  
2. Hello에 hello 단계를 따라 [Maven 환경을 Android 용 필수 구성 요소 tooset](https://github.com/MSOpenTech/azure-activedirectory-library-for-android/wiki/Setting-up-maven-environment-for-Android)합니다.
3. Hello 에뮬레이터 SDK 19로 설정 합니다.
4. Hello 리포지토리를 복제 toohello 루트 폴더를 이동 합니다.
5. 다음 명령을 실행합니다. `mvn clean install`
6. Hello 디렉터리 toohello 빠른 시작 예제를 변경 합니다.`cd samples\hello`
7. 다음 명령을 실행합니다. `mvn android:deploy android:run`

   Hello 응용 프로그램을 시작 하는 것이 나타납니다.
8. 테스트 사용자 자격 증명 tootry를 입력 합니다.

JAR 패키지 hello AAR 패키지 옆에 제출 됩니다.

## <a name="step-4-download-hello-android-adal-and-add-it-tooyour-eclipse-workspace"></a>4 단계: Android ADAL hello를 다운로드 하 고 tooyour Eclipse 작업 공간 추가
만들었고 있습니다 toohave 쉽게 여러 옵션 toouse ADAL Android 프로젝트에서:

* Eclipse 및 링크 tooyour 응용 프로그램으로 hello 소스 코드 tooimport이이 라이브러리를 사용할 수 있습니다.
* Android Studio를 사용 하는 hello AAR 패키지 형식 및 참조 hello 바이너리를 사용할 수 있습니다.

### <a name="option-1-source-zip"></a>옵션 1: 소스 Zip 가져오기
hello 소스 코드의 복사본 toodownload 클릭 **zip 파일 다운로드** hello hello 페이지의 오른쪽에 있습니다. 또는 [GitHub에서 다운로드](https://github.com/AzureAD/azure-activedirectory-library-for-android/archive/v1.0.9.tar.gz)할 수 있습니다.

### <a name="option-2-source-via-git"></a>옵션 2: Git를 통해 소스 가져오기
tooget hello 소스 코드의 hello Git 통해 SDK를 입력 합니다.

    git clone git@github.com:AzureAD/azure-activedirectory-library-for-android.git
    cd ./azure-activedirectory-library-for-android/src

### <a name="option-3-binaries-via-gradle"></a>옵션 3: Gradle을 통해 이진 파일 가져오기
Hello Maven 중앙 리포지토리에서 hello 이진 파일을 가져올 수 있습니다. Android Studio에서 프로젝트에 다음과 같이 hello AAR 패키지를 포함할 수 있습니다.

```gradle
repositories {
    mavenCentral()
    flatDir {
        dirs 'libs'
    }
    maven {
        url "YourLocalMavenRepoPath\\.m2\\repository"
    }
}
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile('com.microsoft.aad:adal:1.1.1') {
        exclude group: 'com.android.support'
    } // Recent version is 1.1.1
}
```

### <a name="option-4-aar-via-maven"></a>옵션 4: Maven을 통해 AAR 가져오기
플러그 인 M2Eclipse hello를 사용 하 여 hello 종속성 pom.xml 파일에 지정할 수 있습니다.

```xml
<dependency>
    <groupId>com.microsoft.aad</groupId>
    <artifactId>adal</artifactId>
    <version>1.1.1</version>
    <type>aar</type>
</dependency>
```


### <a name="option-5-jar-package-inside-hello-libs-folder"></a>옵션 5: JAR 패키지 hello 라이브러리 폴더
Hello Maven 리포지토리에서 hello JAR 파일을 가져와서 하는 hello에 **libs** 프로젝트의 폴더에에서 있습니다. Toocopy hello 필요한 리소스 tooyour 프로젝트도 필요 하면 hello JAR 패키지에 포함 되지 않습니다.

## <a name="step-5-add-references-tooandroid-adal-tooyour-project"></a>5 단계: 참조 tooAndroid ADAL tooyour 프로젝트 추가
1. 참조 tooyour 프로젝트를 추가 하 고 Android 라이브러리로 지정 합니다. 확실히 모르겠으면 어떻게 toodo이 hello에 대 한 자세한 정보를 얻을 수 있습니다 [Android Studio 사이트](http://developer.android.com/tools/projects/projects-eclipse.html)합니다.
2. 프로젝트 설정으로 디버깅을 위해 hello 프로젝트 종속성을 추가 합니다.
3. 프로젝트의 AndroidManifest.xml 파일 tooinclude를 업데이트 합니다.

        <uses-permission android:name="android.permission.INTERNET" />
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
        <application
            android:allowBackup="true"
            android:debuggable="true"
            android:icon="@drawable/ic_launcher"
            android:label="@string/app_name"
            android:theme="@style/AppTheme" >

            <activity
                android:name="com.microsoft.aad.adal.AuthenticationActivity"
                android:label="@string/title_login_hello_app" >
            </activity>
            ....
        <application/>

4. 기본 활동에서 AuthenticationContext의 인스턴스를 만듭니다. 이 호출의 hello 세부 정보는이 항목의 hello 범위 설명 하지만 좋은 시작 hello 확인 하 여 [Android Native Client 샘플](https://github.com/AzureADSamples/NativeClient-Android)합니다. 다음 예제는 hello, SharedPreferences hello 기본 캐시 되며 기관에에서는 hello 형식의 `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`:

    `mContext = new AuthenticationContext(MainActivity.this, authority, true); // mContext is a field in your activity`

5. Hello 사용자 자격 증명을 입력 하 고 인증 코드를 받은 후 AuthenticationActivity이 코드 블록 toohandle hello 끝을 복사 합니다.

        @Override
         protected void onActivityResult(int requestCode, int resultCode, Intent data) {
             super.onActivityResult(requestCode, resultCode, data);
             if (mContext != null) {
                mContext.onActivityResult(requestCode, resultCode, data);
             }
         }

6. 토큰에 대 한 tooask 콜백을 정의:

        private AuthenticationCallback<AuthenticationResult> callback = new AuthenticationCallback<AuthenticationResult>() {

            @Override
            public void onError(Exception exc) {
                if (exc instanceof AuthenticationException) {
                    textViewStatus.setText("Cancelled");
                    Log.d(TAG, "Cancelled");
                } else {
                    textViewStatus.setText("Authentication error:" + exc.getMessage());
                    Log.d(TAG, "Authentication error:" + exc.getMessage());
                }
            }

            @Override
            public void onSuccess(AuthenticationResult result) {
                mResult = result;

                if (result == null || result.getAccessToken() == null
                        || result.getAccessToken().isEmpty()) {
                    textViewStatus.setText("Token is empty");
                    Log.d(TAG, "Token is empty");
                } else {
                    // request is successful
                    Log.d(TAG, "Status:" + result.getStatus() + " Expired:"
                            + result.getExpiresOn().toString());
                    textViewStatus.setText(PASSED);
                }
            }
        };

7. 마지막으로 해당 콜백을 사용하여 토큰을 요청합니다.

    `mContext.acquireToken(MainActivity.this, resource, clientId, redirect, user_loginhint, PromptBehavior.Auto, "",
                   callback);`

Hello 매개 변수 설명은 다음과 같습니다.

* *리소스* 는 필수 이며 tooaccess를 시도 하는 hello 리소스입니다.
* *clientid*는 필수 항목이며 Azure AD에서 제공됩니다.
* *RedirectUri* 필요한 toobe hello acquireToken 호출에 대 한 제공 되었습니다. 패키지 이름으로 설정될 수 있습니다.
* *PromptBehavior* tooask 자격 증명 tooskip hello 캐시 및 쿠키는 데 도움이 됩니다.
* *콜백* hello 권한 부여 코드는 토큰에 대해 교환 된 후에 호출 됩니다. 여기에는 액세스 토큰, 만료 날짜 및 ID 토큰 정보를 포함하는 AuthenticationResult의 개체가 생성됩니다.
* *acquireTokenSilent*는 선택 사항입니다. Toohandle 캐싱 및 새로 고침 토큰을 호출할 수 있습니다. 또한 hello 동기화 버전을 제공합니다. *userId*가 매개 변수로 수락됩니다.

        mContext.acquireTokenSilent(resource, clientid, userId, callback );

이 연습을 사용 하 여 어떤 필요한 toosuccessfully 통합 하면 Azure Active Directory에 있어야 합니다. 이 작업의 추가 예제에 대 한 방문 hello AzureADSamples / GitHub의 리포지토리 합니다.

## <a name="important-information"></a>중요 정보
### <a name="customization"></a>사용자 지정
응용 프로그램 리소스에서 라이브러리 프로젝트 리소스를 덮어쓸 수 있습니다. 앱을 빌드할 때 이러한 동작이 발생합니다. 이러한 이유로 인증 활동 레이아웃 hello 원하는 방식으로 사용자 지정할 수 있습니다. (WebView)를 사용 하 여 해당 ADAL hello 컨트롤의 ID가 있는지 tookeep hello 됩니다.

### <a name="broker"></a>Broker
Microsoft Intune 회사 포털 앱 hello hello broker 구성 요소를 제공합니다. AccountManager에 hello 계정이 생성 됩니다. hello 계정 형식이 "com.microsoft.workaccount." AccountManager에서는 단일 SSO 계정만 허용됩니다. Hello 앱 중 하나에 대 한 hello 장치 챌린지를 완료 한 후 hello 사용자에 대 한 SSO 쿠키를 만듭니다.

ADAL이이 인증자에 단일 사용자 계정을 만들어지고 tooskip 하지 않으려는 경우 hello 브로커 계정을 사용 하 여 것입니다. 사용 하는 hello 브로커 사용자를 건너뛸 수 있습니다.

   `AuthenticationSettings.Instance.setSkipBroker(true);`

Broker 사용에 대 한 특별 한 RedirectUri tooregister를 해야합니다. RedirectUri hello 형식으로 되어 `msauth://packagename/Base64UrlencodedSignature`합니다. Hello 스크립트 brokerRedirectPrint.ps1 또는 hello API 호출 mContext.getBrokerRedirectUri 사용 하 여 앱에 대 한 프로그램 RedirectUri를 얻을 수 있습니다. hello 서명 인증서를 서명 하는 관련된 tooyour입니다.

hello 현재 브로커 모델 한 명의 사용자입니다. AuthenticationContext은 hello API 메서드 tooget hello 브로커 사용자를 제공합니다.

   `String brokerAccount =  mContext.getBrokerUser(); //Broker user is returned if account is valid.`

응용 프로그램 매니페스트에서 사용 권한, toouse AccountManager 계정 다음 hello가 있어야 합니다. 자세한 내용은 참조 hello [hello Android 사이트 AccountManager 정보](http://developer.android.com/reference/android/accounts/AccountManager.html)합니다.

* GET_ACCOUNTS
* USE_CREDENTIALS
* MANAGE_ACCOUNTS

### <a name="authority-url-and-ad-fs"></a>기관 URL 및 AD FS
Active Directory Federation Services (AD FS)의 인스턴스 검색 tooturn 필요 하 고 false hello AuthenticationContext 생성자에 전달 되므로 STS 프로덕션으로 인식 되지 않습니다.

hello 기관 URL STS 인스턴스가 필요 하며 [테 넌 트 이름](https://login.microsoftonline.com/yourtenant.onmicrosoft.com)합니다.

### <a name="querying-cache-items"></a>캐시 항목 쿼리
ADAL은 일부 간단한 캐시 쿼리 함수를 사용하여 SharedPreferences에서 기본 캐시를 제공합니다. 사용 하 여 AuthenticationContext에서 hello 현재 캐시를 얻을 수 있습니다.

    ITokenCacheStore cache = mContext.getCache();

Toocustomize 하려는 경우에 캐시 구현에 제공할 수 있습니다 것입니다.

    mContext = new AuthenticationContext(MainActivity.this, authority, true, yourCache);

### <a name="prompt-behavior"></a>프롬프트 동작
ADAL 옵션 toospecify 프롬프트 동작을 제공합니다. PromptBehavior.Auto는 hello 새로 고침 토큰이 유효 하지 않은 한 사용자 자격 증명이 필요한 경우 hello UI를 표시 합니다. PromptBehavior.Always를 건너뛰어 hello 캐시 사용량 항상 hello UI를 표시 합니다.

### <a name="silent-token-request-from-cache-and-refresh"></a>캐시 및 새로 고침의 자동 토큰 요청
자동 토큰 요청 hello UI 팝업을 사용 하지 않는 및 활동 필요 하지 않습니다. 사용 가능한 경우 hello 캐시에서 토큰을 반환 합니다. Hello 토큰이 만료 된 경우이 메서드 toorefresh를 시도 하는 것입니다. Hello 새로 고침 토큰은 만료 또는 실패 한 경우 AuthenticationException 반환 합니다.

    Future<AuthenticationResult> result = mContext.acquireTokenSilent(resource, clientid, userId, callback );

이 메서드를 사용하여 동기화를 호출할 수도 있습니다. Null toocallback 설정 하거나 acquireTokenSilentSync를 사용할 수 있습니다.

### <a name="diagnostics"></a>진단
다음은 문제를 진단 하는 것에 대 한 정보의 hello 기본 소스입니다.

* 예외
* 로그
* 네트워크 추적

상관 관계 Id는 hello 라이브러리에서 중앙 toohello 진단 note 합니다. Toocorrelate는 ADAL 요청 코드에서 다른 작업을 사용 하려는 경우에 요청 별로 상관 관계 Id를 설정할 수 있습니다. 상관 관계 ID를 설정하지 않으면, ADAL에서 임의의 항목을 생성합니다. 모든 메시지를 로그 하 고 hello 상관 관계 id입니다. 그런 다음 네트워크 호출을 지정 합니다. hello 자체 ID도 변경 요청이 있을 때마다 생성 됩니다.

#### <a name="exceptions"></a>예외
예외 진단 먼저 hello 됩니다. Tooprovide 유용한 오류 메시지 시도 합니다. 유용하지 않은 오류 메시지가 표시되면 문제를 정리한 후 알려주세요. 모델 및 SDK 번호와 같은 장치 정보도 포함합니다.

#### <a name="logs"></a>로그
Hello 라이브러리 toogenerate를 구성할 수 있습니다 toohelp를 사용할 수 있는 로그 메시지 문제를 진단 합니다. Hello 다음 tooconfigure 생성 되는 ADAL toohand 각 로그 메시지에서 사용 되도록 하는 콜백을 호출 하 여 로깅을 구성 합니다.

    Logger.getInstance().setExternalLogger(new ILogger() {
        @Override
        public void Log(String tag, String message, String additionalMessage, LogLevel level, ADALError errorCode) {
        ...
        // You can write this toolog file depending on level or error code.
        writeToLogFile(getApplicationContext(), tag +":" + message + "-" + additionalMessage);
        }
    }

메시지는 hello 코드 다음에 표시 된 대로 tooa 사용자 지정 로그 파일을 작성할 수 있습니다. 그러나 장치에서 로그를 얻는 표준 방법은 없습니다. 이 작업에 도움이 되는 몇 가지 서비스가 있습니다. 와 같은 직접 보내는 hello 파일 tooa 서버를 만들 수 있습니다.

    private syncronized void writeToLogFile(Context ctx, String msg) {
       File directory = ctx.getDir(ctx.getPackageName(), Context.MODE_PRIVATE);
       File logFile = new File(directory, "logfile");
       FileOutputStream outputStream = new FileOutputStream(logFile, true);
       OutputStreamWriter osw = new OutputStreamWriter(outputStream);
       osw.write(msg);
       osw.flush();
       osw.close();
    }

다음은 hello 로깅 수준입니다.
* 오류(예외)
* 경고
* 정보(정보 제공용)
* 자세한 정보 표시(자세한 내용)

다음과 같이 hello 로그 수준 설정:

    Logger.getInstance().setLogLevel(Logger.LogLevel.Verbose);

 모든 로그 메시지가 추가 tooany 사용자 지정 로그 콜백을 toologcat, 보내집니다.
다음과 같이 로그 tooa 파일 logcat에서 얻을 수 있습니다.

    adb logcat > "C:\logmsg\logfile.txt"

 Adb 명령에 대 한 자세한 참조 hello [hello Android 사이트 logcat 정보](https://developer.android.com/tools/debugging/debugging-log.html#startingLogcat)합니다.

#### <a name="network-traces"></a>네트워크 추적
ADAL을 생성 하는 다양 한 도구 toocapture hello HTTP 트래픽을 사용할 수 있습니다.  Hello OAuth 프로토콜에 익숙한 경우 또는 tooprovide 진단 정보 tooMicrosoft 또는 기타 지원 채널을 필요한 경우 가장 유용 합니다.

Fiddler는 hello 쉬운 HTTP 추적 도구입니다. 사용 하 여 hello 다음 링크 tooset toocorrectly 레코드 ADAL 네트워크 트래픽 설정 합니다. Fiddler 또는 Charles toobe 유용한와 같은 추적 도구를 구성 해야 암호화 되지 않은 toorecord SSL 트래픽을 합니다.  

> [!NOTE]
> 이 방식으로 생성된 추적에는 액세스 토큰, 사용자 이름 및 암호와 같은 높은 권한이 필요한 정보가 포함될 수 있습니다. 프로덕션 계정을 사용하는 경우 이러한 추적 정보를 제3자와 공유하지 않도록 하세요. Toosupply 순서 tooget 지원의 추적 toosomeone 필요한 경우 공유 유의 하지 않는 사용자 이름 및 암호와 임시 계정을 사용 하 여 hello 문제를 재현 합니다.

* Hello Telerik 웹 사이트에서: [설정을를 Fiddler에 대 한 Android](http://docs.telerik.com/fiddler/configure-fiddler/tasks/ConfigureForAndroid)
* GitHub: [ADAL에 대한 Fiddler 규칙 구성(영문)](https://github.com/AzureAD/azure-activedirectory-library-for-android/wiki/How-to-listen-to-httpUrlConnection-in-Android-app-from-Fiddler)

### <a name="dialog-mode"></a>대화 상자 모드
활동이 없는 hello acquireToken 메서드 확인 대화를 지원합니다.

### <a name="encryption"></a>암호화
ADAL은 hello 토큰 및 SharedPreferences에서 기본적으로 저장소를 암호화합니다. Hello StorageHelper 클래스 toosee hello 세부 정보를 살펴볼 수 있습니다. Android에서는 개인 키의 보안 저장소인 4.3(API 18)용 Android Keystore를 도입했습니다. ADAL은 API 18 이상에 이 저장소를 사용합니다. 더 낮은 SDK 버전에 대 한 ADAL toouse를 원하는 경우 tooprovide AuthenticationSettings.INSTANCE.setSecretKey에 비밀 키를 해야 합니다.

### <a name="oauth2-bearer-challenge"></a>OAuth2 전달자 챌린지
hello AuthenticationParameters 클래스 기능 tooget authorization_uri hello OAuth2 전달자 챌린지를에서 제공합니다.

### <a name="session-cookies-in-webview"></a>WebView의 세션 쿠키
Android WebView hello 응용 프로그램을 닫은 후 세션 쿠키를 삭제 하지 않습니다. 다음 샘플 코드를 사용하여 이 문제를 처리할 수 있습니다.

    CookieSyncManager.createInstance(getApplicationContext());
    CookieManager cookieManager = CookieManager.getInstance();
    cookieManager.removeSessionCookie();
    CookieSyncManager.getInstance().sync();

쿠키에 대 한 자세한 참조 hello [hello Android 사이트 CookieSyncManager 정보](http://developer.android.com/reference/android/webkit/CookieSyncManager.html)합니다.

### <a name="resource-overrides"></a>리소스 재정의
hello ADAL 라이브러리 ProgressDialog 메시지에 대 한 영어 문자열이 포함 되어 있습니다. 지역화된 문자열을 사용하려는 경우 응용 프로그램이 덮어씁니다.

     <string name="app_loading">Loading...</string>
     <string name="broker_processing">Broker is processing</string>
     <string name="http_auth_dialog_username">Username</string>
     <string name="http_auth_dialog_password">Password</string>
     <string name="http_auth_dialog_title">Sign In</string>
     <string name="http_auth_dialog_login">Login</string>
     <string name="http_auth_dialog_cancel">Cancel</string>

### <a name="ntlm-dialog-box"></a>NTLM 대화 상자
ADAL 버전 1.1.0 WebViewClient에서 hello onReceivedHttpAuthRequest 이벤트를 통해 처리 되는 NTLM 대화 상자를 지원 합니다. Hello 레이아웃과 hello 대화 상자에 대 한 문자열을 사용자 지정할 수 있습니다.

### <a name="cross-app-sso"></a>앱 간 SSO
자세한 내용은 [어떻게 tooenable ADAL을 사용 하 여 android 응용 프로그램 간 SSO](active-directory-sso-android.md)합니다.  

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

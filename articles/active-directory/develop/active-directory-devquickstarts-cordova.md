---
title: "aaaAzure AD Cordova 시작 | Microsoft Docs"
description: "Toobuild Cordova 응용 프로그램 하는 로그인에 대 한 Azure AD와 통합 되어 방법과 OAuth를 사용 하 여 Azure AD로 보호 된 Api를 호출 합니다."
services: active-directory
documentationcenter: 
author: vibronet
manager: mbaldwin
editor: 
ms.assetid: b1a8d7bd-7ad6-44d5-8ccb-5255bb623345
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: vittorib
ms.custom: aaddev
ms.openlocfilehash: 573ed638c2180c5231648bcb8c49ceb6f53296f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-an-apache-cordova-app"></a>Azure AD를 Apache Cordova 앱에 통합
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

완전 한 네이티브 응용 프로그램으로 모바일 장치에서 실행할 수 있는 Apache Cordova toodevelop HTML5/JavaScript 응용 프로그램을 사용할 수 있습니다. Azure Active Directory (Azure AD)와 기업 간 인증 기능 tooyour Cordova 응용 프로그램을 추가할 수 있습니다.

Cordova 플러그 인은 iOS, Android, Windows 스토어 및 Windows Phone에서 Azure AD 네이티브 SDK를 래핑합니다. 플러그 인을 향상 시킬 수 있습니다 응용 프로그램을 사용 하 여 사용자의 Windows Server Active Directory 계정, 이득 액세스 tooOffice 365 및 Azure Api를 사용 하 여 로그인 하 고 심지어 toosupport 호출 tooyour 고유의 사용자 지정 웹 API를 보호할 수 있습니다.

이 자습서에서는 Apache Cordova 플러그 인 hello Active Directory 인증 라이브러리 (ADAL) tooimprove 간단한 응용 프로그램에 대 한 hello 같은 기능을 추가 하 여:

* 단 몇 줄의 코드로, 사용자를 인증하고 토큰을 가져옵니다.
* 해당 토큰 tooinvoke hello Graph API tooquery 해당 디렉터리를 사용 하 고 hello 결과 표시 합니다.  
* Hello ADAL 토큰 캐시 toominimize 인증 사용 hello 사용자에 게 묻습니다.

toomake를 해야 이러한 향상 된 기능:

1. Azure AD에 응용 프로그램을 등록합니다.
2. 코드 tooyour 앱 toorequest 토큰을 추가 합니다.
3. Hello Graph API를 쿼리 하기 위한 코드 toouse hello 토큰을 추가 하 고 결과 표시 합니다.
4. Hello Cordova 배포 프로젝트 만들기 모든 hello 플랫폼과 tootarget, 추가 hello Cordova ADAL 플러그 인을 에뮬레이터의 hello 솔루션을 테스트 합니다.

## <a name="prerequisites"></a>필수 조건
toocomplete 해야이 자습서에서는:

* 앱 개발 권한이 있는 계정이 있는 Azure AD 테넌트
* 가 toouse Apache Cordova를 구성 하는 개발 환경입니다.  

둘 다 이미 있는 경우 설정, 직접 toostep 1 계속 진행 합니다.

Azure AD 테 넌 트를 설정 하지 않은 경우 사용 하 여 hello [방법은 하나 tooget](active-directory-howto-tenant.md)합니다.

사용자 컴퓨터에 설치 하는 Apache Cordova를 설정 하지 않은 경우에 hello 다음을 설치 합니다.

* [Git](http://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
* [Node.JS](https://nodejs.org/download/)
* [Cordova CLI](https://cordova.apache.org/)(`npm install -g cordova` NPM 패키지 관리자를 통해 쉽게 설치 가능)

앞에 설치 하는 hello Mac. hello 및 hello PC에서 모두 작동 해야

대상 플랫폼마다 필수 구성 요소가 다릅니다.

* toobuild 및 Windows 태블릿/PC 또는 Windows Phone 앱 실행:
  * [Windows용 Visual Studio 2013 업데이트 2 이상](http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-windows-8)(Express 또는 다른 버전) 또는 [Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-community)를 설치합니다.

* toobuild 및 iOS 용 앱 실행:

  * Xcode 6.x 이상을 설치합니다. Hello에서 다운로드 [Apple 개발자 사이트](http://developer.apple.com/downloads) 또는 hello [Mac 앱 스토어](http://itunes.apple.com/us/app/xcode/id497799835?mt=12)합니다.
  * [ios-sim](https://www.npmjs.org/package/ios-sim)을 설치합니다. 사용할 수 있습니다 toostart iOS 앱 hello 명령줄에서 ios 시뮬레이터. (Hello 터미널을 통해 쉽게 설치할 수 있습니다: `npm install -g ios-sim`.)
* toobuild 및 Android 용 앱 실행:

  * [JDK(Java Development Kit) 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) 이상을 설치합니다. 확인 `JAVA_HOME` toohello JDK 설치 경로 (예를 들어 C:\Program Files\Java\jdk1.7.0_75)에 따라 (환경 변수) 올바르게 설정 합니다.
  * 설치 [Android SDK](http://developer.android.com/sdk/installing/index.html?pkg=tools) hello 추가 `<android-sdk-location>\tools` 위치 (예를 들어 C:\tools\Android\android-sdk\tools) tooyour `PATH` 환경 변수입니다.
  * Android SDK Manager를 엽니다 (예를 들어 hello 터미널을 통해: `android`) 하 고 설치 합니다.
    * *Android 5.0.1(API 21)* 플랫폼 SDK
    * *Android SDK 빌드 도구* 버전 19.1.0 이상
    * *Android 지원 리포지토리* (기타)

  hello Android SDK는 모든 기본 에뮬레이터 인스턴스를 제공 하지 않습니다. 실행 하 여 만드세요 `android avd` 터미널 hello 및 다음을 선택 하 **만들기**toorun 에뮬레이터의 hello Android 앱을 사용 하려는 경우. API 수준 19 이상을 사용하는 것이 좋습니다. Hello Android 에뮬레이터 및 만들기 옵션에 대 한 자세한 내용은 참조 [AVD Manager](http://developer.android.com/tools/help/avd-manager.html) hello Android 사이트에 있습니다.

## <a name="step-1-register-an-application-with-azure-ad"></a>1단계: Azure AD에 응용 프로그램 등록
이 단계는 옵션입니다. 이 자습서 toosee를 사용할 수 있는 미리 프로 비전된 값 자신의 테 넌 트의 모든 프로 비전을 수행 하지 않고도 작업에 대 한 샘플 hello를 제공 합니다. 그러나이 단계를 수행 하 고 될 수 있으므로 필요한 응용 프로그램을 만들 때 hello 프로세스에 잘 수행 하는 것이 좋습니다.

Azure AD 응용 프로그램을 알려진 토큰 tooonly를 발급 합니다. Azure AD에서 앱을 사용 하려면 먼저 toocreate 항목에 대 한 테 넌 트에 합니다. tooregister 테 넌 트에 새 응용 프로그램:

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. Hello 위쪽 막대에서 계정을 클릭 합니다. Hello에 **디렉터리** 목록 tooregister 원하는 hello Azure AD 테 넌 트 응용 프로그램을 선택 합니다.
3. 클릭 **더 서비스** 에 hello 왼쪽된 창에서 선택한 후 **Azure Active Directory**합니다.
4. **앱 등록**을 클릭하고 **추가**를 선택합니다.
5. 만들고 hello 지시에 따라 한 **네이티브 클라이언트 응용 프로그램**합니다. (Cordova 앱이 HTML 기반이기는 하지만 여기서는 네이티브 클라이언트 응용 프로그램을 만듭니다. hello **네이티브 클라이언트 응용 프로그램** 옵션을 선택 해야 합니다 또는 hello 응용 프로그램에서 작동 하지 않습니다.)
  * **이름** 응용 프로그램 toousers에 설명 합니다.
  * **리디렉션 URI** 는 hello tooreturn 토큰 tooyour 응용 프로그램을 사용 하는 URI입니다. **http://MyDirectorySearcherApp**을 입력합니다.

등록을 완료 한 후 Azure AD는 고유한 응용 프로그램 ID tooyour 응용 프로그램에 할당 합니다. Hello 다음 섹션의이 값이 필요 합니다. 응용 프로그램을 새로 만든 hello hello 응용 프로그램 탭에서 찾을 수 있습니다.

toorun `DirSearchClient Sample`, hello 새로 만든 응용 프로그램 권한 tooquery hello Azure AD Graph API 권한을 부여 합니다.

1. Hello에서 **설정** 페이지에서 **필요한 권한**를 선택한 후 **추가**합니다.  
2. Hello Azure Active Directory 응용 프로그램에 대 한 선택 **Microsoft Graph** 으로 hello를 더하고 API hello **hello 로그인 한 사용자로 디렉터리에 액세스 hello** 에 따른 권한 **위임 된 사용 권한**합니다.  이 통해 사용자에 대 한 프로그램 응용 프로그램 tooquery hello Graph API.

## <a name="step-2-clone-hello-sample-app-repository"></a>2 단계: hello 샘플 앱 리포지토리 복제
셸 또는 명령줄에서 다음 명령을 hello를 입력 합니다.

    git clone -b skeleton https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova.git

## <a name="step-3-create-hello-cordova-app"></a>3 단계: hello Cordova 앱 만들기
여러 가지 방법 toocreate Cordova 응용 프로그램이 있습니다. 이 자습서에서는 hello Cordova CLI (명령줄 인터페이스)를 사용 합니다.

1. 셸 또는 명령줄에서 다음 명령을 hello를 입력 합니다.

        cordova create DirSearchClient

   해당 명령은 hello 폴더 구조 및 hello Cordova 프로젝트에 대 한 스 캐 폴딩을 만듭니다.

2. Toohello 새 DirSearchClient 폴더를 이동 합니다.

        cd .\DirSearchClient

3. 파일 관리자 또는 hello 다음 셸에서에서 명령을 사용 하 여 hello www 하위 폴더에 hello 시작 프로젝트의 hello 콘텐츠를 복사 합니다.

  * Windows: `xcopy ..\NativeClient-MultiTarget-Cordova\DirSearchClient www /E /Y`
  * Mac: `cp -r  ../NativeClient-MultiTarget-Cordova/DirSearchClient/* www`

4. Hello 허용 목록 플러그 인을 추가 합니다. 이 hello Graph API를 호출 하는 데 필요 합니다.

        cordova plugin add cordova-plugin-whitelist

5. Toosupport 원하는 모든 hello 플랫폼을 추가 합니다. 작업 예제 toohave hello 명령 뒤의 tooexecute 하나 이상 필요 합니다. 참고 수 windows 수 tooemulate iOS 또는 mac에서 Windows를 에뮬레이트하 없습니다

        cordova platform add android
        cordova platform add ios
        cordova platform add windows

6. Cordova 플러그 인 tooyour 프로젝트에 대 한 ADAL hello를 추가 합니다.

        cordova plugin add cordova-plugin-ms-adal

## <a name="step-4-add-code-tooauthenticate-users-and-obtain-tokens-from-azure-ad"></a>4 단계: 코드 tooauthenticate 사용자를 추가 하 고 Azure AD에서 토큰을 얻어
이 자습서에서 개발 중인 응용 프로그램으로 hello 간단한 디렉터리 검색 기능을 제공 합니다. hello 사용자 수 하 한 다음, hello 디렉터리에 있는 모든 사용자의 hello 별칭을 입력 하 고, 몇 가지 기본 특성을 시각화 합니다. (에 www/index.html) hello 응용 프로그램의 hello 기본 사용자 인터페이스의 hello 정의 포함 하는 hello 시작 프로젝트 및 기본 응용 프로그램 이벤트를 연결 하는 hello 스 캐 폴딩 주기, 사용자 인터페이스 바인딩 (www/js/index.js)에서 디스플레이 논리 조정은 합니다. hello 유일한 작업 엔은 identity 작업을 구현 하는 tooadd hello 논리입니다.

hello 먼저 toodo 코드에서 필요한 것은 Azure AD 앱을 식별 하는 데 사용 하는 hello 프로토콜 값을 소개 하며 hello 리소스 대상 이러한 값에는 나중에 사용 되는 tooconstruct hello 토큰 요청 게 됩니다. Hello 다음 hello 위쪽 hello index.js 파일의 코드 조각 삽입:

```javascript
var authority = "https://login.microsoftonline.com/common",
    redirectUri = "http://MyDirectorySearcherApp",
    resourceUri = "https://graph.windows.net",
    clientId = "a5d92493-ae5a-4a9f-bcbf-9f1d354067d3",
    graphApiVersion = "2013-11-08";
```

hello `redirectUri` 및 `clientId` 값에는 Azure AD에서 앱을 설명 하는 hello 값과 일치 해야 합니다. Hello에서 찾을 수 있습니다 **구성** 이 자습서의 앞부분에 나오는 1 단계에 설명 된 대로 hello Azure 포털을 탭 합니다.

> [!NOTE]
> 하지 자신의 테 넌 트에 새 앱을 등록 하기 위한를 선택한 경우 hello 미리 구성 된 값은 단순히 붙여넣을 수 있습니다. 그런 다음 프로덕션 환경에는 앱에 대 한 항목을 직접를 항상 만들어야 하지만 hello 샘플 실행을 볼 수 있습니다.

다음으로 hello 토큰 요청 코드를 추가 합니다. 코드 조각 hello 사이 다음 hello 삽입 `search` 및 `renderData` 정의:

```javascript
    // Shows hello user authentication dialog box if required
    authenticate: function (authCompletedCallback) {

        app.context = new Microsoft.ADAL.AuthenticationContext(authority);
        app.context.tokenCache.readItems().then(function (items) {
            if (items.length > 0) {
                authority = items[0].authority;
                app.context = new Microsoft.ADAL.AuthenticationContext(authority);
            }
            // Attempt tooauthorize hello user silently
            app.context.acquireTokenSilentAsync(resourceUri, clientId)
            .then(authCompletedCallback, function () {
                // We require user credentials, so this triggers hello authentication dialog box
                app.context.acquireTokenAsync(resourceUri, clientId, redirectUri)
                .then(authCompletedCallback, function (err) {
                    app.error("Failed tooauthenticate: " + err);
                });
            });
        });

    },
```
두 주요 부분에서 분석하여 해당 함수를 검토해 보겠습니다.
이 샘플 디자인 된 toowork 모든 테 넌 트와는 달리 toobeing 연결 tooa 특정 하나입니다. Hello를 사용 하 여 인증 시에 계정이 hello 사용자 tooenter 수 있도록 하 고 속하는 hello 요청 toohello 테 넌 트를 안내 하는 "/ 일반적인" 끝점입니다.

이 첫 번째 부분에서는 hello 메서드 토큰이 이미 저장 되어 있는 경우 hello ADAL 캐시 toosee를 검사 합니다. 이 경우 hello 메서드가 hello 테 넌 트 hello 토큰에서 ADAL을 다시 초기화 하기 위한 있었던 합니다. 이 이므로 필요한 tooavoid 추가 프롬프트 hello 사용 "/ 일반적인"의 hello 사용자 tooenter 새 계정을 묻는에 항상 발생 합니다.

```javascript
        app.context = new Microsoft.ADAL.AuthenticationContext(authority);
        app.context.tokenCache.readItems().then(function (items) {
            if (items.length > 0) {
                authority = items[0].authority;
                app.context = new Microsoft.ADAL.AuthenticationContext(authority);
            }
```
hello 메서드의 두 번째 부분은 hello hello 적절 한 토큰 요청을 수행합니다. hello `acquireTokenSilentAsync` 메서드 요청 ADAL tooreturn 토큰을 지정 하는 hello에 대 한 모든 사용자 환경 표시 하지 않고 리소스 Hello 캐시에 저장 하 고, 적합 한 액세스 토큰을 이미 있는 경우에 발생할 수 있습니다 새로 고침 토큰 수 있는지 또는 모든 프롬프트를 표시 하지 않고 tooget 새 액세스 토큰을 사용 합니다. 이 시도가 실패 하면, 우리에서 대체 `acquireTokenAsync`-hello 사용자 tooauthenticate 물어봅니다 시각적으로 표시 합니다.

```javascript
            // Attempt tooauthorize hello user silently
            app.context.acquireTokenSilentAsync(resourceUri, clientId)
            .then(authCompletedCallback, function () {
                // We require user credentials, so this triggers hello authentication dialog box
                app.context.acquireTokenAsync(resourceUri, clientId, redirectUri)
                .then(authCompletedCallback, function (err) {
                    app.error("Failed tooauthenticate: " + err);
                });
            });
```
이제 hello 토큰 했으므로 म 수 마지막 hello Graph API 호출과 원하는 hello 검색 쿼리를 수행 합니다. Hello 다음 hello 아래 코드 조각 삽입 `authenticate` 정의:

```javascript
// Makes an API call tooreceive hello user list
    requestData: function (authResult, searchText) {
        var req = new XMLHttpRequest();
        var url = resourceUri + "/" + authResult.tenantId + "/users?api-version=" + graphApiVersion;
        url = searchText ? url + "&$filter=mailNickname eq '" + searchText + "'" : url + "&$top=10";

        req.open("GET", url, true);
        req.setRequestHeader('Authorization', 'Bearer ' + authResult.accessToken);

        req.onload = function(e) {
            if (e.target.status >= 200 && e.target.status < 300) {
                app.renderData(JSON.parse(e.target.response));
                return;
            }
            app.error('Data request failed: ' + e.target.response);
        };
        req.onerror = function(e) {
            app.error('Data request failed: ' + e.error);
        }

        req.send();
    },

```
텍스트 상자에 사용자의 별칭을 입력 하기 위한 간단한 UX를 제공 하는 hello 시작점 파일. 이 메서드를 사용 하 고 그 값 tooconstruct 쿼리, hello 액세스 토큰으로 결합, tooMicrosoft 그래프를 보낼 hello 결과 구문 분석 합니다. hello `renderData` hello 결과 시각화 하는 hello 시작점 파일에 이미 있는 메서드를 담당 합니다.

## <a name="step-5-run-hello-app"></a>5 단계: hello 앱 실행
응용 프로그램에 마지막으로 준비 toorun입니다. 작동 하는 것은 간단: hello 앱이 시작 되 면, toolook 원하는 hello 사용자의 hello 별칭을 입력 하 고 hello 단추를 클릭 합니다. 인증을 위한 메시지가 표시됩니다. 성공적으로 인증 및 검색 시 검색 hello 사용자의 hello 특성이 표시 됩니다.

후속 실행 모든 프롬프트를 표시 하지 않고 hello 검색을 수행 합니다 이면 고마워요 hello toohello 있으면 이전에 캐시에서 토큰.

hello 앱을 실행 하기 위한 구체적인 단계 hello 플랫폼에 따라 다릅니다.

### <a name="windows-10"></a>Windows 10
   태블릿/PC: `cordova run windows --archs=x64 -- --appx=uap`

   모바일 (Windows 10 Mobile 장치 연결 tooa PC 필요):`cordova run windows --archs=arm -- --appx=uap --phone`

   > [!NOTE]
   > 먼저 실행 하 여 hello, 하는 동안 메시지가 나타날 수 있습니다에 toosign 개발자 라이선스에 대 한 합니다. 자세한 내용은 [개발자 라이선스](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx)를 참조하세요.

### <a name="windows-81-tabletpc"></a>Windows 8.1 태블릿/PC
   `cordova run windows`

   > [!NOTE]
   > 먼저 실행 하 여 hello, 하는 동안 메시지가 나타날 수 있습니다에 toosign 개발자 라이선스에 대 한 합니다. 자세한 내용은 [개발자 라이선스](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx)를 참조하세요.

### <a name="windows-phone-81"></a>Windows Phone 8.1
   연결된 된 장치에서 toorun:`cordova run windows --device -- --phone`

   hello 기본 에뮬레이터에 toorun:`cordova emulate windows -- --phone`

   사용 하 여 `cordova run windows --list -- --phone` toosee 모든 사용 가능한 대상 및 `cordova run windows --target=<target_name> -- --phone` 특정 장치 또는 에뮬레이터에서 toorun hello 응용 프로그램 (예를 들어 `cordova run windows --target="Emulator 8.1 720P 4.7 inch" -- --phone`).

### <a name="android"></a>Android
   연결된 된 장치에서 toorun:`cordova run android --device`

   hello 기본 에뮬레이터에 toorun:`cordova emulate android`

   만든 에뮬레이터 인스턴스가 AVD Manager를 사용 하 여 hello "전제 조건" 섹션에서에서 설명한 대로 있는지 확인 합니다.

   사용 하 여 `cordova run android --list` toosee 모든 사용 가능한 대상 및 `cordova run android --target=<target_name>` 특정 장치 또는 에뮬레이터에서 toorun hello 응용 프로그램 (예를 들어 `cordova run android --target="Nexus4_emulator"`).

### <a name="ios"></a>iOS
   연결된 된 장치에서 toorun:`cordova run ios --device`

   hello 기본 에뮬레이터에 toorun:`cordova emulate ios`

   > [!NOTE]
   > Hello 했는지 확인 `ios-sim` hello 에뮬레이터에서 toorun 패키지가 설치 됩니다. 자세한 내용은 hello "전제 조건"을 참조 하세요. 섹션.

    Use `cordova run ios --list` toosee all available targets and `cordova run ios --target=<target_name>` toorun hello application on specific device or emulator (for example, `cordova run android --target="iPhone-6"`).

    Use `cordova run --help` toosee additional build and run options.

## <a name="next-steps"></a>다음 단계
구성 값) (없이 hello 완료 샘플은에서 사용할 수 있는 참조를 위해 [GitHub](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova/tree/complete/DirSearchClient)합니다.

이제 고급 toomore (및 기타 흥미로운)에 이동 시나리오 할 수 있습니다. Tootry 할 수 있습니다: [Azure AD 사용 하 여 Node.js 웹 API 보안](active-directory-devquickstarts-webapi-nodejs.md)합니다.

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

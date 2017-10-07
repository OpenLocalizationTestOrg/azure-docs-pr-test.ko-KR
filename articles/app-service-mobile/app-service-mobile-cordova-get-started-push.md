---
title: "Azure 모바일 앱으로 Cordova 앱 aaaAdd 푸시 알림을 tooApache | Microsoft Docs"
description: "Azure 모바일 앱 toosend toouse 밀어넣기 알림 tooyour Apache Cordova 앱에 알아봅니다."
services: app-service\mobile
documentationcenter: javascript
manager: syntaxc4
editor: 
author: ggailey777
ms.assetid: 92c596a9-875c-4840-b0e1-69198817576f
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 8e1b23d6145b446b6f01599337b677e2f2b31d7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-apache-cordova-app"></a>푸시 알림 tooyour Apache Cordova 앱 추가
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>개요
이 자습서에서는 레코드가 삽입 될 때마다 푸시 알림을 toohello 장치가 전송 되도록 푸시 알림을 toohello [Apache Cordova 퀵 스타트] 프로젝트를 추가 합니다.

사용 하지 않는 경우 hello 퀵 스타트 서버 프로젝트를 다운로드, 푸시 알림 확장 패키지 hello 필요 합니다. 자세한 내용은 참조 [Azure 모바일 앱에 대 한 hello.NET 백 엔드 서버 SDK에서 작동][1]합니다.

## <a name="prerequisites"></a>필수 조건
이 자습서에서는 Google Android 에뮬레이터 hello, Android 장치, Windows 장치 및 iOS 장치에서 실행 되는 Visual Studio 2015를 사용 하 여 개발 하는 Apache Cordova 응용 프로그램에 설명 합니다.

toocomplete 해야이 자습서에서는:

* [Visual Studio Community 2015][2] 이상이 설치된 PC
* [Visual Studio Tools for Apache Cordova][4]
* [활성 Azure 계정][3]
* 완료된 [Apache Cordova 빠른 시작][5] 프로젝트
* (Android)검증된 메일 주소를 사용하는 [Google 계정][6]
* (iOS)[Apple 개발자 프로그램 멤버 자격][7] 및 iOS 장치(iOS 시뮬레이터는 푸시를 지원하지 않음)
* (Windows)[Windows 스토어 개발자 계정][8] 및 Windows 10 장치

## <a name="configure-hub"></a>알림 허브 구성
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

[이 섹션의 단계를 보여 주는 비디오 시청][9]

## <a name="update-hello-server-project"></a>Hello 서버 프로젝트를 업데이트 합니다.
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="add-push-to-app"></a>Cordova 앱 수정
Apache Cordova 응용 프로그램 프로젝트 준비 toohandle 푸시 알림을 hello Cordova 푸시 플러그 인 설치와 모든 플랫폼별 푸시 서비스를 확인 하십시오.

#### <a name="update-hello-cordova-version-in-your-project"></a>프로젝트의 hello Cordova 버전을 업데이트 합니다.
프로젝트에서 v6.1.1 이전 버전의 Apache Cordova를 사용 하는 경우 hello 클라이언트 프로젝트를 업데이트 합니다. tooupdate hello 프로젝트:

* 마우스 오른쪽 단추로 클릭 `config.xml` tooopen hello 구성 디자이너입니다.
* Hello 플랫폼 탭을 선택 합니다.
* Hello에 6.1.1 선택 **Cordova CLI** 입력란.
* 선택 **빌드**, 다음 **솔루션 빌드** tooupdate hello 프로젝트.

#### <a name="install-hello-push-plugin"></a>Hello 푸시 플러그 인 설치
Apache Cordova 응용 프로그램에서는 기본적으로 장치 또는 네트워크 기능을 처리하지 않습니다.  이러한 기능은 [npm][10] 또는 GitHub에 게시된 플러그 인에서 제공됩니다.  hello `phonegap-plugin-push` 플러그 인을 사용 하는 toohandle 네트워크 푸시 알림을 합니다.

다음이 방법 중 하나에 hello 푸시 플러그 인을 설치할 수 있습니다.

**명령 프롬프트를 hello:**

Hello 다음 명령을 실행 합니다.

    cordova plugin add phonegap-plugin-push

**Visual Studio 내에서**

1. Hello를 열고 솔루션 탐색기에서 `config.xml` 파일 클릭 **플러그 인** > **사용자 지정**선택, **Git** 설치 원본으로 다음입력`https://github.com/phonegap/phonegap-plugin-push`hello 소스로 합니다.

   ![][img1]

2. Hello 화살표 다음 toohello 설치 원본을 클릭 합니다.
3. **SENDER_ID**, hello Google 개발자 콘솔 프로젝트에 대 한 숫자 프로젝트 ID를 이미 있는 경우 하면 여기에 추가할 수 있습니다. 그렇지 않으면 자리 표시자 값(예: 777777)을 입력합니다.  Android를 대상으로 하는 경우 나중에 config.xml에서 이 값을 업데이트할 수 있습니다.
4. **추가**를 클릭합니다.

hello 푸시 플러그 인이 설치 됩니다.

#### <a name="install-hello-device-plugin"></a>Hello 장치 플러그 인 설치
다음과 같은 hello tooinstall hello 푸시 플러그 인을 사용 하는 프로시저입니다.  Hello 핵심 플러그 인 목록에서 hello 장치 플러그 인을 추가 (클릭 **플러그 인** > **코어** toofind 것). 이 플러그 인 tooobtain hello 플랫폼 이름이 필요 합니다.

#### <a name="register-your-device-on-application-start-up"></a>응용 프로그램 시작 시 장치 등록
처음에 Android에 대한 최소한의 코드를 포함합니다. 나중에 iOS 또는 Windows 10 앱 toorun hello를 수정 합니다.

1. 호출을 너무 추가**registerForPushNotifications** hello hello 맨 아래에 또는 hello 로그인 프로세스에 대 한 hello 콜백 하는 동안 **onDeviceReady** 메서드:

        // Login toohello service.
        client.login('google')
            .then(function () {
                // Create a table reference
                todoItemTable = client.getTable('todoitem');

                // Refresh hello todoItems
                refreshDisplay();

                // Wire up hello UI Event Handler for hello Add Item
                $('#add-item').submit(addItemHandler);
                $('#refresh').on('click', refreshDisplay);

                    // Added tooregister for push notifications.
                registerForPushNotifications();

            }, handleError);

    이 예제에서는 인증 성공 후에 **registerForPushNotifications**를 호출하는 경우를 보여줍니다.  필요한 만큼 자주 `registerForPushNotifications()`를 호출할 수 있습니다.

2. 새 hello 추가 **registerForPushNotifications** 메서드를 다음과 같이 합니다.

        // Register for Push Notifications. Requires that phonegap-plugin-push be installed.
        var pushRegistration = null;
        function registerForPushNotifications() {
          pushRegistration = PushNotification.init({
              android: { senderID: 'Your_Project_ID' },
              ios: { alert: 'true', badge: 'true', sound: 'true' },
              wns: {}
          });

        // Handle hello registration event.
        pushRegistration.on('registration', function (data) {
          // Get hello native platform of hello device.
          var platform = device.platform;
          // Get hello handle returned during registration.
          var handle = data.registrationId;
          // Set hello device-specific message template.
          if (platform == 'android' || platform == 'Android') {
              // Register for GCM notifications.
              client.push.register('gcm', handle, {
                  mytemplate: { body: { data: { message: "{$(messageParam)}" } } }
              });
          } else if (device.platform === 'iOS') {
              // Register for notifications.
              client.push.register('apns', handle, {
                  mytemplate: { body: { aps: { alert: "{$(messageParam)}" } } }
              });
          } else if (device.platform === 'windows') {
              // Register for WNS notifications.
              client.push.register('wns', handle, {
                  myTemplate: {
                      body: '<toast><visual><binding template="ToastText01"><text id="1">$(messageParam)</text></binding></visual></toast>',
                      headers: { 'X-WNS-Type': 'wns/toast' } }
              });
          }
        });

        pushRegistration.on('notification', function (data, d2) {
          alert('Push Received: ' + data.message);
        });

        pushRegistration.on('error', handleError);
        }
3. (Android) Hello 코드 앞에, 바꿉니다 `Your_Project_ID` 된 hello 숫자 프로젝트에서 응용 프로그램에 대 한 ID는 [Google 개발자 콘솔][18]합니다.

## <a name="optional-configure-and-run-hello-app-on-android"></a>(선택 사항) 구성 하 고 hello 앱을 Android에서 실행
Android에 대 한이 섹션 tooenable 푸시 알림을 완료 합니다.

#### <a name="enable-gcm"></a>Firebase Cloud Messaging 사용
대상으로 hello Google Android 플랫폼 처음, 이후 Firebase Cloud Messaging 설정 해야 합니다.

[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

#### <a name="configure-backend"></a>FCM를 사용 하 여 hello 모바일 앱 백 엔드 toosend 푸시 요청 구성
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push.md)]

#### <a name="configure-your-cordova-app-for-android"></a>Android용 Cordova 앱 구성
Cordova 앱에서 config.xml 열고 대체 `Your_Project_ID` hello에서 응용 프로그램에 대 한 프로젝트 ID 된 hello 숫자 [Google 개발자 콘솔][18]합니다.

        <plugin name="phonegap-plugin-push" version="1.7.1" src="https://github.com/phonegap/phonegap-plugin-push.git">
            <variable name="SENDER_ID" value="Your_Project_ID" />
        </plugin>

Index.js를 열고 업데이트 hello 코드 toouse 프로그램 숫자 프로젝트 id입니다.

        pushRegistration = PushNotification.init({
            android: { senderID: 'Your_Project_ID' },
            ios: { alert: 'true', badge: 'true', sound: 'true' },
            wns: {}
        });

#### <a name="configure-device"></a>USB 디버깅을 위해 Android 장치 구성
사용자 응용 프로그램 tooyour Android 장치를 배포 하기 전에 tooenable USB 디버깅 해야 합니다.  Android 휴대폰에서 다음 단계를 수행합니다.

1. 너무 이동**설정** > **전화에 대 한**, hello를 탭 합니다 **빌드 번호** 개발자 모드 (약 7 번)에 사용 될 때까지 합니다.
2. 다시 **설정** > **개발자 옵션** 사용 **USB 디버깅**, 다음 Android 휴대폰 tooyour 개발 PC는 USB 케이블로 연결 합니다.

이 방법은 Android 6.0(Marshmallow)을 실행하는 Google Nexus 5X를 사용하여 테스트되었습니다.  그러나 hello 기술에서 공통 된 최신 Android 릴리스 합니다.

#### <a name="install-google-play-services"></a>Google Play Services 설치
hello 푸시 플러그 인 밀어넣기 알림에 대 한 Android Google Play 서비스에 의존합니다.

1. Visual Studio에서 클릭 **도구** > **Android** > **Android SDK Manager**, hello 확장 **Extras** 폴더 및 검사 hello 상자 toomake hello Sdk 다음의 각 설치 되어 있는지 합니다.

   * Android 2.3 이상
   * Google Repository 개정 27 이상
   * Google Play Services 9.0.2 이상

2. 클릭 **패키지 설치** hello 설치 toocomplete 될 때까지 기다립니다.

hello 현재 필요한 라이브러리 hello에 나열 된 [phonegap 플러그 인 푸시 설치 설명서][19]합니다.

#### <a name="test-push-notifications-in-hello-app-on-android"></a>Android에서 hello 앱에 푸시 알림을 테스트
이제 테스트 푸시 알림을 실행 하 여 응용 프로그램 및 hello TodoItem 테이블에 삽입 항목 hello 할 수 있습니다. 테스트할 수 있습니다 hello 동일한 장치 또는 두 번째 장치에서 사용 하는 환영 동일한 백 엔드 합니다. Hello 같은 방법으로 다음 중 하나 hello Android 플랫폼에서 Cordova 앱을 테스트 합니다.

* **물리적 장치에서:** USB 케이블을 사용 하 여 Android 장치 tooyour 개발 컴퓨터를 연결 합니다.  **Google Android 에뮬레이터** 대신 **장치**를 선택합니다. Visual Studio는 hello 응용 프로그램 toohello 장치를 배포 하 고 hello 응용 프로그램을 실행 합니다.  다음 hello 장치에서 hello 응용 프로그램과 상호 작용할 수 있습니다.

  개발 환경을 개선합니다.  [Mobizen] [ 20]과 같은 화면 공유 응용 프로그램을 사용하면 Android 응용 프로그램을 개발하는 데 도움이 될 수 있습니다.  Mobizen PC에서 Android 화면 tooa 웹 브라우저를 프로젝션합니다.

* **Android 에뮬레이터에서:** 에뮬레이터에서 실행할 때 필요한 추가 구성 단계가 있습니다.

    Hello Android Virtual Device (AVD) 관리자에 표시 된 대로 hello 대상으로 설정 하는 Google Api가 tooa 가상 장치를 배포 하는 있는지 확인 합니다.

    ![](./media/app-service-mobile-cordova-get-started-push/google-apis-avd-settings.png)

    Toouse 더 빠른 x86를 원하는 경우 에뮬레이터 있습니다 [hello HAXM 드라이버를 설치] [ 11] hello 에뮬레이터 toouse 구성 및 것입니다.

    클릭 하 여 Google 계정 toohello Android 장치를 추가 **앱** > **설정** > **계정을 추가**, 다음 hello 프롬프트를 따릅니다.

    ![](./media/app-service-mobile-cordova-get-started-push/add-google-account.png)

    앞으로 hello todolist 앱을 실행 하 고 새 할 일 항목을 삽입 합니다. 이 이번에는 알림 아이콘 hello 알림 영역에 표시 됩니다. Hello 알림 서랍 tooview hello의 전체 텍스트 알림 hello 열 수 있습니다.

    ![](./media/app-service-mobile-cordova-get-started-push/android-notifications.png)

## <a name="optional-configure-and-run-on-ios"></a>(선택 사항) iOS에서 구성 및 실행
이 섹션은 iOS 장치에서 hello Cordova 프로젝트를 실행 합니다. iOS 장치로 작업하지 않는 경우 이 섹션을 건너뛸 수 있습니다.

#### <a name="install-and-run-hello-ios-remote-build-agent-on-a-mac-or-cloud-service"></a>Mac 또는 클라우드 서비스에는 빌드 에이전트 설치 및 실행된 hello iOS 원격
Visual Studio를 사용 하 여 iOS에서 Cordova 앱을 실행할 수 있습니다, 전에 hello에 hello 단계를 수행해 [iOS 설치 가이드] [ 12] tooinstall와 실행된 hello 원격 빌드 에이전트입니다.

IOS 용 hello 앱을 빌드할 수 있는지 확인 합니다. hello hello 설치 가이드의 단계는 Visual Studio에서 iOS에 대 한 필수 toobuild 합니다. Mac가 hello 원격 빌드 에이전트를 사용 하 여 MacInCloud와 같은 서비스에서 iOS를 빌드할 수 있습니다. 자세한 내용은 참조 하십시오. [hello 클라우드에서 iOS 앱을 실행][21]합니다.

> [!NOTE]
> XCode 7 이상이 필요한 toouse hello iOS에서 플러그 인 밀어넣기입니다.

#### <a name="find-hello-id-toouse-as-your-app-id"></a>응용 프로그램 ID로 hello ID toouse 찾기
푸시 알림에 대 한 앱을 등록 하려면 먼저 Cordova 앱에서 config.xml을 열고, hello `id` 특성 hello 위젯 요소에 값이 있고 나중에 사용할 수 있기 때문입니다. Hello ID는 다음과 같은 XML hello, `io.cordova.myapp7777777`합니다.

        <widget defaultlocale="en-US" id="io.cordova.myapp7777777"
          version="1.0.0" windows-packageVersion="1.1.0.0" xmlns="http://www.w3.org/ns/widgets"
            xmlns:cdv="http://cordova.apache.org/ns/1.0" xmlns:vs="http://schemas.microsoft.com/appx/2014/htmlapps">

나중에 Apple 개발자 포털에서 앱 ID를 만들 때 이 식별자를 사용합니다. Hello 개발자 포털에 다른 응용 프로그램 ID를 만들면이 자습서의 뒷부분에 나오는 몇 가지 추가 단계를 수행 해야 합니다. 위젯 요소 hello ID hello 개발자 포털에서 앱 ID hello와 일치 해야 합니다.

#### <a name="register-hello-app-for-push-notifications-on-apples-developer-portal"></a>Apple 개발자 포털에서 푸시 알림을 hello 앱 등록
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

[유사한 단계를 보여 주는 비디오 보기](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-5-Set-up-apns-for-push)

#### <a name="configure-azure-toosend-push-notifications"></a>Azure toosend 푸시 알림 구성
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

#### <a name="verify-that-your-app-id-matches-your-cordova-app"></a>앱 ID가 Cordova 앱과 일치하는지 확인
Hello 이미 Apple 개발자 계정에서 만든 응용 프로그램 ID의 hello 위젯 요소를 config.xml에 hello ID와 일치할 경우이 단계를 건너뛸 수 있습니다. 그러나 hello Id가 일치 하지 않는 경우 hello 다음 단계를 수행 합니다.

1. 프로젝트에서 hello 플랫폼 폴더를 삭제 합니다.
2. 프로젝트에서 hello 플러그 인 폴더를 삭제 합니다.
3. 프로젝트에서 hello node_modules 폴더를 삭제 합니다.
4. Config.xml toouse hello Apple 개발자 계정에서 만든 응용 프로그램 ID에에서 대 한 hello 위젯 요소의 hello id 특성을 업데이트 합니다.
5. 프로젝트를 다시 빌드합니다.

##### <a name="test-push-notifications-in-your-ios-app"></a>iOS 앱에서 푸시 알림 테스트
1. Visual Studio에서 확인 **iOS** hello 배포 대상으로 선택한 다음 선택 **장치** 연결 된 iOS 장치에서 toorun 합니다.

    IOS 장치가 연결 tooyour PC에서 실행할 수 있습니다 iTunes를 사용 하 여 합니다. hello iOS 시뮬레이터에 푸시 알림을 지원 하지 않습니다.

2. 키를 눌러 hello **실행** 단추 또는 **F5** 에서 Visual Studio toobuild hello 프로젝트와 시작 hello, iOS 장치에서 응용 프로그램 클릭 한 다음 **확인** tooaccept 푸시 알림을 합니다.

   > [!NOTE]
   > hello 앱 hello 먼저 실행 하는 동안 푸시 알림을 확인 하 라는 요청입니다.

3. Hello 앱에서 작업을 입력 하 고 hello 더하기 (+)를 클릭 한 다음 아이콘입니다.
4. 확인 알림이 수신 되 고 확인 toodismiss hello 알림을 클릭 합니다.

## <a name="optional-configure-and-run-on-windows"></a>(선택 사항) Windows에서 구성 및 실행
이 섹션 (hello PhoneGap 푸시 플러그 인은 Windows 10에서 지원 됨)는 Windows 10 장치에서 hello Apache Cordova 앱 프로젝트를 실행 하기 위한입니다. Windows 장치로 작업하지 않는 경우 이 섹션을 건너뛸 수 있습니다.

#### <a name="register-your-windows-app-for-push-notifications-with-wns"></a>WNS를 사용하여 푸시 알림에 대해 Windows 앱 등록
Visual Studio에서 toouse hello 저장소 옵션 hello 솔루션 플랫폼 목록에서 원하는 Windows 대상을 선택 **x64** 또는 **x86** (방지 **Windows AnyCPU** 에 대 한 푸시 알림).

[!INCLUDE [app-service-mobile-register-wns](../../includes/app-service-mobile-register-wns.md)]

[유사한 단계를 보여 주는 비디오 보기][13]

#### <a name="configure-hello-notification-hub-for-wns"></a>Wns hello 알림 허브를 구성 합니다.
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

#### <a name="configure-your-cordova-app-toosupport-windows-push-notifications"></a>Cordova 앱 toosupport Windows 푸시 알림 구성
구성 디자이너 열기 hello (단추로 클릭 하 고 config.xml **뷰 디자이너**)을 선택 hello **Windows** 탭을 선택한 **Windows 10** 아래**Windows 버전을 대상**합니다.

기본 (디버그)에 푸시 알림을 toosupport 빌드 열기 build.json 파일. "릴리스" 구성 tooyour 디버그 구성에 복사 합니다.

        "windows": {
            "release": {
                "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
                "publisherId": "CN=yourpublisherID"
            }
        }

Hello 업데이트 후 hello build.json 코드 다음 hello를 포함 되어야 합니다.

    "windows": {
        "release": {
            "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
            "publisherId": "CN=yourpublisherID"
            },
        "debug": {
            "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
            "publisherId": "CN=yourpublisherID"
            }
        }

Hello 앱을 빌드하고 오류 없이 있는지 확인 합니다. 이제 hello 모바일 앱 백 엔드에서 hello 알림에 대 한 경우에 클라이언트 앱 등록 해야 합니다. 솔루션의 모든 Windows 프로젝트에 대해 이 섹션을 반복합니다.

#### <a name="test-push-notifications-in-your-windows-app"></a>Windows 앱에서 푸시 알림 테스트
Visual Studio에서 Windows 플랫폼와 같은 hello 배포 대상으로 선택 되어 있는지 확인 **x64** 또는 **x86**합니다. Visual Studio를 호스팅하는 Windows 10 PC에 toorun hello 앱 선택 **로컬 컴퓨터**합니다.

키를 눌러 hello 단추 toobuild hello 프로젝트를 실행 하 고 hello 응용 프로그램을 시작 합니다.

Hello 응용 프로그램에서 새 todoitem에 대 한 이름을 입력 하 고 hello 더하기 (+)를 클릭 한 다음 아이콘 tooadd 것입니다.

Hello 항목이 추가 될 때 알림을 받았는지 확인 합니다.

## <a name="next-steps"></a>다음 단계
* 에 대 한 읽기 [알림 허브] [ 17] toolearn 푸시 알림에 대 한 합니다.
* 이미 수행 하 여 hello 자습서를 계속 [인증 추가] [ 14] tooyour Apache Cordova 앱.

Toouse Sdk hello 하는 방법에 대해 알아봅니다.

* [Apache Cordova SDK][15]
* [ASP.NET 서버 SDK][1]
* [Node.js 서버 SDK][16]

<!-- Images -->
[img1]: ./media/app-service-mobile-cordova-get-started-push/add-push-plugin.png

<!-- URLs -->
[1]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[2]: http://www.visualstudio.com/
[3]: https://azure.microsoft.com/pricing/free-trial/
[4]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx
[5]: app-service-mobile-cordova-get-started.md
[6]: http://go.microsoft.com/fwlink/p/?LinkId=268302
[7]: https://developer.apple.com/programs/
[8]: https://developer.microsoft.com/en-us/store/register
[9]: https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-3-Create-azure-notification-hub
[10]: https://www.npmjs.com/
[11]: https://taco.visualstudio.com/en-us/docs/run-app-apache/#HAXM
[12]: http://taco.visualstudio.com/en-us/docs/ios-guide/
[13]: https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-6-Set-up-wns-for-push
[14]: app-service-mobile-cordova-get-started-users.md
[15]: app-service-mobile-cordova-how-to-use-client-library.md
[16]: app-service-mobile-node-backend-how-to-use-server-sdk.md
[17]: ../notification-hubs/notification-hubs-push-notification-overview.md
[18]: https://console.developers.google.com/home/dashboard
[19]: https://github.com/phonegap/phonegap-plugin-push/blob/master/docs/INSTALLATION.md
[20]: https://www.mobizen.com/
[21]: http://taco.visualstudio.com/en-us/docs/build_ios_cloud/

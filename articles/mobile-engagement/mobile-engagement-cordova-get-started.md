---
title: "aaaGet Cordova/Phonegap에 대 한 Azure Mobile Engagement와 시작 됨"
description: "자세한 내용은 방법 Cordova/Phonegap 앱에 대 한 분석 및 푸시 알림을 사용 하 여 Azure Mobile Engagement toouse 합니다."
services: mobile-engagement
documentationcenter: Mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 54fe9113-e239-4ed7-9fd1-a502d7ac7f47
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-phonegap
ms.devlang: js
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: e67dabbdf7886802bb058f38964e558d5ae6854c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-cordovaphonegap"></a>Cordova/Phonegap용 Azure Mobile Engagement 시작
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

이 항목에서는 Cordova를 사용 하 여 응용 프로그램 사용과 송신 푸시 알림을 toosegmented 사용자가 모바일 응용 프로그램에 대 한 개발 toouse Azure Mobile Engagement toounderstand 합니다.

이 자습서에서는 Mac을 사용하여 빈 Cordova 앱을 만들고 Mobile Engagement SDK를 통합합니다. 기본 분석 데이터를 수집하고 iOS용 APNS(Apple 푸시 알림 시스템) 및 Android용 GCM(Google Cloud Messaging)을 사용하여 푸시 알림을 받습니다. 에서는이 tooan iOS 나 Android 장치 테스트를 위한 배포 합니다. 

> [!NOTE]
> toocomplete이이 자습서에서는 활성 Azure 계정이 있어야 합니다. 계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다. 자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-cordova-get-started)을 참조하세요.
> 
> 

이 자습서는 hello 다음을 사항이 필요합니다.

* XCode는 (tooiOS 배포용) Mac 앱 스토어에서 설치할 수 있습니다
* [Android SDK 및 에뮬레이터](http://developer.android.com/sdk/installing/index.html) (tooAndroid 배포용)
* APNS을 위해 Apple 개발자 센터에서 가져올 수 있는 푸시 알림 인증서(.p12)
* GCM을 위해 Google 개발자 콘솔에서 가져올 수 있는 GCM 프로젝트 번호
* [Mobile Engagement Cordova 플러그 인](https://www.npmjs.com/package/cordova-plugin-ms-azure-mobile-engagement)

> [!NOTE]
> 에 hello Cordova 플러그 인에 대 한 추가 정보를 hello와 hello 소스 코드를 찾을 수 [GitHub](https://github.com/Azure/azure-mobile-engagement-cordova)
> 
> 

## <a id="setup-azme"></a>Cordova 앱용 Mobile Engagement 설정
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>응용 프로그램 toohello Mobile Engagement 백 엔드 연결
이 자습서에는 "기본 통합" hello 최소 필수 toocollect 데이터 설정 되 고 푸시 알림을 보내려면 표시 합니다. 

Cordova toodemonstrate hello 통합 기본 앱을 만듭니다.

### <a name="create-a-new-cordova-project"></a>새 Cordova 프로젝트 만들기
1. 시작 *터미널* hello 기본 서식 파일에서 새 Cordova 프로젝트를 만듭니다는 뒤에 Mac 컴퓨터 및 형식 hello에 창. hello 게시 프로필 결국 사용 toodeploy 있는지 확인 하십시오. 앱 ID hello으로 iOS 앱 'com.mycompany.myapp'를 사용 하는 
   
        $ cordova create azme-cordova com.mycompany.myapp
        $ cd azme-cordova
2. 다음 tooconfigure hello에 대 한 프로젝트 실행 **iOS** hello iOS 시뮬레이터에서에서 실행 합니다.
   
        $ cordova platform add ios 
        $ cordova run ios
3. 다음 tooconfigure hello에 대 한 프로젝트 실행 **Android** hello Android 에뮬레이터에서 실행 합니다. Android SDK 에뮬레이터 설정을 갖도록 대상 Google Api (Google Inc.)으로 hello cpu / ABI Google Api ARM으로 합니다.  
   
        $ cordova platform add android
        $ cordova run android
4. Hello Cordova 콘솔 플러그 인을 추가 합니다. 

    ```
    $ cordova plugin add cordova-plugin-console
    ``` 

### <a name="connect-your-app-toomobile-engagement-backend"></a>응용 프로그램 tooMobile Engagement 백 엔드 연결
1. Hello 변수 값 tooconfigure hello 플러그 인을 제공 하면서 hello Azure Mobile Engagement Cordova 플러그 인을 설치 합니다.
   
        cordova plugin add cordova-plugin-ms-azure-mobile-engagement    
             --variable AZME_IOS_CONNECTION_STRING=<iOS Connection String> 
            --variable AZME_IOS_REACH_ICON=... (icon name WITH extension) 
            --variable AZME_ANDROID_CONNECTION_STRING=<Android Connection String> 
            --variable AZME_ANDROID_REACH_ICON=... (icon name WITHOUT extension)       
            --variable AZME_ANDROID_GOOGLE_PROJECT_NUMBER=... (From your Google Cloud console for sending push notifications) 
            --variable AZME_ACTION_URL =... (URL scheme which triggers hello app for deep linking)
            --variable AZME_ENABLE_NATIVE_LOG=true|false
            --variable AZME_ENABLE_PLUGIN_LOG=true|false

*Android 도달 아이콘* : 모든 확장 프로그램 또는 그릴 수 있는 접두사 없이 hello 리소스의 hello 이름 이어야 합니다 (예: mynotificationicon), hello 아이콘 파일 (플랫폼/android/r e s/그릴) android 프로젝트에 복사 해야 하 고

*iOS 도달 아이콘* : 확장명과 hello 리소스의 hello 이름 이어야 합니다 (예: mynotificationicon.png), hello 아이콘 파일 (hello 추가 파일 메뉴 사용) 하는 xcode iOS 프로젝트에 추가 되어야 합니다

## <a id="monitor"></a>실시간 모니터링 사용
1. Hello Cordova 프로젝트-에서 편집 **www/js/index.js** tooMobile Engagement toodeclare 새 활동을 한 번 hello tooadd hello 호출 *deviceReady* 이벤트가 수신 됩니다.
   
         onDeviceReady: function() {
                Engagement.startActivity("myPage",{});
            }
2. Hello 응용 프로그램을 실행 합니다.
   
   * **iOS의 경우**
     
       `Terminal` 창이 hello 다음을 실행 하 여 새 시뮬레이터 인스턴스에서 응용 프로그램을 시작 합니다.
     
           cordova run ios
   * **Android의 경우**
     
       `Terminal` 창이 hello 다음을 실행 하 여 새 에뮬레이터 인스턴스에서 응용 프로그램을 시작 합니다.
     
           cordova run android
3. Hello 다음 hello 콘솔 로그에서 확인할 수 있습니다.
   
        [Engagement] Agent: Session started
        [Engagement] Agent: Activity 'myPage' started
        [Engagement] Connection: Established
        [Engagement] Connection: Sent: appInfo
        [Engagement] Connection: Sent: startSession
        [Engagement] Connection: Sent: activity name='myPage'

## <a id="monitor"></a>실시간 모니터링과 앱 연결
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>푸시 알림 및 앱 내 메시징 사용
Mobile Engagement 푸시 알림과 앱 내 메시징을 캠페인의 hello 컨텍스트에서 사용 하 여 사용자와 toointeract를 허용 합니다. 이 모듈에는 hello Mobile engagement 연결 포털에서 REACH를 라고 합니다.
hello 다음 섹션에서는 설치 응용 프로그램 tooreceive 해당 합니다.

### <a name="configure-push-credentials-for-mobile-engagement"></a>Mobile Engagement에 대한 푸시 자격 증명 구성
사용자 대신 tooallow Mobile Engagement toosend 푸시 알림을, toogrant tooyour Apple iOS 인증서 또는 GCM 서버 API 키에 액세스 해야 합니다. 

1. Mobile engagement 연결 포털 tooyour 이동 합니다. Hello 앱에서는이 프로젝트에 대 한 사용 중이 고 hello에서 클릭 한 다음에 있는 확인 **사로잡는 구성** hello 아래쪽 단추:
   
    ![][1]
2. Engagement 연결 포털에서 hello 설정 페이지에 배치 됩니다. Hello 없어 클릭에서 **하 여 네이티브 푸시** 섹션:
   
    ![][2]
3. iOS 인증서/GCM 서버 API 키 구성
   
    **[iOS]**
   
    a. 다음과 같이 .p12를 선택하여 업로드하고 암호를 입력합니다.
   
    ![][3]
   
    **[Android]**
   
    a. 앞의 hello 편집 아이콘을 클릭 **API 키** hello GCM 설정 섹션 및 참석 hello 팝업 hello GCM 서버 키를 붙여 넣고 클릭 **확인**합니다. 
   
    ![][4]

### <a name="enable-push-notifications-in-hello-cordova-app"></a>Hello Cordova 앱에 푸시 알림을 사용 하도록 설정
편집 **www/js/index.js** tooadd hello 호출 tooMobile Engagement toorequest 푸시 알림 및 처리기를 선언 합니다.

     onDeviceReady: function() {
           Engagement.initializeReach(  
                 // on OpenUrl  
                 function(_url) {   
                 alert(_url);   
                 });  
            Engagement.startActivity("myPage",{});  
        }

### <a name="run-hello-app"></a>Hello 앱 실행
**[iOS]**

1. XCode toobuild를 사용 하 고 iOS에만 푸시 알림을 tooan 실제 장치에서는 있으므로 hello 장치 tootest 푸시 알림에 hello 앱을 배포 합니다. Cordova 프로젝트를 만들 위치 toohello 위치를 이동 하 고 탐색 너무**...\platforms\ios** 위치 합니다. XCode에서 hello 네이티브.xcodeproj 파일을 엽니다. 
2. 빌드 및 프로비저닝 프로필 toohello Mobile engagement 연결 포털 및 앱 Id를 만드는 동안 제공한 hello에 일치 하는 hello 업로드 hello 인증서가 포함 된 hello 있는 hello 계정을 사용 하 여 hello Cordova 앱 toohello iOS 장치를 배포 합니다. hello Cordova 응용 프로그램입니다. Hello 확인할 수 있습니다 *번들 식별자* 에 프로그램 **리소스\*-info.plist** 파일 XCode toomatch 것을 합니다. 
3. 권한 toosend 알림을 요청 하는 hello 표준 iOS 팝업 hello 앱 라는 장치에서 볼 수 있습니다. Hello 권한을 부여 합니다. 

**[Android]**

GCM 알림을 hello Android 에뮬레이터에서 지원 되는 단순히 hello 에뮬레이터 toorun hello Android 앱을 사용할 수 있습니다. 

    cordova run android

## <a id="send"></a>보낼 알림 tooyour 앱
이제 단순한 푸시 알림을 캠페인의 hello 장치에서 실행 되는 푸시 tooyour 앱 보낼 사항을 만듭니다.

1. Toohello 이동 **도달** Mobile engagement 연결 포털에서 탭
2. 클릭 **새 공지** toocreate 푸시 캠페인
   
    ![][6]
3. 입력 toocreate 캠페인 제공 **[Android]**
   
   * 캠페인에 **이름** 을 제공합니다. 
   * 선택 hello **배달 유형** 으로 *시스템 알림* *단순*
   * 선택 hello **배달 시간** 으로 *"Any 시간"*
   * 제공 된 **제목** hello 푸시에서 첫 번째 줄 hello 될 알림에 합니다.
   * 제공 된 **메시지** hello 메시지 본문으로 사용할 알림에 합니다. 
     
     ![][11]
4. 입력 toocreate 캠페인 제공 **[iOS]**
   
   * 캠페인에 **이름** 을 제공합니다. 
   * 선택 hello **배달 시간** 으로 *"app" 부족*
   * 제공 된 **제목** hello 푸시에서 첫 번째 줄 hello 될 알림에 합니다.
   * 제공 된 **메시지** hello 메시지 본문으로 사용할 알림에 합니다. 
     
     ![][12]
5. Hello에서 콘텐츠 섹션을 선택 하 고 아래로 스크롤하여 **알림 전용**
   
    ![][8]
6. [선택 사항] 작업 URL을 제공할 수도 있습니다. Hello 플러그 인을 구성 하는 동안 제공 된 URL 체계를 사용 하는지 확인 **AZME\_리디렉션\_URL** 변수 예: *myapp://test*합니다.  
7. 설정을 hello 가장 기본적인 캠페인 가능한 작업이 끝났습니다. 이제 다시 아래로 스크롤하여 하 고 hello 클릭 **만들기** toosave 캠페인 단추입니다.
8. 마지막으로 캠페인을 **활성화** 합니다.
   
    ![][10]
9. 이제 이 캠페인 부분으로 장치나 에뮬레이터에 푸시 알림이 표시되어야 합니다. 

## <a id="next-steps"></a>다음 단계
[Cordova Mobile Engagement SDK에서 사용 가능한 모든 방법의 개요](https://github.com/Azure/azure-mobile-engagement-cordova)

<!-- Images. -->

[1]: ./media/mobile-engagement-cordova-get-started/engage-button.png
[2]: ./media/mobile-engagement-cordova-get-started/engagement-portal.png
[3]: ./media/mobile-engagement-cordova-get-started/native-push-settings.png
[4]: ./media/mobile-engagement-cordova-get-started/api-key.png
[6]: ./media/mobile-engagement-cordova-get-started/new-announcement.png
[8]: ./media/mobile-engagement-cordova-get-started/campaign-content.png
[10]: ./media/mobile-engagement-cordova-get-started/campaign-activate.png
[11]: ./media/mobile-engagement-cordova-get-started/campaign-first-params-android.png
[12]: ./media/mobile-engagement-cordova-get-started/campaign-first-params-ios.png


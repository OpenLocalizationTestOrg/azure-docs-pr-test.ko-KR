---
title: "iOS Swift에 대 한 Azure Mobile Engagement와 시작 됨 aaaGet | Microsoft Docs"
description: "자세한 내용은 방법 iOS 앱에 대 한 분석 및 푸시 알림을 사용 하 여 Azure Mobile Engagement toouse 합니다."
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 196c282d-6f2f-4cbc-aeee-6517c5ad866d
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: swift
ms.topic: hero-article
ms.date: 09/20/2016
ms.author: piyushjo
ms.openlocfilehash: 9a3841d305745f8b80c6b0c86aabe18e0c7c0e59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-ios-apps-in-swift"></a>Swift에서 iOS 앱용 Azure Mobile Engagement 시작
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

이 항목에서는 Azure Mobile Engagement toounderstand toouse 응용 프로그램 사용 및 송신 푸시 알림 toosegmented 사용자 tooan iOS 응용 프로그램입니다.
이 자습서에서는 기본 데이터를 수집하고 APNS(Apple 푸시 알림 시스템)를 사용하여 푸시 알림을 받는 빈 iOS 앱을 만듭니다.

이 자습서는 hello 다음을 사항이 필요합니다.

* MAC 앱 스토어에서 설치할 수 있는 XCode 8
* hello [Mobile Engagement iOS SDK]
* Apple 개발자 센터에서 가져올 수 있는 푸시 알림 인증서(.p12)

> [!NOTE]
> 이 자습서에서는 Swift 버전 3.0을 사용합니다. 
> 
> 

이 자습서를 완료해야 다른 모든 iOS 앱용 Mobile Engagement 자습서를 진행할 수 있습니다.

> [!NOTE]
> toocomplete이이 자습서에서는 활성 Azure 계정이 있어야 합니다. 계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다. 자세한 내용은 [Azure 평가판](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-swift-get-started)을 참조하세요.
> 
> 

## <a id="setup-azme"></a>iOS 앱용 Mobile Engagement 설정
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>응용 프로그램 toohello Mobile Engagement 백 엔드 연결
이 자습서는 기본적인 "통합", 최소 hello 필요한 toocollect 데이터 설정 되 고 푸시 알림을 보내는 표시 합니다. hello에 hello 완벽 한 통합 설명서를 확인할 수 있습니다 [Mobile Engagement iOS SDK 통합](mobile-engagement-ios-sdk-overview.md)

XCode toodemonstrate hello 통합 기본 앱을 만듭니다.

### <a name="create-a-new-ios-project"></a>새 iOS 프로젝트 만들기
[!INCLUDE [Create a new iOS Project](../../includes/mobile-engagement-create-new-ios-app.md)]

### <a name="connect-your-app-toomobile-engagement-backend"></a>응용 프로그램 tooMobile Engagement 백 엔드 연결
1. Hello 다운로드 [Mobile Engagement iOS SDK]
2. Hello를 추출 합니다. 컴퓨터에 tar.gz 파일 tooa 폴더
3. Hello 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 "파일을 너무 추가..."
   
    ![][1]
4. Hello SDK 및 선택 hello 추출한 toohello 폴더 탐색 `EngagementSDK` 폴더 다음 확인을 누르십시오.
   
    ![][2]
5. 열기 hello `Build Phases` 탭 및 hello `Link Binary With Libraries` 메뉴 아래와 같이 hello 프레임 워크를 추가 합니다.
   
    ![][3]
6. 파일을 선택 하 여 한 브리징 헤더 toobe 수 toouse hello SDK의 목적은 C Api 만들기 > 새로 만들기 > 파일 > iOS > 소스 > 헤더 파일입니다.
   
    ![][4]
7. Hello 브리징 헤더 파일 tooexpose Mobile Engagement Objective-c 코드 tooyour Swift 코드 편집, 추가 import를 수행 하는 hello:
   
        /* Mobile Engagement Agent */
        #import "AEModule.h"
        #import "AEPushMessage.h"
        #import "AEStorage.h"
        #import "EngagementAgent.h"
        #import "EngagementTableViewController.h"
        #import "EngagementViewController.h"
        #import "AEUserNotificationHandler.h"
        #import "AEIdfaProvider.h"
8. 빌드 설정에서 Objective-c 브리징 헤더 빌드 Swift 컴파일러-코드 생성에서 설정 하는 hello 경로 toothis 헤더에 있는지를 확인 합니다. 경로 예제는 다음과 같습니다: **$(SRCROOT)/MySuperApp/MySuperApp-Bridging-Header.h (hello 경로)에 따라 다름**
   
   ![][6]
9. Azure 포털에서 앱의 toohello 돌아가서 *연결 정보입니다.* 페이지 및 복사 hello 연결 문자열
   
   ![][5]
10. 이제 hello에 hello 연결 문자열을 붙여 `didFinishLaunchingWithOptions` 위임
    
        func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool
        {
              [...]
                EngagementAgent.init("Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}")
              [...]
        }

## <a id="monitor"></a>실시간 모니터링 사용
순서 toostart 데이터를 보내고는 hello 사용자가 활성화 되도록 하나 이상 화면 (활동) toohello Mobile Engagement 백 엔드를 보내야 합니다.

1. 열기 hello **ViewController.swift** hello의 기본 클래스를 바꾸고 파일 **ViewController** toobe **EngagementViewController**:
   
    `class ViewController : EngagementViewController {`

## <a id="monitor"></a>실시간 모니터링과 앱 연결
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>푸시 알림 및 앱 내 메시징 사용
Mobile Engagement 있습니다 toointeract 및 푸시 알림과 앱 내 메시징을와 사용자와 REACH 캠페인의 hello 컨텍스트에서. 이 모듈에는 hello Mobile engagement 연결 포털에서 REACH를 라고 합니다.
hello 다음 섹션에서는 설치 응용 프로그램 tooreceive 해당 합니다.

### <a name="enable-your-app-tooreceive-silent-push-notifications"></a>사용자 앱 tooreceive 자동 푸시 알림을 사용 하도록 설정
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

### <a name="add-hello-reach-library-tooyour-project"></a>Hello Reach 라이브러리 tooyour 프로젝트 추가
1. 프로젝트를 마우스 오른쪽 단추로 클릭합니다.
2. `Add file too...`을(를) 선택합니다.
3. Hello SDK의 압축을 푼 toohello 폴더 이동
4. 선택 hello `EngagementReach` 폴더
5. 추가를 클릭합니다.
6. 브리징 헤더 파일 tooexpose Mobile Engagement Objective-c Reach 헤더 hello 편집한 다음 imports hello 추가:
   
        /* Mobile Engagement Reach */
        #import "AEAnnouncementViewController.h"
        #import "AEAutorotateView.h"
        #import "AEContentViewController.h"
        #import "AEDefaultAnnouncementViewController.h"
        #import "AEDefaultNotifier.h"
        #import "AEDefaultPollViewController.h"
        #import "AEInteractiveContent.h"
        #import "AENotificationView.h"
        #import "AENotifier.h"
        #import "AEPollViewController.h"
        #import "AEReachAbstractAnnouncement.h"
        #import "AEReachAnnouncement.h"
        #import "AEReachContent.h"
        #import "AEReachDataPush.h"
        #import "AEReachDataPushDelegate.h"
        #import "AEReachModule.h"
        #import "AEReachNotifAnnouncement.h"
        #import "AEReachPoll.h"
        #import "AEReachPollQuestion.h"
        #import "AEViewControllerUtil.h"
        #import "AEWebAnnouncementJsBridge.h"

### <a name="modify-your-application-delegate"></a>응용 프로그램 대리자 수정
1. 내부 hello `didFinishLaunchingWithOptions` -reach 모듈 만들고 tooyour 기존 Engagement 초기화 줄 전달 합니다.
   
        func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool 
        {
            let reach = AEReachModule.module(withNotificationIcon: UIImage(named:"icon.png")) as! AEReachModule
            EngagementAgent.init("Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}", modulesArray:[reach])
            [...]
            return true
        }

### <a name="enable-your-app-tooreceive-apns-push-notifications"></a>사용자 응용 프로그램 tooreceive APNS 푸시 알림을 사용 하도록 설정
1. 다음 줄 toohello hello 추가 `didFinishLaunchingWithOptions` 메서드:
   
        if #available(iOS 8.0, *)
        {
            if #available(iOS 10.0, *)
            {
                UNUserNotificationCenter.current().requestAuthorization(options: [.alert, .badge, .sound]) { (granted, error) in }
            }else
            {
                let settings = UIUserNotificationSettings(types: [.alert, .badge, .sound], categories: nil)
                application.registerUserNotificationSettings(settings)
            }
            application.registerForRemoteNotifications()
        }
        else
        {
            application.registerForRemoteNotifications(matching: [.alert, .badge, .sound])
        }
2. Hello 추가 `didRegisterForRemoteNotificationsWithDeviceToken` 메서드를 다음과 같이 합니다.
   
        func application(_ application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data) {
            EngagementAgent.shared().registerDeviceToken(deviceToken)
        }
3. Hello 추가 `didReceiveRemoteNotification:fetchCompletionHandler:` 메서드를 다음과 같이 합니다.
   
        func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any], fetchCompletionHandler completionHandler: @escaping (UIBackgroundFetchResult) -> Void) {
            EngagementAgent.shared().applicationDidReceiveRemoteNotification(userInfo, fetchCompletionHandler:completionHandler)
        }

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- URLs. -->
[Mobile Engagement iOS SDK]: http://aka.ms/qk2rnj

<!-- Images. -->
[1]: ./media/mobile-engagement-ios-get-started/xcode-add-files.png
[2]: ./media/mobile-engagement-ios-get-started/xcode-select-engagement-sdk.png
[3]: ./media/mobile-engagement-ios-get-started/xcode-build-phases.png
[4]: ./media/mobile-engagement-ios-swift-get-started/add-header-file.png
[5]: ./media/mobile-engagement-ios-get-started/app-connection-info-page.png
[6]: ./media/mobile-engagement-ios-swift-get-started/add-bridging-header.png

---
title: "Objective C의 iOS 용 Azure Mobile Engagement와 시작 됨 aaaGet | Microsoft Docs"
description: "자세한 내용은 방법 toouse Azure Mobile Engagement iOS 앱에 대 한 분석 및 푸시 알림입니다."
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 117b5742-522b-41de-98c5-f432da2d98f8
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: hero-article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: 51a5013f23d2d04a7b9b30c83b47017898b2bb00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-ios-apps-in-objective-c"></a>Objective C에서 iOS 앱용 Azure Mobile Engagement 시작
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

이 항목에서는 Azure Mobile Engagement toounderstand toouse 응용 프로그램 사용 및 송신 푸시 알림 toosegmented 사용자 tooan iOS 응용 프로그램입니다.
이 자습서에서는 기본 데이터를 수집하고 APNS(Apple 푸시 알림 시스템)를 사용하여 푸시 알림을 받는 빈 iOS 앱을 만듭니다.

이 자습서는 hello 다음을 사항이 필요합니다.

* MAC 앱 스토어에서 설치할 수 있는 XCode 8
* hello [Mobile Engagement iOS SDK]

이 자습서를 완료해야 다른 모든 iOS 앱용 Mobile Engagement 자습서를 진행할 수 있습니다.

> [!NOTE]
> toocomplete이이 자습서에서는 활성 Azure 계정이 있어야 합니다. 계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다. 자세한 내용은 [Azure 평가판](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-get-started)을 참조하세요.
>
>

## <a id="setup-azme"></a>iOS 앱용 Mobile Engagement 설정
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>응용 프로그램 toohello Mobile Engagement 백 엔드 연결
이 자습서는 기본적인 "통합", 최소 hello 필요한 toocollect 데이터 설정 되 고 푸시 알림을 보내는 표시 합니다. hello에 hello 완벽 한 통합 설명서를 확인할 수 있습니다 [Mobile Engagement iOS SDK 통합](mobile-engagement-ios-sdk-overview.md)

XCode toodemonstrate hello 통합 기본 앱을 만듭니다.

### <a name="create-a-new-ios-project"></a>새 iOS 프로젝트 만들기
[!INCLUDE [Create a new iOS Project](../../includes/mobile-engagement-create-new-ios-app.md)]

### <a name="connect-your-app-toohello-mobile-engagement-backend"></a>응용 프로그램 toohello Mobile Engagement 백 엔드 연결
1. Hello 다운로드 [Mobile Engagement iOS SDK]합니다.
2. Hello를 추출 합니다. 컴퓨터에 tar.gz 파일 tooa 폴더입니다.
3. Hello 프로젝트를 마우스 오른쪽 단추로 클릭 한 다음 선택 **파일을 추가**합니다.

    ![][1]
4. Hello SDK의 압축을 푼 toohello 폴더를 탐색, hello 선택 `EngagementSDK` 폴더를 클릭 하 여 **옵션** 왼쪽된 아래 모서리 hello 되 고 해당 hello 확인란이 있는지 확인 **필요한 경우 항목을 복사할** 및 hello 대상에 대 한 확인란 확인 한 다음 키를 눌러 **확인**합니다.

    ![][2]
5. 열기 hello **빌드 단계** 탭 및 hello **링크 이진 파일과 라이브러리** 메뉴에서 다음과 같이 hello 프레임 워크를 추가:

    ![][3]
6. Azure 포털에서 앱의 toohello 돌아가서 **연결 정보입니다.** 페이지 및 복사 hello 연결 문자열입니다.

    ![][4]
7. Hello 다음에 코드 줄을 추가 하면 **AppDelegate.m** 파일입니다.

        #import "EngagementAgent.h"
8. 이제 hello에 hello 연결 문자열을 붙여 `didFinishLaunchingWithOptions` 위임 합니다.

        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
        {
              [...]   
              [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];
              [...]
        }
9. `setTestLogEnabled`하면 tooidentify 문제에 대 한 SDK 로그 수 있도록 하는 선택적 문이입니다.

## <a id="monitor"></a>실시간 모니터링 사용
순서 toostart 데이터를 보내고는 hello 사용자가 활성화 되도록 하나 이상 화면 (활동) toohello Mobile Engagement 백 엔드를 보내야 합니다.

1. 열기 hello **ViewController.h** 파일 및 가져오기 **EngagementViewController.h**:

    `#import "EngagementViewController.h"`
2. 이제 hello의 hello 슈퍼 클래스를 대체 **ViewController** 하 여 인터페이스 `EngagementViewController`:

    `@interface ViewController : EngagementViewController`

## <a id="monitor"></a>실시간 모니터링과 앱 연결
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>푸시 알림 및 앱 내 메시징 사용
Mobile Engagement 사용 하면 사용자와 toointeract 및 도달 범위 푸시 알림과 앱 내 메시징을 캠페인의 hello 컨텍스트에서 사용 합니다. 이 모듈에는 hello Mobile engagement 연결 포털에서 REACH를 라고 합니다.
hello 다음 섹션에서는 앱 tooreceive를 속성을 설정.

### <a name="enable-your-app-tooreceive-silent-push-notifications"></a>사용자 앱 tooreceive 자동 푸시 알림을 사용 하도록 설정
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

### <a name="add-hello-reach-library-tooyour-project"></a>Hello Reach 라이브러리 tooyour 프로젝트 추가
1. 프로젝트를 마우스 오른쪽 단추로 클릭합니다.
2. **파일 추가**를 선택합니다.
3. Hello SDK의 압축을 푼 toohello 폴더를 이동 합니다.
4. 선택 hello `EngagementReach` 폴더입니다.
5. **추가**를 클릭합니다.

### <a name="modify-your-application-delegate"></a>응용 프로그램 대리자 수정
1. 다시 **AppDeletegate.m** 파일, hello Engagement Reach 모듈을 가져옵니다.

        #import "AEReachModule.h"
        #import <UserNotifications/UserNotifications.h>
2. 내부 hello `application:didFinishLaunchingWithOptions` Reach 모듈 만들고 메서드와 tooyour 기존 Engagement 초기화 줄을 전달 합니다.

        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
            AEReachModule * reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
            [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
            [...]
            return YES;
        }

### <a name="enable-your-app-tooreceive-apns-push-notifications"></a>사용자 응용 프로그램 tooreceive APNS 푸시 알림을 사용 하도록 설정
1. 다음 줄 toohello hello 추가 `application:didFinishLaunchingWithOptions` 메서드:

        if (NSFoundationVersionNumber >= NSFoundationVersionNumber_iOS_8_0)
        {
            if (NSFoundationVersionNumber > NSFoundationVersionNumber_iOS_9_x_Max)
            {
                [UNUserNotificationCenter.currentNotificationCenter requestAuthorizationWithOptions:(UNAuthorizationOptionBadge | UNAuthorizationOptionSound | UNAuthorizationOptionAlert) completionHandler:^(BOOL granted, NSError * _Nullable error) {}];
            }else
            {
                [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert)   categories:nil]];
            }
            [application registerForRemoteNotifications];
        }
        else
        {
            [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
        }
2. Hello 추가 `application:didRegisterForRemoteNotificationsWithDeviceToken` 메서드를 다음과 같이 합니다.

        - (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
        {
             [[EngagementAgent shared] registerDeviceToken:deviceToken];
            NSLog(@"Registered Token: %@", deviceToken);
        }
3. Hello 추가 `didFailToRegisterForRemoteNotificationsWithError` 메서드를 다음과 같이 합니다.

        - (void)application:(UIApplication*)application didFailToRegisterForRemoteNotificationsWithError:(NSError*)error
        {
           NSLog(@"Failed tooget token, error: %@", error);
        }
4. Hello 추가 `didReceiveRemoteNotification:fetchCompletionHandler` 메서드를 다음과 같이 합니다.

        - (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
        {
            [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:handler];
        }

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- URLs. -->
[Mobile Engagement iOS SDK]: http://aka.ms/qk2rnj

<!-- Images. -->
[1]: ./media/mobile-engagement-ios-get-started/xcode-add-files.png
[2]: ./media/mobile-engagement-ios-get-started/xcode-select-engagement-sdk.png
[3]: ./media/mobile-engagement-ios-get-started/xcode-build-phases.png
[4]: ./media/mobile-engagement-ios-get-started/app-connection-info-page.png

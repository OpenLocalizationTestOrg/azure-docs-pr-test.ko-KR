---
title: "Mobile Engagement iOS SDK 업그레이드 절차 aaaAzure | Microsoft Docs"
description: "Azure Mobile Engagement용 iOS SDK의 최신 업데이트 및 절차"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 72a9e493-3f14-4e52-b6e2-0490fd04b184
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 12/13/2016
ms.author: piyushjo
ms.openlocfilehash: 5a81bcaaec72aec665b3334e6400d520454d56a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-procedures"></a>업그레이드 절차
통합 한 경우 이미 이전 버전의 서비스 응용 프로그램으로, tooconsider hello hello SDK로 업그레이드 하는 경우 지점 뒤에 있어야 합니다.

각 새 버전의 SDK hello에 대 한 대체 먼저 해야 (제거 하 고 다시 xcode에서 가져올) hello EngagementSDK 및 EngagementReach 폴더입니다.

## <a name="from-300-too400"></a>3.0.0에서 too4.0.0
### <a name="xcode-8"></a>XCode 8
XCode 8은의 hello SDK의 버전 4.0.0부터 반드시 필요 합니다.

> [!NOTE]
> XCode 7에 실제로 종속 경우 hello를 사용할 수 있습니다 [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh)합니다. 10 iOS 장치에서 실행 하는 동안이 이전 버전의 hello 모듈이에 알려진된 버그가 있습니다: 시스템 알림을 작업이 수행 되지 않습니다. toofix tooimplement hello 나면 사용 되지 않는 API `application:didReceiveRemoteNotification:` 응용 프로그램에서 위임 다음과 같습니다.
> 
> 

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> 이 iOS API는 더 이상 사용되지 않으므로 예정된(부분적인) iOS 버전 업그레이드에서는 이 동작이 달라질 수 있습니다. 따라서 **이 해결 방법은 권장되지 않습니다**. 8 tooXCode를 가능한 한 빨리 전환 해야 합니다.
> 
> 

### <a name="usernotifications-framework"></a>UserNotifications 프레임워크
Tooadd hello 필요한 `UserNotifications` 프레임 워크 빌드 단계로 진행에서 합니다.

hello 프로젝트 탐색기에서 프로젝트 창 열고 hello 올바른 대상을 선택 합니다. 그런 다음 hello를 열고 **"빌드 단계"** 탭 및 hello **"링크 이진 파일과 라이브러리"** 메뉴에서 프레임 워크를 추가 `UserNotifications.framework` -으로 hello 링크 설정`Optional`

### <a name="application-push-capability"></a>응용 프로그램 푸시 기능
XCode 8 응용 프로그램을 다시 설정할 수 있습니다 기능 밀어넣기, 다시 확인 하세요 hello에 `capability` 선택한 대상의 탭 합니다.

### <a name="add-hello-new-ios-10-notification-registration-code"></a>Hello 새 iOS 10 알림 등록 코드 추가
iOS 10에서 실행 하는 동안 되지 않는 Api hello 이전 코드 조각 tooregister hello 앱 toonotifications 계속 작동 하지만 암호화를 사용 합니다.

가져오기 hello `User Notification` 프레임 워크:

        #import <UserNotifications/UserNotifications.h> 

응용 프로그램에서 대리자 `application:didFinishLaunchingWithOptions` 메서드 바꾸기:

    if ([application respondsToSelector:@selector(registerUserNotificationSettings:)]) {
        [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert) categories:nil]];
        [application registerForRemoteNotifications];
    }
    else {

        [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
    }

다음으로 바꾸기:

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

### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a>UNUserNotificationCenter 대리자 충돌 해결

*응용 프로그램이나 타사 라이브러리 중 하나에서 `UNUserNotificationCenterDelegate`를 구현하지 않으면 이 부분을 건너뛸 수 있습니다.*

A `UNUserNotificationCenter` 10 이상인 iOS에서 실행 중인 장치에서 Engagement 알림의 hello SDK toomonitor hello 수명 주기를 통해 대리자를 사용 합니다. hello SDK가 자체적으로 구현의 hello `UNUserNotificationCenterDelegate` 프로토콜 있지만 하나만 있을 수 있습니다 `UNUserNotificationCenter` 응용 프로그램당 위임 합니다. 대리자 추가 toohello `UNUserNotificationCenter` hello 하나 Engagement 충돌 하는 개체입니다. Hello SDK 구현 toogive 자체는 사용 되지 것입니다 다음 나에 다른 공급 업체의 대리자를 감지 하면 기회 tooresolve hello 충돌 합니다. Tooadd hello Engagement 논리 tooyour tooresolve hello 충돌 순서로 대리자를 소유 해야 합니다.

있는 경우 두 가지 방법으로 tooachieve이

제안 1, 대리자를 전달 하 여 toohello SDK를 호출 합니다.

    #import <UIKit/UIKit.h>
    #import "EngagementAgent.h"
    #import <UserNotifications/UserNotifications.h>


    @interface MyAppDelegate : NSObject <UIApplicationDelegate, UNUserNotificationCenterDelegate>
    @end

    @implementation MyAppDelegate

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center willPresentNotification:(UNNotification *)notification withCompletionHandler:(void (^)(UNNotificationPresentationOptions options))completionHandler
    {
      // Your own logic.

      [[EngagementAgent shared] userNotificationCenterWillPresentNotification:notification withCompletionHandler:completionHandler]
    }

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center didReceiveNotificationResponse:(UNNotificationResponse *)response withCompletionHandler:(void(^)())completionHandler
    {
      // Your own logic.

      [[EngagementAgent shared] userNotificationCenterDidReceiveNotificationResponse:response withCompletionHandler:completionHandler]
    }
    @end

또는 hello에서 상속 하 여 2, 제안 `AEUserNotificationHandler` 클래스

    #import "AEUserNotificationHandler.h"
    #import "EngagementAgent.h"

    @interface CustomUserNotificationHandler :AEUserNotificationHandler
    @end

    @implementation CustomUserNotificationHandler

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center willPresentNotification:(UNNotification *)notification withCompletionHandler:(void (^)(UNNotificationPresentationOptions options))completionHandler
    {
      // Your own logic.

      [super userNotificationCenter:center willPresentNotification:notification withCompletionHandler:completionHandler];
    }

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center didReceiveNotificationResponse: UNNotificationResponse *)response withCompletionHandler:(void(^)())completionHandler
    {
      // Your own logic.

      [super userNotificationCenter:center didReceiveNotificationResponse:response withCompletionHandler:completionHandler];
    }

    @end

> [!NOTE]
> 알림을 Engagement 또는 전달 하 여 하지 제공 하는지 여부를 확인할 수 있습니다는 `userInfo` 사전 toohello 에이전트 `isEngagementPushPayload:` 클래스 메서드.

해당 hello 있는지 확인 `UNUserNotificationCenter` 개체의 대리자 중 하나가 hello 내에서 tooyour 대리자 설정 되어 `application:willFinishLaunchingWithOptions:` 또는 hello `application:didFinishLaunchingWithOptions:` 응용 프로그램 대리자의 메서드.
예를 들어, 제안 1 위에 hello를 구현 하는 경우:

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code
  
        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }

## <a name="from-200-too300"></a>2.0.0에서 too3.0.0
iOS 4.X에 대한 지원을 삭제했습니다. 적어도 있어야 응용 프로그램의이 버전 hello 배포 대상에서 시작 iOS 6입니다.

추가 해야 하는 경우 범위를 사용 하는 응용 프로그램에서 `remote-notification` 값 toohello `UIBackgroundModes` 순서 tooreceive 원격 알림에 Info.plist 파일의 배열입니다.

메서드를 hello `application:didReceiveRemoteNotification:` toobe로 대체 해야 `application:didReceiveRemoteNotification:fetchCompletionHandler:` 응용 프로그램 대리자에서입니다.

"AEPushDelegate.h"는 사용 되지 않습니다. 인터페이스 할 tooremove 모든 참조 합니다. 여기에 제거 `[[EngagementAgent shared] setPushDelegate:self]` 및 응용 프로그램 대리자에서 메서드를 위임할 hello:

    -(void)willRetrieveLaunchMessage;
    -(void)didFailToRetrieveLaunchMessage;
    -(void)didReceiveLaunchMessage:(AEPushMessage*)launchMessage;

## <a name="from-1160-too200"></a>1.16.0에서 too2.0.0
hello 다음 설명 방법을 toomigrate SDK 통합 hello Capptain 서비스에서에서 제공한 Capptain SAS Azure Mobile Engagement에서 제공 하는 응용 프로그램에 합니다.
이전 버전에서 마이그레이션하려는 경우 먼저 hello Capptain 웹 사이트 toomigrate too1.16 참조 다음 절차를 수행 하는 hello를 적용 하십시오.

> [!IMPORTANT]
> Capptain 및 Mobile Engagement는 동일한 서비스 하지 hello 및 아래에 주어진 hello 프로시저 어떻게 toomigrate hello 클라이언트 응용 프로그램을 강조 표시 합니다. Hello 앱에 마이그레이션 hello SDK hello Capptain 서버 toohello Mobile Engagement 서버에서 데이터를 마이그레이션하지 않습니다.
> 
> 

### <a name="agent"></a>에이전트
메서드를 hello `registerApp:` hello 새 메서드로 바뀌었습니다 `init:`합니다. 그에 따라 응용 프로그램 대리자를 업데이트하고 다음과 같이 연결 문자열을 사용해야 합니다.

            - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
            {
              [...]
              [EngagementAgent init:@"YOUR_CONNECTION_STRING"];
              [...]
            }

SmartAd 추적 하기만 하면 tooremove 함수의 모든 인스턴스의 SDK에서 제거 되었습니다 `AETrackModule` 클래스

### <a name="class-name-changes"></a>클래스 이름 변경
Hello 방법의 일환으로, toobe 변경 해야 하는 클래스/파일 이름의 몇 가지 있습니다.

"CP" 접두사가 붙은 모든 클래스의 이름이 "AE"로 바뀌었습니다.

예제:

* `CPModule.h`이름이 너무`AEModule.h`합니다.

"Capptain" 접두사가 붙은 모든 클래스의 이름이 "Engagement"로 바뀌었습니다.

예제:

* 클래스를 hello `CapptainAgent` 너무 이름이`EngagementAgent`합니다.
* 클래스를 hello `CapptainTableViewController` 너무 이름이`EngagementTableViewController`합니다.
* 클래스를 hello `CapptainUtils` 너무 이름이`EngagementUtils`합니다.
* 클래스를 hello `CapptainViewController` 너무 이름이`EngagementViewController`합니다.


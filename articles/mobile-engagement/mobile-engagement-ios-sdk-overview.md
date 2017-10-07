---
title: "Mobile Engagement SDK 개요 iOS aaaAzure | Microsoft Docs"
description: "Azure Mobile Engagement용 iOS SDK의 최신 업데이트 및 절차"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 3a03bbd6-bcf8-436c-9775-5a8188629252
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: 38f0da2f84df9c62f8fbca233bfda8b9936fdc0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="ios-sdk-for-azure-mobile-engagement"></a>Azure Mobile Engagement용 iOS SDK
여기에서 시작 tooget hello에 대 한 세부 정보를 모두 방법에는 iOS 앱에에서 Azure Mobile Engagement toointegrate 합니다. Toogive 원하는 경우 try 했는지 먼저 확인 해야 하는 것을 수행한 우리의 [15 분 자습서](mobile-engagement-ios-get-started.md)합니다.

Toosee hello 클릭 [SDK 콘텐츠](mobile-engagement-ios-sdk-content.md)

## <a name="integration-procedures"></a>통합 절차
1. 여기에서 시작: [어떻게 toointegrate Mobile Engagement에서 iOS 앱](mobile-engagement-ios-integrate-engagement.md)
2. 알림: [어떻게 iOS 앱에 toointegrate Reach (알림)](mobile-engagement-ios-integrate-engagement-reach.md)
3. 계획 구현 태그: [어떻게 toouse hello 고급 Mobile Engagement API iOS 앱에 태그 지정](mobile-engagement-ios-use-engagement-api.md)

## <a name="release-notes"></a>릴리스 정보
### <a name="410-07172017"></a>4.1.0 (07/17/2017)
* 백그라운드에서 지워진 배지를 수정했습니다.
* 기본 큐에서 호출되지 않는 API에 대한 XCode 9의 경고를 수정했습니다.
* 도달률 설문에서 메모리 누수를 해결했습니다.
* iOS 6.X에 대한 지원을 삭제했습니다. 적어도 있어야 응용 프로그램의이 버전 hello 배포 대상에서 시작 iOS 7입니다.

이전 버전에 대 한 hello를 참조 하십시오 [릴리스 정보를 완료 합니다.](mobile-engagement-ios-release-notes.md)

## <a name="upgrade-procedures"></a>업그레이드 절차
통합 한 경우 이미 이전 버전의 서비스 응용 프로그램으로, tooconsider hello hello SDK로 업그레이드 하는 경우 지점 뒤에 있어야 합니다.

할 수 있습니다 toofollow 몇 가지 절차 여러 버전의 hello SDK 참조를 누락 하는 경우 전체 hello [업그레이드 절차](mobile-engagement-ios-upgrade-procedure.md)합니다.

각 새 버전의 SDK hello에 대 한 대체 먼저 해야 (제거 하 고 다시 xcode에서 가져올) hello EngagementSDK 및 EngagementReach 폴더입니다.

### <a name="from-300-too400"></a>3.0.0에서 too4.0.0
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

#### <a name="usernotifications-framework"></a>UserNotifications 프레임워크
Tooadd hello 필요한 `UserNotifications` 프레임 워크 빌드 단계로 진행에서 합니다.

hello 프로젝트 탐색기에서 프로젝트 창 열고 hello 올바른 대상을 선택 합니다. 그런 다음 hello를 열고 **"빌드 단계"** 탭 및 hello **"링크 이진 파일과 라이브러리"** 메뉴에서 프레임 워크를 추가 `UserNotifications.framework` -으로 hello 링크 설정`Optional`

#### <a name="application-push-capability"></a>응용 프로그램 푸시 기능
XCode 8 응용 프로그램을 다시 설정할 수 있습니다 기능 밀어넣기, 다시 확인 하세요 hello에 `capability` 선택한 대상의 탭 합니다.

#### <a name="add-hello-new-ios-10-notification-registration-code"></a>Hello 새 iOS 10 알림 등록 코드 추가
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

#### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a>UNUserNotificationCenter 대리자 충돌 해결

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

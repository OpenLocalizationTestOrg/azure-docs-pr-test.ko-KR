---
title: "Mobile Engagement iOS SDK 도달 통합 aaaAzure | Microsoft Docs"
description: "Azure Mobile Engagement용 iOS SDK의 최신 업데이트 및 절차"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 1f5f5857-867c-40c5-9d76-675a343a0296
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 12/13/2016
ms.author: piyushjo
ms.openlocfilehash: 40c9bfbdb475ab0b97bdbc9cea798a59cb8a71ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-engagement-reach-on-ios"></a>TooIntegrate Engagement iOS에 도달 하는 방법
Hello에 설명 된 hello 통합 절차를 따라야 [어떻게 iOS 문서에 Engagement tooIntegrate](mobile-engagement-ios-integrate-engagement.md) 이 가이드를 수행 하기 전에.

이 설명서에는 XCode 8이 필요합니다. XCode 7에 실제로 종속 경우 hello를 사용할 수 있습니다 [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh)합니다. iOS 10 장치에서 실행하는 경우 이 이전 버전에는 알려진 버그가 있습니다. 시스템 알림은 작동하지 않습니다. toofix tooimplement hello 나면 사용 되지 않는 API `application:didReceiveRemoteNotification:` 응용 프로그램에서 위임 다음과 같습니다.

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> 이 iOS API는 더 이상 사용되지 않으므로 예정된(부분적인) iOS 버전 업그레이드에서는 이 동작이 달라질 수 있습니다. 따라서 **이 해결 방법은 권장되지 않습니다**. 8 tooXCode를 가능한 한 빨리 전환 해야 합니다.
>
>

### <a name="enable-your-app-tooreceive-silent-push-notifications"></a>사용자 앱 tooreceive 자동 푸시 알림을 사용 하도록 설정
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

## <a name="integration-steps"></a>통합 단계
### <a name="embed-hello-engagement-reach-sdk-into-your-ios-project"></a>IOS 프로젝트에 hello Engagement Reach SDK 포함
* Xcode 프로젝트에서 hello Reach sdk를 추가 합니다. Xcode에서 이동 너무**프로젝트 \> tooproject 추가** hello 선택 `EngagementReach` 폴더입니다.

### <a name="modify-your-application-delegate"></a>응용 프로그램 대리자 수정
* 구현 파일의 hello 위쪽 hello Engagement Reach 모듈을 가져옵니다.

      [...]
      #import "AEReachModule.h"
* 메서드 안에서 `applicationDidFinishLaunching:` 또는 `application:didFinishLaunchingWithOptions:`reach 모듈 만들고 tooyour 기존 Engagement 초기화 줄 전달 합니다.

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
        [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
        [...]

        return YES;
      }
* 수정 **'icon.png'** 프로그램 알림 아이콘으로 사용할 hello 이미지 이름을 포함 하는 문자열입니다.
* Toouse hello 옵션을 원하는 경우 *업데이트 배지 값* Reach 캠페인 또는 toouse 네이티브 푸시 하려는 경우 \<SaaS/Reach API/캠페인 형식/네이티브 푸시\> 캠페인을 알려야 hello Reach 모듈 관리 hello 배지 아이콘이 자체 (hello 응용 프로그램 배지를 자동으로 제거 하 고도 hello 응용 프로그램을 시작 또는 foregrounded 때마다 Engagement에서 저장 된 hello 값 다시 설정). 이 작업은 hello Reach 모듈을 초기화 한 후 다음 줄을 추가 하 여 수행 됩니다.

      [reach setAutoBadgeEnabled:YES];
* Toohello 준수 응용 프로그램 대리인에 게 알려야 toohandle Reach 데이터 푸시 하려는 경우 `AEReachDataPushDelegate` 프로토콜입니다. Hello Reach 모듈을 초기화 한 후 다음 줄을 추가 합니다.

      [reach setDataPushDelegate:self];
* Hello 메서드를 구현할 수 있는 다음 `onDataPushStringReceived:` 및 `onDataPushBase64ReceivedWithDecodedBody:andEncodedBody:` 응용 프로그램 대리자에서:

      -(BOOL)didReceiveStringDataPushWithCategory:(NSString*)category body:(NSString*)body
      {
         NSLog(@"String data push message with category <%@> received: %@", category, body);
         return YES;
      }

      -(BOOL)didReceiveBase64DataPushWithCategory:(NSString*)category decodedBody:(NSData *)decodedBody encodedBody:(NSString *)encodedBody
      {
         NSLog(@"Base64 data push message with category <%@> received: %@", category, encodedBody);
         // Do something useful with decodedBody like updating an image view
         return YES;
      }

### <a name="category"></a>Category
hello 범주 매개 변수의 선택적 데이터 푸시 캠페인을 만들 때 이며 허용 하면 toofilter 데이터 푸시 합니다. Toopush 다양 한 종류를 원하는 경우에 유용의 `Base64` 데이터 및 원하는 tooidentify을 구문 분석 하기 전에 해당 형식입니다.

**응용 프로그램 준비 tooreceive 및 표시 내용에 도달 하는 이제는!**

## <a name="how-tooreceive-announcements-and-polls-at-any-time"></a>어떻게 tooreceive 공지 및 설문 조사의 언제 든 지
Engagement 알림을 보낼 수 Reach tooyour 최종 사용자가 언제 든 지 hello Apple 푸시 알림 서비스를 사용 하 여 합니다.

tooenable이이 기능을가 tooprepare Apple 푸시 알림에 대 한 응용 프로그램 및 응용 프로그램 대리자를 수정 합니다.

### <a name="prepare-your-application-for-apple-push-notifications"></a>Apple 푸시 알림을 받도록 응용 프로그램 준비
Hello 가이드를 따르세요: [어떻게 tooPrepare Apple 푸시 알림에 대 한 응용 프로그램](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)

### <a name="add-hello-necessary-client-code"></a>Hello 필요한 클라이언트 코드를 추가 합니다.
*이 시점에서 응용 프로그램 hello Engagement 프런트 엔드에 등록 된 Apple 푸시 인증서가 있어야 합니다.*

아직 수행 하지는 경우 tooregister 프로그램 응용 프로그램 tooreceive 푸시 알림이 필요한 합니다.

* 가져오기 hello `User Notification` 프레임 워크:

        #import <UserNotifications/UserNotifications.h>
* Hello 응용 프로그램을 시작 하는 경우 다음 줄을 추가 (보통 `application:didFinishLaunchingWithOptions:`):

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

그런 다음 tooprovide tooEngagement hello 장치 토큰 Apple 서버에서 반환 해야 합니다. 라는 hello 메서드 이렇게 `application:didRegisterForRemoteNotificationsWithDeviceToken:` 응용 프로그램 대리자에서:

    - (void)application:(UIApplication*)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData*)deviceToken
    {
        [[EngagementAgent shared] registerDeviceToken:deviceToken];
    }

마지막으로, 응용 프로그램에서 원격 알림을 받으면 tooinform hello Engagement SDK 한 됩니다. 호출 하는 toodo hello 메서드 `applicationDidReceiveRemoteNotification:fetchCompletionHandler:` 응용 프로그램 대리자에서:

    - (void)application:(UIApplication*)application didReceiveRemoteNotification:(NSDictionary*)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:handler];
    }

> [!IMPORTANT]
> 기본적으로 Engagement Reach hello completionHandler을 제어합니다. Toomanually 응답 toohello 하려는 경우 `handler` 코드에서 블록을 hello에 대 한 nil를 전달할 수 있습니다 `handler` 인수 및 제어 hello 완료 자신을 차단 합니다. Hello 참조 `UIBackgroundFetchResult` 목록에 대 한 가능한 값의 형식입니다.
>
>

### <a name="full-example"></a>전체 예제
통합의 전체 예제는 다음과 같습니다.

    #pragma mark -
    #pragma mark Application lifecycle

    - (BOOL)application:(UIApplication*)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions
    {
      /* Reach module */
      AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
      [reach setAutoBadgeEnabled:YES];

      /* Engagement initialization */
      [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
      [[EngagementAgent shared] setPushDelegate:self];

      /* Views */
      [window addSubview:[tabBarController view]];
      [window makeKeyAndVisible];

      [application registerForRemoteNotificationTypes:UIRemoteNotificationTypeAlert|UIRemoteNotificationTypeBadge|UIRemoteNotificationTypeSound];
      return YES;
    }

    - (void)application:(UIApplication*)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData*)deviceToken
    {
      [[EngagementAgent shared] registerDeviceToken:deviceToken];
    }

    - (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:handler];
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

## <a name="how-toocustomize-campaigns"></a>어떻게 toocustomize 캠페인
### <a name="notifications"></a>알림
알림에는 시스템 알림과 앱 내 알림의 두 가지 유형이 있습니다.

시스템 알림은 iOS에서 처리되며 사용자 지정은 가능하지 않습니다.

앱에서 알림은 현재 응용 프로그램 창 toohello 동적으로 추가 되는 보기는 구성 됩니다. 이 보기를 알림 오버레이라고 합니다. 알림 오버레이은 필요 하지 않으므로 toomodify 하면 응용 프로그램의 보기 중 하나에 빠른 통합에 매우 유용 합니다.

#### <a name="layout"></a>레이아웃
앱에서 알림 toomodify hello 모양을 수정할 수 hello 파일 `AENotificationView.xib` hello 태그 값 및 hello 기존 하위 유형의 유지으로 tooyour 필요 합니다.

기본적으로 앱에서 알림은 hello hello 화면 맨 아래에 표시 됩니다. 화면에서 편집 hello의 hello 위쪽에 제공 된 toodisplay 선호 하는 경우 `AENotificationView.xib` hello 변경 `AutoSizing` hello 해당 슈퍼 뷰의 위쪽에 보관할 수 있도록 hello 주 보기의 속성입니다.

#### <a name="categories"></a>범주
레이아웃을 제공 하는 hello를 수정 하는 경우 모든 알림 hello 모양을 수정 합니다. 범주를 사용 toodefine 대상 다양 한 알림 (가능 동작)을 찾습니다. 도달률 캠페인을 만들 때 범주를 지정할 수 있습니다. 범주를 사용하면 알림과 설문 조사도 사용자 지정할 수 있습니다. 여기에 대해서는 이 문서의 뒷부분에서 설명합니다.

알림에 대 한 범주 처리기 tooregister tooadd hello 도달 모듈 호출 초기화 해야 합니다.

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerNotifier:myNotifier forCategory:@"my_category"];
    ...

`myNotifier`toohello 프로토콜을 준수 하는 개체의 인스턴스여야 합니다 `AENotifier`합니다.

혼자서 hello 프로토콜 메서드를 구현할 수 또는 tooreimplement hello 기존 클래스를 선택할 수 있습니다 `AEDefaultNotifier` hello 작업의 대부분을 이미 수행 하는 합니다.

예를 들어 특정 범주에 대 한 tooredefine hello 알림 보기를 하려는 경우이 예제를 따를 수 있습니다.

    #import "AEDefaultNotifier.h"
    #import "AENotificationView.h"
    @interface MyNotifier : AEDefaultNotifier
    @end

    @implementation MyNotifier

    -(NSString*)nibNameForCategory:(NSString*)category
    {
      return "MyNotificationView";
    }

    @end

이 간단한 범주 예제에서는 `MyNotificationView.xib` 파일이 주 응용 프로그램 번들에 포함되어 있다고 가정합니다. Hello 메서드가 해당 수 toofind 없으면 `.xib`, hello 알림이 표시 되지 것입니다 및 Engagement hello 콘솔에서 메시지를 출력 합니다.

제공 된 hello nib 파일 hello 규칙에 따라 허용 해야 합니다.

* 파일에는 뷰가 하나만 포함되어야 합니다.
* 하위 hello 라는 제공 hello nib 파일 내 스토리 hello 동일한 형식을 이어야 합니다.`AENotificationView.xib`
* 하위 hello 라는 제공 hello nib 파일 내 스토리 hello으로 태그를 삽입 동일 해야 합니다.`AENotificationView.xib`

> [!TIP]
> 라는 제공 hello nib 파일 복사 `AENotificationView.xib`, 여기에서 작업을 시작 합니다. 주의 해야 하지만,이 nib 파일은 내부 연결 toohello 클래스 뷰의 hello `AENotificationView`합니다. 이 클래스는 hello 메서드를 재정의 `layoutSubViews` toomove toocontext에 따라 해당 하위 크기를 조정 합니다. Tooreplace 경우가 사용 하 여는 `UIView` 또는 사용자 지정 보기 클래스.
>
>

소스 코드와 클래스 문서를 제공 하는 hello 살펴보면 tootake 좋습니다 (원할 경우 예를 들어 tooload hello 코드에서 직접 보기) 알림 깊은 사용자 지정 해야 할 경우 `Protocol ReferencesDefaultNotifier` 및 `AENotifier`합니다.

참고 사용할 수 있는 여러 범주에 대 한 동일한 알림이 hello 합니다.

다음과 같은 기본 알림도 다시 정의 된 hello 수행할 수 있습니다.

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerNotifier:myNotifier forCategory:kAEReachDefaultCategory];

##### <a name="notification-handling"></a>알림 처리
Hello에서 일부 수명 주기 메서드를 호출 hello 기본 범주를 사용할 경우 `AEReachContent` tooreport 통계 및 업데이트 hello 캠페인 상태 개체:

* Hello 알림이 응용 프로그램에 표시 되 면 hello `displayNotification` (보고 하는 통계) 메서드를 호출 하 여 `AEReachModule` 경우 `handleNotification:` 반환 `YES`합니다.
* Hello 알림은 해제 하는 경우 hello `exitNotification` 메서드는 통계는 보고 되며 다음 캠페인을 지금 처리할 수 있습니다.
* Hello 알림의 클릭할 경우 `actionNotification` 은 호출 통계는 보고 되며 hello 연결 된 작업을 수행 합니다.

경우 구현 `AENotifier` 바이패스 hello 기본 동작, 혼자서 toocall 이러한 수명 주기 메서드를가지고 있어야 합니다. 다음 예제는 hello hello 기본 동작이 사용 하지 않을 경우를 보여 줍니다.

* 범주 처리를 처음부터 구현한 경우처럼 `AEDefaultNotifier`을(를) 확장하지 않은 경우
* 사용자가 `prepareNotificationView:forContent:`있는지 toomap 사이, `onNotificationActioned` 또는 `onNotificationExited` tooone U.I 컨트롤의 합니다.

> [!WARNING]
> 경우 `handleNotification:` hello 콘텐츠 예외가 throw는 삭제 및 `drop` 가 통계를 보고 하 고 호출 다음 캠페인을 지금 처리할 수 있습니다.
>
>

#### <a name="include-notification-as-part-of-an-existing-view"></a>기존 뷰의 일부로 알림 포함
오버레이는 통합을 빠르게 수행하는 데 유용하지만 사용이 불편하거나 원치 않는 부작용을 야기하는 경우도 있습니다.

본인이 hello 오버레이 시스템 중 일부 보기의 내용과 이러한 보기에 대 한 사용자 지정할 수 있습니다.

기존 보기에 tooinclude 우리의 알림 레이아웃을 결정할 수 있습니다. toodo 따라서는 두 가지 구현 스타일:

1. 인터페이스 작성기를 사용 하 여 hello 알림 보기를 추가 합니다.

   * *인터페이스 작성기*
   * 320 x 60 (또는 768 x 60 iPad에 있는 경우)를 배치 `UIView` hello 알림 tooappear 저장할
   * 이 보기에 대 한 hello 태그 값을 너무 설정: **36822491**
2. 프로그래밍 방식으로 hello 알림 보기를 추가 합니다. 뷰 초기화 되었을 때 코드를 다음 hello 추가:

       UIView* notificationView = [[UIView alloc] initWithFrame:CGRectMake(0, 0, 320, 60)]; //Replace x and y coordinate values tooyour needs.
       notificationView.tag = NOTIFICATION_AREA_VIEW_TAG;
       [self.view addSubview:notificationView];

`NOTIFICATION_AREA_VIEW_TAG` 매크로는 `AEDefaultNotifier.h`에 있습니다.

> [!NOTE]
> hello 기본 알림이 해당 hello 알림 레이아웃이이 보기에 포함 되 고 오버레이 대 한 추가 하지 않는 것에 자동으로 검색 합니다.
>
>

### <a name="announcements-and-polls"></a>알림 및 설문 조사
#### <a name="layouts"></a>레이아웃
Hello 파일을 수정할 수 `AEDefaultAnnouncementView.xib` 및 `AEDefaultPollView.xib` 으로 hello 태그 값 및 hello 기존 하위 유형의 유지 합니다.

#### <a name="categories"></a>범주
##### <a name="alternate-layouts"></a>대체 레이아웃
알림, 같이 hello 캠페인의 범주는 공지 및 설문 조사의 toohave 사용 되는 대체 레이아웃 일 수 있습니다.

확장 해야 공지에 대 한 범주 toocreate **AEAnnouncementViewController** hello 모듈이 초기화 되 면 등록:

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerAnnouncementController:[MyCustomAnnouncementViewController class] forCategory:@"my_category"];

> [!NOTE]
> 사용자는 hello 범주를 사용 하 여 알림에 대 한 알림을 클릭 될 때마다 "내\_범주", 등록 된 보기 컨트롤러 (이 경우 `MyCustomAnnouncementViewController`) hello 메서드를 호출 하 여 초기화 될 `initWithAnnouncement:` 및 hello 보기가 포함 됩니다 추가 된 toohello 현재 응용 프로그램 창입니다.
>
>

Hello 구현에서 `AEAnnouncementViewController` tooread hello 속성은 클래스 `announcement` tooinitialize 사용자 하위 뷰가 있습니다. 다음 hello 예제에서는 두는 것이 좋습니다 레이블을 사용 하 여 초기화 된 `title` 및 `body` hello의 속성 `AEReachAnnouncement` 클래스:

    -(void)loadView
    {
        [super loadView];

        UILabel* titleLabel = [[UILabel alloc] initWithFrame:CGRectMake(10, 20, 300, 60)];
        titleLabel.font = [UIFont systemFontOfSize:32.0];
        titleLabel.text = self.announcement.title;

        UILabel* bodyLabel = [[UILabel alloc] initWithFrame:CGRectMake(10, 20, 300, 60)];
        bodyLabel.font = [UIFont systemFontOfSize:24.0];
        bodyLabel.text = self.announcement.body;

        [self.view addSubview:titleLabel];
        [self.view addSubview:bodyLabel];
    }

클래스를 제공 하는 hello 확장 않으려는 tooload 보기 혼자서 하지만 tooreuse hello 기본 알림 보기 레이아웃 선택 하면, 사용자 지정 보기 컨트롤러 만들 수 있습니다 하는지 `AEDefaultAnnouncementViewController`합니다. 이 경우 중복 된 hello nib 파일이 `AEDefaultAnnouncementView.xib` 사용자 지정 보기 컨트롤러에서 로드할 수 있도록로 이름을 바꿉니다 (명명 된 컨트롤러에 대 한 `CustomAnnouncementViewController`, nib 파일을 호출 해야 `CustomAnnouncementView.xib`).

공지의 tooreplace hello 기본 범주에 정의 된 hello 범주에 대 한 사용자 지정 보기 컨트롤러를 등록 하기만 하면 `kAEReachDefaultCategory`:

    [reach registerAnnouncementController:[MyCustomAnnouncementViewController class] forCategory:kAEReachDefaultCategory];

설문에 사용자 지정 된 hello 수 같은 방식으로:

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerPollController:[MyCustomPollViewController class] forCategory:@"my_category"];

이 시간을 제공 하는 hello `MyCustomPollViewController` 확장 해야 `AEPollViewController`합니다. Hello 기본 컨트롤러에서 tooextend를 선택할 수 있습니다 또는: `AEDefaultPollViewController`합니다.

> [!IMPORTANT]
> 하거나 toocall 반드시 `action` (`submitAnswers:` 컨트롤러 보기 사용자 지정 설문 조사에 대 한) 또는 `exit` 메서드 전에 hello 뷰-컨트롤러 해제 되었습니다. 그렇지 않으면, 통계 전송 되지 않습니다. (예: hello 캠페인에 없는 분석) 하 고 hello 응용 프로그램 프로세스를 다시 시작 될 때까지 더 중요 한 것은 다음 캠페인을 받을 수 없습니다.
>
>

##### <a name="implementation-example"></a>구현 예제
이 구현에서 hello 사용자 지정 알림 뷰는 외부 xib 파일에서 로드 됩니다.

와 같은 고급 알림 사용자 지정을 위한 것이 좋습니다 toolook hello 표준 구현의 hello 소스 코드에서.

`CustomAnnouncementViewController.h`

    //Interface
    @interface CustomAnnouncementViewController : AEAnnouncementViewController {
      UILabel* titleLabel;
      UITextView* descTextView;
      UIWebView* htmlWebView;
      UIButton* okButton;
      UIButton* cancelButton;
    }

    @property (nonatomic, retain) IBOutlet UILabel* titleLabel;
    @property (nonatomic, retain) IBOutlet UITextView* descTextView;
    @property (nonatomic, retain) IBOutlet UIWebView* htmlWebView;
    @property (nonatomic, retain) IBOutlet UIButton* okButton;
    @property (nonatomic, retain) IBOutlet UIButton* cancelButton;

    -(IBAction)okButtonClicked:(id)sender;
    -(IBAction)cancelButtonClicked:(id)sender;

`CustomAnnouncementViewController.m`

    //Implementation
    @implementation CustomAnnouncementViewController
    @synthesize titleLabel;
    @synthesize descTextView;
    @synthesize htmlWebView;
    @synthesize okButton;
    @synthesize cancelButton;

    -(id)initWithAnnouncement:(AEReachAnnouncement*)anAnnouncement
    {
      self = [super initWithNibName:@"CustomAnnouncementViewController" bundle:nil];
      if (self != nil) {
        self.announcement = anAnnouncement;
      }
      return self;
    }

    - (void) dealloc
    {
      [titleLabel release];
      [descTextView release];
      [htmlWebView release];
      [okButton release];
      [cancelButton release];
      [super dealloc];
    }

    - (void)viewDidLoad {
      [super viewDidLoad];

      /* Init announcement title */
      titleLabel.text = self.announcement.title;

      /* Init announcement body */
      if(self.announcement.type == AEAnnouncementTypeHtml)
      {
        titleLabel.hidden = YES;
        htmlWebView.hidden = NO;
        [htmlWebView loadHTMLString:self.announcement.body baseURL:[NSURL URLWithString:@"http://localhost/"]];
      }
      else
      {
        titleLabel.hidden = NO;
        htmlWebView.hidden = YES;
        descTextView.text = self.announcement.body;
      }

      /* Set action button label */
      if([self.announcement.actionLabel length] > 0)
        [okButton setTitle:self.announcement.actionLabel forState:UIControlStateNormal];

      /* Set exit button label */
      if([self.announcement.exitLabel length] > 0)
        [cancelButton setTitle:self.announcement.exitLabel forState:UIControlStateNormal];
    }

    #pragma mark Actions

    -(IBAction)okButtonClicked:(id)sender
    {
        [self action];
    }

    -(IBAction)cancelButtonClicked:(id)sender
    {
        [self exit];
    }

    @end

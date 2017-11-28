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
# <a name="how-toointegrate-engagement-reach-on-ios"></a><span data-ttu-id="568d3-103">TooIntegrate Engagement iOS에 도달 하는 방법</span><span class="sxs-lookup"><span data-stu-id="568d3-103">How tooIntegrate Engagement Reach on iOS</span></span>
<span data-ttu-id="568d3-104">Hello에 설명 된 hello 통합 절차를 따라야 [어떻게 iOS 문서에 Engagement tooIntegrate](mobile-engagement-ios-integrate-engagement.md) 이 가이드를 수행 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="568d3-104">You must follow hello integration procedure described in hello [How tooIntegrate Engagement on iOS document](mobile-engagement-ios-integrate-engagement.md) before following this guide.</span></span>

<span data-ttu-id="568d3-105">이 설명서에는 XCode 8이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-105">This documentation requires XCode 8.</span></span> <span data-ttu-id="568d3-106">XCode 7에 실제로 종속 경우 hello를 사용할 수 있습니다 [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh)합니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-106">If you really depend on XCode 7 then you may use hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="568d3-107">iOS 10 장치에서 실행하는 경우 이 이전 버전에는 알려진 버그가 있습니다. 시스템 알림은 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-107">There is a known bug on this previous version while running on iOS 10 devices:  system notifications are not actioned.</span></span> <span data-ttu-id="568d3-108">toofix tooimplement hello 나면 사용 되지 않는 API `application:didReceiveRemoteNotification:` 응용 프로그램에서 위임 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-108">toofix this you will have tooimplement hello deprecated API `application:didReceiveRemoteNotification:` in your app delegate as follows:</span></span>

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> <span data-ttu-id="568d3-109">이 iOS API는 더 이상 사용되지 않으므로 예정된(부분적인) iOS 버전 업그레이드에서는 이 동작이 달라질 수 있습니다. 따라서 **이 해결 방법은 권장되지 않습니다**.</span><span class="sxs-lookup"><span data-stu-id="568d3-109">**We do not recommend this workaround** as this behavior can change in any upcoming (even minor) iOS version upgrade because this iOS API is deprecated.</span></span> <span data-ttu-id="568d3-110">8 tooXCode를 가능한 한 빨리 전환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-110">You should switch tooXCode 8 as soon as possible.</span></span>
>
>

### <a name="enable-your-app-tooreceive-silent-push-notifications"></a><span data-ttu-id="568d3-111">사용자 앱 tooreceive 자동 푸시 알림을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="568d3-111">Enable your app tooreceive Silent Push Notifications</span></span>
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

## <a name="integration-steps"></a><span data-ttu-id="568d3-112">통합 단계</span><span class="sxs-lookup"><span data-stu-id="568d3-112">Integration steps</span></span>
### <a name="embed-hello-engagement-reach-sdk-into-your-ios-project"></a><span data-ttu-id="568d3-113">IOS 프로젝트에 hello Engagement Reach SDK 포함</span><span class="sxs-lookup"><span data-stu-id="568d3-113">Embed hello Engagement Reach SDK into your iOS project</span></span>
* <span data-ttu-id="568d3-114">Xcode 프로젝트에서 hello Reach sdk를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-114">Add hello Reach sdk in your Xcode project.</span></span> <span data-ttu-id="568d3-115">Xcode에서 이동 너무**프로젝트 \> tooproject 추가** hello 선택 `EngagementReach` 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-115">In Xcode, go too**Project \> Add tooproject** and choose hello `EngagementReach` folder.</span></span>

### <a name="modify-your-application-delegate"></a><span data-ttu-id="568d3-116">응용 프로그램 대리자 수정</span><span class="sxs-lookup"><span data-stu-id="568d3-116">Modify your Application Delegate</span></span>
* <span data-ttu-id="568d3-117">구현 파일의 hello 위쪽 hello Engagement Reach 모듈을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-117">At hello top of your implementation file, import hello Engagement Reach module:</span></span>

      [...]
      #import "AEReachModule.h"
* <span data-ttu-id="568d3-118">메서드 안에서 `applicationDidFinishLaunching:` 또는 `application:didFinishLaunchingWithOptions:`reach 모듈 만들고 tooyour 기존 Engagement 초기화 줄 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-118">Inside method `applicationDidFinishLaunching:` or `application:didFinishLaunchingWithOptions:`, create a reach module and pass it tooyour existing Engagement initialization line:</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
        [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
        [...]

        return YES;
      }
* <span data-ttu-id="568d3-119">수정 **'icon.png'** 프로그램 알림 아이콘으로 사용할 hello 이미지 이름을 포함 하는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-119">Modify **'icon.png'** string with hello image name you want as your notification icon.</span></span>
* <span data-ttu-id="568d3-120">Toouse hello 옵션을 원하는 경우 *업데이트 배지 값* Reach 캠페인 또는 toouse 네이티브 푸시 하려는 경우 \<SaaS/Reach API/캠페인 형식/네이티브 푸시\> 캠페인을 알려야 hello Reach 모듈 관리 hello 배지 아이콘이 자체 (hello 응용 프로그램 배지를 자동으로 제거 하 고도 hello 응용 프로그램을 시작 또는 foregrounded 때마다 Engagement에서 저장 된 hello 값 다시 설정).</span><span class="sxs-lookup"><span data-stu-id="568d3-120">If you want toouse hello option *Update badge value* in Reach campaigns or if you want toouse native push \</SaaS/Reach API/Campaign format/Native Push\> campaigns, you must let hello Reach module manage hello badge icon itself (it will automatically clear hello application badge and also reset hello value stored by Engagement every time hello application is started or foregrounded).</span></span> <span data-ttu-id="568d3-121">이 작업은 hello Reach 모듈을 초기화 한 후 다음 줄을 추가 하 여 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-121">This is done by adding hello following line after Reach module initialization:</span></span>

      [reach setAutoBadgeEnabled:YES];
* <span data-ttu-id="568d3-122">Toohello 준수 응용 프로그램 대리인에 게 알려야 toohandle Reach 데이터 푸시 하려는 경우 `AEReachDataPushDelegate` 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-122">If you want toohandle Reach data push, you must let your Application delegate conform toohello `AEReachDataPushDelegate` protocol.</span></span> <span data-ttu-id="568d3-123">Hello Reach 모듈을 초기화 한 후 다음 줄을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-123">Add hello following line after Reach module initialization:</span></span>

      [reach setDataPushDelegate:self];
* <span data-ttu-id="568d3-124">Hello 메서드를 구현할 수 있는 다음 `onDataPushStringReceived:` 및 `onDataPushBase64ReceivedWithDecodedBody:andEncodedBody:` 응용 프로그램 대리자에서:</span><span class="sxs-lookup"><span data-stu-id="568d3-124">Then you can implement hello methods `onDataPushStringReceived:` and `onDataPushBase64ReceivedWithDecodedBody:andEncodedBody:` in your application delegate:</span></span>

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

### <a name="category"></a><span data-ttu-id="568d3-125">Category</span><span class="sxs-lookup"><span data-stu-id="568d3-125">Category</span></span>
<span data-ttu-id="568d3-126">hello 범주 매개 변수의 선택적 데이터 푸시 캠페인을 만들 때 이며 허용 하면 toofilter 데이터 푸시 합니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-126">hello category parameter is optional when you create a Data Push campaign and allows you toofilter data pushes.</span></span> <span data-ttu-id="568d3-127">Toopush 다양 한 종류를 원하는 경우에 유용의 `Base64` 데이터 및 원하는 tooidentify을 구문 분석 하기 전에 해당 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-127">This is useful if you want toopush different kinds of `Base64` data and want tooidentify their type before parsing them.</span></span>

<span data-ttu-id="568d3-128">**응용 프로그램 준비 tooreceive 및 표시 내용에 도달 하는 이제는!**</span><span class="sxs-lookup"><span data-stu-id="568d3-128">**Your application is now ready tooreceive and display reach contents!**</span></span>

## <a name="how-tooreceive-announcements-and-polls-at-any-time"></a><span data-ttu-id="568d3-129">어떻게 tooreceive 공지 및 설문 조사의 언제 든 지</span><span class="sxs-lookup"><span data-stu-id="568d3-129">How tooreceive announcements and polls at any time</span></span>
<span data-ttu-id="568d3-130">Engagement 알림을 보낼 수 Reach tooyour 최종 사용자가 언제 든 지 hello Apple 푸시 알림 서비스를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-130">Engagement can send Reach notifications tooyour end users at any time by using hello Apple Push Notification Service.</span></span>

<span data-ttu-id="568d3-131">tooenable이이 기능을가 tooprepare Apple 푸시 알림에 대 한 응용 프로그램 및 응용 프로그램 대리자를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-131">tooenable this functionality, you'll have tooprepare your application for Apple push notifications and modify your application delegate.</span></span>

### <a name="prepare-your-application-for-apple-push-notifications"></a><span data-ttu-id="568d3-132">Apple 푸시 알림을 받도록 응용 프로그램 준비</span><span class="sxs-lookup"><span data-stu-id="568d3-132">Prepare your application for Apple push notifications</span></span>
<span data-ttu-id="568d3-133">Hello 가이드를 따르세요: [어떻게 tooPrepare Apple 푸시 알림에 대 한 응용 프로그램](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)</span><span class="sxs-lookup"><span data-stu-id="568d3-133">Please follow hello guide : [How tooPrepare your Application for Apple Push Notifications](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)</span></span>

### <a name="add-hello-necessary-client-code"></a><span data-ttu-id="568d3-134">Hello 필요한 클라이언트 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-134">Add hello necessary client code</span></span>
<span data-ttu-id="568d3-135">*이 시점에서 응용 프로그램 hello Engagement 프런트 엔드에 등록 된 Apple 푸시 인증서가 있어야 합니다.*</span><span class="sxs-lookup"><span data-stu-id="568d3-135">*At this point your application should have a registered Apple push certificate in hello Engagement frontend.*</span></span>

<span data-ttu-id="568d3-136">아직 수행 하지는 경우 tooregister 프로그램 응용 프로그램 tooreceive 푸시 알림이 필요한 합니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-136">If it's not done already, you need tooregister your application tooreceive push notifications.</span></span>

* <span data-ttu-id="568d3-137">가져오기 hello `User Notification` 프레임 워크:</span><span class="sxs-lookup"><span data-stu-id="568d3-137">Import hello `User Notification` framework:</span></span>

        #import <UserNotifications/UserNotifications.h>
* <span data-ttu-id="568d3-138">Hello 응용 프로그램을 시작 하는 경우 다음 줄을 추가 (보통 `application:didFinishLaunchingWithOptions:`):</span><span class="sxs-lookup"><span data-stu-id="568d3-138">Add hello following line when your application starts (typically in `application:didFinishLaunchingWithOptions:`):</span></span>

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

<span data-ttu-id="568d3-139">그런 다음 tooprovide tooEngagement hello 장치 토큰 Apple 서버에서 반환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-139">Then, You need tooprovide tooEngagement hello device token returned by Apple servers.</span></span> <span data-ttu-id="568d3-140">라는 hello 메서드 이렇게 `application:didRegisterForRemoteNotificationsWithDeviceToken:` 응용 프로그램 대리자에서:</span><span class="sxs-lookup"><span data-stu-id="568d3-140">This is done in hello method named `application:didRegisterForRemoteNotificationsWithDeviceToken:` in your application delegate:</span></span>

    - (void)application:(UIApplication*)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData*)deviceToken
    {
        [[EngagementAgent shared] registerDeviceToken:deviceToken];
    }

<span data-ttu-id="568d3-141">마지막으로, 응용 프로그램에서 원격 알림을 받으면 tooinform hello Engagement SDK 한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-141">Finally, you have tooinform hello Engagement SDK when your application receives a remote notification.</span></span> <span data-ttu-id="568d3-142">호출 하는 toodo hello 메서드 `applicationDidReceiveRemoteNotification:fetchCompletionHandler:` 응용 프로그램 대리자에서:</span><span class="sxs-lookup"><span data-stu-id="568d3-142">toodo that, call hello method `applicationDidReceiveRemoteNotification:fetchCompletionHandler:` in your application delegate:</span></span>

    - (void)application:(UIApplication*)application didReceiveRemoteNotification:(NSDictionary*)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:handler];
    }

> [!IMPORTANT]
> <span data-ttu-id="568d3-143">기본적으로 Engagement Reach hello completionHandler을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-143">By default, Engagement Reach controls hello completionHandler.</span></span> <span data-ttu-id="568d3-144">Toomanually 응답 toohello 하려는 경우 `handler` 코드에서 블록을 hello에 대 한 nil를 전달할 수 있습니다 `handler` 인수 및 제어 hello 완료 자신을 차단 합니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-144">If you want toomanually respond toohello `handler` block in your code, you can pass nil for hello `handler` argument and control hello completion block yourself.</span></span> <span data-ttu-id="568d3-145">Hello 참조 `UIBackgroundFetchResult` 목록에 대 한 가능한 값의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-145">See hello `UIBackgroundFetchResult` type for a list of possible values.</span></span>
>
>

### <a name="full-example"></a><span data-ttu-id="568d3-146">전체 예제</span><span class="sxs-lookup"><span data-stu-id="568d3-146">Full example</span></span>
<span data-ttu-id="568d3-147">통합의 전체 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-147">Here is a full example of integration:</span></span>

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

### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a><span data-ttu-id="568d3-148">UNUserNotificationCenter 대리자 충돌 해결</span><span class="sxs-lookup"><span data-stu-id="568d3-148">Resolve UNUserNotificationCenter delegate conflicts</span></span>

<span data-ttu-id="568d3-149">*응용 프로그램이나 타사 라이브러리 중 하나에서 `UNUserNotificationCenterDelegate`를 구현하지 않으면 이 부분을 건너뛸 수 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="568d3-149">*If neither your application or one of your third party libraries implements a `UNUserNotificationCenterDelegate` then you can skip this part.*</span></span>

<span data-ttu-id="568d3-150">A `UNUserNotificationCenter` 10 이상인 iOS에서 실행 중인 장치에서 Engagement 알림의 hello SDK toomonitor hello 수명 주기를 통해 대리자를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-150">A `UNUserNotificationCenter` delegate is used by hello SDK toomonitor hello life cycle of Engagement notifications on devices running on iOS 10 or greater.</span></span> <span data-ttu-id="568d3-151">hello SDK가 자체적으로 구현의 hello `UNUserNotificationCenterDelegate` 프로토콜 있지만 하나만 있을 수 있습니다 `UNUserNotificationCenter` 응용 프로그램당 위임 합니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-151">hello SDK has its own implementation of hello `UNUserNotificationCenterDelegate` protocol but there can be only one `UNUserNotificationCenter` delegate per application.</span></span> <span data-ttu-id="568d3-152">대리자 추가 toohello `UNUserNotificationCenter` hello 하나 Engagement 충돌 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-152">Any other delegate added toohello `UNUserNotificationCenter` object will conflict with hello Engagement one.</span></span> <span data-ttu-id="568d3-153">Hello SDK 구현 toogive 자체는 사용 되지 것입니다 다음 나에 다른 공급 업체의 대리자를 감지 하면 기회 tooresolve hello 충돌 합니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-153">If hello SDK detects your or any other third party's delegate then it will not use its own implementation toogive you a chance tooresolve hello conflicts.</span></span> <span data-ttu-id="568d3-154">Tooadd hello Engagement 논리 tooyour tooresolve hello 충돌 순서로 대리자를 소유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-154">You will have tooadd hello Engagement logic tooyour own delegate in order tooresolve hello conflicts.</span></span>

<span data-ttu-id="568d3-155">있는 경우 두 가지 방법으로 tooachieve이</span><span class="sxs-lookup"><span data-stu-id="568d3-155">There are two ways tooachieve this.</span></span>

<span data-ttu-id="568d3-156">제안 1, 대리자를 전달 하 여 toohello SDK를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-156">Proposal 1, simply by forwarding your delegate calls toohello SDK:</span></span>

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

<span data-ttu-id="568d3-157">또는 hello에서 상속 하 여 2, 제안 `AEUserNotificationHandler` 클래스</span><span class="sxs-lookup"><span data-stu-id="568d3-157">Or proposal 2, by inheriting from hello `AEUserNotificationHandler` class</span></span>

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
> <span data-ttu-id="568d3-158">알림을 Engagement 또는 전달 하 여 하지 제공 하는지 여부를 확인할 수 있습니다는 `userInfo` 사전 toohello 에이전트 `isEngagementPushPayload:` 클래스 메서드.</span><span class="sxs-lookup"><span data-stu-id="568d3-158">You can determine whether a notification comes from Engagement or not by passing its `userInfo` dictionary toohello Agent `isEngagementPushPayload:` class method.</span></span>

<span data-ttu-id="568d3-159">해당 hello 있는지 확인 `UNUserNotificationCenter` 개체의 대리자 중 하나가 hello 내에서 tooyour 대리자 설정 되어 `application:willFinishLaunchingWithOptions:` 또는 hello `application:didFinishLaunchingWithOptions:` 응용 프로그램 대리자의 메서드.</span><span class="sxs-lookup"><span data-stu-id="568d3-159">Make sure that hello `UNUserNotificationCenter` object's delegate is set tooyour delegate within either hello `application:willFinishLaunchingWithOptions:` or hello `application:didFinishLaunchingWithOptions:` method of your application delegate.</span></span>
<span data-ttu-id="568d3-160">예를 들어, 제안 1 위에 hello를 구현 하는 경우:</span><span class="sxs-lookup"><span data-stu-id="568d3-160">For instance, if you implemented hello above proposal 1:</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code

        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }

## <a name="how-toocustomize-campaigns"></a><span data-ttu-id="568d3-161">어떻게 toocustomize 캠페인</span><span class="sxs-lookup"><span data-stu-id="568d3-161">How toocustomize campaigns</span></span>
### <a name="notifications"></a><span data-ttu-id="568d3-162">알림</span><span class="sxs-lookup"><span data-stu-id="568d3-162">Notifications</span></span>
<span data-ttu-id="568d3-163">알림에는 시스템 알림과 앱 내 알림의 두 가지 유형이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-163">There are two types of notifications: system and in-app notifications.</span></span>

<span data-ttu-id="568d3-164">시스템 알림은 iOS에서 처리되며 사용자 지정은 가능하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-164">System notifications are handled by iOS, and cannot be customized.</span></span>

<span data-ttu-id="568d3-165">앱에서 알림은 현재 응용 프로그램 창 toohello 동적으로 추가 되는 보기는 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-165">In-app notifications are made of a view that is dynamically added toohello current application window.</span></span> <span data-ttu-id="568d3-166">이 보기를 알림 오버레이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-166">This is called a notification overlay.</span></span> <span data-ttu-id="568d3-167">알림 오버레이은 필요 하지 않으므로 toomodify 하면 응용 프로그램의 보기 중 하나에 빠른 통합에 매우 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-167">Notification overlays are great for a fast integration because they does not require you toomodify any view in your application.</span></span>

#### <a name="layout"></a><span data-ttu-id="568d3-168">레이아웃</span><span class="sxs-lookup"><span data-stu-id="568d3-168">Layout</span></span>
<span data-ttu-id="568d3-169">앱에서 알림 toomodify hello 모양을 수정할 수 hello 파일 `AENotificationView.xib` hello 태그 값 및 hello 기존 하위 유형의 유지으로 tooyour 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-169">toomodify hello look of your in-app notifications, you can simply modify hello file `AENotificationView.xib` tooyour needs, as long as you keep hello tag values and types of hello existing subviews.</span></span>

<span data-ttu-id="568d3-170">기본적으로 앱에서 알림은 hello hello 화면 맨 아래에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-170">By default, in-app notifications are presented at hello bottom of hello screen.</span></span> <span data-ttu-id="568d3-171">화면에서 편집 hello의 hello 위쪽에 제공 된 toodisplay 선호 하는 경우 `AENotificationView.xib` hello 변경 `AutoSizing` hello 해당 슈퍼 뷰의 위쪽에 보관할 수 있도록 hello 주 보기의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-171">If you prefer toodisplay them at hello top of screen, edit hello provided `AENotificationView.xib` and change hello `AutoSizing` property of hello main view so it can be kept at hello top of its superview.</span></span>

#### <a name="categories"></a><span data-ttu-id="568d3-172">범주</span><span class="sxs-lookup"><span data-stu-id="568d3-172">Categories</span></span>
<span data-ttu-id="568d3-173">레이아웃을 제공 하는 hello를 수정 하는 경우 모든 알림 hello 모양을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-173">When you modify hello provided layout, you modify hello look of all your notifications.</span></span> <span data-ttu-id="568d3-174">범주를 사용 toodefine 대상 다양 한 알림 (가능 동작)을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-174">Categories allow you toodefine various targeted looks (possibly behaviors) for notifications.</span></span> <span data-ttu-id="568d3-175">도달률 캠페인을 만들 때 범주를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-175">A category can be specified when you create a Reach campaign.</span></span> <span data-ttu-id="568d3-176">범주를 사용하면 알림과 설문 조사도 사용자 지정할 수 있습니다. 여기에 대해서는 이 문서의 뒷부분에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-176">Keep in mind that categories also let you customize announcements and polls, that is described later in this document.</span></span>

<span data-ttu-id="568d3-177">알림에 대 한 범주 처리기 tooregister tooadd hello 도달 모듈 호출 초기화 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-177">tooregister a category handler for your notifications, you need tooadd a call once hello reach module is initialized.</span></span>

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerNotifier:myNotifier forCategory:@"my_category"];
    ...

<span data-ttu-id="568d3-178">`myNotifier`toohello 프로토콜을 준수 하는 개체의 인스턴스여야 합니다 `AENotifier`합니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-178">`myNotifier` must be an instance of an object that conforms toohello protocol `AENotifier`.</span></span>

<span data-ttu-id="568d3-179">혼자서 hello 프로토콜 메서드를 구현할 수 또는 tooreimplement hello 기존 클래스를 선택할 수 있습니다 `AEDefaultNotifier` hello 작업의 대부분을 이미 수행 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-179">You can implement hello protocol methods by yourself or you can choose tooreimplement hello existing class `AEDefaultNotifier` which already performs most of hello work.</span></span>

<span data-ttu-id="568d3-180">예를 들어 특정 범주에 대 한 tooredefine hello 알림 보기를 하려는 경우이 예제를 따를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-180">For example, if you want tooredefine hello notification view for a specific category, you can follow this example:</span></span>

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

<span data-ttu-id="568d3-181">이 간단한 범주 예제에서는 `MyNotificationView.xib` 파일이 주 응용 프로그램 번들에 포함되어 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-181">This simple example of category assume that you have a file named `MyNotificationView.xib` in your main application bundle.</span></span> <span data-ttu-id="568d3-182">Hello 메서드가 해당 수 toofind 없으면 `.xib`, hello 알림이 표시 되지 것입니다 및 Engagement hello 콘솔에서 메시지를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-182">If hello method is not able toofind a corresponding `.xib`, hello notification will not be displayed and Engagement will output a message in hello console.</span></span>

<span data-ttu-id="568d3-183">제공 된 hello nib 파일 hello 규칙에 따라 허용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-183">hello provided nib file should respect hello following rules:</span></span>

* <span data-ttu-id="568d3-184">파일에는 뷰가 하나만 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-184">It should only contain one view.</span></span>
* <span data-ttu-id="568d3-185">하위 hello 라는 제공 hello nib 파일 내 스토리 hello 동일한 형식을 이어야 합니다.`AENotificationView.xib`</span><span class="sxs-lookup"><span data-stu-id="568d3-185">Subviews should be of hello same types as hello ones inside hello provided nib file named `AENotificationView.xib`</span></span>
* <span data-ttu-id="568d3-186">하위 hello 라는 제공 hello nib 파일 내 스토리 hello으로 태그를 삽입 동일 해야 합니다.`AENotificationView.xib`</span><span class="sxs-lookup"><span data-stu-id="568d3-186">Subviews should have hello same tags as hello ones inside hello provided nib file named `AENotificationView.xib`</span></span>

> [!TIP]
> <span data-ttu-id="568d3-187">라는 제공 hello nib 파일 복사 `AENotificationView.xib`, 여기에서 작업을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-187">Just copy hello provided nib file, named `AENotificationView.xib`, and start working from there.</span></span> <span data-ttu-id="568d3-188">주의 해야 하지만,이 nib 파일은 내부 연결 toohello 클래스 뷰의 hello `AENotificationView`합니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-188">But be careful, hello view inside this nib file is associated toohello class `AENotificationView`.</span></span> <span data-ttu-id="568d3-189">이 클래스는 hello 메서드를 재정의 `layoutSubViews` toomove toocontext에 따라 해당 하위 크기를 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-189">This class redefined hello method `layoutSubViews` toomove and resize its subviews according toocontext.</span></span> <span data-ttu-id="568d3-190">Tooreplace 경우가 사용 하 여는 `UIView` 또는 사용자 지정 보기 클래스.</span><span class="sxs-lookup"><span data-stu-id="568d3-190">You may want tooreplace it with an `UIView` or you custom view class.</span></span>
>
>

<span data-ttu-id="568d3-191">소스 코드와 클래스 문서를 제공 하는 hello 살펴보면 tootake 좋습니다 (원할 경우 예를 들어 tooload hello 코드에서 직접 보기) 알림 깊은 사용자 지정 해야 할 경우 `Protocol ReferencesDefaultNotifier` 및 `AENotifier`합니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-191">If you need deeper customization of your notifications(if you want for instance tooload your view directly from hello code), it is recommended tootake a look at hello provided source code and class documentation of `Protocol ReferencesDefaultNotifier` and `AENotifier`.</span></span>

<span data-ttu-id="568d3-192">참고 사용할 수 있는 여러 범주에 대 한 동일한 알림이 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-192">Note that you can use hello same notifier for multiple categories.</span></span>

<span data-ttu-id="568d3-193">다음과 같은 기본 알림도 다시 정의 된 hello 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-193">You can also redefined hello default notifier like this:</span></span>

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerNotifier:myNotifier forCategory:kAEReachDefaultCategory];

##### <a name="notification-handling"></a><span data-ttu-id="568d3-194">알림 처리</span><span class="sxs-lookup"><span data-stu-id="568d3-194">Notification handling</span></span>
<span data-ttu-id="568d3-195">Hello에서 일부 수명 주기 메서드를 호출 hello 기본 범주를 사용할 경우 `AEReachContent` tooreport 통계 및 업데이트 hello 캠페인 상태 개체:</span><span class="sxs-lookup"><span data-stu-id="568d3-195">When using hello default category, some life cycle methods are called on hello `AEReachContent` object tooreport statistics and update hello campaign state:</span></span>

* <span data-ttu-id="568d3-196">Hello 알림이 응용 프로그램에 표시 되 면 hello `displayNotification` (보고 하는 통계) 메서드를 호출 하 여 `AEReachModule` 경우 `handleNotification:` 반환 `YES`합니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-196">When hello notification is displayed in application, hello `displayNotification` method is called (which reports statistics) by `AEReachModule` if `handleNotification:` returns `YES`.</span></span>
* <span data-ttu-id="568d3-197">Hello 알림은 해제 하는 경우 hello `exitNotification` 메서드는 통계는 보고 되며 다음 캠페인을 지금 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-197">If hello notification is dismissed, hello `exitNotification` method is called, statistic is reported and next campaigns can now be processed.</span></span>
* <span data-ttu-id="568d3-198">Hello 알림의 클릭할 경우 `actionNotification` 은 호출 통계는 보고 되며 hello 연결 된 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-198">If hello notification is clicked, `actionNotification` is called, statistic is reported and hello associated action is performed.</span></span>

<span data-ttu-id="568d3-199">경우 구현 `AENotifier` 바이패스 hello 기본 동작, 혼자서 toocall 이러한 수명 주기 메서드를가지고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-199">If your implementation of `AENotifier` bypasses hello default behavior, you have toocall these life cycle methods by yourself.</span></span> <span data-ttu-id="568d3-200">다음 예제는 hello hello 기본 동작이 사용 하지 않을 경우를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-200">hello following examples illustrate some cases where hello default behavior is bypassed:</span></span>

* <span data-ttu-id="568d3-201">범주 처리를 처음부터 구현한 경우처럼 `AEDefaultNotifier`을(를) 확장하지 않은 경우</span><span class="sxs-lookup"><span data-stu-id="568d3-201">You don't extend `AEDefaultNotifier`, e.g. you implemented category handling from scratch.</span></span>
* <span data-ttu-id="568d3-202">사용자가 `prepareNotificationView:forContent:`있는지 toomap 사이, `onNotificationActioned` 또는 `onNotificationExited` tooone U.I 컨트롤의 합니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-202">You overrode `prepareNotificationView:forContent:`, be sure toomap at least `onNotificationActioned` or `onNotificationExited` tooone of your U.I controls.</span></span>

> [!WARNING]
> <span data-ttu-id="568d3-203">경우 `handleNotification:` hello 콘텐츠 예외가 throw는 삭제 및 `drop` 가 통계를 보고 하 고 호출 다음 캠페인을 지금 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-203">If `handleNotification:` throws an exception, hello content is deleted and `drop` is called, this is reported in statistics and next campaigns can now be processed.</span></span>
>
>

#### <a name="include-notification-as-part-of-an-existing-view"></a><span data-ttu-id="568d3-204">기존 뷰의 일부로 알림 포함</span><span class="sxs-lookup"><span data-stu-id="568d3-204">Include notification as part of an existing view</span></span>
<span data-ttu-id="568d3-205">오버레이는 통합을 빠르게 수행하는 데 유용하지만 사용이 불편하거나 원치 않는 부작용을 야기하는 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-205">Overlays are great for a fast integration but can be sometimes not convenient, or can have unwanted side effects.</span></span>

<span data-ttu-id="568d3-206">본인이 hello 오버레이 시스템 중 일부 보기의 내용과 이러한 보기에 대 한 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-206">If you're not satisfied with hello overlay system in some of your views, you can customize it for these views.</span></span>

<span data-ttu-id="568d3-207">기존 보기에 tooinclude 우리의 알림 레이아웃을 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-207">You can decide tooinclude our notification layout in your existing views.</span></span> <span data-ttu-id="568d3-208">toodo 따라서는 두 가지 구현 스타일:</span><span class="sxs-lookup"><span data-stu-id="568d3-208">toodo so, there is two implementation styles:</span></span>

1. <span data-ttu-id="568d3-209">인터페이스 작성기를 사용 하 여 hello 알림 보기를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-209">Add hello notification view using interface builder</span></span>

   * <span data-ttu-id="568d3-210">*인터페이스 작성기*</span><span class="sxs-lookup"><span data-stu-id="568d3-210">Open *Interface Builder*</span></span>
   * <span data-ttu-id="568d3-211">320 x 60 (또는 768 x 60 iPad에 있는 경우)를 배치 `UIView` hello 알림 tooappear 저장할</span><span class="sxs-lookup"><span data-stu-id="568d3-211">Place a 320x60 (or 768x60 if you are on iPad) `UIView` where you want hello notification tooappear</span></span>
   * <span data-ttu-id="568d3-212">이 보기에 대 한 hello 태그 값을 너무 설정: **36822491**</span><span class="sxs-lookup"><span data-stu-id="568d3-212">Set hello Tag value for this view too: **36822491**</span></span>
2. <span data-ttu-id="568d3-213">프로그래밍 방식으로 hello 알림 보기를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-213">Add hello notification view programmatically.</span></span> <span data-ttu-id="568d3-214">뷰 초기화 되었을 때 코드를 다음 hello 추가:</span><span class="sxs-lookup"><span data-stu-id="568d3-214">Just add hello following code when your view has been initialized:</span></span>

       UIView* notificationView = [[UIView alloc] initWithFrame:CGRectMake(0, 0, 320, 60)]; //Replace x and y coordinate values tooyour needs.
       notificationView.tag = NOTIFICATION_AREA_VIEW_TAG;
       [self.view addSubview:notificationView];

<span data-ttu-id="568d3-215">`NOTIFICATION_AREA_VIEW_TAG` 매크로는 `AEDefaultNotifier.h`에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-215">`NOTIFICATION_AREA_VIEW_TAG` macro can be found in `AEDefaultNotifier.h`.</span></span>

> [!NOTE]
> <span data-ttu-id="568d3-216">hello 기본 알림이 해당 hello 알림 레이아웃이이 보기에 포함 되 고 오버레이 대 한 추가 하지 않는 것에 자동으로 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-216">hello default notifier automatically detects that hello notification layout is included in this view and will not add an overlay for it.</span></span>
>
>

### <a name="announcements-and-polls"></a><span data-ttu-id="568d3-217">알림 및 설문 조사</span><span class="sxs-lookup"><span data-stu-id="568d3-217">Announcements and polls</span></span>
#### <a name="layouts"></a><span data-ttu-id="568d3-218">레이아웃</span><span class="sxs-lookup"><span data-stu-id="568d3-218">Layouts</span></span>
<span data-ttu-id="568d3-219">Hello 파일을 수정할 수 `AEDefaultAnnouncementView.xib` 및 `AEDefaultPollView.xib` 으로 hello 태그 값 및 hello 기존 하위 유형의 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-219">You can modify hello files `AEDefaultAnnouncementView.xib` and `AEDefaultPollView.xib` as long as you keep hello tag values and types of hello existing subviews.</span></span>

#### <a name="categories"></a><span data-ttu-id="568d3-220">범주</span><span class="sxs-lookup"><span data-stu-id="568d3-220">Categories</span></span>
##### <a name="alternate-layouts"></a><span data-ttu-id="568d3-221">대체 레이아웃</span><span class="sxs-lookup"><span data-stu-id="568d3-221">Alternate layouts</span></span>
<span data-ttu-id="568d3-222">알림, 같이 hello 캠페인의 범주는 공지 및 설문 조사의 toohave 사용 되는 대체 레이아웃 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-222">Like notifications, hello campaign's category can be used toohave alternate layouts for your announcements and polls.</span></span>

<span data-ttu-id="568d3-223">확장 해야 공지에 대 한 범주 toocreate **AEAnnouncementViewController** hello 모듈이 초기화 되 면 등록:</span><span class="sxs-lookup"><span data-stu-id="568d3-223">toocreate a category for an announcement, you must extend **AEAnnouncementViewController** and register it once hello reach module has been initialized:</span></span>

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerAnnouncementController:[MyCustomAnnouncementViewController class] forCategory:@"my_category"];

> [!NOTE]
> <span data-ttu-id="568d3-224">사용자는 hello 범주를 사용 하 여 알림에 대 한 알림을 클릭 될 때마다 "내\_범주", 등록 된 보기 컨트롤러 (이 경우 `MyCustomAnnouncementViewController`) hello 메서드를 호출 하 여 초기화 될 `initWithAnnouncement:` 및 hello 보기가 포함 됩니다 추가 된 toohello 현재 응용 프로그램 창입니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-224">Each time a user will click on a notification for an announcement with hello category "my\_category", your registered view controller (in that case `MyCustomAnnouncementViewController`) will be initialized by calling hello method `initWithAnnouncement:` and hello view will be added toohello current application window.</span></span>
>
>

<span data-ttu-id="568d3-225">Hello 구현에서 `AEAnnouncementViewController` tooread hello 속성은 클래스 `announcement` tooinitialize 사용자 하위 뷰가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-225">In your implementation of hello `AEAnnouncementViewController` class you will have tooread hello property `announcement` tooinitialize your subviews.</span></span> <span data-ttu-id="568d3-226">다음 hello 예제에서는 두는 것이 좋습니다 레이블을 사용 하 여 초기화 된 `title` 및 `body` hello의 속성 `AEReachAnnouncement` 클래스:</span><span class="sxs-lookup"><span data-stu-id="568d3-226">Consider hello example below, where two labels are initialized using `title` and `body` properties of hello `AEReachAnnouncement` class:</span></span>

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

<span data-ttu-id="568d3-227">클래스를 제공 하는 hello 확장 않으려는 tooload 보기 혼자서 하지만 tooreuse hello 기본 알림 보기 레이아웃 선택 하면, 사용자 지정 보기 컨트롤러 만들 수 있습니다 하는지 `AEDefaultAnnouncementViewController`합니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-227">If you don't want tooload your views by yourself but you just want tooreuse hello default announcement view layout, you can simply make your custom view controller extends hello provided class `AEDefaultAnnouncementViewController`.</span></span> <span data-ttu-id="568d3-228">이 경우 중복 된 hello nib 파일이 `AEDefaultAnnouncementView.xib` 사용자 지정 보기 컨트롤러에서 로드할 수 있도록로 이름을 바꿉니다 (명명 된 컨트롤러에 대 한 `CustomAnnouncementViewController`, nib 파일을 호출 해야 `CustomAnnouncementView.xib`).</span><span class="sxs-lookup"><span data-stu-id="568d3-228">In that case, duplicate hello nib file `AEDefaultAnnouncementView.xib` and rename it so it can be loaded by your custom view controller (for a controller named `CustomAnnouncementViewController`, you should call your nib file `CustomAnnouncementView.xib`).</span></span>

<span data-ttu-id="568d3-229">공지의 tooreplace hello 기본 범주에 정의 된 hello 범주에 대 한 사용자 지정 보기 컨트롤러를 등록 하기만 하면 `kAEReachDefaultCategory`:</span><span class="sxs-lookup"><span data-stu-id="568d3-229">tooreplace hello default category of announcements, simply register your custom view controller for hello category defined in `kAEReachDefaultCategory`:</span></span>

    [reach registerAnnouncementController:[MyCustomAnnouncementViewController class] forCategory:kAEReachDefaultCategory];

<span data-ttu-id="568d3-230">설문에 사용자 지정 된 hello 수 같은 방식으로:</span><span class="sxs-lookup"><span data-stu-id="568d3-230">Polls can be customized hello same way :</span></span>

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerPollController:[MyCustomPollViewController class] forCategory:@"my_category"];

<span data-ttu-id="568d3-231">이 시간을 제공 하는 hello `MyCustomPollViewController` 확장 해야 `AEPollViewController`합니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-231">This time, hello provided `MyCustomPollViewController` must extend `AEPollViewController`.</span></span> <span data-ttu-id="568d3-232">Hello 기본 컨트롤러에서 tooextend를 선택할 수 있습니다 또는: `AEDefaultPollViewController`합니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-232">Or you can choose tooextend from hello default controller: `AEDefaultPollViewController`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="568d3-233">하거나 toocall 반드시 `action` (`submitAnswers:` 컨트롤러 보기 사용자 지정 설문 조사에 대 한) 또는 `exit` 메서드 전에 hello 뷰-컨트롤러 해제 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-233">Don't forget toocall either `action` (`submitAnswers:` for custom poll view controllers) or `exit` method before hello view controller is dismissed.</span></span> <span data-ttu-id="568d3-234">그렇지 않으면, 통계 전송 되지 않습니다. (예: hello 캠페인에 없는 분석) 하 고 hello 응용 프로그램 프로세스를 다시 시작 될 때까지 더 중요 한 것은 다음 캠페인을 받을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-234">Otherwise, statistics won't be sent (i.e. no analytics on hello campaign) and more importantly next campaigns will not be notified until hello application process is restarted.</span></span>
>
>

##### <a name="implementation-example"></a><span data-ttu-id="568d3-235">구현 예제</span><span class="sxs-lookup"><span data-stu-id="568d3-235">Implementation example</span></span>
<span data-ttu-id="568d3-236">이 구현에서 hello 사용자 지정 알림 뷰는 외부 xib 파일에서 로드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="568d3-236">In this implementation hello custom announcement view is loaded from an external xib file.</span></span>

<span data-ttu-id="568d3-237">와 같은 고급 알림 사용자 지정을 위한 것이 좋습니다 toolook hello 표준 구현의 hello 소스 코드에서.</span><span class="sxs-lookup"><span data-stu-id="568d3-237">Like for advanced notification customization, it is recommended toolook at hello source code of hello standard implementation.</span></span>

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

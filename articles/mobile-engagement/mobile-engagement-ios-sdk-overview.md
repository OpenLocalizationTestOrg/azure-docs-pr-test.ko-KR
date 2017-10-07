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
# <a name="ios-sdk-for-azure-mobile-engagement"></a><span data-ttu-id="6dc61-103">Azure Mobile Engagement용 iOS SDK</span><span class="sxs-lookup"><span data-stu-id="6dc61-103">iOS SDK for Azure Mobile Engagement</span></span>
<span data-ttu-id="6dc61-104">여기에서 시작 tooget hello에 대 한 세부 정보를 모두 방법에는 iOS 앱에에서 Azure Mobile Engagement toointegrate 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc61-104">Start here tooget all hello details on how toointegrate Azure Mobile Engagement in an iOS App.</span></span> <span data-ttu-id="6dc61-105">Toogive 원하는 경우 try 했는지 먼저 확인 해야 하는 것을 수행한 우리의 [15 분 자습서](mobile-engagement-ios-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc61-105">If you'd like toogive it a try first, make sure you do our [15 minutes tutorial](mobile-engagement-ios-get-started.md).</span></span>

<span data-ttu-id="6dc61-106">Toosee hello 클릭 [SDK 콘텐츠](mobile-engagement-ios-sdk-content.md)</span><span class="sxs-lookup"><span data-stu-id="6dc61-106">Click toosee hello [SDK Content](mobile-engagement-ios-sdk-content.md)</span></span>

## <a name="integration-procedures"></a><span data-ttu-id="6dc61-107">통합 절차</span><span class="sxs-lookup"><span data-stu-id="6dc61-107">Integration procedures</span></span>
1. <span data-ttu-id="6dc61-108">여기에서 시작: [어떻게 toointegrate Mobile Engagement에서 iOS 앱](mobile-engagement-ios-integrate-engagement.md)</span><span class="sxs-lookup"><span data-stu-id="6dc61-108">Start here: [How toointegrate Mobile Engagement in your iOS app](mobile-engagement-ios-integrate-engagement.md)</span></span>
2. <span data-ttu-id="6dc61-109">알림: [어떻게 iOS 앱에 toointegrate Reach (알림)](mobile-engagement-ios-integrate-engagement-reach.md)</span><span class="sxs-lookup"><span data-stu-id="6dc61-109">For Notifications: [How toointegrate Reach (Notifications) in your iOS app](mobile-engagement-ios-integrate-engagement-reach.md)</span></span>
3. <span data-ttu-id="6dc61-110">계획 구현 태그: [어떻게 toouse hello 고급 Mobile Engagement API iOS 앱에 태그 지정](mobile-engagement-ios-use-engagement-api.md)</span><span class="sxs-lookup"><span data-stu-id="6dc61-110">Tag plan implementation: [How toouse hello advanced Mobile Engagement tagging API in your iOS app](mobile-engagement-ios-use-engagement-api.md)</span></span>

## <a name="release-notes"></a><span data-ttu-id="6dc61-111">릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="6dc61-111">Release notes</span></span>
### <a name="410-07172017"></a><span data-ttu-id="6dc61-112">4.1.0 (07/17/2017)</span><span class="sxs-lookup"><span data-stu-id="6dc61-112">4.1.0 (07/17/2017)</span></span>
* <span data-ttu-id="6dc61-113">백그라운드에서 지워진 배지를 수정했습니다.</span><span class="sxs-lookup"><span data-stu-id="6dc61-113">Fixed badges cleared in background.</span></span>
* <span data-ttu-id="6dc61-114">기본 큐에서 호출되지 않는 API에 대한 XCode 9의 경고를 수정했습니다.</span><span class="sxs-lookup"><span data-stu-id="6dc61-114">Fixed warnings on XCode 9 about APIs not called in main queue.</span></span>
* <span data-ttu-id="6dc61-115">도달률 설문에서 메모리 누수를 해결했습니다.</span><span class="sxs-lookup"><span data-stu-id="6dc61-115">Fixed a memory leak in Reach polls.</span></span>
* <span data-ttu-id="6dc61-116">iOS 6.X에 대한 지원을 삭제했습니다.</span><span class="sxs-lookup"><span data-stu-id="6dc61-116">Dropped support for iOS 6.X.</span></span> <span data-ttu-id="6dc61-117">적어도 있어야 응용 프로그램의이 버전 hello 배포 대상에서 시작 iOS 7입니다.</span><span class="sxs-lookup"><span data-stu-id="6dc61-117">Starting from this version hello deployment target of your application must be at least iOS 7.</span></span>

<span data-ttu-id="6dc61-118">이전 버전에 대 한 hello를 참조 하십시오 [릴리스 정보를 완료 합니다.](mobile-engagement-ios-release-notes.md)</span><span class="sxs-lookup"><span data-stu-id="6dc61-118">For earlier version please see hello [complete release notes](mobile-engagement-ios-release-notes.md)</span></span>

## <a name="upgrade-procedures"></a><span data-ttu-id="6dc61-119">업그레이드 절차</span><span class="sxs-lookup"><span data-stu-id="6dc61-119">Upgrade procedures</span></span>
<span data-ttu-id="6dc61-120">통합 한 경우 이미 이전 버전의 서비스 응용 프로그램으로, tooconsider hello hello SDK로 업그레이드 하는 경우 지점 뒤에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc61-120">If you already have integrated an older version of Engagement into your application, you have tooconsider hello following points when upgrading hello SDK.</span></span>

<span data-ttu-id="6dc61-121">할 수 있습니다 toofollow 몇 가지 절차 여러 버전의 hello SDK 참조를 누락 하는 경우 전체 hello [업그레이드 절차](mobile-engagement-ios-upgrade-procedure.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc61-121">You may have toofollow several procedures if you missed several versions of hello SDK see hello complete [Upgrade Procedures](mobile-engagement-ios-upgrade-procedure.md).</span></span>

<span data-ttu-id="6dc61-122">각 새 버전의 SDK hello에 대 한 대체 먼저 해야 (제거 하 고 다시 xcode에서 가져올) hello EngagementSDK 및 EngagementReach 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="6dc61-122">For each new version of hello SDK you must first replace (remove and re-import in xcode) hello EngagementSDK and EngagementReach folders.</span></span>

### <a name="from-300-too400"></a><span data-ttu-id="6dc61-123">3.0.0에서 too4.0.0</span><span class="sxs-lookup"><span data-stu-id="6dc61-123">From 3.0.0 too4.0.0</span></span>
### <a name="xcode-8"></a><span data-ttu-id="6dc61-124">XCode 8</span><span class="sxs-lookup"><span data-stu-id="6dc61-124">XCode 8</span></span>
<span data-ttu-id="6dc61-125">XCode 8은의 hello SDK의 버전 4.0.0부터 반드시 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc61-125">XCode 8 is mandatory starting from version 4.0.0 of hello SDK.</span></span>

> [!NOTE]
> <span data-ttu-id="6dc61-126">XCode 7에 실제로 종속 경우 hello를 사용할 수 있습니다 [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh)합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc61-126">If you really depend on XCode 7 then you may use hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="6dc61-127">10 iOS 장치에서 실행 하는 동안이 이전 버전의 hello 모듈이에 알려진된 버그가 있습니다: 시스템 알림을 작업이 수행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6dc61-127">There is a known bug on hello reach module of this previous version while running on iOS 10 devices:  system notifications are not actioned.</span></span> <span data-ttu-id="6dc61-128">toofix tooimplement hello 나면 사용 되지 않는 API `application:didReceiveRemoteNotification:` 응용 프로그램에서 위임 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6dc61-128">toofix this you will have tooimplement hello deprecated API `application:didReceiveRemoteNotification:` in your app delegate as follows:</span></span>
>
>

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> <span data-ttu-id="6dc61-129">이 iOS API는 더 이상 사용되지 않으므로 예정된(부분적인) iOS 버전 업그레이드에서는 이 동작이 달라질 수 있습니다. 따라서 **이 해결 방법은 권장되지 않습니다**.</span><span class="sxs-lookup"><span data-stu-id="6dc61-129">**We do not recommend this workaround** as this behavior can change in any upcoming (even minor) iOS version upgrade because this iOS API is deprecated.</span></span> <span data-ttu-id="6dc61-130">8 tooXCode를 가능한 한 빨리 전환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc61-130">You should switch tooXCode 8 as soon as possible.</span></span>
>
>

#### <a name="usernotifications-framework"></a><span data-ttu-id="6dc61-131">UserNotifications 프레임워크</span><span class="sxs-lookup"><span data-stu-id="6dc61-131">UserNotifications framework</span></span>
<span data-ttu-id="6dc61-132">Tooadd hello 필요한 `UserNotifications` 프레임 워크 빌드 단계로 진행에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc61-132">You need tooadd hello `UserNotifications` framework in your Build Phases.</span></span>

<span data-ttu-id="6dc61-133">hello 프로젝트 탐색기에서 프로젝트 창 열고 hello 올바른 대상을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc61-133">in hello project explorer, open your project pane and select hello correct target.</span></span> <span data-ttu-id="6dc61-134">그런 다음 hello를 열고 **"빌드 단계"** 탭 및 hello **"링크 이진 파일과 라이브러리"** 메뉴에서 프레임 워크를 추가 `UserNotifications.framework` -으로 hello 링크 설정`Optional`</span><span class="sxs-lookup"><span data-stu-id="6dc61-134">Then, open hello **"Build phases"** tab and in hello **"Link Binary With Libraries"** menu, add framework `UserNotifications.framework` - set hello link as `Optional`</span></span>

#### <a name="application-push-capability"></a><span data-ttu-id="6dc61-135">응용 프로그램 푸시 기능</span><span class="sxs-lookup"><span data-stu-id="6dc61-135">Application push capability</span></span>
<span data-ttu-id="6dc61-136">XCode 8 응용 프로그램을 다시 설정할 수 있습니다 기능 밀어넣기, 다시 확인 하세요 hello에 `capability` 선택한 대상의 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc61-136">XCode 8 may reset your app push capability, please double check it in hello `capability` tab of your selected target.</span></span>

#### <a name="add-hello-new-ios-10-notification-registration-code"></a><span data-ttu-id="6dc61-137">Hello 새 iOS 10 알림 등록 코드 추가</span><span class="sxs-lookup"><span data-stu-id="6dc61-137">Add hello new iOS 10 notification registration code</span></span>
<span data-ttu-id="6dc61-138">iOS 10에서 실행 하는 동안 되지 않는 Api hello 이전 코드 조각 tooregister hello 앱 toonotifications 계속 작동 하지만 암호화를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc61-138">hello older code snippet tooregister hello app toonotifications still works but is using deprecated APIs while running on iOS 10.</span></span>

<span data-ttu-id="6dc61-139">가져오기 hello `User Notification` 프레임 워크:</span><span class="sxs-lookup"><span data-stu-id="6dc61-139">Import hello `User Notification` framework:</span></span>

        #import <UserNotifications/UserNotifications.h>

<span data-ttu-id="6dc61-140">응용 프로그램에서 대리자 `application:didFinishLaunchingWithOptions` 메서드 바꾸기:</span><span class="sxs-lookup"><span data-stu-id="6dc61-140">In your application delegate `application:didFinishLaunchingWithOptions` method replace:</span></span>

        if ([application respondsToSelector:@selector(registerUserNotificationSettings:)]) {
            [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert) categories:nil]];
            [application registerForRemoteNotifications];
        }
        else {

            [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
        }

<span data-ttu-id="6dc61-141">다음으로 바꾸기:</span><span class="sxs-lookup"><span data-stu-id="6dc61-141">by :</span></span>

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

#### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a><span data-ttu-id="6dc61-142">UNUserNotificationCenter 대리자 충돌 해결</span><span class="sxs-lookup"><span data-stu-id="6dc61-142">Resolve UNUserNotificationCenter delegate conflicts</span></span>

<span data-ttu-id="6dc61-143">*응용 프로그램이나 타사 라이브러리 중 하나에서 `UNUserNotificationCenterDelegate`를 구현하지 않으면 이 부분을 건너뛸 수 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="6dc61-143">*If neither your application or one of your third party libraries implements a `UNUserNotificationCenterDelegate` then you can skip this part.*</span></span>

<span data-ttu-id="6dc61-144">A `UNUserNotificationCenter` 10 이상인 iOS에서 실행 중인 장치에서 Engagement 알림의 hello SDK toomonitor hello 수명 주기를 통해 대리자를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc61-144">A `UNUserNotificationCenter` delegate is used by hello SDK toomonitor hello life cycle of Engagement notifications on devices running on iOS 10 or greater.</span></span> <span data-ttu-id="6dc61-145">hello SDK가 자체적으로 구현의 hello `UNUserNotificationCenterDelegate` 프로토콜 있지만 하나만 있을 수 있습니다 `UNUserNotificationCenter` 응용 프로그램당 위임 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc61-145">hello SDK has its own implementation of hello `UNUserNotificationCenterDelegate` protocol but there can be only one `UNUserNotificationCenter` delegate per application.</span></span> <span data-ttu-id="6dc61-146">대리자 추가 toohello `UNUserNotificationCenter` hello 하나 Engagement 충돌 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="6dc61-146">Any other delegate added toohello `UNUserNotificationCenter` object will conflict with hello Engagement one.</span></span> <span data-ttu-id="6dc61-147">Hello SDK 구현 toogive 자체는 사용 되지 것입니다 다음 나에 다른 공급 업체의 대리자를 감지 하면 기회 tooresolve hello 충돌 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc61-147">If hello SDK detects your or any other third party's delegate then it will not use its own implementation toogive you a chance tooresolve hello conflicts.</span></span> <span data-ttu-id="6dc61-148">Tooadd hello Engagement 논리 tooyour tooresolve hello 충돌 순서로 대리자를 소유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc61-148">You will have tooadd hello Engagement logic tooyour own delegate in order tooresolve hello conflicts.</span></span>

<span data-ttu-id="6dc61-149">있는 경우 두 가지 방법으로 tooachieve이</span><span class="sxs-lookup"><span data-stu-id="6dc61-149">There are two ways tooachieve this.</span></span>

<span data-ttu-id="6dc61-150">제안 1, 대리자를 전달 하 여 toohello SDK를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc61-150">Proposal 1, simply by forwarding your delegate calls toohello SDK:</span></span>

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

<span data-ttu-id="6dc61-151">또는 hello에서 상속 하 여 2, 제안 `AEUserNotificationHandler` 클래스</span><span class="sxs-lookup"><span data-stu-id="6dc61-151">Or proposal 2, by inheriting from hello `AEUserNotificationHandler` class</span></span>

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
> <span data-ttu-id="6dc61-152">알림을 Engagement 또는 전달 하 여 하지 제공 하는지 여부를 확인할 수 있습니다는 `userInfo` 사전 toohello 에이전트 `isEngagementPushPayload:` 클래스 메서드.</span><span class="sxs-lookup"><span data-stu-id="6dc61-152">You can determine whether a notification comes from Engagement or not by passing its `userInfo` dictionary toohello Agent `isEngagementPushPayload:` class method.</span></span>

<span data-ttu-id="6dc61-153">해당 hello 있는지 확인 `UNUserNotificationCenter` 개체의 대리자 중 하나가 hello 내에서 tooyour 대리자 설정 되어 `application:willFinishLaunchingWithOptions:` 또는 hello `application:didFinishLaunchingWithOptions:` 응용 프로그램 대리자의 메서드.</span><span class="sxs-lookup"><span data-stu-id="6dc61-153">Make sure that hello `UNUserNotificationCenter` object's delegate is set tooyour delegate within either hello `application:willFinishLaunchingWithOptions:` or hello `application:didFinishLaunchingWithOptions:` method of your application delegate.</span></span>
<span data-ttu-id="6dc61-154">예를 들어, 제안 1 위에 hello를 구현 하는 경우:</span><span class="sxs-lookup"><span data-stu-id="6dc61-154">For instance, if you implemented hello above proposal 1:</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code

        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }

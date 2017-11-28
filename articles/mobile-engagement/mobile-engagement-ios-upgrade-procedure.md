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
# <a name="upgrade-procedures"></a><span data-ttu-id="5055c-103">업그레이드 절차</span><span class="sxs-lookup"><span data-stu-id="5055c-103">Upgrade procedures</span></span>
<span data-ttu-id="5055c-104">통합 한 경우 이미 이전 버전의 서비스 응용 프로그램으로, tooconsider hello hello SDK로 업그레이드 하는 경우 지점 뒤에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5055c-104">If you already have integrated an older version of Engagement into your application, you have tooconsider hello following points when upgrading hello SDK.</span></span>

<span data-ttu-id="5055c-105">각 새 버전의 SDK hello에 대 한 대체 먼저 해야 (제거 하 고 다시 xcode에서 가져올) hello EngagementSDK 및 EngagementReach 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="5055c-105">For each new version of hello SDK you must first replace (remove and re-import in xcode) hello EngagementSDK and EngagementReach folders.</span></span>

## <a name="from-300-too400"></a><span data-ttu-id="5055c-106">3.0.0에서 too4.0.0</span><span class="sxs-lookup"><span data-stu-id="5055c-106">From 3.0.0 too4.0.0</span></span>
### <a name="xcode-8"></a><span data-ttu-id="5055c-107">XCode 8</span><span class="sxs-lookup"><span data-stu-id="5055c-107">XCode 8</span></span>
<span data-ttu-id="5055c-108">XCode 8은의 hello SDK의 버전 4.0.0부터 반드시 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5055c-108">XCode 8 is mandatory starting from version 4.0.0 of hello SDK.</span></span>

> [!NOTE]
> <span data-ttu-id="5055c-109">XCode 7에 실제로 종속 경우 hello를 사용할 수 있습니다 [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh)합니다.</span><span class="sxs-lookup"><span data-stu-id="5055c-109">If you really depend on XCode 7 then you may use hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="5055c-110">10 iOS 장치에서 실행 하는 동안이 이전 버전의 hello 모듈이에 알려진된 버그가 있습니다: 시스템 알림을 작업이 수행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5055c-110">There is a known bug on hello reach module of this previous version while running on iOS 10 devices:  system notifications are not actioned.</span></span> <span data-ttu-id="5055c-111">toofix tooimplement hello 나면 사용 되지 않는 API `application:didReceiveRemoteNotification:` 응용 프로그램에서 위임 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5055c-111">toofix this you will have tooimplement hello deprecated API `application:didReceiveRemoteNotification:` in your app delegate as follows:</span></span>
> 
> 

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> <span data-ttu-id="5055c-112">이 iOS API는 더 이상 사용되지 않으므로 예정된(부분적인) iOS 버전 업그레이드에서는 이 동작이 달라질 수 있습니다. 따라서 **이 해결 방법은 권장되지 않습니다**.</span><span class="sxs-lookup"><span data-stu-id="5055c-112">**We do not recommend this workaround** as this behavior can change in any upcoming (even minor) iOS version upgrade because this iOS API is deprecated.</span></span> <span data-ttu-id="5055c-113">8 tooXCode를 가능한 한 빨리 전환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5055c-113">You should switch tooXCode 8 as soon as possible.</span></span>
> 
> 

### <a name="usernotifications-framework"></a><span data-ttu-id="5055c-114">UserNotifications 프레임워크</span><span class="sxs-lookup"><span data-stu-id="5055c-114">UserNotifications framework</span></span>
<span data-ttu-id="5055c-115">Tooadd hello 필요한 `UserNotifications` 프레임 워크 빌드 단계로 진행에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="5055c-115">You need tooadd hello `UserNotifications` framework in your Build Phases.</span></span>

<span data-ttu-id="5055c-116">hello 프로젝트 탐색기에서 프로젝트 창 열고 hello 올바른 대상을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5055c-116">in hello project explorer, open your project pane and select hello correct target.</span></span> <span data-ttu-id="5055c-117">그런 다음 hello를 열고 **"빌드 단계"** 탭 및 hello **"링크 이진 파일과 라이브러리"** 메뉴에서 프레임 워크를 추가 `UserNotifications.framework` -으로 hello 링크 설정`Optional`</span><span class="sxs-lookup"><span data-stu-id="5055c-117">Then, open hello **"Build phases"** tab and in hello **"Link Binary With Libraries"** menu, add framework `UserNotifications.framework` - set hello link as `Optional`</span></span>

### <a name="application-push-capability"></a><span data-ttu-id="5055c-118">응용 프로그램 푸시 기능</span><span class="sxs-lookup"><span data-stu-id="5055c-118">Application push capability</span></span>
<span data-ttu-id="5055c-119">XCode 8 응용 프로그램을 다시 설정할 수 있습니다 기능 밀어넣기, 다시 확인 하세요 hello에 `capability` 선택한 대상의 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5055c-119">XCode 8 may reset your app push capability, please double check it in hello `capability` tab of your selected target.</span></span>

### <a name="add-hello-new-ios-10-notification-registration-code"></a><span data-ttu-id="5055c-120">Hello 새 iOS 10 알림 등록 코드 추가</span><span class="sxs-lookup"><span data-stu-id="5055c-120">Add hello new iOS 10 notification registration code</span></span>
<span data-ttu-id="5055c-121">iOS 10에서 실행 하는 동안 되지 않는 Api hello 이전 코드 조각 tooregister hello 앱 toonotifications 계속 작동 하지만 암호화를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5055c-121">hello older code snippet tooregister hello app toonotifications still works but is using deprecated APIs while running on iOS 10.</span></span>

<span data-ttu-id="5055c-122">가져오기 hello `User Notification` 프레임 워크:</span><span class="sxs-lookup"><span data-stu-id="5055c-122">Import hello `User Notification` framework:</span></span>

        #import <UserNotifications/UserNotifications.h> 

<span data-ttu-id="5055c-123">응용 프로그램에서 대리자 `application:didFinishLaunchingWithOptions` 메서드 바꾸기:</span><span class="sxs-lookup"><span data-stu-id="5055c-123">In your application delegate `application:didFinishLaunchingWithOptions` method replace:</span></span>

    if ([application respondsToSelector:@selector(registerUserNotificationSettings:)]) {
        [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert) categories:nil]];
        [application registerForRemoteNotifications];
    }
    else {

        [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
    }

<span data-ttu-id="5055c-124">다음으로 바꾸기:</span><span class="sxs-lookup"><span data-stu-id="5055c-124">by :</span></span>

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

### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a><span data-ttu-id="5055c-125">UNUserNotificationCenter 대리자 충돌 해결</span><span class="sxs-lookup"><span data-stu-id="5055c-125">Resolve UNUserNotificationCenter delegate conflicts</span></span>

<span data-ttu-id="5055c-126">*응용 프로그램이나 타사 라이브러리 중 하나에서 `UNUserNotificationCenterDelegate`를 구현하지 않으면 이 부분을 건너뛸 수 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="5055c-126">*If neither your application or one of your third party libraries implements a `UNUserNotificationCenterDelegate` then you can skip this part.*</span></span>

<span data-ttu-id="5055c-127">A `UNUserNotificationCenter` 10 이상인 iOS에서 실행 중인 장치에서 Engagement 알림의 hello SDK toomonitor hello 수명 주기를 통해 대리자를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5055c-127">A `UNUserNotificationCenter` delegate is used by hello SDK toomonitor hello life cycle of Engagement notifications on devices running on iOS 10 or greater.</span></span> <span data-ttu-id="5055c-128">hello SDK가 자체적으로 구현의 hello `UNUserNotificationCenterDelegate` 프로토콜 있지만 하나만 있을 수 있습니다 `UNUserNotificationCenter` 응용 프로그램당 위임 합니다.</span><span class="sxs-lookup"><span data-stu-id="5055c-128">hello SDK has its own implementation of hello `UNUserNotificationCenterDelegate` protocol but there can be only one `UNUserNotificationCenter` delegate per application.</span></span> <span data-ttu-id="5055c-129">대리자 추가 toohello `UNUserNotificationCenter` hello 하나 Engagement 충돌 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="5055c-129">Any other delegate added toohello `UNUserNotificationCenter` object will conflict with hello Engagement one.</span></span> <span data-ttu-id="5055c-130">Hello SDK 구현 toogive 자체는 사용 되지 것입니다 다음 나에 다른 공급 업체의 대리자를 감지 하면 기회 tooresolve hello 충돌 합니다.</span><span class="sxs-lookup"><span data-stu-id="5055c-130">If hello SDK detects your or any other third party's delegate then it will not use its own implementation toogive you a chance tooresolve hello conflicts.</span></span> <span data-ttu-id="5055c-131">Tooadd hello Engagement 논리 tooyour tooresolve hello 충돌 순서로 대리자를 소유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5055c-131">You will have tooadd hello Engagement logic tooyour own delegate in order tooresolve hello conflicts.</span></span>

<span data-ttu-id="5055c-132">있는 경우 두 가지 방법으로 tooachieve이</span><span class="sxs-lookup"><span data-stu-id="5055c-132">There are two ways tooachieve this.</span></span>

<span data-ttu-id="5055c-133">제안 1, 대리자를 전달 하 여 toohello SDK를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="5055c-133">Proposal 1, simply by forwarding your delegate calls toohello SDK:</span></span>

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

<span data-ttu-id="5055c-134">또는 hello에서 상속 하 여 2, 제안 `AEUserNotificationHandler` 클래스</span><span class="sxs-lookup"><span data-stu-id="5055c-134">Or proposal 2, by inheriting from hello `AEUserNotificationHandler` class</span></span>

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
> <span data-ttu-id="5055c-135">알림을 Engagement 또는 전달 하 여 하지 제공 하는지 여부를 확인할 수 있습니다는 `userInfo` 사전 toohello 에이전트 `isEngagementPushPayload:` 클래스 메서드.</span><span class="sxs-lookup"><span data-stu-id="5055c-135">You can determine whether a notification comes from Engagement or not by passing its `userInfo` dictionary toohello Agent `isEngagementPushPayload:` class method.</span></span>

<span data-ttu-id="5055c-136">해당 hello 있는지 확인 `UNUserNotificationCenter` 개체의 대리자 중 하나가 hello 내에서 tooyour 대리자 설정 되어 `application:willFinishLaunchingWithOptions:` 또는 hello `application:didFinishLaunchingWithOptions:` 응용 프로그램 대리자의 메서드.</span><span class="sxs-lookup"><span data-stu-id="5055c-136">Make sure that hello `UNUserNotificationCenter` object's delegate is set tooyour delegate within either hello `application:willFinishLaunchingWithOptions:` or hello `application:didFinishLaunchingWithOptions:` method of your application delegate.</span></span>
<span data-ttu-id="5055c-137">예를 들어, 제안 1 위에 hello를 구현 하는 경우:</span><span class="sxs-lookup"><span data-stu-id="5055c-137">For instance, if you implemented hello above proposal 1:</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code
  
        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }

## <a name="from-200-too300"></a><span data-ttu-id="5055c-138">2.0.0에서 too3.0.0</span><span class="sxs-lookup"><span data-stu-id="5055c-138">From 2.0.0 too3.0.0</span></span>
<span data-ttu-id="5055c-139">iOS 4.X에 대한 지원을 삭제했습니다.</span><span class="sxs-lookup"><span data-stu-id="5055c-139">Dropped support for iOS 4.X.</span></span> <span data-ttu-id="5055c-140">적어도 있어야 응용 프로그램의이 버전 hello 배포 대상에서 시작 iOS 6입니다.</span><span class="sxs-lookup"><span data-stu-id="5055c-140">Starting from this version hello deployment target of your application must be at least iOS 6.</span></span>

<span data-ttu-id="5055c-141">추가 해야 하는 경우 범위를 사용 하는 응용 프로그램에서 `remote-notification` 값 toohello `UIBackgroundModes` 순서 tooreceive 원격 알림에 Info.plist 파일의 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="5055c-141">If you are using Reach in your application, you must add `remote-notification` value toohello `UIBackgroundModes` array in your Info.plist file in order tooreceive remote notifications.</span></span>

<span data-ttu-id="5055c-142">메서드를 hello `application:didReceiveRemoteNotification:` toobe로 대체 해야 `application:didReceiveRemoteNotification:fetchCompletionHandler:` 응용 프로그램 대리자에서입니다.</span><span class="sxs-lookup"><span data-stu-id="5055c-142">hello method `application:didReceiveRemoteNotification:` needs toobe replaced by `application:didReceiveRemoteNotification:fetchCompletionHandler:` in your application delegate.</span></span>

<span data-ttu-id="5055c-143">"AEPushDelegate.h"는 사용 되지 않습니다. 인터페이스 할 tooremove 모든 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="5055c-143">"AEPushDelegate.h" is deprecated interface and you need tooremove all references.</span></span> <span data-ttu-id="5055c-144">여기에 제거 `[[EngagementAgent shared] setPushDelegate:self]` 및 응용 프로그램 대리자에서 메서드를 위임할 hello:</span><span class="sxs-lookup"><span data-stu-id="5055c-144">This includes removing `[[EngagementAgent shared] setPushDelegate:self]` and hello delegate methods from your application delegate:</span></span>

    -(void)willRetrieveLaunchMessage;
    -(void)didFailToRetrieveLaunchMessage;
    -(void)didReceiveLaunchMessage:(AEPushMessage*)launchMessage;

## <a name="from-1160-too200"></a><span data-ttu-id="5055c-145">1.16.0에서 too2.0.0</span><span class="sxs-lookup"><span data-stu-id="5055c-145">From 1.16.0 too2.0.0</span></span>
<span data-ttu-id="5055c-146">hello 다음 설명 방법을 toomigrate SDK 통합 hello Capptain 서비스에서에서 제공한 Capptain SAS Azure Mobile Engagement에서 제공 하는 응용 프로그램에 합니다.</span><span class="sxs-lookup"><span data-stu-id="5055c-146">hello following describes how toomigrate an SDK integration from hello Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span>
<span data-ttu-id="5055c-147">이전 버전에서 마이그레이션하려는 경우 먼저 hello Capptain 웹 사이트 toomigrate too1.16 참조 다음 절차를 수행 하는 hello를 적용 하십시오.</span><span class="sxs-lookup"><span data-stu-id="5055c-147">If you are migrating from an earlier version, please consult hello Capptain web site toomigrate too1.16 first then apply hello following procedure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5055c-148">Capptain 및 Mobile Engagement는 동일한 서비스 하지 hello 및 아래에 주어진 hello 프로시저 어떻게 toomigrate hello 클라이언트 응용 프로그램을 강조 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="5055c-148">Capptain and Mobile Engagement are not hello same services and hello procedure given below only highlights how toomigrate hello client app.</span></span> <span data-ttu-id="5055c-149">Hello 앱에 마이그레이션 hello SDK hello Capptain 서버 toohello Mobile Engagement 서버에서 데이터를 마이그레이션하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5055c-149">Migrating hello SDK in hello app will NOT migrate your data from hello Capptain servers toohello Mobile Engagement servers</span></span>
> 
> 

### <a name="agent"></a><span data-ttu-id="5055c-150">에이전트</span><span class="sxs-lookup"><span data-stu-id="5055c-150">Agent</span></span>
<span data-ttu-id="5055c-151">메서드를 hello `registerApp:` hello 새 메서드로 바뀌었습니다 `init:`합니다.</span><span class="sxs-lookup"><span data-stu-id="5055c-151">hello method `registerApp:` has been replaced by hello new method `init:`.</span></span> <span data-ttu-id="5055c-152">그에 따라 응용 프로그램 대리자를 업데이트하고 다음과 같이 연결 문자열을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5055c-152">Your application delegate must be updated accordingly and use connection string:</span></span>

            - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
            {
              [...]
              [EngagementAgent init:@"YOUR_CONNECTION_STRING"];
              [...]
            }

<span data-ttu-id="5055c-153">SmartAd 추적 하기만 하면 tooremove 함수의 모든 인스턴스의 SDK에서 제거 되었습니다 `AETrackModule` 클래스</span><span class="sxs-lookup"><span data-stu-id="5055c-153">SmartAd tracking has been removed from SDK you just have tooremove all instances of `AETrackModule` class</span></span>

### <a name="class-name-changes"></a><span data-ttu-id="5055c-154">클래스 이름 변경</span><span class="sxs-lookup"><span data-stu-id="5055c-154">Class Name Changes</span></span>
<span data-ttu-id="5055c-155">Hello 방법의 일환으로, toobe 변경 해야 하는 클래스/파일 이름의 몇 가지 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5055c-155">As part of hello rebranding, there are couple of class/file names that need toobe changed.</span></span>

<span data-ttu-id="5055c-156">"CP" 접두사가 붙은 모든 클래스의 이름이 "AE"로 바뀌었습니다.</span><span class="sxs-lookup"><span data-stu-id="5055c-156">All classes prefixed with "CP" are renamed with "AE" prefix.</span></span>

<span data-ttu-id="5055c-157">예제:</span><span class="sxs-lookup"><span data-stu-id="5055c-157">Example:</span></span>

* <span data-ttu-id="5055c-158">`CPModule.h`이름이 너무`AEModule.h`합니다.</span><span class="sxs-lookup"><span data-stu-id="5055c-158">`CPModule.h` is renamed too`AEModule.h`.</span></span>

<span data-ttu-id="5055c-159">"Capptain" 접두사가 붙은 모든 클래스의 이름이 "Engagement"로 바뀌었습니다.</span><span class="sxs-lookup"><span data-stu-id="5055c-159">All classes prefixed with "Capptain" are renamed with "Engagement" prefix.</span></span>

<span data-ttu-id="5055c-160">예제:</span><span class="sxs-lookup"><span data-stu-id="5055c-160">Examples:</span></span>

* <span data-ttu-id="5055c-161">클래스를 hello `CapptainAgent` 너무 이름이`EngagementAgent`합니다.</span><span class="sxs-lookup"><span data-stu-id="5055c-161">hello class `CapptainAgent` is renamed too`EngagementAgent`.</span></span>
* <span data-ttu-id="5055c-162">클래스를 hello `CapptainTableViewController` 너무 이름이`EngagementTableViewController`합니다.</span><span class="sxs-lookup"><span data-stu-id="5055c-162">hello class `CapptainTableViewController` is renamed too`EngagementTableViewController`.</span></span>
* <span data-ttu-id="5055c-163">클래스를 hello `CapptainUtils` 너무 이름이`EngagementUtils`합니다.</span><span class="sxs-lookup"><span data-stu-id="5055c-163">hello class `CapptainUtils` is renamed too`EngagementUtils`.</span></span>
* <span data-ttu-id="5055c-164">클래스를 hello `CapptainViewController` 너무 이름이`EngagementViewController`합니다.</span><span class="sxs-lookup"><span data-stu-id="5055c-164">hello class `CapptainViewController` is renamed too`EngagementViewController`.</span></span>


---
title: "Azure Mobile Engagement iOS SDK 업그레이드 절차 | Microsoft Docs"
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
ms.openlocfilehash: 37c7f133d079186f828d58cabce0d2a259efd085
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="upgrade-procedures"></a><span data-ttu-id="7522b-103">업그레이드 절차</span><span class="sxs-lookup"><span data-stu-id="7522b-103">Upgrade procedures</span></span>
<span data-ttu-id="7522b-104">이전 버전의 Engagement를 응용 프로그램에 이미 통합한 경우에는 SDK를 업그레이드할 때 다음 사항을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7522b-104">If you already have integrated an older version of Engagement into your application, you have to consider the following points when upgrading the SDK.</span></span>

<span data-ttu-id="7522b-105">SDK의 각 새 버전에 대해 먼저 EngagementSDK 및 EngagementReach 폴더를 대체해야 합니다. 즉, xcode에서 이 폴더를 제거한 후에 다시 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7522b-105">For each new version of the SDK you must first replace (remove and re-import in xcode) the EngagementSDK and EngagementReach folders.</span></span>

## <a name="from-300-to-400"></a><span data-ttu-id="7522b-106">3.0.0에서 4.0.0으로</span><span class="sxs-lookup"><span data-stu-id="7522b-106">From 3.0.0 to 4.0.0</span></span>
### <a name="xcode-8"></a><span data-ttu-id="7522b-107">XCode 8</span><span class="sxs-lookup"><span data-stu-id="7522b-107">XCode 8</span></span>
<span data-ttu-id="7522b-108">XCode 8은 SDK 버전 4.0.0부터 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="7522b-108">XCode 8 is mandatory starting from version 4.0.0 of the SDK.</span></span>

> [!NOTE]
> <span data-ttu-id="7522b-109">XCode 7을 사용하는 경우 [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh)를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7522b-109">If you really depend on XCode 7 then you may use the [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="7522b-110">iOS 10 장치에서 실행하는 경우 이 이전 버전의 도달률 모듈에는 알려진 버그가 있습니다. 시스템 알림은 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7522b-110">There is a known bug on the reach module of this previous version while running on iOS 10 devices:  system notifications are not actioned.</span></span> <span data-ttu-id="7522b-111">이 문제를 해결하려면 다음과 같이 앱 대리자에서 더 이상 사용되지 않는 API `application:didReceiveRemoteNotification:`을 구현해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7522b-111">To fix this you will have to implement the deprecated API `application:didReceiveRemoteNotification:` in your app delegate as follows:</span></span>
> 
> 

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> <span data-ttu-id="7522b-112">이 iOS API는 더 이상 사용되지 않으므로 예정된(부분적인) iOS 버전 업그레이드에서는 이 동작이 달라질 수 있습니다. 따라서 **이 해결 방법은 권장되지 않습니다**.</span><span class="sxs-lookup"><span data-stu-id="7522b-112">**We do not recommend this workaround** as this behavior can change in any upcoming (even minor) iOS version upgrade because this iOS API is deprecated.</span></span> <span data-ttu-id="7522b-113">가능한 한 빨리 XCode 8로 전환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7522b-113">You should switch to XCode 8 as soon as possible.</span></span>
> 
> 

### <a name="usernotifications-framework"></a><span data-ttu-id="7522b-114">UserNotifications 프레임워크</span><span class="sxs-lookup"><span data-stu-id="7522b-114">UserNotifications framework</span></span>
<span data-ttu-id="7522b-115">빌드 단계에서 `UserNotifications` 프레임워크를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7522b-115">You need to add the `UserNotifications` framework in your Build Phases.</span></span>

<span data-ttu-id="7522b-116">프로젝트 탐색기에서 프로젝트 창을 열고 올바른 대상을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7522b-116">in the project explorer, open your project pane and select the correct target.</span></span> <span data-ttu-id="7522b-117">그런 다음 **"빌드 단계"** 탭을 열고 **"이진과 라이브러리 연결"** 메뉴에서 프레임워크 `UserNotifications.framework` - 링크를 `Optional`로 설정을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7522b-117">Then, open the **"Build phases"** tab and in the **"Link Binary With Libraries"** menu, add framework `UserNotifications.framework` - set the link as `Optional`</span></span>

### <a name="application-push-capability"></a><span data-ttu-id="7522b-118">응용 프로그램 푸시 기능</span><span class="sxs-lookup"><span data-stu-id="7522b-118">Application push capability</span></span>
<span data-ttu-id="7522b-119">XCode 8은 앱 푸시 기능을 다시 설정할 수 있습니다. 선택한 대상의 `capability` 탭에서 한 번 더 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="7522b-119">XCode 8 may reset your app push capability, please double check it in the `capability` tab of your selected target.</span></span>

### <a name="add-the-new-ios-10-notification-registration-code"></a><span data-ttu-id="7522b-120">새 iOS 10 알림 등록 코드</span><span class="sxs-lookup"><span data-stu-id="7522b-120">Add the new iOS 10 notification registration code</span></span>
<span data-ttu-id="7522b-121">알림에 앱을 등록하는 이전 코드 조각은 계속 작동하지만 iOS 10에서 실행되는 동안은 사용이 중단된 API를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7522b-121">The older code snippet to register the app to notifications still works but is using deprecated APIs while running on iOS 10.</span></span>

<span data-ttu-id="7522b-122">`User Notification` 프레임워크 가져오기:</span><span class="sxs-lookup"><span data-stu-id="7522b-122">Import the `User Notification` framework:</span></span>

        #import <UserNotifications/UserNotifications.h> 

<span data-ttu-id="7522b-123">응용 프로그램에서 대리자 `application:didFinishLaunchingWithOptions` 메서드 바꾸기:</span><span class="sxs-lookup"><span data-stu-id="7522b-123">In your application delegate `application:didFinishLaunchingWithOptions` method replace:</span></span>

    if ([application respondsToSelector:@selector(registerUserNotificationSettings:)]) {
        [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert) categories:nil]];
        [application registerForRemoteNotifications];
    }
    else {

        [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
    }

<span data-ttu-id="7522b-124">다음으로 바꾸기:</span><span class="sxs-lookup"><span data-stu-id="7522b-124">by :</span></span>

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

### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a><span data-ttu-id="7522b-125">UNUserNotificationCenter 대리자 충돌 해결</span><span class="sxs-lookup"><span data-stu-id="7522b-125">Resolve UNUserNotificationCenter delegate conflicts</span></span>

<span data-ttu-id="7522b-126">*응용 프로그램이나 타사 라이브러리 중 하나에서 `UNUserNotificationCenterDelegate`를 구현하지 않으면 이 부분을 건너뛸 수 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="7522b-126">*If neither your application or one of your third party libraries implements a `UNUserNotificationCenterDelegate` then you can skip this part.*</span></span>

<span data-ttu-id="7522b-127">`UNUserNotificationCenter` 대리자는 iOS 10 이상에서 실행되는 장치의 Engagement 알림 수명 주기를 모니터링하기 위해 SDK에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7522b-127">A `UNUserNotificationCenter` delegate is used by the SDK to monitor the life cycle of Engagement notifications on devices running on iOS 10 or greater.</span></span> <span data-ttu-id="7522b-128">SDK에는 `UNUserNotificationCenterDelegate` 프로토콜의 자체 구현이 있지만 응용 프로그램당 `UNUserNotificationCenter` 위임자가 하나만 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7522b-128">The SDK has its own implementation of the `UNUserNotificationCenterDelegate` protocol but there can be only one `UNUserNotificationCenter` delegate per application.</span></span> <span data-ttu-id="7522b-129">`UNUserNotificationCenter` 개체에 추가된 다른 모든 대리자는 Engagement 대리인과 충돌합니다.</span><span class="sxs-lookup"><span data-stu-id="7522b-129">Any other delegate added to the `UNUserNotificationCenter` object will conflict with the Engagement one.</span></span> <span data-ttu-id="7522b-130">SDK가 사용자 또는 다른 타사 대리자를 발견하는 경우 충돌을 해결할 기회를 주기 위해 자체 구현을 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7522b-130">If the SDK detects your or any other third party's delegate then it will not use its own implementation to give you a chance to resolve the conflicts.</span></span> <span data-ttu-id="7522b-131">충돌을 해결하기 위해 사용자 고유의 대리자에게 Engagement 논리를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7522b-131">You will have to add the Engagement logic to your own delegate in order to resolve the conflicts.</span></span>

<span data-ttu-id="7522b-132">이 작업은 다음 두 가지 방법으로 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7522b-132">There are two ways to achieve this.</span></span>

<span data-ttu-id="7522b-133">제안 1, SDK에 대리자 호출 전달</span><span class="sxs-lookup"><span data-stu-id="7522b-133">Proposal 1, simply by forwarding your delegate calls to the SDK:</span></span>

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

<span data-ttu-id="7522b-134">또는 제안 2, `AEUserNotificationHandler` 클래스에서 상속</span><span class="sxs-lookup"><span data-stu-id="7522b-134">Or proposal 2, by inheriting from the `AEUserNotificationHandler` class</span></span>

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
> <span data-ttu-id="7522b-135">해당 `userInfo` 사전을 에이전트 `isEngagementPushPayload:` 클래스 메서드에 전달하여 알림이 Engagement에서 온 것인지를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7522b-135">You can determine whether a notification comes from Engagement or not by passing its `userInfo` dictionary to the Agent `isEngagementPushPayload:` class method.</span></span>

<span data-ttu-id="7522b-136">응용 프로그램 대리자의 `application:willFinishLaunchingWithOptions:` 또는 `application:didFinishLaunchingWithOptions:` 메서드 내에서 `UNUserNotificationCenter` 개체의 대리자가 현재 대리자로 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7522b-136">Make sure that the `UNUserNotificationCenter` object's delegate is set to your delegate within either the `application:willFinishLaunchingWithOptions:` or the `application:didFinishLaunchingWithOptions:` method of your application delegate.</span></span>
<span data-ttu-id="7522b-137">예를 들어, 위의 제안 1을 구현하는 경우:</span><span class="sxs-lookup"><span data-stu-id="7522b-137">For instance, if you implemented the above proposal 1:</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code
  
        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }

## <a name="from-200-to-300"></a><span data-ttu-id="7522b-138">2.0.0에서 3.0.0으로</span><span class="sxs-lookup"><span data-stu-id="7522b-138">From 2.0.0 to 3.0.0</span></span>
<span data-ttu-id="7522b-139">iOS 4.X에 대한 지원을 삭제했습니다.</span><span class="sxs-lookup"><span data-stu-id="7522b-139">Dropped support for iOS 4.X.</span></span> <span data-ttu-id="7522b-140">이 버전부터 응용 프로그램의 배포 대상은 iOS 6 이상이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7522b-140">Starting from this version the deployment target of your application must be at least iOS 6.</span></span>

<span data-ttu-id="7522b-141">응용 프로그램에서 도달률을 사용하는 경우 원격 알림을 받기 위해 `remote-notification` 값을 Info.plist 파일의 `UIBackgroundModes` 배열에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7522b-141">If you are using Reach in your application, you must add `remote-notification` value to the `UIBackgroundModes` array in your Info.plist file in order to receive remote notifications.</span></span>

<span data-ttu-id="7522b-142">메서드 `application:didReceiveRemoteNotification:`은 응용 프로그램 대리자의 `application:didReceiveRemoteNotification:fetchCompletionHandler:`로 대체해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7522b-142">The method `application:didReceiveRemoteNotification:` needs to be replaced by `application:didReceiveRemoteNotification:fetchCompletionHandler:` in your application delegate.</span></span>

<span data-ttu-id="7522b-143">"AEPushDelegate.h"는 더 이상 사용되지 않는 인터페이스이므로 모든 참조를 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7522b-143">"AEPushDelegate.h" is deprecated interface and you need to remove all references.</span></span> <span data-ttu-id="7522b-144">여기에는 응용 프로그램 대리자에서 `[[EngagementAgent shared] setPushDelegate:self]` 및 대리자 메서드를 제거하는 일도 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="7522b-144">This includes removing `[[EngagementAgent shared] setPushDelegate:self]` and the delegate methods from your application delegate:</span></span>

    -(void)willRetrieveLaunchMessage;
    -(void)didFailToRetrieveLaunchMessage;
    -(void)didReceiveLaunchMessage:(AEPushMessage*)launchMessage;

## <a name="from-1160-to-200"></a><span data-ttu-id="7522b-145">1.16.0에서 2.0.0으로 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="7522b-145">From 1.16.0 to 2.0.0</span></span>
<span data-ttu-id="7522b-146">아래에서는 SDK 통합을 Capptain SAS 제공 Capptain 서비스에서 Azure Mobile Engagement 구동 앱으로 마이그레이션하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7522b-146">The following describes how to migrate an SDK integration from the Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span>
<span data-ttu-id="7522b-147">이전 버전에서 마이그레이션하는 경우 Capptain 웹 사이트를 참조하여 먼저 1.16으로 마이그레이션한 후 다음 절차를 적용하세요.</span><span class="sxs-lookup"><span data-stu-id="7522b-147">If you are migrating from an earlier version, please consult the Capptain web site to migrate to 1.16 first then apply the following procedure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7522b-148">Capptain과 Mobile Engagement는 같은 서비스가 아니며, 아래에서 제공하는 절차에서는 클라이언트 앱을 마이그레이션하는 방법만 중점적으로 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7522b-148">Capptain and Mobile Engagement are not the same services and the procedure given below only highlights how to migrate the client app.</span></span> <span data-ttu-id="7522b-149">앱에서 SDK를 마이그레이션해도 데이터가 Capptain 서버에서 Mobile Engagement 서버로 마이그레이션되지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7522b-149">Migrating the SDK in the app will NOT migrate your data from the Capptain servers to the Mobile Engagement servers</span></span>
> 
> 

### <a name="agent"></a><span data-ttu-id="7522b-150">에이전트</span><span class="sxs-lookup"><span data-stu-id="7522b-150">Agent</span></span>
<span data-ttu-id="7522b-151">메서드 `registerApp:`이(가) 새 메서드인 `init:`(으)로 바뀌었습니다.</span><span class="sxs-lookup"><span data-stu-id="7522b-151">The method `registerApp:` has been replaced by the new method `init:`.</span></span> <span data-ttu-id="7522b-152">그에 따라 응용 프로그램 대리자를 업데이트하고 다음과 같이 연결 문자열을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7522b-152">Your application delegate must be updated accordingly and use connection string:</span></span>

            - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
            {
              [...]
              [EngagementAgent init:@"YOUR_CONNECTION_STRING"];
              [...]
            }

<span data-ttu-id="7522b-153">SmartAd 추적이 SDK에서 제거되었으므로 `AETrackModule` 클래스의 모든 인스턴스를 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7522b-153">SmartAd tracking has been removed from SDK you just have to remove all instances of `AETrackModule` class</span></span>

### <a name="class-name-changes"></a><span data-ttu-id="7522b-154">클래스 이름 변경</span><span class="sxs-lookup"><span data-stu-id="7522b-154">Class Name Changes</span></span>
<span data-ttu-id="7522b-155">브랜드 변경의 일환으로 몇 가지 클래스/파일 이름을 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7522b-155">As part of the rebranding, there are couple of class/file names that need to be changed.</span></span>

<span data-ttu-id="7522b-156">"CP" 접두사가 붙은 모든 클래스의 이름이 "AE"로 바뀌었습니다.</span><span class="sxs-lookup"><span data-stu-id="7522b-156">All classes prefixed with "CP" are renamed with "AE" prefix.</span></span>

<span data-ttu-id="7522b-157">예제:</span><span class="sxs-lookup"><span data-stu-id="7522b-157">Example:</span></span>

* <span data-ttu-id="7522b-158">`CPModule.h`의 이름이 `AEModule.h`(으)로 바뀌었습니다.</span><span class="sxs-lookup"><span data-stu-id="7522b-158">`CPModule.h` is renamed to `AEModule.h`.</span></span>

<span data-ttu-id="7522b-159">"Capptain" 접두사가 붙은 모든 클래스의 이름이 "Engagement"로 바뀌었습니다.</span><span class="sxs-lookup"><span data-stu-id="7522b-159">All classes prefixed with "Capptain" are renamed with "Engagement" prefix.</span></span>

<span data-ttu-id="7522b-160">예제:</span><span class="sxs-lookup"><span data-stu-id="7522b-160">Examples:</span></span>

* <span data-ttu-id="7522b-161">클래스 `CapptainAgent`의 이름은 `EngagementAgent`(으)로 바뀌었습니다.</span><span class="sxs-lookup"><span data-stu-id="7522b-161">The class `CapptainAgent` is renamed to `EngagementAgent`.</span></span>
* <span data-ttu-id="7522b-162">클래스 `CapptainTableViewController`의 이름은 `EngagementTableViewController`(으)로 바뀌었습니다.</span><span class="sxs-lookup"><span data-stu-id="7522b-162">The class `CapptainTableViewController` is renamed to `EngagementTableViewController`.</span></span>
* <span data-ttu-id="7522b-163">클래스 `CapptainUtils`의 이름은 `EngagementUtils`(으)로 바뀌었습니다.</span><span class="sxs-lookup"><span data-stu-id="7522b-163">The class `CapptainUtils` is renamed to `EngagementUtils`.</span></span>
* <span data-ttu-id="7522b-164">클래스 `CapptainViewController`의 이름은 `EngagementViewController`(으)로 바뀌었습니다.</span><span class="sxs-lookup"><span data-stu-id="7522b-164">The class `CapptainViewController` is renamed to `EngagementViewController`.</span></span>


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
# <a name="get-started-with-azure-mobile-engagement-for-ios-apps-in-objective-c"></a><span data-ttu-id="e0eb1-103">Objective C에서 iOS 앱용 Azure Mobile Engagement 시작</span><span class="sxs-lookup"><span data-stu-id="e0eb1-103">Get Started with Azure Mobile Engagement for iOS apps in Objective C</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="e0eb1-104">이 항목에서는 Azure Mobile Engagement toounderstand toouse 응용 프로그램 사용 및 송신 푸시 알림 toosegmented 사용자 tooan iOS 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="e0eb1-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and send push notifications toosegmented users tooan iOS application.</span></span>
<span data-ttu-id="e0eb1-105">이 자습서에서는 기본 데이터를 수집하고 APNS(Apple 푸시 알림 시스템)를 사용하여 푸시 알림을 받는 빈 iOS 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e0eb1-105">In this tutorial, you create a blank iOS app that collects basic data and receives push notifications using Apple Push Notification System (APNS).</span></span>

<span data-ttu-id="e0eb1-106">이 자습서는 hello 다음을 사항이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e0eb1-106">This tutorial requires hello following:</span></span>

* <span data-ttu-id="e0eb1-107">MAC 앱 스토어에서 설치할 수 있는 XCode 8</span><span class="sxs-lookup"><span data-stu-id="e0eb1-107">XCode 8, which you can install from your MAC App Store</span></span>
* <span data-ttu-id="e0eb1-108">hello [Mobile Engagement iOS SDK]</span><span class="sxs-lookup"><span data-stu-id="e0eb1-108">hello [Mobile Engagement iOS SDK]</span></span>

<span data-ttu-id="e0eb1-109">이 자습서를 완료해야 다른 모든 iOS 앱용 Mobile Engagement 자습서를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0eb1-109">Completing this tutorial is a prerequisite for all other Mobile Engagement tutorials for iOS apps.</span></span>

> [!NOTE]
> <span data-ttu-id="e0eb1-110">toocomplete이이 자습서에서는 활성 Azure 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0eb1-110">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="e0eb1-111">계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0eb1-111">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="e0eb1-112">자세한 내용은 [Azure 평가판](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-get-started)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e0eb1-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-get-started).</span></span>
>
>

## <span data-ttu-id="e0eb1-113"><a id="setup-azme"></a>iOS 앱용 Mobile Engagement 설정</span><span class="sxs-lookup"><span data-stu-id="e0eb1-113"><a id="setup-azme"></a>Setup Mobile Engagement for your iOS app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="e0eb1-114"><a id="connecting-app"></a>응용 프로그램 toohello Mobile Engagement 백 엔드 연결</span><span class="sxs-lookup"><span data-stu-id="e0eb1-114"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="e0eb1-115">이 자습서는 기본적인 "통합", 최소 hello 필요한 toocollect 데이터 설정 되 고 푸시 알림을 보내는 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0eb1-115">This tutorial presents a "basic integration", which is hello minimal set required toocollect data and send a push notification.</span></span> <span data-ttu-id="e0eb1-116">hello에 hello 완벽 한 통합 설명서를 확인할 수 있습니다 [Mobile Engagement iOS SDK 통합](mobile-engagement-ios-sdk-overview.md)</span><span class="sxs-lookup"><span data-stu-id="e0eb1-116">hello complete integration documentation can be found in hello [Mobile Engagement iOS SDK integration](mobile-engagement-ios-sdk-overview.md)</span></span>

<span data-ttu-id="e0eb1-117">XCode toodemonstrate hello 통합 기본 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e0eb1-117">We will create a basic app with XCode toodemonstrate hello integration.</span></span>

### <a name="create-a-new-ios-project"></a><span data-ttu-id="e0eb1-118">새 iOS 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="e0eb1-118">Create a new iOS project</span></span>
[!INCLUDE [Create a new iOS Project](../../includes/mobile-engagement-create-new-ios-app.md)]

### <a name="connect-your-app-toohello-mobile-engagement-backend"></a><span data-ttu-id="e0eb1-119">응용 프로그램 toohello Mobile Engagement 백 엔드 연결</span><span class="sxs-lookup"><span data-stu-id="e0eb1-119">Connect your app toohello Mobile Engagement backend</span></span>
1. <span data-ttu-id="e0eb1-120">Hello 다운로드 [Mobile Engagement iOS SDK]합니다.</span><span class="sxs-lookup"><span data-stu-id="e0eb1-120">Download hello [Mobile Engagement iOS SDK].</span></span>
2. <span data-ttu-id="e0eb1-121">Hello를 추출 합니다. 컴퓨터에 tar.gz 파일 tooa 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="e0eb1-121">Extract hello .tar.gz file tooa folder in your computer.</span></span>
3. <span data-ttu-id="e0eb1-122">Hello 프로젝트를 마우스 오른쪽 단추로 클릭 한 다음 선택 **파일을 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="e0eb1-122">Right-click hello project, and then select **Add files to**.</span></span>

    ![][1]
4. <span data-ttu-id="e0eb1-123">Hello SDK의 압축을 푼 toohello 폴더를 탐색, hello 선택 `EngagementSDK` 폴더를 클릭 하 여 **옵션** 왼쪽된 아래 모서리 hello 되 고 해당 hello 확인란이 있는지 확인 **필요한 경우 항목을 복사할** 및 hello 대상에 대 한 확인란 확인 한 다음 키를 눌러 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="e0eb1-123">Navigate toohello folder where you extracted hello SDK, select hello `EngagementSDK` folder, click **Options** on hello bottom left corner and make sure that hello checkbox **Copy items if needed** and hello checkbox for your target are checked then press **OK**.</span></span>

    ![][2]
5. <span data-ttu-id="e0eb1-124">열기 hello **빌드 단계** 탭 및 hello **링크 이진 파일과 라이브러리** 메뉴에서 다음과 같이 hello 프레임 워크를 추가:</span><span class="sxs-lookup"><span data-stu-id="e0eb1-124">Open hello **Build Phases** tab, and in hello **Link Binary With Libraries** menu, add hello frameworks as shown below:</span></span>

    ![][3]
6. <span data-ttu-id="e0eb1-125">Azure 포털에서 앱의 toohello 돌아가서 **연결 정보입니다.** 페이지 및 복사 hello 연결 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="e0eb1-125">Go back toohello Azure portal in your app's **Connection Info** page and copy hello connection string.</span></span>

    ![][4]
7. <span data-ttu-id="e0eb1-126">Hello 다음에 코드 줄을 추가 하면 **AppDelegate.m** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e0eb1-126">Add hello following line of code in your **AppDelegate.m** file.</span></span>

        #import "EngagementAgent.h"
8. <span data-ttu-id="e0eb1-127">이제 hello에 hello 연결 문자열을 붙여 `didFinishLaunchingWithOptions` 위임 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0eb1-127">Now paste hello connection string in hello `didFinishLaunchingWithOptions` delegate.</span></span>

        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
        {
              [...]   
              [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];
              [...]
        }
9. <span data-ttu-id="e0eb1-128">`setTestLogEnabled`하면 tooidentify 문제에 대 한 SDK 로그 수 있도록 하는 선택적 문이입니다.</span><span class="sxs-lookup"><span data-stu-id="e0eb1-128">`setTestLogEnabled` is an optional statement which enables SDK logs for you tooidentify issues.</span></span>

## <span data-ttu-id="e0eb1-129"><a id="monitor"></a>실시간 모니터링 사용</span><span class="sxs-lookup"><span data-stu-id="e0eb1-129"><a id="monitor"></a>Enable real-time monitoring</span></span>
<span data-ttu-id="e0eb1-130">순서 toostart 데이터를 보내고는 hello 사용자가 활성화 되도록 하나 이상 화면 (활동) toohello Mobile Engagement 백 엔드를 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0eb1-130">In order toostart sending data and ensuring that hello users are active, you must send at least one screen (Activity) toohello Mobile Engagement backend.</span></span>

1. <span data-ttu-id="e0eb1-131">열기 hello **ViewController.h** 파일 및 가져오기 **EngagementViewController.h**:</span><span class="sxs-lookup"><span data-stu-id="e0eb1-131">Open hello **ViewController.h** file and import **EngagementViewController.h**:</span></span>

    `#import "EngagementViewController.h"`
2. <span data-ttu-id="e0eb1-132">이제 hello의 hello 슈퍼 클래스를 대체 **ViewController** 하 여 인터페이스 `EngagementViewController`:</span><span class="sxs-lookup"><span data-stu-id="e0eb1-132">Now replace hello super class of hello **ViewController** interface by `EngagementViewController`:</span></span>

    `@interface ViewController : EngagementViewController`

## <span data-ttu-id="e0eb1-133"><a id="monitor"></a>실시간 모니터링과 앱 연결</span><span class="sxs-lookup"><span data-stu-id="e0eb1-133"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="e0eb1-134"><a id="integrate-push"></a>푸시 알림 및 앱 내 메시징 사용</span><span class="sxs-lookup"><span data-stu-id="e0eb1-134"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="e0eb1-135">Mobile Engagement 사용 하면 사용자와 toointeract 및 도달 범위 푸시 알림과 앱 내 메시징을 캠페인의 hello 컨텍스트에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0eb1-135">Mobile Engagement allows you toointeract with your users and REACH with push notifications and in-app messaging in hello context of campaigns.</span></span> <span data-ttu-id="e0eb1-136">이 모듈에는 hello Mobile engagement 연결 포털에서 REACH를 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0eb1-136">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="e0eb1-137">hello 다음 섹션에서는 앱 tooreceive를 속성을 설정.</span><span class="sxs-lookup"><span data-stu-id="e0eb1-137">hello following sections set up your app tooreceive them.</span></span>

### <a name="enable-your-app-tooreceive-silent-push-notifications"></a><span data-ttu-id="e0eb1-138">사용자 앱 tooreceive 자동 푸시 알림을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="e0eb1-138">Enable your app tooreceive Silent Push Notifications</span></span>
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

### <a name="add-hello-reach-library-tooyour-project"></a><span data-ttu-id="e0eb1-139">Hello Reach 라이브러리 tooyour 프로젝트 추가</span><span class="sxs-lookup"><span data-stu-id="e0eb1-139">Add hello Reach library tooyour project</span></span>
1. <span data-ttu-id="e0eb1-140">프로젝트를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0eb1-140">Right-click your project.</span></span>
2. <span data-ttu-id="e0eb1-141">**파일 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e0eb1-141">Select **Add file to**.</span></span>
3. <span data-ttu-id="e0eb1-142">Hello SDK의 압축을 푼 toohello 폴더를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0eb1-142">Navigate toohello folder where you extracted hello SDK.</span></span>
4. <span data-ttu-id="e0eb1-143">선택 hello `EngagementReach` 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="e0eb1-143">Select hello `EngagementReach` folder.</span></span>
5. <span data-ttu-id="e0eb1-144">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0eb1-144">Click **Add**.</span></span>

### <a name="modify-your-application-delegate"></a><span data-ttu-id="e0eb1-145">응용 프로그램 대리자 수정</span><span class="sxs-lookup"><span data-stu-id="e0eb1-145">Modify your Application Delegate</span></span>
1. <span data-ttu-id="e0eb1-146">다시 **AppDeletegate.m** 파일, hello Engagement Reach 모듈을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e0eb1-146">Back in **AppDeletegate.m** file, import hello Engagement Reach module.</span></span>

        #import "AEReachModule.h"
        #import <UserNotifications/UserNotifications.h>
2. <span data-ttu-id="e0eb1-147">내부 hello `application:didFinishLaunchingWithOptions` Reach 모듈 만들고 메서드와 tooyour 기존 Engagement 초기화 줄을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0eb1-147">Inside hello `application:didFinishLaunchingWithOptions` method, create a Reach module and pass it tooyour existing Engagement initialization line:</span></span>

        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
            AEReachModule * reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
            [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
            [...]
            return YES;
        }

### <a name="enable-your-app-tooreceive-apns-push-notifications"></a><span data-ttu-id="e0eb1-148">사용자 응용 프로그램 tooreceive APNS 푸시 알림을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="e0eb1-148">Enable your app tooreceive APNS Push Notifications</span></span>
1. <span data-ttu-id="e0eb1-149">다음 줄 toohello hello 추가 `application:didFinishLaunchingWithOptions` 메서드:</span><span class="sxs-lookup"><span data-stu-id="e0eb1-149">Add hello following line toohello `application:didFinishLaunchingWithOptions` method:</span></span>

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
2. <span data-ttu-id="e0eb1-150">Hello 추가 `application:didRegisterForRemoteNotificationsWithDeviceToken` 메서드를 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0eb1-150">Add hello `application:didRegisterForRemoteNotificationsWithDeviceToken` method as follows:</span></span>

        - (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
        {
             [[EngagementAgent shared] registerDeviceToken:deviceToken];
            NSLog(@"Registered Token: %@", deviceToken);
        }
3. <span data-ttu-id="e0eb1-151">Hello 추가 `didFailToRegisterForRemoteNotificationsWithError` 메서드를 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0eb1-151">Add hello `didFailToRegisterForRemoteNotificationsWithError` method as follows:</span></span>

        - (void)application:(UIApplication*)application didFailToRegisterForRemoteNotificationsWithError:(NSError*)error
        {
           NSLog(@"Failed tooget token, error: %@", error);
        }
4. <span data-ttu-id="e0eb1-152">Hello 추가 `didReceiveRemoteNotification:fetchCompletionHandler` 메서드를 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0eb1-152">Add hello `didReceiveRemoteNotification:fetchCompletionHandler` method as follows:</span></span>

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

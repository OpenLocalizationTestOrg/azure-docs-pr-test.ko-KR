---
title: "Objective C에서 iOS용 Azure Mobile Engagement 시작 | Microsoft Docs"
description: "iOS 앱에 대해 분석 및 푸시 알림과 함께 Azure Mobile Engagement를 사용하는 방법을 알아봅니다."
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
ms.openlocfilehash: 1b87a2ebb35b31ee3d3139ecead6267e62eb1033
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-ios-apps-in-objective-c"></a><span data-ttu-id="37e05-103">Objective C에서 iOS 앱용 Azure Mobile Engagement 시작</span><span class="sxs-lookup"><span data-stu-id="37e05-103">Get Started with Azure Mobile Engagement for iOS apps in Objective C</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="37e05-104">이 항목에서는 Azure Mobile Engagement를 사용하여 앱 사용법을 이해하고 iOS 응용 프로그램의 분할된 사용자에게 푸시 알림을 보내는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="37e05-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and send push notifications to segmented users to an iOS application.</span></span>
<span data-ttu-id="37e05-105">이 자습서에서는 기본 데이터를 수집하고 APNS(Apple 푸시 알림 시스템)를 사용하여 푸시 알림을 받는 빈 iOS 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="37e05-105">In this tutorial, you create a blank iOS app that collects basic data and receives push notifications using Apple Push Notification System (APNS).</span></span>

<span data-ttu-id="37e05-106">이 자습서를 사용하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="37e05-106">This tutorial requires the following:</span></span>

* <span data-ttu-id="37e05-107">MAC 앱 스토어에서 설치할 수 있는 XCode 8</span><span class="sxs-lookup"><span data-stu-id="37e05-107">XCode 8, which you can install from your MAC App Store</span></span>
* <span data-ttu-id="37e05-108">[Mobile Engagement iOS SDK]</span><span class="sxs-lookup"><span data-stu-id="37e05-108">the [Mobile Engagement iOS SDK]</span></span>

<span data-ttu-id="37e05-109">이 자습서를 완료해야 다른 모든 iOS 앱용 Mobile Engagement 자습서를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37e05-109">Completing this tutorial is a prerequisite for all other Mobile Engagement tutorials for iOS apps.</span></span>

> [!NOTE]
> <span data-ttu-id="37e05-110">이 자습서를 완료하려면 활성 Azure 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="37e05-110">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="37e05-111">계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37e05-111">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="37e05-112">자세한 내용은 [Azure 평가판](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-get-started)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="37e05-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-get-started).</span></span>
>
>

## <span data-ttu-id="37e05-113"><a id="setup-azme"></a>iOS 앱용 Mobile Engagement 설정</span><span class="sxs-lookup"><span data-stu-id="37e05-113"><a id="setup-azme"></a>Setup Mobile Engagement for your iOS app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="37e05-114"><a id="connecting-app"></a>Mobile Engagement 백 엔드에 앱 연결</span><span class="sxs-lookup"><span data-stu-id="37e05-114"><a id="connecting-app"></a>Connect your app to the Mobile Engagement backend</span></span>
<span data-ttu-id="37e05-115">이 자습서에서는 데이터를 수집하고 푸시 알림을 보내는 데 필요한 최소 집합인 "기본 통합" 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="37e05-115">This tutorial presents a "basic integration", which is the minimal set required to collect data and send a push notification.</span></span> <span data-ttu-id="37e05-116">전체 통합 설명서는 [Mobile Engagement iOS SDK 통합](mobile-engagement-ios-sdk-overview.md)</span><span class="sxs-lookup"><span data-stu-id="37e05-116">The complete integration documentation can be found in the [Mobile Engagement iOS SDK integration](mobile-engagement-ios-sdk-overview.md)</span></span>

<span data-ttu-id="37e05-117">여기서는 통합을 시연하기 위해 XCode를 사용하여 기본적인 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="37e05-117">We will create a basic app with XCode to demonstrate the integration.</span></span>

### <a name="create-a-new-ios-project"></a><span data-ttu-id="37e05-118">새 iOS 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="37e05-118">Create a new iOS project</span></span>
[!INCLUDE [Create a new iOS Project](../../includes/mobile-engagement-create-new-ios-app.md)]

### <a name="connect-your-app-to-the-mobile-engagement-backend"></a><span data-ttu-id="37e05-119">Mobile Engagement 백 엔드에 앱 연결</span><span class="sxs-lookup"><span data-stu-id="37e05-119">Connect your app to the Mobile Engagement backend</span></span>
1. <span data-ttu-id="37e05-120">[Mobile Engagement iOS SDK]를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="37e05-120">Download the [Mobile Engagement iOS SDK].</span></span>
2. <span data-ttu-id="37e05-121">컴퓨터의 폴더에 .tar.gz 파일의 압축을 풉니다.</span><span class="sxs-lookup"><span data-stu-id="37e05-121">Extract the .tar.gz file to a folder in your computer.</span></span>
3. <span data-ttu-id="37e05-122">프로젝트를 마우스 오른쪽 단추로 클릭하고 **파일 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="37e05-122">Right-click the project, and then select **Add files to**.</span></span>

    ![][1]
4. <span data-ttu-id="37e05-123">SDK를 추출한 폴더로 이동하고 `EngagementSDK` 폴더를 선택하고 왼쪽 아래 모퉁이에 있는 **옵션**을 클릭하고 **필요한 경우 항목 복사** 확인란 및 대상의 확인란을 선택했는지 확인한 다음 **확인**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="37e05-123">Navigate to the folder where you extracted the SDK, select the `EngagementSDK` folder, click **Options** on the bottom left corner and make sure that the checkbox **Copy items if needed** and the checkbox for your target are checked then press **OK**.</span></span>

    ![][2]
5. <span data-ttu-id="37e05-124">**빌드 단계** 탭을 열고 **이진 파일과 라이브러리 연결** 메뉴에서 아래와 같이 프레임워크를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="37e05-124">Open the **Build Phases** tab, and in the **Link Binary With Libraries** menu, add the frameworks as shown below:</span></span>

    ![][3]
6. <span data-ttu-id="37e05-125">Azure 포털의 앱 **연결 정보** 페이지로 돌아가서 연결 문자열을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="37e05-125">Go back to the Azure portal in your app's **Connection Info** page and copy the connection string.</span></span>

    ![][4]
7. <span data-ttu-id="37e05-126">**AppDelegate.m** 파일에 다음 코드 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="37e05-126">Add the following line of code in your **AppDelegate.m** file.</span></span>

        #import "EngagementAgent.h"
8. <span data-ttu-id="37e05-127">이제 연결 문자열을 `didFinishLaunchingWithOptions` 대리자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="37e05-127">Now paste the connection string in the `didFinishLaunchingWithOptions` delegate.</span></span>

        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
        {
              [...]   
              [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];
              [...]
        }
9. <span data-ttu-id="37e05-128">`setTestLogEnabled`는 SDK 로그를 통해 문제를 식별할 수 있도록 하는 선택적 문입니다.</span><span class="sxs-lookup"><span data-stu-id="37e05-128">`setTestLogEnabled` is an optional statement which enables SDK logs for you to identify issues.</span></span>

## <span data-ttu-id="37e05-129"><a id="monitor"></a>실시간 모니터링 사용</span><span class="sxs-lookup"><span data-stu-id="37e05-129"><a id="monitor"></a>Enable real-time monitoring</span></span>
<span data-ttu-id="37e05-130">데이터 보내기를 시작하고 사용자가 활성 상태인지 확인하려면 Mobile Engagement 백 엔드에 화면(활동)을 하나 이상 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="37e05-130">In order to start sending data and ensuring that the users are active, you must send at least one screen (Activity) to the Mobile Engagement backend.</span></span>

1. <span data-ttu-id="37e05-131">**ViewController.h** 파일을 열고 **EngagementViewController.h**를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="37e05-131">Open the **ViewController.h** file and import **EngagementViewController.h**:</span></span>

    `#import "EngagementViewController.h"`
2. <span data-ttu-id="37e05-132">이제 **ViewController** 인터페이스의 상위 클래스를 `EngagementViewController`로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="37e05-132">Now replace the super class of the **ViewController** interface by `EngagementViewController`:</span></span>

    `@interface ViewController : EngagementViewController`

## <span data-ttu-id="37e05-133"><a id="monitor"></a>실시간 모니터링과 앱 연결</span><span class="sxs-lookup"><span data-stu-id="37e05-133"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="37e05-134"><a id="integrate-push"></a>푸시 알림 및 앱 내 메시징 사용</span><span class="sxs-lookup"><span data-stu-id="37e05-134"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="37e05-135">Mobile Engagement에서는 캠페인 컨텍스트에서 푸시 알림 및 앱 내 메시징을 사용하여 사용자 및 도달률과 상호 작용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37e05-135">Mobile Engagement allows you to interact with your users and REACH with push notifications and in-app messaging in the context of campaigns.</span></span> <span data-ttu-id="37e05-136">Mobile Engagement 포털에서는 이 모듈을 도달률이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="37e05-136">This module is called REACH in the Mobile Engagement portal.</span></span>
<span data-ttu-id="37e05-137">다음 섹션에서는 이러한 알림과 메시지를 받도록 앱을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="37e05-137">The following sections set up your app to receive them.</span></span>

### <a name="enable-your-app-to-receive-silent-push-notifications"></a><span data-ttu-id="37e05-138">앱이 자동 푸시 알림을 받을 수 있도록 설정</span><span class="sxs-lookup"><span data-stu-id="37e05-138">Enable your app to receive Silent Push Notifications</span></span>
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

### <a name="add-the-reach-library-to-your-project"></a><span data-ttu-id="37e05-139">프로젝트에 도달률 라이브러리 추가</span><span class="sxs-lookup"><span data-stu-id="37e05-139">Add the Reach library to your project</span></span>
1. <span data-ttu-id="37e05-140">프로젝트를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="37e05-140">Right-click your project.</span></span>
2. <span data-ttu-id="37e05-141">**파일 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="37e05-141">Select **Add file to**.</span></span>
3. <span data-ttu-id="37e05-142">SDK를 추출한 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="37e05-142">Navigate to the folder where you extracted the SDK.</span></span>
4. <span data-ttu-id="37e05-143">`EngagementReach` 폴더를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="37e05-143">Select the `EngagementReach` folder.</span></span>
5. <span data-ttu-id="37e05-144">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="37e05-144">Click **Add**.</span></span>

### <a name="modify-your-application-delegate"></a><span data-ttu-id="37e05-145">응용 프로그램 대리자 수정</span><span class="sxs-lookup"><span data-stu-id="37e05-145">Modify your Application Delegate</span></span>
1. <span data-ttu-id="37e05-146">**AppDeletegate.m** 파일로 돌아가서 Engagement 도달률 모듈을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="37e05-146">Back in **AppDeletegate.m** file, import the Engagement Reach module.</span></span>

        #import "AEReachModule.h"
        #import <UserNotifications/UserNotifications.h>
2. <span data-ttu-id="37e05-147">다음과 같이 `application:didFinishLaunchingWithOptions` 메서드 내에서 도달률 모듈을 만든 다음 기존 Engagement 초기화 줄에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="37e05-147">Inside the `application:didFinishLaunchingWithOptions` method, create a Reach module and pass it to your existing Engagement initialization line:</span></span>

        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
            AEReachModule * reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
            [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
            [...]
            return YES;
        }

### <a name="enable-your-app-to-receive-apns-push-notifications"></a><span data-ttu-id="37e05-148">앱이 APNS 푸시 알림을 받을 수 있도록 설정</span><span class="sxs-lookup"><span data-stu-id="37e05-148">Enable your app to receive APNS Push Notifications</span></span>
1. <span data-ttu-id="37e05-149">다음 줄을 `application:didFinishLaunchingWithOptions` 메서드에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="37e05-149">Add the following line to the `application:didFinishLaunchingWithOptions` method:</span></span>

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
2. <span data-ttu-id="37e05-150">다음과 같이 `application:didRegisterForRemoteNotificationsWithDeviceToken` 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="37e05-150">Add the `application:didRegisterForRemoteNotificationsWithDeviceToken` method as follows:</span></span>

        - (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
        {
             [[EngagementAgent shared] registerDeviceToken:deviceToken];
            NSLog(@"Registered Token: %@", deviceToken);
        }
3. <span data-ttu-id="37e05-151">다음과 같이 `didFailToRegisterForRemoteNotificationsWithError` 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="37e05-151">Add the `didFailToRegisterForRemoteNotificationsWithError` method as follows:</span></span>

        - (void)application:(UIApplication*)application didFailToRegisterForRemoteNotificationsWithError:(NSError*)error
        {
           NSLog(@"Failed to get token, error: %@", error);
        }
4. <span data-ttu-id="37e05-152">다음과 같이 `didReceiveRemoteNotification:fetchCompletionHandler` 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="37e05-152">Add the `didReceiveRemoteNotification:fetchCompletionHandler` method as follows:</span></span>

        - (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
        {
            [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:handler];
        }

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- URLs. -->
<span data-ttu-id="37e05-153">[Mobile Engagement iOS SDK]: http://aka.ms/qk2rnj</span><span class="sxs-lookup"><span data-stu-id="37e05-153">[Mobile Engagement iOS SDK]: http://aka.ms/qk2rnj</span></span>

<!-- Images. -->
[1]: ./media/mobile-engagement-ios-get-started/xcode-add-files.png
[2]: ./media/mobile-engagement-ios-get-started/xcode-select-engagement-sdk.png
[3]: ./media/mobile-engagement-ios-get-started/xcode-build-phases.png
[4]: ./media/mobile-engagement-ios-get-started/app-connection-info-page.png

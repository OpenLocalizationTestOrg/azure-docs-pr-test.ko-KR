---
title: "Swift에서 iOS용 Azure Mobile Engagement 시작 | Microsoft Docs"
description: "iOS 앱에 대해 분석 및 푸시 알림과 함께 Azure Mobile Engagement를 사용하는 방법을 알아봅니다."
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 196c282d-6f2f-4cbc-aeee-6517c5ad866d
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: swift
ms.topic: hero-article
ms.date: 09/20/2016
ms.author: piyushjo
ms.openlocfilehash: 1011b9823333e79a52cd2d187df4f8d063b1f799
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-ios-apps-in-swift"></a><span data-ttu-id="3d925-103">Swift에서 iOS 앱용 Azure Mobile Engagement 시작</span><span class="sxs-lookup"><span data-stu-id="3d925-103">Get Started with Azure Mobile Engagement for iOS Apps in Swift</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="3d925-104">이 항목에서는 Azure Mobile Engagement를 사용하여 앱 사용법을 이해하고 iOS 응용 프로그램의 분할된 사용자에게 푸시 알림을 보내는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3d925-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and send push notifications to segmented users to an iOS application.</span></span>
<span data-ttu-id="3d925-105">이 자습서에서는 기본 데이터를 수집하고 APNS(Apple 푸시 알림 시스템)를 사용하여 푸시 알림을 받는 빈 iOS 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3d925-105">In this tutorial, you create a blank iOS app that collects basic data and receives push notifications using Apple Push Notification System (APNS).</span></span>

<span data-ttu-id="3d925-106">이 자습서를 사용하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3d925-106">This tutorial requires the following:</span></span>

* <span data-ttu-id="3d925-107">MAC 앱 스토어에서 설치할 수 있는 XCode 8</span><span class="sxs-lookup"><span data-stu-id="3d925-107">XCode 8, which you can install from your MAC App Store</span></span>
* <span data-ttu-id="3d925-108">[Mobile Engagement iOS SDK]</span><span class="sxs-lookup"><span data-stu-id="3d925-108">the [Mobile Engagement iOS SDK]</span></span>
* <span data-ttu-id="3d925-109">Apple 개발자 센터에서 가져올 수 있는 푸시 알림 인증서(.p12)</span><span class="sxs-lookup"><span data-stu-id="3d925-109">Push notification certificate (.p12) that you can obtain on your Apple Dev Center</span></span>

> [!NOTE]
> <span data-ttu-id="3d925-110">이 자습서에서는 Swift 버전 3.0을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3d925-110">This tutorial uses Swift version 3.0.</span></span> 
> 
> 

<span data-ttu-id="3d925-111">이 자습서를 완료해야 다른 모든 iOS 앱용 Mobile Engagement 자습서를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d925-111">Completing this tutorial is a prerequisite for all other Mobile Engagement tutorials for iOS apps.</span></span>

> [!NOTE]
> <span data-ttu-id="3d925-112">이 자습서를 완료하려면 활성 Azure 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d925-112">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="3d925-113">계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d925-113">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="3d925-114">자세한 내용은 [Azure 평가판](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-swift-get-started)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3d925-114">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-swift-get-started).</span></span>
> 
> 

## <span data-ttu-id="3d925-115"><a id="setup-azme"></a>iOS 앱용 Mobile Engagement 설정</span><span class="sxs-lookup"><span data-stu-id="3d925-115"><a id="setup-azme"></a>Setup Mobile Engagement for your iOS app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="3d925-116"><a id="connecting-app"></a>Mobile Engagement 백 엔드에 앱 연결</span><span class="sxs-lookup"><span data-stu-id="3d925-116"><a id="connecting-app"></a>Connect your app to the Mobile Engagement backend</span></span>
<span data-ttu-id="3d925-117">이 자습서에서는 데이터를 수집하고 푸시 알림을 보내는 데 필요한 최소 집합인 "기본 통합" 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3d925-117">This tutorial presents a "basic integration", which is the minimal set required to collect data and send a push notification.</span></span> <span data-ttu-id="3d925-118">전체 통합 설명서는 [Mobile Engagement iOS SDK 통합](mobile-engagement-ios-sdk-overview.md)</span><span class="sxs-lookup"><span data-stu-id="3d925-118">The complete integration documentation can be found in the [Mobile Engagement iOS SDK integration](mobile-engagement-ios-sdk-overview.md)</span></span>

<span data-ttu-id="3d925-119">여기서는 통합을 시연하기 위해 XCode를 사용하여 기본적인 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3d925-119">We will create a basic app with XCode to demonstrate the integration:</span></span>

### <a name="create-a-new-ios-project"></a><span data-ttu-id="3d925-120">새 iOS 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="3d925-120">Create a new iOS project</span></span>
[!INCLUDE [Create a new iOS Project](../../includes/mobile-engagement-create-new-ios-app.md)]

### <a name="connect-your-app-to-mobile-engagement-backend"></a><span data-ttu-id="3d925-121">Mobile Engagement 백 엔드에 앱 연결</span><span class="sxs-lookup"><span data-stu-id="3d925-121">Connect your app to Mobile Engagement backend</span></span>
1. <span data-ttu-id="3d925-122">[Mobile Engagement iOS SDK]</span><span class="sxs-lookup"><span data-stu-id="3d925-122">Download the [Mobile Engagement iOS SDK]</span></span>
2. <span data-ttu-id="3d925-123">.tar.gz 파일을 컴퓨터의 폴더로 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="3d925-123">Extract the .tar.gz file to a folder in your computer</span></span>
3. <span data-ttu-id="3d925-124">프로젝트를 마우스 오른쪽 단추로 클릭하고 "파일을 추가할 위치..."를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3d925-124">Right click the project and select "Add files to ..."</span></span>
   
    ![][1]
4. <span data-ttu-id="3d925-125">SDK를 추출한 폴더로 이동하고 `EngagementSDK` 폴더를 선택한 후 확인을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="3d925-125">Navigate to the folder where you extracted the SDK and select the `EngagementSDK` folder then press OK.</span></span>
   
    ![][2]
5. <span data-ttu-id="3d925-126">`Build Phases` 탭을 열고 `Link Binary With Libraries` 메뉴에서 아래와 같이 프레임워크를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3d925-126">Open the `Build Phases` tab and in the `Link Binary With Libraries` menu add the frameworks as shown below:</span></span>
   
    ![][3]
6. <span data-ttu-id="3d925-127">파일 > 새로 만들기 > 파일 > iOS > 소스 > 헤더 파일을 선택하여 SDK의 Objective C API를 사용할 수 있도록 Bridging 헤더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3d925-127">Create a Bridging header to be able to use the SDK's Objective C APIs by choosing File > New > File > iOS > Source > Header File.</span></span>
   
    ![][4]
7. <span data-ttu-id="3d925-128">Mobile Engagement Objective-C 코드를 Swift 코드에 노출하도록 Bridging 헤더 파일을 편집하고 다음 import를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3d925-128">Edit the bridging header file to expose Mobile Engagement Objective-C code to your Swift code, add the following imports :</span></span>
   
        /* Mobile Engagement Agent */
        #import "AEModule.h"
        #import "AEPushMessage.h"
        #import "AEStorage.h"
        #import "EngagementAgent.h"
        #import "EngagementTableViewController.h"
        #import "EngagementViewController.h"
        #import "AEUserNotificationHandler.h"
        #import "AEIdfaProvider.h"
8. <span data-ttu-id="3d925-129">빌드 설정에서 Swift 컴파일러 - 코드 생성 아래의 Objective-C Bridging 헤더 빌드 설정에 이 헤더에 대한 경로가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3d925-129">Under Build Settings, make sure the Objective-C Bridging Header build setting under Swift Compiler - Code Generation has a path to this header.</span></span> <span data-ttu-id="3d925-130">다음은 경로 예입니다. **$(SRCROOT)/MySuperApp/MySuperApp-Bridging-Header.h (경로에 따라 다름)**</span><span class="sxs-lookup"><span data-stu-id="3d925-130">Here is a path example: **$(SRCROOT)/MySuperApp/MySuperApp-Bridging-Header.h (depending on the path)**</span></span>
   
   ![][6]
9. <span data-ttu-id="3d925-131">Azure 포털의 앱 *연결 정보* 페이지로 돌아가서 연결 문자열을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="3d925-131">Go back to the Azure portal in your app's *Connection Info* page and copy the Connection String</span></span>
   
   ![][5]
10. <span data-ttu-id="3d925-132">이제 연결 문자열을 `didFinishLaunchingWithOptions` 대리자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="3d925-132">Now paste the connection string in the `didFinishLaunchingWithOptions` delegate</span></span>
    
        func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool
        {
              [...]
                EngagementAgent.init("Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}")
              [...]
        }

## <span data-ttu-id="3d925-133"><a id="monitor"></a>실시간 모니터링 사용</span><span class="sxs-lookup"><span data-stu-id="3d925-133"><a id="monitor"></a>Enabling real-time monitoring</span></span>
<span data-ttu-id="3d925-134">데이터 보내기를 시작하고 사용자가 활성 상태인지 확인하려면 Mobile Engagement 백 엔드에 화면(활동)을 하나 이상 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d925-134">In order to start sending data and ensuring that the users are active, you must send at least one screen (Activity) to the Mobile Engagement backend.</span></span>

1. <span data-ttu-id="3d925-135">**ViewController.swift** 파일을 열고 **ViewController**의 기본 클래스를 **EngagementViewController**가 되도록 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3d925-135">Open the **ViewController.swift** file and replace the base class of **ViewController** to be **EngagementViewController**:</span></span>
   
    `class ViewController : EngagementViewController {`

## <span data-ttu-id="3d925-136"><a id="monitor"></a>실시간 모니터링과 앱 연결</span><span class="sxs-lookup"><span data-stu-id="3d925-136"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="3d925-137"><a id="integrate-push"></a>푸시 알림 및 앱 내 메시징 사용</span><span class="sxs-lookup"><span data-stu-id="3d925-137"><a id="integrate-push"></a>Enabling Push Notifications and in-app messaging</span></span>
<span data-ttu-id="3d925-138">Mobile Engagement에서는 캠페인 컨텍스트에서 푸시 알림 및 앱 내 메시징을 사용하여 사용자와 상호 작용하고 사용자에게 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d925-138">Mobile Engagement allows you to interact and REACH with your users with Push Notifications and In-app Messaging in the context of campaigns.</span></span> <span data-ttu-id="3d925-139">Mobile Engagement 포털에서는 이 모듈을 도달률이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d925-139">This module is called REACH in the Mobile Engagement portal.</span></span>
<span data-ttu-id="3d925-140">다음 섹션에서는 해당 알림과 메시지를 받도록 앱을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3d925-140">The following sections will setup your app to receive them.</span></span>

### <a name="enable-your-app-to-receive-silent-push-notifications"></a><span data-ttu-id="3d925-141">앱이 자동 푸시 알림을 받을 수 있도록 설정</span><span class="sxs-lookup"><span data-stu-id="3d925-141">Enable your app to receive Silent Push Notifications</span></span>
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

### <a name="add-the-reach-library-to-your-project"></a><span data-ttu-id="3d925-142">프로젝트에 도달률 라이브러리 추가</span><span class="sxs-lookup"><span data-stu-id="3d925-142">Add the Reach library to your project</span></span>
1. <span data-ttu-id="3d925-143">프로젝트를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3d925-143">Right click your project</span></span>
2. <span data-ttu-id="3d925-144">`Add file to ...`을(를) 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3d925-144">Select `Add file to ...`</span></span>
3. <span data-ttu-id="3d925-145">SDK를 추출한 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="3d925-145">Navigate to the folder where you extracted the SDK</span></span>
4. <span data-ttu-id="3d925-146">`EngagementReach` 폴더를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3d925-146">Select the `EngagementReach` folder</span></span>
5. <span data-ttu-id="3d925-147">추가를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3d925-147">Click Add</span></span>
6. <span data-ttu-id="3d925-148">Mobile Engagement Objective-C Reach 헤더를 노출하도록 Bridging 헤더 파일을 편집하고 다음 import를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3d925-148">Edit the bridging header file to expose Mobile Engagement Objective-C Reach headers and add the following imports :</span></span>
   
        /* Mobile Engagement Reach */
        #import "AEAnnouncementViewController.h"
        #import "AEAutorotateView.h"
        #import "AEContentViewController.h"
        #import "AEDefaultAnnouncementViewController.h"
        #import "AEDefaultNotifier.h"
        #import "AEDefaultPollViewController.h"
        #import "AEInteractiveContent.h"
        #import "AENotificationView.h"
        #import "AENotifier.h"
        #import "AEPollViewController.h"
        #import "AEReachAbstractAnnouncement.h"
        #import "AEReachAnnouncement.h"
        #import "AEReachContent.h"
        #import "AEReachDataPush.h"
        #import "AEReachDataPushDelegate.h"
        #import "AEReachModule.h"
        #import "AEReachNotifAnnouncement.h"
        #import "AEReachPoll.h"
        #import "AEReachPollQuestion.h"
        #import "AEViewControllerUtil.h"
        #import "AEWebAnnouncementJsBridge.h"

### <a name="modify-your-application-delegate"></a><span data-ttu-id="3d925-149">응용 프로그램 대리자 수정</span><span class="sxs-lookup"><span data-stu-id="3d925-149">Modify your Application Delegate</span></span>
1. <span data-ttu-id="3d925-150">다음과 같이 `didFinishLaunchingWithOptions` 내부에서 도달률 모듈을 생성하여 기존 참여 초기화 줄에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="3d925-150">Inside  the `didFinishLaunchingWithOptions` -  create a reach module and pass it to your existing Engagement initialization line:</span></span>
   
        func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool 
        {
            let reach = AEReachModule.module(withNotificationIcon: UIImage(named:"icon.png")) as! AEReachModule
            EngagementAgent.init("Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}", modulesArray:[reach])
            [...]
            return true
        }

### <a name="enable-your-app-to-receive-apns-push-notifications"></a><span data-ttu-id="3d925-151">앱이 APNS 푸시 알림을 받을 수 있도록 설정</span><span class="sxs-lookup"><span data-stu-id="3d925-151">Enable your app to receive APNS Push Notifications</span></span>
1. <span data-ttu-id="3d925-152">다음 줄을 `didFinishLaunchingWithOptions` 메서드에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3d925-152">Add the following line to the `didFinishLaunchingWithOptions` method:</span></span>
   
        if #available(iOS 8.0, *)
        {
            if #available(iOS 10.0, *)
            {
                UNUserNotificationCenter.current().requestAuthorization(options: [.alert, .badge, .sound]) { (granted, error) in }
            }else
            {
                let settings = UIUserNotificationSettings(types: [.alert, .badge, .sound], categories: nil)
                application.registerUserNotificationSettings(settings)
            }
            application.registerForRemoteNotifications()
        }
        else
        {
            application.registerForRemoteNotifications(matching: [.alert, .badge, .sound])
        }
2. <span data-ttu-id="3d925-153">다음과 같이 `didRegisterForRemoteNotificationsWithDeviceToken` 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3d925-153">Add the `didRegisterForRemoteNotificationsWithDeviceToken` method as follows:</span></span>
   
        func application(_ application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data) {
            EngagementAgent.shared().registerDeviceToken(deviceToken)
        }
3. <span data-ttu-id="3d925-154">다음과 같이 `didReceiveRemoteNotification:fetchCompletionHandler:` 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3d925-154">Add the `didReceiveRemoteNotification:fetchCompletionHandler:` method as follows:</span></span>
   
        func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any], fetchCompletionHandler completionHandler: @escaping (UIBackgroundFetchResult) -> Void) {
            EngagementAgent.shared().applicationDidReceiveRemoteNotification(userInfo, fetchCompletionHandler:completionHandler)
        }

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- URLs. -->
<span data-ttu-id="3d925-155">[Mobile Engagement iOS SDK]: http://aka.ms/qk2rnj</span><span class="sxs-lookup"><span data-stu-id="3d925-155">[Mobile Engagement iOS SDK]: http://aka.ms/qk2rnj</span></span>

<!-- Images. -->
[1]: ./media/mobile-engagement-ios-get-started/xcode-add-files.png
[2]: ./media/mobile-engagement-ios-get-started/xcode-select-engagement-sdk.png
[3]: ./media/mobile-engagement-ios-get-started/xcode-build-phases.png
[4]: ./media/mobile-engagement-ios-swift-get-started/add-header-file.png
[5]: ./media/mobile-engagement-ios-get-started/app-connection-info-page.png
[6]: ./media/mobile-engagement-ios-swift-get-started/add-bridging-header.png

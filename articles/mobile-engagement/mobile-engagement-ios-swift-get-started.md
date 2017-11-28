---
title: "iOS Swift에 대 한 Azure Mobile Engagement와 시작 됨 aaaGet | Microsoft Docs"
description: "자세한 내용은 방법 iOS 앱에 대 한 분석 및 푸시 알림을 사용 하 여 Azure Mobile Engagement toouse 합니다."
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
ms.openlocfilehash: 9a3841d305745f8b80c6b0c86aabe18e0c7c0e59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-ios-apps-in-swift"></a><span data-ttu-id="6fd2d-103">Swift에서 iOS 앱용 Azure Mobile Engagement 시작</span><span class="sxs-lookup"><span data-stu-id="6fd2d-103">Get Started with Azure Mobile Engagement for iOS Apps in Swift</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="6fd2d-104">이 항목에서는 Azure Mobile Engagement toounderstand toouse 응용 프로그램 사용 및 송신 푸시 알림 toosegmented 사용자 tooan iOS 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="6fd2d-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and send push notifications toosegmented users tooan iOS application.</span></span>
<span data-ttu-id="6fd2d-105">이 자습서에서는 기본 데이터를 수집하고 APNS(Apple 푸시 알림 시스템)를 사용하여 푸시 알림을 받는 빈 iOS 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6fd2d-105">In this tutorial, you create a blank iOS app that collects basic data and receives push notifications using Apple Push Notification System (APNS).</span></span>

<span data-ttu-id="6fd2d-106">이 자습서는 hello 다음을 사항이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd2d-106">This tutorial requires hello following:</span></span>

* <span data-ttu-id="6fd2d-107">MAC 앱 스토어에서 설치할 수 있는 XCode 8</span><span class="sxs-lookup"><span data-stu-id="6fd2d-107">XCode 8, which you can install from your MAC App Store</span></span>
* <span data-ttu-id="6fd2d-108">hello [Mobile Engagement iOS SDK]</span><span class="sxs-lookup"><span data-stu-id="6fd2d-108">hello [Mobile Engagement iOS SDK]</span></span>
* <span data-ttu-id="6fd2d-109">Apple 개발자 센터에서 가져올 수 있는 푸시 알림 인증서(.p12)</span><span class="sxs-lookup"><span data-stu-id="6fd2d-109">Push notification certificate (.p12) that you can obtain on your Apple Dev Center</span></span>

> [!NOTE]
> <span data-ttu-id="6fd2d-110">이 자습서에서는 Swift 버전 3.0을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd2d-110">This tutorial uses Swift version 3.0.</span></span> 
> 
> 

<span data-ttu-id="6fd2d-111">이 자습서를 완료해야 다른 모든 iOS 앱용 Mobile Engagement 자습서를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fd2d-111">Completing this tutorial is a prerequisite for all other Mobile Engagement tutorials for iOS apps.</span></span>

> [!NOTE]
> <span data-ttu-id="6fd2d-112">toocomplete이이 자습서에서는 활성 Azure 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd2d-112">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="6fd2d-113">계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fd2d-113">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="6fd2d-114">자세한 내용은 [Azure 평가판](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-swift-get-started)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6fd2d-114">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-swift-get-started).</span></span>
> 
> 

## <span data-ttu-id="6fd2d-115"><a id="setup-azme"></a>iOS 앱용 Mobile Engagement 설정</span><span class="sxs-lookup"><span data-stu-id="6fd2d-115"><a id="setup-azme"></a>Setup Mobile Engagement for your iOS app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="6fd2d-116"><a id="connecting-app"></a>응용 프로그램 toohello Mobile Engagement 백 엔드 연결</span><span class="sxs-lookup"><span data-stu-id="6fd2d-116"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="6fd2d-117">이 자습서는 기본적인 "통합", 최소 hello 필요한 toocollect 데이터 설정 되 고 푸시 알림을 보내는 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd2d-117">This tutorial presents a "basic integration", which is hello minimal set required toocollect data and send a push notification.</span></span> <span data-ttu-id="6fd2d-118">hello에 hello 완벽 한 통합 설명서를 확인할 수 있습니다 [Mobile Engagement iOS SDK 통합](mobile-engagement-ios-sdk-overview.md)</span><span class="sxs-lookup"><span data-stu-id="6fd2d-118">hello complete integration documentation can be found in hello [Mobile Engagement iOS SDK integration](mobile-engagement-ios-sdk-overview.md)</span></span>

<span data-ttu-id="6fd2d-119">XCode toodemonstrate hello 통합 기본 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6fd2d-119">We will create a basic app with XCode toodemonstrate hello integration:</span></span>

### <a name="create-a-new-ios-project"></a><span data-ttu-id="6fd2d-120">새 iOS 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="6fd2d-120">Create a new iOS project</span></span>
[!INCLUDE [Create a new iOS Project](../../includes/mobile-engagement-create-new-ios-app.md)]

### <a name="connect-your-app-toomobile-engagement-backend"></a><span data-ttu-id="6fd2d-121">응용 프로그램 tooMobile Engagement 백 엔드 연결</span><span class="sxs-lookup"><span data-stu-id="6fd2d-121">Connect your app tooMobile Engagement backend</span></span>
1. <span data-ttu-id="6fd2d-122">Hello 다운로드 [Mobile Engagement iOS SDK]</span><span class="sxs-lookup"><span data-stu-id="6fd2d-122">Download hello [Mobile Engagement iOS SDK]</span></span>
2. <span data-ttu-id="6fd2d-123">Hello를 추출 합니다. 컴퓨터에 tar.gz 파일 tooa 폴더</span><span class="sxs-lookup"><span data-stu-id="6fd2d-123">Extract hello .tar.gz file tooa folder in your computer</span></span>
3. <span data-ttu-id="6fd2d-124">Hello 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 "파일을 너무 추가..."</span><span class="sxs-lookup"><span data-stu-id="6fd2d-124">Right click hello project and select "Add files too..."</span></span>
   
    ![][1]
4. <span data-ttu-id="6fd2d-125">Hello SDK 및 선택 hello 추출한 toohello 폴더 탐색 `EngagementSDK` 폴더 다음 확인을 누르십시오.</span><span class="sxs-lookup"><span data-stu-id="6fd2d-125">Navigate toohello folder where you extracted hello SDK and select hello `EngagementSDK` folder then press OK.</span></span>
   
    ![][2]
5. <span data-ttu-id="6fd2d-126">열기 hello `Build Phases` 탭 및 hello `Link Binary With Libraries` 메뉴 아래와 같이 hello 프레임 워크를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd2d-126">Open hello `Build Phases` tab and in hello `Link Binary With Libraries` menu add hello frameworks as shown below:</span></span>
   
    ![][3]
6. <span data-ttu-id="6fd2d-127">파일을 선택 하 여 한 브리징 헤더 toobe 수 toouse hello SDK의 목적은 C Api 만들기 > 새로 만들기 > 파일 > iOS > 소스 > 헤더 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="6fd2d-127">Create a Bridging header toobe able toouse hello SDK's Objective C APIs by choosing File > New > File > iOS > Source > Header File.</span></span>
   
    ![][4]
7. <span data-ttu-id="6fd2d-128">Hello 브리징 헤더 파일 tooexpose Mobile Engagement Objective-c 코드 tooyour Swift 코드 편집, 추가 import를 수행 하는 hello:</span><span class="sxs-lookup"><span data-stu-id="6fd2d-128">Edit hello bridging header file tooexpose Mobile Engagement Objective-C code tooyour Swift code, add hello following imports :</span></span>
   
        /* Mobile Engagement Agent */
        #import "AEModule.h"
        #import "AEPushMessage.h"
        #import "AEStorage.h"
        #import "EngagementAgent.h"
        #import "EngagementTableViewController.h"
        #import "EngagementViewController.h"
        #import "AEUserNotificationHandler.h"
        #import "AEIdfaProvider.h"
8. <span data-ttu-id="6fd2d-129">빌드 설정에서 Objective-c 브리징 헤더 빌드 Swift 컴파일러-코드 생성에서 설정 하는 hello 경로 toothis 헤더에 있는지를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd2d-129">Under Build Settings, make sure hello Objective-C Bridging Header build setting under Swift Compiler - Code Generation has a path toothis header.</span></span> <span data-ttu-id="6fd2d-130">경로 예제는 다음과 같습니다: **$(SRCROOT)/MySuperApp/MySuperApp-Bridging-Header.h (hello 경로)에 따라 다름**</span><span class="sxs-lookup"><span data-stu-id="6fd2d-130">Here is a path example: **$(SRCROOT)/MySuperApp/MySuperApp-Bridging-Header.h (depending on hello path)**</span></span>
   
   ![][6]
9. <span data-ttu-id="6fd2d-131">Azure 포털에서 앱의 toohello 돌아가서 *연결 정보입니다.* 페이지 및 복사 hello 연결 문자열</span><span class="sxs-lookup"><span data-stu-id="6fd2d-131">Go back toohello Azure portal in your app's *Connection Info* page and copy hello Connection String</span></span>
   
   ![][5]
10. <span data-ttu-id="6fd2d-132">이제 hello에 hello 연결 문자열을 붙여 `didFinishLaunchingWithOptions` 위임</span><span class="sxs-lookup"><span data-stu-id="6fd2d-132">Now paste hello connection string in hello `didFinishLaunchingWithOptions` delegate</span></span>
    
        func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool
        {
              [...]
                EngagementAgent.init("Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}")
              [...]
        }

## <span data-ttu-id="6fd2d-133"><a id="monitor"></a>실시간 모니터링 사용</span><span class="sxs-lookup"><span data-stu-id="6fd2d-133"><a id="monitor"></a>Enabling real-time monitoring</span></span>
<span data-ttu-id="6fd2d-134">순서 toostart 데이터를 보내고는 hello 사용자가 활성화 되도록 하나 이상 화면 (활동) toohello Mobile Engagement 백 엔드를 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd2d-134">In order toostart sending data and ensuring that hello users are active, you must send at least one screen (Activity) toohello Mobile Engagement backend.</span></span>

1. <span data-ttu-id="6fd2d-135">열기 hello **ViewController.swift** hello의 기본 클래스를 바꾸고 파일 **ViewController** toobe **EngagementViewController**:</span><span class="sxs-lookup"><span data-stu-id="6fd2d-135">Open hello **ViewController.swift** file and replace hello base class of **ViewController** toobe **EngagementViewController**:</span></span>
   
    `class ViewController : EngagementViewController {`

## <span data-ttu-id="6fd2d-136"><a id="monitor"></a>실시간 모니터링과 앱 연결</span><span class="sxs-lookup"><span data-stu-id="6fd2d-136"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="6fd2d-137"><a id="integrate-push"></a>푸시 알림 및 앱 내 메시징 사용</span><span class="sxs-lookup"><span data-stu-id="6fd2d-137"><a id="integrate-push"></a>Enabling Push Notifications and in-app messaging</span></span>
<span data-ttu-id="6fd2d-138">Mobile Engagement 있습니다 toointeract 및 푸시 알림과 앱 내 메시징을와 사용자와 REACH 캠페인의 hello 컨텍스트에서.</span><span class="sxs-lookup"><span data-stu-id="6fd2d-138">Mobile Engagement allows you toointeract and REACH with your users with Push Notifications and In-app Messaging in hello context of campaigns.</span></span> <span data-ttu-id="6fd2d-139">이 모듈에는 hello Mobile engagement 연결 포털에서 REACH를 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd2d-139">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="6fd2d-140">hello 다음 섹션에서는 설치 응용 프로그램 tooreceive 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd2d-140">hello following sections will setup your app tooreceive them.</span></span>

### <a name="enable-your-app-tooreceive-silent-push-notifications"></a><span data-ttu-id="6fd2d-141">사용자 앱 tooreceive 자동 푸시 알림을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="6fd2d-141">Enable your app tooreceive Silent Push Notifications</span></span>
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

### <a name="add-hello-reach-library-tooyour-project"></a><span data-ttu-id="6fd2d-142">Hello Reach 라이브러리 tooyour 프로젝트 추가</span><span class="sxs-lookup"><span data-stu-id="6fd2d-142">Add hello Reach library tooyour project</span></span>
1. <span data-ttu-id="6fd2d-143">프로젝트를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd2d-143">Right click your project</span></span>
2. <span data-ttu-id="6fd2d-144">`Add file too...`을(를) 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd2d-144">Select `Add file too...`</span></span>
3. <span data-ttu-id="6fd2d-145">Hello SDK의 압축을 푼 toohello 폴더 이동</span><span class="sxs-lookup"><span data-stu-id="6fd2d-145">Navigate toohello folder where you extracted hello SDK</span></span>
4. <span data-ttu-id="6fd2d-146">선택 hello `EngagementReach` 폴더</span><span class="sxs-lookup"><span data-stu-id="6fd2d-146">Select hello `EngagementReach` folder</span></span>
5. <span data-ttu-id="6fd2d-147">추가를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd2d-147">Click Add</span></span>
6. <span data-ttu-id="6fd2d-148">브리징 헤더 파일 tooexpose Mobile Engagement Objective-c Reach 헤더 hello 편집한 다음 imports hello 추가:</span><span class="sxs-lookup"><span data-stu-id="6fd2d-148">Edit hello bridging header file tooexpose Mobile Engagement Objective-C Reach headers and add hello following imports :</span></span>
   
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

### <a name="modify-your-application-delegate"></a><span data-ttu-id="6fd2d-149">응용 프로그램 대리자 수정</span><span class="sxs-lookup"><span data-stu-id="6fd2d-149">Modify your Application Delegate</span></span>
1. <span data-ttu-id="6fd2d-150">내부 hello `didFinishLaunchingWithOptions` -reach 모듈 만들고 tooyour 기존 Engagement 초기화 줄 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd2d-150">Inside  hello `didFinishLaunchingWithOptions` -  create a reach module and pass it tooyour existing Engagement initialization line:</span></span>
   
        func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool 
        {
            let reach = AEReachModule.module(withNotificationIcon: UIImage(named:"icon.png")) as! AEReachModule
            EngagementAgent.init("Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}", modulesArray:[reach])
            [...]
            return true
        }

### <a name="enable-your-app-tooreceive-apns-push-notifications"></a><span data-ttu-id="6fd2d-151">사용자 응용 프로그램 tooreceive APNS 푸시 알림을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="6fd2d-151">Enable your app tooreceive APNS Push Notifications</span></span>
1. <span data-ttu-id="6fd2d-152">다음 줄 toohello hello 추가 `didFinishLaunchingWithOptions` 메서드:</span><span class="sxs-lookup"><span data-stu-id="6fd2d-152">Add hello following line toohello `didFinishLaunchingWithOptions` method:</span></span>
   
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
2. <span data-ttu-id="6fd2d-153">Hello 추가 `didRegisterForRemoteNotificationsWithDeviceToken` 메서드를 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd2d-153">Add hello `didRegisterForRemoteNotificationsWithDeviceToken` method as follows:</span></span>
   
        func application(_ application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data) {
            EngagementAgent.shared().registerDeviceToken(deviceToken)
        }
3. <span data-ttu-id="6fd2d-154">Hello 추가 `didReceiveRemoteNotification:fetchCompletionHandler:` 메서드를 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd2d-154">Add hello `didReceiveRemoteNotification:fetchCompletionHandler:` method as follows:</span></span>
   
        func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any], fetchCompletionHandler completionHandler: @escaping (UIBackgroundFetchResult) -> Void) {
            EngagementAgent.shared().applicationDidReceiveRemoteNotification(userInfo, fetchCompletionHandler:completionHandler)
        }

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- URLs. -->
[Mobile Engagement iOS SDK]: http://aka.ms/qk2rnj

<!-- Images. -->
[1]: ./media/mobile-engagement-ios-get-started/xcode-add-files.png
[2]: ./media/mobile-engagement-ios-get-started/xcode-select-engagement-sdk.png
[3]: ./media/mobile-engagement-ios-get-started/xcode-build-phases.png
[4]: ./media/mobile-engagement-ios-swift-get-started/add-header-file.png
[5]: ./media/mobile-engagement-ios-get-started/app-connection-info-page.png
[6]: ./media/mobile-engagement-ios-swift-get-started/add-bridging-header.png

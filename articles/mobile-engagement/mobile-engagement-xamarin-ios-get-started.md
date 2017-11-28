---
title: "aaaGet Xamarin.iOS에 대 한 Azure Mobile Engagement와 시작 됨"
description: "자세한 내용은 방법 toouse 분석 및 푸시 알림 Xamarin.iOS 앱에 대 한 Azure Mobile Engagement 합니다."
services: mobile-engagement
documentationcenter: xamarin
author: piyushjo
manager: erikre
editor: 
ms.assetid: 0448209e-fff6-47bd-985c-2cf074bac12f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 02340a744753dcc5cd1b6888a5fa87628be47b68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-xamarinios-apps"></a><span data-ttu-id="d6ad7-103">Xamarin.iOS 앱용 Azure Mobile Engagement 시작</span><span class="sxs-lookup"><span data-stu-id="d6ad7-103">Get Started with Azure Mobile Engagement for Xamarin.iOS Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="d6ad7-104">이 항목에서는 Azure Mobile Engagement toounderstand toouse Xamarin.iOS 응용 프로그램에서 응용 프로그램 사용 및 송신 푸시 알림을 toosegmented 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="d6ad7-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and send push notifications toosegmented users in a Xamarin.iOS application.</span></span>
<span data-ttu-id="d6ad7-105">이 자습서에서는 기본 데이터를 수집하고 APNS(Apple 푸시 알림 시스템)를 사용하여 푸시 알림을 받는 빈 Xamarin.iOS 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d6ad7-105">In this tutorial, you create a blank Xamarin.iOS app that collects basic data and receives push notifications using Apple Push Notification System (APNS).</span></span>

> [!NOTE]
> <span data-ttu-id="d6ad7-106">hello Azure Mobile Engagement 서비스 년 3 월 2018 사용 중지 될 했으며 현재 사용 가능한 tooexisting 고객만 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6ad7-106">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="d6ad7-107">자세한 내용은 [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d6ad7-107">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="d6ad7-108">이 자습서는 hello 다음을 사항이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d6ad7-108">This tutorial requires hello following:</span></span>

* <span data-ttu-id="d6ad7-109">[Xamarin Studio](http://xamarin.com/studio).</span><span class="sxs-lookup"><span data-stu-id="d6ad7-109">[Xamarin Studio](http://xamarin.com/studio).</span></span> <span data-ttu-id="d6ad7-110">Xamarin이 포함된 Visual Studio를 사용할 수도 있지만 이 자습서에서는 Xamarin Studio를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d6ad7-110">You can also use Visual Studio with Xamarin but this tutorial uses Xamarin Studio.</span></span> <span data-ttu-id="d6ad7-111">또한 설치 지침은 [Visual Studio 및 Xamarin을 위한 설정 및 설치](https://msdn.microsoft.com/library/mt613162.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d6ad7-111">For installation instructions, see [Setup and Install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span></span> 
* [<span data-ttu-id="d6ad7-112">Mobile Engagement Xamarin SDK</span><span class="sxs-lookup"><span data-stu-id="d6ad7-112">Mobile Engagement Xamarin SDK</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Engagement.Xamarin/)

> [!NOTE]
> <span data-ttu-id="d6ad7-113">toocomplete이이 자습서에서는 활성 Azure 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6ad7-113">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="d6ad7-114">계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6ad7-114">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="d6ad7-115">자세한 내용은 [Azure 평가판](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-ios-get-started)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d6ad7-115">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-ios-get-started).</span></span>
> 
> 

## <span data-ttu-id="d6ad7-116"><a id="setup-azme"></a>iOS 앱용 Mobile Engagement 설정</span><span class="sxs-lookup"><span data-stu-id="d6ad7-116"><a id="setup-azme"></a>Setup Mobile Engagement for your iOS app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="d6ad7-117"><a id="connecting-app"></a>응용 프로그램 toohello Mobile Engagement 백 엔드 연결</span><span class="sxs-lookup"><span data-stu-id="d6ad7-117"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="d6ad7-118">이 자습서에는 "기본 통합" hello 최소 필수 toocollect 데이터 설정 되 고 푸시 알림을 보내려면 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6ad7-118">This tutorial presents a "basic integration" which is hello minimal set required toocollect data and send a push notification.</span></span>

<span data-ttu-id="d6ad7-119">Xamarin toodemonstrate hello 통합 기본 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d6ad7-119">We will create a basic app with Xamarin toodemonstrate hello integration:</span></span>

### <a name="create-a-new-xamarinios-project"></a><span data-ttu-id="d6ad7-120">새 Xamarin.iOS 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="d6ad7-120">Create a new Xamarin.iOS project</span></span>
1. <span data-ttu-id="d6ad7-121">Xamarin Studio를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d6ad7-121">Launch Xamarin Studio.</span></span> <span data-ttu-id="d6ad7-122">너무 이동**파일** -> **새로** -> **솔루션**</span><span class="sxs-lookup"><span data-stu-id="d6ad7-122">Go too**File** -> **New** -> **Solution**</span></span> 
   
    ![][1]
2. <span data-ttu-id="d6ad7-123">선택 **단일 앱 보기**, 선택한 hello 언어 인지 확인 **C#** 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="d6ad7-123">Select **Single View App**, make sure hello selected language is **C#** and then click **Next**.</span></span>
   
    ![][2]
3. <span data-ttu-id="d6ad7-124">Hello 입력 **응용 프로그램 이름** 및 hello **조직 식별자** 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="d6ad7-124">Fill in hello **App Name** and hello **Organization Identifier** and then click **Next**.</span></span> 
   
    ![][3]
   
   > [!IMPORTANT]
   > <span data-ttu-id="d6ad7-125">게시 프로필을 iOS 앱에 일치 하는 응용 프로그램 ID를 사용 하는 hello 여기에 있는 번들 식별자와 정확 하 게 toodeploy 결국 사용 하면 해당 hello 있는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="d6ad7-125">Make sure that hello publishing profile you eventually use toodeploy your iOS app is using an App ID which matches exactly with hello Bundle Identifier you have here.</span></span> 
   > 
   > 
4. <span data-ttu-id="d6ad7-126">업데이트 hello **프로젝트 이름**, **솔루션 이름** 및 **위치** 필요 하 고 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="d6ad7-126">Update hello **Project Name**, **Solution Name** and **Location** if required and click **Create**.</span></span>
   
    ![][4]

<span data-ttu-id="d6ad7-127">Xamarin Studio는 Mobile Engagement 통합할 hello 데모 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d6ad7-127">Xamarin Studio will create hello demo app in which we will integrate Mobile Engagement.</span></span> 

### <a name="connect-your-app-toomobile-engagement-backend"></a><span data-ttu-id="d6ad7-128">응용 프로그램 tooMobile Engagement 백 엔드 연결</span><span class="sxs-lookup"><span data-stu-id="d6ad7-128">Connect your app tooMobile Engagement backend</span></span>
1. <span data-ttu-id="d6ad7-129">마우스 오른쪽 단추로 클릭 하 여 hello **패키지** hello 솔루션 창과 선택에서 폴더 **패키지 추가 중...**</span><span class="sxs-lookup"><span data-stu-id="d6ad7-129">Right click hello **Packages** folder in hello Solution windows and select **Add Packages...**</span></span>
   
    ![][5]
2. <span data-ttu-id="d6ad7-130">Hello에 대 한 검색 **Microsoft Azure Mobile Engagement Xamarin SDK** tooyour 솔루션에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6ad7-130">Search for hello **Microsoft Azure Mobile Engagement Xamarin SDK** and add it tooyour solution.</span></span>  
   
    ![][6]
3. <span data-ttu-id="d6ad7-131">열기 **AppDelegate.cs** hello 다음 추가 및 문을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="d6ad7-131">Open **AppDelegate.cs** and add hello following using statement:</span></span>
   
        using Microsoft.Azure.Engagement.Xamarin;
4. <span data-ttu-id="d6ad7-132">Hello에 **FinishedLaunching** 메서드를 다음 Mobile Engagement 백 엔드와 tooinitialize hello 연결 hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6ad7-132">In hello **FinishedLaunching** method, add hello following tooinitialize hello connection with Mobile Engagement backend.</span></span> <span data-ttu-id="d6ad7-133">있는지 tooadd 확인 프로그램 **ConnectionString**합니다.</span><span class="sxs-lookup"><span data-stu-id="d6ad7-133">Make sure tooadd your **ConnectionString**.</span></span> <span data-ttu-id="d6ad7-134">이 코드에서는 dummy **NotificationIcon** hello 할 수도 있습니다는 Mobile Engagement SDK 추가할 tooreplace 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6ad7-134">This code also uses a dummy **NotificationIcon** which is added by hello Mobile Engagement SDK which you may want tooreplace.</span></span> 
   
        EngagementConfiguration config = new EngagementConfiguration {
                        ConnectionString = "YourConnectionStringFromAzurePortal",
                        NotificationIcon = UIImage.FromBundle("close")
                    };
        EngagementAgent.Init (config);

## <span data-ttu-id="d6ad7-135"><a id="monitor"></a>실시간 모니터링 사용</span><span class="sxs-lookup"><span data-stu-id="d6ad7-135"><a id="monitor"></a>Enabling real-time monitoring</span></span>
<span data-ttu-id="d6ad7-136">순서 toostart 데이터를 보내고 hello 사용자는 활성 하나 이상 화면 toohello Mobile Engagement 백 엔드를 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6ad7-136">In order toostart sending data and ensuring hello users are active, you must send at least one screen toohello Mobile Engagement backend.</span></span>

1. <span data-ttu-id="d6ad7-137">열기 **ViewController.cs** hello 다음 추가 및 문을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="d6ad7-137">Open **ViewController.cs** and add hello following using statement:</span></span>
   
        using Microsoft.Azure.Engagement.Xamarin;
2. <span data-ttu-id="d6ad7-138">Hello 클래스를 대체 `ViewController` 에서 상속 `UIViewController` 너무`EngagementViewController`합니다.</span><span class="sxs-lookup"><span data-stu-id="d6ad7-138">Replace hello class from which `ViewController` inherits from `UIViewController` too`EngagementViewController`.</span></span> 

## <span data-ttu-id="d6ad7-139"><a id="monitor"></a>실시간 모니터링과 앱 연결</span><span class="sxs-lookup"><span data-stu-id="d6ad7-139"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="d6ad7-140"><a id="integrate-push"></a>푸시 알림 및 앱 내 메시징 사용</span><span class="sxs-lookup"><span data-stu-id="d6ad7-140"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="d6ad7-141">Mobile Engagement 사용 하면 사용자와 toointeract 및 도달 범위 푸시 알림과 앱 내 메시징을 캠페인의 hello 컨텍스트에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6ad7-141">Mobile Engagement allows you toointeract with your users and REACH with push notifications and in-app messaging in hello context of campaigns.</span></span> <span data-ttu-id="d6ad7-142">이 모듈에는 hello Mobile engagement 연결 포털에서 REACH를 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6ad7-142">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="d6ad7-143">hello 다음 섹션에서는 앱 tooreceive를 속성을 설정.</span><span class="sxs-lookup"><span data-stu-id="d6ad7-143">hello following sections set up your app tooreceive them.</span></span>

### <a name="modify-your-application-delegate"></a><span data-ttu-id="d6ad7-144">응용 프로그램 대리자 수정</span><span class="sxs-lookup"><span data-stu-id="d6ad7-144">Modify your Application Delegate</span></span>
1. <span data-ttu-id="d6ad7-145">열기 hello **AppDelegate.cs** hello 다음 추가 및 문을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="d6ad7-145">Open hello **AppDelegate.cs** and add hello following using statement:</span></span>
   
        using System; 
2. <span data-ttu-id="d6ad7-146">이제 hello 내 `FinishedLaunching` 메서드를 hello tooregister 이후 푸시 메시지에 대 한 다음 추가`EngagementAgent.init(...)`</span><span class="sxs-lookup"><span data-stu-id="d6ad7-146">Now inside hello `FinishedLaunching` method, add hello following tooregister for push messages after `EngagementAgent.init(...)`</span></span>
   
        if (UIDevice.CurrentDevice.CheckSystemVersion(8,0))
        {
            var pushSettings = UIUserNotificationSettings.GetSettingsForTypes (
                (UIUserNotificationType.Badge |
                    UIUserNotificationType.Sound |
                    UIUserNotificationType.Alert),
                null);
            UIApplication.SharedApplication.RegisterUserNotificationSettings (pushSettings);
            UIApplication.SharedApplication.RegisterForRemoteNotifications ();
        }
        else
        {
            UIApplication.SharedApplication.RegisterForRemoteNotificationTypes (
                UIRemoteNotificationType.Badge |
                UIRemoteNotificationType.Sound |
                UIRemoteNotificationType.Alert);
        }
3. <span data-ttu-id="d6ad7-147">-마지막으로 업데이트 하거나 hello 다음 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6ad7-147">Finally - update or add hello following methods:</span></span>
   
        public override void DidReceiveRemoteNotification (UIApplication application, NSDictionary userInfo, 
            Action<UIBackgroundFetchResult> completionHandler)
        {
            EngagementAgent.ApplicationDidReceiveRemoteNotification(userInfo, completionHandler);
        }
   
        public override void RegisteredForRemoteNotifications (UIApplication application, NSData deviceToken)
        {
            // Register device token on Engagement
            EngagementAgent.RegisterDeviceToken(deviceToken);
        }
   
        public override void FailedToRegisterForRemoteNotifications(UIApplication application, NSError error)
        {
            Console.WriteLine("Failed tooregister for remote notifications: Error '{0}'", error);
        }
4. <span data-ttu-id="d6ad7-148">사용자 **Info.plist** hello 솔루션의 파일, 해당 hello 확인 **번들 식별자** hello로 일치 **앱 ID** hello Apple 개발자의에서 프로비저닝 프로필에 있는 가운데 맞춤 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6ad7-148">In your **Info.plist** file in hello solution, confirm that hello **Bundle Identifier** matches with hello **App ID** you have in your provisioning profile in hello Apple Dev Center.</span></span> 
   
    ![][7]
5. <span data-ttu-id="d6ad7-149">동일한 hello **Info.plist** 파일, hello를 선택 했는지 확인 **백그라운드 모드를 사용 하도록 설정** 및 **원격 알림**합니다.</span><span class="sxs-lookup"><span data-stu-id="d6ad7-149">In hello same **Info.plist** file, make sure that you have checked hello **Enable Background Modes** and **Remote Notifications**.</span></span> 
   
     ![][8]
6. <span data-ttu-id="d6ad7-150">이 게시 프로필에 연결 했는지 hello 장치의 hello 앱을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6ad7-150">Run hello app on hello device you have associated with this publishing profile.</span></span> 

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- Images. -->
[1]: ./media/mobile-engagement-xamarin-ios-get-started/new-solution.png
[2]: ./media/mobile-engagement-xamarin-ios-get-started/app-type.png
[3]: ./media/mobile-engagement-xamarin-ios-get-started/configure-project-name.png
[4]: ./media/mobile-engagement-xamarin-ios-get-started/configure-project-confirm.png
[5]: ./media/mobile-engagement-xamarin-ios-get-started/add-nuget.png
[6]: ./media/mobile-engagement-xamarin-ios-get-started/add-nuget-azme.png
[7]: ./media/mobile-engagement-xamarin-ios-get-started/info-plist-confirm-bundle.png
[8]: ./media/mobile-engagement-xamarin-ios-get-started/info-plist-configure-push.png

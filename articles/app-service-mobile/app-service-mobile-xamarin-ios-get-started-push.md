---
title: "Azure 앱 서비스를 사용하여 Xamarin.iOS 앱에 푸시 알림 추가"
description: "Azure 앱 서비스를 사용하여Xamarin.iOS 앱에 푸시 알림을 전송하는 방법을 알아봅니다."
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 2921214a-49f8-45e1-a306-a85ce21defca
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: glenga
ms.openlocfilehash: bf922e49c4c92d0065817a5dd6c7d10a04737304
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="add-push-notifications-to-your-xamarinios-app"></a><span data-ttu-id="869fa-103">Xamarin.iOS 앱에 푸시 알림 추가</span><span class="sxs-lookup"><span data-stu-id="869fa-103">Add push notifications to your Xamarin.iOS App</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="869fa-104">개요</span><span class="sxs-lookup"><span data-stu-id="869fa-104">Overview</span></span>
<span data-ttu-id="869fa-105">이 자습서에서는 푸시 알림을 [Xamarin.iOS 빠른 시작](app-service-mobile-xamarin-ios-get-started.md) 프로젝트에 추가하여 레코드가 삽입될 때마다 장치에 푸시 알림이 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="869fa-105">In this tutorial, you add push notifications to the [Xamarin.iOS quick start](app-service-mobile-xamarin-ios-get-started.md) project so that a push notification is sent to the device every time a record is inserted.</span></span>

<span data-ttu-id="869fa-106">다운로드한 빠른 시작 서버 프로젝트를 사용하지 않는 경우 푸시 알림 확장 패키지가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="869fa-106">If you do not use the downloaded quick start server project, you will need the push notification extension package.</span></span> <span data-ttu-id="869fa-107">자세한 내용은 [Azure Mobile Apps용 .NET 백 엔드 서버 SDK 사용](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="869fa-107">See [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="869fa-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="869fa-108">Prerequisites</span></span>
* <span data-ttu-id="869fa-109">[Xamarin.iOS 빠른 시작 자습서](app-service-mobile-xamarin-ios-get-started.md) 를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="869fa-109">Complete the [Xamarin.iOS quickstart](app-service-mobile-xamarin-ios-get-started.md) tutorial.</span></span>
* <span data-ttu-id="869fa-110">실제 iOS 장치.</span><span class="sxs-lookup"><span data-stu-id="869fa-110">A physical iOS device.</span></span> <span data-ttu-id="869fa-111">푸시 알림은 iOS 시뮬레이터에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="869fa-111">Push notifications are not supported by the iOS simulator.</span></span>

## <a name="register-the-app-for-push-notifications-on-apples-developer-portal"></a><span data-ttu-id="869fa-112">Apple 개발자 포털의 푸시 알림에 대한 앱 등록</span><span class="sxs-lookup"><span data-stu-id="869fa-112">Register the app for push notifications on Apple's developer portal</span></span>
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

## <a name="configure-your-mobile-app-to-send-push-notifications"></a><span data-ttu-id="869fa-113">푸시 알림을 전송하도록 모바일 앱 구성</span><span class="sxs-lookup"><span data-stu-id="869fa-113">Configure your Mobile App to send push notifications</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

## <a name="update-the-server-project-to-send-push-notifications"></a><span data-ttu-id="869fa-114">푸시 알림을 전송하도록 서버 프로젝트 업데이트</span><span class="sxs-lookup"><span data-stu-id="869fa-114">Update the server project to send push notifications</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="configure-your-xamarinios-project"></a><span data-ttu-id="869fa-115">Xamarin.iOS 프로젝트 구성</span><span class="sxs-lookup"><span data-stu-id="869fa-115">Configure your Xamarin.iOS project</span></span>
[!INCLUDE [app-service-mobile-xamarin-ios-configure-project](../../includes/app-service-mobile-xamarin-ios-configure-project.md)]

## <a name="add-push-notifications-to-your-app"></a><span data-ttu-id="869fa-116">앱에 푸시 알림 추가</span><span class="sxs-lookup"><span data-stu-id="869fa-116">Add push notifications to your app</span></span>
1. <span data-ttu-id="869fa-117">**QSTodoService**에서 **AppDelegate**가 모바일 클라이언트를 가져올 수 있도록 다음 속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="869fa-117">In **QSTodoService**, add the following property so that **AppDelegate** can acquire the mobile client:</span></span>
   
            public MobileServiceClient GetClient {
            get
            {
                return client;
            }
            private set
            {
                client = value;
            }
        }
2. <span data-ttu-id="869fa-118">다음 `using` 문을 **AppDelegate.cs** 파일의 맨 위에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="869fa-118">Add the following `using` statement to the top of the **AppDelegate.cs** file.</span></span>
   
        using Microsoft.WindowsAzure.MobileServices;
        using Newtonsoft.Json.Linq;
3. <span data-ttu-id="869fa-119">**AppDelegate**에서 **FinishedLaunching** 이벤트를 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="869fa-119">In **AppDelegate**, override the **FinishedLaunching** event:</span></span>
   
        public override bool FinishedLaunching(UIApplication application, NSDictionary launchOptions)
        {
            // registers for push for iOS8
            var settings = UIUserNotificationSettings.GetSettingsForTypes(
                UIUserNotificationType.Alert
                | UIUserNotificationType.Badge
                | UIUserNotificationType.Sound,
                new NSSet());
   
            UIApplication.SharedApplication.RegisterUserNotificationSettings(settings);
            UIApplication.SharedApplication.RegisterForRemoteNotifications();
   
            return true;
        }
4. <span data-ttu-id="869fa-120">동일한 파일에서 **RegisteredForRemoteNotifications** 이벤트를 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="869fa-120">In the same file, override the **RegisteredForRemoteNotifications** event.</span></span> <span data-ttu-id="869fa-121">이 코드에서는 서버에서 지원하는 모든 플랫폼에서 전송되는 간단한 템플릿 알림을 등록하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="869fa-121">In this code you are registering for a simple template notification that will be sent across all supported platforms by the server.</span></span>
   
    <span data-ttu-id="869fa-122">알림 허브를 사용하는 템플릿에 대한 자세한 내용은 [템플릿](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="869fa-122">For more information on templates with Notification Hubs, see [Templates](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span></span>

        public override void RegisteredForRemoteNotifications(UIApplication application, NSData deviceToken)
        {
            MobileServiceClient client = QSTodoService.DefaultService.GetClient;

            const string templateBodyAPNS = "{\"aps\":{\"alert\":\"$(messageParam)\"}}";

            JObject templates = new JObject();
            templates["genericMessage"] = new JObject
            {
                {"body", templateBodyAPNS}
            };

            // Register for push with your mobile app
            var push = client.GetPush();
            push.RegisterAsync(deviceToken, templates);
        }


1. <span data-ttu-id="869fa-123">그런 다음 **DidReceivedRemoteNotification** 이벤트를 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="869fa-123">Then, override the **DidReceivedRemoteNotification** event:</span></span>
   
        public override void DidReceiveRemoteNotification (UIApplication application, NSDictionary userInfo, Action<UIBackgroundFetchResult> completionHandler)
        {
            NSDictionary aps = userInfo.ObjectForKey(new NSString("aps")) as NSDictionary;
   
            string alert = string.Empty;
            if (aps.ContainsKey(new NSString("alert")))
                alert = (aps [new NSString("alert")] as NSString).ToString();
   
            //show alert
            if (!string.IsNullOrEmpty(alert))
            {
                UIAlertView avAlert = new UIAlertView("Notification", alert, null, "OK", null);
                avAlert.Show();
            }
        }

<span data-ttu-id="869fa-124">이제 앱이 푸시 알림을 지원하도록 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="869fa-124">Your app is now updated to support push notifications.</span></span>

## <span data-ttu-id="869fa-125"><a name="test"></a>앱에서 푸시 알림 테스트</span><span class="sxs-lookup"><span data-stu-id="869fa-125"><a name="test"></a>Test push notifications in your app</span></span>
1. <span data-ttu-id="869fa-126">**실행** 단추를 눌러 프로젝트를 빌드하고 iOS 지원 장치에서 앱을 시작한 다음, **확인**을 클릭하여 푸시 알림을 수락합니다.</span><span class="sxs-lookup"><span data-stu-id="869fa-126">Press the **Run** button to build the project and start the app in an iOS capable device, then click **OK** to accept push notifications.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="869fa-127">앱에서 푸시 알림을 명시적으로 수락해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="869fa-127">You must explicitly accept push notifications from your app.</span></span> <span data-ttu-id="869fa-128">이 요청은 앱이 처음 실행될 때만 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="869fa-128">This request only occurs the first time that the app runs.</span></span>
   > 
   > 
2. <span data-ttu-id="869fa-129">앱에서 작업을 입력한 다음 더하기(**+**) 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="869fa-129">In the app, type a task, and then click the plus (**+**) icon.</span></span>
3. <span data-ttu-id="869fa-130">알림이 수신되는지 확인하고, **확인** 을 클릭하여 알림을 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="869fa-130">Verify that a notification is received, then click **OK** to dismiss the notification.</span></span>
4. <span data-ttu-id="869fa-131">2단계를 반복하여 앱을 즉시 닫은 후 알림이 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="869fa-131">Repeat step 2 and immediately close the app, then verify that a notification is shown.</span></span>

<span data-ttu-id="869fa-132">이 자습서를 성공적으로 완료했습니다.</span><span class="sxs-lookup"><span data-stu-id="869fa-132">You have successfully completed this tutorial.</span></span>

<!-- Images. -->

<!-- URLs. -->




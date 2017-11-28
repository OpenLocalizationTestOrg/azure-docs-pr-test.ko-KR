---
title: "aaaAdd 푸시 알림 tooyour Xamarin.iOS 앱을 Azure 앱 서비스"
description: "Azure 앱 서비스 toosend toouse 밀어넣기 알림 tooyour Xamarin.iOS 앱에 알아봅니다"
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
ms.openlocfilehash: 3e6439aee4f3fe0f60b9786d0bbfd74c4f5e52d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-xamarinios-app"></a><span data-ttu-id="93fef-103">푸시 알림 tooyour Xamarin.iOS 앱 추가</span><span class="sxs-lookup"><span data-stu-id="93fef-103">Add push notifications tooyour Xamarin.iOS App</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="93fef-104">개요</span><span class="sxs-lookup"><span data-stu-id="93fef-104">Overview</span></span>
<span data-ttu-id="93fef-105">이 자습서에서는 푸시 알림을 toohello 추가한 [Xamarin.iOS 퀵 스타트](app-service-mobile-xamarin-ios-get-started.md) 프로젝트 레코드가 삽입 될 때마다 푸시 알림을 toohello 장치가 전송 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="93fef-105">In this tutorial, you add push notifications toohello [Xamarin.iOS quick start](app-service-mobile-xamarin-ios-get-started.md) project so that a push notification is sent toohello device every time a record is inserted.</span></span>

<span data-ttu-id="93fef-106">사용 하지 않는 경우 hello 퀵 스타트 서버 프로젝트를 다운로드, 푸시 알림 확장 패키지 hello 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="93fef-106">If you do not use hello downloaded quick start server project, you will need hello push notification extension package.</span></span> <span data-ttu-id="93fef-107">참조 [Azure 모바일 앱에 대 한 hello.NET 백 엔드 서버 SDK에서 작동](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="93fef-107">See [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="93fef-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="93fef-108">Prerequisites</span></span>
* <span data-ttu-id="93fef-109">전체 hello [Xamarin.iOS 퀵 스타트](app-service-mobile-xamarin-ios-get-started.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="93fef-109">Complete hello [Xamarin.iOS quickstart](app-service-mobile-xamarin-ios-get-started.md) tutorial.</span></span>
* <span data-ttu-id="93fef-110">실제 iOS 장치.</span><span class="sxs-lookup"><span data-stu-id="93fef-110">A physical iOS device.</span></span> <span data-ttu-id="93fef-111">푸시 알림은 hello iOS 시뮬레이터에서 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="93fef-111">Push notifications are not supported by hello iOS simulator.</span></span>

## <a name="register-hello-app-for-push-notifications-on-apples-developer-portal"></a><span data-ttu-id="93fef-112">Apple 개발자 포털에서 푸시 알림을 hello 앱 등록</span><span class="sxs-lookup"><span data-stu-id="93fef-112">Register hello app for push notifications on Apple's developer portal</span></span>
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

## <a name="configure-your-mobile-app-toosend-push-notifications"></a><span data-ttu-id="93fef-113">프로그램 모바일 앱 toosend 푸시 알림 구성</span><span class="sxs-lookup"><span data-stu-id="93fef-113">Configure your Mobile App toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

## <a name="update-hello-server-project-toosend-push-notifications"></a><span data-ttu-id="93fef-114">업데이트 hello 서버 프로젝트 toosend 푸시 알림</span><span class="sxs-lookup"><span data-stu-id="93fef-114">Update hello server project toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="configure-your-xamarinios-project"></a><span data-ttu-id="93fef-115">Xamarin.iOS 프로젝트 구성</span><span class="sxs-lookup"><span data-stu-id="93fef-115">Configure your Xamarin.iOS project</span></span>
[!INCLUDE [app-service-mobile-xamarin-ios-configure-project](../../includes/app-service-mobile-xamarin-ios-configure-project.md)]

## <a name="add-push-notifications-tooyour-app"></a><span data-ttu-id="93fef-116">푸시 알림 tooyour 앱 추가</span><span class="sxs-lookup"><span data-stu-id="93fef-116">Add push notifications tooyour app</span></span>
1. <span data-ttu-id="93fef-117">**QSTodoService**, hello 다음 속성을 추가 되도록 **AppDelegate** hello 모바일 클라이언트를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93fef-117">In **QSTodoService**, add hello following property so that **AppDelegate** can acquire hello mobile client:</span></span>
   
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
2. <span data-ttu-id="93fef-118">Hello 다음 추가 `using` 문 toohello 맨 hello **AppDelegate.cs** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="93fef-118">Add hello following `using` statement toohello top of hello **AppDelegate.cs** file.</span></span>
   
        using Microsoft.WindowsAzure.MobileServices;
        using Newtonsoft.Json.Linq;
3. <span data-ttu-id="93fef-119">**AppDelegate**, hello 재정의 **FinishedLaunching** 이벤트:</span><span class="sxs-lookup"><span data-stu-id="93fef-119">In **AppDelegate**, override hello **FinishedLaunching** event:</span></span>
   
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
4. <span data-ttu-id="93fef-120">동일한 파일 hello 하 hello 재정의 **RegisteredForRemoteNotifications** 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="93fef-120">In hello same file, override hello **RegisteredForRemoteNotifications** event.</span></span> <span data-ttu-id="93fef-121">이 코드에 대 한 hello 서버에서 지원 되는 모든 플랫폼에서 전송 되는 간단한 템플릿 알림을 등록 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="93fef-121">In this code you are registering for a simple template notification that will be sent across all supported platforms by hello server.</span></span>
   
    <span data-ttu-id="93fef-122">알림 허브를 사용하는 템플릿에 대한 자세한 내용은 [템플릿](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="93fef-122">For more information on templates with Notification Hubs, see [Templates](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span></span>

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


1. <span data-ttu-id="93fef-123">그런 다음 재정의 하는 hello **DidReceivedRemoteNotification** 이벤트:</span><span class="sxs-lookup"><span data-stu-id="93fef-123">Then, override hello **DidReceivedRemoteNotification** event:</span></span>
   
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

<span data-ttu-id="93fef-124">앱 업데이트 toosupport 푸시 알림이 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="93fef-124">Your app is now updated toosupport push notifications.</span></span>

## <span data-ttu-id="93fef-125"><a name="test"></a>앱에서 푸시 알림 테스트</span><span class="sxs-lookup"><span data-stu-id="93fef-125"><a name="test"></a>Test push notifications in your app</span></span>
1. <span data-ttu-id="93fef-126">키를 눌러 hello **실행** toobuild hello 프로젝트 단추 하 고 iOS 지원 장치에서 hello 응용 프로그램을 시작 합니다. 다음 클릭 **확인** tooaccept 푸시 알림을 합니다.</span><span class="sxs-lookup"><span data-stu-id="93fef-126">Press hello **Run** button toobuild hello project and start hello app in an iOS capable device, then click **OK** tooaccept push notifications.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="93fef-127">앱에서 푸시 알림을 명시적으로 수락해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93fef-127">You must explicitly accept push notifications from your app.</span></span> <span data-ttu-id="93fef-128">이 요청은만 hello 앱이 실행 hello 처음으로 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="93fef-128">This request only occurs hello first time that hello app runs.</span></span>
   > 
   > 
2. <span data-ttu-id="93fef-129">Hello 응용 프로그램에서 작업을 입력 한 다음 더하기 hello (**+**) 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="93fef-129">In hello app, type a task, and then click hello plus (**+**) icon.</span></span>
3. <span data-ttu-id="93fef-130">알림이 수신 되 면 다음 클릭 확인 **확인** toodismiss hello 알림입니다.</span><span class="sxs-lookup"><span data-stu-id="93fef-130">Verify that a notification is received, then click **OK** toodismiss hello notification.</span></span>
4. <span data-ttu-id="93fef-131">단계 2와 종가 즉시 hello 앱 반복 다음 알림을 표시 되는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="93fef-131">Repeat step 2 and immediately close hello app, then verify that a notification is shown.</span></span>

<span data-ttu-id="93fef-132">이 자습서를 성공적으로 완료했습니다.</span><span class="sxs-lookup"><span data-stu-id="93fef-132">You have successfully completed this tutorial.</span></span>

<!-- Images. -->

<!-- URLs. -->




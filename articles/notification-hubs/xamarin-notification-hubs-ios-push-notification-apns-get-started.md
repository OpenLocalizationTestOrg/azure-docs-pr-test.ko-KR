---
title: "Xamarin 앱 용 알림 허브를 사용 하 여 푸시 알림을 aaaiOS | Microsoft Docs"
description: "이 자습서에서는 Azure 알림 허브 toosend toouse 알림 tooa Xamarin iOS 응용 프로그램을 강제 하는 방법을 배웁니다."
services: notification-hubs
keywords: "ios 푸시 알림, 푸시 메시지, 푸시 알림, 푸시 메시지"
documentationcenter: xamarin
author: ysxu
manager: erikre
editor: 
ms.assetid: 4d4dfd42-c5a5-4360-9d70-7812f96924d2
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 8db60338047dd53074b4d3d4bb127aa6d9f13a25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="ios-push-notifications-with-notification-hubs-for-xamarin-apps"></a><span data-ttu-id="447bf-104">Xamarin 앱용 알림 허브를 사용한 iOS 푸시 알림</span><span class="sxs-lookup"><span data-stu-id="447bf-104">iOS Push Notifications with Notification Hubs for Xamarin apps</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="447bf-105">개요</span><span class="sxs-lookup"><span data-stu-id="447bf-105">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="447bf-106">toocomplete이이 자습서에서는 활성 Azure 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="447bf-106">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="447bf-107">계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="447bf-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="447bf-108">자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="447bf-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).</span></span>
> 
> 

<span data-ttu-id="447bf-109">이 자습서에서는 Azure 알림 허브 toosend toouse 밀어넣기 알림 tooan iOS 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="447bf-109">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooan iOS application.</span></span>
<span data-ttu-id="447bf-110">Hello를 사용 하 여 푸시 알림을 수신 하는 빈 Xamarin.iOS 앱 만들게 [Apple 푸시 알림 서비스 (APNs)](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="447bf-110">You'll create a blank Xamarin.iOS app that receives push notifications by using hello [Apple Push Notification Service (APNs)](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html).</span></span> <span data-ttu-id="447bf-111">수 toouse 수 완료 되 면 알림 허브 toobroadcast 푸시 알림을 tooall hello 장치 앱을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="447bf-111">When you're finished, you'll be able toouse your notification hub toobroadcast push notifications tooall hello devices running your app.</span></span> <span data-ttu-id="447bf-112">hello 완성 된 코드는 hello에서 사용할 수 있는 [NotificationHubs 앱] [ GitHub] 샘플.</span><span class="sxs-lookup"><span data-stu-id="447bf-112">hello finished code is available in hello [NotificationHubs app][GitHub] sample.</span></span>

<span data-ttu-id="447bf-113">이 자습서는 알림 허브와 hello 간단한 푸시 메시지 브로드캐스트 시나리오를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="447bf-113">This tutorial demonstrates hello simple push message broadcast scenario with Notification Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="447bf-114">필수 조건</span><span class="sxs-lookup"><span data-stu-id="447bf-114">Prerequisites</span></span>
<span data-ttu-id="447bf-115">이 자습서는 hello 다음을 사항이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="447bf-115">This tutorial requires hello following:</span></span>

* <span data-ttu-id="447bf-116">[Xcode 6.0][Install Xcode]</span><span class="sxs-lookup"><span data-stu-id="447bf-116">[Xcode 6.0][Install Xcode]</span></span>
* <span data-ttu-id="447bf-117">iOS 7.0(이상) 호환 장치</span><span class="sxs-lookup"><span data-stu-id="447bf-117">An iOS 7.0 (or later version) compatible device</span></span>
* <span data-ttu-id="447bf-118">iOS 개발자 프로그램 멤버 자격</span><span class="sxs-lookup"><span data-stu-id="447bf-118">iOS Developer Program membership</span></span>
* <span data-ttu-id="447bf-119">[Xamarin Studio]</span><span class="sxs-lookup"><span data-stu-id="447bf-119">[Xamarin Studio]</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="447bf-120">IOS 푸시 알림에 대 한 구성 요구 사항 때문에 배포 하 고 hello 시뮬레이터에서 대신 실제 iOS 장치 (iPhone 또는 iPad) hello 샘플 응용 프로그램을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="447bf-120">Because of configuration requirements for iOS push notifications, you must deploy and test hello sample application on a physical iOS device (iPhone or iPad) instead of in hello simulator.</span></span>
  > 
  > 

<span data-ttu-id="447bf-121">이 자습서를 완료해야 다른 모든 Xamarin.iOS 앱용 알림 허브 자습서를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="447bf-121">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Xamarin iOS apps.</span></span>

[!INCLUDE [Notification Hubs Enable Apple Push Notifications](../../includes/notification-hubs-enable-apple-push-notifications.md)]

## <a name="configure-your-notification-hub"></a><span data-ttu-id="447bf-122">알림 허브 구성</span><span class="sxs-lookup"><span data-stu-id="447bf-122">Configure your notification hub</span></span>
<span data-ttu-id="447bf-123">이 섹션에서는 새 알림 허브 만들기 및 hello를 사용 하 여 APNS를 사용 하 여 인증을 구성 하는 과정을 설명 **.p12** 사용자가 만든 푸시 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="447bf-123">This section walks you through creating a new notification hub and configuring authentication with APNS using hello **.p12** push certificate that you created.</span></span> <span data-ttu-id="447bf-124">이미 만든 알림 허브 toouse 원하는 toostep 5를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="447bf-124">If you want toouse a notification hub that you have already created, you can skip toostep 5.</span></span>

[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="7">

<li>

<p><span data-ttu-id="447bf-125">Hello Azure 포털에서에서 tooconfigure hello APNS 연결을 원하는 대로 ande 클릭 설정에 알림 허브에서 열고 <b>Notification Services</b>, hello를 클릭 한 다음 <b>APNS (Apple)</b> hello 목록에서 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="447bf-125">As we want tooconfigure hello APNS connection, in hello Azure Portal, open your Notification Hub settings, ande click on <b>Notification Services</b>, and then click hello <b>Apple (APNS)</b> item in hello list.</span></span> <span data-ttu-id="447bf-126">완료 되 면 클릭 <b>인증서 업로드</b> 및 선택 hello <b>.p12</b> hello 인증서에 대 한 hello 암호 뿐 아니라 앞에서 내보낸 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="447bf-126">Once done, click on <b>Upload Certificate</b> and select hello <b>.p12</b> certificate that you exported earlier, as well as hello password for hello certificate.</span></span></p>

<p><span data-ttu-id="447bf-127">있는지 tooselect 확인 <b>샌드박스</b> 모드 푸시가 보낼 이후 개발 환경에서 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="447bf-127">Make sure tooselect <b>Sandbox</b> mode since you will be sending push messages in a development environment.</span></span> <span data-ttu-id="447bf-128">만 hello를 사용 하 여 <b>프로덕션</b> hello 스토어에서 앱을 이미 구매한 toosend 푸시 알림을 toousers 하려는 경우 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="447bf-128">Only use hello <b>Production</b> setting if you want toosend push notifications toousers who already purchased your app from hello store.</span></span></p>
</li>
</ol>
<span data-ttu-id="447bf-129">&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-apns.png)</span><span class="sxs-lookup"><span data-stu-id="447bf-129">&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-apns.png)</span></span>

&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-sandbox.png)

<span data-ttu-id="447bf-130">알림 허브는 이제 구성 된 toowork apns, 그리고 푸시 알림을 보낼 및 hello 연결 문자열 tooregister 응용 프로그램을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="447bf-130">Your notification hub is now configured toowork with APNS, and you have hello connection strings tooregister your app and send push notifications.</span></span>

## <a name="connect-your-app-toohello-notification-hub"></a><span data-ttu-id="447bf-131">응용 프로그램 toohello 알림 허브를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="447bf-131">Connect your app toohello notification hub</span></span>
#### <a name="create-a-new-project"></a><span data-ttu-id="447bf-132">새 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="447bf-132">Create a new project</span></span>
1. <span data-ttu-id="447bf-133">Xamarin Studio에서 새 iOS 프로젝트를 만들고 hello 선택 **통합 API** > **단일 보기 응용 프로그램** 템플릿.</span><span class="sxs-lookup"><span data-stu-id="447bf-133">In Xamarin Studio, create a new iOS project and select hello **Unified API** > **Single View Application** template.</span></span>
   
     ![Xamarin Studio - 응용 프로그램 유형 선택][31]
2. <span data-ttu-id="447bf-135">참조 toohello Azure 메시징 구성 요소를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="447bf-135">Add a reference toohello Azure Messaging component.</span></span> <span data-ttu-id="447bf-136">솔루션 뷰 hello hello 마우스 오른쪽 단추로 클릭 **구성 요소** 프로젝트에 대 한 폴더를 선택 하 고 **더 구성 요소 가져오기**합니다.</span><span class="sxs-lookup"><span data-stu-id="447bf-136">In hello Solution view, right-click hello **Components** folder for your project and choose **Get More Components**.</span></span> <span data-ttu-id="447bf-137">Hello에 대 한 검색 **Azure 메시징** 구성 요소 및 hello 구성 요소 tooyour 프로젝트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="447bf-137">Search for hello **Azure Messaging** component and add hello component tooyour project.</span></span>
3. <span data-ttu-id="447bf-138">**AppDelegate.cs**, hello 다음 추가 문을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="447bf-138">In **AppDelegate.cs**, add hello following using statement:</span></span>
   
        using WindowsAzure.Messaging;
4. <span data-ttu-id="447bf-139">**SBNotificationHub**인스턴스를 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="447bf-139">Declare an instance of **SBNotificationHub**:</span></span>
   
        private SBNotificationHub Hub { get; set; }
5. <span data-ttu-id="447bf-140">만들기는 **Constants.cs** hello 다음 변수를 사용 하 여 클래스:</span><span class="sxs-lookup"><span data-stu-id="447bf-140">Create a **Constants.cs** class with hello following variables:</span></span>
   
        // Azure app-specific connection string and hub path
        public const string ConnectionString = "<Azure connection string>";
        public const string NotificationHubPath = "<Azure hub path>";
6. <span data-ttu-id="447bf-141">**AppDelegate.cs**, 업데이트 **FinishedLaunching()** toomatch hello 다음:</span><span class="sxs-lookup"><span data-stu-id="447bf-141">In **AppDelegate.cs**, update **FinishedLaunching()** toomatch hello following:</span></span>
   
        public override bool FinishedLaunching(UIApplication application, NSDictionary launchOptions)
        {
            if (UIDevice.CurrentDevice.CheckSystemVersion (8, 0)) {
                var pushSettings = UIUserNotificationSettings.GetSettingsForTypes (
                       UIUserNotificationType.Alert | UIUserNotificationType.Badge | UIUserNotificationType.Sound,
                       new NSSet ());
   
                UIApplication.SharedApplication.RegisterUserNotificationSettings (pushSettings);
                UIApplication.SharedApplication.RegisterForRemoteNotifications ();
            } else {
                UIRemoteNotificationType notificationTypes = UIRemoteNotificationType.Alert | UIRemoteNotificationType.Badge | UIRemoteNotificationType.Sound;
                UIApplication.SharedApplication.RegisterForRemoteNotificationTypes (notificationTypes);
            }
   
            return true;
        }
7. <span data-ttu-id="447bf-142">Hello 재정의 **RegisteredForRemoteNotifications()** 메서드에서 **AppDelegate.cs**:</span><span class="sxs-lookup"><span data-stu-id="447bf-142">Override hello **RegisteredForRemoteNotifications()** method in **AppDelegate.cs**:</span></span>
   
        public override void RegisteredForRemoteNotifications(UIApplication application, NSData deviceToken)
        {
            Hub = new SBNotificationHub(Constants.ConnectionString, Constants.NotificationHubPath);
   
            Hub.UnregisterAllAsync (deviceToken, (error) => {
                if (error != null)
                {
                    Console.WriteLine("Error calling Unregister: {0}", error.ToString());
                    return;
                }
   
                NSSet tags = null; // create tags if you want
                Hub.RegisterNativeAsync(deviceToken, tags, (errorCallback) => {
                    if (errorCallback != null)
                        Console.WriteLine("RegisterNativeAsync error: " + errorCallback.ToString());
                });
            });
        }
8. <span data-ttu-id="447bf-143">Hello 재정의 **ReceivedRemoteNotification()** 메서드에서 **AppDelegate.cs**:</span><span class="sxs-lookup"><span data-stu-id="447bf-143">Override hello **ReceivedRemoteNotification()** method in **AppDelegate.cs**:</span></span>
   
        public override void ReceivedRemoteNotification(UIApplication application, NSDictionary userInfo)
        {
            ProcessNotification(userInfo, false);
        }
9. <span data-ttu-id="447bf-144">Hello 다음 만들기 **ProcessNotification()** 메서드에서 **AppDelegate.cs**:</span><span class="sxs-lookup"><span data-stu-id="447bf-144">Create hello following **ProcessNotification()** method in **AppDelegate.cs**:</span></span>
   
        void ProcessNotification(NSDictionary options, bool fromFinishedLaunching)
        {
            // Check toosee if hello dictionary has hello aps key.  This is hello notification payload you would have sent
            if (null != options && options.ContainsKey(new NSString("aps")))
            {
                //Get hello aps dictionary
                NSDictionary aps = options.ObjectForKey(new NSString("aps")) as NSDictionary;
   
                string alert = string.Empty;
   
                //Extract hello alert text
                // NOTE: If you're using hello simple alert by just specifying
                // "  aps:{alert:"alert msg here"}  ", this will work fine.
                // But if you're using a complex alert with Localization keys, etc.,
                // your "alert" object from hello aps dictionary will be another NSDictionary.
                // Basically hello JSON gets dumped right into a NSDictionary,
                // so keep that in mind.
                if (aps.ContainsKey(new NSString("alert")))
                    alert = (aps [new NSString("alert")] as NSString).ToString();
   
                //If this came from hello ReceivedRemoteNotification while hello app was running,
                // we of course need toomanually process things like hello sound, badge, and alert.
                if (!fromFinishedLaunching)
                {
                    //Manually show an alert
                    if (!string.IsNullOrEmpty(alert))
                    {
                        UIAlertView avAlert = new UIAlertView("Notification", alert, null, "OK", null);
                        avAlert.Show();
                    }
                }
            }
        }
   
   > [!NOTE]
   > <span data-ttu-id="447bf-145">Toooverride를 선택할 수 있습니다 **FailedToRegisterForRemoteNotifications()** toohandle 느낌표 아이콘 네트워크 연결이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="447bf-145">You can choose toooverride **FailedToRegisterForRemoteNotifications()** toohandle situations such as no network connection.</span></span> <span data-ttu-id="447bf-146">여기서 hello 사용자 (예: 비행기) 오프 라인 모드에서 응용 프로그램을 시작할 수이 고 메시징 시나리오 특정 tooyour 앱 toohandle 푸시 하려는 특히 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="447bf-146">This is especially important where hello user might start your application in offline mode (e.g. Airplane) and you want toohandle push messaging scenarios specific tooyour app.</span></span>
   > 
   > 
10. <span data-ttu-id="447bf-147">Hello 앱이 장치에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="447bf-147">Run hello app on your device.</span></span>

## <a name="sending-push-notifications"></a><span data-ttu-id="447bf-148">푸시 알림 보내기</span><span class="sxs-lookup"><span data-stu-id="447bf-148">Sending Push Notifications</span></span>
<span data-ttu-id="447bf-149">Hello에 알림을 전송 하 여 앱에 푸시 알림을 받는 테스트할 수 [Azure 포털] hello를 통해 **테스트 보내기** hello에서 기능 **문제 해결** 오른쪽 아래의 hello 화면에 표시 된 대로 hello 알림 허브 페이지에서 도구 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="447bf-149">You can test receiving push notifications in your app by sending notifications in hello [Azure Portal] via hello **Test Send** capability in hello **Troubleshooting** toolset, right in hello notification hub page, as shown in hello screen below.</span></span>

![](./media/notification-hubs-ios-get-started/notification-hubs-test-send.png)

<span data-ttu-id="447bf-150">푸시 알림은 일반적으로 호환 라이브러리를 사용하는 모바일 서비스 또는 ASP.NET과 같은 백 엔드 서비스를 통해 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="447bf-150">Push notifications are normally sent through a back-end service like Mobile Services or ASP.NET using a compatible library.</span></span> <span data-ttu-id="447bf-151">또한 toosend 푸시 메시지는 라이브러리 시나리오에서 사용할 수 없는 경우 직접 hello REST API를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="447bf-151">You can also use hello REST API directly toosend push messages if a library is not available in your scenario.</span></span> 

<span data-ttu-id="447bf-152">이 자습서에서는 단순하게 유지 하 고 방금 hello.NET SDK를 사용 하 여 백 엔드 서비스는 대신 콘솔 응용 프로그램에서 알림 허브에 대 한 알림을 전송 하 여 클라이언트 앱을 테스트를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="447bf-152">In this tutorial, we will keep it simple and just demonstrate testing your client app by sending notifications using hello .NET SDK for notification hubs in a console application instead of a backend service.</span></span> <span data-ttu-id="447bf-153">Hello 권장 [사용 하 여 알림 허브 toopush 알림 toousers](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) ASP.NET 백 엔드에서 알림을 보내기 위한 hello 다음 단계로 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="447bf-153">We recommend hello [Use Notification Hubs toopush notifications toousers](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial as hello next step for sending notifications from an ASP.NET backend.</span></span> <span data-ttu-id="447bf-154">그러나 다음 방법 hello 알림을 보내는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="447bf-154">However, hello following approaches can be used for sending notifications:</span></span>

* <span data-ttu-id="447bf-155">**REST 인터페이스**: hello를 사용 하 여 모든 백 엔드 플랫폼에 푸시 알림을 지원할 수 있습니다 [REST 인터페이스](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="447bf-155">**REST Interface**:  You can support push notification on any backend platform using  hello [REST interface](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span></span>
* <span data-ttu-id="447bf-156">**Microsoft Azure 알림 허브.NET SDK**: Visual Studio 용 Nuget 패키지 관리자 hello 실행 [Install-package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)합니다.</span><span class="sxs-lookup"><span data-stu-id="447bf-156">**Microsoft Azure Notification Hubs .NET SDK**: In hello Nuget Package Manager for Visual Studio, run [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>
* <span data-ttu-id="447bf-157">**Node.js** : [어떻게 toouse Node.js에서 알림 허브](notification-hubs-nodejs-push-notification-tutorial.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="447bf-157">**Node.js** : [How toouse Notification Hubs from Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span></span>

<span data-ttu-id="447bf-158">**모바일 앱**: 방법의 예에 대 한 알림 허브와 통합 된 Azure 앱 서비스 모바일 앱 백 엔드에서 toosend 알림을 참조 [추가 tooyour 모바일 앱 푸시 알림](../app-service-mobile/app-service-mobile-ios-get-started-push.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="447bf-158">**Mobile Apps**: For an example of how toosend notifications from an Azure App Service Mobile Apps backend that's integrated with Notification Hubs, see [Add push notifications tooyour mobile app](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span></span>

* <span data-ttu-id="447bf-159">**Java / PHP**: toosend 푸시 알림을 사용 하 여 REST Api를 hello 하는 방법의 예제를 보려면 "어떻게 toouse Java/PHP에서 알림 허브" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span><span class="sxs-lookup"><span data-stu-id="447bf-159">**Java / PHP**: For an example of how toosend push notifications by using hello REST APIs, see "How toouse Notification Hubs from Java/PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span></span>

#### <a name="optional-send-push-notifications-from-a-net-console-app"></a><span data-ttu-id="447bf-160">(선택 사항) .NET 콘솔 앱에서 푸시 알림 보내기</span><span class="sxs-lookup"><span data-stu-id="447bf-160">(Optional) Send Push Notifications from a .NET Console App</span></span>
<span data-ttu-id="447bf-161">이 섹션에서는 간단한 .NET 콘솔 앱을 사용하여 푸시 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="447bf-161">In this section, we will send push notifications by using a simple .NET console app.</span></span> <span data-ttu-id="447bf-162">Hello 목적으로이 예제에서는 Visual Studio가 이미 설치 되어 있는 tooa Windows 개발 환경을 전환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="447bf-162">For hello purposes of this example, we will switch tooa Windows development environment that has Visual Studio already installed.</span></span>

1. <span data-ttu-id="447bf-163">Visual Studio에서 다음과 같이 새로운 Visual C# 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="447bf-163">In Visual Studio, create a new Visual C# console application:</span></span>
   
       ![Visual Studio - Create a new console application][213]
2. <span data-ttu-id="447bf-164">Visual Studio에서 **도구**를 클릭하고 **NuGet 패키지 관리자**를 클릭한 다음 **패키지 관리자 콘솔**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="447bf-164">In Visual Studio, click **Tools**, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="447bf-165">hello 패키지 관리자 콘솔에는 Visual Studio 작업 영역에 도킹 된 toohello 맨 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="447bf-165">hello package manager console should appear docked toohello bottom of your Visual Studio workspace.</span></span>
3. <span data-ttu-id="447bf-166">Hello 패키지 관리자 콘솔 창에서에서 설정 hello **기본 프로젝트** tooyour 새 콘솔 응용 프로그램 프로젝트를 선택한 다음 hello 콘솔 창에 다음 명령을 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="447bf-166">In hello Package Manager Console window, set hello **Default project** tooyour new console application project, and then in hello console window, execute hello following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="447bf-167">이렇게 하면 추가 참조 toohello Azure 알림 허브 SDK hello를 사용 하 여 <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification 허브 NuGet 패키지</a>합니다.</span><span class="sxs-lookup"><span data-stu-id="447bf-167">This adds a reference toohello Azure Notification Hubs SDK using hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. <span data-ttu-id="447bf-168">열기 hello `Program.cs` 파일을 hello 다음 추가 `using` 문을 Azure 클래스와 함수 주 클래스 내에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="447bf-168">Open hello `Program.cs` file and add hello following `using` statement, ensuring that we can use Azure classes and functions within your main class:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="447bf-169">사용자 `Program` 클래스, 메서드 뒤 hello 추가 (tooreplace hello를 잊지 마십시오 **연결 문자열** 및 **허브 이름**):</span><span class="sxs-lookup"><span data-stu-id="447bf-169">In your `Program` class, add hello following method (don't forget tooreplace hello **connection string** and **hub name**):</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            var alert = "{\"aps\":{\"alert\":\"Hello from .NET!\"}}";
            await hub.SendAppleNativeNotificationAsync(alert);
        }
6. <span data-ttu-id="447bf-170">Hello 뒤에 있는 줄을 추가 하면 `Main` 메서드:</span><span class="sxs-lookup"><span data-stu-id="447bf-170">Add hello following lines in your `Main` method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="447bf-171">Hello F5 키 toorun hello 응용 프로그램 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="447bf-171">Press hello F5 key toorun hello app.</span></span> <span data-ttu-id="447bf-172">몇 초 이내에 장치에 푸시 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="447bf-172">Within seconds, you should see a push notification appear on your device.</span></span> <span data-ttu-id="447bf-173">Wi-fi 또는 셀룰러 데이터 네트워크를 사용 하는 지 여부를 hello 장치에서 인터넷에 연결 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="447bf-173">Whether you are using Wi-Fi or a cellular data network, make sure that you have an active internet connection on hello device.</span></span>

<span data-ttu-id="447bf-174">Apple hello에서 모든 hello 가능한 페이로드를 찾을 수 있습니다 [로컬 및 푸시 알림 프로그래밍 가이드]합니다.</span><span class="sxs-lookup"><span data-stu-id="447bf-174">You can find all hello possible payloads in hello Apple [Local and Push Notification Programming Guide].</span></span>

#### <a name="optional-send-notifications-from-a-mobile-service"></a><span data-ttu-id="447bf-175">(선택 사항) 모바일 서비스에서 알림 보내기</span><span class="sxs-lookup"><span data-stu-id="447bf-175">(Optional) Send Notifications from a Mobile Service</span></span>
<span data-ttu-id="447bf-176">이 섹션에서는 노드 스크립트를 통해 모바일 서비스를 사용하여 푸시 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="447bf-176">In this section, we will send push notifications using a mobile service through a node script.</span></span>

<span data-ttu-id="447bf-177">모바일 서비스를 사용 하 여 알림 toosend 따라 [모바일 서비스 시작], 차례로:</span><span class="sxs-lookup"><span data-stu-id="447bf-177">toosend a notification by using a mobile service, follow [Get started with Mobile Services], and then:</span></span>

1. <span data-ttu-id="447bf-178">Toohello 로그인 [Azure 클래식 포털], 모바일 서비스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="447bf-178">Sign in toohello [Azure Classic Portal], and select your mobile service.</span></span>
2. <span data-ttu-id="447bf-179">선택 hello **스케줄러** hello 위에 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="447bf-179">Select hello **Scheduler** tab on hello top.</span></span>
   
       ![Azure Classic Portal - Scheduler][215]
3. <span data-ttu-id="447bf-180">새 예약된 작업을 만들고 이름을 삽입한 후 **요청 시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="447bf-180">Create a new scheduled job, insert a name, and select **On demand**.</span></span>
   
       ![Azure Classic Portal - Create new job][216]
4. <span data-ttu-id="447bf-181">Hello 작업이 만들어질 때 hello 작업 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="447bf-181">When hello job is created, click hello job name.</span></span> <span data-ttu-id="447bf-182">Hello 클릭 **스크립트** hello 위쪽 막대를 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="447bf-182">Then click hello **Script** tab on hello top bar.</span></span>
5. <span data-ttu-id="447bf-183">스케줄러 함수 내 스크립트 다음 hello를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="447bf-183">Insert hello following script inside your scheduler function.</span></span> <span data-ttu-id="447bf-184">알림 허브 이름 및 hello 연결 문자열에 있는 있는지 tooreplace hello 자리 표시자 확인 *DefaultFullSharedAccessSignature* 이전에 얻은입니다.</span><span class="sxs-lookup"><span data-stu-id="447bf-184">Make sure tooreplace hello placeholders with your notification hub name and hello connection string for *DefaultFullSharedAccessSignature* that you obtained earlier.</span></span> <span data-ttu-id="447bf-185">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="447bf-185">Click **Save**.</span></span>
   
        var azure = require('azure');
        var notificationHubService = azure.createNotificationHubService('<Hubname>', '<SAS Full access >');
        notificationHubService.apns.send(
            null,
            {"aps":
                {
                  "alert": "Hello from Mobile Services!"
                }
            },
            function (error)
            {
                if (!error) {
                    console.warn("Notification successful");
                }
            }
        );
6. <span data-ttu-id="447bf-186">클릭 **한 번 실행** hello 아래쪽 표시줄에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="447bf-186">Click **Run Once** on hello bottom bar.</span></span> <span data-ttu-id="447bf-187">장치에 대한 경고를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="447bf-187">You should receive an alert on your device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="447bf-188">다음 단계</span><span class="sxs-lookup"><span data-stu-id="447bf-188">Next steps</span></span>
<span data-ttu-id="447bf-189">이 간단한 예제에서는 푸시 알림을 tooall iOS 장치를 브로드캐스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="447bf-189">In this simple example, you broadcasted push notifications tooall your iOS devices.</span></span> <span data-ttu-id="447bf-190">특정 사용자에 게 tootarget 주문 하 toohello 자습서를 참조 하십시오. [사용 하 여 알림 허브 toopush 알림 toousers]합니다.</span><span class="sxs-lookup"><span data-stu-id="447bf-190">In order tootarget specific users, refer toohello tutorial [Use Notification Hubs toopush notifications toousers].</span></span> <span data-ttu-id="447bf-191">원하는 경우 toosegment 관심 그룹으로 사용자를 읽을 수 있습니다 [최신 뉴스 사용 하 여 알림 허브 toosend]합니다.</span><span class="sxs-lookup"><span data-stu-id="447bf-191">If you want toosegment your users by interest groups, you can read [Use Notification Hubs toosend breaking news].</span></span> <span data-ttu-id="447bf-192">에 대 한 자세한 방법에 대 한 toouse 알림 허브에 [알림 허브 지침] 및 hello [알림 허브 방법 toofor iOS]합니다.</span><span class="sxs-lookup"><span data-stu-id="447bf-192">Learn more about how toouse Notification Hubs in [Notification Hubs Guidance] and in hello [Notification Hubs How-toofor iOS].</span></span>

<!-- Images. -->

[213]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-create-console-app.png

[215]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-scheduler1.png
[216]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-scheduler2.png


[31]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-create-ios-app.png




<!-- URLs. -->
[Mobile Services iOS SDK]: http://go.microsoft.com/fwLink/?LinkID=266533
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[모바일 서비스 시작]: /develop/mobile/tutorials/get-started-xamarin-ios
[Azure 클래식 포털]: https://manage.windowsazure.com/
[알림 허브 지침]: http://msdn.microsoft.com/library/jj927170.aspx
[알림 허브 방법 toofor iOS]: http://msdn.microsoft.com/library/jj927168.aspx
[Install Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[iOS Provisioning Portal]: http://go.microsoft.com/fwlink/p/?LinkId=272456

[사용 하 여 알림 허브 toopush 알림 toousers]: /manage/services/notification-hubs/notify-users-aspnet
[최신 뉴스 사용 하 여 알림 허브 toosend]: /manage/services/notification-hubs/breaking-news-dotnet

[로컬 및 푸시 알림 프로그래밍 가이드]:https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/HandlingRemoteNotifications.html#//apple_ref/doc/uid/TP40008194-CH6-SW1
[Apple Push Notification Service]: http://go.microsoft.com/fwlink/p/?LinkId=272584

[Azure Mobile Services Component]: http://components.xamarin.com/view/azure-mobile-services/
[GitHub]: http://go.microsoft.com/fwlink/p/?LinkId=331329
[Xamarin Studio]: http://xamarin.com/download
[WindowsAzure.Messaging]: https://github.com/infosupport/WindowsAzure.Messaging.iOS
[Azure 포털]: https://portal.azure.com

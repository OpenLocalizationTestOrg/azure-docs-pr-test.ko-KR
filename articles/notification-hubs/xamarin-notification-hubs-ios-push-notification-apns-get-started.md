---
title: "Xamarin 앱용 알림 허브를 사용한 iOS 푸시 알림 | Microsoft Docs"
description: "이 자습서에서 Azure 알림 허브를 사용하여 Xamarin iOS 응용 프로그램에 푸시 알림을 보내는 방법을 알아봅니다."
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
ms.openlocfilehash: 72a81fa0deb34ace77b8fb9b1a4e6b24ee164b35
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="ios-push-notifications-with-notification-hubs-for-xamarin-apps"></a><span data-ttu-id="07682-104">Xamarin 앱용 알림 허브를 사용한 iOS 푸시 알림</span><span class="sxs-lookup"><span data-stu-id="07682-104">iOS Push Notifications with Notification Hubs for Xamarin apps</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="07682-105">개요</span><span class="sxs-lookup"><span data-stu-id="07682-105">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="07682-106">이 자습서를 완료하려면 활성 Azure 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07682-106">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="07682-107">계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07682-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="07682-108">자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="07682-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).</span></span>
> 
> 

<span data-ttu-id="07682-109">이 자습서에서는 Azure 알림 허브를 사용하여 iOS 응용 프로그램에 푸시 알림을 보내는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="07682-109">This tutorial shows you how to use Azure Notification Hubs to send push notifications to an iOS application.</span></span>
<span data-ttu-id="07682-110">[APNS(Apple Push Notification Service)](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html)를 사용하여 푸시 알림을 받는 빈 Xamarin.iOS 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="07682-110">You'll create a blank Xamarin.iOS app that receives push notifications by using the [Apple Push Notification Service (APNs)](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html).</span></span> <span data-ttu-id="07682-111">완료하면 알림 허브를 사용하여 앱을 실행하는 모든 장치로 푸시 알림을 브로드캐스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07682-111">When you're finished, you'll be able to use your notification hub to broadcast push notifications to all the devices running your app.</span></span> <span data-ttu-id="07682-112">완성된 코드는 [NotificationHubs 앱][GitHub] 샘플에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07682-112">The finished code is available in the [NotificationHubs app][GitHub] sample.</span></span>

<span data-ttu-id="07682-113">이 자습서에서는 알림 허브를 사용하는 간단한 푸시 메시지 브로드캐스트 시나리오를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="07682-113">This tutorial demonstrates the simple push message broadcast scenario with Notification Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="07682-114">필수 조건</span><span class="sxs-lookup"><span data-stu-id="07682-114">Prerequisites</span></span>
<span data-ttu-id="07682-115">이 자습서를 사용하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="07682-115">This tutorial requires the following:</span></span>

* <span data-ttu-id="07682-116">[Xcode 6.0][Install Xcode]</span><span class="sxs-lookup"><span data-stu-id="07682-116">[Xcode 6.0][Install Xcode]</span></span>
* <span data-ttu-id="07682-117">iOS 7.0(이상) 호환 장치</span><span class="sxs-lookup"><span data-stu-id="07682-117">An iOS 7.0 (or later version) compatible device</span></span>
* <span data-ttu-id="07682-118">iOS 개발자 프로그램 멤버 자격</span><span class="sxs-lookup"><span data-stu-id="07682-118">iOS Developer Program membership</span></span>
* <span data-ttu-id="07682-119">[Xamarin Studio]</span><span class="sxs-lookup"><span data-stu-id="07682-119">[Xamarin Studio]</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="07682-120">iOS 푸시 알림에 대한 구성 요구 사항 때문에 시뮬레이터 대신 실제 iOS 장치(iPhone 또는 iPad)에서 응용 프로그램 예제를 배포 및 테스트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07682-120">Because of configuration requirements for iOS push notifications, you must deploy and test the sample application on a physical iOS device (iPhone or iPad) instead of in the simulator.</span></span>
  > 
  > 

<span data-ttu-id="07682-121">이 자습서를 완료해야 다른 모든 Xamarin.iOS 앱용 알림 허브 자습서를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07682-121">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Xamarin iOS apps.</span></span>

[!INCLUDE [Notification Hubs Enable Apple Push Notifications](../../includes/notification-hubs-enable-apple-push-notifications.md)]

## <a name="configure-your-notification-hub"></a><span data-ttu-id="07682-122">알림 허브 구성</span><span class="sxs-lookup"><span data-stu-id="07682-122">Configure your notification hub</span></span>
<span data-ttu-id="07682-123">이 섹션에서는 새 알림 허브를 만들고 사용자가 만든 **.p12** 푸시 알림을 사용하여 APNS로 인증을 구성하는 방법을 단계별로 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="07682-123">This section walks you through creating a new notification hub and configuring authentication with APNS using the **.p12** push certificate that you created.</span></span> <span data-ttu-id="07682-124">이미 만든 알림 허브를 사용하려는 경우 5단계로 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07682-124">If you want to use a notification hub that you have already created, you can skip to step 5.</span></span>

[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="7">

<li>

<p><span data-ttu-id="07682-125">APNS 연결을 구성하려면 Azure Portal에서 알림 허브 설정을 열고 <b>알림 서비스</b>를 클릭한 다음 목록에서 <b>Apple(APNS)</b> 항목을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07682-125">As we want to configure the APNS connection, in the Azure Portal, open your Notification Hub settings, ande click on <b>Notification Services</b>, and then click the <b>Apple (APNS)</b> item in the list.</span></span> <span data-ttu-id="07682-126">완료되면 <b>인증서 업로드</b>를 클릭하고 앞서 내보낸 <b>.p12</b> 인증서 및 인증서의 암호를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="07682-126">Once done, click on <b>Upload Certificate</b> and select the <b>.p12</b> certificate that you exported earlier, as well as the password for the certificate.</span></span></p>

<p><span data-ttu-id="07682-127">개발 환경에서 푸시 메시지를 전송 중이므로 <b>샌드박스</b> 모드가 선택되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07682-127">Make sure to select <b>Sandbox</b> mode since you will be sending push messages in a development environment.</span></span> <span data-ttu-id="07682-128">스토어에서 앱을 이미 구매한 사용자에게 푸시 알림을 보내려는 경우에만 <b>프로덕션</b> 설정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="07682-128">Only use the <b>Production</b> setting if you want to send push notifications to users who already purchased your app from the store.</span></span></p>
</li>
</ol>
<span data-ttu-id="07682-129">&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-apns.png)</span><span class="sxs-lookup"><span data-stu-id="07682-129">&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-apns.png)</span></span>

&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-sandbox.png)

<span data-ttu-id="07682-130">이제 알림 허브가 APNS와 작동하도록 구성되었으며 앱을 등록하고 푸시 알림을 보내기 위한 연결 문자열이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07682-130">Your notification hub is now configured to work with APNS, and you have the connection strings to register your app and send push notifications.</span></span>

## <a name="connect-your-app-to-the-notification-hub"></a><span data-ttu-id="07682-131">알림 허브에 앱 연결</span><span class="sxs-lookup"><span data-stu-id="07682-131">Connect your app to the notification hub</span></span>
#### <a name="create-a-new-project"></a><span data-ttu-id="07682-132">새 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="07682-132">Create a new project</span></span>
1. <span data-ttu-id="07682-133">Xamarin Studio에서 새 iOS 프로젝트를 만들고 통합 **API** > **단일 보기 응용 프로그램** 템플릿을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="07682-133">In Xamarin Studio, create a new iOS project and select the **Unified API** > **Single View Application** template.</span></span>
   
     ![Xamarin Studio - 응용 프로그램 유형 선택][31]
2. <span data-ttu-id="07682-135">Azure 메시징 구성 요소에 대한 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="07682-135">Add a reference to the Azure Messaging component.</span></span> <span data-ttu-id="07682-136">솔루션 보기에서 프로젝트에 대한 **구성** 요소 폴더를 마우스 오른쪽 단추로 클릭하고 **구성 요소 더 가져오기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="07682-136">In the Solution view, right-click the **Components** folder for your project and choose **Get More Components**.</span></span> <span data-ttu-id="07682-137">**Azure 메시징** 구성 요소를 검색하여 프로젝트에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="07682-137">Search for the **Azure Messaging** component and add the component to your project.</span></span>
3. <span data-ttu-id="07682-138">**AppDelegate.cs**에서 다음 using 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="07682-138">In **AppDelegate.cs**, add the following using statement:</span></span>
   
        using WindowsAzure.Messaging;
4. <span data-ttu-id="07682-139">**SBNotificationHub**인스턴스를 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="07682-139">Declare an instance of **SBNotificationHub**:</span></span>
   
        private SBNotificationHub Hub { get; set; }
5. <span data-ttu-id="07682-140">다음 변수를 사용하여 **Constants.cs** 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="07682-140">Create a **Constants.cs** class with the following variables:</span></span>
   
        // Azure app-specific connection string and hub path
        public const string ConnectionString = "<Azure connection string>";
        public const string NotificationHubPath = "<Azure hub path>";
6. <span data-ttu-id="07682-141">**AppDelegate.cs**에서 **FinishedLaunching()**을 다음과 일치하도록 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="07682-141">In **AppDelegate.cs**, update **FinishedLaunching()** to match the following:</span></span>
   
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
7. <span data-ttu-id="07682-142">**AppDelegate.cs**의 **RegisteredForRemoteNotifications()** 메서드를 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="07682-142">Override the **RegisteredForRemoteNotifications()** method in **AppDelegate.cs**:</span></span>
   
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
8. <span data-ttu-id="07682-143">**AppDelegate.cs**의 **ReceivedRemoteNotification()** 메서드를 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="07682-143">Override the **ReceivedRemoteNotification()** method in **AppDelegate.cs**:</span></span>
   
        public override void ReceivedRemoteNotification(UIApplication application, NSDictionary userInfo)
        {
            ProcessNotification(userInfo, false);
        }
9. <span data-ttu-id="07682-144">**AppDelegate.cs**에 다음 **ProcessNotification()** 메서드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="07682-144">Create the following **ProcessNotification()** method in **AppDelegate.cs**:</span></span>
   
        void ProcessNotification(NSDictionary options, bool fromFinishedLaunching)
        {
            // Check to see if the dictionary has the aps key.  This is the notification payload you would have sent
            if (null != options && options.ContainsKey(new NSString("aps")))
            {
                //Get the aps dictionary
                NSDictionary aps = options.ObjectForKey(new NSString("aps")) as NSDictionary;
   
                string alert = string.Empty;
   
                //Extract the alert text
                // NOTE: If you're using the simple alert by just specifying
                // "  aps:{alert:"alert msg here"}  ", this will work fine.
                // But if you're using a complex alert with Localization keys, etc.,
                // your "alert" object from the aps dictionary will be another NSDictionary.
                // Basically the JSON gets dumped right into a NSDictionary,
                // so keep that in mind.
                if (aps.ContainsKey(new NSString("alert")))
                    alert = (aps [new NSString("alert")] as NSString).ToString();
   
                //If this came from the ReceivedRemoteNotification while the app was running,
                // we of course need to manually process things like the sound, badge, and alert.
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
   > <span data-ttu-id="07682-145">네트워크 연결이 없는 경우를 처리하도록 **FailedToRegisterForRemoteNotifications()** 를 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07682-145">You can choose to override **FailedToRegisterForRemoteNotifications()** to handle situations such as no network connection.</span></span> <span data-ttu-id="07682-146">사용자가 응용 프로그램을 오프라인 모드(예: 비행기)에서 시작할 수 있고 사용자의 앱에 특정한 푸시 메시징 시나리오를 처리하려는 경우 특히 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="07682-146">This is especially important where the user might start your application in offline mode (e.g. Airplane) and you want to handle push messaging scenarios specific to your app.</span></span>
   > 
   > 
10. <span data-ttu-id="07682-147">장치에서 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="07682-147">Run the app on your device.</span></span>

## <a name="sending-push-notifications"></a><span data-ttu-id="07682-148">푸시 알림 보내기</span><span class="sxs-lookup"><span data-stu-id="07682-148">Sending Push Notifications</span></span>
<span data-ttu-id="07682-149">아래 화면과 같이 바로 알림 허브 페이지에서 **문제 해결** 도구 집합의 **테스트 보내기** 기능을 통해 [Azure Portal]에서 알림을 보내서 앱의 푸시 알림 수신을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07682-149">You can test receiving push notifications in your app by sending notifications in the [Azure Portal] via the **Test Send** capability in the **Troubleshooting** toolset, right in the notification hub page, as shown in the screen below.</span></span>

![](./media/notification-hubs-ios-get-started/notification-hubs-test-send.png)

<span data-ttu-id="07682-150">푸시 알림은 일반적으로 호환 라이브러리를 사용하는 모바일 서비스 또는 ASP.NET과 같은 백 엔드 서비스를 통해 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="07682-150">Push notifications are normally sent through a back-end service like Mobile Services or ASP.NET using a compatible library.</span></span> <span data-ttu-id="07682-151">시나리오에 라이브러리를 사용할 수 없는 경우 직접 REST API를 사용하여 푸시 메시지를 보낼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07682-151">You can also use the REST API directly to send push messages if a library is not available in your scenario.</span></span> 

<span data-ttu-id="07682-152">이 자습서에서는 과정을 단순하게 유지하고 백엔드 서비스 대신 콘솔 응용 프로그램에서 알림 허브에 .NET SDK를 사용하여 알림을 보내서 클라이언트 앱의 테스트만 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="07682-152">In this tutorial, we will keep it simple and just demonstrate testing your client app by sending notifications using the .NET SDK for notification hubs in a console application instead of a backend service.</span></span> <span data-ttu-id="07682-153">ASP.NET 백엔드에서 알림을 보내기 위한 다음 단계로 [Notification Hubs를 사용하여 사용자에게 알림을 푸시](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="07682-153">We recommend the [Use Notification Hubs to push notifications to users](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial as the next step for sending notifications from an ASP.NET backend.</span></span> <span data-ttu-id="07682-154">그러나 다음 접근 방식을 사용하여 알림을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07682-154">However, the following approaches can be used for sending notifications:</span></span>

* <span data-ttu-id="07682-155">**REST 인터페이스**: [REST 인터페이스](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx)를 사용하여 백 엔드 플랫폼에서 푸시 알림을 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07682-155">**REST Interface**:  You can support push notification on any backend platform using  the [REST interface](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span></span>
* <span data-ttu-id="07682-156">**Microsoft Azure 알림 허브 .NET SDK**: Visual Studio용 Nuget 패키지 관리자에서 [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="07682-156">**Microsoft Azure Notification Hubs .NET SDK**: In the Nuget Package Manager for Visual Studio, run [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>
* <span data-ttu-id="07682-157">**Node.js** : [Node.js에서 알림 허브 사용 방법](notification-hubs-nodejs-push-notification-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="07682-157">**Node.js** : [How to use Notification Hubs from Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span></span>

<span data-ttu-id="07682-158">**Mobile Apps**: 알림 허브와 통합된 Azure App Service Mobile Apps 백 엔드에서 알림을 보내는 방법에 대한 예제는 [모바일 앱에 푸시 알림 추가](../app-service-mobile/app-service-mobile-ios-get-started-push.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="07682-158">**Mobile Apps**: For an example of how to send notifications from an Azure App Service Mobile Apps backend that's integrated with Notification Hubs, see [Add push notifications to your mobile app](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span></span>

* <span data-ttu-id="07682-159">**Java / PHP**: REST API를 사용하여 푸시 알림을 보내는 방법에 대한 예는 "Java/PHP에서 알림 허브를 사용하는 방법"([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md))을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="07682-159">**Java / PHP**: For an example of how to send push notifications by using the REST APIs, see "How to use Notification Hubs from Java/PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span></span>

#### <a name="optional-send-push-notifications-from-a-net-console-app"></a><span data-ttu-id="07682-160">(선택 사항) .NET 콘솔 앱에서 푸시 알림 보내기</span><span class="sxs-lookup"><span data-stu-id="07682-160">(Optional) Send Push Notifications from a .NET Console App</span></span>
<span data-ttu-id="07682-161">이 섹션에서는 간단한 .NET 콘솔 앱을 사용하여 푸시 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="07682-161">In this section, we will send push notifications by using a simple .NET console app.</span></span> <span data-ttu-id="07682-162">이 예제에서는 Visual Studio가 이미 설치된 Windows 개발 환경으로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="07682-162">For the purposes of this example, we will switch to a Windows development environment that has Visual Studio already installed.</span></span>

1. <span data-ttu-id="07682-163">Visual Studio에서 다음과 같이 새로운 Visual C# 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="07682-163">In Visual Studio, create a new Visual C# console application:</span></span>
   
       ![Visual Studio - Create a new console application][213]
2. <span data-ttu-id="07682-164">Visual Studio에서 **도구**를 클릭하고 **NuGet 패키지 관리자**를 클릭한 다음 **패키지 관리자 콘솔**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07682-164">In Visual Studio, click **Tools**, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="07682-165">패키지 관리자 콘솔이 Visual Studio 작업 영역 맨 아래에 도킹된 상태로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="07682-165">The package manager console should appear docked to the bottom of your Visual Studio workspace.</span></span>
3. <span data-ttu-id="07682-166">패키지 관리자 콘솔 창에서 **기본 프로젝트** 를 새 콘솔 응용 프로그램 프로젝트로 설정한 후 콘솔 창에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="07682-166">In the Package Manager Console window, set the **Default project** to your new console application project, and then in the console window, execute the following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="07682-167">그러면 <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet 패키지</a>를 사용하는 Azure 알림 허브 SDK에 대한 참조가 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="07682-167">This adds a reference to the Azure Notification Hubs SDK using the <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. <span data-ttu-id="07682-168">`Program.cs` 파일을 열고 다음 `using` 문을 추가하여 기본 클래스 내에서 Azure 클래스 및 함수를 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="07682-168">Open the `Program.cs` file and add the following `using` statement, ensuring that we can use Azure classes and functions within your main class:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="07682-169">사용자의 `Program` 클래스에서 다음 메서드를 추가합니다(**연결 문자열** 및 **허브 이름**을 바꾸는 것을 잊지 마세요).</span><span class="sxs-lookup"><span data-stu-id="07682-169">In your `Program` class, add the following method (don't forget to replace the **connection string** and **hub name**):</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            var alert = "{\"aps\":{\"alert\":\"Hello from .NET!\"}}";
            await hub.SendAppleNativeNotificationAsync(alert);
        }
6. <span data-ttu-id="07682-170">`Main` 메서드에 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="07682-170">Add the following lines in your `Main` method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="07682-171">F5 키를 눌러 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="07682-171">Press the F5 key to run the app.</span></span> <span data-ttu-id="07682-172">몇 초 이내에 장치에 푸시 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="07682-172">Within seconds, you should see a push notification appear on your device.</span></span> <span data-ttu-id="07682-173">Wi-Fi 또는 셀룰러 데이터 네트워크 중 어떤 것을 사용하든지 장치에서 활성화된 인터넷 연결이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07682-173">Whether you are using Wi-Fi or a cellular data network, make sure that you have an active internet connection on the device.</span></span>

<span data-ttu-id="07682-174">Apple [Local and Push Notification Programming Guide]에서 가능한 모든 페이로드를 찾아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07682-174">You can find all the possible payloads in the Apple [Local and Push Notification Programming Guide].</span></span>

#### <a name="optional-send-notifications-from-a-mobile-service"></a><span data-ttu-id="07682-175">(선택 사항) 모바일 서비스에서 알림 보내기</span><span class="sxs-lookup"><span data-stu-id="07682-175">(Optional) Send Notifications from a Mobile Service</span></span>
<span data-ttu-id="07682-176">이 섹션에서는 노드 스크립트를 통해 모바일 서비스를 사용하여 푸시 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="07682-176">In this section, we will send push notifications using a mobile service through a node script.</span></span>

<span data-ttu-id="07682-177">모바일 서비스를 사용하여 알림을 보내려면 [모바일 서비스 시작]을 따른 후 다음을 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="07682-177">To send a notification by using a mobile service, follow [Get started with Mobile Services], and then:</span></span>

1. <span data-ttu-id="07682-178">[Azure 클래식 포털]에 로그인하고 모바일 서비스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="07682-178">Sign in to the [Azure Classic Portal], and select your mobile service.</span></span>
2. <span data-ttu-id="07682-179">맨 위에 있는 **스케줄러** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="07682-179">Select the **Scheduler** tab on the top.</span></span>
   
       ![Azure Classic Portal - Scheduler][215]
3. <span data-ttu-id="07682-180">새 예약된 작업을 만들고 이름을 삽입한 후 **요청 시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="07682-180">Create a new scheduled job, insert a name, and select **On demand**.</span></span>
   
       ![Azure Classic Portal - Create new job][216]
4. <span data-ttu-id="07682-181">작업이 만들어졌으면 작업 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07682-181">When the job is created, click the job name.</span></span> <span data-ttu-id="07682-182">그런 다음 위쪽 막대에서 **스크립트** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07682-182">Then click the **Script** tab on the top bar.</span></span>
5. <span data-ttu-id="07682-183">스케줄러 함수 내에 다음 스크립트를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="07682-183">Insert the following script inside your scheduler function.</span></span> <span data-ttu-id="07682-184">자리 표시자를 알림 허브 이름과 앞에서 얻은 *DefaultFullSharedAccessSignature* 의 연결 문자열로 바꿔야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07682-184">Make sure to replace the placeholders with your notification hub name and the connection string for *DefaultFullSharedAccessSignature* that you obtained earlier.</span></span> <span data-ttu-id="07682-185">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07682-185">Click **Save**.</span></span>
   
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
6. <span data-ttu-id="07682-186">아래쪽 막대에서 **한 번 실행** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07682-186">Click **Run Once** on the bottom bar.</span></span> <span data-ttu-id="07682-187">장치에 대한 경고를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="07682-187">You should receive an alert on your device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="07682-188">다음 단계</span><span class="sxs-lookup"><span data-stu-id="07682-188">Next steps</span></span>
<span data-ttu-id="07682-189">이 간단한 예제에서는 모든 iOS 장치로 포시 알림을 브로드캐스트합니다.</span><span class="sxs-lookup"><span data-stu-id="07682-189">In this simple example, you broadcasted push notifications to all your iOS devices.</span></span> <span data-ttu-id="07682-190">특정 사용자를 대상으로 하려면 [알림 허브를 사용하여 사용자에게 알림 푸시](영문) 자습서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="07682-190">In order to target specific users, refer to the tutorial [Use Notification Hubs to push notifications to users].</span></span> <span data-ttu-id="07682-191">사용자를 관심 그룹별로 분할하려면 [알림 허브를 사용하여 뉴스 속보 보내기](영문)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="07682-191">If you want to segment your users by interest groups, you can read [Use Notification Hubs to send breaking news].</span></span> <span data-ttu-id="07682-192">알림 허브 사용 방법에 대해 자세히 알아보려면 [알림 허브 지침] 및 [iOS용 알림 허브 방법]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="07682-192">Learn more about how to use Notification Hubs in [Notification Hubs Guidance] and in the [Notification Hubs How-To for iOS].</span></span>

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

<span data-ttu-id="07682-193">[모바일 서비스 시작]: /develop/mobile/tutorials/get-started-xamarin-ios</span><span class="sxs-lookup"><span data-stu-id="07682-193">[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-xamarin-ios</span></span>
<span data-ttu-id="07682-194">[Azure 클래식 포털]: https://manage.windowsazure.com/</span><span class="sxs-lookup"><span data-stu-id="07682-194">[Azure Classic Portal]: https://manage.windowsazure.com/</span></span>
<span data-ttu-id="07682-195">[알림 허브 지침]: http://msdn.microsoft.com/library/jj927170.aspx</span><span class="sxs-lookup"><span data-stu-id="07682-195">[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx</span></span>
<span data-ttu-id="07682-196">[iOS용 알림 허브 방법]: http://msdn.microsoft.com/library/jj927168.aspx</span><span class="sxs-lookup"><span data-stu-id="07682-196">[Notification Hubs How-To for iOS]: http://msdn.microsoft.com/library/jj927168.aspx</span></span>
[Install Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[iOS Provisioning Portal]: http://go.microsoft.com/fwlink/p/?LinkId=272456

<span data-ttu-id="07682-197">[알림 허브를 사용하여 사용자에게 알림 푸시]: /manage/services/notification-hubs/notify-users-aspnet</span><span class="sxs-lookup"><span data-stu-id="07682-197">[Use Notification Hubs to push notifications to users]: /manage/services/notification-hubs/notify-users-aspnet</span></span>
<span data-ttu-id="07682-198">[알림 허브를 사용하여 뉴스 속보 보내기]: /manage/services/notification-hubs/breaking-news-dotnet</span><span class="sxs-lookup"><span data-stu-id="07682-198">[Use Notification Hubs to send breaking news]: /manage/services/notification-hubs/breaking-news-dotnet</span></span>

<span data-ttu-id="07682-199">[Local and Push Notification Programming Guide]:https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/HandlingRemoteNotifications.html#//apple_ref/doc/uid/TP40008194-CH6-SW1</span><span class="sxs-lookup"><span data-stu-id="07682-199">[Local and Push Notification Programming Guide]:https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/HandlingRemoteNotifications.html#//apple_ref/doc/uid/TP40008194-CH6-SW1</span></span>
[Apple Push Notification Service]: http://go.microsoft.com/fwlink/p/?LinkId=272584

[Azure Mobile Services Component]: http://components.xamarin.com/view/azure-mobile-services/
[GitHub]: http://go.microsoft.com/fwlink/p/?LinkId=331329
<span data-ttu-id="07682-200">[Xamarin Studio]: http://xamarin.com/download</span><span class="sxs-lookup"><span data-stu-id="07682-200">[Xamarin Studio]: http://xamarin.com/download</span></span>
[WindowsAzure.Messaging]: https://github.com/infosupport/WindowsAzure.Messaging.iOS
<span data-ttu-id="07682-201">[Azure Portal]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="07682-201">[Azure Portal]: https://portal.azure.com</span></span>

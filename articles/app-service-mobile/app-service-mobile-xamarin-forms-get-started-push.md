---
title: "Xamarin.Forms 앱에 푸시 알림 추가 | Microsoft Docs"
description: "Azure 서비스를 사용하여 Xamarin.Forms 앱에 다중 플랫폼 푸시 알림을 전송하는 방법을 알아봅니다."
services: app-service\mobile
documentationcenter: xamarin
author: ysxu
manager: syntaxc4
editor: 
ms.assetid: d9b1ba9a-b3f2-4d12-affc-2ee34311538b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: yuaxu
ms.openlocfilehash: 912367636f1b26b3b07fbd5fe3fe8ed053218fd5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="add-push-notifications-to-your-xamarinforms-app"></a><span data-ttu-id="5c95a-103">Xamarin.Forms 앱에 푸시 알림 추가</span><span class="sxs-lookup"><span data-stu-id="5c95a-103">Add push notifications to your Xamarin.Forms app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="5c95a-104">개요</span><span class="sxs-lookup"><span data-stu-id="5c95a-104">Overview</span></span>
<span data-ttu-id="5c95a-105">이 자습서에서는 [Xamarin.Forms 빠른 시작](app-service-mobile-xamarin-forms-get-started.md)으로 인해 발생한 모든 프로젝트에 푸시 알림을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-105">In this tutorial, you add push notifications to all the projects that resulted from the [Xamarin.Forms quick start](app-service-mobile-xamarin-forms-get-started.md).</span></span> <span data-ttu-id="5c95a-106">즉, 레코드가 삽입될 때마다 모든 플랫폼 간 클라이언트로 푸시 알림이 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-106">This means that a push notification is sent to all cross-platform clients every time a record is inserted.</span></span>

<span data-ttu-id="5c95a-107">다운로드한 빠른 시작 서버 프로젝트를 사용하지 않는 경우 푸시 알림 확장 패키지가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-107">If you do not use the downloaded quick start server project, you will need the push notification extension package.</span></span> <span data-ttu-id="5c95a-108">자세한 내용은 [Azure Mobile Apps용 .NET 백 엔드 서버 SDK 사용](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5c95a-108">For more information, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c95a-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="5c95a-109">Prerequisites</span></span>
<span data-ttu-id="5c95a-110">iOS의 경우 [Apple 개발자 프로그램 멤버 자격](https://developer.apple.com/programs/ios/) 및 실제 iOS 장치가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-110">For iOS, you will need an [Apple Developer Program membership](https://developer.apple.com/programs/ios/) and a physical iOS device.</span></span> <span data-ttu-id="5c95a-111">[iOS 시뮬레이터는 푸시 알림을 지원하지 않습니다](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span><span class="sxs-lookup"><span data-stu-id="5c95a-111">The [iOS simulator does not support push notifications](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span></span>

## <span data-ttu-id="5c95a-112"><a name="configure-hub"></a>알림 허브 구성</span><span class="sxs-lookup"><span data-stu-id="5c95a-112"><a name="configure-hub"></a>Configure a notification hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="update-the-server-project-to-send-push-notifications"></a><span data-ttu-id="5c95a-113">푸시 알림을 전송하도록 서버 프로젝트 업데이트</span><span class="sxs-lookup"><span data-stu-id="5c95a-113">Update the server project to send push notifications</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="configure-and-run-the-android-project-optional"></a><span data-ttu-id="5c95a-114">Android 프로젝트 구성 및 실행(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="5c95a-114">Configure and run the Android project (optional)</span></span>
<span data-ttu-id="5c95a-115">이 섹션을 완료하여 Android용 Xamarin.Forms Droid 프로젝트에 대한 푸시 알림을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-115">Complete this section to enable push notifications for the Xamarin.Forms Droid project for Android.</span></span>

### <a name="enable-firebase-cloud-messaging-fcm"></a><span data-ttu-id="5c95a-116">FCM(Firebase Cloud Messaging) 사용</span><span class="sxs-lookup"><span data-stu-id="5c95a-116">Enable Firebase Cloud Messaging (FCM)</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

### <a name="configure-the-mobile-apps-back-end-to-send-push-requests-by-using-fcm"></a><span data-ttu-id="5c95a-117">FCM을 사용하여 푸시 요청을 보내도록 Mobile Apps 백 엔드 구성</span><span class="sxs-lookup"><span data-stu-id="5c95a-117">Configure the Mobile Apps back end to send push requests by using FCM</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push.md)]

### <a name="add-push-notifications-to-the-android-project"></a><span data-ttu-id="5c95a-118">Android 프로젝트에 푸시 알림 추가</span><span class="sxs-lookup"><span data-stu-id="5c95a-118">Add push notifications to the Android project</span></span>
<span data-ttu-id="5c95a-119">FCM를 사용하여 백 엔드를 구성한 경우 FCM에 등록할 클라이언트에 구성 요소 및 코드를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-119">With the back end configured with FCM, you can add components and codes to the client to register with FCM.</span></span> <span data-ttu-id="5c95a-120">또한 Mobile Apps 백 엔드를 통해 Azure Notification Hubs에 푸시 알림을 등록하고 알림을 수신할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-120">You can also register for push notifications with Azure Notification Hubs through the Mobile Apps back end, and receive notifications.</span></span>

1. <span data-ttu-id="5c95a-121">**Droid** 프로젝트에서 **구성 요소** 폴더를 마우스 오른쪽 단추로 클릭하고 **추가 구성 요소 가져오기...**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-121">In the **Droid** project, right-click the **Components** folder, and click **Get More Components...**.</span></span> <span data-ttu-id="5c95a-122">그런 후 **Google Cloud Messaging 클라이언트** 구성 요소를 검색하고 프로젝트에 구성 요소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-122">Then search for the **Google Cloud Messaging Client** component and add it to the project.</span></span> <span data-ttu-id="5c95a-123">이 구성 요소는 Xamarin Android 프로젝트에 대한 푸시 알림을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-123">This component supports push notifications for a Xamarin Android project.</span></span>
2. <span data-ttu-id="5c95a-124">MainActivity.cs 프로젝트 파일을 열고 파일의 맨 위에 다음 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-124">Open the MainActivity.cs project file, and add the following statement at the top of the file:</span></span>

        using Gcm.Client;
3. <span data-ttu-id="5c95a-125">다음 코드를 **LoadApplication**에 호출한 후에 **OnCreate** 메서드에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-125">Add the following code to the **OnCreate** method after the call to **LoadApplication**:</span></span>

        try
        {
            // Check to ensure everything's set up right
            GcmClient.CheckDevice(this);
            GcmClient.CheckManifest(this);

            // Register for push notifications
            System.Diagnostics.Debug.WriteLine("Registering...");
            GcmClient.Register(this, PushHandlerBroadcastReceiver.SENDER_IDS);
        }
        catch (Java.Net.MalformedURLException)
        {
            CreateAndShowDialog("There was an error creating the client. Verify the URL.", "Error");
        }
        catch (Exception e)
        {
            CreateAndShowDialog(e.Message, "Error");
        }
4. <span data-ttu-id="5c95a-126">새 **CreateAndShowDialog** 도우미 메서드를 다음과 같이 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-126">Add a new **CreateAndShowDialog** helper method, as follows:</span></span>

        private void CreateAndShowDialog(String message, String title)
        {
            AlertDialog.Builder builder = new AlertDialog.Builder(this);

            builder.SetMessage (message);
            builder.SetTitle (title);
            builder.Create().Show ();
        }
5. <span data-ttu-id="5c95a-127">다음 코드를 **MainActivity** 클래스에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-127">Add the following code to the **MainActivity** class:</span></span>

        // Create a new instance field for this activity.
        static MainActivity instance = null;

        // Return the current activity instance.
        public static MainActivity CurrentActivity
        {
            get
            {
                return instance;
            }
        }

    <span data-ttu-id="5c95a-128">현재 **MainActivity** 인스턴스를 노출하므로 주 UI 스레드에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-128">This exposes the current **MainActivity** instance, so we can execute on the main UI thread.</span></span>
6. <span data-ttu-id="5c95a-129">다음과 같이 **OnCreate** 메서드 시작 부분에서 변수 `instance`를 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-129">Initialize the `instance` variable at the beginning of the **OnCreate** method, as follows.</span></span>

        // Set the current instance of MainActivity.
        instance = this;
7. <span data-ttu-id="5c95a-130">새 클래스 파일을 `GcmService.cs`로 명명된 **Droid** 프로젝트에 추가하고 다음 **using** 문이 파일 맨 위에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-130">Add a new class file to the **Droid** project named `GcmService.cs`, and make sure the following **using** statements are present at the top of the file:</span></span>

        using Android.App;
        using Android.Content;
        using Android.Media;
        using Android.Support.V4.App;
        using Android.Util;
        using Gcm.Client;
        using Microsoft.WindowsAzure.MobileServices;
        using Newtonsoft.Json.Linq;
        using System;
        using System.Collections.Generic;
        using System.Diagnostics;
        using System.Text;
8. <span data-ttu-id="5c95a-131">파일의 맨 위에서 **using** 문 뒤의 **네임스페이스** 선언 앞에 다음과 같은 사용 권한 요청을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-131">Add the following permission requests at the top of the file, after the **using** statements and before the **namespace** declaration.</span></span>

        [assembly: Permission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "com.google.android.c2dm.permission.RECEIVE")]
        [assembly: UsesPermission(Name = "android.permission.INTERNET")]
        [assembly: UsesPermission(Name = "android.permission.WAKE_LOCK")]
        //GET_ACCOUNTS is only needed for android versions 4.0.3 and below
        [assembly: UsesPermission(Name = "android.permission.GET_ACCOUNTS")]
9. <span data-ttu-id="5c95a-132">네임스페이스에 다음과 같은 클래스 정의를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-132">Add the following class definition to the namespace.</span></span>

       [BroadcastReceiver(Permission = Gcm.Client.Constants.PERMISSION_GCM_INTENTS)]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_MESSAGE }, Categories = new string[] { "@PACKAGE_NAME@" })]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_REGISTRATION_CALLBACK }, Categories = new string[] { "@PACKAGE_NAME@" })]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_LIBRARY_RETRY }, Categories = new string[] { "@PACKAGE_NAME@" })]
       public class PushHandlerBroadcastReceiver : GcmBroadcastReceiverBase<GcmService>
       {
           public static string[] SENDER_IDS = new string[] { "<PROJECT_NUMBER>" };
       }

   > [!NOTE]
   > <span data-ttu-id="5c95a-133">**<PROJECT_NUMBER>**를 앞에서 설명한 프로젝트 번호로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-133">Replace **<PROJECT_NUMBER>** with your project number you noted earlier.</span></span>    
   >
   >
10. <span data-ttu-id="5c95a-134">빈 **GcmService** 클래스를 새 브로드캐스트 수신기를 사용하는 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-134">Replace the empty **GcmService** class with the following code, which uses the new broadcast receiver:</span></span>

         [Service]
         public class GcmService : GcmServiceBase
         {
             public static string RegistrationID { get; private set; }

             public GcmService()
                 : base(PushHandlerBroadcastReceiver.SENDER_IDS){}
         }
11. <span data-ttu-id="5c95a-135">**GcmService** 클래스에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-135">Add the following code to the **GcmService** class.</span></span> <span data-ttu-id="5c95a-136">이렇게 하면 **OnRegistered** 이벤트 처리기가 재정의되고 **Register** 메서드가 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-136">This overrides the **OnRegistered** event handler and implements a **Register** method.</span></span>

        protected override void OnRegistered(Context context, string registrationId)
        {
            Log.Verbose("PushHandlerBroadcastReceiver", "GCM Registered: " + registrationId);
            RegistrationID = registrationId;

            var push = TodoItemManager.DefaultManager.CurrentClient.GetPush();

            MainActivity.CurrentActivity.RunOnUiThread(() => Register(push, null));
        }

        public async void Register(Microsoft.WindowsAzure.MobileServices.Push push, IEnumerable<string> tags)
        {
            try
            {
                const string templateBodyGCM = "{\"data\":{\"message\":\"$(messageParam)\"}}";

                JObject templates = new JObject();
                templates["genericMessage"] = new JObject
                {
                    {"body", templateBodyGCM}
                };

                await push.RegisterAsync(RegistrationID, templates);
                Log.Info("Push Installation Id", push.InstallationId.ToString());
            }
            catch (Exception ex)
            {
                System.Diagnostics.Debug.WriteLine(ex.Message);
                Debugger.Break();
            }
        }

    <span data-ttu-id="5c95a-137">이 코드는 템플릿 등록에서 `messageParam` 매개 변수를 사용한다는 점에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="5c95a-137">Note that this code uses the `messageParam` parameter in the template registration.</span></span>
12. <span data-ttu-id="5c95a-138">**OnMessage**를 구현하는 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-138">Add the following code that implements **OnMessage**:</span></span>

        protected override void OnMessage(Context context, Intent intent)
        {
            Log.Info("PushHandlerBroadcastReceiver", "GCM Message Received!");

            var msg = new StringBuilder();

            if (intent != null && intent.Extras != null)
            {
                foreach (var key in intent.Extras.KeySet())
                    msg.AppendLine(key + "=" + intent.Extras.Get(key).ToString());
            }

            //Store the message
            var prefs = GetSharedPreferences(context.PackageName, FileCreationMode.Private);
            var edit = prefs.Edit();
            edit.PutString("last_msg", msg.ToString());
            edit.Commit();

            string message = intent.Extras.GetString("message");
            if (!string.IsNullOrEmpty(message))
            {
                createNotification("New todo item!", "Todo item: " + message);
                return;
            }

            string msg2 = intent.Extras.GetString("msg");
            if (!string.IsNullOrEmpty(msg2))
            {
                createNotification("New hub message!", msg2);
                return;
            }

            createNotification("Unknown message details", msg.ToString());
        }

        void createNotification(string title, string desc)
        {
            //Create notification
            var notificationManager = GetSystemService(Context.NotificationService) as NotificationManager;

            //Create an intent to show ui
            var uiIntent = new Intent(this, typeof(MainActivity));

            //Use Notification Builder
            NotificationCompat.Builder builder = new NotificationCompat.Builder(this);

            //Create the notification
            //we use the pending intent, passing our ui intent over which will get called
            //when the notification is tapped.
            var notification = builder.SetContentIntent(PendingIntent.GetActivity(this, 0, uiIntent, 0))
                    .SetSmallIcon(Android.Resource.Drawable.SymActionEmail)
                    .SetTicker(title)
                    .SetContentTitle(title)
                    .SetContentText(desc)

                    //Set the notification sound
                    .SetSound(RingtoneManager.GetDefaultUri(RingtoneType.Notification))

                    //Auto cancel will remove the notification once the user touches it
                    .SetAutoCancel(true).Build();

            //Show the notification
            notificationManager.Notify(1, notification);
        }

    <span data-ttu-id="5c95a-139">이 코드는 들어오는 알림을 처리하고 표시될 알림 관리자로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-139">This handles incoming notifications and sends them to the notification manager to be displayed.</span></span>
13. <span data-ttu-id="5c95a-140">**GcmServiceBase**를 사용하려면 **OnUnRegistered** 및 **OnError** 처리기 메서드를 구현해야 하며 다음과 같이 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-140">**GcmServiceBase** also requires you to implement the **OnUnRegistered** and **OnError** handler methods, which you can do as follows:</span></span>

        protected override void OnUnRegistered(Context context, string registrationId)
        {
            Log.Error("PushHandlerBroadcastReceiver", "Unregistered RegisterationId : " + registrationId);
        }

        protected override void OnError(Context context, string errorId)
        {
            Log.Error("PushHandlerBroadcastReceiver", "GCM Error: " + errorId);
        }

<span data-ttu-id="5c95a-141">이제 Android 장치 또는 에뮬레이터에서 실행 중인 앱에서 푸시 알림을 테스트할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-141">Now, you are ready test push notifications in the app running on an Android device or the emulator.</span></span>

### <a name="test-push-notifications-in-your-android-app"></a><span data-ttu-id="5c95a-142">Android 앱에서 푸시 알림 테스트</span><span class="sxs-lookup"><span data-stu-id="5c95a-142">Test push notifications in your Android app</span></span>
<span data-ttu-id="5c95a-143">처음 두 단계는 에뮬레이터에서 테스트할 때만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-143">The first two steps are required only when you're testing on an emulator.</span></span>

1. <span data-ttu-id="5c95a-144">아래와 같이 Android 가상 장치 관리자에서 대상으로 설정된 Google API가 있는 가상 장치에 배포하거나 해당 가상 장치에서 디버그해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-144">Make sure that you are deploying to or debugging on a virtual device that has Google APIs set as the target, as shown below in the Android Virtual Device manager.</span></span>
2. <span data-ttu-id="5c95a-145">**앱** > **설정** > **계정 추가**를 클릭하여 Android 장치에 Google 계정을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-145">Add a Google account to the Android device by clicking **Apps** > **Settings** > **Add account**.</span></span> <span data-ttu-id="5c95a-146">그런 후 화면 지시에 따라 장치에 기존 Google 계정을 추가하거나 새 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-146">Then follow the prompts to add an existing Google account to the device, or to create a new one.</span></span>
3. <span data-ttu-id="5c95a-147">Visual Studio 또는 Xamarin Studio에서 **Droid** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **시작 프로젝트로 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-147">In Visual Studio or Xamarin Studio, right-click the **Droid** project and click **Set as startup project**.</span></span>
4. <span data-ttu-id="5c95a-148">**실행**을 클릭하여 프로젝트를 빌드하고 Android 장치 또는 에뮬레이터에서 앱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-148">Click **Run** to build the project and start the app on your Android device or emulator.</span></span>
5. <span data-ttu-id="5c95a-149">앱에서 작업을 입력한 다음 더하기(**+**) 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-149">In the app, type a task, and then click the plus (**+**) icon.</span></span>
6. <span data-ttu-id="5c95a-150">항목이 추가될 때 알림을 받았는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-150">Verify that a notification is received when an item is added.</span></span>

## <a name="configure-and-run-the-ios-project-optional"></a><span data-ttu-id="5c95a-151">iOS 프로젝트 구성 및 실행(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="5c95a-151">Configure and run the iOS project (optional)</span></span>
<span data-ttu-id="5c95a-152">이 섹션에서는 iOS 장치용 Xamarin iOS 프로젝트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-152">This section is for running the Xamarin iOS project for iOS devices.</span></span> <span data-ttu-id="5c95a-153">iOS 장치를 작업하지 않는 경우 이 섹션을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-153">You can skip this section if you are not working with iOS devices.</span></span>

[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

#### <a name="configure-the-notification-hub-for-apns"></a><span data-ttu-id="5c95a-154">APNS에 대한 알림 허브 구성</span><span class="sxs-lookup"><span data-stu-id="5c95a-154">Configure the notification hub for APNS</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

<span data-ttu-id="5c95a-155">다음에는 Xamarin Studio 또는 Visual Studio에서 iOS 프로젝트 설정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-155">Next, you will configure the iOS project setting in Xamarin Studio or Visual Studio.</span></span>

[!INCLUDE [app-service-mobile-xamarin-ios-configure-project](../../includes/app-service-mobile-xamarin-ios-configure-project.md)]

#### <a name="add-push-notifications-to-your-ios-app"></a><span data-ttu-id="5c95a-156">iOS 앱에 푸시 알림 추가</span><span class="sxs-lookup"><span data-stu-id="5c95a-156">Add push notifications to your iOS app</span></span>
1. <span data-ttu-id="5c95a-157">**iOS** 프로젝트에서 AppDelegate.cs를 열고 다음 문을 코드 파일의 맨 위에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-157">In the **iOS** project, open AppDelegate.cs and add the following statement to the top of the code file.</span></span>

        using Newtonsoft.Json.Linq;
2. <span data-ttu-id="5c95a-158">또한 **AppDelegate** 클래스에서 **RegisteredForRemoteNotifications** 이벤트 재정의를 추가하여 알림을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-158">In the **AppDelegate** class, add an override for the **RegisteredForRemoteNotifications** event to register for notifications:</span></span>

        public override void RegisteredForRemoteNotifications(UIApplication application,
            NSData deviceToken)
        {
            const string templateBodyAPNS = "{\"aps\":{\"alert\":\"$(messageParam)\"}}";

            JObject templates = new JObject();
            templates["genericMessage"] = new JObject
                {
                  {"body", templateBodyAPNS}
                };

            // Register for push with your mobile app
            Push push = TodoItemManager.DefaultManager.CurrentClient.GetPush();
            push.RegisterAsync(deviceToken, templates);
        }
3. <span data-ttu-id="5c95a-159">**AppDelegate**에서 **DidReceiveRemoteNotification** 이벤트 처리기에 대한 다음 재정의도 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-159">In **AppDelegate**, also add the following override for the **DidReceiveRemoteNotification** event handler:</span></span>

        public override void DidReceiveRemoteNotification(UIApplication application,
            NSDictionary userInfo, Action<UIBackgroundFetchResult> completionHandler)
        {
            NSDictionary aps = userInfo.ObjectForKey(new NSString("aps")) as NSDictionary;

            string alert = string.Empty;
            if (aps.ContainsKey(new NSString("alert")))
                alert = (aps[new NSString("alert")] as NSString).ToString();

            //show alert
            if (!string.IsNullOrEmpty(alert))
            {
                UIAlertView avAlert = new UIAlertView("Notification", alert, null, "OK", null);
                avAlert.Show();
            }
        }

    <span data-ttu-id="5c95a-160">이 메서드는 앱을 실행하는 동안 들어오는 알림을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-160">This method handles incoming notifications while the app is running.</span></span>
4. <span data-ttu-id="5c95a-161">**AppDelegate** 클래스에서 다음 코드를 **FinishedLaunching** 메서드에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-161">In the **AppDelegate** class, add the following code to the **FinishedLaunching** method:</span></span>

        // Register for push notifications.
        var settings = UIUserNotificationSettings.GetSettingsForTypes(
            UIUserNotificationType.Alert
            | UIUserNotificationType.Badge
            | UIUserNotificationType.Sound,
            new NSSet());

        UIApplication.SharedApplication.RegisterUserNotificationSettings(settings);
        UIApplication.SharedApplication.RegisterForRemoteNotifications();

    <span data-ttu-id="5c95a-162">이를 통해 원격 알림을 지원하고 푸시 등록을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-162">This enables support for remote notifications and requests push registration.</span></span>

<span data-ttu-id="5c95a-163">이제 앱이 푸시 알림을 지원하도록 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-163">Your app is now updated to support push notifications.</span></span>

#### <a name="test-push-notifications-in-your-ios-app"></a><span data-ttu-id="5c95a-164">iOS 앱에서 푸시 알림 테스트</span><span class="sxs-lookup"><span data-stu-id="5c95a-164">Test push notifications in your iOS app</span></span>
1. <span data-ttu-id="5c95a-165">iOS 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **시작 프로젝트로 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-165">Right-click the iOS project, and click **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="5c95a-166">Visual Studio에서 **실행** 단추 또는 **F5** 키를 눌러 프로젝트를 빌드하고 iOS 장치에서 앱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-166">Press the **Run** button or **F5** in Visual Studio to build the project and start the app in an iOS device.</span></span> <span data-ttu-id="5c95a-167">그런 다음 **확인**을 클릭하여 푸시 알림을 허용하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-167">Then click **OK** to accept push notifications.</span></span>

   > [!NOTE]
   > <span data-ttu-id="5c95a-168">앱에서 푸시 알림을 명시적으로 수락해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-168">You must explicitly accept push notifications from your app.</span></span> <span data-ttu-id="5c95a-169">이 요청은 앱이 처음 실행될 때만 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-169">This request only occurs the first time that the app runs.</span></span>
   >
   >
3. <span data-ttu-id="5c95a-170">앱에서 작업을 입력한 다음 더하기(**+**) 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-170">In the app, type a task, and then click the plus (**+**) icon.</span></span>
4. <span data-ttu-id="5c95a-171">알림이 수신되는지 확인한 다음 **확인**을 클릭하여 알림을 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-171">Verify that a notification is received, and then click **OK** to dismiss the notification.</span></span>

## <a name="configure-and-run-windows-projects-optional"></a><span data-ttu-id="5c95a-172">Windows 프로젝트 구성 및 실행(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="5c95a-172">Configure and run Windows projects (optional)</span></span>
<span data-ttu-id="5c95a-173">이 섹션에서는 Windows 장치용 Xamarin.Forms WinApp 및 WinPhone81 프로젝트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-173">This section is for running the Xamarin.Forms WinApp and WinPhone81 projects for Windows devices.</span></span> <span data-ttu-id="5c95a-174">이 단계에서는 UWP(범용 Windows 플랫폼) 프로젝트도 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-174">These steps also support Universal Windows Platform (UWP) projects.</span></span> <span data-ttu-id="5c95a-175">Windows 장치를 작업하지 않는 경우 이 섹션을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-175">You can skip this section if you are not working with Windows devices.</span></span>

#### <a name="register-your-windows-app-for-push-notifications-with-windows-notification-service-wns"></a><span data-ttu-id="5c95a-176">WNS(Windows 알림 서비스)를 통한 푸시 알림에 Windows 앱 등록</span><span class="sxs-lookup"><span data-stu-id="5c95a-176">Register your Windows app for push notifications with Windows Notification Service (WNS)</span></span>
[!INCLUDE [app-service-mobile-register-wns](../../includes/app-service-mobile-register-wns.md)]

#### <a name="configure-the-notification-hub-for-wns"></a><span data-ttu-id="5c95a-177">WNS에 대한 알림 허브 구성</span><span class="sxs-lookup"><span data-stu-id="5c95a-177">Configure the notification hub for WNS</span></span>
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

#### <a name="add-push-notifications-to-your-windows-app"></a><span data-ttu-id="5c95a-178">Windows 앱에 푸시 알림 추가</span><span class="sxs-lookup"><span data-stu-id="5c95a-178">Add push notifications to your Windows app</span></span>
1. <span data-ttu-id="5c95a-179">Visual Studio의 Windows 프로젝트에서 **App.xaml.cs**를 열고 다음 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-179">In Visual Studio, open **App.xaml.cs** in a Windows project, and add the following statements.</span></span>

        using Newtonsoft.Json.Linq;
        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
        using Windows.Networking.PushNotifications;
        using <your_TodoItemManager_portable_class_namespace>;

    <span data-ttu-id="5c95a-180">`<your_TodoItemManager_portable_class_namespace>`를 `TodoItemManager` 클래스가 들어 있는 이식 가능 프로젝트의 네임스페이스로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-180">Replace `<your_TodoItemManager_portable_class_namespace>` with the namespace of your portable project that contains the `TodoItemManager` class.</span></span>
2. <span data-ttu-id="5c95a-181">App.xaml.cs에서 다음 **InitNotificationsAsync** 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-181">In App.xaml.cs, add the following **InitNotificationsAsync** method:</span></span>

        private async Task InitNotificationsAsync()
        {
            var channel = await PushNotificationChannelManager
                .CreatePushNotificationChannelForApplicationAsync();

            const string templateBodyWNS =
                "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">$(messageParam)</text></binding></visual></toast>";

            JObject headers = new JObject();
            headers["X-WNS-Type"] = "wns/toast";

            JObject templates = new JObject();
            templates["genericMessage"] = new JObject
            {
                {"body", templateBodyWNS},
                {"headers", headers} // Needed for WNS.
            };

            await TodoItemManager.DefaultManager.CurrentClient.GetPush()
                .RegisterAsync(channel.Uri, templates);
        }

    <span data-ttu-id="5c95a-182">이 메서드는 푸시 알림 채널을 가져오고 알림 허브에서 템플릿 알림을 수신하기 위해 템플릿을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-182">This method gets the push notification channel, and registers a template to receive template notifications from your notification hub.</span></span> <span data-ttu-id="5c95a-183">*messageParam*을 지원하는 템플릿 알림이 이 클라이언트에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-183">A template notification that supports *messageParam* will be delivered to this client.</span></span>
3. <span data-ttu-id="5c95a-184">App.xaml.cs에서 `async` 한정자를 추가하여 **OnLaunched** 이벤트 처리기 메서드 정의를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-184">In App.xaml.cs, update the **OnLaunched** event handler method definition by adding the `async` modifier.</span></span> <span data-ttu-id="5c95a-185">그런 후 다음 코드 줄을 메서드의 끝에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-185">Then add the following line of code at the end of the method:</span></span>

        await InitNotificationsAsync();

    <span data-ttu-id="5c95a-186">이렇게 하면 앱이 시작될 때마다 푸시 알림 등록이 생성되거나 새로 고쳐집니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-186">This ensures that the push notification registration is created or refreshed every time the app is launched.</span></span> <span data-ttu-id="5c95a-187">WNS 푸시 채널이 항상 활성화되도록 이 작업을 수행하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-187">It's important to do this to guarantee that the WNS push channel is always active.</span></span>  
4. <span data-ttu-id="5c95a-188">Visual Studio용 솔루션 탐색기에서 **Package.appxmanifest** 파일을 열고 **알림**에서 **알림 가능**을 **예**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-188">In Solution Explorer for Visual Studio, open the **Package.appxmanifest** file, and set **Toast Capable** to **Yes** under **Notifications**.</span></span>
5. <span data-ttu-id="5c95a-189">앱을 빌드하고 오류가 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-189">Build the app and verify you have no errors.</span></span> <span data-ttu-id="5c95a-190">이제 클라이언트 앱이 Mobile Apps 백 엔드에서 템플릿 알림을 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-190">Your client app should now register for the template notifications from the Mobile Apps back end.</span></span> <span data-ttu-id="5c95a-191">솔루션의 모든 Windows 프로젝트에 대해 이 섹션을 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-191">Repeat this section for every Windows project in your solution.</span></span>

#### <a name="test-push-notifications-in-your-windows-app"></a><span data-ttu-id="5c95a-192">Windows 앱에서 푸시 알림 테스트</span><span class="sxs-lookup"><span data-stu-id="5c95a-192">Test push notifications in your Windows app</span></span>
1. <span data-ttu-id="5c95a-193">Visual Studio에서 Windows 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **시작 프로젝트로 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-193">In Visual Studio, right-click a Windows project, and click **Set as startup project**.</span></span>
2. <span data-ttu-id="5c95a-194">**실행** 단추를 눌러 프로젝트를 빌드하고 앱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-194">Press the **Run** button to build the project and start the app.</span></span>
3. <span data-ttu-id="5c95a-195">앱에서 새 todoitem에 대한 이름을 입력한 다음 더하기(**+**) 아이콘을 클릭하여 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-195">In the app, type a name for a new todoitem, and then click the plus (**+**) icon to add it.</span></span>
4. <span data-ttu-id="5c95a-196">항목이 추가될 때 알림을 받았는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-196">Verify that a notification is received when the item is added.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5c95a-197">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5c95a-197">Next steps</span></span>
<span data-ttu-id="5c95a-198">푸시 알림에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-198">You can learn more about push notifications:</span></span>

* [<span data-ttu-id="5c95a-199">푸시 알림 문제 진단</span><span class="sxs-lookup"><span data-stu-id="5c95a-199">Diagnose push notification issues</span></span>](../notification-hubs/notification-hubs-push-notification-fixer.md)  
  <span data-ttu-id="5c95a-200">장치에서 알림이 삭제되거나 끝나지 않는 다양한 이유가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-200">There are various reasons why notifications may get dropped or do not end up on devices.</span></span> <span data-ttu-id="5c95a-201">이 항목에서는 푸시 알림 실패의 근본 원인을 분석 및 파악하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-201">This topic shows you how to analyze and figure out the root cause of push notification failures.</span></span>

<span data-ttu-id="5c95a-202">다음 자습서 중 하나를 계속 진행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-202">You can also continue on to one of the following tutorials:</span></span>

* [<span data-ttu-id="5c95a-203">앱에 인증 추가 </span><span class="sxs-lookup"><span data-stu-id="5c95a-203">Add authentication to your app </span></span>](app-service-mobile-xamarin-forms-get-started-users.md)  
  <span data-ttu-id="5c95a-204">ID 공급자를 사용하여 앱 사용자를 인증하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-204">Learn how to authenticate users of your app with an identity provider.</span></span>
* [<span data-ttu-id="5c95a-205">앱에 오프라인 동기화 사용</span><span class="sxs-lookup"><span data-stu-id="5c95a-205">Enable offline sync for your app</span></span>](app-service-mobile-xamarin-forms-get-started-offline-data.md)  
  <span data-ttu-id="5c95a-206">Mobile Apps 백 엔드를 사용하여 앱에 오프라인 지원을 추가하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-206">Learn how to add offline support for your app by using a Mobile Apps back end.</span></span> <span data-ttu-id="5c95a-207">오프라인 동기화를 사용하면 사용자는 네트워크에 연결되어 있지 않을 때도 모바일 앱&mdash;데이터 보기, 추가 또는 수정&mdash;과 같은 상호 작용을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c95a-207">With offline sync, users can interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Images. -->

<!-- URLs. -->
[Install Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[Xcode]: https://go.microsoft.com/fwLink/?LinkID=266532
[apns object]: http://go.microsoft.com/fwlink/p/?LinkId=272333

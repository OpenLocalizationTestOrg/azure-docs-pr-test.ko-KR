---
title: "aaaAdd 푸시 알림 tooyour Xamarin.Forms 앱 | Microsoft Docs"
description: "Azure toouse toosend 다중 플랫폼 푸시 알림 tooyour Xamarin.Forms 앱을 서비스 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 9133a0b6dd99c01def525607c20ce5a9c19b9502
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-xamarinforms-app"></a><span data-ttu-id="01568-103">푸시 알림 tooyour Xamarin.Forms 앱 추가</span><span class="sxs-lookup"><span data-stu-id="01568-103">Add push notifications tooyour Xamarin.Forms app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="01568-104">개요</span><span class="sxs-lookup"><span data-stu-id="01568-104">Overview</span></span>
<span data-ttu-id="01568-105">이 자습서에서는 hello에서 발생 하는 푸시 알림 tooall hello 프로젝트 추가한 [Xamarin.Forms 퀵 스타트](app-service-mobile-xamarin-forms-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="01568-105">In this tutorial, you add push notifications tooall hello projects that resulted from hello [Xamarin.Forms quick start](app-service-mobile-xamarin-forms-get-started.md).</span></span> <span data-ttu-id="01568-106">즉, 레코드가 삽입 될 때마다 푸시 알림이 tooall 플랫폼 간 클라이언트 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="01568-106">This means that a push notification is sent tooall cross-platform clients every time a record is inserted.</span></span>

<span data-ttu-id="01568-107">사용 하지 않는 경우 hello 퀵 스타트 서버 프로젝트를 다운로드, 푸시 알림 확장 패키지 hello 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="01568-107">If you do not use hello downloaded quick start server project, you will need hello push notification extension package.</span></span> <span data-ttu-id="01568-108">자세한 내용은 참조 [Azure 모바일 앱에 대 한 hello.NET 백 엔드 서버 SDK에서 작동](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="01568-108">For more information, see [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="01568-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="01568-109">Prerequisites</span></span>
<span data-ttu-id="01568-110">iOS의 경우 [Apple 개발자 프로그램 멤버 자격](https://developer.apple.com/programs/ios/) 및 실제 iOS 장치가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="01568-110">For iOS, you will need an [Apple Developer Program membership](https://developer.apple.com/programs/ios/) and a physical iOS device.</span></span> <span data-ttu-id="01568-111">hello [iOS 시뮬레이터에 푸시 알림을 지원 하지 않는](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="01568-111">hello [iOS simulator does not support push notifications](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span></span>

## <span data-ttu-id="01568-112"><a name="configure-hub"></a>알림 허브 구성</span><span class="sxs-lookup"><span data-stu-id="01568-112"><a name="configure-hub"></a>Configure a notification hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="update-hello-server-project-toosend-push-notifications"></a><span data-ttu-id="01568-113">업데이트 hello 서버 프로젝트 toosend 푸시 알림</span><span class="sxs-lookup"><span data-stu-id="01568-113">Update hello server project toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="configure-and-run-hello-android-project-optional"></a><span data-ttu-id="01568-114">구성 하 고 (선택 사항) hello Android 프로젝트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="01568-114">Configure and run hello Android project (optional)</span></span>
<span data-ttu-id="01568-115">이 섹션 tooenable 푸시 알림을 hello Xamarin.Forms 로봇 프로젝트에 대 한 Android 용를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="01568-115">Complete this section tooenable push notifications for hello Xamarin.Forms Droid project for Android.</span></span>

### <a name="enable-firebase-cloud-messaging-fcm"></a><span data-ttu-id="01568-116">FCM(Firebase Cloud Messaging) 사용</span><span class="sxs-lookup"><span data-stu-id="01568-116">Enable Firebase Cloud Messaging (FCM)</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

### <a name="configure-hello-mobile-apps-back-end-toosend-push-requests-by-using-fcm"></a><span data-ttu-id="01568-117">FCM를 사용 하 여 hello 모바일 앱 백 엔드 toosend 푸시 요청을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="01568-117">Configure hello Mobile Apps back end toosend push requests by using FCM</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push.md)]

### <a name="add-push-notifications-toohello-android-project"></a><span data-ttu-id="01568-118">푸시 알림 toohello Android 프로젝트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="01568-118">Add push notifications toohello Android project</span></span>
<span data-ttu-id="01568-119">Hello 백 엔드에서 FCM를 사용 하 여 구성 된 FCM toohello 클라이언트 tooregister 반환 코드 및 구성 요소를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01568-119">With hello back end configured with FCM, you can add components and codes toohello client tooregister with FCM.</span></span> <span data-ttu-id="01568-120">Azure 알림 허브를 사용 하 여 다시 모바일 앱을 종료 하 고 알림을 받을 hello 통해 푸시 알림을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01568-120">You can also register for push notifications with Azure Notification Hubs through hello Mobile Apps back end, and receive notifications.</span></span>

1. <span data-ttu-id="01568-121">Hello에 **로봇** 프로젝트를 hello를 마우스 오른쪽 단추로 클릭 **구성 요소** 폴더, **더 구성 요소 가져오기...** . Hello에 대 한 다음 검색 **Google 클라우드 메시징 클라이언트** 구성 요소 toohello 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="01568-121">In hello **Droid** project, right-click hello **Components** folder, and click **Get More Components...**. Then search for hello **Google Cloud Messaging Client** component and add it toohello project.</span></span> <span data-ttu-id="01568-122">이 구성 요소는 Xamarin Android 프로젝트에 대한 푸시 알림을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="01568-122">This component supports push notifications for a Xamarin Android project.</span></span>
2. <span data-ttu-id="01568-123">Hello MainActivity.cs 프로젝트 파일을 열고 hello 문 hello 위쪽 hello 파일에 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="01568-123">Open hello MainActivity.cs project file, and add hello following statement at hello top of hello file:</span></span>

        using Gcm.Client;
3. <span data-ttu-id="01568-124">다음 코드 toohello hello 추가 **OnCreate** hello 후 메서드 호출을 통해서도**LoadApplication**:</span><span class="sxs-lookup"><span data-stu-id="01568-124">Add hello following code toohello **OnCreate** method after hello call too**LoadApplication**:</span></span>

        try
        {
            // Check tooensure everything's set up right
            GcmClient.CheckDevice(this);
            GcmClient.CheckManifest(this);

            // Register for push notifications
            System.Diagnostics.Debug.WriteLine("Registering...");
            GcmClient.Register(this, PushHandlerBroadcastReceiver.SENDER_IDS);
        }
        catch (Java.Net.MalformedURLException)
        {
            CreateAndShowDialog("There was an error creating hello client. Verify hello URL.", "Error");
        }
        catch (Exception e)
        {
            CreateAndShowDialog(e.Message, "Error");
        }
4. <span data-ttu-id="01568-125">새 **CreateAndShowDialog** 도우미 메서드를 다음과 같이 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="01568-125">Add a new **CreateAndShowDialog** helper method, as follows:</span></span>

        private void CreateAndShowDialog(String message, String title)
        {
            AlertDialog.Builder builder = new AlertDialog.Builder(this);

            builder.SetMessage (message);
            builder.SetTitle (title);
            builder.Create().Show ();
        }
5. <span data-ttu-id="01568-126">다음 코드 toohello hello 추가 **MainActivity** 클래스:</span><span class="sxs-lookup"><span data-stu-id="01568-126">Add hello following code toohello **MainActivity** class:</span></span>

        // Create a new instance field for this activity.
        static MainActivity instance = null;

        // Return hello current activity instance.
        public static MainActivity CurrentActivity
        {
            get
            {
                return instance;
            }
        }

    <span data-ttu-id="01568-127">Hello 현재 노출 되어 **MainActivity** 인스턴스 없으므로 hello 주 UI 스레드에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01568-127">This exposes hello current **MainActivity** instance, so we can execute on hello main UI thread.</span></span>
6. <span data-ttu-id="01568-128">Hello 초기화 `instance` hello hello 맨 앞에 변수 **OnCreate** 메서드를 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="01568-128">Initialize hello `instance` variable at hello beginning of hello **OnCreate** method, as follows.</span></span>

        // Set hello current instance of MainActivity.
        instance = this;
7. <span data-ttu-id="01568-129">새 클래스 파일 toohello 추가 **로봇** 라는 프로젝트 `GcmService.cs`, 있는지 hello 다음을 확인 하 고 **를 사용 하 여** hello 파일 hello 상단의 문이 있는지:</span><span class="sxs-lookup"><span data-stu-id="01568-129">Add a new class file toohello **Droid** project named `GcmService.cs`, and make sure hello following **using** statements are present at hello top of hello file:</span></span>

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
8. <span data-ttu-id="01568-130">Hello hello 후 권한 요청 hello 위쪽 hello 파일에 다음 추가 **를 사용 하 여** 문을 hello 하기 전에 **네임 스페이스** 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="01568-130">Add hello following permission requests at hello top of hello file, after hello **using** statements and before hello **namespace** declaration.</span></span>

        [assembly: Permission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "com.google.android.c2dm.permission.RECEIVE")]
        [assembly: UsesPermission(Name = "android.permission.INTERNET")]
        [assembly: UsesPermission(Name = "android.permission.WAKE_LOCK")]
        //GET_ACCOUNTS is only needed for android versions 4.0.3 and below
        [assembly: UsesPermission(Name = "android.permission.GET_ACCOUNTS")]
9. <span data-ttu-id="01568-131">클래스 정의 toohello 네임 스페이스 다음 hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="01568-131">Add hello following class definition toohello namespace.</span></span>

       [BroadcastReceiver(Permission = Gcm.Client.Constants.PERMISSION_GCM_INTENTS)]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_MESSAGE }, Categories = new string[] { "@PACKAGE_NAME@" })]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_REGISTRATION_CALLBACK }, Categories = new string[] { "@PACKAGE_NAME@" })]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_LIBRARY_RETRY }, Categories = new string[] { "@PACKAGE_NAME@" })]
       public class PushHandlerBroadcastReceiver : GcmBroadcastReceiverBase<GcmService>
       {
           public static string[] SENDER_IDS = new string[] { "<PROJECT_NUMBER>" };
       }

   > [!NOTE]
   > <span data-ttu-id="01568-132">**<PROJECT_NUMBER>**를 앞에서 설명한 프로젝트 번호로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="01568-132">Replace **<PROJECT_NUMBER>** with your project number you noted earlier.</span></span>    
   >
   >
10. <span data-ttu-id="01568-133">빈 hello 대체 **GcmService** hello 코드 hello 새 브로드캐스트 수신기를 사용 하 여 다음을 사용 하 여 클래스:</span><span class="sxs-lookup"><span data-stu-id="01568-133">Replace hello empty **GcmService** class with hello following code, which uses hello new broadcast receiver:</span></span>

         [Service]
         public class GcmService : GcmServiceBase
         {
             public static string RegistrationID { get; private set; }

             public GcmService()
                 : base(PushHandlerBroadcastReceiver.SENDER_IDS){}
         }
11. <span data-ttu-id="01568-134">다음 코드 toohello hello 추가 **GcmService** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="01568-134">Add hello following code toohello **GcmService** class.</span></span> <span data-ttu-id="01568-135">이 재정의 hello **OnRegistered** 이벤트 처리기를 구현 하는 **등록** 메서드.</span><span class="sxs-lookup"><span data-stu-id="01568-135">This overrides hello **OnRegistered** event handler and implements a **Register** method.</span></span>

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

    <span data-ttu-id="01568-136">이 코드에서는 hello를 사용 하는 참고 `messageParam` hello 템플릿 등록에 대 한 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="01568-136">Note that this code uses hello `messageParam` parameter in hello template registration.</span></span>
12. <span data-ttu-id="01568-137">추가 코드를 구현 하는 다음 hello **OnMessage**:</span><span class="sxs-lookup"><span data-stu-id="01568-137">Add hello following code that implements **OnMessage**:</span></span>

        protected override void OnMessage(Context context, Intent intent)
        {
            Log.Info("PushHandlerBroadcastReceiver", "GCM Message Received!");

            var msg = new StringBuilder();

            if (intent != null && intent.Extras != null)
            {
                foreach (var key in intent.Extras.KeySet())
                    msg.AppendLine(key + "=" + intent.Extras.Get(key).ToString());
            }

            //Store hello message
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

            //Create an intent tooshow ui
            var uiIntent = new Intent(this, typeof(MainActivity));

            //Use Notification Builder
            NotificationCompat.Builder builder = new NotificationCompat.Builder(this);

            //Create hello notification
            //we use hello pending intent, passing our ui intent over which will get called
            //when hello notification is tapped.
            var notification = builder.SetContentIntent(PendingIntent.GetActivity(this, 0, uiIntent, 0))
                    .SetSmallIcon(Android.Resource.Drawable.SymActionEmail)
                    .SetTicker(title)
                    .SetContentTitle(title)
                    .SetContentText(desc)

                    //Set hello notification sound
                    .SetSound(RingtoneManager.GetDefaultUri(RingtoneType.Notification))

                    //Auto cancel will remove hello notification once hello user touches it
                    .SetAutoCancel(true).Build();

            //Show hello notification
            notificationManager.Notify(1, notification);
        }

    <span data-ttu-id="01568-138">들어오는 알림을 처리 하 고 표시 toohello 알림 관리자 toobe 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="01568-138">This handles incoming notifications and sends them toohello notification manager toobe displayed.</span></span>
13. <span data-ttu-id="01568-139">**GcmServiceBase** tooimplement hello 요구 **OnUnRegistered** 및 **OnError** 처리기 메서드를 다음과 같이 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01568-139">**GcmServiceBase** also requires you tooimplement hello **OnUnRegistered** and **OnError** handler methods, which you can do as follows:</span></span>

        protected override void OnUnRegistered(Context context, string registrationId)
        {
            Log.Error("PushHandlerBroadcastReceiver", "Unregistered RegisterationId : " + registrationId);
        }

        protected override void OnError(Context context, string errorId)
        {
            Log.Error("PushHandlerBroadcastReceiver", "GCM Error: " + errorId);
        }

<span data-ttu-id="01568-140">이제 Android 장치에서 실행 중인 hello 앱에 푸시 알림을 준비 테스트는 또는 에뮬레이터 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="01568-140">Now, you are ready test push notifications in hello app running on an Android device or hello emulator.</span></span>

### <a name="test-push-notifications-in-your-android-app"></a><span data-ttu-id="01568-141">Android 앱에서 푸시 알림 테스트</span><span class="sxs-lookup"><span data-stu-id="01568-141">Test push notifications in your Android app</span></span>
<span data-ttu-id="01568-142">hello 처음 두 단계는 에뮬레이터에서 테스트 하는 경우에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="01568-142">hello first two steps are required only when you're testing on an emulator.</span></span>

1. <span data-ttu-id="01568-143">배포 하는 tooor 디버깅 hello Android 가상 장치 관리자에서 다음과 같이 hello 대상으로 설정 하는 Google Api가 가상 장치에 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="01568-143">Make sure that you are deploying tooor debugging on a virtual device that has Google APIs set as hello target, as shown below in hello Android Virtual Device manager.</span></span>
2. <span data-ttu-id="01568-144">Google 계정 toohello Android 장치를 클릭 하 여 추가 **앱** > **설정** > **계정 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="01568-144">Add a Google account toohello Android device by clicking **Apps** > **Settings** > **Add account**.</span></span> <span data-ttu-id="01568-145">그런 다음 따릅니다 hello 프롬프트 tooadd 기존 Google 계정 toohello 장치, 또는 toocreate 새.</span><span class="sxs-lookup"><span data-stu-id="01568-145">Then follow hello prompts tooadd an existing Google account toohello device, or toocreate a new one.</span></span>
3. <span data-ttu-id="01568-146">Visual Studio 또는 Xamarin Studio 단추로 클릭 하 고 hello **로봇** 프로젝트 **시작 프로젝트로 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="01568-146">In Visual Studio or Xamarin Studio, right-click hello **Droid** project and click **Set as startup project**.</span></span>
4. <span data-ttu-id="01568-147">클릭 **실행** toobuild 프로젝트 hello 및 Android 장치 또는 에뮬레이터의 hello 응용 프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="01568-147">Click **Run** toobuild hello project and start hello app on your Android device or emulator.</span></span>
5. <span data-ttu-id="01568-148">Hello 응용 프로그램에서 작업을 입력 한 다음 더하기 hello (**+**) 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="01568-148">In hello app, type a task, and then click hello plus (**+**) icon.</span></span>
6. <span data-ttu-id="01568-149">항목이 추가될 때 알림을 받았는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="01568-149">Verify that a notification is received when an item is added.</span></span>

## <a name="configure-and-run-hello-ios-project-optional"></a><span data-ttu-id="01568-150">구성 하 고 (선택 사항) hello iOS 프로젝트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="01568-150">Configure and run hello iOS project (optional)</span></span>
<span data-ttu-id="01568-151">이 섹션은 iOS 장치에 대 한 hello Xamarin iOS 프로젝트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="01568-151">This section is for running hello Xamarin iOS project for iOS devices.</span></span> <span data-ttu-id="01568-152">iOS 장치를 작업하지 않는 경우 이 섹션을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01568-152">You can skip this section if you are not working with iOS devices.</span></span>

[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

#### <a name="configure-hello-notification-hub-for-apns"></a><span data-ttu-id="01568-153">APNS에 대 한 hello 알림 허브 구성</span><span class="sxs-lookup"><span data-stu-id="01568-153">Configure hello notification hub for APNS</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

<span data-ttu-id="01568-154">다음으로, Xamarin Studio 또는 Visual Studio에서 hello iOS 프로젝트 설정을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="01568-154">Next, you will configure hello iOS project setting in Xamarin Studio or Visual Studio.</span></span>

[!INCLUDE [app-service-mobile-xamarin-ios-configure-project](../../includes/app-service-mobile-xamarin-ios-configure-project.md)]

#### <a name="add-push-notifications-tooyour-ios-app"></a><span data-ttu-id="01568-155">푸시 알림 tooyour iOS 앱 추가</span><span class="sxs-lookup"><span data-stu-id="01568-155">Add push notifications tooyour iOS app</span></span>
1. <span data-ttu-id="01568-156">Hello에 **iOS** 프로젝트 AppDelegate.cs 연 hello hello 코드 파일의 문 toohello 맨 위에 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="01568-156">In hello **iOS** project, open AppDelegate.cs and add hello following statement toohello top of hello code file.</span></span>

        using Newtonsoft.Json.Linq;
2. <span data-ttu-id="01568-157">Hello에 **AppDelegate** 클래스 hello에 대 한 재정의 추가, **RegisteredForRemoteNotifications** 알림에 대 한 이벤트 tooregister:</span><span class="sxs-lookup"><span data-stu-id="01568-157">In hello **AppDelegate** class, add an override for hello **RegisteredForRemoteNotifications** event tooregister for notifications:</span></span>

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
3. <span data-ttu-id="01568-158">**AppDelegate**를 추가적으로 hello에 대 한 재정의 수행 하는 hello **DidReceiveRemoteNotification** 이벤트 처리기.</span><span class="sxs-lookup"><span data-stu-id="01568-158">In **AppDelegate**, also add hello following override for hello **DidReceiveRemoteNotification** event handler:</span></span>

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

    <span data-ttu-id="01568-159">이 메서드는 hello 응용 프로그램을 실행 하는 동안 받는 알림을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="01568-159">This method handles incoming notifications while hello app is running.</span></span>
4. <span data-ttu-id="01568-160">Hello에 **AppDelegate** 클래스, 다음 코드 toohello hello 추가 **FinishedLaunching** 메서드:</span><span class="sxs-lookup"><span data-stu-id="01568-160">In hello **AppDelegate** class, add hello following code toohello **FinishedLaunching** method:</span></span>

        // Register for push notifications.
        var settings = UIUserNotificationSettings.GetSettingsForTypes(
            UIUserNotificationType.Alert
            | UIUserNotificationType.Badge
            | UIUserNotificationType.Sound,
            new NSSet());

        UIApplication.SharedApplication.RegisterUserNotificationSettings(settings);
        UIApplication.SharedApplication.RegisterForRemoteNotifications();

    <span data-ttu-id="01568-161">이를 통해 원격 알림을 지원하고 푸시 등록을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="01568-161">This enables support for remote notifications and requests push registration.</span></span>

<span data-ttu-id="01568-162">앱 업데이트 toosupport 푸시 알림이 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="01568-162">Your app is now updated toosupport push notifications.</span></span>

#### <a name="test-push-notifications-in-your-ios-app"></a><span data-ttu-id="01568-163">iOS 앱에서 푸시 알림 테스트</span><span class="sxs-lookup"><span data-stu-id="01568-163">Test push notifications in your iOS app</span></span>
1. <span data-ttu-id="01568-164">Hello iOS 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 **시작 프로젝트로 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="01568-164">Right-click hello iOS project, and click **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="01568-165">키를 눌러 hello **실행** 단추 또는 **F5** Visual Studio에서 toobuild 프로젝트 hello 및 iOS 장치에서 hello 응용 프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="01568-165">Press hello **Run** button or **F5** in Visual Studio toobuild hello project and start hello app in an iOS device.</span></span> <span data-ttu-id="01568-166">클릭 **확인** tooaccept 푸시 알림을 합니다.</span><span class="sxs-lookup"><span data-stu-id="01568-166">Then click **OK** tooaccept push notifications.</span></span>

   > [!NOTE]
   > <span data-ttu-id="01568-167">앱에서 푸시 알림을 명시적으로 수락해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="01568-167">You must explicitly accept push notifications from your app.</span></span> <span data-ttu-id="01568-168">이 요청은만 hello 앱이 실행 hello 처음으로 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="01568-168">This request only occurs hello first time that hello app runs.</span></span>
   >
   >
3. <span data-ttu-id="01568-169">Hello 응용 프로그램에서 작업을 입력 한 다음 더하기 hello (**+**) 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="01568-169">In hello app, type a task, and then click hello plus (**+**) icon.</span></span>
4. <span data-ttu-id="01568-170">알림이 수신 되 고 클릭 한 다음 확인 **확인** toodismiss hello 알림입니다.</span><span class="sxs-lookup"><span data-stu-id="01568-170">Verify that a notification is received, and then click **OK** toodismiss hello notification.</span></span>

## <a name="configure-and-run-windows-projects-optional"></a><span data-ttu-id="01568-171">Windows 프로젝트 구성 및 실행(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="01568-171">Configure and run Windows projects (optional)</span></span>
<span data-ttu-id="01568-172">Windows 장치에 대 한 Xamarin.Forms WinApp 및 WinPhone81 프로젝트 hello를 실행 하기 위한이 섹션이입니다.</span><span class="sxs-lookup"><span data-stu-id="01568-172">This section is for running hello Xamarin.Forms WinApp and WinPhone81 projects for Windows devices.</span></span> <span data-ttu-id="01568-173">이 단계에서는 UWP(범용 Windows 플랫폼) 프로젝트도 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="01568-173">These steps also support Universal Windows Platform (UWP) projects.</span></span> <span data-ttu-id="01568-174">Windows 장치를 작업하지 않는 경우 이 섹션을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01568-174">You can skip this section if you are not working with Windows devices.</span></span>

#### <a name="register-your-windows-app-for-push-notifications-with-windows-notification-service-wns"></a><span data-ttu-id="01568-175">WNS(Windows 알림 서비스)를 통한 푸시 알림에 Windows 앱 등록</span><span class="sxs-lookup"><span data-stu-id="01568-175">Register your Windows app for push notifications with Windows Notification Service (WNS)</span></span>
[!INCLUDE [app-service-mobile-register-wns](../../includes/app-service-mobile-register-wns.md)]

#### <a name="configure-hello-notification-hub-for-wns"></a><span data-ttu-id="01568-176">Wns hello 알림 허브를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="01568-176">Configure hello notification hub for WNS</span></span>
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

#### <a name="add-push-notifications-tooyour-windows-app"></a><span data-ttu-id="01568-177">푸시 알림 tooyour Windows 앱 추가</span><span class="sxs-lookup"><span data-stu-id="01568-177">Add push notifications tooyour Windows app</span></span>
1. <span data-ttu-id="01568-178">Visual Studio에서 열고 **App.xaml.cs** windows에서 프로젝트를 연 다음 조건 hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="01568-178">In Visual Studio, open **App.xaml.cs** in a Windows project, and add hello following statements.</span></span>

        using Newtonsoft.Json.Linq;
        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
        using Windows.Networking.PushNotifications;
        using <your_TodoItemManager_portable_class_namespace>;

    <span data-ttu-id="01568-179">대체 `<your_TodoItemManager_portable_class_namespace>` hello 포함 된 이식 가능한 프로젝트의 hello 네임 스페이스를 가진 `TodoItemManager` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="01568-179">Replace `<your_TodoItemManager_portable_class_namespace>` with hello namespace of your portable project that contains hello `TodoItemManager` class.</span></span>
2. <span data-ttu-id="01568-180">App.xaml.cs에서 hello 다음 추가 **InitNotificationsAsync** 메서드:</span><span class="sxs-lookup"><span data-stu-id="01568-180">In App.xaml.cs, add hello following **InitNotificationsAsync** method:</span></span>

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

    <span data-ttu-id="01568-181">이 메서드는 hello 푸시 알림 채널을 가져오고 알림 허브에서 템플릿 tooreceive 템플릿 알림을 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="01568-181">This method gets hello push notification channel, and registers a template tooreceive template notifications from your notification hub.</span></span> <span data-ttu-id="01568-182">지원 되는 템플릿 알림을 *messageParam* toothis 클라이언트 배달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="01568-182">A template notification that supports *messageParam* will be delivered toothis client.</span></span>
3. <span data-ttu-id="01568-183">App.xaml.cs, 업데이트 hello **OnLaunched** hello를 추가 하 여 이벤트 처리기 메서드 정의 `async` 한정자입니다.</span><span class="sxs-lookup"><span data-stu-id="01568-183">In App.xaml.cs, update hello **OnLaunched** event handler method definition by adding hello `async` modifier.</span></span> <span data-ttu-id="01568-184">Hello 다음 hello 메서드의 hello 끝에 코드 줄을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="01568-184">Then add hello following line of code at hello end of hello method:</span></span>

        await InitNotificationsAsync();

    <span data-ttu-id="01568-185">이렇게 하면 hello 푸시 알림 등록이 생성 되었거나 hello 앱이 시작 될 때마다 새로 고쳐집니다.</span><span class="sxs-lookup"><span data-stu-id="01568-185">This ensures that hello push notification registration is created or refreshed every time hello app is launched.</span></span> <span data-ttu-id="01568-186">반드시 toodo WNS 푸시 채널 hello이 tooguarantee 항상 활성화 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01568-186">It's important toodo this tooguarantee that hello WNS push channel is always active.</span></span>  
4. <span data-ttu-id="01568-187">Visual Studio의 솔루션 탐색기를 열고 hello **Package.appxmanifest** 파일, 설정 및 **알림 가능** 너무**예** 아래 **알림**.</span><span class="sxs-lookup"><span data-stu-id="01568-187">In Solution Explorer for Visual Studio, open hello **Package.appxmanifest** file, and set **Toast Capable** too**Yes** under **Notifications**.</span></span>
5. <span data-ttu-id="01568-188">Hello 앱을 빌드하고 오류가 없는지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="01568-188">Build hello app and verify you have no errors.</span></span> <span data-ttu-id="01568-189">클라이언트 앱 알림에 대 한 hello 템플릿 hello 모바일 앱을 다시 종료 이제 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="01568-189">Your client app should now register for hello template notifications from hello Mobile Apps back end.</span></span> <span data-ttu-id="01568-190">솔루션의 모든 Windows 프로젝트에 대해 이 섹션을 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="01568-190">Repeat this section for every Windows project in your solution.</span></span>

#### <a name="test-push-notifications-in-your-windows-app"></a><span data-ttu-id="01568-191">Windows 앱에서 푸시 알림 테스트</span><span class="sxs-lookup"><span data-stu-id="01568-191">Test push notifications in your Windows app</span></span>
1. <span data-ttu-id="01568-192">Visual Studio에서 Windows 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **시작 프로젝트로 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="01568-192">In Visual Studio, right-click a Windows project, and click **Set as startup project**.</span></span>
2. <span data-ttu-id="01568-193">키를 눌러 hello **실행** toobuild hello 프로젝트 단추 및 hello 응용 프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="01568-193">Press hello **Run** button toobuild hello project and start hello app.</span></span>
3. <span data-ttu-id="01568-194">Hello 응용 프로그램에서 새 todoitem에 대 한 이름을 입력 한 다음 더하기 hello (**+**) 아이콘 tooadd 것입니다.</span><span class="sxs-lookup"><span data-stu-id="01568-194">In hello app, type a name for a new todoitem, and then click hello plus (**+**) icon tooadd it.</span></span>
4. <span data-ttu-id="01568-195">Hello 항목이 추가 될 때 알림을 받았는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="01568-195">Verify that a notification is received when hello item is added.</span></span>

## <a name="next-steps"></a><span data-ttu-id="01568-196">다음 단계</span><span class="sxs-lookup"><span data-stu-id="01568-196">Next steps</span></span>
<span data-ttu-id="01568-197">푸시 알림에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="01568-197">You can learn more about push notifications:</span></span>

* [<span data-ttu-id="01568-198">푸시 알림 문제 진단</span><span class="sxs-lookup"><span data-stu-id="01568-198">Diagnose push notification issues</span></span>](../notification-hubs/notification-hubs-push-notification-fixer.md)  
  <span data-ttu-id="01568-199">장치에서 알림이 삭제되거나 끝나지 않는 다양한 이유가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01568-199">There are various reasons why notifications may get dropped or do not end up on devices.</span></span> <span data-ttu-id="01568-200">이 항목에서는 tooanalyze 및 hello 루트 계산 푸시 알림 오류의 발생 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="01568-200">This topic shows you how tooanalyze and figure out hello root cause of push notification failures.</span></span>

<span data-ttu-id="01568-201">자습서를 따라 hello의 tooone을 계속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01568-201">You can also continue on tooone of hello following tutorials:</span></span>

* [<span data-ttu-id="01568-202">인증 tooyour 앱 추가</span><span class="sxs-lookup"><span data-stu-id="01568-202">Add authentication tooyour app </span></span>](app-service-mobile-xamarin-forms-get-started-users.md)  
  <span data-ttu-id="01568-203">자세한 내용은 방법 tooauthenticate 사용자가 id 공급자로 사용 하 여 앱의 합니다.</span><span class="sxs-lookup"><span data-stu-id="01568-203">Learn how tooauthenticate users of your app with an identity provider.</span></span>
* [<span data-ttu-id="01568-204">앱에 오프라인 동기화 사용</span><span class="sxs-lookup"><span data-stu-id="01568-204">Enable offline sync for your app</span></span>](app-service-mobile-xamarin-forms-get-started-offline-data.md)  
  <span data-ttu-id="01568-205">자세한 방법을 모바일 앱을 사용 하 여 앱에 대 한 오프 라인 지원 tooadd 백 엔드 합니다.</span><span class="sxs-lookup"><span data-stu-id="01568-205">Learn how tooadd offline support for your app by using a Mobile Apps back end.</span></span> <span data-ttu-id="01568-206">오프라인 동기화를 사용하면 사용자는 네트워크에 연결되어 있지 않을 때도 모바일 앱&mdash;데이터 보기, 추가 또는 수정&mdash;과 같은 상호 작용을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01568-206">With offline sync, users can interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Images. -->

<!-- URLs. -->
[Install Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[Xcode]: https://go.microsoft.com/fwLink/?LinkID=266532
[apns object]: http://go.microsoft.com/fwlink/p/?LinkId=272333

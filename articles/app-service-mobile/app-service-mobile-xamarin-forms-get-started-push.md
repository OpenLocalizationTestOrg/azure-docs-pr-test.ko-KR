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
# <a name="add-push-notifications-tooyour-xamarinforms-app"></a>푸시 알림 tooyour Xamarin.Forms 앱 추가
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>개요
이 자습서에서는 hello에서 발생 하는 푸시 알림 tooall hello 프로젝트 추가한 [Xamarin.Forms 퀵 스타트](app-service-mobile-xamarin-forms-get-started.md)합니다. 즉, 레코드가 삽입 될 때마다 푸시 알림이 tooall 플랫폼 간 클라이언트 전송 됩니다.

사용 하지 않는 경우 hello 퀵 스타트 서버 프로젝트를 다운로드, 푸시 알림 확장 패키지 hello 필요 합니다. 자세한 내용은 참조 [Azure 모바일 앱에 대 한 hello.NET 백 엔드 서버 SDK에서 작동](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md)합니다.

## <a name="prerequisites"></a>필수 조건
iOS의 경우 [Apple 개발자 프로그램 멤버 자격](https://developer.apple.com/programs/ios/) 및 실제 iOS 장치가 필요합니다. hello [iOS 시뮬레이터에 푸시 알림을 지원 하지 않는](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html)합니다.

## <a name="configure-hub"></a>알림 허브 구성
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="update-hello-server-project-toosend-push-notifications"></a>업데이트 hello 서버 프로젝트 toosend 푸시 알림
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="configure-and-run-hello-android-project-optional"></a>구성 하 고 (선택 사항) hello Android 프로젝트를 실행 합니다.
이 섹션 tooenable 푸시 알림을 hello Xamarin.Forms 로봇 프로젝트에 대 한 Android 용를 완료 합니다.

### <a name="enable-firebase-cloud-messaging-fcm"></a>FCM(Firebase Cloud Messaging) 사용
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

### <a name="configure-hello-mobile-apps-back-end-toosend-push-requests-by-using-fcm"></a>FCM를 사용 하 여 hello 모바일 앱 백 엔드 toosend 푸시 요청을 구성 합니다.
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push.md)]

### <a name="add-push-notifications-toohello-android-project"></a>푸시 알림 toohello Android 프로젝트를 추가 합니다.
Hello 백 엔드에서 FCM를 사용 하 여 구성 된 FCM toohello 클라이언트 tooregister 반환 코드 및 구성 요소를 추가할 수 있습니다. Azure 알림 허브를 사용 하 여 다시 모바일 앱을 종료 하 고 알림을 받을 hello 통해 푸시 알림을 등록할 수 있습니다.

1. Hello에 **로봇** 프로젝트를 hello를 마우스 오른쪽 단추로 클릭 **구성 요소** 폴더, **더 구성 요소 가져오기...** . Hello에 대 한 다음 검색 **Google 클라우드 메시징 클라이언트** 구성 요소 toohello 프로젝트에 추가 합니다. 이 구성 요소는 Xamarin Android 프로젝트에 대한 푸시 알림을 지원합니다.
2. Hello MainActivity.cs 프로젝트 파일을 열고 hello 문 hello 위쪽 hello 파일에 다음을 추가 합니다.

        using Gcm.Client;
3. 다음 코드 toohello hello 추가 **OnCreate** hello 후 메서드 호출을 통해서도**LoadApplication**:

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
4. 새 **CreateAndShowDialog** 도우미 메서드를 다음과 같이 추가합니다.

        private void CreateAndShowDialog(String message, String title)
        {
            AlertDialog.Builder builder = new AlertDialog.Builder(this);

            builder.SetMessage (message);
            builder.SetTitle (title);
            builder.Create().Show ();
        }
5. 다음 코드 toohello hello 추가 **MainActivity** 클래스:

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

    Hello 현재 노출 되어 **MainActivity** 인스턴스 없으므로 hello 주 UI 스레드에서 실행할 수 있습니다.
6. Hello 초기화 `instance` hello hello 맨 앞에 변수 **OnCreate** 메서드를 다음과 같이 합니다.

        // Set hello current instance of MainActivity.
        instance = this;
7. 새 클래스 파일 toohello 추가 **로봇** 라는 프로젝트 `GcmService.cs`, 있는지 hello 다음을 확인 하 고 **를 사용 하 여** hello 파일 hello 상단의 문이 있는지:

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
8. Hello hello 후 권한 요청 hello 위쪽 hello 파일에 다음 추가 **를 사용 하 여** 문을 hello 하기 전에 **네임 스페이스** 선언 합니다.

        [assembly: Permission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "com.google.android.c2dm.permission.RECEIVE")]
        [assembly: UsesPermission(Name = "android.permission.INTERNET")]
        [assembly: UsesPermission(Name = "android.permission.WAKE_LOCK")]
        //GET_ACCOUNTS is only needed for android versions 4.0.3 and below
        [assembly: UsesPermission(Name = "android.permission.GET_ACCOUNTS")]
9. 클래스 정의 toohello 네임 스페이스 다음 hello를 추가 합니다.

       [BroadcastReceiver(Permission = Gcm.Client.Constants.PERMISSION_GCM_INTENTS)]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_MESSAGE }, Categories = new string[] { "@PACKAGE_NAME@" })]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_REGISTRATION_CALLBACK }, Categories = new string[] { "@PACKAGE_NAME@" })]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_LIBRARY_RETRY }, Categories = new string[] { "@PACKAGE_NAME@" })]
       public class PushHandlerBroadcastReceiver : GcmBroadcastReceiverBase<GcmService>
       {
           public static string[] SENDER_IDS = new string[] { "<PROJECT_NUMBER>" };
       }

   > [!NOTE]
   > **<PROJECT_NUMBER>**를 앞에서 설명한 프로젝트 번호로 바꿉니다.    
   >
   >
10. 빈 hello 대체 **GcmService** hello 코드 hello 새 브로드캐스트 수신기를 사용 하 여 다음을 사용 하 여 클래스:

         [Service]
         public class GcmService : GcmServiceBase
         {
             public static string RegistrationID { get; private set; }

             public GcmService()
                 : base(PushHandlerBroadcastReceiver.SENDER_IDS){}
         }
11. 다음 코드 toohello hello 추가 **GcmService** 클래스입니다. 이 재정의 hello **OnRegistered** 이벤트 처리기를 구현 하는 **등록** 메서드.

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

    이 코드에서는 hello를 사용 하는 참고 `messageParam` hello 템플릿 등록에 대 한 매개 변수입니다.
12. 추가 코드를 구현 하는 다음 hello **OnMessage**:

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

    들어오는 알림을 처리 하 고 표시 toohello 알림 관리자 toobe 보냅니다.
13. **GcmServiceBase** tooimplement hello 요구 **OnUnRegistered** 및 **OnError** 처리기 메서드를 다음과 같이 수행할 수 있습니다.

        protected override void OnUnRegistered(Context context, string registrationId)
        {
            Log.Error("PushHandlerBroadcastReceiver", "Unregistered RegisterationId : " + registrationId);
        }

        protected override void OnError(Context context, string errorId)
        {
            Log.Error("PushHandlerBroadcastReceiver", "GCM Error: " + errorId);
        }

이제 Android 장치에서 실행 중인 hello 앱에 푸시 알림을 준비 테스트는 또는 에뮬레이터 hello 합니다.

### <a name="test-push-notifications-in-your-android-app"></a>Android 앱에서 푸시 알림 테스트
hello 처음 두 단계는 에뮬레이터에서 테스트 하는 경우에 필요 합니다.

1. 배포 하는 tooor 디버깅 hello Android 가상 장치 관리자에서 다음과 같이 hello 대상으로 설정 하는 Google Api가 가상 장치에 있는지 확인 합니다.
2. Google 계정 toohello Android 장치를 클릭 하 여 추가 **앱** > **설정** > **계정 추가**합니다. 그런 다음 따릅니다 hello 프롬프트 tooadd 기존 Google 계정 toohello 장치, 또는 toocreate 새.
3. Visual Studio 또는 Xamarin Studio 단추로 클릭 하 고 hello **로봇** 프로젝트 **시작 프로젝트로 설정**합니다.
4. 클릭 **실행** toobuild 프로젝트 hello 및 Android 장치 또는 에뮬레이터의 hello 응용 프로그램을 시작 합니다.
5. Hello 응용 프로그램에서 작업을 입력 한 다음 더하기 hello (**+**) 아이콘입니다.
6. 항목이 추가될 때 알림을 받았는지 확인합니다.

## <a name="configure-and-run-hello-ios-project-optional"></a>구성 하 고 (선택 사항) hello iOS 프로젝트를 실행 합니다.
이 섹션은 iOS 장치에 대 한 hello Xamarin iOS 프로젝트를 실행 합니다. iOS 장치를 작업하지 않는 경우 이 섹션을 건너뛸 수 있습니다.

[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

#### <a name="configure-hello-notification-hub-for-apns"></a>APNS에 대 한 hello 알림 허브 구성
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

다음으로, Xamarin Studio 또는 Visual Studio에서 hello iOS 프로젝트 설정을 구성 합니다.

[!INCLUDE [app-service-mobile-xamarin-ios-configure-project](../../includes/app-service-mobile-xamarin-ios-configure-project.md)]

#### <a name="add-push-notifications-tooyour-ios-app"></a>푸시 알림 tooyour iOS 앱 추가
1. Hello에 **iOS** 프로젝트 AppDelegate.cs 연 hello hello 코드 파일의 문 toohello 맨 위에 다음을 추가 합니다.

        using Newtonsoft.Json.Linq;
2. Hello에 **AppDelegate** 클래스 hello에 대 한 재정의 추가, **RegisteredForRemoteNotifications** 알림에 대 한 이벤트 tooregister:

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
3. **AppDelegate**를 추가적으로 hello에 대 한 재정의 수행 하는 hello **DidReceiveRemoteNotification** 이벤트 처리기.

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

    이 메서드는 hello 응용 프로그램을 실행 하는 동안 받는 알림을 처리 합니다.
4. Hello에 **AppDelegate** 클래스, 다음 코드 toohello hello 추가 **FinishedLaunching** 메서드:

        // Register for push notifications.
        var settings = UIUserNotificationSettings.GetSettingsForTypes(
            UIUserNotificationType.Alert
            | UIUserNotificationType.Badge
            | UIUserNotificationType.Sound,
            new NSSet());

        UIApplication.SharedApplication.RegisterUserNotificationSettings(settings);
        UIApplication.SharedApplication.RegisterForRemoteNotifications();

    이를 통해 원격 알림을 지원하고 푸시 등록을 요청합니다.

앱 업데이트 toosupport 푸시 알림이 되었습니다.

#### <a name="test-push-notifications-in-your-ios-app"></a>iOS 앱에서 푸시 알림 테스트
1. Hello iOS 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 **시작 프로젝트로 설정**합니다.
2. 키를 눌러 hello **실행** 단추 또는 **F5** Visual Studio에서 toobuild 프로젝트 hello 및 iOS 장치에서 hello 응용 프로그램을 시작 합니다. 클릭 **확인** tooaccept 푸시 알림을 합니다.

   > [!NOTE]
   > 앱에서 푸시 알림을 명시적으로 수락해야 합니다. 이 요청은만 hello 앱이 실행 hello 처음으로 발생 합니다.
   >
   >
3. Hello 응용 프로그램에서 작업을 입력 한 다음 더하기 hello (**+**) 아이콘입니다.
4. 알림이 수신 되 고 클릭 한 다음 확인 **확인** toodismiss hello 알림입니다.

## <a name="configure-and-run-windows-projects-optional"></a>Windows 프로젝트 구성 및 실행(선택 사항)
Windows 장치에 대 한 Xamarin.Forms WinApp 및 WinPhone81 프로젝트 hello를 실행 하기 위한이 섹션이입니다. 이 단계에서는 UWP(범용 Windows 플랫폼) 프로젝트도 지원합니다. Windows 장치를 작업하지 않는 경우 이 섹션을 건너뛸 수 있습니다.

#### <a name="register-your-windows-app-for-push-notifications-with-windows-notification-service-wns"></a>WNS(Windows 알림 서비스)를 통한 푸시 알림에 Windows 앱 등록
[!INCLUDE [app-service-mobile-register-wns](../../includes/app-service-mobile-register-wns.md)]

#### <a name="configure-hello-notification-hub-for-wns"></a>Wns hello 알림 허브를 구성 합니다.
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

#### <a name="add-push-notifications-tooyour-windows-app"></a>푸시 알림 tooyour Windows 앱 추가
1. Visual Studio에서 열고 **App.xaml.cs** windows에서 프로젝트를 연 다음 조건 hello를 추가 합니다.

        using Newtonsoft.Json.Linq;
        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
        using Windows.Networking.PushNotifications;
        using <your_TodoItemManager_portable_class_namespace>;

    대체 `<your_TodoItemManager_portable_class_namespace>` hello 포함 된 이식 가능한 프로젝트의 hello 네임 스페이스를 가진 `TodoItemManager` 클래스입니다.
2. App.xaml.cs에서 hello 다음 추가 **InitNotificationsAsync** 메서드:

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

    이 메서드는 hello 푸시 알림 채널을 가져오고 알림 허브에서 템플릿 tooreceive 템플릿 알림을 등록 합니다. 지원 되는 템플릿 알림을 *messageParam* toothis 클라이언트 배달 됩니다.
3. App.xaml.cs, 업데이트 hello **OnLaunched** hello를 추가 하 여 이벤트 처리기 메서드 정의 `async` 한정자입니다. Hello 다음 hello 메서드의 hello 끝에 코드 줄을 추가 합니다.

        await InitNotificationsAsync();

    이렇게 하면 hello 푸시 알림 등록이 생성 되었거나 hello 앱이 시작 될 때마다 새로 고쳐집니다. 반드시 toodo WNS 푸시 채널 hello이 tooguarantee 항상 활성화 되어 있습니다.  
4. Visual Studio의 솔루션 탐색기를 열고 hello **Package.appxmanifest** 파일, 설정 및 **알림 가능** 너무**예** 아래 **알림**.
5. Hello 앱을 빌드하고 오류가 없는지 확인 해야 합니다. 클라이언트 앱 알림에 대 한 hello 템플릿 hello 모바일 앱을 다시 종료 이제 등록 해야 합니다. 솔루션의 모든 Windows 프로젝트에 대해 이 섹션을 반복합니다.

#### <a name="test-push-notifications-in-your-windows-app"></a>Windows 앱에서 푸시 알림 테스트
1. Visual Studio에서 Windows 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **시작 프로젝트로 설정**을 클릭합니다.
2. 키를 눌러 hello **실행** toobuild hello 프로젝트 단추 및 hello 응용 프로그램을 시작 합니다.
3. Hello 응용 프로그램에서 새 todoitem에 대 한 이름을 입력 한 다음 더하기 hello (**+**) 아이콘 tooadd 것입니다.
4. Hello 항목이 추가 될 때 알림을 받았는지 확인 합니다.

## <a name="next-steps"></a>다음 단계
푸시 알림에 대해 자세히 알아봅니다.

* [푸시 알림 문제 진단](../notification-hubs/notification-hubs-push-notification-fixer.md)  
  장치에서 알림이 삭제되거나 끝나지 않는 다양한 이유가 있습니다. 이 항목에서는 tooanalyze 및 hello 루트 계산 푸시 알림 오류의 발생 하는 방법을 보여 줍니다.

자습서를 따라 hello의 tooone을 계속할 수 있습니다.

* [인증 tooyour 앱 추가](app-service-mobile-xamarin-forms-get-started-users.md)  
  자세한 내용은 방법 tooauthenticate 사용자가 id 공급자로 사용 하 여 앱의 합니다.
* [앱에 오프라인 동기화 사용](app-service-mobile-xamarin-forms-get-started-offline-data.md)  
  자세한 방법을 모바일 앱을 사용 하 여 앱에 대 한 오프 라인 지원 tooadd 백 엔드 합니다. 오프라인 동기화를 사용하면 사용자는 네트워크에 연결되어 있지 않을 때도 모바일 앱&mdash;데이터 보기, 추가 또는 수정&mdash;과 같은 상호 작용을 수행할 수 있습니다.

<!-- Images. -->

<!-- URLs. -->
[Install Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[Xcode]: https://go.microsoft.com/fwLink/?LinkID=266532
[apns object]: http://go.microsoft.com/fwlink/p/?LinkId=272333

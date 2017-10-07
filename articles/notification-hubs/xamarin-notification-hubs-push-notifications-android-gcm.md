---
title: "Xamarin.Android 앱 용 알림 허브 시작 aaaGet | Microsoft Docs"
description: "이 자습서에서는 toouse Azure 알림 허브 toosend 알림 tooa Xamarin Android 응용 프로그램을 강제 하는 방법을 배웁니다."
author: ysxu
manager: erikre
editor: 
services: notification-hubs
documentationcenter: xamarin
ms.assetid: 0be600fe-d5f3-43a5-9e5e-3135c9743e54
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: c5c7ead9a9381ab9fb6bbe86e930a8a9254813d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-notification-hubs-with-xamarin-for-android"></a>Android용 Xamarin을 통해 알림 허브 시작
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>개요
이 자습서에서는 Azure 알림 허브 toosend toouse 밀어넣기 알림 tooa Xamarin.Android 응용 프로그램입니다.
GCM(Google Cloud Messaging)을 사용하여 푸시 알림을 받는 빈 Xamarin.Android 앱을 만듭니다. 수 toouse 수 완료 되 면 알림 허브 toobroadcast 푸시 알림을 tooall hello 장치 앱을 실행 합니다. hello 완성 된 코드는 hello에서 사용할 수 있는 [NotificationHubs 앱] [ GitHub] 샘플.

이 자습서에서는 알림 허브를 사용 하 여 hello 간단한 브로드캐스트 시나리오를 설명 합니다.

## <a name="before-you-begin"></a>시작하기 전에
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

이 자습서를 완료 하는 hello 코드 GitHub에서 확인할 수 있습니다 [여기](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/Xamarin/GetStartedXamarinAndroid)합니다.

## <a name="prerequisites"></a>필수 조건
이 자습서는 hello 다음을 사항이 필요합니다.

* Windows의 Xamarin이 포함된 Visual Studio 또는 Mac OS X의 Xamarin Studio. 전체 설치 지침은 [Visual Studio 및 Xamarin을 위한 설정 및 설치](https://msdn.microsoft.com/library/mt613162.aspx)에 있습니다.
* 활성 Google 계정
* [Azure 메시징 구성 요소]
* [Google Cloud Messaging 클라이언트 구성 요소]

이 자습서를 완료해야 다른 모든 Xamarin.Android 앱용 알림 허브 자습서를 진행할 수 있습니다.

> [!IMPORTANT]
> toocomplete이이 자습서에서는 활성 Azure 계정이 있어야 합니다. 계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다. 자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A9C9624B5&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-android-get-started%2F)을 참조하세요.
> 
> 

## <a name="enable-google-cloud-messaging"></a>Google Cloud Messaging 사용
[!INCLUDE [mobile-services-enable-Google-cloud-messaging](../../includes/mobile-services-enable-google-cloud-messaging.md)]

## <a name="configure-your-notification-hub"></a>알림 허브 구성
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="7">

<li><p>Hello 클릭 <b>구성</b> hello 위쪽에 탭을 hello 입력 <b>API 키</b> hello 이전 섹션에서 가져온 값을 클릭 한 다음 <b>저장</b>합니다.</p>
</li>
</ol>
&emsp;&emsp;![](./media/notification-hubs-android-get-started/notification-hub-configure-android.png)

알림 허브는 이제, GCM과 함께 구성 된 toowork 있고 hello 연결 문자열 tooboth 앱 tooreceive 알림과 toosend 푸시 알림을 등록 합니다.

## <a name="connect-your-app-toohello-notification-hub"></a>응용 프로그램 toohello 알림 허브를 연결 합니다.
### <a name="create-a-new-project"></a>새 프로젝트 만들기
1. Xamarin Studio에서 **새 솔루션**, **Android 앱**, **다음**을 차례로 클릭합니다.
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-project1.png)

2. **앱 이름**과 **식별자**를 입력합니다. Hello 클릭 **대상 플랫폼의 경우 문자의** toosupport 하 고을 클릭 한 다음 **다음** 및 **만들기**합니다.
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-project2.png)

    그러면 새 Android 프로젝트가 만들어집니다.

1. Hello 솔루션 보기에서에서 새 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 하 여 hello 프로젝트 속성을 열고 **옵션**합니다. 선택 hello **Android 응용 프로그램** hello에서 항목 **빌드** 섹션.
   
    해당 hello 첫 번째 문자를 확인 프로그램 **패키지 이름** 는 소문자로 표시 합니다.
   
   > [!IMPORTANT]
   > hello hello 패키지 이름의 첫 글자는 소문자 여야 합니다. 그렇지 않으면 아래에서 푸시 알림에 대한 **BroadcastReceiver** 및 **IntentFilter**를 등록할 때 응용 프로그램 매니페스트 오류가 표시됩니다.
   > 
   > 
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub--xamarin-android-app-options.png)
2. 필요에 따라 집합 hello **최소 Android 버전** tooanother API 레벨입니다.
3. 필요에 따라 집합 hello **대상 Android 버전** toohello tootarget (API 수준 8 이상 이어야)를 지정 하는 다른 API 버전입니다.

클릭 **확인** 및 닫기 hello 프로젝트 옵션 대화 상자.

### <a name="add-hello-required-components-tooyour-project"></a>Hello 필수 구성 요소 tooyour 프로젝트 추가
Google 클라우드 메시징 클라이언트 hello Xamarin 구성 요소 저장소에서 사용할 수 있는 hello Xamarin.Android에서 푸시 알림을 지원 hello 과정이 간단해 집니다.

1. Xamarin.Android 응용 프로그램에서 hello 구성 요소 폴더를 마우스 오른쪽 단추로 클릭 하 고 선택 **더 구성 요소 가져오기**합니다.
2. Hello에 대 한 검색 **Azure 메시징** 구성 요소 toohello 프로젝트에 추가 합니다.
3. Hello에 대 한 검색 **Google 클라우드 메시징 클라이언트** 구성 요소 toohello 프로젝트에 추가 합니다.

### <a name="set-up-notification-hubs-in-your-project"></a>프로젝트에서 알림 허브 설정
1. Hello 다음 Android 응용 프로그램 및 알림 허브에 대 한 정보를 수집 합니다.
   
   * **GoogleProjectNumber**: hello Google 개발자 포털에서 앱의 hello 개요에서이 프로젝트 번호 값을 가져옵니다. Hello 포털에 hello 앱을 만드는 경우에이 값을 이전 기록을 했습니다.
   * **연결 문자열을 수신 대기**: hello hello 대시보드에서 [Azure 클래식 포털], 클릭 **연결 문자열 보기**합니다. 복사 hello *DefaultListenSharedAccessSignature* 이 값에 대 한 연결 문자열입니다.
   * **허브 이름**: hello에서 허브 이름 hello입니다 [Azure 클래식 포털]합니다. 예를 들어 *mynotificationhub2*입니다.
     
     만들기는 **Constants.cs** Xamarin 프로젝트에 대 한 클래스 및 hello 다음 hello 클래스에서 상수 값을 정의 합니다. Hello 자리 표시자 값으로 대체 합니다.
     
       public static class Constants   {
     
           public const string SenderID = "<GoogleProjectNumber>"; // Google API Project Number
           public const string ListenConnectionString = "<Listen connection string>";
           public const string NotificationHubName = "<hub name>";
       }
2. Hello 다음 추가 너무 문을 사용 하 여**MainActivity.cs**:
   
        using Android.Util;
        using Gcm.Client;
3. 추가 인스턴스 변수 toohello `MainActivity` hello 앱이 실행 중일 때 사용 되는 tooshow 경고 대화 하는 클래스:
   
        public static MainActivity instance;
4. Hello에 대 한 메서드를 다음 hello 만들기 **MainActivity** 클래스:
   
        private void RegisterWithGCM()
        {
            // Check tooensure everything's set up right
            GcmClient.CheckDevice(this);
            GcmClient.CheckManifest(this);
   
            // Register for push notifications
            Log.Info("MainActivity", "Registering...");
            GcmClient.Register(this, Constants.SenderID);
        }
5. Hello에 `OnCreate` 방식의 **MainActivity.cs**, hello 초기화 `instance` 변수 너무 호출 추가`RegisterWithGCM`:
   
        protected override void OnCreate (Bundle bundle)
        {
            instance = this;
   
            base.OnCreate (bundle);
   
            // Set your view from hello "main" layout resource
            SetContentView (Resource.Layout.Main);
   
            // Get your button from hello layout resource,
            // and attach an event tooit
            Button button = FindViewById<Button> (Resource.Id.myButton);
   
            RegisterWithGCM();
        }
6. **MyBroadcastReceiver**라는 새 클래스를 만듭니다.
   
   > [!NOTE]
   > 아래에서 **BroadcastReceiver** 클래스를 처음부터 만드는 과정을 설명합니다. 그러나 만드는 빠른 대체 toomanually **MyBroadcastReceiver.cs** toorefer toohello은 **GcmService.cs** hello에포함된hello샘플Xamarin.Android프로젝트에서찾을파일[NotificationHubs 샘플][GitHub]합니다. 복제 **GcmService.cs** 클래스 이름 바꾸기가는 좋은 곳 toostart 하나일 수 있습니다.
   > 
   > 
7. Hello 다음 추가 너무 문을 사용 하 여**MyBroadcastReceiver.cs** (toohello 구성 요소 및 이전에 추가한 어셈블리 참조).
   
        using System.Collections.Generic;
        using System.Text;
        using Android.App;
        using Android.Content;
        using Android.Util;
        using Gcm.Client;
        using WindowsAzure.Messaging;
8. **MyBroadcastReceiver.cs**, 권한 요청 hello 사이 다음 hello 추가 **를 사용 하 여** 문과 hello **네임 스페이스** 선언:
   
        [assembly: Permission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "com.google.android.c2dm.permission.RECEIVE")]
   
        //GET_ACCOUNTS is needed only for Android versions 4.0.3 and below
        [assembly: UsesPermission(Name = "android.permission.GET_ACCOUNTS")]
        [assembly: UsesPermission(Name = "android.permission.INTERNET")]
        [assembly: UsesPermission(Name = "android.permission.WAKE_LOCK")]
9. **MyBroadcastReceiver.cs**, hello 변경 **MyBroadcastReceiver** toomatch hello 다음 클래스:
   
        [BroadcastReceiver(Permission=Gcm.Client.Constants.PERMISSION_GCM_INTENTS)]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_MESSAGE },
            Categories = new string[] { "@PACKAGE_NAME@" })]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_REGISTRATION_CALLBACK },
            Categories = new string[] { "@PACKAGE_NAME@" })]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_LIBRARY_RETRY },
            Categories = new string[] { "@PACKAGE_NAME@" })]
        public class MyBroadcastReceiver : GcmBroadcastReceiverBase<PushHandlerService>
        {
            public static string[] SENDER_IDS = new string[] { Constants.SenderID };
   
            public const string TAG = "MyBroadcastReceiver-GCM";
        }
10. **MyBroadcastReceiver.cs**에서 **GcmServiceBase**에서 파생된 **PushHandlerService** 클래스를 추가합니다. 있는지 tooapply hello 확인 **서비스** 특성 toohello 클래스:
    
         [Service] // Must use hello service tag
         public class PushHandlerService : GcmServiceBase
         {
             public static string RegistrationID { get; private set; }
             private NotificationHub Hub { get; set; }
    
             public PushHandlerService() : base(Constants.SenderID)
                {
                 Log.Info(MyBroadcastReceiver.TAG, "PushHandlerService() constructor");
             }
         }
11. **GcmServiceBase**는 **OnRegistered()**, **OnUnRegistered()**, **OnMessage()**, **OnRecoverableError()** 및 **OnError()** 메서드를 구현합니다. 우리의 **PushHandlerService** 응답 toointeracting hello 알림 허브에서 이러한 메서드는 발생 하 고 구현 클래스는 이러한 메서드를 재정의 해야 합니다.
12. Hello 재정의 **OnRegistered()** 메서드에서 **PushHandlerService** 코드 다음 hello를 사용 하 여:
    
         protected override void OnRegistered(Context context, string registrationId)
         {
             Log.Verbose(MyBroadcastReceiver.TAG, "GCM Registered: " + registrationId);
             RegistrationID = registrationId;
    
             createNotification("PushHandlerService-GCM Registered...",
                                 "hello device has been Registered!");
    
             Hub = new NotificationHub(Constants.NotificationHubName, Constants.ListenConnectionString,
                                         context);
             try
             {
                 Hub.UnregisterAll(registrationId);
             }
             catch (Exception ex)
             {
                 Log.Error(MyBroadcastReceiver.TAG, ex.Message);
             }
    
             //var tags = new List<string>() { "falcons" }; // create tags if you want
             var tags = new List<string>() {};
    
             try
             {
                 var hubRegistration = Hub.Register(registrationId, tags.ToArray());
             }
             catch (Exception ex)
             {
                 Log.Error(MyBroadcastReceiver.TAG, ex.Message);
             }
         }
    
    > [!NOTE]
    > Hello에 **OnRegistered()** 위의 코드를 특정 메시징 채널에 대 한 hello 기능 toospecify 태그 tooregister 점에 유의 해야 합니다.
    > 
    > 
13. Hello 재정의 **OnMessage** 메서드에서 **PushHandlerService** 코드 다음 hello를 사용 하 여:
    
        protected override void OnMessage(Context context, Intent intent)
        {
            Log.Info(MyBroadcastReceiver.TAG, "GCM Message Received!");
    
            var msg = new StringBuilder();
    
            if (intent != null && intent.Extras != null)
            {
                foreach (var key in intent.Extras.KeySet())
                    msg.AppendLine(key + "=" + intent.Extras.Get(key).ToString());
            }
    
            string messageText = intent.Extras.GetString("message");
            if (!string.IsNullOrEmpty (messageText))
            {
                createNotification ("New hub message!", messageText);
            }
            else
            {
                createNotification ("Unknown message details", msg.ToString ());
            }
        }
14. Hello 다음 추가 **createNotification** 및 **dialogNotify** 메서드 너무**PushHandlerService** 알림의 받을 때 사용자에 게 알리는 합니다.
    
    > [!NOTE]
    > Android 버전 5.0 이후의 알림 설계는 이전 버전과 상당한 차이가 있습니다. Android 5.0 이상이 테스트를 hello 앱 toobe tooreceive hello 알림 실행 해야 합니다. 자세한 내용은 [Android 알림](http://go.microsoft.com/fwlink/?LinkId=615880)을 참조하세요.
    > 
    > 
    
        void createNotification(string title, string desc)
        {
            //Create notification
            var notificationManager = GetSystemService(Context.NotificationService) as NotificationManager;
    
            //Create an intent tooshow UI
            var uiIntent = new Intent(this, typeof(MainActivity));
    
            //Create hello notification
            var notification = new Notification(Android.Resource.Drawable.SymActionEmail, title);
    
            //Auto-cancel will remove hello notification once hello user touches it
            notification.Flags = NotificationFlags.AutoCancel;
    
            //Set hello notification info
            //we use hello pending intent, passing our ui intent over, which will get called
            //when hello notification is tapped.
            notification.SetLatestEventInfo(this, title, desc, PendingIntent.GetActivity(this, 0, uiIntent, 0));
    
            //Show hello notification
            notificationManager.Notify(1, notification);
            dialogNotify (title, desc);
        }
    
        protected void dialogNotify(String title, String message)
        {
    
            MainActivity.instance.RunOnUiThread(() => {
                AlertDialog.Builder dlg = new AlertDialog.Builder(MainActivity.instance);
                AlertDialog alert = dlg.Create();
                alert.SetTitle(title);
                alert.SetButton("Ok", delegate {
                    alert.Dismiss();
                });
                alert.SetMessage(message);
                alert.Show();
            });
        }
15. 코드가 컴파일되도록 추상 멤버 **OnUnRegistered()**, **OnRecoverableError()** 및 **OnError()**를 재정의합니다.
    
        protected override void OnUnRegistered(Context context, string registrationId)
        {
            Log.Verbose(MyBroadcastReceiver.TAG, "GCM Unregistered: " + registrationId);
    
            createNotification("GCM Unregistered...", "hello device has been unregistered!");
        }
    
        protected override bool OnRecoverableError(Context context, string errorId)
        {
            Log.Warn(MyBroadcastReceiver.TAG, "Recoverable Error: " + errorId);
    
            return base.OnRecoverableError (context, errorId);
        }
    
        protected override void OnError(Context context, string errorId)
        {
            Log.Error(MyBroadcastReceiver.TAG, "GCM Error: " + errorId);
        }

## <a name="run-your-app-in-hello-emulator"></a>Hello 에뮬레이터에서 앱 실행
Hello 에뮬레이터에서이 응용 프로그램을 실행 하는 경우는 가상 장치 AVD (Android)을 지 원하는 Google Api를 사용 하 고 있는지 확인 합니다.

> [!IMPORTANT]
> 순서 tooreceive 푸시 알림을에서 Android 가상 장치에서 Google 계정 설정 해야 합니다. (너무 hello 에뮬레이터 이동**설정** 클릭 **계정 추가**.) 해당 hello 에뮬레이터에 연결 된 toohello 인터넷 인지 확인 합니다.
> 
> [!NOTE]
> Android 버전 5.0 이후의 알림 설계는 이전 버전과 상당한 차이가 있습니다. 자세한 내용은 [Android 알림](http://go.microsoft.com/fwlink/?LinkId=615880)을 참조하세요.
> 
> 

1. **Tools**에서 **Open Android Emulator Manager**를 클릭하고 해당 장치를 선택한 후 **Edit**를 클릭합니다.
   
      ![][18]
2. **대상**에서 **Google API**를 선택하고 **확인**을 클릭합니다.
   
      ![][19]
3. Hello 맨 위의 도구 모음에서 클릭 **실행**, 한 다음 앱을 선택 합니다. 이 hello 에뮬레이터를 시작 하 고 hello 응용 프로그램을 실행 합니다.
   
   hello 앱 검색 hello *registrationId* GCM 및 레지스터 hello 알림 허브를 사용 합니다.

## <a name="send-notifications-from-your-backend"></a>백 엔드에서 알림 보내기
Hello에 알림을 전송 하 여 앱에서 알림 받기 테스트할 수 [Azure 클래식 포털] hello를 통해 hello 알림 허브에 탭 아래의 hello 화면에 표시 된 것 처럼 디버그 합니다.

![][30]

푸시 알림은 일반적으로 호환 라이브러리를 통해 모바일 서비스 또는 ASP.NET과 같은 백 엔드 서비스에서 전송됩니다. 또한 toosend 알림 메시지는 라이브러리 백 엔드에 대해 사용할 수 없는 경우 직접 hello REST API를 사용할 수 있습니다.

알림을 보내기 위한 tooreview를 취소할 수 있음을 일부 다른 자습서의 목록을 다음과 같습니다.

* ASP.NET: 참조 [사용 하 여 알림 허브 toopush 알림 toousers]합니다.
* Azure 알림 허브 Java SDK: 참조 [어떻게 toouse Java에서 알림 허브](notification-hubs-java-push-notification-tutorial.md) Java에서 알림을 전송 합니다. 이는 Eclipse for Android Development에서 테스트되었습니다.
* PHP: 참조 [어떻게 toouse PHP에서 알림 허브](notification-hubs-php-push-notification-tutorial.md)합니다.

Hello 자습서의 다음 하위 섹션 hello.NET 콘솔 응용 프로그램을 사용 하 고 노드 스크립트를 통해 모바일 서비스를 사용 하 여 알림을 보냅니다.

#### <a name="optional-send-notifications-by-using-a-net-app"></a>(선택 사항) .NET 앱을 사용하여 알림 보내기
이 섹션에서는 .NET 콘솔 앱을 사용하여 알림을 보냅니다.

1. 새 Visual C# 콘솔 응용 프로그램을 만듭니다.
   
      ![][20]
2. Visual Studio에서 **도구**를 클릭하고 **NuGet 패키지 관리자**를 클릭한 다음 **패키지 관리자 콘솔**을 클릭합니다.
   
    Visual Studio에서 패키지 관리자 콘솔 hello 표시 됩니다.
3. Hello 패키지 관리자 콘솔 창에서에서 설정 hello **기본 프로젝트** tooyour 새 콘솔 응용 프로그램 프로젝트를 선택한 다음 hello 콘솔 창에 다음 명령을 hello를 실행 합니다.
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    이렇게 하면 추가 참조 toohello Azure 알림 허브 SDK hello를 사용 하 여 <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification 허브 NuGet 패키지</a>합니다.
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. Hello Program.cs 파일을 열고 hello 다음 추가 `using` 문:
   
        using Microsoft.Azure.NotificationHubs;
5. 사용자 `Program` 클래스, 메서드 뒤 hello를 추가 합니다. Hello 자리 표시자 텍스트와 업데이트 프로그램 *DefaultFullSharedAccessSignature* hello에서 연결 문자열 및 허브 이름을 [Azure 클래식 포털]합니다.
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            await hub.SendGcmNativeNotificationAsync("{ \"data\" : {\"message\":\"Hello from Azure!\"}}");
        }
6. Hello 뒤에 있는 줄을 추가 하면 **Main** 메서드:
   
         SendNotificationAsync();
         Console.ReadLine();
7. Hello F5 키 toorun hello 응용 프로그램 키를 누릅니다. Hello 앱에서 알림을 받게 됩니다.
   
      ![][21]

#### <a name="optional-send-notifications-by-using-a-mobile-service"></a>(선택 사항) 모바일 서비스를 사용하여 알림 보내기
1. [모바일 서비스 시작]을 수행합니다.
2. Toohello 로그인 [Azure 클래식 포털], 모바일 서비스를 선택 합니다.
3. 선택 hello **스케줄러** hello 위에 탭 합니다.
   
      ![][22]
4. 새 예약된 작업을 만들고 이름을 삽입한 후 **요청 시**를 선택합니다.
   
      ![][23]
5. Hello 작업이 만들어질 때 hello 작업 이름을 클릭 합니다. Hello 클릭 **스크립트** hello 위쪽 막대를 탭 합니다.
6. 스케줄러 함수 내 스크립트 다음 hello를 삽입 합니다. 알림 허브 이름 및 hello 연결 문자열에 있는 있는지 tooreplace hello 자리 표시자 확인 *DefaultFullSharedAccessSignature* 이전에 얻은입니다. **Save**를 클릭합니다.
   
        var azure = require('azure');
        var notificationHubService = azure.createNotificationHubService('<hub name>', '<connection string>');
        notificationHubService.gcm.send(null,'{"data":{"message" : "Hello from Mobile Services!"}}',
          function (error)
          {
            if (!error) {
               console.warn("Notification successful");
            }
            else
            {
              console.warn("Notification failed" + error);
            }
          }
        );
7. 클릭 **한 번 실행** hello 아래쪽 표시줄에 있습니다. 그러면 알림 메시지가 수신되어야 합니다.

## <a name="next-steps"></a>다음 단계
이 간단한 예제에서는 Android 장치 알림 tooall 브로드캐스트 있습니다. 특정 사용자에 게 tootarget 주문 하 toohello 자습서를 참조 하십시오. [사용 하 여 알림 허브 toopush 알림 toousers]합니다. 원하는 경우 toosegment 관심 그룹으로 사용자를 읽을 수 있습니다 [최신 뉴스 사용 하 여 알림 허브 toosend]합니다. 에 대 한 자세한 방법에 대 한 toouse 알림 허브에 [알림 허브 지침] 및 hello [알림 허브 방법 toofor Android]합니다.

<!-- Anchors. -->
[Enable Google Cloud Messaging]: #register
[Configure your Notification Hub]: #configure-hub
[Connecting your app toohello Notification Hub]: #connecting-app
[Run your app with hello emulator]: #run-app
[Send notifications from your back-end]: #send
[Next steps]:#next-steps

<!-- Images. -->

[11]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-configure-android.png

[13]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-app1.png
[15]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-app3.png

[18]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-android-app7.png
[19]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-android-app8.png

[20]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-console-app.png
[21]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-android-toast.png
[22]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-scheduler1.png
[23]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-scheduler2.png

[30]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hubs-debug-hub-gcm.png


<!-- URLs. -->
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[모바일 서비스 시작]: /develop/mobile/tutorials/get-started-xamarin-android/#create-new-service
[JavaScript and HTML]: /develop/mobile/tutorials/get-started-with-push-js

[Azure 클래식 포털]: https://manage.windowsazure.com/
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
[알림 허브 지침]: http://msdn.microsoft.com/library/jj927170.aspx
[알림 허브 방법 toofor Android]: http://msdn.microsoft.com/library/dn282661.aspx

[사용 하 여 알림 허브 toopush 알림 toousers]: /manage/services/notification-hubs/notify-users-aspnet
[최신 뉴스 사용 하 여 알림 허브 toosend]: /manage/services/notification-hubs/breaking-news-dotnet
[GCMClient Component page]: http://components.xamarin.com/view/GCMClient
[Xamarin.NotificationHub GitHub page]: https://github.com/SaschaDittmann/Xamarin.NotificationHub
[GitHub]: http://go.microsoft.com/fwlink/p/?LinkId=331329
[Google Cloud Messaging 클라이언트 구성 요소]: http://components.xamarin.com/view/GCMClient/
[Azure 메시징 구성 요소]: http://components.xamarin.com/view/azure-messaging

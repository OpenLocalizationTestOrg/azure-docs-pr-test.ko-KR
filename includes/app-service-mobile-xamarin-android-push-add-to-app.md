1. 라는 hello 프로젝트에서 새 클래스 만들기 `ToDoBroadcastReceiver`합니다.
2. Hello 다음 추가 너무 문을 사용 하 여**ToDoBroadcastReceiver** 클래스:
   
        using Gcm.Client;
        using Microsoft.WindowsAzure.MobileServices;
        using Newtonsoft.Json.Linq;
3. 추가 권한 요청 hello 사이 다음 hello **를 사용 하 여** 문과 hello **네임 스페이스** 선언:
   
        [assembly: Permission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "com.google.android.c2dm.permission.RECEIVE")]
   
        //GET_ACCOUNTS is only needed for android versions 4.0.3 and below
        [assembly: UsesPermission(Name = "android.permission.GET_ACCOUNTS")]
        [assembly: UsesPermission(Name = "android.permission.INTERNET")]
        [assembly: UsesPermission(Name = "android.permission.WAKE_LOCK")]
4. Hello 기존 항목 바꾸기 **ToDoBroadcastReceiver** 클래스 hello 다음과 같이 정의 합니다.
   
        [BroadcastReceiver(Permission = Gcm.Client.Constants.PERMISSION_GCM_INTENTS)]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_MESSAGE }, 
            Categories = new string[] { "@PACKAGE_NAME@" })]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_REGISTRATION_CALLBACK }, 
            Categories = new string[] { "@PACKAGE_NAME@" })]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_LIBRARY_RETRY }, 
        Categories = new string[] { "@PACKAGE_NAME@" })]
        public class ToDoBroadcastReceiver : GcmBroadcastReceiverBase<PushHandlerService>
        {
            // Set hello Google app ID.
            public static string[] senderIDs = new string[] { "<PROJECT_NUMBER>" };
        }
   
    코드 위의 hello,에서는 대체 해야  *`<PROJECT_NUMBER>`*  hello 프로젝트 번호 hello Google 개발자 포털에서 응용 프로그램을 프로 비전 할 때 Google에서 할당 합니다. 
5. Hello ToDoBroadcastReceiver.cs 프로젝트 파일에서 추가 hello를 정의 하는 코드를 다음 hello **PushHandlerService** 클래스:
   
        // hello ServiceAttribute must be applied toohello class.
        [Service] 
        public class PushHandlerService : GcmServiceBase
        {
            public static string RegistrationID { get; private set; }
   
            public PushHandlerService() : base(ToDoBroadcastReceiver.senderIDs) { }
        }
   
    이 클래스에서 파생 되는 참고 **GcmServiceBase** 및 해당 hello **서비스** 특성이 있어야 toothis 클래스를 적용 합니다.
   
   > [!NOTE]
   > hello **GcmServiceBase** 클래스 구현 hello **OnRegistered()**, **OnUnRegistered()**, **OnMessage()** 및  **OnError()** 메서드. Hello에서 이러한 메서드를 재정의 해야 **PushHandlerService** 클래스입니다.
   > 
   > 
6. 다음 코드 toohello hello 추가 **PushHandlerService** hello를 재정의 하는 클래스 **OnRegistered** 이벤트 처리기입니다. 
   
        protected override void OnRegistered(Context context, string registrationId)
        {
            System.Diagnostics.Debug.WriteLine("hello device has been registered with GCM.", "Success!");
   
            // Get hello MobileServiceClient from hello current activity instance.
            MobileServiceClient client = ToDoActivity.CurrentActivity.CurrentClient;
            var push = client.GetPush();
   
            // Define a message body for GCM.
            const string templateBodyGCM = "{\"data\":{\"message\":\"$(messageParam)\"}}";
   
            // Define hello template registration as JSON.
            JObject templates = new JObject();
            templates["genericMessage"] = new JObject
            {
              {"body", templateBodyGCM }
            };
   
            try
            {
                // Make sure we run hello registration on hello same thread as hello activity, 
                // tooavoid threading errors.
                ToDoActivity.CurrentActivity.RunOnUiThread(
   
                    // Register hello template with Notification Hubs.
                    async () => await push.RegisterAsync(registrationId, templates));
   
                System.Diagnostics.Debug.WriteLine(
                    string.Format("Push Installation Id", push.InstallationId.ToString()));
            }
            catch (Exception ex)
            {
                System.Diagnostics.Debug.WriteLine(
                    string.Format("Error with Azure push registration: {0}", ex.Message));
            }
        }
   
    이 메서드는 푸시 알림에 대 한 GCM 등록 ID tooregister Azure와 함께 반환 된 hello를 사용 합니다. 태그 수를 추가할 수 있습니다 toohello 등록 생성 됩니다. 자세한 내용은 참조 [하는 방법: 추가 tooa 장치 설치 tooenable 푸시--태그에 태그를 삽입](../articles/app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#tags)합니다.
7. Hello 재정의 **OnMessage** 메서드에서 **PushHandlerService** 코드 다음 hello로:
   
       protected override void OnMessage(Context context, Intent intent)
       {          
           string message = string.Empty;
   
           // Extract hello push notification message from hello intent.
           if (intent.Extras.ContainsKey("message"))
           {
               message = intent.Extras.Get("message").ToString();
               var title = "New item added:";
   
               // Create a notification manager toosend hello notification.
               var notificationManager = 
                   GetSystemService(Context.NotificationService) as NotificationManager;
   
               // Create a new intent tooshow hello notification in hello UI. 
               PendingIntent contentIntent = 
                   PendingIntent.GetActivity(context, 0, 
                   new Intent(this, typeof(ToDoActivity)), 0);              
   
               // Create hello notification using hello builder.
               var builder = new Notification.Builder(context);
               builder.SetAutoCancel(true);
               builder.SetContentTitle(title);
               builder.SetContentText(message);
               builder.SetSmallIcon(Resource.Drawable.ic_launcher);
               builder.SetContentIntent(contentIntent);
               var notification = builder.Build();
   
               // Display hello notification in hello Notifications Area.
               notificationManager.Notify(1, notification);
   
           }
       }
8. Hello 재정의 **OnUnRegistered()** 및 **OnError()** 코드 다음 hello 사용 하 여 메서드.
   
       protected override void OnUnRegistered(Context context, string registrationId)
       {
           throw new NotImplementedException();
       }
   
       protected override void OnError(Context context, string errorId)
       {
           System.Diagnostics.Debug.WriteLine(
               string.Format("Error occurred in hello notification: {0}.", errorId));
       }


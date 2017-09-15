1. <span data-ttu-id="cd8b1-101">`ToDoBroadcastReceiver`(이)라는 프로젝트에서 새 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cd8b1-101">Create a new class in the project called `ToDoBroadcastReceiver`.</span></span>
2. <span data-ttu-id="cd8b1-102">**ToDoBroadcastReceiver** 클래스에 다음 using 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cd8b1-102">Add the following using statements to **ToDoBroadcastReceiver** class:</span></span>
   
        using Gcm.Client;
        using Microsoft.WindowsAzure.MobileServices;
        using Newtonsoft.Json.Linq;
3. <span data-ttu-id="cd8b1-103">**using** 문과 **namespace** 선언 사이에 다음 사용 권한 요청을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cd8b1-103">Add the following permission requests between the **using** statements and the **namespace** declaration:</span></span>
   
        [assembly: Permission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "com.google.android.c2dm.permission.RECEIVE")]
   
        //GET_ACCOUNTS is only needed for android versions 4.0.3 and below
        [assembly: UsesPermission(Name = "android.permission.GET_ACCOUNTS")]
        [assembly: UsesPermission(Name = "android.permission.INTERNET")]
        [assembly: UsesPermission(Name = "android.permission.WAKE_LOCK")]
4. <span data-ttu-id="cd8b1-104">기존 **ToDoBroadcastReceiver** 클래스 정의를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="cd8b1-104">Replace the existing **ToDoBroadcastReceiver** class definition with the following:</span></span>
   
        [BroadcastReceiver(Permission = Gcm.Client.Constants.PERMISSION_GCM_INTENTS)]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_MESSAGE }, 
            Categories = new string[] { "@PACKAGE_NAME@" })]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_REGISTRATION_CALLBACK }, 
            Categories = new string[] { "@PACKAGE_NAME@" })]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_LIBRARY_RETRY }, 
        Categories = new string[] { "@PACKAGE_NAME@" })]
        public class ToDoBroadcastReceiver : GcmBroadcastReceiverBase<PushHandlerService>
        {
            // Set the Google app ID.
            public static string[] senderIDs = new string[] { "<PROJECT_NUMBER>" };
        }
   
    <span data-ttu-id="cd8b1-105">위의 코드에서 Google 개발자 포털에서 앱을 프로비전할 때 Google에서 할당한 프로젝트 번호로 *`<PROJECT_NUMBER>`*을(를) 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="cd8b1-105">In the above code, you must replace *`<PROJECT_NUMBER>`* with the project number assigned by Google when you provisioned your app in the Google developer portal.</span></span> 
5. <span data-ttu-id="cd8b1-106">ToDoBroadcastReceiver.cs 프로젝트 파일에서 **PushHandlerService** 클래스를 정의하는 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cd8b1-106">In the ToDoBroadcastReceiver.cs project file, add the following code that defines the **PushHandlerService** class:</span></span>
   
        // The ServiceAttribute must be applied to the class.
        [Service] 
        public class PushHandlerService : GcmServiceBase
        {
            public static string RegistrationID { get; private set; }
   
            public PushHandlerService() : base(ToDoBroadcastReceiver.senderIDs) { }
        }
   
    <span data-ttu-id="cd8b1-107">이 클래스는 **GcmServiceBase**에서 파생되며 **Service** 특성이 이 클래스에 적용되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd8b1-107">Note that this class derives from **GcmServiceBase** and that the **Service** attribute must be applied to this class.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="cd8b1-108">**GcmServiceBase** 클래스는 **OnRegistered()**, **OnUnRegistered()**, **OnMessage()** 및 **OnError()** 메서드를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="cd8b1-108">The **GcmServiceBase** class implements the **OnRegistered()**, **OnUnRegistered()**, **OnMessage()** and **OnError()** methods.</span></span> <span data-ttu-id="cd8b1-109">**PushHandlerService** 클래스에서 이러한 메서드를 재정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd8b1-109">You must override these methods in the **PushHandlerService** class.</span></span>
   > 
   > 
6. <span data-ttu-id="cd8b1-110">**OnRegistered** 이벤트 처리기를 재정의하는 **PushHandlerService** 클래스에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cd8b1-110">Add the following code to the **PushHandlerService** class that overrides the **OnRegistered** event handler.</span></span> 
   
        protected override void OnRegistered(Context context, string registrationId)
        {
            System.Diagnostics.Debug.WriteLine("The device has been registered with GCM.", "Success!");
   
            // Get the MobileServiceClient from the current activity instance.
            MobileServiceClient client = ToDoActivity.CurrentActivity.CurrentClient;
            var push = client.GetPush();
   
            // Define a message body for GCM.
            const string templateBodyGCM = "{\"data\":{\"message\":\"$(messageParam)\"}}";
   
            // Define the template registration as JSON.
            JObject templates = new JObject();
            templates["genericMessage"] = new JObject
            {
              {"body", templateBodyGCM }
            };
   
            try
            {
                // Make sure we run the registration on the same thread as the activity, 
                // to avoid threading errors.
                ToDoActivity.CurrentActivity.RunOnUiThread(
   
                    // Register the template with Notification Hubs.
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
   
    <span data-ttu-id="cd8b1-111">이 메서드는 반환된 GCM 등록 ID를 사용하여 푸시 알림을 위해 Azure에 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="cd8b1-111">This method uses the returned GCM registration ID to register with Azure for push notifications.</span></span> <span data-ttu-id="cd8b1-112">생성된 후 등록에 태그만 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd8b1-112">Tags can only be added to the registration after it is created.</span></span> <span data-ttu-id="cd8b1-113">자세한 내용은 [방법: 태그에 푸시를 사용하도록 설정하기 위해 장치 설치에 태그 추가](../articles/app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#tags)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cd8b1-113">For more information, see [How to: Add tags to a device installation to enable push-to-tags](../articles/app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#tags).</span></span>
7. <span data-ttu-id="cd8b1-114">**PushHandlerService**의 **OnMessage** 메서드를 다음 코드로 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="cd8b1-114">Override the **OnMessage** method in **PushHandlerService** with the following code:</span></span>
   
       protected override void OnMessage(Context context, Intent intent)
       {          
           string message = string.Empty;
   
           // Extract the push notification message from the intent.
           if (intent.Extras.ContainsKey("message"))
           {
               message = intent.Extras.Get("message").ToString();
               var title = "New item added:";
   
               // Create a notification manager to send the notification.
               var notificationManager = 
                   GetSystemService(Context.NotificationService) as NotificationManager;
   
               // Create a new intent to show the notification in the UI. 
               PendingIntent contentIntent = 
                   PendingIntent.GetActivity(context, 0, 
                   new Intent(this, typeof(ToDoActivity)), 0);              
   
               // Create the notification using the builder.
               var builder = new Notification.Builder(context);
               builder.SetAutoCancel(true);
               builder.SetContentTitle(title);
               builder.SetContentText(message);
               builder.SetSmallIcon(Resource.Drawable.ic_launcher);
               builder.SetContentIntent(contentIntent);
               var notification = builder.Build();
   
               // Display the notification in the Notifications Area.
               notificationManager.Notify(1, notification);
   
           }
       }
8. <span data-ttu-id="cd8b1-115">다음 코드를 사용하여 **OnUnRegistered()** 및 **OnError()** 메서드를 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="cd8b1-115">Override the **OnUnRegistered()** and **OnError()** methods with the following code.</span></span>
   
       protected override void OnUnRegistered(Context context, string registrationId)
       {
           throw new NotImplementedException();
       }
   
       protected override void OnError(Context context, string errorId)
       {
           System.Diagnostics.Debug.WriteLine(
               string.Format("Error occurred in the notification: {0}.", errorId));
       }


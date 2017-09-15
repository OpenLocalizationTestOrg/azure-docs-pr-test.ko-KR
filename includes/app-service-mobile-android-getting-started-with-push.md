1. <span data-ttu-id="24447-101">**앱** 프로젝트에서 `AndroidManifest.xml` 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="24447-101">In your **app** project, open the file `AndroidManifest.xml`.</span></span> <span data-ttu-id="24447-102">다음 두 단계의 코드에서 *`**my_app_package**`*를 프로젝트의 앱 패키지 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="24447-102">In the code in the next two steps, replace *`**my_app_package**`* with the name of the app package for your project.</span></span> <span data-ttu-id="24447-103">`manifest` 태그의 `package` 특성 값입니다.</span><span class="sxs-lookup"><span data-stu-id="24447-103">This is the value of the `package` attribute of the `manifest` tag.</span></span>
2. <span data-ttu-id="24447-104">기존 `uses-permission` 요소 뒤에 다음과 같은 새 사용 권한을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="24447-104">Add the following new permissions after the existing `uses-permission` element:</span></span>

        <permission android:name="**my_app_package**.permission.C2D_MESSAGE"
            android:protectionLevel="signature" />
        <uses-permission android:name="**my_app_package**.permission.C2D_MESSAGE" />
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
        <uses-permission android:name="android.permission.GET_ACCOUNTS" />
        <uses-permission android:name="android.permission.WAKE_LOCK" />
3. <span data-ttu-id="24447-105">다음 코드를 `application` 시작 태그 뒤에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="24447-105">Add the following code after the `application` opening tag:</span></span>

        <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
                                         android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="**my_app_package**" />
            </intent-filter>
        </receiver>
4. <span data-ttu-id="24447-106">*ToDoActivity.java*파일을 열고 다음 import 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="24447-106">Open the file *ToDoActivity.java*, and add the following import statement:</span></span>

        import com.microsoft.windowsazure.notifications.NotificationsManager;
5. <span data-ttu-id="24447-107">클래스에 다음 private 변수를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="24447-107">Add the following private variable to the class.</span></span> <span data-ttu-id="24447-108">*`<PROJECT_NUMBER>`*를 Google이 위의 절차에서 앱에 할당한 프로젝트 번호로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="24447-108">Replace *`<PROJECT_NUMBER>`* with the project number assigned by Google to your app in the preceding procedure.</span></span>

        public static final String SENDER_ID = "<PROJECT_NUMBER>";
6. <span data-ttu-id="24447-109">*MobileServiceClient*의 정의를 **private**에서 **public static**으로 변경하면 이제 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="24447-109">Change the definition of *MobileServiceClient* from **private** to **public static**, so it now looks like this:</span></span>

        public static MobileServiceClient mClient;
7. <span data-ttu-id="24447-110">알림을 처리하는 새 클래스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="24447-110">Add a new class to handle notifications.</span></span> <span data-ttu-id="24447-111">Project Explorer에서 **src** > **main** > **java** 노드를 열고 패키지 이름 노드를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="24447-111">In Project Explorer, open the **src** > **main** > **java** nodes, and right-click the package name node.</span></span> <span data-ttu-id="24447-112">**새로 만들기**를 클릭한 후 **Java Class**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="24447-112">Click **New**, and then click **Java Class**.</span></span>
8. <span data-ttu-id="24447-113">**이름**에 `MyHandler`를 입력하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="24447-113">In **Name**, type `MyHandler`, and then click **OK**.</span></span>

    ![](./media/app-service-mobile-android-configure-push/android-studio-create-class.png)

9. <span data-ttu-id="24447-114">MyHandler 파일에서 클래스 선언을 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="24447-114">In the MyHandler file, replace the class declaration with:</span></span>

        public class MyHandler extends NotificationsHandler {
10. <span data-ttu-id="24447-115">`MyHandler` 클래스에 대한 다음 import 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="24447-115">Add the following import statements for the `MyHandler` class:</span></span>

        import com.microsoft.windowsazure.notifications.NotificationsHandler;
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.os.AsyncTask;
        import android.os.Bundle;
        import android.support.v4.app.NotificationCompat;
11. <span data-ttu-id="24447-116">이제 이 구성원을 `MyHandler` 클래스에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="24447-116">Next add this member to the `MyHandler` class:</span></span>

        public static final int NOTIFICATION_ID = 1;
12. <span data-ttu-id="24447-117">`MyHandler` 클래스에서 다음 코드를 추가하여 장치를 모바일 서비스 알림 허브에 등록하는 **onRegistered** 메서드를 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="24447-117">In the `MyHandler` class, add the following code to override the **onRegistered** method, which registers your device with the mobile service notification hub.</span></span>

        @Override
        public void onRegistered(Context context,  final String gcmRegistrationId) {
           super.onRegistered(context, gcmRegistrationId);

           new AsyncTask<Void, Void, Void>() {

               protected Void doInBackground(Void... params) {
                   try {
                       ToDoActivity.mClient.getPush().register(gcmRegistrationId);
                       return null;
                   }
                   catch(Exception e) {
                       // handle error                
                   }
                   return null;              
               }
           }.execute();
       <span data-ttu-id="24447-118">}</span><span class="sxs-lookup"><span data-stu-id="24447-118">}</span></span>
13. <span data-ttu-id="24447-119">`MyHandler` 클래스에서 다음 코드를 추가하여 **onReceive** 메서드를 재정의하면 알림 수신 시 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="24447-119">In the `MyHandler` class, add the following code to override the **onReceive** method, which causes the notification to display when it is received.</span></span>

        @Override
        public void onReceive(Context context, Bundle bundle) {
               String msg = bundle.getString("message");

               PendingIntent contentIntent = PendingIntent.getActivity(context,
                       0, // requestCode
                       new Intent(context, ToDoActivity.class),
                       0); // flags

               Notification notification = new NotificationCompat.Builder(context)
                       .setSmallIcon(R.drawable.ic_launcher)
                       .setContentTitle("Notification Hub Demo")
                       .setStyle(new NotificationCompat.BigTextStyle().bigText(msg))
                       .setContentText(msg)
                       .setContentIntent(contentIntent)
                       .build();

               NotificationManager notificationManager = (NotificationManager)
                       context.getSystemService(Context.NOTIFICATION_SERVICE);
               notificationManager.notify(NOTIFICATION_ID, notification);
       <span data-ttu-id="24447-120">}</span><span class="sxs-lookup"><span data-stu-id="24447-120">}</span></span>
14. <span data-ttu-id="24447-121">다시 TodoActivity.java 파일에서 **ToDoActivity** 클래스의 *onCreate* 메서드를 업데이트하여 알림 처리기 클래스를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="24447-121">Back in the TodoActivity.java file, update the **onCreate** method of the *ToDoActivity* class to register the notification handler class.</span></span> <span data-ttu-id="24447-122">*MobileServiceClient* 가 인스턴스화된 후에 이 코드를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="24447-122">Make sure to add this code after the *MobileServiceClient* is instantiated.</span></span>

        NotificationsManager.handleNotifications(this, SENDER_ID, MyHandler.class);

    <span data-ttu-id="24447-123">이제 푸시 알림을 지원하도록 앱이 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="24447-123">Your app is now updated to support push notifications.</span></span>

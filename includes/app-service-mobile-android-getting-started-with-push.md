1. <span data-ttu-id="d2f61-101">사용자 **앱** 프로젝트, 열기 hello 파일 `AndroidManifest.xml`합니다.</span><span class="sxs-lookup"><span data-stu-id="d2f61-101">In your **app** project, open hello file `AndroidManifest.xml`.</span></span> <span data-ttu-id="d2f61-102">Hello 다음 두 단계에서 hello 코드에서 대체할  *`**my_app_package**`*  hello 앱 패키지의 프로젝트에 대 한 hello 이름으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2f61-102">In hello code in hello next two steps, replace *`**my_app_package**`* with hello name of hello app package for your project.</span></span> <span data-ttu-id="d2f61-103">이 hello hello 값 `package` hello 특성 `manifest` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="d2f61-103">This is hello value of hello `package` attribute of hello `manifest` tag.</span></span>
2. <span data-ttu-id="d2f61-104">다음 새 권한을 hello 기존 hello 추가 `uses-permission` 요소:</span><span class="sxs-lookup"><span data-stu-id="d2f61-104">Add hello following new permissions after hello existing `uses-permission` element:</span></span>

        <permission android:name="**my_app_package**.permission.C2D_MESSAGE"
            android:protectionLevel="signature" />
        <uses-permission android:name="**my_app_package**.permission.C2D_MESSAGE" />
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
        <uses-permission android:name="android.permission.GET_ACCOUNTS" />
        <uses-permission android:name="android.permission.WAKE_LOCK" />
3. <span data-ttu-id="d2f61-105">Hello hello 후 코드를 다음 추가 `application` 여는 태그:</span><span class="sxs-lookup"><span data-stu-id="d2f61-105">Add hello following code after hello `application` opening tag:</span></span>

        <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
                                         android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="**my_app_package**" />
            </intent-filter>
        </receiver>
4. <span data-ttu-id="d2f61-106">열기 hello 파일 *ToDoActivity.java*, hello 다음 import 문을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2f61-106">Open hello file *ToDoActivity.java*, and add hello following import statement:</span></span>

        import com.microsoft.windowsazure.notifications.NotificationsManager;
5. <span data-ttu-id="d2f61-107">Hello 개인 변수 toohello 클래스에 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2f61-107">Add hello following private variable toohello class.</span></span> <span data-ttu-id="d2f61-108">대체  *`<PROJECT_NUMBER>`*  hello 프로젝트 번호 앞에 프로시저 hello에서 Google tooyour 응용 프로그램에서 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2f61-108">Replace *`<PROJECT_NUMBER>`* with hello project number assigned by Google tooyour app in hello preceding procedure.</span></span>

        public static final String SENDER_ID = "<PROJECT_NUMBER>";
6. <span data-ttu-id="d2f61-109">정의 hello 변경 *MobileServiceClient* 에서 **개인** 너무**공용 정적**이므로 이제 다음과 같이 표시:</span><span class="sxs-lookup"><span data-stu-id="d2f61-109">Change hello definition of *MobileServiceClient* from **private** too**public static**, so it now looks like this:</span></span>

        public static MobileServiceClient mClient;
7. <span data-ttu-id="d2f61-110">새 클래스 toohandle 알림을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2f61-110">Add a new class toohandle notifications.</span></span> <span data-ttu-id="d2f61-111">프로젝트 탐색기에서 열어 hello **src** > **주** > **java** 노드와 hello 패키지 이름 노드를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2f61-111">In Project Explorer, open hello **src** > **main** > **java** nodes, and right-click hello package name node.</span></span> <span data-ttu-id="d2f61-112">**새로 만들기**를 클릭한 후 **Java Class**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d2f61-112">Click **New**, and then click **Java Class**.</span></span>
8. <span data-ttu-id="d2f61-113">**이름**에 `MyHandler`를 입력하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d2f61-113">In **Name**, type `MyHandler`, and then click **OK**.</span></span>

    ![](./media/app-service-mobile-android-configure-push/android-studio-create-class.png)

9. <span data-ttu-id="d2f61-114">Hello MyHandler 파일에서 사용 하는 hello 클래스 선언을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d2f61-114">In hello MyHandler file, replace hello class declaration with:</span></span>

        public class MyHandler extends NotificationsHandler {
10. <span data-ttu-id="d2f61-115">다음 가져오기 조건 hello에 대 한 hello 추가 `MyHandler` 클래스:</span><span class="sxs-lookup"><span data-stu-id="d2f61-115">Add hello following import statements for hello `MyHandler` class:</span></span>

        import com.microsoft.windowsazure.notifications.NotificationsHandler;
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.os.AsyncTask;
        import android.os.Bundle;
        import android.support.v4.app.NotificationCompat;
11. <span data-ttu-id="d2f61-116">이 멤버 toohello 다음 추가 `MyHandler` 클래스:</span><span class="sxs-lookup"><span data-stu-id="d2f61-116">Next add this member toohello `MyHandler` class:</span></span>

        public static final int NOTIFICATION_ID = 1;
12. <span data-ttu-id="d2f61-117">Hello에 `MyHandler` 클래스, 다음 코드 toooverride hello hello 추가 **onRegistered** hello 모바일 서비스 알림 허브를 장치를 등록 하는 메서드.</span><span class="sxs-lookup"><span data-stu-id="d2f61-117">In hello `MyHandler` class, add hello following code toooverride hello **onRegistered** method, which registers your device with hello mobile service notification hub.</span></span>

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
       <span data-ttu-id="d2f61-118">}</span><span class="sxs-lookup"><span data-stu-id="d2f61-118">}</span></span>
13. <span data-ttu-id="d2f61-119">Hello에 `MyHandler` 클래스, 다음 코드 toooverride hello hello 추가 **onReceive** 메서드에 hello 알림 toodisplay 수신 될 때입니다.</span><span class="sxs-lookup"><span data-stu-id="d2f61-119">In hello `MyHandler` class, add hello following code toooverride hello **onReceive** method, which causes hello notification toodisplay when it is received.</span></span>

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
       <span data-ttu-id="d2f61-120">}</span><span class="sxs-lookup"><span data-stu-id="d2f61-120">}</span></span>
14. <span data-ttu-id="d2f61-121">Hello TodoActivity.java 파일에 다시 hello 업데이트 **onCreate** hello 방식의 *ToDoActivity* tooregister hello 알림 처리기 클래스 클래스.</span><span class="sxs-lookup"><span data-stu-id="d2f61-121">Back in hello TodoActivity.java file, update hello **onCreate** method of hello *ToDoActivity* class tooregister hello notification handler class.</span></span> <span data-ttu-id="d2f61-122">Hello 후 있는지 tooadd이이 코드를 확인 *MobileServiceClient* 인스턴스화됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2f61-122">Make sure tooadd this code after hello *MobileServiceClient* is instantiated.</span></span>

        NotificationsManager.handleNotifications(this, SENDER_ID, MyHandler.class);

    <span data-ttu-id="d2f61-123">앱 업데이트 toosupport 푸시 알림이 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d2f61-123">Your app is now updated toosupport push notifications.</span></span>

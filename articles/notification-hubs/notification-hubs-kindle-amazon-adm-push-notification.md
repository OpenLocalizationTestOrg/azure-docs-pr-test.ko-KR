---
title: "Kindle 앱에 대한 Azure 알림 허브 시작 | Microsoft Docs"
description: "이 자습서에서 Azure 알림 허브를 사용하여 Kindle 응용 프로그램에 푸시 알림을 보내는 방법을 알아봅니다."
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 346fc8e5-294b-4e4f-9f27-7a82d9626e93
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-kindle
ms.devlang: Java
ms.topic: hero-article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 7206f152ed7270abc62536a9ee164f7227833bcc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-notification-hubs-for-kindle-apps"></a><span data-ttu-id="d79c2-103">Kindle 앱에 대한 알림 허브 시작</span><span class="sxs-lookup"><span data-stu-id="d79c2-103">Get started with Notification Hubs for Kindle apps</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="d79c2-104">개요</span><span class="sxs-lookup"><span data-stu-id="d79c2-104">Overview</span></span>
<span data-ttu-id="d79c2-105">이 자습서에서는 Azure 알림 허브를 사용하여 Kindle 응용 프로그램에 푸시 알림을 보내는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d79c2-105">This tutorial shows you how to use Azure Notification Hubs to send push notifications to a Kindle application.</span></span>
<span data-ttu-id="d79c2-106">ADM(Amazon 장치 메시징)을 사용하여 푸시 알림을 받는 빈 Kindle 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d79c2-106">You'll create a blank Kindle app that receives push notifications by using Amazon Device Messaging (ADM).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d79c2-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d79c2-107">Prerequisites</span></span>
<span data-ttu-id="d79c2-108">이 자습서를 사용하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d79c2-108">This tutorial requires the following:</span></span>

* <span data-ttu-id="d79c2-109"><a href="http://go.microsoft.com/fwlink/?LinkId=389797">Android 사이트</a>에서 Android SDK(Eclipse를 사용한다고 가정)를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d79c2-109">Get the Android SDK (we assume that you will use Eclipse) from the <a href="http://go.microsoft.com/fwlink/?LinkId=389797">Android site</a>.</span></span>
* <span data-ttu-id="d79c2-110"><a href="https://developer.amazon.com/appsandservices/resources/development-tools/ide-tools/tech-docs/01-setting-up-your-development-environment">개발 환경 설정</a>의 단계에 따라 Kindle에 대한 개발 환경을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d79c2-110">Follow the steps in <a href="https://developer.amazon.com/appsandservices/resources/development-tools/ide-tools/tech-docs/01-setting-up-your-development-environment">Setting Up Your Development Environment</a> to set up your development environment for Kindle.</span></span>

## <a name="add-a-new-app-to-the-developer-portal"></a><span data-ttu-id="d79c2-111">개발자 포털에 새 앱 추가</span><span class="sxs-lookup"><span data-stu-id="d79c2-111">Add a new app to the developer portal</span></span>
1. <span data-ttu-id="d79c2-112">먼저 [Amazon 개발자 포털]에서 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d79c2-112">First, create an app in the [Amazon developer portal].</span></span>
   
    ![][0]
2. <span data-ttu-id="d79c2-113">**응용 프로그램 키**를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="d79c2-113">Copy the **Application Key**.</span></span>
   
    ![][1]
3. <span data-ttu-id="d79c2-114">포털에서 앱의 이름을 클릭한 다음 **Device Messaging** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d79c2-114">In the portal, click the name of your app, and then click the **Device Messaging** tab.</span></span>
   
    ![][2]
4. <span data-ttu-id="d79c2-115">**Create a New Security Profile**을 클릭한 다음 새 보안 프로필(예: **TestAdm 보안 프로필**)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d79c2-115">Click **Create a New Security Profile**, and then create a new security profile (for example, **TestAdm security profile**).</span></span> <span data-ttu-id="d79c2-116">그런 다음 **Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d79c2-116">Then click **Save**.</span></span>
   
    ![][3]
5. <span data-ttu-id="d79c2-117">**Security Profiles** 를 클릭하여 방금 만든 보안 프로필을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d79c2-117">Click **Security Profiles** to view the security profile that you just created.</span></span> <span data-ttu-id="d79c2-118">나중에 사용할 수 있도록 **클라이언트 ID** 및 **클라이언트 암호** 값을 복사해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="d79c2-118">Copy the **Client ID** and **Client Secret** values for later use.</span></span>
   
    ![][4]

## <a name="create-an-api-key"></a><span data-ttu-id="d79c2-119">API 키 만들기</span><span class="sxs-lookup"><span data-stu-id="d79c2-119">Create an API key</span></span>
1. <span data-ttu-id="d79c2-120">관리자 권한으로 명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d79c2-120">Open a command prompt with administrator privileges.</span></span>
2. <span data-ttu-id="d79c2-121">Android SDK 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d79c2-121">Navigate to the Android SDK folder.</span></span>
3. <span data-ttu-id="d79c2-122">다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d79c2-122">Enter the following command:</span></span>
   
        keytool -list -v -alias androiddebugkey -keystore ./debug.keystore
   
    ![][5]
4. <span data-ttu-id="d79c2-123">**keystore** 암호에 **android**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d79c2-123">For the **keystore** password, type **android**.</span></span>
5. <span data-ttu-id="d79c2-124">**MD5** 지문을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="d79c2-124">Copy the **MD5** fingerprint.</span></span>
6. <span data-ttu-id="d79c2-125">개발자 포털로 돌아가서 **메시징** 탭에서 **Android/Kindle**을 클릭하고 앱에 대한 패키지 이름(예: **com.sample.notificationhubtest**)과 **MD5** 값을 입력한 다음 **API 키 생성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d79c2-125">Back in the developer portal, on the **Messaging** tab, click **Android/Kindle** and enter the name of the package for your app (for example, **com.sample.notificationhubtest**) and the **MD5** value, and then click **Generate API Key**.</span></span>

## <a name="add-credentials-to-the-hub"></a><span data-ttu-id="d79c2-126">허브에 자격 증명 추가</span><span class="sxs-lookup"><span data-stu-id="d79c2-126">Add credentials to the hub</span></span>
<span data-ttu-id="d79c2-127">포털에서 알림 허브의 **구성** 탭에 클라이언트 암호와 클라이언트 ID를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d79c2-127">In the portal, add the client secret and client ID to the **Configure** tab of your notification hub.</span></span>

## <a name="set-up-your-application"></a><span data-ttu-id="d79c2-128">응용 프로그램 설정</span><span class="sxs-lookup"><span data-stu-id="d79c2-128">Set up your application</span></span>
> [!NOTE]
> <span data-ttu-id="d79c2-129">응용 프로그램을 만들 때 API Level 17 이상을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d79c2-129">When you're creating an application, use at least API Level 17.</span></span>
> 
> 

<span data-ttu-id="d79c2-130">Eclipse 프로젝트에 ADM 라이브러리를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d79c2-130">Add the ADM libraries to your Eclipse project:</span></span>

1. <span data-ttu-id="d79c2-131">ADM 라이브러리를 가져오려면 [SDK를 다운로드합니다].</span><span class="sxs-lookup"><span data-stu-id="d79c2-131">To obtain the ADM library, [download the SDK].</span></span> <span data-ttu-id="d79c2-132">SDK zip 파일의 압축을 풉니다.</span><span class="sxs-lookup"><span data-stu-id="d79c2-132">Extract the SDK zip file.</span></span>
2. <span data-ttu-id="d79c2-133">Eclipse에서 프로젝트를 마우스 오른쪽 단추로 클릭한 후 **Properties**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d79c2-133">In Eclipse, right-click your project, and then click **Properties**.</span></span> <span data-ttu-id="d79c2-134">선택 **Java 빌드 경로** 왼쪽에서 선택한 후는 * * 라이브러리 * * 맨 위 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d79c2-134">Select **Java Build Path** on the left, and then select the **Libraries **tab at the top.</span></span> <span data-ttu-id="d79c2-135">**Add External Jar**을 클릭하고, Amazon SDK의 압축을 푼 디렉터리에서 `\SDK\Android\DeviceMessaging\lib\amazon-device-messaging-*.jar` 파일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d79c2-135">Click **Add External Jar**, and select the file `\SDK\Android\DeviceMessaging\lib\amazon-device-messaging-*.jar` from the directory in which you extracted the Amazon SDK.</span></span>
3. <span data-ttu-id="d79c2-136">NotificationHubs Android SDK(링크)를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="d79c2-136">Download the NotificationHubs Android SDK (link).</span></span>
4. <span data-ttu-id="d79c2-137">패키지의 압축을 푼 후 `notification-hubs-sdk.jar` 파일을 Eclipse의 `libs` 폴더로 끌어옵니다.</span><span class="sxs-lookup"><span data-stu-id="d79c2-137">Unzip the package, and then drag the file `notification-hubs-sdk.jar` into the `libs` folder in Eclipse.</span></span>

<span data-ttu-id="d79c2-138">ADM을 지원하도록 앱 매니페스트를 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="d79c2-138">Edit your app manifest to support ADM:</span></span>

1. <span data-ttu-id="d79c2-139">루트 매니페스트 요소에 Amazon 네임스페이스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d79c2-139">Add the Amazon namespace in the root manifest element:</span></span>

        xmlns:amazon="http://schemas.amazon.com/apk/res/android"

1. <span data-ttu-id="d79c2-140">사용 권한을 매니페스트 요소 아래에 첫 번째 요소로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d79c2-140">Add permissions as the first element under the manifest element.</span></span> <span data-ttu-id="d79c2-141">**[YOUR PACKAGE NAME]** 을 앱을 만드는 데 사용한 패키지로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d79c2-141">Substitute **[YOUR PACKAGE NAME]** with the package that you used to create your app.</span></span>
   
        <permission
         android:name="[YOUR PACKAGE NAME].permission.RECEIVE_ADM_MESSAGE"
         android:protectionLevel="signature" />
   
        <uses-permission android:name="android.permission.INTERNET"/>
   
        <uses-permission android:name="[YOUR PACKAGE NAME].permission.RECEIVE_ADM_MESSAGE" />
   
        <!-- This permission allows your app access to receive push notifications
        from ADM. -->
        <uses-permission android:name="com.amazon.device.messaging.permission.RECEIVE" />
   
        <!-- ADM uses WAKE_LOCK to keep the processor from sleeping when a message is received. -->
        <uses-permission android:name="android.permission.WAKE_LOCK" />
2. <span data-ttu-id="d79c2-142">응용 프로그램 요소의 첫 번째 자식으로 다음 요소를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="d79c2-142">Insert the following element as the first child of the application element.</span></span> <span data-ttu-id="d79c2-143">**[YOUR SERVICE NAME]**을 다음 섹션에서 만드는 ADM 메시지 처리기의 이름(패키지 포함)으로 바꾸고, **[YOUR PACKAGE NAME]**을 앱을 만들 때 사용한 패키지 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d79c2-143">Remember to substitute **[YOUR SERVICE NAME]** with the name of your ADM message handler that you create in the next section (including the package), and replace **[YOUR PACKAGE NAME]** with the package name with which you created your app.</span></span>
   
        <amazon:enable-feature
              android:name="com.amazon.device.messaging"
                     android:required="true"/>
        <service
            android:name="[YOUR SERVICE NAME]"
            android:exported="false" />
   
        <receiver
            android:name="[YOUR SERVICE NAME]$Receiver" />
   
            <!-- This permission ensures that only ADM can send your app registration broadcasts. -->
            android:permission="com.amazon.device.messaging.permission.SEND" >
   
            <!-- To interact with ADM, your app must listen for the following intents. -->
            <intent-filter>
          <action android:name="com.amazon.device.messaging.intent.REGISTRATION" />
          <action android:name="com.amazon.device.messaging.intent.RECEIVE" />
   
          <!-- Replace the name in the category tag with your app's package name. -->
          <category android:name="[YOUR PACKAGE NAME]" />
            </intent-filter>
        </receiver>

## <a name="create-your-adm-message-handler"></a><span data-ttu-id="d79c2-144">ADM 메시지 처리기 만들기</span><span class="sxs-lookup"><span data-stu-id="d79c2-144">Create your ADM message handler</span></span>
1. <span data-ttu-id="d79c2-145">다음 그림에 표시된 것처럼 `com.amazon.device.messaging.ADMMessageHandlerBase`에서 상속되는 새 클래스를 만들고 이름을 `MyADMMessageHandler`로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d79c2-145">Create a new class that inherits from `com.amazon.device.messaging.ADMMessageHandlerBase` and name it `MyADMMessageHandler`, as shown in the following figure:</span></span>
   
    ![][6]
2. <span data-ttu-id="d79c2-146">다음 `import` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d79c2-146">Add the following `import` statements:</span></span>
   
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.support.v4.app.NotificationCompat;
        import com.amazon.device.messaging.ADMMessageReceiver;
        import com.microsoft.windowsazure.messaging.NotificationHub
3. <span data-ttu-id="d79c2-147">만든 클래스에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d79c2-147">Add the following code in the class that you created.</span></span> <span data-ttu-id="d79c2-148">허브 이름 및 연결 문자열(수신)을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d79c2-148">Remember to substitute the hub name and connection string (listen):</span></span>
   
        public static final int NOTIFICATION_ID = 1;
        private NotificationManager mNotificationManager;
        NotificationCompat.Builder builder;
          private static NotificationHub hub;
        public static NotificationHub getNotificationHub(Context context) {
            Log.v("com.wa.hellokindlefire", "getNotificationHub");
            if (hub == null) {
                hub = new NotificationHub("[hub name]", "[listen connection string]", context);
            }
            return hub;
        }
   
        public MyADMMessageHandler() {
                super("MyADMMessageHandler");
            }
   
            public static class Receiver extends ADMMessageReceiver
            {
                public Receiver()
                {
                    super(MyADMMessageHandler.class);
                }
            }
   
            private void sendNotification(String msg) {
                Context ctx = getApplicationContext();
   
                mNotificationManager = (NotificationManager)
                    ctx.getSystemService(Context.NOTIFICATION_SERVICE);
   
            PendingIntent contentIntent = PendingIntent.getActivity(ctx, 0,
                  new Intent(ctx, MainActivity.class), 0);
   
            NotificationCompat.Builder mBuilder =
                  new NotificationCompat.Builder(ctx)
                  .setSmallIcon(R.mipmap.ic_launcher)
                  .setContentTitle("Notification Hub Demo")
                  .setStyle(new NotificationCompat.BigTextStyle()
                         .bigText(msg))
                  .setContentText(msg);
   
             mBuilder.setContentIntent(contentIntent);
             mNotificationManager.notify(NOTIFICATION_ID, mBuilder.build());
        }
4. <span data-ttu-id="d79c2-149">`OnMessage()` 메서드에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d79c2-149">Add the following code to the `OnMessage()` method:</span></span>
   
        String nhMessage = intent.getExtras().getString("msg");
        sendNotification(nhMessage);
5. <span data-ttu-id="d79c2-150">`OnRegistered` 메서드에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d79c2-150">Add the following code to the `OnRegistered` method:</span></span>
   
            try {
        getNotificationHub(getApplicationContext()).register(registrationId);
            } catch (Exception e) {
        Log.e("[your package name]", "Fail onRegister: " + e.getMessage(), e);
            }
6. <span data-ttu-id="d79c2-151">`OnUnregistered` 메서드에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d79c2-151">Add the following code to the `OnUnregistered` method:</span></span>
   
         try {
             getNotificationHub(getApplicationContext()).unregister();
         } catch (Exception e) {
             Log.e("[your package name]", "Fail onUnregister: " + e.getMessage(), e);
         }
7. <span data-ttu-id="d79c2-152">`MainActivity` 메서드에 다음 import 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d79c2-152">In the `MainActivity` method, add the following import statement:</span></span>
   
        import com.amazon.device.messaging.ADM;
8. <span data-ttu-id="d79c2-153">`OnCreate` 메서드의 끝에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d79c2-153">Add the following code at the end of the `OnCreate` method:</span></span>
   
        final ADM adm = new ADM(this);
        if (adm.getRegistrationId() == null)
        {
           adm.startRegister();
        } else {
            new AsyncTask() {
                  @Override
                  protected Object doInBackground(Object... params) {
                     try {                         MyADMMessageHandler.getNotificationHub(getApplicationContext()).register(adm.getRegistrationId());
                     } catch (Exception e) {
                         Log.e("com.wa.hellokindlefire", "Failed registration with hub", e);
                         return e;
                     }
                     return null;
                 }
               }.execute(null, null, null);
        }

## <a name="add-your-api-key-to-your-app"></a><span data-ttu-id="d79c2-154">앱에 API 키 추가</span><span class="sxs-lookup"><span data-stu-id="d79c2-154">Add your API key to your app</span></span>
1. <span data-ttu-id="d79c2-155">Eclipse에서 프로젝트의 디렉터리 자산에 **api_key.txt**라는 새 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d79c2-155">In Eclipse, create a new file named **api_key.txt** in the directory assets of your project.</span></span>
2. <span data-ttu-id="d79c2-156">파일을 열고 Amazon 개발자 포털에서 생성한 API 키를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="d79c2-156">Open the file and copy the API key that you generated in the Amazon developer portal.</span></span>

## <a name="run-the-app"></a><span data-ttu-id="d79c2-157">앱 실행</span><span class="sxs-lookup"><span data-stu-id="d79c2-157">Run the app</span></span>
1. <span data-ttu-id="d79c2-158">에뮬레이터를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d79c2-158">Start the emulator.</span></span>
2. <span data-ttu-id="d79c2-159">에뮬레이터에서 위에서 아래로 살짝 밀고 **설정**, **내 계정**을 차례로 클릭한 다음 유효한 Amazon 계정을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="d79c2-159">In the emulator, swipe from the top and click **Settings**, and then click **My account** and register with a valid Amazon account.</span></span>
3. <span data-ttu-id="d79c2-160">Eclipse에서 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d79c2-160">In Eclipse, run the app.</span></span>

> [!NOTE]
> <span data-ttu-id="d79c2-161">문제가 발생하면 에뮬레이터 또는 장치의 시간을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d79c2-161">If a problem occurs, check the time of the emulator (or device).</span></span> <span data-ttu-id="d79c2-162">시간 값이 정확해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d79c2-162">The time value must be accurate.</span></span> <span data-ttu-id="d79c2-163">Kindle 에뮬레이터의 시간을 변경하려면 Android SDK 플랫폼 도구 디렉터리에서 다음 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d79c2-163">To change the time of the Kindle emulator, you can run the following command from your Android SDK platform-tools directory:</span></span>
> 
> 

        adb shell  date -s "yyyymmdd.hhmmss"

## <a name="send-a-message"></a><span data-ttu-id="d79c2-164">메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="d79c2-164">Send a message</span></span>
<span data-ttu-id="d79c2-165">.NET을 사용하여 메시지를 보내려면</span><span class="sxs-lookup"><span data-stu-id="d79c2-165">To send a message by using .NET:</span></span>

        static void Main(string[] args)
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("[conn string]", "[hub name]");

            hub.SendAdmNativeNotificationAsync("{\"data\":{\"msg\" : \"Hello from .NET!\"}}").Wait();
        }

![][7]

<!-- URLs. -->
<span data-ttu-id="d79c2-166">[Amazon 개발자 포털]: https://developer.amazon.com/home.html</span><span class="sxs-lookup"><span data-stu-id="d79c2-166">[Amazon developer portal]: https://developer.amazon.com/home.html</span></span>
<span data-ttu-id="d79c2-167">[SDK를 다운로드합니다]: https://developer.amazon.com/public/resources/development-tools/sdk</span><span class="sxs-lookup"><span data-stu-id="d79c2-167">[download the SDK]: https://developer.amazon.com/public/resources/development-tools/sdk</span></span>

[0]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal1.png
[1]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal2.png
[2]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal3.png
[3]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal4.png
[4]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal5.png
[5]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-cmd-window.png
[6]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-new-java-class.png
[7]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-notification.png

---
title: "aaaGet Kindle 앱 용 Azure 알림 허브 시작 | Microsoft Docs"
description: "이 자습서에서는 Azure 알림 허브 toosend toouse 알림 tooa Kindle 응용 프로그램을 강제 하는 방법을 배웁니다."
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
ms.openlocfilehash: 7c28d64372cd2d90bab9cd9bf818d333f3478f7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-notification-hubs-for-kindle-apps"></a><span data-ttu-id="943bd-103">Kindle 앱에 대한 알림 허브 시작</span><span class="sxs-lookup"><span data-stu-id="943bd-103">Get started with Notification Hubs for Kindle apps</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="943bd-104">개요</span><span class="sxs-lookup"><span data-stu-id="943bd-104">Overview</span></span>
<span data-ttu-id="943bd-105">이 자습서에서는 Azure 알림 허브 toosend toouse 밀어넣기 알림 tooa Kindle 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="943bd-105">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa Kindle application.</span></span>
<span data-ttu-id="943bd-106">ADM(Amazon 장치 메시징)을 사용하여 푸시 알림을 받는 빈 Kindle 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="943bd-106">You'll create a blank Kindle app that receives push notifications by using Amazon Device Messaging (ADM).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="943bd-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="943bd-107">Prerequisites</span></span>
<span data-ttu-id="943bd-108">이 자습서는 hello 다음을 사항이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="943bd-108">This tutorial requires hello following:</span></span>

* <span data-ttu-id="943bd-109">Android SDK (가정 Eclipse 사용 하 여) hello hello에서 가져올 <a href="http://go.microsoft.com/fwlink/?LinkId=389797">Android 사이트</a>합니다.</span><span class="sxs-lookup"><span data-stu-id="943bd-109">Get hello Android SDK (we assume that you will use Eclipse) from hello <a href="http://go.microsoft.com/fwlink/?LinkId=389797">Android site</a>.</span></span>
* <span data-ttu-id="943bd-110">Hello 단계에 따라 <a href="https://developer.amazon.com/appsandservices/resources/development-tools/ide-tools/tech-docs/01-setting-up-your-development-environment">개발 환경 설정을</a> Kindle 용 개발 환경을 tooset 합니다.</span><span class="sxs-lookup"><span data-stu-id="943bd-110">Follow hello steps in <a href="https://developer.amazon.com/appsandservices/resources/development-tools/ide-tools/tech-docs/01-setting-up-your-development-environment">Setting Up Your Development Environment</a> tooset up your development environment for Kindle.</span></span>

## <a name="add-a-new-app-toohello-developer-portal"></a><span data-ttu-id="943bd-111">새 앱 toohello 개발자 포털 추가</span><span class="sxs-lookup"><span data-stu-id="943bd-111">Add a new app toohello developer portal</span></span>
1. <span data-ttu-id="943bd-112">첫째, hello에서 앱을 만들 [Amazon developer portal]합니다.</span><span class="sxs-lookup"><span data-stu-id="943bd-112">First, create an app in hello [Amazon developer portal].</span></span>
   
    ![][0]
2. <span data-ttu-id="943bd-113">복사 hello **응용 프로그램 키**합니다.</span><span class="sxs-lookup"><span data-stu-id="943bd-113">Copy hello **Application Key**.</span></span>
   
    ![][1]
3. <span data-ttu-id="943bd-114">Hello 포털 응용 프로그램의 hello 이름을 클릭 하 고 hello 클릭 **장치 메시징** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="943bd-114">In hello portal, click hello name of your app, and then click hello **Device Messaging** tab.</span></span>
   
    ![][2]
4. <span data-ttu-id="943bd-115">**Create a New Security Profile**을 클릭한 다음 새 보안 프로필(예: **TestAdm 보안 프로필**)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="943bd-115">Click **Create a New Security Profile**, and then create a new security profile (for example, **TestAdm security profile**).</span></span> <span data-ttu-id="943bd-116">그런 다음 **Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="943bd-116">Then click **Save**.</span></span>
   
    ![][3]
5. <span data-ttu-id="943bd-117">클릭 **보안 프로필** 방금 만든 tooview hello 보안 프로필.</span><span class="sxs-lookup"><span data-stu-id="943bd-117">Click **Security Profiles** tooview hello security profile that you just created.</span></span> <span data-ttu-id="943bd-118">복사 hello **클라이언트 ID** 및 **클라이언트 암호** 나중에 사용할 값입니다.</span><span class="sxs-lookup"><span data-stu-id="943bd-118">Copy hello **Client ID** and **Client Secret** values for later use.</span></span>
   
    ![][4]

## <a name="create-an-api-key"></a><span data-ttu-id="943bd-119">API 키 만들기</span><span class="sxs-lookup"><span data-stu-id="943bd-119">Create an API key</span></span>
1. <span data-ttu-id="943bd-120">관리자 권한으로 명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="943bd-120">Open a command prompt with administrator privileges.</span></span>
2. <span data-ttu-id="943bd-121">Toohello Android SDK 폴더를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="943bd-121">Navigate toohello Android SDK folder.</span></span>
3. <span data-ttu-id="943bd-122">Hello 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="943bd-122">Enter hello following command:</span></span>
   
        keytool -list -v -alias androiddebugkey -keystore ./debug.keystore
   
    ![][5]
4. <span data-ttu-id="943bd-123">Hello에 대 한 **keystore** 암호를 입력 **android**합니다.</span><span class="sxs-lookup"><span data-stu-id="943bd-123">For hello **keystore** password, type **android**.</span></span>
5. <span data-ttu-id="943bd-124">복사 hello **MD5** 지문입니다.</span><span class="sxs-lookup"><span data-stu-id="943bd-124">Copy hello **MD5** fingerprint.</span></span>
6. <span data-ttu-id="943bd-125">Hello에 hello 개발자 포털에 다시 **메시징** 탭을 클릭 **Android/Kindle** hello 패키지의 앱에 대 한 hello 이름 입력 (예를 들어 **com.sample.notificationhubtest**) hello 및 **MD5** 값을 클릭 한 다음 **API 키 생성**합니다.</span><span class="sxs-lookup"><span data-stu-id="943bd-125">Back in hello developer portal, on hello **Messaging** tab, click **Android/Kindle** and enter hello name of hello package for your app (for example, **com.sample.notificationhubtest**) and hello **MD5** value, and then click **Generate API Key**.</span></span>

## <a name="add-credentials-toohello-hub"></a><span data-ttu-id="943bd-126">자격 증명 toohello 허브 추가</span><span class="sxs-lookup"><span data-stu-id="943bd-126">Add credentials toohello hub</span></span>
<span data-ttu-id="943bd-127">Hello 포털에서 추가 hello 클라이언트 암호 및 클라이언트 ID toohello **구성** 알림 허브의 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="943bd-127">In hello portal, add hello client secret and client ID toohello **Configure** tab of your notification hub.</span></span>

## <a name="set-up-your-application"></a><span data-ttu-id="943bd-128">응용 프로그램 설정</span><span class="sxs-lookup"><span data-stu-id="943bd-128">Set up your application</span></span>
> [!NOTE]
> <span data-ttu-id="943bd-129">응용 프로그램을 만들 때 API Level 17 이상을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="943bd-129">When you're creating an application, use at least API Level 17.</span></span>
> 
> 

<span data-ttu-id="943bd-130">Hello ADM 라이브러리 tooyour Eclipse 프로젝트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="943bd-130">Add hello ADM libraries tooyour Eclipse project:</span></span>

1. <span data-ttu-id="943bd-131">tooobtain hello ADM 라이브러리 [hello SDK 다운로드]합니다.</span><span class="sxs-lookup"><span data-stu-id="943bd-131">tooobtain hello ADM library, [download hello SDK].</span></span> <span data-ttu-id="943bd-132">Hello SDK zip 파일을 추출 합니다.</span><span class="sxs-lookup"><span data-stu-id="943bd-132">Extract hello SDK zip file.</span></span>
2. <span data-ttu-id="943bd-133">Eclipse에서 프로젝트를 마우스 오른쪽 단추로 클릭한 후 **Properties**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="943bd-133">In Eclipse, right-click your project, and then click **Properties**.</span></span> <span data-ttu-id="943bd-134">선택 **Java 빌드 경로** 왼쪽, hello 및 선택 hello에서 * * 라이브러리 * * hello 위쪽 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="943bd-134">Select **Java Build Path** on hello left, and then select hello **Libraries **tab at hello top.</span></span> <span data-ttu-id="943bd-135">클릭 **외부 Jar 추가**, 및 select hello 파일 `\SDK\Android\DeviceMessaging\lib\amazon-device-messaging-*.jar` hello Amazon SDK 압축을 푼 hello 디렉터리에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="943bd-135">Click **Add External Jar**, and select hello file `\SDK\Android\DeviceMessaging\lib\amazon-device-messaging-*.jar` from hello directory in which you extracted hello Amazon SDK.</span></span>
3. <span data-ttu-id="943bd-136">Hello NotificationHubs Android SDK (링크)를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="943bd-136">Download hello NotificationHubs Android SDK (link).</span></span>
4. <span data-ttu-id="943bd-137">Hello 패키지 압축 해제 한 다음 끌어다 hello 파일 `notification-hubs-sdk.jar` hello에 `libs` Eclipse에서 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="943bd-137">Unzip hello package, and then drag hello file `notification-hubs-sdk.jar` into hello `libs` folder in Eclipse.</span></span>

<span data-ttu-id="943bd-138">응용 프로그램 매니페스트 toosupport ADM를 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="943bd-138">Edit your app manifest toosupport ADM:</span></span>

1. <span data-ttu-id="943bd-139">Hello 루트 매니페스트 요소에 hello Amazon 네임 스페이스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="943bd-139">Add hello Amazon namespace in hello root manifest element:</span></span>

        xmlns:amazon="http://schemas.amazon.com/apk/res/android"

1. <span data-ttu-id="943bd-140">Hello 매니페스트 요소 아래의 hello 첫 번째 요소로 권한을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="943bd-140">Add permissions as hello first element under hello manifest element.</span></span> <span data-ttu-id="943bd-141">대체 **[YOUR 패키지 NAME]** hello 패키지를 사용 하 여 toocreate 앱.</span><span class="sxs-lookup"><span data-stu-id="943bd-141">Substitute **[YOUR PACKAGE NAME]** with hello package that you used toocreate your app.</span></span>
   
        <permission
         android:name="[YOUR PACKAGE NAME].permission.RECEIVE_ADM_MESSAGE"
         android:protectionLevel="signature" />
   
        <uses-permission android:name="android.permission.INTERNET"/>
   
        <uses-permission android:name="[YOUR PACKAGE NAME].permission.RECEIVE_ADM_MESSAGE" />
   
        <!-- This permission allows your app access tooreceive push notifications
        from ADM. -->
        <uses-permission android:name="com.amazon.device.messaging.permission.RECEIVE" />
   
        <!-- ADM uses WAKE_LOCK tookeep hello processor from sleeping when a message is received. -->
        <uses-permission android:name="android.permission.WAKE_LOCK" />
2. <span data-ttu-id="943bd-142">Hello 요소 다음에 오는 hello hello 응용 프로그램 요소의 첫 번째 자식으로 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="943bd-142">Insert hello following element as hello first child of hello application element.</span></span> <span data-ttu-id="943bd-143">Toosubstitute 기억 **[서비스 사용자 이름]** hello 다음 섹션 (hello 패키지 포함)에서 만들고 대체 하는 ADM 메시지 처리기의 hello 이름의 **[YOUR 패키지 NAME]** hello로 응용 프로그램을 만들 때 사용한 패키지 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="943bd-143">Remember toosubstitute **[YOUR SERVICE NAME]** with hello name of your ADM message handler that you create in hello next section (including hello package), and replace **[YOUR PACKAGE NAME]** with hello package name with which you created your app.</span></span>
   
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
   
            <!-- toointeract with ADM, your app must listen for hello following intents. -->
            <intent-filter>
          <action android:name="com.amazon.device.messaging.intent.REGISTRATION" />
          <action android:name="com.amazon.device.messaging.intent.RECEIVE" />
   
          <!-- Replace hello name in hello category tag with your app's package name. -->
          <category android:name="[YOUR PACKAGE NAME]" />
            </intent-filter>
        </receiver>

## <a name="create-your-adm-message-handler"></a><span data-ttu-id="943bd-144">ADM 메시지 처리기 만들기</span><span class="sxs-lookup"><span data-stu-id="943bd-144">Create your ADM message handler</span></span>
1. <span data-ttu-id="943bd-145">상속 되는 새 클래스를 만듭니다 `com.amazon.device.messaging.ADMMessageHandlerBase` 하 고 이름을 `MyADMMessageHandler`hello 다음 그림에에서 나온 것 처럼:</span><span class="sxs-lookup"><span data-stu-id="943bd-145">Create a new class that inherits from `com.amazon.device.messaging.ADMMessageHandlerBase` and name it `MyADMMessageHandler`, as shown in hello following figure:</span></span>
   
    ![][6]
2. <span data-ttu-id="943bd-146">Hello 다음 추가 `import` 문:</span><span class="sxs-lookup"><span data-stu-id="943bd-146">Add hello following `import` statements:</span></span>
   
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.support.v4.app.NotificationCompat;
        import com.amazon.device.messaging.ADMMessageReceiver;
        import com.microsoft.windowsazure.messaging.NotificationHub
3. <span data-ttu-id="943bd-147">Hello 코드 만든 hello 클래스에 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="943bd-147">Add hello following code in hello class that you created.</span></span> <span data-ttu-id="943bd-148">Toosubstitute hello 허브 이름 및 연결 문자열 (수신)에 유의 하십시오.</span><span class="sxs-lookup"><span data-stu-id="943bd-148">Remember toosubstitute hello hub name and connection string (listen):</span></span>
   
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
4. <span data-ttu-id="943bd-149">다음 코드 toohello hello 추가 `OnMessage()` 메서드:</span><span class="sxs-lookup"><span data-stu-id="943bd-149">Add hello following code toohello `OnMessage()` method:</span></span>
   
        String nhMessage = intent.getExtras().getString("msg");
        sendNotification(nhMessage);
5. <span data-ttu-id="943bd-150">다음 코드 toohello hello 추가 `OnRegistered` 메서드:</span><span class="sxs-lookup"><span data-stu-id="943bd-150">Add hello following code toohello `OnRegistered` method:</span></span>
   
            try {
        getNotificationHub(getApplicationContext()).register(registrationId);
            } catch (Exception e) {
        Log.e("[your package name]", "Fail onRegister: " + e.getMessage(), e);
            }
6. <span data-ttu-id="943bd-151">다음 코드 toohello hello 추가 `OnUnregistered` 메서드:</span><span class="sxs-lookup"><span data-stu-id="943bd-151">Add hello following code toohello `OnUnregistered` method:</span></span>
   
         try {
             getNotificationHub(getApplicationContext()).unregister();
         } catch (Exception e) {
             Log.e("[your package name]", "Fail onUnregister: " + e.getMessage(), e);
         }
7. <span data-ttu-id="943bd-152">Hello에 `MainActivity` 메서드를 hello 다음 import 문을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="943bd-152">In hello `MainActivity` method, add hello following import statement:</span></span>
   
        import com.amazon.device.messaging.ADM;
8. <span data-ttu-id="943bd-153">Hello 코드 hello의 hello 끝에 다음 추가 `OnCreate` 메서드:</span><span class="sxs-lookup"><span data-stu-id="943bd-153">Add hello following code at hello end of hello `OnCreate` method:</span></span>
   
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

## <a name="add-your-api-key-tooyour-app"></a><span data-ttu-id="943bd-154">API 키 tooyour 앱 추가</span><span class="sxs-lookup"><span data-stu-id="943bd-154">Add your API key tooyour app</span></span>
1. <span data-ttu-id="943bd-155">Eclipse에서 라는 새 파일을 만들어 **api_key.txt** 프로젝트의 hello 디렉터리 자산에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="943bd-155">In Eclipse, create a new file named **api_key.txt** in hello directory assets of your project.</span></span>
2. <span data-ttu-id="943bd-156">Hello 파일과 복사본 hello API 키 hello Amazon developer portal에서 생성을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="943bd-156">Open hello file and copy hello API key that you generated in hello Amazon developer portal.</span></span>

## <a name="run-hello-app"></a><span data-ttu-id="943bd-157">Hello 앱 실행</span><span class="sxs-lookup"><span data-stu-id="943bd-157">Run hello app</span></span>
1. <span data-ttu-id="943bd-158">Hello 에뮬레이터를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="943bd-158">Start hello emulator.</span></span>
2. <span data-ttu-id="943bd-159">클릭 하 고 hello 위쪽에서으로 살짝 hello 에뮬레이터에서 **설정**, 클릭 하 고 **내 계정** 올바른 Amazon 계정으로 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="943bd-159">In hello emulator, swipe from hello top and click **Settings**, and then click **My account** and register with a valid Amazon account.</span></span>
3. <span data-ttu-id="943bd-160">Eclipse에서 hello 앱을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="943bd-160">In Eclipse, run hello app.</span></span>

> [!NOTE]
> <span data-ttu-id="943bd-161">문제가 발생 한 경우 hello 에뮬레이터 (또는 장치)의 hello 시간을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="943bd-161">If a problem occurs, check hello time of hello emulator (or device).</span></span> <span data-ttu-id="943bd-162">hello 시간 값은 정확 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="943bd-162">hello time value must be accurate.</span></span> <span data-ttu-id="943bd-163">실행할 수 있습니다 toochange hello Kindle 에뮬레이터의 hello 시간을 다음 Android SDK 플랫폼 도구 디렉터리에서 명령을 hello:</span><span class="sxs-lookup"><span data-stu-id="943bd-163">toochange hello time of hello Kindle emulator, you can run hello following command from your Android SDK platform-tools directory:</span></span>
> 
> 

        adb shell  date -s "yyyymmdd.hhmmss"

## <a name="send-a-message"></a><span data-ttu-id="943bd-164">메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="943bd-164">Send a message</span></span>
<span data-ttu-id="943bd-165">toosend.NET을 사용 하 여 메시지:</span><span class="sxs-lookup"><span data-stu-id="943bd-165">toosend a message by using .NET:</span></span>

        static void Main(string[] args)
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("[conn string]", "[hub name]");

            hub.SendAdmNativeNotificationAsync("{\"data\":{\"msg\" : \"Hello from .NET!\"}}").Wait();
        }

![][7]

<!-- URLs. -->
[Amazon developer portal]: https://developer.amazon.com/home.html
[hello SDK 다운로드]: https://developer.amazon.com/public/resources/development-tools/sdk

[0]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal1.png
[1]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal2.png
[2]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal3.png
[3]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal4.png
[4]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal5.png
[5]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-cmd-window.png
[6]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-new-java-class.png
[7]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-notification.png

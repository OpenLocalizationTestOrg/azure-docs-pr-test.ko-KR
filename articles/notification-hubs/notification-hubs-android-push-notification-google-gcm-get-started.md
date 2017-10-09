---
title: "Azure 알림 허브와 aaaSending 푸시 알림 tooAndroid | Microsoft Docs"
description: "이 자습서에 설명 어떻게 toouse Azure 알림 허브 toopush 알림 tooAndroid 장치입니다."
services: notification-hubs
documentationcenter: android
keywords: "푸시 알림,푸시알림,android 푸시 알림"
author: ysxu
manager: erikre
editor: 
ms.assetid: 8268c6ef-af63-433c-b14e-a20b04a0342a
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: hero-article
ms.date: 07/05/2016
ms.author: yuaxu
ms.openlocfilehash: 6b15a477d86cf1e6efffb21c5bcef0de7761af79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-tooandroid-with-azure-notification-hubs"></a><span data-ttu-id="2662b-104">Azure 알림 허브 푸시 알림을 tooAndroid 보내기</span><span class="sxs-lookup"><span data-stu-id="2662b-104">Sending push notifications tooAndroid with Azure Notification Hubs</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="2662b-105">개요</span><span class="sxs-lookup"><span data-stu-id="2662b-105">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="2662b-106">이 항목에서는 GCM(Google Cloud Messaging)을 사용한 푸시 알림을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-106">This topic demonstrates push notifications with Google Cloud Messaging (GCM).</span></span> <span data-ttu-id="2662b-107">Google의 Firebase 클라우드 메시징 (FCM)를 사용 하는 경우 참조 [Azure 알림 허브와 FCM 보내는 푸시 알림 tooAndroid](notification-hubs-android-push-notification-google-fcm-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-107">If you are using Google's Firebase Cloud Messaging (FCM), see [Sending push notifications tooAndroid with Azure Notification Hubs and FCM](notification-hubs-android-push-notification-google-fcm-get-started.md).</span></span>
> 
> 

<span data-ttu-id="2662b-108">이 자습서에서는 Azure 알림 허브 toosend toouse 밀어넣기 알림 tooan Android 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-108">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooan Android application.</span></span>
<span data-ttu-id="2662b-109">GCM(Google Cloud Messaging)을 사용하여 푸시 알림을 받는 빈 Android 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-109">You'll create a blank Android app that receives push notifications by using Google Cloud Messaging (GCM).</span></span>

[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="2662b-110">이 자습서를 완료 하는 hello 코드 GitHub에서 다운로드할 수 있습니다 [여기](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStarted)합니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-110">hello completed code for this tutorial can be downloaded from GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStarted).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2662b-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="2662b-111">Prerequisites</span></span>
> [!IMPORTANT]
> <span data-ttu-id="2662b-112">toocomplete이이 자습서에서는 활성 Azure 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-112">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="2662b-113">계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-113">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="2662b-114">자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-android-get-started)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2662b-114">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-android-get-started).</span></span>
> 
> 

<span data-ttu-id="2662b-115">또한 tooan 활성 Azure 계정 위에서 언급 한이 자습서를만 사용 하려면 최신 버전의 hello [Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797)합니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-115">In addition tooan active Azure account mentioned above, this tutorial only requires hello latest version of [Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797).</span></span>

<span data-ttu-id="2662b-116">이 자습서를 완료해야 다른 모든 Android 앱용 알림 허브 자습서를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-116">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Android apps.</span></span>

## <a name="creating-a-project-that-supports-google-cloud-messaging"></a><span data-ttu-id="2662b-117">Google Cloud Messaging을 지원하는 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="2662b-117">Creating a project that supports Google Cloud Messaging</span></span>
[!INCLUDE [mobile-services-enable-Google-cloud-messaging](../../includes/mobile-services-enable-google-cloud-messaging.md)]

## <a name="configure-a-new-notification-hub"></a><span data-ttu-id="2662b-118">새 알림 허브 구성</span><span class="sxs-lookup"><span data-stu-id="2662b-118">Configure a new notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<span data-ttu-id="2662b-119">&emsp;&emsp;6.</span><span class="sxs-lookup"><span data-stu-id="2662b-119">&emsp;&emsp;6.</span></span>   <span data-ttu-id="2662b-120">Hello에 **설정** 블레이드를 **Notification Services** 차례로 **GCM (Google)**합니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-120">In hello **Settings** blade, select **Notification Services** and then **Google (GCM)**.</span></span> <span data-ttu-id="2662b-121">Hello API 키를 입력 하 고 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-121">Enter hello API key and click **Save**.</span></span>

&emsp;&emsp;![Azure 알림 허브 - Google(GCM)](./media/notification-hubs-android-get-started/notification-hubs-gcm-api.png)

<span data-ttu-id="2662b-123">알림 허브는 이제 구성 된 toowork GCM 사용 하며 앱 tooreceive를 등록 하 고 푸시 알림을 보내려면 연결 문자열 tooboth hello를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-123">Your notification hub is now configured toowork with GCM, and you have hello connection strings tooboth register your app tooreceive and send push notifications.</span></span>

## <span data-ttu-id="2662b-124"><a id="connecting-app"></a>응용 프로그램 toohello 알림 허브를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-124"><a id="connecting-app"></a>Connect your app toohello notification hub</span></span>
### <a name="create-a-new-android-project"></a><span data-ttu-id="2662b-125">새 Android 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="2662b-125">Create a new Android project</span></span>
1. <span data-ttu-id="2662b-126">Android Studio에서 새 Android Studio 프로젝트를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-126">In Android Studio, start a new Android Studio project.</span></span>
   
   ![Android Studio - 새 프로젝트][13]
2. <span data-ttu-id="2662b-128">Hello 선택 **전화 및 태블릿** 폼 팩터 및 hello **최소 SDK** toosupport 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-128">Choose hello **Phone and Tablet** form factor and hello **Minimum SDK** that you want toosupport.</span></span> <span data-ttu-id="2662b-129">그런 후 **Next**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-129">Then click **Next**.</span></span>
   
   ![Android Studio - 프로젝트 만들기 워크플로][14]
3. <span data-ttu-id="2662b-131">선택 **빈 활동** hello 기본 활동에 대 한 클릭 **다음**, 클릭 하 고 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-131">Choose **Empty Activity** for hello main activity, click **Next**, and then click **Finish**.</span></span>

### <a name="add-google-play-services-toohello-project"></a><span data-ttu-id="2662b-132">Google Play 서비스 toohello 프로젝트 추가</span><span class="sxs-lookup"><span data-stu-id="2662b-132">Add Google Play services toohello project</span></span>
[!INCLUDE [Add Play Services](../../includes/notification-hubs-android-studio-add-google-play-services.md)]

### <a name="adding-azure-notification-hubs-libraries"></a><span data-ttu-id="2662b-133">Azure 알림 허브 라이브러리 추가</span><span class="sxs-lookup"><span data-stu-id="2662b-133">Adding Azure Notification Hubs libraries</span></span>
1. <span data-ttu-id="2662b-134">Hello에 `Build.Gradle` hello에 대 한 파일 **앱**, hello hello에 있는 줄을 다음 추가 **종속성** 섹션.</span><span class="sxs-lookup"><span data-stu-id="2662b-134">In hello `Build.Gradle` file for hello **app**, add hello following lines in hello **dependencies** section.</span></span>
   
        compile 'com.microsoft.azure:notification-hubs-android-sdk:0.4@aar'
        compile 'com.microsoft.azure:azure-notifications-handler:1.0.1@aar'
2. <span data-ttu-id="2662b-135">추가 저장소 hello 후 다음 hello **종속성** 섹션.</span><span class="sxs-lookup"><span data-stu-id="2662b-135">Add hello following repository after hello **dependencies** section.</span></span>
   
        repositories {
            maven {
                url "http://dl.bintray.com/microsoftazuremobile/SDK"
            }
        }

### <a name="updating-hello-androidmanifestxml"></a><span data-ttu-id="2662b-136">Hello AndroidManifest.xml 업데이트 중입니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-136">Updating hello AndroidManifest.xml.</span></span>
1. <span data-ttu-id="2662b-137">GCM toosupport 너무 사용 되는 코드에 인스턴스 ID 수신기 서비스를 구현 해야 했습니다[등록 토큰을 얻어](https://developers.google.com/cloud-messaging/android/client#sample-register) 를 사용 하 여 [Google의 인스턴스 ID API](https://developers.google.com/instance-id/)합니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-137">toosupport GCM, we must implement a Instance ID listener service in our code which is used too[obtain registration tokens](https://developers.google.com/cloud-messaging/android/client#sample-register) using [Google's Instance ID API](https://developers.google.com/instance-id/).</span></span> <span data-ttu-id="2662b-138">이 자습서에서는 hello 클래스 이름을 `MyInstanceIDService`합니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-138">In this tutorial we will name hello class `MyInstanceIDService`.</span></span> 
   
    <span data-ttu-id="2662b-139">다음 hello 내 서비스 정의 toohello AndroidManifest.xml 파일 hello 추가 `<application>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-139">Add hello following service definition toohello AndroidManifest.xml file, inside hello `<application>` tag.</span></span> <span data-ttu-id="2662b-140">Hello 대체 `<your package>` 자리 표시자 hello hello hello 위쪽에 표시 된 프로그램 실제 패키지 이름을 `AndroidManifest.xml` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-140">Replace hello `<your package>` placeholder with hello your actual package name shown at hello top of hello `AndroidManifest.xml` file.</span></span>
   
        <service android:name="<your package>.MyInstanceIDService" android:exported="false">
            <intent-filter>
                <action android:name="com.google.android.gms.iid.InstanceID"/>
            </intent-filter>
        </service>
2. <span data-ttu-id="2662b-141">Hello 인스턴스 ID API에서에서 우리의 GCM 등록 토큰을 수신 있습니다 사용할 것 너무[hello Azure 알림 허브로 등록](notification-hubs-push-notification-registration-management.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-141">Once we have received our GCM registration token from hello Instance ID API, we will use it too[register with hello Azure Notification Hub](notification-hubs-push-notification-registration-management.md).</span></span> <span data-ttu-id="2662b-142">이 등록 사용 하 여 hello 백그라운드에서 지원 되며는 `IntentService` 라는 `RegistrationIntentService`합니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-142">We will support this registration in hello background using an `IntentService` named `RegistrationIntentService`.</span></span> <span data-ttu-id="2662b-143">이 서비스는 [GCM 등록 토큰 새로 고침](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens)에 대한 책임도 맡습니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-143">This service will also be responsible for [refreshing our GCM registration token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens).</span></span>
   
    <span data-ttu-id="2662b-144">다음 hello 내 서비스 정의 toohello AndroidManifest.xml 파일 hello 추가 `<application>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-144">Add hello following service definition toohello AndroidManifest.xml file, inside hello `<application>` tag.</span></span> <span data-ttu-id="2662b-145">Hello 대체 `<your package>` 자리 표시자 hello hello hello 위쪽에 표시 된 프로그램 실제 패키지 이름을 `AndroidManifest.xml` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-145">Replace hello `<your package>` placeholder with hello your actual package name shown at hello top of hello `AndroidManifest.xml` file.</span></span> 
   
        <service
            android:name="<your package>.RegistrationIntentService"
            android:exported="false">
        </service>
3. <span data-ttu-id="2662b-146">또한 수신기 tooreceive 알림의 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-146">We will also define a receiver tooreceive notifications.</span></span> <span data-ttu-id="2662b-147">다음 hello 내부 수신기 정의 toohello AndroidManifest.xml 파일 hello 추가 `<application>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-147">Add hello following receiver definition toohello AndroidManifest.xml file, inside hello `<application>` tag.</span></span> <span data-ttu-id="2662b-148">Hello 대체 `<your package>` 자리 표시자 hello hello hello 위쪽에 표시 된 프로그램 실제 패키지 이름을 `AndroidManifest.xml` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-148">Replace hello `<your package>` placeholder with hello your actual package name shown at hello top of hello `AndroidManifest.xml` file.</span></span>
   
        <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
            android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<your package name>" />
            </intent-filter>
        </receiver>
4. <span data-ttu-id="2662b-149">필요한 GCM 다음 hello hello 아래 사용 권한 관련 추가 `</application>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-149">Add hello following necessary GCM related permissions below hello  `</application>` tag.</span></span> <span data-ttu-id="2662b-150">있는지 tooreplace 확인 `<your package>` hello hello 위쪽에 표시 된 hello 패키지 이름의 `AndroidManifest.xml` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-150">Make sure tooreplace `<your package>` with hello package name shown at hello top of hello `AndroidManifest.xml` file.</span></span>
   
    <span data-ttu-id="2662b-151">이러한 권한에 대한 자세한 내용은 [Android용 GCM 클라이언트 앱 설치](https://developers.google.com/cloud-messaging/android/client#manifest)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2662b-151">For more information on these permissions, see [Setup a GCM Client app for Android](https://developers.google.com/cloud-messaging/android/client#manifest).</span></span>
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.GET_ACCOUNTS"/>
        <uses-permission android:name="android.permission.WAKE_LOCK"/>
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
   
        <permission android:name="<your package>.permission.C2D_MESSAGE" android:protectionLevel="signature" />
        <uses-permission android:name="<your package>.permission.C2D_MESSAGE"/>

### <a name="adding-code"></a><span data-ttu-id="2662b-152">코드 추가</span><span class="sxs-lookup"><span data-stu-id="2662b-152">Adding code</span></span>
1. <span data-ttu-id="2662b-153">Hello 프로젝트 보기, 확장 **앱** > **src** > **주** > **java**합니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-153">In hello Project View, expand **app** > **src** > **main** > **java**.</span></span> <span data-ttu-id="2662b-154">**java** 아래의 패키지 폴더를 마우스 오른쪽 단추로 클릭하고 **새로 만들기**, **Java 클래스**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-154">Right-click your package folder under **java**, click **New**, and then click **Java Class**.</span></span> <span data-ttu-id="2662b-155">`NotificationSettings`(이)라는 새 클래스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-155">Add a new class named `NotificationSettings`.</span></span> 
   
    ![Android Studio - 새 Java 프로젝트][6]
   
    <span data-ttu-id="2662b-157">Tooupdate hello 이러한 세 자리 표시자 hello hello에 대 한 코드 뒤에 있는지 확인 `NotificationSettings` 클래스:</span><span class="sxs-lookup"><span data-stu-id="2662b-157">Make sure tooupdate hello these three placeholders in hello following code for hello `NotificationSettings` class:</span></span>
   
   * <span data-ttu-id="2662b-158">**SenderId**: hello 앞에서 가져온 프로젝트 번호 hello [Google 클라우드 콘솔](http://cloud.google.com/console)합니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-158">**SenderId**: hello project number you obtained earlier in hello [Google Cloud Console](http://cloud.google.com/console).</span></span>
   * <span data-ttu-id="2662b-159">**HubListenConnectionString**: hello **DefaultListenAccessSignature** 허브에 대 한 연결 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-159">**HubListenConnectionString**: hello **DefaultListenAccessSignature** connection string for your hub.</span></span> <span data-ttu-id="2662b-160">클릭 하 여 해당 연결 문자열을 복사할 수는 있지만 **액세스 정책을** hello에 **설정** hello에 허브의 블레이드에서 [Azure 포털]합니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-160">You can copy that connection string by clicking **Access Policies** on hello **Settings** blade of your hub on hello [Azure Portal].</span></span>
   * <span data-ttu-id="2662b-161">**HubName**: hello에 허브 블레이드 hello에에서 표시 되는 알림 허브의 hello 이름 사용 [Azure 포털]합니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-161">**HubName**: Use hello name of your notification hub that appears in hello hub blade in hello [Azure Portal].</span></span>
     
     <span data-ttu-id="2662b-162">`NotificationSettings` 코드:</span><span class="sxs-lookup"><span data-stu-id="2662b-162">`NotificationSettings` code:</span></span>
     
       <span data-ttu-id="2662b-163">공용 클래스 NotificationSettings {</span><span class="sxs-lookup"><span data-stu-id="2662b-163">public class NotificationSettings {</span></span>
     
           public static String SenderId = "<Your project number>";
           public static String HubName = "<Your HubName>";
           public static String HubListenConnectionString = "<Your default listen connection string>";
       <span data-ttu-id="2662b-164">}</span><span class="sxs-lookup"><span data-stu-id="2662b-164">}</span></span>
2. <span data-ttu-id="2662b-165">라는 다른 새 클래스 추가 위의 hello 단계를 사용 하 여 `MyInstanceIDService`합니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-165">Using hello steps above, add another new class named `MyInstanceIDService`.</span></span> <span data-ttu-id="2662b-166">이것으로 인스턴스 ID 수신기 서비스가 구현될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-166">This will be our Instance ID listener service implementation.</span></span>
   
    <span data-ttu-id="2662b-167">이 클래스에 대 한 hello 코드를 호출 합니다 우리의 `IntentService` 너무[새로 고침 hello GCM 토큰](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) hello 백그라운드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-167">hello code for this class will call our `IntentService` too[refresh hello GCM token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) in hello background.</span></span>
   
        import android.content.Intent;
        import android.util.Log;
        import com.google.android.gms.iid.InstanceIDListenerService;

        public class MyInstanceIDService extends InstanceIDListenerService {

            private static final String TAG = "MyInstanceIDService";

            @Override
            public void onTokenRefresh() {

                Log.i(TAG, "Refreshing GCM Registration Token");

                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        };


1. <span data-ttu-id="2662b-168">명명 된, 또 다른 새 클래스 tooyour 프로젝트 추가 `RegistrationIntentService`합니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-168">Add another new class tooyour project named, `RegistrationIntentService`.</span></span> <span data-ttu-id="2662b-169">이 대 한 hello 구현 됩니다 우리의 `IntentService` 처리할 수 있는 [hello GCM 토큰 새로 고침](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) 및 [hello 알림 허브 등록](notification-hubs-push-notification-registration-management.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-169">This will be hello implementation for our `IntentService` that will handle [refreshing hello GCM token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) and [registering with hello notification hub](notification-hubs-push-notification-registration-management.md).</span></span>
   
    <span data-ttu-id="2662b-170">이 클래스에 대 한 코드 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-170">Use hello following code for this class.</span></span>
   
        import android.app.IntentService;
        import android.content.Intent;
        import android.content.SharedPreferences;
        import android.preference.PreferenceManager;
        import android.util.Log;
   
        import com.google.android.gms.gcm.GoogleCloudMessaging;
        import com.google.android.gms.iid.InstanceID;
        import com.microsoft.windowsazure.messaging.NotificationHub;
   
        public class RegistrationIntentService extends IntentService {
   
            private static final String TAG = "RegIntentService";
   
            private NotificationHub hub;
   
            public RegistrationIntentService() {
                super(TAG);
            }
   
            @Override
            protected void onHandleIntent(Intent intent) {        
                SharedPreferences sharedPreferences = PreferenceManager.getDefaultSharedPreferences(this);
                String resultString = null;
                String regID = null;
   
                try {
                    InstanceID instanceID = InstanceID.getInstance(this);
                    String token = instanceID.getToken(NotificationSettings.SenderId,
                            GoogleCloudMessaging.INSTANCE_ID_SCOPE);        
                    Log.i(TAG, "Got GCM Registration Token: " + token);
   
                    // Storing hello registration id that indicates whether hello generated token has been
                    // sent tooyour server. If it is not stored, send hello token tooyour server,
                    // otherwise your server should have already received hello token.
                    if ((regID=sharedPreferences.getString("registrationID", null)) == null) {        
                        NotificationHub hub = new NotificationHub(NotificationSettings.HubName,
                                NotificationSettings.HubListenConnectionString, this);
                        Log.i(TAG, "Attempting tooregister with NH using token : " + token);
   
                        regID = hub.register(token).getRegistrationId();
   
                        // If you want toouse tags...
                        // Refer too: https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
                        // regID = hub.register(token, "tag1", "tag2").getRegistrationId();
   
                        resultString = "Registered Successfully - RegId : " + regID;
                        Log.i(TAG, resultString);        
                        sharedPreferences.edit().putString("registrationID", regID ).apply();
                    } else {
                        resultString = "Previously Registered Successfully - RegId : " + regID;
                    }
                } catch (Exception e) {
                    Log.e(TAG, resultString="Failed toocomplete token refresh", e);
                    // If an exception happens while fetching hello new token or updating our registration data
                    // on a third-party server, this ensures that we'll attempt hello update at a later time.
                }
   
                // Notify UI that registration has completed.
                if (MainActivity.isVisible) {
                    MainActivity.mainActivity.ToastNotify(resultString);
                }
            }
        }
2. <span data-ttu-id="2662b-171">사용자 `MainActivity` 클래스, hello 다음 추가 `import` hello 위의 문은 클래스 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-171">In your `MainActivity` class, add hello following `import` statements above hello class declaration.</span></span>
   
        import com.google.android.gms.common.ConnectionResult;
        import com.google.android.gms.common.GoogleApiAvailability;
        import com.google.android.gms.gcm.*;
        import com.microsoft.windowsazure.notifications.NotificationsManager;
        import android.util.Log;
        import android.widget.TextView;
        import android.widget.Toast;
3. <span data-ttu-id="2662b-172">Hello 다음 hello 위쪽 hello 클래스의 전용 멤버를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-172">Add hello following private members at hello top of hello class.</span></span> <span data-ttu-id="2662b-173">사용 하 여 이러한 [Google 권장 사항에 따라 Google Play 서비스의 hello 가용성을 확인](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk)합니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-173">We will use these [check hello availability of Google Play Services as recommended by Google](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk).</span></span>
   
        public static MainActivity mainActivity;
        public static Boolean isVisible = false;    
        private GoogleCloudMessaging gcm;
        private static final int PLAY_SERVICES_RESOLUTION_REQUEST = 9000;
4. <span data-ttu-id="2662b-174">사용자 `MainActivity` 클래스, Google Play 서비스 메서드 toohello 출시 이후 hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-174">In your `MainActivity` class, add hello following method toohello availability of Google Play Services.</span></span> 
   
        /**
         * Check hello device toomake sure it has hello Google Play Services APK. If
         * it doesn't, display a dialog that allows users toodownload hello APK from
         * hello Google Play Store or enable it in hello device's system settings.
         */
        private boolean checkPlayServices() {
            GoogleApiAvailability apiAvailability = GoogleApiAvailability.getInstance();
            int resultCode = apiAvailability.isGooglePlayServicesAvailable(this);
            if (resultCode != ConnectionResult.SUCCESS) {
                if (apiAvailability.isUserResolvableError(resultCode)) {
                    apiAvailability.getErrorDialog(this, resultCode, PLAY_SERVICES_RESOLUTION_REQUEST)
                            .show();
                } else {
                    Log.i(TAG, "This device is not supported by Google Play Services.");
                    ToastNotify("This device is not supported by Google Play Services.");
                    finish();
                }
                return false;
            }
            return true;
        }
5. <span data-ttu-id="2662b-175">사용자 `MainActivity` 클래스, Google Play 서비스를 호출 하기 전에 검사 하는 코드 다음 hello 추가 프로그램 `IntentService` tooget GCM 등록 토큰 및 알림 허브에 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-175">In your `MainActivity` class, add hello following code that will check for Google Play Services before calling your `IntentService` tooget your GCM registration token and register with your notification hub.</span></span>
   
        public void registerWithNotificationHubs()
        {
            Log.i(TAG, " Registering with Notification Hubs");
   
            if (checkPlayServices()) {
                // Start IntentService tooregister this application with GCM.
                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        }
6. <span data-ttu-id="2662b-176">Hello에 `OnCreate` hello 방식의 `MainActivity` 클래스 활동이 생성 될 때 코드 toostart hello 등록 프로세스를 수행 하는 hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-176">In hello `OnCreate` method of hello `MainActivity` class, add hello following code toostart hello registration process when activity is created.</span></span>
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            mainActivity = this;
            NotificationsManager.handleNotifications(this, NotificationSettings.SenderId, MyHandler.class);
            registerWithNotificationHubs();
        }
7. <span data-ttu-id="2662b-177">이러한 추가 메서드 toohello 추가 `MainActivity` 응용 프로그램에서 tooverify 앱 상태 및 보고 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-177">Add these additional methods toohello `MainActivity` tooverify app state and report status in your app.</span></span>
   
        @Override
        protected void onStart() {
            super.onStart();
            isVisible = true;
        }
   
        @Override
        protected void onPause() {
            super.onPause();
            isVisible = false;
        }
   
        @Override
        protected void onResume() {
            super.onResume();
            isVisible = true;
        }
   
        @Override
        protected void onStop() {
            super.onStop();
            isVisible = false;
        }
   
        public void ToastNotify(final String notificationMessage) {
            runOnUiThread(new Runnable() {
                @Override
                public void run() {
                    Toast.makeText(MainActivity.this, notificationMessage, Toast.LENGTH_LONG).show();
                    TextView helloText = (TextView) findViewById(R.id.text_hello);
                    helloText.setText(notificationMessage);
                }
            });
        }
8. <span data-ttu-id="2662b-178">hello `ToastNotify` 방법은 hello를 사용 하 여 *"Hello World"* `TextView` tooreport 상태 및 지속적으로 hello 앱에서 알림을 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-178">hello `ToastNotify` method uses hello *"Hello World"* `TextView` control tooreport status and notifications persistently in hello app.</span></span> <span data-ttu-id="2662b-179">Activity_main.xml 레이아웃에 hello 다음 해당 컨트롤에 대 한 id를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-179">In your activity_main.xml layout, add hello following id for that control.</span></span>
   
       android:id="@+id/text_hello"
9. <span data-ttu-id="2662b-180">다음 AndroidManifest.xml hello에 정의한 우리의 수신기에 대 한 하위 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-180">Next we will add a subclass for our receiver we defined in hello AndroidManifest.xml.</span></span> <span data-ttu-id="2662b-181">라는 또 다른 새 클래스 tooyour 프로젝트 추가 `MyHandler`합니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-181">Add another new class tooyour project named `MyHandler`.</span></span>
10. <span data-ttu-id="2662b-182">다음의 hello 위쪽 가져오기 조건 hello 추가 `MyHandler.java`:</span><span class="sxs-lookup"><span data-stu-id="2662b-182">Add hello following import statements at hello top of `MyHandler.java`:</span></span>
    
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.os.Bundle;
        import android.support.v4.app.NotificationCompat;
        import com.microsoft.windowsazure.notifications.NotificationsHandler;
11. <span data-ttu-id="2662b-183">Hello 코드 hello에 대 한 다음 추가 `MyHandler` 클래스의 서브 클래스를 만드는 `com.microsoft.windowsazure.notifications.NotificationsHandler`합니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-183">Add hello following code for hello `MyHandler` class making it a subclass of `com.microsoft.windowsazure.notifications.NotificationsHandler`.</span></span>
    
    <span data-ttu-id="2662b-184">이 코드는 hello 재정의 `OnReceive` 메서드를 사용할 수 없으므로 hello 처리기에 수신 되는 알림을 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-184">This code overrides hello `OnReceive` method, so hello handler will report notifications that are received.</span></span> <span data-ttu-id="2662b-185">hello 처리기 hello를 사용 하 여 hello 푸시 알림 toohello Android 알림 관리자를 함께 전송 `sendNotification()` 메서드.</span><span class="sxs-lookup"><span data-stu-id="2662b-185">hello handler also sends hello push notification toohello Android notification manager by using hello `sendNotification()` method.</span></span> <span data-ttu-id="2662b-186">hello `sendNotification()` hello 응용 프로그램은 실행 되지 하 고 알림의 받을 때 메서드를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-186">hello `sendNotification()` method should be executed when hello app is not running and a notification is received.</span></span>
    
        public class MyHandler extends NotificationsHandler {
            public static final int NOTIFICATION_ID = 1;
            private NotificationManager mNotificationManager;
            NotificationCompat.Builder builder;
            Context ctx;
    
            @Override
            public void onReceive(Context context, Bundle bundle) {
                ctx = context;
                String nhMessage = bundle.getString("message");
                sendNotification(nhMessage);
                if (MainActivity.isVisible) {
                    MainActivity.mainActivity.ToastNotify(nhMessage);
                }
            }
    
            private void sendNotification(String msg) {
    
                Intent intent = new Intent(ctx, MainActivity.class);
                intent.addFlags(Intent.FLAG_ACTIVITY_CLEAR_TOP);
    
                mNotificationManager = (NotificationManager)
                        ctx.getSystemService(Context.NOTIFICATION_SERVICE);
    
                PendingIntent contentIntent = PendingIntent.getActivity(ctx, 0,
                        intent, PendingIntent.FLAG_ONE_SHOT);
    
                Uri defaultSoundUri = RingtoneManager.getDefaultUri(RingtoneManager.TYPE_NOTIFICATION);
                NotificationCompat.Builder mBuilder =
                        new NotificationCompat.Builder(ctx)
                                .setSmallIcon(R.mipmap.ic_launcher)
                                .setContentTitle("Notification Hub Demo")
                                .setStyle(new NotificationCompat.BigTextStyle()
                                        .bigText(msg))
                                .setSound(defaultSoundUri)
                                .setContentText(msg);
    
                mBuilder.setContentIntent(contentIntent);
                mNotificationManager.notify(NOTIFICATION_ID, mBuilder.build());
            }
        }
12. <span data-ttu-id="2662b-187">Android Studio에서 hello 메뉴 모음에서 **빌드** > **프로젝트를 다시 작성** toomake 코드에 오류가 있는지 합니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-187">In Android Studio on hello menu bar, click **Build** > **Rebuild Project** toomake sure that no errors are present in your code.</span></span>

## <a name="sending-push-notifications"></a><span data-ttu-id="2662b-188">푸시 알림 보내기</span><span class="sxs-lookup"><span data-stu-id="2662b-188">Sending push notifications</span></span>
<span data-ttu-id="2662b-189">Hello를 통해 전송 하 여 앱에 푸시 알림을 받는 테스트할 수 [Azure 포털] -hello 찾아보십시오 **문제 해결** 아래와 같이 hello 허브 블레이드에서 섹션.</span><span class="sxs-lookup"><span data-stu-id="2662b-189">You can test receiving push notifications in your app by sending them via hello [Azure Portal] - look for hello **Troubleshooting** Section in hello hub blade, as shown below.</span></span>

![Azure 알림 허브 - 전송 테스트](./media/notification-hubs-android-get-started/notification-hubs-test-send.png)

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="optional-send-push-notifications-directly-from-hello-app"></a><span data-ttu-id="2662b-191">(선택 사항) Hello 앱에서 직접 푸시 알림을 보내려면</span><span class="sxs-lookup"><span data-stu-id="2662b-191">(Optional) Send push notifications directly from hello app</span></span>
<span data-ttu-id="2662b-192">일반적으로, 백 엔드 서버를 사용하여 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-192">Normally, you would send notifications using a backend server.</span></span> <span data-ttu-id="2662b-193">일부 경우 hello 클라이언트 응용 프로그램에서 직접 toobe 수 toosend 푸시 알림을 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-193">For some cases, you might want toobe able toosend push notifications directly from hello client application.</span></span> <span data-ttu-id="2662b-194">이 섹션에서는 방법을 사용 하 여 hello 클라이언트에서 toosend 알림 hello [Azure 알림 허브 REST API](https://msdn.microsoft.com/library/azure/dn223264.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-194">This section explains how toosend notifications from hello client using hello [Azure Notification Hub REST API](https://msdn.microsoft.com/library/azure/dn223264.aspx).</span></span>

1. <span data-ttu-id="2662b-195">Android Studio 프로젝트 뷰에서 **앱** > **src** > **기본** > **자원** > **레이아웃**을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-195">In Android Studio Project View, expand **App** > **src** > **main** > **res** > **layout**.</span></span> <span data-ttu-id="2662b-196">열기 hello `activity_main.xml` 레이아웃 파일을 hello 클릭 **텍스트** hello 파일의 tooupdate hello 텍스트 콘텐츠를 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-196">Open hello `activity_main.xml` layout file and click hello **Text** tab tooupdate hello text contents of hello file.</span></span> <span data-ttu-id="2662b-197">로 업데이트 hello 아래 코드에서 새로 추가 하는 `Button` 및 `EditText` 보내기 위한 컨트롤 알림 메시지 toohello 알림 허브 푸시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-197">Update it with hello code below, which adds new `Button` and `EditText` controls for sending push notification messages toohello notification hub.</span></span> <span data-ttu-id="2662b-198">바로 앞에 hello 맨 아래에이 코드를 추가 `</RelativeLayout>`합니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-198">Add this code at hello bottom, just before `</RelativeLayout>`.</span></span>
   
        <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/send_button"
        android:id="@+id/sendbutton"
        android:layout_centerVertical="true"
        android:layout_centerHorizontal="true"
        android:onClick="sendNotificationButtonOnClick" />
   
        <EditText
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:id="@+id/editTextNotificationMessage"
        android:layout_above="@+id/sendbutton"
        android:layout_centerHorizontal="true"
        android:layout_marginBottom="42dp"
        android:hint="@string/notification_message_hint" />
2. <span data-ttu-id="2662b-199">Android Studio 프로젝트 뷰에서 **앱** > **src** > **기본** > **자원** > **값**을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-199">In Android Studio Project View, expand **App** > **src** > **main** > **res** > **values**.</span></span> <span data-ttu-id="2662b-200">열기 hello `strings.xml` 파일을 새 hello에서 참조 되는 hello 문자열 값을 추가할 `Button` 및 `EditText` 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-200">Open hello `strings.xml` file and add hello string values that are referenced by hello new `Button` and `EditText` controls.</span></span> <span data-ttu-id="2662b-201">Hello hello 파일 맨 아래에 이러한 바로 앞에 추가 `</resources>`합니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-201">Add these at hello bottom of hello file, just before `</resources>`.</span></span>
   
        <string name="send_button">Send Notification</string>
        <string name="notification_message_hint">Enter notification message text</string>
3. <span data-ttu-id="2662b-202">사용자 `NotificationSetting.java` 파일에서 다음 설정을 toohello hello 추가 `NotificationSettings` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-202">In your `NotificationSetting.java` file, add hello following setting toohello `NotificationSettings` class.</span></span>
   
    <span data-ttu-id="2662b-203">업데이트 `HubFullAccess` hello로 **DefaultFullSharedAccessSignature** 허브에 대 한 연결 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-203">Update `HubFullAccess` with hello **DefaultFullSharedAccessSignature** connection string for your hub.</span></span> <span data-ttu-id="2662b-204">이 연결 문자열 hello에서 복사할 수 있습니다 [Azure 포털] 클릭 하 여 **액세스 정책을** hello에 **설정을** 블레이드 알림 허브에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-204">This connection string can be copied from hello [Azure Portal] by clicking **Access Policies** on hello **Settings** blade for your notification hub.</span></span>
   
        public static String HubFullAccess = "<Enter Your DefaultFullSharedAccess Connection string>";
4. <span data-ttu-id="2662b-205">사용자 `MainActivity.java` 파일, hello 다음 추가 `import` hello 위의 문은 `MainActivity` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-205">In your `MainActivity.java` file, add hello following `import` statements above hello `MainActivity` class.</span></span>
   
        import java.io.BufferedOutputStream;
        import java.io.BufferedReader;
        import java.io.InputStreamReader;
        import java.io.OutputStream;
        import java.net.HttpURLConnection;
        import java.net.URL;
        import java.net.URLEncoder;
        import javax.crypto.Mac;
        import javax.crypto.spec.SecretKeySpec;
        import android.util.Base64;
        import android.view.View;
        import android.widget.EditText;
5. <span data-ttu-id="2662b-206">사용자 `MainActivity.java` 파일, hello hello hello 위쪽에 있는 멤버를 다음 추가 `MainActivity` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-206">In your `MainActivity.java` file, add hello following members at hello top of hello `MainActivity` class.</span></span>    
   
        private String HubEndpoint = null;
        private String HubSasKeyName = null;
        private String HubSasKeyValue = null;
6. <span data-ttu-id="2662b-207">소프트웨어 액세스 서명 (SaS) 토큰 tooauthenticate POST 요청 toosend 메시지 tooyour 알림 허브를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-207">You must create a Software Access Signature (SaS) token tooauthenticate a POST request toosend messages tooyour notification hub.</span></span> <span data-ttu-id="2662b-208">이 hello hello 연결 문자열에서 키 데이터를 구문 분석 하 여 수행 되 고 hello에 설명 된 대로 SaS 토큰을 hello 만든 다음 [일반적인 개념](http://msdn.microsoft.com/library/azure/dn495627.aspx) REST API 참조입니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-208">This is done by parsing hello key data from hello connection string and then creating hello SaS token, as mentioned in hello [Common Concepts](http://msdn.microsoft.com/library/azure/dn495627.aspx) REST API reference.</span></span> <span data-ttu-id="2662b-209">hello 코드 다음에 예제 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-209">hello following code is an example implementation.</span></span>
   
    <span data-ttu-id="2662b-210">`MainActivity.java`, hello 메서드 toohello 다음 추가 `MainActivity` 클래스 tooparse 연결 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-210">In `MainActivity.java`, add hello following method toohello `MainActivity` class tooparse your connection string.</span></span>
   
        /**
         * Example code from http://msdn.microsoft.com/library/azure/dn495627.aspx
         * tooparse hello connection string so a SaS authentication token can be
         * constructed.
         *
         * @param connectionString This must be hello DefaultFullSharedAccess connection
         *                         string for this example.
         */
        private void ParseConnectionString(String connectionString)
        {
            String[] parts = connectionString.split(";");
            if (parts.length != 3)
                throw new RuntimeException("Error parsing connection string: "
                        + connectionString);
   
            for (int i = 0; i < parts.length; i++) {
                if (parts[i].startsWith("Endpoint")) {
                    this.HubEndpoint = "https" + parts[i].substring(11);
                } else if (parts[i].startsWith("SharedAccessKeyName")) {
                    this.HubSasKeyName = parts[i].substring(20);
                } else if (parts[i].startsWith("SharedAccessKey")) {
                    this.HubSasKeyValue = parts[i].substring(16);
                }
            }
        }
7. <span data-ttu-id="2662b-211">`MainActivity.java`, hello 메서드 toohello 다음 추가 `MainActivity` 클래스 toocreate SaS 인증 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-211">In `MainActivity.java`, add hello following method toohello `MainActivity` class toocreate a SaS authentication token.</span></span>
   
        /**
         * Example code from http://msdn.microsoft.com/library/azure/dn495627.aspx to
         * construct a SaS token from hello access key tooauthenticate a request.
         *
         * @param uri hello unencoded resource URI string for this operation. hello resource
         *            URI is hello full URI of hello Service Bus resource toowhich access is
         *            claimed. For example,
         *            "http://<namespace>.servicebus.windows.net/<hubName>"
         */
        private String generateSasToken(String uri) {
   
            String targetUri;
            String token = null;
            try {
                targetUri = URLEncoder
                        .encode(uri.toString().toLowerCase(), "UTF-8")
                        .toLowerCase();
   
                long expiresOnDate = System.currentTimeMillis();
                int expiresInMins = 60; // 1 hour
                expiresOnDate += expiresInMins * 60 * 1000;
                long expires = expiresOnDate / 1000;
                String toSign = targetUri + "\n" + expires;
   
                // Get an hmac_sha1 key from hello raw key bytes
                byte[] keyBytes = HubSasKeyValue.getBytes("UTF-8");
                SecretKeySpec signingKey = new SecretKeySpec(keyBytes, "HmacSHA256");
   
                // Get an hmac_sha1 Mac instance and initialize with hello signing key
                Mac mac = Mac.getInstance("HmacSHA256");
                mac.init(signingKey);
   
                // Compute hello hmac on input data bytes
                byte[] rawHmac = mac.doFinal(toSign.getBytes("UTF-8"));
   
                // Using android.util.Base64 for Android Studio instead of
                // Apache commons codec
                String signature = URLEncoder.encode(
                        Base64.encodeToString(rawHmac, Base64.NO_WRAP).toString(), "UTF-8");
   
                // Construct authorization string
                token = "SharedAccessSignature sr=" + targetUri + "&sig="
                        + signature + "&se=" + expires + "&skn=" + HubSasKeyName;
            } catch (Exception e) {
                if (isVisible) {
                    ToastNotify("Exception Generating SaS : " + e.getMessage().toString());
                }
            }
   
            return token;
        }
8. <span data-ttu-id="2662b-212">`MainActivity.java`, hello 메서드 toohello 다음 추가 `MainActivity` 클래스 toohandle hello **알림 보내기** 단추를 클릭 하 고 사용 하 여 메시지 toohello 허브 REST API를 기본 제공 hello hello 푸시 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-212">In `MainActivity.java`, add hello following method toohello `MainActivity` class toohandle hello **Send Notification** button click and send hello push notification message toohello hub by using hello built-in REST API.</span></span>
   
        /**
         * Send Notification button click handler. This method parses the
         * DefaultFullSharedAccess connection string and generates a SaS token. The
         * token is added toohello Authorization header on hello POST request toothe
         * notification hub. hello text in hello editTextNotificationMessage control
         * is added as hello JSON body for hello request tooadd a GCM message toohello hub.
         *
         * @param v
         */
        public void sendNotificationButtonOnClick(View v) {
            EditText notificationText = (EditText) findViewById(R.id.editTextNotificationMessage);
            final String json = "{\"data\":{\"message\":\"" + notificationText.getText().toString() + "\"}}";
   
            new Thread()
            {
                public void run()
                {
                    try
                    {
                        // Based on reference documentation...
                        // http://msdn.microsoft.com/library/azure/dn223273.aspx
                        ParseConnectionString(NotificationSettings.HubFullAccess);
                        URL url = new URL(HubEndpoint + NotificationSettings.HubName +
                                "/messages/?api-version=2015-01");
   
                        HttpURLConnection urlConnection = (HttpURLConnection)url.openConnection();
   
                        try {
                            // POST request
                            urlConnection.setDoOutput(true);
   
                            // Authenticate hello POST request with hello SaS token
                            urlConnection.setRequestProperty("Authorization", 
                                generateSasToken(url.toString()));
   
                            // Notification format should be GCM
                            urlConnection.setRequestProperty("ServiceBusNotification-Format", "gcm");
   
                            // Include any tags
                            // Example below targets 3 specific tags
                            // Refer too: https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
                            // urlConnection.setRequestProperty("ServiceBusNotification-Tags", 
                            //        "tag1 || tag2 || tag3");
   
                            // Send notification message
                            urlConnection.setFixedLengthStreamingMode(json.length());
                            OutputStream bodyStream = new BufferedOutputStream(urlConnection.getOutputStream());
                            bodyStream.write(json.getBytes());
                            bodyStream.close();
   
                            // Get reponse
                            urlConnection.connect();
                            int responseCode = urlConnection.getResponseCode();
                            if ((responseCode != 200) && (responseCode != 201)) {
                                BufferedReader br = new BufferedReader(new InputStreamReader((urlConnection.getErrorStream())));
                                String line;
                                StringBuilder builder = new StringBuilder("Send Notification returned " +
                                        responseCode + " : ")  ;
                                while ((line = br.readLine()) != null) {
                                    builder.append(line);
                                }
   
                                ToastNotify(builder.toString());
                            }
                        } finally {
                            urlConnection.disconnect();
                        }
                    }
                    catch(Exception e)
                    {
                        if (isVisible) {
                            ToastNotify("Exception Sending Notification : " + e.getMessage().toString());
                        }
                    }
                }
            }.start();
        }

## <a name="testing-your-app"></a><span data-ttu-id="2662b-213">앱 테스트</span><span class="sxs-lookup"><span data-stu-id="2662b-213">Testing your app</span></span>
#### <a name="push-notifications-in-hello-emulator"></a><span data-ttu-id="2662b-214">Hello 에뮬레이터에 대 한 푸시 알림</span><span class="sxs-lookup"><span data-stu-id="2662b-214">Push notifications in hello emulator</span></span>
<span data-ttu-id="2662b-215">에뮬레이터 내 tootest 푸시 알림을 하려는 경우 에뮬레이터 이미지 응용 프로그램에 대해 선택한 hello Google API 수준을 지원 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-215">If you want tootest push notifications inside an emulator, make sure that your emulator image supports hello Google API level that you chose for your app.</span></span> <span data-ttu-id="2662b-216">Hello로 결국 것 이미지 네이티브 Google Api를 지원 하지 않으면 **서비스\_하지\_사용 가능** 예외입니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-216">If your image doesn't support native Google APIs, you will end up with hello **SERVICE\_NOT\_AVAILABLE** exception.</span></span>

<span data-ttu-id="2662b-217">또한 위의 toohello에서 에뮬레이터를 실행 하 여 Google 계정 tooyour 추가 했는지 확인 **설정** > **계정**합니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-217">In addition toohello above, ensure that you have added your Google account tooyour running emulator under **Settings** > **Accounts**.</span></span> <span data-ttu-id="2662b-218">그렇지 않으면 GCM과 프로그램 시도 tooregister hello 발생할 수 있습니다 **인증\_실패** 예외입니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-218">Otherwise, your attempts tooregister with GCM may result in hello **AUTHENTICATION\_FAILED** exception.</span></span>

#### <a name="running-hello-application"></a><span data-ttu-id="2662b-219">Hello 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="2662b-219">Running hello application</span></span>
1. <span data-ttu-id="2662b-220">Hello 응용 프로그램을 실행 하 고 hello 등록 ID 성공적인 등록에 대 한 보고 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-220">Run hello app and notice that hello registration ID is reported for a successful registration.</span></span>
   
      ![Android에서 테스트 - 채널 등록][18]
2. <span data-ttu-id="2662b-222">Hello 허브에 등록 tooall Android 장치를 전송 하는 알림 메시지 toobe를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-222">Enter a notification message toobe sent tooall Android devices that have registered with hello hub.</span></span>
   
      ![Android에서 테스트 - 메시지 보내기][19]

3. <span data-ttu-id="2662b-224">**알림 보내기**를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-224">Press **Send Notification**.</span></span> <span data-ttu-id="2662b-225">Hello 응용 프로그램 실행을 설정한 모든 장치의 표시 됩니다는 `AlertDialog` hello 푸시 알림 메시지를 사용 하 여 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="2662b-225">Any devices that have hello app running will show an `AlertDialog` instance with hello push notification message.</span></span> <span data-ttu-id="2662b-226">푸시 알림을 응용 프로그램 실행 hello 필요는 없지만 이전에 등록 된 하는 장치는 hello Android 알림 관리자에에서는 알림을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-226">Devices that don't have hello app running but were previously registered for push notifications will receive a notification in hello Android Notification Manager.</span></span> <span data-ttu-id="2662b-227">Hello 왼쪽 위 모서리에서 아래로 살짝 밀면 하는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-227">Those can be viewed by swiping down from hello upper-left corner.</span></span>
   
      ![Android에서 테스트 - 알림][21]

## <a name="next-steps"></a><span data-ttu-id="2662b-229">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2662b-229">Next steps</span></span>
<span data-ttu-id="2662b-230">Hello 권장 [사용 하 여 알림 허브 toopush 알림 toousers] hello 다음 단계로 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-230">We recommend hello [Use Notification Hubs toopush notifications toousers] tutorial as hello next step.</span></span> <span data-ttu-id="2662b-231">설명에서 사용 하 여 ASP.NET 백 엔드 toosend 알림을 tootarget 특정 사용자에 게 태그를 삽입 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-231">It will show you how toosend notifications from an ASP.NET backend using tags tootarget specific users.</span></span>

<span data-ttu-id="2662b-232">관심 그룹으로 사용자 toosegment을 원하는 경우 hello를 확인해 [최신 뉴스 사용 하 여 알림 허브 toosend] 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-232">If you want toosegment your users by interest groups, check out hello [Use Notification Hubs toosend breaking news] tutorial.</span></span>

<span data-ttu-id="2662b-233">toolearn 알림 허브에 대 한 자세한 내용은 우리의 [알림 허브 지침]합니다.</span><span class="sxs-lookup"><span data-stu-id="2662b-233">toolearn more general information about Notification Hubs, see our [Notification Hubs Guidance].</span></span>

<!-- Images. -->
[6]: ./media/notification-hubs-android-get-started/notification-hub-android-new-class.png

[12]: ./media/notification-hubs-android-get-started/notification-hub-connection-strings.png

[13]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-new-project.png
[14]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-choose-form-factor.png
[15]: ./media/notification-hubs-android-get-started/notification-hub-create-android-app4.png
[16]: ./media/notification-hubs-android-get-started/notification-hub-create-android-app5.png
[17]: ./media/notification-hubs-android-get-started/notification-hub-create-android-app6.png

[18]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-registered.png
[19]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-set-message.png

[20]: ./media/notification-hubs-android-get-started/notification-hub-create-console-app.png
[21]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-received-message.png
[22]: ./media/notification-hubs-android-get-started/notification-hub-scheduler1.png
[23]: ./media/notification-hubs-android-get-started/notification-hub-scheduler2.png
[29]: ./media/mobile-services-android-get-started-push/mobile-eclipse-import-Play-library.png

[30]: ./media/notification-hubs-android-get-started/notification-hubs-debug-hub-gcm.png

[31]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-add-ui.png


<!-- URLs. -->
[Get started with push notifications in Mobile Services]: ../mobile-services-javascript-backend-android-get-started-push.md  
[Mobile Services Android SDK]: https://go.microsoft.com/fwLink/?LinkID=280126&clcid=0x409
[Referencing a library project]: http://go.microsoft.com/fwlink/?LinkId=389800
[Azure Classic Portal]: https://manage.windowsazure.com/
[알림 허브 지침]: http://msdn.microsoft.com/library/jj927170.aspx
[사용 하 여 알림 허브 toopush 알림 toousers]: notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md
[최신 뉴스 사용 하 여 알림 허브 toosend]: notification-hubs-aspnet-backend-android-xplat-segmented-gcm-push-notification.md
[Azure 포털]: https://portal.azure.com

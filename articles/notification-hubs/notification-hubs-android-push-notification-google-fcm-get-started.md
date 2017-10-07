---
title: "Azure 알림 허브와 Firebase Cloud Messaging aaaSending 푸시 알림 tooAndroid | Microsoft Docs"
description: "이 자습서에 설명 어떻게 toouse Azure 알림 허브 및 Firebase Cloud Messaging toopush 알림 tooAndroid 장치입니다."
services: notification-hubs
documentationcenter: android
keywords: "푸시 알림, 푸시알림, Android 푸시 알림, FCM, Firebase Cloud Messaging"
author: ysxu
manager: erikre
editor: 
ms.assetid: 02298560-da61-4bbb-b07c-e79bd520e420
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: hero-article
ms.date: 07/14/2016
ms.author: yuaxu
ms.openlocfilehash: d2e57437ac7b0ef77abf048f991043620621e58d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-tooandroid-with-azure-notification-hubs"></a><span data-ttu-id="93b0e-104">Azure 알림 허브 푸시 알림을 tooAndroid 보내기</span><span class="sxs-lookup"><span data-stu-id="93b0e-104">Sending push notifications tooAndroid with Azure Notification Hubs</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="93b0e-105">개요</span><span class="sxs-lookup"><span data-stu-id="93b0e-105">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="93b0e-106">이 항목에서는 FCM(Google Firebase Cloud Messaging)을 사용한 푸시 알림을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-106">This topic demonstrates push notifications with Google Firebase Cloud Messaging (FCM).</span></span> <span data-ttu-id="93b0e-107">Google 클라우드 메시징 (GCM), 여전히 사용 되는 경우 참조 [Azure 알림 허브와 GCM 보내는 푸시 알림 tooAndroid](notification-hubs-android-push-notification-google-gcm-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-107">If you are still using Google Cloud Messaging (GCM), see [Sending push notifications tooAndroid with Azure Notification Hubs and GCM](notification-hubs-android-push-notification-google-gcm-get-started.md).</span></span>
> 
> 

<span data-ttu-id="93b0e-108">이 자습서에서는 Azure 알림 허브 toouse 및 Firebase Cloud Messaging toosend 밀어넣기 알림 tooan Android 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-108">This tutorial shows you how toouse Azure Notification Hubs and Firebase Cloud Messaging toosend push notifications tooan Android application.</span></span>
<span data-ttu-id="93b0e-109">FCM(Firebase Cloud Messaging)을 사용하여 푸시 알림을 받는 빈 Android 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-109">You'll create a blank Android app that receives push notifications by using Firebase Cloud Messaging (FCM).</span></span>

[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="93b0e-110">이 자습서를 완료 하는 hello 코드 GitHub에서 다운로드할 수 있습니다 [여기](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStartedFirebase)합니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-110">hello completed code for this tutorial can be downloaded from GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStartedFirebase).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="93b0e-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="93b0e-111">Prerequisites</span></span>
> [!IMPORTANT]
> <span data-ttu-id="93b0e-112">toocomplete이이 자습서에서는 활성 Azure 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-112">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="93b0e-113">계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-113">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="93b0e-114">자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-android-get-started)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="93b0e-114">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-android-get-started).</span></span>
> 
> 

* <span data-ttu-id="93b0e-115">또한 tooan 활성 Azure 계정 위에서 언급 한이 자습서에서는 최신 버전의 hello [Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797)합니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-115">In addition tooan active Azure account mentioned above, this tutorial requires hello latest version of [Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797).</span></span>
* <span data-ttu-id="93b0e-116">Firebase Cloud Messaging에 Android 2.3 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-116">Android 2.3 or higher for Firebase Cloud Messaging.</span></span>
* <span data-ttu-id="93b0e-117">Firebase Cloud Messaging에 Google 리포지토리 수정 27 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-117">Google Repository revision 27 or higher is required for Firebase Cloud Messaging.</span></span>
* <span data-ttu-id="93b0e-118">Firebase Cloud Messaging에 Google Play Services 9.0.2 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-118">Google Play Services 9.0.2 or higher for Firebase Cloud Messaging.</span></span>
* <span data-ttu-id="93b0e-119">이 자습서를 완료해야 다른 모든 Android 앱용 알림 허브 자습서를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-119">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Android apps.</span></span>

## <a name="create-a-new-android-studio-project"></a><span data-ttu-id="93b0e-120">새 Android Studio 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="93b0e-120">Create a new Android Studio Project</span></span>
1. <span data-ttu-id="93b0e-121">Android Studio에서 새 Android Studio 프로젝트를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-121">In Android Studio, start a new Android Studio project.</span></span>
   
       ![Android Studio - new project](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-new-project.png)
2. <span data-ttu-id="93b0e-122">Hello 선택 **전화 및 태블릿** 폼 팩터 및 hello **최소 SDK** toosupport 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-122">Choose hello **Phone and Tablet** form factor and hello **Minimum SDK** that you want toosupport.</span></span> <span data-ttu-id="93b0e-123">그런 후 **Next**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-123">Then click **Next**.</span></span>
   
       ![Android Studio - project creation workflow](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-choose-form-factor.png)
3. <span data-ttu-id="93b0e-124">선택 **빈 활동** hello 기본 활동에 대 한 클릭 **다음**, 클릭 하 고 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-124">Choose **Empty Activity** for hello main activity, click **Next**, and then click **Finish**.</span></span>

## <a name="create-a-project-that-supports-firebase-cloud-messaging"></a><span data-ttu-id="93b0e-125">Firebase Cloud Messaging을 지원하는 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="93b0e-125">Create a project that supports Firebase Cloud Messaging</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-a-new-notification-hub"></a><span data-ttu-id="93b0e-126">새 알림 허브 구성</span><span class="sxs-lookup"><span data-stu-id="93b0e-126">Configure a new notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<span data-ttu-id="93b0e-127">&emsp;&emsp;6.</span><span class="sxs-lookup"><span data-stu-id="93b0e-127">&emsp;&emsp;6.</span></span> <span data-ttu-id="93b0e-128">Hello에 **설정** 선택 하면 알림 허브의 블레이드에서 **Notification Services** 차례로 **GCM (Google)**합니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-128">In hello **Settings** blade of your notification hub, select **Notification Services** and then **Google (GCM)**.</span></span> <span data-ttu-id="93b0e-129">Hello에서 앞에서 복사한 hello FCM 서버 키 입력 [Firebase 콘솔](https://firebase.google.com/console/) 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-129">Enter hello FCM server key you copied earlier from hello [Firebase console](https://firebase.google.com/console/) and click **Save**.</span></span>

&emsp;&emsp;![Azure 알림 허브 - Google(GCM)](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-gcm-api.png)

<span data-ttu-id="93b0e-131">알림 허브는 이제 Firebase 클라우드 Messagin와 구성 된 toowork 있고 hello 연결 문자열 tooboth 앱 tooreceive를 등록 하 고 푸시 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-131">Your notification hub is now configured toowork with Firebase Cloud Messagin, and you have hello connection strings tooboth register your app tooreceive and send push notifications.</span></span>

## <span data-ttu-id="93b0e-132"><a id="connecting-app"></a>응용 프로그램 toohello 알림 허브를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-132"><a id="connecting-app"></a>Connect your app toohello notification hub</span></span>
### <a name="add-google-play-services-toohello-project"></a><span data-ttu-id="93b0e-133">Google Play 서비스 toohello 프로젝트 추가</span><span class="sxs-lookup"><span data-stu-id="93b0e-133">Add Google Play services toohello project</span></span>
[!INCLUDE [Add Play Services](../../includes/notification-hubs-android-studio-add-google-play-services.md)]

### <a name="adding-azure-notification-hubs-libraries"></a><span data-ttu-id="93b0e-134">Azure 알림 허브 라이브러리 추가</span><span class="sxs-lookup"><span data-stu-id="93b0e-134">Adding Azure Notification Hubs libraries</span></span>
1. <span data-ttu-id="93b0e-135">Hello에 `Build.Gradle` hello에 대 한 파일 **앱**, hello hello에 있는 줄을 다음 추가 **종속성** 섹션.</span><span class="sxs-lookup"><span data-stu-id="93b0e-135">In hello `Build.Gradle` file for hello **app**, add hello following lines in hello **dependencies** section.</span></span>
   
        compile 'com.microsoft.azure:notification-hubs-android-sdk:0.4@aar'
        compile 'com.microsoft.azure:azure-notifications-handler:1.0.1@aar'
2. <span data-ttu-id="93b0e-136">추가 저장소 hello 후 다음 hello **종속성** 섹션.</span><span class="sxs-lookup"><span data-stu-id="93b0e-136">Add hello following repository after hello **dependencies** section.</span></span>
   
        repositories {
            maven {
                url "http://dl.bintray.com/microsoftazuremobile/SDK"
            }
        }

### <a name="updating-hello-androidmanifestxml"></a><span data-ttu-id="93b0e-137">Hello AndroidManifest.xml 업데이트 중입니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-137">Updating hello AndroidManifest.xml.</span></span>
1. <span data-ttu-id="93b0e-138">FCM toosupport 너무 사용 되는 코드에 인스턴스 ID 수신기 서비스를 구현 해야 했습니다[등록 토큰을 얻어](https://firebase.google.com/docs/cloud-messaging/android/client#sample-register) 를 사용 하 여 [Google의 FirebaseInstanceId API](https://firebase.google.com/docs/reference/android/com/google/firebase/iid/FirebaseInstanceId)합니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-138">toosupport FCM, we must implement a Instance ID listener service in our code which is used too[obtain registration tokens](https://firebase.google.com/docs/cloud-messaging/android/client#sample-register) using [Google's FirebaseInstanceId API](https://firebase.google.com/docs/reference/android/com/google/firebase/iid/FirebaseInstanceId).</span></span> <span data-ttu-id="93b0e-139">이 자습서에서는 hello 클래스 이름을 `MyInstanceIDService`합니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-139">In this tutorial we will name hello class `MyInstanceIDService`.</span></span> 
   
    <span data-ttu-id="93b0e-140">다음 hello 내 서비스 정의 toohello AndroidManifest.xml 파일 hello 추가 `<application>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-140">Add hello following service definition toohello AndroidManifest.xml file, inside hello `<application>` tag.</span></span> 
   
        <service android:name=".MyInstanceIDService">
            <intent-filter>
                <action android:name="com.google.firebase.INSTANCE_ID_EVENT"/>
            </intent-filter>
        </service>
2. <span data-ttu-id="93b0e-141">Hello FirebaseInstanceId API에서에서 우리의 FCM 등록 토큰을 수신 있습니다 사용할 것 너무[hello Azure 알림 허브로 등록](notification-hubs-push-notification-registration-management.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-141">Once we have received our FCM registration token from hello FirebaseInstanceId API, we will use it too[register with hello Azure Notification Hub](notification-hubs-push-notification-registration-management.md).</span></span> <span data-ttu-id="93b0e-142">이 등록 사용 하 여 hello 백그라운드에서 지원 되며는 `IntentService` 라는 `RegistrationIntentService`합니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-142">We will support this registration in hello background using an `IntentService` named `RegistrationIntentService`.</span></span> <span data-ttu-id="93b0e-143">이 서비스에는 FCM 등록 토큰 새로 고침에 대한 책임이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-143">This service will also be responsible for refreshing our FCM registration token.</span></span>
   
    <span data-ttu-id="93b0e-144">다음 hello 내 서비스 정의 toohello AndroidManifest.xml 파일 hello 추가 `<application>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-144">Add hello following service definition toohello AndroidManifest.xml file, inside hello `<application>` tag.</span></span> 
   
        <service
            android:name=".RegistrationIntentService"
            android:exported="false">
        </service>
3. <span data-ttu-id="93b0e-145">또한 수신기 tooreceive 알림의 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-145">We will also define a receiver tooreceive notifications.</span></span> <span data-ttu-id="93b0e-146">다음 hello 내부 수신기 정의 toohello AndroidManifest.xml 파일 hello 추가 `<application>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-146">Add hello following receiver definition toohello AndroidManifest.xml file, inside hello `<application>` tag.</span></span> <span data-ttu-id="93b0e-147">Hello 대체 `<your package>` 자리 표시자 hello hello hello 위쪽에 표시 된 프로그램 실제 패키지 이름을 `AndroidManifest.xml` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-147">Replace hello `<your package>` placeholder with hello your actual package name shown at hello top of hello `AndroidManifest.xml` file.</span></span>
   
        <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
            android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<your package name>" />
            </intent-filter>
        </receiver>
4. <span data-ttu-id="93b0e-148">필요한 FCM 다음 hello hello 아래 사용 권한 관련 추가 `</application>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-148">Add hello following necessary FCM related permissions below hello  `</application>` tag.</span></span> <span data-ttu-id="93b0e-149">있는지 tooreplace 확인 `<your package>` hello hello 위쪽에 표시 된 hello 패키지 이름의 `AndroidManifest.xml` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-149">Make sure tooreplace `<your package>` with hello package name shown at hello top of hello `AndroidManifest.xml` file.</span></span>
   
    <span data-ttu-id="93b0e-150">이러한 권한에 대 한 자세한 내용은 참조 [Android 용 GCM 클라이언트 응용 프로그램 설치](https://developers.google.com/cloud-messaging/android/client#manifest) 및 [Android tooFirebase Cloud Messaging에 대 한 GCM 클라이언트 응용 프로그램을 마이그레이션할](https://developers.google.com/cloud-messaging/android/android-migrate-fcm#remove_the_permissions_required_by_gcm)합니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-150">For more information on these permissions, see [Setup a GCM Client app for Android](https://developers.google.com/cloud-messaging/android/client#manifest) and [Migrate a GCM Client App for Android tooFirebase Cloud Messaging](https://developers.google.com/cloud-messaging/android/android-migrate-fcm#remove_the_permissions_required_by_gcm).</span></span>
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.GET_ACCOUNTS"/>
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />

### <a name="adding-code"></a><span data-ttu-id="93b0e-151">코드 추가</span><span class="sxs-lookup"><span data-stu-id="93b0e-151">Adding code</span></span>
1. <span data-ttu-id="93b0e-152">Hello 프로젝트 보기, 확장 **앱** > **src** > **주** > **java**합니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-152">In hello Project View, expand **app** > **src** > **main** > **java**.</span></span> <span data-ttu-id="93b0e-153">**java** 아래의 패키지 폴더를 마우스 오른쪽 단추로 클릭하고 **새로 만들기**, **Java 클래스**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-153">Right-click your package folder under **java**, click **New**, and then click **Java Class**.</span></span> <span data-ttu-id="93b0e-154">`NotificationSettings`(이)라는 새 클래스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-154">Add a new class named `NotificationSettings`.</span></span> 
   
    ![Android Studio - 새 Java 프로젝트](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hub-android-new-class.png)
   
    <span data-ttu-id="93b0e-156">Tooupdate hello 이러한 세 자리 표시자 hello hello에 대 한 코드 뒤에 있는지 확인 `NotificationSettings` 클래스:</span><span class="sxs-lookup"><span data-stu-id="93b0e-156">Make sure tooupdate hello these three placeholders in hello following code for hello `NotificationSettings` class:</span></span>
   
   * <span data-ttu-id="93b0e-157">**SenderId**: hello 앞에서 적어 둔 보낸 사람 Id hello **Cloud Messaging** hello에 프로젝트 설정에 탭 [Firebase 콘솔](https://firebase.google.com/console/)합니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-157">**SenderId**: hello Sender Id you obtained earlier in hello **Cloud Messaging** tab of your project settings in hello [Firebase console](https://firebase.google.com/console/).</span></span>
   * <span data-ttu-id="93b0e-158">**HubListenConnectionString**: hello **DefaultListenAccessSignature** 허브에 대 한 연결 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-158">**HubListenConnectionString**: hello **DefaultListenAccessSignature** connection string for your hub.</span></span> <span data-ttu-id="93b0e-159">클릭 하 여 해당 연결 문자열을 복사할 수는 있지만 **액세스 정책을** hello에 **설정** hello에 허브의 블레이드에서 [Azure 포털]합니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-159">You can copy that connection string by clicking **Access Policies** on hello **Settings** blade of your hub on hello [Azure Portal].</span></span>
   * <span data-ttu-id="93b0e-160">**HubName**: hello에 허브 블레이드 hello에에서 표시 되는 알림 허브의 hello 이름 사용 [Azure 포털]합니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-160">**HubName**: Use hello name of your notification hub that appears in hello hub blade in hello [Azure Portal].</span></span>
     
     <span data-ttu-id="93b0e-161">`NotificationSettings` 코드:</span><span class="sxs-lookup"><span data-stu-id="93b0e-161">`NotificationSettings` code:</span></span>
     
       <span data-ttu-id="93b0e-162">공용 클래스 NotificationSettings {</span><span class="sxs-lookup"><span data-stu-id="93b0e-162">public class NotificationSettings {</span></span>
     
           public static String SenderId = "<Your project number>";
           public static String HubName = "<Your HubName>";
           public static String HubListenConnectionString = "<Enter your DefaultListenSharedAccessSignature connection string>";
       <span data-ttu-id="93b0e-163">}</span><span class="sxs-lookup"><span data-stu-id="93b0e-163">}</span></span>
2. <span data-ttu-id="93b0e-164">라는 다른 새 클래스 추가 위의 hello 단계를 사용 하 여 `MyInstanceIDService`합니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-164">Using hello steps above, add another new class named `MyInstanceIDService`.</span></span> <span data-ttu-id="93b0e-165">이것으로 인스턴스 ID 수신기 서비스가 구현될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-165">This will be our Instance ID listener service implementation.</span></span>
   
    <span data-ttu-id="93b0e-166">이 클래스에 대 한 hello 코드를 호출 합니다 우리의 `IntentService` 너무[새로 고침 hello FCM 토큰](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) hello 백그라운드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-166">hello code for this class will call our `IntentService` too[refresh hello FCM token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) in hello background.</span></span>
   
        import android.content.Intent;
        import android.util.Log;
        import com.google.firebase.iid.FirebaseInstanceIdService;

        public class MyInstanceIDService extends FirebaseInstanceIdService {

            private static final String TAG = "MyInstanceIDService";

            @Override
            public void onTokenRefresh() {

                Log.d(TAG, "Refreshing GCM Registration Token");

                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        };


1. <span data-ttu-id="93b0e-167">명명 된, 또 다른 새 클래스 tooyour 프로젝트 추가 `RegistrationIntentService`합니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-167">Add another new class tooyour project named, `RegistrationIntentService`.</span></span> <span data-ttu-id="93b0e-168">이 대 한 hello 구현 됩니다 우리의 `IntentService` 처리할 수 있는 [hello FCM 토큰 새로 고침](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) 및 [hello 알림 허브 등록](notification-hubs-push-notification-registration-management.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-168">This will be hello implementation for our `IntentService` that will handle [refreshing hello FCM token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) and [registering with hello notification hub](notification-hubs-push-notification-registration-management.md).</span></span>
   
    <span data-ttu-id="93b0e-169">이 클래스에 대 한 코드 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-169">Use hello following code for this class.</span></span>
   
        import android.app.IntentService;
        import android.content.Intent;
        import android.content.SharedPreferences;
        import android.preference.PreferenceManager;
        import android.util.Log;        
        import com.google.firebase.iid.FirebaseInstanceId;
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
                String storedToken = null;
   
                try {
                    String FCM_token = FirebaseInstanceId.getInstance().getToken();
                    Log.d(TAG, "FCM Registration Token: " + FCM_token);
   
                    // Storing hello registration id that indicates whether hello generated token has been
                    // sent tooyour server. If it is not stored, send hello token tooyour server,
                    // otherwise your server should have already received hello token.
                    if (((regID=sharedPreferences.getString("registrationID", null)) == null)){
   
                        NotificationHub hub = new NotificationHub(NotificationSettings.HubName,
                                NotificationSettings.HubListenConnectionString, this);
                        Log.d(TAG, "Attempting a new registration with NH using FCM token : " + FCM_token);
                        regID = hub.register(FCM_token).getRegistrationId();
   
                        // If you want toouse tags...
                        // Refer too: https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
                        // regID = hub.register(token, "tag1,tag2").getRegistrationId();
   
                        resultString = "New NH Registration Successfully - RegId : " + regID;
                        Log.d(TAG, resultString);
   
                        sharedPreferences.edit().putString("registrationID", regID ).apply();
                        sharedPreferences.edit().putString("FCMtoken", FCM_token ).apply();
                    }
   
                    // Check if hello token may have been compromised and needs refreshing.
                    else if ((storedToken=sharedPreferences.getString("FCMtoken", "")) != FCM_token) {
   
                        NotificationHub hub = new NotificationHub(NotificationSettings.HubName,
                                NotificationSettings.HubListenConnectionString, this);
                        Log.d(TAG, "NH Registration refreshing with token : " + FCM_token);
                        regID = hub.register(FCM_token).getRegistrationId();
   
                        // If you want toouse tags...
                        // Refer too: https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
                        // regID = hub.register(token, "tag1,tag2").getRegistrationId();
   
                        resultString = "New NH Registration Successfully - RegId : " + regID;
                        Log.d(TAG, resultString);
   
                        sharedPreferences.edit().putString("registrationID", regID ).apply();
                        sharedPreferences.edit().putString("FCMtoken", FCM_token ).apply();
                    }
   
                    else {
                        resultString = "Previously Registered Successfully - RegId : " + regID;
                    }
                } catch (Exception e) {
                    Log.e(TAG, resultString="Failed toocomplete registration", e);
                    // If an exception happens while fetching hello new token or updating our registration data
                    // on a third-party server, this ensures that we'll attempt hello update at a later time.
                }
   
                // Notify UI that registration has completed.
                if (MainActivity.isVisible) {
                    MainActivity.mainActivity.ToastNotify(resultString);
                }
            }
        }
2. <span data-ttu-id="93b0e-170">사용자 `MainActivity` 클래스, hello 다음 추가 `import` hello 위의 문은 클래스 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-170">In your `MainActivity` class, add hello following `import` statements above hello class declaration.</span></span>
   
        import com.google.android.gms.common.ConnectionResult;
        import com.google.android.gms.common.GoogleApiAvailability;
        import com.microsoft.windowsazure.notifications.NotificationsManager;
        import android.content.Intent;
        import android.util.Log;
        import android.widget.TextView;
        import android.widget.Toast;
3. <span data-ttu-id="93b0e-171">Hello 다음 hello 위쪽 hello 클래스의 전용 멤버를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-171">Add hello following private members at hello top of hello class.</span></span> <span data-ttu-id="93b0e-172">사용 하 여 이러한 [Google 권장 사항에 따라 Google Play 서비스의 hello 가용성을 확인](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk)합니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-172">We will use these [check hello availability of Google Play Services as recommended by Google](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk).</span></span>
   
        public static MainActivity mainActivity;
        public static Boolean isVisible = false;    
        private static final String TAG = "MainActivity";
        private static final int PLAY_SERVICES_RESOLUTION_REQUEST = 9000;
4. <span data-ttu-id="93b0e-173">사용자 `MainActivity` 클래스, Google Play 서비스 메서드 toohello 출시 이후 hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-173">In your `MainActivity` class, add hello following method toohello availability of Google Play Services.</span></span> 
   
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
5. <span data-ttu-id="93b0e-174">사용자 `MainActivity` 클래스, Google Play 서비스를 호출 하기 전에 검사 하는 코드 다음 hello 추가 프로그램 `IntentService` tooget FCM 등록 토큰 및 알림 허브에 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-174">In your `MainActivity` class, add hello following code that will check for Google Play Services before calling your `IntentService` tooget your FCM registration token and register with your notification hub.</span></span>
   
        public void registerWithNotificationHubs()
        {
            if (checkPlayServices()) {
                // Start IntentService tooregister this application with FCM.
                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        }
6. <span data-ttu-id="93b0e-175">Hello에 `OnCreate` hello 방식의 `MainActivity` 클래스 활동이 생성 될 때 코드 toostart hello 등록 프로세스를 수행 하는 hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-175">In hello `OnCreate` method of hello `MainActivity` class, add hello following code toostart hello registration process when activity is created.</span></span>
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            mainActivity = this;
            NotificationsManager.handleNotifications(this, NotificationSettings.SenderId, MyHandler.class);
            registerWithNotificationHubs();
        }
7. <span data-ttu-id="93b0e-176">이러한 추가 메서드 toohello 추가 `MainActivity` 응용 프로그램에서 tooverify 앱 상태 및 보고 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-176">Add these additional methods toohello `MainActivity` tooverify app state and report status in your app.</span></span>
   
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
8. <span data-ttu-id="93b0e-177">hello `ToastNotify` 방법은 hello를 사용 하 여 *"Hello World"* `TextView` tooreport 상태 및 지속적으로 hello 앱에서 알림을 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-177">hello `ToastNotify` method uses hello *"Hello World"* `TextView` control tooreport status and notifications persistently in hello app.</span></span> <span data-ttu-id="93b0e-178">Activity_main.xml 레이아웃에 hello 다음 해당 컨트롤에 대 한 id를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-178">In your activity_main.xml layout, add hello following id for that control.</span></span>
   
       android:id="@+id/text_hello"
9. <span data-ttu-id="93b0e-179">다음 AndroidManifest.xml hello에 정의한 우리의 수신기에 대 한 하위 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-179">Next we will add a subclass for our receiver we defined in hello AndroidManifest.xml.</span></span> <span data-ttu-id="93b0e-180">라는 또 다른 새 클래스 tooyour 프로젝트 추가 `MyHandler`합니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-180">Add another new class tooyour project named `MyHandler`.</span></span>
10. <span data-ttu-id="93b0e-181">다음의 hello 위쪽 가져오기 조건 hello 추가 `MyHandler.java`:</span><span class="sxs-lookup"><span data-stu-id="93b0e-181">Add hello following import statements at hello top of `MyHandler.java`:</span></span>
    
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.media.RingtoneManager;
        import android.net.Uri;
        import android.os.Bundle;
        import android.support.v4.app.NotificationCompat;
        import com.microsoft.windowsazure.notifications.NotificationsHandler;
11. <span data-ttu-id="93b0e-182">Hello 코드 hello에 대 한 다음 추가 `MyHandler` 클래스의 서브 클래스를 만드는 `com.microsoft.windowsazure.notifications.NotificationsHandler`합니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-182">Add hello following code for hello `MyHandler` class making it a subclass of `com.microsoft.windowsazure.notifications.NotificationsHandler`.</span></span>
    
    <span data-ttu-id="93b0e-183">이 코드는 hello 재정의 `OnReceive` 메서드를 사용할 수 없으므로 hello 처리기에 수신 되는 알림을 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-183">This code overrides hello `OnReceive` method, so hello handler will report notifications that are received.</span></span> <span data-ttu-id="93b0e-184">hello 처리기 hello를 사용 하 여 hello 푸시 알림 toohello Android 알림 관리자를 함께 전송 `sendNotification()` 메서드.</span><span class="sxs-lookup"><span data-stu-id="93b0e-184">hello handler also sends hello push notification toohello Android notification manager by using hello `sendNotification()` method.</span></span> <span data-ttu-id="93b0e-185">hello `sendNotification()` hello 응용 프로그램은 실행 되지 하 고 알림의 받을 때 메서드를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-185">hello `sendNotification()` method should be executed when hello app is not running and a notification is received.</span></span>
    
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
12. <span data-ttu-id="93b0e-186">Android Studio에서 hello 메뉴 모음에서 **빌드** > **프로젝트를 다시 작성** toomake 코드에 오류가 있는지 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-186">In Android Studio on hello menu bar, click **Build** > **Rebuild Project** toomake sure that no errors are present in your code.</span></span>
13. <span data-ttu-id="93b0e-187">Hello 앱이 장치에서 실행 하 고 hello 알림 허브를 성공적으로 등록을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-187">Run hello app on your device and verify it registers successfully with hello notification hub.</span></span> 
    
    > [!NOTE]
    > <span data-ttu-id="93b0e-188">등록은 hello 초기 시작 시 hello까지 실패할 수 있습니다 `onTokenRefresh()` 인스턴스 Id 서비스의 메서드가 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-188">Registration may fail on hello initial launch until hello `onTokenRefresh()` method of instance Id service is called.</span></span> <span data-ttu-id="93b0e-189">hello 새로 고침 hello 알림 허브 등록을 성공적으로 실행을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-189">hello refresh should intiate a successful registration with hello notification hub.</span></span>
    > 
    > 

## <a name="sending-push-notifications"></a><span data-ttu-id="93b0e-190">푸시 알림 보내기</span><span class="sxs-lookup"><span data-stu-id="93b0e-190">Sending push notifications</span></span>
<span data-ttu-id="93b0e-191">Hello를 통해 전송 하 여 앱에 푸시 알림을 받는 테스트할 수 [Azure 포털] -hello 찾아보십시오 **문제 해결** 아래와 같이 hello 허브 블레이드에서 섹션.</span><span class="sxs-lookup"><span data-stu-id="93b0e-191">You can test receiving push notifications in your app by sending them via hello [Azure Portal] - look for hello **Troubleshooting** Section in hello hub blade, as shown below.</span></span>

![Azure 알림 허브 - 전송 테스트](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-test-send.png)

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="optional-send-push-notifications-directly-from-hello-app"></a><span data-ttu-id="93b0e-193">(선택 사항) Hello 앱에서 직접 푸시 알림을 보내려면</span><span class="sxs-lookup"><span data-stu-id="93b0e-193">(Optional) Send push notifications directly from hello app</span></span>
> [!IMPORTANT]
> <span data-ttu-id="93b0e-194">이 예에서는 hello 클라이언트 앱에서 알림을 보낼 학습 목적 으로만 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-194">This example of sending notifications from hello client app is provided for learning purposes only.</span></span> <span data-ttu-id="93b0e-195">이 경우 hello 해야 하므로 `DefaultFullSharedAccessSignature` toobe hello 클라이언트 응용 프로그램에 있는, 사용자 수 얻을 있는 액세스 권한이 없는 toosend 알림 tooyour 클라이언트 알림 허브 toohello 위험에 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-195">Since this will require hello `DefaultFullSharedAccessSignature` toobe present on hello client app, it exposes your notification hub toohello risk that a user may gain access toosend unauthorized notifications tooyour clients.</span></span>
> 
> 

<span data-ttu-id="93b0e-196">일반적으로, 백 엔드 서버를 사용하여 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-196">Normally, you would send notifications using a backend server.</span></span> <span data-ttu-id="93b0e-197">일부 경우 hello 클라이언트 응용 프로그램에서 직접 toobe 수 toosend 푸시 알림을 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-197">For some cases, you might want toobe able toosend push notifications directly from hello client application.</span></span> <span data-ttu-id="93b0e-198">이 섹션에서는 방법을 사용 하 여 hello 클라이언트에서 toosend 알림 hello [Azure 알림 허브 REST API](https://msdn.microsoft.com/library/azure/dn223264.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-198">This section explains how toosend notifications from hello client using hello [Azure Notification Hub REST API](https://msdn.microsoft.com/library/azure/dn223264.aspx).</span></span>

1. <span data-ttu-id="93b0e-199">Android Studio 프로젝트 뷰에서 **앱** > **src** > **기본** > **자원** > **레이아웃**을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-199">In Android Studio Project View, expand **App** > **src** > **main** > **res** > **layout**.</span></span> <span data-ttu-id="93b0e-200">열기 hello `activity_main.xml` 레이아웃 파일을 hello 클릭 **텍스트** hello 파일의 tooupdate hello 텍스트 콘텐츠를 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-200">Open hello `activity_main.xml` layout file and click hello **Text** tab tooupdate hello text contents of hello file.</span></span> <span data-ttu-id="93b0e-201">로 업데이트 hello 아래 코드에서 새로 추가 하는 `Button` 및 `EditText` 보내기 위한 컨트롤 알림 메시지 toohello 알림 허브 푸시 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-201">Update it with hello code below, which adds new `Button` and `EditText` controls for sending push notification messages toohello notification hub.</span></span> <span data-ttu-id="93b0e-202">바로 앞에 hello 맨 아래에이 코드를 추가 `</RelativeLayout>`합니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-202">Add this code at hello bottom, just before `</RelativeLayout>`.</span></span>
   
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
2. <span data-ttu-id="93b0e-203">Android Studio 프로젝트 뷰에서 **앱** > **src** > **기본** > **자원** > **값**을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-203">In Android Studio Project View, expand **App** > **src** > **main** > **res** > **values**.</span></span> <span data-ttu-id="93b0e-204">열기 hello `strings.xml` 파일을 새 hello에서 참조 되는 hello 문자열 값을 추가할 `Button` 및 `EditText` 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-204">Open hello `strings.xml` file and add hello string values that are referenced by hello new `Button` and `EditText` controls.</span></span> <span data-ttu-id="93b0e-205">Hello hello 파일 맨 아래에 이러한 바로 앞에 추가 `</resources>`합니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-205">Add these at hello bottom of hello file, just before `</resources>`.</span></span>
   
        <string name="send_button">Send Notification</string>
        <string name="notification_message_hint">Enter notification message text</string>
3. <span data-ttu-id="93b0e-206">사용자 `NotificationSetting.java` 파일에서 다음 설정을 toohello hello 추가 `NotificationSettings` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-206">In your `NotificationSetting.java` file, add hello following setting toohello `NotificationSettings` class.</span></span>
   
    <span data-ttu-id="93b0e-207">업데이트 `HubFullAccess` hello로 **DefaultFullSharedAccessSignature** 허브에 대 한 연결 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-207">Update `HubFullAccess` with hello **DefaultFullSharedAccessSignature** connection string for your hub.</span></span> <span data-ttu-id="93b0e-208">이 연결 문자열 hello에서 복사할 수 있습니다 [Azure 포털] 클릭 하 여 **액세스 정책을** hello에 **설정을** 블레이드 알림 허브에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-208">This connection string can be copied from hello [Azure Portal] by clicking **Access Policies** on hello **Settings** blade for your notification hub.</span></span>
   
        public static String HubFullAccess = "<Enter Your DefaultFullSharedAccessSignature Connection string>";
4. <span data-ttu-id="93b0e-209">사용자 `MainActivity.java` 파일, hello 다음 추가 `import` hello 위의 문은 `MainActivity` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-209">In your `MainActivity.java` file, add hello following `import` statements above hello `MainActivity` class.</span></span>
   
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
5. <span data-ttu-id="93b0e-210">사용자 `MainActivity.java` 파일, hello hello hello 위쪽에 있는 멤버를 다음 추가 `MainActivity` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-210">In your `MainActivity.java` file, add hello following members at hello top of hello `MainActivity` class.</span></span>    
   
        private String HubEndpoint = null;
        private String HubSasKeyName = null;
        private String HubSasKeyValue = null;
6. <span data-ttu-id="93b0e-211">소프트웨어 액세스 서명 (SaS) 토큰 tooauthenticate POST 요청 toosend 메시지 tooyour 알림 허브를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-211">You must create a Software Access Signature (SaS) token tooauthenticate a POST request toosend messages tooyour notification hub.</span></span> <span data-ttu-id="93b0e-212">이 hello hello 연결 문자열에서 키 데이터를 구문 분석 하 여 수행 되 고 hello에 설명 된 대로 SaS 토큰을 hello 만든 다음 [일반적인 개념](http://msdn.microsoft.com/library/azure/dn495627.aspx) REST API 참조입니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-212">This is done by parsing hello key data from hello connection string and then creating hello SaS token, as mentioned in hello [Common Concepts](http://msdn.microsoft.com/library/azure/dn495627.aspx) REST API reference.</span></span> <span data-ttu-id="93b0e-213">hello 코드 다음에 예제 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-213">hello following code is an example implementation.</span></span>
   
    <span data-ttu-id="93b0e-214">`MainActivity.java`, hello 메서드 toohello 다음 추가 `MainActivity` 클래스 tooparse 연결 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-214">In `MainActivity.java`, add hello following method toohello `MainActivity` class tooparse your connection string.</span></span>
   
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
7. <span data-ttu-id="93b0e-215">`MainActivity.java`, hello 메서드 toohello 다음 추가 `MainActivity` 클래스 toocreate SaS 인증 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-215">In `MainActivity.java`, add hello following method toohello `MainActivity` class toocreate a SaS authentication token.</span></span>
   
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
8. <span data-ttu-id="93b0e-216">`MainActivity.java`, hello 메서드 toohello 다음 추가 `MainActivity` 클래스 toohandle hello **알림 보내기** 단추를 클릭 하 고 사용 하 여 메시지 toohello 허브 REST API를 기본 제공 hello hello 푸시 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-216">In `MainActivity.java`, add hello following method toohello `MainActivity` class toohandle hello **Send Notification** button click and send hello push notification message toohello hub by using hello built-in REST API.</span></span>
   
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

## <a name="testing-your-app"></a><span data-ttu-id="93b0e-217">앱 테스트</span><span class="sxs-lookup"><span data-stu-id="93b0e-217">Testing your app</span></span>
#### <a name="push-notifications-in-hello-emulator"></a><span data-ttu-id="93b0e-218">Hello 에뮬레이터에 대 한 푸시 알림</span><span class="sxs-lookup"><span data-stu-id="93b0e-218">Push notifications in hello emulator</span></span>
<span data-ttu-id="93b0e-219">에뮬레이터 내 tootest 푸시 알림을 하려는 경우 에뮬레이터 이미지 응용 프로그램에 대해 선택한 hello Google API 수준을 지원 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-219">If you want tootest push notifications inside an emulator, make sure that your emulator image supports hello Google API level that you chose for your app.</span></span> <span data-ttu-id="93b0e-220">Hello로 결국 것 이미지 네이티브 Google Api를 지원 하지 않으면 **서비스\_하지\_사용 가능** 예외입니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-220">If your image doesn't support native Google APIs, you will end up with hello **SERVICE\_NOT\_AVAILABLE** exception.</span></span>

<span data-ttu-id="93b0e-221">또한 위의 toohello에서 에뮬레이터를 실행 하 여 Google 계정 tooyour 추가 했는지 확인 **설정** > **계정**합니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-221">In addition toohello above, ensure that you have added your Google account tooyour running emulator under **Settings** > **Accounts**.</span></span> <span data-ttu-id="93b0e-222">그렇지 않으면 GCM과 프로그램 시도 tooregister hello 발생할 수 있습니다 **인증\_실패** 예외입니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-222">Otherwise, your attempts tooregister with GCM may result in hello **AUTHENTICATION\_FAILED** exception.</span></span>

#### <a name="running-hello-application"></a><span data-ttu-id="93b0e-223">Hello 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="93b0e-223">Running hello application</span></span>
1. <span data-ttu-id="93b0e-224">Hello 응용 프로그램을 실행 하 고 hello 등록 ID 성공적인 등록에 대 한 보고 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-224">Run hello app and notice that hello registration ID is reported for a successful registration.</span></span>
   
       ![Testing on Android - Channel registration](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-registered.png)
2. <span data-ttu-id="93b0e-225">Hello 허브에 등록 tooall Android 장치를 전송 하는 알림 메시지 toobe를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-225">Enter a notification message toobe sent tooall Android devices that have registered with hello hub.</span></span>
   
       ![Testing on Android - sending a message](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-set-message.png)
3. <span data-ttu-id="93b0e-226">**알림 보내기**를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-226">Press **Send Notification**.</span></span> <span data-ttu-id="93b0e-227">Hello 응용 프로그램 실행을 설정한 모든 장치의 표시 됩니다는 `AlertDialog` hello 푸시 알림 메시지를 사용 하 여 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="93b0e-227">Any devices that have hello app running will show an `AlertDialog` instance with hello push notification message.</span></span> <span data-ttu-id="93b0e-228">푸시 알림을 응용 프로그램 실행 hello 필요는 없지만 이전에 등록 된 하는 장치는 hello Android 알림 관리자에에서는 알림을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-228">Devices that don't have hello app running but were previously registered for push notifications will receive a notification in hello Android Notification Manager.</span></span> <span data-ttu-id="93b0e-229">Hello 왼쪽 위 모서리에서 아래로 살짝 밀면 하는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-229">Those can be viewed by swiping down from hello upper-left corner.</span></span>
   
       ![Testing on Android - notifications](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-received-message.png)

## <a name="next-steps"></a><span data-ttu-id="93b0e-230">다음 단계</span><span class="sxs-lookup"><span data-stu-id="93b0e-230">Next steps</span></span>
<span data-ttu-id="93b0e-231">Hello 권장 [사용 하 여 알림 허브 toopush 알림 toousers] hello 다음 단계로 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-231">We recommend hello [Use Notification Hubs toopush notifications toousers] tutorial as hello next step.</span></span> <span data-ttu-id="93b0e-232">설명에서 사용 하 여 ASP.NET 백 엔드 toosend 알림을 tootarget 특정 사용자에 게 태그를 삽입 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-232">It will show you how toosend notifications from an ASP.NET backend using tags tootarget specific users.</span></span>

<span data-ttu-id="93b0e-233">관심 그룹으로 사용자 toosegment을 원하는 경우 hello를 확인해 [최신 뉴스 사용 하 여 알림 허브 toosend] 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-233">If you want toosegment your users by interest groups, check out hello [Use Notification Hubs toosend breaking news] tutorial.</span></span>

<span data-ttu-id="93b0e-234">toolearn 알림 허브에 대 한 자세한 내용은 우리의 [알림 허브 지침]합니다.</span><span class="sxs-lookup"><span data-stu-id="93b0e-234">toolearn more general information about Notification Hubs, see our [Notification Hubs Guidance].</span></span>

<!-- Images. -->



<!-- URLs. -->
[Get started with push notifications in Mobile Services]: ../mobile-services-javascript-backend-android-get-started-push.md  
[Mobile Services Android SDK]: https://go.microsoft.com/fwLink/?LinkID=280126&clcid=0x409
[Referencing a library project]: http://go.microsoft.com/fwlink/?LinkId=389800
[Azure Classic Portal]: https://manage.windowsazure.com/
[알림 허브 지침]: notification-hubs-push-notification-overview.md
[사용 하 여 알림 허브 toopush 알림 toousers]: notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md
[최신 뉴스 사용 하 여 알림 허브 toosend]: notification-hubs-aspnet-backend-android-xplat-segmented-gcm-push-notification.md
[Azure 포털]: https://portal.azure.com

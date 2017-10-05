---
title: "Azure 알림 허브 및 Firebase Cloud Messaging을 사용하여 Android에 푸시 알림 보내기 | Microsoft Docs"
description: "이 자습서에서 Azure 알림 허브 및 Firebase Cloud Messaging을 사용하여 Android 장치로 푸시 알림을 보내는 방법을 알아봅니다."
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
ms.openlocfilehash: 45a3fa5c7190e039fd637c78a41eeb3f6ede9bc7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="sending-push-notifications-to-android-with-azure-notification-hubs"></a><span data-ttu-id="c9caa-104">Azure 알림 허브를 사용하여 Android에 푸시 알림 보내기</span><span class="sxs-lookup"><span data-stu-id="c9caa-104">Sending push notifications to Android with Azure Notification Hubs</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="c9caa-105">개요</span><span class="sxs-lookup"><span data-stu-id="c9caa-105">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="c9caa-106">이 항목에서는 FCM(Google Firebase Cloud Messaging)을 사용한 푸시 알림을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-106">This topic demonstrates push notifications with Google Firebase Cloud Messaging (FCM).</span></span> <span data-ttu-id="c9caa-107">GCM(Google Cloud Messaging)을 사용하는 경우 [Azure 알림 허브 및 GCM을 사용하여 Android에 푸시 알림 보내기](notification-hubs-android-push-notification-google-gcm-get-started.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c9caa-107">If you are still using Google Cloud Messaging (GCM), see [Sending push notifications to Android with Azure Notification Hubs and GCM](notification-hubs-android-push-notification-google-gcm-get-started.md).</span></span>
> 
> 

<span data-ttu-id="c9caa-108">이 자습서에서는 Azure 알림 허브 및 Firebase Cloud Messaging을 사용하여 Android 응용 프로그램에 푸시 알림을 보내는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-108">This tutorial shows you how to use Azure Notification Hubs and Firebase Cloud Messaging to send push notifications to an Android application.</span></span>
<span data-ttu-id="c9caa-109">FCM(Firebase Cloud Messaging)을 사용하여 푸시 알림을 받는 빈 Android 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-109">You'll create a blank Android app that receives push notifications by using Firebase Cloud Messaging (FCM).</span></span>

[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="c9caa-110">이 자습서에 대해 완료된 코드는 GitHub의 [여기](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStartedFirebase)서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-110">The completed code for this tutorial can be downloaded from GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStartedFirebase).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c9caa-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c9caa-111">Prerequisites</span></span>
> [!IMPORTANT]
> <span data-ttu-id="c9caa-112">이 자습서를 완료하려면 활성 Azure 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-112">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="c9caa-113">계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-113">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="c9caa-114">자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-android-get-started)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c9caa-114">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-android-get-started).</span></span>
> 
> 

* <span data-ttu-id="c9caa-115">이 자습서에서는 위에서 언급한 활성 Azure 계정 외에도 [Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797)최신 버전이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-115">In addition to an active Azure account mentioned above, this tutorial requires the latest version of [Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797).</span></span>
* <span data-ttu-id="c9caa-116">Firebase Cloud Messaging에 Android 2.3 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-116">Android 2.3 or higher for Firebase Cloud Messaging.</span></span>
* <span data-ttu-id="c9caa-117">Firebase Cloud Messaging에 Google 리포지토리 수정 27 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-117">Google Repository revision 27 or higher is required for Firebase Cloud Messaging.</span></span>
* <span data-ttu-id="c9caa-118">Firebase Cloud Messaging에 Google Play Services 9.0.2 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-118">Google Play Services 9.0.2 or higher for Firebase Cloud Messaging.</span></span>
* <span data-ttu-id="c9caa-119">이 자습서를 완료해야 다른 모든 Android 앱용 알림 허브 자습서를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-119">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Android apps.</span></span>

## <a name="create-a-new-android-studio-project"></a><span data-ttu-id="c9caa-120">새 Android Studio 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="c9caa-120">Create a new Android Studio Project</span></span>
1. <span data-ttu-id="c9caa-121">Android Studio에서 새 Android Studio 프로젝트를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-121">In Android Studio, start a new Android Studio project.</span></span>
   
       ![Android Studio - new project](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-new-project.png)
2. <span data-ttu-id="c9caa-122">**휴대폰 및 태블릿** 폼 팩터와 지원할 **최소 SDK**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-122">Choose the **Phone and Tablet** form factor and the **Minimum SDK** that you want to support.</span></span> <span data-ttu-id="c9caa-123">그런 후 **Next**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-123">Then click **Next**.</span></span>
   
       ![Android Studio - project creation workflow](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-choose-form-factor.png)
3. <span data-ttu-id="c9caa-124">**빈 활동**을 기본 활동으로 선택하고 **다음**, **마침**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-124">Choose **Empty Activity** for the main activity, click **Next**, and then click **Finish**.</span></span>

## <a name="create-a-project-that-supports-firebase-cloud-messaging"></a><span data-ttu-id="c9caa-125">Firebase Cloud Messaging을 지원하는 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="c9caa-125">Create a project that supports Firebase Cloud Messaging</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-a-new-notification-hub"></a><span data-ttu-id="c9caa-126">새 알림 허브 구성</span><span class="sxs-lookup"><span data-stu-id="c9caa-126">Configure a new notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<span data-ttu-id="c9caa-127">&emsp;&emsp;6.</span><span class="sxs-lookup"><span data-stu-id="c9caa-127">&emsp;&emsp;6.</span></span> <span data-ttu-id="c9caa-128">알림 허브의 **설정** 블레이드에서 **알림 서비스**를 선택한 다음 **Google(GCM)**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-128">In the **Settings** blade of your notification hub, select **Notification Services** and then **Google (GCM)**.</span></span> <span data-ttu-id="c9caa-129">[Firebase 콘솔](https://firebase.google.com/console/) 에서 이전에 복사한 FCM 서버 키를 입력하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-129">Enter the FCM server key you copied earlier from the [Firebase console](https://firebase.google.com/console/) and click **Save**.</span></span>

&emsp;&emsp;![Azure 알림 허브 - Google(GCM)](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-gcm-api.png)

<span data-ttu-id="c9caa-131">이제 알림 허브가 Firebase Cloud Messaging과 작동하도록 구성되었으며, 푸시 알림을 받고 보내도록 앱을 등록하기 위한 연결 문자열이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-131">Your notification hub is now configured to work with Firebase Cloud Messagin, and you have the connection strings to both register your app to receive and send push notifications.</span></span>

## <span data-ttu-id="c9caa-132"><a id="connecting-app"></a>알림 허브에 앱 연결</span><span class="sxs-lookup"><span data-stu-id="c9caa-132"><a id="connecting-app"></a>Connect your app to the notification hub</span></span>
### <a name="add-google-play-services-to-the-project"></a><span data-ttu-id="c9caa-133">프로젝트에 Google Play Services 추가</span><span class="sxs-lookup"><span data-stu-id="c9caa-133">Add Google Play services to the project</span></span>
[!INCLUDE [Add Play Services](../../includes/notification-hubs-android-studio-add-google-play-services.md)]

### <a name="adding-azure-notification-hubs-libraries"></a><span data-ttu-id="c9caa-134">Azure 알림 허브 라이브러리 추가</span><span class="sxs-lookup"><span data-stu-id="c9caa-134">Adding Azure Notification Hubs libraries</span></span>
1. <span data-ttu-id="c9caa-135">**앱**의 `Build.Gradle` 파일에서 **종속성** 섹션에 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-135">In the `Build.Gradle` file for the **app**, add the following lines in the **dependencies** section.</span></span>
   
        compile 'com.microsoft.azure:notification-hubs-android-sdk:0.4@aar'
        compile 'com.microsoft.azure:azure-notifications-handler:1.0.1@aar'
2. <span data-ttu-id="c9caa-136">**종속성** 섹션 뒤에 다음 리포지토리를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-136">Add the following repository after the **dependencies** section.</span></span>
   
        repositories {
            maven {
                url "http://dl.bintray.com/microsoftazuremobile/SDK"
            }
        }

### <a name="updating-the-androidmanifestxml"></a><span data-ttu-id="c9caa-137">AndroidManifest.xml을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-137">Updating the AndroidManifest.xml.</span></span>
1. <span data-ttu-id="c9caa-138">FCM을 지원하기 위해, 코드에 [Google FirebaseInstanceId API](https://firebase.google.com/docs/reference/android/com/google/firebase/iid/FirebaseInstanceId)를 사용하여 [등록 토큰 가져오기](https://firebase.google.com/docs/cloud-messaging/android/client#sample-register)에 사용되는 인스턴스 ID 수신기 서비스를 구현해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-138">To support FCM, we must implement a Instance ID listener service in our code which is used to [obtain registration tokens](https://firebase.google.com/docs/cloud-messaging/android/client#sample-register) using [Google's FirebaseInstanceId API](https://firebase.google.com/docs/reference/android/com/google/firebase/iid/FirebaseInstanceId).</span></span> <span data-ttu-id="c9caa-139">이 자습서에서는 클래스의 이름을 `MyInstanceIDService`라고 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-139">In this tutorial we will name the class `MyInstanceIDService`.</span></span> 
   
    <span data-ttu-id="c9caa-140">AndroidManifest.xml 파일의 `<application>` 태그 내부에 다음 서비스 정의를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-140">Add the following service definition to the AndroidManifest.xml file, inside the `<application>` tag.</span></span> 
   
        <service android:name=".MyInstanceIDService">
            <intent-filter>
                <action android:name="com.google.firebase.INSTANCE_ID_EVENT"/>
            </intent-filter>
        </service>
2. <span data-ttu-id="c9caa-141">FirebaseInstanceId API에서 FCM 등록 토큰을 수신하면 해당 토큰을 사용하여 [Azure 알림 허브에 등록](notification-hubs-push-notification-registration-management.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-141">Once we have received our FCM registration token from the FirebaseInstanceId API, we will use it to [register with the Azure Notification Hub](notification-hubs-push-notification-registration-management.md).</span></span> <span data-ttu-id="c9caa-142">이 등록은 `RegistrationIntentService`라는 `IntentService`를 사용하여 백그라운드에서 지원될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-142">We will support this registration in the background using an `IntentService` named `RegistrationIntentService`.</span></span> <span data-ttu-id="c9caa-143">이 서비스에는 FCM 등록 토큰 새로 고침에 대한 책임이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-143">This service will also be responsible for refreshing our FCM registration token.</span></span>
   
    <span data-ttu-id="c9caa-144">AndroidManifest.xml 파일의 `<application>` 태그 내부에 다음 서비스 정의를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-144">Add the following service definition to the AndroidManifest.xml file, inside the `<application>` tag.</span></span> 
   
        <service
            android:name=".RegistrationIntentService"
            android:exported="false">
        </service>
3. <span data-ttu-id="c9caa-145">또한 알림을 수신하도록 수신기를 정의할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-145">We will also define a receiver to receive notifications.</span></span> <span data-ttu-id="c9caa-146">다음 수신기 정의를 `<application>` 태그 안의 AndroidManifest.xml 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-146">Add the following receiver definition to the AndroidManifest.xml file, inside the `<application>` tag.</span></span> <span data-ttu-id="c9caa-147">`<your package>` 자리 표시자를 `AndroidManifest.xml` 파일의 맨 위에 표시된 실제 패키지 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-147">Replace the `<your package>` placeholder with the your actual package name shown at the top of the `AndroidManifest.xml` file.</span></span>
   
        <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
            android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<your package name>" />
            </intent-filter>
        </receiver>
4. <span data-ttu-id="c9caa-148">`</application>` 태그 아래에 다음 필수 FCM 관련 권한을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-148">Add the following necessary FCM related permissions below the  `</application>` tag.</span></span> <span data-ttu-id="c9caa-149">반드시 `<your package>`을(를) `AndroidManifest.xml` 파일 맨 위에 있는 패키지 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-149">Make sure to replace `<your package>` with the package name shown at the top of the `AndroidManifest.xml` file.</span></span>
   
    <span data-ttu-id="c9caa-150">이러한 사용 권한에 대한 자세한 내용은 [Android용 GCM 클라이언트 앱 설치](https://developers.google.com/cloud-messaging/android/client#manifest) 및 [Firebase Cloud Messaging에 Android용 GCM 클라이언트 앱 마이그레이션](https://developers.google.com/cloud-messaging/android/android-migrate-fcm#remove_the_permissions_required_by_gcm)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c9caa-150">For more information on these permissions, see [Setup a GCM Client app for Android](https://developers.google.com/cloud-messaging/android/client#manifest) and [Migrate a GCM Client App for Android to Firebase Cloud Messaging](https://developers.google.com/cloud-messaging/android/android-migrate-fcm#remove_the_permissions_required_by_gcm).</span></span>
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.GET_ACCOUNTS"/>
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />

### <a name="adding-code"></a><span data-ttu-id="c9caa-151">코드 추가</span><span class="sxs-lookup"><span data-stu-id="c9caa-151">Adding code</span></span>
1. <span data-ttu-id="c9caa-152">프로젝트 뷰에서 **앱** > **src** > **기본** > **java**를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-152">In the Project View, expand **app** > **src** > **main** > **java**.</span></span> <span data-ttu-id="c9caa-153">**java** 아래의 패키지 폴더를 마우스 오른쪽 단추로 클릭하고 **새로 만들기**, **Java 클래스**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-153">Right-click your package folder under **java**, click **New**, and then click **Java Class**.</span></span> <span data-ttu-id="c9caa-154">`NotificationSettings`(이)라는 새 클래스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-154">Add a new class named `NotificationSettings`.</span></span> 
   
    ![Android Studio - 새 Java 프로젝트](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hub-android-new-class.png)
   
    <span data-ttu-id="c9caa-156">`NotificationSettings` 클래스에 대한 다음 코드에서 아래 세 개의 자리 표시자를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-156">Make sure to update the these three placeholders in the following code for the `NotificationSettings` class:</span></span>
   
   * <span data-ttu-id="c9caa-157">**SenderId**: [Firebase 콘솔](https://firebase.google.com/console/)의 프로젝트 설정에 있는 **클라우드 메시징** 탭에서 이전에 가져온 보낸 사람 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-157">**SenderId**: The Sender Id you obtained earlier in the **Cloud Messaging** tab of your project settings in the [Firebase console](https://firebase.google.com/console/).</span></span>
   * <span data-ttu-id="c9caa-158">**HubListenConnectionString**: 허브의 **DefaultListenAccessSignature** 연결 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-158">**HubListenConnectionString**: The **DefaultListenAccessSignature** connection string for your hub.</span></span> <span data-ttu-id="c9caa-159">[Azure Portal]에 있는 허브의 **설정** 블레이드에서 **액세스 정책**을 클릭하여 이 연결 문자열을 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-159">You can copy that connection string by clicking **Access Policies** on the **Settings** blade of your hub on the [Azure Portal].</span></span>
   * <span data-ttu-id="c9caa-160">**HubName**: [Azure Portal]의 허브 블레이드에 표시되는 알림 허브 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-160">**HubName**: Use the name of your notification hub that appears in the hub blade in the [Azure Portal].</span></span>
     
     <span data-ttu-id="c9caa-161">`NotificationSettings` 코드:</span><span class="sxs-lookup"><span data-stu-id="c9caa-161">`NotificationSettings` code:</span></span>
     
       <span data-ttu-id="c9caa-162">공용 클래스 NotificationSettings {</span><span class="sxs-lookup"><span data-stu-id="c9caa-162">public class NotificationSettings {</span></span>
     
           public static String SenderId = "<Your project number>";
           public static String HubName = "<Your HubName>";
           public static String HubListenConnectionString = "<Enter your DefaultListenSharedAccessSignature connection string>";
       <span data-ttu-id="c9caa-163">}</span><span class="sxs-lookup"><span data-stu-id="c9caa-163">}</span></span>
2. <span data-ttu-id="c9caa-164">위의 단계에 따라 `MyInstanceIDService`라는 또 다른 새 클래스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-164">Using the steps above, add another new class named `MyInstanceIDService`.</span></span> <span data-ttu-id="c9caa-165">이것으로 인스턴스 ID 수신기 서비스가 구현될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-165">This will be our Instance ID listener service implementation.</span></span>
   
    <span data-ttu-id="c9caa-166">이 클래스의 코드는 `IntentService` 를 호출하여 백그라운드에서 [FCM 토큰을 새로 고칩니다](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) .</span><span class="sxs-lookup"><span data-stu-id="c9caa-166">The code for this class will call our `IntentService` to [refresh the FCM token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) in the background.</span></span>
   
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


1. <span data-ttu-id="c9caa-167">`RegistrationIntentService`라는 프로젝트에 또 다른 새 클래스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-167">Add another new class to your project named, `RegistrationIntentService`.</span></span> <span data-ttu-id="c9caa-168">그러면 [FCM 토큰 새로 고침](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) 및 [알림 허브 등록](notification-hubs-push-notification-registration-management.md)을 처리하는 `IntentService`에 대한 솔루션이 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-168">This will be the implementation for our `IntentService` that will handle [refreshing the FCM token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) and [registering with the notification hub](notification-hubs-push-notification-registration-management.md).</span></span>
   
    <span data-ttu-id="c9caa-169">이 클래스에 대해 다음 코드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-169">Use the following code for this class.</span></span>
   
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
   
                    // Storing the registration id that indicates whether the generated token has been
                    // sent to your server. If it is not stored, send the token to your server,
                    // otherwise your server should have already received the token.
                    if (((regID=sharedPreferences.getString("registrationID", null)) == null)){
   
                        NotificationHub hub = new NotificationHub(NotificationSettings.HubName,
                                NotificationSettings.HubListenConnectionString, this);
                        Log.d(TAG, "Attempting a new registration with NH using FCM token : " + FCM_token);
                        regID = hub.register(FCM_token).getRegistrationId();
   
                        // If you want to use tags...
                        // Refer to : https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
                        // regID = hub.register(token, "tag1,tag2").getRegistrationId();
   
                        resultString = "New NH Registration Successfully - RegId : " + regID;
                        Log.d(TAG, resultString);
   
                        sharedPreferences.edit().putString("registrationID", regID ).apply();
                        sharedPreferences.edit().putString("FCMtoken", FCM_token ).apply();
                    }
   
                    // Check if the token may have been compromised and needs refreshing.
                    else if ((storedToken=sharedPreferences.getString("FCMtoken", "")) != FCM_token) {
   
                        NotificationHub hub = new NotificationHub(NotificationSettings.HubName,
                                NotificationSettings.HubListenConnectionString, this);
                        Log.d(TAG, "NH Registration refreshing with token : " + FCM_token);
                        regID = hub.register(FCM_token).getRegistrationId();
   
                        // If you want to use tags...
                        // Refer to : https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
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
                    Log.e(TAG, resultString="Failed to complete registration", e);
                    // If an exception happens while fetching the new token or updating our registration data
                    // on a third-party server, this ensures that we'll attempt the update at a later time.
                }
   
                // Notify UI that registration has completed.
                if (MainActivity.isVisible) {
                    MainActivity.mainActivity.ToastNotify(resultString);
                }
            }
        }
2. <span data-ttu-id="c9caa-170">`MainActivity` 클래스에서 다음 `import` 문을 클래스 선언 위에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-170">In your `MainActivity` class, add the following `import` statements above the class declaration.</span></span>
   
        import com.google.android.gms.common.ConnectionResult;
        import com.google.android.gms.common.GoogleApiAvailability;
        import com.microsoft.windowsazure.notifications.NotificationsManager;
        import android.content.Intent;
        import android.util.Log;
        import android.widget.TextView;
        import android.widget.Toast;
3. <span data-ttu-id="c9caa-171">클래스의 맨 위에 다음과 같은 private 멤버를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-171">Add the following private members at the top of the class.</span></span> <span data-ttu-id="c9caa-172">[Google 권장 사항에 따라 Google Play Services의 가용성을 확인](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk)합니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-172">We will use these [check the availability of Google Play Services as recommended by Google](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk).</span></span>
   
        public static MainActivity mainActivity;
        public static Boolean isVisible = false;    
        private static final String TAG = "MainActivity";
        private static final int PLAY_SERVICES_RESOLUTION_REQUEST = 9000;
4. <span data-ttu-id="c9caa-173">`MainActivity` 클래스에서 Google Play Services 가용성에 다음 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-173">In your `MainActivity` class, add the following method to the availability of Google Play Services.</span></span> 
   
        /**
         * Check the device to make sure it has the Google Play Services APK. If
         * it doesn't, display a dialog that allows users to download the APK from
         * the Google Play Store or enable it in the device's system settings.
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
5. <span data-ttu-id="c9caa-174">`MainActivity` 클래스에서 Google Play Services를 검사한 후 `IntentService`를 호출하는 다음 코드를 추가하여 FCM 등록 토큰을 가져와서 알림 허브에 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-174">In your `MainActivity` class, add the following code that will check for Google Play Services before calling your `IntentService` to get your FCM registration token and register with your notification hub.</span></span>
   
        public void registerWithNotificationHubs()
        {
            if (checkPlayServices()) {
                // Start IntentService to register this application with FCM.
                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        }
6. <span data-ttu-id="c9caa-175">`MainActivity` 클래스의 `OnCreate` 메서드에서 활동이 생성되면 등록 프로세스를 시작하는 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-175">In the `OnCreate` method of the `MainActivity` class, add the following code to start the registration process when activity is created.</span></span>
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            mainActivity = this;
            NotificationsManager.handleNotifications(this, NotificationSettings.SenderId, MyHandler.class);
            registerWithNotificationHubs();
        }
7. <span data-ttu-id="c9caa-176">`MainActivity` 에 이러한 추가 메서드를 추가하여 앱 상태를 확인하고 앱에서 상태를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-176">Add these additional methods to the `MainActivity` to verify app state and report status in your app.</span></span>
   
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
8. <span data-ttu-id="c9caa-177">`ToastNotify` 메서드는 *"Hello World"* `TextView` 컨트롤을 사용하여 앱에서 영구적으로 상태 및 알림을 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-177">The `ToastNotify` method uses the *"Hello World"* `TextView` control to report status and notifications persistently in the app.</span></span> <span data-ttu-id="c9caa-178">activity_main.xml 레이아웃에서 해당 컨트롤에 대한 다음 ID를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-178">In your activity_main.xml layout, add the following id for that control.</span></span>
   
       android:id="@+id/text_hello"
9. <span data-ttu-id="c9caa-179">다음으로 AndroidManifest.xml에서 정의한 수신기에 대한 하위 클래스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-179">Next we will add a subclass for our receiver we defined in the AndroidManifest.xml.</span></span> <span data-ttu-id="c9caa-180">`MyHandler`라는 프로젝트에 또 다른 새 클래스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-180">Add another new class to your project named `MyHandler`.</span></span>
10. <span data-ttu-id="c9caa-181">그런 다음 `MyHandler.java`의 맨 위에 다음 import 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-181">Add the following import statements at the top of `MyHandler.java`:</span></span>
    
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.media.RingtoneManager;
        import android.net.Uri;
        import android.os.Bundle;
        import android.support.v4.app.NotificationCompat;
        import com.microsoft.windowsazure.notifications.NotificationsHandler;
11. <span data-ttu-id="c9caa-182">`MyHandler` 클래스에 대해 다음 코드를 추가하여 `com.microsoft.windowsazure.notifications.NotificationsHandler`의 하위 클래스로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-182">Add the following code for the `MyHandler` class making it a subclass of `com.microsoft.windowsazure.notifications.NotificationsHandler`.</span></span>
    
    <span data-ttu-id="c9caa-183">이 코드는 처리기가 받은 알림을 보고할 수 있도록 `OnReceive` 메서드를 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-183">This code overrides the `OnReceive` method, so the handler will report notifications that are received.</span></span> <span data-ttu-id="c9caa-184">또한 처리기는 `sendNotification()` 메서드를 사용하여 Android 알림 관리자에 푸시 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-184">The handler also sends the push notification to the Android notification manager by using the `sendNotification()` method.</span></span> <span data-ttu-id="c9caa-185">`sendNotification()` 메서드는 앱이 실행되지 않을 때, 알림이 수신될 때 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-185">The `sendNotification()` method should be executed when the app is not running and a notification is received.</span></span>
    
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
12. <span data-ttu-id="c9caa-186">Android Studio의 메뉴 모음에서 **빌드** > **프로젝트 다시 빌드**를 클릭하여 코드에 오류가 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-186">In Android Studio on the menu bar, click **Build** > **Rebuild Project** to make sure that no errors are present in your code.</span></span>
13. <span data-ttu-id="c9caa-187">장치에서 앱을 실행하고 알림 허브를 사용하여 성공적으로 등록되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-187">Run the app on your device and verify it registers successfully with the notification hub.</span></span> 
    
    > [!NOTE]
    > <span data-ttu-id="c9caa-188">등록은 인스턴스 ID 서비스의 `onTokenRefresh()` 메서드를 호출할 때까지 초기 시작 시 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-188">Registration may fail on the initial launch until the `onTokenRefresh()` method of instance Id service is called.</span></span> <span data-ttu-id="c9caa-189">새로 고침은 알림 허브를 사용하여 성공적으로 등록하기 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-189">The refresh should intiate a successful registration with the notification hub.</span></span>
    > 
    > 

## <a name="sending-push-notifications"></a><span data-ttu-id="c9caa-190">푸시 알림 보내기</span><span class="sxs-lookup"><span data-stu-id="c9caa-190">Sending push notifications</span></span>
<span data-ttu-id="c9caa-191">[Azure Portal]을 통해 푸시 알림을 보내서 앱에서 푸시 알림 수신을 테스트할 수 있습니다. 아래와 같이 허브 블레이드의 **문제 해결** 섹션을 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="c9caa-191">You can test receiving push notifications in your app by sending them via the [Azure Portal] - look for the **Troubleshooting** Section in the hub blade, as shown below.</span></span>

![Azure 알림 허브 - 전송 테스트](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-test-send.png)

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="optional-send-push-notifications-directly-from-the-app"></a><span data-ttu-id="c9caa-193">(선택 사항) 앱에서 바로 푸시 알림 보내기</span><span class="sxs-lookup"><span data-stu-id="c9caa-193">(Optional) Send push notifications directly from the app</span></span>
> [!IMPORTANT]
> <span data-ttu-id="c9caa-194">클라이언트 앱에서 알림을 보내는 이 예제는 학습 목적으로만 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-194">This example of sending notifications from the client app is provided for learning purposes only.</span></span> <span data-ttu-id="c9caa-195">이를 위해서 `DefaultFullSharedAccessSignature` 이 클라이언트 응용 프로그램에 표시되어야 하므로 사용자가 클라이언트에 무단으로 알림을 보내는 액세스 권한을 가질 수 있는 위험에 알림 허브가 노출됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-195">Since this will require the `DefaultFullSharedAccessSignature` to be present on the client app, it exposes your notification hub to the risk that a user may gain access to send unauthorized notifications to your clients.</span></span>
> 
> 

<span data-ttu-id="c9caa-196">일반적으로, 백 엔드 서버를 사용하여 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-196">Normally, you would send notifications using a backend server.</span></span> <span data-ttu-id="c9caa-197">경우에 따라, 클라이언트 응용 프로그램에서 직접 푸시 알림을 보낼 수 있기를 원하기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-197">For some cases, you might want to be able to send push notifications directly from the client application.</span></span> <span data-ttu-id="c9caa-198">이 섹션은 [Azure 알림 허브 REST API](https://msdn.microsoft.com/library/azure/dn223264.aspx)를 사용하여 클라이언트에서 알림을 보내는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-198">This section explains how to send notifications from the client using the [Azure Notification Hub REST API](https://msdn.microsoft.com/library/azure/dn223264.aspx).</span></span>

1. <span data-ttu-id="c9caa-199">Android Studio 프로젝트 뷰에서 **앱** > **src** > **기본** > **자원** > **레이아웃**을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-199">In Android Studio Project View, expand **App** > **src** > **main** > **res** > **layout**.</span></span> <span data-ttu-id="c9caa-200">`activity_main.xml` 레이아웃 파일을 열고 **텍스트** 탭을 클릭하여 파일의 텍스트 내용을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-200">Open the `activity_main.xml` layout file and click the **Text** tab to update the text contents of the file.</span></span> <span data-ttu-id="c9caa-201">아래 코드로 업데이트하여 알림 허브에 푸시 알림 메시지를 보내는 새 `Button` 및 `EditText` 컨트롤을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-201">Update it with the code below, which adds new `Button` and `EditText` controls for sending push notification messages to the notification hub.</span></span> <span data-ttu-id="c9caa-202">이 코드를 맨 아래의 `</RelativeLayout>`바로 앞에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-202">Add this code at the bottom, just before `</RelativeLayout>`.</span></span>
   
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
2. <span data-ttu-id="c9caa-203">Android Studio 프로젝트 뷰에서 **앱** > **src** > **기본** > **자원** > **값**을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-203">In Android Studio Project View, expand **App** > **src** > **main** > **res** > **values**.</span></span> <span data-ttu-id="c9caa-204">`strings.xml` 파일을 열고 새 `Button` 및 `EditText` 컨트롤에서 참조하는 문자열 값을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-204">Open the `strings.xml` file and add the string values that are referenced by the new `Button` and `EditText` controls.</span></span> <span data-ttu-id="c9caa-205">파일 맨 아래의 `</resources>`바로 앞에 이를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-205">Add these at the bottom of the file, just before `</resources>`.</span></span>
   
        <string name="send_button">Send Notification</string>
        <string name="notification_message_hint">Enter notification message text</string>
3. <span data-ttu-id="c9caa-206">`NotificationSetting.java` 파일에서 `NotificationSettings` 클래스에 다음 설정을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-206">In your `NotificationSetting.java` file, add the following setting to the `NotificationSettings` class.</span></span>
   
    <span data-ttu-id="c9caa-207">허브에 **DefaultFullSharedAccessSignature** 연결 문자열을 사용하여 `HubFullAccess`을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-207">Update `HubFullAccess` with the **DefaultFullSharedAccessSignature** connection string for your hub.</span></span> <span data-ttu-id="c9caa-208">알림 허브에 대한 **설정** 블레이드에서 **액세스 정책**을 클릭하여 [Azure Portal]에서 이 연결 문자열을 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-208">This connection string can be copied from the [Azure Portal] by clicking **Access Policies** on the **Settings** blade for your notification hub.</span></span>
   
        public static String HubFullAccess = "<Enter Your DefaultFullSharedAccessSignature Connection string>";
4. <span data-ttu-id="c9caa-209">`MainActivity.java` 파일에서 `MainActivity` 클래스 위에 다음 `import` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-209">In your `MainActivity.java` file, add the following `import` statements above the `MainActivity` class.</span></span>
   
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
5. <span data-ttu-id="c9caa-210">`MainActivity.java` 파일에서 다음 멤버를 `MainActivity` 클래스 위에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-210">In your `MainActivity.java` file, add the following members at the top of the `MainActivity` class.</span></span>    
   
        private String HubEndpoint = null;
        private String HubSasKeyName = null;
        private String HubSasKeyValue = null;
6. <span data-ttu-id="c9caa-211">알림 허브로 메시지를 보낼 POST 요청을 인증하기 위해 SaS(Software Access Signature) 토큰을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-211">You must create a Software Access Signature (SaS) token to authenticate a POST request to send messages to your notification hub.</span></span> <span data-ttu-id="c9caa-212">연결 문자열에서 키 데이터를 구문 분석한 다음 [일반적인 개념](http://msdn.microsoft.com/library/azure/dn495627.aspx) REST API 참조에 설명된 대로 SaS 토큰을 만들면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-212">This is done by parsing the key data from the connection string and then creating the SaS token, as mentioned in the [Common Concepts](http://msdn.microsoft.com/library/azure/dn495627.aspx) REST API reference.</span></span> <span data-ttu-id="c9caa-213">다음 코드는 구현 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-213">The following code is an example implementation.</span></span>
   
    <span data-ttu-id="c9caa-214">`MainActivity.java`에서 `MainActivity` 클래스에 다음 메서드를 추가하여 연결 문자열의 구문을 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-214">In `MainActivity.java`, add the following method to the `MainActivity` class to parse your connection string.</span></span>
   
        /**
         * Example code from http://msdn.microsoft.com/library/azure/dn495627.aspx
         * to parse the connection string so a SaS authentication token can be
         * constructed.
         *
         * @param connectionString This must be the DefaultFullSharedAccess connection
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
7. <span data-ttu-id="c9caa-215">`MainActivity.java`에서 `MainActivity` 클래스에 다음 메서드를 추가하여 SaS 인증 토큰을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-215">In `MainActivity.java`, add the following method to the `MainActivity` class to create a SaS authentication token.</span></span>
   
        /**
         * Example code from http://msdn.microsoft.com/library/azure/dn495627.aspx to
         * construct a SaS token from the access key to authenticate a request.
         *
         * @param uri The unencoded resource URI string for this operation. The resource
         *            URI is the full URI of the Service Bus resource to which access is
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
   
                // Get an hmac_sha1 key from the raw key bytes
                byte[] keyBytes = HubSasKeyValue.getBytes("UTF-8");
                SecretKeySpec signingKey = new SecretKeySpec(keyBytes, "HmacSHA256");
   
                // Get an hmac_sha1 Mac instance and initialize with the signing key
                Mac mac = Mac.getInstance("HmacSHA256");
                mac.init(signingKey);
   
                // Compute the hmac on input data bytes
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
8. <span data-ttu-id="c9caa-216">`MainActivity.java`에서 `MainActivity` 클래스에 다음 메서드를 추가하여 **알림 보내기** 단추 클릭을 처리하고 내장된 REST API를 사용하여 허브에 푸시 알림 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-216">In `MainActivity.java`, add the following method to the `MainActivity` class to handle the **Send Notification** button click and send the push notification message to the hub by using the built-in REST API.</span></span>
   
        /**
         * Send Notification button click handler. This method parses the
         * DefaultFullSharedAccess connection string and generates a SaS token. The
         * token is added to the Authorization header on the POST request to the
         * notification hub. The text in the editTextNotificationMessage control
         * is added as the JSON body for the request to add a GCM message to the hub.
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
   
                            // Authenticate the POST request with the SaS token
                            urlConnection.setRequestProperty("Authorization", 
                                generateSasToken(url.toString()));
   
                            // Notification format should be GCM
                            urlConnection.setRequestProperty("ServiceBusNotification-Format", "gcm");
   
                            // Include any tags
                            // Example below targets 3 specific tags
                            // Refer to : https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
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

## <a name="testing-your-app"></a><span data-ttu-id="c9caa-217">앱 테스트</span><span class="sxs-lookup"><span data-stu-id="c9caa-217">Testing your app</span></span>
#### <a name="push-notifications-in-the-emulator"></a><span data-ttu-id="c9caa-218">에뮬레이터의 푸시 알림</span><span class="sxs-lookup"><span data-stu-id="c9caa-218">Push notifications in the emulator</span></span>
<span data-ttu-id="c9caa-219">에뮬레이터 내부에서 푸시 알림을 테스트하려는 경우 에뮬레이터 이미지가 앱에 대해 선택한 Google API 수준을 지원하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-219">If you want to test push notifications inside an emulator, make sure that your emulator image supports the Google API level that you chose for your app.</span></span> <span data-ttu-id="c9caa-220">이미지가 네이티브 Google API를 지원하지 않으면 **SERVICE\_NOT\_AVAILABLE** 예외가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-220">If your image doesn't support native Google APIs, you will end up with the **SERVICE\_NOT\_AVAILABLE** exception.</span></span>

<span data-ttu-id="c9caa-221">또한 **설정** > **계정**를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c9caa-221">In addition to the above, ensure that you have added your Google account to your running emulator under **Settings** > **Accounts**.</span></span> <span data-ttu-id="c9caa-222">그렇지 않으면 GCM 등록 시 **AUTHENTICATION\_FAILED** 예외가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-222">Otherwise, your attempts to register with GCM may result in the **AUTHENTICATION\_FAILED** exception.</span></span>

#### <a name="running-the-application"></a><span data-ttu-id="c9caa-223">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="c9caa-223">Running the application</span></span>
1. <span data-ttu-id="c9caa-224">앱을 실행하고 등록에 성공한 경우 등록 ID가 보고되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-224">Run the app and notice that the registration ID is reported for a successful registration.</span></span>
   
       ![Testing on Android - Channel registration](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-registered.png)
2. <span data-ttu-id="c9caa-225">허브에 등록된 모든 Android 장치로 보낼 알림 메시지를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-225">Enter a notification message to be sent to all Android devices that have registered with the hub.</span></span>
   
       ![Testing on Android - sending a message](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-set-message.png)
3. <span data-ttu-id="c9caa-226">**알림 보내기**를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-226">Press **Send Notification**.</span></span> <span data-ttu-id="c9caa-227">앱을 실행 중인 장치에 푸시 알림 메시지가 포함된 `AlertDialog` 인스턴스가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-227">Any devices that have the app running will show an `AlertDialog` instance with the push notification message.</span></span> <span data-ttu-id="c9caa-228">앱이 실행되고 있지는 않지만 이전에 푸시 알림을 등록한 장치는 Android 알림 관리자에서 알림을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-228">Devices that don't have the app running but were previously registered for push notifications will receive a notification in the Android Notification Manager.</span></span> <span data-ttu-id="c9caa-229">왼쪽 위 모서리에서 아래로 살짝 밀어 알림을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-229">Those can be viewed by swiping down from the upper-left corner.</span></span>
   
       ![Testing on Android - notifications](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-received-message.png)

## <a name="next-steps"></a><span data-ttu-id="c9caa-230">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c9caa-230">Next steps</span></span>
<span data-ttu-id="c9caa-231">다음 단계로 [알림 허브를 사용하여 사용자에게 알림 푸시] 자습서를 수행하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-231">We recommend the [Use Notification Hubs to push notifications to users] tutorial as the next step.</span></span> <span data-ttu-id="c9caa-232">특정 사용자를 대상으로 하는 태그를 사용하여 ASP.NET 백엔드에서 알림을 보내는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c9caa-232">It will show you how to send notifications from an ASP.NET backend using tags to target specific users.</span></span>

<span data-ttu-id="c9caa-233">사용자를 관심 그룹별로 분할하려면 [알림 허브를 사용하여 뉴스 속보 보내기] 자습서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c9caa-233">If you want to segment your users by interest groups, check out the [Use Notification Hubs to send breaking news] tutorial.</span></span>

<span data-ttu-id="c9caa-234">알림 허브에 대한 일반적인 정보를 알아보려면 [알림 허브 지침]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c9caa-234">To learn more general information about Notification Hubs, see our [Notification Hubs Guidance].</span></span>

<!-- Images. -->



<!-- URLs. -->
[Get started with push notifications in Mobile Services]: ../mobile-services-javascript-backend-android-get-started-push.md  
[Mobile Services Android SDK]: https://go.microsoft.com/fwLink/?LinkID=280126&clcid=0x409
[Referencing a library project]: http://go.microsoft.com/fwlink/?LinkId=389800
[Azure Classic Portal]: https://manage.windowsazure.com/
<span data-ttu-id="c9caa-235">[알림 허브 지침]: notification-hubs-push-notification-overview.md</span><span class="sxs-lookup"><span data-stu-id="c9caa-235">[Notification Hubs Guidance]: notification-hubs-push-notification-overview.md</span></span>
<span data-ttu-id="c9caa-236">[알림 허브를 사용하여 사용자에게 알림 푸시]: notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md</span><span class="sxs-lookup"><span data-stu-id="c9caa-236">[Use Notification Hubs to push notifications to users]: notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md</span></span>
<span data-ttu-id="c9caa-237">[알림 허브를 사용하여 뉴스 속보 보내기]: notification-hubs-aspnet-backend-android-xplat-segmented-gcm-push-notification.md</span><span class="sxs-lookup"><span data-stu-id="c9caa-237">[Use Notification Hubs to send breaking news]: notification-hubs-aspnet-backend-android-xplat-segmented-gcm-push-notification.md</span></span>
<span data-ttu-id="c9caa-238">[Azure Portal]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="c9caa-238">[Azure Portal]: https://portal.azure.com</span></span>

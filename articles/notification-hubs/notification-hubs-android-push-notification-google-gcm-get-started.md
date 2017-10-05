---
title: "Azure 알림 허브를 사용하여 Android에 푸시 알림 보내기 | Microsoft Docs"
description: "이 자습서에서 Azure 알림 허브를 사용하여 Android 장치로 푸시 알림을 보내는 방법을 알아봅니다."
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
ms.openlocfilehash: 808fc10ef1ebb3288facbdf2e9e817b27d4fc6bc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="sending-push-notifications-to-android-with-azure-notification-hubs"></a><span data-ttu-id="8d0db-104">Azure 알림 허브를 사용하여 Android에 푸시 알림 보내기</span><span class="sxs-lookup"><span data-stu-id="8d0db-104">Sending push notifications to Android with Azure Notification Hubs</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="8d0db-105">개요</span><span class="sxs-lookup"><span data-stu-id="8d0db-105">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="8d0db-106">이 항목에서는 GCM(Google Cloud Messaging)을 사용한 푸시 알림을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-106">This topic demonstrates push notifications with Google Cloud Messaging (GCM).</span></span> <span data-ttu-id="8d0db-107">Google의 FCM(Firebase Cloud Messaging)을 사용하는 경우 [Azure 알림 허브 및 FCM을 사용하여 Android에 푸시 알림 보내기](notification-hubs-android-push-notification-google-fcm-get-started.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8d0db-107">If you are using Google's Firebase Cloud Messaging (FCM), see [Sending push notifications to Android with Azure Notification Hubs and FCM](notification-hubs-android-push-notification-google-fcm-get-started.md).</span></span>
> 
> 

<span data-ttu-id="8d0db-108">이 자습서에서는 Azure 알림 허브를 사용하여 Android 응용 프로그램에 푸시 알림을 보내는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-108">This tutorial shows you how to use Azure Notification Hubs to send push notifications to an Android application.</span></span>
<span data-ttu-id="8d0db-109">GCM(Google Cloud Messaging)을 사용하여 푸시 알림을 받는 빈 Android 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-109">You'll create a blank Android app that receives push notifications by using Google Cloud Messaging (GCM).</span></span>

[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="8d0db-110">이 자습서에 대해 완료된 코드는 GitHub의 [여기](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStarted)서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-110">The completed code for this tutorial can be downloaded from GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStarted).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8d0db-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="8d0db-111">Prerequisites</span></span>
> [!IMPORTANT]
> <span data-ttu-id="8d0db-112">이 자습서를 완료하려면 활성 Azure 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-112">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="8d0db-113">계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-113">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="8d0db-114">자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-android-get-started)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8d0db-114">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-android-get-started).</span></span>
> 
> 

<span data-ttu-id="8d0db-115">이 자습서에서는 위에서 언급한 활성 Azure 계정 이외에 [Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797)최신 버전만 있으면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-115">In addition to an active Azure account mentioned above, this tutorial only requires the latest version of [Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797).</span></span>

<span data-ttu-id="8d0db-116">이 자습서를 완료해야 다른 모든 Android 앱용 알림 허브 자습서를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-116">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Android apps.</span></span>

## <a name="creating-a-project-that-supports-google-cloud-messaging"></a><span data-ttu-id="8d0db-117">Google Cloud Messaging을 지원하는 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="8d0db-117">Creating a project that supports Google Cloud Messaging</span></span>
[!INCLUDE [mobile-services-enable-Google-cloud-messaging](../../includes/mobile-services-enable-google-cloud-messaging.md)]

## <a name="configure-a-new-notification-hub"></a><span data-ttu-id="8d0db-118">새 알림 허브 구성</span><span class="sxs-lookup"><span data-stu-id="8d0db-118">Configure a new notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<span data-ttu-id="8d0db-119">&emsp;&emsp;6.</span><span class="sxs-lookup"><span data-stu-id="8d0db-119">&emsp;&emsp;6.</span></span>   <span data-ttu-id="8d0db-120">**설정** 블레이드에서 **알림 서비스**를 선택한 다음 **Google(GCM)**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-120">In the **Settings** blade, select **Notification Services** and then **Google (GCM)**.</span></span> <span data-ttu-id="8d0db-121">API 키를 입력하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-121">Enter the API key and click **Save**.</span></span>

&emsp;&emsp;![Azure 알림 허브 - Google(GCM)](./media/notification-hubs-android-get-started/notification-hubs-gcm-api.png)

<span data-ttu-id="8d0db-123">이제 알림 허브가 GCM과 작동하도록 구성되었으며, 푸시 알림을 받고 보내도록 앱을 등록하기 위한 연결 문자열이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-123">Your notification hub is now configured to work with GCM, and you have the connection strings to both register your app to receive and send push notifications.</span></span>

## <span data-ttu-id="8d0db-124"><a id="connecting-app"></a>알림 허브에 앱 연결</span><span class="sxs-lookup"><span data-stu-id="8d0db-124"><a id="connecting-app"></a>Connect your app to the notification hub</span></span>
### <a name="create-a-new-android-project"></a><span data-ttu-id="8d0db-125">새 Android 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="8d0db-125">Create a new Android project</span></span>
1. <span data-ttu-id="8d0db-126">Android Studio에서 새 Android Studio 프로젝트를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-126">In Android Studio, start a new Android Studio project.</span></span>
   
   ![Android Studio - 새 프로젝트][13]
2. <span data-ttu-id="8d0db-128">**휴대폰 및 태블릿** 폼 팩터와 지원할 **최소 SDK**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-128">Choose the **Phone and Tablet** form factor and the **Minimum SDK** that you want to support.</span></span> <span data-ttu-id="8d0db-129">그런 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-129">Then click **Next**.</span></span>
   
   ![Android Studio - 프로젝트 만들기 워크플로][14]
3. <span data-ttu-id="8d0db-131">**빈 활동**을 기본 활동으로 선택하고 **다음**, **마침**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-131">Choose **Empty Activity** for the main activity, click **Next**, and then click **Finish**.</span></span>

### <a name="add-google-play-services-to-the-project"></a><span data-ttu-id="8d0db-132">프로젝트에 Google Play Services 추가</span><span class="sxs-lookup"><span data-stu-id="8d0db-132">Add Google Play services to the project</span></span>
[!INCLUDE [Add Play Services](../../includes/notification-hubs-android-studio-add-google-play-services.md)]

### <a name="adding-azure-notification-hubs-libraries"></a><span data-ttu-id="8d0db-133">Azure 알림 허브 라이브러리 추가</span><span class="sxs-lookup"><span data-stu-id="8d0db-133">Adding Azure Notification Hubs libraries</span></span>
1. <span data-ttu-id="8d0db-134">**앱**의 `Build.Gradle` 파일에서 **종속성** 섹션에 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-134">In the `Build.Gradle` file for the **app**, add the following lines in the **dependencies** section.</span></span>
   
        compile 'com.microsoft.azure:notification-hubs-android-sdk:0.4@aar'
        compile 'com.microsoft.azure:azure-notifications-handler:1.0.1@aar'
2. <span data-ttu-id="8d0db-135">**종속성** 섹션 뒤에 다음 리포지토리를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-135">Add the following repository after the **dependencies** section.</span></span>
   
        repositories {
            maven {
                url "http://dl.bintray.com/microsoftazuremobile/SDK"
            }
        }

### <a name="updating-the-androidmanifestxml"></a><span data-ttu-id="8d0db-136">AndroidManifest.xml을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-136">Updating the AndroidManifest.xml.</span></span>
1. <span data-ttu-id="8d0db-137">GCM을 지원하기 위해, 코드에 [Google 인스턴스 ID API](https://developers.google.com/instance-id/)를 사용하여 [등록 토큰 가져오기](https://developers.google.com/cloud-messaging/android/client#sample-register)에 사용되는 인스턴스 ID 수신기 서비스를 구현해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-137">To support GCM, we must implement a Instance ID listener service in our code which is used to [obtain registration tokens](https://developers.google.com/cloud-messaging/android/client#sample-register) using [Google's Instance ID API](https://developers.google.com/instance-id/).</span></span> <span data-ttu-id="8d0db-138">이 자습서에서는 클래스의 이름을 `MyInstanceIDService`라고 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-138">In this tutorial we will name the class `MyInstanceIDService`.</span></span> 
   
    <span data-ttu-id="8d0db-139">AndroidManifest.xml 파일의 `<application>` 태그 내부에 다음 서비스 정의를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-139">Add the following service definition to the AndroidManifest.xml file, inside the `<application>` tag.</span></span> <span data-ttu-id="8d0db-140">`<your package>` 자리 표시자를 `AndroidManifest.xml` 파일의 맨 위에 표시된 실제 패키지 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-140">Replace the `<your package>` placeholder with the your actual package name shown at the top of the `AndroidManifest.xml` file.</span></span>
   
        <service android:name="<your package>.MyInstanceIDService" android:exported="false">
            <intent-filter>
                <action android:name="com.google.android.gms.iid.InstanceID"/>
            </intent-filter>
        </service>
2. <span data-ttu-id="8d0db-141">인스턴스 ID API에서 GCM 등록 토큰을 수신하면 해당 토큰을 사용하여 [Azure 알림 허브에 등록](notification-hubs-push-notification-registration-management.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-141">Once we have received our GCM registration token from the Instance ID API, we will use it to [register with the Azure Notification Hub](notification-hubs-push-notification-registration-management.md).</span></span> <span data-ttu-id="8d0db-142">이 등록은 `RegistrationIntentService`라는 `IntentService`를 사용하여 백그라운드에서 지원될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-142">We will support this registration in the background using an `IntentService` named `RegistrationIntentService`.</span></span> <span data-ttu-id="8d0db-143">이 서비스는 [GCM 등록 토큰 새로 고침](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens)에 대한 책임도 맡습니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-143">This service will also be responsible for [refreshing our GCM registration token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens).</span></span>
   
    <span data-ttu-id="8d0db-144">AndroidManifest.xml 파일의 `<application>` 태그 내부에 다음 서비스 정의를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-144">Add the following service definition to the AndroidManifest.xml file, inside the `<application>` tag.</span></span> <span data-ttu-id="8d0db-145">`<your package>` 자리 표시자를 `AndroidManifest.xml` 파일의 맨 위에 표시된 실제 패키지 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-145">Replace the `<your package>` placeholder with the your actual package name shown at the top of the `AndroidManifest.xml` file.</span></span> 
   
        <service
            android:name="<your package>.RegistrationIntentService"
            android:exported="false">
        </service>
3. <span data-ttu-id="8d0db-146">또한 알림을 수신하도록 수신기를 정의할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-146">We will also define a receiver to receive notifications.</span></span> <span data-ttu-id="8d0db-147">다음 수신기 정의를 `<application>` 태그 안의 AndroidManifest.xml 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-147">Add the following receiver definition to the AndroidManifest.xml file, inside the `<application>` tag.</span></span> <span data-ttu-id="8d0db-148">`<your package>` 자리 표시자를 `AndroidManifest.xml` 파일의 맨 위에 표시된 실제 패키지 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-148">Replace the `<your package>` placeholder with the your actual package name shown at the top of the `AndroidManifest.xml` file.</span></span>
   
        <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
            android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<your package name>" />
            </intent-filter>
        </receiver>
4. <span data-ttu-id="8d0db-149">`</application>` 태그 아래에 다음 필수 GCM 관련 권한을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-149">Add the following necessary GCM related permissions below the  `</application>` tag.</span></span> <span data-ttu-id="8d0db-150">반드시 `<your package>`을(를) `AndroidManifest.xml` 파일 맨 위에 있는 패키지 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-150">Make sure to replace `<your package>` with the package name shown at the top of the `AndroidManifest.xml` file.</span></span>
   
    <span data-ttu-id="8d0db-151">이러한 권한에 대한 자세한 내용은 [Android용 GCM 클라이언트 앱 설치](https://developers.google.com/cloud-messaging/android/client#manifest)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8d0db-151">For more information on these permissions, see [Setup a GCM Client app for Android](https://developers.google.com/cloud-messaging/android/client#manifest).</span></span>
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.GET_ACCOUNTS"/>
        <uses-permission android:name="android.permission.WAKE_LOCK"/>
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
   
        <permission android:name="<your package>.permission.C2D_MESSAGE" android:protectionLevel="signature" />
        <uses-permission android:name="<your package>.permission.C2D_MESSAGE"/>

### <a name="adding-code"></a><span data-ttu-id="8d0db-152">코드 추가</span><span class="sxs-lookup"><span data-stu-id="8d0db-152">Adding code</span></span>
1. <span data-ttu-id="8d0db-153">프로젝트 뷰에서 **앱** > **src** > **기본** > **java**를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-153">In the Project View, expand **app** > **src** > **main** > **java**.</span></span> <span data-ttu-id="8d0db-154">**java** 아래의 패키지 폴더를 마우스 오른쪽 단추로 클릭하고 **새로 만들기**, **Java 클래스**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-154">Right-click your package folder under **java**, click **New**, and then click **Java Class**.</span></span> <span data-ttu-id="8d0db-155">`NotificationSettings`(이)라는 새 클래스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-155">Add a new class named `NotificationSettings`.</span></span> 
   
    ![Android Studio - 새 Java 프로젝트][6]
   
    <span data-ttu-id="8d0db-157">`NotificationSettings` 클래스에 대한 다음 코드에서 아래 세 개의 자리 표시자를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-157">Make sure to update the these three placeholders in the following code for the `NotificationSettings` class:</span></span>
   
   * <span data-ttu-id="8d0db-158">**SenderId**: 이전에 [Google 클라우드 콘솔](http://cloud.google.com/console)에서 얻은 프로젝트 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-158">**SenderId**: The project number you obtained earlier in the [Google Cloud Console](http://cloud.google.com/console).</span></span>
   * <span data-ttu-id="8d0db-159">**HubListenConnectionString**: 허브의 **DefaultListenAccessSignature** 연결 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-159">**HubListenConnectionString**: The **DefaultListenAccessSignature** connection string for your hub.</span></span> <span data-ttu-id="8d0db-160">[Azure Portal]에 있는 허브의 **설정** 블레이드에서 **액세스 정책**을 클릭하여 이 연결 문자열을 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-160">You can copy that connection string by clicking **Access Policies** on the **Settings** blade of your hub on the [Azure Portal].</span></span>
   * <span data-ttu-id="8d0db-161">**HubName**: [Azure Portal]의 허브 블레이드에 표시되는 알림 허브 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-161">**HubName**: Use the name of your notification hub that appears in the hub blade in the [Azure Portal].</span></span>
     
     <span data-ttu-id="8d0db-162">`NotificationSettings` 코드:</span><span class="sxs-lookup"><span data-stu-id="8d0db-162">`NotificationSettings` code:</span></span>
     
       <span data-ttu-id="8d0db-163">공용 클래스 NotificationSettings {</span><span class="sxs-lookup"><span data-stu-id="8d0db-163">public class NotificationSettings {</span></span>
     
           public static String SenderId = "<Your project number>";
           public static String HubName = "<Your HubName>";
           public static String HubListenConnectionString = "<Your default listen connection string>";
       <span data-ttu-id="8d0db-164">}</span><span class="sxs-lookup"><span data-stu-id="8d0db-164">}</span></span>
2. <span data-ttu-id="8d0db-165">위의 단계에 따라 `MyInstanceIDService`라는 또 다른 새 클래스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-165">Using the steps above, add another new class named `MyInstanceIDService`.</span></span> <span data-ttu-id="8d0db-166">이것으로 인스턴스 ID 수신기 서비스가 구현될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-166">This will be our Instance ID listener service implementation.</span></span>
   
    <span data-ttu-id="8d0db-167">이 클래스의 코드는 `IntentService` 를 호출하여 백그라운드에서 [GCM 토큰을 새로 고칩니다](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) .</span><span class="sxs-lookup"><span data-stu-id="8d0db-167">The code for this class will call our `IntentService` to [refresh the GCM token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) in the background.</span></span>
   
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


1. <span data-ttu-id="8d0db-168">`RegistrationIntentService`라는 프로젝트에 또 다른 새 클래스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-168">Add another new class to your project named, `RegistrationIntentService`.</span></span> <span data-ttu-id="8d0db-169">그러면 [GCM 토큰 새로 고침](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) 및 [알림 허브 등록](notification-hubs-push-notification-registration-management.md)을 처리하는 `IntentService`에 대한 솔루션이 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-169">This will be the implementation for our `IntentService` that will handle [refreshing the GCM token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) and [registering with the notification hub](notification-hubs-push-notification-registration-management.md).</span></span>
   
    <span data-ttu-id="8d0db-170">이 클래스에 대해 다음 코드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-170">Use the following code for this class.</span></span>
   
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
   
                    // Storing the registration id that indicates whether the generated token has been
                    // sent to your server. If it is not stored, send the token to your server,
                    // otherwise your server should have already received the token.
                    if ((regID=sharedPreferences.getString("registrationID", null)) == null) {        
                        NotificationHub hub = new NotificationHub(NotificationSettings.HubName,
                                NotificationSettings.HubListenConnectionString, this);
                        Log.i(TAG, "Attempting to register with NH using token : " + token);
   
                        regID = hub.register(token).getRegistrationId();
   
                        // If you want to use tags...
                        // Refer to : https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
                        // regID = hub.register(token, "tag1", "tag2").getRegistrationId();
   
                        resultString = "Registered Successfully - RegId : " + regID;
                        Log.i(TAG, resultString);        
                        sharedPreferences.edit().putString("registrationID", regID ).apply();
                    } else {
                        resultString = "Previously Registered Successfully - RegId : " + regID;
                    }
                } catch (Exception e) {
                    Log.e(TAG, resultString="Failed to complete token refresh", e);
                    // If an exception happens while fetching the new token or updating our registration data
                    // on a third-party server, this ensures that we'll attempt the update at a later time.
                }
   
                // Notify UI that registration has completed.
                if (MainActivity.isVisible) {
                    MainActivity.mainActivity.ToastNotify(resultString);
                }
            }
        }
2. <span data-ttu-id="8d0db-171">`MainActivity` 클래스에서 다음 `import` 문을 클래스 선언 위에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-171">In your `MainActivity` class, add the following `import` statements above the class declaration.</span></span>
   
        import com.google.android.gms.common.ConnectionResult;
        import com.google.android.gms.common.GoogleApiAvailability;
        import com.google.android.gms.gcm.*;
        import com.microsoft.windowsazure.notifications.NotificationsManager;
        import android.util.Log;
        import android.widget.TextView;
        import android.widget.Toast;
3. <span data-ttu-id="8d0db-172">클래스의 맨 위에 다음과 같은 private 멤버를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-172">Add the following private members at the top of the class.</span></span> <span data-ttu-id="8d0db-173">[Google 권장 사항에 따라 Google Play Services의 가용성을 확인](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk)합니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-173">We will use these [check the availability of Google Play Services as recommended by Google](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk).</span></span>
   
        public static MainActivity mainActivity;
        public static Boolean isVisible = false;    
        private GoogleCloudMessaging gcm;
        private static final int PLAY_SERVICES_RESOLUTION_REQUEST = 9000;
4. <span data-ttu-id="8d0db-174">`MainActivity` 클래스에서 Google Play Services 가용성에 다음 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-174">In your `MainActivity` class, add the following method to the availability of Google Play Services.</span></span> 
   
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
5. <span data-ttu-id="8d0db-175">`MainActivity` 클래스에서 Google Play Services를 검사한 후 `IntentService`를 호출하는 다음 코드를 추가하여 GCM 등록 토큰을 가져와 알림 허브에 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-175">In your `MainActivity` class, add the following code that will check for Google Play Services before calling your `IntentService` to get your GCM registration token and register with your notification hub.</span></span>
   
        public void registerWithNotificationHubs()
        {
            Log.i(TAG, " Registering with Notification Hubs");
   
            if (checkPlayServices()) {
                // Start IntentService to register this application with GCM.
                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        }
6. <span data-ttu-id="8d0db-176">`MainActivity` 클래스의 `OnCreate` 메서드에서 활동이 생성되면 등록 프로세스를 시작하는 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-176">In the `OnCreate` method of the `MainActivity` class, add the following code to start the registration process when activity is created.</span></span>
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            mainActivity = this;
            NotificationsManager.handleNotifications(this, NotificationSettings.SenderId, MyHandler.class);
            registerWithNotificationHubs();
        }
7. <span data-ttu-id="8d0db-177">`MainActivity` 에 이러한 추가 메서드를 추가하여 앱 상태를 확인하고 앱에서 상태를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-177">Add these additional methods to the `MainActivity` to verify app state and report status in your app.</span></span>
   
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
8. <span data-ttu-id="8d0db-178">`ToastNotify` 메서드는 *"Hello World"* `TextView` 컨트롤을 사용하여 앱에서 영구적으로 상태 및 알림을 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-178">The `ToastNotify` method uses the *"Hello World"* `TextView` control to report status and notifications persistently in the app.</span></span> <span data-ttu-id="8d0db-179">activity_main.xml 레이아웃에서 해당 컨트롤에 대한 다음 ID를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-179">In your activity_main.xml layout, add the following id for that control.</span></span>
   
       android:id="@+id/text_hello"
9. <span data-ttu-id="8d0db-180">다음으로 AndroidManifest.xml에서 정의한 수신기에 대한 하위 클래스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-180">Next we will add a subclass for our receiver we defined in the AndroidManifest.xml.</span></span> <span data-ttu-id="8d0db-181">`MyHandler`라는 프로젝트에 또 다른 새 클래스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-181">Add another new class to your project named `MyHandler`.</span></span>
10. <span data-ttu-id="8d0db-182">그런 다음 `MyHandler.java`의 맨 위에 다음 import 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-182">Add the following import statements at the top of `MyHandler.java`:</span></span>
    
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.os.Bundle;
        import android.support.v4.app.NotificationCompat;
        import com.microsoft.windowsazure.notifications.NotificationsHandler;
11. <span data-ttu-id="8d0db-183">`MyHandler` 클래스에 대해 다음 코드를 추가하여 `com.microsoft.windowsazure.notifications.NotificationsHandler`의 하위 클래스로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-183">Add the following code for the `MyHandler` class making it a subclass of `com.microsoft.windowsazure.notifications.NotificationsHandler`.</span></span>
    
    <span data-ttu-id="8d0db-184">이 코드는 처리기가 받은 알림을 보고할 수 있도록 `OnReceive` 메서드를 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-184">This code overrides the `OnReceive` method, so the handler will report notifications that are received.</span></span> <span data-ttu-id="8d0db-185">또한 처리기는 `sendNotification()` 메서드를 사용하여 Android 알림 관리자에 푸시 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-185">The handler also sends the push notification to the Android notification manager by using the `sendNotification()` method.</span></span> <span data-ttu-id="8d0db-186">`sendNotification()` 메서드는 앱이 실행되지 않을 때, 알림이 수신될 때 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-186">The `sendNotification()` method should be executed when the app is not running and a notification is received.</span></span>
    
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
12. <span data-ttu-id="8d0db-187">Android Studio의 메뉴 모음에서 **빌드** > **프로젝트 다시 빌드**를 클릭하여 코드에 오류가 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-187">In Android Studio on the menu bar, click **Build** > **Rebuild Project** to make sure that no errors are present in your code.</span></span>

## <a name="sending-push-notifications"></a><span data-ttu-id="8d0db-188">푸시 알림 보내기</span><span class="sxs-lookup"><span data-stu-id="8d0db-188">Sending push notifications</span></span>
<span data-ttu-id="8d0db-189">[Azure Portal]을 통해 푸시 알림을 보내서 앱에서 푸시 알림 수신을 테스트할 수 있습니다. 아래와 같이 허브 블레이드의 **문제 해결** 섹션을 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="8d0db-189">You can test receiving push notifications in your app by sending them via the [Azure Portal] - look for the **Troubleshooting** Section in the hub blade, as shown below.</span></span>

![Azure 알림 허브 - 전송 테스트](./media/notification-hubs-android-get-started/notification-hubs-test-send.png)

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="optional-send-push-notifications-directly-from-the-app"></a><span data-ttu-id="8d0db-191">(선택 사항) 앱에서 바로 푸시 알림 보내기</span><span class="sxs-lookup"><span data-stu-id="8d0db-191">(Optional) Send push notifications directly from the app</span></span>
<span data-ttu-id="8d0db-192">일반적으로, 백 엔드 서버를 사용하여 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-192">Normally, you would send notifications using a backend server.</span></span> <span data-ttu-id="8d0db-193">경우에 따라, 클라이언트 응용 프로그램에서 직접 푸시 알림을 보낼 수 있기를 원하기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-193">For some cases, you might want to be able to send push notifications directly from the client application.</span></span> <span data-ttu-id="8d0db-194">이 섹션은 [Azure 알림 허브 REST API](https://msdn.microsoft.com/library/azure/dn223264.aspx)를 사용하여 클라이언트에서 알림을 보내는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-194">This section explains how to send notifications from the client using the [Azure Notification Hub REST API](https://msdn.microsoft.com/library/azure/dn223264.aspx).</span></span>

1. <span data-ttu-id="8d0db-195">Android Studio 프로젝트 뷰에서 **앱** > **src** > **기본** > **자원** > **레이아웃**을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-195">In Android Studio Project View, expand **App** > **src** > **main** > **res** > **layout**.</span></span> <span data-ttu-id="8d0db-196">`activity_main.xml` 레이아웃 파일을 열고 **텍스트** 탭을 클릭하여 파일의 텍스트 내용을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-196">Open the `activity_main.xml` layout file and click the **Text** tab to update the text contents of the file.</span></span> <span data-ttu-id="8d0db-197">아래 코드로 업데이트하여 알림 허브에 푸시 알림 메시지를 보내는 새 `Button` 및 `EditText` 컨트롤을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-197">Update it with the code below, which adds new `Button` and `EditText` controls for sending push notification messages to the notification hub.</span></span> <span data-ttu-id="8d0db-198">이 코드를 맨 아래의 `</RelativeLayout>`바로 앞에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-198">Add this code at the bottom, just before `</RelativeLayout>`.</span></span>
   
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
2. <span data-ttu-id="8d0db-199">Android Studio 프로젝트 뷰에서 **앱** > **src** > **기본** > **자원** > **값**을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-199">In Android Studio Project View, expand **App** > **src** > **main** > **res** > **values**.</span></span> <span data-ttu-id="8d0db-200">`strings.xml` 파일을 열고 새 `Button` 및 `EditText` 컨트롤에서 참조하는 문자열 값을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-200">Open the `strings.xml` file and add the string values that are referenced by the new `Button` and `EditText` controls.</span></span> <span data-ttu-id="8d0db-201">파일 맨 아래의 `</resources>`바로 앞에 이를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-201">Add these at the bottom of the file, just before `</resources>`.</span></span>
   
        <string name="send_button">Send Notification</string>
        <string name="notification_message_hint">Enter notification message text</string>
3. <span data-ttu-id="8d0db-202">`NotificationSetting.java` 파일에서 `NotificationSettings` 클래스에 다음 설정을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-202">In your `NotificationSetting.java` file, add the following setting to the `NotificationSettings` class.</span></span>
   
    <span data-ttu-id="8d0db-203">허브에 **DefaultFullSharedAccessSignature** 연결 문자열을 사용하여 `HubFullAccess`을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-203">Update `HubFullAccess` with the **DefaultFullSharedAccessSignature** connection string for your hub.</span></span> <span data-ttu-id="8d0db-204">알림 허브에 대한 **설정** 블레이드에서 **액세스 정책**을 클릭하여 [Azure Portal]에서 이 연결 문자열을 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-204">This connection string can be copied from the [Azure Portal] by clicking **Access Policies** on the **Settings** blade for your notification hub.</span></span>
   
        public static String HubFullAccess = "<Enter Your DefaultFullSharedAccess Connection string>";
4. <span data-ttu-id="8d0db-205">`MainActivity.java` 파일에서 `MainActivity` 클래스 위에 다음 `import` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-205">In your `MainActivity.java` file, add the following `import` statements above the `MainActivity` class.</span></span>
   
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
5. <span data-ttu-id="8d0db-206">`MainActivity.java` 파일에서 다음 멤버를 `MainActivity` 클래스 위에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-206">In your `MainActivity.java` file, add the following members at the top of the `MainActivity` class.</span></span>    
   
        private String HubEndpoint = null;
        private String HubSasKeyName = null;
        private String HubSasKeyValue = null;
6. <span data-ttu-id="8d0db-207">알림 허브로 메시지를 보낼 POST 요청을 인증하기 위해 SaS(Software Access Signature) 토큰을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-207">You must create a Software Access Signature (SaS) token to authenticate a POST request to send messages to your notification hub.</span></span> <span data-ttu-id="8d0db-208">연결 문자열에서 키 데이터를 구문 분석한 다음 [일반적인 개념](http://msdn.microsoft.com/library/azure/dn495627.aspx) REST API 참조에 설명된 대로 SaS 토큰을 만들면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-208">This is done by parsing the key data from the connection string and then creating the SaS token, as mentioned in the [Common Concepts](http://msdn.microsoft.com/library/azure/dn495627.aspx) REST API reference.</span></span> <span data-ttu-id="8d0db-209">다음 코드는 구현 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-209">The following code is an example implementation.</span></span>
   
    <span data-ttu-id="8d0db-210">`MainActivity.java`에서 `MainActivity` 클래스에 다음 메서드를 추가하여 연결 문자열의 구문을 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-210">In `MainActivity.java`, add the following method to the `MainActivity` class to parse your connection string.</span></span>
   
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
7. <span data-ttu-id="8d0db-211">`MainActivity.java`에서 `MainActivity` 클래스에 다음 메서드를 추가하여 SaS 인증 토큰을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-211">In `MainActivity.java`, add the following method to the `MainActivity` class to create a SaS authentication token.</span></span>
   
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
8. <span data-ttu-id="8d0db-212">`MainActivity.java`에서 `MainActivity` 클래스에 다음 메서드를 추가하여 **알림 보내기** 단추 클릭을 처리하고 내장된 REST API를 사용하여 허브에 푸시 알림 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-212">In `MainActivity.java`, add the following method to the `MainActivity` class to handle the **Send Notification** button click and send the push notification message to the hub by using the built-in REST API.</span></span>
   
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

## <a name="testing-your-app"></a><span data-ttu-id="8d0db-213">앱 테스트</span><span class="sxs-lookup"><span data-stu-id="8d0db-213">Testing your app</span></span>
#### <a name="push-notifications-in-the-emulator"></a><span data-ttu-id="8d0db-214">에뮬레이터의 푸시 알림</span><span class="sxs-lookup"><span data-stu-id="8d0db-214">Push notifications in the emulator</span></span>
<span data-ttu-id="8d0db-215">에뮬레이터 내부에서 푸시 알림을 테스트하려는 경우 에뮬레이터 이미지가 앱에 대해 선택한 Google API 수준을 지원하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-215">If you want to test push notifications inside an emulator, make sure that your emulator image supports the Google API level that you chose for your app.</span></span> <span data-ttu-id="8d0db-216">이미지가 네이티브 Google API를 지원하지 않으면 **SERVICE\_NOT\_AVAILABLE** 예외가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-216">If your image doesn't support native Google APIs, you will end up with the **SERVICE\_NOT\_AVAILABLE** exception.</span></span>

<span data-ttu-id="8d0db-217">또한 **설정** > **계정**를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8d0db-217">In addition to the above, ensure that you have added your Google account to your running emulator under **Settings** > **Accounts**.</span></span> <span data-ttu-id="8d0db-218">그렇지 않으면 GCM 등록 시 **AUTHENTICATION\_FAILED** 예외가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-218">Otherwise, your attempts to register with GCM may result in the **AUTHENTICATION\_FAILED** exception.</span></span>

#### <a name="running-the-application"></a><span data-ttu-id="8d0db-219">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="8d0db-219">Running the application</span></span>
1. <span data-ttu-id="8d0db-220">앱을 실행하고 등록에 성공한 경우 등록 ID가 보고되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-220">Run the app and notice that the registration ID is reported for a successful registration.</span></span>
   
      ![Android에서 테스트 - 채널 등록][18]
2. <span data-ttu-id="8d0db-222">허브에 등록된 모든 Android 장치로 보낼 알림 메시지를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-222">Enter a notification message to be sent to all Android devices that have registered with the hub.</span></span>
   
      ![Android에서 테스트 - 메시지 보내기][19]

3. <span data-ttu-id="8d0db-224">**알림 보내기**를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-224">Press **Send Notification**.</span></span> <span data-ttu-id="8d0db-225">앱을 실행 중인 장치에 푸시 알림 메시지가 포함된 `AlertDialog` 인스턴스가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-225">Any devices that have the app running will show an `AlertDialog` instance with the push notification message.</span></span> <span data-ttu-id="8d0db-226">앱이 실행되고 있지는 않지만 이전에 푸시 알림을 등록한 장치는 Android 알림 관리자에서 알림을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-226">Devices that don't have the app running but were previously registered for push notifications will receive a notification in the Android Notification Manager.</span></span> <span data-ttu-id="8d0db-227">왼쪽 위 모서리에서 아래로 살짝 밀어 알림을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-227">Those can be viewed by swiping down from the upper-left corner.</span></span>
   
      ![Android에서 테스트 - 알림][21]

## <a name="next-steps"></a><span data-ttu-id="8d0db-229">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8d0db-229">Next steps</span></span>
<span data-ttu-id="8d0db-230">다음 단계로 [알림 허브를 사용하여 사용자에게 알림 푸시] 자습서를 수행하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-230">We recommend the [Use Notification Hubs to push notifications to users] tutorial as the next step.</span></span> <span data-ttu-id="8d0db-231">특정 사용자를 대상으로 하는 태그를 사용하여 ASP.NET 백엔드에서 알림을 보내는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8d0db-231">It will show you how to send notifications from an ASP.NET backend using tags to target specific users.</span></span>

<span data-ttu-id="8d0db-232">사용자를 관심 그룹별로 분할하려면 [알림 허브를 사용하여 뉴스 속보 보내기] 자습서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8d0db-232">If you want to segment your users by interest groups, check out the [Use Notification Hubs to send breaking news] tutorial.</span></span>

<span data-ttu-id="8d0db-233">알림 허브에 대한 일반적인 정보를 알아보려면 [알림 허브 지침]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8d0db-233">To learn more general information about Notification Hubs, see our [Notification Hubs Guidance].</span></span>

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
<span data-ttu-id="8d0db-234">[알림 허브 지침]: http://msdn.microsoft.com/library/jj927170.aspx</span><span class="sxs-lookup"><span data-stu-id="8d0db-234">[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx</span></span>
<span data-ttu-id="8d0db-235">[알림 허브를 사용하여 사용자에게 알림 푸시]: notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md</span><span class="sxs-lookup"><span data-stu-id="8d0db-235">[Use Notification Hubs to push notifications to users]: notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md</span></span>
<span data-ttu-id="8d0db-236">[알림 허브를 사용하여 뉴스 속보 보내기]: notification-hubs-aspnet-backend-android-xplat-segmented-gcm-push-notification.md</span><span class="sxs-lookup"><span data-stu-id="8d0db-236">[Use Notification Hubs to send breaking news]: notification-hubs-aspnet-backend-android-xplat-segmented-gcm-push-notification.md</span></span>
<span data-ttu-id="8d0db-237">[Azure Portal]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="8d0db-237">[Azure Portal]: https://portal.azure.com</span></span>

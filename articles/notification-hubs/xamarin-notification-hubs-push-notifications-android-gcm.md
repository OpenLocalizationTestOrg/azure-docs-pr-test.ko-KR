---
title: "Xamarin.Android 앱에 대한 알림 허브 시작 | Microsoft Docs"
description: "이 자습서에서 Azure 알림 허브를 사용하여 Xamarin.Android 응용 프로그램에 푸시 알림을 보내는 방법을 알아봅니다."
author: ysxu
manager: erikre
editor: 
services: notification-hubs
documentationcenter: xamarin
ms.assetid: 0be600fe-d5f3-43a5-9e5e-3135c9743e54
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: e0ef1b006a2b202c08a71caaff4ef4d763d50d0a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-notification-hubs-with-xamarin-for-android"></a><span data-ttu-id="723f8-103">Android용 Xamarin을 통해 알림 허브 시작</span><span class="sxs-lookup"><span data-stu-id="723f8-103">Get started with Notification Hubs with Xamarin for Android</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="723f8-104">개요</span><span class="sxs-lookup"><span data-stu-id="723f8-104">Overview</span></span>
<span data-ttu-id="723f8-105">이 자습서에서는 Azure 알림 허브를 사용하여 Xamarin.Android 응용 프로그램에 푸시 알림을 보내는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-105">This tutorial shows you how to use Azure Notification Hubs to send push notifications to a Xamarin.Android application.</span></span>
<span data-ttu-id="723f8-106">GCM(Google Cloud Messaging)을 사용하여 푸시 알림을 받는 빈 Xamarin.Android 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-106">You'll create a blank Xamarin.Android app that receives push notifications by using Google Cloud Messaging (GCM).</span></span> <span data-ttu-id="723f8-107">완료하면 알림 허브를 사용하여 앱을 실행하는 모든 장치로 푸시 알림을 브로드캐스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-107">When you're finished, you'll be able to use your notification hub to broadcast push notifications to all the devices running your app.</span></span> <span data-ttu-id="723f8-108">완성된 코드는 [NotificationHubs 앱][GitHub] 샘플에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-108">The finished code is available in the [NotificationHubs app][GitHub] sample.</span></span>

<span data-ttu-id="723f8-109">이 자습서에서는 알림 허브를 사용하는 간단한 브로드캐스트 시나리오를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-109">This tutorial demonstrates the simple broadcast scenario in using Notification Hubs.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="723f8-110">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="723f8-110">Before you begin</span></span>
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="723f8-111">이 자습서에 대해 완료된 코드는 GitHub의 [여기](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/Xamarin/GetStartedXamarinAndroid)서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-111">The completed code for this tutorial can be found on GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/Xamarin/GetStartedXamarinAndroid).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="723f8-112">필수 조건</span><span class="sxs-lookup"><span data-stu-id="723f8-112">Prerequisites</span></span>
<span data-ttu-id="723f8-113">이 자습서를 사용하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-113">This tutorial requires the following:</span></span>

* <span data-ttu-id="723f8-114">Windows의 Xamarin이 포함된 Visual Studio 또는 Mac OS X의 Xamarin Studio. 전체 설치 지침은 [Visual Studio 및 Xamarin을 위한 설정 및 설치](https://msdn.microsoft.com/library/mt613162.aspx)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-114">Visual Studio with Xamarin on Windows or Xamarin Studio on Mac OS X. Complete installation instructions are on [Setup and Install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span></span>
* <span data-ttu-id="723f8-115">활성 Google 계정</span><span class="sxs-lookup"><span data-stu-id="723f8-115">Active Google account</span></span>
* <span data-ttu-id="723f8-116">[Azure 메시징 구성 요소]</span><span class="sxs-lookup"><span data-stu-id="723f8-116">[Azure Messaging Component]</span></span>
* <span data-ttu-id="723f8-117">[Google Cloud Messaging 클라이언트 구성 요소]</span><span class="sxs-lookup"><span data-stu-id="723f8-117">[Google Cloud Messaging Client Component]</span></span>

<span data-ttu-id="723f8-118">이 자습서를 완료해야 다른 모든 Xamarin.Android 앱용 알림 허브 자습서를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-118">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Xamarin.Android apps.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="723f8-119">이 자습서를 완료하려면 활성 Azure 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-119">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="723f8-120">계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-120">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="723f8-121">자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A9C9624B5&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-android-get-started%2F)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="723f8-121">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A9C9624B5&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-android-get-started%2F).</span></span>
> 
> 

## <a name="enable-google-cloud-messaging"></a><span data-ttu-id="723f8-122">Google Cloud Messaging 사용</span><span class="sxs-lookup"><span data-stu-id="723f8-122">Enable Google Cloud Messaging</span></span>
[!INCLUDE [mobile-services-enable-Google-cloud-messaging](../../includes/mobile-services-enable-google-cloud-messaging.md)]

## <a name="configure-your-notification-hub"></a><span data-ttu-id="723f8-123">알림 허브 구성</span><span class="sxs-lookup"><span data-stu-id="723f8-123">Configure your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="7">

<li><p><span data-ttu-id="723f8-124">맨 위에 있는 <b>구성</b> 탭을 클릭하고 이전 섹션에서 받은 <b>API 키</b> 값을 입력한 후 <b>저장</b>을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-124">Click the <b>Configure</b> tab at the top, enter the <b>API Key</b> value you obtained in the previous section, and then click <b>Save</b>.</span></span></p>
</li>
</ol>
<span data-ttu-id="723f8-125">&emsp;&emsp;![](./media/notification-hubs-android-get-started/notification-hub-configure-android.png)</span><span class="sxs-lookup"><span data-stu-id="723f8-125">&emsp;&emsp;![](./media/notification-hubs-android-get-started/notification-hub-configure-android.png)</span></span>

<span data-ttu-id="723f8-126">이제 알림 허브가 GCM과 작동하도록 구성되었으며 알림을 받고 푸시 알림을 보내도록 앱을 등록하기 위한 연결 문자열이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-126">Your notification hub is now configured to work with GCM, and you have the connection strings to both register your app to receive notifications and to send push notifications.</span></span>

## <a name="connect-your-app-to-the-notification-hub"></a><span data-ttu-id="723f8-127">알림 허브에 앱 연결</span><span class="sxs-lookup"><span data-stu-id="723f8-127">Connect your app to the notification hub</span></span>
### <a name="create-a-new-project"></a><span data-ttu-id="723f8-128">새 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="723f8-128">Create a new project</span></span>
1. <span data-ttu-id="723f8-129">Xamarin Studio에서 **새 솔루션**, **Android 앱**, **다음**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-129">In Xamarin Studio, click **New Solution**, click **Android App**, and click **Next**.</span></span>
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-project1.png)

2. <span data-ttu-id="723f8-130">**앱 이름**과 **식별자**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-130">Enter your **App Name** and **Identifier**.</span></span> <span data-ttu-id="723f8-131">지원하려는 **대상 플랫폼**, **다음**, **만들기**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-131">Click the **Target Plaforms** you want to support and then click **Next** and **Create**.</span></span>
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-project2.png)

    <span data-ttu-id="723f8-132">그러면 새 Android 프로젝트가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-132">This creates a new Android project.</span></span>

1. <span data-ttu-id="723f8-133">솔루션 보기에서 새 프로젝트를 마우스 오른쪽 단추로 클릭하고 **옵션**를 선택하여 프로젝트 속성을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-133">Open the project properties by right-clicking your new project in the Solution view and choosing **Options**.</span></span> <span data-ttu-id="723f8-134">**Build** 섹션에서 **Android Application** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-134">Select the **Android Application** item in the **Build** section.</span></span>
   
    <span data-ttu-id="723f8-135">**Package name** 의 첫 문자는 소문자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-135">Ensure that the first letter of your **Package name** is lowercase.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="723f8-136">패키지 이름의 첫 문자는 소문자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-136">The first letter of the package name must be lowercase.</span></span> <span data-ttu-id="723f8-137">그렇지 않으면 아래에서 푸시 알림에 대한 **BroadcastReceiver** 및 **IntentFilter**를 등록할 때 응용 프로그램 매니페스트 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-137">Otherwise, you will receive application manifest errors when you register your **BroadcastReceiver** and **IntentFilter** for push notifications below.</span></span>
   > 
   > 
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub--xamarin-android-app-options.png)
2. <span data-ttu-id="723f8-138">또는 **최소 Android 버전** 을 다른 API 수준으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-138">Optionally, set the **Minimum Android version** to another API Level.</span></span>
3. <span data-ttu-id="723f8-139">**대상 Android 버전** 을 대상으로 지정할 다른 API 버전으로 설정합니다(API 수준 8 이상이어야 함).</span><span class="sxs-lookup"><span data-stu-id="723f8-139">Optionally, set the **Target Android version** to the another API version that you want to target (must be API level 8 or higher).</span></span>

<span data-ttu-id="723f8-140">**확인** 을 클릭하고 프로젝트 옵션 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-140">Click **OK** and close the Project Options dialog.</span></span>

### <a name="add-the-required-components-to-your-project"></a><span data-ttu-id="723f8-141">프로젝트에 필요한 구성 요소 추가</span><span class="sxs-lookup"><span data-stu-id="723f8-141">Add the required components to your project</span></span>
<span data-ttu-id="723f8-142">Xamarin Component Store에서 제공되는 Google Cloud Messaging 클라이언트는 Xamarin.Android에서 푸시 알림을 지원하는 프로세스를 간소화합니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-142">The Google Cloud Messaging Client available on the Xamarin Component Store simplifies the process of supporting push notifications in Xamarin.Android.</span></span>

1. <span data-ttu-id="723f8-143">Xamarin.Android 앱에서 구성 요소 폴더를 마우스 오른쪽 단추로 클릭하고 **구성 요소 더 가져오기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-143">Right-click the Components folder in Xamarin.Android app and choose **Get More Components**.</span></span>
2. <span data-ttu-id="723f8-144">**Azure 메시징** 구성 요소를 검색하고 프로젝트에 구성 요소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-144">Search for the **Azure Messaging** component and add it to the project.</span></span>
3. <span data-ttu-id="723f8-145">**Google Cloud Messaging 클라이언트** 구성 요소를 검색하고 프로젝트에 구성 요소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-145">Search for the **Google Cloud Messaging Client** component and add it to the project.</span></span>

### <a name="set-up-notification-hubs-in-your-project"></a><span data-ttu-id="723f8-146">프로젝트에서 알림 허브 설정</span><span class="sxs-lookup"><span data-stu-id="723f8-146">Set up notification hubs in your project</span></span>
1. <span data-ttu-id="723f8-147">Android 앱 및 알림 허브에 대해 다음 정보를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-147">Gather the following information for your Android app and notification hub:</span></span>
   
   * <span data-ttu-id="723f8-148">**GoogleProjectNumber**: Google 개발자 포털의 앱 개요에서 이 프로젝트의 번호 값을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-148">**GoogleProjectNumber**:  Get this Project Number value from the overview of your app on the Google Developer Portal.</span></span> <span data-ttu-id="723f8-149">앞서 포털에서 앱을 생성할 때 이 값을 기입해 두었습니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-149">You made a note of this value earlier when you created the app on the portal.</span></span>
   * <span data-ttu-id="723f8-150">**연결 문자열 수신 대기**: [Azure 클래식 포털]의 대시보드에서 **연결 문자열 보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-150">**Listen connection string**: On the dashboard in the [Azure Classic Portal], click **View connection strings**.</span></span> <span data-ttu-id="723f8-151">이 값에 대해 *DefaultListenSharedAccessSignature* 연결 문자열을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-151">Copy the *DefaultListenSharedAccessSignature* connection string for this value.</span></span>
   * <span data-ttu-id="723f8-152">**허브 이름**: [Azure 클래식 포털]에서 허브의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-152">**Hub name**: This is the name of your hub from the [Azure Classic Portal].</span></span> <span data-ttu-id="723f8-153">예를 들어 *mynotificationhub2*입니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-153">For example, *mynotificationhub2*.</span></span>
     
     <span data-ttu-id="723f8-154">Xamarin 프로젝트에 대해 **Constants.cs** 클래스를 만들고 클래스에 다음 상수 값을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-154">Create a **Constants.cs** class for your Xamarin project and define the following constant values in the class.</span></span> <span data-ttu-id="723f8-155">자리 표시자는 해당 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-155">Replace the placeholders with your values.</span></span>
     
       <span data-ttu-id="723f8-156">public static class Constants   {</span><span class="sxs-lookup"><span data-stu-id="723f8-156">public static class Constants   {</span></span>
     
           public const string SenderID = "<GoogleProjectNumber>"; // Google API Project Number
           public const string ListenConnectionString = "<Listen connection string>";
           public const string NotificationHubName = "<hub name>";
       <span data-ttu-id="723f8-157">}</span><span class="sxs-lookup"><span data-stu-id="723f8-157">}</span></span>
2. <span data-ttu-id="723f8-158">**MainActivity.cs**에 다음 using 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-158">Add the following using statements to **MainActivity.cs**:</span></span>
   
        using Android.Util;
        using Gcm.Client;
3. <span data-ttu-id="723f8-159">앱 실행 중에 경고 대화 상자를 표시하는 데 사용할 `MainActivity` 클래스에 인스턴스 변수를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-159">Add an instance variable to the `MainActivity` class that will be used to show an alert dialog when the app is running:</span></span>
   
        public static MainActivity instance;
4. <span data-ttu-id="723f8-160">**MainActivity** 클래스에 다음 메서드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-160">Create the following method in the **MainActivity** class:</span></span>
   
        private void RegisterWithGCM()
        {
            // Check to ensure everything's set up right
            GcmClient.CheckDevice(this);
            GcmClient.CheckManifest(this);
   
            // Register for push notifications
            Log.Info("MainActivity", "Registering...");
            GcmClient.Register(this, Constants.SenderID);
        }
5. <span data-ttu-id="723f8-161">**MainActivity.cs**의 `OnCreate` 메서드에서 `instance` 변수를 초기화하고 `RegisterWithGCM`에 호출을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-161">In the `OnCreate` method of **MainActivity.cs**, initialize the `instance` variable and add a call to `RegisterWithGCM`:</span></span>
   
        protected override void OnCreate (Bundle bundle)
        {
            instance = this;
   
            base.OnCreate (bundle);
   
            // Set your view from the "main" layout resource
            SetContentView (Resource.Layout.Main);
   
            // Get your button from the layout resource,
            // and attach an event to it
            Button button = FindViewById<Button> (Resource.Id.myButton);
   
            RegisterWithGCM();
        }
6. <span data-ttu-id="723f8-162">**MyBroadcastReceiver**라는 새 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-162">Create a new class, **MyBroadcastReceiver**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="723f8-163">아래에서 **BroadcastReceiver** 클래스를 처음부터 만드는 과정을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-163">We will walk through creating a **BroadcastReceiver** class from scratch below.</span></span> <span data-ttu-id="723f8-164">그러나 수동으로 **MyBroadcastReceiver.cs**를 만드는 대신 [NotificationHubs 샘플][GitHub]에 포함된 샘플 Xamarin.Android 프로젝트에 있는 **GcmService.cs** 파일을 참조하면 더 빠르게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-164">However, a quick alternative to manually creating **MyBroadcastReceiver.cs** is to refer to the **GcmService.cs** file found in the sample Xamarin.Android project included with the [NotificationHubs samples][GitHub].</span></span> <span data-ttu-id="723f8-165">또한 **GcmService.cs** 를 복제하고 클래스 이름을 변경하면 빨리 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-165">Duplicating **GcmService.cs** and changing class names can be a great place to start as well.</span></span>
   > 
   > 
7. <span data-ttu-id="723f8-166">다음 using 문을 **MyBroadcastReceiver.cs** 에 추가합니다.(앞에서 만든 구성 요소 및 어셈블리 참조)</span><span class="sxs-lookup"><span data-stu-id="723f8-166">Add the following using statements to **MyBroadcastReceiver.cs** (referring to the component and assembly that you added earlier):</span></span>
   
        using System.Collections.Generic;
        using System.Text;
        using Android.App;
        using Android.Content;
        using Android.Util;
        using Gcm.Client;
        using WindowsAzure.Messaging;
8. <span data-ttu-id="723f8-167">**MyBroadcastReceiver.cs**에서 **using** 문과 **namespace** 선언 사이에 다음 사용 권한 요청을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-167">In **MyBroadcastReceiver.cs**, add the following permission requests between the **using** statements and the **namespace** declaration:</span></span>
   
        [assembly: Permission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "com.google.android.c2dm.permission.RECEIVE")]
   
        //GET_ACCOUNTS is needed only for Android versions 4.0.3 and below
        [assembly: UsesPermission(Name = "android.permission.GET_ACCOUNTS")]
        [assembly: UsesPermission(Name = "android.permission.INTERNET")]
        [assembly: UsesPermission(Name = "android.permission.WAKE_LOCK")]
9. <span data-ttu-id="723f8-168">**MyBroadcastReceiver.cs**에서 **MyBroadcastReceiver** 클래스를 다음과 일치하도록 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-168">In **MyBroadcastReceiver.cs**, change the **MyBroadcastReceiver** class to match the following:</span></span>
   
        [BroadcastReceiver(Permission=Gcm.Client.Constants.PERMISSION_GCM_INTENTS)]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_MESSAGE },
            Categories = new string[] { "@PACKAGE_NAME@" })]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_REGISTRATION_CALLBACK },
            Categories = new string[] { "@PACKAGE_NAME@" })]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_LIBRARY_RETRY },
            Categories = new string[] { "@PACKAGE_NAME@" })]
        public class MyBroadcastReceiver : GcmBroadcastReceiverBase<PushHandlerService>
        {
            public static string[] SENDER_IDS = new string[] { Constants.SenderID };
   
            public const string TAG = "MyBroadcastReceiver-GCM";
        }
10. <span data-ttu-id="723f8-169">**MyBroadcastReceiver.cs**에서 **GcmServiceBase**에서 파생된 **PushHandlerService** 클래스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-169">Add another class in **MyBroadcastReceiver.cs** named **PushHandlerService**, which derives from **GcmServiceBase**.</span></span> <span data-ttu-id="723f8-170">클래스에 **Service** 특성을 적용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-170">Make sure to apply the **Service** attribute to the class:</span></span>
    
         [Service] // Must use the service tag
         public class PushHandlerService : GcmServiceBase
         {
             public static string RegistrationID { get; private set; }
             private NotificationHub Hub { get; set; }
    
             public PushHandlerService() : base(Constants.SenderID)
                {
                 Log.Info(MyBroadcastReceiver.TAG, "PushHandlerService() constructor");
             }
         }
11. <span data-ttu-id="723f8-171">**GcmServiceBase**는 **OnRegistered()**, **OnUnRegistered()**, **OnMessage()**, **OnRecoverableError()** 및 **OnError()** 메서드를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-171">**GcmServiceBase** implements methods **OnRegistered()**, **OnUnRegistered()**, **OnMessage()**, **OnRecoverableError()**, and **OnError()**.</span></span> <span data-ttu-id="723f8-172">**PushHandlerService** 구현 클래스는 이러한 메서드를 재정의해야 하며, 해당 메서드는 알림 허브와 상호 작용에 대한 응답으로 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-172">Our **PushHandlerService** implementation class must override these methods, and these methods will fire in response to interacting with the notification hub.</span></span>
12. <span data-ttu-id="723f8-173">**PushHandlerService**의 **OnRegistered()** 메서드를 다음 코드로 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-173">Override the **OnRegistered()** method in **PushHandlerService** by using the following code:</span></span>
    
         protected override void OnRegistered(Context context, string registrationId)
         {
             Log.Verbose(MyBroadcastReceiver.TAG, "GCM Registered: " + registrationId);
             RegistrationID = registrationId;
    
             createNotification("PushHandlerService-GCM Registered...",
                                 "The device has been Registered!");
    
             Hub = new NotificationHub(Constants.NotificationHubName, Constants.ListenConnectionString,
                                         context);
             try
             {
                 Hub.UnregisterAll(registrationId);
             }
             catch (Exception ex)
             {
                 Log.Error(MyBroadcastReceiver.TAG, ex.Message);
             }
    
             //var tags = new List<string>() { "falcons" }; // create tags if you want
             var tags = new List<string>() {};
    
             try
             {
                 var hubRegistration = Hub.Register(registrationId, tags.ToArray());
             }
             catch (Exception ex)
             {
                 Log.Error(MyBroadcastReceiver.TAG, ex.Message);
             }
         }
    
    > [!NOTE]
    > <span data-ttu-id="723f8-174">위의 **OnRegistered()** 코드에서 태그를 지정하여 특정 메시징 채널에 등록하는 기능을 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-174">In the **OnRegistered()** code above, you should note the ability to specify tags to register for specific messaging channels.</span></span>
    > 
    > 
13. <span data-ttu-id="723f8-175">다음 코드를 사용하여 **PushHandlerService**의 **OnMessage** 메서드를 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-175">Override the **OnMessage** method in **PushHandlerService** by using the following code:</span></span>
    
        protected override void OnMessage(Context context, Intent intent)
        {
            Log.Info(MyBroadcastReceiver.TAG, "GCM Message Received!");
    
            var msg = new StringBuilder();
    
            if (intent != null && intent.Extras != null)
            {
                foreach (var key in intent.Extras.KeySet())
                    msg.AppendLine(key + "=" + intent.Extras.Get(key).ToString());
            }
    
            string messageText = intent.Extras.GetString("message");
            if (!string.IsNullOrEmpty (messageText))
            {
                createNotification ("New hub message!", messageText);
            }
            else
            {
                createNotification ("Unknown message details", msg.ToString ());
            }
        }
14. <span data-ttu-id="723f8-176">알림이 수신되면 사용자에게 알리도록 다음 **createNotification** 및 **dialogNotify** 메서드를 **PushHandlerService**에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-176">Add the following **createNotification** and **dialogNotify** methods to **PushHandlerService** for notifying users when a notification is received.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="723f8-177">Android 버전 5.0 이후의 알림 설계는 이전 버전과 상당한 차이가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-177">Notification design in Android version 5.0 and later represents a significant departure from that of previous versions.</span></span> <span data-ttu-id="723f8-178">Android 5.0에서 이를 테스트할 때는 알림 수신을 위해 앱을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-178">If you test this on Android 5.0 or later, the app will need to be running to receive the notification.</span></span> <span data-ttu-id="723f8-179">자세한 내용은 [Android 알림](http://go.microsoft.com/fwlink/?LinkId=615880)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="723f8-179">For more information, see [Android Notifications](http://go.microsoft.com/fwlink/?LinkId=615880).</span></span>
    > 
    > 
    
        void createNotification(string title, string desc)
        {
            //Create notification
            var notificationManager = GetSystemService(Context.NotificationService) as NotificationManager;
    
            //Create an intent to show UI
            var uiIntent = new Intent(this, typeof(MainActivity));
    
            //Create the notification
            var notification = new Notification(Android.Resource.Drawable.SymActionEmail, title);
    
            //Auto-cancel will remove the notification once the user touches it
            notification.Flags = NotificationFlags.AutoCancel;
    
            //Set the notification info
            //we use the pending intent, passing our ui intent over, which will get called
            //when the notification is tapped.
            notification.SetLatestEventInfo(this, title, desc, PendingIntent.GetActivity(this, 0, uiIntent, 0));
    
            //Show the notification
            notificationManager.Notify(1, notification);
            dialogNotify (title, desc);
        }
    
        protected void dialogNotify(String title, String message)
        {
    
            MainActivity.instance.RunOnUiThread(() => {
                AlertDialog.Builder dlg = new AlertDialog.Builder(MainActivity.instance);
                AlertDialog alert = dlg.Create();
                alert.SetTitle(title);
                alert.SetButton("Ok", delegate {
                    alert.Dismiss();
                });
                alert.SetMessage(message);
                alert.Show();
            });
        }
15. <span data-ttu-id="723f8-180">코드가 컴파일되도록 추상 멤버 **OnUnRegistered()**, **OnRecoverableError()** 및 **OnError()**를 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-180">Override abstract members **OnUnRegistered()**, **OnRecoverableError()**, and **OnError()** so that your code compiles:</span></span>
    
        protected override void OnUnRegistered(Context context, string registrationId)
        {
            Log.Verbose(MyBroadcastReceiver.TAG, "GCM Unregistered: " + registrationId);
    
            createNotification("GCM Unregistered...", "The device has been unregistered!");
        }
    
        protected override bool OnRecoverableError(Context context, string errorId)
        {
            Log.Warn(MyBroadcastReceiver.TAG, "Recoverable Error: " + errorId);
    
            return base.OnRecoverableError (context, errorId);
        }
    
        protected override void OnError(Context context, string errorId)
        {
            Log.Error(MyBroadcastReceiver.TAG, "GCM Error: " + errorId);
        }

## <a name="run-your-app-in-the-emulator"></a><span data-ttu-id="723f8-181">에뮬레이터에서 앱 실행</span><span class="sxs-lookup"><span data-stu-id="723f8-181">Run your app in the emulator</span></span>
<span data-ttu-id="723f8-182">에뮬레이터에서 이 앱을 실행하는 경우 Google API를 지원하는 AVD(Android Virtual Device)를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-182">If you run this app in the emulator, make sure that you use an Android Virtual Device (AVD) that supports Google APIs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="723f8-183">푸시 알림을 받으려면 Android 가상 장치에서 Google 계정을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-183">In order to receive push notifications, you must set up a Google account on your Android Virtual Device.</span></span> <span data-ttu-id="723f8-184">(에뮬레이터에서 **설정**으로 이동하고 **계정 추가**를 클릭함.) 에뮬레이터가 인터넷에 연결되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-184">(In the emulator, navigate to **Settings** and click **Add Account**.) Also, make sure that the emulator is connected to the Internet.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="723f8-185">Android 버전 5.0 이후의 알림 설계는 이전 버전과 상당한 차이가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-185">Notification design in Android version 5.0 and later represents a significant departure from that of previous versions.</span></span> <span data-ttu-id="723f8-186">자세한 내용은 [Android 알림](http://go.microsoft.com/fwlink/?LinkId=615880)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="723f8-186">For more information, see [Android Notifications](http://go.microsoft.com/fwlink/?LinkId=615880).</span></span>
> 
> 

1. <span data-ttu-id="723f8-187">**Tools**에서 **Open Android Emulator Manager**를 클릭하고 해당 장치를 선택한 후 **Edit**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-187">From **Tools**, click **Open Android Emulator Manager**, select your device, and then click **Edit**.</span></span>
   
      ![][18]
2. <span data-ttu-id="723f8-188">**대상**에서 **Google API**를 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-188">Select **Google APIs** in **Target**, and then click **OK**.</span></span>
   
      ![][19]
3. <span data-ttu-id="723f8-189">위쪽 도구 모음에서 **Run**을 클릭하고 앱을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-189">On the top toolbar, click **Run**, and then select your app.</span></span> <span data-ttu-id="723f8-190">에뮬레이터가 시작되고 앱이 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-190">This starts the emulator and runs the app.</span></span>
   
   <span data-ttu-id="723f8-191">앱이 GCM에서 *registrationId* 를 검색하고 알림 허브에 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-191">The app retrieves the *registrationId* from GCM and registers with the notification hub.</span></span>

## <a name="send-notifications-from-your-backend"></a><span data-ttu-id="723f8-192">백 엔드에서 알림 보내기</span><span class="sxs-lookup"><span data-stu-id="723f8-192">Send notifications from your backend</span></span>
<span data-ttu-id="723f8-193">아래 화면과 같이 알림 허브의 디버그 탭을 통해 [Azure 클래식 포털] 에서 알림을 보내서 앱의 알림 수신을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-193">You can test receiving notifications in your app by sending notifications in the [Azure Classic Portal] via the debug tab on the notification hub, as shown in the screen below.</span></span>

![][30]

<span data-ttu-id="723f8-194">푸시 알림은 일반적으로 호환 라이브러리를 통해 모바일 서비스 또는 ASP.NET과 같은 백 엔드 서비스에서 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-194">Push notifications are normally sent in a backend service like Mobile Services or ASP.NET through a compatible library.</span></span> <span data-ttu-id="723f8-195">백 엔드에 라이브러리를 사용할 수 없는 경우 직접 REST API를 사용하여 알림 메시지를 보낼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-195">You can also use the REST API directly to send notification messages if a library is not available for your backend.</span></span>

<span data-ttu-id="723f8-196">알림을 보내기 위해 검토할 수 있는 다른 자습서 목록은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-196">Here is a list of some other tutorials that you may want to review for sending notifications:</span></span>

* <span data-ttu-id="723f8-197">ASP.NET: [알림 허브를 사용하여 사용자에게 알림 푸시]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="723f8-197">ASP.NET: See [Use Notification Hubs to push notifications to users].</span></span>
* <span data-ttu-id="723f8-198">Azure 알림 허브 Java SDK: Java에서 알림을 보내는 방법은 [Java에서 알림 허브를 사용하는 방법](notification-hubs-java-push-notification-tutorial.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="723f8-198">Azure Notification Hubs Java SDK: See [How to use Notification Hubs from Java](notification-hubs-java-push-notification-tutorial.md) for sending notifications from Java.</span></span> <span data-ttu-id="723f8-199">이는 Eclipse for Android Development에서 테스트되었습니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-199">This has been tested in Eclipse for Android Development.</span></span>
* <span data-ttu-id="723f8-200">PHP: [PHP에서 알림 허브를 사용하는 방법](notification-hubs-php-push-notification-tutorial.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="723f8-200">PHP: See [How to use Notification Hubs from PHP](notification-hubs-php-push-notification-tutorial.md).</span></span>

<span data-ttu-id="723f8-201">이 자습서의 다음 부분에서는 .NET 콘솔 앱을 사용하고 노드 스크립트를 통해 모바일 서비스를 사용하여 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-201">In the next subsections of the tutorial, you send notifications by using a .NET console app, and by using a mobile service through a node script.</span></span>

#### <a name="optional-send-notifications-by-using-a-net-app"></a><span data-ttu-id="723f8-202">(선택 사항) .NET 앱을 사용하여 알림 보내기</span><span class="sxs-lookup"><span data-stu-id="723f8-202">(Optional) Send notifications by using a .NET app</span></span>
<span data-ttu-id="723f8-203">이 섹션에서는 .NET 콘솔 앱을 사용하여 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-203">In this section, we will send notifications by using a .NET console app</span></span>

1. <span data-ttu-id="723f8-204">새 Visual C# 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-204">Create a new Visual C# console application:</span></span>
   
      ![][20]
2. <span data-ttu-id="723f8-205">Visual Studio에서 **도구**를 클릭하고 **NuGet 패키지 관리자**를 클릭한 다음 **패키지 관리자 콘솔**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-205">In Visual Studio, click **Tools**, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="723f8-206">그러면 Visual Studio에 패키지 관리자 콘솔이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-206">This displays the Package Manager Console in Visual Studio.</span></span>
3. <span data-ttu-id="723f8-207">패키지 관리자 콘솔 창에서 **기본 프로젝트**를 새 콘솔 응용 프로그램 프로젝트로 설정한 후 콘솔 창에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-207">In the Package Manager Console window, set the **Default project** to your new console application project, and then in the console window, execute the following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="723f8-208">그러면 <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet 패키지</a>를 사용하는 Azure Notification Hubs SDK에 대한 참조가 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-208">This adds a reference to the Azure Notification Hubs SDK using the <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. <span data-ttu-id="723f8-209">Program.cs 파일을 열고 다음 `using` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-209">Open the Program.cs file and add the following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="723f8-210">`Program` 클래스에 다음 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-210">In your `Program` class, add the following method.</span></span> <span data-ttu-id="723f8-211">자리 표시자 텍스트를 *DefaultFullSharedAccessSignature* 연결 문자열과 [Azure 클래식 포털]의 허브 이름을 사용하여 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-211">Update the placeholder text with your *DefaultFullSharedAccessSignature* connection string and hub name from the [Azure Classic Portal].</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            await hub.SendGcmNativeNotificationAsync("{ \"data\" : {\"message\":\"Hello from Azure!\"}}");
        }
6. <span data-ttu-id="723f8-212">**Main** 메서드에 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-212">Add the following lines in your **Main** method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="723f8-213">F5 키를 눌러 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-213">Press the F5 key to run the app.</span></span> <span data-ttu-id="723f8-214">그러면 앱에서 알림을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-214">You should receive a notification in the app.</span></span>
   
      ![][21]

#### <a name="optional-send-notifications-by-using-a-mobile-service"></a><span data-ttu-id="723f8-215">(선택 사항) 모바일 서비스를 사용하여 알림 보내기</span><span class="sxs-lookup"><span data-stu-id="723f8-215">(Optional) Send notifications by using a mobile service</span></span>
1. <span data-ttu-id="723f8-216">[모바일 서비스 시작]을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-216">Follow [Get started with Mobile Services].</span></span>
2. <span data-ttu-id="723f8-217">[Azure 클래식 포털]에 로그인하고 모바일 서비스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-217">Sign in to the [Azure Classic Portal], and select your mobile service.</span></span>
3. <span data-ttu-id="723f8-218">맨 위에 있는 **스케줄러** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-218">Select the **Scheduler** tab on the top.</span></span>
   
      ![][22]
4. <span data-ttu-id="723f8-219">새 예약된 작업을 만들고 이름을 삽입한 후 **요청 시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-219">Create a new scheduled job, insert a name, and select **On demand**.</span></span>
   
      ![][23]
5. <span data-ttu-id="723f8-220">작업이 만들어졌으면 작업 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-220">When the job is created, click the job name.</span></span> <span data-ttu-id="723f8-221">그런 다음 위쪽 막대에서 **스크립트** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-221">Then click the **Script** tab on the top bar.</span></span>
6. <span data-ttu-id="723f8-222">스케줄러 함수 내에 다음 스크립트를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-222">Insert the following script inside your scheduler function.</span></span> <span data-ttu-id="723f8-223">자리 표시자를 알림 허브 이름과 앞에서 얻은 *DefaultFullSharedAccessSignature* 의 연결 문자열로 바꿔야 합니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-223">Make sure to replace the placeholders with your notification hub name and the connection string for *DefaultFullSharedAccessSignature* that you obtained earlier.</span></span> <span data-ttu-id="723f8-224">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-224">Click **Save**.</span></span>
   
        var azure = require('azure');
        var notificationHubService = azure.createNotificationHubService('<hub name>', '<connection string>');
        notificationHubService.gcm.send(null,'{"data":{"message" : "Hello from Mobile Services!"}}',
          function (error)
          {
            if (!error) {
               console.warn("Notification successful");
            }
            else
            {
              console.warn("Notification failed" + error);
            }
          }
        );
7. <span data-ttu-id="723f8-225">아래쪽 막대에서 **한 번 실행** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-225">Click **Run Once** on the bottom bar.</span></span> <span data-ttu-id="723f8-226">그러면 알림 메시지가 수신되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-226">You should receive a toast notification.</span></span>

## <a name="next-steps"></a><span data-ttu-id="723f8-227">다음 단계</span><span class="sxs-lookup"><span data-stu-id="723f8-227">Next steps</span></span>
<span data-ttu-id="723f8-228">이 간단한 예제에서는 모든 Android 장치로 알림을 브로드캐스트합니다.</span><span class="sxs-lookup"><span data-stu-id="723f8-228">In this simple example, you broadcasted notifications to all your Android devices.</span></span> <span data-ttu-id="723f8-229">특정 사용자를 대상으로 하려면 [알림 허브를 사용하여 사용자에게 알림 푸시](영문) 자습서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="723f8-229">In order to target specific users, refer to the tutorial [Use Notification Hubs to push notifications to users].</span></span> <span data-ttu-id="723f8-230">사용자를 관심 그룹별로 분할하려면 [알림 허브를 사용하여 뉴스 속보 보내기](영문)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="723f8-230">If you want to segment your users by interest groups, you can read [Use Notification Hubs to send breaking news].</span></span> <span data-ttu-id="723f8-231">알림 허브 사용 방법에 대해 자세히 알아보려면 [알림 허브 지침] 및 [Android용 알림 허브 방법]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="723f8-231">Learn more about how to use Notification Hubs in [Notification Hubs Guidance] and in the [Notification Hubs How-To for Android].</span></span>

<!-- Anchors. -->
[Enable Google Cloud Messaging]: #register
[Configure your Notification Hub]: #configure-hub
[Connecting your app to the Notification Hub]: #connecting-app
[Run your app with the emulator]: #run-app
[Send notifications from your back-end]: #send
[Next steps]:#next-steps

<!-- Images. -->

[11]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-configure-android.png

[13]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-app1.png
[15]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-app3.png

[18]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-android-app7.png
[19]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-android-app8.png

[20]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-console-app.png
[21]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-android-toast.png
[22]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-scheduler1.png
[23]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-scheduler2.png

[30]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hubs-debug-hub-gcm.png


<!-- URLs. -->
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
<span data-ttu-id="723f8-232">[모바일 서비스 시작]: /develop/mobile/tutorials/get-started-xamarin-android/#create-new-service</span><span class="sxs-lookup"><span data-stu-id="723f8-232">[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-xamarin-android/#create-new-service</span></span>
[JavaScript and HTML]: /develop/mobile/tutorials/get-started-with-push-js

<span data-ttu-id="723f8-233">[Azure 클래식 포털]: https://manage.windowsazure.com/</span><span class="sxs-lookup"><span data-stu-id="723f8-233">[Azure Classic Portal]: https://manage.windowsazure.com/</span></span>
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
<span data-ttu-id="723f8-234">[알림 허브 지침]: http://msdn.microsoft.com/library/jj927170.aspx</span><span class="sxs-lookup"><span data-stu-id="723f8-234">[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx</span></span>
<span data-ttu-id="723f8-235">[Android용 알림 허브 방법]: http://msdn.microsoft.com/library/dn282661.aspx</span><span class="sxs-lookup"><span data-stu-id="723f8-235">[Notification Hubs How-To for Android]: http://msdn.microsoft.com/library/dn282661.aspx</span></span>

<span data-ttu-id="723f8-236">[알림 허브를 사용하여 사용자에게 알림 푸시]: /manage/services/notification-hubs/notify-users-aspnet</span><span class="sxs-lookup"><span data-stu-id="723f8-236">[Use Notification Hubs to push notifications to users]: /manage/services/notification-hubs/notify-users-aspnet</span></span>
<span data-ttu-id="723f8-237">[알림 허브를 사용하여 뉴스 속보 보내기]: /manage/services/notification-hubs/breaking-news-dotnet</span><span class="sxs-lookup"><span data-stu-id="723f8-237">[Use Notification Hubs to send breaking news]: /manage/services/notification-hubs/breaking-news-dotnet</span></span>
[GCMClient Component page]: http://components.xamarin.com/view/GCMClient
[Xamarin.NotificationHub GitHub page]: https://github.com/SaschaDittmann/Xamarin.NotificationHub
[GitHub]: http://go.microsoft.com/fwlink/p/?LinkId=331329
<span data-ttu-id="723f8-238">[Google Cloud Messaging 클라이언트 구성 요소]: http://components.xamarin.com/view/GCMClient/</span><span class="sxs-lookup"><span data-stu-id="723f8-238">[Google Cloud Messaging Client Component]: http://components.xamarin.com/view/GCMClient/</span></span>
<span data-ttu-id="723f8-239">[Azure 메시징 구성 요소]: http://components.xamarin.com/view/azure-messaging</span><span class="sxs-lookup"><span data-stu-id="723f8-239">[Azure Messaging Component]: http://components.xamarin.com/view/azure-messaging</span></span>

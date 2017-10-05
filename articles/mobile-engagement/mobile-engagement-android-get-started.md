---
title: "Android 앱 Azure Mobile Engagement 시작"
description: "Android 앱에 대해 분석 및 푸시 알림과 함께 Azure Mobile Engagement를 사용하는 방법을 알아봅니다."
services: mobile-engagement
documentationcenter: android
author: piyushjo
manager: erikre
editor: 
ms.assetid: 3c286c6d-cfef-4e3e-9b2c-715429fe82db
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: hero-article
ms.date: 08/10/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: dc255a930bf71e6ef6d964bc5e3472a38ce4e467
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-android-apps"></a><span data-ttu-id="52fd6-103">Android 앱용 Azure Mobile Engagement 시작</span><span class="sxs-lookup"><span data-stu-id="52fd6-103">Get started with Azure Mobile Engagement for Android apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="52fd6-104">이 항목에서는 Azure Mobile Engagement를 사용하여 앱 사용을 이해하고 Android 응용 프로그램의 분할된 사용자에게 푸시 알림을 보내는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="52fd6-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and how to send push notifications to segmented users of an Android application.</span></span>
<span data-ttu-id="52fd6-105">이 자습서에서는 Mobile Engagement를 사용하는 간단한 브로드캐스트 시나리오를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="52fd6-105">This tutorial demonstrates the simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="52fd6-106">해당 시나리오에서 기본 데이터를 수집하고 GCM(Google Cloud Messaging)을 사용하여 푸시 알림을 받는 빈 Android 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="52fd6-106">In it, you create a blank Android app that collects basic data and receives push notifications using Google Cloud Messaging (GCM).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="52fd6-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="52fd6-107">Prerequisites</span></span>
<span data-ttu-id="52fd6-108">이 자습서를 완료하려면 Android Studio 통합 개발 환경이 포함된 [Android 개발자 도구](https://developer.android.com/sdk/index.html)및 최신 Android 플랫폼이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="52fd6-108">Completing this tutorial requires the [Android Developer Tools](https://developer.android.com/sdk/index.html), which includes the Android Studio integrated development environment, and the latest Android platform.</span></span>

<span data-ttu-id="52fd6-109">[Mobile Engagement Android SDK](https://aka.ms/vq9mfn)도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="52fd6-109">It also requires the [Mobile Engagement Android SDK](https://aka.ms/vq9mfn).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="52fd6-110">이 자습서를 완료하려면 활성 Azure 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="52fd6-110">To complete this tutorial, you need an active Azure account.</span></span> <span data-ttu-id="52fd6-111">계정이 없는 경우 몇 분 만에 무료 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52fd6-111">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="52fd6-112">자세한 내용은 [Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-android-get-started)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="52fd6-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-android-get-started).</span></span>
>
>

## <a name="set-up-mobile-engagement-for-your-android-app"></a><span data-ttu-id="52fd6-113">Android 앱용 Mobile Engagement 설정</span><span class="sxs-lookup"><span data-stu-id="52fd6-113">Set up Mobile Engagement for your Android app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a name="connect-your-app-to-the-mobile-engagement-backend"></a><span data-ttu-id="52fd6-114">Mobile Engagement 백 엔드에 앱 연결</span><span class="sxs-lookup"><span data-stu-id="52fd6-114">Connect your app to the Mobile Engagement backend</span></span>
<span data-ttu-id="52fd6-115">이 자습서에서는 데이터를 수집하고 푸시 알림을 보내는 데 필요한 최소 집합인 "기본 통합" 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="52fd6-115">This tutorial presents a "basic integration", which is the minimal set required to collect data and send a push notification.</span></span> <span data-ttu-id="52fd6-116">통합을 시연하기 위해 Android Studio로 기본 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="52fd6-116">You create a basic app with Android Studio to demonstrate the integration.</span></span>

<span data-ttu-id="52fd6-117">전체 통합 설명서는 [Mobile Engagement Android SDK 통합](mobile-engagement-android-sdk-overview.md)에서 찾아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52fd6-117">The complete integration documentation can be found in the [Mobile Engagement Android SDK integration](mobile-engagement-android-sdk-overview.md).</span></span>

### <a name="create-an-android-project"></a><span data-ttu-id="52fd6-118">Android 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="52fd6-118">Create an Android project</span></span>
1. <span data-ttu-id="52fd6-119">**Android Studio**를 시작하고 팝업에서 **새 Android Studio 프로젝트 시작**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="52fd6-119">Start **Android Studio**, and in the pop-up, select **Start a new Android Studio project**.</span></span>

    ![][1]
2. <span data-ttu-id="52fd6-120">앱 이름 및 회사 도메인을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="52fd6-120">Provide an app name and company domain.</span></span> <span data-ttu-id="52fd6-121">나중에 필요하기 때문에 입력한 내용을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="52fd6-121">Make a note of what you are filling, because you need it later.</span></span> <span data-ttu-id="52fd6-122">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="52fd6-122">Click **Next**.</span></span>

    ![][2]
3. <span data-ttu-id="52fd6-123">대상 폼 팩터 및 API 수준을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="52fd6-123">Select the target form factor and API level, and click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="52fd6-124">Mobile Engagement를 사용하려면 API 수준 10 이상(Android 2.3.3)이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="52fd6-124">Mobile Engagement requires API level 10 minimum (Android 2.3.3).</span></span>
   >
   >

    ![][3]
4. <span data-ttu-id="52fd6-125">이 앱에 대한 유일한 화면인 **빈 활동**을 여기서 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="52fd6-125">Select **Blank Activity** here, which is the only screen for this app and click **Next**.</span></span>

    ![][4]
5. <span data-ttu-id="52fd6-126">마지막으로 기본값을 그대로 두고 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="52fd6-126">Finally, leave the defaults as is and click **Finish**.</span></span>

    ![][5]

<span data-ttu-id="52fd6-127">이제 Android Studio가 Mobile Engagement를 통합할 데모 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="52fd6-127">Android Studio now creates the demo app into which we integrate Mobile Engagement.</span></span>

### <a name="include-the-sdk-library-in-your-project"></a><span data-ttu-id="52fd6-128">프로젝트에 SDK 라이브러리 포함</span><span class="sxs-lookup"><span data-stu-id="52fd6-128">Include the SDK library in your project</span></span>
1. <span data-ttu-id="52fd6-129">[Mobile Engagement Android SDK](https://aka.ms/vq9mfn)를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="52fd6-129">Download the [Mobile Engagement Android SDK](https://aka.ms/vq9mfn).</span></span>
2. <span data-ttu-id="52fd6-130">보관 파일을 컴퓨터의 폴더로 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="52fd6-130">Extract the archive file to a folder in your computer.</span></span>
3. <span data-ttu-id="52fd6-131">이 SDK의 최신 버전에 대한 .jar 라이브러리를 확인하고 클립보드로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="52fd6-131">Identify the .jar library for the current version of this SDK and copy it to the Clipboard.</span></span>

      ![][6]
4. <span data-ttu-id="52fd6-132">**Project** 섹션으로 이동하여(1) libs 폴더에 .jar을 붙여넣습니다(2).</span><span class="sxs-lookup"><span data-stu-id="52fd6-132">Navigate to the **Project** section (1) and paste the .jar in the libs folder (2).</span></span>

      ![][7]
5. <span data-ttu-id="52fd6-133">라이브러리를 로드하려면 프로젝트를 동기화합니다.</span><span class="sxs-lookup"><span data-stu-id="52fd6-133">To load the library, sync the project .</span></span>

      ![][8]

### <a name="connect-your-app-to-mobile-engagement-backend-with-the-connection-string"></a><span data-ttu-id="52fd6-134">연결 문자열을 사용하여 Mobile Engagement 백 엔드에 앱 연결</span><span class="sxs-lookup"><span data-stu-id="52fd6-134">Connect your app to Mobile Engagement backend with the Connection String</span></span>
1. <span data-ttu-id="52fd6-135">작업 생성에 다음 코드 줄을 복사합니다(응용 프로그램의 한 위치에서만 수행해야 하며, 일반적으로 기본 작업에서 수행함).</span><span class="sxs-lookup"><span data-stu-id="52fd6-135">Copy the following lines of code into the activity creation (must be done only in one place of your application, usually the main activity).</span></span> <span data-ttu-id="52fd6-136">이 샘플 앱의 경우  src -> 기본 -> java 폴더에서 MainActivity를 열고 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="52fd6-136">For this sample app, open up the MainActivity under src -> main -> java folder and add the following:</span></span>

        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
        EngagementAgent.getInstance(this).init(engagementConfiguration);
2. <span data-ttu-id="52fd6-137">Alt + Enter를 누르거나 다음 import 문을 추가하여 참조를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="52fd6-137">Resolve the references by pressing Alt + Enter or adding the following import statements:</span></span>

        import com.microsoft.azure.engagement.EngagementAgent;
        import com.microsoft.azure.engagement.EngagementConfiguration;
3. <span data-ttu-id="52fd6-138">앱 **연결 정보** 페이지의 Azure 클래식 포털로 돌아가서 **연결 문자열**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="52fd6-138">Go back to the Azure Classic Portal in your app's **Connection Info** page and copy the **Connection String**.</span></span>

      ![][9]
4. <span data-ttu-id="52fd6-139">이를 `setConnectionString` 매개 변수에 붙여 넣어 다음 코드에 표시된 전체 문자열을 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="52fd6-139">Paste it into the `setConnectionString` parameter, replacing the entire string shown in the following code:</span></span>

        engagementConfiguration.setConnectionString("Endpoint=my-company-name.device.mobileengagement.windows.net;SdkKey=********************;AppId=*********");

### <a name="add-permissions-and-a-service-declaration"></a><span data-ttu-id="52fd6-140">권한 및 서비스 선언 추가</span><span class="sxs-lookup"><span data-stu-id="52fd6-140">Add permissions and a service declaration</span></span>
1. <span data-ttu-id="52fd6-141">프로젝트의 Manifest.xml에서 `<application>` 태그 바로 앞에 다음 권한을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="52fd6-141">Add these permissions to the Manifest.xml of your project immediately before or after the `<application>` tag:</span></span>

        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
2. <span data-ttu-id="52fd6-142">에이전트 서비스를 선언하려면 `<application>` 태그와 `</application>` 태그 사이에 이 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="52fd6-142">To declare the agent service, add this code between the `<application>` and `</application>` tags:</span></span>

        <service
             android:name="com.microsoft.azure.engagement.service.EngagementService"
             android:exported="false"
             android:label="<Your application name>"
             android:process=":Engagement"/>
3. <span data-ttu-id="52fd6-143">붙여 넣은 코드에서 레이블의 `"<Your application name>"`을(를) 대체합니다. 레이블은 장치에서 실행 중인 서비스를 볼 수 있는 **설정** 메뉴에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="52fd6-143">In the code you pasted, replace `"<Your application name>"` in the label, which is displayed in the **Settings** menu where you can see services running on the device.</span></span> <span data-ttu-id="52fd6-144">예를 들어 해당 레이블에 "서비스"라는 단어를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52fd6-144">You can add the word "Service" in that label for example.</span></span>

### <a name="send-a-screen-to-mobile-engagement"></a><span data-ttu-id="52fd6-145">Mobile Engagement에 화면 보내기</span><span class="sxs-lookup"><span data-stu-id="52fd6-145">Send a screen to Mobile Engagement</span></span>
<span data-ttu-id="52fd6-146">데이터 보내기를 시작하고 사용자가 활성 상태인지 확인하려면 Mobile Engagement 백 엔드에 화면(활동)을 하나 이상 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="52fd6-146">To start sending data and ensure that the users are active, you must send at least one screen (Activity) to the Mobile Engagement backend.</span></span>

<span data-ttu-id="52fd6-147">**MainActivity.java**로 이동하고 다음을 추가하여 **MainActivity**의 기본 클래스를 **EngagementActivity**로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="52fd6-147">Go to **MainActivity.java** and add the following to replace the base class of **MainActivity** to **EngagementActivity**:</span></span>

    public class MainActivity extends EngagementActivity {

> [!NOTE]
> <span data-ttu-id="52fd6-148">기본 클래스가 *활동*이 아닌 경우 [고급 Android 보고](mobile-engagement-android-advanced-reporting.md) 에서 다른 클래스에서 상속하는 방법을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="52fd6-148">If your base class is not *Activity*, consult [Advanced Android Reporting](mobile-engagement-android-advanced-reporting.md) for how to inherit from different classes.</span></span>
>
>

<span data-ttu-id="52fd6-149">간단한 샘플 시나리오에 대해 다음 줄을 주석 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="52fd6-149">Comment out the following line for this simple sample scenario:</span></span>

    // setSupportActionBar(toolbar);

<span data-ttu-id="52fd6-150">앱에서 `ActionBar` 을(를) 유지하려는 경우 [고급 Android 보고](mobile-engagement-android-advanced-reporting.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="52fd6-150">If you want to keep the `ActionBar` in your app, see [Advanced Android Reporting](mobile-engagement-android-advanced-reporting.md).</span></span>

## <a name="connect-app-with-real-time-monitoring"></a><span data-ttu-id="52fd6-151">실시간 모니터링과 앱 연결</span><span class="sxs-lookup"><span data-stu-id="52fd6-151">Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a name="enable-push-notifications-and-in-app-messaging"></a><span data-ttu-id="52fd6-152">푸시 알림 및 앱 내 메시징 사용</span><span class="sxs-lookup"><span data-stu-id="52fd6-152">Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="52fd6-153">캠페인 도중 Mobile Engagement에서는 사용자와 상호 작용하고 푸시 알림 및 앱 내 메시징을 통해 사용자에게 알릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52fd6-153">During a campaign, Mobile Engagement lets you interact with and REACH your users with push notifications and in-app messaging.</span></span> <span data-ttu-id="52fd6-154">Mobile Engagement 포털에서는 이 모듈을 도달률이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="52fd6-154">This module is called REACH in the Mobile Engagement portal.</span></span>
<span data-ttu-id="52fd6-155">다음 섹션에서는 이를 수신하도록 앱을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="52fd6-155">The following section sets up your app to receive them.</span></span>

### <a name="copy-sdk-resources-in-your-project"></a><span data-ttu-id="52fd6-156">프로젝트에 SDK 리소스 복사</span><span class="sxs-lookup"><span data-stu-id="52fd6-156">Copy SDK resources in your project</span></span>
1. <span data-ttu-id="52fd6-157">다시 SDK 다운로드 콘텐츠로 돌아가서 **res** 폴더를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="52fd6-157">Navigate back to your SDK download content and copy the **res** folder.</span></span>

    ![][10]
2. <span data-ttu-id="52fd6-158">Android Studio로 돌아가서 프로젝트 파일의 **main** 디렉터리를 선택하고 붙여넣어 프로젝트에 리소스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="52fd6-158">Go back to Android Studio, select the **main** directory of your project files, and then paste it to add the resources to your project.</span></span>

    ![][11]

[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

[!INCLUDE [Enable in-app messaging](../../includes/mobile-engagement-android-send-push.md)]

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="52fd6-159">다음 단계</span><span class="sxs-lookup"><span data-stu-id="52fd6-159">Next steps</span></span>
<span data-ttu-id="52fd6-160">[Android SDK](mobile-engagement-android-sdk-overview.md) 로 돌아가 SDK 통합에 대한 자세한 정보를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="52fd6-160">Go to [Android SDK](mobile-engagement-android-sdk-overview.md) to get detailed knowledge about the SDK integration.</span></span>

<!-- Images. -->
[1]: ./media/mobile-engagement-android-get-started/android-studio-new-project.png
[2]: ./media/mobile-engagement-android-get-started/android-studio-project-props.png
[3]: ./media/mobile-engagement-android-get-started/android-studio-project-props2.png
[4]: ./media/mobile-engagement-android-get-started/android-studio-add-activity.png
[5]: ./media/mobile-engagement-android-get-started/android-studio-activity-name.png
[6]: ./media/mobile-engagement-android-get-started/sdk-content.png
[7]: ./media/mobile-engagement-android-get-started/paste-jar.png
[8]: ./media/mobile-engagement-android-get-started/sync-project.png
[9]: ./media/mobile-engagement-android-get-started/app-connection-info-page.png
[10]: ./media/mobile-engagement-android-get-started/copy-resources.png
[11]: ./media/mobile-engagement-android-get-started/paste-resources.png

---
title: "Android 앱 Azure Mobile Engagement aaaGet 시작"
description: "자세한 방법을 toouse Azure Mobile Engagement Android 앱에 대 한 분석 및 푸시 알림 사용 합니다."
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
ms.openlocfilehash: e8c92607691104750cdf1c4f7639a041d8a7bcd5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-android-apps"></a><span data-ttu-id="80267-103">Android 앱용 Azure Mobile Engagement 시작</span><span class="sxs-lookup"><span data-stu-id="80267-103">Get started with Azure Mobile Engagement for Android apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="80267-104">이 항목에서는 Azure Mobile Engagement toounderstand toouse 앱 사용량과 toosend 밀어넣기 Android 응용 프로그램의 알림을 toosegmented 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="80267-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and how toosend push notifications toosegmented users of an Android application.</span></span>
<span data-ttu-id="80267-105">이 자습서에는 hello 간단한 브로드캐스트 시나리오를 Mobile Engagement를 사용 하 여 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="80267-105">This tutorial demonstrates hello simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="80267-106">해당 시나리오에서 기본 데이터를 수집하고 GCM(Google Cloud Messaging)을 사용하여 푸시 알림을 받는 빈 Android 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="80267-106">In it, you create a blank Android app that collects basic data and receives push notifications using Google Cloud Messaging (GCM).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="80267-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="80267-107">Prerequisites</span></span>
<span data-ttu-id="80267-108">Hello 필요이 자습서를 완료 [Android 개발자 도구](https://developer.android.com/sdk/index.html), hello Android Studio 통합된 개발 환경 및 hello 최신 Android 플랫폼 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="80267-108">Completing this tutorial requires hello [Android Developer Tools](https://developer.android.com/sdk/index.html), which includes hello Android Studio integrated development environment, and hello latest Android platform.</span></span>

<span data-ttu-id="80267-109">또한 hello 해야 [Mobile Engagement Android SDK](https://aka.ms/vq9mfn)합니다.</span><span class="sxs-lookup"><span data-stu-id="80267-109">It also requires hello [Mobile Engagement Android SDK](https://aka.ms/vq9mfn).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="80267-110">toocomplete이이 자습서에서는 활성 Azure 계정이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="80267-110">toocomplete this tutorial, you need an active Azure account.</span></span> <span data-ttu-id="80267-111">계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80267-111">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="80267-112">자세한 내용은 [Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-android-get-started)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="80267-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-android-get-started).</span></span>
>
>

## <a name="set-up-mobile-engagement-for-your-android-app"></a><span data-ttu-id="80267-113">Android 앱용 Mobile Engagement 설정</span><span class="sxs-lookup"><span data-stu-id="80267-113">Set up Mobile Engagement for your Android app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a name="connect-your-app-toohello-mobile-engagement-backend"></a><span data-ttu-id="80267-114">응용 프로그램 toohello Mobile Engagement 백 엔드 연결</span><span class="sxs-lookup"><span data-stu-id="80267-114">Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="80267-115">이 자습서는 기본적인 "통합", 최소 hello 필요한 toocollect 데이터 설정 되 고 푸시 알림을 보내는 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="80267-115">This tutorial presents a "basic integration", which is hello minimal set required toocollect data and send a push notification.</span></span> <span data-ttu-id="80267-116">Android Studio toodemonstrate hello 통합 된 기본 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="80267-116">You create a basic app with Android Studio toodemonstrate hello integration.</span></span>

<span data-ttu-id="80267-117">hello에 hello 완벽 한 통합 설명서를 확인할 수 있습니다 [Mobile Engagement Android SDK 통합](mobile-engagement-android-sdk-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="80267-117">hello complete integration documentation can be found in hello [Mobile Engagement Android SDK integration](mobile-engagement-android-sdk-overview.md).</span></span>

### <a name="create-an-android-project"></a><span data-ttu-id="80267-118">Android 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="80267-118">Create an Android project</span></span>
1. <span data-ttu-id="80267-119">시작 **Android Studio**, hello 팝업에서 선택 하 고 **새 Android Studio 프로젝트 시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="80267-119">Start **Android Studio**, and in hello pop-up, select **Start a new Android Studio project**.</span></span>

    ![][1]
2. <span data-ttu-id="80267-120">앱 이름 및 회사 도메인을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="80267-120">Provide an app name and company domain.</span></span> <span data-ttu-id="80267-121">나중에 필요하기 때문에 입력한 내용을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="80267-121">Make a note of what you are filling, because you need it later.</span></span> <span data-ttu-id="80267-122">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="80267-122">Click **Next**.</span></span>

    ![][2]
3. <span data-ttu-id="80267-123">Hello 대상 폼 팩터 수준 요약과 API 수준 선택 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="80267-123">Select hello target form factor and API level, and click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="80267-124">Mobile Engagement를 사용하려면 API 수준 10 이상(Android 2.3.3)이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="80267-124">Mobile Engagement requires API level 10 minimum (Android 2.3.3).</span></span>
   >
   >

    ![][3]
4. <span data-ttu-id="80267-125">선택 **빈 활동** 여기 클릭 하 고이 응용 프로그램에 대 한 유일한 화면 hello **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="80267-125">Select **Blank Activity** here, which is hello only screen for this app and click **Next**.</span></span>

    ![][4]
5. <span data-ttu-id="80267-126">마지막으로, 클릭 하 고 hello 기본값 그대로 두고 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="80267-126">Finally, leave hello defaults as is and click **Finish**.</span></span>

    ![][5]

<span data-ttu-id="80267-127">Android Studio는 이제 Mobile Engagement 통합 우리는 hello 데모 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="80267-127">Android Studio now creates hello demo app into which we integrate Mobile Engagement.</span></span>

### <a name="include-hello-sdk-library-in-your-project"></a><span data-ttu-id="80267-128">프로젝트에 hello SDK 라이브러리를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="80267-128">Include hello SDK library in your project</span></span>
1. <span data-ttu-id="80267-129">Hello 다운로드 [Mobile Engagement Android SDK](https://aka.ms/vq9mfn)합니다.</span><span class="sxs-lookup"><span data-stu-id="80267-129">Download hello [Mobile Engagement Android SDK](https://aka.ms/vq9mfn).</span></span>
2. <span data-ttu-id="80267-130">컴퓨터의 보관 파일 tooa 폴더 hello를 추출 합니다.</span><span class="sxs-lookup"><span data-stu-id="80267-130">Extract hello archive file tooa folder in your computer.</span></span>
3. <span data-ttu-id="80267-131">이 SDK의 현재 버전 hello에 대 한 hello.jar 라이브러리를 식별 하 고 toohello 클립보드로 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="80267-131">Identify hello .jar library for hello current version of this SDK and copy it toohello Clipboard.</span></span>

      ![][6]
4. <span data-ttu-id="80267-132">Toohello 이동 **프로젝트** 섹션 (1) 및 hello.jar hello libs 폴더 (2)에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="80267-132">Navigate toohello **Project** section (1) and paste hello .jar in hello libs folder (2).</span></span>

      ![][7]
5. <span data-ttu-id="80267-133">동기화 hello 프로젝트 tooload hello 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="80267-133">tooload hello library, sync hello project .</span></span>

      ![][8]

### <a name="connect-your-app-toomobile-engagement-backend-with-hello-connection-string"></a><span data-ttu-id="80267-134">연결 문자열 hello를 사용 하 여 응용 프로그램 tooMobile Engagement 백 엔드 연결</span><span class="sxs-lookup"><span data-stu-id="80267-134">Connect your app tooMobile Engagement backend with hello Connection String</span></span>
1. <span data-ttu-id="80267-135">Hello (hello 기본 활동 일반적으로 응용 프로그램의 한 곳에만 수행 해야 합니다) hello 작업 만들기에 줄의 코드를 다음을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="80267-135">Copy hello following lines of code into hello activity creation (must be done only in one place of your application, usually hello main activity).</span></span> <span data-ttu-id="80267-136">이 샘플 응용 프로그램에 대 한 hello MainActivity src에서 열고 주->-> java 폴더 및 hello 다음 추가:</span><span class="sxs-lookup"><span data-stu-id="80267-136">For this sample app, open up hello MainActivity under src -> main -> java folder and add hello following:</span></span>

        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
        EngagementAgent.getInstance(this).init(engagementConfiguration);
2. <span data-ttu-id="80267-137">Alt + Enter를 누르거나 hello 다음 import 문을 추가 하 여 hello 참조를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="80267-137">Resolve hello references by pressing Alt + Enter or adding hello following import statements:</span></span>

        import com.microsoft.azure.engagement.EngagementAgent;
        import com.microsoft.azure.engagement.EngagementConfiguration;
3. <span data-ttu-id="80267-138">Toohello Azure 클래식 포털에서 앱의 돌아가서 **연결 정보입니다.** 페이지 및 복사 hello **연결 문자열**합니다.</span><span class="sxs-lookup"><span data-stu-id="80267-138">Go back toohello Azure Classic Portal in your app's **Connection Info** page and copy hello **Connection String**.</span></span>

      ![][9]
4. <span data-ttu-id="80267-139">Hello에 붙여 `setConnectionString` hello hello 코드 다음에 표시 되는 전체 문자열 대체 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="80267-139">Paste it into hello `setConnectionString` parameter, replacing hello entire string shown in hello following code:</span></span>

        engagementConfiguration.setConnectionString("Endpoint=my-company-name.device.mobileengagement.windows.net;SdkKey=********************;AppId=*********");

### <a name="add-permissions-and-a-service-declaration"></a><span data-ttu-id="80267-140">권한 및 서비스 선언 추가</span><span class="sxs-lookup"><span data-stu-id="80267-140">Add permissions and a service declaration</span></span>
1. <span data-ttu-id="80267-141">바로 앞 또는 뒤 hello 이러한 사용 권한을 toohello Manifest.xml 프로젝트의 추가 `<application>` 태그:</span><span class="sxs-lookup"><span data-stu-id="80267-141">Add these permissions toohello Manifest.xml of your project immediately before or after hello `<application>` tag:</span></span>

        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
2. <span data-ttu-id="80267-142">toodeclare hello 사이 다음이 코드를 추가, 에이전트 서비스를 hello `<application>` 및 `</application>` 태그:</span><span class="sxs-lookup"><span data-stu-id="80267-142">toodeclare hello agent service, add this code between hello `<application>` and `</application>` tags:</span></span>

        <service
             android:name="com.microsoft.azure.engagement.service.EngagementService"
             android:exported="false"
             android:label="<Your application name>"
             android:process=":Engagement"/>
3. <span data-ttu-id="80267-143">붙여 넣은 hello 코드에서 대체할 `"<Your application name>"` hello 레이블에 표시 되는 hello에 **설정을** 메뉴 hello 장치에서 실행 되는 서비스를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80267-143">In hello code you pasted, replace `"<Your application name>"` in hello label, which is displayed in hello **Settings** menu where you can see services running on hello device.</span></span> <span data-ttu-id="80267-144">예를 들어 hello 단어 "서비스" 해당 레이블에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80267-144">You can add hello word "Service" in that label for example.</span></span>

### <a name="send-a-screen-toomobile-engagement"></a><span data-ttu-id="80267-145">화면 tooMobile Engagement 보내기</span><span class="sxs-lookup"><span data-stu-id="80267-145">Send a screen tooMobile Engagement</span></span>
<span data-ttu-id="80267-146">데이터 보내기 toostart 확인 hello 사용자는 active, 하나 이상의 화면 (활동) toohello Mobile Engagement 백 엔드를 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="80267-146">toostart sending data and ensure that hello users are active, you must send at least one screen (Activity) toohello Mobile Engagement backend.</span></span>

<span data-ttu-id="80267-147">너무 이동**MainActivity.java** hello tooreplace hello 기본 클래스의 다음 추가 **MainActivity** 너무**EngagementActivity**:</span><span class="sxs-lookup"><span data-stu-id="80267-147">Go too**MainActivity.java** and add hello following tooreplace hello base class of **MainActivity** too**EngagementActivity**:</span></span>

    public class MainActivity extends EngagementActivity {

> [!NOTE]
> <span data-ttu-id="80267-148">기본 클래스가 없는 경우 *활동*, 참조 [고급 Android 보고](mobile-engagement-android-advanced-reporting.md) 방법에 대 한 서로 다른 클래스에서 tooinherit 합니다.</span><span class="sxs-lookup"><span data-stu-id="80267-148">If your base class is not *Activity*, consult [Advanced Android Reporting](mobile-engagement-android-advanced-reporting.md) for how tooinherit from different classes.</span></span>
>
>

<span data-ttu-id="80267-149">다음 줄이 간단한 샘플 시나리오에 대 한 hello 주석 처리.</span><span class="sxs-lookup"><span data-stu-id="80267-149">Comment out hello following line for this simple sample scenario:</span></span>

    // setSupportActionBar(toolbar);

<span data-ttu-id="80267-150">Tookeep hello를 원하는 경우 `ActionBar` 응용 프로그램에서 참조 [고급 Android 보고](mobile-engagement-android-advanced-reporting.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="80267-150">If you want tookeep hello `ActionBar` in your app, see [Advanced Android Reporting](mobile-engagement-android-advanced-reporting.md).</span></span>

## <a name="connect-app-with-real-time-monitoring"></a><span data-ttu-id="80267-151">실시간 모니터링과 앱 연결</span><span class="sxs-lookup"><span data-stu-id="80267-151">Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a name="enable-push-notifications-and-in-app-messaging"></a><span data-ttu-id="80267-152">푸시 알림 및 앱 내 메시징 사용</span><span class="sxs-lookup"><span data-stu-id="80267-152">Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="80267-153">캠페인 도중 Mobile Engagement에서는 사용자와 상호 작용하고 푸시 알림 및 앱 내 메시징을 통해 사용자에게 알릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80267-153">During a campaign, Mobile Engagement lets you interact with and REACH your users with push notifications and in-app messaging.</span></span> <span data-ttu-id="80267-154">이 모듈에는 hello Mobile engagement 연결 포털에서 REACH를 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="80267-154">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="80267-155">hello 섹션 다음에 앱 tooreceive를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="80267-155">hello following section sets up your app tooreceive them.</span></span>

### <a name="copy-sdk-resources-in-your-project"></a><span data-ttu-id="80267-156">프로젝트에 SDK 리소스 복사</span><span class="sxs-lookup"><span data-stu-id="80267-156">Copy SDK resources in your project</span></span>
1. <span data-ttu-id="80267-157">뒤로 tooyour SDK 다운로드 콘텐츠 및 복사 hello 이동 **res** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="80267-157">Navigate back tooyour SDK download content and copy hello **res** folder.</span></span>

    ![][10]
2. <span data-ttu-id="80267-158">Studio 선택 hello tooAndroid 돌아가서 **주** 디렉터리로 프로젝트 파일을 복사한 후 tooadd hello 리소스 tooyour 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="80267-158">Go back tooAndroid Studio, select hello **main** directory of your project files, and then paste it tooadd hello resources tooyour project.</span></span>

    ![][11]

[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

[!INCLUDE [Enable in-app messaging](../../includes/mobile-engagement-android-send-push.md)]

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="80267-159">다음 단계</span><span class="sxs-lookup"><span data-stu-id="80267-159">Next steps</span></span>
<span data-ttu-id="80267-160">너무 이동[Android SDK](mobile-engagement-android-sdk-overview.md) tooget hello SDK 통합에 대 한 정보를 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="80267-160">Go too[Android SDK](mobile-engagement-android-sdk-overview.md) tooget detailed knowledge about hello SDK integration.</span></span>

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

---
title: "Cordova/Phonegap용 Azure Mobile Engagement 시작"
description: "Cordova/Phonegap 앱에 대해 분석 및 푸시 알림과 함께 Azure Mobile Engagement를 사용하는 방법을 알아봅니다."
services: mobile-engagement
documentationcenter: Mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 54fe9113-e239-4ed7-9fd1-a502d7ac7f47
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-phonegap
ms.devlang: js
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: d7a761310782faab1dda023785f93cf90742e2ae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-cordovaphonegap"></a><span data-ttu-id="a6dac-103">Cordova/Phonegap용 Azure Mobile Engagement 시작</span><span class="sxs-lookup"><span data-stu-id="a6dac-103">Get Started with Azure Mobile Engagement for Cordova/Phonegap</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="a6dac-104">이 항목에서는 Azure Mobile Engagement를 사용하여 Cordova에서 개발된 모바일 응용 프로그램의 구분된 사용자에게 푸시 알림을 보내고 앱 사용량을 파악하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a6dac-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and send push notifications to segmented users for a mobile application developed with Cordova.</span></span>

<span data-ttu-id="a6dac-105">이 자습서에서는 Mac을 사용하여 빈 Cordova 앱을 만들고 Mobile Engagement SDK를 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="a6dac-105">In this tutorial, we will create a blank Cordova app using Mac and then integrate Mobile Engagement SDK.</span></span> <span data-ttu-id="a6dac-106">기본 분석 데이터를 수집하고 iOS용 APNS(Apple 푸시 알림 시스템) 및 Android용 GCM(Google Cloud Messaging)을 사용하여 푸시 알림을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="a6dac-106">It collects basic analytics data and receives push notifications using Apple Push Notification System (APNS) for iOS and Google Cloud Messaging (GCM) for Android.</span></span> <span data-ttu-id="a6dac-107">테스트를 위해 iOS 또는 Android 장치에 이 앱을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="a6dac-107">We will deploy this to an iOS or Android device for testing.</span></span> 

> [!NOTE]
> <span data-ttu-id="a6dac-108">이 자습서를 완료하려면 활성 Azure 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6dac-108">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="a6dac-109">계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6dac-109">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="a6dac-110">자세한 내용은 [Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-cordova-get-started)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a6dac-110">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-cordova-get-started).</span></span>
> 
> 

<span data-ttu-id="a6dac-111">이 자습서를 사용하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a6dac-111">This tutorial requires the following:</span></span>

* <span data-ttu-id="a6dac-112">Mac 앱 스토어에서 설치할 수 있는 Xcode(iOS 배포용)</span><span class="sxs-lookup"><span data-stu-id="a6dac-112">XCode, which you can install from Mac App Store (for deploying to iOS)</span></span>
* <span data-ttu-id="a6dac-113">[Android SDK 및 에뮬레이터](http://developer.android.com/sdk/installing/index.html)(Android 배포용)</span><span class="sxs-lookup"><span data-stu-id="a6dac-113">[Android SDK & Emulator](http://developer.android.com/sdk/installing/index.html) (for deploying to Android)</span></span>
* <span data-ttu-id="a6dac-114">APNS을 위해 Apple 개발자 센터에서 가져올 수 있는 푸시 알림 인증서(.p12)</span><span class="sxs-lookup"><span data-stu-id="a6dac-114">Push notification certificate (.p12) that you can obtain from Apple Dev Center for APNS</span></span>
* <span data-ttu-id="a6dac-115">GCM을 위해 Google 개발자 콘솔에서 가져올 수 있는 GCM 프로젝트 번호</span><span class="sxs-lookup"><span data-stu-id="a6dac-115">GCM Project number that you can obtain from your Google Developer Console for GCM</span></span>
* [<span data-ttu-id="a6dac-116">Mobile Engagement Cordova 플러그 인</span><span class="sxs-lookup"><span data-stu-id="a6dac-116">Mobile Engagement Cordova Plugin</span></span>](https://www.npmjs.com/package/cordova-plugin-ms-azure-mobile-engagement)

> [!NOTE]
> <span data-ttu-id="a6dac-117">[GitHub](https://github.com/Azure/azure-mobile-engagement-cordova)에서 Cordova 플러그 인에 대한 소스 코드와 추가 정보를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6dac-117">You can find the source code and the ReadMe for the Cordova plugin on [GitHub](https://github.com/Azure/azure-mobile-engagement-cordova)</span></span>
> 
> 

## <span data-ttu-id="a6dac-118"><a id="setup-azme"></a>Cordova 앱용 Mobile Engagement 설정</span><span class="sxs-lookup"><span data-stu-id="a6dac-118"><a id="setup-azme"></a>Setup Mobile Engagement for your Cordova app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="a6dac-119"><a id="connecting-app"></a>Mobile Engagement 백 엔드에 앱 연결</span><span class="sxs-lookup"><span data-stu-id="a6dac-119"><a id="connecting-app"></a>Connecting your app to the Mobile Engagement backend</span></span>
<span data-ttu-id="a6dac-120">이 자습서에서는 데이터를 수집하고 푸시 알림을 보내는 데 필요한 최소 집합인 "기본 통합" 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a6dac-120">This tutorial presents a "basic integration" which is the minimal set required to collect data and send a push notification.</span></span> 

<span data-ttu-id="a6dac-121">여기서는 통합을 시연하기 위해 Cordova를 사용하여 기본 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a6dac-121">We will create a basic app with Cordova to demonstrate the integration:</span></span>

### <a name="create-a-new-cordova-project"></a><span data-ttu-id="a6dac-122">새 Cordova 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="a6dac-122">Create a new Cordova project</span></span>
1. <span data-ttu-id="a6dac-123">Mac 컴퓨터에서 *Terminal* 창을 시작하고 기본 템플릿에서 새 Cordova 프로젝트를 만들 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a6dac-123">Launch *Terminal* window on your Mac machine and type the following which will create a new Cordova project from the default template.</span></span> <span data-ttu-id="a6dac-124">iOS 앱을 배포하는 데 사용할 최종 게시 프로필이 앱 ID로 'com.mycompany.myapp'을 사용하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a6dac-124">Make sure that the publishing profile you eventually use to deploy your iOS app is using 'com.mycompany.myapp' as the App ID.</span></span> 
   
        $ cordova create azme-cordova com.mycompany.myapp
        $ cd azme-cordova
2. <span data-ttu-id="a6dac-125">다음을 실행하여 **iOS** 에 대한 프로젝트를 구성하고 iOS 시뮬레이터에서 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a6dac-125">Execute the following to configure your project for **iOS** and run it in the iOS Simulator:</span></span>
   
        $ cordova platform add ios 
        $ cordova run ios
3. <span data-ttu-id="a6dac-126">다음을 실행하여 **Android**에 대한 프로젝트를 구성하고 Android 에뮬레이터에서 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a6dac-126">Execute the following to configure your project for **Android** and run it in the Android emulator.</span></span> <span data-ttu-id="a6dac-127">Android SDK 에뮬레이터 설정에서 대상이 Google API(Google Inc.)이고 CPU/ABI가 Google API ARM인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a6dac-127">Make sure that your Android SDK Emulator settings have its Target as Google APIs (Google Inc.) with the CPU / ABI as Google APIs ARM.</span></span>  
   
        $ cordova platform add android
        $ cordova run android
4. <span data-ttu-id="a6dac-128">Cordova 콘솔 플러그 인을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a6dac-128">Add the Cordova Console plugin.</span></span> 

    ```
    $ cordova plugin add cordova-plugin-console
    ``` 

### <a name="connect-your-app-to-mobile-engagement-backend"></a><span data-ttu-id="a6dac-129">Mobile Engagement 백 엔드에 앱 연결</span><span class="sxs-lookup"><span data-stu-id="a6dac-129">Connect your app to Mobile Engagement backend</span></span>
1. <span data-ttu-id="a6dac-130">변수 값을 제공하여 플러그 인을 구성하는 동안 Azure Mobile Engagement Cordova 플러그 인을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="a6dac-130">Install the Azure Mobile Engagement Cordova plugin while providing the variable values to configure the plugin:</span></span>
   
        cordova plugin add cordova-plugin-ms-azure-mobile-engagement    
             --variable AZME_IOS_CONNECTION_STRING=<iOS Connection String> 
            --variable AZME_IOS_REACH_ICON=... (icon name WITH extension) 
            --variable AZME_ANDROID_CONNECTION_STRING=<Android Connection String> 
            --variable AZME_ANDROID_REACH_ICON=... (icon name WITHOUT extension)       
            --variable AZME_ANDROID_GOOGLE_PROJECT_NUMBER=... (From your Google Cloud console for sending push notifications) 
            --variable AZME_ACTION_URL =... (URL scheme which triggers the app for deep linking)
            --variable AZME_ENABLE_NATIVE_LOG=true|false
            --variable AZME_ENABLE_PLUGIN_LOG=true|false

<span data-ttu-id="a6dac-131">*Android 도달률 아이콘* : 확장자 없고 그릴 수 있는 접두사도 없는 리소스 이름(예: mynotificationicon)이어야 하며 아이콘 파일을 사용자의 Android 프로젝트(platforms/android/res/drawable)에 복사해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6dac-131">*Android Reach Icon* : must be the name of the resource without any extension, nor drawable prefix (ex: mynotificationicon), and the icon file must be copied into your android project (platforms/android/res/drawable)</span></span>

<span data-ttu-id="a6dac-132">*iOS 도달률 아이콘*: 확장자가 있는 리소스 이름(예: mynotificationicon.png)이어야 하며 XCode를 사용하여 아이콘 파일을 사용자의 iOS 프로젝트에 추가해야 합니다(파일 추가 메뉴 사용).</span><span class="sxs-lookup"><span data-stu-id="a6dac-132">*iOS Reach Icon*  : must be the name of the resource with its extension (ex:  mynotificationicon.png), and the icon file must be added into your iOS project with XCode (using the Add Files Menu)</span></span>

## <span data-ttu-id="a6dac-133"><a id="monitor"></a>실시간 모니터링 사용</span><span class="sxs-lookup"><span data-stu-id="a6dac-133"><a id="monitor"></a>Enabling real-time monitoring</span></span>
1. <span data-ttu-id="a6dac-134">Cordova 프로젝트에서 **www/js/index.js** 를 편집하여 Mobile Engagement에 대한 호출을 추가하고 *deviceReady* 이벤트가 수신된 후 새 활동을 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="a6dac-134">In the Cordova project - edit **www/js/index.js** to add the call to Mobile Engagement to declare a new activity once the *deviceReady* event is received.</span></span>
   
         onDeviceReady: function() {
                Engagement.startActivity("myPage",{});
            }
2. <span data-ttu-id="a6dac-135">응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a6dac-135">Run the application:</span></span>
   
   * <span data-ttu-id="a6dac-136">**iOS의 경우**</span><span class="sxs-lookup"><span data-stu-id="a6dac-136">**For iOS**</span></span>
     
       <span data-ttu-id="a6dac-137">`Terminal` 창에서는 다음을 실행하여 앱을 새 시뮬레이터 인스턴스에서 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="a6dac-137">In `Terminal` window launch your app in a new Simulator instance by executing the following:</span></span>
     
           cordova run ios
   * <span data-ttu-id="a6dac-138">**Android의 경우**</span><span class="sxs-lookup"><span data-stu-id="a6dac-138">**For Android**</span></span>
     
       <span data-ttu-id="a6dac-139">`Terminal` 창에서는 다음을 실행하여 앱을 새 에뮬레이터 인스턴스에서 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="a6dac-139">In `Terminal` window launch your app in a new emulator instance by executing the following:</span></span>
     
           cordova run android
3. <span data-ttu-id="a6dac-140">콘솔 로그에서 다음을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6dac-140">You can see the following in the console logs:</span></span>
   
        [Engagement] Agent: Session started
        [Engagement] Agent: Activity 'myPage' started
        [Engagement] Connection: Established
        [Engagement] Connection: Sent: appInfo
        [Engagement] Connection: Sent: startSession
        [Engagement] Connection: Sent: activity name='myPage'

## <span data-ttu-id="a6dac-141"><a id="monitor"></a>실시간 모니터링과 앱 연결</span><span class="sxs-lookup"><span data-stu-id="a6dac-141"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="a6dac-142"><a id="integrate-push"></a>푸시 알림 및 앱 내 메시징 사용</span><span class="sxs-lookup"><span data-stu-id="a6dac-142"><a id="integrate-push"></a>Enabling Push Notifications and in-app messaging</span></span>
<span data-ttu-id="a6dac-143">Mobile Engagement에서는 캠페인 컨텍스트에서 푸시 알림 및 앱 내 메시징을 사용하여 사용자와 상호 작용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6dac-143">Mobile Engagement allows you to interact with your users using Push Notifications and in-app messaging in the context of campaigns.</span></span> <span data-ttu-id="a6dac-144">Mobile Engagement 포털에서는 이 모듈을 도달률이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6dac-144">This module is called REACH in the Mobile Engagement portal.</span></span>
<span data-ttu-id="a6dac-145">다음 섹션에서는 해당 알림과 메시지를 받도록 앱을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a6dac-145">The following sections will setup your app to receive them.</span></span>

### <a name="configure-push-credentials-for-mobile-engagement"></a><span data-ttu-id="a6dac-146">Mobile Engagement에 대한 푸시 자격 증명 구성</span><span class="sxs-lookup"><span data-stu-id="a6dac-146">Configure Push credentials for Mobile Engagement</span></span>
<span data-ttu-id="a6dac-147">사용자를 대신하여 Mobile Engagement에서 푸시 알림을 보내도록 허용하려면 Apple iOS 인증서 또는 GCM 서버 API 키에 대한 액세스 권한을 Mobile Engagement에 부여해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6dac-147">To allow Mobile Engagement to send Push Notifications on your behalf, you need to grant it access to your Apple iOS certificate or GCM Server API Key.</span></span> 

1. <span data-ttu-id="a6dac-148">Mobile Engagement 포털로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a6dac-148">Navigate to your Mobile Engagement portal.</span></span> <span data-ttu-id="a6dac-149">이 프로젝트용으로 사용 중인 앱이 열려 있는지 확인하고 맨 아래에서 **참여** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a6dac-149">Ensure you're in the app we're using for this project and then click on the **Engage** button at the bottom:</span></span>
   
    ![][1]
2. <span data-ttu-id="a6dac-150">그러면 Engagement 포털의 설정 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6dac-150">You will land in the settings page in your Engagement Portal.</span></span> <span data-ttu-id="a6dac-151">여기에서 다음과 같이 **네이티브 푸시** 섹션을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a6dac-151">From there click on the **Native Push** section:</span></span>
   
    ![][2]
3. <span data-ttu-id="a6dac-152">iOS 인증서/GCM 서버 API 키 구성</span><span class="sxs-lookup"><span data-stu-id="a6dac-152">Configure iOS Certificate/GCM Server API Key</span></span>
   
    <span data-ttu-id="a6dac-153">**[iOS]**</span><span class="sxs-lookup"><span data-stu-id="a6dac-153">**[iOS]**</span></span>
   
    <span data-ttu-id="a6dac-154">a.</span><span class="sxs-lookup"><span data-stu-id="a6dac-154">a.</span></span> <span data-ttu-id="a6dac-155">다음과 같이 .p12를 선택하여 업로드하고 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a6dac-155">Select your .p12, upload it and type your password:</span></span>
   
    ![][3]
   
    <span data-ttu-id="a6dac-156">**[Android]**</span><span class="sxs-lookup"><span data-stu-id="a6dac-156">**[Android]**</span></span>
   
    <span data-ttu-id="a6dac-157">a.</span><span class="sxs-lookup"><span data-stu-id="a6dac-157">a.</span></span> <span data-ttu-id="a6dac-158">GCM 설정 섹션 및 표시된 팝업에서 **API 키** 앞의 편집 아이콘을 클릭하고 GCM 서버 키를 붙여넣고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a6dac-158">Click the edit icon in front of **API Key** in the GCM Settings section and in the popup which shows up, paste the GCM Server Key and click **OK**.</span></span> 
   
    ![][4]

### <a name="enable-push-notifications-in-the-cordova-app"></a><span data-ttu-id="a6dac-159">Cordova 앱에서 푸시 알림을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="a6dac-159">Enable push notifications in the Cordova app</span></span>
<span data-ttu-id="a6dac-160">**www/js/index.js** 를 편집하여 푸시 알림을 요청하고 처리기를 선언하기 위한 Mobile Engagement에 대한 호출을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a6dac-160">Edit **www/js/index.js** to add the call to Mobile Engagement to request push notifications and declare a handler:</span></span>

     onDeviceReady: function() {
           Engagement.initializeReach(  
                 // on OpenUrl  
                 function(_url) {   
                 alert(_url);   
                 });  
            Engagement.startActivity("myPage",{});  
        }

### <a name="run-the-app"></a><span data-ttu-id="a6dac-161">앱 실행</span><span class="sxs-lookup"><span data-stu-id="a6dac-161">Run the app</span></span>
<span data-ttu-id="a6dac-162">**[iOS]**</span><span class="sxs-lookup"><span data-stu-id="a6dac-162">**[iOS]**</span></span>

1. <span data-ttu-id="a6dac-163">iOS에서는 실제 장치에 대한 푸시 알림만 허용하므로 XCode를 사용하여 푸시 알림을 테스트할 장치에서 앱을 빌드하고 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="a6dac-163">We will use XCode to build and deploy the app on the device to test push notifications since iOS only allows push notifications to an actual device.</span></span> <span data-ttu-id="a6dac-164">Cordova 프로젝트가 생성된 위치로 이동하고 **...\platforms\ios** 위치로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a6dac-164">Go to the location where your Cordova project is created and navigate to **...\platforms\ios** location.</span></span> <span data-ttu-id="a6dac-165">XCode에서 네이티브 .xcodeproj 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a6dac-165">Open up the native .xcodeproj file in XCode.</span></span> 
2. <span data-ttu-id="a6dac-166">방금 Mobile Engagement 포털에 업로드한 인증서가 포함된 프로비저닝 프로필이 있는 계정과 Cordova 앱을 만들 때 제공한 것과 일치하는 앱 ID를 사용하여 Cordova 앱을 빌드하고 iOS 장치에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="a6dac-166">Build and deploy the Cordova app to the iOS device using the account which has the provisioning profile containing the certificate you just uploaded to the Mobile Engagement portal and the App Id which matches the one you provided while creating the Cordova app.</span></span> <span data-ttu-id="a6dac-167">XCode의 **Resources\*-info.plist** 파일에서 *번들 식별자*가 일치하는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6dac-167">You can check out the *Bundle identifier* in your **Resources\*-info.plist** file in XCode to match it up.</span></span> 
3. <span data-ttu-id="a6dac-168">앱에서 알림을 보낼 권한을 요청함을 나타내는 표준 iOS 팝업이 장치에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6dac-168">You will see the standard iOS popup on your device saying that the app requests permission to send notifications.</span></span> <span data-ttu-id="a6dac-169">권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="a6dac-169">Grant the permission.</span></span> 

<span data-ttu-id="a6dac-170">**[Android]**</span><span class="sxs-lookup"><span data-stu-id="a6dac-170">**[Android]**</span></span>

<span data-ttu-id="a6dac-171">GCM 알림은 Android 에뮬레이터에서 지원되므로 에뮬레이터를 사용하여 Android 앱을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6dac-171">You can simply use the emulator to run the Android app as GCM notifications are supported on the Android emulator.</span></span> 

    cordova run android

## <span data-ttu-id="a6dac-172"><a id="send"></a>앱에 알림 보내기</span><span class="sxs-lookup"><span data-stu-id="a6dac-172"><a id="send"></a>Send a notification to your app</span></span>
<span data-ttu-id="a6dac-173">이제 장치에서 실행 중인 앱에 푸시를 보낼 간단한 푸시 알림 캠페인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a6dac-173">We will now create a simple Push Notification campaign that will send a push to your app running on the device:</span></span>

1. <span data-ttu-id="a6dac-174">Mobile Engagement 포털에서 **도달률** 탭으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a6dac-174">Navigate to the **Reach** tab in your Mobile Engagement portal</span></span>
2. <span data-ttu-id="a6dac-175">**새 알림** 을 클릭하여 푸시 캠페인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a6dac-175">Click **New Announcement** to create your push campaign</span></span>
   
    ![][6]
3. <span data-ttu-id="a6dac-176">입력을 제공하여 캠페인을 만듭니다. **[Android]**</span><span class="sxs-lookup"><span data-stu-id="a6dac-176">Provide inputs to create your campaign **[Android]**</span></span>
   
   * <span data-ttu-id="a6dac-177">캠페인에 **이름** 을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a6dac-177">Provide a **Name** for your campaign.</span></span> 
   * <span data-ttu-id="a6dac-178">**전달 형식**을 *시스템 알림* *단순*으로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a6dac-178">Select the **Delivery Type** as *System notification* *Simple*</span></span>
   * <span data-ttu-id="a6dac-179">**전달 시간** 을 *"언제든지"*</span><span class="sxs-lookup"><span data-stu-id="a6dac-179">Select the **Delivery time** as *"Any Time"*</span></span>
   * <span data-ttu-id="a6dac-180">푸시에서 첫째 줄에 있는 알림에 **제목** 을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a6dac-180">Provide a **Title** for your notification which will be the first line in the push.</span></span>
   * <span data-ttu-id="a6dac-181">메시지 본문으로 사용하는 알림에 **메시지** 를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a6dac-181">Provide a **Message** for your notification which will serve as the message body.</span></span> 
     
     ![][11]
4. <span data-ttu-id="a6dac-182">입력을 제공하여 캠페인을 만듭니다. **[iOS]**</span><span class="sxs-lookup"><span data-stu-id="a6dac-182">Provide inputs to create your campaign **[iOS]**</span></span>
   
   * <span data-ttu-id="a6dac-183">캠페인에 **이름** 을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a6dac-183">Provide a **Name** for your campaign.</span></span> 
   * <span data-ttu-id="a6dac-184">**전달 시간** 을*"앱 외부에서만"*</span><span class="sxs-lookup"><span data-stu-id="a6dac-184">Select the **Delivery time** as *"Out of app only"*</span></span>
   * <span data-ttu-id="a6dac-185">푸시에서 첫째 줄에 있는 알림에 **제목** 을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a6dac-185">Provide a **Title** for your notification which will be the first line in the push.</span></span>
   * <span data-ttu-id="a6dac-186">메시지 본문으로 사용하는 알림에 **메시지** 를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a6dac-186">Provide a **Message** for your notification which will serve as the message body.</span></span> 
     
     ![][12]
5. <span data-ttu-id="a6dac-187">아래로 스크롤하여 콘텐츠 섹션에서 **알림만**</span><span class="sxs-lookup"><span data-stu-id="a6dac-187">Scroll down, and in the content section select **Notification only**</span></span>
   
    ![][8]
6. <span data-ttu-id="a6dac-188">[선택 사항] 작업 URL을 제공할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6dac-188">[Optional] You can also provide an Action URL.</span></span> <span data-ttu-id="a6dac-189">플러그 인의 **AZME\_REDIRECT\_URL** 변수를 구성하는 동안 제공된 URL 체계가 사용되는지 확인합니다(예: *myapp://test*).</span><span class="sxs-lookup"><span data-stu-id="a6dac-189">Make sure that it uses a URL scheme provided while configuring the plugin's **AZME\_REDIRECT\_URL** variable e.g. *myapp://test*.</span></span>  
7. <span data-ttu-id="a6dac-190">가능한 가장 기본적인 캠페인 설정을 완료했습니다.</span><span class="sxs-lookup"><span data-stu-id="a6dac-190">You're done setting the most basic campaign possible.</span></span> <span data-ttu-id="a6dac-191">이제 다시 아래로 스크롤하고 **만들기** 단추를 클릭하여 캠페인을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="a6dac-191">Now scroll down again and click the **Create** button to save your campaign.</span></span>
8. <span data-ttu-id="a6dac-192">마지막으로 캠페인을 **활성화** 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6dac-192">Finally **Activate** your campaign</span></span>
   
    ![][10]
9. <span data-ttu-id="a6dac-193">이제 이 캠페인 부분으로 장치나 에뮬레이터에 푸시 알림이 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6dac-193">You should now see a push notification on your device or emulator as part of this campaign.</span></span> 

## <span data-ttu-id="a6dac-194"><a id="next-steps"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="a6dac-194"><a id="next-steps"></a>Next Steps</span></span>
[<span data-ttu-id="a6dac-195">Cordova Mobile Engagement SDK에서 사용 가능한 모든 방법의 개요</span><span class="sxs-lookup"><span data-stu-id="a6dac-195">Overview of all methods available with Cordova Mobile Engagement SDK</span></span>](https://github.com/Azure/azure-mobile-engagement-cordova)

<!-- Images. -->

[1]: ./media/mobile-engagement-cordova-get-started/engage-button.png
[2]: ./media/mobile-engagement-cordova-get-started/engagement-portal.png
[3]: ./media/mobile-engagement-cordova-get-started/native-push-settings.png
[4]: ./media/mobile-engagement-cordova-get-started/api-key.png
[6]: ./media/mobile-engagement-cordova-get-started/new-announcement.png
[8]: ./media/mobile-engagement-cordova-get-started/campaign-content.png
[10]: ./media/mobile-engagement-cordova-get-started/campaign-activate.png
[11]: ./media/mobile-engagement-cordova-get-started/campaign-first-params-android.png
[12]: ./media/mobile-engagement-cordova-get-started/campaign-first-params-ios.png


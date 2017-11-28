---
title: "aaaGet Cordova/Phonegap에 대 한 Azure Mobile Engagement와 시작 됨"
description: "자세한 내용은 방법 Cordova/Phonegap 앱에 대 한 분석 및 푸시 알림을 사용 하 여 Azure Mobile Engagement toouse 합니다."
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
ms.openlocfilehash: e67dabbdf7886802bb058f38964e558d5ae6854c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-cordovaphonegap"></a><span data-ttu-id="17a0b-103">Cordova/Phonegap용 Azure Mobile Engagement 시작</span><span class="sxs-lookup"><span data-stu-id="17a0b-103">Get Started with Azure Mobile Engagement for Cordova/Phonegap</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="17a0b-104">이 항목에서는 Cordova를 사용 하 여 응용 프로그램 사용과 송신 푸시 알림을 toosegmented 사용자가 모바일 응용 프로그램에 대 한 개발 toouse Azure Mobile Engagement toounderstand 합니다.</span><span class="sxs-lookup"><span data-stu-id="17a0b-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and send push notifications toosegmented users for a mobile application developed with Cordova.</span></span>

<span data-ttu-id="17a0b-105">이 자습서에서는 Mac을 사용하여 빈 Cordova 앱을 만들고 Mobile Engagement SDK를 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="17a0b-105">In this tutorial, we will create a blank Cordova app using Mac and then integrate Mobile Engagement SDK.</span></span> <span data-ttu-id="17a0b-106">기본 분석 데이터를 수집하고 iOS용 APNS(Apple 푸시 알림 시스템) 및 Android용 GCM(Google Cloud Messaging)을 사용하여 푸시 알림을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="17a0b-106">It collects basic analytics data and receives push notifications using Apple Push Notification System (APNS) for iOS and Google Cloud Messaging (GCM) for Android.</span></span> <span data-ttu-id="17a0b-107">에서는이 tooan iOS 나 Android 장치 테스트를 위한 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="17a0b-107">We will deploy this tooan iOS or Android device for testing.</span></span> 

> [!NOTE]
> <span data-ttu-id="17a0b-108">toocomplete이이 자습서에서는 활성 Azure 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17a0b-108">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="17a0b-109">계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17a0b-109">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="17a0b-110">자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-cordova-get-started)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="17a0b-110">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-cordova-get-started).</span></span>
> 
> 

<span data-ttu-id="17a0b-111">이 자습서는 hello 다음을 사항이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="17a0b-111">This tutorial requires hello following:</span></span>

* <span data-ttu-id="17a0b-112">XCode는 (tooiOS 배포용) Mac 앱 스토어에서 설치할 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="17a0b-112">XCode, which you can install from Mac App Store (for deploying tooiOS)</span></span>
* <span data-ttu-id="17a0b-113">[Android SDK 및 에뮬레이터](http://developer.android.com/sdk/installing/index.html) (tooAndroid 배포용)</span><span class="sxs-lookup"><span data-stu-id="17a0b-113">[Android SDK & Emulator](http://developer.android.com/sdk/installing/index.html) (for deploying tooAndroid)</span></span>
* <span data-ttu-id="17a0b-114">APNS을 위해 Apple 개발자 센터에서 가져올 수 있는 푸시 알림 인증서(.p12)</span><span class="sxs-lookup"><span data-stu-id="17a0b-114">Push notification certificate (.p12) that you can obtain from Apple Dev Center for APNS</span></span>
* <span data-ttu-id="17a0b-115">GCM을 위해 Google 개발자 콘솔에서 가져올 수 있는 GCM 프로젝트 번호</span><span class="sxs-lookup"><span data-stu-id="17a0b-115">GCM Project number that you can obtain from your Google Developer Console for GCM</span></span>
* [<span data-ttu-id="17a0b-116">Mobile Engagement Cordova 플러그 인</span><span class="sxs-lookup"><span data-stu-id="17a0b-116">Mobile Engagement Cordova Plugin</span></span>](https://www.npmjs.com/package/cordova-plugin-ms-azure-mobile-engagement)

> [!NOTE]
> <span data-ttu-id="17a0b-117">에 hello Cordova 플러그 인에 대 한 추가 정보를 hello와 hello 소스 코드를 찾을 수 [GitHub](https://github.com/Azure/azure-mobile-engagement-cordova)</span><span class="sxs-lookup"><span data-stu-id="17a0b-117">You can find hello source code and hello ReadMe for hello Cordova plugin on [GitHub](https://github.com/Azure/azure-mobile-engagement-cordova)</span></span>
> 
> 

## <span data-ttu-id="17a0b-118"><a id="setup-azme"></a>Cordova 앱용 Mobile Engagement 설정</span><span class="sxs-lookup"><span data-stu-id="17a0b-118"><a id="setup-azme"></a>Setup Mobile Engagement for your Cordova app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="17a0b-119"><a id="connecting-app"></a>응용 프로그램 toohello Mobile Engagement 백 엔드 연결</span><span class="sxs-lookup"><span data-stu-id="17a0b-119"><a id="connecting-app"></a>Connecting your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="17a0b-120">이 자습서에는 "기본 통합" hello 최소 필수 toocollect 데이터 설정 되 고 푸시 알림을 보내려면 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="17a0b-120">This tutorial presents a "basic integration" which is hello minimal set required toocollect data and send a push notification.</span></span> 

<span data-ttu-id="17a0b-121">Cordova toodemonstrate hello 통합 기본 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="17a0b-121">We will create a basic app with Cordova toodemonstrate hello integration:</span></span>

### <a name="create-a-new-cordova-project"></a><span data-ttu-id="17a0b-122">새 Cordova 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="17a0b-122">Create a new Cordova project</span></span>
1. <span data-ttu-id="17a0b-123">시작 *터미널* hello 기본 서식 파일에서 새 Cordova 프로젝트를 만듭니다는 뒤에 Mac 컴퓨터 및 형식 hello에 창.</span><span class="sxs-lookup"><span data-stu-id="17a0b-123">Launch *Terminal* window on your Mac machine and type hello following which will create a new Cordova project from hello default template.</span></span> <span data-ttu-id="17a0b-124">hello 게시 프로필 결국 사용 toodeploy 있는지 확인 하십시오. 앱 ID hello으로 iOS 앱 'com.mycompany.myapp'를 사용 하는</span><span class="sxs-lookup"><span data-stu-id="17a0b-124">Make sure that hello publishing profile you eventually use toodeploy your iOS app is using 'com.mycompany.myapp' as hello App ID.</span></span> 
   
        $ cordova create azme-cordova com.mycompany.myapp
        $ cd azme-cordova
2. <span data-ttu-id="17a0b-125">다음 tooconfigure hello에 대 한 프로젝트 실행 **iOS** hello iOS 시뮬레이터에서에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="17a0b-125">Execute hello following tooconfigure your project for **iOS** and run it in hello iOS Simulator:</span></span>
   
        $ cordova platform add ios 
        $ cordova run ios
3. <span data-ttu-id="17a0b-126">다음 tooconfigure hello에 대 한 프로젝트 실행 **Android** hello Android 에뮬레이터에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="17a0b-126">Execute hello following tooconfigure your project for **Android** and run it in hello Android emulator.</span></span> <span data-ttu-id="17a0b-127">Android SDK 에뮬레이터 설정을 갖도록 대상 Google Api (Google Inc.)으로 hello cpu / ABI Google Api ARM으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="17a0b-127">Make sure that your Android SDK Emulator settings have its Target as Google APIs (Google Inc.) with hello CPU / ABI as Google APIs ARM.</span></span>  
   
        $ cordova platform add android
        $ cordova run android
4. <span data-ttu-id="17a0b-128">Hello Cordova 콘솔 플러그 인을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="17a0b-128">Add hello Cordova Console plugin.</span></span> 

    ```
    $ cordova plugin add cordova-plugin-console
    ``` 

### <a name="connect-your-app-toomobile-engagement-backend"></a><span data-ttu-id="17a0b-129">응용 프로그램 tooMobile Engagement 백 엔드 연결</span><span class="sxs-lookup"><span data-stu-id="17a0b-129">Connect your app tooMobile Engagement backend</span></span>
1. <span data-ttu-id="17a0b-130">Hello 변수 값 tooconfigure hello 플러그 인을 제공 하면서 hello Azure Mobile Engagement Cordova 플러그 인을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="17a0b-130">Install hello Azure Mobile Engagement Cordova plugin while providing hello variable values tooconfigure hello plugin:</span></span>
   
        cordova plugin add cordova-plugin-ms-azure-mobile-engagement    
             --variable AZME_IOS_CONNECTION_STRING=<iOS Connection String> 
            --variable AZME_IOS_REACH_ICON=... (icon name WITH extension) 
            --variable AZME_ANDROID_CONNECTION_STRING=<Android Connection String> 
            --variable AZME_ANDROID_REACH_ICON=... (icon name WITHOUT extension)       
            --variable AZME_ANDROID_GOOGLE_PROJECT_NUMBER=... (From your Google Cloud console for sending push notifications) 
            --variable AZME_ACTION_URL =... (URL scheme which triggers hello app for deep linking)
            --variable AZME_ENABLE_NATIVE_LOG=true|false
            --variable AZME_ENABLE_PLUGIN_LOG=true|false

<span data-ttu-id="17a0b-131">*Android 도달 아이콘* : 모든 확장 프로그램 또는 그릴 수 있는 접두사 없이 hello 리소스의 hello 이름 이어야 합니다 (예: mynotificationicon), hello 아이콘 파일 (플랫폼/android/r e s/그릴) android 프로젝트에 복사 해야 하 고</span><span class="sxs-lookup"><span data-stu-id="17a0b-131">*Android Reach Icon* : must be hello name of hello resource without any extension, nor drawable prefix (ex: mynotificationicon), and hello icon file must be copied into your android project (platforms/android/res/drawable)</span></span>

<span data-ttu-id="17a0b-132">*iOS 도달 아이콘* : 확장명과 hello 리소스의 hello 이름 이어야 합니다 (예: mynotificationicon.png), hello 아이콘 파일 (hello 추가 파일 메뉴 사용) 하는 xcode iOS 프로젝트에 추가 되어야 합니다</span><span class="sxs-lookup"><span data-stu-id="17a0b-132">*iOS Reach Icon*  : must be hello name of hello resource with its extension (ex:  mynotificationicon.png), and hello icon file must be added into your iOS project with XCode (using hello Add Files Menu)</span></span>

## <span data-ttu-id="17a0b-133"><a id="monitor"></a>실시간 모니터링 사용</span><span class="sxs-lookup"><span data-stu-id="17a0b-133"><a id="monitor"></a>Enabling real-time monitoring</span></span>
1. <span data-ttu-id="17a0b-134">Hello Cordova 프로젝트-에서 편집 **www/js/index.js** tooMobile Engagement toodeclare 새 활동을 한 번 hello tooadd hello 호출 *deviceReady* 이벤트가 수신 됩니다.</span><span class="sxs-lookup"><span data-stu-id="17a0b-134">In hello Cordova project - edit **www/js/index.js** tooadd hello call tooMobile Engagement toodeclare a new activity once hello *deviceReady* event is received.</span></span>
   
         onDeviceReady: function() {
                Engagement.startActivity("myPage",{});
            }
2. <span data-ttu-id="17a0b-135">Hello 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="17a0b-135">Run hello application:</span></span>
   
   * <span data-ttu-id="17a0b-136">**iOS의 경우**</span><span class="sxs-lookup"><span data-stu-id="17a0b-136">**For iOS**</span></span>
     
       <span data-ttu-id="17a0b-137">`Terminal` 창이 hello 다음을 실행 하 여 새 시뮬레이터 인스턴스에서 응용 프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="17a0b-137">In `Terminal` window launch your app in a new Simulator instance by executing hello following:</span></span>
     
           cordova run ios
   * <span data-ttu-id="17a0b-138">**Android의 경우**</span><span class="sxs-lookup"><span data-stu-id="17a0b-138">**For Android**</span></span>
     
       <span data-ttu-id="17a0b-139">`Terminal` 창이 hello 다음을 실행 하 여 새 에뮬레이터 인스턴스에서 응용 프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="17a0b-139">In `Terminal` window launch your app in a new emulator instance by executing hello following:</span></span>
     
           cordova run android
3. <span data-ttu-id="17a0b-140">Hello 다음 hello 콘솔 로그에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17a0b-140">You can see hello following in hello console logs:</span></span>
   
        [Engagement] Agent: Session started
        [Engagement] Agent: Activity 'myPage' started
        [Engagement] Connection: Established
        [Engagement] Connection: Sent: appInfo
        [Engagement] Connection: Sent: startSession
        [Engagement] Connection: Sent: activity name='myPage'

## <span data-ttu-id="17a0b-141"><a id="monitor"></a>실시간 모니터링과 앱 연결</span><span class="sxs-lookup"><span data-stu-id="17a0b-141"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="17a0b-142"><a id="integrate-push"></a>푸시 알림 및 앱 내 메시징 사용</span><span class="sxs-lookup"><span data-stu-id="17a0b-142"><a id="integrate-push"></a>Enabling Push Notifications and in-app messaging</span></span>
<span data-ttu-id="17a0b-143">Mobile Engagement 푸시 알림과 앱 내 메시징을 캠페인의 hello 컨텍스트에서 사용 하 여 사용자와 toointeract를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="17a0b-143">Mobile Engagement allows you toointeract with your users using Push Notifications and in-app messaging in hello context of campaigns.</span></span> <span data-ttu-id="17a0b-144">이 모듈에는 hello Mobile engagement 연결 포털에서 REACH를 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="17a0b-144">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="17a0b-145">hello 다음 섹션에서는 설치 응용 프로그램 tooreceive 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="17a0b-145">hello following sections will setup your app tooreceive them.</span></span>

### <a name="configure-push-credentials-for-mobile-engagement"></a><span data-ttu-id="17a0b-146">Mobile Engagement에 대한 푸시 자격 증명 구성</span><span class="sxs-lookup"><span data-stu-id="17a0b-146">Configure Push credentials for Mobile Engagement</span></span>
<span data-ttu-id="17a0b-147">사용자 대신 tooallow Mobile Engagement toosend 푸시 알림을, toogrant tooyour Apple iOS 인증서 또는 GCM 서버 API 키에 액세스 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17a0b-147">tooallow Mobile Engagement toosend Push Notifications on your behalf, you need toogrant it access tooyour Apple iOS certificate or GCM Server API Key.</span></span> 

1. <span data-ttu-id="17a0b-148">Mobile engagement 연결 포털 tooyour 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="17a0b-148">Navigate tooyour Mobile Engagement portal.</span></span> <span data-ttu-id="17a0b-149">Hello 앱에서는이 프로젝트에 대 한 사용 중이 고 hello에서 클릭 한 다음에 있는 확인 **사로잡는 구성** hello 아래쪽 단추:</span><span class="sxs-lookup"><span data-stu-id="17a0b-149">Ensure you're in hello app we're using for this project and then click on hello **Engage** button at hello bottom:</span></span>
   
    ![][1]
2. <span data-ttu-id="17a0b-150">Engagement 연결 포털에서 hello 설정 페이지에 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="17a0b-150">You will land in hello settings page in your Engagement Portal.</span></span> <span data-ttu-id="17a0b-151">Hello 없어 클릭에서 **하 여 네이티브 푸시** 섹션:</span><span class="sxs-lookup"><span data-stu-id="17a0b-151">From there click on hello **Native Push** section:</span></span>
   
    ![][2]
3. <span data-ttu-id="17a0b-152">iOS 인증서/GCM 서버 API 키 구성</span><span class="sxs-lookup"><span data-stu-id="17a0b-152">Configure iOS Certificate/GCM Server API Key</span></span>
   
    <span data-ttu-id="17a0b-153">**[iOS]**</span><span class="sxs-lookup"><span data-stu-id="17a0b-153">**[iOS]**</span></span>
   
    <span data-ttu-id="17a0b-154">a.</span><span class="sxs-lookup"><span data-stu-id="17a0b-154">a.</span></span> <span data-ttu-id="17a0b-155">다음과 같이 .p12를 선택하여 업로드하고 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="17a0b-155">Select your .p12, upload it and type your password:</span></span>
   
    ![][3]
   
    <span data-ttu-id="17a0b-156">**[Android]**</span><span class="sxs-lookup"><span data-stu-id="17a0b-156">**[Android]**</span></span>
   
    <span data-ttu-id="17a0b-157">a.</span><span class="sxs-lookup"><span data-stu-id="17a0b-157">a.</span></span> <span data-ttu-id="17a0b-158">앞의 hello 편집 아이콘을 클릭 **API 키** hello GCM 설정 섹션 및 참석 hello 팝업 hello GCM 서버 키를 붙여 넣고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="17a0b-158">Click hello edit icon in front of **API Key** in hello GCM Settings section and in hello popup which shows up, paste hello GCM Server Key and click **OK**.</span></span> 
   
    ![][4]

### <a name="enable-push-notifications-in-hello-cordova-app"></a><span data-ttu-id="17a0b-159">Hello Cordova 앱에 푸시 알림을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="17a0b-159">Enable push notifications in hello Cordova app</span></span>
<span data-ttu-id="17a0b-160">편집 **www/js/index.js** tooadd hello 호출 tooMobile Engagement toorequest 푸시 알림 및 처리기를 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="17a0b-160">Edit **www/js/index.js** tooadd hello call tooMobile Engagement toorequest push notifications and declare a handler:</span></span>

     onDeviceReady: function() {
           Engagement.initializeReach(  
                 // on OpenUrl  
                 function(_url) {   
                 alert(_url);   
                 });  
            Engagement.startActivity("myPage",{});  
        }

### <a name="run-hello-app"></a><span data-ttu-id="17a0b-161">Hello 앱 실행</span><span class="sxs-lookup"><span data-stu-id="17a0b-161">Run hello app</span></span>
<span data-ttu-id="17a0b-162">**[iOS]**</span><span class="sxs-lookup"><span data-stu-id="17a0b-162">**[iOS]**</span></span>

1. <span data-ttu-id="17a0b-163">XCode toobuild를 사용 하 고 iOS에만 푸시 알림을 tooan 실제 장치에서는 있으므로 hello 장치 tootest 푸시 알림에 hello 앱을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="17a0b-163">We will use XCode toobuild and deploy hello app on hello device tootest push notifications since iOS only allows push notifications tooan actual device.</span></span> <span data-ttu-id="17a0b-164">Cordova 프로젝트를 만들 위치 toohello 위치를 이동 하 고 탐색 너무**...\platforms\ios** 위치 합니다.</span><span class="sxs-lookup"><span data-stu-id="17a0b-164">Go toohello location where your Cordova project is created and navigate too**...\platforms\ios** location.</span></span> <span data-ttu-id="17a0b-165">XCode에서 hello 네이티브.xcodeproj 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="17a0b-165">Open up hello native .xcodeproj file in XCode.</span></span> 
2. <span data-ttu-id="17a0b-166">빌드 및 프로비저닝 프로필 toohello Mobile engagement 연결 포털 및 앱 Id를 만드는 동안 제공한 hello에 일치 하는 hello 업로드 hello 인증서가 포함 된 hello 있는 hello 계정을 사용 하 여 hello Cordova 앱 toohello iOS 장치를 배포 합니다. hello Cordova 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="17a0b-166">Build and deploy hello Cordova app toohello iOS device using hello account which has hello provisioning profile containing hello certificate you just uploaded toohello Mobile Engagement portal and hello App Id which matches hello one you provided while creating hello Cordova app.</span></span> <span data-ttu-id="17a0b-167">Hello 확인할 수 있습니다 *번들 식별자* 에 프로그램 **리소스\*-info.plist** 파일 XCode toomatch 것을 합니다.</span><span class="sxs-lookup"><span data-stu-id="17a0b-167">You can check out hello *Bundle identifier* in your **Resources\*-info.plist** file in XCode toomatch it up.</span></span> 
3. <span data-ttu-id="17a0b-168">권한 toosend 알림을 요청 하는 hello 표준 iOS 팝업 hello 앱 라는 장치에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17a0b-168">You will see hello standard iOS popup on your device saying that hello app requests permission toosend notifications.</span></span> <span data-ttu-id="17a0b-169">Hello 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="17a0b-169">Grant hello permission.</span></span> 

<span data-ttu-id="17a0b-170">**[Android]**</span><span class="sxs-lookup"><span data-stu-id="17a0b-170">**[Android]**</span></span>

<span data-ttu-id="17a0b-171">GCM 알림을 hello Android 에뮬레이터에서 지원 되는 단순히 hello 에뮬레이터 toorun hello Android 앱을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17a0b-171">You can simply use hello emulator toorun hello Android app as GCM notifications are supported on hello Android emulator.</span></span> 

    cordova run android

## <span data-ttu-id="17a0b-172"><a id="send"></a>보낼 알림 tooyour 앱</span><span class="sxs-lookup"><span data-stu-id="17a0b-172"><a id="send"></a>Send a notification tooyour app</span></span>
<span data-ttu-id="17a0b-173">이제 단순한 푸시 알림을 캠페인의 hello 장치에서 실행 되는 푸시 tooyour 앱 보낼 사항을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="17a0b-173">We will now create a simple Push Notification campaign that will send a push tooyour app running on hello device:</span></span>

1. <span data-ttu-id="17a0b-174">Toohello 이동 **도달** Mobile engagement 연결 포털에서 탭</span><span class="sxs-lookup"><span data-stu-id="17a0b-174">Navigate toohello **Reach** tab in your Mobile Engagement portal</span></span>
2. <span data-ttu-id="17a0b-175">클릭 **새 공지** toocreate 푸시 캠페인</span><span class="sxs-lookup"><span data-stu-id="17a0b-175">Click **New Announcement** toocreate your push campaign</span></span>
   
    ![][6]
3. <span data-ttu-id="17a0b-176">입력 toocreate 캠페인 제공 **[Android]**</span><span class="sxs-lookup"><span data-stu-id="17a0b-176">Provide inputs toocreate your campaign **[Android]**</span></span>
   
   * <span data-ttu-id="17a0b-177">캠페인에 **이름** 을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="17a0b-177">Provide a **Name** for your campaign.</span></span> 
   * <span data-ttu-id="17a0b-178">선택 hello **배달 유형** 으로 *시스템 알림* *단순*</span><span class="sxs-lookup"><span data-stu-id="17a0b-178">Select hello **Delivery Type** as *System notification* *Simple*</span></span>
   * <span data-ttu-id="17a0b-179">선택 hello **배달 시간** 으로 *"Any 시간"*</span><span class="sxs-lookup"><span data-stu-id="17a0b-179">Select hello **Delivery time** as *"Any Time"*</span></span>
   * <span data-ttu-id="17a0b-180">제공 된 **제목** hello 푸시에서 첫 번째 줄 hello 될 알림에 합니다.</span><span class="sxs-lookup"><span data-stu-id="17a0b-180">Provide a **Title** for your notification which will be hello first line in hello push.</span></span>
   * <span data-ttu-id="17a0b-181">제공 된 **메시지** hello 메시지 본문으로 사용할 알림에 합니다.</span><span class="sxs-lookup"><span data-stu-id="17a0b-181">Provide a **Message** for your notification which will serve as hello message body.</span></span> 
     
     ![][11]
4. <span data-ttu-id="17a0b-182">입력 toocreate 캠페인 제공 **[iOS]**</span><span class="sxs-lookup"><span data-stu-id="17a0b-182">Provide inputs toocreate your campaign **[iOS]**</span></span>
   
   * <span data-ttu-id="17a0b-183">캠페인에 **이름** 을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="17a0b-183">Provide a **Name** for your campaign.</span></span> 
   * <span data-ttu-id="17a0b-184">선택 hello **배달 시간** 으로 *"app" 부족*</span><span class="sxs-lookup"><span data-stu-id="17a0b-184">Select hello **Delivery time** as *"Out of app only"*</span></span>
   * <span data-ttu-id="17a0b-185">제공 된 **제목** hello 푸시에서 첫 번째 줄 hello 될 알림에 합니다.</span><span class="sxs-lookup"><span data-stu-id="17a0b-185">Provide a **Title** for your notification which will be hello first line in hello push.</span></span>
   * <span data-ttu-id="17a0b-186">제공 된 **메시지** hello 메시지 본문으로 사용할 알림에 합니다.</span><span class="sxs-lookup"><span data-stu-id="17a0b-186">Provide a **Message** for your notification which will serve as hello message body.</span></span> 
     
     ![][12]
5. <span data-ttu-id="17a0b-187">Hello에서 콘텐츠 섹션을 선택 하 고 아래로 스크롤하여 **알림 전용**</span><span class="sxs-lookup"><span data-stu-id="17a0b-187">Scroll down, and in hello content section select **Notification only**</span></span>
   
    ![][8]
6. <span data-ttu-id="17a0b-188">[선택 사항] 작업 URL을 제공할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17a0b-188">[Optional] You can also provide an Action URL.</span></span> <span data-ttu-id="17a0b-189">Hello 플러그 인을 구성 하는 동안 제공 된 URL 체계를 사용 하는지 확인 **AZME\_리디렉션\_URL** 변수 예: *myapp://test*합니다.</span><span class="sxs-lookup"><span data-stu-id="17a0b-189">Make sure that it uses a URL scheme provided while configuring hello plugin's **AZME\_REDIRECT\_URL** variable e.g. *myapp://test*.</span></span>  
7. <span data-ttu-id="17a0b-190">설정을 hello 가장 기본적인 캠페인 가능한 작업이 끝났습니다.</span><span class="sxs-lookup"><span data-stu-id="17a0b-190">You're done setting hello most basic campaign possible.</span></span> <span data-ttu-id="17a0b-191">이제 다시 아래로 스크롤하여 하 고 hello 클릭 **만들기** toosave 캠페인 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="17a0b-191">Now scroll down again and click hello **Create** button toosave your campaign.</span></span>
8. <span data-ttu-id="17a0b-192">마지막으로 캠페인을 **활성화** 합니다.</span><span class="sxs-lookup"><span data-stu-id="17a0b-192">Finally **Activate** your campaign</span></span>
   
    ![][10]
9. <span data-ttu-id="17a0b-193">이제 이 캠페인 부분으로 장치나 에뮬레이터에 푸시 알림이 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17a0b-193">You should now see a push notification on your device or emulator as part of this campaign.</span></span> 

## <span data-ttu-id="17a0b-194"><a id="next-steps"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="17a0b-194"><a id="next-steps"></a>Next Steps</span></span>
[<span data-ttu-id="17a0b-195">Cordova Mobile Engagement SDK에서 사용 가능한 모든 방법의 개요</span><span class="sxs-lookup"><span data-stu-id="17a0b-195">Overview of all methods available with Cordova Mobile Engagement SDK</span></span>](https://github.com/Azure/azure-mobile-engagement-cordova)

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


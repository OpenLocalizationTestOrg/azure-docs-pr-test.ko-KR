---
title: "Azure 모바일 앱으로 Cordova 앱 aaaAdd 푸시 알림을 tooApache | Microsoft Docs"
description: "Azure 모바일 앱 toosend toouse 밀어넣기 알림 tooyour Apache Cordova 앱에 알아봅니다."
services: app-service\mobile
documentationcenter: javascript
manager: syntaxc4
editor: 
author: ggailey777
ms.assetid: 92c596a9-875c-4840-b0e1-69198817576f
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 8e1b23d6145b446b6f01599337b677e2f2b31d7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-apache-cordova-app"></a><span data-ttu-id="a98f7-103">푸시 알림 tooyour Apache Cordova 앱 추가</span><span class="sxs-lookup"><span data-stu-id="a98f7-103">Add push notifications tooyour Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="a98f7-104">개요</span><span class="sxs-lookup"><span data-stu-id="a98f7-104">Overview</span></span>
<span data-ttu-id="a98f7-105">이 자습서에서는 레코드가 삽입 될 때마다 푸시 알림을 toohello 장치가 전송 되도록 푸시 알림을 toohello [Apache Cordova 퀵 스타트] 프로젝트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-105">In this tutorial, you add push notifications toohello [Apache Cordova quick start] project so that a push notification is sent toohello device every time a record is inserted.</span></span>

<span data-ttu-id="a98f7-106">사용 하지 않는 경우 hello 퀵 스타트 서버 프로젝트를 다운로드, 푸시 알림 확장 패키지 hello 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-106">If you do not use hello downloaded quick start server project, you need hello push notification extension package.</span></span> <span data-ttu-id="a98f7-107">자세한 내용은 참조 [Azure 모바일 앱에 대 한 hello.NET 백 엔드 서버 SDK에서 작동][1]합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-107">For more information, see [Work with hello .NET backend server SDK for Azure Mobile Apps][1].</span></span>

## <span data-ttu-id="a98f7-108"><a name="prerequisites"></a>필수 조건</span><span class="sxs-lookup"><span data-stu-id="a98f7-108"><a name="prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="a98f7-109">이 자습서에서는 Google Android 에뮬레이터 hello, Android 장치, Windows 장치 및 iOS 장치에서 실행 되는 Visual Studio 2015를 사용 하 여 개발 하는 Apache Cordova 응용 프로그램에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-109">This tutorial covers an Apache Cordova application developed with Visual Studio 2015 that runs on hello Google Android Emulator, an Android device, a Windows device, and an iOS device.</span></span>

<span data-ttu-id="a98f7-110">toocomplete 해야이 자습서에서는:</span><span class="sxs-lookup"><span data-stu-id="a98f7-110">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="a98f7-111">[Visual Studio Community 2015][2] 이상이 설치된 PC</span><span class="sxs-lookup"><span data-stu-id="a98f7-111">A PC with [Visual Studio Community 2015][2] or later versions.</span></span>
* <span data-ttu-id="a98f7-112">[Visual Studio Tools for Apache Cordova][4]</span><span class="sxs-lookup"><span data-stu-id="a98f7-112">[Visual Studio Tools for Apache Cordova][4].</span></span>
* <span data-ttu-id="a98f7-113">[활성 Azure 계정][3]</span><span class="sxs-lookup"><span data-stu-id="a98f7-113">An [active Azure account][3].</span></span>
* <span data-ttu-id="a98f7-114">완료된 [Apache Cordova 빠른 시작][5] 프로젝트</span><span class="sxs-lookup"><span data-stu-id="a98f7-114">A completed [Apache Cordova quick start][5] project.</span></span>
* <span data-ttu-id="a98f7-115">(Android)검증된 메일 주소를 사용하는 [Google 계정][6]</span><span class="sxs-lookup"><span data-stu-id="a98f7-115">(Android) A [Google account][6] with a verified email address.</span></span>
* <span data-ttu-id="a98f7-116">(iOS)[Apple 개발자 프로그램 멤버 자격][7] 및 iOS 장치(iOS 시뮬레이터는 푸시를 지원하지 않음)</span><span class="sxs-lookup"><span data-stu-id="a98f7-116">(iOS) An [Apple Developer Program membership][7] and an iOS device (iOS Simulator does not support push).</span></span>
* <span data-ttu-id="a98f7-117">(Windows)[Windows 스토어 개발자 계정][8] 및 Windows 10 장치</span><span class="sxs-lookup"><span data-stu-id="a98f7-117">(Windows) A [Windows Store Developer Account][8] and a Windows 10 device.</span></span>

## <span data-ttu-id="a98f7-118"><a name="configure-hub"></a>알림 허브 구성</span><span class="sxs-lookup"><span data-stu-id="a98f7-118"><a name="configure-hub"></a>Configure a notification hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

<span data-ttu-id="a98f7-119">[이 섹션의 단계를 보여 주는 비디오 시청][9]</span><span class="sxs-lookup"><span data-stu-id="a98f7-119">[Watch a video showing steps in this section][9]</span></span>

## <a name="update-hello-server-project"></a><span data-ttu-id="a98f7-120">Hello 서버 프로젝트를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-120">Update hello server project</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <span data-ttu-id="a98f7-121"><a name="add-push-to-app"></a>Cordova 앱 수정</span><span class="sxs-lookup"><span data-stu-id="a98f7-121"><a name="add-push-to-app"></a>Modify your Cordova app</span></span>
<span data-ttu-id="a98f7-122">Apache Cordova 응용 프로그램 프로젝트 준비 toohandle 푸시 알림을 hello Cordova 푸시 플러그 인 설치와 모든 플랫폼별 푸시 서비스를 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="a98f7-122">Ensure your Apache Cordova app project is ready toohandle push notifications by installing hello Cordova push plugin plus any platform-specific push services.</span></span>

#### <a name="update-hello-cordova-version-in-your-project"></a><span data-ttu-id="a98f7-123">프로젝트의 hello Cordova 버전을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-123">Update hello Cordova version in your project.</span></span>
<span data-ttu-id="a98f7-124">프로젝트에서 v6.1.1 이전 버전의 Apache Cordova를 사용 하는 경우 hello 클라이언트 프로젝트를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-124">If your project uses a version of Apache Cordova earlier than v6.1.1, update hello client project.</span></span> <span data-ttu-id="a98f7-125">tooupdate hello 프로젝트:</span><span class="sxs-lookup"><span data-stu-id="a98f7-125">tooupdate hello project:</span></span>

* <span data-ttu-id="a98f7-126">마우스 오른쪽 단추로 클릭 `config.xml` tooopen hello 구성 디자이너입니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-126">Right-click `config.xml` tooopen hello configuration designer.</span></span>
* <span data-ttu-id="a98f7-127">Hello 플랫폼 탭을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-127">Select hello Platforms tab.</span></span>
* <span data-ttu-id="a98f7-128">Hello에 6.1.1 선택 **Cordova CLI** 입력란.</span><span class="sxs-lookup"><span data-stu-id="a98f7-128">Choose 6.1.1 in hello **Cordova CLI** text box.</span></span>
* <span data-ttu-id="a98f7-129">선택 **빌드**, 다음 **솔루션 빌드** tooupdate hello 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="a98f7-129">Choose **Build**, then **Build Solution** tooupdate hello project.</span></span>

#### <a name="install-hello-push-plugin"></a><span data-ttu-id="a98f7-130">Hello 푸시 플러그 인 설치</span><span class="sxs-lookup"><span data-stu-id="a98f7-130">Install hello push plugin</span></span>
<span data-ttu-id="a98f7-131">Apache Cordova 응용 프로그램에서는 기본적으로 장치 또는 네트워크 기능을 처리하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-131">Apache Cordova applications do not natively handle device or network capabilities.</span></span>  <span data-ttu-id="a98f7-132">이러한 기능은 [npm][10] 또는 GitHub에 게시된 플러그 인에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-132">These capabilities are provided by plugins that are published either on [npm][10] or on GitHub.</span></span>  <span data-ttu-id="a98f7-133">hello `phonegap-plugin-push` 플러그 인을 사용 하는 toohandle 네트워크 푸시 알림을 합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-133">hello `phonegap-plugin-push` plugin is used toohandle network push notifications.</span></span>

<span data-ttu-id="a98f7-134">다음이 방법 중 하나에 hello 푸시 플러그 인을 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-134">You can install hello push plugin in one of these ways:</span></span>

<span data-ttu-id="a98f7-135">**명령 프롬프트를 hello:**</span><span class="sxs-lookup"><span data-stu-id="a98f7-135">**From hello command-prompt:**</span></span>

<span data-ttu-id="a98f7-136">Hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-136">Execute hello following command:</span></span>

    cordova plugin add phonegap-plugin-push

<span data-ttu-id="a98f7-137">**Visual Studio 내에서**</span><span class="sxs-lookup"><span data-stu-id="a98f7-137">**From within Visual Studio:**</span></span>

1. <span data-ttu-id="a98f7-138">Hello를 열고 솔루션 탐색기에서 `config.xml` 파일 클릭 **플러그 인** > **사용자 지정**선택, **Git** 설치 원본으로 다음입력`https://github.com/phonegap/phonegap-plugin-push`hello 소스로 합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-138">In Solution Explorer, open hello `config.xml` file click **Plugins** > **Custom**, select **Git** as the  installation source, then enter `https://github.com/phonegap/phonegap-plugin-push` as hello source.</span></span>

   ![][img1]

2. <span data-ttu-id="a98f7-139">Hello 화살표 다음 toohello 설치 원본을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-139">Click hello arrow next toohello installation source.</span></span>
3. <span data-ttu-id="a98f7-140">**SENDER_ID**, hello Google 개발자 콘솔 프로젝트에 대 한 숫자 프로젝트 ID를 이미 있는 경우 하면 여기에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-140">In **SENDER_ID**, if you already have a numeric project ID for hello Google Developer Console project, you can add it here.</span></span> <span data-ttu-id="a98f7-141">그렇지 않으면 자리 표시자 값(예: 777777)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-141">Otherwise, enter a placeholder value, like 777777.</span></span>  <span data-ttu-id="a98f7-142">Android를 대상으로 하는 경우 나중에 config.xml에서 이 값을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-142">If you are targeting Android, you can update this value in config.xml later.</span></span>
4. <span data-ttu-id="a98f7-143">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-143">Click **Add**.</span></span>

<span data-ttu-id="a98f7-144">hello 푸시 플러그 인이 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-144">hello push plugin is now installed.</span></span>

#### <a name="install-hello-device-plugin"></a><span data-ttu-id="a98f7-145">Hello 장치 플러그 인 설치</span><span class="sxs-lookup"><span data-stu-id="a98f7-145">Install hello device plugin</span></span>
<span data-ttu-id="a98f7-146">다음과 같은 hello tooinstall hello 푸시 플러그 인을 사용 하는 프로시저입니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-146">Follow hello same procedure you used tooinstall hello push plugin.</span></span>  <span data-ttu-id="a98f7-147">Hello 핵심 플러그 인 목록에서 hello 장치 플러그 인을 추가 (클릭 **플러그 인** > **코어** toofind 것).</span><span class="sxs-lookup"><span data-stu-id="a98f7-147">Add hello Device plugin from hello Core plugins list (click **Plugins** > **Core** toofind it).</span></span> <span data-ttu-id="a98f7-148">이 플러그 인 tooobtain hello 플랫폼 이름이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-148">You need this plugin tooobtain hello platform name.</span></span>

#### <a name="register-your-device-on-application-start-up"></a><span data-ttu-id="a98f7-149">응용 프로그램 시작 시 장치 등록</span><span class="sxs-lookup"><span data-stu-id="a98f7-149">Register your device on application start-up</span></span>
<span data-ttu-id="a98f7-150">처음에 Android에 대한 최소한의 코드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-150">Initially, we include some minimal code for Android.</span></span> <span data-ttu-id="a98f7-151">나중에 iOS 또는 Windows 10 앱 toorun hello를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-151">Later, modify hello app toorun on iOS or Windows 10.</span></span>

1. <span data-ttu-id="a98f7-152">호출을 너무 추가**registerForPushNotifications** hello hello 맨 아래에 또는 hello 로그인 프로세스에 대 한 hello 콜백 하는 동안 **onDeviceReady** 메서드:</span><span class="sxs-lookup"><span data-stu-id="a98f7-152">Add a call too**registerForPushNotifications** during hello callback for hello login process, or at hello bottom of  hello **onDeviceReady** method:</span></span>

        // Login toohello service.
        client.login('google')
            .then(function () {
                // Create a table reference
                todoItemTable = client.getTable('todoitem');

                // Refresh hello todoItems
                refreshDisplay();

                // Wire up hello UI Event Handler for hello Add Item
                $('#add-item').submit(addItemHandler);
                $('#refresh').on('click', refreshDisplay);

                    // Added tooregister for push notifications.
                registerForPushNotifications();

            }, handleError);

    <span data-ttu-id="a98f7-153">이 예제에서는 인증 성공 후에 **registerForPushNotifications**를 호출하는 경우를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-153">This example shows calling **registerForPushNotifications** after authentication succeeds.</span></span>  <span data-ttu-id="a98f7-154">필요한 만큼 자주 `registerForPushNotifications()`를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-154">You can call `registerForPushNotifications()` as often as is required.</span></span>

2. <span data-ttu-id="a98f7-155">새 hello 추가 **registerForPushNotifications** 메서드를 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-155">Add hello new **registerForPushNotifications** method as follows:</span></span>

        // Register for Push Notifications. Requires that phonegap-plugin-push be installed.
        var pushRegistration = null;
        function registerForPushNotifications() {
          pushRegistration = PushNotification.init({
              android: { senderID: 'Your_Project_ID' },
              ios: { alert: 'true', badge: 'true', sound: 'true' },
              wns: {}
          });

        // Handle hello registration event.
        pushRegistration.on('registration', function (data) {
          // Get hello native platform of hello device.
          var platform = device.platform;
          // Get hello handle returned during registration.
          var handle = data.registrationId;
          // Set hello device-specific message template.
          if (platform == 'android' || platform == 'Android') {
              // Register for GCM notifications.
              client.push.register('gcm', handle, {
                  mytemplate: { body: { data: { message: "{$(messageParam)}" } } }
              });
          } else if (device.platform === 'iOS') {
              // Register for notifications.
              client.push.register('apns', handle, {
                  mytemplate: { body: { aps: { alert: "{$(messageParam)}" } } }
              });
          } else if (device.platform === 'windows') {
              // Register for WNS notifications.
              client.push.register('wns', handle, {
                  myTemplate: {
                      body: '<toast><visual><binding template="ToastText01"><text id="1">$(messageParam)</text></binding></visual></toast>',
                      headers: { 'X-WNS-Type': 'wns/toast' } }
              });
          }
        });

        pushRegistration.on('notification', function (data, d2) {
          alert('Push Received: ' + data.message);
        });

        pushRegistration.on('error', handleError);
        }
3. <span data-ttu-id="a98f7-156">(Android) Hello 코드 앞에, 바꿉니다 `Your_Project_ID` 된 hello 숫자 프로젝트에서 응용 프로그램에 대 한 ID는 [Google 개발자 콘솔][18]합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-156">(Android) In hello preceding code, replace `Your_Project_ID` with hello numeric project ID for your app from the  [Google Developer Console][18].</span></span>

## <a name="optional-configure-and-run-hello-app-on-android"></a><span data-ttu-id="a98f7-157">(선택 사항) 구성 하 고 hello 앱을 Android에서 실행</span><span class="sxs-lookup"><span data-stu-id="a98f7-157">(Optional) Configure and run hello app on Android</span></span>
<span data-ttu-id="a98f7-158">Android에 대 한이 섹션 tooenable 푸시 알림을 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-158">Complete this section tooenable push notifications for Android.</span></span>

#### <span data-ttu-id="a98f7-159"><a name="enable-gcm"></a>Firebase Cloud Messaging 사용</span><span class="sxs-lookup"><span data-stu-id="a98f7-159"><a name="enable-gcm"></a>Enable Firebase Cloud Messaging</span></span>
<span data-ttu-id="a98f7-160">대상으로 hello Google Android 플랫폼 처음, 이후 Firebase Cloud Messaging 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-160">Since we are targeting hello Google Android platform initially, you must enable Firebase Cloud Messaging.</span></span>

[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

#### <span data-ttu-id="a98f7-161"><a name="configure-backend"></a>FCM를 사용 하 여 hello 모바일 앱 백 엔드 toosend 푸시 요청 구성</span><span class="sxs-lookup"><span data-stu-id="a98f7-161"><a name="configure-backend"></a>Configure hello Mobile App backend toosend push requests using FCM</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push.md)]

#### <a name="configure-your-cordova-app-for-android"></a><span data-ttu-id="a98f7-162">Android용 Cordova 앱 구성</span><span class="sxs-lookup"><span data-stu-id="a98f7-162">Configure your Cordova app for Android</span></span>
<span data-ttu-id="a98f7-163">Cordova 앱에서 config.xml 열고 대체 `Your_Project_ID` hello에서 응용 프로그램에 대 한 프로젝트 ID 된 hello 숫자 [Google 개발자 콘솔][18]합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-163">In your Cordova app, open config.xml and replace `Your_Project_ID` with hello numeric project ID for your app from hello [Google Developer Console][18].</span></span>

        <plugin name="phonegap-plugin-push" version="1.7.1" src="https://github.com/phonegap/phonegap-plugin-push.git">
            <variable name="SENDER_ID" value="Your_Project_ID" />
        </plugin>

<span data-ttu-id="a98f7-164">Index.js를 열고 업데이트 hello 코드 toouse 프로그램 숫자 프로젝트 id입니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-164">Open index.js and update hello code toouse your numeric project ID.</span></span>

        pushRegistration = PushNotification.init({
            android: { senderID: 'Your_Project_ID' },
            ios: { alert: 'true', badge: 'true', sound: 'true' },
            wns: {}
        });

#### <span data-ttu-id="a98f7-165"><a name="configure-device"></a>USB 디버깅을 위해 Android 장치 구성</span><span class="sxs-lookup"><span data-stu-id="a98f7-165"><a name="configure-device"></a>Configure your Android device for USB debugging</span></span>
<span data-ttu-id="a98f7-166">사용자 응용 프로그램 tooyour Android 장치를 배포 하기 전에 tooenable USB 디버깅 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-166">Before you can deploy your application tooyour Android Device, you need tooenable USB Debugging.</span></span>  <span data-ttu-id="a98f7-167">Android 휴대폰에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-167">Perform the following steps on your Android phone:</span></span>

1. <span data-ttu-id="a98f7-168">너무 이동**설정** > **전화에 대 한**, hello를 탭 합니다 **빌드 번호** 개발자 모드 (약 7 번)에 사용 될 때까지 합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-168">Go too**Settings** > **About phone**, then tap hello **Build number** until developer mode is enabled  (about seven times).</span></span>
2. <span data-ttu-id="a98f7-169">다시 **설정** > **개발자 옵션** 사용 **USB 디버깅**, 다음 Android 휴대폰 tooyour 개발 PC는 USB 케이블로 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-169">Back in **Settings** > **Developer Options** enable **USB debugging**, then connect your Android phone  tooyour development PC with a USB Cable.</span></span>

<span data-ttu-id="a98f7-170">이 방법은 Android 6.0(Marshmallow)을 실행하는 Google Nexus 5X를 사용하여 테스트되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-170">We tested this using a Google Nexus 5X device running Android 6.0 (Marshmallow).</span></span>  <span data-ttu-id="a98f7-171">그러나 hello 기술에서 공통 된 최신 Android 릴리스 합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-171">However, hello techniques are common across any modern Android release.</span></span>

#### <a name="install-google-play-services"></a><span data-ttu-id="a98f7-172">Google Play Services 설치</span><span class="sxs-lookup"><span data-stu-id="a98f7-172">Install Google Play Services</span></span>
<span data-ttu-id="a98f7-173">hello 푸시 플러그 인 밀어넣기 알림에 대 한 Android Google Play 서비스에 의존합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-173">hello push plugin relies on Android Google Play Services for push notifications.</span></span>

1. <span data-ttu-id="a98f7-174">Visual Studio에서 클릭 **도구** > **Android** > **Android SDK Manager**, hello 확장 **Extras** 폴더 및 검사 hello 상자 toomake hello Sdk 다음의 각 설치 되어 있는지 합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-174">In Visual Studio, click **Tools** > **Android** > **Android SDK Manager**, expand hello **Extras** folder and  check hello box toomake sure that each of hello following SDKs is installed.</span></span>

   * <span data-ttu-id="a98f7-175">Android 2.3 이상</span><span class="sxs-lookup"><span data-stu-id="a98f7-175">Android 2.3 or higher</span></span>
   * <span data-ttu-id="a98f7-176">Google Repository 개정 27 이상</span><span class="sxs-lookup"><span data-stu-id="a98f7-176">Google Repository revision 27 or higher</span></span>
   * <span data-ttu-id="a98f7-177">Google Play Services 9.0.2 이상</span><span class="sxs-lookup"><span data-stu-id="a98f7-177">Google Play Services 9.0.2 or higher</span></span>

2. <span data-ttu-id="a98f7-178">클릭 **패키지 설치** hello 설치 toocomplete 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-178">Click **Install Packages** and wait for hello installation toocomplete.</span></span>

<span data-ttu-id="a98f7-179">hello 현재 필요한 라이브러리 hello에 나열 된 [phonegap 플러그 인 푸시 설치 설명서][19]합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-179">hello current required libraries are listed in hello [phonegap-plugin-push installation documentation][19].</span></span>

#### <a name="test-push-notifications-in-hello-app-on-android"></a><span data-ttu-id="a98f7-180">Android에서 hello 앱에 푸시 알림을 테스트</span><span class="sxs-lookup"><span data-stu-id="a98f7-180">Test push notifications in hello app on Android</span></span>
<span data-ttu-id="a98f7-181">이제 테스트 푸시 알림을 실행 하 여 응용 프로그램 및 hello TodoItem 테이블에 삽입 항목 hello 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-181">You can now test push notifications by running hello app and inserting items in hello TodoItem table.</span></span> <span data-ttu-id="a98f7-182">테스트할 수 있습니다 hello 동일한 장치 또는 두 번째 장치에서 사용 하는 환영 동일한 백 엔드 합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-182">You can test from hello same device or from a second device, as long as you are using hello same backend.</span></span> <span data-ttu-id="a98f7-183">Hello 같은 방법으로 다음 중 하나 hello Android 플랫폼에서 Cordova 앱을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-183">Test your Cordova app on hello Android platform in one of hello following ways:</span></span>

* <span data-ttu-id="a98f7-184">**물리적 장치에서:** USB 케이블을 사용 하 여 Android 장치 tooyour 개발 컴퓨터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-184">**On a physical device:** Attach your Android device tooyour development computer with a USB cable.</span></span>  <span data-ttu-id="a98f7-185">**Google Android 에뮬레이터** 대신 **장치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-185">Instead of **Google Android Emulator**, select **Device**.</span></span> <span data-ttu-id="a98f7-186">Visual Studio는 hello 응용 프로그램 toohello 장치를 배포 하 고 hello 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-186">Visual Studio deploys hello application toohello device and then runs hello application.</span></span>  <span data-ttu-id="a98f7-187">다음 hello 장치에서 hello 응용 프로그램과 상호 작용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-187">You can then interact with hello application on hello device.</span></span>

  <span data-ttu-id="a98f7-188">개발 환경을 개선합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-188">Improve your development experience.</span></span>  <span data-ttu-id="a98f7-189">[Mobizen] [ 20]과 같은 화면 공유 응용 프로그램을 사용하면 Android 응용 프로그램을 개발하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-189">Screen sharing applications such as [Mobizen][20] can assist you in developing an Android application.</span></span>  <span data-ttu-id="a98f7-190">Mobizen PC에서 Android 화면 tooa 웹 브라우저를 프로젝션합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-190">Mobizen projects your Android screen tooa web browser on your PC.</span></span>

* <span data-ttu-id="a98f7-191">**Android 에뮬레이터에서:** 에뮬레이터에서 실행할 때 필요한 추가 구성 단계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-191">**On an Android emulator:** There are additional configuration steps required when running on an emulator.</span></span>

    <span data-ttu-id="a98f7-192">Hello Android Virtual Device (AVD) 관리자에 표시 된 대로 hello 대상으로 설정 하는 Google Api가 tooa 가상 장치를 배포 하는 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-192">Make sure you are deploying tooa virtual device that has Google APIs set as hello target, as shown in hello Android Virtual Device (AVD) manager.</span></span>

    ![](./media/app-service-mobile-cordova-get-started-push/google-apis-avd-settings.png)

    <span data-ttu-id="a98f7-193">Toouse 더 빠른 x86를 원하는 경우 에뮬레이터 있습니다 [hello HAXM 드라이버를 설치] [ 11] hello 에뮬레이터 toouse 구성 및 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-193">If you want toouse a faster x86 emulator, you [install hello HAXM driver][11] and configure hello emulator toouse it.</span></span>

    <span data-ttu-id="a98f7-194">클릭 하 여 Google 계정 toohello Android 장치를 추가 **앱** > **설정** > **계정을 추가**, 다음 hello 프롬프트를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-194">Add a Google account toohello Android device by clicking **Apps** > **Settings** > **Add account**, then follow hello prompts.</span></span>

    ![](./media/app-service-mobile-cordova-get-started-push/add-google-account.png)

    <span data-ttu-id="a98f7-195">앞으로 hello todolist 앱을 실행 하 고 새 할 일 항목을 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-195">Run hello todolist app as before and insert a new todo item.</span></span> <span data-ttu-id="a98f7-196">이 이번에는 알림 아이콘 hello 알림 영역에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-196">This time, a notification icon is displayed in hello notification area.</span></span> <span data-ttu-id="a98f7-197">Hello 알림 서랍 tooview hello의 전체 텍스트 알림 hello 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-197">You can open hello notification drawer tooview hello full text of hello notification.</span></span>

    ![](./media/app-service-mobile-cordova-get-started-push/android-notifications.png)

## <a name="optional-configure-and-run-on-ios"></a><span data-ttu-id="a98f7-198">(선택 사항) iOS에서 구성 및 실행</span><span class="sxs-lookup"><span data-stu-id="a98f7-198">(Optional) Configure and run on iOS</span></span>
<span data-ttu-id="a98f7-199">이 섹션은 iOS 장치에서 hello Cordova 프로젝트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-199">This section is for running hello Cordova project on iOS devices.</span></span> <span data-ttu-id="a98f7-200">iOS 장치로 작업하지 않는 경우 이 섹션을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-200">If you are not working with iOS devices, you can skip this section.</span></span>

#### <a name="install-and-run-hello-ios-remote-build-agent-on-a-mac-or-cloud-service"></a><span data-ttu-id="a98f7-201">Mac 또는 클라우드 서비스에는 빌드 에이전트 설치 및 실행된 hello iOS 원격</span><span class="sxs-lookup"><span data-stu-id="a98f7-201">Install and run hello iOS remote build agent on a Mac or cloud service</span></span>
<span data-ttu-id="a98f7-202">Visual Studio를 사용 하 여 iOS에서 Cordova 앱을 실행할 수 있습니다, 전에 hello에 hello 단계를 수행해 [iOS 설치 가이드] [ 12] tooinstall와 실행된 hello 원격 빌드 에이전트입니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-202">Before you can run a Cordova app on iOS using Visual Studio, go through hello steps in hello [iOS Setup Guide][12] tooinstall and run hello remote build agent.</span></span>

<span data-ttu-id="a98f7-203">IOS 용 hello 앱을 빌드할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-203">Make sure you can build hello app for iOS.</span></span> <span data-ttu-id="a98f7-204">hello hello 설치 가이드의 단계는 Visual Studio에서 iOS에 대 한 필수 toobuild 합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-204">hello steps in hello setup guide are required toobuild for iOS from Visual Studio.</span></span> <span data-ttu-id="a98f7-205">Mac가 hello 원격 빌드 에이전트를 사용 하 여 MacInCloud와 같은 서비스에서 iOS를 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-205">If you do not have a Mac, you can build for iOS using hello remote build agent on a service like MacInCloud.</span></span> <span data-ttu-id="a98f7-206">자세한 내용은 참조 하십시오. [hello 클라우드에서 iOS 앱을 실행][21]합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-206">For more info, see [Run your iOS app in hello cloud][21].</span></span>

> [!NOTE]
> <span data-ttu-id="a98f7-207">XCode 7 이상이 필요한 toouse hello iOS에서 플러그 인 밀어넣기입니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-207">XCode 7 or greater is required toouse hello push plugin on iOS.</span></span>

#### <a name="find-hello-id-toouse-as-your-app-id"></a><span data-ttu-id="a98f7-208">응용 프로그램 ID로 hello ID toouse 찾기</span><span class="sxs-lookup"><span data-stu-id="a98f7-208">Find hello ID toouse as your App ID</span></span>
<span data-ttu-id="a98f7-209">푸시 알림에 대 한 앱을 등록 하려면 먼저 Cordova 앱에서 config.xml을 열고, hello `id` 특성 hello 위젯 요소에 값이 있고 나중에 사용할 수 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-209">Before you register your app for push notifications, open config.xml in your Cordova app, find hello `id` attribute value in hello widget element, and copy it for later use.</span></span> <span data-ttu-id="a98f7-210">Hello ID는 다음과 같은 XML hello, `io.cordova.myapp7777777`합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-210">In hello following XML, hello ID is `io.cordova.myapp7777777`.</span></span>

        <widget defaultlocale="en-US" id="io.cordova.myapp7777777"
          version="1.0.0" windows-packageVersion="1.1.0.0" xmlns="http://www.w3.org/ns/widgets"
            xmlns:cdv="http://cordova.apache.org/ns/1.0" xmlns:vs="http://schemas.microsoft.com/appx/2014/htmlapps">

<span data-ttu-id="a98f7-211">나중에 Apple 개발자 포털에서 앱 ID를 만들 때 이 식별자를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-211">Later, use this identifier when you create an App ID on Apple's developer portal.</span></span> <span data-ttu-id="a98f7-212">Hello 개발자 포털에 다른 응용 프로그램 ID를 만들면이 자습서의 뒷부분에 나오는 몇 가지 추가 단계를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-212">If you create a different App ID on hello developer portal, you must take a few extra steps later in this tutorial.</span></span> <span data-ttu-id="a98f7-213">위젯 요소 hello ID hello 개발자 포털에서 앱 ID hello와 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-213">hello ID in the widget element must match hello App ID on hello developer portal.</span></span>

#### <a name="register-hello-app-for-push-notifications-on-apples-developer-portal"></a><span data-ttu-id="a98f7-214">Apple 개발자 포털에서 푸시 알림을 hello 앱 등록</span><span class="sxs-lookup"><span data-stu-id="a98f7-214">Register hello app for push notifications on Apple's developer portal</span></span>
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

[<span data-ttu-id="a98f7-215">유사한 단계를 보여 주는 비디오 보기</span><span class="sxs-lookup"><span data-stu-id="a98f7-215">Watch a video showing similar steps</span></span>](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-5-Set-up-apns-for-push)

#### <a name="configure-azure-toosend-push-notifications"></a><span data-ttu-id="a98f7-216">Azure toosend 푸시 알림 구성</span><span class="sxs-lookup"><span data-stu-id="a98f7-216">Configure Azure toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

#### <a name="verify-that-your-app-id-matches-your-cordova-app"></a><span data-ttu-id="a98f7-217">앱 ID가 Cordova 앱과 일치하는지 확인</span><span class="sxs-lookup"><span data-stu-id="a98f7-217">Verify that your App ID matches your Cordova app</span></span>
<span data-ttu-id="a98f7-218">Hello 이미 Apple 개발자 계정에서 만든 응용 프로그램 ID의 hello 위젯 요소를 config.xml에 hello ID와 일치할 경우이 단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-218">If hello App ID you created in your Apple Developer Account already matches hello ID of hello widget element in config.xml, you can skip this step.</span></span> <span data-ttu-id="a98f7-219">그러나 hello Id가 일치 하지 않는 경우 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-219">However, if hello IDs don't match, take hello following steps:</span></span>

1. <span data-ttu-id="a98f7-220">프로젝트에서 hello 플랫폼 폴더를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-220">Delete hello platforms folder from your project.</span></span>
2. <span data-ttu-id="a98f7-221">프로젝트에서 hello 플러그 인 폴더를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-221">Delete hello plugins folder from your project.</span></span>
3. <span data-ttu-id="a98f7-222">프로젝트에서 hello node_modules 폴더를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-222">Delete hello node_modules folder from your project.</span></span>
4. <span data-ttu-id="a98f7-223">Config.xml toouse hello Apple 개발자 계정에서 만든 응용 프로그램 ID에에서 대 한 hello 위젯 요소의 hello id 특성을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-223">Update hello id attribute of hello widget element in config.xml toouse hello App ID that you created in your  Apple Developer Account.</span></span>
5. <span data-ttu-id="a98f7-224">프로젝트를 다시 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-224">Rebuild your project.</span></span>

##### <a name="test-push-notifications-in-your-ios-app"></a><span data-ttu-id="a98f7-225">iOS 앱에서 푸시 알림 테스트</span><span class="sxs-lookup"><span data-stu-id="a98f7-225">Test push notifications in your iOS app</span></span>
1. <span data-ttu-id="a98f7-226">Visual Studio에서 확인 **iOS** hello 배포 대상으로 선택한 다음 선택 **장치** 연결 된 iOS 장치에서 toorun 합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-226">In Visual Studio, make sure that **iOS** is selected as hello deployment target, and then choose **Device** toorun on your connected iOS device.</span></span>

    <span data-ttu-id="a98f7-227">IOS 장치가 연결 tooyour PC에서 실행할 수 있습니다 iTunes를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-227">You can run on an iOS device connected tooyour PC using iTunes.</span></span> <span data-ttu-id="a98f7-228">hello iOS 시뮬레이터에 푸시 알림을 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-228">hello iOS Simulator does not support push notifications.</span></span>

2. <span data-ttu-id="a98f7-229">키를 눌러 hello **실행** 단추 또는 **F5** 에서 Visual Studio toobuild hello 프로젝트와 시작 hello, iOS 장치에서 응용 프로그램 클릭 한 다음 **확인** tooaccept 푸시 알림을 합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-229">Press hello **Run** button or **F5** in Visual Studio toobuild hello project and start hello app in an iOS  device, then click **OK** tooaccept push notifications.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a98f7-230">hello 앱 hello 먼저 실행 하는 동안 푸시 알림을 확인 하 라는 요청입니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-230">hello app requests confirmation for push notifications during hello first run.</span></span>

3. <span data-ttu-id="a98f7-231">Hello 앱에서 작업을 입력 하 고 hello 더하기 (+)를 클릭 한 다음 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-231">In hello app, type a task, and then click hello plus (+) icon.</span></span>
4. <span data-ttu-id="a98f7-232">확인 알림이 수신 되 고 확인 toodismiss hello 알림을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-232">Verify that a notification is received, then click OK toodismiss hello notification.</span></span>

## <a name="optional-configure-and-run-on-windows"></a><span data-ttu-id="a98f7-233">(선택 사항) Windows에서 구성 및 실행</span><span class="sxs-lookup"><span data-stu-id="a98f7-233">(Optional) Configure and run on Windows</span></span>
<span data-ttu-id="a98f7-234">이 섹션 (hello PhoneGap 푸시 플러그 인은 Windows 10에서 지원 됨)는 Windows 10 장치에서 hello Apache Cordova 앱 프로젝트를 실행 하기 위한입니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-234">This section is for running hello Apache Cordova app project on Windows 10 devices (hello PhoneGap push plugin is supported on Windows 10).</span></span> <span data-ttu-id="a98f7-235">Windows 장치로 작업하지 않는 경우 이 섹션을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-235">If you are not working with Windows devices, you can skip this section.</span></span>

#### <a name="register-your-windows-app-for-push-notifications-with-wns"></a><span data-ttu-id="a98f7-236">WNS를 사용하여 푸시 알림에 대해 Windows 앱 등록</span><span class="sxs-lookup"><span data-stu-id="a98f7-236">Register your Windows app for push notifications with WNS</span></span>
<span data-ttu-id="a98f7-237">Visual Studio에서 toouse hello 저장소 옵션 hello 솔루션 플랫폼 목록에서 원하는 Windows 대상을 선택 **x64** 또는 **x86** (방지 **Windows AnyCPU** 에 대 한 푸시 알림).</span><span class="sxs-lookup"><span data-stu-id="a98f7-237">toouse hello Store options in Visual Studio, select a Windows target from hello Solution Platforms list, like **Windows-x64** or **Windows-x86** (avoid **Windows-AnyCPU** for push notifications).</span></span>

[!INCLUDE [app-service-mobile-register-wns](../../includes/app-service-mobile-register-wns.md)]

<span data-ttu-id="a98f7-238">[유사한 단계를 보여 주는 비디오 보기][13]</span><span class="sxs-lookup"><span data-stu-id="a98f7-238">[Watch a video showing similar steps][13]</span></span>

#### <a name="configure-hello-notification-hub-for-wns"></a><span data-ttu-id="a98f7-239">Wns hello 알림 허브를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-239">Configure hello notification hub for WNS</span></span>
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

#### <a name="configure-your-cordova-app-toosupport-windows-push-notifications"></a><span data-ttu-id="a98f7-240">Cordova 앱 toosupport Windows 푸시 알림 구성</span><span class="sxs-lookup"><span data-stu-id="a98f7-240">Configure your Cordova app toosupport Windows push notifications</span></span>
<span data-ttu-id="a98f7-241">구성 디자이너 열기 hello (단추로 클릭 하 고 config.xml **뷰 디자이너**)을 선택 hello **Windows** 탭을 선택한 **Windows 10** 아래**Windows 버전을 대상**합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-241">Open hello configuration designer (right-click on config.xml and select **View Designer**), select hello **Windows** tab, and choose **Windows 10** under **Windows Target Version**.</span></span>

<span data-ttu-id="a98f7-242">기본 (디버그)에 푸시 알림을 toosupport 빌드 열기 build.json 파일.</span><span class="sxs-lookup"><span data-stu-id="a98f7-242">toosupport push notifications in your default (debug) builds, open build.json file.</span></span> <span data-ttu-id="a98f7-243">"릴리스" 구성 tooyour 디버그 구성에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-243">Copy the "release" configuration tooyour debug configuration.</span></span>

        "windows": {
            "release": {
                "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
                "publisherId": "CN=yourpublisherID"
            }
        }

<span data-ttu-id="a98f7-244">Hello 업데이트 후 hello build.json 코드 다음 hello를 포함 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-244">After hello update, hello build.json should contain hello following code:</span></span>

    "windows": {
        "release": {
            "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
            "publisherId": "CN=yourpublisherID"
            },
        "debug": {
            "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
            "publisherId": "CN=yourpublisherID"
            }
        }

<span data-ttu-id="a98f7-245">Hello 앱을 빌드하고 오류 없이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-245">Build hello app and verify that you have no errors.</span></span> <span data-ttu-id="a98f7-246">이제 hello 모바일 앱 백 엔드에서 hello 알림에 대 한 경우에 클라이언트 앱 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-246">Your client app should now register for hello notifications from hello Mobile App backend.</span></span> <span data-ttu-id="a98f7-247">솔루션의 모든 Windows 프로젝트에 대해 이 섹션을 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-247">Repeat this section for every Windows project in your solution.</span></span>

#### <a name="test-push-notifications-in-your-windows-app"></a><span data-ttu-id="a98f7-248">Windows 앱에서 푸시 알림 테스트</span><span class="sxs-lookup"><span data-stu-id="a98f7-248">Test push notifications in your Windows app</span></span>
<span data-ttu-id="a98f7-249">Visual Studio에서 Windows 플랫폼와 같은 hello 배포 대상으로 선택 되어 있는지 확인 **x64** 또는 **x86**합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-249">In Visual Studio, make sure that a Windows platform is selected as hello deployment target, such as **Windows-x64** or **Windows-x86**.</span></span> <span data-ttu-id="a98f7-250">Visual Studio를 호스팅하는 Windows 10 PC에 toorun hello 앱 선택 **로컬 컴퓨터**합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-250">toorun hello app on a Windows 10 PC hosting Visual Studio, choose **Local Machine**.</span></span>

<span data-ttu-id="a98f7-251">키를 눌러 hello 단추 toobuild hello 프로젝트를 실행 하 고 hello 응용 프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-251">Press hello Run button toobuild hello project and start hello app.</span></span>

<span data-ttu-id="a98f7-252">Hello 응용 프로그램에서 새 todoitem에 대 한 이름을 입력 하 고 hello 더하기 (+)를 클릭 한 다음 아이콘 tooadd 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-252">In hello app, type a name for a new todoitem, and then click hello plus (+) icon tooadd it.</span></span>

<span data-ttu-id="a98f7-253">Hello 항목이 추가 될 때 알림을 받았는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-253">Verify that a notification is received when hello item is added.</span></span>

## <span data-ttu-id="a98f7-254"><a name="next-steps"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="a98f7-254"><a name="next-steps"></a>Next Steps</span></span>
* <span data-ttu-id="a98f7-255">에 대 한 읽기 [알림 허브] [ 17] toolearn 푸시 알림에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-255">Read about [Notification Hubs][17] toolearn about push notifications.</span></span>
* <span data-ttu-id="a98f7-256">이미 수행 하 여 hello 자습서를 계속 [인증 추가] [ 14] tooyour Apache Cordova 앱.</span><span class="sxs-lookup"><span data-stu-id="a98f7-256">If you have not already done so, continue hello tutorial by [Adding Authentication][14] tooyour Apache Cordova app.</span></span>

<span data-ttu-id="a98f7-257">Toouse Sdk hello 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a98f7-257">Learn how toouse hello SDKs.</span></span>

* <span data-ttu-id="a98f7-258">[Apache Cordova SDK][15]</span><span class="sxs-lookup"><span data-stu-id="a98f7-258">[Apache Cordova SDK][15]</span></span>
* <span data-ttu-id="a98f7-259">[ASP.NET 서버 SDK][1]</span><span class="sxs-lookup"><span data-stu-id="a98f7-259">[ASP.NET Server SDK][1]</span></span>
* <span data-ttu-id="a98f7-260">[Node.js 서버 SDK][16]</span><span class="sxs-lookup"><span data-stu-id="a98f7-260">[Node.js Server SDK][16]</span></span>

<!-- Images -->
[img1]: ./media/app-service-mobile-cordova-get-started-push/add-push-plugin.png

<!-- URLs -->
[1]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[2]: http://www.visualstudio.com/
[3]: https://azure.microsoft.com/pricing/free-trial/
[4]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx
[5]: app-service-mobile-cordova-get-started.md
[6]: http://go.microsoft.com/fwlink/p/?LinkId=268302
[7]: https://developer.apple.com/programs/
[8]: https://developer.microsoft.com/en-us/store/register
[9]: https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-3-Create-azure-notification-hub
[10]: https://www.npmjs.com/
[11]: https://taco.visualstudio.com/en-us/docs/run-app-apache/#HAXM
[12]: http://taco.visualstudio.com/en-us/docs/ios-guide/
[13]: https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-6-Set-up-wns-for-push
[14]: app-service-mobile-cordova-get-started-users.md
[15]: app-service-mobile-cordova-how-to-use-client-library.md
[16]: app-service-mobile-node-backend-how-to-use-server-sdk.md
[17]: ../notification-hubs/notification-hubs-push-notification-overview.md
[18]: https://console.developers.google.com/home/dashboard
[19]: https://github.com/phonegap/phonegap-plugin-push/blob/master/docs/INSTALLATION.md
[20]: https://www.mobizen.com/
[21]: http://taco.visualstudio.com/en-us/docs/build_ios_cloud/

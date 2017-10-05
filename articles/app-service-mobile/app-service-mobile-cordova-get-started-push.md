---
title: "Azure Mobile App을 사용하여 Apache Cordova 앱에 푸시 알림 추가 | Microsoft Docs"
description: "Azure 모바일 앱을 사용하여 Apache Cordova 앱에 푸시 알림을 보내는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: dc3cab0a6a8b4a56ab0fba1a02e5bba9d0ed1b1f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="add-push-notifications-to-your-apache-cordova-app"></a><span data-ttu-id="c5efe-103">Apache Cordova 앱에 푸시 알림 추가</span><span class="sxs-lookup"><span data-stu-id="c5efe-103">Add push notifications to your Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="c5efe-104">개요</span><span class="sxs-lookup"><span data-stu-id="c5efe-104">Overview</span></span>
<span data-ttu-id="c5efe-105">이 자습서에서는 푸시 알림을 [Apache Cordova 빠른 시작] 프로젝트에 추가하여 레코드가 삽입될 때마다 장치에 푸시 알림이 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-105">In this tutorial, you add push notifications to the [Apache Cordova quick start] project so that a push notification is sent to the device every time a record is inserted.</span></span>

<span data-ttu-id="c5efe-106">다운로드한 빠른 시작 서버 프로젝트를 사용하지 않는 경우 푸시 알림 확장 패키지가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-106">If you do not use the downloaded quick start server project, you need the push notification extension package.</span></span> <span data-ttu-id="c5efe-107">자세한 내용은 [Azure Mobile Apps용 .NET 백 엔드 서버 SDK 사용][1]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c5efe-107">For more information, see [Work with the .NET backend server SDK for Azure Mobile Apps][1].</span></span>

## <span data-ttu-id="c5efe-108"><a name="prerequisites"></a>필수 조건</span><span class="sxs-lookup"><span data-stu-id="c5efe-108"><a name="prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="c5efe-109">이 자습서는 Visual Studio 2015 내에서 개발되고 Google Android 에뮬레이터, Android 장치, Windows 장치 및 iOS 장치에서 실행되는 Apache Cordova 응용 프로그램을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-109">This tutorial covers an Apache Cordova application developed with Visual Studio 2015 that runs on the Google Android Emulator, an Android device, a Windows device, and an iOS device.</span></span>

<span data-ttu-id="c5efe-110">이 자습서를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-110">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="c5efe-111">[Visual Studio Community 2015][2] 이상이 설치된 PC</span><span class="sxs-lookup"><span data-stu-id="c5efe-111">A PC with [Visual Studio Community 2015][2] or later versions.</span></span>
* <span data-ttu-id="c5efe-112">[Visual Studio Tools for Apache Cordova][4]</span><span class="sxs-lookup"><span data-stu-id="c5efe-112">[Visual Studio Tools for Apache Cordova][4].</span></span>
* <span data-ttu-id="c5efe-113">[활성 Azure 계정][3]</span><span class="sxs-lookup"><span data-stu-id="c5efe-113">An [active Azure account][3].</span></span>
* <span data-ttu-id="c5efe-114">완료된 [Apache Cordova 빠른 시작][5] 프로젝트</span><span class="sxs-lookup"><span data-stu-id="c5efe-114">A completed [Apache Cordova quick start][5] project.</span></span>
* <span data-ttu-id="c5efe-115">(Android)검증된 메일 주소를 사용하는 [Google 계정][6]</span><span class="sxs-lookup"><span data-stu-id="c5efe-115">(Android) A [Google account][6] with a verified email address.</span></span>
* <span data-ttu-id="c5efe-116">(iOS)[Apple 개발자 프로그램 멤버 자격][7] 및 iOS 장치(iOS 시뮬레이터는 푸시를 지원하지 않음)</span><span class="sxs-lookup"><span data-stu-id="c5efe-116">(iOS) An [Apple Developer Program membership][7] and an iOS device (iOS Simulator does not support push).</span></span>
* <span data-ttu-id="c5efe-117">(Windows)[Windows 스토어 개발자 계정][8] 및 Windows 10 장치</span><span class="sxs-lookup"><span data-stu-id="c5efe-117">(Windows) A [Windows Store Developer Account][8] and a Windows 10 device.</span></span>

## <span data-ttu-id="c5efe-118"><a name="configure-hub"></a>알림 허브 구성</span><span class="sxs-lookup"><span data-stu-id="c5efe-118"><a name="configure-hub"></a>Configure a notification hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

<span data-ttu-id="c5efe-119">[이 섹션의 단계를 보여 주는 비디오 시청][9]</span><span class="sxs-lookup"><span data-stu-id="c5efe-119">[Watch a video showing steps in this section][9]</span></span>

## <a name="update-the-server-project"></a><span data-ttu-id="c5efe-120">서버 프로젝트 업데이트</span><span class="sxs-lookup"><span data-stu-id="c5efe-120">Update the server project</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <span data-ttu-id="c5efe-121"><a name="add-push-to-app"></a>Cordova 앱 수정</span><span class="sxs-lookup"><span data-stu-id="c5efe-121"><a name="add-push-to-app"></a>Modify your Cordova app</span></span>
<span data-ttu-id="c5efe-122">Apache Cordova 앱 프로젝트가 Cordova 푸시 플러그 인 및 플랫폼별 푸시 서비스를 설치하여 푸시 알림을 처리할 준비가 되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-122">Ensure your Apache Cordova app project is ready to handle push notifications by installing the Cordova push plugin plus any platform-specific push services.</span></span>

#### <a name="update-the-cordova-version-in-your-project"></a><span data-ttu-id="c5efe-123">프로젝트에서 Cordova 버전을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-123">Update the Cordova version in your project.</span></span>
<span data-ttu-id="c5efe-124">프로젝트에서 v6.1.1보다 이전 버전의 Apache Cordova가 사용되는 경우 클라이언트 프로젝트를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-124">If your project uses a version of Apache Cordova earlier than v6.1.1, update the client project.</span></span> <span data-ttu-id="c5efe-125">프로젝트를 업데이트하려면</span><span class="sxs-lookup"><span data-stu-id="c5efe-125">To update the project:</span></span>

* <span data-ttu-id="c5efe-126">`config.xml`을 마우스 오른쪽 단추로 클릭하여 구성 디자이너를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-126">Right-click `config.xml` to open the configuration designer.</span></span>
* <span data-ttu-id="c5efe-127">플랫폼 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-127">Select the Platforms tab.</span></span>
* <span data-ttu-id="c5efe-128">**Cordova CLI** 텍스트 상자에서 6.1.1을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-128">Choose 6.1.1 in the **Cordova CLI** text box.</span></span>
* <span data-ttu-id="c5efe-129">**빌드** 및 **솔루션 빌드**를 차례로 선택하여 프로젝트를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-129">Choose **Build**, then **Build Solution** to update the project.</span></span>

#### <a name="install-the-push-plugin"></a><span data-ttu-id="c5efe-130">푸시 플러그 인 설치</span><span class="sxs-lookup"><span data-stu-id="c5efe-130">Install the push plugin</span></span>
<span data-ttu-id="c5efe-131">Apache Cordova 응용 프로그램에서는 기본적으로 장치 또는 네트워크 기능을 처리하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-131">Apache Cordova applications do not natively handle device or network capabilities.</span></span>  <span data-ttu-id="c5efe-132">이러한 기능은 [npm][10] 또는 GitHub에 게시된 플러그 인에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-132">These capabilities are provided by plugins that are published either on [npm][10] or on GitHub.</span></span>  <span data-ttu-id="c5efe-133">`phonegap-plugin-push` 플러그 인은 네트워크 푸시 알림을 처리하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-133">The `phonegap-plugin-push` plugin is used to handle network push notifications.</span></span>

<span data-ttu-id="c5efe-134">이러한 방법 중 하나로 푸시 플러그 인을 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-134">You can install the push plugin in one of these ways:</span></span>

<span data-ttu-id="c5efe-135">**명령 프롬프트에서:**</span><span class="sxs-lookup"><span data-stu-id="c5efe-135">**From the command-prompt:**</span></span>

<span data-ttu-id="c5efe-136">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-136">Execute the following command:</span></span>

    cordova plugin add phonegap-plugin-push

<span data-ttu-id="c5efe-137">**Visual Studio 내에서**</span><span class="sxs-lookup"><span data-stu-id="c5efe-137">**From within Visual Studio:**</span></span>

1. <span data-ttu-id="c5efe-138">솔루션 탐색기에서 `config.xml` 파일을 열고, **플러그 인** > **사용자 지정**을 클릭하고, 설치 원본으로 **Git**을 선택한 후 원본으로 `https://github.com/phonegap/phonegap-plugin-push`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-138">In Solution Explorer, open the `config.xml` file click **Plugins** > **Custom**, select **Git** as the  installation source, then enter `https://github.com/phonegap/phonegap-plugin-push` as the source.</span></span>

   ![][img1]

2. <span data-ttu-id="c5efe-139">설치 원본 옆의 화살표를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-139">Click the arrow next to the installation source.</span></span>
3. <span data-ttu-id="c5efe-140">**SENDER_ID**에서 Google 개발자 콘솔 프로젝트에 대해 숫자 프로젝트 ID가 이미 지정된 경우 여기에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-140">In **SENDER_ID**, if you already have a numeric project ID for the Google Developer Console project, you can add it here.</span></span> <span data-ttu-id="c5efe-141">그렇지 않으면 자리 표시자 값(예: 777777)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-141">Otherwise, enter a placeholder value, like 777777.</span></span>  <span data-ttu-id="c5efe-142">Android를 대상으로 하는 경우 나중에 config.xml에서 이 값을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-142">If you are targeting Android, you can update this value in config.xml later.</span></span>
4. <span data-ttu-id="c5efe-143">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-143">Click **Add**.</span></span>

<span data-ttu-id="c5efe-144">이제 푸시 플러그 인이 설치되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-144">The push plugin is now installed.</span></span>

#### <a name="install-the-device-plugin"></a><span data-ttu-id="c5efe-145">장치 플러그 인 설치</span><span class="sxs-lookup"><span data-stu-id="c5efe-145">Install the device plugin</span></span>
<span data-ttu-id="c5efe-146">푸시 플러그 인을 설치할 때 사용한 것과 동일한 절차를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-146">Follow the same procedure you used to install the push plugin.</span></span>  <span data-ttu-id="c5efe-147">코어 플러그 인 목록에서 장치 플러그 인을 추가합니다(**플러그 인** > **코어**를 클릭하여 찾음).</span><span class="sxs-lookup"><span data-stu-id="c5efe-147">Add the Device plugin from the Core plugins list (click **Plugins** > **Core** to find it).</span></span> <span data-ttu-id="c5efe-148">플랫폼 이름을 가져오려면 이 플러그 인이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-148">You need this plugin to obtain the platform name.</span></span>

#### <a name="register-your-device-on-application-start-up"></a><span data-ttu-id="c5efe-149">응용 프로그램 시작 시 장치 등록</span><span class="sxs-lookup"><span data-stu-id="c5efe-149">Register your device on application start-up</span></span>
<span data-ttu-id="c5efe-150">처음에 Android에 대한 최소한의 코드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-150">Initially, we include some minimal code for Android.</span></span> <span data-ttu-id="c5efe-151">나중에 iOS 또는 Windows 10에서 실행되도록 앱을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-151">Later, modify the app to run on iOS or Windows 10.</span></span>

1. <span data-ttu-id="c5efe-152">로그인 프로세스에 대한 콜백 중에 또는 **onDeviceReady** 메서드 맨 아래에 **registerForPushNotifications** 호출을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-152">Add a call to **registerForPushNotifications** during the callback for the login process, or at the bottom of  the **onDeviceReady** method:</span></span>

        // Login to the service.
        client.login('google')
            .then(function () {
                // Create a table reference
                todoItemTable = client.getTable('todoitem');

                // Refresh the todoItems
                refreshDisplay();

                // Wire up the UI Event Handler for the Add Item
                $('#add-item').submit(addItemHandler);
                $('#refresh').on('click', refreshDisplay);

                    // Added to register for push notifications.
                registerForPushNotifications();

            }, handleError);

    <span data-ttu-id="c5efe-153">이 예제에서는 인증 성공 후에 **registerForPushNotifications**를 호출하는 경우를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-153">This example shows calling **registerForPushNotifications** after authentication succeeds.</span></span>  <span data-ttu-id="c5efe-154">필요한 만큼 자주 `registerForPushNotifications()`를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-154">You can call `registerForPushNotifications()` as often as is required.</span></span>

2. <span data-ttu-id="c5efe-155">다음과 같이 새 **registerForPushNotifications** 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-155">Add the new **registerForPushNotifications** method as follows:</span></span>

        // Register for Push Notifications. Requires that phonegap-plugin-push be installed.
        var pushRegistration = null;
        function registerForPushNotifications() {
          pushRegistration = PushNotification.init({
              android: { senderID: 'Your_Project_ID' },
              ios: { alert: 'true', badge: 'true', sound: 'true' },
              wns: {}
          });

        // Handle the registration event.
        pushRegistration.on('registration', function (data) {
          // Get the native platform of the device.
          var platform = device.platform;
          // Get the handle returned during registration.
          var handle = data.registrationId;
          // Set the device-specific message template.
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
3. <span data-ttu-id="c5efe-156">(Android) 앞의 코드에서는 `Your_Project_ID`를 [Google 개발자 콘솔][18]의 앱에 대한 숫자 프로젝트 ID로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-156">(Android) In the preceding code, replace `Your_Project_ID` with the numeric project ID for your app from the  [Google Developer Console][18].</span></span>

## <a name="optional-configure-and-run-the-app-on-android"></a><span data-ttu-id="c5efe-157">(선택 사항) Android에서 앱 구성 및 실행</span><span class="sxs-lookup"><span data-stu-id="c5efe-157">(Optional) Configure and run the app on Android</span></span>
<span data-ttu-id="c5efe-158">이 섹션을 완료하여 Android에 대한 푸시 알림을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-158">Complete this section to enable push notifications for Android.</span></span>

#### <span data-ttu-id="c5efe-159"><a name="enable-gcm"></a>Firebase Cloud Messaging 사용</span><span class="sxs-lookup"><span data-stu-id="c5efe-159"><a name="enable-gcm"></a>Enable Firebase Cloud Messaging</span></span>
<span data-ttu-id="c5efe-160">처음에는 Google Android 플랫폼을 대상으로 하므로 Firebase Cloud Messaging을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-160">Since we are targeting the Google Android platform initially, you must enable Firebase Cloud Messaging.</span></span>

[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

#### <span data-ttu-id="c5efe-161"><a name="configure-backend"></a>FCM을 사용하여 푸시 요청을 보내도록 모바일 앱 백 엔드 구성</span><span class="sxs-lookup"><span data-stu-id="c5efe-161"><a name="configure-backend"></a>Configure the Mobile App backend to send push requests using FCM</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push.md)]

#### <a name="configure-your-cordova-app-for-android"></a><span data-ttu-id="c5efe-162">Android용 Cordova 앱 구성</span><span class="sxs-lookup"><span data-stu-id="c5efe-162">Configure your Cordova app for Android</span></span>
<span data-ttu-id="c5efe-163">Cordova 앱에서 config.xml을 열고 `Your_Project_ID`를 [Google 개발자 콘솔][18]의 앱에 대한 숫자 프로젝트 ID로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-163">In your Cordova app, open config.xml and replace `Your_Project_ID` with the numeric project ID for your app from the [Google Developer Console][18].</span></span>

        <plugin name="phonegap-plugin-push" version="1.7.1" src="https://github.com/phonegap/phonegap-plugin-push.git">
            <variable name="SENDER_ID" value="Your_Project_ID" />
        </plugin>

<span data-ttu-id="c5efe-164">Index.js를 열고 숫자 프로젝트 ID를 사용하도록 코드를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-164">Open index.js and update the code to use your numeric project ID.</span></span>

        pushRegistration = PushNotification.init({
            android: { senderID: 'Your_Project_ID' },
            ios: { alert: 'true', badge: 'true', sound: 'true' },
            wns: {}
        });

#### <span data-ttu-id="c5efe-165"><a name="configure-device"></a>USB 디버깅을 위해 Android 장치 구성</span><span class="sxs-lookup"><span data-stu-id="c5efe-165"><a name="configure-device"></a>Configure your Android device for USB debugging</span></span>
<span data-ttu-id="c5efe-166">Android 장치에 응용 프로그램을 배포하려면 먼저 USB 디버깅을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-166">Before you can deploy your application to your Android Device, you need to enable USB Debugging.</span></span>  <span data-ttu-id="c5efe-167">Android 휴대폰에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-167">Perform the following steps on your Android phone:</span></span>

1. <span data-ttu-id="c5efe-168">**설정** > **전화 정보**로 이동한 다음 개발자 모드가 사용하도록 설정될 때까지 **빌드 번호**를 누릅니다(약 7회).</span><span class="sxs-lookup"><span data-stu-id="c5efe-168">Go to **Settings** > **About phone**, then tap the **Build number** until developer mode is enabled  (about seven times).</span></span>
2. <span data-ttu-id="c5efe-169">**설정** > **개발자 옵션**으로 돌아가서 **USB 디버깅**을 사용하도록 설정한 다음 USB 케이블을 사용하여 Android 휴대폰을 개발 PC에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-169">Back in **Settings** > **Developer Options** enable **USB debugging**, then connect your Android phone  to your development PC with a USB Cable.</span></span>

<span data-ttu-id="c5efe-170">이 방법은 Android 6.0(Marshmallow)을 실행하는 Google Nexus 5X를 사용하여 테스트되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-170">We tested this using a Google Nexus 5X device running Android 6.0 (Marshmallow).</span></span>  <span data-ttu-id="c5efe-171">그러나 기술은 모든 최신 Android 릴리스에서 공통적입니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-171">However, the techniques are common across any modern Android release.</span></span>

#### <a name="install-google-play-services"></a><span data-ttu-id="c5efe-172">Google Play Services 설치</span><span class="sxs-lookup"><span data-stu-id="c5efe-172">Install Google Play Services</span></span>
<span data-ttu-id="c5efe-173">푸시 플러그 인은 푸시 알림용으로 Google Play Services를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-173">The push plugin relies on Android Google Play Services for push notifications.</span></span>

1. <span data-ttu-id="c5efe-174">Visual Studio에서 **도구**> **Android** > **Android SDK Manager**를 클릭하고, **Extras** 폴더를 확장한 후 다음 SDK가 모두 설치되도록 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-174">In Visual Studio, click **Tools** > **Android** > **Android SDK Manager**, expand the **Extras** folder and  check the box to make sure that each of the following SDKs is installed.</span></span>

   * <span data-ttu-id="c5efe-175">Android 2.3 이상</span><span class="sxs-lookup"><span data-stu-id="c5efe-175">Android 2.3 or higher</span></span>
   * <span data-ttu-id="c5efe-176">Google Repository 개정 27 이상</span><span class="sxs-lookup"><span data-stu-id="c5efe-176">Google Repository revision 27 or higher</span></span>
   * <span data-ttu-id="c5efe-177">Google Play Services 9.0.2 이상</span><span class="sxs-lookup"><span data-stu-id="c5efe-177">Google Play Services 9.0.2 or higher</span></span>

2. <span data-ttu-id="c5efe-178">**패키지 설치**를 클릭하고 설치가 완료될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-178">Click **Install Packages** and wait for the installation to complete.</span></span>

<span data-ttu-id="c5efe-179">현재 필요한 라이브러리가 [phonegap-plugin-push 설치 설명서][19]에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-179">The current required libraries are listed in the [phonegap-plugin-push installation documentation][19].</span></span>

#### <a name="test-push-notifications-in-the-app-on-android"></a><span data-ttu-id="c5efe-180">Android 앱에서 푸시 알림 테스트</span><span class="sxs-lookup"><span data-stu-id="c5efe-180">Test push notifications in the app on Android</span></span>
<span data-ttu-id="c5efe-181">이제 앱을 실행하고 TodoItem 테이블에 항목을 삽입하여 푸시 알림을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-181">You can now test push notifications by running the app and inserting items in the TodoItem table.</span></span> <span data-ttu-id="c5efe-182">동일한 백 엔드를 사용하는 한, 같은 장치에서 테스트해도 되고 두 번째 장치에서 테스트해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-182">You can test from the same device or from a second device, as long as you are using the same backend.</span></span> <span data-ttu-id="c5efe-183">다음 방법 중 하나로 Android 플랫폼에서 Cordova 앱을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-183">Test your Cordova app on the Android platform in one of the following ways:</span></span>

* <span data-ttu-id="c5efe-184">**실제 장치에서:** USB 케이블을 사용하여 Android 장치를 개발 컴퓨터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-184">**On a physical device:** Attach your Android device to your development computer with a USB cable.</span></span>  <span data-ttu-id="c5efe-185">**Google Android 에뮬레이터** 대신 **장치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-185">Instead of **Google Android Emulator**, select **Device**.</span></span> <span data-ttu-id="c5efe-186">Visual Studio에서 장치에 응용 프로그램을 배포하고 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-186">Visual Studio deploys the application to the device and then runs the application.</span></span>  <span data-ttu-id="c5efe-187">이제 장치에서 응용 프로그램과 상호 작용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-187">You can then interact with the application on the device.</span></span>

  <span data-ttu-id="c5efe-188">개발 환경을 개선합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-188">Improve your development experience.</span></span>  <span data-ttu-id="c5efe-189">[Mobizen] [ 20]과 같은 화면 공유 응용 프로그램을 사용하면 Android 응용 프로그램을 개발하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-189">Screen sharing applications such as [Mobizen][20] can assist you in developing an Android application.</span></span>  <span data-ttu-id="c5efe-190">Mobizen은 PC의 웹 브라우저에 Android 화면을 투영합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-190">Mobizen projects your Android screen to a web browser on your PC.</span></span>

* <span data-ttu-id="c5efe-191">**Android 에뮬레이터에서:** 에뮬레이터에서 실행할 때 필요한 추가 구성 단계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-191">**On an Android emulator:** There are additional configuration steps required when running on an emulator.</span></span>

    <span data-ttu-id="c5efe-192">아래와 같이 AVD(Android 가상 장치) 관리자에서 대상으로 설정된 Google API가 있는 가상 장치에 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-192">Make sure you are deploying to a virtual device that has Google APIs set as the target, as shown in the Android Virtual Device (AVD) manager.</span></span>

    ![](./media/app-service-mobile-cordova-get-started-push/google-apis-avd-settings.png)

    <span data-ttu-id="c5efe-193">더 빠른 x86 에뮬레이터를 사용하려는 경우 [HAXM 드라이버를 설치][11]하고 해당 드라이버를 사용하도록 에뮬레이터를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-193">If you want to use a faster x86 emulator, you [install the HAXM driver][11] and configure the emulator to use it.</span></span>

    <span data-ttu-id="c5efe-194">**앱** > **설정** > **계정 추가**를 클릭하여 Android 장치에 Google 계정을 추가한 다음 지시를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-194">Add a Google account to the Android device by clicking **Apps** > **Settings** > **Add account**, then follow the prompts.</span></span>

    ![](./media/app-service-mobile-cordova-get-started-push/add-google-account.png)

    <span data-ttu-id="c5efe-195">이전처럼 todolist 앱을 실행하고 새 todo 항목을 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-195">Run the todolist app as before and insert a new todo item.</span></span> <span data-ttu-id="c5efe-196">이때 알림 아이콘이 알림 영역에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-196">This time, a notification icon is displayed in the notification area.</span></span> <span data-ttu-id="c5efe-197">알림 서랍을 열어서 전체 알림 텍스트를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-197">You can open the notification drawer to view the full text of the notification.</span></span>

    ![](./media/app-service-mobile-cordova-get-started-push/android-notifications.png)

## <a name="optional-configure-and-run-on-ios"></a><span data-ttu-id="c5efe-198">(선택 사항) iOS에서 구성 및 실행</span><span class="sxs-lookup"><span data-stu-id="c5efe-198">(Optional) Configure and run on iOS</span></span>
<span data-ttu-id="c5efe-199">이 섹션은 iOS 장치에서 Cordova 프로젝트를 실행하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-199">This section is for running the Cordova project on iOS devices.</span></span> <span data-ttu-id="c5efe-200">iOS 장치로 작업하지 않는 경우 이 섹션을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-200">If you are not working with iOS devices, you can skip this section.</span></span>

#### <a name="install-and-run-the-ios-remote-build-agent-on-a-mac-or-cloud-service"></a><span data-ttu-id="c5efe-201">Mac 또는 클라우드 서비스에서 iOS remotebuild 에이전트를 설치하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-201">Install and run the iOS remote build agent on a Mac or cloud service</span></span>
<span data-ttu-id="c5efe-202">Visual Studio를 사용하여 iOS에서 Cordova 앱을 실행하려면 먼저 [iOS 설치 가이드][12]의 단계에 따라 remotebuild 에이전트를 설치하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-202">Before you can run a Cordova app on iOS using Visual Studio, go through the steps in the [iOS Setup Guide][12] to install and run the remote build agent.</span></span>

<span data-ttu-id="c5efe-203">IOS용 앱을 빌드할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-203">Make sure you can build the app for iOS.</span></span> <span data-ttu-id="c5efe-204">설치 가이드의 단계는 Visual Studio에서 iOS를 빌드하는 데 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-204">The steps in the setup guide are required to build for iOS from Visual Studio.</span></span> <span data-ttu-id="c5efe-205">Mac이 없는 경우 MacInCloud와 같은 서비스에서 remotebuild 에이전트를 사용하여 iOS를 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-205">If you do not have a Mac, you can build for iOS using the remote build agent on a service like MacInCloud.</span></span> <span data-ttu-id="c5efe-206">자세한 내용은 [클라우드에서 iOS 앱 실행][21]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c5efe-206">For more info, see [Run your iOS app in the cloud][21].</span></span>

> [!NOTE]
> <span data-ttu-id="c5efe-207">XCode 7 이상에서는 iOS에 대한 푸시 플러그 인을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-207">XCode 7 or greater is required to use the push plugin on iOS.</span></span>

#### <a name="find-the-id-to-use-as-your-app-id"></a><span data-ttu-id="c5efe-208">앱 ID로 사용할 ID 찾기</span><span class="sxs-lookup"><span data-stu-id="c5efe-208">Find the ID to use as your App ID</span></span>
<span data-ttu-id="c5efe-209">푸시 알림을 위해 앱을 등록하기 전에 Cordova 앱에서 config.xml을 열고, 위젯 요소에서 `id` 특성 값을 찾은 후 나중에 사용할 수 있도록 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-209">Before you register your app for push notifications, open config.xml in your Cordova app, find the `id` attribute value in the widget element, and copy it for later use.</span></span> <span data-ttu-id="c5efe-210">다음 XML에서 ID는 `io.cordova.myapp7777777`입니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-210">In the following XML, the ID is `io.cordova.myapp7777777`.</span></span>

        <widget defaultlocale="en-US" id="io.cordova.myapp7777777"
          version="1.0.0" windows-packageVersion="1.1.0.0" xmlns="http://www.w3.org/ns/widgets"
            xmlns:cdv="http://cordova.apache.org/ns/1.0" xmlns:vs="http://schemas.microsoft.com/appx/2014/htmlapps">

<span data-ttu-id="c5efe-211">나중에 Apple 개발자 포털에서 앱 ID를 만들 때 이 식별자를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-211">Later, use this identifier when you create an App ID on Apple's developer portal.</span></span> <span data-ttu-id="c5efe-212">개발자 포털에서 다른 앱 ID를 만들 경우 이 자습서의 뒷부분에 나오는 몇 가지 추가 단계를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-212">If you create a different App ID on the developer portal, you must take a few extra steps later in this tutorial.</span></span> <span data-ttu-id="c5efe-213">위젯 요소의 ID는 개발자 포털의 앱 ID와 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-213">The ID in the widget element must match the App ID on the developer portal.</span></span>

#### <a name="register-the-app-for-push-notifications-on-apples-developer-portal"></a><span data-ttu-id="c5efe-214">Apple 개발자 포털의 푸시 알림에 대한 앱 등록</span><span class="sxs-lookup"><span data-stu-id="c5efe-214">Register the app for push notifications on Apple's developer portal</span></span>
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

[<span data-ttu-id="c5efe-215">유사한 단계를 보여 주는 비디오 보기</span><span class="sxs-lookup"><span data-stu-id="c5efe-215">Watch a video showing similar steps</span></span>](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-5-Set-up-apns-for-push)

#### <a name="configure-azure-to-send-push-notifications"></a><span data-ttu-id="c5efe-216">푸시 알림을 전송하도록 Azure 구성</span><span class="sxs-lookup"><span data-stu-id="c5efe-216">Configure Azure to send push notifications</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

#### <a name="verify-that-your-app-id-matches-your-cordova-app"></a><span data-ttu-id="c5efe-217">앱 ID가 Cordova 앱과 일치하는지 확인</span><span class="sxs-lookup"><span data-stu-id="c5efe-217">Verify that your App ID matches your Cordova app</span></span>
<span data-ttu-id="c5efe-218">Apple 개발자 계정에서 만든 앱 ID가 config.xml의 위젯 요소 ID와 일치할 경우 이 단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-218">If the App ID you created in your Apple Developer Account already matches the ID of the widget element in config.xml, you can skip this step.</span></span> <span data-ttu-id="c5efe-219">그러나 ID가 일치하지 않는 경우 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-219">However, if the IDs don't match, take the following steps:</span></span>

1. <span data-ttu-id="c5efe-220">프로젝트에서 플랫폼 폴더를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-220">Delete the platforms folder from your project.</span></span>
2. <span data-ttu-id="c5efe-221">프로젝트에서 플러그 인 폴더를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-221">Delete the plugins folder from your project.</span></span>
3. <span data-ttu-id="c5efe-222">프로젝트에서 node_modules 폴더를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-222">Delete the node_modules folder from your project.</span></span>
4. <span data-ttu-id="c5efe-223">Apple 개발자 계정에서 만든 앱 ID를 사용하도록 config.xml 파일에 있는 위젯 요소의 ID 특성을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-223">Update the id attribute of the widget element in config.xml to use the App ID that you created in your  Apple Developer Account.</span></span>
5. <span data-ttu-id="c5efe-224">프로젝트를 다시 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-224">Rebuild your project.</span></span>

##### <a name="test-push-notifications-in-your-ios-app"></a><span data-ttu-id="c5efe-225">iOS 앱에서 푸시 알림 테스트</span><span class="sxs-lookup"><span data-stu-id="c5efe-225">Test push notifications in your iOS app</span></span>
1. <span data-ttu-id="c5efe-226">Visual Studio에서 **iOS**가 배포 대상으로 선택되어 있는지 확인한 후 **장치**를 선택하여 연결된 iOS 장치에서 실행되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-226">In Visual Studio, make sure that **iOS** is selected as the deployment target, and then choose **Device** to run on your connected iOS device.</span></span>

    <span data-ttu-id="c5efe-227">ITunes를 사용하여 PC에 연결된 iOS 장치에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-227">You can run on an iOS device connected to your PC using iTunes.</span></span> <span data-ttu-id="c5efe-228">iOS 시뮬레이터는 푸시 알림을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-228">The iOS Simulator does not support push notifications.</span></span>

2. <span data-ttu-id="c5efe-229">Visual Studio에서 **실행** 단추 또는 **F5** 키를 눌러 프로젝트를 빌드하고 iOS 장치에서 앱을 시작한 다음, **확인**을 클릭하여 푸시 알림을 수락합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-229">Press the **Run** button or **F5** in Visual Studio to build the project and start the app in an iOS  device, then click **OK** to accept push notifications.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c5efe-230">앱은 첫 번째 실행 동안 푸시 알림에 대한 확인을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-230">The app requests confirmation for push notifications during the first run.</span></span>

3. <span data-ttu-id="c5efe-231">앱에서 작업을 입력하고 더하기(+) 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-231">In the app, type a task, and then click the plus (+) icon.</span></span>
4. <span data-ttu-id="c5efe-232">알림이 수신되는지 확인한 다음 확인을 클릭하여 알림을 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-232">Verify that a notification is received, then click OK to dismiss the notification.</span></span>

## <a name="optional-configure-and-run-on-windows"></a><span data-ttu-id="c5efe-233">(선택 사항) Windows에서 구성 및 실행</span><span class="sxs-lookup"><span data-stu-id="c5efe-233">(Optional) Configure and run on Windows</span></span>
<span data-ttu-id="c5efe-234">이 섹션은 Windows 10 장치에서 Apache Cordova 앱 프로젝트를 실행하기 위해 작성되었습니다(PhoneGap 푸시 플러그 인은 Windows 10에서 지원됨).</span><span class="sxs-lookup"><span data-stu-id="c5efe-234">This section is for running the Apache Cordova app project on Windows 10 devices (the PhoneGap push plugin is supported on Windows 10).</span></span> <span data-ttu-id="c5efe-235">Windows 장치로 작업하지 않는 경우 이 섹션을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-235">If you are not working with Windows devices, you can skip this section.</span></span>

#### <a name="register-your-windows-app-for-push-notifications-with-wns"></a><span data-ttu-id="c5efe-236">WNS를 사용하여 푸시 알림에 대해 Windows 앱 등록</span><span class="sxs-lookup"><span data-stu-id="c5efe-236">Register your Windows app for push notifications with WNS</span></span>
<span data-ttu-id="c5efe-237">Visual Studio에서 저장소 옵션을 사용하려면 솔루션 플랫폼 목록에서 Windows 대상(예: **Windows-x64** 또는 **Windows-x86**)을 선택합니다(푸시 알림에 대해 **Windows-AnyCPU** 선택 안 함).</span><span class="sxs-lookup"><span data-stu-id="c5efe-237">To use the Store options in Visual Studio, select a Windows target from the Solution Platforms list, like **Windows-x64** or **Windows-x86** (avoid **Windows-AnyCPU** for push notifications).</span></span>

[!INCLUDE [app-service-mobile-register-wns](../../includes/app-service-mobile-register-wns.md)]

<span data-ttu-id="c5efe-238">[유사한 단계를 보여 주는 비디오 보기][13]</span><span class="sxs-lookup"><span data-stu-id="c5efe-238">[Watch a video showing similar steps][13]</span></span>

#### <a name="configure-the-notification-hub-for-wns"></a><span data-ttu-id="c5efe-239">WNS에 대한 알림 허브 구성</span><span class="sxs-lookup"><span data-stu-id="c5efe-239">Configure the notification hub for WNS</span></span>
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

#### <a name="configure-your-cordova-app-to-support-windows-push-notifications"></a><span data-ttu-id="c5efe-240">Windows 푸시 알림을 지원하도록 Cordova 앱 구성</span><span class="sxs-lookup"><span data-stu-id="c5efe-240">Configure your Cordova app to support Windows push notifications</span></span>
<span data-ttu-id="c5efe-241">구성 디자이너를 열고(config.xml을 마우스 오른쪽 단추로 클릭하고 **뷰 디자이너** 선택) **Windows** 탭을 선택한 후 **Windows 대상 버전**에서 **Windows 10**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-241">Open the configuration designer (right-click on config.xml and select **View Designer**), select the **Windows** tab, and choose **Windows 10** under **Windows Target Version**.</span></span>

<span data-ttu-id="c5efe-242">기본(디버그) 빌드에서 푸시 알림을 지원하려면 build.json 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-242">To support push notifications in your default (debug) builds, open build.json file.</span></span> <span data-ttu-id="c5efe-243">"릴리스" 구성을 디버그 구성에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-243">Copy the "release" configuration to your debug configuration.</span></span>

        "windows": {
            "release": {
                "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
                "publisherId": "CN=yourpublisherID"
            }
        }

<span data-ttu-id="c5efe-244">업데이트 후에 build.json에는 다음 코드가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-244">After the update, the build.json should contain the following code:</span></span>

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

<span data-ttu-id="c5efe-245">앱을 빌드하고 오류가 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-245">Build the app and verify that you have no errors.</span></span> <span data-ttu-id="c5efe-246">이제 클라이언트 앱이 모바일 앱 백 엔드에서 알림을 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-246">Your client app should now register for the notifications from the Mobile App backend.</span></span> <span data-ttu-id="c5efe-247">솔루션의 모든 Windows 프로젝트에 대해 이 섹션을 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-247">Repeat this section for every Windows project in your solution.</span></span>

#### <a name="test-push-notifications-in-your-windows-app"></a><span data-ttu-id="c5efe-248">Windows 앱에서 푸시 알림 테스트</span><span class="sxs-lookup"><span data-stu-id="c5efe-248">Test push notifications in your Windows app</span></span>
<span data-ttu-id="c5efe-249">Visual Studio에서 Windows 플랫폼이 배포 대상(예: **Windows-x64** 또는 **Windows-x86**)으로 선택되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-249">In Visual Studio, make sure that a Windows platform is selected as the deployment target, such as **Windows-x64** or **Windows-x86**.</span></span> <span data-ttu-id="c5efe-250">Visual Studio를 호스트하는 Windows 10 PC에서 앱을 실행하려면 **로컬 컴퓨터**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-250">To run the app on a Windows 10 PC hosting Visual Studio, choose **Local Machine**.</span></span>

<span data-ttu-id="c5efe-251">실행 단추를 눌러 프로젝트를 빌드하고 앱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-251">Press the Run button to build the project and start the app.</span></span>

<span data-ttu-id="c5efe-252">앱에서 새 todoitem에 대한 이름을 입력한 다음 더하기(+) 아이콘을 클릭하여 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-252">In the app, type a name for a new todoitem, and then click the plus (+) icon to add it.</span></span>

<span data-ttu-id="c5efe-253">항목이 추가될 때 알림을 받았는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-253">Verify that a notification is received when the item is added.</span></span>

## <span data-ttu-id="c5efe-254"><a name="next-steps"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="c5efe-254"><a name="next-steps"></a>Next Steps</span></span>
* <span data-ttu-id="c5efe-255">푸시 알림에 대한 자세한 내용은 [Notification Hubs][17]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c5efe-255">Read about [Notification Hubs][17] to learn about push notifications.</span></span>
* <span data-ttu-id="c5efe-256">아직 Apache Cordova 앱에 [인증을 추가][14]하지 않은 경우 추가하여 자습서를 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-256">If you have not already done so, continue the tutorial by [Adding Authentication][14] to your Apache Cordova app.</span></span>

<span data-ttu-id="c5efe-257">SDK 사용 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c5efe-257">Learn how to use the SDKs.</span></span>

* <span data-ttu-id="c5efe-258">[Apache Cordova SDK][15]</span><span class="sxs-lookup"><span data-stu-id="c5efe-258">[Apache Cordova SDK][15]</span></span>
* <span data-ttu-id="c5efe-259">[ASP.NET 서버 SDK][1]</span><span class="sxs-lookup"><span data-stu-id="c5efe-259">[ASP.NET Server SDK][1]</span></span>
* <span data-ttu-id="c5efe-260">[Node.js 서버 SDK][16]</span><span class="sxs-lookup"><span data-stu-id="c5efe-260">[Node.js Server SDK][16]</span></span>

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

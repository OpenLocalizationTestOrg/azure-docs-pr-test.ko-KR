---
title: "Azure 알림 허브를 사용하여 Chrome 앱에 푸시 알림 보내기 | Microsoft Docs"
description: "Azure 알림 허브를 사용하여 Chrome 앱에 푸시 알림을 보내는 방법을 알아봅니다."
services: notification-hubs
keywords: "모바일 푸시 알림, 푸시 알림, 푸시 알림, Chrome 푸시 알림"
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 75d4ff59-d04a-455f-bd44-0130a68e641f
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-chrome
ms.devlang: JavaScript
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 600b1b7e5f3987c9a0acc33b7049f7118442b931
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="send-push-notifications-to-chrome-apps-with-azure-notification-hubs"></a><span data-ttu-id="b9496-104">Azure 알림 허브를 사용하여 Chrome 앱에 푸시 알림 보내기</span><span class="sxs-lookup"><span data-stu-id="b9496-104">Send push notifications to Chrome apps with Azure Notification Hubs</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

<span data-ttu-id="b9496-105">이 항목에서는 Azure 알림 허브를 사용하여 Google Chrome 브라우저의 컨텍스트 내에서 표시되는 Chrome 앱에 푸시 알림을 보내는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-105">This topic shows you how to use Azure Notification Hubs to send push notifications to a Chrome App, which will be displayed within the context of the Google Chrome browser.</span></span> <span data-ttu-id="b9496-106">이 자습서에서는 [GCM(Google Cloud Messaging)](https://developers.google.com/cloud-messaging/)을 사용하여 푸시 알림을 받는 Chrome 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-106">In this tutorial, we will create a Chrome app that receives push notifications by using [Google Cloud Messaging (GCM)](https://developers.google.com/cloud-messaging/).</span></span> 

> [!NOTE]
> <span data-ttu-id="b9496-107">이 자습서를 완료하려면 활성 Azure 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-107">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="b9496-108">계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-108">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="b9496-109">자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%notification-hubs-chrome-get-started%2F)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b9496-109">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%notification-hubs-chrome-get-started%2F).</span></span>
> 
> 

<span data-ttu-id="b9496-110">이 자습서에서는 푸시 알림을 사용하도록 설정하는 다음 기본 단계를 차례로 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-110">The tutorial walks you through these basic steps to enable push notifications:</span></span>

* [<span data-ttu-id="b9496-111">Google Cloud Messaging 사용</span><span class="sxs-lookup"><span data-stu-id="b9496-111">Enable Google Cloud Messaging</span></span>](#register)
* [<span data-ttu-id="b9496-112">알림 허브 구성</span><span class="sxs-lookup"><span data-stu-id="b9496-112">Configure your notification hub</span></span>](#configure-hub)
* [<span data-ttu-id="b9496-113">알림 허브에 Chrome 앱 연결</span><span class="sxs-lookup"><span data-stu-id="b9496-113">Connect your Chrome App to the notification hub</span></span>](#connect-app)
* [<span data-ttu-id="b9496-114">Chrome 앱에 푸시 알림 보내기</span><span class="sxs-lookup"><span data-stu-id="b9496-114">Send a push notification to your Chrome App</span></span>](#send)
* [<span data-ttu-id="b9496-115">추가 기능 및 성능</span><span class="sxs-lookup"><span data-stu-id="b9496-115">Additional functionality & capabilities</span></span>](#next-steps)

> [!NOTE]
> <span data-ttu-id="b9496-116">Chrome 앱 푸시 알림은 일반적인 브라우저 내 알림이 아닙니다. 브라우저 확장성 모델에 특정됩니다(자세한 내용은 [Chrome 앱 개요] 참조).</span><span class="sxs-lookup"><span data-stu-id="b9496-116">Chrome app push notifications are not generic in-browser notifications - they are specific to the browser extensibility model (see [Chrome Apps Overview] for details).</span></span> <span data-ttu-id="b9496-117">데스크톱 브라우저 외에도 Chrome 앱은 모바일(Android 및 iOS)에서 Apache Cordova를 통해 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-117">In addition to the desktop browser, Chrome apps run on mobile (Android and iOS) through Apache Cordova.</span></span> <span data-ttu-id="b9496-118">자세한 내용은 [모바일의 Chrome 앱]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b9496-118">See [Chrome Apps on Mobile] to learn more.</span></span>
> 
> 

<span data-ttu-id="b9496-119">GCM과 Azure 알림 허브를 구성하는 작업은 Android용 구성 작업과 같습니다. [Google Cloud Messaging for Chrome]은 더 이상 사용되지 않으며, 이제는 동일한 GCM이 Android 장치와 Chrome 인스턴스를 모두 지원하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-119">Configuring GCM and Azure Notification Hubs is identical to configuring for Android, since [Google Cloud Messaging for Chrome] has been deprecated and the same GCM now supports both Android devices and Chrome instances.</span></span>

## <span data-ttu-id="b9496-120"><a id="register"></a>Google Cloud Messaging 사용</span><span class="sxs-lookup"><span data-stu-id="b9496-120"><a id="register"></a>Enable Google Cloud Messaging</span></span>
1. <span data-ttu-id="b9496-121">[Google 클라우드 콘솔] 웹 사이트로 이동하여 Google 계정 자격 증명으로 로그인한 후에 **프로젝트 만들기** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-121">Navigate to the [Google Cloud Console] website, sign in with your Google account credentials, and then click the **Create Project** button.</span></span> <span data-ttu-id="b9496-122">적합한 **프로젝트 이름**을 입력하고 **만들기** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-122">Provide an appropriate **Project Name**, and then click the **Create** button.</span></span>
   
       ![Google Cloud Console - Create Project][1]
2. <span data-ttu-id="b9496-123">방금 만든 프로젝트의 **프로젝트** 페이지에서 **프로젝트 번호**를 적어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-123">Make a note of the **Project Number** on the **Projects** page for the project that you just created.</span></span> <span data-ttu-id="b9496-124">이 번호를 Chrome 앱에서 GCM에 등록하기 위한 **GCM 보낸 사람 ID** 로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-124">You will use this as the **GCM Sender ID** in the Chrome App to register with GCM.</span></span>
   
       ![Google Cloud Console - Project Number][2]
3. <span data-ttu-id="b9496-125">왼쪽 창에서 **API 및 인증**을 클릭하고 아래로 스크롤한 다음 토글을 클릭하여 **Google Cloud Messaging for Android**를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-125">In the left pane, click **APIs & auth**, and then scroll down and click the toggle to enable **Google Cloud Messaging for Android**.</span></span> <span data-ttu-id="b9496-126">**Google Cloud Messaging for Chrome**을 사용하도록 설정할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-126">You don't have to enable **Google Cloud Messaging for Chrome**.</span></span>
   
       ![Google Cloud Console - Server Key][3]
4. <span data-ttu-id="b9496-127">왼쪽 창에서 **자격 증명** > **새 키 만들기** > **서버 키** > **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-127">In the left pane, click **Credentials** > **Create New Key** > **Server Key** > **Create**.</span></span>
   
       ![Google Cloud Console - Credentials][4]
5. <span data-ttu-id="b9496-128">서버 **API 키**값을 적어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-128">Make a note of the server **API Key**.</span></span> <span data-ttu-id="b9496-129">다음으로 알림 허브에서 이 키를 구성하여 GCM으로 푸시 알림을 보내도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-129">You will configure this in your notification hub next, to enable it to send push notifications to GCM.</span></span>
   
       ![Google Cloud Console - API Key][5]

## <span data-ttu-id="b9496-130"><a id="configure-hub"></a>알림 허브 구성</span><span class="sxs-lookup"><span data-stu-id="b9496-130"><a id="configure-hub"></a>Configure your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<span data-ttu-id="b9496-131">&emsp;&emsp;6.</span><span class="sxs-lookup"><span data-stu-id="b9496-131">&emsp;&emsp;6.</span></span>   <span data-ttu-id="b9496-132">**설정** 블레이드에서 **알림 서비스**를 선택한 다음 **Google(GCM)**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-132">In the **Settings** blade, select **Notification Services** and then **Google (GCM)**.</span></span> <span data-ttu-id="b9496-133">API 키를 입력하고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-133">Enter the API key and save.</span></span>

&emsp;&emsp;![Azure 알림 허브 - Google(GCM)](./media/notification-hubs-android-get-started/notification-hubs-gcm-api.png)

## <span data-ttu-id="b9496-135"><a id="connect-app"></a>알림 허브에 Chrome 앱 연결</span><span class="sxs-lookup"><span data-stu-id="b9496-135"><a id="connect-app"></a>Connect your Chrome App to the notification hub</span></span>
<span data-ttu-id="b9496-136">이제 알림 허브가 GCM과 작동하도록 구성되었으며, 푸시 알림을 받고 보내도록 앱을 등록하기 위한 연결 문자열이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-136">Your notification hub is now configured to work with GCM, and you have the connection strings to register your app to both receive and send push notifications.</span></span> <span data-ttu-id="b9496-137">LK</span><span class="sxs-lookup"><span data-stu-id="b9496-137">LK</span></span>

### <a name="create-a-new-chrome-app"></a><span data-ttu-id="b9496-138">새 Chrome 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="b9496-138">Create a new Chrome App</span></span>
<span data-ttu-id="b9496-139">[Chrome App GCM 샘플] 을 기반으로 하는 아래 샘플에서는 권장되는 방식으로 Chrome 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-139">The sample below is based on the [Chrome App GCM Sample] and uses the recommended way to create a Chrome App.</span></span> <span data-ttu-id="b9496-140">Azure 알림 허브에 관련된 단계를 중점적으로 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-140">We will highlight the steps specifically related to Azure Notification Hubs.</span></span> 

> [!NOTE]
> <span data-ttu-id="b9496-141">[Chrome 앱 알림 허브 샘플]에서 이 Chrome 앱용 소스를 다운로드하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-141">We recommend that you download the source for this Chrome App from [Chrome App Notification Hub Sample].</span></span>
> 
> 

<span data-ttu-id="b9496-142">JavaScript를 사용하여 Chrome 앱을 만듭니다. 이때 원하는 단어 편집기를 사용하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-142">The Chrome App is created via JavaScript, and you can use any of your preferred word editors for creating it.</span></span> <span data-ttu-id="b9496-143">아래에 이 Chrome 앱이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-143">Below is what this Chrome App will look like.</span></span>

![Google Chrome 앱][15]

1. <span data-ttu-id="b9496-145">폴더를 만들고 이름을 `ChromePushApp`로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-145">Create a folder and name it `ChromePushApp`.</span></span> <span data-ttu-id="b9496-146">물론 이름은 임의입니다. 이름이 다른 경우 필요한 코드 세그먼트에서 경로를 대체하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-146">Of course, the name is arbitrary - if you name it something different, make sure you substitute the path in the required code segments.</span></span>
2. <span data-ttu-id="b9496-147">두 번째 단계에서 만든 폴더에 [crypto-js 라이브러리] 를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-147">Download the [crypto-js library] in the folder you created in the second step.</span></span> <span data-ttu-id="b9496-148">이 라이브러리 폴더에는 `components` 및 `rollups`이라는 두 하위 폴더가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-148">This library folder will contain two subfolders: `components` and `rollups`.</span></span>
3. <span data-ttu-id="b9496-149">`manifest.json` 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-149">Create a `manifest.json` file.</span></span> <span data-ttu-id="b9496-150">모든 Chrome 앱은 앱 메타데이터 및 사용자가 설치하는 경우 앱에 부여된 권한을 모두 포함하는 매니페스트 파일에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-150">All Chrome Apps are backed by a manifest file that contains the app metadata and, most importantly, all permissions that are granted to the app when the user installs it.</span></span>
   
        {
          "name": "NH-GCM Notifications",
          "description": "Chrome platform app.",
          "manifest_version": 2,
          "version": "0.1",
          "app": {
            "background": {
              "scripts": ["background.js"]
            }
          },
          "permissions": ["gcm", "storage", "notifications", "https://*.servicebus.windows.net/*"],
          "icons": { "128": "gcm_128.png" }
        }
   
    <span data-ttu-id="b9496-151">위 코드에서는 이 Chrome 앱이 GCM에서 푸시 알림을 받을 수 있도록 지정하는 `permissions` 요소를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-151">Notice the `permissions` element, which specifies that this Chrome App will be able to receive push notifications from GCM.</span></span> <span data-ttu-id="b9496-152">이 요소는 Chrome 앱이 등록을 위한 REST 호출을 수행하는 Azure 알림 허브 URI도 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-152">It must also specify the Azure Notification Hubs URI where the Chrome App will make a REST call to register.</span></span>
    <span data-ttu-id="b9496-153">또한 샘플 앱은 원본 GCM 샘플에서 다시 사용되는 소스에 들어 있는 `gcm_128.png`아이콘 파일을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-153">Our sample app also uses an icon file, `gcm_128.png`, that you will find at the source that's reused from the original GCM sample.</span></span> <span data-ttu-id="b9496-154">[아이콘 조건](https://developer.chrome.com/apps/manifest/icons)에 맞는 이미지로 대체할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-154">You can substitute it for any image that fits the [icon criteria](https://developer.chrome.com/apps/manifest/icons).</span></span>
4. <span data-ttu-id="b9496-155">다음 코드를 사용하여 `background.js` 라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-155">Create a file called `background.js` with the following code:</span></span>
   
        // Returns a new notification ID used in the notification.
        function getNotificationId() {
          var id = Math.floor(Math.random() * 9007199254740992) + 1;
          return id.toString();
        }
   
        function messageReceived(message) {
          // A message is an object with a data property that
          // consists of key-value pairs.
   
          // Concatenate all key-value pairs to form a display string.
          var messageString = "";
          for (var key in message.data) {
            if (messageString != "")
              messageString += ", "
            messageString += key + ":" + message.data[key];
          }
          console.log("Message received: " + messageString);
   
          // Pop up a notification to show the GCM message.
          chrome.notifications.create(getNotificationId(), {
            title: 'GCM Message',
            iconUrl: 'gcm_128.png',
            type: 'basic',
            message: messageString
          }, function() {});
        }
   
        var registerWindowCreated = false;
   
        function firstTimeRegistration() {
          chrome.storage.local.get("registered", function(result) {
   
            registerWindowCreated = true;
            chrome.app.window.create(
              "register.html",
              {  width: 520,
                 height: 500,
                 frame: 'chrome'
              },
              function(appWin) {}
            );
          });
        }
   
        // Set up a listener for GCM message event.
        chrome.gcm.onMessage.addListener(messageReceived);
   
        // Set up listeners to trigger the first-time registration.
        chrome.runtime.onInstalled.addListener(firstTimeRegistration);
        chrome.runtime.onStartup.addListener(firstTimeRegistration);
   
    <span data-ttu-id="b9496-156">이 파일은 Chrome 앱 창 HTML(**register.html**) 팝업을 표시하며 들어오는 푸시 알림을 처리하는 처리기 **messageReceived**도 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-156">This is the file that pops up the Chrome App window HTML (**register.html**) and also defines the handler **messageReceived** to handle the incoming push notification.</span></span>
5. <span data-ttu-id="b9496-157">`register.html` 라는 파일 만들기 - Chrome 앱의 UI를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-157">Create a file called `register.html` - this defines the UI of the Chrome App.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="b9496-158">이 샘플은 **CryptoJS v3.1.2**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-158">This sample uses **CryptoJS v3.1.2**.</span></span> <span data-ttu-id="b9496-159">다른 버전의 라이브러리를 다운로드한 경우 `src` 경로에서 버전을 제대로 대체하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-159">If you downloaded another version of the library, make sure you properly substitute the version in the `src` path.</span></span>
   > 
   > 
   
        <html>
   
        <head>
        <title>GCM Registration</title>
        <script src="register.js"></script>
        <script src="CryptoJS v3.1.2/rollups/hmac-sha256.js"></script>
        <script src="CryptoJS v3.1.2/components/enc-base64-min.js"></script>
        </head>
   
        <body>
   
        Sender ID:<br/><input id="senderId" type="TEXT" size="20"><br/>
        <button id="registerWithGCM">Register with GCM</button>
        <br/>
        <br/>
        <br/>
   
        Notification Hub Name:<br/><input id="hubName" type="TEXT" style="width:400px"><br/><br/>
        Connection String:<br/><textarea id="connectionString" type="TEXT" style="width:400px;height:60px"></textarea>
   
        <br/>
   
        <button id="registerWithNH" disabled="true">Register with Azure Notification Hubs</button>
   
        <br/>
        <br/>
   
        <textarea id="console" type="TEXT" readonly style="width:500px;height:200px;background-color:#e5e5e5;padding:5px"></textarea>
   
        </body>
   
        </html>
6. <span data-ttu-id="b9496-160">아래 코드로 `register.js` 이라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-160">Create a file called `register.js` with the code below.</span></span> <span data-ttu-id="b9496-161">이 파일은 `register.html`의 스크립트를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-161">This file specifies the script behind `register.html`.</span></span> <span data-ttu-id="b9496-162">Chrome 앱은 인라인 실행을 허용하지 않으므로 UI에 대해 별도의 지원 스크립트를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-162">Chrome Apps do not allow inline execution, so you have to create a separate backing script for your UI.</span></span>
   
        var registrationId = "";
        var hubName        = "", connectionString = "";
        var originalUri    = "", targetUri = "", endpoint = "", sasKeyName = "", sasKeyValue = "", sasToken = "";
   
        window.onload = function() {
           document.getElementById("registerWithGCM").onclick = registerWithGCM;  
           document.getElementById("registerWithNH").onclick = registerWithNH;
           updateLog("You have not registered yet. Please provider sender ID and register with GCM and then with  Notification Hubs.");
        }
   
        function updateLog(status) {
          currentStatus = document.getElementById("console").innerHTML;
          if (currentStatus != "") {
            currentStatus = currentStatus + "\n\n";
          }
   
          document.getElementById("console").innerHTML = currentStatus  + status;
        }
   
        function registerWithGCM() {
          var senderId = document.getElementById("senderId").value.trim();
          chrome.gcm.register([senderId], registerCallback);
   
          // Prevent register button from being clicked again before the registration finishes.
          document.getElementById("registerWithGCM").disabled = true;
        }
   
        function registerCallback(regId) {
          registrationId = regId;
          document.getElementById("registerWithGCM").disabled = false;
   
          if (chrome.runtime.lastError) {
            // When the registration fails, handle the error and retry the
            // registration later.
            updateLog("Registration failed: " + chrome.runtime.lastError.message);
            return;
          }
   
          updateLog("Registration with GCM succeeded.");
          document.getElementById("registerWithNH").disabled = false;
   
          // Mark that the first-time registration is done.
          chrome.storage.local.set({registered: true});
        }
   
        function registerWithNH() {
          hubName = document.getElementById("hubName").value.trim();
          connectionString = document.getElementById("connectionString").value.trim();
          splitConnectionString();
          generateSaSToken();
          sendNHRegistrationRequest();
        }
   
        // From http://msdn.microsoft.com/library/dn495627.aspx
        function splitConnectionString()
        {
          var parts = connectionString.split(';');
          if (parts.length != 3)
          throw "Error parsing connection string";
   
          parts.forEach(function(part) {
            if (part.indexOf('Endpoint') == 0) {
            endpoint = 'https' + part.substring(11);
            } else if (part.indexOf('SharedAccessKeyName') == 0) {
            sasKeyName = part.substring(20);
            } else if (part.indexOf('SharedAccessKey') == 0) {
            sasKeyValue = part.substring(16);
            }
          });
   
          originalUri = endpoint + hubName;
        }
   
        function generateSaSToken()
        {
          targetUri = encodeURIComponent(originalUri.toLowerCase()).toLowerCase();
          var expiresInMins = 10; // 10 minute expiration
   
          // Set expiration in seconds.
          var expireOnDate = new Date();
          expireOnDate.setMinutes(expireOnDate.getMinutes() + expiresInMins);
          var expires = Date.UTC(expireOnDate.getUTCFullYear(), expireOnDate
            .getUTCMonth(), expireOnDate.getUTCDate(), expireOnDate
            .getUTCHours(), expireOnDate.getUTCMinutes(), expireOnDate
            .getUTCSeconds()) / 1000;
          var tosign = targetUri + '\n' + expires;
   
          // Using CryptoJS.
          var signature = CryptoJS.HmacSHA256(tosign, sasKeyValue);
          var base64signature = signature.toString(CryptoJS.enc.Base64);
          var base64UriEncoded = encodeURIComponent(base64signature);
   
          // Construct authorization string.
          sasToken = "SharedAccessSignature sr=" + targetUri + "&sig="
                          + base64UriEncoded + "&se=" + expires + "&skn=" + sasKeyName;
        }
   
        function sendNHRegistrationRequest()
        {
          var registrationPayload =
          "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
          "<entry xmlns=\"http://www.w3.org/2005/Atom\">" +
              "<content type=\"application/xml\">" +
                  "<GcmRegistrationDescription xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/netservices/2010/10/servicebus/connect\">" +
                      "<GcmRegistrationId>{GCMRegistrationId}</GcmRegistrationId>" +
                  "</GcmRegistrationDescription>" +
              "</content>" +
          "</entry>";
   
          // Update the payload with the registration ID obtained earlier.
          registrationPayload = registrationPayload.replace("{GCMRegistrationId}", registrationId);
   
          var url = originalUri + "/registrations/?api-version=2014-09";
          var client = new XMLHttpRequest();
   
          client.onload = function () {
            if (client.readyState == 4) {
              if (client.status == 200) {
                updateLog("Notification Hub Registration succesful!");
                updateLog(client.responseText);
              } else {
                updateLog("Notification Hub Registration did not succeed!");
                updateLog("HTTP Status: " + client.status + " : " + client.statusText);
                updateLog("HTTP Response: " + "\n" + client.responseText);
              }
            }
          };
   
          client.onerror = function () {
                updateLog("ERROR - Notification Hub Registration did not succeed!");
          }
   
          client.open("POST", url, true);
          client.setRequestHeader("Content-Type", "application/atom+xml;type=entry;charset=utf-8");
          client.setRequestHeader("Authorization", sasToken);
          client.setRequestHeader("x-ms-version", "2014-09");
   
          try {
              client.send(registrationPayload);
          }
          catch(err) {
              updateLog(err.message);
          }
        }
   
    <span data-ttu-id="b9496-163">위의 스크립트에는 다음과 같은 주요 매개 변수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-163">The above script has the following key parameters:</span></span>
   
   * <span data-ttu-id="b9496-164">**window.onload** 는 UI에서 두 단추의 단추 클릭 이벤트를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-164">**window.onload** defines the button-click events of the two buttons on the UI.</span></span> <span data-ttu-id="b9496-165">하나는 GCM으로 등록하고 다른 하나는 GCM으로 등록한 후에 반환되는 등록 ID를 사용하여 Azure 알림 허브로 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-165">One registers with GCM, and the other uses the registration ID that's returned after registration with GCM to register with Azure Notification Hubs.</span></span>
   * <span data-ttu-id="b9496-166">**updateLog** 는 간단한 로깅 기능을 처리하도록 허용하는 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-166">**updateLog** is the function that allows us to handle simple logging capabilities.</span></span>
   * <span data-ttu-id="b9496-167">**registerWithGCM**은 GCM에 대한 `chrome.gcm.register` 호출을 수행하여 현재 Chrome 앱 인스턴스를 등록하는 첫 번째 단추 클릭 처리기입니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-167">**registerWithGCM** is the first button-click handler, which makes the `chrome.gcm.register` call to GCM to register the current Chrome App instance.</span></span>
   * <span data-ttu-id="b9496-168">**registerCallback** 은 GCM 등록 호출이 반환될 때 호출되는 콜백 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-168">**registerCallback** is the callback function that gets called when the GCM registration call returns.</span></span>
   * <span data-ttu-id="b9496-169">**registerWithNH** 는 알림 허브로 등록하는 두 번째 단추 클릭 처리기입니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-169">**registerWithNH** is the second button-click handler, which registers with Notification Hubs.</span></span> <span data-ttu-id="b9496-170">사용자가 지정한 `hubName` 및 `connectionString`을 가져와 알림 허브 등록 REST API 호출을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-170">It gets `hubName` and `connectionString` (which the user has specified) and crafts the Notification Hubs Registration REST API call.</span></span>
   * <span data-ttu-id="b9496-171">**splitConnectionString** 및 **generateSaSToken**은 모든 REST API 호출에서 사용되어야 하는 SaS 토큰 만들기 프로세스의 JavaScript 구현을 나타내는 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-171">**splitConnectionString** and **generateSaSToken** are helpers that represent the JavaScript implementation of a SaS token creation process, that must be used in all REST API calls.</span></span> <span data-ttu-id="b9496-172">자세한 내용은 [일반적인 개념](http://msdn.microsoft.com/library/dn495627.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b9496-172">For more information, see [Common Concepts](http://msdn.microsoft.com/library/dn495627.aspx).</span></span>
   * <span data-ttu-id="b9496-173">**sendNHRegistrationRequest** 는 Azure 알림 허브에 대한 HTTP REST 호출을 수행하는 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-173">**sendNHRegistrationRequest** is the function that makes a HTTP REST call to Azure Notification Hubs.</span></span>
   * <span data-ttu-id="b9496-174">**registrationPayload** 는 등록 XML 페이로드를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-174">**registrationPayload** defines the registration XML payload.</span></span> <span data-ttu-id="b9496-175">자세한 내용은 [등록 NH REST API 만들기]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b9496-175">For more information, see [Create Registration NH REST API].</span></span> <span data-ttu-id="b9496-176">여기서는 GCM에서 받은 정보를 사용하여 등록 ID를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-176">We update the registration ID in it with what we received from GCM.</span></span>
   * <span data-ttu-id="b9496-177">**클라이언트**는 HTTP 게시 요청을 수행하는 데 사용하는 **XMLHttpRequest** 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-177">**client** is an instance of **XMLHttpRequest** that we use to make the HTTP POST request.</span></span> <span data-ttu-id="b9496-178">여기서는 `sasToken`를 사용하여 `Authorization` 헤더를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-178">Note that we update the `Authorization` header with `sasToken`.</span></span> <span data-ttu-id="b9496-179">이 호출이 정상적으로 완료되면 이 Chrome 앱 인스턴스가 Azure 알림 허브에 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-179">Successful completion of this call will register this Chrome App instance with Azure Notification Hubs.</span></span>

<span data-ttu-id="b9496-180">이 프로젝트에 대한 전체 폴더 구조는 ![Google Chrome 앱 - 폴더 구조][21]와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-180">The overall folder structure for this project should resemble this: ![Google Chrome App - Folder Structure][21]</span></span>

### <a name="set-up-and-test-your-chrome-app"></a><span data-ttu-id="b9496-181">Chrome 앱 설치 및 테스트</span><span class="sxs-lookup"><span data-stu-id="b9496-181">Set up and test your Chrome App</span></span>
1. <span data-ttu-id="b9496-182">Chrome 브라우저를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-182">Open your Chrome browser.</span></span> <span data-ttu-id="b9496-183">**Chrome 확장**을 열고 **개발자 모드**를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-183">Open **Chrome extensions** and enable **Developer mode**.</span></span>
   
       ![Google Chrome - Enable Developer Mode][16]
2. <span data-ttu-id="b9496-184">**압축 해제된 확장 로드** 를 클릭하고 파일을 만든 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-184">Click **Load unpacked extension** and navigate to the folder where you created the files.</span></span> <span data-ttu-id="b9496-185">또한 선택적으로 **크롬 앱 및 확장 개발자 도구**를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-185">You can also optionally use the **Chrome Apps & Extensions Developer Tool**.</span></span> <span data-ttu-id="b9496-186">이 도구는(Chrome 웹 스토어에서 설치된) Chrome 응용 프로그램 자체이며 크롬 앱 개발에 대한 고급 디버깅 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-186">This tool is a Chrome App in itself (installed from the Chrome Web Store) and provides advanced debugging capabilities for your Chrome App development.</span></span>
   
       ![Google Chrome - Load Unpacked Extension][17]
3. <span data-ttu-id="b9496-187">Chrome 앱이 오류 없이 작성되면 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-187">If the Chrome App is created without any errors, then you will see your Chrome App show up.</span></span>
   
       ![Google Chrome - Chrome App Display][18]
4. <span data-ttu-id="b9496-188">이전에 **Google 클라우드 콘솔**에서 확인한 **프로젝트 번호**를 보낸 사람 ID로 입력하고 **GCM에 등록**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-188">Enter the **Project Number** that you got earlier from the **Google Cloud Console** as the sender ID, and click **Register with GCM**.</span></span> <span data-ttu-id="b9496-189">**GCM로 등록 성공**</span><span class="sxs-lookup"><span data-stu-id="b9496-189">You must see the message **Registration with GCM succeeded.**</span></span>
   
       ![Google Chrome - Chrome App Customization][19]
5. <span data-ttu-id="b9496-190">앞에서 포털에서 확인한 **알림 허브 이름** 및 **DefaultListenSharedAccessSignature**를 입력하고 **Azure 알림 허브에 등록**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-190">Enter your **Notification Hub Name** and the **DefaultListenSharedAccessSignature** that you obtained from the portal earlier, and click **Register with Azure Notification Hub**.</span></span> <span data-ttu-id="b9496-191">**성공적으로 알림 허브 등록!**</span><span class="sxs-lookup"><span data-stu-id="b9496-191">You must see the message **Notification Hub Registration successful!**</span></span> <span data-ttu-id="b9496-192">메시지가 표시되고 Azure 알림 허브 등록 ID가 포함된 등록 응답 세부 정보도 함께 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-192">and the details of the registration response, which contains the Azure Notification Hubs registration ID.</span></span>
   
       ![Google Chrome - Specify Notification Hub Details][20]  

## <span data-ttu-id="b9496-193"><a name="send"></a>Chrome 앱에 알림 보내기</span><span class="sxs-lookup"><span data-stu-id="b9496-193"><a name="send"></a>Send a notification to your Chrome App</span></span>
<span data-ttu-id="b9496-194">테스트를 위해 .NET 콘솔 응용 프로그램을 사용하여 Chrome 푸시 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-194">For testing purposes, we will send Chrome push notifications by using a .NET console application.</span></span> 

> [!NOTE]
> <span data-ttu-id="b9496-195">공용 <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">REST 인터페이스</a>를 통해 모든 백 엔드에서 알림 허브를 사용하여 푸시 알림을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-195">You can send push notifications with Notification Hubs from any backend via our public <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">REST interface</a>.</span></span> <span data-ttu-id="b9496-196">더 많은 플랫폼 간 예제는 [설명서 포털](https://azure.microsoft.com/documentation/services/notification-hubs/) 을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-196">Check out our [documentation portal](https://azure.microsoft.com/documentation/services/notification-hubs/) for more cross-platform examples.</span></span>
> 
> 

1. <span data-ttu-id="b9496-197">Visual Studio의 **파일** 메뉴에서 **새로 만들기**와 **프로젝트**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-197">In Visual Studio, from the **File** menu, select **New** and then **Project**.</span></span> <span data-ttu-id="b9496-198">**Visual C#**에서 **Windows** 및 **콘솔 응용 프로그램**을 클릭하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-198">Under **Visual C#**, click **Windows** and **Console Application**, and then click **OK**.</span></span>  <span data-ttu-id="b9496-199">그러면 새 콘솔 응용 프로그램 프로젝트가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-199">This creates a new console application project.</span></span>
2. <span data-ttu-id="b9496-200">**도구** 메뉴에서 **라이브러리 패키지 관리자**, **패키지 관리자 콘솔**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-200">From the **Tools** menu, click **Library Package Manager** and then **Package Manager Console**.</span></span> <span data-ttu-id="b9496-201">그러면 패키지 관리자 콘솔이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-201">This displays the Package Manager Console.</span></span>
3. <span data-ttu-id="b9496-202">콘솔 창에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-202">In the console window, execute the following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
       This adds a reference to the Azure Service Bus SDK with the <a href="http://nuget.org/packages/  WindowsAzure.ServiceBus/">WindowsAzure.ServiceBus NuGet package</a>.
4. <span data-ttu-id="b9496-203">`Program.cs`을 열고 다음 `using` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-203">Open `Program.cs` and add the following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="b9496-204">`Program` 클래스에 다음 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-204">In the `Program` class, add the following method:</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            String message = "{\"data\":{\"message\":\"Hello Chrome from Azure Notification Hubs\"}}";
            await hub.SendGcmNativeNotificationAsync(message);
        }
   
       Make sure to replace the `<hub name>` placeholder with the name of the notification hub that appears in the [portal](https://portal.azure.com) in your Notification Hub blade. Also, replace the connection string placeholder with the connection string called `DefaultFullSharedAccessSignature` that you obtained in the notification hub configuration section.
   
   > [!NOTE]
   > <span data-ttu-id="b9496-205">**수신 대기** 권한이 아니라 **모든** 권한을 가진 연결 문자열을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-205">Make sure that you use the connection string with **Full** access, not **Listen** access.</span></span> <span data-ttu-id="b9496-206">**수신** 액세스 연결 문자열은 푸시 알림을 보내는 권한을 부여하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-206">The **Listen** access connection string does not grant permissions to send push notifications.</span></span>
   > 
   > 
6. <span data-ttu-id="b9496-207">`Main` 메서드에 다음 호출을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-207">Add the following calls in the `Main` method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="b9496-208">Chrome을 실행하도록 하고 콘솔 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-208">Make sure that Chrome is running, and run the console application.</span></span>
8. <span data-ttu-id="b9496-209">바탕 화면에 다음 알림 팝업이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-209">You should see the following notification pop up on your desktop.</span></span>
   
       ![Google Chrome - Notification][13]
9. <span data-ttu-id="b9496-210">또한 Chrome이 실행 중일 때 Window의 작업 표시줄에서 Chrome 알림 창을 사용하여 모든 알림을 확인할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-210">You can also see all your notifications by using the Chrome Notifications window in the taskbar (in Windows) when Chrome is running.</span></span>
   
       ![Google Chrome - Notifications List][14]

> [!NOTE]
> <span data-ttu-id="b9496-211">크롬 앱을 실행하거나 브라우저에서 열 필요가 없습니다.(Chrome 브라우저 자체를 실행해야 함)</span><span class="sxs-lookup"><span data-stu-id="b9496-211">You don't need to have the Chrome App running or open in the browser (though the Chrome browser itself must be running).</span></span> <span data-ttu-id="b9496-212">또한 Chrome 알림 창에서 모든 알림의 통합된 보기가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-212">You also get a consolidated view of all your notifications in the Chrome Notifications window.</span></span>
> 
> 

## <span data-ttu-id="b9496-213"><a name="next-steps"> </a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="b9496-213"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="b9496-214">알림 허브에 대한 자세한 내용은 [알림 허브 개요]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b9496-214">Learn more about Notification Hubs in [Notification Hubs Overview].</span></span>

<span data-ttu-id="b9496-215">특정 사용자를 대상으로 하려면 [Azure 알림 허브 알릴 사용자] 자습서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b9496-215">To target specific users, refer to the [Azure Notification Hubs Notify Users] tutorial.</span></span> 

<span data-ttu-id="b9496-216">사용자를 관심 그룹별로 분할하려면 [Azure 알림 허브 뉴스 속보] 자습서를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9496-216">If you want to segment your users by interest groups, you can follow the [Azure Notification Hubs breaking news] tutorial.</span></span>

<!-- Images. -->
[1]: ./media/notification-hubs-chrome-get-started/GoogleConsoleCreateProject.PNG
[2]: ./media/notification-hubs-chrome-get-started/GoogleProjectNumber.png
[3]: ./media/notification-hubs-chrome-get-started/EnableGCM.png
[4]: ./media/notification-hubs-chrome-get-started/CreateServerKey.png
[5]: ./media/notification-hubs-chrome-get-started/ServerKey.png
[6]: ./media/notification-hubs-chrome-get-started/CreateNH.png
[7]: ./media/notification-hubs-chrome-get-started/NHNamespace.png
[8]: ./media/notification-hubs-chrome-get-started/NamespaceConfigure.png
[9]: ./media/notification-hubs-chrome-get-started/NHConfigure.png
[10]: ./media/notification-hubs-chrome-get-started/NHConfigureGCM.png
[11]: ./media/notification-hubs-chrome-get-started/NHDashboard.png
[12]: ./media/notification-hubs-chrome-get-started/NHConnString.png
[13]: ./media/notification-hubs-chrome-get-started/ChromeNotification.png
[14]: ./media/notification-hubs-chrome-get-started/ChromeNotificationWindow.png
[15]: ./media/notification-hubs-chrome-get-started/ChromeApp.png
[16]: ./media/notification-hubs-chrome-get-started/ChromeExtensions.png
[17]: ./media/notification-hubs-chrome-get-started/ChromeLoadExtension.png
[18]: ./media/notification-hubs-chrome-get-started/ChromeAppLoaded.png
[19]: ./media/notification-hubs-chrome-get-started/ChromeAppGCM.png
[20]: ./media/notification-hubs-chrome-get-started/ChromeAppNH.png
[21]: ./media/notification-hubs-chrome-get-started/FinalFolderView.png

<!-- URLs. -->
<span data-ttu-id="b9496-217">[Chrome 앱 알림 허브 샘플]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToChromeApps</span><span class="sxs-lookup"><span data-stu-id="b9496-217">[Chrome App Notification Hub Sample]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToChromeApps</span></span>
<span data-ttu-id="b9496-218">[Google 클라우드 콘솔]: http://cloud.google.com/console</span><span class="sxs-lookup"><span data-stu-id="b9496-218">[Google Cloud Console]: http://cloud.google.com/console</span></span>
[Azure Classic Portal]: https://manage.windowsazure.com/
<span data-ttu-id="b9496-219">[알림 허브 개요]: notification-hubs-push-notification-overview.md</span><span class="sxs-lookup"><span data-stu-id="b9496-219">[Notification Hubs Overview]: notification-hubs-push-notification-overview.md</span></span>
<span data-ttu-id="b9496-220">[Chrome 앱 개요]: https://developer.chrome.com/apps/about_apps</span><span class="sxs-lookup"><span data-stu-id="b9496-220">[Chrome Apps Overview]: https://developer.chrome.com/apps/about_apps</span></span>
<span data-ttu-id="b9496-221">[Chrome App GCM 샘플]: https://github.com/GoogleChrome/chrome-app-samples/tree/master/samples/gcm-notifications</span><span class="sxs-lookup"><span data-stu-id="b9496-221">[Chrome App GCM Sample]: https://github.com/GoogleChrome/chrome-app-samples/tree/master/samples/gcm-notifications</span></span>
[Installable Web Apps]: https://developers.google.com/chrome/apps/docs/
<span data-ttu-id="b9496-222">[모바일의 Chrome 앱]: https://developer.chrome.com/apps/chrome_apps_on_mobile</span><span class="sxs-lookup"><span data-stu-id="b9496-222">[Chrome Apps on Mobile]: https://developer.chrome.com/apps/chrome_apps_on_mobile</span></span>
<span data-ttu-id="b9496-223">[등록 NH REST API 만들기]: http://msdn.microsoft.com/library/azure/dn223265.aspx</span><span class="sxs-lookup"><span data-stu-id="b9496-223">[Create Registration NH REST API]: http://msdn.microsoft.com/library/azure/dn223265.aspx</span></span>
<span data-ttu-id="b9496-224">[crypto-js 라이브러리]: http://code.google.com/p/crypto-js/</span><span class="sxs-lookup"><span data-stu-id="b9496-224">[crypto-js library]: http://code.google.com/p/crypto-js/</span></span>
[GCM with Chrome Apps]: https://developer.chrome.com/apps/cloudMessaging
<span data-ttu-id="b9496-225">[Google Cloud Messaging for Chrome]: https://developer.chrome.com/apps/cloudMessagingV1</span><span class="sxs-lookup"><span data-stu-id="b9496-225">[Google Cloud Messaging for Chrome]: https://developer.chrome.com/apps/cloudMessagingV1</span></span>
<span data-ttu-id="b9496-226">[Azure 알림 허브 알릴 사용자]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md</span><span class="sxs-lookup"><span data-stu-id="b9496-226">[Azure Notification Hubs Notify Users]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md</span></span>
<span data-ttu-id="b9496-227">[Azure 알림 허브 뉴스 속보]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md</span><span class="sxs-lookup"><span data-stu-id="b9496-227">[Azure Notification Hubs breaking news]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md</span></span>

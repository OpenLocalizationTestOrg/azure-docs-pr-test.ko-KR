---
title: "Azure 알림 허브를 사용 하 여 aaaSend 푸시 알림 tooChrome 앱 | Microsoft Docs"
description: "Azure 알림 허브 toosend toouse 밀어넣기 알림 tooa 크롬 응용 프로그램에 알아봅니다."
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
ms.openlocfilehash: 7dec8ab02622563bc3730a2e96820da8932d22f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="send-push-notifications-toochrome-apps-with-azure-notification-hubs"></a>Azure 알림 허브를 사용 하 여 알림 tooChrome 앱 푸시 보내기
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

이 항목 toouse Azure 알림 허브 toosend 알림 tooa hello Google Chrome 브라우저의 hello 컨텍스트 내에서 표시 되는 크롬 응용 프로그램을 강제 하는 방법을 보여 줍니다. 이 자습서에서는 [GCM(Google Cloud Messaging)](https://developers.google.com/cloud-messaging/)을 사용하여 푸시 알림을 받는 Chrome 앱을 만듭니다. 

> [!NOTE]
> toocomplete이이 자습서에서는 활성 Azure 계정이 있어야 합니다. 계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다. 자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%notification-hubs-chrome-get-started%2F)을 참조하세요.
> 
> 

hello 자습서는 이러한 기본 단계 tooenable 푸시 알림의 안내합니다.

* [Google Cloud Messaging 사용](#register)
* [알림 허브 구성](#configure-hub)
* [크롬 앱 toohello 알림 허브를 연결 합니다.](#connect-app)
* [푸시 알림 tooyour 크롬 앱 보내기](#send)
* [추가 기능 및 성능](#next-steps)

> [!NOTE]
> 크롬 앱 푸시 알림을 일반 브라우저에서 알림 가능 하지-특정 toohello 브라우저 확장성 모델 (참조 [크롬 앱 개요] 세부 정보에 대 한). 또한 toohello 데스크톱 브라우저 크롬 앱 실행 mobile (Android 및 iOS) Apache Cordova를 통해 됩니다. 참조 [크롬 앱이 모바일] toolearn 더 합니다.
> 
> 

GCM 및 Azure 알림 허브 구성은 android의 경우 동일한 tooconfiguring 이후로 [Chrome에 대 한 Google Cloud Messaging] 사용 되지 않으며 동일한 GCM hello 이제 Android 장치 및 Chrome 인스턴스를 모두 지원 합니다.

## <a id="register"></a>Google Cloud Messaging 사용
1. Toohello 이동 [Google 클라우드 콘솔] 웹 사이트, Google 계정 자격 증명으로 로그인 하 고 클릭 hello **프로젝트 만들기** 단추입니다. 적절 한 **프로젝트 이름**, hello를 클릭 한 다음 **만들기** 단추입니다.
   
       ![Google Cloud Console - Create Project][1]
2. Hello 메모 **프로젝트 번호** hello에 **프로젝트** 방금 만든 hello 프로젝트에 대 한 페이지. Hello로 사용 합니다 **GCM 보낸 사람 ID** GCM과 함께 hello 크롬 앱 tooregister에 있습니다.
   
       ![Google Cloud Console - Project Number][2]
3. Hello 왼쪽된 창에서 클릭 **Api & auth**, hello 토글 tooenable 클릭 하 고 아래로 스크롤한 다음 **Android 용 Google Cloud Messaging**합니다. Tooenable 없는 **Chrome에 대 한 Google Cloud Messaging**합니다.
   
       ![Google Cloud Console - Server Key][3]
4. Hello 왼쪽된 창에서 클릭 **자격 증명** > **새 키 만들기** > **서버 키** > **만들기**.
   
       ![Google Cloud Console - Credentials][4]
5. Hello 서버 메모 **API 키**합니다. 알림 허브 다음 tooenable에서이 구성 것 toosend 푸시 알림 tooGCM 합니다.
   
       ![Google Cloud Console - API Key][5]

## <a id="configure-hub"></a>알림 허브 구성
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

&emsp;&emsp;6.   Hello에 **설정** 블레이드를 **Notification Services** 차례로 **GCM (Google)**합니다. Hello API 키를 입력 하 고 저장 합니다.

&emsp;&emsp;![Azure 알림 허브 - Google(GCM)](./media/notification-hubs-android-get-started/notification-hubs-gcm-api.png)

## <a id="connect-app"></a>크롬 앱 toohello 알림 허브를 연결 합니다.
알림 허브는 이제 구성 된 toowork GCM 사용 하며 응용 프로그램 tooboth 수신 및 푸시 알림을 보내려면 연결 문자열 tooregister hello를 해야 합니다. LK

### <a name="create-a-new-chrome-app"></a>새 Chrome 앱 만들기
아래 hello 예제는 hello 기반 [크롬 앱 GCM 샘플] 사용 하 여 hello 권장 방법은 toocreate 크롬 응용 프로그램 및입니다. Hello 단계 특별히 관련 된 알림 허브 tooAzure 중점적으로 다루겠습니다. 

> [!NOTE]
> 이 크롬 앱에 대 한 hello 소스를 다운로드 하는 것이 좋습니다 [크롬 앱 알림 허브 샘플]합니다.
> 
> 

JavaScript를 통해 hello 크롬 앱 만들어지고 것을 만들기 위한 기본 단어 편집기 중 하나를 사용할 수 있습니다. 아래에 이 Chrome 앱이 나와 있습니다.

![Google Chrome 앱][15]

1. 폴더를 만들고 이름을 `ChromePushApp`로 지정합니다. 물론, hello 이름이 임의의-이름을 다른 작업을 하는 경우 필요한 hello 코드 세그먼트에 hello 경로 바꾸면 있는지 확인 합니다.
2. Hello 다운로드 [crypto js 라이브러리] hello 두 번째 단계에서 만든 hello 폴더에 있습니다. 이 라이브러리 폴더에는 `components` 및 `rollups`이라는 두 하위 폴더가 포함됩니다.
3. `manifest.json` 파일을 만듭니다. 모든 Chrome 앱 hello 응용 프로그램 메타 데이터와 대부분을 포함 하는 매니페스트 파일에 의해 지원 됩니다 hello 사용자는이 프로그램을 설치 하는 경우 toohello 앱 부여 된 권한은 모든 것이 중요 합니다.
   
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
   
    공지 hello `permissions` 이 크롬 앱 GCM에서 푸시 알림을 수 tooreceive가 되도록 지정 하는 요소입니다. Hello hello 크롬 앱 REST 호출 tooregister를 만들게 될 Azure 알림 허브 URI를 지정 해야 합니다.
    샘플 앱도 사용 하 여 아이콘 파일을 `gcm_128.png`, 하 hello 원래 GCM 샘플에서 다시 사용 되는 hello 소스에서 얻을 수 있습니다. Hello에 맞는 모든 이미지에 대 한 대체할 수 [아이콘 조건](https://developer.chrome.com/apps/manifest/icons)합니다.
4. 파일을 만들 `background.js` 코드 다음 hello로:
   
        // Returns a new notification ID used in hello notification.
        function getNotificationId() {
          var id = Math.floor(Math.random() * 9007199254740992) + 1;
          return id.toString();
        }
   
        function messageReceived(message) {
          // A message is an object with a data property that
          // consists of key-value pairs.
   
          // Concatenate all key-value pairs tooform a display string.
          var messageString = "";
          for (var key in message.data) {
            if (messageString != "")
              messageString += ", "
            messageString += key + ":" + message.data[key];
          }
          console.log("Message received: " + messageString);
   
          // Pop up a notification tooshow hello GCM message.
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
   
        // Set up listeners tootrigger hello first-time registration.
        chrome.runtime.onInstalled.addListener(firstTimeRegistration);
        chrome.runtime.onStartup.addListener(firstTimeRegistration);
   
    이 hello 크롬 앱 창을 HTML 팝업 되 hello 파일 (**register.html**) hello 처리기 정의 **messageReceived** toohandle hello 들어오는 푸시 알림입니다.
5. 파일을 만들 `register.html` -hello hello 크롬 응용 프로그램의 UI를 정의 합니다. 
   
   > [!NOTE]
   > 이 샘플은 **CryptoJS v3.1.2**를 사용합니다. Hello 라이브러리의 다른 버전을 다운로드 한 경우 대체 hello에 hello 버전이 제대로 있는지 확인 `src` 경로입니다.
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
6. 파일을 만들 `register.js` 아래 hello 코드로 합니다. 이 파일은 뒤에 있는 hello 스크립트 지정 `register.html`합니다. 크롬 앱 해야 하므로 toocreate 별도 백업 스크립트를 UI에 대 한 인라인 실행을 허용 하지 않습니다.
   
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
   
          // Prevent register button from being clicked again before hello registration finishes.
          document.getElementById("registerWithGCM").disabled = true;
        }
   
        function registerCallback(regId) {
          registrationId = regId;
          document.getElementById("registerWithGCM").disabled = false;
   
          if (chrome.runtime.lastError) {
            // When hello registration fails, handle hello error and retry the
            // registration later.
            updateLog("Registration failed: " + chrome.runtime.lastError.message);
            return;
          }
   
          updateLog("Registration with GCM succeeded.");
          document.getElementById("registerWithNH").disabled = false;
   
          // Mark that hello first-time registration is done.
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
   
          // Update hello payload with hello registration ID obtained earlier.
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
   
    위의 스크립트는 hello hello 키 매개 변수 뒤에 있습니다.
   
   * **window.onload** hello UI에 hello 두 단추의 hello 단추 클릭 이벤트를 정의 합니다. 하나, GCM에 등록 하 고 다른 hello GCM tooregister Azure 알림 허브와 등록 후 반환 되는 hello 등록 ID를 사용 합니다.
   * **updateLog** hello 함수을 toohandle 간단한 로깅 기능을 파악할 수 있습니다.
   * **registerWithGCM** hello를 사용 하면 hello 첫 번째 단추 클릭 처리기가 `chrome.gcm.register` 호출 tooGCM tooregister hello 현재 크롬 응용 프로그램 인스턴스.
   * **registerCallback** 은 hello GCM 등록 호출이 반환 될 때 호출 되는 hello 콜백 함수입니다.
   * **registerWithNH** 알림 허브에 등록 hello 두 번째 단추 클릭 처리기입니다. 가져오는 `hubName` 및 `connectionString` (어떤 hello 사용자가 지정) 공예 hello 알림 허브 등록 REST API 호출 및 합니다.
   * **splitConnectionString** 및 **generateSaSToken** 는 REST API에 대 한 모든 호출에 사용 해야 하는 SaS 토큰 만들기 프로세스의 JavaScript 구현을 hello을 나타내는 도우미입니다. 자세한 내용은 [일반적인 개념](http://msdn.microsoft.com/library/dn495627.aspx)을 참조하세요.
   * **sendNHRegistrationRequest** HTTP REST hello 함수 tooAzure 알림 허브를 호출 합니다.
   * **registrationPayload** hello 등록 XML 페이로드를 정의 합니다. 자세한 내용은 [등록 NH REST API 만들기]를 참조하세요. GCM에서 접수 hello 등록 ID를 업데이트 합니다.
   * **클라이언트** 의 인스턴스가 **XMLHttpRequest** 을 사용 하 여 toomake hello HTTP POST 요청입니다. Hello를 업데이트 했습니다 `Authorization` 헤더와 `sasToken`합니다. 이 호출이 정상적으로 완료되면 이 Chrome 앱 인스턴스가 Azure 알림 허브에 등록됩니다.

hello이 프로젝트에 대 한 전체 폴더 구조는 다음과 유사 합니다: ![Google Chrome 앱 폴더 구조][21]

### <a name="set-up-and-test-your-chrome-app"></a>Chrome 앱 설치 및 테스트
1. Chrome 브라우저를 엽니다. **Chrome 확장**을 열고 **개발자 모드**를 사용하도록 설정합니다.
   
       ![Google Chrome - Enable Developer Mode][16]
2. 클릭 **압축 푼된 확장 로드** toohello 만든 폴더를 hello 파일을 이동 합니다. Hello를 선택적으로 사용할 수 있습니다 **크롬 Apps & 확장 개발자 도구**합니다. 이 도구는 크롬 앱 (hello 크롬 Web Store에서에서 설치) 자체의 이며 크롬 앱 개발에 대 한 고급 디버깅 기능을 제공 합니다.
   
       ![Google Chrome - Load Unpacked Extension][17]
3. 를 오류 없이 hello 크롬 응용 프로그램을 만들면 다음 표시 됩니다 크롬 앱 표시 합니다.
   
       ![Google Chrome - Chrome App Display][18]
4. Hello 입력 **프로젝트 번호** hello에서 이전 받은 있는지 **Google 클라우드 콘솔** hello 보낸 사람 ID 및 클릭으로 **GCM 등록**합니다. Hello 메시지를 표시 해야 **성공 GCM과 함께 등록 합니다.**
   
       ![Google Chrome - Chrome App Customization][19]
5. 입력 프로그램 **알림 허브 이름** 및 hello **DefaultListenSharedAccessSignature** hello 포털 앞에서 및 클릭에서 가져온 있는지 **Azure알림허브등록**. Hello 메시지를 표시 해야 **알림 허브 등록 되었습니다!** Azure 알림 허브 등록 hello를 포함 하는 hello 등록 응답의 세부 정보 hello id
   
       ![Google Chrome - Specify Notification Hub Details][20]  

## <a name="send"></a>알림 tooyour 크롬 앱 보내기
테스트를 위해 .NET 콘솔 응용 프로그램을 사용하여 Chrome 푸시 알림을 보냅니다. 

> [!NOTE]
> 공용 <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">REST 인터페이스</a>를 통해 모든 백 엔드에서 알림 허브를 사용하여 푸시 알림을 보낼 수 있습니다. 더 많은 플랫폼 간 예제는 [설명서 포털](https://azure.microsoft.com/documentation/services/notification-hubs/) 을 확인합니다.
> 
> 

1. Hello에서 Visual Studio에서 **파일** 메뉴 선택 **새로** 차례로 **프로젝트**합니다. **Visual C#**에서 **Windows** 및 **콘솔 응용 프로그램**을 클릭하고 **확인**을 클릭합니다.  그러면 새 콘솔 응용 프로그램 프로젝트가 만들어집니다.
2. Hello에서 **도구** 메뉴를 클릭 하 여 **라이브러리 패키지 관리자** 차례로 **패키지 관리자 콘솔**합니다. 패키지 관리자 콘솔 hello 표시 됩니다.
3. Hello 콘솔 창의 hello 다음 명령을 실행 합니다.
   
        Install-Package Microsoft.Azure.NotificationHubs
   
       This adds a reference toohello Azure Service Bus SDK with hello <a href="http://nuget.org/packages/  WindowsAzure.ServiceBus/">WindowsAzure.ServiceBus NuGet package</a>.
4. 열기 `Program.cs` hello 다음 추가 및 `using` 문:
   
        using Microsoft.Azure.NotificationHubs;
5. Hello에 `Program` 클래스, 메서드 뒤 hello 추가:
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            String message = "{\"data\":{\"message\":\"Hello Chrome from Azure Notification Hubs\"}}";
            await hub.SendGcmNativeNotificationAsync(message);
        }
   
       Make sure tooreplace hello `<hub name>` placeholder with hello name of hello notification hub that appears in hello [portal](https://portal.azure.com) in your Notification Hub blade. Also, replace hello connection string placeholder with hello connection string called `DefaultFullSharedAccessSignature` that you obtained in hello notification hub configuration section.
   
   > [!NOTE]
   > 연결 문자열을 hello를 사용 하면 **전체** 액세스 하지 **수신** 액세스 합니다. hello **수신** 액세스 연결 문자열 권한이 toosend 푸시 알림을 부여 되지 않습니다.
   > 
   > 
6. Hello에 hello 다음 호출은 추가 `Main` 메서드:
   
         SendNotificationAsync();
         Console.ReadLine();
7. 크롬이 실행 중인지 확인 하 고 hello 콘솔 응용 프로그램을 실행 합니다.
8. Hello 다음을 참조 해야 팝업 창이 바탕 화면에서 알림입니다.
   
       ![Google Chrome - Notification][13]
9. Hello 작업 표시줄에서 hello 크롬 알림 창 (Windows)에 사용 하 여 모든 알림이 참고할 수 크롬 실행 되는 경우.
   
       ![Google Chrome - Notifications List][14]

> [!NOTE]
> 않아도 toohave hello 크롬 응용 프로그램 실행 중이거나 hello 브라우저에서 열기 (하지만 자체 hello Chrome 브라우저를 실행 해야 합니다). Hello 크롬 알림 창에서 모든 알림의 통합된 보기를 가져올 수도 있습니다.
> 
> 

## <a name="next-steps"> </a>다음 단계
알림 허브에 대한 자세한 내용은 [알림 허브 개요]를 참조하세요.

사용자가 특정 tootarget 참조 toohello [Azure 알림 허브에 게 알림 사용자] 자습서입니다. 

관심 그룹으로 사용자 toosegment을 원하는 경우 참고할 수 hello [최신 뉴스는 Azure 알림 허브] 자습서입니다.

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
[크롬 앱 알림 허브 샘플]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToChromeApps
[Google 클라우드 콘솔]: http://cloud.google.com/console
[Azure Classic Portal]: https://manage.windowsazure.com/
[알림 허브 개요]: notification-hubs-push-notification-overview.md
[크롬 앱 개요]: https://developer.chrome.com/apps/about_apps
[크롬 앱 GCM 샘플]: https://github.com/GoogleChrome/chrome-app-samples/tree/master/samples/gcm-notifications
[Installable Web Apps]: https://developers.google.com/chrome/apps/docs/
[크롬 앱이 모바일]: https://developer.chrome.com/apps/chrome_apps_on_mobile
[등록 NH REST API 만들기]: http://msdn.microsoft.com/library/azure/dn223265.aspx
[crypto js 라이브러리]: http://code.google.com/p/crypto-js/
[GCM with Chrome Apps]: https://developer.chrome.com/apps/cloudMessaging
[Chrome에 대 한 Google Cloud Messaging]: https://developer.chrome.com/apps/cloudMessagingV1
[Azure 알림 허브에 게 알림 사용자]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[최신 뉴스는 Azure 알림 허브]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md

---
title: "Xamarin 앱 용 알림 허브를 사용 하 여 푸시 알림을 aaaiOS | Microsoft Docs"
description: "이 자습서에서는 Azure 알림 허브 toosend toouse 알림 tooa Xamarin iOS 응용 프로그램을 강제 하는 방법을 배웁니다."
services: notification-hubs
keywords: "ios 푸시 알림, 푸시 메시지, 푸시 알림, 푸시 메시지"
documentationcenter: xamarin
author: ysxu
manager: erikre
editor: 
ms.assetid: 4d4dfd42-c5a5-4360-9d70-7812f96924d2
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 8db60338047dd53074b4d3d4bb127aa6d9f13a25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="ios-push-notifications-with-notification-hubs-for-xamarin-apps"></a>Xamarin 앱용 알림 허브를 사용한 iOS 푸시 알림
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>개요
> [!IMPORTANT]
> toocomplete이이 자습서에서는 활성 Azure 계정이 있어야 합니다. 계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다. 자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started)을 참조하세요.
> 
> 

이 자습서에서는 Azure 알림 허브 toosend toouse 밀어넣기 알림 tooan iOS 응용 프로그램입니다.
Hello를 사용 하 여 푸시 알림을 수신 하는 빈 Xamarin.iOS 앱 만들게 [Apple 푸시 알림 서비스 (APNs)](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html)합니다. 수 toouse 수 완료 되 면 알림 허브 toobroadcast 푸시 알림을 tooall hello 장치 앱을 실행 합니다. hello 완성 된 코드는 hello에서 사용할 수 있는 [NotificationHubs 앱] [ GitHub] 샘플.

이 자습서는 알림 허브와 hello 간단한 푸시 메시지 브로드캐스트 시나리오를 보여 줍니다.

## <a name="prerequisites"></a>필수 조건
이 자습서는 hello 다음을 사항이 필요합니다.

* [Xcode 6.0][Install Xcode]
* iOS 7.0(이상) 호환 장치
* iOS 개발자 프로그램 멤버 자격
* [Xamarin Studio]
  
  > [!NOTE]
  > IOS 푸시 알림에 대 한 구성 요구 사항 때문에 배포 하 고 hello 시뮬레이터에서 대신 실제 iOS 장치 (iPhone 또는 iPad) hello 샘플 응용 프로그램을 테스트 합니다.
  > 
  > 

이 자습서를 완료해야 다른 모든 Xamarin.iOS 앱용 알림 허브 자습서를 진행할 수 있습니다.

[!INCLUDE [Notification Hubs Enable Apple Push Notifications](../../includes/notification-hubs-enable-apple-push-notifications.md)]

## <a name="configure-your-notification-hub"></a>알림 허브 구성
이 섹션에서는 새 알림 허브 만들기 및 hello를 사용 하 여 APNS를 사용 하 여 인증을 구성 하는 과정을 설명 **.p12** 사용자가 만든 푸시 인증서입니다. 이미 만든 알림 허브 toouse 원하는 toostep 5를 건너뛸 수 있습니다.

[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="7">

<li>

<p>Hello Azure 포털에서에서 tooconfigure hello APNS 연결을 원하는 대로 ande 클릭 설정에 알림 허브에서 열고 <b>Notification Services</b>, hello를 클릭 한 다음 <b>APNS (Apple)</b> hello 목록에서 항목입니다. 완료 되 면 클릭 <b>인증서 업로드</b> 및 선택 hello <b>.p12</b> hello 인증서에 대 한 hello 암호 뿐 아니라 앞에서 내보낸 인증서입니다.</p>

<p>있는지 tooselect 확인 <b>샌드박스</b> 모드 푸시가 보낼 이후 개발 환경에서 메시지입니다. 만 hello를 사용 하 여 <b>프로덕션</b> hello 스토어에서 앱을 이미 구매한 toosend 푸시 알림을 toousers 하려는 경우 설정 합니다.</p>
</li>
</ol>
&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-apns.png)

&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-sandbox.png)

알림 허브는 이제 구성 된 toowork apns, 그리고 푸시 알림을 보낼 및 hello 연결 문자열 tooregister 응용 프로그램을 있습니다.

## <a name="connect-your-app-toohello-notification-hub"></a>응용 프로그램 toohello 알림 허브를 연결 합니다.
#### <a name="create-a-new-project"></a>새 프로젝트 만들기
1. Xamarin Studio에서 새 iOS 프로젝트를 만들고 hello 선택 **통합 API** > **단일 보기 응용 프로그램** 템플릿.
   
     ![Xamarin Studio - 응용 프로그램 유형 선택][31]
2. 참조 toohello Azure 메시징 구성 요소를 추가 합니다. 솔루션 뷰 hello hello 마우스 오른쪽 단추로 클릭 **구성 요소** 프로젝트에 대 한 폴더를 선택 하 고 **더 구성 요소 가져오기**합니다. Hello에 대 한 검색 **Azure 메시징** 구성 요소 및 hello 구성 요소 tooyour 프로젝트를 추가 합니다.
3. **AppDelegate.cs**, hello 다음 추가 문을 사용 하 여:
   
        using WindowsAzure.Messaging;
4. **SBNotificationHub**인스턴스를 선언합니다.
   
        private SBNotificationHub Hub { get; set; }
5. 만들기는 **Constants.cs** hello 다음 변수를 사용 하 여 클래스:
   
        // Azure app-specific connection string and hub path
        public const string ConnectionString = "<Azure connection string>";
        public const string NotificationHubPath = "<Azure hub path>";
6. **AppDelegate.cs**, 업데이트 **FinishedLaunching()** toomatch hello 다음:
   
        public override bool FinishedLaunching(UIApplication application, NSDictionary launchOptions)
        {
            if (UIDevice.CurrentDevice.CheckSystemVersion (8, 0)) {
                var pushSettings = UIUserNotificationSettings.GetSettingsForTypes (
                       UIUserNotificationType.Alert | UIUserNotificationType.Badge | UIUserNotificationType.Sound,
                       new NSSet ());
   
                UIApplication.SharedApplication.RegisterUserNotificationSettings (pushSettings);
                UIApplication.SharedApplication.RegisterForRemoteNotifications ();
            } else {
                UIRemoteNotificationType notificationTypes = UIRemoteNotificationType.Alert | UIRemoteNotificationType.Badge | UIRemoteNotificationType.Sound;
                UIApplication.SharedApplication.RegisterForRemoteNotificationTypes (notificationTypes);
            }
   
            return true;
        }
7. Hello 재정의 **RegisteredForRemoteNotifications()** 메서드에서 **AppDelegate.cs**:
   
        public override void RegisteredForRemoteNotifications(UIApplication application, NSData deviceToken)
        {
            Hub = new SBNotificationHub(Constants.ConnectionString, Constants.NotificationHubPath);
   
            Hub.UnregisterAllAsync (deviceToken, (error) => {
                if (error != null)
                {
                    Console.WriteLine("Error calling Unregister: {0}", error.ToString());
                    return;
                }
   
                NSSet tags = null; // create tags if you want
                Hub.RegisterNativeAsync(deviceToken, tags, (errorCallback) => {
                    if (errorCallback != null)
                        Console.WriteLine("RegisterNativeAsync error: " + errorCallback.ToString());
                });
            });
        }
8. Hello 재정의 **ReceivedRemoteNotification()** 메서드에서 **AppDelegate.cs**:
   
        public override void ReceivedRemoteNotification(UIApplication application, NSDictionary userInfo)
        {
            ProcessNotification(userInfo, false);
        }
9. Hello 다음 만들기 **ProcessNotification()** 메서드에서 **AppDelegate.cs**:
   
        void ProcessNotification(NSDictionary options, bool fromFinishedLaunching)
        {
            // Check toosee if hello dictionary has hello aps key.  This is hello notification payload you would have sent
            if (null != options && options.ContainsKey(new NSString("aps")))
            {
                //Get hello aps dictionary
                NSDictionary aps = options.ObjectForKey(new NSString("aps")) as NSDictionary;
   
                string alert = string.Empty;
   
                //Extract hello alert text
                // NOTE: If you're using hello simple alert by just specifying
                // "  aps:{alert:"alert msg here"}  ", this will work fine.
                // But if you're using a complex alert with Localization keys, etc.,
                // your "alert" object from hello aps dictionary will be another NSDictionary.
                // Basically hello JSON gets dumped right into a NSDictionary,
                // so keep that in mind.
                if (aps.ContainsKey(new NSString("alert")))
                    alert = (aps [new NSString("alert")] as NSString).ToString();
   
                //If this came from hello ReceivedRemoteNotification while hello app was running,
                // we of course need toomanually process things like hello sound, badge, and alert.
                if (!fromFinishedLaunching)
                {
                    //Manually show an alert
                    if (!string.IsNullOrEmpty(alert))
                    {
                        UIAlertView avAlert = new UIAlertView("Notification", alert, null, "OK", null);
                        avAlert.Show();
                    }
                }
            }
        }
   
   > [!NOTE]
   > Toooverride를 선택할 수 있습니다 **FailedToRegisterForRemoteNotifications()** toohandle 느낌표 아이콘 네트워크 연결이 없습니다. 여기서 hello 사용자 (예: 비행기) 오프 라인 모드에서 응용 프로그램을 시작할 수이 고 메시징 시나리오 특정 tooyour 앱 toohandle 푸시 하려는 특히 유용 합니다.
   > 
   > 
10. Hello 앱이 장치에서 실행 합니다.

## <a name="sending-push-notifications"></a>푸시 알림 보내기
Hello에 알림을 전송 하 여 앱에 푸시 알림을 받는 테스트할 수 [Azure 포털] hello를 통해 **테스트 보내기** hello에서 기능 **문제 해결** 오른쪽 아래의 hello 화면에 표시 된 대로 hello 알림 허브 페이지에서 도구 집합입니다.

![](./media/notification-hubs-ios-get-started/notification-hubs-test-send.png)

푸시 알림은 일반적으로 호환 라이브러리를 사용하는 모바일 서비스 또는 ASP.NET과 같은 백 엔드 서비스를 통해 전송됩니다. 또한 toosend 푸시 메시지는 라이브러리 시나리오에서 사용할 수 없는 경우 직접 hello REST API를 사용할 수 있습니다. 

이 자습서에서는 단순하게 유지 하 고 방금 hello.NET SDK를 사용 하 여 백 엔드 서비스는 대신 콘솔 응용 프로그램에서 알림 허브에 대 한 알림을 전송 하 여 클라이언트 앱을 테스트를 설명 합니다. Hello 권장 [사용 하 여 알림 허브 toopush 알림 toousers](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) ASP.NET 백 엔드에서 알림을 보내기 위한 hello 다음 단계로 자습서입니다. 그러나 다음 방법 hello 알림을 보내는 데 사용할 수 있습니다.

* **REST 인터페이스**: hello를 사용 하 여 모든 백 엔드 플랫폼에 푸시 알림을 지원할 수 있습니다 [REST 인터페이스](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx)합니다.
* **Microsoft Azure 알림 허브.NET SDK**: Visual Studio 용 Nuget 패키지 관리자 hello 실행 [Install-package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)합니다.
* **Node.js** : [어떻게 toouse Node.js에서 알림 허브](notification-hubs-nodejs-push-notification-tutorial.md)합니다.

**모바일 앱**: 방법의 예에 대 한 알림 허브와 통합 된 Azure 앱 서비스 모바일 앱 백 엔드에서 toosend 알림을 참조 [추가 tooyour 모바일 앱 푸시 알림](../app-service-mobile/app-service-mobile-ios-get-started-push.md)합니다.

* **Java / PHP**: toosend 푸시 알림을 사용 하 여 REST Api를 hello 하는 방법의 예제를 보려면 "어떻게 toouse Java/PHP에서 알림 허브" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).

#### <a name="optional-send-push-notifications-from-a-net-console-app"></a>(선택 사항) .NET 콘솔 앱에서 푸시 알림 보내기
이 섹션에서는 간단한 .NET 콘솔 앱을 사용하여 푸시 알림을 보냅니다. Hello 목적으로이 예제에서는 Visual Studio가 이미 설치 되어 있는 tooa Windows 개발 환경을 전환 됩니다.

1. Visual Studio에서 다음과 같이 새로운 Visual C# 콘솔 응용 프로그램을 만듭니다.
   
       ![Visual Studio - Create a new console application][213]
2. Visual Studio에서 **도구**를 클릭하고 **NuGet 패키지 관리자**를 클릭한 다음 **패키지 관리자 콘솔**을 클릭합니다.
   
    hello 패키지 관리자 콘솔에는 Visual Studio 작업 영역에 도킹 된 toohello 맨 표시 되어야 합니다.
3. Hello 패키지 관리자 콘솔 창에서에서 설정 hello **기본 프로젝트** tooyour 새 콘솔 응용 프로그램 프로젝트를 선택한 다음 hello 콘솔 창에 다음 명령을 hello를 실행 합니다.
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    이렇게 하면 추가 참조 toohello Azure 알림 허브 SDK hello를 사용 하 여 <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification 허브 NuGet 패키지</a>합니다.
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. 열기 hello `Program.cs` 파일을 hello 다음 추가 `using` 문을 Azure 클래스와 함수 주 클래스 내에서 사용할 수 있습니다.
   
        using Microsoft.Azure.NotificationHubs;
5. 사용자 `Program` 클래스, 메서드 뒤 hello 추가 (tooreplace hello를 잊지 마십시오 **연결 문자열** 및 **허브 이름**):
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            var alert = "{\"aps\":{\"alert\":\"Hello from .NET!\"}}";
            await hub.SendAppleNativeNotificationAsync(alert);
        }
6. Hello 뒤에 있는 줄을 추가 하면 `Main` 메서드:
   
         SendNotificationAsync();
         Console.ReadLine();
7. Hello F5 키 toorun hello 응용 프로그램 키를 누릅니다. 몇 초 이내에 장치에 푸시 알림이 표시됩니다. Wi-fi 또는 셀룰러 데이터 네트워크를 사용 하는 지 여부를 hello 장치에서 인터넷에 연결 되어 있는지 확인 합니다.

Apple hello에서 모든 hello 가능한 페이로드를 찾을 수 있습니다 [로컬 및 푸시 알림 프로그래밍 가이드]합니다.

#### <a name="optional-send-notifications-from-a-mobile-service"></a>(선택 사항) 모바일 서비스에서 알림 보내기
이 섹션에서는 노드 스크립트를 통해 모바일 서비스를 사용하여 푸시 알림을 보냅니다.

모바일 서비스를 사용 하 여 알림 toosend 따라 [모바일 서비스 시작], 차례로:

1. Toohello 로그인 [Azure 클래식 포털], 모바일 서비스를 선택 합니다.
2. 선택 hello **스케줄러** hello 위에 탭 합니다.
   
       ![Azure Classic Portal - Scheduler][215]
3. 새 예약된 작업을 만들고 이름을 삽입한 후 **요청 시**를 선택합니다.
   
       ![Azure Classic Portal - Create new job][216]
4. Hello 작업이 만들어질 때 hello 작업 이름을 클릭 합니다. Hello 클릭 **스크립트** hello 위쪽 막대를 탭 합니다.
5. 스케줄러 함수 내 스크립트 다음 hello를 삽입 합니다. 알림 허브 이름 및 hello 연결 문자열에 있는 있는지 tooreplace hello 자리 표시자 확인 *DefaultFullSharedAccessSignature* 이전에 얻은입니다. **Save**를 클릭합니다.
   
        var azure = require('azure');
        var notificationHubService = azure.createNotificationHubService('<Hubname>', '<SAS Full access >');
        notificationHubService.apns.send(
            null,
            {"aps":
                {
                  "alert": "Hello from Mobile Services!"
                }
            },
            function (error)
            {
                if (!error) {
                    console.warn("Notification successful");
                }
            }
        );
6. 클릭 **한 번 실행** hello 아래쪽 표시줄에 있습니다. 장치에 대한 경고를 받게 됩니다.

## <a name="next-steps"></a>다음 단계
이 간단한 예제에서는 푸시 알림을 tooall iOS 장치를 브로드캐스트 합니다. 특정 사용자에 게 tootarget 주문 하 toohello 자습서를 참조 하십시오. [사용 하 여 알림 허브 toopush 알림 toousers]합니다. 원하는 경우 toosegment 관심 그룹으로 사용자를 읽을 수 있습니다 [최신 뉴스 사용 하 여 알림 허브 toosend]합니다. 에 대 한 자세한 방법에 대 한 toouse 알림 허브에 [알림 허브 지침] 및 hello [알림 허브 방법 toofor iOS]합니다.

<!-- Images. -->

[213]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-create-console-app.png

[215]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-scheduler1.png
[216]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-scheduler2.png


[31]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-create-ios-app.png




<!-- URLs. -->
[Mobile Services iOS SDK]: http://go.microsoft.com/fwLink/?LinkID=266533
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[모바일 서비스 시작]: /develop/mobile/tutorials/get-started-xamarin-ios
[Azure 클래식 포털]: https://manage.windowsazure.com/
[알림 허브 지침]: http://msdn.microsoft.com/library/jj927170.aspx
[알림 허브 방법 toofor iOS]: http://msdn.microsoft.com/library/jj927168.aspx
[Install Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[iOS Provisioning Portal]: http://go.microsoft.com/fwlink/p/?LinkId=272456

[사용 하 여 알림 허브 toopush 알림 toousers]: /manage/services/notification-hubs/notify-users-aspnet
[최신 뉴스 사용 하 여 알림 허브 toosend]: /manage/services/notification-hubs/breaking-news-dotnet

[로컬 및 푸시 알림 프로그래밍 가이드]:https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/HandlingRemoteNotifications.html#//apple_ref/doc/uid/TP40008194-CH6-SW1
[Apple Push Notification Service]: http://go.microsoft.com/fwlink/p/?LinkId=272584

[Azure Mobile Services Component]: http://components.xamarin.com/view/azure-mobile-services/
[GitHub]: http://go.microsoft.com/fwlink/p/?LinkId=331329
[Xamarin Studio]: http://xamarin.com/download
[WindowsAzure.Messaging]: https://github.com/infosupport/WindowsAzure.Messaging.iOS
[Azure 포털]: https://portal.azure.com

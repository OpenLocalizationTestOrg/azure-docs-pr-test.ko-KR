---
title: "Windows Phone Azure 알림 허브와 aaaSending 푸시 알림을 | Microsoft Docs"
description: "이 자습서에 알아봅니다 어떻게 toouse Azure 알림 허브 toopush 알림 tooa Windows Phone 8 또는 Windows Phone 8.1 Silverlight 응용 프로그램입니다."
services: notification-hubs
documentationcenter: windows
keywords: "푸시 알림, 푸시 알림, windows phone 푸시"
author: ysxu
manager: erikre
editor: erikre
ms.assetid: d872d8dc-4658-4d65-9e71-fa8e34fae96e
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 1a0ad238fe7788ae2e4f47f02d113391af03dd1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-with-azure-notification-hubs-on-windows-phone"></a>Windows Phone에서 Azure 알림 허브를 사용하여 푸시 알림 보내기
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>개요
> [!NOTE]
> toocomplete이이 자습서에서는 활성 Azure 계정이 있어야 합니다. 계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다. 자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-phone-get-started%2F)을 참조하세요.
> 
> 

이 자습서에서는 Azure 알림 허브 toosend toouse 밀어넣기 알림 tooa Windows Phone 8 또는 Windows Phone 8.1 Silverlight 응용 프로그램입니다. Windows Phone 8.1 (Silverlight가 아닌) 대상으로 하는 경우 다음 toohello 참조 [Windows 유니버설](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) 버전입니다.
이 자습서에서는 hello Microsoft 푸시 알림 서비스 (MPNS)를 사용 하 여 푸시 알림을 수신 하는 빈 Windows Phone 8 앱을 만들 수 있습니다. 수 toouse 수 완료 되 면 알림 허브 toobroadcast 푸시 알림을 tooall hello 장치 앱을 실행 합니다.

> [!NOTE]
> 알림 허브 Windows Phone SDK hello hello WNS Windows 푸시 알림 서비스 ()를 사용 하 여 Windows Phone 8.1 Silverlight 앱을 지원 하지 않습니다. Windows Phone 8.1 Silverlight 앱 (MPNS) 대신 WNS toouse hello에 따라 [알림 허브-Windows Phone Silverlight 자습서], REST Api를 사용 하 여 합니다.
> 
> 

hello 자습서 알림 허브를 사용 하 여 hello 간단한 브로드캐스트 시나리오를 보여 줍니다.

## <a name="prerequisites"></a>필수 조건
이 자습서는 hello 다음을 사항이 필요합니다.

* [Visual Studio 2012 Express for Windows Phone]이상 버전

이 자습서를 완료해야 다른 모든 Windows Phone 8 앱용 알림 허브 자습서를 진행할 수 있습니다.

## <a name="create-your-notification-hub"></a>알림 허브 만들기
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">
<li><p>Hello 클릭 <b>Notification Services</b> 섹션 (내 <i>설정</i>)를 클릭 <b>Windows Phone (MPNS)</b> hello를 클릭 한 다음 <b>인증 되지 않은 푸시를 사용 하도록 설정 </b> 확인란 합니다.</p>
</li>
</ol>

&emsp;&emsp;![Azure 포털 - 인증되지 않은 푸시 알림 사용](./media/notification-hubs-windows-phone-get-started/azure-portal-unauth.png)

Windows Phone 대 한 인증 되지 않은 생성 되 고 구성 된 toosend 알림 허브가 되었습니다.

> [!NOTE]
> 이 자습서에서는 인증되지 않은 모드로 MPNS를 사용합니다. MPNS 인증 되지 않은 모드 알림을 통해 tooeach 채널을 보낼 수 있음을 제한 사항이 포함 되어 있습니다. 알림 허브 지원 [MPNS 인증 모드](http://msdn.microsoft.com/library/windowsphone/develop/ff941099.aspx) tooupload를 허용 하 여 인증서입니다.
> 
> 

## <a name="connecting-your-app-toohello-notification-hub"></a>응용 프로그램 toohello 알림 허브를 연결합니다.
1. Visual Studio에서 새 Windows Phone 8 응용 프로그램을 만듭니다.
   
       ![Visual Studio - New Project - Windows Phone App][13]
   
    Visual Studio 2013 업데이트 2 이상에서는 대신 Windows Phone Silverlight 응용 프로그램을 만듭니다.
   
    ![Visual Studio - 새 프로젝트 - 새 응용 프로그램 - Windows Phone Silverlight][11]
2. Visual Studio에서 hello 솔루션을 마우스 오른쪽 단추로 클릭 하 고 클릭 **NuGet 패키지 관리**합니다.
   
    Hello 표시 **NuGet 패키지 관리** 대화 상자.
3. 검색할 `WindowsAzure.Messaging.Managed` 클릭 **설치**, 다음 hello 사용 약관을 수락 합니다.
   
    ![Visual Studio - NuGet 패키지 관리자][20]
   
    다운로드이 설치 하 고 hello를 사용 하 여 Windows 용 참조 toohello Azure 메시징 라이브러리 추가 <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">WindowsAzure.Messaging.Managed NuGet 패키지</a>합니다.
4. Hello 파일 App.xaml.cs 열고 hello 다음 추가 `using` 문:
   
        using Microsoft.Phone.Notification;
        using Microsoft.WindowsAzure.Messaging;
5. 코드의 hello 위쪽 다음 hello 추가 **Application_Launching** App.xaml.cs에 메서드:
   
        var channel = HttpNotificationChannel.Find("MyPushChannel");
        if (channel == null)
        {
            channel = new HttpNotificationChannel("MyPushChannel");
            channel.Open();
            channel.BindToShellToast();
        }
   
        channel.ChannelUriUpdated += new EventHandler<NotificationChannelUriEventArgs>(async (o, args) =>
        {
            var hub = new NotificationHub("<hub name>", "<connection string>");
            var result = await hub.RegisterNativeAsync(args.ChannelUri.ToString());
   
            System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() =>
            {
                MessageBox.Show("Registration :" + result.RegistrationId, "Registered", MessageBoxButton.OK);
            });
        });
   
   > [!NOTE]
   > 값 hello **MyPushChannel** 사용 되는 toolookup hello에 기존 채널에 있는 인덱스는 [HttpNotificationChannel](https://msdn.microsoft.com/library/windows/apps/microsoft.phone.notification.httpnotificationchannel.aspx) 컬렉션입니다. 항목이 없으면 해당 이름을 가진 새 항목을 만듭니다.
   > 
   > 
   
    허브 및 hello 연결 문자열의 tooinsert hello 이름 호출 했는지 확인 **DefaultListenSharedAccessSignature** hello 이전 섹션에서 가져온 합니다.
    이 코드에서 MPNS, hello 앱에 대 한 hello 채널 URI를 검색 하 고 알림 허브에 해당 채널 URI를 등록 합니다. 또한 URI 각 시간 hello 응용 프로그램이 시작 하 여 알림 허브에 등록 되어 해당 hello 채널을 보장 합니다.
   
   > [!NOTE]
   > 이 자습서에서는 알림을 알림 toohello 장치를 보냅니다. 타일 알림을 보낼 때 대신 hello를 호출 해야 **BindToShellTile** hello 채널에서 메서드. toosupport 알림과 타일 알림을 모두 호출 **BindToShellTile** 및 **BindToShellToast**합니다.
   > 
   > 
6. 솔루션 탐색기에서 확장 **속성**개방형 hello `WMAppManifest.xml` 파일, hello 클릭 **기능** 탭을 만들고 해당 hello **ID_CAP_PUSH_NOTIFICATION** 기능 선택 되어 있습니다.
   
       ![Visual Studio - Windows Phone App Capabilities][14]
   
       This ensures that your app can receive push notifications. Without it, any attempt toosend a push notification toohello app will fail.
7. 키를 눌러 hello `F5` 키 toorun hello 앱.
   
    등록 메시지 hello 앱에 표시 됩니다.
8. Hello 닫기는 응용 프로그램.  
   
   > [!NOTE]
   > 푸시 알림 tooreceive hello 포그라운드로 hello 응용 프로그램을 실행 되어야 합니다.
   > 
   > 

## <a name="send-push-notifications-from-your-backend"></a>백 엔드에서 푸시 알림 보내기
Hello 공개를 통해 원하는 백 엔드에서 알림 허브를 사용 하 여 푸시 알림을 보낼 수 <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">REST 인터페이스</a>합니다. 이 자습서에서는 .NET 콘솔 응용 프로그램을 사용하여 푸시 알림을 보냅니다. 

어떻게 toosend 푸시 알림을 알림 허브와 통합 된 ASP.NET WebAPI 백 엔드에서 예제를 보려면 [Azure 알림 허브 사용자에 게 알림.NET 백 엔드와](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md)합니다.  

Toosend 푸시 알림을 사용 하 여 hello 하는 방법에 대 한 예제 [REST Api](https://msdn.microsoft.com/library/azure/dn223264.aspx), 체크 아웃 [어떻게 toouse Java에서 알림 허브](notification-hubs-java-push-notification-tutorial.md) 및 [어떻게 toouse PHP에서 알림 허브](notification-hubs-php-push-notification-tutorial.md) .

1. 마우스 오른쪽 단추로 클릭 hello 솔루션을 선택 **추가** 및 **새 프로젝트...** , 그 다음 **Visual C#**, 클릭 **Windows** 및 **콘솔 응용 프로그램**를 클릭 하 고 **확인**합니다.
   
       ![Visual Studio - New Project - Console Application][6]
   
    이 새 Visual C# 콘솔 응용 프로그램 toohello 솔루션을 추가합니다. 별도의 솔루션에서 이 작업을 수행할 수도 있습니다.
2. **도구**를 클릭하고 **라이브러리 패키지 관리자**를 클릭한 다음 **패키지 관리자 콘솔**을 클릭합니다.
   
    패키지 관리자 콘솔 hello 표시 됩니다.
3. Hello에 **패키지 관리자 콘솔** 창, 집합 hello **기본 프로젝트** tooyour 새 콘솔 응용 프로그램 프로젝트를 선택한 다음 hello 콘솔 창에 다음 명령을 hello를 실행 합니다.
   
       Install-Package Microsoft.Azure.NotificationHubs
   
   이렇게 하면 추가 참조 toohello Azure 알림 허브 SDK hello를 사용 하 여 <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification 허브 NuGet 패키지</a>합니다.
4. 열기 hello `Program.cs` 파일을 hello 다음 추가 `using` 문:
   
        using Microsoft.Azure.NotificationHubs;
5. Hello에 `Program` 클래스, 메서드 뒤 hello 추가:
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient
                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            string toast = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                "<wp:Notification xmlns:wp=\"WPNotification\">" +
                   "<wp:Toast>" +
                        "<wp:Text1>Hello from a .NET App!</wp:Text1>" +
                   "</wp:Toast> " +
                "</wp:Notification>";
            await hub.SendMpnsNativeNotificationAsync(toast);
        }
   
    있는지 tooreplace hello 확인 `<hub name>` hello 포털에 표시 되는 hello 알림 허브의 hello 이름의 자리 표시자입니다. 또한 연결 문자열 자리 표시자 hello 호출 hello 연결 문자열로 대체 **DefaultFullSharedAccessSignature** 는 가져온 hello 섹션의 "알림 허브를 구성 합니다."
   
   > [!NOTE]
   > 연결 문자열을 hello를 사용 하면 **전체** 액세스 하지 **수신** 액세스 합니다. hello 수신 액세스 문자열에는 사용 권한을 toosend 푸시 알림이 없습니다.
   > 
   > 
6. 다음 줄에서 hello 추가 프로그램 `Main` 메서드:
   
         SendNotificationAsync();
         Console.ReadLine();
7. Windows Phone 에뮬레이터를 실행 하 고 응용 프로그램 설정, 닫힌 hello 콘솔 응용 프로그램 프로젝트 hello로 시작 프로젝트를 기본와 hello 키를 누릅니다 `F5` 키 toorun hello 앱.
   
    푸시 알림 메시지가 수신됩니다. Hello 앱을 로드 hello 알림 배너를 탭 합니다.

Hello에서 모든 hello 가능한 페이로드를 찾을 수 있습니다 [알림 카탈로그] 및 [타일 카탈로그] msdn 항목.

## <a name="next-steps"></a>다음 단계
이 간단한 예제에서는 푸시 알림을 tooall Windows Phone 8 장치를 브로드캐스트 합니다. 

특정 사용자에 게 tootarget 주문 하 toohello 참조 [사용 하 여 알림 허브 toopush 알림 toousers] 자습서입니다. 

원하는 경우 toosegment 관심 그룹으로 사용자를 읽을 수 있습니다 [최신 뉴스 사용 하 여 알림 허브 toosend]합니다. 

방법에 대 한 자세한 정보에 알림 허브 toouse [알림 허브 지침]합니다.

<!-- Images. -->
[6]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-console-app.png
[7]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-from-portal.png
[8]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-from-portal2.png
[9]: ./media/notification-hubs-windows-phone-get-started/notification-hub-select-from-portal.png
[10]: ./media/notification-hubs-windows-phone-get-started/notification-hub-select-from-portal2.png
[11]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-wp-silverlight-app.png
[12]: ./media/notification-hubs-windows-phone-get-started/notification-hub-connection-strings.png

[13]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-wp-app.png
[14]: ./media/notification-hubs-windows-phone-get-started/mobile-app-enable-push-wp8.png
[15]: ./media/notification-hubs-windows-phone-get-started/notification-hub-pushauth.png
[20]: ./media/notification-hubs-windows-phone-get-started/notification-hub-windows-universal-app-install-package.png
[213]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-console-app.png





<!-- URLs. -->
[Visual Studio 2012 Express for Windows Phone]: https://go.microsoft.com/fwLink/p/?LinkID=268374
[알림 허브 지침]: http://msdn.microsoft.com/library/jj927170.aspx
[MPNS authenticated mode]: http://msdn.microsoft.com/library/windowsphone/develop/ff941099(v=vs.105).aspx
[사용 하 여 알림 허브 toopush 알림 toousers]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[최신 뉴스 사용 하 여 알림 허브 toosend]: notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md
[알림 카탈로그]: http://msdn.microsoft.com/library/windowsphone/develop/jj662938(v=vs.105).aspx
[타일 카탈로그]: http://msdn.microsoft.com/library/windowsphone/develop/hh202948(v=vs.105).aspx
[알림 허브-Windows Phone Silverlight 자습서]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToSLPhoneApp


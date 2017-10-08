---
title: "Azure 알림 허브에 대 한 Windows 유니버설 플랫폼 앱 aaaGet 시작 | Microsoft Docs"
description: "이 자습서에 설명 어떻게 toouse Azure 알림 허브 toopush 알림 tooa 유니버설 Windows 플랫폼 응용 프로그램입니다."
services: notification-hubs
documentationcenter: windows
author: ysxu
manager: erikre
editor: erikre
ms.assetid: cf307cf3-8c58-4628-9c63-8751e6a0ef43
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 11056842d205522ed493dc61c76ecf78ebb5a363
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-notification-hubs-for-windows-universal-platform-apps"></a>Windows 유니버설 플랫폼 앱용 Notification Hubs 시작
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>개요
이 자습서에서는 Azure 알림 허브 toosend toouse 밀어넣기 알림 tooa 유니버설 Windows 플랫폼 (UWP) 응용 프로그램입니다.

이 자습서에서는 Windows 푸시 알림 서비스 (WNS) hello를 사용 하 여 푸시 알림을 수신 하는 빈 Windows 스토어 앱을 만들 수 있습니다. 수 toouse 수 완료 되 면 알림 허브 toobroadcast 푸시 알림을 tooall hello 장치 앱을 실행 합니다.

## <a name="before-you-begin"></a>시작하기 전에
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

이 자습서를 완료 하는 hello 코드 GitHub에서 확인할 수 있습니다 [여기](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/GetStartedWindowsUniversal)합니다.

## <a name="prerequisites"></a>필수 조건
이 자습서는 hello 다음을 사항이 필요합니다.

* [Microsoft Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs) 이상 버전
* [유니버설 Windows 앱 개발 도구 설치](https://msdn.microsoft.com/windows/uwp/get-started/get-set-up)
* 활성 Azure 계정  <br/>계정이 없는 경우 몇 분 만에 무료 평가판 계정을 만들 수 있습니다. 자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-store-dotnet-get-started%2F)을 참조하세요.
* 활성 Windows 스토어 계정

이 자습서를 완료해야 다른 모든 Windows 유니버설 플랫폼 앱용 Notification Hubs 자습서를 진행할 수 있습니다.

## <a name="register-your-app-for-hello-windows-store"></a>Hello Windows 스토어에 앱 등록
toosend 푸시 알림을 tooUWP 응용 프로그램, Windows 스토어에 앱 toohello를 연결 해야 합니다. WNS 있는 알림 허브 toointegrate를 구성 해야 합니다.

1. 이미 앱을 등록 하지 않은 경우 탐색 toohello [Windows 개발자 센터](https://dev.windows.com/overview), Microsoft 계정으로 로그인 하 고 클릭 **새 앱 만들기**합니다.

2. 앱의 이름을 입력하고 **앱 이름 예약**을 클릭합니다. 이렇게 하면 앱을 새로 Windows 스토어에 등록하게 됩니다.

3. Visual Studio에서 유니버설 Windows hello를 사용 하 여 새 Visual C# 스토어 앱 프로젝트를 만들 **비어 있는 앱** 템플릿을 **확인**합니다.

4. Hello 대상과 최소 플랫폼 버전에 대 한 hello 기본값을 적용 합니다.

5. 솔루션 탐색기, 마우스 오른쪽 단추로 클릭 hello Windows 스토어 응용 프로그램 프로젝트에서에서 클릭 **저장소**, 클릭 하 고 **hello 저장소로 응용 프로그램 연결 중...** . hello **연결로 앱을 Windows 스토어 hello** 마법사가 나타납니다.

6. Hello 마법사에서 Microsoft 계정으로 로그인 합니다.

7. 2 단계에서 등록 된 hello 앱, **다음**, 클릭 하 고 **연결**합니다. 이 hello 필요한 Windows 스토어 등록 정보 toohello 응용 프로그램 매니페스트를 추가합니다.

8. Hello에 다시 [Windows 개발자 센터](http://dev.windows.com/overview) 새 앱에 대 한 페이지에서 클릭 **서비스**, 클릭 **푸시 알림**, 클릭 하 고 **WNS/MPNS**합니다.

9. **새 알림**을 클릭합니다.

10. **빈 값(알림)** 템플릿을 클릭하고 **확인**을 클릭합니다.

11. 알림 **이름** 및 시각적 **컨텍스트** 메시지를 입력합니다. 그런 후 **임시 저장**을 클릭합니다.

12. Toohello 이동 [응용 프로그램 등록 포털](http://apps.dev.microsoft.com) 로그인 하십시오.

13. 응용 프로그램 이름을 클릭합니다. Hello 메모 **응용 프로그램 암호** 암호 및 hello **패키지 보안 식별자 (SID)** hello에 **Windows 스토어** 플랫폼 설정 합니다.

     > [AZURE.WARNING]
    hello 응용 프로그램 암호와 패키지 SID는 중요 한 보안 자격 증명. 다른 사람과 공유하지 말고 앱과 함께 분산하지 마세요.

## <a name="configure-your-notification-hub"></a>알림 허브 구성
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">
<li><p>선택 hello <b>Notification Services</b> 옵션과 hello <b>WNS (Windows)</b> 옵션입니다. 다음 입력 hello <b>응용 프로그램 암호</b> hello에 암호 <b>보안 키</b> 필드입니다. 입력 프로그램 <b>패키지 SID</b> hello 이전 단원의 WNS에서 가져온을 클릭 한 다음 값 <b>저장</b>합니다.</p>
</li>
</ol>

&emsp;&emsp;![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-configure-wns.png)

알림 허브 이제 WNS와 함께 구성 된 toowork 이며 앱 hello 연결 문자열 tooregister 있어야 하 고 알림을 보낼 합니다.

## <a name="connect-your-app-toohello-notification-hub"></a>응용 프로그램 toohello 알림 허브를 연결 합니다.
1. Visual Studio에서 hello 솔루션을 마우스 오른쪽 단추로 클릭 하 고 클릭 **NuGet 패키지 관리**합니다.
   
    Hello 표시 **NuGet 패키지 관리** 대화 상자.
2. 검색할 `WindowsAzure.Messaging.Managed` 클릭 **설치**, hello 사용 약관을 수락 합니다.
   
    ![][20]
   
    다운로드이 설치 하 고 hello를 사용 하 여 Windows 용 참조 toohello Azure 메시징 라이브러리 추가 <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">WindowsAzure.Messaging.Managed NuGet 패키지</a>합니다.
3. Hello App.xaml.cs 프로젝트 파일을 열고 hello 다음 추가 `using` 문. 
   
        using Windows.Networking.PushNotifications;
        using Microsoft.WindowsAzure.Messaging;
        using Windows.UI.Popups;
4. 또한, App.xaml.cs에 hello 다음 추가 **InitNotificationsAsync** 메서드 정의 toohello **앱** 클래스:
   
        private async void InitNotificationsAsync()
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            var hub = new NotificationHub("< your hub name>", "<Your DefaultListenSharedAccessSignature connection string>");
            var result = await hub.RegisterNativeAsync(channel.Uri);
   
            // Displays hello registration ID so you know it was successful
            if (result.RegistrationId != null)
            {
                var dialog = new MessageDialog("Registration successful: " + result.RegistrationId);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
            }
   
        }
   
    이 코드는 WNS에서 hello 앱에 대 한 hello 채널 URI를 검색 하 고 알림 허브에 해당 채널 URI를 등록 합니다.
   
   > [!NOTE]
   > "허브 이름" hello Azure 포털에에서 표시 되는 hello 알림 허브의 hello 이름 자리 표시자 hello 있는지 tooreplace를 확인 합니다. 또한 hello로 hello 연결 문자열 자리 표시자를 대체 **DefaultListenSharedAccessSignature** 연결 문자열 hello에서 가져온 **액세스 정책은** 에서 알림 허브의 페이지는 이전 섹션입니다.
   > 
   > 
5. Hello의 hello 위쪽 **OnLaunched** App.xaml.cs, 이벤트 처리기 추가 호출 toohello 새 다음 hello **InitNotificationsAsync** 메서드:
   
        InitNotificationsAsync();
   
    이렇게 하면 해당 hello 채널 URI 각 시간 hello 응용 프로그램이 시작 하 여 알림 허브에 등록 됩니다.
6. 키를 눌러 hello **F5** 키 toorun hello 앱. Hello 등록 키를 포함 하는 팝업 대화 상자가 표시 됩니다.

이제 앱이 준비 tooreceive 알림 메시지입니다.

## <a name="send-notifications"></a>알림 보내기
Hello에 알림을 전송 하 여 앱에서 알림 받기 신속 하 게 테스트할 수 있습니다 [Azure 포털](https://portal.azure.com/) hello를 사용 하 여 **테스트 보내기** hello 화면 아래에 나와 있는 것 처럼 hello 알림 허브에서 단추가 있습니다.

![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-test-send-wns.png)

푸시 알림은 일반적으로 호환 라이브러리를 사용하는 Mobile Services 또는 ASP.NET과 같은 백 엔드 서비스에서 전송됩니다. 또한 toosend 알림 메시지는 라이브러리 백 엔드에 대해 사용할 수 없는 경우 직접 hello REST API를 사용할 수 있습니다. 

이 자습서에서는 단순하게 유지 하 고 방금 hello.NET SDK를 사용 하 여 백 엔드 서비스는 대신 콘솔 응용 프로그램에서 알림 허브에 대 한 알림을 전송 하 여 클라이언트 앱을 테스트를 설명 합니다. Hello 권장 [사용 하 여 알림 허브 toopush 알림 toousers] ASP.NET 백 엔드에서 알림을 보내기 위한 hello 다음 단계로 자습서입니다. 그러나 다음 방법 hello 알림을 보내는 데 사용할 수 있습니다.

* **REST 인터페이스**: hello를 사용 하 여 모든 백 엔드 플랫폼에서 알림을 지원할 수 있습니다 [REST 인터페이스](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx)합니다.
* **Microsoft Azure 알림 허브.NET SDK**: Visual Studio 용 Nuget 패키지 관리자 hello 실행 [Install-package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)합니다.
* **Node.js** : [어떻게 toouse Node.js에서 알림 허브](notification-hubs-nodejs-push-notification-tutorial.md)합니다.
* **Azure 모바일 앱**: 방법의 예에 대 한 알림 허브와 통합 되는 Azure 모바일 앱에서 알림을 toosend 참조 [모바일 앱에 대 한 푸시 알림 추가](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md)합니다.
* **Java / PHP**: toosend 알림을 사용 하 여 REST Api를 hello 하는 방법의 예제를 보려면 "어떻게 toouse Java/PHP에서 알림 허브" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).

## <a name="optional-send-notifications-from-a-console-app"></a>(선택 사항) 콘솔 응용 프로그램에서 알림 보내기
toosend 알림을.NET 콘솔 응용 프로그램을 사용 하 여 다음이 단계를 수행 합니다. 

1. 마우스 오른쪽 단추로 클릭 hello 솔루션을 선택 **추가** 및 **새 프로젝트...** , 그 다음 **Visual C#**, 클릭 **Windows** 및 **콘솔 응용 프로그램**를 클릭 하 고 **확인**합니다.
   
    이 새 Visual C# 콘솔 응용 프로그램 toohello 솔루션을 추가합니다. 별도의 솔루션에서 이 작업을 수행할 수도 있습니다.

2. Visual Studio에서 **도구**를 클릭하고 **NuGet 패키지 관리자**를 클릭한 다음 **패키지 관리자 콘솔**을 클릭합니다.
   
    Visual Studio에서 패키지 관리자 콘솔 hello 표시 됩니다.
3. Hello 패키지 관리자 콘솔 창에서에서 설정 hello **기본 프로젝트** tooyour 새 콘솔 응용 프로그램 프로젝트를 선택한 다음 hello 콘솔 창에 다음 명령을 hello를 실행 합니다.
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    이렇게 하면 추가 참조 toohello Azure 알림 허브 SDK hello를 사용 하 여 <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification 허브 NuGet 패키지</a>합니다.
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. Hello Program.cs 파일을 열고 hello 다음 추가 `using` 문:
   
        using Microsoft.Azure.NotificationHubs;
5. Hello에 **프로그램** 클래스, 메서드 뒤 hello 추가:
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient
                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">Hello from a .NET App!</text></binding></visual></toast>";
            await hub.SendWindowsNativeNotificationAsync(toast);
        }
   
       Make sure tooreplace hello "hub name" placeholder with hello name of hello notification hub that as it appears in hello Azure Portal. Also, replace hello connection string placeholder with hello **DefaultFullSharedAccessSignature** connection string that you obtained from hello **Access Policies** page of your Notification Hub in hello section called "Configure your notification hub."
   
   > [!NOTE]
   > Hello 연결 문자열을 사용 하 고 있는지 확인 **전체** 액세스 되지 **수신** 액세스 합니다. hello 수신 액세스 문자열에는 사용 권한을 toosend 알림이 없습니다.
   > 
   > 
6. Hello에 있는 줄을 다음 hello 추가 **Main** 메서드:
   
         SendNotificationAsync();
         Console.ReadLine();
7. Visual Studio에서 hello 콘솔 응용 프로그램 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 **시작 프로젝트로 설정** tooset hello 시작 프로젝트로 것입니다. Hello 키를 누릅니다 **F5** toorun hello 응용 프로그램 키입니다.
   
    그러면 등록된 모든 장치에 대한 알림 메시지를 수신하게 됩니다. 클릭 하거나 눌러 hello 알림을 배너 hello 앱을 로드합니다.

Hello에서 모든 지원 되는 hello 페이로드를 찾을 수 있습니다 [알림 카탈로그], [타일 카탈로그], 및 [개요 배지] msdn 항목.

## <a name="next-steps"></a>다음 단계
이 간단한 예제에서는 브로드캐스트 알림을 tooall hello 포털 또는 콘솔 응용 프로그램을 사용 하 여 Windows 장치를 보냈습니다. Hello 권장 [사용 하 여 알림 허브 toopush 알림 toousers] hello 다음 단계로 자습서입니다. 설명에서 사용 하 여 ASP.NET 백 엔드 toosend 알림을 tootarget 특정 사용자에 게 태그를 삽입 방법입니다.

Toosegment 관심 그룹으로 사용자, 참조 [최신 뉴스 사용 하 여 알림 허브 toosend]합니다. 

toolearn 알림 허브에 대 한 자세한 내용은 [알림 허브 지침](notification-hubs-push-notification-overview.md)합니다.

<!-- Images. -->
[13]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-create-console-app.png
[14]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-toast.png
[19]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-reg.png
[20]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-universal-app-install-package.png

<!-- URLs. -->

[사용 하 여 알림 허브 toopush 알림 toousers]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[최신 뉴스 사용 하 여 알림 허브 toosend]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md

[알림 카탈로그]: http://msdn.microsoft.com/library/windows/apps/hh761494.aspx
[타일 카탈로그]: http://msdn.microsoft.com/library/windows/apps/hh761491.aspx
[개요 배지]: http://msdn.microsoft.com/library/windows/apps/hh779719.aspx

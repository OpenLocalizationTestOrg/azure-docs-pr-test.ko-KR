---
title: "aaaAdd 푸시 알림 tooyour 유니버설 Windows 플랫폼 (UWP) 응용 프로그램 | Microsoft Docs"
description: "Azure 앱 서비스 모바일 앱 toouse 및 Azure 알림 허브 toosend 밀어넣기 알림 tooyour 유니버설 Windows 플랫폼 (UWP) 응용 프로그램에 알아봅니다."
services: app-service\mobile,notification-hubs
documentationcenter: windows
author: ysxu
manager: syntaxc4
editor: 
ms.assetid: 6de1b9d4-bd28-43e4-8db4-94cd3b187aa3
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: yuaxu
ms.openlocfilehash: 378ce59cab974830c0a3801108b24b30a21ae5cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-windows-app"></a>푸시 알림 tooyour Windows 앱 추가
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>개요
이 자습서에서는 푸시 알림을 toohello 추가한 [Windows 빠른 시작](app-service-mobile-windows-store-dotnet-get-started.md) 프로젝트 레코드가 삽입 될 때마다 푸시 알림을 toohello 장치 보내집니다.

사용 하지 않는 경우 hello 퀵 스타트 서버 프로젝트를 다운로드, 푸시 알림 확장 패키지 hello 필요 합니다. 참조 [Azure 모바일 앱에 대 한 hello.NET 백 엔드 서버 SDK에서 작동](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) 자세한 정보에 대 한 합니다.

## <a name="configure-hub"></a>알림 허브 구성
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="register-your-app-for-push-notifications"></a>푸시 알림에 대해 앱 등록
Windows 스토어에 앱 toohello toosubmit 필요한 서버 프로젝트 toointegrate toosend 푸시 알림 서비스 WNS (Windows) 구성 합니다.

1. Visual Studio 솔루션 탐색기, 마우스 오른쪽 단추로 클릭 hello UWP 앱 프로젝트에서에서 클릭 **저장소** > **hello 저장소로 응용 프로그램 연결 중...** .

    ![Windows 스토어에 응용 프로그램 연결](./media/app-service-mobile-windows-store-dotnet-get-started-push/notification-hub-associate-uwp-app.png)
2. Hello 마법사에서 **다음**, इ न क ा Microsoft ख에서 응용 프로그램에 대 한 이름을 입력 **새로운 앱 이름 예약**, 클릭 **예약**합니다.
3. Hello 앱 등록을 성공적으로 만든 hello 새로운 앱 이름 되 면 클릭 **다음**, 클릭 하 고 **연결**합니다. 이 hello 필요한 Windows 스토어 등록 정보 toohello 응용 프로그램 매니페스트를 추가합니다.  
4. Toohello 이동 [Windows 개발자 센터](https://dev.windows.com/en-us/overview), Microsoft 계정으로 로그인, 클릭 hello에 새 응용 프로그램 등록 **My apps**를 확장 한 다음 **서비스**  >  **푸시 알림**합니다.
5. Hello에 **푸시 알림** 페이지 **Live 서비스 사이트** 아래 **Microsoft Azure 모바일 서비스**합니다.
6. Hello 등록 페이지에 아래 hello 값 기록해 **응용 프로그램 암호** 및 hello **패키지 SID**이며 다음 사용할 tooconfigure 모바일 앱 백 합니다.

    ![Windows 스토어에 응용 프로그램 연결](./media/app-service-mobile-windows-store-dotnet-get-started-push/app-service-mobile-uwp-app-push-auth.png)

   > [!IMPORTANT]
   > hello 클라이언트 암호와 패키지 SID는 중요 한 보안 자격 증명. 다른 사람과 공유하지 말고 앱과 함께 분산하지 마세요. hello **응용 프로그램 Id** hello 비밀 tooconfigure Microsoft 계정 인증과 함께 사용 됩니다.
   >
   >

## <a name="configure-hello-backend-toosend-push-notifications"></a>Hello 백 엔드 toosend 푸시 알림 구성
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

## <a id="update-service"></a>업데이트 hello 서버 toosend 푸시 알림
백 엔드 프로젝트 형식과 일치 하는 hello 절차 아래를 사용 하 여&mdash;어느 [.NET 백 엔드](#dotnet) 또는 [Node.js 백 엔드](#nodejs)합니다.

### <a name="dotnet"></a>.NET 백 엔드 프로젝트
1. Visual Studio에서 hello 서버 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 **NuGet 패키지 관리**검색 Microsoft.Azure.NotificationHubs, 한 다음 클릭, **설치**합니다. Hello 알림 허브 클라이언트 라이브러리를 설치합니다.
2. 확장 **컨트롤러**TodoItemController.cs를 열고 hello 다음 추가 문을 사용 하 여:

        using System.Collections.Generic;
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.Mobile.Server.Config;
3. Hello에 **PostTodoItem** 메서드를 너무 hello 호출 후 코드를 다음 hello 추가**InsertAsync**:

        // Get hello settings for hello server project.
        HttpConfiguration config = this.Configuration;
        MobileAppSettingsDictionary settings =
            this.Configuration.GetMobileAppSettingsProvider().GetMobileAppSettings();

        // Get hello Notification Hubs credentials for hello Mobile App.
        string notificationHubName = settings.NotificationHubName;
        string notificationHubConnection = settings
            .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

        // Create hello notification hub client.
        NotificationHubClient hub = NotificationHubClient
            .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

        // Define a WNS payload
        var windowsToastPayload = @"<toast><visual><binding template=""ToastText01""><text id=""1"">"
                                + item.Text + @"</text></binding></visual></toast>";
        try
        {
            // Send hello push notification.
            var result = await hub.SendWindowsNativeNotificationAsync(windowsToastPayload);

            // Write hello success result toohello logs.
            config.Services.GetTraceWriter().Info(result.State.ToString());
        }
        catch (System.Exception ex)
        {
            // Write hello failure result toohello logs.
            config.Services.GetTraceWriter()
                .Error(ex.Message, null, "Push.SendAsync Error");
        }

    이 코드는 새 항목은 삽입 후 푸시 알림을 알림 허브 toosend hello를 지시 합니다.
4. Hello 서버 프로젝트를 다시 게시 합니다.

### <a name="nodejs"></a>Node.js 백 엔드 프로젝트
1. 따라서 아직 수행 하지 않은 경우 [hello 퀵 스타트 프로젝트를 다운로드](app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart) 하거나 다른 hello를 사용 하 여 [hello Azure 포털에서에서 온라인 편집기](app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor)합니다.
2. Hello 다음 hello hello todoitem.js 파일의 기존 코드를 바꿉니다.

        var azureMobileApps = require('azure-mobile-apps'),
        promises = require('azure-mobile-apps/src/utilities/promises'),
        logger = require('azure-mobile-apps/src/logger');

        var table = azureMobileApps.table();

        table.insert(function (context) {
        // For more information about hello Notification Hubs JavaScript SDK,
        // see http://aka.ms/nodejshubs
        logger.info('Running TodoItem.insert');

        // Define hello WNS payload that contains hello new item Text.
        var payload = "<toast><visual><binding template=\ToastText01\><text id=\"1\">"
                                    + context.item.text + "</text></binding></visual></toast>";

        // Execute hello insert.  hello insert returns hello results as a Promise,
        // Do hello push as a post-execute action within hello promise flow.
        return context.execute()
            .then(function (results) {
                // Only do hello push if configured
                if (context.push) {
                    // Send a WNS native toast notification.
                    context.push.wns.sendToast(null, payload, function (error) {
                        if (error) {
                            logger.error('Error while sending push notification: ', error);
                        } else {
                            logger.info('Push notification sent successfully!');
                        }
                    });
                }
                // Don't forget tooreturn hello results from hello context.execute()
                return results;
            })
            .catch(function (error) {
                logger.error('Error while running context.execute: ', error);
            });
        });

        module.exports = table;

    이 hello item.text 새 할 일 항목을 삽입 하는 경우 포함 된 WNS 알림을 메시지를 보냅니다.
3. 로컬 컴퓨터에 hello 파일을 편집할 때 hello 서버 프로젝트를 다시 게시 합니다.

## <a id="update-app"></a>푸시 알림 tooyour 앱 추가
다음으로 앱은 시작에서 푸시 알림에 등록해야 합니다. 인증을 이미 활성화 하는 경우 해당 hello 사용자가 로그인 tooregister ध 전에 있는지 확인 합니다.

1. 열기 hello **App.xaml.cs** 프로젝트 파일 및 hello 다음 추가 `using` 문:

        using System.Threading.Tasks;
        using Windows.Networking.PushNotifications;
2. 동일한 파일 hello 하 hello 다음 추가 **InitNotificationsAsync** 메서드 정의 toohello **앱** 클래스:

        private async Task InitNotificationsAsync()
        {
            // Get a channel URI from WNS.
            var channel = await PushNotificationChannelManager
                .CreatePushNotificationChannelForApplicationAsync();

            // Register hello channel URI with Notification Hubs.
            await App.MobileService.GetPush().RegisterAsync(channel.Uri);
        }

    이 코드는 WNS에서 hello 앱에 대 한 hello ChannelURI를 검색 하 고 만든 다음 해당 ChannelURI 앱 서비스 모바일 앱과 함께 등록 합니다.
3. Hello 위쪽 hello에 **OnLaunched** 의 이벤트 처리기 **App.xaml.cs**, hello 추가 **비동기** 한정자 toohello 메서드 정의 하 고 hello 다음 호출은 toohello 새 추가 **InitNotificationsAsync** hello 다음 예제와 같이 메서드를:

        protected async override void OnLaunched(LaunchActivatedEventArgs e)
        {
            await InitNotificationsAsync();

            // ...
        }

    이렇게 하면 해당 hello 수명이 짧은 ChannelURI hello 응용 프로그램이 시작 될 때마다 등록 됩니다.
4. UWP 앱 프로젝트를 다시 빌드합니다. 이제 앱이 준비 tooreceive 알림 메시지입니다.

## <a id="test"></a>앱에서 푸시 알림 테스트
[!INCLUDE [app-service-mobile-windows-universal-test-push](../../includes/app-service-mobile-windows-universal-test-push.md)]

## <a id="more"></a>다음 단계
푸시 알림에 대해 자세히 알아봅니다.

* [Toouse hello Azure 모바일 앱에 대 한 클라이언트를 관리 하는 방법](app-service-mobile-dotnet-how-to-use-client-library.md#pushnotifications)  
  서식 파일에는 유연성 toosend 플랫폼 간 푸시 및 지역화 된 푸시 제공합니다. 자세한 내용은 방법 tooregister 템플릿.
* [푸시 알림 문제 진단](../notification-hubs/notification-hubs-push-notification-fixer.md)  
  장치에서 알림이 삭제되거나 끝나지 않는 다양한 이유가 있습니다. 이 항목에서는 tooanalyze 및 hello 루트 계산 푸시 알림 오류의 발생 하는 방법을 보여 줍니다.

Tooone의 hello 다음 자습서를 계속 진행 하는 것이 좋습니다.

* [인증 tooyour 앱 추가](app-service-mobile-windows-store-dotnet-get-started-users.md)  
  자세한 내용은 방법 tooauthenticate 사용자가 id 공급자로 사용 하 여 앱의 합니다.
* [앱에 오프라인 동기화 사용](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  오프 라인 tooadd는 모바일 앱 백 엔드를 사용 하 여 앱을 지 원하는 방법에 대해 알아봅니다. 오프 라인 동기화 허용 모바일 앱과 함께 최종 사용자에 게 toointeract&mdash;보기, 추가 또는 데이터 수정&mdash;네트워크 연결이 없는 경우에 합니다.

<!-- Anchors. -->

<!-- URLs. -->
[Azure Portal]: https://portal.azure.com/

<!-- Images. -->

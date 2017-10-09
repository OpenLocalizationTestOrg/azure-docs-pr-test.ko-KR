이 섹션에서는 새 항목이 추가 될 때마다 기존 모바일 앱 백 엔드 프로젝트 toosend 푸시 알림 프로그램에서 코드를 업데이트 합니다. Hello 연결 된 값이 [템플릿](../articles/notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) 플랫폼 간 푸시를 사용 하도록 설정 되는 Azure 알림 허브의 기능입니다. hello 다양 한 클라이언트에 대해 등록 된 푸시 알림 템플릿을 사용 하 고 단일 유니버설 푸시 tooall 클라이언트 플랫폼 가져올 수 있습니다.

백 엔드 프로젝트 형식에 맞는 hello 다음 절차 중 하나를 선택&mdash;어느 [.NET 백 엔드](#dotnet) 또는 [Node.js 백 엔드](#nodejs)합니다.

### <a name="dotnet"></a>.NET 백 엔드 프로젝트
1. Visual Studio에서 hello 서버 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 **NuGet 패키지 관리**합니다. `Microsoft.Azure.NotificationHubs`를 검색한 다음 **설치**를 클릭합니다. 백 엔드에서 알림을 보내기 위한 hello 알림 허브 라이브러리를 설치 합니다.
2. Hello 서버 프로젝트를 열고 **컨트롤러** > **TodoItemController.cs**를 더하고 hello 다음 문을 사용 하 여:

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

        // Create a new Notification Hub client.
        NotificationHubClient hub = NotificationHubClient
        .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

        // Sending hello message so that all template registrations that contain "messageParam"
        // will receive hello notifications. This includes APNS, GCM, WNS, and MPNS template registrations.
        Dictionary<string,string> templateParams = new Dictionary<string,string>();
        templateParams["messageParam"] = item.Text + " was added toohello list.";

        try
        {
            // Send hello push notification and log hello results.
            var result = await hub.SendTemplateNotificationAsync(templateParams);

            // Write hello success result toohello logs.
            config.Services.GetTraceWriter().Info(result.State.ToString());
        }
        catch (System.Exception ex)
        {
            // Write hello failure result toohello logs.
            config.Services.GetTraceWriter()
                .Error(ex.Message, null, "Push.SendAsync Error");
        }

    Hello 항목을 포함 하는 템플릿 알림을 보냅니다. 새 항목이 삽입 될 때 텍스트입니다.
4. Hello 서버 프로젝트를 다시 게시 합니다.

### <a name="nodejs"></a>Node.js 백 엔드 프로젝트
1. 따라서 아직 수행 하지 않은 경우 [hello 퀵 스타트 백 엔드 프로젝트를 다운로드](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart), 하거나 다른 hello를 사용 하 여 [hello Azure 포털에서에서 온라인 편집기](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor)합니다.
2. Hello 다음 hello todoitem.js의 기존 코드를 바꿉니다.

        var azureMobileApps = require('azure-mobile-apps'),
        promises = require('azure-mobile-apps/src/utilities/promises'),
        logger = require('azure-mobile-apps/src/logger');

        var table = azureMobileApps.table();

        table.insert(function (context) {
        // For more information about hello Notification Hubs JavaScript SDK,
        // see http://aka.ms/nodejshubs
        logger.info('Running TodoItem.insert');

        // Define hello template payload.
        var payload = '{"messageParam": "' + context.item.text + '" }';  

        // Execute hello insert.  hello insert returns hello results as a Promise,
        // Do hello push as a post-execute action within hello promise flow.
        return context.execute()
            .then(function (results) {
                // Only do hello push if configured
                if (context.push) {
                    // Send a template notification.
                    context.push.send(null, payload, function (error) {
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

    새 항목이 삽입 될 때 hello item.text를 포함 하는 템플릿 알림을 보냅니다.
3. 로컬 컴퓨터에 hello 파일을 편집할 때 hello 서버 프로젝트를 다시 게시 합니다.

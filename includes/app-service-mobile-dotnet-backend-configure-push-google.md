백 엔드 프로젝트 형식에 맞는 hello 프로시저를 사용 하 여&mdash;어느 [.NET 백 엔드](#dotnet) 또는 [Node.js 백 엔드](#nodejs)합니다.

### <a name="dotnet"></a>.NET 백 엔드 프로젝트
1. Visual Studio에서 hello 서버 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 **NuGet 패키지 관리**합니다. `Microsoft.Azure.NotificationHubs`를 검색한 다음 **설치**를 클릭합니다. Hello 알림 허브 클라이언트 라이브러리를 설치합니다.
2. 안녕하세요 Controllers 폴더에서 TodoItemController.cs 열고 hello 다음 추가 `using` 문:

        using Microsoft.Azure.Mobile.Server.Config;
        using Microsoft.Azure.NotificationHubs;
3. Hello 대체 `PostTodoItem` 메서드 코드 다음 hello로:  

        public async Task<IHttpActionResult> PostTodoItem(TodoItem item)
        {
            TodoItem current = await InsertAsync(item);
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

            // Android payload
            var androidNotificationPayload = "{ \"data\" : {\"message\":\"" + item.Text + "\"}}";

            try
            {
                // Send hello push notification and log hello results.
                var result = await hub.SendGcmNativeNotificationAsync(androidNotificationPayload);

                // Write hello success result toohello logs.
                config.Services.GetTraceWriter().Info(result.State.ToString());
            }
            catch (System.Exception ex)
            {
                // Write hello failure result toohello logs.
                config.Services.GetTraceWriter()
                    .Error(ex.Message, null, "Push.SendAsync Error");
            }
            return CreatedAtRoute("Tables", new { id = current.Id }, current);
        }

4. Hello 서버 프로젝트를 다시 게시 합니다.

### <a name="nodejs"></a>Node.js 백 엔드 프로젝트
1. 따라서 아직 수행 하지 않은 경우 [hello 퀵 스타트 프로젝트를 다운로드](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart), 하거나 다른 hello를 사용 하 여 [hello Azure 포털에서에서 온라인 편집기](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor)합니다.
2. Hello 다음 hello hello todoitem.js 파일의 기존 코드를 바꿉니다.

        var azureMobileApps = require('azure-mobile-apps'),
        promises = require('azure-mobile-apps/src/utilities/promises'),
        logger = require('azure-mobile-apps/src/logger');

        var table = azureMobileApps.table();

        table.insert(function (context) {
        // For more information about hello Notification Hubs JavaScript SDK,
        // see http://aka.ms/nodejshubs
        logger.info('Running TodoItem.insert');

        // Define hello GCM payload.
        var payload = {
            "data": {
                "message": context.item.text
            }
        };   

        // Execute hello insert.  hello insert returns hello results as a Promise,
        // Do hello push as a post-execute action within hello promise flow.
        return context.execute()
            .then(function (results) {
                // Only do hello push if configured
                if (context.push) {
                    // Send a GCM native notification.
                    context.push.gcm.send(null, payload, function (error) {
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

    이 새 할 일 항목을 삽입할 때 hello item.text 포함 된 GCM 알림을 보냅니다.
3. 로컬 컴퓨터에 hello 파일을 편집할 때 hello 서버 프로젝트를 다시 게시 합니다.

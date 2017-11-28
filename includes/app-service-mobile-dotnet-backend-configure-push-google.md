<span data-ttu-id="d5424-101">백 엔드 프로젝트 형식&mdash;([.NET 백 엔드](#dotnet) 또는[ Node.js 백 엔드](#nodejs))과 일치하는 절차를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d5424-101">Use the procedure that matches your back-end project type&mdash;either [.NET back end](#dotnet) or [Node.js back end](#nodejs).</span></span>

### <span data-ttu-id="d5424-102"><a name="dotnet"></a>.NET 백 엔드 프로젝트</span><span class="sxs-lookup"><span data-stu-id="d5424-102"><a name="dotnet"></a>.NET back-end project</span></span>
1. <span data-ttu-id="d5424-103">Visual Studio에서 서버 프로젝트를 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d5424-103">In Visual Studio, right-click the server project, and click **Manage NuGet Packages**.</span></span> <span data-ttu-id="d5424-104">`Microsoft.Azure.NotificationHubs`를 검색한 다음 **설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d5424-104">Search for `Microsoft.Azure.NotificationHubs`, and then click **Install**.</span></span> <span data-ttu-id="d5424-105">알림 허브 클라이언트 라이브러리를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d5424-105">This installs the Notification Hubs client library.</span></span>
2. <span data-ttu-id="d5424-106">컨트롤러 폴더에서 TodoItemController.cs를 열고 다음 `using` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d5424-106">In the Controllers folder, open TodoItemController.cs and add the following `using` statements:</span></span>

        using Microsoft.Azure.Mobile.Server.Config;
        using Microsoft.Azure.NotificationHubs;
3. <span data-ttu-id="d5424-107">`PostTodoItem` 메서드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d5424-107">Replace the `PostTodoItem` method with the following code:</span></span>  

        public async Task<IHttpActionResult> PostTodoItem(TodoItem item)
        {
            TodoItem current = await InsertAsync(item);
            // Get the settings for the server project.
            HttpConfiguration config = this.Configuration;

            MobileAppSettingsDictionary settings =
                this.Configuration.GetMobileAppSettingsProvider().GetMobileAppSettings();

            // Get the Notification Hubs credentials for the Mobile App.
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
                // Send the push notification and log the results.
                var result = await hub.SendGcmNativeNotificationAsync(androidNotificationPayload);

                // Write the success result to the logs.
                config.Services.GetTraceWriter().Info(result.State.ToString());
            }
            catch (System.Exception ex)
            {
                // Write the failure result to the logs.
                config.Services.GetTraceWriter()
                    .Error(ex.Message, null, "Push.SendAsync Error");
            }
            return CreatedAtRoute("Tables", new { id = current.Id }, current);
        }

4. <span data-ttu-id="d5424-108">서버 프로젝트를 다시 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="d5424-108">Republish the server project.</span></span>

### <span data-ttu-id="d5424-109"><a name="nodejs"></a>Node.js 백 엔드 프로젝트</span><span class="sxs-lookup"><span data-stu-id="d5424-109"><a name="nodejs"></a>Node.js back-end project</span></span>
1. <span data-ttu-id="d5424-110">아직 수행하지 않은 경우 [빠른 시작 프로젝트를 다운로드](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart)하거나 [Azure Portal에서 온라인 편집기](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d5424-110">If you haven't already done so, [download the quickstart project](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart), or else use the [online editor in the Azure portal](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span></span>
2. <span data-ttu-id="d5424-111">todoitem.js 파일의 기존 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d5424-111">Replace the existing code in the todoitem.js file with the following:</span></span>

        var azureMobileApps = require('azure-mobile-apps'),
        promises = require('azure-mobile-apps/src/utilities/promises'),
        logger = require('azure-mobile-apps/src/logger');

        var table = azureMobileApps.table();

        table.insert(function (context) {
        // For more information about the Notification Hubs JavaScript SDK,
        // see http://aka.ms/nodejshubs
        logger.info('Running TodoItem.insert');

        // Define the GCM payload.
        var payload = {
            "data": {
                "message": context.item.text
            }
        };   

        // Execute the insert.  The insert returns the results as a Promise,
        // Do the push as a post-execute action within the promise flow.
        return context.execute()
            .then(function (results) {
                // Only do the push if configured
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
                // Don't forget to return the results from the context.execute()
                return results;
            })
            .catch(function (error) {
                logger.error('Error while running context.execute: ', error);
            });
        });

        module.exports = table;  

    <span data-ttu-id="d5424-112">이는 새 todo 항목이 삽입된 경우 item.text가 포함된 GCM 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d5424-112">This sends a GCM notification that contains the item.text when a new todo item is inserted.</span></span>
3. <span data-ttu-id="d5424-113">로컬 컴퓨터에서 파일을 편집할 때 서버 프로젝트를 다시 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="d5424-113">When editing the file in your local computer, republish the server project.</span></span>

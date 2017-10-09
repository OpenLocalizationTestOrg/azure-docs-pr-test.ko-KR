
* <span data-ttu-id="8863b-101">**.NET 백 엔드(C#)**:</span><span class="sxs-lookup"><span data-stu-id="8863b-101">**.NET backend (C#)**:</span></span>      
  
  1. <span data-ttu-id="8863b-102">Visual Studio에서 hello 서버 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 **NuGet 패키지 관리**, 검색할 `Microsoft.Azure.NotificationHubs`, 클릭 **설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="8863b-102">In Visual Studio, right-click hello server project and click **Manage NuGet Packages**, search for `Microsoft.Azure.NotificationHubs`, then click **Install**.</span></span> <span data-ttu-id="8863b-103">백 엔드에서 알림을 보내기 위한 hello 알림 허브 라이브러리를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="8863b-103">This installs hello Notification Hubs library for sending notifications from your backend.</span></span>
  2. <span data-ttu-id="8863b-104">Hello 백 엔드의 Visual Studio 프로젝트를 열고 **컨트롤러** > **TodoItemController.cs**합니다.</span><span class="sxs-lookup"><span data-stu-id="8863b-104">In hello backend's Visual Studio project, open **Controllers** > **TodoItemController.cs**.</span></span> <span data-ttu-id="8863b-105">Hello 파일의 hello 위쪽 hello 다음 추가 `using` 문:</span><span class="sxs-lookup"><span data-stu-id="8863b-105">At hello top of hello file, add hello following `using` statement:</span></span>
     
          using Microsoft.Azure.Mobile.Server.Config;
          using Microsoft.Azure.NotificationHubs;

    3. <span data-ttu-id="8863b-106">Hello 대체 `PostTodoItem` 메서드 코드 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="8863b-106">Replace hello `PostTodoItem` method with hello following code:</span></span>  

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

                // iOS payload
                var appleNotificationPayload = "{\"aps\":{\"alert\":\"" + item.Text + "\"}}";

                try
                {
                    // Send hello push notification and log hello results.
                    var result = await hub.SendAppleNativeNotificationAsync(appleNotificationPayload);

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

    4. <span data-ttu-id="8863b-107">Hello 서버 프로젝트를 다시 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="8863b-107">Republish hello server project.</span></span>

* <span data-ttu-id="8863b-108">**Node.js 백 엔드** :</span><span class="sxs-lookup"><span data-stu-id="8863b-108">**Node.js backend** :</span></span> 
  
  1. <span data-ttu-id="8863b-109">따라서 아직 수행 하지 않은 경우 [hello 퀵 스타트 프로젝트를 다운로드](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart) 하거나 다른 hello를 사용 하 여 [hello Azure 포털에서에서 온라인 편집기](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor)합니다.</span><span class="sxs-lookup"><span data-stu-id="8863b-109">If you haven't already done so, [download hello quickstart project](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart) or else use hello [online editor in hello Azure portal](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span></span>    
  2. <span data-ttu-id="8863b-110">Hello todoitem.js 테이블 스크립트를 코드 다음 hello로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="8863b-110">Replace hello todoitem.js table script with hello following code:</span></span>

            var azureMobileApps = require('azure-mobile-apps'),
                promises = require('azure-mobile-apps/src/utilities/promises'),
                logger = require('azure-mobile-apps/src/logger');

            var table = azureMobileApps.table();

            // When adding record, send a push notification via APNS
            table.insert(function (context) {
                // For details of hello Notification Hubs JavaScript SDK, 
                // see http://aka.ms/nodejshubs
                logger.info('Running TodoItem.insert');

                // Create a payload that contains hello new item Text.
                var payload = "{\"aps\":{\"alert\":\"" + context.item.text + "\"}}";

                // Execute hello insert; Push as a post-execute action when results are returned as a Promise.
                return context.execute()
                    .then(function (results) {
                        // Only do hello push if configured
                        if (context.push) {
                            context.push.apns.send(null, payload, function (error) {
                                if (error) {
                                    logger.error('Error while sending push notification: ', error);
                                } else {
                                    logger.info('Push notification sent successfully!');
                                }
                            });
                        }
                        return results;
                    })
                    .catch(function (error) {
                        logger.error('Error while running context.execute: ', error);
                    });
            });

            module.exports = table;

    2. <span data-ttu-id="8863b-111">로컬 컴퓨터에 hello 파일을 편집할 때 hello 서버 프로젝트를 다시 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="8863b-111">When editing hello file on your local computer, republish hello server project.</span></span>

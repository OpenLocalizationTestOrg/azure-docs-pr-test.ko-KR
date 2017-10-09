<span data-ttu-id="3df84-101">이 섹션에서는 새 항목이 추가 될 때마다 기존 모바일 앱 백 엔드 프로젝트 toosend 푸시 알림 프로그램에서 코드를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="3df84-101">In this section, you update code in your existing Mobile Apps back-end project toosend a push notification every time a new item is added.</span></span> <span data-ttu-id="3df84-102">Hello 연결 된 값이 [템플릿](../articles/notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) 플랫폼 간 푸시를 사용 하도록 설정 되는 Azure 알림 허브의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="3df84-102">This is powered by hello [template](../articles/notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) feature of Azure Notification Hubs, enabling cross-platform pushes.</span></span> <span data-ttu-id="3df84-103">hello 다양 한 클라이언트에 대해 등록 된 푸시 알림 템플릿을 사용 하 고 단일 유니버설 푸시 tooall 클라이언트 플랫폼 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3df84-103">hello various clients are registered for push notifications using templates, and a single universal push can get tooall client platforms.</span></span>

<span data-ttu-id="3df84-104">백 엔드 프로젝트 형식에 맞는 hello 다음 절차 중 하나를 선택&mdash;어느 [.NET 백 엔드](#dotnet) 또는 [Node.js 백 엔드](#nodejs)합니다.</span><span class="sxs-lookup"><span data-stu-id="3df84-104">Choose one of hello following procedures that matches your back-end project type&mdash;either [.NET back end](#dotnet) or [Node.js back end](#nodejs).</span></span>

### <span data-ttu-id="3df84-105"><a name="dotnet"></a>.NET 백 엔드 프로젝트</span><span class="sxs-lookup"><span data-stu-id="3df84-105"><a name="dotnet"></a>.NET back-end project</span></span>
1. <span data-ttu-id="3df84-106">Visual Studio에서 hello 서버 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="3df84-106">In Visual Studio, right-click hello server project and click **Manage NuGet Packages**.</span></span> <span data-ttu-id="3df84-107">`Microsoft.Azure.NotificationHubs`를 검색한 다음 **설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3df84-107">Search for `Microsoft.Azure.NotificationHubs`, and then click **Install**.</span></span> <span data-ttu-id="3df84-108">백 엔드에서 알림을 보내기 위한 hello 알림 허브 라이브러리를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="3df84-108">This installs hello Notification Hubs library for sending notifications from your back end.</span></span>
2. <span data-ttu-id="3df84-109">Hello 서버 프로젝트를 열고 **컨트롤러** > **TodoItemController.cs**를 더하고 hello 다음 문을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="3df84-109">In hello server project, open **Controllers** > **TodoItemController.cs**, and add hello following using statements:</span></span>

        using System.Collections.Generic;
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.Mobile.Server.Config;
3. <span data-ttu-id="3df84-110">Hello에 **PostTodoItem** 메서드를 너무 hello 호출 후 코드를 다음 hello 추가**InsertAsync**:</span><span class="sxs-lookup"><span data-stu-id="3df84-110">In hello **PostTodoItem** method, add hello following code after hello call too**InsertAsync**:</span></span>  

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

    <span data-ttu-id="3df84-111">Hello 항목을 포함 하는 템플릿 알림을 보냅니다. 새 항목이 삽입 될 때 텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="3df84-111">This sends a template notification that contains hello item.Text when a new item is inserted.</span></span>
4. <span data-ttu-id="3df84-112">Hello 서버 프로젝트를 다시 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="3df84-112">Republish hello server project.</span></span>

### <span data-ttu-id="3df84-113"><a name="nodejs"></a>Node.js 백 엔드 프로젝트</span><span class="sxs-lookup"><span data-stu-id="3df84-113"><a name="nodejs"></a>Node.js back-end project</span></span>
1. <span data-ttu-id="3df84-114">따라서 아직 수행 하지 않은 경우 [hello 퀵 스타트 백 엔드 프로젝트를 다운로드](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart), 하거나 다른 hello를 사용 하 여 [hello Azure 포털에서에서 온라인 편집기](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor)합니다.</span><span class="sxs-lookup"><span data-stu-id="3df84-114">If you haven't already done so, [download hello quickstart back-end project](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart), or else use hello [online editor in hello Azure portal](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span></span>
2. <span data-ttu-id="3df84-115">Hello 다음 hello todoitem.js의 기존 코드를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3df84-115">Replace hello existing code in todoitem.js with hello following:</span></span>

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

    <span data-ttu-id="3df84-116">새 항목이 삽입 될 때 hello item.text를 포함 하는 템플릿 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="3df84-116">This sends a template notification that contains hello item.text when a new item is inserted.</span></span>
3. <span data-ttu-id="3df84-117">로컬 컴퓨터에 hello 파일을 편집할 때 hello 서버 프로젝트를 다시 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="3df84-117">When editing hello file on your local computer, republish hello server project.</span></span>

## <a name="webapi-project"></a><span data-ttu-id="7f5b3-101">WebAPI 프로젝트</span><span class="sxs-lookup"><span data-stu-id="7f5b3-101">WebAPI Project</span></span>
1. <span data-ttu-id="7f5b3-102">Visual Studio에서 **사용자에게 알림** 자습서에서 만든 **AppBackend** 프로젝트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7f5b3-102">In Visual Studio, open the **AppBackend** project that you created in the **Notify Users** tutorial.</span></span>
2. <span data-ttu-id="7f5b3-103">Notifications.cs에서 전체 **Notifications** 클래스를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="7f5b3-103">In Notifications.cs, replace the whole **Notifications** class with the following code.</span></span> <span data-ttu-id="7f5b3-104">자리 표시자를 알림 허브에 대한 연결 문자열(모든 권한 사용) 및 허브 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="7f5b3-104">Be sure to replace the placeholders with your connection string (with full access) for your notification hub, and the hub name.</span></span> <span data-ttu-id="7f5b3-105">[Azure 클래식 포털](http://manage.windowsazure.com)에서 이러한 값을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5b3-105">You can obtain these values from the [Azure Classic Portal](http://manage.windowsazure.com).</span></span> <span data-ttu-id="7f5b3-106">이 모듈은 이제 전송할 다른 보안 알림을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="7f5b3-106">This module now represents the different secure notifications that will be sent.</span></span> <span data-ttu-id="7f5b3-107">완전한 구현에서 알림은 데이터베이스에 저장됩니다. 여기서는 단순화를 위해 메모리에 알림을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5b3-107">In a complete implementation, the notifications will be stored in a database; for simplicity, in this case we store them in memory.</span></span>
   
        public class Notification
        {
            public int Id { get; set; }
            public string Payload { get; set; }
            public bool Read { get; set; }
        }

        public class Notifications
        {
            public static Notifications Instance = new Notifications();

            private List<Notification> notifications = new List<Notification>();

            public NotificationHubClient Hub { get; set; }

            private Notifications() {
                Hub = NotificationHubClient.CreateClientFromConnectionString("{conn string with full access}",     "{hub name}");
            }

            public Notification CreateNotification(string payload)
            {
                var notification = new Notification() {
                Id = notifications.Count,
                Payload = payload,
                Read = false
                };

                notifications.Add(notification);

                return notification;
            }

            public Notification ReadNotification(int id)
            {
                return notifications.ElementAt(id);
            }
        }

1. <span data-ttu-id="7f5b3-108">NotificationsController.cs에서, **NotificationsController** 클래스 정의 내의 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="7f5b3-108">In NotificationsController.cs, replace the code inside the **NotificationsController** class definition with the following code.</span></span> <span data-ttu-id="7f5b3-109">이 구성 요소는 장치에서 알림을 안전하게 검색할 수 있는 방법을 구현하며, 이 자습서에서는 사용자가 자신의 장치로 보안 푸시를 트리거할 수 있는 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5b3-109">This component implements a way for the device to retrieve the notification securely, and also provides a way (for the purposes of this tutorial) to trigger a secure push to your devices.</span></span> <span data-ttu-id="7f5b3-110">알림 허브로 알림을 보낼 때에는 알림의 ID만 포함된 원시 알림(실제 메시지 없음)을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="7f5b3-110">Note that when sending the notification to the notification hub, we only send a raw notification with the ID of the notification (and no actual message):</span></span>
   
       public NotificationsController()
       {
           Notifications.Instance.CreateNotification("This is a secure notification!");
       }
   
       // GET api/notifications/id
       public Notification Get(int id)
       {
           return Notifications.Instance.ReadNotification(id);
       }
   
       public async Task<HttpResponseMessage> Post()
       {
           var secureNotificationInTheBackend = Notifications.Instance.CreateNotification("Secure confirmation.");
           var usernameTag = "username:" + HttpContext.Current.User.Identity.Name;
   
           // windows
           var rawNotificationToBeSent = new Microsoft.Azure.NotificationHubs.WindowsNotification(secureNotificationInTheBackend.Id.ToString(),
                           new Dictionary<string, string> {
                               {"X-WNS-Type", "wns/raw"}
                           });
           await Notifications.Instance.Hub.SendNotificationAsync(rawNotificationToBeSent, usernameTag);
   
           // apns
           await Notifications.Instance.Hub.SendAppleNativeNotificationAsync("{\"aps\": {\"content-available\": 1}, \"secureId\": \"" + secureNotificationInTheBackend.Id.ToString() + "\"}", usernameTag);
   
           // gcm
           await Notifications.Instance.Hub.SendGcmNativeNotificationAsync("{\"data\": {\"secureId\": \"" + secureNotificationInTheBackend.Id.ToString() + "\"}}", usernameTag);

            return Request.CreateResponse(HttpStatusCode.OK);
        }


<span data-ttu-id="7f5b3-111">이제 `Post` 메서드는 알림 메시지를 보내지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5b3-111">Note that the `Post` method now does not send a toast notification.</span></span> <span data-ttu-id="7f5b3-112">중요 콘텐츠가 아닌 알림 ID만 포함하는 원시 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="7f5b3-112">It sends a raw notification that contains only the notification ID, and not any sensitive content.</span></span> <span data-ttu-id="7f5b3-113">또한 알림 허브에서 자격 증명을 구성하지 않은 플랫폼에 대한 보내기 작업은 오류를 발생시키므로 이 작업을 주석으로 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5b3-113">Also, make sure to comment the send operation for the platforms for which you do not have credentials configured on your notification hub, as they will result in errors.</span></span>

1. <span data-ttu-id="7f5b3-114">이제 모든 장치에서 액세스할 수 있도록 이 앱을 Azure 웹 사이트에 다시 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5b3-114">Now we will re-deploy this app to an Azure Website in order to make it accessible from all devices.</span></span> <span data-ttu-id="7f5b3-115">**AppBackend** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **게시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5b3-115">Right-click on the **AppBackend** project and select **Publish**.</span></span>
2. <span data-ttu-id="7f5b3-116">Azure 웹 사이트를 게시 대상으로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5b3-116">Select Azure Website as your publish target.</span></span> <span data-ttu-id="7f5b3-117">Azure 계정으로 로그인하여 기존 또는 새로운 웹 사이트를 선택하며, **연결** 탭의 **대상 URL** 속성을 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5b3-117">Log in with your Azure account and select an existing or new Website, and make a note of the **destination URL** property in the **Connection** tab.</span></span> <span data-ttu-id="7f5b3-118">이 자습서의 뒷부분에서 이 URL을 *백 엔드 끝점* 이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5b3-118">We will refer to this URL as your *backend endpoint* later in this tutorial.</span></span> <span data-ttu-id="7f5b3-119">**게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5b3-119">Click **Publish**.</span></span>


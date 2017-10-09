## <a name="webapi-project"></a><span data-ttu-id="eedd1-101">WebAPI 프로젝트</span><span class="sxs-lookup"><span data-stu-id="eedd1-101">WebAPI Project</span></span>
1. <span data-ttu-id="eedd1-102">Visual Studio에서 열고 hello **AppBackend** hello에서 만든 프로젝트 **사용자에 게 알림** 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="eedd1-102">In Visual Studio, open hello **AppBackend** project that you created in hello **Notify Users** tutorial.</span></span>
2. <span data-ttu-id="eedd1-103">Notifications.cs, 대체 hello 전체에서 **알림** 코드 다음 hello 사용 하 여 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="eedd1-103">In Notifications.cs, replace hello whole **Notifications** class with hello following code.</span></span> <span data-ttu-id="eedd1-104">알림 허브 및 허브 이름을 hello에 대 한 (모든 권한)으로 연결 문자열이 있는지 tooreplace hello 자리 표시자 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eedd1-104">Be sure tooreplace hello placeholders with your connection string (with full access) for your notification hub, and hello hub name.</span></span> <span data-ttu-id="eedd1-105">Hello에서 이러한 값을 가져올 수 있습니다 [Azure 클래식 포털](http://manage.windowsazure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="eedd1-105">You can obtain these values from hello [Azure Classic Portal](http://manage.windowsazure.com).</span></span> <span data-ttu-id="eedd1-106">이 모듈에는 이제 hello 서로 다른 보안 알림을 보낼 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="eedd1-106">This module now represents hello different secure notifications that will be sent.</span></span> <span data-ttu-id="eedd1-107">완전 한 구현에서 hello 알림은; 데이터베이스에 저장 됩니다. 간단한 설명을 위해이 경우에서는 메모리에 저장할 합니다.</span><span class="sxs-lookup"><span data-stu-id="eedd1-107">In a complete implementation, hello notifications will be stored in a database; for simplicity, in this case we store them in memory.</span></span>
   
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

1. <span data-ttu-id="eedd1-108">NotificationsController.cs, 바꿉니다 hello 내부에서 코드를 hello **NotificationsController** 클래스 코드 다음 hello로 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="eedd1-108">In NotificationsController.cs, replace hello code inside hello **NotificationsController** class definition with hello following code.</span></span> <span data-ttu-id="eedd1-109">이 구성 요소는 hello 장치 tooretrieve hello 알림 방법을 안전 하 게 구현 하며 보안 밀어넣기 tooyour 장치 (용 hello이이 자습서의) 방식으로 tootrigger를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="eedd1-109">This component implements a way for hello device tooretrieve hello notification securely, and also provides a way (for hello purposes of this tutorial) tootrigger a secure push tooyour devices.</span></span> <span data-ttu-id="eedd1-110">Note는 hello 알림 toohello 알림 허브를 보낼 때만 원시 알림이 전송 hello ID 인 hello 알림 (및 실제 메시지):</span><span class="sxs-lookup"><span data-stu-id="eedd1-110">Note that when sending hello notification toohello notification hub, we only send a raw notification with hello ID of hello notification (and no actual message):</span></span>
   
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


<span data-ttu-id="eedd1-111">해당 hello 참고 `Post` 메서드 이제 알림을 보낼 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="eedd1-111">Note that hello `Post` method now does not send a toast notification.</span></span> <span data-ttu-id="eedd1-112">Hello 알림 ID만 중요 한 콘텐츠를 포함 하는 푸시 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="eedd1-112">It sends a raw notification that contains only hello notification ID, and not any sensitive content.</span></span> <span data-ttu-id="eedd1-113">또한 보내기 작업을 없는 알림 허브에 구성 된 자격 증명으로는 오류를 발생 하는 hello 플랫폼에 대 한 있는지 toocomment hello를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="eedd1-113">Also, make sure toocomment hello send operation for hello platforms for which you do not have credentials configured on your notification hub, as they will result in errors.</span></span>

1. <span data-ttu-id="eedd1-114">순서 toomake이 응용 프로그램 tooan Azure 웹 사이트를 다시 배포 됩니다에서는 이제는 모든 장치에서 액세스할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="eedd1-114">Now we will re-deploy this app tooan Azure Website in order toomake it accessible from all devices.</span></span> <span data-ttu-id="eedd1-115">Hello를 마우스 오른쪽 단추로 클릭 **AppBackend** 프로젝트를 마우스 선택 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="eedd1-115">Right-click on hello **AppBackend** project and select **Publish**.</span></span>
2. <span data-ttu-id="eedd1-116">Azure 웹 사이트를 게시 대상으로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="eedd1-116">Select Azure Website as your publish target.</span></span> <span data-ttu-id="eedd1-117">Azure 계정으로 로그인을 기존 또는 새 웹 사이트를 선택 하 고 hello 메모 **대상 URL** hello에 대 한 속성 **연결** 탭 합니다. 다음 URL로 toothis 이라고 합니다 프로그램 *백 엔드 끝점* 이 자습서의 뒷부분에 나오는 합니다.</span><span class="sxs-lookup"><span data-stu-id="eedd1-117">Log in with your Azure account and select an existing or new Website, and make a note of hello **destination URL** property in hello **Connection** tab. We will refer toothis URL as your *backend endpoint* later in this tutorial.</span></span> <span data-ttu-id="eedd1-118">**게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="eedd1-118">Click **Publish**.</span></span>


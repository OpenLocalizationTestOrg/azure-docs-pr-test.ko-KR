## <a name="webapi-project"></a>WebAPI 프로젝트
1. Visual Studio에서 열고 hello **AppBackend** hello에서 만든 프로젝트 **사용자에 게 알림** 자습서입니다.
2. Notifications.cs, 대체 hello 전체에서 **알림** 코드 다음 hello 사용 하 여 클래스입니다. 알림 허브 및 허브 이름을 hello에 대 한 (모든 권한)으로 연결 문자열이 있는지 tooreplace hello 자리 표시자 수 있습니다. Hello에서 이러한 값을 가져올 수 있습니다 [Azure 클래식 포털](http://manage.windowsazure.com)합니다. 이 모듈에는 이제 hello 서로 다른 보안 알림을 보낼 나타냅니다. 완전 한 구현에서 hello 알림은; 데이터베이스에 저장 됩니다. 간단한 설명을 위해이 경우에서는 메모리에 저장할 합니다.
   
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

1. NotificationsController.cs, 바꿉니다 hello 내부에서 코드를 hello **NotificationsController** 클래스 코드 다음 hello로 정의 합니다. 이 구성 요소는 hello 장치 tooretrieve hello 알림 방법을 안전 하 게 구현 하며 보안 밀어넣기 tooyour 장치 (용 hello이이 자습서의) 방식으로 tootrigger를 제공 합니다. Note는 hello 알림 toohello 알림 허브를 보낼 때만 원시 알림이 전송 hello ID 인 hello 알림 (및 실제 메시지):
   
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


해당 hello 참고 `Post` 메서드 이제 알림을 보낼 하지 않습니다. Hello 알림 ID만 중요 한 콘텐츠를 포함 하는 푸시 알림을 보냅니다. 또한 보내기 작업을 없는 알림 허브에 구성 된 자격 증명으로는 오류를 발생 하는 hello 플랫폼에 대 한 있는지 toocomment hello를 확인 합니다.

1. 순서 toomake이 응용 프로그램 tooan Azure 웹 사이트를 다시 배포 됩니다에서는 이제는 모든 장치에서 액세스할 수 있게 합니다. Hello를 마우스 오른쪽 단추로 클릭 **AppBackend** 프로젝트를 마우스 선택 **게시**합니다.
2. Azure 웹 사이트를 게시 대상으로 선택합니다. Azure 계정으로 로그인을 기존 또는 새 웹 사이트를 선택 하 고 hello 메모 **대상 URL** hello에 대 한 속성 **연결** 탭 합니다. 다음 URL로 toothis 이라고 합니다 프로그램 *백 엔드 끝점* 이 자습서의 뒷부분에 나오는 합니다. **게시**를 클릭합니다.


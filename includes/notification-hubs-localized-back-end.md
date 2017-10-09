



속성 집합이 tooprovide 하기만 하면 템플릿 알림을 보낼 때 경우에 메일이 hello 집합 예를 들어 hello hello 현재 뉴스의 지역화 된 버전을 포함 한 속성

    {
        "News_English": "World News in English!",
        "News_French": "World News in French!",
        "News_Mandarin": "World News in Mandarin!"
    }


이 섹션에서는 어떻게 콘솔 응용 프로그램을 사용 하 여 toosend 알림

hello는 hello 백 엔드 지원 hello 장치의 tooany 브로드캐스트할 수 있으므로 코드 브로드캐스트 tooboth Windows 스토어 및 iOS 장치를 포함 합니다.

### <a name="toosend-notifications-using-a-c-console-app"></a>C# 콘솔 응용 프로그램을 사용 하 여 toosend 알림
Hello 수정 `SendTemplateNotificationAsync` 코드 다음 hello를 사용 하 여 이전에 만든 hello 콘솔 응용 프로그램에서 메서드. 어떻게이 경우에 포함 되어 있음을 알 필요가 toosend 없습니다 다른 로캘 및 플랫폼에 대해 여러 알림을 합니다.

        private static async void SendTemplateNotificationAsync()
        {
            // Define hello notification hub.
            NotificationHubClient hub = 
                NotificationHubClient.CreateClientFromConnectionString(
                    "<connection string with full access>", "<hub name>");

            // Sending hello notification as a template notification. All template registrations that contain 
            // "messageParam" or "News_<local selected>" and hello proper tags will receive hello notifications. 
            // This includes APNS, GCM, WNS, and MPNS template registrations.
            Dictionary<string, string> templateParams = new Dictionary<string, string>();

            // Create an array of breaking news categories.
            var categories = new string[] { "World", "Politics", "Business", "Technology", "Science", "Sports"};
            var locales = new string[] { "English", "French", "Mandarin" };

            foreach (var category in categories)
            {
                templateParams["messageParam"] = "Breaking " + category + " News!";

                // Sending localized News for each tag too...
                foreach( var locale in locales)
                {
                    string key = "News_" + locale;

                    // Your real localized news content would go here.
                    templateParams[key] = "Breaking " + category + " News in " + locale + "!";
                }

                await hub.SendTemplateNotificationAsync(templateParams, category);
            }
        }


이 간단한 호출은 hello 지역화 된 부분의 뉴스를 너무 실현 될 것에 유의**모든** hello 플랫폼에 관계 없이 장치에 알림 허브를 작성 하 고 배달 hello 올바른 네이티브 페이로드 tooall hello 장치 등록 tooa 특정 태그입니다.

### <a name="sending-hello-notification-with-mobile-services"></a>모바일 서비스는 hello 알림을 보내기
사용자의 모바일 서비스 스케줄러 hello 다음 스크립트를 사용할 수 있습니다.

    var azure = require('azure');
    var notificationHubService = azure.createNotificationHubService('<hub name>', '<connection string with full access>');
    var notification = {
            "News_English": "World News in English!",
            "News_French": "World News in French!",
            "News_Mandarin", "World News in Mandarin!"
    }
    notificationHubService.send('World', notification, function(error) {
        if (!error) {
            console.warn("Notification successful");
        }
    });



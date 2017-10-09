



<span data-ttu-id="f32bf-101">속성 집합이 tooprovide 하기만 하면 템플릿 알림을 보낼 때 경우에 메일이 hello 집합 예를 들어 hello hello 현재 뉴스의 지역화 된 버전을 포함 한 속성</span><span class="sxs-lookup"><span data-stu-id="f32bf-101">When you send template notifications you only need tooprovide a set of properties, in our case we will send hello set of properties containing hello localized version of hello current news, for instance:</span></span>

    {
        "News_English": "World News in English!",
        "News_French": "World News in French!",
        "News_Mandarin": "World News in Mandarin!"
    }


<span data-ttu-id="f32bf-102">이 섹션에서는 어떻게 콘솔 응용 프로그램을 사용 하 여 toosend 알림</span><span class="sxs-lookup"><span data-stu-id="f32bf-102">This section shows how toosend notifications using a console app</span></span>

<span data-ttu-id="f32bf-103">hello는 hello 백 엔드 지원 hello 장치의 tooany 브로드캐스트할 수 있으므로 코드 브로드캐스트 tooboth Windows 스토어 및 iOS 장치를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="f32bf-103">hello included code broadcasts tooboth Windows Store and iOS devices, since hello backend can broadcast tooany of hello supported devices.</span></span>

### <a name="toosend-notifications-using-a-c-console-app"></a><span data-ttu-id="f32bf-104">C# 콘솔 응용 프로그램을 사용 하 여 toosend 알림</span><span class="sxs-lookup"><span data-stu-id="f32bf-104">toosend notifications using a C# console app</span></span>
<span data-ttu-id="f32bf-105">Hello 수정 `SendTemplateNotificationAsync` 코드 다음 hello를 사용 하 여 이전에 만든 hello 콘솔 응용 프로그램에서 메서드.</span><span class="sxs-lookup"><span data-stu-id="f32bf-105">Modify hello `SendTemplateNotificationAsync` method in hello console app you previously created with hello following code.</span></span> <span data-ttu-id="f32bf-106">어떻게이 경우에 포함 되어 있음을 알 필요가 toosend 없습니다 다른 로캘 및 플랫폼에 대해 여러 알림을 합니다.</span><span class="sxs-lookup"><span data-stu-id="f32bf-106">Notice how in this case there is no need toosend multiple notifications for different locales and platforms.</span></span>

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


<span data-ttu-id="f32bf-107">이 간단한 호출은 hello 지역화 된 부분의 뉴스를 너무 실현 될 것에 유의**모든** hello 플랫폼에 관계 없이 장치에 알림 허브를 작성 하 고 배달 hello 올바른 네이티브 페이로드 tooall hello 장치 등록 tooa 특정 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="f32bf-107">Note that this simple call will deliver hello localized piece of news too**all** your devices, irrespective of hello platform, as your Notification Hub builds and delivers hello correct native payload tooall hello devices subscribed tooa specific tag.</span></span>

### <a name="sending-hello-notification-with-mobile-services"></a><span data-ttu-id="f32bf-108">모바일 서비스는 hello 알림을 보내기</span><span class="sxs-lookup"><span data-stu-id="f32bf-108">Sending hello notification with Mobile Services</span></span>
<span data-ttu-id="f32bf-109">사용자의 모바일 서비스 스케줄러 hello 다음 스크립트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f32bf-109">In your Mobile Service scheduler, you can use hello following script:</span></span>

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



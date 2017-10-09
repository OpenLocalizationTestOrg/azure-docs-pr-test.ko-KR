
이 섹션에서는 최신 뉴스도 toosend 태그가.NET 콘솔 응용 프로그램에서 템플릿 알림을 지정 하는 방법을 보여 줍니다.

모바일 앱을 사용 하는 경우 toohello를 참조 하십시오 [모바일 앱에 대 한 푸시 알림 추가] 자습서 hello 위쪽에 플랫폼을 선택 하 고 있습니다.

Toouse Java 또는 PHP 너무 참조[어떻게 toouse Java/PHP에서 알림 허브]합니다. [Notification Hubs REST 인터페이스]를 사용하여 아무 백 엔드에서나 알림을 보낼 수 있습니다.

Skip 완료 알림을 보내기 위한 hello 콘솔 응용 프로그램을 만든 경우 1-3 단계 [알림 허브 시작]합니다.

1. Visual Studio에서 다음과 같이 새로운 Visual C# 콘솔 응용프로그램을 만듭니다.
   
       ![][13]
2. Hello Visual Studio 주 메뉴에서 클릭 **도구**, **라이브러리 패키지 관리자**, 및 **패키지 관리자 콘솔**다음 hello 콘솔 창에서를 입력 한 다음 키를 누릅니다 **입력**:
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    이렇게 하면 추가 참조 toohello Azure 알림 허브 SDK hello를 사용 하 여 [Microsoft.Azure.Notification 허브 NuGet 패키지]합니다.
3. Hello 파일 Program.cs를 열고 hello 다음 추가 `using` 문:
   
        using Microsoft.Azure.NotificationHubs;
4. Hello에 `Program` 클래스, 메서드를 다음 hello를 추가 하거나 이미 있는 경우 대체:
   
        private static async void SendTemplateNotificationAsync()
        {
            // Define hello notification hub.
            NotificationHubClient hub =
                NotificationHubClient.CreateClientFromConnectionString(
                    "<connection string with full access>", "<hub name>");
   
            // Create an array of breaking news categories.
            var categories = new string[] { "World", "Politics", "Business",
                                            "Technology", "Science", "Sports"};
   
            // Sending hello notification as a template notification. All template registrations that contain
            // "messageParam" and hello proper tags will receive hello notifications.
            // This includes APNS, GCM, WNS, and MPNS template registrations.
   
            Dictionary<string, string> templateParams = new Dictionary<string, string>();
   
            foreach (var category in categories)
            {
                templateParams["messageParam"] = "Breaking " + category + " News!";
                await hub.SendTemplateNotificationAsync(templateParams, category);
            }
         }
   
    이 코드는 hello hello 문자열 배열에서 6 개의 태그의 각 템플릿 알림을 보냅니다. 태그의 hello를 사용 하면 장치 등록 hello 범주에 대 한 알림을 받도록 합니다.
5. 코드 위의 hello, 바꿉니다 hello `<hub name>` 및 `<connection string with full access>` 와 알림 허브 이름 및 hello 연결 문자열에 대 한 자리 표시자 *DefaultFullSharedAccessSignature* 알림 허브의 hello 대시보드에서 .
6. Hello에 있는 줄을 다음 hello 추가 **Main** 메서드:
   
         SendTemplateNotificationAsync();
         Console.ReadLine();
7. Hello 콘솔 응용 프로그램을 빌드하십시오.

<!-- Images. -->
[13]: ./media/notification-hubs-back-end/notification-hub-create-console-app.png

<!-- URLs. -->
[알림 허브 시작]: ../articles/notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md
[Notification Hubs REST 인터페이스]: http://msdn.microsoft.com/library/windowsazure/dn223264.aspx
[모바일 앱에 대 한 푸시 알림 추가]: ../articles/app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md
[어떻게 toouse Java/PHP에서 알림 허브]: ../articles/notification-hubs/notification-hubs-java-push-notification-tutorial.md
[Microsoft.Azure.Notification 허브 NuGet 패키지]: http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/

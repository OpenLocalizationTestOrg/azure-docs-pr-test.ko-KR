---
title: "aaaNotification 허브-엔터프라이즈 푸시 아키텍처"
description: "엔터프라이즈 환경에서 Azure 알림 허브 사용에 대한 지침"
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 903023e9-9347-442a-924b-663af85e05c6
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: c3afb83de1ba0882bf99e10f38cca40cb42d07a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enterprise-push-architectural-guidance"></a>엔터프라이즈 푸시 아키텍처 지침
오늘 기업에서는 최종 사용자에 게 (외부)에 맞게 모바일 응용 프로그램을 만들 때 또는 hello 직원 (내부)에 대 한 점차적으로 이동 하는 합니다. 기존 백 엔드 시스템을 제대로 메인프레임 컴퓨터 수 나 일부 LoB 응용 프로그램에 통합 해야 하는 모바일 응용 프로그램 아키텍처 hello 합니다. 이 가이드는 toocommon 시나리오 가능한 솔루션을 권장 해 주므로이 통합 toodo 최선의 방법에 대 한 설명 합니다.

자주 요구 사항은 전송용 푸시 알림 toohello 사용자의 모바일 응용 프로그램을 통해 hello 백 엔드 시스템에서 관련 이벤트 발생입니다. 예: 그녀의 iPhone에 있는 hello 은행의 은행 업무용 앱은 은행 고객이 원하는 toobe 일정량의 계정 또는 여기서 자신의 Windows Phone 대해 예산 승인 응용 프로그램을 가진 직원 재무 부서에서가 toobe 인트라넷 시나리오에서 위에 debit 만들어지면 알림이 표시 그 승인 요청을 가져올 때 알림을 받습니다.

hello 은행 계좌 또는 승인 처리에 밀어넣기 toohello 사용자를 초기화 해야 하는 일부 백 엔드 시스템에서 수행 하는 가능성이 toobe입니다. 이러한 여러 백 엔드 있을 수 있습니다는 이벤트 알림을 트리거할 때 모든 빌드 해야 하는 시스템 hello 같은 종류의 논리 tooimplement 푸시 합니다. 여기에 hello 복잡성은 최종 사용자 toodifferent 알림 구독 수 있습니다.와 될 수 있습니다 hello 인트라넷 모바일 앱의 hello 경우의 예를 들어 여러 모바일 응용 프로그램 수 있는 단일 밀어넣기 시스템 함께 여러 백 엔드 시스템 통합에서 찾을 수 여기서 한 모바일 응용 프로그램 이러한 여러 백 엔드 시스템에서 tooreceive 알림을 내보낼 수 있습니다. hello 백 엔드 시스템 알고 하지 않거나 push 기술의 의미 체계/tooknow 일반적인 솔루션은 일반적으로 되었습니다 toointroduce 관심 있는 모든 이벤트에 대 한 백 엔드 시스템 hello 폴링한 hello 푸시 메시지를 보내기 위한를 담당 하는 구성 요소 필요 toohello 클라이언트입니다.
여기 Azure 서비스 버스 확장 가능한 hello 솔루션을 만들면서 hello 복잡성을 줄일 수 있는 항목/구독 모델을 사용 하 여 보다 나은 해결책 방법을 설명 합니다.

Hello 솔루션의 일반 아키텍처 hello 다음과 같습니다 (일반화 된 여러 모바일 앱 사용 하지만 모바일 응용 프로그램을 하나의 경우에 동일 하 게 적용할 수)

## <a name="architecture"></a>아키텍처
![][1]

hello 주요이 아키텍처 다이어그램에는 Azure 서비스 버스 항목/구독 프로그래밍 모델을 제공 하는 (에서에 더 [서비스 버스 Pub/Sub 프로그래밍]). hello 모바일 백 엔드에이 경우에 hello 수신기 (일반적으로 [Azure 모바일 서비스], 푸시 toohello 모바일 앱을 시작 합니다는) hello 백 엔드 시스템에서 직접 메시지를 수신 하지 않지만 대신 했으므로 제공 하는 중간 추상화 계층 [Azure 서비스 버스] 모바일 백 엔드 tooreceive 메시지 하나 이상의 백 엔드 시스템에서 할 수 있게 합니다. 서비스 버스 항목 hello 백 엔드 시스템의 예: 계정에는 기본적으로 "항목"으로 푸시 알림을 전송 하는 메시지 toobe 시작 있는 관심 있는 Finance, HR 각각에 대해 만든 toobe가 필요 합니다. hello 백 엔드 시스템에서 메시지를 보낼 toothese 항목입니다. 모바일 백 엔드 서비스 버스 구독을 만들어 tooone 또는 더 등의 항목을 구독할 수 있습니다. 이 인해 hello 모바일 백 엔드 tooreceive hello 해당 백 엔드 시스템에서 알림의 권한을 부여한 다음 됩니다. 모바일 백 엔드 toolisten 메시지에 대 한 구독에서 계속 해 서 및 메시지가 도착 하는 즉시 다시 설정 및 알림 tooits 알림 허브로 보냅니다. 알림 허브 결국 파일을 전달 하 hello 메시지 toohello 모바일 앱입니다. Toosummarize hello 주요 구성 요소를 사용해 보도록 하겠습니다.

1. 백엔드 시스템(LoB/레거시 시스템)
   * 서비스 버스 항목 만들기
   * 메시지 보내기
2. 모바일 백엔드
   * 서비스 구독 만들기
   * 메시지 받기(백엔드 시스템에서)
   * 알림 tooclients를 (Azure 알림 허브)를 통해 보냅니다.
3. 모바일 응용 프로그램
   * 알림 수신 및 표시

### <a name="benefits"></a>이점:
1. hello hello 수신기 (모바일 응용 프로그램/서비스 알림 허브를 통해) 및 보낸 사람 (백 엔드 시스템) 확장점 거의 변경 하지 않고도과 통합 되는 추가 백 엔드 시스템 수 있습니다.
2. 하나 이상의 백 엔드 시스템에서 수 tooreceive 이벤트 되는 여러 모바일 앱의 hello 시나리오를 따라서 있습니다.  

## <a name="sample"></a>샘플:
### <a name="prerequisites"></a>필수 조건
Hello 자습서 toofamiliarize hello 개념 뿐 아니라 공통 만들기 및 구성 단계에 따라 완료 해야 합니다.

1. [서비스 버스 Pub/Sub 프로그래밍] -서비스 버스 항목/구독와 작업의 hello 세부 정보를 어떻게 이런 toocreate 네임 스페이스 toocontain 항목/구독, 어떻게 toosend & 임원의 메시지를 수신 합니다.
2. [알림 허브-Windows 유니버설 자습서] -방법을 tooset를 Windows 스토어 앱 및 사용 하 여 알림 허브 tooregister 다음 알림을 받을 설명 합니다.

### <a name="sample-code"></a>샘플 코드
hello 전체 샘플 코드에서 사용할 수는 [알림 허브 샘플]합니다. 세 가지 구성 요소로 구성되어 있습니다.

1. **EnterprisePushBackendSystem**
   
    a. 이 프로젝트 hello를 사용 하 여 *WindowsAzure.ServiceBus* Nuget 패키지에 따라 [서비스 버스 Pub/Sub 프로그래밍]합니다.
   
    b. 간단한 C# 콘솔 응용 프로그램 toosimulate hello 메시지 toobe 배달 toohello 모바일 앱을 시작 하는 LoB 시스템입니다.
   
        static void Main(string[] args)
        {
            string connectionString =
                CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");
   
            // Create hello topic where we will send notifications
            CreateTopic(connectionString);
   
            // Send message
            SendMessage(connectionString);
        }
   
    c. `CreateTopic`메시지를 발송 될 것 사용 되는 toocreate hello 서비스 버스 항목이입니다.
   
        public static void CreateTopic(string connectionString)
        {
            // Create hello topic if it does not exist already
   
            var namespaceManager =
                NamespaceManager.CreateFromConnectionString(connectionString);
   
            if (!namespaceManager.TopicExists(sampleTopic))
            {
                namespaceManager.CreateTopic(sampleTopic);
            }
        }
   
    d. `SendMessage`가 사용 되는 toosend hello 메시지 toothis 서비스 버스 항목입니다. 여기 hello 샘플의 hello 목적을 위해 주기적으로 임의 메시지 toohello 항목 집합이 전송 됩니다. 일반적으로 이벤트가 발생하면 메시지를 보내는 백엔드 시스템이 됩니다.
   
        public static void SendMessage(string connectionString)
        {
            TopicClient client =
                TopicClient.CreateFromConnectionString(connectionString, sampleTopic);
   
            // Sends random messages every 10 seconds toohello topic
            string[] messages =
            {
                "Employee Id '{0}' has joined.",
                "Employee Id '{0}' has left.",
                "Employee Id '{0}' has switched tooa different team."
            };
   
            while (true)
            {
                Random rnd = new Random();
                string employeeId = rnd.Next(10000, 99999).ToString();
                string notification = String.Format(messages[rnd.Next(0,messages.Length)], employeeId);
   
                // Send Notification
                BrokeredMessage message = new BrokeredMessage(notification);
                client.Send(message);
   
                Console.WriteLine("{0} Message sent - '{1}'", DateTime.Now, notification);
   
                System.Threading.Thread.Sleep(new TimeSpan(0, 0, 10));
            }
        }
2. **ReceiveAndSendNotification**
   
    a. 이 프로젝트 hello를 사용 하 여 *WindowsAzure.ServiceBus* 및 *Microsoft.Web.WebJobs.Publish* Nuget 패키지와 기반 [서비스 버스 Pub/Sub 프로그래밍]합니다.
   
    b. 이것은 다른 C# 콘솔 응용 프로그램으로 실행 한 [Azure WebJob] toolisten에 대 한 hello LoB/백 엔드 시스템에서 메시지를 지속적으로 toorun에 있기 때문입니다. 모바일 백엔드의 일부가 됩니다.
   
        static void Main(string[] args)
        {
            string connectionString =
                     CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");
   
            // Create hello subscription which will receive messages
            CreateSubscription(connectionString);
   
            // Receive message
            ReceiveMessageAndSendNotification(connectionString);
        }
   
    c. `CreateSubscription`가 사용 되는 toocreate hello 항목에 대 한 서비스 버스 구독 hello 백 엔드 시스템에서 메시지를 보낼 위치입니다. Hello 비즈니스 시나리오에 따라이 구성 요소는 항목을 만들어 하나 이상의 구독 toocorresponding (예: 일부에서 수신할 수 있습니다 메시지 재무 시스템에서 일부 HR 시스템)
   
        static void CreateSubscription(string connectionString)
        {
            // Create hello subscription if it does not exist already
            var namespaceManager =
                NamespaceManager.CreateFromConnectionString(connectionString);
   
            if (!namespaceManager.SubscriptionExists(sampleTopic, sampleSubscription))
            {
                namespaceManager.CreateSubscription(sampleTopic, sampleSubscription);
            }
        }
   
    d. ReceiveMessageAndSendNotification 오케스트레이션의 등록을 사용 하 여 hello 항목에서 사용 되는 tooread hello 메시지 이며 hello 읽기에 성공 하면 다음 모바일 알림 (hello 샘플 시나리오에서 Windows 기본 알림) 전송 toobe toohello 만들 Azure 알림 허브를 사용 하 여 응용 프로그램입니다.
   
        static void ReceiveMessageAndSendNotification(string connectionString)
        {
            // Initialize hello Notification Hub
            string hubConnectionString = CloudConfigurationManager.GetSetting
                    ("Microsoft.NotificationHub.ConnectionString");
            hub = NotificationHubClient.CreateClientFromConnectionString
                    (hubConnectionString, "enterprisepushservicehub");
   
            SubscriptionClient Client =
                SubscriptionClient.CreateFromConnectionString
                        (connectionString, sampleTopic, sampleSubscription);
   
            Client.Receive();
   
            // Continuously process messages received from hello subscription
            while (true)
            {
                BrokeredMessage message = Client.Receive();
                var toastMessage = @"<toast><visual><binding template=""ToastText01""><text id=""1"">{messagepayload}</text></binding></visual></toast>";
   
                if (message != null)
                {
                    try
                    {
                        Console.WriteLine(message.MessageId);
                        Console.WriteLine(message.SequenceNumber);
                        string messageBody = message.GetBody<string>();
                        Console.WriteLine("Body: " + messageBody + "\n");
   
                        toastMessage = toastMessage.Replace("{messagepayload}", messageBody);
                        SendNotificationAsync(toastMessage);
   
                        // Remove message from subscription
                        message.Complete();
                    }
                    catch (Exception)
                    {
                        // Indicate a problem, unlock message in subscription
                        message.Abandon();
                    }
                }
            }
        }
        static async void SendNotificationAsync(string message)
        {
            await hub.SendWindowsNativeNotificationAsync(message);
        }
   
    e. 게시용으로이 **WebJob**Visual Studio에서 hello 솔루션을 마우스 오른쪽 단추로 클릭 하 고 선택 **WebJob로 게시**
   
    ![][2]
   
    f. 게시 프로필을 선택 하 고 없는 경우 이미이 WebJob 호스팅할 때와 다음 hello 웹 사이트가 있는 새 Azure 웹 사이트를 만들 **게시**합니다.
   
    ![][3]
   
    g. "계속 실행" 작업 toobe hello 구성 toohello에 로그인 할 때 [Azure 클래식 포털] hello 다음과 같은 항목이 표시 됩니다.
   
    ![][4]
3. **EnterprisePushMobileApp**
   
    a. 이것이 hello WebJob 실행 모바일 백 엔드의 일환으로 알림 메시지를 수신 하 고 표시 하는 Windows 스토어 응용 프로그램입니다. [알림 허브-Windows 유니버설 자습서]를 기반으로 합니다.  
   
    b. 응용 프로그램을 사용 하도록 설정된 tooreceive 알림 메시지를 확인 합니다.
   
    c. 알림 허브 등록 코드 다음 해당 hello hello 응용 프로그램 시작에서 호출 되 고 있는지 확인 (hello를 바꾼 후 *HubName* 및 *DefaultListenSharedAccessSignature*:
   
        private async void InitNotificationsAsync()
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            var hub = new NotificationHub("[HubName]", "[DefaultListenSharedAccessSignature]");
            var result = await hub.RegisterNativeAsync(channel.Uri);
   
            // Displays hello registration ID so you know it was successful
            if (result.RegistrationId != null)
            {
                var dialog = new MessageDialog("Registration successful: " + result.RegistrationId);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
            }
        }

### <a name="running-sample"></a>샘플 실행:
1. 확인 WebJob 성공적으로 실행 되 고 예약 너무 "지속적으로 실행" 합니다.
2. Hello 실행 **EnterprisePushMobileApp** 는 hello Windows 스토어 앱이 시작 됩니다.
3. Hello 실행 **EnterprisePushBackendSystem** hello LoB 백 엔드를 시뮬레이트합니다 이며 보내기 시작 하는 콘솔 응용 프로그램 메시지 및 hello 다음과 같이 표시 되는 알림 메시지를 표시 됩니다.
   
    ![][5]
4. hello 메시지를 웹 작업에서 서비스 버스 구독에서 모니터링 된 tooService 버스 주제를 보낸 원래입니다. 메시지가 수신 되 면 알림은 생성 되어 toohello 모바일 앱에 전송 됩니다. WebJob tooconfirm hello toohello 로그 링크를 이동할 때 처리를 기록 하는 hello를 살펴볼 수 있습니다 [Azure 클래식 포털] 웹 작업에 대 한:
   
    ![][6]

<!-- Images -->
[1]: ./media/notification-hubs-enterprise-push-architecture/architecture.png
[2]: ./media/notification-hubs-enterprise-push-architecture/WebJobsContextMenu.png
[3]: ./media/notification-hubs-enterprise-push-architecture/PublishAsWebJob.png
[4]: ./media/notification-hubs-enterprise-push-architecture/WebJob.png
[5]: ./media/notification-hubs-enterprise-push-architecture/Notifications.png
[6]: ./media/notification-hubs-enterprise-push-architecture/WebJobsLog.png

<!-- Links -->
[알림 허브 샘플]: https://github.com/Azure/azure-notificationhubs-samples
[Azure 모바일 서비스]: http://azure.microsoft.com/documentation/services/mobile-services/
[Azure 서비스 버스]: http://azure.microsoft.com/documentation/articles/fundamentals-service-bus-hybrid-solutions/
[서비스 버스 Pub/Sub 프로그래밍]: http://azure.microsoft.com/documentation/articles/service-bus-dotnet-how-to-use-topics-subscriptions/
[Azure WebJob]: http://azure.microsoft.com/documentation/articles/web-sites-create-web-jobs/
[알림 허브-Windows 유니버설 자습서]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started/
[Azure 클래식 포털]: https://manage.windowsazure.com/

---
title: "Visual Studio에서 Azure 코드 aaaOptimizing | Microsoft Docs"
description: "Visual Studio에서 Azure 코드 최적화 도구를 사용하여 더욱 강력하고 성능이 뛰어난 코드를 만드는 방법에 대해 알아보세요."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: ed48ee06-e2d2-4322-af22-07200fb16987
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 7df932def9dc16c93de29fc6a77c8fc121fda338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="optimizing-your-azure-code"></a>Azure 코드 최적화
Microsoft Azure를 사용 하는 앱을 프로그래밍할 때의 앱 확장성, 동작 및 클라우드 환경에서 성능 문제를 방지 하는 일부 코딩 방법을 toohelp 따라야 가지 있습니다. Microsoft는 이와 같이 자주 발생하는 문제를 인식 및 식별하고 해결해 주는 Azure 코드 분석 도구를 제공합니다. NuGet 통해 Visual Studio의 hello 도구를 다운로드할 수 있습니다.

## <a name="azure-code-analysis-rules"></a>Azure 코드 분석 규칙
hello Azure 코드 분석 도구 규칙 tooautomatically 플래그입니다. Azure 코드 성능에 영향을 주는 알려진된 문제를 발견 하면 hello를 사용 합니다. 감지된 문제는 경고 또는 컴파일러 오류로 나타납니다. 코드 수정 또는 제안 사항은 tooresolve hello 경고 또는 오류가 종종 전구 아이콘을 통해 제공 됩니다.

## <a name="avoid-using-default-in-process-session-state-mode"></a>기본(In-Process) 세션 상태 모드 방지
### <a name="id"></a>ID
AP0000

### <a name="description"></a>설명
클라우드 응용 프로그램에 대 한 hello 기본 (in-process) 세션 상태 모드를 사용 하는 경우 세션 상태를 잃을 수 있습니다.

[Azure 코드 분석 의견](http://go.microsoft.com/fwlink/?LinkId=403771)에서 아이디어와 의견을 공유해 주세요.

### <a name="reason"></a>이유
기본적으로 hello 세션 상태 모드 hello web.config 파일에 지정 된 프로세스에는 합니다. 또한 경우 hello 구성 파일에 지정 된 항목이, hello 세션 상태 모드 tooin 프로세스 기본값입니다. hello in-process 모드 hello 웹 서버의 메모리에 세션 상태를 저장합니다. 인스턴스를 다시 시작 또는 새 인스턴스를 부하 분산 또는 장애 조치 지원을 사용 되는 경우에 hello 웹 서버의 메모리에 저장 된 hello 세션 상태가 저장 되지 않습니다. 이러한 상황을 확장할 hello 클라우드 hello 응용 프로그램을 방지 합니다.

ASP.NET 세션 상태는 세션 상태 데이터에 대해 다양한 저장소 옵션(InProc, StateServer, SQLServer, 사용자 지정, 해제)을 지원합니다. 사용 하는 사용자 지정 모드 toohost 데이터에 대해 외부 세션 상태 저장소와 같은 것이 좋습니다. [Redis 용 Azure 세션 상태 공급자](http://go.microsoft.com/fwlink/?LinkId=401521)합니다.

### <a name="solution"></a>해결 방법
하나의 권장된 솔루션은 관리 캐시 서비스에서 toostore 세션 상태입니다. 자세한 내용은 방법 toouse [Redis 용 Azure 세션 상태 공급자](http://go.microsoft.com/fwlink/?LinkId=401521) toostore 세션 상태입니다. 또한 저장소 세션 명시할 수 다른 장소 tooensure에 hello 클라우드에서 응용 프로그램은 확장 가능 합니다. toolearn 읽으십시오 대체 솔루션에 대 한 자세한 [세션 상태 모드](https://msdn.microsoft.com/library/ms178586)합니다.

## <a name="run-method-should-not-be-async"></a>실행 메서드는 비동기가 아니어야 함
### <a name="id"></a>ID
AP1000

### <a name="description"></a>설명
비동기 메서드를 만듭니다 (같은 [await](https://msdn.microsoft.com/library/hh156528.aspx)) hello 외부 [run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) 메서드 및에서 hello 비동기 메서드를 호출 [run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)합니다. Hello 선언 [ [run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) 비동기 메서드로 인해 hello 작업자 역할 tooenter 다시 시작 루프입니다.

[Azure 코드 분석 의견](http://go.microsoft.com/fwlink/?LinkId=403771)에서 아이디어와 의견을 공유해 주세요.

### <a name="reason"></a>이유
Hello 내에서 비동기 메서드 호출 [run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) 메서드를 사용 하면 hello 클라우드 서비스 런타임 toorecycle hello 작업자 역할입니다. 모든 프로그램 실행은 hello 내에서 수행 작업자 역할이 시작 될 때 [run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) 메서드. 기존 hello [run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) 메서드로 인해 hello 작업자 역할 toorestart 합니다. Hello 작업자 역할 런타임이 비동기 메서드에 hello에 도달 hello 비동기 메서드의 한 후 모든 작업을 디스패치 하 고 반환 합니다. 이 인해 hello 작업자 역할 tooexit hello에서 [ [ [ [run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) 메서드 및 다시 시작 합니다. 실행의 다음 반복 hello에서에서 hello 작업자 역할에는 hello 비동기 메서드를 다시 및 장치 재시작을 일으키는 hello 작업자 역할 toorecycle도 다시 적중 횟수입니다.

### <a name="solution"></a>해결 방법
Hello 이외의 모든 비동기 작업을 배치 [run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) 메서드. 그런 다음에서 리팩터링 hello 비동기 메서드를 호출 hello 내 [ [run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) RunAsync ().wait 등의 방법을 합니다. hello Azure 코드 분석 도구입니다.이 문제를 해결할 수 있습니다.

다음 코드 조각 hello hello 코드이 문제 해결을 위해이 보여 줍니다.

```
public override void Run()
{
    RunAsync().Wait();
}

public async Task RunAsync()
{
    //Asynchronous operations code logic
    // This is a sample worker implementation. Replace with your logic.

    Trace.TraceInformation("WorkerRole1 entry point called");

    HttpClient client = new HttpClient();

    Task<string> urlString = client.GetStringAsync("http://msdn.microsoft.com");

    while (true)
    {
        Thread.Sleep(10000);
        Trace.TraceInformation("Working");

        string stream = await urlString;
    }

}
```

## <a name="use-service-bus-shared-access-signature-authentication"></a>서비스 버스 공유 액세스 서명 인증 사용
### <a name="id"></a>ID
AP2000

### <a name="description"></a>설명
인증에 SAS(공유 액세스 서명)를 사용합니다. 서비스 버스 인증에 ACS(액세스 제어 서비스)를 사용 중입니다.

[Azure 코드 분석 의견](http://go.microsoft.com/fwlink/?LinkId=403771)에서 아이디어와 의견을 공유해 주세요.

### <a name="reason"></a>이유
보안 강화를 위해 Azure Active Directory에서 ACS 인증을 SAS 인증으로 대체합니다. 참조 [Azure Active Directory ACS의 향후 hello는](http://blogs.technet.com/b/ad/archive/2013/06/22/azure-active-directory-is-the-future-of-acs.aspx) hello 전환 계획에 대 한 내용은 합니다.

### <a name="solution"></a>해결 방법
앱에 SAS 인증을 사용합니다. 다음 예제는 hello 네임 스페이스 또는 엔터티에 toouse는 기존 SAS 토큰 tooaccess 서비스 버스 하는 방법을 보여 줍니다.

```
MessagingFactory listenMF = MessagingFactory.Create(endpoints, new StaticSASTokenProvider(subscriptionToken));
SubscriptionClient sc = listenMF.CreateSubscriptionClient(topicPath, subscriptionName);
BrokeredMessage receivedMessage = sc.Receive();
```

다음 항목에 대 한 자세한 내용은 hello를 참조 하십시오.

* 개요를 보려면 [서비스 버스를 사용한 공유 액세스 서명 인증](https://msdn.microsoft.com/library/dn170477.aspx)
* [어떻게 toouse 서비스 버스를 통해 공유 액세스 서명 인증](https://msdn.microsoft.com/library/dn205161.aspx)
* 샘플 프로젝트를 보려면 [서비스 버스를 사용한 SAS(공유 액세스 서명) 인증 사용](http://code.msdn.microsoft.com/windowsazure/Using-Shared-Access-e605b37c)

## <a name="consider-using-onmessage-method-tooavoid-receive-loop"></a>"수신 루프" OnMessage 메서드 tooavoid를 사용 하는 것이 좋습니다.
### <a name="id"></a>ID
AP2002

### <a name="description"></a>설명
"수신 루프"으로 옮기기 tooavoid 호출 hello **OnMessage** 메서드는 호출 hello 보다 메시지를 받기 위한 더 나은 솔루션 **수신** 메서드. 그러나 hello를 사용 해야 할 경우 **수신** 메서드를 기본이 아닌 서버 대기 시간을 지정 hello 서버 대기 시간은 1 분 이상 있는지 확인 합니다.

[Azure 코드 분석 의견](http://go.microsoft.com/fwlink/?LinkId=403771)에서 아이디어와 의견을 공유해 주세요.

### <a name="reason"></a>이유
호출할 때 **OnMessage**, hello 클라이언트 hello 큐 또는 구독을 지속적으로 폴링하는 내부 메시지 펌프를 시작 합니다. 이 메시지 펌프 tooreceive 메시지 호출을 실행 하는 무한 루프가 포함 되어 있습니다. Hello 호출 시간이 초과 되 면 새 호출이 발급 됩니다. hello 제한 시간 간격의 hello hello 값에 의해 결정 됩니다 [OperationTimeout](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout.aspx) hello 속성 [MessagingFactory](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactory.aspx)사용 중인 합니다.

사용 시의 이점은 hello **OnMessage** 너무 비교**수신** 가 메시지에 대 한 폴링, 예외 처리, 병렬로 여러 메시지를 처리 및 hello 완료 toomanually을 갖지 못하도록은 메시지입니다.

호출 하는 경우 **수신** 기본값을 사용 하지 않고도 수 있는지 hello *ServerWaitTime* 값은 1 분 보다 길어야 합니다. 설정 *ServerWaitTime* 1 분 보다 toomore hello 메시지가 완전히 수신 되기 전에 초과 hello 서버를 방지 합니다.

### <a name="solution"></a>해결 방법
권장된 사용법에 대 한 코드 예제를 따르는 hello를 참조 하십시오. 자세한 내용은 [QueueClient.OnMessage 메서드(Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.onmessage.aspx) 및 [QueueClient.Receive 메서드(Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.receive.aspx)를 참조하세요.

hello Azure 메시징 인프라의 tooimprove hello 성능 디자인 패턴 hello 참조 [비동기 메시징 입문서](https://msdn.microsoft.com/library/dn589781.aspx)합니다.

hello 다음은 사용 하는 예제 **OnMessage** tooreceive 메시지입니다.

```
void ReceiveMessages()
{
    // Initialize message pump options.
    OnMessageOptions options = new OnMessageOptions();
    options.AutoComplete = true; // Indicates if hello message-pump should call complete on messages after hello callback has completed processing.
    options.MaxConcurrentCalls = 1; // Indicates hello maximum number of concurrent calls toohello callback hello pump should initiate.
    options.ExceptionReceived += LogErrors; // Enables you tooget notified of any errors encountered by hello message pump.

    // Start receiving messages.
    QueueClient client = QueueClient.Create("myQueue");
    client.OnMessage((receivedMessage) => // Initiates hello message pump and callback is invoked for each message that is recieved, calling close on hello client will stop hello pump.
    {
        // Process hello message.
    }, options);
    Console.WriteLine("Press any key tooexit.");
    Console.ReadKey();
```

hello 다음은 사용 하는 예제 **수신** hello 기본 서버와 대기 시간입니다.

```
string connectionString =  
CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");

QueueClient Client =  
    QueueClient.CreateFromConnectionString(connectionString, "TestQueue");

while (true)  
{   
   BrokeredMessage message = Client.Receive();
   if (message != null)
   {
      try  
      {
         Console.WriteLine("Body: " + message.GetBody<string>());
         Console.WriteLine("MessageID: " + message.MessageId);
         Console.WriteLine("Test Property: " +  
            message.Properties["TestProperty"]);

         // Remove message from queue
         message.Complete();
      }

      catch (Exception)
      {
         // Indicate a problem, unlock message in queue
         message.Abandon();
      }
   }
```

hello 다음은 사용 하는 예제 **수신** 기본이 아닌 서버 대기 시간입니다.

```
while (true)  
{   
   BrokeredMessage message = Client.Receive(new TimeSpan(0,1,0));

   if (message != null)
   {
      try  
      {
         Console.WriteLine("Body: " + message.GetBody<string>());
         Console.WriteLine("MessageID: " + message.MessageId);
         Console.WriteLine("Test Property: " +  
            message.Properties["TestProperty"]);

         // Remove message from queue
         message.Complete();
      }

      catch (Exception)
      {
         // Indicate a problem, unlock message in queue
         message.Abandon();
      }
   }
}
```
## <a name="consider-using-asynchronous-service-bus-methods"></a>비동기 서비스 버스 메서드 사용 고려
### <a name="id"></a>ID
AP2003

### <a name="description"></a>설명
비동기 서비스 버스 메서드 tooimprove 성능 조정 된 메시징을 사용 합니다.

[Azure 코드 분석 의견](http://go.microsoft.com/fwlink/?LinkId=403771)에서 아이디어와 의견을 공유해 주세요.

### <a name="reason"></a>이유
비동기 메서드를 사용 하 여 hello 주 스레드를 차단 하지 않는 각 호출을 실행 하기 때문에 응용 프로그램 동시성이 보장을 수 있습니다. 서비스 버스 메시징 메서드를 사용할 때 작업(보내기, 받기, 삭제 등)을 수행하면 다소 시간이 소요됩니다. 이 시간 hello 요청과 hello 회신의 추가 toohello 대기 시간에 서비스 버스 서비스 hello 하 여 hello hello 작업 처리를 포함합니다. 시간당 작업 tooincrease hello 번호 작업이 동시에 실행 해야 합니다. 자세한 내용은 참조 하십시오 너무[성능 향상을 사용 하 여 서비스 버스 조정 된 메시징에 대 한 유용한](https://msdn.microsoft.com/library/azure/hh528527.aspx)합니다.

### <a name="solution"></a>해결 방법
참조 [QueueClient 클래스 (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.aspx) toouse hello 비동기 메서드를 권장 하는 방법에 대 한 정보에 대 한 합니다.

hello Azure 메시징 인프라의 tooimprove hello 성능 디자인 패턴 hello 참조 [비동기 메시징 입문서](https://msdn.microsoft.com/library/dn589781.aspx)합니다.

## <a name="consider-partitioning-service-bus-queues-and-topics"></a>서비스 버스 큐 및 토픽 분할 고려
### <a name="id"></a>ID
AP2004

### <a name="description"></a>설명
서비스 버스 메시징에서 성능을 향상하려면 서비스 버스 큐와 토픽을 분할합니다.

[Azure 코드 분석 의견](http://go.microsoft.com/fwlink/?LinkId=403771)에서 아이디어와 의견을 공유해 주세요.

### <a name="reason"></a>이유
서비스 버스 큐 및 항목 분할 제한 되기 때문에 hello 분할 된 큐 또는 항목의 전체 처리량은 더 이상 단일 메시지 브로커 또는 메시징 저장소의 hello 성능으로 성능 처리량 및 서비스 가용성이 증가 합니다. 또한 메시징 스토어가 일시적으로 중단된 경우에도 분할된 큐 또는 토픽을 계속 사용할 수 있습니다. 자세한 내용은 [메시징 엔터티 분할](https://msdn.microsoft.com/library/azure/dn520246.aspx)을 참조하세요.

### <a name="solution"></a>해결 방법
어떻게 코드 조각에 나와 있는 다음 hello toopartition 메시징 엔터티입니다.

```
// Create partitioned topic.
NamespaceManager ns = NamespaceManager.CreateFromConnectionString(myConnectionString);
TopicDescription td = new TopicDescription(TopicName);
td.EnablePartitioning = true;
ns.CreateTopic(td);
```

자세한 내용은 참조 [분할 서비스 버스 큐 및 항목 | Microsoft Azure 블로그](https://azure.microsoft.com/blog/2013/10/29/partitioned-service-bus-queues-and-topics/) 하 고 체크 아웃 hello [Microsoft Azure 서비스 버스 분할 된 큐](https://code.msdn.microsoft.com/windowsazure/Service-Bus-Partitioned-7dfd3f1f) 샘플.

## <a name="do-not-set-sharedaccessstarttime"></a>SharedAccessStartTime을 설정하지 마십시오.
### <a name="id"></a>ID
AP3001

### <a name="description"></a>설명
SharedAccessStartTimeset toohello tooimmediately hello 공유 액세스 정책을 시작 하는 현재 시간을 사용 하지 않아야 합니다. 필요할 때만 tooset이이 속성 toostart hello 공유 액세스 정책을 나중에 하려는 경우.

[Azure 코드 분석 의견](http://go.microsoft.com/fwlink/?LinkId=403771)에서 아이디어와 의견을 공유해 주세요.

### <a name="reason"></a>이유
클록 동기화는 데이터 센터 간 약간의 시간 차이를 발생시킵니다. 예를 들어 논리적으로 겠 설정을 hello 시작 시간의 저장소 SAS 정책의 hello DateTime.Now 또는 비슷한 메서드를 사용 하 여 현재 시간 하면 hello SAS 정책 tootake 효과 즉시으로 합니다. 그러나 데이터 센터 간에 시간이 약간씩 차이점 hello 일부 데이터 센터 시간이 조금 늦은 hello 시작 시간 보다 이후 될 수에 문제가 발생할 수 있습니다. 신속 하 게 (또는 심지어 즉시) hello 정책 SAS 만료 될 수 있습니다 결과적으로, hello 정책 수명을 너무 짧게 설정 됩니다.

Azure 저장소에서 공유 액세스 서명을 사용 하 여에 대 한 자세한 지침을 참조 하십시오. [소개 테이블 SAS (공유 액세스 서명), 큐 SAS 및 업데이트 tooBlob SAS-Microsoft Azure 저장소 팀 블로그-사이트 홈-MSDN 블로그](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx)합니다.

### <a name="solution"></a>해결 방법
Hello 공유 액세스 정책의 hello 시작 시간을 설정 하는 hello 문을 제거 합니다. hello Azure 코드 분석 도구는이 문제에 대 한 수정 프로그램을 제공합니다. 보안 관리에 대 한 자세한 내용은 디자인 패턴 hello를 참조 하십시오 [Valet 키 패턴](https://msdn.microsoft.com/library/dn568102.aspx)합니다.

다음 코드 조각 hello이이 문제에 대 한 hello 코드 수정을 보여 줍니다.

```
// hello shared access policy provides  
// read/write access toohello container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // tooensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
   SharedAccessExpiryTime = DateTime.UtcNow.AddHours(10),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

## <a name="shared-access-policy-expiry-time-must-be-more-than-five-minutes"></a>공유 액세스 정책 만료 시간은 5분을 초과해야 합니다.
### <a name="id"></a>ID
AP3002

### <a name="description"></a>설명
시계 "클록 스큐입니다." 이라는 tooa 조건 인해 서로 다른 위치에 있는 데이터 센터 간에 최대 5 분의 시간 차이 만큼 수 있습니다. tooprevent hello SAS 정책 토큰이 만료 되는 작업이 계획 hello 만료 시간 toobe 5 분 이상 설정 합니다.

[Azure 코드 분석 의견](http://go.microsoft.com/fwlink/?LinkId=403771)에서 아이디어와 의견을 공유해 주세요.

### <a name="reason"></a>이유
Hello 전 세계 서로 다른 위치에 있는 데이터 센터는 클록 신호 여 동기화합니다. 클록 신호 tootravel toodifferent 위치에 대 한 시간을 사용 하기 때문에 있을 수 있습니다 서로 다른 지리적 위치에 있는 데이터 센터 간에 시간 차이가 모든 항목이 동기화 된다고 있지만. 이 시간 차이 hello는 공유 액세스 정책 시작 시간 및 만료 간격에 영향을 줄 수 있습니다. 따라서 tooensure 공유 액세스 정책을 즉시 적용, hello 시작 시간은 지정 하지 않습니다. 또한 hello 만료 시간에는 5 분 tooprevent 초기 제한 시간 보다 더 있는지 확인 합니다.

Azure 저장소에서 공유 액세스 서명을 사용 하는 방법에 대 한 자세한 내용은 참조 [소개 테이블 SAS (공유 액세스 서명), 큐 SAS 및 업데이트 tooBlob SAS-Microsoft Azure 저장소 팀 블로그-사이트 홈-MSDN 블로그](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx)합니다.

### <a name="solution"></a>해결 방법
보안 관리에 대 한 자세한 내용은 hello 디자인 패턴을 참조 하십시오. [Valet 키 패턴](https://msdn.microsoft.com/library/dn568102.aspx)합니다.

hello 다음은 공유 액세스 정책 시작 시간을 지정 하지 않는 예입니다.

```
// hello shared access policy provides  
// read/write access toohello container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // tooensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
   SharedAccessExpiryTime = DateTime.UtcNow.AddHours(10),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

hello 다음은 정책 만료 기간이 5 분 보다 큰 공유 액세스 정책 시작 시간을 지정 하는 예로입니다.

```
// hello shared access policy provides  
// read/write access toohello container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // tooensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
  SharedAccessStartTime = new DateTime(2014,1,20),   
 SharedAccessExpiryTime = new DateTime(2014, 1, 21),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

자세한 내용은 [공유 액세스 서명 만들기 및 사용](https://msdn.microsoft.com/library/azure/jj721951.aspx)을 참조하세요.

## <a name="use-cloudconfigurationmanager"></a>CloudConfigurationManager 사용
### <a name="id"></a>ID
AP4000

### <a name="description"></a>설명
Hello를 사용 하 여 [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) Azure 웹 사이트와 Azure 모바일 서비스에 런타임 문제가 발생 하지 않습니다와 같은 프로젝트에 대 한 클래스입니다. 그러나 모범 사례로, 것이 좋습니다 toouse 클라우드[ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) 모든 Azure 클라우드 응용 프로그램에 대 한 구성을 관리 하는 단일화 된 방법을으로 합니다.

[Azure 코드 분석 의견](http://go.microsoft.com/fwlink/?LinkId=403771)에서 아이디어와 의견을 공유해 주세요.

### <a name="reason"></a>이유
CloudConfigurationManager는 hello 구성 파일의 적절 한 toohello 응용 프로그램 환경을 읽습니다.

[CloudConfigurationManager](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx)

### <a name="solution"></a>해결 방법
리팩터링 코드 toouse hello [CloudConfigurationManager 클래스](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx)합니다. 이 문제에 대 한 코드 수정 hello Azure 코드 분석 도구에서 제공 됩니다.

다음 코드 조각 hello이이 문제에 대 한 hello 코드 수정을 보여 줍니다. Replace

`var settings = ConfigurationManager.AppSettings["mySettings"];`

다음으로 바꿀 수 있습니다.

`var settings = CloudConfigurationManager.GetSetting("mySettings");`

어떻게 toostore hello App.config 또는 Web.config 파일에서 구성 설정의 예를 들면 다음과 같습니다. Hello 구성 파일의 hello 설정 toohello appSettings 섹션을 추가 합니다. hello 다음은 이전 코드 예제의 hello에 대 한 hello Web.config 파일입니다.

```
<appSettings>
    <add key="webpages:Version" value="3.0.0.0" />
    <add key="webpages:Enabled" value="false" />
    <add key="ClientValidationEnabled" value="true" />
    <add key="UnobtrusiveJavaScriptEnabled" value="true" />
    <add key="mySettings" value="[put_your_setting_here]"/>
  </appSettings>  
```

## <a name="avoid-using-hard-coded-connection-strings"></a>하드 코드된 연결 문자열을 사용하지 마십시오.
### <a name="id"></a>ID
AP4001

### <a name="description"></a>설명
하드 코드 된 연결 문자열을 사용 하 고 필요한 tooupdate toomake 변경 tooyour 소스 코드가 있는 hello 응용 프로그램을 다시 컴파일해야 하는 나중에 해당 합니다. 그러나 구성 파일에서 연결 문자열을 저장 하는 경우 변경할 수 있습니다에 나중에 간단히 hello 구성 파일을 업데이트 하 여 합니다.

[Azure 코드 분석 의견](http://go.microsoft.com/fwlink/?LinkId=403771)에서 아이디어와 의견을 공유해 주세요.

### <a name="reason"></a>이유
하드 코딩 연결 문자열은 연결 문자열 toobe 신속 하 게 변경 해야 하는 경우 문제를 유발 하기 때문에 좋지 합니다. 또한 hello 프로젝트 체크 인 toosource 컨트롤 toobe를 필요한 경우 하드 코드 된 연결 문자열 있으므로 보안이 취약해를 집니다 hello 문자열 hello 소스 코드에서 볼 수 있습니다.

### <a name="solution"></a>해결 방법
Hello 구성 파일 또는 Azure 환경에 연결 문자열을 저장 합니다.

* 독립 실행형 응용 프로그램에 대 한 app.config toostore 연결 문자열 설정을 사용 합니다.
* IIS에서 호스트 웹 응용 프로그램에 대 한 web.config toostore 연결 문자열을 사용 합니다.
* ASP.NET vNext 응용 프로그램의 경우 configuration.json toostore 연결 문자열을 사용 합니다.

web.config 또는 app.config와 같은 구성 파일을 사용하는 방법은 [ASP.NET 웹 구성 지침](https://msdn.microsoft.com/library/vstudio/ff400235\(v=vs.100\).aspx)을 참조하세요. Azure 환경 변수의 작동 방식에 대해서는 [Azure 웹 사이트: 응용 프로그램 문자열 및 연결 문자열 작동 방식](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/)을 참조하세요. 연결 문자열을 소스 제어에 저장하는 방법에 대한 자세한 내용은 [연결 문자열과 같은 민감한 정보를 소스 코드 리포지토리에 저장된 파일에 두지 않는 방식](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control)을 참조하세요.

## <a name="use-diagnostics-configuration-file"></a>진단 구성 파일 사용
### <a name="id"></a>ID
AP5000

### <a name="description"></a>설명
Hello Microsoft.WindowsAzure.Diagnostics 프로그래밍 API를 사용 하 여과 같은 코드에서 진단 설정을 구성 하는 대신, hello diagnostics.wadcfg 파일의 진단 설정을 구성 해야 합니다. Azure SDK 2.5를 사용하는 경우에는 diagnostics.wadcfgx를 사용합니다. 이 통해 코드 toorecompile 필요 없이 진단 설정을 변경할 수 있습니다.

[Azure 코드 분석 의견](http://go.microsoft.com/fwlink/?LinkId=403771)에서 아이디어와 의견을 공유해 주세요.

### <a name="reason"></a>이유
먼저 여러 가지 방법을 사용 하 여 WAD (Azure 진단), Azure SDK 2.5 (사용 하 여 Azure 진단 1.3)를 구성할 수 없습니다: 추가 toohello 구성 blob 저장소의 명령적 코드, 선언 구성 또는 hello default를 사용 하 여 구성입니다. 그러나 hello 방식으로 tooconfigure diagnostics toouse hello 응용 프로그램 프로젝트에서 XML 구성 파일 (diagnostics.wadcfg 또는 SDK 2.5 이상 버전 이상의 경우)에 기본 설정입니다. 이 방법에서는 hello diagnostics.wadcfg 파일 완전히 hello 구성을 정의 및 업데이트 되어를 다시 배포 합니다. Hello를 사용 하 여 구성을 설정 하는 프로그래밍 방법도 hello와 hello diagnostics.wadcfg 구성 파일의 hello 사용을 혼합 [DiagnosticMonitor](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.diagnosticmonitor.aspx)또는 [RoleInstanceDiagnosticManager](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.management.roleinstancediagnosticmanager.aspx) 클래스는 tooconfusion을 발생할 수 있습니다. 자세한 내용은 [Azure 진단 구성 초기화 또는 변경](https://msdn.microsoft.com/library/azure/hh411537.aspx) 을 참조하세요.

(Azure SDK 2.5에 포함) WAD 1.3 부터는 것은 더 이상 가능한 toouse 코드 tooconfigure 진단 합니다. 결과적으로, hello 구성 적용 하거나 hello 진단 확장을 업데이트할 때 제공할 수 있습니다.

### <a name="solution"></a>해결 방법
Hello 진단 구성 디자이너 toomove 진단 설정을 toohello 진단 구성 파일 (diagnositcs.wadcfg 또는 SDK 2.5 이상 버전 이상의 경우)를 사용 합니다. 설치 하는 것이 좋습니다 [Azure SDK 2.5](http://go.microsoft.com/fwlink/?LinkId=513188) hello 최신 진단 기능을 사용 합니다.

1. Hello tooconfigure hello 역할에 대 한 바로 가기 메뉴에서 속성을 선택 하 고 hello 구성 탭을 선택 합니다.
2. Hello에 **진단** 섹션에, 해당 hello 반드시 **진단 사용** 확인란을 선택 합니다.
3. Hello 선택 **구성** 단추입니다.

   ![Hello 진단 사용 옵션 액세스](./media/vs-azure-tools-optimizing-azure-code-in-visual-studio/IC796660.png)

   자세한 내용은 [Azure 클라우드 서비스 및 가상 컴퓨터에서 진단 구성](vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) 을 참조하세요.

## <a name="avoid-declaring-dbcontext-objects-as-static"></a>DbContext 개체를 정적으로 선언하지 마십시오
### <a name="id"></a>ID
AP6000

### <a name="description"></a>설명
toosave 메모리 DBContext 개체를 정적으로 선언 하지 마십시오.

[Azure 코드 분석 의견](http://go.microsoft.com/fwlink/?LinkId=403771)에서 아이디어와 의견을 공유해 주세요.

### <a name="reason"></a>이유
DBContext 개체 hello 각 호출에서 쿼리 결과 저장 합니다. DBContext 개체를 정적 hello 응용 프로그램 도메인이 언로드될 때까지 삭제 됩니다. 따라서 정적 DBContext 개체는 많은 양의 메모리를 사용할 수 있습니다.

### <a name="solution"></a>해결 방법
DBContext를 지역 변수 또는 비정적 인스턴스 필드로 선언하고 작업에 사용한 다음 사용 후 삭제되도록 합니다.

다음 예제에서는 MVC 컨트롤러 클래스 hello toouse DBContext 개체 hello 하는 방법을 보여 줍니다.

```
public class BlogsController : Controller
    {
        //BloggingContext is a subclass tooDbContext        
        private BloggingContext db = new BloggingContext();
        // GET: Blogs
        public ActionResult Index()
        {
            //business logics…
            return View();
        }
        protected override void Dispose(bool disposing)
        {
            if (disposing)
            {
                db.Dispose();
            }
            base.Dispose(disposing);
        }
    }
```

## <a name="next-steps"></a>다음 단계
Azure 응용 프로그램 문제 해결 및 최적화에 대해 자세히 toolearn 참조 [Visual Studio를 사용 하 여 Azure 앱 서비스의 웹 앱의 문제를 해결](app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md)합니다.

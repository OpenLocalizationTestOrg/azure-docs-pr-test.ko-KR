---
title: "Azure 이벤트 허브를 사용 하 여에서 aaaReceive 이벤트는.NET Framework hello | Microsoft Docs"
description: ".NET Framework hello를 사용 하 여 Azure 이벤트 허브에서이 자습서 tooreceive 이벤트를 따릅니다."
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: c4974bd3-2a79-48a1-aa3b-8ee2d6655b28
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/12/2017
ms.author: sethm
ms.openlocfilehash: a88c3feeacfd3de9622dbb86e25222e861750204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="receive-events-from-azure-event-hubs-using-hello-net-framework"></a>.NET Framework hello를 사용 하 여 Azure 이벤트 허브에서 이벤트를 수신 합니다.

## <a name="introduction"></a>소개

이벤트 허브는 연결된 장치 및 응용 프로그램에서 많은 양의 이벤트 데이터(원격 분석)를 처리하는 서비스입니다. 이벤트 허브로 데이터를 수집한 후 저장소 클러스터를 사용 하 여 hello 데이터를 저장할 수도 있고 실시간 분석 공급자를 사용 하 여 변환할 수 있습니다. 이 대규모 이벤트 수집 및 처리 기능은 hello 인터넷 IoT (사물)를 포함 하 여 최신 응용 프로그램 아키텍처의 핵심 구성 요소입니다.

이 자습서에서는 어떻게 toowrite.NET Framework 콘솔 hello를 사용 하 여 이벤트 허브에서 메시지를 수신 하는 응용 프로그램  **[이벤트 프로세서 호스트][EventProcessorHost]**합니다. hello.NET Framework를 사용 하 여 toosend 이벤트 참조 hello [tooAzure 이벤트 허브.NET Framework hello를 사용 하 여 이벤트를 보내는](event-hubs-dotnet-framework-getstarted-send.md) , 문서 또는 hello hello 내용의 왼쪽 테이블에서 적절 한 보내는 언어를 선택 합니다.

hello [이벤트 프로세서 호스트] [ EventProcessorHost] 영구 검사점을 관리 하 여 이벤트 허브에서 수신 이벤트를 간소화 하는.NET 클래스 이며 해당 이벤트 허브에서 병렬 받습니다. Hello를 사용 하 여 [이벤트 프로세서 호스트][Event Processor Host], 서로 다른 노드에에서 호스팅되는 경우에 여러 수신기에서 이벤트를 분할할 수 있습니다. 이 예에서는 어떻게 toouse hello [이벤트 프로세서 호스트] [ EventProcessorHost] 단일 수신자에 대 한 합니다. hello [이벤트 처리 확장] [ Scale out Event Processing with Event Hubs] 방법을 보여 줍니다 샘플 toouse hello [이벤트 프로세서 호스트] [ EventProcessorHost] 여러 수신기와 함께 합니다.

## <a name="prerequisites"></a>필수 조건

toocomplete이이 자습서에서는 다음 필수 구성 요소는 hello 필요:

* [Microsoft Visual Studio 2015 이상](http://visualstudio.com). 이 자습서에서는 hello 스크린 샷 Visual Studio 2017을 사용합니다.
* 활성 Azure 계정. 계정이 없는 경우 몇 분 만에 무료 계정을 만들 수 있습니다. 자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/free/)을 참조하세요.

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a>Event Hubs 네임스페이스 및 이벤트 허브 만들기

hello 첫 번째 단계는 toouse hello [Azure 포털](https://portal.azure.com) toocreate의 네임 스페이스는 이벤트 허브를 입력 하 고 hello toocommunicate hello 이벤트 허브 응용 프로그램에서 필요로 하는 관리 자격 증명을 가져옵니다. toocreate 네임 스페이스 및 이벤트 허브 hello 절차에 따라 [이 여기서](event-hubs-create.md), 다음 hello이이 자습서에서는 다음 단계를 진행 합니다.

## <a name="create-an-azure-storage-account"></a>Azure 저장소 계정 만들기

toouse hello [이벤트 프로세서 호스트][EventProcessorHost], 있어야는 [Azure 저장소 계정][Azure Storage account]:

1. Toohello 로그온 [Azure 포털][Azure portal], 클릭 하 고 **새로** hello에 왼쪽 상단 hello 화면에 있습니다.
2. **저장소**를 클릭한 다음 **저장소 계정**을 클릭합니다.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage1.png)
3. Hello에 **저장소 계정 만들기** 블레이드에서 hello 저장소 계정에 대 한 이름 입력 합니다. Toocreate hello 리소스에는 Azure 구독, 리소스 그룹 및 위치를 선택 합니다. 그런 다음 **Create**를 클릭합니다.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage2.png)
4. Hello 저장소 계정 목록에서 새로 만든 저장소 계정 hello를 클릭 합니다.
5. 저장소 계정 블레이드에서 hello 클릭 **액세스 키**합니다. hello 값을 복사 **key1** 이 자습서의 뒷부분에 나오는 toouse 합니다.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage3.png)

## <a name="create-a-receiver-console-application"></a>수신기 콘솔 응용 프로그램을 만듭니다.

1. Visual Studio에서 hello를 사용 하 여 새 Visual C# 데스크톱 앱 프로젝트를 만듭니다 **콘솔 응용 프로그램** 서식 파일 프로젝트. 이름 hello 프로젝트 **수신기**합니다.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-receiver-csharp1.png)
2. 솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 hello **수신기** 프로젝트를 마우스 클릭 **솔루션에 대 한 NuGet 패키지 관리**합니다.
3. Hello 클릭 **찾아보기** tab, 이후 검색할 `Microsoft Azure Service Bus Event Hub - EventProcessorHost`합니다. 클릭 **설치**, hello 사용 약관을 수락 합니다.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-eph-csharp1.png)
   
    Visual Studio 다운로드, 설치 및 추가 참조 toohello [Azure 서비스 버스 이벤트 허브 EventProcessorHost NuGet 패키지](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost), 모든 종속성과 함께 합니다.
4. 마우스 오른쪽 단추로 클릭 hello **수신기** 프로젝트를 클릭 하 여 **추가**, 클릭 하 고 **클래스**합니다. Hello 새 클래스 이름을 **SimpleEventProcessor**, 클릭 하 고 **추가** toocreate hello 클래스입니다.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-receiver-csharp2.png)
5. 다음 조건 hello SimpleEventProcessor.cs 파일 hello 상단의 hello를 추가 합니다.
    
  ```csharp
  using Microsoft.ServiceBus.Messaging;
  using System.Diagnostics;
  ```
    
  그런 다음 대체할 hello 클래스의 hello 본문에 대 한 코드 다음 hello:
    
  ```csharp
  class SimpleEventProcessor : IEventProcessor
  {
    Stopwatch checkpointStopWatch;
    
    async Task IEventProcessor.CloseAsync(PartitionContext context, CloseReason reason)
    {
        Console.WriteLine("Processor Shutting Down. Partition '{0}', Reason: '{1}'.", context.Lease.PartitionId, reason);
        if (reason == CloseReason.Shutdown)
        {
            await context.CheckpointAsync();
        }
    }
    
    Task IEventProcessor.OpenAsync(PartitionContext context)
    {
        Console.WriteLine("SimpleEventProcessor initialized.  Partition: '{0}', Offset: '{1}'", context.Lease.PartitionId, context.Lease.Offset);
        this.checkpointStopWatch = new Stopwatch();
        this.checkpointStopWatch.Start();
        return Task.FromResult<object>(null);
    }
    
    async Task IEventProcessor.ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
    {
        foreach (EventData eventData in messages)
        {
            string data = Encoding.UTF8.GetString(eventData.GetBytes());
    
            Console.WriteLine(string.Format("Message received.  Partition: '{0}', Data: '{1}'",
                context.Lease.PartitionId, data));
        }
    
        //Call checkpoint every 5 minutes, so that worker can resume processing from 5 minutes back if it restarts.
        if (this.checkpointStopWatch.Elapsed > TimeSpan.FromMinutes(5))
        {
            await context.CheckpointAsync();
            this.checkpointStopWatch.Restart();
        }
    }
  }
  ```
    
  이 클래스는 hello 호출한 **EventProcessorHost** hello 이벤트 허브에서 받은 tooprocess 이벤트입니다. hello `SimpleEventProcessor` 클래스 스톱 워치 tooperiodically 호출 hello 검사점 메서드를 사용 하 여 hello에 **EventProcessorHost** 컨텍스트. 이러한 처리, hello 수신기를 다시 시작할 경우 최대 5 분 이내 처리 작업을 손실 되도록 합니다.
6. Hello에 **프로그램** 클래스, hello 다음 추가 `using` hello 파일의 맨 위에 hello에 문:
    
  ```csharp
  using Microsoft.ServiceBus.Messaging;
  ```
    
  Hello 바꿉니다 `Main` hello에 대 한 메서드 `Program` 코드 다음 hello로 클래스, 이전에 저장 하는 문자열 및 저장소 계정 및 hello에서 복사한 키 hello hello 이벤트 허브 이름 및 네임 스페이스 수준 연결 hello 대체 합니다. 이전 섹션입니다. 
    
  ```csharp
  static void Main(string[] args)
  {
    string eventHubConnectionString = "{Event Hubs namespace connection string}";
    string eventHubName = "{Event Hub name}";
    string storageAccountName = "{storage account name}";
    string storageAccountKey = "{storage account key}";
    string storageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", storageAccountName, storageAccountKey);
    
    string eventProcessorHostName = Guid.NewGuid().ToString();
    EventProcessorHost eventProcessorHost = new EventProcessorHost(eventProcessorHostName, eventHubName, EventHubConsumerGroup.DefaultGroupName, eventHubConnectionString, storageConnectionString);
    Console.WriteLine("Registering EventProcessor...");
    var options = new EventProcessorOptions();
    options.ExceptionReceived += (sender, e) => { Console.WriteLine(e.Exception); };
    eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>(options).Wait();
    
    Console.WriteLine("Receiving. Press enter key toostop worker.");
    Console.ReadLine();
    eventProcessorHost.UnregisterEventProcessorAsync().Wait();
  }
  ```

7. Hello 프로그램을 실행 하 고 오류가 없는지 확인 하십시오.
  
축하합니다. 이제 이벤트 프로세서 호스트 hello를 사용 하 여 이벤트 허브에서 메시지를 받았습니다.


> [!NOTE]
> 이 자습서에서는 [EventProcessorHost][EventProcessorHost]의 단일 인스턴스를 사용합니다. tooincrease 처리량 것이 좋습니다의 여러 인스턴스를 실행 하는 [EventProcessorHost][EventProcessorHost]hello [이벤트 처리 아웃 배율]에 나타난 것 처럼 [이벤트 처리 아웃 배율] 샘플. 이 경우 hello 다양 한 인스턴스 자동으로 이벤트를 조정 서로 tooload 균형 hello를 받았습니다. 여러 개의 수신기 tooeach 프로세스를 원하는 경우 *모든* 이벤트 hello hello를 사용 해야 **ConsumerGroup** 개념입니다. 서로 다른 컴퓨터에서 이벤트를 받을 때는 것에 대 한 유용한 toospecify 이름을 [EventProcessorHost] [ EventProcessorHost] 인스턴스 기반 hello 컴퓨터 (또는 역할)에 배포 됩니다. 이러한 항목에 대 한 자세한 내용은 참조 hello [이벤트 허브 개요] [ Event Hubs overview] 및 hello [이벤트 허브 프로그래밍 가이드] [ Event Hubs Programming Guide] 항목입니다.
> 
> 

## <a name="next-steps"></a>다음 단계

이벤트 허브를 만들고 보냅니다 및 데이터를 수신 하는 작업 중인 응용 프로그램을 만든 했으므로 hello 다음 링크를 방문 하 여 자세히 알아볼 수 있습니다.

* [이벤트 프로세서 호스트][Event Processor Host]
* [Event Hubs 개요][Event Hubs overview]
* [Event Hubs FAQ](event-hubs-faq.md)

<!-- Images. -->
[19]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj1.png
[20]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj2.png
[21]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs1.png
[22]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs2.png

<!-- Links -->
[EventProcessorHost]: https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[Scale out Event Processing with Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3
[Event Hubs Programming Guide]: event-hubs-programming-guide.md
[Azure Storage account]:../storage/common/storage-create-storage-account.md
[Event Processor Host]: /dotnet/api/microsoft.servicebus.messaging.eventprocessorhost
[Azure portal]: https://portal.azure.com

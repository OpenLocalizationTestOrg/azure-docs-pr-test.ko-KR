---
title: "Java를 사용 하 여 Azure 이벤트 허브에서 aaaReceive 이벤트 | Microsoft Docs"
description: "Java를 사용하여 Event Hubs에서 수신 시작"
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 38e3be53-251c-488f-a856-9a500f41b6ca
ms.service: event-hubs
ms.workload: core
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: 05414a22e6616296752c678bb0af887d6f070c12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="receive-events-from-azure-event-hubs-using-java"></a>Java를 사용하여 Azure Event Hubs에서 이벤트 수신


## <a name="introduction"></a>소개
이벤트 허브는 수백만 개의 초당 응용 프로그램 tooprocess 활성화 이벤트를 수집 하 고 연결 된 장치 및 응용 프로그램에서 생성 되는 데이터의 양이 hello를 분석할 수 있는 확장성이 높은 수집 시스템. 이벤트 허브로 수집된 데이터는 실시간 분석 공급자나 저장소 클러스터를 사용하여 변환하고 저장할 수 있습니다.

자세한 내용은 참조 hello [이벤트 허브 개요][Event Hubs overview]합니다.

이 자습서에서는 어떻게 Java로 작성 된 콘솔 응용 프로그램을 사용 하 여 이벤트 허브로 tooreceive 이벤트입니다.

## <a name="prerequisites"></a>필수 조건

Toocomplete 순서에서에서이 자습서에서는 필요한 다음 필수 구성 요소는 hello:

* Java 개발 환경. 이 자습서에서는 [Eclipse](https://www.eclipse.org/)를 사용한다고 가정합니다.
* 활성 Azure 계정. <br/>계정이 없는 경우 몇 분 만에 무료 계정을 만들 수 있습니다. 자세한 내용은 <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Azure 무료 체험</a>을 참조하세요.

## <a name="receive-messages-with-eventprocessorhost-in-java"></a>Java에서 EventProcessorHost를 사용하여 메시지 수신

**EventProcessorHost**는 영구적 검사점을 관리하여 Event Hubs의 이벤트 수신을 간소화하고 이러한 Event Hubs에서 병렬 수신하는 Java 클래스입니다. EventProcessorHost를 사용하면 다른 노드에 호스트된 경우라도 여러 수신기 간에 이벤트를 분할할 수 있습니다. 이 예에서는 어떻게 toouse EventProcessorHost 단일 수신자에 대 한 합니다.

### <a name="create-a-storage-account"></a>저장소 계정 만들기
EventProcessorHost toouse 있어야는 [Azure 저장소 계정][Azure Storage account]:

1. Toohello 로그온 [Azure 포털][Azure portal]를 클릭 하 고 **+ 새로 만들기** hello hello 화면 왼쪽에 있습니다.
2. **저장소**를 클릭한 다음 **저장소 계정**을 클릭합니다. Hello에 **저장소 계정 만들기** 블레이드에서 hello 저장소 계정에 대 한 이름 입력 합니다. 완료 hello 나머지 hello 필드에서 원하는 지역을 선택한 다음 클릭 **만들기**합니다.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage2.png)

3. Hello 새로 만든 저장소 계정을 클릭 한 다음 클릭 **액세스 키 관리**:
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage3.png)

    Hello 기본 액세스 키 tooa 임시 위치,이 자습서의 뒷부분에 나오는 toouse를 복사 합니다.

### <a name="create-a-java-project-using-hello-eventprocessor-host"></a>Hello EventProcessor 호스트를 사용 하 여 Java 프로젝트 만들기
hello 이벤트 허브에 대 한 Java 클라이언트 라이브러리는 hello에서 Maven 프로젝트에서 사용할 수 있는 [Maven 중앙 리포지토리에][Maven Package], 내부 종속성 선언 뒤 hello를 사용 하 여 참조할 수 있습니다 프로그램 Maven 프로젝트 파일:    

```xml
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs</artifactId>
    <version>{VERSION}</version>
</dependency>
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs-eph</artifactId>
    <version>{VERSION}</version>
</dependency>
<dependency>
  <groupId>com.microsoft.azure</groupId>
  <artifactId>azure-eventhubs-eph</artifactId>
  <version>0.14.0</version>
</dependency>
```

빌드 환경, 다양 한 유형의 얻을 수 있습니다 명시적으로 릴리스된 최신 hello JAR 파일에서 hello [Maven 중앙 리포지토리에] [ Maven Package] 또는 [릴리스 배포 지점에 hello GitHub](https://github.com/Azure/azure-event-hubs/releases)합니다.  

1. 다음 예제는 hello에 대 한 먼저 즐겨 찾는 Java 개발 환경에서 콘솔/셸 응용 프로그램에 대 한 새 Maven 프로젝트를 만듭니다. hello 라고 `ErrorNotificationHandler`합니다.     
   
    ```java
    import java.util.function.Consumer;
    import com.microsoft.azure.eventprocessorhost.ExceptionReceivedEventArgs;
   
    public class ErrorNotificationHandler implements Consumer<ExceptionReceivedEventArgs>
    {
        @Override
        public void accept(ExceptionReceivedEventArgs t)
        {
            System.out.println("SAMPLE: Host " + t.getHostname() + " received general error notification during " + t.getAction() + ": " + t.getException().toString());
        }
    }
    ```
2. 사용 하 여 hello 다음 toocreate 라는 새 클래스가 코드 `EventProcessor`합니다.
   
    ```java
    import com.microsoft.azure.eventhubs.EventData;
    import com.microsoft.azure.eventprocessorhost.CloseReason;
    import com.microsoft.azure.eventprocessorhost.IEventProcessor;
    import com.microsoft.azure.eventprocessorhost.PartitionContext;
   
    public class EventProcessor implements IEventProcessor
    {
        private int checkpointBatchingCount = 0;
   
        @Override
        public void onOpen(PartitionContext context) throws Exception
        {
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " is opening");
        }
   
        @Override
        public void onClose(PartitionContext context, CloseReason reason) throws Exception
        {
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " is closing for reason " + reason.toString());
        }
   
        @Override
        public void onError(PartitionContext context, Throwable error)
        {
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " onError: " + error.toString());
        }
   
        @Override
        public void onEvents(PartitionContext context, Iterable<EventData> messages) throws Exception
        {
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " got message batch");
            int messageCount = 0;
            for (EventData data : messages)
            {
                System.out.println("SAMPLE (" + context.getPartitionId() + "," + data.getSystemProperties().getOffset() + "," +
                        data.getSystemProperties().getSequenceNumber() + "): " + new String(data.getBody(), "UTF8"));
                messageCount++;
   
                this.checkpointBatchingCount++;
                if ((checkpointBatchingCount % 5) == 0)
                {
                    System.out.println("SAMPLE: Partition " + context.getPartitionId() + " checkpointing at " +
                        data.getSystemProperties().getOffset() + "," + data.getSystemProperties().getSequenceNumber());
                    context.checkpoint(data);
                }
            }
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " batch size was " + messageCount + " for host " + context.getOwner());
        }
    }
    ```
3. 라는 하나의 더 많은 클래스를 만들어 `EventProcessorSample`를 사용 하 여 다음 코드 hello 합니다.
   
    ```java
    import com.microsoft.azure.eventprocessorhost.*;
    import com.microsoft.azure.servicebus.ConnectionStringBuilder;
    import com.microsoft.azure.eventhubs.EventData;
   
    public class EventProcessorSample
    {
        public static void main(String args[])
        {
            final String consumerGroupName = "$Default";
            final String namespaceName = "----ServiceBusNamespaceName-----";
            final String eventHubName = "----EventHubName-----";
            final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
            final String sasKey = "---SharedAccessSignatureKey----";
   
            final String storageAccountName = "---StorageAccountName----";
            final String storageAccountKey = "---StorageAccountKey----";
            final String storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=" + storageAccountName + ";AccountKey=" + storageAccountKey;
   
            ConnectionStringBuilder eventHubConnectionString = new ConnectionStringBuilder(namespaceName, eventHubName, sasKeyName, sasKey);
   
            EventProcessorHost host = new EventProcessorHost(eventHubName, consumerGroupName, eventHubConnectionString.toString(), storageConnectionString);
   
            System.out.println("Registering host named " + host.getHostName());
            EventProcessorOptions options = new EventProcessorOptions();
            options.setExceptionNotification(new ErrorNotificationHandler());
            try
            {
                host.registerEventProcessor(EventProcessor.class, options).get();
            }
            catch (Exception e)
            {
                System.out.print("Failure while registering: ");
                if (e instanceof ExecutionException)
                {
                    Throwable inner = e.getCause();
                    System.out.println(inner.toString());
                }
                else
                {
                    System.out.println(e.toString());
                }
            }
   
            System.out.println("Press enter toostop");
            try
            {
                System.in.read();
                host.unregisterEventProcessor();
   
                System.out.println("Calling forceExecutorShutdown");
                EventProcessorHost.forceExecutorShutdown(120);
            }
            catch(Exception e)
            {
                System.out.println(e.toString());
                e.printStackTrace();
            }
   
            System.out.println("End of sample");
        }
    }
    ```
4. Hello 이벤트 허브 및 저장소 계정을 만들 때 사용한 hello 값이 포함 된 필드를 다음 hello를 대체 합니다.
   
    ```java
    final String namespaceName = "----ServiceBusNamespaceName-----";
    final String eventHubName = "----EventHubName-----";
   
    final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
    final String sasKey = "---SharedAccessSignatureKey----";
   
    final String storageAccountName = "---StorageAccountName----"
    final String storageAccountKey = "---StorageAccountKey----";
    ```

> [!NOTE]
> 이 자습서에서는 EventProcessorHost의 단일 인스턴스를 사용합니다. tooincrease 처리량 것은 실행 하는 좋습니다 EventProcessorHost의 여러 인스턴스 가급적 별도 컴퓨터에 있습니다.  그러면 중복성도 함께 제공됩니다. 이러한 경우 hello 다양 한 인스턴스는 자동으로 서로 순서 tooload 균형 hello 조정 이벤트를 받았습니다. 여러 개의 수신기 tooeach 프로세스를 원하는 경우 *모든* 이벤트 hello hello를 사용 해야 **ConsumerGroup** 개념입니다. 서로 다른 컴퓨터에서 이벤트를 받을 때의 배포 된 hello 컴퓨터 (또는 역할)에 따라 EventProcessorHost 인스턴스에 대 한 유용한 toospecify 이름을 수 있습니다.
> 
> 

## <a name="next-steps"></a>다음 단계
Hello 다음 링크를 방문 하 여 이벤트 허브에 대 한 자세히 알아볼 수 있습니다.

* [이벤트 허브 개요](event-hubs-what-is-event-hubs.md)
* [이벤트 허브 만들기](event-hubs-create.md)
* [Event Hubs FAQ](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[Azure Storage account]: ../storage/common/storage-create-storage-account.md
[Azure portal]: https://portal.azure.com
[Maven Package]: https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs-eph%22

<!-- Images -->
[11]: ./media/service-bus-event-hubs-get-started-receive-ephjava/create-eph-csharp2.png
[12]: ./media/service-bus-event-hubs-get-started-receive-ephjava/create-eph-csharp3.png

---
title: "Java를 통해 aaaHow toouse Azure 서비스 버스 큐 | Microsoft Docs"
description: "Azure에서 서비스 버스 toouse 큐 대기 하는 방법에 대해 알아봅니다. 코드 샘플은 Java로 작성되었습니다."
services: service-bus-messaging
documentationcenter: java
author: sethmanheim
manager: timlt
ms.assetid: f701439c-553e-402c-94a7-64400f997d59
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: f68e941438134090c5eee53459e7667bda13ff3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-java"></a>Java를 통해 toouse 서비스 버스 큐 대기 하는 방법
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

이 문서에서는 설명 방법을 toouse 서비스 버스 큐입니다. hello 샘플 Java 작성 되 고 hello를 사용 하 여 [Azure SDK for Java][Azure SDK for Java]합니다. hello 가이드에서 다루는 시나리오 포함 **큐를 만드는**, **메시지 보내기 및 받기**, 및 **큐 삭제**합니다.

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="configure-your-application-toouse-service-bus"></a>사용자 응용 프로그램 toouse 서비스 버스를 구성 합니다.
Hello를 설치 했는지 확인 [Azure SDK for Java] [ Azure SDK for Java] 이 샘플을 작성 하기 전에. Eclipse를 사용 하는 경우에 hello을 설치할 수 있습니다 [Azure Toolkit for Eclipse] [ Azure Toolkit for Eclipse] hello Java 용 Azure SDK를 포함 하는 합니다. Hello를 추가할 수 있습니다 **Microsoft Azure Libraries for Java** tooyour 프로젝트:

![](./media/service-bus-java-how-to-use-queues/eclipselibs.png)

Hello 다음 추가 `import` 문 toohello 맨 hello Java 파일:

```java
// Include hello following imports toouse Service Bus APIs
import com.microsoft.windowsazure.services.servicebus.*;
import com.microsoft.windowsazure.services.servicebus.models.*;
import com.microsoft.windowsazure.core.*;
import javax.xml.datatype.*;
```

## <a name="create-a-queue"></a>큐 만들기
**ServiceBusContract** 클래스를 통해 Service Bus 큐에 대한 관리 작업을 수행할 수 있습니다. A **ServiceBusContract** 개체,와 hello toomanage 사용 권한 사용 하 여 SAS 토큰을 캡슐화 하는 적절 한 구성이로 구성 되며 **ServiceBusContract** 클래스는 hello 유일한 지점 Azure와 통신 합니다.

hello **ServiceBusService** toocreate 메서드를 제공 하는 클래스, 열거 및 큐를 삭제 합니다. 다음 예제에서는 어떻게 hello는 **ServiceBusService** 개체 라는 큐를 사용 하는 toocreate 수 `TestQueue`, 라는 네임 스페이스와 `HowToSample`:

```java
Configuration config =
    ServiceBusConfiguration.configureWithSASAuthentication(
            "HowToSample",
            "RootManageSharedAccessKey",
            "SAS_key_value",
            ".servicebus.windows.net"
            );

ServiceBusContract service = ServiceBusService.create(config);
QueueInfo queueInfo = new QueueInfo("TestQueue");
try
{
    CreateQueueResult result = service.createQueue(queueInfo);
}
catch (ServiceException e)
{
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

에 메서드가 있습니다 `QueueInfo` hello 큐 toobe 튜닝의 속성을 허용 하는 (예: tooset hello 기본 활성 시간 (TTL) 값 적용 toobe toomessages toohello 큐 전송) 합니다. hello 다음 예제에서는 어떻게 toocreate 큐 라는 `TestQueue` 5GB의 최대 크기:

````java
long maxSizeInMegabytes = 5120;
QueueInfo queueInfo = new QueueInfo("TestQueue");
queueInfo.setMaxSizeInMegabytes(maxSizeInMegabytes);
CreateQueueResult result = service.createQueue(queueInfo);
````

Hello를 사용할 수 있는 참고 `listQueues` 메서드를 **ServiceBusContract** 서비스 네임 스페이스 내에서 지정 된 이름의 큐가 이미 있으면 toocheck 개체입니다.

## <a name="send-messages-tooa-queue"></a>송신 메시지 tooa 큐
메시지 tooa 서비스 버스 큐 toosend 프로그램 응용 프로그램 구성 파일을 **ServiceBusContract** 개체입니다. 코드에서 보여 주는 방법을 다음 hello toosend hello에 대 한 메시지 `TestQueue` hello에서 이전에 만든 큐 `HowToSample` 네임 스페이스:

```java
try
{
    BrokeredMessage message = new BrokeredMessage("MyMessage");
    service.sendQueueMessage("TestQueue", message);
}
catch (ServiceException e)
{
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

메시지 전송 및 서비스 버스에서 수신 큐는 hello 인스턴스의 [BrokeredMessage] [ BrokeredMessage] 클래스입니다. [BrokeredMessage] [ BrokeredMessage] 개체에는 표준 속성 집합이 있습니다 (예: [레이블](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.label#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) 및 [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.timetolive#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), 사용 되는 toohold 사용자 지정 사전 응용 프로그램 관련 속성 및 임의 응용 프로그램 데이터의 본문입니다. 응용 프로그램의 hello hello 생성자에 직렬화 된 개체를 전달 하 여 hello hello 메시지 본문을 설정할 수 [BrokeredMessage][BrokeredMessage], hello 적절 한 serializer가 사용 됩니다 하 고 tooserialize hello 개체입니다. 또는 **java.IO.InputStream** 개체를 제공할 수 있습니다.

hello 다음 예제에서는 5 toosend 테스트 toothe 메시지 방법을 `TestQueue` **MessageSender** hello 이전 코드 조각의 얻 었:

```java
for (int i=0; i<5; i++)
{
     // Create message, passing a string message for hello body.
     BrokeredMessage message = new BrokeredMessage("Test message " + i);
     // Set an additional app-specific property.
     message.setProperty("MyProperty", i);
     // Send message toohello queue
     service.sendQueueMessage("TestQueue", message);
}
```

서비스 버스 큐 최대 메시지 크기는 256KB hello 지원 [표준 계층](service-bus-premium-messaging.md) 및 hello에서 1 MB [Premium 계층](service-bus-premium-messaging.md)합니다. hello 표준 및 사용자 지정 응용 프로그램 속성을 포함 하는 hello 헤더는 64KB의 최대 크기를 가질 수 있습니다. 큐에 유지 하는 메시지의 hello 수를 제한 하지 않으며 cap hello 총 크기는 큐에서 대기 하는 hello 메시지에입니다. 이 큐 크기는 생성 시 정의되며 상한이 5GB입니다.

## <a name="receive-messages-from-a-queue"></a>큐에서 메시지 받기
큐에서 hello 기본적인 방법은 tooreceive 메시지는 toouse는 **ServiceBusContract** 개체입니다. 받은 메시지는 **ReceiveAndDelete** 및 **PeekLock**의 두 가지 모드로 작동할 수 있습니다.

Hello를 사용 하는 경우 **ReceiveAndDelete** 모드에서는 수신은 1 단계 작업-즉, 서비스 버스 큐의 메시지에 대 한 읽기 요청을 받으면 hello 메시지 사용 되는 것을 표시 하 고 toohello 응용 프로그램을 반환 합니다. **ReceiveAndDelete** 모드 (기본 모드 hello)는 hello 간단한 모델 이며는 응용 프로그램은 오류의 hello 이벤트에서 메시지를 처리 하지 허용할 수 없는 시나리오에 가장 적합 합니다. toounderstand hello는 hello 소비자 문제에 요청을 수신 하는 시나리오 및 후 처리 하기 전에 크래시 합니다.
서비스 버스 사용 되는 것을 다음 hello 응용 프로그램 다시 시작 되 고 메시지 사용을 시작할 때 hello 메시지를 표시 한 됩니다, 때문에 누락 됩니다 hello 메시지 했던 이전 toohello 크래시를 사용 합니다.

**PeekLock** 모드에서는 수신 하므로 누락 된 메시지를 허용할 수 없는 가능한 toosupport 응용 프로그램 2 단계 작업이 됩니다. 서비스 버스 요청을 받으면 다음 메시지 toobe hello 사용 다른 소비자가 수신할 tooprevent 잠근 하 고 toohello 응용 프로그램 반환 찾습니다. Hello hello의 두 번째 단계를 완료 후 hello 응용 프로그램 hello 메시지 처리를 완료 (또는 이후 처리를 위해 안정적으로 저장)를 호출 하 여 수신 프로세스 **삭제** hello 받은 메시지에 합니다. 서비스 버스 hello를 표시 하는 경우 **삭제** 호출 hello 메시지를 사용 되 고 표시 하 고 hello 큐에서 제거 합니다.

hello 다음 예제에서는 메시지를 수신할 수 방법 및 처리를 사용 하 여 **PeekLock** 모드 (하지 hello 기본 모드). hello 아래 예제에서는 무한 루프에 메시지를 처리 하에 도착 했을 때 우리의 `TestQueue`:

```java
try
{
    ReceiveMessageOptions opts = ReceiveMessageOptions.DEFAULT;
    opts.setReceiveMode(ReceiveMode.PEEK_LOCK);

    while(true)  {
         ReceiveQueueMessageResult resultQM =
                 service.receiveQueueMessage("TestQueue", opts);
        BrokeredMessage message = resultQM.getValue();
        if (message != null && message.getMessageId() != null)
        {
            System.out.println("MessageID: " + message.getMessageId());
            // Display hello queue message.
            System.out.print("From queue: ");
            byte[] b = new byte[200];
            String s = null;
            int numRead = message.getBody().read(b);
            while (-1 != numRead)
            {
                s = new String(b);
                s = s.trim();
                System.out.print(s);
                numRead = message.getBody().read(b);
            }
            System.out.println();
            System.out.println("Custom Property: " +
                message.getProperty("MyProperty"));
            // Remove message from queue.
            System.out.println("Deleting this message.");
            //service.deleteMessage(message);
        }  
        else  
        {
            System.out.println("Finishing up - no more messages.");
            break;
            // Added toohandle no more messages.
            // Could instead wait for more messages toobe added.
        }
    }
}
catch (ServiceException e) {
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
catch (Exception e) {
    System.out.print("Generic exception encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Toohandle 응용 프로그램이 크래시 되는 방법 및 읽을 수 없는 메시지
서비스 버스 기능 toohelp 정상적으로 응용 프로그램 또는 메시지를 처리 하는 데 문제가 오류 로부터 복구를 제공 합니다. 수신기 응용 프로그램 수 없는 경우 몇 가지 이유로 tooprocess 환영 메시지가 다음 hello를 호출할 수 있습니다 **unlockMessage** 메서드를 수신 하는 hello 메시지 (hello 대신 **deleteMessage** 메서드). 이 인해 서비스 버스 toounlock hello hello 큐 내에서 메시지와 수신, 다시 사용할 수 있는 toobe 확인 하거나으로 hello를 많이 사용 응용 프로그램 또는 다른 소비 응용 프로그램에서 동일 합니다.

(예를 들어 hello 응용 프로그램이 충돌할 경우) 잠금 시간 제한이 만료 되기 전에 hello 응용 프로그램 실패 tooprocess hello 메시지는 큐에 메시지와 관련 된 제한 시간 이기도 다음 서비스 버스 hello 메시지를 자동으로 잠금 해제 하 고 수신 다시 사용할 수 있는 toobe가 있습니다.

Hello hello 응용 프로그램 이벤트 충돌 hello 메시지 처리 전후에 그러나 hello 전에 **deleteMessage** 요청이 발생 한 후 다시 시작할 때 hello 메시지는 다시 전달한 toohello 응용 프로그램입니다. 이 이라고 하는데 *일단 처리 이상*; 즉, 각 메시지가 최소 한 번 처리 되지만 특정 상황 hello에 동일한 메시지를 다시 배달 될 수 있습니다. Hello 시나리오 중복 처리가 허용 되지 않는, 응용 프로그램 개발자가 추가 논리 tootheir 응용 프로그램을 toohandle 중복 메시지 배달을 추가 해야 합니다. 이 대개 달성 hello를 사용 하 여 **getMessageId** 메서드 hello 메시지를 배달 시도에서 일관적으로 유지 합니다.

## <a name="next-steps"></a>다음 단계
서비스 버스 큐의 hello 기본 사항 학습 한, 했으므로 참조 [큐, 토픽 및 구독] [ Queues, topics, and subscriptions] 자세한 정보에 대 한 합니다.

자세한 내용은 참조 hello [Java 개발자 센터](https://azure.microsoft.com/develop/java/)합니다.

[Azure SDK for Java]: http://azure.microsoft.com/develop/java/
[Azure Toolkit for Eclipse]: https://msdn.microsoft.com/library/azure/hh694271.aspx
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage

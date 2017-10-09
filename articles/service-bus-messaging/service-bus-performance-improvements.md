---
title: "Azure 서비스 버스를 사용 하 여 성능을 향상 시키기 위한 aaaBest 사례 | Microsoft Docs"
description: "교환할 때 서비스 버스 toooptimize 성능 toouse 메시지를 조정 하는 방법을 설명 합니다."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: e756c15d-31fc-45c0-8df4-0bca0da10bb2
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/10/2017
ms.author: sethm
ms.openlocfilehash: 52764d227757cbb11246675878933f21685817f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-performance-improvements-using-service-bus-messaging"></a>Service Bus 메시징을 사용한 성능 향상의 모범 사례

이 문서에서는 설명 방법을 toouse [Azure 서비스 버스 메시징](https://azure.microsoft.com/services/service-bus/) toooptimize 성능을 교환할 때 메시지를 조정 합니다. 이 항목의 첫 번째 부분 hello hello toohelp 증가 성능이 제공 되는 서로 다른 메커니즘을 설명 합니다. 두 번째 부분은 hello 방법을 제공할 수 있는 방식으로 서비스 버스 toouse hello 지정된 된 시나리오에서 성능을 최대화 하에 지침을 제공 합니다.

이 항목 전반 hello 라는 용어 "클라이언트" 서비스 버스에 액세스 하는 tooany 엔터티를 나타냅니다. 클라이언트는 발신자 또는 수신자의 hello 역할을 사용할 수 있습니다. "sender" hello 용어 메시지 tooa 서비스 버스 큐 또는 항목을 전송 하는 서비스 버스 큐 또는 항목 클라이언트에 사용 됩니다. hello "수신자" 이라는 용어는 tooa 서비스 버스 큐 또는 구독 클라이언트를 서비스 버스 큐 또는 구독에서 메시지를 수신 합니다.

이 섹션에서는 서비스 버스 toohelp 성능을 높이기를 사용 하는 몇 가지 개념을 소개 합니다.

## <a name="protocols"></a>프로토콜
서비스 버스 클라이언트 toosend 있으며 특정 프로토콜 중 하나를 통해 메시지를 수신 합니다.

1. AMQP(고급 메시지 큐 프로토콜)
2. SBMP(Service Bus 메시징 프로토콜)
3. HTTP

AMQP 및 SBMP는 hello 메시징 팩터리 존재 hello 연결 tooService 버스 유지 하기 때문에 더 효율적입니다. 또한 일괄 처리와 프리페치도 구현합니다. 명시적으로 언급 하지 않는 한이 항목의 모든 콘텐츠는 AMQP 또는 SBMP hello 사용을 가정 합니다.

## <a name="reusing-factories-and-clients"></a>팩터리 및 클라이언트 다시 사용
[QueueClient][QueueClient] 또는 [MessageSender][MessageSender]와 같은 Service Bus 클라이언트 개체는 내부 연결 관리도 제공하는 [MessagingFactory][MessagingFactory] 개체를 통해 만듭니다. 메시징 팩터리 나 큐, 항목 및 구독 클라이언트는 메시지를 보내고 다음 다시 작성 hello 다음 메시지를 보낼 때 후 닫기 해야 합니다. Hello 팩터리를 다시 만들 때 새 연결이 설정 되 및 hello 연결 toohello 서비스 버스 서비스를 삭제 하는 메시징 팩터리를 닫으면 합니다. 여러 작업에 대 한 개체 연결이 다시 사용 하 여 방지할 수 있습니다는 비용이 많이 드는 작업 hello 같은 팩터리 및 클라이언트를 설정 합니다. Hello를 안전 하 게 사용할 수 있습니다 [QueueClient] [ QueueClient] 동시 비동기 작업 및 다중 스레드에서 메시지를 보내기 위한 개체입니다. 

## <a name="concurrent-operations"></a>동시 작업
작업(보내기, 받기, 삭제 등) 수행은 다소 시간이 걸립니다. 이 시간 hello 요청과 hello 회신의 추가 toohello 대기 시간에 서비스 버스 서비스 hello 하 여 hello hello 작업 처리를 포함합니다. 시간당 작업 tooincrease hello 번호 작업이 동시에 실행 해야 합니다. 이 작업은 다양한 방법으로 수행할 수 있습니다.

* **비동기 작업**: hello 클라이언트는 비동기 작업을 수행 하 여 작업을 예약 합니다. hello 이전 요청을 완료 하기 전에 hello 다음 요청이 시작 됩니다. hello 다음은 비동기 보내기 작업의 예입니다.
  
 ```csharp
  BrokeredMessage m1 = new BrokeredMessage(body);
  BrokeredMessage m2 = new BrokeredMessage(body);
  
  Task send1 = queueClient.SendAsync(m1).ContinueWith((t) => 
    {
      Console.WriteLine("Sent message #1");
    });
  Task send2 = queueClient.SendAsync(m2).ContinueWith((t) => 
    {
      Console.WriteLine("Sent message #2");
    });
  Task.WaitAll(send1, send2);
  Console.WriteLine("All messages sent");
  ```
  
  다음은 비동기 수신 작업의 예제입니다.
  
  ```csharp
  Task receive1 = queueClient.ReceiveAsync().ContinueWith(ProcessReceivedMessage);
  Task receive2 = queueClient.ReceiveAsync().ContinueWith(ProcessReceivedMessage);
  
  Task.WaitAll(receive1, receive2);
  Console.WriteLine("All messages received");
  
  async void ProcessReceivedMessage(Task<BrokeredMessage> t)
  {
    BrokeredMessage m = t.Result;
    Console.WriteLine("{0} received", m.Label);
    await m.CompleteAsync();
    Console.WriteLine("{0} complete", m.Label);
  }
  ```
* **여러 팩터리**:에 의해 만들어진 모든 클라이언트 (보낸 사람 더하기 tooreceivers) hello 같은 팩터리 공유 하나의 TCP 연결 합니다. hello 최대 메시지 처리량이 TCP 연결을 통과할 수 있는 작업의 hello 수로 제한 됩니다. 단일 팩터리를 통해 얻을 수 있는 hello 처리량 TCP 왕복 시간 및 메시지 크기를 크게 달라 집니다. 처리량 속도 더 tooobtain, 여러 메시징 팩터리를 사용 해야 합니다.

## <a name="receive-mode"></a>수신 모드
큐 또는 구독 클라이언트를 만들 때 *보기-잠금* 또는 *수신 및 삭제* 중에서 수신 모드를 지정할 수 있습니다. hello 기본 수신 모드는 [PeekLock][PeekLock]합니다. 이 모드에서 작업할 때 클라이언트 hello 메시지를 보냅니다 요청 tooreceive 서비스 버스에서. Hello 클라이언트 hello 메시지를 받은 경우 요청 toocomplete hello 메시지를 보냅니다.

Hello 설정 수신 모드 너무[ReceiveAndDelete][ReceiveAndDelete], 두 단계가 단일 요청에 결합 됩니다. 작업의 전체 번호가 hello 줄어들고 hello를 향상 시킬 수 있습니다이 전반적인 메시지 처리량입니다. 메시지가 손실의 위험 hello에 성능상의 이점이 제공 됩니다.

서비스 버스는 수신 및 삭제 작업에 대한 트랜잭션을 지원하지 않습니다. 또한 미리 보기-잠금 의미 체계는 어떤 hello에 클라이언트가 원하는 toodefer 모든 시나리오에 필요 하거나 [배달 못 한 편지](service-bus-dead-letter-queues.md) 메시지입니다.

## <a name="client-side-batching"></a>클라이언트 쪽 일괄 처리
큐 또는 항목 클라이언트 toodelay hello 메시지 보내기를 일정 기간에 대 한 클라이언트 쪽 일괄 처리 수 있습니다. 클라이언트 hello이 시간 동안 추가 메시지를 보내면, 단일 일괄 처리의 hello 메시지를 전송 합니다. 클라이언트 쪽 일괄 처리 큐 또는 구독 클라이언트 toobatch로 인해 여러 **완료** 단일 요청으로 요청 합니다. 일괄 처리는 비동기 **전송** 및 **완료** 작업에만 사용할 수 있습니다. 동기 작업 toohello 서비스 버스 서비스를 즉시 전송 됩니다. 일괄 처리는 보기 또는 수신 작업에 대해 발생하지 않으며 클라이언트 전반에서도 발생하지 않습니다.

기본적으로 클라이언트는 20ms의 배치 간격을 사용합니다. Hello 설정 하 여 hello 일괄 처리 간격을 변경할 수 있습니다 [BatchFlushInterval] [ BatchFlushInterval] 속성을 만들기 전에 hello 메시징 팩터리입니다. 이 설정은이 이 팩터리에서 만든 모든 클라이언트에 영향을 줍니다.

hello 설정 toodisable 일괄 처리, [BatchFlushInterval] [ BatchFlushInterval] 속성 너무**TimeSpan.Zero**합니다. 예:

```csharp
MessagingFactorySettings mfs = new MessagingFactorySettings();
mfs.TokenProvider = tokenProvider;
mfs.NetMessagingTransportSettings.BatchFlushInterval = TimeSpan.FromSeconds(0.05);
MessagingFactory messagingFactory = MessagingFactory.Create(namespaceUri, mfs);
```

일괄 처리 hello 청구 가능한 메시징 작업 수에 영향을 주지 않습니다 되며 hello 서비스 버스 클라이언트 프로토콜에 대해서만 사용할 수 있습니다. HTTP 프로토콜 hello 일괄 처리를 지원 하지 않습니다.

## <a name="batching-store-access"></a>저장소 액세스 일괄 처리
큐, 항목 또는 구독의 tooincrease hello 처리량, tooits 내부 저장소에 쓸 때 서비스 버스 여러 개의 메시지 일괄 처리. 큐 또는 항목에서 활성화 hello 저장소로의 메시지 쓰기가 일괄 처리할 됩니다. 큐 또는 구독에서 활성화 hello 저장소에서 메시지를 삭제 일괄 처리할 됩니다. 엔터티에 대 한 일괄 처리 방식된 저장소 액세스를 사용 하는 경우 서비스 버스 too20ms 구성 하 여 해당 엔터티에 대 한 저장소 쓰기 작업을 지연 됩니다. 이 간격 동안 발생 하는 추가 저장소 작업 toohello 일괄 처리에 추가 됩니다. 일괄 처리된 저장소 액세스는 **전송** 및 **완료** 작업에만 영향을 주고 수신 작업은 영향을 받지 않습니다. 일괄 처리된 저장소 액세스는 엔터티의 속성입니다. 일괄 처리는 일괄 처리된 저장소 액세스가 가능한 모든 엔터티에서 발생합니다.

새 큐, 토픽 또는 구독을 만들면 기본적으로 일괄 처리된 저장소 액세스가 사용하도록 설정됩니다. toodisable 일괄 저장소 액세스, 집합 hello [EnableBatchedOperations] [ EnableBatchedOperations] 속성 너무**false** hello 엔터티를 만들기 전에 합니다. 예:

```csharp
QueueDescription qd = new QueueDescription();
qd.EnableBatchedOperations = false;
Queue q = namespaceManager.CreateQueue(qd);
```

일괄 처리 방식된 저장소 액세스 hello 청구 가능한 메시징 작업 수에 영향을 주지 않습니다 되며, 큐, 항목 또는 구독의 속성입니다. Hello 독립적일 수신 하는 클라이언트 및 서비스 버스 서비스 hello 간에 사용 되는 모드와 hello 프로토콜입니다.

## <a name="prefetching"></a>프리페치
프리페치는 수신 작업을 수행할 때 hello 큐 또는 구독 클라이언트 tooload 추가 서비스에서 메시지를 hello 수 있습니다. hello 클라이언트는 로컬 캐시에서 이러한 메시지를 저장합니다. hello 캐시의 hello 크기 hello 따라 사용자가 [QueueClient.PrefetchCount] [ QueueClient.PrefetchCount] 또는 [SubscriptionClient.PrefetchCount] [ SubscriptionClient.PrefetchCount] 속성입니다. 프리페치를 사용할 수 있는 각 클라이언트는 각각의 캐시를 유지합니다. 캐시는 클라이언트 사이에서 공유되지 않습니다. Hello 클라이언트가 수신 작업을 시작 하는 경우 해당 캐시가 비어 hello 서비스는 메시지의 일괄 처리를 전송 합니다. hello hello 일괄 처리 크기는 hello 크기 hello 캐시 또는 256KB 이면 중 더 작은 값입니다. 수신 작업을 시작 하는 hello 클라이언트 hello 캐시에 메시지를 포함 하는 경우 hello 캐시에서 hello 메시지를 가져옵니다.

때 메시지를 프리페치 hello 서비스 잠금이 hello 프리페치된 메시지입니다. 이 작업을 수행 하 여 다른 수신기가 hello 프리페치된 메시지를 받을 수 없습니다. Hello 수신기를 완료할 수 없으면 hello 메시지 hello 잠금이 만료 되기 전에 사용할 수 있는 tooother 수신기 hello 메시지에 있게 됩니다. 사전 인출 hello hello 메시지 사본을 hello 캐시에 남아 있습니다. hello hello를 사용 하는 수신기 만료 캐시 된 복사본에서 해당 메시지 toocomplete 읽으려고 할 때 예외를 수신 합니다. 기본적으로 hello 메시지 잠금은 60 초 후에 만료 됩니다. 이 값은 확장된 too5 분 수 있습니다. 만료 된 메시지의 tooprevent hello 소비, hello 캐시 크기가 항상 보다 작아야 hello hello 잠금 시간 제한 간격 내 클라이언트에서 사용할 수 있는 메시지 수입니다.

좋은 값을 60 초 hello 기본 잠금 만료를 사용할 경우 [SubscriptionClient.PrefetchCount] [ SubscriptionClient.PrefetchCount] 최대 20 회 hello 처리는 모든 hello 팩터리 수신자의 속도입니다. 예를 들어 팩터리가 수신자 3 개 및 각 수신자는 초당 too10 메시지를 처리할 수 있습니다. hello 프리페치 수는 20 X 3 X 10 = 600을 넘지 않아야 합니다. 기본적으로 [QueueClient.PrefetchCount] [ QueueClient.PrefetchCount] hello 서비스에서 추가 메시지를 가져오지는 즉 집합 too0 됩니다.

증가 hello 메시지 작업 또는 왕복 전체 번호가 감소 하므로 큐 또는 구독에 대 한 전반적인 처리량 hello 메시지를 프리페치 합니다. 그러나 Hello 첫 번째 메시지를 인출 합니다. 더 오래 걸립니다 (인해 증가 toohello 메시지 크기). 프리페치된 메시지를 받는 속도가 더 빠를 수 hello 클라이언트가 이미 다운로드 된 이러한 메시지입니다.

메시지의 hello 활성 시간 (TTL) 속성이 hello 서버 hello 메시지 toohello 클라이언트 전송 hello 시 hello 서버에 의해 확인 됩니다. hello 클라이언트 hello 메시지를 받을 때 hello 메시지의 TTL 속성을 확인 하지 않습니다. 대신, hello 클라이언트 hello 메시지를 캐시 하는 동안 hello 메시지의 TTL이 경과 하는 경우에 hello 메시지를 받을 수 있습니다.

프리페치 hello 청구 가능한 메시징 작업 수에 영향을 주지 않습니다 되며 hello 서비스 버스 클라이언트 프로토콜에 대해서만 사용할 수 있습니다. HTTP 프로토콜 hello 프리페치를 지원 하지 않습니다. 프리페치는 동기 및 비동기 수신 작업에 사용할 수 있습니다.

## <a name="express-queues-and-topics"></a>명시적 큐 및 토픽

Express 엔터티는 높은 처리량 및 대기 시간 단축된 시나리오를 사용 하도록 설정 하 고 hello 표준 메시징 계층 에서만 지원 됩니다. 만든 엔터티 [Premium 네임 스페이스](service-bus-premium-messaging.md) hello express 옵션을 지원 하지 않습니다. Express 엔터티 사용 tooa 큐 또는 항목에는 메시지를 보내는 경우 hello 메시지는 되지 즉시 hello 메시징 저장소에 저장 합니다. 대신 메모리에 캐시됩니다. 여러 시간 (초)에 대 한 hello 큐에 메시지가 남아 있으면 tooan 중단 인해 손실 로부터 보호할 toostable 저장소, 자동으로 기록 됩니다. 메모리 캐시로 hello 메시지 처리량이 증가 및 없습니다 액세스 toostable 있기 때문에 대기 시간이 단축 작성 hello 시간 hello 메시지 저장소에 전송 됩니다. 몇 초 내에 사용 되는 메시지는 메시지 저장소 toohello를 기록 되지 않습니다. 다음 예제는 hello express 항목을 만듭니다.

```csharp
TopicDescription td = new TopicDescription(TopicName);
td.EnableExpress = true;
namespaceManager.CreateTopic(td);
```

Hello 보낸 사람에 게 서비스 버스를 강제할 수 손실 되지 않아야 하는 중요 한 정보를 포함 하는 메시지를 보내면 tooan express 엔터티로 tooimmediately 영구 hello 설정 하 여 hello 메시지 toostable 저장소 [ForcePersistence] [ ForcePersistence] 속성 너무**true**합니다.

> [!NOTE]
> 기본 엔터티는 트랜잭션을 지원하지 않습니다.

## <a name="use-of-partitioned-queues-or-topics"></a>분할된 큐 또는 토픽 사용
내부적으로 사용 하 여 서비스 버스 같은 노드 및 메시징 저장소 tooprocess hello 및 메시징 엔터티 (큐 또는 항목)에 대 한 모든 메시지를 저장 합니다. 분할 된 큐 또는 항목 hello에 다른 손 여러 노드 및 메시징 저장소에서 배포 됩니다. 분할된 큐와 토픽은 일반 큐 및 토픽보다 높은 처리량뿐만 아니라 뛰어난 가용성을 제공합니다. toocreate 분할된 된 엔터티 집합 hello [EnablePartitioning] [ EnablePartitioning] 속성 너무**true**hello 다음 예제에에서 나온 것 처럼 합니다. 분할된 엔터티에 대한 자세한 내용은 [분할된 메시징 엔터티][Partitioned messaging entities]를 참조하세요.

```csharp
// Create partitioned queue.
QueueDescription qd = new QueueDescription(QueueName);
qd.EnablePartitioning = true;
namespaceManager.CreateQueue(qd);
```

## <a name="use-of-multiple-queues"></a>여러 큐 사용

분할 된 큐 또는 항목 또는 hello 예상 단일 분할 된 큐 또는 항목에서 부하를 처리할 수 없는 가능한 toouse 없는 경우에 여러 메시징 엔터티를 사용 해야 합니다. 여러 엔터티를 사용할 때 각 엔터티에 대해 전용된 클라이언트를 만들고, 사용 하는 대신 동일한 hello 모든 엔터티에 대 한 클라이언트입니다.

## <a name="development-and-testing-features"></a>개발 및 테스트 기능

Service Bus에는 특별히 **프로덕션 구성에서 사용해서는 안 되는** 개발에 사용되는 한 가지 기능이 있습니다. [TopicDescription.EnableFilteringMessagesBeforePublishing][]

새 규칙 또는 필터 toohello 항목을 추가 하는 경우 사용할 수 있습니다 [TopicDescription.EnableFilteringMessagesBeforePublishing][] 새 필터 식을 hello tooverify 예상 대로 작동 합니다.

## <a name="scenarios"></a>시나리오
hello 다음 섹션에서는 일반적인 메시징 시나리오에 설명 하 고 기본 설정 hello 서비스 버스 설정을 설명 합니다. 처리량 속도는 적음(초당 1개 메시지 미만), 보통(초당 1개 메시지 이상, 초당 100개 메시지 미만), 높음(초당 100개 메시지 이상)으로 분류됩니다. hello 클라이언트 수가으로 분류 됩니다 (5 개 더 적은) 보통 (5 개 보다 많이 미만 이지만 또는 같은 too20), 및 대형 (둘 이상의 20).

### <a name="high-throughput-queue"></a>처리량이 높은 큐
목표: 단일 큐의 hello 처리량을 최대화 합니다. 발신자와 수신자의 hello 수는 적습니다.

* 성능 및 가용성 향상을 위해 분할된 큐를 사용합니다.
* 전반적인 tooincrease hello hello 큐로 전송 속도, 여러 메시지 팩터리 toocreate 보낸 사람을 사용 합니다. 각 발신기에 대해 비동기 작업이나 여러 스레드를 사용합니다.
* 전반적인 tooincrease hello hello 큐에서 수신 속도, 여러 메시지 팩터리 toocreate 수신기를 사용 합니다.
* 클라이언트 쪽 일괄 처리의 비동기 작업 tootake 장점은 사용 합니다.
* 서비스 버스 클라이언트 프로토콜 전송 간격 too50ms tooreduce hello 수 일괄 처리 하는 hello를 설정 합니다. 여러 발신자를 사용 하는 hello 간격 too100ms 일괄 처리를 늘립니다.
* 일괄 처리된 저장소 액세스는 사용하도록 설정한 상태로 둡니다. 전반적인 hello 증가 속도는 메시지 hello 큐에 쓸 수 있습니다.
* 모든 팩터리 수신자의 최대 처리 속도 hello hello 프리페치 개수 too20 시간을 설정 합니다. 이렇게 하면 서비스 버스 클라이언트 프로토콜 전송 hello 수가 줄어듭니다.

### <a name="multiple-high-throughput-queues"></a>처리량이 높은 복수 큐
목표: 여러 큐의 전체 처리량을 극대화합니다. 개별 큐의 hello 처리량은 보통 또는 높음입니다.

tooobtain 여러 큐에서 최대 처리량을 hello 설정을 사용 하 여 단일 큐의 toomaximize hello 처리량을 설명합니다. 또한 다른 큐에서 송신 또는 수신 하는 서로 다른 여러 팩터리 toocreate 클라이언트를 사용 합니다.

### <a name="low-latency-queue"></a>대기 시간이 짧은 큐
목표: 큐 또는 토픽의 종단간 대기 시간을 최소화합니다. 발신자와 수신자의 hello 수는 적습니다. hello 큐의 hello 처리량은 낮음 또는 보통입니다.

* 가용성 향상을 위해 분할된 큐를 사용합니다.
* 클라이언트 쪽 일괄 처리를 사용하지 않도록 설정합니다. 클라이언트 hello 메시지를 즉시 보냅니다.
* 일괄 처리된 저장소 액세스를 사용하지 않도록 설정합니다. hello 서비스는 hello 메시지 toohello 저장소를 즉시 씁니다.
* 단일 클라이언트를 사용 하는 경우 hello 프리페치 개수 too20 hello 처리 속도 hello 수신기를 설정 합니다. 동일한 hello hello에는 큐에 여러 메시지가 도착 하는 경우 시간, 서비스 버스 클라이언트 프로토콜 hello hello에 모두 전송 동시 합니다. Hello 클라이언트 hello 다음 메시지를 받으면 해당 메시지 hello 로컬 캐시에 이미입니다. hello 캐시는 작아야 합니다.
* 여러 클라이언트를 사용 하는 경우 프리페치 개수 too0 hello를 설정 합니다. 이 작업을 수행 하 여 hello 두 번째 클라이언트가 첫 번째 클라이언트 hello 아직 hello 첫 번째 메시지를 처리 하는 동안 hello 두 번째 메시지를 받을 수 있습니다.

### <a name="queue-with-a-large-number-of-senders"></a>발신기 수가 많은 큐
목표: 발신기 수가 많은 큐 또는 토픽의 처리량 극대화 각 발신기는 보통 속도의 메시지를 전송합니다. 수신자의 hello 수는 적습니다.

Too1000 동시 연결 tooa 메시징 엔터티를 사용 하면 서비스 버스 (5000 또는 AMQP를 사용 하 여). 이 제한을 hello 네임 스페이스 수준에서 적용 하 고 큐/항목/구독은 네임 스페이스 당 동시 연결 hello 제한으로 제한 됩니다. 큐의 경우 이 숫자는 발신기와 수신기 사이에 공유됩니다. 모든 연결 허용-보낸 사람에 대 한 증명이 hello 큐를 항목 및 단일 구독으로 바꿔야 합니다. 항목은 hello 구독 수신자의 추가 1000 동시 연결을 허용 하는 반면 too1000 발신자의 동시 연결을 허용 합니다. 1000 개 이상 동시 발신자 필요한 경우 보낸 사람 hello 메시지 toohello HTTP 통해 서비스 버스 프로토콜 보내야 합니다.

toomaximize 처리량 다음 hello지 않습니다.

* 성능 및 가용성 향상을 위해 분할된 큐를 사용합니다.
* 각 발신기가 다른 프로세스에 상주하는 경우 프로세스당 하나의 팩터리만 사용합니다.
* 클라이언트 쪽 일괄 처리의 비동기 작업 tootake 장점은 사용 합니다.
* Hello 기본 일괄 처리 간격 20ms tooreduce hello 서비스 버스 클라이언트 프로토콜 전송 수를 사용 합니다.
* 일괄 처리된 저장소 액세스는 사용하도록 설정한 상태로 둡니다. 전반적인 hello 증가 속도는 메시지 hello 큐 또는 항목에 쓸 수 있습니다.
* 모든 팩터리 수신자의 최대 처리 속도 hello hello 프리페치 개수 too20 시간을 설정 합니다. 이렇게 하면 서비스 버스 클라이언트 프로토콜 전송 hello 수가 줄어듭니다.

### <a name="queue-with-a-large-number-of-receivers"></a>수신기 수가 많은 큐
목표: hello 최대화 수신 큐 또는 구독 수신자 수가 많은을 비율입니다. 각 수신자는 보통 속도로 메시지를 받습니다. 보낸 사람 hello 수는 적습니다.

서비스 버스 too1000 동시 연결 tooan 엔터티를 수 있습니다. 큐에 1000 개 이상의 수신기 필요한 hello 큐를 항목 및 여러 구독으로 바꿔야 합니다. 각 구독 too1000 동시 연결을 지원할 수 있습니다. 또한 수신기 hello 큐 hello HTTP 프로토콜을 통해 액세스할 수 있습니다.

toomaximize 처리량 다음 hello지 않습니다.

* 성능 및 가용성 향상을 위해 분할된 큐를 사용합니다.
* 각 수신기가 다른 프로세스에 상주하는 경우 프로세스당 하나의 팩터리만 사용합니다.
* 수신기는 동기 또는 비동기 작업을 사용할 수 있습니다. Hello 보통 지정한 수신 개별 수신자의 속도 때 Complete 요청의 클라이언트 쪽 일괄 처리 수신자 처리량에 영향을 주지 않습니다.
* 일괄 처리된 저장소 액세스는 사용하도록 설정한 상태로 둡니다. 이렇게 하면 hello 줄어듭니다 hello 엔터티의 전체 부하가 합니다. Hello 감소 전체적 비율을 메시지 hello 큐 또는 항목에 쓸 수 있습니다.
* Hello 프리페치 개수 tooa 작은 값을 설정 (예: PrefetchCount = 10). 이렇게 하면 발신기에 많은 수의 메시지가 캐시된 동안 수신기가 유휴 상태가 되지 않습니다.

### <a name="topic-with-a-small-number-of-subscriptions"></a>구독 수가 적은 토픽
목표: 구독 수가 적은 항목의 hello 처리량을 최대화 합니다. 메시지가 hello 결합을 의미 하는 여러 구독에서 수신 되 수신 속도가 모든 구독에 대해 hello 송신 속도 보다 더 높습니다. 보낸 사람 hello 수는 적습니다. 구독 당 수신자 hello 수는 적습니다.

toomaximize 처리량 다음 hello지 않습니다.

* 성능 및 가용성 향상을 위해 분할된 토픽을 사용합니다.
* 전반적인 tooincrease hello hello 항목에 전송 속도, 여러 메시지 팩터리 toocreate 보낸 사람을 사용 합니다. 각 발신기에 대해 비동기 작업이나 여러 스레드를 사용합니다.
* 전반적인 tooincrease hello 구독에서 수신 속도, 여러 메시지 팩터리 toocreate 수신기를 사용 합니다. 각 수신기에 대해 비동기 작업이나 여러 스레드를 사용합니다.
* 클라이언트 쪽 일괄 처리의 비동기 작업 tootake 장점은 사용 합니다.
* Hello 기본 일괄 처리 간격 20ms tooreduce hello 서비스 버스 클라이언트 프로토콜 전송 수를 사용 합니다.
* 일괄 처리된 저장소 액세스는 사용하도록 설정한 상태로 둡니다. 전반적인 hello 증가 속도는 메시지 hello 항목에 쓸 수 있습니다.
* 모든 팩터리 수신자의 최대 처리 속도 hello hello 프리페치 개수 too20 시간을 설정 합니다. 이렇게 하면 서비스 버스 클라이언트 프로토콜 전송 hello 수가 줄어듭니다.

### <a name="topic-with-a-large-number-of-subscriptions"></a>구독 수가 많은 토픽
목표: 구독 수가 많은 항목의 hello 처리량을 최대화 합니다. 메시지가 hello 결합을 의미 하는 여러 구독에서 수신 되 수신 모든 구독에 대해 속도 hello 전송 속도 보다 훨씬 큽니다. 보낸 사람 hello 수는 적습니다. 구독 당 수신자 hello 수는 적습니다.

구독 수가 많은 주제는 일반적으로 모든 메시지는 라우트된 tooall 구독 하는 경우 전반적인 처리량이 낮아집니다를 노출 합니다. 이 hello 팩트 각 메시지를 여러 번 수신 및 저장 동일 항목에 포함 된 모든 메시지와 모든 구독 hello에 저장 됩니다. 발신자 수가 hello 및 구독 당 수신자 수 작습니다 간주 됩니다. 서비스 버스 too2, 항목당 000 구독을 지원합니다.

toomaximize 처리량 다음 hello지 않습니다.

* 성능 및 가용성 향상을 위해 분할된 토픽을 사용합니다.
* 클라이언트 쪽 일괄 처리의 비동기 작업 tootake 장점은 사용 합니다.
* Hello 기본 일괄 처리 간격 20ms tooreduce hello 서비스 버스 클라이언트 프로토콜 전송 수를 사용 합니다.
* 일괄 처리된 저장소 액세스는 사용하도록 설정한 상태로 둡니다. 전반적인 hello 증가 속도는 메시지 hello 항목에 쓸 수 있습니다.
* Hello 프리페치 개수 too20 번 hello 예상 수신 속도 (초)에서으로 설정 합니다. 이렇게 하면 서비스 버스 클라이언트 프로토콜 전송 hello 수가 줄어듭니다.

## <a name="next-steps"></a>다음 단계
서비스 버스 성능 최적화에 대 한 더 toolearn 참조 [메시징 엔터티 분할][Partitioned messaging entities]합니다.

[QueueClient]: /dotnet/api/microsoft.servicebus.messaging.queueclient
[MessageSender]: /dotnet/api/microsoft.servicebus.messaging.messagesender
[MessagingFactory]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory
[PeekLock]: /dotnet/api/microsoft.servicebus.messaging.receivemode
[ReceiveAndDelete]: /dotnet/api/microsoft.servicebus.messaging.receivemode
[BatchFlushInterval]: /dotnet/api/microsoft.servicebus.messaging.netmessagingtransportsettings.batchflushinterval#Microsoft_ServiceBus_Messaging_NetMessagingTransportSettings_BatchFlushInterval
[EnableBatchedOperations]: /dotnet/api/microsoft.servicebus.messaging.queuedescription.enablebatchedoperations#Microsoft_ServiceBus_Messaging_QueueDescription_EnableBatchedOperations
[QueueClient.PrefetchCount]: /dotnet/api/microsoft.servicebus.messaging.queueclient.prefetchcount#Microsoft_ServiceBus_Messaging_QueueClient_PrefetchCount
[SubscriptionClient.PrefetchCount]: /dotnet/api/microsoft.servicebus.messaging.subscriptionclient.prefetchcount#Microsoft_ServiceBus_Messaging_SubscriptionClient_PrefetchCount
[ForcePersistence]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage.forcepersistence#Microsoft_ServiceBus_Messaging_BrokeredMessage_ForcePersistence
[EnablePartitioning]: /dotnet/api/microsoft.servicebus.messaging.queuedescription.enablepartitioning#Microsoft_ServiceBus_Messaging_QueueDescription_EnablePartitioning
[Partitioned messaging entities]: service-bus-partitioning.md
[TopicDescription.EnableFilteringMessagesBeforePublishing]: /dotnet/api/microsoft.servicebus.messaging.topicdescription.enablefilteringmessagesbeforepublishing#Microsoft_ServiceBus_Messaging_TopicDescription_EnableFilteringMessagesBeforePublishing

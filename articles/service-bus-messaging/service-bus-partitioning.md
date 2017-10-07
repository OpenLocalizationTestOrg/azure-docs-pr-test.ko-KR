---
title: "Azure 서비스 버스 큐 및 항목 aaaCreate 분할 | Microsoft Docs"
description: "Toopartition 서비스 버스 큐 및 주제 여러 메시지를 사용 하 여 브로커 방법을 설명 합니다."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a0c7d5a2-4876-42cb-8344-a1fc988746e7
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;hillaryc
ms.openlocfilehash: 6d42556a0714d6a012dc319f662521c8b0bb958b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="partitioned-queues-and-topics"></a>분할 큐 및 항목
여러 메시지 브로커 tooprocess 메시지를 사용 하는 azure 서비스 버스 및 여러 메시징 toostore 메시지를 저장 합니다. 일반적인 큐 또는 항목은 단일 메시지 broker에서 처리되며 하나의 메시징 저장소에 저장됩니다. 서비스 버스 *파티션을* 큐와 항목을 사용 하도록 설정 또는 *메시징 엔터티*, toobe 여러 메시지 브로커 및 메시징 저장소에서 분할 합니다. 이 즉, 분할된 된 엔터티의 전체 처리량을 hello 더 이상 단일 메시지 브로커 또는 메시징 저장소의 hello 성능을 제한 됩니다. 또한 메시징 스토어가 일시적으로 중단된 경우에도 분할된 큐 또는 항목을 계속 렌더링할 수 없습니다. 분할된 큐 및 항목은 트랜잭션 및 세션에 대한 지원 같은 모든 고급 Service Bus 기능을 포함할 수 있습니다.

서비스 버스 내부 구조에 대 한 정보를 참조 hello [서비스 버스 아키텍처] [ Service Bus architecture] 문서.

표준 및 프리미엄 메시징 둘 다의 모든 큐 및 토픽에서 엔티티가 생성될 때 기본적으로 파티션이 사용되도록 설정됩니다. 분할 없이 표준 메시징 계층 엔터티를 만들 수 있지만 프리미엄 네임스페이스의 큐 및 토픽은 항상 분할되므로 이 옵션을 사용하지 않도록 설정할 수 없습니다. 

가능한 toochange hello 없으면 기존 큐 또는 항목 표준 또는 프리미엄 계층의 옵션에 분할을 설정할 수 있습니다 hello 옵션 hello 엔터티를 만들 때.

## <a name="how-it-works"></a>작동 방법

분할된 큐 및 항목 각각은 여러 조각으로 구성됩니다. 각 조각은 다른 메시징 저장소에 저장되고 서로 다른 메시지 broker에서 처리됩니다. 메시지 tooa 분할 된 큐 또는 항목을 보낼 때 서비스 버스 hello 메시지 tooone hello 조각에 할당 합니다. hello 선택 영역 서비스 버스를 통해 임의로 이루어집니다 또는 보낸 사람 hello 파티션 키를 사용 하 여 지정할 수 있습니다.

클라이언트가 tooreceive 분할된 된 큐에서 메시지 또는 서비스 버스 구독 tooa 분할 된 항목에서 메시지에 대 한 모든 조각이 쿼리 하는 경우에 hello 메시징 저장소 toohello 수신기 중 하나에서 가져온 hello 첫 번째 메시지를 반환 합니다. 서비스 버스 캐시는 다른 메시지와 추가 받을 때 해당 요청을 수신 하는 반환 hello 합니다. 수신 클라이언트 hello 분할; 인식 하지 않습니다. hello 분할 된 큐 또는 항목의 클라이언트 측 동작 (예: 읽기, 완료, 지연, 배달 못함, 프리페치)은 일반 엔터티의 동일한 toohello 동작 합니다.

분할된 큐 또는 항목에 메시지를 보내거나 메시지를 받을 때 추가 비용이 없습니다.

## <a name="enable-partitioning"></a>분할 사용

Azure SDK 버전 2.2 이상을 hello를 사용 하거나 지정 toouse 분할 된 큐 및 Azure 서비스 버스 주제 `api-version=2013-10` HTTP 요청에 있습니다.

### <a name="standard"></a>Standard

표준 메시징 계층 hello에에서 서비스 버스 큐 및 항목 (hello 기본값은 1GB) 1, 2, 3, 4 또는 5GB 크기로 만들 수 있습니다. 분할을 사용, 서비스 버스 지정한 각 GB에 대 한 hello 엔터티의 16 복사본 (16 파티션)을 만듭니다. 따라서 크기 5GB 인 큐를 만든 경우 16 개의 파티션이 있는 hello 최대 큐 크기는 (5 \* 16) = 80GB입니다. Hello에 항목을 확인 하 여 hello 분할 된 큐 또는 항목의 최대 크기를 볼 수 있습니다 [Azure 포털][Azure portal], hello에 **개요** 블레이드 해당 엔터티에 대 한 합니다.

### <a name="premium"></a>Premium

프리미엄 계층 네임 스페이스에 1, 2, 3, 4, 5, 10, 20, 40, 또는 80GB 크기 (hello 기본값은 1GB)의 서비스 버스 큐 및 항목을 만들 수 있습니다. 기본적으로 분할이 사용되도록 설정되면 Service Bus는 엔터티마다 두 개의 파티션을 만듭니다. Hello에 항목을 확인 하 여 hello 분할 된 큐 또는 항목의 최대 크기를 볼 수 있습니다 [Azure 포털][Azure portal], hello에 **개요** 블레이드 해당 엔터티에 대 한 합니다.

Hello 프리미엄 메시징 계층에서 분할 하는 방법에 대 한 자세한 내용은 참조 [서비스 버스 고급 도메인 및 표준 메시징 계층](service-bus-premium-messaging.md)합니다. 

### <a name="create-a-partitioned-entity"></a>분할된 엔터티 만들기

여러 가지 방법으로 toocreate 분할된 된 큐 또는 항목 있습니다. 응용 프로그램에서 hello 큐 또는 항목을 만들 때 hello를 각각 설정 하 여 hello 큐 또는 항목에 대 한 분할을 설정할 수 있습니다 [QueueDescription.EnablePartitioning] [ QueueDescription.EnablePartitioning] 또는 [TopicDescription.EnablePartitioning] [ TopicDescription.EnablePartitioning] 속성 너무**true**합니다. Hello hello 큐 시간에서 이러한 속성을 설정 해야 합니다 또는 항목이 만들어질 합니다. 앞에서 설명한 것 처럼 불가능 toochange에 대해 이러한 속성의 기존 큐 또는 항목. 예:

```csharp
// Create partitioned topic
NamespaceManager ns = NamespaceManager.CreateFromConnectionString(myConnectionString);
TopicDescription td = new TopicDescription(TopicName);
td.EnablePartitioning = true;
ns.CreateTopic(td);
```

Hello에 분할 된 큐 또는 항목을 만들 수 또는 [Azure 포털] [ Azure portal] 또는 Visual Studio에서. Hello 포털에서 큐 또는 항목을 만들 때 hello **분할을 사용 하도록 설정** hello 큐 또는 항목에서 옵션 **만들기** 블레이드는 기본적으로 선택 됩니다. 표준 계층 엔터티에;이 옵션을 해제할만 수 있습니다. hello에서 Premium 계층 분할은 항상 설정 됩니다. Visual Studio에서 클릭 hello **분할 사용** hello 확인란을 선택 **새 큐** 또는 **새 주제** 대화 상자.

## <a name="use-of-partition-keys"></a>파티션 키의 사용
메시지가 분할 된 큐 또는 항목에 넣을 때 서비스 버스 hello는 파티션 키가 있는지 확인 합니다. 를 찾은 경우 해당 키에 따라 hello 조각을 선택 합니다. 파티션 키를 찾지 못하면 경우 내부 알고리즘에 따라 hello 조각을 선택 합니다.

### <a name="using-a-partition-key"></a>파티션 키 사용
세션 또는 트랜잭션과 같은 일부 시나리오를 특정 조각에 저장 된 메시지 toobe가 필요 합니다. 이러한 모든 시나리오에는 파티션 키 hello 사용을 해야합니다. 사용 하 여 hello 동일한 파티션 키에 할당 된 모든 메시지 조각 toohello 동일 합니다. 서비스 버스 hello 조각을 일시적으로 사용할 수 없는 경우 오류가 발생 합니다.

Hello 시나리오에 따라 서로 다른 메시지 속성이 파티션 키로 사용 됩니다.

**SessionId**: 메시지의 hello [BrokeredMessage.SessionId] [ BrokeredMessage.SessionId] 속성을 설정한 후 서비스 버스 hello 파티션 키로이 속성을 사용 합니다. 이러한 방식으로, toohello 속해 있는 모든 메시지가 동일한 세션에서 처리 hello 동일한 메시지 브로커 합니다. 따라서 서비스 버스 tooguarantee 메시지를 hello 세션 상태의 일관성을 뿐만 아니라 주문 수 있습니다.

**PartitionKey**: 메시지의 hello [BrokeredMessage.PartitionKey] [ BrokeredMessage.PartitionKey] 속성 하지만 하지 hello [BrokeredMessage.SessionId] [ BrokeredMessage.SessionId] 속성을 설정한 후 서비스 버스 hello를 사용 하 여 [PartitionKey] [ PartitionKey] hello 파티션 키로 속성입니다. Hello 메시지에 두 hello [SessionId] [ SessionId] 및 hello [PartitionKey] [ PartitionKey] 속성 집합을 두 속성이 동일 해야 합니다. 경우 hello [PartitionKey] [ PartitionKey] 속성 hello 보다 tooa 서로 다른 값으로 설정 되어 [SessionId] [ SessionId] 속성, 서비스 버스에 잘못 된 반환 작업 예외입니다. hello [PartitionKey] [ PartitionKey] 비 세션 인식 트랜잭션 메시지를 보내는 경우 속성을 사용 해야 합니다. hello 파티션 키를 트랜잭션 내에서 보낸 모든 메시지는 처리 되도록 hello에서 동일한 메시지 브로커 합니다.

**MessageId**: hello 큐 또는 항목에 hello [QueueDescription.RequiresDuplicateDetection] [ QueueDescription.RequiresDuplicateDetection] 속성이 너무 설정**true** 및 hello [BrokeredMessage.SessionId] [ BrokeredMessage.SessionId] 또는 [BrokeredMessage.PartitionKey] [ BrokeredMessage.PartitionKey] 속성을 설정 하지 않은 다음 hello[BrokeredMessage.MessageId] [ BrokeredMessage.MessageId] hello 파티션 키로 사용 합니다. (Hello Microsoft.NET 및 AMQP 라이브러리 hello 보내는 응용 프로그램, 없는 경우 자동으로 메시지 ID를 할당 하 note). 이 경우 동일한 메시지에 의해 처리 됩니다 hello의 모든 복사본이 동일한 메시지 브로커를 hello 합니다. 서비스 버스 toodetect 있으며 중복 된 메시지를 제거 합니다. 경우 hello [QueueDescription.RequiresDuplicateDetection] [ QueueDescription.RequiresDuplicateDetection] 속성이 너무 설정 되지 않은**true**, 서비스 버스 hello를 고려 하지 않습니다 [MessageId] [ MessageId] 파티션 키로 속성입니다.

### <a name="not-using-a-partition-key"></a>파티션 키 사용하지 않음
파티션 키 hello 없는 경우, 서비스 버스 hello 분할 된 큐 또는 항목의 라운드 로빈 방식으로 tooall hello 조각에 메시지를 배포합니다. Hello 선택한 조각을 사용할 수 없는 경우 서비스 버스 hello 메시지 tooa 다른 조각에 할당 합니다. 이러한 방식으로 hello 보내기 작업은 메시징 저장소의 hello 일시적인 장애가 불구 하 고 성공합니다. 그러나 보장 된 순서는 파티션 키를 제공 하는 hello를 얻지 못합니다.

가용성 (파티션 키)과 일관성 (파티션 키 사용) 간의 hello 관계의 한 심도 있는 논의 알려면 [이 여기서](../event-hubs/event-hubs-availability-and-consistency.md)합니다. 이 정보는 toopartitioned 서비스 버스 엔터티 및 이벤트 허브 파티션에 균등 하 게 적용합니다.

toogive 서비스 버스 충분 한 시간 tooenqueue hello 메시지를 다른 조각에 hello [MessagingFactorySettings.OperationTimeout] [ MessagingFactorySettings.OperationTimeout] hello 클라이언트 hello 메시지를 전송 하 여 지정 된 값 15 초 보다 커야 합니다. Hello를 설정 하는 것이 좋습니다. [OperationTimeout] [ OperationTimeout] 속성 toohello 기본값인 60 초입니다.

파티션 키 "고정" 메시지 tooa 특정 조각 참고 합니다. 이 조각이 저장 된 hello 메시징 저장소를 사용할 수 없는 경우 서비스 버스 오류가 반환 됩니다. 파티션 키 hello 없는 경우, 서비스 버스를 다른 조각에 선택할 수 있으며 hello 작업이 성공 합니다. 그러므로 필요한 경우가 아니면 파티션 키를 제공하지 않는 것이 좋습니다.

## <a name="advanced-topics-use-transactions-with-partitioned-entities"></a>고급 항목: 분할된 엔터티로 트랜잭션 사용
트랜잭션의 일부로 전송되는 메시지는 파티션 키를 지정해야 합니다. Hello 다음과 같은 속성 중 하나일 수 있습니다이: [BrokeredMessage.SessionId][BrokeredMessage.SessionId], [BrokeredMessage.PartitionKey][BrokeredMessage.PartitionKey], 또는 [ BrokeredMessage.MessageId][BrokeredMessage.MessageId]합니다. 동일한 트랜잭션을 지정 해야 하는 hello의 일부로 보내지는 모든 메시지 hello 동일한 파티션 키입니다. 트랜잭션 내에서 파티션 키 없이 메시지 toosend 시도 하면 서비스 버스 잘못 된 작업 예외를 반환 합니다. 파티션 키, 서비스 버스 toosend 내에서 여러 메시지 hello 다른 동일한 트랜잭션을 사용 하려는 경우 잘못 된 작업 예외를 반환 합니다. 예:

```csharp
CommittableTransaction committableTransaction = new CommittableTransaction();
using (TransactionScope ts = new TransactionScope(committableTransaction))
{
    BrokeredMessage msg = new BrokeredMessage("This is a message");
    msg.PartitionKey = "myPartitionKey";
    messageSender.Send(msg); 
    ts.Complete();
}
committableTransaction.Commit();
```

파티션 키로 사용 되는 hello 속성을 설정 하는 경우 서비스 버스 핀 hello 메시지 tooa 특정 조각입니다. 이 동작은 트랜잭션이 사용되는지 여부와 상관 없이 발생합니다. 필요하지 않은 경우 파티션 키를 지정하지 않는 것이 좋습니다.

## <a name="using-sessions-with-partitioned-entities"></a>분할된 엔터티로 세션 사용
hello 메시지 hello toosend 트랜잭션 메시지 tooa 세션 인식 항목 또는 큐 있어야 [BrokeredMessage.SessionId] [ BrokeredMessage.SessionId] 속성 집합입니다. 경우 hello [BrokeredMessage.PartitionKey] [ BrokeredMessage.PartitionKey] 속성 속성도 지정 된, 동일한 toohello 해야 [SessionId] [ SessionId] 속성입니다. 다른 경우 Service Bus가 잘못된 작업 예외를 반환합니다.

일반 (분할 되지 않은) 큐 또는 항목과 달리 아닙니다 가능한 toouse 단일 트랜잭션으로 toosend 여러 메시지 toodifferent 세션. 시도할 경우 Service Bus가 잘못된 작업 예외를 반환합니다. 예:

```csharp
CommittableTransaction committableTransaction = new CommittableTransaction();
using (TransactionScope ts = new TransactionScope(committableTransaction))
{
    BrokeredMessage msg = new BrokeredMessage("This is a message");
    msg.SessionId = "mySession";
    messageSender.Send(msg); 
    ts.Complete();
}
committableTransaction.Commit();
```

## <a name="automatic-message-forwarding-with-partitioned-entities"></a>분할된 엔터티로 자동 메시지 전달
Service Bus는 분할된 엔터티 간에 자동 메시지 전달을 지원합니다. tooenable 자동 메시지 전달, 설정 hello [QueueDescription.ForwardTo] [ QueueDescription.ForwardTo] hello 소스 큐 또는 구독에는 속성입니다. Hello 메시지 파티션 키를 지정 하는 경우 ([SessionId][SessionId], [PartitionKey][PartitionKey], 또는 [MessageId] [ MessageId]), hello 대상 엔터티의 해당 파티션 키 사용 됩니다.

## <a name="considerations-and-guidelines"></a>고려 사항 및 지침
* **높은 일관성 기능**: 세션, 중복 감지 또는 분할 키를 명시적으로 제어할 등의 기능을 사용 하 여 엔터티의 경우 hello 메시징 작업은 항상 라우트된 toospecific 조각입니다. Hello 내부 저장소 손상 되었습니다. 트래픽이 많은 hello 조각 중 하나라도 발생할 경우 이러한 작업이 실패 하 고 가용성 감소 됩니다. Hello 일관성은 분할 되지 않은 엔터티; 보다 훨씬 여전히 더 전반적으로, 트래픽의 하위 집합만 것과 반대로 tooall hello 트래픽, 문제가 발생 합니다. 자세한 내용은 이 [가용성 및 일관성 논의](../event-hubs/event-hubs-availability-and-consistency.md)를 참조하세요.
* **관리**: hello 엔터티의 모든 hello 조각에서 Create, Update 및 Delete 등의 작업을 수행 해야 합니다. 어떤 부분이라도 손상되면 이러한 작업이 실패할 수 있습니다. Hello 가져오기 작업에 대 한 정보 메시지 수와 같은 집계 해야 모든 조각의 합니다. 된 조각 상태가 정상이 아닌 경우 제한으로 hello 엔터티 가용성 상태가 보고 됩니다.
* **볼륨 메시지 시나리오 낮은**: 이러한 시나리오, 특히 hello HTTP 프로토콜을 사용 하는 경우, tooperform 할 수 있습니다 여러 개의 받기 작업 순서 tooobtain 모든 hello 메시지입니다. 수신 요청에 대 한 hello 프런트 엔드 hello 조각이 모두에 대해 receive를 수행 하 고 받은 모든 hello 응답을 캐시 합니다. 같은 연결 것이 캐싱은 구현할 수 있으며 수신 대기 하는 hello에 후속 수신 요청이 되지 것입니다. 그러나 연결이 여러 개 있거나 HTTP를 사용하는 경우 각 요청에 대해 새 연결이 설정됩니다. 따라서 보장이 없습니다 hello에 도착 합니다는 동일한 노드. 모든 기존 메시지 잠금이 설정 되 고 hello 다른 프런트 엔드에 캐시 하는 경우 수신 작업 반환 **null**합니다. 결과적으로 메시지가 만료되고 다시 받을 수 있습니다. HTTP 연결 유지를 사용하는 것이 좋습니다.
* **메시지 찾아보기/Peek**: [PeekBatch](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_PeekBatch_System_Int32_) 항상 hello hello에 지정 된 메시지 수를 반환 하지 않는 [MessageCount](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_MessageCount) 속성입니다. 그 이유에는 일반적으로 다음 두 가지가 있습니다. 한 가지 이유는 해당 hello 메시지의 hello 컬렉션의 집계 크기는 256kb hello 최대 크기를 초과 합니다. 또 다른 이유 하는 경우는 hello 큐 또는 항목에 hello [EnablePartitioning 속성](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_EnablePartitioning) 도**true**, 파티션을 충분 한 메시지를 사용할 수 없습니다 toocomplete hello 요청 메시지의 수입니다. 일반적으로 응용 프로그램가 tooreceive 특정 개수의 메시지를 호출 해야 [PeekBatch](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_PeekBatch_System_Int32_) 반복 해 서 때까지 해당 개수의 메시지를 가져와서 자세한 메시지 toopeek 없습니다. 코드 샘플을 비롯한 자세한 내용은 [QueueClient.PeekBatch](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_PeekBatch_System_Int32_) 또는 [SubscriptionClient.PeekBatch](/dotnet/api/microsoft.servicebus.messaging.subscriptionclient#Microsoft_ServiceBus_Messaging_SubscriptionClient_PeekBatch_System_Int32_)를 참조하세요.

## <a name="latest-added-features"></a>최근에 추가된 기능
* 이제 분할된 엔터티에 대해 규칙 추가 또는 제거가 지원됩니다. 분할되지 않은 엔터티와 달리, 트랜잭션에서 이러한 작업은 지원되지 않습니다. 
* 분할 된 엔터티에서 tooand 메시지 송수신에 대해 AMQP 이제 지원 됩니다.
* AMQP hello 작업 다음에 지원 됩니다: [일괄 처리 보내기](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_SendBatch_System_Collections_Generic_IEnumerable_Microsoft_ServiceBus_Messaging_BrokeredMessage__), [일괄 수신](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_ReceiveBatch_System_Int32_), [시퀀스 번호로 받기](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_Receive_System_Int64_), [피킹](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_Peek), [ 잠금을 갱신](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_RenewMessageLock_System_Guid_), [메시지 예약](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_ScheduleMessageAsync_Microsoft_ServiceBus_Messaging_BrokeredMessage_System_DateTimeOffset_), [취소 예약 된 메시지](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_CancelScheduledMessageAsync_System_Int64_), [규칙 추가](/dotnet/api/microsoft.servicebus.messaging.ruledescription), [규칙 제거](/dotnet/api/microsoft.servicebus.messaging.ruledescription), [세션 잠금 갱신](/dotnet/api/microsoft.servicebus.messaging.messagesession#Microsoft_ServiceBus_Messaging_MessageSession_RenewLock), [세션 상태 설정](/dotnet/api/microsoft.servicebus.messaging.messagesession#Microsoft_ServiceBus_Messaging_MessageSession_SetState_System_IO_Stream_), [Get 세션 상태](/dotnet/api/microsoft.servicebus.messaging.messagesession#Microsoft_ServiceBus_Messaging_MessageSession_GetState), 및 [세션 열거](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_GetMessageSessionsAsync)합니다.

## <a name="partitioned-entities-limitations"></a>분할된 엔터티 제한 사항
현재 Service Bus에 분할 된 큐 및 항목에 다음과 같은 제한을 hello를 설정 합니다.

* 분할 된 큐 및 항목 toodifferent 속한 메시지를 보내는 지원 하지 않는 단일 트랜잭션 내에서 세션입니다.
* 서비스 버스는 현재 too100 분할 된 큐 또는 항목 네임 스페이스 당를 허용합니다. 각 분할 된 큐 또는 항목 (tooPremium 계층을 적용 되지 않음) 네임 스페이스 당 10, 000 엔터티 hello 할당량에 합산 됩니다.

## <a name="next-steps"></a>다음 단계
Hello 설명은 참조 [AMQP 1.0 지원에 대 한 서비스 버스 큐 및 항목 분할] [ AMQP 1.0 support for Service Bus partitioned queues and topics] toolearn 메시징 엔터티 분할 하는 방법에 대 한 자세한 합니다. 

[Service Bus architecture]: service-bus-architecture.md
[Azure portal]: https://portal.azure.com
[QueueDescription.EnablePartitioning]: /dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_EnablePartitioning
[TopicDescription.EnablePartitioning]: /dotnet/api/microsoft.servicebus.messaging.topicdescription#Microsoft_ServiceBus_Messaging_TopicDescription_EnablePartitioning
[BrokeredMessage.SessionId]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_SessionId
[BrokeredMessage.PartitionKey]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_PartitionKey
[SessionId]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_SessionId
[PartitionKey]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_PartitionKey
[QueueDescription.RequiresDuplicateDetection]: /dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_RequiresDuplicateDetection
[BrokeredMessage.MessageId]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId
[MessageId]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId
[MessagingFactorySettings.OperationTimeout]: /dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings#Microsoft_ServiceBus_Messaging_MessagingFactorySettings_OperationTimeout
[OperationTimeout]: /dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings#Microsoft_ServiceBus_Messaging_MessagingFactorySettings_OperationTimeout
[QueueDescription.ForwardTo]: /dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_ForwardTo
[AMQP 1.0 support for Service Bus partitioned queues and topics]: service-bus-partitioned-queues-and-topics-amqp-overview.md

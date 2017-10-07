---
title: "aaaService 버스 배달 못 한 편지 큐 | Microsoft Docs"
description: "Azure 서비스 버스 배달 못 한 편지 큐의 개요"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 68b2aa38-dba7-491a-9c26-0289bc15d397
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/17/2017
ms.author: clemensv;sethm
ms.openlocfilehash: 1638272085b8a3a59e8814f6f943caee35a2bfdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-service-bus-dead-letter-queues"></a>서비스 버스 배달 못 한 편지 큐의 개요

Service Bus 큐 및 토픽 구독은 *배달 못 한 편지 큐*(DLQ)라고 하는 보조 하위 큐를 제공합니다. hello 배달 못 한 편지 큐 toobe 명시적으로 생성 하지 않아도 및 삭제 하거나 관리 되는 독립 hello 주 엔터티의 수 없습니다.

이 문서에서는 Azure Service Bus에서 배달하지 못한 편지 큐에 대해 설명합니다. Hello에서 대부분의 hello 토론을 확인할 [배달 못 한 편지 큐 샘플](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/DeadletterQueue) GitHub에서 합니다.
 
## <a name="hello-dead-letter-queue"></a>hello 배달 못 한 편지 큐

hello hello 배달 못 한 편지 큐의 목적은 tooany 수신기 배달할 수 없는 toohold 메시지 또는 메시지를 처리할 수 없습니다. 다음 메시지는 hello dlq가에서 제거 되며, 검사할 수 있습니다. 응용 프로그램 수, 사용 하 여 연산자를 문제를 수정 및 hello 메시지 다시 전송, 로그 hello 팩트 오류가 발생 했습니다 수정 작업을 수행 합니다. 

프로토콜 및 API의 관점에서 dlq가 hello는 비슷한 tooany 주로 다른 큐 메시지 hello 부모 엔터티의 hello 배달 못 한 편지 제스처를 통해 제출할 수 있습니다. 뿐만 아니라 활성 시간이 관찰되지 않으며, DLQ의 메시지를 배달 못 한 편지로 처리할 수 없습니다. hello 배달 못 한 편지 큐는 배달 미리 보기-잠금 및 트랜잭션 작업에 완벽 하 게 지원 합니다.

자동 정리 작업의 hello dlq가 있다는 것을 참고 합니다. 메시지에에서 계속 남아 hello dlq가 dlq가 hello와 호출에서 명시적으로 검색할 [complete ()](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_CompleteAsync) hello 배달 못 한 메시지에 있습니다.

## <a name="moving-messages-toohello-dlq"></a>Toohello dlq가 메시지 이동

서비스 버스에서 메시지 tooget hello 메시징 엔진 자체 내에서 dlq가 toohello 푸시되는 몇 가지 활동 있습니다. 응용 프로그램 메시지 toohello dlq가 명시적으로 이동할 수 있습니다. 

Hello 브로커에 의해 hello 메시지가 이동, 두 개의 속성이 추가 됩니다 toohello 메시지 hello broker hello의 내부 버전을 호출 하므로 [배달 못한 편지](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_DeadLetter_System_String_System_String_) hello 메시지에 대 한 메서드: `DeadLetterReason` 및 `DeadLetterErrorDescription`합니다.

응용 프로그램 hello에 대 한 고유 코드를 정의할 수 `DeadLetterReason` 속성이 아니라 hello 시스템 집합 hello 다음 값입니다.

| 조건 | DeadLetterReason | DeadLetterErrorDescription |
| --- | --- | --- |
| 항상 |HeaderSizeExceeded |이 스트림에 대 한 hello 크기 할당량 초과 했습니다. |
| !TopicDescription.<br />EnableFilteringMessagesBeforePublishing and SubscriptionDescription.<br />EnableDeadLetteringOnFilterEvaluationExceptions |exception.GetType().Name |exception.Message |
| EnableDeadLetteringOnMessageExpiration |TTLExpiredException |hello 메시지 만료 되어 배달 못 한 편지로 처리 했습니다. |
| SubscriptionDescription.RequiresSession |세션 ID가 null입니다. |세션이 활성화된 엔터티가 세션 식별자가 null인 메시지를 허용하지 않습니다. |
| !dead letter queue |MaxTransferHopCountExceeded |Null |
| 응용 프로그램에서 명시적으로 배달 못 한 편지로 처리 |응용 프로그램에서 지정 |응용 프로그램에서 지정 |

## <a name="exceeding-maxdeliverycount"></a>Exceeding MaxDeliveryCount
큐 및 구독에는 각가 [QueueDescription.MaxDeliveryCount](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_MaxDeliveryCount) 및 [SubscriptionDescription.MaxDeliveryCount](/dotnet/api/microsoft.servicebus.messaging.subscriptiondescription#Microsoft_ServiceBus_Messaging_SubscriptionDescription_MaxDeliveryCount) 속성 기본값은 10 각각; hello 합니다. 잠금이 있는 메시지를 전달한 때마다 ([ReceiveMode.PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode))에 하지만 하거나 명시적으로 중단 또는 hello 잠금이 만료 된 hello 메시지 [BrokeredMessage.DeliveryCount](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_DeliveryCount) 은 증가합니다. 때 [DeliveryCount](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_DeliveryCount) 초과 [MaxDeliveryCount](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_MaxDeliveryCount), hello 메시지는 이동된 toohello hello 지정 dlq가 `MaxDeliveryCountExceeded` 이유 코드입니다.

이 동작을 사용할 수 있지만 설정할 수 있습니다 [MaxDeliveryCount](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_MaxDeliveryCount) tooa 매우 많은 수 있습니다.

## <a name="exceeding-timetolive"></a>TimeToLive 초과
Hello 때 [QueueDescription.EnableDeadLetteringOnMessageExpiration](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_EnableDeadLetteringOnMessageExpiration) 또는 [SubscriptionDescription.EnableDeadLetteringOnMessageExpiration](/dotnet/api/microsoft.servicebus.messaging.subscriptiondescription#Microsoft_ServiceBus_Messaging_SubscriptionDescription_EnableDeadLetteringOnMessageExpiration) 너무 속성이**true** (hello 기본값은 **false**)을 만료 하는 모든 메시지는 이동된 toohello hello 지정 dlq가 `TTLExpiredException` 이유 코드입니다.

만료 된 메시지에만 제거 됩니다 및 당겨 hello 주 큐 또는 구독;에 하나 이상의 활성 수신기 경우 toohello dlq가 따라서 이동 note 해당 동작은 의도 된 것입니다.

## <a name="errors-while-processing-subscription-rules"></a>구독 규칙을 처리하는 동안 오류 발생
Hello 때 [SubscriptionDescription.EnableDeadLetteringOnFilterEvaluationExceptions](/dotnet/api/microsoft.servicebus.messaging.subscriptiondescription#Microsoft_ServiceBus_Messaging_SubscriptionDescription_EnableDeadLetteringOnFilterEvaluationExceptions) 구독에 대 한 속성이 사용 되는지, 구독의 SQL 필터 규칙이 실행 되는 동안 발생 하는 오류 dlq가 hello에 캡처됩니다. 함께 메시지를 잘못 된 번호입니다.

## <a name="application-level-dead-lettering"></a>응용 프로그램 수준에서 배달 못 한 편지 처리
또한 toohello 시스템 제공 배달 못 한 편지 처리 기능을 응용 프로그램 hello dlq가 tooexplicitly 거부 허용 되지 않는 메시지를 사용할 수 있습니다. 이 시스템 문제, 잘못 된 형식의 페이로드를 포함 하는 메시지 또는 일부 메시지 수준 보안 체계를 사용 하는 경우 인증에 실패 하는 메시지의 tooany 정렬 인해 제대로 처리할 수 없는 메시지를 포함할 수 있습니다.

## <a name="dead-lettering-in-forwardto-or-sendvia-scenarios"></a>ForwardTo 또는 SendVia 시나리오의 배달 못한 편지

메시지를 보낸된 toohello 전송 배달 못 한 편지 큐 hello 다음 조건에서 됩니다.

- 메시지는 [함께 체인으로 연결된](service-bus-auto-forwarding.md) 3개 이상의 큐 또는 항목을 통과합니다.
- hello 대상 큐 또는 항목 사용 하지 않도록 설정 되었거나 삭제 됩니다.
- hello 대상 큐 또는 항목 hello 최대 엔터티 크기를 초과합니다.

tooretrieve 이러한 배달 못 한 편지로 처리 메시지를 hello를 사용 하 여 수신기를 만들 수 있습니다 [FormatTransferDeadletterPath](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_FormatTransferDeadLetterPath_System_String_) 유틸리티 메서드.

## <a name="example"></a>예제
다음 코드 조각 hello 메시지 수신기를 만듭니다. Hello hello 기본 큐에 대 한 루프를 수신, hello 코드 hello 메시지를 검색 하 고 [Receive(TimeSpan.Zero)](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_Receive_System_TimeSpan_)를 원활 하 게 사용 되는 모든 메시지 반환 hello 브로커 tooinstantly 묻는 또는 tooreturn 없는 결과 함께 합니다. Hello 코드는 메시지를 받을 경우 즉시 찾는 취소, hello 증가 `DeliveryCount`합니다. Hello 주 큐는 비어 있으며으로 루프 종료 되거나, hello hello 시스템은 hello 메시지 toohello dlq가 이동 되 면 [ReceiveAsync](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_ReceiveAsync_System_TimeSpan_) 반환 **null**합니다.

```csharp
var receiver = await receiverFactory.CreateMessageReceiverAsync(queueName, ReceiveMode.PeekLock);
while(true)
{
    var msg = await receiver.ReceiveAsync(TimeSpan.Zero);
    if (msg != null)
    {
        Console.WriteLine("Picked up message; DeliveryCount {0}", msg.DeliveryCount);
        await msg.AbandonAsync();
    }
    else
    {
        break;
    }
}
```

## <a name="next-steps"></a>다음 단계
서비스 버스 큐에 대 한 자세한 내용은 문서 다음 hello 참조:

* [Service Bus 큐 시작](service-bus-dotnet-get-started-with-queues.md)
* [Azure 큐와 Service Bus 큐 비교](service-bus-azure-and-service-bus-queues-compared-contrasted.md)


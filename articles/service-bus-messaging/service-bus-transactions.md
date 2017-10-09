---
title: "Azure 서비스 버스에서 트랜잭션 처리의 aaaOverview | Microsoft Docs"
description: "Azure 서비스 버스 원자성 트랜잭션 및 send via에 대한 개요"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 64449247-1026-44ba-b15a-9610f9385ed8
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/17/2017
ms.author: clemensv;sethm
ms.openlocfilehash: 5ed4d1fd3a089b8ebcd69a568f4ac863e753aecd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-service-bus-transaction-processing"></a>서비스 버스 트랜잭션 처리의 개요
이 문서에서는 Azure 서비스 버스의 hello 트랜잭션 기능을 설명 합니다. Hello에서 대부분의 hello 토론을 확인할 [서비스 버스 예제와 함께 원자성 트랜잭션을](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions)합니다. 이 문서는 트랜잭션 처리 및 hello 제한 tooan 개요 *통해 보낼* hello 원자성 트랜잭션을 샘플 값이 범위에 광범위 한 고 더 복잡 한 서비스 버스의 기능입니다.

## <a name="transactions-in-service-bus"></a>서비스 버스의 트랜잭션
[트랜잭션](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions#what-are-transactions)은 두 개 이상의 작업을 *실행 범위*로 그룹화합니다. 기본적으로 이러한 트랜잭션 tooa 작업 그룹에 속한 모든 작업에 성공 또는 실패할 공동 있는지 확인 해야 합니다. 이 트랜잭션을 참조 tooas 자주 변경 되는 한 단위로 동작 *원자성*합니다. 

서비스 버스는 트랜잭션 메시지 broker이며 메시지 저장소에 대한 모든 내부 작업의 트랜잭션 무결성을 보장합니다. 이동 메시지 tooa 같은 내부 서비스 버스에서 메시지의 모든 전송을 [배달 못 한 편지 큐](service-bus-dead-letter-queues.md) 또는 [자동 전달](service-bus-auto-forwarding.md) 엔터티 간의 메시지는 트랜잭션. 따라서 서비스 버스에서 메시지를 수락할 경우 이미 저장되어 시퀀스 번호가 레이블로 지정되었습니다. 이제부터 서비스 버스 내에서 모든 메시지 전달이 조정된 작업이 엔터티에서을 둘 다를 일으킵니다 tooloss (소스 성공 및 실패 대상) 또는 tooduplication (실패 하는 원본 및 대상 성공) hello 메시지의 합니다.

서비스 버스는 트랜잭션의 단일 메시징 엔터티 (큐, 항목, 구독) hello 범위 내에 대 한 그룹화 작업을 지원합니다. 예를 들어 트랜잭션 범위 내에서 여러 메시지 tooone 큐를 보낼 수 있습니다 및 hello 트랜잭션이 성공적으로 완료 되 면 hello 메시지를 커밋할된 toohello 큐의 로그 수만 있습니다.

## <a name="operations-within-a-transaction-scope"></a>트랜잭션 범위 내 작업
트랜잭션 범위 내에서 수행할 수 있는 hello 작업은 다음과 같습니다.

* **[QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient), [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender), [TopicClient](/dotnet/api/microsoft.servicebus.messaging.topicclient)**: Send, SendAsync, SendBatch, SendBatchAsync 
* **[BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)**: Complete, CompleteAsync, Abandon, AbandonAsync, Deadletter, DeadletterAsync, Defer, DeferAsync, RenewLock, RenewLockAsync 

수신 hello 응용 프로그램 hello를 사용 하 여 메시지를 획득 하 가정 하기 때문에 작업이 포함 되지 않습니다 [ReceiveMode.PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode) 몇몇 내부 모드에서는 수신 루프 또는 [OnMessage](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_OnMessage_System_Action_Microsoft_ServiceBus_Messaging_BrokeredMessage__Microsoft_ServiceBus_Messaging_OnMessageOptions_) 콜백을 및 다음 트랜잭션이 열리고 hello 메시지 처리에 대 한 범위입니다.

hello (완료, 중단, 배달 못 한 편지, 연기) hello 메시지의 처리 방식을 다음 내에서 발생 하 고에 의존 하는 hello 범위를 hello hello 트랜잭션의 전반적인 결과입니다.

## <a name="transfers-and-send-via"></a>전송 및 "send via"
tooenable 큐 tooa 프로세서와 다음 tooanother 큐에서 데이터의 트랜잭션 인계, Service Bus 지원 *전송*합니다. 전송 작업을 사용 하는 처음 보내는 메시지 tooa "전송 큐"와 hello 전송 큐는 hello 메시지 toohello 강력한 동일한 전송 구현 hello 자동 전달 기능을 사용 하는 hello를 사용 하 여 대상 큐를 위한 것 바로 이동 켜 집니다. hello 메시지는 표시 될 hello 전송 큐의 소비자에 대 한 방식으로 커밋된 toohello 전송 큐의 로그는 되지 않습니다.

hello 전송 큐 자체 원본인 hello hello 보낸 사람의 입력된 메시지의 경우이 트랜잭션 기능은 hello 전원이 드러납니다. 즉, 서비스 버스를 전송할 수 hello 메시지 toohello 대상 큐 "via" hello 전송 큐 전체를 수행 하는 동안 (또는 지연 시킬 또는 배달 못 한 편지)에서 하나의 원자성 작업 hello 입력된 메시지에 대 한 작업이 있습니다. 

### <a name="see-it-in-code"></a>실제 코드 엿보기
이러한을 tooset, hello 전송 큐를 통해 hello 대상 큐를 대상으로 하는 메시지 보낸 사람을 만들어야 합니다. 또한, 같은 큐에서 메시지를 풀링하는 수신기가 있을 수도 있습니다. 예:

```csharp
var sender = this.messagingFactory.CreateMessageSender(destinationQueue, myQueueName);
var receiver = this.messagingFactory.CreateMessageReceiver(myQueueName);
```

그런 다음 간단한 트랜잭션 hello 다음 예제와 같이 이러한 요소를 사용 합니다.

```csharp
var msg = receiver.Receive();

using (scope = new TransactionScope())
{
    // Do whatever work is required 

    var newmsg = ... // package hello result 

    msg.Complete(); // mark hello message as done
    sender.Send(newmsg); // forward hello result

    scope.Complete(); // declare hello transaction done
} 
```

## <a name="next-steps"></a>다음 단계

서비스 버스 큐에 대 한 자세한 내용은 문서 다음 hello 참조:

* [자동 전달을 사용한 Service Bus 엔터티 연결](service-bus-auto-forwarding.md)
* [자동 전달 샘플](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AutoForward)
* [Service Bus 샘플과 함께 원자성 트랜잭션](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions)
* [Azure 큐와 Service Bus 큐 비교](service-bus-azure-and-service-bus-queues-compared-contrasted.md)
* [어떻게 toouse 서비스 버스 큐](service-bus-dotnet-get-started-with-queues.md)


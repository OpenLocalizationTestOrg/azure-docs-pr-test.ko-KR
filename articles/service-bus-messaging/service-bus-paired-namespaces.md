---
title: "aaaAzure 서비스 버스 네임 스페이스 쌍이 | Microsoft Docs"
description: "쌍을 이루는 네임스페이스 구현의 세부 사항 및 비용"
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 2440c8d3-ed2e-47e0-93cf-ab7fbb855d2e
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: sethm
ms.openlocfilehash: 4c44b2b95d2228e1ad8075b52634d88a1593d3b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="paired-namespace-implementation-details-and-cost-implications"></a>쌍을 이루는 네임스페이스 구현의 세부 사항 및 비용의 영향
hello [PairNamespaceAsync] [ PairNamespaceAsync] 메서드를 사용 하는 [SendAvailabilityPairedNamespaceOptions] [ SendAvailabilityPairedNamespaceOptions] 인스턴스를 표시 하는 작업을 수행 사용자 대신 합니다. Hello 기능을 사용할 때 고려 사항 비용이 며, 되므로 유용 toounderstand 작업 수행 되는 경우 hello 동작을 예상할 수 있도록 합니다. hello API에서 사용자 대신 자동 동작을 수행 하는 hello 맞물릴 때:

* 백로그 큐를 만듭니다.
* 만들기는 [MessageSender] [ MessageSender] tooqueues 또는 항목을 설명 하는 개체입니다.
* 메시징 엔터티를 사용할 수 없을 때 ping 경우 메시지를 전송 toohello 엔터티 시도 toodetect에서 해당 엔터티를 다시 사용할 수 있습니다.
* "메시지 펌프" 집합의 메시지에서 이동 hello 백로그 큐 toohello 기본 큐를 만듭니다 필요에 따라.
* 기본 및 보조 hello 닫기/오류 조정 [MessagingFactory] [ MessagingFactory] 인스턴스.

상위 수준 hello 기능은 다음과 같습니다: hello 주 엔터티가 정상 상태 이면 없는 동작이 변경 될 수 있습니다. Hello 때 [FailoverInterval] [ FailoverInterval] 기간이 경과 되 고 hello 주 엔터티는 일시적이 지 않은 후 없습니다 성공적인 보냅니다 표시 [MessagingException] [ MessagingException] 또는 [TimeoutException][TimeoutException], hello 다음 동작이 발생 합니다.

1. 주 엔터티 해제 되 고 hello 시스템 ping hello 기본 엔터티에 ping를 성공적으로 전달 될 때까지 작업 toohello를 보냅니다.
2. 임의 백로그 큐가 선택됩니다.
3. [BrokeredMessage] [ BrokeredMessage] 개체는 라우트된 toohello 백로그 큐를 선택 합니다.
4. 선택한 백로그 큐는 송신 작업 toohello 실패 하면 해당 큐 hello 순환에서 끌어온 하 고 새 큐를 선택 합니다. Hello에 대 한 보낸 사람 모두 [MessagingFactory] [ MessagingFactory] hello 오류의 인스턴스에 알아봅니다.

다음 수치 hello hello 순서를 나타냅니다. 첫째, hello 보낸 메시지를 보냅니다.

![쌍을 이루는 네임스페이스][0]

오류 toosend toohello 기본 큐, 시 hello 보낸 사람 메시지 tooa 임의로 선택 백로그 큐를 보내기 시작 합니다. 동시에 Ping 작업을 시작합니다.

![쌍을 이루는 네임스페이스][1]

이 시점에서 hello 메시지 hello 보조 큐에는 이며 toohello 기본 큐 배달 되지 않은. 기본 큐 hello 다시 정상 상태가 되 면 프로세스 하나 이상 hello 사이 펀을 실행 합니다. hello 사이 펀 hello 메시지 배달 모든 hello 다양 한 백로그에서 큐 toohello 적절 한 대상 엔터티 (큐 및 토픽).

![쌍을 이루는 네임스페이스][2]

이 항목의 나머지 부분에서는 hello hello 세부 사항 이러한 각 작업이 작동 하는 방법을 설명 합니다.

## <a name="creation-of-backlog-queues"></a>백로그 큐 만들기
hello [SendAvailabilityPairedNamespaceOptions] [ SendAvailabilityPairedNamespaceOptions] toohello 전달 된 개체가 [PairNamespaceAsync] [ PairNamespaceAsync] 메서드 hello를 나타냅니다. 백로그의 수를 큐 대기 하면 toouse 원하는 합니다. 각 백로그 큐는 hello를 사용 하 여 만든 후 다음 속성이 명시적으로 설정 됩니다 (다른 모든 값 toohello 설정 [QueueDescription] [ QueueDescription] 기본값):

| Path | [기본 네임스페이스]/x-servicebus-transfer/[index] 여기서 [index]는 [0, BacklogQueueCount] 사이의 값입니다. |
| --- | --- |
| MaxSizeInMegabytes |5120 |
| MaxDeliveryCount |int.MaxValue |
| DefaultMessageTimeToLive |TimeSpan.MaxValue |
| AutoDeleteOnIdle |TimeSpan.MaxValue |
| LockDuration |1분 |
| EnableDeadLetteringOnMessageExpiration |true |
| EnableBatchedOperations |true |

네임 스페이스에 대 한 첫 번째 백로그 큐 hello 생성 하는 예를 들어 **contoso** 라는 `contoso/x-servicebus-transfer/0`합니다.

Hello 큐를 만들 때 해당 큐가 있으면 hello 코드는 먼저 toosee를 확인 합니다. Hello 큐가 없는 경우 hello 큐가 만들어집니다. hello 코드는 그렇지 않습니다 "추가" 백로그 큐를 정리 합니다. 응용 프로그램을 기본 네임 스페이스 hello 경우 hello, 특히 **contoso** 백로그 큐 5 개 하지만 hello 경로로 백로그 큐 요청 `contoso/x-servicebus-transfer/7` 있는 경우 해당 추가 백로그 큐는 남아 있지만 사용 되지 않습니다. hello 시스템에서 사용 되지 않는 추가 백로그 큐 tooexist 명시적으로 허용 합니다. Hello 네임 스페이스 소유자는 사용 하지 않는/원치 않는 백로그 큐를 정리 됩니다. hello이이 결정은 서비스 버스 네임 스페이스에서 모든 hello 큐에 대 한 용도 존재 알 수 없습니다. 또한 큐 hello 지정 된 이름의 있지만 가정 hello에 맞지 않는 경우 [QueueDescription][QueueDescription], 이유는 hello 기본 동작에 대 한 직접 변경 합니다. 가 보장 되지 수정 toohello 백로그 큐에 대 한 코드에서 만들어진입니다. 있는지 tootest 변경 내용을 철저 하 게 확인 합니다.

## <a name="custom-messagesender"></a>사용자 지정 MessageSender
전송할 때, 모든 메시지가 통과 내부 [MessageSender] [ MessageSender] 작동 모든 항목 및 작업 "을 중단 합니다." 때 toohello 백로그 큐를 리디렉션하는 정상적으로 작동 하는 개체 일시적이지 않은 오류가 발생할 경우 타이머가 시작됩니다. 이후에 [TimeSpan] [ TimeSpan] hello로 구성 된 기간 [FailoverInterval] [ FailoverInterval] 성공 메시지가 전송 되는 속성 값 참여 하는 hello 장애 조치 합니다. 이 시점에서 hello 다음 작업이 수행 각 엔터티에 대해:

* Ping 작업이 실행 마다 [PingPrimaryInterval] [ PingPrimaryInterval] toocheck hello 엔터티가 사용할 수 있는 경우. 이 작업이 성공 하면 즉시 hello 엔터티를 사용 하는 모든 클라이언트 코드는 새 메시지 toohello 기본 네임 스페이스를 보내기 시작 합니다.
* 다른 발신자에서 동일한 엔터티 hello 하면 앞으로 요청 toosend toothat [BrokeredMessage] [ BrokeredMessage] hello 백로그 큐에 toosit 수정 toobe 송신할 합니다. hello에서 일부 속성을 제거 하는 hello 수정 [BrokeredMessage] [ BrokeredMessage] 개체를 다른 위치에 저장 합니다. hello 다음과 같은 속성이 선택이 취소 되며 서비스 버스 및 허용 hello SDK tooprocess 메시지 균일 하 게 새 별칭을 아래에 추가 합니다.

| 이전 속성 이름 | 새 속성 이름 |
| --- | --- |
| SessionId |x-ms-sessionid |
| TimeToLive |x-ms-timetolive |
| ScheduledEnqueueTimeUtc |x-ms-path |

원래 대상 경로도 hello x ms 경로 속성으로 hello 메시지에도 저장 됩니다. 이 설계는 단일 백로그 큐에 많은 엔터티 toocoexist에 대 한 메시지를 허용합니다. hello 속성 hello 사이 펀에 의해 다시 변환 됩니다.

사용자 지정 hello [MessageSender] [ MessageSender] 메시지 hello 256KB 제한에 근접 하 고 장애 조치 수행 중이 던 개체 문제가 발생할 수 있습니다. 사용자 지정 hello [MessageSender] [ MessageSender] 모든 큐 및 항목 hello 백로그 큐에서 메시지를 저장 하는 개체입니다. 이 개체는 hello 백로그 큐 내에 함께 많은 보관의 메시지를 혼합합니다. toohandle 간의 부하 분산 알지 못할 각 다른 hello SDK 임의로 많은 클라이언트에서 각 백로그 큐 하나를 선택 [QueueClient] [ QueueClient] 또는 [TopicClient] [ TopicClient] 코드에서 만들어야 합니다.

## <a name="pings"></a>Ping
Ping 메시지는 빈 [BrokeredMessage] [ BrokeredMessage] 와 해당 [ContentType] [ ContentType] 속성이 설정 tooapplication/vnd.ms-servicebus-ping 및 [TimeToLive] [ TimeToLive] 1 초 값입니다. 이러한 ping 서비스 버스의 한 특수 한 특성은: 모든 호출자가 요청할 때 하지 ping을 배달 hello 서버는 [BrokeredMessage][BrokeredMessage]합니다. 따라서 하지 않아도 toolearn 어떻게 tooreceive 하 고 이러한 메시지를 무시 합니다. 각 엔터티 (고유 큐 또는 토픽) 당 [MessagingFactory] [ MessagingFactory] 클라이언트당 인스턴스는 ping을 실행할 간주 되 면 toobe 사용할 수 없습니다. 기본적으로 이 작업은 1분에 한 번씩 수행됩니다. Ping 메시지 toobe 일반 서비스 버스 메시지로 간주 되며 대역폭 및 메시지 요금이 발생할 수 있습니다. Hello 클라이언트 hello 시스템을 사용할 수를 검색 하는 즉시 hello 메시지 중지 합니다.

## <a name="hello-syphon"></a>hello 사이 펀
Hello 응용 프로그램의 실행 프로그램을 하나 이상 hello 사이 펀 적극적으로 실행 되어야 합니다. hello 사이 펀 수행 긴 폴링 수신을 15 분 동안 지속 되 합니다. 모든 엔터티를 사용할 수 있는 백로그 큐가 10을 hello hello 사이 펀 호출 hello 수신 40 번 / 시간, 일, 당 960 번 및 28800 시간 30 일 이내에에서 작업을 호스팅하는 응용 프로그램입니다. Hello 사이 펀은 hello 백로그 toohello 기본 큐에서 메시지를 이동, 각 메시지에 요금 (메시지 크기와 대역폭에 대 한 표준 요금이 모든 단계에서 적용 됨)를 수행 하는 hello에서 발생 합니다.

1. Toohello 백로그를 보냅니다.
2. Hello 백로그에서 받기
3. 기본 toohello를 보냅니다.
4. 기본 hello에서 수신 합니다.

## <a name="closefault-behavior"></a>닫기/오류 동작
Hello 사이 펀, 한 번 hello primary 또는 secondary 상태를 호스팅하는 응용 프로그램 내에서 [MessagingFactory] [ MessagingFactory] 가 닫히거나 정의와 오류가 발생 한/닫히는 파트너 및 hello 없이 사이 펀이이 상태를 검색 hello 사이 펀 작동 합니다. 하는 경우 다른 hello [MessagingFactory] [ MessagingFactory] 닫혀 있지 않으면 hello 사이 펀은 hello 아직 열려 5 초 안에 오류 [MessagingFactory] [ MessagingFactory] .

## <a name="next-steps"></a>다음 단계
Service Bus 비동기 메시징에 대한 자세한 내용은 [비동기 메시징 패턴 및 고가용성][Asynchronous messaging patterns and high availability]을 참조하세요. 

[PairNamespaceAsync]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_PairNamespaceAsync_Microsoft_ServiceBus_Messaging_PairedNamespaceOptions_
[SendAvailabilityPairedNamespaceOptions]: /dotnet/api/microsoft.servicebus.messaging.sendavailabilitypairednamespaceoptions
[MessageSender]: /dotnet/api/microsoft.servicebus.messaging.messagesender
[MessagingFactory]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory
[FailoverInterval]: /dotnet/api/microsoft.servicebus.messaging.pairednamespaceoptions#Microsoft_ServiceBus_Messaging_PairedNamespaceOptions_FailoverInterval
[MessagingException]: /dotnet/api/microsoft.servicebus.messaging.messagingexception
[TimeoutException]: https://msdn.microsoft.com/library/azure/system.timeoutexception.aspx
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[QueueDescription]: /dotnet/api/microsoft.servicebus.messaging.queuedescription
[TimeSpan]: https://msdn.microsoft.com/library/azure/system.timespan.aspx
[PingPrimaryInterval]: /dotnet/api/microsoft.servicebus.messaging.sendavailabilitypairednamespaceoptions#Microsoft_ServiceBus_Messaging_SendAvailabilityPairedNamespaceOptions_PingPrimaryInterval
[QueueClient]: /dotnet/api/microsoft.servicebus.messaging.queueclient
[TopicClient]: /dotnet/api/microsoft.servicebus.messaging.topicclient
[ContentType]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_ContentType
[TimeToLive]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive
[Asynchronous messaging patterns and high availability]: service-bus-async-messaging.md
[0]: ./media/service-bus-paired-namespaces/IC673405.png
[1]: ./media/service-bus-paired-namespaces/IC673406.png
[2]: ./media/service-bus-paired-namespaces/IC673407.png

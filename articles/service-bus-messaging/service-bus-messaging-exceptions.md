---
title: "서비스 버스 메시징 예외 aaaAzure | Microsoft Docs"
description: "서비스 버스 메시징 예외 및 제안 조치의 목록입니다."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 3d8526fe-6e47-4119-9f3e-c56d916a98f9
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/06/2017
ms.author: sethm
ms.openlocfilehash: 0a206b7bbc808c1190044c1dfd6ffd47b9d454fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-messaging-exceptions"></a>서비스 버스 메시징 예외
이 문서에서는 Microsoft Azure 서비스 버스 hello에 의해 생성 된 몇 가지 예외가 나열 메시징 Api입니다. 이 참조는 주체 toochange, 업데이트에 대 한 다시 확인 합니다.

## <a name="exception-categories"></a>예외 범주
hello 메시지 Api 예외 생성 hello 다음 범주에 속하는 수, 연결 된 hello 동작 함께 tootry toofix 취할 수 있습니다 이러한. Hello 의미 하 고 예외는 메시징 엔터티 (큐/항목 또는 이벤트 허브)의 hello 형식에 따라 달라질 수 있습니다.

1. 사용자 코딩 오류([System.ArgumentException](https://msdn.microsoft.com/library/system.argumentexception.aspx), [System.InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception.aspx), [System.OperationCanceledException](https://msdn.microsoft.com/library/system.operationcanceledexception.aspx), [System.Runtime.Serialization.SerializationException](https://msdn.microsoft.com/library/system.runtime.serialization.serializationexception.aspx)). 일반 작업: 계속 하기 전에 toofix hello 코드를 사용해 보십시오.
2. 설치/구성 오류 ([Microsoft.ServiceBus.Messaging.MessagingEntityNotFoundException](/dotnet/api/microsoft.servicebus.messaging.messagingentitynotfoundexception), [System.UnauthorizedAccessException](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx). 일반 조치: 구성을 검토하고 필요한 경우 변경합니다.
3. 일시적 예외 ([Microsoft.ServiceBus.Messaging.MessagingException](/dotnet/api/microsoft.servicebus.messaging.messagingexception), [Microsoft.ServiceBus.Messaging.ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception), [Microsoft.ServiceBus.Messaging.MessagingCommunicationException](/dotnet/api/microsoft.servicebus.messaging.messagingcommunicationexception)). 일반 작업: hello 작업을 다시 시도 하거나 사용자에 게 알립니다.
4. 기타 예외 ([System.Transactions.TransactionException](https://msdn.microsoft.com/library/system.transactions.transactionexception.aspx), [System.TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx), [Microsoft.ServiceBus.Messaging.MessageLockLostException](/dotnet/api/microsoft.servicebus.messaging.messagelocklostexception), [Microsoft.ServiceBus.Messaging.SessionLockLostException](/dotnet/api/microsoft.servicebus.messaging.sessionlocklostexception)). 일반 동작: 특정 toohello 예외 형식입니다. toohello 표에 hello 다음 단원을 참조 하십시오. 

## <a name="exception-types"></a>예외 유형
hello 다음 표에 메시징 예외 형식, 원인 및 메모 권장된 작업 수행할 수 있습니다.

| **예외 유형** | **설명/원인/예** | **권장 조치** | **자동/즉시 다시 시도 참고** |
| --- | --- | --- | --- |
| [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx) |hello 서버 응답 하지 않았습니다 toohello 요청에 의해 제어 되는 시간을 지정 하는 hello 내에서 작업 [OperationTimeout](/dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings#Microsoft_ServiceBus_Messaging_MessagingFactorySettings_OperationTimeout)합니다. hello 서버가 완료 hello 요청 된 작업입니다. 이 toonetwork 또는 기타 인프라 지연 인해 발생할 수 있습니다. |일관성을 위해 hello 시스템 상태를 확인 하 고 필요한 경우 다시 시도 합니다. [시간 제한 예외](#timeoutexception)를 참조하세요. |다시 시도 하십시오; 일부 경우에 도움이 될 수 있습니다. 다시 시도 논리 toocode를 추가 합니다. |
| [InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception.aspx) |hello 요청 hello 서버 또는 서비스 내에서 사용자 작업이 허용 되지 않습니다. 자세한 내용은 hello 예외 메시지를 참조 하십시오. 예를 들어 [완료](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) hello 메시지에서 수신 된 경우이 예외를 생성 합니다 [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode) 모드입니다. |Hello 코드 및 hello 설명서를 확인 합니다. Hello 요청한 작업을 수행할 수 있는지 확인 합니다. |재시도로 해결되지 않습니다. |
| [OperationCanceledException](https://msdn.microsoft.com/library/system.operationcanceledexception.aspx) |시도 tooinvoke 이미 닫혀, 중단 또는 삭제 하는 개체에 대 한 작업을 수행 합니다. 드문 경우 지만 hello 앰비언트 트랜잭션이 이미 삭제 되었습니다. |Hello 코드를 확인 하 고 삭제 된 개체에 대 한 작업을 호출 하지 있는지 확인 합니다. |재시도로 해결되지 않습니다. |
| [UnauthorizedAccessException](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx) |hello [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) 개체 토큰을 가져올 수 없습니다, hello 토큰이 유효 하지 않거나 hello 토큰 hello 클레임 필요한 tooperform hello 작업이 포함 되지 않습니다. |Hello 올바른 값으로 hello 토큰 공급자가 생성 되었는지 확인 합니다. 액세스 제어 서비스 hello hello 구성을 확인 합니다. |다시 시도 하십시오; 일부 경우에 도움이 될 수 있습니다. 다시 시도 논리 toocode를 추가 합니다. |
| [ArgumentException](https://msdn.microsoft.com/library/system.argumentexception.aspx)<br /> [ArgumentNullException](https://msdn.microsoft.com/library/system.argumentnullexception.aspx)<br />[ArgumentOutOfRangeException](https://msdn.microsoft.com/library/system.argumentoutofrangeexception.aspx) |하나 이상의 제공 된 인수 toohello 메서드에 유효 하지 않습니다.<br /> hello 제공 된 URI 너무[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) 또는 [만들기](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_Create_System_Collections_Generic_IEnumerable_System_Uri__) 경로 세그먼트를 포함 합니다.<br /> hello URI 체계 너무 제공[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) 또는 [만들기](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_Create_System_Collections_Generic_IEnumerable_System_Uri__) 올바르지 않습니다. <br />hello 속성 값 32KB 보다 큽니다. |Hello 호출 코드 hello 인수가 올바른지 확인 하십시오. |재시도로 해결되지 않습니다. |
| [MessagingEntityNotFoundException](/dotnet/api/microsoft.servicebus.messaging.messagingentitynotfoundexception) |Hello 작업과 연결 된 엔터티가 존재 하지 않거나 삭제 되었습니다. |Hello 엔터티 있는지 확인 합니다. |재시도로 해결되지 않습니다. |
| [MessageNotFoundException](/dotnet/api/microsoft.servicebus.messaging.messagenotfoundexception) |특정 시퀀스 번호가 tooreceive 메시지를 시도 합니다. 이 메시지가 없습니다. |Hello 메시지를 받지 못했습니다 이미 있는지 확인 합니다. Hello 메시지가 배달 못한 메시지로 분류 상태인 경우 hello 배달 못한 편지 큐 toosee를 확인 합니다. |재시도로 해결되지 않습니다. |
| [MessagingCommunicationException](/dotnet/api/microsoft.servicebus.messaging.messagingcommunicationexception) |클라이언트 수 tooestablish 연결 tooService 버스 되지 않습니다. |제공 된 hello 호스트 이름이 올바른지와 hello 호스트에 연결할 수 있는지 확인 합니다. |간헐적인 연결 문제라면 재시도로 문제를 해결할 수 있습니다. |
| [ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception) |이 이번에 서비스를 hello 요청 tooprocess 수 없습니다. |클라이언트는 hello 작업을 다시 시도 한 다음 시간 동안 대기 수입니다. |클라이언트가 일정 시간 이후에 다시 시도할 수 있습니다. 재시도에서 다른 예외가 발생한 경우 해당 예외의 재시도 작동을 확인합니다. |
| [MessageLockLostException](/dotnet/api/microsoft.servicebus.messaging.messagelocklostexception) |Hello 메시지와 관련 된 잠금 토큰이 만료 되었는지 또는 hello 잠금 토큰을 찾을 수 없습니다. |Hello 메시지를 삭제 합니다. |재시도로 해결되지 않습니다. |
| [SessionLockLostException](/dotnet/api/microsoft.servicebus.messaging.sessionlocklostexception) |이 세션에 연결된 잠금이 손실되었습니다. |Hello 중단 [MessageSession](/dotnet/api/microsoft.servicebus.messaging.messagesession) 개체입니다. |재시도로 해결되지 않습니다. |
| [MessagingException](/dotnet/api/microsoft.servicebus.messaging.messagingexception) |일반 예외 hello 다음의 경우에에서 throw 될 수 있는 메시징:<br /> Toocreate 하려고 시도 하는 한 [QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient) 이름이 나 속한 tooa 다른 엔터티 유형 (예를 들어 항목) 경로 사용 하 여 합니다.<br />  이 시도가 수행 toosend 메시지가 256KB 보다 크면 합니다. hello 서버 또는 서비스 hello 요청을 처리 하는 동안 오류가 발생 했습니다. 자세한 내용은 hello 예외 메시지를 참조 하십시오. 보통은 일시적인 예외입니다. |Hello 코드를 확인 하 고 직렬화 가능 개체에 대해서만 hello 메시지 본문에 사용 되도록 (또는 사용자 지정 serializer를 사용 하 여). Hello 속성의 값 형식은 지원 hello 및 지원 되는 사용 유형을 hello 설명서를 확인 합니다. Hello 확인 [IsTransient](/dotnet/api/microsoft.servicebus.messaging.messagingexception#Microsoft_ServiceBus_Messaging_MessagingException_IsTransient) 속성입니다. 이 경우 **true**, hello 작업을 다시 시도할 수 있습니다. |재시도 동작이 정의되지 않았으면 도움이 되지 않습니다. |
| [MessagingEntityAlreadyExistsException](/dotnet/api/microsoft.servicebus.messaging.messagingentityalreadyexistsexception) |해당 서비스 네임 스페이스의 다른 엔터티에 의해 이미 사용 되는 이름 가진 엔터티가 toocreate를 시도 합니다. |Hello 기존 엔터티를 삭제 하거나 hello 엔터티 toobe 생성에 대 한 다른 이름을 선택 합니다. |재시도로 해결되지 않습니다. |
| [QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) |hello 메시징 엔터티의 최대 허용 크기에 도달 했습니다 또는 hello 연결 tooa 네임 스페이스의 최대 수를 초과 했습니다. |Hello 엔터티의 hello 엔터티에서 메시지를 받기 또는 해당 하위 큐에서 공간을 만듭니다. [QuotaExceededException](#quotaexceededexception)을 참조하세요. |그 동안 hello에서 제거 된 메시지 다시 시도 도움이 될 수 있습니다. |
| [RuleActionException](/dotnet/api/microsoft.servicebus.messaging.ruleactionexception) |서비스 버스 toocreate 잘못 된 규칙 작업을 시도 하는 경우이 예외를 반환 합니다. 서비스 버스는 해당 메시지에 대 한 hello 규칙 작업을 처리 하는 동안 오류가 발생 한 경우이 예외 tooa 배달 못한 메시지로 분류 메시지를 연결 합니다. |정확성에 대 한 hello 규칙 작업을 확인 합니다. |재시도로 해결되지 않습니다. |
| [FilterException](/dotnet/api/microsoft.servicebus.messaging.filterexception) |서비스 버스 toocreate 잘못 된 필터가 사용 하려는 경우이 예외를 반환 합니다. 서비스 버스는 해당 메시지에 대 한 hello 필터를 처리 하는 동안 오류가 발생 하는 경우이 예외 tooa 배달 못한 메시지로 분류 메시지를 연결 합니다. |Hello 필터를 올바른지 확인 하십시오. |재시도로 해결되지 않습니다. |
| [SessionCannotBeLockedException](/dotnet/api/microsoft.servicebus.messaging.sessioncannotbelockedexception) |세션을 특정 세션 ID 사용 하지만 hello 세션 다른 클라이언트에 의해 현재 잠겨 tooaccept을 시도 합니다. |Hello 세션 다른 클라이언트에서 잠겨 있는지 확인 합니다. |다시 시도 hello 세션 hello 중간에 해제 된 경우에 도움이 될 수 있습니다. |
| [TransactionSizeExceededException](/dotnet/api/microsoft.servicebus.messaging.transactionsizeexceededexception) |너무 많은 작업은 hello 트랜잭션의 일부입니다. |이 트랜잭션의 일부인 작업 hello 수를 줄입니다. |재시도로 해결되지 않습니다. |
| [MessagingEntityDisabledException](/dotnet/api/microsoft.servicebus.messaging.messagingentitydisabledexception) |비활성화된 엔터티의 런타임 작업에 대한 요청입니다. |Hello 엔터티를 활성화 합니다. |다시 시도 hello 엔터티 hello 중간에 활성화 된 경우에 도움이 될 수 있습니다. |
| [NoMatchingSubscriptionException](/dotnet/api/microsoft.servicebus.messaging.nomatchingsubscriptionexception) |서비스 버스 사용 사전 필터링 하 고 있고 hello 필터 조건과 일치 하는 메시지 tooa 항목을 보낼 경우이 예외를 반환 합니다. |하나 이상의 필터가 일치하는지 확인합니다. |재시도로 해결되지 않습니다. |
| [MessageSizeExceededException](/dotnet/api/microsoft.servicebus.messaging.messagesizeexceededexception) |메시지 페이로드 hello 256KB 제한을 초과 했습니다. Note hello 256KB 제한에는 시스템 속성 및.NET 오버 헤드를 포함할 수 있는 hello 총 메시지 크기입니다. |Hello 메시지 페이로드의 hello 크기를 줄인 다음 hello 작업을 다시 시도 합니다. |재시도로 해결되지 않습니다. |
| [TransactionException](https://msdn.microsoft.com/library/system.transactions.transactionexception.aspx) |앰비언트 트랜잭션을 hello (*Transaction.Current*) 올바르지 않습니다. 완료되었거나 중단되었을 수 있습니다. 내부 예외가 추가 정보를 제공할 수 있습니다. | |재시도로 해결되지 않습니다. |
| [TransactionInDoubtException](https://msdn.microsoft.com/library/system.transactions.transactionindoubtexception.aspx) |작업을 수행 하 여 의심 스러운, 트랜잭션에 하려고 또는 하려고 toocommit hello 트랜잭션 하 고 hello 트랜잭션 의심 스러운에서 됩니다. |Hello 트랜잭션이 이미 커밋 되었을 때 응용 프로그램에서 특별 한 경우), (으로이 예외를 처리 해야 합니다. |- |

## <a name="quotaexceededexception"></a>QuotaExceededException
[QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) 은 특정 엔터티에 대한 할당량이 초과됐음을 나타냅니다.

### <a name="queues-and-topics"></a>큐 및 토픽
큐 및 항목에 대 한이 방식은 hello 큐의 hello 크기입니다. hello 오류 메시지 속성에는 다음 예제는 hello와 같이 자세한 내용은 포함 됩니다.

```
Microsoft.ServiceBus.Messaging.QuotaExceededException
Message: hello maximum entity size has been reached or exceeded for Topic: ‘xxx-xxx-xxx’. 
    Size of entity in bytes:1073742326, Max entity size in bytes:
1073741824..TrackingId:xxxxxxxxxxxxxxxxxxxxxxxxxx, TimeStamp:3/15/2013 7:50:18 AM
```

hello 메시지 상태가 해당 hello 항목이 case 1GB (hello 기본 크기 제한)에 해당 크기 제한을 초과 했습니다. 

### <a name="namespaces"></a>네임스페이스

네임 스페이스에 [QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) 응용 프로그램가 hello 연결 tooa 네임 스페이스의 최대 수를 초과 했음을 나타낼 수 있습니다. 예:

```
Microsoft.ServiceBus.Messaging.QuotaExceededException: ConnectionsQuotaExceeded for namespace xxx.
<tracking-id-guid>_G12 ---> 
System.ServiceModel.FaultException`1[System.ServiceModel.ExceptionDetail]: 
ConnectionsQuotaExceeded for namespace xxx.
```

#### <a name="common-causes"></a>일반적인 원인
이 오류에 대 한 일반적인 두 가지 원인은: 배달 못 한 편지 큐 및 메시지 수신기 검색할 hello 합니다.

1. **배달 못 한 편지 큐** 판독기 toocomplete 메시지 실패와 hello 잠금이 만료 된 hello 메시지 toohello 큐/항목에 반환 됩니다. Hello 판독기에서 호출 하지 못하게 하는 예외를 발견 하는 경우 이러한 현상이 [BrokeredMessage.Complete](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.brokeredmessage.complete.aspx)합니다. 메시지를 읽은 후에 10 회 후 toohello 배달 못 한 편지 큐 기본적으로 이동 합니다. 이 동작은 hello에 의해 제어 됩니다 [QueueDescription.MaxDeliveryCount](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.queuedescription.maxdeliverycount.aspx) 속성 이며 10의 기본값은입니다. 메시지 hello 배달 못 한 편지 큐에 충돌 하는 대로 공간을 차지 합니다.
   
    tooresolve hello 문제 때 hello 배달 못 한 편지 큐에서 읽기 및 전체 hello 메시지 다른 큐에서 것입니다. hello [QueueClient](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.queueclient.aspx) 클래스도 포함 되어는 [FormatDeadLetterPath](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.queueclient.formatdeadletterpath.aspx) 메서드 toohelp 형식 hello 배달 못 한 편지 큐 경로입니다.
2. **수신기 중지됨** 수신기가 큐 또는 구독에서 메시지 수신을 중지했습니다. 방식으로 tooidentify hello hello에 toolook 이것이 [QueueDescription.MessageCountDetails](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.queuedescription.messagecountdetails.aspx) 속성 hello hello 메시지 전체 필드도 함께 표시 합니다. 경우 hello [ActiveMessageCount](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.messagecountdetails.activemessagecount.aspx) 높거나 성장 하 고 속성은 다음 hello 메시지 기록 되는 가능한 한 빨리 읽은 되지 않습니다.

### <a name="event-hubs"></a>Event Hubs
이벤트 허브는 이벤트 허브당 20개의 소비자 그룹으로 제한됩니다. 더 많은 toocreate 시도할 때 수신 된 [QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception)합니다. 

## <a name="timeoutexception"></a>TimeoutException
A [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx) 사용자가 시작한 작업 hello 작업이 제한 시간 보다 오래 걸리고 있는지를 나타냅니다. 

Hello의 hello 값을 확인 해야 [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit) 속성이이 제한에 도달 하는으로 인해 발생할 수도 있습니다는 [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx)합니다.

### <a name="queues-and-topics"></a>큐 및 토픽
Hello 제한 시간이 지정 된 큐 및 항목에 대 한 hello에서 [MessagingFactorySettings.OperationTimeout](/dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings#Microsoft_ServiceBus_Messaging_MessagingFactorySettings_OperationTimeout) 속성을 통해 또는 hello 연결 문자열의 일부로 [ServiceBusConnectionStringBuilder](/dotnet/api/microsoft.servicebus.servicebusconnectionstringbuilder). hello 오류 메시지 자체 다를 수 있습니다 하지만 항상 hello 현재 작업에 대해 지정 된 hello 제한 시간 값을 포함 합니다. 

### <a name="event-hubs"></a>Event Hubs
이벤트 허브에 대 한를 통해 또는 hello 연결 문자열의 일부로 써 hello 제한 시간이 지정 된 [ServiceBusConnectionStringBuilder](/dotnet/api/microsoft.servicebus.servicebusconnectionstringbuilder)합니다. hello 오류 메시지 자체 다를 수 있습니다 하지만 항상 hello 현재 작업에 대해 지정 된 hello 제한 시간 값을 포함 합니다. 

### <a name="common-causes"></a>일반적인 원인
이 오류에 대한 일반적인 두 가지 원인은 잘못된 구성 또는 일시적 서비스 오류입니다.

1. **잘못 된 구성** hello 작업 시간 초과 hello 작동 상태에 대 한 너무 작을 수 있습니다. hello hello client SDK의에서 hello 작업 시간 초과 대 한 기본값은 60 초입니다. 코드 hello 값이 있으면 toosee toosomething 너무 작게 설정 확인 합니다. Hello 네트워크의 hello 상황 및 CPU 사용량 hello 작업 시간 초과 tooa 매우 작은 값 설정 해야 하므로 특정 작업 toocomplete 걸리는 hello 시간에 영향을 줄 수 있습니다.
2. **임시 서비스 오류** 경우가 hello 서비스 버스 서비스 요청 처리의; 예를 들어 높은 트래픽이 시간에 지연이 발생할 수 있습니다. 이러한 경우 hello 작업이 성공할 때까지 잠시 후 작업을를 다시 시도할 수 있습니다. Hello 동일한 작업을 계속 실패 하면 여러 번 시도한 후 hello를 방문 하십시오 [Azure 서비스 상태 사이트](https://azure.microsoft.com/status/) toosee 알려진된 서비스의 작동 중지 시간 없는 경우.

## <a name="next-steps"></a>다음 단계

전체 서비스 버스.NET API 참조 hello에 대 한 참조 hello [Azure.NET API 참조](/dotnet/api/overview/azure/servicebus)합니다.

에 대 한 자세한 toolearn [서비스 버스](https://azure.microsoft.com/services/service-bus/), hello 다음 항목을 참조 하세요.

* [서비스 버스 메시징 개요](service-bus-messaging-overview.md)
* [서비스 버스 기본 사항](service-bus-fundamentals-hybrid-solutions.md)
* [서비스 버스 아키텍처](service-bus-architecture.md)


---
title: "aaaAzure 릴레이 예외와 방법을 tooresolve 해당 | Microsoft Docs"
description: "Azure 릴레이 예외 목록을 가져오고 toohelp 수행할 수 있는 권장된 조치가 문제를 해결 합니다."
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 5f9dd02c-cce0-43b3-8eb8-744f0c27f38c
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/23/2017
ms.author: sethm
ms.openlocfilehash: de417c8e9e43407ef355fd44f6170cf2cdc46d6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-relay-exceptions"></a>Azure Relay 예외

이 문서에서는 Azure 릴레이 Api hello로 인해 발생할 수 있는 몇 가지 예외가 나열 합니다. 이 참조는 주체 toochange, 업데이트에 대 한 다시 확인 합니다.

## <a name="exception-categories"></a>예외 범주

hello 릴레이 Api hello 다음 범주에 속하는 예외를 생성 합니다. 에 권장된 조치를 수행할 수 있는 toohelp 해결 hello 예외가 있습니다.

*   **사용자 코딩 오류**: [System.ArgumentException](https://msdn.microsoft.com/library/system.argumentexception.aspx), [System.InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception.aspx), [System.OperationCanceledException](https://msdn.microsoft.com/library/system.operationcanceledexception.aspx), [System.Runtime.Serialization.SerializationException](https://msdn.microsoft.com/library/system.runtime.serialization.serializationexception.aspx). 

    **일반 작업**: 계속 하기 전에 toofix hello 코드를 사용해 보십시오.
*   **설치/구성 오류**: [System.UnauthorizedAccessException](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx). 

    **일반 조치**: 구성을 검토합니다. 필요한 경우 hello 구성을 변경 합니다.
*   **일시적 예외**: [Microsoft.ServiceBus.Messaging.MessagingException](/dotnet/api/microsoft.servicebus.messaging.messagingexception), [Microsoft.ServiceBus.Messaging.ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception), [Microsoft.ServiceBus.Messaging.MessagingCommunicationException](/dotnet/api/microsoft.servicebus.messaging.messagingcommunicationexception). 

    **일반 작업**: hello 작업을 다시 시도 하거나 사용자에 게 알립니다.
*   **다른 예외**: [System.Transactions.TransactionException](https://msdn.microsoft.com/library/system.transactions.transactionexception.aspx), [System.TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx). 

    **일반 작업**: 특정 toohello 예외 형식입니다. 다음 단원을 hello에 hello 표를 참조 하세요. 

## <a name="exception-types"></a>예외 유형

hello 다음 표에 메시징 예외 형식 및 원인이 있습니다. 또한 제안 된 동작을 수행할 수 toohelp 해결 hello 예외를 설명 합니다.

| **예외 형식** | **설명** | **권장 조치** | **자동 또는 즉시 다시 시도 참고** |
| --- | --- | --- | --- |
| [시간 제한](https://msdn.microsoft.com/library/system.timeoutexception.aspx) |hello 서버 응답 하지 않았습니다 toohello 요청에 의해 제어 되는 시간을 지정 하는 hello 내에서 작업 [OperationTimeout](/dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout)합니다. 요청 된 작업을 완료 된 hello 있을 수 있습니다 서버를 hello 합니다. 이 toonetwork 또는 기타 인프라 지연 인해 발생할 수 있습니다. |일관성을 위해 hello 시스템 상태를 확인 하 고, 필요한 경우 다시 시도 합니다. [TimeoutException](#timeoutexception)을 참조하세요. |다시 시도 하십시오; 일부 경우에 도움이 될 수 있습니다. 다시 시도 논리 toocode를 추가 합니다. |
| [유효하지 않은 작업](https://msdn.microsoft.com/library/system.invalidoperationexception.aspx) |hello 요청 hello 서버 또는 서비스 내에서 사용자 작업이 허용 되지 않습니다. 자세한 내용은 hello 예외 메시지를 참조 하십시오. |Hello 코드 및 hello 설명서를 확인 합니다. 해당 hello 요청한 작업을 수행할 수 있는지 확인 합니다. |재시도로 해결되지 않습니다. |
| [작업 취소됨](https://msdn.microsoft.com/library/system.operationcanceledexception.aspx) |시도 tooinvoke 이미 닫혀, 중단 또는 삭제 하는 개체에 대 한 작업을 수행 합니다. 드문 경우 지만 hello 앰비언트 트랜잭션이 이미 삭제 되었습니다. |Hello 코드를 확인 하 고 삭제 된 개체에 대 한 작업을 호출 하지 있는지 확인 합니다. |재시도로 해결되지 않습니다. |
| [무단 액세스](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx) |hello [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) 개체 토큰을 가져올 수 없습니다, hello 토큰이 유효 하지 않거나 hello 토큰 hello 클레임 필요한 tooperform hello 작업이 포함 되지 않습니다. |Hello 올바른 값으로 해당 hello 토큰 공급자가 생성 되었는지 확인 합니다. 액세스 제어 서비스 hello hello 구성을 확인 합니다. |다시 시도 하십시오; 일부 경우에 도움이 될 수 있습니다. 다시 시도 논리 toocode를 추가 합니다. |
| [인수 예외](https://msdn.microsoft.com/library/system.argumentexception.aspx)<br /> [인수 Null](https://msdn.microsoft.com/library/system.argumentnullexception.aspx)<br />[인수가 범위를 벗어남](https://msdn.microsoft.com/library/system.argumentoutofrangeexception.aspx) |Hello 다음 중 하나 이상 발생 했습니다.<br />하나 이상의 제공 된 인수 toohello 메서드에 유효 하지 않습니다.<br /> hello 제공 된 URI 너무[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) 또는 [만들기](/dotnet/api/microsoft.servicebus.messaging.messagingfactory.create) 하나 이상의 경로 세그먼트를 포함 합니다.<br />hello URI 체계 너무 제공[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) 또는 [만들기](/dotnet/api/microsoft.servicebus.messaging.messagingfactory.create) 올바르지 않습니다. <br />hello 속성 값 32KB 보다 큽니다. |Hello 호출 코드 hello 인수가 올바른지 확인 하십시오. |재시도로 해결되지 않습니다. |
| [서버 작업 중](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception) |이 이번에 서비스를 hello 요청 tooprocess 수 없습니다. |클라이언트 hello 일정 시간 동안 대기 다음 hello 작업을 다시 시도 수입니다. |클라이언트 hello 특정 간격 이후에 다시 시도 될 수 있습니다. 경우에 다른 예외를 다시 시도 결과 해당 예외의 hello 다시 시도 동작을 확인 합니다. |
| [할당량이 초과됨](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) |hello 메시징 엔터티의 최대 허용 크기에 도달 했습니다. |Hello 엔터티의 hello 엔터티에서 메시지를 받기 또는 해당 하위 큐에서 공간을 만듭니다. [QuotaExceededException](#quotaexceededexception)을 참조하세요. |그 동안 hello에서 제거 된 메시지 다시 시도 도움이 될 수 있습니다. |
| [메시지 크기 초과됨](/dotnet/api/microsoft.servicebus.messaging.messagesizeexceededexception) |메시지 페이로드 hello 256KB 제한을 초과 했습니다. Note hello 256KB 제한에 hello 총 메시지 크기입니다. hello 총 메시지 크기는 시스템 속성 및 Microsoft.NET 오버 헤드에 포함할 수 있습니다. |Hello 메시지 페이로드의 hello 크기를 줄인 다음 hello 작업을 다시 시도 합니다. |재시도로 해결되지 않습니다. |

## <a name="quotaexceededexception"></a>QuotaExceededException

[QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) 은 특정 엔터티에 대한 할당량이 초과됐음을 나타냅니다.

릴레이 대 한이 예외는 hello 래핑합니다 [System.ServiceModel.QuotaExceededException](https://msdn.microsoft.com/library/system.servicemodel.quotaexceededexception.aspx),이 끝점에 대 한 hello 최대 항목 수를 수신기를 나타내는 초과 합니다. 이 hello 표시 **MaximumListenersPerEndpoint** hello 예외 메시지의 값입니다.

## <a name="timeoutexception"></a>TimeoutException
A [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx) 사용자가 시작한 작업 hello 작업이 제한 시간 보다 오래 걸리고 있는지를 나타냅니다. 

Hello의 hello 값을 확인 [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit) 속성입니다. 제한에 도달하면 [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx)이 발생할 수 있습니다.

릴레이의 경우 릴레이 발신자 연결을 처음 열 때 시간 제한 예외가 발생할 수 있습니다. 이 예외의 일반적인 원인은 다음과 같이 두 가지가 있습니다.

*   hello [OpenTimeout](https://msdn.microsoft.com/library/wcf.opentimeout.aspx) 값 (도 의해 두 번째 부분) 너무 작을 수 있습니다.
* 온-프레미스 릴레이 수신기를 응답 하지 않을 수 있습니다 (또는 새 클라이언트 연결을 수락할 수신기 수 없게 하는 방화벽 규칙 문제를 발생할 수) 및 hello [OpenTimeout](https://msdn.microsoft.com/library/wcf.opentimeout.aspx) 값은 20 초 보다 작은 약 합니다.

예제:

```
'System.TimeoutException’: hello operation did not complete within hello allotted timeout of 00:00:10.
hello time allotted toothis operation may have been a portion of a longer timeout.
```

### <a name="common-causes"></a>일반적인 원인
이 오류의 일반적인 원인은 다음과 같이 두 가지입니다.

*   **잘못된 구성**
    
    작업 시간 초과 hello hello 작동 상태에 대 한 너무 작을 수 있습니다. hello hello client SDK의에서 hello 작업 시간 초과 대 한 기본값은 60 초입니다. Toosee를 코드의 hello 값 너무 작아서 toosomething를 설정 되었는지 여부를 확인 합니다. 참고 hello 네트워크의 CPU 사용량 및 hello 상태 소요 되는 작업 toocomplete hello 시간에 영향을 줄 수 있습니다. 것이 좋습니다 tooset hello 작업이 시간 초과 tooa 매우 작은 값이 아닌 합니다.
*   **일시적인 서비스 오류**

    경우에 따라서는 hello 릴레이 서비스 요청 처리에 지연이 발생할 수 있습니다. 예를 들어 트래픽이 높은 경우 발생할 수 있습니다. 이 경우에 hello 작업이 성공할 때까지 지연 후 작업을 다시 시도 합니다. Hello 동일한 작업을 계속 되 면 toofail 여러 번 시도한 후 확인 hello [Azure 서비스 상태 사이트](https://azure.microsoft.com/status/) toosee 서비스 중단 알고 있는 경우.

## <a name="next-steps"></a>다음 단계
* [Azure Relay FAQ](relay-faq.md)
* [릴레이 네임스페이스 만들기](relay-create-namespace-portal.md)
* [Azure Relay 및 .NET 시작](relay-hybrid-connections-dotnet-get-started.md)
* [Azure Relay 및 Node 시작](relay-hybrid-connections-node-get-started.md)


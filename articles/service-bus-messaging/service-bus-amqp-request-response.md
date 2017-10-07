---
title: "Azure 서비스 버스 요청-응답 기반 작업에서 aaaAMQP 1.0 | Microsoft Docs"
description: "Microsoft Azure Service Bus 요청/응답 기반 작업 목록입니다."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/27/2017
ms.author: sethm
ms.openlocfilehash: e4f26219c53b0c4172747af683fe511d6366ff2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="amqp-10-in-microsoft-azure-service-bus-request-response-based-operations"></a>Microsoft Azure Service Bus에서 AMQP 1.0: Microsoft Azure Service Bus 요청/응답 기반 작업

이 항목에는 Microsoft Azure 서비스 버스 요청/응답 기반 작업의 hello 목록을 정의합니다. 이 정보는 hello AMQP 관리 버전 1.0의 시행 중인 초안을 기반으로 합니다.  
  
자세한 지침을 보려면 유선 수준 AMQP 1.0 프로토콜, 서비스 버스를 구현 하 고 hello OASIS AMQP 기술 사양에 빌드하 하는 방법을 설명에 참조 hello [Azure 서비스 버스 및 이벤트 허브 프로토콜 가이드에서 AMQP 1.0](service-bus-amqp-protocol-guide.md)합니다.  
  
## <a name="concepts"></a>개념  
  
### <a name="entity-description"></a>엔터티 설명  

엔터티 설명을 tooeither 서비스 버스 참조 [QueueDescription 클래스](/dotnet/api/microsoft.servicebus.messaging.queuedescription), [TopicDescription 클래스](/dotnet/api/microsoft.servicebus.messaging.topicdescription), 또는 [SubscriptionDescription 클래스](/dotnet/api/microsoft.servicebus.messaging.subscriptiondescription) 개체입니다.  
  
### <a name="brokered-message"></a>broker 저장 메시지  

서비스 버스를 매핑된 tooan AMQP 메시지에서 메시지를 나타냅니다. hello에 hello 매핑이 정의 되어 [서비스 버스 AMQP 프로토콜 가이드](service-bus-amqp-protocol-guide.md)합니다.  
  
## <a name="attach-tooentity-management-node"></a>Tooentity 관리 노드를 연결 합니다.  

이 문서에 설명 된 모든 hello 작업이 요청/응답 패턴을 따르는 범위가 지정 된 tooan 엔터티 되며 tooan 엔터티 관리 노드를 연결 해야 합니다.  
  
### <a name="create-link-for-sending-requests"></a>요청 전송을 위한 링크 만들기  

요청을 보내기 위한 링크 toohello 관리 노드를 만듭니다.  
  
```  
requestLink = session.attach(     
role: SENDER,   
    target: { address: "<entity address>/$management" },   
    source: { address: ""<my request link unique address>" }   
)  
  
```  
  
### <a name="create-link-for-receiving-responses"></a>응답 수신을 위한 링크 만들기  

Hello 관리 노드에서 응답을 받기에 대 한 링크를 만듭니다.  
  
```  
responseLink = session.attach(    
role: RECEIVER,   
    source: { address: "<entity address>/$management" }   
    target: { address: "<my response link unique address>" }   
)  
  
```  
  
### <a name="transfer-a-request-message"></a>요청 메시지 전송  

요청 메시지를 전송합니다.  
  
```  
requestLink.sendTransfer(  
        Message(  
                properties: {  
                        message-id: <request id>,  
                        reply-to: "<my response link unique address>"  
                },  
                application-properties: {  
                        "operation" -> "<operation>",  
                },  
        )  
```  
  
### <a name="receive-a-response-message"></a>응답 메시지 수신  

Hello 응답 링크에서 hello 응답 메시지를 받습니다.  
  
```  
responseMessage = responseLink.receiveTransfer()  
```  
  
hello 응답 메시지는 다음 폼 hello에:
  
```  
Message(  
properties: {     
        correlation-id: <request id>  
    },  
    application-properties: {  
            "statusCode" -> <status code>,  
            "statusDescription" -> <status description>,  
           },         
)  
  
```  
  
### <a name="service-bus-entity-address"></a>Service Bus 엔터티 주소  

Service Bus 엔터티 주소는 다음과 같아야 합니다.  
  
|엔터티 형식|주소|예|  
|-----------------|-------------|-------------|  
|큐|`<queue_name>`|`“myQueue”`<br /><br /> `“site1/myQueue”`|  
|토픽|`<topic_name>`|`“myTopic”`<br /><br /> `“site2/page1/myQueue”`|  
|subscription|`<topic_name>/Subscriptions/<subscription_name>`|`“myTopic/Subscriptions/MySub”`|  
  
## <a name="message-operations"></a>메시지 작업  
  
### <a name="message-renew-lock"></a>메시지 갱신 잠금  

Hello 시간별 hello 엔터티 설명에 지정 된 메시지의 잠금 hello를 확장 합니다.  
  
#### <a name="request"></a>요청  

hello 요청 메시지에는 다음과 같은 응용 프로그램 속성 hello를 포함 되어야 합니다.  
  
|키|값 형식|필수|값 내용|  
|---------|----------------|--------------|--------------------|  
|operation|string|예|`com.microsoft:renew-lock`|  
|`com.microsoft:server-timeout`|uint|아니요|작업 서버 제한 시간(밀리초)입니다.|  
  
 항목을 다음 hello로 맵을 포함 하는 amqp 값 섹션 hello 요청 메시지 본문 구성 되어야 합니다.  
  
|키|값 형식|필수|값 내용|  
|---------|----------------|--------------|--------------------|  
|`lock-tokens`|uuid의 배열|예|메시지 잠금 토큰 toorenew 합니다.|  
  
#### <a name="response"></a>응답  

hello 응답 메시지는 hello 다음과 같은 응용 프로그램 속성을 포함 해야 합니다.  
  
|키|값 형식|필수|값 내용|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|예|HTTP 응답 코드 [RFC2616]<br /><br /> 200: OK – 성공, 그렇지 않으면 실패입니다.|  
|statusDescription|string|아니요|Hello 상태에 대 한 설명입니다.|  
  
항목을 다음 hello로 맵을 포함 하는 amqp 값 섹션 hello 응답 메시지 본문 구성 되어야 합니다.  
  
|키|값 형식|필수|값 내용|  
|---------|----------------|--------------|--------------------|  
|만료|타임 스탬프 배열|예|메시지 잠금 토큰 새 만료 해당 toohello 요청 잠금 토큰입니다.|  
  
### <a name="peek-message"></a>메시지 보기  

잠그지 않고 메시지를 봅니다.  
  
#### <a name="request"></a>요청  

hello 요청 메시지에는 다음과 같은 응용 프로그램 속성 hello를 포함 되어야 합니다.  
  
|키|값 형식|필수|값 내용|  
|---------|----------------|--------------|--------------------|  
|operation|string|예|`com.microsoft:peek-message`|  
|`com.microsoft:server-timeout`|uint|아니요|작업 서버 제한 시간(밀리초)입니다.|  
  
hello 요청 메시지 본문으로 구성 되어야는 **amqp 값** 섹션을 포함 하는 **지도** 항목 다음 hello로:  
  
|키|값 형식|필수|값 내용|  
|---------|----------------|--------------|--------------------|  
|`from-sequence-number`|long|예|Toostart 피킹은에서 시퀀스 번호입니다.|  
|`message-count`|int|예|메시지 toopeek의 최대 수입니다.|  
  
#### <a name="response"></a>응답  

hello 응답 메시지는 hello 다음과 같은 응용 프로그램 속성을 포함 해야 합니다.  
  
|키|값 형식|필수|값 내용|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|예|HTTP 응답 코드 [RFC2616]<br /><br /> 200: OK – 더 많은 메시지가 있음<br /><br /> 0xcc: 콘텐츠 없음 – 더 이상 메시지가 없음|  
|statusDescription|string|아니요|Hello 상태에 대 한 설명입니다.|  
  
hello 응답 메시지 본문으로 구성 되어야는 **amqp 값** 섹션을 포함 하는 **지도** 항목 다음 hello로:  
  
|키|값 형식|필수|값 내용|  
|---------|----------------|--------------|--------------------|  
|메시지의 최대 전달 수|맵 목록|예|모든 맵이 메시지를 나타내는 메시지 목록입니다.|  
  
메시지를 나타내는 hello 맵 hello 다음 항목을 포함 해야 합니다.  
  
|키|값 형식|필수|값 내용|  
|---------|----------------|--------------|--------------------|  
|message|바이트 배열|예|AMQP 1.0 실시간 인코딩된 메시지입니다.|  
  
### <a name="schedule-message"></a>메시지 예약  

메시지를 예약합니다.  
  
#### <a name="request"></a>요청  

hello 요청 메시지에는 다음과 같은 응용 프로그램 속성 hello를 포함 되어야 합니다.  
  
|키|값 형식|필수|값 내용|  
|---------|----------------|--------------|--------------------|  
|operation|string|예|`com.microsoft:schedule-message`|  
|`com.microsoft:server-timeout`|uint|아니요|작업 서버 제한 시간(밀리초)입니다.|  
  
hello 요청 메시지 본문으로 구성 되어야는 **amqp 값** 섹션을 포함 하는 **지도** 항목 다음 hello로:  
  
|키|값 형식|필수|값 내용|  
|---------|----------------|--------------|--------------------|  
|메시지의 최대 전달 수|맵 목록|예|모든 맵이 메시지를 나타내는 메시지 목록입니다.|  
  
메시지를 나타내는 hello 맵 hello 다음 항목을 포함 해야 합니다.  
  
|키|값 형식|필수|값 내용|  
|---------|----------------|--------------|--------------------|  
|message-id|string|예|string으로 `amqpMessage.Properties.MessageId`|  
|session-id|string|예|`amqpMessage.Properties.GroupId as string`|  
|파티션 키|string|예|`amqpMessage.MessageAnnotations.”x-opt-partition-key"`|  
|message|바이트 배열|예|AMQP 1.0 실시간 인코딩된 메시지입니다.|  
  
#### <a name="response"></a>응답  

hello 응답 메시지는 hello 다음과 같은 응용 프로그램 속성을 포함 해야 합니다.  
  
|키|값 형식|필수|값 내용|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|예|HTTP 응답 코드 [RFC2616]<br /><br /> 200: OK – 성공, 그렇지 않으면 실패입니다.|  
|statusDescription|string|아니요|Hello 상태에 대 한 설명입니다.|  
  
hello 응답 메시지 본문으로 구성 되어야는 **amqp 값** 지도 항목을 다음 hello로 포함 된 섹션:  
  
|키|값 형식|필수|값 내용|  
|---------|----------------|--------------|--------------------|  
|시퀀스 번호|long 배열|예|예약된 메시지의 시퀀스 번호입니다. 시퀀스 번호가 사용 되는 toocancel입니다.|  
  
### <a name="cancel-scheduled-message"></a>예약된 메시지 취소  

예약된 메시지를 취소합니다.  
  
#### <a name="request"></a>요청  

hello 요청 메시지에는 다음과 같은 응용 프로그램 속성 hello를 포함 되어야 합니다.  
  
|키|값 형식|필수|값 내용|  
|---------|----------------|--------------|--------------------|  
|operation|string|예|`com.microsoft:cancel-scheduled-message`|  
|`com.microsoft:server-timeout`|uint|아니요|작업 서버 제한 시간(밀리초)입니다.|  
  
hello 요청 메시지 본문으로 구성 되어야는 **amqp 값** 섹션을 포함 하는 **지도** 항목 다음 hello로:  
  
|키|값 형식|필수|값 내용|  
|---------|----------------|--------------|--------------------|  
|시퀀스 번호|long 배열|예|예약 된 메시지 toocancel의 시퀀스 번호입니다.|  
  
#### <a name="response"></a>응답  

hello 응답 메시지는 hello 다음과 같은 응용 프로그램 속성을 포함 해야 합니다.  
  
|키|값 형식|필수|값 내용|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|예|HTTP 응답 코드 [RFC2616]<br /><br /> 200: OK – 성공, 그렇지 않으면 실패입니다.|  
|statusDescription|string|아니요|Hello 상태에 대 한 설명입니다.|  
  
hello 응답 메시지 본문으로 구성 되어야는 **amqp 값** 지도 항목을 다음 hello로 포함 된 섹션:  
  
|키|값 형식|필수|값 내용|  
|---------|----------------|--------------|--------------------|  
|시퀀스 번호|long 배열|예|예약된 메시지의 시퀀스 번호입니다. 시퀀스 번호가 사용 되는 toocancel입니다.|  
  
## <a name="session-operations"></a>세션 작업  
  
### <a name="session-renew-lock"></a>세션 갱신 잠금  

Hello 시간별 hello 엔터티 설명에 지정 된 메시지의 잠금 hello를 확장 합니다.  
  
#### <a name="request"></a>요청  

hello 요청 메시지에는 다음과 같은 응용 프로그램 속성 hello를 포함 되어야 합니다.  
  
|키|값 형식|필수|값 내용|  
|---------|----------------|--------------|--------------------|  
|operation|string|예|`com.microsoft:renew-session-lock`|  
|`com.microsoft:server-timeout`|uint|아니요|작업 서버 제한 시간(밀리초)입니다.|  
  
hello 요청 메시지 본문으로 구성 되어야는 **amqp 값** 섹션을 포함 하는 **지도** 항목 다음 hello로:  
  
|키|값 형식|필수|값 내용|  
|---------|----------------|--------------|--------------------|  
|session-id|string|예|세션 ID.|  
  
#### <a name="response"></a>응답  

hello 응답 메시지는 hello 다음과 같은 응용 프로그램 속성을 포함 해야 합니다.  
  
|키|값 형식|필수|값 내용|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|예|HTTP 응답 코드 [RFC2616]<br /><br /> 200: OK – 더 많은 메시지가 있음<br /><br /> 0xcc: 콘텐츠 없음 – 더 이상 메시지가 없음|  
|statusDescription|string|아니요|Hello 상태에 대 한 설명입니다.|  
  
hello 응답 메시지 본문으로 구성 되어야는 **amqp 값** 지도 항목을 다음 hello로 포함 된 섹션:  
  
|키|값 형식|필수|값 내용|  
|---------|----------------|--------------|--------------------|  
|expiration|timestamp|예|새 만료.|  
  
### <a name="peek-session-message"></a>세션 메시지 보기  

잠그지 않고 세션 메시지를 봅니다.  
  
#### <a name="request"></a>요청  

hello 요청 메시지에는 다음과 같은 응용 프로그램 속성 hello를 포함 되어야 합니다.  
  
|키|값 형식|필수|값 내용|  
|---------|----------------|--------------|--------------------|  
|operation|string|예|`com.microsoft:peek-message`|  
|`com.microsoft:server-timeout`|uint|아니요|작업 서버 제한 시간(밀리초)입니다.|  
  
hello 요청 메시지 본문으로 구성 되어야는 **amqp 값** 섹션을 포함 하는 **지도** 항목 다음 hello로:  
  
|키|값 형식|필수|값 내용|  
|---------|----------------|--------------|--------------------|  
|from-sequence-number|long|예|Toostart 피킹은에서 시퀀스 번호입니다.|  
|message-count|int|예|메시지 toopeek의 최대 수입니다.|  
|session-id|string|예|세션 ID.|  
  
#### <a name="response"></a>응답  

hello 응답 메시지는 hello 다음과 같은 응용 프로그램 속성을 포함 해야 합니다.  
  
|키|값 형식|필수|값 내용|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|예|HTTP 응답 코드 [RFC2616]<br /><br /> 200: OK – 더 많은 메시지가 있음<br /><br /> 0xcc: 콘텐츠 없음 – 더 이상 메시지가 없음|  
|statusDescription|string|아니요|Hello 상태에 대 한 설명입니다.|  
  
hello 응답 메시지 본문으로 구성 되어야는 **amqp 값** 지도 항목을 다음 hello로 포함 된 섹션:  
  
|키|값 형식|필수|값 내용|  
|---------|----------------|--------------|--------------------|  
|메시지의 최대 전달 수|맵 목록|예|모든 맵이 메시지를 나타내는 메시지 목록입니다.|  
  
 메시지를 나타내는 hello 맵 hello 다음 항목을 포함 해야 합니다.  
  
|키|값 형식|필수|값 내용|  
|---------|----------------|--------------|--------------------|  
|message|바이트 배열|예|AMQP 1.0 실시간 인코딩된 메시지입니다.|  
  
### <a name="set-session-state"></a>세션 상태 설정  

집합 hello 세션의 상태입니다.  
  
#### <a name="request"></a>요청  

hello 요청 메시지에는 다음과 같은 응용 프로그램 속성 hello를 포함 되어야 합니다.  
  
|키|값 형식|필수|값 내용|  
|---------|----------------|--------------|--------------------|  
|operation|string|예|`com.microsoft:peek-message`|  
|`com.microsoft:server-timeout`|uint|아니요|작업 서버 제한 시간(밀리초)입니다.|  
  
hello 요청 메시지 본문으로 구성 되어야는 **amqp 값** 섹션을 포함 하는 **지도** 항목 다음 hello로:  
  
|키|값 형식|필수|값 내용|  
|---------|----------------|--------------|--------------------|  
|session-id|string|예|세션 ID.|  
|session-state|바이트 배열|예|불투명한 이진 본문.|  
  
#### <a name="response"></a>응답  

hello 응답 메시지는 hello 다음과 같은 응용 프로그램 속성을 포함 해야 합니다.  
  
|키|값 형식|필수|값 내용|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|예|HTTP 응답 코드 [RFC2616]<br /><br /> 200: OK – 성공, 그렇지 않으면 실패입니다.|  
|statusDescription|string|아니요|Hello 상태에 대 한 설명입니다.|  
  
### <a name="get-session-state"></a>세션 상태 가져오기  

세션의 hello 상태를 가져옵니다.  
  
#### <a name="request"></a>요청  

hello 요청 메시지에는 다음과 같은 응용 프로그램 속성 hello를 포함 되어야 합니다.  
  
|키|값 형식|필수|값 내용|  
|---------|----------------|--------------|--------------------|  
|operation|string|예|`com.microsoft:get-session-state`|  
|`com.microsoft:server-timeout`|uint|아니요|작업 서버 제한 시간(밀리초)입니다.|  
  
hello 요청 메시지 본문으로 구성 되어야는 **amqp 값** 섹션을 포함 하는 **지도** 항목 다음 hello로:  
  
|키|값 형식|필수|값 내용|  
|---------|----------------|--------------|--------------------|  
|session-id|string|예|세션 ID.|  
  
#### <a name="response"></a>응답  

hello 응답 메시지는 hello 다음과 같은 응용 프로그램 속성을 포함 해야 합니다.  
  
|키|값 형식|필수|값 내용|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|예|HTTP 응답 코드 [RFC2616]<br /><br /> 200: OK – 성공, 그렇지 않으면 실패입니다.|  
|statusDescription|string|아니요|Hello 상태에 대 한 설명입니다.|  
  
hello 응답 메시지 본문으로 구성 되어야는 **amqp 값** 섹션을 포함 하는 **지도** 항목 다음 hello로:  
  
|키|값 형식|필수|값 내용|  
|---------|----------------|--------------|--------------------|  
|session-state|바이트 배열|예|불투명한 이진 본문.|  
  
### <a name="enumerate-sessions"></a>세션 열거  

메시지 엔터티에서 세션을 열거합니다.  
  
#### <a name="request"></a>요청  

hello 요청 메시지에는 다음과 같은 응용 프로그램 속성 hello를 포함 되어야 합니다.  
  
|키|값 형식|필수|값 내용|  
|---------|----------------|--------------|--------------------|  
|operation|string|예|`com.microsoft:get-message-sessions`|  
|`com.microsoft:server-timeout`|uint|아니요|작업 서버 제한 시간(밀리초)입니다.|  
  
hello 요청 메시지 본문으로 구성 되어야는 **amqp 값** 섹션을 포함 하는 **지도** 항목 다음 hello로:  
  
|키|값 형식|필수|값 내용|  
|---------|----------------|--------------|--------------------|  
|last-updated-time|timestamp|예|지정된 된 시간 후에 업데이트 tooinclude만 세션을 필터링 합니다.|  
|skip|int|예|세션 수를 건너뜁니다.|  
|top|int|예|최대 세션 수입니다.|  
  
#### <a name="response"></a>응답  

hello 응답 메시지는 hello 다음과 같은 응용 프로그램 속성을 포함 해야 합니다.  
  
|키|값 형식|필수|값 내용|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|예|HTTP 응답 코드 [RFC2616]<br /><br /> 200: OK – 더 많은 메시지가 있음<br /><br /> 0xcc: 콘텐츠 없음 – 더 이상 메시지가 없음|  
|statusDescription|string|아니요|Hello 상태에 대 한 설명입니다.|  
  
hello 응답 메시지 본문으로 구성 되어야는 **amqp 값** 섹션을 포함 하는 **지도** 항목 다음 hello로:  
  
|키|값 형식|필수|값 내용|  
|---------|----------------|--------------|--------------------|  
|skip|int|예|상태 코드가 200인 경우 건너뛴 세션 수입니다.|  
|sessions-ids|문자열 배열입니다.|예|상태 코드가 200인 경우 세션 ID 배열입니다.|  
  
## <a name="rule-operations"></a>규칙 작업  
  
### <a name="add-rule"></a>규칙 추가  
  
#### <a name="request"></a>요청  

hello 요청 메시지에는 다음과 같은 응용 프로그램 속성 hello를 포함 되어야 합니다.  
  
|키|값 형식|필수|값 내용|  
|---------|----------------|--------------|--------------------|  
|operation|string|예|`com.microsoft:add-rule`|  
|`com.microsoft:server-timeout`|uint|아니요|작업 서버 제한 시간(밀리초)입니다.|  
  
hello 요청 메시지 본문으로 구성 되어야는 **amqp 값** 섹션을 포함 하는 **지도** 항목 다음 hello로:  
  
|키|값 형식|필수|값 내용|  
|---------|----------------|--------------|--------------------|  
|rule-name|string|예|구독 및 토픽 이름을 포함하지 않는 규칙 이름입니다.|  
|rule-description|map|예|다음 섹션에 지정된 대로 규칙 설명입니다.|  
  
hello **규칙 설명** 맵 항목을 다음 hello 있어야 합니다. 여기서 **sql 필터** 및 **상관 관계 필터** 함께 사용할 수 없습니다:  
  
|키|값 형식|필수|값 내용|  
|---------|----------------|--------------|--------------------|  
|sql-filter|map|예|`sql-filter`hello 다음 섹션에 지정 된 대로 합니다.|  
|correlation-filter|map|예|`correlation-filter`hello 다음 섹션에 지정 된 대로 합니다.|  
|sql-rule-action|map|예|`sql-rule-action`hello 다음 섹션에 지정 된 대로 합니다.|  
  
hello sql 필터 맵 hello 다음 항목을 포함 해야 합니다.  
  
|키|값 형식|필수|값 내용|  
|---------|----------------|--------------|--------------------|  
|식|string|예|Sql 필터 식.|  
  
hello **상관 관계 필터** 맵에 hello 다음 항목 중 하나 이상을 포함 해야 합니다.  
  
|키|값 형식|필수|값 내용|  
|---------|----------------|--------------|--------------------|  
|correlation-id|string|아니요||  
|message-id|string|아니요||  
|to|string|아니요||  
|reply-to|string|아니요||  
|label|string|아니요||  
|session-id|string|아니요||  
|reply-to-session-id|string|아니요||  
|content-type|string|아니요||  
|properties|map|아니요|버스 tooService 매핑합니다 [BrokeredMessage.Properties](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Properties)합니다.|  
  
hello **sql 규칙-작업** 지도 hello 다음 항목을 포함 해야 합니다.  
  
|키|값 형식|필수|값 내용|  
|---------|----------------|--------------|--------------------|  
|식|string|예|Sql 작업 식.|  
  
#### <a name="response"></a>응답  

hello 응답 메시지는 hello 다음과 같은 응용 프로그램 속성을 포함 해야 합니다.  
  
|키|값 형식|필수|값 내용|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|예|HTTP 응답 코드 [RFC2616]<br /><br /> 200: OK – 성공, 그렇지 않으면 실패입니다.|  
|statusDescription|string|아니요|Hello 상태에 대 한 설명입니다.|  
  
### <a name="remove-rule"></a>규칙 제거  
  
#### <a name="request"></a>요청  

hello 요청 메시지에는 다음과 같은 응용 프로그램 속성 hello를 포함 되어야 합니다.  
  
|키|값 형식|필수|값 내용|  
|---------|----------------|--------------|--------------------|  
|operation|string|예|`com.microsoft:remove-rule`|  
|`com.microsoft:server-timeout`|uint|아니요|작업 서버 제한 시간(밀리초)입니다.|  
  
hello 요청 메시지 본문으로 구성 되어야는 **amqp 값** 섹션을 포함 하는 **지도** 항목 다음 hello로:  
  
|키|값 형식|필수|값 내용|  
|---------|----------------|--------------|--------------------|  
|rule-name|string|예|구독 및 토픽 이름을 포함하지 않는 규칙 이름입니다.|  
  
#### <a name="response"></a>응답  

hello 응답 메시지는 hello 다음과 같은 응용 프로그램 속성을 포함 해야 합니다.  
  
|키|값 형식|필수|값 내용|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|예|HTTP 응답 코드 [RFC2616]<br /><br /> 200: OK – 성공, 그렇지 않으면 실패입니다.|  
|statusDescription|string|아니요|Hello 상태에 대 한 설명입니다.|  
  
## <a name="deferred-message-operations"></a>지연된 메시지 작업  
  
### <a name="receive-by-sequence-number"></a>시퀀스 번호로 받기  

시퀀스 번호로 지연된 메시지를 받습니다.  
  
#### <a name="request"></a>요청  

hello 요청 메시지에는 다음과 같은 응용 프로그램 속성 hello를 포함 되어야 합니다.  
  
|키|값 형식|필수|값 내용|  
|---------|----------------|--------------|--------------------|  
|operation|string|예|`com.microsoft:receive-by-sequence-number`|  
|`com.microsoft:server-timeout`|uint|아니요|작업 서버 제한 시간(밀리초)입니다.|  
  
hello 요청 메시지 본문으로 구성 되어야는 **amqp 값** 섹션을 포함 하는 **지도** 항목 다음 hello로:  
  
|키|값 형식|필수|값 내용|  
|---------|----------------|--------------|--------------------|  
|시퀀스 번호|long 배열|예|시퀀스 번호.|  
|receiver-settle-mode|ubyte|예|AMQP 코어 v1.0에 지정된 대로 **수신기 장착** 모드입니다.|  
  
#### <a name="response"></a>응답  

hello 응답 메시지는 hello 다음과 같은 응용 프로그램 속성을 포함 해야 합니다.  
  
|키|값 형식|필수|값 내용|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|예|HTTP 응답 코드 [RFC2616]<br /><br /> 200: OK – 성공, 그렇지 않으면 실패입니다.|  
|statusDescription|string|아니요|Hello 상태에 대 한 설명입니다.|  
  
hello 응답 메시지 본문으로 구성 되어야는 **amqp 값** 섹션을 포함 하는 **지도** 항목 다음 hello로:  
  
|키|값 형식|필수|값 내용|  
|---------|----------------|--------------|--------------------|  
|메시지의 최대 전달 수|맵 목록|예|모든 맵이 메시지를 나타내는 메시지 목록입니다.|  
  
메시지를 나타내는 hello 맵 hello 다음 항목을 포함 해야 합니다.  
  
|키|값 형식|필수|값 내용|  
|---------|----------------|--------------|--------------------|  
|lock-token|uuid|예|`receiver-settle-mode`가 1인 경우 토큰을 잠급니다.|  
|message|바이트 배열|예|AMQP 1.0 실시간 인코딩된 메시지입니다.|  
  
### <a name="update-disposition-status"></a>처리 상태 업데이트  

지연 된 메시지의 hello 처리 상태를 업데이트합니다.  
  
#### <a name="request"></a>요청  

hello 요청 메시지에는 다음과 같은 응용 프로그램 속성 hello를 포함 되어야 합니다.  
  
|키|값 형식|필수|값 내용|  
|---------|----------------|--------------|--------------------|  
|operation|string|예|`com.microsoft:update-disposition`|  
|`com.microsoft:server-timeout`|uint|아니요|작업 서버 제한 시간(밀리초)입니다.|  
  
hello 요청 메시지 본문으로 구성 되어야는 **amqp 값** 섹션을 포함 하는 **지도** 항목 다음 hello로:  
  
|키|값 형식|필수|값 내용|  
|---------|----------------|--------------|--------------------|  
|disposition-status|string|예|완료됨<br /><br /> 중단됨<br /><br /> 일시 중단됨|  
|lock-tokens|uuid의 배열|예|메시지 잠금 토큰 tooupdate 처리 상태입니다.|  
|deadletter-reason|string|아니요|처리 상태 너무 설정 된 경우에 설정할 수 있습니다**일시 중단**합니다.|  
|deadletter-description|string|아니요|처리 상태 너무 설정 된 경우에 설정할 수 있습니다**일시 중단**합니다.|  
|properties-to-modify|map|아니요|메시지 속성 toomodify를 중개 하는 서비스 버스의 목록입니다.|  
  
#### <a name="response"></a>응답  

hello 응답 메시지는 hello 다음과 같은 응용 프로그램 속성을 포함 해야 합니다.  
  
|키|값 형식|필수|값 내용|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|예|HTTP 응답 코드 [RFC2616]<br /><br /> 200: OK – 성공, 그렇지 않으면 실패입니다.|  
|statusDescription|string|아니요|Hello 상태에 대 한 설명입니다.|

## <a name="next-steps"></a>다음 단계

AMQP 및 서비스 버스에 대해 자세히 toolearn 방문 링크를 따라 hello:

* [Service Bus AMQP 개요]
* [Service Bus 분할 큐 및 토픽에 대한 AMQP 1.0 지원]
* [Windows Server용 Service Bus의 AMQP]

[Service Bus AMQP 개요]: service-bus-amqp-overview.md
[Service Bus 분할 큐 및 토픽에 대한 AMQP 1.0 지원]: service-bus-partitioned-queues-and-topics-amqp-overview.md
[Windows Server용 Service Bus의 AMQP]: https://msdn.microsoft.com/library/dn574799.asp
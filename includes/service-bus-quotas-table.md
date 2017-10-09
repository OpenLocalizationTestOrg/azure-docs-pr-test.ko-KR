다음 표에서 hello 할당량 정보 특정 tooService 버스 메시징 나열 합니다. 가격에 대 한 정보 및 서비스 버스에 대 한 기타 할당량에 대 한 참조 hello [서비스 버스 가격](https://azure.microsoft.com/pricing/details/service-bus/) 개요입니다.

| 할당량 이름 | 범위 | 유형 | 초과 시 동작 | 값 |
| --- | --- | --- | --- | --- |
| Azure 구독당 기본 / 표준 네임스페이스 최대 수 |네임스페이스 |정적 |Hello 포털에서 추가 기본 / 표준 네임 스페이스를 위한 후속 요청이 거부 됩니다. |100|
| Azure 구독당 프리미엄 네임스페이스 최대 수 |네임스페이스 |정적 |추가 프리미엄 네임 스페이스에 대 한 후속 요청 hello 포털에서 거부 됩니다. |10 |
| 큐/토픽 크기 |엔터티 |Hello 큐/항목 작성 시 정의 합니다. |들어오는 메시지가 거부 되 고 hello 호출 코드에서 예외가 수신 됩니다. |1, 2, 3, 4 또는 5GB입니다.<br /><br />경우 [분할](../articles/service-bus-messaging/service-bus-partitioning.md) 가 활성화 hello 최대 큐/항목 크기는 80GB입니다. |
| 네임스페이스에 대한 동시 연결 수 |네임스페이스 |정적 |추가 연결에 대 한 후속 요청 거부 되 고 hello 호출 코드에서 예외가 수신 됩니다. REST 작업은 동시 TCP 연결 계산에 포함되지 않습니다. |NetMessaging: 1,000<br /><br />AMQP: 5,000 |
| 큐/토픽/구독 엔터티의 동시 수신 요청 수 |엔터티 |정적 |후속 수신 요청이 거부 되 고 hello 호출 코드에서 예외가 수신 됩니다. 이 할당량은 결합 toohello 적용 됩니다. 수의 동시 수신 작업 항목에 대 한 모든 구독 전반에 걸쳐 있습니다. |5, 000 |
| 서비스 네임스페이스당 토픽/큐 수 |시스템 수준 |정적 |새 항목 또는 hello 서비스 네임 스페이스에 큐를 만들기 위한 이후 요청이 거부 됩니다. Hello를 통해 구성 된 경우 결과적으로 [Azure 포털][Azure portal], 오류 메시지가 생성 됩니다. Hello 관리 API 호출 하는 경우 hello 호출 코드에서 예외가 수신 됩니다. |10000<br /><br />hello 총의 서비스 네임 스페이스에서 항목 및 큐 수 보다 작거나 같은 too10, 000입니다.<br/>모든 엔터티를 분할 하는 대로 해당 tooPremium 아닙니다. |
| 서비스 네임스페이스당 분할된 토픽/큐 수 |시스템 수준 |정적 |새 분할 된 항목 또는 hello 서비스 네임 스페이스에 큐 만들기 위한 후속 요청이 거부 됩니다. Hello를 통해 구성 된 경우 결과적으로 [Azure 포털][Azure portal], 오류 메시지가 생성 됩니다. Hello 관리 API에서에서 호출 된 경우는 **QuotaExceededException** hello 호출 코드에서 예외를 수신 합니다. |기본 및 표준 계층 - 100<br />[프리미엄](../articles/service-bus-messaging/service-bus-premium-messaging.md) - 1,000(메시징 단위당)<br/><br />각 분할 된 큐 또는 항목의 네임 스페이스 당 10, 000 엔터티 hello 할당량에 합산 됩니다. |
| 모든 메시징 엔터티 경로의 최대 크기: 큐 또는 토픽 |엔터티 |정적 |- |260자 |
| 모든 메시징 엔터티 이름의 최대 크기: 네임스페이스, 구독 또는 구독 규칙 |엔터티 |정적 |- |50자 |
| 큐/토픽/구독 엔터티의 메시지 크기 |시스템 수준 |정적 |이러한 할당량을 초과 하는 들어오는 메시지가 거부 되 고 hello 호출 코드에서 예외가 수신 됩니다. |최대 메시지 크기: 256KB([표준 계층](../articles/service-bus-messaging/service-bus-premium-messaging.md))/1MB([프리미엄 계층](../articles/service-bus-messaging/service-bus-premium-messaging.md)). <br /><br />**참고** toosystem 오버 헤드로 인해이 제한은 일반적으로 약간 덜 합니다.<br /><br />최대 헤더 크기: 64KB<br /><br />속성 모음에서 헤더 속성의 최대 수: **byte/int.MaxValue**<br /><br />속성 모음의 최대 속성 크기: 명시적 제한은 없습니다. 최대 헤더 크기로 제한됩니다. |
| 큐/토픽/구독 엔터티의 메시지 속성 크기 |시스템 수준 |정적 |A **SerializationException** 예외가 생성됩니다. |각 속성에 대한 최대 메시지 속성 크기는 32K입니다. 모든 속성의 누적 크기는 64K를 초과할 수 없습니다. Hello의 전체 헤더 toohello이 적용 됩니다 [BrokeredMessage](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.aspx), 항목이 둘 다 사용자 속성 뿐만 아니라 시스템 속성 (같은 [SequenceNumber](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.sequencenumber.aspx), [레이블](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.label.aspx), [ MessageId](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.messageid.aspx)등). |
| 토픽당 구독 수 |시스템 수준 |정적 |Hello 항목에 대 한 추가 구독을 만들기 위한 이후 요청이 거부 됩니다. 결과적으로, hello 포털을 통해 구성 하는 경우 오류 메시지가 표시 됩니다. Hello 관리 API에서 호출 된 경우 hello 호출 코드에서 예외가 수신 됩니다. |2, 000 |
| 토픽당 SQL 필터 수 |시스템 수준 |정적 |Hello 항목에 대 한 추가 필터를 만들기 위한 이후 요청이 거부 되 고 hello 호출 코드에서 예외가 수신 됩니다. |2, 000 |
| 토픽당 상관 관계 필터 수 |시스템 수준 |정적 |Hello 항목에 대 한 추가 필터를 만들기 위한 이후 요청이 거부 되 고 hello 호출 코드에서 예외가 수신 됩니다. |100,000 |
| SQL 필터/작업의 크기 |시스템 수준 |정적 |추가 필터를 만들기 위한 후속 요청이 거부 되 고 hello 호출 코드에서 예외가 수신 됩니다. |필터 조건 문자열의 최대 길이: 1024(1K)<br /><br />규칙 작업 문자열의 최대 길이: 1024(1K)<br /><br />규칙 작업당 식의 최대 수: 32 |
| 네임스페이스, 큐 또는 토픽당 [SharedAccessAuthorizationRule](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.sharedaccessauthorizationrule.aspx) 규칙 수 |엔터티, 네임스페이스 |정적 |추가 규칙을 만들기 위한 후속 요청이 거부 되 고 hello 호출 코드에서 예외가 수신 됩니다. |최대 규칙 수: 12 <br /><br /> 서비스 버스 네임 스페이스에 구성 된 규칙에는 해당 네임 스페이스의 tooall 큐 및 항목 적용 됩니다. |

[Azure portal]: https://portal.azure.com
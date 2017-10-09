hello 다음 표에서 할당량 고 특정 tooAzure 이벤트 허브를 제한 합니다. Event Hubs 가격에 대한 자세한 내용은 [Event Hubs 가격 책정](https://azure.microsoft.com/pricing/details/event-hubs/)을 참조하세요.

| 제한 | 범위 | 유형 | 초과 시 동작 | 값 |
| --- | --- | --- | --- | --- |
| 네임스페이스당 이벤트 허브 개수 |네임스페이스 |정적 |새로운 네임스페이스 생성에 대한 이후 요청은 거부됩니다. |10 |
| 이벤트 허브당 파티션 수 |엔터티 |정적 |- |32 |
| 이벤트 허브당 소비자 그룹 수 |엔터티 |정적 |- |20 |
| 네임스페이스당 AMQP 연결 수 |네임스페이스 |정적 |추가 연결에 대 한 후속 요청 거부 되 고 hello 호출 코드에서 예외가 수신 됩니다. |5, 000 |
| Event Hubs 이벤트의 최대 크기|시스템 수준 |정적 |- |256 KB |
| Event Hub 이름의 최대 크기 |엔터티 |정적 |- |50자 |
| 소비자 그룹당 비 Epoch 수신자 수 |엔터티 |정적 |- |5 |
| 이벤트 데이터의 최대 보존 기간 |엔터티 |정적 |- |1-7일 |
| 최대 처리량 단위 |네임스페이스 |정적 |초과 hello 처리량 단위 제한인 제한 하 여 데이터 toobe 시키고 유효성 검사를 생성 한  **[ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception)**합니다. 표준 계층의 경우 [지원 요청](/azure/azure-supportability/how-to-create-azure-support-request)을 작성하여 더 많은 수의 처리량 단위를 요청할 수 있습니다. [추가 처리량 단위](../articles/event-hubs/event-hubs-auto-inflate.md)는 약정된 구매를 기준으로 20개 단위로 사용할 수 있습니다. |20 |


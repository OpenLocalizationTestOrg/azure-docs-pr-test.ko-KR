---
title: "python aaaHow toouse Azure 서비스 버스 주제 | Microsoft Docs"
description: "자세한 방법을 toouse Azure 서비스 버스 항목 및 Python에서 구독 합니다."
services: service-bus-messaging
documentationcenter: python
author: sethmanheim
manager: timlt
editor: 
ms.assetid: c4f1d76c-7567-4b33-9193-3788f82934e4
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 1171cbe8061bb3d73e2ce92ecc0cf45afae37054
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-python"></a>어떻게 toouse 서비스 버스 항목 및 구독 python

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

이 문서에서는 설명 방법을 toouse 서비스 버스 항목 및 구독 합니다. hello 샘플 Python에서 작성 되 고 hello를 사용 하 여 [Azure Python SDK 패키지][Azure Python package]합니다. hello 가이드에서 다루는 시나리오 포함 **항목 및 구독을 만드는**, **구독 필터를 만드는**, **tooa 부분 메시지를 보내는**, **받기 구독에서 메시지**, 및 **항목 및 구독을 삭제**합니다. 항목 및 구독에 대 한 자세한 내용은 참조 hello [다음 단계](#next-steps) 섹션.

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

> [!NOTE] 
> Python tooinstall 또는 hello 필요 하면 [Azure Python 패키지][Azure Python package], hello 참조 [Python 설치 가이드](../python-how-to-install.md)합니다.

## <a name="create-a-topic"></a>토픽 만들기
hello **ServiceBusService** 개체를 사용 하면 toowork 항목과 함께 합니다. 서비스 버스 tooprogrammatically 액세스 원하는 모든 Python 파일의 hello 맨 위 근처에 hello 다음을 추가 합니다.

```python
from azure.servicebus import ServiceBusService, Message, Topic, Rule, DEFAULT_RULE_NAME
```

hello 다음 코드에서는 **ServiceBusService** 개체입니다. `mynamespace`, `sharedaccesskeyname` 및 `sharedaccesskey`를 실제 네임스페이스, SAS(공유 액세스 서명) 키 이름 및 키 값으로 바꿉니다.

```python
bus_service = ServiceBusService(
    service_namespace='mynamespace',
    shared_access_key_name='sharedaccesskeyname',
    shared_access_key_value='sharedaccesskey')
```

Hello에서 hello SAS 키 이름에 대 한 hello 값 및 값을 얻을 수 있습니다 [Azure 포털][Azure portal]합니다.

```python
bus_service.create_topic('mytopic')
```

hello `create_topic` 메서드는 또한 메시지 시간 toolive 또는 최대 항목 크기와 같은 toooverride 기본 항목 설정을 사용할 수 있는 추가 옵션을 지원 합니다. hello 다음 예제에서는 설정 hello 최대 항목 크기 too5 GB 인데 1 분의 시간 toolive (TTL) 값:

```python
topic_options = Topic()
topic_options.max_size_in_megabytes = '5120'
topic_options.default_message_time_to_live = 'PT1M'

bus_service.create_topic('mytopic', topic_options)
```

## <a name="create-subscriptions"></a>구독 만들기
Hello로 만들어집니다 구독 tootopics **ServiceBusService** 개체입니다. 이름이 지정 된 구독과 hello toohello 구독의 가상 큐에 배달 된 메시지 집합을 제한 하는 선택적 필터가 있을 수 있습니다.

> [!NOTE]
> 구독 영구 tooexist 중 하나가 될 때까지 계속 사용 되며 또는 hello toowhich 항목은 구독, 삭제 됩니다.
> 
> 

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a>Hello 기본 (MatchAll) 필터와 구독 만들기
hello **MatchAll** 필터는 필터 지정 하지 않으면은 새 구독을 만들 때 사용 되는 hello 기본 필터. Hello 때 **MatchAll** 필터 사용 하는 경우 모든 부분 메시지 게시 된 toohello hello 구독의 가상 큐에 배치 됩니다. hello 다음 예제에서는 구독을 만드는 라는 `AllMessages` 사용 하 여 기본 hello 및 **MatchAll** 필터입니다.

```python
bus_service.create_subscription('mytopic', 'AllMessages')
```

### <a name="create-subscriptions-with-filters"></a>필터를 사용하여 구독 만들기
Toospecify tooa 항목에 특정 항목을 구독 내에서 표시 됩니다. 보낸 메시지 수 있도록 하는 필터를 정의할 수도 있습니다.

hello 가장 유연한 구독에서 지 원하는 필터 형식은 **SqlFilter**, SQL92의 하위 집합을 구현 하는 합니다. SQL 필터가 있는 게시 된 toohello 항목 hello 메시지의 hello 속성에서 작동 합니다. SQL 필터와 함께 사용할 수 있는 hello 식에 대 한 자세한 내용은 참조 hello [SqlFilter.SqlExpression] [ SqlFilter.SqlExpression] 구문입니다.

Hello를 사용 하 여 필터 tooa 구독을 추가 하려면 **만들\_규칙** hello 방식의 **ServiceBusService** 개체입니다. 이 방법을 사용 하면 tooadd 새 필터 tooan 기존 구독이 있습니다.

> [!NOTE]
> Hello 기본 필터를 자동으로 적용 되기 때문에 tooall 새 구독 hello 기본 필터 또는 hello를 먼저 제거 해야 **MatchAll** 지정할 수 있는 필터를 재정의 합니다. Hello를 사용 하 여 hello 기본 규칙을 제거할 수 있습니다 `delete_rule` hello 방식의 **ServiceBusService** 개체입니다.
> 
> 

hello 다음 예제에서는 구독을 만드는 라는 `HighMessages` 와 **SqlFilter** 만 사용자 지정 하는 메시지를 선택 하는 `messagenumber` 3 보다 큰 속성:

```python
bus_service.create_subscription('mytopic', 'HighMessages')

rule = Rule()
rule.filter_type = 'SqlFilter'
rule.filter_expression = 'messagenumber > 3'

bus_service.create_rule('mytopic', 'HighMessages', 'HighMessageFilter', rule)
bus_service.delete_rule('mytopic', 'HighMessages', DEFAULT_RULE_NAME)
```

마찬가지로, hello 다음 예제에서는 구독을 만드는 라는 `LowMessages` 와 **SqlFilter** 만 설정 된 메시지를 선택 하는 `messagenumber` 속성 작은 보다 짧거나 too3:

```python
bus_service.create_subscription('mytopic', 'LowMessages')

rule = Rule()
rule.filter_type = 'SqlFilter'
rule.filter_expression = 'messagenumber <= 3'

bus_service.create_rule('mytopic', 'LowMessages', 'LowMessageFilter', rule)
bus_service.delete_rule('mytopic', 'LowMessages', DEFAULT_RULE_NAME)
```

이제 메시지를 보내면 너무`mytopic` 구독 tooreceivers toohello 항상 제공 된다는 **AllMessages** 항목 구독 및 구독 하는 선택적으로 배달 된 tooreceivers toohello **HighMessages**  및 **LowMessages** 주제 구독 (에 따라 hello 메시지 콘텐츠 포함).

## <a name="send-messages-tooa-topic"></a>Tooa 부분 메시지 보내기
메시지 tooa 서비스 버스 항목 toosend 응용 프로그램 hello를 사용 해야 `send_topic_message` hello 방식의 **ServiceBusService** 개체입니다.

hello 다음 예제에서는 5 toosend 테스트 너무 메시지 방법을`mytopic`합니다. 해당 hello 참고 `messagenumber` hello 루프의 반복 hello에 각 메시지의 속성 값 달라 집니다 (결정 구독 받는):

```python
for i in range(5):
    msg = Message('Msg {0}'.format(i).encode('utf-8'), custom_properties={'messagenumber':i})
    bus_service.send_topic_message('mytopic', msg)
```

서비스 버스 주제 hello에서 최대 메시지 크기는 256KB 지원 [표준 계층](service-bus-premium-messaging.md) 및 hello에서 1 MB [Premium 계층](service-bus-premium-messaging.md)합니다. hello 표준 및 사용자 지정 응용 프로그램 속성을 포함 하는 hello 헤더는 64KB의 최대 크기를 가질 수 있습니다. Hello 메시지에 항목을 보유할 수에 제한이 없음을 않으며 항목을 보유 하는 hello 메시지의 총 크기 hello 켜져 캡입니다. 이 토픽 크기는 생성 시 정의되며 상한이 5GB입니다. 할당량에 대한 자세한 내용은 [Service Bus 할당량][Service Bus quotas]을 참조하세요.

## <a name="receive-messages-from-a-subscription"></a>구독에서 메시지 받기
Hello를 사용 하 여 구독에서 메시지를 받을 `receive_subscription_message` 메서드 hello **ServiceBusService** 개체:

```python
msg = bus_service.receive_subscription_message('mytopic', 'LowMessages', peek_lock=False)
print(msg.body)
```

메시지를 읽고 때 hello 구독에서 삭제 됩니다 매개 변수를 hello `peek_lock` 너무 설정 되어**False**합니다. (미리 보기)를 읽을 수 있으며 hello 매개 변수를 설정 하 여 hello 큐에서 삭제 하지 않고 hello 메시지 잠금 `peek_lock` 너무**True**합니다.

읽기의 동작은 hello 및 hello의 일부 수신 작업으로 hello 메시지를 삭제 합니다.는 hello 간단한 모델 시나리오는 응용 프로그램 실패 하는 hello 이벤트의 메시지를 처리 하지 않아도 안전한 수에 가장 적합 합니다. toounderstand hello는 hello 소비자 문제에 요청을 수신 하는 시나리오 및 후 처리 하기 전에 크래시 합니다. 서비스 버스 사용 되는 것을 다음 hello 응용 프로그램 다시 시작 되 고 메시지 사용을 시작할 때 hello 메시지를 표시 한 됩니다, 때문에 누락 됩니다 hello 메시지 했던 이전 toohello 크래시를 사용 합니다.

경우 hello `peek_lock` 매개 변수가 너무 설정 된**True**, hello 수신 하므로 누락 된 메시지를 허용할 수 없는 가능한 toosupport 응용 프로그램 2 단계 작업이 됩니다. 서비스 버스 요청을 받으면 다음 메시지 toobe hello 사용 다른 소비자가 수신할 tooprevent 잠근 하 고 toohello 응용 프로그램 반환 찾습니다. Hello hello의 두 번째 단계를 완료 후 hello 응용 프로그램 hello 메시지 처리를 완료 (또는 이후 처리를 위해 안정적으로 저장)를 호출 하 여 수신 프로세스 `delete` hello에 대 한 메서드 **메시지** 개체입니다. hello `delete` 메서드 사용 되는 것 hello 메시지를 표시 하 고 hello 구독에서 제거 합니다.

```python
msg = bus_service.receive_subscription_message('mytopic', 'LowMessages', peek_lock=True)
print(msg.body)

msg.delete()
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Toohandle 응용 프로그램이 크래시 되는 방법 및 읽을 수 없는 메시지
서비스 버스 기능 toohelp 정상적으로 응용 프로그램 또는 메시지를 처리 하는 데 문제가 오류 로부터 복구를 제공 합니다. 수신기 응용 프로그램 수 없는 경우 몇 가지 이유로 tooprocess 환영 메시지가 다음 hello 호출할 수 있는 `unlock` 메서드 hello **메시지** 개체입니다. Hello 구독 내에서 서비스 버스 toounlock hello 메시지 시키며 수신 다시 사용할 수 있는 toobe 확인, 사용자가 여를 많이 사용 응용 프로그램 또는 다른 소비 응용 프로그램에서 동일한 hello 중 하나입니다.

또한 hello 구독 내에서 잠긴 메시지와 관련 된 제한 시간 집합과 hello 응용 프로그램 실패 하기 전에 hello 메시지 tooprocess hello 잠금 제한 시간이 만료 (예를 들어 hello 응용 프로그램이 충돌할 경우), 서비스 버스 hello 메시지의 잠금을 해제 한 다음 자동으로 수신 다시 사용할 수 있는 toobe로 전환 합니다.

Hello hello 응용 프로그램 이벤트 충돌 hello 메시지 처리 전후에 그러나 hello 전에 `delete` 메서드는 다음 다시 시작할 때 hello 메시지 다시 전달한 toohello 응용 프로그램 됩니다. 이 이라고 하는데 *일단 처리 이상*, 즉, 각 메시지가 최소 한 번 처리 되지만 특정 상황 hello에 동일한 메시지를 다시 배달 될 수 있습니다. Hello 시나리오 중복 처리가 허용 되지 않는, 응용 프로그램 개발자가 추가 논리 tootheir 응용 프로그램을 toohandle 중복 메시지 배달을 추가 해야 합니다. 이 대개 달성 hello를 사용 하 여 **MessageId** 배달 시도 간에 일정 남아 있는 hello 메시지의 속성입니다.

## <a name="delete-topics-and-subscriptions"></a>토픽 및 구독 삭제
항목과 구독은 영구적이 고 명시적으로 해야 hello 통해 삭제 [Azure 포털] [ Azure portal] 또는 프로그래밍 방식으로 합니다. hello 다음 예제에서는 toodelete hello 항목 이름을 지정 하는 방법 `mytopic`:

```python
bus_service.delete_topic('mytopic')
```

항목을 삭제 하면 모든 구독에 등록 된 hello 항목을 삭제 합니다. 구독을 개별적으로 삭제할 수도 있습니다. hello 다음 코드를 보여 줍니다 방법과 toodelete 구독 이름 `HighMessages` hello에서 `mytopic` 항목:

```python
bus_service.delete_subscription('mytopic', 'HighMessages')
```

## <a name="next-steps"></a>다음 단계
서비스 버스 항목의 hello 기본 사항 학습 한, 했으므로 이러한 링크 toolearn 자세한 수행 합니다.

* [큐, 토픽 및 구독][Queues, topics, and subscriptions]을 참조하세요.
* [SqlFilter.SqlExpression][SqlFilter.SqlExpression]에 대한 참조입니다.

[Azure portal]: https://portal.azure.com
[Azure Python package]: https://pypi.python.org/pypi/azure  
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter.SqlExpression]: service-bus-messaging-sql-filter.md
[Service Bus quotas]: service-bus-quotas.md 

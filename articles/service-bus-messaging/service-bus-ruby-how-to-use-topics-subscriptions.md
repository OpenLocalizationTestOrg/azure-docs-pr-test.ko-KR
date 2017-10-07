---
title: "aaaHow toouse 서비스 버스 주제 (Ruby) | Microsoft Docs"
description: "자세한 방법을 toouse 서비스 버스 항목 및 Azure에서 구독 합니다. 코드 샘플은 Ruby 응용 프로그램용으로 작성되었습니다."
services: service-bus-messaging
documentationcenter: ruby
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 3ef2295e-7c5f-4c54-a13b-a69c8045d4b6
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 236d6495825e68e336c23e1b500d0764ee512e49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-ruby"></a>어떻게 toouse 서비스 버스 토픽 및 구독 Ruby
 
[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

이 문서에서는 설명 방법을 toouse 서비스 버스 항목 및 Ruby 응용 프로그램에서 구독 합니다. hello 가이드에서 다루는 시나리오 포함 **항목 및 구독 필터를 메시지를 보내는 구독을 만드는** tooa 항목 **구독에서 메시지를 받는**, 및  **항목 및 구독을 삭제**합니다. 항목 및 구독에 대 한 자세한 내용은 참조 hello [다음 단계](#next-steps) 섹션.

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

[!INCLUDE [service-bus-ruby-setup](../../includes/service-bus-ruby-setup.md)]

## <a name="create-a-topic"></a>토픽 만들기
hello **Azure::ServiceBusService** 개체를 사용 하면 toowork 항목과 함께 합니다. hello 다음 코드에서는 **Azure::ServiceBusService** 개체입니다. toocreate 항목을 사용 하 여 hello `create_topic()` 메서드. 다음 예제는 hello 항목을 만들거나 hello 오류가 있는 경우 출력 합니다.

```ruby
azure_service_bus_service = Azure::ServiceBus::ServiceBusService.new(sb_host, { signer: signer})
begin
  topic = azure_service_bus_service.create_queue("test-topic")
rescue
  puts $!
end
```

전달할 수도 있습니다는 **Azure::ServiceBus::Topic** 메시지 시간 toolive 또는 최대 큐 크기와 같은 toooverride 기본 항목 설정을 사용할 수 있는 추가 옵션이 포함 된 개체입니다. hello hello 최대 큐를 설정 하는 다음 예제와 size too5 GB 및 toolive too1 분 시간:

```ruby
topic = Azure::ServiceBus::Topic.new("test-topic")
topic.max_size_in_megabytes = 5120
topic.default_message_time_to_live = "PT1M"

topic = azure_service_bus_service.create_topic(topic)
```

## <a name="create-subscriptions"></a>구독 만들기
주제 구독에도 hello를 사용 하 여 만들어진 **Azure::ServiceBusService** 개체입니다. 이름이 지정 된 구독과 hello toohello 구독의 가상 큐에 배달 된 메시지 집합을 제한 하는 선택적 필터가 있을 수 있습니다.

구독 영구 tooexist 중 하나가 될 때까지 계속 사용 되며 또는 hello이 항목은 연관 된, 삭제 됩니다. 응용 프로그램 논리 toocreate 구독 있으면 hello getSubscription 메서드를 사용 하 여 hello 구독에 이미 존재 하는 경우 확인 먼저 합니다.

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a>Hello 기본 (MatchAll) 필터와 구독 만들기
hello **MatchAll** 필터는 필터 지정 하지 않으면은 새 구독을 만들 때 사용 되는 hello 기본 필터. Hello 때 **MatchAll** 필터 사용 하는 경우 모든 부분 메시지 게시 된 toohello hello 구독의 가상 큐에 배치 됩니다. hello 다음 예제에서는 "전체 메시지" 이라는 구독을 만들고 사용 하 여 기본 hello **MatchAll** 필터입니다.

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "all-messages")
```

### <a name="create-subscriptions-with-filters"></a>필터를 사용하여 구독 만들기
Toospecify tooa 항목에 특정 구독 내에서 표시 됩니다. 보낸 메시지 수 있도록 하는 필터를 정의할 수도 있습니다.

hello 가장 유연한 구독에서 지 원하는 필터 형식은 hello **Azure::ServiceBus::SqlFilter**를 구현 하는 SQL92의 하위 집합입니다. SQL 필터가 있는 게시 된 toohello 항목 hello 메시지의 hello 속성에서 작동 합니다. SQL 필터와 함께 사용할 수 있는 hello 식에 대 한 자세한 내용은 hello 검토 [SqlFilter](service-bus-messaging-sql-filter.md) 구문입니다.

Hello를 사용 하 여 필터 tooa 구독을 추가 하려면 `create_rule()` hello 방식의 **Azure::ServiceBusService** 개체입니다. 이 방법을 사용 하면 tooadd 새 필터 tooan 기존 구독이 있습니다.

Hello 기본 필터는 자동으로 적용 한 이후 tooall 새 구독을 먼저 hello 기본 필터를 제거 하거나 hello **MatchAll** 지정할 수 있는 필터를 재정의 합니다. Hello를 사용 하 여 hello 기본 규칙을 제거할 수 있습니다 `delete_rule()` 메서드 hello **Azure::ServiceBusService** 개체입니다.

hello 다음 예제에서는 구독을 만드는 "높은 메시지" 이라는 **Azure::ServiceBus::SqlFilter** 만 사용자 지정 하는 메시지를 선택 하는 `message_number` 3 보다 큰 속성:

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "high-messages")
azure_service_bus_service.delete_rule("test-topic", "high-messages", "$Default")

rule = Azure::ServiceBus::Rule.new("high-messages-rule")
rule.topic = "test-topic"
rule.subscription = "high-messages"
rule.filter = Azure::ServiceBus::SqlFilter.new({
  :sql_expression => "message_number > 3" })
rule = azure_service_bus_service.create_rule(rule)
```

마찬가지로, hello 다음 예제에서는 구독을 만드는 라는 `low-messages` 와 **Azure::ServiceBus::SqlFilter** 만 설정 된 메시지를 선택 하는 `message_number` 속성 작은 보다 짧거나 too3:

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "low-messages")
azure_service_bus_service.delete_rule("test-topic", "low-messages", "$Default")

rule = Azure::ServiceBus::Rule.new("low-messages-rule")
rule.topic = "test-topic"
rule.subscription = "low-messages"
rule.filter = Azure::ServiceBus::SqlFilter.new({
  :sql_expression => "message_number <= 3" })
rule = azure_service_bus_service.create_rule(rule)
```

메시지는 이제 보내면 너무`test-topic`, 구독 배달된 tooreceivers toohello 항상 수는 `all-messages` 항목 구독 및 구독 하는 선택적으로 배달 된 tooreceivers toohello `high-messages` 및 `low-messages` 항목 구독 ( 에 따라 hello 메시지 내용을).

## <a name="send-messages-tooa-topic"></a>Tooa 부분 메시지 보내기
메시지 tooa 서비스 버스 항목 toosend 응용 프로그램 hello를 사용 해야 `send_topic_message()` 메서드 hello **Azure::ServiceBusService** 개체입니다. 메시지가 전송 tooService 버스 주제는 hello 인스턴스의 **Azure::ServiceBus::BrokeredMessage** 개체입니다. **Azure::ServiceBus::BrokeredMessage** 개체에는 표준 속성 집합이 있습니다 (같은 `label` 및 `time_to_live`), 사용자 지정 응용 프로그램 특정 속성 사용 되는 toohold 있는 사전 및 문자열 데이터의 본문입니다. 응용 프로그램 문자열 값 toohello 전달 하 여 hello hello 메시지 본문을 설정할 수 `send_topic_message()` 메서드 및 필수 표준 속성 기본 값으로 채워집니다.

hello 다음 예제에서는 5 toosend 테스트 너무 메시지 방법을`test-topic`합니다. 해당 hello 참고 `message_number` hello 루프의 반복 hello에 각 메시지의 사용자 지정 속성 값 달라 집니다 (결정 구독 수신):

```ruby
5.times do |i|
  message = Azure::ServiceBus::BrokeredMessage.new("test message " + i,
    { :message_number => i })
  azure_service_bus_service.send_topic_message("test-topic", message)
end
```

서비스 버스 주제 hello에서 최대 메시지 크기는 256KB 지원 [표준 계층](service-bus-premium-messaging.md) 및 hello에서 1 MB [Premium 계층](service-bus-premium-messaging.md)합니다. hello 표준 및 사용자 지정 응용 프로그램 속성을 포함 하는 hello 헤더는 64KB의 최대 크기를 가질 수 있습니다. Hello 메시지에 항목을 보유할 수에 제한이 없음을 않으며 항목을 보유 하는 hello 메시지의 총 크기 hello 켜져 캡입니다. 이 토픽 크기는 생성 시 정의되며 상한이 5GB입니다.

## <a name="receive-messages-from-a-subscription"></a>구독에서 메시지 받기
Hello를 사용 하 여 구독에서 메시지를 받을 `receive_subscription_message()` 메서드 hello **Azure::ServiceBusService** 개체입니다. 기본적으로 메시지 read(peak) 되며 hello 구독에서 삭제 하지 않고 잠겨 있습니다. 읽을 수 있으며 hello 설정 하 여 hello 메시지 hello 구독에서 삭제 `peek_lock` 옵션**false**합니다.

hello 기본 동작을 사용 하면 hello 읽기 및 삭제는 2 단계 작업을 사용 하면 누락 된 메시지를 허용할 수 없는 가능한 toosupport 응용 프로그램입니다. 서비스 버스 요청을 받으면 다음 메시지 toobe hello 사용 다른 소비자가 수신할 tooprevent 잠근 하 고 toohello 응용 프로그램 반환 찾습니다. Hello hello의 두 번째 단계를 완료 hello 응용 프로그램 hello 메시지 처리를 완료 (또는 이후 처리를 위해 안정적으로 저장) 한 후 호출 하 여 수신 프로세스 `delete_subscription_message()` 메서드와 hello 메시지 toobe 삭제 매개 변수로 제공 합니다. hello `delete_subscription_message()` 메서드 hello 메시지를 사용 되 고 표시 하 고 hello 구독에서 제거 합니다.

경우 hello `:peek_lock` 매개 변수가 너무 설정 된**false**, 읽기 및 hello 가장 간단한 모델 hello 메시지를 삭제 되며 시나리오는 응용 프로그램의 hello 이벤트에서 메시지를 처리 하지 않아도 안전한 수에 가장 적합 한 오류가 발생 했습니다. toounderstand hello는 hello 소비자 문제에 요청을 수신 하는 시나리오 및 후 처리 하기 전에 크래시 합니다. 서비스 버스 사용 되는 것을 다음 hello 응용 프로그램 다시 시작 되 고 메시지 사용을 시작할 때 hello 메시지를 표시 한 됩니다, 때문에 누락 됩니다 hello 메시지 했던 이전 toohello 크래시를 사용 합니다.

hello 다음 예제에서는 메시지를 수신할 수 방법 및 처리를 사용 하 여 `receive_subscription_message()`합니다. hello 예제에서 먼저 수신 하 고 hello에서 메시지를 삭제 `low-messages` 를 사용 하 여 구독 `:peek_lock` 도**false**, hello에서 다른 메시지를 받고 다음 `high-messages` 다음 삭제 hello 메시지를 사용 하 고 `delete_subscription_message()`:

```ruby
message = azure_service_bus_service.receive_subscription_message(
  "test-topic", "low-messages", { :peek_lock => false })
message = azure_service_bus_service.receive_subscription_message(
  "test-topic", "high-messages")
azure_service_bus_service.delete_subscription_message(message)
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Toohandle 응용 프로그램이 크래시 되는 방법 및 읽을 수 없는 메시지
서비스 버스 기능 toohelp 정상적으로 응용 프로그램 또는 메시지를 처리 하는 데 문제가 오류 로부터 복구를 제공 합니다. 수신기 응용 프로그램 수 없는 경우 몇 가지 이유로 tooprocess 환영 메시지가 다음 hello 호출할 수 있는 `unlock_subscription_message()` 메서드 hello **Azure::ServiceBusService** 개체입니다. 이 인해 서비스 버스 toounlock hello hello 구독 내에서 메시지와 수신, 다시 사용할 수 있는 toobe 확인 하거나으로 hello를 많이 사용 응용 프로그램 또는 다른 소비 응용 프로그램에서 동일 합니다.

또한 hello 구독 내에서 잠긴 메시지와 관련 된 제한 시간 집합과 hello 응용 프로그램 실패 하기 전에 hello 메시지 tooprocess hello 잠금 제한 시간이 만료 (예를 들어 hello 응용 프로그램이 충돌할 경우), 서비스 버스에서 hello 메시지를 잠금 해제 한 다음 자동으로 사용할 수 있는 toobe 수신 다시 확인 합니다.

Hello hello 응용 프로그램 이벤트 충돌 hello 메시지 처리 전후에 그러나 hello 전에 `delete_subscription_message()` 메서드는 다음 다시 시작할 때 hello 메시지는 다시 전달한 toohello 응용 프로그램입니다. 이 이라고 하는데 *일단 처리 이상*; 즉, 각 메시지가 최소 한 번 처리 되지만 특정 상황 hello에 동일한 메시지를 다시 배달 될 수 있습니다. Hello 시나리오 중복 처리가 허용 되지 않는, 응용 프로그램 개발자가 추가 논리 tootheir 응용 프로그램을 toohandle 중복 메시지 배달을 추가 해야 합니다. 이 논리 자주 사용 하 여 이루어집니다 hello `message_id` 배달 시도 간에 일정 남아 있는 hello 메시지의 속성입니다.

## <a name="delete-topics-and-subscriptions"></a>토픽 및 구독 삭제
항목과 구독은 영구적이 고 명시적으로 해야 hello 통해 삭제 [Azure 포털] [ Azure portal] 또는 프로그래밍 방식으로 합니다. hello 아래 예제 toodelete hello 항목 이름을 지정 하는 방법 `test-topic`합니다.

```ruby
azure_service_bus_service.delete_topic("test-topic")
```

항목을 삭제 하면 모든 구독에 등록 된 hello 항목을 삭제 합니다. 구독을 개별적으로 삭제할 수도 있습니다. hello 다음 코드에서는 toodelete hello 구독 이름을 지정 하는 방법 `high-messages` hello에서 `test-topic` 항목:

```ruby
azure_service_bus_service.delete_subscription("test-topic", "high-messages")
```

## <a name="next-steps"></a>다음 단계
서비스 버스 항목의 hello 기본 사항 학습 한, 했으므로 이러한 링크 toolearn 자세한 수행 합니다.

* [큐, 토픽 및 구독](service-bus-queues-topics-subscriptions.md)을 참조하세요.
* [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter)에 대한 API 참조.
* Hello 방문 [Ruby 용 Azure SDK](https://github.com/Azure/azure-sdk-for-ruby) GitHub의 리포지토리 합니다.

[Azure portal]: https://portal.azure.com

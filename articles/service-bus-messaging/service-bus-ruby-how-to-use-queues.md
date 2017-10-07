---
title: "Ruby와 aaaHow toouse Azure 서비스 버스 큐 | Microsoft Docs"
description: "Azure에서 서비스 버스 toouse 큐 대기 하는 방법에 대해 알아봅니다. 코드 샘플은 Ruby로 작성되었습니다."
services: service-bus-messaging
documentationcenter: ruby
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 0a11eab2-823f-4cc7-842b-fbbe0f953751
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 7270154583f98e3372e82efbb967ea7a5acd1686
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-ruby"></a>Ruby와 toouse 서비스 버스 큐 대기 하는 방법

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

이 가이드에서는 설명 방법을 toouse 서비스 버스 큐입니다. hello 샘플 Ruby 작성 되 고 Azure 보석 hello를 사용 합니다. hello 가이드에서 다루는 시나리오 포함 **메시지 송신 및 수신 큐를 만드는**, 및 **큐 삭제**합니다. 서비스 버스 큐에 대 한 자세한 내용은 참조 hello [다음 단계](#next-steps) 섹션.

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]
   
[!INCLUDE [service-bus-ruby-setup](../../includes/service-bus-ruby-setup.md)]

## <a name="how-toocreate-a-queue"></a>어떻게 toocreate 큐
hello **Azure::ServiceBusService** 개체를 사용 하면 큐와 toowork 합니다. toocreate 큐를 사용 하 여 hello `create_queue()` 메서드. hello 다음 예제에서는 큐를 만듭니다 또는 모든 오류를 출력 합니다.

```ruby
azure_service_bus_service = Azure::ServiceBus::ServiceBusService.new(sb_host, { signer: signer})
begin
  queue = azure_service_bus_service.create_queue("test-queue")
rescue
  puts $!
end
```

전달할 수도 있습니다는 **Azure::ServiceBus::Queue** 메시지 시간 toolive 또는 최대 큐 크기 같은 toooverride hello 기본 큐 설정 수 있는 추가 옵션이 포함 된 개체입니다. 다음 예제는 hello tooset 최대 큐 크기 too5 GB hello 방법과 toolive too1 분 시간을 보여 줍니다.

```ruby
queue = Azure::ServiceBus::Queue.new("test-queue")
queue.max_size_in_megabytes = 5120
queue.default_message_time_to_live = "PT1M"

queue = azure_service_bus_service.create_queue(queue)
```

## <a name="how-toosend-messages-tooa-queue"></a>Toosend 메시지 큐가 tooa 방법
메시지 tooa 서비스 버스 큐 toosend 응용 프로그램 호출 hello `send_queue_message()` 메서드 hello **Azure::ServiceBusService** 개체입니다. 너무 (보내고 받은에서) 서비스 버스 큐는 메시지 **Azure::ServiceBus::BrokeredMessage** 개체, 및 표준 속성 집합이 있습니다 (같은 `label` 및 `time_to_live`), 사용 되는 toohold 사전 사용자 지정 응용 프로그램 관련 속성 및 임의 응용 프로그램 데이터의 본문입니다. 응용 프로그램 hello 메시지와 문자열 값을 전달 하 여 hello hello 메시지 본문을 설정할 수 있습니다 및 모든 필수 표준 속성은 기본 값으로 채워집니다.

hello 다음 예제에서는 toosend toohello 큐 테스트 메시지의 이름을 지정 방법 `test-queue` 를 사용 하 여 `send_queue_message()`:

```ruby
message = Azure::ServiceBus::BrokeredMessage.new("test queue message")
message.correlation_id = "test-correlation-id"
azure_service_bus_service.send_queue_message("test-queue", message)
```

서비스 버스 큐 최대 메시지 크기는 256KB hello 지원 [표준 계층](service-bus-premium-messaging.md) 및 hello에서 1 MB [Premium 계층](service-bus-premium-messaging.md)합니다. hello 표준 및 사용자 지정 응용 프로그램 속성을 포함 하는 hello 헤더는 64KB의 최대 크기를 가질 수 있습니다. 큐에 유지 하는 메시지의 hello 수를 제한 하지 않으며 cap hello 총 크기는 큐에서 대기 하는 hello 메시지에입니다. 이 큐 크기는 생성 시 정의되며 상한이 5GB입니다.

## <a name="how-tooreceive-messages-from-a-queue"></a>큐에서 메시지를 tooreceive 방법
Hello를 사용 하 여 큐에서 메시지가 수신 되 `receive_queue_message()` 메서드 hello **Azure::ServiceBusService** 개체입니다. 기본적으로 메시지는 읽고 hello 큐에서 삭제 되지 않고 잠겨 있습니다. 그러나에서 삭제할 수 있습니다 메시지 큐 hello hello 설정 하 여 읽어 `:peek_lock` 옵션**false**합니다.

hello 기본 동작을 사용 하면 hello 읽기 및 삭제는 2 단계 작업을 사용 하면 누락 된 메시지를 허용할 수 없는 가능한 toosupport 응용 프로그램입니다. 서비스 버스 요청을 받으면 다음 메시지 toobe hello 사용 다른 소비자가 수신할 tooprevent 잠근 하 고 toohello 응용 프로그램 반환 찾습니다. Hello hello의 두 번째 단계를 완료 hello 응용 프로그램 hello 메시지 처리를 완료 (또는 이후 처리를 위해 안정적으로 저장) 한 후 호출 하 여 수신 프로세스 `delete_queue_message()` 메서드와 hello 메시지 toobe 삭제 매개 변수로 제공 합니다. hello `delete_queue_message()` 메서드 hello 메시지를 사용 되 고 표시 하 고 hello 큐에서 제거 합니다.

경우 hello `:peek_lock` 매개 변수가 너무 설정 된**false**, 읽기 및 hello 가장 간단한 모델 hello 메시지를 삭제 되며 시나리오는 응용 프로그램의 hello 이벤트에서 메시지를 처리 하지 않아도 안전한 수에 가장 적합 한 오류가 발생 했습니다. toounderstand hello는 hello 소비자 문제에 요청을 수신 하는 시나리오 및 후 처리 하기 전에 크래시 합니다. 서비스 버스에 hello 메시지 hello 응용 프로그램 다시 시작 되 고 메시지 사용을 시작 하는 경우 사용 되는 것으로 표시 하기 때문에 누락 됩니다 hello 메시지 했던 이전 toohello 크래시를 사용 합니다.

hello 다음 예제에서는 tooreceive 및 프로세스 메시지 방법을 사용 하 여 `receive_queue_message()`합니다. hello 예제에서 먼저 수신 하 고 사용 하 여 메시지를 삭제 `:peek_lock` 도**false**다음 다른 메시지를 수신 하 고 다음 삭제 hello 메시지를 사용 하 여 `delete_queue_message()`:

```ruby
message = azure_service_bus_service.receive_queue_message("test-queue",
  { :peek_lock => false })
message = azure_service_bus_service.receive_queue_message("test-queue")
azure_service_bus_service.delete_queue_message(message)
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Toohandle 응용 프로그램이 크래시 되는 방법 및 읽을 수 없는 메시지
서비스 버스 기능 toohelp 정상적으로 응용 프로그램 또는 메시지를 처리 하는 데 문제가 오류 로부터 복구를 제공 합니다. 수신기 응용 프로그램 수 없는 경우 몇 가지 이유로 tooprocess 환영 메시지가 다음 hello 호출할 수 있는 `unlock_queue_message()` 메서드 hello **Azure::ServiceBusService** 개체입니다. 이 호출으로 인해 서비스 버스 toounlock hello hello 큐 내에서 메시지와 수신, 다시 사용할 수 있는 toobe 확인 하거나으로 hello를 많이 사용 응용 프로그램 또는 다른 소비 응용 프로그램에서 동일 합니다.

또한 hello 큐 내에서 잠긴 메시지와 관련 된 제한 시간 집합과 hello 응용 프로그램 실패 하기 전에 hello 메시지 tooprocess hello 잠금 제한 시간이 만료 (예를 들어 hello 응용 프로그램이 충돌할 경우), 서비스 버스 hello 메시지의 잠금을 해제 한 다음 자동으로 수신 다시 사용할 수 있는 toobe로 전환 합니다.

Hello hello 응용 프로그램 이벤트 충돌 hello 메시지 처리 전후에 그러나 hello 전에 `delete_queue_message()` 메서드는 다음 다시 시작할 때 hello 메시지는 다시 전달한 toohello 응용 프로그램입니다. 이 프로세스를 일반적으로 라고 *일단 처리 이상*; 즉, 각 메시지가 최소 한 번 처리 되지만 특정 상황 hello에 동일한 메시지를 다시 배달 될 수 있습니다. Hello 시나리오 중복 처리가 허용 되지 않는, 응용 프로그램 개발자가 추가 논리 tootheir 응용 프로그램을 toohandle 중복 메시지 배달을 추가 해야 합니다. 이 대개 달성 hello를 사용 하 여 `message_id` 배달 시도 간에 일정 하 게 유지 하는 hello 메시지의 속성입니다.

## <a name="next-steps"></a>다음 단계
서비스 버스 큐의 hello 기본 사항 학습 한, 했으므로 이러한 링크 toolearn 자세한 수행 합니다.

* [큐, 토픽 및 구독](service-bus-queues-topics-subscriptions.md) 개요.
* Hello 방문 [Ruby 용 Azure SDK](https://github.com/Azure/azure-sdk-for-ruby) GitHub의 리포지토리 합니다.

이 문서에서 설명 하는 hello Azure 서비스 버스 큐 및 hello에서 설명 하는 Azure 큐 간의 비교에 대 한 [어떻게 toouse Ruby에서 큐 저장소](../storage/queues/storage-ruby-how-to-use-queue-storage.md) 문서를 참조 하십시오. [Azure 큐 및 Azure 서비스 버스 큐-비교 및 대조](service-bus-azure-and-service-bus-queues-compared-contrasted.md)


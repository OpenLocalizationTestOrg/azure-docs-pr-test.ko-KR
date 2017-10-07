---
title: "python aaaHow toouse Azure 서비스 버스 큐 | Microsoft Docs"
description: "Python에서 toouse Azure 서비스 버스 큐 대기 하는 방법에 대해 알아봅니다."
services: service-bus-messaging
documentationcenter: python
author: sethmanheim
manager: timlt
editor: 
ms.assetid: b95ee5cd-3b31-459c-a7f3-cf8bcf77858b
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm;lmazuel
ms.openlocfilehash: bceb84d04ff3445c3087a9c246c583d6630f07af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-python"></a>Python toouse 서비스 버스 큐 대기 하는 방법

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

이 문서에서는 설명 방법을 toouse 서비스 버스 큐입니다. hello 샘플 Python에서 작성 되 고 hello를 사용 하 여 [Python Azure 서비스 버스 패키지][Python Azure Service Bus package]합니다. hello 가이드에서 다루는 시나리오 포함 **메시지 송신 및 수신 큐를 만드는**, 및 **큐 삭제**합니다.

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

> [!NOTE]
> Python 또는 hello tooinstall [Python Azure 서비스 버스 패키지][Python Azure Service Bus package], hello 참조 [Python 설치 가이드](../python-how-to-install.md)합니다.
> 
> 

## <a name="create-a-queue"></a>큐 만들기
hello **ServiceBusService** 개체를 사용 하면 큐와 toowork 합니다. 서비스 버스 tooprogrammatically 액세스 원하는 모든 Python 파일의 hello 맨 위 근처 코드 다음 hello를 추가 합니다.

```python
from azure.servicebus import ServiceBusService, Message, Queue
```

hello 다음 코드에서는 **ServiceBusService** 개체입니다. `mynamespace`, `sharedaccesskeyname` 및 `sharedaccesskey`를 네임스페이스, SAS(공유 액세스 서명) 키 이름 및 값으로 바꿉니다.

```python
bus_service = ServiceBusService(
    service_namespace='mynamespace',
    shared_access_key_name='sharedaccesskeyname',
    shared_access_key_value='sharedaccesskey')
```

hello hello SAS 키 이름 및 값에 대 한 값에서에서 확인할 수 있습니다 hello [Azure 포털] [ Azure portal] 연결 정보 또는 Visual Studio hello **속성** 창을 선택 하는 경우 서버 탐색기에서 서비스 버스 네임 스페이스를 hello (같이 hello 이전 섹션에서).

```python
bus_service.create_queue('taskqueue')
```

hello `create_queue` 메서드는 또한 메시지 toolive TTL (time) 또는 최대 큐 크기와 같은 toooverride 기본 큐 설정을 사용할 수 있는 추가 옵션을 지원 합니다. hello 다음 예제에서는 설정 hello 최대 큐 크기 too5 증가 하 고 hello TTL 값 too1 분:

```python
queue_options = Queue()
queue_options.max_size_in_megabytes = '5120'
queue_options.default_message_time_to_live = 'PT1M'

bus_service.create_queue('taskqueue', queue_options)
```

## <a name="send-messages-tooa-queue"></a>송신 메시지 tooa 큐
메시지 tooa 서비스 버스 큐 toosend 응용 프로그램 호출 hello `send_queue_message` 메서드 hello **ServiceBusService** 개체입니다.

hello 다음 예제에서는 toosend toohello 큐 테스트 메시지의 이름을 지정 방법 `taskqueue` 를 사용 하 여 `send_queue_message`:

```python
msg = Message(b'Test Message')
bus_service.send_queue_message('taskqueue', msg)
```

서비스 버스 큐 최대 메시지 크기는 256KB hello 지원 [표준 계층](service-bus-premium-messaging.md) 및 hello에서 1 MB [Premium 계층](service-bus-premium-messaging.md)합니다. hello 표준 및 사용자 지정 응용 프로그램 속성을 포함 하는 hello 헤더는 64KB의 최대 크기를 가질 수 있습니다. 큐에 유지 하는 메시지의 hello 수를 제한 하지 않으며 cap hello 총 크기는 큐에서 대기 하는 hello 메시지에입니다. 이 큐 크기는 생성 시 정의되며 상한이 5GB입니다. 할당량에 대한 자세한 내용은 [Service Bus 할당량][Service Bus quotas]을 참조하세요.

## <a name="receive-messages-from-a-queue"></a>큐에서 메시지 받기
Hello를 사용 하 여 큐에서 메시지가 수신 되 `receive_queue_message` 메서드 hello **ServiceBusService** 개체:

```python
msg = bus_service.receive_queue_message('taskqueue', peek_lock=False)
print(msg.body)
```

읽어 때 hello 큐에서 메시지가 삭제 되도록 hello 매개 변수 `peek_lock` 너무 설정**False**합니다. (미리 보기)를 읽을 수 있으며 hello 매개 변수를 설정 하 여 hello 큐에서 삭제 하지 않고 hello 메시지 잠금 `peek_lock` 너무**True**합니다.

읽기의 동작은 hello 및 hello의 일부 수신 작업으로 hello 메시지를 삭제 합니다.는 hello 간단한 모델 시나리오는 응용 프로그램 실패 하는 hello 이벤트의 메시지를 처리 하지 않아도 안전한 수에 가장 적합 합니다. toounderstand hello는 hello 소비자 문제에 요청을 수신 하는 시나리오 및 후 처리 하기 전에 크래시 합니다. 서비스 버스 사용 되는 것을 다음 hello 응용 프로그램 다시 시작 되 고 메시지 사용을 시작할 때 hello 메시지를 표시 한 됩니다, 때문에 누락 됩니다 hello 메시지 했던 이전 toohello 크래시를 사용 합니다.

경우 hello `peek_lock` 매개 변수가 너무 설정 된**True**, hello 수신 하므로 누락 된 메시지를 허용할 수 없는 가능한 toosupport 응용 프로그램 2 단계 작업이 됩니다. 서비스 버스 요청을 받으면 다음 메시지 toobe hello 사용 다른 소비자가 수신할 tooprevent 잠근 하 고 toohello 응용 프로그램 반환 찾습니다. Hello hello의 두 번째 단계를 완료 hello 응용 프로그램 hello 메시지 처리를 완료 (또는 이후 처리를 위해 안정적으로 저장) 한 후 hello를 호출 하 여 수신 프로세스 **삭제** 메서드 hello **메시지** 개체입니다. hello **삭제** 메서드 hello 메시지를 사용 되 고 표시 하 고 hello 큐에서 제거 합니다.

```python
msg = bus_service.receive_queue_message('taskqueue', peek_lock=True)
print(msg.body)

msg.delete()
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Toohandle 응용 프로그램이 크래시 되는 방법 및 읽을 수 없는 메시지
서비스 버스 기능 toohelp 정상적으로 응용 프로그램 또는 메시지를 처리 하는 데 문제가 오류 로부터 복구를 제공 합니다. 수신기 응용 프로그램 수 없는 경우 몇 가지 이유로 tooprocess 환영 메시지가 다음 hello 호출할 수 있는 **잠금 해제** 메서드 hello **메시지** 개체입니다. Hello 큐 내에서 서비스 버스 toounlock hello 메시지 시키며 수신 다시 사용할 수 있는 toobe 확인, 사용자가 여를 많이 사용 응용 프로그램 또는 다른 소비 응용 프로그램에서 동일한 hello 중 하나입니다.

또한 hello 큐 내에서 잠긴 메시지와 관련 된 제한 시간 집합과 tooprocess hello 메시지 하기 전에 hello 응용 프로그램 실패 hello 잠금 제한 시간이 만료 (예: hello 응용 프로그램이 충돌할 경우), 서비스 버스는 hello 메시지 잠금을 자동으로 해제 한 다음 사용할 수 있는 toobe 수신 다시 확인 합니다.

Hello hello 응용 프로그램 이벤트 충돌 hello 메시지 처리 전후에 그러나 hello 전에 **삭제** 메서드는 다음 다시 시작할 때 hello 메시지 다시 전달한 toohello 응용 프로그램 됩니다. 이 이라고 하는데 **일단 처리 이상**, 즉, 각 메시지가 최소 한 번 처리 되지만 특정 상황 hello에 동일한 메시지를 다시 배달 될 수 있습니다. Hello 시나리오 중복 처리가 허용 되지 않는, 응용 프로그램 개발자가 추가 논리 tootheir 응용 프로그램을 toohandle 중복 메시지 배달을 추가 해야 합니다. 이 대개 달성 hello를 사용 하 여 **MessageId** 배달 시도 간에 일정 남아 있는 hello 메시지의 속성입니다.

## <a name="next-steps"></a>다음 단계
서비스 버스 큐의 hello 기본 사항을 파악 했으므로, 이제는 이러한 문서 toolearn 자세한를 참조 하십시오.

* [큐, 토픽 및 구독][Queues, topics, and subscriptions]

[Azure portal]: https://portal.azure.com
[Python Azure Service Bus package]: https://pypi.python.org/pypi/azure-servicebus  
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[Service Bus quotas]: service-bus-quotas.md


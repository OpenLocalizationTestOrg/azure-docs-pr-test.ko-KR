---
title: "Python에서 큐 저장소 aaaHow toouse | Microsoft Docs"
description: "방법 toouse hello Python toocreate에서 Azure 큐 서비스 및 큐를 삭제 하 고 삽입, 및 메시지 삭제에 대해 알아봅니다."
services: storage
documentationcenter: python
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: cc0d2da2-379a-4b58-a234-8852b4e3d99d
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: ce8d999d9fafaef0dab48442560d004c034c0804
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-python"></a>어떻게 toouse Python에서 큐 저장소
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>개요
이 가이드에서는 tooperform 일반적인 시나리오를 사용 하 여 Azure 큐 저장소 서비스를 hello 하는 방법을 알아봅니다. hello 샘플 Python에서 작성 되 고 hello를 사용 하 여 [Python에 대 한 Microsoft Azure 저장소 SDK]합니다. hello 가이드에서 다루는 시나리오 포함 **삽입**, **관찰**, **가져오는**, 및 **삭제** 메시지를 큐와  **만들기 및 큐 삭제**합니다. 큐에 대 한 자세한 내용은 toohello [다음 단계] 섹션을 참조 하십시오.

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="how-to-create-a-queue"></a>큐를 만드는 방법
hello **QueueService** 개체 큐를 사용할 수 있습니다. hello 다음 코드에서는 **QueueService** 개체입니다. Hello 다음 원하는 tooprogrammatically 액세스 Azure 저장소는 모든 Python 파일의 hello 맨 위 근처에 추가 합니다.

```python
from azure.storage.queue import QueueService
```

hello 다음 코드에서는 **QueueService** hello 저장소 계정 이름 및 계정 키를 사용 하 여 개체입니다. 'myaccount' 및 'mykey'를 사용자의 계정 이름 및 키로 바꾸세요.

```python
queue_service = QueueService(account_name='myaccount', account_key='mykey')

queue_service.create_queue('taskqueue')
```

## <a name="how-to-insert-a-message-into-a-queue"></a>큐에 메시지를 삽입하는 방법
tooinsert 큐로 사용 하 여 hello 메시지 **배치\_메시지** 메서드를 새 메시지를 만들고 toohello 큐를 추가 합니다.

```python
queue_service.put_message('taskqueue', u'Hello World')
```

## <a name="how-to-peek-at-hello-next-message"></a>방법: hello 다음 메시지 피킹
Hello를 호출 하 여 hello 큐에서 제거 하지 않고 큐의 hello 앞에 hello 메시지를 피킹할 수 있습니다 **peek\_메시지** 메서드. 기본적으로 **peek\_messages**는 단일 메시지를 읽습니다.

```python
messages = queue_service.peek_messages('taskqueue')
for message in messages:
    print(message.content)
```

## <a name="how-to-dequeue-messages"></a>방법: 큐에서 메시지 제거
다음 코드는 2단계를 거쳐 큐에서 메시지를 제거합니다. 호출 하는 경우 **가져오기\_메시지**, 기본적으로 큐에 있는 다음 메시지로 hello를 얻을 수 있습니다. 반환 된 메시지 **가져오기\_메시지** 보이지 않는 tooany이이 큐에서 메시지를 읽을 다른 코드 됩니다. 기본적으로, 이 메시지는 30초간 표시되지 않습니다. toofinish 제거 hello 큐에서에서 메시지를 hello 호출 해야 **삭제\_메시지**합니다. 메시지를 제거 하는이 두 단계 과정 통해 있는 코드에 tooprocess 하드웨어나 소프트웨어 장애 때문에 메시지가 실패 하면 코드의 다른 인스턴스 수 동일한 메시지가 다시 시도 하십시오 있습니다. 코드 호출 **삭제\_메시지** 직후 hello 메시지를 처리 합니다.

```python
messages = queue_service.get_messages('taskqueue')
for message in messages:
    print(message.content)
    queue_service.delete_message('taskqueue', message.id, message.pop_receipt)
```

큐에서 메시지 검색을 사용자 지정할 수 있는 방법으로는 두 가지가 있습니다.
첫째, 일괄 처리 메시지 (위쪽 too32)을 얻을 수 있습니다. 둘째, 하면 프로그램 코드를 더 길거나 더 짧은 표시 안 함 시간 제한이 설정할 수 있습니다 또는 적은 시간 toofully 각 메시지를 처리 합니다. hello 다음 코드 예제에서는 **가져오기\_메시지** 메서드 tooget 16 메시지 한 번 호출에서 합니다. 그런 다음에 for 루프를 사용하여 각 메시지를 처리합니다. 또한 각 메시지에 대해 5 분 hello 표시 안 함 시간 제한을 설정합니다.

```python
messages = queue_service.get_messages('taskqueue', num_messages=16, visibility_timeout=5*60)
for message in messages:
    print(message.content)
    queue_service.delete_message('taskqueue', message.id, message.pop_receipt)        
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a>방법: 대기 중인 메시지의 내용을 hello 변경
메시지 전체 hello 큐에서의 hello 내용을 변경할 수 있습니다. 메시지 작업 작업을 나타내는 경우에이 기능 tooupdate hello 작업 작업의 상태를 사용할 수 있습니다. 아래 hello 코드 hello를 사용 하 여 **업데이트\_메시지** 메서드 tooupdate 메시지입니다. hello 표시 제한 시간은 too0, 즉 메시지가 즉시 표시 되 고 hello 내용을 업데이트할 때 설정 됩니다.

```python
messages = queue_service.get_messages('taskqueue')
for message in messages:
    queue_service.update_message('taskqueue', message.id, message.pop_receipt, 0, u'Hello World Again')
```

## <a name="how-to-get-hello-queue-length"></a>방법: hello 큐 길이 가져오기
큐에 있는 hello 메시지 수의 예측을 얻을 수 있습니다. **가져오기\_큐\_메타 데이터** 메서드 묻고 hello 큐에 대 한 큐 서비스 tooreturn 메타 데이터를 hello hello **approximate_message_count**합니다. 메시지를 추가 또는 큐 서비스 tooyour 요청 응답 한 후 제거 될 수 있으므로 hello 결과 대략적인만입니다.

```python
metadata = queue_service.get_queue_metadata('taskqueue')
count = metadata.approximate_message_count
```

## <a name="how-to-delete-a-queue"></a>방법: 큐 삭제
toodelete는 큐와 모든 hello 메시지에 포함 된, 호출 된 **삭제\_큐** 메서드.

```python
queue_service.delete_queue('taskqueue')
```

## <a name="next-steps"></a>다음 단계
큐 저장소의 hello 기본 사항 학습 한, 했으므로 이러한 링크 toolearn 자세한 수행 합니다.

* [Python 개발자 센터](/develop/python/)
* [Azure 저장소 서비스 REST API](http://msdn.microsoft.com/library/azure/dd179355)
* [Azure 저장소 팀 블로그]
* [Python에 대 한 Microsoft Azure 저장소 SDK]

[Azure 저장소 팀 블로그]: http://blogs.msdn.com/b/windowsazurestorage/
[Python에 대 한 Microsoft Azure 저장소 SDK]: https://github.com/Azure/azure-storage-python
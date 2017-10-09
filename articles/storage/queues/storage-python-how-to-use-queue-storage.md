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
ms.openlocfilehash: f4f902a2c314401e5c1768fbc80566c8ba25c058
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-python"></a><span data-ttu-id="131f5-103">어떻게 toouse Python에서 큐 저장소</span><span class="sxs-lookup"><span data-stu-id="131f5-103">How toouse Queue storage from Python</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="131f5-104">개요</span><span class="sxs-lookup"><span data-stu-id="131f5-104">Overview</span></span>
<span data-ttu-id="131f5-105">이 가이드에서는 tooperform 일반적인 시나리오를 사용 하 여 Azure 큐 저장소 서비스를 hello 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="131f5-105">This guide shows you how tooperform common scenarios using hello Azure Queue storage service.</span></span> <span data-ttu-id="131f5-106">hello 샘플 Python에서 작성 되 고 hello를 사용 하 여 [Python에 대 한 Microsoft Azure 저장소 SDK]합니다.</span><span class="sxs-lookup"><span data-stu-id="131f5-106">hello samples are written in Python and use hello [Microsoft Azure Storage SDK for Python].</span></span> <span data-ttu-id="131f5-107">hello 가이드에서 다루는 시나리오 포함 **삽입**, **관찰**, **가져오는**, 및 **삭제** 메시지를 큐와  **만들기 및 큐 삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="131f5-107">hello scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span> <span data-ttu-id="131f5-108">큐에 대 한 자세한 내용은 toohello [다음 단계] 섹션을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="131f5-108">For more information on queues, refer toohello [Next Steps] section.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="how-to-create-a-queue"></a><span data-ttu-id="131f5-109">큐를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="131f5-109">How To: Create a Queue</span></span>
<span data-ttu-id="131f5-110">hello **QueueService** 개체 큐를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="131f5-110">hello **QueueService** object lets you work with queues.</span></span> <span data-ttu-id="131f5-111">hello 다음 코드에서는 **QueueService** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="131f5-111">hello following code creates a **QueueService** object.</span></span> <span data-ttu-id="131f5-112">Hello 다음 원하는 tooprogrammatically 액세스 Azure 저장소는 모든 Python 파일의 hello 맨 위 근처에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="131f5-112">Add hello following near hello top of any Python file in which you wish tooprogrammatically access Azure Storage:</span></span>

```python
from azure.storage.queue import QueueService
```

<span data-ttu-id="131f5-113">hello 다음 코드에서는 **QueueService** hello 저장소 계정 이름 및 계정 키를 사용 하 여 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="131f5-113">hello following code creates a **QueueService** object using hello storage account name and account key.</span></span> <span data-ttu-id="131f5-114">'myaccount' 및 'mykey'를 사용자의 계정 이름 및 키로 바꾸세요.</span><span class="sxs-lookup"><span data-stu-id="131f5-114">Replace 'myaccount' and 'mykey' with your account name and key.</span></span>

```python
queue_service = QueueService(account_name='myaccount', account_key='mykey')

queue_service.create_queue('taskqueue')
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="131f5-115">큐에 메시지를 삽입하는 방법</span><span class="sxs-lookup"><span data-stu-id="131f5-115">How To: Insert a Message into a Queue</span></span>
<span data-ttu-id="131f5-116">tooinsert 큐로 사용 하 여 hello 메시지 **배치\_메시지** 메서드를 새 메시지를 만들고 toohello 큐를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="131f5-116">tooinsert a message into a queue, use hello **put\_message** method to create a new message and add it toohello queue.</span></span>

```python
queue_service.put_message('taskqueue', u'Hello World')
```

## <a name="how-to-peek-at-hello-next-message"></a><span data-ttu-id="131f5-117">방법: hello 다음 메시지 피킹</span><span class="sxs-lookup"><span data-stu-id="131f5-117">How To: Peek at hello Next Message</span></span>
<span data-ttu-id="131f5-118">Hello를 호출 하 여 hello 큐에서 제거 하지 않고 큐의 hello 앞에 hello 메시지를 피킹할 수 있습니다 **peek\_메시지** 메서드.</span><span class="sxs-lookup"><span data-stu-id="131f5-118">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **peek\_messages** method.</span></span> <span data-ttu-id="131f5-119">기본적으로 **peek\_messages**는 단일 메시지를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="131f5-119">By default, **peek\_messages** peeks at a single message.</span></span>

```python
messages = queue_service.peek_messages('taskqueue')
for message in messages:
    print(message.content)
```

## <a name="how-to-dequeue-messages"></a><span data-ttu-id="131f5-120">방법: 큐에서 메시지 제거</span><span class="sxs-lookup"><span data-stu-id="131f5-120">How To: Dequeue Messages</span></span>
<span data-ttu-id="131f5-121">다음 코드는 2단계를 거쳐 큐에서 메시지를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="131f5-121">Your code removes a message from a queue in two steps.</span></span> <span data-ttu-id="131f5-122">호출 하는 경우 **가져오기\_메시지**, 기본적으로 큐에 있는 다음 메시지로 hello를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="131f5-122">When you call **get\_messages**, you get hello next message in a queue by default.</span></span> <span data-ttu-id="131f5-123">반환 된 메시지 **가져오기\_메시지** 보이지 않는 tooany이이 큐에서 메시지를 읽을 다른 코드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="131f5-123">A message returned from **get\_messages** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="131f5-124">기본적으로, 이 메시지는 30초간 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="131f5-124">By default, this message stays invisible for 30 seconds.</span></span> <span data-ttu-id="131f5-125">toofinish 제거 hello 큐에서에서 메시지를 hello 호출 해야 **삭제\_메시지**합니다.</span><span class="sxs-lookup"><span data-stu-id="131f5-125">toofinish removing hello message from hello queue, you must also call **delete\_message**.</span></span> <span data-ttu-id="131f5-126">메시지를 제거 하는이 두 단계 과정 통해 있는 코드에 tooprocess 하드웨어나 소프트웨어 장애 때문에 메시지가 실패 하면 코드의 다른 인스턴스 수 동일한 메시지가 다시 시도 하십시오 있습니다.</span><span class="sxs-lookup"><span data-stu-id="131f5-126">This two-step process of removing a message assures that when your code fails tooprocess a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="131f5-127">코드 호출 **삭제\_메시지** 직후 hello 메시지를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="131f5-127">Your code calls **delete\_message** right after hello message has been processed.</span></span>

```python
messages = queue_service.get_messages('taskqueue')
for message in messages:
    print(message.content)
    queue_service.delete_message('taskqueue', message.id, message.pop_receipt)
```

<span data-ttu-id="131f5-128">큐에서 메시지 검색을 사용자 지정할 수 있는 방법으로는 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="131f5-128">There are two ways you can customize message retrieval from a queue.</span></span>
<span data-ttu-id="131f5-129">첫째, 일괄 처리 메시지 (위쪽 too32)을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="131f5-129">First, you can get a batch of messages (up too32).</span></span> <span data-ttu-id="131f5-130">둘째, 하면 프로그램 코드를 더 길거나 더 짧은 표시 안 함 시간 제한이 설정할 수 있습니다 또는 적은 시간 toofully 각 메시지를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="131f5-130">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span> <span data-ttu-id="131f5-131">hello 다음 코드 예제에서는 **가져오기\_메시지** 메서드 tooget 16 메시지 한 번 호출에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="131f5-131">hello following code example uses the **get\_messages** method tooget 16 messages in one call.</span></span> <span data-ttu-id="131f5-132">그런 다음에 for 루프를 사용하여 각 메시지를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="131f5-132">Then it processes each message using a for loop.</span></span> <span data-ttu-id="131f5-133">또한 각 메시지에 대해 5 분 hello 표시 안 함 시간 제한을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="131f5-133">It also sets hello invisibility timeout to five minutes for each message.</span></span>

```python
messages = queue_service.get_messages('taskqueue', num_messages=16, visibility_timeout=5*60)
for message in messages:
    print(message.content)
    queue_service.delete_message('taskqueue', message.id, message.pop_receipt)        
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a><span data-ttu-id="131f5-134">방법: 대기 중인 메시지의 내용을 hello 변경</span><span class="sxs-lookup"><span data-stu-id="131f5-134">How To: Change hello Contents of a Queued Message</span></span>
<span data-ttu-id="131f5-135">메시지 전체 hello 큐에서의 hello 내용을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="131f5-135">You can change hello contents of a message in-place in hello queue.</span></span> <span data-ttu-id="131f5-136">메시지 작업 작업을 나타내는 경우에이 기능 tooupdate hello 작업 작업의 상태를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="131f5-136">If the message represents a work task, you could use this feature tooupdate the status of hello work task.</span></span> <span data-ttu-id="131f5-137">아래 hello 코드 hello를 사용 하 여 **업데이트\_메시지** 메서드 tooupdate 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="131f5-137">hello code below uses hello **update\_message** method tooupdate a message.</span></span> <span data-ttu-id="131f5-138">hello 표시 제한 시간은 too0, 즉 메시지가 즉시 표시 되 고 hello 내용을 업데이트할 때 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="131f5-138">hello visibility timeout is set too0, meaning the message appears immediately and hello content is updated.</span></span>

```python
messages = queue_service.get_messages('taskqueue')
for message in messages:
    queue_service.update_message('taskqueue', message.id, message.pop_receipt, 0, u'Hello World Again')
```

## <a name="how-to-get-hello-queue-length"></a><span data-ttu-id="131f5-139">방법: hello 큐 길이 가져오기</span><span class="sxs-lookup"><span data-stu-id="131f5-139">How To: Get hello Queue Length</span></span>
<span data-ttu-id="131f5-140">큐에 있는 hello 메시지 수의 예측을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="131f5-140">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="131f5-141">**가져오기\_큐\_메타 데이터** 메서드 묻고 hello 큐에 대 한 큐 서비스 tooreturn 메타 데이터를 hello hello **approximate_message_count**합니다.</span><span class="sxs-lookup"><span data-stu-id="131f5-141">The **get\_queue\_metadata** method asks hello queue service tooreturn metadata about hello queue, and hello **approximate_message_count**.</span></span> <span data-ttu-id="131f5-142">메시지를 추가 또는 큐 서비스 tooyour 요청 응답 한 후 제거 될 수 있으므로 hello 결과 대략적인만입니다.</span><span class="sxs-lookup"><span data-stu-id="131f5-142">hello result is only approximate because messages can be added or removed after the queue service responds tooyour request.</span></span>

```python
metadata = queue_service.get_queue_metadata('taskqueue')
count = metadata.approximate_message_count
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="131f5-143">방법: 큐 삭제</span><span class="sxs-lookup"><span data-stu-id="131f5-143">How To: Delete a Queue</span></span>
<span data-ttu-id="131f5-144">toodelete는 큐와 모든 hello 메시지에 포함 된, 호출 된 **삭제\_큐** 메서드.</span><span class="sxs-lookup"><span data-stu-id="131f5-144">toodelete a queue and all hello messages contained in it, call the **delete\_queue** method.</span></span>

```python
queue_service.delete_queue('taskqueue')
```

## <a name="next-steps"></a><span data-ttu-id="131f5-145">다음 단계</span><span class="sxs-lookup"><span data-stu-id="131f5-145">Next Steps</span></span>
<span data-ttu-id="131f5-146">큐 저장소의 hello 기본 사항 학습 한, 했으므로 이러한 링크 toolearn 자세한 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="131f5-146">Now that you've learned hello basics of Queue storage, follow these links toolearn more.</span></span>

* [<span data-ttu-id="131f5-147">Python 개발자 센터</span><span class="sxs-lookup"><span data-stu-id="131f5-147">Python Developer Center</span></span>](/develop/python/)
* [<span data-ttu-id="131f5-148">Azure 저장소 서비스 REST API</span><span class="sxs-lookup"><span data-stu-id="131f5-148">Azure Storage Services REST API</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="131f5-149">[Azure 저장소 팀 블로그]</span><span class="sxs-lookup"><span data-stu-id="131f5-149">[Azure Storage Team Blog]</span></span>
* <span data-ttu-id="131f5-150">[Python에 대 한 Microsoft Azure 저장소 SDK]</span><span class="sxs-lookup"><span data-stu-id="131f5-150">[Microsoft Azure Storage SDK for Python]</span></span>

[Azure 저장소 팀 블로그]: http://blogs.msdn.com/b/windowsazurestorage/
[Python에 대 한 Microsoft Azure 저장소 SDK]: https://github.com/Azure/azure-storage-python
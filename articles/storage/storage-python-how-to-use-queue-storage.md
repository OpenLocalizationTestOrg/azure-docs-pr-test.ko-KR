---
title: "Python에서 큐 저장소를 사용하는 방법 | Microsoft Docs"
description: "Azure 큐 서비스를 사용하여 Python에서 큐를 작성 및 삭제하고 메시지를 삽입하고 가져오고 삭제하는 방법을 알아봅니다.\""
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
ms.openlocfilehash: 1ad3ba6853edda93034b84996823262cb017c71a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-queue-storage-from-python"></a><span data-ttu-id="bedda-103">Python에서 큐 저장소를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="bedda-103">How to use Queue storage from Python</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="bedda-104">개요</span><span class="sxs-lookup"><span data-stu-id="bedda-104">Overview</span></span>
<span data-ttu-id="bedda-105">이 가이드에서는 Azure 큐 저장소 서비스를 사용하여 일반 시나리오를 수행하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="bedda-105">This guide shows you how to perform common scenarios using the Azure Queue storage service.</span></span> <span data-ttu-id="bedda-106">샘플은 Python으로 작성되었으며 [Microsoft Azure Storage SDK for Python]을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bedda-106">The samples are written in Python and use the [Microsoft Azure Storage SDK for Python].</span></span> <span data-ttu-id="bedda-107">여기서 다루는 시나리오에는 **큐 만들기 및 삭제**뿐만 아니라 큐 메시지 **삽입**, **보기**, **가져오기** 및 **삭제**가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="bedda-107">The scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span> <span data-ttu-id="bedda-108">큐에 대한 자세한 내용은 [다음 단계] 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bedda-108">For more information on queues, refer to the [Next Steps] section.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="how-to-create-a-queue"></a><span data-ttu-id="bedda-109">큐를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="bedda-109">How To: Create a Queue</span></span>
<span data-ttu-id="bedda-110">**QueueService** 개체를 사용하면 큐로 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bedda-110">The **QueueService** object lets you work with queues.</span></span> <span data-ttu-id="bedda-111">다음 코드는 **QueueService** 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bedda-111">The following code creates a **QueueService** object.</span></span> <span data-ttu-id="bedda-112">프로그래밍 방식으로 Azure 저장소에 액세스하려는 Python 파일의 맨 위쪽에 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bedda-112">Add the following near the top of any Python file in which you wish to programmatically access Azure Storage:</span></span>

```python
from azure.storage.queue import QueueService
```

<span data-ttu-id="bedda-113">다음 코드는 저장소 계정 이름 및 계정 키를 사용하는 **QueueService** 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bedda-113">The following code creates a **QueueService** object using the storage account name and account key.</span></span> <span data-ttu-id="bedda-114">'myaccount' 및 'mykey'를 사용자의 계정 이름 및 키로 바꾸세요.</span><span class="sxs-lookup"><span data-stu-id="bedda-114">Replace 'myaccount' and 'mykey' with your account name and key.</span></span>

```python
queue_service = QueueService(account_name='myaccount', account_key='mykey')

queue_service.create_queue('taskqueue')
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="bedda-115">큐에 메시지를 삽입하는 방법</span><span class="sxs-lookup"><span data-stu-id="bedda-115">How To: Insert a Message into a Queue</span></span>
<span data-ttu-id="bedda-116">큐에 메시지를 삽입하려면 **put\_message** 메서드를 사용하여 새 메시지를 만들고 큐에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bedda-116">To insert a message into a queue, use the **put\_message** method to create a new message and add it to the queue.</span></span>

```python
queue_service.put_message('taskqueue', u'Hello World')
```

## <a name="how-to-peek-at-the-next-message"></a><span data-ttu-id="bedda-117">다음 메시지를 보는 방법</span><span class="sxs-lookup"><span data-stu-id="bedda-117">How To: Peek at the Next Message</span></span>
<span data-ttu-id="bedda-118">큐에서 메시지를 제거하지 않고도 **peek\_messages** 메서드를 호출하여 큐의 맨 앞에서 원하는 메시지를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bedda-118">You can peek at the message in the front of a queue without removing it from the queue by calling the **peek\_messages** method.</span></span> <span data-ttu-id="bedda-119">기본적으로 **peek\_messages**는 단일 메시지를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="bedda-119">By default, **peek\_messages** peeks at a single message.</span></span>

```python
messages = queue_service.peek_messages('taskqueue')
for message in messages:
    print(message.content)
```

## <a name="how-to-dequeue-messages"></a><span data-ttu-id="bedda-120">방법: 큐에서 메시지 제거</span><span class="sxs-lookup"><span data-stu-id="bedda-120">How To: Dequeue Messages</span></span>
<span data-ttu-id="bedda-121">다음 코드는 2단계를 거쳐 큐에서 메시지를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="bedda-121">Your code removes a message from a queue in two steps.</span></span> <span data-ttu-id="bedda-122">**get\_messages**를 호출하면 기본적으로 큐에서 다음 메시지를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="bedda-122">When you call **get\_messages**, you get the next message in a queue by default.</span></span> <span data-ttu-id="bedda-123">**get\_messages**에서 반환된 메시지는 이 큐의 메시지를 읽는 다른 코드에는 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bedda-123">A message returned from **get\_messages** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="bedda-124">기본적으로, 이 메시지는 30초간 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bedda-124">By default, this message stays invisible for 30 seconds.</span></span> <span data-ttu-id="bedda-125">큐에서 메시지 제거를 완료하려면 **delete\_message**도 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bedda-125">To finish removing the message from the queue, you must also call **delete\_message**.</span></span> <span data-ttu-id="bedda-126">메시지를 제거하는 이 2단계 프로세스는 코드가 하드웨어 또는 소프트웨어 오류로 인해 메시지를 처리하지 못하는 경우 코드의 다른 인스턴스가 동일한 메시지를 가져와서 다시 시도할 수 있도록 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="bedda-126">This two-step process of removing a message assures that when your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="bedda-127">코드는 메시지가 처리된 직후에 **delete\_message**를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="bedda-127">Your code calls **delete\_message** right after the message has been processed.</span></span>

```python
messages = queue_service.get_messages('taskqueue')
for message in messages:
    print(message.content)
    queue_service.delete_message('taskqueue', message.id, message.pop_receipt)
```

<span data-ttu-id="bedda-128">큐에서 메시지 검색을 사용자 지정할 수 있는 방법으로는 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bedda-128">There are two ways you can customize message retrieval from a queue.</span></span>
<span data-ttu-id="bedda-129">먼저, 메시지의 배치(최대 32개)를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bedda-129">First, you can get a batch of messages (up to 32).</span></span> <span data-ttu-id="bedda-130">두 번째로, 표시하지 않는 제한 시간을 더 길거나 더 짧게 설정하여 코드에서 각 메시지를 완전히 처리하는 시간을 늘리거나 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bedda-130">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span> <span data-ttu-id="bedda-131">다음 코드 예제는 **get\_messages** 메서드를 사용하여 한 번 호출에 16개의 메시지를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="bedda-131">The following code example uses the **get\_messages** method to get 16 messages in one call.</span></span> <span data-ttu-id="bedda-132">그런 다음에 for 루프를 사용하여 각 메시지를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="bedda-132">Then it processes each message using a for loop.</span></span> <span data-ttu-id="bedda-133">또한 각 메시지에 대해 표시하지 않는 제한 시간을 5분으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="bedda-133">It also sets the invisibility timeout to five minutes for each message.</span></span>

```python
messages = queue_service.get_messages('taskqueue', num_messages=16, visibility_timeout=5*60)
for message in messages:
    print(message.content)
    queue_service.delete_message('taskqueue', message.id, message.pop_receipt)        
```

## <a name="how-to-change-the-contents-of-a-queued-message"></a><span data-ttu-id="bedda-134">대기 중인 메시지의 콘텐츠 변경 방법</span><span class="sxs-lookup"><span data-stu-id="bedda-134">How To: Change the Contents of a Queued Message</span></span>
<span data-ttu-id="bedda-135">큐에 있는 메시지의 콘텐츠를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bedda-135">You can change the contents of a message in-place in the queue.</span></span> <span data-ttu-id="bedda-136">메시지가 작업을 나타내는 경우 이 기능을 사용하여 작업의 상태를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bedda-136">If the message represents a work task, you could use this feature to update the status of the work task.</span></span> <span data-ttu-id="bedda-137">아래 코드에서는 **update\_message** 메서드를 사용하여 메시지를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="bedda-137">The code below uses the **update\_message** method to update a message.</span></span> <span data-ttu-id="bedda-138">표시 제한 시간은 0으로 설정되어 있습니다.이는 메시지가 즉시 표시되고 콘텐츠가 업데이트됨을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="bedda-138">The visibility timeout is set to 0, meaning the message appears immediately and the content is updated.</span></span>

```python
messages = queue_service.get_messages('taskqueue')
for message in messages:
    queue_service.update_message('taskqueue', message.id, message.pop_receipt, 0, u'Hello World Again')
```

## <a name="how-to-get-the-queue-length"></a><span data-ttu-id="bedda-139">방법: 큐 길이 가져오기</span><span class="sxs-lookup"><span data-stu-id="bedda-139">How To: Get the Queue Length</span></span>
<span data-ttu-id="bedda-140">큐에 있는 메시지의 추정된 개수를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bedda-140">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="bedda-141">**get\_queue\_metadata** 메서드는 큐 서비스에 큐에 대한 메타데이터 및 **approximate_message_count**를 반환하도록 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="bedda-141">The **get\_queue\_metadata** method asks the queue service to return metadata about the queue, and the **approximate_message_count**.</span></span> <span data-ttu-id="bedda-142">큐 서비스가 요청에 응답한 후 메시지가 추가되거나 제거될 수 있으므로 이 결과는 근사치일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="bedda-142">The result is only approximate because messages can be added or removed after the queue service responds to your request.</span></span>

```python
metadata = queue_service.get_queue_metadata('taskqueue')
count = metadata.approximate_message_count
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="bedda-143">방법: 큐 삭제</span><span class="sxs-lookup"><span data-stu-id="bedda-143">How To: Delete a Queue</span></span>
<span data-ttu-id="bedda-144">큐 및 해당 큐의 모든 메시지를 삭제하려면 **delete\_queue** 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="bedda-144">To delete a queue and all the messages contained in it, call the **delete\_queue** method.</span></span>

```python
queue_service.delete_queue('taskqueue')
```

## <a name="next-steps"></a><span data-ttu-id="bedda-145">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bedda-145">Next Steps</span></span>
<span data-ttu-id="bedda-146">이제 큐 저장소의 기본 사항을 배웠으므로 다음 링크를 따라 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="bedda-146">Now that you've learned the basics of Queue storage, follow these links to learn more.</span></span>

* [<span data-ttu-id="bedda-147">Python 개발자 센터</span><span class="sxs-lookup"><span data-stu-id="bedda-147">Python Developer Center</span></span>](/develop/python/)
* [<span data-ttu-id="bedda-148">Azure 저장소 서비스 REST API</span><span class="sxs-lookup"><span data-stu-id="bedda-148">Azure Storage Services REST API</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="bedda-149">[Azure 저장소 팀 블로그]</span><span class="sxs-lookup"><span data-stu-id="bedda-149">[Azure Storage Team Blog]</span></span>
* <span data-ttu-id="bedda-150">[Microsoft Azure Storage SDK for Python]</span><span class="sxs-lookup"><span data-stu-id="bedda-150">[Microsoft Azure Storage SDK for Python]</span></span>

<span data-ttu-id="bedda-151">[Azure 저장소 팀 블로그]: http://blogs.msdn.com/b/windowsazurestorage/</span><span class="sxs-lookup"><span data-stu-id="bedda-151">[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/</span></span>
<span data-ttu-id="bedda-152">[Microsoft Azure Storage SDK for Python]: https://github.com/Azure/azure-storage-python</span><span class="sxs-lookup"><span data-stu-id="bedda-152">[Microsoft Azure Storage SDK for Python]: https://github.com/Azure/azure-storage-python</span></span>
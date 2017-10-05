---
title: "Ruby에서 Queue Storage를 사용하는 방법 | Microsoft Docs"
description: "Azure 큐 서비스를 사용하여 큐를 작성 및 삭제하고 메시지를 삽입하고 가져오고 삭제하는 방법을 알아봅니다. 샘플은 Ruby로 작성되었습니다."
services: storage
documentationcenter: ruby
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 59c2d81b-db9c-46ee-ade2-2f0caae6b1e6
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: b978b65bb3b717362697a41510c5b2b4d057cf1f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-queue-storage-from-ruby"></a><span data-ttu-id="1d6fe-104">Ruby에서 큐 저장소를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="1d6fe-104">How to use Queue storage from Ruby</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="1d6fe-105">개요</span><span class="sxs-lookup"><span data-stu-id="1d6fe-105">Overview</span></span>
<span data-ttu-id="1d6fe-106">이 가이드에서는 Microsoft Azure 큐 저장소 서비스를 사용하여 일반 시나리오를 수행하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6fe-106">This guide shows you how to perform common scenarios using the Microsoft Azure Queue Storage service.</span></span> <span data-ttu-id="1d6fe-107">샘플은 Ruby Azure API를 사용하여 작성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1d6fe-107">The samples are written using the Ruby Azure API.</span></span>
<span data-ttu-id="1d6fe-108">여기서 다루는 시나리오에는 **큐 만들기 및 삭제**뿐만 아니라 큐 메시지 **삽입**, **보기**, **가져오기** 및 **삭제**가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="1d6fe-108">The scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a><span data-ttu-id="1d6fe-109">Ruby 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="1d6fe-109">Create a Ruby Application</span></span>
<span data-ttu-id="1d6fe-110">Ruby 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1d6fe-110">Create a Ruby application.</span></span> <span data-ttu-id="1d6fe-111">지침은 [Azure VM의 Ruby on Rails 웹 응용 프로그램](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1d6fe-111">For instructions, see [Ruby on Rails Web application on an Azure VM](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span></span>

## <a name="configure-your-application-to-access-storage"></a><span data-ttu-id="1d6fe-112">저장소에 액세스하도록 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="1d6fe-112">Configure Your Application to Access Storage</span></span>
<span data-ttu-id="1d6fe-113">Azure 저장소를 사용하려면 저장소 REST 서비스와 통신하는 편리한 라이브러리 집합이 포함된 Ruby Azure 패키지를 다운로드하여 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6fe-113">To use Azure storage, you need to download and use the Ruby azure package, which includes a set of convenience libraries that communicate with the storage REST services.</span></span>

### <a name="use-rubygems-to-obtain-the-package"></a><span data-ttu-id="1d6fe-114">RubyGems를 사용하여 패키지 가져오기</span><span class="sxs-lookup"><span data-stu-id="1d6fe-114">Use RubyGems to obtain the package</span></span>
1. <span data-ttu-id="1d6fe-115">**PowerShell**(Windows), **Terminal**(Mac) 또는 **Bash**(Unix)와 같은 명령줄 인터페이스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6fe-115">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="1d6fe-116">명령 창에 "gem install azure"를 입력하여 gem 및 종속성을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6fe-116">Type "gem install azure" in the command window to install the gem and dependencies.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="1d6fe-117">패키지 가져오기</span><span class="sxs-lookup"><span data-stu-id="1d6fe-117">Import the package</span></span>
<span data-ttu-id="1d6fe-118">원하는 텍스트 편집기를 사용하여 저장소를 사용하려는 Ruby 파일의 맨 위에 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6fe-118">Use your favorite text editor, add the following to the top of the Ruby file where you intend to use storage:</span></span>

```ruby
require "azure"
```

## <a name="setup-an-azure-storage-connection"></a><span data-ttu-id="1d6fe-119">Azure 저장소 연결 설정</span><span class="sxs-lookup"><span data-stu-id="1d6fe-119">Setup an Azure Storage Connection</span></span>
<span data-ttu-id="1d6fe-120">Azure 모듈은 **AZURE\_STORAGE\_ACCOUNT** 및 **AZURE\_STORAGE\_ACCESS_KEY** 환경 변수를 읽고 Azure Storage 계정에 연결하는 데 필요한 정보를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6fe-120">The azure module will read the environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS_KEY** for information required to connect to your Azure storage account.</span></span> <span data-ttu-id="1d6fe-121">이러한 환경 변수가 설정되지 않으면 **Azure::QueueService** 를 사용하기 전에 다음 코드로 계정 정보를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6fe-121">If these environment variables are not set, you must specify the account information before using **Azure::QueueService** with the following code:</span></span>

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your Azure storage access key>"
```

<span data-ttu-id="1d6fe-122">Azure 포털의 클래식 또는 Resource Manager 저장소 계정에서 이러한 값을 가져오려면</span><span class="sxs-lookup"><span data-stu-id="1d6fe-122">To obtain these values from a classic or Resource Manager storage account in the Azure portal:</span></span>

1. <span data-ttu-id="1d6fe-123">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6fe-123">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="1d6fe-124">사용하려는 저장소 계정으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6fe-124">Navigate to the storage account you want to use.</span></span>
3. <span data-ttu-id="1d6fe-125">오른쪽의 설정 블레이드에서 **액세스 키**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6fe-125">In the Settings blade on the right, click **Access Keys**.</span></span>
4. <span data-ttu-id="1d6fe-126">나타나는 액세스 키 블레이드에 액세스 키 1 및 액세스 키 2가 표시되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d6fe-126">In the Access keys blade that appears, you'll see the access key 1 and access key 2.</span></span> <span data-ttu-id="1d6fe-127">이 둘 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d6fe-127">You can use either of these.</span></span> 
5. <span data-ttu-id="1d6fe-128">복사 아이콘을 클릭하여 키를 클립보드에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6fe-128">Click the copy icon to copy the key to the clipboard.</span></span> 

<span data-ttu-id="1d6fe-129">클래식 Azure 포털의 클래식 저장소 계정에서 이러한 값을 가져오려면</span><span class="sxs-lookup"><span data-stu-id="1d6fe-129">To obtain these values from a classic storage account in the classic Azure portal:</span></span>

1. <span data-ttu-id="1d6fe-130">[클래식 Azure 포털](https://manage.windowsazure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6fe-130">Log in to the [classic Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="1d6fe-131">사용하려는 저장소 계정으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6fe-131">Navigate to the storage account you want to use.</span></span>
3. <span data-ttu-id="1d6fe-132">탐색 창 아래쪽에서 **액세스 키 관리** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6fe-132">Click **MANAGE ACCESS KEYS** at the bottom of the navigation pane.</span></span>
4. <span data-ttu-id="1d6fe-133">팝업 대화 상자에 저장소 계정 이름, 기본 액세스 키 및 보조 액세스 키가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1d6fe-133">In the pop up dialog, you'll see the storage account name, primary access key and secondary access key.</span></span> <span data-ttu-id="1d6fe-134">액세스 키의 경우 기본 액세스 키 또는 보조 액세스 키를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d6fe-134">For access key, you can use either the primary one or the secondary one.</span></span> 
5. <span data-ttu-id="1d6fe-135">복사 아이콘을 클릭하여 키를 클립보드에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6fe-135">Click the copy icon to copy the key to the clipboard.</span></span>

## <a name="how-to-create-a-queue"></a><span data-ttu-id="1d6fe-136">큐를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="1d6fe-136">How To: Create a Queue</span></span>
<span data-ttu-id="1d6fe-137">다음 코드는 **Azure::QueueService** 개체를 만들어 큐 작업을 수행할 수 있게 해 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1d6fe-137">The following code creates a **Azure::QueueService** object, which enables you to work with queues.</span></span>

```ruby
azure_queue_service = Azure::QueueService.new
```

<span data-ttu-id="1d6fe-138">**create_queue()** 메서드를 사용하여 지정된 이름이 있는 큐를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1d6fe-138">Use the **create_queue()** method to create a queue with the specified name.</span></span>

```ruby
begin
  azure_queue_service.create_queue("test-queue")
rescue
  puts $!
end
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="1d6fe-139">큐에 메시지를 삽입하는 방법</span><span class="sxs-lookup"><span data-stu-id="1d6fe-139">How To: Insert a Message into a Queue</span></span>
<span data-ttu-id="1d6fe-140">큐에 메시지를 삽입하려면 **create_message()** 메서드를 사용하여 새 메시지를 만들고 이 메시지를 큐에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6fe-140">To insert a message into a queue, use the **create_message()** method to create a new message and add it to the queue.</span></span>

```ruby
azure_queue_service.create_message("test-queue", "test message")
```

## <a name="how-to-peek-at-the-next-message"></a><span data-ttu-id="1d6fe-141">다음 메시지를 보는 방법</span><span class="sxs-lookup"><span data-stu-id="1d6fe-141">How To: Peek at the Next Message</span></span>
<span data-ttu-id="1d6fe-142">큐에서 메시지를 제거하지 않고도 **peek\_messages()** 메서드를 호출하여 큐의 맨 앞에서 원하는 메시지를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d6fe-142">You can peek at the message in the front of a queue without removing it from the queue by calling the **peek\_messages()** method.</span></span> <span data-ttu-id="1d6fe-143">기본적으로 **peek\_messages()**는 단일 메시지를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="1d6fe-143">By default, **peek\_messages()** peeks at a single message.</span></span> <span data-ttu-id="1d6fe-144">보려는 메시지의 수를 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d6fe-144">You can also specify how many messages you want to peek.</span></span>

```ruby
result = azure_queue_service.peek_messages("test-queue",
  {:number_of_messages => 10})
```

## <a name="how-to-dequeue-the-next-message"></a><span data-ttu-id="1d6fe-145">큐에서 다음 메시지를 제거하는 방법</span><span class="sxs-lookup"><span data-stu-id="1d6fe-145">How To: Dequeue the Next Message</span></span>
<span data-ttu-id="1d6fe-146">2단계를 거쳐 큐에서 메시지를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d6fe-146">You can remove a message from a queue in two steps.</span></span>

1. <span data-ttu-id="1d6fe-147">**list\_messages()**를 호출하면 기본적으로 큐에서 다음 메시지를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1d6fe-147">When you call **list\_messages()**, you get the next message in a queue by default.</span></span> <span data-ttu-id="1d6fe-148">가져오려는 메시지의 수를 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d6fe-148">You can also specify how many messages you want to get.</span></span> <span data-ttu-id="1d6fe-149">**list\_messages()**에서 반환된 메시지는 이 큐의 메시지를 읽는 다른 코드에는 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1d6fe-149">The messages returned from **list\_messages()** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="1d6fe-150">표시 제한 시간(초 단위)을 매개 변수로 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6fe-150">You pass in the visibility timeout in seconds as a parameter.</span></span>
2. <span data-ttu-id="1d6fe-151">큐에서 메시지 제거를 완료하려면 **delete_message()**도 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6fe-151">To finish removing the message from the queue, you must also call **delete_message()**.</span></span>

<span data-ttu-id="1d6fe-152">메시지를 제거하는 이 2단계 프로세스는 코드가 하드웨어 또는 소프트웨어 오류로 인해 메시지를 처리하지 못하는 경우 코드의 다른 인스턴스가 동일한 메시지를 가져와서 다시 시도할 수 있도록 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6fe-152">This two-step process of removing a message assures that when your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="1d6fe-153">코드는 메시지가 처리된 직후에 **delete\_message()**를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6fe-153">Your code calls **delete\_message()** right after the message has been processed.</span></span>

```ruby
messages = azure_queue_service.list_messages("test-queue", 30)
azure_queue_service.delete_message("test-queue", 
  messages[0].id, messages[0].pop_receipt)
```

## <a name="how-to-change-the-contents-of-a-queued-message"></a><span data-ttu-id="1d6fe-154">대기 중인 메시지의 콘텐츠 변경 방법</span><span class="sxs-lookup"><span data-stu-id="1d6fe-154">How To: Change the Contents of a Queued Message</span></span>
<span data-ttu-id="1d6fe-155">큐에 있는 메시지의 콘텐츠를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d6fe-155">You can change the contents of a message in-place in the queue.</span></span> <span data-ttu-id="1d6fe-156">아래 코드는 **update_message()** 메서드를 사용하여 메시지를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6fe-156">The code below uses the **update_message()** method to update a message.</span></span> <span data-ttu-id="1d6fe-157">이 메서드는 큐 메시지의 pop 확인 및 메시지가 큐에 표시되는 시간을 나타내는 UTC 날짜 시간 값이 포함된 튜플을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6fe-157">The method will return a tuple which contains the pop receipt of the queue message and a UTC date time value that represents when the message will be visible on the queue.</span></span>

```ruby
message = azure_queue_service.list_messages("test-queue", 30)
pop_receipt, time_next_visible = azure_queue_service.update_message(
  "test-queue", message.id, message.pop_receipt, "updated test message", 
  30)
```

## <a name="how-to-additional-options-for-dequeuing-messages"></a><span data-ttu-id="1d6fe-158">dequeuing 메시지의 추가옵션을 설정하는 방법</span><span class="sxs-lookup"><span data-stu-id="1d6fe-158">How To: Additional Options for Dequeuing Messages</span></span>
<span data-ttu-id="1d6fe-159">큐에서 메시지 검색을 사용자 지정할 수 있는 방법으로는 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d6fe-159">There are two ways you can customize message retrieval from a queue.</span></span>

1. <span data-ttu-id="1d6fe-160">메시지의 배치를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d6fe-160">You can get a batch of message.</span></span>
2. <span data-ttu-id="1d6fe-161">표시하지 않는 제한 시간을 더 길거나 더 짧게 설정하여 코드에서 각 메시지를 완전히 처리하는 시간을 늘리거나 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d6fe-161">You can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span>

<span data-ttu-id="1d6fe-162">다음 코드 예제는 **list\_messages()** 메서드를 사용하여 한 번 호출에서 15개의 메시지를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1d6fe-162">The following code example uses the **list\_messages()** method to get 15 messages in one call.</span></span> <span data-ttu-id="1d6fe-163">그런 다음 각 메시지를 인쇄하고 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6fe-163">Then it prints and deletes each message.</span></span> <span data-ttu-id="1d6fe-164">또한 각 메시지에 대해 표시하지 않는 제한 시간을 5분으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6fe-164">It also sets the invisibility timeout to five minutes for each message.</span></span>

```ruby
azure_queue_service.list_messages("test-queue", 300
  {:number_of_messages => 15}).each do |m|
  puts m.message_text
  azure_queue_service.delete_message("test-queue", m.id, m.pop_receipt)
end
```

## <a name="how-to-get-the-queue-length"></a><span data-ttu-id="1d6fe-165">방법: 큐 길이 가져오기</span><span class="sxs-lookup"><span data-stu-id="1d6fe-165">How To: Get the Queue Length</span></span>
<span data-ttu-id="1d6fe-166">큐에 있는 메시지의 추정된 개수를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d6fe-166">You can get an estimation of the number of messages in the queue.</span></span> <span data-ttu-id="1d6fe-167">**get\_queue\_metadata()** 메서드는 큐 서비스에 대략적인 메시지 개수 및 큐에 대한 메타데이터를 반환하도록 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6fe-167">The **get\_queue\_metadata()** method asks the queue service to return the approximate message count and metadata about the queue.</span></span>

```ruby
message_count, metadata = azure_queue_service.get_queue_metadata(
  "test-queue")
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="1d6fe-168">방법: 큐 삭제</span><span class="sxs-lookup"><span data-stu-id="1d6fe-168">How To: Delete a Queue</span></span>
<span data-ttu-id="1d6fe-169">큐 및 해당 큐의 모든 메시지를 삭제하려면 큐 개체의 **delete\_queue()** 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="1d6fe-169">To delete a queue and all the messages contained in it, call the **delete\_queue()** method on the queue object.</span></span>

```ruby
azure_queue_service.delete_queue("test-queue")
```

## <a name="next-steps"></a><span data-ttu-id="1d6fe-170">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1d6fe-170">Next Steps</span></span>
<span data-ttu-id="1d6fe-171">이제 큐 저장소의 기본 사항을 배웠으므로 다음 링크를 따라 좀 더 복잡한 저장소 작업에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="1d6fe-171">Now that you've learned the basics of queue storage, follow these links to learn about more complex storage tasks.</span></span>

* <span data-ttu-id="1d6fe-172">[Azure 저장소 팀 블로그](http://blogs.msdn.com/b/windowsazurestorage/)</span><span class="sxs-lookup"><span data-stu-id="1d6fe-172">Visit the [Azure Storage Team Blog](http://blogs.msdn.com/b/windowsazurestorage/)</span></span>
* <span data-ttu-id="1d6fe-173">GitHub에서 [Azure SDK for Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) (영문) 리포지토리를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="1d6fe-173">Visit the [Azure SDK for Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span></span>

<span data-ttu-id="1d6fe-174">이 항목에서 다룬 Azure 큐 서비스와 [Service Bus 큐를 사용하는 방법](/develop/ruby/how-to-guides/service-bus-queues/) 항목에서 다루는 Azure Service Bus 큐를 비교하려면 [Azure Queues 및 Service Bus 큐 - 비교 및 대조](../service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1d6fe-174">For a comparison between the Azure Queue Service discussed in this article and Azure Service Bus Queues discussed in the [How to use Service Bus Queues](/develop/ruby/how-to-guides/service-bus-queues/) article, see [Azure Queues and Service Bus Queues - Compared and Contrasted](../service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted.md)</span></span>
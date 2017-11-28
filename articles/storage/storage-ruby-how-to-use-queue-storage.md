---
title: "aaaHow toouse Ruby에서 큐 저장소 | Microsoft Docs"
description: "방법 toouse hello Azure 큐 서비스 toocreate 및 큐 삭제 및 삽입, 및 메시지 삭제에 대해 알아봅니다. 샘플은 Ruby로 작성되었습니다."
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
ms.openlocfilehash: 726c7d2f08b2d5938ee5f9dcdc2735e447388856
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-ruby"></a><span data-ttu-id="f5b54-104">어떻게 toouse Ruby에서 큐 저장소</span><span class="sxs-lookup"><span data-stu-id="f5b54-104">How toouse Queue storage from Ruby</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="f5b54-105">개요</span><span class="sxs-lookup"><span data-stu-id="f5b54-105">Overview</span></span>
<span data-ttu-id="f5b54-106">이 가이드에서는 tooperform 일반적인 시나리오를 사용 하 여 Microsoft Azure 큐 저장소 서비스를 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f5b54-106">This guide shows you how tooperform common scenarios using hello Microsoft Azure Queue Storage service.</span></span> <span data-ttu-id="f5b54-107">hello 샘플 hello Ruby Azure API를 사용 하 여 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5b54-107">hello samples are written using hello Ruby Azure API.</span></span>
<span data-ttu-id="f5b54-108">hello 가이드에서 다루는 시나리오 포함 **삽입**, **관찰**, **가져오는**, 및 **삭제** 메시지를 큐와  **만들기 및 큐 삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b54-108">hello scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a><span data-ttu-id="f5b54-109">Ruby 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="f5b54-109">Create a Ruby Application</span></span>
<span data-ttu-id="f5b54-110">Ruby 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f5b54-110">Create a Ruby application.</span></span> <span data-ttu-id="f5b54-111">지침은 [Azure VM의 Ruby on Rails 웹 응용 프로그램](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f5b54-111">For instructions, see [Ruby on Rails Web application on an Azure VM](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span></span>

## <a name="configure-your-application-tooaccess-storage"></a><span data-ttu-id="f5b54-112">응용 프로그램 tooAccess 저장소 구성</span><span class="sxs-lookup"><span data-stu-id="f5b54-112">Configure Your Application tooAccess Storage</span></span>
<span data-ttu-id="f5b54-113">Azure 저장소 toouse toodownload 및 사용 하 여 hello hello 저장소 REST 서비스와 통신 하는 편리한 라이브러리의 집합을 포함 하는 Ruby azure 패키지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b54-113">toouse Azure storage, you need toodownload and use hello Ruby azure package, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-rubygems-tooobtain-hello-package"></a><span data-ttu-id="f5b54-114">RubyGems tooobtain hello 패키지 사용</span><span class="sxs-lookup"><span data-stu-id="f5b54-114">Use RubyGems tooobtain hello package</span></span>
1. <span data-ttu-id="f5b54-115">**PowerShell**(Windows), **Terminal**(Mac) 또는 **Bash**(Unix)와 같은 명령줄 인터페이스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b54-115">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="f5b54-116">"보석" 설치 azure의 hello 명령 창 tooinstall hello 보석 및 종속성을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b54-116">Type "gem install azure" in hello command window tooinstall hello gem and dependencies.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="f5b54-117">Hello 패키지 가져오기</span><span class="sxs-lookup"><span data-stu-id="f5b54-117">Import hello package</span></span>
<span data-ttu-id="f5b54-118">원하는 텍스트 편집기를 사용 하 여 hello toohello hello toouse 저장소 이점을 얻을 수 Ruby 파일 맨 뒤를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b54-118">Use your favorite text editor, add hello following toohello top of hello Ruby file where you intend toouse storage:</span></span>

```ruby
require "azure"
```

## <a name="setup-an-azure-storage-connection"></a><span data-ttu-id="f5b54-119">Azure 저장소 연결 설정</span><span class="sxs-lookup"><span data-stu-id="f5b54-119">Setup an Azure Storage Connection</span></span>
<span data-ttu-id="f5b54-120">hello azure 모듈 hello 환경 변수는 읽기 **AZURE\_저장소\_계정** 및 **AZURE\_저장소\_ACCESS_KEY** 에 대 한 정보는 tooconnect tooyour Azure 저장소 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b54-120">hello azure module will read hello environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS_KEY** for information required tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="f5b54-121">사용 하기 전에 hello 계정 정보를 지정 해야 이러한 환경 변수가 설정 되지 않은 경우 **Azure::QueueService** 코드 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="f5b54-121">If these environment variables are not set, you must specify hello account information before using **Azure::QueueService** with hello following code:</span></span>

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your Azure storage access key>"
```

<span data-ttu-id="f5b54-122">tooobtain hello Azure 포털에서에서 기존 또는 리소스 관리자 저장소에서 이러한 값 계정:</span><span class="sxs-lookup"><span data-stu-id="f5b54-122">tooobtain these values from a classic or Resource Manager storage account in hello Azure portal:</span></span>

1. <span data-ttu-id="f5b54-123">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b54-123">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f5b54-124">Toouse 사용할 toohello 저장소 계정을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b54-124">Navigate toohello storage account you want toouse.</span></span>
3. <span data-ttu-id="f5b54-125">Hello 오른쪽에 hello 설정 블레이드에서 클릭 **선택 키**합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b54-125">In hello Settings blade on hello right, click **Access Keys**.</span></span>
4. <span data-ttu-id="f5b54-126">나타나는 hello 액세스 키 블레이드에서 hello 선택 키 1 및 2 선택 키 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5b54-126">In hello Access keys blade that appears, you'll see hello access key 1 and access key 2.</span></span> <span data-ttu-id="f5b54-127">이 둘 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5b54-127">You can use either of these.</span></span> 
5. <span data-ttu-id="f5b54-128">Hello 아이콘 toocopy hello 키 toohello 클립보드로 복사를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b54-128">Click hello copy icon toocopy hello key toohello clipboard.</span></span> 

<span data-ttu-id="f5b54-129">tooobtain 클래식 저장소에서 이러한 값 hello 클래식 Azure 포털의 계정:</span><span class="sxs-lookup"><span data-stu-id="f5b54-129">tooobtain these values from a classic storage account in hello classic Azure portal:</span></span>

1. <span data-ttu-id="f5b54-130">Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b54-130">Log in toohello [classic Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="f5b54-131">Toouse 사용할 toohello 저장소 계정을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b54-131">Navigate toohello storage account you want toouse.</span></span>
3. <span data-ttu-id="f5b54-132">클릭 **액세스 키 관리** hello hello 탐색 창 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5b54-132">Click **MANAGE ACCESS KEYS** at hello bottom of hello navigation pane.</span></span>
4. <span data-ttu-id="f5b54-133">팝업 대화 상자 창이 hello, hello 저장소 계정 이름, 기본 액세스 키 및 보조 액세스 키를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5b54-133">In hello pop up dialog, you'll see hello storage account name, primary access key and secondary access key.</span></span> <span data-ttu-id="f5b54-134">선택 키에 대 한 hello 기본 또는 보조 로케이터로 hello 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5b54-134">For access key, you can use either hello primary one or hello secondary one.</span></span> 
5. <span data-ttu-id="f5b54-135">Hello 아이콘 toocopy hello 키 toohello 클립보드로 복사를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b54-135">Click hello copy icon toocopy hello key toohello clipboard.</span></span>

## <a name="how-to-create-a-queue"></a><span data-ttu-id="f5b54-136">큐를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="f5b54-136">How To: Create a Queue</span></span>
<span data-ttu-id="f5b54-137">hello 다음 코드에서는 **Azure::QueueService** toowork 큐로 사용할 수 있는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="f5b54-137">hello following code creates a **Azure::QueueService** object, which enables you toowork with queues.</span></span>

```ruby
azure_queue_service = Azure::QueueService.new
```

<span data-ttu-id="f5b54-138">사용 하 여 hello **create_queue()** 메서드 toocreate hello로 큐 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b54-138">Use hello **create_queue()** method toocreate a queue with hello specified name.</span></span>

```ruby
begin
  azure_queue_service.create_queue("test-queue")
rescue
  puts $!
end
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="f5b54-139">큐에 메시지를 삽입하는 방법</span><span class="sxs-lookup"><span data-stu-id="f5b54-139">How To: Insert a Message into a Queue</span></span>
<span data-ttu-id="f5b54-140">메시지 큐를 사용 하 여 hello에 tooinsert **create_message()** 메서드 toocreate 새 메시지 toohello 큐에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b54-140">tooinsert a message into a queue, use hello **create_message()** method toocreate a new message and add it toohello queue.</span></span>

```ruby
azure_queue_service.create_message("test-queue", "test message")
```

## <a name="how-to-peek-at-hello-next-message"></a><span data-ttu-id="f5b54-141">방법: hello 다음 메시지 피킹</span><span class="sxs-lookup"><span data-stu-id="f5b54-141">How To: Peek at hello Next Message</span></span>
<span data-ttu-id="f5b54-142">Hello를 호출 하 여 hello 큐에서 제거 하지 않고 큐의 hello 앞에 hello 메시지를 피킹할 수 있습니다 **peek\_messages()** 메서드.</span><span class="sxs-lookup"><span data-stu-id="f5b54-142">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **peek\_messages()** method.</span></span> <span data-ttu-id="f5b54-143">기본적으로 **peek\_messages()**는 단일 메시지를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="f5b54-143">By default, **peek\_messages()** peeks at a single message.</span></span> <span data-ttu-id="f5b54-144">메시지 수를 지정할 수도 있습니다 toopeek 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b54-144">You can also specify how many messages you want toopeek.</span></span>

```ruby
result = azure_queue_service.peek_messages("test-queue",
  {:number_of_messages => 10})
```

## <a name="how-to-dequeue-hello-next-message"></a><span data-ttu-id="f5b54-145">방법: hello 다음 메시지 큐에서 제거</span><span class="sxs-lookup"><span data-stu-id="f5b54-145">How To: Dequeue hello Next Message</span></span>
<span data-ttu-id="f5b54-146">2단계를 거쳐 큐에서 메시지를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5b54-146">You can remove a message from a queue in two steps.</span></span>

1. <span data-ttu-id="f5b54-147">호출 하는 경우 **목록\_messages()**, 기본적으로 큐에 있는 다음 메시지로 hello를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5b54-147">When you call **list\_messages()**, you get hello next message in a queue by default.</span></span> <span data-ttu-id="f5b54-148">메시지 수를 지정할 수도 있습니다 tooget 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b54-148">You can also specify how many messages you want tooget.</span></span> <span data-ttu-id="f5b54-149">반환 된 메시지 hello **목록\_messages()** 보이지 않는 tooany이이 큐에서 메시지를 읽을 다른 코드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5b54-149">hello messages returned from **list\_messages()** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="f5b54-150">매개 변수로 초 hello 표시 제한 시간에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b54-150">You pass in hello visibility timeout in seconds as a parameter.</span></span>
2. <span data-ttu-id="f5b54-151">toofinish 제거 hello 큐에서에서 메시지를 hello 호출 해야 **delete_message()**합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b54-151">toofinish removing hello message from hello queue, you must also call **delete_message()**.</span></span>

<span data-ttu-id="f5b54-152">이러한 2 단계 프로세스의 메시지를 제거 되었는지를 확인 다시 toohardware 또는 소프트웨어 오류가, 코드의 다른 인스턴스는 메시지를 가져올 수 하 여 코드 실패 tooprocess hello 같은 메시지와 시도 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="f5b54-152">This two-step process of removing a message assures that when your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="f5b54-153">코드 호출 **삭제\_message()** 직후 hello 메시지를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b54-153">Your code calls **delete\_message()** right after hello message has been processed.</span></span>

```ruby
messages = azure_queue_service.list_messages("test-queue", 30)
azure_queue_service.delete_message("test-queue", 
  messages[0].id, messages[0].pop_receipt)
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a><span data-ttu-id="f5b54-154">방법: 대기 중인 메시지의 내용을 hello 변경</span><span class="sxs-lookup"><span data-stu-id="f5b54-154">How To: Change hello Contents of a Queued Message</span></span>
<span data-ttu-id="f5b54-155">메시지 전체 hello 큐에서의 hello 내용을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5b54-155">You can change hello contents of a message in-place in hello queue.</span></span> <span data-ttu-id="f5b54-156">아래 hello 코드 hello를 사용 하 여 **update_message()** 메서드 tooupdate 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="f5b54-156">hello code below uses hello **update_message()** method tooupdate a message.</span></span> <span data-ttu-id="f5b54-157">hello 메서드 hello 큐 메시지의 popreceipt hello 포함 된 튜플 및 hello 메시지가 hello 큐에 표시 될 때를 나타내는 UTC 날짜 시간 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b54-157">hello method will return a tuple which contains hello pop receipt of hello queue message and a UTC date time value that represents when hello message will be visible on hello queue.</span></span>

```ruby
message = azure_queue_service.list_messages("test-queue", 30)
pop_receipt, time_next_visible = azure_queue_service.update_message(
  "test-queue", message.id, message.pop_receipt, "updated test message", 
  30)
```

## <a name="how-to-additional-options-for-dequeuing-messages"></a><span data-ttu-id="f5b54-158">dequeuing 메시지의 추가옵션을 설정하는 방법</span><span class="sxs-lookup"><span data-stu-id="f5b54-158">How To: Additional Options for Dequeuing Messages</span></span>
<span data-ttu-id="f5b54-159">큐에서 메시지 검색을 사용자 지정할 수 있는 방법으로는 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5b54-159">There are two ways you can customize message retrieval from a queue.</span></span>

1. <span data-ttu-id="f5b54-160">메시지의 배치를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5b54-160">You can get a batch of message.</span></span>
2. <span data-ttu-id="f5b54-161">각 메시지를 처리 하는 작은 시간 toofully 또는 코드를 자세히 허용 더 길거나 더 짧은 표시 안 함 시간 제한이 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5b54-161">You can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span>

<span data-ttu-id="f5b54-162">hello 다음 코드 예제에서는 hello **목록\_messages()** 메서드 tooget 15 메시지 한 번 호출에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b54-162">hello following code example uses hello **list\_messages()** method tooget 15 messages in one call.</span></span> <span data-ttu-id="f5b54-163">그런 다음 각 메시지를 인쇄하고 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b54-163">Then it prints and deletes each message.</span></span> <span data-ttu-id="f5b54-164">또한 각 메시지에 대 한 hello 표시 안 함 시간 초과 toofive 분을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b54-164">It also sets hello invisibility timeout toofive minutes for each message.</span></span>

```ruby
azure_queue_service.list_messages("test-queue", 300
  {:number_of_messages => 15}).each do |m|
  puts m.message_text
  azure_queue_service.delete_message("test-queue", m.id, m.pop_receipt)
end
```

## <a name="how-to-get-hello-queue-length"></a><span data-ttu-id="f5b54-165">방법: hello 큐 길이 가져오기</span><span class="sxs-lookup"><span data-stu-id="f5b54-165">How To: Get hello Queue Length</span></span>
<span data-ttu-id="f5b54-166">Hello 큐에 메시지 hello 수의 예측을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5b54-166">You can get an estimation of hello number of messages in hello queue.</span></span> <span data-ttu-id="f5b54-167">hello **가져오기\_큐\_metadata()** 메서드 hello 큐에 대 한 hello 큐 서비스 tooreturn hello 대략적인 메시지 수 및 메타 데이터를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b54-167">hello **get\_queue\_metadata()** method asks hello queue service tooreturn hello approximate message count and metadata about hello queue.</span></span>

```ruby
message_count, metadata = azure_queue_service.get_queue_metadata(
  "test-queue")
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="f5b54-168">방법: 큐 삭제</span><span class="sxs-lookup"><span data-stu-id="f5b54-168">How To: Delete a Queue</span></span>
<span data-ttu-id="f5b54-169">toodelete는 큐와 모든 hello 메시지에 포함 된, 호출 hello **삭제\_queue ()** hello 큐 개체에서 메서드.</span><span class="sxs-lookup"><span data-stu-id="f5b54-169">toodelete a queue and all hello messages contained in it, call hello **delete\_queue()** method on hello queue object.</span></span>

```ruby
azure_queue_service.delete_queue("test-queue")
```

## <a name="next-steps"></a><span data-ttu-id="f5b54-170">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f5b54-170">Next Steps</span></span>
<span data-ttu-id="f5b54-171">큐 저장소의 hello 기본 사항 학습 한, 했으므로 더 복잡 한 저장소 작업에 대 한 이러한 링크 toolearn을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="f5b54-171">Now that you've learned hello basics of queue storage, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="f5b54-172">Hello 방문 [Azure 저장소 팀 블로그](http://blogs.msdn.com/b/windowsazurestorage/)</span><span class="sxs-lookup"><span data-stu-id="f5b54-172">Visit hello [Azure Storage Team Blog](http://blogs.msdn.com/b/windowsazurestorage/)</span></span>
* <span data-ttu-id="f5b54-173">Hello 방문 [Ruby 용 Azure SDK](https://github.com/WindowsAzure/azure-sdk-for-ruby) GitHub의 리포지토리</span><span class="sxs-lookup"><span data-stu-id="f5b54-173">Visit hello [Azure SDK for Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span></span>

<span data-ttu-id="f5b54-174">간의 비교에 대 한 Azure 큐 서비스 및이 아티클과 hello에서 설명 하는 Azure 서비스 버스 큐에 설명 된 hello [어떻게 toouse 서비스 버스 큐](/develop/ruby/how-to-guides/service-bus-queues/) 문서를 참조 하십시오. [Azure 큐 및 서비스 버스 큐-비교 및 대조](../service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted.md)</span><span class="sxs-lookup"><span data-stu-id="f5b54-174">For a comparison between hello Azure Queue Service discussed in this article and Azure Service Bus Queues discussed in hello [How toouse Service Bus Queues](/develop/ruby/how-to-guides/service-bus-queues/) article, see [Azure Queues and Service Bus Queues - Compared and Contrasted](../service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted.md)</span></span>

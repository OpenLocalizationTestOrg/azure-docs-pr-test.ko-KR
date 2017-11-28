---
title: ".NET을 사용하여 Azure 큐 저장소 시작 | Microsoft Docs"
description: "Azure 큐는 응용 프로그램 구성 요소 간에 안정적인 비동기 메시징을 제공합니다. 클라우드 메시징을 사용하면 응용 프로그램 구성 요소를 독립적으로 조정할 수 있습니다."
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: c0f82537-a613-4f01-b2ed-fc82e5eea2a7
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 03/27/2017
ms.author: robinsh
ms.openlocfilehash: aa292c1eb048444f988a641df44183312cf39d28
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-azure-queue-storage-using-net"></a><span data-ttu-id="c2bdc-104">.NET을 사용하여 Azure 큐 저장소 시작</span><span class="sxs-lookup"><span data-stu-id="c2bdc-104">Get started with Azure Queue storage using .NET</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../../includes/storage-check-out-samples-dotnet.md)]

## <a name="overview"></a><span data-ttu-id="c2bdc-105">개요</span><span class="sxs-lookup"><span data-stu-id="c2bdc-105">Overview</span></span>
<span data-ttu-id="c2bdc-106">Azure 큐 저장소는 응용 프로그램 구성 요소 간에 클라우드 메시징을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c2bdc-106">Azure Queue storage provides cloud messaging between application components.</span></span> <span data-ttu-id="c2bdc-107">규모를 고려하여 응용 프로그램을 디자인할 때는 응용 프로그램 구성 요소를 개별적으로 확장할 수 있도록 각 구성 요소를 분리하는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="c2bdc-107">In designing applications for scale, application components are often decoupled, so that they can scale independently.</span></span> <span data-ttu-id="c2bdc-108">큐 저장소는 클라우드, 데스크톱, 온-프레미스 서버 또는 모바일 장치에서 실행 중인지와 관계 없이 응용 프로그램 구성 요소 간에 통신을 위한 비동기 메시징을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c2bdc-108">Queue storage delivers asynchronous messaging for communication between application components, whether they are running in the cloud, on the desktop, on an on-premises server, or on a mobile device.</span></span> <span data-ttu-id="c2bdc-109">큐 저장소는 또한 비동기 작업 관리와 프로세스 워크플로 작성을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="c2bdc-109">Queue storage also supports managing asynchronous tasks and building process work flows.</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="c2bdc-110">이 자습서 정보</span><span class="sxs-lookup"><span data-stu-id="c2bdc-110">About this tutorial</span></span>
<span data-ttu-id="c2bdc-111">이 자습서에서는 Azure 큐 저장소를 사용하여 몇 가지 일반적인 시나리오에 대한 .NET 코드를 작성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c2bdc-111">This tutorial shows how to write .NET code for some common scenarios using Azure Queue storage.</span></span> <span data-ttu-id="c2bdc-112">여기서 다루는 시나리오에는 큐 만들기 및 삭제, 큐 메시지 추가, 읽기 및 삭제가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c2bdc-112">Scenarios covered include creating and deleting queues and adding, reading, and deleting queue messages.</span></span>

<span data-ttu-id="c2bdc-113">**예상 완료 시간:** 45분</span><span class="sxs-lookup"><span data-stu-id="c2bdc-113">**Estimated time to complete:** 45 minutes</span></span>

<span data-ttu-id="c2bdc-114">**필수 구성 요소**</span><span class="sxs-lookup"><span data-stu-id="c2bdc-114">**Prerequisities:**</span></span>

* [<span data-ttu-id="c2bdc-115">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c2bdc-115">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="c2bdc-116">.NET용 Azure 저장소 클라이언트 라이브러리</span><span class="sxs-lookup"><span data-stu-id="c2bdc-116">Azure Storage Client Library for .NET</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [<span data-ttu-id="c2bdc-117">.NET용 Azure 구성 관리자</span><span class="sxs-lookup"><span data-stu-id="c2bdc-117">Azure Configuration Manager for .NET</span></span>](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* <span data-ttu-id="c2bdc-118">[Azure 저장소 계정](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="c2bdc-118">An [Azure storage account](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json#create-a-storage-account)</span></span>

[!INCLUDE [storage-dotnet-client-library-version-include](../../../includes/storage-dotnet-client-library-version-include.md)]

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a><span data-ttu-id="c2bdc-119">지시문을 사용하여 추가</span><span class="sxs-lookup"><span data-stu-id="c2bdc-119">Add using directives</span></span>
<span data-ttu-id="c2bdc-120">다음 `using` 지시문을 `Program.cs` 파일 맨 위에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c2bdc-120">Add the following `using` directives to the top of the `Program.cs` file:</span></span>

```csharp
using Microsoft.Azure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Queue; // Namespace for Queue storage types
```

### <a name="parse-the-connection-string"></a><span data-ttu-id="c2bdc-121">연결 문자열 구문 분석</span><span class="sxs-lookup"><span data-stu-id="c2bdc-121">Parse the connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-the-queue-service-client"></a><span data-ttu-id="c2bdc-122">큐 서비스 클라이언트 만들기</span><span class="sxs-lookup"><span data-stu-id="c2bdc-122">Create the Queue service client</span></span>
<span data-ttu-id="c2bdc-123">**CloudQueueClient** 클래스를 사용하면 큐 저장소에 저장된 큐를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2bdc-123">The **CloudQueueClient** class enables you to retrieve queues stored in Queue storage.</span></span> <span data-ttu-id="c2bdc-124">서비스 클라이언트를 만드는 한 가지 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c2bdc-124">Here's one way to create the service client:</span></span>

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
```
    
<span data-ttu-id="c2bdc-125">이제 데이터를 읽어 오고 큐 저장소에 데이터를 기록하는 코드를 작성할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c2bdc-125">Now you are ready to write code that reads data from and writes data to Queue storage.</span></span>

## <a name="create-a-queue"></a><span data-ttu-id="c2bdc-126">큐 만들기</span><span class="sxs-lookup"><span data-stu-id="c2bdc-126">Create a queue</span></span>
<span data-ttu-id="c2bdc-127">이 예제에서는 큐가 없는 경우 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c2bdc-127">This example shows how to create a queue if it does not already exist:</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a container.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Create the queue if it doesn't already exist
queue.CreateIfNotExists();
```

## <a name="insert-a-message-into-a-queue"></a><span data-ttu-id="c2bdc-128">큐에 메시지 삽입</span><span class="sxs-lookup"><span data-stu-id="c2bdc-128">Insert a message into a queue</span></span>
<span data-ttu-id="c2bdc-129">기존 큐에 메시지를 삽입하려면 먼저 새 **CloudQueueMessage**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c2bdc-129">To insert a message into an existing queue, first create a new **CloudQueueMessage**.</span></span> <span data-ttu-id="c2bdc-130">그런 다음, **AddMessage** 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="c2bdc-130">Next, call the **AddMessage** method.</span></span> <span data-ttu-id="c2bdc-131">**CloudQueueMessage**는 문자열(UTF-8 형식) 또는 **바이트** 배열에서 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2bdc-131">A **CloudQueueMessage** can be created from either a string (in UTF-8 format) or a **byte** array.</span></span> <span data-ttu-id="c2bdc-132">다음은 큐가 없는 경우 새로 만들고 'Hello, World' 메시지를 삽입하는 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="c2bdc-132">Here is code which creates a queue (if it doesn't exist) and inserts the message 'Hello, World':</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Create the queue if it doesn't already exist.
queue.CreateIfNotExists();

// Create a message and add it to the queue.
CloudQueueMessage message = new CloudQueueMessage("Hello, World");
queue.AddMessage(message);
```

## <a name="peek-at-the-next-message"></a><span data-ttu-id="c2bdc-133">다음 메시지 보기</span><span class="sxs-lookup"><span data-stu-id="c2bdc-133">Peek at the next message</span></span>
<span data-ttu-id="c2bdc-134">큐에서 메시지를 제거하지 않고도 **PeekMessage** 메서드를 호출하여 큐의 맨 앞에서 원하는 메시지를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2bdc-134">You can peek at the message in the front of a queue without removing it from the queue by calling the **PeekMessage** method.</span></span>

```csharp
// Retrieve storage account from connection string
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Peek at the next message
CloudQueueMessage peekedMessage = queue.PeekMessage();

// Display message.
Console.WriteLine(peekedMessage.AsString);
```

## <a name="change-the-contents-of-a-queued-message"></a><span data-ttu-id="c2bdc-135">대기 중인 메시지의 콘텐츠 변경</span><span class="sxs-lookup"><span data-stu-id="c2bdc-135">Change the contents of a queued message</span></span>
<span data-ttu-id="c2bdc-136">큐에 있는 메시지의 콘텐츠를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2bdc-136">You can change the contents of a message in-place in the queue.</span></span> <span data-ttu-id="c2bdc-137">메시지가 작업을 나타내는 경우 이 기능을 사용하여 작업의 상태를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2bdc-137">If the message represents a work task, you could use this feature to update the status of the work task.</span></span> <span data-ttu-id="c2bdc-138">다음 코드는 큐 메시지를 새로운 콘텐츠로 업데이트하고 표시 제한 시간이 60초 더 늘어나도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c2bdc-138">The following code updates the queue message with new contents, and sets the visibility timeout to extend another 60 seconds.</span></span> <span data-ttu-id="c2bdc-139">그러면 메시지와 연결된 작업의 상태가 저장되고 클라이언트에서 메시지에 대한 작업을 계속할 수 있는 시간이 1분 더 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c2bdc-139">This saves the state of work associated with the message, and gives the client another minute to continue working on the message.</span></span> <span data-ttu-id="c2bdc-140">이 기술을 사용하여 처리 단계가 하드웨어 또는 소프트웨어 오류로 인해 실패하는 경우 처음부터 시작하지 않고도 큐 메시지에 대한 여러 단계의 워크플로를 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2bdc-140">You could use this technique to track multi-step workflows on queue messages, without having to start over from the beginning if a processing step fails due to hardware or software failure.</span></span> <span data-ttu-id="c2bdc-141">일반적으로 재시도 횟수도 유지하고, 메시지가 *n*번 이상 다시 시도되면 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="c2bdc-141">Typically, you would keep a retry count as well, and if the message is retried more than *n* times, you would delete it.</span></span> <span data-ttu-id="c2bdc-142">이 기능은 처리될 때마다 응용 프로그램 오류를 트리거하는 메시지를 차단하여 보호해 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c2bdc-142">This protects against a message that triggers an application error each time it is processed.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Get the message from the queue and update the message contents.
CloudQueueMessage message = queue.GetMessage();
message.SetMessageContent("Updated contents.");
queue.UpdateMessage(message,
    TimeSpan.FromSeconds(60.0),  // Make it invisible for another 60 seconds.
    MessageUpdateFields.Content | MessageUpdateFields.Visibility);
```

## <a name="de-queue-the-next-message"></a><span data-ttu-id="c2bdc-143">큐에서 다음 메시지 제거</span><span class="sxs-lookup"><span data-stu-id="c2bdc-143">De-queue the next message</span></span>
<span data-ttu-id="c2bdc-144">다음 코드는 2단계를 거쳐 큐에서 메시지를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="c2bdc-144">Your code de-queues a message from a queue in two steps.</span></span> <span data-ttu-id="c2bdc-145">**GetMessage**를 호출하면 큐에서 다음 메시지를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2bdc-145">When you call **GetMessage**, you get the next message in a queue.</span></span> <span data-ttu-id="c2bdc-146">**GetMessage** 에서 반환된 메시지는 이 큐의 메시지를 읽는 다른 코드에는 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c2bdc-146">A message returned from **GetMessage** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="c2bdc-147">기본적으로, 이 메시지는 30초간 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c2bdc-147">By default, this message stays invisible for 30 seconds.</span></span> <span data-ttu-id="c2bdc-148">큐에서 메시지 제거를 완료하려면 **DeleteMessage**도 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2bdc-148">To finish removing the message from the queue, you must also call **DeleteMessage**.</span></span> <span data-ttu-id="c2bdc-149">메시지를 제거하는 이 2단계 프로세스는 코드가 하드웨어 또는 소프트웨어 오류로 인해 메시지를 처리하지 못하는 경우 코드의 다른 인스턴스가 동일한 메시지를 가져와서 다시 시도할 수 있도록 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="c2bdc-149">This two-step process of removing a message assures that if your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="c2bdc-150">코드는 메시지가 처리된 직후에 **DeleteMessage** 를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="c2bdc-150">Your code calls **DeleteMessage** right after the message has been processed.</span></span>

```csharp
// Retrieve storage account from connection string
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Get the next message
CloudQueueMessage retrievedMessage = queue.GetMessage();

//Process the message in less than 30 seconds, and then delete the message
queue.DeleteMessage(retrievedMessage);
```

## <a name="use-async-await-pattern-with-common-queue-storage-apis"></a><span data-ttu-id="c2bdc-151">일반적인 큐 저장소 API와 함께 Async-Await 패턴 사용</span><span class="sxs-lookup"><span data-stu-id="c2bdc-151">Use Async-Await pattern with common Queue storage APIs</span></span>
<span data-ttu-id="c2bdc-152">이 예제에서는 일반적인 큐 저장소 API와 함께 Async- Await 패턴을 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c2bdc-152">This example shows how to use the Async-Await pattern with common Queue storage APIs.</span></span> <span data-ttu-id="c2bdc-153">샘플의 경우 지정된 각 메서드의 비동기 버전을 호출하는데, 이 버전은 각 메서드의 *Async* 접미사로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c2bdc-153">The sample calls the asynchronous version of each of the given methods, as indicated by the *Async* suffix of each method.</span></span> <span data-ttu-id="c2bdc-154">비동기 메서드가 사용되는 경우 호출이 완료될 때까지 Async-Await 패턴이 로컬 실행을 일시 중단합니다.</span><span class="sxs-lookup"><span data-stu-id="c2bdc-154">When an async method is used, the async-await pattern suspends local execution until the call completes.</span></span> <span data-ttu-id="c2bdc-155">이 동작은 현재 스레드가 성능 병목 현상을 방지해주는 다른 작업을 수행할 수 있게 해주며, 응용 프로그램의 전반적인 응답성을 향상시킵니다.</span><span class="sxs-lookup"><span data-stu-id="c2bdc-155">This behavior allows the current thread to do other work, which helps avoid performance bottlenecks and improves the overall responsiveness of your application.</span></span> <span data-ttu-id="c2bdc-156">.NET에서의 Async-Await 패턴 사용에 대한 자세한 내용은 [Async 및 Await(C# 및 Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c2bdc-156">For more details on using the Async-Await pattern in .NET see [Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span></span>

```csharp
// Create the queue if it doesn't already exist
if(await queue.CreateIfNotExistsAsync())
{
    Console.WriteLine("Queue '{0}' Created", queue.Name);
}
else
{
    Console.WriteLine("Queue '{0}' Exists", queue.Name);
}

// Create a message to put in the queue
CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

// Async enqueue the message
await queue.AddMessageAsync(cloudQueueMessage);
Console.WriteLine("Message added");

// Async dequeue the message
CloudQueueMessage retrievedMessage = await queue.GetMessageAsync();
Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

// Async delete the message
await queue.DeleteMessageAsync(retrievedMessage);
Console.WriteLine("Deleted message");
```
    
## <a name="leverage-additional-options-for-de-queuing-messages"></a><span data-ttu-id="c2bdc-157">큐에서 메시지를 제거하는 추가 옵션 활용</span><span class="sxs-lookup"><span data-stu-id="c2bdc-157">Leverage additional options for de-queuing messages</span></span>
<span data-ttu-id="c2bdc-158">큐에서 메시지 검색을 사용자 지정할 수 있는 방법으로는 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2bdc-158">There are two ways you can customize message retrieval from a queue.</span></span>
<span data-ttu-id="c2bdc-159">먼저, 메시지의 배치(최대 32개)를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2bdc-159">First, you can get a batch of messages (up to 32).</span></span> <span data-ttu-id="c2bdc-160">두 번째로, 표시하지 않는 제한 시간을 더 길거나 더 짧게 설정하여 코드에서 각 메시지를 완전히 처리하는 시간을 늘리거나 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2bdc-160">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span> <span data-ttu-id="c2bdc-161">다음 코드 예제는 **GetMessages** 메서드를 사용하여 한 번 호출에 20개의 메시지를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c2bdc-161">The following code example uses the **GetMessages** method to get 20 messages in one call.</span></span> <span data-ttu-id="c2bdc-162">그런 다음에 **foreach** 루프를 사용하여 각 메시지를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="c2bdc-162">Then it processes each message using a **foreach** loop.</span></span> <span data-ttu-id="c2bdc-163">또한 각 메시지에 대해 표시하지 않는 제한 시간을 5분으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c2bdc-163">It also sets the invisibility timeout to five minutes for each message.</span></span> <span data-ttu-id="c2bdc-164">5분은 모든 메시지에 대해 동시에 시작되므로, **GetMessages**에 대한 호출 이후로 5분이 지나고 나면 삭제되지 않은 모든 메시지가 다시 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c2bdc-164">Note that the 5 minutes starts for all messages at the same time, so after 5 minutes have passed since the call to **GetMessages**, any messages which have not been deleted will become visible again.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

foreach (CloudQueueMessage message in queue.GetMessages(20, TimeSpan.FromMinutes(5)))
{
    // Process all messages in less than 5 minutes, deleting each message after processing.
    queue.DeleteMessage(message);
}
```

## <a name="get-the-queue-length"></a><span data-ttu-id="c2bdc-165">큐 길이 가져오기</span><span class="sxs-lookup"><span data-stu-id="c2bdc-165">Get the queue length</span></span>
<span data-ttu-id="c2bdc-166">큐에 있는 메시지의 추정된 개수를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2bdc-166">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="c2bdc-167">**FetchAttributes** 메서드는 메시지 수를 포함하여 큐 특성을 검색하도록 큐 서비스에 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="c2bdc-167">The **FetchAttributes** method asks the Queue service to retrieve the queue attributes, including the message count.</span></span> <span data-ttu-id="c2bdc-168">**ApproximateMessageCount** 속성은 큐 서비스를 호출하지 않고 **FetchAttributes** 메서드에서 검색한 마지막 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c2bdc-168">The **ApproximateMessageCount** property returns the last value retrieved by the **FetchAttributes** method, without calling the Queue service.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Fetch the queue attributes.
queue.FetchAttributes();

// Retrieve the cached approximate message count.
int? cachedMessageCount = queue.ApproximateMessageCount;

// Display number of messages.
Console.WriteLine("Number of messages in queue: " + cachedMessageCount);
```

## <a name="delete-a-queue"></a><span data-ttu-id="c2bdc-169">큐 삭제</span><span class="sxs-lookup"><span data-stu-id="c2bdc-169">Delete a queue</span></span>
<span data-ttu-id="c2bdc-170">큐 및 해당 큐의 모든 메시지를 삭제하려면 큐 개체의 **Delete** 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="c2bdc-170">To delete a queue and all the messages contained in it, call the **Delete** method on the queue object.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Delete the queue.
queue.Delete();
```
    

## <a name="next-steps"></a><span data-ttu-id="c2bdc-171">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c2bdc-171">Next steps</span></span>
<span data-ttu-id="c2bdc-172">이제 큐 저장소의 기본 사항을 배웠으므로 다음 링크를 따라 좀 더 복잡한 저장소 작업에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="c2bdc-172">Now that you've learned the basics of Queue storage, follow these links to learn about more complex storage tasks.</span></span>

* <span data-ttu-id="c2bdc-173">사용 가능한 API에 대한 자세한 내용은 큐 서비스 참조 설명서를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="c2bdc-173">View the Queue service reference documentation for complete details about available APIs:</span></span>
  * [<span data-ttu-id="c2bdc-174">Storage Client Library for .NET 참조</span><span class="sxs-lookup"><span data-stu-id="c2bdc-174">Storage Client Library for .NET reference</span></span>](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)
  * [<span data-ttu-id="c2bdc-175">REST API 참조</span><span class="sxs-lookup"><span data-stu-id="c2bdc-175">REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="c2bdc-176">[Azure WebJobs SDK](../../app-service-web/websites-dotnet-webjobs-sdk.md)를 사용하여 Azure 저장소 작업을 위해 작성하는 코드를 간소화하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c2bdc-176">Learn how to simplify the code you write to work with Azure Storage by using the [Azure WebJobs SDK](../../app-service-web/websites-dotnet-webjobs-sdk.md).</span></span>
* <span data-ttu-id="c2bdc-177">Azure에 데이터를 저장하기 위한 추가 옵션에 대한 자세한 내용은 추가 기능 가이드를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="c2bdc-177">View more feature guides to learn about additional options for storing data in Azure.</span></span>
  * <span data-ttu-id="c2bdc-178">[.NET을 사용하여 Azure 테이블 저장소를 시작](../../cosmos-db/table-storage-how-to-use-dotnet.md) 하여 구조화된 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="c2bdc-178">[Get started with Azure Table storage using .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md) to store structured data.</span></span>
  * <span data-ttu-id="c2bdc-179">[.NET을 사용하여 Azure Blob 저장소를 시작](../blobs/storage-dotnet-how-to-use-blobs.md) 하여 구조화되지 않은 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="c2bdc-179">[Get started with Azure Blob storage using .NET](../blobs/storage-dotnet-how-to-use-blobs.md) to store unstructured data.</span></span>
  * <span data-ttu-id="c2bdc-180">[.NET(C#)을 사용하여 SQL Database에 연결](../../sql-database/sql-database-connect-query-dotnet-core.md)하여 관계형 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="c2bdc-180">[Connect to SQL Database by using .NET (C#)](../../sql-database/sql-database-connect-query-dotnet-core.md) to store relational data.</span></span>

[Download and install the Azure SDK for .NET]: /develop/net/
[.NET client library reference]: http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409
[Creating a Azure Project in Visual Studio]: http://msdn.microsoft.com/library/azure/ee405487.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[OData]: http://nuget.org/packages/Microsoft.Data.OData/5.0.2
[Edm]: http://nuget.org/packages/Microsoft.Data.Edm/5.0.2
[Spatial]: http://nuget.org/packages/System.Spatial/5.0.2

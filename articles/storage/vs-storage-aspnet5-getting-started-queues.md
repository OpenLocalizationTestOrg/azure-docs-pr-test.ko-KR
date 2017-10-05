---
title: "Queue Storage 및 Visual Studio 연결된 서비스 시작(ASP.NET Core) | Microsoft Docs"
description: "Visual Studio의 ASP.NET Core 프로젝트에서 Azure Queue Storage를 사용하는 방법"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 04977069-5b2d-4cba-84ae-9fb2f5eb1006
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 4622496544ce6e1057ac68a2e9946917573e997e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-queue-storage-and-visual-studio-connected-services-aspnet-core"></a><span data-ttu-id="19eff-103">Queue Storage 및 Visual Studio 연결 서비스 시작(ASP.NET Core)</span><span class="sxs-lookup"><span data-stu-id="19eff-103">Get started with queue storage and Visual Studio connected services (ASP.NET Core)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="19eff-104">개요</span><span class="sxs-lookup"><span data-stu-id="19eff-104">Overview</span></span>
<span data-ttu-id="19eff-105">이 문서에서는 Visual Studio **연결된 서비스 추가** 대화 상자를 사용하여 ASP.NET Core 프로젝트에서 Azure Storage 계정을 만들거나 참조한 후 Visual Studio에서 Azure Queue Storage 사용을 시작하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="19eff-105">This article describes how to get started using Azure Queue storage in Visual Studio after you have created or referenced an Azure storage account in an ASP.NET Core project by using the Visual Studio **Add Connected Services** dialog.</span></span> <span data-ttu-id="19eff-106">**연결된 서비스 추가** 작업은 프로젝트의 Azure 저장소에 액세스하는 데 적합한 NuGet 패키지를 설치하고 프로젝트 구성 파일에 저장소 계정에 대한 연결 문자열을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="19eff-106">The **Add Connected Services** operation installs the appropriate NuGet packages to access Azure storage in your project and adds the connection string for the storage account to your project configuration files.</span></span>

<span data-ttu-id="19eff-107">Azure 큐 저장소는 HTTP 또는 HTTPS를 사용하여 인증된 호출을 통해 전 세계 어디에서나 액세스할 수 있는 다수의 메시지를 저장하기 위한 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="19eff-107">Azure queue storage is a service for storing large numbers of messages that can be accessed from anywhere in the world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="19eff-108">단일 큐 메시지의 크기는 최대 64KB일 수 있으며, 하나의 큐에 저장소 계정의 총 용량 제한까지 수백만 개의 메시지가 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19eff-108">A single queue message can be up to 64 kilobytes (KB) in size, and a queue can contain millions of messages, up to the total capacity limit of a storage account.</span></span>

<span data-ttu-id="19eff-109">시작하려면 먼저 저장소 계정에서 Azure 큐를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="19eff-109">To get started, you first need to create an Azure queue in your storage account.</span></span> <span data-ttu-id="19eff-110">코드에서 큐를 만드는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="19eff-110">We'll show you how to create a queue in code.</span></span> <span data-ttu-id="19eff-111">큐 메시지 추가, 수정, 읽기 및 제거와 같은 기본 큐 작업을 수행하는 방법도 알려드립니다.</span><span class="sxs-lookup"><span data-stu-id="19eff-111">We'll also show you how to perform basic queue operations, such as adding, modifying, reading, and removing queue messages.</span></span> <span data-ttu-id="19eff-112">샘플은 C\# 코드로 작성되었으며 Azure Storage Client Library for .NET을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="19eff-112">The samples are written in C\# code and use the Azure Storage Client Library for .NET.</span></span> <span data-ttu-id="19eff-113">ASP.NET에 대한 자세한 내용은 [ASP.NET(영문)](http://www.asp.net)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="19eff-113">For more information about ASP.NET, see [ASP.NET](http://www.asp.net).</span></span>

<span data-ttu-id="19eff-114">**참고:** ASP.NET Core에서 Azure Storage에 대한 호출을 수행하는 일부 API는 비동기적입니다.</span><span class="sxs-lookup"><span data-stu-id="19eff-114">**NOTE:** Some of the APIs that perform calls to Azure storage in ASP.NET Core are asynchronous.</span></span> <span data-ttu-id="19eff-115">자세한 내용은 [Async 및 Await를 사용한 비동기 프로그래밍](http://msdn.microsoft.com/library/hh191443.aspx) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="19eff-115">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="19eff-116">아래 코드에서는 비동기 프로그래밍 메서드를 사용한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="19eff-116">The code below assumes async programming methods are being used.</span></span>

* <span data-ttu-id="19eff-117">큐를 프로그래밍 방식으로 조작하는 방법에 대한 자세한 내용은 [.NET을 사용하여 Azure 큐 저장소 시작](storage-dotnet-how-to-use-queues.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="19eff-117">See [Get started with Azure Queue storage using .NET](storage-dotnet-how-to-use-queues.md) for more information on programmatically manipulating queues.</span></span>
* <span data-ttu-id="19eff-118">Azure 저장소에 대한 일반적인 내용은 [저장소 설명서](https://azure.microsoft.com/documentation/services/storage/) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="19eff-118">See [Storage documentation](https://azure.microsoft.com/documentation/services/storage/) for general information about Azure Storage.</span></span>
* <span data-ttu-id="19eff-119">Azure 클라우드 서비스에 대한 일반적인 내용은 [클라우드 서비스 설명서](https://azure.microsoft.com/documentation/services/cloud-services/) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="19eff-119">See [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/) for general information about Azure cloud services.</span></span>
* <span data-ttu-id="19eff-120">ASP.NET 응용 프로그램을 프로그래밍하는 방법에 대한 자세한 내용은 [ASP.NET](http://www.asp.net) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="19eff-120">See [ASP.NET](http://www.asp.net) for more information about programming ASP.NET applications.</span></span>

## <a name="access-queues-in-code"></a><span data-ttu-id="19eff-121">코드에서 큐 액세스</span><span class="sxs-lookup"><span data-stu-id="19eff-121">Access queues in code</span></span>
<span data-ttu-id="19eff-122">ASP.NET Core 프로젝트의 큐에 액세스하려면 Azure Queue Storage에 액세스하는 C# 소스 파일에 다음 항목을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="19eff-122">To access queues in ASP.NET Core projects, you need to include the following items to any C# source file that accesses Azure queue storage.</span></span>

1. <span data-ttu-id="19eff-123">C# 파일 맨 위의 네임스페이스 선언에 이러한 **using** 문이 포함되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="19eff-123">Make sure the namespace declarations at the top of the C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Queue;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="19eff-124">저장소 계정 정보를 나타내는 **CloudStorageAccount** 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="19eff-124">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="19eff-125">Azure 서비스 구성에서 저장소 연결 문자열 및 저장소 계정 정보를 가져오려면 다음 코드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="19eff-125">Use the following code to get the your storage connection string and storage account information from the Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
3. <span data-ttu-id="19eff-126">저장소 계정의 큐 개체를 참조하려면 **CloudQueueClient** 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="19eff-126">Get a **CloudQueueClient** object to reference the queue objects in your storage account.</span></span>  
   
        // Create the CloudQueueClient object for the storage account.
        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
4. <span data-ttu-id="19eff-127">특정 큐를 참조하려면 **CloudQueue** 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="19eff-127">Get a **CloudQueue** object to reference a specific queue.</span></span>
   
        // Get a reference to the CloudQueue named "messageQueue"
        CloudQueue messageQueue = queueClient.GetQueueReference("messageQueue");

<span data-ttu-id="19eff-128">**참고:** 다음 샘플의 코드 앞에 위의 코드를 모두 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="19eff-128">**NOTE:** Use all of the above code in front of the code in the following samples.</span></span>

### <a name="create-a-queue-in-code"></a><span data-ttu-id="19eff-129">코드에서 큐 만들기</span><span class="sxs-lookup"><span data-stu-id="19eff-129">Create a queue in code</span></span>
<span data-ttu-id="19eff-130">코드에서 Azure 큐를 만들려면 **CreateIfNotExistsAsync**에 대한 호출을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="19eff-130">To create the Azure queue in code, just add a call to **CreateIfNotExistsAsync**.</span></span>

    // Create the CloudQueue if it does not exist.
    await messageQueue.CreateIfNotExistsAsync();

## <a name="add-a-message-to-a-queue"></a><span data-ttu-id="19eff-131">큐에 메시지 추가</span><span class="sxs-lookup"><span data-stu-id="19eff-131">Add a message to a queue</span></span>
<span data-ttu-id="19eff-132">기존 큐에 메시지를 삽입하려면 새 **CloudQueueMessage** 개체를 만든 다음 **AddMessageAsync** 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="19eff-132">To insert a message into an existing queue, create a new **CloudQueueMessage** object, then call the **AddMessageAsync** method.</span></span>

<span data-ttu-id="19eff-133">**CloudQueueMessage** 개체는 문자열(UTF-8 형식) 또는 바이트 배열에서 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19eff-133">A **CloudQueueMessage** object can be created from either a string (in UTF-8 format) or a byte array.</span></span>

<span data-ttu-id="19eff-134">다음은 'Hello, World' 메시지를 삽입하는 예입니다.</span><span class="sxs-lookup"><span data-stu-id="19eff-134">Here is an example which inserts the message 'Hello, World'.</span></span>

    // Create a message and add it to the queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    await messageQueue.AddMessageAsync(message);

## <a name="read-a-message-in-a-queue"></a><span data-ttu-id="19eff-135">큐의 메시지 읽기</span><span class="sxs-lookup"><span data-stu-id="19eff-135">Read a message in a queue</span></span>
<span data-ttu-id="19eff-136">큐에서 메시지를 제거하지 않고도 **PeekMessageAsync** 메서드를 호출하여 큐의 맨 앞에서 원하는 메시지를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19eff-136">You can peek at the message in the front of a queue without removing it from the queue by calling the **PeekMessageAsync** method.</span></span>

    // Peek the next message in the queue. 
    CloudQueueMessage peekedMessage = await messageQueue.PeekMessageAsync();


## <a name="read-and-remove-a-message-in-a-queue"></a><span data-ttu-id="19eff-137">큐의 메시지 읽기 및 제거</span><span class="sxs-lookup"><span data-stu-id="19eff-137">Read and remove a message in a queue</span></span>
<span data-ttu-id="19eff-138">이 코드에서는 2단계를 거쳐 큐에서 메시지를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19eff-138">Your code can remove (dequeue) a message from a queue in two steps.</span></span>

1. <span data-ttu-id="19eff-139">**GetMessageAsync** 를 호출하여 큐에서 다음 메시지를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="19eff-139">Call **GetMessageAsync** to get the next message in a queue.</span></span> <span data-ttu-id="19eff-140">**GetMessageAsync** 에서 반환된 메시지는 이 큐의 메시지를 읽는 다른 코드에는 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="19eff-140">A message returned from **GetMessageAsync** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="19eff-141">기본적으로, 이 메시지는 30초간 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="19eff-141">By default, this message stays invisible for 30 seconds.</span></span>
2. <span data-ttu-id="19eff-142">큐에서 메시지 제거를 완료하려면 **DeleteMessageAsync**를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="19eff-142">To finish removing the message from the queue, call **DeleteMessageAsync**.</span></span>

<span data-ttu-id="19eff-143">메시지를 제거하는 이 2단계 프로세스는 코드가 하드웨어 또는 소프트웨어 오류로 인해 메시지를 처리하지 못하는 경우 코드의 다른 인스턴스가 동일한 메시지를 가져와서 다시 시도할 수 있도록 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="19eff-143">This two-step process of removing a message assures that if your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="19eff-144">다음 코드에서는 메시지가 처리된 직후에 **DeleteMessageAsync** 를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="19eff-144">The following code calls **DeleteMessageAsync** right after the message has been processed.</span></span>

    // Get the next message in the queue.
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();

    // Process the message in less than 30 seconds.

    // Then delete the message.
    await messageQueue.DeleteMessageAsync(retrievedMessage);

## <a name="leverage-additional-options-for-dequeuing-messages"></a><span data-ttu-id="19eff-145">큐에서 메시지를 제거하는 추가 옵션 활용</span><span class="sxs-lookup"><span data-stu-id="19eff-145">Leverage additional options for dequeuing messages</span></span>
<span data-ttu-id="19eff-146">큐에서 메시지 검색을 사용자 지정할 수 있는 방법으로는 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19eff-146">There are two ways you can customize message retrieval from a queue.</span></span>
<span data-ttu-id="19eff-147">먼저, 메시지의 배치(최대 32개)를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19eff-147">First, you can get a batch of messages (up to 32).</span></span> <span data-ttu-id="19eff-148">두 번째로, 표시하지 않는 제한 시간을 더 길거나 더 짧게 설정하여 코드에서 각 메시지를 완전히 처리하는 시간을 늘리거나 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19eff-148">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span> <span data-ttu-id="19eff-149">다음 코드 예제는 **GetMessages** 메서드를 사용하여 한 번 호출에 20개의 메시지를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="19eff-149">The following code example uses the **GetMessages** method to get 20 messages in one call.</span></span> <span data-ttu-id="19eff-150">그런 다음에 **foreach** 루프를 사용하여 각 메시지를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="19eff-150">Then it processes each message using a **foreach** loop.</span></span> <span data-ttu-id="19eff-151">또한 각 메시지에 대해 표시하지 않는 시간 제한을 5분으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="19eff-151">It also sets the invisibility timeout to 5 minutes for each message.</span></span> <span data-ttu-id="19eff-152">5분은 모든 메시지에 대해 동시에 시작되므로, **GetMessages**호출 이후 5분이 지나고 나면 삭제되지 않은 모든 메시지가 다시 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="19eff-152">Note that the 5 minutes start for all messages at the same time, so after 5 minutes have passed after the call to **GetMessages**, any messages which have not been deleted become visible again.</span></span>

    // Retrieve 20 messages at a time, keeping those messages invisible for 5 minutes, 
    //   delete each message after processing.

    foreach (CloudQueueMessage message in messageQueue.GetMessages(20, TimeSpan.FromMinutes(5)))
    {
        // Process all messages in less than 5 minutes, deleting each message after processing.
        queue.DeleteMessage(message);
    }

## <a name="get-the-queue-length"></a><span data-ttu-id="19eff-153">큐 길이 가져오기</span><span class="sxs-lookup"><span data-stu-id="19eff-153">Get the queue length</span></span>
<span data-ttu-id="19eff-154">큐에 있는 메시지의 추정된 개수를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19eff-154">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="19eff-155">**FetchAttributes** 메서드는 메시지 수를 포함하여 큐 특성을 검색하도록 큐 서비스에 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="19eff-155">The **FetchAttributes** method asks the queue service to retrieve the queue attributes, including the message count.</span></span> <span data-ttu-id="19eff-156">**ApproximateMethodCount** 속성은 큐 서비스를 호출하지 않고도 **FetchAttributes** 메서드를 통해 검색된 마지막 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="19eff-156">The **ApproximateMethodCount** property returns the last value retrieved by the **FetchAttributes** method, without calling the queue service.</span></span>

    // Fetch the queue attributes.
    messageQueue.FetchAttributes();

    // Retrieve the cached approximate message count.
    int? cachedMessageCount = messageQueue.ApproximateMessageCount;

    // Display the number of messages.
    Console.WriteLine("Number of messages in queue: " + cachedMessageCount);

## <a name="use-the-async-await-pattern-with-common-queue-apis"></a><span data-ttu-id="19eff-157">일반적인 큐 API와 함께 Async-Await 패턴 사용</span><span class="sxs-lookup"><span data-stu-id="19eff-157">Use the Async-Await pattern with common queue APIs</span></span>
<span data-ttu-id="19eff-158">이 예제에서는 일반적인 큐 API와 함께 Async- Await 패턴을 사용하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="19eff-158">This example shows how to use the Async-Await pattern with common queue APIs.</span></span> <span data-ttu-id="19eff-159">샘플은 지정된 각 메서드의 비동기 버전을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="19eff-159">The sample calls the async version of each of the given methods.</span></span> <span data-ttu-id="19eff-160">이것은 각 메서드의 Async 사후 수정에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19eff-160">This can be seen by the Async post-fix of each method.</span></span> <span data-ttu-id="19eff-161">비동기 메서드가 사용되는 경우 호출이 완료될 때까지 Async-Await 패턴이 로컬 실행을 일시 중단합니다.</span><span class="sxs-lookup"><span data-stu-id="19eff-161">When an async method is used, the Async-Await pattern suspends local execution until the call is completed.</span></span> <span data-ttu-id="19eff-162">이 동작은 현재 스레드가 성능 병목 현상을 방지해주는 다른 작업을 수행할 수 있게 해주며, 응용 프로그램의 전반적인 응답성을 향상시킵니다.</span><span class="sxs-lookup"><span data-stu-id="19eff-162">This behavior allows the current thread to do other work which helps avoid performance bottlenecks and improves the overall responsiveness of your application.</span></span> <span data-ttu-id="19eff-163">.NET에서 Async-Await 패턴의 사용에 대한 자세한 내용은 [Async 및 Await(C# 및 Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span><span class="sxs-lookup"><span data-stu-id="19eff-163">For more details on using the Async-Await pattern in .NET, see [Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span></span>

    // Create a message to add to the queue.
    CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

    // Async enqueue the message.
    await messageQueue.AddMessageAsync(cloudQueueMessage);
    Console.WriteLine("Message added");

    // Async dequeue the message.
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();
    Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

    // Async delete the message.
    await messageQueue.DeleteMessageAsync(retrievedMessage);
    Console.WriteLine("Deleted message");
## <a name="delete-a-queue"></a><span data-ttu-id="19eff-164">큐 삭제</span><span class="sxs-lookup"><span data-stu-id="19eff-164">Delete a queue</span></span>
<span data-ttu-id="19eff-165">큐 및 해당 큐의 모든 메시지를 삭제하려면 큐 개체의 **Delete** 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="19eff-165">To delete a queue and all the messages contained in it, call the **Delete** method on the queue object.</span></span>

    // Delete the queue.
    messageQueue.Delete();


## <a name="next-steps"></a><span data-ttu-id="19eff-166">다음 단계</span><span class="sxs-lookup"><span data-stu-id="19eff-166">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-queues-next-steps](../../includes/vs-storage-dotnet-queues-next-steps.md)]


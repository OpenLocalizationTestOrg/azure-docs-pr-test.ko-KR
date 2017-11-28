---
title: "큐 저장소 사용 방법(C++) | Microsoft Docs"
description: "Azure에서 큐 저장소 서비스를 사용하는 방법에 대해 알아봅니다. 샘플은 C++로 작성되었습니다."
services: storage
documentationcenter: .net
author: cbrooksmsft
manager: jahogg
editor: tysonn
ms.assetid: c8a36365-29f6-404d-8fd1-858a7f33b50a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: cpp
ms.topic: article
ms.date: 05/11/2017
ms.author: cbrooksmsft
ms.openlocfilehash: 5e81d5e0af9871099b7f921f355cf94249e4d30c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-queue-storage-from-c"></a><span data-ttu-id="d7603-104">C++에서 큐 저장소를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="d7603-104">How to use Queue Storage from C++</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="d7603-105">개요</span><span class="sxs-lookup"><span data-stu-id="d7603-105">Overview</span></span>
<span data-ttu-id="d7603-106">이 가이드에서는 Azure 큐 저장소 서비스를 사용하여 일반 시나리오를 수행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d7603-106">This guide will show you how to perform common scenarios using the Azure Queue storage service.</span></span> <span data-ttu-id="d7603-107">샘플은 C++로 작성되었으며 [Azure Storage Client Library for C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d7603-107">The samples are written in C++ and use the [Azure Storage Client Library for C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span></span> <span data-ttu-id="d7603-108">여기서 다루는 시나리오에는 **큐 만들기 및 삭제**뿐만 아니라 큐 메시지 **삽입**, **보기**, **가져오기** 및 **삭제**가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7603-108">The scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span>

> [!NOTE]
> <span data-ttu-id="d7603-109">이 가이드는 Azure Storage Client Library for C++ 버전 1.0.0 이상을 대상으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7603-109">This guide targets the Azure Storage Client Library for C++ version 1.0.0 and above.</span></span> <span data-ttu-id="d7603-110">권장되는 버전은 Storage Client Library 2.2.0이며, [NuGet](http://www.nuget.org/packages/wastorage) 또는 [GitHub](http://github.com/Azure/azure-storage-cpp/)를 통해 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="d7603-110">The recommended version is Storage Client Library 2.2.0, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](http://github.com/Azure/azure-storage-cpp/).</span></span>
> 
> 

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a><span data-ttu-id="d7603-111">C++ 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="d7603-111">Create a C++ application</span></span>
<span data-ttu-id="d7603-112">이 가이드에서는 C++ 응용 프로그램 내에서 실행할 수 있는 저장소 기능을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d7603-112">In this guide, you will use storage features which can be run within a C++ application.</span></span>

<span data-ttu-id="d7603-113">이 기능을 사용하려면, Azure Storage Client Library for C++를 설치하고 Azure 구독에서 Azure 저장소 계정을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7603-113">To do so, you will need to install the Azure Storage Client Library for C++ and create an Azure storage account in your Azure subscription.</span></span>

<span data-ttu-id="d7603-114">Azure Storage Client Library for C++를 설치하려면 다음 메서드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7603-114">To install the Azure Storage Client Library for C++, you can use the following methods:</span></span>

* <span data-ttu-id="d7603-115">**Linux:**[Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) 페이지의 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="d7603-115">**Linux:** Follow the instructions given in the [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>
* <span data-ttu-id="d7603-116">**Windows:** Visual Studio에서 **도구 > NuGet 패키지 관리자 > 패키지 관리자 콘솔**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d7603-116">**Windows:** In Visual Studio, click **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="d7603-117">[NuGet 패키지 관리자 콘솔](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) 에 다음 명령을 입력하고 **ENTER**를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="d7603-117">Type the following command into the [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press **ENTER**.</span></span>

```  
Install-Package wastorage
```

## <a name="configure-your-application-to-access-queue-storage"></a><span data-ttu-id="d7603-118">큐 저장소에 액세스하도록 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="d7603-118">Configure your application to access Queue Storage</span></span>
<span data-ttu-id="d7603-119">Azure 저장소 API를 사용하여 큐에 액세스하려는 C++ 파일의 맨 위에 다음 include 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d7603-119">Add the following include statements to the top of the C++ file where you want to use the Azure storage APIs to access queues:</span></span>  

```cpp
#include <was/storage_account.h>
#include <was/queue.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="d7603-120">Azure 저장소 연결 문자열 설정</span><span class="sxs-lookup"><span data-stu-id="d7603-120">Set up an Azure storage connection string</span></span>
<span data-ttu-id="d7603-121">Azure 저장소 클라이언트는 저장소 연결 문자열을 사용하여 데이터 관리 서비스에 액세스하기 위한 끝점 및 자격 증명을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="d7603-121">An Azure storage client uses a storage connection string to store endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="d7603-122">클라이언트 응용 프로그램에서 실행할 경우, 저장소 계정의 이름 및 [Azure Portal](https://portal.azure.com)에 나열된 저장소 계정의 저장소 액세스 키를 *AccountName* 및 *AccountKey* 값에 사용하여 다음 형식의 저장소 연결 문자열을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7603-122">When running in a client application, you must provide the storage connection string in the following format, using the name of your storage account and the storage access key for the storage account listed in the [Azure Portal](https://portal.azure.com) for the *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="d7603-123">저장소 계정 및 액세스 키에 대한 자세한 내용은 [Azure 저장소 계정 정보](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d7603-123">For information on storage accounts and access keys, see [About Azure Storage Accounts](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json).</span></span> <span data-ttu-id="d7603-124">이 예제는 정적 필드가 연결 문자열을 포함할 수 있도록 선언하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d7603-124">This example shows how you can declare a static field to hold the connection string:</span></span>  

```cpp
// Define the connection-string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

<span data-ttu-id="d7603-125">로컬 Windows 컴퓨터에서 응용 프로그램을 테스트 하려면 [Azure SDK](https://azure.microsoft.com/downloads/)와 함께 설치된 Microsoft Azure [Storage 에뮬레이터](../common/storage-use-emulator.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7603-125">To test your application in your local Windows computer, you can use the Microsoft Azure [storage emulator](../common/storage-use-emulator.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) that is installed with the [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="d7603-126">저장소 에뮬레이터는 로컬 개발 컴퓨터의Azure에서 사용할 수 있는 Blob, 큐 및 테이블 서비스를 시뮬레이션하는 유틸리티입니다.</span><span class="sxs-lookup"><span data-stu-id="d7603-126">The storage emulator is a utility that simulates the Blob, Queue, and Table services available in Azure on your local development machine.</span></span> <span data-ttu-id="d7603-127">다음 예제에서는 로컬 저장소 에뮬레이터에 연결 문자열을 포함할 수 있도록 정적 필드를 선언하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="d7603-127">The following example shows how you can declare a static field to hold the connection string to your local storage emulator:</span></span>  

```cpp
// Define the connection-string with Azure Storage Emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

<span data-ttu-id="d7603-128">Azure Storage 에뮬레이터를 시작하려면 **시작** 단추를 선택하거나 **Windows** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="d7603-128">To start the Azure storage emulator, select the **Start** button or press the **Windows** key.</span></span> <span data-ttu-id="d7603-129">**Azure Storage 에뮬레이터** 입력을 시작하고 응용 프로그램 목록에서 **Microsoft Azure Storage 에뮬레이터**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d7603-129">Begin typing **Azure Storage Emulator**, and select **Microsoft Azure Storage Emulator** from the list of applications.</span></span>

<span data-ttu-id="d7603-130">다음 샘플에서는 저장소 연결 문자열을 가져오기 위해 위의 두 메서드 중 하나를 사용한 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="d7603-130">The following samples assume that you have used one of these two methods to get the storage connection string.</span></span>

## <a name="retrieve-your-connection-string"></a><span data-ttu-id="d7603-131">연결 문자열 검색</span><span class="sxs-lookup"><span data-stu-id="d7603-131">Retrieve your connection string</span></span>
<span data-ttu-id="d7603-132">**cloud_storage_account** 클래스를 사용하여 저장소 계정 정보를 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7603-132">You can use the **cloud_storage_account** class to represent your Storage Account information.</span></span> <span data-ttu-id="d7603-133">저장소 연결 문자열에서 저장소 계정 정보를 검색하려면 **구문 분석** 메서드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7603-133">To retrieve your storage account information from the storage connection string, you can use the **parse** method.</span></span>

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

## <a name="how-to-create-a-queue"></a><span data-ttu-id="d7603-134">방법: 큐 만들기</span><span class="sxs-lookup"><span data-stu-id="d7603-134">How to: Create a queue</span></span>
<span data-ttu-id="d7603-135">**cloud_queue_client** 개체를 통해 큐에 대한 참조 개체를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7603-135">A **cloud_queue_client** object lets you get reference objects for queues.</span></span> <span data-ttu-id="d7603-136">다음 코드는 **cloud_queue_client** 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d7603-136">The following code creates a **cloud_queue_client** object.</span></span>

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create a queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();
```

<span data-ttu-id="d7603-137">**cloud_queue_client** 개체를 사용하여 사용할 큐에 대한 참조를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7603-137">Use the **cloud_queue_client** object to get a reference to the queue you want to use.</span></span> <span data-ttu-id="d7603-138">큐가 없는 경우 새로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7603-138">You can create the queue if it doesn't exist.</span></span>

```cpp
// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Create the queue if it doesn't already exist.
 queue.create_if_not_exists();  
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="d7603-139">방법: 큐에 메시지 삽입</span><span class="sxs-lookup"><span data-stu-id="d7603-139">How to: Insert a message into a queue</span></span>
<span data-ttu-id="d7603-140">기존 큐에 메시지를 삽입하려면 먼저 새 **cloud_queue_message**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d7603-140">To insert a message into an existing queue, first create a new **cloud_queue_message**.</span></span> <span data-ttu-id="d7603-141">그런 다음, **add_message** 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="d7603-141">Next, call the **add_message** method.</span></span> <span data-ttu-id="d7603-142">**cloud_queue_message**는 문자열 또는 **바이트** 배열에서 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7603-142">A **cloud_queue_message** can be created from either a string or a **byte** array.</span></span> <span data-ttu-id="d7603-143">다음은 큐가 없는 경우 새로 만들고 'Hello, World' 메시지를 삽입하는 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="d7603-143">Here is code which creates a queue (if it doesn't exist) and inserts the message 'Hello, World':</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Create the queue if it doesn't already exist.
queue.create_if_not_exists();

// Create a message and add it to the queue.
azure::storage::cloud_queue_message message1(U("Hello, World"));
queue.add_message(message1);  
```

## <a name="how-to-peek-at-the-next-message"></a><span data-ttu-id="d7603-144">방법: 다음 메시지 보기</span><span class="sxs-lookup"><span data-stu-id="d7603-144">How to: Peek at the next message</span></span>
<span data-ttu-id="d7603-145">큐에서 메시지를 제거하지 않고도 **peek_message** 메서드를 호출하여 큐의 맨 앞에서 원하는 메시지를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7603-145">You can peek at the message in the front of a queue without removing it from the queue by calling the **peek_message** method.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Peek at the next message.
azure::storage::cloud_queue_message peeked_message = queue.peek_message();

// Output the message content.
std::wcout << U("Peeked message content: ") << peeked_message.content_as_string() << std::endl;
```

## <a name="how-to-change-the-contents-of-a-queued-message"></a><span data-ttu-id="d7603-146">방법: 대기 중인 메시지의 콘텐츠 변경</span><span class="sxs-lookup"><span data-stu-id="d7603-146">How to: Change the contents of a queued message</span></span>
<span data-ttu-id="d7603-147">큐에 있는 메시지의 콘텐츠를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7603-147">You can change the contents of a message in-place in the queue.</span></span> <span data-ttu-id="d7603-148">메시지가 작업을 나타내는 경우 이 기능을 사용하여 작업의 상태를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7603-148">If the message represents a work task, you could use this feature to update the status of the work task.</span></span> <span data-ttu-id="d7603-149">다음 코드는 큐 메시지를 새로운 콘텐츠로 업데이트하고 표시 제한 시간이 60초 더 늘어나도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d7603-149">The following code updates the queue message with new contents, and sets the visibility timeout to extend another 60 seconds.</span></span> <span data-ttu-id="d7603-150">그러면 메시지와 연결된 작업의 상태가 저장되고 클라이언트에서 메시지에 대한 작업을 계속할 수 있는 시간이 1분 더 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7603-150">This saves the state of work associated with the message, and gives the client another minute to continue working on the message.</span></span> <span data-ttu-id="d7603-151">이 기술을 사용하여 처리 단계가 하드웨어 또는 소프트웨어 오류로 인해 실패하는 경우 처음부터 시작하지 않고도 큐 메시지에 대한 여러 단계의 워크플로를 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7603-151">You could use this technique to track multi-step workflows on queue messages, without having to start over from the beginning if a processing step fails due to hardware or software failure.</span></span> <span data-ttu-id="d7603-152">일반적으로 다시 시도 수도 유지하므로, 메시지가 n번 넘게 다시 시도된 경우 메시지를 지울 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7603-152">Typically, you would keep a retry count as well, and if the message is retried more than n times, you would delete it.</span></span> <span data-ttu-id="d7603-153">이 기능은 처리될 때마다 응용 프로그램 오류를 트리거하는 메시지를 차단하여 보호해 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d7603-153">This protects against a message that triggers an application error each time it is processed.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_conection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Get the message from the queue and update the message contents.
// The visibility timeout "0" means make it visible immediately.
// The visibility timeout "60" means the client can get another minute to continue
// working on the message.
azure::storage::cloud_queue_message changed_message = queue.get_message();

changed_message.set_content(U("Changed message"));
queue.update_message(changed_message, std::chrono::seconds(60), true);

// Output the message content.
std::wcout << U("Changed message content: ") << changed_message.content_as_string() << std::endl;  
```

## <a name="how-to-de-queue-the-next-message"></a><span data-ttu-id="d7603-154">방법: 큐에서 다음 메시지 제거</span><span class="sxs-lookup"><span data-stu-id="d7603-154">How to: De-queue the next message</span></span>
<span data-ttu-id="d7603-155">다음 코드는 2단계를 거쳐 큐에서 메시지를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="d7603-155">Your code de-queues a message from a queue in two steps.</span></span> <span data-ttu-id="d7603-156">**get_message**를 호출하면 큐에서 다음 메시지를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7603-156">When you call **get_message**, you get the next message in a queue.</span></span> <span data-ttu-id="d7603-157">**get_message**에서 반환된 메시지는 이 큐의 메시지를 읽는 다른 코드에는 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d7603-157">A message returned from **get_message** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="d7603-158">큐에서 메시지 제거를 완료하려면 **delete_message**도 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7603-158">To finish removing the message from the queue, you must also call **delete_message**.</span></span> <span data-ttu-id="d7603-159">메시지를 제거하는 이 2단계 프로세스는 코드가 하드웨어 또는 소프트웨어 오류로 인해 메시지를 처리하지 못하는 경우 코드의 다른 인스턴스가 동일한 메시지를 가져와서 다시 시도할 수 있도록 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="d7603-159">This two-step process of removing a message assures that if your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="d7603-160">코드는 메시지가 처리된 직후에 **delete_message**를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="d7603-160">Your code calls **delete_message** right after the message has been processed.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Get the next message.
azure::storage::cloud_queue_message dequeued_message = queue.get_message();
std::wcout << U("Dequeued message: ") << dequeued_message.content_as_string() << std::endl;

// Delete the message.
queue.delete_message(dequeued_message);
```

## <a name="how-to-leverage-additional-options-for-de-queuing-messages"></a><span data-ttu-id="d7603-161">방법: 큐에서 메시지를 제거하는 추가 옵션 활용</span><span class="sxs-lookup"><span data-stu-id="d7603-161">How to: Leverage additional options for de-queuing messages</span></span>
<span data-ttu-id="d7603-162">큐에서 메시지 검색을 사용자 지정할 수 있는 방법으로는 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7603-162">There are two ways you can customize message retrieval from a queue.</span></span> <span data-ttu-id="d7603-163">먼저, 메시지의 배치(최대 32개)를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7603-163">First, you can get a batch of messages (up to 32).</span></span> <span data-ttu-id="d7603-164">두 번째로, 표시하지 않는 제한 시간을 더 길거나 더 짧게 설정하여 코드에서 각 메시지를 완전히 처리하는 시간을 늘리거나 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7603-164">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span> <span data-ttu-id="d7603-165">다음 코드 예제는 **get_messages** 메서드를 사용하여 한 번 호출에서 20개의 메시지를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d7603-165">The following code example uses the **get_messages** method to get 20 messages in one call.</span></span> <span data-ttu-id="d7603-166">그런 다음 **for** 루프를 사용하여 각 메시지를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="d7603-166">Then it processes each message using a **for** loop.</span></span> <span data-ttu-id="d7603-167">또한 각 메시지에 대해 표시하지 않는 제한 시간을 5분으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d7603-167">It also sets the invisibility timeout to five minutes for each message.</span></span> <span data-ttu-id="d7603-168">5분은 모든 메시지에 대해 동시에 시작되므로, **get_messages**에 대한 호출 이후로 5분이 지나고 나면 삭제되지 않은 모든 메시지가 다시 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7603-168">Note that the 5 minutes starts for all messages at the same time, so after 5 minutes have passed since the call to **get_messages**, any messages which have not been deleted will become visible again.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Dequeue some queue messages (maximum 32 at a time) and set their visibility timeout to
// 5 minutes (300 seconds).
azure::storage::queue_request_options options;
azure::storage::operation_context context;

// Retrieve 20 messages from the queue with a visibility timeout of 300 seconds.
std::vector<azure::storage::cloud_queue_message> messages = queue.get_messages(20, std::chrono::seconds(300), options, context);

for (auto it = messages.cbegin(); it != messages.cend(); ++it)
{
    // Display the contents of the message.
    std::wcout << U("Get: ") << it->content_as_string() << std::endl;
}
```

## <a name="how-to-get-the-queue-length"></a><span data-ttu-id="d7603-169">방법: 큐 길이 가져오기</span><span class="sxs-lookup"><span data-stu-id="d7603-169">How to: Get the queue length</span></span>
<span data-ttu-id="d7603-170">큐에 있는 메시지의 추정된 개수를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7603-170">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="d7603-171">**download_attributes** 메서드는 메시지 수를 포함하여 큐 특성을 검색하도록 큐 서비스에 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="d7603-171">The **download_attributes** method asks the Queue service to retrieve the queue attributes, including the message count.</span></span> <span data-ttu-id="d7603-172">**approximate_message_count** 메서드는 큐에 메시지의 대략적인 수를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d7603-172">The **approximate_message_count** method gets the approximate number of messages in the queue.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Fetch the queue attributes.
queue.download_attributes();

// Retrieve the cached approximate message count.
int cachedMessageCount = queue.approximate_message_count();

// Display number of messages.
std::wcout << U("Number of messages in queue: ") << cachedMessageCount << std::endl;  
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="d7603-173">방법: 큐 삭제</span><span class="sxs-lookup"><span data-stu-id="d7603-173">How to: Delete a queue</span></span>
<span data-ttu-id="d7603-174">큐 및 해당 큐에 포함된 모든 메시지를 삭제하려면 큐 개체의 **delete_queue_if_exists** 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="d7603-174">To delete a queue and all the messages contained in it, call the **delete_queue_if_exists** method on the queue object.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// If the queue exists and delete it.
queue.delete_queue_if_exists();  
```

## <a name="next-steps"></a><span data-ttu-id="d7603-175">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d7603-175">Next steps</span></span>
<span data-ttu-id="d7603-176">이제 큐 저장소의 기본 사항을 배웠으므로 다음 링크를 따라 Azure 저장소에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="d7603-176">Now that you've learned the basics of Queue storage, follow these links to learn more about Azure Storage.</span></span>

* [<span data-ttu-id="d7603-177">C++에서 Blob 저장소를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="d7603-177">How to use Blob Storage from C++</span></span>](../blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="d7603-178">C++에서 테이블 저장소를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="d7603-178">How to use Table Storage from C++</span></span>](../../cosmos-db/table-storage-how-to-use-c-plus.md)
* [<span data-ttu-id="d7603-179">C++에서 Azure 저장소 리소스 나열</span><span class="sxs-lookup"><span data-stu-id="d7603-179">List Azure Storage Resources in C++</span></span>](../common/storage-c-plus-plus-enumeration.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json)
* [<span data-ttu-id="d7603-180">C++용 Storage Client Library 참조(영문)</span><span class="sxs-lookup"><span data-stu-id="d7603-180">Storage Client Library for C++ Reference</span></span>](http://azure.github.io/azure-storage-cpp)
* [<span data-ttu-id="d7603-181">Azure 저장소 설명서</span><span class="sxs-lookup"><span data-stu-id="d7603-181">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
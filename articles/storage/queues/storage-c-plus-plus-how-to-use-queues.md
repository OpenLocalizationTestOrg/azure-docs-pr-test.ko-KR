---
title: "aaaHow toouse 큐 저장소 (c + +) | Microsoft Docs"
description: "어떻게 toouse hello azure에서 큐 저장소 서비스에 알아봅니다. 샘플은 C++로 작성되었습니다."
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
ms.openlocfilehash: b0cddf017878e9fab87f47d24b2906e40c9f4ad5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-c"></a><span data-ttu-id="c811a-104">어떻게 toouse c + +에서 큐 저장소</span><span class="sxs-lookup"><span data-stu-id="c811a-104">How toouse Queue Storage from C++</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="c811a-105">개요</span><span class="sxs-lookup"><span data-stu-id="c811a-105">Overview</span></span>
<span data-ttu-id="c811a-106">이 가이드 어떻게 tooperform 일반적인 시나리오를 사용 하 여 hello Azure 큐 저장소 서비스에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c811a-106">This guide will show you how tooperform common scenarios using hello Azure Queue storage service.</span></span> <span data-ttu-id="c811a-107">hello 예제 c + +에서 작성 되 고 hello를 사용 하 여 [c + +에 대 한 Azure 저장소 클라이언트 라이브러리](http://github.com/Azure/azure-storage-cpp/blob/master/README.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c811a-107">hello samples are written in C++ and use hello [Azure Storage Client Library for C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span></span> <span data-ttu-id="c811a-108">hello 가이드에서 다루는 시나리오 포함 **삽입**, **관찰**, **가져오는**, 및 **삭제** 메시지를 큐와  **만들기 및 큐 삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="c811a-108">hello scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span>

> [!NOTE]
> <span data-ttu-id="c811a-109">이 가이드의 대상으로 c + + 버전 1.0.0 이상용 Azure 저장소 클라이언트 라이브러리를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="c811a-109">This guide targets hello Azure Storage Client Library for C++ version 1.0.0 and above.</span></span> <span data-ttu-id="c811a-110">hello 권장 버전을 통해 사용할 수 있는 저장소 클라이언트 라이브러리, 2.2.0 [NuGet](http://www.nuget.org/packages/wastorage) 또는 [GitHub](http://github.com/Azure/azure-storage-cpp/)합니다.</span><span class="sxs-lookup"><span data-stu-id="c811a-110">hello recommended version is Storage Client Library 2.2.0, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](http://github.com/Azure/azure-storage-cpp/).</span></span>
> 
> 

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a><span data-ttu-id="c811a-111">C++ 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="c811a-111">Create a C++ application</span></span>
<span data-ttu-id="c811a-112">이 가이드에서는 C++ 응용 프로그램 내에서 실행할 수 있는 저장소 기능을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c811a-112">In this guide, you will use storage features which can be run within a C++ application.</span></span>

<span data-ttu-id="c811a-113">toodo tooinstall, 나오는 c + +에 대 한 Azure 저장소 클라이언트 라이브러리를 hello 및 Azure 구독에 Azure 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c811a-113">toodo so, you will need tooinstall hello Azure Storage Client Library for C++ and create an Azure storage account in your Azure subscription.</span></span>

<span data-ttu-id="c811a-114">Azure 저장소 클라이언트 라이브러리 tooinstall hello c + +에 대 한 hello 다음 메서드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c811a-114">tooinstall hello Azure Storage Client Library for C++, you can use hello following methods:</span></span>

* <span data-ttu-id="c811a-115">**Linux:** hello에 제공 된 hello 지침에 따라 [c + + 추가 정보에 대 한 Azure 저장소 클라이언트 라이브러리](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) 페이지.</span><span class="sxs-lookup"><span data-stu-id="c811a-115">**Linux:** Follow hello instructions given in hello [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>
* <span data-ttu-id="c811a-116">**Windows:** Visual Studio에서 **도구 > NuGet 패키지 관리자 > 패키지 관리자 콘솔**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c811a-116">**Windows:** In Visual Studio, click **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="c811a-117">Hello에 형식 hello 다음 명령은 [NuGet 패키지 관리자 콘솔](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) 누릅니다 **ENTER**합니다.</span><span class="sxs-lookup"><span data-stu-id="c811a-117">Type hello following command into hello [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press **ENTER**.</span></span>

```  
Install-Package wastorage
```

## <a name="configure-your-application-tooaccess-queue-storage"></a><span data-ttu-id="c811a-118">사용자 응용 프로그램 tooaccess 큐 저장소를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c811a-118">Configure your application tooaccess Queue Storage</span></span>
<span data-ttu-id="c811a-119">Hello 다음 포함 toouse hello Azure 저장소 Api tooaccess 큐 저장할 hello c + + 파일의 문 toohello 맨 위에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c811a-119">Add hello following include statements toohello top of hello C++ file where you want toouse hello Azure storage APIs tooaccess queues:</span></span>  

```cpp
#include <was/storage_account.h>
#include <was/queue.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="c811a-120">Azure 저장소 연결 문자열 설정</span><span class="sxs-lookup"><span data-stu-id="c811a-120">Set up an Azure storage connection string</span></span>
<span data-ttu-id="c811a-121">Azure 저장소 클라이언트는 저장소 연결 문자열 toostore 끝점을 사용 하 여 및 데이터 관리 서비스에 액세스 하기 위한 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="c811a-121">An Azure storage client uses a storage connection string toostore endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="c811a-122">형식에 따라, hello에 나열 된 hello 저장소 계정에 대 한 저장소 계정 및 hello 저장소 액세스 키의 hello 이름을 사용 하 여 hello hello 저장소 연결 문자열을 제공 해야, 클라이언트 응용 프로그램에서 실행할 때는 [Azure 포털](https://portal.azure.com)hello에 대 한 *AccountName* 및 *AccountKey* 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c811a-122">When running in a client application, you must provide hello storage connection string in hello following format, using hello name of your storage account and hello storage access key for hello storage account listed in hello [Azure Portal](https://portal.azure.com) for hello *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="c811a-123">저장소 계정 및 액세스 키에 대한 자세한 내용은 [Azure 저장소 계정 정보](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c811a-123">For information on storage accounts and access keys, see [About Azure Storage Accounts](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json).</span></span> <span data-ttu-id="c811a-124">이 예에서는 정적 필드 toohold hello 연결 문자열을 선언할 수는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c811a-124">This example shows how you can declare a static field toohold hello connection string:</span></span>  

```cpp
// Define hello connection-string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

<span data-ttu-id="c811a-125">tootest 응용 프로그램 사용자의 로컬 Windows 컴퓨터에서 Microsoft Azure hello를 사용할 수 있습니다 [저장소 에뮬레이터](../common/storage-use-emulator.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) hello로 설치 된 [Azure SDK](https://azure.microsoft.com/downloads/)합니다.</span><span class="sxs-lookup"><span data-stu-id="c811a-125">tootest your application in your local Windows computer, you can use hello Microsoft Azure [storage emulator](../common/storage-use-emulator.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) that is installed with hello [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="c811a-126">hello 저장소 에뮬레이터는 로컬 개발 컴퓨터에 Azure에서 제공 하는 hello Blob, 큐 및 테이블 서비스를 시뮬레이션 하는 유틸리티입니다.</span><span class="sxs-lookup"><span data-stu-id="c811a-126">hello storage emulator is a utility that simulates hello Blob, Queue, and Table services available in Azure on your local development machine.</span></span> <span data-ttu-id="c811a-127">hello 다음 예제는 어떻게는 정적 필드 toohold hello 연결 문자열 tooyour 로컬 저장소 에뮬레이터를 선언할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c811a-127">hello following example shows how you can declare a static field toohold hello connection string tooyour local storage emulator:</span></span>  

```cpp
// Define hello connection-string with Azure Storage Emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

<span data-ttu-id="c811a-128">toostart hello Azure 저장소 에뮬레이터를 선택 하는 hello **시작** 단추를 클릭 하거나 눌러 hello **Windows** 키입니다.</span><span class="sxs-lookup"><span data-stu-id="c811a-128">toostart hello Azure storage emulator, select hello **Start** button or press hello **Windows** key.</span></span> <span data-ttu-id="c811a-129">입력을 시작 **Azure 저장소 에뮬레이터**를 선택 하 고 **Microsoft Azure 저장소 에뮬레이터** hello 응용 프로그램 목록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="c811a-129">Begin typing **Azure Storage Emulator**, and select **Microsoft Azure Storage Emulator** from hello list of applications.</span></span>

<span data-ttu-id="c811a-130">hello 다음과 같은 샘플 가정 이러한 두 가지 방법 tooget hello 저장소 연결 문자열 중 하나 사용 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="c811a-130">hello following samples assume that you have used one of these two methods tooget hello storage connection string.</span></span>

## <a name="retrieve-your-connection-string"></a><span data-ttu-id="c811a-131">연결 문자열 검색</span><span class="sxs-lookup"><span data-stu-id="c811a-131">Retrieve your connection string</span></span>
<span data-ttu-id="c811a-132">Hello를 사용할 수 있습니다 **cloud_storage_account** 클래스 toorepresent 저장소 계정 정보.</span><span class="sxs-lookup"><span data-stu-id="c811a-132">You can use hello **cloud_storage_account** class toorepresent your Storage Account information.</span></span> <span data-ttu-id="c811a-133">tooretrieve 저장소 계정 hello 저장소 연결 문자열 정보, hello를 사용할 수 있습니다 **구문 분석** 메서드.</span><span class="sxs-lookup"><span data-stu-id="c811a-133">tooretrieve your storage account information from hello storage connection string, you can use hello **parse** method.</span></span>

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

## <a name="how-to-create-a-queue"></a><span data-ttu-id="c811a-134">방법: 큐 만들기</span><span class="sxs-lookup"><span data-stu-id="c811a-134">How to: Create a queue</span></span>
<span data-ttu-id="c811a-135">**cloud_queue_client** 개체를 통해 큐에 대한 참조 개체를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c811a-135">A **cloud_queue_client** object lets you get reference objects for queues.</span></span> <span data-ttu-id="c811a-136">hello 다음 코드에서는 **cloud_queue_client** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="c811a-136">hello following code creates a **cloud_queue_client** object.</span></span>

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create a queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();
```

<span data-ttu-id="c811a-137">사용 하 여 hello **cloud_queue_client** tooget toouse 원하는 참조 toohello 큐 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="c811a-137">Use hello **cloud_queue_client** object tooget a reference toohello queue you want toouse.</span></span> <span data-ttu-id="c811a-138">존재 하지 않는 경우 hello 큐를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c811a-138">You can create hello queue if it doesn't exist.</span></span>

```cpp
// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Create hello queue if it doesn't already exist.
 queue.create_if_not_exists();  
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="c811a-139">방법: 큐에 메시지 삽입</span><span class="sxs-lookup"><span data-stu-id="c811a-139">How to: Insert a message into a queue</span></span>
<span data-ttu-id="c811a-140">tooinsert를 기존 큐에 메시지를 먼저 새로 만들려면 **cloud_queue_message**합니다.</span><span class="sxs-lookup"><span data-stu-id="c811a-140">tooinsert a message into an existing queue, first create a new **cloud_queue_message**.</span></span> <span data-ttu-id="c811a-141">그런 다음 호출 하는 hello **add_message** 메서드.</span><span class="sxs-lookup"><span data-stu-id="c811a-141">Next, call hello **add_message** method.</span></span> <span data-ttu-id="c811a-142">**cloud_queue_message**는 문자열 또는 **바이트** 배열에서 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c811a-142">A **cloud_queue_message** can be created from either a string or a **byte** array.</span></span> <span data-ttu-id="c811a-143">코드 (존재 하지 않는) 하는 경우 큐를 만듦 및 삽입 hello 메시지 'Hello World' 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c811a-143">Here is code which creates a queue (if it doesn't exist) and inserts hello message 'Hello, World':</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Create hello queue if it doesn't already exist.
queue.create_if_not_exists();

// Create a message and add it toohello queue.
azure::storage::cloud_queue_message message1(U("Hello, World"));
queue.add_message(message1);  
```

## <a name="how-to-peek-at-hello-next-message"></a><span data-ttu-id="c811a-144">방법: hello 다음 메시지 피킹</span><span class="sxs-lookup"><span data-stu-id="c811a-144">How to: Peek at hello next message</span></span>
<span data-ttu-id="c811a-145">Hello를 호출 하 여 hello 큐에서 제거 하지 않고 큐의 hello 앞에 hello 메시지를 피킹할 수 있습니다 **peek_message** 메서드.</span><span class="sxs-lookup"><span data-stu-id="c811a-145">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **peek_message** method.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Peek at hello next message.
azure::storage::cloud_queue_message peeked_message = queue.peek_message();

// Output hello message content.
std::wcout << U("Peeked message content: ") << peeked_message.content_as_string() << std::endl;
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a><span data-ttu-id="c811a-146">방법: 대기 중인된 메시지의 hello 내용을 변경</span><span class="sxs-lookup"><span data-stu-id="c811a-146">How to: Change hello contents of a queued message</span></span>
<span data-ttu-id="c811a-147">메시지 전체 hello 큐에서의 hello 내용을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c811a-147">You can change hello contents of a message in-place in hello queue.</span></span> <span data-ttu-id="c811a-148">Hello 메시지 작업 작업을 나타내는 경우에이 기능 tooupdate hello hello 작업 작업의 상태를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c811a-148">If hello message represents a work task, you could use this feature tooupdate hello status of hello work task.</span></span> <span data-ttu-id="c811a-149">코드 다음 hello hello 큐 메시지를 새 내용으로 업데이트 하 고 집합 hello 가시성 제한 시간 tooextend 다른 60 초입니다.</span><span class="sxs-lookup"><span data-stu-id="c811a-149">hello following code updates hello queue message with new contents, and sets hello visibility timeout tooextend another 60 seconds.</span></span> <span data-ttu-id="c811a-150">이 hello 메시지와 관련 된 작업의 hello 상태를 저장 하 고 hello 클라이언트 hello 메시지에서 작업 하는 다른 분 toocontinue를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c811a-150">This saves hello state of work associated with hello message, and gives hello client another minute toocontinue working on hello message.</span></span> <span data-ttu-id="c811a-151">부터 hello toohardware 또는 소프트웨어 오류로 인해 실패 하면 처리 단계를 통해 toostart 필요 없이 큐의 메시지에이 기술을 tootrack multi-step 워크플로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c811a-151">You could use this technique tootrack multi-step workflows on queue messages, without having toostart over from hello beginning if a processing step fails due toohardware or software failure.</span></span> <span data-ttu-id="c811a-152">일반적으로는 다시 시도 횟수를 보관할 때 고 hello 메시지를 여러 개 n 번 다시 시도 하는 경우 파일을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="c811a-152">Typically, you would keep a retry count as well, and if hello message is retried more than n times, you would delete it.</span></span> <span data-ttu-id="c811a-153">이 기능은 처리될 때마다 응용 프로그램 오류를 트리거하는 메시지를 차단하여 보호해 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c811a-153">This protects against a message that triggers an application error each time it is processed.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_conection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Get hello message from hello queue and update hello message contents.
// hello visibility timeout "0" means make it visible immediately.
// hello visibility timeout "60" means hello client can get another minute toocontinue
// working on hello message.
azure::storage::cloud_queue_message changed_message = queue.get_message();

changed_message.set_content(U("Changed message"));
queue.update_message(changed_message, std::chrono::seconds(60), true);

// Output hello message content.
std::wcout << U("Changed message content: ") << changed_message.content_as_string() << std::endl;  
```

## <a name="how-to-de-queue-hello-next-message"></a><span data-ttu-id="c811a-154">방법: hello 다음 메시지 큐에서 제거</span><span class="sxs-lookup"><span data-stu-id="c811a-154">How to: De-queue hello next message</span></span>
<span data-ttu-id="c811a-155">다음 코드는 2단계를 거쳐 큐에서 메시지를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="c811a-155">Your code de-queues a message from a queue in two steps.</span></span> <span data-ttu-id="c811a-156">호출 하는 경우 **get_message**, 큐에 있는 hello 다음 메시지를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c811a-156">When you call **get_message**, you get hello next message in a queue.</span></span> <span data-ttu-id="c811a-157">반환 된 메시지 **get_message** 보이지 않는 tooany이이 큐에서 메시지를 읽을 다른 코드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c811a-157">A message returned from **get_message** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="c811a-158">toofinish 제거 hello 큐에서에서 메시지를 hello 호출 해야 **delete_message**합니다.</span><span class="sxs-lookup"><span data-stu-id="c811a-158">toofinish removing hello message from hello queue, you must also call **delete_message**.</span></span> <span data-ttu-id="c811a-159">이 2 단계 프로세스의 메시지를 제거 하는 코드 tooprocess toohardware 또는 소프트웨어 오류가, 코드의 다른 인스턴스는 메시지를 가져올 수 없으면 동일한 메시지 hello 고 다시 시도 하십시오 보장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c811a-159">This two-step process of removing a message assures that if your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="c811a-160">코드 호출 **delete_message** 직후 hello 메시지를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="c811a-160">Your code calls **delete_message** right after hello message has been processed.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Get hello next message.
azure::storage::cloud_queue_message dequeued_message = queue.get_message();
std::wcout << U("Dequeued message: ") << dequeued_message.content_as_string() << std::endl;

// Delete hello message.
queue.delete_message(dequeued_message);
```

## <a name="how-to-leverage-additional-options-for-de-queuing-messages"></a><span data-ttu-id="c811a-161">방법: 큐에서 메시지를 제거하는 추가 옵션 활용</span><span class="sxs-lookup"><span data-stu-id="c811a-161">How to: Leverage additional options for de-queuing messages</span></span>
<span data-ttu-id="c811a-162">큐에서 메시지 검색을 사용자 지정할 수 있는 방법으로는 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c811a-162">There are two ways you can customize message retrieval from a queue.</span></span> <span data-ttu-id="c811a-163">첫째, 일괄 처리 메시지 (위쪽 too32)을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c811a-163">First, you can get a batch of messages (up too32).</span></span> <span data-ttu-id="c811a-164">둘째, 하면 프로그램 코드를 더 길거나 더 짧은 표시 안 함 시간 제한이 설정할 수 있습니다 또는 적은 시간 toofully 각 메시지를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="c811a-164">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span> <span data-ttu-id="c811a-165">hello 다음 코드 예제에서는 hello **get_messages** 메서드 tooget 20 메시지 한 번 호출에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="c811a-165">hello following code example uses hello **get_messages** method tooget 20 messages in one call.</span></span> <span data-ttu-id="c811a-166">그런 다음 **for** 루프를 사용하여 각 메시지를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="c811a-166">Then it processes each message using a **for** loop.</span></span> <span data-ttu-id="c811a-167">또한 각 메시지에 대 한 hello 표시 안 함 시간 초과 toofive 분을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c811a-167">It also sets hello invisibility timeout toofive minutes for each message.</span></span> <span data-ttu-id="c811a-168">5 분 해당 hello 참고 hello에서 모든 메시지에 대 한 시작 시간이, 하므로 5 분 이후 경과한 hello 호출 너무 나면**get_messages**, 모든 메시지는 삭제 되지 않았으므로 다시 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c811a-168">Note that hello 5 minutes starts for all messages at hello same time, so after 5 minutes have passed since hello call too**get_messages**, any messages which have not been deleted will become visible again.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Dequeue some queue messages (maximum 32 at a time) and set their visibility timeout to
// 5 minutes (300 seconds).
azure::storage::queue_request_options options;
azure::storage::operation_context context;

// Retrieve 20 messages from hello queue with a visibility timeout of 300 seconds.
std::vector<azure::storage::cloud_queue_message> messages = queue.get_messages(20, std::chrono::seconds(300), options, context);

for (auto it = messages.cbegin(); it != messages.cend(); ++it)
{
    // Display hello contents of hello message.
    std::wcout << U("Get: ") << it->content_as_string() << std::endl;
}
```

## <a name="how-to-get-hello-queue-length"></a><span data-ttu-id="c811a-169">방법: hello 큐 길이 가져오기</span><span class="sxs-lookup"><span data-stu-id="c811a-169">How to: Get hello queue length</span></span>
<span data-ttu-id="c811a-170">큐에 있는 hello 메시지 수의 예측을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c811a-170">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="c811a-171">hello **download_attributes** 메서드 hello 큐 서비스 tooretrieve hello 메시지 수를 포함 된 hello 큐 특성을 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="c811a-171">hello **download_attributes** method asks hello Queue service tooretrieve hello queue attributes, including hello message count.</span></span> <span data-ttu-id="c811a-172">hello **approximate_message_count** 메서드 hello 큐에 있는 hello 대략적인 메시지 수를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c811a-172">hello **approximate_message_count** method gets hello approximate number of messages in hello queue.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Fetch hello queue attributes.
queue.download_attributes();

// Retrieve hello cached approximate message count.
int cachedMessageCount = queue.approximate_message_count();

// Display number of messages.
std::wcout << U("Number of messages in queue: ") << cachedMessageCount << std::endl;  
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="c811a-173">방법: 큐 삭제</span><span class="sxs-lookup"><span data-stu-id="c811a-173">How to: Delete a queue</span></span>
<span data-ttu-id="c811a-174">큐와 모든 hello 메시지에 포함 된, 호출 hello toodelete **delete_queue_if_exists** hello 큐 개체에서 메서드.</span><span class="sxs-lookup"><span data-stu-id="c811a-174">toodelete a queue and all hello messages contained in it, call hello **delete_queue_if_exists** method on hello queue object.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// If hello queue exists and delete it.
queue.delete_queue_if_exists();  
```

## <a name="next-steps"></a><span data-ttu-id="c811a-175">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c811a-175">Next steps</span></span>
<span data-ttu-id="c811a-176">큐 저장소의 hello 기본 사항 학습 한, 했으므로 이러한 링크 toolearn Azure 저장소에 대 한 자세한를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c811a-176">Now that you've learned hello basics of Queue storage, follow these links toolearn more about Azure Storage.</span></span>

* [<span data-ttu-id="c811a-177">어떻게 toouse c + +에서 Blob 저장소</span><span class="sxs-lookup"><span data-stu-id="c811a-177">How toouse Blob Storage from C++</span></span>](../blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="c811a-178">어떻게 toouse c + +에서 테이블 저장소</span><span class="sxs-lookup"><span data-stu-id="c811a-178">How toouse Table Storage from C++</span></span>](../../cosmos-db/table-storage-how-to-use-c-plus.md)
* [<span data-ttu-id="c811a-179">C++에서 Azure 저장소 리소스 나열</span><span class="sxs-lookup"><span data-stu-id="c811a-179">List Azure Storage Resources in C++</span></span>](../common/storage-c-plus-plus-enumeration.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json)
* [<span data-ttu-id="c811a-180">C++용 Storage Client Library 참조(영문)</span><span class="sxs-lookup"><span data-stu-id="c811a-180">Storage Client Library for C++ Reference</span></span>](http://azure.github.io/azure-storage-cpp)
* [<span data-ttu-id="c811a-181">Azure 저장소 설명서</span><span class="sxs-lookup"><span data-stu-id="c811a-181">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
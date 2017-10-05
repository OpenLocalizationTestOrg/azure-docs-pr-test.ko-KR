---
title: "C++에서 Blob Storage(개체 저장소)를 사용하는 방법 | Microsoft Docs"
description: "Azure Blob 저장소(개체 저장소)를 사용하여 클라우드에 구조화되지 않은 데이터를 저장합니다."
services: storage
documentationcenter: .net
author: michaelhauss
manager: vamshik
editor: tysonn
ms.assetid: 53844120-1c48-4e2f-8f77-5359ed0147a4
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: michaelhauss
ms.openlocfilehash: daf480b7be78dc001712010eac6386d4744c3c1d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-blob-storage-from-c"></a><span data-ttu-id="f5de2-103">C++에서 Blob 저장소를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="f5de2-103">How to use Blob Storage from C++</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="f5de2-104">개요</span><span class="sxs-lookup"><span data-stu-id="f5de2-104">Overview</span></span>
<span data-ttu-id="f5de2-105">Azure Blob 저장소는 클라우드에 구조화되지 않은 데이터를 개체/Blob로 저장하는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="f5de2-105">Azure Blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span></span> <span data-ttu-id="f5de2-106">Blob 저장소는 문서, 미디어 파일 또는 응용 프로그램 설치 프로그램과 같은 모든 종류의 텍스트 또는 이진 데이터를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5de2-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="f5de2-107">또한 Blob 저장소를 개체 저장소라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5de2-107">Blob storage is also referred to as object storage.</span></span>

<span data-ttu-id="f5de2-108">이 가이드에서는 Azure Blob 저장소 서비스를 사용하여 일반 시나리오를 수행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f5de2-108">This guide will demonstrate how to perform common scenarios using the Azure Blob storage service.</span></span> <span data-ttu-id="f5de2-109">샘플은 C++로 작성되었으며 [Azure Storage Client Library for C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f5de2-109">The samples are written in C++ and use the [Azure Storage Client Library for C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span></span> <span data-ttu-id="f5de2-110">여기서 다루는 시나리오에는 Blob **업로드**, **나열**, **다운로드** 및 **삭제**가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5de2-110">The scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span>  

> [!NOTE]
> <span data-ttu-id="f5de2-111">이 가이드는 Azure Storage Client Library for C++ 버전 1.0.0 이상을 대상으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5de2-111">This guide targets the Azure Storage Client Library for C++ version 1.0.0 and above.</span></span> <span data-ttu-id="f5de2-112">권장되는 버전은 Storage Client Library 2.2.0이며, [NuGet](http://www.nuget.org/packages/wastorage) 또는 [GitHub](https://github.com/Azure/azure-storage-cpp)를 통해 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="f5de2-112">The recommended version is Storage Client Library 2.2.0, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](https://github.com/Azure/azure-storage-cpp).</span></span>
> 
> 

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a><span data-ttu-id="f5de2-113">C++ 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="f5de2-113">Create a C++ application</span></span>
<span data-ttu-id="f5de2-114">이 가이드에서는 C++ 응용 프로그램 내에서 실행할 수 있는 저장소 기능을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f5de2-114">In this guide, you will use storage features which can be run within a C++ application.</span></span>  

<span data-ttu-id="f5de2-115">이 기능을 사용하려면, Azure Storage Client Library for C++를 설치하고 Azure 구독에서 Azure 저장소 계정을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5de2-115">To do so, you will need to install the Azure Storage Client Library for C++ and create an Azure storage account in your Azure subscription.</span></span>   

<span data-ttu-id="f5de2-116">Azure Storage Client Library for C++를 설치하려면 다음 메서드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5de2-116">To install the Azure Storage Client Library for C++, you can use the following methods:</span></span>

* <span data-ttu-id="f5de2-117">**Linux:**[Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) 페이지의 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="f5de2-117">**Linux:** Follow the instructions given in the [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>  
* <span data-ttu-id="f5de2-118">**Windows:** Visual Studio에서 **도구 > NuGet 패키지 관리자 > 패키지 관리자 콘솔**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f5de2-118">**Windows:** In Visual Studio, click **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="f5de2-119">[NuGet 패키지 관리자 콘솔](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) 에 다음 명령을 입력하고 **ENTER**를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="f5de2-119">Type the following command into the [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press **ENTER**.</span></span>  
  
     <span data-ttu-id="f5de2-120">Install-Package wastorage</span><span class="sxs-lookup"><span data-stu-id="f5de2-120">Install-Package wastorage</span></span>

## <a name="configure-your-application-to-access-blob-storage"></a><span data-ttu-id="f5de2-121">Blob 저장소에 액세스하도록 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="f5de2-121">Configure your application to access Blob Storage</span></span>
<span data-ttu-id="f5de2-122">Azure 저장소 API를 사용하여 Blob에 액세스하려는 C++ 파일의 맨 위에 다음 include 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f5de2-122">Add the following include statements to the top of the C++ file where you want to use the Azure storage APIs to access blobs:</span></span>  

```cpp
#include <was/storage_account.h>
#include <was/blob.h>
```

## <a name="setup-an-azure-storage-connection-string"></a><span data-ttu-id="f5de2-123">Azure 저장소 연결 문자열 설정</span><span class="sxs-lookup"><span data-stu-id="f5de2-123">Setup an Azure storage connection string</span></span>
<span data-ttu-id="f5de2-124">Azure 저장소 클라이언트는 저장소 연결 문자열을 사용하여 데이터 관리 서비스에 액세스하기 위한 끝점 및 자격 증명을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f5de2-124">An Azure storage client uses a storage connection string to store endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="f5de2-125">클라이언트 응용 프로그램에서 실행할 경우, 저장소 계정의 이름 및 [Azure Portal](https://portal.azure.com)에 나열된 저장소 계정의 저장소 액세스 키를 *AccountName* 및 *AccountKey* 값에 사용하여 다음 형식의 저장소 연결 문자열을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5de2-125">When running in a client application, you must provide the storage connection string in the following format, using the name of your storage account and the storage access key for the storage account listed in the [Azure Portal](https://portal.azure.com) for the *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="f5de2-126">저장소 계정 및 액세스 키에 대한 자세한 내용은 [Azure 저장소 계정 정보](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f5de2-126">For information on storage accounts and access keys, see [About Azure Storage Accounts](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span></span> <span data-ttu-id="f5de2-127">이 예제는 정적 필드가 연결 문자열을 포함할 수 있도록 선언하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f5de2-127">This example shows how you can declare a static field to hold the connection string:</span></span>  

```cpp
// Define the connection-string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

<span data-ttu-id="f5de2-128">로컬 Windows 컴퓨터에서 응용 프로그램을 테스트 하려면 [Azure SDK](https://azure.microsoft.com/downloads/)와 함께 설치된 Microsoft Azure [Storage 에뮬레이터](../storage-use-emulator.md)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5de2-128">To test your application in your local Windows computer, you can use the Microsoft Azure [storage emulator](../storage-use-emulator.md) that is installed with the [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="f5de2-129">저장소 에뮬레이터는 로컬 개발 컴퓨터의Azure에서 사용할 수 있는 Blob, 큐 및 테이블 서비스를 시뮬레이션하는 유틸리티입니다.</span><span class="sxs-lookup"><span data-stu-id="f5de2-129">The storage emulator is a utility that simulates the Blob, Queue, and Table services available in Azure on your local development machine.</span></span> <span data-ttu-id="f5de2-130">다음 예제에서는 로컬 저장소 에뮬레이터에 연결 문자열을 포함할 수 있도록 정적 필드를 선언하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="f5de2-130">The following example shows how you can declare a static field to hold the connection string to your local storage emulator:</span></span>

```cpp
// Define the connection-string with Azure Storage Emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

<span data-ttu-id="f5de2-131">Azure Storage 에뮬레이터를 시작하려면 **시작** 단추를 선택하거나 **Windows** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="f5de2-131">To start the Azure storage emulator, Select the **Start** button or press the **Windows** key.</span></span> <span data-ttu-id="f5de2-132">**Azure Storage 에뮬레이터** 입력을 시작하고 응용 프로그램 목록에서 **Microsoft Azure Storage 에뮬레이터**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f5de2-132">Begin typing **Azure Storage Emulator**, and select **Microsoft Azure Storage Emulator** from the list of applications.</span></span>  

<span data-ttu-id="f5de2-133">다음 샘플에서는 저장소 연결 문자열을 가져오기 위해 위의 두 메서드 중 하나를 사용한 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="f5de2-133">The following samples assume that you have used one of these two methods to get the storage connection string.</span></span>  

## <a name="retrieve-your-connection-string"></a><span data-ttu-id="f5de2-134">연결 문자열 검색</span><span class="sxs-lookup"><span data-stu-id="f5de2-134">Retrieve your connection string</span></span>
<span data-ttu-id="f5de2-135">**cloud_storage_account** 클래스를 사용하여 저장소 계정 정보를 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5de2-135">You can use the **cloud_storage_account** class to represent your Storage Account information.</span></span> <span data-ttu-id="f5de2-136">저장소 연결 문자열에서 저장소 계정 정보를 검색하려면 **구문 분석** 메서드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5de2-136">To retrieve your storage account information from the storage connection string, you can use the **parse** method.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

<span data-ttu-id="f5de2-137">다음으로, Blob Storage 서비스에 저장된 Blob과 컨테이너를 나타내는 개체를 검색할 수 있도록 **cloud_blob_client** 클래스에 대한 참조를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f5de2-137">Next, get a reference to a **cloud_blob_client** class as it allows you to retrieve objects that represent containers and blobs stored within the Blob Storage Service.</span></span> <span data-ttu-id="f5de2-138">다음 코드는 위에서 검색한 저장소 계정 개체를 사용하여 **cloud_blob_client** 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f5de2-138">The following code creates a **cloud_blob_client** object using the storage account object we retrieved above:</span></span>  

```cpp
// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();  
```

## <a name="how-to-create-a-container"></a><span data-ttu-id="f5de2-139">방법: 컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="f5de2-139">How to: Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="f5de2-140">이 예제에서는 컨테이너가 없는 경우 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f5de2-140">This example shows how to create a container if it does not already exist:</span></span>  

```cpp
try
{
    // Retrieve storage account from connection string.
    azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

    // Create the blob client.
    azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

    // Retrieve a reference to a container.
    azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

    // Create the container if it doesn't already exist.
    container.create_if_not_exists();
}
catch (const std::exception& e)
{
    std::wcout << U("Error: ") << e.what() << std::endl;
}  
```

<span data-ttu-id="f5de2-141">기본적으로 새 컨테이너는 전용이며, 이 컨테이너에서 Blob을 다운로드하려면 저장소 액세스 키를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5de2-141">By default, the new container is private and you must specify your storage access key to download blobs from this container.</span></span> <span data-ttu-id="f5de2-142">컨테이너 내의 파일(Blob)을 모든 사용자가 사용할 수 있게 하려는 경우 다음 코드를 사용하여 컨테이너를 공용으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5de2-142">If you want to make the files (blobs) within the container available to everyone, you can set the container to be public using the following code:</span></span>  

```cpp
// Make the blob container publicly accessible.
azure::storage::blob_container_permissions permissions;
permissions.set_public_access(azure::storage::blob_container_public_access_type::blob);
container.upload_permissions(permissions);  
```

<span data-ttu-id="f5de2-143">인터넷상의 누구든지 공용 컨테이너의 Blob을 볼 수 있지만 해당 액세스 키가 있는 경우에만 수정하거나 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5de2-143">Anyone on the Internet can see blobs in a public container, but you can modify or delete them only if you have the appropriate access key.</span></span>  

## <a name="how-to-upload-a-blob-into-a-container"></a><span data-ttu-id="f5de2-144">방법: 컨테이너에 Blob 업로드</span><span class="sxs-lookup"><span data-stu-id="f5de2-144">How to: Upload a blob into a container</span></span>
<span data-ttu-id="f5de2-145">Azure Blob 저장소는 블록 Blob 및 페이지 Blob을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="f5de2-145">Azure Blob Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="f5de2-146">대부분의 경우 블록 Blob을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f5de2-146">In the majority of cases, block blob is the recommended type to use.</span></span>  

<span data-ttu-id="f5de2-147">블록 Blob에 파일을 업로드하려면 컨테이너 참조를 가져온 다음 이 참조를 사용하여 블록 Blob 참조를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f5de2-147">To upload a file to a block blob, get a container reference and use it to get a block blob reference.</span></span> <span data-ttu-id="f5de2-148">Blob 참조가 있는 경우 **upload_from_stream** 메서드를 호출하여 데이터 스트림을 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5de2-148">Once you have a blob reference, you can upload any stream of data to it by calling the **upload_from_stream** method.</span></span> <span data-ttu-id="f5de2-149">이 작업은 Blob이 없는 경우 새로 만들고, Blob이 있는 경우 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="f5de2-149">This operation will create the blob if it didn't previously exist, or overwrite it if it does exist.</span></span> <span data-ttu-id="f5de2-150">다음 예제에서는 컨테이너에 Blob을 업로드하는 방법을 보여 주며, 컨테이너가 이미 만들어져 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="f5de2-150">The following example shows how to upload a blob into a container and assumes that the container was already created.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference to a previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference to a blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Create or overwrite the "my-blob-1" blob with contents from a local file.
concurrency::streams::istream input_stream = concurrency::streams::file_stream<uint8_t>::open_istream(U("DataFile.txt")).get();
blockBlob.upload_from_stream(input_stream);
input_stream.close().wait();

// Create or overwrite the "my-blob-2" and "my-blob-3" blobs with contents from text.
// Retrieve a reference to a blob named "my-blob-2".
azure::storage::cloud_block_blob blob2 = container.get_block_blob_reference(U("my-blob-2"));
blob2.upload_text(U("more text"));

// Retrieve a reference to a blob named "my-blob-3".
azure::storage::cloud_block_blob blob3 = container.get_block_blob_reference(U("my-directory/my-sub-directory/my-blob-3"));
blob3.upload_text(U("other text"));  
```

<span data-ttu-id="f5de2-151">또는, **upload_from_file** 메서드를 사용하여 블록 Blob에 파일을 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5de2-151">Alternatively, you can use the **upload_from_file** method to upload a file to a block blob.</span></span>

## <a name="how-to-list-the-blobs-in-a-container"></a><span data-ttu-id="f5de2-152">방법: 컨테이너에 Blob 나열</span><span class="sxs-lookup"><span data-stu-id="f5de2-152">How to: List the blobs in a container</span></span>
<span data-ttu-id="f5de2-153">컨테이너의 Blob을 나열하려면 먼저 컨테이너 참조를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f5de2-153">To list the blobs in a container, first get a container reference.</span></span> <span data-ttu-id="f5de2-154">컨테이너의 **list_blobs** 메서드를 사용하여 컨테이너 내의 Blob 및/또는 디렉터리를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5de2-154">You can then use the container's **list_blobs** method to retrieve the blobs and/or directories within it.</span></span> <span data-ttu-id="f5de2-155">반환된 **list_blob_item**의 메서드 및 다양한 속성에 액세스하려면 **cloud_blob** 개체를 가져오는 **list_blob_item.as_blob** 메서드를 호출하거나, cloud_blob_directory 개체를 가져오는**list_blob.as_directory** 메서드를 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5de2-155">To access the rich set of properties and methods for a returned **list_blob_item**, you must call the **list_blob_item.as_blob** method to get a  **cloud_blob** object, or the **list_blob.as_directory** method to get a  cloud_blob_directory object.</span></span> <span data-ttu-id="f5de2-156">다음 코드는 **my-sample-container** 컨테이너에 있는 각 항목의 URI를 검색하고 출력하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f5de2-156">The following code demonstrates how to retrieve and output the URI of each item in the **my-sample-container** container:</span></span>

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference to a previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Output URI of each item.
azure::storage::list_blob_item_iterator end_of_results;
for (auto it = container.list_blobs(); it != end_of_results; ++it)
{
    if (it->is_blob())
    {
        std::wcout << U("Blob: ") << it->as_blob().uri().primary_uri().to_string() << std::endl;
    }
    else
    {
        std::wcout << U("Directory: ") << it->as_directory().uri().primary_uri().to_string() << std::endl;
    }
}
```

<span data-ttu-id="f5de2-157">작업 나열에 대한 자세한 내용은 [C++에서 Azure 저장소 리소스 나열](../storage-c-plus-plus-enumeration.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f5de2-157">For more details on listing operations, see [List Azure Storage Resources in C++](../storage-c-plus-plus-enumeration.md).</span></span>

## <a name="how-to-download-blobs"></a><span data-ttu-id="f5de2-158">방법: Blob 다운로드</span><span class="sxs-lookup"><span data-stu-id="f5de2-158">How to: Download blobs</span></span>
<span data-ttu-id="f5de2-159">Blob을 다운로드하려면 먼저 Blob 참조를 검색한 다음 **download_to_stream** 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="f5de2-159">To download blobs, first retrieve a blob reference and then call the **download_to_stream** method.</span></span> <span data-ttu-id="f5de2-160">다음 예제에서는 **download_to_stream** 메서드를 사용하여 Blob 콘텐츠를 스트림 개체로 전송한 다음 이 개체를 로컬 파일에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5de2-160">The following example uses the **download_to_stream** method to transfer the blob contents to a stream object that you can then persist to a local file.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference to a previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference to a blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Save blob contents to a file.
concurrency::streams::container_buffer<std::vector<uint8_t>> buffer;
concurrency::streams::ostream output_stream(buffer);
blockBlob.download_to_stream(output_stream);

std::ofstream outfile("DownloadBlobFile.txt", std::ofstream::binary);
std::vector<unsigned char>& data = buffer.collection();

outfile.write((char *)&data[0], buffer.size());
outfile.close();  
```

<span data-ttu-id="f5de2-161">또는 **download_to_file** 메서드를 사용하여 Blob의 콘텐츠를 파일에 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5de2-161">Alternatively, you can use the **download_to_file** method to download the contents of a blob to a file.</span></span>
<span data-ttu-id="f5de2-162">또한 **download_text** 메서드를 사용하여 Blob 콘텐츠를 텍스트 문자열로 다운로드할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5de2-162">In addition, you can also use the **download_text** method to download the contents of a blob as a text string.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference to a previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference to a blob named "my-blob-2".
azure::storage::cloud_block_blob text_blob = container.get_block_blob_reference(U("my-blob-2"));

// Download the contents of a blog as a text string.
utility::string_t text = text_blob.download_text();
```

## <a name="how-to-delete-blobs"></a><span data-ttu-id="f5de2-163">방법: Blob 삭제</span><span class="sxs-lookup"><span data-stu-id="f5de2-163">How to: Delete blobs</span></span>
<span data-ttu-id="f5de2-164">Blob을 삭제하려면 먼저 Blob 참조를 가져온 다음 **delete_blob** 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="f5de2-164">To delete a blob, first get a blob reference and then call the **delete_blob** method on it.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference to a previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference to a blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Delete the blob.
blockBlob.delete_blob();
```

## <a name="next-steps"></a><span data-ttu-id="f5de2-165">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f5de2-165">Next steps</span></span>
<span data-ttu-id="f5de2-166">이제 Blob 저장소의 기본 사항을 배웠으므로 다음 링크를 따라 Azure 저장소 작업에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="f5de2-166">Now that you've learned the basics of blob storage, follow these links to learn more about Azure Storage.</span></span>  

* [<span data-ttu-id="f5de2-167">C++에서 큐 저장소를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="f5de2-167">How to use Queue Storage from C++</span></span>](../storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="f5de2-168">C++에서 테이블 저장소를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="f5de2-168">How to use Table Storage from C++</span></span>](../../cosmos-db/table-storage-how-to-use-c-plus.md)
* [<span data-ttu-id="f5de2-169">C++에서 Azure 저장소 리소스 나열</span><span class="sxs-lookup"><span data-stu-id="f5de2-169">List Azure Storage Resources in C++</span></span>](../storage-c-plus-plus-enumeration.md)
* [<span data-ttu-id="f5de2-170">C++용 Storage Client Library 참조(영문)</span><span class="sxs-lookup"><span data-stu-id="f5de2-170">Storage Client Library for C++ Reference</span></span>](http://azure.github.io/azure-storage-cpp)
* [<span data-ttu-id="f5de2-171">Azure 저장소 설명서</span><span class="sxs-lookup"><span data-stu-id="f5de2-171">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
* [<span data-ttu-id="f5de2-172">AzCopy 명령줄 유틸리티로 데이터 전송</span><span class="sxs-lookup"><span data-stu-id="f5de2-172">Transfer data with the AzCopy command-line utility</span></span>](../storage-use-azcopy.md)


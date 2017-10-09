---
title: "c + +에서 aaaHow toouse blob 저장소 (개체 저장소) | Microsoft Docs"
description: "Azure Blob 저장소 (개체 저장소)를 사용 하는 hello 클라우드에 구조화 되지 않은 데이터를 저장 합니다."
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
ms.openlocfilehash: e63df4683e5c10c9f8fbe4106c655df61be0e1a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-c"></a><span data-ttu-id="8c857-103">어떻게 toouse c + +에서 Blob 저장소</span><span class="sxs-lookup"><span data-stu-id="8c857-103">How toouse Blob Storage from C++</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="8c857-104">개요</span><span class="sxs-lookup"><span data-stu-id="8c857-104">Overview</span></span>
<span data-ttu-id="8c857-105">Azure Blob 저장소는 hello 클라우드에서 개체/blob으로 구조화 되지 않은 데이터를 저장 하는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="8c857-105">Azure Blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="8c857-106">Blob storage는 문서, 미디어 파일 또는 응용 프로그램 설치 프로그램과 같은 모든 종류의 텍스트 또는 이진 데이터를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c857-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="8c857-107">Blob 저장소 참조 tooas 개체 저장소 이기도합니다.</span><span class="sxs-lookup"><span data-stu-id="8c857-107">Blob storage is also referred tooas object storage.</span></span>

<span data-ttu-id="8c857-108">이 가이드에서는 tooperform 일반적인 시나리오를 사용 하 여 Azure Blob 저장소 서비스를 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8c857-108">This guide will demonstrate how tooperform common scenarios using hello Azure Blob storage service.</span></span> <span data-ttu-id="8c857-109">hello 예제 c + +에서 작성 되 고 hello를 사용 하 여 [c + +에 대 한 Azure 저장소 클라이언트 라이브러리](http://github.com/Azure/azure-storage-cpp/blob/master/README.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8c857-109">hello samples are written in C++ and use hello [Azure Storage Client Library for C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span></span> <span data-ttu-id="8c857-110">hello 가이드에서 다루는 시나리오 포함 **업로드**, **나열**, **다운로드**, 및 **삭제** blob입니다.</span><span class="sxs-lookup"><span data-stu-id="8c857-110">hello scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span>  

> [!NOTE]
> <span data-ttu-id="8c857-111">이 가이드의 대상으로 c + + 버전 1.0.0 이상용 Azure 저장소 클라이언트 라이브러리를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c857-111">This guide targets hello Azure Storage Client Library for C++ version 1.0.0 and above.</span></span> <span data-ttu-id="8c857-112">hello 권장 버전을 통해 사용할 수 있는 저장소 클라이언트 라이브러리, 2.2.0 [NuGet](http://www.nuget.org/packages/wastorage) 또는 [GitHub](https://github.com/Azure/azure-storage-cpp)합니다.</span><span class="sxs-lookup"><span data-stu-id="8c857-112">hello recommended version is Storage Client Library 2.2.0, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](https://github.com/Azure/azure-storage-cpp).</span></span>
> 
> 

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a><span data-ttu-id="8c857-113">C++ 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="8c857-113">Create a C++ application</span></span>
<span data-ttu-id="8c857-114">이 가이드에서는 C++ 응용 프로그램 내에서 실행할 수 있는 저장소 기능을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8c857-114">In this guide, you will use storage features which can be run within a C++ application.</span></span>  

<span data-ttu-id="8c857-115">toodo tooinstall, 나오는 c + +에 대 한 Azure 저장소 클라이언트 라이브러리를 hello 및 Azure 구독에 Azure 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8c857-115">toodo so, you will need tooinstall hello Azure Storage Client Library for C++ and create an Azure storage account in your Azure subscription.</span></span>   

<span data-ttu-id="8c857-116">Azure 저장소 클라이언트 라이브러리 tooinstall hello c + +에 대 한 hello 다음 메서드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c857-116">tooinstall hello Azure Storage Client Library for C++, you can use hello following methods:</span></span>

* <span data-ttu-id="8c857-117">**Linux:** hello에 제공 된 hello 지침에 따라 [c + + 추가 정보에 대 한 Azure 저장소 클라이언트 라이브러리](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) 페이지.</span><span class="sxs-lookup"><span data-stu-id="8c857-117">**Linux:** Follow hello instructions given in hello [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>  
* <span data-ttu-id="8c857-118">**Windows:** Visual Studio에서 **도구 > NuGet 패키지 관리자 > 패키지 관리자 콘솔**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8c857-118">**Windows:** In Visual Studio, click **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="8c857-119">Hello에 형식 hello 다음 명령은 [NuGet 패키지 관리자 콘솔](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) 누릅니다 **ENTER**합니다.</span><span class="sxs-lookup"><span data-stu-id="8c857-119">Type hello following command into hello [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press **ENTER**.</span></span>  
  
     <span data-ttu-id="8c857-120">Install-Package wastorage</span><span class="sxs-lookup"><span data-stu-id="8c857-120">Install-Package wastorage</span></span>

## <a name="configure-your-application-tooaccess-blob-storage"></a><span data-ttu-id="8c857-121">사용자 응용 프로그램 tooaccess Blob 저장소 구성</span><span class="sxs-lookup"><span data-stu-id="8c857-121">Configure your application tooaccess Blob Storage</span></span>
<span data-ttu-id="8c857-122">Hello 다음 포함 toouse hello Azure 저장소 Api tooaccess blob 저장할 hello c + + 파일의 문 toohello 맨 위에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c857-122">Add hello following include statements toohello top of hello C++ file where you want toouse hello Azure storage APIs tooaccess blobs:</span></span>  

```cpp
#include <was/storage_account.h>
#include <was/blob.h>
```

## <a name="setup-an-azure-storage-connection-string"></a><span data-ttu-id="8c857-123">Azure 저장소 연결 문자열 설정</span><span class="sxs-lookup"><span data-stu-id="8c857-123">Setup an Azure storage connection string</span></span>
<span data-ttu-id="8c857-124">Azure 저장소 클라이언트는 저장소 연결 문자열 toostore 끝점을 사용 하 여 및 데이터 관리 서비스에 액세스 하기 위한 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="8c857-124">An Azure storage client uses a storage connection string toostore endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="8c857-125">형식에 따라, hello에 나열 된 hello 저장소 계정에 대 한 저장소 계정 및 hello 저장소 액세스 키의 hello 이름을 사용 하 여 hello hello 저장소 연결 문자열을 제공 해야, 클라이언트 응용 프로그램에서 실행할 때는 [Azure 포털](https://portal.azure.com)hello에 대 한 *AccountName* 및 *AccountKey* 값입니다.</span><span class="sxs-lookup"><span data-stu-id="8c857-125">When running in a client application, you must provide hello storage connection string in hello following format, using hello name of your storage account and hello storage access key for hello storage account listed in hello [Azure Portal](https://portal.azure.com) for hello *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="8c857-126">저장소 계정 및 액세스 키에 대한 자세한 내용은 [Azure 저장소 계정 정보](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8c857-126">For information on storage accounts and access keys, see [About Azure Storage Accounts](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span></span> <span data-ttu-id="8c857-127">이 예에서는 정적 필드 toohold hello 연결 문자열을 선언할 수는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8c857-127">This example shows how you can declare a static field toohold hello connection string:</span></span>  

```cpp
// Define hello connection-string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

<span data-ttu-id="8c857-128">tootest 응용 프로그램 사용자의 로컬 Windows 컴퓨터에서 Microsoft Azure hello를 사용할 수 있습니다 [저장소 에뮬레이터](../storage-use-emulator.md) hello로 설치 된 [Azure SDK](https://azure.microsoft.com/downloads/)합니다.</span><span class="sxs-lookup"><span data-stu-id="8c857-128">tootest your application in your local Windows computer, you can use hello Microsoft Azure [storage emulator](../storage-use-emulator.md) that is installed with hello [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="8c857-129">hello 저장소 에뮬레이터는 로컬 개발 컴퓨터에 Azure에서 제공 하는 hello Blob, 큐 및 테이블 서비스를 시뮬레이션 하는 유틸리티입니다.</span><span class="sxs-lookup"><span data-stu-id="8c857-129">hello storage emulator is a utility that simulates hello Blob, Queue, and Table services available in Azure on your local development machine.</span></span> <span data-ttu-id="8c857-130">hello 다음 예제는 어떻게는 정적 필드 toohold hello 연결 문자열 tooyour 로컬 저장소 에뮬레이터를 선언할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c857-130">hello following example shows how you can declare a static field toohold hello connection string tooyour local storage emulator:</span></span>

```cpp
// Define hello connection-string with Azure Storage Emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

<span data-ttu-id="8c857-131">toostart hello Azure 저장소 에뮬레이터를 선택 하는 hello **시작** 단추를 클릭 하거나 눌러 hello **Windows** 키입니다.</span><span class="sxs-lookup"><span data-stu-id="8c857-131">toostart hello Azure storage emulator, Select hello **Start** button or press hello **Windows** key.</span></span> <span data-ttu-id="8c857-132">입력을 시작 **Azure 저장소 에뮬레이터**를 선택 하 고 **Microsoft Azure 저장소 에뮬레이터** hello 응용 프로그램 목록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c857-132">Begin typing **Azure Storage Emulator**, and select **Microsoft Azure Storage Emulator** from hello list of applications.</span></span>  

<span data-ttu-id="8c857-133">hello 다음과 같은 샘플 가정 이러한 두 가지 방법 tooget hello 저장소 연결 문자열 중 하나 사용 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c857-133">hello following samples assume that you have used one of these two methods tooget hello storage connection string.</span></span>  

## <a name="retrieve-your-connection-string"></a><span data-ttu-id="8c857-134">연결 문자열 검색</span><span class="sxs-lookup"><span data-stu-id="8c857-134">Retrieve your connection string</span></span>
<span data-ttu-id="8c857-135">Hello를 사용할 수 있습니다 **cloud_storage_account** 클래스 toorepresent 저장소 계정 정보.</span><span class="sxs-lookup"><span data-stu-id="8c857-135">You can use hello **cloud_storage_account** class toorepresent your Storage Account information.</span></span> <span data-ttu-id="8c857-136">tooretrieve 저장소 계정 hello 저장소 연결 문자열 정보, hello를 사용할 수 있습니다 **구문 분석** 메서드.</span><span class="sxs-lookup"><span data-stu-id="8c857-136">tooretrieve your storage account information from hello storage connection string, you can use hello **parse** method.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

<span data-ttu-id="8c857-137">다음으로, 참조 tooa 가져올 **cloud_blob_client** 컨테이너 및 Blob 저장소 서비스 hello 내에 저장 된 blob을 나타내는 개체를 tooretrieve 수 있으므로 클래스.</span><span class="sxs-lookup"><span data-stu-id="8c857-137">Next, get a reference tooa **cloud_blob_client** class as it allows you tooretrieve objects that represent containers and blobs stored within hello Blob Storage Service.</span></span> <span data-ttu-id="8c857-138">hello 다음 코드에서는 **cloud_blob_client** 위에 검색에서는 hello 저장소 계정 개체를 사용 하 여 개체:</span><span class="sxs-lookup"><span data-stu-id="8c857-138">hello following code creates a **cloud_blob_client** object using hello storage account object we retrieved above:</span></span>  

```cpp
// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();  
```

## <a name="how-to-create-a-container"></a><span data-ttu-id="8c857-139">방법: 컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="8c857-139">How to: Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="8c857-140">이 예에서는 어떻게 toocreate 아직 없는 경우 컨테이너:</span><span class="sxs-lookup"><span data-stu-id="8c857-140">This example shows how toocreate a container if it does not already exist:</span></span>  

```cpp
try
{
    // Retrieve storage account from connection string.
    azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

    // Create hello blob client.
    azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

    // Retrieve a reference tooa container.
    azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

    // Create hello container if it doesn't already exist.
    container.create_if_not_exists();
}
catch (const std::exception& e)
{
    std::wcout << U("Error: ") << e.what() << std::endl;
}  
```

<span data-ttu-id="8c857-141">기본적으로 hello 새 컨테이너는 전용 포트 이며이 컨테이너에서 저장소 액세스 키 toodownload blob를 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c857-141">By default, hello new container is private and you must specify your storage access key toodownload blobs from this container.</span></span> <span data-ttu-id="8c857-142">Hello 컨테이너 사용 가능한 tooeveryone 내 toomake hello 파일 (blob)을 사용할 경우 hello 컨테이너 toobe 공용 코드 다음 hello를 사용 하 여 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c857-142">If you want toomake hello files (blobs) within hello container available tooeveryone, you can set hello container toobe public using hello following code:</span></span>  

```cpp
// Make hello blob container publicly accessible.
azure::storage::blob_container_permissions permissions;
permissions.set_public_access(azure::storage::blob_container_public_access_type::blob);
container.upload_permissions(permissions);  
```

<span data-ttu-id="8c857-143">Hello 인터넷에서 누구나 공용 컨테이너의 blob를 볼 수 있지만 수정 하거나 hello 적절 한 액세스 키가 있는 경우에 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c857-143">Anyone on hello Internet can see blobs in a public container, but you can modify or delete them only if you have hello appropriate access key.</span></span>  

## <a name="how-to-upload-a-blob-into-a-container"></a><span data-ttu-id="8c857-144">방법: 컨테이너에 Blob 업로드</span><span class="sxs-lookup"><span data-stu-id="8c857-144">How to: Upload a blob into a container</span></span>
<span data-ttu-id="8c857-145">Azure Blob Storage는 블록 Blob 및 페이지 Blob을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="8c857-145">Azure Blob Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="8c857-146">Hello 대부분의 경우에서 블록 blob는 형식 toouse 권장 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c857-146">In hello majority of cases, block blob is hello recommended type toouse.</span></span>  

<span data-ttu-id="8c857-147">tooupload 파일 tooa 블록 blob 컨테이너 참조를 가져오고 tooget 블록 blob 참조를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c857-147">tooupload a file tooa block blob, get a container reference and use it tooget a block blob reference.</span></span> <span data-ttu-id="8c857-148">Hello를 호출 하 여 모든 스트림 데이터 tooit의 blob 참조를 만든 후 업로드할 수 있습니다 **upload_from_stream** 메서드.</span><span class="sxs-lookup"><span data-stu-id="8c857-148">Once you have a blob reference, you can upload any stream of data tooit by calling hello **upload_from_stream** method.</span></span> <span data-ttu-id="8c857-149">이전에 존재 하거나 파일이 있으면 덮어씁니다 하지 않은 경우이 작업은 hello blob을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8c857-149">This operation will create hello blob if it didn't previously exist, or overwrite it if it does exist.</span></span> <span data-ttu-id="8c857-150">hello 방법을 예제와 다음 tooupload blob 컨테이너에 이미 해당 hello 컨테이너를 만든 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c857-150">hello following example shows how tooupload a blob into a container and assumes that hello container was already created.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Create or overwrite hello "my-blob-1" blob with contents from a local file.
concurrency::streams::istream input_stream = concurrency::streams::file_stream<uint8_t>::open_istream(U("DataFile.txt")).get();
blockBlob.upload_from_stream(input_stream);
input_stream.close().wait();

// Create or overwrite hello "my-blob-2" and "my-blob-3" blobs with contents from text.
// Retrieve a reference tooa blob named "my-blob-2".
azure::storage::cloud_block_blob blob2 = container.get_block_blob_reference(U("my-blob-2"));
blob2.upload_text(U("more text"));

// Retrieve a reference tooa blob named "my-blob-3".
azure::storage::cloud_block_blob blob3 = container.get_block_blob_reference(U("my-directory/my-sub-directory/my-blob-3"));
blob3.upload_text(U("other text"));  
```

<span data-ttu-id="8c857-151">Hello 또는 사용할 수 있습니다 **upload_from_file** 메서드 tooupload 파일 tooa 블록 blob입니다.</span><span class="sxs-lookup"><span data-stu-id="8c857-151">Alternatively, you can use hello **upload_from_file** method tooupload a file tooa block blob.</span></span>

## <a name="how-to-list-hello-blobs-in-a-container"></a><span data-ttu-id="8c857-152">방법: 컨테이너에서 hello blob 나열</span><span class="sxs-lookup"><span data-stu-id="8c857-152">How to: List hello blobs in a container</span></span>
<span data-ttu-id="8c857-153">먼저 toolist hello에서에서 컨테이너의 blob를 컨테이너 참조를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="8c857-153">toolist hello blobs in a container, first get a container reference.</span></span> <span data-ttu-id="8c857-154">Hello 컨테이너를 사용 하 여 있습니다 **list_blobs** tooretrieve hello blob 메서드 및/또는 디렉터리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c857-154">You can then use hello container's **list_blobs** method tooretrieve hello blobs and/or directories within it.</span></span> <span data-ttu-id="8c857-155">tooaccess 다양 한 속성 및 메서드는 반환 된 작업에 대 한 hello **list_blob_item**, hello를 호출 해야 **list_blob_item.as_blob** 메서드 tooget는 **cloud_blob** 개체 또는 hello **list_blob.as_directory** 메서드 tooget cloud_blob_directory 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="8c857-155">tooaccess hello rich set of properties and methods for a returned **list_blob_item**, you must call hello **list_blob_item.as_blob** method tooget a  **cloud_blob** object, or hello **list_blob.as_directory** method tooget a  cloud_blob_directory object.</span></span> <span data-ttu-id="8c857-156">hello 다음 코드에서는 방법을 tooretrieve 및 출력 hello hello의 각 항목의 URI **샘플 컨테이너 내** 컨테이너:</span><span class="sxs-lookup"><span data-stu-id="8c857-156">hello following code demonstrates how tooretrieve and output hello URI of each item in hello **my-sample-container** container:</span></span>

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
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

<span data-ttu-id="8c857-157">작업 나열에 대한 자세한 내용은 [C++에서 Azure 저장소 리소스 나열](../storage-c-plus-plus-enumeration.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8c857-157">For more details on listing operations, see [List Azure Storage Resources in C++](../storage-c-plus-plus-enumeration.md).</span></span>

## <a name="how-to-download-blobs"></a><span data-ttu-id="8c857-158">방법: Blob 다운로드</span><span class="sxs-lookup"><span data-stu-id="8c857-158">How to: Download blobs</span></span>
<span data-ttu-id="8c857-159">toodownload blob을 먼저 blob 참조를 검색 하 고 hello 호출 **download_to_stream** 메서드.</span><span class="sxs-lookup"><span data-stu-id="8c857-159">toodownload blobs, first retrieve a blob reference and then call hello **download_to_stream** method.</span></span> <span data-ttu-id="8c857-160">hello 다음 예제에서는 hello **download_to_stream** 메서드 tootransfer hello blob 내용 tooa stream 개체 다음 tooa 로컬 파일 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c857-160">hello following example uses hello **download_to_stream** method tootransfer hello blob contents tooa stream object that you can then persist tooa local file.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Save blob contents tooa file.
concurrency::streams::container_buffer<std::vector<uint8_t>> buffer;
concurrency::streams::ostream output_stream(buffer);
blockBlob.download_to_stream(output_stream);

std::ofstream outfile("DownloadBlobFile.txt", std::ofstream::binary);
std::vector<unsigned char>& data = buffer.collection();

outfile.write((char *)&data[0], buffer.size());
outfile.close();  
```

<span data-ttu-id="8c857-161">Hello 또는 사용할 수 있습니다 **download_to_file** blob tooa 파일 내용의 toodownload hello 메서드.</span><span class="sxs-lookup"><span data-stu-id="8c857-161">Alternatively, you can use hello **download_to_file** method toodownload hello contents of a blob tooa file.</span></span>
<span data-ttu-id="8c857-162">또한 사용할 수도 있습니다 hello **download_text** 텍스트 문자열로 blob 내용의 toodownload hello 메서드.</span><span class="sxs-lookup"><span data-stu-id="8c857-162">In addition, you can also use hello **download_text** method toodownload hello contents of a blob as a text string.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-2".
azure::storage::cloud_block_blob text_blob = container.get_block_blob_reference(U("my-blob-2"));

// Download hello contents of a blog as a text string.
utility::string_t text = text_blob.download_text();
```

## <a name="how-to-delete-blobs"></a><span data-ttu-id="8c857-163">방법: Blob 삭제</span><span class="sxs-lookup"><span data-stu-id="8c857-163">How to: Delete blobs</span></span>
<span data-ttu-id="8c857-164">toodelete blob blob 참조를 먼저 가져온 고 hello 호출 **delete_blob** 메서드를 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c857-164">toodelete a blob, first get a blob reference and then call hello **delete_blob** method on it.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Delete hello blob.
blockBlob.delete_blob();
```

## <a name="next-steps"></a><span data-ttu-id="8c857-165">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8c857-165">Next steps</span></span>
<span data-ttu-id="8c857-166">Blob 저장소의 기본 사항 hello를 알아보았습니다 했으므로 이러한 링크 toolearn Azure 저장소에 대 한 자세한를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c857-166">Now that you've learned hello basics of blob storage, follow these links toolearn more about Azure Storage.</span></span>  

* [<span data-ttu-id="8c857-167">어떻게 toouse c + +에서 큐 저장소</span><span class="sxs-lookup"><span data-stu-id="8c857-167">How toouse Queue Storage from C++</span></span>](../storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="8c857-168">어떻게 toouse c + +에서 테이블 저장소</span><span class="sxs-lookup"><span data-stu-id="8c857-168">How toouse Table Storage from C++</span></span>](../../cosmos-db/table-storage-how-to-use-c-plus.md)
* [<span data-ttu-id="8c857-169">C++에서 Azure 저장소 리소스 나열</span><span class="sxs-lookup"><span data-stu-id="8c857-169">List Azure Storage Resources in C++</span></span>](../storage-c-plus-plus-enumeration.md)
* [<span data-ttu-id="8c857-170">C++용 Storage Client Library 참조(영문)</span><span class="sxs-lookup"><span data-stu-id="8c857-170">Storage Client Library for C++ Reference</span></span>](http://azure.github.io/azure-storage-cpp)
* [<span data-ttu-id="8c857-171">Azure Storage 설명서</span><span class="sxs-lookup"><span data-stu-id="8c857-171">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
* [<span data-ttu-id="8c857-172">Hello AzCopy 명령줄 유틸리티를 사용 하 여 데이터를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c857-172">Transfer data with hello AzCopy command-line utility</span></span>](../storage-use-azcopy.md)


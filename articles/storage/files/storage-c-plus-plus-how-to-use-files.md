---
title: "Azure 파일 저장소 c + +에 대 한 aaaDevelop | Microsoft Docs"
description: "어떻게 toodevelop c + + 응용 프로그램 및 서비스 Azure 파일 저장소 toostore를 사용 하는 파일 데이터에 알아봅니다."
services: storage
documentationcenter: .net
author: renashahmsft
manager: aungoo
editor: tysonn
ms.assetid: a1e8c99e-47a6-43a9-9541-c9262eb00b38
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2017
ms.author: renashahmsft
ms.openlocfilehash: 48f668cf9359f88baeaaa08ee0d44e70bd0f5f1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-c"></a><span data-ttu-id="70886-103">C++를 사용하여 Azure File Storage 개발</span><span class="sxs-lookup"><span data-stu-id="70886-103">Develop for Azure File storage with C++</span></span>
[!INCLUDE [storage-selector-file-include](../../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-try-azure-tools-files](../../../includes/storage-try-azure-tools-files.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="70886-104">이 자습서 정보</span><span class="sxs-lookup"><span data-stu-id="70886-104">About this tutorial</span></span>

<span data-ttu-id="70886-105">이 자습서에서는 알아봅니다 어떻게 tooperform Azure 파일 저장소에 대 한 기본 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="70886-105">In this tutorial, you'll learn how tooperform basic operations on Azure File storage.</span></span> <span data-ttu-id="70886-106">통해 c + +로 작성 된 샘플을 알아봅니다 toocreate 공유 하는 방법 및 디렉터리, 업로드, 목록 및 파일을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="70886-106">Through samples written in C++, you'll learn how toocreate shares and directories, upload, list, and delete files.</span></span> <span data-ttu-id="70886-107">새 tooAzure 파일 저장소 인 경우에 다음 hello 섹션에 대 한 hello 개념을 진행 하 고 hello 샘플 이해 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70886-107">If you are new tooAzure File storage , going through hello concepts in hello sections that follow will be helpful in understanding hello samples.</span></span>


* <span data-ttu-id="70886-108">Azure 파일 공유 만들기 및 삭제</span><span class="sxs-lookup"><span data-stu-id="70886-108">Create and delete Azure File shares</span></span>
* <span data-ttu-id="70886-109">디렉터리 만들기 및 삭제</span><span class="sxs-lookup"><span data-stu-id="70886-109">Create and delete directories</span></span>
* <span data-ttu-id="70886-110">Azure 파일 공유의 파일 및 디렉터리 열거</span><span class="sxs-lookup"><span data-stu-id="70886-110">Enumerate files and directories in an Azure File share</span></span>
* <span data-ttu-id="70886-111">파일 업로드, 다운로드 및 삭제</span><span class="sxs-lookup"><span data-stu-id="70886-111">Upload, download, and delete a file</span></span>
* <span data-ttu-id="70886-112">Azure 파일 공유에 대 한 hello 할당량 (최대 크기)를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="70886-112">Set hello quota (maximum size) for an Azure File share</span></span>
* <span data-ttu-id="70886-113">Hello 공유에 정의 된 공유 액세스 정책을 사용 하는 파일에 대 한 공유 액세스 서명 (SAS 키)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="70886-113">Create a shared access signature (SAS key) for a file that uses a shared access policy defined on hello share.</span></span>

> [!Note]  
> <span data-ttu-id="70886-114">SMB를 통한 Azure 파일 저장소에 액세스할 수 있습니다, 되므로 hello 표준 c + + I/O 클래스 및 함수를 사용 하 여 hello Azure 파일 공유에 액세스 가능한 toowrite 간단한 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="70886-114">Because Azure File storage may be accessed over SMB, it is possible toowrite simple applications that access hello Azure File share using hello standard C++ I/O classes and functions.</span></span> <span data-ttu-id="70886-115">이 문서를 사용 하는 toowrite 응용 프로그램 hello를 사용 하 여 Azure 저장소 c + + SDK hello 하는 방법을 설명 합니다 [Azure 파일 저장소 REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure 파일 저장소.</span><span class="sxs-lookup"><span data-stu-id="70886-115">This article will describe how toowrite applications that use hello Azure Storage C++ SDK, which uses hello [Azure File storage REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure File storage.</span></span>

## <a name="create-a-c-application"></a><span data-ttu-id="70886-116">C++ 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="70886-116">Create a C++ application</span></span>
<span data-ttu-id="70886-117">toobuild hello 샘플 tooinstall hello Azure 저장소 클라이언트 라이브러리 2.4.0 c + +에 대 한 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="70886-117">toobuild hello samples, you will need tooinstall hello Azure Storage Client Library 2.4.0 for C++.</span></span> <span data-ttu-id="70886-118">Azure 저장소 계정도 만들었어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70886-118">You should also have created an Azure storage account.</span></span>

<span data-ttu-id="70886-119">Azure 저장소 클라이언트 2.4.0 tooinstall hello c + +에 대 한 메서드를 다음 hello 중 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70886-119">tooinstall hello Azure Storage Client 2.4.0 for C++, you can use one of hello following methods:</span></span>

* <span data-ttu-id="70886-120">**Linux:** hello에 제공 된 hello 지침에 따라 [c + + 추가 정보에 대 한 Azure 저장소 클라이언트 라이브러리](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) 페이지.</span><span class="sxs-lookup"><span data-stu-id="70886-120">**Linux:** Follow hello instructions given in hello [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>
* <span data-ttu-id="70886-121">**Windows:** Visual Studio에서 **도구 &gt; NuGet 패키지 관리자 &gt; 패키지 관리자 콘솔**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70886-121">**Windows:** In Visual Studio, click **Tools &gt; NuGet Package Manager &gt; Package Manager Console**.</span></span> <span data-ttu-id="70886-122">Hello에 형식 hello 다음 명령은 [NuGet 패키지 관리자 콘솔](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) 누릅니다 **ENTER**합니다.</span><span class="sxs-lookup"><span data-stu-id="70886-122">Type hello following command into hello [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press **ENTER**.</span></span>
  
```
Install-Package wastorage
```

## <a name="set-up-your-application-toouse-azure-file-storage"></a><span data-ttu-id="70886-123">사용자 응용 프로그램 toouse Azure 파일 저장소 설정</span><span class="sxs-lookup"><span data-stu-id="70886-123">Set up your application toouse Azure File storage</span></span>
<span data-ttu-id="70886-124">Hello 다음 포함 toomanipulate Azure 파일 저장소를 원하는 hello c + + 소스 파일의 문 toohello 맨 위에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="70886-124">Add hello following include statements toohello top of hello C++ source file where you want toomanipulate Azure File storage:</span></span>

```cpp
#include <was/storage_account.h>
#include <was/file.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="70886-125">Azure 저장소 연결 문자열 설정</span><span class="sxs-lookup"><span data-stu-id="70886-125">Set up an Azure storage connection string</span></span>
<span data-ttu-id="70886-126">파일 저장소 toouse tooconnect tooyour Azure 저장소 계정이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="70886-126">toouse File storage, you need tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="70886-127">hello 첫 번째 단계는 것,에서는 연결 문자열을 tooconfigure tooconnect tooyour 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="70886-127">hello first step would be tooconfigure a connection string, which we'll use tooconnect tooyour storage account.</span></span> <span data-ttu-id="70886-128">정적 변수 toodo 정의입니다.</span><span class="sxs-lookup"><span data-stu-id="70886-128">Let's define a static variable toodo that.</span></span>

```cpp
// Define hello connection-string with your values.
const utility::string_t 
storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

## <a name="connecting-tooan-azure-storage-account"></a><span data-ttu-id="70886-129">Tooan Azure 저장소 계정 연결</span><span class="sxs-lookup"><span data-stu-id="70886-129">Connecting tooan Azure storage account</span></span>
<span data-ttu-id="70886-130">Hello를 사용할 수 있습니다 **cloud_storage_account** 클래스 toorepresent 저장소 계정 정보.</span><span class="sxs-lookup"><span data-stu-id="70886-130">You can use hello **cloud_storage_account** class toorepresent your Storage Account information.</span></span> <span data-ttu-id="70886-131">tooretrieve 저장소 계정 hello 저장소 연결 문자열 정보, hello를 사용할 수 있습니다 **구문 분석** 메서드.</span><span class="sxs-lookup"><span data-stu-id="70886-131">tooretrieve your storage account information from hello storage connection string, you can use hello **parse** method.</span></span>

```cpp
// Retrieve storage account from connection string.    
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);
```

## <a name="create-an-azure-file-share"></a><span data-ttu-id="70886-132">Azure 파일 공유 만들기</span><span class="sxs-lookup"><span data-stu-id="70886-132">Create an Azure File share</span></span>
<span data-ttu-id="70886-133">Azure File Storage의 모든 파일 및 디렉터리는 **공유**라는 이름의 컨테이너 안에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70886-133">All files and directories in Azure File storage reside in a container called a **Share**.</span></span> <span data-ttu-id="70886-134">저장소 계정은 계정 용량이 허용하는 만큼의 공유를 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70886-134">Your storage account can have as many shares as your account capacity allows.</span></span> <span data-ttu-id="70886-135">tooobtain 액세스 tooa 공유 및 그 내용을 toouse Azure 파일 저장소 클라이언트 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="70886-135">tooobtain access tooa share and its contents, you need toouse a Azure File storage client.</span></span>

```cpp
// Create hello Azure File storage client.
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();
```

<span data-ttu-id="70886-136">Hello Azure 파일 저장소 클라이언트를 사용 하는 참조 tooa 공유를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70886-136">Using hello Azure File storage client, you can then obtain a reference tooa share.</span></span>

```cpp
// Get a reference toohello file share
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));
```

<span data-ttu-id="70886-137">toocreate hello 공유를 사용 하 여 hello **create_if_not_exists** hello 방식의 **cloud_file_share** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="70886-137">toocreate hello share, use hello **create_if_not_exists** method of hello **cloud_file_share** object.</span></span>

```cpp
if (share.create_if_not_exists()) {    
    std::wcout << U("New share created") << std::endl;    
}
```

<span data-ttu-id="70886-138">이 시점에서 **공유** 참조 tooa 공유 이름의 보유 **샘플 공유 내**합니다.</span><span class="sxs-lookup"><span data-stu-id="70886-138">At this point, **share** holds a reference tooa share named **my-sample-share**.</span></span>

## <a name="delete-an-azure-file-share"></a><span data-ttu-id="70886-139">Azure 파일 공유 삭제</span><span class="sxs-lookup"><span data-stu-id="70886-139">Delete an Azure File share</span></span>
<span data-ttu-id="70886-140">호출 hello 이루어진다는 공유 삭제 **delete_if_exists** cloud_file_share 개체에서 메서드.</span><span class="sxs-lookup"><span data-stu-id="70886-140">Deleting a share is done by calling hello **delete_if_exists** method on a cloud_file_share object.</span></span> <span data-ttu-id="70886-141">다음이 샘플 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="70886-141">Here's sample code that does that.</span></span>

```cpp
// Get a reference toohello share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

// delete hello share if exists
share.delete_share_if_exists();
```

## <a name="create-a-directory"></a><span data-ttu-id="70886-142">디렉터리 만들기</span><span class="sxs-lookup"><span data-stu-id="70886-142">Create a directory</span></span>
<span data-ttu-id="70886-143">대신 모든 hello 루트 디렉터리에 하위 디렉터리 내의 파일을 배치 하 여 저장소를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70886-143">You can organize storage by putting files inside subdirectories instead of having all of them in hello root directory.</span></span> <span data-ttu-id="70886-144">Azure 파일 저장소에서는 허용 하는 사용자 계정에는으로 여러 디렉터리 만큼 toocreate를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="70886-144">Azure File storage allows you toocreate as many directories as your account will allow.</span></span> <span data-ttu-id="70886-145">아래 hello 코드 라는 디렉터리를 만듭니다. **샘플 디렉터리 내** hello 루트 디렉터리 뿐 아니라 라는 하위 디렉터리에서 **내 하위 샘플**합니다.</span><span class="sxs-lookup"><span data-stu-id="70886-145">hello code below will create a directory named **my-sample-directory** under hello root directory as well as a subdirectory named **my-sample-subdirectory**.</span></span>

```cpp
// Retrieve a reference tooa directory
azure::storage::cloud_file_directory directory = share.get_directory_reference(_XPLATSTR("my-sample-directory"));

// Return value is true if hello share did not exist and was successfully created.
directory.create_if_not_exists();

// Create a subdirectory.
azure::storage::cloud_file_directory subdirectory = 
  directory.get_subdirectory_reference(_XPLATSTR("my-sample-subdirectory"));
subdirectory.create_if_not_exists();
```

## <a name="delete-a-directory"></a><span data-ttu-id="70886-146">디렉터리 삭제</span><span class="sxs-lookup"><span data-stu-id="70886-146">Delete a directory</span></span>
<span data-ttu-id="70886-147">디렉터리의 삭제는 간단한 작업입니다. 단, 여전히 파일 또는 기타 디렉터리가 포함된 디렉터리는 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="70886-147">Deleting a directory is a simple task, although it should be noted that you cannot delete a directory that still contains files or other directories.</span></span>

```cpp
// Get a reference toohello share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

// Get a reference toohello directory.
azure::storage::cloud_file_directory directory = 
  share.get_directory_reference(_XPLATSTR("my-sample-directory"));

// Get a reference toohello subdirectory you want toodelete.
azure::storage::cloud_file_directory sub_directory =
  directory.get_subdirectory_reference(_XPLATSTR("my-sample-subdirectory"));

// Delete hello subdirectory and hello sample directory.
sub_directory.delete_directory_if_exists();

directory.delete_directory_if_exists();
```

## <a name="enumerate-files-and-directories-in-an-azure-file-share"></a><span data-ttu-id="70886-148">Azure 파일 공유의 파일 및 디렉터리 열거</span><span class="sxs-lookup"><span data-stu-id="70886-148">Enumerate files and directories in an Azure File share</span></span>
<span data-ttu-id="70886-149">공유 내에서 파일 및 디렉터리 목록을 가져오는 것은 **cloud_file_directory** 참조에서 **list_files_and_directories**를 호출하여 쉽게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70886-149">Obtaining a list of files and directories within a share is easily done by calling **list_files_and_directories** on a **cloud_file_directory** reference.</span></span> <span data-ttu-id="70886-150">tooaccess 다양 한 속성 및 메서드는 반환 된 작업에 대 한 hello **list_file_and_directory_item**, hello를 호출 해야 **list_file_and_directory_item.as_file** 메서드 tooget는 **cloud_ 파일** 개체나 hello **list_file_and_directory_item.as_directory** 메서드 tooget는 **cloud_file_directory** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="70886-150">tooaccess hello rich set of properties and methods for a returned **list_file_and_directory_item**, you must call hello **list_file_and_directory_item.as_file** method tooget a **cloud_file** object, or hello **list_file_and_directory_item.as_directory** method tooget a **cloud_file_directory** object.</span></span>

<span data-ttu-id="70886-151">코드 다음 hello tooretrieve 및 출력 hello 공유의 hello 루트 디렉터리의 각 항목의 URI hello 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="70886-151">hello following code demonstrates how tooretrieve and output hello URI of each item in hello root directory of hello share.</span></span>

```cpp
//Get a reference toohello root directory for hello share.
azure::storage::cloud_file_directory root_dir = 
  share.get_root_directory_reference();

// Output URI of each item.
azure::storage::list_file_and_diretory_result_iterator end_of_results;

for (auto it = directory.list_files_and_directories(); it != end_of_results; ++it)
{
    if(it->is_directory())
    {
        ucout << "Directory: " << it->as_directory().uri().primary_uri().to_string() << std::endl;
    }
    else if (it->is_file())
    {
        ucout << "File: " << it->as_file().uri().primary_uri().to_string() << std::endl;
    }        
}
```

## <a name="upload-a-file"></a><span data-ttu-id="70886-152">파일 업로드</span><span class="sxs-lookup"><span data-stu-id="70886-152">Upload a file</span></span>
<span data-ttu-id="70886-153">최소한, 매우 hello에서 Azure 파일 공유가 파일이 수 있는 루트 디렉터리를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="70886-153">At hello very least, an Azure File share contains a root directory where files can reside.</span></span> <span data-ttu-id="70886-154">이 섹션에서는 tooupload hello에 대 한 로컬 저장소에서 파일 루트 디렉터리를 공유 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="70886-154">In this section, you'll learn how tooupload a file from local storage onto hello root directory of a share.</span></span>

<span data-ttu-id="70886-155">파일 업로드 hello 첫 번째 단계에는 tooobtain 상주해 야 참조 toohello 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="70886-155">hello first step in uploading a file is tooobtain a reference toohello directory where it should reside.</span></span> <span data-ttu-id="70886-156">이렇게 하려면 호출 hello **get_root_directory_reference** hello 공유 개체의 메서드.</span><span class="sxs-lookup"><span data-stu-id="70886-156">You do this by calling hello **get_root_directory_reference** method of hello share object.</span></span>

```cpp
//Get a reference toohello root directory for hello share.
azure::storage::cloud_file_directory root_dir = share.get_root_directory_reference();
```

<span data-ttu-id="70886-157">Hello 공유의 참조 toohello 루트 디렉터리를가지고 놓아서 파일을 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70886-157">Now that you have a reference toohello root directory of hello share, you can upload a file onto it.</span></span> <span data-ttu-id="70886-158">이 예제에서는 파일, 텍스트 및 스트림에서 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="70886-158">This example uploads from a file, from text, and from a stream.</span></span>

```cpp
// Upload a file from a stream.
concurrency::streams::istream input_stream = 
  concurrency::streams::file_stream<uint8_t>::open_istream(_XPLATSTR("DataFile.txt")).get();

azure::storage::cloud_file file1 = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-1"));
file1.upload_from_stream(input_stream);

// Upload some files from text.
azure::storage::cloud_file file2 = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-2"));
file2.upload_text(_XPLATSTR("more text"));

// Upload a file from a file.
azure::storage::cloud_file file4 = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-3"));
file4.upload_from_file(_XPLATSTR("DataFile.txt"));    
```

## <a name="download-a-file"></a><span data-ttu-id="70886-159">파일 다운로드</span><span class="sxs-lookup"><span data-stu-id="70886-159">Download a file</span></span>
<span data-ttu-id="70886-160">toodownload 파일 파일 참조를 먼저 검색 하 고 hello 호출 **download_to_stream** 메서드 tootransfer hello 파일 내용 tooa 스트림 개체를 지속할 수 있습니다 tooa 로컬 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="70886-160">toodownload files, first retrieve a file reference and then call hello **download_to_stream** method tootransfer hello file contents tooa stream object, which you can then persist tooa local file.</span></span> <span data-ttu-id="70886-161">Hello 또는 사용할 수 있습니다 **download_to_file** 파일 tooa 로컬 파일 내용의 toodownload hello 메서드.</span><span class="sxs-lookup"><span data-stu-id="70886-161">Alternatively, you can use hello **download_to_file** method toodownload hello contents of a file tooa local file.</span></span> <span data-ttu-id="70886-162">Hello를 사용할 수 있습니다 **download_text** 텍스트 문자열로 파일 내용의 toodownload hello 메서드.</span><span class="sxs-lookup"><span data-stu-id="70886-162">You can use hello **download_text** method toodownload hello contents of a file as a text string.</span></span>

<span data-ttu-id="70886-163">hello 다음 예제에서는 hello **download_to_stream** 및 **download_text** 메서드 toodemonstrate 이전 섹션에서 만든 hello 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="70886-163">hello following example uses hello **download_to_stream** and **download_text** methods toodemonstrate downloading hello files, which were created in previous sections.</span></span>

```cpp
// Download as text
azure::storage::cloud_file text_file = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-2"));
utility::string_t text = text_file.download_text();
ucout << "File Text: " << text << std::endl;

// Download as a stream.
azure::storage::cloud_file stream_file = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-3"));

concurrency::streams::container_buffer<std::vector<uint8_t>> buffer;
concurrency::streams::ostream output_stream(buffer);
stream_file.download_to_stream(output_stream);
std::ofstream outfile("DownloadFile.txt", std::ofstream::binary);
std::vector<unsigned char>& data = buffer.collection();
outfile.write((char *)&data[0], buffer.size());
outfile.close();
```

## <a name="delete-a-file"></a><span data-ttu-id="70886-164">파일 삭제</span><span class="sxs-lookup"><span data-stu-id="70886-164">Delete a file</span></span>
<span data-ttu-id="70886-165">다른 일반적인 Azure File Storage 작업은 파일의 삭제입니다.</span><span class="sxs-lookup"><span data-stu-id="70886-165">Another common Azure File storage operation is file deletion.</span></span> <span data-ttu-id="70886-166">hello 다음 코드를 삭제 내-샘플-파일-3 hello 루트 디렉터리 아래에 저장 된 이라는 파일로 내보내집니다.</span><span class="sxs-lookup"><span data-stu-id="70886-166">hello following code deletes a file named my-sample-file-3 stored under hello root directory.</span></span>

```cpp
// Get a reference toohello root directory for hello share.    
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

azure::storage::cloud_file_directory root_dir = 
  share.get_root_directory_reference();

azure::storage::cloud_file file = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-3"));

file.delete_file_if_exists();
```

## <a name="set-hello-quota-maximum-size-for-an-azure-file-share"></a><span data-ttu-id="70886-167">Azure 파일 공유에 대 한 hello 할당량 (최대 크기)를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="70886-167">Set hello quota (maximum size) for an Azure File share</span></span>
<span data-ttu-id="70886-168">(기가바이트)에서 파일 공유에 대 한 hello 할당량 (또는 최대 크기)을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70886-168">You can set hello quota (or maximum size) for a file share, in gigabytes.</span></span> <span data-ttu-id="70886-169">데이터의 양을 현재 hello 공유에 저장 된 toosee를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70886-169">You can also check toosee how much data is currently stored on hello share.</span></span>

<span data-ttu-id="70886-170">공유에 대 한 hello 할당량을 설정 하 여 hello hello 공유에 저장 된 hello 파일의 전체 크기를 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70886-170">By setting hello quota for a share, you can limit hello total size of hello files stored on hello share.</span></span> <span data-ttu-id="70886-171">Hello hello 공유에 있는 파일의 전체 크기를 초과 하는 경우 hello 공유에 hello 할당량을 설정한 후 클라이언트는 수 없습니다 tooincrease hello 크기의 기존 파일 또는 이러한 파일은 비어 경우가 아니면 새 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="70886-171">If hello total size of files on hello share exceeds hello quota set on hello share, then clients will be unable tooincrease hello size of existing files or create new files, unless those files are empty.</span></span>

<span data-ttu-id="70886-172">다음 예제에서는 hello 방법을 toocheck hello 공유에 대 한 현재 사용량 및 tooset hello 공유에 대 한 할당량을 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="70886-172">hello example below shows how toocheck hello current usage for a share and how tooset hello quota for hello share.</span></span>

```cpp
// Parse hello connection string for hello storage account.
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello file client.
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();

// Get a reference toohello share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));
if (share.exists())
{
    std::cout << "Current share usage: " << share.download_share_usage() << "/" << share.properties().quota();

    //This line sets hello quota too2560GB
    share.resize(2560);

    std::cout << "Quota increased: " << share.download_share_usage() << "/" << share.properties().quota();

}
```

## <a name="generate-a-shared-access-signature-for-a-file-or-file-share"></a><span data-ttu-id="70886-173">파일 또는 파일 공유에 대한 공유 액세스 서명 생성</span><span class="sxs-lookup"><span data-stu-id="70886-173">Generate a shared access signature for a file or file share</span></span>
<span data-ttu-id="70886-174">파일 공유 또는 개별 파일에 대한 SAS(공유 액세스 서명)를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70886-174">You can generate a shared access signature (SAS) for a file share or for an individual file.</span></span> <span data-ttu-id="70886-175">서명 파일 공유 toomanage 공유 액세스에 공유 액세스 정책을도 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70886-175">You can also create a shared access policy on a file share toomanage shared access signatures.</span></span> <span data-ttu-id="70886-176">공유 액세스 정책 만들기 좋습니다 해야 손상 되 면 hello SAS를 해지 하는 수단을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="70886-176">Creating a shared access policy is recommended, as it provides a means of revoking hello SAS if it should be compromised.</span></span>

<span data-ttu-id="70886-177">다음 예제는 hello 공유에 공유 액세스 정책을 만들고 정책 tooprovide hello 제약 조건을 SAS에 대 한 hello에서 파일 공유를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="70886-177">hello following example creates a shared access policy on a share, and then uses that policy tooprovide hello constraints for a SAS on a file in hello share.</span></span>

```cpp
// Parse hello connection string for hello storage account.
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello file client and get a reference toohello share
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();

azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

if (share.exists())
{
    // Create and assign a policy
    utility::string_t policy_name = _XPLATSTR("sampleSharePolicy");

    azure::storage::file_shared_access_policy sharedPolicy = 
      azure::storage::file_shared_access_policy();

    //set permissions tooexpire in 90 minutes
    sharedPolicy.set_expiry(utility::datetime::utc_now() + 
       utility::datetime::from_minutes(90));

    //give read and write permissions
    sharedPolicy.set_permissions(azure::storage::file_shared_access_policy::permissions::write | azure::storage::file_shared_access_policy::permissions::read);

    //set permissions for hello share
    azure::storage::file_share_permissions permissions;    

    //retrieve hello current list of shared access policies
    azure::storage::shared_access_policies<azure::storage::file_shared_access_policy> policies;

    //add hello new shared policy
    policies.insert(std::make_pair(policy_name, sharedPolicy));

    //save hello updated policy list
    permissions.set_policies(policies);
    share.upload_permissions(permissions);

    //Retrieve hello root directory and file references
    azure::storage::cloud_file_directory root_dir = 
        share.get_root_directory_reference();
    azure::storage::cloud_file file = 
      root_dir.get_file_reference(_XPLATSTR("my-sample-file-1"));

    // Generate a SAS for a file in hello share 
    //  and associate this access policy with it.        
    utility::string_t sas_token = file.get_shared_access_signature(sharedPolicy);

    // Create a new CloudFile object from hello SAS, and write some text toohello file.        
    azure::storage::cloud_file file_with_sas(azure::storage::storage_credentials(sas_token).transform_uri(file.uri().primary_uri()));
    utility::string_t text = _XPLATSTR("My sample content");        
    file_with_sas.upload_text(text);        

    //Download and print URL with SAS.
    utility::string_t downloaded_text = file_with_sas.download_text();        
    ucout << downloaded_text << std::endl;        
    ucout << azure::storage::storage_credentials(sas_token).transform_uri(file.uri().primary_uri()).to_string() << std::endl;

}
```
## <a name="next-steps"></a><span data-ttu-id="70886-178">다음 단계</span><span class="sxs-lookup"><span data-stu-id="70886-178">Next steps</span></span>
<span data-ttu-id="70886-179">Azure 저장소에 대해 자세히 toolearn이 리소스를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="70886-179">toolearn more about Azure Storage, explore these resources:</span></span>

* [<span data-ttu-id="70886-180">Storage Client Library for C++</span><span class="sxs-lookup"><span data-stu-id="70886-180">Storage Client Library for C++</span></span>](https://github.com/Azure/azure-storage-cpp)
* <span data-ttu-id="70886-181">[C++로 작성된 Azure Storage File 서비스 샘플] (https://github.com/Azure-Samples/storage-file-cpp-getting-started)</span><span class="sxs-lookup"><span data-stu-id="70886-181">[Azure Storage File Service Samples in C++] (https://github.com/Azure-Samples/storage-file-cpp-getting-started)</span></span>
* [<span data-ttu-id="70886-182">Azure 저장소 탐색기</span><span class="sxs-lookup"><span data-stu-id="70886-182">Azure Storage Explorer</span></span>](http://go.microsoft.com/fwlink/?LinkID=822673&clcid=0x409)
* [<span data-ttu-id="70886-183">Azure 저장소 설명서</span><span class="sxs-lookup"><span data-stu-id="70886-183">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
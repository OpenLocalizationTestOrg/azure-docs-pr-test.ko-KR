---
title: "Python을 사용하여 Azure File Storage용으로 개발 | Microsoft Docs"
description: "Azure File Storage를 사용하여 파일 데이터를 저장하는 Python 응용 프로그램 및 서비스를 개발하는 방법에 대해 알아봅니다."
services: storage
documentationcenter: python
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 297f3a14-6b3a-48b0-9da4-db5907827fb5
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 3dd14e8d3ea7d1e50f41633a7920a6d36becf789
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="develop-for-azure-file-storage-with-python"></a><span data-ttu-id="5a6dc-103">Python을 사용하여 Azure File Storage용으로 개발</span><span class="sxs-lookup"><span data-stu-id="5a6dc-103">Develop for Azure File storage with Python</span></span>
[!INCLUDE [storage-selector-file-include](../../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-try-azure-tools-files](../../../includes/storage-try-azure-tools-files.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="5a6dc-104">이 자습서 정보</span><span class="sxs-lookup"><span data-stu-id="5a6dc-104">About this tutorial</span></span>
<span data-ttu-id="5a6dc-105">이 자습서에서는 Azure File Storage를 사용하여 파일 데이터를 저장하는 응용 프로그램이나 서비스를 Python을 사용하여 개발하는 데 필요한 기본 사항을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5a6dc-105">This tutorial will demonstrate the basics of using Python to develop applications or services that use Azure File storage to store file data.</span></span> <span data-ttu-id="5a6dc-106">즉 간단한 콘솔 응용 프로그램을 만들고, Python 및 Azure File Storage를 통해 기본 작업을 수행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5a6dc-106">In this tutorial, we will create a simple console application and show how to perform basic actions with Python and Azure File storage:</span></span>

* <span data-ttu-id="5a6dc-107">Azure 파일 공유 만들기</span><span class="sxs-lookup"><span data-stu-id="5a6dc-107">Create Azure File shares</span></span>
* <span data-ttu-id="5a6dc-108">디렉터리 만들기</span><span class="sxs-lookup"><span data-stu-id="5a6dc-108">Create directories</span></span>
* <span data-ttu-id="5a6dc-109">Azure 파일 공유에 파일 및 디렉터리 열거</span><span class="sxs-lookup"><span data-stu-id="5a6dc-109">Enumerate files and directories in an Azure File share</span></span>
* <span data-ttu-id="5a6dc-110">파일 업로드, 다운로드 및 삭제</span><span class="sxs-lookup"><span data-stu-id="5a6dc-110">Upload, download, and delete a file</span></span>

> [!Note]  
> <span data-ttu-id="5a6dc-111">Azure File Storage는 SMB를 통해 액세스할 수 있기 때문에 표준 Python I/O 클래스 및 함수를 사용하여 Azure 파일 공유에 액세스하는 간단한 응용 프로그램을 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a6dc-111">Because Azure File storage may be accessed over SMB, it is possible to write simple applications that access the Azure File share using the standard Python I/O classes and functions.</span></span> <span data-ttu-id="5a6dc-112">이 문서에서는 [Azure File Storage REST API](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/file-service-rest-api)를 사용하여 Azure File Storage와 통신하는 Azure Storage Python SDK를 사용하는 응용 프로그램을 작성하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6dc-112">This article will describe how to write applications that use the Azure Storage Python SDK, which uses the [Azure File storage REST API](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/file-service-rest-api) to talk to Azure File storage.</span></span>

### <a name="set-up-your-application-to-use-azure-file-storage"></a><span data-ttu-id="5a6dc-113">Azure File Storage를 사용하도록 응용 프로그램 설정</span><span class="sxs-lookup"><span data-stu-id="5a6dc-113">Set up your application to use Azure File storage</span></span>
<span data-ttu-id="5a6dc-114">프로그래밍 방식으로 Azure Storage에 액세스하려는 Python 원본 파일의 맨 위쪽에 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6dc-114">Add the following near the top of any Python source file in which you wish to programmatically access Azure Storage.</span></span>

```python
from azure.storage.file import FileService
```

### <a name="set-up-a-connection-to-azure-file-storage"></a><span data-ttu-id="5a6dc-115">Azure File Storage에 대한 연결 설정</span><span class="sxs-lookup"><span data-stu-id="5a6dc-115">Set up a connection to Azure File storage</span></span> 
<span data-ttu-id="5a6dc-116">`FileService` 개체를 사용하면 공유, 디렉터리 및 파일 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a6dc-116">The `FileService` object lets you work with shares, directories and files.</span></span> <span data-ttu-id="5a6dc-117">다음 코드는 저장소 계정 이름 및 계정 키를 사용하는 `FileService` 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5a6dc-117">The following code creates a `FileService` object using the storage account name and account key.</span></span> <span data-ttu-id="5a6dc-118">`<myaccount>` 및 `<mykey>`를 사용자의 계정 이름 및 키로 바꾸세요.</span><span class="sxs-lookup"><span data-stu-id="5a6dc-118">Replace `<myaccount>` and `<mykey>` with your account name and key.</span></span>

```python
file_service = FileService(account_name='myaccount', account_key='mykey')
```

### <a name="create-an-azure-file-share"></a><span data-ttu-id="5a6dc-119">Azure 파일 공유 만들기</span><span class="sxs-lookup"><span data-stu-id="5a6dc-119">Create an Azure File share</span></span>
<span data-ttu-id="5a6dc-120">다음 코드 예제에서는 `FileService` 개체를 사용하여 공유가 없는 경우 새로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a6dc-120">In the following code example, you can use a `FileService` object to create the share if it doesn't exist.</span></span>

```python
file_service.create_share('myshare')
```

### <a name="create-a-directory"></a><span data-ttu-id="5a6dc-121">디렉터리 만들기</span><span class="sxs-lookup"><span data-stu-id="5a6dc-121">Create a directory</span></span>
<span data-ttu-id="5a6dc-122">또한 루트 디렉터리에 이들 모두를 포함하는 대신 하위 디렉터리 내에서 파일을 배치하여 저장소를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a6dc-122">You can also organize storage by putting files inside sub-directories instead of having all of them in the root directory.</span></span> <span data-ttu-id="5a6dc-123">Azure File Storage를 사용하면 계정이 허용하는 만큼 많은 디렉터리를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a6dc-123">Azure File storage allows you to create as many directories as your account will allow.</span></span> <span data-ttu-id="5a6dc-124">아래 코드는 루트 디렉터리 아래에 **sampledir** 라는 이름의 하위 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5a6dc-124">The code below will create a sub-directory named **sampledir** under the root directory.</span></span>

```python
file_service.create_directory('myshare', 'sampledir')
```

### <a name="enumerate-files-and-directories-in-an-azure-file-share"></a><span data-ttu-id="5a6dc-125">Azure 파일 공유에 파일 및 디렉터리 열거</span><span class="sxs-lookup"><span data-stu-id="5a6dc-125">Enumerate files and directories in an Azure File share</span></span>
<span data-ttu-id="5a6dc-126">공유의 파일 및 디렉터리를 나열하려면 **list\_directories\_and\_files** 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6dc-126">To list the files and directories in a share, use the **list\_directories\_and\_files** method.</span></span> <span data-ttu-id="5a6dc-127">이 메서드는 생성기를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6dc-127">This method returns a generator.</span></span> <span data-ttu-id="5a6dc-128">다음 코드는 공유에 있는 각 파일 및 디렉터리의 **이름** 을 콘솔에 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6dc-128">The following code outputs the **name** of each file and directory in a share to the console.</span></span>

```python
generator = file_service.list_directories_and_files('myshare')
for file_or_dir in generator:
    print(file_or_dir.name)
```

### <a name="upload-a-file"></a><span data-ttu-id="5a6dc-129">파일 업로드</span><span class="sxs-lookup"><span data-stu-id="5a6dc-129">Upload a file</span></span> 
<span data-ttu-id="5a6dc-130">Azure 파일 공유에는 파일이 상주할 수 있는 최소한의 루트 디렉터리가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a6dc-130">Azure File share contains at the very least, a root directory where files can reside.</span></span> <span data-ttu-id="5a6dc-131">이 섹션에서는 로컬 저장소에서 공유의 루트 디렉터리로 파일을 업로드하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="5a6dc-131">In this section, you'll learn how to upload a file from local storage onto the root directory of a share.</span></span>

<span data-ttu-id="5a6dc-132">파일을 만들고 데이터를 업로드하려면 `create_file_from_path`, `create_file_from_stream`, `create_file_from_bytes` 또는 `create_file_from_text` 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6dc-132">To create a file and upload data, use the `create_file_from_path`, `create_file_from_stream`, `create_file_from_bytes` or `create_file_from_text` methods.</span></span> <span data-ttu-id="5a6dc-133">이러한 메서드는 데이터의 크기가 64MB를 초과할 경우 필요한 청크를 수행하는 고급 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="5a6dc-133">They are high-level methods that perform the necessary chunking when the size of the data exceeds 64 MB.</span></span>

<span data-ttu-id="5a6dc-134">`create_file_from_path`는 지정된 경로에서 파일의 콘텐츠를 업로드하고, `create_file_from_stream`은 이미 열려 있는 파일/스트림에서 콘텐츠를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6dc-134">`create_file_from_path` uploads the contents of a file from the specified path, and `create_file_from_stream` uploads the contents from an already opened file/stream.</span></span> <span data-ttu-id="5a6dc-135">`create_file_from_bytes`는 바이트 배열을 업로드하고, `create_file_from_text`는 지정된 인코딩(기본값: UTF-8)을 사용하여 지정된 텍스트 값을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6dc-135">`create_file_from_bytes` uploads an array of bytes, and `create_file_from_text` uploads the specified text value using the specified encoding (defaults to UTF-8).</span></span>

<span data-ttu-id="5a6dc-136">다음 예제에서는 **sunset.png** 파일의 내용을 **myfile** 파일에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6dc-136">The following example uploads the contents of the **sunset.png** file into the **myfile** file.</span></span>

```python
from azure.storage.file import ContentSettings
file_service.create_file_from_path(
    'myshare',
    None, # We want to create this blob in the root directory, so we specify None for the directory_name
    'myfile',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png'))
```

### <a name="download-a-file"></a><span data-ttu-id="5a6dc-137">파일 다운로드</span><span class="sxs-lookup"><span data-stu-id="5a6dc-137">Download a file</span></span>
<span data-ttu-id="5a6dc-138">파일에서 데이터를 다운로드하려면 `get_file_to_path`, `get_file_to_stream`, `get_file_to_bytes` 또는 `get_file_to_text`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6dc-138">To download data from a file, use `get_file_to_path`, `get_file_to_stream`, `get_file_to_bytes`, or `get_file_to_text`.</span></span> <span data-ttu-id="5a6dc-139">이러한 메서드는 데이터의 크기가 64MB를 초과할 경우 필요한 청크를 수행하는 고급 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="5a6dc-139">They are high-level methods that perform the necessary chunking when the size of the data exceeds 64 MB.</span></span>

<span data-ttu-id="5a6dc-140">다음 예제에서는 `get_file_to_path`를 사용하여 **myfile** 파일의 콘텐츠를 다운로드한 다음 **out-sunset.png** 파일에 저장하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5a6dc-140">The following example demonstrates using `get_file_to_path` to download the contents of the **myfile** file and store it to the **out-sunset.png** file.</span></span>

```python
file_service.get_file_to_path('myshare', None, 'myfile', 'out-sunset.png')
```

### <a name="delete-a-file"></a><span data-ttu-id="5a6dc-141">파일 삭제</span><span class="sxs-lookup"><span data-stu-id="5a6dc-141">Delete a file</span></span>
<span data-ttu-id="5a6dc-142">마지막으로 파일을 삭제하려면 `delete_file`을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="5a6dc-142">Finally, to delete a file, call `delete_file`.</span></span>

```python
file_service.delete_file('myshare', None, 'myfile')
```

## <a name="next-steps"></a><span data-ttu-id="5a6dc-143">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5a6dc-143">Next steps</span></span>
<span data-ttu-id="5a6dc-144">이제 Python으로 Azure File Storage를 조작하는 방법을 배웠으므로 다음 링크를 통해 자세한 내용을 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="5a6dc-144">Now that you've learned how to manipulate Azure File storage with Python, follow these links to learn more.</span></span>

* [<span data-ttu-id="5a6dc-145">Python 개발자 센터</span><span class="sxs-lookup"><span data-stu-id="5a6dc-145">Python Developer Center</span></span>](/develop/python/)
* [<span data-ttu-id="5a6dc-146">Azure 저장소 서비스 REST API</span><span class="sxs-lookup"><span data-stu-id="5a6dc-146">Azure Storage Services REST API</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* [<span data-ttu-id="5a6dc-147">Microsoft Azure Storage SDK for Python</span><span class="sxs-lookup"><span data-stu-id="5a6dc-147">Microsoft Azure Storage SDK for Python</span></span>](https://github.com/Azure/azure-storage-python)
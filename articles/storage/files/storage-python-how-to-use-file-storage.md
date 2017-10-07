---
title: "Azure 파일 저장소 Python에 대 한 aaaDevelop | Microsoft Docs"
description: "어떻게 toodevelop Python 응용 프로그램 및 서비스 Azure 파일 저장소 toostore를 사용 하는 파일 데이터에 알아봅니다."
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
ms.openlocfilehash: 2adc5aac2765b98a8022ab1f706c1fcdbca1b43c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-python"></a><span data-ttu-id="236b1-103">Python을 사용하여 Azure File Storage용으로 개발</span><span class="sxs-lookup"><span data-stu-id="236b1-103">Develop for Azure File storage with Python</span></span>
[!INCLUDE [storage-selector-file-include](../../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-try-azure-tools-files](../../../includes/storage-try-azure-tools-files.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="236b1-104">이 자습서 정보</span><span class="sxs-lookup"><span data-stu-id="236b1-104">About this tutorial</span></span>
<span data-ttu-id="236b1-105">이 자습서에서는 Python toodevelop 응용 프로그램이 나 Azure 파일 저장소 toostore 파일 데이터를 사용 하는 서비스를 사용 하 여의 hello 기본 사항을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="236b1-105">This tutorial will demonstrate hello basics of using Python toodevelop applications or services that use Azure File storage toostore file data.</span></span> <span data-ttu-id="236b1-106">이 자습서에서는 간단한 콘솔 응용 프로그램 만들어져 표시 방법을 Python 및 Azure 파일 저장소를 사용 하 여 기본 동작 tooperform:</span><span class="sxs-lookup"><span data-stu-id="236b1-106">In this tutorial, we will create a simple console application and show how tooperform basic actions with Python and Azure File storage:</span></span>

* <span data-ttu-id="236b1-107">Azure 파일 공유 만들기</span><span class="sxs-lookup"><span data-stu-id="236b1-107">Create Azure File shares</span></span>
* <span data-ttu-id="236b1-108">디렉터리 만들기</span><span class="sxs-lookup"><span data-stu-id="236b1-108">Create directories</span></span>
* <span data-ttu-id="236b1-109">Azure 파일 공유에 파일 및 디렉터리 열거</span><span class="sxs-lookup"><span data-stu-id="236b1-109">Enumerate files and directories in an Azure File share</span></span>
* <span data-ttu-id="236b1-110">파일 업로드, 다운로드 및 삭제</span><span class="sxs-lookup"><span data-stu-id="236b1-110">Upload, download, and delete a file</span></span>

> [!Note]  
> <span data-ttu-id="236b1-111">SMB를 통한 Azure 파일 저장소에 액세스할 수 있습니다, 되므로 hello 표준 Python I/O 클래스 및 함수를 사용 하 여 hello Azure 파일 공유에 액세스 가능한 toowrite 간단한 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="236b1-111">Because Azure File storage may be accessed over SMB, it is possible toowrite simple applications that access hello Azure File share using hello standard Python I/O classes and functions.</span></span> <span data-ttu-id="236b1-112">이 문서를 사용 하는 toowrite 응용 프로그램 hello를 사용 하 여 Azure 저장소 Python SDK hello 하는 방법을 설명 합니다 [Azure 파일 저장소 REST API](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure 파일 저장소.</span><span class="sxs-lookup"><span data-stu-id="236b1-112">This article will describe how toowrite applications that use hello Azure Storage Python SDK, which uses hello [Azure File storage REST API](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure File storage.</span></span>

### <a name="set-up-your-application-toouse-azure-file-storage"></a><span data-ttu-id="236b1-113">사용자 응용 프로그램 toouse Azure 파일 저장소 설정</span><span class="sxs-lookup"><span data-stu-id="236b1-113">Set up your application toouse Azure File storage</span></span>
<span data-ttu-id="236b1-114">Azure 저장소 tooprogrammatically 액세스 원하는 모든 Python 원본 파일의 hello 위쪽 hello 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="236b1-114">Add hello following near hello top of any Python source file in which you wish tooprogrammatically access Azure Storage.</span></span>

```python
from azure.storage.file import FileService
```

### <a name="set-up-a-connection-tooazure-file-storage"></a><span data-ttu-id="236b1-115">연결 tooAzure 파일 저장소 설정</span><span class="sxs-lookup"><span data-stu-id="236b1-115">Set up a connection tooAzure File storage</span></span> 
<span data-ttu-id="236b1-116">hello `FileService` 개체를 사용 하면 공유, 디렉터리 및 파일을 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="236b1-116">hello `FileService` object lets you work with shares, directories and files.</span></span> <span data-ttu-id="236b1-117">hello 다음 코드에서는 `FileService` hello 저장소 계정 이름 및 계정 키를 사용 하 여 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="236b1-117">hello following code creates a `FileService` object using hello storage account name and account key.</span></span> <span data-ttu-id="236b1-118">`<myaccount>` 및 `<mykey>`를 사용자의 계정 이름 및 키로 바꾸세요.</span><span class="sxs-lookup"><span data-stu-id="236b1-118">Replace `<myaccount>` and `<mykey>` with your account name and key.</span></span>

```python
file_service = FileService(account_name='myaccount', account_key='mykey')
```

### <a name="create-an-azure-file-share"></a><span data-ttu-id="236b1-119">Azure 파일 공유 만들기</span><span class="sxs-lookup"><span data-stu-id="236b1-119">Create an Azure File share</span></span>
<span data-ttu-id="236b1-120">다음 코드 예제는 hello에서 사용할 수 있습니다는 `FileService` 존재 하지 않는 경우 개체 toocreate hello 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="236b1-120">In hello following code example, you can use a `FileService` object toocreate hello share if it doesn't exist.</span></span>

```python
file_service.create_share('myshare')
```

### <a name="create-a-directory"></a><span data-ttu-id="236b1-121">디렉터리 만들기</span><span class="sxs-lookup"><span data-stu-id="236b1-121">Create a directory</span></span>
<span data-ttu-id="236b1-122">또한 하는 대신 모든 hello 루트 디렉터리에 하위 디렉터리 내의 파일을 배치 하 여 저장소를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="236b1-122">You can also organize storage by putting files inside sub-directories instead of having all of them in hello root directory.</span></span> <span data-ttu-id="236b1-123">Azure 파일 저장소에서는 허용 하는 사용자 계정에는으로 여러 디렉터리 만큼 toocreate를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="236b1-123">Azure File storage allows you toocreate as many directories as your account will allow.</span></span> <span data-ttu-id="236b1-124">아래 hello 코드 라는 하위 디렉터리를 만듭니다. **sampledir** hello 루트 디렉터리 아래.</span><span class="sxs-lookup"><span data-stu-id="236b1-124">hello code below will create a sub-directory named **sampledir** under hello root directory.</span></span>

```python
file_service.create_directory('myshare', 'sampledir')
```

### <a name="enumerate-files-and-directories-in-an-azure-file-share"></a><span data-ttu-id="236b1-125">Azure 파일 공유의 파일 및 디렉터리 열거</span><span class="sxs-lookup"><span data-stu-id="236b1-125">Enumerate files and directories in an Azure File share</span></span>
<span data-ttu-id="236b1-126">toolist hello 파일 및 디렉터리를 공유에서 사용 하 여 hello **목록\_디렉터리\_및\_파일** 메서드.</span><span class="sxs-lookup"><span data-stu-id="236b1-126">toolist hello files and directories in a share, use hello **list\_directories\_and\_files** method.</span></span> <span data-ttu-id="236b1-127">이 메서드는 생성기를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="236b1-127">This method returns a generator.</span></span> <span data-ttu-id="236b1-128">hello 다음 코드에서는 출력 hello **이름** 각 파일 및 공유 toohello 콘솔에서 디렉터리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="236b1-128">hello following code outputs hello **name** of each file and directory in a share toohello console.</span></span>

```python
generator = file_service.list_directories_and_files('myshare')
for file_or_dir in generator:
    print(file_or_dir.name)
```

### <a name="upload-a-file"></a><span data-ttu-id="236b1-129">파일 업로드</span><span class="sxs-lookup"><span data-stu-id="236b1-129">Upload a file</span></span> 
<span data-ttu-id="236b1-130">Azure 파일 공유에 hello에 매우 이상의 루트 디렉터리 파일이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="236b1-130">Azure File share contains at hello very least, a root directory where files can reside.</span></span> <span data-ttu-id="236b1-131">이 섹션에서는 tooupload hello에 대 한 로컬 저장소에서 파일 루트 디렉터리를 공유 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="236b1-131">In this section, you'll learn how tooupload a file from local storage onto hello root directory of a share.</span></span>

<span data-ttu-id="236b1-132">toocreate 파일 및 데이터 업로드 hello를 사용 하 여 `create_file_from_path`, `create_file_from_stream`, `create_file_from_bytes` 또는 `create_file_from_text` 메서드.</span><span class="sxs-lookup"><span data-stu-id="236b1-132">toocreate a file and upload data, use hello `create_file_from_path`, `create_file_from_stream`, `create_file_from_bytes` or `create_file_from_text` methods.</span></span> <span data-ttu-id="236b1-133">hello 데이터의 크기가 hello 초과 64MB hello 필요한 청크를 수행 하는 높은 수준의 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="236b1-133">They are high-level methods that perform hello necessary chunking when hello size of hello data exceeds 64 MB.</span></span>

<span data-ttu-id="236b1-134">`create_file_from_path`업로드 hello 지정 된 경로에서 파일의 내용을 hello 및 `create_file_from_stream` 업로드 hello 내용을 이미 열린 파일/스트림에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="236b1-134">`create_file_from_path` uploads hello contents of a file from hello specified path, and `create_file_from_stream` uploads hello contents from an already opened file/stream.</span></span> <span data-ttu-id="236b1-135">`create_file_from_bytes`업로드, 바이트의 배열 및 `create_file_from_text` 업로드 hello hello를 사용 하 여 텍스트 값 지정 인코딩 (기본값 tooUTF-8)을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="236b1-135">`create_file_from_bytes` uploads an array of bytes, and `create_file_from_text` uploads hello specified text value using hello specified encoding (defaults tooUTF-8).</span></span>

<span data-ttu-id="236b1-136">hello 다음 예제에서는 업로드 hello 내용의 hello **sunset.png** hello에 파일을 **myfile** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="236b1-136">hello following example uploads hello contents of hello **sunset.png** file into hello **myfile** file.</span></span>

```python
from azure.storage.file import ContentSettings
file_service.create_file_from_path(
    'myshare',
    None, # We want toocreate this blob in hello root directory, so we specify None for hello directory_name
    'myfile',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png'))
```

### <a name="download-a-file"></a><span data-ttu-id="236b1-137">파일 다운로드</span><span class="sxs-lookup"><span data-stu-id="236b1-137">Download a file</span></span>
<span data-ttu-id="236b1-138">toodownload 데이터 파일에서 사용 하 여 `get_file_to_path`, `get_file_to_stream`, `get_file_to_bytes`, 또는 `get_file_to_text`합니다.</span><span class="sxs-lookup"><span data-stu-id="236b1-138">toodownload data from a file, use `get_file_to_path`, `get_file_to_stream`, `get_file_to_bytes`, or `get_file_to_text`.</span></span> <span data-ttu-id="236b1-139">hello 데이터의 크기가 hello 초과 64MB hello 필요한 청크를 수행 하는 높은 수준의 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="236b1-139">They are high-level methods that perform hello necessary chunking when hello size of hello data exceeds 64 MB.</span></span>

<span data-ttu-id="236b1-140">hello 다음 예제를 사용 하 여 `get_file_to_path` toodownload hello 내용의 hello **myfile** 파일을 저장할 toohello **아웃 sunset.png** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="236b1-140">hello following example demonstrates using `get_file_to_path` toodownload hello contents of hello **myfile** file and store it toohello **out-sunset.png** file.</span></span>

```python
file_service.get_file_to_path('myshare', None, 'myfile', 'out-sunset.png')
```

### <a name="delete-a-file"></a><span data-ttu-id="236b1-141">파일 삭제</span><span class="sxs-lookup"><span data-stu-id="236b1-141">Delete a file</span></span>
<span data-ttu-id="236b1-142">마지막으로 파일을 toodelete 호출 `delete_file`합니다.</span><span class="sxs-lookup"><span data-stu-id="236b1-142">Finally, toodelete a file, call `delete_file`.</span></span>

```python
file_service.delete_file('myshare', None, 'myfile')
```

## <a name="next-steps"></a><span data-ttu-id="236b1-143">다음 단계</span><span class="sxs-lookup"><span data-stu-id="236b1-143">Next steps</span></span>
<span data-ttu-id="236b1-144">지금까지 학습 했으므로 toomanipulate python, Azure 파일 저장소의 자세한 이러한 링크 toolearn 지키는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="236b1-144">Now that you've learned how toomanipulate Azure File storage with Python, follow these links toolearn more.</span></span>

* [<span data-ttu-id="236b1-145">Python 개발자 센터</span><span class="sxs-lookup"><span data-stu-id="236b1-145">Python Developer Center</span></span>](/develop/python/)
* [<span data-ttu-id="236b1-146">Azure 저장소 서비스 REST API</span><span class="sxs-lookup"><span data-stu-id="236b1-146">Azure Storage Services REST API</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* [<span data-ttu-id="236b1-147">Microsoft Azure Storage SDK for Python</span><span class="sxs-lookup"><span data-stu-id="236b1-147">Microsoft Azure Storage SDK for Python</span></span>](https://github.com/Azure/azure-storage-python)
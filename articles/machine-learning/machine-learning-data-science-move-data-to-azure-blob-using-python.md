---
title: "Python을 사용하여 Azure Blob Storage의 데이터 이동 | Microsoft Docs"
description: "Python을 사용하여 Azure Blob 저장소의 데이터 이동"
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 24276252-b3dd-4edf-9e5d-f6803f8ccccc
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 0eea1ff8e4f4c1d108445e1a1250b6fa8ff48910
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="move-data-to-and-from-azure-blob-storage-using-python"></a><span data-ttu-id="b7e96-103">Python을 사용하여 Azure Blob Storage 간 데이터 이동</span><span class="sxs-lookup"><span data-stu-id="b7e96-103">Move data to and from Azure Blob Storage using Python</span></span>
<span data-ttu-id="b7e96-104">이 항목에서는 Python API를 사용하여 blob를 나열, 업로드 및 다운로드하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b7e96-104">This topic describes how to list, upload, and download blobs using the Python API.</span></span> <span data-ttu-id="b7e96-105">Azure SDK에 제공되는 Python API를 사용하여 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7e96-105">With the Python API provided in Azure SDK, you can:</span></span>

* <span data-ttu-id="b7e96-106">컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="b7e96-106">Create a container</span></span>
* <span data-ttu-id="b7e96-107">컨테이너에 Blob 업로드</span><span class="sxs-lookup"><span data-stu-id="b7e96-107">Upload a blob into a container</span></span>
* <span data-ttu-id="b7e96-108">Blob 다운로드</span><span class="sxs-lookup"><span data-stu-id="b7e96-108">Download blobs</span></span>
* <span data-ttu-id="b7e96-109">컨테이너의 Blob 나열</span><span class="sxs-lookup"><span data-stu-id="b7e96-109">List the blobs in a container</span></span>
* <span data-ttu-id="b7e96-110">Blob 삭제</span><span class="sxs-lookup"><span data-stu-id="b7e96-110">Delete a blob</span></span>

<span data-ttu-id="b7e96-111">Python API 사용에 대한 자세한 내용은 [Python에서 Blob 저장소 서비스를 사용하는 방법](../storage/blobs/storage-python-how-to-use-blob-storage.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b7e96-111">For more information about using the Python API, see [How to Use the Blob Storage Service from Python](../storage/blobs/storage-python-how-to-use-blob-storage.md).</span></span>

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> <span data-ttu-id="b7e96-112">[Azure의 데이터 과학 가상 컴퓨터](machine-learning-data-science-virtual-machines.md)에서 제공하는 스크립트를 통해 설정된 VM을 사용하는 경우 AzCopy가 VM에 이미 설치되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7e96-112">If you are using VM that was set up with the scripts provided by [Data Science Virtual machines in Azure](machine-learning-data-science-virtual-machines.md), then AzCopy is already installed on the VM.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="b7e96-113">Azure Blob Storage에 대한 전체 소개 내용은 [Azure Blob 기본 사항](../storage/blobs/storage-dotnet-how-to-use-blobs.md) 및 [Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b7e96-113">For a complete introduction to Azure blob storage, refer to [Azure Blob Basics](../storage/blobs/storage-dotnet-how-to-use-blobs.md) and to [Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="b7e96-114">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b7e96-114">Prerequisites</span></span>
<span data-ttu-id="b7e96-115">이 문서에서는 사용자에게 Azure 구독, 저장소 계정 및 계정에 해당하는 저장소 키가 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="b7e96-115">This document assumes that you have an Azure subscription, a storage account, and the corresponding storage key for that account.</span></span> <span data-ttu-id="b7e96-116">데이터를 업로드/다운로드하려면 Azure 저장소 계정 이름 및 계정 키를 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7e96-116">Before uploading/downloading data, you must know your Azure storage account name and account key.</span></span>

* <span data-ttu-id="b7e96-117">Azure 구독을 설정하려면 [1개월 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b7e96-117">To set up an Azure subscription, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="b7e96-118">저장소 계정을 만들고 계정 및 키 정보를 가져오는 방법에 대한 지침은 [Azure 저장소 계정 정보](../storage/common/storage-create-storage-account.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b7e96-118">For instructions on creating a storage account and for getting account and key information, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

## <a name="upload-data-to-blob"></a><span data-ttu-id="b7e96-119">Blob에 데이터 업로드</span><span class="sxs-lookup"><span data-stu-id="b7e96-119">Upload Data to Blob</span></span>
<span data-ttu-id="b7e96-120">프로그래밍 방식으로 Azure 저장소에 액세스하려는 Python 코드의 맨 위쪽에 다음 코드 조각을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b7e96-120">Add the following snippet near the top of any Python code in which you wish to programmatically access Azure Storage:</span></span>

    from azure.storage.blob import BlobService

<span data-ttu-id="b7e96-121">**BlobService** 개체를 통해 컨테이너 및 Blob에 대한 작업을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7e96-121">The **BlobService** object lets you work with containers and blobs.</span></span> <span data-ttu-id="b7e96-122">다음 코드에서는 저장소 계정 이름 및 계정 키를 사용하는 BlobService 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b7e96-122">The following code creates a BlobService object using the storage account name and account key.</span></span> <span data-ttu-id="b7e96-123">계정 이름 및 계정 키를 실제 계정 및 키로 바꾸세요.</span><span class="sxs-lookup"><span data-stu-id="b7e96-123">Replace account name and account key with your real account and key.</span></span>

    blob_service = BlobService(account_name="<your_account_name>", account_key="<your_account_key>")

<span data-ttu-id="b7e96-124">다음 메서드를 사용하여 blob에 데이터를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="b7e96-124">Use the following methods to upload data to a blob:</span></span>

1. <span data-ttu-id="b7e96-125">put\_block\_blob\_from\_path(지정된 경로의 파일 콘텐츠 업로드)</span><span class="sxs-lookup"><span data-stu-id="b7e96-125">put\_block\_blob\_from\_path (uploads the contents of a file from the specified path)</span></span>
2. <span data-ttu-id="b7e96-126">put\_block_blob\_from\_file(이미 열려 있는 파일/스트림의 콘텐츠 업로드)</span><span class="sxs-lookup"><span data-stu-id="b7e96-126">put\_block_blob\_from\_file (uploads the contents from an already opened file/stream)</span></span>
3. <span data-ttu-id="b7e96-127">put\_block\_blob\_from\_bytes(바이트 배열 업로드)</span><span class="sxs-lookup"><span data-stu-id="b7e96-127">put\_block\_blob\_from\_bytes (uploads an array of bytes)</span></span>
4. <span data-ttu-id="b7e96-128">put\_block\_blob\_from\_text(지정된 인코딩을 사용하여 지정된 텍스트 값 업로드)</span><span class="sxs-lookup"><span data-stu-id="b7e96-128">put\_block\_blob\_from\_text (uploads the specified text value using the specified encoding)</span></span>

<span data-ttu-id="b7e96-129">다음은 로컬 파일을 컨테이너에 업로드하는 샘플 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="b7e96-129">The following sample code uploads a local file to a container:</span></span>

    blob_service.put_block_blob_from_path("<your_container_name>", "<your_blob_name>", "<your_local_file_name>")

<span data-ttu-id="b7e96-130">다음은 로컬 디렉터리의 모든 파일(디렉터리 제외)을 blob 저장소에 업로드하는 샘플 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="b7e96-130">The following sample code uploads all the files (excluding directories) in a local directory to blob storage:</span></span>

    from azure.storage.blob import BlobService
    from os import listdir
    from os.path import isfile, join

    # Set parameters here
    ACCOUNT_NAME = "<your_account_name>"
    ACCOUNT_KEY = "<your_account_key>"
    CONTAINER_NAME = "<your_container_name>"
    LOCAL_DIRECT = "<your_local_directory>"        

    blob_service = BlobService(account_name=ACCOUNT_NAME, account_key=ACCOUNT_KEY)
    # find all files in the LOCAL_DIRECT (excluding directory)
    local_file_list = [f for f in listdir(LOCAL_DIRECT) if isfile(join(LOCAL_DIRECT, f))]

    file_num = len(local_file_list)
    for i in range(file_num):
        local_file = join(LOCAL_DIRECT, local_file_list[i])
        blob_name = local_file_list[i]
        try:
            blob_service.put_block_blob_from_path(CONTAINER_NAME, blob_name, local_file)
        except:
            print "something wrong happened when uploading the data %s"%blob_name


## <a name="download-data-from-blob"></a><span data-ttu-id="b7e96-131">Blob에서 데이터 다운로드</span><span class="sxs-lookup"><span data-stu-id="b7e96-131">Download Data from Blob</span></span>
<span data-ttu-id="b7e96-132">다음 메서드를 사용하여 blob에서 데이터를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="b7e96-132">Use the following methods to download data from a blob:</span></span>

1. <span data-ttu-id="b7e96-133">get\_blob\_to\_path</span><span class="sxs-lookup"><span data-stu-id="b7e96-133">get\_blob\_to\_path</span></span>
2. <span data-ttu-id="b7e96-134">get\_blob\_to\_file</span><span class="sxs-lookup"><span data-stu-id="b7e96-134">get\_blob\_to\_file</span></span>
3. <span data-ttu-id="b7e96-135">get\_blob\_to\_bytes</span><span class="sxs-lookup"><span data-stu-id="b7e96-135">get\_blob\_to\_bytes</span></span>
4. <span data-ttu-id="b7e96-136">get\_blob\_to\_text</span><span class="sxs-lookup"><span data-stu-id="b7e96-136">get\_blob\_to\_text</span></span>

<span data-ttu-id="b7e96-137">데이터의 크기가 64MB를 초과할 경우 필요한 청크를 수행하는 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="b7e96-137">These methods that perform the necessary chunking when the size of the data exceeds 64 MB.</span></span>

<span data-ttu-id="b7e96-138">다음은 컨테이너에 있는 blob의 콘텐츠를 로컬 파일에 다운로드하는 샘플 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="b7e96-138">The following sample code downloads the contents of a blob in a container to a local file:</span></span>

    blob_service.get_blob_to_path("<your_container_name>", "<your_blob_name>", "<your_local_file_name>")

<span data-ttu-id="b7e96-139">다음은 컨테이너의 모든 blob를 다운로드하는 샘플 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="b7e96-139">The following sample code downloads all blobs from a container.</span></span> <span data-ttu-id="b7e96-140">이 샘플 코드는 list\_blobs를 사용하여 컨테이너의 사용 가능한 Blob 목록을 가져오고 로컬 디렉터리에 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="b7e96-140">It uses list\_blobs to get the list of available blobs in the container and downloads them to a local directory.</span></span>

    from azure.storage.blob import BlobService
    from os.path import join

    # Set parameters here
    ACCOUNT_NAME = "<your_account_name>"
    ACCOUNT_KEY = "<your_account_key>"
    CONTAINER_NAME = "<your_container_name>"
    LOCAL_DIRECT = "<your_local_directory>"        

    blob_service = BlobService(account_name=ACCOUNT_NAME, account_key=ACCOUNT_KEY)

    # List all blobs and download them one by one
    blobs = blob_service.list_blobs(CONTAINER_NAME)
    for blob in blobs:
        local_file = join(LOCAL_DIRECT, blob.name)
        try:
            blob_service.get_blob_to_path(CONTAINER_NAME, blob.name, local_file)
        except:
            print "something wrong happened when downloading the data %s"%blob.name

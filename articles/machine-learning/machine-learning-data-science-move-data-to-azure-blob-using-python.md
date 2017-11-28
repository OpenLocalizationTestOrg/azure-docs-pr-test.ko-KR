---
title: "Python을 사용 하 여 Azure Blob 저장소에서 데이터 tooand aaaMove | Microsoft Docs"
description: "Python을 사용 하 여 Azure Blob 저장소에서 데이터 tooand 이동"
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
ms.openlocfilehash: c2be9600e0d6cb05bcf4109a8d554db522704ecb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-blob-storage-using-python"></a><span data-ttu-id="eaac7-103">Python을 사용 하 여 Azure Blob 저장소에서 데이터 tooand 이동</span><span class="sxs-lookup"><span data-stu-id="eaac7-103">Move data tooand from Azure Blob Storage using Python</span></span>
<span data-ttu-id="eaac7-104">이 항목에서는 toolist, 업로드 하 고 hello Python API를 사용 하 여 blob를 다운로드 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaac7-104">This topic describes how toolist, upload, and download blobs using hello Python API.</span></span> <span data-ttu-id="eaac7-105">Azure SDK에 제공 된 Python API hello로 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaac7-105">With hello Python API provided in Azure SDK, you can:</span></span>

* <span data-ttu-id="eaac7-106">컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="eaac7-106">Create a container</span></span>
* <span data-ttu-id="eaac7-107">컨테이너에 Blob 업로드</span><span class="sxs-lookup"><span data-stu-id="eaac7-107">Upload a blob into a container</span></span>
* <span data-ttu-id="eaac7-108">Blob 다운로드</span><span class="sxs-lookup"><span data-stu-id="eaac7-108">Download blobs</span></span>
* <span data-ttu-id="eaac7-109">컨테이너에서 hello blob 나열</span><span class="sxs-lookup"><span data-stu-id="eaac7-109">List hello blobs in a container</span></span>
* <span data-ttu-id="eaac7-110">Blob 삭제</span><span class="sxs-lookup"><span data-stu-id="eaac7-110">Delete a blob</span></span>

<span data-ttu-id="eaac7-111">Hello Python API를 사용 하는 방법에 대 한 자세한 내용은 참조 [어떻게 tooUse hello Python에서 Blob 저장소 서비스](../storage/blobs/storage-python-how-to-use-blob-storage.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="eaac7-111">For more information about using hello Python API, see [How tooUse hello Blob Storage Service from Python](../storage/blobs/storage-python-how-to-use-blob-storage.md).</span></span>

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> <span data-ttu-id="eaac7-112">제공 된 hello 스크립트를 사용 하 여 설정 된 VM을 사용 하는 경우 [Azure의 데이터 과학 가상 컴퓨터](machine-learning-data-science-virtual-machines.md), 다음 AzCopy hello VM에 이미 설치 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaac7-112">If you are using VM that was set up with hello scripts provided by [Data Science Virtual machines in Azure](machine-learning-data-science-virtual-machines.md), then AzCopy is already installed on hello VM.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="eaac7-113">전체 소개 tooAzure blob 저장소에 대 한 참조 너무[Azure Blob 기본 사항](../storage/blobs/storage-dotnet-how-to-use-blobs.md) 및 너무[Azure Blob 서비스](https://msdn.microsoft.com/library/azure/dd179376.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="eaac7-113">For a complete introduction tooAzure blob storage, refer too[Azure Blob Basics](../storage/blobs/storage-dotnet-how-to-use-blobs.md) and too[Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="eaac7-114">필수 조건</span><span class="sxs-lookup"><span data-stu-id="eaac7-114">Prerequisites</span></span>
<span data-ttu-id="eaac7-115">이 문서는 Azure 구독, 저장소 계정 및 해당 계정에 대 한 해당 저장소 키 hello 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaac7-115">This document assumes that you have an Azure subscription, a storage account, and hello corresponding storage key for that account.</span></span> <span data-ttu-id="eaac7-116">데이터를 업로드/다운로드하려면 Azure 저장소 계정 이름 및 계정 키를 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaac7-116">Before uploading/downloading data, you must know your Azure storage account name and account key.</span></span>

* <span data-ttu-id="eaac7-117">한 Azure 구독을 tooset 참조 [무료 1 개월 평가판](https://azure.microsoft.com/pricing/free-trial/)합니다.</span><span class="sxs-lookup"><span data-stu-id="eaac7-117">tooset up an Azure subscription, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="eaac7-118">저장소 계정을 만들고 계정 및 키 정보를 가져오는 방법에 대한 지침은 [Azure 저장소 계정 정보](../storage/common/storage-create-storage-account.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="eaac7-118">For instructions on creating a storage account and for getting account and key information, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

## <a name="upload-data-tooblob"></a><span data-ttu-id="eaac7-119">데이터 tooBlob 업로드</span><span class="sxs-lookup"><span data-stu-id="eaac7-119">Upload Data tooBlob</span></span>
<span data-ttu-id="eaac7-120">다음 코드 조각 tooprogrammatically Azure 저장소 액세스 원하는 모든 Python 코드의 hello 위쪽 hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaac7-120">Add hello following snippet near hello top of any Python code in which you wish tooprogrammatically access Azure Storage:</span></span>

    from azure.storage.blob import BlobService

<span data-ttu-id="eaac7-121">hello **BlobService** 개체 컨테이너 및 blob를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaac7-121">hello **BlobService** object lets you work with containers and blobs.</span></span> <span data-ttu-id="eaac7-122">hello 코드 다음에 hello 저장소 계정 이름 및 계정 키를 사용 하 여 BlobService 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eaac7-122">hello following code creates a BlobService object using hello storage account name and account key.</span></span> <span data-ttu-id="eaac7-123">계정 이름 및 계정 키를 실제 계정 및 키로 바꾸세요.</span><span class="sxs-lookup"><span data-stu-id="eaac7-123">Replace account name and account key with your real account and key.</span></span>

    blob_service = BlobService(account_name="<your_account_name>", account_key="<your_account_key>")

<span data-ttu-id="eaac7-124">다음 메서드 tooupload 데이터 tooa blob hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaac7-124">Use hello following methods tooupload data tooa blob:</span></span>

1. <span data-ttu-id="eaac7-125">배치\_블록\_blob\_에서\_경로 (hello 지정 된 경로에서 파일의 내용을 hello 업로드)</span><span class="sxs-lookup"><span data-stu-id="eaac7-125">put\_block\_blob\_from\_path (uploads hello contents of a file from hello specified path)</span></span>
2. <span data-ttu-id="eaac7-126">배치\_block_blob\_에서\_(이미 열려 있는 파일/스트림에서 hello 내용을 업로드) 파일</span><span class="sxs-lookup"><span data-stu-id="eaac7-126">put\_block_blob\_from\_file (uploads hello contents from an already opened file/stream)</span></span>
3. <span data-ttu-id="eaac7-127">put\_block\_blob\_from\_bytes(바이트 배열 업로드)</span><span class="sxs-lookup"><span data-stu-id="eaac7-127">put\_block\_blob\_from\_bytes (uploads an array of bytes)</span></span>
4. <span data-ttu-id="eaac7-128">배치\_블록\_blob\_에서\_텍스트 (지정 된 hello 업로드 hello를 사용 하 여 텍스트 값 인코딩을 지정)</span><span class="sxs-lookup"><span data-stu-id="eaac7-128">put\_block\_blob\_from\_text (uploads hello specified text value using hello specified encoding)</span></span>

<span data-ttu-id="eaac7-129">다음 샘플 코드는 hello 업로드 로컬 파일 tooa 컨테이너:</span><span class="sxs-lookup"><span data-stu-id="eaac7-129">hello following sample code uploads a local file tooa container:</span></span>

    blob_service.put_block_blob_from_path("<your_container_name>", "<your_blob_name>", "<your_local_file_name>")

<span data-ttu-id="eaac7-130">hello 다음 샘플 코드 파일을 업로드 모든 hello (디렉터리 제외)은 로컬 디렉터리 tooblob 저장소에서:</span><span class="sxs-lookup"><span data-stu-id="eaac7-130">hello following sample code uploads all hello files (excluding directories) in a local directory tooblob storage:</span></span>

    from azure.storage.blob import BlobService
    from os import listdir
    from os.path import isfile, join

    # Set parameters here
    ACCOUNT_NAME = "<your_account_name>"
    ACCOUNT_KEY = "<your_account_key>"
    CONTAINER_NAME = "<your_container_name>"
    LOCAL_DIRECT = "<your_local_directory>"        

    blob_service = BlobService(account_name=ACCOUNT_NAME, account_key=ACCOUNT_KEY)
    # find all files in hello LOCAL_DIRECT (excluding directory)
    local_file_list = [f for f in listdir(LOCAL_DIRECT) if isfile(join(LOCAL_DIRECT, f))]

    file_num = len(local_file_list)
    for i in range(file_num):
        local_file = join(LOCAL_DIRECT, local_file_list[i])
        blob_name = local_file_list[i]
        try:
            blob_service.put_block_blob_from_path(CONTAINER_NAME, blob_name, local_file)
        except:
            print "something wrong happened when uploading hello data %s"%blob_name


## <a name="download-data-from-blob"></a><span data-ttu-id="eaac7-131">Blob에서 데이터 다운로드</span><span class="sxs-lookup"><span data-stu-id="eaac7-131">Download Data from Blob</span></span>
<span data-ttu-id="eaac7-132">Blob에서 같은 메서드 toodownload 데이터가 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaac7-132">Use hello following methods toodownload data from a blob:</span></span>

1. <span data-ttu-id="eaac7-133">get\_blob\_to\_path</span><span class="sxs-lookup"><span data-stu-id="eaac7-133">get\_blob\_to\_path</span></span>
2. <span data-ttu-id="eaac7-134">get\_blob\_to\_file</span><span class="sxs-lookup"><span data-stu-id="eaac7-134">get\_blob\_to\_file</span></span>
3. <span data-ttu-id="eaac7-135">get\_blob\_to\_bytes</span><span class="sxs-lookup"><span data-stu-id="eaac7-135">get\_blob\_to\_bytes</span></span>
4. <span data-ttu-id="eaac7-136">get\_blob\_to\_text</span><span class="sxs-lookup"><span data-stu-id="eaac7-136">get\_blob\_to\_text</span></span>

<span data-ttu-id="eaac7-137">Hello 데이터의 크기가 hello 초과 64MB hello 필요한 청크를 수행 하는 이러한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="eaac7-137">These methods that perform hello necessary chunking when hello size of hello data exceeds 64 MB.</span></span>

<span data-ttu-id="eaac7-138">hello 다음 샘플 코드를 다운로드 컨테이너 tooa 로컬 파일에 있는 blob의 내용을 hello:</span><span class="sxs-lookup"><span data-stu-id="eaac7-138">hello following sample code downloads hello contents of a blob in a container tooa local file:</span></span>

    blob_service.get_blob_to_path("<your_container_name>", "<your_blob_name>", "<your_local_file_name>")

<span data-ttu-id="eaac7-139">hello 다음 샘플 코드를 다운로드 모든 blob 컨테이너에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaac7-139">hello following sample code downloads all blobs from a container.</span></span> <span data-ttu-id="eaac7-140">목록을 사용 하 여\_tooget hello 목록 hello 컨테이너에 사용할 수 있는 blob의 blob를 tooa 로컬 디렉터리를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaac7-140">It uses list\_blobs tooget hello list of available blobs in hello container and downloads them tooa local directory.</span></span>

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
            print "something wrong happened when downloading hello data %s"%blob.name

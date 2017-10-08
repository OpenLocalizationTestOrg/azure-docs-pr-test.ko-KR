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
# <a name="move-data-tooand-from-azure-blob-storage-using-python"></a>Python을 사용 하 여 Azure Blob 저장소에서 데이터 tooand 이동
이 항목에서는 toolist, 업로드 하 고 hello Python API를 사용 하 여 blob를 다운로드 하는 방법에 대해 설명 합니다. Azure SDK에 제공 된 Python API hello로 다음을 수행할 수 있습니다.

* 컨테이너 만들기
* 컨테이너에 Blob 업로드
* Blob 다운로드
* 컨테이너에서 hello blob 나열
* Blob 삭제

Hello Python API를 사용 하는 방법에 대 한 자세한 내용은 참조 [어떻게 tooUse hello Python에서 Blob 저장소 서비스](../storage/blobs/storage-python-how-to-use-blob-storage.md)합니다.

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> 제공 된 hello 스크립트를 사용 하 여 설정 된 VM을 사용 하는 경우 [Azure의 데이터 과학 가상 컴퓨터](machine-learning-data-science-virtual-machines.md), 다음 AzCopy hello VM에 이미 설치 되어 있습니다.
> 
> [!NOTE]
> 전체 소개 tooAzure blob 저장소에 대 한 참조 너무[Azure Blob 기본 사항](../storage/blobs/storage-dotnet-how-to-use-blobs.md) 및 너무[Azure Blob 서비스](https://msdn.microsoft.com/library/azure/dd179376.aspx)합니다.
> 
> 

## <a name="prerequisites"></a>필수 조건
이 문서는 Azure 구독, 저장소 계정 및 해당 계정에 대 한 해당 저장소 키 hello 있다고 가정 합니다. 데이터를 업로드/다운로드하려면 Azure 저장소 계정 이름 및 계정 키를 알아야 합니다.

* 한 Azure 구독을 tooset 참조 [무료 1 개월 평가판](https://azure.microsoft.com/pricing/free-trial/)합니다.
* 저장소 계정을 만들고 계정 및 키 정보를 가져오는 방법에 대한 지침은 [Azure 저장소 계정 정보](../storage/common/storage-create-storage-account.md)를 참조하세요.

## <a name="upload-data-tooblob"></a>데이터 tooBlob 업로드
다음 코드 조각 tooprogrammatically Azure 저장소 액세스 원하는 모든 Python 코드의 hello 위쪽 hello를 추가 합니다.

    from azure.storage.blob import BlobService

hello **BlobService** 개체 컨테이너 및 blob를 사용할 수 있습니다. hello 코드 다음에 hello 저장소 계정 이름 및 계정 키를 사용 하 여 BlobService 개체를 만듭니다. 계정 이름 및 계정 키를 실제 계정 및 키로 바꾸세요.

    blob_service = BlobService(account_name="<your_account_name>", account_key="<your_account_key>")

다음 메서드 tooupload 데이터 tooa blob hello를 사용 합니다.

1. 배치\_블록\_blob\_에서\_경로 (hello 지정 된 경로에서 파일의 내용을 hello 업로드)
2. 배치\_block_blob\_에서\_(이미 열려 있는 파일/스트림에서 hello 내용을 업로드) 파일
3. put\_block\_blob\_from\_bytes(바이트 배열 업로드)
4. 배치\_블록\_blob\_에서\_텍스트 (지정 된 hello 업로드 hello를 사용 하 여 텍스트 값 인코딩을 지정)

다음 샘플 코드는 hello 업로드 로컬 파일 tooa 컨테이너:

    blob_service.put_block_blob_from_path("<your_container_name>", "<your_blob_name>", "<your_local_file_name>")

hello 다음 샘플 코드 파일을 업로드 모든 hello (디렉터리 제외)은 로컬 디렉터리 tooblob 저장소에서:

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


## <a name="download-data-from-blob"></a>Blob에서 데이터 다운로드
Blob에서 같은 메서드 toodownload 데이터가 hello를 사용 합니다.

1. get\_blob\_to\_path
2. get\_blob\_to\_file
3. get\_blob\_to\_bytes
4. get\_blob\_to\_text

Hello 데이터의 크기가 hello 초과 64MB hello 필요한 청크를 수행 하는 이러한 방법입니다.

hello 다음 샘플 코드를 다운로드 컨테이너 tooa 로컬 파일에 있는 blob의 내용을 hello:

    blob_service.get_blob_to_path("<your_container_name>", "<your_blob_name>", "<your_local_file_name>")

hello 다음 샘플 코드를 다운로드 모든 blob 컨테이너에서 합니다. 목록을 사용 하 여\_tooget hello 목록 hello 컨테이너에 사용할 수 있는 blob의 blob를 tooa 로컬 디렉터리를 다운로드 합니다.

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

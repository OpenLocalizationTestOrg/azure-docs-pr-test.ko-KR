---
title: "aaaHow toouse Python에서 Azure Blob 저장소 (개체 저장소) | Microsoft Docs"
description: "Azure Blob 저장소 (개체 저장소)를 사용 하는 hello 클라우드에 구조화 되지 않은 데이터를 저장 합니다."
services: storage
documentationcenter: python
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 0348e360-b24d-41fa-bb12-b8f18990d8bc
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 2/24/2017
ms.author: marsma
ms.openlocfilehash: 6efc61aa89e6d2544b7a18c80ce3546640f90462
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-blob-storage-from-python"></a>어떻게 toouse Python에서 Azure Blob 저장소
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>개요
Azure Blob 저장소는 hello 클라우드에서 개체/blob으로 구조화 되지 않은 데이터를 저장 하는 서비스입니다. Blob storage는 문서, 미디어 파일 또는 응용 프로그램 설치 프로그램과 같은 모든 종류의 텍스트 또는 이진 데이터를 저장할 수 있습니다. Blob 저장소 참조 tooas 개체 저장소 이기도합니다.

이 문서에서는 보여 어떻게 tooperform Blob 저장소를 사용 하는 일반적인 시나리오입니다. hello 샘플 Python에서 작성 되 고 hello를 사용 하 여 [Python에 대 한 Microsoft Azure 저장소 SDK]합니다. 가이드에서 다루는 hello 시나리오 업로드, 나열, 다운로드 및 blob 삭제를 포함 합니다.

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-container"></a>컨테이너 만들기
Blob의 hello 형식에 따라 원하는 toouse을 만듭니다는 **BlockBlobService**, **AppendBlobService**, 또는 **PageBlobService** 개체입니다. hello 다음 코드에서는 **BlockBlobService** 개체입니다. 원하는 tooprogrammatically 액세스 Azure 블록 Blob 저장소에 있는 모든 Python 파일의 hello 맨 위 근처에 hello 다음을 추가 합니다.

```python
from azure.storage.blob import BlockBlobService
```

hello 다음 코드에서는 **BlockBlobService** hello 저장소 계정 이름 및 계정 키를 사용 하 여 개체입니다.  'myaccount' 및 'mykey'를 사용자의 계정 이름 및 키로 바꾸세요.

```python
block_blob_service = BlockBlobService(account_name='myaccount', account_key='mykey')
```

[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

다음 코드 예제는 hello에서 사용할 수 있습니다는 **BlockBlobService** 개체 toocreate hello 컨테이너 존재 하지 않는 경우.

```python
block_blob_service.create_container('mycontainer')
```

기본적으로 hello 새 컨테이너는 private 이므로 (마찬가지로 이전 버전) 저장소 액세스 키를 지정 해야이 컨테이너에서 blob toodownload 합니다. Hello 컨테이너 사용 가능한 tooeveryone 내 toomake hello blob을 원한다 면 hello 컨테이너를 만들고 코드 다음 hello를 사용 하 여 hello 공용 액세스 수준을 전달할 수 있습니다.

```python
from azure.storage.blob import PublicAccess
block_blob_service.create_container('mycontainer', public_access=PublicAccess.Container)
```

또는 코드 다음 hello를 사용 하 여 만든 후에 컨테이너를 수정할 수 있습니다.

```python
block_blob_service.set_container_acl('mycontainer', public_access=PublicAccess.Container)
```

이 변경 후 hello 인터넷에서 누구 든 지 공용 컨테이너의 blob를 볼 수 있지만 수정 하거나 삭제할 수 있습니다.

## <a name="upload-a-blob-into-a-container"></a>컨테이너에 Blob 업로드
toocreate 블록 blob 및 업로드 데이터를 사용 하 여 hello **만들\_blob\_에서\_경로**, **만들\_blob\_에서\_스트림**, **만들\_blob\_에서\_바이트** 또는 **만들\_blob\_에서\_텍스트** 메서드를 합니다. hello 데이터의 크기가 hello 초과 64MB hello 필요한 청크를 수행 하는 높은 수준의 메서드입니다.

**만들\_blob\_에서\_경로** 업로드 hello 지정 된 경로에서 파일의 내용을 hello 및 **만들\_blob\_에서\_스트림** 업로드 hello 내용을 이미 열린 파일/스트림에서 합니다. **만들\_blob\_에서\_바이트** 업로드, 바이트의 배열 및 **만들\_blob\_에서\_텍스트** 지정 hello 업로드 hello를 사용 하 여 텍스트 값 인코딩 (기본값 tooUTF-8)를 지정 합니다.

hello 다음 예제에서는 업로드 hello 내용의 hello **sunset.png** hello에 파일을 **myblob** blob입니다.

```python
from azure.storage.blob import ContentSettings
block_blob_service.create_blob_from_path(
    'mycontainer',
    'myblockblob',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png')
            )
```

## <a name="list-hello-blobs-in-a-container"></a>컨테이너에서 hello blob 나열
toolist hello blob 컨테이너에서 hello를 사용 하 여 **목록\_blob** 메서드. 이 메서드는 생성기를 반환합니다. hello 다음 코드에서는 출력 hello **이름** 컨테이너 toohello 콘솔에서 각 blob의 합니다.

```python
generator = block_blob_service.list_blobs('mycontainer')
for blob in generator:
    print(blob.name)
```

## <a name="download-blobs"></a>Blob 다운로드
toodownload 데이터는 blob에서 사용 하 여 **가져오기\_blob\_를\_경로**, **가져오기\_blob\_를\_스트림**, **가져올\_blob\_를\_바이트**, 또는 **가져오기\_blob\_를\_텍스트**합니다. hello 데이터의 크기가 hello 초과 64MB hello 필요한 청크를 수행 하는 높은 수준의 메서드입니다.

hello 다음 예제를 사용 하 여 **가져오기\_blob\_를\_경로** toodownload hello 내용의 hello **myblob** blob 및 toohello 저장**아웃 sunset.png** 파일입니다.

```python
block_blob_service.get_blob_to_path('mycontainer', 'myblockblob', 'out-sunset.png')
```

## <a name="delete-a-blob"></a>Blob 삭제
마지막으로, blob toodelete 호출 **delete_blob**합니다.

```python
block_blob_service.delete_blob('mycontainer', 'myblockblob')
```

## <a name="writing-tooan-append-blob"></a>쓰기 tooan 추가 blob
추가 Blob은 로깅 등의 추가 작업에 최적화되어 있습니다. 블록 blob와 같은 추가 blob는 블록으로 구성 됩니다 이지만 새 블록 tooan 추가 blob에 추가 하면 항상 hello blob의 추가 toohello 종료 합니다. 추가 Blob의 기존 블록을 업데이트하거나 삭제할 수는 없습니다. 추가 blob에 대 한 hello 블록 Id에는 블록 blob으로 노출 되지 않습니다.

추가 blob의 각 블록 tooa 최대 4MB, 위로 크기가 다양할 수 있습니다 및 추가 blob는 최대 50, 000 블록을 포함할 수 있습니다. hello 추가 blob의 최대 크기 (4 MB X 50, 000 블록) 195 GB 보다 조금 더 큰 되므로 합니다.

hello 감시할 새 blob를 만들고 간단한 로깅 작업을 시뮬레이션 일부 데이터 tooit 추가 합니다.

```python
from azure.storage.blob import AppendBlobService
append_blob_service = AppendBlobService(account_name='myaccount', account_key='mykey')

# hello same containers can hold all types of blobs
append_blob_service.create_container('mycontainer')

# Append blobs must be created before they are appended to
append_blob_service.create_blob('mycontainer', 'myappendblob')
append_blob_service.append_blob_from_text('mycontainer', 'myappendblob', u'Hello, world!')

append_blob = append_blob_service.get_blob_to_text('mycontainer', 'myappendblob')
```

## <a name="next-steps"></a>다음 단계
Blob 저장소의 기본 사항 hello를 알아보았습니다 했으므로 이러한 링크 toolearn 자세한 수행 합니다.

* [Python 개발자 센터](https://azure.microsoft.com/develop/python/)
* [Azure 저장소 서비스 REST API](http://msdn.microsoft.com/library/azure/dd179355)
* [Azure 저장소 팀 블로그]
* [Python에 대 한 Microsoft Azure 저장소 SDK]

[Azure 저장소 팀 블로그]: http://blogs.msdn.com/b/windowsazurestorage/
[Python에 대 한 Microsoft Azure 저장소 SDK]: https://github.com/Azure/azure-storage-python

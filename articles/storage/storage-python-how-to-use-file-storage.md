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
ms.openlocfilehash: 45623e6dbec6f140cedc4e58e56a93fb4af9054e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-python"></a>Python을 사용하여 Azure File Storage용으로 개발
[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-try-azure-tools-files](../../includes/storage-try-azure-tools-files.md)]

## <a name="about-this-tutorial"></a>이 자습서 정보
이 자습서에서는 Python toodevelop 응용 프로그램이 나 Azure 파일 저장소 toostore 파일 데이터를 사용 하는 서비스를 사용 하 여의 hello 기본 사항을 보여 줍니다. 이 자습서에서는 간단한 콘솔 응용 프로그램 만들어져 표시 방법을 Python 및 Azure 파일 저장소를 사용 하 여 기본 동작 tooperform:

* Azure 파일 공유 만들기
* 디렉터리 만들기
* Azure 파일 공유에 파일 및 디렉터리 열거
* 파일 업로드, 다운로드 및 삭제

> [!Note]  
> SMB를 통한 Azure 파일 저장소에 액세스할 수 있습니다, 되므로 hello 표준 Python I/O 클래스 및 함수를 사용 하 여 hello Azure 파일 공유에 액세스 가능한 toowrite 간단한 응용 프로그램. 이 문서를 사용 하는 toowrite 응용 프로그램 hello를 사용 하 여 Azure 저장소 Python SDK hello 하는 방법을 설명 합니다 [Azure 파일 저장소 REST API](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure 파일 저장소.

### <a name="set-up-your-application-toouse-azure-file-storage"></a>사용자 응용 프로그램 toouse Azure 파일 저장소 설정
Azure 저장소 tooprogrammatically 액세스 원하는 모든 Python 원본 파일의 hello 위쪽 hello 다음을 추가 합니다.

```python
from azure.storage.file import FileService
```

### <a name="set-up-a-connection-tooazure-file-storage"></a>연결 tooAzure 파일 저장소 설정 
hello `FileService` 개체를 사용 하면 공유, 디렉터리 및 파일을 작업할 수 있습니다. hello 다음 코드에서는 `FileService` hello 저장소 계정 이름 및 계정 키를 사용 하 여 개체입니다. `<myaccount>` 및 `<mykey>`를 사용자의 계정 이름 및 키로 바꾸세요.

```python
file_service = FileService(account_name='myaccount', account_key='mykey')
```

### <a name="create-an-azure-file-share"></a>Azure 파일 공유 만들기
다음 코드 예제는 hello에서 사용할 수 있습니다는 `FileService` 존재 하지 않는 경우 개체 toocreate hello 공유 합니다.

```python
file_service.create_share('myshare')
```

### <a name="create-a-directory"></a>디렉터리 만들기
또한 하는 대신 모든 hello 루트 디렉터리에 하위 디렉터리 내의 파일을 배치 하 여 저장소를 구성할 수 있습니다. Azure 파일 저장소에서는 허용 하는 사용자 계정에는으로 여러 디렉터리 만큼 toocreate를 허용 합니다. 아래 hello 코드 라는 하위 디렉터리를 만듭니다. **sampledir** hello 루트 디렉터리 아래.

```python
file_service.create_directory('myshare', 'sampledir')
```

### <a name="enumerate-files-and-directories-in-an-azure-file-share"></a>Azure 파일 공유의 파일 및 디렉터리 열거
toolist hello 파일 및 디렉터리를 공유에서 사용 하 여 hello **목록\_디렉터리\_및\_파일** 메서드. 이 메서드는 생성기를 반환합니다. hello 다음 코드에서는 출력 hello **이름** 각 파일 및 공유 toohello 콘솔에서 디렉터리에 있습니다.

```python
generator = file_service.list_directories_and_files('myshare')
for file_or_dir in generator:
    print(file_or_dir.name)
```

### <a name="upload-a-file"></a>파일 업로드 
Azure 파일 공유에 hello에 매우 이상의 루트 디렉터리 파일이 있을 수 있습니다. 이 섹션에서는 tooupload hello에 대 한 로컬 저장소에서 파일 루트 디렉터리를 공유 하는 방법을 설명 합니다.

toocreate 파일 및 데이터 업로드 hello를 사용 하 여 `create_file_from_path`, `create_file_from_stream`, `create_file_from_bytes` 또는 `create_file_from_text` 메서드. hello 데이터의 크기가 hello 초과 64MB hello 필요한 청크를 수행 하는 높은 수준의 메서드입니다.

`create_file_from_path`업로드 hello 지정 된 경로에서 파일의 내용을 hello 및 `create_file_from_stream` 업로드 hello 내용을 이미 열린 파일/스트림에서 합니다. `create_file_from_bytes`업로드, 바이트의 배열 및 `create_file_from_text` 업로드 hello hello를 사용 하 여 텍스트 값 지정 인코딩 (기본값 tooUTF-8)을 지정 합니다.

hello 다음 예제에서는 업로드 hello 내용의 hello **sunset.png** hello에 파일을 **myfile** 파일입니다.

```python
from azure.storage.file import ContentSettings
file_service.create_file_from_path(
    'myshare',
    None, # We want toocreate this blob in hello root directory, so we specify None for hello directory_name
    'myfile',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png'))
```

### <a name="download-a-file"></a>파일 다운로드
toodownload 데이터 파일에서 사용 하 여 `get_file_to_path`, `get_file_to_stream`, `get_file_to_bytes`, 또는 `get_file_to_text`합니다. hello 데이터의 크기가 hello 초과 64MB hello 필요한 청크를 수행 하는 높은 수준의 메서드입니다.

hello 다음 예제를 사용 하 여 `get_file_to_path` toodownload hello 내용의 hello **myfile** 파일을 저장할 toohello **아웃 sunset.png** 파일입니다.

```python
file_service.get_file_to_path('myshare', None, 'myfile', 'out-sunset.png')
```

### <a name="delete-a-file"></a>파일 삭제
마지막으로 파일을 toodelete 호출 `delete_file`합니다.

```python
file_service.delete_file('myshare', None, 'myfile')
```

## <a name="next-steps"></a>다음 단계
지금까지 학습 했으므로 toomanipulate python, Azure 파일 저장소의 자세한 이러한 링크 toolearn 지키는 방법입니다.

* [Python 개발자 센터](/develop/python/)
* [Azure 저장소 서비스 REST API](http://msdn.microsoft.com/library/azure/dd179355)
* [Microsoft Azure Storage SDK for Python](https://github.com/Azure/azure-storage-python)
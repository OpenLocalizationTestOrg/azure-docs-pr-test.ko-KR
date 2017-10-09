---
title: "aaaHow toouse Ruby에서 Blob 저장소 (개체 저장소) | Microsoft Docs"
description: "Azure Blob 저장소 (개체 저장소)를 사용 하는 hello 클라우드에 구조화 되지 않은 데이터를 저장 합니다."
services: storage
documentationcenter: ruby
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: e2fe4c45-27b0-4d15-b3fb-e7eb574db717
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 776e7d788e69d4960f8dde0b783513f6b39b7a47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-ruby"></a>어떻게 toouse Ruby에서 Blob 저장소
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>개요
Azure Blob 저장소는 hello 클라우드에서 개체/blob으로 구조화 되지 않은 데이터를 저장 하는 서비스입니다. Blob storage는 문서, 미디어 파일 또는 응용 프로그램 설치 프로그램과 같은 모든 종류의 텍스트 또는 이진 데이터를 저장할 수 있습니다. Blob 저장소 참조 tooas 개체 저장소 이기도합니다.

이 가이드에서는 설명 어떻게 tooperform Blob 저장소를 사용 하는 일반적인 시나리오입니다. hello 샘플 hello Ruby API를 사용 하 여 기록 됩니다. hello 가이드에서 다루는 시나리오 포함 **업로드, 나열, 다운로드,** 및 **삭제** blob입니다.

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a>Ruby 응용 프로그램 만들기
Ruby 응용 프로그램을 만듭니다. 지침은 [Azure VM의 Ruby on Rails 웹 응용 프로그램](../../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md)을 참조하세요.

## <a name="configure-your-application-tooaccess-storage"></a>사용자 응용 프로그램 tooaccess 저장소 구성
Azure 저장소 toouse toodownload 및 사용 하 여 hello hello 저장소 REST 서비스와 통신 하는 편리한 라이브러리의 집합을 포함 하는 Ruby azure 패키지 해야 합니다.

### <a name="use-rubygems-tooobtain-hello-package"></a>RubyGems tooobtain hello 패키지 사용
1. **PowerShell**(Windows), **Terminal**(Mac) 또는 **Bash**(Unix)와 같은 명령줄 인터페이스를 사용합니다.
2. "보석" 설치 azure의 hello 명령 창 tooinstall hello 보석 및 종속성을 입력 합니다.

### <a name="import-hello-package"></a>Hello 패키지 가져오기
원하는 텍스트 편집기를 사용 하 여 hello toohello 위쪽 hello toouse 저장소 이점을 얻을 수 Ruby 파일에 다음을 추가 합니다.

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a>Azure Storage 연결 설정
hello azure 모듈 hello 환경 변수는 읽기 **AZURE\_저장소\_계정** 및 **AZURE\_저장소\_ACCESS_KEY** 에 대 한 정보는 tooconnect tooyour Azure 저장소 계정이 필요합니다. 사용 하기 전에 hello 계정 정보를 지정 해야 이러한 환경 변수가 설정 되지 않은 경우 **Azure::Blob::BlobService** 코드 다음 hello로:

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your azure storage access key>"
```

tooobtain hello Azure 포털에서에서 기존 또는 리소스 관리자 저장소에서 이러한 값 계정:

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. Toouse 사용할 toohello 저장소 계정을 이동 합니다.
3. Hello 오른쪽에 hello 설정 블레이드에서 클릭 **선택 키**합니다.
4. 나타나는 hello 액세스 키 블레이드에서 hello 선택 키 1 및 2 선택 키 표시 됩니다. 이 둘 중 하나를 사용할 수 있습니다.
5. Hello 아이콘 toocopy hello 키 toohello 클립보드로 복사를 클릭 합니다.

## <a name="create-a-container"></a>컨테이너 만들기
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

hello **Azure::Blob::BlobService** 개체 컨테이너 및 blob를 사용할 수 있습니다. toocreate 컨테이너를 사용 하 여 hello **만들\_container()** 메서드.

hello 다음 코드 예제에서는 컨테이너 만들거나 되어 hello 오류를 인쇄 합니다.

```ruby
azure_blob_service = Azure::Blob::BlobService.new
begin
    container = azure_blob_service.create_container("test-container")
rescue
    puts $!
end
```

Hello 컨테이너에서 hello 파일 toomake를 지정 하려면 공용 hello 컨테이너의 사용 권한을 설정할 수 있습니다.

Hello만 수정할 수 있습니다 <strong>만들\_container()</strong> 호출 toopass hello **: 공용\_액세스\_수준** 옵션:

```ruby
container = azure_blob_service.create_container("test-container",
    :public_access_level => "<public access level>")
```

Hello에 대 한 유효한 값 **: 공용\_액세스\_수준** 옵션:

* **blob:** BLOB에 대한 공용 읽기 권한을 지정합니다. 이 컨테이너 내의 Blob 데이터는 익명 요청을 통해 읽을 수 있으나 컨테이너 데이터는 읽을 수 없습니다. 클라이언트는 익명 요청을 통해 hello 컨테이너 내 blob를 열거할 수 없습니다.
* **container:** 컨테이너 및 BLOB 데이터에 대한 전체 공용 읽기 액세스 권한을 지정합니다. 클라이언트가 익명 요청을 통해 hello 컨테이너 내 blob를 열거할 수 있지만 hello 저장소 계정 내 컨테이너는 열거할 수 없습니다.

컨테이너의 공용 액세스 수준을 hello를 사용 하 여 수정할 수 있습니다 또는 **설정\_컨테이너\_acl()** 메서드 toospecify hello 공용 액세스 수준을 합니다.

다음 코드 예제에서는 변경 내용을 hello 공용 액세스 수준을 너무 hello**컨테이너**:

```ruby
azure_blob_service.set_container_acl('test-container', "container")
```

## <a name="upload-a-blob-into-a-container"></a>컨테이너에 Blob 업로드
tooupload 콘텐츠 tooa blob을 사용 하 여 hello **만들\_블록\_blob()** 메서드 toocreate hello blob 파일을 사용 또는 hello blob의 콘텐츠를 hello로 문자열입니다.

hello 다음 코드 파일을 업로드 hello **test.png** 라는 "이미지 blob" hello 컨테이너에서 새 blob으로 합니다.

```ruby
content = File.open("test.png", "rb") { |file| file.read }
blob = azure_blob_service.create_block_blob(container.name,
    "image-blob", content)
puts blob.name
```

## <a name="list-hello-blobs-in-a-container"></a>컨테이너에서 hello blob 나열
toolist hello 컨테이너를 사용 하 여 **list_containers()** 메서드.
toolist hello blob는 컨테이너 내에서 사용 하 여 **목록\_blobs()** 메서드.

모든 hello blob hello 계정에 대 한 모든 hello 컨테이너에서 hello url를 출력합니다.

```ruby
containers = azure_blob_service.list_containers()
containers.each do |container|
    blobs = azure_blob_service.list_blobs(container.name)
    blobs.each do |blob|
    puts blob.name
    end
end
```

## <a name="download-blobs"></a>Blob 다운로드
toodownload blob을 사용 하 여 hello **가져오기\_blob()** 메서드 tooretrieve hello 내용입니다.

hello 다음 코드 예제에서는 사용 하 여 **가져오기\_blob()** toodownload "이미지 blob"의 내용을 hello 및 tooa 로컬 파일을 작성 합니다.

```ruby
blob, content = azure_blob_service.get_blob(container.name,"image-blob")
File.open("download.png","wb") {|f| f.write(content)}
```

## <a name="delete-a-blob"></a>Blob 삭제
Blob를 toodelete hello를 사용 하는 마지막으로, **삭제\_blob()** 메서드. hello 다음 코드 예제에서는 어떻게 toodelete blob입니다.

```ruby
azure_blob_service.delete_blob(container.name, "image-blob")
```

## <a name="next-steps"></a>다음 단계
더 복잡 한 저장소 작업에 대 한 toolearn 다음 링크:

* [Azure 저장소 팀 블로그](http://blogs.msdn.com/b/windowsazurestorage/)
* [Azure SDK for Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) (영문) 리포지토리
* [Hello AzCopy 명령줄 유틸리티를 사용 하 여 데이터를 전송 합니다.](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)


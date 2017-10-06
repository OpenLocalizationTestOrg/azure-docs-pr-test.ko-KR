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
ms.openlocfilehash: 0d7e7436a109ef54fc07cc238c03cfc7cf2caac0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-c"></a>어떻게 toouse c + +에서 Blob 저장소
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>개요
Azure Blob 저장소는 hello 클라우드에서 개체/blob으로 구조화 되지 않은 데이터를 저장 하는 서비스입니다. Blob storage는 문서, 미디어 파일 또는 응용 프로그램 설치 프로그램과 같은 모든 종류의 텍스트 또는 이진 데이터를 저장할 수 있습니다. Blob 저장소 참조 tooas 개체 저장소 이기도합니다.

이 가이드에서는 tooperform 일반적인 시나리오를 사용 하 여 Azure Blob 저장소 서비스를 hello 하는 방법을 보여 줍니다. hello 예제 c + +에서 작성 되 고 hello를 사용 하 여 [c + +에 대 한 Azure 저장소 클라이언트 라이브러리](http://github.com/Azure/azure-storage-cpp/blob/master/README.md)합니다. hello 가이드에서 다루는 시나리오 포함 **업로드**, **나열**, **다운로드**, 및 **삭제** blob입니다.  

> [!NOTE]
> 이 가이드의 대상으로 c + + 버전 1.0.0 이상용 Azure 저장소 클라이언트 라이브러리를 hello 합니다. hello 권장 버전을 통해 사용할 수 있는 저장소 클라이언트 라이브러리, 2.2.0 [NuGet](http://www.nuget.org/packages/wastorage) 또는 [GitHub](https://github.com/Azure/azure-storage-cpp)합니다.
> 
> 

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a>C++ 응용 프로그램 만들기
이 가이드에서는 C++ 응용 프로그램 내에서 실행할 수 있는 저장소 기능을 사용합니다.  

toodo tooinstall, 나오는 c + +에 대 한 Azure 저장소 클라이언트 라이브러리를 hello 및 Azure 구독에 Azure 저장소 계정을 만듭니다.   

Azure 저장소 클라이언트 라이브러리 tooinstall hello c + +에 대 한 hello 다음 메서드를 사용할 수 있습니다.

* **Linux:** hello에 제공 된 hello 지침에 따라 [c + + 추가 정보에 대 한 Azure 저장소 클라이언트 라이브러리](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) 페이지.  
* **Windows:** Visual Studio에서 **도구 > NuGet 패키지 관리자 > 패키지 관리자 콘솔**을 클릭합니다. Hello에 형식 hello 다음 명령은 [NuGet 패키지 관리자 콘솔](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) 누릅니다 **ENTER**합니다.  
  
     Install-Package wastorage

## <a name="configure-your-application-tooaccess-blob-storage"></a>사용자 응용 프로그램 tooaccess Blob 저장소 구성
Hello 다음 포함 toouse hello Azure 저장소 Api tooaccess blob 저장할 hello c + + 파일의 문 toohello 맨 위에 추가 합니다.  

```cpp
#include <was/storage_account.h>
#include <was/blob.h>
```

## <a name="setup-an-azure-storage-connection-string"></a>Azure 저장소 연결 문자열 설정
Azure 저장소 클라이언트는 저장소 연결 문자열 toostore 끝점을 사용 하 여 및 데이터 관리 서비스에 액세스 하기 위한 자격 증명입니다. 형식에 따라, hello에 나열 된 hello 저장소 계정에 대 한 저장소 계정 및 hello 저장소 액세스 키의 hello 이름을 사용 하 여 hello hello 저장소 연결 문자열을 제공 해야, 클라이언트 응용 프로그램에서 실행할 때는 [Azure 포털](https://portal.azure.com)hello에 대 한 *AccountName* 및 *AccountKey* 값입니다. 저장소 계정 및 액세스 키에 대한 자세한 내용은 [Azure 저장소 계정 정보](storage-create-storage-account.md)를 참조하세요. 이 예에서는 정적 필드 toohold hello 연결 문자열을 선언할 수는 방법을 보여 줍니다.  

```cpp
// Define hello connection-string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

tootest 응용 프로그램 사용자의 로컬 Windows 컴퓨터에서 Microsoft Azure hello를 사용할 수 있습니다 [저장소 에뮬레이터](storage-use-emulator.md) hello로 설치 된 [Azure SDK](https://azure.microsoft.com/downloads/)합니다. hello 저장소 에뮬레이터는 로컬 개발 컴퓨터에 Azure에서 제공 하는 hello Blob, 큐 및 테이블 서비스를 시뮬레이션 하는 유틸리티입니다. hello 다음 예제는 어떻게는 정적 필드 toohold hello 연결 문자열 tooyour 로컬 저장소 에뮬레이터를 선언할 수 있습니다.

```cpp
// Define hello connection-string with Azure Storage Emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

toostart hello Azure 저장소 에뮬레이터를 선택 하는 hello **시작** 단추를 클릭 하거나 눌러 hello **Windows** 키입니다. 입력을 시작 **Azure 저장소 에뮬레이터**를 선택 하 고 **Microsoft Azure 저장소 에뮬레이터** hello 응용 프로그램 목록에서 합니다.  

hello 다음과 같은 샘플 가정 이러한 두 가지 방법 tooget hello 저장소 연결 문자열 중 하나 사용 하 합니다.  

## <a name="retrieve-your-connection-string"></a>연결 문자열 검색
Hello를 사용할 수 있습니다 **cloud_storage_account** 클래스 toorepresent 저장소 계정 정보. tooretrieve 저장소 계정 hello 저장소 연결 문자열 정보, hello를 사용할 수 있습니다 **구문 분석** 메서드.  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

다음으로, 참조 tooa 가져올 **cloud_blob_client** 컨테이너 및 Blob 저장소 서비스 hello 내에 저장 된 blob을 나타내는 개체를 tooretrieve 수 있으므로 클래스. hello 다음 코드에서는 **cloud_blob_client** 위에 검색에서는 hello 저장소 계정 개체를 사용 하 여 개체:  

```cpp
// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();  
```

## <a name="how-to-create-a-container"></a>방법: 컨테이너 만들기
[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

이 예에서는 어떻게 toocreate 아직 없는 경우 컨테이너:  

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

기본적으로 hello 새 컨테이너는 전용 포트 이며이 컨테이너에서 저장소 액세스 키 toodownload blob를 지정 해야 합니다. Hello 컨테이너 사용 가능한 tooeveryone 내 toomake hello 파일 (blob)을 사용할 경우 hello 컨테이너 toobe 공용 코드 다음 hello를 사용 하 여 설정할 수 있습니다.  

```cpp
// Make hello blob container publicly accessible.
azure::storage::blob_container_permissions permissions;
permissions.set_public_access(azure::storage::blob_container_public_access_type::blob);
container.upload_permissions(permissions);  
```

Hello 인터넷에서 누구나 공용 컨테이너의 blob를 볼 수 있지만 수정 하거나 hello 적절 한 액세스 키가 있는 경우에 삭제할 수 있습니다.  

## <a name="how-to-upload-a-blob-into-a-container"></a>방법: 컨테이너에 Blob 업로드
Azure Blob Storage는 블록 Blob 및 페이지 Blob을 지원합니다. Hello 대부분의 경우에서 블록 blob는 형식 toouse 권장 hello를 사용 합니다.  

tooupload 파일 tooa 블록 blob 컨테이너 참조를 가져오고 tooget 블록 blob 참조를 사용 합니다. Hello를 호출 하 여 모든 스트림 데이터 tooit의 blob 참조를 만든 후 업로드할 수 있습니다 **upload_from_stream** 메서드. 이전에 존재 하거나 파일이 있으면 덮어씁니다 하지 않은 경우이 작업은 hello blob을 만듭니다. hello 방법을 예제와 다음 tooupload blob 컨테이너에 이미 해당 hello 컨테이너를 만든 가정 합니다.  

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

Hello 또는 사용할 수 있습니다 **upload_from_file** 메서드 tooupload 파일 tooa 블록 blob입니다.

## <a name="how-to-list-hello-blobs-in-a-container"></a>방법: 컨테이너에서 hello blob 나열
먼저 toolist hello에서에서 컨테이너의 blob를 컨테이너 참조를 가져옵니다. Hello 컨테이너를 사용 하 여 있습니다 **list_blobs** tooretrieve hello blob 메서드 및/또는 디렉터리에 있습니다. tooaccess 다양 한 속성 및 메서드는 반환 된 작업에 대 한 hello **list_blob_item**, hello를 호출 해야 **list_blob_item.as_blob** 메서드 tooget는 **cloud_blob** 개체 또는 hello **list_blob.as_directory** 메서드 tooget cloud_blob_directory 개체입니다. hello 다음 코드에서는 방법을 tooretrieve 및 출력 hello hello의 각 항목의 URI **샘플 컨테이너 내** 컨테이너:

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

작업 나열에 대한 자세한 내용은 [C++에서 Azure 저장소 리소스 나열](storage-c-plus-plus-enumeration.md)을 참조하세요.

## <a name="how-to-download-blobs"></a>방법: Blob 다운로드
toodownload blob을 먼저 blob 참조를 검색 하 고 hello 호출 **download_to_stream** 메서드. hello 다음 예제에서는 hello **download_to_stream** 메서드 tootransfer hello blob 내용 tooa stream 개체 다음 tooa 로컬 파일 유지할 수 있습니다.  

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

Hello 또는 사용할 수 있습니다 **download_to_file** blob tooa 파일 내용의 toodownload hello 메서드.
또한 사용할 수도 있습니다 hello **download_text** 텍스트 문자열로 blob 내용의 toodownload hello 메서드.  

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

## <a name="how-to-delete-blobs"></a>방법: Blob 삭제
toodelete blob blob 참조를 먼저 가져온 고 hello 호출 **delete_blob** 메서드를 합니다.  

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

## <a name="next-steps"></a>다음 단계
Blob 저장소의 기본 사항 hello를 알아보았습니다 했으므로 이러한 링크 toolearn Azure 저장소에 대 한 자세한를 수행 합니다.  

* [어떻게 toouse c + +에서 큐 저장소](storage-c-plus-plus-how-to-use-queues.md)
* [어떻게 toouse c + +에서 테이블 저장소](storage-c-plus-plus-how-to-use-tables.md)
* [C++에서 Azure 저장소 리소스 나열](storage-c-plus-plus-enumeration.md)
* [C++용 Storage Client Library 참조(영문)](http://azure.github.io/azure-storage-cpp)
* [Azure Storage 설명서](https://azure.microsoft.com/documentation/services/storage/)
* [Hello AzCopy 명령줄 유틸리티를 사용 하 여 데이터를 전송 합니다.](storage-use-azcopy.md)


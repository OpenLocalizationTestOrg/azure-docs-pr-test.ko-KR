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
# <a name="develop-for-azure-file-storage-with-c"></a>C++를 사용하여 Azure File Storage 개발
[!INCLUDE [storage-selector-file-include](../../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-try-azure-tools-files](../../../includes/storage-try-azure-tools-files.md)]

## <a name="about-this-tutorial"></a>이 자습서 정보

이 자습서에서는 알아봅니다 어떻게 tooperform Azure 파일 저장소에 대 한 기본 작업입니다. 통해 c + +로 작성 된 샘플을 알아봅니다 toocreate 공유 하는 방법 및 디렉터리, 업로드, 목록 및 파일을 삭제 합니다. 새 tooAzure 파일 저장소 인 경우에 다음 hello 섹션에 대 한 hello 개념을 진행 하 고 hello 샘플 이해 유용할 수 있습니다.


* Azure 파일 공유 만들기 및 삭제
* 디렉터리 만들기 및 삭제
* Azure 파일 공유의 파일 및 디렉터리 열거
* 파일 업로드, 다운로드 및 삭제
* Azure 파일 공유에 대 한 hello 할당량 (최대 크기)를 설정 합니다.
* Hello 공유에 정의 된 공유 액세스 정책을 사용 하는 파일에 대 한 공유 액세스 서명 (SAS 키)를 만듭니다.

> [!Note]  
> SMB를 통한 Azure 파일 저장소에 액세스할 수 있습니다, 되므로 hello 표준 c + + I/O 클래스 및 함수를 사용 하 여 hello Azure 파일 공유에 액세스 가능한 toowrite 간단한 응용 프로그램. 이 문서를 사용 하는 toowrite 응용 프로그램 hello를 사용 하 여 Azure 저장소 c + + SDK hello 하는 방법을 설명 합니다 [Azure 파일 저장소 REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure 파일 저장소.

## <a name="create-a-c-application"></a>C++ 응용 프로그램 만들기
toobuild hello 샘플 tooinstall hello Azure 저장소 클라이언트 라이브러리 2.4.0 c + +에 대 한 필요 합니다. Azure 저장소 계정도 만들었어야 합니다.

Azure 저장소 클라이언트 2.4.0 tooinstall hello c + +에 대 한 메서드를 다음 hello 중 사용할 수 있습니다.

* **Linux:** hello에 제공 된 hello 지침에 따라 [c + + 추가 정보에 대 한 Azure 저장소 클라이언트 라이브러리](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) 페이지.
* **Windows:** Visual Studio에서 **도구 &gt; NuGet 패키지 관리자 &gt; 패키지 관리자 콘솔**을 클릭합니다. Hello에 형식 hello 다음 명령은 [NuGet 패키지 관리자 콘솔](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) 누릅니다 **ENTER**합니다.
  
```
Install-Package wastorage
```

## <a name="set-up-your-application-toouse-azure-file-storage"></a>사용자 응용 프로그램 toouse Azure 파일 저장소 설정
Hello 다음 포함 toomanipulate Azure 파일 저장소를 원하는 hello c + + 소스 파일의 문 toohello 맨 위에 추가 합니다.

```cpp
#include <was/storage_account.h>
#include <was/file.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a>Azure 저장소 연결 문자열 설정
파일 저장소 toouse tooconnect tooyour Azure 저장소 계정이 필요 합니다. hello 첫 번째 단계는 것,에서는 연결 문자열을 tooconfigure tooconnect tooyour 저장소 계정입니다. 정적 변수 toodo 정의입니다.

```cpp
// Define hello connection-string with your values.
const utility::string_t 
storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

## <a name="connecting-tooan-azure-storage-account"></a>Tooan Azure 저장소 계정 연결
Hello를 사용할 수 있습니다 **cloud_storage_account** 클래스 toorepresent 저장소 계정 정보. tooretrieve 저장소 계정 hello 저장소 연결 문자열 정보, hello를 사용할 수 있습니다 **구문 분석** 메서드.

```cpp
// Retrieve storage account from connection string.    
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);
```

## <a name="create-an-azure-file-share"></a>Azure 파일 공유 만들기
Azure File Storage의 모든 파일 및 디렉터리는 **공유**라는 이름의 컨테이너 안에 있습니다. 저장소 계정은 계정 용량이 허용하는 만큼의 공유를 가질 수 있습니다. tooobtain 액세스 tooa 공유 및 그 내용을 toouse Azure 파일 저장소 클라이언트 해야합니다.

```cpp
// Create hello Azure File storage client.
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();
```

Hello Azure 파일 저장소 클라이언트를 사용 하는 참조 tooa 공유를 얻을 수 있습니다.

```cpp
// Get a reference toohello file share
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));
```

toocreate hello 공유를 사용 하 여 hello **create_if_not_exists** hello 방식의 **cloud_file_share** 개체입니다.

```cpp
if (share.create_if_not_exists()) {    
    std::wcout << U("New share created") << std::endl;    
}
```

이 시점에서 **공유** 참조 tooa 공유 이름의 보유 **샘플 공유 내**합니다.

## <a name="delete-an-azure-file-share"></a>Azure 파일 공유 삭제
호출 hello 이루어진다는 공유 삭제 **delete_if_exists** cloud_file_share 개체에서 메서드. 다음이 샘플 코드입니다.

```cpp
// Get a reference toohello share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

// delete hello share if exists
share.delete_share_if_exists();
```

## <a name="create-a-directory"></a>디렉터리 만들기
대신 모든 hello 루트 디렉터리에 하위 디렉터리 내의 파일을 배치 하 여 저장소를 구성할 수 있습니다. Azure 파일 저장소에서는 허용 하는 사용자 계정에는으로 여러 디렉터리 만큼 toocreate를 허용 합니다. 아래 hello 코드 라는 디렉터리를 만듭니다. **샘플 디렉터리 내** hello 루트 디렉터리 뿐 아니라 라는 하위 디렉터리에서 **내 하위 샘플**합니다.

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

## <a name="delete-a-directory"></a>디렉터리 삭제
디렉터리의 삭제는 간단한 작업입니다. 단, 여전히 파일 또는 기타 디렉터리가 포함된 디렉터리는 삭제할 수 없습니다.

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

## <a name="enumerate-files-and-directories-in-an-azure-file-share"></a>Azure 파일 공유의 파일 및 디렉터리 열거
공유 내에서 파일 및 디렉터리 목록을 가져오는 것은 **cloud_file_directory** 참조에서 **list_files_and_directories**를 호출하여 쉽게 수행할 수 있습니다. tooaccess 다양 한 속성 및 메서드는 반환 된 작업에 대 한 hello **list_file_and_directory_item**, hello를 호출 해야 **list_file_and_directory_item.as_file** 메서드 tooget는 **cloud_ 파일** 개체나 hello **list_file_and_directory_item.as_directory** 메서드 tooget는 **cloud_file_directory** 개체입니다.

코드 다음 hello tooretrieve 및 출력 hello 공유의 hello 루트 디렉터리의 각 항목의 URI hello 방법을 보여 줍니다.

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

## <a name="upload-a-file"></a>파일 업로드
최소한, 매우 hello에서 Azure 파일 공유가 파일이 수 있는 루트 디렉터리를 포함 합니다. 이 섹션에서는 tooupload hello에 대 한 로컬 저장소에서 파일 루트 디렉터리를 공유 하는 방법을 설명 합니다.

파일 업로드 hello 첫 번째 단계에는 tooobtain 상주해 야 참조 toohello 디렉터리입니다. 이렇게 하려면 호출 hello **get_root_directory_reference** hello 공유 개체의 메서드.

```cpp
//Get a reference toohello root directory for hello share.
azure::storage::cloud_file_directory root_dir = share.get_root_directory_reference();
```

Hello 공유의 참조 toohello 루트 디렉터리를가지고 놓아서 파일을 업로드할 수 있습니다. 이 예제에서는 파일, 텍스트 및 스트림에서 업로드합니다.

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

## <a name="download-a-file"></a>파일 다운로드
toodownload 파일 파일 참조를 먼저 검색 하 고 hello 호출 **download_to_stream** 메서드 tootransfer hello 파일 내용 tooa 스트림 개체를 지속할 수 있습니다 tooa 로컬 파일입니다. Hello 또는 사용할 수 있습니다 **download_to_file** 파일 tooa 로컬 파일 내용의 toodownload hello 메서드. Hello를 사용할 수 있습니다 **download_text** 텍스트 문자열로 파일 내용의 toodownload hello 메서드.

hello 다음 예제에서는 hello **download_to_stream** 및 **download_text** 메서드 toodemonstrate 이전 섹션에서 만든 hello 파일을 다운로드 합니다.

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

## <a name="delete-a-file"></a>파일 삭제
다른 일반적인 Azure File Storage 작업은 파일의 삭제입니다. hello 다음 코드를 삭제 내-샘플-파일-3 hello 루트 디렉터리 아래에 저장 된 이라는 파일로 내보내집니다.

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

## <a name="set-hello-quota-maximum-size-for-an-azure-file-share"></a>Azure 파일 공유에 대 한 hello 할당량 (최대 크기)를 설정 합니다.
(기가바이트)에서 파일 공유에 대 한 hello 할당량 (또는 최대 크기)을 설정할 수 있습니다. 데이터의 양을 현재 hello 공유에 저장 된 toosee를 확인할 수 있습니다.

공유에 대 한 hello 할당량을 설정 하 여 hello hello 공유에 저장 된 hello 파일의 전체 크기를 제한할 수 있습니다. Hello hello 공유에 있는 파일의 전체 크기를 초과 하는 경우 hello 공유에 hello 할당량을 설정한 후 클라이언트는 수 없습니다 tooincrease hello 크기의 기존 파일 또는 이러한 파일은 비어 경우가 아니면 새 파일을 만듭니다.

다음 예제에서는 hello 방법을 toocheck hello 공유에 대 한 현재 사용량 및 tooset hello 공유에 대 한 할당량을 hello 하는 방법을 보여 줍니다.

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

## <a name="generate-a-shared-access-signature-for-a-file-or-file-share"></a>파일 또는 파일 공유에 대한 공유 액세스 서명 생성
파일 공유 또는 개별 파일에 대한 SAS(공유 액세스 서명)를 생성할 수 있습니다. 서명 파일 공유 toomanage 공유 액세스에 공유 액세스 정책을도 만들 수 있습니다. 공유 액세스 정책 만들기 좋습니다 해야 손상 되 면 hello SAS를 해지 하는 수단을 제공 합니다.

다음 예제는 hello 공유에 공유 액세스 정책을 만들고 정책 tooprovide hello 제약 조건을 SAS에 대 한 hello에서 파일 공유를 사용 하 여 합니다.

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
## <a name="next-steps"></a>다음 단계
Azure 저장소에 대해 자세히 toolearn이 리소스를 살펴봅니다.

* [Storage Client Library for C++](https://github.com/Azure/azure-storage-cpp)
* [C++로 작성된 Azure Storage File 서비스 샘플] (https://github.com/Azure-Samples/storage-file-cpp-getting-started)
* [Azure 저장소 탐색기](http://go.microsoft.com/fwlink/?LinkID=822673&clcid=0x409)
* [Azure 저장소 설명서](https://azure.microsoft.com/documentation/services/storage/)
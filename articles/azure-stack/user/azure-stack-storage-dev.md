---
title: "Azure 스택 저장소 개발 도구 시작"
description: "Azure 스택 저장소 개발 도구를 사용 하 여 시작에 대 한 지침"
services: azure-stack
author: xiaofmao
ms.author: xiaofmao
ms.date: 9/25/2017
ms.topic: get-started-article
ms.service: azure-stack
ms.openlocfilehash: 5b2898c64c0f1b5d804e63fa4e4e1218fa7a672c
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/11/2017
---
# <a name="get-started-with-azure-stack-storage-development-tools"></a>Azure 스택 저장소 개발 도구 시작

*적용 대상: Azure 스택 통합 시스템과 Azure 스택 개발 키트*


Microsoft Azure 스택 Azure Blob, 테이블 및 큐 저장소를 포함 하 여 저장소 서비스의 집합을 제공 합니다.

이 문서는 Azure 스택 저장소 개발 도구를 사용 하 여 시작 하는 방법에 빠른 지침을 제공 합니다. 해당 하는 Azure 저장소 자습서에 보다 자세한 정보 및 예제 코드를 찾을 수 있습니다.

Azure 저장소와 각 플랫폼에 대 한 몇 가지 특정 요구 사항을 포함 하 여 Azure 스택 저장소와 차이점 알려져 있습니다. 예를 들어 특정 클라이언트 라이브러리 및 Azure 스택에 대 한 특정 끝점 접미사 요구 됩니다. 자세한 내용은 참조 [Azure 스택 저장소: 차이점과 고려 사항을](azure-stack-acs-differences.md)합니다.

## <a name="azure-client-libraries"></a>Azure 클라이언트 라이브러리
Azure 스택 저장소에 대 한 지원 되는 REST API 버전 2015-04-05입니다. 최신 버전의 Azure 저장소 REST API와 함께 전체 패리티가 되어 있지 않습니다. 따라서 저장소 클라이언트 라이브러리에 대 한 필요한 REST API 2015-04-05와 호환 되는 버전을 알고 있어야 합니다.


|클라이언트 라이브러리|Azure 스택 지원 되는 버전|링크|끝점 지정|
|---------|---------|---------|---------|
|.NET     |6.2.0|Nuget 패키지:<br>[https://www.nuget.org/packages/WindowsAzure.Storage/6.2.0](https://www.nuget.org/packages/WindowsAzure.Storage/6.2.0)<br><br>GitHub 릴리스:<br>[https://github.com/Azure/azure-storage-net/releases/tag/v6.2.1](https://github.com/Azure/azure-storage-net/releases/tag/v6.2.1)|app.config 파일|
|Java|4.1.0|Maven 패키지:<br>[http://mvnrepository.com/artifact/com.microsoft.azure/azure-storage/4.1.0](http://mvnrepository.com/artifact/com.microsoft.azure/azure-storage/4.1.0)<br><br>GitHub 릴리스:<br> [https://github.com/Azure/azure-storage-java/releases/tag/v4.1.0](https://github.com/Azure/azure-storage-java/releases/tag/v4.1.0)|연결 문자열 설정|
|Node.js     |1.1.0|NPM 링크:<br>[https://www.npmjs.com/package/azure-storage](https://www.npmjs.com/package/azure-storage)<br>(실행:`npm install azure-storage@1.1.0)`<br><br>Github 릴리스:<br>[https://github.com/Azure/azure-storage-node/releases/tag/1.1.0](https://github.com/Azure/azure-storage-node/releases/tag/1.1.0)|서비스 인스턴스 선언||C++|2.4.0|Nuget 패키지:<br>[https://www.nuget.org/packages/wastorage.v140/2.4.0](https://www.nuget.org/packages/wastorage.v140/2.4.0)<br><br>GitHub 릴리스:<br>[https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0](https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0)|연결 문자열 설정|
|C++|2.4.0|Nuget 패키지:<br>[https://www.nuget.org/packages/wastorage.v140/2.4.0](https://www.nuget.org/packages/wastorage.v140/2.4.0)<br><br>GitHub 릴리스:<br>[https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0](https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0)|연결 문자열 설정|
|PHP|0.15.0|GitHub 릴리스:<br>[https://github.com/Azure/azure-storage-php/releases/tag/v0.15.0](https://github.com/Azure/azure-storage-php/releases/tag/v0.15.0)<br><br>작성기를 통해 설치 (아래 세부 정보 참조)|연결 문자열 설정|
|Python     |0.30.0|PIP 패키지:<br> [https://pypi.python.org/pypi/azure-storage/0.30.0](https://pypi.python.org/pypi/azure-storage/0.30.0)<br>(실행:`pip install -v azure-storage==0.30.0)`<br><br>GitHub 릴리스:<br> [https://github.com/Azure/azure-storage-python/releases/tag/v0.30.0](https://github.com/Azure/azure-storage-python/releases/tag/v0.30.0)|서비스 인스턴스 선언|
|루비|0.12.1<br>미리 보기|RubyGems 패키지:<br> [https://rubygems.org/gems/azure-storage/versions/0.12.1.preview](https://rubygems.org/gems/azure-storage/versions/0.12.1.preview)<br><br>GitHub 릴리스:<br> [https://github.com/Azure/azure-storage-ruby/releases/tag/v0.12.1](https://github.com/Azure/azure-storage-ruby/releases/tag/v0.12.1)|연결 문자열 설정|

> [!NOTE]
> PHP 세부 정보<br><br>
>작성기를 통해 설치 하는 방법
>1. 라는 파일을 만들어 `composer.json` 다음 코드를 사용 하 여 프로젝트의 루트에서:<br>
>
>   ```
>   {
>       "require":{
>           "Microsoft/azure-storage":"0.15.0"
>        }
>    }
>   ```
>
>2. 다운로드 [composer.phar](http://getcomposer.org/composer.phar) 프로젝트 루트에 있습니다.
>3. `php composer.phar install`을 실행합니다.
>


## <a name="endpoint-declaration"></a>끝점 선언
두 요소를 포함 하는 Azure 스택 끝점: 영역 및 Azure 스택 도메인 이름입니다.
Azure 스택 개발 키트에 기본 끝점은 **local.azurestack.external**합니다.
확실 하지 않은 끝점에 대 한 경우 클라우드 관리자에 게 문의 합니다.

## <a name="examples"></a>예


### <a name="net"></a>.NET

Azure 스택에 대 한 끝점 접미사는 app.config 파일에 지정 됩니다.

```
<add key="StorageConnectionString" 
value="DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey;
EndpointSuffix=local.azurestack.external;" />
```
### <a name="java"></a>Java

Azure 스택에 대 한 끝점 접미사는 설치 하는 연결 문자열에에서 지정 됩니다.

```
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key;" +
    "EndpointSuffix=local.azurestack.external";
```

### <a name="nodejs"></a>Node.js

Azure 스택에 대 한 끝점 접미사 선언 인스턴스에 지정 됩니다.

```
var blobSvc = azure.createBlobService('myaccount', 'mykey',
'myaccount.blob.local.azurestack.external');
```
### <a name="c"></a>C++

Azure 스택에 대 한 끝점 접미사는 설치 하는 연결 문자열에에서 지정 됩니다.

```
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;
AccountName=your_storage_account;
AccountKey=your_storage_account_key;
EndpointSuffix=local.azurestack.external"));
```

### <a name="php"></a>PHP

Azure 스택에 대 한 끝점 접미사는 설치 하는 연결 문자열에에서 지정 됩니다.

```
$connectionString = 'BlobEndpoint=http://<storage account name>.blob.local.azurestack.external/;
QueueEndpoint=http:// <storage account name>.queue.local.azurestack.external/;
TableEndpoint=http:// <storage account name>.table.local.azurestack.external/;
AccountName=<storage account name>;AccountKey=<storage account key>'
```

### <a name="python"></a>Python

Azure 스택에 대 한 끝점 접미사 선언 인스턴스에 지정 됩니다.

```
block_blob_service = BlockBlobService(account_name='myaccount',
account_key='mykey',
endpoint_suffix='local.azurestack.external')
```
### <a name="ruby"></a>루비

Azure 스택에 대 한 끝점 접미사는 설치 하는 연결 문자열에에서 지정 됩니다.

```
set
AZURE_STORAGE_CONNECTION_STRING=DefaultEndpointsProtocol=https;
AccountName=myaccount;
AccountKey=mykey;
EndpointSuffix=local.azurestack.external
```

## <a name="blob-storage"></a>Blob 저장소

다음 Azure Blob 저장소 자습서에서는 Azure 스택에 적용 됩니다. 이전에 설명 된 Azure 스택에 대 한 특정 끝점 접미사 요구 사항에 유의 [예제](#examples) 섹션.

* [.NET을 사용하여 Azure Blob 저장소 시작](../../storage/blobs/storage-dotnet-how-to-use-blobs.md)
* [Java에서 Blob 저장소를 사용하는 방법](../../storage/blobs/storage-java-how-to-use-blob-storage.md)
* [Node.js에서 Blob 저장소를 사용 하는 방법을]... /.. / storage/blobs/storage-nodejs-how-to-use-blob-storage.md)
* [C++에서 Blob 저장소를 사용하는 방법](../../storage/blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [PHP에서 Blob 저장소를 사용하는 방법](../../storage/blobs/storage-php-how-to-use-blobs.md)
* [Python에서 Azure Blob 저장소를 사용 하는 방법](../../storage/blobs/storage-python-how-to-use-blob-storage.md)
* [Ruby에서 Blob 저장소를 사용하는 방법](../../storage/blobs/storage-ruby-how-to-use-blob-storage.md)

## <a name="queue-storage"></a>큐 저장소

다음 Azure 큐 저장소 자습서에서는 Azure 스택에 적용 됩니다. 이전에 설명 된 Azure 스택에 대 한 특정 끝점 접미사 요구 사항에 유의 [예제](#examples) 섹션.

* [.NET을 사용하여 Azure 큐 저장소 시작](../../storage/queues/storage-dotnet-how-to-use-queues.md)
* [Java에서 큐 저장소를 사용하는 방법](../../storage/queues/storage-java-how-to-use-queue-storage.md)
* [Node.js에서 큐 저장소를 사용하는 방법](../../storage/queues/storage-nodejs-how-to-use-queues.md)
* [C++에서 큐 저장소를 사용하는 방법](../../storage/queues/storage-c-plus-plus-how-to-use-queues.md)
* [PHP에서 큐 저장소를 사용하는 방법](../../storage/queues/storage-php-how-to-use-queues.md)
* [Python에서 큐 저장소를 사용하는 방법](../../storage/queues/storage-python-how-to-use-queue-storage.md)
* [Ruby에서 큐 저장소를 사용하는 방법](../../storage/queues/storage-ruby-how-to-use-queue-storage.md)


## <a name="table-storage"></a>테이블 저장소

다음 Azure 테이블 저장소 자습서에서는 Azure 스택에 적용 됩니다. 이전에 설명 된 Azure 스택에 대 한 특정 끝점 접미사 요구 사항에 유의 [예제](#examples) 섹션.

* [.NET을 사용하여 Azure 테이블 저장소 시작](../../cosmos-db/table-storage-how-to-use-dotnet.md)
* [Java에서 테이블 저장소를 사용하는 방법](../../cosmos-db/table-storage-how-to-use-java.md)
* [Node.js에서 Azure 테이블 저장소를 사용 하는 방법](../../cosmos-db/table-storage-how-to-use-nodejs.md)
* [C + +에서 테이블 저장소를 사용 하는 방법](../../cosmos-db/table-storage-how-to-use-c-plus.md)
* [PHP에서 테이블 저장소를 사용하는 방법](../../cosmos-db/table-storage-how-to-use-php.md)
* [Python에서 테이블 저장소를 사용 하는 방법](../../cosmos-db/table-storage-how-to-use-python.md)
* [Ruby에서 테이블 저장소를 사용하는 방법](../../cosmos-db/table-storage-how-to-use-ruby.md)

## <a name="next-steps"></a>다음 단계

* [Microsoft Azure Storage 소개](../../storage/common/storage-introduction.md)
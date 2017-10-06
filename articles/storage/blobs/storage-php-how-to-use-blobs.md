---
title: "PHP에서 aaaHow toouse blob 저장소 (개체 저장소) | Microsoft Docs"
description: "Azure Blob 저장소 (개체 저장소)를 사용 하는 hello 클라우드에 구조화 되지 않은 데이터를 저장 합니다."
documentationcenter: php
services: storage
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 1af56b59-b3f0-4b46-8441-aab463ae088e
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 2e77415519b38007652e3ea372da531b3a97c5d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-php"></a>Toouse blob 저장소 PHP에서 하는 방법
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>개요
Azure Blob 저장소는 hello 클라우드에서 개체/blob으로 구조화 되지 않은 데이터를 저장 하는 서비스입니다. Blob storage는 문서, 미디어 파일 또는 응용 프로그램 설치 프로그램과 같은 모든 종류의 텍스트 또는 이진 데이터를 저장할 수 있습니다. Blob 저장소 참조 tooas 개체 저장소 이기도합니다.

이 가이드에서는 tooperform 일반적인 시나리오 hello Azure를 사용 하 여 blob 서비스 하는 방법을 알아봅니다. hello PHP로 작성 된 100 개의 샘플과 hello를 사용 하 여 [PHP 용 Azure SDK][download]합니다. hello 가이드에서 다루는 시나리오 포함 **업로드**, **나열**, **다운로드**, 및 **삭제** blob입니다. Blob에 대 한 자세한 내용은 참조 hello [다음 단계](#next-steps) 섹션.

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a>PHP 응용 프로그램 만들기
hello Azure blob 서비스에 액세스 하는 PHP 응용 프로그램을 만들기 위한 요구 사항은 hello만 hello 코드 내에서 hello Azure SDK의에서 클래스 중에서 PHP에 대 한 참조입니다. 모든 개발 도구 toocreate 메모장 등 응용 프로그램을 사용할 수 있습니다.

이 가이드에서는 PHP 응용 프로그램 내에서 로컬로 또는 Azure 웹 역할, 작업자 역할 또는 웹 사이트 내에서 실행되는 코드에서 호출할 수 있는 서비스 기능을 사용합니다.

## <a name="get-hello-azure-client-libraries"></a>Hello Azure 클라이언트 라이브러리 가져오기
[!INCLUDE [get-client-libraries](../../../includes/get-client-libraries.md)]

## <a name="configure-your-application-tooaccess-hello-blob-service"></a>응용 프로그램 tooaccess hello blob 서비스를 구성 합니다.
toouse hello Azure blob 서비스 Api 해야합니다.

1. Hello를 사용 하 여 참조 hello 자동 로더에 파일 [require_once] 문 및
2. 사용할 수 있는 모든 클래스 참조

hello 다음 예제에서는 어떻게 tooinclude hello 자동 로더 파일과 참조 hello **ServicesBuilder** 클래스입니다.

> [!NOTE]
> 이 문서의 hello 예제 hello 작성기를 통해 Azure에 대 한 PHP 클라이언트 라이브러리를 설치한 경우를 가정 합니다. Hello 라이브러리를 수동으로 설치 해야 tooreference hello `WindowsAzure.php` 자동 로더에 파일입니다.
>
>

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

아래의 hello 예제 hello `require_once` 문에 항상 표시 되지만 hello 클래스만 hello 예제 tooexecute에 필요한 참조 됩니다.

## <a name="set-up-an-azure-storage-connection"></a>Azure 저장소 연결 설정
Azure blob 서비스 클라이언트 tooinstantiate 먼저 유효한 연결 문자열을 있어야 합니다. hello hello blob 서비스 연결 문자열 형식은 다음과 같습니다.

Live 서비스에 액세스하는 경우:

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

Hello 저장소 에뮬레이터에 액세스 합니다.

```php
UseDevelopmentStorage=true
```

toocreate 모든 Azure 서비스 클라이언트 toouse hello 해야 **ServicesBuilder** 클래스입니다. 다음을 수행할 수 있습니다.

* Hello 연결을 통과할 tooit 직접 문자열 또는
* 사용 하 여 hello **CloudConfigurationManager (CCM)** toocheck hello 연결 문자열에 대 한 여러 외부 원본:
  * 기본적으로 하나의 외부 소스, 환경 변수에 대한 지원이 제공됩니다.
  * Hello를 확장 하 여 새 원본을 추가할 수 있습니다 **ConnectionStringSource** 클래스입니다.

Hello 여기에 설명 된 예제를 보려면 hello 연결 문자열을 직접 전달 됩니다.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);
```

## <a name="create-a-container"></a>컨테이너 만들기
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

A **BlobRestProxy** 개체를 사용 하면 hello로 blob 컨테이너를 만들 **createContainer** 메서드. 컨테이너를 만들 때에 hello 컨테이너에는 옵션을 설정할 수 있지만, 이렇게 하면 하지 필요 합니다. (tooset hello 컨테이너 제어 목록 (ACL)와 컨테이너 메타 데이터를 액세스 하는 방법을 hello 감시할 보여 줍니다.)

```php
require_once 'vendor\autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Blob\Models\CreateContainerOptions;
use MicrosoftAzure\Storage\Blob\Models\PublicAccessType;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);


// OPTIONAL: Set public access policy and metadata.
// Create container options object.
$createContainerOptions = new CreateContainerOptions();

// Set public access policy. Possible values are
// PublicAccessType::CONTAINER_AND_BLOBS and PublicAccessType::BLOBS_ONLY.
// CONTAINER_AND_BLOBS:
// Specifies full public read access for container and blob data.
// proxys can enumerate blobs within hello container via anonymous
// request, but cannot enumerate containers within hello storage account.
//
// BLOBS_ONLY:
// Specifies public read access for blobs. Blob data within this
// container can be read via anonymous request, but container data is not
// available. proxys cannot enumerate blobs within hello container via
// anonymous request.
// If this value is not specified in hello request, container data is
// private toohello account owner.
$createContainerOptions->setPublicAccess(PublicAccessType::CONTAINER_AND_BLOBS);

// Set container metadata.
$createContainerOptions->addMetaData("key1", "value1");
$createContainerOptions->addMetaData("key2", "value2");

try    {
    // Create container.
    $blobRestProxy->createContainer("mycontainer", $createContainerOptions);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

호출 **setPublicAccess (PublicAccessType::CONTAINER\_AND\_BLOB)** 는 hello 익명 요청을 통해 액세스할 수 있는 컨테이너 및 blob 데이터입니다. **setPublicAccess(PublicAccessType::BLOBS_ONLY)**를 호출하면 익명 요청을 통해 Blob 데이터에만 액세스할 수 있습니다. 컨테이너 ACL에 대한 자세한 내용은 [컨테이너 ACL 설정(REST API)][container-acl]을 참조하세요.

Blob service 오류 코드에 대한 자세한 내용은 [Blob service 오류 코드][error-codes](영문)를 참조하십시오.

## <a name="upload-a-blob-into-a-container"></a>컨테이너에 Blob 업로드
파일을 사용 하 여 hello blob으로 tooupload **BlobRestProxy createBlockBlob->** 메서드. 이 작업은 존재 하지 않으면 되거나 이미 있으면 덮어씁니다 hello blob을 만듭니다. hello 아래 코드 예제에서는 해당 hello 컨테이너 이미 만들어져 고 가정 사용 하 여 [fopen] [ fopen] 스트림으로 tooopen hello 파일입니다.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);


$content = fopen("c:\myfile.txt", "r");
$blob_name = "myblob";

try    {
    //Upload blob
    $blobRestProxy->createBlockBlob("mycontainer", $blob_name, $content);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

이전 샘플 hello를 스트림으로 blob을 업로드 합니다. 하지만 Blob을 사용 하 여 문자열로, 예를 들어 hello 업로드할 수도 있습니다 [파일\_가져오기\_내용을] [ file_get_contents] 함수입니다. toodo이 hello 이전 샘플을 사용 하 여 변경할 `$content = fopen("c:\myfile.txt", "r");` 너무`$content = file_get_contents("c:\myfile.txt");`합니다.

## <a name="list-hello-blobs-in-a-container"></a>컨테이너에서 hello blob 나열
toolist hello blob 컨테이너에서 hello를 사용 하 여 **BlobRestProxy listBlobs->** 메서드는 **foreach** tooloop hello 결과 통해 반복 합니다. hello 다음 코드 컨테이너에서 출력으로 각 blob의 hello 이름을 표시 하 고 해당 URI toohello 브라우저를 표시 합니다.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);


try    {
    // List blobs.
    $blob_list = $blobRestProxy->listBlobs("mycontainer");
    $blobs = $blob_list->getBlobs();

    foreach($blobs as $blob)
    {
        echo $blob->getName().": ".$blob->getUrl()."<br />";
    }
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="download-a-blob"></a>Blob 다운로드
toodownload blob 호출 hello **BlobRestProxy getBlob->** 메서드를 다음 호출 hello **getContentStream** hello 결과에서 메서드가 **GetBlobResult** 개체입니다.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);


try    {
    // Get blob.
    $blob = $blobRestProxy->getBlob("mycontainer", "myblob");
    fpassthru($blob->getContentStream());
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

Note 위의 그 hello 예에서 blob 스트림 리소스 (hello 기본 동작)를 가져옵니다. 그러나 hello를 사용할 수 있습니다 [스트림\_가져오기\_내용을] [ stream-get-contents] 함수 tooconvert hello 스트림 tooa 문자열을 반환 했습니다.

## <a name="delete-a-blob"></a>Blob 삭제
blob를 toodelete hello 컨테이너 이름 및 blob 이름 전달 너무**BlobRestProxy deleteBlob->**합니다.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);


try    {
    // Delete blob.
    $blobRestProxy->deleteBlob("mycontainer", "myblob");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="delete-a-blob-container"></a>Blob 컨테이너 삭제
마지막으로, blob 컨테이너 toodelete hello 컨테이너 이름을 전달 너무**BlobRestProxy deleteContainer->**합니다.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);

try    {
    // Delete container.
    $blobRestProxy->deleteContainer("mycontainer");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="next-steps"></a>다음 단계
Hello Azure blob 서비스의 기본 사항 hello를 알아보았습니다 했으므로 더 복잡 한 저장소 작업에 대 한 이러한 링크 toolearn를 수행 합니다.

* Hello 방문 [Azure 저장소 팀 블로그](http://blogs.msdn.com/b/windowsazurestorage/)
* Hello 참조 [PHP 블록 blob 예제](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/BlockBlobExample.php)합니다.
* Hello 참조 [PHP 페이지 blob 예제](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/PageBlobExample.php)합니다.
* [Hello AzCopy 명령줄 유틸리티를 사용 하 여 데이터를 전송 합니다.](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

자세한 내용은 참고 항목 hello [PHP 개발자 센터](/develop/php/)합니다.

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[container-acl]: http://msdn.microsoft.com/library/azure/dd179391.aspx
[error-codes]: http://msdn.microsoft.com/library/azure/dd179439.aspx
[file_get_contents]: http://php.net/file_get_contents
[require_once]: http://php.net/require_once
[fopen]: http://www.php.net/fopen
[stream-get-contents]: http://www.php.net/stream_get_contents

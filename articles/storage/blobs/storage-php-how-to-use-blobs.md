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
# <a name="how-toouse-blob-storage-from-php"></a><span data-ttu-id="46c51-103">Toouse blob 저장소 PHP에서 하는 방법</span><span class="sxs-lookup"><span data-stu-id="46c51-103">How toouse blob storage from PHP</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="46c51-104">개요</span><span class="sxs-lookup"><span data-stu-id="46c51-104">Overview</span></span>
<span data-ttu-id="46c51-105">Azure Blob 저장소는 hello 클라우드에서 개체/blob으로 구조화 되지 않은 데이터를 저장 하는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="46c51-105">Azure Blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="46c51-106">Blob storage는 문서, 미디어 파일 또는 응용 프로그램 설치 프로그램과 같은 모든 종류의 텍스트 또는 이진 데이터를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46c51-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="46c51-107">Blob 저장소 참조 tooas 개체 저장소 이기도합니다.</span><span class="sxs-lookup"><span data-stu-id="46c51-107">Blob storage is also referred tooas object storage.</span></span>

<span data-ttu-id="46c51-108">이 가이드에서는 tooperform 일반적인 시나리오 hello Azure를 사용 하 여 blob 서비스 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="46c51-108">This guide shows you how tooperform common scenarios using hello Azure blob service.</span></span> <span data-ttu-id="46c51-109">hello PHP로 작성 된 100 개의 샘플과 hello를 사용 하 여 [PHP 용 Azure SDK][download]합니다.</span><span class="sxs-lookup"><span data-stu-id="46c51-109">hello samples are written in PHP and use hello [Azure SDK for PHP][download].</span></span> <span data-ttu-id="46c51-110">hello 가이드에서 다루는 시나리오 포함 **업로드**, **나열**, **다운로드**, 및 **삭제** blob입니다.</span><span class="sxs-lookup"><span data-stu-id="46c51-110">hello scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span> <span data-ttu-id="46c51-111">Blob에 대 한 자세한 내용은 참조 hello [다음 단계](#next-steps) 섹션.</span><span class="sxs-lookup"><span data-stu-id="46c51-111">For more information on blobs, see hello [Next steps](#next-steps) section.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="46c51-112">PHP 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="46c51-112">Create a PHP application</span></span>
<span data-ttu-id="46c51-113">hello Azure blob 서비스에 액세스 하는 PHP 응용 프로그램을 만들기 위한 요구 사항은 hello만 hello 코드 내에서 hello Azure SDK의에서 클래스 중에서 PHP에 대 한 참조입니다.</span><span class="sxs-lookup"><span data-stu-id="46c51-113">hello only requirement for creating a PHP application that accesses hello Azure blob service is hello referencing of classes in hello Azure SDK for PHP from within your code.</span></span> <span data-ttu-id="46c51-114">모든 개발 도구 toocreate 메모장 등 응용 프로그램을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46c51-114">You can use any development tools toocreate your application, including Notepad.</span></span>

<span data-ttu-id="46c51-115">이 가이드에서는 PHP 응용 프로그램 내에서 로컬로 또는 Azure 웹 역할, 작업자 역할 또는 웹 사이트 내에서 실행되는 코드에서 호출할 수 있는 서비스 기능을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="46c51-115">In this guide, you use service features, which can be called within a PHP application locally or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-hello-azure-client-libraries"></a><span data-ttu-id="46c51-116">Hello Azure 클라이언트 라이브러리 가져오기</span><span class="sxs-lookup"><span data-stu-id="46c51-116">Get hello Azure Client Libraries</span></span>
[!INCLUDE [get-client-libraries](../../../includes/get-client-libraries.md)]

## <a name="configure-your-application-tooaccess-hello-blob-service"></a><span data-ttu-id="46c51-117">응용 프로그램 tooaccess hello blob 서비스를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="46c51-117">Configure your application tooaccess hello blob service</span></span>
<span data-ttu-id="46c51-118">toouse hello Azure blob 서비스 Api 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="46c51-118">toouse hello Azure blob service APIs, you need to:</span></span>

1. <span data-ttu-id="46c51-119">Hello를 사용 하 여 참조 hello 자동 로더에 파일 [require_once] 문 및</span><span class="sxs-lookup"><span data-stu-id="46c51-119">Reference hello autoloader file using hello [require_once] statement, and</span></span>
2. <span data-ttu-id="46c51-120">사용할 수 있는 모든 클래스 참조</span><span class="sxs-lookup"><span data-stu-id="46c51-120">Reference any classes you might use.</span></span>

<span data-ttu-id="46c51-121">hello 다음 예제에서는 어떻게 tooinclude hello 자동 로더 파일과 참조 hello **ServicesBuilder** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="46c51-121">hello following example shows how tooinclude hello autoloader file and reference hello **ServicesBuilder** class.</span></span>

> [!NOTE]
> <span data-ttu-id="46c51-122">이 문서의 hello 예제 hello 작성기를 통해 Azure에 대 한 PHP 클라이언트 라이브러리를 설치한 경우를 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="46c51-122">hello examples in this article assume you have installed hello PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="46c51-123">Hello 라이브러리를 수동으로 설치 해야 tooreference hello `WindowsAzure.php` 자동 로더에 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="46c51-123">If you installed hello libraries manually, you need tooreference hello `WindowsAzure.php` autoloader file.</span></span>
>
>

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="46c51-124">아래의 hello 예제 hello `require_once` 문에 항상 표시 되지만 hello 클래스만 hello 예제 tooexecute에 필요한 참조 됩니다.</span><span class="sxs-lookup"><span data-stu-id="46c51-124">In hello examples below, hello `require_once` statement will be shown always, but only hello classes necessary for hello example tooexecute are referenced.</span></span>

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="46c51-125">Azure 저장소 연결 설정</span><span class="sxs-lookup"><span data-stu-id="46c51-125">Set up an Azure storage connection</span></span>
<span data-ttu-id="46c51-126">Azure blob 서비스 클라이언트 tooinstantiate 먼저 유효한 연결 문자열을 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="46c51-126">tooinstantiate an Azure blob service client, you must first have a valid connection string.</span></span> <span data-ttu-id="46c51-127">hello hello blob 서비스 연결 문자열 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="46c51-127">hello format for hello blob service connection string is:</span></span>

<span data-ttu-id="46c51-128">Live 서비스에 액세스하는 경우:</span><span class="sxs-lookup"><span data-stu-id="46c51-128">For accessing a live service:</span></span>

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

<span data-ttu-id="46c51-129">Hello 저장소 에뮬레이터에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="46c51-129">For accessing hello storage emulator:</span></span>

```php
UseDevelopmentStorage=true
```

<span data-ttu-id="46c51-130">toocreate 모든 Azure 서비스 클라이언트 toouse hello 해야 **ServicesBuilder** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="46c51-130">toocreate any Azure service client, you need toouse hello **ServicesBuilder** class.</span></span> <span data-ttu-id="46c51-131">다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46c51-131">You can:</span></span>

* <span data-ttu-id="46c51-132">Hello 연결을 통과할 tooit 직접 문자열 또는</span><span class="sxs-lookup"><span data-stu-id="46c51-132">Pass hello connection string directly tooit or</span></span>
* <span data-ttu-id="46c51-133">사용 하 여 hello **CloudConfigurationManager (CCM)** toocheck hello 연결 문자열에 대 한 여러 외부 원본:</span><span class="sxs-lookup"><span data-stu-id="46c51-133">Use hello **CloudConfigurationManager (CCM)** toocheck multiple external sources for hello connection string:</span></span>
  * <span data-ttu-id="46c51-134">기본적으로 하나의 외부 소스, 환경 변수에 대한 지원이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="46c51-134">By default, it comes with support for one external source - environmental variables.</span></span>
  * <span data-ttu-id="46c51-135">Hello를 확장 하 여 새 원본을 추가할 수 있습니다 **ConnectionStringSource** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="46c51-135">You can add new sources by extending hello **ConnectionStringSource** class.</span></span>

<span data-ttu-id="46c51-136">Hello 여기에 설명 된 예제를 보려면 hello 연결 문자열을 직접 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="46c51-136">For hello examples outlined here, hello connection string will be passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);
```

## <a name="create-a-container"></a><span data-ttu-id="46c51-137">컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="46c51-137">Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="46c51-138">A **BlobRestProxy** 개체를 사용 하면 hello로 blob 컨테이너를 만들 **createContainer** 메서드.</span><span class="sxs-lookup"><span data-stu-id="46c51-138">A **BlobRestProxy** object lets you create a blob container with hello **createContainer** method.</span></span> <span data-ttu-id="46c51-139">컨테이너를 만들 때에 hello 컨테이너에는 옵션을 설정할 수 있지만, 이렇게 하면 하지 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="46c51-139">When creating a container, you can set options on hello container, but doing so is not required.</span></span> <span data-ttu-id="46c51-140">(tooset hello 컨테이너 제어 목록 (ACL)와 컨테이너 메타 데이터를 액세스 하는 방법을 hello 감시할 보여 줍니다.)</span><span class="sxs-lookup"><span data-stu-id="46c51-140">(hello example below shows how tooset hello container access control list (ACL) and container metadata.)</span></span>

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

<span data-ttu-id="46c51-141">호출 **setPublicAccess (PublicAccessType::CONTAINER\_AND\_BLOB)** 는 hello 익명 요청을 통해 액세스할 수 있는 컨테이너 및 blob 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="46c51-141">Calling **setPublicAccess(PublicAccessType::CONTAINER\_AND\_BLOBS)** makes hello container and blob data accessible via anonymous requests.</span></span> <span data-ttu-id="46c51-142">**setPublicAccess(PublicAccessType::BLOBS_ONLY)**를 호출하면 익명 요청을 통해 Blob 데이터에만 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46c51-142">Calling **setPublicAccess(PublicAccessType::BLOBS_ONLY)** makes only blob data accessible via anonymous requests.</span></span> <span data-ttu-id="46c51-143">컨테이너 ACL에 대한 자세한 내용은 [컨테이너 ACL 설정(REST API)][container-acl]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="46c51-143">For more information about container ACLs, see [Set container ACL (REST API)][container-acl].</span></span>

<span data-ttu-id="46c51-144">Blob service 오류 코드에 대한 자세한 내용은 [Blob service 오류 코드][error-codes](영문)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="46c51-144">For more information about Blob service error codes, see [Blob Service Error Codes][error-codes].</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="46c51-145">컨테이너에 Blob 업로드</span><span class="sxs-lookup"><span data-stu-id="46c51-145">Upload a blob into a container</span></span>
<span data-ttu-id="46c51-146">파일을 사용 하 여 hello blob으로 tooupload **BlobRestProxy createBlockBlob->** 메서드.</span><span class="sxs-lookup"><span data-stu-id="46c51-146">tooupload a file as a blob, use hello **BlobRestProxy->createBlockBlob** method.</span></span> <span data-ttu-id="46c51-147">이 작업은 존재 하지 않으면 되거나 이미 있으면 덮어씁니다 hello blob을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="46c51-147">This operation creates hello blob if it doesn't exist, or overwrites it if it does.</span></span> <span data-ttu-id="46c51-148">hello 아래 코드 예제에서는 해당 hello 컨테이너 이미 만들어져 고 가정 사용 하 여 [fopen] [ fopen] 스트림으로 tooopen hello 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="46c51-148">hello code example below assumes that hello container has already been created and uses [fopen][fopen] tooopen hello file as a stream.</span></span>

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

<span data-ttu-id="46c51-149">이전 샘플 hello를 스트림으로 blob을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="46c51-149">Note that hello previous sample uploads a blob as a stream.</span></span> <span data-ttu-id="46c51-150">하지만 Blob을 사용 하 여 문자열로, 예를 들어 hello 업로드할 수도 있습니다 [파일\_가져오기\_내용을] [ file_get_contents] 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="46c51-150">However, a blob can also be uploaded as a string using, for example, hello [file\_get\_contents][file_get_contents] function.</span></span> <span data-ttu-id="46c51-151">toodo이 hello 이전 샘플을 사용 하 여 변경할 `$content = fopen("c:\myfile.txt", "r");` 너무`$content = file_get_contents("c:\myfile.txt");`합니다.</span><span class="sxs-lookup"><span data-stu-id="46c51-151">toodo this using hello previous sample, change `$content = fopen("c:\myfile.txt", "r");` too`$content = file_get_contents("c:\myfile.txt");`.</span></span>

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="46c51-152">컨테이너에서 hello blob 나열</span><span class="sxs-lookup"><span data-stu-id="46c51-152">List hello blobs in a container</span></span>
<span data-ttu-id="46c51-153">toolist hello blob 컨테이너에서 hello를 사용 하 여 **BlobRestProxy listBlobs->** 메서드는 **foreach** tooloop hello 결과 통해 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="46c51-153">toolist hello blobs in a container, use hello **BlobRestProxy->listBlobs** method with a **foreach** loop tooloop through hello result.</span></span> <span data-ttu-id="46c51-154">hello 다음 코드 컨테이너에서 출력으로 각 blob의 hello 이름을 표시 하 고 해당 URI toohello 브라우저를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="46c51-154">hello following code displays hello name of each blob as output in a container and displays its URI toohello browser.</span></span>

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

## <a name="download-a-blob"></a><span data-ttu-id="46c51-155">Blob 다운로드</span><span class="sxs-lookup"><span data-stu-id="46c51-155">Download a blob</span></span>
<span data-ttu-id="46c51-156">toodownload blob 호출 hello **BlobRestProxy getBlob->** 메서드를 다음 호출 hello **getContentStream** hello 결과에서 메서드가 **GetBlobResult** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="46c51-156">toodownload a blob, call hello **BlobRestProxy->getBlob** method, then call hello **getContentStream** method on hello resulting **GetBlobResult** object.</span></span>

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

<span data-ttu-id="46c51-157">Note 위의 그 hello 예에서 blob 스트림 리소스 (hello 기본 동작)를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="46c51-157">Note that hello example above gets a blob as a stream resource (hello default behavior).</span></span> <span data-ttu-id="46c51-158">그러나 hello를 사용할 수 있습니다 [스트림\_가져오기\_내용을] [ stream-get-contents] 함수 tooconvert hello 스트림 tooa 문자열을 반환 했습니다.</span><span class="sxs-lookup"><span data-stu-id="46c51-158">However, you can use hello [stream\_get\_contents][stream-get-contents] function tooconvert hello returned stream tooa string.</span></span>

## <a name="delete-a-blob"></a><span data-ttu-id="46c51-159">Blob 삭제</span><span class="sxs-lookup"><span data-stu-id="46c51-159">Delete a blob</span></span>
<span data-ttu-id="46c51-160">blob를 toodelete hello 컨테이너 이름 및 blob 이름 전달 너무**BlobRestProxy deleteBlob->**합니다.</span><span class="sxs-lookup"><span data-stu-id="46c51-160">toodelete a blob, pass hello container name and blob name too**BlobRestProxy->deleteBlob**.</span></span>

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

## <a name="delete-a-blob-container"></a><span data-ttu-id="46c51-161">Blob 컨테이너 삭제</span><span class="sxs-lookup"><span data-stu-id="46c51-161">Delete a blob container</span></span>
<span data-ttu-id="46c51-162">마지막으로, blob 컨테이너 toodelete hello 컨테이너 이름을 전달 너무**BlobRestProxy deleteContainer->**합니다.</span><span class="sxs-lookup"><span data-stu-id="46c51-162">Finally, toodelete a blob container, pass hello container name too**BlobRestProxy->deleteContainer**.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="46c51-163">다음 단계</span><span class="sxs-lookup"><span data-stu-id="46c51-163">Next steps</span></span>
<span data-ttu-id="46c51-164">Hello Azure blob 서비스의 기본 사항 hello를 알아보았습니다 했으므로 더 복잡 한 저장소 작업에 대 한 이러한 링크 toolearn를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="46c51-164">Now that you've learned hello basics of hello Azure blob service, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="46c51-165">Hello 방문 [Azure 저장소 팀 블로그](http://blogs.msdn.com/b/windowsazurestorage/)</span><span class="sxs-lookup"><span data-stu-id="46c51-165">Visit hello [Azure Storage team blog](http://blogs.msdn.com/b/windowsazurestorage/)</span></span>
* <span data-ttu-id="46c51-166">Hello 참조 [PHP 블록 blob 예제](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/BlockBlobExample.php)합니다.</span><span class="sxs-lookup"><span data-stu-id="46c51-166">See hello [PHP block blob example](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/BlockBlobExample.php).</span></span>
* <span data-ttu-id="46c51-167">Hello 참조 [PHP 페이지 blob 예제](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/PageBlobExample.php)합니다.</span><span class="sxs-lookup"><span data-stu-id="46c51-167">See hello [PHP page blob example](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/PageBlobExample.php).</span></span>
* [<span data-ttu-id="46c51-168">Hello AzCopy 명령줄 유틸리티를 사용 하 여 데이터를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="46c51-168">Transfer data with hello AzCopy Command-Line Utility</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

<span data-ttu-id="46c51-169">자세한 내용은 참고 항목 hello [PHP 개발자 센터](/develop/php/)합니다.</span><span class="sxs-lookup"><span data-stu-id="46c51-169">For more information, see also hello [PHP Developer Center](/develop/php/).</span></span>

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[container-acl]: http://msdn.microsoft.com/library/azure/dd179391.aspx
[error-codes]: http://msdn.microsoft.com/library/azure/dd179439.aspx
[file_get_contents]: http://php.net/file_get_contents
[require_once]: http://php.net/require_once
[fopen]: http://www.php.net/fopen
[stream-get-contents]: http://www.php.net/stream_get_contents

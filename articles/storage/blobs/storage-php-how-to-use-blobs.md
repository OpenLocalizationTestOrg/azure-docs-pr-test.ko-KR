---
title: "PHP에서 Blob Storage(개체 저장소)를 사용하는 방법 | Microsoft Docs"
description: "Azure Blob 저장소(개체 저장소)를 사용하여 클라우드에 구조화되지 않은 데이터를 저장합니다."
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
ms.openlocfilehash: 4b68844c5d0553eaede3997bf09bff4fe570e850
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-blob-storage-from-php"></a><span data-ttu-id="44924-103">PHP에서 Blob Storage를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="44924-103">How to use blob storage from PHP</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="44924-104">개요</span><span class="sxs-lookup"><span data-stu-id="44924-104">Overview</span></span>
<span data-ttu-id="44924-105">Azure Blob 저장소는 클라우드에 구조화되지 않은 데이터를 개체/Blob로 저장하는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="44924-105">Azure Blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span></span> <span data-ttu-id="44924-106">Blob 저장소는 문서, 미디어 파일 또는 응용 프로그램 설치 프로그램과 같은 모든 종류의 텍스트 또는 이진 데이터를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44924-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="44924-107">또한 Blob Storage를 개체 저장소라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="44924-107">Blob storage is also referred to as object storage.</span></span>

<span data-ttu-id="44924-108">이 가이드에서는 Azure Blob 서비스를 사용하여 일반 시나리오를 수행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="44924-108">This guide shows you how to perform common scenarios using the Azure blob service.</span></span> <span data-ttu-id="44924-109">샘플은 PHP로 작성되었으며 [PHP용 Azure SDK][download]를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="44924-109">The samples are written in PHP and use the [Azure SDK for PHP][download].</span></span> <span data-ttu-id="44924-110">여기서 다루는 시나리오에는 Blob **업로드**, **나열**, **다운로드** 및 **삭제**가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="44924-110">The scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span> <span data-ttu-id="44924-111">Blob에 대한 자세한 내용은 [다음 단계](#next-steps) 섹션을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="44924-111">For more information on blobs, see the [Next steps](#next-steps) section.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="44924-112">PHP 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="44924-112">Create a PHP application</span></span>
<span data-ttu-id="44924-113">Azure Blob 서비스에 액세스하는 PHP 응용 프로그램을 만드는 데 유일한 요구 사항은 코드 내에서 PHP용 Azure SDK의 클래스를 참조하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="44924-113">The only requirement for creating a PHP application that accesses the Azure blob service is the referencing of classes in the Azure SDK for PHP from within your code.</span></span> <span data-ttu-id="44924-114">응용 프로그램을 만드는 데는 메모장을 포함한 어떠한 개발 도구도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44924-114">You can use any development tools to create your application, including Notepad.</span></span>

<span data-ttu-id="44924-115">이 가이드에서는 PHP 응용 프로그램 내에서 로컬로 또는 Azure 웹 역할, 작업자 역할 또는 웹 사이트 내에서 실행되는 코드에서 호출할 수 있는 서비스 기능을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="44924-115">In this guide, you use service features, which can be called within a PHP application locally or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-the-azure-client-libraries"></a><span data-ttu-id="44924-116">Azure 클라이언트 라이브러리 가져오기</span><span class="sxs-lookup"><span data-stu-id="44924-116">Get the Azure Client Libraries</span></span>
[!INCLUDE [get-client-libraries](../../../includes/get-client-libraries.md)]

## <a name="configure-your-application-to-access-the-blob-service"></a><span data-ttu-id="44924-117">응용 프로그램에서 Blob 서비스에 액세스하도록 구성</span><span class="sxs-lookup"><span data-stu-id="44924-117">Configure your application to access the blob service</span></span>
<span data-ttu-id="44924-118">Azure Blob 서비스 API를 사용하려면 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="44924-118">To use the Azure blob service APIs, you need to:</span></span>

1. <span data-ttu-id="44924-119">[require_once] 문을 사용하여 자동 로더 파일 참조 및</span><span class="sxs-lookup"><span data-stu-id="44924-119">Reference the autoloader file using the [require_once] statement, and</span></span>
2. <span data-ttu-id="44924-120">사용할 수 있는 모든 클래스 참조</span><span class="sxs-lookup"><span data-stu-id="44924-120">Reference any classes you might use.</span></span>

<span data-ttu-id="44924-121">다음 예제에서는 자동 로더 파일을 포함하고 **ServicesBuilder** 클래스를 참조하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="44924-121">The following example shows how to include the autoloader file and reference the **ServicesBuilder** class.</span></span>

> [!NOTE]
> <span data-ttu-id="44924-122">이 문서의 예제에서는 Azure용 PHP 클라이언트 라이브러리를 작성기를 통해 설치했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="44924-122">The examples in this article assume you have installed the PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="44924-123">라이브러리를 수동으로 설치한 경우 `WindowsAzure.php` 자동 로더 파일을 참조해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="44924-123">If you installed the libraries manually, you need to reference the `WindowsAzure.php` autoloader file.</span></span>
>
>

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="44924-124">아래 예제에서 `require_once` 문은 항상 표시되지만 예제를 실행하는 데 필요한 클래스만 참조됩니다.</span><span class="sxs-lookup"><span data-stu-id="44924-124">In the examples below, the `require_once` statement will be shown always, but only the classes necessary for the example to execute are referenced.</span></span>

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="44924-125">Azure 저장소 연결 설정</span><span class="sxs-lookup"><span data-stu-id="44924-125">Set up an Azure storage connection</span></span>
<span data-ttu-id="44924-126">Azure Blob 서비스 클라이언트를 인스턴스화하려면 먼저 유효한 연결 문자열이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="44924-126">To instantiate an Azure blob service client, you must first have a valid connection string.</span></span> <span data-ttu-id="44924-127">Blob 서비스 연결 문자열 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="44924-127">The format for the blob service connection string is:</span></span>

<span data-ttu-id="44924-128">Live 서비스에 액세스하는 경우:</span><span class="sxs-lookup"><span data-stu-id="44924-128">For accessing a live service:</span></span>

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

<span data-ttu-id="44924-129">저장소 에뮬레이터에 액세스하는 경우:</span><span class="sxs-lookup"><span data-stu-id="44924-129">For accessing the storage emulator:</span></span>

```php
UseDevelopmentStorage=true
```

<span data-ttu-id="44924-130">Azure 서비스 클라이언트를 만들려면 **ServicesBuilder** 클래스를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="44924-130">To create any Azure service client, you need to use the **ServicesBuilder** class.</span></span> <span data-ttu-id="44924-131">다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44924-131">You can:</span></span>

* <span data-ttu-id="44924-132">연결 문자열을 직접 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44924-132">Pass the connection string directly to it or</span></span>
* <span data-ttu-id="44924-133">**CCM(CloudConfigurationManager)** 을 사용하여 여러 외부 소스에서 연결 문자열을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44924-133">Use the **CloudConfigurationManager (CCM)** to check multiple external sources for the connection string:</span></span>
  * <span data-ttu-id="44924-134">기본적으로 하나의 외부 소스, 환경 변수에 대한 지원이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="44924-134">By default, it comes with support for one external source - environmental variables.</span></span>
  * <span data-ttu-id="44924-135">**ConnectionStringSource** 클래스를 확장하여 새 소스를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44924-135">You can add new sources by extending the **ConnectionStringSource** class.</span></span>

<span data-ttu-id="44924-136">여기에 설명된 예제의 경우 연결 문자열이 직접 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="44924-136">For the examples outlined here, the connection string will be passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);
```

## <a name="create-a-container"></a><span data-ttu-id="44924-137">컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="44924-137">Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="44924-138">**BlobRestProxy** 개체를 사용하여 **createContainer** 메서드로 Blob 컨테이너를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44924-138">A **BlobRestProxy** object lets you create a blob container with the **createContainer** method.</span></span> <span data-ttu-id="44924-139">컨테이너를 만드는 경우 컨테이너에 대한 옵션을 설정할 수 있으나 반드시 옵션을 설정해야 하는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="44924-139">When creating a container, you can set options on the container, but doing so is not required.</span></span> <span data-ttu-id="44924-140">아래 예제에서는 컨테이너 ACL(액세스 제어 목록) 및 컨테이너 메타데이터를 설정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="44924-140">(The example below shows how to set the container access control list (ACL) and container metadata.)</span></span>

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
// proxys can enumerate blobs within the container via anonymous
// request, but cannot enumerate containers within the storage account.
//
// BLOBS_ONLY:
// Specifies public read access for blobs. Blob data within this
// container can be read via anonymous request, but container data is not
// available. proxys cannot enumerate blobs within the container via
// anonymous request.
// If this value is not specified in the request, container data is
// private to the account owner.
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

<span data-ttu-id="44924-141">**setPublicAccess(PublicAccessType::CONTAINER\_AND\_BLOBS)**를 호출하면 익명 요청을 통해 컨테이너 및 Blob 데이터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44924-141">Calling **setPublicAccess(PublicAccessType::CONTAINER\_AND\_BLOBS)** makes the container and blob data accessible via anonymous requests.</span></span> <span data-ttu-id="44924-142">**setPublicAccess(PublicAccessType::BLOBS_ONLY)**를 호출하면 익명 요청을 통해 Blob 데이터에만 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44924-142">Calling **setPublicAccess(PublicAccessType::BLOBS_ONLY)** makes only blob data accessible via anonymous requests.</span></span> <span data-ttu-id="44924-143">컨테이너 ACL에 대한 자세한 내용은 [컨테이너 ACL 설정(REST API)][container-acl]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="44924-143">For more information about container ACLs, see [Set container ACL (REST API)][container-acl].</span></span>

<span data-ttu-id="44924-144">Blob service 오류 코드에 대한 자세한 내용은 [Blob service 오류 코드][error-codes](영문)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="44924-144">For more information about Blob service error codes, see [Blob Service Error Codes][error-codes].</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="44924-145">컨테이너에 Blob 업로드</span><span class="sxs-lookup"><span data-stu-id="44924-145">Upload a blob into a container</span></span>
<span data-ttu-id="44924-146">파일을 Blob으로 업로드하려면 **BlobRestProxy->createBlockBlob** 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="44924-146">To upload a file as a blob, use the **BlobRestProxy->createBlockBlob** method.</span></span> <span data-ttu-id="44924-147">이 작업은 Blob이 없는 경우 새로 만들고, Blob이 있는 경우 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="44924-147">This operation creates the blob if it doesn't exist, or overwrites it if it does.</span></span> <span data-ttu-id="44924-148">아래 코드 예제에서는 컨테이너가 이미 만들어졌고 [fopen][fopen]을 사용하여 파일을 스트림으로 연다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="44924-148">The code example below assumes that the container has already been created and uses [fopen][fopen] to open the file as a stream.</span></span>

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

<span data-ttu-id="44924-149">이전 샘플에서는 Blob을 스트림으로 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="44924-149">Note that the previous sample uploads a blob as a stream.</span></span> <span data-ttu-id="44924-150">그러나 Blob은 예를 들어 [file\_get\_contents][file_get_contents] 함수를 사용하여 문자열로 업로드될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44924-150">However, a blob can also be uploaded as a string using, for example, the [file\_get\_contents][file_get_contents] function.</span></span> <span data-ttu-id="44924-151">이전 샘플을 사용하여 이 작업을 수행하려면 `$content = fopen("c:\myfile.txt", "r");`을 `$content = file_get_contents("c:\myfile.txt");`로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="44924-151">To do this using the previous sample, change `$content = fopen("c:\myfile.txt", "r");` to `$content = file_get_contents("c:\myfile.txt");`.</span></span>

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="44924-152">컨테이너의 Blob 나열</span><span class="sxs-lookup"><span data-stu-id="44924-152">List the blobs in a container</span></span>
<span data-ttu-id="44924-153">컨테이너의 Blob을 나열하려면 **BlobRestProxy->listBlobs** 메서드를 **foreach** 루프와 함께 사용하여 결과를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="44924-153">To list the blobs in a container, use the **BlobRestProxy->listBlobs** method with a **foreach** loop to loop through the result.</span></span> <span data-ttu-id="44924-154">다음 코드는 컨테이너의 각 Blob 이름을 출력으로 표시하고 해당 URI를 브라우저에 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="44924-154">The following code displays the name of each blob as output in a container and displays its URI to the browser.</span></span>

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

## <a name="download-a-blob"></a><span data-ttu-id="44924-155">Blob 다운로드</span><span class="sxs-lookup"><span data-stu-id="44924-155">Download a blob</span></span>
<span data-ttu-id="44924-156">Blob을 다운로드하려면 **BlobRestProxy->getBlob** 메서드를 호출한 다음 결과 **GetBlobResult** 개체에서 **getContentStream** 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="44924-156">To download a blob, call the **BlobRestProxy->getBlob** method, then call the **getContentStream** method on the resulting **GetBlobResult** object.</span></span>

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

<span data-ttu-id="44924-157">위의 예제에서는 Blob을 스트림 리소스로 가져옵니다(기본 동작).</span><span class="sxs-lookup"><span data-stu-id="44924-157">Note that the example above gets a blob as a stream resource (the default behavior).</span></span> <span data-ttu-id="44924-158">그러나 [stream\_get\_contents][stream-get-contents] 함수를 사용하여 반환된 스트림을 문자열로 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44924-158">However, you can use the [stream\_get\_contents][stream-get-contents] function to convert the returned stream to a string.</span></span>

## <a name="delete-a-blob"></a><span data-ttu-id="44924-159">Blob 삭제</span><span class="sxs-lookup"><span data-stu-id="44924-159">Delete a blob</span></span>
<span data-ttu-id="44924-160">Blob을 삭제하려면 컨테이너 이름 및 Blob 이름을 **BlobRestProxy->deleteBlob**에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="44924-160">To delete a blob, pass the container name and blob name to **BlobRestProxy->deleteBlob**.</span></span>

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

## <a name="delete-a-blob-container"></a><span data-ttu-id="44924-161">Blob 컨테이너 삭제</span><span class="sxs-lookup"><span data-stu-id="44924-161">Delete a blob container</span></span>
<span data-ttu-id="44924-162">마지막으로 Blob 컨테이너를 삭제하려면 컨테이너 이름을 **BlobRestProxy->deleteContainer**에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="44924-162">Finally, to delete a blob container, pass the container name to **BlobRestProxy->deleteContainer**.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="44924-163">다음 단계</span><span class="sxs-lookup"><span data-stu-id="44924-163">Next steps</span></span>
<span data-ttu-id="44924-164">이제 Azure Blob 서비스의 기본 사항을 배웠으므로 다음 링크를 따라 좀더 복잡한 저장소 작업에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="44924-164">Now that you've learned the basics of the Azure blob service, follow these links to learn about more complex storage tasks.</span></span>

* <span data-ttu-id="44924-165">[Azure 저장소 팀 블로그](http://blogs.msdn.com/b/windowsazurestorage/)</span><span class="sxs-lookup"><span data-stu-id="44924-165">Visit the [Azure Storage team blog](http://blogs.msdn.com/b/windowsazurestorage/)</span></span>
* <span data-ttu-id="44924-166">[PHP 블록 Blob 예](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/BlockBlobExample.php)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="44924-166">See the [PHP block blob example](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/BlockBlobExample.php).</span></span>
* <span data-ttu-id="44924-167">[PHP 페이지 Blob 예](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/PageBlobExample.php)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="44924-167">See the [PHP page blob example](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/PageBlobExample.php).</span></span>
* [<span data-ttu-id="44924-168">AzCopy 명령줄 유틸리티로 데이터 전송</span><span class="sxs-lookup"><span data-stu-id="44924-168">Transfer data with the AzCopy Command-Line Utility</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

<span data-ttu-id="44924-169">자세한 내용은 [PHP 개발자 센터](/develop/php/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="44924-169">For more information, see also the [PHP Developer Center](/develop/php/).</span></span>

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[container-acl]: http://msdn.microsoft.com/library/azure/dd179391.aspx
[error-codes]: http://msdn.microsoft.com/library/azure/dd179439.aspx
[file_get_contents]: http://php.net/file_get_contents
[require_once]: http://php.net/require_once
[fopen]: http://www.php.net/fopen
[stream-get-contents]: http://www.php.net/stream_get_contents

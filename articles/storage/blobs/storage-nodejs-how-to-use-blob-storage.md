---
title: "Node.js에서 Blob Storage를 사용하는 방법 | Microsoft Docs"
description: "Azure Blob 저장소(개체 저장소)를 사용하여 클라우드에 구조화되지 않은 데이터를 저장합니다."
services: storage
documentationcenter: nodejs
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 8b0df222-1ca8-4967-8248-6d6d720947b8
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: e83ad647f6b7c70f34ef0c69b5bf322da5b6d60d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-blob-storage-from-nodejs"></a><span data-ttu-id="255ef-103">Node.js에서 Blob Storage를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="255ef-103">How to use Blob storage from Node.js</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-all](../../../includes/storage-check-out-samples-all.md)]

## <a name="overview"></a><span data-ttu-id="255ef-104">개요</span><span class="sxs-lookup"><span data-stu-id="255ef-104">Overview</span></span>
<span data-ttu-id="255ef-105">이 문서에서는 Blob Storage를 사용하여 일반 시나리오를 수행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-105">This article shows you how to perform common scenarios using Blob storage.</span></span> <span data-ttu-id="255ef-106">샘플은 Node.js API를 사용하여 작성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-106">The samples are written via the Node.js API.</span></span> <span data-ttu-id="255ef-107">여기서 다루는 시나리오는 Blob을 업로드, 나열, 다운로드 및 삭제하는 방법을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-107">The scenarios covered include how to upload, list, download, and delete blobs.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="255ef-108">Node.js 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="255ef-108">Create a Node.js application</span></span>
<span data-ttu-id="255ef-109">Node.js 응용 프로그램을 만드는 방법에 대한 지침은 [Azure App Service에서 Node.js 웹앱 만들기], [Azure Cloud Service에 Node.js 응용 프로그램 빌드 및 배포](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md)(Windows PowerShell 사용) 또는 [Web Matrix를 사용하여 Azure에 Node.js 웹앱 빌드 및 배포](https://www.microsoft.com/web/webmatrix/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="255ef-109">For instructions on how to create a Node.js application, see [Create a Node.js web app in Azure App Service], [Build and deploy a Node.js application to an Azure Cloud Service](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) -- using Windows PowerShell, or [Build and deploy a Node.js web app to Azure using Web Matrix](https://www.microsoft.com/web/webmatrix/).</span></span>

## <a name="configure-your-application-to-access-storage"></a><span data-ttu-id="255ef-110">저장소에 액세스하도록 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="255ef-110">Configure your application to access storage</span></span>
<span data-ttu-id="255ef-111">Azure 저장소를 사용하려면 저장소 REST 서비스와 통신하는 편리한 라이브러리 집합이 포함되어 있는 Node.js용 Azure 저장소 SDK가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-111">To use Azure storage, you need the Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with the storage REST services.</span></span>

### <a name="use-node-package-manager-npm-to-obtain-the-package"></a><span data-ttu-id="255ef-112">NPM(Node Package Manager)을 사용하여 패키지 가져오기</span><span class="sxs-lookup"><span data-stu-id="255ef-112">Use Node Package Manager (NPM) to obtain the package</span></span>
1. <span data-ttu-id="255ef-113">**PowerShell**(Windows), **Terminal**(Mac), **Bash**(Unix) 등과 같은 명령줄 인터페이스를 사용하여 샘플 응용 프로그램을 만든 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-113">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix), to navigate to the folder where you created your sample application.</span></span>
2. <span data-ttu-id="255ef-114">명령 창에 **npm install azure-storage** 를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-114">Type **npm install azure-storage** in the command window.</span></span> <span data-ttu-id="255ef-115">명령 출력은 다음 코드 예제와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-115">Output from the command is similar to the following code example.</span></span>

        azure-storage@0.5.0 node_modules\azure-storage
        +-- extend@1.2.1
        +-- xmlbuilder@0.4.3
        +-- mime@1.2.11
        +-- node-uuid@1.4.3
        +-- validator@3.22.2
        +-- underscore@1.4.4
        +-- readable-stream@1.0.33 (string_decoder@0.10.31, isarray@0.0.1, inherits@2.0.1, core-util-is@1.0.1)
        +-- xml2js@0.2.7 (sax@0.5.2)
        +-- request@2.57.0 (caseless@0.10.0, aws-sign2@0.5.0, forever-agent@0.6.1, stringstream@0.0.4, oauth-sign@0.8.0, tunnel-agent@0.4.1, isstream@0.1.2, json-stringify-safe@5.0.1, bl@0.9.4, combined-stream@1.0.5, qs@3.1.0, mime-types@2.0.14, form-data@0.2.0, http-signature@0.11.0, tough-cookie@2.0.0, hawk@2.3.1, har-validator@1.8.0)
3. <span data-ttu-id="255ef-116">**ls** 명령을 수동으로 실행하여 **node\_modules** 폴더가 만들어졌는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-116">You can manually run the **ls** command to verify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="255ef-117">해당 폴더 내에서 저장소에 액세스하는 데 필요한 라이브러리가 들어 있는 **azure-storage** 패키지를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-117">Inside that folder, find the **azure-storage** package, which contains the libraries that you need to access storage.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="255ef-118">패키지 가져오기</span><span class="sxs-lookup"><span data-stu-id="255ef-118">Import the package</span></span>
<span data-ttu-id="255ef-119">메모장 또는 다른 텍스트 편집기를 사용하여 저장소를 사용할 응용 프로그램의 **server.js** 파일 맨 위에 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-119">Using Notepad or another text editor, add the following to the top of the **server.js** file of the application where you intend to use storage:</span></span>

```nodejs
var azure = require('azure-storage');
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="255ef-120">Azure 저장소 연결 설정</span><span class="sxs-lookup"><span data-stu-id="255ef-120">Set up an Azure Storage connection</span></span>
<span data-ttu-id="255ef-121">Azure 모듈은 및 또는 환경 변수를 읽고 `AZURE_STORAGE_ACCOUNT``AZURE_STORAGE_ACCESS_KEY`Azure 저장소 계정에 연결하는 데 `AZURE_STORAGE_CONNECTION_STRING`필요한 정보를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-121">The Azure module will read the environment variables `AZURE_STORAGE_ACCOUNT` and `AZURE_STORAGE_ACCESS_KEY`, or `AZURE_STORAGE_CONNECTION_STRING`, for information required to connect to your Azure storage account.</span></span> <span data-ttu-id="255ef-122">이러한 환경 변수가 설정되어 있지 않은 경우 **createBlobService**를 호출할 때 계정 정보를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-122">If these environment variables are not set, you must specify the account information when calling **createBlobService**.</span></span>

<span data-ttu-id="255ef-123">Azure 웹앱의 [Azure Portal](https://portal.azure.com)에서 환경 변수를 설정하는 방법에 대한 예제는 [Azure Table Service를 사용하는 Node.js 웹앱](../../app-service-web/storage-nodejs-use-table-storage-web-site.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="255ef-123">For an example of setting the environment variables in the [Azure portal](https://portal.azure.com) for an Azure web app, see [Node.js web app using the Azure Table Service](../../app-service-web/storage-nodejs-use-table-storage-web-site.md).</span></span>

## <a name="create-a-container"></a><span data-ttu-id="255ef-124">컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="255ef-124">Create a container</span></span>
<span data-ttu-id="255ef-125">**BlobService** 개체를 통해 컨테이너 및 Blob에 대한 작업을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-125">The **BlobService** object lets you work with containers and blobs.</span></span> <span data-ttu-id="255ef-126">다음 코드는 **BlobService** 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-126">The following code creates a **BlobService** object.</span></span> <span data-ttu-id="255ef-127">**server.js**의 위쪽에 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-127">Add the following near the top of **server.js**:</span></span>

```nodejs
var blobSvc = azure.createBlobService();
```

> [!NOTE]
> <span data-ttu-id="255ef-128">**createBlobServiceAnonymous** 를 사용하고 호스트 주소를 제공하여 익명으로 Blob에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-128">You can access a blob anonymously by using **createBlobServiceAnonymous** and providing the host address.</span></span> <span data-ttu-id="255ef-129">예를 들면 `var blobSvc = azure.createBlobServiceAnonymous('https://myblob.blob.core.windows.net/');`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-129">For example, use `var blobSvc = azure.createBlobServiceAnonymous('https://myblob.blob.core.windows.net/');`.</span></span>
>
>

[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="255ef-130">새 컨테이너를 만들려면 **createContainerIfNotExists**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-130">To create a new container, use **createContainerIfNotExists**.</span></span> <span data-ttu-id="255ef-131">다음 코드 예제에서는 'mycontainer'라는 이름의 새 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-131">The following code example creates a new container named 'mycontainer':</span></span>

```nodejs
blobSvc.createContainerIfNotExists('mycontainer', function(error, result, response){
    if(!error){
      // Container exists and is private
    }
});
```

<span data-ttu-id="255ef-132">컨테이너를 새로 작성하는 경우 `result.created` 는 true입니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-132">If the container is newly created, `result.created` is true.</span></span> <span data-ttu-id="255ef-133">컨테이너가 이미 있는 경우 `result.created` 는 false입니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-133">If the container already exists, `result.created` is false.</span></span> <span data-ttu-id="255ef-134">`response` 에는 컨테이너의 ETag 정보와 같은 작업 관련 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-134">`response` contains information about the operation, including the ETag information for the container.</span></span>

### <a name="container-security"></a><span data-ttu-id="255ef-135">컨테이너 보안</span><span class="sxs-lookup"><span data-stu-id="255ef-135">Container security</span></span>
<span data-ttu-id="255ef-136">기본적으로 새 컨테이너는 개인 컨테이너이며 익명으로 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-136">By default, new containers are private and cannot be accessed anonymously.</span></span> <span data-ttu-id="255ef-137">컨테이너를 공용으로 만들어 익명으로 액세스할 수 있게 하려면 컨테이너의 액세스 수준을 **blob** 또는 **컨테이너**로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-137">To make the container public so that you can access it anonymously, you can set the container's access level to **blob** or **container**.</span></span>

* <span data-ttu-id="255ef-138">**blob** - 이 컨테이너 내의 Blob 콘텐츠와 메타데이터에는 익명 읽기 액세스가 허용되지만, 컨테이너 내의 모든 Blob 나열과 같은 컨테이너 메타데이터에는 익명 읽기 권한이 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-138">**blob** - allows anonymous read access to blob content and metadata within this container, but not to container metadata such as listing all blobs within a container</span></span>
* <span data-ttu-id="255ef-139">**컨테이너** - Blob 콘텐츠 및 메타데이터와 컨테이너 메타데이터에 대한 익명 읽기 권한을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-139">**container** - allows anonymous read access to blob content and metadata as well as container metadata</span></span>

<span data-ttu-id="255ef-140">다음 코드 예제에서는 액세스 수준을 **Blob**으로 설정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-140">The following code example demonstrates setting the access level to **blob**:</span></span>

```nodejs
blobSvc.createContainerIfNotExists('mycontainer', {publicAccessLevel : 'blob'}, function(error, result, response){
    if(!error){
      // Container exists and allows
      // anonymous read access to blob
      // content and metadata within this container
    }
});
```

<span data-ttu-id="255ef-141">또는 **setContainerAcl** 로 액세스 수준을 지정하여 컨테이너의 액세스 수준을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-141">Alternatively, you can modify the access level of a container by using **setContainerAcl** to specify the access level.</span></span> <span data-ttu-id="255ef-142">다음 코드 예제에서는 액세스 수준을 container로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-142">The following code example changes the access level to container:</span></span>

```nodejs
blobSvc.setContainerAcl('mycontainer', null /* signedIdentifiers */, {publicAccessLevel : 'container'} /* publicAccessLevel*/, function(error, result, response){
  if(!error){
    // Container access level set to 'container'
  }
});
```

<span data-ttu-id="255ef-143">result 값에는 컨테이너의 **ETag** 정보와 같은 작업 관련 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-143">The result contains information about the operation, including the current **ETag** for the container.</span></span>

### <a name="filters"></a><span data-ttu-id="255ef-144">필터</span><span class="sxs-lookup"><span data-stu-id="255ef-144">Filters</span></span>
<span data-ttu-id="255ef-145">**BlobService**를 사용하여 수행되는 작업에 선택적 필터링 작업을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-145">You can apply optional filtering operations to operations performed using **BlobService**.</span></span> <span data-ttu-id="255ef-146">필터링 작업은 로깅, 자동 재시도 등을 포함할 수 있습니다. 필터는 시그니쳐가 있는 메서드를 구현하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-146">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with the signature:</span></span>

```nodejs
function handle (requestOptions, next)
```

<span data-ttu-id="255ef-147">요청 옵션에 대한 전처리를 수행한 후 메서드는 다음 서명을 사용하여 콜백을 전달하는 "next"를 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-147">After doing its preprocessing on the request options, the method needs to call "next", passing a callback with the following signature:</span></span>

```nodejs
function (returnObject, finalCallback, next)
```

<span data-ttu-id="255ef-148">이 콜백에서 returnObject(서버에 요청 응답 반환)를 처리한 후 콜백은 next(있는 경우)를 호출하여 다른 필터를 계속 처리하거나 finalCallback을 호출하여 서비스 호출을 종료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-148">In this callback, and after processing the returnObject (the response from the request to the server), the callback needs to either invoke next if it exists to continue processing other filters or simply invoke finalCallback to end the service invocation.</span></span>

<span data-ttu-id="255ef-149">Node.js용 Azure SDK에는 재시도 논리를 구현하는 두 필터 **ExponentialRetryPolicyFilter** 및 **LinearRetryPolicyFilter**가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-149">Two filters that implement retry logic are included with the Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="255ef-150">다음은 **ExponentialRetryPolicyFilter**를 사용하는 **BlobService** 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-150">The following creates a **BlobService** object that uses the **ExponentialRetryPolicyFilter**:</span></span>

```nodejs
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var blobSvc = azure.createBlobService().withFilter(retryOperations);
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="255ef-151">컨테이너에 Blob 업로드</span><span class="sxs-lookup"><span data-stu-id="255ef-151">Upload a blob into a container</span></span>
<span data-ttu-id="255ef-152">블록 Blob, 페이지 Blob 및 추가 Blob의 세 가지 Blob 유형이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-152">There are three types of blobs: block blobs, page blobs and append blobs.</span></span> <span data-ttu-id="255ef-153">블록 Blob을 사용하면 대용량 데이터를 보다 효율적으로 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-153">Block blobs allow you to more efficiently upload large data.</span></span> <span data-ttu-id="255ef-154">추가 Blob은 추가 작업에 최적화되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-154">Append blobs are optimized for append operations.</span></span> <span data-ttu-id="255ef-155">페이지 Blob은 읽기/쓰기 작업에 최적화되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-155">Page blobs are optimized for read/write operations.</span></span> <span data-ttu-id="255ef-156">자세한 내용은 [블록 Blob, 추가 Blob 및 페이지 Blob 이해](http://msdn.microsoft.com/library/azure/ee691964.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="255ef-156">For more information, see [Understanding Block Blobs, Append Blobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span></span>

### <a name="block-blobs"></a><span data-ttu-id="255ef-157">블록 Blob</span><span class="sxs-lookup"><span data-stu-id="255ef-157">Block blobs</span></span>
<span data-ttu-id="255ef-158">데이터를 블록 Blob으로 업로드하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-158">To upload data to a block blob, use the following:</span></span>

* <span data-ttu-id="255ef-159">**createBlockBlobFromLocalFile** - 새 블록 Blob을 만들고 파일 내용을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-159">**createBlockBlobFromLocalFile** - creates a new block blob and uploads the contents of a file</span></span>
* <span data-ttu-id="255ef-160">**createBlockBlobFromStream** - 새 블록 Blob을 만들고 스트림의 내용을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-160">**createBlockBlobFromStream** - creates a new block blob and uploads the contents of a stream</span></span>
* <span data-ttu-id="255ef-161">**createBlockBlobFromText** - 새 블록 Blob을 만들고 문자열의 내용을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-161">**createBlockBlobFromText** - creates a new block blob and uploads the contents of a string</span></span>
* <span data-ttu-id="255ef-162">**createWriteStreamToBlockBlob** - 블록 Blob에 쓰기 스트림을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-162">**createWriteStreamToBlockBlob** - provides a write stream to a block blob</span></span>

<span data-ttu-id="255ef-163">다음 코드 예제에서는 **test.txt** 파일의 내용을 **myblob**에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-163">The following code example uploads the contents of the **test.txt** file into **myblob**.</span></span>

```nodejs
blobSvc.createBlockBlobFromLocalFile('mycontainer', 'myblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

<span data-ttu-id="255ef-164">이 메서드에 의해 `result` 반환되면 Blob의 **ETag** 와 같은 작업 관련 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-164">The `result` returned by these methods contains information on the operation, such as the **ETag** of the blob.</span></span>

### <a name="append-blobs"></a><span data-ttu-id="255ef-165">추가 Blob</span><span class="sxs-lookup"><span data-stu-id="255ef-165">Append blobs</span></span>
<span data-ttu-id="255ef-166">데이터를 추가 Blob으로 업로드하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-166">To upload data to a new append blob, use the following:</span></span>

* <span data-ttu-id="255ef-167">**createAppendBlobFromLocalFile** - 새 추가 Blob을 만들고 파일 내용을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-167">**createAppendBlobFromLocalFile** - creates a new append blob and uploads the contents of a file</span></span>
* <span data-ttu-id="255ef-168">**createAppendBlobFromStream** - 새 추가 Blob을 만들고 스트림 내용을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-168">**createAppendBlobFromStream** - creates a new append blob and uploads the contents of a stream</span></span>
* <span data-ttu-id="255ef-169">**createAppendBlobFromText** - 새 추가 Blob을 만들고 문자열 내용을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-169">**createAppendBlobFromText** - creates a new append blob and uploads the contents of a string</span></span>
* <span data-ttu-id="255ef-170">**createWriteStreamToNewAppendBlob** - 새 추가 Blob을 만든 다음 쓸 스트림을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-170">**createWriteStreamToNewAppendBlob** - creates a new append blob and then provides a stream to write to it</span></span>

<span data-ttu-id="255ef-171">다음 코드 예제에서는 **test.txt** 파일의 내용을 **myappendblob**에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-171">The following code example uploads the contents of the **test.txt** file into **myappendblob**.</span></span>

```nodejs
blobSvc.createAppendBlobFromLocalFile('mycontainer', 'myappendblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

<span data-ttu-id="255ef-172">기존 추가 Blob에 블록을 추가하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-172">To append a block to an existing append blob, use the following:</span></span>

* <span data-ttu-id="255ef-173">**appendFromLocalFile** -기존 추가 Blob에 파일 내용을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-173">**appendFromLocalFile** - append the contents of a file to an existing append blob</span></span>
* <span data-ttu-id="255ef-174">**appendFromStream** -기존 추가 Blob에 스트림 내용을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-174">**appendFromStream** - append the contents of a stream to an existing append blob</span></span>
* <span data-ttu-id="255ef-175">**appendFromText** -기존 추가 Blob에 문자열 내용을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-175">**appendFromText** - append the contents of a string to an existing append blob</span></span>
* <span data-ttu-id="255ef-176">**appendBlockFromStream** -기존 추가 Blob에 스트림 내용을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-176">**appendBlockFromStream** - append the contents of a stream to an existing append blob</span></span>
* <span data-ttu-id="255ef-177">**appendBlockFromText** -기존 추가 Blob에 문자열 내용을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-177">**appendBlockFromText** - append the contents of a string to an existing append blob</span></span>

> [!NOTE]
> <span data-ttu-id="255ef-178">appendFromXXX API는 불필요한 서버 호출을 방지하기 위해 빠른 오류에 대한 일부 클라이언트 쪽 유효성 검사를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-178">appendFromXXX APIs will do some client-side validation to fail fast to avoid unnecessary server calls.</span></span> <span data-ttu-id="255ef-179">appendBlockFromXXX는 이를 수행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-179">appendBlockFromXXX won't.</span></span>
>
>

<span data-ttu-id="255ef-180">다음 코드 예제에서는 **test.txt** 파일의 내용을 **myappendblob**에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-180">The following code example uploads the contents of the **test.txt** file into **myappendblob**.</span></span>

```nodejs
blobSvc.appendFromText('mycontainer', 'myappendblob', 'text to be appended', function(error, result, response){
  if(!error){
    // text appended
  }
});
```

### <a name="page-blobs"></a><span data-ttu-id="255ef-181">페이지 Blob</span><span class="sxs-lookup"><span data-stu-id="255ef-181">Page blobs</span></span>
<span data-ttu-id="255ef-182">데이터를 페이지 Blob으로 업로드하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-182">To upload data to a page blob, use the following:</span></span>

* <span data-ttu-id="255ef-183">**createPageBlob** - 특정 길이의 새 페이지 Blob을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-183">**createPageBlob** - creates a new page blob of a specific length</span></span>
* <span data-ttu-id="255ef-184">**createPageBlobFromLocalFile** - 새 페이지 Blob을 만들고 파일 내용을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-184">**createPageBlobFromLocalFile** - creates a new page blob and uploads the contents of a file</span></span>
* <span data-ttu-id="255ef-185">**createPageBlobFromStream** - 새 페이지 Blob을 만들고 스트림의 내용을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-185">**createPageBlobFromStream** - creates a new page blob and uploads the contents of a stream</span></span>
* <span data-ttu-id="255ef-186">**createWriteStreamToExistingPageBlob** - 기존 페이지 Blob에 쓰기 스트림을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-186">**createWriteStreamToExistingPageBlob** - provides a write stream to an existing page blob</span></span>
* <span data-ttu-id="255ef-187">**createWriteStreamToNewPageBlob** - 새 페이지 Blob을 만든 다음 쓸 스트림을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-187">**createWriteStreamToNewPageBlob** - creates a new page blob and then provides a stream to write to it</span></span>

<span data-ttu-id="255ef-188">다음 코드 예제에서는 **test.txt** 파일의 내용을 **mypageblob**에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-188">The following code example uploads the contents of the **test.txt** file into **mypageblob**.</span></span>

```nodejs
blobSvc.createPageBlobFromLocalFile('mycontainer', 'mypageblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

> [!NOTE]
> <span data-ttu-id="255ef-189">페이지 Bobl은 512바이트의 '페이지'로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-189">Page blobs consist of 512-byte 'pages'.</span></span> <span data-ttu-id="255ef-190">크기가 512의 배수가 아닌 경우에는 데이터를 업로드할 때 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-190">You will receive an error when uploading data with a size that is not a multiple of 512.</span></span>
>
>

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="255ef-191">컨테이너의 Blob 나열</span><span class="sxs-lookup"><span data-stu-id="255ef-191">List the blobs in a container</span></span>
<span data-ttu-id="255ef-192">컨테이너 내의 Blob을 나열하려면 **listBlobsSegmented** 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-192">To list the blobs in a container, use the **listBlobsSegmented** method.</span></span> <span data-ttu-id="255ef-193">특정 접두사가 있는 Blob을 반환하려면 **listBlobsSegmentedWithPrefix**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-193">If you'd like to return blobs with a specific prefix, use **listBlobsSegmentedWithPrefix**.</span></span>

```nodejs
blobSvc.listBlobsSegmented('mycontainer', null, function(error, result, response){
  if(!error){
      // result.entries contains the entries
      // If not all blobs were returned, result.continuationToken has the continuation token.
  }
});
```

<span data-ttu-id="255ef-194">`result`에는 각 Blob을 설명하는 개체의 배열인 `entries` 컬렉션이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-194">The `result` contains an `entries` collection, which is an array of objects that describe each blob.</span></span> <span data-ttu-id="255ef-195">또한 Blob을 모두 반환할 수 없는 경우에는 `result`에서 추가 항목 검색에 두 번째 매개 변수로 사용할 수 있는 `continuationToken`을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-195">If all blobs cannot be returned, the `result` also provides a `continuationToken`, which you may use as the second parameter to retrieve additional entries.</span></span>

## <a name="download-blobs"></a><span data-ttu-id="255ef-196">Blob 다운로드</span><span class="sxs-lookup"><span data-stu-id="255ef-196">Download blobs</span></span>
<span data-ttu-id="255ef-197">Blob에서 데이터를 다운로드하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-197">To download data from a blob, use the following:</span></span>

* <span data-ttu-id="255ef-198">**getBlobToLocalFile** - Blob의 내용을 파일에 씁니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-198">**getBlobToLocalFile** - writes the blob contents to file</span></span>
* <span data-ttu-id="255ef-199">**getBlobToStream** - Blob의 내용을 스트림에 씁니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-199">**getBlobToStream** - writes the blob contents to a stream</span></span>
* <span data-ttu-id="255ef-200">**getBlobToText** - Blob의 내용을 문자열에 씁니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-200">**getBlobToText** - writes the blob contents to a string</span></span>
* <span data-ttu-id="255ef-201">**createReadStream** - Blob에서 읽는 스트림을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-201">**createReadStream** - provides a stream to read from the blob</span></span>

<span data-ttu-id="255ef-202">다음 코드 예제에서는 **getBlobToStream**을 사용하여 **myblob** Blob의 콘텐츠를 다운로드한 다음 스트림을 사용하여 **output.txt** 파일에 저장하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-202">The following code example demonstrates using **getBlobToStream** to download the contents of the **myblob** blob and store it to the **output.txt** file by using a stream:</span></span>

```nodejs
var fs = require('fs');
blobSvc.getBlobToStream('mycontainer', 'myblob', fs.createWriteStream('output.txt'), function(error, result, response){
  if(!error){
    // blob retrieved
  }
});
```

<span data-ttu-id="255ef-203">`result` 에는 **ETag** 정보를 비롯한 Blob 관련 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-203">The `result` contains information about the blob, including **ETag** information.</span></span>

## <a name="delete-a-blob"></a><span data-ttu-id="255ef-204">Blob 삭제</span><span class="sxs-lookup"><span data-stu-id="255ef-204">Delete a blob</span></span>
<span data-ttu-id="255ef-205">마지막으로 Blob을 삭제하려면 **deleteBlob**을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-205">Finally, to delete a blob, call **deleteBlob**.</span></span> <span data-ttu-id="255ef-206">다음 코드 예제에서는 **myblob**이라는 Blob을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-206">The following code example deletes the blob named **myblob**.</span></span>

```nodejs
blobSvc.deleteBlob(containerName, 'myblob', function(error, response){
  if(!error){
    // Blob has been deleted
  }
});
```

## <a name="concurrent-access"></a><span data-ttu-id="255ef-207">동시 액세스</span><span class="sxs-lookup"><span data-stu-id="255ef-207">Concurrent access</span></span>
<span data-ttu-id="255ef-208">여러 클라이언트 또는 여러 프로세스 인스턴스에서 Blob에 대한 동시 액세스를 지원하려면 **ETags** 또는 **임대**를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-208">To support concurrent access to a blob from multiple clients or multiple process instances, you can use **ETags** or **leases**.</span></span>

* <span data-ttu-id="255ef-209">**Etag** - Blob이나 컨테이너를 다른 프로세스에서 수정했는지 감지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-209">**Etag** - provides a way to detect that the blob or container has been modified by another process</span></span>
* <span data-ttu-id="255ef-210">**임대** - Blob에 대해 일정 기간 동안 단독, 갱신 가능, 쓰기 또는 삭제 권한을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-210">**Lease** - provides a way to obtain exclusive, renewable, write or delete access to a blob for a period of time</span></span>

### <a name="etag"></a><span data-ttu-id="255ef-211">ETag</span><span class="sxs-lookup"><span data-stu-id="255ef-211">ETag</span></span>
<span data-ttu-id="255ef-212">ETag는 여러 클라이언트 또는 인스턴스에서 블록 Blob에 또는 페이지 Blob에 동시에 쓰기를 허용해야 하는 경우에 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-212">Use ETags if you need to allow multiple clients or instances to write to the block Blob or page Blob simultaneously.</span></span> <span data-ttu-id="255ef-213">ETag를 사용하면 컨테이너나 Blob을 처음 읽거나 만든 후에 수정되었는지 확인하여 다른 클라이언트나 프로세스에서 커밋된 변경 사항을 덮어쓰는 것을 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-213">The ETag allows you to determine if the container or blob was modified since you initially read or created it, which allows you to avoid overwriting changes committed by another client or process.</span></span>

<span data-ttu-id="255ef-214">ETag 조건은 선택적인 `options.accessConditions` 매개 변수를 사용하여 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-214">You can set ETag conditions by using the optional `options.accessConditions` parameter.</span></span> <span data-ttu-id="255ef-215">다음 코드 예제에서는 Blob이 이미 존재하고 `etagToMatch`에 포함된 ETag 값이 있는 경우에만 **test.txt** 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-215">The following code example only uploads the **test.txt** file if the blob already exists and has the ETag value contained by `etagToMatch`.</span></span>

```nodejs
blobSvc.createBlockBlobFromLocalFile('mycontainer', 'myblob', 'test.txt', { accessConditions: { EtagMatch: etagToMatch} }, function(error, result, response){
    if(!error){
    // file uploaded
  }
});
```

<span data-ttu-id="255ef-216">ETag를 사용하는 경우 일반적인 패턴:</span><span class="sxs-lookup"><span data-stu-id="255ef-216">When you're using ETags, the general pattern is:</span></span>

1. <span data-ttu-id="255ef-217">create, list 또는 get 작업의 결과로 ETag를 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-217">Obtain the ETag as the result of a create, list, or get operation.</span></span>
2. <span data-ttu-id="255ef-218">ETag 값이 수정되지 않은 것을 확인하며 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-218">Perform an action, checking that the ETag value has not been modified.</span></span>

<span data-ttu-id="255ef-219">값이 수정되지 않았다면 ETag 값을 얻은 후로 다른 클라이언트 또는 인스턴스에서 Blob이나 컨테이너를 수정한 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-219">If the value was modified, this indicates that another client or instance modified the blob or container since you obtained the ETag value.</span></span>

### <a name="lease"></a><span data-ttu-id="255ef-220">임대</span><span class="sxs-lookup"><span data-stu-id="255ef-220">Lease</span></span>
<span data-ttu-id="255ef-221">**acquireLease** 메서드를 사용하여 임대를 받을 Blob 또는 컨테이너를 지정하면 새 임대를 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-221">You can acquire a new lease by using the **acquireLease** method, specifying the blob or container that you wish to obtain a lease on.</span></span> <span data-ttu-id="255ef-222">예를 들어 다음 코드에서는 **myblob**에 임대를 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-222">For example, the following code acquires a lease on **myblob**.</span></span>

```nodejs
blobSvc.acquireLease('mycontainer', 'myblob', function(error, result, response){
  if(!error) {
    console.log('leaseId: ' + result.id);
  }
});
```

<span data-ttu-id="255ef-223">**myblob**의 후속 작업에서는 `options.leaseId` 매개 변수를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-223">Subsequent operations on **myblob** must provide the `options.leaseId` parameter.</span></span> <span data-ttu-id="255ef-224">임대 ID는 **acquireLease**에서 `result.id`로 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-224">The lease ID is returned as `result.id` from **acquireLease**.</span></span>

> [!NOTE]
> <span data-ttu-id="255ef-225">기본적으로 임대 기간은 무한입니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-225">By default, the lease duration is infinite.</span></span> <span data-ttu-id="255ef-226">15초에서 60초까지의 유한한 기간을 지정하려면 `options.leaseDuration` 매개 변수를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-226">You can specify a non-infinite duration (between 15 and 60 seconds) by providing the `options.leaseDuration` parameter.</span></span>
>
>

<span data-ttu-id="255ef-227">임대를 제거하려면 **releaseLease**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-227">To remove a lease, use **releaseLease**.</span></span> <span data-ttu-id="255ef-228">임대를 중단하면서 원래 기간이 만료될 때까지 다른 사람이 새 임대를 얻지 못하게 하려면 **breakLease**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-228">To break a lease, but prevent others from obtaining a new lease until the original duration has expired, use **breakLease**.</span></span>

## <a name="work-with-shared-access-signatures"></a><span data-ttu-id="255ef-229">공유 액세스 서명 작업</span><span class="sxs-lookup"><span data-stu-id="255ef-229">Work with shared access signatures</span></span>
<span data-ttu-id="255ef-230">SAS(공유 액세스 서명)는 저장소 계정 이름이나 키를 제공하지 않으면서 Blob 및 컨테이너에 세분화된 액세스 권한을 안전하게 제공하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-230">Shared access signatures (SAS) are a secure way to provide granular access to blobs and containers without providing your storage account name or keys.</span></span> <span data-ttu-id="255ef-231">공유 액세스 서명은 모바일 앱에서 Blob에 액세스하는 경우와 같이 데이터에 대해 제한된 액세스를 제공하는 경우에 자주 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-231">Shared access signatures are often used to provide limited access to your data, such as allowing a mobile app to access blobs.</span></span>

> [!NOTE]
> <span data-ttu-id="255ef-232">Blob에 대해 익명 액세스를 허용할 수도 있지만 공유 액세스 서명에서 더 잘 제어된 액세스를 제공할 수 있으므로 SAS를 생성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-232">While you can also allow anonymous access to blobs, shared access signatures allow you to provide more controlled access, as you must generate the SAS.</span></span>
>
>

<span data-ttu-id="255ef-233">클라우드 기반 서비스와 같이 신뢰할 수 있는 응용 프로그램에서는 **BlobService**의 **generateSharedAccessSignature**를 사용하여 공유 액세스 서명을 생성하고, 이를 모바일 앱과 같은 신뢰할 수 없거나 신뢰가 약한 응용 프로그램에 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-233">A trusted application such as a cloud-based service generates shared access signatures using the **generateSharedAccessSignature** of the **BlobService**, and provides it to an untrusted or semi-trusted application such as a mobile app.</span></span> <span data-ttu-id="255ef-234">공유 액세스 서명은 공유 액세스 서명이 유효한 시작 및 종료 날짜와 공유 액세스 서명 소유자에게 부여되는 액세스 수준을 설명하는 정책을 사용하여 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-234">Shared access signatures are generated using a policy, which describes the start and end dates during which the shared access signatures are valid, as well as the access level granted to the shared access signatures holder.</span></span>

<span data-ttu-id="255ef-235">다음 코드 예제에서는 공유 액세스 서명 소유자가 **myblob** Blob에서 읽기 작업을 수행할 수 있도록 허용하며 만든 후 100분이 지나면 만료되는 새 공유 액세스 정책을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-235">The following code example generates a new shared access policy that allows the shared access signatures holder to perform read operations on the **myblob** blob, and expires 100 minutes after the time it is created.</span></span>

```nodejs
var startDate = new Date();
var expiryDate = new Date(startDate);
expiryDate.setMinutes(startDate.getMinutes() + 100);
startDate.setMinutes(startDate.getMinutes() - 100);

var sharedAccessPolicy = {
  AccessPolicy: {
    Permissions: azure.BlobUtilities.SharedAccessPermissions.READ,
    Start: startDate,
    Expiry: expiryDate
  },
};

var blobSAS = blobSvc.generateSharedAccessSignature('mycontainer', 'myblob', sharedAccessPolicy);
var host = blobSvc.host;
```

<span data-ttu-id="255ef-236">공유 액세스 서명 소유자가 컨테이너에 액세스할 때 필요하므로 호스트 정보도 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-236">Note that the host information must be provided also, as it is required when the shared access signatures holder attempts to access the container.</span></span>

<span data-ttu-id="255ef-237">그러고 나면 클라이언트 응용 프로그램에서 **BlobServiceWithSAS** 에 공유 액세스 서명을 사용하여 Blob에 대한 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-237">The client application then uses shared access signatures with **BlobServiceWithSAS** to perform operations against the blob.</span></span> <span data-ttu-id="255ef-238">다음에서는 **myblob**에 대한 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-238">The following gets information about **myblob**.</span></span>

```nodejs
var sharedBlobSvc = azure.createBlobServiceWithSas(host, blobSAS);
sharedBlobSvc.getBlobProperties('mycontainer', 'myblob', function (error, result, response) {
  if(!error) {
    // retrieved info
  }
});
```

<span data-ttu-id="255ef-239">Blob를 수정하려고 하는 경우 공유 액세스 서명이 읽기 전용 액세스로 생성되었으므로 오류가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-239">Since the shared access signatures were generated with read-only access, if an attempt is made to modify the blob, an error will be returned.</span></span>

### <a name="access-control-lists"></a><span data-ttu-id="255ef-240">액세스 제어 목록</span><span class="sxs-lookup"><span data-stu-id="255ef-240">Access control lists</span></span>
<span data-ttu-id="255ef-241">ACL(액세스 제어 목록)을 사용하여 SAS에 액세스 정책을 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-241">You can also use an access control list (ACL) to set the access policy for SAS.</span></span> <span data-ttu-id="255ef-242">이 방법은 여러 클라이언트에서 컨테이너에 액세스하게 하면서 각 클라이언트에 서로 다른 액세스 정책을 제공하려는 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-242">This is useful if you wish to allow multiple clients to access a container but provide different access policies for each client.</span></span>

<span data-ttu-id="255ef-243">ACL은 각 정책에 ID가 연결된 액세스 정책 배열을 사용하여 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-243">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span></span> <span data-ttu-id="255ef-244">다음 코드 예제에서는 'user1'와 'user2'에 대해 하나씩, 두 개의 정책을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-244">The following code example defines two policies, one for 'user1' and one for 'user2':</span></span>

```nodejs
var sharedAccessPolicy = {
  user1: {
    Permissions: azure.BlobUtilities.SharedAccessPermissions.READ,
    Start: startDate,
    Expiry: expiryDate
  },
  user2: {
    Permissions: azure.BlobUtilities.SharedAccessPermissions.WRITE,
    Start: startDate,
    Expiry: expiryDate
  }
};
```

<span data-ttu-id="255ef-245">다음 코드 예제에서는 **mycontainer**에 대한 현재 ACL을 가져온 다음 **setBlobAcl**을 사용하여 새 정책을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-245">The following code example gets the current ACL for **mycontainer**, and then adds the new policies using **setBlobAcl**.</span></span> <span data-ttu-id="255ef-246">이 접근 방식을 통해 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-246">This approach allows:</span></span>

```nodejs
var extend = require('extend');
blobSvc.getBlobAcl('mycontainer', function(error, result, response) {
  if(!error){
    var newSignedIdentifiers = extend(true, result.signedIdentifiers, sharedAccessPolicy);
    blobSvc.setBlobAcl('mycontainer', newSignedIdentifiers, function(error, result, response){
      if(!error){
        // ACL set
      }
    });
  }
});
```

<span data-ttu-id="255ef-247">ACL이 설정되고 나면 정책의 ID를 기반으로 공유 액세스 서명을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-247">Once the ACL is set, you can then create shared access signatures based on the ID for a policy.</span></span> <span data-ttu-id="255ef-248">다음 코드 예제에서는 ‘user2'에 대한 새 공유 액세스 서명을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="255ef-248">The following code example creates new shared access signatures for 'user2':</span></span>

```nodejs
blobSAS = blobSvc.generateSharedAccessSignature('mycontainer', { Id: 'user2' });
```

## <a name="next-steps"></a><span data-ttu-id="255ef-249">다음 단계</span><span class="sxs-lookup"><span data-stu-id="255ef-249">Next steps</span></span>
<span data-ttu-id="255ef-250">자세한 내용은 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="255ef-250">For more information, see the following resources.</span></span>

* <span data-ttu-id="255ef-251">[Node용 Azure Storage SDK API 참조][Node용 Azure Storage SDK API 참조]</span><span class="sxs-lookup"><span data-stu-id="255ef-251">[Azure Storage SDK for Node API Reference][Azure Storage SDK for Node API Reference]</span></span>
* <span data-ttu-id="255ef-252">[Azure Storage 팀 블로그][Azure Storage 팀 블로그]</span><span class="sxs-lookup"><span data-stu-id="255ef-252">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>
* <span data-ttu-id="255ef-253">GitHub의 [Azure Storage SDK for Node][Azure Storage SDK for Node] 리포지토리</span><span class="sxs-lookup"><span data-stu-id="255ef-253">[Azure Storage SDK for Node][Azure Storage SDK for Node] repository on GitHub</span></span>
* [<span data-ttu-id="255ef-254">Node.js 개발자 센터</span><span class="sxs-lookup"><span data-stu-id="255ef-254">Node.js Developer Center</span></span>](https://azure.microsoft.com/develop/nodejs/)
* [<span data-ttu-id="255ef-255">AzCopy 명령줄 유틸리티로 데이터 전송</span><span class="sxs-lookup"><span data-stu-id="255ef-255">Transfer data with the AzCopy command-line utility</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

[Azure Storage SDK for Node]: https://github.com/Azure/azure-storage-node

<span data-ttu-id="255ef-256">[Azure Table Service를 사용하는 Node.js 웹앱](../../app-service-web/storage-nodejs-use-table-storage-web-site.md)  </span><span class="sxs-lookup"><span data-stu-id="255ef-256">[Node.js web app using the Azure Table Service](../../app-service-web/storage-nodejs-use-table-storage-web-site.md)  </span></span>  
<span data-ttu-id="255ef-257">[Web Matrix를 사용하여 Azure에 Node.js 웹앱 빌드 및 배포]: https://www.microsoft.com/web/webmatrix/</span><span class="sxs-lookup"><span data-stu-id="255ef-257">[Build and deploy a Node.js web app to Azure using Web Matrix]: https://www.microsoft.com/web/webmatrix/</span></span>  
<span data-ttu-id="255ef-258">[REST API 사용]: http://msdn.microsoft.com/library/azure/hh264518.aspx [Azure Portal]: https://portal.azure.com [Azure Cloud Service에 Node.js 응용 프로그램 빌드 및 배포](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) [Azure Storage 팀 블로그]: http://blogs.msdn.com/b/windowsazurestorage/ [Node용 Azure Storage SDK API 참조]: http://dl.windowsazure.com/nodestoragedocs/index.html</span><span class="sxs-lookup"><span data-stu-id="255ef-258">[Using the REST API]: http://msdn.microsoft.com/library/azure/hh264518.aspx [Azure portal]: https://portal.azure.com [Build and deploy a Node.js application to an Azure Cloud Service](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) [Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/ [Azure Storage SDK for Node API Reference]: http://dl.windowsazure.com/nodestoragedocs/index.html</span></span>

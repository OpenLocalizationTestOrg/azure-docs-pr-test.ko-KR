---
title: "Node.js에서 Blob 저장소 aaaHow toouse | Microsoft Docs"
description: "Azure Blob 저장소 (개체 저장소)를 사용 하는 hello 클라우드에 구조화 되지 않은 데이터를 저장 합니다."
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
ms.openlocfilehash: 572e7fc9f7b19ff01720a7cadd495c809ed49fb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-nodejs"></a><span data-ttu-id="10987-103">어떻게 toouse Node.js에서 Blob 저장소</span><span class="sxs-lookup"><span data-stu-id="10987-103">How toouse Blob storage from Node.js</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-all](../../../includes/storage-check-out-samples-all.md)]

## <a name="overview"></a><span data-ttu-id="10987-104">개요</span><span class="sxs-lookup"><span data-stu-id="10987-104">Overview</span></span>
<span data-ttu-id="10987-105">이 문서에서는 Blob 저장소를 사용 하 여 tooperform 일반적인 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="10987-105">This article shows you how tooperform common scenarios using Blob storage.</span></span> <span data-ttu-id="10987-106">hello 샘플 hello Node.js API를 통해 작성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="10987-106">hello samples are written via hello Node.js API.</span></span> <span data-ttu-id="10987-107">가이드에서 다루는 hello 시나리오 tooupload를 나열, 다운로드 및 blob 삭제 방법을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="10987-107">hello scenarios covered include how tooupload, list, download, and delete blobs.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="10987-108">Node.js 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="10987-108">Create a Node.js application</span></span>
<span data-ttu-id="10987-109">방법에 대 한 지침은 toocreate는 Node.js 응용 프로그램 참조 [Azure 앱 서비스에서 Node.js 웹 앱 만들기] [빌드하고 Node.js 응용 프로그램 tooan Azure 클라우드 서비스 배포](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) -Windows PowerShell을 사용 하 여 또는 [빌드 및 웹 매트릭스를 사용 하는 Node.js 웹 응용 프로그램 tooAzure 배포](https://www.microsoft.com/web/webmatrix/)합니다.</span><span class="sxs-lookup"><span data-stu-id="10987-109">For instructions on how toocreate a Node.js application, see [Create a Node.js web app in Azure App Service], [Build and deploy a Node.js application tooan Azure Cloud Service](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) -- using Windows PowerShell, or [Build and deploy a Node.js web app tooAzure using Web Matrix](https://www.microsoft.com/web/webmatrix/).</span></span>

## <a name="configure-your-application-tooaccess-storage"></a><span data-ttu-id="10987-110">응용 프로그램 tooaccess 저장소 구성</span><span class="sxs-lookup"><span data-stu-id="10987-110">Configure your application tooaccess storage</span></span>
<span data-ttu-id="10987-111">Azure 저장소 toouse hello 저장소 REST 서비스와 통신 하는 편리한 라이브러리의 집합을 포함 하는 Node.js 용 hello Azure 저장소 SDK 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10987-111">toouse Azure storage, you need hello Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a><span data-ttu-id="10987-112">노드 패키지 관리자 (NPM) tooobtain hello 패키지 사용</span><span class="sxs-lookup"><span data-stu-id="10987-112">Use Node Package Manager (NPM) tooobtain hello package</span></span>
1. <span data-ttu-id="10987-113">와 같은 명령줄 인터페이스를 사용 하 여 **PowerShell** (Windows) **터미널** (Mac) 또는 **를 이용한 적** (Unix) 샘플을 만들었으므로 toonavigate toohello 폴더 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="10987-113">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix), toonavigate toohello folder where you created your sample application.</span></span>
2. <span data-ttu-id="10987-114">형식 **npm 설치 azure storage** hello 명령 창에서.</span><span class="sxs-lookup"><span data-stu-id="10987-114">Type **npm install azure-storage** in hello command window.</span></span> <span data-ttu-id="10987-115">Hello 명령 출력은 다음 코드 예제와 비슷한 toohello입니다.</span><span class="sxs-lookup"><span data-stu-id="10987-115">Output from hello command is similar toohello following code example.</span></span>

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
3. <span data-ttu-id="10987-116">Hello를 수동으로 실행할 수 있습니다 **ls** 명령 tooverify 하는 **노드\_모듈** 폴더를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="10987-116">You can manually run hello **ls** command tooverify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="10987-117">해당 폴더 내의 hello 찾습니다 **azure 저장소** tooaccess 저장 해야 하는 hello 라이브러리를 포함 하는 패키지입니다.</span><span class="sxs-lookup"><span data-stu-id="10987-117">Inside that folder, find hello **azure-storage** package, which contains hello libraries that you need tooaccess storage.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="10987-118">Hello 패키지 가져오기</span><span class="sxs-lookup"><span data-stu-id="10987-118">Import hello package</span></span>
<span data-ttu-id="10987-119">메모장 이나 다른 텍스트 편집기를 사용 하 여 추가 hello toohello 맨 뒤 hello **server.js** toouse 저장소 이점을 얻을 수 hello 응용 프로그램의 파일:</span><span class="sxs-lookup"><span data-stu-id="10987-119">Using Notepad or another text editor, add hello following toohello top of hello **server.js** file of hello application where you intend toouse storage:</span></span>

```nodejs
var azure = require('azure-storage');
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="10987-120">Azure 저장소 연결 설정</span><span class="sxs-lookup"><span data-stu-id="10987-120">Set up an Azure Storage connection</span></span>
<span data-ttu-id="10987-121">hello Azure 모듈 읽힙니다 hello 환경 변수 `AZURE_STORAGE_ACCOUNT` 및 `AZURE_STORAGE_ACCESS_KEY`, 또는 `AZURE_STORAGE_CONNECTION_STRING`, 필요한 tooconnect tooyour Azure 저장소 계정 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="10987-121">hello Azure module will read hello environment variables `AZURE_STORAGE_ACCOUNT` and `AZURE_STORAGE_ACCESS_KEY`, or `AZURE_STORAGE_CONNECTION_STRING`, for information required tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="10987-122">호출할 때 hello 계정 정보를 지정 해야 이러한 환경 변수가 설정 되지 않은 경우 **createBlobService**합니다.</span><span class="sxs-lookup"><span data-stu-id="10987-122">If these environment variables are not set, you must specify hello account information when calling **createBlobService**.</span></span>

<span data-ttu-id="10987-123">Hello에 hello 환경 변수 설정에 대 한 예제 [Azure 포털](https://portal.azure.com) 는 Azure 웹 앱에 대 한 참조 [Azure 테이블 서비스 hello 사용 하 여 Node.js 웹 응용 프로그램](../../app-service-web/storage-nodejs-use-table-storage-web-site.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="10987-123">For an example of setting hello environment variables in hello [Azure portal](https://portal.azure.com) for an Azure web app, see [Node.js web app using hello Azure Table Service](../../app-service-web/storage-nodejs-use-table-storage-web-site.md).</span></span>

## <a name="create-a-container"></a><span data-ttu-id="10987-124">컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="10987-124">Create a container</span></span>
<span data-ttu-id="10987-125">hello **BlobService** 개체 컨테이너 및 blob를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10987-125">hello **BlobService** object lets you work with containers and blobs.</span></span> <span data-ttu-id="10987-126">hello 다음 코드에서는 **BlobService** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="10987-126">hello following code creates a **BlobService** object.</span></span> <span data-ttu-id="10987-127">hello 위쪽 hello 다음 추가 **server.js**:</span><span class="sxs-lookup"><span data-stu-id="10987-127">Add hello following near hello top of **server.js**:</span></span>

```nodejs
var blobSvc = azure.createBlobService();
```

> [!NOTE]
> <span data-ttu-id="10987-128">사용 하 여 blob을 익명으로 액세스할 수 있습니다 **createBlobServiceAnonymous** hello 호스트 주소를 제공 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10987-128">You can access a blob anonymously by using **createBlobServiceAnonymous** and providing hello host address.</span></span> <span data-ttu-id="10987-129">예를 들면 `var blobSvc = azure.createBlobServiceAnonymous('https://myblob.blob.core.windows.net/');`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="10987-129">For example, use `var blobSvc = azure.createBlobServiceAnonymous('https://myblob.blob.core.windows.net/');`.</span></span>
>
>

[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="10987-130">toocreate 새 컨테이너를 사용 하 여 **createContainerIfNotExists**합니다.</span><span class="sxs-lookup"><span data-stu-id="10987-130">toocreate a new container, use **createContainerIfNotExists**.</span></span> <span data-ttu-id="10987-131">hello 다음 코드 예제에서는 'mycontainer' 라는 새 컨테이너:</span><span class="sxs-lookup"><span data-stu-id="10987-131">hello following code example creates a new container named 'mycontainer':</span></span>

```nodejs
blobSvc.createContainerIfNotExists('mycontainer', function(error, result, response){
    if(!error){
      // Container exists and is private
    }
});
```

<span data-ttu-id="10987-132">Hello 컨테이너를 새로 작성 하는 경우 `result.created` 그렇습니다.</span><span class="sxs-lookup"><span data-stu-id="10987-132">If hello container is newly created, `result.created` is true.</span></span> <span data-ttu-id="10987-133">Hello 컨테이너에 이미 있으면 `result.created` 은 false입니다.</span><span class="sxs-lookup"><span data-stu-id="10987-133">If hello container already exists, `result.created` is false.</span></span> <span data-ttu-id="10987-134">`response`hello 컨테이너에 대 한 hello ETag 정보를 포함 하는 hello 작업에 대 한 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="10987-134">`response` contains information about hello operation, including hello ETag information for hello container.</span></span>

### <a name="container-security"></a><span data-ttu-id="10987-135">컨테이너 보안</span><span class="sxs-lookup"><span data-stu-id="10987-135">Container security</span></span>
<span data-ttu-id="10987-136">기본적으로 새 컨테이너는 개인 컨테이너이며 익명으로 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="10987-136">By default, new containers are private and cannot be accessed anonymously.</span></span> <span data-ttu-id="10987-137">익명으로 액세스할 수 있도록 공용 toomake hello 컨테이너 설정할 수 있습니다 hello 컨테이너의 액세스 수준을 너무**blob** 또는 **컨테이너**합니다.</span><span class="sxs-lookup"><span data-stu-id="10987-137">toomake hello container public so that you can access it anonymously, you can set hello container's access level too**blob** or **container**.</span></span>

* <span data-ttu-id="10987-138">**blob** -익명 읽기 권한을 tooblob 콘텐츠 및이 컨테이너에 있는 메타 데이터는 있지만 하지 toocontainer 등의 메타 데이터 컨테이너 내 모든 blob을 나열 허용</span><span class="sxs-lookup"><span data-stu-id="10987-138">**blob** - allows anonymous read access tooblob content and metadata within this container, but not toocontainer metadata such as listing all blobs within a container</span></span>
* <span data-ttu-id="10987-139">**컨테이너** -익명 읽기 권한을 tooblob 콘텐츠 및 메타 데이터 뿐 아니라 컨테이너 메타 데이터를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="10987-139">**container** - allows anonymous read access tooblob content and metadata as well as container metadata</span></span>

<span data-ttu-id="10987-140">hello 다음 코드 예제에서는 hello 액세스 수준을 설정 너무**blob**:</span><span class="sxs-lookup"><span data-stu-id="10987-140">hello following code example demonstrates setting hello access level too**blob**:</span></span>

```nodejs
blobSvc.createContainerIfNotExists('mycontainer', {publicAccessLevel : 'blob'}, function(error, result, response){
    if(!error){
      // Container exists and allows
      // anonymous read access tooblob
      // content and metadata within this container
    }
});
```

<span data-ttu-id="10987-141">컨테이너의 액세스 수준을 hello를 사용 하 여 수정할 수 있습니다 또는 **setContainerAcl** toospecify hello 액세스 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="10987-141">Alternatively, you can modify hello access level of a container by using **setContainerAcl** toospecify hello access level.</span></span> <span data-ttu-id="10987-142">hello 다음 코드 예제에서는 변경 내용을 hello 액세스 수준 toocontainer:</span><span class="sxs-lookup"><span data-stu-id="10987-142">hello following code example changes hello access level toocontainer:</span></span>

```nodejs
blobSvc.setContainerAcl('mycontainer', null /* signedIdentifiers */, {publicAccessLevel : 'container'} /* publicAccessLevel*/, function(error, result, response){
  if(!error){
    // Container access level set too'container'
  }
});
```

<span data-ttu-id="10987-143">hello 결과 대 한 정보가 hello 현재 포함 하는 hello 작업 **ETag** hello 컨테이너에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="10987-143">hello result contains information about hello operation, including hello current **ETag** for hello container.</span></span>

### <a name="filters"></a><span data-ttu-id="10987-144">필터</span><span class="sxs-lookup"><span data-stu-id="10987-144">Filters</span></span>
<span data-ttu-id="10987-145">선택적 작업 수행 toooperations 사용 하는 필터를 적용할 수 있습니다 **BlobService**합니다.</span><span class="sxs-lookup"><span data-stu-id="10987-145">You can apply optional filtering operations toooperations performed using **BlobService**.</span></span> <span data-ttu-id="10987-146">필터링 작업은 로깅, 자동 재시도 등을 포함할 수 있습니다. 필터는 hello 서명으로 메서드를 구현 하는 개체:</span><span class="sxs-lookup"><span data-stu-id="10987-146">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with hello signature:</span></span>

```nodejs
function handle (requestOptions, next)
```

<span data-ttu-id="10987-147">Hello 요청 옵션에 전처리를 수행한 후 hello 메서드는 toocall "다음" 필요 콜백을 뒤 서명에 hello로 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="10987-147">After doing its preprocessing on hello request options, hello method needs toocall "next", passing a callback with hello following signature:</span></span>

```nodejs
function (returnObject, finalCallback, next)
```

<span data-ttu-id="10987-148">이 콜백에서 hello returnObject (hello toohello 서버 요청에서에서 응답 hello)를 처리 한 후, hello 콜백 필요 tooeither 단순히 finalCallback tooend hello 서비스를 호출 하거나 다른 필터를 처리 하는 toocontinue 있는 경우 다음에 호출할 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="10987-148">In this callback, and after processing hello returnObject (hello response from hello request toohello server), hello callback needs tooeither invoke next if it exists toocontinue processing other filters or simply invoke finalCallback tooend hello service invocation.</span></span>

<span data-ttu-id="10987-149">재시도 논리를 구현 하는 두 개의 필터 hello Node.js 용 Azure SDK에 포함 된 **ExponentialRetryPolicyFilter** 및 **LinearRetryPolicyFilter**합니다.</span><span class="sxs-lookup"><span data-stu-id="10987-149">Two filters that implement retry logic are included with hello Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="10987-150">hello 다음 만듭니다는 **BlobService** hello를 사용 하는 개체 **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="10987-150">hello following creates a **BlobService** object that uses hello **ExponentialRetryPolicyFilter**:</span></span>

```nodejs
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var blobSvc = azure.createBlobService().withFilter(retryOperations);
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="10987-151">컨테이너에 Blob 업로드</span><span class="sxs-lookup"><span data-stu-id="10987-151">Upload a blob into a container</span></span>
<span data-ttu-id="10987-152">블록 Blob, 페이지 Blob 및 추가 Blob의 세 가지 Blob 유형이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10987-152">There are three types of blobs: block blobs, page blobs and append blobs.</span></span> <span data-ttu-id="10987-153">블록 blob를 사용 하면 toomore 효율적으로 큰 데이터를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="10987-153">Block blobs allow you toomore efficiently upload large data.</span></span> <span data-ttu-id="10987-154">추가 Blob은 추가 작업에 최적화되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10987-154">Append blobs are optimized for append operations.</span></span> <span data-ttu-id="10987-155">페이지 Blob은 읽기/쓰기 작업에 최적화되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10987-155">Page blobs are optimized for read/write operations.</span></span> <span data-ttu-id="10987-156">자세한 내용은 [블록 Blob, 추가 Blob 및 페이지 Blob 이해](http://msdn.microsoft.com/library/azure/ee691964.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="10987-156">For more information, see [Understanding Block Blobs, Append Blobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span></span>

### <a name="block-blobs"></a><span data-ttu-id="10987-157">블록 Blob</span><span class="sxs-lookup"><span data-stu-id="10987-157">Block blobs</span></span>
<span data-ttu-id="10987-158">tooupload 데이터 tooa 블록 blob을 사용 하 여 hello 다음:</span><span class="sxs-lookup"><span data-stu-id="10987-158">tooupload data tooa block blob, use hello following:</span></span>

* <span data-ttu-id="10987-159">**createBlockBlobFromLocalFile** -새 블록 blob를 만들고 업로드 된 파일의 내용을 hello</span><span class="sxs-lookup"><span data-stu-id="10987-159">**createBlockBlobFromLocalFile** - creates a new block blob and uploads hello contents of a file</span></span>
* <span data-ttu-id="10987-160">**createBlockBlobFromStream** -새 블록 blob를 만들고 stream의 hello 내용 업로드</span><span class="sxs-lookup"><span data-stu-id="10987-160">**createBlockBlobFromStream** - creates a new block blob and uploads hello contents of a stream</span></span>
* <span data-ttu-id="10987-161">**createBlockBlobFromText** -새 블록 blob를 만들고 문자열의 내용을 hello 업로드</span><span class="sxs-lookup"><span data-stu-id="10987-161">**createBlockBlobFromText** - creates a new block blob and uploads hello contents of a string</span></span>
* <span data-ttu-id="10987-162">**createWriteStreamToBlockBlob** -쓰기 스트림을 tooa 블록 blob를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="10987-162">**createWriteStreamToBlockBlob** - provides a write stream tooa block blob</span></span>

<span data-ttu-id="10987-163">hello 다음 코드 예제에서는 업로드 hello 내용의 hello **test.txt** 파일 **myblob**합니다.</span><span class="sxs-lookup"><span data-stu-id="10987-163">hello following code example uploads hello contents of hello **test.txt** file into **myblob**.</span></span>

```nodejs
blobSvc.createBlockBlobFromLocalFile('mycontainer', 'myblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

<span data-ttu-id="10987-164">hello `result` 이러한 메서드에 의해 반환 된 hello 등 hello 작업에 대 한 정보 **ETag** hello blob의 합니다.</span><span class="sxs-lookup"><span data-stu-id="10987-164">hello `result` returned by these methods contains information on hello operation, such as hello **ETag** of hello blob.</span></span>

### <a name="append-blobs"></a><span data-ttu-id="10987-165">추가 Blob</span><span class="sxs-lookup"><span data-stu-id="10987-165">Append blobs</span></span>
<span data-ttu-id="10987-166">tooupload 데이터 tooa 새 blob을 추가, hello 다음을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="10987-166">tooupload data tooa new append blob, use hello following:</span></span>

* <span data-ttu-id="10987-167">**createAppendBlobFromLocalFile** -새 blob를 만들고 업로드 된 파일의 내용을 hello</span><span class="sxs-lookup"><span data-stu-id="10987-167">**createAppendBlobFromLocalFile** - creates a new append blob and uploads hello contents of a file</span></span>
* <span data-ttu-id="10987-168">**createAppendBlobFromStream** -새 blob를 만들고 stream의 hello 내용 업로드</span><span class="sxs-lookup"><span data-stu-id="10987-168">**createAppendBlobFromStream** - creates a new append blob and uploads hello contents of a stream</span></span>
* <span data-ttu-id="10987-169">**createAppendBlobFromText** -새 blob를 만들고 문자열의 내용을 hello 업로드</span><span class="sxs-lookup"><span data-stu-id="10987-169">**createAppendBlobFromText** - creates a new append blob and uploads hello contents of a string</span></span>
* <span data-ttu-id="10987-170">**createWriteStreamToNewAppendBlob** -새 blob 키를 만들고 다음 스트림 toowrite tooit 제공</span><span class="sxs-lookup"><span data-stu-id="10987-170">**createWriteStreamToNewAppendBlob** - creates a new append blob and then provides a stream toowrite tooit</span></span>

<span data-ttu-id="10987-171">hello 다음 코드 예제에서는 업로드 hello 내용의 hello **test.txt** 파일 **myappendblob**합니다.</span><span class="sxs-lookup"><span data-stu-id="10987-171">hello following code example uploads hello contents of hello **test.txt** file into **myappendblob**.</span></span>

```nodejs
blobSvc.createAppendBlobFromLocalFile('mycontainer', 'myappendblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

<span data-ttu-id="10987-172">tooappend 블록 tooan 기존 blob의 경우 다음 사용 하 여 hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="10987-172">tooappend a block tooan existing append blob, use hello following:</span></span>

* <span data-ttu-id="10987-173">**appendFromLocalFile** -hello 내용을 추가 합니다. 기존 파일 tooan의 blob 추가</span><span class="sxs-lookup"><span data-stu-id="10987-173">**appendFromLocalFile** - append hello contents of a file tooan existing append blob</span></span>
* <span data-ttu-id="10987-174">**appendFromStream** -hello 내용을 추가할 추가 blob를 기존 스트림에 tooan의</span><span class="sxs-lookup"><span data-stu-id="10987-174">**appendFromStream** - append hello contents of a stream tooan existing append blob</span></span>
* <span data-ttu-id="10987-175">**appendFromText** -hello 내용을 추가 하는 문자열 tooan의 blob를 추가할 기존</span><span class="sxs-lookup"><span data-stu-id="10987-175">**appendFromText** - append hello contents of a string tooan existing append blob</span></span>
* <span data-ttu-id="10987-176">**appendBlockFromStream** -hello 내용을 추가할 추가 blob를 기존 스트림에 tooan의</span><span class="sxs-lookup"><span data-stu-id="10987-176">**appendBlockFromStream** - append hello contents of a stream tooan existing append blob</span></span>
* <span data-ttu-id="10987-177">**appendBlockFromText** -hello 내용을 추가 하는 문자열 tooan의 blob를 추가할 기존</span><span class="sxs-lookup"><span data-stu-id="10987-177">**appendBlockFromText** - append hello contents of a string tooan existing append blob</span></span>

> [!NOTE]
> <span data-ttu-id="10987-178">appendFromXXX Api는 일부 클라이언트 쪽 유효성 검사 toofail 빠른 tooavoid 불필요 한 서버 호출을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="10987-178">appendFromXXX APIs will do some client-side validation toofail fast tooavoid unnecessary server calls.</span></span> <span data-ttu-id="10987-179">appendBlockFromXXX는 이를 수행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="10987-179">appendBlockFromXXX won't.</span></span>
>
>

<span data-ttu-id="10987-180">hello 다음 코드 예제에서는 업로드 hello 내용의 hello **test.txt** 파일 **myappendblob**합니다.</span><span class="sxs-lookup"><span data-stu-id="10987-180">hello following code example uploads hello contents of hello **test.txt** file into **myappendblob**.</span></span>

```nodejs
blobSvc.appendFromText('mycontainer', 'myappendblob', 'text toobe appended', function(error, result, response){
  if(!error){
    // text appended
  }
});
```

### <a name="page-blobs"></a><span data-ttu-id="10987-181">페이지 Blob</span><span class="sxs-lookup"><span data-stu-id="10987-181">Page blobs</span></span>
<span data-ttu-id="10987-182">tooupload 데이터 tooa 페이지 blob의 경우 다음 사용 하 여 hello:</span><span class="sxs-lookup"><span data-stu-id="10987-182">tooupload data tooa page blob, use hello following:</span></span>

* <span data-ttu-id="10987-183">**createPageBlob** - 특정 길이의 새 페이지 Blob을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="10987-183">**createPageBlob** - creates a new page blob of a specific length</span></span>
* <span data-ttu-id="10987-184">**createPageBlobFromLocalFile** -새 페이지 blob를 만들고 업로드 된 파일의 내용을 hello</span><span class="sxs-lookup"><span data-stu-id="10987-184">**createPageBlobFromLocalFile** - creates a new page blob and uploads hello contents of a file</span></span>
* <span data-ttu-id="10987-185">**createPageBlobFromStream** -새 페이지 blob를 만들고 stream의 hello 내용 업로드</span><span class="sxs-lookup"><span data-stu-id="10987-185">**createPageBlobFromStream** - creates a new page blob and uploads hello contents of a stream</span></span>
* <span data-ttu-id="10987-186">**createWriteStreamToExistingPageBlob** -쓰기 스트림을 tooan 기존 페이지 blob를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="10987-186">**createWriteStreamToExistingPageBlob** - provides a write stream tooan existing page blob</span></span>
* <span data-ttu-id="10987-187">**createWriteStreamToNewPageBlob** -새 페이지 blob를 만들고 스트림 toowrite tooit를 제공 합니다</span><span class="sxs-lookup"><span data-stu-id="10987-187">**createWriteStreamToNewPageBlob** - creates a new page blob and then provides a stream toowrite tooit</span></span>

<span data-ttu-id="10987-188">hello 다음 코드 예제에서는 업로드 hello 내용의 hello **test.txt** 파일 **mypageblob**합니다.</span><span class="sxs-lookup"><span data-stu-id="10987-188">hello following code example uploads hello contents of hello **test.txt** file into **mypageblob**.</span></span>

```nodejs
blobSvc.createPageBlobFromLocalFile('mycontainer', 'mypageblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

> [!NOTE]
> <span data-ttu-id="10987-189">페이지 Bobl은 512바이트의 '페이지'로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="10987-189">Page blobs consist of 512-byte 'pages'.</span></span> <span data-ttu-id="10987-190">크기가 512의 배수가 아닌 경우에는 데이터를 업로드할 때 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="10987-190">You will receive an error when uploading data with a size that is not a multiple of 512.</span></span>
>
>

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="10987-191">컨테이너에서 hello blob 나열</span><span class="sxs-lookup"><span data-stu-id="10987-191">List hello blobs in a container</span></span>
<span data-ttu-id="10987-192">toolist hello blob 컨테이너에서 hello를 사용 하 여 **listBlobsSegmented** 메서드.</span><span class="sxs-lookup"><span data-stu-id="10987-192">toolist hello blobs in a container, use hello **listBlobsSegmented** method.</span></span> <span data-ttu-id="10987-193">사용 하 여 지정 된 접두사로 tooreturn blob를 원하는 경우 **listBlobsSegmentedWithPrefix**합니다.</span><span class="sxs-lookup"><span data-stu-id="10987-193">If you'd like tooreturn blobs with a specific prefix, use **listBlobsSegmentedWithPrefix**.</span></span>

```nodejs
blobSvc.listBlobsSegmented('mycontainer', null, function(error, result, response){
  if(!error){
      // result.entries contains hello entries
      // If not all blobs were returned, result.continuationToken has hello continuation token.
  }
});
```

<span data-ttu-id="10987-194">hello `result` 포함 한 `entries` 컬렉션은 각 blob에 설명 하는 개체의 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="10987-194">hello `result` contains an `entries` collection, which is an array of objects that describe each blob.</span></span> <span data-ttu-id="10987-195">모든 blob를 반환할 수 없는 경우 hello `result` 제공는 `continuationToken`, hello 두 번째 매개 변수 tooretrieve 추가 항목으로 사용할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="10987-195">If all blobs cannot be returned, hello `result` also provides a `continuationToken`, which you may use as hello second parameter tooretrieve additional entries.</span></span>

## <a name="download-blobs"></a><span data-ttu-id="10987-196">Blob 다운로드</span><span class="sxs-lookup"><span data-stu-id="10987-196">Download blobs</span></span>
<span data-ttu-id="10987-197">blob에서 toodownload 데이터 hello 다음을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="10987-197">toodownload data from a blob, use hello following:</span></span>

* <span data-ttu-id="10987-198">**getBlobToLocalFile** -hello blob 내용을 toofile 씁니다.</span><span class="sxs-lookup"><span data-stu-id="10987-198">**getBlobToLocalFile** - writes hello blob contents toofile</span></span>
* <span data-ttu-id="10987-199">**getBlobToStream** -hello blob 내용을 tooa 스트림에 씁니다.</span><span class="sxs-lookup"><span data-stu-id="10987-199">**getBlobToStream** - writes hello blob contents tooa stream</span></span>
* <span data-ttu-id="10987-200">**getBlobToText** -hello blob 콘텐츠가 tooa 문자열을 씁니다.</span><span class="sxs-lookup"><span data-stu-id="10987-200">**getBlobToText** - writes hello blob contents tooa string</span></span>
* <span data-ttu-id="10987-201">**createReadStream** -hello blob에서 스트림 tooread 제공</span><span class="sxs-lookup"><span data-stu-id="10987-201">**createReadStream** - provides a stream tooread from hello blob</span></span>

<span data-ttu-id="10987-202">hello 다음 코드 예제에서는 사용 하 여 **getBlobToStream** toodownload hello 내용의 hello **myblob** blob 및 toohello 저장 **output.txt 라는** 사용 하 여 파일을 스트림:</span><span class="sxs-lookup"><span data-stu-id="10987-202">hello following code example demonstrates using **getBlobToStream** toodownload hello contents of hello **myblob** blob and store it toohello **output.txt** file by using a stream:</span></span>

```nodejs
var fs = require('fs');
blobSvc.getBlobToStream('mycontainer', 'myblob', fs.createWriteStream('output.txt'), function(error, result, response){
  if(!error){
    // blob retrieved
  }
});
```

<span data-ttu-id="10987-203">hello `result` hello blob에 대 한 정보도 포함 하 여 **ETag** 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="10987-203">hello `result` contains information about hello blob, including **ETag** information.</span></span>

## <a name="delete-a-blob"></a><span data-ttu-id="10987-204">Blob 삭제</span><span class="sxs-lookup"><span data-stu-id="10987-204">Delete a blob</span></span>
<span data-ttu-id="10987-205">마지막으로, blob toodelete 호출 **deleteBlob**합니다.</span><span class="sxs-lookup"><span data-stu-id="10987-205">Finally, toodelete a blob, call **deleteBlob**.</span></span> <span data-ttu-id="10987-206">다음 코드 예제에서는 삭제 hello 라는 blob hello **myblob**합니다.</span><span class="sxs-lookup"><span data-stu-id="10987-206">hello following code example deletes hello blob named **myblob**.</span></span>

```nodejs
blobSvc.deleteBlob(containerName, 'myblob', function(error, response){
  if(!error){
    // Blob has been deleted
  }
});
```

## <a name="concurrent-access"></a><span data-ttu-id="10987-207">동시 액세스</span><span class="sxs-lookup"><span data-stu-id="10987-207">Concurrent access</span></span>
<span data-ttu-id="10987-208">사용할 수 있습니다 toosupport 동시 액세스 tooa 여러 클라이언트 또는 여러 프로세스에서 blob, **Etag** 또는 **임대**합니다.</span><span class="sxs-lookup"><span data-stu-id="10987-208">toosupport concurrent access tooa blob from multiple clients or multiple process instances, you can use **ETags** or **leases**.</span></span>

* <span data-ttu-id="10987-209">**Etag** -다른 프로세스에서 수정 했습니다. blob 또는 컨테이너 hello 하는 방식으로 toodetect 제공</span><span class="sxs-lookup"><span data-stu-id="10987-209">**Etag** - provides a way toodetect that hello blob or container has been modified by another process</span></span>
* <span data-ttu-id="10987-210">**임대** -tooobtain 단독, 갱신, 쓰기 방식으로 제공 하거나 일정 기간에 대 한 액세스 tooa blob 삭제</span><span class="sxs-lookup"><span data-stu-id="10987-210">**Lease** - provides a way tooobtain exclusive, renewable, write or delete access tooa blob for a period of time</span></span>

### <a name="etag"></a><span data-ttu-id="10987-211">ETag</span><span class="sxs-lookup"><span data-stu-id="10987-211">ETag</span></span>
<span data-ttu-id="10987-212">여러 클라이언트 또는 인스턴스 toowrite toohello 블록 Blob 또는 페이지 Blob 동시에 tooallow 해야 할 경우 Etag를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="10987-212">Use ETags if you need tooallow multiple clients or instances toowrite toohello block Blob or page Blob simultaneously.</span></span> <span data-ttu-id="10987-213">hello ETag 있습니다 toodetermine를 hello 컨테이너 또는 blob가 수정 되었으면 이후 처음 읽기 또는 생성자, 다른 클라이언트 또는 프로세스에 의해 커밋된 변경 내용을 덮어쓰지 tooavoid 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10987-213">hello ETag allows you toodetermine if hello container or blob was modified since you initially read or created it, which allows you tooavoid overwriting changes committed by another client or process.</span></span>

<span data-ttu-id="10987-214">선택적 hello를 사용 하 여 ETag 조건을 설정할 수 있습니다 `options.accessConditions` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="10987-214">You can set ETag conditions by using hello optional `options.accessConditions` parameter.</span></span> <span data-ttu-id="10987-215">hello 다음 코드 예제에서는 업로드 hello **test.txt** hello blob에서 이미 존재 하 고 hello ETag 값이 파일에 포함 된 `etagToMatch`합니다.</span><span class="sxs-lookup"><span data-stu-id="10987-215">hello following code example only uploads hello **test.txt** file if hello blob already exists and has hello ETag value contained by `etagToMatch`.</span></span>

```nodejs
blobSvc.createBlockBlobFromLocalFile('mycontainer', 'myblob', 'test.txt', { accessConditions: { EtagMatch: etagToMatch} }, function(error, result, response){
    if(!error){
    // file uploaded
  }
});
```

<span data-ttu-id="10987-216">Etag를 사용 하는 hello 일반적인 패턴은:</span><span class="sxs-lookup"><span data-stu-id="10987-216">When you're using ETags, hello general pattern is:</span></span>

1. <span data-ttu-id="10987-217">만들기, 목록 또는 가져오기 작업의 hello 결과로 hello를 ETag를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="10987-217">Obtain hello ETag as hello result of a create, list, or get operation.</span></span>
2. <span data-ttu-id="10987-218">해당 hello ETag 값을 수정 되지 않았는지 검사 동작을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="10987-218">Perform an action, checking that hello ETag value has not been modified.</span></span>

<span data-ttu-id="10987-219">Hello 값이 수정 된 경우 다른 클라이언트 또는 인스턴스 hello ETag 값을 가져온 이후 hello blob 또는 컨테이너를 수정 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="10987-219">If hello value was modified, this indicates that another client or instance modified hello blob or container since you obtained hello ETag value.</span></span>

### <a name="lease"></a><span data-ttu-id="10987-220">임대</span><span class="sxs-lookup"><span data-stu-id="10987-220">Lease</span></span>
<span data-ttu-id="10987-221">Hello를 사용 하 여 새로운 임대를 획득 수 **acquireLease** 메서드에 맞다면 tooobtain 임대에 hello blob 또는 컨테이너를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="10987-221">You can acquire a new lease by using hello **acquireLease** method, specifying hello blob or container that you wish tooobtain a lease on.</span></span> <span data-ttu-id="10987-222">Hello 코드 다음에 임대를 획득 하는 예를 들어 **myblob**합니다.</span><span class="sxs-lookup"><span data-stu-id="10987-222">For example, hello following code acquires a lease on **myblob**.</span></span>

```nodejs
blobSvc.acquireLease('mycontainer', 'myblob', function(error, result, response){
  if(!error) {
    console.log('leaseId: ' + result.id);
  }
});
```

<span data-ttu-id="10987-223">에 대 한 후속 작업 **myblob** hello를 제공 해야 `options.leaseId` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="10987-223">Subsequent operations on **myblob** must provide hello `options.leaseId` parameter.</span></span> <span data-ttu-id="10987-224">ID가으로 반환 하는 hello 임대 `result.id` 에서 **acquireLease**합니다.</span><span class="sxs-lookup"><span data-stu-id="10987-224">hello lease ID is returned as `result.id` from **acquireLease**.</span></span>

> [!NOTE]
> <span data-ttu-id="10987-225">기본적으로 hello 임대 기간이 무한정입니다.</span><span class="sxs-lookup"><span data-stu-id="10987-225">By default, hello lease duration is infinite.</span></span> <span data-ttu-id="10987-226">Hello를 제공 하 여 (15 ~ 60 초) 사이 유한 기간을 지정할 수 있습니다 `options.leaseDuration` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="10987-226">You can specify a non-infinite duration (between 15 and 60 seconds) by providing hello `options.leaseDuration` parameter.</span></span>
>
>

<span data-ttu-id="10987-227">tooremove 임대를 사용 하 여 **releaseLease**합니다.</span><span class="sxs-lookup"><span data-stu-id="10987-227">tooremove a lease, use **releaseLease**.</span></span> <span data-ttu-id="10987-228">임대를 toobreak 하지만 다른 방지에서 hello 원래 지속 시간이 만료 될 때까지 새로운 임대를 획득할를 사용 하 여 **breakLease**합니다.</span><span class="sxs-lookup"><span data-stu-id="10987-228">toobreak a lease, but prevent others from obtaining a new lease until hello original duration has expired, use **breakLease**.</span></span>

## <a name="work-with-shared-access-signatures"></a><span data-ttu-id="10987-229">공유 액세스 서명 작업</span><span class="sxs-lookup"><span data-stu-id="10987-229">Work with shared access signatures</span></span>
<span data-ttu-id="10987-230">공유 액세스 서명 (SAS)은 안전 하 게 tooprovide 세부적인 액세스 tooblobs 및 저장소 계정 이름 또는 키를 제공 하지 않고 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="10987-230">Shared access signatures (SAS) are a secure way tooprovide granular access tooblobs and containers without providing your storage account name or keys.</span></span> <span data-ttu-id="10987-231">공유 액세스 서명에 사용 되는 tooprovide 제한 된 액세스 tooyour 데이터 tooaccess blob 모바일 앱을 허용 하는 등 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="10987-231">Shared access signatures are often used tooprovide limited access tooyour data, such as allowing a mobile app tooaccess blobs.</span></span>

> [!NOTE]
> <span data-ttu-id="10987-232">Tooblobs 익명 액세스를 허용할 수도 있습니다 공유 액세스 서명을 수 제어 요소가 많은 tooprovide 액세스 hello SAS를 생성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="10987-232">While you can also allow anonymous access tooblobs, shared access signatures allow you tooprovide more controlled access, as you must generate hello SAS.</span></span>
>
>

<span data-ttu-id="10987-233">클라우드 기반 서비스와 같은 신뢰할 수 있는 응용 hello를 사용 하 여 공유 액세스 서명을 생성 하 **generateSharedAccessSignature** 의 hello **BlobService**, 제공 하 고 신뢰할 수 없는 tooan 또는 모바일 앱과 같은 부분 신뢰 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="10987-233">A trusted application such as a cloud-based service generates shared access signatures using hello **generateSharedAccessSignature** of hello **BlobService**, and provides it tooan untrusted or semi-trusted application such as a mobile app.</span></span> <span data-ttu-id="10987-234">공유 액세스 서명을 hello 시작에 설명 하는 정책을 사용 하 여 생성할 및 종료 날짜는 hello 하는 동안 공유 액세스 서명에 유효 뿐 아니라 hello 수준 부여한 toohello 공유 액세스 서명을 홀더를 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="10987-234">Shared access signatures are generated using a policy, which describes hello start and end dates during which hello shared access signatures are valid, as well as hello access level granted toohello shared access signatures holder.</span></span>

<span data-ttu-id="10987-235">hello 다음 코드 예제에서는 발생 하는 hello 공유 액세스 서명을 소유자 tooperform 읽기 hello에 대 한 작업을 허용 하는 새 공유 액세스 정책을 **myblob** blob, 이며 100 분 만들어질 hello 시간이 지난 후 만료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="10987-235">hello following code example generates a new shared access policy that allows hello shared access signatures holder tooperform read operations on hello **myblob** blob, and expires 100 minutes after hello time it is created.</span></span>

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

<span data-ttu-id="10987-236">Note 또한 필요에 따라 hello 공유 액세스 서명을 소유자가 시도할 때 tooaccess hello 컨테이너 제공 hello 호스트 정보 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="10987-236">Note that hello host information must be provided also, as it is required when hello shared access signatures holder attempts tooaccess hello container.</span></span>

<span data-ttu-id="10987-237">hello 그런 다음 클라이언트 응용 프로그램 사용 하 여 공유 액세스 서명은 **BlobServiceWithSAS** hello blob에 대 한 tooperform 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="10987-237">hello client application then uses shared access signatures with **BlobServiceWithSAS** tooperform operations against hello blob.</span></span> <span data-ttu-id="10987-238">hello 다음 정보를 가져옵니다에 대 한 **myblob**합니다.</span><span class="sxs-lookup"><span data-stu-id="10987-238">hello following gets information about **myblob**.</span></span>

```nodejs
var sharedBlobSvc = azure.createBlobServiceWithSas(host, blobSAS);
sharedBlobSvc.getBlobProperties('mycontainer', 'myblob', function (error, result, response) {
  if(!error) {
    // retrieved info
  }
});
```

<span data-ttu-id="10987-239">Hello 공유 액세스 서명을 toomodify hello blob 하려고 시도 하는 경우 읽기 전용 액세스 권한으로 생성 된 이후 오류가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="10987-239">Since hello shared access signatures were generated with read-only access, if an attempt is made toomodify hello blob, an error will be returned.</span></span>

### <a name="access-control-lists"></a><span data-ttu-id="10987-240">액세스 제어 목록</span><span class="sxs-lookup"><span data-stu-id="10987-240">Access control lists</span></span>
<span data-ttu-id="10987-241">SAS에 대 한 액세스 제어 목록 (ACL) tooset hello 액세스 정책을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10987-241">You can also use an access control list (ACL) tooset hello access policy for SAS.</span></span> <span data-ttu-id="10987-242">각 클라이언트에 대 한 다른 액세스 정책을 제공 하지만 여러 클라이언트 tooaccess 컨테이너 tooallow 원하는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="10987-242">This is useful if you wish tooallow multiple clients tooaccess a container but provide different access policies for each client.</span></span>

<span data-ttu-id="10987-243">ACL은 각 정책에 ID가 연결된 액세스 정책 배열을 사용하여 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="10987-243">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span></span> <span data-ttu-id="10987-244">다음 코드 예제는 hello 'user1' 및 'user2'에 대 한 두 개의 정책을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="10987-244">hello following code example defines two policies, one for 'user1' and one for 'user2':</span></span>

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

<span data-ttu-id="10987-245">다음 코드 예제에서는 hello hello에 대 한 현재 ACL **mycontainer**, 다음 사용 하 여 hello 새 정책을 추가 **setBlobAcl**합니다.</span><span class="sxs-lookup"><span data-stu-id="10987-245">hello following code example gets hello current ACL for **mycontainer**, and then adds hello new policies using **setBlobAcl**.</span></span> <span data-ttu-id="10987-246">이 접근 방식을 통해 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10987-246">This approach allows:</span></span>

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

<span data-ttu-id="10987-247">한 번 hello ACL이 설정, 만들 수 있습니다는 정책에 대 한 hello ID에 따라 공유 액세스 서명 합니다.</span><span class="sxs-lookup"><span data-stu-id="10987-247">Once hello ACL is set, you can then create shared access signatures based on hello ID for a policy.</span></span> <span data-ttu-id="10987-248">다음 코드 예제는 hello 사용자 '2'에 대 한 새 공유 액세스 서명을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="10987-248">hello following code example creates new shared access signatures for 'user2':</span></span>

```nodejs
blobSAS = blobSvc.generateSharedAccessSignature('mycontainer', { Id: 'user2' });
```

## <a name="next-steps"></a><span data-ttu-id="10987-249">다음 단계</span><span class="sxs-lookup"><span data-stu-id="10987-249">Next steps</span></span>
<span data-ttu-id="10987-250">자세한 내용은 다음 리소스는 hello를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="10987-250">For more information, see hello following resources.</span></span>

* <span data-ttu-id="10987-251">[Node용 Azure Storage SDK API 참조][Node용 Azure Storage SDK API 참조]</span><span class="sxs-lookup"><span data-stu-id="10987-251">[Azure Storage SDK for Node API Reference][Azure Storage SDK for Node API Reference]</span></span>
* <span data-ttu-id="10987-252">[Azure Storage 팀 블로그][Azure Storage 팀 블로그]</span><span class="sxs-lookup"><span data-stu-id="10987-252">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>
* <span data-ttu-id="10987-253">GitHub의 [Azure Storage SDK for Node][Azure Storage SDK for Node] 리포지토리</span><span class="sxs-lookup"><span data-stu-id="10987-253">[Azure Storage SDK for Node][Azure Storage SDK for Node] repository on GitHub</span></span>
* [<span data-ttu-id="10987-254">Node.js 개발자 센터</span><span class="sxs-lookup"><span data-stu-id="10987-254">Node.js Developer Center</span></span>](https://azure.microsoft.com/develop/nodejs/)
* [<span data-ttu-id="10987-255">Hello AzCopy 명령줄 유틸리티를 사용 하 여 데이터를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="10987-255">Transfer data with hello AzCopy command-line utility</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

[Azure Storage SDK for Node]: https://github.com/Azure/azure-storage-node

<span data-ttu-id="10987-256">[Hello Azure 테이블 서비스를 사용 하 여 Node.js 웹 응용 프로그램](../../app-service-web/storage-nodejs-use-table-storage-web-site.md)  </span><span class="sxs-lookup"><span data-stu-id="10987-256">[Node.js web app using hello Azure Table Service](../../app-service-web/storage-nodejs-use-table-storage-web-site.md)  </span></span>  
<span data-ttu-id="10987-257">[빌드하고 웹 매트릭스를 사용 하는 Node.js 웹 응용 프로그램 tooAzure 배포]: https://www.microsoft.com/web/webmatrix/</span><span class="sxs-lookup"><span data-stu-id="10987-257">[Build and deploy a Node.js web app tooAzure using Web Matrix]: https://www.microsoft.com/web/webmatrix/</span></span>  
<span data-ttu-id="10987-258">[REST API를 hello를 사용 하 여]: [Azure 포털] http://msdn.microsoft.com/library/azure/hh264518.aspx: https://portal.azure.com [빌드하고 Node.js 응용 프로그램 tooan Azure 클라우드 서비스 배포](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) [Azure 저장소 팀 블로그]: http:// [Azure 저장소 노드 API 참조에 대 한 SDK] blogs.msdn.com/b/windowsazurestorage/: http://dl.windowsazure.com/nodestoragedocs/index.html</span><span class="sxs-lookup"><span data-stu-id="10987-258">[Using hello REST API]: http://msdn.microsoft.com/library/azure/hh264518.aspx [Azure portal]: https://portal.azure.com [Build and deploy a Node.js application tooan Azure Cloud Service](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) [Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/ [Azure Storage SDK for Node API Reference]: http://dl.windowsazure.com/nodestoragedocs/index.html</span></span>

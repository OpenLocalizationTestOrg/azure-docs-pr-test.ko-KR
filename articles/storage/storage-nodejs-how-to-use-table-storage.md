---
title: "Node.js에서 Azure Table Storage를 사용하는 방법 | Microsoft Docs"
description: "Azure 테이블 저장소, NoSQL 데이터 저장소를 사용하여 클라우드에 구조화된 데이터를 저장합니다."
services: storage
documentationcenter: nodejs
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: fc2e33d2-c5da-4861-8503-53fdc25750de
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: f004408910aecc380e20f7da54dbd155d179aaa5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-table-storage-from-nodejs"></a><span data-ttu-id="53e50-103">Node.js에서 Azure 테이블 저장소를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="53e50-103">How to use Azure Table storage from Node.js</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="53e50-104">개요</span><span class="sxs-lookup"><span data-stu-id="53e50-104">Overview</span></span>
<span data-ttu-id="53e50-105">이 항목에서는 Node.js 응용 프로그램의 Azure 테이블 서비스를 사용하여 일반 시나리오를 수행하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-105">This topic shows how to perform common scenarios using the Azure Table service in a Node.js application.</span></span>

<span data-ttu-id="53e50-106">이 항목의 코드 예제에서는 Node.js 응용 프로그램이 이미 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-106">The code examples in this topic assume you already have a Node.js application.</span></span> <span data-ttu-id="53e50-107">Azure에서 Node.js 응용 프로그램을 만드는 방법에 대한 자세한 내용은 다음 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="53e50-107">For information about how to create a Node.js application in Azure, see any of these topics:</span></span>

* [<span data-ttu-id="53e50-108">Azure 앱 서비스에서 Node.js 웹 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="53e50-108">Create a Node.js web app in Azure App Service</span></span>](../app-service-web/app-service-web-get-started-nodejs.md)
* [<span data-ttu-id="53e50-109">WebMatrix를 사용하여 Node.js 웹앱 빌드 및 Azure에 배포</span><span class="sxs-lookup"><span data-stu-id="53e50-109">Build and deploy a Node.js web app to Azure using WebMatrix</span></span>](../app-service-web/web-sites-nodejs-use-webmatrix.md)
* <span data-ttu-id="53e50-110">[Node.js 응용 프로그램 빌드 및 Azure 클라우드 서비스에 배포](../cloud-services/cloud-services-nodejs-develop-deploy-app.md) (Windows PowerShell 사용)</span><span class="sxs-lookup"><span data-stu-id="53e50-110">[Build and deploy a Node.js application to an Azure Cloud Service](../cloud-services/cloud-services-nodejs-develop-deploy-app.md) (using Windows PowerShell)</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="configure-your-application-to-access-azure-storage"></a><span data-ttu-id="53e50-111">Azure 저장소에 액세스하도록 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="53e50-111">Configure your application to access Azure Storage</span></span>
<span data-ttu-id="53e50-112">Azure 저장소를 사용하려면 저장소 REST 서비스와 통신하는 편리한 라이브러리 집합이 포함되어 있는 Node.js용 Azure 저장소 SDK가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-112">To use Azure Storage, you need the Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with the storage REST services.</span></span>

### <a name="use-node-package-manager-npm-to-install-the-package"></a><span data-ttu-id="53e50-113">NPM(Node Package Manager)을 사용하여 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="53e50-113">Use Node Package Manager (NPM) to install the package</span></span>
1. <span data-ttu-id="53e50-114">**PowerShell**(Windows), **Terminal**(Mac) 또는 **Bash**(Unix) 등과 같은 명령줄 인터페이스를 사용하여 응용 프로그램을 만든 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-114">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix), and navigate to the folder where you created your application.</span></span>
2. <span data-ttu-id="53e50-115">명령 창에 **npm install azure-storage** 를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-115">Type **npm install azure-storage** in the command window.</span></span> <span data-ttu-id="53e50-116">명령 출력은 다음 예제와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-116">Output from the command is similar to the following example.</span></span>

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
3. <span data-ttu-id="53e50-117">**ls** 명령을 수동으로 실행하여 **node\_modules** 폴더가 만들어졌는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-117">You can manually run the **ls** command to verify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="53e50-118">이 폴더에서 저장소에 액세스하는 데 필요한 라이브러리가 들어 있는 **azure-storage** 패키지를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-118">Inside that folder you will find the **azure-storage** package, which contains the libraries you need to access storage.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="53e50-119">패키지 가져오기</span><span class="sxs-lookup"><span data-stu-id="53e50-119">Import the package</span></span>
<span data-ttu-id="53e50-120">응용 프로그램에서 아래 코드를 **server.js** 파일의 맨 위에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-120">Add the following code to the top of the **server.js** file in your application:</span></span>

```nodejs
var azure = require('azure-storage');
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="53e50-121">Azure 저장소 연결 설정</span><span class="sxs-lookup"><span data-stu-id="53e50-121">Set up an Azure Storage connection</span></span>
<span data-ttu-id="53e50-122">Azure 모듈은 AZURE\_STORAGE\_ACCOUNT 및 AZURE\_STORAGE\_ACCESS\_KEY 또는 AZURE\_STORAGE\_CONNECTION\_STRING 환경 변수를 읽고 Azure Storage 계정에 연결하는 데 필요한 정보를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-122">The azure module will read the environment variables AZURE\_STORAGE\_ACCOUNT and AZURE\_STORAGE\_ACCESS\_KEY, or AZURE\_STORAGE\_CONNECTION\_STRING for information required to connect to your Azure storage account.</span></span> <span data-ttu-id="53e50-123">이러한 환경 변수가 설정되어 있지 않은 경우 **TableService**를 호출할 때 계정 정보를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-123">If these environment variables are not set, you must specify the account information when calling **TableService**.</span></span>

<span data-ttu-id="53e50-124">Azure 웹 사이트의 [Azure Portal](https://portal.azure.com)에서 환경 변수를 설정하는 방법에 대한 예제는 [Azure Table Service를 사용하는 Node.js 웹앱](../app-service-web/storage-nodejs-use-table-storage-web-site.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="53e50-124">For an example of setting the environment variables in the [Azure portal](https://portal.azure.com) for an Azure Website, see [Node.js web app using the Azure Table Service](../app-service-web/storage-nodejs-use-table-storage-web-site.md).</span></span>

## <a name="create-a-table"></a><span data-ttu-id="53e50-125">테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="53e50-125">Create a table</span></span>
<span data-ttu-id="53e50-126">다음 코드는 **TableService** 개체를 만든 다음 이 개체를 사용하여 새 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-126">The following code creates a **TableService** object and uses it to create a new table.</span></span> <span data-ttu-id="53e50-127">**server.js**의 위쪽에 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-127">Add the following near the top of **server.js**.</span></span>

```nodejs
var tableSvc = azure.createTableService();
```

<span data-ttu-id="53e50-128">**createTableIfNotExists** 를 호출하면 지정된 이름을 사용하는 테이블이 없는 경우 새 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-128">The call to **createTableIfNotExists** will create a new table with the specified name if it does not already exist.</span></span> <span data-ttu-id="53e50-129">다음 예제에서는 'mytable'이라는 새 테이블(없는 경우)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-129">The following example creates a new table named 'mytable' if it does not already exist:</span></span>

```nodejs
tableSvc.createTableIfNotExists('mytable', function(error, result, response){
  if(!error){
    // Table exists or created
  }
});
```

<span data-ttu-id="53e50-130">새 테이블이 만들어지면 `result.created`는 `true`가 되고, 테이블이 이미 있으면 `false`가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-130">The `result.created` will be `true` if a new table is created, and `false` if the table already exists.</span></span> <span data-ttu-id="53e50-131">`response` 에는 요청에 대한 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-131">The `response` will contain information about the request.</span></span>

### <a name="filters"></a><span data-ttu-id="53e50-132">필터</span><span class="sxs-lookup"><span data-stu-id="53e50-132">Filters</span></span>
<span data-ttu-id="53e50-133">**TableService**를 사용하여 수행되는 작업에 선택적 필터링 작업을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-133">Optional filtering operations can be applied to operations performed using **TableService**.</span></span> <span data-ttu-id="53e50-134">필터링 작업은 로깅, 자동 재시도 등을 포함할 수 있습니다. 필터는 시그니쳐가 있는 메서드를 구현하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-134">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with the signature:</span></span>

```nodejs
function handle (requestOptions, next)
```

<span data-ttu-id="53e50-135">요청 옵션에 대한 전처리를 수행한 후 메서드는 다음 서명을 사용하여 콜백을 전달하는 "next"를 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-135">After doing its preprocessing on the request options, the method needs to call "next", passing a callback with the following signature:</span></span>

```nodejs
function (returnObject, finalCallback, next)
```

<span data-ttu-id="53e50-136">이 콜백에서 returnObject(서버에 요청 응답 반환)를 처리한 후 콜백은 next(있는 경우)를 호출하여 다른 필터를 계속 처리하거나 finalCallback을 호출하여 서비스 호출을 종료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-136">In this callback, and after processing the returnObject (the response from the request to the server), the callback needs to either invoke next if it exists to continue processing other filters or simply invoke finalCallback otherwise to end the service invocation.</span></span>

<span data-ttu-id="53e50-137">Node.js용 Azure SDK에는 재시도 논리를 구현하는 두 필터 **ExponentialRetryPolicyFilter** 및 **LinearRetryPolicyFilter**가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-137">Two filters that implement retry logic are included with the Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="53e50-138">다음은 **ExponentialRetryPolicyFilter**를 사용하는 **TableService** 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-138">The following creates a **TableService** object that uses the **ExponentialRetryPolicyFilter**:</span></span>

```nodejs
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var tableSvc = azure.createTableService().withFilter(retryOperations);
```

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="53e50-139">테이블에 엔터티 추가</span><span class="sxs-lookup"><span data-stu-id="53e50-139">Add an entity to a table</span></span>
<span data-ttu-id="53e50-140">엔터티를 추가하려면 먼저 엔터티 속성을 정의하는 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-140">To add an entity, first create an object that defines your entity properties.</span></span> <span data-ttu-id="53e50-141">모든 엔터티에는 엔터티의 고유 식별자인 **PartitionKey**와 **RowKey**를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-141">All entities must contain a **PartitionKey** and **RowKey**, which are unique identifiers for the entity.</span></span>

* <span data-ttu-id="53e50-142">**PartitionKey** - 엔터티가 저장된 파티션을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-142">**PartitionKey** - determines the partition that the entity is stored in</span></span>
* <span data-ttu-id="53e50-143">**RowKey** - 파티션에 있는 엔터티를 고유하게 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-143">**RowKey** - uniquely identifies the entity within the partition</span></span>

<span data-ttu-id="53e50-144">**PartitionKey**와 **RowKey**는 모두 문자열 값이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-144">Both **PartitionKey** and **RowKey** must be string values.</span></span> <span data-ttu-id="53e50-145">자세한 내용은 [테이블 서비스 데이터 모델 이해](http://msdn.microsoft.com/library/azure/dd179338.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="53e50-145">For more information, see [Understanding the Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

<span data-ttu-id="53e50-146">다음은 엔터티를 정의하는 경우의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-146">The following is an example of defining an entity.</span></span> <span data-ttu-id="53e50-147">**dueDate**는 **Edm.DateTime** 형식으로 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-147">Note that **dueDate** is defined as a type of **Edm.DateTime**.</span></span> <span data-ttu-id="53e50-148">유형 지정은 선택적이며 지정하지 않을 경우 유형이 유추됩니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-148">Specifying the type is optional, and types will be inferred if not specified.</span></span>

```nodejs
var task = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'take out the trash'},
  dueDate: {'_':new Date(2015, 6, 20), '$':'Edm.DateTime'}
};
```

> [!NOTE]
> <span data-ttu-id="53e50-149">각 레코드에는 엔터티가 삽입되거나 업데이트될 경우 Azure에서 설정되는 **Timestamp** 필드도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-149">There is also a **Timestamp** field for each record, which is set by Azure when an entity is inserted or updated.</span></span>
>
>

<span data-ttu-id="53e50-150">**entityGenerator** 를 사용하여 엔터티를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-150">You can also use the **entityGenerator** to create entities.</span></span> <span data-ttu-id="53e50-151">다음 예에서는 **entityGenerator**를 사용하여 같은 작업 엔터티를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-151">The following example creates the same task entity using the **entityGenerator**.</span></span>

```nodejs
var entGen = azure.TableUtilities.entityGenerator;
var task = {
  PartitionKey: entGen.String('hometasks'),
  RowKey: entGen.String('1'),
  description: entGen.String('take out the trash'),
  dueDate: entGen.DateTime(new Date(Date.UTC(2015, 6, 20))),
};
```

<span data-ttu-id="53e50-152">테이블에 엔터티를 추가하려면 엔터티 개체를 **insertEntity** 메서드에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-152">To add an entity to your table, pass the entity object to the **insertEntity** method.</span></span>

```nodejs
tableSvc.insertEntity('mytable',task, function (error, result, response) {
  if(!error){
    // Entity inserted
  }
});
```

<span data-ttu-id="53e50-153">작업에 성공할 경우 `result` 값에는 삽입한 레코드의 [ETag](http://en.wikipedia.org/wiki/HTTP_ETag)가 포함되고 `response` 값에는 작업에 대한 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-153">If the operation is successful, `result` will contain the [ETag](http://en.wikipedia.org/wiki/HTTP_ETag) of the inserted record and `response` will contain information about the operation.</span></span>

<span data-ttu-id="53e50-154">예제 응답:</span><span class="sxs-lookup"><span data-stu-id="53e50-154">Example response:</span></span>

```nodejs
{ '.metadata': { etag: 'W/"datetime\'2015-02-25T01%3A22%3A22.5Z\'"' } }
```

> [!NOTE]
> <span data-ttu-id="53e50-155">기본적으로 **insertEntity**는 삽입된 엔터티를 `response` 정보의 일부로 반환하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-155">By default, **insertEntity** does not return the inserted entity as part of the `response` information.</span></span> <span data-ttu-id="53e50-156">이 엔터티에서 다른 작업을 수행할 계획이거나 정보를 캐시하고 싶은 경우 `result`의 일부로 반환하면 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-156">If you plan on performing other operations on this entity, or wish to cache the information, it can be useful to have it returned as part of the `result`.</span></span> <span data-ttu-id="53e50-157">다음과 같이 **echoContent** 를 사용하도록 설정하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-157">You can do this by enabling **echoContent** as follows:</span></span>
>
> `tableSvc.insertEntity('mytable', task, {echoContent: true}, function (error, result, response) {...}`
>
>

## <a name="update-an-entity"></a><span data-ttu-id="53e50-158">엔터티 업데이트</span><span class="sxs-lookup"><span data-stu-id="53e50-158">Update an entity</span></span>
<span data-ttu-id="53e50-159">다음과 같은 여러 메서드를 사용하여 기존 엔터티를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-159">There are multiple methods available to update an existing entity:</span></span>

* <span data-ttu-id="53e50-160">**replaceEntity** - 기존 엔터티를 바꾸어서 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-160">**replaceEntity** - updates an existing entity by replacing it</span></span>
* <span data-ttu-id="53e50-161">**mergeEntity** - 새 속성 값을 기존 엔터티에 병합하여 기존 엔터티를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-161">**mergeEntity** - updates an existing entity by merging new property values into the existing entity</span></span>
* <span data-ttu-id="53e50-162">**insertOrReplaceEntity** - 기존 엔터티를 바꾸어서 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-162">**insertOrReplaceEntity** - updates an existing entity by replacing it.</span></span> <span data-ttu-id="53e50-163">엔터티가 없는 경우 새 엔터티를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-163">If no entity exists, a new one will be inserted</span></span>
* <span data-ttu-id="53e50-164">**insertOrMergeEntity** - 새 속성 값을 기존 항목에 병합하여 기존 엔터티를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-164">**insertOrMergeEntity** - updates an existing entity by merging new property values into the existing.</span></span> <span data-ttu-id="53e50-165">엔터티가 없는 경우 새 엔터티를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-165">If no entity exists, a new one will be inserted</span></span>

<span data-ttu-id="53e50-166">다음 예제에서는 **replaceEntity**를 사용하여 엔터티를 업데이트하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-166">The following example demonstrates updating an entity using **replaceEntity**:</span></span>

```nodejs
tableSvc.replaceEntity('mytable', updatedTask, function(error, result, response){
  if(!error) {
    // Entity updated
  }
});
```

> [!NOTE]
> <span data-ttu-id="53e50-167">기본적으로는 엔터티를 업데이트할 때 업데이트할 데이터를 다른 프로세서에서 이전에 수정했는지 확인하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-167">By default, updating an entity does not check to see if the data being updated has previously been modified by another process.</span></span> <span data-ttu-id="53e50-168">동시 업데이트를 지원하려면:</span><span class="sxs-lookup"><span data-stu-id="53e50-168">To support concurrent updates:</span></span>
>
> 1. <span data-ttu-id="53e50-169">업데이트할 개체의 ETag를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-169">Get the ETag of the object being updated.</span></span> <span data-ttu-id="53e50-170">모든 엔터티 관련 작업에서의 `response`의 일부로 반환되며 `response['.metadata'].etag`를 통해 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-170">This is returned as part of the `response` for any entity-related operation and can be retrieved through `response['.metadata'].etag`.</span></span>
> 2. <span data-ttu-id="53e50-171">엔터티에서 업데이트 작업을 수행할 때 이전에 검색한 ETag 정보를 새 엔터티에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-171">When performing an update operation on an entity, add the ETag information previously retrieved to the new entity.</span></span> <span data-ttu-id="53e50-172">예:</span><span class="sxs-lookup"><span data-stu-id="53e50-172">For example:</span></span>
>
>       <span data-ttu-id="53e50-173">entity2['.metadata'].etag = currentEtag;</span><span class="sxs-lookup"><span data-stu-id="53e50-173">entity2['.metadata'].etag = currentEtag;</span></span>
> 3. <span data-ttu-id="53e50-174">업데이트 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-174">Perform the update operation.</span></span> <span data-ttu-id="53e50-175">ETag 값을 검색한 후에 응용 프로그램의 다른 인스턴스 등에서 엔터티가 수정된 경우에는 요청에 지정된 업데이트 조건이 충족되지 않았다는 내용의 `error` 가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-175">If the entity has been modified since you retrieved the ETag value, such as another instance of your application, an `error` will be returned stating that the update condition specified in the request was not satisfied.</span></span>
>
>

<span data-ttu-id="53e50-176">**replaceEntity** 및 **mergeEntity**를 사용할 때 업데이트 중인 엔터티가 없는 경우 업데이트 작업이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-176">With **replaceEntity** and **mergeEntity**, if the entity that is being updated doesn't exist, then the update operation will fail.</span></span> <span data-ttu-id="53e50-177">따라서 엔터티의 존재 여부에 상관없이 엔터티를 저장하려면 **insertOrReplaceEntity** 또는 **insertOrMergeEntity**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-177">Therefore if you wish to store an entity regardless of whether it already exists, use **insertOrReplaceEntity** or **insertOrMergeEntity**.</span></span>

<span data-ttu-id="53e50-178">업데이트 작업이 성공할 경우 `result` 값에는 업데이트된 엔터티의 **Etag** 가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-178">The `result` for successful update operations will contain the **Etag** of the updated entity.</span></span>

## <a name="work-with-groups-of-entities"></a><span data-ttu-id="53e50-179">엔터티 그룹 작업</span><span class="sxs-lookup"><span data-stu-id="53e50-179">Work with groups of entities</span></span>
<span data-ttu-id="53e50-180">서버에서 원자성 처리를 수행하도록 여러 작업을 일괄적으로 제출하는 것이 좋은 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-180">Sometimes it makes sense to submit multiple operations together in a batch to ensure atomic processing by the server.</span></span> <span data-ttu-id="53e50-181">이렇게 하려면 **TableBatch** 클래스를 사용하여 배치를 만든 다음 **TableService**의 **executeBatch** 메서드를 사용하여 일괄 처리 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-181">To accomplish that, use the **TableBatch** class to create a batch, and then use the **executeBatch** method of **TableService** to perform the batched operations.</span></span>

 <span data-ttu-id="53e50-182">다음 예제에서는 두 엔터티를 일괄적으로 제출하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-182">The following example demonstrates submitting two entities in a batch:</span></span>

```nodejs
var task1 = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'Take out the trash'},
  dueDate: {'_':new Date(2015, 6, 20)}
};
var task2 = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '2'},
  description: {'_':'Wash the dishes'},
  dueDate: {'_':new Date(2015, 6, 20)}
};

var batch = new azure.TableBatch();

batch.insertEntity(task1, {echoContent: true});
batch.insertEntity(task2, {echoContent: true});

tableSvc.executeBatch('mytable', batch, function (error, result, response) {
  if(!error) {
    // Batch completed
  }
});
```

<span data-ttu-id="53e50-183">일괄 처리 작업에 성공할 경우 `result` 값에는 일괄 처리의 각 작업에 대한 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-183">For successful batch operations, `result` will contain information for each operation in the batch.</span></span>

### <a name="work-with-batched-operations"></a><span data-ttu-id="53e50-184">일괄 처리 작업</span><span class="sxs-lookup"><span data-stu-id="53e50-184">Work with batched operations</span></span>
<span data-ttu-id="53e50-185">배치에 추가된 작업은 `operations` 속성을 보고 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-185">Operations added to a batch can be inspected by viewing the `operations` property.</span></span> <span data-ttu-id="53e50-186">작업에 다음 메서드를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-186">You can also use the following methods to work with operations:</span></span>

* <span data-ttu-id="53e50-187">**clear** - 배치에서 모든 작업을 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-187">**clear** - clears all operations from a batch</span></span>
* <span data-ttu-id="53e50-188">**getOperations** - 배치에서 작업을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-188">**getOperations** - gets an operation from the batch</span></span>
* <span data-ttu-id="53e50-189">**hasOperations** - 배치에 작업이 포함되어 있으면 true를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-189">**hasOperations** - returns true if the batch contains operations</span></span>
* <span data-ttu-id="53e50-190">**removeOperations** - 작업을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-190">**removeOperations** - removes an operation</span></span>
* <span data-ttu-id="53e50-191">**size** - 배치에 있는 작업의 수를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-191">**size** - returns the number of operations in the batch</span></span>

## <a name="retrieve-an-entity-by-key"></a><span data-ttu-id="53e50-192">키를 통해 엔터티 검색</span><span class="sxs-lookup"><span data-stu-id="53e50-192">Retrieve an entity by key</span></span>
<span data-ttu-id="53e50-193">**PartitionKey** 및 **RowKey**를 기준으로 특정 엔터티를 반환하려면 **retrieveEntity** 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-193">To return a specific entity based on the **PartitionKey** and **RowKey**, use the **retrieveEntity** method.</span></span>

```nodejs
tableSvc.retrieveEntity('mytable', 'hometasks', '1', function(error, result, response){
  if(!error){
    // result contains the entity
  }
});
```

<span data-ttu-id="53e50-194">이 작업이 완료되면 `result` 에 엔터티가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-194">Once this operation is complete, `result` will contain the entity.</span></span>

## <a name="query-a-set-of-entities"></a><span data-ttu-id="53e50-195">엔터티 집합 쿼리</span><span class="sxs-lookup"><span data-stu-id="53e50-195">Query a set of entities</span></span>
<span data-ttu-id="53e50-196">테이블을 쿼리하려면 **TableQuery** 개체와 다음 절을 사용하여 쿼리 식을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-196">To query a table, use the **TableQuery** object to build up a query expression using the following clauses:</span></span>

* <span data-ttu-id="53e50-197">**select** - 쿼리에서 반환할 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-197">**select** - the fields to be returned from the query</span></span>
* <span data-ttu-id="53e50-198">**where** - where 절입니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-198">**where** - the where clause</span></span>

  * <span data-ttu-id="53e50-199">**and** - `and` where 조건입니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-199">**and** - an `and` where condition</span></span>
  * <span data-ttu-id="53e50-200">**or** - `or` where 조건입니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-200">**or** - an `or` where condition</span></span>
* <span data-ttu-id="53e50-201">**top** - 가져올 항목의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-201">**top** - the number of items to fetch</span></span>

<span data-ttu-id="53e50-202">다음 예에서는 PartitionKey가 'hometasks'인 상위 5개의 항목을 반환하는 쿼리를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-202">The following example builds a query that will return the top five items with a PartitionKey of 'hometasks'.</span></span>

```nodejs
var query = new azure.TableQuery()
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

<span data-ttu-id="53e50-203">**select** 가 사용되지 않았기 때문에 모든 필드가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-203">Since **select** is not used, all fields will be returned.</span></span> <span data-ttu-id="53e50-204">테이블에 대해 쿼리를 수행하려면 **queryEntities**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-204">To perform the query against a table, use **queryEntities**.</span></span> <span data-ttu-id="53e50-205">다음 예에서는 이 쿼리를 사용하여 'mytable'에서 엔터티를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-205">The following example uses this query to return entities from 'mytable'.</span></span>

```nodejs
tableSvc.queryEntities('mytable',query, null, function(error, result, response) {
  if(!error) {
    // query was successful
  }
});
```

<span data-ttu-id="53e50-206">성공할 경우에는 `result.entries` 값에는 쿼리와 일치하는 엔터티의 배열이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-206">If successful, `result.entries` will contain an array of entities that match the query.</span></span> <span data-ttu-id="53e50-207">쿼리에서 엔터티를 모두 반환할 수 없는 경우 `result.continuationToken` 이*null* 이 아닌 값이 되므로 **queryEntities** 의 세 번째 매개 변수로 사용하여 더 많은 결과를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-207">If the query was unable to return all entities, `result.continuationToken` will be non-*null* and can be used as the third parameter of **queryEntities** to retrieve more results.</span></span> <span data-ttu-id="53e50-208">초기 쿼리의 경우 세 번째 매개 변수에 *null* 을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-208">For the initial query, use *null* for the third parameter.</span></span>

### <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="53e50-209">엔터티 속성 하위 집합 쿼리</span><span class="sxs-lookup"><span data-stu-id="53e50-209">Query a subset of entity properties</span></span>
<span data-ttu-id="53e50-210">테이블 쿼리에서는 엔터티에서 일부 필드만 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-210">A query to a table can retrieve just a few fields from an entity.</span></span>
<span data-ttu-id="53e50-211">따라서 대역폭이 줄어들며 특히 큰 엔터티의 경우 쿼리 성능이 향상될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-211">This reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="53e50-212">**select** 절을 사용하여 반환할 필드의 이름을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-212">Use the **select** clause and pass the names of the fields to be returned.</span></span> <span data-ttu-id="53e50-213">예를 들어 다음 쿼리에서는 **description** 및 **dueDate** 필드만 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-213">For example, the following query will return only the **description** and **dueDate** fields.</span></span>

```nodejs
var query = new azure.TableQuery()
  .select(['description', 'dueDate'])
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

## <a name="delete-an-entity"></a><span data-ttu-id="53e50-214">엔터티 삭제</span><span class="sxs-lookup"><span data-stu-id="53e50-214">Delete an entity</span></span>
<span data-ttu-id="53e50-215">파티션 및 행 키를 사용하여 엔터티를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-215">You can delete an entity using its partition and row keys.</span></span> <span data-ttu-id="53e50-216">이 예제에서 **task1** 개체는 삭제할 엔터티의 **RowKey** 및 **PartitionKey** 값을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-216">In this example, the **task1** object contains the **RowKey** and **PartitionKey** values of the entity to be deleted.</span></span> <span data-ttu-id="53e50-217">그런 다음 개체는 **deleteEntity** 메서드에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-217">Then the object is passed to the **deleteEntity** method.</span></span>

```nodejs
var task = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'}
};

tableSvc.deleteEntity('mytable', task, function(error, response){
  if(!error) {
    // Entity deleted
  }
});
```

> [!NOTE]
> <span data-ttu-id="53e50-218">항목을 삭제할 때 항목이 다른 프로세스에서 수정되지 않았는지 확인할 수 있도록 ETag를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-218">Consider using ETags when deleting items, to ensure that the item hasn't been modified by another process.</span></span> <span data-ttu-id="53e50-219">ETag 사용 방법에 대한 자세한 내용은 [엔터티 업데이트](#update-an-entity) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="53e50-219">See [Update an entity](#update-an-entity) for information on using ETags.</span></span>
>
>

## <a name="delete-a-table"></a><span data-ttu-id="53e50-220">테이블 삭제</span><span class="sxs-lookup"><span data-stu-id="53e50-220">Delete a table</span></span>
<span data-ttu-id="53e50-221">다음 코드는 저장소 계정에서 테이블을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-221">The following code deletes a table from a storage account.</span></span>

```nodejs
tableSvc.deleteTable('mytable', function(error, response){
    if(!error){
        // Table deleted
    }
});
```

<span data-ttu-id="53e50-222">테이블이 있는지 확실하지 않은 경우에는 **deleteTableIfExists**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-222">If you are uncertain whether the table exists, use **deleteTableIfExists**.</span></span>

## <a name="use-continuation-tokens"></a><span data-ttu-id="53e50-223">연속토큰 사용</span><span class="sxs-lookup"><span data-stu-id="53e50-223">Use continuation tokens</span></span>
<span data-ttu-id="53e50-224">많은 양의 결과를 얻기 위해 테이블을 쿼리하는 경우 연속 토큰을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-224">When you are querying tables for large amounts of results, look for continuation tokens.</span></span> <span data-ttu-id="53e50-225">당신이 인식하지 못한 쿼리에 대한 사용 가능한 많은 양의 데이터가 있을 경우 연속토큰의 유무를 인식하지 못하도록 작성하지마세요.</span><span class="sxs-lookup"><span data-stu-id="53e50-225">There may be large amounts of data available for your query that you might not realize if you do not build to recognize when a continuation token is present.</span></span>

<span data-ttu-id="53e50-226">연속 토큰이 있을 경우 `continuationToken` 속성을 설정하는 엔터티를 쿼리하는 동안 결과 개체가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-226">The results object returned during querying entities sets a `continuationToken` property when such a token is present.</span></span> <span data-ttu-id="53e50-227">그 다음 파티션 및 테이블 엔터티 간에 이동을 계속하기 위해 쿼리를 수행 할 경우 이것을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-227">You can then use this when performing a query to continue to move across the partition and table entities.</span></span>

<span data-ttu-id="53e50-228">쿼리할 때, 쿼리개체 인스턴스와 콜백 기능간에 연속토큰 매개 변수가 제공될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-228">When querying, a continuationToken parameter may be provided between the query object instance and the callback function:</span></span>

```nodejs
var nextContinuationToken = null;
dc.table.queryEntities(tableName,
    query,
    nextContinuationToken,
    function (error, results) {
        if (error) throw error;

        // iterate through results.entries with results

        if (results.continuationToken) {
            nextContinuationToken = results.continuationToken;
        }

    });
```

<span data-ttu-id="53e50-229">`continuationToken` 개체를 조사하면, 모든 결과를 반복하는 데 사용할 수 있는 `nextPartitionKey`, `nextRowKey` 및 `targetLocation`과 같은 속성을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-229">If you inspect the `continuationToken` object, you will find properties such as `nextPartitionKey`, `nextRowKey` and `targetLocation`, which can be used to iterate through all the results.</span></span>

<span data-ttu-id="53e50-230">또한 GitHub의 Azure Storage Node.js 리포지토리 내에 연속된 샘플이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-230">There is also a continuation sample within the Azure Storage Node.js repo on GitHub.</span></span> <span data-ttu-id="53e50-231">`examples/samples/continuationsample.js`를 찾아보세요.</span><span class="sxs-lookup"><span data-stu-id="53e50-231">Look for `examples/samples/continuationsample.js`.</span></span>

## <a name="work-with-shared-access-signatures"></a><span data-ttu-id="53e50-232">공유 액세스 서명 작업</span><span class="sxs-lookup"><span data-stu-id="53e50-232">Work with shared access signatures</span></span>
<span data-ttu-id="53e50-233">SAS(공유 액세스 서명)는 저장소 계정 이름이나 키를 제공하지 않으면서 테이블에 세분화된 액세스 권한을 안전하게 제공하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-233">Shared access signatures (SAS) are a secure way to provide granular access to tables without providing your storage account name or keys.</span></span> <span data-ttu-id="53e50-234">SAS는 모바일 앱에서 레코드를 쿼리하는 경우와 같이 데이터에 대해 제한된 액세스를 제공하는 경우에 자주 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-234">SAS are often used to provide limited access to your data, such as allowing a mobile app to query records.</span></span>

<span data-ttu-id="53e50-235">클라우드 기반 서비스와 같이 신뢰할 수 있는 응용 프로그램에서는 **TableService**의 **generateSharedAccessSignature**를 사용하여 SAS를 생성하고, 이를 모바일 앱과 같은 신뢰할 수 없거나 신뢰가 약한 응용 프로그램에 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-235">A trusted application such as a cloud-based service generates a SAS using the **generateSharedAccessSignature** of the **TableService**, and provides it to an untrusted or semi-trusted application such as a mobile app.</span></span> <span data-ttu-id="53e50-236">SAS는 SAS가 유효한 시작 및 종료 날짜와 SAS 소유자에게 부여되는 액세스 수준을 설명하는 정책을 사용하여 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-236">The SAS is generated using a policy, which describes the start and end dates during which the SAS is valid, as well as the access level granted to the SAS holder.</span></span>

<span data-ttu-id="53e50-237">다음 예에서는 SAS 소유자가 테이블을 쿼리('r')할 수 있도록 허용하며 만든 후 100분이 지나면 만료되는 새 공유 액세스 정책을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-237">The following example generates a new shared access policy that will allow the SAS holder to query ('r') the table, and expires 100 minutes after the time it is created.</span></span>

```nodejs
var startDate = new Date();
var expiryDate = new Date(startDate);
expiryDate.setMinutes(startDate.getMinutes() + 100);
startDate.setMinutes(startDate.getMinutes() - 100);

var sharedAccessPolicy = {
  AccessPolicy: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.QUERY,
    Start: startDate,
    Expiry: expiryDate
  },
};

var tableSAS = tableSvc.generateSharedAccessSignature('mytable', sharedAccessPolicy);
var host = tableSvc.host;
```

<span data-ttu-id="53e50-238">SAS 소유자가 테이블에 액세스할 때 필요하므로 호스트 정보도 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-238">Note that the host information must be provided also, as it is required when the SAS holder attempts to access the table.</span></span>

<span data-ttu-id="53e50-239">그러고 나면 클라이언트 응용 프로그램에서 **TableServiceWithSAS** 에 SAS를 사용하여 테이블에 대한 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-239">The client application then uses the SAS with **TableServiceWithSAS** to perform operations against the table.</span></span> <span data-ttu-id="53e50-240">다음 예에서는 테이블을 연결하고 쿼리를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-240">The following example connects to the table and performs a query.</span></span>

```nodejs
var sharedTableService = azure.createTableServiceWithSas(host, tableSAS);
var query = azure.TableQuery()
  .where('PartitionKey eq ?', 'hometasks');

sharedTableService.queryEntities(query, null, function(error, result, response) {
  if(!error) {
    // result contains the entities
  }
});
```

<span data-ttu-id="53e50-241">SAS가 쿼리 액세스만으로 생성되었기 때문에 엔터티를 삽입, 업데이트 또는 삭제하려고 하면 오류가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-241">Since the SAS was generated with only query access, if an attempt were made to insert, update, or delete entities, an error would be returned.</span></span>

### <a name="access-control-lists"></a><span data-ttu-id="53e50-242">액세스 제어 목록</span><span class="sxs-lookup"><span data-stu-id="53e50-242">Access Control Lists</span></span>
<span data-ttu-id="53e50-243">ACL(액세스 제어 목록)을 사용하여 SAS에 액세스 정책을 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-243">You can also use an Access Control List (ACL) to set the access policy for a SAS.</span></span> <span data-ttu-id="53e50-244">이 방법은 여러 클라이언트에서 테이블에 액세스하게 하면서 각 클라이언트에 서로 다른 액세스 정책을 제공하려는 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-244">This is useful if you wish to allow multiple clients to access the table, but provide different access policies for each client.</span></span>

<span data-ttu-id="53e50-245">ACL은 각 정책에 ID가 연결된 액세스 정책 배열을 사용하여 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-245">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span></span> <span data-ttu-id="53e50-246">다음 예에서는 'user1'와 'user2'에 대해 하나씩, 두 개의 정책을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-246">The following example defines two policies, one for 'user1' and one for 'user2':</span></span>

```nodejs
var sharedAccessPolicy = {
  user1: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.QUERY,
    Start: startDate,
    Expiry: expiryDate
  },
  user2: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.ADD,
    Start: startDate,
    Expiry: expiryDate
  }
};
```

<span data-ttu-id="53e50-247">다음 예제에서는 **hometasks** 테이블의 현재 ACL을 가져온 다음 **setTableAcl**을 사용하여 새 정책을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-247">The following example gets the current ACL for the **hometasks** table, and then adds the new policies using **setTableAcl**.</span></span> <span data-ttu-id="53e50-248">이 접근 방식을 통해 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-248">This approach allows:</span></span>

```nodejs
var extend = require('extend');
tableSvc.getTableAcl('hometasks', function(error, result, response) {
if(!error){
    var newSignedIdentifiers = extend(true, result.signedIdentifiers, sharedAccessPolicy);
    tableSvc.setTableAcl('hometasks', newSignedIdentifiers, function(error, result, response){
      if(!error){
        // ACL set
      }
    });
  }
});
```

<span data-ttu-id="53e50-249">ACL이 설정되고 나면 정책의 ID를 기반으로 SAS를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-249">Once the ACL has been set, you can then create a SAS based on the ID for a policy.</span></span> <span data-ttu-id="53e50-250">다음 예에서는 'user2'에 대해 새 SAS를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-250">The following example creates a new SAS for 'user2':</span></span>

```nodejs
tableSAS = tableSvc.generateSharedAccessSignature('hometasks', { Id: 'user2' });
```

## <a name="next-steps"></a><span data-ttu-id="53e50-251">다음 단계</span><span class="sxs-lookup"><span data-stu-id="53e50-251">Next steps</span></span>
<span data-ttu-id="53e50-252">자세한 내용은 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="53e50-252">For more information, see the following resources.</span></span>

* <span data-ttu-id="53e50-253">[Microsoft Azure Storage 탐색기](../vs-azure-tools-storage-manage-with-storage-explorer.md)는 Windows, MacOS 및 Linux에서 Azure Storage 데이터로 시각적으로 작업할 수 있도록 해주는 Microsoft의 독립 실행형 무료 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="53e50-253">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="53e50-254">[Azure Storage SDK for Node](https://github.com/Azure/azure-storage-node) 리포지토리</span><span class="sxs-lookup"><span data-stu-id="53e50-254">[Azure Storage SDK for Node](https://github.com/Azure/azure-storage-node) repository on GitHub.</span></span>
* [<span data-ttu-id="53e50-255">Node.js 개발자 센터</span><span class="sxs-lookup"><span data-stu-id="53e50-255">Node.js Developer Center</span></span>](/develop/nodejs/)
* [<span data-ttu-id="53e50-256">Node.js 응용 프로그램을 만들어 Azure 웹 사이트에 배포</span><span class="sxs-lookup"><span data-stu-id="53e50-256">Create and deploy a Node.js application to an Azure website</span></span>](../app-service-web/app-service-web-get-started-nodejs.md)
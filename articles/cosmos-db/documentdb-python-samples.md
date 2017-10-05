---
title: "Azure Cosmos DB에 대한 DocumentDB API Python 예제 | Microsoft Docs"
description: "CRUD 작업을 비롯한 Azure Cosmos DB의 일반적인 작업에 대한 github의 Python 예제를 찾습니다."
keywords: "Python 예제"
services: cosmos-db
author: moderakh
manager: jhubbard
editor: monicar
documentationcenter: python
ms.assetid: 7f4f8db3-e9db-4645-92ef-7819d486a349
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2016
ms.author: moderakh
ms.openlocfilehash: d1577eeeb8fe8007394431ce70a1c7a6ee61776b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-python-examples"></a><span data-ttu-id="13fd1-104">Azure Cosmos DB Python 예제</span><span class="sxs-lookup"><span data-stu-id="13fd1-104">Azure Cosmos DB Python examples</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="13fd1-105">.NET 예제</span><span class="sxs-lookup"><span data-stu-id="13fd1-105">.NET Examples</span></span>](documentdb-dotnet-samples.md)
> * [<span data-ttu-id="13fd1-106">Node.js 예제</span><span class="sxs-lookup"><span data-stu-id="13fd1-106">Node.js Examples</span></span>](documentdb-nodejs-samples.md)
> * [<span data-ttu-id="13fd1-107">Python 예제</span><span class="sxs-lookup"><span data-stu-id="13fd1-107">Python Examples</span></span>](documentdb-python-samples.md)
> * [<span data-ttu-id="13fd1-108">Azure 코드 샘플 갤러리</span><span class="sxs-lookup"><span data-stu-id="13fd1-108">Azure Code Sample Gallery</span></span>](https://azure.microsoft.com/documentation/samples/?service=documentdb)
> 
> 

<span data-ttu-id="13fd1-109">Azure Cosmos DB 리소스에 대해 CRUD 작업 및 다른 일반적인 작업을 수행하는 샘플 솔루션은 [azure-documentdb-python](https://github.com/Azure/azure-documentdb-python/tree/master/samples) GitHub 리포지토리에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13fd1-109">Sample solutions that perform CRUD operations and other common operations on Azure Cosmos DB resources are included in the [azure-documentdb-python](https://github.com/Azure/azure-documentdb-python/tree/master/samples) GitHub repository.</span></span> <span data-ttu-id="13fd1-110">이 문서는 다음을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="13fd1-110">This article provides:</span></span>

* <span data-ttu-id="13fd1-111">각 Python 예제 프로젝트 파일에서 작업에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="13fd1-111">Links to the tasks in each of the Python example project files.</span></span> 
* <span data-ttu-id="13fd1-112">관련된 API 참조 콘텐츠에 대한 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="13fd1-112">Links to the related API reference content.</span></span>

<span data-ttu-id="13fd1-113">**필수 구성 요소**</span><span class="sxs-lookup"><span data-stu-id="13fd1-113">**Prerequisites**</span></span>

1. <span data-ttu-id="13fd1-114">이러한 Python 예제를 사용하려면 Azure 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="13fd1-114">You need an Azure account to use these Python examples:</span></span>
   * <span data-ttu-id="13fd1-115">[Azure 계정을 무료로 개설](https://azure.microsoft.com/pricing/free-trial/)할 수 있음: 유료 Azure 서비스를 사용해볼 수 있는 크레딧을 받게 되며 크레딧을 모두 사용한 후에도 계정을 유지하고 무료 Azure 서비스(예: 웹 서비스)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13fd1-115">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/): You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services, such as Websites.</span></span> <span data-ttu-id="13fd1-116">설정을 명시적으로 변경하여 결제를 요청하지 않는 한 신용 카드로 결제되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="13fd1-116">Your credit card will never be charged, unless you explicitly change your settings and ask to be charged.</span></span>
     * <span data-ttu-id="13fd1-117">[Visual Studio 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)할 수 있음: Visual Studio 구독은 유료 Azure 서비스에 사용할 수 있는 크레딧을 매달 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="13fd1-117">You can [activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/): Your Visual Studio subscription gives you credits every month that you can use for paid Azure services.</span></span>
2. <span data-ttu-id="13fd1-118">또한 [Python SDK](documentdb-sdk-python.md)가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="13fd1-118">You also need the [Python SDK](documentdb-sdk-python.md).</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="13fd1-119">각 샘플은 자체 포함되며 자체를 설정하고 자체를 정리합니다.</span><span class="sxs-lookup"><span data-stu-id="13fd1-119">Each sample is self-contained, it sets itself up and cleans up after itself.</span></span> <span data-ttu-id="13fd1-120">샘플은 [document_client.CreateCollection](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html)에 대한 여러 호출을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="13fd1-120">As such, the samples issue multiple calls to [document_client.CreateCollection](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html).</span></span> <span data-ttu-id="13fd1-121">구독에 이렇게 영향을 줄 때마다 생성되는 컬렉션의 성능 계층 당 1시간 사용량이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="13fd1-121">Each time this is done your subscription will be billed for 1 hour of usage per the performance tier of the collection being created.</span></span> 
   > 
   > 

## <a name="database-examples"></a><span data-ttu-id="13fd1-122">데이터베이스 예제</span><span class="sxs-lookup"><span data-stu-id="13fd1-122">Database examples</span></span>
<span data-ttu-id="13fd1-123">[DatabaseManagement](https://github.com/Azure/azure-documentdb-python/tree/master/samples/DatabaseManagement) 프로젝트의 [Program.py](https://github.com/Azure/azure-documentdb-python/tree/master/samples/DatabaseManagement/Program.py) 파일은 다음 작업을 수행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="13fd1-123">The [Program.py](https://github.com/Azure/azure-documentdb-python/tree/master/samples/DatabaseManagement/Program.py) file of the [DatabaseManagement](https://github.com/Azure/azure-documentdb-python/tree/master/samples/DatabaseManagement) project shows how to perform the following tasks.</span></span>

| <span data-ttu-id="13fd1-124">작업</span><span class="sxs-lookup"><span data-stu-id="13fd1-124">Task</span></span> | <span data-ttu-id="13fd1-125">API 참조</span><span class="sxs-lookup"><span data-stu-id="13fd1-125">API reference</span></span> |
| --- | --- |
| [<span data-ttu-id="13fd1-126">데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="13fd1-126">Create a database</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L65-L76) |[<span data-ttu-id="13fd1-127">document_client.CreateDatabase</span><span class="sxs-lookup"><span data-stu-id="13fd1-127">document_client.CreateDatabase</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |
| [<span data-ttu-id="13fd1-128">데이터베이스에 대한 계정 쿼리</span><span class="sxs-lookup"><span data-stu-id="13fd1-128">Query an account for a database</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L49-L62) |[<span data-ttu-id="13fd1-129">document_client.QueryDatabases</span><span class="sxs-lookup"><span data-stu-id="13fd1-129">document_client.QueryDatabases</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |
| [<span data-ttu-id="13fd1-130">ID에서 데이터베이스 읽기</span><span class="sxs-lookup"><span data-stu-id="13fd1-130">Read a database by Id</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L79-L96) |[<span data-ttu-id="13fd1-131">document_client.ReadDatabase</span><span class="sxs-lookup"><span data-stu-id="13fd1-131">document_client.ReadDatabase</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |
| [<span data-ttu-id="13fd1-132">계정에 대한 데이터베이스 나열</span><span class="sxs-lookup"><span data-stu-id="13fd1-132">List databases for an account</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L99-L110) |[<span data-ttu-id="13fd1-133">document_client.ReadDatabases</span><span class="sxs-lookup"><span data-stu-id="13fd1-133">document_client.ReadDatabases</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |
| [<span data-ttu-id="13fd1-134">데이터베이스 삭제</span><span class="sxs-lookup"><span data-stu-id="13fd1-134">Delete a database</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L113-L126) |[<span data-ttu-id="13fd1-135">document_client.DeleteDatabase</span><span class="sxs-lookup"><span data-stu-id="13fd1-135">document_client.DeleteDatabase</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |

## <a name="collection-examples"></a><span data-ttu-id="13fd1-136">컬렉션 예제</span><span class="sxs-lookup"><span data-stu-id="13fd1-136">Collection examples</span></span>
<span data-ttu-id="13fd1-137">[CollectionManagement](https://github.com/Azure/azure-documentdb-python/tree/master/samples/CollectionManagement) 프로젝트의 [Program.py](https://github.com/Azure/azure-documentdb-python/tree/master/samples/CollectionManagement/Program.py) 파일은 다음 작업을 수행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="13fd1-137">The [Program.py](https://github.com/Azure/azure-documentdb-python/tree/master/samples/CollectionManagement/Program.py) file of the [CollectionManagement](https://github.com/Azure/azure-documentdb-python/tree/master/samples/CollectionManagement) project shows how to perform the following tasks.</span></span>

| <span data-ttu-id="13fd1-138">작업</span><span class="sxs-lookup"><span data-stu-id="13fd1-138">Task</span></span> | <span data-ttu-id="13fd1-139">API 참조</span><span class="sxs-lookup"><span data-stu-id="13fd1-139">API reference</span></span> |
| --- | --- |
| [<span data-ttu-id="13fd1-140">컬렉션 만들기</span><span class="sxs-lookup"><span data-stu-id="13fd1-140">Create a collection</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L84-L135) |[<span data-ttu-id="13fd1-141">document_client.CreateCollection</span><span class="sxs-lookup"><span data-stu-id="13fd1-141">document_client.CreateCollection</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [<span data-ttu-id="13fd1-142">데이터베이스에서 모든 컬렉션의 목록 읽기</span><span class="sxs-lookup"><span data-stu-id="13fd1-142">Read a list of all collections in a database</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L198-L225) |[<span data-ttu-id="13fd1-143">document_client.ListCollections</span><span class="sxs-lookup"><span data-stu-id="13fd1-143">document_client.ListCollections</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [<span data-ttu-id="13fd1-144">ID에서 컬렉션 가져오기</span><span class="sxs-lookup"><span data-stu-id="13fd1-144">Get a collection by Id</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L178-L195) |[<span data-ttu-id="13fd1-145">document_client.ReadCollection</span><span class="sxs-lookup"><span data-stu-id="13fd1-145">document_client.ReadCollection</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [<span data-ttu-id="13fd1-146">컬렉션의 성능 계층 가져오기</span><span class="sxs-lookup"><span data-stu-id="13fd1-146">Get performance tier of a collection</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L139-L161) |[<span data-ttu-id="13fd1-147">DocumentQueryable.QueryOffers</span><span class="sxs-lookup"><span data-stu-id="13fd1-147">DocumentQueryable.QueryOffers</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [<span data-ttu-id="13fd1-148">컬렉션의 성능 계층 변경</span><span class="sxs-lookup"><span data-stu-id="13fd1-148">Change performance tier of a collection</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L163-L175) |[<span data-ttu-id="13fd1-149">document_client.ReplaceOffer</span><span class="sxs-lookup"><span data-stu-id="13fd1-149">document_client.ReplaceOffer</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [<span data-ttu-id="13fd1-150">컬렉션 삭제</span><span class="sxs-lookup"><span data-stu-id="13fd1-150">Delete a collection</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L212-L225) |[<span data-ttu-id="13fd1-151">document_client.DeleteCollection</span><span class="sxs-lookup"><span data-stu-id="13fd1-151">document_client.DeleteCollection</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |


---
title: "Azure Cosmos DB에 대 한 API aaaDocumentDB Python 예제 | Microsoft Docs"
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
ms.openlocfilehash: d8f240782b0997f2d32b68d310dc6f4ff6cb36d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-python-examples"></a><span data-ttu-id="fd611-104">Azure Cosmos DB Python 예제</span><span class="sxs-lookup"><span data-stu-id="fd611-104">Azure Cosmos DB Python examples</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fd611-105">.NET 예제</span><span class="sxs-lookup"><span data-stu-id="fd611-105">.NET Examples</span></span>](documentdb-dotnet-samples.md)
> * [<span data-ttu-id="fd611-106">Node.js 예제</span><span class="sxs-lookup"><span data-stu-id="fd611-106">Node.js Examples</span></span>](documentdb-nodejs-samples.md)
> * [<span data-ttu-id="fd611-107">Python 예제</span><span class="sxs-lookup"><span data-stu-id="fd611-107">Python Examples</span></span>](documentdb-python-samples.md)
> * [<span data-ttu-id="fd611-108">Azure 코드 샘플 갤러리</span><span class="sxs-lookup"><span data-stu-id="fd611-108">Azure Code Sample Gallery</span></span>](https://azure.microsoft.com/documentation/samples/?service=documentdb)
> 
> 

<span data-ttu-id="fd611-109">샘플 솔루션을 CRUD 작업 및 Azure Cosmos DB 리소스에서 기타 일반적인 작업을 수행 하는 hello에 포함 된 [azure-documentdb-python](https://github.com/Azure/azure-documentdb-python/tree/master/samples) GitHub 리포지토리 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd611-109">Sample solutions that perform CRUD operations and other common operations on Azure Cosmos DB resources are included in hello [azure-documentdb-python](https://github.com/Azure/azure-documentdb-python/tree/master/samples) GitHub repository.</span></span> <span data-ttu-id="fd611-110">이 문서는 다음을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fd611-110">This article provides:</span></span>

* <span data-ttu-id="fd611-111">각 hello Python 예제 프로젝트 파일에서 링크 toohello 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="fd611-111">Links toohello tasks in each of hello Python example project files.</span></span> 
* <span data-ttu-id="fd611-112">링크 toohello 관련 API 참조 콘텐츠입니다.</span><span class="sxs-lookup"><span data-stu-id="fd611-112">Links toohello related API reference content.</span></span>

<span data-ttu-id="fd611-113">**필수 구성 요소**</span><span class="sxs-lookup"><span data-stu-id="fd611-113">**Prerequisites**</span></span>

1. <span data-ttu-id="fd611-114">Azure 계정 toouse 이러한 Python 예제 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="fd611-114">You need an Azure account toouse these Python examples:</span></span>
   * <span data-ttu-id="fd611-115">할 수 있습니다 [무료로 Azure 계정을 개설](https://azure.microsoft.com/pricing/free-trial/): 크레딧을 얻게 유료 Azure 서비스 아웃 tootry 사용할 수 있으며 사용 후에 최대 hello 계정 등에 사용 하 여 웹 사이트와 같은 Azure 서비스를 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd611-115">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/): You get credits you can use tootry out paid Azure services, and even after they're used up you can keep hello account and use free Azure services, such as Websites.</span></span> <span data-ttu-id="fd611-116">명시적으로 설정을 변경 하 고 청구 toobe 요청 하지 않는 한 신용 카드, 청구 됩니다 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fd611-116">Your credit card will never be charged, unless you explicitly change your settings and ask toobe charged.</span></span>
     * <span data-ttu-id="fd611-117">[Visual Studio 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)할 수 있음: Visual Studio 구독은 유료 Azure 서비스에 사용할 수 있는 크레딧을 매달 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fd611-117">You can [activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/): Your Visual Studio subscription gives you credits every month that you can use for paid Azure services.</span></span>
2. <span data-ttu-id="fd611-118">또한 hello 해야 [Python SDK](documentdb-sdk-python.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fd611-118">You also need hello [Python SDK](documentdb-sdk-python.md).</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="fd611-119">각 샘플은 자체 포함되며 자체를 설정하고 자체를 정리합니다.</span><span class="sxs-lookup"><span data-stu-id="fd611-119">Each sample is self-contained, it sets itself up and cleans up after itself.</span></span> <span data-ttu-id="fd611-120">이와 같이 hello 샘플 발급 여러 번 호출 너무[document_client 합니다. CreateCollection](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="fd611-120">As such, hello samples issue multiple calls too[document_client.CreateCollection](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html).</span></span> <span data-ttu-id="fd611-121">구독에 영향을 주는 이렇게 될 때마다 생성 되 고 hello 컬렉션의 hello 성능 계층 당 사용량의 1 시간에 대 한 청구 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd611-121">Each time this is done your subscription will be billed for 1 hour of usage per hello performance tier of hello collection being created.</span></span> 
   > 
   > 

## <a name="database-examples"></a><span data-ttu-id="fd611-122">데이터베이스 예제</span><span class="sxs-lookup"><span data-stu-id="fd611-122">Database examples</span></span>
<span data-ttu-id="fd611-123">hello [Program.py](https://github.com/Azure/azure-documentdb-python/tree/master/samples/DatabaseManagement/Program.py) 파일의 hello [DatabaseManagement](https://github.com/Azure/azure-documentdb-python/tree/master/samples/DatabaseManagement) 프로젝트 tooperform hello 다음 작업 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fd611-123">hello [Program.py](https://github.com/Azure/azure-documentdb-python/tree/master/samples/DatabaseManagement/Program.py) file of hello [DatabaseManagement](https://github.com/Azure/azure-documentdb-python/tree/master/samples/DatabaseManagement) project shows how tooperform hello following tasks.</span></span>

| <span data-ttu-id="fd611-124">작업</span><span class="sxs-lookup"><span data-stu-id="fd611-124">Task</span></span> | <span data-ttu-id="fd611-125">API 참조</span><span class="sxs-lookup"><span data-stu-id="fd611-125">API reference</span></span> |
| --- | --- |
| [<span data-ttu-id="fd611-126">데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="fd611-126">Create a database</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L65-L76) |[<span data-ttu-id="fd611-127">document_client.CreateDatabase</span><span class="sxs-lookup"><span data-stu-id="fd611-127">document_client.CreateDatabase</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |
| [<span data-ttu-id="fd611-128">데이터베이스에 대한 계정 쿼리</span><span class="sxs-lookup"><span data-stu-id="fd611-128">Query an account for a database</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L49-L62) |[<span data-ttu-id="fd611-129">document_client.QueryDatabases</span><span class="sxs-lookup"><span data-stu-id="fd611-129">document_client.QueryDatabases</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |
| [<span data-ttu-id="fd611-130">ID에서 데이터베이스 읽기</span><span class="sxs-lookup"><span data-stu-id="fd611-130">Read a database by Id</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L79-L96) |[<span data-ttu-id="fd611-131">document_client.ReadDatabase</span><span class="sxs-lookup"><span data-stu-id="fd611-131">document_client.ReadDatabase</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |
| [<span data-ttu-id="fd611-132">계정에 대한 데이터베이스 나열</span><span class="sxs-lookup"><span data-stu-id="fd611-132">List databases for an account</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L99-L110) |[<span data-ttu-id="fd611-133">document_client.ReadDatabases</span><span class="sxs-lookup"><span data-stu-id="fd611-133">document_client.ReadDatabases</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |
| [<span data-ttu-id="fd611-134">데이터베이스 삭제</span><span class="sxs-lookup"><span data-stu-id="fd611-134">Delete a database</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L113-L126) |[<span data-ttu-id="fd611-135">document_client.DeleteDatabase</span><span class="sxs-lookup"><span data-stu-id="fd611-135">document_client.DeleteDatabase</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |

## <a name="collection-examples"></a><span data-ttu-id="fd611-136">컬렉션 예제</span><span class="sxs-lookup"><span data-stu-id="fd611-136">Collection examples</span></span>
<span data-ttu-id="fd611-137">hello [Program.py](https://github.com/Azure/azure-documentdb-python/tree/master/samples/CollectionManagement/Program.py) 파일의 hello [CollectionManagement](https://github.com/Azure/azure-documentdb-python/tree/master/samples/CollectionManagement) 프로젝트 tooperform hello 다음 작업 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fd611-137">hello [Program.py](https://github.com/Azure/azure-documentdb-python/tree/master/samples/CollectionManagement/Program.py) file of hello [CollectionManagement](https://github.com/Azure/azure-documentdb-python/tree/master/samples/CollectionManagement) project shows how tooperform hello following tasks.</span></span>

| <span data-ttu-id="fd611-138">작업</span><span class="sxs-lookup"><span data-stu-id="fd611-138">Task</span></span> | <span data-ttu-id="fd611-139">API 참조</span><span class="sxs-lookup"><span data-stu-id="fd611-139">API reference</span></span> |
| --- | --- |
| [<span data-ttu-id="fd611-140">컬렉션 만들기</span><span class="sxs-lookup"><span data-stu-id="fd611-140">Create a collection</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L84-L135) |[<span data-ttu-id="fd611-141">document_client.CreateCollection</span><span class="sxs-lookup"><span data-stu-id="fd611-141">document_client.CreateCollection</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [<span data-ttu-id="fd611-142">데이터베이스에서 모든 컬렉션의 목록 읽기</span><span class="sxs-lookup"><span data-stu-id="fd611-142">Read a list of all collections in a database</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L198-L225) |[<span data-ttu-id="fd611-143">document_client.ListCollections</span><span class="sxs-lookup"><span data-stu-id="fd611-143">document_client.ListCollections</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [<span data-ttu-id="fd611-144">ID에서 컬렉션 가져오기</span><span class="sxs-lookup"><span data-stu-id="fd611-144">Get a collection by Id</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L178-L195) |[<span data-ttu-id="fd611-145">document_client.ReadCollection</span><span class="sxs-lookup"><span data-stu-id="fd611-145">document_client.ReadCollection</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [<span data-ttu-id="fd611-146">컬렉션의 성능 계층 가져오기</span><span class="sxs-lookup"><span data-stu-id="fd611-146">Get performance tier of a collection</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L139-L161) |[<span data-ttu-id="fd611-147">DocumentQueryable.QueryOffers</span><span class="sxs-lookup"><span data-stu-id="fd611-147">DocumentQueryable.QueryOffers</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [<span data-ttu-id="fd611-148">컬렉션의 성능 계층 변경</span><span class="sxs-lookup"><span data-stu-id="fd611-148">Change performance tier of a collection</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L163-L175) |[<span data-ttu-id="fd611-149">document_client.ReplaceOffer</span><span class="sxs-lookup"><span data-stu-id="fd611-149">document_client.ReplaceOffer</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [<span data-ttu-id="fd611-150">컬렉션 삭제</span><span class="sxs-lookup"><span data-stu-id="fd611-150">Delete a collection</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L212-L225) |[<span data-ttu-id="fd611-151">document_client.DeleteCollection</span><span class="sxs-lookup"><span data-stu-id="fd611-151">document_client.DeleteCollection</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |


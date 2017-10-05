---
title: "MongoDB API의 Azure Cosmos DB 전역 배포 자습서 | Microsoft Docs"
description: "MongoDB API를 사용하여 Azure Cosmos DB 전역 배포를 설정하는 방법에 대해 알아봅니다."
services: cosmos-db
keywords: "전역 배포, MongoDB"
documentationcenter: 
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 8b815047-2868-4b10-af1d-40a1af419a70
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: a2747102f4d8cac412b67abc3fd07cfa3661bcee
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-setup-azure-cosmos-db-global-distribution-using-the-mongodb-api"></a><span data-ttu-id="88978-104">MongoDB API를 사용하여 Azure Cosmos DB 전역 배포를 설정하는 방법</span><span class="sxs-lookup"><span data-stu-id="88978-104">How to setup Azure Cosmos DB global distribution using the MongoDB API</span></span>

<span data-ttu-id="88978-105">이 문서에서는 Azure Portal을 사용하여 Azure Cosmos DB 전역 배포를 설정한 다음 MongoDB API를 사용하여 연결하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="88978-105">In this article, we show how to use the Azure portal to setup Azure Cosmos DB global distribution and then connect using the MongoDB API.</span></span>

<span data-ttu-id="88978-106">이 문서에서 다루는 작업은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="88978-106">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="88978-107">Azure Portal을 사용하여 전역 배포 구성</span><span class="sxs-lookup"><span data-stu-id="88978-107">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="88978-108">[MongoDB API](mongodb-introduction.md)를 사용하여 전역 배포 구성</span><span class="sxs-lookup"><span data-stu-id="88978-108">Configure global distribution using the [MongoDB API](mongodb-introduction.md)</span></span>

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]

## <a name="verifying-your-regional-setup-using-the-mongodb-api"></a><span data-ttu-id="88978-109">MongoDB API를 사용하여 지역별 설정 확인</span><span class="sxs-lookup"><span data-stu-id="88978-109">Verifying your regional setup using the MongoDB API</span></span>
<span data-ttu-id="88978-110">MongoDB API 내에서 글로벌 구성을 이중 확인하는 가장 간단한 방법은 Mongo Shell에서 *isMaster()* 명령을 실행하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="88978-110">The simplest way of double checking your global configuration within API for MongoDB is to run the *isMaster()* command from the Mongo Shell.</span></span>

<span data-ttu-id="88978-111">Mongo Shell에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="88978-111">From your Mongo Shell:</span></span>

   ```
      db.isMaster()
   ```
   
<span data-ttu-id="88978-112">결과 예:</span><span class="sxs-lookup"><span data-stu-id="88978-112">Example results:</span></span>

   ```JSON
      {
         "_t": "IsMasterResponse",
         "ok": 1,
         "ismaster": true,
         "maxMessageSizeBytes": 4194304,
         "maxWriteBatchSize": 1000,
         "minWireVersion": 0,
         "maxWireVersion": 2,
         "tags": {
            "region": "South India"
         },
         "hosts": [
            "vishi-api-for-mongodb-southcentralus.documents.azure.com:10255",
            "vishi-api-for-mongodb-westeurope.documents.azure.com:10255",
            "vishi-api-for-mongodb-southindia.documents.azure.com:10255"
         ],
         "setName": "globaldb",
         "setVersion": 1,
         "primary": "vishi-api-for-mongodb-southindia.documents.azure.com:10255",
         "me": "vishi-api-for-mongodb-southindia.documents.azure.com:10255"
      }
   ```

## <a name="connecting-to-a-preferred-region-using-the-mongodb-api"></a><span data-ttu-id="88978-113">MongoDB API를 사용하여 기본 설정 지역에 연결</span><span class="sxs-lookup"><span data-stu-id="88978-113">Connecting to a preferred region using the MongoDB API</span></span>

<span data-ttu-id="88978-114">MongoDB API를 사용하면 전역적으로 분산된 데이터베이스에 대한 컬렉션의 읽기 기본 설정을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88978-114">The MongoDB API enables you to specify your collection's read preference for a globally distributed database.</span></span> <span data-ttu-id="88978-115">짧은 대기 시간 읽기 및 글로벌 고가용성을 위해 컬렉션의 읽기 기본 설정을 *nearest*(최근접)로 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="88978-115">For both low latency reads and global high availability, we recommend setting your collection's read preference to *nearest*.</span></span> <span data-ttu-id="88978-116">*nearest*(최근접)의 읽기 기본 설정은 가장 가까운 지역에서 읽도록 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="88978-116">A read preference of *nearest* is configured to read from the closest region.</span></span>

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.Nearest));
```

<span data-ttu-id="88978-117">주 읽기/쓰기 지역 및 재해 복구(DR) 시나리오를 위한 보조 지역이 있는 응용 프로그램에는 컬렉션의 읽기 기본 설정을 *secondary preferred*(보조 기본 설정)로 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="88978-117">For applications with a primary read/write region and a secondary region for disaster recovery (DR) scenarios, we recommend setting your collection's read preference to *secondary preferred*.</span></span> <span data-ttu-id="88978-118">*secondary preferred*(보조 기본 설정)의 읽기 기본 설정은 주 지역의 데이터를 사용할 수 없는 경우 보조 지역에서 읽도록 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="88978-118">A read preference of *secondary preferred* is configured to read from the secondary region when the primary region is unavailable.</span></span>

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.SecondaryPreferred));
```

<span data-ttu-id="88978-119">마지막으로 읽기 지역을 수동으로 지정하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="88978-119">Lastly, if you would like to manually specify your read regions.</span></span> <span data-ttu-id="88978-120">읽기 기본 설정 내에서 지역 태그를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88978-120">You can set the region Tag within your read preference.</span></span>

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
var tag = new Tag("region", "Southeast Asia");
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.Secondary, new[] { new TagSet(new[] { tag }) }));
```

<span data-ttu-id="88978-121">이것으로 끝이며, 이 자습서를 완료했습니다!</span><span class="sxs-lookup"><span data-stu-id="88978-121">That's it, that completes this tutorial.</span></span> <span data-ttu-id="88978-122">[Azure Cosmos DB의 일관성 수준](consistency-levels.md)을 참조하여 전역적으로 복제한 계정의 일관성을 관리하는 방법에 대해 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88978-122">You can learn how to manage the consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="88978-123">그리고 Azure Cosmos DB에서 전역 데이터베이스 복제가 작동하는 방법에 대한 자세한 내용은 [Azure Cosmos DB를 사용하여 전역적으로 데이터 배포](distribute-data-globally.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="88978-123">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="88978-124">다음 단계</span><span class="sxs-lookup"><span data-stu-id="88978-124">Next steps</span></span>

<span data-ttu-id="88978-125">이 자습서에서는 다음을 수행했습니다.</span><span class="sxs-lookup"><span data-stu-id="88978-125">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="88978-126">Azure Portal을 사용하여 전역 배포 구성</span><span class="sxs-lookup"><span data-stu-id="88978-126">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="88978-127">DocumentDB API를 사용하여 전역 배포 구성</span><span class="sxs-lookup"><span data-stu-id="88978-127">Configure global distribution using the DocumentDB APIs</span></span>

<span data-ttu-id="88978-128">이제 다음 자습서로 진행하여 Azure Cosmos DB 로컬 에뮬레이터를 사용하여 로컬로 개발하는 방법에 대해 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88978-128">You can now proceed to the next tutorial to learn how to develop locally using the Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="88978-129">에뮬레이터를 사용하여 로컬로 개발</span><span class="sxs-lookup"><span data-stu-id="88978-129">Develop locally with the emulator</span></span>](local-emulator.md)
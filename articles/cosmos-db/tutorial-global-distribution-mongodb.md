---
title: "MongoDB API에 대 한 aaaAzure Cosmos DB 글로벌 메일 자습서 | Microsoft Docs"
description: "어떻게 MongoDB API를 사용 하 여 toosetup Azure Cosmos DB 글로벌 메일 hello에 대해 알아봅니다."
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
ms.openlocfilehash: 0fc2d670bb4e21ac5f813f9586b407ba06ccf354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-mongodb-api"></a><span data-ttu-id="9742a-104">어떻게 MongoDB API를 사용 하 여 toosetup Azure Cosmos DB 글로벌 메일 hello</span><span class="sxs-lookup"><span data-stu-id="9742a-104">How toosetup Azure Cosmos DB global distribution using hello MongoDB API</span></span>

<span data-ttu-id="9742a-105">이 문서에서는 toouse hello Azure 포털 toosetup Azure Cosmos DB 글로벌 배포 하 고 다음 hello MongoDB API를 사용 하 여를 연결 하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="9742a-105">In this article, we show how toouse hello Azure portal toosetup Azure Cosmos DB global distribution and then connect using hello MongoDB API.</span></span>

<span data-ttu-id="9742a-106">이 문서에서는 다음 작업 hello를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="9742a-106">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="9742a-107">Hello Azure 포털을 사용 하 여 글로벌 배포를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="9742a-107">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="9742a-108">Hello를 사용 하 여 글로벌 배포를 구성 [MongoDB API](mongodb-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="9742a-108">Configure global distribution using hello [MongoDB API](mongodb-introduction.md)</span></span>

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]

## <a name="verifying-your-regional-setup-using-hello-mongodb-api"></a><span data-ttu-id="9742a-109">Hello MongoDB API를 사용 하 여 국가별 설치 확인</span><span class="sxs-lookup"><span data-stu-id="9742a-109">Verifying your regional setup using hello MongoDB API</span></span>
<span data-ttu-id="9742a-110">MongoDB toorun hello에 대 한 API 내에서 전역 구성을 검사 하는 double의 가장 간단한 방법은 hello *isMaster()* hello Mongo 셸 명령을 합니다.</span><span class="sxs-lookup"><span data-stu-id="9742a-110">hello simplest way of double checking your global configuration within API for MongoDB is toorun hello *isMaster()* command from hello Mongo Shell.</span></span>

<span data-ttu-id="9742a-111">Mongo Shell에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9742a-111">From your Mongo Shell:</span></span>

   ```
      db.isMaster()
   ```
   
<span data-ttu-id="9742a-112">결과 예:</span><span class="sxs-lookup"><span data-stu-id="9742a-112">Example results:</span></span>

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

## <a name="connecting-tooa-preferred-region-using-hello-mongodb-api"></a><span data-ttu-id="9742a-113">Hello MongoDB API를 사용 하 여 tooa 기본 영역 연결</span><span class="sxs-lookup"><span data-stu-id="9742a-113">Connecting tooa preferred region using hello MongoDB API</span></span>

<span data-ttu-id="9742a-114">hello MongoDB API를 사용 하면 있습니다 toospecify 세계적으로 분산 된 데이터베이스에 대 한 컬렉션의 읽기 기본 설정.</span><span class="sxs-lookup"><span data-stu-id="9742a-114">hello MongoDB API enables you toospecify your collection's read preference for a globally distributed database.</span></span> <span data-ttu-id="9742a-115">컬렉션의 읽기 기본 설정 지정 너무 권장 읽기 대기 시간 및 전역 높은 가용성, 낮은 둘 다에 대 한*가장 가까운*합니다.</span><span class="sxs-lookup"><span data-stu-id="9742a-115">For both low latency reads and global high availability, we recommend setting your collection's read preference too*nearest*.</span></span> <span data-ttu-id="9742a-116">기본 설정을 읽기 *가장 가까운* hello 가장 가까운 영역에서 구성 된 tooread 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9742a-116">A read preference of *nearest* is configured tooread from hello closest region.</span></span>

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.Nearest));
```

<span data-ttu-id="9742a-117">응용 프로그램을 기본 읽기/쓰기가 지역과 보조 지역에 대 한 재해 복구 (DR) 시나리오에 대 한 컬렉션의 읽기 기본 설정 지정 너무는 것이 좋습니다*선호 하는 보조*합니다.</span><span class="sxs-lookup"><span data-stu-id="9742a-117">For applications with a primary read/write region and a secondary region for disaster recovery (DR) scenarios, we recommend setting your collection's read preference too*secondary preferred*.</span></span> <span data-ttu-id="9742a-118">읽기 기본 설정을 *선호 하는 보조* hello 기본 지역에 사용할 수 없는 경우 hello 보조 지역에서 구성 된 tooread는 합니다.</span><span class="sxs-lookup"><span data-stu-id="9742a-118">A read preference of *secondary preferred* is configured tooread from hello secondary region when hello primary region is unavailable.</span></span>

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.SecondaryPreferred));
```

<span data-ttu-id="9742a-119">마지막으로 지정 하면 읽기 영역 toomanually와 같은 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="9742a-119">Lastly, if you would like toomanually specify your read regions.</span></span> <span data-ttu-id="9742a-120">Hello 지역 태그 읽기 기본 설정 내에서 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9742a-120">You can set hello region Tag within your read preference.</span></span>

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
var tag = new Tag("region", "Southeast Asia");
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.Secondary, new[] { new TagSet(new[] { tag }) }));
```

<span data-ttu-id="9742a-121">이것으로 끝이며, 이 자습서를 완료했습니다!</span><span class="sxs-lookup"><span data-stu-id="9742a-121">That's it, that completes this tutorial.</span></span> <span data-ttu-id="9742a-122">읽어 toomanage 전역적으로 복제 된 계정의 일관성 hello 하는 방법을 학습할 수 있는 [Azure Cosmos DB의 일관성 수준](consistency-levels.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9742a-122">You can learn how toomanage hello consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="9742a-123">그리고 Azure Cosmos DB에서 전역 데이터베이스 복제가 작동하는 방법에 대한 자세한 내용은 [Azure Cosmos DB를 사용하여 전역적으로 데이터 배포](distribute-data-globally.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9742a-123">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9742a-124">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9742a-124">Next steps</span></span>

<span data-ttu-id="9742a-125">이 자습서에서는 hello 다음 작업을 수행 하면:</span><span class="sxs-lookup"><span data-stu-id="9742a-125">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9742a-126">Hello Azure 포털을 사용 하 여 글로벌 배포를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="9742a-126">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="9742a-127">Hello DocumentDB Api를 사용 하 여 글로벌 배포를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="9742a-127">Configure global distribution using hello DocumentDB APIs</span></span>

<span data-ttu-id="9742a-128">다음 자습서 toolearn toohello 이제 진행할 수 있습니다 어떻게 사용 하 여 로컬로 toodevelop hello Azure Cosmos DB의 로컬 에뮬레이터입니다.</span><span class="sxs-lookup"><span data-stu-id="9742a-128">You can now proceed toohello next tutorial toolearn how toodevelop locally using hello Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9742a-129">Hello 에뮬레이터를 사용 하 여 로컬 개발</span><span class="sxs-lookup"><span data-stu-id="9742a-129">Develop locally with hello emulator</span></span>](local-emulator.md)

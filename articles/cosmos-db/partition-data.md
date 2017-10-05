---
title: "Azure Cosmos DB에서 분할 및 수평적 확장 | Microsoft Docs"
description: "Azure Cosmos DB에서 분할 작동 방법, 분할 및 파티션 키를 구성하는 방법 및 응용 프로그램에 대한 올바른 파티션 키를 선택하는 방법에 대해 알아봅니다."
services: cosmos-db
author: arramac
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: cac9a8cd-b5a3-4827-8505-d40bb61b2416
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: arramac
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e2d2847276e553d7511241ff323c3e00aad8e5c9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-partition-and-scale-in-azure-cosmos-db"></a><span data-ttu-id="6609a-103">Azure Cosmos DB에서 분할 및 확장하는 방법</span><span class="sxs-lookup"><span data-stu-id="6609a-103">How to partition and scale in Azure Cosmos DB</span></span>

<span data-ttu-id="6609a-104">[Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/)는 전역적으로 배포된 다중 모델 데이터베이스 서비스로써 신속하고 예측 가능한 성능을 얻을 수 있고, 응용 프로그램 증가에 따라 효율적인 확장이 가능하도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-104">[Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) is a global distributed, multi-model database service designed to help you achieve fast, predictable performance and scale seamlessly along with your application as it grows.</span></span> <span data-ttu-id="6609a-105">이 문서에서는 Azure Cosmos DB에서 모든 데이터 모델에 분할이 작동하는 방식을 개괄적으로 살펴보고, 응용 프로그램을 효과적으로 확장하도록 Azure Cosmos DB 컨테이너를 구성하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-105">This article provides an overview of how partitioning works for all the data models in Azure Cosmos DB, and describes how you can configure Azure Cosmos DB containers to effectively scale your applications.</span></span>

<span data-ttu-id="6609a-106">Scott Hanselman과 Azure Cosmos DB 수석 엔지니어링 관리자 Shireesh Thota가 진행하는 이 Azure Friday 비디오에서는 분할 및 파티션 키에 대해서도 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-106">Partitioning and partition keys are also covered in this Azure Friday video with Scott Hanselman and Azure Cosmos DB Principal Engineering Manager, Shireesh Thota.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-DocumentDB-Elastic-Scale-Partitioning/player]
> 

## <a name="partitioning-in-azure-cosmos-db"></a><span data-ttu-id="6609a-107">Azure Cosmos DB에서 분할</span><span class="sxs-lookup"><span data-stu-id="6609a-107">Partitioning in Azure Cosmos DB</span></span>
<span data-ttu-id="6609a-108">Azure Cosmos DB에서는 규모에 상관없이 밀리초 단위의 응답 시간 순으로 스키마 없는 데이터를 저장하고 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-108">In Azure Cosmos DB, you can store and query schema-less data with order-of-millisecond response times at any scale.</span></span> <span data-ttu-id="6609a-109">Cosmos DB는 **컬렉션(문서의 경우), 그래프 및 표**라는 데이터 저장용 컨테이너를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-109">Cosmos DB provides containers for storing data called **collections (for document), graphs, or tables**.</span></span> <span data-ttu-id="6609a-110">컨테이너는 하나 이상의 물리적 파티션 또는 서버에 걸쳐 있을 수 있는 논리적 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-110">Containers are logical resources and can span one or more physical partitions or servers.</span></span> <span data-ttu-id="6609a-111">파티션 수는 컨테이너의 프로비전된 처리량 및 저장소 크기에 따라 Cosmos DB에 의해 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-111">The number of partitions is determined by Cosmos DB based on the storage size and the provisioned throughput of the container.</span></span> <span data-ttu-id="6609a-112">Cosmos DB의 모든 파티션은 고정된 양의 SSD 지원 저장소에 연결되며, 고가용성을 위해 복제됩니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-112">Every partition in Cosmos DB has a fixed amount of SSD-backed storage associated with it, and is replicated for high availability.</span></span> <span data-ttu-id="6609a-113">파티션 관리는 Azure Cosmos DB에 의해 완전히 관리되므로 복잡한 코드를 작성하거나 파티션을 관리할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-113">Partition management is fully managed by Azure Cosmos DB, and you do not have to write complex code or manage your partitions.</span></span> <span data-ttu-id="6609a-114">Cosmos DB 컨테이너는 처리량 및 저장소 면에서 제한되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-114">Cosmos DB containers are unlimited in terms of storage and throughput.</span></span> 

![horizontal](./media/introduction/azure-cosmos-db-partitioning.png) 

<span data-ttu-id="6609a-116">분할은 응용 프로그램에 대해 투명합니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-116">Partitioning is transparent to your application.</span></span> <span data-ttu-id="6609a-117">Cosmos DB는 빠른 읽기 및 쓰기, 쿼리, 트랜잭션 논리, 일관성 수준 및 단일 컨테이너 리소스에 대한 메서드/API를 통해 세분화된 액세스 제어를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-117">Cosmos DB supports fast reads and writes, queries, transactional logic, consistency levels, and fine-grained access control via methods/APIs to a single container resource.</span></span> <span data-ttu-id="6609a-118">이 서비스는 파티션 간의 데이터 분산 및 올바른 파티션에 대한 쿼리 요청을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-118">The service handles distributing data across partitions and routing query requests to the right partition.</span></span> 

<span data-ttu-id="6609a-119">분할은 어떻게 작동하나요?</span><span class="sxs-lookup"><span data-stu-id="6609a-119">How does partitioning work?</span></span> <span data-ttu-id="6609a-120">각 항목에는 파티션 키 및 행 키가 있어서 항목을 고유하게 식별해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-120">Each item must have a partition key and a row key, which uniquely identify it.</span></span> <span data-ttu-id="6609a-121">파티션 키는 데이터에 대한 논리적 분할의 역할을 하고 파티션 간에 데이터를 배포하는 자연 경계를 가진 Cosmos DB를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-121">Your partition key acts as a logical partition for your data, and provides Cosmos DB with a natural boundary for distributing data across partitions.</span></span> <span data-ttu-id="6609a-122">간단히 말해, Azure Cosmos DB에서 분할의 작동 방식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-122">In brief, here is how partitioning works in Azure Cosmos DB:</span></span>

* <span data-ttu-id="6609a-123">`T` 요청/초 처리량으로 Cosmos DB 컨테이너를 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-123">You provision a Cosmos DB container with `T` requests/s throughput</span></span>
* <span data-ttu-id="6609a-124">Cosmos DB는 내부적으로 `T` 요청/초를 제공하는 데 필요한 파티션을 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-124">Behind the scenes, Cosmos DB provisions partitions needed to serve `T` requests/s.</span></span> <span data-ttu-id="6609a-125">`T`이 파티션당 최대 처리량 `t`보다 높은 경우 Cosmos DB는 `N` = `T/t` 파티션을 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-125">If `T` is higher than the maximum throughput per partition `t`, then Cosmos DB provisions `N` = `T/t` partitions</span></span>
* <span data-ttu-id="6609a-126">Cosmos DB는 `N` 파티션에 걸쳐 균등하게 파티션 키 해시의 주요 공간을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-126">Cosmos DB allocates the key space of partition key hashes evenly across the `N` partitions.</span></span> <span data-ttu-id="6609a-127">따라서 각 파티션(실제 파티션)은 1-N 파티션 키 값(논리 파티션)을 호스팅합니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-127">So, each partition (physical partition) hosts 1-N partition key values (logical partitions)</span></span>
* <span data-ttu-id="6609a-128">실제 파티션 `p`이 저장 한도에 도달하는 경우 Cosmos DB는 `p`를 `p1` 및 `p2`라는 두 개의 새 파티션으로 원활하게 나누고 각 파티션에 대해 약 절반의 키에 해당하는 값을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-128">When a physical partition `p` reaches its storage limit, Cosmos DB seamlessly splits `p` into two new partitions `p1` and `p2` and distributes values corresponding to roughly half the keys to each of the partitions.</span></span> <span data-ttu-id="6609a-129">이 분리 작업은 응용 프로그램에 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-129">This split operation is invisible to your application.</span></span>
* <span data-ttu-id="6609a-130">마찬가지로 `t*N`보다 높은 처리량을 프로비전할 경우 Cosmos DB는 더 높은 처리량을 지원하기 위해 하나 이상의 파티션을 나눕니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-130">Similarly, when you provision throughput higher than `t*N` throughput, Cosmos DB splits one or more of your partitions to support the higher throughput</span></span>

<span data-ttu-id="6609a-131">파티션 키의 의미 체계는 다음 표에 나와 있는 것처럼 각 API의 의미 체계와 약간 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-131">The semantics for partition keys are slightly different to match the semantics of each API, as shown in the following table:</span></span>

| <span data-ttu-id="6609a-132">API</span><span class="sxs-lookup"><span data-stu-id="6609a-132">API</span></span> | <span data-ttu-id="6609a-133">Partition Key</span><span class="sxs-lookup"><span data-stu-id="6609a-133">Partition Key</span></span> | <span data-ttu-id="6609a-134">Row Key</span><span class="sxs-lookup"><span data-stu-id="6609a-134">Row Key</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6609a-135">DocumentDB</span><span class="sxs-lookup"><span data-stu-id="6609a-135">DocumentDB</span></span> | <span data-ttu-id="6609a-136">custom partition key path</span><span class="sxs-lookup"><span data-stu-id="6609a-136">custom partition key path</span></span> | <span data-ttu-id="6609a-137">fixed `id`</span><span class="sxs-lookup"><span data-stu-id="6609a-137">fixed `id`</span></span> | 
| <span data-ttu-id="6609a-138">MongoDB</span><span class="sxs-lookup"><span data-stu-id="6609a-138">MongoDB</span></span> | <span data-ttu-id="6609a-139">custom shard key</span><span class="sxs-lookup"><span data-stu-id="6609a-139">custom shard key</span></span>  | <span data-ttu-id="6609a-140">fixed `_id`</span><span class="sxs-lookup"><span data-stu-id="6609a-140">fixed `_id`</span></span> | 
| <span data-ttu-id="6609a-141">그래프</span><span class="sxs-lookup"><span data-stu-id="6609a-141">Graph</span></span> | <span data-ttu-id="6609a-142">custom partition key property</span><span class="sxs-lookup"><span data-stu-id="6609a-142">custom partition key property</span></span> | <span data-ttu-id="6609a-143">fixed `id`</span><span class="sxs-lookup"><span data-stu-id="6609a-143">fixed `id`</span></span> | 
| <span data-ttu-id="6609a-144">테이블</span><span class="sxs-lookup"><span data-stu-id="6609a-144">Table</span></span> | <span data-ttu-id="6609a-145">fixed `PartitionKey`</span><span class="sxs-lookup"><span data-stu-id="6609a-145">fixed `PartitionKey`</span></span> | <span data-ttu-id="6609a-146">fixed `RowKey`</span><span class="sxs-lookup"><span data-stu-id="6609a-146">fixed `RowKey`</span></span> | 

<span data-ttu-id="6609a-147">Cosmos DB는 해시 기반 분할을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-147">Cosmos DB uses hash-based partitioning.</span></span> <span data-ttu-id="6609a-148">항목을 작성하는 경우 Cosmos DB는 파티션 키 값을 해시하고 해시된 결과를 사용하여 항목을 저장할 파티션을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-148">When you write an item, Cosmos DB hashes the partition key value and use the hashed result to determine which partition to store the item in.</span></span> <span data-ttu-id="6609a-149">Cosmos DB는 동일한 실제 파티션에 동일한 파티션 키를 가진 모든 항목을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-149">Cosmos DB stores all items with the same partition key in the same physical partition.</span></span> <span data-ttu-id="6609a-150">파티션 키의 선택은 디자인 타임에서 결정해야 하는 중요한 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-150">The choice of the partition key is an important decision that you have to make at design time.</span></span> <span data-ttu-id="6609a-151">다양한 범위의 값과 균일한 액세스 패턴을 가진 속성 이름을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-151">You must pick a property name that has a wide range of values and has even access patterns.</span></span>

> [!NOTE]
> <span data-ttu-id="6609a-152">많은 고유 값(최소한 수백~수천 개)을 가진 파티션 키를 갖는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-152">It is a best practice to have a partition key with many distinct values (100s-1000s at a minimum).</span></span>
>

<span data-ttu-id="6609a-153">Azure Cosmos DB 컨테이너를 "고정" 또는 "무제한"으로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-153">Azure Cosmos DB containers can be created as "fixed" or "unlimited."</span></span> <span data-ttu-id="6609a-154">고정 크기 컨테이너는 최대 제한 10GB 및 10,000RU/s 처리량을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-154">Fixed-size containers have a maximum limit of 10 GB and 10,000 RU/s throughput.</span></span> <span data-ttu-id="6609a-155">일부 API를 사용하면 고정된 크기의 컨테이너에서 파티션 키를 생략할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-155">Some APIs allow the partition key to be omitted for fixed-size containers.</span></span> <span data-ttu-id="6609a-156">무제한으로 컨테이너를 만들려면 최소 처리량 2500RU/s를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-156">To create a container as unlimited, you must specify a minimum throughput of 2500 RU/s.</span></span>

## <a name="partitioning-and-provisioned-throughput"></a><span data-ttu-id="6609a-157">분할 및 프로비전된 처리량</span><span class="sxs-lookup"><span data-stu-id="6609a-157">Partitioning and provisioned throughput</span></span>
<span data-ttu-id="6609a-158">Cosmos DB는 예측 가능한 성능을 위해 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-158">Cosmos DB is designed for predictable performance.</span></span> <span data-ttu-id="6609a-159">컨테이너를 만들 때 **RU/m의 잠재적인 기능으로 초당 [요청 단위](request-units.md)(RU)** 측면에서 처리량을 예약합니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-159">When you create a container, you reserve throughput in terms of **[request units](request-units.md) (RU) per second with a potential add-on for RU per minute**.</span></span> <span data-ttu-id="6609a-160">각 요청에는 작업에 소비된 CPU, 메모리 및 IO 같은 시스템 리소스의 양에 비례하는 요청 단위 요금이 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-160">Each request is assigned a request unit charge that is proportionate to the amount of system resources like CPU, Memory, and IO consumed by the operation.</span></span> <span data-ttu-id="6609a-161">세션 일관성에 따라 1KB 문서를 읽을 경우 1RU(요청 단위)가 소비됩니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-161">A read of a 1-KB document with Session consistency consumes one request unit.</span></span> <span data-ttu-id="6609a-162">저장된 항목 수 또는 동시에 실행되는 요청 수에 상관없이 읽기당 1RU입니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-162">A read is 1 RU regardless of the number of items stored or the number of concurrent requests running at the same time.</span></span> <span data-ttu-id="6609a-163">항목의 크기가 클수록 크기에 따라 더 높은 요청 단위가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-163">Larger items require higher request units depending on the size.</span></span> <span data-ttu-id="6609a-164">응용 프로그램에 지원해야 하는 엔터티 크기 및 읽기 수를 알고 있는 경우 응용 프로그램의 읽기 요구 사항에 필요한 정확한 양의 처리량을 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-164">If you know the size of your entities and the number of reads you need to support for your application, you can provision the exact amount of throughput required for your application's read needs.</span></span> 

> [!NOTE]
> <span data-ttu-id="6609a-165">컨테이너의 전체 처리량을 달성하려면 다양한 파티션 키 값 간에 요청을 균등하게 분산시킬 수 있는 파티션 키를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-165">To achieve the full throughput of the container, you must choose a partition key that allows you to evenly distribute requests among some distinct partition key values.</span></span>
> 
> 

<a name="designing-for-partitioning"></a>
## <a name="working-with-the-azure-cosmos-db-apis"></a><span data-ttu-id="6609a-166">Azure Cosmos DB API 사용</span><span class="sxs-lookup"><span data-stu-id="6609a-166">Working with the Azure Cosmos DB APIs</span></span>
<span data-ttu-id="6609a-167">Azure Portal 또는 Azure CLI를 사용하여 언제든지 컨테이너를 만들고 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-167">You can use the Azure portal or Azure CLI to create containers and scale them at any time.</span></span> <span data-ttu-id="6609a-168">이 섹션에서는 컨테이너를 만들고 각 지원되는 API의 처리량 및 파티션 키 정의를 지정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-168">This section shows how to create containers and specify the throughput and partition key definition in each of the supported APIs.</span></span>

### <a name="documentdb-api"></a><span data-ttu-id="6609a-169">DocumentDB API</span><span class="sxs-lookup"><span data-stu-id="6609a-169">DocumentDB API</span></span>
<span data-ttu-id="6609a-170">다음 샘플에서는 DocumentDB API를 사용하여 컨테이너(컬렉션)를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-170">The following sample shows how to create a container (collection) using the DocumentDB API.</span></span> <span data-ttu-id="6609a-171">[DocumentDB API를 사용하여 분할](partition-data.md)에서 자세한 내용을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-171">You can find more details in [Partitioning with DocumentDB API](partition-data.md).</span></span>

```csharp
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey);
await client.CreateDatabaseAsync(new Database { Id = "db" });

DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 20000 });
```

<span data-ttu-id="6609a-172">REST API에서 `GET` 메서드 또는 SDK 중 하나에서 `ReadDocumentAsync`를 사용하여 항목(문서)을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-172">You can read an item (document) using the `GET` method in the REST API or using `ReadDocumentAsync` in one of the SDKs.</span></span>

```csharp
// Read document. Needs the partition key and the ID to be specified
DeviceReading document = await client.ReadDocumentAsync<DeviceReading>(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });
```

### <a name="mongodb-api"></a><span data-ttu-id="6609a-173">MongoDB API</span><span class="sxs-lookup"><span data-stu-id="6609a-173">MongoDB API</span></span>
<span data-ttu-id="6609a-174">MongoDB API를 사용하면 선호하는 도구, 드라이버 또는 SDK를 통해 공유 컬렉션을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-174">With the MongoDB API, you can create a sharded collection through your favorite tool, driver, or SDK.</span></span> <span data-ttu-id="6609a-175">이 예에서는 Mongo Shell을 사용하여 컬렉션을 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-175">In this example, we use the Mongo Shell for the collection creation.</span></span>

<span data-ttu-id="6609a-176">Mongo Shell에서:</span><span class="sxs-lookup"><span data-stu-id="6609a-176">In the Mongo Shell:</span></span>

```
db.runCommand( { shardCollection: "admin.people", key: { region: "hashed" } } )
```
    
<span data-ttu-id="6609a-177">결과:</span><span class="sxs-lookup"><span data-stu-id="6609a-177">Results:</span></span>

```JSON
{
    "_t" : "ShardCollectionResponse",
    "ok" : 1,
    "collectionsharded" : "admin.people"
}
```

### <a name="table-api"></a><span data-ttu-id="6609a-178">테이블 API</span><span class="sxs-lookup"><span data-stu-id="6609a-178">Table API</span></span>

<span data-ttu-id="6609a-179">테이블 API에서 응용 프로그램의 appSettings 구성에 있는 테이블의 처리량을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-179">With the Table API, you specify the throughput for tables in the appSettings configuration for your application:</span></span>

```xml
<configuration>
    <appSettings>
      <!--Table creation options -->
      <add key="TableThroughput" value="700"/>
    </appSettings>
</configuration>
```

<span data-ttu-id="6609a-180">그런 다음 Azure Table Storage SDK를 사용하여 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-180">Then you create a table using the Azure Table storage SDK.</span></span> <span data-ttu-id="6609a-181">파티션 키는 암시적으로 `PartitionKey` 값으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-181">The partition key is implicitly created as the `PartitionKey` value.</span></span> 

```csharp
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

CloudTable table = tableClient.GetTableReference("people");
table.CreateIfNotExists();
```

<span data-ttu-id="6609a-182">다음 코드 조각을 사용하여 단일 엔터티를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-182">You can retrieve a single entity using the following snippet:</span></span>

```csharp
// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute the retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);
```
<span data-ttu-id="6609a-183">자세한 내용은 [테이블 API를 사용하여 개발](tutorial-develop-table-dotnet.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6609a-183">See [Developing with the Table API](tutorial-develop-table-dotnet.md) for more details.</span></span>

### <a name="graph-api"></a><span data-ttu-id="6609a-184">그래프 API</span><span class="sxs-lookup"><span data-stu-id="6609a-184">Graph API</span></span>

<span data-ttu-id="6609a-185">Graph API에서 Azure Portal 또는 CLI를 사용하여 컨테이너를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-185">With the Graph API, you must use the Azure portal or CLI to create containers.</span></span> <span data-ttu-id="6609a-186">또는 Azure Cosmos DB가 다중 모델이므로 다른 모델 중 하나를 사용하여 그래프 컨테이너를 만들고 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-186">Alternatively, since Azure Cosmos DB is multi-model, you can use one of the other models to create and scale your graph container.</span></span>

<span data-ttu-id="6609a-187">Gremlin에서 파티션 키 및 ID를 사용하여 꼭짓점 또는 에지를 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-187">You can read any vertex or edge using the partition key and id in Gremlin.</span></span> <span data-ttu-id="6609a-188">예를 들어, 지역("미국")의 그래프가 파티션 키이고 "시애틀"이 행 키인 경우 다음 구문을 사용하여 꼭짓점을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-188">For example, for a graph with region ("USA") as the partition key, and "Seattle" as the row key, you can find a vertex using the following syntax:</span></span>

```
g.V(['USA', 'Seattle'])
```

<span data-ttu-id="6609a-189">에지와 동일하게 파티션 키와 행 키를 사용하는 에지를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-189">Same with edges, you can reference an edge using the partition key and row key.</span></span>

```
g.E(['USA', 'I5'])
```

<span data-ttu-id="6609a-190">자세한 내용은 [Cosmos DB에 대한 Gremlin 지원](gremlin-support.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6609a-190">See [Gremlin support for Cosmos DB](gremlin-support.md) for more details.</span></span>


<a name="designing-for-partitioning"></a>
## <a name="designing-for-partitioning"></a><span data-ttu-id="6609a-191">분할 디자인</span><span class="sxs-lookup"><span data-stu-id="6609a-191">Designing for partitioning</span></span>
<span data-ttu-id="6609a-192">Azure Cosmos DB를 효과적으로 확장하려면 컨테이너를 만들 때 적절한 파티션 키를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-192">To scale effectively with Azure Cosmos DB, you need to pick a good partition key when you create your container.</span></span> <span data-ttu-id="6609a-193">파티션 키를 선택하는 두 가지 주요 고려 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-193">There are two key considerations for choosing a partition key:</span></span>

* <span data-ttu-id="6609a-194">**쿼리 및 트랜잭션의 경계**: 파티션 키를 선택할 때는 트랜잭션 사용에 대한 요구 사항과 여러 파티션 키에 엔터티를 분산하는 데 대한 요구 사항 간에 균형을 유지하여 솔루션의 확장성을 보장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-194">**Boundary for query and transactions**: Your choice of partition key should balance the need to enable the use of transactions against the requirement to distribute your entities across multiple partition keys to ensure a scalable solution.</span></span> <span data-ttu-id="6609a-195">한 쪽으로 치우치면 모든 항목에 동일한 파티션 키를 설정할 수 있지만 솔루션의 확장성이 제한될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-195">At one extreme, you could set the same partition key for all your items, but this may limit the scalability of your solution.</span></span> <span data-ttu-id="6609a-196">다른 쪽으로 치우치면 각 항목에 고유한 파티션 키를 할당할 수 있으므로 확장성이 매우 높지만 저장 프로시저 및 트리거를 통해 문서 트랜잭션 간에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-196">At the other extreme, you could assign a unique partition key for each item, which would be highly scalable but would prevent you from using cross document transactions via stored procedures and triggers.</span></span> <span data-ttu-id="6609a-197">이상적인 파티션 키는 효율적인 쿼리를 사용할 수 있도록 하고 솔루션을 확장할 수 있는 충분한 카디널리티가 있는 키입니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-197">An ideal partition key is one that enables you to use efficient queries and that has sufficient cardinality to ensure your solution is scalable.</span></span> 
* <span data-ttu-id="6609a-198">**저장소 및 성능 병목 현상 없음**: 쓰기를 다양한 고유 값에 분산할 수 있는 속성을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-198">**No storage and performance bottlenecks**: It is important to pick a property that allows writes to be distributed across various distinct values.</span></span> <span data-ttu-id="6609a-199">동일한 파티션 키에 대한 요청은 단일 파티션의 처리량을 초과할 수 없으며 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-199">Requests to the same partition key cannot exceed the throughput of a single partition, and are throttled.</span></span> <span data-ttu-id="6609a-200">따라서 응용 프로그램 내에서 "핫 스폿"을 초래하지 않는 파티션 키를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-200">So it is important to pick a partition key that does not result in "hot spots" within your application.</span></span> <span data-ttu-id="6609a-201">단일 파티션 키에 대한 모든 데이터는 파티션 내에 저장해야 하므로 같은 가격에 데이터 볼륨이 많은 파티션 키는 피하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-201">Since all the data for a single partition key must be stored within a partition, it is also recommended to avoid partition keys that have high volumes of data for the same value.</span></span> 

<span data-ttu-id="6609a-202">몇 가지 실제 시나리오 및 적절한 파티션 키를 각각 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-202">Let's look at a few real-world scenarios, and good partition keys for each:</span></span>
* <span data-ttu-id="6609a-203">사용자 프로필 백 엔드를 구현하는 경우 사용자 ID를 파티션 키로 선택하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-203">If you’re implementing a user profile backend, then the user ID is a good choice for partition key.</span></span>
* <span data-ttu-id="6609a-204">IoT 데이터(예: 장치 상태)를 저장하는 경우 장치 ID를 파티션 키로 선택하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-204">If you’re storing IoT data for example, device state, a device ID is a good choice for partition key.</span></span>
* <span data-ttu-id="6609a-205">시계열 데이터를 기록하는 데 Azure Cosmos DB를 사용하는 경우 호스트 이름 또는 프로세스 ID를 파티션 키로 선택하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-205">If you’re using Azure Cosmos DB for logging time-series data, then the hostname or process ID is a good choice for partition key.</span></span>
* <span data-ttu-id="6609a-206">다중 테넌트 아키텍처가 있는 경우 테넌트 ID를 파티션 키로 선택하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-206">If you have a multi-tenant architecture, the tenant ID is a good choice for partition key.</span></span>

<span data-ttu-id="6609a-207">일부 사례(예: IoT 및 사용자 프로필)에서는 파티션 키가 사용자 ID(문서 키)와 동일할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-207">In some use cases like IoT and user profiles, the partition key might be the same as your id (document key).</span></span> <span data-ttu-id="6609a-208">시계열 데이터와 같은 다른 사례에서는 id와 다른 파티션 키를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-208">In others like the time series data, you might have a partition key that’s different than the id.</span></span>

### <a name="partitioning-and-loggingtime-series-data"></a><span data-ttu-id="6609a-209">분할 및 로깅/시계열 데이터</span><span class="sxs-lookup"><span data-stu-id="6609a-209">Partitioning and logging/time-series data</span></span>
<span data-ttu-id="6609a-210">Cosmos DB의 일반적인 사용 사례 중 하나는 로깅 및 원격 분석입니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-210">One of the common use cases of Cosmos DB is for logging and telemetry.</span></span> <span data-ttu-id="6609a-211">방대한 양의 데이터를 읽기/쓰기 해야 할 수 있으므로 적절한 파티션 키를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-211">It is important to pick a good partition key since you might need to read/write vast volumes of data.</span></span> <span data-ttu-id="6609a-212">사용자의 읽기 및 쓰기 비율 및 실행할 쿼리의 종류에 따라 선택이 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-212">The choice depends on your read and write rates and kinds of queries you expect to run.</span></span> <span data-ttu-id="6609a-213">다음은 적절한 파티션 키를 선택하는 방법에 대한 몇 가지 팁입니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-213">Here are some tips on how to choose a good partition key.</span></span>

* <span data-ttu-id="6609a-214">사용 사례가 오랜 기간 동안 축적하는 작은 비율의 쓰기를 포함하고 타임스탬프 및 다른 필터의 범위를 기준으로 쿼리해야 하는 경우 파티션 키로 타임스탬프(예: 날짜)의 롤업을 사용하는 것이 좋은 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-214">If your use case involves a small rate of writes accumulating over a long period of time, and need to query by ranges of timestamps and other filters, then using a rollup of the timestamp, for example,  date as a partition key is a good approach.</span></span> <span data-ttu-id="6609a-215">이렇게 하면 단일 파티션에서 날짜에 대한 모든 데이터를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-215">This allows you to query over all the data for a date from a single partition.</span></span> 
* <span data-ttu-id="6609a-216">일반적으로 워크로드에 쓰기 작업이 많은 경우 Cosmos DB가 다양한 파티션에 쓰기를 균등하게 분산할 수 있도록 타임스탬프에 기반하지 않는 파티션 키를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-216">If your workload is written heavy, which is more common, you should use a partition key that’s not based on timestamp so that Cosmos DB can distribute writes evenly across various partitions.</span></span> <span data-ttu-id="6609a-217">여기서 높은 카디널리티의 호스트 이름, 프로세스 ID, 작업 ID 또는 다른 속성을 선택하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-217">Here a hostname, process ID, activity ID, or another property with high cardinality is a good choice.</span></span> 
* <span data-ttu-id="6609a-218">세 번째 방법은 여러 컨테이너가 있는(각 일/월에 대해 하나) 하이브리드이며 파티션 키는 호스트 이름처럼 세부적인 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-218">A third approach is a hybrid one where you have multiple containers, one for each day/month and the partition key is a granular property like hostname.</span></span> <span data-ttu-id="6609a-219">시간 창에 기반한 다양한 처리량을 설정할 수 있다는 장점이 있습니다. 예를 들어 현재 월에 대한 컨테이너는 읽기 및 쓰기를 제공하므로 높은 처리량으로 프로비전되는 반면 이전 달은 읽기만을 제공하므로 낮은 처리량으로 프로비전됩니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-219">This has the benefit that you can set different throughput based on the time window, for example, the container for the current month is provisioned with higher throughput since it serves reads and writes, whereas previous months with lower throughput since they only serve reads.</span></span>

### <a name="partitioning-and-multi-tenancy"></a><span data-ttu-id="6609a-220">분할 및 다중 테넌트</span><span class="sxs-lookup"><span data-stu-id="6609a-220">Partitioning and multi-tenancy</span></span>
<span data-ttu-id="6609a-221">Cosmos DB를 사용하여 다중 테넌트 응용 프로그램을 구현하는 경우 테넌트당 하나의 파티션 키 및 테넌트당 하나의 컨테이너라는 두 가지 인기 있는 패턴이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-221">If you are implementing a multi-tenant application using Cosmos DB, there are two popular patterns – one partition key per tenant, and one container per tenant.</span></span> <span data-ttu-id="6609a-222">각각의 장단점은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-222">Here are the pros and cons for each:</span></span>

* <span data-ttu-id="6609a-223">테넌트당 하나의 파티션 키: 이 모델에서는 테넌트가 단일 컨테이너 내에 함께 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-223">One Partition Key per tenant: In this model, tenants are collocated within a single container.</span></span> <span data-ttu-id="6609a-224">그러나 단일 파티션 내의 항목에 대한 쿼리 및 삽입을 단일 파티션에 대해 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-224">But queries and inserts for items within a single tenant can be performed against a single partition.</span></span> <span data-ttu-id="6609a-225">또한 테넌트 내의 모든 항목에서 트랜잭션 논리를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-225">You can also implement transactional logic across all items within a tenant.</span></span> <span data-ttu-id="6609a-226">다중 테넌트는 컨테이너를 공유하기 때문에 각 테넌트에 대한 추가 헤드룸을 프로비전하는 대신 테넌트에 대한 리소스를 풀링하여 저장소 및 처리량을 단일 컨테이너 내에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-226">Since multiple tenants share a container, you can save storage and throughput costs by pooling resources for tenants within a single container rather than provisioning extra headroom for each tenant.</span></span> <span data-ttu-id="6609a-227">단점은 테넌트당 성능 격리가 없다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-227">The drawback is that you do not have performance isolation per tenant.</span></span> <span data-ttu-id="6609a-228">성능/처리량 증가가 대상 테넌트에 대한 증가가 아니라 전체 컨테이너에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-228">Performance/throughput increases apply to the entire container vs targeted increases for tenants.</span></span>
* <span data-ttu-id="6609a-229">테넌트당 하나의 컨테이너: 각 테넌트에 고유한 컨테이너가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-229">One Container per tenant: Each tenant has its own container.</span></span> <span data-ttu-id="6609a-230">이 모델에서는 테넌트당 성능을 예약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-230">In this model, you can reserve performance per tenant.</span></span> <span data-ttu-id="6609a-231">Cosmos DB의 새로운 프로비전 가격 책정 모델을 사용하는 이 모델은 몇몇 테넌트가 있는 다중 테넌트 응용 프로그램에 보다 비용 효율적입니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-231">With Cosmos DB's new provisioning pricing model, this model is more cost-effective for multi-tenant applications with a few tenants.</span></span>

<span data-ttu-id="6609a-232">소수의 테넌트를 함께 배치하고 더 큰 테넌트를 고유한 컨테이너로 마이그레이션하는 조합/계층형 접근 방식을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-232">You can also use a combination/tiered approach that collocates small tenants and migrates larger tenants to their own container.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6609a-233">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6609a-233">Next steps</span></span>
<span data-ttu-id="6609a-234">이 문서에서는 Azure Cosmos DB API를 사용하여 분할하기 위한 개념 및 모범 사례의 개요를 제공했습니다.</span><span class="sxs-lookup"><span data-stu-id="6609a-234">In this article, we provided an overview for an overview of concepts and best practices for partitioning with any Azure Cosmos DB API.</span></span> 

* <span data-ttu-id="6609a-235">[Azure Cosmos DB에서 프로비전된 처리량](request-units.md)에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="6609a-235">Learn about [provisioned throughput in Azure Cosmos DB](request-units.md)</span></span>
* <span data-ttu-id="6609a-236">[Azure Cosmos DB에서 글로벌 배포](distribute-data-globally.md)에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="6609a-236">Learn about [global distribution in Azure Cosmos DB](distribute-data-globally.md)</span></span>




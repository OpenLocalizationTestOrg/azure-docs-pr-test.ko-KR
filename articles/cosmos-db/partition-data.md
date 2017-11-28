---
title: "aaaPartitioning Azure Cosmos DB에서 가로 크기를 조정 | Microsoft Docs"
description: "Azure Cosmos DB에서 분할 방법을 작동에 대 한 어떻게 tooconfigure 분할 및 파티션 키, 그리고 toopick 오른쪽 hello 파티션 키에 대 한 응용 프로그램에 대해 알아봅니다."
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
ms.openlocfilehash: 87d56db8c4ccc6b94b1650baff0fcfb3db6d1777
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toopartition-and-scale-in-azure-cosmos-db"></a><span data-ttu-id="eb51f-103">어떻게 toopartition와 Azure Cosmos DB에서 소수 자릿수</span><span class="sxs-lookup"><span data-stu-id="eb51f-103">How toopartition and scale in Azure Cosmos DB</span></span>

<span data-ttu-id="eb51f-104">[Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) 있습니다 달성 신속 하 고 예측 가능한 성능 및 확장성 원활 하 게 응용 프로그램과 함께 커짐에 따라 글로벌 분산, 다중-모델 데이터베이스 설계 된 서비스 toohelp 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-104">[Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) is a global distributed, multi-model database service designed toohelp you achieve fast, predictable performance and scale seamlessly along with your application as it grows.</span></span> <span data-ttu-id="eb51f-105">이 문서에서는 분할은 모든 hello 데이터에 대 한 Azure Cosmos DB에서 모델 및 Azure Cosmos DB 컨테이너 tooeffectively 크기 조정 응용 프로그램 구성할 수 있는 방법을 설명 방법의 개요를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-105">This article provides an overview of how partitioning works for all hello data models in Azure Cosmos DB, and describes how you can configure Azure Cosmos DB containers tooeffectively scale your applications.</span></span>

<span data-ttu-id="eb51f-106">Scott Hanselman과 Azure Cosmos DB 수석 엔지니어링 관리자 Shireesh Thota가 진행하는 이 Azure Friday 비디오에서는 분할 및 파티션 키에 대해서도 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-106">Partitioning and partition keys are also covered in this Azure Friday video with Scott Hanselman and Azure Cosmos DB Principal Engineering Manager, Shireesh Thota.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-DocumentDB-Elastic-Scale-Partitioning/player]
> 

## <a name="partitioning-in-azure-cosmos-db"></a><span data-ttu-id="eb51f-107">Azure Cosmos DB에서 분할</span><span class="sxs-lookup"><span data-stu-id="eb51f-107">Partitioning in Azure Cosmos DB</span></span>
<span data-ttu-id="eb51f-108">Azure Cosmos DB에서는 규모에 상관없이 밀리초 단위의 응답 시간 순으로 스키마 없는 데이터를 저장하고 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-108">In Azure Cosmos DB, you can store and query schema-less data with order-of-millisecond response times at any scale.</span></span> <span data-ttu-id="eb51f-109">Cosmos DB는 **컬렉션(문서의 경우), 그래프 및 표**라는 데이터 저장용 컨테이너를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-109">Cosmos DB provides containers for storing data called **collections (for document), graphs, or tables**.</span></span> <span data-ttu-id="eb51f-110">컨테이너는 하나 이상의 물리적 파티션 또는 서버에 걸쳐 있을 수 있는 논리적 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-110">Containers are logical resources and can span one or more physical partitions or servers.</span></span> <span data-ttu-id="eb51f-111">파티션 수가 hello Cosmos db hello 저장소 크기와 hello hello 컨테이너의 프로 비전 된 처리량에 따라 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-111">hello number of partitions is determined by Cosmos DB based on hello storage size and hello provisioned throughput of hello container.</span></span> <span data-ttu-id="eb51f-112">Cosmos DB의 모든 파티션은 고정된 양의 SSD 지원 저장소에 연결되며, 고가용성을 위해 복제됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-112">Every partition in Cosmos DB has a fixed amount of SSD-backed storage associated with it, and is replicated for high availability.</span></span> <span data-ttu-id="eb51f-113">파티션 관리 Azure Cosmos DB에서 관리 하는 완벽 하 게 하 고 toowrite 복잡 한 코드가 있는 또는 파티션을 관리 하지 않는 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-113">Partition management is fully managed by Azure Cosmos DB, and you do not have toowrite complex code or manage your partitions.</span></span> <span data-ttu-id="eb51f-114">Cosmos DB 컨테이너는 처리량 및 저장소 면에서 제한되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-114">Cosmos DB containers are unlimited in terms of storage and throughput.</span></span> 

![horizontal](./media/introduction/azure-cosmos-db-partitioning.png) 

<span data-ttu-id="eb51f-116">분할은 투명 tooyour 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-116">Partitioning is transparent tooyour application.</span></span> <span data-ttu-id="eb51f-117">Cosmos DB 빠른 읽기 및 쓰기, 쿼리, 트랜잭션 논리, 일관성 수준 및 메서드/Api tooa 단일 컨테이너 리소스를 통해 세분화 된 액세스 제어를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-117">Cosmos DB supports fast reads and writes, queries, transactional logic, consistency levels, and fine-grained access control via methods/APIs tooa single container resource.</span></span> <span data-ttu-id="eb51f-118">hello 파티션 간에 데이터를 배포 및 쿼리 요청 toohello 올바른 파티션 라우팅 서비스 핸들입니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-118">hello service handles distributing data across partitions and routing query requests toohello right partition.</span></span> 

<span data-ttu-id="eb51f-119">분할은 어떻게 작동하나요?</span><span class="sxs-lookup"><span data-stu-id="eb51f-119">How does partitioning work?</span></span> <span data-ttu-id="eb51f-120">각 항목에는 파티션 키 및 행 키가 있어서 항목을 고유하게 식별해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-120">Each item must have a partition key and a row key, which uniquely identify it.</span></span> <span data-ttu-id="eb51f-121">파티션 키는 데이터에 대한 논리적 분할의 역할을 하고 파티션 간에 데이터를 배포하는 자연 경계를 가진 Cosmos DB를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-121">Your partition key acts as a logical partition for your data, and provides Cosmos DB with a natural boundary for distributing data across partitions.</span></span> <span data-ttu-id="eb51f-122">간단히 말해, Azure Cosmos DB에서 분할의 작동 방식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-122">In brief, here is how partitioning works in Azure Cosmos DB:</span></span>

* <span data-ttu-id="eb51f-123">`T` 요청/초 처리량으로 Cosmos DB 컨테이너를 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-123">You provision a Cosmos DB container with `T` requests/s throughput</span></span>
* <span data-ttu-id="eb51f-124">Hello 백그라운드 Cosmos DB 프로 비전 파티션에 필요한 tooserve `T` 요청/초입니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-124">Behind hello scenes, Cosmos DB provisions partitions needed tooserve `T` requests/s.</span></span> <span data-ttu-id="eb51f-125">경우 `T` 파티션당 hello 최대 처리량 보다 높은 `t`, Cosmos DB 프로 비전 한 다음 `N`  =  `T/t` 파티션</span><span class="sxs-lookup"><span data-stu-id="eb51f-125">If `T` is higher than hello maximum throughput per partition `t`, then Cosmos DB provisions `N` = `T/t` partitions</span></span>
* <span data-ttu-id="eb51f-126">Cosmos DB 공간 할당 하는 hello 키 파티션 키 해시 균등 하 게 hello에서 `N` 파티션을 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-126">Cosmos DB allocates hello key space of partition key hashes evenly across hello `N` partitions.</span></span> <span data-ttu-id="eb51f-127">따라서 각 파티션(실제 파티션)은 1-N 파티션 키 값(논리 파티션)을 호스팅합니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-127">So, each partition (physical partition) hosts 1-N partition key values (logical partitions)</span></span>
* <span data-ttu-id="eb51f-128">때 실제 파티션을 `p` 저장소 한도 Cosmos DB 원활 하 게 분할 하는 정도 `p` 두 개의 새 파티션으로 `p1` 및 `p2` 하 고이 배포의 hello tooroughly 절반 hello 키 tooeach 해당 값 파티션입니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-128">When a physical partition `p` reaches its storage limit, Cosmos DB seamlessly splits `p` into two new partitions `p1` and `p2` and distributes values corresponding tooroughly half hello keys tooeach of hello partitions.</span></span> <span data-ttu-id="eb51f-129">이 작업을 분할은 보이지 않는 tooyour 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-129">This split operation is invisible tooyour application.</span></span>
* <span data-ttu-id="eb51f-130">마찬가지로, 보다 높은 처리량을 제공 하는 하면 `t*N` 하나 이상의 파티션 toosupport hello 더 높은 처리량을 분할 하는 처리량, Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="eb51f-130">Similarly, when you provision throughput higher than `t*N` throughput, Cosmos DB splits one or more of your partitions toosupport hello higher throughput</span></span>

<span data-ttu-id="eb51f-131">파티션 키에 대 한 hello 의미 hello 표 다음에 표시 된 것과 같이 각 API의 약간 다른 toomatch hello 의미 체계를 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-131">hello semantics for partition keys are slightly different toomatch hello semantics of each API, as shown in hello following table:</span></span>

| <span data-ttu-id="eb51f-132">API</span><span class="sxs-lookup"><span data-stu-id="eb51f-132">API</span></span> | <span data-ttu-id="eb51f-133">Partition Key</span><span class="sxs-lookup"><span data-stu-id="eb51f-133">Partition Key</span></span> | <span data-ttu-id="eb51f-134">Row Key</span><span class="sxs-lookup"><span data-stu-id="eb51f-134">Row Key</span></span> |
| --- | --- | --- |
| <span data-ttu-id="eb51f-135">DocumentDB</span><span class="sxs-lookup"><span data-stu-id="eb51f-135">DocumentDB</span></span> | <span data-ttu-id="eb51f-136">custom partition key path</span><span class="sxs-lookup"><span data-stu-id="eb51f-136">custom partition key path</span></span> | <span data-ttu-id="eb51f-137">fixed `id`</span><span class="sxs-lookup"><span data-stu-id="eb51f-137">fixed `id`</span></span> | 
| <span data-ttu-id="eb51f-138">MongoDB</span><span class="sxs-lookup"><span data-stu-id="eb51f-138">MongoDB</span></span> | <span data-ttu-id="eb51f-139">custom shard key</span><span class="sxs-lookup"><span data-stu-id="eb51f-139">custom shard key</span></span>  | <span data-ttu-id="eb51f-140">fixed `_id`</span><span class="sxs-lookup"><span data-stu-id="eb51f-140">fixed `_id`</span></span> | 
| <span data-ttu-id="eb51f-141">그래프</span><span class="sxs-lookup"><span data-stu-id="eb51f-141">Graph</span></span> | <span data-ttu-id="eb51f-142">custom partition key property</span><span class="sxs-lookup"><span data-stu-id="eb51f-142">custom partition key property</span></span> | <span data-ttu-id="eb51f-143">fixed `id`</span><span class="sxs-lookup"><span data-stu-id="eb51f-143">fixed `id`</span></span> | 
| <span data-ttu-id="eb51f-144">테이블</span><span class="sxs-lookup"><span data-stu-id="eb51f-144">Table</span></span> | <span data-ttu-id="eb51f-145">fixed `PartitionKey`</span><span class="sxs-lookup"><span data-stu-id="eb51f-145">fixed `PartitionKey`</span></span> | <span data-ttu-id="eb51f-146">fixed `RowKey`</span><span class="sxs-lookup"><span data-stu-id="eb51f-146">fixed `RowKey`</span></span> | 

<span data-ttu-id="eb51f-147">Cosmos DB는 해시 기반 분할을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-147">Cosmos DB uses hash-based partitioning.</span></span> <span data-ttu-id="eb51f-148">항목을 작성 하는 경우 Cosmos DB hello 파티션 키 값을 해시 및 사용 하 여 hello 해시 결과 toodetermine 어떤 파티션 toostore hello 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-148">When you write an item, Cosmos DB hashes hello partition key value and use hello hashed result toodetermine which partition toostore hello item in.</span></span> <span data-ttu-id="eb51f-149">Cosmos DB 저장소 인 모든 항목에 동일한 파티션 키 hello hello 동일한 실제 파티션을 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-149">Cosmos DB stores all items with hello same partition key in hello same physical partition.</span></span> <span data-ttu-id="eb51f-150">hello 선택 hello 파티션 키에는 디자인 타임에 toomake 한지 중요 한 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-150">hello choice of hello partition key is an important decision that you have toomake at design time.</span></span> <span data-ttu-id="eb51f-151">다양한 범위의 값과 균일한 액세스 패턴을 가진 속성 이름을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-151">You must pick a property name that has a wide range of values and has even access patterns.</span></span>

> [!NOTE]
> <span data-ttu-id="eb51f-152">모범 사례 toohave 많은 고유 값 (단위: 100 1000s 최소한)를 사용 하 여 파티션 키 이며</span><span class="sxs-lookup"><span data-stu-id="eb51f-152">It is a best practice toohave a partition key with many distinct values (100s-1000s at a minimum).</span></span>
>

<span data-ttu-id="eb51f-153">Azure Cosmos DB 컨테이너를 "고정" 또는 "무제한"으로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-153">Azure Cosmos DB containers can be created as "fixed" or "unlimited."</span></span> <span data-ttu-id="eb51f-154">고정 크기 컨테이너는 최대 제한 10GB 및 10,000RU/s 처리량을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-154">Fixed-size containers have a maximum limit of 10 GB and 10,000 RU/s throughput.</span></span> <span data-ttu-id="eb51f-155">일부 Api는 고정 크기의 컨테이너에 대 한 hello 파티션 키 toobe 생략 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-155">Some APIs allow hello partition key toobe omitted for fixed-size containers.</span></span> <span data-ttu-id="eb51f-156">무제한으로 컨테이너 toocreate 2500 000RU/s의 최소 처리량을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-156">toocreate a container as unlimited, you must specify a minimum throughput of 2500 RU/s.</span></span>

## <a name="partitioning-and-provisioned-throughput"></a><span data-ttu-id="eb51f-157">분할 및 프로비전된 처리량</span><span class="sxs-lookup"><span data-stu-id="eb51f-157">Partitioning and provisioned throughput</span></span>
<span data-ttu-id="eb51f-158">Cosmos DB는 예측 가능한 성능을 위해 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-158">Cosmos DB is designed for predictable performance.</span></span> <span data-ttu-id="eb51f-159">컨테이너를 만들 때 **RU/m의 잠재적인 기능으로 초당 [요청 단위](request-units.md)(RU)** 측면에서 처리량을 예약합니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-159">When you create a container, you reserve throughput in terms of **[request units](request-units.md) (RU) per second with a potential add-on for RU per minute**.</span></span> <span data-ttu-id="eb51f-160">각 요청은 요청 단위 요금이 비례 toohello 양의 CPU, 메모리 및 IO hello 작업에 의해 소비와 같은 시스템 리소스를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-160">Each request is assigned a request unit charge that is proportionate toohello amount of system resources like CPU, Memory, and IO consumed by hello operation.</span></span> <span data-ttu-id="eb51f-161">세션 일관성에 따라 1KB 문서를 읽을 경우 1RU(요청 단위)가 소비됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-161">A read of a 1-KB document with Session consistency consumes one request unit.</span></span> <span data-ttu-id="eb51f-162">읽기는 1 hello 항목 수에 관계 없이 RU hello에서 실행 되는 동시 요청 수가 hello 또는 저장 된 같은 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-162">A read is 1 RU regardless of hello number of items stored or hello number of concurrent requests running at hello same time.</span></span> <span data-ttu-id="eb51f-163">더 큰 항목 hello 크기에 따라 더 높은 요청 단위를 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-163">Larger items require higher request units depending on hello size.</span></span> <span data-ttu-id="eb51f-164">엔터티가 hello 크기를 알고 있으며 읽기 횟수가 hello toosupport 응용 프로그램에 필요한, hello 정확한 양을 응용 프로그램의 요구 사항을 읽이 필요한 처리량을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-164">If you know hello size of your entities and hello number of reads you need toosupport for your application, you can provision hello exact amount of throughput required for your application's read needs.</span></span> 

> [!NOTE]
> <span data-ttu-id="eb51f-165">hello 컨테이너의 tooachieve hello의 전체 처리량을 선택 해야 tooevenly 수 있는 파티션 키 일부 고유 파티션 키 값 사이 요청을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-165">tooachieve hello full throughput of hello container, you must choose a partition key that allows you tooevenly distribute requests among some distinct partition key values.</span></span>
> 
> 

<a name="designing-for-partitioning"></a>
## <a name="working-with-hello-azure-cosmos-db-apis"></a><span data-ttu-id="eb51f-166">Hello Azure Cosmos DB Api 사용</span><span class="sxs-lookup"><span data-stu-id="eb51f-166">Working with hello Azure Cosmos DB APIs</span></span>
<span data-ttu-id="eb51f-167">Hello Azure 포털 또는 Azure CLI toocreate 컨테이너를 사용할 수 있으며 언제 든 지를 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-167">You can use hello Azure portal or Azure CLI toocreate containers and scale them at any time.</span></span> <span data-ttu-id="eb51f-168">이 섹션에서는 어떻게 toocreate 컨테이너 hello 처리량과 파티션 키 정의의 hello 각 지원 되는 Api를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-168">This section shows how toocreate containers and specify hello throughput and partition key definition in each of hello supported APIs.</span></span>

### <a name="documentdb-api"></a><span data-ttu-id="eb51f-169">DocumentDB API</span><span class="sxs-lookup"><span data-stu-id="eb51f-169">DocumentDB API</span></span>
<span data-ttu-id="eb51f-170">다음 예제는 hello 사용 하 여 컨테이너 (컬렉션) toocreate DocumentDB API hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-170">hello following sample shows how toocreate a container (collection) using hello DocumentDB API.</span></span> <span data-ttu-id="eb51f-171">[DocumentDB API를 사용하여 분할](partition-data.md)에서 자세한 내용을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-171">You can find more details in [Partitioning with DocumentDB API](partition-data.md).</span></span>

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

<span data-ttu-id="eb51f-172">Hello를 사용 하 여 항목 (문서)를 읽을 수 `GET` 메서드 hello REST API 또는 사용 하 여 `ReadDocumentAsync` hello Sdk 중 하나에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-172">You can read an item (document) using hello `GET` method in hello REST API or using `ReadDocumentAsync` in one of hello SDKs.</span></span>

```csharp
// Read document. Needs hello partition key and hello ID toobe specified
DeviceReading document = await client.ReadDocumentAsync<DeviceReading>(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });
```

### <a name="mongodb-api"></a><span data-ttu-id="eb51f-173">MongoDB API</span><span class="sxs-lookup"><span data-stu-id="eb51f-173">MongoDB API</span></span>
<span data-ttu-id="eb51f-174">Hello MongoDB API, 임의의 도구, 드라이버 또는 SDK를 통해 분할 된 컬렉션을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-174">With hello MongoDB API, you can create a sharded collection through your favorite tool, driver, or SDK.</span></span> <span data-ttu-id="eb51f-175">이 예에서는 hello 컬렉션 만들기에 대 한 hello Mongo 셸을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-175">In this example, we use hello Mongo Shell for hello collection creation.</span></span>

<span data-ttu-id="eb51f-176">Mongo 셸을 hello:</span><span class="sxs-lookup"><span data-stu-id="eb51f-176">In hello Mongo Shell:</span></span>

```
db.runCommand( { shardCollection: "admin.people", key: { region: "hashed" } } )
```
    
<span data-ttu-id="eb51f-177">결과:</span><span class="sxs-lookup"><span data-stu-id="eb51f-177">Results:</span></span>

```JSON
{
    "_t" : "ShardCollectionResponse",
    "ok" : 1,
    "collectionsharded" : "admin.people"
}
```

### <a name="table-api"></a><span data-ttu-id="eb51f-178">테이블 API</span><span class="sxs-lookup"><span data-stu-id="eb51f-178">Table API</span></span>

<span data-ttu-id="eb51f-179">테이블 API hello로 응용 프로그램에 대 한 hello appSettings 구성에서 테이블에 대 한 hello 처리량을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-179">With hello Table API, you specify hello throughput for tables in hello appSettings configuration for your application:</span></span>

```xml
<configuration>
    <appSettings>
      <!--Table creation options -->
      <add key="TableThroughput" value="700"/>
    </appSettings>
</configuration>
```

<span data-ttu-id="eb51f-180">그런 다음 hello Azure 테이블 저장소 SDK를 사용 하 여 테이블을 만들면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-180">Then you create a table using hello Azure Table storage SDK.</span></span> <span data-ttu-id="eb51f-181">hello 파티션 키 hello로 암시적으로 생성 되어 `PartitionKey` 값입니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-181">hello partition key is implicitly created as hello `PartitionKey` value.</span></span> 

```csharp
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

CloudTable table = tableClient.GetTableReference("people");
table.CreateIfNotExists();
```

<span data-ttu-id="eb51f-182">다음 코드 조각 hello를 사용 하 여 단일 엔터티를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-182">You can retrieve a single entity using hello following snippet:</span></span>

```csharp
// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute hello retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);
```
<span data-ttu-id="eb51f-183">참조 [hello 테이블 API로 개발](tutorial-develop-table-dotnet.md) 내용을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-183">See [Developing with hello Table API](tutorial-develop-table-dotnet.md) for more details.</span></span>

### <a name="graph-api"></a><span data-ttu-id="eb51f-184">그래프 API</span><span class="sxs-lookup"><span data-stu-id="eb51f-184">Graph API</span></span>

<span data-ttu-id="eb51f-185">Graph API hello로 hello Azure 포털 또는 CLI toocreate 컨테이너를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-185">With hello Graph API, you must use hello Azure portal or CLI toocreate containers.</span></span> <span data-ttu-id="eb51f-186">또는 Azure Cosmos DB 다중 모델 이므로 다른 모델 toocreate hello 중 하나를 사용 하 고 그래프 컨테이너를 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-186">Alternatively, since Azure Cosmos DB is multi-model, you can use one of hello other models toocreate and scale your graph container.</span></span>

<span data-ttu-id="eb51f-187">모든 꼭 짓 점 또는 가장자리 Gremlin에 hello 파티션 키 및 id를 사용 하 여 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-187">You can read any vertex or edge using hello partition key and id in Gremlin.</span></span> <span data-ttu-id="eb51f-188">예를 들어 hello 파티션 키 및 "Seattle" hello 행 키로 영역 ("미국")와 그래프를 구문 다음 hello를 사용 하 여 꼭지점을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-188">For example, for a graph with region ("USA") as hello partition key, and "Seattle" as hello row key, you can find a vertex using hello following syntax:</span></span>

```
g.V(['USA', 'Seattle'])
```

<span data-ttu-id="eb51f-189">가장자리와 동일 하지만, hello 파티션 키와 행 키를 사용 하 여 가장자리를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-189">Same with edges, you can reference an edge using hello partition key and row key.</span></span>

```
g.E(['USA', 'I5'])
```

<span data-ttu-id="eb51f-190">자세한 내용은 [Cosmos DB에 대한 Gremlin 지원](gremlin-support.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="eb51f-190">See [Gremlin support for Cosmos DB](gremlin-support.md) for more details.</span></span>


<a name="designing-for-partitioning"></a>
## <a name="designing-for-partitioning"></a><span data-ttu-id="eb51f-191">분할 디자인</span><span class="sxs-lookup"><span data-stu-id="eb51f-191">Designing for partitioning</span></span>
<span data-ttu-id="eb51f-192">Azure Cosmos DB와 함께 효과적으로 tooscale, 해야 toopick 파티션 키 컨테이너를 만들 때.</span><span class="sxs-lookup"><span data-stu-id="eb51f-192">tooscale effectively with Azure Cosmos DB, you need toopick a good partition key when you create your container.</span></span> <span data-ttu-id="eb51f-193">파티션 키를 선택하는 두 가지 주요 고려 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-193">There are two key considerations for choosing a partition key:</span></span>

* <span data-ttu-id="eb51f-194">**쿼리 및 트랜잭션에 대해 경계**: 선택 하는 파티션 키를 조정 해야 hello 필요 tooenable hello 사용 요구 사항이 toodistribute hello에 대 한 트랜잭션 엔터티에서 여러 파티션 키 tooensure는 확장 가능한 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-194">**Boundary for query and transactions**: Your choice of partition key should balance hello need tooenable hello use of transactions against hello requirement toodistribute your entities across multiple partition keys tooensure a scalable solution.</span></span> <span data-ttu-id="eb51f-195">최대 hello를 설정할 수 있습니다이 있지만 모든 항목에 대 한 파티션 키를 동일한 솔루션의 hello 확장성이 제한 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-195">At one extreme, you could set hello same partition key for all your items, but this may limit hello scalability of your solution.</span></span> <span data-ttu-id="eb51f-196">다른 한편으로을 hello에 확장성이 높은 것 이지만으로 인해에서 저장된 프로시저 및 트리거를 통해 교차 문서 트랜잭션을 사용 하는 각 항목에 대 한 고유 파티션 키를 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-196">At hello other extreme, you could assign a unique partition key for each item, which would be highly scalable but would prevent you from using cross document transactions via stored procedures and triggers.</span></span> <span data-ttu-id="eb51f-197">이상적인 파티션 키가 수 있게 해 주는 toouse 효율적인 쿼리 및 충분 한 카디널리티가 하나 tooensure 솔루션은 확장 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-197">An ideal partition key is one that enables you toouse efficient queries and that has sufficient cardinality tooensure your solution is scalable.</span></span> 
* <span data-ttu-id="eb51f-198">**저장소 및 성능 병목 현상이 없습니다**: 것이 중요 toopick 수 있도록 하는 속성에 다양 한 고유 값에 분산 toobe 씁니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-198">**No storage and performance bottlenecks**: It is important toopick a property that allows writes toobe distributed across various distinct values.</span></span> <span data-ttu-id="eb51f-199">동일한 파티션 키 단일 파티션의 hello 처리량을 초과할 수 없습니다 들어오고 정체 되 toohello를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-199">Requests toohello same partition key cannot exceed hello throughput of a single partition, and are throttled.</span></span> <span data-ttu-id="eb51f-200">따라서 것이 중요 한 toopick "핫 스폿을" 응용 프로그램 내에서 발생 하지 않는 파티션 키입니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-200">So it is important toopick a partition key that does not result in "hot spots" within your application.</span></span> <span data-ttu-id="eb51f-201">모든 hello 데이터 이후에 파티션 내에서 단일 파티션 키를 저장 해야 합니다는 반드시 대용량의 hello에 대 한 데이터를 포함 하는 tooavoid 파티션 키 값입니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-201">Since all hello data for a single partition key must be stored within a partition, it is also recommended tooavoid partition keys that have high volumes of data for hello same value.</span></span> 

<span data-ttu-id="eb51f-202">몇 가지 실제 시나리오 및 적절한 파티션 키를 각각 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-202">Let's look at a few real-world scenarios, and good partition keys for each:</span></span>
* <span data-ttu-id="eb51f-203">사용자 프로필 백엔드를 구현 하는 경우 hello 사용자 ID가 파티션 키에 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-203">If you’re implementing a user profile backend, then hello user ID is a good choice for partition key.</span></span>
* <span data-ttu-id="eb51f-204">IoT 데이터(예: 장치 상태)를 저장하는 경우 장치 ID를 파티션 키로 선택하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-204">If you’re storing IoT data for example, device state, a device ID is a good choice for partition key.</span></span>
* <span data-ttu-id="eb51f-205">시계열 데이터를 기록 하기 위한 Azure Cosmos DB를 사용할 경우 다음 호스트 이름이 hello 또는 프로세스 ID는 파티션 키에 대 한 좋은 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-205">If you’re using Azure Cosmos DB for logging time-series data, then hello hostname or process ID is a good choice for partition key.</span></span>
* <span data-ttu-id="eb51f-206">Hello 테 넌 트 ID는 다중 테 넌 트 아키텍처 있을 경우 파티션 키에 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-206">If you have a multi-tenant architecture, hello tenant ID is a good choice for partition key.</span></span>

<span data-ttu-id="eb51f-207">몇 가지 사용 사례 IoT 및 사용자 프로필, hello 파티션 키와 같은 수 있습니다 (문서 키) id로 hello 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-207">In some use cases like IoT and user profiles, hello partition key might be hello same as your id (document key).</span></span> <span data-ttu-id="eb51f-208">Hello 시계열 데이터와 같은 다른 hello id와 다른 파티션 키를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-208">In others like hello time series data, you might have a partition key that’s different than hello id.</span></span>

### <a name="partitioning-and-loggingtime-series-data"></a><span data-ttu-id="eb51f-209">분할 및 로깅/시계열 데이터</span><span class="sxs-lookup"><span data-stu-id="eb51f-209">Partitioning and logging/time-series data</span></span>
<span data-ttu-id="eb51f-210">Cosmos db hello 일반적인 사용 사례 중 하나는 로깅 및 원격 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-210">One of hello common use cases of Cosmos DB is for logging and telemetry.</span></span> <span data-ttu-id="eb51f-211">중요 한 toopick 파티션 키가 tooread/쓰기 방대한 양의 데이터를 할 수 있으므로.</span><span class="sxs-lookup"><span data-stu-id="eb51f-211">It is important toopick a good partition key since you might need tooread/write vast volumes of data.</span></span> <span data-ttu-id="eb51f-212">읽기 및 쓰기 속도 및 종류의 쿼리 toorun 예상 사항에 따라 hello 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-212">hello choice depends on your read and write rates and kinds of queries you expect toorun.</span></span> <span data-ttu-id="eb51f-213">다음 방법에 대 한 몇 가지 팁은 toochoose 파티션 키입니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-213">Here are some tips on how toochoose a good partition key.</span></span>

* <span data-ttu-id="eb51f-214">사용 사례의 작은 비율 포함 되는 경우의 파티션 키가 있는 좋은 방법으로 날짜 hello timestamp에 대 한 롤업을 사용 하 여 다음를 타임 스탬프 및 다른 필터의 범위를 기준으로 시간과 필요 tooquery 오랜 기간 동안 누적 씁니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-214">If your use case involves a small rate of writes accumulating over a long period of time, and need tooquery by ranges of timestamps and other filters, then using a rollup of hello timestamp, for example,  date as a partition key is a good approach.</span></span> <span data-ttu-id="eb51f-215">그러면 있습니다 tooquery 모든 hello 데이터에 대해 단일 파티션의 날짜에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-215">This allows you tooquery over all hello data for a date from a single partition.</span></span> 
* <span data-ttu-id="eb51f-216">일반적으로 워크로드에 쓰기 작업이 많은 경우 Cosmos DB가 다양한 파티션에 쓰기를 균등하게 분산할 수 있도록 타임스탬프에 기반하지 않는 파티션 키를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-216">If your workload is written heavy, which is more common, you should use a partition key that’s not based on timestamp so that Cosmos DB can distribute writes evenly across various partitions.</span></span> <span data-ttu-id="eb51f-217">여기서 높은 카디널리티의 호스트 이름, 프로세스 ID, 작업 ID 또는 다른 속성을 선택하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-217">Here a hostname, process ID, activity ID, or another property with high cardinality is a good choice.</span></span> 
* <span data-ttu-id="eb51f-218">세 번째 방법에는 하이브리드 하나 있는 각 일/월에 대해 하나씩 여러 컨테이너가 하 고 hello 파티션 키가 호스트 이름 처럼 세부적인 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-218">A third approach is a hybrid one where you have multiple containers, one for each day/month and hello partition key is a granular property like hostname.</span></span> <span data-ttu-id="eb51f-219">예를 들어 hello 현재 달에 대 한 hello 컨테이너 프로 비전 된 처리량이 높은 읽기와 쓰기 사용 되므로으로 이전 달 뿐만 이후 처리량이 낮아질 반면,이 hello 기간에 따라 다른 처리량을 설정할 수 있는 hello 혜택 읽기만 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-219">This has hello benefit that you can set different throughput based on hello time window, for example, hello container for hello current month is provisioned with higher throughput since it serves reads and writes, whereas previous months with lower throughput since they only serve reads.</span></span>

### <a name="partitioning-and-multi-tenancy"></a><span data-ttu-id="eb51f-220">분할 및 다중 테넌트</span><span class="sxs-lookup"><span data-stu-id="eb51f-220">Partitioning and multi-tenancy</span></span>
<span data-ttu-id="eb51f-221">Cosmos DB를 사용하여 다중 테넌트 응용 프로그램을 구현하는 경우 테넌트당 하나의 파티션 키 및 테넌트당 하나의 컨테이너라는 두 가지 인기 있는 패턴이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-221">If you are implementing a multi-tenant application using Cosmos DB, there are two popular patterns – one partition key per tenant, and one container per tenant.</span></span> <span data-ttu-id="eb51f-222">Hello 장점 및 단점 각각에 대해 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-222">Here are hello pros and cons for each:</span></span>

* <span data-ttu-id="eb51f-223">테넌트당 하나의 파티션 키: 이 모델에서는 테넌트가 단일 컨테이너 내에 함께 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-223">One Partition Key per tenant: In this model, tenants are collocated within a single container.</span></span> <span data-ttu-id="eb51f-224">그러나 단일 파티션 내의 항목에 대한 쿼리 및 삽입을 단일 파티션에 대해 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-224">But queries and inserts for items within a single tenant can be performed against a single partition.</span></span> <span data-ttu-id="eb51f-225">또한 테넌트 내의 모든 항목에서 트랜잭션 논리를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-225">You can also implement transactional logic across all items within a tenant.</span></span> <span data-ttu-id="eb51f-226">다중 테넌트는 컨테이너를 공유하기 때문에 각 테넌트에 대한 추가 헤드룸을 프로비전하는 대신 테넌트에 대한 리소스를 풀링하여 저장소 및 처리량을 단일 컨테이너 내에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-226">Since multiple tenants share a container, you can save storage and throughput costs by pooling resources for tenants within a single container rather than provisioning extra headroom for each tenant.</span></span> <span data-ttu-id="eb51f-227">hello 단점은 테 넌 트 당 성능 격리는입니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-227">hello drawback is that you do not have performance isolation per tenant.</span></span> <span data-ttu-id="eb51f-228">테 넌 트에 대 한 toohello 전체 컨테이너 대상으로 vs 증가 적용 하는 성능/처리량 증가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-228">Performance/throughput increases apply toohello entire container vs targeted increases for tenants.</span></span>
* <span data-ttu-id="eb51f-229">테넌트당 하나의 컨테이너: 각 테넌트에 고유한 컨테이너가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-229">One Container per tenant: Each tenant has its own container.</span></span> <span data-ttu-id="eb51f-230">이 모델에서는 테넌트당 성능을 예약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-230">In this model, you can reserve performance per tenant.</span></span> <span data-ttu-id="eb51f-231">Cosmos DB의 새로운 프로비전 가격 책정 모델을 사용하는 이 모델은 몇몇 테넌트가 있는 다중 테넌트 응용 프로그램에 보다 비용 효율적입니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-231">With Cosmos DB's new provisioning pricing model, this model is more cost-effective for multi-tenant applications with a few tenants.</span></span>

<span data-ttu-id="eb51f-232">또한 collocates 작은 테 넌 트 및 테 넌 트 tootheir 자체 더 큰 컨테이너 마이그레이션합니다는 조합/계층화 된 접근 방식을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-232">You can also use a combination/tiered approach that collocates small tenants and migrates larger tenants tootheir own container.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eb51f-233">다음 단계</span><span class="sxs-lookup"><span data-stu-id="eb51f-233">Next steps</span></span>
<span data-ttu-id="eb51f-234">이 문서에서는 Azure Cosmos DB API를 사용하여 분할하기 위한 개념 및 모범 사례의 개요를 제공했습니다.</span><span class="sxs-lookup"><span data-stu-id="eb51f-234">In this article, we provided an overview for an overview of concepts and best practices for partitioning with any Azure Cosmos DB API.</span></span> 

* <span data-ttu-id="eb51f-235">[Azure Cosmos DB에서 프로비전된 처리량](request-units.md)에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="eb51f-235">Learn about [provisioned throughput in Azure Cosmos DB](request-units.md)</span></span>
* <span data-ttu-id="eb51f-236">[Azure Cosmos DB에서 글로벌 배포](distribute-data-globally.md)에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="eb51f-236">Learn about [global distribution in Azure Cosmos DB](distribute-data-globally.md)</span></span>




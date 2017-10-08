---
title: "aaaRequest 단위 및 예상 처리량-Azure Cosmos DB | Microsoft Docs"
description: "Toounderstand,이 지정 하 고 Azure Cosmos DB에서 요청 단위 요구 사항을 예측 하는 방법에 대해 알아봅니다."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: d0a3c310-eb63-4e45-8122-b7724095c32f
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 13c4e7aeb6222fa14ef982e238716e15a0159fd5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="request-units-in-azure-cosmos-db"></a><span data-ttu-id="3e47f-103">Azure Cosmos DB의 요청 단위</span><span class="sxs-lookup"><span data-stu-id="3e47f-103">Request Units in Azure Cosmos DB</span></span>
<span data-ttu-id="3e47f-104">지금 사용 가능: Azure Cosmos DB [요청 단위 계산기](https://www.documentdb.com/capacityplanner).</span><span class="sxs-lookup"><span data-stu-id="3e47f-104">Now available: Azure Cosmos DB [request unit calculator](https://www.documentdb.com/capacityplanner).</span></span> <span data-ttu-id="3e47f-105">자세한 내용을 보려면 [처리량 요구 예측](request-units.md#estimating-throughput-needs)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3e47f-105">Learn more in [Estimating your throughput needs](request-units.md#estimating-throughput-needs).</span></span>

![처리량 계산기][5]

## <a name="introduction"></a><span data-ttu-id="3e47f-107">소개</span><span class="sxs-lookup"><span data-stu-id="3e47f-107">Introduction</span></span>
<span data-ttu-id="3e47f-108">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/)는 전 세계에 배포된 Microsoft의 다중 모델 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-108">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) is Microsoft's globally distributed multi-model database.</span></span> <span data-ttu-id="3e47f-109">Azure Cosmos DB와 함께 하지 않는 toorent 가상 컴퓨터, 소프트웨어를 배포 했거나 데이터베이스를 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-109">With Azure Cosmos DB, you don't have toorent virtual machines, deploy software, or monitor databases.</span></span> <span data-ttu-id="3e47f-110">Azure Cosmos DB은 운영 하 고 Microsoft 상위 엔지니어 toodeliver world 클래스 가용성, 성능 및 데이터 보호에서 지속적으로 모니터링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-110">Azure Cosmos DB is operated and continuously monitored by Microsoft top engineers toodeliver world class availability, performance, and data protection.</span></span> <span data-ttu-id="3e47f-111">[DocumentDB SQL](documentdb-sql-query.md)(문서), MongoDB(문서), [Azure Table Storage](https://azure.microsoft.com/services/storage/tables/)(키-값) 및 [Gremlin](https://tinkerpop.apache.org/gremlin.html)(그래프)가 모두 기본적으로 지원되므로 원하는 API를 사용하여 데이터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-111">You can access your data using APIs of your choice, as [DocumentDB SQL](documentdb-sql-query.md) (document), MongoDB (document), [Azure Table Storage](https://azure.microsoft.com/services/storage/tables/) (key-value), and [Gremlin](https://tinkerpop.apache.org/gremlin.html) (graph) are all natively supported.</span></span> <span data-ttu-id="3e47f-112">Cosmos DB Azure의 hello 통화는 hello 요청 단위 (RU)입니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-112">hello currency of Azure Cosmos DB is hello Request Unit (RU).</span></span> <span data-ttu-id="3e47f-113">RUs와 않아도 tooreserve 읽기/쓰기 용량 또는 프로 비전 CPU, 메모리 및 IOPS입니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-113">With RUs, you do not need tooreserve read/write capacities or provision CPU, Memory and IOPS.</span></span>

<span data-ttu-id="3e47f-114">Azure Cosmos DB 간단한 읽기에서 사이의 다른 작업에 다양 한 Api 지원 하며 toocomplex graph 쿼리를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-114">Azure Cosmos DB supports a number of APIs with different operations ranging from simple reads and writes toocomplex graph queries.</span></span> <span data-ttu-id="3e47f-115">정규화 된 수량 할당 된 모든 요청 값이 같으면 이후 **요청 단위** 계산 필요한 tooserve hello 요청의 hello 금액에 따른 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-115">Since not all requests are equal, they are assigned a normalized quantity of **request units** based on hello amount of computation required tooserve hello request.</span></span> <span data-ttu-id="3e47f-116">작업에 대 한 요청 단위 수가 hello 결정적 이며 hello 응답 헤더를 통해 Azure Cosmos DB에서 모든 작업에서 사용 하는 요청 단위 수를 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-116">hello number of request units for an operation is deterministic, and you can track hello number of request units consumed by any operation in Azure Cosmos DB via a response header.</span></span> 

<span data-ttu-id="3e47f-117">tooprovide 예측 가능한 성능, 필요한 tooreserve 처리량이 100 단위에서 RU 수/초입니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-117">tooprovide predictable performance, you need tooreserve throughput in units of 100 RU/second.</span></span> 

<span data-ttu-id="3e47f-118">이 문서를 읽은 후 다음 질문 수 tooanswer hello 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-118">After reading this article, you'll be able tooanswer hello following questions:</span></span>  

* <span data-ttu-id="3e47f-119">요청 단위 및 요청 요금이 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="3e47f-119">What are request units and request charges?</span></span>
* <span data-ttu-id="3e47f-120">컬렉션에 대해 요청 단위 용량을 지정하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="3e47f-120">How do I specify request unit capacity for a collection?</span></span>
* <span data-ttu-id="3e47f-121">내 응용 프로그램에 필요한 요청 단위를 어떻게 추정할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="3e47f-121">How do I estimate my application's request unit needs?</span></span>
* <span data-ttu-id="3e47f-122">컬렉션의 요청 단위 용량을 초과하면 어떻게 되나요?</span><span class="sxs-lookup"><span data-stu-id="3e47f-122">What happens if I exceed request unit capacity for a collection?</span></span>

<span data-ttu-id="3e47f-123">Azure Cosmos DB 다중 모델 데이터베이스는 때 중요 한 toonote 문서 API, graph API에 대 한 그래프/노드 및 테이블 API에 대 한 테이블/엔터티 tooa 컬렉션/문서는 이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-123">As Azure Cosmos DB is a multi-model database, it is important toonote that we will refer tooa collection/document for a document API, a graph/node for a graph API and a table/entity for table API.</span></span> <span data-ttu-id="3e47f-124">처리량이이 문서에서는 toohello 개념 컨테이너/항목의 일반화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-124">Throughput this document we will generalize toohello concepts of container/item.</span></span>

## <a name="request-units-and-request-charges"></a><span data-ttu-id="3e47f-125">요청 단위 및 요청 요금</span><span class="sxs-lookup"><span data-stu-id="3e47f-125">Request units and request charges</span></span>
<span data-ttu-id="3e47f-126">Azure Cosmos DB 하 여 신속 하 고 예측 가능한 성능을 제공 *예약* 리소스 toosatisfy 응용 프로그램의 처리량이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-126">Azure Cosmos DB delivers fast, predictable performance by *reserving* resources toosatisfy your application's throughput needs.</span></span>  <span data-ttu-id="3e47f-127">응용 프로그램 로드 시간에 따른 변경을 패턴에 액세스 하기 때문에 Azure Cosmos DB tooeasily 증가 허용 또는 예약 된 처리량 tooyour 사용 가능한 응용 프로그램의 hello 양을 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-127">Because application load and access patterns change over time, Azure Cosmos DB allows you tooeasily increase or decrease hello amount of reserved throughput available tooyour application.</span></span>

<span data-ttu-id="3e47f-128">Azure Cosmos DB에서는 예약된 처리량이 초당 처리되는 요청 단위로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-128">With Azure Cosmos DB, reserved throughput is specified in terms of request units processing per second.</span></span> <span data-ttu-id="3e47f-129">상상할 수 있는 요청 단위 처리량 통화로, 그에 따라 있습니다 *예약* 는 양의 초 단위로에서 사용할 수 있는 tooyour 응용 프로그램 요청 단위를 보장 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-129">You can think of request units as throughput currency, whereby you *reserve* an amount of guaranteed request units available tooyour application on per second basis.</span></span>  <span data-ttu-id="3e47f-130">문서 작성, 쿼리 수행, 문서 업데이트 등 Azure Cosmos DB의 각 작업에서는 CPU, 메모리 및 IOPS를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-130">Each operation in Azure Cosmos DB - writing a document, performing a query, updating a document - consumes CPU, memory, and IOPS.</span></span>  <span data-ttu-id="3e47f-131">즉, 각 작업이 *요청 요금*을 발생시키고, 요청 요금은 *요청 단위*로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-131">That is, each operation incurs a *request charge*, which is expressed in *request units*.</span></span>  <span data-ttu-id="3e47f-132">응용 프로그램의 처리량 요구 사항 함께 요청 단위 요금에 영향을 주는 hello 요인을 이해 가능한 한 효과적으로 비용으로 응용을 프로그램 toorun 있습니다 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-132">Understanding hello factors which impact request unit charges, along with your application's throughput requirements, enables you toorun your application as cost effectively as possible.</span></span> <span data-ttu-id="3e47f-133">hello 쿼리 탐색기는 쿼리는 매우 유용한 도구 tootest hello 코어 이기도합니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-133">hello query explorer is also a wonderful tool tootest hello core of a query.</span></span>

<span data-ttu-id="3e47f-134">다음 비디오에서는 Aravind Ramachandran 요청 단위 및 Azure Cosmos DB와 함께 예측 가능한 성능의 설명 하는 여기서 hello를 시청 하 여 시작 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-134">We recommend getting started by watching hello following video, where Aravind Ramachandran explains request units and predictable performance with Azure Cosmos DB.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Predictable-Performance-with-DocumentDB/player]
> 
> 

## <a name="specifying-request-unit-capacity-in-azure-cosmos-db"></a><span data-ttu-id="3e47f-135">Azure Cosmos DB에서 요청 단위 용량 지정</span><span class="sxs-lookup"><span data-stu-id="3e47f-135">Specifying request unit capacity in Azure Cosmos DB</span></span>
<span data-ttu-id="3e47f-136">Hello 수를 지정 하는 새 컬렉션, 테이블 또는 그래프를 시작할 때 예약 하려면 (초당 RU) 초당 요청 단위입니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-136">When starting a new collection, table or graph, you specify hello number of request units per second (RU per second) you want reserved.</span></span> <span data-ttu-id="3e47f-137">Hello 프로 비전 된 처리량에 따라, Azure Cosmos DB 할당 실제 파티션을 toohost 컬렉션 및 분할/rebalances 데이터 파티션에서 커짐에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-137">Based on hello provisioned throughput, Azure Cosmos DB allocates physical partitions toohost your collection and splits/rebalances data across partitions as it grows.</span></span>

<span data-ttu-id="3e47f-138">Azure Cosmos DB 파티션 키 toobe 컬렉션은 2, 500 요청 단위를 통해 프로 비전 또는 더 높은 때을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-138">Azure Cosmos DB requires a partition key toobe specified when a collection is provisioned with 2,500 request units or higher.</span></span> <span data-ttu-id="3e47f-139">파티션 키는도 필요한 tooscale 컬렉션의 처리량 hello 향후 2, 500 요청 단위를 초과 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-139">A partition key is also required tooscale your collection's throughput beyond 2,500 request units in hello future.</span></span> <span data-ttu-id="3e47f-140">따라서이 가장 좋습니다 tooconfigure는 [파티션 키](partition-data.md) 초기 처리량에 관계 없이 컨테이너를 만들 때.</span><span class="sxs-lookup"><span data-stu-id="3e47f-140">Therefore, it is highly recommended tooconfigure a [partition key](partition-data.md) when creating a container regardless of your initial throughput.</span></span> <span data-ttu-id="3e47f-141">이기 때문에 데이터를 여러 파티션에 분할 toobe 해야할 필요한 toopick 카디널리티가 높은 (고유 값 100 toomillions) 컬렉션/테이블/그래프 및 요청 균일 하 게 하 여 확장할 있습니다 Azure Cosmos DB 수 있도록 하는 파티션 키입니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-141">Since your data might have toobe split across multiple partitions, it is necessary toopick a partition key that has a high cardinality (100 toomillions of distinct values) so that your collection/table/graph and requests can be scaled uniformly by Azure Cosmos DB.</span></span> 

> [!NOTE]
> <span data-ttu-id="3e47f-142">파티션 키는 논리적 경계이며 실제 경계가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-142">A partition key is a logical boundary, and not a physical one.</span></span> <span data-ttu-id="3e47f-143">따라서 toolimit hello 고유 파티션 키 값 수가 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-143">Therefore, you do not need toolimit hello number of distinct partition key values.</span></span> <span data-ttu-id="3e47f-144">더 나은 toohave 더 분명가 실제로 Azure Cosmos DB에 더 많은 부하 분산 옵션, 보다 키 값을 분할 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-144">It is in fact better toohave more distinct partition key values than less, as Azure Cosmos DB has more load balancing options.</span></span>

<span data-ttu-id="3e47f-145">다음은 3, 000으로 컬렉션을 만들기 위한 코드 조각 사용 하 고 초당 단위 hello.NET SDK 요청:</span><span class="sxs-lookup"><span data-stu-id="3e47f-145">Here is a code snippet for creating a collection with 3,000 request units per second using hello .NET SDK:</span></span>

```csharp
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 3000 });
```

<span data-ttu-id="3e47f-146">Azure Cosmos DB는 처리량의 예약 모델에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-146">Azure Cosmos DB operates on a reservation model on throughput.</span></span> <span data-ttu-id="3e47f-147">즉, 처리량 양을 hello에 대 한 요금이 청구 됩니다 *예약*적극적으로 어느 정도의 처리량 인지에 관계 없이 *사용*합니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-147">That is, you are billed for hello amount of throughput *reserved*, regardless of how much of that throughput is actively *used*.</span></span> <span data-ttu-id="3e47f-148">응용 프로그램의 로드, 데이터 및 사용 패턴 변경 위쪽 / 아래쪽에 쉽게 확장할 수으로 Sdk 통해 예약 된 RUs 양을 hello 또는 hello를 사용 하 여 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-148">As your application's load, data, and usage patterns change you can easily scale up and down hello amount of reserved RUs through SDKs or using hello [Azure Portal](https://portal.azure.com).</span></span>

<span data-ttu-id="3e47f-149">각 컬렉션/테이블/그래프 매핑된 tooan `Offer` hello 프로 비전 된 처리량에 대 한 메타 데이터가 Cosmos db에서 Azure 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-149">Each collection/table/graph are mapped tooan `Offer` resource in Azure Cosmos DB, which has metadata about hello provisioned throughput.</span></span> <span data-ttu-id="3e47f-150">컨테이너에 대 한 hello 해당 제안 리소스를 찾는 다음 hello 새 처리량 값으로 업데이트 하 여 할당 된 hello 처리량을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-150">You can change hello allocated throughput by looking up hello corresponding offer resource for a container, then updating it with hello new throughput value.</span></span> <span data-ttu-id="3e47f-151">다음 컬렉션 too5의 hello 처리량을 변경 하기 위한 코드 조각으로 사용 하 고 초당 요청 단위 000 hello.NET SDK.</span><span class="sxs-lookup"><span data-stu-id="3e47f-151">Here is a code snippet for changing hello throughput of a collection too5,000 request units per second using hello .NET SDK:</span></span>

```csharp
// Fetch hello resource toobe updated
Offer offer = client.CreateOfferQuery()
                .Where(r => r.ResourceLink == collection.SelfLink)    
                .AsEnumerable()
                .SingleOrDefault();

// Set hello throughput too5000 request units per second
offer = new OfferV2(offer, 5000);

// Now persist these changes toohello database by replacing hello original resource
await client.ReplaceOfferAsync(offer);
```

<span data-ttu-id="3e47f-152">Hello 처리량을 변경 하면 영향 toohello 컨테이너의 사용 가능한 시간이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-152">There is no impact toohello availability of your container when you change hello throughput.</span></span> <span data-ttu-id="3e47f-153">일반적으로 hello 새롭게 예약 된 처리량은 hello 새 처리량의 응용 프로그램에 몇 초 이내 효과적입니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-153">Typically hello new reserved throughput is effective within seconds on application of hello new throughput.</span></span>

## <a name="request-unit-considerations"></a><span data-ttu-id="3e47f-154">요청 단위 고려 사항</span><span class="sxs-lookup"><span data-stu-id="3e47f-154">Request unit considerations</span></span>
<span data-ttu-id="3e47f-155">Cosmos DB Azure 컨테이너에 대 한 요청 단위 tooreserve hello 수 예측, 경우에 변수 고려 사항에 따라 중요 한 tootake hello:</span><span class="sxs-lookup"><span data-stu-id="3e47f-155">When estimating hello number of request units tooreserve for your Azure Cosmos DB container, it is important tootake hello following variables into consideration:</span></span>

* <span data-ttu-id="3e47f-156">**항목 크기**.</span><span class="sxs-lookup"><span data-stu-id="3e47f-156">**Item size**.</span></span> <span data-ttu-id="3e47f-157">크기가 증가 hello 사용 된 단위 tooread 또는 hello 데이터 쓰기 늘어납니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-157">As size increases hello units consumed tooread or write hello data will also increase.</span></span>
* <span data-ttu-id="3e47f-158">**항목 속성 개수**.</span><span class="sxs-lookup"><span data-stu-id="3e47f-158">**Item property count**.</span></span> <span data-ttu-id="3e47f-159">문서/노드/ntity hello 속성 수가 증가 함에 따라 증가 합니다 hello 사용 된 단위 toowrite 모든 속성의 기본 인덱싱 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-159">Assuming default indexing of all properties, hello units consumed toowrite a document/node/ntity will increase as hello property count increases.</span></span>
* <span data-ttu-id="3e47f-160">**데이터 일관성**.</span><span class="sxs-lookup"><span data-stu-id="3e47f-160">**Data consistency**.</span></span> <span data-ttu-id="3e47f-161">Strong 또는 Bounded Staleness의 데이터 일관성 수준을 사용 하는 경우 추가 단위가 소비 된 tooread 항목 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-161">When using data consistency levels of Strong or Bounded Staleness, additional units will be consumed tooread items.</span></span>
* <span data-ttu-id="3e47f-162">**인덱싱된 속성**.</span><span class="sxs-lookup"><span data-stu-id="3e47f-162">**Indexed properties**.</span></span> <span data-ttu-id="3e47f-163">각 컨테이너의 인덱스 정책에 따라 기본적으로 인덱싱되는 속성이 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-163">An index policy on each container determines which properties are indexed by default.</span></span> <span data-ttu-id="3e47f-164">인덱싱된 속성의 hello 수를 제한 하거나 lazy 인덱싱을 사용 하도록 설정 하 여 요청 단위 사용을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-164">You can reduce your request unit consumption by limiting hello number of indexed properties or by enabling lazy indexing.</span></span>
* <span data-ttu-id="3e47f-165">**문서 인덱싱**.</span><span class="sxs-lookup"><span data-stu-id="3e47f-165">**Document indexing**.</span></span> <span data-ttu-id="3e47f-166">각 항목은 자동으로 인덱싱됩니다 기본적으로 항목의 일부 하지 tooindex 선택 하는 경우 더 적은 요청 단위를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-166">By default each item is automatically indexed, you will consume fewer request units if you choose not tooindex some of your items.</span></span>
* <span data-ttu-id="3e47f-167">**쿼리 패턴**.</span><span class="sxs-lookup"><span data-stu-id="3e47f-167">**Query patterns**.</span></span> <span data-ttu-id="3e47f-168">hello 복잡 한 쿼리 요청 단위의 수는 작업에 대 한 사용 되는 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-168">hello complexity of a query impacts how many Request Units are consumed for an operation.</span></span> <span data-ttu-id="3e47f-169">조건자의 hello 개수, hello 조건자, 프로젝션, Udf의 수와 모든 영향을 줄의 hello 비용 hello 원본 데이터 집합의 hello 크기의 특성 작업을 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-169">hello number of predicates, nature of hello predicates, projections, number of UDFs, and hello size of hello source data set all influence hello cost of query operations.</span></span>
* <span data-ttu-id="3e47f-170">**스크립트 사용량**.</span><span class="sxs-lookup"><span data-stu-id="3e47f-170">**Script usage**.</span></span>  <span data-ttu-id="3e47f-171">저장된 프로시저 및 트리거는 쿼리와 마찬가지로 수행 되는 hello 작업의 hello 복잡성에 따라 요청 단위 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-171">As with queries, stored procedures and triggers consume request units based on hello complexity of hello operations being performed.</span></span> <span data-ttu-id="3e47f-172">응용 프로그램을 개발할 때는 hello 요청 충전 검사 헤더 toobetter 각 작업은 요청 단위 용량을 사용 하는 방법을 이해 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-172">As you develop your application, inspect hello request charge header toobetter understand how each operation is consuming request unit capacity.</span></span>

## <a name="estimating-throughput-needs"></a><span data-ttu-id="3e47f-173">필요한 처리량 예측</span><span class="sxs-lookup"><span data-stu-id="3e47f-173">Estimating throughput needs</span></span>
<span data-ttu-id="3e47f-174">요청 단위는 요청 처리 비용의 정규화된 측정값입니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-174">A request unit is a normalized measure of request processing cost.</span></span> <span data-ttu-id="3e47f-175">단일 요청 단위 (시스템 속성은 제외) 10 개의 고유 속성 값을 항목으로 구성 된 단일 1KB hello 처리 필요한 용량 tooread를 (통해 자체 링크 또는 id)를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-175">A single request unit represents hello processing capacity required tooread (via self link or id) a single 1KB item consisting of 10 unique property values (excluding system properties).</span></span> <span data-ttu-id="3e47f-176">요청 toocreate (삽입) 바꾸거나 hello 동일 항목을 사용 하면 추가 처리가 hello 서비스에서 삭제 및 함으로써 더 요청 단위입니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-176">A request toocreate (insert), replace or delete hello same item will consume more processing from hello service and thereby more request units.</span></span>   

> [!NOTE]
> <span data-ttu-id="3e47f-177">1 개의 요청이 단위의 hello 초기는 1KB tooa 간단한를 해당 항목에 대 한 자체 링크 또는 hello 항목의 id로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-177">hello baseline of 1 request unit for a 1KB item corresponds tooa simple GET by self link or id of hello item.</span></span>
> 
> 

<span data-ttu-id="3e47f-178">예를 들어 다음 요청 수를 보여 주는 표는 세 가지 다른 항목 크기 (1KB, 4KB 이며 및 64KB) 및 두 개의 서로 다른 성능 수준에서 단위 tooprovision (500 읽기/초 + 100 쓰기/초 및 500 읽기/초 + 500 쓰기/초)입니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-178">For example, here's a table that shows how many request units tooprovision at three different item sizes (1KB, 4KB, and 64KB) and at two different performance levels (500 reads/second + 100 writes/second and 500 reads/second + 500 writes/second).</span></span> <span data-ttu-id="3e47f-179">세션에서 구성 된 hello 데이터 일관성 및 인덱싱 정책을 hello tooNone 설정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-179">hello data consistency was configured at Session, and hello indexing policy was set tooNone.</span></span>

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><span data-ttu-id="3e47f-180"><strong>항목 크기</strong></span><span class="sxs-lookup"><span data-stu-id="3e47f-180"><strong>Item size</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="3e47f-181"><strong>읽기/초</strong></span><span class="sxs-lookup"><span data-stu-id="3e47f-181"><strong>Reads/second</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="3e47f-182"><strong>쓰기/초</strong></span><span class="sxs-lookup"><span data-stu-id="3e47f-182"><strong>Writes/second</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="3e47f-183"><strong>요청 단위</strong></span><span class="sxs-lookup"><span data-stu-id="3e47f-183"><strong>Request units</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="3e47f-184">1KB</span><span class="sxs-lookup"><span data-stu-id="3e47f-184">1 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="3e47f-185">500</span><span class="sxs-lookup"><span data-stu-id="3e47f-185">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="3e47f-186">100</span><span class="sxs-lookup"><span data-stu-id="3e47f-186">100</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="3e47f-187">(500 * 1) + (100 * 5) = 1,000RU/s</span><span class="sxs-lookup"><span data-stu-id="3e47f-187">(500 * 1) + (100 * 5) = 1,000 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="3e47f-188">1KB</span><span class="sxs-lookup"><span data-stu-id="3e47f-188">1 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="3e47f-189">500</span><span class="sxs-lookup"><span data-stu-id="3e47f-189">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="3e47f-190">500</span><span class="sxs-lookup"><span data-stu-id="3e47f-190">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="3e47f-191">(500 * 1) + (500 * 5) = 3,000RU/s</span><span class="sxs-lookup"><span data-stu-id="3e47f-191">(500 * 1) + (500 * 5) = 3,000 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="3e47f-192">4KB</span><span class="sxs-lookup"><span data-stu-id="3e47f-192">4 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="3e47f-193">500</span><span class="sxs-lookup"><span data-stu-id="3e47f-193">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="3e47f-194">100</span><span class="sxs-lookup"><span data-stu-id="3e47f-194">100</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="3e47f-195">(500 * 1.3) + (100 * 7) = 1,350RU/s</span><span class="sxs-lookup"><span data-stu-id="3e47f-195">(500 * 1.3) + (100 * 7) = 1,350 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="3e47f-196">4KB</span><span class="sxs-lookup"><span data-stu-id="3e47f-196">4 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="3e47f-197">500</span><span class="sxs-lookup"><span data-stu-id="3e47f-197">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="3e47f-198">500</span><span class="sxs-lookup"><span data-stu-id="3e47f-198">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="3e47f-199">(500 * 1.3) + (500 * 7) = 4,150RU/s</span><span class="sxs-lookup"><span data-stu-id="3e47f-199">(500 * 1.3) + (500 * 7) = 4,150 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="3e47f-200">64KB</span><span class="sxs-lookup"><span data-stu-id="3e47f-200">64 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="3e47f-201">500</span><span class="sxs-lookup"><span data-stu-id="3e47f-201">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="3e47f-202">100</span><span class="sxs-lookup"><span data-stu-id="3e47f-202">100</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="3e47f-203">(500 * 10) + (100 * 48) = 9,800RU/s</span><span class="sxs-lookup"><span data-stu-id="3e47f-203">(500 * 10) + (100 * 48) = 9,800 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="3e47f-204">64KB</span><span class="sxs-lookup"><span data-stu-id="3e47f-204">64 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="3e47f-205">500</span><span class="sxs-lookup"><span data-stu-id="3e47f-205">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="3e47f-206">500</span><span class="sxs-lookup"><span data-stu-id="3e47f-206">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="3e47f-207">(500 * 10) + (500 * 48) = 29,000RU/s</span><span class="sxs-lookup"><span data-stu-id="3e47f-207">(500 * 10) + (500 * 48) = 29,000 RU/s</span></span></p></td>
        </tr>
    </tbody>
</table>

### <a name="use-hello-request-unit-calculator"></a><span data-ttu-id="3e47f-208">Hello 요청 단위 계산기를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="3e47f-208">Use hello request unit calculator</span></span>
<span data-ttu-id="3e47f-209">미세 하 게 toohelp 고객의 처리량은 예측이 잘못 조정, 기반으로 웹이 [요청 단위 계산기](https://www.documentdb.com/capacityplanner) toohelp hello 요청 단위에 필요한 예측 등과 같은 일반적인 작업을 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-209">toohelp customers fine tune their throughput estimations, there is a web based [request unit calculator](https://www.documentdb.com/capacityplanner) toohelp estimate hello request unit requirements for typical operations, including:</span></span>

* <span data-ttu-id="3e47f-210">항목 만들기(쓰기)</span><span class="sxs-lookup"><span data-stu-id="3e47f-210">Item creates (writes)</span></span>
* <span data-ttu-id="3e47f-211">항목 읽기</span><span class="sxs-lookup"><span data-stu-id="3e47f-211">Item reads</span></span>
* <span data-ttu-id="3e47f-212">항목 삭제</span><span class="sxs-lookup"><span data-stu-id="3e47f-212">Item deletes</span></span>
* <span data-ttu-id="3e47f-213">항목 업데이트</span><span class="sxs-lookup"><span data-stu-id="3e47f-213">Item updates</span></span>

<span data-ttu-id="3e47f-214">hello 도구에는 데이터 저장소 요구를 제공 하는 hello 샘플 항목을 기반으로 예측에 대 한 지원이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-214">hello tool also includes support for estimating data storage needs based on hello sample items you provide.</span></span>

<span data-ttu-id="3e47f-215">Hello 도구를 사용 하는 것은 간단 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-215">Using hello tool is simple:</span></span>

1. <span data-ttu-id="3e47f-216">하나 이상의 대표 항목을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-216">Upload one or more representative items.</span></span>
   
    ![항목 toohello 요청 단위 계산기를 업로드 합니다.][2]
2. <span data-ttu-id="3e47f-218">tooestimate 데이터 저장소 요구 사항 hello 총 수를 입력 하려는 toostore 항목의 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-218">tooestimate data storage requirements, enter hello total number of items you expect toostore.</span></span>
3. <span data-ttu-id="3e47f-219">입력 항목 수가 hello 만들기, 읽기, 업데이트 및 삭제 작업 (초 단위 기준) 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-219">Enter hello number of items create, read, update, and delete operations you require (on a per-second basis).</span></span> <span data-ttu-id="3e47f-220">항목 업데이트 작업의 tooestimate hello 요청 단위 요금이 일반적인 필드 업데이트가 포함 된 위의 1 단계에서 hello 샘플 항목의 복사본을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-220">tooestimate hello request unit charges of item update operations, upload a copy of hello sample item from step 1 above that includes typical field updates.</span></span>  <span data-ttu-id="3e47f-221">예를 들어 항목 업데이트 lastLogin 및 userVisits, 라는 두 개의 속성을 수정 일반적으로 다음 hello 샘플 항목을 복사 하기만 하는 경우 이러한 두 속성에 대 한 hello 값 업데이트 되 고 복사 하는 hello 항목을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-221">For example, if item updates typically modify two properties named lastLogin and userVisits, then simply copy hello sample item, update hello values for those two properties, and upload hello copied item.</span></span>
   
    ![Hello 요청 단위 계산기의 처리량 요구 사항을 입력합니다][3]
4. <span data-ttu-id="3e47f-223">클릭 하 여 계산 하 고 hello 결과 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-223">Click calculate and examine hello results.</span></span>
   
    ![요청 단위 계산기 결과][4]

> [!NOTE]
> <span data-ttu-id="3e47f-225">인덱싱된 속성의 크기와 hello 수 측면에서 크게 달라 집니다 항목 형식을 설정한 경우 다음 각 예제 업로드 *형식* 일반적인 항목 toohello의 도구를 다음 hello 결과 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-225">If you have item types which will differ dramatically in terms of size and hello number of indexed properties, then upload a sample of each *type* of typical item toohello tool and then calculate hello results.</span></span>
> 
> 

### <a name="use-hello-azure-cosmos-db-request-charge-response-header"></a><span data-ttu-id="3e47f-226">Hello Azure Cosmos DB 요청 충전 응답 헤더를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="3e47f-226">Use hello Azure Cosmos DB request charge response header</span></span>
<span data-ttu-id="3e47f-227">사용자 지정 헤더를 포함 하는 hello Azure Cosmos DB 서비스에서에서 모든 응답 (`x-ms-request-charge`) hello 요청에 대 한 사용 된 hello 요청 단위를 포함 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-227">Every response from hello Azure Cosmos DB service includes a custom header (`x-ms-request-charge`) that contains hello request units consumed for hello request.</span></span> <span data-ttu-id="3e47f-228">이 헤더 hello Azure Cosmos DB Sdk를 통해 액세스할 수 이기도합니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-228">This header is also accessible through hello Azure Cosmos DB SDKs.</span></span> <span data-ttu-id="3e47f-229">.NET SDK hello RequestCharge hello ResourceResponse 개체의 속성을입니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-229">In hello .NET SDK, RequestCharge is a property of hello ResourceResponse object.</span></span>  <span data-ttu-id="3e47f-230">쿼리에 대 한 hello Azure 포털에서에서 Azure Cosmos DB 쿼리 탐색기 hello 실행 된 쿼리에 대 한 요청 충전 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-230">For queries, hello Azure Cosmos DB Query Explorer in hello Azure portal provides request charge information for executed queries.</span></span>

![쿼리 탐색기 hello에 RU 요금을 검사 하는 중][1]

<span data-ttu-id="3e47f-232">이 점을 고려 hello 양을 응용 프로그램에 필요한 예약 된 처리량을 예측 하기 위한 한 가지 방법은 toorecord hello 요청 단위 충전 응용 프로그램에서 사용 되는 대표적인 항목에 대해 실행 되는 일반적인 작업와 관련 된 다음 매 초 마다 수행 예상 hello 작업 수를 예측 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-232">With this in mind, one method for estimating hello amount of reserved throughput required by your application is toorecord hello request unit charge associated with running typical operations against a representative item used by your application and then estimating hello number of operations you anticipate performing each second.</span></span>  <span data-ttu-id="3e47f-233">있는지 toomeasure 되며 일반적인 쿼리 및 뿐만 아니라 Azure Cosmos DB 스크립트 사용 등.</span><span class="sxs-lookup"><span data-stu-id="3e47f-233">Be sure toomeasure and include typical queries and Azure Cosmos DB script usage as well.</span></span>

> [!NOTE]
> <span data-ttu-id="3e47f-234">인덱싱된 속성의 크기와 hello 수 측면에서 크게 달라 집니다 항목 형식을 설정한 경우 다음 hello 적용 가능한 작업과 요청 단위 충전 각 연결 된 기록 *형식* 일반적인 항목의 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-234">If you have item types which will differ dramatically in terms of size and hello number of indexed properties, then record hello applicable operation request unit charge associated with each *type* of typical item.</span></span>
> 
> 

<span data-ttu-id="3e47f-235">예:</span><span class="sxs-lookup"><span data-stu-id="3e47f-235">For example:</span></span>

1. <span data-ttu-id="3e47f-236">기록 hello 요청 단위 효율적인 (삽입)를 만드는 일반적인 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-236">Record hello request unit charge of creating (inserting) a typical item.</span></span> 
2. <span data-ttu-id="3e47f-237">일반적인 항목을 읽을 레코드 hello 요청 단위 요금이 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-237">Record hello request unit charge of reading a typical item.</span></span>
3. <span data-ttu-id="3e47f-238">레코드 hello 요청 단위 효율적인 일반적인 항목을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-238">Record hello request unit charge of updating a typical item.</span></span>
4. <span data-ttu-id="3e47f-239">레코드 hello 요청 단위 요금이 청구 일반적이 고 일반적인 항목 쿼리.</span><span class="sxs-lookup"><span data-stu-id="3e47f-239">Record hello request unit charge of typical, common item queries.</span></span>
5. <span data-ttu-id="3e47f-240">레코드 hello 요청 단위 효율적인 사용자 정의 스크립트 (저장된 프로시저, 트리거, 사용자 정의 함수) hello 응용 프로그램에서 활용</span><span class="sxs-lookup"><span data-stu-id="3e47f-240">Record hello request unit charge of any custom scripts (stored procedures, triggers, user-defined functions) leveraged by hello application</span></span>
6. <span data-ttu-id="3e47f-241">작업의 수를 예상 하는 hello 주어진 단위를 예상 toorun 매 초 마다 hello 필요한 요청을 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-241">Calculate hello required request units given hello estimated number of operations you anticipate toorun each second.</span></span>

### <span data-ttu-id="3e47f-242"><a id="GetLastRequestStatistics"></a>MongoDB API의 GetLastRequestStatistics 명령 사용</span><span class="sxs-lookup"><span data-stu-id="3e47f-242"><a id="GetLastRequestStatistics"></a>Use API for MongoDB's GetLastRequestStatistics command</span></span>
<span data-ttu-id="3e47f-243">MongoDB에 대 한 API 지원 사용자 지정 명령 *getLastRequestStatistics*, 지정 된 작업에 대 한 요청 충전 hello를 검색 하기 위한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-243">API for MongoDB supports a custom command, *getLastRequestStatistics*, for retrieving hello request charge for specified operations.</span></span>

<span data-ttu-id="3e47f-244">예를 들어 hello Mongo 셸을, tooverify hello 요청 요금은 hello 작업을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-244">For example, in hello Mongo Shell, execute hello operation you want tooverify hello request charge for.</span></span>
```
> db.sample.find()
```

<span data-ttu-id="3e47f-245">다음을 실행 하는 hello 명령 *getLastRequestStatistics*합니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-245">Next, execute hello command *getLastRequestStatistics*.</span></span>
```
> db.runCommand({getLastRequestStatistics: 1})
{
    "_t": "GetRequestStatisticsResponse",
    "ok": 1,
    "CommandName": "OP_QUERY",
    "RequestCharge": 2.48,
    "RequestDurationInMilliSeconds" : 4.0048
}
```

<span data-ttu-id="3e47f-246">이 점을 고려 hello 양을 응용 프로그램에 필요한 예약 된 처리량을 예측 하기 위한 한 가지 방법은 toorecord hello 요청 단위 충전 응용 프로그램에서 사용 되는 대표적인 항목에 대해 실행 되는 일반적인 작업와 관련 된 다음 매 초 마다 수행 예상 hello 작업 수를 예측 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-246">With this in mind, one method for estimating hello amount of reserved throughput required by your application is toorecord hello request unit charge associated with running typical operations against a representative item used by your application and then estimating hello number of operations you anticipate performing each second.</span></span>

> [!NOTE]
> <span data-ttu-id="3e47f-247">인덱싱된 속성의 크기와 hello 수 측면에서 크게 달라 집니다 항목 형식을 설정한 경우 다음 hello 적용 가능한 작업과 요청 단위 충전 각 연결 된 기록 *형식* 일반적인 항목의 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-247">If you have item types which will differ dramatically in terms of size and hello number of indexed properties, then record hello applicable operation request unit charge associated with each *type* of typical item.</span></span>
> 
> 

## <a name="use-api-for-mongodbs-portal-metrics"></a><span data-ttu-id="3e47f-248">MongoDB API 포털 메트릭 사용</span><span class="sxs-lookup"><span data-stu-id="3e47f-248">Use API for MongoDB's portal metrics</span></span>
<span data-ttu-id="3e47f-249">MongoDB 데이터베이스 toouse hello에 대 한 API에 대 한 요금이 청구 요청 단위의 좋은 예측 하는 가장 간단한 방법은 tooget hello [Azure 포털](https://portal.azure.com) 메트릭.</span><span class="sxs-lookup"><span data-stu-id="3e47f-249">hello simplest way tooget a good estimation of request unit charges for your API for MongoDB database is toouse hello [Azure portal](https://portal.azure.com) metrics.</span></span> <span data-ttu-id="3e47f-250">Hello로 *요청 수가* 및 *요청 충전* 차트, 요청 단위를 사용 중인 각 작업은 요청 단위의 수의 예측을 얻을 수 있습니다 상대 tooone 차지 다른 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-250">With hello *Number of requests* and *Request Charge* charts, you can get an estimation of how many request units each operation is consuming and how many request units they consume relative tooone another.</span></span>

![MongoDB API 포털 메트릭][6]

## <a name="a-request-unit-estimation-example"></a><span data-ttu-id="3e47f-252">요청 단위 추정 예제</span><span class="sxs-lookup"><span data-stu-id="3e47f-252">A request unit estimation example</span></span>
<span data-ttu-id="3e47f-253">Hello ~ 1 KB 문서 다음을 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-253">Consider hello following ~1KB document:</span></span>

```json
{
 "id": "08259",
  "description": "Cereals ready-to-eat, KELLOGG, KELLOGG'S CRISPIX",
  "tags": [
    {
      "name": "cereals ready-to-eat"
    },
    {
      "name": "kellogg"
    },
    {
      "name": "kellogg's crispix"
    }
  ],
  "version": 1,
  "commonName": "Includes USDA Commodity B855",
  "manufacturerName": "Kellogg, Co.",
  "isFromSurvey": false,
  "foodGroup": "Breakfast Cereals",
  "nutrients": [
    {
      "id": "262",
      "description": "Caffeine",
      "nutritionValue": 0,
      "units": "mg"
    },
    {
      "id": "307",
      "description": "Sodium, Na",
      "nutritionValue": 611,
      "units": "mg"
    },
    {
      "id": "309",
      "description": "Zinc, Zn",
      "nutritionValue": 5.2,
      "units": "mg"
    }
  ],
  "servings": [
    {
      "amount": 1,
      "description": "cup (1 NLEA serving)",
      "weightInGrams": 29
    }
  ]
}
```

> [!NOTE]
> <span data-ttu-id="3e47f-254">문서는 hello 시스템 위의 hello 문서 크기가 1KB 보다 약간 짧으므로 계산 되므로 Azure Cosmos DB에서 축소 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-254">Documents are minified in Azure Cosmos DB, so hello system calculated size of hello document above is slightly less than 1KB.</span></span>
> 
> 

<span data-ttu-id="3e47f-255">hello 다음 표에서 대략적인 요청을이 항목에 대 한 일반적인 작업에 대 한 단위 요금이 (hello 대략적인 요청 단위 충전 hello 계정 일관성 수준이 너무 설정 된 것으로 가정 "세션" 하 고 모든 항목은 자동으로 인덱스):</span><span class="sxs-lookup"><span data-stu-id="3e47f-255">hello following table shows approximate request unit charges for typical operations on this item (hello approximate request unit charge assumes that hello account consistency level is set too“Session” and that all items are automatically indexed):</span></span>

| <span data-ttu-id="3e47f-256">작업</span><span class="sxs-lookup"><span data-stu-id="3e47f-256">Operation</span></span> | <span data-ttu-id="3e47f-257">요청 단위 요금</span><span class="sxs-lookup"><span data-stu-id="3e47f-257">Request Unit Charge</span></span> |
| --- | --- |
| <span data-ttu-id="3e47f-258">항목 만들기</span><span class="sxs-lookup"><span data-stu-id="3e47f-258">Create item</span></span> |<span data-ttu-id="3e47f-259">~15 RU</span><span class="sxs-lookup"><span data-stu-id="3e47f-259">~15 RU</span></span> |
| <span data-ttu-id="3e47f-260">항목 읽기</span><span class="sxs-lookup"><span data-stu-id="3e47f-260">Read item</span></span> |<span data-ttu-id="3e47f-261">~1 RU</span><span class="sxs-lookup"><span data-stu-id="3e47f-261">~1 RU</span></span> |
| <span data-ttu-id="3e47f-262">ID로 항목 쿼리</span><span class="sxs-lookup"><span data-stu-id="3e47f-262">Query item by id</span></span> |<span data-ttu-id="3e47f-263">~2.5 RU</span><span class="sxs-lookup"><span data-stu-id="3e47f-263">~2.5 RU</span></span> |

<span data-ttu-id="3e47f-264">또한이 표에서 단위 요금이 hello 응용 프로그램에서 사용 되는 일반적인 쿼리에 대 한 대략적인 요청을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-264">Additionally, this table shows approximate request unit charges for typical queries used in hello application:</span></span>

| <span data-ttu-id="3e47f-265">쿼리</span><span class="sxs-lookup"><span data-stu-id="3e47f-265">Query</span></span> | <span data-ttu-id="3e47f-266">요청 단위 요금</span><span class="sxs-lookup"><span data-stu-id="3e47f-266">Request Unit Charge</span></span> | <span data-ttu-id="3e47f-267">반환된 항목 수</span><span class="sxs-lookup"><span data-stu-id="3e47f-267"># of Returned Items</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3e47f-268">ID로 음식 선택</span><span class="sxs-lookup"><span data-stu-id="3e47f-268">Select food by id</span></span> |<span data-ttu-id="3e47f-269">~2.5 RU</span><span class="sxs-lookup"><span data-stu-id="3e47f-269">~2.5 RU</span></span> |<span data-ttu-id="3e47f-270">1</span><span class="sxs-lookup"><span data-stu-id="3e47f-270">1</span></span> |
| <span data-ttu-id="3e47f-271">제조업체로 음식 선택</span><span class="sxs-lookup"><span data-stu-id="3e47f-271">Select foods by manufacturer</span></span> |<span data-ttu-id="3e47f-272">~7 RU</span><span class="sxs-lookup"><span data-stu-id="3e47f-272">~7 RU</span></span> |<span data-ttu-id="3e47f-273">7</span><span class="sxs-lookup"><span data-stu-id="3e47f-273">7</span></span> |
| <span data-ttu-id="3e47f-274">음식 그룹으로 선택하고 무게로 주문</span><span class="sxs-lookup"><span data-stu-id="3e47f-274">Select by food group and order by weight</span></span> |<span data-ttu-id="3e47f-275">~70 RU</span><span class="sxs-lookup"><span data-stu-id="3e47f-275">~70 RU</span></span> |<span data-ttu-id="3e47f-276">100</span><span class="sxs-lookup"><span data-stu-id="3e47f-276">100</span></span> |
| <span data-ttu-id="3e47f-277">음식 그룹의 상위 10개 음식 선택</span><span class="sxs-lookup"><span data-stu-id="3e47f-277">Select top 10 foods in a food group</span></span> |<span data-ttu-id="3e47f-278">~10 RU</span><span class="sxs-lookup"><span data-stu-id="3e47f-278">~10 RU</span></span> |<span data-ttu-id="3e47f-279">10</span><span class="sxs-lookup"><span data-stu-id="3e47f-279">10</span></span> |

> [!NOTE]
> <span data-ttu-id="3e47f-280">RU 요금 hello 반환 되는 항목 수에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-280">RU charges vary based on hello number of items returned.</span></span>
> 
> 

<span data-ttu-id="3e47f-281">이 정보를 통해 작업 및 쿼리 / 초 라고 생각이 제공 된 응용 프로그램 hello 수에 대 한 hello RU 요구 사항을 예상할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-281">With this information, we can estimate hello RU requirements for this application given hello number of operations and queries we expect per second:</span></span>

| <span data-ttu-id="3e47f-282">작업/쿼리</span><span class="sxs-lookup"><span data-stu-id="3e47f-282">Operation/Query</span></span> | <span data-ttu-id="3e47f-283">예상되는 초당 수</span><span class="sxs-lookup"><span data-stu-id="3e47f-283">Estimated number per second</span></span> | <span data-ttu-id="3e47f-284">필요한 RU</span><span class="sxs-lookup"><span data-stu-id="3e47f-284">Required RUs</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3e47f-285">항목 만들기</span><span class="sxs-lookup"><span data-stu-id="3e47f-285">Create item</span></span> |<span data-ttu-id="3e47f-286">10</span><span class="sxs-lookup"><span data-stu-id="3e47f-286">10</span></span> |<span data-ttu-id="3e47f-287">150</span><span class="sxs-lookup"><span data-stu-id="3e47f-287">150</span></span> |
| <span data-ttu-id="3e47f-288">항목 읽기</span><span class="sxs-lookup"><span data-stu-id="3e47f-288">Read item</span></span> |<span data-ttu-id="3e47f-289">100</span><span class="sxs-lookup"><span data-stu-id="3e47f-289">100</span></span> |<span data-ttu-id="3e47f-290">100</span><span class="sxs-lookup"><span data-stu-id="3e47f-290">100</span></span> |
| <span data-ttu-id="3e47f-291">제조업체로 음식 선택</span><span class="sxs-lookup"><span data-stu-id="3e47f-291">Select foods by manufacturer</span></span> |<span data-ttu-id="3e47f-292">25</span><span class="sxs-lookup"><span data-stu-id="3e47f-292">25</span></span> |<span data-ttu-id="3e47f-293">175</span><span class="sxs-lookup"><span data-stu-id="3e47f-293">175</span></span> |
| <span data-ttu-id="3e47f-294">음식 그룹으로 선택</span><span class="sxs-lookup"><span data-stu-id="3e47f-294">Select by food group</span></span> |<span data-ttu-id="3e47f-295">10</span><span class="sxs-lookup"><span data-stu-id="3e47f-295">10</span></span> |<span data-ttu-id="3e47f-296">700</span><span class="sxs-lookup"><span data-stu-id="3e47f-296">700</span></span> |
| <span data-ttu-id="3e47f-297">상위 10개 선택</span><span class="sxs-lookup"><span data-stu-id="3e47f-297">Select top 10</span></span> |<span data-ttu-id="3e47f-298">15</span><span class="sxs-lookup"><span data-stu-id="3e47f-298">15</span></span> |<span data-ttu-id="3e47f-299">총 150</span><span class="sxs-lookup"><span data-stu-id="3e47f-299">150 Total</span></span> |

<span data-ttu-id="3e47f-300">이 예에서는 필요한 평균 처리량이 1,275 RU/s로 예상됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-300">In this case, we expect an average throughput requirement of 1,275 RU/s.</span></span>  <span data-ttu-id="3e47f-301">100 가장 가까운 toohello를 반올림이 응용 프로그램의이 컬렉션에 대 한 1, 300 000RU/s를 프로 비전는 했습니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-301">Rounding up toohello nearest 100, we would provision 1,300 RU/s for this application's collection.</span></span>

## <span data-ttu-id="3e47f-302"><a id="RequestRateTooLarge"></a> Azure Cosmos DB에서 예약된 처리량 제한 초과</span><span class="sxs-lookup"><span data-stu-id="3e47f-302"><a id="RequestRateTooLarge"></a> Exceeding reserved throughput limits in Azure Cosmos DB</span></span>
<span data-ttu-id="3e47f-303">Hello 예산 비어 있으면 요청 단위 소비 초 당 속도로 계산 됨을 기억 하십시오.</span><span class="sxs-lookup"><span data-stu-id="3e47f-303">Recall that request unit consumption is evaluated as a rate per second if hello budget is empty.</span></span> <span data-ttu-id="3e47f-304">Hello를 초과 하는 응용 프로그램에 대 한 프로 비전 된 요청 단위는 컨테이너에 대 한 요청 수 hello 속도 hello 예약 된 수준 아래로 떨어질 때까지 toothat 컬렉션 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-304">For applications that exceed hello provisioned request unit rate for a container, requests toothat collection will be throttled until hello rate drops below hello reserved level.</span></span> <span data-ttu-id="3e47f-305">(HTTP 상태 코드 429) RequestRateTooLargeException hello 요청 하 고 반환 hello x-ms-다시 시도-후-ms을 나타내는 헤더 hello 양의 시간 (밀리초), 사용자 hello 하기 전에 대기 해야 hello 서버 스로틀 되는 경우 종료 미리 됩니다. hello 요청을 다시 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-305">When a throttle occurs, hello server will preemptively end hello request with RequestRateTooLargeException (HTTP status code 429) and return hello x-ms-retry-after-ms header indicating hello amount of time, in milliseconds, that hello user must wait before reattempting hello request.</span></span>

    HTTP Status 429
    Status Line: RequestRateTooLarge
    x-ms-retry-after-ms :100

<span data-ttu-id="3e47f-306">측면 hello 서버에 지정 된 retry-after 헤더 hello.NET 클라이언트 SDK 및 LINQ 쿼리에 다음 하지 않아도이 예외와 toodeal hello 현재 버전의.NET 클라이언트 SDK hello이이 응답을 암시적으로 catch 하는 대로 hello 시간의 대부분을 사용 하는 경우 및 hello 요청을 다시 시도 횟수입니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-306">If you are using hello .NET Client SDK and LINQ queries, then most of hello time you never have toodeal with this exception, as hello current version of hello .NET Client SDK implicitly catches this response, respects hello server-specified retry-after header, and retries hello request.</span></span> <span data-ttu-id="3e47f-307">계정 여러 클라이언트에서 동시에 액세스 하는, 하지 않는 한 hello 다음 재시도 성공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-307">Unless your account is being accessed concurrently by multiple clients, hello next retry will succeed.</span></span>

<span data-ttu-id="3e47f-308">누적 클라이언트가 여러 개 있는 경우 hello 기본 다시 시도 동작이 수 요구 사항을 충족 하지, 및 hello 클라이언트에서는 상태 코드 429 toohello 응용 프로그램과 함께 DocumentClientException throw hello 요청 속도 이상으로 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-308">If you have more than one client cumulatively operating above hello request rate, hello default retry behavior may not suffice, and hello client will throw a DocumentClientException with status code 429 toohello application.</span></span> <span data-ttu-id="3e47f-309">이와 같은 경우에 다시 시도 동작이 및 응용 프로그램의 오류 처리 루틴 또는 hello hello 컨테이너에 대 한 예약 된 처리량을 증가에서 논리를 처리를 고려할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-309">In cases such as this, you may consider handling retry behavior and logic in your application's error handling routines or increasing hello reserved throughput for hello container.</span></span>

## <span data-ttu-id="3e47f-310"><a id="RequestRateTooLargeAPIforMongoDB"></a> MongoDB API에서 예약된 처리량 제한 초과</span><span class="sxs-lookup"><span data-stu-id="3e47f-310"><a id="RequestRateTooLargeAPIforMongoDB"></a> Exceeding reserved throughput limits in API for MongoDB</span></span>
<span data-ttu-id="3e47f-311">Hello 속도 hello 예약 된 수준 아래로 떨어질 때까지 컬렉션에 대 한 사용자를 프로 비전 하는 hello 요청 단위를 초과 하는 응용 프로그램 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-311">Applications that exceed hello provisioned request units for a collection will be throttled until hello rate drops below hello reserved level.</span></span> <span data-ttu-id="3e47f-312">사용 하 여 hello 요청 스로틀 발생할 때 hello 백 엔드 끝납니다 여기서는 *16500* 오류 코드- *너무 많은 요청*합니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-312">When a throttle occurs, hello backend will preemptively end hello request with a *16500* error code - *Too Many Requests*.</span></span> <span data-ttu-id="3e47f-313">기본적으로 API MongoDB에 대 한 자동으로 다시 too10 시간을 반환 하기 전에 *너무 많은 요청* 오류 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-313">By default, API for MongoDB will automatically retry up too10 times before returning a *Too Many Requests* error code.</span></span> <span data-ttu-id="3e47f-314">많은 발생 하는 경우 *너무 많은 요청* 오류 코드를 응용 프로그램의 오류 처리 루틴에에서 추가 하거나 다시 시도 동작을 고려할 수 있습니다 또는 [hellohello컬렉션에대한예약된처리량을증가](set-throughput.md).</span><span class="sxs-lookup"><span data-stu-id="3e47f-314">If you are receiving many *Too Many Requests* error codes, you may consider either adding retry behavior in your application's error handling routines or [increasing hello reserved throughput for hello collection](set-throughput.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3e47f-315">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3e47f-315">Next steps</span></span>
<span data-ttu-id="3e47f-316">toolearn Azure Cosmos DB 데이터베이스와 예약 된 처리량에 대 한 자세한이 리소스를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-316">toolearn more about reserved throughput with Azure Cosmos DB databases, explore these resources:</span></span>

* <span data-ttu-id="3e47f-317">[Azure Cosmos DB 가격 책정](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="3e47f-317">[Azure Cosmos DB pricing](https://azure.microsoft.com/pricing/details/cosmos-db/)</span></span>
* [<span data-ttu-id="3e47f-318">Azure Cosmos DB에서 데이터 분할</span><span class="sxs-lookup"><span data-stu-id="3e47f-318">Partitioning data in Azure Cosmos DB</span></span>](partition-data.md)

<span data-ttu-id="3e47f-319">Azure Cosmos DB에 대해 자세히 toolearn hello Azure Cosmos DB 참조 [설명서](https://azure.microsoft.com/documentation/services/cosmos-db/)합니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-319">toolearn more about Azure Cosmos DB, see hello Azure Cosmos DB [documentation](https://azure.microsoft.com/documentation/services/cosmos-db/).</span></span> 

<span data-ttu-id="3e47f-320">확장 및 성능 Azure Cosmos DB를 사용 하 여 테스트 시작 tooget 참조 [성능 및 배율 Azure Cosmos DB를 사용 하 여 테스트](performance-testing.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3e47f-320">tooget started with scale and performance testing with Azure Cosmos DB, see [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md).</span></span>

[1]: ./media/request-units/queryexplorer.png 
[2]: ./media/request-units/RUEstimatorUpload.png
[3]: ./media/request-units/RUEstimatorDocuments.png
[4]: ./media/request-units/RUEstimatorResults.png
[5]: ./media/request-units/RUCalculator2.png
[6]: ./media/request-units/api-for-mongodb-metrics.png

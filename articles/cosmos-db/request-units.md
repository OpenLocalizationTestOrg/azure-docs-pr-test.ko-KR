---
title: "요청 단위 및 예상 처리량 - Azure Cosmos DB | Microsoft Docs"
description: "Azure Cosmos DB의 요청 단위 요구 사항을 이해, 지정 및 예측하는 방법을 알아봅니다."
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
ms.openlocfilehash: 7a4efc0fb9b3855b9dbbe445768ceb2a9940d0b2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="request-units-in-azure-cosmos-db"></a><span data-ttu-id="a0b6e-103">Azure Cosmos DB의 요청 단위</span><span class="sxs-lookup"><span data-stu-id="a0b6e-103">Request Units in Azure Cosmos DB</span></span>
<span data-ttu-id="a0b6e-104">지금 사용 가능: Azure Cosmos DB [요청 단위 계산기](https://www.documentdb.com/capacityplanner).</span><span class="sxs-lookup"><span data-stu-id="a0b6e-104">Now available: Azure Cosmos DB [request unit calculator](https://www.documentdb.com/capacityplanner).</span></span> <span data-ttu-id="a0b6e-105">자세한 내용을 보려면 [처리량 요구 예측](request-units.md#estimating-throughput-needs)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-105">Learn more in [Estimating your throughput needs](request-units.md#estimating-throughput-needs).</span></span>

![처리량 계산기][5]

## <a name="introduction"></a><span data-ttu-id="a0b6e-107">소개</span><span class="sxs-lookup"><span data-stu-id="a0b6e-107">Introduction</span></span>
<span data-ttu-id="a0b6e-108">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/)는 전 세계에 배포된 Microsoft의 다중 모델 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-108">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) is Microsoft's globally distributed multi-model database.</span></span> <span data-ttu-id="a0b6e-109">Azure Cosmos DB를 사용하면 가상 컴퓨터를 임대하거나, 소프트웨어를 배포하거나, 데이터베이스를 모니터링할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-109">With Azure Cosmos DB, you don't have to rent virtual machines, deploy software, or monitor databases.</span></span> <span data-ttu-id="a0b6e-110">세계적 수준의 가용성, 성능 및 데이터 보호를 제공하기 위해 Microsoft의 최고 엔지니어가 Azure Cosmos DB를 작동하고 지속적으로 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-110">Azure Cosmos DB is operated and continuously monitored by Microsoft top engineers to deliver world class availability, performance, and data protection.</span></span> <span data-ttu-id="a0b6e-111">[DocumentDB SQL](documentdb-sql-query.md)(문서), MongoDB(문서), [Azure Table Storage](https://azure.microsoft.com/services/storage/tables/)(키-값) 및 [Gremlin](https://tinkerpop.apache.org/gremlin.html)(그래프)가 모두 기본적으로 지원되므로 원하는 API를 사용하여 데이터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-111">You can access your data using APIs of your choice, as [DocumentDB SQL](documentdb-sql-query.md) (document), MongoDB (document), [Azure Table Storage](https://azure.microsoft.com/services/storage/tables/) (key-value), and [Gremlin](https://tinkerpop.apache.org/gremlin.html) (graph) are all natively supported.</span></span> <span data-ttu-id="a0b6e-112">Azure Cosmos DB의 통화는 RU(요청 단위)입니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-112">The currency of Azure Cosmos DB is the Request Unit (RU).</span></span> <span data-ttu-id="a0b6e-113">RU를 사용하면 읽기/쓰기 용량을 예약하거나 CPU, 메모리 및 IOPS를 프로비전할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-113">With RUs, you do not need to reserve read/write capacities or provision CPU, Memory and IOPS.</span></span>

<span data-ttu-id="a0b6e-114">Azure Cosmos DB는 단순한 읽기 및 쓰기부터 복잡한 그래프 쿼리에 이르기까지 다양한 작업에서 많은 API를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-114">Azure Cosmos DB supports a number of APIs with different operations ranging from simple reads and writes to complex graph queries.</span></span> <span data-ttu-id="a0b6e-115">모든 요청 값이 같지 않으므로 요청을 처리하는 데 필요한 계산의 양에 기반하여 정규화된 양의 **요청 단위**가 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-115">Since not all requests are equal, they are assigned a normalized quantity of **request units** based on the amount of computation required to serve the request.</span></span> <span data-ttu-id="a0b6e-116">작업에 대한 요청 단위 수는 결정적이며 응답 헤더를 통해 Azure Cosmos DB의 모든 작업에 사용된 요청 단위 수를 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-116">The number of request units for an operation is deterministic, and you can track the number of request units consumed by any operation in Azure Cosmos DB via a response header.</span></span> 

<span data-ttu-id="a0b6e-117">예측 가능한 성능을 제공하려면 100 RU/초 단위로 처리량을 예약해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-117">To provide predictable performance, you need to reserve throughput in units of 100 RU/second.</span></span> 

<span data-ttu-id="a0b6e-118">이 문서를 읽은 다음에는 다음과 같은 질문에 답할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-118">After reading this article, you'll be able to answer the following questions:</span></span>  

* <span data-ttu-id="a0b6e-119">요청 단위 및 요청 요금이 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="a0b6e-119">What are request units and request charges?</span></span>
* <span data-ttu-id="a0b6e-120">컬렉션에 대해 요청 단위 용량을 지정하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="a0b6e-120">How do I specify request unit capacity for a collection?</span></span>
* <span data-ttu-id="a0b6e-121">내 응용 프로그램에 필요한 요청 단위를 어떻게 추정할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="a0b6e-121">How do I estimate my application's request unit needs?</span></span>
* <span data-ttu-id="a0b6e-122">컬렉션의 요청 단위 용량을 초과하면 어떻게 되나요?</span><span class="sxs-lookup"><span data-stu-id="a0b6e-122">What happens if I exceed request unit capacity for a collection?</span></span>

<span data-ttu-id="a0b6e-123">Azure Cosmos DB는 다중 모델 데이터베이스이므로 문서 API에는 컬렉션/문서를, Graph API에는 그래프/노드를, 테이블 API에는 테이블/엔터티를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-123">As Azure Cosmos DB is a multi-model database, it is important to note that we will refer to a collection/document for a document API, a graph/node for a graph API and a table/entity for table API.</span></span> <span data-ttu-id="a0b6e-124">이 문서 전체에서 컨테이너/항목의 개념을 일반화합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-124">Throughput this document we will generalize to the concepts of container/item.</span></span>

## <a name="request-units-and-request-charges"></a><span data-ttu-id="a0b6e-125">요청 단위 및 요청 요금</span><span class="sxs-lookup"><span data-stu-id="a0b6e-125">Request units and request charges</span></span>
<span data-ttu-id="a0b6e-126">Azure Cosmos DB는 응용 프로그램의 처리량 수요를 충족하도록 리소스를 *예약*하여 신속하고 예측 가능한 성능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-126">Azure Cosmos DB delivers fast, predictable performance by *reserving* resources to satisfy your application's throughput needs.</span></span>  <span data-ttu-id="a0b6e-127">시간이 지나면 응용 프로그램 로드 및 액세스 패턴이 변하는데, Azure Cosmos DB를 사용하면 응용 프로그램에 제공되는 예약된 처리량을 간편하게 늘리거나 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-127">Because application load and access patterns change over time, Azure Cosmos DB allows you to easily increase or decrease the amount of reserved throughput available to your application.</span></span>

<span data-ttu-id="a0b6e-128">Azure Cosmos DB에서는 예약된 처리량이 초당 처리되는 요청 단위로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-128">With Azure Cosmos DB, reserved throughput is specified in terms of request units processing per second.</span></span> <span data-ttu-id="a0b6e-129">요청 단위란 응용 프로그램에 보장되는 초당 요청 단위의 양을 *예약* 할 수 있는 처리량 통화라고 생각하시면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-129">You can think of request units as throughput currency, whereby you *reserve* an amount of guaranteed request units available to your application on per second basis.</span></span>  <span data-ttu-id="a0b6e-130">문서 작성, 쿼리 수행, 문서 업데이트 등 Azure Cosmos DB의 각 작업에서는 CPU, 메모리 및 IOPS를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-130">Each operation in Azure Cosmos DB - writing a document, performing a query, updating a document - consumes CPU, memory, and IOPS.</span></span>  <span data-ttu-id="a0b6e-131">즉, 각 작업이 *요청 요금*을 발생시키고, 요청 요금은 *요청 단위*로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-131">That is, each operation incurs a *request charge*, which is expressed in *request units*.</span></span>  <span data-ttu-id="a0b6e-132">응용 프로그램의 처리량 요구 사항과 함께 요청 단위 요금에 영향을 주는 요소를 이해하면 응용 프로그램을 최대한 경제적으로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-132">Understanding the factors which impact request unit charges, along with your application's throughput requirements, enables you to run your application as cost effectively as possible.</span></span> <span data-ttu-id="a0b6e-133">쿼리 탐색기는 쿼리의 핵심을 테스트하는 데 유용한 도구이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-133">The query explorer is also a wonderful tool to test the core of a query.</span></span>

<span data-ttu-id="a0b6e-134">먼저 Aravind Ramachandran이 Azure Cosmos DB의 요청 단위 및 예측 가능한 성능을 설명하는 다음 동영상을 보는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-134">We recommend getting started by watching the following video, where Aravind Ramachandran explains request units and predictable performance with Azure Cosmos DB.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Predictable-Performance-with-DocumentDB/player]
> 
> 

## <a name="specifying-request-unit-capacity-in-azure-cosmos-db"></a><span data-ttu-id="a0b6e-135">Azure Cosmos DB에서 요청 단위 용량 지정</span><span class="sxs-lookup"><span data-stu-id="a0b6e-135">Specifying request unit capacity in Azure Cosmos DB</span></span>
<span data-ttu-id="a0b6e-136">새 컬렉션, 테이블 또는 그래프를 시작할 때 예약하려는 초당 요청 단위 수(초당 RU)를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-136">When starting a new collection, table or graph, you specify the number of request units per second (RU per second) you want reserved.</span></span> <span data-ttu-id="a0b6e-137">프로비전된 처리량에 따라 Azure Cosmos DB는 컬렉션을 호스트하는 실제 파티션을 할당하고 확장됨에 따라 파티션에서 데이터를 분할/균형 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-137">Based on the provisioned throughput, Azure Cosmos DB allocates physical partitions to host your collection and splits/rebalances data across partitions as it grows.</span></span>

<span data-ttu-id="a0b6e-138">Azure Cosmos DB에서는 컬렉션이 2,500개 이상의 요청 단위로 프로비전된 경우 파티션 키를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-138">Azure Cosmos DB requires a partition key to be specified when a collection is provisioned with 2,500 request units or higher.</span></span> <span data-ttu-id="a0b6e-139">나중에 2,500개 이상의 요청 단위로 컬렉션 처리량의 크기를 조정하려는 경우에도 파티션 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-139">A partition key is also required to scale your collection's throughput beyond 2,500 request units in the future.</span></span> <span data-ttu-id="a0b6e-140">따라서 초기 처리량에 관계없이 컨테이너를 만들 때 [파티션 키](partition-data.md)를 구성하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-140">Therefore, it is highly recommended to configure a [partition key](partition-data.md) when creating a container regardless of your initial throughput.</span></span> <span data-ttu-id="a0b6e-141">데이터는 여러 파티션에 분할되어야 하므로 컬렉션/테이블/그래프 및 요청이 Azure Cosmos DB에서 균일하게 확장될 수 있도록 카디널리티가 높은(수백~수백만 개의 고유 값) 파티션 키를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-141">Since your data might have to be split across multiple partitions, it is necessary to pick a partition key that has a high cardinality (100 to millions of distinct values) so that your collection/table/graph and requests can be scaled uniformly by Azure Cosmos DB.</span></span> 

> [!NOTE]
> <span data-ttu-id="a0b6e-142">파티션 키는 논리적 경계이며 실제 경계가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-142">A partition key is a logical boundary, and not a physical one.</span></span> <span data-ttu-id="a0b6e-143">따라서 특정 파티션 키 값의 수를 제한할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-143">Therefore, you do not need to limit the number of distinct partition key values.</span></span> <span data-ttu-id="a0b6e-144">사실 Azure Cosmos DB에 더 많은 부하 분산 옵션이 있으므로 고유 파티션 키 값이 적은 것보다 많은 것이 더 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-144">It is in fact better to have more distinct partition key values than less, as Azure Cosmos DB has more load balancing options.</span></span>

<span data-ttu-id="a0b6e-145">.NET SDK를 사용하여 초당 3,000 요청 단위로 컬렉션을 만들기 위한 코드 조각은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-145">Here is a code snippet for creating a collection with 3,000 request units per second using the .NET SDK:</span></span>

```csharp
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 3000 });
```

<span data-ttu-id="a0b6e-146">Azure Cosmos DB는 처리량의 예약 모델에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-146">Azure Cosmos DB operates on a reservation model on throughput.</span></span> <span data-ttu-id="a0b6e-147">즉, 활발하게 *사용된* 처리량에 관계없이 *예약된* 처리량에 따라 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-147">That is, you are billed for the amount of throughput *reserved*, regardless of how much of that throughput is actively *used*.</span></span> <span data-ttu-id="a0b6e-148">응용 프로그램의 부하, 데이터 및 사용 패턴이 변하면 그에 따라 SDK를 통해 또는 [Azure Portal](https://portal.azure.com)을 사용하여 예약된 RU 양을 간단하게 늘리거나 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-148">As your application's load, data, and usage patterns change you can easily scale up and down the amount of reserved RUs through SDKs or using the [Azure Portal](https://portal.azure.com).</span></span>

<span data-ttu-id="a0b6e-149">각 컬렉션/테이블/그래프는 프로비전된 처리량에 대한 메타데이터가 있는 Azure Cosmos DB의 `Offer` 리소스에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-149">Each collection/table/graph are mapped to an `Offer` resource in Azure Cosmos DB, which has metadata about the provisioned throughput.</span></span> <span data-ttu-id="a0b6e-150">컨테이너에 해당하는 제품 리소스를 조회한 다음 새 처리량 값으로 업데이트하여 할당된 처리량을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-150">You can change the allocated throughput by looking up the corresponding offer resource for a container, then updating it with the new throughput value.</span></span> <span data-ttu-id="a0b6e-151">다음 코드 조각에서는 .NET SDK를 사용하여 컬렉션 처리량을 5,000RU/s로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-151">Here is a code snippet for changing the throughput of a collection to 5,000 request units per second using the .NET SDK:</span></span>

```csharp
// Fetch the resource to be updated
Offer offer = client.CreateOfferQuery()
                .Where(r => r.ResourceLink == collection.SelfLink)    
                .AsEnumerable()
                .SingleOrDefault();

// Set the throughput to 5000 request units per second
offer = new OfferV2(offer, 5000);

// Now persist these changes to the database by replacing the original resource
await client.ReplaceOfferAsync(offer);
```

<span data-ttu-id="a0b6e-152">처리량을 변경할 때 컨테이너의 가용성에는 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-152">There is no impact to the availability of your container when you change the throughput.</span></span> <span data-ttu-id="a0b6e-153">일반적으로 새로 예약된 처리량은 새 처리량의 응용 프로그램에서 몇 초 이내에 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-153">Typically the new reserved throughput is effective within seconds on application of the new throughput.</span></span>

## <a name="request-unit-considerations"></a><span data-ttu-id="a0b6e-154">요청 단위 고려 사항</span><span class="sxs-lookup"><span data-stu-id="a0b6e-154">Request unit considerations</span></span>
<span data-ttu-id="a0b6e-155">Azure Cosmos DB 컨테이너에 대해 예약할 요청 단위 수를 추정하는 경우 다음 변수를 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-155">When estimating the number of request units to reserve for your Azure Cosmos DB container, it is important to take the following variables into consideration:</span></span>

* <span data-ttu-id="a0b6e-156">**항목 크기**.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-156">**Item size**.</span></span> <span data-ttu-id="a0b6e-157">크기가 증가할수록 데이터를 읽거나 쓰는 데 사용되는 단위도 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-157">As size increases the units consumed to read or write the data will also increase.</span></span>
* <span data-ttu-id="a0b6e-158">**항목 속성 개수**.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-158">**Item property count**.</span></span> <span data-ttu-id="a0b6e-159">모든 속성의 기본 인덱싱을 가정할 경우 속성 수가 증가할수록 문서/노드/엔터티를 쓰는 데 사용되는 단위가 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-159">Assuming default indexing of all properties, the units consumed to write a document/node/ntity will increase as the property count increases.</span></span>
* <span data-ttu-id="a0b6e-160">**데이터 일관성**.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-160">**Data consistency**.</span></span> <span data-ttu-id="a0b6e-161">강력 또는 제한된 부실 데이터 일관성 수준을 사용하는 경우 항목을 읽는 데 추가 단위가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-161">When using data consistency levels of Strong or Bounded Staleness, additional units will be consumed to read items.</span></span>
* <span data-ttu-id="a0b6e-162">**인덱싱된 속성**.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-162">**Indexed properties**.</span></span> <span data-ttu-id="a0b6e-163">각 컨테이너의 인덱스 정책에 따라 기본적으로 인덱싱되는 속성이 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-163">An index policy on each container determines which properties are indexed by default.</span></span> <span data-ttu-id="a0b6e-164">인덱싱되는 속성 수를 제한하거나 지연 인덱싱을 사용하면 요청 단위 사용을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-164">You can reduce your request unit consumption by limiting the number of indexed properties or by enabling lazy indexing.</span></span>
* <span data-ttu-id="a0b6e-165">**문서 인덱싱**.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-165">**Document indexing**.</span></span> <span data-ttu-id="a0b6e-166">기본적으로 각 항목이 자동으로 인덱싱되며, 일부 항목을 인덱싱하지 않도록 선택하면 더 적은 요청 단위가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-166">By default each item is automatically indexed, you will consume fewer request units if you choose not to index some of your items.</span></span>
* <span data-ttu-id="a0b6e-167">**쿼리 패턴**.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-167">**Query patterns**.</span></span> <span data-ttu-id="a0b6e-168">쿼리의 복잡성은 작업에 사용되는 요청 단위의 양에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-168">The complexity of a query impacts how many Request Units are consumed for an operation.</span></span> <span data-ttu-id="a0b6e-169">조건자의 수, 조건자의 특성, 프로젝션, UDF 수 및 원본 데이터 집합의 크기는 모두 쿼리 작업의 비용에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-169">The number of predicates, nature of the predicates, projections, number of UDFs, and the size of the source data set all influence the cost of query operations.</span></span>
* <span data-ttu-id="a0b6e-170">**스크립트 사용량**.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-170">**Script usage**.</span></span>  <span data-ttu-id="a0b6e-171">쿼리와 마찬가지로, 저장된 프로시저 및 트리거는 수행하는 작업의 복잡성에 따라 요청 단위를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-171">As with queries, stored procedures and triggers consume request units based on the complexity of the operations being performed.</span></span> <span data-ttu-id="a0b6e-172">응용 프로그램을 개발하면서 요청 요금 헤더를 검사하면 각 작업이 요청 단위 용량을 어떻게 사용하는지 파악하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-172">As you develop your application, inspect the request charge header to better understand how each operation is consuming request unit capacity.</span></span>

## <a name="estimating-throughput-needs"></a><span data-ttu-id="a0b6e-173">필요한 처리량 예측</span><span class="sxs-lookup"><span data-stu-id="a0b6e-173">Estimating throughput needs</span></span>
<span data-ttu-id="a0b6e-174">요청 단위는 요청 처리 비용의 정규화된 측정값입니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-174">A request unit is a normalized measure of request processing cost.</span></span> <span data-ttu-id="a0b6e-175">단일 요청 단위는 10개의 고유한 속성 값(시스템 속성 제외)으로 구성된 1KB 항목 하나를 읽는 데(self 링크 또는 ID를 통해) 필요한 처리 용량을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-175">A single request unit represents the processing capacity required to read (via self link or id) a single 1KB item consisting of 10 unique property values (excluding system properties).</span></span> <span data-ttu-id="a0b6e-176">동일한 항목을 생성(삽입), 대체 또는 삭제하는 요청은 서비스에서 추가 처리를 사용하므로 더 많은 요청 단위가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-176">A request to create (insert), replace or delete the same item will consume more processing from the service and thereby more request units.</span></span>   

> [!NOTE]
> <span data-ttu-id="a0b6e-177">1KB 항목에 대한 요청 단위 1개의 기준은 항목의 self 링크 또는 ID에 의한 간단한 GET에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-177">The baseline of 1 request unit for a 1KB item corresponds to a simple GET by self link or id of the item.</span></span>
> 
> 

<span data-ttu-id="a0b6e-178">예를 들어 다음 표에는 세 가지 항목 크기(1KB, 4KB 및 64KB)와 두 가지 다른 성능(500읽기/초 + 100쓰기/초 및 500읽기/초 +500 쓰기/초)에서 프로비전할 요청 단위가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-178">For example, here's a table that shows how many request units to provision at three different item sizes (1KB, 4KB, and 64KB) and at two different performance levels (500 reads/second + 100 writes/second and 500 reads/second + 500 writes/second).</span></span> <span data-ttu-id="a0b6e-179">데이터 일관성은 세션에서 구성되었으며 인덱싱 정책은 None으로 설정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-179">The data consistency was configured at Session, and the indexing policy was set to None.</span></span>

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><span data-ttu-id="a0b6e-180"><strong>항목 크기</strong></span><span class="sxs-lookup"><span data-stu-id="a0b6e-180"><strong>Item size</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="a0b6e-181"><strong>읽기/초</strong></span><span class="sxs-lookup"><span data-stu-id="a0b6e-181"><strong>Reads/second</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="a0b6e-182"><strong>쓰기/초</strong></span><span class="sxs-lookup"><span data-stu-id="a0b6e-182"><strong>Writes/second</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="a0b6e-183"><strong>요청 단위</strong></span><span class="sxs-lookup"><span data-stu-id="a0b6e-183"><strong>Request units</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="a0b6e-184">1KB</span><span class="sxs-lookup"><span data-stu-id="a0b6e-184">1 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="a0b6e-185">500</span><span class="sxs-lookup"><span data-stu-id="a0b6e-185">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="a0b6e-186">100</span><span class="sxs-lookup"><span data-stu-id="a0b6e-186">100</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="a0b6e-187">(500 * 1) + (100 * 5) = 1,000RU/s</span><span class="sxs-lookup"><span data-stu-id="a0b6e-187">(500 * 1) + (100 * 5) = 1,000 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="a0b6e-188">1KB</span><span class="sxs-lookup"><span data-stu-id="a0b6e-188">1 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="a0b6e-189">500</span><span class="sxs-lookup"><span data-stu-id="a0b6e-189">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="a0b6e-190">500</span><span class="sxs-lookup"><span data-stu-id="a0b6e-190">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="a0b6e-191">(500 * 1) + (500 * 5) = 3,000RU/s</span><span class="sxs-lookup"><span data-stu-id="a0b6e-191">(500 * 1) + (500 * 5) = 3,000 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="a0b6e-192">4KB</span><span class="sxs-lookup"><span data-stu-id="a0b6e-192">4 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="a0b6e-193">500</span><span class="sxs-lookup"><span data-stu-id="a0b6e-193">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="a0b6e-194">100</span><span class="sxs-lookup"><span data-stu-id="a0b6e-194">100</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="a0b6e-195">(500 * 1.3) + (100 * 7) = 1,350RU/s</span><span class="sxs-lookup"><span data-stu-id="a0b6e-195">(500 * 1.3) + (100 * 7) = 1,350 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="a0b6e-196">4KB</span><span class="sxs-lookup"><span data-stu-id="a0b6e-196">4 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="a0b6e-197">500</span><span class="sxs-lookup"><span data-stu-id="a0b6e-197">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="a0b6e-198">500</span><span class="sxs-lookup"><span data-stu-id="a0b6e-198">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="a0b6e-199">(500 * 1.3) + (500 * 7) = 4,150RU/s</span><span class="sxs-lookup"><span data-stu-id="a0b6e-199">(500 * 1.3) + (500 * 7) = 4,150 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="a0b6e-200">64KB</span><span class="sxs-lookup"><span data-stu-id="a0b6e-200">64 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="a0b6e-201">500</span><span class="sxs-lookup"><span data-stu-id="a0b6e-201">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="a0b6e-202">100</span><span class="sxs-lookup"><span data-stu-id="a0b6e-202">100</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="a0b6e-203">(500 * 10) + (100 * 48) = 9,800RU/s</span><span class="sxs-lookup"><span data-stu-id="a0b6e-203">(500 * 10) + (100 * 48) = 9,800 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="a0b6e-204">64KB</span><span class="sxs-lookup"><span data-stu-id="a0b6e-204">64 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="a0b6e-205">500</span><span class="sxs-lookup"><span data-stu-id="a0b6e-205">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="a0b6e-206">500</span><span class="sxs-lookup"><span data-stu-id="a0b6e-206">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="a0b6e-207">(500 * 10) + (500 * 48) = 29,000RU/s</span><span class="sxs-lookup"><span data-stu-id="a0b6e-207">(500 * 10) + (500 * 48) = 29,000 RU/s</span></span></p></td>
        </tr>
    </tbody>
</table>

### <a name="use-the-request-unit-calculator"></a><span data-ttu-id="a0b6e-208">요청 단위 계산기를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-208">Use the request unit calculator</span></span>
<span data-ttu-id="a0b6e-209">고객이 해당 처리량 예측을 미세 조정하도록 도우려면 다음을 포함한 일반적인 작업에 대한 요청 단위 요구 사항을 예측하는 웹 기반 [요청 단위 계산기](https://www.documentdb.com/capacityplanner) 를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-209">To help customers fine tune their throughput estimations, there is a web based [request unit calculator](https://www.documentdb.com/capacityplanner) to help estimate the request unit requirements for typical operations, including:</span></span>

* <span data-ttu-id="a0b6e-210">항목 만들기(쓰기)</span><span class="sxs-lookup"><span data-stu-id="a0b6e-210">Item creates (writes)</span></span>
* <span data-ttu-id="a0b6e-211">항목 읽기</span><span class="sxs-lookup"><span data-stu-id="a0b6e-211">Item reads</span></span>
* <span data-ttu-id="a0b6e-212">항목 삭제</span><span class="sxs-lookup"><span data-stu-id="a0b6e-212">Item deletes</span></span>
* <span data-ttu-id="a0b6e-213">항목 업데이트</span><span class="sxs-lookup"><span data-stu-id="a0b6e-213">Item updates</span></span>

<span data-ttu-id="a0b6e-214">이 도구에는 제공한 샘플 항목을 기반으로 하여 데이터 저장소 필요를 예측하는 지원이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-214">The tool also includes support for estimating data storage needs based on the sample items you provide.</span></span>

<span data-ttu-id="a0b6e-215">도구를 사용하는 것은 간단합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-215">Using the tool is simple:</span></span>

1. <span data-ttu-id="a0b6e-216">하나 이상의 대표 항목을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-216">Upload one or more representative items.</span></span>
   
    ![요청 단위 계산기에 항목 업로드][2]
2. <span data-ttu-id="a0b6e-218">데이터 저장소 요구 사항을 예측하려면 저장할 항목의 총수를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-218">To estimate data storage requirements, enter the total number of items you expect to store.</span></span>
3. <span data-ttu-id="a0b6e-219">항목 수를 입력하여 필요한 작업을 만들고 읽고 업데이트하고 삭제합니다(초 단위별로).</span><span class="sxs-lookup"><span data-stu-id="a0b6e-219">Enter the number of items create, read, update, and delete operations you require (on a per-second basis).</span></span> <span data-ttu-id="a0b6e-220">항목 업데이트 작업의 요청 단위 요금을 예측하려면 일반적인 필드 업데이트가 포함된 위의 1단계에서 샘플 항목의 복사본을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-220">To estimate the request unit charges of item update operations, upload a copy of the sample item from step 1 above that includes typical field updates.</span></span>  <span data-ttu-id="a0b6e-221">예를 들어 항목 업데이트가 일반적으로 lastLogin 및 userVisits라는 두 가지 속성을 수정하는 경우 샘플 항목을 복사하고 해당 두 가지 속성의 값을 업데이트한 다음 복사된 항목을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-221">For example, if item updates typically modify two properties named lastLogin and userVisits, then simply copy the sample item, update the values for those two properties, and upload the copied item.</span></span>
   
    ![요청 단위 계산기에 처리량 요구 입력][3]
4. <span data-ttu-id="a0b6e-223">결과를 계산하고 검토하도록 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-223">Click calculate and examine the results.</span></span>
   
    ![요청 단위 계산기 결과][4]

> [!NOTE]
> <span data-ttu-id="a0b6e-225">인덱싱된 속성과 크기 및 개수가 완전히 다른 항목 유형이 있는 경우 일반 항목의 각 *유형*을 도구에 업로드한 다음 결과를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-225">If you have item types which will differ dramatically in terms of size and the number of indexed properties, then upload a sample of each *type* of typical item to the tool and then calculate the results.</span></span>
> 
> 

### <a name="use-the-azure-cosmos-db-request-charge-response-header"></a><span data-ttu-id="a0b6e-226">Azure Cosmos DB 요청 요금 응답 헤더 사용</span><span class="sxs-lookup"><span data-stu-id="a0b6e-226">Use the Azure Cosmos DB request charge response header</span></span>
<span data-ttu-id="a0b6e-227">Azure Cosmos DB 서비스의 모든 응답에는 요청에 사용된 요청 단위가 포함된 사용자 지정 헤더(`x-ms-request-charge`)가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-227">Every response from the Azure Cosmos DB service includes a custom header (`x-ms-request-charge`) that contains the request units consumed for the request.</span></span> <span data-ttu-id="a0b6e-228">이 헤더는 Azure Cosmos DB SDK를 통해 액세스할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-228">This header is also accessible through the Azure Cosmos DB SDKs.</span></span> <span data-ttu-id="a0b6e-229">.NET SDK에서 RequestCharge는 ResourceResponse 개체의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-229">In the .NET SDK, RequestCharge is a property of the ResourceResponse object.</span></span>  <span data-ttu-id="a0b6e-230">쿼리의 경우 Azure Portal의 Azure Cosmos DB 쿼리 탐색기는 실행된 쿼리에 대한 요청 요금 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-230">For queries, the Azure Cosmos DB Query Explorer in the Azure portal provides request charge information for executed queries.</span></span>

![쿼리 탐색기에서 RU 요금을 검사하는 중][1]

<span data-ttu-id="a0b6e-232">이 점을 염두에 두고, 응용 프로그램에 필요한 예약된 처리량을 예측하는 한 가지 방법은 응용 프로그램에서 사용하는 대표적인 항목에 대해 실행되는 일반 작업과 연결된 요청 단위 요금을 기록한 다음, 예상되는 초당 수행되는 작업 수를 추정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-232">With this in mind, one method for estimating the amount of reserved throughput required by your application is to record the request unit charge associated with running typical operations against a representative item used by your application and then estimating the number of operations you anticipate performing each second.</span></span>  <span data-ttu-id="a0b6e-233">일반 쿼리 및 Azure Cosmos DB 스크립트 사용량도 측정하여 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-233">Be sure to measure and include typical queries and Azure Cosmos DB script usage as well.</span></span>

> [!NOTE]
> <span data-ttu-id="a0b6e-234">인덱싱된 속성과 크기 및 개수가 완전히 다른 항목 유형이 있는 경우에는 일반 항목의 각 *유형*과 연결된 적용 가능한 작업 요청 단위 요금을 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-234">If you have item types which will differ dramatically in terms of size and the number of indexed properties, then record the applicable operation request unit charge associated with each *type* of typical item.</span></span>
> 
> 

<span data-ttu-id="a0b6e-235">예:</span><span class="sxs-lookup"><span data-stu-id="a0b6e-235">For example:</span></span>

1. <span data-ttu-id="a0b6e-236">일반 항목을 만드는(삽입하는) 요청 단위 요금을 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-236">Record the request unit charge of creating (inserting) a typical item.</span></span> 
2. <span data-ttu-id="a0b6e-237">일반 항목을 읽는 요청 단위 요금을 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-237">Record the request unit charge of reading a typical item.</span></span>
3. <span data-ttu-id="a0b6e-238">일반 항목을 업데이트하는 요청 단위 요금을 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-238">Record the request unit charge of updating a typical item.</span></span>
4. <span data-ttu-id="a0b6e-239">일반적이고 공통적인 항목 쿼리의 요청 단위 요금을 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-239">Record the request unit charge of typical, common item queries.</span></span>
5. <span data-ttu-id="a0b6e-240">응용 프로그램에서 활용하는 모든 사용자 지정 스크립트(저장된 프로시저, 트리거, 사용자 정의 함수)의 요청 단위 요금을 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-240">Record the request unit charge of any custom scripts (stored procedures, triggers, user-defined functions) leveraged by the application</span></span>
6. <span data-ttu-id="a0b6e-241">예상되는 초당 작업 수를 고려하여 필요한 요청 단위를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-241">Calculate the required request units given the estimated number of operations you anticipate to run each second.</span></span>

### <span data-ttu-id="a0b6e-242"><a id="GetLastRequestStatistics"></a>MongoDB API의 GetLastRequestStatistics 명령 사용</span><span class="sxs-lookup"><span data-stu-id="a0b6e-242"><a id="GetLastRequestStatistics"></a>Use API for MongoDB's GetLastRequestStatistics command</span></span>
<span data-ttu-id="a0b6e-243">MongoDB API는 지정된 작업에 대한 요청 비용을 검색하는 데 사용자 지정 명령인 *getLastRequestStatistics*를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-243">API for MongoDB supports a custom command, *getLastRequestStatistics*, for retrieving the request charge for specified operations.</span></span>

<span data-ttu-id="a0b6e-244">예를 들어 Mongo Shell에서 요청 비용을 확인할 작업을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-244">For example, in the Mongo Shell, execute the operation you want to verify the request charge for.</span></span>
```
> db.sample.find()
```

<span data-ttu-id="a0b6e-245">다음으로 *getLastRequestStatistics* 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-245">Next, execute the command *getLastRequestStatistics*.</span></span>
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

<span data-ttu-id="a0b6e-246">이 점을 염두에 두고, 응용 프로그램에 필요한 예약된 처리량을 예측하는 한 가지 방법은 응용 프로그램에서 사용하는 대표적인 항목에 대해 실행되는 일반 작업과 연결된 요청 단위 요금을 기록한 다음, 예상되는 초당 수행되는 작업 수를 추정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-246">With this in mind, one method for estimating the amount of reserved throughput required by your application is to record the request unit charge associated with running typical operations against a representative item used by your application and then estimating the number of operations you anticipate performing each second.</span></span>

> [!NOTE]
> <span data-ttu-id="a0b6e-247">인덱싱된 속성과 크기 및 개수가 완전히 다른 항목 유형이 있는 경우에는 일반 항목의 각 *유형*과 연결된 적용 가능한 작업 요청 단위 요금을 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-247">If you have item types which will differ dramatically in terms of size and the number of indexed properties, then record the applicable operation request unit charge associated with each *type* of typical item.</span></span>
> 
> 

## <a name="use-api-for-mongodbs-portal-metrics"></a><span data-ttu-id="a0b6e-248">MongoDB API 포털 메트릭 사용</span><span class="sxs-lookup"><span data-stu-id="a0b6e-248">Use API for MongoDB's portal metrics</span></span>
<span data-ttu-id="a0b6e-249">MongoDB API 데이터베이스에 대한 요청 단위 요금을 적절히 추정하는 가장 간단한 방법은 [Azure Portal](https://portal.azure.com) 메트릭을 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-249">The simplest way to get a good estimation of request unit charges for your API for MongoDB database is to use the [Azure portal](https://portal.azure.com) metrics.</span></span> <span data-ttu-id="a0b6e-250">*요청 수* 및 *요청 요금* 차트에서 각 작업에서 사용하는 요청 단위 수와 서로 상대적으로 사용하는 요청 단위 수를 추정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-250">With the *Number of requests* and *Request Charge* charts, you can get an estimation of how many request units each operation is consuming and how many request units they consume relative to one another.</span></span>

![MongoDB API 포털 메트릭][6]

## <a name="a-request-unit-estimation-example"></a><span data-ttu-id="a0b6e-252">요청 단위 추정 예제</span><span class="sxs-lookup"><span data-stu-id="a0b6e-252">A request unit estimation example</span></span>
<span data-ttu-id="a0b6e-253">다음과 같은 ~1KB 문서를 가정하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-253">Consider the following ~1KB document:</span></span>

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
> <span data-ttu-id="a0b6e-254">문서가 Azure Cosmos DB에서 축소되기 때문에 위에서 시스템이 계산한 문서 크기는 1KB보다 약간 작습니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-254">Documents are minified in Azure Cosmos DB, so the system calculated size of the document above is slightly less than 1KB.</span></span>
> 
> 

<span data-ttu-id="a0b6e-255">다음 표에서는 이 항목의 일반 작업에 대한 대략적인 요청 단위 요금을 보여 줍니다(대략적인 요청 단위 요금은 계정 일관성 수준이 "세션"으로 설정되어 있고 모든 항목이 자동으로 인덱싱되는 것으로 가정).</span><span class="sxs-lookup"><span data-stu-id="a0b6e-255">The following table shows approximate request unit charges for typical operations on this item (the approximate request unit charge assumes that the account consistency level is set to “Session” and that all items are automatically indexed):</span></span>

| <span data-ttu-id="a0b6e-256">작업</span><span class="sxs-lookup"><span data-stu-id="a0b6e-256">Operation</span></span> | <span data-ttu-id="a0b6e-257">요청 단위 요금</span><span class="sxs-lookup"><span data-stu-id="a0b6e-257">Request Unit Charge</span></span> |
| --- | --- |
| <span data-ttu-id="a0b6e-258">항목 만들기</span><span class="sxs-lookup"><span data-stu-id="a0b6e-258">Create item</span></span> |<span data-ttu-id="a0b6e-259">~15 RU</span><span class="sxs-lookup"><span data-stu-id="a0b6e-259">~15 RU</span></span> |
| <span data-ttu-id="a0b6e-260">항목 읽기</span><span class="sxs-lookup"><span data-stu-id="a0b6e-260">Read item</span></span> |<span data-ttu-id="a0b6e-261">~1 RU</span><span class="sxs-lookup"><span data-stu-id="a0b6e-261">~1 RU</span></span> |
| <span data-ttu-id="a0b6e-262">ID로 항목 쿼리</span><span class="sxs-lookup"><span data-stu-id="a0b6e-262">Query item by id</span></span> |<span data-ttu-id="a0b6e-263">~2.5 RU</span><span class="sxs-lookup"><span data-stu-id="a0b6e-263">~2.5 RU</span></span> |

<span data-ttu-id="a0b6e-264">이 테이블은 응용 프로그램에 사용되는 일반 쿼리의 대략적인 요청 단위 요금도 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-264">Additionally, this table shows approximate request unit charges for typical queries used in the application:</span></span>

| <span data-ttu-id="a0b6e-265">쿼리</span><span class="sxs-lookup"><span data-stu-id="a0b6e-265">Query</span></span> | <span data-ttu-id="a0b6e-266">요청 단위 요금</span><span class="sxs-lookup"><span data-stu-id="a0b6e-266">Request Unit Charge</span></span> | <span data-ttu-id="a0b6e-267">반환된 항목 수</span><span class="sxs-lookup"><span data-stu-id="a0b6e-267"># of Returned Items</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a0b6e-268">ID로 음식 선택</span><span class="sxs-lookup"><span data-stu-id="a0b6e-268">Select food by id</span></span> |<span data-ttu-id="a0b6e-269">~2.5 RU</span><span class="sxs-lookup"><span data-stu-id="a0b6e-269">~2.5 RU</span></span> |<span data-ttu-id="a0b6e-270">1</span><span class="sxs-lookup"><span data-stu-id="a0b6e-270">1</span></span> |
| <span data-ttu-id="a0b6e-271">제조업체로 음식 선택</span><span class="sxs-lookup"><span data-stu-id="a0b6e-271">Select foods by manufacturer</span></span> |<span data-ttu-id="a0b6e-272">~7 RU</span><span class="sxs-lookup"><span data-stu-id="a0b6e-272">~7 RU</span></span> |<span data-ttu-id="a0b6e-273">7</span><span class="sxs-lookup"><span data-stu-id="a0b6e-273">7</span></span> |
| <span data-ttu-id="a0b6e-274">음식 그룹으로 선택하고 무게로 주문</span><span class="sxs-lookup"><span data-stu-id="a0b6e-274">Select by food group and order by weight</span></span> |<span data-ttu-id="a0b6e-275">~70 RU</span><span class="sxs-lookup"><span data-stu-id="a0b6e-275">~70 RU</span></span> |<span data-ttu-id="a0b6e-276">100</span><span class="sxs-lookup"><span data-stu-id="a0b6e-276">100</span></span> |
| <span data-ttu-id="a0b6e-277">음식 그룹의 상위 10개 음식 선택</span><span class="sxs-lookup"><span data-stu-id="a0b6e-277">Select top 10 foods in a food group</span></span> |<span data-ttu-id="a0b6e-278">~10 RU</span><span class="sxs-lookup"><span data-stu-id="a0b6e-278">~10 RU</span></span> |<span data-ttu-id="a0b6e-279">10</span><span class="sxs-lookup"><span data-stu-id="a0b6e-279">10</span></span> |

> [!NOTE]
> <span data-ttu-id="a0b6e-280">RU 요금은 반환되는 항목 수에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-280">RU charges vary based on the number of items returned.</span></span>
> 
> 

<span data-ttu-id="a0b6e-281">이 정보를 통해, 예상되는 초당 작업 및 쿼리 수에 따라 이 응용 프로그램에 필요한 RU를 예측할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-281">With this information, we can estimate the RU requirements for this application given the number of operations and queries we expect per second:</span></span>

| <span data-ttu-id="a0b6e-282">작업/쿼리</span><span class="sxs-lookup"><span data-stu-id="a0b6e-282">Operation/Query</span></span> | <span data-ttu-id="a0b6e-283">예상되는 초당 수</span><span class="sxs-lookup"><span data-stu-id="a0b6e-283">Estimated number per second</span></span> | <span data-ttu-id="a0b6e-284">필요한 RU</span><span class="sxs-lookup"><span data-stu-id="a0b6e-284">Required RUs</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a0b6e-285">항목 만들기</span><span class="sxs-lookup"><span data-stu-id="a0b6e-285">Create item</span></span> |<span data-ttu-id="a0b6e-286">10</span><span class="sxs-lookup"><span data-stu-id="a0b6e-286">10</span></span> |<span data-ttu-id="a0b6e-287">150</span><span class="sxs-lookup"><span data-stu-id="a0b6e-287">150</span></span> |
| <span data-ttu-id="a0b6e-288">항목 읽기</span><span class="sxs-lookup"><span data-stu-id="a0b6e-288">Read item</span></span> |<span data-ttu-id="a0b6e-289">100</span><span class="sxs-lookup"><span data-stu-id="a0b6e-289">100</span></span> |<span data-ttu-id="a0b6e-290">100</span><span class="sxs-lookup"><span data-stu-id="a0b6e-290">100</span></span> |
| <span data-ttu-id="a0b6e-291">제조업체로 음식 선택</span><span class="sxs-lookup"><span data-stu-id="a0b6e-291">Select foods by manufacturer</span></span> |<span data-ttu-id="a0b6e-292">25</span><span class="sxs-lookup"><span data-stu-id="a0b6e-292">25</span></span> |<span data-ttu-id="a0b6e-293">175</span><span class="sxs-lookup"><span data-stu-id="a0b6e-293">175</span></span> |
| <span data-ttu-id="a0b6e-294">음식 그룹으로 선택</span><span class="sxs-lookup"><span data-stu-id="a0b6e-294">Select by food group</span></span> |<span data-ttu-id="a0b6e-295">10</span><span class="sxs-lookup"><span data-stu-id="a0b6e-295">10</span></span> |<span data-ttu-id="a0b6e-296">700</span><span class="sxs-lookup"><span data-stu-id="a0b6e-296">700</span></span> |
| <span data-ttu-id="a0b6e-297">상위 10개 선택</span><span class="sxs-lookup"><span data-stu-id="a0b6e-297">Select top 10</span></span> |<span data-ttu-id="a0b6e-298">15</span><span class="sxs-lookup"><span data-stu-id="a0b6e-298">15</span></span> |<span data-ttu-id="a0b6e-299">총 150</span><span class="sxs-lookup"><span data-stu-id="a0b6e-299">150 Total</span></span> |

<span data-ttu-id="a0b6e-300">이 예에서는 필요한 평균 처리량이 1,275 RU/s로 예상됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-300">In this case, we expect an average throughput requirement of 1,275 RU/s.</span></span>  <span data-ttu-id="a0b6e-301">가장 가까운 100자리 숫자로 반올림하면 이 응용 프로그램의 컬렉션에 1,300 RU/s를 프로비전하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-301">Rounding up to the nearest 100, we would provision 1,300 RU/s for this application's collection.</span></span>

## <span data-ttu-id="a0b6e-302"><a id="RequestRateTooLarge"></a> Azure Cosmos DB에서 예약된 처리량 제한 초과</span><span class="sxs-lookup"><span data-stu-id="a0b6e-302"><a id="RequestRateTooLarge"></a> Exceeding reserved throughput limits in Azure Cosmos DB</span></span>
<span data-ttu-id="a0b6e-303">요청 단위 소비는 예산이 비어 있는 경우 초당 비율로 평가된다는 점을 기억하세요.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-303">Recall that request unit consumption is evaluated as a rate per second if the budget is empty.</span></span> <span data-ttu-id="a0b6e-304">컨테이너에서 프로비전된 요청 단위 속도를 초과하는 응용 프로그램의 경우 비율이 예약된 수준 이하로 떨어질 때까지 해당 컬렉션에 대한 요청이 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-304">For applications that exceed the provisioned request unit rate for a container, requests to that collection will be throttled until the rate drops below the reserved level.</span></span> <span data-ttu-id="a0b6e-305">제한이 발생하면 서버에서 RequestRateTooLargeException(HTTP 상태 코드 429)를 사용하여 선제적으로 요청을 종료하고, 사용자가 요청을 다시 시도할 수 있을 때까지 기다려야 하는 시간을 밀리초 단위로 표시하는 x-ms-retry-after-ms 헤더를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-305">When a throttle occurs, the server will preemptively end the request with RequestRateTooLargeException (HTTP status code 429) and return the x-ms-retry-after-ms header indicating the amount of time, in milliseconds, that the user must wait before reattempting the request.</span></span>

    HTTP Status 429
    Status Line: RequestRateTooLarge
    x-ms-retry-after-ms :100

<span data-ttu-id="a0b6e-306">.NET 클라이언트 SDK 및 LINQ 쿼리를 사용하는 경우에는 거의 대부분 이 예외를 처리할 필요가 없습니다. .NET 클라이언트 SDK 최신 버전이 이 응답을 암시적으로 catch하고, 서버에서 지정한 retry-after 헤더를 준수하고, 요청을 다시 시도하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-306">If you are using the .NET Client SDK and LINQ queries, then most of the time you never have to deal with this exception, as the current version of the .NET Client SDK implicitly catches this response, respects the server-specified retry-after header, and retries the request.</span></span> <span data-ttu-id="a0b6e-307">동시에 여러 클라이언트가 계정에 액세스하지만 않으면 다음 재시도가 성공할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-307">Unless your account is being accessed concurrently by multiple clients, the next retry will succeed.</span></span>

<span data-ttu-id="a0b6e-308">여러 클라이언트가 누적적으로 요청 속도를 초과하여 작동하는 경우에는 기본 재시도 동작으로 충분하지 않을 수 있으며, 클라이언트가 응용 프로그램에 상태 코드 429와 함께 DocumentClientException을 throw합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-308">If you have more than one client cumulatively operating above the request rate, the default retry behavior may not suffice, and the client will throw a DocumentClientException with status code 429 to the application.</span></span> <span data-ttu-id="a0b6e-309">이 경우 응용 프로그램의 오류 처리 루틴에서 재시도 동작 및 논리를 처리하는 방법 또는 컨테이너에 대해 예약된 처리량을 늘리는 방법을 고려해 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-309">In cases such as this, you may consider handling retry behavior and logic in your application's error handling routines or increasing the reserved throughput for the container.</span></span>

## <span data-ttu-id="a0b6e-310"><a id="RequestRateTooLargeAPIforMongoDB"></a> MongoDB API에서 예약된 처리량 제한 초과</span><span class="sxs-lookup"><span data-stu-id="a0b6e-310"><a id="RequestRateTooLargeAPIforMongoDB"></a> Exceeding reserved throughput limits in API for MongoDB</span></span>
<span data-ttu-id="a0b6e-311">컬렉션에서 프로비전된 요청 단위를 초과하는 응용 프로그램의 경우 비율이 예약된 수준 이하로 떨어질 때까지 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-311">Applications that exceed the provisioned request units for a collection will be throttled until the rate drops below the reserved level.</span></span> <span data-ttu-id="a0b6e-312">제한이 발생하면 백 엔드는 *16500* 오류 코드 - *너무 많은 요청*으로 요청을 먼저 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-312">When a throttle occurs, the backend will preemptively end the request with a *16500* error code - *Too Many Requests*.</span></span> <span data-ttu-id="a0b6e-313">기본적으로 MongoDB API는 *너무 많은 요청* 오류 코드를 반환되기까지 최대 10번 자동으로 재시도합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-313">By default, API for MongoDB will automatically retry up to 10 times before returning a *Too Many Requests* error code.</span></span> <span data-ttu-id="a0b6e-314">*너무 많은 요청* 오류 코드가 자주 발생하면 응용 프로그램의 오류 처리 루틴에서 재시도 동작을 추가하거나 [컬렉션에 대해 예약된 처리량을 늘리는 방법](set-throughput.md)을 고려해 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-314">If you are receiving many *Too Many Requests* error codes, you may consider either adding retry behavior in your application's error handling routines or [increasing the reserved throughput for the collection](set-throughput.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a0b6e-315">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a0b6e-315">Next steps</span></span>
<span data-ttu-id="a0b6e-316">Azure Cosmos DB 데이터베이스의 예약된 처리량에 대한 자세한 내용은 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-316">To learn more about reserved throughput with Azure Cosmos DB databases, explore these resources:</span></span>

* <span data-ttu-id="a0b6e-317">[Azure Cosmos DB 가격 책정](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="a0b6e-317">[Azure Cosmos DB pricing](https://azure.microsoft.com/pricing/details/cosmos-db/)</span></span>
* [<span data-ttu-id="a0b6e-318">Azure Cosmos DB에서 데이터 분할</span><span class="sxs-lookup"><span data-stu-id="a0b6e-318">Partitioning data in Azure Cosmos DB</span></span>](partition-data.md)

<span data-ttu-id="a0b6e-319">Azure Cosmos DB에 대한 자세한 내용은 Azure Cosmos DB [설명서](https://azure.microsoft.com/documentation/services/cosmos-db/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-319">To learn more about Azure Cosmos DB, see the Azure Cosmos DB [documentation](https://azure.microsoft.com/documentation/services/cosmos-db/).</span></span> 

<span data-ttu-id="a0b6e-320">Azure Cosmos DB를 사용하여 규모 및 성능 테스트를 시작하려면 [Azure Cosmos DB를 사용한 성능 및 규모 테스트](performance-testing.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-320">To get started with scale and performance testing with Azure Cosmos DB, see [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md).</span></span>

[1]: ./media/request-units/queryexplorer.png 
[2]: ./media/request-units/RUEstimatorUpload.png
[3]: ./media/request-units/RUEstimatorDocuments.png
[4]: ./media/request-units/RUEstimatorResults.png
[5]: ./media/request-units/RUCalculator2.png
[6]: ./media/request-units/api-for-mongodb-metrics.png

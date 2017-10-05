---
title: "Azure Cosmos DB의 분할 및 크기 조정 | Microsoft Docs"
description: "Azure Cosmos DB에서 분할 작동 방법, 분할 및 파티션 키를 구성하는 방법 및 응용 프로그램에 대한 올바른 파티션 키를 선택하는 방법을 알아봅니다."
services: cosmos-db
author: arramac
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 702c39b4-1798-48dd-9993-4493a2f6df9e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: arramac
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 81010d91ac7fe8fa7149c52ed56af304cf4e83d9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="partitioning-in-azure-cosmos-db-using-the-documentdb-api"></a><span data-ttu-id="d51ac-103">DocumentDB API를 사용하여 Azure Cosmos DB에서 분할</span><span class="sxs-lookup"><span data-stu-id="d51ac-103">Partitioning in Azure Cosmos DB using the DocumentDB API</span></span>

<span data-ttu-id="d51ac-104">[Microsoft Azure Cosmos DB](../cosmos-db/introduction.md)는 전역적으로 배포된 다중 모델 데이터베이스 서비스로써 신속하고 예측 가능한 성능을 얻을 수 있고, 응용 프로그램 증가에 따라 효율적인 확장이 가능하도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d51ac-104">[Microsoft Azure Cosmos DB](../cosmos-db/introduction.md) is a global distributed, multi-model database service designed to help you achieve fast, predictable performance and scale seamlessly along with your application as it grows.</span></span> 

<span data-ttu-id="d51ac-105">이 문서에서는 DocumentDB API를 사용하여 Cosmos DB 컨테이너의 분할 작업을 수행하는 방법에 대한 개요를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d51ac-105">This article provides an overview of how to work with partitioning of Cosmos DB containers with the DocumentDB API.</span></span> <span data-ttu-id="d51ac-106">Azure Cosmos DB API를 사용하여 분할하기 위한 개념 및 모범 사례의 개요는 [분할 및 수평적 크기 조정](../cosmos-db/partition-data.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d51ac-106">See [partitioning and horizontal scaling](../cosmos-db/partition-data.md) for an overview of concepts and best practices for partitioning with any Azure Cosmos DB API.</span></span> 

<span data-ttu-id="d51ac-107">코드를 시작하려면 [Github](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark)에서 프로젝트를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="d51ac-107">To get started with code, download the project from [Github](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span></span> 

<span data-ttu-id="d51ac-108">이 문서를 읽은 다음에는 다음과 같은 질문에 답할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d51ac-108">After reading this article, you will be able to answer the following questions:</span></span>   

* <span data-ttu-id="d51ac-109">Azure Cosmos DB에서 분할이 작동하는 방식</span><span class="sxs-lookup"><span data-stu-id="d51ac-109">How does partitioning work in Azure Cosmos DB?</span></span>
* <span data-ttu-id="d51ac-110">Azure Cosmos DB에서 분할을 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="d51ac-110">How do I configure partitioning in Azure Cosmos DB</span></span>
* <span data-ttu-id="d51ac-111">파티션 키의 정의 및 응용 프로그램에 올바른 파티션 키를 선택하는 방법</span><span class="sxs-lookup"><span data-stu-id="d51ac-111">What are partition keys, and how do I pick the right partition key for my application?</span></span>

<span data-ttu-id="d51ac-112">코드를 시작하려면 [Azure Cosmos DB 성능 테스트 드라이버 샘플](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark)에서 프로젝트를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="d51ac-112">To get started with code, download the project from [Azure Cosmos DB Performance Testing Driver Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span></span> 

<!-- placeholder until we have a permanent solution-->
<a name="partition-keys"></a>
<a name="single-partition-and-partitioned-collections"></a>
<a name="migrating-from-single-partition"></a>

## <a name="partition-keys"></a><span data-ttu-id="d51ac-113">파티션 키</span><span class="sxs-lookup"><span data-stu-id="d51ac-113">Partition keys</span></span>

<span data-ttu-id="d51ac-114">DocumentDB API에서 JSON 경로 형태로 파티션 키 정의를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d51ac-114">In the DocumentDB API, you specify the partition key definition in the form of a JSON path.</span></span> <span data-ttu-id="d51ac-115">다음 표에서는 파티션 키 정의 및 각 키에 해당하는 값의 예를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d51ac-115">The following table shows examples of partition key definitions and the values corresponding to each.</span></span> <span data-ttu-id="d51ac-116">파티션 키는 경로로 지정됩니다. 예를 들어 `/department`는 department 속성을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d51ac-116">The partition key is specified as a path, e.g. `/department` represents the property department.</span></span> 

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><span data-ttu-id="d51ac-117"><strong>파티션 키</strong></span><span class="sxs-lookup"><span data-stu-id="d51ac-117"><strong>Partition Key</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="d51ac-118"><strong>설명</strong></span><span class="sxs-lookup"><span data-stu-id="d51ac-118"><strong>Description</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="d51ac-119">/department</span><span class="sxs-lookup"><span data-stu-id="d51ac-119">/department</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="d51ac-120">doc가 항목인 doc.department의 값에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="d51ac-120">Corresponds to the value of doc.department where doc is the item.</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="d51ac-121">/properties/name</span><span class="sxs-lookup"><span data-stu-id="d51ac-121">/properties/name</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="d51ac-122">doc가 항목인 doc.properties.name의 값에 해당합니다(중첩된 속성).</span><span class="sxs-lookup"><span data-stu-id="d51ac-122">Corresponds to the value of doc.properties.name where doc is the item (nested property).</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="d51ac-123">/id</span><span class="sxs-lookup"><span data-stu-id="d51ac-123">/id</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="d51ac-124">doc.id의 값에 해당합니다(ID 및 파티션 키는 동일한 속성임).</span><span class="sxs-lookup"><span data-stu-id="d51ac-124">Corresponds to the value of doc.id (id and partition key are the same property).</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="d51ac-125">/"department name"</span><span class="sxs-lookup"><span data-stu-id="d51ac-125">/"department name"</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="d51ac-126">doc가 항목인 doc["department name"]의 값에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="d51ac-126">Corresponds to the value of doc["department name"] where doc is the item.</span></span></p></td>
        </tr>
    </tbody>
</table>

> [!NOTE]
> <span data-ttu-id="d51ac-127">파티션 키 구문은 인덱싱 정책 경로에 대한 경로 지정과 유사하지만, 경로가 값 대신 속성에 해당한다는 주요 차이점이 있습니다. 즉, 끝에 와일드카드가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d51ac-127">The syntax for partition key is similar to the path specification for indexing policy paths with the key difference that the path corresponds to the property instead of the value, i.e. there is no wild card at the end.</span></span> <span data-ttu-id="d51ac-128">즉, 끝에는 와일드 카드가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d51ac-128">For example, you would specify /department/?</span></span> <span data-ttu-id="d51ac-129">예를 들어 부서 아래에서 값을 인덱싱하도록 /department/?를 지정하지만 /department를 파티션 키 정의로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d51ac-129">to index the values under department, but specify /department as the partition key definition.</span></span> <span data-ttu-id="d51ac-130">파티션 키는 암시적으로 인덱싱되며, 인덱싱 정책 재정의를 사용하여 인덱싱에서 제외할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d51ac-130">The partition key is implicitly indexed and cannot be excluded from indexing using indexing policy overrides.</span></span>
> 
> 

<span data-ttu-id="d51ac-131">파티션 키의 선택이 응용 프로그램의 성능에 미치는 영향을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d51ac-131">Let's look at how the choice of partition key impacts the performance of your application.</span></span>

## <a name="working-with-the-azure-cosmos-db-sdks"></a><span data-ttu-id="d51ac-132">Azure Cosmos DB SDK 사용</span><span class="sxs-lookup"><span data-stu-id="d51ac-132">Working with the Azure Cosmos DB SDKs</span></span>
<span data-ttu-id="d51ac-133">Azure Cosmos DB에는 [REST API 버전 2015-12-16](/rest/api/documentdb/)을 사용한 자동 분할에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d51ac-133">Azure Cosmos DB added support for automatic partitioning with [REST API version 2015-12-16](/rest/api/documentdb/).</span></span> <span data-ttu-id="d51ac-134">분할된 컨테이너를 만들려면 지원되는 SDK 플랫폼(.NET, Node.js, Java, Python, MongoDB) 중 하나에서 SDK 버전 1.6.0 이상을 다운로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d51ac-134">In order to create partitioned containers, you must download SDK versions 1.6.0 or newer in one of the supported SDK platforms (.NET, Node.js, Java, Python, MongoDB).</span></span> 

### <a name="creating-containers"></a><span data-ttu-id="d51ac-135">컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="d51ac-135">Creating containers</span></span>
<span data-ttu-id="d51ac-136">다음 샘플에서는 처리량이 초당 20,000개 요청 단위인 장치 원격 분석 데이터를 저장하는 컨테이너를 만드는 .NET 코드 조각을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d51ac-136">The following sample shows a .NET snippet to create a container to store device telemetry data of 20,000 request units per second of throughput.</span></span> <span data-ttu-id="d51ac-137">SDK는 OfferThroughput 값을 설정합니다(이 값은 REST API에서 `x-ms-offer-throughput` 요청 헤더를 설정함).</span><span class="sxs-lookup"><span data-stu-id="d51ac-137">The SDK sets the OfferThroughput value (which in turn sets the `x-ms-offer-throughput` request header in the REST API).</span></span> <span data-ttu-id="d51ac-138">여기에서는 `/deviceId` 를 파티션 키로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d51ac-138">Here we set the `/deviceId` as the partition key.</span></span> <span data-ttu-id="d51ac-139">선택한 파티션 키는 이름 및 인덱싱 정책과 같은 나머지 컨테이너 메타데이터와 함께 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="d51ac-139">The choice of partition key is saved along with the rest of the container metadata like name and indexing policy.</span></span>

<span data-ttu-id="d51ac-140">이 샘플에서는 (a) 장치 수가 많고, 쓰기가 파티션 간에 균등하게 분산될 수 있으며, 대용량 데이터를 수집하도록 데이터베이스를 확장할 수 있으며, (b) 장치에 대한 최신 읽기 가져오기와 같은 요청이 대부분 단일 deviceId로 범위가 지정되고 단일 파티션에서 검색될 수 있음을 알고 있기 때문에 `deviceId` 를 선택했습니다.</span><span class="sxs-lookup"><span data-stu-id="d51ac-140">For this sample, we picked `deviceId` since we know that (a) since there are a large number of devices, writes can be distributed across partitions evenly and allowing us to scale the database to ingest massive volumes of data and (b) many of the requests like fetching the latest reading for a device are scoped to a single deviceId and can be retrieved from a single partition.</span></span>

```csharp
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey);
await client.CreateDatabaseAsync(new Database { Id = "db" });

// Container for device telemetry. Here the property deviceId will be used as the partition key to 
// spread across partitions. Configured for 10K RU/s throughput and an indexing policy that supports 
// sorting against any number or string property.
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 20000 });
```

<span data-ttu-id="d51ac-141">이 메서드에서 Cosmos DB에 대한 REST API 호출을 실행하면 이 서비스가 요청된 처리량에 따라 파티션 수를 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="d51ac-141">This method makes a REST API call to Cosmos DB, and the service will provision a number of partitions based on the requested throughput.</span></span> <span data-ttu-id="d51ac-142">성능은 향상되어야 하므로 컨테이너의 처리량을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d51ac-142">You can change the throughput of a container as your performance needs evolve.</span></span> 

### <a name="reading-and-writing-items"></a><span data-ttu-id="d51ac-143">항목 읽기 및 쓰기</span><span class="sxs-lookup"><span data-stu-id="d51ac-143">Reading and writing items</span></span>
<span data-ttu-id="d51ac-144">이제 Cosmos DB에 데이터를 삽입해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d51ac-144">Now, let's insert data into Cosmos DB.</span></span> <span data-ttu-id="d51ac-145">다음은 장치 읽기 및 새 장치 읽기를 컨테이너에 삽입하는 CreateDocumentAsync 호출이 포함된 샘플 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="d51ac-145">Here's a sample class containing a device reading, and a call to CreateDocumentAsync to insert a new device reading into a container.</span></span> <span data-ttu-id="d51ac-146">DocumentDB API를 활용하는 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d51ac-146">This is an example leveraging the DocumentDB API:</span></span>

```csharp
public class DeviceReading
{
    [JsonProperty("id")]
    public string Id;

    [JsonProperty("deviceId")]
    public string DeviceId;

    [JsonConverter(typeof(IsoDateTimeConverter))]
    [JsonProperty("readingTime")]
    public DateTime ReadingTime;

    [JsonProperty("metricType")]
    public string MetricType;

    [JsonProperty("unit")]
    public string Unit;

    [JsonProperty("metricValue")]
    public double MetricValue;
  }

// Create a document. Here the partition key is extracted as "XMS-0001" based on the collection definition
await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "coll"),
    new DeviceReading
    {
        Id = "XMS-001-FE24C",
        DeviceId = "XMS-0001",
        MetricType = "Temperature",
        MetricValue = 105.00,
        Unit = "Fahrenheit",
        ReadingTime = DateTime.UtcNow
    });
```

<span data-ttu-id="d51ac-147">파티션 키와 ID로 항목을 읽고 업데이트한 다음 마지막 단계로 파티션 키와 ID로 해당 항목을 삭제해 보겠습니다. 읽기에 PartitionKey 값(REST API의 `x-ms-documentdb-partitionkey` 요청 헤더에 해당)이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="d51ac-147">Let's read the item by its partition key and id, update it, and then as a final step, delete it by partition key and id. Note that the reads include a PartitionKey value (corresponding to the `x-ms-documentdb-partitionkey` request header in the REST API).</span></span>

```csharp
// Read document. Needs the partition key and the ID to be specified
Document result = await client.ReadDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });

DeviceReading reading = (DeviceReading)(dynamic)result;

// Update the document. Partition key is not required, again extracted from the document
reading.MetricValue = 104;
reading.ReadingTime = DateTime.UtcNow;

await client.ReplaceDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  reading);

// Delete document. Needs partition key
await client.DeleteDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });
```

### <a name="querying-partitioned-containers"></a><span data-ttu-id="d51ac-148">분할된 컨테이너 쿼리</span><span class="sxs-lookup"><span data-stu-id="d51ac-148">Querying partitioned containers</span></span>
<span data-ttu-id="d51ac-149">분할된 컨테이너의 데이터를 쿼리하면 Azure Cosmos DB에서 필터에 지정된 파티션 키 값(있는 경우)에 해당하는 파티션으로 쿼리를 자동으로 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="d51ac-149">When you query data in partitioned containers, Cosmos DB automatically routes the query to the partitions corresponding to the partition key values specified in the filter (if there are any).</span></span> <span data-ttu-id="d51ac-150">예를 들어 이 쿼리는 파티션 키 "XMS-0001"이 포함된 파티션으로만 라우팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="d51ac-150">For example, this query is routed to just the partition containing the partition key "XMS-0001".</span></span>

```csharp
// Query using partition key
IQueryable<DeviceReading> query = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"))
    .Where(m => m.MetricType == "Temperature" && m.DeviceId == "XMS-0001");
```
    
<span data-ttu-id="d51ac-151">다음 쿼리는 파티션 키(DeviceId)에 대한 필터가 없으므로 파티션의 인덱스에 대해 실행되는 모든 파티션으로 팬아웃됩니다.</span><span class="sxs-lookup"><span data-stu-id="d51ac-151">The following query does not have a filter on the partition key (DeviceId) and is fanned out to all partitions where it is executed against the partition's index.</span></span> <span data-ttu-id="d51ac-152">SDK가 파티션에 걸쳐 쿼리를 실행하도록 EnableCrossPartitionQuery(REST API의`x-ms-documentdb-query-enablecrosspartition` )를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d51ac-152">Note that you have to specify the EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` in the REST API) to have the SDK to execute a query across partitions.</span></span>

```csharp
// Query across partition keys
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true })
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100);
```

<span data-ttu-id="d51ac-153">Cosmos DB는 SDK 1.12.0 이상에서 SQL을 사용하는 분할된 컨테이너에서 [집계 함수](documentdb-sql-query.md#Aggregates) `COUNT`, `MIN`, `MAX`, `SUM` 및 `AVG`를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d51ac-153">Cosmos DB supports [aggregate functions](documentdb-sql-query.md#Aggregates) `COUNT`, `MIN`, `MAX`, `SUM` and `AVG` over partitioned containers using SQL starting with SDKs 1.12.0 and above.</span></span> <span data-ttu-id="d51ac-154">쿼리는 단일 집계 연산자를 포함해야 하고 프로젝션에 단일 값을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d51ac-154">Queries must include a single aggregate operator, and must include a single value in the projection.</span></span>

### <a name="parallel-query-execution"></a><span data-ttu-id="d51ac-155">병렬 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="d51ac-155">Parallel query execution</span></span>
<span data-ttu-id="d51ac-156">Cosmos DB SDK 1.9.0 이상에서는 다수의 파티션에 연결해야 하는 경우에도 분할된 컬렉션에 대해 대기 시간이 짧은 쿼리를 수행할 수 있도록 하는 병렬 쿼리 실행 옵션을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d51ac-156">The Cosmos DB SDKs 1.9.0 and above support parallel query execution options, which allow you to perform low latency queries against partitioned collections, even when they need to touch a large number of partitions.</span></span> <span data-ttu-id="d51ac-157">예를 들어 다음 쿼리는 파티션에 걸쳐 병렬로 실행되도록 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d51ac-157">For example, the following query is configured to run in parallel across partitions.</span></span>

```csharp
// Cross-partition Order By Queries
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true, MaxDegreeOfParallelism = 10, MaxBufferedItemCount = 100})
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100)
    .OrderBy(m => m.MetricValue);
```
    
<span data-ttu-id="d51ac-158">다음 매개 변수를 조정하여 병렬 쿼리 실행을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d51ac-158">You can manage parallel query execution by tuning the following parameters:</span></span>

* <span data-ttu-id="d51ac-159">`MaxDegreeOfParallelism`을 설정하여 컨테이너의 파티션에 대한 최대 동시 네트워크 연결 수를 나타내는 병렬 처리 수준을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d51ac-159">By setting `MaxDegreeOfParallelism`, you can control the degree of parallelism i.e., the maximum number of simultaneous network connections to the container's partitions.</span></span> <span data-ttu-id="d51ac-160">이 값을 -1로 설정하는 경우 병렬 처리 수준이 SDK에서 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="d51ac-160">If you set this to -1, the degree of parallelism is managed by the SDK.</span></span> <span data-ttu-id="d51ac-161">`MaxDegreeOfParallelism`이 지정되지 않았거나 기본값인 0으로 설정된 경우 컨테이너의 파티션에 단일 네트워크 연결이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="d51ac-161">If the `MaxDegreeOfParallelism` is not specified or set to 0, which is the default value, there will be a single network connection to the container's partitions.</span></span>
* <span data-ttu-id="d51ac-162">`MaxBufferedItemCount`를 설정하여 쿼리 대기 시간과 클라이언트 쪽 메모리 사용률 간에 균형을 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d51ac-162">By setting `MaxBufferedItemCount`, you can trade off query latency and client-side memory utilization.</span></span> <span data-ttu-id="d51ac-163">이 매개 변수를 생략하거나 -1로 설정하는 경우 병렬 쿼리 실행 중에 버퍼링되는 항목의 수가 SDK에서 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="d51ac-163">If you omit this parameter or set this to -1, the number of items buffered during parallel query execution is managed by the SDK.</span></span>

<span data-ttu-id="d51ac-164">컬렉션에 동일한 상태를 지정할 경우, 병렬 쿼리는 직렬 실행의 경우와 동일한 순서로 결과를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d51ac-164">Given the same state of the collection, a parallel query will return results in the same order as in serial execution.</span></span> <span data-ttu-id="d51ac-165">정렬(ORDER BY 및/또는 TOP)을 포함하는 파티션 간 쿼리를 수행할 경우 Azure Cosmos DB SDK는 파티션에 걸쳐 병렬로 쿼리를 실행하고, 클라이언트 쪽에서 부분적으로 정렬된 결과를 병합하여 전역으로 정렬된 결과를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="d51ac-165">When performing a cross-partition query that includes sorting (ORDER BY and/or TOP), the Azure Cosmos DB SDK issues the query in parallel across partitions and merges partially sorted results in the client side to produce globally ordered results.</span></span>

### <a name="executing-stored-procedures"></a><span data-ttu-id="d51ac-166">저장된 프로시저 실행</span><span class="sxs-lookup"><span data-stu-id="d51ac-166">Executing stored procedures</span></span>
<span data-ttu-id="d51ac-167">장치 ID가 동일한 문서에 대해 원자성 트랜잭션을 실행할 수도 있습니다(예: 장치의 최신 상태 또는 집계를 단일 항목에서 유지 관리하는 경우).</span><span class="sxs-lookup"><span data-stu-id="d51ac-167">You can also execute atomic transactions against documents with the same device ID, e.g. if you're maintaining aggregates or the latest state of a device in a single item.</span></span> 

```csharp
await client.ExecuteStoredProcedureAsync<DeviceReading>(
    UriFactory.CreateStoredProcedureUri("db", "coll", "SetLatestStateAcrossReadings"),
    new RequestOptions { PartitionKey = new PartitionKey("XMS-001") }, 
    "XMS-001-FE24C");
```
   
<span data-ttu-id="d51ac-168">다음 섹션에서는 단일 파티션 컨테이너에서 분할된 컨테이너로 이동하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d51ac-168">In the next section, we look at how you can move to partitioned containers from single-partition containers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d51ac-169">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d51ac-169">Next steps</span></span>
<span data-ttu-id="d51ac-170">이 문서에서는 DocumentDB API를 사용하여 Azure Cosmos DB 컨테이너의 분할 작업을 수행하는 방법에 대한 개요를 제공했습니다.</span><span class="sxs-lookup"><span data-stu-id="d51ac-170">In this article, we provided an overview of how to work with partitioning of Azure Cosmos DB containers with the DocumentDB API.</span></span> <span data-ttu-id="d51ac-171">Azure Cosmos DB API를 사용하여 분할하기 위한 개념 및 모범 사례의 개요는 [분할 및 수평적 크기 조정](../cosmos-db/partition-data.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d51ac-171">Also see [partitioning and horizontal scaling](../cosmos-db/partition-data.md) for an overview of concepts and best practices for partitioning with any Azure Cosmos DB API.</span></span> 

* <span data-ttu-id="d51ac-172">Azure Cosmos DB를 사용하여 규모 및 성능 테스트를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d51ac-172">Perform scale and performance testing with Azure Cosmos DB.</span></span> <span data-ttu-id="d51ac-173">샘플에 대해서는 [Azure Cosmos DB를 사용한 성능 및 규모 테스트](performance-testing.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d51ac-173">See [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md) for a sample.</span></span>
* <span data-ttu-id="d51ac-174">[SDKs](documentdb-sdk-dotnet.md) 또는 [REST API](/rest/api/documentdb/)를 사용하여 코딩 시작</span><span class="sxs-lookup"><span data-stu-id="d51ac-174">Get started coding with the [SDKs](documentdb-sdk-dotnet.md) or the [REST API](/rest/api/documentdb/)</span></span>
* <span data-ttu-id="d51ac-175">[Azure Cosmos DB에서 프로비전된 처리량](request-units.md)에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="d51ac-175">Learn about [provisioned throughput in Azure Cosmos DB](request-units.md)</span></span>


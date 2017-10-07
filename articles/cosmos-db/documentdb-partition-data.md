---
title: "aaaPartitioning Azure Cosmos DB에서 크기를 조정 | Microsoft Docs"
description: "Azure Cosmos DB에서 분할 방법을 작동에 대 한 어떻게 tooconfigure 분할 및 파티션 키, 그리고 toopick 오른쪽 hello 파티션 키에 대 한 응용 프로그램에 대해 알아봅니다."
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
ms.openlocfilehash: 30621d2ba0b89efb72005680d5f3a73998347514
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="partitioning-in-azure-cosmos-db-using-hello-documentdb-api"></a><span data-ttu-id="49b60-103">Hello DocumentDB API를 사용 하 여 Azure Cosmos DB에서 분</span><span class="sxs-lookup"><span data-stu-id="49b60-103">Partitioning in Azure Cosmos DB using hello DocumentDB API</span></span>

<span data-ttu-id="49b60-104">[Microsoft Azure Cosmos DB](../cosmos-db/introduction.md) 있습니다 달성 신속 하 고 예측 가능한 성능 및 확장성 원활 하 게 응용 프로그램과 함께 커짐에 따라 글로벌 분산, 다중-모델 데이터베이스 설계 된 서비스 toohelp 됩니다.</span><span class="sxs-lookup"><span data-stu-id="49b60-104">[Microsoft Azure Cosmos DB](../cosmos-db/introduction.md) is a global distributed, multi-model database service designed toohelp you achieve fast, predictable performance and scale seamlessly along with your application as it grows.</span></span> 

<span data-ttu-id="49b60-105">이 문서에서는 방법을 사용 하 여 Cosmos DB 컨테이너의 분할 toowork hello DocumentDB API의 개요를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="49b60-105">This article provides an overview of how toowork with partitioning of Cosmos DB containers with hello DocumentDB API.</span></span> <span data-ttu-id="49b60-106">Azure Cosmos DB API를 사용하여 분할하기 위한 개념 및 모범 사례의 개요는 [분할 및 수평적 크기 조정](../cosmos-db/partition-data.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="49b60-106">See [partitioning and horizontal scaling](../cosmos-db/partition-data.md) for an overview of concepts and best practices for partitioning with any Azure Cosmos DB API.</span></span> 

<span data-ttu-id="49b60-107">tooget 시작 코드에서 hello 프로젝트를 다운로드, [Github](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark)합니다.</span><span class="sxs-lookup"><span data-stu-id="49b60-107">tooget started with code, download hello project from [Github](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span></span> 

<span data-ttu-id="49b60-108">이 문서를 읽은 후 다음 질문 수 tooanswer hello 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49b60-108">After reading this article, you will be able tooanswer hello following questions:</span></span>   

* <span data-ttu-id="49b60-109">Azure Cosmos DB에서 분할이 작동하는 방식</span><span class="sxs-lookup"><span data-stu-id="49b60-109">How does partitioning work in Azure Cosmos DB?</span></span>
* <span data-ttu-id="49b60-110">Azure Cosmos DB에서 분할을 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="49b60-110">How do I configure partitioning in Azure Cosmos DB</span></span>
* <span data-ttu-id="49b60-111">파티션 키 무엇 이며 응용 프로그램에 대 한 hello 올바른 파티션 키는 어떻게 선택 않으면 합니까?</span><span class="sxs-lookup"><span data-stu-id="49b60-111">What are partition keys, and how do I pick hello right partition key for my application?</span></span>

<span data-ttu-id="49b60-112">tooget 시작 코드에서 hello 프로젝트를 다운로드, [Azure Cosmos DB 성능 테스트 드라이버 샘플](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark)합니다.</span><span class="sxs-lookup"><span data-stu-id="49b60-112">tooget started with code, download hello project from [Azure Cosmos DB Performance Testing Driver Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span></span> 

<!-- placeholder until we have a permanent solution-->
<a name="partition-keys"></a>
<a name="single-partition-and-partitioned-collections"></a>
<a name="migrating-from-single-partition"></a>

## <a name="partition-keys"></a><span data-ttu-id="49b60-113">파티션 키</span><span class="sxs-lookup"><span data-stu-id="49b60-113">Partition keys</span></span>

<span data-ttu-id="49b60-114">DocumentDB API hello에서는 JSON 경로의 hello 형태로 hello 파티션 키 정의 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="49b60-114">In hello DocumentDB API, you specify hello partition key definition in hello form of a JSON path.</span></span> <span data-ttu-id="49b60-115">hello 다음 표에서 파티션 키 정의와 tooeach에 해당 하는 hello 값의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="49b60-115">hello following table shows examples of partition key definitions and hello values corresponding tooeach.</span></span> <span data-ttu-id="49b60-116">예를 들어 한 경로로 지정 된 hello 파티션 키 `/department` 나타냅니다 hello 속성 부서입니다.</span><span class="sxs-lookup"><span data-stu-id="49b60-116">hello partition key is specified as a path, e.g. `/department` represents hello property department.</span></span> 

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><span data-ttu-id="49b60-117"><strong>파티션 키</strong></span><span class="sxs-lookup"><span data-stu-id="49b60-117"><strong>Partition Key</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="49b60-118"><strong>설명</strong></span><span class="sxs-lookup"><span data-stu-id="49b60-118"><strong>Description</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="49b60-119">/department</span><span class="sxs-lookup"><span data-stu-id="49b60-119">/department</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="49b60-120">문서는 hello 항목 doc.department toohello 값에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="49b60-120">Corresponds toohello value of doc.department where doc is hello item.</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="49b60-121">/properties/name</span><span class="sxs-lookup"><span data-stu-id="49b60-121">/properties/name</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="49b60-122">여기서 doc는 hello 항목 (중첩 된 속성) doc.properties.name toohello 값에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="49b60-122">Corresponds toohello value of doc.properties.name where doc is hello item (nested property).</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="49b60-123">/id</span><span class="sxs-lookup"><span data-stu-id="49b60-123">/id</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="49b60-124">해당 doc.id toohello 값 (id와 파티션 키가 동일한 hello는 속성).</span><span class="sxs-lookup"><span data-stu-id="49b60-124">Corresponds toohello value of doc.id (id and partition key are hello same property).</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="49b60-125">/"department name"</span><span class="sxs-lookup"><span data-stu-id="49b60-125">/"department name"</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="49b60-126">문서 ["부서 이름"] 문서는 hello 항목의 toohello 값에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="49b60-126">Corresponds toohello value of doc["department name"] where doc is hello item.</span></span></p></td>
        </tr>
    </tbody>
</table>

> [!NOTE]
> <span data-ttu-id="49b60-127">hello에 대 한 파티션 키 구문은 유사 toohello 경로 지정 toohello 속성 hello 값 대신 해당 경로 hello hello 주요 차이점을 사용 하 여 정책 경로 인덱싱, 즉, 즉 와일드 카드가 없습니다 hello 끝 합니다.</span><span class="sxs-lookup"><span data-stu-id="49b60-127">hello syntax for partition key is similar toohello path specification for indexing policy paths with hello key difference that hello path corresponds toohello property instead of hello value, i.e. there is no wild card at hello end.</span></span> <span data-ttu-id="49b60-128">즉, 끝에는 와일드 카드가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="49b60-128">For example, you would specify /department/?</span></span> <span data-ttu-id="49b60-129">tooindex hello 부서, 아래 값 이지만 /department hello 파티션 키 정의로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="49b60-129">tooindex hello values under department, but specify /department as hello partition key definition.</span></span> <span data-ttu-id="49b60-130">hello 파티션 키가 암시적으로 인덱싱되며 인덱싱 정책 재정의 사용 하 여 인덱싱에서 제외할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="49b60-130">hello partition key is implicitly indexed and cannot be excluded from indexing using indexing policy overrides.</span></span>
> 
> 

<span data-ttu-id="49b60-131">Hello 선택 파티션 키 응용 프로그램의 hello 성능에 미치는 영향에 대해 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="49b60-131">Let's look at how hello choice of partition key impacts hello performance of your application.</span></span>

## <a name="working-with-hello-azure-cosmos-db-sdks"></a><span data-ttu-id="49b60-132">Hello Azure Cosmos DB Sdk 사용</span><span class="sxs-lookup"><span data-stu-id="49b60-132">Working with hello Azure Cosmos DB SDKs</span></span>
<span data-ttu-id="49b60-133">Azure Cosmos DB에는 [REST API 버전 2015-12-16](/rest/api/documentdb/)을 사용한 자동 분할에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="49b60-133">Azure Cosmos DB added support for automatic partitioning with [REST API version 2015-12-16](/rest/api/documentdb/).</span></span> <span data-ttu-id="49b60-134">1.6.0 SDK 버전을 다운로드 해야 순서 toocreate 분할 컨테이너에서 hello 중 하나에서 최신 지원 또는 SDK 플랫폼 (.NET, Node.js, Java, Python, MongoDB).</span><span class="sxs-lookup"><span data-stu-id="49b60-134">In order toocreate partitioned containers, you must download SDK versions 1.6.0 or newer in one of hello supported SDK platforms (.NET, Node.js, Java, Python, MongoDB).</span></span> 

### <a name="creating-containers"></a><span data-ttu-id="49b60-135">컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="49b60-135">Creating containers</span></span>
<span data-ttu-id="49b60-136">hello 다음 샘플에서는.NET 코드 조각 toocreate 처리량의 초 당 요청 단위를 20, 000의 컨테이너 toostore 장치 원격 분석 데이터</span><span class="sxs-lookup"><span data-stu-id="49b60-136">hello following sample shows a .NET snippet toocreate a container toostore device telemetry data of 20,000 request units per second of throughput.</span></span> <span data-ttu-id="49b60-137">hello OfferThroughput 값을 설정 하는 hello SDK (hello를 다시 설정 하는 `x-ms-offer-throughput` hello REST API에서에서 요청 헤더).</span><span class="sxs-lookup"><span data-stu-id="49b60-137">hello SDK sets hello OfferThroughput value (which in turn sets hello `x-ms-offer-throughput` request header in hello REST API).</span></span> <span data-ttu-id="49b60-138">Hello 설정 여기 `/deviceId` hello 파티션 키로 합니다.</span><span class="sxs-lookup"><span data-stu-id="49b60-138">Here we set hello `/deviceId` as hello partition key.</span></span> <span data-ttu-id="49b60-139">파티션 키의 hello 선택한 hello 나머지 이름 및 인덱싱 정책을 등과 같은 hello 컨테이너 메타 데이터와 함께 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="49b60-139">hello choice of partition key is saved along with hello rest of hello container metadata like name and indexing policy.</span></span>

<span data-ttu-id="49b60-140">이 샘플을 선택 했습니다 `deviceId` (a) 이어서 다 수의 장치를 알고, 있으므로 쓰기 여러 파티션에 균등 하 게 배포할 수 있습니다 및 허락해 tooscale hello 데이터베이스 tooingest 대규모 데이터 볼륨 및 (b) 많은 hello 요청 hello 최신 정보를 가져오는 장치에 대 한 범위 지정 된 tooa 단일 deviceId 되며 단일 파티션에에서 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49b60-140">For this sample, we picked `deviceId` since we know that (a) since there are a large number of devices, writes can be distributed across partitions evenly and allowing us tooscale hello database tooingest massive volumes of data and (b) many of hello requests like fetching hello latest reading for a device are scoped tooa single deviceId and can be retrieved from a single partition.</span></span>

```csharp
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey);
await client.CreateDatabaseAsync(new Database { Id = "db" });

// Container for device telemetry. Here hello property deviceId will be used as hello partition key too
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

<span data-ttu-id="49b60-141">이 메서드는 호출 tooCosmos DB, REST API 만들고 hello 서비스는 hello 요청된 처리량에 기반 하는 파티션의 수를 프로 비전 합니다.</span><span class="sxs-lookup"><span data-stu-id="49b60-141">This method makes a REST API call tooCosmos DB, and hello service will provision a number of partitions based on hello requested throughput.</span></span> <span data-ttu-id="49b60-142">성능 개선 요구 사항이 컨테이너의 hello 처리량을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49b60-142">You can change hello throughput of a container as your performance needs evolve.</span></span> 

### <a name="reading-and-writing-items"></a><span data-ttu-id="49b60-143">항목 읽기 및 쓰기</span><span class="sxs-lookup"><span data-stu-id="49b60-143">Reading and writing items</span></span>
<span data-ttu-id="49b60-144">이제 Cosmos DB에 데이터를 삽입해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="49b60-144">Now, let's insert data into Cosmos DB.</span></span> <span data-ttu-id="49b60-145">다음은 장치 읽기 및 호출 tooCreateDocumentAsync tooinsert 읽는 컨테이너에 새 장치를 포함 하는 샘플 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="49b60-145">Here's a sample class containing a device reading, and a call tooCreateDocumentAsync tooinsert a new device reading into a container.</span></span> <span data-ttu-id="49b60-146">다음은 hello DocumentDB API를 활용 하는 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="49b60-146">This is an example leveraging hello DocumentDB API:</span></span>

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

// Create a document. Here hello partition key is extracted as "XMS-0001" based on hello collection definition
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

<span data-ttu-id="49b60-147">파티션 키 및 id 사용 하 여 hello 항목 읽기, 업데이트 및 마지막 단계로 다음 파티션 키와 id에 의해 삭제 하겠습니다. Hello 읽기 PartitionKey 값에 포함 (해당 toohello `x-ms-documentdb-partitionkey` hello REST API에서에서 요청 헤더).</span><span class="sxs-lookup"><span data-stu-id="49b60-147">Let's read hello item by its partition key and id, update it, and then as a final step, delete it by partition key and id. Note that hello reads include a PartitionKey value (corresponding toohello `x-ms-documentdb-partitionkey` request header in hello REST API).</span></span>

```csharp
// Read document. Needs hello partition key and hello ID toobe specified
Document result = await client.ReadDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });

DeviceReading reading = (DeviceReading)(dynamic)result;

// Update hello document. Partition key is not required, again extracted from hello document
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

### <a name="querying-partitioned-containers"></a><span data-ttu-id="49b60-148">분할된 컨테이너 쿼리</span><span class="sxs-lookup"><span data-stu-id="49b60-148">Querying partitioned containers</span></span>
<span data-ttu-id="49b60-149">Cosmos DB 분할 된 컨테이너에 데이터를 자동으로 쿼리할 때 경로 (있는 경우) hello 필터에 지정 된 toohello 파티션 키 값에 해당 하는 쿼리 toohello 파티션이 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="49b60-149">When you query data in partitioned containers, Cosmos DB automatically routes hello query toohello partitions corresponding toohello partition key values specified in hello filter (if there are any).</span></span> <span data-ttu-id="49b60-150">예를 들어이 쿼리는 라우트된 toojust hello 파티션 포함 hello 파티션 키 "x m S-0001"입니다.</span><span class="sxs-lookup"><span data-stu-id="49b60-150">For example, this query is routed toojust hello partition containing hello partition key "XMS-0001".</span></span>

```csharp
// Query using partition key
IQueryable<DeviceReading> query = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"))
    .Where(m => m.MetricType == "Temperature" && m.DeviceId == "XMS-0001");
```
    
<span data-ttu-id="49b60-151">hello 다음 쿼리는 필터 hello 파티션 키 (DeviceId)에 없으며 hello 파티션 인덱스에 대해 실행 되는 tooall 파티션 정렬 됩니다.</span><span class="sxs-lookup"><span data-stu-id="49b60-151">hello following query does not have a filter on hello partition key (DeviceId) and is fanned out tooall partitions where it is executed against hello partition's index.</span></span> <span data-ttu-id="49b60-152">Toospecify hello EnableCrossPartitionQuery가 (`x-ms-documentdb-query-enablecrosspartition` hello REST API에에서) toohave hello SDK tooexecute 파티션에서 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="49b60-152">Note that you have toospecify hello EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` in hello REST API) toohave hello SDK tooexecute a query across partitions.</span></span>

```csharp
// Query across partition keys
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true })
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100);
```

<span data-ttu-id="49b60-153">Cosmos DB는 SDK 1.12.0 이상에서 SQL을 사용하는 분할된 컨테이너에서 [집계 함수](documentdb-sql-query.md#Aggregates) `COUNT`, `MIN`, `MAX`, `SUM` 및 `AVG`를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="49b60-153">Cosmos DB supports [aggregate functions](documentdb-sql-query.md#Aggregates) `COUNT`, `MIN`, `MAX`, `SUM` and `AVG` over partitioned containers using SQL starting with SDKs 1.12.0 and above.</span></span> <span data-ttu-id="49b60-154">쿼리는 단일 집계 연산자를 포함 해야 하며 hello 투영에는 단일 값을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="49b60-154">Queries must include a single aggregate operator, and must include a single value in hello projection.</span></span>

### <a name="parallel-query-execution"></a><span data-ttu-id="49b60-155">병렬 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="49b60-155">Parallel query execution</span></span>
<span data-ttu-id="49b60-156">Cosmos DB Sdk 1.9.0 hello 지원 위에 tooperform 짧은 대기 시간 수 있게 하는 병렬 쿼리 실행 옵션에 대해 쿼리를 분할 된 컬렉션 tootouch 필요한 경우에 많은 수의 파티션 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="49b60-156">hello Cosmos DB SDKs 1.9.0 and above support parallel query execution options, which allow you tooperform low latency queries against partitioned collections, even when they need tootouch a large number of partitions.</span></span> <span data-ttu-id="49b60-157">예를 들어 다음 쿼리는 hello 여러 파티션에 병렬로 구성된 toorun입니다.</span><span class="sxs-lookup"><span data-stu-id="49b60-157">For example, hello following query is configured toorun in parallel across partitions.</span></span>

```csharp
// Cross-partition Order By Queries
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true, MaxDegreeOfParallelism = 10, MaxBufferedItemCount = 100})
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100)
    .OrderBy(m => m.MetricValue);
```
    
<span data-ttu-id="49b60-158">Hello 매개 변수 뒤를 튜닝 하 여 병렬 쿼리 실행을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49b60-158">You can manage parallel query execution by tuning hello following parameters:</span></span>

* <span data-ttu-id="49b60-159">설정 하 여 `MaxDegreeOfParallelism`를 병렬 처리 수준, 즉 hello 최대 동시 네트워크 연결 toohello 컨테이너 파티션 수 정도 hello 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49b60-159">By setting `MaxDegreeOfParallelism`, you can control hello degree of parallelism i.e., hello maximum number of simultaneous network connections toohello container's partitions.</span></span> <span data-ttu-id="49b60-160">로 설정 하면이-1 너무 hello 병렬 처리 수준은 hello SDK에서 관리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="49b60-160">If you set this too-1, hello degree of parallelism is managed by hello SDK.</span></span> <span data-ttu-id="49b60-161">경우 hello `MaxDegreeOfParallelism` 지정 하지 않거나 too0는 hello 기본값을 설정 하지는 단일 네트워크 연결 toohello 컨테이너의 파티션이 있을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="49b60-161">If hello `MaxDegreeOfParallelism` is not specified or set too0, which is hello default value, there will be a single network connection toohello container's partitions.</span></span>
* <span data-ttu-id="49b60-162">`MaxBufferedItemCount`를 설정하여 쿼리 대기 시간과 클라이언트 쪽 메모리 사용률 간에 균형을 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49b60-162">By setting `MaxBufferedItemCount`, you can trade off query latency and client-side memory utilization.</span></span> <span data-ttu-id="49b60-163">이 매개 변수를 생략 하거나이-1 너무 설정 hello SDK hello 개수의 병렬 쿼리 실행 중에 버퍼링 하는 항목을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="49b60-163">If you omit this parameter or set this too-1, hello number of items buffered during parallel query execution is managed by hello SDK.</span></span>

<span data-ttu-id="49b60-164">Hello 제공 hello 컬렉션의 동일한 상태 병렬 쿼리의 직렬 실행에서와 같이 주문 동일 hello에 결과 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="49b60-164">Given hello same state of hello collection, a parallel query will return results in hello same order as in serial execution.</span></span> <span data-ttu-id="49b60-165">정렬 (ORDER BY 및 TOP)을 포함 하는 분할 간 쿼리를 수행할 때는 hello Azure Cosmos DB SDK 문제 파티션과 병합 부분적으로 정렬 된 결과 전체적으로 결과 정렬 하는 hello 클라이언트 쪽 tooproduce에 걸쳐 병렬로 쿼리를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="49b60-165">When performing a cross-partition query that includes sorting (ORDER BY and/or TOP), hello Azure Cosmos DB SDK issues hello query in parallel across partitions and merges partially sorted results in hello client side tooproduce globally ordered results.</span></span>

### <a name="executing-stored-procedures"></a><span data-ttu-id="49b60-166">저장된 프로시저 실행</span><span class="sxs-lookup"><span data-stu-id="49b60-166">Executing stored procedures</span></span>
<span data-ttu-id="49b60-167">원자성 트랜잭션을 사용 하 여 문서에 대해 실행할 수도 있습니다 동일한 장치 ID, 예를 들어 hello 집계를 관리 하 고 또는 단일 항목에서 장치의 최신 상태를 환영 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="49b60-167">You can also execute atomic transactions against documents with hello same device ID, e.g. if you're maintaining aggregates or hello latest state of a device in a single item.</span></span> 

```csharp
await client.ExecuteStoredProcedureAsync<DeviceReading>(
    UriFactory.CreateStoredProcedureUri("db", "coll", "SetLatestStateAcrossReadings"),
    new RequestOptions { PartitionKey = new PartitionKey("XMS-001") }, 
    "XMS-001-FE24C");
```
   
<span data-ttu-id="49b60-168">Hello 다음 섹션의 단일 파티션 컨테이너에서 toopartitioned 컨테이너를 이동할 수는 방법을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="49b60-168">In hello next section, we look at how you can move toopartitioned containers from single-partition containers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="49b60-169">다음 단계</span><span class="sxs-lookup"><span data-stu-id="49b60-169">Next steps</span></span>
<span data-ttu-id="49b60-170">이 문서에서는 방법을 사용 하 여 Azure Cosmos DB 컨테이너의 분할 toowork hello DocumentDB API의 개요를 제공 했습니다.</span><span class="sxs-lookup"><span data-stu-id="49b60-170">In this article, we provided an overview of how toowork with partitioning of Azure Cosmos DB containers with hello DocumentDB API.</span></span> <span data-ttu-id="49b60-171">Azure Cosmos DB API를 사용하여 분할하기 위한 개념 및 모범 사례의 개요는 [분할 및 수평적 크기 조정](../cosmos-db/partition-data.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="49b60-171">Also see [partitioning and horizontal scaling](../cosmos-db/partition-data.md) for an overview of concepts and best practices for partitioning with any Azure Cosmos DB API.</span></span> 

* <span data-ttu-id="49b60-172">Azure Cosmos DB를 사용하여 규모 및 성능 테스트를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="49b60-172">Perform scale and performance testing with Azure Cosmos DB.</span></span> <span data-ttu-id="49b60-173">샘플에 대해서는 [Azure Cosmos DB를 사용한 성능 및 규모 테스트](performance-testing.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="49b60-173">See [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md) for a sample.</span></span>
* <span data-ttu-id="49b60-174">Hello로 코딩을 시작 해 [Sdk](documentdb-sdk-dotnet.md) 또는 hello [REST API](/rest/api/documentdb/)</span><span class="sxs-lookup"><span data-stu-id="49b60-174">Get started coding with hello [SDKs](documentdb-sdk-dotnet.md) or hello [REST API](/rest/api/documentdb/)</span></span>
* <span data-ttu-id="49b60-175">[Azure Cosmos DB에서 프로비전된 처리량](request-units.md)에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="49b60-175">Learn about [provisioned throughput in Azure Cosmos DB](request-units.md)</span></span>


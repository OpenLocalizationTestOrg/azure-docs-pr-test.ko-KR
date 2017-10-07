---
title: "Azure Cosmos DB에서 날짜와 함께 aaaWorking | Microsoft Docs"
description: "Toowork와 Azure Cosmos DB에서 날짜 하는 방법에 대해 알아봅니다."
services: cosmos-db
author: arramac
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: e587772f-ce9f-498c-a017-a51e7265bb23
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: arramac
ms.openlocfilehash: 27ec170e4bef72c0b5b456738f1275ef02543024
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-dates-in-azure-cosmos-db"></a><span data-ttu-id="018d0-103">Azure Cosmos DB에서 날짜 사용</span><span class="sxs-lookup"><span data-stu-id="018d0-103">Working with Dates in Azure Cosmos DB</span></span>
<span data-ttu-id="018d0-104">Azure Cosmos DB는 네이티브 [JSON](http://www.json.org) 데이터 모델을 통해 스키마 유연성과 풍부한 인덱싱을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="018d0-104">Azure Cosmos DB delivers schema flexibility and rich indexing via a native [JSON](http://www.json.org) data model.</span></span> <span data-ttu-id="018d0-105">데이터베이스, 컬렉션, 문서 및 저장 프로시저를 포함한 모든 Azure Cosmos DB 리소스는 모델링되어 JSON 문서로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="018d0-105">All Azure Cosmos DB resources including databases, collections, documents, and stored procedures are modeled and stored as JSON documents.</span></span> <span data-ttu-id="018d0-106">이식 가능성을 위한 요구 사항인 JSON(및 Azure Cosmos DB)은 String, Number, Boolean, Array, Object 및 Null과 같은 기본 형식만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="018d0-106">As a requirement for being portable, JSON (and Azure Cosmos DB) supports only a small set of basic types: String, Number, Boolean, Array, Object, and Null.</span></span> <span data-ttu-id="018d0-107">그러나 JSON 유연한 이며 이러한 기본 형식을 사용 하 고 개체 또는 배열로 작성 하는 방식을 더 복잡 한 형식을 개발자 및 프레임 워크 toorepresent를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="018d0-107">However, JSON is flexible and allow developers and frameworks toorepresent more complex types using these primitives and composing them as objects or arrays.</span></span> 

<span data-ttu-id="018d0-108">또한 toohello 기본 형식에서 많은 응용 프로그램 필요 hello [DateTime](https://msdn.microsoft.com/library/system.datetime(v=vs.110).aspx) toorepresent 날짜 및 타임 스탬프를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="018d0-108">In addition toohello basic types, many applications need hello [DateTime](https://msdn.microsoft.com/library/system.datetime(v=vs.110).aspx) type toorepresent dates and timestamps.</span></span> <span data-ttu-id="018d0-109">이 문서에서는 개발자가 수를 저장, 검색 및 hello.NET SDK를 사용 하 여 Azure Cosmos DB에서 날짜를 쿼리 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="018d0-109">This article describes how developers can store, retrieve, and query dates in Azure Cosmos DB using hello .NET SDK.</span></span>

## <a name="storing-datetimes"></a><span data-ttu-id="018d0-110">날짜/시간 저장</span><span class="sxs-lookup"><span data-stu-id="018d0-110">Storing DateTimes</span></span>
<span data-ttu-id="018d0-111">기본적으로 hello [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) DateTime 값으로 serialize [ISO 8601](http://www.iso.org/iso/catalogue_detail?csnumber=40874) 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="018d0-111">By default, hello [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) serializes DateTime values as [ISO 8601](http://www.iso.org/iso/catalogue_detail?csnumber=40874) strings.</span></span> <span data-ttu-id="018d0-112">대부분의 응용 프로그램 DateTime hello 기본 문자열 표현을 다음 이유로 hello 용 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="018d0-112">Most applications can use hello default string representation for DateTime for hello following reasons:</span></span>

* <span data-ttu-id="018d0-113">문자열을 비교 하 고 hello hello 날짜/시간 값의 순서 지정 상대 변형 된 toostrings 있을 때 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="018d0-113">Strings can be compared, and hello relative ordering of hello DateTime values is preserved when they are transformed toostrings.</span></span> 
* <span data-ttu-id="018d0-114">이 접근 방식에는 JSON 변환에 대해 사용자 지정 코드 또는 속성이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="018d0-114">This approach doesn't require any custom code or attributes for JSON conversion.</span></span>
* <span data-ttu-id="018d0-115">JSON에 저장 되어 있는 hello 날짜는 사람이 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="018d0-115">hello dates as stored in JSON are human readable.</span></span>
* <span data-ttu-id="018d0-116">이 접근 방식은 빠른 쿼리 성능을 위해 Azure Cosmos DB의 인덱스를 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="018d0-116">This approach can take advantage of Azure Cosmos DB's index for fast query performance.</span></span>

<span data-ttu-id="018d0-117">예를 들어 다음 코드 조각 저장소 hello는 `Order` 개체의 포함 된 두 개의 날짜/시간 속성- `ShipDate` 및 `OrderDate` hello.NET SDK를 사용 하는 문서로:</span><span class="sxs-lookup"><span data-stu-id="018d0-117">For example, hello following snippet stores an `Order` object containing two DateTime properties - `ShipDate` and `OrderDate` as a document using hello .NET SDK:</span></span>

    public class Order
    {
        [JsonProperty(PropertyName="id")]
        public string Id { get; set; }
        public DateTime OrderDate { get; set; }
        public DateTime ShipDate { get; set; }
        public double Total { get; set; }
    }

    await client.CreateDocumentAsync("/dbs/orderdb/colls/orders", 
        new Order 
        { 
            Id = "09152014101",
            OrderDate = DateTime.UtcNow.AddDays(-30),
            ShipDate = DateTime.UtcNow.AddDays(-14), 
            Total = 113.39
        });

<span data-ttu-id="018d0-118">이 문서는 다음과 같이 Azure Cosmos DB에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="018d0-118">This document is stored in Azure Cosmos DB as follows:</span></span>

    {
        "id": "09152014101",
        "OrderDate": "2014-09-15T23:14:25.7251173Z",
        "ShipDate": "2014-09-30T23:14:25.7251173Z",
        "Total": 113.39
    }
    

<span data-ttu-id="018d0-119">또는 hello 1970 년 1 월 1 일 이후 경과 된 초 수를 나타내는 숫자, Datetime Unix 타임 스탬프로 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="018d0-119">Alternatively, you can store DateTimes as Unix timestamps, that is, as a number representing hello number of elapsed seconds since January 1, 1970.</span></span> <span data-ttu-id="018d0-120">Azure Cosmos DB의 내부 타임스탬프(`_ts`) 속성은 이 접근 방식을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="018d0-120">Azure Cosmos DB's internal Timestamp (`_ts`) property follows this approach.</span></span> <span data-ttu-id="018d0-121">Hello를 사용할 수 있습니다 [UnixDateTimeConverter](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.unixdatetimeconverter.aspx) 클래스 tooserialize Datetime as 번호.</span><span class="sxs-lookup"><span data-stu-id="018d0-121">You can use hello [UnixDateTimeConverter](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.unixdatetimeconverter.aspx) class tooserialize DateTimes as numbers.</span></span> 

## <a name="indexing-datetimes-for-range-queries"></a><span data-ttu-id="018d0-122">범위 쿼리의 날짜/시간 인덱싱</span><span class="sxs-lookup"><span data-stu-id="018d0-122">Indexing DateTimes for range queries</span></span>
<span data-ttu-id="018d0-123">범위 쿼리는 일반적으로 DateTime 값입니다.</span><span class="sxs-lookup"><span data-stu-id="018d0-123">Range queries are common with DateTime values.</span></span> <span data-ttu-id="018d0-124">예를 들어, 어제 이후에 만들어진 모든 주문을 toofind 필요 하거나 지난 5 분 동안 hello에서 제공 하는 모든 주문 찾기 tooperform 범위 쿼리에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="018d0-124">For example, if you need toofind all orders created since yesterday, or find all orders shipped in hello last five minutes, you need tooperform range queries.</span></span> <span data-ttu-id="018d0-125">이러한 쿼리를 효율적으로 tooexecute, 문자열에는 인덱스가 범위에 대 한 사용자 컬렉션을 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="018d0-125">tooexecute these queries efficiently, you must configure your collection for Range indexing on strings.</span></span>

    DocumentCollection collection = new DocumentCollection { Id = "orders" };
    collection.IndexingPolicy = new IndexingPolicy(new RangeIndex(DataType.String) { Precision = -1 });
    await client.CreateDocumentCollectionAsync("/dbs/orderdb", collection);

<span data-ttu-id="018d0-126">자세한 방법에 대 한 내용은 tooconfigure 색인에 정책을 [Azure Cosmos DB 인덱싱 정책을](indexing-policies.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="018d0-126">You can learn more about how tooconfigure indexing policies at [Azure Cosmos DB Indexing Policies](indexing-policies.md).</span></span>

## <a name="querying-datetimes-in-linq"></a><span data-ttu-id="018d0-127">LINQ에서 날짜/시간 쿼리</span><span class="sxs-lookup"><span data-stu-id="018d0-127">Querying DateTimes in LINQ</span></span>
<span data-ttu-id="018d0-128">DocumentDB.NET SDK hello LINQ 통해 Azure Cosmos DB에 저장 된 데이터를 쿼리를 자동으로 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="018d0-128">hello DocumentDB .NET SDK automatically supports querying data stored in Azure Cosmos DB via LINQ.</span></span> <span data-ttu-id="018d0-129">예를 들어 hello 다음 코드 조각에서는 LINQ 쿼리를 해당 필터 운송 된 주문에 hello에서 마지막 3 일</span><span class="sxs-lookup"><span data-stu-id="018d0-129">For example, hello following snippet shows a LINQ query that filters orders that were shipped in hello last three days.</span></span>

    IQueryable<Order> orders = client.CreateDocumentQuery<Order>("/dbs/orderdb/colls/orders")
        .Where(o => o.ShipDate >= DateTime.UtcNow.AddDays(-3));
          
    // Translated toohello following SQL statement and executed on Azure Cosmos DB
    SELECT * FROM root WHERE (root["ShipDate"] >= "2016-12-18T21:55:03.45569Z")

<span data-ttu-id="018d0-130">Azure Cosmos DB SQL 쿼리 언어 및 hello LINQ 공급자에 대해 자세히 알아볼 수 있습니다 [Cosmos DB 쿼리](documentdb-sql-query.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="018d0-130">You can learn more about Azure Cosmos DB's SQL query language and hello LINQ provider at [Querying Cosmos DB](documentdb-sql-query.md).</span></span>

<span data-ttu-id="018d0-131">이 문서에서는 toostore, 인덱스 및 Azure Cosmos DB에서 Datetime 쿼리 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="018d0-131">In this article, we looked at how toostore, index, and query DateTimes in Azure Cosmos DB.</span></span>

## <a name="next-steps"></a><span data-ttu-id="018d0-132">다음 단계</span><span class="sxs-lookup"><span data-stu-id="018d0-132">Next Steps</span></span>
* <span data-ttu-id="018d0-133">다운로드 및 실행 hello [GitHub의 샘플 코드](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples)</span><span class="sxs-lookup"><span data-stu-id="018d0-133">Download and run hello [Code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples)</span></span>
* <span data-ttu-id="018d0-134">[DocumentDB API 쿼리](documentdb-sql-query.md)에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="018d0-134">Learn more about [DocumentDB API Query](documentdb-sql-query.md)</span></span>
* <span data-ttu-id="018d0-135">[Azure Cosmos DB 인덱싱 정책에 대해 알아보기](indexing-policies.md)</span><span class="sxs-lookup"><span data-stu-id="018d0-135">Learn more about [Azure Cosmos DB Indexing Policies](indexing-policies.md)</span></span>

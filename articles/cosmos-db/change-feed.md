---
title: "Azure Cosmos DB에서 변경 피드 지원 사용 | Microsoft Docs"
description: "Azure Cosmos DB의 변경 피드 지원을 사용하여 문서에서 변경 내용을 추적하고 트리거와 마찬가지로 이벤트 기반 처리를 수행하고 캐시 및 분석 시스템을 최신 상태로 유지합니다."
keywords: "변경 피드"
services: cosmos-db
author: arramac
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 2d7798db-857f-431a-b10f-3ccbc7d93b50
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: rest-api
ms.topic: article
ms.date: 08/15/2017
ms.author: arramac
ms.openlocfilehash: 160fbc98e0f3dcc7d17cbe0c7f7425811596a896
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="working-with-the-change-feed-support-in-azure-cosmos-db"></a><span data-ttu-id="75333-104">Azure Cosmos DB에서 변경 피드 지원 사용</span><span class="sxs-lookup"><span data-stu-id="75333-104">Working with the change feed support in Azure Cosmos DB</span></span>
<span data-ttu-id="75333-105">[Azure Cosmos DB](../cosmos-db/introduction.md)는 빠르고 유연성 있는, 전역적으로 복제된 데이터베이스 서비스로 읽기 및 쓰기에 대해 한 자릿수 밀리초인 예측 가능한 대기 시간 동안 대량의 트랜잭션 및 운영 데이터를 저장하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="75333-105">[Azure Cosmos DB](../cosmos-db/introduction.md) is a fast and flexible globally replicated database service that is used for storing high-volume transactional and operational data with predictable single-digit millisecond latency for reads and writes.</span></span> <span data-ttu-id="75333-106">따라서 IoT, 게임, 소매 및 운영 로깅 응용 프로그램에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-106">This makes it well-suited for IoT, gaming, retail, and operational logging applications.</span></span> <span data-ttu-id="75333-107">이러한 응용 프로그램에서 일반적인 디자인 패턴은 Azure Cosmos DB 데이터에 대한 변경 내용을 추적하고 구체화된 뷰를 업데이트하며 실시간 분석을 수행하고 콜드 저장소에 데이터를 보관하며 이러한 변경 내용을 기반으로 특정 이벤트에 대한 알림을 트리거하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="75333-107">A common design pattern in these applications is to track changes made to Azure Cosmos DB data, and update materialized views, perform real-time analytics, archive data to cold storage, and trigger notifications on certain events based on these changes.</span></span> <span data-ttu-id="75333-108">Azure Cosmos DB의 **변경 피드 지원**을 사용하면 이러한 패턴 각각에 대해 효율적이고 확장 가능한 솔루션을 구축할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75333-108">The **change feed support** in Azure Cosmos DB enables you to build efficient and scalable solutions for each of these patterns.</span></span>

<span data-ttu-id="75333-109">Azure Cosmos DB에서는 변경 피드 지원을 사용하여 Azure Cosmos DB 컬렉션 내 문서의 정렬된 목록을 수정된 순서로 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-109">With change feed support, Azure Cosmos DB provides a sorted list of documents within an Azure Cosmos DB collection in the order in which they were modified.</span></span> <span data-ttu-id="75333-110">컬렉션 내에서 데이터에 대한 수정을 수신 대기하고 다음과 같은 작업을 수행하기 위해 이 피드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75333-110">This feed can be used to listen for modifications to data within the collection and perform actions such as:</span></span>

* <span data-ttu-id="75333-111">문서를 삽입하거나 수정하는 경우 API에 대한 호출 트리거</span><span class="sxs-lookup"><span data-stu-id="75333-111">Trigger a call to an API when a document is inserted or modified</span></span>
* <span data-ttu-id="75333-112">업데이트에 대한 실시간(스트림) 처리 수행</span><span class="sxs-lookup"><span data-stu-id="75333-112">Perform real-time (stream) processing on updates</span></span>
* <span data-ttu-id="75333-113">캐시, 검색 엔진 또는 데이터 웨어하우스와 데이터 동기화</span><span class="sxs-lookup"><span data-stu-id="75333-113">Synchronize data with a cache, search engine, or data warehouse</span></span>

<span data-ttu-id="75333-114">Azure Cosmos DB의 변경 내용이 유지되면 비동기적으로 처리되고 병렬 처리를 위해 한 명 이상의 소비자에게 분산될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75333-114">Changes in Azure Cosmos DB are persisted and can be processed asynchronously, and distributed across one or more consumers for parallel processing.</span></span> <span data-ttu-id="75333-115">변경 피드에 대한 API 및 이를 사용하여 확장 가능한 실시간 응용 프로그램을 빌드하는 방법에 대해 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="75333-115">Let's look at the APIs for change feed and how you can use them to build scalable real-time applications.</span></span> <span data-ttu-id="75333-116">이 문서에서는 Azure Cosmos DB 변경 피드 및 DocumentDB API를 사용하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="75333-116">This article shows how to work with Azure Cosmos DB change feed and the DocumentDB API.</span></span> 

![Azure Cosmos DB 변경 피드를 사용하여 실시간 분석 및 이벤트 기반 컴퓨팅 시나리오 작동](./media/change-feed/changefeedoverview.png)

> [!NOTE]
> <span data-ttu-id="75333-118">이 시점에 변경 피드 지원은 DocumentDB API에만 제공됩니다. Graph API 및 Table API는 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="75333-118">Change feed support is only provided for the DocumentDB API at this time; the Graph API and Table API are not currently supported.</span></span>

## <a name="use-cases-and-scenarios"></a><span data-ttu-id="75333-119">사용 사례 및 시나리오</span><span class="sxs-lookup"><span data-stu-id="75333-119">Use cases and scenarios</span></span>
<span data-ttu-id="75333-120">변경 피드를 사용하면 많은 양의 쓰기가 포함된 큰 데이터 집합을 효율적으로 처리할 수 있고 변경된 내용을 식별하는 전체 데이터 집합을 쿼리하는 대안을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-120">Change feed allows for efficient processing of large datasets with a high volume of writes, and offers an alternative to querying entire datasets to identify what has changed.</span></span> <span data-ttu-id="75333-121">예를 들어, 다음 작업을 효율적으로 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75333-121">For example, you can perform the following tasks efficiently:</span></span>

* <span data-ttu-id="75333-122">Azure Cosmos DB에 저장된 데이터를 사용하여 캐시, 검색 인덱스 또는 데이터 웨어하우스를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-122">Update a cache, search index, or a data warehouse with data stored in Azure Cosmos DB.</span></span>
* <span data-ttu-id="75333-123">응용 프로그램 수준 데이터 계층 및 보관을 구현합니다. 즉, Azure Cosmos DB에 "핫 데이터"를 저장하고 "콜드 데이터"를 [Azure Blob Storage](../storage/common/storage-introduction.md) 또는 [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md)로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="75333-123">Implement application-level data tiering and archival, that is, store "hot data" in Azure Cosmos DB, and age out "cold data" to [Azure Blob Storage](../storage/common/storage-introduction.md) or [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md).</span></span>
* <span data-ttu-id="75333-124">[Apache Hadoop](run-hadoop-with-hdinsight.md)를 사용하여 데이터에 대한 Batch 분석을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-124">Implement batch analytics on data using [Apache Hadoop](run-hadoop-with-hdinsight.md).</span></span>
* <span data-ttu-id="75333-125">Azure Cosmos DB를 사용하여 [Azure의 람다 파이프라인](https://blogs.technet.microsoft.com/msuspartner/2016/01/27/azure-partner-community-big-data-advanced-analytics-and-lambda-architecture/)을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-125">Implement [lambda pipelines on Azure](https://blogs.technet.microsoft.com/msuspartner/2016/01/27/azure-partner-community-big-data-advanced-analytics-and-lambda-architecture/) with Azure Cosmos DB.</span></span> <span data-ttu-id="75333-126">Azure Cosmos DB는 수집 및 쿼리를 모두 처리할 수 있는 확장성이 뛰어난 데이터베이스 솔루션을 제공하고 TCO가 낮은 람다 아키텍처를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-126">Azure Cosmos DB provides a scalable database solution that can handle both ingestion and query, and implement lambda architectures with low TCO.</span></span> 
* <span data-ttu-id="75333-127">다른 파티션 구성표를 사용하여 다른 Azure Cosmos DB 계정에 대한 중단 시간이 없는 마이그레이션을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-127">Perform zero down-time migrations to another Azure Cosmos DB account with a different partitioning scheme.</span></span>

<span data-ttu-id="75333-128">**수집 및 쿼리에 Azure Cosmos DB를 사용하는 람다 파이프라인:**</span><span class="sxs-lookup"><span data-stu-id="75333-128">**Lambda Pipelines with Azure Cosmos DB for ingestion and query:**</span></span>

![수집 및 쿼리에 대한 Azure Cosmos DB 기반 람다 파이프라인](./media/change-feed/lambda.png)

<span data-ttu-id="75333-130">Azure Cosmos DB를 사용하여 장치, 센서, 인프라 및 응용 프로그램에서 이벤트 데이터를 수신하고 저장하며 [Azure Stream Analytics](../stream-analytics/stream-analytics-documentdb-output.md), [Apache Storm](../hdinsight/hdinsight-storm-overview.md) 또는 [Apache Spark](../hdinsight/hdinsight-apache-spark-overview.md)를 사용하여 이러한 이벤트를 실시간으로 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-130">You can use Azure Cosmos DB to receive and store event data from devices, sensors, infrastructure, and applications, and process these events in real-time with [Azure Stream Analytics](../stream-analytics/stream-analytics-documentdb-output.md), [Apache Storm](../hdinsight/hdinsight-storm-overview.md), or [Apache Spark](../hdinsight/hdinsight-apache-spark-overview.md).</span></span> 

<span data-ttu-id="75333-131">[서버를 사용하지 않는](http://azure.com/serverless) 웹 및 모바일 앱 내에서는 [Azure Functions](../azure-functions/functions-bindings-documentdb.md) 또는 [App Services](https://azure.microsoft.com/services/app-service/)를 사용하여 해당 장치에 푸시 알림을 보내는 등의 특정 작업을 트리거하기 위해 고객의 프로필, 기본 설정 또는 위치에 대한 변경 내용과 같은 이벤트를 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75333-131">Within your [serverless](http://azure.com/serverless) web and mobile apps, you can track events such as changes to your customer's profile, preferences, or location to trigger certain actions like sending push notifications to their devices using [Azure Functions](../azure-functions/functions-bindings-documentdb.md) or [App Services](https://azure.microsoft.com/services/app-service/).</span></span> <span data-ttu-id="75333-132">예를 들어, Azure Cosmos DB를 사용하여 게임을 빌드하는 경우 변경 피드를 사용하여 완료된 게임의 점수에 따라 실시간 순위표를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75333-132">If you're using Azure Cosmos DB to build a game, you can, for example, use change feed to implement real-time leaderboards based on scores from completed games.</span></span>

## <a name="how-change-feed-works-in-azure-cosmos-db"></a><span data-ttu-id="75333-133">Azure Cosmos DB에서 변경 피드의 작동 방식</span><span class="sxs-lookup"><span data-stu-id="75333-133">How change feed works in Azure Cosmos DB</span></span>
<span data-ttu-id="75333-134">Azure Cosmos DB에서는 증분 방식으로 Azure Cosmos DB 컬렉션에 이뤄진 업데이트를 읽는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-134">Azure Cosmos DB provides the ability to incrementally read updates made to an Azure Cosmos DB collection.</span></span> <span data-ttu-id="75333-135">이 변경 피드에는 다음과 같은 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75333-135">This change feed has the following properties:</span></span>

* <span data-ttu-id="75333-136">변경 내용이 Azure Cosmos DB에서 지속되면 비동기적으로 처리될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75333-136">Changes are persistent in Azure Cosmos DB and can be processed asynchronously.</span></span>
* <span data-ttu-id="75333-137">컬렉션 내 문서에 대한 변경 내용은 변경 피드에서 즉시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75333-137">Changes to documents within a collection are available immediately in the change feed.</span></span>
* <span data-ttu-id="75333-138">각 문서에 대한 변경 내용이 한 번 변경 피드에 즉시 표시되고 클라이언트는 해당 검사점 논리를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-138">Each change to a document appears exactly once in the change feed, and clients manage their checkpointing logic.</span></span> <span data-ttu-id="75333-139">변경 피드 프로세서 라이브러리는 자동 검사점 및 “최소 한 번” 의미 체계를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-139">The change feed processor library provides automatic checkpointing and "at least once" semantics.</span></span>
* <span data-ttu-id="75333-140">지정된 문서에 대한 가장 최근의 변경 내용만이 변경 로그에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="75333-140">Only the most recent change for a given document is included in the change log.</span></span> <span data-ttu-id="75333-141">중간 변경 내용을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="75333-141">Intermediate changes may not be available.</span></span>
* <span data-ttu-id="75333-142">변경 피드는 각 파티션 키 값 내에서 수정된 순서로 정렬됩니다.</span><span class="sxs-lookup"><span data-stu-id="75333-142">The change feed is sorted by order of modification within each partition key value.</span></span> <span data-ttu-id="75333-143">파티션 키 값에 보장된 순서가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="75333-143">There is no guaranteed order across partition-key values.</span></span>
* <span data-ttu-id="75333-144">특정 시점에서 변경 내용을 동기화할 수 있습니다. 즉, 변경 내용을 사용할 수 있는 고정 데이터 보존 기간이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="75333-144">Changes can be synchronized from any point-in-time, that is, there is no fixed data retention period for which changes are available.</span></span>
* <span data-ttu-id="75333-145">변경 내용은 파티션 키 범위에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75333-145">Changes are available in chunks of partition key ranges.</span></span> <span data-ttu-id="75333-146">이 기능을 사용하면 대규모 컬렉션의 변경 내용을 여러 소비자/서버에 의해 병렬로 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75333-146">This capability allows changes from large collections to be processed in parallel by multiple consumers/servers.</span></span>
* <span data-ttu-id="75333-147">응용 프로그램은 동일한 컬렉션에서 동시에 여러 변경 피드를 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75333-147">Applications can request for multiple change feeds simultaneously on the same collection.</span></span>

<span data-ttu-id="75333-148">Azure Cosmos DB의 변경 피드는 모든 계정에 기본적으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="75333-148">Azure Cosmos DB's change feed is enabled by default for all accounts.</span></span> <span data-ttu-id="75333-149">쓰기 지역 또는 [읽기 지역](distribute-data-globally.md)에서 [프로비전된 처리량](request-units.md)을 사용하여 Azure Cosmos DB의 다른 작업과 마찬가지로 변경 피드에서 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75333-149">You can use your [provisioned throughput](request-units.md) in your write region or any [read region](distribute-data-globally.md) to read from the change feed, just like any other operation from Azure Cosmos DB.</span></span> <span data-ttu-id="75333-150">변경 피드는 컬렉션 내의 문서에 수행된 삽입 및 업데이트 작업을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-150">The change feed includes inserts and update operations made to documents within the collection.</span></span> <span data-ttu-id="75333-151">삭제 대신 문서 내에서 "soft-delete" 플래그를 설정하여 삭제를 캡처할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75333-151">You can capture deletes by setting a "soft-delete" flag within your documents in place of deletes.</span></span> <span data-ttu-id="75333-152">또는 [TTL 기능](time-to-live.md)을 통해 문서에 대한 제한 만료 기간을 설정할 수 있습니다. 예를 들어, 24시간으로 설정하고 해당 속성의 값을 사용하여 삭제를 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-152">Alternatively, you can set a finite expiration period for your documents via the [TTL capability](time-to-live.md), for example, 24 hours and use the value of that property to capture deletes.</span></span> <span data-ttu-id="75333-153">이 솔루션을 사용하여 TTL 만료 기간보다 짧은 시간 간격 내에 변경 내용을 처리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-153">With this solution, you have to process changes within a shorter time interval than the TTL expiration period.</span></span> <span data-ttu-id="75333-154">변경 피드는 문서 컬렉션 내에서 각 파티션 키 범위에 대해 사용할 수 있으며 따라서 병렬 처리를 위해 한 명 이상의 소비자에게 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75333-154">The change feed is available for each partition key range within the document collection, and thus can be distributed across one or more consumers for parallel processing.</span></span> 

![Azure Cosmos DB 변경 피드의 분산 처리](./media/change-feed/changefeedvisual.png)

<span data-ttu-id="75333-156">클라이언트 코드에서 변경 피드를 구현하는 방법에는 몇 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75333-156">You have a few options in how you implement a change feed in your client code.</span></span> <span data-ttu-id="75333-157">다음에 이어지는 섹션에서는 Azure Cosmos DB REST API 및 DocumentDB SDK를 사용하여 변경 피드를 구현하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-157">The sections that immediately follow describe how to implement the change feed using the Azure Cosmos DB REST API and the DocumentDB SDKs.</span></span> <span data-ttu-id="75333-158">그러나 .NET 응용 프로그램의 경우, 새로운 [변경 피드 프로세서 라이브러리](#change-feed-processor)를 사용하여 변경 피드의 이벤트를 처리하는 것이 좋습니다. 이 라이브러리 사용 시, 전체 파티션의 변경 사항 읽기가 간소해지고 여러 스레드를 병렬로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75333-158">However, for .NET applications, we recommend using the new [Change feed processor library](#change-feed-processor) for processing events from the change feed as it simplifies reading changes across partitions and enables multiple threads working in parallel.</span></span> 

## <span data-ttu-id="75333-159"><a id="rest-apis"></a>REST API 및 DocumentDB SDK 사용</span><span class="sxs-lookup"><span data-stu-id="75333-159"><a id="rest-apis"></a>Working with the REST API and DocumentDB SDKs</span></span>
<span data-ttu-id="75333-160">Azure Cosmos DB에서는 **컬렉션**이라는 저장소 및 처리량의 탄력적인 컨테이너를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-160">Azure Cosmos DB provides elastic containers of storage and throughput called **collections**.</span></span> <span data-ttu-id="75333-161">확장성 및 성능을 위해 [파티션 키](partition-data.md)를 사용하여 컬렉션 내의 데이터를 논리적으로 그룹화합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-161">Data within collections is logically grouped using [partition keys](partition-data.md) for scalability and performance.</span></span> <span data-ttu-id="75333-162">Azure Cosmos DB에서는 ID(읽기/가져오기), 쿼리 및 읽기-피드(검색) 기준 조회를 포함하여 이 데이터에 액세스하기 위한 다양한 API를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-162">Azure Cosmos DB provides various APIs for accessing this data, including lookup by ID (Read/Get), query, and read-feeds (scans).</span></span> <span data-ttu-id="75333-163">변경 피드는 DocumentDB의 `ReadDocumentFeed` API에 두 가지 새로운 요청 헤더를 채워서 가져올 수 있으며 파티션 키 범위에서 동시에 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75333-163">The change feed can be obtained by populating two new request headers to the DocumentDB `ReadDocumentFeed` API, and can be processed in parallel across ranges of partition keys.</span></span>

### <a name="readdocumentfeed-api"></a><span data-ttu-id="75333-164">ReadDocumentFeed API</span><span class="sxs-lookup"><span data-stu-id="75333-164">ReadDocumentFeed API</span></span>
<span data-ttu-id="75333-165">ReadDocumentFeed의 작동 방식에 대해 간략하게 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="75333-165">Let's take a brief look at how ReadDocumentFeed works.</span></span> <span data-ttu-id="75333-166">Azure Cosmos DB에서는 `ReadDocumentFeed` API를 통해 컬렉션 내에서 문서의 피드를 읽도록 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-166">Azure Cosmos DB supports reading a feed of documents within a collection via the `ReadDocumentFeed` API.</span></span> <span data-ttu-id="75333-167">예를 들어, 다음 요청은 `serverlogs` 컬렉션의 내부에서 문서의 페이지를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-167">For example, the following request returns a page of documents inside the `serverlogs` collection.</span></span> 

    GET https://mydocumentdb.documents.azure.com/dbs/smalldb/colls/serverlogs HTTP/1.1
    x-ms-date: Tue, 22 Nov 2016 17:05:14 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dgo7JEogZDn6ritWhwc5hX%2fNTV4wwM1u9V2Is1H4%2bDRg%3d
    Cache-Control: no-cache
    x-ms-consistency-level: Strong
    User-Agent: Microsoft.Azure.Documents.Client/1.10.27.5
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: mydocumentdb.documents.azure.com

<span data-ttu-id="75333-168">`x-ms-max-item-count` 헤더를 사용하여 결과를 제한할 수 있고 이전 응답에서 반환된 `x-ms-continuation` 헤더로 요청을 다시 제출하여 읽기를 다시 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75333-168">Results can be limited by using the `x-ms-max-item-count` header, and reads can be resumed by resubmitting the request with a `x-ms-continuation` header returned in the previous response.</span></span> <span data-ttu-id="75333-169">단일 클라이언트에서 수행되는 경우, `ReadDocumentFeed`는 전체 파티션의 결과를 순차적으로 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-169">When performed from a single client, `ReadDocumentFeed` iterates through results across partitions serially.</span></span> 

<span data-ttu-id="75333-170">**문서 피드의 순차적 읽기**</span><span class="sxs-lookup"><span data-stu-id="75333-170">**Serial read document feed**</span></span>

<span data-ttu-id="75333-171">지원되는 [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) 중 하나를 사용하여 문서의 피드를 검색할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75333-171">You can also retrieve the feed of documents using one of the supported [Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="75333-172">예를 들어, 다음 코드 조각은 .NET에서 [ReadDocumentFeedAsync 메서드](/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentfeedasync?view=azure-dotnet)를 사용하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="75333-172">For example, the following snippet shows how to use the [ReadDocumentFeedAsync method](/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentfeedasync?view=azure-dotnet) in .NET.</span></span>

```csharp
FeedResponse<dynamic> feedResponse = null;
do
{
    feedResponse = await client.ReadDocumentFeedAsync(collection, new FeedOptions { MaxItemCount = -1 });
}
while (feedResponse.ResponseContinuation != null);
```

### <a name="distributed-execution-of-readdocumentfeed"></a><span data-ttu-id="75333-173">ReadDocumentFeed의 분산 실행</span><span class="sxs-lookup"><span data-stu-id="75333-173">Distributed execution of ReadDocumentFeed</span></span>
<span data-ttu-id="75333-174">테라바이트 이상의 데이터를 포함하거나 대량의 업데이트를 수집하는 컬렉션의 경우, 단일 클라이언트 컴퓨터에서 읽기 피드를 순차적으로 실행하면 실용적이지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="75333-174">For collections that contain terabytes of data or more, or ingest a large volume of updates, serial execution of read feed from a single client machine might not be practical.</span></span> <span data-ttu-id="75333-175">이러한 빅 데이터 시나리오를 지원하기 위해 Azure Cosmos DB에서는 API를 제공하여 여러 클라이언트 판독기/소비자에게 `ReadDocumentFeed` 호출을 투명하게 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-175">In order to support these big data scenarios, Azure Cosmos DB provides APIs to distribute `ReadDocumentFeed` calls transparently across multiple client readers/consumers.</span></span> 

<span data-ttu-id="75333-176">**분산 읽기 문서 피드**</span><span class="sxs-lookup"><span data-stu-id="75333-176">**Distributed Read Document Feed**</span></span>

<span data-ttu-id="75333-177">증분 변경 내용의 확장 가능한 처리를 제공하기 위해 Azure Cosmos DB에서는 파티션 키 범위에 따라 변경 피드 API의 확장 모델을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-177">To provide scalable processing of incremental changes, Azure Cosmos DB supports a scale-out model for the change feed API based on ranges of partition keys.</span></span>

* <span data-ttu-id="75333-178">`ReadPartitionKeyRanges` 호출을 수행하는 컬렉션에 대한 파티션 키 범위의 목록을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75333-178">You can obtain a list of partition key ranges for a collection performing a `ReadPartitionKeyRanges` call.</span></span> 
* <span data-ttu-id="75333-179">각 파티션 키 범위의 경우 해당 범위 내에서 파티션 키를 사용하여 문서를 읽는 `ReadDocumentFeed`을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75333-179">For each partition key range, you can perform a `ReadDocumentFeed` to read documents with partition keys within that range.</span></span>

### <a name="retrieving-partition-key-ranges-for-a-collection"></a><span data-ttu-id="75333-180">컬렉션에 대한 파티션 키 범위 검색</span><span class="sxs-lookup"><span data-stu-id="75333-180">Retrieving partition key ranges for a collection</span></span>
<span data-ttu-id="75333-181">컬렉션 내에서 `pkranges` 리소스를 요청하여 파티션 키 범위를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75333-181">You can retrieve the partition key ranges by requesting the `pkranges` resource within a collection.</span></span> <span data-ttu-id="75333-182">예를 들어, 다음 요청은 `serverlogs` 컬렉션에 대한 파티션 키 범위 목록을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-182">For example the following request retrieves the list of partition key ranges for the `serverlogs` collection:</span></span>

    GET https://querydemo.documents.azure.com/dbs/bigdb/colls/serverlogs/pkranges HTTP/1.1
    x-ms-date: Tue, 15 Nov 2016 07:26:51 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dEConYmRgDExu6q%2bZ8GjfUGOH0AcOx%2behkancw3LsGQ8%3d
    x-ms-consistency-level: Session
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: querydemo.documents.azure.com

<span data-ttu-id="75333-183">이 요청에는 파티션 키 범위에 대한 메타데이터가 포함된 다음과 같은 응답을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-183">This request returns the following response containing metadata about the partition key ranges:</span></span>

    HTTP/1.1 200 Ok
    Content-Type: application/json
    x-ms-item-count: 25
    x-ms-schemaversion: 1.1
    Date: Tue, 15 Nov 2016 07:26:51 GMT

    {
       "_rid":"qYcAAPEvJBQ=",
       "PartitionKeyRanges":[
          {
             "_rid":"qYcAAPEvJBQCAAAAAAAAUA==",
             "id":"0",
             "_etag":"\"00002800-0000-0000-0000-580ac4ea0000\"",
             "minInclusive":"",
             "maxExclusive":"05C1CFFFFFFFF8",
             "_self":"dbs\/qYcAAA==\/colls\/qYcAAPEvJBQ=\/pkranges\/qYcAAPEvJBQCAAAAAAAAUA==\/",
             "_ts":1477100776
          },
          ...
       ],
       "_count": 25
    }


<span data-ttu-id="75333-184">**파티션 키 범위 속성**: 각 파티션 키 범위에는 다음 테이블에 있는 메타데이터 속성이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="75333-184">**Partition key range properties**: Each partition key range includes the metadata properties in the following table:</span></span>

<table>
    <tr>
        <th><span data-ttu-id="75333-185">헤더 이름</span><span class="sxs-lookup"><span data-stu-id="75333-185">Header name</span></span></th>
        <th><span data-ttu-id="75333-186">설명</span><span class="sxs-lookup"><span data-stu-id="75333-186">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="75333-187">id</span><span class="sxs-lookup"><span data-stu-id="75333-187">id</span></span></td>
        <td>
            <p><span data-ttu-id="75333-188">파티션 키 범위에 대한 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="75333-188">The ID for the partition key range.</span></span> <span data-ttu-id="75333-189">각 컬렉션 내에서 안정적이고 고유한 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="75333-189">This is a stable and unique ID within each collection.</span></span></p>
            <p><span data-ttu-id="75333-190">파티션 키 범위에서 변경 내용을 읽는 다음 호출에서 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-190">Must be used in the following call to read changes by partition key range.</span></span></p>
        </td>
    </tr>
    <tr>
        <td><span data-ttu-id="75333-191">maxExclusive</span><span class="sxs-lookup"><span data-stu-id="75333-191">maxExclusive</span></span></td>
        <td><span data-ttu-id="75333-192">파티션 키 범위에 대한 파티션 키 해시의 최대 값입니다.</span><span class="sxs-lookup"><span data-stu-id="75333-192">The maximum partition key hash value for the partition key range.</span></span> <span data-ttu-id="75333-193">내부에 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-193">For internal use.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="75333-194">minInclusive</span><span class="sxs-lookup"><span data-stu-id="75333-194">minInclusive</span></span></td>
        <td><span data-ttu-id="75333-195">파티션 키 범위에 대한 파티션 키 해시의 최소 값입니다.</span><span class="sxs-lookup"><span data-stu-id="75333-195">The minimum partition key hash value for the partition key range.</span></span> <span data-ttu-id="75333-196">내부에 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-196">For internal use.</span></span></td>
    </tr>       
</table>

<span data-ttu-id="75333-197">지원되는 [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) 중 하나를 사용하여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75333-197">You can do this using one of the supported [Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="75333-198">예를 들어, 다음 코드 조각은 [ReadPartitionKeyRangeFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readpartitionkeyrangefeedasync?view=azure-dotnet) 메서드를 사용하여 .NET에서 파티션 키 범위를 검색하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="75333-198">For example, the following snippet shows how to retrieve partition key ranges in .NET using the [ReadPartitionKeyRangeFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readpartitionkeyrangefeedasync?view=azure-dotnet) method.</span></span>

```csharp
string pkRangesResponseContinuation = null;
List<PartitionKeyRange> partitionKeyRanges = new List<PartitionKeyRange>();

do
{
    FeedResponse<PartitionKeyRange> pkRangesResponse = await client.ReadPartitionKeyRangeFeedAsync(
        collectionUri, 
        new FeedOptions { RequestContinuation = pkRangesResponseContinuation });

    partitionKeyRanges.AddRange(pkRangesResponse);
    pkRangesResponseContinuation = pkRangesResponse.ResponseContinuation;
}
while (pkRangesResponseContinuation != null);
```

<span data-ttu-id="75333-199">Azure Cosmos DB에서는 옵션 `x-ms-documentdb-partitionkeyrangeid` 헤더를 설정하여 파티션 키 범위당 문서 검색을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-199">Azure Cosmos DB supports retrieval of documents per partition key range by setting the optional `x-ms-documentdb-partitionkeyrangeid` header.</span></span> 

### <a name="performing-an-incremental-readdocumentfeed"></a><span data-ttu-id="75333-200">증분 ReadDocumentFeed 수행</span><span class="sxs-lookup"><span data-stu-id="75333-200">Performing an incremental ReadDocumentFeed</span></span>
<span data-ttu-id="75333-201">ReadDocumentFeed는 Azure Cosmos DB 컬렉션의 변경 내용을 증분 처리하는 다음과 같은 시나리오/작업을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-201">ReadDocumentFeed supports the following scenarios/tasks for incremental processing of changes in Azure Cosmos DB collections:</span></span>

* <span data-ttu-id="75333-202">처음부터 즉, 컬렉션 생성에서부터 문서에 대한 모든 변경 내용을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="75333-202">Read all changes to documents from the beginning, that is, from collection creation.</span></span>
* <span data-ttu-id="75333-203">현재 시간부터 문서의 향후 업데이트에 대한 모든 변경 내용 또는 사용자가 지정한 시간 이후의 변경 내용을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="75333-203">Read all changes to future updates to documents from current time, or any changes since a user-specified time.</span></span>
* <span data-ttu-id="75333-204">컬렉션의 논리 버전부터 문서에 대한 모든 변경 내용을 읽습니다(ETag).</span><span class="sxs-lookup"><span data-stu-id="75333-204">Read all changes to documents from a logical version of the collection (ETag).</span></span> <span data-ttu-id="75333-205">증분 읽기 피드 요청에서 반환된 ETag에 따라 소비자의 검사점을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75333-205">You can checkpoint your consumers based on the returned ETag from incremental read-feed requests.</span></span>

<span data-ttu-id="75333-206">변경 내용에는 문서에 대한 삽입 및 업데이트가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="75333-206">The changes include inserts and updates to documents.</span></span> <span data-ttu-id="75333-207">삭제를 캡처하려면 문서 내에서 "soft delete" 속성을 사용하거나 [기본 제공 TTL 속성](time-to-live.md)을 사용하여 변경 피드에서 보류 중인 삭제를 알려야 합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-207">To capture deletes, you must use a "soft delete" property within your documents, or use the [built-in TTL property](time-to-live.md) to signal a pending deletion in the change feed.</span></span>

<span data-ttu-id="75333-208">다음 테이블에서는 ReadDocumentFeed 작업에 대한 [요청](/rest/api/documentdb/common-documentdb-rest-request-headers.md) 및 [응답 헤더](/rest/api/documentdb/common-documentdb-rest-response-headers.md)를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-208">The following table lists the [request](/rest/api/documentdb/common-documentdb-rest-request-headers.md) and [response headers](/rest/api/documentdb/common-documentdb-rest-response-headers.md) for ReadDocumentFeed operations.</span></span>

<span data-ttu-id="75333-209">**증분 ReadDocumentFeed에 대한 요청 헤더**:</span><span class="sxs-lookup"><span data-stu-id="75333-209">**Request headers for incremental ReadDocumentFeed**:</span></span>

<table>
    <tr>
        <th><span data-ttu-id="75333-210">헤더 이름</span><span class="sxs-lookup"><span data-stu-id="75333-210">Header name</span></span></th>
        <th><span data-ttu-id="75333-211">설명</span><span class="sxs-lookup"><span data-stu-id="75333-211">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="75333-212">A-IM</span><span class="sxs-lookup"><span data-stu-id="75333-212">A-IM</span></span></td>
        <td><span data-ttu-id="75333-213">"증분 피드"로 설정하거나 그렇지 않으면 생략해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-213">Must be set to "Incremental feed", or omitted otherwise</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="75333-214">If-None-Match</span><span class="sxs-lookup"><span data-stu-id="75333-214">If-None-Match</span></span></td>
        <td>
            <p><span data-ttu-id="75333-215">헤더 없음: 처음(컬렉션 생성)부터 모든 변경 내용을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-215">No header: returns all changes from the beginning (collection creation)</span></span></p>
            <p><span data-ttu-id="75333-216">"*": 컬렉션 내의 데이터에 대한 새 변경 내용을 모두 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-216">"*": returns all new changes to data within the collection</span></span></p>           
            <p><span data-ttu-id="75333-217">&lt;etag&gt;: ETag 컬렉션에 설정한 경우 해당 논리 타임스탬프 이후에 변경한 모든 내용을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-217">&lt;etag&gt;: If set to a collection ETag, returns all changes made since that logical timestamp</span></span></p>
        </td>
    </tr>
    <tr>    
        <td><span data-ttu-id="75333-218">If-Modified-Since</span><span class="sxs-lookup"><span data-stu-id="75333-218">If-Modified-Since</span></span></td> 
        <td><span data-ttu-id="75333-219">RFC 1123 시간 형식: If-None-Match가 지정된 경우 무시합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-219">RFC 1123 time format; ignored if If-None-Match is specified</span></span></td> 
    </tr> 
    <tr>
        <td><span data-ttu-id="75333-220">x-ms-documentdb-partitionkeyrangeid</span><span class="sxs-lookup"><span data-stu-id="75333-220">x-ms-documentdb-partitionkeyrangeid</span></span></td>
        <td><span data-ttu-id="75333-221">데이터를 읽는 파티션 키 범위 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="75333-221">The partition key range ID for reading data.</span></span></td>
    </tr>
</table>

<span data-ttu-id="75333-222">**증분 ReadDocumentFeed에 대한 응답 헤더**:</span><span class="sxs-lookup"><span data-stu-id="75333-222">**Response headers for incremental ReadDocumentFeed**:</span></span>

<table> <tr>
        <th><span data-ttu-id="75333-223">헤더 이름</span><span class="sxs-lookup"><span data-stu-id="75333-223">Header name</span></span></th>
        <th><span data-ttu-id="75333-224">설명</span><span class="sxs-lookup"><span data-stu-id="75333-224">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="75333-225">etag</span><span class="sxs-lookup"><span data-stu-id="75333-225">etag</span></span></td>
        <td>
            <p><span data-ttu-id="75333-226">응답에서 반환되는 최근 문서의 LSN(논리 시퀀스 번호)입니다.</span><span class="sxs-lookup"><span data-stu-id="75333-226">The logical sequence number (LSN) of last document returned in the response.</span></span></p>
            <p><span data-ttu-id="75333-227">증분 ReadDocumentFeed는 If-None-Match에서 이 값을 다시 제출하여 다시 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75333-227">Incremental ReadDocumentFeed can be resumed by resubmitting this value in If-None-Match.</span></span></p>
        </td>
    </tr>
</table>

<span data-ttu-id="75333-228">다음 논리적 버전/ETag `28535` 및 파티션 키 범위 = `16`의 컬렉션에서 모든 증분 변경 내용을 반환하는 샘플 요청입니다.</span><span class="sxs-lookup"><span data-stu-id="75333-228">Here's a sample request to return all incremental changes in collection from the logical version/ETag `28535` and partition key range = `16`:</span></span>

    GET https://mydocumentdb.documents.azure.com/dbs/bigdb/colls/bigcoll/docs HTTP/1.1
    x-ms-max-item-count: 1
    If-None-Match: "28535"
    A-IM: Incremental feed
    x-ms-documentdb-partitionkeyrangeid: 16
    x-ms-date: Tue, 22 Nov 2016 20:43:01 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dzdpL2QQ8TCfiNbW%2fEcT88JHNvWeCgDA8gWeRZ%2btfN5o%3d
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: mydocumentdb.documents.azure.com

<span data-ttu-id="75333-229">변경 내용은 파티션 키 범위 내의 각 파티션 키 값 안에서 시간 기준으로 정렬됩니다.</span><span class="sxs-lookup"><span data-stu-id="75333-229">Changes are ordered by time within each partition key value within the partition key range.</span></span> <span data-ttu-id="75333-230">파티션 키 값에 보장된 순서가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="75333-230">There is no guaranteed order across partition-key values.</span></span> <span data-ttu-id="75333-231">단일 페이지에 맞출 수 있는 것보다 결과가 많은 경우 이전 응답의 `etag`와 같은 값을 포함한 `If-None-Match` 헤더로 요청을 다시 제출하여 결과의 다음 페이지를 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75333-231">If there are more results than can fit in a single page, you can read the next page of results by resubmitting the request with the `If-None-Match` header with value equal to the `etag` from the previous response.</span></span> <span data-ttu-id="75333-232">저장 프로시저 또는 트리거 내에서 여러 문서를 트랜잭션 방식으로 삽입 또는 업데이트한 경우 동일한 응답 페이지 내에서 모두 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="75333-232">If multiple documents were inserted or updated transactionally within a stored procedure or trigger, they will all be returned within the same response page.</span></span>

> [!NOTE]
> <span data-ttu-id="75333-233">변경 피드를 사용하면 저장된 프로시저 또는 트리거 내에서 여러 문서를 삽입 또는 업데이트할 때 `x-ms-max-item-count`에 지정된 것보다 더 많은 항목이 한 페이지에 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="75333-233">With change feed, you might get more items returned in a page than specified in `x-ms-max-item-count` in the case of multiple documents inserted or updated inside a stored procedures or triggers.</span></span> 

<span data-ttu-id="75333-234">.NET SDK(1.17.0)를 사용하는 경우 `CreateDocumentChangeFeedQuery`를 호출할 때 `StartTime` 이후에 변경된 문서를 즉시 반환하도록 `ChangeFeedOptions`의 `StartTime` 필드를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-234">When using the .NET SDK (1.17.0), set the field `StartTime` in `ChangeFeedOptions` to directly return changed documents since `StartTime` when calling  `CreateDocumentChangeFeedQuery`.</span></span> <span data-ttu-id="75333-235">REST API를 사용하여 `If-Modified-Since`를 지정하면 사용자 요청은 문서 자체가 아닌 응답 헤더의 연속 토큰 또는 `etag`를 반환하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="75333-235">By specifying `If-Modified-Since` using the REST API, your request will return not the documents themselves, but rather the continuation token or `etag` in the response header.</span></span> <span data-ttu-id="75333-236">지정된 시간이 수정된 문서를 반환하려면 `If-None-Match`를 사용하는 다음 요청에 연속 토큰 `etag`를 사용하여 실제 문서를 반환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-236">To return the documents modified the specified time, the continuation token `etag` must then be used in the next request with `If-None-Match` to return the actual documents.</span></span> 

<span data-ttu-id="75333-237">.NET SDK는 컬렉션의 변경 내용에 액세스할 수 있도록 [CreateDocumentChangeFeedQuery](/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery?view=azure-dotnet) 및 [ChangeFeedOptions](/dotnet/api/microsoft.azure.documents.client.changefeedoptions?view=azure-dotnet) 도우미 클래스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-237">The .NET SDK provides the [CreateDocumentChangeFeedQuery](/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery?view=azure-dotnet) and [ChangeFeedOptions](/dotnet/api/microsoft.azure.documents.client.changefeedoptions?view=azure-dotnet) helper classes to access changes made to a collection.</span></span> <span data-ttu-id="75333-238">다음 코드 조각에서는 단일 클라이언트에서 .NET SDK를 사용하여 처음부터 모든 변경 내용을 검색하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="75333-238">The following snippet shows how to retrieve all changes from the beginning using the .NET SDK from a single client.</span></span>

```csharp
private async Task<Dictionary<string, string>> GetChanges(
    DocumentClient client,
    string collection,
    Dictionary<string, string> checkpoints)
{
    string pkRangesResponseContinuation = null;
    List<PartitionKeyRange> partitionKeyRanges = new List<PartitionKeyRange>();

    do
    {
        FeedResponse<PartitionKeyRange> pkRangesResponse = await client.ReadPartitionKeyRangeFeedAsync(
            collectionUri, 
            new FeedOptions { RequestContinuation = pkRangesResponseContinuation });

        partitionKeyRanges.AddRange(pkRangesResponse);
        pkRangesResponseContinuation = pkRangesResponse.ResponseContinuation;
    }
    while (pkRangesResponseContinuation != null);

    foreach (PartitionKeyRange pkRange in partitionKeyRanges)
    {
        string continuation = null;
        checkpoints.TryGetValue(pkRange.Id, out continuation);

        IDocumentQuery<Document> query = client.CreateDocumentChangeFeedQuery(
            collection,
            new ChangeFeedOptions
            {
                PartitionKeyRangeId = pkRange.Id,
                StartFromBeginning = true,
                RequestContinuation = continuation,
                MaxItemCount = 1
            });

        while (query.HasMoreResults)
        {
            FeedResponse<DeviceReading> readChangesResponse = query.ExecuteNextAsync<DeviceReading>().Result;

            foreach (DeviceReading changedDocument in readChangesResponse)
            {
                Console.WriteLine(changedDocument.Id);
            }

            checkpoints[pkRange.Id] = readChangesResponse.ResponseContinuation;
        }
    }

    return checkpoints;
}
```
<span data-ttu-id="75333-239">다음 코드 조각에서는 변경 피드 지원과 앞의 함수를 사용하여 Azure Cosmos DB에서 실시간으로 변경 내용을 처리하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="75333-239">And the following snippet shows how to process changes in real-time with Azure Cosmos DB by using the change feed support and the preceding function.</span></span> <span data-ttu-id="75333-240">첫 번째 호출은 컬렉션에 있는 모든 문서를 반환하고 두 번째 호출은 최근 검사점 이후에 만들어진 만든 두 개의 문서만을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-240">The first call returns all the documents in the collection, and the second only returns the two documents created that were created since the last checkpoint.</span></span>

```csharp
// Returns all documents in the collection.
Dictionary<string, string> checkpoints = await GetChanges(client, collection, new Dictionary<string, string>());

await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-201", MetricType = "Temperature", Unit = "Celsius", MetricValue = 1000 });
await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-212", MetricType = "Pressure", Unit = "psi", MetricValue = 1000 });

// Returns only the two documents created above.
checkpoints = await GetChanges(client, collection, checkpoints);
```

<span data-ttu-id="75333-241">선택적으로 이벤트를 처리하기 위해 클라이언트 쪽 논리를 사용하여 변경 피드를 필터링할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75333-241">You can also filter the change feed using client side logic to selectively process events.</span></span> <span data-ttu-id="75333-242">예를 들어, 장치 센서에서 온도 변경 이벤트만을 처리하는 클라이언트 쪽 LINQ를 사용하는 코드 조각은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="75333-242">For example, here's a snippet that uses client side LINQ to process only temperature change events from device sensors.</span></span>

```csharp
FeedResponse<DeviceReading> readChangesResponse = query.ExecuteNextAsync<DeviceReading>().Result;

foreach (DeviceReading changedDocument in 
    readChangesResponse.AsEnumerable().Where(d => d.MetricType == "Temperature" && d.MetricValue > 1000L))
{
    // trigger an action, like call an API
}
```

## <span data-ttu-id="75333-243"><a id="change-feed-processor"></a>변경 피드 프로세서 라이브러리</span><span class="sxs-lookup"><span data-stu-id="75333-243"><a id="change-feed-processor"></a>Change Feed Processor library</span></span>
<span data-ttu-id="75333-244">또 다른 옵션은 [Azure Cosmos DB 변경 피드 프로세서 라이브러리](https://docs.microsoft.com/azure/cosmos-db/documentdb-sdk-dotnet-changefeed)를 사용하는 것입니다. 이 라이브러리 사용 시, 여러 소비자에게 변경 피드의 이벤트 처리를 쉽게 분산할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75333-244">Another option is to use the [Azure Cosmos DB Change Feed Processor library](https://docs.microsoft.com/azure/cosmos-db/documentdb-sdk-dotnet-changefeed), which can help you easily distribute event processing from a change feed across multiple consumers.</span></span> <span data-ttu-id="75333-245">이 라이브러리는 .NET 플랫폼에서 변경 피드 독자(reader)를 구축하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-245">The library is great for building change feed readers on the .NET platform.</span></span> <span data-ttu-id="75333-246">다른 Cosmos DB SDK에 포함된 메서드에 변경 피드 프로세서 라이브러리를 사용하면, 다음 워크플로가 간소화됩니다.</span><span class="sxs-lookup"><span data-stu-id="75333-246">Some workflows that would be simplified by using the Change Feed Processor library over the methods included in the other Cosmos DB SDKs include:</span></span> 

* <span data-ttu-id="75333-247">데이터가 여러 파티션에 저장되어 있는 경우, 변경 피드에서 업데이트 풀링</span><span class="sxs-lookup"><span data-stu-id="75333-247">Pulling updates from change feed when data is stored across multiple partitions</span></span>
* <span data-ttu-id="75333-248">컬렉션 간, 데이터 이동 또는 복제</span><span class="sxs-lookup"><span data-stu-id="75333-248">Moving or replicating data from one collection to another</span></span>
* <span data-ttu-id="75333-249">데이터 및 변경 피드의 업데이트에 의해 트리거되는 작업의 병렬 실행</span><span class="sxs-lookup"><span data-stu-id="75333-249">Parallel execution of actions triggered by updates to data and change feed</span></span> 

<span data-ttu-id="75333-250">Cosmos SDK에서 API를 사용하면 각 파티션의 변경 피드 업데이트에 정확하게 액세스할 수 있는 반면, 변경 피드 프로세서 라이브러리를 사용하면 전체 파티션의 변경 사항 읽기가 간소해지고 여러 스레드를 병렬로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75333-250">While using the APIs in the Cosmos SDKs provides precise access to change feed updates in each partition, using the Change Feed Processor library simplifies reading changes across partitions and multiple threads working in parallel.</span></span> <span data-ttu-id="75333-251">변경 피드 프로세서는 수동으로 각 컨테이너에서 변경 내용을 읽고 각 파티션의 연속 토큰을 저장하지 않고 임대 메커니즘을 사용하여 전체 파티션의 변경 사항 읽기를 자동으로 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-251">Instead of manually reading changes from each container and saving a continuation token for each partition, the Change Feed Processor automatically manages reading changes across partitions using a lease mechanism.</span></span>

<span data-ttu-id="75333-252">이 라이브러리는 NuGet 패키지인  [Microsoft.Azure.Documents.ChangeFeedProcessor](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/)로 제공되며, 소스 코드에서 Github [샘플](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/ChangeFeedProcessor)로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75333-252">The library is available as a NuGet Package: [Microsoft.Azure.Documents.ChangeFeedProcessor](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/) and from source code as a Github [sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/ChangeFeedProcessor).</span></span> 

### <a name="understanding-change-feed-processor-library"></a><span data-ttu-id="75333-253">변경 피드 프로세서 라이브러리의 이해</span><span class="sxs-lookup"><span data-stu-id="75333-253">Understanding Change Feed Processor library</span></span> 

<span data-ttu-id="75333-254">변경 피드 프로세서를 구현하는 4개의 주요 구성 요소는 '모니터링되는 컬렉션, 임대 컬렉션, 프로세서 호스트, 소비자'입니다.</span><span class="sxs-lookup"><span data-stu-id="75333-254">There are four main components of implementing the Change Feed Processor: the monitored collection, the lease collection, the processor host, and the consumers.</span></span> 

<span data-ttu-id="75333-255">**모니터링되는 컬렉션:** 모니터링되는 컬렉션은 변경 피드가 생성되는 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="75333-255">**Monitored Collection:** The monitored collection is the data from which the change feed is generated.</span></span> <span data-ttu-id="75333-256">모니터링되는 컬렉션에 대한 모든 삽입 및 변경 내용은 컬렉션의 변경 피드에 반영됩니다.</span><span class="sxs-lookup"><span data-stu-id="75333-256">Any inserts and changes to the monitored collection are reflected in the change feed of the collection.</span></span> 

<span data-ttu-id="75333-257">**임대 컬렉션:** 임대 컬렉션은 여러 작업자 사이에서 변경 피드의 처리를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-257">**Lease Collection:** The lease collection coordinates processing the change feed across multiple workers.</span></span> <span data-ttu-id="75333-258">임대는 개별 컬렉션을 사용하여 저장됩니다(각 파티션마다 하나의 임대).</span><span class="sxs-lookup"><span data-stu-id="75333-258">A separate collection is used to store the leases with one lease per partition.</span></span> <span data-ttu-id="75333-259">이 임대 컬렉션은 변경 피드 프로세서를 실행하는 곳과 가장 근접한 쓰기 영역에서 다른 계정으로 저장하는 것이 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-259">It is advantageous to store this lease collection on a different account with the write region closer to where the Change Feed Processor is running.</span></span> <span data-ttu-id="75333-260">임대 개체에는 다음 특성이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="75333-260">A lease object contains the following attributes:</span></span> 
* <span data-ttu-id="75333-261">Owner: 임대를 소유하는 호스트를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-261">Owner: Specifies the host that owns the lease</span></span>
* <span data-ttu-id="75333-262">Continuation: 특정 파티션에 대한 변경 피드에서의 위치(연속 토큰)를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-262">Continuation: Specifies the position (continuation token) in the change feed for a particular partition</span></span>
* <span data-ttu-id="75333-263">Timestamp: 마지막으로 임대가 업데이트된 시간입니다. 타임스탬프를 사용하여 임대가 만료된 것으로 간주되는지 여부를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75333-263">Timestamp: Last time lease was updated; the timestamp can be used to check whether the lease is considered expired</span></span> 

<span data-ttu-id="75333-264">**프로세서 호스트:** 각 호스트는 활성 임대가 포함된 호스트의 다른 인스턴스 수에 따라, 처리할 파티션 수를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-264">**Processor Host:** Each host determines how many partitions to process based on how many other instances of hosts have active leases.</span></span> 
1.  <span data-ttu-id="75333-265">호스트가 시작되면 임대를 획득하여 모든 호스트에서 워크로드를 분산합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-265">When a host starts up, it acquires leases to balance the workload across all hosts.</span></span> <span data-ttu-id="75333-266">호스트는 임대가 활성 상태로 유지되도록 주기적으로 임대를 갱신합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-266">A host periodically renews leases, so leases remain active.</span></span> 
2.  <span data-ttu-id="75333-267">호스트는 읽기를 수행할 때마다 해당 임대에 대한 가장 최근 연속 토큰의 검사점을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-267">A host checkpoints the last continuation token to its lease for each read.</span></span> <span data-ttu-id="75333-268">동시성 안전을 보장하기 위해 호스트는 각 임대 업데이트에 대한 ETag를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-268">To ensure concurrency safety, a host checks the ETag for each lease update.</span></span> <span data-ttu-id="75333-269">다른 검사점 전략도 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="75333-269">Other checkpoint strategies are also supported.</span></span>  
3.  <span data-ttu-id="75333-270">종료 시 호스트는 모든 임대를 해제하지만 나중에 저장된 검사점에서 읽기를 다시 시작할 수 있도록 연속 정보를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-270">Upon shutdown, a host releases all leases but keeps the continuation information, so it can resume reading from the stored checkpoint later.</span></span> 

<span data-ttu-id="75333-271">이 경우에 호스트 수는 파티션(임대) 수보다 클 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="75333-271">At this time the number of hosts cannot be greater than the number of partitions (leases).</span></span>

<span data-ttu-id="75333-272">**소비자:** 소비자나 작업자는 각 호스트에서 시작된 변경 피드 처리를 수행하는 스레드입니다.</span><span class="sxs-lookup"><span data-stu-id="75333-272">**Consumers:** Consumers, or workers, are threads that perform the change feed processing initiated by each host.</span></span> <span data-ttu-id="75333-273">각 프로세서 호스트에는 여러 소비자가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75333-273">Each processor host can have multiple consumers.</span></span> <span data-ttu-id="75333-274">각 소비자는 할당된 파티션에서 변경 피드를 읽고 호스트에게 변경 사항 및 만료된 임대를 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="75333-274">Each consumer reads the change feed from the partition it is assigned to and notifies its host of changes and expired leases.</span></span>

<span data-ttu-id="75333-275">변경 피드 프로세서의 이러한 4개의 요소가 상호 작용하는 방법을 이해하기 위해 다음 다이어그램의 예제를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="75333-275">To further understand how these four elements of Change Feed Processor work together, let's look at an example in the following diagram.</span></span> <span data-ttu-id="75333-276">모니터링되는 컬렉션은 문서를 저장하고 파티션 키로 "city"를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-276">The monitored collection stores documents and uses the "city" as the partition key.</span></span> <span data-ttu-id="75333-277">파란색 파티션에는 "A~E"의 "city" 필드가 있는 문서가 포함된 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75333-277">We see that the blue partition contains documents with the "city" field from "A-E" and so on.</span></span> <span data-ttu-id="75333-278">두 호스트에는 동시에 4개의 파티션을 읽는 두 명의 소비자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75333-278">There are two hosts, each with two consumers reading from the four partitions in parallel.</span></span> <span data-ttu-id="75333-279">화살표는 소비자가 읽는 변경 피드의 특정 지점을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-279">The arrows show the consumers reading from a specific spot in the change feed.</span></span> <span data-ttu-id="75333-280">첫 번째 파티션에서, 어두운 파란색은 변경 피드의 아직 읽지 않은 변경 내용을 나타내는 반면, 연한 파란색은 이미 읽은 변경 내용을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="75333-280">In the first partition, the darker blue represents unread changes while the light blue represents the already read changes on the change feed.</span></span> <span data-ttu-id="75333-281">호스트는 임대 컬렉션을 사용하여 "continuation" 값을 저장하고, 이로써 각 소비자의 현재 읽기 위치를 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75333-281">The hosts use the lease collection to store a "continuation" value to keep track of the current reading position for each consumer.</span></span> 

![Azure Cosmos DB 변경 피드 프로세서 호스트 사용](./media/change-feed/changefeedprocessornew.png)

### <a name="using-change-feed-processor-library"></a><span data-ttu-id="75333-283">변경 피드 프로세서 라이브러리 사용</span><span class="sxs-lookup"><span data-stu-id="75333-283">Using Change Feed Processor Library</span></span> 
<span data-ttu-id="75333-284">다음 섹션에서는 소스 컬렉션에서 대상 컬렉션에 변경 내용을 복제하는 컨텍스트에서 변경 피드 프로세서 라이브러리를 사용하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-284">The following section explains how to use the Change Feed Processor library in the context of replicating changes from a source collection to a destination collection.</span></span> <span data-ttu-id="75333-285">여기에서 소스 컬렉션은 변경 피드 프로세서에서 모니터링되는 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="75333-285">Here, the source collection is the monitored collection in Change Feed Processor.</span></span> 

<span data-ttu-id="75333-286">**변경 피드 프로세서 NuGet 패키지를 설치하고 포함하기**</span><span class="sxs-lookup"><span data-stu-id="75333-286">**Install and include the Change Feed Processor NuGet package**</span></span> 

<span data-ttu-id="75333-287">변경 피드 프로세서 NuGet 패키지를 설치하기 전에 먼저 다음을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-287">Before installing Change Feed Processor NuGet Package, first install:</span></span> 
* <span data-ttu-id="75333-288">Microsoft.Azure.DocumentDB, 버전 1.13.1 이상</span><span class="sxs-lookup"><span data-stu-id="75333-288">Microsoft.Azure.DocumentDB, version 1.13.1 or above</span></span> 
* <span data-ttu-id="75333-289">Newtonsoft.Json, 9.0.1 버전 이상 `Microsoft.Azure.DocumentDB.ChangeFeedProcessor` 설치 및 참조로 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-289">Newtonsoft.Json, version 9.0.1 or above Install `Microsoft.Azure.DocumentDB.ChangeFeedProcessor` and include it as a reference.</span></span>

<span data-ttu-id="75333-290">**모니터링되는 컬렉션, 임대 및 대상 컬렉션 만들기**</span><span class="sxs-lookup"><span data-stu-id="75333-290">**Create a monitored, lease and destination collection**</span></span> 

<span data-ttu-id="75333-291">변경 피드 프로세서 라이브러리를 사용하려면 프로세서 호스트를 실행하기 전에 임대 컬렉션을 생성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-291">In order to use the Change Feed Processor Library, the lease collection needs to be created before running the processor host(s).</span></span> <span data-ttu-id="75333-292">앞서 언급했지만, 임대 컬렉션은 변경 피드 프로세서를 실행하는 곳과 가장 근접한 쓰기 영역에서 다른 계정으로 저장하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="75333-292">Again, we recommend storing a lease collection on a different account with a write region closer to where the Change Feed Processor is running.</span></span> <span data-ttu-id="75333-293">이 데이터 이동 예제에서는 변경 피드 프로세서 호스트를 실행하기 전에 대상 컬렉션을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-293">In this data movement example, we need to create the destination collection before running the Change Feed Processor host.</span></span> <span data-ttu-id="75333-294">샘플 코드에서 도우미 메서드를 호출하여 모니터링되는 컬렉션, 임대되는 컬렉션, 대상 컬렉션이 존재하지 않을 경우 이러한 컬렉션을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75333-294">In the sample code we call a helper method to create the monitored, leased, and destination collections if they do not already exist.</span></span> 

> [!WARNING]
> <span data-ttu-id="75333-295">응용 프로그램이 Azure Cosmos DB와 통신하기 위해 처리량을 예약할 때 컬렉션을 만드는 것은 가격에 영향을 미칩니다.</span><span class="sxs-lookup"><span data-stu-id="75333-295">Creating a collection has pricing implications, as you are reserving throughput for the application to communicate with Azure Cosmos DB.</span></span> <span data-ttu-id="75333-296">자세한 내용은 [가격 책정 페이지](https://azure.microsoft.com/pricing/details/cosmos-db/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="75333-296">For more details, please visit the [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/)</span></span>
> 
> 

<span data-ttu-id="75333-297">*프로세서 호스트 만들기*</span><span class="sxs-lookup"><span data-stu-id="75333-297">*Creating a processor host*</span></span>

<span data-ttu-id="75333-298">`ChangeFeedProcessorHost` 클래스는 검사점 및 파티션 임대 관리를 제공하는 이벤트 처리기 구현을 위한 스레드 안전, 다중 프로세스, 안전한 런타임 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-298">The `ChangeFeedProcessorHost` class provides a thread-safe, multi-process, safe runtime environment for event processor implementations that also provides checkpointing and partition lease management.</span></span> <span data-ttu-id="75333-299">`ChangeFeedProcessorHost` 클래스를 사용하려면 `IChangeFeedObserver`를 구현하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="75333-299">To use the `ChangeFeedProcessorHost` class, you can implement `IChangeFeedObserver`.</span></span> <span data-ttu-id="75333-300">이 인터페이스는 세 가지 메서드가 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-300">This interface contains three methods:</span></span>

* <span data-ttu-id="75333-301">`OpenAsync`: 이 함수는 변경 피드 관찰자를 열 때 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="75333-301">`OpenAsync`: This function is called when change feed observer is opened.</span></span> <span data-ttu-id="75333-302">소비자/관찰자가 열릴 때 특정 작업을 수행하도록 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75333-302">It can be modified to perform a specific action when consumer/observer is opened.</span></span>  
* <span data-ttu-id="75333-303">`CloseAsync`: 이 함수는 변경 피드 관찰자를 종료할 때 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="75333-303">`CloseAsync`: This function is called when change feed observer is terminated.</span></span> <span data-ttu-id="75333-304">소비자/관찰자가 닫힐 때 특정 작업을 수행하도록 함수를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75333-304">It can be modified to perform a specific action when consumer/observer is closed.</span></span>  
* <span data-ttu-id="75333-305">`ProcessChangesAsync`: 이 함수는 변경 피드에서 문서의 새로운 변경 내용을 사용할 수 있을 때 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="75333-305">`ProcessChangesAsync`: This function is called when document new changes are available on change feed.</span></span> <span data-ttu-id="75333-306">모든 변경 피드 업데이트 시 특정 작업을 수행하도록 함수를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75333-306">It can be modified to perform a specific action upon every change feed update.</span></span>  

<span data-ttu-id="75333-307">이 예제에서는 `DocumentFeedObserver` 클래스를 통해 `IChangeFeedObserver` 인터페이스를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-307">In our example, we implement the interface `IChangeFeedObserver` through the `DocumentFeedObserver` class.</span></span> <span data-ttu-id="75333-308">여기서 `ProcessChangesAsync` 함수는 변경 피드에서 대상 컬렉션에 문서를 upsert(업데이트)합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-308">Here, the `ProcessChangesAsync` function upserts (updates) a document from change feed into the destination collection.</span></span> <span data-ttu-id="75333-309">이 예제는 데이터 집합의 파티션 키를 변경하기 위해 하나의 컬렉션에서 다른 컬렉션으로 데이터를 이동하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-309">This example is useful for moving data from one collection to another in order to change the partition key of a data set.</span></span> 

<span data-ttu-id="75333-310">*프로세서 호스트 실행*</span><span class="sxs-lookup"><span data-stu-id="75333-310">*Running the Processor Host*</span></span>

<span data-ttu-id="75333-311">이벤트 처리를 시작하기 전에, 변경 피드 옵션 및 변경 피드 호스트 옵션을 모두 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75333-311">Before beginning event processing, both change feed options and change feed host options can be customized.</span></span> 
```csharp
    // Customizable change feed option and host options 
    ChangeFeedOptions feedOptions = new ChangeFeedOptions();

    // ie customize StartFromBeginning so change feed reads from beginning
    // can customize MaxItemCount, PartitonKeyRangeId, RequestContinuation, SessionToken and StartFromBeginning
    feedOptions.StartFromBeginning = true;

    ChangeFeedHostOptions feedHostOptions = new ChangeFeedHostOptions();

    // ie. customizing lease renewal interval to 15 seconds
    // can customize LeaseRenewInterval, LeaseAcquireInterval, LeaseExpirationInterval, FeedPollDelay 
    feedHostOptions.LeaseRenewInterval = TimeSpan.FromSeconds(15);

```
<span data-ttu-id="75333-312">사용자 지정할 수 있는 특정 필드는 다음 표에 요약되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75333-312">The specific fields that can be customized are summarized in the following tables.</span></span> 

<span data-ttu-id="75333-313">**변경 피드 옵션**:</span><span class="sxs-lookup"><span data-stu-id="75333-313">**Change Feed Options**:</span></span>
<table>
    <tr>
        <th><span data-ttu-id="75333-314">속성 이름</span><span class="sxs-lookup"><span data-stu-id="75333-314">Property Name</span></span></th>
        <th><span data-ttu-id="75333-315">설명</span><span class="sxs-lookup"><span data-stu-id="75333-315">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="75333-316">MaxItemCount</span><span class="sxs-lookup"><span data-stu-id="75333-316">MaxItemCount</span></span></td>
        <td><span data-ttu-id="75333-317">Azure Cosmos DB 데이터베이스 서비스의 열거 작업에서 반환할 항목의 최대 수를 가져오거나 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-317">Gets or sets the maximum number of items to be returned in the enumeration operation in the Azure Cosmos DB database service.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="75333-318">PartitionKeyRangeId</span><span class="sxs-lookup"><span data-stu-id="75333-318">PartitionKeyRangeId</span></span></td>
        <td><span data-ttu-id="75333-319">Azure Cosmos DB 데이터베이스 서비스에서 현재 요청에 대한 파티션 키 범위 ID를 가져오거나 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-319">Gets or sets the partition key range id for the current request in the Azure Cosmos DB database service.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="75333-320">RequestContinuation</span><span class="sxs-lookup"><span data-stu-id="75333-320">RequestContinuation</span></span></td>
        <td><span data-ttu-id="75333-321">Azure Cosmos DB 데이터베이스 서비스에서 요청 연속 토큰을 가져오거나 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-321">Gets or sets the request continuation token in the Azure Cosmos DB database service.</span></span></td>
    </tr>
        <tr>
        <td><span data-ttu-id="75333-322">SessionToken</span><span class="sxs-lookup"><span data-stu-id="75333-322">SessionToken</span></span></td>
        <td><span data-ttu-id="75333-323">Azure Cosmos DB 데이터베이스 서비스에서 세션 일관성에 사용할 세션 토큰을 가져오거나 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-323">Gets or sets the session token for use with session consistency in the Azure Cosmos DB database service.</span></span></td>
    </tr>
        <tr>
        <td><span data-ttu-id="75333-324">StartFromBeginning</span><span class="sxs-lookup"><span data-stu-id="75333-324">StartFromBeginning</span></span></td>
        <td><span data-ttu-id="75333-325">Azure Cosmos DB 데이터베이스 서비스에서 변경 피드가 처음(true)부터 시작해야 하는지 아니면 현재(false)부터 시작해야 하는지를 가져오거나 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-325">Gets or sets whether change feed in the Azure Cosmos DB database service should start from the beginning (true) or from current (false).</span></span> <span data-ttu-id="75333-326">기본적으로 현재(false)부터 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-326">By default, it starts from current (false).</span></span></td>
    </tr>
</table>

<span data-ttu-id="75333-327">**변경 피드 호스트 옵션**:</span><span class="sxs-lookup"><span data-stu-id="75333-327">**Change Feed Host Options**:</span></span>
<table>
    <tr>
        <th><span data-ttu-id="75333-328">속성 이름</span><span class="sxs-lookup"><span data-stu-id="75333-328">Property Name</span></span></th>
        <th><span data-ttu-id="75333-329">형식</span><span class="sxs-lookup"><span data-stu-id="75333-329">Type</span></span></th>
        <th><span data-ttu-id="75333-330">설명</span><span class="sxs-lookup"><span data-stu-id="75333-330">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="75333-331">LeaseRenewInterval</span><span class="sxs-lookup"><span data-stu-id="75333-331">LeaseRenewInterval</span></span></td>
        <td><span data-ttu-id="75333-332">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="75333-332">TimeSpan</span></span></td>
        <td><span data-ttu-id="75333-333">ChangeFeedEventHost 인스턴스에서 현재 보유한 파티션의 모든 임대에 대한 간격입니다.</span><span class="sxs-lookup"><span data-stu-id="75333-333">The interval for all leases for partitions currently held by the ChangeFeedEventHost instance.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="75333-334">LeaseAcquireInterval</span><span class="sxs-lookup"><span data-stu-id="75333-334">LeaseAcquireInterval</span></span></td>
        <td><span data-ttu-id="75333-335">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="75333-335">TimeSpan</span></span></td>
        <td><span data-ttu-id="75333-336">파티션이 알려진 호스트 인스턴스 간에 균등하게 배포되는지를 계산하는 태스크를 시작하는 간격입니다.</span><span class="sxs-lookup"><span data-stu-id="75333-336">The interval to kick off a task to compute whether partitions are distributed evenly among known host instances.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="75333-337">LeaseExpirationInterval</span><span class="sxs-lookup"><span data-stu-id="75333-337">LeaseExpirationInterval</span></span></td>
        <td><span data-ttu-id="75333-338">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="75333-338">TimeSpan</span></span></td>
        <td><span data-ttu-id="75333-339">파티션을 나타내는 임대에 대한 임대 기간인 간격입니다.</span><span class="sxs-lookup"><span data-stu-id="75333-339">The interval for which the lease is taken on a lease representing a partition.</span></span> <span data-ttu-id="75333-340">이 간격 내에서 임대를 갱신하지 않으면 기간이 만료되어 다른 ChangeFeedEventHost 인스턴스로 파티션 소유권이 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-340">If the lease is not renewed within this interval, it is expired and ownership of the partition moves to another ChangeFeedEventHost instance.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="75333-341">FeedPollDelay</span><span class="sxs-lookup"><span data-stu-id="75333-341">FeedPollDelay</span></span></td>
        <td><span data-ttu-id="75333-342">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="75333-342">TimeSpan</span></span></td>
        <td><span data-ttu-id="75333-343">현재 변경 내용이 모두 삭제된 후에 피드에 대한 새로운 변경 내용의 파티션을 폴링하는 작업 간의 지연입니다.</span><span class="sxs-lookup"><span data-stu-id="75333-343">The delay between polling a partition for new changes on the feed, after all current changes are drained.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="75333-344">CheckpointFrequency</span><span class="sxs-lookup"><span data-stu-id="75333-344">CheckpointFrequency</span></span></td>
        <td><span data-ttu-id="75333-345">CheckpointFrequency</span><span class="sxs-lookup"><span data-stu-id="75333-345">CheckpointFrequency</span></span></td>
        <td><span data-ttu-id="75333-346">검사점 임대에 대한 빈도입니다.</span><span class="sxs-lookup"><span data-stu-id="75333-346">The frequency to checkpoint leases.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="75333-347">MinPartitionCount</span><span class="sxs-lookup"><span data-stu-id="75333-347">MinPartitionCount</span></span></td>
        <td><span data-ttu-id="75333-348">int</span><span class="sxs-lookup"><span data-stu-id="75333-348">Int</span></span></td>
        <td><span data-ttu-id="75333-349">호스트의 최소 파티션 수입니다.</span><span class="sxs-lookup"><span data-stu-id="75333-349">The minimum partition count for the host.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="75333-350">MaxPartitionCount</span><span class="sxs-lookup"><span data-stu-id="75333-350">MaxPartitionCount</span></span></td>
        <td><span data-ttu-id="75333-351">int</span><span class="sxs-lookup"><span data-stu-id="75333-351">Int</span></span></td>
        <td><span data-ttu-id="75333-352">호스트에 가능한 최대 파티션 수입니다.</span><span class="sxs-lookup"><span data-stu-id="75333-352">The maximum number of partitions the host can serve.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="75333-353">DiscardExistingLeases</span><span class="sxs-lookup"><span data-stu-id="75333-353">DiscardExistingLeases</span></span></td>
        <td><span data-ttu-id="75333-354">Bool</span><span class="sxs-lookup"><span data-stu-id="75333-354">Bool</span></span></td>
        <td><span data-ttu-id="75333-355">호스트의 시작에서 모든 기존 임대를 삭제하고 호스트를 처음부터 다시 시작해야 하는지 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="75333-355">Whether on the start of the host all existing leases should be deleted and the host should start from scratch.</span></span></td>
    </tr>
</table>


<span data-ttu-id="75333-356">이벤트 처리를 시작하려면 Azure Cosmos DB 컬렉션에 적절한 매개 변수를 제공하여 `ChangeFeedProcessorHost`를 인스턴스화합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-356">To start event processing, instantiate `ChangeFeedProcessorHost`, providing the appropriate parameters for your Azure Cosmos DB collection.</span></span> <span data-ttu-id="75333-357">그런 다음 `RegisterObserverAsync`를 호출하여 `IChangeFeedObserver`(이 예제의 DocumentFeedObserver) 구현을 런타임에 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-357">Then, call `RegisterObserverAsync` to register your `IChangeFeedObserver` (DocumentFeedObserver in this example) implementation with the runtime.</span></span> <span data-ttu-id="75333-358">이 시점에서 호스트는 "greedy" 알고리즘을 사용하여 Azure Cosmos DB 컬렉션의 모든 파티션 키 범위에서 임대를 획득하려 합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-358">At this point, the host attempts to acquire a lease on every partition key range in the Azure Cosmos DB collection using a "greedy" algorithm.</span></span> <span data-ttu-id="75333-359">이러한 임대는 지정된 시간 프레임 동안 지속되며 갱신되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-359">These leases last for a given timeframe and must then be renewed.</span></span> <span data-ttu-id="75333-360">새 노드(이 예제에서는 작업자(worker) 인스턴스)가 온라인 상태가 되면 임대 예약을 하고, 각 호스트가 더 많은 임대를 획득하려 하면서 시간이 지남에 따라 노드 간에 부하가 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-360">As new nodes, worker instances, in this case, come online, they place lease reservations and over time the load shifts between nodes as each host attempts to acquire more leases.</span></span> 

<span data-ttu-id="75333-361">이 샘플 코드에서는 팩터리 클래스(DocumentFeedObserverFactory.cs)를 사용하여 관찰자를 만들고 `RegistObserverFactoryAsync`로 관찰자를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="75333-361">In the sample code, we use a factory class (DocumentFeedObserverFactory.cs) to create an observer and the `RegistObserverFactoryAsync` to register the observer.</span></span> 

```csharp
using (DocumentClient destClient = new DocumentClient(destCollInfo.Uri, destCollInfo.MasterKey))
    {
        DocumentFeedObserverFactory docObserverFactory = new DocumentFeedObserverFactory(destClient, destCollInfo);
        ChangeFeedEventHost host = new ChangeFeedEventHost(hostName, documentCollectionLocation, leaseCollectionLocation, feedOptions, feedHostOptions);

        await host.RegisterObserverFactoryAsync(docObserverFactory);

        Console.WriteLine("Running... Press enter to stop.");
        Console.ReadLine();

        await host.UnregisterObserversAsync();
    }
```
<span data-ttu-id="75333-362">시간이 지남에 따라 평형이 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="75333-362">Over time, an equilibrium is established.</span></span> <span data-ttu-id="75333-363">이 동적 기능을 사용하면 확장 및 축소 모두에 대해 CPU 기반의 자동 크기 조정을 소비자에게 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75333-363">This dynamic capability enables CPU-based auto-scaling to be applied to consumers for both scale-up and scale-down.</span></span> <span data-ttu-id="75333-364">변경 내용을 소비자가 처리할 수 있는 것보다 빠르게 Azure Cosmos DB에서 사용할 수 있는 경우 소비자에 대한 CPU가 증가하여 작업자 인스턴스 수의 크기를 자동으로 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75333-364">If changes are available in Azure Cosmos DB at a faster rate than consumers can process, the CPU increase on consumers can be used to cause an auto-scale on worker instance count.</span></span>

## <a name="next-steps"></a><span data-ttu-id="75333-365">다음 단계</span><span class="sxs-lookup"><span data-stu-id="75333-365">Next steps</span></span>
* <span data-ttu-id="75333-366">[GitHub의 Azure Cosmos DB 변경 피드 코드 샘플](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/ChangeFeed) 사용</span><span class="sxs-lookup"><span data-stu-id="75333-366">Try the [Azure Cosmos DB Change feed code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/ChangeFeed)</span></span>
* <span data-ttu-id="75333-367">[Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) 또는 [REST API](/rest/api/documentdb/)를 사용하여 코딩 시작</span><span class="sxs-lookup"><span data-stu-id="75333-367">Get started coding with the [Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md) or the [REST API](/rest/api/documentdb/).</span></span>

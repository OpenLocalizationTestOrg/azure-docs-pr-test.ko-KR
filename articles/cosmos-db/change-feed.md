---
title: "hello 변경 aaaWorking Azure Cosmos DB에서 지원 피드 | Microsoft Docs"
description: "사용 하 여 Azure Cosmos DB 문서에 피드 지원 tootrack 변경 사항을 변경 하 고 트리거와 마찬가지로 이벤트 기반 처리와 캐시 및 분석 시스템을 최신 상태로 유지를 수행 합니다."
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
ms.openlocfilehash: a4dcf4ceb476e3e08266dbcdcbee1d75e1d1eed4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-hello-change-feed-support-in-azure-cosmos-db"></a><span data-ttu-id="aaf64-104">Cosmos DB Azure의에서 hello 변경 피드 지원 팀과 작업</span><span class="sxs-lookup"><span data-stu-id="aaf64-104">Working with hello change feed support in Azure Cosmos DB</span></span>
<span data-ttu-id="aaf64-105">[Azure Cosmos DB](../cosmos-db/introduction.md)는 빠르고 유연성 있는, 전역적으로 복제된 데이터베이스 서비스로 읽기 및 쓰기에 대해 한 자릿수 밀리초인 예측 가능한 대기 시간 동안 대량의 트랜잭션 및 운영 데이터를 저장하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-105">[Azure Cosmos DB](../cosmos-db/introduction.md) is a fast and flexible globally replicated database service that is used for storing high-volume transactional and operational data with predictable single-digit millisecond latency for reads and writes.</span></span> <span data-ttu-id="aaf64-106">따라서 IoT, 게임, 소매 및 운영 로깅 응용 프로그램에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-106">This makes it well-suited for IoT, gaming, retail, and operational logging applications.</span></span> <span data-ttu-id="aaf64-107">이러한 응용 프로그램에서 일반적인 디자인 패턴 tootrack 변경 내용을 tooAzure Cosmos DB 데이터 및 구체화 된 뷰를 업데이트, 이러한 변경 내용에 따라 특정 이벤트에서 실시간 분석, 보관 데이터 toocold 저장소 및 알림을 전송할 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-107">A common design pattern in these applications is tootrack changes made tooAzure Cosmos DB data, and update materialized views, perform real-time analytics, archive data toocold storage, and trigger notifications on certain events based on these changes.</span></span> <span data-ttu-id="aaf64-108">hello **변경 피드 지원** Azure Cosmos DB에서 사용 하면 toobuild 효율적이 고 확장 가능한 솔루션 각 이러한 패턴에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-108">hello **change feed support** in Azure Cosmos DB enables you toobuild efficient and scalable solutions for each of these patterns.</span></span>

<span data-ttu-id="aaf64-109">지원 피드 변경으로 인해 Azure Cosmos DB 문서 수정 된 hello 순서로 프로그램 Azure Cosmos DB 컬렉션 내에서 정렬 된 목록을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-109">With change feed support, Azure Cosmos DB provides a sorted list of documents within an Azure Cosmos DB collection in hello order in which they were modified.</span></span> <span data-ttu-id="aaf64-110">이 피드 hello 컬렉션 내에서 toodata 수정에 대 한 사용된 toolisten 수 및와 같은 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-110">This feed can be used toolisten for modifications toodata within hello collection and perform actions such as:</span></span>

* <span data-ttu-id="aaf64-111">문서를 삽입 하거나 수정할 때 호출 tooan API 트리거</span><span class="sxs-lookup"><span data-stu-id="aaf64-111">Trigger a call tooan API when a document is inserted or modified</span></span>
* <span data-ttu-id="aaf64-112">업데이트에 대한 실시간(스트림) 처리 수행</span><span class="sxs-lookup"><span data-stu-id="aaf64-112">Perform real-time (stream) processing on updates</span></span>
* <span data-ttu-id="aaf64-113">캐시, 검색 엔진 또는 데이터 웨어하우스와 데이터 동기화</span><span class="sxs-lookup"><span data-stu-id="aaf64-113">Synchronize data with a cache, search engine, or data warehouse</span></span>

<span data-ttu-id="aaf64-114">Azure Cosmos DB의 변경 내용이 유지되면 비동기적으로 처리되고 병렬 처리를 위해 한 명 이상의 소비자에게 분산될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-114">Changes in Azure Cosmos DB are persisted and can be processed asynchronously, and distributed across one or more consumers for parallel processing.</span></span> <span data-ttu-id="aaf64-115">변경 피드를 사용 하는 방법으로 toobuild 확장 가능한 실시간 응용 프로그램에 대 한 Api hello를 살펴 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-115">Let's look at hello APIs for change feed and how you can use them toobuild scalable real-time applications.</span></span> <span data-ttu-id="aaf64-116">이 문서 toowork Azure Cosmos DB와 함께 피드 및 hello DocumentDB API을 변경 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-116">This article shows how toowork with Azure Cosmos DB change feed and hello DocumentDB API.</span></span> 

![Azure Cosmos DB 변경을 사용 하 여 피드 toopower 실시간 분석 및 이벤트 기반 컴퓨팅 시나리오](./media/change-feed/changefeedoverview.png)

> [!NOTE]
> <span data-ttu-id="aaf64-118">지원 피드 변경에만 제공 됩니다 hello DocumentDB API 시킵니다. Graph API hello 및 테이블 API 현재 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-118">Change feed support is only provided for hello DocumentDB API at this time; hello Graph API and Table API are not currently supported.</span></span>

## <a name="use-cases-and-scenarios"></a><span data-ttu-id="aaf64-119">사용 사례 및 시나리오</span><span class="sxs-lookup"><span data-stu-id="aaf64-119">Use cases and scenarios</span></span>
<span data-ttu-id="aaf64-120">변경 피드는 많은 양의 쓰기와 큰 데이터 집합의 효율적인 처리를 허용 하 고 변경 된 내용을 대체 tooquerying 전체 데이터 집합 tooidentify를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-120">Change feed allows for efficient processing of large datasets with a high volume of writes, and offers an alternative tooquerying entire datasets tooidentify what has changed.</span></span> <span data-ttu-id="aaf64-121">예를 들어 hello 작업을 효율적으로 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-121">For example, you can perform hello following tasks efficiently:</span></span>

* <span data-ttu-id="aaf64-122">Azure Cosmos DB에 저장된 데이터를 사용하여 캐시, 검색 인덱스 또는 데이터 웨어하우스를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-122">Update a cache, search index, or a data warehouse with data stored in Azure Cosmos DB.</span></span>
* <span data-ttu-id="aaf64-123">응용 프로그램 수준 데이터 계층화 및 보관 구현, 즉, Azure Cosmos DB에서 "핫 데이터를" 저장 하 고 너무 "콜드 데이터 를" age[Azure Blob 저장소](../storage/common/storage-introduction.md) 또는 [Azure 데이터 레이크 저장소](../data-lake-store/data-lake-store-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-123">Implement application-level data tiering and archival, that is, store "hot data" in Azure Cosmos DB, and age out "cold data" too[Azure Blob Storage](../storage/common/storage-introduction.md) or [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md).</span></span>
* <span data-ttu-id="aaf64-124">[Apache Hadoop](run-hadoop-with-hdinsight.md)를 사용하여 데이터에 대한 Batch 분석을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-124">Implement batch analytics on data using [Apache Hadoop](run-hadoop-with-hdinsight.md).</span></span>
* <span data-ttu-id="aaf64-125">Azure Cosmos DB를 사용하여 [Azure의 람다 파이프라인](https://blogs.technet.microsoft.com/msuspartner/2016/01/27/azure-partner-community-big-data-advanced-analytics-and-lambda-architecture/)을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-125">Implement [lambda pipelines on Azure](https://blogs.technet.microsoft.com/msuspartner/2016/01/27/azure-partner-community-big-data-advanced-analytics-and-lambda-architecture/) with Azure Cosmos DB.</span></span> <span data-ttu-id="aaf64-126">Azure Cosmos DB는 수집 및 쿼리를 모두 처리할 수 있는 확장성이 뛰어난 데이터베이스 솔루션을 제공하고 TCO가 낮은 람다 아키텍처를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-126">Azure Cosmos DB provides a scalable database solution that can handle both ingestion and query, and implement lambda architectures with low TCO.</span></span> 
* <span data-ttu-id="aaf64-127">0 가동 중지 시간이 마이그레이션 tooanother Azure Cosmos DB 계정과 다른 파티션 구성표를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-127">Perform zero down-time migrations tooanother Azure Cosmos DB account with a different partitioning scheme.</span></span>

<span data-ttu-id="aaf64-128">**수집 및 쿼리에 Azure Cosmos DB를 사용하는 람다 파이프라인:**</span><span class="sxs-lookup"><span data-stu-id="aaf64-128">**Lambda Pipelines with Azure Cosmos DB for ingestion and query:**</span></span>

![수집 및 쿼리에 대한 Azure Cosmos DB 기반 람다 파이프라인](./media/change-feed/lambda.png)

<span data-ttu-id="aaf64-130">Azure Cosmos DB tooreceive를 사용 하 여 하 고 장치, 센서, 인프라 및 응용 프로그램에서 이벤트 데이터를 저장 하 고 이러한 이벤트를 처리 수와 실시간 [Azure 스트림 분석](../stream-analytics/stream-analytics-documentdb-output.md), [Apache Storm](../hdinsight/hdinsight-storm-overview.md), 또는 [Apache Spark](../hdinsight/hdinsight-apache-spark-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-130">You can use Azure Cosmos DB tooreceive and store event data from devices, sensors, infrastructure, and applications, and process these events in real-time with [Azure Stream Analytics](../stream-analytics/stream-analytics-documentdb-output.md), [Apache Storm](../hdinsight/hdinsight-storm-overview.md), or [Apache Spark](../hdinsight/hdinsight-apache-spark-overview.md).</span></span> 

<span data-ttu-id="aaf64-131">내에서 프로그램 [서버가 없는](http://azure.com/serverless) 웹 및 모바일 앱 푸시 알림 tootheir 장치 를사용하여보내는같은특정작업변경내용tooyour고객프로필,기본설정또는위치tootrigger같은추적이벤트수있습니다[Azure 함수](../azure-functions/functions-bindings-documentdb.md) 또는 [응용 프로그램 서비스](https://azure.microsoft.com/services/app-service/)합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-131">Within your [serverless](http://azure.com/serverless) web and mobile apps, you can track events such as changes tooyour customer's profile, preferences, or location tootrigger certain actions like sending push notifications tootheir devices using [Azure Functions](../azure-functions/functions-bindings-documentdb.md) or [App Services](https://azure.microsoft.com/services/app-service/).</span></span> <span data-ttu-id="aaf64-132">Azure Cosmos DB toobuild 게임을 사용 하는 경우 예를 들어 변경 피드 tooimplement 실시간 순위표 완료 게임에서 점수에 따라 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-132">If you're using Azure Cosmos DB toobuild a game, you can, for example, use change feed tooimplement real-time leaderboards based on scores from completed games.</span></span>

## <a name="how-change-feed-works-in-azure-cosmos-db"></a><span data-ttu-id="aaf64-133">Azure Cosmos DB에서 변경 피드의 작동 방식</span><span class="sxs-lookup"><span data-stu-id="aaf64-133">How change feed works in Azure Cosmos DB</span></span>
<span data-ttu-id="aaf64-134">Azure Cosmos DB hello 기능 tooincrementally 읽기 업데이트를 수행 해도 tooan Azure Cosmos DB 컬렉션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-134">Azure Cosmos DB provides hello ability tooincrementally read updates made tooan Azure Cosmos DB collection.</span></span> <span data-ttu-id="aaf64-135">이 변경 피드 hello 다음과 같은 속성에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-135">This change feed has hello following properties:</span></span>

* <span data-ttu-id="aaf64-136">변경 내용이 Azure Cosmos DB에서 지속되면 비동기적으로 처리될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-136">Changes are persistent in Azure Cosmos DB and can be processed asynchronously.</span></span>
* <span data-ttu-id="aaf64-137">컬렉션 내에서 변경 내용을 toodocuments hello 변경 피드 즉시 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-137">Changes toodocuments within a collection are available immediately in hello change feed.</span></span>
* <span data-ttu-id="aaf64-138">각 변경 tooa 문서 hello 변경 피드에 정확히 한 번만 표시 하 고 클라이언트 검사점 논리를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-138">Each change tooa document appears exactly once in hello change feed, and clients manage their checkpointing logic.</span></span> <span data-ttu-id="aaf64-139">hello 변경 피드 프로세서 라이브러리 자동 검사점을 설정 하 고 "최소 한 번" 의미 체계를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-139">hello change feed processor library provides automatic checkpointing and "at least once" semantics.</span></span>
* <span data-ttu-id="aaf64-140">지정된 된 문서에 대 한 유일한 hello 가장 최근의 변경 hello 변경 로그에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-140">Only hello most recent change for a given document is included in hello change log.</span></span> <span data-ttu-id="aaf64-141">중간 변경 내용을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-141">Intermediate changes may not be available.</span></span>
* <span data-ttu-id="aaf64-142">hello 변경 피드 내 각 파티션 키 값 수정 순서를 기준으로 정렬 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-142">hello change feed is sorted by order of modification within each partition key value.</span></span> <span data-ttu-id="aaf64-143">파티션 키 값에 보장된 순서가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-143">There is no guaranteed order across partition-key values.</span></span>
* <span data-ttu-id="aaf64-144">특정 시점에서 변경 내용을 동기화할 수 있습니다. 즉, 변경 내용을 사용할 수 있는 고정 데이터 보존 기간이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-144">Changes can be synchronized from any point-in-time, that is, there is no fixed data retention period for which changes are available.</span></span>
* <span data-ttu-id="aaf64-145">변경 내용은 파티션 키 범위에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-145">Changes are available in chunks of partition key ranges.</span></span> <span data-ttu-id="aaf64-146">이 기능을 동시에 여러 소비자/서버에서 처리 하는 광범위 한 모음 toobe의 변경 내용을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-146">This capability allows changes from large collections toobe processed in parallel by multiple consumers/servers.</span></span>
* <span data-ttu-id="aaf64-147">여러 개의 변경 피드를 동시에 hello에 동일한 응용 프로그램 요청 수 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-147">Applications can request for multiple change feeds simultaneously on hello same collection.</span></span>

<span data-ttu-id="aaf64-148">Azure Cosmos DB의 변경 피드는 모든 계정에 기본적으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-148">Azure Cosmos DB's change feed is enabled by default for all accounts.</span></span> <span data-ttu-id="aaf64-149">사용할 수 있습니다 프로그램 [프로 비전 된 처리량](request-units.md) 쓰기 지역 또는에 [영역을 읽을](distribute-data-globally.md) hello에서 tooread Azure Cosmos DB에서 다른 작업에서와 마찬가지로 피드를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-149">You can use your [provisioned throughput](request-units.md) in your write region or any [read region](distribute-data-globally.md) tooread from hello change feed, just like any other operation from Azure Cosmos DB.</span></span> <span data-ttu-id="aaf64-150">hello 변경 피드에 삽입 및 toodocuments hello 컬렉션 내에서 실행 한 업데이트 작업이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-150">hello change feed includes inserts and update operations made toodocuments within hello collection.</span></span> <span data-ttu-id="aaf64-151">삭제 대신 문서 내에서 "soft-delete" 플래그를 설정하여 삭제를 캡처할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-151">You can capture deletes by setting a "soft-delete" flag within your documents in place of deletes.</span></span> <span data-ttu-id="aaf64-152">또는 hello 통해 문서에 대 한 유한 만료 기간을 설정할 수 [TTL 기능](time-to-live.md)예: 24 시간 및 사용 하 여 hello 값에 대 한 해당 속성의 toocapture 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-152">Alternatively, you can set a finite expiration period for your documents via hello [TTL capability](time-to-live.md), for example, 24 hours and use hello value of that property toocapture deletes.</span></span> <span data-ttu-id="aaf64-153">이 솔루션을 hello TTL 만료 기간 보다 짧은 시간 간격 내 tooprocess 변경 내용이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-153">With this solution, you have tooprocess changes within a shorter time interval than hello TTL expiration period.</span></span> <span data-ttu-id="aaf64-154">hello 변경 피드 hello 문서 컬렉션 내에서 각 파티션 키 범위에 사용할 수 있으며 따라서 병렬 처리에 대 한 하나 이상의 소비자에서 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-154">hello change feed is available for each partition key range within hello document collection, and thus can be distributed across one or more consumers for parallel processing.</span></span> 

![Azure Cosmos DB 변경 피드의 분산 처리](./media/change-feed/changefeedvisual.png)

<span data-ttu-id="aaf64-156">클라이언트 코드에서 변경 피드를 구현하는 방법에는 몇 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-156">You have a few options in how you implement a change feed in your client code.</span></span> <span data-ttu-id="aaf64-157">다음 tooimplement이 hello Azure Cosmos DB REST API를 사용 하 여 변경 공급 hello 하 고 DocumentDB Sdk hello 하는 방법을 설명 하는 즉시 hello 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-157">hello sections that immediately follow describe how tooimplement hello change feed using hello Azure Cosmos DB REST API and hello DocumentDB SDKs.</span></span> <span data-ttu-id="aaf64-158">그러나.NET 응용 프로그램에 사용할 수 있는 권장 hello 새 [변경 피드 프로세서 라이브러리](#change-feed-processor) hello에서 이벤트를 처리 파티션 간에 읽기 변경 사항을 간소화 하 고에서 작업 하는 여러 스레드가 피드 변경 병렬 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-158">However, for .NET applications, we recommend using hello new [Change feed processor library](#change-feed-processor) for processing events from hello change feed as it simplifies reading changes across partitions and enables multiple threads working in parallel.</span></span> 

## <span data-ttu-id="aaf64-159"><a id="rest-apis"></a>REST API 및 DocumentDB Sdk hello 사용</span><span class="sxs-lookup"><span data-stu-id="aaf64-159"><a id="rest-apis"></a>Working with hello REST API and DocumentDB SDKs</span></span>
<span data-ttu-id="aaf64-160">Azure Cosmos DB에서는 **컬렉션**이라는 저장소 및 처리량의 탄력적인 컨테이너를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-160">Azure Cosmos DB provides elastic containers of storage and throughput called **collections**.</span></span> <span data-ttu-id="aaf64-161">확장성 및 성능을 위해 [파티션 키](partition-data.md)를 사용하여 컬렉션 내의 데이터를 논리적으로 그룹화합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-161">Data within collections is logically grouped using [partition keys](partition-data.md) for scalability and performance.</span></span> <span data-ttu-id="aaf64-162">Azure Cosmos DB에서는 ID(읽기/가져오기), 쿼리 및 읽기-피드(검색) 기준 조회를 포함하여 이 데이터에 액세스하기 위한 다양한 API를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-162">Azure Cosmos DB provides various APIs for accessing this data, including lookup by ID (Read/Get), query, and read-feeds (scans).</span></span> <span data-ttu-id="aaf64-163">hello 변경 피드 얻을 수 있습니다 두 개의 새 요청 헤더 toohello DocumentDB를 채워 `ReadDocumentFeed` API를 파티션 키 범위에서 동시에 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-163">hello change feed can be obtained by populating two new request headers toohello DocumentDB `ReadDocumentFeed` API, and can be processed in parallel across ranges of partition keys.</span></span>

### <a name="readdocumentfeed-api"></a><span data-ttu-id="aaf64-164">ReadDocumentFeed API</span><span class="sxs-lookup"><span data-stu-id="aaf64-164">ReadDocumentFeed API</span></span>
<span data-ttu-id="aaf64-165">ReadDocumentFeed의 작동 방식에 대해 간략하게 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-165">Let's take a brief look at how ReadDocumentFeed works.</span></span> <span data-ttu-id="aaf64-166">Azure Cosmos DB 지원 문서 hello 통해 컬렉션 내에서 피드를 읽는 `ReadDocumentFeed` API입니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-166">Azure Cosmos DB supports reading a feed of documents within a collection via hello `ReadDocumentFeed` API.</span></span> <span data-ttu-id="aaf64-167">예를 들어 hello 다음 요청 페이지를 반환 hello 구조로 문서 `serverlogs` 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-167">For example, hello following request returns a page of documents inside hello `serverlogs` collection.</span></span> 

    GET https://mydocumentdb.documents.azure.com/dbs/smalldb/colls/serverlogs HTTP/1.1
    x-ms-date: Tue, 22 Nov 2016 17:05:14 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dgo7JEogZDn6ritWhwc5hX%2fNTV4wwM1u9V2Is1H4%2bDRg%3d
    Cache-Control: no-cache
    x-ms-consistency-level: Strong
    User-Agent: Microsoft.Azure.Documents.Client/1.10.27.5
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: mydocumentdb.documents.azure.com

<span data-ttu-id="aaf64-168">Hello를 사용 하 여 결과 제한 될 수 있습니다 `x-ms-max-item-count` 머리글과 읽기와 hello 요청을 다시 제출 하 여 다시 시작할 수는 `x-ms-continuation` hello 이전 응답에서 헤더를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-168">Results can be limited by using hello `x-ms-max-item-count` header, and reads can be resumed by resubmitting hello request with a `x-ms-continuation` header returned in hello previous response.</span></span> <span data-ttu-id="aaf64-169">단일 클라이언트에서 수행되는 경우, `ReadDocumentFeed`는 전체 파티션의 결과를 순차적으로 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-169">When performed from a single client, `ReadDocumentFeed` iterates through results across partitions serially.</span></span> 

<span data-ttu-id="aaf64-170">**문서 피드의 순차적 읽기**</span><span class="sxs-lookup"><span data-stu-id="aaf64-170">**Serial read document feed**</span></span>

<span data-ttu-id="aaf64-171">지원 되는 hello 중 하나를 사용 하 여 문서의 hello 피드를 검색할 수도 있습니다 [Azure Cosmos DB Sdk](documentdb-sdk-dotnet.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-171">You can also retrieve hello feed of documents using one of hello supported [Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="aaf64-172">예를 들어 hello를 조각과 방법을 따르는 toouse hello [ReadDocumentFeedAsync 메서드](/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentfeedasync?view=azure-dotnet) .net에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-172">For example, hello following snippet shows how toouse hello [ReadDocumentFeedAsync method](/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentfeedasync?view=azure-dotnet) in .NET.</span></span>

```csharp
FeedResponse<dynamic> feedResponse = null;
do
{
    feedResponse = await client.ReadDocumentFeedAsync(collection, new FeedOptions { MaxItemCount = -1 });
}
while (feedResponse.ResponseContinuation != null);
```

### <a name="distributed-execution-of-readdocumentfeed"></a><span data-ttu-id="aaf64-173">ReadDocumentFeed의 분산 실행</span><span class="sxs-lookup"><span data-stu-id="aaf64-173">Distributed execution of ReadDocumentFeed</span></span>
<span data-ttu-id="aaf64-174">테라바이트 이상의 데이터를 포함하거나 대량의 업데이트를 수집하는 컬렉션의 경우, 단일 클라이언트 컴퓨터에서 읽기 피드를 순차적으로 실행하면 실용적이지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-174">For collections that contain terabytes of data or more, or ingest a large volume of updates, serial execution of read feed from a single client machine might not be practical.</span></span> <span data-ttu-id="aaf64-175">순서 toosupport 이러한 빅 데이터 시나리오, Azure Cosmos DB 제공 Api toodistribute `ReadDocumentFeed` 여러 클라이언트 판독기/소비자를 넘어선 투명 하 게 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-175">In order toosupport these big data scenarios, Azure Cosmos DB provides APIs toodistribute `ReadDocumentFeed` calls transparently across multiple client readers/consumers.</span></span> 

<span data-ttu-id="aaf64-176">**분산 읽기 문서 피드**</span><span class="sxs-lookup"><span data-stu-id="aaf64-176">**Distributed Read Document Feed**</span></span>

<span data-ttu-id="aaf64-177">증분 변경, Azure Cosmos DB tooprovide 확장성이 높은 처리 hello 변경 피드 파티션 키의 범위에 따라 API는 확장 모델을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-177">tooprovide scalable processing of incremental changes, Azure Cosmos DB supports a scale-out model for hello change feed API based on ranges of partition keys.</span></span>

* <span data-ttu-id="aaf64-178">`ReadPartitionKeyRanges` 호출을 수행하는 컬렉션에 대한 파티션 키 범위의 목록을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-178">You can obtain a list of partition key ranges for a collection performing a `ReadPartitionKeyRanges` call.</span></span> 
* <span data-ttu-id="aaf64-179">각 파티션 키 범위에 대해 수행할 수 있습니다는 `ReadDocumentFeed` 범위 내에서 파티션 키를 사용 하 여 tooread 문서.</span><span class="sxs-lookup"><span data-stu-id="aaf64-179">For each partition key range, you can perform a `ReadDocumentFeed` tooread documents with partition keys within that range.</span></span>

### <a name="retrieving-partition-key-ranges-for-a-collection"></a><span data-ttu-id="aaf64-180">컬렉션에 대한 파티션 키 범위 검색</span><span class="sxs-lookup"><span data-stu-id="aaf64-180">Retrieving partition key ranges for a collection</span></span>
<span data-ttu-id="aaf64-181">요청 hello 여 hello 파티션 키 범위를 검색할 수 있습니다 `pkranges` 컬렉션 내의 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-181">You can retrieve hello partition key ranges by requesting hello `pkranges` resource within a collection.</span></span> <span data-ttu-id="aaf64-182">예를 들어 hello 다음 요청 hello의 목록을 검색 hello에 대 한 파티션 키 범위 `serverlogs` 컬렉션:</span><span class="sxs-lookup"><span data-stu-id="aaf64-182">For example hello following request retrieves hello list of partition key ranges for hello `serverlogs` collection:</span></span>

    GET https://querydemo.documents.azure.com/dbs/bigdb/colls/serverlogs/pkranges HTTP/1.1
    x-ms-date: Tue, 15 Nov 2016 07:26:51 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dEConYmRgDExu6q%2bZ8GjfUGOH0AcOx%2behkancw3LsGQ8%3d
    x-ms-consistency-level: Session
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: querydemo.documents.azure.com

<span data-ttu-id="aaf64-183">이 요청 hello 다음 hello 파티션 키 범위에 대 한 메타 데이터를 포함 하는 응답을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-183">This request returns hello following response containing metadata about hello partition key ranges:</span></span>

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


<span data-ttu-id="aaf64-184">**키 범위 속성을 파티션**: 다음 표에 hello에 hello 메타 데이터 속성을 포함 하는 각 파티션 키 범위:</span><span class="sxs-lookup"><span data-stu-id="aaf64-184">**Partition key range properties**: Each partition key range includes hello metadata properties in hello following table:</span></span>

<table>
    <tr>
        <th><span data-ttu-id="aaf64-185">헤더 이름</span><span class="sxs-lookup"><span data-stu-id="aaf64-185">Header name</span></span></th>
        <th><span data-ttu-id="aaf64-186">설명</span><span class="sxs-lookup"><span data-stu-id="aaf64-186">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="aaf64-187">id</span><span class="sxs-lookup"><span data-stu-id="aaf64-187">id</span></span></td>
        <td>
            <p><span data-ttu-id="aaf64-188">hello 파티션 키 범위에 대 한 hello ID입니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-188">hello ID for hello partition key range.</span></span> <span data-ttu-id="aaf64-189">각 컬렉션 내에서 안정적이고 고유한 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-189">This is a stable and unique ID within each collection.</span></span></p>
            <p><span data-ttu-id="aaf64-190">파티션 키 범위 하 여 hello tooread 변경 내용을 호출 다음에 사용 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-190">Must be used in hello following call tooread changes by partition key range.</span></span></p>
        </td>
    </tr>
    <tr>
        <td><span data-ttu-id="aaf64-191">maxExclusive</span><span class="sxs-lookup"><span data-stu-id="aaf64-191">maxExclusive</span></span></td>
        <td><span data-ttu-id="aaf64-192">hello 파티션 키 범위에 대 한 hello 최대 파티션 키 해시 값입니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-192">hello maximum partition key hash value for hello partition key range.</span></span> <span data-ttu-id="aaf64-193">내부에 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-193">For internal use.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="aaf64-194">minInclusive</span><span class="sxs-lookup"><span data-stu-id="aaf64-194">minInclusive</span></span></td>
        <td><span data-ttu-id="aaf64-195">hello 파티션 키 범위에 대 한 hello 최소 파티션 키 해시 값입니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-195">hello minimum partition key hash value for hello partition key range.</span></span> <span data-ttu-id="aaf64-196">내부에 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-196">For internal use.</span></span></td>
    </tr>       
</table>

<span data-ttu-id="aaf64-197">지원 되는 hello 중 하나를 사용 하 여 수행할 수 있습니다 [Azure Cosmos DB Sdk](documentdb-sdk-dotnet.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-197">You can do this using one of hello supported [Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="aaf64-198">예를 들어 hello 다음 코드 조각에서는.net에서 tooretrieve 파티션 키 범위 하는 방법을 hello를 사용 하 여 [ReadPartitionKeyRangeFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readpartitionkeyrangefeedasync?view=azure-dotnet) 메서드.</span><span class="sxs-lookup"><span data-stu-id="aaf64-198">For example, hello following snippet shows how tooretrieve partition key ranges in .NET using hello [ReadPartitionKeyRangeFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readpartitionkeyrangefeedasync?view=azure-dotnet) method.</span></span>

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

<span data-ttu-id="aaf64-199">선택적 설정 hello 하 여 파티션 키 범위 당 문서를 검색할 수 있도록 azure Cosmos DB `x-ms-documentdb-partitionkeyrangeid` 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-199">Azure Cosmos DB supports retrieval of documents per partition key range by setting hello optional `x-ms-documentdb-partitionkeyrangeid` header.</span></span> 

### <a name="performing-an-incremental-readdocumentfeed"></a><span data-ttu-id="aaf64-200">증분 ReadDocumentFeed 수행</span><span class="sxs-lookup"><span data-stu-id="aaf64-200">Performing an incremental ReadDocumentFeed</span></span>
<span data-ttu-id="aaf64-201">ReadDocumentFeed는 시나리오/의 Azure Cosmos DB 컬렉션의 변경 내용 증분 처리에 대 한 작업을 수행 하는 hello를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-201">ReadDocumentFeed supports hello following scenarios/tasks for incremental processing of changes in Azure Cosmos DB collections:</span></span>

* <span data-ttu-id="aaf64-202">모든 읽기 컬렉션 만들기에서 hello부터 toodocuments 즉, 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-202">Read all changes toodocuments from hello beginning, that is, from collection creation.</span></span>
* <span data-ttu-id="aaf64-203">모든 읽기 사용자가 지정한 시간 이후에 현재 시간 또는 변경 내용을 toofuture 업데이트 toodocuments를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-203">Read all changes toofuture updates toodocuments from current time, or any changes since a user-specified time.</span></span>
* <span data-ttu-id="aaf64-204">모든 읽기 hello 컬렉션 (ETag)의 논리적 버전에서 toodocuments를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-204">Read all changes toodocuments from a logical version of hello collection (ETag).</span></span> <span data-ttu-id="aaf64-205">소비자 기반 증분 피드 읽기 요청에서 ETag를 반환 하는 hello로 검사점을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-205">You can checkpoint your consumers based on hello returned ETag from incremental read-feed requests.</span></span>

<span data-ttu-id="aaf64-206">hello 변경 내용에는 삽입 및 업데이트 toodocuments를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-206">hello changes include inserts and updates toodocuments.</span></span> <span data-ttu-id="aaf64-207">toocapture 삭제 되 면 문서, 내에서 "소프트 삭제" 속성을 사용 하거나 hello를 사용 하 여 [기본 제공 TTL 속성](time-to-live.md) toosignal hello에 보류 중인 삭제 피드를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-207">toocapture deletes, you must use a "soft delete" property within your documents, or use hello [built-in TTL property](time-to-live.md) toosignal a pending deletion in hello change feed.</span></span>

<span data-ttu-id="aaf64-208">다음 테이블 목록 hello hello [요청](/rest/api/documentdb/common-documentdb-rest-request-headers.md) 및 [응답 헤더](/rest/api/documentdb/common-documentdb-rest-response-headers.md) ReadDocumentFeed 작업에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-208">hello following table lists hello [request](/rest/api/documentdb/common-documentdb-rest-request-headers.md) and [response headers](/rest/api/documentdb/common-documentdb-rest-response-headers.md) for ReadDocumentFeed operations.</span></span>

<span data-ttu-id="aaf64-209">**증분 ReadDocumentFeed에 대한 요청 헤더**:</span><span class="sxs-lookup"><span data-stu-id="aaf64-209">**Request headers for incremental ReadDocumentFeed**:</span></span>

<table>
    <tr>
        <th><span data-ttu-id="aaf64-210">헤더 이름</span><span class="sxs-lookup"><span data-stu-id="aaf64-210">Header name</span></span></th>
        <th><span data-ttu-id="aaf64-211">설명</span><span class="sxs-lookup"><span data-stu-id="aaf64-211">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="aaf64-212">A-IM</span><span class="sxs-lookup"><span data-stu-id="aaf64-212">A-IM</span></span></td>
        <td><span data-ttu-id="aaf64-213">설정 해야 너무 "증분 피드" 그렇지 않으면 생략 하거나</span><span class="sxs-lookup"><span data-stu-id="aaf64-213">Must be set too"Incremental feed", or omitted otherwise</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="aaf64-214">If-None-Match</span><span class="sxs-lookup"><span data-stu-id="aaf64-214">If-None-Match</span></span></td>
        <td>
            <p><span data-ttu-id="aaf64-215">머리글이 없음: (컬렉션 생성)를 시작 하는 hello에서 모든 변경 내용을 반환</span><span class="sxs-lookup"><span data-stu-id="aaf64-215">No header: returns all changes from hello beginning (collection creation)</span></span></p>
            <p><span data-ttu-id="aaf64-216">"*": hello 컬렉션 내에서 모든 새 변경 내용을 toodata 반환</span><span class="sxs-lookup"><span data-stu-id="aaf64-216">"*": returns all new changes toodata within hello collection</span></span></p>         
            <p><span data-ttu-id="aaf64-217">&lt;etag&gt;: 경우 ETag tooa 컬렉션 설정, 해당 논리 타임 스탬프 이후 모든 변경 내용을 반환</span><span class="sxs-lookup"><span data-stu-id="aaf64-217">&lt;etag&gt;: If set tooa collection ETag, returns all changes made since that logical timestamp</span></span></p>
        </td>
    </tr>
    <tr>    
        <td><span data-ttu-id="aaf64-218">If-Modified-Since</span><span class="sxs-lookup"><span data-stu-id="aaf64-218">If-Modified-Since</span></span></td> 
        <td><span data-ttu-id="aaf64-219">RFC 1123 시간 형식: If-None-Match가 지정된 경우 무시합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-219">RFC 1123 time format; ignored if If-None-Match is specified</span></span></td> 
    </tr> 
    <tr>
        <td><span data-ttu-id="aaf64-220">x-ms-documentdb-partitionkeyrangeid</span><span class="sxs-lookup"><span data-stu-id="aaf64-220">x-ms-documentdb-partitionkeyrangeid</span></span></td>
        <td><span data-ttu-id="aaf64-221">데이터를 읽기 위한 hello 파티션 키 범위 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-221">hello partition key range ID for reading data.</span></span></td>
    </tr>
</table>

<span data-ttu-id="aaf64-222">**증분 ReadDocumentFeed에 대한 응답 헤더**:</span><span class="sxs-lookup"><span data-stu-id="aaf64-222">**Response headers for incremental ReadDocumentFeed**:</span></span>

<table> <tr>
        <th><span data-ttu-id="aaf64-223">헤더 이름</span><span class="sxs-lookup"><span data-stu-id="aaf64-223">Header name</span></span></th>
        <th><span data-ttu-id="aaf64-224">설명</span><span class="sxs-lookup"><span data-stu-id="aaf64-224">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="aaf64-225">etag</span><span class="sxs-lookup"><span data-stu-id="aaf64-225">etag</span></span></td>
        <td>
            <p><span data-ttu-id="aaf64-226">hello 논리적 시퀀스 번호 (LSN) hello 응답에서 반환 된 마지막 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-226">hello logical sequence number (LSN) of last document returned in hello response.</span></span></p>
            <p><span data-ttu-id="aaf64-227">증분 ReadDocumentFeed는 If-None-Match에서 이 값을 다시 제출하여 다시 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-227">Incremental ReadDocumentFeed can be resumed by resubmitting this value in If-None-Match.</span></span></p>
        </td>
    </tr>
</table>

<span data-ttu-id="aaf64-228">다음 샘플 요청 tooreturn은 hello 논리 버전/ETag에서 컬렉션의 모든 증분 변경 내용을 `28535` 키 범위를 분할 하 고 = `16`:</span><span class="sxs-lookup"><span data-stu-id="aaf64-228">Here's a sample request tooreturn all incremental changes in collection from hello logical version/ETag `28535` and partition key range = `16`:</span></span>

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

<span data-ttu-id="aaf64-229">변경 내용은 hello 파티션 키 범위 내에서 각 파티션 키 값에서 시간으로 정렬 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-229">Changes are ordered by time within each partition key value within hello partition key range.</span></span> <span data-ttu-id="aaf64-230">파티션 키 값에 보장된 순서가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-230">There is no guaranteed order across partition-key values.</span></span> <span data-ttu-id="aaf64-231">단일 페이지에 포함할 수 있는 것 보다 많은 결과가 있으면 hello로 hello 요청을 다시 제출 하 여 hello 결과의 다음 페이지를 읽을 수 있습니다 `If-None-Match` 값 같은 toohello 헤더 `etag` hello 이전 응답에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-231">If there are more results than can fit in a single page, you can read hello next page of results by resubmitting hello request with hello `If-None-Match` header with value equal toohello `etag` from hello previous response.</span></span> <span data-ttu-id="aaf64-232">여러 문서 삽입 되거나 저장된 프로시저 또는 트리거 내에서 트랜잭션 방식으로 업데이트 된 경우 모두 반환 됩니다 hello 내에서 동일한 응답 페이지.</span><span class="sxs-lookup"><span data-stu-id="aaf64-232">If multiple documents were inserted or updated transactionally within a stored procedure or trigger, they will all be returned within hello same response page.</span></span>

> [!NOTE]
> <span data-ttu-id="aaf64-233">변경 피드를 사용 더 많은 항목에 지정 된 버전과 페이지에 반환 될 수 있습니다 `x-ms-max-item-count` 삽입 되거나 업데이트 저장된 프로시저 내의 여러 문서의 경우 hello 또는 트리거.</span><span class="sxs-lookup"><span data-stu-id="aaf64-233">With change feed, you might get more items returned in a page than specified in `x-ms-max-item-count` in hello case of multiple documents inserted or updated inside a stored procedures or triggers.</span></span> 

<span data-ttu-id="aaf64-234">Hello.NET SDK (1.17.0)를 사용할 때는 hello 필드 설정 `StartTime` 에 `ChangeFeedOptions` 이후 변경 toodirectly 반환 문서 `StartTime` 를 호출할 때 `CreateDocumentChangeFeedQuery`합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-234">When using hello .NET SDK (1.17.0), set hello field `StartTime` in `ChangeFeedOptions` toodirectly return changed documents since `StartTime` when calling  `CreateDocumentChangeFeedQuery`.</span></span> <span data-ttu-id="aaf64-235">지정 하 여 `If-Modified-Since` hello REST API를 사용 하 여 요청은 문서를 반환 하지 hello 자체 하지만 대신 hello 연속 토큰 또는 `etag` hello 응답 헤더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-235">By specifying `If-Modified-Since` using hello REST API, your request will return not hello documents themselves, but rather hello continuation token or `etag` in hello response header.</span></span> <span data-ttu-id="aaf64-236">시간, hello continuation 토큰을 지정 하는 수정 된 hello tooreturn hello 문서 `etag` hello 다음 요청에 사용 해야 합니다 `If-None-Match` tooreturn hello 실제 문서.</span><span class="sxs-lookup"><span data-stu-id="aaf64-236">tooreturn hello documents modified hello specified time, hello continuation token `etag` must then be used in hello next request with `If-None-Match` tooreturn hello actual documents.</span></span> 

<span data-ttu-id="aaf64-237">.NET SDK hello 제공 hello [CreateDocumentChangeFeedQuery](/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery?view=azure-dotnet) 및 [ChangeFeedOptions](/dotnet/api/microsoft.azure.documents.client.changefeedoptions?view=azure-dotnet) 도우미 클래스가 tooaccess 변경한 tooa 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-237">hello .NET SDK provides hello [CreateDocumentChangeFeedQuery](/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery?view=azure-dotnet) and [ChangeFeedOptions](/dotnet/api/microsoft.azure.documents.client.changefeedoptions?view=azure-dotnet) helper classes tooaccess changes made tooa collection.</span></span> <span data-ttu-id="aaf64-238">hello 다음 코드 조각은 변경 내역을 보여 tooretrieve 모든 단일 클라이언트에서.NET SDK hello를 사용 하 여 hello부터에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-238">hello following snippet shows how tooretrieve all changes from hello beginning using hello .NET SDK from a single client.</span></span>

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
<span data-ttu-id="aaf64-239">Hello 다음 코드 조각은 변경 내역을 보여 tooprocess 실시간 및 hello 변경 사용 하 여 Azure Cosmos DB와 함께 지원 피드 및 hello 함수 앞에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-239">And hello following snippet shows how tooprocess changes in real-time with Azure Cosmos DB by using hello change feed support and hello preceding function.</span></span> <span data-ttu-id="aaf64-240">hello 첫 번째 호출이 hello 컬렉션의 모든 hello 문서를 반환 하 고 hello 둘째만 hello hello 마지막 검사점 이후 생성 된 만든 두 문서</span><span class="sxs-lookup"><span data-stu-id="aaf64-240">hello first call returns all hello documents in hello collection, and hello second only returns hello two documents created that were created since hello last checkpoint.</span></span>

```csharp
// Returns all documents in hello collection.
Dictionary<string, string> checkpoints = await GetChanges(client, collection, new Dictionary<string, string>());

await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-201", MetricType = "Temperature", Unit = "Celsius", MetricValue = 1000 });
await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-212", MetricType = "Pressure", Unit = "psi", MetricValue = 1000 });

// Returns only hello two documents created above.
checkpoints = await GetChanges(client, collection, checkpoints);
```

<span data-ttu-id="aaf64-241">클라이언트 쪽 논리 tooselectively 프로세스 이벤트를 사용 하 여 hello 변경 공급을 필터링 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-241">You can also filter hello change feed using client side logic tooselectively process events.</span></span> <span data-ttu-id="aaf64-242">예를 들어 다음은 장치 센서의 온도 변경 이벤트에만 클라이언트 쪽 LINQ tooprocess를 사용 하는 조각입니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-242">For example, here's a snippet that uses client side LINQ tooprocess only temperature change events from device sensors.</span></span>

```csharp
FeedResponse<DeviceReading> readChangesResponse = query.ExecuteNextAsync<DeviceReading>().Result;

foreach (DeviceReading changedDocument in 
    readChangesResponse.AsEnumerable().Where(d => d.MetricType == "Temperature" && d.MetricValue > 1000L))
{
    // trigger an action, like call an API
}
```

## <span data-ttu-id="aaf64-243"><a id="change-feed-processor"></a>변경 피드 프로세서 라이브러리</span><span class="sxs-lookup"><span data-stu-id="aaf64-243"><a id="change-feed-processor"></a>Change Feed Processor library</span></span>
<span data-ttu-id="aaf64-244">두 번째 방법은 toouse hello [Azure Cosmos DB 변경 피드 프로세서 라이브러리](https://docs.microsoft.com/azure/cosmos-db/documentdb-sdk-dotnet-changefeed)를 쉽게 이벤트 여러 소비자에서 피드는 변경 내용으로 인해 처리를 배포 하면 도움이 될 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-244">Another option is toouse hello [Azure Cosmos DB Change Feed Processor library](https://docs.microsoft.com/azure/cosmos-db/documentdb-sdk-dotnet-changefeed), which can help you easily distribute event processing from a change feed across multiple consumers.</span></span> <span data-ttu-id="aaf64-245">hello 라이브러리는 변경 판독기 hello.NET 플랫폼에서 피드를 구축 하기 위한 훌륭한입니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-245">hello library is great for building change feed readers on hello .NET platform.</span></span> <span data-ttu-id="aaf64-246">Hello에 포함 된 hello 메서드를 통해 hello 프로세서 피드 교환 라이브러리를 사용 하 여 단순화 하는 일부 워크플로 다른 Cosmos DB Sdk를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-246">Some workflows that would be simplified by using hello Change Feed Processor library over hello methods included in hello other Cosmos DB SDKs include:</span></span> 

* <span data-ttu-id="aaf64-247">데이터가 여러 파티션에 저장되어 있는 경우, 변경 피드에서 업데이트 풀링</span><span class="sxs-lookup"><span data-stu-id="aaf64-247">Pulling updates from change feed when data is stored across multiple partitions</span></span>
* <span data-ttu-id="aaf64-248">이동 하거나 컬렉션을 하나 tooanother에서 데이터 복제</span><span class="sxs-lookup"><span data-stu-id="aaf64-248">Moving or replicating data from one collection tooanother</span></span>
* <span data-ttu-id="aaf64-249">업데이트 toodata가 트리거하는 작업 및 변경 피드의 병렬 실행</span><span class="sxs-lookup"><span data-stu-id="aaf64-249">Parallel execution of actions triggered by updates toodata and change feed</span></span> 

<span data-ttu-id="aaf64-250">Hello Cosmos Sdk의에서 Api hello를 사용 하 여 정확한 액세스 toochange 파티션마다에서 업데이트 피드 제공 하며, hello 프로세서 피드 교환 라이브러리를 사용 하 여 변경 내용을 읽는 파티션과 병렬로 작동 하는 여러 스레드 간에 간단해 집니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-250">While using hello APIs in hello Cosmos SDKs provides precise access toochange feed updates in each partition, using hello Change Feed Processor library simplifies reading changes across partitions and multiple threads working in parallel.</span></span> <span data-ttu-id="aaf64-251">수동으로 각 컨테이너에서 변경 내용을 읽는 각 파티션에 대 한 연속 토큰을 저장 하는 대신 hello 프로세서 피드 교환 임대 메커니즘을 사용 하 여 파티션 간에 읽기 변경 내용을 자동으로 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-251">Instead of manually reading changes from each container and saving a continuation token for each partition, hello Change Feed Processor automatically manages reading changes across partitions using a lease mechanism.</span></span>

<span data-ttu-id="aaf64-252">hello 라이브러리는 NuGet 패키지로 사용할 수 있는: [Microsoft.Azure.Documents.ChangeFeedProcessor](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/) Github로 소스 코드와 [샘플](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/ChangeFeedProcessor)합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-252">hello library is available as a NuGet Package: [Microsoft.Azure.Documents.ChangeFeedProcessor](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/) and from source code as a Github [sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/ChangeFeedProcessor).</span></span> 

### <a name="understanding-change-feed-processor-library"></a><span data-ttu-id="aaf64-253">변경 피드 프로세서 라이브러리의 이해</span><span class="sxs-lookup"><span data-stu-id="aaf64-253">Understanding Change Feed Processor library</span></span> 

<span data-ttu-id="aaf64-254">네 가지 주요 요소가 hello 프로세서 피드 교환 구현의: hello 컬렉션, hello 임대 컬렉션, hello 프로세서 호스트 및 hello 소비자를 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-254">There are four main components of implementing hello Change Feed Processor: hello monitored collection, hello lease collection, hello processor host, and hello consumers.</span></span> 

<span data-ttu-id="aaf64-255">**모니터링 대상된 컬렉션:** 모니터링 hello 컬렉션이 hello 데이터는 hello에서 변경 피드가 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-255">**Monitored Collection:** hello monitored collection is hello data from which hello change feed is generated.</span></span> <span data-ttu-id="aaf64-256">모든 삽입 및 변경 내용을 모니터링 toohello 컬렉션 hello 컬렉션의 변경 피드 hello에에서 반영 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-256">Any inserts and changes toohello monitored collection are reflected in hello change feed of hello collection.</span></span> 

<span data-ttu-id="aaf64-257">**임대 수집:** hello 임대 컬렉션 좌표 여러 작업자 간에 피드 hello 변경 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-257">**Lease Collection:** hello lease collection coordinates processing hello change feed across multiple workers.</span></span> <span data-ttu-id="aaf64-258">별도 컬렉션은 사용 되는 toostore hello 임대 파티션당 1 개씩 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-258">A separate collection is used toostore hello leases with one lease per partition.</span></span> <span data-ttu-id="aaf64-259">유리 toostore hello로 다른 계정에이 임대 수집 쓰기 지역 자세히 toowhere hello 변경 피드 프로세서가 실행 중인 경우</span><span class="sxs-lookup"><span data-stu-id="aaf64-259">It is advantageous toostore this lease collection on a different account with hello write region closer toowhere hello Change Feed Processor is running.</span></span> <span data-ttu-id="aaf64-260">임대 개체 특성을 다음 hello를 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-260">A lease object contains hello following attributes:</span></span> 
* <span data-ttu-id="aaf64-261">소유자: hello 임대를 소유 하는 hello 호스트를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-261">Owner: Specifies hello host that owns hello lease</span></span>
* <span data-ttu-id="aaf64-262">특정 파티션에 대 한 피드 hello 변경에 hello 위치 (연속 토큰)를 지정 하는 연속 작업:</span><span class="sxs-lookup"><span data-stu-id="aaf64-262">Continuation: Specifies hello position (continuation token) in hello change feed for a particular partition</span></span>
* <span data-ttu-id="aaf64-263">타임 스탬프: 임대 업데이트 된 시간입니다. hello 타임 스탬프 hello 임대가 만료 된 것으로 간주 됩니다 여부를 사용 하는 toocheck 될 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="aaf64-263">Timestamp: Last time lease was updated; hello timestamp can be used toocheck whether hello lease is considered expired</span></span> 

<span data-ttu-id="aaf64-264">**프로세서 호스트:** 각 호스트 호스트의 다른 인스턴스를 개수에 활성 임대가 기준으로 파티션을 tooprocess 개수를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-264">**Processor Host:** Each host determines how many partitions tooprocess based on how many other instances of hosts have active leases.</span></span> 
1.  <span data-ttu-id="aaf64-265">호스트 시작 되 면 모든 호스트에 걸쳐 임대 toobalance hello 작업 부하를 획득 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-265">When a host starts up, it acquires leases toobalance hello workload across all hosts.</span></span> <span data-ttu-id="aaf64-266">호스트는 임대가 활성 상태로 유지되도록 주기적으로 임대를 갱신합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-266">A host periodically renews leases, so leases remain active.</span></span> 
2.  <span data-ttu-id="aaf64-267">호스트 검사점 hello 마지막 연속 토큰 tooits 임대 각 읽기에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-267">A host checkpoints hello last continuation token tooits lease for each read.</span></span> <span data-ttu-id="aaf64-268">tooensure 동시성 안전 호스트 각 임대 업데이트에 대 한 hello ETag를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-268">tooensure concurrency safety, a host checks hello ETag for each lease update.</span></span> <span data-ttu-id="aaf64-269">다른 검사점 전략도 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-269">Other checkpoint strategies are also supported.</span></span>  
3.  <span data-ttu-id="aaf64-270">종료, 모든 임대를 해제 하는 호스트 않고 유지 hello 연속 정보 나중 hello 저장 된 검사점에서 읽기를 다시 시작할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-270">Upon shutdown, a host releases all leases but keeps hello continuation information, so it can resume reading from hello stored checkpoint later.</span></span> 

<span data-ttu-id="aaf64-271">이 이번에 hello 호스트 수가 파티션 (임대) hello 수보다 클 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-271">At this time hello number of hosts cannot be greater than hello number of partitions (leases).</span></span>

<span data-ttu-id="aaf64-272">**소비자가:** 소비자나 작업자는 각 호스트에 의해 시작 된 처리 피드 hello 변경을 수행 하는 스레드입니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-272">**Consumers:** Consumers, or workers, are threads that perform hello change feed processing initiated by each host.</span></span> <span data-ttu-id="aaf64-273">각 프로세서 호스트에는 여러 소비자가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-273">Each processor host can have multiple consumers.</span></span> <span data-ttu-id="aaf64-274">각 소비자가 읽는 hello 변경 피드 hello에서 tooand 할당 된 파티션 변경의 해당 호스트에 알립니다 및 만료 된 임대 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-274">Each consumer reads hello change feed from hello partition it is assigned tooand notifies its host of changes and expired leases.</span></span>

<span data-ttu-id="aaf64-275">toofurther 변경 피드 프로세서의 이러한 4 개의 요소를 함께 작동을 hello 다이어그램을 다음의 예제를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-275">toofurther understand how these four elements of Change Feed Processor work together, let's look at an example in hello following diagram.</span></span> <span data-ttu-id="aaf64-276">hello는 컬렉션 저장소 문서를 모니터링 하 고 hello 파티션 키로 hello "city"를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-276">hello monitored collection stores documents and uses hello "city" as hello partition key.</span></span> <span data-ttu-id="aaf64-277">파란색 hello 파티션 포함 "E" hello "city" 필드를 사용 하 여 문서에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-277">We see that hello blue partition contains documents with hello "city" field from "A-E" and so on.</span></span> <span data-ttu-id="aaf64-278">각각 4 hello 파티션을 병렬로 읽는 두 소비자와 함께 두 호스트 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-278">There are two hosts, each with two consumers reading from hello four partitions in parallel.</span></span> <span data-ttu-id="aaf64-279">hello 화살표 hello의 특정 지점에서 읽는 hello 소비자 변경 피드를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-279">hello arrows show hello consumers reading from a specific spot in hello change feed.</span></span> <span data-ttu-id="aaf64-280">Hello 첫 번째 파티션에 hello 어두운 파란색 hello 연한 파랑은 hello 변경 피드에 변경 내용을 이미 파악 하는 hello 읽지 않은 변경 내용을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-280">In hello first partition, hello darker blue represents unread changes while hello light blue represents hello already read changes on hello change feed.</span></span> <span data-ttu-id="aaf64-281">hello 호스트 hello 임대 컬렉션 toostore "연속" 값 tookeep 트랙의 각 소비자에 대 한 위치를 읽는 현재 hello 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-281">hello hosts use hello lease collection toostore a "continuation" value tookeep track of hello current reading position for each consumer.</span></span> 

![프로세서 호스트 피드 hello Azure Cosmos DB 변경 사용](./media/change-feed/changefeedprocessornew.png)

### <a name="using-change-feed-processor-library"></a><span data-ttu-id="aaf64-283">변경 피드 프로세서 라이브러리 사용</span><span class="sxs-lookup"><span data-stu-id="aaf64-283">Using Change Feed Processor Library</span></span> 
<span data-ttu-id="aaf64-284">다음 단원을 hello toouse 소스 컬렉션 tooa 대상 컬렉션에서 변경 내용 복제의 hello 컨텍스트에서 변경 내용 피드 처리기 라이브러리 hello 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-284">hello following section explains how toouse hello Change Feed Processor library in hello context of replicating changes from a source collection tooa destination collection.</span></span> <span data-ttu-id="aaf64-285">여기서 hello 소스 컬렉션은 변경 피드 프로세서에서 모니터링 하는 hello 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-285">Here, hello source collection is hello monitored collection in Change Feed Processor.</span></span> 

<span data-ttu-id="aaf64-286">**설치 하 고 hello 변경 피드 프로세서 NuGet 패키지를 포함 합니다.**</span><span class="sxs-lookup"><span data-stu-id="aaf64-286">**Install and include hello Change Feed Processor NuGet package**</span></span> 

<span data-ttu-id="aaf64-287">변경 피드 프로세서 NuGet 패키지를 설치하기 전에 먼저 다음을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-287">Before installing Change Feed Processor NuGet Package, first install:</span></span> 
* <span data-ttu-id="aaf64-288">Microsoft.Azure.DocumentDB, 버전 1.13.1 이상</span><span class="sxs-lookup"><span data-stu-id="aaf64-288">Microsoft.Azure.DocumentDB, version 1.13.1 or above</span></span> 
* <span data-ttu-id="aaf64-289">Newtonsoft.Json, 9.0.1 버전 이상 `Microsoft.Azure.DocumentDB.ChangeFeedProcessor` 설치 및 참조로 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-289">Newtonsoft.Json, version 9.0.1 or above Install `Microsoft.Azure.DocumentDB.ChangeFeedProcessor` and include it as a reference.</span></span>

<span data-ttu-id="aaf64-290">**모니터링되는 컬렉션, 임대 및 대상 컬렉션 만들기**</span><span class="sxs-lookup"><span data-stu-id="aaf64-290">**Create a monitored, lease and destination collection**</span></span> 

<span data-ttu-id="aaf64-291">순서 toouse hello 프로세서 라이브러리 피드 변경, hello 임대 컬렉션 hello 프로세서 호스트를 실행 하기 전에 만든 toobe 제공 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-291">In order toouse hello Change Feed Processor Library, hello lease collection needs toobe created before running hello processor host(s).</span></span> <span data-ttu-id="aaf64-292">다시 임대 컬렉션 변경 피드 프로세서에서 실행 되 고 쓰기 지역 자세히 toowhere hello로 다른 계정에 저장 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-292">Again, we recommend storing a lease collection on a different account with a write region closer toowhere hello Change Feed Processor is running.</span></span> <span data-ttu-id="aaf64-293">이 예에서 데이터 이동 toocreate hello 대상 컬렉션 hello 프로세서 피드 교환 호스트를 실행 하기 전에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-293">In this data movement example, we need toocreate hello destination collection before running hello Change Feed Processor host.</span></span> <span data-ttu-id="aaf64-294">Hello 샘플 코드에서 지속적으로 모니터링 하는 도우미 메서드 toocreate hello 이라고 임대 및 존재 하지 않을 경우 대상 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-294">In hello sample code we call a helper method toocreate hello monitored, leased, and destination collections if they do not already exist.</span></span> 

> [!WARNING]
> <span data-ttu-id="aaf64-295">컬렉션을 만드는 영향을 줍니다 가격의 Azure Cosmos DB와 함께 응용 프로그램 toocommunicate hello에 대 한 처리량을 예약 하는.</span><span class="sxs-lookup"><span data-stu-id="aaf64-295">Creating a collection has pricing implications, as you are reserving throughput for hello application toocommunicate with Azure Cosmos DB.</span></span> <span data-ttu-id="aaf64-296">자세한 내용은 hello를 방문 하세요 [가격 책정 페이지](https://azure.microsoft.com/pricing/details/cosmos-db/)</span><span class="sxs-lookup"><span data-stu-id="aaf64-296">For more details, please visit hello [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/)</span></span>
> 
> 

<span data-ttu-id="aaf64-297">*프로세서 호스트 만들기*</span><span class="sxs-lookup"><span data-stu-id="aaf64-297">*Creating a processor host*</span></span>

<span data-ttu-id="aaf64-298">hello `ChangeFeedProcessorHost` 클래스는 검사점 설정 및 파티션 임대 관리 기능도 제공 하는 이벤트 프로세서 구현을 스레드로부터 안전한, 다중 프로세스, 안전한 런타임 환경을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-298">hello `ChangeFeedProcessorHost` class provides a thread-safe, multi-process, safe runtime environment for event processor implementations that also provides checkpointing and partition lease management.</span></span> <span data-ttu-id="aaf64-299">toouse hello `ChangeFeedProcessorHost` 클래스를 구현할 수 있습니다 `IChangeFeedObserver`합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-299">toouse hello `ChangeFeedProcessorHost` class, you can implement `IChangeFeedObserver`.</span></span> <span data-ttu-id="aaf64-300">이 인터페이스는 세 가지 메서드가 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-300">This interface contains three methods:</span></span>

* <span data-ttu-id="aaf64-301">`OpenAsync`: 이 함수는 변경 피드 관찰자를 열 때 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-301">`OpenAsync`: This function is called when change feed observer is opened.</span></span> <span data-ttu-id="aaf64-302">소비자/관찰자를 열 때 수정 된 tooperform 특정 작업을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-302">It can be modified tooperform a specific action when consumer/observer is opened.</span></span>  
* <span data-ttu-id="aaf64-303">`CloseAsync`: 이 함수는 변경 피드 관찰자를 종료할 때 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-303">`CloseAsync`: This function is called when change feed observer is terminated.</span></span> <span data-ttu-id="aaf64-304">소비자/관찰자를 닫으면 수정 된 tooperform 특정 작업을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-304">It can be modified tooperform a specific action when consumer/observer is closed.</span></span>  
* <span data-ttu-id="aaf64-305">`ProcessChangesAsync`: 이 함수는 변경 피드에서 문서의 새로운 변경 내용을 사용할 수 있을 때 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-305">`ProcessChangesAsync`: This function is called when document new changes are available on change feed.</span></span> <span data-ttu-id="aaf64-306">수정 된 tooperform 모든 피드 변경 업데이트할 때 특정 작업을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-306">It can be modified tooperform a specific action upon every change feed update.</span></span>  

<span data-ttu-id="aaf64-307">Hello 인터페이스 구현 예제에서는 `IChangeFeedObserver` hello를 통해 `DocumentFeedObserver` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-307">In our example, we implement hello interface `IChangeFeedObserver` through hello `DocumentFeedObserver` class.</span></span> <span data-ttu-id="aaf64-308">여기에서 hello `ProcessChangesAsync` upserts (업데이트) 변경 내용으로 인해 문서 피드 hello 대상 컬렉션으로 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-308">Here, hello `ProcessChangesAsync` function upserts (updates) a document from change feed into hello destination collection.</span></span> <span data-ttu-id="aaf64-309">이 예제는 데이터 집합의 순서 toochange hello 파티션 키의 컬렉션을 하나 tooanother에서 데이터를 이동 하는 데 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-309">This example is useful for moving data from one collection tooanother in order toochange hello partition key of a data set.</span></span> 

<span data-ttu-id="aaf64-310">*실행 중인 hello 프로세서 호스트*</span><span class="sxs-lookup"><span data-stu-id="aaf64-310">*Running hello Processor Host*</span></span>

<span data-ttu-id="aaf64-311">이벤트 처리를 시작하기 전에, 변경 피드 옵션 및 변경 피드 호스트 옵션을 모두 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-311">Before beginning event processing, both change feed options and change feed host options can be customized.</span></span> 
```csharp
    // Customizable change feed option and host options 
    ChangeFeedOptions feedOptions = new ChangeFeedOptions();

    // ie customize StartFromBeginning so change feed reads from beginning
    // can customize MaxItemCount, PartitonKeyRangeId, RequestContinuation, SessionToken and StartFromBeginning
    feedOptions.StartFromBeginning = true;

    ChangeFeedHostOptions feedHostOptions = new ChangeFeedHostOptions();

    // ie. customizing lease renewal interval too15 seconds
    // can customize LeaseRenewInterval, LeaseAcquireInterval, LeaseExpirationInterval, FeedPollDelay 
    feedHostOptions.LeaseRenewInterval = TimeSpan.FromSeconds(15);

```
<span data-ttu-id="aaf64-312">다음 표에서 hello에 지정할 수 있는 hello 특정 필드 요약 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-312">hello specific fields that can be customized are summarized in hello following tables.</span></span> 

<span data-ttu-id="aaf64-313">**변경 피드 옵션**:</span><span class="sxs-lookup"><span data-stu-id="aaf64-313">**Change Feed Options**:</span></span>
<table>
    <tr>
        <th><span data-ttu-id="aaf64-314">속성 이름</span><span class="sxs-lookup"><span data-stu-id="aaf64-314">Property Name</span></span></th>
        <th><span data-ttu-id="aaf64-315">설명</span><span class="sxs-lookup"><span data-stu-id="aaf64-315">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="aaf64-316">MaxItemCount</span><span class="sxs-lookup"><span data-stu-id="aaf64-316">MaxItemCount</span></span></td>
        <td><span data-ttu-id="aaf64-317">Hello 항목 toobe hello Azure Cosmos DB 데이터베이스 서비스의에서 hello 열거 작업에서 반환 된 최대 수를 가져오거나 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-317">Gets or sets hello maximum number of items toobe returned in hello enumeration operation in hello Azure Cosmos DB database service.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="aaf64-318">PartitionKeyRangeId</span><span class="sxs-lookup"><span data-stu-id="aaf64-318">PartitionKeyRangeId</span></span></td>
        <td><span data-ttu-id="aaf64-319">Hello Azure Cosmos DB 데이터베이스 서비스에서 hello 현재 요청에 대 한 hello 파티션 키 범위 id를 가져오거나 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-319">Gets or sets hello partition key range id for hello current request in hello Azure Cosmos DB database service.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="aaf64-320">RequestContinuation</span><span class="sxs-lookup"><span data-stu-id="aaf64-320">RequestContinuation</span></span></td>
        <td><span data-ttu-id="aaf64-321">Hello Azure Cosmos DB 데이터베이스 서비스에서 hello 요청 continuation 토큰을 가져오거나 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-321">Gets or sets hello request continuation token in hello Azure Cosmos DB database service.</span></span></td>
    </tr>
        <tr>
        <td><span data-ttu-id="aaf64-322">SessionToken</span><span class="sxs-lookup"><span data-stu-id="aaf64-322">SessionToken</span></span></td>
        <td><span data-ttu-id="aaf64-323">세션 일관성 hello Azure Cosmos DB 데이터베이스 서비스에에서 사용 하기 위해 hello 세션 토큰을 가져오거나 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-323">Gets or sets hello session token for use with session consistency in hello Azure Cosmos DB database service.</span></span></td>
    </tr>
        <tr>
        <td><span data-ttu-id="aaf64-324">StartFromBeginning</span><span class="sxs-lookup"><span data-stu-id="aaf64-324">StartFromBeginning</span></span></td>
        <td><span data-ttu-id="aaf64-325">Hello Azure Cosmos DB 데이터베이스 서비스에서 피드 변경 (true) 시작 하 고 hello 또는 현재 (false)에서 시작할지 여부를 나타내는 값을 가져오거나 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-325">Gets or sets whether change feed in hello Azure Cosmos DB database service should start from hello beginning (true) or from current (false).</span></span> <span data-ttu-id="aaf64-326">기본적으로 현재(false)부터 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-326">By default, it starts from current (false).</span></span></td>
    </tr>
</table>

<span data-ttu-id="aaf64-327">**변경 피드 호스트 옵션**:</span><span class="sxs-lookup"><span data-stu-id="aaf64-327">**Change Feed Host Options**:</span></span>
<table>
    <tr>
        <th><span data-ttu-id="aaf64-328">속성 이름</span><span class="sxs-lookup"><span data-stu-id="aaf64-328">Property Name</span></span></th>
        <th><span data-ttu-id="aaf64-329">형식</span><span class="sxs-lookup"><span data-stu-id="aaf64-329">Type</span></span></th>
        <th><span data-ttu-id="aaf64-330">설명</span><span class="sxs-lookup"><span data-stu-id="aaf64-330">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="aaf64-331">LeaseRenewInterval</span><span class="sxs-lookup"><span data-stu-id="aaf64-331">LeaseRenewInterval</span></span></td>
        <td><span data-ttu-id="aaf64-332">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="aaf64-332">TimeSpan</span></span></td>
        <td><span data-ttu-id="aaf64-333">hello ChangeFeedEventHost 인스턴스에서 현재 보유 하는 파티션에 대 한 모든 임대에 대 한 hello 간격입니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-333">hello interval for all leases for partitions currently held by hello ChangeFeedEventHost instance.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="aaf64-334">LeaseAcquireInterval</span><span class="sxs-lookup"><span data-stu-id="aaf64-334">LeaseAcquireInterval</span></span></td>
        <td><span data-ttu-id="aaf64-335">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="aaf64-335">TimeSpan</span></span></td>
        <td><span data-ttu-id="aaf64-336">파티션에 균등 하 게 알려진된 호스트 인스턴스에서 여부를 태스크 toocompute 오프 간격 tookick을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-336">hello interval tookick off a task toocompute whether partitions are distributed evenly among known host instances.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="aaf64-337">LeaseExpirationInterval</span><span class="sxs-lookup"><span data-stu-id="aaf64-337">LeaseExpirationInterval</span></span></td>
        <td><span data-ttu-id="aaf64-338">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="aaf64-338">TimeSpan</span></span></td>
        <td><span data-ttu-id="aaf64-339">hello 간격은 hello에 대 한 파티션을 나타내는 임대를 임대를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-339">hello interval for which hello lease is taken on a lease representing a partition.</span></span> <span data-ttu-id="aaf64-340">이 간격을 hello 임대 갱신 하지 않으면 만료 되어 및 hello 파티션의 소유권 tooanother ChangeFeedEventHost 인스턴스를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-340">If hello lease is not renewed within this interval, it is expired and ownership of hello partition moves tooanother ChangeFeedEventHost instance.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="aaf64-341">FeedPollDelay</span><span class="sxs-lookup"><span data-stu-id="aaf64-341">FeedPollDelay</span></span></td>
        <td><span data-ttu-id="aaf64-342">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="aaf64-342">TimeSpan</span></span></td>
        <td><span data-ttu-id="aaf64-343">모든 현재 변경 내용을 종료 후 hello hello에 새 변경 내용에 대 한 파티션을 폴링 간격 피드입니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-343">hello delay between polling a partition for new changes on hello feed, after all current changes are drained.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="aaf64-344">CheckpointFrequency</span><span class="sxs-lookup"><span data-stu-id="aaf64-344">CheckpointFrequency</span></span></td>
        <td><span data-ttu-id="aaf64-345">CheckpointFrequency</span><span class="sxs-lookup"><span data-stu-id="aaf64-345">CheckpointFrequency</span></span></td>
        <td><span data-ttu-id="aaf64-346">hello 주파수 toocheckpoint 임대 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-346">hello frequency toocheckpoint leases.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="aaf64-347">MinPartitionCount</span><span class="sxs-lookup"><span data-stu-id="aaf64-347">MinPartitionCount</span></span></td>
        <td><span data-ttu-id="aaf64-348">int</span><span class="sxs-lookup"><span data-stu-id="aaf64-348">Int</span></span></td>
        <td><span data-ttu-id="aaf64-349">hello hello 호스트에 대 한 최소 파티션 수입니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-349">hello minimum partition count for hello host.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="aaf64-350">MaxPartitionCount</span><span class="sxs-lookup"><span data-stu-id="aaf64-350">MaxPartitionCount</span></span></td>
        <td><span data-ttu-id="aaf64-351">int</span><span class="sxs-lookup"><span data-stu-id="aaf64-351">Int</span></span></td>
        <td><span data-ttu-id="aaf64-352">hello 파티션 hello 호스트의 최대 수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-352">hello maximum number of partitions hello host can serve.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="aaf64-353">DiscardExistingLeases</span><span class="sxs-lookup"><span data-stu-id="aaf64-353">DiscardExistingLeases</span></span></td>
        <td><span data-ttu-id="aaf64-354">Bool</span><span class="sxs-lookup"><span data-stu-id="aaf64-354">Bool</span></span></td>
        <td><span data-ttu-id="aaf64-355">여부에서 hello 시작 hello 호스트의 모든 기존 임대 삭제 하 고 hello 호스트는 처음부터 다시 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-355">Whether on hello start of hello host all existing leases should be deleted and hello host should start from scratch.</span></span></td>
    </tr>
</table>


<span data-ttu-id="aaf64-356">toostart 이벤트 처리를 인스턴스화할 `ChangeFeedProcessorHost`, Azure Cosmos DB 컬렉션에 대 한 hello 적절 한 매개 변수를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-356">toostart event processing, instantiate `ChangeFeedProcessorHost`, providing hello appropriate parameters for your Azure Cosmos DB collection.</span></span> <span data-ttu-id="aaf64-357">그런 다음 호출 `RegisterObserverAsync` tooregister 프로그램 `IChangeFeedObserver` hello 런타임 (이 예제의 DocumentFeedObserver) 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-357">Then, call `RegisterObserverAsync` tooregister your `IChangeFeedObserver` (DocumentFeedObserver in this example) implementation with hello runtime.</span></span> <span data-ttu-id="aaf64-358">이 시점에서 hello 호스트 tooacquire 모든 파티션 키 범위 "과 대" 알고리즘을 사용 하 여 hello Azure Cosmos DB 컬렉션에 대 한 임 대권을 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-358">At this point, hello host attempts tooacquire a lease on every partition key range in hello Azure Cosmos DB collection using a "greedy" algorithm.</span></span> <span data-ttu-id="aaf64-359">이러한 임대는 지정된 시간 프레임 동안 지속되며 갱신되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-359">These leases last for a given timeframe and must then be renewed.</span></span> <span data-ttu-id="aaf64-360">새 노드로 작업자 인스턴스는이 경우 온라인 상태로, 임대를 예약을 배치 하 고 시간이 지남에 따라 hello 부하 이동 노드 간 각 호스트 시도 tooacquire 임대가 더 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-360">As new nodes, worker instances, in this case, come online, they place lease reservations and over time hello load shifts between nodes as each host attempts tooacquire more leases.</span></span> 

<span data-ttu-id="aaf64-361">Hello 샘플 코드를 사용 하 여 팩터리 클래스 (DocumentFeedObserverFactory.cs) toocreate 관찰자 및 hello `RegistObserverFactoryAsync` tooregister hello observer입니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-361">In hello sample code, we use a factory class (DocumentFeedObserverFactory.cs) toocreate an observer and hello `RegistObserverFactoryAsync` tooregister hello observer.</span></span> 

```csharp
using (DocumentClient destClient = new DocumentClient(destCollInfo.Uri, destCollInfo.MasterKey))
    {
        DocumentFeedObserverFactory docObserverFactory = new DocumentFeedObserverFactory(destClient, destCollInfo);
        ChangeFeedEventHost host = new ChangeFeedEventHost(hostName, documentCollectionLocation, leaseCollectionLocation, feedOptions, feedHostOptions);

        await host.RegisterObserverFactoryAsync(docObserverFactory);

        Console.WriteLine("Running... Press enter toostop.");
        Console.ReadLine();

        await host.UnregisterObserversAsync();
    }
```
<span data-ttu-id="aaf64-362">시간이 지남에 따라 평형이 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-362">Over time, an equilibrium is established.</span></span> <span data-ttu-id="aaf64-363">이 동적 기능을 사용 하면 수직 확장 및 축소 모두에 대 한 자동 크기 조정 적용 toobe tooconsumers CPU 기반 합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-363">This dynamic capability enables CPU-based auto-scaling toobe applied tooconsumers for both scale-up and scale-down.</span></span> <span data-ttu-id="aaf64-364">변경 내용을 처리할 수 있는 것 보다 빠른 속도로 Azure Cosmos DB에서 사용할 수 있는 경우 소비자에 대 한 hello CPU 증가 작업자 인스턴스 수에 사용 되는 toocause 자동으로 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-364">If changes are available in Azure Cosmos DB at a faster rate than consumers can process, hello CPU increase on consumers can be used toocause an auto-scale on worker instance count.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aaf64-365">다음 단계</span><span class="sxs-lookup"><span data-stu-id="aaf64-365">Next steps</span></span>
* <span data-ttu-id="aaf64-366">Hello 시도 [Azure Cosmos DB 변경 GitHub에서 코드 샘플 피드](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/ChangeFeed)</span><span class="sxs-lookup"><span data-stu-id="aaf64-366">Try hello [Azure Cosmos DB Change feed code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/ChangeFeed)</span></span>
* <span data-ttu-id="aaf64-367">Hello로 코딩을 시작 해 [Azure Cosmos DB Sdk](documentdb-sdk-dotnet.md) 또는 hello [REST API](/rest/api/documentdb/)합니다.</span><span class="sxs-lookup"><span data-stu-id="aaf64-367">Get started coding with hello [Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md) or hello [REST API](/rest/api/documentdb/).</span></span>

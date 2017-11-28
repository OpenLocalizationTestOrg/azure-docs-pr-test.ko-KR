---
title: "Azure Cosmos DB: DocumentDB Java API, SDK 및 리소스 | Microsoft Docs"
description: "Java API와 SDK 릴리스 날짜, 사용 중지 날짜 및 hello Azure Cosmos DB DocumentDB Java SDK의 각 버전 간의 변경 내용을 포함 하 여 hello에 대 한 모든에 대해 알아봅니다."
services: cosmos-db
documentationcenter: java
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 7861cadf-2a05-471a-9925-0fec0599351b
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 07/11/2017
ms.author: khdang
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8ef43ebeb7ae1bfc55512c4a7489c1b7930122d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-documentdb-java-sdk-release-notes-and-resources"></a><span data-ttu-id="48449-103">Azure Cosmos DB: DocumentDB Java SDK 릴리스 정보 및 리소스</span><span class="sxs-lookup"><span data-stu-id="48449-103">Azure Cosmos DB: DocumentDB Java SDK release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="48449-104">.NET</span><span class="sxs-lookup"><span data-stu-id="48449-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="48449-105">.NET 변경 피드</span><span class="sxs-lookup"><span data-stu-id="48449-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="48449-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="48449-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="48449-107">Node.JS</span><span class="sxs-lookup"><span data-stu-id="48449-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="48449-108">Java</span><span class="sxs-lookup"><span data-stu-id="48449-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="48449-109">Python</span><span class="sxs-lookup"><span data-stu-id="48449-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="48449-110">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="48449-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="48449-111">REST 리소스 공급자</span><span class="sxs-lookup"><span data-stu-id="48449-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="48449-112">SQL</span><span class="sxs-lookup"><span data-stu-id="48449-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="48449-113">**SDK 다운로드**</span><span class="sxs-lookup"><span data-stu-id="48449-113">**SDK Download**</span></span></td><td>[<span data-ttu-id="48449-114">Maven</span><span class="sxs-lookup"><span data-stu-id="48449-114">Maven</span></span>](http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22com.microsoft.azure%22%20AND%20a%3A%22azure-documentdb%22)</td></tr>

<tr><td><span data-ttu-id="48449-115">**API 설명서**</span><span class="sxs-lookup"><span data-stu-id="48449-115">**API documentation**</span></span></td><td>[<span data-ttu-id="48449-116">Java API 참조 설명서</span><span class="sxs-lookup"><span data-stu-id="48449-116">Java API reference documentation</span></span>](/java/api/com.microsoft.azure.documentdb)</td></tr>

<tr><td><span data-ttu-id="48449-117">**TooSDK 영향**</span><span class="sxs-lookup"><span data-stu-id="48449-117">**Contribute tooSDK**</span></span></td><td>[<span data-ttu-id="48449-118">GitHub</span><span class="sxs-lookup"><span data-stu-id="48449-118">GitHub</span></span>](https://github.com/Azure/azure-documentdb-java/)</td></tr>

<tr><td><span data-ttu-id="48449-119">**시작**</span><span class="sxs-lookup"><span data-stu-id="48449-119">**Get started**</span></span></td><td>[<span data-ttu-id="48449-120">Hello Java SDK 시작</span><span class="sxs-lookup"><span data-stu-id="48449-120">Get started with hello Java SDK</span></span>](documentdb-java-get-started.md)</td></tr>

<tr><td><span data-ttu-id="48449-121">**웹앱 자습서**</span><span class="sxs-lookup"><span data-stu-id="48449-121">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="48449-122">Azure Cosmos DB를 사용한 웹 응용 프로그램 개발</span><span class="sxs-lookup"><span data-stu-id="48449-122">Web application development with Azure Cosmos DB</span></span>](documentdb-java-application.md)</td></tr>

<tr><td><span data-ttu-id="48449-123">**현재 지원되는 런타임**</span><span class="sxs-lookup"><span data-stu-id="48449-123">**Current supported runtime**</span></span></td><td>[<span data-ttu-id="48449-124">JDK 7</span><span class="sxs-lookup"><span data-stu-id="48449-124">JDK 7</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)</td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="48449-125">릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="48449-125">Release Notes</span></span>

### <a name="a-name11201120"></a><span data-ttu-id="48449-126"><a name="1.12.0"/>1.12.0</span><span class="sxs-lookup"><span data-stu-id="48449-126"><a name="1.12.0"/>1.12.0</span></span>
* <span data-ttu-id="48449-127">파티션 중를 처리 하는 중요 한 버그 수정 toorequest 분할 합니다.</span><span class="sxs-lookup"><span data-stu-id="48449-127">Critical bug fixes toorequest processing during partition splits.</span></span>
* <span data-ttu-id="48449-128">강력한 hello 및 BoundedStaleness 일관성 수준 관련 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="48449-128">Fixed an issue with hello Strong and BoundedStaleness consistency levels.</span></span>

### <a name="a-name11101110"></a><span data-ttu-id="48449-129"><a name="1.11.0"/>1.11.0</span><span class="sxs-lookup"><span data-stu-id="48449-129"><a name="1.11.0"/>1.11.0</span></span>
* <span data-ttu-id="48449-130">ConsistentPrefix라는 새로운 일관성 수준에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="48449-130">Added support for a new consistency level called ConsistentPrefix.</span></span>
* <span data-ttu-id="48449-131">세션 모드에서 컬렉션을 읽을 때 발생하는 버그를 수정했습니다.</span><span class="sxs-lookup"><span data-stu-id="48449-131">Fixed a bug in reading collection in session mode.</span></span>

### <a name="a-name11001100"></a><span data-ttu-id="48449-132"><a name="1.10.0"/>1.10.0</span><span class="sxs-lookup"><span data-stu-id="48449-132"><a name="1.10.0"/>1.10.0</span></span>
* <span data-ttu-id="48449-133">초당 2,500 RU 및 초당 100 RU의 규모 조정 능력을 통해 분할된 컬렉션을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="48449-133">Enabled support for partitioned collection with as low as 2,500 RU/sec and scale in increments of 100 RU/sec.</span></span>
* <span data-ttu-id="48449-134">일부 쿼리에서 NullRef 예외가 발생할 수 있는 네이티브 어셈블리 hello에서에서 버그를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="48449-134">Fixed a bug in hello native assembly which can cause NullRef exception in some queries.</span></span>

### <a name="a-name196196"></a><span data-ttu-id="48449-135"><a name="1.9.6"/>1.9.6</span><span class="sxs-lookup"><span data-stu-id="48449-135"><a name="1.9.6"/>1.9.6</span></span>
* <span data-ttu-id="48449-136">게이트웨이 모드에서 쿼리에 대 한 예외를 일으킬 수 있는 hello 쿼리 엔진 구성에서 버그를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="48449-136">Fixed a bug in hello query engine configuration that may cause exceptions for queries in Gateway mode.</span></span>
* <span data-ttu-id="48449-137">컬렉션을 만든 후 즉시 요청에 대 한 "소유자 리소스를 찾을 수 없습니다." 예외를 일으킬 수 있는 hello 세션 컨테이너에 몇 가지 버그도 수정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="48449-137">Fixed a few bugs in hello session container that may cause an "Owner resource not found" exception for requests immediately after collection creation.</span></span>

### <a name="a-name195195"></a><span data-ttu-id="48449-138"><a name="1.9.5"/>1.9.5</span><span class="sxs-lookup"><span data-stu-id="48449-138"><a name="1.9.5"/>1.9.5</span></span>
* <span data-ttu-id="48449-139">집계 쿼리(COUNT, MIN, MAX, SUM 및 AVG)에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="48449-139">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span> <span data-ttu-id="48449-140">[집계 지원](documentdb-sql-query.md#Aggregates)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="48449-140">See [Aggregation support](documentdb-sql-query.md#Aggregates).</span></span>
* <span data-ttu-id="48449-141">변경 피드에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="48449-141">Added support for change feed.</span></span>
* <span data-ttu-id="48449-142">RequestOptions.setPopulateQuotaInfo를 통한 컬렉션 할당량 정보에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="48449-142">Added support for collection quota information through RequestOptions.setPopulateQuotaInfo.</span></span>
* <span data-ttu-id="48449-143">RequestOptions.setScriptLoggingEnabled를 통한 저장 프로시저 스크립트에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="48449-143">Added support for stored procedure script logging through RequestOptions.setScriptLoggingEnabled.</span></span>
* <span data-ttu-id="48449-144">제한 오류가 발생할 때 DirectHttps 모드의 쿼리가 중단될 수 있는 버그를 수정했습니다.</span><span class="sxs-lookup"><span data-stu-id="48449-144">Fixed a bug where query in DirectHttps mode may hang when encountering throttle failures.</span></span>
* <span data-ttu-id="48449-145">세션 일관성 모드의 버그를 수정했습니다.</span><span class="sxs-lookup"><span data-stu-id="48449-145">Fixed a bug in session consistency mode.</span></span>
* <span data-ttu-id="48449-146">요청 속도가 높은 경우 HttpContext에서 NullReferenceException을 유발할 수 있는 버그를 수정했습니다.</span><span class="sxs-lookup"><span data-stu-id="48449-146">Fixed a bug which may cause NullReferenceException in HttpContext when request rate is high.</span></span>
* <span data-ttu-id="48449-147">DirectHttps 모드의 성능이 향상되었습니다.</span><span class="sxs-lookup"><span data-stu-id="48449-147">Improved performance of DirectHttps mode.</span></span>

### <a name="a-name194194"></a><span data-ttu-id="48449-148"><a name="1.9.4"/>1.9.4</span><span class="sxs-lookup"><span data-stu-id="48449-148"><a name="1.9.4"/>1.9.4</span></span>
* <span data-ttu-id="48449-149">ConnectionPolicy.setProxy() API와 함께 샘플 클라이언트 인스턴스 기반 프록시 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="48449-149">Added simple client instance-based proxy support with ConnectionPolicy.setProxy() API.</span></span>
* <span data-ttu-id="48449-150">추가 된 DocumentClient.close() API tooproperly DocumentClient 인스턴스 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="48449-150">Added DocumentClient.close() API tooproperly shutdown DocumentClient instance.</span></span>
* <span data-ttu-id="48449-151">쿼리 성능이 향상된 hello 쿼리 계획 hello 게이트웨이 대신 hello 네이티브 어셈블리에서 파생 하 여 직접 연결 모드에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48449-151">Improved query performance in direct connectivity mode by deriving hello query plan from hello native assembly instead of hello Gateway.</span></span>
* <span data-ttu-id="48449-152">FAIL_ON_UNKNOWN_PROPERTIES 설정 false = 사용자가 자신의 POJO에 JsonIgnoreProperties toodefine 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="48449-152">Set FAIL_ON_UNKNOWN_PROPERTIES = false so users don't need toodefine JsonIgnoreProperties in their POJO.</span></span>
* <span data-ttu-id="48449-153">로깅 toouse SLF4J를 리팩터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="48449-153">Refactored logging toouse SLF4J.</span></span>
* <span data-ttu-id="48449-154">일관성 판독기의 몇 가지 버그를 수정했습니다.</span><span class="sxs-lookup"><span data-stu-id="48449-154">Fixed a few other bugs in consistency reader.</span></span>

### <a name="a-name193193"></a><span data-ttu-id="48449-155"><a name="1.9.3"/>1.9.3</span><span class="sxs-lookup"><span data-stu-id="48449-155"><a name="1.9.3"/>1.9.3</span></span>
* <span data-ttu-id="48449-156">직접 연결 모드에서 hello 연결 관리 tooprevent 연결 누수에서 버그를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="48449-156">Fixed a bug in hello connection management tooprevent connection leaks in direct connectivity mode.</span></span>
* <span data-ttu-id="48449-157">NullReferenece 예외가 throw 될 수 있는 hello TOP 쿼리에서 버그를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="48449-157">Fixed a bug in hello TOP query where it may throw NullReferenece exception.</span></span>
* <span data-ttu-id="48449-158">Hello hello 내부 캐시에 대 한 네트워크 호출 수를 줄이면 성능이 향상 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="48449-158">Improved performance by reducing hello number of network call for hello internal caches.</span></span>
* <span data-ttu-id="48449-159">DocumentClientException에 상태 코드 ActivityID 및 요청 URI를 추가하여 문제 해결을 개선했습니다.</span><span class="sxs-lookup"><span data-stu-id="48449-159">Added status code, ActivityID and Request URI in DocumentClientException for better troubleshooting.</span></span>

### <a name="a-name192192"></a><span data-ttu-id="48449-160"><a name="1.9.2"/>1.9.2</span><span class="sxs-lookup"><span data-stu-id="48449-160"><a name="1.9.2"/>1.9.2</span></span>
* <span data-ttu-id="48449-161">안정성에 대 한 hello 연결 관리 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="48449-161">Fixed an issue in hello connection management for stability.</span></span>

### <a name="a-name191191"></a><span data-ttu-id="48449-162"><a name="1.9.1"/>1.9.1</span><span class="sxs-lookup"><span data-stu-id="48449-162"><a name="1.9.1"/>1.9.1</span></span>
* <span data-ttu-id="48449-163">BoundedStaleness 일관성 수준에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="48449-163">Added support for BoundedStaleness consistency level.</span></span>
* <span data-ttu-id="48449-164">분할된 컬렉션의 CRUD 작업에 대한 직접 연결 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="48449-164">Added support for direct connectivity for CRUD operations for partitioned collections.</span></span>
* <span data-ttu-id="48449-165">SQL을 사용하여 데이터베이스를 쿼리할 때의 버그가 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="48449-165">Fixed a bug in querying a database with SQL.</span></span>
* <span data-ttu-id="48449-166">여기서 세션 토큰이 설정 되는 경우 올바르게 hello 세션 캐시에는 버그를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="48449-166">Fixed a bug in hello session cache where session token may be set incorrectly.</span></span>

### <a name="a-name190190"></a><span data-ttu-id="48449-167"><a name="1.9.0"/>1.9.0</span><span class="sxs-lookup"><span data-stu-id="48449-167"><a name="1.9.0"/>1.9.0</span></span>
* <span data-ttu-id="48449-168">파티션 간 병렬 쿼리에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="48449-168">Added support for cross partition parallel queries.</span></span>
* <span data-ttu-id="48449-169">분할된 컬렉션의 TOP/ORDER BY 쿼리에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="48449-169">Added support for TOP/ORDER BY queries for partitioned collections.</span></span>
* <span data-ttu-id="48449-170">강력한 일관성에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="48449-170">Added support for strong consistency.</span></span>
* <span data-ttu-id="48449-171">직접 연결을 사용할 때 이름 기반 요청에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="48449-171">Added support for name based requests when using direct connectivity.</span></span>
* <span data-ttu-id="48449-172">고정된 toomake ActivityId 전체 하 게 유지 일관 된 모든 요청 다시 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="48449-172">Fixed toomake ActivityId stay consistent across all request retries.</span></span>
* <span data-ttu-id="48449-173">버그를 수정 hello 사용 하 여 컬렉션을 다시 만들 때 toohello 세션 캐시와 관련 된 동일한 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="48449-173">Fixed a bug related toohello session cache when recreating a collection with hello same name.</span></span>
* <span data-ttu-id="48449-174">지역 펜싱 공간 쿼리에 대한 컬렉션 인덱싱 정책을 지정하는 동안 Polygon 및 LineString 데이터 형식이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="48449-174">Added Polygon and LineString DataTypes while specifying collection indexing policy for geo-fencing spatial queries.</span></span>
* <span data-ttu-id="48449-175">Java 1.8용 Java 문서 관련 문제가 해결되었습니다.</span><span class="sxs-lookup"><span data-stu-id="48449-175">Fixed issues with Java Doc for Java 1.8.</span></span>

### <a name="a-name181181"></a><span data-ttu-id="48449-176"><a name="1.8.1"/>1.8.1</span><span class="sxs-lookup"><span data-stu-id="48449-176"><a name="1.8.1"/>1.8.1</span></span>
* <span data-ttu-id="48449-177">PartitionKeyDefinitionMap에서 버그를 수정 toocache 단일 파티션 컬렉션 및 추가 만들지 인출 파티션 키를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="48449-177">Fixed a bug in PartitionKeyDefinitionMap toocache single partition collections and not make extra fetch partition key requests.</span></span>
* <span data-ttu-id="48449-178">잘못 된 파티션 키 값이 제공 하는 경우 버그 toonot 다시 시도 고정 합니다.</span><span class="sxs-lookup"><span data-stu-id="48449-178">Fixed a bug toonot retry when an incorrect partition key value is provided.</span></span>

### <a name="a-name180180"></a><span data-ttu-id="48449-179"><a name="1.8.0"/>1.8.0</span><span class="sxs-lookup"><span data-stu-id="48449-179"><a name="1.8.0"/>1.8.0</span></span>
* <span data-ttu-id="48449-180">다중 영역 데이터베이스 계정에 대 한 추가 된 hello 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="48449-180">Added hello support for multi-region database accounts.</span></span>
* <span data-ttu-id="48449-181">자동 다시 시도 최대 옵션 toocustomize hello로 제한 된 요청에 대 한 지원 추가 재시도 횟수와 최대 대기 시간을 다시 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="48449-181">Added support for automatic retry on throttled requests with options toocustomize hello max retry attempts and max retry wait time.</span></span>  <span data-ttu-id="48449-182">RetryOptions와 ConnectionPolicy.getRetryOptions()을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="48449-182">See RetryOptions and ConnectionPolicy.getRetryOptions().</span></span>
* <span data-ttu-id="48449-183">IPartitionResolver 기반 사용자 지정 파티셔닝 코드의 사용이 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="48449-183">Deprecated IPartitionResolver based custom partitioning code.</span></span> <span data-ttu-id="48449-184">보다 큰 저장소 및 처리량에는 파티션된 컬렉션을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="48449-184">Please use partitioned collections for higher storage and throughput.</span></span>

### <a name="a-name171171"></a><span data-ttu-id="48449-185"><a name="1.7.1"/>1.7.1</span><span class="sxs-lookup"><span data-stu-id="48449-185"><a name="1.7.1"/>1.7.1</span></span>
* <span data-ttu-id="48449-186">제한에 대한 재시도 정책 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="48449-186">Added retry policy support for throttling.</span></span>  

### <a name="a-name170170"></a><span data-ttu-id="48449-187"><a name="1.7.0"/>1.7.0</span><span class="sxs-lookup"><span data-stu-id="48449-187"><a name="1.7.0"/>1.7.0</span></span>
* <span data-ttu-id="48449-188">문서에 대 한 시간 toolive (TTL) 지원이 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="48449-188">Added time toolive (TTL) support for documents.</span></span>

### <a name="a-name160160"></a><span data-ttu-id="48449-189"><a name="1.6.0"/>1.6.0</span><span class="sxs-lookup"><span data-stu-id="48449-189"><a name="1.6.0"/>1.6.0</span></span>
* <span data-ttu-id="48449-190">[분할된 컬렉션](partition-data.md) 및 [사용자 정의 성능 수준](performance-levels.md)이 구현되었습니다.</span><span class="sxs-lookup"><span data-stu-id="48449-190">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span>

### <a name="a-name151151"></a><span data-ttu-id="48449-191"><a name="1.5.1"/>1.5.1</span><span class="sxs-lookup"><span data-stu-id="48449-191"><a name="1.5.1"/>1.5.1</span></span>
* <span data-ttu-id="48449-192">다른 Sdk와 일치 하는 little endian toobe HashPartitionResolver toogenerate 해시 값에서 버그를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="48449-192">Fixed a bug in HashPartitionResolver toogenerate hash values in little-endian toobe consistent with other SDKs.</span></span>

### <a name="a-name150150"></a><span data-ttu-id="48449-193"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="48449-193"><a name="1.5.0"/>1.5.0</span></span>
* <span data-ttu-id="48449-194">추가 해시 & 범위 파티션 확인자 tooassist 여러 파티션에서 분할 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="48449-194">Add Hash & Range partition resolvers tooassist with sharding applications across multiple partitions.</span></span>

### <a name="a-name140140"></a><span data-ttu-id="48449-195"><a name="1.4.0"/>1.4.0</span><span class="sxs-lookup"><span data-stu-id="48449-195"><a name="1.4.0"/>1.4.0</span></span>
* <span data-ttu-id="48449-196">Upsert를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="48449-196">Implement Upsert.</span></span> <span data-ttu-id="48449-197">새 upsertXXX 메서드가 toosupport Upsert 기능을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="48449-197">New upsertXXX methods added toosupport Upsert feature.</span></span>
* <span data-ttu-id="48449-198">ID 기반 라우팅을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="48449-198">Implement ID Based Routing.</span></span> <span data-ttu-id="48449-199">공용 API 변경 없이 모두 내부에서 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="48449-199">No public API changes, all changes internal.</span></span>

### <a name="a-name130130"></a><span data-ttu-id="48449-200"><a name="1.3.0"/>1.3.0</span><span class="sxs-lookup"><span data-stu-id="48449-200"><a name="1.3.0"/>1.3.0</span></span>
* <span data-ttu-id="48449-201">릴리스 건너뛴 정렬을 다른 Sdk 사용 하 여 toobring 버전 번호</span><span class="sxs-lookup"><span data-stu-id="48449-201">Release skipped toobring version number in alignment with other SDKs</span></span>

### <a name="a-name120120"></a><span data-ttu-id="48449-202"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="48449-202"><a name="1.2.0"/>1.2.0</span></span>
* <span data-ttu-id="48449-203">지리 공간 인덱스 지원</span><span class="sxs-lookup"><span data-stu-id="48449-203">Supports GeoSpatial Index</span></span>
* <span data-ttu-id="48449-204">모든 리소스에 대한 ID 속성의 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="48449-204">Validates id property for all resources.</span></span> <span data-ttu-id="48449-205">리소스에 대한 ID는 ?, /, #, \, 문자를 포함하거나 공백으로 끝날 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="48449-205">Ids for resources cannot contain ?, /, #, \, characters or end with a space.</span></span>
* <span data-ttu-id="48449-206">새 헤더 "인덱스 변환 진행 중" tooResourceResponse를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="48449-206">Adds new header "index transformation progress" tooResourceResponse.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="48449-207"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="48449-207"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="48449-208">V2 인덱싱 정책 구현</span><span class="sxs-lookup"><span data-stu-id="48449-208">Implements V2 indexing policy</span></span>

### <a name="a-name100100"></a><span data-ttu-id="48449-209"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="48449-209"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="48449-210">GA SDK</span><span class="sxs-lookup"><span data-stu-id="48449-210">GA SDK</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="48449-211">릴리스 및 사용 중지 날짜</span><span class="sxs-lookup"><span data-stu-id="48449-211">Release & Retirement Dates</span></span>
<span data-ttu-id="48449-212">Microsoft는 알림을 적어도 제공 **12 개월** 순서 toosmooth hello 전환 tooa 지원/최신 버전의 SDK를 사용 중지 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="48449-212">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order toosmooth hello transition tooa newer/supported version.</span></span>

<span data-ttu-id="48449-213">새로운 기능 및 기능 및 최적화는 toohello 현재만 추가 그렇게 하면 항상 업그레이드 toohello 최신 SDK 버전을 가능한 한 빨리 권장는 SDK입니다.</span><span class="sxs-lookup"><span data-stu-id="48449-213">New features and functionality and optimizations are only added toohello current SDK, as such it is  recommend that you always upgrade toohello latest SDK version as early as possible.</span></span>

<span data-ttu-id="48449-214">모든 요청 tooCosmos 사용 중지 된 SDK를 사용 하 여 DB hello 서비스에서 거부 됩니다.</span><span class="sxs-lookup"><span data-stu-id="48449-214">Any request tooCosmos DB using a retired SDK will be rejected by hello service.</span></span>

> [!WARNING]
> <span data-ttu-id="48449-215">모든 버전의 Java 이전 tooversion에 대 한 DocumentDB SDK hello **1.0.0** 에 사용 중지 될 예정 **2016 년 2 월 29 일**합니다.</span><span class="sxs-lookup"><span data-stu-id="48449-215">All versions of hello DocumentDB SDK for Java prior tooversion **1.0.0** will be retired on **February 29, 2016**.</span></span>
> 
> 

<br/>

| <span data-ttu-id="48449-216">버전</span><span class="sxs-lookup"><span data-stu-id="48449-216">Version</span></span> | <span data-ttu-id="48449-217">릴리스 날짜</span><span class="sxs-lookup"><span data-stu-id="48449-217">Release Date</span></span> | <span data-ttu-id="48449-218">사용 중지 날짜</span><span class="sxs-lookup"><span data-stu-id="48449-218">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="48449-219">1.12.0</span><span class="sxs-lookup"><span data-stu-id="48449-219">1.12.0</span></span>](#1.12.0) |<span data-ttu-id="48449-220">2017년 7월 11일</span><span class="sxs-lookup"><span data-stu-id="48449-220">July 11, 2017</span></span> |--- |
| [<span data-ttu-id="48449-221">1.11.0</span><span class="sxs-lookup"><span data-stu-id="48449-221">1.11.0</span></span>](#1.11.0) |<span data-ttu-id="48449-222">2017년 5월 10일</span><span class="sxs-lookup"><span data-stu-id="48449-222">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="48449-223">1.10.0</span><span class="sxs-lookup"><span data-stu-id="48449-223">1.10.0</span></span>](#1.10.0) |<span data-ttu-id="48449-224">2017년 3월 11일</span><span class="sxs-lookup"><span data-stu-id="48449-224">March 11, 2017</span></span> |--- |
| [<span data-ttu-id="48449-225">1.9.6</span><span class="sxs-lookup"><span data-stu-id="48449-225">1.9.6</span></span>](#1.9.6) |<span data-ttu-id="48449-226">2017년 2월 21일</span><span class="sxs-lookup"><span data-stu-id="48449-226">February 21, 2017</span></span> |--- |
| [<span data-ttu-id="48449-227">1.9.5</span><span class="sxs-lookup"><span data-stu-id="48449-227">1.9.5</span></span>](#1.9.5) |<span data-ttu-id="48449-228">2017년 1월 31일</span><span class="sxs-lookup"><span data-stu-id="48449-228">January 31, 2017</span></span> |--- |
| [<span data-ttu-id="48449-229">1.9.4</span><span class="sxs-lookup"><span data-stu-id="48449-229">1.9.4</span></span>](#1.9.4) |<span data-ttu-id="48449-230">2016년 11월 24일</span><span class="sxs-lookup"><span data-stu-id="48449-230">November 24, 2016</span></span> |--- |
| [<span data-ttu-id="48449-231">1.9.3</span><span class="sxs-lookup"><span data-stu-id="48449-231">1.9.3</span></span>](#1.9.3) |<span data-ttu-id="48449-232">2016년 10월 30일</span><span class="sxs-lookup"><span data-stu-id="48449-232">October 30, 2016</span></span> |--- |
| [<span data-ttu-id="48449-233">1.9.2</span><span class="sxs-lookup"><span data-stu-id="48449-233">1.9.2</span></span>](#1.9.2) |<span data-ttu-id="48449-234">2016년 10월 28일</span><span class="sxs-lookup"><span data-stu-id="48449-234">October 28, 2016</span></span> |--- |
| [<span data-ttu-id="48449-235">1.9.1</span><span class="sxs-lookup"><span data-stu-id="48449-235">1.9.1</span></span>](#1.9.1) |<span data-ttu-id="48449-236">2016년 10월 26일</span><span class="sxs-lookup"><span data-stu-id="48449-236">October 26, 2016</span></span> |--- |
| [<span data-ttu-id="48449-237">1.9.0</span><span class="sxs-lookup"><span data-stu-id="48449-237">1.9.0</span></span>](#1.9.0) |<span data-ttu-id="48449-238">2016년 10월 3일</span><span class="sxs-lookup"><span data-stu-id="48449-238">October 03, 2016</span></span> |--- |
| [<span data-ttu-id="48449-239">1.8.1</span><span class="sxs-lookup"><span data-stu-id="48449-239">1.8.1</span></span>](#1.8.1) |<span data-ttu-id="48449-240">2016년 6월 30일</span><span class="sxs-lookup"><span data-stu-id="48449-240">June 30, 2016</span></span> |--- |
| [<span data-ttu-id="48449-241">1.8.0</span><span class="sxs-lookup"><span data-stu-id="48449-241">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="48449-242">2016년 6월 14일</span><span class="sxs-lookup"><span data-stu-id="48449-242">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="48449-243">1.7.1</span><span class="sxs-lookup"><span data-stu-id="48449-243">1.7.1</span></span>](#1.7.1) |<span data-ttu-id="48449-244">2016년 4월 30일</span><span class="sxs-lookup"><span data-stu-id="48449-244">April 30, 2016</span></span> |--- |
| [<span data-ttu-id="48449-245">1.7.0</span><span class="sxs-lookup"><span data-stu-id="48449-245">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="48449-246">2016년 4월 27일</span><span class="sxs-lookup"><span data-stu-id="48449-246">April 27, 2016</span></span> |--- |
| [<span data-ttu-id="48449-247">1.6.0</span><span class="sxs-lookup"><span data-stu-id="48449-247">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="48449-248">2016년 3월 29일</span><span class="sxs-lookup"><span data-stu-id="48449-248">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="48449-249">1.5.1</span><span class="sxs-lookup"><span data-stu-id="48449-249">1.5.1</span></span>](#1.5.1) |<span data-ttu-id="48449-250">2015년 12월 31일</span><span class="sxs-lookup"><span data-stu-id="48449-250">December 31, 2015</span></span> |--- |
| [<span data-ttu-id="48449-251">1.5.0</span><span class="sxs-lookup"><span data-stu-id="48449-251">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="48449-252">2015년 12월 4일</span><span class="sxs-lookup"><span data-stu-id="48449-252">December 04, 2015</span></span> |--- |
| [<span data-ttu-id="48449-253">1.4.0</span><span class="sxs-lookup"><span data-stu-id="48449-253">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="48449-254">2015년 10월 5일</span><span class="sxs-lookup"><span data-stu-id="48449-254">October 05, 2015</span></span> |--- |
| [<span data-ttu-id="48449-255">1.3.0</span><span class="sxs-lookup"><span data-stu-id="48449-255">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="48449-256">2015년 10월 5일</span><span class="sxs-lookup"><span data-stu-id="48449-256">October 05, 2015</span></span> |--- |
| [<span data-ttu-id="48449-257">1.2.0</span><span class="sxs-lookup"><span data-stu-id="48449-257">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="48449-258">2015년 8월 5일</span><span class="sxs-lookup"><span data-stu-id="48449-258">August 05, 2015</span></span> |--- |
| [<span data-ttu-id="48449-259">1.1.0</span><span class="sxs-lookup"><span data-stu-id="48449-259">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="48449-260">2015년 7월 9일</span><span class="sxs-lookup"><span data-stu-id="48449-260">July 09, 2015</span></span> |--- |
| [<span data-ttu-id="48449-261">1.0.1</span><span class="sxs-lookup"><span data-stu-id="48449-261">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="48449-262">2015년 5월 12일</span><span class="sxs-lookup"><span data-stu-id="48449-262">May 12, 2015</span></span> |--- |
| [<span data-ttu-id="48449-263">1.0.0</span><span class="sxs-lookup"><span data-stu-id="48449-263">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="48449-264">2015년 4월 7일</span><span class="sxs-lookup"><span data-stu-id="48449-264">April 07, 2015</span></span> |--- |
| <span data-ttu-id="48449-265">0.9.5-prelease</span><span class="sxs-lookup"><span data-stu-id="48449-265">0.9.5-prelease</span></span> |<span data-ttu-id="48449-266">2015년 3월 9일</span><span class="sxs-lookup"><span data-stu-id="48449-266">Mar 09, 2015</span></span> |<span data-ttu-id="48449-267">2016년 2월 29일</span><span class="sxs-lookup"><span data-stu-id="48449-267">February 29, 2016</span></span> |
| <span data-ttu-id="48449-268">0.9.4-prelease</span><span class="sxs-lookup"><span data-stu-id="48449-268">0.9.4-prelease</span></span> |<span data-ttu-id="48449-269">2015년 2월 17일</span><span class="sxs-lookup"><span data-stu-id="48449-269">February 17, 2015</span></span> |<span data-ttu-id="48449-270">2016년 2월 29일</span><span class="sxs-lookup"><span data-stu-id="48449-270">February 29, 2016</span></span> |
| <span data-ttu-id="48449-271">0.9.3-prelease</span><span class="sxs-lookup"><span data-stu-id="48449-271">0.9.3-prelease</span></span> |<span data-ttu-id="48449-272">2015년 1월 13일</span><span class="sxs-lookup"><span data-stu-id="48449-272">January 13, 2015</span></span> |<span data-ttu-id="48449-273">2016년 2월 29일</span><span class="sxs-lookup"><span data-stu-id="48449-273">February 29, 2016</span></span> |
| <span data-ttu-id="48449-274">0.9.2-prelease</span><span class="sxs-lookup"><span data-stu-id="48449-274">0.9.2-prelease</span></span> |<span data-ttu-id="48449-275">2014년 12월 19일</span><span class="sxs-lookup"><span data-stu-id="48449-275">December 19, 2014</span></span> |<span data-ttu-id="48449-276">2016년 2월 29일</span><span class="sxs-lookup"><span data-stu-id="48449-276">February 29, 2016</span></span> |
| <span data-ttu-id="48449-277">0.9.1-prelease</span><span class="sxs-lookup"><span data-stu-id="48449-277">0.9.1-prelease</span></span> |<span data-ttu-id="48449-278">2014년 12월 19일</span><span class="sxs-lookup"><span data-stu-id="48449-278">December 19, 2014</span></span> |<span data-ttu-id="48449-279">2016년 2월 29일</span><span class="sxs-lookup"><span data-stu-id="48449-279">February 29, 2016</span></span> |
| <span data-ttu-id="48449-280">0.9.0-prelease</span><span class="sxs-lookup"><span data-stu-id="48449-280">0.9.0-prelease</span></span> |<span data-ttu-id="48449-281">2014년 12월 10일</span><span class="sxs-lookup"><span data-stu-id="48449-281">December 10, 2014</span></span> |<span data-ttu-id="48449-282">2016년 2월 29일</span><span class="sxs-lookup"><span data-stu-id="48449-282">February 29, 2016</span></span> |

## <a name="faq"></a><span data-ttu-id="48449-283">FAQ</span><span class="sxs-lookup"><span data-stu-id="48449-283">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="48449-284">참고 항목</span><span class="sxs-lookup"><span data-stu-id="48449-284">See Also</span></span>
<span data-ttu-id="48449-285">Cosmos DB에 대해 자세히 toolearn 참조 [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) 서비스 페이지.</span><span class="sxs-lookup"><span data-stu-id="48449-285">toolearn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span>


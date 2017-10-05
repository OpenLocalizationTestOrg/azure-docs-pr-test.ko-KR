---
title: "Azure Cosmos DB: DocumentDB Java API, SDK 및 리소스 | Microsoft Docs"
description: "릴리스 날짜, 사용 중지 날짜 및 Azure Cosmos DB DocumentDB Java SDK의 각 버전 간의 변경 내용을 포함하는 Java API 및 SDK에 대한 모든 것을 알아봅니다."
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
ms.openlocfilehash: 15e3f7ef3bfd6b1f61fe6081a378bdb29e0a1aa2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-documentdb-java-sdk-release-notes-and-resources"></a><span data-ttu-id="c5c4c-103">Azure Cosmos DB: DocumentDB Java SDK 릴리스 정보 및 리소스</span><span class="sxs-lookup"><span data-stu-id="c5c4c-103">Azure Cosmos DB: DocumentDB Java SDK release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c5c4c-104">.NET</span><span class="sxs-lookup"><span data-stu-id="c5c4c-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="c5c4c-105">.NET 변경 피드</span><span class="sxs-lookup"><span data-stu-id="c5c4c-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="c5c4c-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="c5c4c-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="c5c4c-107">Node.JS</span><span class="sxs-lookup"><span data-stu-id="c5c4c-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="c5c4c-108">Java</span><span class="sxs-lookup"><span data-stu-id="c5c4c-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="c5c4c-109">Python</span><span class="sxs-lookup"><span data-stu-id="c5c4c-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="c5c4c-110">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="c5c4c-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="c5c4c-111">REST 리소스 공급자</span><span class="sxs-lookup"><span data-stu-id="c5c4c-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="c5c4c-112">SQL</span><span class="sxs-lookup"><span data-stu-id="c5c4c-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="c5c4c-113">**SDK 다운로드**</span><span class="sxs-lookup"><span data-stu-id="c5c4c-113">**SDK Download**</span></span></td><td>[<span data-ttu-id="c5c4c-114">Maven</span><span class="sxs-lookup"><span data-stu-id="c5c4c-114">Maven</span></span>](http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22com.microsoft.azure%22%20AND%20a%3A%22azure-documentdb%22)</td></tr>

<tr><td><span data-ttu-id="c5c4c-115">**API 설명서**</span><span class="sxs-lookup"><span data-stu-id="c5c4c-115">**API documentation**</span></span></td><td>[<span data-ttu-id="c5c4c-116">Java API 참조 설명서</span><span class="sxs-lookup"><span data-stu-id="c5c4c-116">Java API reference documentation</span></span>](/java/api/com.microsoft.azure.documentdb)</td></tr>

<tr><td><span data-ttu-id="c5c4c-117">**SDK에 참여**</span><span class="sxs-lookup"><span data-stu-id="c5c4c-117">**Contribute to SDK**</span></span></td><td>[<span data-ttu-id="c5c4c-118">GitHub</span><span class="sxs-lookup"><span data-stu-id="c5c4c-118">GitHub</span></span>](https://github.com/Azure/azure-documentdb-java/)</td></tr>

<tr><td><span data-ttu-id="c5c4c-119">**시작**</span><span class="sxs-lookup"><span data-stu-id="c5c4c-119">**Get started**</span></span></td><td>[<span data-ttu-id="c5c4c-120">Java SDK 시작</span><span class="sxs-lookup"><span data-stu-id="c5c4c-120">Get started with the Java SDK</span></span>](documentdb-java-get-started.md)</td></tr>

<tr><td><span data-ttu-id="c5c4c-121">**웹앱 자습서**</span><span class="sxs-lookup"><span data-stu-id="c5c4c-121">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="c5c4c-122">Azure Cosmos DB를 사용한 웹 응용 프로그램 개발</span><span class="sxs-lookup"><span data-stu-id="c5c4c-122">Web application development with Azure Cosmos DB</span></span>](documentdb-java-application.md)</td></tr>

<tr><td><span data-ttu-id="c5c4c-123">**현재 지원되는 런타임**</span><span class="sxs-lookup"><span data-stu-id="c5c4c-123">**Current supported runtime**</span></span></td><td>[<span data-ttu-id="c5c4c-124">JDK 7</span><span class="sxs-lookup"><span data-stu-id="c5c4c-124">JDK 7</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)</td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="c5c4c-125">릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="c5c4c-125">Release Notes</span></span>

### <a name="a-name11201120"></a><span data-ttu-id="c5c4c-126"><a name="1.12.0"/>1.12.0</span><span class="sxs-lookup"><span data-stu-id="c5c4c-126"><a name="1.12.0"/>1.12.0</span></span>
* <span data-ttu-id="c5c4c-127">파티션 분할 동안 요청 처리에 대한 중요한 버그 수정.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-127">Critical bug fixes to request processing during partition splits.</span></span>
* <span data-ttu-id="c5c4c-128">Strong 및 BoundedStaleness 일관성 수준 관련 문제를 수정했습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-128">Fixed an issue with the Strong and BoundedStaleness consistency levels.</span></span>

### <a name="a-name11101110"></a><span data-ttu-id="c5c4c-129"><a name="1.11.0"/>1.11.0</span><span class="sxs-lookup"><span data-stu-id="c5c4c-129"><a name="1.11.0"/>1.11.0</span></span>
* <span data-ttu-id="c5c4c-130">ConsistentPrefix라는 새로운 일관성 수준에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-130">Added support for a new consistency level called ConsistentPrefix.</span></span>
* <span data-ttu-id="c5c4c-131">세션 모드에서 컬렉션을 읽을 때 발생하는 버그를 수정했습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-131">Fixed a bug in reading collection in session mode.</span></span>

### <a name="a-name11001100"></a><span data-ttu-id="c5c4c-132"><a name="1.10.0"/>1.10.0</span><span class="sxs-lookup"><span data-stu-id="c5c4c-132"><a name="1.10.0"/>1.10.0</span></span>
* <span data-ttu-id="c5c4c-133">초당 2,500 RU 및 초당 100 RU의 규모 조정 능력을 통해 분할된 컬렉션을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-133">Enabled support for partitioned collection with as low as 2,500 RU/sec and scale in increments of 100 RU/sec.</span></span>
* <span data-ttu-id="c5c4c-134">일부 쿼리에서 NullRef 예외를 일으킬 수 있는 네이티브 어셈블리 버그를 수정했습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-134">Fixed a bug in the native assembly which can cause NullRef exception in some queries.</span></span>

### <a name="a-name196196"></a><span data-ttu-id="c5c4c-135"><a name="1.9.6"/>1.9.6</span><span class="sxs-lookup"><span data-stu-id="c5c4c-135"><a name="1.9.6"/>1.9.6</span></span>
* <span data-ttu-id="c5c4c-136">게이트웨이 모드에서 쿼리에 대한 예외를 일으킬 수 있는 쿼리 엔진 구성에서 버그를 수정했습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-136">Fixed a bug in the query engine configuration that may cause exceptions for queries in Gateway mode.</span></span>
* <span data-ttu-id="c5c4c-137">컬렉션을 만든 후 즉시 요청에 대한 "소유자 리소스를 찾을 수 없습니다." 예외를 일으킬 수 있는 세션 컨테이너에 몇 가지 버그가 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-137">Fixed a few bugs in the session container that may cause an "Owner resource not found" exception for requests immediately after collection creation.</span></span>

### <a name="a-name195195"></a><span data-ttu-id="c5c4c-138"><a name="1.9.5"/>1.9.5</span><span class="sxs-lookup"><span data-stu-id="c5c4c-138"><a name="1.9.5"/>1.9.5</span></span>
* <span data-ttu-id="c5c4c-139">집계 쿼리(COUNT, MIN, MAX, SUM 및 AVG)에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-139">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span> <span data-ttu-id="c5c4c-140">[집계 지원](documentdb-sql-query.md#Aggregates)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-140">See [Aggregation support](documentdb-sql-query.md#Aggregates).</span></span>
* <span data-ttu-id="c5c4c-141">변경 피드에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-141">Added support for change feed.</span></span>
* <span data-ttu-id="c5c4c-142">RequestOptions.setPopulateQuotaInfo를 통한 컬렉션 할당량 정보에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-142">Added support for collection quota information through RequestOptions.setPopulateQuotaInfo.</span></span>
* <span data-ttu-id="c5c4c-143">RequestOptions.setScriptLoggingEnabled를 통한 저장 프로시저 스크립트에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-143">Added support for stored procedure script logging through RequestOptions.setScriptLoggingEnabled.</span></span>
* <span data-ttu-id="c5c4c-144">제한 오류가 발생할 때 DirectHttps 모드의 쿼리가 중단될 수 있는 버그를 수정했습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-144">Fixed a bug where query in DirectHttps mode may hang when encountering throttle failures.</span></span>
* <span data-ttu-id="c5c4c-145">세션 일관성 모드의 버그를 수정했습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-145">Fixed a bug in session consistency mode.</span></span>
* <span data-ttu-id="c5c4c-146">요청 속도가 높은 경우 HttpContext에서 NullReferenceException을 유발할 수 있는 버그를 수정했습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-146">Fixed a bug which may cause NullReferenceException in HttpContext when request rate is high.</span></span>
* <span data-ttu-id="c5c4c-147">DirectHttps 모드의 성능이 향상되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-147">Improved performance of DirectHttps mode.</span></span>

### <a name="a-name194194"></a><span data-ttu-id="c5c4c-148"><a name="1.9.4"/>1.9.4</span><span class="sxs-lookup"><span data-stu-id="c5c4c-148"><a name="1.9.4"/>1.9.4</span></span>
* <span data-ttu-id="c5c4c-149">ConnectionPolicy.setProxy() API와 함께 샘플 클라이언트 인스턴스 기반 프록시 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-149">Added simple client instance-based proxy support with ConnectionPolicy.setProxy() API.</span></span>
* <span data-ttu-id="c5c4c-150">DocumentClient 인스턴스를 올바르게 종료하기 위한 DocumentClient.close() API가 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-150">Added DocumentClient.close() API to properly shutdown DocumentClient instance.</span></span>
* <span data-ttu-id="c5c4c-151">게이트웨이 대신 네이티브 어셈블리에서 쿼리 계획을 파생하여 직접 연결 모드의 쿼리 성능을 개선했습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-151">Improved query performance in direct connectivity mode by deriving the query plan from the native assembly instead of the Gateway.</span></span>
* <span data-ttu-id="c5c4c-152">사용자가 POJO에서 JsonIgnoreProperties를 정의할 필요가 없도록 FAIL_ON_UNKNOWN_PROPERTIES = false로 설정했습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-152">Set FAIL_ON_UNKNOWN_PROPERTIES = false so users don't need to define JsonIgnoreProperties in their POJO.</span></span>
* <span data-ttu-id="c5c4c-153">SLF4J를 사용하도록 로깅을 리팩터링했습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-153">Refactored logging to use SLF4J.</span></span>
* <span data-ttu-id="c5c4c-154">일관성 판독기의 몇 가지 버그를 수정했습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-154">Fixed a few other bugs in consistency reader.</span></span>

### <a name="a-name193193"></a><span data-ttu-id="c5c4c-155"><a name="1.9.3"/>1.9.3</span><span class="sxs-lookup"><span data-stu-id="c5c4c-155"><a name="1.9.3"/>1.9.3</span></span>
* <span data-ttu-id="c5c4c-156">직접 연결 모드에서 연결 누수를 방지하기 위해 연결 관리의 버그를 수정했습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-156">Fixed a bug in the connection management to prevent connection leaks in direct connectivity mode.</span></span>
* <span data-ttu-id="c5c4c-157">NullReferenece 예외가 throw 될 수 있는 상위 쿼리의 버그를 수정했습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-157">Fixed a bug in the TOP query where it may throw NullReferenece exception.</span></span>
* <span data-ttu-id="c5c4c-158">내부 캐시에 대한 네트워크 호출의 수를 줄여 성능을 개선했습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-158">Improved performance by reducing the number of network call for the internal caches.</span></span>
* <span data-ttu-id="c5c4c-159">DocumentClientException에 상태 코드 ActivityID 및 요청 URI를 추가하여 문제 해결을 개선했습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-159">Added status code, ActivityID and Request URI in DocumentClientException for better troubleshooting.</span></span>

### <a name="a-name192192"></a><span data-ttu-id="c5c4c-160"><a name="1.9.2"/>1.9.2</span><span class="sxs-lookup"><span data-stu-id="c5c4c-160"><a name="1.9.2"/>1.9.2</span></span>
* <span data-ttu-id="c5c4c-161">연결 관리의 문제를 해결하여 안정성을 높였습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-161">Fixed an issue in the connection management for stability.</span></span>

### <a name="a-name191191"></a><span data-ttu-id="c5c4c-162"><a name="1.9.1"/>1.9.1</span><span class="sxs-lookup"><span data-stu-id="c5c4c-162"><a name="1.9.1"/>1.9.1</span></span>
* <span data-ttu-id="c5c4c-163">BoundedStaleness 일관성 수준에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-163">Added support for BoundedStaleness consistency level.</span></span>
* <span data-ttu-id="c5c4c-164">분할된 컬렉션의 CRUD 작업에 대한 직접 연결 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-164">Added support for direct connectivity for CRUD operations for partitioned collections.</span></span>
* <span data-ttu-id="c5c4c-165">SQL을 사용하여 데이터베이스를 쿼리할 때의 버그가 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-165">Fixed a bug in querying a database with SQL.</span></span>
* <span data-ttu-id="c5c4c-166">세션 토큰이 잘못 설정된 경우에 발생할 수 있는 세션 캐시의 버그가 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-166">Fixed a bug in the session cache where session token may be set incorrectly.</span></span>

### <a name="a-name190190"></a><span data-ttu-id="c5c4c-167"><a name="1.9.0"/>1.9.0</span><span class="sxs-lookup"><span data-stu-id="c5c4c-167"><a name="1.9.0"/>1.9.0</span></span>
* <span data-ttu-id="c5c4c-168">파티션 간 병렬 쿼리에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-168">Added support for cross partition parallel queries.</span></span>
* <span data-ttu-id="c5c4c-169">분할된 컬렉션의 TOP/ORDER BY 쿼리에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-169">Added support for TOP/ORDER BY queries for partitioned collections.</span></span>
* <span data-ttu-id="c5c4c-170">강력한 일관성에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-170">Added support for strong consistency.</span></span>
* <span data-ttu-id="c5c4c-171">직접 연결을 사용할 때 이름 기반 요청에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-171">Added support for name based requests when using direct connectivity.</span></span>
* <span data-ttu-id="c5c4c-172">모든 요청 다시 시도 간에 ActivityId가 일관성을 유지하도록 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-172">Fixed to make ActivityId stay consistent across all request retries.</span></span>
* <span data-ttu-id="c5c4c-173">동일한 이름의 컬렉션을 다시 만들 때 세션 캐시와 관련된 버그가 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-173">Fixed a bug related to the session cache when recreating a collection with the same name.</span></span>
* <span data-ttu-id="c5c4c-174">지역 펜싱 공간 쿼리에 대한 컬렉션 인덱싱 정책을 지정하는 동안 Polygon 및 LineString 데이터 형식이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-174">Added Polygon and LineString DataTypes while specifying collection indexing policy for geo-fencing spatial queries.</span></span>
* <span data-ttu-id="c5c4c-175">Java 1.8용 Java 문서 관련 문제가 해결되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-175">Fixed issues with Java Doc for Java 1.8.</span></span>

### <a name="a-name181181"></a><span data-ttu-id="c5c4c-176"><a name="1.8.1"/>1.8.1</span><span class="sxs-lookup"><span data-stu-id="c5c4c-176"><a name="1.8.1"/>1.8.1</span></span>
* <span data-ttu-id="c5c4c-177">PartitionKeyDefinitionMap에서 버그를 수정하여 단일 파티션 컬렉션을 캐시하고 추가 인출 파티션 키를 요청하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-177">Fixed a bug in PartitionKeyDefinitionMap to cache single partition collections and not make extra fetch partition key requests.</span></span>
* <span data-ttu-id="c5c4c-178">잘못된 파티션 키 값이 제공되는 경우 버그가 다시 시도되지 않도록 수정했습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-178">Fixed a bug to not retry when an incorrect partition key value is provided.</span></span>

### <a name="a-name180180"></a><span data-ttu-id="c5c4c-179"><a name="1.8.0"/>1.8.0</span><span class="sxs-lookup"><span data-stu-id="c5c4c-179"><a name="1.8.0"/>1.8.0</span></span>
* <span data-ttu-id="c5c4c-180">다중 지역 데이터베이스 계정에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-180">Added the support for multi-region database accounts.</span></span>
* <span data-ttu-id="c5c4c-181">최대 재시도 횟수와 최대 재시도 대기 시간을 지정하는 옵션과 함께 정제된 요청의 자동 재시도 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-181">Added support for automatic retry on throttled requests with options to customize the max retry attempts and max retry wait time.</span></span>  <span data-ttu-id="c5c4c-182">RetryOptions와 ConnectionPolicy.getRetryOptions()을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-182">See RetryOptions and ConnectionPolicy.getRetryOptions().</span></span>
* <span data-ttu-id="c5c4c-183">IPartitionResolver 기반 사용자 지정 파티셔닝 코드의 사용이 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-183">Deprecated IPartitionResolver based custom partitioning code.</span></span> <span data-ttu-id="c5c4c-184">보다 큰 저장소 및 처리량에는 파티션된 컬렉션을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-184">Please use partitioned collections for higher storage and throughput.</span></span>

### <a name="a-name171171"></a><span data-ttu-id="c5c4c-185"><a name="1.7.1"/>1.7.1</span><span class="sxs-lookup"><span data-stu-id="c5c4c-185"><a name="1.7.1"/>1.7.1</span></span>
* <span data-ttu-id="c5c4c-186">제한에 대한 재시도 정책 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-186">Added retry policy support for throttling.</span></span>  

### <a name="a-name170170"></a><span data-ttu-id="c5c4c-187"><a name="1.7.0"/>1.7.0</span><span class="sxs-lookup"><span data-stu-id="c5c4c-187"><a name="1.7.0"/>1.7.0</span></span>
* <span data-ttu-id="c5c4c-188">문서에 대한 TTL(Time to Live) 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-188">Added time to live (TTL) support for documents.</span></span>

### <a name="a-name160160"></a><span data-ttu-id="c5c4c-189"><a name="1.6.0"/>1.6.0</span><span class="sxs-lookup"><span data-stu-id="c5c4c-189"><a name="1.6.0"/>1.6.0</span></span>
* <span data-ttu-id="c5c4c-190">[분할된 컬렉션](partition-data.md) 및 [사용자 정의 성능 수준](performance-levels.md)이 구현되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-190">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span>

### <a name="a-name151151"></a><span data-ttu-id="c5c4c-191"><a name="1.5.1"/>1.5.1</span><span class="sxs-lookup"><span data-stu-id="c5c4c-191"><a name="1.5.1"/>1.5.1</span></span>
* <span data-ttu-id="c5c4c-192">다른 SDK와 일치하도록 little-endian의 해시 값을 생성하는 HashPartitionResolver의 버그를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-192">Fixed a bug in HashPartitionResolver to generate hash values in little-endian to be consistent with other SDKs.</span></span>

### <a name="a-name150150"></a><span data-ttu-id="c5c4c-193"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="c5c4c-193"><a name="1.5.0"/>1.5.0</span></span>
* <span data-ttu-id="c5c4c-194">여러 파티션 간의 응용 프로그램 분할을 지원하기 위해 해시 및 범위 파티션 해결 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-194">Add Hash & Range partition resolvers to assist with sharding applications across multiple partitions.</span></span>

### <a name="a-name140140"></a><span data-ttu-id="c5c4c-195"><a name="1.4.0"/>1.4.0</span><span class="sxs-lookup"><span data-stu-id="c5c4c-195"><a name="1.4.0"/>1.4.0</span></span>
* <span data-ttu-id="c5c4c-196">Upsert를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-196">Implement Upsert.</span></span> <span data-ttu-id="c5c4c-197">새로운 upsertXXX 메서드가 Upsert 기능을 지원하기 위해 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-197">New upsertXXX methods added to support Upsert feature.</span></span>
* <span data-ttu-id="c5c4c-198">ID 기반 라우팅을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-198">Implement ID Based Routing.</span></span> <span data-ttu-id="c5c4c-199">공용 API 변경 없이 모두 내부에서 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-199">No public API changes, all changes internal.</span></span>

### <a name="a-name130130"></a><span data-ttu-id="c5c4c-200"><a name="1.3.0"/>1.3.0</span><span class="sxs-lookup"><span data-stu-id="c5c4c-200"><a name="1.3.0"/>1.3.0</span></span>
* <span data-ttu-id="c5c4c-201">다른 SDK와 일치하는 버전 번호 가져오기를 생략하는 릴리스</span><span class="sxs-lookup"><span data-stu-id="c5c4c-201">Release skipped to bring version number in alignment with other SDKs</span></span>

### <a name="a-name120120"></a><span data-ttu-id="c5c4c-202"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="c5c4c-202"><a name="1.2.0"/>1.2.0</span></span>
* <span data-ttu-id="c5c4c-203">지리 공간 인덱스 지원</span><span class="sxs-lookup"><span data-stu-id="c5c4c-203">Supports GeoSpatial Index</span></span>
* <span data-ttu-id="c5c4c-204">모든 리소스에 대한 ID 속성의 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-204">Validates id property for all resources.</span></span> <span data-ttu-id="c5c4c-205">리소스에 대한 ID는 ?, /, #, \, 문자를 포함하거나 공백으로 끝날 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-205">Ids for resources cannot contain ?, /, #, \, characters or end with a space.</span></span>
* <span data-ttu-id="c5c4c-206">ResourceResponse에 새 헤더 "인덱스 변환 진행"을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-206">Adds new header "index transformation progress" to ResourceResponse.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="c5c4c-207"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="c5c4c-207"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="c5c4c-208">V2 인덱싱 정책 구현</span><span class="sxs-lookup"><span data-stu-id="c5c4c-208">Implements V2 indexing policy</span></span>

### <a name="a-name100100"></a><span data-ttu-id="c5c4c-209"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="c5c4c-209"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="c5c4c-210">GA SDK</span><span class="sxs-lookup"><span data-stu-id="c5c4c-210">GA SDK</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="c5c4c-211">릴리스 및 사용 중지 날짜</span><span class="sxs-lookup"><span data-stu-id="c5c4c-211">Release & Retirement Dates</span></span>
<span data-ttu-id="c5c4c-212">Microsoft는 매끄럽게 최신/지원 버전으로 전환할 수 있도록 적어도 SDK 사용 중지 **12개월** 전에 알림을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-212">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order to smooth the transition to a newer/supported version.</span></span>

<span data-ttu-id="c5c4c-213">새로운 기능 및 최적화는 현재 SDK에만 추가되어 있으며, 따라서 항상 최신 SDK 버전으로 가능한 한 빨리 업그레이드할 것을 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-213">New features and functionality and optimizations are only added to the current SDK, as such it is  recommend that you always upgrade to the latest SDK version as early as possible.</span></span>

<span data-ttu-id="c5c4c-214">사용 중지된 SDK를 사용하는 Cosmos DB에 대한 요청은 서비스에서 거부됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-214">Any request to Cosmos DB using a retired SDK will be rejected by the service.</span></span>

> [!WARNING]
> <span data-ttu-id="c5c4c-215">**1.0.0** 이전 버전의 Java에 대한 모든 버전의 DocumentDB SDK는 **2016년 2월 29일**에 사용 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-215">All versions of the DocumentDB SDK for Java prior to version **1.0.0** will be retired on **February 29, 2016**.</span></span>
> 
> 

<br/>

| <span data-ttu-id="c5c4c-216">버전</span><span class="sxs-lookup"><span data-stu-id="c5c4c-216">Version</span></span> | <span data-ttu-id="c5c4c-217">릴리스 날짜</span><span class="sxs-lookup"><span data-stu-id="c5c4c-217">Release Date</span></span> | <span data-ttu-id="c5c4c-218">사용 중지 날짜</span><span class="sxs-lookup"><span data-stu-id="c5c4c-218">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="c5c4c-219">1.12.0</span><span class="sxs-lookup"><span data-stu-id="c5c4c-219">1.12.0</span></span>](#1.12.0) |<span data-ttu-id="c5c4c-220">2017년 7월 11일</span><span class="sxs-lookup"><span data-stu-id="c5c4c-220">July 11, 2017</span></span> |--- |
| [<span data-ttu-id="c5c4c-221">1.11.0</span><span class="sxs-lookup"><span data-stu-id="c5c4c-221">1.11.0</span></span>](#1.11.0) |<span data-ttu-id="c5c4c-222">2017년 5월 10일</span><span class="sxs-lookup"><span data-stu-id="c5c4c-222">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="c5c4c-223">1.10.0</span><span class="sxs-lookup"><span data-stu-id="c5c4c-223">1.10.0</span></span>](#1.10.0) |<span data-ttu-id="c5c4c-224">2017년 3월 11일</span><span class="sxs-lookup"><span data-stu-id="c5c4c-224">March 11, 2017</span></span> |--- |
| [<span data-ttu-id="c5c4c-225">1.9.6</span><span class="sxs-lookup"><span data-stu-id="c5c4c-225">1.9.6</span></span>](#1.9.6) |<span data-ttu-id="c5c4c-226">2017년 2월 21일</span><span class="sxs-lookup"><span data-stu-id="c5c4c-226">February 21, 2017</span></span> |--- |
| [<span data-ttu-id="c5c4c-227">1.9.5</span><span class="sxs-lookup"><span data-stu-id="c5c4c-227">1.9.5</span></span>](#1.9.5) |<span data-ttu-id="c5c4c-228">2017년 1월 31일</span><span class="sxs-lookup"><span data-stu-id="c5c4c-228">January 31, 2017</span></span> |--- |
| [<span data-ttu-id="c5c4c-229">1.9.4</span><span class="sxs-lookup"><span data-stu-id="c5c4c-229">1.9.4</span></span>](#1.9.4) |<span data-ttu-id="c5c4c-230">2016년 11월 24일</span><span class="sxs-lookup"><span data-stu-id="c5c4c-230">November 24, 2016</span></span> |--- |
| [<span data-ttu-id="c5c4c-231">1.9.3</span><span class="sxs-lookup"><span data-stu-id="c5c4c-231">1.9.3</span></span>](#1.9.3) |<span data-ttu-id="c5c4c-232">2016년 10월 30일</span><span class="sxs-lookup"><span data-stu-id="c5c4c-232">October 30, 2016</span></span> |--- |
| [<span data-ttu-id="c5c4c-233">1.9.2</span><span class="sxs-lookup"><span data-stu-id="c5c4c-233">1.9.2</span></span>](#1.9.2) |<span data-ttu-id="c5c4c-234">2016년 10월 28일</span><span class="sxs-lookup"><span data-stu-id="c5c4c-234">October 28, 2016</span></span> |--- |
| [<span data-ttu-id="c5c4c-235">1.9.1</span><span class="sxs-lookup"><span data-stu-id="c5c4c-235">1.9.1</span></span>](#1.9.1) |<span data-ttu-id="c5c4c-236">2016년 10월 26일</span><span class="sxs-lookup"><span data-stu-id="c5c4c-236">October 26, 2016</span></span> |--- |
| [<span data-ttu-id="c5c4c-237">1.9.0</span><span class="sxs-lookup"><span data-stu-id="c5c4c-237">1.9.0</span></span>](#1.9.0) |<span data-ttu-id="c5c4c-238">2016년 10월 3일</span><span class="sxs-lookup"><span data-stu-id="c5c4c-238">October 03, 2016</span></span> |--- |
| [<span data-ttu-id="c5c4c-239">1.8.1</span><span class="sxs-lookup"><span data-stu-id="c5c4c-239">1.8.1</span></span>](#1.8.1) |<span data-ttu-id="c5c4c-240">2016년 6월 30일</span><span class="sxs-lookup"><span data-stu-id="c5c4c-240">June 30, 2016</span></span> |--- |
| [<span data-ttu-id="c5c4c-241">1.8.0</span><span class="sxs-lookup"><span data-stu-id="c5c4c-241">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="c5c4c-242">2016년 6월 14일</span><span class="sxs-lookup"><span data-stu-id="c5c4c-242">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="c5c4c-243">1.7.1</span><span class="sxs-lookup"><span data-stu-id="c5c4c-243">1.7.1</span></span>](#1.7.1) |<span data-ttu-id="c5c4c-244">2016년 4월 30일</span><span class="sxs-lookup"><span data-stu-id="c5c4c-244">April 30, 2016</span></span> |--- |
| [<span data-ttu-id="c5c4c-245">1.7.0</span><span class="sxs-lookup"><span data-stu-id="c5c4c-245">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="c5c4c-246">2016년 4월 27일</span><span class="sxs-lookup"><span data-stu-id="c5c4c-246">April 27, 2016</span></span> |--- |
| [<span data-ttu-id="c5c4c-247">1.6.0</span><span class="sxs-lookup"><span data-stu-id="c5c4c-247">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="c5c4c-248">2016년 3월 29일</span><span class="sxs-lookup"><span data-stu-id="c5c4c-248">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="c5c4c-249">1.5.1</span><span class="sxs-lookup"><span data-stu-id="c5c4c-249">1.5.1</span></span>](#1.5.1) |<span data-ttu-id="c5c4c-250">2015년 12월 31일</span><span class="sxs-lookup"><span data-stu-id="c5c4c-250">December 31, 2015</span></span> |--- |
| [<span data-ttu-id="c5c4c-251">1.5.0</span><span class="sxs-lookup"><span data-stu-id="c5c4c-251">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="c5c4c-252">2015년 12월 4일</span><span class="sxs-lookup"><span data-stu-id="c5c4c-252">December 04, 2015</span></span> |--- |
| [<span data-ttu-id="c5c4c-253">1.4.0</span><span class="sxs-lookup"><span data-stu-id="c5c4c-253">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="c5c4c-254">2015년 10월 5일</span><span class="sxs-lookup"><span data-stu-id="c5c4c-254">October 05, 2015</span></span> |--- |
| [<span data-ttu-id="c5c4c-255">1.3.0</span><span class="sxs-lookup"><span data-stu-id="c5c4c-255">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="c5c4c-256">2015년 10월 5일</span><span class="sxs-lookup"><span data-stu-id="c5c4c-256">October 05, 2015</span></span> |--- |
| [<span data-ttu-id="c5c4c-257">1.2.0</span><span class="sxs-lookup"><span data-stu-id="c5c4c-257">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="c5c4c-258">2015년 8월 5일</span><span class="sxs-lookup"><span data-stu-id="c5c4c-258">August 05, 2015</span></span> |--- |
| [<span data-ttu-id="c5c4c-259">1.1.0</span><span class="sxs-lookup"><span data-stu-id="c5c4c-259">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="c5c4c-260">2015년 7월 9일</span><span class="sxs-lookup"><span data-stu-id="c5c4c-260">July 09, 2015</span></span> |--- |
| [<span data-ttu-id="c5c4c-261">1.0.1</span><span class="sxs-lookup"><span data-stu-id="c5c4c-261">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="c5c4c-262">2015년 5월 12일</span><span class="sxs-lookup"><span data-stu-id="c5c4c-262">May 12, 2015</span></span> |--- |
| [<span data-ttu-id="c5c4c-263">1.0.0</span><span class="sxs-lookup"><span data-stu-id="c5c4c-263">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="c5c4c-264">2015년 4월 7일</span><span class="sxs-lookup"><span data-stu-id="c5c4c-264">April 07, 2015</span></span> |--- |
| <span data-ttu-id="c5c4c-265">0.9.5-prelease</span><span class="sxs-lookup"><span data-stu-id="c5c4c-265">0.9.5-prelease</span></span> |<span data-ttu-id="c5c4c-266">2015년 3월 9일</span><span class="sxs-lookup"><span data-stu-id="c5c4c-266">Mar 09, 2015</span></span> |<span data-ttu-id="c5c4c-267">2016년 2월 29일</span><span class="sxs-lookup"><span data-stu-id="c5c4c-267">February 29, 2016</span></span> |
| <span data-ttu-id="c5c4c-268">0.9.4-prelease</span><span class="sxs-lookup"><span data-stu-id="c5c4c-268">0.9.4-prelease</span></span> |<span data-ttu-id="c5c4c-269">2015년 2월 17일</span><span class="sxs-lookup"><span data-stu-id="c5c4c-269">February 17, 2015</span></span> |<span data-ttu-id="c5c4c-270">2016년 2월 29일</span><span class="sxs-lookup"><span data-stu-id="c5c4c-270">February 29, 2016</span></span> |
| <span data-ttu-id="c5c4c-271">0.9.3-prelease</span><span class="sxs-lookup"><span data-stu-id="c5c4c-271">0.9.3-prelease</span></span> |<span data-ttu-id="c5c4c-272">2015년 1월 13일</span><span class="sxs-lookup"><span data-stu-id="c5c4c-272">January 13, 2015</span></span> |<span data-ttu-id="c5c4c-273">2016년 2월 29일</span><span class="sxs-lookup"><span data-stu-id="c5c4c-273">February 29, 2016</span></span> |
| <span data-ttu-id="c5c4c-274">0.9.2-prelease</span><span class="sxs-lookup"><span data-stu-id="c5c4c-274">0.9.2-prelease</span></span> |<span data-ttu-id="c5c4c-275">2014년 12월 19일</span><span class="sxs-lookup"><span data-stu-id="c5c4c-275">December 19, 2014</span></span> |<span data-ttu-id="c5c4c-276">2016년 2월 29일</span><span class="sxs-lookup"><span data-stu-id="c5c4c-276">February 29, 2016</span></span> |
| <span data-ttu-id="c5c4c-277">0.9.1-prelease</span><span class="sxs-lookup"><span data-stu-id="c5c4c-277">0.9.1-prelease</span></span> |<span data-ttu-id="c5c4c-278">2014년 12월 19일</span><span class="sxs-lookup"><span data-stu-id="c5c4c-278">December 19, 2014</span></span> |<span data-ttu-id="c5c4c-279">2016년 2월 29일</span><span class="sxs-lookup"><span data-stu-id="c5c4c-279">February 29, 2016</span></span> |
| <span data-ttu-id="c5c4c-280">0.9.0-prelease</span><span class="sxs-lookup"><span data-stu-id="c5c4c-280">0.9.0-prelease</span></span> |<span data-ttu-id="c5c4c-281">2014년 12월 10일</span><span class="sxs-lookup"><span data-stu-id="c5c4c-281">December 10, 2014</span></span> |<span data-ttu-id="c5c4c-282">2016년 2월 29일</span><span class="sxs-lookup"><span data-stu-id="c5c4c-282">February 29, 2016</span></span> |

## <a name="faq"></a><span data-ttu-id="c5c4c-283">FAQ</span><span class="sxs-lookup"><span data-stu-id="c5c4c-283">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="c5c4c-284">참고 항목</span><span class="sxs-lookup"><span data-stu-id="c5c4c-284">See Also</span></span>
<span data-ttu-id="c5c4c-285">Cosmos DB에 대한 자세한 내용은 [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) 서비스 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c5c4c-285">To learn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span>


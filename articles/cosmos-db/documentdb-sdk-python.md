---
title: "Azure Cosmos DB Python API, SDK 및 리소스 | Microsoft Docs"
description: "릴리스 날짜, 사용 중지 날짜 및 Azure Cosmos DB Python SDK의 각 버전 간의 변경 내용을 포함하는 Python API 및 SDK에 대한 모든 것을 알아봅니다."
services: cosmos-db
documentationcenter: python
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 3ac344a9-b2fa-4a3f-a4cc-02d287e05469
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/24/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 70d2550f713ff0e9daed235eb8053589b8682633
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-python-sdk-release-notes-and-resources"></a><span data-ttu-id="08ede-103">Azure Cosmos DB Python SDK: 릴리스 정보 및 리소스</span><span class="sxs-lookup"><span data-stu-id="08ede-103">Azure Cosmos DB Python SDK: Release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="08ede-104">.NET</span><span class="sxs-lookup"><span data-stu-id="08ede-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="08ede-105">.NET 변경 피드</span><span class="sxs-lookup"><span data-stu-id="08ede-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="08ede-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="08ede-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="08ede-107">Node.JS</span><span class="sxs-lookup"><span data-stu-id="08ede-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="08ede-108">Java</span><span class="sxs-lookup"><span data-stu-id="08ede-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="08ede-109">Python</span><span class="sxs-lookup"><span data-stu-id="08ede-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="08ede-110">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="08ede-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="08ede-111">REST 리소스 공급자</span><span class="sxs-lookup"><span data-stu-id="08ede-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="08ede-112">SQL</span><span class="sxs-lookup"><span data-stu-id="08ede-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="08ede-113">**SDK 다운로드**</span><span class="sxs-lookup"><span data-stu-id="08ede-113">**Download SDK**</span></span></td><td>[<span data-ttu-id="08ede-114">PyPI</span><span class="sxs-lookup"><span data-stu-id="08ede-114">PyPI</span></span>](https://pypi.python.org/pypi/pydocumentdb)</td></tr>

<tr><td><span data-ttu-id="08ede-115">**API 설명서**</span><span class="sxs-lookup"><span data-stu-id="08ede-115">**API documentation**</span></span></td><td>[<span data-ttu-id="08ede-116">Python API 참조 설명서</span><span class="sxs-lookup"><span data-stu-id="08ede-116">Python API reference documentation</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.html)</td></tr>

<tr><td><span data-ttu-id="08ede-117">**SDK 설치 지침**</span><span class="sxs-lookup"><span data-stu-id="08ede-117">**SDK installation instructions**</span></span></td><td>[<span data-ttu-id="08ede-118">Python SDK 설치 지침</span><span class="sxs-lookup"><span data-stu-id="08ede-118">Python SDK installation instructions</span></span>](http://azure.github.io/azure-documentdb-python/)</td></tr>

<tr><td><span data-ttu-id="08ede-119">**SDK에 참여**</span><span class="sxs-lookup"><span data-stu-id="08ede-119">**Contribute to SDK**</span></span></td><td>[<span data-ttu-id="08ede-120">GitHub</span><span class="sxs-lookup"><span data-stu-id="08ede-120">GitHub</span></span>](https://github.com/Azure/azure-documentdb-python)</td></tr>

<tr><td><span data-ttu-id="08ede-121">**시작**</span><span class="sxs-lookup"><span data-stu-id="08ede-121">**Get started**</span></span></td><td>[<span data-ttu-id="08ede-122">Python SDK 시작</span><span class="sxs-lookup"><span data-stu-id="08ede-122">Get started with the Python SDK</span></span>](documentdb-python-application.md)</td></tr>

<tr><td><span data-ttu-id="08ede-123">**현재 지원되는 플랫폼**</span><span class="sxs-lookup"><span data-stu-id="08ede-123">**Current supported platform**</span></span></td><td><span data-ttu-id="08ede-124">[Python 2.7](https://www.python.org/downloads/) 및 [Python 3.5](https://www.python.org/downloads/)</span><span class="sxs-lookup"><span data-stu-id="08ede-124">[Python 2.7](https://www.python.org/downloads/) and [Python 3.5](https://www.python.org/downloads/)</span></span></td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="08ede-125">릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="08ede-125">Release notes</span></span>
### <a name="a-name220220"></a><span data-ttu-id="08ede-126"><a name="2.2.0"/>2.2.0</span><span class="sxs-lookup"><span data-stu-id="08ede-126"><a name="2.2.0"/>2.2.0</span></span>
* <span data-ttu-id="08ede-127">ConsistentPrefix라는 새로운 일관성 수준에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="08ede-127">Added support for a new consistency level called ConsistentPrefix.</span></span>


### <a name="a-name210210"></a><span data-ttu-id="08ede-128"><a name="2.1.0"/>2.1.0</span><span class="sxs-lookup"><span data-stu-id="08ede-128"><a name="2.1.0"/>2.1.0</span></span>
* <span data-ttu-id="08ede-129">집계 쿼리(COUNT, MIN, MAX, SUM 및 AVG)에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="08ede-129">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="08ede-130">Cosmos DB 에뮬레이터에 대해 실행하는 경우 SSL 유효성 검사를 비활성화하기 위한 옵션을 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="08ede-130">Added an option for disabling SSL verification when running against Cosmos DB Emulator.</span></span>
* <span data-ttu-id="08ede-131">종속 요청 모듈이 정확히 2.10.0이어야 하는 제한을 제거했습니다.</span><span class="sxs-lookup"><span data-stu-id="08ede-131">Removed the restriction of dependent requests module to be exactly 2.10.0.</span></span>
* <span data-ttu-id="08ede-132">분할된 컬렉션에 대한 최소 처리량이 10,100RU/s에서 2500RU/s로 감소됩니다.</span><span class="sxs-lookup"><span data-stu-id="08ede-132">Lowered minimum throughput on partitioned collections from 10,100 RU/s to 2500 RU/s.</span></span>
* <span data-ttu-id="08ede-133">저장된 프로시저가 실행되는 동안 스크립트 로깅을 사용할 수 있도록 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="08ede-133">Added support for enabling script logging during stored procedure execution.</span></span>
* <span data-ttu-id="08ede-134">이 릴리스에서 REST API 버전이 '2017-01-19'로 증가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="08ede-134">REST API version bumped to '2017-01-19' with this release.</span></span>

### <a name="a-name201201"></a><span data-ttu-id="08ede-135"><a name="2.0.1"/>2.0.1</span><span class="sxs-lookup"><span data-stu-id="08ede-135"><a name="2.0.1"/>2.0.1</span></span>
* <span data-ttu-id="08ede-136">문서 주석에 대한 편집이 변경되었습니다.</span><span class="sxs-lookup"><span data-stu-id="08ede-136">Made editorial changes to documentation comments.</span></span>

### <a name="a-name200200"></a><span data-ttu-id="08ede-137"><a name="2.0.0"/>2.0.0</span><span class="sxs-lookup"><span data-stu-id="08ede-137"><a name="2.0.0"/>2.0.0</span></span>
* <span data-ttu-id="08ede-138">Python 3.5에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="08ede-138">Added support for Python 3.5.</span></span>
* <span data-ttu-id="08ede-139">요청 모듈을 사용하는 연결 풀링에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="08ede-139">Added support for connection pooling using a requests module.</span></span>
* <span data-ttu-id="08ede-140">세션 일관성에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="08ede-140">Added support for session consistency.</span></span>
* <span data-ttu-id="08ede-141">분할된 컬렉션의 TOP/ORDERBY 쿼리에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="08ede-141">Added support for TOP/ORDERBY queries for partitioned collections.</span></span>

### <a name="a-name190190"></a><span data-ttu-id="08ede-142"><a name="1.9.0"/>1.9.0</span><span class="sxs-lookup"><span data-stu-id="08ede-142"><a name="1.9.0"/>1.9.0</span></span>
* <span data-ttu-id="08ede-143">제한된 요청에 대한 재시도 정책 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="08ede-143">Added retry policy support for throttled requests.</span></span> <span data-ttu-id="08ede-144">(제한된 요청은 오류 코드 429, 요청 속도가 너무 크다는 예외를 수신합니다.) 기본적으로 오류 코드 429가 발생하면 Azure Cosmos DB는 각 요청을 9번 다시 시도하며 응답 헤더에서 retryAfter 시간을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="08ede-144">(Throttled requests receive a request rate too large exception, error code 429.) By default, Azure Cosmos DB retries nine times for each request when error code 429 is encountered, honoring the retryAfter time in the response header.</span></span> <span data-ttu-id="08ede-145">이제 다시 시도 간의 서버에서 반환한 retryAfter 시간을 무시하려는 경우 고정된 다시 시도 간격 시간은 ConnectionPolicy 개체에서 RetryOptions 속성의 일부로 설정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08ede-145">A fixed retry interval time can now be set as part of the RetryOptions property on the ConnectionPolicy object if you want to ignore the retryAfter time returned by server between the retries.</span></span> <span data-ttu-id="08ede-146">Azure Cosmos DB는 제한된 요청 각각에 대해 30초 동안 대기하고(다시 시도 횟수와 관계 없이) 오류 코드 429를 포함하는 응답을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="08ede-146">Azure Cosmos DB now waits for a maximum of 30 seconds for each request that is being throttled (irrespective of retry count) and returns the response with error code 429.</span></span> <span data-ttu-id="08ede-147">이 시간도 ConnectionPolicy 개체에 있는 RetryOptions 속성에서 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08ede-147">This time can also be overriden in the RetryOptions property on ConnectionPolicy object.</span></span>
* <span data-ttu-id="08ede-148">이제 Cosmos DB는 x-ms-throttle-retry-count 및 x-ms-throttle-retry-wait-time-ms를 다시 시도 사이에 요청이 대기한 제한 다시 시도 수 및 누적 시간을 표시하는 모든 요청의 응답 헤더로 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="08ede-148">Cosmos DB now returns x-ms-throttle-retry-count and x-ms-throttle-retry-wait-time-ms as the response headers in every request to denote the throttle retry count and the cummulative time the request waited between the retries.</span></span>
* <span data-ttu-id="08ede-149">document_client 클래스에 노출된 RetryPolicy 클래스 및 해당 속성(retry_policy)을 제거하고 대신 일부 기본 다시 시도 옵션을 재정의하는 데 사용할 수 있는 ConnectionPolicy 클래스의 RetryOptions 속성을 노출하는 RetryOptions 클래스를 지정했습니다.</span><span class="sxs-lookup"><span data-stu-id="08ede-149">Removed the RetryPolicy class and the corresponding property (retry_policy) exposed on the document_client class and instead introduced a RetryOptions class exposing the RetryOptions property on ConnectionPolicy class that can be used to override some of the default retry options.</span></span>

### <a name="a-name180180"></a><span data-ttu-id="08ede-150"><a name="1.8.0"/>1.8.0</span><span class="sxs-lookup"><span data-stu-id="08ede-150"><a name="1.8.0"/>1.8.0</span></span>
* <span data-ttu-id="08ede-151">다중 지역 데이터베이스 계정에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="08ede-151">Added the support for multi-region database accounts.</span></span>

### <a name="a-name170170"></a><span data-ttu-id="08ede-152"><a name="1.7.0"/>1.7.0</span><span class="sxs-lookup"><span data-stu-id="08ede-152"><a name="1.7.0"/>1.7.0</span></span>
* <span data-ttu-id="08ede-153">문서의 TTL(Time to Live) 기능에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="08ede-153">Added the support for Time To Live(TTL) feature for documents.</span></span>

### <a name="a-name161161"></a><span data-ttu-id="08ede-154"><a name="1.6.1"/>1.6.1</span><span class="sxs-lookup"><span data-stu-id="08ede-154"><a name="1.6.1"/>1.6.1</span></span>
* <span data-ttu-id="08ede-155">partitionkey 경로에 특수 문자를 허용하는 서버 쪽 분할과 관련된 버그 수정입니다.</span><span class="sxs-lookup"><span data-stu-id="08ede-155">Bug fixes related to server side partitioning to allow special characters in partitionkey path.</span></span>

### <a name="a-name160160"></a><span data-ttu-id="08ede-156"><a name="1.6.0"/>1.6.0</span><span class="sxs-lookup"><span data-stu-id="08ede-156"><a name="1.6.0"/>1.6.0</span></span>
* <span data-ttu-id="08ede-157">[분할된 컬렉션](partition-data.md) 및 [사용자 정의 성능 수준](performance-levels.md)이 구현되었습니다.</span><span class="sxs-lookup"><span data-stu-id="08ede-157">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span> 

### <a name="a-name150150"></a><span data-ttu-id="08ede-158"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="08ede-158"><a name="1.5.0"/>1.5.0</span></span>
* <span data-ttu-id="08ede-159">여러 파티션 간의 응용 프로그램 분할을 지원하기 위해 해시 및 범위 파티션 해결 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="08ede-159">Add Hash & Range partition resolvers to assist with sharding applications across multiple partitions.</span></span>

### <a name="a-name142142"></a><span data-ttu-id="08ede-160"><a name="1.4.2"/>1.4.2</span><span class="sxs-lookup"><span data-stu-id="08ede-160"><a name="1.4.2"/>1.4.2</span></span>
* <span data-ttu-id="08ede-161">Upsert를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="08ede-161">Implement Upsert.</span></span> <span data-ttu-id="08ede-162">새로운 UpsertXXX 메서드가 Upsert 기능을 지원하기 위해 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="08ede-162">New UpsertXXX methods added to support Upsert feature.</span></span>
* <span data-ttu-id="08ede-163">ID 기반 라우팅을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="08ede-163">Implement ID Based Routing.</span></span> <span data-ttu-id="08ede-164">공용 API 변경 없이 모두 내부에서 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="08ede-164">No public API changes, all changes internal.</span></span>

### <a name="a-name120120"></a><span data-ttu-id="08ede-165"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="08ede-165"><a name="1.2.0"/>1.2.0</span></span>
* <span data-ttu-id="08ede-166">지리 공간 인덱스를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="08ede-166">Supports GeoSpatial index.</span></span>
* <span data-ttu-id="08ede-167">모든 리소스에 대한 ID 속성의 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="08ede-167">Validates id property for all resources.</span></span> <span data-ttu-id="08ede-168">리소스에 대한 ID는 ?, /, #, \, 문자를 포함하거나 공백으로 끝날 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="08ede-168">Ids for resources cannot contain ?, /, #, \, characters or end with a space.</span></span>
* <span data-ttu-id="08ede-169">ResourceResponse에 새 헤더 "인덱스 변환 진행"을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="08ede-169">Adds new header "index transformation progress" to ResourceResponse.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="08ede-170"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="08ede-170"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="08ede-171">V2 인덱싱 정책을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="08ede-171">Implements V2 indexing policy.</span></span>

### <a name="a-name101101"></a><span data-ttu-id="08ede-172"><a name="1.0.1"/>1.0.1</span><span class="sxs-lookup"><span data-stu-id="08ede-172"><a name="1.0.1"/>1.0.1</span></span>
* <span data-ttu-id="08ede-173">프록시 연결을 지원합니다</span><span class="sxs-lookup"><span data-stu-id="08ede-173">Supports proxy connection.</span></span>

### <a name="a-name100100"></a><span data-ttu-id="08ede-174"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="08ede-174"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="08ede-175">GA SDK.</span><span class="sxs-lookup"><span data-stu-id="08ede-175">GA SDK.</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="08ede-176">릴리스 및 사용 중지 날짜</span><span class="sxs-lookup"><span data-stu-id="08ede-176">Release & retirement dates</span></span>
<span data-ttu-id="08ede-177">Microsoft는 매끄럽게 최신/지원 버전으로 전환할 수 있도록 적어도 SDK 사용 중지 **12개월** 전에 알림을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="08ede-177">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order to smooth the transition to a newer/supported version.</span></span>

<span data-ttu-id="08ede-178">새로운 기능 및 최적화는 현재 SDK에만 추가되어 있으며, 따라서 항상 최신 SDK 버전으로 가능한 한 빨리 업그레이드할 것을 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="08ede-178">New features and functionality and optimizations are only added to the current SDK, as such it is  recommend that you always upgrade to the latest SDK version as early as possible.</span></span> 

<span data-ttu-id="08ede-179">사용 중지된 SDK를 사용하는 Cosmos DB에 대한 요청은 서비스에서 거부됩니다.</span><span class="sxs-lookup"><span data-stu-id="08ede-179">Any request to Cosmos DB using a retired SDK will be rejected by the service.</span></span>

> [!WARNING]
> <span data-ttu-id="08ede-180">**1.0.0** 이전 버전의 Python에 대한 모든 버전의 Azure DocumentDB SDK는 **2016년 2월 29일**에 사용 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="08ede-180">All versions of the Azure DocumentDB SDK for Python prior to version **1.0.0** will be retired on **February 29, 2016**.</span></span> 
> 
> 

<br/>

| <span data-ttu-id="08ede-181">버전</span><span class="sxs-lookup"><span data-stu-id="08ede-181">Version</span></span> | <span data-ttu-id="08ede-182">릴리스 날짜</span><span class="sxs-lookup"><span data-stu-id="08ede-182">Release Date</span></span> | <span data-ttu-id="08ede-183">사용 중지 날짜</span><span class="sxs-lookup"><span data-stu-id="08ede-183">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="08ede-184">2.2.0</span><span class="sxs-lookup"><span data-stu-id="08ede-184">2.2.0</span></span>](#2.2.0) |<span data-ttu-id="08ede-185">2017년 5월 10일</span><span class="sxs-lookup"><span data-stu-id="08ede-185">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="08ede-186">2.1.0</span><span class="sxs-lookup"><span data-stu-id="08ede-186">2.1.0</span></span>](#2.1.0) |<span data-ttu-id="08ede-187">2017년 5월 1일</span><span class="sxs-lookup"><span data-stu-id="08ede-187">May 01, 2017</span></span> |--- |
| [<span data-ttu-id="08ede-188">2.0.1</span><span class="sxs-lookup"><span data-stu-id="08ede-188">2.0.1</span></span>](#2.0.1) |<span data-ttu-id="08ede-189">2016년 10월 30일</span><span class="sxs-lookup"><span data-stu-id="08ede-189">October 30, 2016</span></span> |--- |
| [<span data-ttu-id="08ede-190">2.0.0</span><span class="sxs-lookup"><span data-stu-id="08ede-190">2.0.0</span></span>](#2.0.0) |<span data-ttu-id="08ede-191">2016년 9월 29일</span><span class="sxs-lookup"><span data-stu-id="08ede-191">September 29, 2016</span></span> |--- |
| [<span data-ttu-id="08ede-192">1.9.0</span><span class="sxs-lookup"><span data-stu-id="08ede-192">1.9.0</span></span>](#1.9.0) |<span data-ttu-id="08ede-193">2016년 7월 7일</span><span class="sxs-lookup"><span data-stu-id="08ede-193">July 07, 2016</span></span> |--- |
| [<span data-ttu-id="08ede-194">1.8.0</span><span class="sxs-lookup"><span data-stu-id="08ede-194">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="08ede-195">2016년 6월 14일</span><span class="sxs-lookup"><span data-stu-id="08ede-195">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="08ede-196">1.7.0</span><span class="sxs-lookup"><span data-stu-id="08ede-196">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="08ede-197">2016년 4월 26일</span><span class="sxs-lookup"><span data-stu-id="08ede-197">April 26, 2016</span></span> |--- |
| [<span data-ttu-id="08ede-198">1.6.1</span><span class="sxs-lookup"><span data-stu-id="08ede-198">1.6.1</span></span>](#1.6.1) |<span data-ttu-id="08ede-199">2016년 4월 8일</span><span class="sxs-lookup"><span data-stu-id="08ede-199">April 08, 2016</span></span> |--- |
| [<span data-ttu-id="08ede-200">1.6.0</span><span class="sxs-lookup"><span data-stu-id="08ede-200">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="08ede-201">2016년 3월 29일</span><span class="sxs-lookup"><span data-stu-id="08ede-201">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="08ede-202">1.5.0</span><span class="sxs-lookup"><span data-stu-id="08ede-202">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="08ede-203">2016년 1월 3일</span><span class="sxs-lookup"><span data-stu-id="08ede-203">January 03, 2016</span></span> |--- |
| [<span data-ttu-id="08ede-204">1.4.2</span><span class="sxs-lookup"><span data-stu-id="08ede-204">1.4.2</span></span>](#1.4.2) |<span data-ttu-id="08ede-205">2015년 10월 6일</span><span class="sxs-lookup"><span data-stu-id="08ede-205">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="08ede-206">1.4.1</span><span class="sxs-lookup"><span data-stu-id="08ede-206">1.4.1</span></span>](#1.4.1) |<span data-ttu-id="08ede-207">2015년 10월 6일</span><span class="sxs-lookup"><span data-stu-id="08ede-207">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="08ede-208">1.2.0</span><span class="sxs-lookup"><span data-stu-id="08ede-208">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="08ede-209">2015년 8월 6일</span><span class="sxs-lookup"><span data-stu-id="08ede-209">August 06, 2015</span></span> |--- |
| [<span data-ttu-id="08ede-210">1.1.0</span><span class="sxs-lookup"><span data-stu-id="08ede-210">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="08ede-211">2015년 7월 9일</span><span class="sxs-lookup"><span data-stu-id="08ede-211">July 09, 2015</span></span> |--- |
| [<span data-ttu-id="08ede-212">1.0.1</span><span class="sxs-lookup"><span data-stu-id="08ede-212">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="08ede-213">2015년 5월 25일</span><span class="sxs-lookup"><span data-stu-id="08ede-213">May 25, 2015</span></span> |--- |
| [<span data-ttu-id="08ede-214">1.0.0</span><span class="sxs-lookup"><span data-stu-id="08ede-214">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="08ede-215">2015년 4월 7일</span><span class="sxs-lookup"><span data-stu-id="08ede-215">April 07, 2015</span></span> |--- |
| <span data-ttu-id="08ede-216">0.9.4-prelease</span><span class="sxs-lookup"><span data-stu-id="08ede-216">0.9.4-prelease</span></span> |<span data-ttu-id="08ede-217">2015년 1월 14일</span><span class="sxs-lookup"><span data-stu-id="08ede-217">January 14, 2015</span></span> |<span data-ttu-id="08ede-218">2016년 2월 29일</span><span class="sxs-lookup"><span data-stu-id="08ede-218">February 29, 2016</span></span> |
| <span data-ttu-id="08ede-219">0.9.3-prelease</span><span class="sxs-lookup"><span data-stu-id="08ede-219">0.9.3-prelease</span></span> |<span data-ttu-id="08ede-220">2014년 12월 9일</span><span class="sxs-lookup"><span data-stu-id="08ede-220">December 09, 2014</span></span> |<span data-ttu-id="08ede-221">2016년 2월 29일</span><span class="sxs-lookup"><span data-stu-id="08ede-221">February 29, 2016</span></span> |
| <span data-ttu-id="08ede-222">0.9.2-prelease</span><span class="sxs-lookup"><span data-stu-id="08ede-222">0.9.2-prelease</span></span> |<span data-ttu-id="08ede-223">2014년 11월 25일</span><span class="sxs-lookup"><span data-stu-id="08ede-223">November 25, 2014</span></span> |<span data-ttu-id="08ede-224">2016년 2월 29일</span><span class="sxs-lookup"><span data-stu-id="08ede-224">February 29, 2016</span></span> |
| <span data-ttu-id="08ede-225">0.9.1-prelease</span><span class="sxs-lookup"><span data-stu-id="08ede-225">0.9.1-prelease</span></span> |<span data-ttu-id="08ede-226">2014년 9월 23일</span><span class="sxs-lookup"><span data-stu-id="08ede-226">September 23, 2014</span></span> |<span data-ttu-id="08ede-227">2016년 2월 29일</span><span class="sxs-lookup"><span data-stu-id="08ede-227">February 29, 2016</span></span> |
| <span data-ttu-id="08ede-228">0.9.0-prelease</span><span class="sxs-lookup"><span data-stu-id="08ede-228">0.9.0-prelease</span></span> |<span data-ttu-id="08ede-229">2014년 8월 21일</span><span class="sxs-lookup"><span data-stu-id="08ede-229">August 21, 2014</span></span> |<span data-ttu-id="08ede-230">2016년 2월 29일</span><span class="sxs-lookup"><span data-stu-id="08ede-230">February 29, 2016</span></span> |

## <a name="faq"></a><span data-ttu-id="08ede-231">FAQ</span><span class="sxs-lookup"><span data-stu-id="08ede-231">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="08ede-232">참고 항목</span><span class="sxs-lookup"><span data-stu-id="08ede-232">See also</span></span>
<span data-ttu-id="08ede-233">Cosmos DB에 대한 자세한 내용은 [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) 서비스 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="08ede-233">To learn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span> 


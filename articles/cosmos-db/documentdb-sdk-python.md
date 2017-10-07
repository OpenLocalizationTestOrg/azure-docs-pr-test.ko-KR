---
title: "aaaAzure Cosmos DB Python API SDK 및 리소스 | Microsoft Docs"
description: "Python API와 SDK 릴리스 날짜, 사용 중지 날짜 및 hello Azure Cosmos DB Python SDK의 각 버전 간의 변경 내용을 포함 하 여 hello에 대 한 모든에 대해 알아봅니다."
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
ms.openlocfilehash: 1a164b72d2bd819de87df0229357b82e2177af2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-python-sdk-release-notes-and-resources"></a><span data-ttu-id="dc3ae-103">Azure Cosmos DB Python SDK: 릴리스 정보 및 리소스</span><span class="sxs-lookup"><span data-stu-id="dc3ae-103">Azure Cosmos DB Python SDK: Release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="dc3ae-104">.NET</span><span class="sxs-lookup"><span data-stu-id="dc3ae-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="dc3ae-105">.NET 변경 피드</span><span class="sxs-lookup"><span data-stu-id="dc3ae-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="dc3ae-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="dc3ae-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="dc3ae-107">Node.JS</span><span class="sxs-lookup"><span data-stu-id="dc3ae-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="dc3ae-108">Java</span><span class="sxs-lookup"><span data-stu-id="dc3ae-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="dc3ae-109">Python</span><span class="sxs-lookup"><span data-stu-id="dc3ae-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="dc3ae-110">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="dc3ae-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="dc3ae-111">REST 리소스 공급자</span><span class="sxs-lookup"><span data-stu-id="dc3ae-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="dc3ae-112">SQL</span><span class="sxs-lookup"><span data-stu-id="dc3ae-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="dc3ae-113">**SDK 다운로드**</span><span class="sxs-lookup"><span data-stu-id="dc3ae-113">**Download SDK**</span></span></td><td>[<span data-ttu-id="dc3ae-114">PyPI</span><span class="sxs-lookup"><span data-stu-id="dc3ae-114">PyPI</span></span>](https://pypi.python.org/pypi/pydocumentdb)</td></tr>

<tr><td><span data-ttu-id="dc3ae-115">**API 설명서**</span><span class="sxs-lookup"><span data-stu-id="dc3ae-115">**API documentation**</span></span></td><td>[<span data-ttu-id="dc3ae-116">Python API 참조 설명서</span><span class="sxs-lookup"><span data-stu-id="dc3ae-116">Python API reference documentation</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.html)</td></tr>

<tr><td><span data-ttu-id="dc3ae-117">**SDK 설치 지침**</span><span class="sxs-lookup"><span data-stu-id="dc3ae-117">**SDK installation instructions**</span></span></td><td>[<span data-ttu-id="dc3ae-118">Python SDK 설치 지침</span><span class="sxs-lookup"><span data-stu-id="dc3ae-118">Python SDK installation instructions</span></span>](http://azure.github.io/azure-documentdb-python/)</td></tr>

<tr><td><span data-ttu-id="dc3ae-119">**TooSDK 영향**</span><span class="sxs-lookup"><span data-stu-id="dc3ae-119">**Contribute tooSDK**</span></span></td><td>[<span data-ttu-id="dc3ae-120">GitHub</span><span class="sxs-lookup"><span data-stu-id="dc3ae-120">GitHub</span></span>](https://github.com/Azure/azure-documentdb-python)</td></tr>

<tr><td><span data-ttu-id="dc3ae-121">**시작**</span><span class="sxs-lookup"><span data-stu-id="dc3ae-121">**Get started**</span></span></td><td>[<span data-ttu-id="dc3ae-122">Hello Python SDK 시작</span><span class="sxs-lookup"><span data-stu-id="dc3ae-122">Get started with hello Python SDK</span></span>](documentdb-python-application.md)</td></tr>

<tr><td><span data-ttu-id="dc3ae-123">**현재 지원되는 플랫폼**</span><span class="sxs-lookup"><span data-stu-id="dc3ae-123">**Current supported platform**</span></span></td><td><span data-ttu-id="dc3ae-124">[Python 2.7](https://www.python.org/downloads/) 및 [Python 3.5](https://www.python.org/downloads/)</span><span class="sxs-lookup"><span data-stu-id="dc3ae-124">[Python 2.7](https://www.python.org/downloads/) and [Python 3.5](https://www.python.org/downloads/)</span></span></td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="dc3ae-125">릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="dc3ae-125">Release notes</span></span>
### <a name="a-name220220"></a><span data-ttu-id="dc3ae-126"><a name="2.2.0"/>2.2.0</span><span class="sxs-lookup"><span data-stu-id="dc3ae-126"><a name="2.2.0"/>2.2.0</span></span>
* <span data-ttu-id="dc3ae-127">ConsistentPrefix라는 새로운 일관성 수준에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="dc3ae-127">Added support for a new consistency level called ConsistentPrefix.</span></span>


### <a name="a-name210210"></a><span data-ttu-id="dc3ae-128"><a name="2.1.0"/>2.1.0</span><span class="sxs-lookup"><span data-stu-id="dc3ae-128"><a name="2.1.0"/>2.1.0</span></span>
* <span data-ttu-id="dc3ae-129">집계 쿼리(COUNT, MIN, MAX, SUM 및 AVG)에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="dc3ae-129">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="dc3ae-130">Cosmos DB 에뮬레이터에 대해 실행하는 경우 SSL 유효성 검사를 비활성화하기 위한 옵션을 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="dc3ae-130">Added an option for disabling SSL verification when running against Cosmos DB Emulator.</span></span>
* <span data-ttu-id="dc3ae-131">종속 요청 모듈 toobe 정확히 2.10.0 hello 제한을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc3ae-131">Removed hello restriction of dependent requests module toobe exactly 2.10.0.</span></span>
* <span data-ttu-id="dc3ae-132">10,100 000RU/s too2500 000RU/s에서 분할 된 컬렉션에 대해 최소 처리량을 적어집니다.</span><span class="sxs-lookup"><span data-stu-id="dc3ae-132">Lowered minimum throughput on partitioned collections from 10,100 RU/s too2500 RU/s.</span></span>
* <span data-ttu-id="dc3ae-133">저장된 프로시저가 실행되는 동안 스크립트 로깅을 사용할 수 있도록 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="dc3ae-133">Added support for enabling script logging during stored procedure execution.</span></span>
* <span data-ttu-id="dc3ae-134">REST API 버전 ' 2017 추락 너무-01-19' 이번 릴리스부터 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc3ae-134">REST API version bumped too'2017-01-19' with this release.</span></span>

### <a name="a-name201201"></a><span data-ttu-id="dc3ae-135"><a name="2.0.1"/>2.0.1</span><span class="sxs-lookup"><span data-stu-id="dc3ae-135"><a name="2.0.1"/>2.0.1</span></span>
* <span data-ttu-id="dc3ae-136">Toodocumentation 주석 편집 변경 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc3ae-136">Made editorial changes toodocumentation comments.</span></span>

### <a name="a-name200200"></a><span data-ttu-id="dc3ae-137"><a name="2.0.0"/>2.0.0</span><span class="sxs-lookup"><span data-stu-id="dc3ae-137"><a name="2.0.0"/>2.0.0</span></span>
* <span data-ttu-id="dc3ae-138">Python 3.5에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="dc3ae-138">Added support for Python 3.5.</span></span>
* <span data-ttu-id="dc3ae-139">요청 모듈을 사용하는 연결 풀링에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="dc3ae-139">Added support for connection pooling using a requests module.</span></span>
* <span data-ttu-id="dc3ae-140">세션 일관성에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="dc3ae-140">Added support for session consistency.</span></span>
* <span data-ttu-id="dc3ae-141">분할된 컬렉션의 TOP/ORDERBY 쿼리에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="dc3ae-141">Added support for TOP/ORDERBY queries for partitioned collections.</span></span>

### <a name="a-name190190"></a><span data-ttu-id="dc3ae-142"><a name="1.9.0"/>1.9.0</span><span class="sxs-lookup"><span data-stu-id="dc3ae-142"><a name="1.9.0"/>1.9.0</span></span>
* <span data-ttu-id="dc3ae-143">제한된 요청에 대한 재시도 정책 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="dc3ae-143">Added retry policy support for throttled requests.</span></span> <span data-ttu-id="dc3ae-144">(제한된 요청은 오류 코드 429, 요청 속도가 너무 크다는 예외를 수신합니다.) 기본적으로 Azure Cosmos DB 다시 시도 9 번 각 요청에 대 한 오류 코드 429 오류가 발생 하면 hello retryAfter 시간 hello 응답 헤더에 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc3ae-144">(Throttled requests receive a request rate too large exception, error code 429.) By default, Azure Cosmos DB retries nine times for each request when error code 429 is encountered, honoring hello retryAfter time in hello response header.</span></span> <span data-ttu-id="dc3ae-145">고정 된 다시 시도 간격 시간 수 이제 hello RetryOptions 속성의 일부로 개체에 설정 될 hello ConnectionPolicy hello 다시 시도 대기 중 서버에서 반환 된 tooignore hello retryAfter 시간이 필요한 경우.</span><span class="sxs-lookup"><span data-stu-id="dc3ae-145">A fixed retry interval time can now be set as part of hello RetryOptions property on hello ConnectionPolicy object if you want tooignore hello retryAfter time returned by server between hello retries.</span></span> <span data-ttu-id="dc3ae-146">이제 azure Cosmos DB 최대 (관계 없이 다시 시도 횟수)가 제한 및 오류 코드: 429 hello 응답을 반환 하는 각 요청에 대 한 30 초까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="dc3ae-146">Azure Cosmos DB now waits for a maximum of 30 seconds for each request that is being throttled (irrespective of retry count) and returns hello response with error code 429.</span></span> <span data-ttu-id="dc3ae-147">이 이번에는 hello RetryOptions ConnectionPolicy 개체 속성에서에서 재정의 된 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc3ae-147">This time can also be overriden in hello RetryOptions property on ConnectionPolicy object.</span></span>
* <span data-ttu-id="dc3ae-148">Cosmos DB 이제 x-ms-스로틀-다시 시도-횟수 및 반환 x-ms-throttle-retry-wait-time-ms hello 응답 헤더의 모든 요청 toodenote hello 스로틀 수 및 hello cummulative hello 요청 대기 시간 hello 재시도 간격을 다시 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="dc3ae-148">Cosmos DB now returns x-ms-throttle-retry-count and x-ms-throttle-retry-wait-time-ms as hello response headers in every request toodenote hello throttle retry count and hello cummulative time hello request waited between hello retries.</span></span>
* <span data-ttu-id="dc3ae-149">제거 hello RetryPolicy 클래스 및 (retry_policy) 속성을 해당 하는 hello hello document_client 클래스에 노출 되며 대신 hello RetryOptions 클래스의 속성을 ConnectionPolicy toooverride 사용된 될 수 있는 노출 RetryOptions 클래스를 도입 일부 hello 기본 옵션을 다시 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="dc3ae-149">Removed hello RetryPolicy class and hello corresponding property (retry_policy) exposed on hello document_client class and instead introduced a RetryOptions class exposing hello RetryOptions property on ConnectionPolicy class that can be used toooverride some of hello default retry options.</span></span>

### <a name="a-name180180"></a><span data-ttu-id="dc3ae-150"><a name="1.8.0"/>1.8.0</span><span class="sxs-lookup"><span data-stu-id="dc3ae-150"><a name="1.8.0"/>1.8.0</span></span>
* <span data-ttu-id="dc3ae-151">다중 영역 데이터베이스 계정에 대 한 추가 된 hello 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc3ae-151">Added hello support for multi-region database accounts.</span></span>

### <a name="a-name170170"></a><span data-ttu-id="dc3ae-152"><a name="1.7.0"/>1.7.0</span><span class="sxs-lookup"><span data-stu-id="dc3ae-152"><a name="1.7.0"/>1.7.0</span></span>
* <span data-ttu-id="dc3ae-153">추가 된 hello 문서에 대 한 시간 tooLive(TTL) 기능에 대 한 지원.</span><span class="sxs-lookup"><span data-stu-id="dc3ae-153">Added hello support for Time tooLive(TTL) feature for documents.</span></span>

### <a name="a-name161161"></a><span data-ttu-id="dc3ae-154"><a name="1.6.1"/>1.6.1</span><span class="sxs-lookup"><span data-stu-id="dc3ae-154"><a name="1.6.1"/>1.6.1</span></span>
* <span data-ttu-id="dc3ae-155">버그 수정 관련 tooserver 쪽 tooallow partitionkey 경로에서 특수 문자를 분할 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc3ae-155">Bug fixes related tooserver side partitioning tooallow special characters in partitionkey path.</span></span>

### <a name="a-name160160"></a><span data-ttu-id="dc3ae-156"><a name="1.6.0"/>1.6.0</span><span class="sxs-lookup"><span data-stu-id="dc3ae-156"><a name="1.6.0"/>1.6.0</span></span>
* <span data-ttu-id="dc3ae-157">[분할된 컬렉션](partition-data.md) 및 [사용자 정의 성능 수준](performance-levels.md)이 구현되었습니다.</span><span class="sxs-lookup"><span data-stu-id="dc3ae-157">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span> 

### <a name="a-name150150"></a><span data-ttu-id="dc3ae-158"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="dc3ae-158"><a name="1.5.0"/>1.5.0</span></span>
* <span data-ttu-id="dc3ae-159">추가 해시 & 범위 파티션 확인자 tooassist 여러 파티션에서 분할 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="dc3ae-159">Add Hash & Range partition resolvers tooassist with sharding applications across multiple partitions.</span></span>

### <a name="a-name142142"></a><span data-ttu-id="dc3ae-160"><a name="1.4.2"/>1.4.2</span><span class="sxs-lookup"><span data-stu-id="dc3ae-160"><a name="1.4.2"/>1.4.2</span></span>
* <span data-ttu-id="dc3ae-161">Upsert를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="dc3ae-161">Implement Upsert.</span></span> <span data-ttu-id="dc3ae-162">새 UpsertXXX 메서드가 toosupport Upsert 기능을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc3ae-162">New UpsertXXX methods added toosupport Upsert feature.</span></span>
* <span data-ttu-id="dc3ae-163">ID 기반 라우팅을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="dc3ae-163">Implement ID Based Routing.</span></span> <span data-ttu-id="dc3ae-164">공용 API 변경 없이 모두 내부에서 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc3ae-164">No public API changes, all changes internal.</span></span>

### <a name="a-name120120"></a><span data-ttu-id="dc3ae-165"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="dc3ae-165"><a name="1.2.0"/>1.2.0</span></span>
* <span data-ttu-id="dc3ae-166">지리 공간 인덱스를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="dc3ae-166">Supports GeoSpatial index.</span></span>
* <span data-ttu-id="dc3ae-167">모든 리소스에 대한 ID 속성의 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="dc3ae-167">Validates id property for all resources.</span></span> <span data-ttu-id="dc3ae-168">리소스에 대한 ID는 ?, /, #, \, 문자를 포함하거나 공백으로 끝날 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="dc3ae-168">Ids for resources cannot contain ?, /, #, \, characters or end with a space.</span></span>
* <span data-ttu-id="dc3ae-169">새 헤더 "인덱스 변환 진행 중" tooResourceResponse를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="dc3ae-169">Adds new header "index transformation progress" tooResourceResponse.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="dc3ae-170"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="dc3ae-170"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="dc3ae-171">V2 인덱싱 정책을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="dc3ae-171">Implements V2 indexing policy.</span></span>

### <a name="a-name101101"></a><span data-ttu-id="dc3ae-172"><a name="1.0.1"/>1.0.1</span><span class="sxs-lookup"><span data-stu-id="dc3ae-172"><a name="1.0.1"/>1.0.1</span></span>
* <span data-ttu-id="dc3ae-173">프록시 연결을 지원합니다</span><span class="sxs-lookup"><span data-stu-id="dc3ae-173">Supports proxy connection.</span></span>

### <a name="a-name100100"></a><span data-ttu-id="dc3ae-174"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="dc3ae-174"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="dc3ae-175">GA SDK.</span><span class="sxs-lookup"><span data-stu-id="dc3ae-175">GA SDK.</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="dc3ae-176">릴리스 및 사용 중지 날짜</span><span class="sxs-lookup"><span data-stu-id="dc3ae-176">Release & retirement dates</span></span>
<span data-ttu-id="dc3ae-177">Microsoft는 알림을 적어도 제공 **12 개월** 순서 toosmooth hello 전환 tooa 지원/최신 버전의 SDK를 사용 중지 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc3ae-177">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order toosmooth hello transition tooa newer/supported version.</span></span>

<span data-ttu-id="dc3ae-178">새로운 기능 및 기능 및 최적화는 toohello 현재만 추가 그렇게 하면 항상 업그레이드 toohello 최신 SDK 버전을 가능한 한 빨리 권장는 SDK입니다.</span><span class="sxs-lookup"><span data-stu-id="dc3ae-178">New features and functionality and optimizations are only added toohello current SDK, as such it is  recommend that you always upgrade toohello latest SDK version as early as possible.</span></span> 

<span data-ttu-id="dc3ae-179">모든 요청 tooCosmos 사용 중지 된 SDK를 사용 하 여 DB hello 서비스에서 거부 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc3ae-179">Any request tooCosmos DB using a retired SDK will be rejected by hello service.</span></span>

> [!WARNING]
> <span data-ttu-id="dc3ae-180">모든 버전의 이전 tooversion Python에 대 한 Azure DocumentDB SDK hello **1.0.0** 에 사용 중지 될 예정 **2016 년 2 월 29 일**합니다.</span><span class="sxs-lookup"><span data-stu-id="dc3ae-180">All versions of hello Azure DocumentDB SDK for Python prior tooversion **1.0.0** will be retired on **February 29, 2016**.</span></span> 
> 
> 

<br/>

| <span data-ttu-id="dc3ae-181">버전</span><span class="sxs-lookup"><span data-stu-id="dc3ae-181">Version</span></span> | <span data-ttu-id="dc3ae-182">릴리스 날짜</span><span class="sxs-lookup"><span data-stu-id="dc3ae-182">Release Date</span></span> | <span data-ttu-id="dc3ae-183">사용 중지 날짜</span><span class="sxs-lookup"><span data-stu-id="dc3ae-183">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="dc3ae-184">2.2.0</span><span class="sxs-lookup"><span data-stu-id="dc3ae-184">2.2.0</span></span>](#2.2.0) |<span data-ttu-id="dc3ae-185">2017년 5월 10일</span><span class="sxs-lookup"><span data-stu-id="dc3ae-185">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="dc3ae-186">2.1.0</span><span class="sxs-lookup"><span data-stu-id="dc3ae-186">2.1.0</span></span>](#2.1.0) |<span data-ttu-id="dc3ae-187">2017년 5월 1일</span><span class="sxs-lookup"><span data-stu-id="dc3ae-187">May 01, 2017</span></span> |--- |
| [<span data-ttu-id="dc3ae-188">2.0.1</span><span class="sxs-lookup"><span data-stu-id="dc3ae-188">2.0.1</span></span>](#2.0.1) |<span data-ttu-id="dc3ae-189">2016년 10월 30일</span><span class="sxs-lookup"><span data-stu-id="dc3ae-189">October 30, 2016</span></span> |--- |
| [<span data-ttu-id="dc3ae-190">2.0.0</span><span class="sxs-lookup"><span data-stu-id="dc3ae-190">2.0.0</span></span>](#2.0.0) |<span data-ttu-id="dc3ae-191">2016년 9월 29일</span><span class="sxs-lookup"><span data-stu-id="dc3ae-191">September 29, 2016</span></span> |--- |
| [<span data-ttu-id="dc3ae-192">1.9.0</span><span class="sxs-lookup"><span data-stu-id="dc3ae-192">1.9.0</span></span>](#1.9.0) |<span data-ttu-id="dc3ae-193">2016년 7월 7일</span><span class="sxs-lookup"><span data-stu-id="dc3ae-193">July 07, 2016</span></span> |--- |
| [<span data-ttu-id="dc3ae-194">1.8.0</span><span class="sxs-lookup"><span data-stu-id="dc3ae-194">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="dc3ae-195">2016년 6월 14일</span><span class="sxs-lookup"><span data-stu-id="dc3ae-195">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="dc3ae-196">1.7.0</span><span class="sxs-lookup"><span data-stu-id="dc3ae-196">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="dc3ae-197">2016년 4월 26일</span><span class="sxs-lookup"><span data-stu-id="dc3ae-197">April 26, 2016</span></span> |--- |
| [<span data-ttu-id="dc3ae-198">1.6.1</span><span class="sxs-lookup"><span data-stu-id="dc3ae-198">1.6.1</span></span>](#1.6.1) |<span data-ttu-id="dc3ae-199">2016년 4월 8일</span><span class="sxs-lookup"><span data-stu-id="dc3ae-199">April 08, 2016</span></span> |--- |
| [<span data-ttu-id="dc3ae-200">1.6.0</span><span class="sxs-lookup"><span data-stu-id="dc3ae-200">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="dc3ae-201">2016년 3월 29일</span><span class="sxs-lookup"><span data-stu-id="dc3ae-201">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="dc3ae-202">1.5.0</span><span class="sxs-lookup"><span data-stu-id="dc3ae-202">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="dc3ae-203">2016년 1월 3일</span><span class="sxs-lookup"><span data-stu-id="dc3ae-203">January 03, 2016</span></span> |--- |
| [<span data-ttu-id="dc3ae-204">1.4.2</span><span class="sxs-lookup"><span data-stu-id="dc3ae-204">1.4.2</span></span>](#1.4.2) |<span data-ttu-id="dc3ae-205">2015년 10월 6일</span><span class="sxs-lookup"><span data-stu-id="dc3ae-205">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="dc3ae-206">1.4.1</span><span class="sxs-lookup"><span data-stu-id="dc3ae-206">1.4.1</span></span>](#1.4.1) |<span data-ttu-id="dc3ae-207">2015년 10월 6일</span><span class="sxs-lookup"><span data-stu-id="dc3ae-207">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="dc3ae-208">1.2.0</span><span class="sxs-lookup"><span data-stu-id="dc3ae-208">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="dc3ae-209">2015년 8월 6일</span><span class="sxs-lookup"><span data-stu-id="dc3ae-209">August 06, 2015</span></span> |--- |
| [<span data-ttu-id="dc3ae-210">1.1.0</span><span class="sxs-lookup"><span data-stu-id="dc3ae-210">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="dc3ae-211">2015년 7월 9일</span><span class="sxs-lookup"><span data-stu-id="dc3ae-211">July 09, 2015</span></span> |--- |
| [<span data-ttu-id="dc3ae-212">1.0.1</span><span class="sxs-lookup"><span data-stu-id="dc3ae-212">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="dc3ae-213">2015년 5월 25일</span><span class="sxs-lookup"><span data-stu-id="dc3ae-213">May 25, 2015</span></span> |--- |
| [<span data-ttu-id="dc3ae-214">1.0.0</span><span class="sxs-lookup"><span data-stu-id="dc3ae-214">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="dc3ae-215">2015년 4월 7일</span><span class="sxs-lookup"><span data-stu-id="dc3ae-215">April 07, 2015</span></span> |--- |
| <span data-ttu-id="dc3ae-216">0.9.4-prelease</span><span class="sxs-lookup"><span data-stu-id="dc3ae-216">0.9.4-prelease</span></span> |<span data-ttu-id="dc3ae-217">2015년 1월 14일</span><span class="sxs-lookup"><span data-stu-id="dc3ae-217">January 14, 2015</span></span> |<span data-ttu-id="dc3ae-218">2016년 2월 29일</span><span class="sxs-lookup"><span data-stu-id="dc3ae-218">February 29, 2016</span></span> |
| <span data-ttu-id="dc3ae-219">0.9.3-prelease</span><span class="sxs-lookup"><span data-stu-id="dc3ae-219">0.9.3-prelease</span></span> |<span data-ttu-id="dc3ae-220">2014년 12월 9일</span><span class="sxs-lookup"><span data-stu-id="dc3ae-220">December 09, 2014</span></span> |<span data-ttu-id="dc3ae-221">2016년 2월 29일</span><span class="sxs-lookup"><span data-stu-id="dc3ae-221">February 29, 2016</span></span> |
| <span data-ttu-id="dc3ae-222">0.9.2-prelease</span><span class="sxs-lookup"><span data-stu-id="dc3ae-222">0.9.2-prelease</span></span> |<span data-ttu-id="dc3ae-223">2014년 11월 25일</span><span class="sxs-lookup"><span data-stu-id="dc3ae-223">November 25, 2014</span></span> |<span data-ttu-id="dc3ae-224">2016년 2월 29일</span><span class="sxs-lookup"><span data-stu-id="dc3ae-224">February 29, 2016</span></span> |
| <span data-ttu-id="dc3ae-225">0.9.1-prelease</span><span class="sxs-lookup"><span data-stu-id="dc3ae-225">0.9.1-prelease</span></span> |<span data-ttu-id="dc3ae-226">2014년 9월 23일</span><span class="sxs-lookup"><span data-stu-id="dc3ae-226">September 23, 2014</span></span> |<span data-ttu-id="dc3ae-227">2016년 2월 29일</span><span class="sxs-lookup"><span data-stu-id="dc3ae-227">February 29, 2016</span></span> |
| <span data-ttu-id="dc3ae-228">0.9.0-prelease</span><span class="sxs-lookup"><span data-stu-id="dc3ae-228">0.9.0-prelease</span></span> |<span data-ttu-id="dc3ae-229">2014년 8월 21일</span><span class="sxs-lookup"><span data-stu-id="dc3ae-229">August 21, 2014</span></span> |<span data-ttu-id="dc3ae-230">2016년 2월 29일</span><span class="sxs-lookup"><span data-stu-id="dc3ae-230">February 29, 2016</span></span> |

## <a name="faq"></a><span data-ttu-id="dc3ae-231">FAQ</span><span class="sxs-lookup"><span data-stu-id="dc3ae-231">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="dc3ae-232">참고 항목</span><span class="sxs-lookup"><span data-stu-id="dc3ae-232">See also</span></span>
<span data-ttu-id="dc3ae-233">Cosmos DB에 대해 자세히 toolearn 참조 [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) 서비스 페이지.</span><span class="sxs-lookup"><span data-stu-id="dc3ae-233">toolearn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span> 


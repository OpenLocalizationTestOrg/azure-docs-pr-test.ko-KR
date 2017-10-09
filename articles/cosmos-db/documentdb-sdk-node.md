---
title: "aaaAzure Cosmos DB Node.js API SDK 및 리소스 | Microsoft Docs"
description: "Node.js API와 SDK 릴리스 날짜, 사용 중지 날짜 및 hello Azure Cosmos DB Node.js SDK의 각 버전 간의 변경 내용을 포함 하 여 hello에 대 한 모든에 대해 알아봅니다."
services: cosmos-db
documentationcenter: nodejs
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 9d5621fa-0e11-4619-a28b-a19d872bcf37
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/14/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d450b9a9ea7b0f4717ddae8940121fc458ea3744
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-nodejs-sdk-release-notes-and-resources"></a><span data-ttu-id="4f7f4-103">Azure Cosmos DB Node.js SDK: 릴리스 정보 및 리소스</span><span class="sxs-lookup"><span data-stu-id="4f7f4-103">Azure Cosmos DB Node.js SDK: Release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4f7f4-104">.NET</span><span class="sxs-lookup"><span data-stu-id="4f7f4-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="4f7f4-105">.NET 변경 피드</span><span class="sxs-lookup"><span data-stu-id="4f7f4-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="4f7f4-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="4f7f4-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="4f7f4-107">Node.JS</span><span class="sxs-lookup"><span data-stu-id="4f7f4-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="4f7f4-108">Java</span><span class="sxs-lookup"><span data-stu-id="4f7f4-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="4f7f4-109">Python</span><span class="sxs-lookup"><span data-stu-id="4f7f4-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="4f7f4-110">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="4f7f4-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="4f7f4-111">REST 리소스 공급자</span><span class="sxs-lookup"><span data-stu-id="4f7f4-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="4f7f4-112">SQL</span><span class="sxs-lookup"><span data-stu-id="4f7f4-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="4f7f4-113">**SDK 다운로드**</span><span class="sxs-lookup"><span data-stu-id="4f7f4-113">**Download SDK**</span></span></td><td>[<span data-ttu-id="4f7f4-114">NPM</span><span class="sxs-lookup"><span data-stu-id="4f7f4-114">NPM</span></span>](https://www.npmjs.com/package/documentdb)</td></tr>

<tr><td><span data-ttu-id="4f7f4-115">**API 설명서**</span><span class="sxs-lookup"><span data-stu-id="4f7f4-115">**API documentation**</span></span></td><td>[<span data-ttu-id="4f7f4-116">Node.js API 참조 설명서</span><span class="sxs-lookup"><span data-stu-id="4f7f4-116">Node.js API reference documentation</span></span>](http://azure.github.io/azure-documentdb-node/DocumentClient.html)</td></tr>

<tr><td><span data-ttu-id="4f7f4-117">**SDK 설치 지침**</span><span class="sxs-lookup"><span data-stu-id="4f7f4-117">**SDK installation instructions**</span></span></td><td>[<span data-ttu-id="4f7f4-118">설치 지침</span><span class="sxs-lookup"><span data-stu-id="4f7f4-118">Installation instructions</span></span>](http://azure.github.io/azure-documentdb-node/)</td></tr>

<tr><td><span data-ttu-id="4f7f4-119">**TooSDK 영향**</span><span class="sxs-lookup"><span data-stu-id="4f7f4-119">**Contribute tooSDK**</span></span></td><td>[<span data-ttu-id="4f7f4-120">GitHub</span><span class="sxs-lookup"><span data-stu-id="4f7f4-120">GitHub</span></span>](https://github.com/Azure/azure-documentdb-node/tree/master/source)</td></tr>

<tr><td><span data-ttu-id="4f7f4-121">**샘플**</span><span class="sxs-lookup"><span data-stu-id="4f7f4-121">**Samples**</span></span></td><td>[<span data-ttu-id="4f7f4-122">Node.js 코드 샘플</span><span class="sxs-lookup"><span data-stu-id="4f7f4-122">Node.js code samples</span></span>](documentdb-nodejs-samples.md)</td></tr>

<tr><td><span data-ttu-id="4f7f4-123">**시작 자습서**</span><span class="sxs-lookup"><span data-stu-id="4f7f4-123">**Get started tutorial**</span></span></td><td>[<span data-ttu-id="4f7f4-124">Node.js SDK hello로 시작</span><span class="sxs-lookup"><span data-stu-id="4f7f4-124">Get started with hello Node.js SDK</span></span>](documentdb-nodejs-get-started.md)</td></tr>

<tr><td><span data-ttu-id="4f7f4-125">**웹앱 자습서**</span><span class="sxs-lookup"><span data-stu-id="4f7f4-125">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="4f7f4-126">Azure Cosmos DB를 사용하여 Node.js 웹 응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="4f7f4-126">Build a Node.js web application using Azure Cosmos DB</span></span>](documentdb-nodejs-application.md)</td></tr>

<tr><td><span data-ttu-id="4f7f4-127">**현재 지원되는 플랫폼**</span><span class="sxs-lookup"><span data-stu-id="4f7f4-127">**Current supported platform**</span></span></td><td> 
[<span data-ttu-id="4f7f4-128">Node.js v6.x</span><span class="sxs-lookup"><span data-stu-id="4f7f4-128">Node.js v6.x</span></span>](https://nodejs.org/en/blog/release/v6.10.3/)<br/> 
[<span data-ttu-id="4f7f4-129">Node.js v4.2.0</span><span class="sxs-lookup"><span data-stu-id="4f7f4-129">Node.js v4.2.0</span></span>](https://nodejs.org/en/blog/release/v4.2.0/)<br/> 
[<span data-ttu-id="4f7f4-130">Node.js v0.12</span><span class="sxs-lookup"><span data-stu-id="4f7f4-130">Node.js v0.12</span></span>](https://nodejs.org/en/blog/release/v0.12.0/)<br/> 
<span data-ttu-id="4f7f4-131">[Node.js v0.10](https://nodejs.org/en/blog/release/v0.10.0/) 
</span><span class="sxs-lookup"><span data-stu-id="4f7f4-131">[Node.js v0.10](https://nodejs.org/en/blog/release/v0.10.0/) 
</span></span></td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="4f7f4-132">릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="4f7f4-132">Release notes</span></span>

### <span data-ttu-id="4f7f4-133"><a name="1.12.2"/>1.12.2</a></span><span class="sxs-lookup"><span data-stu-id="4f7f4-133"><a name="1.12.2"/>1.12.2</a></span></span>
*   <span data-ttu-id="4f7f4-134">npm 설명서가 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4f7f4-134">npm documentation fixed.</span></span>

### <span data-ttu-id="4f7f4-135"><a name="1.12.1"/>1.12.1</a></span><span class="sxs-lookup"><span data-stu-id="4f7f4-135"><a name="1.12.1"/>1.12.1</a></span></span>
* <span data-ttu-id="4f7f4-136">관련된 문서에 특수 유니코드 문자(LS, PS)가 있는 executeStoredProcedure의 버그를 수정했습니다.</span><span class="sxs-lookup"><span data-stu-id="4f7f4-136">Fixed a bug in executeStoredProcedure where documents involved had special Unicode characters (LS, PS).</span></span>
* <span data-ttu-id="4f7f4-137">Hello 파티션 키의 유니코드 문자를 사용 하 여 문서를 처리 하는 버그를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f7f4-137">Fixed a bug in handling documents with Unicode characters in hello partition key.</span></span>
* <span data-ttu-id="4f7f4-138">Hello 이름 미디어를 사용 하 여 컬렉션을 만들기에 대 한 고정된 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f7f4-138">Fixed support for creating collections with hello name media.</span></span> <span data-ttu-id="4f7f4-139">Github 문제 #114.</span><span class="sxs-lookup"><span data-stu-id="4f7f4-139">Github issue #114.</span></span>
* <span data-ttu-id="4f7f4-140">권한 부여 토큰에 대한 지원을 수정했습니다.</span><span class="sxs-lookup"><span data-stu-id="4f7f4-140">Fixed support for permission authorization token.</span></span> <span data-ttu-id="4f7f4-141">Github 문제 #178.</span><span class="sxs-lookup"><span data-stu-id="4f7f4-141">Github issue #178.</span></span>

### <span data-ttu-id="4f7f4-142"><a name="1.12.0"/>1.12.0</a></span><span class="sxs-lookup"><span data-stu-id="4f7f4-142"><a name="1.12.0"/>1.12.0</a></span></span>
* <span data-ttu-id="4f7f4-143">ConsistentPrefix라고 하는 새로운 [일관성 수준](consistency-levels.md)에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4f7f4-143">Added support for a new [consistency level](consistency-levels.md) called ConsistentPrefix.</span></span>
* <span data-ttu-id="4f7f4-144">UriFactory에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4f7f4-144">Added support for UriFactory.</span></span>
* <span data-ttu-id="4f7f4-145">유니코드 지원 버그를 수정했습니다.</span><span class="sxs-lookup"><span data-stu-id="4f7f4-145">Fixed a Unicode support bug.</span></span> <span data-ttu-id="4f7f4-146">GitHub 문제 #171.</span><span class="sxs-lookup"><span data-stu-id="4f7f4-146">GitHub issue #171.</span></span>

### <span data-ttu-id="4f7f4-147"><a name="1.11.0"/>1.11.0</a></span><span class="sxs-lookup"><span data-stu-id="4f7f4-147"><a name="1.11.0"/>1.11.0</a></span></span>
* <span data-ttu-id="4f7f4-148">집계 쿼리 (COUNT, MIN, MAX, SUM 및 AVG)에 대 한 추가 된 hello 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f7f4-148">Added hello support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="4f7f4-149">에 대 한 병렬 처리 수준 크로스 파티션 쿼리를 제어 하기 위한 추가 된 hello 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="4f7f4-149">Added hello option for controlling degree of parallelism for cross partition queries.</span></span>
* <span data-ttu-id="4f7f4-150">Cosmos DB Azure 에뮬레이터에 대해 실행할 때 SSL 유효성 검사를 비활성화 하기 위한 추가 된 hello 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="4f7f4-150">Added hello option for disabling SSL verification when running against Azure Cosmos DB Emulator.</span></span>
* <span data-ttu-id="4f7f4-151">10,100 000RU/s too2500 000RU/s에서 분할 된 컬렉션에 대해 최소 처리량을 적어집니다.</span><span class="sxs-lookup"><span data-stu-id="4f7f4-151">Lowered minimum throughput on partitioned collections from 10,100 RU/s too2500 RU/s.</span></span>
* <span data-ttu-id="4f7f4-152">단일 파티션 컬렉션에 대 한 고정된 hello 연속 작업의 토큰 버그입니다.</span><span class="sxs-lookup"><span data-stu-id="4f7f4-152">Fixed hello continuation token bug for single partition collection.</span></span> <span data-ttu-id="4f7f4-153">Github 문제 #107.</span><span class="sxs-lookup"><span data-stu-id="4f7f4-153">Github issue #107.</span></span>
* <span data-ttu-id="4f7f4-154">단일 매개 변수 형태로 0 처리 고정된 hello executeStoredProcedure 버그입니다.</span><span class="sxs-lookup"><span data-stu-id="4f7f4-154">Fixed hello executeStoredProcedure bug in handling 0 as single param.</span></span> <span data-ttu-id="4f7f4-155">Github 문제 #155.</span><span class="sxs-lookup"><span data-stu-id="4f7f4-155">Github issue #155.</span></span>

### <span data-ttu-id="4f7f4-156"><a name="1.10.2"/>1.10.2</a></span><span class="sxs-lookup"><span data-stu-id="4f7f4-156"><a name="1.10.2"/>1.10.2</a></span></span>
* <span data-ttu-id="4f7f4-157">고정 된 사용자 에이전트 헤더 tooinclude hello SDK 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="4f7f4-157">Fixed user-agent header tooinclude hello SDK version.</span></span>
* <span data-ttu-id="4f7f4-158">사소한 코드 정리입니다.</span><span class="sxs-lookup"><span data-stu-id="4f7f4-158">Minor code cleanup.</span></span>

### <span data-ttu-id="4f7f4-159"><a name="1.10.1"/>1.10.1</a></span><span class="sxs-lookup"><span data-stu-id="4f7f4-159"><a name="1.10.1"/>1.10.1</a></span></span>
* <span data-ttu-id="4f7f4-160">SDK tootarget hello emulator(hostname=localhost) hello를 사용 하는 경우 SSL 유효성 검사를 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f7f4-160">Disabling SSL verification when using hello SDK tootarget hello emulator(hostname=localhost).</span></span>
* <span data-ttu-id="4f7f4-161">저장된 프로시저가 실행되는 동안 스크립트 로깅을 사용할 수 있도록 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4f7f4-161">Added support for enabling script logging during stored procedure execution.</span></span>

### <span data-ttu-id="4f7f4-162"><a name="1.10.0"/>1.10.0</a></span><span class="sxs-lookup"><span data-stu-id="4f7f4-162"><a name="1.10.0"/>1.10.0</a></span></span>
* <span data-ttu-id="4f7f4-163">파티션 간 병렬 쿼리에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4f7f4-163">Added support for cross partition parallel queries.</span></span>
* <span data-ttu-id="4f7f4-164">분할된 컬렉션의 TOP/ORDER BY 쿼리에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4f7f4-164">Added support for TOP/ORDER BY queries for partitioned collections.</span></span>

### <span data-ttu-id="4f7f4-165"><a name="1.9.0"/>1.9.0</a></span><span class="sxs-lookup"><span data-stu-id="4f7f4-165"><a name="1.9.0"/>1.9.0</a></span></span>
* <span data-ttu-id="4f7f4-166">제한된 요청에 대한 재시도 정책 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4f7f4-166">Added retry policy support for throttled requests.</span></span> <span data-ttu-id="4f7f4-167">(제한된 요청은 오류 코드 429, 요청 속도가 너무 크다는 예외를 수신합니다.) 기본적으로 Azure Cosmos DB 다시 시도 9 번 각 요청에 대 한 오류 코드 429 오류가 발생 하면 hello retryAfter 시간 hello 응답 헤더에 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f7f4-167">(Throttled requests receive a request rate too large exception, error code 429.) By default, Azure Cosmos DB retries nine times for each request when error code 429 is encountered, honoring hello retryAfter time in hello response header.</span></span> <span data-ttu-id="4f7f4-168">고정 된 다시 시도 간격 시간 수 이제 hello RetryOptions 속성의 일부로 개체에 설정 될 hello ConnectionPolicy hello 다시 시도 대기 중 서버에서 반환 된 tooignore hello retryAfter 시간이 필요한 경우.</span><span class="sxs-lookup"><span data-stu-id="4f7f4-168">A fixed retry interval time can now be set as part of hello RetryOptions property on hello ConnectionPolicy object if you want tooignore hello retryAfter time returned by server between hello retries.</span></span> <span data-ttu-id="4f7f4-169">이제 azure Cosmos DB 최대 (관계 없이 다시 시도 횟수)가 제한 및 오류 코드: 429 hello 응답을 반환 하는 각 요청에 대 한 30 초까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="4f7f4-169">Azure Cosmos DB now waits for a maximum of 30 seconds for each request that is being throttled (irrespective of retry count) and returns hello response with error code 429.</span></span> <span data-ttu-id="4f7f4-170">이 시간 hello RetryOptions ConnectionPolicy 개체 속성에서에서 재정의할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f7f4-170">This time can also be overridden in hello RetryOptions property on ConnectionPolicy object.</span></span>
* <span data-ttu-id="4f7f4-171">Cosmos DB 이제 x-ms-스로틀-다시 시도-횟수 및 반환 x-ms-throttle-retry-wait-time-ms hello 응답 헤더의 모든 요청 toodenote hello 스로틀 수 및 hello 누적 hello 요청 대기 시간 hello 재시도 간격을 다시 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="4f7f4-171">Cosmos DB now returns x-ms-throttle-retry-count and x-ms-throttle-retry-wait-time-ms as hello response headers in every request toodenote hello throttle retry count and hello cumulative time hello request waited between hello retries.</span></span>
* <span data-ttu-id="4f7f4-172">hello RetryOptions 속성 노출 hello RetryOptions 클래스 추가 된 hello ConnectionPolicy 클래스 toooverride 사용된 될 수 있는 일부 hello 기본 다시 시도 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="4f7f4-172">hello RetryOptions class was added, exposing hello RetryOptions property on hello ConnectionPolicy class that can be used toooverride some of hello default retry options.</span></span>

### <span data-ttu-id="4f7f4-173"><a name="1.8.0"/>1.8.0</a></span><span class="sxs-lookup"><span data-stu-id="4f7f4-173"><a name="1.8.0"/>1.8.0</a></span></span>
* <span data-ttu-id="4f7f4-174">다중 영역 데이터베이스 계정에 대 한 추가 된 hello 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f7f4-174">Added hello support for multi-region database accounts.</span></span>

### <span data-ttu-id="4f7f4-175"><a name="1.7.0"/>1.7.0</a></span><span class="sxs-lookup"><span data-stu-id="4f7f4-175"><a name="1.7.0"/>1.7.0</a></span></span>
* <span data-ttu-id="4f7f4-176">추가 된 hello 문서에 대 한 시간 tooLive(TTL) 기능에 대 한 지원.</span><span class="sxs-lookup"><span data-stu-id="4f7f4-176">Added hello support for Time tooLive(TTL) feature for documents.</span></span>

### <span data-ttu-id="4f7f4-177"><a name="1.6.0"/>1.6.0</a></span><span class="sxs-lookup"><span data-stu-id="4f7f4-177"><a name="1.6.0"/>1.6.0</a></span></span>
* <span data-ttu-id="4f7f4-178">[분할된 컬렉션](partition-data.md) 및 [사용자 정의 성능 수준](performance-levels.md)이 구현되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4f7f4-178">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span>

### <span data-ttu-id="4f7f4-179"><a name="1.5.6"/>1.5.6</a></span><span class="sxs-lookup"><span data-stu-id="4f7f4-179"><a name="1.5.6"/>1.5.6</a></span></span>
* <span data-ttu-id="4f7f4-180">RangePartitionResolver.resolveForRead 버그 여기서 결과의 잘못 된 concat tooa 인해 링크를 반환 하지 했습니다.</span><span class="sxs-lookup"><span data-stu-id="4f7f4-180">Fixed RangePartitionResolver.resolveForRead bug where it was not returning links due tooa bad concat of results.</span></span>

### <span data-ttu-id="4f7f4-181"><a name="1.5.5"/>1.5.5</a></span><span class="sxs-lookup"><span data-stu-id="4f7f4-181"><a name="1.5.5"/>1.5.5</a></span></span>
* <span data-ttu-id="4f7f4-182">hashParitionResolver resolveForRead() 해결: 예외를 throw하는 제공된 파티션 키가 없는 경우 모든 등록된 링크의 목록을 대신 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4f7f4-182">Fixed hashParitionResolver resolveForRead(): When no partition key supplied was throwing exception, instead of returning a list of all registered links.</span></span>

### <span data-ttu-id="4f7f4-183"><a name="1.5.4"/>1.5.4</a></span><span class="sxs-lookup"><span data-stu-id="4f7f4-183"><a name="1.5.4"/>1.5.4</a></span></span>
* <span data-ttu-id="4f7f4-184">문제를 해결 [#100](https://github.com/Azure/azure-documentdb-node/issues/100) -HTTPS 에이전트 전용: hello Azure Cosmos DB 목적에 대 한 전역 에이전트 수정 되지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f7f4-184">Fixes issue [#100](https://github.com/Azure/azure-documentdb-node/issues/100) - Dedicated HTTPS Agent: Avoid modifying hello global agent for Azure Cosmos DB purposes.</span></span> <span data-ttu-id="4f7f4-185">모든 hello lib 요청에 대 한 전용된 에이전트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f7f4-185">Use a dedicated agent for all of hello lib’s requests.</span></span>

### <span data-ttu-id="4f7f4-186"><a name="1.5.3"/>1.5.3</a></span><span class="sxs-lookup"><span data-stu-id="4f7f4-186"><a name="1.5.3"/>1.5.3</a></span></span>
* <span data-ttu-id="4f7f4-187">문제 해결 [#81](https://github.com/Azure/azure-documentdb-node/issues/81) - 미디어 ID에서 대시를 올바르게 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="4f7f4-187">Fixes issue [#81](https://github.com/Azure/azure-documentdb-node/issues/81) - Properly handle dashes in media ids.</span></span>

### <span data-ttu-id="4f7f4-188"><a name="1.5.2"/>1.5.2</a></span><span class="sxs-lookup"><span data-stu-id="4f7f4-188"><a name="1.5.2"/>1.5.2</a></span></span>
* <span data-ttu-id="4f7f4-189">문제 해결 [#95](https://github.com/Azure/azure-documentdb-node/issues/95) - EventEmitter 수신기 누수 경고</span><span class="sxs-lookup"><span data-stu-id="4f7f4-189">Fixes issue [#95](https://github.com/Azure/azure-documentdb-node/issues/95) - EventEmitter listener leak warning.</span></span>

### <span data-ttu-id="4f7f4-190"><a name="1.5.1"/>1.5.1</a></span><span class="sxs-lookup"><span data-stu-id="4f7f4-190"><a name="1.5.1"/>1.5.1</a></span></span>
* <span data-ttu-id="4f7f4-191">문제를 해결 [#92](https://github.com/Azure/azure-documentdb-node/issues/90) -대/소문자 구분 시스템에 대 한 해시 toohash 폴더 이름을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="4f7f4-191">Fixes issue [#92](https://github.com/Azure/azure-documentdb-node/issues/90) - rename folder Hash toohash for case-sensitive systems.</span></span>

### <span data-ttu-id="4f7f4-192"><a name="1.5.0"/>1.5.0</a></span><span class="sxs-lookup"><span data-stu-id="4f7f4-192"><a name="1.5.0"/>1.5.0</a></span></span>
* <span data-ttu-id="4f7f4-193">해시 및 범위 파티션 해결 프로그램을 추가하여 분할 지원 구현</span><span class="sxs-lookup"><span data-stu-id="4f7f4-193">Implement sharding support by adding hash & range partition resolvers.</span></span>

### <span data-ttu-id="4f7f4-194"><a name="1.4.0"/>1.4.0</a></span><span class="sxs-lookup"><span data-stu-id="4f7f4-194"><a name="1.4.0"/>1.4.0</a></span></span>
* <span data-ttu-id="4f7f4-195">Upsert를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="4f7f4-195">Implement Upsert.</span></span> <span data-ttu-id="4f7f4-196">DocumentClient의 새로운 upsertXXX 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="4f7f4-196">New upsertXXX methods on documentClient.</span></span>

### <span data-ttu-id="4f7f4-197"><a name="1.3.0"/>1.3.0</a></span><span class="sxs-lookup"><span data-stu-id="4f7f4-197"><a name="1.3.0"/>1.3.0</a></span></span>
* <span data-ttu-id="4f7f4-198">다른 Sdk에 맞게 정렬에서 toobring 버전 번호를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="4f7f4-198">Skipped toobring version numbers in alignment with other SDKs.</span></span>

### <span data-ttu-id="4f7f4-199"><a name="1.2.2"/>1.2.2</a></span><span class="sxs-lookup"><span data-stu-id="4f7f4-199"><a name="1.2.2"/>1.2.2</a></span></span>
* <span data-ttu-id="4f7f4-200">분할 Q 래퍼 toonew 리포지토리를 약속 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f7f4-200">Split Q promises wrapper toonew repository.</span></span>
* <span data-ttu-id="4f7f4-201">Npm 레지스트리에 대 한 toopackage 파일을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f7f4-201">Update toopackage file for npm registry.</span></span>

### <span data-ttu-id="4f7f4-202"><a name="1.2.1"/>1.2.1</a></span><span class="sxs-lookup"><span data-stu-id="4f7f4-202"><a name="1.2.1"/>1.2.1</a></span></span>
* <span data-ttu-id="4f7f4-203">ID 기반 라우팅을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="4f7f4-203">Implements ID Based Routing.</span></span>
* <span data-ttu-id="4f7f4-204">문제 [#49](https://github.com/Azure/azure-documentdb-node/issues/49) 수정 - 현재 속성이 메서드 current()와 충돌합니다.</span><span class="sxs-lookup"><span data-stu-id="4f7f4-204">Fixes Issue [#49](https://github.com/Azure/azure-documentdb-node/issues/49) - current property conflicts with method current().</span></span>

### <span data-ttu-id="4f7f4-205"><a name="1.2.0"/>1.2.0</a></span><span class="sxs-lookup"><span data-stu-id="4f7f4-205"><a name="1.2.0"/>1.2.0</a></span></span>
* <span data-ttu-id="4f7f4-206">지리 공간 인덱스에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4f7f4-206">Added support for GeoSpatial index.</span></span>
* <span data-ttu-id="4f7f4-207">모든 리소스에 대한 ID 속성의 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="4f7f4-207">Validates id property for all resources.</span></span> <span data-ttu-id="4f7f4-208">리소스의 ID는 ?, /, #, &#47;&#47; 문자를 포함할 수 없으며 공백으로 끝날 수도 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4f7f4-208">Ids for resources cannot contain ?, /, #, &#47;&#47;, characters or end with a space.</span></span>
* <span data-ttu-id="4f7f4-209">새 헤더 "인덱스 변환 진행 중" tooResourceResponse를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4f7f4-209">Adds new header "index transformation progress" tooResourceResponse.</span></span>

### <span data-ttu-id="4f7f4-210"><a name="1.1.0"/>1.1.0</a></span><span class="sxs-lookup"><span data-stu-id="4f7f4-210"><a name="1.1.0"/>1.1.0</a></span></span>
* <span data-ttu-id="4f7f4-211">V2 인덱싱 정책을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="4f7f4-211">Implements V2 indexing policy.</span></span>

### <span data-ttu-id="4f7f4-212"><a name="1.0.3"/>1.0.3</a></span><span class="sxs-lookup"><span data-stu-id="4f7f4-212"><a name="1.0.3"/>1.0.3</a></span></span>
* <span data-ttu-id="4f7f4-213">문제 [#40](https://github.com/Azure/azure-documentdb-node/issues/40) -eslint 구현 및 grunt hello 코어에서 구성 하 고 SDK를 약속 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f7f4-213">Issue [#40](https://github.com/Azure/azure-documentdb-node/issues/40) - Implemented eslint and grunt configurations in hello core and promise SDK.</span></span>

### <span data-ttu-id="4f7f4-214"><a name="1.0.2"/>1.0.2</a></span><span class="sxs-lookup"><span data-stu-id="4f7f4-214"><a name="1.0.2"/>1.0.2</a></span></span>
* <span data-ttu-id="4f7f4-215">문제 [#45](https://github.com/Azure/azure-documentdb-node/issues/45) - 프라미스 래퍼에 오류가 있는 헤더가 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4f7f4-215">Issue [#45](https://github.com/Azure/azure-documentdb-node/issues/45) - Promises wrapper does not include header with error.</span></span>

### <span data-ttu-id="4f7f4-216"><a name="1.0.1"/>1.0.1</a></span><span class="sxs-lookup"><span data-stu-id="4f7f4-216"><a name="1.0.1"/>1.0.1</a></span></span>
* <span data-ttu-id="4f7f4-217">ReadConflicts, readConflictAsync, 및 queryConflicts 추가 하 여 충돌에 대 한 기능 tooquery를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f7f4-217">Implemented ability tooquery for conflicts by adding readConflicts, readConflictAsync, and queryConflicts.</span></span>
* <span data-ttu-id="4f7f4-218">API 설명서가 업데이트되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4f7f4-218">Updated API documentation.</span></span>
* <span data-ttu-id="4f7f4-219">문제 [#41](https://github.com/Azure/azure-documentdb-node/issues/41) - client.createDocumentAsync 오류</span><span class="sxs-lookup"><span data-stu-id="4f7f4-219">Issue [#41](https://github.com/Azure/azure-documentdb-node/issues/41) - client.createDocumentAsync error.</span></span>

### <span data-ttu-id="4f7f4-220"><a name="1.0.0"/>1.0.0</a></span><span class="sxs-lookup"><span data-stu-id="4f7f4-220"><a name="1.0.0"/>1.0.0</a></span></span>
* <span data-ttu-id="4f7f4-221">GA SDK.</span><span class="sxs-lookup"><span data-stu-id="4f7f4-221">GA SDK.</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="4f7f4-222">릴리스 및 사용 중지 날짜</span><span class="sxs-lookup"><span data-stu-id="4f7f4-222">Release & Retirement Dates</span></span>
<span data-ttu-id="4f7f4-223">Microsoft는 알림 최소 **12 개월** 순서 toosmooth hello 전환 tooa 지원/최신 버전의 SDK를 사용 중지 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f7f4-223">Microsoft provides notification at least **12 months** in advance of retiring an SDK in order toosmooth hello transition tooa newer/supported version.</span></span>

<span data-ttu-id="4f7f4-224">새로운 기능 및 기능 및 최적화는 toohello 현재만 추가 SDK, 따라서 것이 좋습니다 하면 항상 업그레이드 toohello 최신 SDK 버전 가능한 한 빨리 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f7f4-224">New features and functionality and optimizations are only added toohello current SDK, as such it is  recommended that you always upgrade toohello latest SDK version as early as possible.</span></span>

<span data-ttu-id="4f7f4-225">TooCosmos 사용 중지 된 SDK를 사용 하 여 DB에는 모든 요청은 hello 서비스에서 거부 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f7f4-225">Any request tooCosmos DB using a retired SDK is be rejected by hello service.</span></span>

<br/>

| <span data-ttu-id="4f7f4-226">버전</span><span class="sxs-lookup"><span data-stu-id="4f7f4-226">Version</span></span> | <span data-ttu-id="4f7f4-227">릴리스 날짜</span><span class="sxs-lookup"><span data-stu-id="4f7f4-227">Release Date</span></span> | <span data-ttu-id="4f7f4-228">사용 중지 날짜</span><span class="sxs-lookup"><span data-stu-id="4f7f4-228">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="4f7f4-229">1.12.2</span><span class="sxs-lookup"><span data-stu-id="4f7f4-229">1.12.2</span></span>](#1.12.2) |<span data-ttu-id="4f7f4-230">2017년 8월 10일</span><span class="sxs-lookup"><span data-stu-id="4f7f4-230">August 10, 2017</span></span> |--- |
| [<span data-ttu-id="4f7f4-231">1.12.1</span><span class="sxs-lookup"><span data-stu-id="4f7f4-231">1.12.1</span></span>](#1.12.1) |<span data-ttu-id="4f7f4-232">2017년 8월 10일</span><span class="sxs-lookup"><span data-stu-id="4f7f4-232">August 10, 2017</span></span> |--- |
| [<span data-ttu-id="4f7f4-233">1.12.0</span><span class="sxs-lookup"><span data-stu-id="4f7f4-233">1.12.0</span></span>](#1.12.0) |<span data-ttu-id="4f7f4-234">2017년 5월 10일</span><span class="sxs-lookup"><span data-stu-id="4f7f4-234">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="4f7f4-235">1.11.0</span><span class="sxs-lookup"><span data-stu-id="4f7f4-235">1.11.0</span></span>](#1.11.0) |<span data-ttu-id="4f7f4-236">2017년 3월 16일</span><span class="sxs-lookup"><span data-stu-id="4f7f4-236">March 16, 2017</span></span> |--- |
| [<span data-ttu-id="4f7f4-237">1.10.2</span><span class="sxs-lookup"><span data-stu-id="4f7f4-237">1.10.2</span></span>](#1.10.2) |<span data-ttu-id="4f7f4-238">2017년 1월 27일</span><span class="sxs-lookup"><span data-stu-id="4f7f4-238">January 27, 2017</span></span> |--- |
| [<span data-ttu-id="4f7f4-239">1.10.1</span><span class="sxs-lookup"><span data-stu-id="4f7f4-239">1.10.1</span></span>](#1.10.1) |<span data-ttu-id="4f7f4-240">2016년 12월 22일</span><span class="sxs-lookup"><span data-stu-id="4f7f4-240">December 22, 2016</span></span> |--- |
| [<span data-ttu-id="4f7f4-241">1.10.0</span><span class="sxs-lookup"><span data-stu-id="4f7f4-241">1.10.0</span></span>](#1.10.0) |<span data-ttu-id="4f7f4-242">2016년 10월 3일</span><span class="sxs-lookup"><span data-stu-id="4f7f4-242">October 03, 2016</span></span> |--- |
| [<span data-ttu-id="4f7f4-243">1.9.0</span><span class="sxs-lookup"><span data-stu-id="4f7f4-243">1.9.0</span></span>](#1.9.0) |<span data-ttu-id="4f7f4-244">2016년 7월 7일</span><span class="sxs-lookup"><span data-stu-id="4f7f4-244">July 07, 2016</span></span> |--- |
| [<span data-ttu-id="4f7f4-245">1.8.0</span><span class="sxs-lookup"><span data-stu-id="4f7f4-245">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="4f7f4-246">2016년 6월 14일</span><span class="sxs-lookup"><span data-stu-id="4f7f4-246">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="4f7f4-247">1.7.0</span><span class="sxs-lookup"><span data-stu-id="4f7f4-247">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="4f7f4-248">2016년 4월 26일</span><span class="sxs-lookup"><span data-stu-id="4f7f4-248">April 26, 2016</span></span> |--- |
| [<span data-ttu-id="4f7f4-249">1.6.0</span><span class="sxs-lookup"><span data-stu-id="4f7f4-249">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="4f7f4-250">2016년 3월 29일</span><span class="sxs-lookup"><span data-stu-id="4f7f4-250">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="4f7f4-251">1.5.6</span><span class="sxs-lookup"><span data-stu-id="4f7f4-251">1.5.6</span></span>](#1.5.6) |<span data-ttu-id="4f7f4-252">2016년 3월 8일</span><span class="sxs-lookup"><span data-stu-id="4f7f4-252">March 08, 2016</span></span> |--- |
| [<span data-ttu-id="4f7f4-253">1.5.5</span><span class="sxs-lookup"><span data-stu-id="4f7f4-253">1.5.5</span></span>](#1.5.5) |<span data-ttu-id="4f7f4-254">2016년 2월 2일</span><span class="sxs-lookup"><span data-stu-id="4f7f4-254">February 02, 2016</span></span> |--- |
| [<span data-ttu-id="4f7f4-255">1.5.4</span><span class="sxs-lookup"><span data-stu-id="4f7f4-255">1.5.4</span></span>](#1.5.4) |<span data-ttu-id="4f7f4-256">2016년 2월 1일</span><span class="sxs-lookup"><span data-stu-id="4f7f4-256">February 01, 2016</span></span> |--- |
| [<span data-ttu-id="4f7f4-257">1.5.2</span><span class="sxs-lookup"><span data-stu-id="4f7f4-257">1.5.2</span></span>](#1.5.2) |<span data-ttu-id="4f7f4-258">2016년 1월 26일</span><span class="sxs-lookup"><span data-stu-id="4f7f4-258">January 26, 2016</span></span> |--- |
| [<span data-ttu-id="4f7f4-259">1.5.2</span><span class="sxs-lookup"><span data-stu-id="4f7f4-259">1.5.2</span></span>](#1.5.2) |<span data-ttu-id="4f7f4-260">2016년 1월 22일</span><span class="sxs-lookup"><span data-stu-id="4f7f4-260">January 22, 2016</span></span> |--- |
| [<span data-ttu-id="4f7f4-261">1.5.1</span><span class="sxs-lookup"><span data-stu-id="4f7f4-261">1.5.1</span></span>](#1.5.1) |<span data-ttu-id="4f7f4-262">2016년 1월 4일</span><span class="sxs-lookup"><span data-stu-id="4f7f4-262">January 4, 2016</span></span> |--- |
| [<span data-ttu-id="4f7f4-263">1.5.0</span><span class="sxs-lookup"><span data-stu-id="4f7f4-263">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="4f7f4-264">2015년 12월 31일</span><span class="sxs-lookup"><span data-stu-id="4f7f4-264">December 31, 2015</span></span> |--- |
| [<span data-ttu-id="4f7f4-265">1.4.0</span><span class="sxs-lookup"><span data-stu-id="4f7f4-265">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="4f7f4-266">2015년 10월 6일</span><span class="sxs-lookup"><span data-stu-id="4f7f4-266">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="4f7f4-267">1.3.0</span><span class="sxs-lookup"><span data-stu-id="4f7f4-267">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="4f7f4-268">2015년 10월 6일</span><span class="sxs-lookup"><span data-stu-id="4f7f4-268">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="4f7f4-269">1.2.2</span><span class="sxs-lookup"><span data-stu-id="4f7f4-269">1.2.2</span></span>](#1.2.2) |<span data-ttu-id="4f7f4-270">2015년 9월 10일</span><span class="sxs-lookup"><span data-stu-id="4f7f4-270">September 10, 2015</span></span> |--- |
| [<span data-ttu-id="4f7f4-271">1.2.1</span><span class="sxs-lookup"><span data-stu-id="4f7f4-271">1.2.1</span></span>](#1.2.1) |<span data-ttu-id="4f7f4-272">2015년 8월 15일</span><span class="sxs-lookup"><span data-stu-id="4f7f4-272">August 15, 2015</span></span> |--- |
| [<span data-ttu-id="4f7f4-273">1.2.0</span><span class="sxs-lookup"><span data-stu-id="4f7f4-273">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="4f7f4-274">2015년 8월 5일</span><span class="sxs-lookup"><span data-stu-id="4f7f4-274">August 05, 2015</span></span> |--- |
| [<span data-ttu-id="4f7f4-275">1.1.0</span><span class="sxs-lookup"><span data-stu-id="4f7f4-275">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="4f7f4-276">2015년 7월 9일</span><span class="sxs-lookup"><span data-stu-id="4f7f4-276">July 09, 2015</span></span> |--- |
| [<span data-ttu-id="4f7f4-277">1.0.3</span><span class="sxs-lookup"><span data-stu-id="4f7f4-277">1.0.3</span></span>](#1.0.3) |<span data-ttu-id="4f7f4-278">2015년 6월 4일</span><span class="sxs-lookup"><span data-stu-id="4f7f4-278">June 04, 2015</span></span> |--- |
| [<span data-ttu-id="4f7f4-279">1.0.2</span><span class="sxs-lookup"><span data-stu-id="4f7f4-279">1.0.2</span></span>](#1.0.2) |<span data-ttu-id="4f7f4-280">2015년 5월 23일</span><span class="sxs-lookup"><span data-stu-id="4f7f4-280">May 23, 2015</span></span> |--- |
| [<span data-ttu-id="4f7f4-281">1.0.1</span><span class="sxs-lookup"><span data-stu-id="4f7f4-281">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="4f7f4-282">2015년 5월 15일</span><span class="sxs-lookup"><span data-stu-id="4f7f4-282">May 15, 2015</span></span> |--- |
| [<span data-ttu-id="4f7f4-283">1.0.0</span><span class="sxs-lookup"><span data-stu-id="4f7f4-283">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="4f7f4-284">2015년 4월 8일</span><span class="sxs-lookup"><span data-stu-id="4f7f4-284">April 08, 2015</span></span> |--- |

## <a name="faq"></a><span data-ttu-id="4f7f4-285">FAQ</span><span class="sxs-lookup"><span data-stu-id="4f7f4-285">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="4f7f4-286">참고 항목</span><span class="sxs-lookup"><span data-stu-id="4f7f4-286">See also</span></span>
<span data-ttu-id="4f7f4-287">Cosmos DB에 대해 자세히 toolearn 참조 [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) 서비스 페이지.</span><span class="sxs-lookup"><span data-stu-id="4f7f4-287">toolearn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span>


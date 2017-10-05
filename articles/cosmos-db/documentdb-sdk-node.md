---
title: "Azure Cosmos DB Node.js API, SDK 및 리소스 | Microsoft Docs"
description: "릴리스 날짜, 사용 중지 날짜 및 Azure Cosmos DB Node.js SDK의 각 버전 간의 변경 내용을 포함한 Node.js API 및 SDK에 대해 모두 알아봅니다."
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
ms.openlocfilehash: 4376a5c07b5f00311ce0fe3c0056efdf79c273f9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-nodejs-sdk-release-notes-and-resources"></a><span data-ttu-id="88d31-103">Azure Cosmos DB Node.js SDK: 릴리스 정보 및 리소스</span><span class="sxs-lookup"><span data-stu-id="88d31-103">Azure Cosmos DB Node.js SDK: Release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="88d31-104">.NET</span><span class="sxs-lookup"><span data-stu-id="88d31-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="88d31-105">.NET 변경 피드</span><span class="sxs-lookup"><span data-stu-id="88d31-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="88d31-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="88d31-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="88d31-107">Node.JS</span><span class="sxs-lookup"><span data-stu-id="88d31-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="88d31-108">Java</span><span class="sxs-lookup"><span data-stu-id="88d31-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="88d31-109">Python</span><span class="sxs-lookup"><span data-stu-id="88d31-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="88d31-110">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="88d31-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="88d31-111">REST 리소스 공급자</span><span class="sxs-lookup"><span data-stu-id="88d31-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="88d31-112">SQL</span><span class="sxs-lookup"><span data-stu-id="88d31-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="88d31-113">**SDK 다운로드**</span><span class="sxs-lookup"><span data-stu-id="88d31-113">**Download SDK**</span></span></td><td>[<span data-ttu-id="88d31-114">NPM</span><span class="sxs-lookup"><span data-stu-id="88d31-114">NPM</span></span>](https://www.npmjs.com/package/documentdb)</td></tr>

<tr><td><span data-ttu-id="88d31-115">**API 설명서**</span><span class="sxs-lookup"><span data-stu-id="88d31-115">**API documentation**</span></span></td><td>[<span data-ttu-id="88d31-116">Node.js API 참조 설명서</span><span class="sxs-lookup"><span data-stu-id="88d31-116">Node.js API reference documentation</span></span>](http://azure.github.io/azure-documentdb-node/DocumentClient.html)</td></tr>

<tr><td><span data-ttu-id="88d31-117">**SDK 설치 지침**</span><span class="sxs-lookup"><span data-stu-id="88d31-117">**SDK installation instructions**</span></span></td><td>[<span data-ttu-id="88d31-118">설치 지침</span><span class="sxs-lookup"><span data-stu-id="88d31-118">Installation instructions</span></span>](http://azure.github.io/azure-documentdb-node/)</td></tr>

<tr><td><span data-ttu-id="88d31-119">**SDK에 참여**</span><span class="sxs-lookup"><span data-stu-id="88d31-119">**Contribute to SDK**</span></span></td><td>[<span data-ttu-id="88d31-120">GitHub</span><span class="sxs-lookup"><span data-stu-id="88d31-120">GitHub</span></span>](https://github.com/Azure/azure-documentdb-node/tree/master/source)</td></tr>

<tr><td><span data-ttu-id="88d31-121">**샘플**</span><span class="sxs-lookup"><span data-stu-id="88d31-121">**Samples**</span></span></td><td>[<span data-ttu-id="88d31-122">Node.js 코드 샘플</span><span class="sxs-lookup"><span data-stu-id="88d31-122">Node.js code samples</span></span>](documentdb-nodejs-samples.md)</td></tr>

<tr><td><span data-ttu-id="88d31-123">**시작 자습서**</span><span class="sxs-lookup"><span data-stu-id="88d31-123">**Get started tutorial**</span></span></td><td>[<span data-ttu-id="88d31-124">Node.js SDK 시작</span><span class="sxs-lookup"><span data-stu-id="88d31-124">Get started with the Node.js SDK</span></span>](documentdb-nodejs-get-started.md)</td></tr>

<tr><td><span data-ttu-id="88d31-125">**웹앱 자습서**</span><span class="sxs-lookup"><span data-stu-id="88d31-125">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="88d31-126">Azure Cosmos DB를 사용하여 Node.js 웹 응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="88d31-126">Build a Node.js web application using Azure Cosmos DB</span></span>](documentdb-nodejs-application.md)</td></tr>

<tr><td><span data-ttu-id="88d31-127">**현재 지원되는 플랫폼**</span><span class="sxs-lookup"><span data-stu-id="88d31-127">**Current supported platform**</span></span></td><td> 
[<span data-ttu-id="88d31-128">Node.js v6.x</span><span class="sxs-lookup"><span data-stu-id="88d31-128">Node.js v6.x</span></span>](https://nodejs.org/en/blog/release/v6.10.3/)<br/> 
[<span data-ttu-id="88d31-129">Node.js v4.2.0</span><span class="sxs-lookup"><span data-stu-id="88d31-129">Node.js v4.2.0</span></span>](https://nodejs.org/en/blog/release/v4.2.0/)<br/> 
[<span data-ttu-id="88d31-130">Node.js v0.12</span><span class="sxs-lookup"><span data-stu-id="88d31-130">Node.js v0.12</span></span>](https://nodejs.org/en/blog/release/v0.12.0/)<br/> 
<span data-ttu-id="88d31-131">[Node.js v0.10](https://nodejs.org/en/blog/release/v0.10.0/) 
</span><span class="sxs-lookup"><span data-stu-id="88d31-131">[Node.js v0.10](https://nodejs.org/en/blog/release/v0.10.0/) 
</span></span></td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="88d31-132">릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="88d31-132">Release notes</span></span>

### <span data-ttu-id="88d31-133"><a name="1.12.2"/>1.12.2</a></span><span class="sxs-lookup"><span data-stu-id="88d31-133"><a name="1.12.2"/>1.12.2</a></span></span>
*   <span data-ttu-id="88d31-134">npm 설명서가 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="88d31-134">npm documentation fixed.</span></span>

### <span data-ttu-id="88d31-135"><a name="1.12.1"/>1.12.1</a></span><span class="sxs-lookup"><span data-stu-id="88d31-135"><a name="1.12.1"/>1.12.1</a></span></span>
* <span data-ttu-id="88d31-136">관련된 문서에 특수 유니코드 문자(LS, PS)가 있는 executeStoredProcedure의 버그를 수정했습니다.</span><span class="sxs-lookup"><span data-stu-id="88d31-136">Fixed a bug in executeStoredProcedure where documents involved had special Unicode characters (LS, PS).</span></span>
* <span data-ttu-id="88d31-137">파티션 키의 유니코드 문자를 사용하여 문서를 처리할 때 버그를 수정했습니다.</span><span class="sxs-lookup"><span data-stu-id="88d31-137">Fixed a bug in handling documents with Unicode characters in the partition key.</span></span>
* <span data-ttu-id="88d31-138">이름 미디어를 사용하여 컬렉션을 만들기 위한 지원을 수정했습니다.</span><span class="sxs-lookup"><span data-stu-id="88d31-138">Fixed support for creating collections with the name media.</span></span> <span data-ttu-id="88d31-139">Github 문제 #114.</span><span class="sxs-lookup"><span data-stu-id="88d31-139">Github issue #114.</span></span>
* <span data-ttu-id="88d31-140">권한 부여 토큰에 대한 지원을 수정했습니다.</span><span class="sxs-lookup"><span data-stu-id="88d31-140">Fixed support for permission authorization token.</span></span> <span data-ttu-id="88d31-141">Github 문제 #178.</span><span class="sxs-lookup"><span data-stu-id="88d31-141">Github issue #178.</span></span>

### <span data-ttu-id="88d31-142"><a name="1.12.0"/>1.12.0</a></span><span class="sxs-lookup"><span data-stu-id="88d31-142"><a name="1.12.0"/>1.12.0</a></span></span>
* <span data-ttu-id="88d31-143">ConsistentPrefix라고 하는 새로운 [일관성 수준](consistency-levels.md)에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="88d31-143">Added support for a new [consistency level](consistency-levels.md) called ConsistentPrefix.</span></span>
* <span data-ttu-id="88d31-144">UriFactory에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="88d31-144">Added support for UriFactory.</span></span>
* <span data-ttu-id="88d31-145">유니코드 지원 버그를 수정했습니다.</span><span class="sxs-lookup"><span data-stu-id="88d31-145">Fixed a Unicode support bug.</span></span> <span data-ttu-id="88d31-146">GitHub 문제 #171.</span><span class="sxs-lookup"><span data-stu-id="88d31-146">GitHub issue #171.</span></span>

### <span data-ttu-id="88d31-147"><a name="1.11.0"/>1.11.0</a></span><span class="sxs-lookup"><span data-stu-id="88d31-147"><a name="1.11.0"/>1.11.0</a></span></span>
* <span data-ttu-id="88d31-148">집계 쿼리(COUNT, MIN, MAX, SUM 및 AVG)에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="88d31-148">Added the support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="88d31-149">파티션 간 쿼리에 대한 병렬 처리 수준을 제어하기 위한 옵션을 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="88d31-149">Added the option for controlling degree of parallelism for cross partition queries.</span></span>
* <span data-ttu-id="88d31-150">Azure Cosmos DB 에뮬레이터에 대해 실행하는 경우 SSL 유효성 검사를 비활성화하기 위한 옵션을 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="88d31-150">Added the option for disabling SSL verification when running against Azure Cosmos DB Emulator.</span></span>
* <span data-ttu-id="88d31-151">분할된 컬렉션에 대한 최소 처리량이 10,100RU/s에서 2500RU/s로 감소됩니다.</span><span class="sxs-lookup"><span data-stu-id="88d31-151">Lowered minimum throughput on partitioned collections from 10,100 RU/s to 2500 RU/s.</span></span>
* <span data-ttu-id="88d31-152">단일 파티션 컬렉션에 대한 연속 토큰 버그를 수정했습니다.</span><span class="sxs-lookup"><span data-stu-id="88d31-152">Fixed the continuation token bug for single partition collection.</span></span> <span data-ttu-id="88d31-153">Github 문제 #107.</span><span class="sxs-lookup"><span data-stu-id="88d31-153">Github issue #107.</span></span>
* <span data-ttu-id="88d31-154">단일 매개 변수인 0을 처리하는 도중 executeStoredProcedure 버그를 수정했습니다.</span><span class="sxs-lookup"><span data-stu-id="88d31-154">Fixed the executeStoredProcedure bug in handling 0 as single param.</span></span> <span data-ttu-id="88d31-155">Github 문제 #155.</span><span class="sxs-lookup"><span data-stu-id="88d31-155">Github issue #155.</span></span>

### <span data-ttu-id="88d31-156"><a name="1.10.2"/>1.10.2</a></span><span class="sxs-lookup"><span data-stu-id="88d31-156"><a name="1.10.2"/>1.10.2</a></span></span>
* <span data-ttu-id="88d31-157">SDK 버전을 포함하도록 수정된 사용자 에이전트 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="88d31-157">Fixed user-agent header to include the SDK version.</span></span>
* <span data-ttu-id="88d31-158">사소한 코드 정리입니다.</span><span class="sxs-lookup"><span data-stu-id="88d31-158">Minor code cleanup.</span></span>

### <span data-ttu-id="88d31-159"><a name="1.10.1"/>1.10.1</a></span><span class="sxs-lookup"><span data-stu-id="88d31-159"><a name="1.10.1"/>1.10.1</a></span></span>
* <span data-ttu-id="88d31-160">SDK를 사용하여 에뮬레이터를 대상으로 지정할 때(hostname=localhost) SSL 유효성 검사를 사용하지 않도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="88d31-160">Disabling SSL verification when using the SDK to target the emulator(hostname=localhost).</span></span>
* <span data-ttu-id="88d31-161">저장된 프로시저가 실행되는 동안 스크립트 로깅을 사용할 수 있도록 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="88d31-161">Added support for enabling script logging during stored procedure execution.</span></span>

### <span data-ttu-id="88d31-162"><a name="1.10.0"/>1.10.0</a></span><span class="sxs-lookup"><span data-stu-id="88d31-162"><a name="1.10.0"/>1.10.0</a></span></span>
* <span data-ttu-id="88d31-163">파티션 간 병렬 쿼리에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="88d31-163">Added support for cross partition parallel queries.</span></span>
* <span data-ttu-id="88d31-164">분할된 컬렉션의 TOP/ORDER BY 쿼리에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="88d31-164">Added support for TOP/ORDER BY queries for partitioned collections.</span></span>

### <span data-ttu-id="88d31-165"><a name="1.9.0"/>1.9.0</a></span><span class="sxs-lookup"><span data-stu-id="88d31-165"><a name="1.9.0"/>1.9.0</a></span></span>
* <span data-ttu-id="88d31-166">제한된 요청에 대한 재시도 정책 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="88d31-166">Added retry policy support for throttled requests.</span></span> <span data-ttu-id="88d31-167">(제한된 요청은 오류 코드 429, 요청 속도가 너무 크다는 예외를 수신합니다.) 기본적으로 오류 코드 429가 발생하면 Azure Cosmos DB는 각 요청을 9번 다시 시도하며 응답 헤더에서 retryAfter 시간을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="88d31-167">(Throttled requests receive a request rate too large exception, error code 429.) By default, Azure Cosmos DB retries nine times for each request when error code 429 is encountered, honoring the retryAfter time in the response header.</span></span> <span data-ttu-id="88d31-168">이제 다시 시도 간의 서버에서 반환한 retryAfter 시간을 무시하려는 경우 고정된 다시 시도 간격 시간은 ConnectionPolicy 개체에서 RetryOptions 속성의 일부로 설정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88d31-168">A fixed retry interval time can now be set as part of the RetryOptions property on the ConnectionPolicy object if you want to ignore the retryAfter time returned by server between the retries.</span></span> <span data-ttu-id="88d31-169">Azure Cosmos DB는 제한된 요청 각각에 대해 30초 동안 대기하고(다시 시도 횟수와 관계 없이) 오류 코드 429를 포함하는 응답을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="88d31-169">Azure Cosmos DB now waits for a maximum of 30 seconds for each request that is being throttled (irrespective of retry count) and returns the response with error code 429.</span></span> <span data-ttu-id="88d31-170">이 시간도 ConnectionPolicy 개체에 있는 RetryOptions 속성에서 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88d31-170">This time can also be overridden in the RetryOptions property on ConnectionPolicy object.</span></span>
* <span data-ttu-id="88d31-171">이제 Cosmos DB는 x-ms-throttle-retry-count 및 x-ms-throttle-retry-wait-time-ms를 다시 시도 사이에 요청이 대기한 제한 다시 시도 수 및 누적 시간을 표시하는 모든 요청의 응답 헤더로 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="88d31-171">Cosmos DB now returns x-ms-throttle-retry-count and x-ms-throttle-retry-wait-time-ms as the response headers in every request to denote the throttle retry count and the cumulative time the request waited between the retries.</span></span>
* <span data-ttu-id="88d31-172">기본 다시 시도 옵션의 일부를 재정의하는 데 사용할 수 있는 ConnectionPolicy 클래스에 RetryOptions 속성을 노출하여 RetryOptions 클래스를 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="88d31-172">The RetryOptions class was added, exposing the RetryOptions property on the ConnectionPolicy class that can be used to override some of the default retry options.</span></span>

### <span data-ttu-id="88d31-173"><a name="1.8.0"/>1.8.0</a></span><span class="sxs-lookup"><span data-stu-id="88d31-173"><a name="1.8.0"/>1.8.0</a></span></span>
* <span data-ttu-id="88d31-174">다중 지역 데이터베이스 계정에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="88d31-174">Added the support for multi-region database accounts.</span></span>

### <span data-ttu-id="88d31-175"><a name="1.7.0"/>1.7.0</a></span><span class="sxs-lookup"><span data-stu-id="88d31-175"><a name="1.7.0"/>1.7.0</a></span></span>
* <span data-ttu-id="88d31-176">문서의 TTL(Time to Live) 기능에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="88d31-176">Added the support for Time To Live(TTL) feature for documents.</span></span>

### <span data-ttu-id="88d31-177"><a name="1.6.0"/>1.6.0</a></span><span class="sxs-lookup"><span data-stu-id="88d31-177"><a name="1.6.0"/>1.6.0</a></span></span>
* <span data-ttu-id="88d31-178">[분할된 컬렉션](partition-data.md) 및 [사용자 정의 성능 수준](performance-levels.md)이 구현되었습니다.</span><span class="sxs-lookup"><span data-stu-id="88d31-178">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span>

### <span data-ttu-id="88d31-179"><a name="1.5.6"/>1.5.6</a></span><span class="sxs-lookup"><span data-stu-id="88d31-179"><a name="1.5.6"/>1.5.6</a></span></span>
* <span data-ttu-id="88d31-180">잘못된 concat 결과로 인해 링크를 반환하지 못했던 RangePartitionResolver.resolveForRead 버그가 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="88d31-180">Fixed RangePartitionResolver.resolveForRead bug where it was not returning links due to a bad concat of results.</span></span>

### <span data-ttu-id="88d31-181"><a name="1.5.5"/>1.5.5</a></span><span class="sxs-lookup"><span data-stu-id="88d31-181"><a name="1.5.5"/>1.5.5</a></span></span>
* <span data-ttu-id="88d31-182">hashParitionResolver resolveForRead() 해결: 예외를 throw하는 제공된 파티션 키가 없는 경우 모든 등록된 링크의 목록을 대신 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="88d31-182">Fixed hashParitionResolver resolveForRead(): When no partition key supplied was throwing exception, instead of returning a list of all registered links.</span></span>

### <span data-ttu-id="88d31-183"><a name="1.5.4"/>1.5.4</a></span><span class="sxs-lookup"><span data-stu-id="88d31-183"><a name="1.5.4"/>1.5.4</a></span></span>
* <span data-ttu-id="88d31-184">문제 해결 [#100](https://github.com/Azure/azure-documentdb-node/issues/100) - 전용 HTTPS 에이전트: Azure Cosmos DB 목적으로 전역 에이전트를 수정하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="88d31-184">Fixes issue [#100](https://github.com/Azure/azure-documentdb-node/issues/100) - Dedicated HTTPS Agent: Avoid modifying the global agent for Azure Cosmos DB purposes.</span></span> <span data-ttu-id="88d31-185">모든 lib의 요청에 대해 전용 에이전트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="88d31-185">Use a dedicated agent for all of the lib’s requests.</span></span>

### <span data-ttu-id="88d31-186"><a name="1.5.3"/>1.5.3</a></span><span class="sxs-lookup"><span data-stu-id="88d31-186"><a name="1.5.3"/>1.5.3</a></span></span>
* <span data-ttu-id="88d31-187">문제 해결 [#81](https://github.com/Azure/azure-documentdb-node/issues/81) - 미디어 ID에서 대시를 올바르게 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="88d31-187">Fixes issue [#81](https://github.com/Azure/azure-documentdb-node/issues/81) - Properly handle dashes in media ids.</span></span>

### <span data-ttu-id="88d31-188"><a name="1.5.2"/>1.5.2</a></span><span class="sxs-lookup"><span data-stu-id="88d31-188"><a name="1.5.2"/>1.5.2</a></span></span>
* <span data-ttu-id="88d31-189">문제 해결 [#95](https://github.com/Azure/azure-documentdb-node/issues/95) - EventEmitter 수신기 누수 경고</span><span class="sxs-lookup"><span data-stu-id="88d31-189">Fixes issue [#95](https://github.com/Azure/azure-documentdb-node/issues/95) - EventEmitter listener leak warning.</span></span>

### <span data-ttu-id="88d31-190"><a name="1.5.1"/>1.5.1</a></span><span class="sxs-lookup"><span data-stu-id="88d31-190"><a name="1.5.1"/>1.5.1</a></span></span>
* <span data-ttu-id="88d31-191">문제 [#92](https://github.com/Azure/azure-documentdb-node/issues/90) 해결 - 대/소문자 구분 시스템으로 인해 Hash 폴더의 이름을 hash로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="88d31-191">Fixes issue [#92](https://github.com/Azure/azure-documentdb-node/issues/90) - rename folder Hash to hash for case-sensitive systems.</span></span>

### <span data-ttu-id="88d31-192"><a name="1.5.0"/>1.5.0</a></span><span class="sxs-lookup"><span data-stu-id="88d31-192"><a name="1.5.0"/>1.5.0</a></span></span>
* <span data-ttu-id="88d31-193">해시 및 범위 파티션 해결 프로그램을 추가하여 분할 지원 구현</span><span class="sxs-lookup"><span data-stu-id="88d31-193">Implement sharding support by adding hash & range partition resolvers.</span></span>

### <span data-ttu-id="88d31-194"><a name="1.4.0"/>1.4.0</a></span><span class="sxs-lookup"><span data-stu-id="88d31-194"><a name="1.4.0"/>1.4.0</a></span></span>
* <span data-ttu-id="88d31-195">Upsert를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="88d31-195">Implement Upsert.</span></span> <span data-ttu-id="88d31-196">DocumentClient의 새로운 upsertXXX 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="88d31-196">New upsertXXX methods on documentClient.</span></span>

### <span data-ttu-id="88d31-197"><a name="1.3.0"/>1.3.0</a></span><span class="sxs-lookup"><span data-stu-id="88d31-197"><a name="1.3.0"/>1.3.0</a></span></span>
* <span data-ttu-id="88d31-198">다른 SDK와 정렬된 버전 번호를 가져오기 위해 건너뛰었습니다.</span><span class="sxs-lookup"><span data-stu-id="88d31-198">Skipped to bring version numbers in alignment with other SDKs.</span></span>

### <span data-ttu-id="88d31-199"><a name="1.2.2"/>1.2.2</a></span><span class="sxs-lookup"><span data-stu-id="88d31-199"><a name="1.2.2"/>1.2.2</a></span></span>
* <span data-ttu-id="88d31-200">프라미스 래퍼를 새 리포지토리로 분할합니다.</span><span class="sxs-lookup"><span data-stu-id="88d31-200">Split Q promises wrapper to new repository.</span></span>
* <span data-ttu-id="88d31-201">npm 레지스트리에 대한 패키지 파일로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="88d31-201">Update to package file for npm registry.</span></span>

### <span data-ttu-id="88d31-202"><a name="1.2.1"/>1.2.1</a></span><span class="sxs-lookup"><span data-stu-id="88d31-202"><a name="1.2.1"/>1.2.1</a></span></span>
* <span data-ttu-id="88d31-203">ID 기반 라우팅을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="88d31-203">Implements ID Based Routing.</span></span>
* <span data-ttu-id="88d31-204">문제 [#49](https://github.com/Azure/azure-documentdb-node/issues/49) 수정 - 현재 속성이 메서드 current()와 충돌합니다.</span><span class="sxs-lookup"><span data-stu-id="88d31-204">Fixes Issue [#49](https://github.com/Azure/azure-documentdb-node/issues/49) - current property conflicts with method current().</span></span>

### <span data-ttu-id="88d31-205"><a name="1.2.0"/>1.2.0</a></span><span class="sxs-lookup"><span data-stu-id="88d31-205"><a name="1.2.0"/>1.2.0</a></span></span>
* <span data-ttu-id="88d31-206">지리 공간 인덱스에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="88d31-206">Added support for GeoSpatial index.</span></span>
* <span data-ttu-id="88d31-207">모든 리소스에 대한 ID 속성의 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="88d31-207">Validates id property for all resources.</span></span> <span data-ttu-id="88d31-208">리소스의 ID는 ?, /, #, &#47;&#47; 문자를 포함할 수 없으며 공백으로 끝날 수도 없습니다.</span><span class="sxs-lookup"><span data-stu-id="88d31-208">Ids for resources cannot contain ?, /, #, &#47;&#47;, characters or end with a space.</span></span>
* <span data-ttu-id="88d31-209">새 헤더 "인덱스 변환 진행률"을 ResourceResponse에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="88d31-209">Adds new header "index transformation progress" to ResourceResponse.</span></span>

### <span data-ttu-id="88d31-210"><a name="1.1.0"/>1.1.0</a></span><span class="sxs-lookup"><span data-stu-id="88d31-210"><a name="1.1.0"/>1.1.0</a></span></span>
* <span data-ttu-id="88d31-211">V2 인덱싱 정책을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="88d31-211">Implements V2 indexing policy.</span></span>

### <span data-ttu-id="88d31-212"><a name="1.0.3"/>1.0.3</a></span><span class="sxs-lookup"><span data-stu-id="88d31-212"><a name="1.0.3"/>1.0.3</a></span></span>
* <span data-ttu-id="88d31-213">문제 [#40](https://github.com/Azure/azure-documentdb-node/issues/40) - 핵심 및 프라미스 SDK에서 eslint 및 grunt 구성을 구현했습니다.</span><span class="sxs-lookup"><span data-stu-id="88d31-213">Issue [#40](https://github.com/Azure/azure-documentdb-node/issues/40) - Implemented eslint and grunt configurations in the core and promise SDK.</span></span>

### <span data-ttu-id="88d31-214"><a name="1.0.2"/>1.0.2</a></span><span class="sxs-lookup"><span data-stu-id="88d31-214"><a name="1.0.2"/>1.0.2</a></span></span>
* <span data-ttu-id="88d31-215">문제 [#45](https://github.com/Azure/azure-documentdb-node/issues/45) - 프라미스 래퍼에 오류가 있는 헤더가 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="88d31-215">Issue [#45](https://github.com/Azure/azure-documentdb-node/issues/45) - Promises wrapper does not include header with error.</span></span>

### <span data-ttu-id="88d31-216"><a name="1.0.1"/>1.0.1</a></span><span class="sxs-lookup"><span data-stu-id="88d31-216"><a name="1.0.1"/>1.0.1</a></span></span>
* <span data-ttu-id="88d31-217">readConflicts, readConflictAsync 및 queryConflicts를 추가하여 충돌을 쿼리하는 기능을 구현했습니다.</span><span class="sxs-lookup"><span data-stu-id="88d31-217">Implemented ability to query for conflicts by adding readConflicts, readConflictAsync, and queryConflicts.</span></span>
* <span data-ttu-id="88d31-218">API 설명서가 업데이트되었습니다.</span><span class="sxs-lookup"><span data-stu-id="88d31-218">Updated API documentation.</span></span>
* <span data-ttu-id="88d31-219">문제 [#41](https://github.com/Azure/azure-documentdb-node/issues/41) - client.createDocumentAsync 오류</span><span class="sxs-lookup"><span data-stu-id="88d31-219">Issue [#41](https://github.com/Azure/azure-documentdb-node/issues/41) - client.createDocumentAsync error.</span></span>

### <span data-ttu-id="88d31-220"><a name="1.0.0"/>1.0.0</a></span><span class="sxs-lookup"><span data-stu-id="88d31-220"><a name="1.0.0"/>1.0.0</a></span></span>
* <span data-ttu-id="88d31-221">GA SDK.</span><span class="sxs-lookup"><span data-stu-id="88d31-221">GA SDK.</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="88d31-222">릴리스 및 사용 중지 날짜</span><span class="sxs-lookup"><span data-stu-id="88d31-222">Release & Retirement Dates</span></span>
<span data-ttu-id="88d31-223">Microsoft는 최신/지원 버전으로 원활히 전환할 수 있도록 SDK 사용 중지 최소 **12개월** 전에 알림을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="88d31-223">Microsoft provides notification at least **12 months** in advance of retiring an SDK in order to smooth the transition to a newer/supported version.</span></span>

<span data-ttu-id="88d31-224">새로운 기능 및 최적화는 현재 SDK에만 추가되어 있으며, 따라서 항상 최신 SDK 버전으로 가능한 한 빨리 업그레이드할 것을 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="88d31-224">New features and functionality and optimizations are only added to the current SDK, as such it is  recommended that you always upgrade to the latest SDK version as early as possible.</span></span>

<span data-ttu-id="88d31-225">사용 중지된 SDK를 사용하는 Cosmos DB에 대한 요청은 서비스에서 거부됩니다.</span><span class="sxs-lookup"><span data-stu-id="88d31-225">Any request to Cosmos DB using a retired SDK is be rejected by the service.</span></span>

<br/>

| <span data-ttu-id="88d31-226">버전</span><span class="sxs-lookup"><span data-stu-id="88d31-226">Version</span></span> | <span data-ttu-id="88d31-227">릴리스 날짜</span><span class="sxs-lookup"><span data-stu-id="88d31-227">Release Date</span></span> | <span data-ttu-id="88d31-228">사용 중지 날짜</span><span class="sxs-lookup"><span data-stu-id="88d31-228">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="88d31-229">1.12.2</span><span class="sxs-lookup"><span data-stu-id="88d31-229">1.12.2</span></span>](#1.12.2) |<span data-ttu-id="88d31-230">2017년 8월 10일</span><span class="sxs-lookup"><span data-stu-id="88d31-230">August 10, 2017</span></span> |--- |
| [<span data-ttu-id="88d31-231">1.12.1</span><span class="sxs-lookup"><span data-stu-id="88d31-231">1.12.1</span></span>](#1.12.1) |<span data-ttu-id="88d31-232">2017년 8월 10일</span><span class="sxs-lookup"><span data-stu-id="88d31-232">August 10, 2017</span></span> |--- |
| [<span data-ttu-id="88d31-233">1.12.0</span><span class="sxs-lookup"><span data-stu-id="88d31-233">1.12.0</span></span>](#1.12.0) |<span data-ttu-id="88d31-234">2017년 5월 10일</span><span class="sxs-lookup"><span data-stu-id="88d31-234">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="88d31-235">1.11.0</span><span class="sxs-lookup"><span data-stu-id="88d31-235">1.11.0</span></span>](#1.11.0) |<span data-ttu-id="88d31-236">2017년 3월 16일</span><span class="sxs-lookup"><span data-stu-id="88d31-236">March 16, 2017</span></span> |--- |
| [<span data-ttu-id="88d31-237">1.10.2</span><span class="sxs-lookup"><span data-stu-id="88d31-237">1.10.2</span></span>](#1.10.2) |<span data-ttu-id="88d31-238">2017년 1월 27일</span><span class="sxs-lookup"><span data-stu-id="88d31-238">January 27, 2017</span></span> |--- |
| [<span data-ttu-id="88d31-239">1.10.1</span><span class="sxs-lookup"><span data-stu-id="88d31-239">1.10.1</span></span>](#1.10.1) |<span data-ttu-id="88d31-240">2016년 12월 22일</span><span class="sxs-lookup"><span data-stu-id="88d31-240">December 22, 2016</span></span> |--- |
| [<span data-ttu-id="88d31-241">1.10.0</span><span class="sxs-lookup"><span data-stu-id="88d31-241">1.10.0</span></span>](#1.10.0) |<span data-ttu-id="88d31-242">2016년 10월 3일</span><span class="sxs-lookup"><span data-stu-id="88d31-242">October 03, 2016</span></span> |--- |
| [<span data-ttu-id="88d31-243">1.9.0</span><span class="sxs-lookup"><span data-stu-id="88d31-243">1.9.0</span></span>](#1.9.0) |<span data-ttu-id="88d31-244">2016년 7월 7일</span><span class="sxs-lookup"><span data-stu-id="88d31-244">July 07, 2016</span></span> |--- |
| [<span data-ttu-id="88d31-245">1.8.0</span><span class="sxs-lookup"><span data-stu-id="88d31-245">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="88d31-246">2016년 6월 14일</span><span class="sxs-lookup"><span data-stu-id="88d31-246">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="88d31-247">1.7.0</span><span class="sxs-lookup"><span data-stu-id="88d31-247">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="88d31-248">2016년 4월 26일</span><span class="sxs-lookup"><span data-stu-id="88d31-248">April 26, 2016</span></span> |--- |
| [<span data-ttu-id="88d31-249">1.6.0</span><span class="sxs-lookup"><span data-stu-id="88d31-249">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="88d31-250">2016년 3월 29일</span><span class="sxs-lookup"><span data-stu-id="88d31-250">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="88d31-251">1.5.6</span><span class="sxs-lookup"><span data-stu-id="88d31-251">1.5.6</span></span>](#1.5.6) |<span data-ttu-id="88d31-252">2016년 3월 8일</span><span class="sxs-lookup"><span data-stu-id="88d31-252">March 08, 2016</span></span> |--- |
| [<span data-ttu-id="88d31-253">1.5.5</span><span class="sxs-lookup"><span data-stu-id="88d31-253">1.5.5</span></span>](#1.5.5) |<span data-ttu-id="88d31-254">2016년 2월 2일</span><span class="sxs-lookup"><span data-stu-id="88d31-254">February 02, 2016</span></span> |--- |
| [<span data-ttu-id="88d31-255">1.5.4</span><span class="sxs-lookup"><span data-stu-id="88d31-255">1.5.4</span></span>](#1.5.4) |<span data-ttu-id="88d31-256">2016년 2월 1일</span><span class="sxs-lookup"><span data-stu-id="88d31-256">February 01, 2016</span></span> |--- |
| [<span data-ttu-id="88d31-257">1.5.2</span><span class="sxs-lookup"><span data-stu-id="88d31-257">1.5.2</span></span>](#1.5.2) |<span data-ttu-id="88d31-258">2016년 1월 26일</span><span class="sxs-lookup"><span data-stu-id="88d31-258">January 26, 2016</span></span> |--- |
| [<span data-ttu-id="88d31-259">1.5.2</span><span class="sxs-lookup"><span data-stu-id="88d31-259">1.5.2</span></span>](#1.5.2) |<span data-ttu-id="88d31-260">2016년 1월 22일</span><span class="sxs-lookup"><span data-stu-id="88d31-260">January 22, 2016</span></span> |--- |
| [<span data-ttu-id="88d31-261">1.5.1</span><span class="sxs-lookup"><span data-stu-id="88d31-261">1.5.1</span></span>](#1.5.1) |<span data-ttu-id="88d31-262">2016년 1월 4일</span><span class="sxs-lookup"><span data-stu-id="88d31-262">January 4, 2016</span></span> |--- |
| [<span data-ttu-id="88d31-263">1.5.0</span><span class="sxs-lookup"><span data-stu-id="88d31-263">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="88d31-264">2015년 12월 31일</span><span class="sxs-lookup"><span data-stu-id="88d31-264">December 31, 2015</span></span> |--- |
| [<span data-ttu-id="88d31-265">1.4.0</span><span class="sxs-lookup"><span data-stu-id="88d31-265">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="88d31-266">2015년 10월 6일</span><span class="sxs-lookup"><span data-stu-id="88d31-266">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="88d31-267">1.3.0</span><span class="sxs-lookup"><span data-stu-id="88d31-267">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="88d31-268">2015년 10월 6일</span><span class="sxs-lookup"><span data-stu-id="88d31-268">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="88d31-269">1.2.2</span><span class="sxs-lookup"><span data-stu-id="88d31-269">1.2.2</span></span>](#1.2.2) |<span data-ttu-id="88d31-270">2015년 9월 10일</span><span class="sxs-lookup"><span data-stu-id="88d31-270">September 10, 2015</span></span> |--- |
| [<span data-ttu-id="88d31-271">1.2.1</span><span class="sxs-lookup"><span data-stu-id="88d31-271">1.2.1</span></span>](#1.2.1) |<span data-ttu-id="88d31-272">2015년 8월 15일</span><span class="sxs-lookup"><span data-stu-id="88d31-272">August 15, 2015</span></span> |--- |
| [<span data-ttu-id="88d31-273">1.2.0</span><span class="sxs-lookup"><span data-stu-id="88d31-273">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="88d31-274">2015년 8월 5일</span><span class="sxs-lookup"><span data-stu-id="88d31-274">August 05, 2015</span></span> |--- |
| [<span data-ttu-id="88d31-275">1.1.0</span><span class="sxs-lookup"><span data-stu-id="88d31-275">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="88d31-276">2015년 7월 9일</span><span class="sxs-lookup"><span data-stu-id="88d31-276">July 09, 2015</span></span> |--- |
| [<span data-ttu-id="88d31-277">1.0.3</span><span class="sxs-lookup"><span data-stu-id="88d31-277">1.0.3</span></span>](#1.0.3) |<span data-ttu-id="88d31-278">2015년 6월 4일</span><span class="sxs-lookup"><span data-stu-id="88d31-278">June 04, 2015</span></span> |--- |
| [<span data-ttu-id="88d31-279">1.0.2</span><span class="sxs-lookup"><span data-stu-id="88d31-279">1.0.2</span></span>](#1.0.2) |<span data-ttu-id="88d31-280">2015년 5월 23일</span><span class="sxs-lookup"><span data-stu-id="88d31-280">May 23, 2015</span></span> |--- |
| [<span data-ttu-id="88d31-281">1.0.1</span><span class="sxs-lookup"><span data-stu-id="88d31-281">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="88d31-282">2015년 5월 15일</span><span class="sxs-lookup"><span data-stu-id="88d31-282">May 15, 2015</span></span> |--- |
| [<span data-ttu-id="88d31-283">1.0.0</span><span class="sxs-lookup"><span data-stu-id="88d31-283">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="88d31-284">2015년 4월 8일</span><span class="sxs-lookup"><span data-stu-id="88d31-284">April 08, 2015</span></span> |--- |

## <a name="faq"></a><span data-ttu-id="88d31-285">FAQ</span><span class="sxs-lookup"><span data-stu-id="88d31-285">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="88d31-286">참고 항목</span><span class="sxs-lookup"><span data-stu-id="88d31-286">See also</span></span>
<span data-ttu-id="88d31-287">Cosmos DB에 대한 자세한 내용은 [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) 서비스 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="88d31-287">To learn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span>


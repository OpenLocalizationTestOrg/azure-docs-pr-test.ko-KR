---
title: "aaaAzure Cosmos DB.NET SDK 및 리소스 | Microsoft Docs"
description: ".NET API 및 SDK 릴리스 날짜, 사용 중지 날짜 및 hello Cosmos DB AZURE.NET SDK의 각 버전 간의 변경 내용을 포함 하 여 hello에 대 한 모든에 대해 알아봅니다."
services: cosmos-db
documentationcenter: .net
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 8e239217-9085-49f5-b0a7-58d6e6b61949
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/11/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0ec30e0130067a9b8d4c9176cf7465bac8925bf9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-net-sdk-download-and-release-notes"></a><span data-ttu-id="49842-103">Azure Cosmos DB .NET SDK: 다운로드 및 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="49842-103">Azure Cosmos DB .NET SDK: Download and release notes</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="49842-104">.NET</span><span class="sxs-lookup"><span data-stu-id="49842-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="49842-105">.NET 변경 피드</span><span class="sxs-lookup"><span data-stu-id="49842-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="49842-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="49842-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="49842-107">Node.JS</span><span class="sxs-lookup"><span data-stu-id="49842-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="49842-108">Java</span><span class="sxs-lookup"><span data-stu-id="49842-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="49842-109">Python</span><span class="sxs-lookup"><span data-stu-id="49842-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="49842-110">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="49842-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="49842-111">REST 리소스 공급자</span><span class="sxs-lookup"><span data-stu-id="49842-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="49842-112">SQL</span><span class="sxs-lookup"><span data-stu-id="49842-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="49842-113">**SDK 다운로드**</span><span class="sxs-lookup"><span data-stu-id="49842-113">**SDK download**</span></span></td><td>[<span data-ttu-id="49842-114">NuGet</span><span class="sxs-lookup"><span data-stu-id="49842-114">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/)</td></tr>

<tr><td><span data-ttu-id="49842-115">**API 설명서**</span><span class="sxs-lookup"><span data-stu-id="49842-115">**API documentation**</span></span></td><td>[<span data-ttu-id="49842-116">.NET API 참조 설명서</span><span class="sxs-lookup"><span data-stu-id="49842-116">.NET API reference documentation</span></span>](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet)</td></tr>

<tr><td><span data-ttu-id="49842-117">**샘플**</span><span class="sxs-lookup"><span data-stu-id="49842-117">**Samples**</span></span></td><td>[<span data-ttu-id="49842-118">.NET 코드 샘플</span><span class="sxs-lookup"><span data-stu-id="49842-118">.NET code samples</span></span>](documentdb-dotnet-samples.md)</td></tr>

<tr><td><span data-ttu-id="49842-119">**시작**</span><span class="sxs-lookup"><span data-stu-id="49842-119">**Get started**</span></span></td><td>[<span data-ttu-id="49842-120">Cosmos DB AZURE.NET SDK hello로 시작.</span><span class="sxs-lookup"><span data-stu-id="49842-120">Get started with hello Azure Cosmos DB .NET SDK</span></span>](documentdb-get-started.md)</td></tr>

<tr><td><span data-ttu-id="49842-121">**웹앱 자습서**</span><span class="sxs-lookup"><span data-stu-id="49842-121">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="49842-122">Azure Cosmos DB를 사용한 웹 응용 프로그램 개발</span><span class="sxs-lookup"><span data-stu-id="49842-122">Web application development with Azure Cosmos DB</span></span>](documentdb-dotnet-application.md)</td></tr>

<tr><td><span data-ttu-id="49842-123">**현재 지원되는 프레임워크**</span><span class="sxs-lookup"><span data-stu-id="49842-123">**Current supported framework**</span></span></td><td>[<span data-ttu-id="49842-124">Microsoft .NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="49842-124">Microsoft .NET Framework 4.5</span></span>](https://www.microsoft.com/download/details.aspx?id=30653)</td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="49842-125">릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="49842-125">Release notes</span></span>

### <a name="a-name11701170"></a><span data-ttu-id="49842-126"><a name="1.17.0"/>1.17.0</span><span class="sxs-lookup"><span data-stu-id="49842-126"><a name="1.17.0"/>1.17.0</span></span> 

* <span data-ttu-id="49842-127">쿼리 결과 tooa 특정 파티션 키 범위 값의 범위를 지정 하는 것에 대 한 FeedOption으로 PartitionKeyRangeId에 대 한 지원이 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="49842-127">Added support for PartitionKeyRangeId as a FeedOption for scoping query results tooa specific partition key range value.</span></span> 
* <span data-ttu-id="49842-128">해당 시간 이후에 hello 변경 내용 검색 ChangeFeedOption toostart로 StartTime에 대 한 지원이 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="49842-128">Added support for StartTime as a ChangeFeedOption toostart looking for hello changes after that time.</span></span>

### <a name="a-name11611161"></a><span data-ttu-id="49842-129"><a name="1.16.1"/>1.16.1</span><span class="sxs-lookup"><span data-stu-id="49842-129"><a name="1.16.1"/>1.16.1</span></span>
* <span data-ttu-id="49842-130">Hello 스택 오버플로 예외를 일으킬 수 있는 JsonSerializable 클래스에에서는 문제가 해결 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="49842-130">Fixed an issue in hello JsonSerializable class that may cause a stack overflow exception.</span></span>

### <a name="a-name11601160"></a><span data-ttu-id="49842-131"><a name="1.16.0"/>1.16.0</span><span class="sxs-lookup"><span data-stu-id="49842-131"><a name="1.16.0"/>1.16.0</span></span>
*   <span data-ttu-id="49842-132">Hello DocumentClient 생성자에서 선택적 매개 변수로 인해 JsonSerializerSettings toohello 도입 hello 응용 프로그램의 다시 컴파일하는 데 필요한 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="49842-132">Fixed an issue that required recompiling of hello application due toohello introduction of JsonSerializerSettings as an optional parameter in hello DocumentClient constructor.</span></span>
* <span data-ttu-id="49842-133">표시 된 hello DocumentClient 사용 되지 않는 생성자에 JsonSerializerSettings 매개 변수를 전달할 때 ConnectionPolicy 및 ConsistencyLevel 매개 변수 기본값에 대 한 마지막 매개 변수 tooallow hello와 JsonSerializerSettings를 필요한입니다.</span><span class="sxs-lookup"><span data-stu-id="49842-133">Marked hello DocumentClient constructor obsolete that required JsonSerializerSettings as hello last parameter tooallow for default values of ConnectionPolicy and ConsistencyLevel parameters when passing in JsonSerializerSettings parameter.</span></span>

### <a name="a-name11501150"></a><span data-ttu-id="49842-134"><a name="1.15.0"/>1.15.0</span><span class="sxs-lookup"><span data-stu-id="49842-134"><a name="1.15.0"/>1.15.0</span></span>
*   <span data-ttu-id="49842-135">[DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet)를 인스턴스화하는 동안 사용자 지정 JsonSerializerSettings를 지정하기 위한 지원을 추가하였습니다.</span><span class="sxs-lookup"><span data-stu-id="49842-135">Added support for specifying custom JsonSerializerSettings while instantiating [DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet).</span></span>

### <a name="a-name11411141"></a><span data-ttu-id="49842-136"><a name="1.14.1"/>1.14.1</span><span class="sxs-lookup"><span data-stu-id="49842-136"><a name="1.14.1"/>1.14.1</span></span>
*   <span data-ttu-id="49842-137">SSE4 명령을 지원하지 않고 Azure Cosmos DB DocumentDB API 쿼리를 실행할 때 SEHException을 throw하는 x64 컴퓨터에 영향을 준 문제가 해결되었습니다.</span><span class="sxs-lookup"><span data-stu-id="49842-137">Fixed an issue that affected x64 machines that don’t support SSE4 instruction and throw an SEHException when running Azure Cosmos DB DocumentDB API queries.</span></span>

### <a name="a-name11401140"></a><span data-ttu-id="49842-138"><a name="1.14.0"/>1.14.0</span><span class="sxs-lookup"><span data-stu-id="49842-138"><a name="1.14.0"/>1.14.0</span></span>
*   <span data-ttu-id="49842-139">ConsistentPrefix라는 새로운 일관성 수준에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="49842-139">Added support for a new consistency level called ConsistentPrefix.</span></span>
*   <span data-ttu-id="49842-140">개별 파티션의 쿼리 메트릭에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="49842-140">Added support for query metrics for individual partitions.</span></span>
*   <span data-ttu-id="49842-141">쿼리에 대 한 hello 연속 토큰의 hello 크기 제한에 대 한 지원이 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="49842-141">Added support for limiting hello size of hello continuation token for queries.</span></span>
*   <span data-ttu-id="49842-142">실패한 요청의 자세한 추적에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="49842-142">Added support for more detailed tracing for failed requests.</span></span>
*   <span data-ttu-id="49842-143">Hello SDK 일부 성능 향상이 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="49842-143">Made some performance improvements in hello SDK.</span></span>

### <a name="a-name11341134"></a><span data-ttu-id="49842-144"><a name="1.13.4"/>1.13.4</span><span class="sxs-lookup"><span data-stu-id="49842-144"><a name="1.13.4"/>1.13.4</span></span>
* <span data-ttu-id="49842-145">기능적으로 1.13.3과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="49842-145">Functionally same as 1.13.3.</span></span> <span data-ttu-id="49842-146">내부적으로 약간 변경되었습니다.</span><span class="sxs-lookup"><span data-stu-id="49842-146">Made some internal changes.</span></span>

### <a name="a-name11331133"></a><span data-ttu-id="49842-147"><a name="1.13.3"/>1.13.3</span><span class="sxs-lookup"><span data-stu-id="49842-147"><a name="1.13.3"/>1.13.3</span></span>
* <span data-ttu-id="49842-148">기능적으로 1.13.2와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="49842-148">Functionally same as 1.13.2.</span></span> <span data-ttu-id="49842-149">내부적으로 약간 변경되었습니다.</span><span class="sxs-lookup"><span data-stu-id="49842-149">Made some internal changes.</span></span>

### <a name="a-name11321132"></a><span data-ttu-id="49842-150"><a name="1.13.2"/>1.13.2</span><span class="sxs-lookup"><span data-stu-id="49842-150"><a name="1.13.2"/>1.13.2</span></span>
* <span data-ttu-id="49842-151">집계 쿼리에 대 한 FeedOptions에 제공 된 hello PartitionKey 값을 무시 하는 문제가 해결 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="49842-151">Fixed an issue that ignored hello PartitionKey value provided in FeedOptions for aggregate queries.</span></span>
* <span data-ttu-id="49842-152">플라이트 중간의 파티션 간 Order By 쿼리를 실행하는 동안 파티션 관리의 투명한 처리 문제를 해결했습니다.</span><span class="sxs-lookup"><span data-stu-id="49842-152">Fixed an issue in transparent handling of partition management during mid-flight cross-partition Order By query execution.</span></span>

### <a name="a-name11311131"></a><span data-ttu-id="49842-153"><a name="1.13.1"/>1.13.1</span><span class="sxs-lookup"><span data-stu-id="49842-153"><a name="1.13.1"/>1.13.1</span></span>
* <span data-ttu-id="49842-154">Hello 비동기 ASP.NET 컨텍스트 내에서 사용 하는 경우 Api의 일부에서 교착 상태를 일으킨 문제가 해결 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="49842-154">Fixed an issue which caused deadlocks in some of hello async APIs when used inside ASP.NET context.</span></span>

### <a name="a-name11301130"></a><span data-ttu-id="49842-155"><a name="1.13.0"/>1.13.0</span><span class="sxs-lookup"><span data-stu-id="49842-155"><a name="1.13.0"/>1.13.0</span></span>
* <span data-ttu-id="49842-156">SDK toomake 더 해결 특정 조건에서 탄력적인 tooautomatic 장애 조치 합니다.</span><span class="sxs-lookup"><span data-stu-id="49842-156">Fixes toomake SDK more resilient tooautomatic failover under certain conditions.</span></span>

### <a name="a-name11221122"></a><span data-ttu-id="49842-157"><a name="1.12.2"/>1.12.2</span><span class="sxs-lookup"><span data-stu-id="49842-157"><a name="1.12.2"/>1.12.2</span></span>
* <span data-ttu-id="49842-158">경우에 따라 WebException을 야기 하는 문제에 대 한 수정: hello 원격 이름을 확인할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="49842-158">Fix for an issue that occasionally causes a WebException: hello remote name could not be resolved.</span></span>
* <span data-ttu-id="49842-159">추가 된 hello 직접 새 오버 로드 tooReadDocumentAsync API를 추가 하 여 형식화 된 문서를 읽기 위한 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="49842-159">Added hello support for directly reading a typed document by adding new overloads tooReadDocumentAsync API.</span></span>

### <a name="a-name11211121"></a><span data-ttu-id="49842-160"><a name="1.12.1"/>1.12.1</span><span class="sxs-lookup"><span data-stu-id="49842-160"><a name="1.12.1"/>1.12.1</span></span>
* <span data-ttu-id="49842-161">집계 쿼리(COUNT, MIN, MAX, SUM 및 AVG)에 대한 LINQ 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="49842-161">Added LINQ support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="49842-162">용 hello 이벤트 처리기를 사용 하 여 발생 하는 hello ConnectionPolicy 개체에 대 한 메모리 누수 문제를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="49842-162">Fix for a memory leak issue for hello ConnectionPolicy object caused by hello use of event handler.</span></span>
* <span data-ttu-id="49842-163">ETag를 사용할 때 UpsertAttachmentAsync가 작동하지 않는 문제를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="49842-163">Fix for an issue wherein UpsertAttachmentAsync was not working when ETag was used.</span></span>
* <span data-ttu-id="49842-164">문자열 필드를 정렬할 때 파티션 간 order-by 쿼리 연속 작업이 작동하지 않는 문제를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="49842-164">Fix for an issue wherein cross partition order-by query continuation was not working when sorting on string field.</span></span>

### <a name="a-name11201120"></a><span data-ttu-id="49842-165"><a name="1.12.0"/>1.12.0</span><span class="sxs-lookup"><span data-stu-id="49842-165"><a name="1.12.0"/>1.12.0</span></span>
* <span data-ttu-id="49842-166">집계 쿼리(COUNT, MIN, MAX, SUM 및 AVG)에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="49842-166">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span> <span data-ttu-id="49842-167">[집계 지원](documentdb-sql-query.md#Aggregates)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="49842-167">See [Aggregation support](documentdb-sql-query.md#Aggregates).</span></span>
* <span data-ttu-id="49842-168">10,100 000RU/s too2500 000RU/s에서 분할 된 컬렉션에 대해 최소 처리량을 적어집니다.</span><span class="sxs-lookup"><span data-stu-id="49842-168">Lowered minimum throughput on partitioned collections from 10,100 RU/s too2500 RU/s.</span></span>

### <a name="a-name11141114"></a><span data-ttu-id="49842-169"><a name="1.11.4"/>1.11.4</span><span class="sxs-lookup"><span data-stu-id="49842-169"><a name="1.11.4"/>1.11.4</span></span>
* <span data-ttu-id="49842-170">여기서 hello 32 비트 호스트 프로세스에 실패 했던 hello 크로스 파티션 쿼리의 일부 문제를 수정 하세요.</span><span class="sxs-lookup"><span data-stu-id="49842-170">Fix for an issue wherein some of hello cross-partition queries were failing in hello 32-bit host process.</span></span>
* <span data-ttu-id="49842-171">여기서 hello 세션 컨테이너 되 고 새로 고쳐지지 않았습니다 게이트웨이 모드에서 실패 한 요청에 대 한 hello 토큰으로 문제를 수정 하세요.</span><span class="sxs-lookup"><span data-stu-id="49842-171">Fix for an issue wherein hello session container was not being updated with hello token for failed requests in Gateway mode.</span></span>
* <span data-ttu-id="49842-172">경우에 따라 프로젝션에서 UDF 호출을 사용하는 쿼리가 실패하는 문제를 수정했습니다.</span><span class="sxs-lookup"><span data-stu-id="49842-172">Fix for an issue wherein a query with UDF calls in projection was failing in some cases.</span></span>
* <span data-ttu-id="49842-173">Hello 증가 하는 것에 대 한 클라이언트 쪽 성능 수정 읽고의 hello 요청 처리량을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="49842-173">Client side performance fixes for increasing hello read and write throughput of hello requests.</span></span>

### <a name="a-name11131113"></a><span data-ttu-id="49842-174"><a name="1.11.3"/>1.11.3</span><span class="sxs-lookup"><span data-stu-id="49842-174"><a name="1.11.3"/>1.11.3</span></span>
* <span data-ttu-id="49842-175">여기서 hello 세션 컨테이너 업데이트 되지 않았습니다 되 고 실패 한 요청에 대 한 hello 토큰으로 문제를 수정 하세요.</span><span class="sxs-lookup"><span data-stu-id="49842-175">Fix for an issue wherein hello session container was not being updated with hello token for failed requests.</span></span>
* <span data-ttu-id="49842-176">Hello SDK toowork 32 비트 호스트 프로세스에서에 대 한 지원이 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="49842-176">Added support for hello SDK toowork in a 32-bit host process.</span></span> <span data-ttu-id="49842-177">파티션 간 쿼리를 사용하는 경우 향상된 성능을 위해 64비트 호스트를 처리하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="49842-177">Note that if you use cross partition queries, 64-bit host processing is recommended for improved performance.</span></span>
* <span data-ttu-id="49842-178">IN 식에 많은 수의 파티션 키 값을 사용하는 쿼리와 관련된 시나리오의 성능이 향상되었습니다.</span><span class="sxs-lookup"><span data-stu-id="49842-178">Improved performance for scenarios involving queries with a large number of partition key values in an IN expression.</span></span>
* <span data-ttu-id="49842-179">PopulateQuotaInfo 요청 옵션이 설정 된 경우 문서 컬렉션 읽기 요청에 대 한 다양 한 리소스 할당량 stats를 ResourceResponse hello에 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="49842-179">Populated various resource quota stats in hello ResourceResponse for document collection read requests when PopulateQuotaInfo request option is set.</span></span>

### <a name="a-name11111111"></a><span data-ttu-id="49842-180"><a name="1.11.1"/>1.11.1</span><span class="sxs-lookup"><span data-stu-id="49842-180"><a name="1.11.1"/>1.11.1</span></span>
* <span data-ttu-id="49842-181">Hello 1.11.0에 도입 된 CreateDocumentCollectionIfNotExistsAsync API에 대 한 보조 성능 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="49842-181">Minor performance fix for hello CreateDocumentCollectionIfNotExistsAsync API introduced in 1.11.0.</span></span>
* <span data-ttu-id="49842-182">높은 수준의 동시 요청 수를 포함 하는 시나리오에 대 한 hello SDK의에서 성능 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="49842-182">Performance fix in hello SDK for scenarios that involve high degree of concurrent requests.</span></span>

### <a name="a-name11101110"></a><span data-ttu-id="49842-183"><a name="1.11.0"/>1.11.0</span><span class="sxs-lookup"><span data-stu-id="49842-183"><a name="1.11.0"/>1.11.0</span></span>
* <span data-ttu-id="49842-184">새 클래스 및 메서드 tooprocess hello에 대 한 지원 [피드 변경](change-feed.md) 컬렉션 내에서 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="49842-184">Support for new classes and methods tooprocess hello [change feed](change-feed.md) of documents within a collection.</span></span>
* <span data-ttu-id="49842-185">파티션 간 쿼리 연속 및 파티션 간 쿼리에 대한 일부 성능 향상 지원</span><span class="sxs-lookup"><span data-stu-id="49842-185">Support for cross-partition query continuation and some perf improvements for cross-partition queries.</span></span>
* <span data-ttu-id="49842-186">CreateDatabaseIfNotExistsAsync 및 CreateDocumentCollectionIfNotExistsAsync 메서드 추가</span><span class="sxs-lookup"><span data-stu-id="49842-186">Addition of CreateDatabaseIfNotExistsAsync and CreateDocumentCollectionIfNotExistsAsync methods.</span></span>
* <span data-ttu-id="49842-187">시스템 함수에 대한 LINQ 지원: IsDefined, IsNull 및 IsPrimitive</span><span class="sxs-lookup"><span data-stu-id="49842-187">LINQ support for system functions: IsDefined, IsNull and IsPrimitive.</span></span>
* <span data-ttu-id="49842-188">프로젝트에 project.json 도구와 hello Nuget 패키지를 사용 하는 경우 자동 binplacing Microsoft.Azure.Documents.ServiceInterop.dll 및 DocumentDB.Spatial.Sql.dll 어셈블리 tooapplication의 bin 폴더에 대 한 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="49842-188">Fix for automatic binplacing of Microsoft.Azure.Documents.ServiceInterop.dll and DocumentDB.Spatial.Sql.dll assemblies tooapplication’s bin folder when using hello Nuget package with projects that have project.json tooling.</span></span>
* <span data-ttu-id="49842-189">시나리오를 디버깅하는 데 도움이 될 수 있는 클라이언트 쪽 ETW 추적 내보내기 지원</span><span class="sxs-lookup"><span data-stu-id="49842-189">Support for emitting client side ETW traces which could be helpful in debugging scenarios.</span></span>

### <a name="a-name11001100"></a><span data-ttu-id="49842-190"><a name="1.10.0"/>1.10.0</span><span class="sxs-lookup"><span data-stu-id="49842-190"><a name="1.10.0"/>1.10.0</span></span>
* <span data-ttu-id="49842-191">분할된 컬렉션에 대한 직접 연결 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="49842-191">Added direct connectivity support for partitioned collections.</span></span>
* <span data-ttu-id="49842-192">Hello Bounded Staleness 일관성 수준에 대 한 성능이 향상 됩니다.</span><span class="sxs-lookup"><span data-stu-id="49842-192">Improved performance for hello Bounded Staleness consistency level.</span></span>
* <span data-ttu-id="49842-193">지역 펜싱 공간 쿼리에 대한 컬렉션 인덱싱 정책을 지정하는 동안 Polygon 및 LineString 데이터 형식이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="49842-193">Added Polygon and LineString DataTypes while specifying collection indexing policy for geo-fencing spatial queries.</span></span>
* <span data-ttu-id="49842-194">조건자를 변환하는 동안 StringEnumConverter, IsoDateTimeConverter 및 UnixDateTimeConverter에 대한 LINQ 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="49842-194">Added LINQ support for StringEnumConverter, IsoDateTimeConverter and UnixDateTimeConverter while translating predicates.</span></span>
* <span data-ttu-id="49842-195">다양한 SDK 버그가 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="49842-195">Various SDK bug fixes.</span></span>

### <a name="a-name195195"></a><span data-ttu-id="49842-196"><a name="1.9.5"/>1.9.5</span><span class="sxs-lookup"><span data-stu-id="49842-196"><a name="1.9.5"/>1.9.5</span></span>
* <span data-ttu-id="49842-197">해당 않아 hello NotFoundException 다음 문제 해결: hello 세션 hello 입력된 세션 토큰을 사용할 수 없으면 읽기입니다.</span><span class="sxs-lookup"><span data-stu-id="49842-197">Fixed an issue that caused hello following NotFoundException: hello read session is not available for hello input session token.</span></span> <span data-ttu-id="49842-198">Hello 읽기 액세스 지리적으로 분산 계정의 지역에 대 한 쿼리 하는 경우에 따라이 예외가 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="49842-198">This exception occurred in some cases when querying for hello read-region of a geo-distributed account.</span></span>
* <span data-ttu-id="49842-199">Hello ResourceResponse 클래스를 통해 응답에서 toohello 내부 스트림에 대 한 직접 액세스의에서 hello ResponseStream 속성을 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="49842-199">Exposed hello ResponseStream property in hello ResourceResponse class, which enables direct access toohello underlying stream from a response.</span></span>

### <a name="a-name194194"></a><span data-ttu-id="49842-200"><a name="1.9.4"/>1.9.4</span><span class="sxs-lookup"><span data-stu-id="49842-200"><a name="1.9.4"/>1.9.4</span></span>
* <span data-ttu-id="49842-201">수정 된 hello ResourceResponse, FeedResponse, StoredProcedureResponse 및 MediaResponse 클래스 tooimplement hello (TDD) 배포를 제어 하는 테스트에 대 한 모의 수 있도록 공용 인터페이스에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="49842-201">Modified hello ResourceResponse, FeedResponse, StoredProcedureResponse and MediaResponse classes tooimplement hello corresponding public interface so that they can be mocked for test driven deployment (TDD).</span></span>
* <span data-ttu-id="49842-202">데이터 직렬화를 위해 사용자 지정 JsonSerializerSettings 개체를 사용할 때 잘못된 파티션 키 헤더가 발생하는 문제가 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="49842-202">Fixed an issue that caused a malformed partition key header when using a custom JsonSerializerSettings object for serializing data.</span></span>

### <a name="a-name193193"></a><span data-ttu-id="49842-203"><a name="1.9.3"/>1.9.3</span><span class="sxs-lookup"><span data-stu-id="49842-203"><a name="1.9.3"/>1.9.3</span></span>
* <span data-ttu-id="49842-204">장기 실행 쿼리 toofail 오류로 인해 발생 하는 문제 해결: 권한 부여 토큰이 잘못 되었습니다. hello에 현재 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="49842-204">Fixed an issue that caused long running queries toofail with error: Authorization token is not valid at hello current time.</span></span>
* <span data-ttu-id="49842-205">제거 하는 문제가 hello 크로스 파티션 top/order by 쿼리에서 원래 SqlParameterCollection 고정 합니다.</span><span class="sxs-lookup"><span data-stu-id="49842-205">Fixed an issue that removed hello original SqlParameterCollection from cross partition top/order-by queries.</span></span>

### <a name="a-name192192"></a><span data-ttu-id="49842-206"><a name="1.9.2"/>1.9.2</span><span class="sxs-lookup"><span data-stu-id="49842-206"><a name="1.9.2"/>1.9.2</span></span>
* <span data-ttu-id="49842-207">분할된 컬렉션에 대한 병렬 쿼리에 지원을 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="49842-207">Added support for parallel queries for partitioned collections.</span></span>
* <span data-ttu-id="49842-208">분할된 컬렉션에 대한 파티션 간 Order By 및 TOP 쿼리에 대한 지원을 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="49842-208">Added support for cross partition ORDER BY and TOP queries for partitioned collections.</span></span>
* <span data-ttu-id="49842-209">누락 된 참조 tooDocumentDB.Spatial.Sql.dll 및 Microsoft.Azure.Documents.ServiceInterop.dll 참조 toohello Azure Cosmos DB Nuget 패키지와 프로그램 Cosmos DB Azure 프로젝트를 참조 하는 경우 필요 없는 고정된 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="49842-209">Fixed hello missing references tooDocumentDB.Spatial.Sql.dll and Microsoft.Azure.Documents.ServiceInterop.dll that are required when referencing an Azure Cosmos DB project with a reference toohello Azure Cosmos DB Nuget package.</span></span>
* <span data-ttu-id="49842-210">LINQ에서 사용자 정의 함수를 사용할 때는 hello 기능 여러 유형의 toouse 매개 변수를 수정 했습니다.</span><span class="sxs-lookup"><span data-stu-id="49842-210">Fixed hello ability toouse parameters of different types when using user-defined functions in LINQ.</span></span> 
* <span data-ttu-id="49842-211">Upsert 호출 쓰기 위치 대신 tooread 방향이 지정 된 위치를 되기 때문에 전역적으로 복제 된 계정에 대 한 버그를 수정 했습니다.</span><span class="sxs-lookup"><span data-stu-id="49842-211">Fixed a bug for globally replicated accounts where Upsert calls were being directed tooread locations instead of write locations.</span></span>
* <span data-ttu-id="49842-212">누락 된 추가 된 메서드 toohello IDocumentClient 인터페이스:</span><span class="sxs-lookup"><span data-stu-id="49842-212">Added methods toohello IDocumentClient interface that were missing:</span></span> 
  * <span data-ttu-id="49842-213">mediaStream 및 options를 매개 변수로 사용하는 UpsertAttachmentAsync 메서드</span><span class="sxs-lookup"><span data-stu-id="49842-213">UpsertAttachmentAsync method that takes mediaStream and options as parameters</span></span>
  * <span data-ttu-id="49842-214">options를 매개 변수로 사용하는 CreateAttachmentAsync 메서드</span><span class="sxs-lookup"><span data-stu-id="49842-214">CreateAttachmentAsync method that takes options as a parameter</span></span>
  * <span data-ttu-id="49842-215">querySpec을 매개 변수로 사용하는 CreateOfferQuery 메서드</span><span class="sxs-lookup"><span data-stu-id="49842-215">CreateOfferQuery method that takes querySpec as a parameter.</span></span>
* <span data-ttu-id="49842-216">Hello IDocumentClient 인터페이스에 노출 되는 봉인 되지 않은 공용 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="49842-216">Unsealed public classes that are exposed in hello IDocumentClient interface.</span></span>

### <a name="a-name180180"></a><span data-ttu-id="49842-217"><a name="1.8.0"/>1.8.0</span><span class="sxs-lookup"><span data-stu-id="49842-217"><a name="1.8.0"/>1.8.0</span></span>
* <span data-ttu-id="49842-218">다중 영역 데이터베이스 계정에 대 한 추가 된 hello 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="49842-218">Added hello support for multi-region database accounts.</span></span>
* <span data-ttu-id="49842-219">정제된 요청에 대한 재시도 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="49842-219">Added support for retry on throttled requests.</span></span>  <span data-ttu-id="49842-220">사용자 hello 재시도 횟수를 사용자 지정할 수 및 hello ConnectionPolicy.RetryOptions 속성을 구성 하 여 hello 최대 대기 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="49842-220">User can customize hello number of retries and hello max wait time by configuring hello ConnectionPolicy.RetryOptions property.</span></span>
* <span data-ttu-id="49842-221">모든 DocumenClient 속성 및 메서드의 hello 시그니처를 정의 하는 새 IDocumentClient 인터페이스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="49842-221">Added a new IDocumentClient interface that defines hello signatures of all DocumenClient properties and methods.</span></span>  <span data-ttu-id="49842-222">이러한 변경의 일환으로, 또한 읽기 전용 이므로 hello DocumentClient 클래스 자체에서 IQueryable 및 IOrderedQueryable toomethods 만드는 확장 메서드</span><span class="sxs-lookup"><span data-stu-id="49842-222">As part of this change, also changed extension methods that create IQueryable and IOrderedQueryable toomethods on hello DocumentClient class itself.</span></span>
* <span data-ttu-id="49842-223">지정된 된 Azure Cosmos DB 끝점 Uri에 대 한 구성 옵션 tooset hello ServicePoint.ConnectionLimit 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="49842-223">Added configuration option tooset hello ServicePoint.ConnectionLimit for a given Azure Cosmos DB endpoint Uri.</span></span>  <span data-ttu-id="49842-224">Too50 설정 되어 있는 ConnectionPolicy.MaxConnectionLimit toochange hello 기본 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="49842-224">Use ConnectionPolicy.MaxConnectionLimit toochange hello default value, which is set too50.</span></span>
* <span data-ttu-id="49842-225">IPartitionResolver와 해당 구현의 사용이 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="49842-225">Deprecated IPartitionResolver and its implementation.</span></span>  <span data-ttu-id="49842-226">IPartitionResolver 지원이 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="49842-226">Support for IPartitionResolver is now obsolete.</span></span> <span data-ttu-id="49842-227">보다 큰 저장소 및 처리량에는 파티션된 컬렉션을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="49842-227">It's recommended that you use Partitioned Collections for higher storage and throughput.</span></span>

### <a name="a-name171171"></a><span data-ttu-id="49842-228"><a name="1.7.1"/>1.7.1</span><span class="sxs-lookup"><span data-stu-id="49842-228"><a name="1.7.1"/>1.7.1</span></span>
* <span data-ttu-id="49842-229">오버 로드 tooUri 기반 RequestOptions 매개 변수로 받아들이는 ExecuteStoredProcedureAsync 방법을 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="49842-229">Added an overload tooUri based ExecuteStoredProcedureAsync method that takes RequestOptions as a parameter.</span></span>

### <a name="a-name170170"></a><span data-ttu-id="49842-230"><a name="1.7.0"/>1.7.0</span><span class="sxs-lookup"><span data-stu-id="49842-230"><a name="1.7.0"/>1.7.0</span></span>
* <span data-ttu-id="49842-231">문서에 대 한 시간 toolive (TTL) 지원이 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="49842-231">Added time toolive (TTL) support for documents.</span></span>

### <a name="a-name163163"></a><span data-ttu-id="49842-232"><a name="1.6.3"/>1.6.3</span><span class="sxs-lookup"><span data-stu-id="49842-232"><a name="1.6.3"/>1.6.3</span></span>
* <span data-ttu-id="49842-233">Azure 클라우드 서비스 솔루션의 일부로 패키징에 대한 .NET SDK의 Nuget 패키징에서 버그가 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="49842-233">Fixed a bug in Nuget packaging of .NET SDK for packaging it as part of an Azure Cloud Service solution.</span></span>

### <a name="a-name162162"></a><span data-ttu-id="49842-234"><a name="1.6.2"/>1.6.2</span><span class="sxs-lookup"><span data-stu-id="49842-234"><a name="1.6.2"/>1.6.2</span></span>
* <span data-ttu-id="49842-235">[분할된 컬렉션](partition-data.md) 및 [사용자 정의 성능 수준](performance-levels.md)이 구현되었습니다.</span><span class="sxs-lookup"><span data-stu-id="49842-235">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span> 

### <a name="a-name153153"></a><span data-ttu-id="49842-236"><a name="1.5.3"/>1.5.3</span><span class="sxs-lookup"><span data-stu-id="49842-236"><a name="1.5.3"/>1.5.3</span></span>
* <span data-ttu-id="49842-237">**[고정]**  Azure Cosmos DB 쿼리 끝점 throw: ' System.Net.Http.HttpRequestException: 콘텐츠 tooa 스트림을 복사 하는 동안 오류 '.</span><span class="sxs-lookup"><span data-stu-id="49842-237">**[Fixed]** Querying Azure Cosmos DB endpoint throws: 'System.Net.Http.HttpRequestException: Error while copying content tooa stream'.</span></span>

### <a name="a-name152152"></a><span data-ttu-id="49842-238"><a name="1.5.2"/>1.5.2</span><span class="sxs-lookup"><span data-stu-id="49842-238"><a name="1.5.2"/>1.5.2</span></span>
* <span data-ttu-id="49842-239">페이징, 조건식 및 범위 비교에 대한 새 연산자를 포함하는 LINQ 지원이 확장되었습니다.</span><span class="sxs-lookup"><span data-stu-id="49842-239">Expanded LINQ support including new operators for paging, conditional expressions, and range comparison.</span></span>
  * <span data-ttu-id="49842-240">Linq에서 연산자 tooenable SELECT TOP 동작 수행</span><span class="sxs-lookup"><span data-stu-id="49842-240">Take operator tooenable SELECT TOP behavior in LINQ</span></span>
  * <span data-ttu-id="49842-241">CompareTo 연산자 tooenable 문자열 범위 비교</span><span class="sxs-lookup"><span data-stu-id="49842-241">CompareTo operator tooenable string range comparisons</span></span>
  * <span data-ttu-id="49842-242">조건부 (?) 및 병합 연산자 (??)</span><span class="sxs-lookup"><span data-stu-id="49842-242">Conditional (?) and coalesce operators (??)</span></span>
* <span data-ttu-id="49842-243">**[수정됨]** 모델 프로젝션을 LINQ 쿼리의 Where-In과 결합할 때의 ArgumentOutOfRangeException이 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="49842-243">**[Fixed]** ArgumentOutOfRangeException when combining Model projection with Where-In in a LINQ query.</span></span> [<span data-ttu-id="49842-244">#81</span><span class="sxs-lookup"><span data-stu-id="49842-244">#81</span></span>](https://github.com/Azure/azure-documentdb-dotnet/issues/81)

### <a name="a-name151151"></a><span data-ttu-id="49842-245"><a name="1.5.1"/>1.5.1</span><span class="sxs-lookup"><span data-stu-id="49842-245"><a name="1.5.1"/>1.5.1</span></span>
* <span data-ttu-id="49842-246">**[고정]**  선택 hello 마지막 식 hello 없으면 LINQ 공급자 프로젝션이 없습니다 것으로 간주 하 고 선택 생성 * 잘못 합니다.</span><span class="sxs-lookup"><span data-stu-id="49842-246">**[Fixed]** If Select is not hello last expression hello LINQ Provider assumed no projection and produced SELECT * incorrectly.</span></span>  [<span data-ttu-id="49842-247">#58</span><span class="sxs-lookup"><span data-stu-id="49842-247">#58</span></span>](https://github.com/Azure/azure-documentdb-dotnet/issues/58)

### <a name="a-name150150"></a><span data-ttu-id="49842-248"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="49842-248"><a name="1.5.0"/>1.5.0</span></span>
* <span data-ttu-id="49842-249">Upsert가 구현되고 UpsertXXXAsync 메서드가 추가됨</span><span class="sxs-lookup"><span data-stu-id="49842-249">Implemented Upsert, Added UpsertXXXAsync methods</span></span>
* <span data-ttu-id="49842-250">모든 요청에 대한 성능 향상</span><span class="sxs-lookup"><span data-stu-id="49842-250">Performance improvements for all requests</span></span>
* <span data-ttu-id="49842-251">문자열의 조건부, 병합 및 CompareTo 메서드에 대한 LINQ 공급자 지원</span><span class="sxs-lookup"><span data-stu-id="49842-251">LINQ Provider support for conditional, coalesce, and CompareTo methods for strings</span></span>
* <span data-ttu-id="49842-252">**[고정]**  LINQ 공급자 구현 포함 목록 toogenerate에서 메서드 a b l e 및 배열에서와 동일한 SQL hello--></span><span class="sxs-lookup"><span data-stu-id="49842-252">**[Fixed]** LINQ provider --> Implement Contains method on List toogenerate hello same SQL as on IEnumerable and Array</span></span>
* <span data-ttu-id="49842-253">**[고정]**  BackoffRetryUtility 사용 하 여 다시 시도 새로 만드는 대신 다시 동일한 HttpRequestMessage hello</span><span class="sxs-lookup"><span data-stu-id="49842-253">**[Fixed]** BackoffRetryUtility uses hello same HttpRequestMessage again instead of creating a new one on retry</span></span>
* <span data-ttu-id="49842-254">**[사용되지 않음]** UriFactory.CreateCollection --> 이제 UriFactory.CreateDocumentCollection을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="49842-254">**[Obsolete]** UriFactory.CreateCollection --> should now use UriFactory.CreateDocumentCollection</span></span>

### <a name="a-name141141"></a><span data-ttu-id="49842-255"><a name="1.4.1"/>1.4.1</span><span class="sxs-lookup"><span data-stu-id="49842-255"><a name="1.4.1"/>1.4.1</span></span>
* <span data-ttu-id="49842-256">**[수정됨]** nl-NL 등과 같은 en 이외의 문화권 정보를 사용할 때의 지역화 문제</span><span class="sxs-lookup"><span data-stu-id="49842-256">**[Fixed]** Localization issues when using non en culture info such as nl-NL, etc.</span></span> 

### <a name="a-name140140"></a><span data-ttu-id="49842-257"><a name="1.4.0"/>1.4.0</span><span class="sxs-lookup"><span data-stu-id="49842-257"><a name="1.4.0"/>1.4.0</span></span>
* <span data-ttu-id="49842-258">ID 기반 라우팅 추가</span><span class="sxs-lookup"><span data-stu-id="49842-258">Added ID-based routing</span></span>
  * <span data-ttu-id="49842-259">ID 기반 리소스 링크를 작성 하는 새 UriFactory 도우미 tooassist</span><span class="sxs-lookup"><span data-stu-id="49842-259">New UriFactory helper tooassist with constructing ID-based resource links</span></span>
  * <span data-ttu-id="49842-260">URI에 DocumentClient tootake에 새 오버 로드</span><span class="sxs-lookup"><span data-stu-id="49842-260">New overloads on DocumentClient tootake in URI</span></span>
* <span data-ttu-id="49842-261">LINQ에서 지리 공간에 대한 IsValid() 및 IsValidDetailed() 추가됨</span><span class="sxs-lookup"><span data-stu-id="49842-261">Added IsValid() and IsValidDetailed() in LINQ for geospatial</span></span>
* <span data-ttu-id="49842-262">LINQ 공급자 지원이 향상되었습니다.</span><span class="sxs-lookup"><span data-stu-id="49842-262">LINQ Provider support enhanced:</span></span>
  * <span data-ttu-id="49842-263">**수학** - Abs, Acos, Asin, Atan, Ceiling, Cos, Exp, Floor, Log, Log10, Pow, Round, Sign, Sin, Sqrt, Tan, Truncate</span><span class="sxs-lookup"><span data-stu-id="49842-263">**Math** - Abs, Acos, Asin, Atan, Ceiling, Cos, Exp, Floor, Log, Log10, Pow, Round, Sign, Sin, Sqrt, Tan, Truncate</span></span>
  * <span data-ttu-id="49842-264">**문자열** - Concat, Contains, EndsWith, IndexOf, Count, ToLower, TrimStart, Replace, Reverse, TrimEnd, StartsWith, SubString, ToUpper</span><span class="sxs-lookup"><span data-stu-id="49842-264">**String** - Concat, Contains, EndsWith, IndexOf, Count, ToLower, TrimStart, Replace, Reverse, TrimEnd, StartsWith, SubString, ToUpper</span></span>
  * <span data-ttu-id="49842-265">**배열** - Concat, Contains, Count</span><span class="sxs-lookup"><span data-stu-id="49842-265">**Array** - Concat, Contains, Count</span></span>
  * <span data-ttu-id="49842-266">**IN** 연산자</span><span class="sxs-lookup"><span data-stu-id="49842-266">**IN** operator</span></span>

### <a name="a-name130130"></a><span data-ttu-id="49842-267"><a name="1.3.0"/>1.3.0</span><span class="sxs-lookup"><span data-stu-id="49842-267"><a name="1.3.0"/>1.3.0</span></span>
* <span data-ttu-id="49842-268">인덱싱 정책 수정 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="49842-268">Added support for modifying indexing policies.</span></span>
  * <span data-ttu-id="49842-269">DocumentClient의 새로운 ReplaceDocumentCollectionAsync 메서드</span><span class="sxs-lookup"><span data-stu-id="49842-269">New ReplaceDocumentCollectionAsync method in DocumentClient</span></span>
  * <span data-ttu-id="49842-270">인덱스 정책 변경 진행률을 추적하기 위한 ResourceResponse<T>의 새로운 IndexTransformationProgress 속성</span><span class="sxs-lookup"><span data-stu-id="49842-270">New IndexTransformationProgress property in ResourceResponse<T> for tracking percent progress of index policy changes</span></span>
  * <span data-ttu-id="49842-271">이제 DocumentCollection.IndexingPolicy를 변경할 수 있음</span><span class="sxs-lookup"><span data-stu-id="49842-271">DocumentCollection.IndexingPolicy is now mutable</span></span>
* <span data-ttu-id="49842-272">공간 인덱싱 및 쿼리 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="49842-272">Added support for spatial indexing and query.</span></span>
  * <span data-ttu-id="49842-273">점 및 다각형과 같은 공간 형식을 직렬화/역직렬화하기 위한 새로운 Microsoft.Azure.Documents.Spatial 네임스페이스</span><span class="sxs-lookup"><span data-stu-id="49842-273">New Microsoft.Azure.Documents.Spatial namespace for serializing/deserializing spatial types like Point and Polygon</span></span>
  * <span data-ttu-id="49842-274">Cosmos DB에 저장된 GeoJSON 데이터를 인덱싱하기 위한 새로운 SpatialIndex 클래스</span><span class="sxs-lookup"><span data-stu-id="49842-274">New SpatialIndex class for indexing GeoJSON data stored in Cosmos DB</span></span>
* <span data-ttu-id="49842-275">**[수정됨]** LINQ 식 [#38](https://github.com/Azure/azure-documentdb-net/issues/38)에서 생성된 잘못된 SQL 쿼리.</span><span class="sxs-lookup"><span data-stu-id="49842-275">**[Fixed]** Incorrect SQL query generated from a LINQ expression [#38](https://github.com/Azure/azure-documentdb-net/issues/38).</span></span>

### <a name="a-name120120"></a><span data-ttu-id="49842-276"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="49842-276"><a name="1.2.0"/>1.2.0</span></span>
* <span data-ttu-id="49842-277">Newtonsoft.Json v5.0.7에 대한 종속성이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="49842-277">Added a dependency on Newtonsoft.Json v5.0.7.</span></span>
* <span data-ttu-id="49842-278">Order By toosupport 변경 했습니다.</span><span class="sxs-lookup"><span data-stu-id="49842-278">Made changes toosupport Order By:</span></span>
  
  * <span data-ttu-id="49842-279">OrderBy() 또는 OrderByDescending()에 대한 LINQ 공급자 지원</span><span class="sxs-lookup"><span data-stu-id="49842-279">LINQ provider support for OrderBy() or OrderByDescending()</span></span>
  * <span data-ttu-id="49842-280">Order By IndexingPolicy toosupport</span><span class="sxs-lookup"><span data-stu-id="49842-280">IndexingPolicy toosupport Order By</span></span> 
    
    <span data-ttu-id="49842-281">**가능한 주요 변경 내용**</span><span class="sxs-lookup"><span data-stu-id="49842-281">**Possible breaking change**</span></span> 
    
    <span data-ttu-id="49842-282">사용자 지정 인덱싱 정책 사용 하 여 해당 프로 비전 컬렉션 기존 코드가 있는 경우 기존 프로그램 코드 요구 toobe toosupport hello 새 IndexingPolicy 클래스 업데이트.</span><span class="sxs-lookup"><span data-stu-id="49842-282">If you have existing code that provisions collections with a custom indexing policy, then your existing code needs toobe updated toosupport hello new IndexingPolicy class.</span></span> <span data-ttu-id="49842-283">사용자 지정 인덱싱 정책이 없다면 이 변경 사항은 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="49842-283">If you have no custom indexing policy, then this change does not affect you.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="49842-284"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="49842-284"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="49842-285">Hello 새 HashPartitionResolver 및 RangePartitionResolver 클래스와 IPartitionResolver hello를 사용 하 여 데이터를 분할 하는 것에 대 한 지원이 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="49842-285">Added support for partitioning data by using hello new HashPartitionResolver and RangePartitionResolver classes and hello IPartitionResolver.</span></span>
* <span data-ttu-id="49842-286">DataContract serialization이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="49842-286">Added DataContract serialization.</span></span>
* <span data-ttu-id="49842-287">LINQ 공급자의 GUID 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="49842-287">Added GUID support in LINQ provider.</span></span>
* <span data-ttu-id="49842-288">LINQ의 UDF 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="49842-288">Added UDF support in LINQ.</span></span>

### <a name="a-name100100"></a><span data-ttu-id="49842-289"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="49842-289"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="49842-290">GA SDK</span><span class="sxs-lookup"><span data-stu-id="49842-290">GA SDK</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="49842-291">릴리스 및 사용 중지 날짜</span><span class="sxs-lookup"><span data-stu-id="49842-291">Release & Retirement dates</span></span>
<span data-ttu-id="49842-292">Microsoft는 알림 최소 **12 개월** 순서 toosmooth hello 전환 tooa 지원/최신 버전의 SDK를 사용 중지 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="49842-292">Microsoft provides notification at least **12 months** in advance of retiring an SDK in order toosmooth hello transition tooa newer/supported version.</span></span>

<span data-ttu-id="49842-293">새로운 기능 및 기능 및 최적화는 toohello 현재만 추가 SDK, 따라서 것이 좋습니다 하면 항상 업그레이드 toohello 최신 SDK 버전 가능한 한 빨리 합니다.</span><span class="sxs-lookup"><span data-stu-id="49842-293">New features and functionality and optimizations are only added toohello current SDK, as such it is recommended that you always upgrade toohello latest SDK version as early as possible.</span></span> 

<span data-ttu-id="49842-294">모든 요청 tooAzure 사용 중지 된 SDK를 사용 하 여 Cosmos DB hello 서비스에서 거부 됩니다.</span><span class="sxs-lookup"><span data-stu-id="49842-294">Any requests tooAzure Cosmos DB using a retired SDK are rejected by hello service.</span></span>

<br/>

| <span data-ttu-id="49842-295">버전</span><span class="sxs-lookup"><span data-stu-id="49842-295">Version</span></span> | <span data-ttu-id="49842-296">릴리스 날짜</span><span class="sxs-lookup"><span data-stu-id="49842-296">Release Date</span></span> | <span data-ttu-id="49842-297">사용 중지 날짜</span><span class="sxs-lookup"><span data-stu-id="49842-297">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="49842-298">1.17.0</span><span class="sxs-lookup"><span data-stu-id="49842-298">1.17.0</span></span>](#1.17.0) |<span data-ttu-id="49842-299">2017년 8월 10일</span><span class="sxs-lookup"><span data-stu-id="49842-299">August 10, 2017</span></span> |--- |
| [<span data-ttu-id="49842-300">1.16.1</span><span class="sxs-lookup"><span data-stu-id="49842-300">1.16.1</span></span>](#1.16.1) |<span data-ttu-id="49842-301">2017년 8월 7일</span><span class="sxs-lookup"><span data-stu-id="49842-301">August 07, 2017</span></span> |--- |
| [<span data-ttu-id="49842-302">1.16.0</span><span class="sxs-lookup"><span data-stu-id="49842-302">1.16.0</span></span>](#1.16.0) |<span data-ttu-id="49842-303">2017년 8월 2일</span><span class="sxs-lookup"><span data-stu-id="49842-303">August 02, 2017</span></span> |--- |
| [<span data-ttu-id="49842-304">1.15.0</span><span class="sxs-lookup"><span data-stu-id="49842-304">1.15.0</span></span>](#1.15.0) |<span data-ttu-id="49842-305">2017년 6월 30일</span><span class="sxs-lookup"><span data-stu-id="49842-305">June 30, 2017</span></span> |--- |
| [<span data-ttu-id="49842-306">1.14.1</span><span class="sxs-lookup"><span data-stu-id="49842-306">1.14.1</span></span>](#1.14.1) |<span data-ttu-id="49842-307">2017년 5월 23일</span><span class="sxs-lookup"><span data-stu-id="49842-307">May 23, 2017</span></span> |--- |
| [<span data-ttu-id="49842-308">1.14.0</span><span class="sxs-lookup"><span data-stu-id="49842-308">1.14.0</span></span>](#1.14.0) |<span data-ttu-id="49842-309">2017년 5월 10일</span><span class="sxs-lookup"><span data-stu-id="49842-309">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="49842-310">1.13.4</span><span class="sxs-lookup"><span data-stu-id="49842-310">1.13.4</span></span>](#1.13.4) |<span data-ttu-id="49842-311">2017년 5월 09일</span><span class="sxs-lookup"><span data-stu-id="49842-311">May 09, 2017</span></span> |--- |
| [<span data-ttu-id="49842-312">1.13.3</span><span class="sxs-lookup"><span data-stu-id="49842-312">1.13.3</span></span>](#1.13.3) |<span data-ttu-id="49842-313">2017년 5월 06일</span><span class="sxs-lookup"><span data-stu-id="49842-313">May 06, 2017</span></span> |--- |
| [<span data-ttu-id="49842-314">1.13.2</span><span class="sxs-lookup"><span data-stu-id="49842-314">1.13.2</span></span>](#1.13.2) |<span data-ttu-id="49842-315">2017년 4월 19일</span><span class="sxs-lookup"><span data-stu-id="49842-315">April 19, 2017</span></span> |--- |
| [<span data-ttu-id="49842-316">1.13.1</span><span class="sxs-lookup"><span data-stu-id="49842-316">1.13.1</span></span>](#1.13.1) |<span data-ttu-id="49842-317">2017년 3월 29일</span><span class="sxs-lookup"><span data-stu-id="49842-317">March 29, 2017</span></span> |--- |
| [<span data-ttu-id="49842-318">1.13.0</span><span class="sxs-lookup"><span data-stu-id="49842-318">1.13.0</span></span>](#1.13.0) |<span data-ttu-id="49842-319">2017년 3월 24일</span><span class="sxs-lookup"><span data-stu-id="49842-319">March 24, 2017</span></span> |--- |
| [<span data-ttu-id="49842-320">1.12.2</span><span class="sxs-lookup"><span data-stu-id="49842-320">1.12.2</span></span>](#1.12.2) |<span data-ttu-id="49842-321">2017년 3월 20일</span><span class="sxs-lookup"><span data-stu-id="49842-321">March 20, 2017</span></span> |--- |
| [<span data-ttu-id="49842-322">1.12.1</span><span class="sxs-lookup"><span data-stu-id="49842-322">1.12.1</span></span>](#1.12.1) |<span data-ttu-id="49842-323">2017년 3월 14일</span><span class="sxs-lookup"><span data-stu-id="49842-323">March 14, 2017</span></span> |--- |
| [<span data-ttu-id="49842-324">1.12.0</span><span class="sxs-lookup"><span data-stu-id="49842-324">1.12.0</span></span>](#1.12.0) |<span data-ttu-id="49842-325">2017년 2월 15일</span><span class="sxs-lookup"><span data-stu-id="49842-325">February 15, 2017</span></span> |--- |
| [<span data-ttu-id="49842-326">1.11.4</span><span class="sxs-lookup"><span data-stu-id="49842-326">1.11.4</span></span>](#1.11.4) |<span data-ttu-id="49842-327">2017년 2월 6일</span><span class="sxs-lookup"><span data-stu-id="49842-327">February 06, 2017</span></span> |--- |
| [<span data-ttu-id="49842-328">1.11.3</span><span class="sxs-lookup"><span data-stu-id="49842-328">1.11.3</span></span>](#1.11.3) |<span data-ttu-id="49842-329">2017년 1월 26일</span><span class="sxs-lookup"><span data-stu-id="49842-329">January 26, 2017</span></span> |--- |
| [<span data-ttu-id="49842-330">1.11.1</span><span class="sxs-lookup"><span data-stu-id="49842-330">1.11.1</span></span>](#1.11.1) |<span data-ttu-id="49842-331">2016년 12월 21일</span><span class="sxs-lookup"><span data-stu-id="49842-331">December 21, 2016</span></span> |--- |
| [<span data-ttu-id="49842-332">1.11.0</span><span class="sxs-lookup"><span data-stu-id="49842-332">1.11.0</span></span>](#1.11.0) |<span data-ttu-id="49842-333">2016년 12월 8일</span><span class="sxs-lookup"><span data-stu-id="49842-333">December 08, 2016</span></span> |--- |
| [<span data-ttu-id="49842-334">1.10.0</span><span class="sxs-lookup"><span data-stu-id="49842-334">1.10.0</span></span>](#1.10.0) |<span data-ttu-id="49842-335">2016년 9월 27일</span><span class="sxs-lookup"><span data-stu-id="49842-335">September 27, 2016</span></span> |--- |
| [<span data-ttu-id="49842-336">1.9.5</span><span class="sxs-lookup"><span data-stu-id="49842-336">1.9.5</span></span>](#1.9.5) |<span data-ttu-id="49842-337">2016년 9월 1일</span><span class="sxs-lookup"><span data-stu-id="49842-337">September 01, 2016</span></span> |--- |
| [<span data-ttu-id="49842-338">1.9.4</span><span class="sxs-lookup"><span data-stu-id="49842-338">1.9.4</span></span>](#1.9.4) |<span data-ttu-id="49842-339">2016년 8월 24일</span><span class="sxs-lookup"><span data-stu-id="49842-339">August 24, 2016</span></span> |--- |
| [<span data-ttu-id="49842-340">1.9.3</span><span class="sxs-lookup"><span data-stu-id="49842-340">1.9.3</span></span>](#1.9.3) |<span data-ttu-id="49842-341">2016년 8월 15일</span><span class="sxs-lookup"><span data-stu-id="49842-341">August 15, 2016</span></span> |--- |
| [<span data-ttu-id="49842-342">1.9.2</span><span class="sxs-lookup"><span data-stu-id="49842-342">1.9.2</span></span>](#1.9.2) |<span data-ttu-id="49842-343">2016년 7월 23일</span><span class="sxs-lookup"><span data-stu-id="49842-343">July 23, 2016</span></span> |--- |
| [<span data-ttu-id="49842-344">1.8.0</span><span class="sxs-lookup"><span data-stu-id="49842-344">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="49842-345">2016년 6월 14일</span><span class="sxs-lookup"><span data-stu-id="49842-345">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="49842-346">1.7.1</span><span class="sxs-lookup"><span data-stu-id="49842-346">1.7.1</span></span>](#1.7.1) |<span data-ttu-id="49842-347">2016년 5월 6일</span><span class="sxs-lookup"><span data-stu-id="49842-347">May 06, 2016</span></span> |--- |
| [<span data-ttu-id="49842-348">1.7.0</span><span class="sxs-lookup"><span data-stu-id="49842-348">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="49842-349">2016년 4월 26일</span><span class="sxs-lookup"><span data-stu-id="49842-349">April 26, 2016</span></span> |--- |
| [<span data-ttu-id="49842-350">1.6.3</span><span class="sxs-lookup"><span data-stu-id="49842-350">1.6.3</span></span>](#1.6.3) |<span data-ttu-id="49842-351">2016년 4월 8일</span><span class="sxs-lookup"><span data-stu-id="49842-351">April 08, 2016</span></span> |--- |
| [<span data-ttu-id="49842-352">1.6.2</span><span class="sxs-lookup"><span data-stu-id="49842-352">1.6.2</span></span>](#1.6.2) |<span data-ttu-id="49842-353">2016년 3월 29일</span><span class="sxs-lookup"><span data-stu-id="49842-353">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="49842-354">1.5.3</span><span class="sxs-lookup"><span data-stu-id="49842-354">1.5.3</span></span>](#1.5.3) |<span data-ttu-id="49842-355">2016년 2월 19일</span><span class="sxs-lookup"><span data-stu-id="49842-355">February 19, 2016</span></span> |--- |
| [<span data-ttu-id="49842-356">1.5.2</span><span class="sxs-lookup"><span data-stu-id="49842-356">1.5.2</span></span>](#1.5.2) |<span data-ttu-id="49842-357">2015년 12월 14일</span><span class="sxs-lookup"><span data-stu-id="49842-357">December 14, 2015</span></span> |--- |
| [<span data-ttu-id="49842-358">1.5.1</span><span class="sxs-lookup"><span data-stu-id="49842-358">1.5.1</span></span>](#1.5.1) |<span data-ttu-id="49842-359">2015년 11월 23일</span><span class="sxs-lookup"><span data-stu-id="49842-359">November 23, 2015</span></span> |--- |
| [<span data-ttu-id="49842-360">1.5.0</span><span class="sxs-lookup"><span data-stu-id="49842-360">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="49842-361">2015년 10월 5일</span><span class="sxs-lookup"><span data-stu-id="49842-361">October 05, 2015</span></span> |--- |
| [<span data-ttu-id="49842-362">1.4.1</span><span class="sxs-lookup"><span data-stu-id="49842-362">1.4.1</span></span>](#1.4.1) |<span data-ttu-id="49842-363">2015년 8월 25일</span><span class="sxs-lookup"><span data-stu-id="49842-363">August 25, 2015</span></span> |--- |
| [<span data-ttu-id="49842-364">1.4.0</span><span class="sxs-lookup"><span data-stu-id="49842-364">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="49842-365">2015년 8월 13일</span><span class="sxs-lookup"><span data-stu-id="49842-365">August 13, 2015</span></span> |--- |
| [<span data-ttu-id="49842-366">1.3.0</span><span class="sxs-lookup"><span data-stu-id="49842-366">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="49842-367">2015년 8월 5일</span><span class="sxs-lookup"><span data-stu-id="49842-367">August 05, 2015</span></span> |--- |
| [<span data-ttu-id="49842-368">1.2.0</span><span class="sxs-lookup"><span data-stu-id="49842-368">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="49842-369">2015년 7월 6일</span><span class="sxs-lookup"><span data-stu-id="49842-369">July 06, 2015</span></span> |--- |
| [<span data-ttu-id="49842-370">1.1.0</span><span class="sxs-lookup"><span data-stu-id="49842-370">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="49842-371">2015년 4월 30일</span><span class="sxs-lookup"><span data-stu-id="49842-371">April 30, 2015</span></span> |--- |
| [<span data-ttu-id="49842-372">1.0.0</span><span class="sxs-lookup"><span data-stu-id="49842-372">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="49842-373">2015년 4월 8일</span><span class="sxs-lookup"><span data-stu-id="49842-373">April 08, 2015</span></span> |--- |


## <a name="faq"></a><span data-ttu-id="49842-374">FAQ</span><span class="sxs-lookup"><span data-stu-id="49842-374">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="49842-375">참고 항목</span><span class="sxs-lookup"><span data-stu-id="49842-375">See also</span></span>
<span data-ttu-id="49842-376">Cosmos DB에 대해 자세히 toolearn 참조 [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) 서비스 페이지.</span><span class="sxs-lookup"><span data-stu-id="49842-376">toolearn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span> 


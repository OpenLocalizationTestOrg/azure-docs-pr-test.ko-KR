---
title: "Azure Cosmos DB .NET SDK 및 리소스 | Microsoft Docs"
description: "릴리스 날짜, 사용 중지 날짜 및 Azure Cosmos DB .NET SDK의 각 버전 간의 변경 내용을 포함하는 .NET API 및 SDK에 대한 모든 것을 알아봅니다."
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
ms.openlocfilehash: 317792e04244a96cf8e47bc7e4a7f633f7a6d8c3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-net-sdk-download-and-release-notes"></a><span data-ttu-id="fb53c-103">Azure Cosmos DB .NET SDK: 다운로드 및 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="fb53c-103">Azure Cosmos DB .NET SDK: Download and release notes</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fb53c-104">.NET</span><span class="sxs-lookup"><span data-stu-id="fb53c-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="fb53c-105">.NET 변경 피드</span><span class="sxs-lookup"><span data-stu-id="fb53c-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="fb53c-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="fb53c-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="fb53c-107">Node.JS</span><span class="sxs-lookup"><span data-stu-id="fb53c-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="fb53c-108">Java</span><span class="sxs-lookup"><span data-stu-id="fb53c-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="fb53c-109">Python</span><span class="sxs-lookup"><span data-stu-id="fb53c-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="fb53c-110">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="fb53c-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="fb53c-111">REST 리소스 공급자</span><span class="sxs-lookup"><span data-stu-id="fb53c-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="fb53c-112">SQL</span><span class="sxs-lookup"><span data-stu-id="fb53c-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="fb53c-113">**SDK 다운로드**</span><span class="sxs-lookup"><span data-stu-id="fb53c-113">**SDK download**</span></span></td><td>[<span data-ttu-id="fb53c-114">NuGet</span><span class="sxs-lookup"><span data-stu-id="fb53c-114">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/)</td></tr>

<tr><td><span data-ttu-id="fb53c-115">**API 설명서**</span><span class="sxs-lookup"><span data-stu-id="fb53c-115">**API documentation**</span></span></td><td>[<span data-ttu-id="fb53c-116">.NET API 참조 설명서</span><span class="sxs-lookup"><span data-stu-id="fb53c-116">.NET API reference documentation</span></span>](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet)</td></tr>

<tr><td><span data-ttu-id="fb53c-117">**샘플**</span><span class="sxs-lookup"><span data-stu-id="fb53c-117">**Samples**</span></span></td><td>[<span data-ttu-id="fb53c-118">.NET 코드 샘플</span><span class="sxs-lookup"><span data-stu-id="fb53c-118">.NET code samples</span></span>](documentdb-dotnet-samples.md)</td></tr>

<tr><td><span data-ttu-id="fb53c-119">**시작**</span><span class="sxs-lookup"><span data-stu-id="fb53c-119">**Get started**</span></span></td><td>[<span data-ttu-id="fb53c-120">Azure Cosmos DB .NET SDK 시작</span><span class="sxs-lookup"><span data-stu-id="fb53c-120">Get started with the Azure Cosmos DB .NET SDK</span></span>](documentdb-get-started.md)</td></tr>

<tr><td><span data-ttu-id="fb53c-121">**웹앱 자습서**</span><span class="sxs-lookup"><span data-stu-id="fb53c-121">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="fb53c-122">Azure Cosmos DB를 사용한 웹 응용 프로그램 개발</span><span class="sxs-lookup"><span data-stu-id="fb53c-122">Web application development with Azure Cosmos DB</span></span>](documentdb-dotnet-application.md)</td></tr>

<tr><td><span data-ttu-id="fb53c-123">**현재 지원되는 프레임워크**</span><span class="sxs-lookup"><span data-stu-id="fb53c-123">**Current supported framework**</span></span></td><td>[<span data-ttu-id="fb53c-124">Microsoft .NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="fb53c-124">Microsoft .NET Framework 4.5</span></span>](https://www.microsoft.com/download/details.aspx?id=30653)</td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="fb53c-125">릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="fb53c-125">Release notes</span></span>

### <a name="a-name11701170"></a><span data-ttu-id="fb53c-126"><a name="1.17.0"/>1.17.0</span><span class="sxs-lookup"><span data-stu-id="fb53c-126"><a name="1.17.0"/>1.17.0</span></span> 

* <span data-ttu-id="fb53c-127">특정 파티션 키 범위 값으로 쿼리 결과의 범위를 지정하기 위해 PartitionKeyRangeId에 대한 지원이 FeedOption으로 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-127">Added support for PartitionKeyRangeId as a FeedOption for scoping query results to a specific partition key range value.</span></span> 
* <span data-ttu-id="fb53c-128">해당 시간 이후에 변경 검색을 시작할 수 있도록 StartTime에 대한 지원이 ChangeFeedOption으로 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-128">Added support for StartTime as a ChangeFeedOption to start looking for the changes after that time.</span></span>

### <a name="a-name11611161"></a><span data-ttu-id="fb53c-129"><a name="1.16.1"/>1.16.1</span><span class="sxs-lookup"><span data-stu-id="fb53c-129"><a name="1.16.1"/>1.16.1</span></span>
* <span data-ttu-id="fb53c-130">스택 오버플로 예외를 일으킬 수 있는 JsonSerializable 클래스의 문제가 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-130">Fixed an issue in the JsonSerializable class that may cause a stack overflow exception.</span></span>

### <a name="a-name11601160"></a><span data-ttu-id="fb53c-131"><a name="1.16.0"/>1.16.0</span><span class="sxs-lookup"><span data-stu-id="fb53c-131"><a name="1.16.0"/>1.16.0</span></span>
*   <span data-ttu-id="fb53c-132">JsonSerializerSettings가 DocumentClient 생성자의 선택적 매개 변수로 도입된 것으로 인해 응용 프로그램을 다시 컴파일해야 하는 문제가 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-132">Fixed an issue that required recompiling of the application due to the introduction of JsonSerializerSettings as an optional parameter in the DocumentClient constructor.</span></span>
* <span data-ttu-id="fb53c-133">JsonSerializerSettings 매개 변수 전달 시 ConnectionPolicy 및 ConsistencyLevel 매개 변수의 기본값을 허용하도록 마지막 매개 변수로 JsonSerializerSettings가 필요한 DocumentClient 생성자가 더 이상 사용되지 않는 것으로 표시되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-133">Marked the DocumentClient constructor obsolete that required JsonSerializerSettings as the last parameter to allow for default values of ConnectionPolicy and ConsistencyLevel parameters when passing in JsonSerializerSettings parameter.</span></span>

### <a name="a-name11501150"></a><span data-ttu-id="fb53c-134"><a name="1.15.0"/>1.15.0</span><span class="sxs-lookup"><span data-stu-id="fb53c-134"><a name="1.15.0"/>1.15.0</span></span>
*   <span data-ttu-id="fb53c-135">[DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet)를 인스턴스화하는 동안 사용자 지정 JsonSerializerSettings를 지정하기 위한 지원을 추가하였습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-135">Added support for specifying custom JsonSerializerSettings while instantiating [DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet).</span></span>

### <a name="a-name11411141"></a><span data-ttu-id="fb53c-136"><a name="1.14.1"/>1.14.1</span><span class="sxs-lookup"><span data-stu-id="fb53c-136"><a name="1.14.1"/>1.14.1</span></span>
*   <span data-ttu-id="fb53c-137">SSE4 명령을 지원하지 않고 Azure Cosmos DB DocumentDB API 쿼리를 실행할 때 SEHException을 throw하는 x64 컴퓨터에 영향을 준 문제가 해결되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-137">Fixed an issue that affected x64 machines that don’t support SSE4 instruction and throw an SEHException when running Azure Cosmos DB DocumentDB API queries.</span></span>

### <a name="a-name11401140"></a><span data-ttu-id="fb53c-138"><a name="1.14.0"/>1.14.0</span><span class="sxs-lookup"><span data-stu-id="fb53c-138"><a name="1.14.0"/>1.14.0</span></span>
*   <span data-ttu-id="fb53c-139">ConsistentPrefix라는 새로운 일관성 수준에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-139">Added support for a new consistency level called ConsistentPrefix.</span></span>
*   <span data-ttu-id="fb53c-140">개별 파티션의 쿼리 메트릭에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-140">Added support for query metrics for individual partitions.</span></span>
*   <span data-ttu-id="fb53c-141">쿼리의 연속 토큰 크기 제한에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-141">Added support for limiting the size of the continuation token for queries.</span></span>
*   <span data-ttu-id="fb53c-142">실패한 요청의 자세한 추적에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-142">Added support for more detailed tracing for failed requests.</span></span>
*   <span data-ttu-id="fb53c-143">SDK의 성능이 약간 향상되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-143">Made some performance improvements in the SDK.</span></span>

### <a name="a-name11341134"></a><span data-ttu-id="fb53c-144"><a name="1.13.4"/>1.13.4</span><span class="sxs-lookup"><span data-stu-id="fb53c-144"><a name="1.13.4"/>1.13.4</span></span>
* <span data-ttu-id="fb53c-145">기능적으로 1.13.3과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-145">Functionally same as 1.13.3.</span></span> <span data-ttu-id="fb53c-146">내부적으로 약간 변경되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-146">Made some internal changes.</span></span>

### <a name="a-name11331133"></a><span data-ttu-id="fb53c-147"><a name="1.13.3"/>1.13.3</span><span class="sxs-lookup"><span data-stu-id="fb53c-147"><a name="1.13.3"/>1.13.3</span></span>
* <span data-ttu-id="fb53c-148">기능적으로 1.13.2와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-148">Functionally same as 1.13.2.</span></span> <span data-ttu-id="fb53c-149">내부적으로 약간 변경되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-149">Made some internal changes.</span></span>

### <a name="a-name11321132"></a><span data-ttu-id="fb53c-150"><a name="1.13.2"/>1.13.2</span><span class="sxs-lookup"><span data-stu-id="fb53c-150"><a name="1.13.2"/>1.13.2</span></span>
* <span data-ttu-id="fb53c-151">집계 쿼리에 대한 FeedOptions에 제공된 PartitionKey 값을 무시하던 문제를 해결했습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-151">Fixed an issue that ignored the PartitionKey value provided in FeedOptions for aggregate queries.</span></span>
* <span data-ttu-id="fb53c-152">플라이트 중간의 파티션 간 Order By 쿼리를 실행하는 동안 파티션 관리의 투명한 처리 문제를 해결했습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-152">Fixed an issue in transparent handling of partition management during mid-flight cross-partition Order By query execution.</span></span>

### <a name="a-name11311131"></a><span data-ttu-id="fb53c-153"><a name="1.13.1"/>1.13.1</span><span class="sxs-lookup"><span data-stu-id="fb53c-153"><a name="1.13.1"/>1.13.1</span></span>
* <span data-ttu-id="fb53c-154">ASP.NET 컨텍스트 내에서 사용할 경우 일부 비동기 API에서 교착 상태를 일으키는 문제를 해결했습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-154">Fixed an issue which caused deadlocks in some of the async APIs when used inside ASP.NET context.</span></span>

### <a name="a-name11301130"></a><span data-ttu-id="fb53c-155"><a name="1.13.0"/>1.13.0</span><span class="sxs-lookup"><span data-stu-id="fb53c-155"><a name="1.13.0"/>1.13.0</span></span>
* <span data-ttu-id="fb53c-156">특정 조건에서 자동 장애 조치(Failover)를 수행하도록 SDK를 좀 더 탄력적으로 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-156">Fixes to make SDK more resilient to automatic failover under certain conditions.</span></span>

### <a name="a-name11221122"></a><span data-ttu-id="fb53c-157"><a name="1.12.2"/>1.12.2</span><span class="sxs-lookup"><span data-stu-id="fb53c-157"><a name="1.12.2"/>1.12.2</span></span>
* <span data-ttu-id="fb53c-158">문제를 수정하는 경우 때때로 WebException이 발생합니다. 원격 이름을 확인할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-158">Fix for an issue that occasionally causes a WebException: The remote name could not be resolved.</span></span>
* <span data-ttu-id="fb53c-159">ReadDocumentAsync API에 새 오버로드를 추가하여 형식화된 문서를 직접 읽기 위한 지원을 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-159">Added the support for directly reading a typed document by adding new overloads to ReadDocumentAsync API.</span></span>

### <a name="a-name11211121"></a><span data-ttu-id="fb53c-160"><a name="1.12.1"/>1.12.1</span><span class="sxs-lookup"><span data-stu-id="fb53c-160"><a name="1.12.1"/>1.12.1</span></span>
* <span data-ttu-id="fb53c-161">집계 쿼리(COUNT, MIN, MAX, SUM 및 AVG)에 대한 LINQ 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-161">Added LINQ support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="fb53c-162">이벤트 처리기를 사용하여 발생한 ConnectionPolicy 개체의 메모리 누수 문제를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-162">Fix for a memory leak issue for the ConnectionPolicy object caused by the use of event handler.</span></span>
* <span data-ttu-id="fb53c-163">ETag를 사용할 때 UpsertAttachmentAsync가 작동하지 않는 문제를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-163">Fix for an issue wherein UpsertAttachmentAsync was not working when ETag was used.</span></span>
* <span data-ttu-id="fb53c-164">문자열 필드를 정렬할 때 파티션 간 order-by 쿼리 연속 작업이 작동하지 않는 문제를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-164">Fix for an issue wherein cross partition order-by query continuation was not working when sorting on string field.</span></span>

### <a name="a-name11201120"></a><span data-ttu-id="fb53c-165"><a name="1.12.0"/>1.12.0</span><span class="sxs-lookup"><span data-stu-id="fb53c-165"><a name="1.12.0"/>1.12.0</span></span>
* <span data-ttu-id="fb53c-166">집계 쿼리(COUNT, MIN, MAX, SUM 및 AVG)에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-166">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span> <span data-ttu-id="fb53c-167">[집계 지원](documentdb-sql-query.md#Aggregates)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fb53c-167">See [Aggregation support](documentdb-sql-query.md#Aggregates).</span></span>
* <span data-ttu-id="fb53c-168">분할된 컬렉션에 대한 최소 처리량이 10,100RU/s에서 2500RU/s로 감소됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-168">Lowered minimum throughput on partitioned collections from 10,100 RU/s to 2500 RU/s.</span></span>

### <a name="a-name11141114"></a><span data-ttu-id="fb53c-169"><a name="1.11.4"/>1.11.4</span><span class="sxs-lookup"><span data-stu-id="fb53c-169"><a name="1.11.4"/>1.11.4</span></span>
* <span data-ttu-id="fb53c-170">32비트 호스트 프로세스에서 일부 파티션 간 쿼리가 실패하는 문제를 수정했습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-170">Fix for an issue wherein some of the cross-partition queries were failing in the 32-bit host process.</span></span>
* <span data-ttu-id="fb53c-171">게이트웨이 모드에서 실패한 요청에 대한 토큰으로 세션 컨테이너를 업데이트하지 않는 문제를 수정했습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-171">Fix for an issue wherein the session container was not being updated with the token for failed requests in Gateway mode.</span></span>
* <span data-ttu-id="fb53c-172">경우에 따라 프로젝션에서 UDF 호출을 사용하는 쿼리가 실패하는 문제를 수정했습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-172">Fix for an issue wherein a query with UDF calls in projection was failing in some cases.</span></span>
* <span data-ttu-id="fb53c-173">요청의 읽기 및 쓰기 처리량을 높이기 위해 클라이언트 쪽 성능을 수정했습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-173">Client side performance fixes for increasing the read and write throughput of the requests.</span></span>

### <a name="a-name11131113"></a><span data-ttu-id="fb53c-174"><a name="1.11.3"/>1.11.3</span><span class="sxs-lookup"><span data-stu-id="fb53c-174"><a name="1.11.3"/>1.11.3</span></span>
* <span data-ttu-id="fb53c-175">실패한 요청에 대한 토큰으로 세션 컨테이너를 업데이트하지 않는 문제를 수정했습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-175">Fix for an issue wherein the session container was not being updated with the token for failed requests.</span></span>
* <span data-ttu-id="fb53c-176">32비트 호스트 프로세스에서 작동하도록 SDK에 대한 지원을 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-176">Added support for the SDK to work in a 32-bit host process.</span></span> <span data-ttu-id="fb53c-177">파티션 간 쿼리를 사용하는 경우 향상된 성능을 위해 64비트 호스트를 처리하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-177">Note that if you use cross partition queries, 64-bit host processing is recommended for improved performance.</span></span>
* <span data-ttu-id="fb53c-178">IN 식에 많은 수의 파티션 키 값을 사용하는 쿼리와 관련된 시나리오의 성능이 향상되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-178">Improved performance for scenarios involving queries with a large number of partition key values in an IN expression.</span></span>
* <span data-ttu-id="fb53c-179">PopulateQuotaInfo 요청 옵션을 설정하는 경우 문서 컬렉션 읽기 요청에 대한 ResourceResponse에서 다양한 리소스 할당량 통계가 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-179">Populated various resource quota stats in the ResourceResponse for document collection read requests when PopulateQuotaInfo request option is set.</span></span>

### <a name="a-name11111111"></a><span data-ttu-id="fb53c-180"><a name="1.11.1"/>1.11.1</span><span class="sxs-lookup"><span data-stu-id="fb53c-180"><a name="1.11.1"/>1.11.1</span></span>
* <span data-ttu-id="fb53c-181">1.11.0에 도입된 CreateDocumentCollectionIfNotExistsAsync API 성능이 약간 향상되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-181">Minor performance fix for the CreateDocumentCollectionIfNotExistsAsync API introduced in 1.11.0.</span></span>
* <span data-ttu-id="fb53c-182">높은 수준의 동시 요청이 개입되는 시나리오를 위한 SDK의 성능 픽스입니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-182">Performance fix in the SDK for scenarios that involve high degree of concurrent requests.</span></span>

### <a name="a-name11101110"></a><span data-ttu-id="fb53c-183"><a name="1.11.0"/>1.11.0</span><span class="sxs-lookup"><span data-stu-id="fb53c-183"><a name="1.11.0"/>1.11.0</span></span>
* <span data-ttu-id="fb53c-184">컬렉션 내 문서의 [피드 변경](change-feed.md) 프로세스에 대한 새 클래스 및 메서드 지원</span><span class="sxs-lookup"><span data-stu-id="fb53c-184">Support for new classes and methods to process the [change feed](change-feed.md) of documents within a collection.</span></span>
* <span data-ttu-id="fb53c-185">파티션 간 쿼리 연속 및 파티션 간 쿼리에 대한 일부 성능 향상 지원</span><span class="sxs-lookup"><span data-stu-id="fb53c-185">Support for cross-partition query continuation and some perf improvements for cross-partition queries.</span></span>
* <span data-ttu-id="fb53c-186">CreateDatabaseIfNotExistsAsync 및 CreateDocumentCollectionIfNotExistsAsync 메서드 추가</span><span class="sxs-lookup"><span data-stu-id="fb53c-186">Addition of CreateDatabaseIfNotExistsAsync and CreateDocumentCollectionIfNotExistsAsync methods.</span></span>
* <span data-ttu-id="fb53c-187">시스템 함수에 대한 LINQ 지원: IsDefined, IsNull 및 IsPrimitive</span><span class="sxs-lookup"><span data-stu-id="fb53c-187">LINQ support for system functions: IsDefined, IsNull and IsPrimitive.</span></span>
* <span data-ttu-id="fb53c-188">project.json 도구를 포함한 프로젝트의 NuGet 패키지를 사용할 때 Microsoft.Azure.Documents.ServiceInterop.dll 및 DocumentDB.Spatial.Sql.dll 어셈블리가 자동으로 응용 프로그램의 휴지통에 들어가는 현상 수정</span><span class="sxs-lookup"><span data-stu-id="fb53c-188">Fix for automatic binplacing of Microsoft.Azure.Documents.ServiceInterop.dll and DocumentDB.Spatial.Sql.dll assemblies to application’s bin folder when using the Nuget package with projects that have project.json tooling.</span></span>
* <span data-ttu-id="fb53c-189">시나리오를 디버깅하는 데 도움이 될 수 있는 클라이언트 쪽 ETW 추적 내보내기 지원</span><span class="sxs-lookup"><span data-stu-id="fb53c-189">Support for emitting client side ETW traces which could be helpful in debugging scenarios.</span></span>

### <a name="a-name11001100"></a><span data-ttu-id="fb53c-190"><a name="1.10.0"/>1.10.0</span><span class="sxs-lookup"><span data-stu-id="fb53c-190"><a name="1.10.0"/>1.10.0</span></span>
* <span data-ttu-id="fb53c-191">분할된 컬렉션에 대한 직접 연결 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-191">Added direct connectivity support for partitioned collections.</span></span>
* <span data-ttu-id="fb53c-192">제한된 부실 일관성 수준에 대한 성능이 향상되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-192">Improved performance for the Bounded Staleness consistency level.</span></span>
* <span data-ttu-id="fb53c-193">지역 펜싱 공간 쿼리에 대한 컬렉션 인덱싱 정책을 지정하는 동안 Polygon 및 LineString 데이터 형식이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-193">Added Polygon and LineString DataTypes while specifying collection indexing policy for geo-fencing spatial queries.</span></span>
* <span data-ttu-id="fb53c-194">조건자를 변환하는 동안 StringEnumConverter, IsoDateTimeConverter 및 UnixDateTimeConverter에 대한 LINQ 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-194">Added LINQ support for StringEnumConverter, IsoDateTimeConverter and UnixDateTimeConverter while translating predicates.</span></span>
* <span data-ttu-id="fb53c-195">다양한 SDK 버그가 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-195">Various SDK bug fixes.</span></span>

### <a name="a-name195195"></a><span data-ttu-id="fb53c-196"><a name="1.9.5"/>1.9.5</span><span class="sxs-lookup"><span data-stu-id="fb53c-196"><a name="1.9.5"/>1.9.5</span></span>
* <span data-ttu-id="fb53c-197">입력 세션 토큰에 대해 읽기 세션을 사용할 수 없다는 NotFoundException을 발생시키는 문제를 해결했습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-197">Fixed an issue that caused the following NotFoundException: The read session is not available for the input session token.</span></span> <span data-ttu-id="fb53c-198">이 예외는 지리적으로 분산된 계정의 읽기 영역을 쿼리할 때 가끔 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-198">This exception occurred in some cases when querying for the read-region of a geo-distributed account.</span></span>
* <span data-ttu-id="fb53c-199">응답에서 내부 스트림에 직접 액세스할 수 있도록 하는 ResourceResponse 클래스의 ResponseStream 속성이 노출되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-199">Exposed the ResponseStream property in the ResourceResponse class, which enables direct access to the underlying stream from a response.</span></span>

### <a name="a-name194194"></a><span data-ttu-id="fb53c-200"><a name="1.9.4"/>1.9.4</span><span class="sxs-lookup"><span data-stu-id="fb53c-200"><a name="1.9.4"/>1.9.4</span></span>
* <span data-ttu-id="fb53c-201">ResourceResponse, FeedResponse, StoredProcedureResponse 및 MediaResponse 클래스가 해당하는 공용 인터페이스를 구현하도록 수정되어 테스트 지향 배포(TDD)를 위해 모의 수행할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-201">Modified the ResourceResponse, FeedResponse, StoredProcedureResponse and MediaResponse classes to implement the corresponding public interface so that they can be mocked for test driven deployment (TDD).</span></span>
* <span data-ttu-id="fb53c-202">데이터 직렬화를 위해 사용자 지정 JsonSerializerSettings 개체를 사용할 때 잘못된 파티션 키 헤더가 발생하는 문제가 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-202">Fixed an issue that caused a malformed partition key header when using a custom JsonSerializerSettings object for serializing data.</span></span>

### <a name="a-name193193"></a><span data-ttu-id="fb53c-203"><a name="1.9.3"/>1.9.3</span><span class="sxs-lookup"><span data-stu-id="fb53c-203"><a name="1.9.3"/>1.9.3</span></span>
* <span data-ttu-id="fb53c-204">오래 실행하는 쿼리가 오류와 함께 실패하게 한 문제를 해결했습니다. 인증 토큰은 현재 시간에 올바르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-204">Fixed an issue that caused long running queries to fail with error: Authorization token is not valid at the current time.</span></span>
* <span data-ttu-id="fb53c-205">크로스 파티션 위쪽/order-by 쿼리에서 원래 SqlParameterCollection을 제거하는 문제를 해결했습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-205">Fixed an issue that removed the original SqlParameterCollection from cross partition top/order-by queries.</span></span>

### <a name="a-name192192"></a><span data-ttu-id="fb53c-206"><a name="1.9.2"/>1.9.2</span><span class="sxs-lookup"><span data-stu-id="fb53c-206"><a name="1.9.2"/>1.9.2</span></span>
* <span data-ttu-id="fb53c-207">분할된 컬렉션에 대한 병렬 쿼리에 지원을 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-207">Added support for parallel queries for partitioned collections.</span></span>
* <span data-ttu-id="fb53c-208">분할된 컬렉션에 대한 파티션 간 Order By 및 TOP 쿼리에 대한 지원을 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-208">Added support for cross partition ORDER BY and TOP queries for partitioned collections.</span></span>
* <span data-ttu-id="fb53c-209">Azure Cosmos DB Nuget 패키지에 대한 참조와 함께 Azure Cosmos DB 프로젝트를 참조할 때 필요한 DocumentDB.Spatial.Sql.dll 및 Microsoft.Azure.Documents.ServiceInterop.dll에 대한 누락된 참조를 수정했습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-209">Fixed the missing references to DocumentDB.Spatial.Sql.dll and Microsoft.Azure.Documents.ServiceInterop.dll that are required when referencing an Azure Cosmos DB project with a reference to the Azure Cosmos DB Nuget package.</span></span>
* <span data-ttu-id="fb53c-210">LINQ에서 사용자 정의 함수를 사용할 때 여러 유형의 매개 변수를 사용하도록 기능을 수정했습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-210">Fixed the ability to use parameters of different types when using user-defined functions in LINQ.</span></span> 
* <span data-ttu-id="fb53c-211">쓰기 위치 대신 읽기 위치에 Upsert 호출을 전달하는 전역적으로 복제된 계정에 대한 버그를 수정했습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-211">Fixed a bug for globally replicated accounts where Upsert calls were being directed to read locations instead of write locations.</span></span>
* <span data-ttu-id="fb53c-212">IDocumentClient 인터페이스에 누락된 다음 메서드를 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-212">Added methods to the IDocumentClient interface that were missing:</span></span> 
  * <span data-ttu-id="fb53c-213">mediaStream 및 options를 매개 변수로 사용하는 UpsertAttachmentAsync 메서드</span><span class="sxs-lookup"><span data-stu-id="fb53c-213">UpsertAttachmentAsync method that takes mediaStream and options as parameters</span></span>
  * <span data-ttu-id="fb53c-214">options를 매개 변수로 사용하는 CreateAttachmentAsync 메서드</span><span class="sxs-lookup"><span data-stu-id="fb53c-214">CreateAttachmentAsync method that takes options as a parameter</span></span>
  * <span data-ttu-id="fb53c-215">querySpec을 매개 변수로 사용하는 CreateOfferQuery 메서드</span><span class="sxs-lookup"><span data-stu-id="fb53c-215">CreateOfferQuery method that takes querySpec as a parameter.</span></span>
* <span data-ttu-id="fb53c-216">IDocumentClient 인터페이스에 노출된 공용 클래스를 공개했습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-216">Unsealed public classes that are exposed in the IDocumentClient interface.</span></span>

### <a name="a-name180180"></a><span data-ttu-id="fb53c-217"><a name="1.8.0"/>1.8.0</span><span class="sxs-lookup"><span data-stu-id="fb53c-217"><a name="1.8.0"/>1.8.0</span></span>
* <span data-ttu-id="fb53c-218">다중 지역 데이터베이스 계정에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-218">Added the support for multi-region database accounts.</span></span>
* <span data-ttu-id="fb53c-219">정제된 요청에 대한 재시도 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-219">Added support for retry on throttled requests.</span></span>  <span data-ttu-id="fb53c-220">사용자가 ConnectionPolicy.RetryOptions 속성을 구성하여 재시도 횟수와 최대 대기 시간을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-220">User can customize the number of retries and the max wait time by configuring the ConnectionPolicy.RetryOptions property.</span></span>
* <span data-ttu-id="fb53c-221">모든 DocumentClient 속성 및 메서드의 시그니처를 정의하는 새로운 IDocumentClient 인터페이스가 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-221">Added a new IDocumentClient interface that defines the signatures of all DocumenClient properties and methods.</span></span>  <span data-ttu-id="fb53c-222">이러한 변경의 일환으로 DocumentClient 클래스 자체에서 IQueryable과 IOrderedQueryable을 메서드로 만드는 확장 메서드도 변경되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-222">As part of this change, also changed extension methods that create IQueryable and IOrderedQueryable to methods on the DocumentClient class itself.</span></span>
* <span data-ttu-id="fb53c-223">특정 Azure Cosmos DB 끝점 Uri에 대해 ServicePoint.ConnectionLimit를 설정하는 구성 옵션이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-223">Added configuration option to set the ServicePoint.ConnectionLimit for a given Azure Cosmos DB endpoint Uri.</span></span>  <span data-ttu-id="fb53c-224">ConnectionPolicy.MaxConnectionLimit를 사용하여 기본값(50)을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-224">Use ConnectionPolicy.MaxConnectionLimit to change the default value, which is set to 50.</span></span>
* <span data-ttu-id="fb53c-225">IPartitionResolver와 해당 구현의 사용이 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-225">Deprecated IPartitionResolver and its implementation.</span></span>  <span data-ttu-id="fb53c-226">IPartitionResolver 지원이 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-226">Support for IPartitionResolver is now obsolete.</span></span> <span data-ttu-id="fb53c-227">보다 큰 저장소 및 처리량에는 파티션된 컬렉션을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-227">It's recommended that you use Partitioned Collections for higher storage and throughput.</span></span>

### <a name="a-name171171"></a><span data-ttu-id="fb53c-228"><a name="1.7.1"/>1.7.1</span><span class="sxs-lookup"><span data-stu-id="fb53c-228"><a name="1.7.1"/>1.7.1</span></span>
* <span data-ttu-id="fb53c-229">RequestOptions를 매개 변수로 사용하는 Uri 기반 ExecuteStoredProcedureAsync 메서드에 오버로드가 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-229">Added an overload to Uri based ExecuteStoredProcedureAsync method that takes RequestOptions as a parameter.</span></span>

### <a name="a-name170170"></a><span data-ttu-id="fb53c-230"><a name="1.7.0"/>1.7.0</span><span class="sxs-lookup"><span data-stu-id="fb53c-230"><a name="1.7.0"/>1.7.0</span></span>
* <span data-ttu-id="fb53c-231">문서에 대한 TTL(Time to Live) 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-231">Added time to live (TTL) support for documents.</span></span>

### <a name="a-name163163"></a><span data-ttu-id="fb53c-232"><a name="1.6.3"/>1.6.3</span><span class="sxs-lookup"><span data-stu-id="fb53c-232"><a name="1.6.3"/>1.6.3</span></span>
* <span data-ttu-id="fb53c-233">Azure 클라우드 서비스 솔루션의 일부로 패키징에 대한 .NET SDK의 Nuget 패키징에서 버그가 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-233">Fixed a bug in Nuget packaging of .NET SDK for packaging it as part of an Azure Cloud Service solution.</span></span>

### <a name="a-name162162"></a><span data-ttu-id="fb53c-234"><a name="1.6.2"/>1.6.2</span><span class="sxs-lookup"><span data-stu-id="fb53c-234"><a name="1.6.2"/>1.6.2</span></span>
* <span data-ttu-id="fb53c-235">[분할된 컬렉션](partition-data.md) 및 [사용자 정의 성능 수준](performance-levels.md)이 구현되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-235">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span> 

### <a name="a-name153153"></a><span data-ttu-id="fb53c-236"><a name="1.5.3"/>1.5.3</span><span class="sxs-lookup"><span data-stu-id="fb53c-236"><a name="1.5.3"/>1.5.3</span></span>
* <span data-ttu-id="fb53c-237">**[수정됨]** Azure Cosmos DB 끝점을 쿼리하면 'System.Net.Http.HttpRequestException: 스트림에 콘텐츠를 복사하는 중 오류가 발생했습니다.'가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-237">**[Fixed]** Querying Azure Cosmos DB endpoint throws: 'System.Net.Http.HttpRequestException: Error while copying content to a stream'.</span></span>

### <a name="a-name152152"></a><span data-ttu-id="fb53c-238"><a name="1.5.2"/>1.5.2</span><span class="sxs-lookup"><span data-stu-id="fb53c-238"><a name="1.5.2"/>1.5.2</span></span>
* <span data-ttu-id="fb53c-239">페이징, 조건식 및 범위 비교에 대한 새 연산자를 포함하는 LINQ 지원이 확장되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-239">Expanded LINQ support including new operators for paging, conditional expressions, and range comparison.</span></span>
  * <span data-ttu-id="fb53c-240">LINQ에서 SELECT TOP 동작을 사용하도록 설정하는 Take 연산자</span><span class="sxs-lookup"><span data-stu-id="fb53c-240">Take operator to enable SELECT TOP behavior in LINQ</span></span>
  * <span data-ttu-id="fb53c-241">문자열 범위 비교를 사용하도록 설정하는 CompareTo 연산자</span><span class="sxs-lookup"><span data-stu-id="fb53c-241">CompareTo operator to enable string range comparisons</span></span>
  * <span data-ttu-id="fb53c-242">조건부 (?) 및 병합 연산자 (??)</span><span class="sxs-lookup"><span data-stu-id="fb53c-242">Conditional (?) and coalesce operators (??)</span></span>
* <span data-ttu-id="fb53c-243">**[수정됨]** 모델 프로젝션을 LINQ 쿼리의 Where-In과 결합할 때의 ArgumentOutOfRangeException이 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-243">**[Fixed]** ArgumentOutOfRangeException when combining Model projection with Where-In in a LINQ query.</span></span> [<span data-ttu-id="fb53c-244">#81</span><span class="sxs-lookup"><span data-stu-id="fb53c-244">#81</span></span>](https://github.com/Azure/azure-documentdb-dotnet/issues/81)

### <a name="a-name151151"></a><span data-ttu-id="fb53c-245"><a name="1.5.1"/>1.5.1</span><span class="sxs-lookup"><span data-stu-id="fb53c-245"><a name="1.5.1"/>1.5.1</span></span>
* <span data-ttu-id="fb53c-246">**[수정됨]** Select가 마지막 식이 아니면 LINQ 공급자는 프로젝션이 없다고 가정하고 SELECT *를 잘못 생성했습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-246">**[Fixed]** If Select is not the last expression the LINQ Provider assumed no projection and produced SELECT * incorrectly.</span></span>  [<span data-ttu-id="fb53c-247">#58</span><span class="sxs-lookup"><span data-stu-id="fb53c-247">#58</span></span>](https://github.com/Azure/azure-documentdb-dotnet/issues/58)

### <a name="a-name150150"></a><span data-ttu-id="fb53c-248"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="fb53c-248"><a name="1.5.0"/>1.5.0</span></span>
* <span data-ttu-id="fb53c-249">Upsert가 구현되고 UpsertXXXAsync 메서드가 추가됨</span><span class="sxs-lookup"><span data-stu-id="fb53c-249">Implemented Upsert, Added UpsertXXXAsync methods</span></span>
* <span data-ttu-id="fb53c-250">모든 요청에 대한 성능 향상</span><span class="sxs-lookup"><span data-stu-id="fb53c-250">Performance improvements for all requests</span></span>
* <span data-ttu-id="fb53c-251">문자열의 조건부, 병합 및 CompareTo 메서드에 대한 LINQ 공급자 지원</span><span class="sxs-lookup"><span data-stu-id="fb53c-251">LINQ Provider support for conditional, coalesce, and CompareTo methods for strings</span></span>
* <span data-ttu-id="fb53c-252">**[수정됨]** LINQ 공급자 --> 목록에 Contains 메서드를 구현하여 IEnumerable 및 배열과 동일한 SQL을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-252">**[Fixed]** LINQ provider --> Implement Contains method on List to generate the same SQL as on IEnumerable and Array</span></span>
* <span data-ttu-id="fb53c-253">**[수정됨]** BackoffRetryUtility가 다시 시도할 때 새로 만드는 대신 동일한 HttpRequestMessage를 다시 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-253">**[Fixed]** BackoffRetryUtility uses the same HttpRequestMessage again instead of creating a new one on retry</span></span>
* <span data-ttu-id="fb53c-254">**[사용되지 않음]** UriFactory.CreateCollection --> 이제 UriFactory.CreateDocumentCollection을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-254">**[Obsolete]** UriFactory.CreateCollection --> should now use UriFactory.CreateDocumentCollection</span></span>

### <a name="a-name141141"></a><span data-ttu-id="fb53c-255"><a name="1.4.1"/>1.4.1</span><span class="sxs-lookup"><span data-stu-id="fb53c-255"><a name="1.4.1"/>1.4.1</span></span>
* <span data-ttu-id="fb53c-256">**[수정됨]** nl-NL 등과 같은 en 이외의 문화권 정보를 사용할 때의 지역화 문제</span><span class="sxs-lookup"><span data-stu-id="fb53c-256">**[Fixed]** Localization issues when using non en culture info such as nl-NL, etc.</span></span> 

### <a name="a-name140140"></a><span data-ttu-id="fb53c-257"><a name="1.4.0"/>1.4.0</span><span class="sxs-lookup"><span data-stu-id="fb53c-257"><a name="1.4.0"/>1.4.0</span></span>
* <span data-ttu-id="fb53c-258">ID 기반 라우팅 추가</span><span class="sxs-lookup"><span data-stu-id="fb53c-258">Added ID-based routing</span></span>
  * <span data-ttu-id="fb53c-259">ID 기반 리소스 링크 생성을 지원하기 위한 새 UriFactory 도우미</span><span class="sxs-lookup"><span data-stu-id="fb53c-259">New UriFactory helper to assist with constructing ID-based resource links</span></span>
  * <span data-ttu-id="fb53c-260">URI에서 수행할 DocumentClient의 새 오버로드</span><span class="sxs-lookup"><span data-stu-id="fb53c-260">New overloads on DocumentClient to take in URI</span></span>
* <span data-ttu-id="fb53c-261">LINQ에서 지리 공간에 대한 IsValid() 및 IsValidDetailed() 추가됨</span><span class="sxs-lookup"><span data-stu-id="fb53c-261">Added IsValid() and IsValidDetailed() in LINQ for geospatial</span></span>
* <span data-ttu-id="fb53c-262">LINQ 공급자 지원이 향상되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-262">LINQ Provider support enhanced:</span></span>
  * <span data-ttu-id="fb53c-263">**수학** - Abs, Acos, Asin, Atan, Ceiling, Cos, Exp, Floor, Log, Log10, Pow, Round, Sign, Sin, Sqrt, Tan, Truncate</span><span class="sxs-lookup"><span data-stu-id="fb53c-263">**Math** - Abs, Acos, Asin, Atan, Ceiling, Cos, Exp, Floor, Log, Log10, Pow, Round, Sign, Sin, Sqrt, Tan, Truncate</span></span>
  * <span data-ttu-id="fb53c-264">**문자열** - Concat, Contains, EndsWith, IndexOf, Count, ToLower, TrimStart, Replace, Reverse, TrimEnd, StartsWith, SubString, ToUpper</span><span class="sxs-lookup"><span data-stu-id="fb53c-264">**String** - Concat, Contains, EndsWith, IndexOf, Count, ToLower, TrimStart, Replace, Reverse, TrimEnd, StartsWith, SubString, ToUpper</span></span>
  * <span data-ttu-id="fb53c-265">**배열** - Concat, Contains, Count</span><span class="sxs-lookup"><span data-stu-id="fb53c-265">**Array** - Concat, Contains, Count</span></span>
  * <span data-ttu-id="fb53c-266">**IN** 연산자</span><span class="sxs-lookup"><span data-stu-id="fb53c-266">**IN** operator</span></span>

### <a name="a-name130130"></a><span data-ttu-id="fb53c-267"><a name="1.3.0"/>1.3.0</span><span class="sxs-lookup"><span data-stu-id="fb53c-267"><a name="1.3.0"/>1.3.0</span></span>
* <span data-ttu-id="fb53c-268">인덱싱 정책 수정 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-268">Added support for modifying indexing policies.</span></span>
  * <span data-ttu-id="fb53c-269">DocumentClient의 새로운 ReplaceDocumentCollectionAsync 메서드</span><span class="sxs-lookup"><span data-stu-id="fb53c-269">New ReplaceDocumentCollectionAsync method in DocumentClient</span></span>
  * <span data-ttu-id="fb53c-270">인덱스 정책 변경 진행률을 추적하기 위한 ResourceResponse<T>의 새로운 IndexTransformationProgress 속성</span><span class="sxs-lookup"><span data-stu-id="fb53c-270">New IndexTransformationProgress property in ResourceResponse<T> for tracking percent progress of index policy changes</span></span>
  * <span data-ttu-id="fb53c-271">이제 DocumentCollection.IndexingPolicy를 변경할 수 있음</span><span class="sxs-lookup"><span data-stu-id="fb53c-271">DocumentCollection.IndexingPolicy is now mutable</span></span>
* <span data-ttu-id="fb53c-272">공간 인덱싱 및 쿼리 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-272">Added support for spatial indexing and query.</span></span>
  * <span data-ttu-id="fb53c-273">점 및 다각형과 같은 공간 형식을 직렬화/역직렬화하기 위한 새로운 Microsoft.Azure.Documents.Spatial 네임스페이스</span><span class="sxs-lookup"><span data-stu-id="fb53c-273">New Microsoft.Azure.Documents.Spatial namespace for serializing/deserializing spatial types like Point and Polygon</span></span>
  * <span data-ttu-id="fb53c-274">Cosmos DB에 저장된 GeoJSON 데이터를 인덱싱하기 위한 새로운 SpatialIndex 클래스</span><span class="sxs-lookup"><span data-stu-id="fb53c-274">New SpatialIndex class for indexing GeoJSON data stored in Cosmos DB</span></span>
* <span data-ttu-id="fb53c-275">**[수정됨]** LINQ 식 [#38](https://github.com/Azure/azure-documentdb-net/issues/38)에서 생성된 잘못된 SQL 쿼리.</span><span class="sxs-lookup"><span data-stu-id="fb53c-275">**[Fixed]** Incorrect SQL query generated from a LINQ expression [#38](https://github.com/Azure/azure-documentdb-net/issues/38).</span></span>

### <a name="a-name120120"></a><span data-ttu-id="fb53c-276"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="fb53c-276"><a name="1.2.0"/>1.2.0</span></span>
* <span data-ttu-id="fb53c-277">Newtonsoft.Json v5.0.7에 대한 종속성이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-277">Added a dependency on Newtonsoft.Json v5.0.7.</span></span>
* <span data-ttu-id="fb53c-278">Order By를 지원하기 위한 변경 내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-278">Made changes to support Order By:</span></span>
  
  * <span data-ttu-id="fb53c-279">OrderBy() 또는 OrderByDescending()에 대한 LINQ 공급자 지원</span><span class="sxs-lookup"><span data-stu-id="fb53c-279">LINQ provider support for OrderBy() or OrderByDescending()</span></span>
  * <span data-ttu-id="fb53c-280">Order By를 지원하기 위한 IndexingPolicy</span><span class="sxs-lookup"><span data-stu-id="fb53c-280">IndexingPolicy to support Order By</span></span> 
    
    <span data-ttu-id="fb53c-281">**가능한 주요 변경 내용**</span><span class="sxs-lookup"><span data-stu-id="fb53c-281">**Possible breaking change**</span></span> 
    
    <span data-ttu-id="fb53c-282">사용자 지정 인덱싱 정책을 사용하여 컬렉션을 프로비전하는 기존 코드가 있다면 기존 코드는 새 IndexingPolicy 클래스를 지원하도록 업데이트되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-282">If you have existing code that provisions collections with a custom indexing policy, then your existing code needs to be updated to support the new IndexingPolicy class.</span></span> <span data-ttu-id="fb53c-283">사용자 지정 인덱싱 정책이 없다면 이 변경 사항은 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-283">If you have no custom indexing policy, then this change does not affect you.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="fb53c-284"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="fb53c-284"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="fb53c-285">새로운 HashPartitionResolver 및 RangePartitionResolver 클래스와 IPartitionResolver를 사용한 데이터 분할 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-285">Added support for partitioning data by using the new HashPartitionResolver and RangePartitionResolver classes and the IPartitionResolver.</span></span>
* <span data-ttu-id="fb53c-286">DataContract serialization이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-286">Added DataContract serialization.</span></span>
* <span data-ttu-id="fb53c-287">LINQ 공급자의 GUID 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-287">Added GUID support in LINQ provider.</span></span>
* <span data-ttu-id="fb53c-288">LINQ의 UDF 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-288">Added UDF support in LINQ.</span></span>

### <a name="a-name100100"></a><span data-ttu-id="fb53c-289"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="fb53c-289"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="fb53c-290">GA SDK</span><span class="sxs-lookup"><span data-stu-id="fb53c-290">GA SDK</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="fb53c-291">릴리스 및 사용 중지 날짜</span><span class="sxs-lookup"><span data-stu-id="fb53c-291">Release & Retirement dates</span></span>
<span data-ttu-id="fb53c-292">Microsoft는 최신/지원 버전으로 원활히 전환할 수 있도록 SDK 사용 중지 최소 **12개월** 전에 알림을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-292">Microsoft provides notification at least **12 months** in advance of retiring an SDK in order to smooth the transition to a newer/supported version.</span></span>

<span data-ttu-id="fb53c-293">새로운 기능 및 최적화는 현재 SDK에만 추가되어 있으며, 따라서 항상 최신 SDK 버전으로 가능한 한 빨리 업그레이드할 것을 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-293">New features and functionality and optimizations are only added to the current SDK, as such it is recommended that you always upgrade to the latest SDK version as early as possible.</span></span> 

<span data-ttu-id="fb53c-294">사용 중지된 SDK를 사용하는 Azure Cosmos DB에 대한 요청은 서비스에서 거부됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb53c-294">Any requests to Azure Cosmos DB using a retired SDK are rejected by the service.</span></span>

<br/>

| <span data-ttu-id="fb53c-295">버전</span><span class="sxs-lookup"><span data-stu-id="fb53c-295">Version</span></span> | <span data-ttu-id="fb53c-296">릴리스 날짜</span><span class="sxs-lookup"><span data-stu-id="fb53c-296">Release Date</span></span> | <span data-ttu-id="fb53c-297">사용 중지 날짜</span><span class="sxs-lookup"><span data-stu-id="fb53c-297">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="fb53c-298">1.17.0</span><span class="sxs-lookup"><span data-stu-id="fb53c-298">1.17.0</span></span>](#1.17.0) |<span data-ttu-id="fb53c-299">2017년 8월 10일</span><span class="sxs-lookup"><span data-stu-id="fb53c-299">August 10, 2017</span></span> |--- |
| [<span data-ttu-id="fb53c-300">1.16.1</span><span class="sxs-lookup"><span data-stu-id="fb53c-300">1.16.1</span></span>](#1.16.1) |<span data-ttu-id="fb53c-301">2017년 8월 7일</span><span class="sxs-lookup"><span data-stu-id="fb53c-301">August 07, 2017</span></span> |--- |
| [<span data-ttu-id="fb53c-302">1.16.0</span><span class="sxs-lookup"><span data-stu-id="fb53c-302">1.16.0</span></span>](#1.16.0) |<span data-ttu-id="fb53c-303">2017년 8월 2일</span><span class="sxs-lookup"><span data-stu-id="fb53c-303">August 02, 2017</span></span> |--- |
| [<span data-ttu-id="fb53c-304">1.15.0</span><span class="sxs-lookup"><span data-stu-id="fb53c-304">1.15.0</span></span>](#1.15.0) |<span data-ttu-id="fb53c-305">2017년 6월 30일</span><span class="sxs-lookup"><span data-stu-id="fb53c-305">June 30, 2017</span></span> |--- |
| [<span data-ttu-id="fb53c-306">1.14.1</span><span class="sxs-lookup"><span data-stu-id="fb53c-306">1.14.1</span></span>](#1.14.1) |<span data-ttu-id="fb53c-307">2017년 5월 23일</span><span class="sxs-lookup"><span data-stu-id="fb53c-307">May 23, 2017</span></span> |--- |
| [<span data-ttu-id="fb53c-308">1.14.0</span><span class="sxs-lookup"><span data-stu-id="fb53c-308">1.14.0</span></span>](#1.14.0) |<span data-ttu-id="fb53c-309">2017년 5월 10일</span><span class="sxs-lookup"><span data-stu-id="fb53c-309">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="fb53c-310">1.13.4</span><span class="sxs-lookup"><span data-stu-id="fb53c-310">1.13.4</span></span>](#1.13.4) |<span data-ttu-id="fb53c-311">2017년 5월 09일</span><span class="sxs-lookup"><span data-stu-id="fb53c-311">May 09, 2017</span></span> |--- |
| [<span data-ttu-id="fb53c-312">1.13.3</span><span class="sxs-lookup"><span data-stu-id="fb53c-312">1.13.3</span></span>](#1.13.3) |<span data-ttu-id="fb53c-313">2017년 5월 06일</span><span class="sxs-lookup"><span data-stu-id="fb53c-313">May 06, 2017</span></span> |--- |
| [<span data-ttu-id="fb53c-314">1.13.2</span><span class="sxs-lookup"><span data-stu-id="fb53c-314">1.13.2</span></span>](#1.13.2) |<span data-ttu-id="fb53c-315">2017년 4월 19일</span><span class="sxs-lookup"><span data-stu-id="fb53c-315">April 19, 2017</span></span> |--- |
| [<span data-ttu-id="fb53c-316">1.13.1</span><span class="sxs-lookup"><span data-stu-id="fb53c-316">1.13.1</span></span>](#1.13.1) |<span data-ttu-id="fb53c-317">2017년 3월 29일</span><span class="sxs-lookup"><span data-stu-id="fb53c-317">March 29, 2017</span></span> |--- |
| [<span data-ttu-id="fb53c-318">1.13.0</span><span class="sxs-lookup"><span data-stu-id="fb53c-318">1.13.0</span></span>](#1.13.0) |<span data-ttu-id="fb53c-319">2017년 3월 24일</span><span class="sxs-lookup"><span data-stu-id="fb53c-319">March 24, 2017</span></span> |--- |
| [<span data-ttu-id="fb53c-320">1.12.2</span><span class="sxs-lookup"><span data-stu-id="fb53c-320">1.12.2</span></span>](#1.12.2) |<span data-ttu-id="fb53c-321">2017년 3월 20일</span><span class="sxs-lookup"><span data-stu-id="fb53c-321">March 20, 2017</span></span> |--- |
| [<span data-ttu-id="fb53c-322">1.12.1</span><span class="sxs-lookup"><span data-stu-id="fb53c-322">1.12.1</span></span>](#1.12.1) |<span data-ttu-id="fb53c-323">2017년 3월 14일</span><span class="sxs-lookup"><span data-stu-id="fb53c-323">March 14, 2017</span></span> |--- |
| [<span data-ttu-id="fb53c-324">1.12.0</span><span class="sxs-lookup"><span data-stu-id="fb53c-324">1.12.0</span></span>](#1.12.0) |<span data-ttu-id="fb53c-325">2017년 2월 15일</span><span class="sxs-lookup"><span data-stu-id="fb53c-325">February 15, 2017</span></span> |--- |
| [<span data-ttu-id="fb53c-326">1.11.4</span><span class="sxs-lookup"><span data-stu-id="fb53c-326">1.11.4</span></span>](#1.11.4) |<span data-ttu-id="fb53c-327">2017년 2월 6일</span><span class="sxs-lookup"><span data-stu-id="fb53c-327">February 06, 2017</span></span> |--- |
| [<span data-ttu-id="fb53c-328">1.11.3</span><span class="sxs-lookup"><span data-stu-id="fb53c-328">1.11.3</span></span>](#1.11.3) |<span data-ttu-id="fb53c-329">2017년 1월 26일</span><span class="sxs-lookup"><span data-stu-id="fb53c-329">January 26, 2017</span></span> |--- |
| [<span data-ttu-id="fb53c-330">1.11.1</span><span class="sxs-lookup"><span data-stu-id="fb53c-330">1.11.1</span></span>](#1.11.1) |<span data-ttu-id="fb53c-331">2016년 12월 21일</span><span class="sxs-lookup"><span data-stu-id="fb53c-331">December 21, 2016</span></span> |--- |
| [<span data-ttu-id="fb53c-332">1.11.0</span><span class="sxs-lookup"><span data-stu-id="fb53c-332">1.11.0</span></span>](#1.11.0) |<span data-ttu-id="fb53c-333">2016년 12월 8일</span><span class="sxs-lookup"><span data-stu-id="fb53c-333">December 08, 2016</span></span> |--- |
| [<span data-ttu-id="fb53c-334">1.10.0</span><span class="sxs-lookup"><span data-stu-id="fb53c-334">1.10.0</span></span>](#1.10.0) |<span data-ttu-id="fb53c-335">2016년 9월 27일</span><span class="sxs-lookup"><span data-stu-id="fb53c-335">September 27, 2016</span></span> |--- |
| [<span data-ttu-id="fb53c-336">1.9.5</span><span class="sxs-lookup"><span data-stu-id="fb53c-336">1.9.5</span></span>](#1.9.5) |<span data-ttu-id="fb53c-337">2016년 9월 1일</span><span class="sxs-lookup"><span data-stu-id="fb53c-337">September 01, 2016</span></span> |--- |
| [<span data-ttu-id="fb53c-338">1.9.4</span><span class="sxs-lookup"><span data-stu-id="fb53c-338">1.9.4</span></span>](#1.9.4) |<span data-ttu-id="fb53c-339">2016년 8월 24일</span><span class="sxs-lookup"><span data-stu-id="fb53c-339">August 24, 2016</span></span> |--- |
| [<span data-ttu-id="fb53c-340">1.9.3</span><span class="sxs-lookup"><span data-stu-id="fb53c-340">1.9.3</span></span>](#1.9.3) |<span data-ttu-id="fb53c-341">2016년 8월 15일</span><span class="sxs-lookup"><span data-stu-id="fb53c-341">August 15, 2016</span></span> |--- |
| [<span data-ttu-id="fb53c-342">1.9.2</span><span class="sxs-lookup"><span data-stu-id="fb53c-342">1.9.2</span></span>](#1.9.2) |<span data-ttu-id="fb53c-343">2016년 7월 23일</span><span class="sxs-lookup"><span data-stu-id="fb53c-343">July 23, 2016</span></span> |--- |
| [<span data-ttu-id="fb53c-344">1.8.0</span><span class="sxs-lookup"><span data-stu-id="fb53c-344">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="fb53c-345">2016년 6월 14일</span><span class="sxs-lookup"><span data-stu-id="fb53c-345">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="fb53c-346">1.7.1</span><span class="sxs-lookup"><span data-stu-id="fb53c-346">1.7.1</span></span>](#1.7.1) |<span data-ttu-id="fb53c-347">2016년 5월 6일</span><span class="sxs-lookup"><span data-stu-id="fb53c-347">May 06, 2016</span></span> |--- |
| [<span data-ttu-id="fb53c-348">1.7.0</span><span class="sxs-lookup"><span data-stu-id="fb53c-348">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="fb53c-349">2016년 4월 26일</span><span class="sxs-lookup"><span data-stu-id="fb53c-349">April 26, 2016</span></span> |--- |
| [<span data-ttu-id="fb53c-350">1.6.3</span><span class="sxs-lookup"><span data-stu-id="fb53c-350">1.6.3</span></span>](#1.6.3) |<span data-ttu-id="fb53c-351">2016년 4월 8일</span><span class="sxs-lookup"><span data-stu-id="fb53c-351">April 08, 2016</span></span> |--- |
| [<span data-ttu-id="fb53c-352">1.6.2</span><span class="sxs-lookup"><span data-stu-id="fb53c-352">1.6.2</span></span>](#1.6.2) |<span data-ttu-id="fb53c-353">2016년 3월 29일</span><span class="sxs-lookup"><span data-stu-id="fb53c-353">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="fb53c-354">1.5.3</span><span class="sxs-lookup"><span data-stu-id="fb53c-354">1.5.3</span></span>](#1.5.3) |<span data-ttu-id="fb53c-355">2016년 2월 19일</span><span class="sxs-lookup"><span data-stu-id="fb53c-355">February 19, 2016</span></span> |--- |
| [<span data-ttu-id="fb53c-356">1.5.2</span><span class="sxs-lookup"><span data-stu-id="fb53c-356">1.5.2</span></span>](#1.5.2) |<span data-ttu-id="fb53c-357">2015년 12월 14일</span><span class="sxs-lookup"><span data-stu-id="fb53c-357">December 14, 2015</span></span> |--- |
| [<span data-ttu-id="fb53c-358">1.5.1</span><span class="sxs-lookup"><span data-stu-id="fb53c-358">1.5.1</span></span>](#1.5.1) |<span data-ttu-id="fb53c-359">2015년 11월 23일</span><span class="sxs-lookup"><span data-stu-id="fb53c-359">November 23, 2015</span></span> |--- |
| [<span data-ttu-id="fb53c-360">1.5.0</span><span class="sxs-lookup"><span data-stu-id="fb53c-360">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="fb53c-361">2015년 10월 5일</span><span class="sxs-lookup"><span data-stu-id="fb53c-361">October 05, 2015</span></span> |--- |
| [<span data-ttu-id="fb53c-362">1.4.1</span><span class="sxs-lookup"><span data-stu-id="fb53c-362">1.4.1</span></span>](#1.4.1) |<span data-ttu-id="fb53c-363">2015년 8월 25일</span><span class="sxs-lookup"><span data-stu-id="fb53c-363">August 25, 2015</span></span> |--- |
| [<span data-ttu-id="fb53c-364">1.4.0</span><span class="sxs-lookup"><span data-stu-id="fb53c-364">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="fb53c-365">2015년 8월 13일</span><span class="sxs-lookup"><span data-stu-id="fb53c-365">August 13, 2015</span></span> |--- |
| [<span data-ttu-id="fb53c-366">1.3.0</span><span class="sxs-lookup"><span data-stu-id="fb53c-366">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="fb53c-367">2015년 8월 5일</span><span class="sxs-lookup"><span data-stu-id="fb53c-367">August 05, 2015</span></span> |--- |
| [<span data-ttu-id="fb53c-368">1.2.0</span><span class="sxs-lookup"><span data-stu-id="fb53c-368">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="fb53c-369">2015년 7월 6일</span><span class="sxs-lookup"><span data-stu-id="fb53c-369">July 06, 2015</span></span> |--- |
| [<span data-ttu-id="fb53c-370">1.1.0</span><span class="sxs-lookup"><span data-stu-id="fb53c-370">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="fb53c-371">2015년 4월 30일</span><span class="sxs-lookup"><span data-stu-id="fb53c-371">April 30, 2015</span></span> |--- |
| [<span data-ttu-id="fb53c-372">1.0.0</span><span class="sxs-lookup"><span data-stu-id="fb53c-372">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="fb53c-373">2015년 4월 8일</span><span class="sxs-lookup"><span data-stu-id="fb53c-373">April 08, 2015</span></span> |--- |


## <a name="faq"></a><span data-ttu-id="fb53c-374">FAQ</span><span class="sxs-lookup"><span data-stu-id="fb53c-374">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="fb53c-375">참고 항목</span><span class="sxs-lookup"><span data-stu-id="fb53c-375">See also</span></span>
<span data-ttu-id="fb53c-376">Cosmos DB에 대한 자세한 내용은 [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) 서비스 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fb53c-376">To learn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span> 


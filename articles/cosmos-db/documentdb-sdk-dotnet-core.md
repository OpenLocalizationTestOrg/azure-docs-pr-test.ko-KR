---
title: "Azure Cosmos DB .NET Core API, SDK 및 리소스 | Microsoft Docs"
description: "릴리스 날짜, 사용 중지 날짜 및 Azure Cosmos DB .NET Core SDK의 각 버전 간 변경 내용을 포함하여 .NET Core API 및 SDK에 대한 모든 것을 알아봅니다."
services: cosmos-db
documentationcenter: .net
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: f899b314-26ac-4ddb-86b2-bfdf05c2abf2
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/11/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a7ce4d771e9c655687f72f4b46c7405cf64aeb74
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-net-core-sdk-release-notes-and-resources"></a><span data-ttu-id="8dbc7-103">Azure Cosmos DB .NET Core SDK: 릴리스 정보 및 리소스</span><span class="sxs-lookup"><span data-stu-id="8dbc7-103">Azure Cosmos DB .NET Core SDK: Release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8dbc7-104">.NET</span><span class="sxs-lookup"><span data-stu-id="8dbc7-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="8dbc7-105">.NET 변경 피드</span><span class="sxs-lookup"><span data-stu-id="8dbc7-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="8dbc7-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="8dbc7-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="8dbc7-107">Node.JS</span><span class="sxs-lookup"><span data-stu-id="8dbc7-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="8dbc7-108">Java</span><span class="sxs-lookup"><span data-stu-id="8dbc7-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="8dbc7-109">Python</span><span class="sxs-lookup"><span data-stu-id="8dbc7-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="8dbc7-110">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="8dbc7-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="8dbc7-111">REST 리소스 공급자</span><span class="sxs-lookup"><span data-stu-id="8dbc7-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="8dbc7-112">SQL</span><span class="sxs-lookup"><span data-stu-id="8dbc7-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="8dbc7-113">**SDK 다운로드**</span><span class="sxs-lookup"><span data-stu-id="8dbc7-113">**SDK download**</span></span></td><td>[<span data-ttu-id="8dbc7-114">NuGet</span><span class="sxs-lookup"><span data-stu-id="8dbc7-114">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core/)</td></tr>

<tr><td><span data-ttu-id="8dbc7-115">**API 설명서**</span><span class="sxs-lookup"><span data-stu-id="8dbc7-115">**API documentation**</span></span></td><td>[<span data-ttu-id="8dbc7-116">.NET API 참조 설명서</span><span class="sxs-lookup"><span data-stu-id="8dbc7-116">.NET API reference documentation</span></span>](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet)</td></tr>

<tr><td><span data-ttu-id="8dbc7-117">**샘플**</span><span class="sxs-lookup"><span data-stu-id="8dbc7-117">**Samples**</span></span></td><td>[<span data-ttu-id="8dbc7-118">.NET 코드 샘플</span><span class="sxs-lookup"><span data-stu-id="8dbc7-118">.NET code samples</span></span>](documentdb-dotnet-samples.md)</td></tr>

<tr><td><span data-ttu-id="8dbc7-119">**시작**</span><span class="sxs-lookup"><span data-stu-id="8dbc7-119">**Get started**</span></span></td><td>[<span data-ttu-id="8dbc7-120">Azure Cosmos DB .NET Core SDK 시작</span><span class="sxs-lookup"><span data-stu-id="8dbc7-120">Get started with the Azure Cosmos DB .NET Core SDK</span></span>](documentdb-dotnetcore-get-started.md)</td></tr>

<tr><td><span data-ttu-id="8dbc7-121">**웹앱 자습서**</span><span class="sxs-lookup"><span data-stu-id="8dbc7-121">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="8dbc7-122">Azure Cosmos DB를 사용한 웹 응용 프로그램 개발</span><span class="sxs-lookup"><span data-stu-id="8dbc7-122">Web application development with Azure Cosmos DB</span></span>](documentdb-dotnet-application.md)</td></tr>

<tr><td><span data-ttu-id="8dbc7-123">**현재 지원되는 프레임워크**</span><span class="sxs-lookup"><span data-stu-id="8dbc7-123">**Current supported framework**</span></span></td><td>[<span data-ttu-id="8dbc7-124">.NET Standard 1.6 및 .NET Standard 1.5</span><span class="sxs-lookup"><span data-stu-id="8dbc7-124">.NET Standard 1.6 and .NET Standard 1.5</span></span>](https://www.nuget.org/packages/NETStandard.Library)</td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="8dbc7-125">릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="8dbc7-125">Release Notes</span></span>

<span data-ttu-id="8dbc7-126">Azure Cosmos DB .NET Core SDK에는 [Azure Cosmos DB .NET SDK](documentdb-sdk-dotnet.md)의 최신 버전에 대응하는 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8dbc7-126">The Azure Cosmos DB .NET Core SDK has feature parity with the latest version of the [Azure Cosmos DB .NET SDK](documentdb-sdk-dotnet.md).</span></span>

> [!NOTE] 
> <span data-ttu-id="8dbc7-127">Azure Cosmos DB .NET Core SDK는 UWP(유니버설 Windows 플랫폼) 앱과 호환되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8dbc7-127">The Azure Cosmos DB .NET Core SDK is not yet compatible with Universal Windows Platform (UWP) apps.</span></span> <span data-ttu-id="8dbc7-128">UWP 앱을 지원하는 .NET Core SDK에 관심이 있는 경우 [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com)(으)로 전자 메일을 보내세요.</span><span class="sxs-lookup"><span data-stu-id="8dbc7-128">If you are interested in the .NET Core SDK that does support UWP apps, send email to [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

### <a name="a-name150150"></a><span data-ttu-id="8dbc7-129"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="8dbc7-129"><a name="1.5.0"/>1.5.0</span></span> 

* <span data-ttu-id="8dbc7-130">특정 파티션 키 범위 값으로 쿼리 결과의 범위를 지정하기 위해 PartitionKeyRangeId에 대한 지원이 FeedOption으로 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8dbc7-130">Added support for PartitionKeyRangeId as a FeedOption for scoping query results to a specific partition key range value.</span></span> 
* <span data-ttu-id="8dbc7-131">해당 시간 이후에 변경 검색을 시작할 수 있도록 StartTime에 대한 지원이 ChangeFeedOption으로 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8dbc7-131">Added support for StartTime as a ChangeFeedOption to start looking for the changes after that time.</span></span> 

### <a name="a-name141141"></a><span data-ttu-id="8dbc7-132"><a name="1.4.1"/>1.4.1</span><span class="sxs-lookup"><span data-stu-id="8dbc7-132"><a name="1.4.1"/>1.4.1</span></span>

*   <span data-ttu-id="8dbc7-133">스택 오버플로 예외를 일으킬 수 있는 JsonSerializable 클래스의 문제가 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8dbc7-133">Fixed an issue in the JsonSerializable class that may cause a stack overflow exception.</span></span>

### <a name="a-name140140"></a><span data-ttu-id="8dbc7-134"><a name="1.4.0"/>1.4.0</span><span class="sxs-lookup"><span data-stu-id="8dbc7-134"><a name="1.4.0"/>1.4.0</span></span>

*   <span data-ttu-id="8dbc7-135">[DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet) 인스턴스를 인스턴스화하는 동안 사용자 지정 JsonSerializerSettings를 지정하기 위한 지원을 추가하였습니다.</span><span class="sxs-lookup"><span data-stu-id="8dbc7-135">Added support for specifying custom JsonSerializerSettings while instantiating a [DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet) instance.</span></span>

### <a name="a-name132132"></a><span data-ttu-id="8dbc7-136"><a name="1.3.2"/>1.3.2</span><span class="sxs-lookup"><span data-stu-id="8dbc7-136"><a name="1.3.2"/>1.3.2</span></span>

*   <span data-ttu-id="8dbc7-137">대상 프레임워크 중 하나로 .NET Standard 1.5를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="8dbc7-137">Supporting .NET Standard 1.5 as one of the target frameworks.</span></span>

### <a name="a-name131131"></a><span data-ttu-id="8dbc7-138"><a name="1.3.1"/>1.3.1</span><span class="sxs-lookup"><span data-stu-id="8dbc7-138"><a name="1.3.1"/>1.3.1</span></span>

*   <span data-ttu-id="8dbc7-139">SSE4 명령을 지원하지 않고 Azure Cosmos DB 쿼리를 실행할 때 SEHException을 throw하는 X64 컴퓨터에 영향을 준 문제가 해결되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8dbc7-139">Fixed an issue that affected x64 machines that don’t support SSE4 instruction and throw SEHException when running Azure Cosmos DB queries.</span></span>

### <a name="a-name130130"></a><span data-ttu-id="8dbc7-140"><a name="1.3.0"/>1.3.0</span><span class="sxs-lookup"><span data-stu-id="8dbc7-140"><a name="1.3.0"/>1.3.0</span></span>

*   <span data-ttu-id="8dbc7-141">ConsistentPrefix라는 새로운 일관성 수준에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8dbc7-141">Added support for a new consistency level called ConsistentPrefix.</span></span>
*   <span data-ttu-id="8dbc7-142">개별 파티션의 쿼리 메트릭에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8dbc7-142">Added support for query metrics for individual partitions.</span></span>
*   <span data-ttu-id="8dbc7-143">쿼리의 연속 토큰 크기 제한에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8dbc7-143">Added support for limiting the size of the continuation token for queries.</span></span>
*   <span data-ttu-id="8dbc7-144">실패한 요청의 자세한 추적에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8dbc7-144">Added support for more detailed tracing for failed requests.</span></span>
*   <span data-ttu-id="8dbc7-145">SDK의 성능이 약간 향상되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8dbc7-145">Made some performance improvements in the SDK.</span></span>

### <a name="a-name122122"></a><span data-ttu-id="8dbc7-146"><a name="1.2.2"/>1.2.2</span><span class="sxs-lookup"><span data-stu-id="8dbc7-146"><a name="1.2.2"/>1.2.2</span></span>

* <span data-ttu-id="8dbc7-147">집계 쿼리에 대한 FeedOptions에 제공된 PartitionKey 값을 무시하던 문제를 해결했습니다.</span><span class="sxs-lookup"><span data-stu-id="8dbc7-147">Fixed an issue that ignored the PartitionKey value provided in FeedOptions for aggregate queries.</span></span>
* <span data-ttu-id="8dbc7-148">플라이트 중간의 파티션 간 Order By 쿼리를 실행하는 동안 파티션 관리의 투명한 처리 문제를 해결했습니다.</span><span class="sxs-lookup"><span data-stu-id="8dbc7-148">Fixed an issue in transparent handling of partition management during mid-flight cross-partition Order By query execution.</span></span>

### <a name="a-name121121"></a><span data-ttu-id="8dbc7-149"><a name="1.2.1"/>1.2.1</span><span class="sxs-lookup"><span data-stu-id="8dbc7-149"><a name="1.2.1"/>1.2.1</span></span>

* <span data-ttu-id="8dbc7-150">ASP.NET 컨텍스트 내에서 사용할 경우 일부 비동기 API에서 교착 상태를 일으키는 문제를 해결했습니다.</span><span class="sxs-lookup"><span data-stu-id="8dbc7-150">Fixed an issue which caused deadlocks in some of the async APIs when used inside ASP.NET context.</span></span>

### <a name="a-name120120"></a><span data-ttu-id="8dbc7-151"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="8dbc7-151"><a name="1.2.0"/>1.2.0</span></span>

* <span data-ttu-id="8dbc7-152">특정 조건에서 자동 장애 조치(Failover)를 수행하도록 SDK를 좀 더 탄력적으로 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="8dbc7-152">Fixes to make SDK more resilient to automatic failover under certain conditions.</span></span>

### <a name="a-name112112"></a><span data-ttu-id="8dbc7-153"><a name="1.1.2"/>1.1.2</span><span class="sxs-lookup"><span data-stu-id="8dbc7-153"><a name="1.1.2"/>1.1.2</span></span>

* <span data-ttu-id="8dbc7-154">문제를 수정하는 경우 때때로 WebException이 발생합니다. 원격 이름을 확인할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8dbc7-154">Fix for an issue that occasionally causes a WebException: The remote name could not be resolved.</span></span>
* <span data-ttu-id="8dbc7-155">ReadDocumentAsync API에 새 오버로드를 추가하여 형식화된 문서를 직접 읽기 위한 지원을 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="8dbc7-155">Added the support for directly reading a typed document by adding new overloads to ReadDocumentAsync API.</span></span>

### <a name="a-name111111"></a><span data-ttu-id="8dbc7-156"><a name="1.1.1"/>1.1.1</span><span class="sxs-lookup"><span data-stu-id="8dbc7-156"><a name="1.1.1"/>1.1.1</span></span>

* <span data-ttu-id="8dbc7-157">집계 쿼리(COUNT, MIN, MAX, SUM 및 AVG)에 대한 LINQ 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8dbc7-157">Added LINQ support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="8dbc7-158">이벤트 처리기를 사용하여 발생한 ConnectionPolicy 개체의 메모리 누수 문제를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="8dbc7-158">Fix for a memory leak issue for the ConnectionPolicy object caused by the use of event handler.</span></span>
* <span data-ttu-id="8dbc7-159">ETag를 사용할 때 UpsertAttachmentAsync가 작동하지 않는 문제를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="8dbc7-159">Fix for an issue wherein UpsertAttachmentAsync was not working when ETag was used.</span></span>
* <span data-ttu-id="8dbc7-160">문자열 필드를 정렬할 때 파티션 간 order-by 쿼리 연속 작업이 작동하지 않는 문제를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="8dbc7-160">Fix for an issue wherein cross partition order-by query continuation was not working when sorting on string field.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="8dbc7-161"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="8dbc7-161"><a name="1.1.0"/>1.1.0</span></span>

* <span data-ttu-id="8dbc7-162">집계 쿼리(COUNT, MIN, MAX, SUM 및 AVG)에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8dbc7-162">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span> <span data-ttu-id="8dbc7-163">[집계 지원](documentdb-sql-query.md#Aggregates)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8dbc7-163">See [Aggregation support](documentdb-sql-query.md#Aggregates).</span></span>
* <span data-ttu-id="8dbc7-164">분할된 컬렉션에 대한 최소 처리량이 10,100RU/s에서 2500RU/s로 감소됩니다.</span><span class="sxs-lookup"><span data-stu-id="8dbc7-164">Lowered minimum throughput on partitioned collections from 10,100 RU/s to 2500 RU/s.</span></span>

### <a name="a-name100100"></a><span data-ttu-id="8dbc7-165"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="8dbc7-165"><a name="1.0.0"/>1.0.0</span></span>

<span data-ttu-id="8dbc7-166">Azure Cosmos DB .NET Core SDK를 사용하면 Windows, Mac 및 Linux에서 실행하는 빠른 플랫폼 간 [ASP.NET Core](https://www.asp.net/core) 및 [.NET Core](https://www.microsoft.com/net/core#windows) 앱을 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8dbc7-166">The Azure Cosmos DB .NET Core SDK enables you to build fast, cross-platform [ASP.NET Core](https://www.asp.net/core) and [.NET Core](https://www.microsoft.com/net/core#windows) apps to run on Windows, Mac, and Linux.</span></span> <span data-ttu-id="8dbc7-167">Azure Cosmos DB .NET Core SDK 최신 릴리스는 [Xamarin](https://www.xamarin.com)과 완벽하게 호환되며 iOS, Android 및 Mono(Linux)를 대상으로 하는 응용 프로그램을 빌드하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="8dbc7-167">The latest release of the Azure Cosmos DB .NET Core SDK is fully [Xamarin](https://www.xamarin.com) compatible and be used to build applications that target iOS, Android, and Mono (Linux).</span></span>  

### <a name="a-name010-preview010-preview"></a><span data-ttu-id="8dbc7-168"><a name="0.1.0-preview"/>0.1.0-preview</span><span class="sxs-lookup"><span data-stu-id="8dbc7-168"><a name="0.1.0-preview"/>0.1.0-preview</span></span>

<span data-ttu-id="8dbc7-169">Azure Cosmos DB .NET Core Preview SDK를 사용하면 Windows, Mac 및 Linux에서 실행하는 빠른 플랫폼 간 [ASP.NET Core](https://www.asp.net/core) 및 [.NET Core](https://www.microsoft.com/net/core#windows) 앱을 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8dbc7-169">The Azure Cosmos DB .NET Core Preview SDK enables you to build fast, cross-platform [ASP.NET Core](https://www.asp.net/core) and [.NET Core](https://www.microsoft.com/net/core#windows) apps to run on Windows, Mac, and Linux.</span></span>

<span data-ttu-id="8dbc7-170">Azure Cosmos DB .NET Core Preview SDK에는 [Azure Cosmos DB .NET SDK](documentdb-sdk-dotnet.md)의 최신 버전에 대응하는 기능이 있으며 다음이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="8dbc7-170">The Azure Cosmos DB .NET Core Preview SDK has feature parity with the latest version of the [Azure Cosmos DB .NET SDK](documentdb-sdk-dotnet.md) and supports the following:</span></span>
* <span data-ttu-id="8dbc7-171">모든 [연결 모드](performance-tips.md#networking): 게이트웨이 모드, Direct TCP 및 Direct HTTP</span><span class="sxs-lookup"><span data-stu-id="8dbc7-171">All [connection modes](performance-tips.md#networking): Gateway mode, Direct TCP, and Direct HTTPs.</span></span> 
* <span data-ttu-id="8dbc7-172">모든 [일관성 수준](consistency-levels.md): 강함, 세션, 제한된 부실, 최종</span><span class="sxs-lookup"><span data-stu-id="8dbc7-172">All [consistency levels](consistency-levels.md): Strong, Session, Bounded Staleness, and Eventual.</span></span>
* <span data-ttu-id="8dbc7-173">[분할된 컬렉션](partition-data.md)</span><span class="sxs-lookup"><span data-stu-id="8dbc7-173">[Partitioned collections](partition-data.md).</span></span> 
* <span data-ttu-id="8dbc7-174">[다중 하위 지역 데이터베이스 계정 및 지역에서 복제](distribute-data-globally.md)</span><span class="sxs-lookup"><span data-stu-id="8dbc7-174">[Multi-region database accounts and geo-replication](distribute-data-globally.md).</span></span>

<span data-ttu-id="8dbc7-175">이 SDK와 관련된 질문이 있으면 [StackOverflow](http://stackoverflow.com/questions/tagged/azure-documentdb)에 게시하거나 [github 저장소](https://github.com/Azure/azure-documentdb-dotnet/issues)에서 문제를 제기하세요.</span><span class="sxs-lookup"><span data-stu-id="8dbc7-175">If you have questions related to this SDK, post to [StackOverflow](http://stackoverflow.com/questions/tagged/azure-documentdb), or file an issue in the [github repository](https://github.com/Azure/azure-documentdb-dotnet/issues).</span></span> 

## <a name="release--retirement-dates"></a><span data-ttu-id="8dbc7-176">릴리스 및 사용 중지 날짜</span><span class="sxs-lookup"><span data-stu-id="8dbc7-176">Release & Retirement Dates</span></span>

| <span data-ttu-id="8dbc7-177">버전</span><span class="sxs-lookup"><span data-stu-id="8dbc7-177">Version</span></span> | <span data-ttu-id="8dbc7-178">릴리스 날짜</span><span class="sxs-lookup"><span data-stu-id="8dbc7-178">Release Date</span></span> | <span data-ttu-id="8dbc7-179">사용 중지 날짜</span><span class="sxs-lookup"><span data-stu-id="8dbc7-179">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="8dbc7-180">1.5.0</span><span class="sxs-lookup"><span data-stu-id="8dbc7-180">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="8dbc7-181">2017년 8월 10일</span><span class="sxs-lookup"><span data-stu-id="8dbc7-181">August 10, 2017</span></span> |--- | 
| [<span data-ttu-id="8dbc7-182">1.4.1</span><span class="sxs-lookup"><span data-stu-id="8dbc7-182">1.4.1</span></span>](#1.4.1) |<span data-ttu-id="8dbc7-183">2017년 8월 7일</span><span class="sxs-lookup"><span data-stu-id="8dbc7-183">August 07, 2017</span></span> |--- |
| [<span data-ttu-id="8dbc7-184">1.4.0</span><span class="sxs-lookup"><span data-stu-id="8dbc7-184">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="8dbc7-185">2017년 8월 2일</span><span class="sxs-lookup"><span data-stu-id="8dbc7-185">August 02, 2017</span></span> |--- |
| [<span data-ttu-id="8dbc7-186">1.3.2</span><span class="sxs-lookup"><span data-stu-id="8dbc7-186">1.3.2</span></span>](#1.3.2) |<span data-ttu-id="8dbc7-187">2017년 6월 12일</span><span class="sxs-lookup"><span data-stu-id="8dbc7-187">June 12, 2017</span></span> |--- |
| [<span data-ttu-id="8dbc7-188">1.3.1</span><span class="sxs-lookup"><span data-stu-id="8dbc7-188">1.3.1</span></span>](#1.3.1) |<span data-ttu-id="8dbc7-189">2017년 5월 23일</span><span class="sxs-lookup"><span data-stu-id="8dbc7-189">May 23, 2017</span></span> |--- |
| [<span data-ttu-id="8dbc7-190">1.3.0</span><span class="sxs-lookup"><span data-stu-id="8dbc7-190">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="8dbc7-191">2017년 5월 10일</span><span class="sxs-lookup"><span data-stu-id="8dbc7-191">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="8dbc7-192">1.2.2</span><span class="sxs-lookup"><span data-stu-id="8dbc7-192">1.2.2</span></span>](#1.2.2) |<span data-ttu-id="8dbc7-193">2017년 4월 19일</span><span class="sxs-lookup"><span data-stu-id="8dbc7-193">April 19, 2017</span></span> |--- |
| [<span data-ttu-id="8dbc7-194">1.2.1</span><span class="sxs-lookup"><span data-stu-id="8dbc7-194">1.2.1</span></span>](#1.2.1) |<span data-ttu-id="8dbc7-195">2017년 3월 29일</span><span class="sxs-lookup"><span data-stu-id="8dbc7-195">March 29, 2017</span></span> |--- |
| [<span data-ttu-id="8dbc7-196">1.2.0</span><span class="sxs-lookup"><span data-stu-id="8dbc7-196">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="8dbc7-197">2017년 3월 25일</span><span class="sxs-lookup"><span data-stu-id="8dbc7-197">March 25, 2017</span></span> |--- |
| [<span data-ttu-id="8dbc7-198">1.1.2</span><span class="sxs-lookup"><span data-stu-id="8dbc7-198">1.1.2</span></span>](#1.1.2) |<span data-ttu-id="8dbc7-199">2017년 3월 20일</span><span class="sxs-lookup"><span data-stu-id="8dbc7-199">March 20, 2017</span></span> |--- |
| [<span data-ttu-id="8dbc7-200">1.1.1</span><span class="sxs-lookup"><span data-stu-id="8dbc7-200">1.1.1</span></span>](#1.1.1) |<span data-ttu-id="8dbc7-201">2017년 3월 14일</span><span class="sxs-lookup"><span data-stu-id="8dbc7-201">March 14, 2017</span></span> |--- |
| [<span data-ttu-id="8dbc7-202">1.1.0</span><span class="sxs-lookup"><span data-stu-id="8dbc7-202">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="8dbc7-203">2017년 2월 16일</span><span class="sxs-lookup"><span data-stu-id="8dbc7-203">February 16, 2017</span></span> |--- |
| [<span data-ttu-id="8dbc7-204">1.0.0</span><span class="sxs-lookup"><span data-stu-id="8dbc7-204">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="8dbc7-205">2016년 12월 21일</span><span class="sxs-lookup"><span data-stu-id="8dbc7-205">December 21, 2016</span></span> |--- |
| [<span data-ttu-id="8dbc7-206">0.1.0-preview</span><span class="sxs-lookup"><span data-stu-id="8dbc7-206">0.1.0-preview</span></span>](#0.1.0-preview) |<span data-ttu-id="8dbc7-207">2016년 11월 15일</span><span class="sxs-lookup"><span data-stu-id="8dbc7-207">November 15, 2016</span></span> |<span data-ttu-id="8dbc7-208">2015년 12월 31일</span><span class="sxs-lookup"><span data-stu-id="8dbc7-208">December 31, 2016</span></span> |

## <a name="see-also"></a><span data-ttu-id="8dbc7-209">참고 항목</span><span class="sxs-lookup"><span data-stu-id="8dbc7-209">See Also</span></span>
<span data-ttu-id="8dbc7-210">Cosmos DB에 대한 자세한 내용은 [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) 서비스 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8dbc7-210">To learn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span> 


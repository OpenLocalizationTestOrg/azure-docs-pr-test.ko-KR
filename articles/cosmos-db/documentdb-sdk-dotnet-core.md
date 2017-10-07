---
title: "aaaAzure Cosmos DB.NET Core API SDK 및 리소스 | Microsoft Docs"
description: ".NET Core API 및 SDK 릴리스 날짜, 사용 중지 날짜 및 hello Azure Cosmos DB.NET Core SDK의 각 버전 간의 변경 내용을 포함 하 여 hello에 대 한 모든에 대해 알아봅니다."
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
ms.openlocfilehash: 1269cafe0ea1caaa871404d507b12632dbb3ed82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-net-core-sdk-release-notes-and-resources"></a><span data-ttu-id="60ffb-103">Azure Cosmos DB .NET Core SDK: 릴리스 정보 및 리소스</span><span class="sxs-lookup"><span data-stu-id="60ffb-103">Azure Cosmos DB .NET Core SDK: Release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="60ffb-104">.NET</span><span class="sxs-lookup"><span data-stu-id="60ffb-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="60ffb-105">.NET 변경 피드</span><span class="sxs-lookup"><span data-stu-id="60ffb-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="60ffb-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="60ffb-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="60ffb-107">Node.JS</span><span class="sxs-lookup"><span data-stu-id="60ffb-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="60ffb-108">Java</span><span class="sxs-lookup"><span data-stu-id="60ffb-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="60ffb-109">Python</span><span class="sxs-lookup"><span data-stu-id="60ffb-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="60ffb-110">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="60ffb-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="60ffb-111">REST 리소스 공급자</span><span class="sxs-lookup"><span data-stu-id="60ffb-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="60ffb-112">SQL</span><span class="sxs-lookup"><span data-stu-id="60ffb-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="60ffb-113">**SDK 다운로드**</span><span class="sxs-lookup"><span data-stu-id="60ffb-113">**SDK download**</span></span></td><td>[<span data-ttu-id="60ffb-114">NuGet</span><span class="sxs-lookup"><span data-stu-id="60ffb-114">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core/)</td></tr>

<tr><td><span data-ttu-id="60ffb-115">**API 설명서**</span><span class="sxs-lookup"><span data-stu-id="60ffb-115">**API documentation**</span></span></td><td>[<span data-ttu-id="60ffb-116">.NET API 참조 설명서</span><span class="sxs-lookup"><span data-stu-id="60ffb-116">.NET API reference documentation</span></span>](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet)</td></tr>

<tr><td><span data-ttu-id="60ffb-117">**샘플**</span><span class="sxs-lookup"><span data-stu-id="60ffb-117">**Samples**</span></span></td><td>[<span data-ttu-id="60ffb-118">.NET 코드 샘플</span><span class="sxs-lookup"><span data-stu-id="60ffb-118">.NET code samples</span></span>](documentdb-dotnet-samples.md)</td></tr>

<tr><td><span data-ttu-id="60ffb-119">**시작**</span><span class="sxs-lookup"><span data-stu-id="60ffb-119">**Get started**</span></span></td><td>[<span data-ttu-id="60ffb-120">Hello Azure Cosmos DB.NET Core SDK 시작</span><span class="sxs-lookup"><span data-stu-id="60ffb-120">Get started with hello Azure Cosmos DB .NET Core SDK</span></span>](documentdb-dotnetcore-get-started.md)</td></tr>

<tr><td><span data-ttu-id="60ffb-121">**웹앱 자습서**</span><span class="sxs-lookup"><span data-stu-id="60ffb-121">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="60ffb-122">Azure Cosmos DB를 사용한 웹 응용 프로그램 개발</span><span class="sxs-lookup"><span data-stu-id="60ffb-122">Web application development with Azure Cosmos DB</span></span>](documentdb-dotnet-application.md)</td></tr>

<tr><td><span data-ttu-id="60ffb-123">**현재 지원되는 프레임워크**</span><span class="sxs-lookup"><span data-stu-id="60ffb-123">**Current supported framework**</span></span></td><td>[<span data-ttu-id="60ffb-124">.NET Standard 1.6 및 .NET Standard 1.5</span><span class="sxs-lookup"><span data-stu-id="60ffb-124">.NET Standard 1.6 and .NET Standard 1.5</span></span>](https://www.nuget.org/packages/NETStandard.Library)</td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="60ffb-125">릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="60ffb-125">Release Notes</span></span>

<span data-ttu-id="60ffb-126">hello Azure Cosmos DB.NET Core SDK에 기능 패리티를 최신 버전의 hello hello [Cosmos DB AZURE.NET SDK](documentdb-sdk-dotnet.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="60ffb-126">hello Azure Cosmos DB .NET Core SDK has feature parity with hello latest version of hello [Azure Cosmos DB .NET SDK](documentdb-sdk-dotnet.md).</span></span>

> [!NOTE] 
> <span data-ttu-id="60ffb-127">hello Azure Cosmos DB.NET Core SDK 유니버설 Windows 플랫폼 (UWP) 앱과 호환 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="60ffb-127">hello Azure Cosmos DB .NET Core SDK is not yet compatible with Universal Windows Platform (UWP) apps.</span></span> <span data-ttu-id="60ffb-128">UWP 앱에서는.NET Core SDK hello에 관심이 있는 경우 전자 메일 보내기 너무[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="60ffb-128">If you are interested in hello .NET Core SDK that does support UWP apps, send email too[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

### <a name="a-name150150"></a><span data-ttu-id="60ffb-129"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="60ffb-129"><a name="1.5.0"/>1.5.0</span></span> 

* <span data-ttu-id="60ffb-130">쿼리 결과 tooa 특정 파티션 키 범위 값의 범위를 지정 하는 것에 대 한 FeedOption으로 PartitionKeyRangeId에 대 한 지원이 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="60ffb-130">Added support for PartitionKeyRangeId as a FeedOption for scoping query results tooa specific partition key range value.</span></span> 
* <span data-ttu-id="60ffb-131">해당 시간 이후에 hello 변경 내용 검색 ChangeFeedOption toostart로 StartTime에 대 한 지원이 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="60ffb-131">Added support for StartTime as a ChangeFeedOption toostart looking for hello changes after that time.</span></span> 

### <a name="a-name141141"></a><span data-ttu-id="60ffb-132"><a name="1.4.1"/>1.4.1</span><span class="sxs-lookup"><span data-stu-id="60ffb-132"><a name="1.4.1"/>1.4.1</span></span>

*   <span data-ttu-id="60ffb-133">Hello 스택 오버플로 예외를 일으킬 수 있는 JsonSerializable 클래스에에서는 문제가 해결 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="60ffb-133">Fixed an issue in hello JsonSerializable class that may cause a stack overflow exception.</span></span>

### <a name="a-name140140"></a><span data-ttu-id="60ffb-134"><a name="1.4.0"/>1.4.0</span><span class="sxs-lookup"><span data-stu-id="60ffb-134"><a name="1.4.0"/>1.4.0</span></span>

*   <span data-ttu-id="60ffb-135">[DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet) 인스턴스를 인스턴스화하는 동안 사용자 지정 JsonSerializerSettings를 지정하기 위한 지원을 추가하였습니다.</span><span class="sxs-lookup"><span data-stu-id="60ffb-135">Added support for specifying custom JsonSerializerSettings while instantiating a [DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet) instance.</span></span>

### <a name="a-name132132"></a><span data-ttu-id="60ffb-136"><a name="1.3.2"/>1.3.2</span><span class="sxs-lookup"><span data-stu-id="60ffb-136"><a name="1.3.2"/>1.3.2</span></span>

*   <span data-ttu-id="60ffb-137">Hello 대상 프레임 워크 중 하나로.NET 표준 1.5를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="60ffb-137">Supporting .NET Standard 1.5 as one of hello target frameworks.</span></span>

### <a name="a-name131131"></a><span data-ttu-id="60ffb-138"><a name="1.3.1"/>1.3.1</span><span class="sxs-lookup"><span data-stu-id="60ffb-138"><a name="1.3.1"/>1.3.1</span></span>

*   <span data-ttu-id="60ffb-139">SSE4 명령을 지원하지 않고 Azure Cosmos DB 쿼리를 실행할 때 SEHException을 throw하는 X64 컴퓨터에 영향을 준 문제가 해결되었습니다.</span><span class="sxs-lookup"><span data-stu-id="60ffb-139">Fixed an issue that affected x64 machines that don’t support SSE4 instruction and throw SEHException when running Azure Cosmos DB queries.</span></span>

### <a name="a-name130130"></a><span data-ttu-id="60ffb-140"><a name="1.3.0"/>1.3.0</span><span class="sxs-lookup"><span data-stu-id="60ffb-140"><a name="1.3.0"/>1.3.0</span></span>

*   <span data-ttu-id="60ffb-141">ConsistentPrefix라는 새로운 일관성 수준에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="60ffb-141">Added support for a new consistency level called ConsistentPrefix.</span></span>
*   <span data-ttu-id="60ffb-142">개별 파티션의 쿼리 메트릭에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="60ffb-142">Added support for query metrics for individual partitions.</span></span>
*   <span data-ttu-id="60ffb-143">쿼리에 대 한 hello 연속 토큰의 hello 크기 제한에 대 한 지원이 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="60ffb-143">Added support for limiting hello size of hello continuation token for queries.</span></span>
*   <span data-ttu-id="60ffb-144">실패한 요청의 자세한 추적에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="60ffb-144">Added support for more detailed tracing for failed requests.</span></span>
*   <span data-ttu-id="60ffb-145">Hello SDK 일부 성능 향상이 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="60ffb-145">Made some performance improvements in hello SDK.</span></span>

### <a name="a-name122122"></a><span data-ttu-id="60ffb-146"><a name="1.2.2"/>1.2.2</span><span class="sxs-lookup"><span data-stu-id="60ffb-146"><a name="1.2.2"/>1.2.2</span></span>

* <span data-ttu-id="60ffb-147">집계 쿼리에 대 한 FeedOptions에 제공 된 hello PartitionKey 값을 무시 하는 문제가 해결 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="60ffb-147">Fixed an issue that ignored hello PartitionKey value provided in FeedOptions for aggregate queries.</span></span>
* <span data-ttu-id="60ffb-148">플라이트 중간의 파티션 간 Order By 쿼리를 실행하는 동안 파티션 관리의 투명한 처리 문제를 해결했습니다.</span><span class="sxs-lookup"><span data-stu-id="60ffb-148">Fixed an issue in transparent handling of partition management during mid-flight cross-partition Order By query execution.</span></span>

### <a name="a-name121121"></a><span data-ttu-id="60ffb-149"><a name="1.2.1"/>1.2.1</span><span class="sxs-lookup"><span data-stu-id="60ffb-149"><a name="1.2.1"/>1.2.1</span></span>

* <span data-ttu-id="60ffb-150">Hello 비동기 ASP.NET 컨텍스트 내에서 사용 하는 경우 Api의 일부에서 교착 상태를 일으킨 문제가 해결 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="60ffb-150">Fixed an issue which caused deadlocks in some of hello async APIs when used inside ASP.NET context.</span></span>

### <a name="a-name120120"></a><span data-ttu-id="60ffb-151"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="60ffb-151"><a name="1.2.0"/>1.2.0</span></span>

* <span data-ttu-id="60ffb-152">SDK toomake 더 해결 특정 조건에서 탄력적인 tooautomatic 장애 조치 합니다.</span><span class="sxs-lookup"><span data-stu-id="60ffb-152">Fixes toomake SDK more resilient tooautomatic failover under certain conditions.</span></span>

### <a name="a-name112112"></a><span data-ttu-id="60ffb-153"><a name="1.1.2"/>1.1.2</span><span class="sxs-lookup"><span data-stu-id="60ffb-153"><a name="1.1.2"/>1.1.2</span></span>

* <span data-ttu-id="60ffb-154">경우에 따라 WebException을 야기 하는 문제에 대 한 수정: hello 원격 이름을 확인할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="60ffb-154">Fix for an issue that occasionally causes a WebException: hello remote name could not be resolved.</span></span>
* <span data-ttu-id="60ffb-155">추가 된 hello 직접 새 오버 로드 tooReadDocumentAsync API를 추가 하 여 형식화 된 문서를 읽기 위한 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="60ffb-155">Added hello support for directly reading a typed document by adding new overloads tooReadDocumentAsync API.</span></span>

### <a name="a-name111111"></a><span data-ttu-id="60ffb-156"><a name="1.1.1"/>1.1.1</span><span class="sxs-lookup"><span data-stu-id="60ffb-156"><a name="1.1.1"/>1.1.1</span></span>

* <span data-ttu-id="60ffb-157">집계 쿼리(COUNT, MIN, MAX, SUM 및 AVG)에 대한 LINQ 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="60ffb-157">Added LINQ support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="60ffb-158">용 hello 이벤트 처리기를 사용 하 여 발생 하는 hello ConnectionPolicy 개체에 대 한 메모리 누수 문제를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="60ffb-158">Fix for a memory leak issue for hello ConnectionPolicy object caused by hello use of event handler.</span></span>
* <span data-ttu-id="60ffb-159">ETag를 사용할 때 UpsertAttachmentAsync가 작동하지 않는 문제를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="60ffb-159">Fix for an issue wherein UpsertAttachmentAsync was not working when ETag was used.</span></span>
* <span data-ttu-id="60ffb-160">문자열 필드를 정렬할 때 파티션 간 order-by 쿼리 연속 작업이 작동하지 않는 문제를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="60ffb-160">Fix for an issue wherein cross partition order-by query continuation was not working when sorting on string field.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="60ffb-161"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="60ffb-161"><a name="1.1.0"/>1.1.0</span></span>

* <span data-ttu-id="60ffb-162">집계 쿼리(COUNT, MIN, MAX, SUM 및 AVG)에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="60ffb-162">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span> <span data-ttu-id="60ffb-163">[집계 지원](documentdb-sql-query.md#Aggregates)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60ffb-163">See [Aggregation support](documentdb-sql-query.md#Aggregates).</span></span>
* <span data-ttu-id="60ffb-164">10,100 000RU/s too2500 000RU/s에서 분할 된 컬렉션에 대해 최소 처리량을 적어집니다.</span><span class="sxs-lookup"><span data-stu-id="60ffb-164">Lowered minimum throughput on partitioned collections from 10,100 RU/s too2500 RU/s.</span></span>

### <a name="a-name100100"></a><span data-ttu-id="60ffb-165"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="60ffb-165"><a name="1.0.0"/>1.0.0</span></span>

<span data-ttu-id="60ffb-166">hello Azure Cosmos DB.NET Core SDK를 사용 하면 toobuild 빠름, 플랫폼 간 [ASP.NET Core](https://www.asp.net/core) 및 [.NET Core](https://www.microsoft.com/net/core#windows) Windows, Mac 및 Linux에서 앱 toorun 합니다.</span><span class="sxs-lookup"><span data-stu-id="60ffb-166">hello Azure Cosmos DB .NET Core SDK enables you toobuild fast, cross-platform [ASP.NET Core](https://www.asp.net/core) and [.NET Core](https://www.microsoft.com/net/core#windows) apps toorun on Windows, Mac, and Linux.</span></span> <span data-ttu-id="60ffb-167">hello hello Azure Cosmos DB.NET Core SDK의 최신 릴리스는 완벽 하 게 [Xamarin](https://www.xamarin.com) 호환 iOS, Android 및 모노 (Linux)을 대상으로 하는 응용 프로그램에서 사용 되는 toobuild 이어야 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60ffb-167">hello latest release of hello Azure Cosmos DB .NET Core SDK is fully [Xamarin](https://www.xamarin.com) compatible and be used toobuild applications that target iOS, Android, and Mono (Linux).</span></span>  

### <a name="a-name010-preview010-preview"></a><span data-ttu-id="60ffb-168"><a name="0.1.0-preview"/>0.1.0-preview</span><span class="sxs-lookup"><span data-stu-id="60ffb-168"><a name="0.1.0-preview"/>0.1.0-preview</span></span>

<span data-ttu-id="60ffb-169">hello Azure Cosmos DB.NET Core 미리 보기 SDK를 사용 하면 toobuild 빠름, 플랫폼 간 [ASP.NET Core](https://www.asp.net/core) 및 [.NET Core](https://www.microsoft.com/net/core#windows) Windows, Mac 및 Linux에서 앱 toorun 합니다.</span><span class="sxs-lookup"><span data-stu-id="60ffb-169">hello Azure Cosmos DB .NET Core Preview SDK enables you toobuild fast, cross-platform [ASP.NET Core](https://www.asp.net/core) and [.NET Core](https://www.microsoft.com/net/core#windows) apps toorun on Windows, Mac, and Linux.</span></span>

<span data-ttu-id="60ffb-170">hello Azure Cosmos DB.NET Core 미리 보기 SDK에 기능 패리티를 최신 버전의 hello hello [Cosmos DB AZURE.NET SDK](documentdb-sdk-dotnet.md) hello 다음과 같은 지원 및:</span><span class="sxs-lookup"><span data-stu-id="60ffb-170">hello Azure Cosmos DB .NET Core Preview SDK has feature parity with hello latest version of hello [Azure Cosmos DB .NET SDK](documentdb-sdk-dotnet.md) and supports hello following:</span></span>
* <span data-ttu-id="60ffb-171">모든 [연결 모드](performance-tips.md#networking): 게이트웨이 모드, Direct TCP 및 Direct HTTP</span><span class="sxs-lookup"><span data-stu-id="60ffb-171">All [connection modes](performance-tips.md#networking): Gateway mode, Direct TCP, and Direct HTTPs.</span></span> 
* <span data-ttu-id="60ffb-172">모든 [일관성 수준](consistency-levels.md): 강함, 세션, 제한된 부실, 최종</span><span class="sxs-lookup"><span data-stu-id="60ffb-172">All [consistency levels](consistency-levels.md): Strong, Session, Bounded Staleness, and Eventual.</span></span>
* <span data-ttu-id="60ffb-173">[분할된 컬렉션](partition-data.md)</span><span class="sxs-lookup"><span data-stu-id="60ffb-173">[Partitioned collections](partition-data.md).</span></span> 
* <span data-ttu-id="60ffb-174">[다중 하위 지역 데이터베이스 계정 및 지역에서 복제](distribute-data-globally.md)</span><span class="sxs-lookup"><span data-stu-id="60ffb-174">[Multi-region database accounts and geo-replication](distribute-data-globally.md).</span></span>

<span data-ttu-id="60ffb-175">질문 관련된 toothis SDK를 사용 하도록 설정한 경우 너무 게시[StackOverflow](http://stackoverflow.com/questions/tagged/azure-documentdb), hello에 문제를 제출 또는 [github 리포지토리](https://github.com/Azure/azure-documentdb-dotnet/issues)합니다.</span><span class="sxs-lookup"><span data-stu-id="60ffb-175">If you have questions related toothis SDK, post too[StackOverflow](http://stackoverflow.com/questions/tagged/azure-documentdb), or file an issue in hello [github repository](https://github.com/Azure/azure-documentdb-dotnet/issues).</span></span> 

## <a name="release--retirement-dates"></a><span data-ttu-id="60ffb-176">릴리스 및 사용 중지 날짜</span><span class="sxs-lookup"><span data-stu-id="60ffb-176">Release & Retirement Dates</span></span>

| <span data-ttu-id="60ffb-177">버전</span><span class="sxs-lookup"><span data-stu-id="60ffb-177">Version</span></span> | <span data-ttu-id="60ffb-178">릴리스 날짜</span><span class="sxs-lookup"><span data-stu-id="60ffb-178">Release Date</span></span> | <span data-ttu-id="60ffb-179">사용 중지 날짜</span><span class="sxs-lookup"><span data-stu-id="60ffb-179">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="60ffb-180">1.5.0</span><span class="sxs-lookup"><span data-stu-id="60ffb-180">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="60ffb-181">2017년 8월 10일</span><span class="sxs-lookup"><span data-stu-id="60ffb-181">August 10, 2017</span></span> |--- | 
| [<span data-ttu-id="60ffb-182">1.4.1</span><span class="sxs-lookup"><span data-stu-id="60ffb-182">1.4.1</span></span>](#1.4.1) |<span data-ttu-id="60ffb-183">2017년 8월 7일</span><span class="sxs-lookup"><span data-stu-id="60ffb-183">August 07, 2017</span></span> |--- |
| [<span data-ttu-id="60ffb-184">1.4.0</span><span class="sxs-lookup"><span data-stu-id="60ffb-184">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="60ffb-185">2017년 8월 2일</span><span class="sxs-lookup"><span data-stu-id="60ffb-185">August 02, 2017</span></span> |--- |
| [<span data-ttu-id="60ffb-186">1.3.2</span><span class="sxs-lookup"><span data-stu-id="60ffb-186">1.3.2</span></span>](#1.3.2) |<span data-ttu-id="60ffb-187">2017년 6월 12일</span><span class="sxs-lookup"><span data-stu-id="60ffb-187">June 12, 2017</span></span> |--- |
| [<span data-ttu-id="60ffb-188">1.3.1</span><span class="sxs-lookup"><span data-stu-id="60ffb-188">1.3.1</span></span>](#1.3.1) |<span data-ttu-id="60ffb-189">2017년 5월 23일</span><span class="sxs-lookup"><span data-stu-id="60ffb-189">May 23, 2017</span></span> |--- |
| [<span data-ttu-id="60ffb-190">1.3.0</span><span class="sxs-lookup"><span data-stu-id="60ffb-190">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="60ffb-191">2017년 5월 10일</span><span class="sxs-lookup"><span data-stu-id="60ffb-191">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="60ffb-192">1.2.2</span><span class="sxs-lookup"><span data-stu-id="60ffb-192">1.2.2</span></span>](#1.2.2) |<span data-ttu-id="60ffb-193">2017년 4월 19일</span><span class="sxs-lookup"><span data-stu-id="60ffb-193">April 19, 2017</span></span> |--- |
| [<span data-ttu-id="60ffb-194">1.2.1</span><span class="sxs-lookup"><span data-stu-id="60ffb-194">1.2.1</span></span>](#1.2.1) |<span data-ttu-id="60ffb-195">2017년 3월 29일</span><span class="sxs-lookup"><span data-stu-id="60ffb-195">March 29, 2017</span></span> |--- |
| [<span data-ttu-id="60ffb-196">1.2.0</span><span class="sxs-lookup"><span data-stu-id="60ffb-196">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="60ffb-197">2017년 3월 25일</span><span class="sxs-lookup"><span data-stu-id="60ffb-197">March 25, 2017</span></span> |--- |
| [<span data-ttu-id="60ffb-198">1.1.2</span><span class="sxs-lookup"><span data-stu-id="60ffb-198">1.1.2</span></span>](#1.1.2) |<span data-ttu-id="60ffb-199">2017년 3월 20일</span><span class="sxs-lookup"><span data-stu-id="60ffb-199">March 20, 2017</span></span> |--- |
| [<span data-ttu-id="60ffb-200">1.1.1</span><span class="sxs-lookup"><span data-stu-id="60ffb-200">1.1.1</span></span>](#1.1.1) |<span data-ttu-id="60ffb-201">2017년 3월 14일</span><span class="sxs-lookup"><span data-stu-id="60ffb-201">March 14, 2017</span></span> |--- |
| [<span data-ttu-id="60ffb-202">1.1.0</span><span class="sxs-lookup"><span data-stu-id="60ffb-202">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="60ffb-203">2017년 2월 16일</span><span class="sxs-lookup"><span data-stu-id="60ffb-203">February 16, 2017</span></span> |--- |
| [<span data-ttu-id="60ffb-204">1.0.0</span><span class="sxs-lookup"><span data-stu-id="60ffb-204">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="60ffb-205">2016년 12월 21일</span><span class="sxs-lookup"><span data-stu-id="60ffb-205">December 21, 2016</span></span> |--- |
| [<span data-ttu-id="60ffb-206">0.1.0-preview</span><span class="sxs-lookup"><span data-stu-id="60ffb-206">0.1.0-preview</span></span>](#0.1.0-preview) |<span data-ttu-id="60ffb-207">2016년 11월 15일</span><span class="sxs-lookup"><span data-stu-id="60ffb-207">November 15, 2016</span></span> |<span data-ttu-id="60ffb-208">2015년 12월 31일</span><span class="sxs-lookup"><span data-stu-id="60ffb-208">December 31, 2016</span></span> |

## <a name="see-also"></a><span data-ttu-id="60ffb-209">참고 항목</span><span class="sxs-lookup"><span data-stu-id="60ffb-209">See Also</span></span>
<span data-ttu-id="60ffb-210">Cosmos DB에 대해 자세히 toolearn 참조 [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) 서비스 페이지.</span><span class="sxs-lookup"><span data-stu-id="60ffb-210">toolearn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span> 


---
title: "Cosmos DB aaaAzure 확장성 및 성능 테스트 | Microsoft Docs"
description: "Tooperform 확장 하는 방법을 알아보고 Azure Cosmos DB와 함께 성능 테스트"
keywords: "성능 테스트"
services: cosmos-db
author: arramac
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: f4c96ebd-f53c-427d-a500-3f28fe7b11d0
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: arramac
ms.openlocfilehash: 46d1217e11a39ee970a868de9a5c5dfcf52cedf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="performance-and-scale-testing-with-azure-cosmos-db"></a><span data-ttu-id="5d8ee-104">Azure Cosmos DB를 사용한 성능 및 규모 테스트</span><span class="sxs-lookup"><span data-stu-id="5d8ee-104">Performance and scale testing with Azure Cosmos DB</span></span>
<span data-ttu-id="5d8ee-105">성능 및 규모 테스트는 응용 프로그램 개발의 핵심 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="5d8ee-105">Performance and scale testing is a key step in application development.</span></span> <span data-ttu-id="5d8ee-106">대부분의 응용 프로그램에 대 한 hello 데이터베이스 계층에 상당한 영향을 전반적인 성능 및 확장성에 hello 및 따라서 성능의 주요 구성 요소 테스트 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5d8ee-106">For many applications, hello database tier has a significant impact on hello overall performance and scalability, and is therefore a critical component of performance testing.</span></span> <span data-ttu-id="5d8ee-107">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/)는 탄력적인 규모 및 예측 가능한 성능을 위해 작성되었으므로 고성능 데이터베이스 계층을 필요로 하는 응용 프로그램에 가장 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="5d8ee-107">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) is purpose-built for elastic scale and predictable performance, and therefore a great fit for applications that need a high-performance database tier.</span></span> 

<span data-ttu-id="5d8ee-108">이 문서는 개발자가 자신의 Cosmos DB 작업에 대한 성능 테스트 모음을 구현하거나 Cosmos DB에서 고성능 응용 프로그램 시나리오를 평가할 때 참조로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d8ee-108">This article is a reference for developers implementing performance test suites for their Cosmos DB workloads, or evaluating Cosmos DB for high-performance application scenarios.</span></span> <span data-ttu-id="5d8ee-109">이 hello 데이터베이스의 격리 된 성능 테스트에 주로 초점을 하지만 또한 프로덕션 응용 프로그램에 대 한 유용한 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d8ee-109">It focuses primarily on isolated performance testing of hello database, but also includes best practices for production applications.</span></span>

<span data-ttu-id="5d8ee-110">이 문서를 읽은 후 다음 질문 수 tooanswer hello 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d8ee-110">After reading this article, you will be able tooanswer hello following questions:</span></span>   

* <span data-ttu-id="5d8ee-111">Cosmos DB의 성능 테스트를 위한 샘플 .NET 클라이언트 응용 프로그램은 어디에서 찾을 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="5d8ee-111">Where can I find a sample .NET client application for performance testing of Cosmos DB?</span></span> 
* <span data-ttu-id="5d8ee-112">클라이언트 응용 프로그램에서 Cosmos DB를 사용하여 높은 처리량 수준을 달성하려면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="5d8ee-112">How do I achieve high throughput levels with Cosmos DB from my client application?</span></span>

<span data-ttu-id="5d8ee-113">코드로 시작 tooget hello 프로젝트를 다운로드 하세요 [Azure Cosmos DB 성능 테스트 샘플](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark)합니다.</span><span class="sxs-lookup"><span data-stu-id="5d8ee-113">tooget started with code, please download hello project from [Azure Cosmos DB Performance Testing Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark).</span></span> 

> [!NOTE]
> <span data-ttu-id="5d8ee-114">이 응용 프로그램의 hello 목표에는 적은 수의 클라이언트 컴퓨터와 더 나은 성능을 극대화 Cosmos DB을 추출 하기 위한 toodemonstrate 모범 사례입니다.</span><span class="sxs-lookup"><span data-stu-id="5d8ee-114">hello goal of this application is toodemonstrate best practices for extracting better performance out of Cosmos DB with a small number of client machines.</span></span> <span data-ttu-id="5d8ee-115">Limitlessly 확장 될 수 있는 hello 서비스의 toodemonstrate hello 최대 용량을 이루어지지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="5d8ee-115">This was not made toodemonstrate hello peak capacity of hello service, which can scale limitlessly.</span></span>
> 
> 

<span data-ttu-id="5d8ee-116">클라이언트 쪽 구성 옵션 tooimprove Cosmos DB 성능에 대 한 찾고 있는 경우 참조 [Azure Cosmos DB 성능 팁](performance-tips.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5d8ee-116">If you're looking for client-side configuration options tooimprove Cosmos DB performance, see [Azure Cosmos DB performance tips](performance-tips.md).</span></span>

## <a name="run-hello-performance-testing-application"></a><span data-ttu-id="5d8ee-117">Hello 성능 응용 프로그램 테스트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d8ee-117">Run hello performance testing application</span></span>
<span data-ttu-id="5d8ee-118">가장 빠른 방법은 tooget hello hello 단계 아래에 설명 된 대로 toocompile 및 아래 실행된 hello.NET 예제는 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d8ee-118">hello quickest way tooget started is toocompile and run hello .NET sample below, as described in hello steps below.</span></span> <span data-ttu-id="5d8ee-119">Hello 소스 코드를 검토 하 고 유사한 구성 tooyour 자체 클라이언트 응용 프로그램을 구현할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d8ee-119">You can also review hello source code and implement similar configurations tooyour own client applications.</span></span>

<span data-ttu-id="5d8ee-120">**1 단계:** 다운로드 hello 프로젝트에서 [Azure Cosmos DB 성능 테스트 샘플](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark), 또는 fork hello GitHub 리포지토리에 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d8ee-120">**Step 1:** Download hello project from [Azure Cosmos DB Performance Testing Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark), or fork hello GitHub repository.</span></span>

<span data-ttu-id="5d8ee-121">**2 단계:** EndpointUrl, AuthorizationKey, CollectionThroughput 및 DocumentTemplate (선택 사항) App.config에 대 한 hello 설정을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d8ee-121">**Step 2:** Modify hello settings for EndpointUrl, AuthorizationKey, CollectionThroughput and DocumentTemplate (optional) in App.config.</span></span>

> [!NOTE]
> <span data-ttu-id="5d8ee-122">높은 처리량을 사용 하 여 컬렉션을 프로 비전 하기 전에 toohello를 참조 하십시오 [가격 페이지](https://azure.microsoft.com/pricing/details/cosmos-db/) 컬렉션당 tooestimate hello 비용입니다.</span><span class="sxs-lookup"><span data-stu-id="5d8ee-122">Before provisioning collections with high throughput, please refer toohello [Pricing Page](https://azure.microsoft.com/pricing/details/cosmos-db/) tooestimate hello costs per collection.</span></span> <span data-ttu-id="5d8ee-123">Azure Cosmos DB 삭제 하거나 테스트 한 후 Azure Cosmos DB 컬렉션의 hello 처리량을 낮추면 하 여 비용을 저장할 수 있도록 저장소 및는 시간 단위로에서 독립적으로 처리량을 청구 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d8ee-123">Azure Cosmos DB bills storage and throughput independently on an hourly basis, so you can save costs by deleting or lowering hello throughput of your Azure Cosmos DB collections after testing.</span></span>
> 
> 

<span data-ttu-id="5d8ee-124">**3 단계:** 컴파일하고 hello 명령줄에서 hello 콘솔 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d8ee-124">**Step 3:** Compile and run hello console app from hello command line.</span></span> <span data-ttu-id="5d8ee-125">Hello 다음과 같은 출력이 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d8ee-125">You should see output like hello following:</span></span>

    Summary:
    ---------------------------------------------------------------------
    Endpoint: https://docdb-scale-demo.documents.azure.com:443/
    Collection : db.testdata at 50000 request units per second
    Document Template*: Player.json
    Degree of parallelism*: 500
    ---------------------------------------------------------------------

    DocumentDBBenchmark starting...
    Creating database db
    Creating collection testdata
    Creating metric collection metrics
    Retrying after sleeping for 00:03:34.1720000
    Starting Inserts with 500 tasks
    Inserted 661 docs @ 656 writes/s, 6860 RU/s (18B max monthly 1KB reads)
    Inserted 6505 docs @ 2668 writes/s, 27962 RU/s (72B max monthly 1KB reads)
    Inserted 11756 docs @ 3240 writes/s, 33957 RU/s (88B max monthly 1KB reads)
    Inserted 17076 docs @ 3590 writes/s, 37627 RU/s (98B max monthly 1KB reads)
    Inserted 22106 docs @ 3748 writes/s, 39281 RU/s (102B max monthly 1KB reads)
    Inserted 28430 docs @ 3902 writes/s, 40897 RU/s (106B max monthly 1KB reads)
    Inserted 33492 docs @ 3928 writes/s, 41168 RU/s (107B max monthly 1KB reads)
    Inserted 38392 docs @ 3963 writes/s, 41528 RU/s (108B max monthly 1KB reads)
    Inserted 43371 docs @ 4012 writes/s, 42051 RU/s (109B max monthly 1KB reads)
    Inserted 48477 docs @ 4035 writes/s, 42282 RU/s (110B max monthly 1KB reads)
    Inserted 53845 docs @ 4088 writes/s, 42845 RU/s (111B max monthly 1KB reads)
    Inserted 59267 docs @ 4138 writes/s, 43364 RU/s (112B max monthly 1KB reads)
    Inserted 64703 docs @ 4197 writes/s, 43981 RU/s (114B max monthly 1KB reads)
    Inserted 70428 docs @ 4216 writes/s, 44181 RU/s (115B max monthly 1KB reads)
    Inserted 75868 docs @ 4247 writes/s, 44505 RU/s (115B max monthly 1KB reads)
    Inserted 81571 docs @ 4280 writes/s, 44852 RU/s (116B max monthly 1KB reads)
    Inserted 86271 docs @ 4273 writes/s, 44783 RU/s (116B max monthly 1KB reads)
    Inserted 91993 docs @ 4299 writes/s, 45056 RU/s (117B max monthly 1KB reads)
    Inserted 97469 docs @ 4292 writes/s, 44984 RU/s (117B max monthly 1KB reads)
    Inserted 99736 docs @ 4192 writes/s, 43930 RU/s (114B max monthly 1KB reads)
    Inserted 99997 docs @ 4013 writes/s, 42051 RU/s (109B max monthly 1KB reads)
    Inserted 100000 docs @ 3846 writes/s, 40304 RU/s (104B max monthly 1KB reads)

    Summary:
    ---------------------------------------------------------------------
    Inserted 100000 docs @ 3834 writes/s, 40180 RU/s (104B max monthly 1KB reads)
    ---------------------------------------------------------------------
    DocumentDBBenchmark completed successfully.


<span data-ttu-id="5d8ee-126">**필요한 경우 4 단계:** hello 처리량 보고 (000RU/s) hello 도구에서 hello hello 컬렉션의 프로 비전 된 처리량 보다 높거나 같은 hello 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d8ee-126">**Step 4 (if necessary):** hello throughput reported (RU/s) from hello tool should be hello same or higher than hello provisioned throughput of hello collection.</span></span> <span data-ttu-id="5d8ee-127">그렇지 않은 경우 작은 단위로 증가 hello DegreeOfParallelism hello 제한에 도달 하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d8ee-127">If not, increasing hello DegreeOfParallelism in small increments may help you reach hello limit.</span></span> <span data-ttu-id="5d8ee-128">클라이언트 앱에서 hello 처리량 언덕이에 hello 응용 프로그램의 여러 인스턴스를 시작할 hello 동일 하거나 서로 다른 컴퓨터 서로 다른 인스턴스 간에 hello hello를 프로 비전 한도 도달 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d8ee-128">If hello throughput from your client app plateaus, launching multiple instances of hello app on hello same or different machines will help you reach hello provisioned limit across hello different instances.</span></span> <span data-ttu-id="5d8ee-129">이 단계에서 도움이 필요한 경우 전자 메일을 작성해 주세요, tooaskcosmosdb@microsoft.com hello에서 지원 티켓을 보관 또는 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="5d8ee-129">If you need help with this step, please, write an email tooaskcosmosdb@microsoft.com or file a support ticket from hello [Azure Portal](https://portal.azure.com).</span></span>

<span data-ttu-id="5d8ee-130">Hello 앱이 실행 중인를 만든 후 다른 시도할 수 [인덱싱 정책을](indexing-policies.md) 및 [일관성 수준](consistency-levels.md) toounderstand 처리량 및 대기 시간에 대 한 영향입니다.</span><span class="sxs-lookup"><span data-stu-id="5d8ee-130">Once you have hello app running, you can try different [Indexing policies](indexing-policies.md) and [Consistency levels](consistency-levels.md) toounderstand their impact on throughput and latency.</span></span> <span data-ttu-id="5d8ee-131">Hello 소스 코드를 검토 하 고 유사한 구성 tooyour 자체 테스트 도구 모음 또는 프로덕션 응용 프로그램을 구현할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d8ee-131">You can also review hello source code and implement similar configurations tooyour own test suites or production applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5d8ee-132">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5d8ee-132">Next steps</span></span>
<span data-ttu-id="5d8ee-133">이 문서에서는 .NET 콘솔 앱을 사용하여 Cosmos DB로 성능 및 규모 테스트를 수행하는 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="5d8ee-133">In this article, we looked at how you can perform performance and scale testing with Cosmos DB using a .NET console app.</span></span> <span data-ttu-id="5d8ee-134">Cosmos DB Azure 사용에 대 한 자세한 내용은 아래 toohello 링크를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="5d8ee-134">Please refer toohello links below for additional information on working with Azure Cosmos DB.</span></span>

* [<span data-ttu-id="5d8ee-135">Azure Cosmos DB 성능 테스트 샘플</span><span class="sxs-lookup"><span data-stu-id="5d8ee-135">Azure Cosmos DB performance testing sample</span></span>](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark)
* [<span data-ttu-id="5d8ee-136">클라이언트 구성 옵션 tooimprove Azure Cosmos DB 성능</span><span class="sxs-lookup"><span data-stu-id="5d8ee-136">Client configuration options tooimprove Azure Cosmos DB performance</span></span>](performance-tips.md)
* [<span data-ttu-id="5d8ee-137">Azure Cosmos DB의 서버 쪽 분할</span><span class="sxs-lookup"><span data-stu-id="5d8ee-137">Server-side partitioning in Azure Cosmos DB</span></span>](partition-data.md)


